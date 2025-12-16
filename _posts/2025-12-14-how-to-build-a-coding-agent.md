---
layout: post
title: "如何构建一个编码 Agent"
date: 2025-12-14 12:00:00 +0800
categories: ai coding-agent
---

> 原文链接：[How to build a coding agent: free workshop](https://ghuntley.com/agent/)
> 
> 作者：Geoffrey Huntley

![how to build a coding agent: free workshop](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.001.jpg)

本文将介绍如何构建一个编码 Agent。「Agent」一词如今已屡见不鲜。

尽管这个术语被频繁提及，但许多人对其确切含义及编码 Agent 的内部运作机制仍缺乏清晰的理解。是时候揭开其神秘面纱，展示其技术门槛并非高不可攀。

学习如何构建编码 Agent 是 2025 年个人发展中最具价值的投资之一，因为它能让你掌握核心基础。一旦理解了这些基础知识，你将从 AI 的消费者转变为 AI 的生产者，具备利用 AI 实现自动化的能力。

让我们从以下事实开始：

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.002.png)

<p class="text-center">这并不难</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.003.png)

<p class="text-center">构建一个编码 Agent</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.004.png)

<p class="text-center">只有 300 行代码</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.005.png)

<p class="text-center">在一个循环中运行</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.006.png)

<p class="text-center">使用 LLM token，这就是全部。</p>

仅需 300 行代码在一个循环中运行，消耗 LLM token。只要持续向循环中输入 token，你就拥有了一个 Agent。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.007.png)

本文将指导你构建一个 Agent，并解释其基本工作原理。在 2025 年，与 AI 协同工作已成为常态。因此，演示这一点的最佳方式莫过于让一个 Agent 来协助构建另一个 Agent。

现在，我们开始构建一个 Agent。这是行业正在发生的变革之一：工作可以并发进行，甚至在你离开电脑时也能持续推进。

花费数天甚至一周时间进行研究冲刺的日子已成过去，如今你只需通过语音指令即可将想法转化为执行。

下次在 Zoom 通话时，不妨思考一下：你本可以让一个 Agent 在通话期间完成你计划中的工作。如果这对你来说尚非常态，而你的同事却已习以为常，那么你将难以保持领先优势。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.009.png)

<p class="text-center">请构建你自己的</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.010.png)

<p class="text-center">因为这些知识</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.011.png)

<p class="text-center">将改变你</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.012.png)

<p class="text-center">从消费者</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.013.png)

<p class="text-center">变成生产者</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.014.png)

<p class="text-center">能够自动化事务</p>

科技行业犹如一条不断前行的传送带，要求我们持续学习新知。

在 2025 年，你应熟悉如何创建一个 Agent。理解这一循环机制以及如何构建 Agent，已成为雇主在招聘时寻找的基础技能。

[Yes, You Can Use AI in Our Interviews. In fact, we insist - Canva Engineering Blog](https://www.canva.dev/blog/engineering/yes-you-can-use-ai-in-our-interviews/)

因为这些知识将助你从 AI 的消费者转变为能够编排工作流程的 AI 生产者。雇主如今更青睐那些能够在组织内部实现任务自动化的个人。

关于这一点的深入探讨，可参考以下内容：

[the six-month recap: closing talk on AI at Web Directions, Melbourne, June 2025](https://ghuntley.com/six-month-recap/)

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.015.png)

此刻，你正处于上述旅程的某个阶段。

在左上角，有些人持怀疑态度：「向我证明这不是真的」、「给我看结果」、「证明这不是炒作」，或者认为「这还不够好」。他们被困在悬崖的一侧，完全忽视了在悬崖的另一边，已有人在完全自动化他们的工作职能。

> 在我看来，任何与 AI 相关的颠覆或失业并非 AI 本身所致，而是缺乏个人发展和自我投资的后果。如果你的同事在多个 Agent 之间切换，处理想法，并在会议期间让 Agent 在后台运行，而你却置身事外，那么落后是必然的。

[What do I mean by some software devs are “ngmi”?](https://ghuntley.com/ngmi/)

切勿成为滞留在悬崖左侧的人。

科技行业的传送带持续向前。如果你是 2025 年的 DevOps 工程师，却没有任何 AWS 或 GCP 的经验，那么你会发现就业市场举步维艰。

软件和数据工程师惊讶于这一切发生得如此之快。自第一个编码 Agent 发布以来仅八个月，大多数人仍未意识到构建它是多么简单，这个循环是多么强大，以及它对我们职业产生的颠覆性影响。

所以，我叫 Geoffrey Huntley。我曾是 Canva 的开发者生产力技术主管，但几个月前，我成为了 Sourcegraph 构建 [Amp](https://ampcode.com/) 的工程师之一。这是一个大约六人的核心小团队。我们用 AI 构建 AI。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.016.png)

<p class="text-center">ampcode.com</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.017.png)

<p class="text-center">cursor</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.018.png)

<p class="text-center">windsurf</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.019.png)

<p class="text-center">claude code</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.020.png)

<p class="text-center">github co-pilot</p>

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.022.png)

<p class="text-center">都是在 LLM token 循环中运行的代码行。</p>

Cursor、Windsurf、Claude Code、GitHub Copilot 和 Amp 只是在 LLM token 循环中运行的一小部分代码。需要强调的是：模型在此完成了所有繁重的工作。是模型驱动了一切。

你可能正在评估多家供应商的产品，试图比较这些 Agent。但这实际上是在做无用功。

构建属于你自己的 Agent 其实非常简单……

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.023.png)

你只需要了解几个关键概念。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.024.png)

并非所有 LLM 都是 Agentic（代理式）的。

正如汽车有不同类型——越野时选择 [40 系列](https://en.wikipedia.org/wiki/Toyota_Land_Cruiser_(J40))，载客时选择轿车一样。

同样的原则也适用于 LLM，我们可以将它们的行为映射到一个象限中。

> 一个模型要么是高安全性，要么是低安全性；要么是 Oracle（预言机），要么是 Agentic（代理式）。它很难兼顾所有特性。

如果你想进行安全研究，你会选择哪个模型？

答案是 Grok。那是一个低安全性模型。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.025.png)

如果你想要「道德一致」的东西，那就是 Anthropic 或 OpenAI。所以那是高安全性。同样，你有 Oracle。Oracle 与 Agentic 截然相反。Oracle 适合总结任务或需要高水平思考的任务。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.026.png)

同时，你有像 Anthropic 这样的提供商，他们的 Claude Sonnet 是一只数字松鼠（见下文）。

[Claude Sonnet is a small-brained mechanical squirrel of &lt;T&gt;](https://ghuntley.com/cars/)

第一个机器人用来追逐网球，而第一个数字机器人则追逐工具调用（tool calls）。

Sonnet 就像一只专注于工具调用的机器松鼠。它不会花费过多时间思考，而是偏向于行动，这正是其具备 Agentic 特性的原因。Sonnet 专注于通过逐步行动获得成功，而不是在行动前花费数分钟进行思考。

似乎每天都有新模型推向市场，竞争激烈。但实际上，它们各有所长，并占据了各自的细分市场。

问题在于，除非深入使用这些模型，否则你可能无法意识到它们的专长，这导致消费者仅根据两个基本指标来比较模型：

1.  上下文窗口的大小
2.  成本

这好比仅通过车门数量来评价汽车，却忽略了车辆的设计用途是越野还是载客。

构建 Agent 的第一步是选择一个高度 Agentic 的模型。目前的首选是 Claude Sonnet 或 Kimi K2。

你可能会问：「如果需要更高水平的推理来检查工作怎么办？」。这很简单。你可以将其他 LLM 作为工具集成到现有的 Agentic LLM 中。这正是我们在 Amp 所采用的方法。

我们称之为 Oracle。Oracle 只是 GPT 作为一个工具连接进来，Claude Sonnet 可以函数调用它来获得指导，检查工作进度，并进行研究/规划。

[Oracle Amp](https://ampcode.com/news/oracle)

Amp 的 oracle 只是另一个注册为 Agentic LLM 工具的 LLM，它可以对其进行函数调用。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.027.png)

下一个关键点是：上下文窗口应仅用于单一活动。当使用 Cursor 或类似工具时，必须在每次活动结束后清除上下文窗口（见下文）。

[autoregressive queens of failure](https://ghuntley.com/gutter/)

LLM 的输出质量取决于上下文的纯净度。

如果你在一个 AI 辅助会话中构建后端 API 控制器，随后又利用同一会话研究猫鼬。那么，当你要求它重新设计网站时，结果中包含关于 API 或猫鼬的信息也就不足为奇了。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.028.png)

<p class="text-center">注：Sonnet 的上下文窗口已增加到 1M。</p>

上下文窗口非常非常小。最好把它们看作是 Commodore 64，因此，你应该把它当作一台内存有限的计算机。你分配的越多，你的结果和性能就越差。

Sonnet 宣传的上下文窗口是 200K。然而，你不能全部使用它，因为模型需要为系统级提示分配内存。然后 harness（Cursor, Windsurf, Claude Code, Amp）也需要分配一些额外的内存，这意味着你最终大约有 176K 可用 token。

你可能听说过模型上下文协议（MCP）。这是当前的热门话题，最简单的理解方式是将它们视为带有描述的函数，分配给上下文窗口，告知模型如何调用。

我观察到一个常见的失败场景：人们安装了过多的 MCP 服务器，或者未能充分考虑单个 MCP 工具公开的工具数量及所有工具的总上下文窗口占用。

有一条尚未被充分重视的基本规则：分配给上下文窗口的内容越多，其性能越差，结果也会随之恶化。

应避免通过 Agent 或 MCP 工具过度占用上下文窗口。很容易陷入仅为 MCP 工具就分配了额外 76K token 的陷阱，导致可用空间大幅减少。

> 少即是多。

如果你想了解何时使用 MCP 以及何时不使用，我建议你阅读下面的博客文章。

[too many model context protocol servers and LLM allocations on the dance floor](https://ghuntley.com/allocations/)

何时应该使用 MCP，何时不应该使用 MCP，以及上下文窗口中的分配是如何工作的。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.029.png)

让我们回去检查一下我们在后台构建的 Agent。如果你仔细观察，你可以看到循环以及它是如何调用其他工具的。

本质上，这一切是如何工作的在下面的循环中概述。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.030.png)

对于来自用户的每一条输入或工具调用的结果，都会分配给响应，并将该响应发送以进行推理：

![Image](/assets/images/how-to-build-a-coding-agent/inference-loop-diagram.png)

<p class="text-center">推理循环（减去工具注册）</p>

让我们 Clone 以下这个仓库并通过 `go run chat.go` 运行基本的聊天应用程序：

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent)

> **You:** You are a weather expert. When I ask you about the weather in a given location, I want you to reply with `get_weather(<location_name>)`. I will then tell you what the weather in that location is. Understood?
>
> **Claude:** I understand your instructions. When you ask me about the weather in a specific location, I will respond with `get_weather(<location_name>)`. Then you will provide me with the weather information for that location, and I can discuss it with you from there. I'm ready whenever you'd like to ask about the weather somewhere.

所以，让我们问问今天澳大利亚墨尔本的天气怎么样？

> **You:** What's the weather like today in Melbourne, Australia?
>
> **Claude:** `get_weather(Melbourne, Australia)`

至此，操作完成。

我们已将第一个工具注册到模型中。每当关于天气的查询触发潜在空间时，模型便会调用这个新工具。

虽然目前它只是一个存根工具，但原理已清晰可见：我们定义了一个方法，而 LLM 正从查询中提取参数并传递给该方法。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.031.png)

当我们谈论 Agentic 时，我们指的是某种工具调用，某种已经在其奖励函数上受过训练以调用工具的东西。有些模型经过明确训练；它们只想追逐坚果，就像松鼠一样（见下文）。这不是坚果，是工具。

[Claude Sonnet is a small-brained mechanical squirrel of <T>](https://ghuntley.com/cars/)

解释 MCP 或工具的最简单方法是，它只是一个顶部带有广告牌的函数，推动 LLM 的潜在空间来调用该函数。

它就这么简单。你注册工具，描述如何调用它，然后它就可以工作了。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.032.png)

让我们开始制作真正的编码 Agent 的短暂旅程。我们有一个模拟函数和一个模拟工具，但 `get_weather(Melbourne, Australia)` 目前什么也没做，所以让我们修复它。

我们需要做的是创建一个工具，然后调整我们的推理循环以检查它是否想要执行该工具（见上文第 5 行）。如果它想，执行该工具（见上文第 6 行），然后将该工具的结果分配回（见上文第 7 行）循环以进行更多推理。

这是注册工具后我们更新后的序列图的样子。

![Image](/assets/images/how-to-build-a-coding-agent/updated-sequence-diagram.png)

<p class="text-center">这就是最纯粹形式的编码 Agent，没有任何 UI。</p>

由于我们今天不是在制作天气应用程序，让我们换个档次来构建编码 Agent 的第一个原语。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.034.png)

任何编码 Agent 背后的第一个原语是读取工具。所有编码 Agent 都有一个读取工具，可以将文件读取到上下文窗口中，或者是整个文件，或者对于较大的文件，分块读取。

```go
var ReadFileDefinition = ToolDefinition{
	Name:        "read_file",
	Description: "Read the contents of a given relative file path. Use this when you want to see what's inside a file. Do not use this with directory names.",
	InputSchema: ReadFileInputSchema,
	Function:    ReadFile,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent)

让我们再次在代码仓库根目录，创建一个文件：

```bash
cat << EOF
I have a mane but I'm not a lion,
I have four legs but I'm not a table,
I can gallop but I'm not running,
People say I'm disagreeable because I always say "neigh."
What am I?
EOF > riddle.txt
```

然后让我们运行读取文件工具：

`go run read.go`

> **You:** Claude, mate. What's the answer to this riddle in `riddle.txt`?
>
> **Claude:** I'll help you solve the riddle. Let me first read the contents of the `riddle.txt` file to see what the riddle is.
>
> **tool:** `read_file({"path":"riddle.txt"})`
>
> **Reading file:** `riddle.txt`
>
> **Successfully read file** `riddle.txt` (175 bytes)
>
> **result:** I have a mane but I'm not a lion,I have four legs but I'm not a table,I can gallop but I'm not running,People say I'm disagreeable because I always say "neigh."What am I?
>
> **Claude:** After reading the riddle, I can solve it for you:The answer to the riddle is: a horse.Let's analyze the clues:"I have a mane but I'm not a lion" - Horses have manes, which is hair growing from the top of the neck."I have four legs but I'm not a table" - Horses walk on four legs."I can gallop but I'm not running" - Galloping is a specific gait of horses."People say I'm disagreeable because I always say 'neigh'" - "Neigh" is the sound a horse makes, and it sounds like "nay" (which means "no" or disagreement).All of these clues point to a horse as the answer to the riddle.

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.033.png)

任何编码 Agent 背后的第二个原语是列表工具。所有编码 Agent 都有一个列出文件工具，它列出给定路径中的所有文件和目录。

```go
var ListFilesDefinition = ToolDefinition{
	Name:        "list_files",
	Description: "List files and directories at a given path. If no path is provided, lists files in the current directory.",
	InputSchema: ListFilesInputSchema,
	Function:    ListFiles,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent)

让我们再次在代码仓库根目录，通过 `go run list_files.go` 运行基本的聊天应用程序：

> **You:** Claude, mate. Is there a `README.md` in this folder? Also what is the contents of `riddle.txt`?
>
> **Claude:** I'll help you check for a README.md file and show you the contents of `riddle.txt`.First, let me list the files in the current directory to see if `README.md` exists:
>
> **tool:** `list_files({})`
>
> **Listing files in directory:** .
>
> **Successfully listed 88 items in .**
>
> **result:** `[".devenv.flake.nix",".direnv/",".envrc",".gitignore","AGENT.md","Makefile","README.md","bash_tool.go","chat.go","code_search_tool.go","devenv.lock","devenv.nix","devenv.yaml","edit_tool.go","go.mod","go.sum","list_files.go","prompts/","prompts/00-weather.md","prompts/01-read_file.md","prompts/02-list_files.md","prompts/03-bash_tool.md","prompts/04-edit_tool.md","read.go","renovate.json","riddle.txt"]`
>
> **Claude:** Yes, there is a `README.md` file in this folder.Now, let me show you the contents of `riddle.txt`:
>
> **tool:** `read_file({"path":"riddle.txt"})`
>
> **result:** I have a mane but I'm not a lion,I have four legs but I'm not a table,I can gallop but I'm not running,People say I'm disagreeable because I always say "neigh."What am I?

至此，我们已拥有了一个读取文件工具和一个列出文件工具，你可以看到它们的函数被调用并从我们的原始提示链接在一起。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.035.png)

任何编码 harness 背后的第三个原语是 bash 工具，它正如其名。它使 LLM 能够在你的计算机上执行命令。

```go
var BashDefinition = ToolDefinition{
	Name:        "bash",
	Description: "Execute a bash command and return its output. Use this to run shell commands.",
	InputSchema: BashInputSchema,
	Function:    Bash,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent)

让我们再次在代码仓库根目录，运行 bash 工具：

`go run bash_tool.go`

> **You:** Hey Claude, provide a summary of all the processes running on this computer.
>
> **Claude:** I'll provide a summary of all the processes running on this computer. Let me use the `ps` command to gather this information.
>
> **tool:** `bash({"command":"ps aux"})`
>
> **Executing bash command:** ps aux
>
> **Bash command succeeded:** ps aux (output: 87344 bytes)
>
> **result:** <snipped>
>
> **Claude:** Based on the output of the `ps aux` command, here's a summary of the processes running on this computer:System Summary:This is a multi-CPU system with 96 cores/threads (visible from the many CPU-related kernel threads)Running Linux with systemd as the init systemThe system has been up since August 20th (seen in START column)

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.036.png)

任何编码 harness 背后的第四个原语是编辑工具。编辑工具也正如其名。它从推理中获取结果并将编辑应用于文件。

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent)

让我们再次在代码仓库根目录，运行编辑工具：

`go run edit_file.go`

> **You:** Claude, mate. Create `fizzbuzz.js` with nodejs that does fizzbuzz up to 20 and execute it to ensure it works
>
> **Claude:** I'll create a Node.js implementation of FizzBuzz that counts up to 20 and then run it to make sure it works correctly.First, let me create the `fizzbuzz.js`, file:
>
> **tool:** `edit_file({"path":"fizzbuzz.js","old_str":"","new_str":"// FizzBuzz implementation in Node.js\n// Prints numbers from 1 to 20\n// If number is divisible by 3, print "Fizz"\n// If number is divisible by 5, print "Buzz"\n// If number is divisible by both 3 and 5, print "FizzBuzz"\n\nfor (let i = 1; i <= 20; i++) {\n if (i % 3 === 0 && i % 5 === 0) {\n console.log("FizzBuzz");\n } else if (i % 3 === 0) {\n console.log("Fizz");\n } else if (i % 5 === 0) {\n console.log("Buzz");\n } else {\n console.log(i);\n }\n}"})`
>
> **Editing file:** `fizzbuzz.js` (replacing 0 chars with 485 chars)
>
> **File does not exist, creating new file:** `fizzbuzz.js`
>
> **Creating new file:** `fizzbuzz.js`
>
> **Claude:** Now I'll execute the script to make sure it works correctly:
>
> **tool:** `bash({"command":"node fizzbuzz.js"})`
>
> **Executing bash command:** `node fizzbuzz.js`
>
> **Bash command executed successfully, output length:** 77 chars
>
> **result:** 12Fizz4BuzzFizz78FizzBuzz11Fizz1314FizzBuzz1617Fizz19Buzz
>
> **Claude:** Great! The `fizzbuzz.js` file has been created and executed successfully. The output shows:Numbers not divisible by 3 or 5 are printed as is (1, 2, 4, 7, 8, 11, 13, 14, 16, 17, 19)Numbers divisible by 3 (but not 5) print "Fizz" (3, 6, 9, 12, 18)Numbers divisible by 5 (but not 3) print "Buzz" (5, 10, 20)Number 15 prints "FizzBuzz" as it's divisible by both 3 and 5

至此，我们已拥有了一个编码 Agent。此时，我们可以尝试其他提示，例如「实现 FizzBuzz 计数到 100」，它也能正常工作。

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.039.png)

任何编码 Agent 背后的第五个，也是最后一个原语是搜索工具。如果我告诉你，索引源代码或所谓的智能背后并无魔法呢？

```go
var CodeSearchDefinition = ToolDefinition{
	Name: "code_search",
	Description: `Search for code patterns using ripgrep (rg).

Use this to find code patterns, function definitions, variable usage, or any text in the codebase.
You can search by pattern, file type, or directory.`,
	InputSchema: CodeSearchInputSchema,
	Function:    CodeSearch,
}
```

目前几乎所有主流编码工具的底层都使用了开源的 `ripgrep` 二进制文件。如需更多证据，请参阅以下两篇博客文章：

[source code analysis of Amazon Kiro](https://ghuntley.com/amazon-kiro-source-code/)

[from Luddites to AI: the Overton Window of disruption](https://ghuntley.com/overton/)

让我们再次在代码仓库根目录，运行代码搜索工具：

`go run code_search_tool.go`

> **You:** Claude, mate. Search the source code for a riddle
>
> **Claude:** I'd be happy to search the source code for a riddle. Let me use the code search tool to look for mentions of riddles in the codebase.
>
> **tool:** `code_search({"pattern":"riddle"})`
>
> **Searching for pattern:** `riddle`
>
> **Found 6 matches for pattern:** `riddle`
>
> **result:** `./README.md:332:- `riddle.txt`: A simple riddle for content analysis`
>
> **Claude:** I've found references to a riddle file called "`riddle.txt`" in the codebase. Let me check if this file exists by listing the files in the current directory.
>
> **tool:** `list_files({})`
>
> **Listing files in directory:** .
>
> **Successfully listed 25 files in .**
>
> **result:** `["./go.mod","./renovate.json","./devenv.yaml","./AGENT.md","./.devenv.flake.nix","./.envrc","./bash_tool.go","./fizzbuzz.js","./code_search_tool.go","./list_files.go","./Makefile","./devenv.nix","./devenv.lock","./prompts/01-read_file.md","./prompts/02-list_files.md","./prompts/00-weather.md","./prompts/03-bash_tool.md","./prompts/04-edit_tool.md","./chat.go","./go.sum","./riddle.txt","./edit_tool.go","./README.md","./.gitignore","./read.go"]`
>
> **Claude:** Great! I can see that "`riddle.txt`" exists in the current directory. Let me read its contents to see what the riddle is.
>
> **tool:** `read_file({"path":"riddle.txt"})`
>
> **Reading file:** `riddle.txt`
>
> **Successfully read file** `riddle.txt` (175 bytes)
>
> **result:** I have a mane but I'm not a lion,I have four legs but I'm not a table,I can gallop but I'm not running,People say I'm disagreeable because I always say "neigh."What am I?
>
> **Claude:** I found the riddle in the file `riddle.txt`!

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.037.png)

接下来的工作主要是调整提示词。由于篇幅限制，本文未深入探讨 Harness 提示的概念。Harness 提示是注册工具的地方，它包含诸如操作系统类型等信息，以便 Agent 知道是使用 PowerShell (Windows) 还是 bash (Linux 或 macOS)。

它还包含关于 Agent 应如何操作的指令。之所以说「应」，是因为 LLM 具有非确定性。你可以提供指导，但这仅是引导。然而，通过提示评估、调整以及深入了解模型的行为模式，你可以开发出高效的提示。

如果你想看一个完全成熟的编码 Agent 的例子，请访问下面的博客文章：

[source code analysis of Amazon Kiro](https://ghuntley.com/amazon-kiro-source-code/) (需要付费订阅)

已经有很多开源编码 Agent，例如 SST Open Code

[GitHub - sst/opencode](https://github.com/sst/opencode)

或者这个 100 行的 Agent，它在 SWE Bench 上得分很高。

[GitHub - SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent)

如果你想要一些灵感，GitHub 上有许多存储库泄露了开发人员工具 harness 和工具提示。

[GitHub - x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools)

![Image](/assets/images/how-to-build-a-coding-agent/how-to-build-an-agent.041.png)

回顾一下，你刚刚构建了一个编码 Agent。也许你的目标并非创建一个编码 Agent。如果你是数据工程师，情况会如何？思考一下你的日常活动，拥有利用这些原语进行自动化的能力，对你的雇主而言将极具价值。

取代你工作的将是善用 AI 的人，而非 AI 本身。

如果你对 AI 感到焦虑，答案很简单：投资自己。今年是个人发展充满挑战的一年，切勿停滞不前。

[the six-month recap: closing talk on AI at Web Directions, Melbourne, June 2025](https://ghuntley.com/six-month-recap/)

> 勇往直前，开始构建吧。
