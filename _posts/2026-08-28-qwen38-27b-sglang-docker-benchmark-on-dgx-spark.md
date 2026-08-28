---
layout: post
title: "Qwen3.8-27B SGLang Docker 部署测速报告（GB10 / DGX Spark）：NVFP4 vs BF16 × EAGLE 开关"
date: 2026-08-28 12:00:00 +0800
categories: ai dgx-spark sglang llm-inference benchmark qwen
---

* TOC
{:toc}

测试日期：2026-08-28

SGLang 官方 cookbook 给出了 Qwen3.8-27B 在 DGX Spark 上的完整启动配方（48 种组合全部验证过"能启动、能服务"），但**没有给出任何吞吐数据**——DGX Spark 是该页面上唯一只做了 boot-and-serve 验证的硬件。本文用实际的 Docker 部署 + curl 流式调用补上这块空白：两个 checkpoint（NVFP4 量化 / BF16 原版）× 两种推测解码（EAGLE 开 / 关），共 4 组配置，覆盖短上下文、8K、23K 三种输入规模和 4 路并发。

## 1. 测试环境

| 项目 | 配置 |
|---|---|
| GPU | NVIDIA GB10（DGX Spark，aarch64，sm_121，128GB LPDDR5x 统一内存，官方标称带宽 273GB/s） |
| 驱动 | 580.173.02（CUDA 13.0）；`nvidia-smi` 显存栏显示 Not Supported（与 CPU 共享） |
| CPU / 内存 | 20 核 ARM（10× Cortex-X925 + 10× Cortex-A725）；系统总内存 127.6GB |
| SGLang | 0.0.0.dev0+qwen38.27b.g561c8f3（`lmsysorg/sglang:qwen38-27b` 镜像，Docker 部署） |
| torch / flashinfer | 2.13.0+cu130 / 0.6.18（满足 MTP + FlashInfer 所需的 uniform_q_len 支持） |
| 部署方式 | `make run` / `make run-eagle`（Makefile 封装 `docker run --gpus all --shm-size 32g --ipc=host`） |

## 2. 部署方式（SGLang Docker）

启动参数完全对齐 [官方 cookbook 的 DGX Spark 低延迟配方](https://docs.sglang.io/cookbook/autoregressive/Qwen/Qwen3.8-27B)：EAGLE（3 步 / topk 1 / 4 draft tokens）+ `--enable-linear-replayssm-spec` + `--mamba-full-memory-ratio 4.59` + `extra_buffer` + SSM float32 + KV fp8_e4m3 + flashinfer。Makefile 里的两个核心 target：

| target | 关键差异 |
|---|---|
| `make run` | 基础服务，无推测解码，`--mem-fraction-static 0.85` |
| `make run-eagle` | 在基础参数上追加 `--speculative-algorithm EAGLE --speculative-num-steps 3 --speculative-eagle-topk 1 --speculative-num-draft-tokens 4 --enable-linear-replayssm-spec` |

几点部署相关的实测/对照信息：

* 术语澄清：被开关的技术是**推测解码（Speculative Decoding）**；EAGLE 是 SGLang 中该技术的算法实现，NEXTN 是它的旧名/别名（cookbook 明确两者等价）；而 **MTP 头不是算法本身，是 checkpoint 内置的草稿权重**——EAGLE 运行时用它充当草稿模型，一次猜多个 token、主模型一次前向并行验证，因此无需单独下载 draft checkpoint（BF16 checkpoint 加载时能看到单独的 `Qwen3_5ForCausalLMMTP`，约 4.9GB）。"关闭推测解码"即回到逐 token 的纯自回归解码。
* `--mem-fraction-static 0.85` 在 DGX Spark 上有 earlyoom 风险（cookbook 的 48 格矩阵中 15 格在 0.85 被系统 OOM 守护进程以 -15 杀掉），官方 DGX Spark 配方定在 **0.80**。本文 NVFP4 组沿用本机 Makefile 默认 0.85（实测多次启停稳定），BF16 组按官方建议用 0.80。
* 开启推测解码时若不显式设置 `--max-running-requests`，SGLang 会固定为 48（本机实测 NVFP4+EAGLE = 48，关闭推测后按显存自动算出 79）。

## 3. 模型文件

| 路径 | 格式 | 大小 | 来源 | 加载耗时 |
|---|---|---|---|---|
| RadixArk/Qwen3.8-27B-NVFP4 | NVFP4 W4A4（FP8 注意力投影，FP4 lm_head，内置 MTP 头） | 21G | ModelScope | ~110s |
| Qwen/Qwen3.8-27B | BF16 原版（18 个分片，含 MTP 头） | 52G | ModelScope | ~295s |

两个模型主体权重结构相同（64 层：48 层 Gated DeltaNet 线性注意力 + 16 层 GQA 全注意力），差异只在量化和 lm_head 打包方式，是同一架构下"精度换带宽"的直接对照。

## 4. 测速方法

用 `curl -sN` 流式调用 `/v1/chat/completions`（SSE），`stream_options.include_usage` 拿服务端 token 计数，`temperature 0`、`ignore_eos true` 固定输出长度。指标定义：

* **TTFT**：从发请求到收到首个内容块
* **Prefill** = prompt_tokens / TTFT（只取冷缓存首跑，避免 radix cache 命中后虚高）
* **Decode** = (completion_tokens - 1) / (末 token 时刻 - 首 token 时刻)

| 场景 | 输入（服务端计数） | 输出 |
|---|---|---|
| 短上下文 | 251 tokens | 256 |
| 8K 级 | 5,802 tokens | 1,024 |
| 23K 级 | 22,821 tokens | 512 |
| 并发 | 5,802 tokens × 4 路 | 512 × 4 |

每组跑 3 遍取后 2 遍的稳态值（首跑含冷启动单独标注）；thinking 模式保持默认开启。服务端日志的 `gen throughput` 与客户端聚合值相互印证（如 4 并发时服务端 84~88 tok/s vs 客户端 83~85 tok/s）。

## 5. 测试结果

### 5.1 单流 Decode 速度（tok/s）

| 配置 | 短上下文 | 8K 级 | 23K 级 |
|---|---|---|---|
| **NVFP4 + EAGLE** | **28.7** | **23.7** | **25.5** |
| NVFP4 | 14.0 | 12.0 | 14.2 |
| BF16 + EAGLE | 11.3 | 11.2 | 11.0 |
| BF16 | 4.85 | 4.15 | 4.87 |

* EAGLE 带来的加速：NVFP4 上 **1.8~2.1×**，BF16 上 **2.3~2.7×**（8K 处收益最大）。服务端统计的平均接受长度：NVFP4 2.69/4 步，BF16 2.85/4 步。
* NVFP4 对 BF16 的加速：关闭推测解码时 **2.9×**，开启后 **2.1×**（EAGLE 摊薄了读取权重的开销，量化优势被部分抹平）。
* 带宽模型验证：273GB/s ÷ 21GB ≈ 13 tok/s（NVFP4 理论上限），273GB/s ÷ 52.9GB ≈ 5.2 tok/s（BF16），与实测 12.0 和 4.15~4.87 基本吻合——**单流 decode 就是权重带宽的物理极限**，与此前另一份 GB10 测速报告"~23 tok/s 天花板"（NVFP4+NEXTN 达 23.02）的结论一致，本文同配方实测 23.7~25.5。

### 5.2 TTFT 与 Prefill

| 配置 | 短上下文 TTFT | 8K TTFT（冷/暖） | Prefill 冷缓存（8K / 23K） |
|---|---|---|---|
| **NVFP4 + EAGLE** | **1.6~2.1s** | 4.2s / 2.7s | **1,394 / 1,787** |
| NVFP4 | 3.4~3.8s | 7.0s / 4.5s | 831 / 1,453 |
| BF16 + EAGLE | 3.9~4.2s | 9.5s / 5.3~6.0s | 613 / 1,230 |
| BF16 | 10.4~11.0s | 16.0s / 11.8s | 363 / 919 |

* BF16 短上下文的首 token 也要 10 秒上下，NVFP4 只要约 2 秒——长 prompt 的 prefill NVFP4 快 1.7×，短请求的固定开销差 5×。
* 长输入下 chunked prefill 摊薄了每块固定开销，各配置的 23K prefill 都高于 8K（NVFP4+EAGLE 冷缓存能到 ~1.8K tok/s）。
* radix cache 暖机后重复请求 TTFT 明显下降（如 NVFP4+EAGLE 8K 从 4.2s 降到 2.7s），但此时"prefill 速率"读数含缓存命中成分，不具可比性，故表中只列冷缓存值。

### 5.3 并发测试（5.8K 输入，4 路并发 × 512 输出）

| 配置 | 每路 decode | 聚合 decode |
|---|---|---|
| **NVFP4 + EAGLE** | **24.2~24.9** | **83~85** |
| NVFP4 | ~11.9 | 42.0 |
| BF16 + EAGLE | 10.1~10.9 | 35.6~36.6 |
| BF16 | 4.76~4.83 | 17.6 |

* 最意外的结果：**NVFP4 + EAGLE 在 4 并发下单路速度几乎不掉**（24.9 vs 单流 23.7），推测解码的 draft/verify 随 batch 摊销得很好；聚合吞吐达到单流的 3.5×。
* BF16 关闭推测解码时批处理几乎"免费"：每路 4.8 ≈ 单流 4.85，聚合约线性扩展（17.6 ≈ 4.15 × 4.2）——纯带宽瓶颈下多路只是把权重读取摊给更多请求。
* 对照 cookbook 的警告：推测解码会把 `max-running-requests` 重置为 48，本机 NVFP4+EAGLE 实测 KV 池 37.5 万 token、上限 48 路，4 并发只用了 KV 池的 2%。

### 5.4 内存与 KV 池

| 配置 | 权重 | KV 池（max_total_num_tokens） | max_running_requests |
|---|---|---|---|
| NVFP4 + EAGLE | 21G | 374,793 | 48（spec 固定） |
| NVFP4 | 21G | **413,359** | 79（自动） |
| BF16 + EAGLE | 52G + 4.9G（MTP） | 174,718 | 32 |
| BF16 | 52G | 204,597 | 39（自动） |

NVFP4 把 31GB 的权重差省下来给了 KV 池：同等 `mem-fraction` 下可用上下文容量是 BF16 的约 2 倍（41.3 万 vs 20.5 万 token，均远超模型原生的 262K 上下文）。

## 6. 结论

1. **推荐组合：NVFP4 + EAGLE（`make run-eagle` 默认配置）**。单流 24~29 tok/s，4 并发聚合 84 tok/s 且单路体验不掉速，KV 池 37.5 万 token，加载仅 110 秒——在 GB10 上是速度、容量、启动时间的全面最优。
2. **BF16 原版不适合做常驻服务**：单流 4~5 tok/s、短请求 TTFT 10 秒起步；但它的价值在于给出带宽物理上限的干净参照（4.15 ≈ 273GB/s ÷ 52.9GB），以及验证 EAGLE 输出分布不受推测解码影响。
3. **EAGLE/MTP 是 DGX Spark 上的必选项**：两个 checkpoint 上都是 1.8~2.7× 加速，接受长度 2.69~2.85/4 且并发下不衰减；BF16 受益更大（权重读取每步摊薄近 3 倍）。
4. **量化的收益在推测解码面前缩水**：NVFP4 对 BF16 的单流优势从关闭推测解码时的 2.9× 降到开启后的 2.1×——EAGLE 本质上是"用一次权重读取换 2.7 个 token"，与量化的省钱逻辑同向叠加但有边际。
5. 单流 decode 天花板由 273GB/s 内存带宽锁死，与模型/引擎优化无关；想再快只能换更大的 spec 模型或期待硬件换代，23K 长上下文的 prefill 反而还有优化空间（chunk 8192 等参数未在本文展开）。

## 7. 过程中的环境备忘

* `nvidia-smi` 在 GB10 上显存栏是 Not Supported（统一内存），判断能否再起一个容器要看 `/proc/meminfo` 的 MemAvailable，而不是 nvidia-smi。
* `--mem-fraction-static 0.85` + BF16 是 earlyoom 高危组合（cookbook 实测 15/48 格被杀，exit -15 无 traceback），DGX Spark 上建议 0.80；本文 NVFP4@0.85 多次启停未复现被杀。
* 推测解码未显式设置 `--max-running-requests` 时会被固定为 48，关闭推测后本机自动算出 79——做并发压测前先确认这个隐含上限。
* 官方 cookbook 对 DGX Spark 的 48 格矩阵只做了 boot-and-serve 验证（ISL 8192 / OSL 1024、并发 1，无吞吐数据）；RTX 5090 / RTX PRO 6000 才有完整性能数字，本文数据可用于填补 DGX Spark 这一格。
* 镜像 `lmsysorg/sglang:qwen38-27b`（sglang g561c8f3 + flashinfer 0.6.18）满足 MTP + FlashInfer 对 uniform_q_len 的版本要求，无需退回 triton 后端。

## 参考

* [SGLang Cookbook: Qwen3.8-27B](https://docs.sglang.io/cookbook/autoregressive/Qwen/Qwen3.8-27B)（官方部署配方与 DGX Spark 验证说明）
* [Qwen3.8-27B 部署测速报告（GB10 / DGX Spark）- 阿里云开发者社区](https://developer.aliyun.com/article/1756323)（同硬件、同配方家族的第三方数据，单流 23.02 tok/s）
