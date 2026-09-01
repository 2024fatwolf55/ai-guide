# VSCode + GitHub Copilot: Microsoft’s All-in-One AI Coding Practice

> A step-by-step guide from installation to real-world practice with VSCode + GitHub Copilot



Hello, I’m Yupi.

AI coding tools are truly blooming everywhere right now. Cursor, Claude Code, OpenCode… every so often, a new contender pops up.

I had been addicted to Cursor and Claude Code for a long time, but when I seriously tried GitHub Copilot while building a new project recently, I realized this thing is actually pretty awesome!

![](https://pic.yupi.icu/1/13c2a89f183a7161be27361ce4908ed6.png)

Let me briefly introduce the stars of the show. **VSCode** is Microsoft’s code editor and the most popular in the world, with over a hundred million installs. **GitHub Copilot** is GitHub’s official AI coding assistant plugin, which you use directly inside VSCode.

Based on my personal experience, compared with other AI coding tools, it has four major advantages:

1. It supports the latest AI large models. Opus, GPT, Gemini, Claude—you can switch freely, and the coding quality is genuinely excellent. Full-stack projects can be done in one shot.
2. It supports multiple runtime modes including local, background CLI, cloud, and Claude Code, so the compatibility is extremely strong.
3. It supports visual management for MCP, Skills, and tool calls. It’s flexible and convenient, and you don’t have to write configuration by hand.
4. It supports sub-agents, and every step of interaction with the AI is clearly visible, so the Agent execution experience is excellent.

Wait, what? What are all these things?

![](https://pic.yupi.icu/1/image-20260305141036239.png)

Even if you don’t understand any of that yet, don’t worry. This article will take everyone from zero to getting started with VSCode + GitHub Copilot, from installation to real-world practice, and from the basics to the core features—a full one-stop package.

This is a dense article packed with useful information, so I recommend bookmarking it first, then finding a quiet place, clearing your mind, and slowly reading through it. Excellent sleep-aid potential too~



## Installation and Setup

1) First, go to the [VSCode official website](https://code.visualstudio.com/) and download the installer. Just follow the standard installation process.

![](https://pic.yupi.icu/1/image-20260305141229310.png)

2) Open VSCode, click the “Extensions Marketplace” icon on the left, search for `GitHub Copilot`, and install the official AI coding plugin.

![](https://pic.yupi.icu/1/image-20260305141416199.png)

If you want, you can also install the Chinese localization plugin, which is convenient for domestic users in China:

![](https://pic.yupi.icu/1/image-20260305153013870.png)

3) After installation, click the Copilot icon in the VSCode status bar at the bottom and log in to your GitHub account by following the instructions.

![](https://pic.yupi.icu/1/setup-copilot-status-bar.png)

If you don’t already have a Copilot subscription, you’ll automatically enter the **Copilot Free** plan, which includes a certain monthly quota for AI chat and code completion—perfect for getting started with zero barrier. If you want the full feature set, Copilot Pro offers a 30-day free trial for new users. A domestic Visa card is enough to activate it.

I got myself a free 30-day premium trial, which means I can save a bit of quota from other AI coding tools lately haha~ 🤣

At this point, all the installation and configuration is done. Compared with Claude Code’s combo of network restrictions, account restrictions, and pure command-line darkness, this setup is much easier.

![](https://pic.yupi.icu/1/1766562559951-d1371bb9-99d3-467a-aeec-421cd12eb3bb.png)



## Basic Usage

Now that it’s installed, let’s first experience the most basic AI coding workflow.



### AI Chat

Click the “chat button” at the top of VSCode to open the Chat panel, and then you can happily chat with AI. Ask it to analyze requirements, write code, fix bugs—whatever you want.

![](https://pic.yupi.icu/1/image-20260305142129090.png)

There’s an **agent selector** in the chat area that lets you switch between three built-in modes:

- Agent mode: fully autonomous. AI analyzes, writes code, runs commands, and completes tasks end-to-end by itself (the one I use most)
- Plan mode: AI produces a plan before acting, suitable for more complex tasks
- Ask mode: pure Q&A only, no code modification, suitable for exploration and learning (I use this less)

![](https://pic.yupi.icu/1/image-20260305142244467.png)

Besides the Chat panel, there are two lighter-weight AI conversation methods.

1) Press `Ctrl+I` (`Cmd+I` on Mac) to open inline chat and interact with AI directly inside the code:

![](https://pic.yupi.icu/1/image-20260305142602604.png)

2) Press `Ctrl+Shift+Alt+L` (`Cmd+Shift+Option+L` on Mac) to open Quick Chat, which is great for fast questions and quick answers.

![](https://pic.yupi.icu/1/image-20260305143009366.png)



### AI Code Completion

While you’re writing code, Copilot automatically gives you light-colored completion suggestions. Press `Tab` to accept them. For example, if you start with a function name like `plusDate`, it can directly complete the whole function body for you.

![](https://pic.yupi.icu/1/image-20260305143231950.png)

Even smarter is Next Edit Suggestions (NES). It doesn’t just complete the current location—it can predict where you’ll want to edit next!

A small arrow appears on the left side of the editor. Press `Tab` and it jumps there and applies the suggestion.

![](https://pic.yupi.icu/1/image-20260305143512348.png)

For example, if you rename a class from `Point` to `Point3D`, it will automatically suggest adding a `z` variable further down. The experience is smooth as silk.

![](https://pic.yupi.icu/1/nes-point.png)

If you’ve used Cursor, these two features should feel familiar. The overall experience is similar, though personally I think Copilot’s NES is slightly better in prediction accuracy.

Alright, those are the basic functions. If you’ve read this far, you’ve already surpassed 70% of the students!

Next comes the real topic: AI Agent coding in practice.



## AI Agent Coding Practice

The chat and code completion features above are only appetizers. Agent mode is GitHub Copilot’s real killer feature.

So what is an Agent?

Simply put, you give it a requirement, and it analyzes the project, makes a plan, creates files, writes code, runs commands, installs dependencies, and even automatically fixes errors when something goes wrong—all autonomously.

In fact, the Agent modes found in Manus, OpenClaw, and various AI coding tools are all fundamentally the same thing: AI autonomously planning, calling tools, and executing tasks.

Now every major AI coding tool is competing on Agent capability. For example, Cursor lets sub-agents operate the browser for autonomous verification, and Claude Code introduced Agent Teams so multiple AI workers can collaborate. GitHub Copilot is not backing down either. Besides Agent mode, it also provides the **Plan mode** that many tools support now. AI first helps you design a plan and break steps down, and only after you confirm it will it start implementing. That makes it suitable for slightly more complex projects and reduces the chance of AI diving straight into code and crashing.

Next, I’ll show you a real example by combining Plan mode + Agent mode to build an **“AI fortune-teller website”** where users enter a question, AI draws tarot cards, and then generates an interpretation.



### Step 1. Use Plan Mode to Create the Plan

Create a new empty project folder (for example, `ai-diviner`) and open it in VSCode. The Chat panel should open by default.

![Create a new project](https://pic.yupi.icu/1/image-20260305144504583.png)

In the chat area, choose Plan mode from the agent selector and select a model (such as Claude Opus), then enter the requirement:

```
帮我用 HTML + CSS + JavaScript 做一个 AI 塔罗牌占卜网站。

功能描述：
1. 用户输入一个问题（比如「我最近事业运如何」）
2. 点击「开始占卜」后，展示 3 张塔罗牌的翻牌动画
3. 翻牌完成后，根据抽到的牌生成 AI 占卜解读
4. 界面要神秘华丽，深紫色主题配金色纹理，星空背景
5. 有流畅的翻牌动画效果
6. 响应式布局，手机也能用
```

![AI executing in Plan mode](https://pic.yupi.icu/1/image-20260305144551103.png)

Once Plan mode is selected, AI does not start writing code immediately.

It first studies your requirements, and may even ask you a few questions. For example: should the AI interpretation be generated by calling a large-model API, or randomly selected from a preset text library?

You just tell AI your thoughts as if you were chatting with a person. For example, I wanted it to call the DeepSeek large-model API:

![](https://pic.yupi.icu/1/image-20260305144900988.png)

If you’re not sure yourself, you can also let AI analyze the pros and cons of different approaches, or simply let it decide on its own.

After AI understands your requirements, it gives you a structured implementation plan.

![](https://pic.yupi.icu/1/image-20260305145315374.png)

The plan lists which files to create, what each file is responsible for, the order of implementation steps, and how to verify the result. At this step, you can discuss and adjust the plan with AI repeatedly until you’re satisfied.

![](https://pic.yupi.icu/1/image-20260305145352874.png)

At its core, Plan mode uses a four-stage iterative workflow: requirement research → question alignment → solution design → iterative refinement. AI first uses read-only tools to deeply inspect your codebase, then resolves ambiguity through interactive Q&A, and only then produces a proposal draft.

This is actually the standard software development process. Even if you don’t use Copilot’s built-in Plan mode, you can still guide AI with prompts to design a plan first, get human confirmation, and then move into implementation. It helps build the good habit of **thinking things through before you start coding**.



### Step 2. Use Agent Mode to Execute the Plan

Once the plan looks good, click the “Start Implementation” button below it and let the AI start executing automatically until the plan is implemented.

![](https://pic.yupi.icu/1/image-20260305145604534.png)

During execution, the Agent automatically manages a Todos list to track progress. You can clearly see what it’s doing—for example, creating `index.html`, `style.css`, and `script.js`, writing code into them, and even opening the terminal to run commands if needed.

![](https://pic.yupi.icu/1/image-20260305145807776.png)

If the AI needs to run terminal commands or call certain tools, a confirmation dialog will pop up for your approval, which keeps things safe.

![](https://pic.yupi.icu/1/image-20260305150107141.png)

You can also continue sending messages while the Agent is working—queue them, interrupt immediately, or guide AI to change direction.

For people new to AI coding, I recommend paying close attention to how the AI works. If you notice it going off the rails, intervene quickly. That can save tokens and reduce rework.



### Step 3. Check the Result

A few minutes later, the Agent not only finished the development task, but also started a web server using Python and ran the site for me.

![](https://pic.yupi.icu/1/image-20260305150430976.png)

Good grief—this thing really doesn’t want me to do even one extra step, does it? At this rate, sooner or later I’ll degrade back to Hello World level.

Still, I prefer testing in Chrome, so I copied the URL into the browser and opened it, then entered the large-model API Key from the [DeepSeek Open Platform](https://platform.deepseek.com/api_keys):

![](https://pic.yupi.icu/1/image-20260305150858949.png)

![](https://pic.yupi.icu/1/image-20260305150957888.png)

Then I entered a question to test my love luck this year and clicked “Start Divination”:

![](https://pic.yupi.icu/1/image-20260305151027082.png)

Three tarot cards flipped over one by one, and an AI-generated interpretation appeared below. The dark purple starry background, gold borders, and smooth flip animations made it look surprisingly convincing.

![](https://pic.yupi.icu/1/image-20260305151413007.png)

I honestly feel like I could open a little tarot booth now. Maybe that’s not an illusion…

![](https://pic.yupi.icu/1/image-20260305151303905.png)

If you’re not happy with some details of the page, you can click the “select element” button in the built-in browser, click whatever bothers you, and then write a prompt in the Chat box. For example:

```
改为鱼皮塔罗
```

![](https://pic.yupi.icu/1/image-20260305151754685.png)

The Agent will automatically locate the corresponding code and modify it precisely. Then you just refresh the preview.

![](https://pic.yupi.icu/1/image-20260305152037670.png)

The whole process—from writing the requirement to getting the finished result—took only a few minutes. If I had built a divination website with animations from scratch by myself before, it definitely would have taken me an entire afternoon.

You can also keep talking with AI to add more features, but throughout the process you must pay attention to **context usage**. If the context fills up, AI may start forgetting things and randomly editing the wrong stuff.

![](https://pic.yupi.icu/1/image-20260305152200805.png)

So when the context is nearly full, it’s best to have AI consolidate the current project information into documentation. That way, the next time you open a new conversation, you can simply hand those documents to AI and quickly restore its memory.

OK, that wraps up the hands-on demo. If you’ve made it this far, you’ve already beaten 90% of the students!

Next, let’s look at GitHub Copilot’s core features—these are the things that really create the gap.



## Core Features

### Tools - AI’s Toolbox

The reason an Agent can work autonomously is tool use.

Tools are the various abilities AI can call when executing tasks—things like searching code, reading and writing files, running terminal commands, fetching webpage content, and so on. Without tools, AI can only talk and tell you what to do. With tools, AI can actually do the work for you.

VSCode provides three types of tools for AI:

- Built-in tools: ready to use out of the box, including code search, file read/write, terminal execution, problem diagnosis, and other common capabilities
- MCP tools: external tools connected through the MCP protocol (more on that below)
- Extension tools: tools provided by VSCode plugins, automatically available once the corresponding plugin is installed

All tools can be visually managed through the “Configure Tools” button in the Chat area, which is extremely convenient:

![](https://pic.yupi.icu/1/image-20260305152856918.png)

You can freely enable or disable tools without writing any config files, which is much more convenient than many other AI coding tools.

After enabling tools, AI will automatically decide which ones to call in most cases. You can also manually reference a specific tool in the conversation with `#`, such as `#codebase` to search the whole codebase, `#fetch codefather.cn` to grab webpage content, or `#problems` to view all current errors in the project.

![](https://pic.yupi.icu/1/image-20260305153343950.png)

When the Agent executes terminal commands, there’s also a safety approval mechanism. We saw this in the hands-on demo earlier. By default, it pops up a confirmation dialog and waits for human approval. You can also configure auto-approval rules or even enable terminal sandboxing (currently supported on macOS and Linux) to restrict file and network access for maximum safety.

![](https://pic.yupi.icu/1/image-20260305153647365.png)

There’s also a useful feature called Tool Sets. You can package multiple related tools into a group and reference them all at once in chat using `#toolset-name`.

For example, you can create a tool set called `reader` that includes read-only tools such as `codebase` search, `problems` diagnosis, `usages` reference lookup, and `search`. That’s very handy for code review.

First, enable “Tool Sets” in the chat panel settings, click to create a new tool set file, and enter a name:

![](https://pic.yupi.icu/1/image-20260306104630540.png)

Then the tool set config file pops up automatically. Add the following code and save it:

```json
{
  "reader": {
    "tools": ["codebase", "problems", "usages", "search"],
    "description": "只读工具集，适合代码审查",
    "icon": "book"
  }
}
```

![](https://pic.yupi.icu/1/image-20260306104906332.png)

After configuring it, typing `#reader` in the conversation will enable that whole read-only tool group at once:

![](https://pic.yupi.icu/1/image-20260306105151652.png)



### MCP - Let AI Connect to External Capabilities

MCP (Model Context Protocol) is an open standard protocol that allows AI to connect to external tools and services. You can think of it as a universal interface for AI. Through it, AI can operate databases, call APIs, control browsers, and much more.

MCP is already extremely popular in the AI world, and various AI coding tools support it. But GitHub Copilot’s MCP management experience genuinely impressed me—Microsoft directly integrated MCP into the VSCode extension marketplace!

You just open the VSCode extension marketplace, enable the MCP server marketplace, and you’ll see a bunch of popular MCP services. There’s no need to search MCP resource sites and install things manually anymore?!

![](https://pic.yupi.icu/1/image-20260305154025676.png)

For example, if I want to use Context7, an MCP for fetching the latest technical documentation, I simply click install, and it automatically pops up a dialog asking for the API Key:

![](https://pic.yupi.icu/1/image-20260305154459227.png)

After confirming, it works normally. AI automatically calls the tools provided by the MCP during task execution, and you can also proactively reference them with `#`.

For example, after installing Context7, when you ask AI to write code, it can automatically fetch the latest technical docs for reference, reducing the chance that AI hallucinates APIs.

![](https://pic.yupi.icu/1/image-20260306110049012.png)

The whole process requires no hand-written JSON config. It’s all visual selection and installation, which is especially beginner-friendly. In Cursor, configuring MCP used to mean hunting down JSON and pasting it yourself. Here, a few clicks and it’s done~

Of course, if you’re experienced, you can still manually configure MCP services through `.vscode/mcp.json`.

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp"
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@microsoft/mcp-server-playwright"]
    }
  }
}
```

This file is not generated automatically. You need to create it yourself, or open it through VSCode’s command palette with `MCP: Open Workspace Folder Configuration`:

![](https://pic.yupi.icu/1/image-20260306110305648.png)

Besides tools, MCP services also support Resources and MCP Apps. Resources can provide AI with context like database tables or API responses. MCP Apps can render interactive UI components like forms and dashboards directly inside the conversation, which is a fantastic experience.

![](https://pic.yupi.icu/1/mcp-apps-flame-graph.png)

In addition, VSCode can automatically discover MCP services already configured in other apps, saving you from repeated setup. Just search `chat.mcp.discovery.enabled` in the chat settings to enable it.

![](https://pic.yupi.icu/1/image-20260306110930161.png)

MCP configuration also supports cross-device sync through Settings Sync. Just check the “MCP servers” option in sync settings, and you won’t need to configure everything again on another machine.

![](https://pic.yupi.icu/1/image-20260306110740774.png)



### Agent Skills - Skill Packs for AI

Agent Skills are capability expansion packs for AI. Unlike the Tools mentioned above, Skills are more like detailed work manuals. They can include operating guides, scripts, example code, and other resources so that AI performs more professionally on specific tasks.

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

For example, you can install a “Web App Testing” Skill for AI, and inside it define a standard process, templates, and best practices for writing Playwright tests. Then when you ask AI to write tests, it follows that standard instead of making things up differently every time.

Note that Skills are an [open standard](https://agentskills.io/). They don’t just work in GitHub Copilot—they can also be used in Claude Code, Cursor, and other AI coding tools. One Skill, many places. That’s one reason they became so popular.

So where do you get Skills?

In most cases, you can directly install Skills other people have already built. For example, my [Yupi AI Navigation Skills collection](https://ai.codefather.cn/skills) includes curated skill packs, and you can also browse GitHub’s [awesome-copilot](https://github.com/github/awesome-copilot) repository, where the community has contributed many practical Skills that are ready to use.

![](https://pic.yupi.icu/1/image-20260306111855649.png)

In VSCode, you can view and manage locally available Skills through the Skills settings button in the chat box:

![](https://pic.yupi.icu/1/image-20260306111219014.png)

Of course, you can also create your own Skills. Through the visual interface, you can choose where to install them—for example, in the current project (usable only by this project), or in the user directory (usable by all projects on your computer):

![](https://pic.yupi.icu/1/image-20260306112025446.png)

The core of creating a Skill is writing the `SKILL.md` file that describes it. For example, below is a sample “Web App Testing” Skill:

```markdown
---
name: webapp-testing
description: 使用 Playwright 测试 Web 应用的指南，当需要创建或运行浏览器测试时使用
---

# Web 应用测试指南

## 创建测试
1. 参考 [测试模板](./test-template.js)
2. 确定要测试的用户流程
3. 在 tests/ 目录创建新的测试文件
4. 使用 Playwright 的定位器来查找元素

## 运行测试
运行命令：npx playwright test

## 最佳实践
- 为动态内容使用 data-testid 属性
- 保持测试独立和原子化
- 使用 Page Object Model 组织复杂页面的测试
```

![](https://pic.yupi.icu/1/image-20260306112358350.png)

After a Skill is created, you can call it manually with a slash command like `/webapp-testing` in the conversation, or let AI automatically match and load it based on the task.

![](https://pic.yupi.icu/1/image-20260306112515795.png)

Skills use a progressive disclosure design. AI only loads the content of a relevant Skill when needed, rather than stuffing all Skills into context at once. That saves tokens while staying flexible. Even if you install dozens of Skills, you don’t need to worry about context explosion.



### Multiple Agent Runtime Modes

In the hands-on demo earlier, we used the local Agent. But in fact, GitHub Copilot supports four Agent runtime modes, each suitable for different scenarios:

| Runtime Mode        | Characteristics                                  | Best For |
| ------------------- | ------------------------------------------------ | -------- |
| Local               | Runs interactively in VSCode with real-time feedback | Exploratory tasks and development requiring immediate feedback |
| Background          | Runs autonomously in the local background using Git worktree isolation | Clear tasks that you want AI to handle while you do something else |
| Cloud               | Runs on a remote server and automatically opens a PR when done | Team collaboration and tasks where you don’t want to use local resources |
| Third-party         | Connects to third-party Agents like Anthropic Claude and OpenAI | Situations where you want a specific vendor’s capabilities |

You can switch between these runtime modes at any time through the dropdown menu at the bottom of the Chat area:

![](https://pic.yupi.icu/1/image-20260306094253979.png)

A pretty slick trick is that you can hand tasks off between different Agents. For example, you can first use a local Agent to create a Plan, and once you’re happy with it, hand it off in one click to a Cloud Agent for execution. It automatically creates a branch, writes code, runs tests, and finally opens a Pull Request for your team to review.

You can also open multiple Agent Sessions at the same time, with each Session handling a different task, and manage them all uniformly in the Sessions list of the Chat panel.

Just like Claude Code can keep multiple terminal tabs open simultaneously, Copilot’s Sessions list lets you manage the status of all AI tasks in one place, which is a workflow strongly recommended in GitHub’s official documentation.

![](https://pic.yupi.icu/1/image-20260306112932393.png)



### Hooks - Scripts Triggered Automatically

Hooks let you automatically run custom scripts at key points in the Agent workflow. Put simply, at certain moments during the Agent’s work, your predefined commands are triggered automatically.

You can view and manage configured Hooks in VSCode settings:

![](https://pic.yupi.icu/1/image-20260306094814153.png)

Currently supported lifecycle events include:

- PreToolUse: triggered before the Agent calls a tool, for example to block dangerous commands like `rm -rf`
- PostToolUse: triggered after the Agent calls a tool, for example to automatically run Prettier on modified code
- SessionStart / Stop: triggered when an Agent session starts and ends (the official event names are `SessionStart` and `Stop`), for example to auto-inject project context at the beginning and generate a work report at the end
- UserPromptSubmit: triggered when the user submits a prompt, for example to audit user requests or inject system context
- SubagentStart / SubagentStop: triggered when a sub-agent starts and finishes, for example to track subtask execution and resource consumption

For example, create a JSON config file under `.github/hooks/` and add the following content:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

![](https://pic.yupi.icu/1/image-20260306113256929.png)

That way, every time the Agent uses a tool to modify a code file, it automatically runs Prettier once to keep code style consistent.

Hooks have many use cases: automatically formatting code, intercepting dangerous commands like `rm -rf` and `DROP TABLE`, and logging every tool call for troubleshooting. Better yet, their configuration format is compatible with Claude Code. So if you already set up Hooks there before, you can reuse them directly.



### Custom Instructions - Make AI Follow Your Rules

Custom instructions are basically rules for AI.

You write your coding conventions, technical preferences, and project agreements in a Markdown file, and AI automatically follows them in every conversation. That means you don’t have to keep repeating things like “use TypeScript” or “don’t name variables a, b, c.”

In fact, this is very similar to `AGENTS.md` in concept. Both use files to tell AI a project’s conventions and agreements. The difference is that Copilot’s instruction file path is `.github/copilot-instructions.md`, and it supports finer-grained file-pattern matching, similar to Cursor Rules.

Creating instructions is easy. In the chat area settings, open “Chat Instructions” and choose where to create the file:

![](https://pic.yupi.icu/1/image-20260306113751454.png)

Or manually create `.github/copilot-instructions.md` in the project root and fill it with content such as:

```markdown
# 项目编码规范

## 代码风格
- 使用语义化 HTML5 元素
- 优先使用 ES6+ 语法（const/let、箭头函数、模板字符串）
- 变量命名使用 camelCase，组件命名使用 PascalCase

## 技术偏好
- 前端框架优先用 React + TypeScript
- CSS 使用 Tailwind CSS
- 测试使用 Vitest

## 代码质量
- 函数和变量名要有意义，能自解释
- 复杂逻辑要加注释
- 用户输入和 API 调用要加错误处理
```

![](https://pic.yupi.icu/1/image-20260306114223424.png)

VSCode supports two kinds of instructions. One is Always-on instructions, which are automatically applied to all conversations. The other is File-based instructions, which use file pattern matching—for example, React component rules for `.tsx` files and testing rules for `.test.ts` files—and only apply when the matching file type is involved.

A YAML front matter structure like the one below is the standard format for File-based instructions. The `description` field explains when the instruction should apply, and the `applyTo` field specifies the file patterns:

![](https://pic.yupi.icu/1/image-20260306121336765.png)

There’s also a nice trick: type `/init` in the chat area, and AI will automatically analyze your project structure and coding style, then generate a custom instruction file for you, saving you from writing one from scratch. This is especially useful when taking over an old project or expanding an existing one, because AI can quickly summarize the codebase’s existing conventions.

![](https://pic.yupi.icu/1/image-20260306100241500.png)



### Custom Agents - Assign Roles to AI

Custom Agents are how you assign different roles to AI. For example, you can create a security reviewer, a test engineer, an architect, and so on. Each role has its own instructions, tool permissions, and behavior rules.

Unlike Custom Instructions, which are global rules AI always follows no matter what you’re discussing, Custom Agents are role switches. Once you choose a particular role, AI works only according to that role’s settings—including which tools it can use and which operations it cannot perform.

There are two ways to create a custom Agent.

One is to open “Custom Agents” in the chat area settings, choose a creation location (current project or user directory), and let VSCode automatically create the corresponding file:

![](https://pic.yupi.icu/1/image-20260306114509869.png)

The other method is to manually write a `.agent.md` file in `.github/agents/`. For example, here’s a writing assistant called `article.agent.md`:

```markdown
---
name: 写作助手
description: 帮助撰写和优化技术文章、项目文档
tools: ['search', 'codebase', 'fetch', 'editFiles']
---

# 写作助手

你是一位经验丰富的技术写作者，擅长把复杂的技术概念讲得通俗易懂。

## 写作风格
- 用口语化的表达，像跟朋友聊天一样
- 段落要短，避免大段文字堆砌
- 适当加入类比和例子帮助理解

## 重要规则
- 先列大纲，确认后再写正文
- 每段都要有明确的主题
- 技术术语第一次出现时要解释
```

![](https://pic.yupi.icu/1/image-20260306121541349.png)

After saving it, this writing assistant will appear in the agent dropdown menu in the chat area. Once selected, AI will work according to the role you defined.

![](https://pic.yupi.icu/1/image-20260306121613414.png)

Custom Agents also have an even more powerful use case called Handoffs. You can define “next action” buttons inside Agent files to let agents pass tasks to each other.

For example, after a planning Agent finishes producing a plan, a “Start Implementation” button can appear at the bottom. Clicking it automatically switches to Agent mode for coding while passing over the full context of the plan:

```yaml
handoffs:
  - label: 开始实现        # 按钮上显示的文字
    agent: agent           # 移交给哪个智能体
    prompt: 按照上面的方案开始编码  # 自动填入的提示词
    send: false            # false 表示不自动发送，等你确认后再发
```

Besides Handoffs, you can also orchestrate collaboration among multiple specialist agents.

Suppose you’re building a new feature and need to first research existing code patterns in the project before writing code. You can create a “feature development” main agent, let it first call a read-only “researcher” sub-agent to analyze related modules and design patterns in the codebase, and then call a “coder” sub-agent to write new code following those discovered patterns. This kind of multi-agent orchestration is especially useful for complex features—each role does its own job, and it’s far more reliable than having one AI randomly hack everything together.

VSCode also supports Claude-format Agent files (placed under `.claude/agents`). So if you previously created custom Agents in Claude Code, you can bring them over directly with seamless compatibility.



### Prompt Files - Reusable Prompt Templates

Prompt Files let you package frequently used tasks into **slash commands** that you can reuse in conversations at any time.

For example, maybe you often need to generate React components, run security reviews, or write unit tests. Normally you’d have to keep typing similar prompts over and over again. With Prompt Files, you don’t need to.

The difference from custom instructions is that instructions apply automatically to all conversations, while Prompt Files are manually triggered by typing `/command-name` in chat, making them better for specific task scenarios.

The creation method is very similar to custom instructions. In the chat area settings, open “Prompt Files” and then choose “Create New Prompt File” from the dialog:

![](https://pic.yupi.icu/1/image-20260306122919311.png)

Then choose where to create it (current project or user directory), and VSCode automatically generates the corresponding file:

![](https://pic.yupi.icu/1/image-20260306123109760.png)

You can also directly create a `.prompt.md` file under `.github/prompts/`. For example, here’s a `/gen-test` command that automatically generates unit tests:

```markdown
---
description: 为当前文件生成单元测试
agent: agent
tools: ['search', 'search/codebase', 'edit/editFiles']
---
为 [${fileBasename}](${file}) 生成单元测试。

- 测试文件放在同目录下：${fileDirname}
- 命名为：${fileBasenameNoExtension}.test.ts
- 测试框架：${input:framework:jest or vitest}
- 参考项目的测试规范：[testing.md](../docs/testing.md)
```

This uses some variables. For example, `${file}` is automatically replaced with the path of the currently open file, and `${input:framework}` means the value comes from what the user enters in a dialog.

![](https://pic.yupi.icu/1/image-20260306123242156.png)

After saving it, typing `/gen-test` in the conversation triggers it. You can also append extra instructions afterward, for example: `/gen-test 只测试登录相关的函数`.

![](https://pic.yupi.icu/1/image-20260306123816437.png)



### Smart Actions - AI Shortcut Operations

Besides the core features above, Copilot also hides many AI shortcuts throughout VSCode called Smart Actions. You don’t need to write prompts for them—just use the right-click menu.

Here are some common ones. You can skip them for now and come back later when needed:

- Auto-generate Commit Message: click the small star icon in the Source Control panel and AI generates a commit message based on your code changes
- Explain code: select some code, right-click “Explain,” and AI tells you what it does
- Generate tests: select code, right-click “Generate Tests,” and AI writes unit tests
- Generate docs: select code, right-click “Generate Docs,” and AI writes documentation comments
- Fix errors: when code has an error, AI automatically pops up a fix suggestion
- Code review: select code, right-click “Review,” and AI performs a code review for you
- Semantic search: enable AI search in the search panel to search code semantically instead of matching raw text only
- AI-assisted rename: when renaming a variable, AI suggests better names based on context

The one I personally use most is auto-generating commit messages. I no longer have to rack my brain over how to word them.

![](https://pic.yupi.icu/1/image-20260306121819177.png)

Each of these little features may seem minor on its own, but together they save a surprising amount of effort.

Congratulations—if you’ve read this far, you’ve already surpassed 99% of the students!



## Final Thoughts

To sum it up, the strongest impression VSCode + GitHub Copilot gives me is **comprehensiveness**.

To be honest, in terms of the ultimate Agent coding experience, Claude Code is still a bit stronger. And in terms of speed of new feature releases and iteration cadence, Cursor remains ahead too.

But Copilot wins by being an all-rounder. From code completion to AI chat, from Agent programming to the MCP ecosystem, from custom instructions to agent orchestration, it basically has all the capabilities an AI coding tool should have—and the experience in each area is quite smooth.

Also, I suspect many people were already using VSCode long before AI became popular. Now they can just install one plugin and seamlessly upgrade into AI coding—no need to switch editors, relearn workflows, or migrate configurations. The barrier to adoption is the lowest of all.

If you’re interested, go give it a try. Don’t forget to grab the free 30-day Pro trial~ And if you’re a student, you can also apply for verification through [GitHub Education](https://education.github.com/pack). Once approved, Copilot Pro becomes completely free with no time limit! Why didn’t this exist when I was in school?

By the way, if you want to use GitHub Copilot for more complex full-stack project practice, you can follow along with Yupi’s latest [AI Hot Topic Monitoring Project](https://www.codefather.cn/course/2026625439052627970). I’ve already tested it for everyone—Copilot can absolutely handle enterprise-level large projects too.

![](https://pic.yupi.icu/1/image-20260304102630302.png)

That’s it for now. If you found this helpful, remember to bookmark the article, and feel free to chat in the comments about which AI coding tool you like most so more students can make better choices.



## Recommended Resources

1) Yupi’s AI Navigation site: [A complete collection of AI resources, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussions and Q&A](https://www.codefather.cn)

3) Programmer interview cheat sheet: [High-frequency topics for internships / campus hiring / experienced hiring, plus real interview question analysis](https://www.mianshiya.com)

4) Resume builder for programmers: [Professional templates, rich example phrases, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships / campus hiring / experienced hiring](https://ai.mianshiya.com)
