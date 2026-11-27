---
layout: post
title: "像编排容器一样编排 Session：企业级 AI Agent 平台核心架构"
date: 2026-11-27 11:30:00 +0800
categories: ai agent architecture platform
---

* TOC
{:toc}

在[《如何构建一个编码 Agent》](/2025/12/14/how-to-build-a-coding-agent/)里，一个能跑起来的编码 Agent 核心只有 300 行代码，在一个循环里消耗 Token、调工具。

放到企业生产环境里，多人共用、沙箱隔离、调内部业务接口、跨会话记东西，每一块都会把那 300 行循环撑破。把外围的对象存储网关、离线评测和运营监控先拿掉，这套 Agent 平台的架构主线其实就一句话：像编排调度容器一样编排调度 Session。

Kubernetes 把 Pod 当作最小调度单元，用控制面、节点代理（`kubelet`）和运行时接口（CRI）把编排与执行彻底分开。这里把最小调度单元换成了 Session：入口层、主控层、沙箱底座和运行时抽象层几乎与 Kubernetes 同构。不同之处在于，Session 会调用企业内部接口，也需要在会话结束后留下长期经验，所以平台在编排骨架之外补上了工具网关和记忆服务两块 Agent 原生底座。

## 一、整体分层

整套设计守住四条边界：控制面不跑模型循环，算力隔离与运行时解耦，内部接口统一走网关，沙箱内不直连记忆服务也不存业务密钥。

![企业级 AI Agent 平台核心架构](/assets/images/enterprise-agent-platform-architecture/architecture-overview.png)

各层之间通过 REST、SSE、WebSocket、ACP、MCP 和 Kubernetes CRD 通信，彼此不共享数据库。对照 Kubernetes 的分层来看，六个核心组件的定位非常直接：

| 层级 | 组件 | K8s 类比 | 技术栈 | 职责 |
| --- | --- | --- | --- | --- |
| 入口层 | `Agent Web` / `AgentCtl` / `SDK` | Dashboard / `kubectl` / Client SDK | React / Rust / 多语言 SDK | 承接人、终端与业务系统三类请求，统一进入控制面 |
| 主控层 | `Agent Manager` | Control Plane (API Server / Scheduler / Reconciler) | Go | 管理资产、权限、会话编排、记忆预装配与沙箱调度 |
| 沙箱底座 | `agent-sandbox` | Node / 算力节点 | Go / Kubernetes CRD | 基于开源 `kubernetes-sigs/agent-sandbox`，以 CRD 管理运行时 Pod 的身份、存储与隔离 |
| 运行时抽象与镜像 | `Agentlet` + ACP Runtimes + 统一镜像 | `kubelet` + CRI + `containerd` + 容器镜像 | Go + ACP / Rust | 运行在沙箱内的节点代理，依托 All-in-One 镜像和 ACP 协议纳管 `Claude Code`、`Codex` 与 OpenCode 的 Rust 实现 |
| 工具接入层 | `MCP Gateway` | Agent 原生扩展 | Java / Spring Boot | 把企业内部微服务 API 收口为标准 MCP Tool，统一做鉴权、风控与审计 |
| 记忆层 | `Agent Memory` | Agent 原生扩展 | Python / Mem0 / Qdrant | 提供跨会话、按组织树继承的长期记忆存储、混合检索与异步蒸馏 |

## 二、入口层：Agent Web、AgentCtl 与 SDK

企业里调用 Agent 的有三种角色，入口层对应分成三个客户端。

`Agent Web` 给人用，负责 Agent 编排、Skill、Prompt 和 MCP 资产管理，以及对话和审批界面。权限判断全放在后端，接口返回节点能力位，前端只按能力位决定按钮能不能点。

`AgentCtl` 是 Rust 写的单文件 CLI，命令风格贴近 `kubectl`，既给研发管理平台资源，也给 AI 编码代理自己调企业工具。为了省 Context Token，工具调用拆成 `search → get → call` 三步：搜索只返回工具名和简短描述，选定之后再拉完整的 `inputSchema`。输出契约偏向机器解析，stdout 只吐数据，stderr 只吐单行 JSON 错误，退出码按未登录、无权限、参数错误、网关暂不可达细分。CLI 刻意不提供 `--yes` 之类的本地跳过参数，高危操作一律在服务端拦住。

`SDK` 给企业内部业务系统用，封装了非流式对话、SSE 流式对话和会话状态接口。流式调用的重试边界划得很死：建连阶段可以按配置重试，一旦 SSE 响应头交给业务回调就禁止自动重试，避免业务收到两段重复文本、后台 Agent 被重复触发。业务方如果要把终端用户的邮箱、SSO Token、租户或记忆维度传给下游工具，SDK 会用公钥把这些字段加密进单个 `Agent-Business-Context` 请求头，避免明文凭据流经沙箱和模型上下文。

## 三、主控层：Agent Manager

`Agent Manager` 用 Go 编写，管着 Agent 定义与版本、Skill 与 Prompt 目录、模型配置、多租户权限、IM 与定时渠道，以及引擎池和会话生命周期。

架构上最重要的一条约束是：`Agent Manager` 只管编排、路由和状态，绝不在控制面进程里跑 LLM 循环或执行工具。

这样拆开后，控制面日常发版不会打断正在跑长任务的会话，单个执行节点挂掉也不会拖垮管理后台。收到请求时，控制面从关系型数据库里捞出 Prompt、绑定的 Skills、模型配置和授权 MCP 列表，再按场景去记忆服务拉好上下文，整包装配完调度给空闲的沙箱节点。

## 四、沙箱底座：agent-sandbox

把 Agent 运行时直接丢进普通的 Kubernetes `Deployment` 或 `StatefulSet`，用一段时间就会碰到几个绕不开的问题。`Deployment` 面向无状态副本，没有单实例稳定身份、独立持久工作目录和休眠恢复语义，很难支持按 Agent 独占绑定的长会话。`StatefulSet` 的副本按 `0, 1, 2...` 顺序编排，想把中间某个空闲或解绑的专属实例单独删掉非常别扭，也没法直接做高并发认领池。

平台因此直接引入了 Kubernetes SIG Apps 孵化的开源项目 [`kubernetes-sigs/agent-sandbox`](https://github.com/kubernetes-sigs/agent-sandbox)。

生产主链路上，`Agent Manager` 里的 `SandboxManager` 直接通过 `agents.x-k8s.io` clientset 管理集群里的 `Sandbox` CR，给每个运行时实例分配稳定的网络身份和持久化工作目录，同时支持共享引擎池和按 Agent 独占绑定两种模式。缩容或回收节点时，控制面先原子地把节点状态改成 `draining`，停掉新会话派发，等在途任务全部结束再删对应的 `Sandbox` CR。

在这个核心 CRD 之上，`agent-sandbox` 开源生态还自带 `SandboxTemplate`、`SandboxWarmPool` 和 `SandboxClaim`（预热池秒级认领，用来压低冷启动），并能通过 Kubernetes `RuntimeClass` 把内核和网络隔离交给 gVisor 或 Kata Containers，后续做强隔离执行可以直接沿这套标准扩展。

## 五、运行时抽象与镜像环境：Agentlet、ACP 与统一镜像

`agent-sandbox` 负责把 Pod 拉起来，跑在 Pod 里面跟 `Agent Manager` 对话的是 `Agentlet`。

类比 Kubernetes 的分层：`kubelet` 通过 CRI 屏蔽底层容器运行时，这里用 `Agentlet` 配合 ACP（Agent Client Protocol）协议，把控制面调度和底层各种 Agent Runtime 隔开。

### 5.1 用统一契约收敛多类 Runtime

Sandbox Pod 启动后，`Agentlet` 主动向 `Agent Manager` 反向注册，上报本机可用的运行时列表和负载心跳。往下按运行时是否原生支持标准 ACP 分两条路，统一收敛到 `Agentlet` 的运行时契约（ARI）里：

- 自研主力多租户引擎（OpenCode 的 Rust 实现）：`Agentlet` 走 HTTP Provision 加 ACP-v1/WebSocket 协议，早期的直连 HTTP/SSE 路径已经彻底删掉。
- 原生支持 ACP 的代理（如 OpenCode CLI）：直接以 `<bin> acp` 启动标准 ACP stdio 服务。
- `Claude Code` 与 `Codex`：官方 CLI 原生不支持标准 ACP，Claude 走 `stream-json` over stdio，Codex 走自家的 `app-server` JSON-RPC。平台在 `Agentlet` 里用内置 Go SDK 直接驱动它们并实现同一套运行时契约。

这里踩过一个值得记下来的协议取舍：早期尝试过给 Claude 和 Codex 强行套一层进程内的 ACP Facade，让所有引擎都走标准 ACP 管道。但标准 ACP 的 `session/new` 和 `session/prompt` 是按「编辑器对接 Agent」设计的，放不下平台多租户调度需要的参数（比如按会话隔离的 `CODEX_HOME`、语义无进展超时预算、service tier 和 thinking level），在协议边界手写字段映射还曾静默漏掉 8 个配置项。最终改成原生支持 ACP 的走 ACP、走私有协议的由内置 SDK 直接对接 `Agentlet` 契约，上层控制面和业务方切 Runtime 依然只需要改配置，不用动调度代码。

### 5.2 把 OpenCode 用 Rust 重写

平台主力多租户引擎本质上是 OpenCode 的 Rust 实现。早期直接拿 TypeScript/Bun 的单用户 CLI 改造成服务端引擎，跑上多租户并发后很快暴露了运行时瓶颈：单 JS 线程互相阻塞、V8 GC 停顿拖慢 SSE 推送、全进程共享单文件 SQLite 写锁打架，MCP 连接也没法复用，断连后工具直接消失。

团队在保留 OpenCode 能力语义的前提下，用 Rust 和 Tokio 重写了一遍，把存储改成 per-session 独立 SQLite，补上 MCP 工具缓存、断连自动恢复和多租户子任务公平排队，单节点表现拉开了一个量级：

| 指标 | 旧引擎 (TS / Bun 单用户改造) | 自研 Rust Runtime (OpenCode Rust 实现) |
| --- | --- | --- |
| 单 Pod 稳定并发 | ~15 Sessions | 100+ Sessions |
| 进程内存基线 | ~120 MB (V8 堆) | ~8 MB (无 GC) |
| 冷启动耗时 | ~800 ms | ~50 ms |
| 存储与并发隔离 | 全进程单文件 SQLite、单线程共享 | per-session 独立 SQLite、Tokio 多线程隔离 |

因为上层只认 `Agentlet` 和 ACP，这次引擎替换对控制面和前端没有造成改动。

### 5.3 All-in-One 镜像与滚动更新

沙箱容器采用 All-in-One 统一镜像，底层基于预装 Python/Conda 和 Node LTS 的基础镜像，方便沙箱里直接跑数据分析、用户脚本和 Skill 工具链。镜像里同时装好 `Agentlet`（用 `exec` 作为 PID 1，直接接 `SIGTERM` 做优雅排空）以及 `Claude Code`、`Codex` 和 OpenCode Rust 实现三个二进制。同一套引擎池能按会话配置动态选 Runtime，省去了为每种引擎单独维护镜像和算力池的麻烦。

所有运行时和工具都先沉淀到企业内网制品库，构建时锁定不可变版本，不用 `:latest`。各家 CLI 一律弃用 npm loader，改用官方原生二进制。之前踩过一个很具体的坑：npm loader 版的 CLI 光跑一次 `--version` 就要 14 秒以上，直接打爆 `Agentlet` 启动期 10 秒的版本探针，导致节点拒绝注册该 Runtime；换成原生二进制后降到 0.05 秒。

受管容器镜像目录和引擎池模板由 `Agent Manager` 统一维护。基础环境或 Runtime 升级时，Reconciler 结合前面提到的 `draining` 排空机制，自动把集群里的 Sandbox 节点逐批滚完。

## 六、工具接入层：MCP Gateway

企业里的业务接口动辄成百上千，如果让每个 Agent 自己拼 HTTP 请求、管 Token、写审计，维护和安全都会失控。`MCP Gateway`（Java / Spring Boot）作为统一工具网关，把内部微服务 API 转成标准 MCP Tool 暴露出来。

网关对外只开一个 `/mcp` 端点，支持 Streamable HTTP 以及基于 `Last-Event-ID` 的 SSE 断线重放。`tools/list` 按 `tags` 场景标签和权限策略动态裁剪返回结果，避免把几百个接口 Schema 一次灌进模型上下文。工具元数据存 MySQL，加一层本地内存和 Redis 缓存支持热刷新。下游接口的认证方式（Bearer、Basic、API Key、OAuth2）、请求体编码、参数映射和响应提取（JSONPath、JSON Pointer）全部做成可配置策略，业务方接内部接口不用写胶水代码。

安全层面，网关内置 ABAC 权限校验和四级风险分级（`LOW`、`MEDIUM`、`HIGH`、`CRITICAL`），高危写接口可以强制拦截或要求人工确认（Human-in-the-Loop），所有调用异步落盘三层审计日志。入口 SDK 加密传进来的 `Agent-Business-Context` 请求头，穿过沙箱和执行引擎期间一直保持密文，直到 `MCP Gateway` 这一跳才还原，按模板变量塞进下游微服务的请求头或参数里。

## 七、记忆层：Agent Memory

没有记忆服务的 Agent，每次新开会话都得重新交代一遍背景和团队规范。`Agent Memory`（Python / FastAPI / Mem0 / Qdrant / MySQL）把长期记忆独立出来，同时支持 REST 和可选 MCP 接口。

记忆按一棵 N 级组织树组织（如 `company → bu → dept → center → team → personal`），并覆盖 Agent、代码仓库、群聊等多个维度，再用 `scene` 把 IM 群聊和平台对话这类不同场景隔开。检索时跨维度多路扇出，在 Qdrant 里同时做语义向量和 BM25 稀疏检索，部分分片失败时降级返回不拖垮整次查询。记忆内容分为四类：`directive`（红线指令）、`procedural`（流程 SOP）、`semantic`（事实知识）和 `episodic`（历史经历）。排序权重按类型和组织深度做插值，指令类偏向根节点（公司规范压过个人习惯），经历类偏向叶节点（个人最近一次排障比半年前的记录更优先）。

存储一致性上，服务明确以 Mem0/Qdrant 为主数据面，MySQL 只做备份投影、审计历史和恢复账本。写入不走同步双写，而是走 Write Intent Log（写入意图日志）：先落一条带幂等键的意图记录，再写 Mem0/Qdrant，最后异步更新 MySQL 投影；遇到超时或未知状态，由后台 Worker 按状态机查证恢复。

接入方式按会话阶段分成三段，确保沙箱里不直连记忆服务：

- 会话前：`Agent Manager` 在 Session Provision 阶段按用户和 `scene` 从 `Agent Memory` 拉取记忆清单，随会话上下文一并下发。
- 运行中：Runtime 本地只维护工作目录里的 `Agent.md`。如果推理过程中需要主动查或写组织记忆，统一调 `MCP Gateway` 暴露的 Memory 工具，沙箱进程本身不持有记忆服务的密钥。
- 会话后：`Agent Memory` 的 `Session Dream` 后台任务定时扫描静默结束的会话存储，异步抽取高价值经验回写记忆库，敏感维度叠加隐私门禁和人工审批。

## 八、一次完整请求的流转

![一次完整对话请求的端到端流转](/assets/images/enterprise-agent-platform-architecture/request-flow.png)

整条链路上，控制面负责配置装配、记忆预拉取和沙箱调度；沙箱里的 `Agentlet` 和 Runtime 只管推理与本地执行，既不直连内部业务接口，也不持有记忆服务密钥；所有对企业内部系统与组织记忆的访问都收口在 `MCP Gateway`。
