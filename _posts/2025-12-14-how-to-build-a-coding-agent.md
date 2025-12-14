---
layout: post
title: "如何构建一个编码 Agent：免费研讨会"
date: 2025-12-14 12:00:00 +0800
categories: ai agent
---

> 原文链接：[How to build a coding agent: free workshop](https://ghuntley.com/agent/)
> 
> 作者：Geoffrey Huntley

![how to build a coding agent: free workshop](https://ghuntley.com/content/images/size/w2000/2025/07/how-to-build-an-agent.001.jpg)

😎 以下内容是上个月开发的，并且已经在两个会议上发表过。如果你希望我在你的公司举办类似的研讨会，请[联系我](https://ghuntley.com/workshops/)。

大家好，今天我在这里教大家如何构建一个编码 Agent。在这个会议阶段，你可能已经厌倦了听到“Agent”这个词。

你经常听到这个词。然而，似乎每个人都在松散地使用这个术语，而没有清楚地理解它的含义或这些编码 Agent 内部是如何运作的。是时候揭开面纱，展示这里并没有什么护城河了。

学习如何构建编码 Agent 是你在 2025 年个人发展中能做的最好的事情之一，因为它教会你基础知识。一旦你理解了这些基础知识，你将从 AI 的消费者转变为 AI 的生产者，能够用 AI 自动化事务。

让我以以下事实开场：

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.002.png)

这并不难

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.003.png)

构建一个编码 Agent

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.004.png)

只有 300 行代码

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.005.png)

在一个循环中运行

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.006.png)

使用 LLM token，这就是全部。

300 行代码在一个循环中运行，使用 LLM token。你只需要不断向循环中投入 token，然后你就拥有了一个 Agent。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.007.png)

今天，我们要构建一个。我们将现场进行，我会解释它是如何工作的基本原理。既然我们现在是在 2025 年，与 AI 协助并发工作已成为常态。那么，有什么比让一个 Agent 在我发表演讲的同时为我构建一个 Agent 更好的方式来演示这次演讲的重点呢？

酷。我们现在正在构建一个 Agent。这是我们行业正在发生的变化之一，因为工作可以并发完成，而且是在你离开电脑的时候。

花一周或几天时间进行研究冲刺的日子已经结束了，因为你只需对着电脑说话就可以将想法转化为执行。

下次你在 Zoom 通话时，考虑一下你本可以让一个 Agent 在通话期间构建你计划要做的工作。如果这对你来说不是常态，而对你的同事来说是，那么你自然不会领先。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.009.png)

请构建你自己的

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.010.png)

因为这些知识

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.011.png)

将改变你

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.012.png)

从消费者

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.013.png)

变成生产者

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.014.png)

能够自动化事务

科技行业就像一条传送带——我们需要不断学习新事物。

如果我问你什么是主键，你应该知道什么是主键。这在很长一段时间里都是常态。

在 2024 年，理解什么是主键是必不可少的。

在 2025 年，你应该熟悉什么是主键以及如何创建一个 Agent，因为知道这个循环是什么以及如何构建一个 Agent 现在是雇主在让你进门之前寻找的基础知识。

[Yes, You Can Use AI in Our Interviews. In fact, we insist - Canva Engineering Blog](https://www.canva.dev/blog/engineering/yes-you-can-use-ai-in-our-interviews/?ref=ghuntley.com)

因为这些知识将把你从 AI 的消费者转变为能够编排工作职能的 AI 生产者。雇主现在正在寻找能够在组织内自动化任务的个人。

如果你今天下午晚些时候参加会议闭幕式（见下文），我将更深入地探讨上述内容。

[the six-month recap: closing talk on AI at Web Directions, Melbourne, June 2025](https://ghuntley.com/six-month-recap/)

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.015.png)

现在，你将处于上述旅程的某个位置。

在左上角，我们有“向我证明，这不是真的”，“向我证明，给我看结果”，“向我证明这不是炒作”，以及一群“这还不够好”的人，他们被困在悬崖的左侧，完全忽略了悬崖另一边有人正在完全自动化他们的工作职能。

> 在我看来，任何与 AI 相关的颠覆或失业都不是 AI 本身的结果，而是缺乏个人发展和自我投资的后果。如果你的同事在多个 Agent 之间跳跃，咀嚼想法，并在会议期间在后台运行，而你没有参与其中，那么你自然会落后。

[What do I mean by some software devs are “ngmi”?](https://ghuntley.com/ngmi/)

不要成为悬崖左边的人。

科技行业的传送带继续向前移动。如果你是 2025 年的 DevOps 工程师，而你没有任何 AWS 或 GCP 的经验，那么你会发现就业市场非常艰难。

软件和数据工程师感到惊讶的是，这一切发生得如此之快。自从第一个编码 Agent 发布以来已经八个月了，大多数人仍然不知道构建一个是多么简单，这个循环是多么强大，以及它对我们职业的颠覆性影响。

所以，我叫 Geoffrey Huntley。我曾是 Canva 的开发者生产力技术主管，但几个月前，我成为了 Sourcegraph 构建 [Amp](https://ampcode.com/?ref=ghuntley.com) 的工程师之一。这是一个大约六人的核心小团队。我们用 AI 构建 AI。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.016.png)

ampcode.com

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.017.png)

cursor

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.018.png)

windsurf

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.019.png)

claude code

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.020.png)

github co-pilot

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.022.png)

都是在 LLM token 循环中运行的代码行。

Cursor, Windsurf, Claude Code, GitHub Copilot, 和 Amp 只是在 LLM token 循环中运行的一小部分代码。我怎么强调都不为过。模型在这里完成了所有繁重的工作，伙计们。是模型完成了一切。

你可能正在评估五个供应商的产品，试图比较所有这些 Agent。但实际上，你只是在追逐自己的尾巴。

构建你自己的太容易了...

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.023.png)

你只需要了解几个关键概念。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.024.png)

并非所有 LLM 都是 Agentic（代理式）的。

就像你有不同类型的汽车一样，如果你想越野，你有 [40 系列](https://en.wikipedia.org/wiki/Toyota_Land_Cruiser_(J40)?ref=ghuntley.com)，如果你想运送人，你有载人汽车。

同样的原则适用于 LLM，我已经能够将它们的行为映射到一个象限中。

> 一个模型要么是高安全性，低安全性，Oracle（预言机），要么是 Agentic。它从来都不是两者兼有或全部。

如果你想做一些安全研究，你会用哪个模型？

那是 Grok。那是一个低安全性模型。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.025.png)

如果你想要“道德一致”的东西，那就是 Anthropic 或 OpenAI。所以那是高安全性。同样，你有 Oracle。Oracle 与 Agentic 截然相反。Oracle 适合总结任务或需要高水平思考的任务。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.026.png)

同时，你有像 Anthropic 这样的提供商，他们的 Claude Sonnet 是一只数字松鼠（见下文）。

[Claude Sonnet is a small-brained mechanical squirrel of <T>](https://ghuntley.com/cars/)

第一个机器人用来追逐网球。第一个数字机器人追逐工具调用（tool calls）。

Sonnet 是一只只想做工具调用的机器松鼠。它不会花太多时间思考；它偏向于行动，这就是它成为 Agentic 的原因。Sonnet 专注于逐步获得成功，而不是在采取行动之前每回合思考几分钟。

似乎每天都有新模型推向市场，它们都在相互竞争。但说实话，它们有自己的专长，并开辟了自己的利基市场。

问题是，除非你在亲密层面上使用这些模型，否则你可能没有意识到模型的这些专长，这导致消费者仅根据两个基本原语比较模型：

1.  上下文窗口的大小
2.  成本

这有点像看一辆车，看它是两门还是三门，而忽略了有些车辆是为越野设计的，而另一些是为客运设计的这一事实。

要构建一个 Agent，第一步是选择一个高度 Agentic 的模型。目前是 Claude Sonnet 或 Kimi K2。

现在，你可能会想，“如果你想要更高水平的推理和检查增量松鼠的工作怎么办？”。啊，这很简单。你可以将其他 LLM 作为工具连接到现有的 Agentic LLM 中。这就是我们在 Amp 所做的。

我们称之为 Oracle。Oracle 只是 GPT 作为一个工具连接进来，Claude Sonnet 可以函数调用它来获得指导，检查工作进度，并进行研究/规划。

[Oracle Amp](https://ampcode.com/news/oracle?ref=ghuntley.com)

Amp 的 oracle 只是另一个注册为 Agentic LLM 工具的 LLM，它可以对其进行函数调用。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.027.png)

下一个要学习的重要事情是，你应该只将上下文窗口用于一项活动。当你使用 Cursor 或任何这些工具时，必须在每次活动后清除上下文窗口（见下文）。

[autoregressive queens of failure](https://ghuntley.com/gutter/)

LLM 的结果是你分配到草堆中的草堆里的一根针。

如果你开始一个 AI 辅助会话来构建后端 API 控制器，然后重用该会话来研究关于猫鼬的事实。那么当你告诉它重新设计网站时，网站最终可能会包含关于你的 API 或猫鼬的事实，或者两者兼有，这也就不足为奇了。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.028.png)

注：自本次研讨会以来，Sonnet 的上下文窗口已增加到 1m。

上下文窗口非常非常小。最好把它们看作是 Commodore 64，因此，你应该把它当作一台内存有限的计算机。你分配的越多，你的结果和性能就越差。

Sonnet 宣传的上下文窗口是 200k。然而，你不能全部使用它，因为模型需要为系统级提示分配内存。然后 harness（Cursor, Windsurf, Claude Code, Amp）也需要分配一些额外的内存，这意味着你最终大约有 176k 可用 token。

你可能听说过很多关于模型上下文协议（MCP）的事情。它们是当前的热门事物，最简单的思考方式是将它们视为分配给上下文窗口的带有描述的函数，告诉它如何调用该函数。

我观察到的一个常见失败场景是人们安装了过多的 MCP 服务器，或者未能考虑单个 MCP 工具公开的工具数量或所有工具的总上下文窗口分配。

有一个尚未被充分理解的基本规则。你分配给上下文窗口的越多，上下文窗口的性能就越差，你的结果就会恶化。

避免通过你的 Agent 或 MCP 工具消耗过度分配上下文窗口。很容易陷入仅为 MCP 工具分配额外 76K token 的陷阱，这意味着你只有 100K 可用。

> 少即是多，伙计们。少即是多。

如果你想了解何时使用 MCP 以及何时不使用，我建议你阅读下面的博客文章。

[too many model context protocol servers and LLM allocations on the dance floor](https://ghuntley.com/allocations/)

何时应该使用 MCP，何时不应该使用 MCP，以及上下文窗口中的分配是如何工作的。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.029.png)

让我们回去检查一下我们在后台构建的 Agent。如果你仔细观察，你可以看到循环以及它是如何调用其他工具的。

本质上，这一切是如何工作的在下面的循环中概述。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.030.png)

对于来自用户的每一条输入或工具调用的结果，都会分配给响应，并将该响应发送以进行推理：

![Image](https://ghuntley.com/content/images/size/w1600/2025/08/Untitled-diagram-_-Mermaid-Chart-2025-08-24-015242.png)

推理循环（减去工具注册）

让我们打开研讨会材料（如下）并通过 `go run chat.go` 运行基本的聊天应用程序：

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent?ref=ghuntley.com)

> **You:** You are a weather expert. When I ask you about the weather in a given location, I want you to reply with `get_weather(<location_name>)`. I will then tell you what the weather in that location is. Understood?
>
> **Claude:** I understand your instructions. When you ask me about the weather in a specific location, I will respond with `get_weather(<location_name>)`. Then you will provide me with the weather information for that location, and I can discuss it with you from there. I'm ready whenever you'd like to ask about the weather somewhere.

所以，让我们问问今天澳大利亚墨尔本的天气怎么样？

> **You:** What's the weather like today in Melbourne, Australia?
>
> **Claude:** `get_weather(Melbourne, Australia)`

Boom！就是这样！

我们已经将我们的第一个工具注册到模型中，每当我们用关于天气的查询触动潜在空间时，它就会函数调用我们的新工具。

它目前是一个存根工具，但你可以看到它；我们有一个方法，LLM 正在从我们的查询中将参数传递给该方法。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.031.png)

当我们谈论 Agentic 时，我们指的是某种工具调用，某种已经在其奖励函数上受过训练以调用工具的东西。有些模型经过明确训练；它们只想追逐坚果，就像松鼠一样（见下文）。这不是坚果，是工具。

[Claude Sonnet is a small-brained mechanical squirrel of <T>](https://ghuntley.com/cars/)

解释 MCP 或工具的最简单方法是，它只是一个顶部带有广告牌的函数，推动 LLM 的潜在空间来调用该函数。

它就这么简单。你注册工具，描述如何调用它，然后它就可以工作了。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.032.png)

让我们开始制作真正的编码 Agent 的短暂旅程。我们有一个模拟函数和一个模拟工具，但 `get_weather(Melbourne, Australia)` 目前什么也没做，所以让我们修复它。

我们需要做的是创建一个工具，然后调整我们的推理循环以检查它是否想要执行该工具（见上文第 5 行）。如果它想，执行该工具（见上文第 6 行），然后将该工具的结果分配回（见上文第 7 行）循环以进行更多推理。

这是注册工具后我们更新后的序列图的样子。

![Image](https://ghuntley.com/content/images/size/w1600/2025/08/Untitled-diagram-_-Mermaid-Chart-2025-08-24-015409.png)

这就是最纯粹形式的编码 Agent，没有任何 UI。

由于我们今天不是在制作天气应用程序，让我们换个档次来构建编码 Agent 的第一个原语。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.034.png)

任何编码 Agent 背后的第一个原语是读取工具。所有编码 Agent 都有一个读取工具，可以将文件读取到上下文窗口中，或者是整个文件，或者对于较大的文件，分块读取。

```go
var ReadFileDefinition = ToolDefinition{
	Name:        "read_file",
	Description: "Read the contents of a given relative file path. Use this when you want to see what's inside a file. Do not use this with directory names.",
	InputSchema: ReadFileInputSchema,
	Function:    ReadFile,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent?ref=ghuntley.com)

让我们再次打开研讨会材料（上文）并创建一个文件：

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

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.033.png)

任何编码 Agent 背后的第二个原语是列表工具。所有编码 Agent 都有一个列出文件工具，它列出给定路径中的所有文件和目录。

```go
var ListFilesDefinition = ToolDefinition{
	Name:        "list_files",
	Description: "List files and directories at a given path. If no path is provided, lists files in the current directory.",
	InputSchema: ListFilesInputSchema,
	Function:    ListFiles,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent?ref=ghuntley.com)

让我们再次打开研讨会材料（上文）并通过 `go run list_files.go` 运行基本的聊天应用程序：

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

Boom！我们现在有一个读取文件工具和一个列出文件工具，你可以看到它们的函数被调用并从我们的原始提示链接在一起。

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.035.png)

任何编码 harness 背后的第三个原语是 bash 工具，它正如其名。它使 LLM 能够在你的计算机上执行命令。

```go
var BashDefinition = ToolDefinition{
	Name:        "bash",
	Description: "Execute a bash command and return its output. Use this to run shell commands.",
	InputSchema: BashInputSchema,
	Function:    Bash,
}
```

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent?ref=ghuntley.com)

让我们再次打开研讨会材料（上文）并运行 bash 工具：

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

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.036.png)

任何编码 harness 背后的第四个原语是编辑工具。编辑工具也正如其名。它从推理中获取结果并将编辑应用于文件。

[GitHub - ghuntley/how-to-build-a-coding-agent](https://github.com/ghuntley/how-to-build-a-coding-agent?ref=ghuntley.com)

让我们再次打开研讨会材料（上文）并运行编辑工具：

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

And voila，我们现在有了一个编码 Agent。是不是在这一点上我们可以抛出一些其他提示说，“嘿，让我们做 FizzBuzz 到 100，它就会工作。”

![Image](https://ghuntley.com/content/images/size/w1600/2025/08/how-to-build-a-agent.039.png)

任何编码 harness 背后的第五个也是最后一个原语是搜索工具。如果我告诉你索引源代码或任何智能都没有魔法呢？

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

目前几乎所有可用的编码工具都在底层使用开源的 `ripgrep` 二进制文件。如果你想要更多证据，请参阅下面的两篇博客文章：

[source code analysis of Amazon Kiro](https://ghuntley.com/amazon-kiro-source-code/)

[from Luddites to AI: the Overton Window of disruption](https://ghuntley.com/overton/)

让我们再次打开研讨会材料并运行代码搜索工具：

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

![Image](https://ghuntley.com/content/images/size/w1600/2025/07/how-to-build-a-agent.037.png)

从这一点开始的一切都只是调整你的提示的问题。由于时间限制，我们没有深入探讨 harness 提示的概念。Harness 提示是你注册工具的地方。它包含诸如你正在运行的操作系统之类的信息，因此它知道是使用 PowerShell (Windows) 还是 bash (Linux 或 macOS)。

它还包含有关 Agent 应如何操作的说明。我说“应”是因为 LLM 是非确定性的。你可以包含指导，但这只是指导。然而，通过提示评估、调整以及花时间玩模型以了解它们的行为方式，你可以开发出有效的提示。

如果你想看一个完全成熟的编码 Agent 的例子，请访问下面的博客文章：

[source code analysis of Amazon Kiro](https://ghuntley.com/amazon-kiro-source-code/)

已经有很多开源编码 Agent，例如 SST Open Code

[GitHub - sst/opencode](https://github.com/sst/opencode?ref=ghuntley.com)

或者这个 100 行的 Agent，它在 SWE Bench 上得分很高。

[GitHub - SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent?ref=ghuntley.com)

如果你想要一些灵感，GitHub 上有许多存储库泄露了开发人员工具 harness 和工具提示。

[GitHub - x1xhlol/system-prompts-and-models-of-ai-tools](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools?ref=ghuntley.com)

![Image](https://ghuntley.com/content/images/size/w1600/2025/08/how-to-build-a-agent.041.png)

回顾一下。你刚刚构建的是一个编码 Agent。也许你不想创建一个编码 Agent。如果你从事数据工程职业怎么办？那会是什么样子？想想你日常做的所有活动，拥有使用这些原语进行自动化的能力对你的雇主来说可能是方便或有价值的。

你现在的工人将取代你的工作，而不是 AI。

如果你担心 AI，答案很简单：投资你自己。就这么简单。今年是在个人发展方面睡大觉的一个特别具有挑战性的时期。

[the six-month recap: closing talk on AI at Web Directions, Melbourne, June 2025](https://ghuntley.com/six-month-recap/)

我希望今天下午晚些时候能在会议闭幕式上见到你。

> 前进并构建吧。

ps. 社交媒体

• X - [https://x.com/GeoffreyHuntley/status/1959453609240007052](https://x.com/GeoffreyHuntley/status/1959453609240007052?ref=ghuntley.com)
• Linkedin : [https://www.linkedin.com/posts/geoffreyhuntley_how-to-build-an-agent-activity-7365220712707485697-EiJO](https://www.linkedin.com/posts/geoffreyhuntley_how-to-build-an-agent-activity-7365220712707485697-EiJO?utm_source=share&utm_medium=member_desktop&rcm=ACoAAABQKuUB2AJ059keUcRUVLbtmoa6miLVlTI)
• Bluesky: [https://bsky.app/profile/ghuntley.com/post/3lx4jmqsclk2q](https://bsky.app/profile/ghuntley.com/post/3lx4jmqsclk2q?ref=ghuntley.com)
