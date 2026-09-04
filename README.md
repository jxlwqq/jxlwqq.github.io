# jxlwqq 的技术博客

这是一个使用 Jekyll 搭建并托管在 GitHub Pages 上的个人博客。

## 博客地址

访问 [https://jxlwqq.github.io](https://jxlwqq.github.io) 查看博客。

## 推荐文章

### [LLM 的「误刹」：复杂任务中模型为何过早宣布完成](https://jxlwqq.github.io/2026/09/04/how-llms-prematurely-declare-done/)

任务还没做完，模型却自信地写下了「所有测试已通过 ✅」。《LLM 的「刹车」》姊妹篇：拆解过早终止的五个成因——从 SFT 数据里的「完成文体」、局部完整的误判，到 RLHF 的自信偏好——并给出协议层、上下文工程与模型层的对应对策。

[全文阅读](https://jxlwqq.github.io/2026/09/04/how-llms-prematurely-declare-done/)

### [LLM 的「刹车」：下一个 Token 预测机如何知道何时停止](https://jxlwqq.github.io/2026/09/04/how-llm-knows-when-to-stop/)

大语言模型的本质是一台下一个 Token 预测机——每一步它能做的唯一事情，就是从词表里再挑出一个 Token，「不输出」根本不在选项里。那么，终止的信号是从哪一步、以什么形式冒出来的？本文结合 nanochat 源码，拆解模型层、协议层与运行时层如何协作，让一台永不停歇的预测机知道何时停止。

[全文阅读](https://jxlwqq.github.io/2026/09/04/how-llm-knows-when-to-stop/)

### [如何构建一个编码 Agent](https://jxlwqq.github.io/2025/12/14/how-to-build-a-coding-agent/)

本文将介绍如何构建一个编码 Agent。「Agent」一词如今已屡见不鲜。尽管这个术语被频繁提及，但许多人对其确切含义及编码 Agent 的内部运作机制仍缺乏清晰的理解。是时候揭开其神秘面纱，展示其技术门槛并非高不可攀。

[全文阅读](https://jxlwqq.github.io/2025/12/14/how-to-build-a-coding-agent/)

### [从零构建超迷你 ChatGPT：在 DGX Spark 上全流程训练 nanochat](https://jxlwqq.github.io/2025/12/05/nanochat-training/)

Andrej Karpathy 最近开源了 nanochat 项目，号称花 100 美元就能从零训出一个能聊天的模型。正好手边有台 DGX Spark，于是决定跑一遍完整流程，顺便记录下来。

[全文阅读](https://jxlwqq.github.io/2025/12/05/nanochat-training/)

