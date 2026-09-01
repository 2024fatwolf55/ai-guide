# Cursor Beginner-Friendly Tutorial: One Article to Get Through Your First AI Programming Lesson

Competition among AI programming tools has already entered a fierce stage. Abroad, you have the three giants Cursor, Claude Code, and Codex. In China, you have ByteDance’s TRAE, Alibaba’s Qoder, and Tencent’s CodeBuddy.

Among them, Cursor was actually one of the earliest products I personally paid for. Although people complain about it nowadays because of the price and other factors, it’s still a very capable mainstream AI programming tool, and it updates crazy fast.

![](https://pic.yupi.icu/1/1_cursor.png)

I’ve used Cursor to build quite a few projects, and it’s also the one I’ve spent the most money on. In this article, I’ll start from installation and take you through using Cursor to build a complete website project from scratch, so you can experience the full AI programming workflow. After reading it, you’ll be able to use Cursor independently for all kinds of AI programming tasks.

This article is packed with useful content, so I recommend bookmarking it and reading it somewhere quiet~



## 1. Installation and Basic Preparation

### Download and Install

Open the [Cursor official website](https://cursor.com). It automatically detects your operating system, so you can just download the installer and keep clicking Next. It’s as simple as installing WeChat.

![](https://pic.yupi.icu/1/image-20260604161516577.png)

After installation, open Cursor and register an account. I recommend signing up with your GitHub account, because later when you build projects, you’ll likely use GitHub for code management and deployment, so it’s more convenient to link it in advance.

![](https://pic.yupi.icu/1/image-20260604161539548.png)



### Two Interfaces

Cursor provides two sets of interfaces.

One is called **Agent Window**. Looks familiar, doesn’t it?

It’s similar to the AI chat tools you already use every day: project and conversation management on the left, chatting with AI in the center. It’s especially friendly for beginners.

![](https://pic.yupi.icu/1/image-20260604161607946.png)

The other is called **Editor Window**, which is a full code editor interface: files on the left, code in the center, AI chat on the right, and the terminal at the bottom. It’s more suitable for managing complex code projects.

![](https://pic.yupi.icu/1/image-20260604161653209.png)

You can open both interfaces at the same time and switch between them whenever you want. For beginners, I suggest starting with Agent Window because the interface is simpler and has almost zero learning barrier. Once you’re more familiar with Cursor, then switch over to Editor Window.



### Free Version and Paid Version

Cursor provides a free Hobby plan by default, which lets you try its basic AI chat functionality, but the model capability and usage quota are limited.

If you want to seriously learn AI programming, I recommend at least subscribing to the Pro plan, which costs $20 per month (about 150 RMB). The more advanced Pro+ and Ultra plans mainly increase your usage quota. Functionally they’re the same as Pro, so you can just upgrade later if you run out.

![](https://pic.yupi.icu/1/image-20260604161759761.png)



### Choosing an AI Model

Cursor Pro users can freely choose their AI model. Cursor supports mainstream overseas models such as Claude, GPT, Gemini, and Grok. You can switch them with one click in the model selector of the chat panel, and you can also adjust the model’s reasoning level.

![](https://pic.yupi.icu/1/image-20260604161830863.png)

If you don’t know what to choose, just use **Auto** mode. Cursor will automatically pick a suitable model for you, which saves both money and effort. Once you get more experienced, you can switch manually based on task complexity—for example, using a cheaper faster model for simple tasks and a stronger model for complex ones.

![](https://pic.yupi.icu/1/image-20260604161906303.png)

Alright, the preparation is done. Next, let’s officially try Cursor’s AI capabilities.



## 2. Get to Know Cursor’s Capabilities

### First Taste of Agent Mode

When you open a new conversation, it starts in Agent mode by default. This is Cursor’s most core and most commonly used mode. AI can analyze requirements, create files, call tools, write code, and run commands all by itself, completing the whole task end to end.

Let’s start with a simple one and ask AI to generate an HTML report page about AI programming news:

```plain
今天有哪些值得关注的 AI 编程热点？
总结为一份 HTML 网页报告
```

AI automatically searches the web for the latest information, summarizes it for you, and generates an HTML webpage file.

![](https://pic.yupi.icu/1/image-20260604161950784.png)

Take a look at the result. With just one sentence to AI, the world’s hottest news is in your hands~

![](https://pic.yupi.icu/1/image-20260604162054901.png)



### Other Interaction Methods

Besides Agent mode, Cursor also offers several lighter interaction methods.

**Ask mode** is pure Q&A. It runs quickly, but it can’t modify files, so it’s good when you want to understand some concept or ask AI to explain a piece of code.

![](https://pic.yupi.icu/1/image-20260604162242454.png)

When you code in editor mode, AI can also predict what you want to write next. Press Tab to accept the suggestion and enter a “Tab, Tab, Tab” rhythm of continuous completion.

![](https://pic.yupi.icu/1/image-20260604162414383.png)

If you select a piece of code and press `Cmd+K` (Mac) or `Ctrl+K` (Windows), a small dialog pops up so you can ask AI to modify code right at that location. It’s a lighter-weight interaction style.

![](https://pic.yupi.icu/1/image-20260604162514930.png)

That said, once you have Agent mode, in most scenarios you barely need to write code manually anymore. Agent mode is Cursor’s true killer feature. Next, let’s use it to build a complete project.



## 3. AI Programming Practice — Webpage Summarizer Tool

### Clarify What You Want to Build

The first step of any project is always requirement analysis. You must first figure out what you want to build.

The function of this tool is simple: the user inputs a URL, and AI automatically extracts the webpage content and generates a summary so you can quickly understand the core ideas of an article without reading it word by word.

I personally read lots of overseas technical blogs and news, so a tool like this is genuinely convenient.



### Plan Mode — Think It Through Before Building

Create an empty folder to serve as the project directory. Ideally the path should be in pure English, because Chinese paths sometimes cause weird compatibility issues.

Then open that folder in Cursor’s Editor Window, and switch the chat panel to **Plan** mode (you can quickly switch modes with `Shift+Tab`).

![](https://pic.yupi.icu/1/image-20260604162640727.png)

The advantage of Plan mode is that AI first helps you think through the solution, generating an implementation plan before writing any code. This avoids the common problem of AI rushing in and writing random stuff right away.

Let’s assume I know absolutely nothing about technology and just throw the requirement to AI:

```plain
帮我开发一个网页总结工具，功能如下：

1. 用户在页面上输入一个网址
2. 点击按钮后，自动提取该网页的内容
3. 然后用 AI 对内容进行总结概括，生成简洁的摘要
4. 支持中英文网页，结果都用中文展示
5. 界面要简洁美观，有加载动画

请先帮我规划一下整体的技术方案和实施步骤
```

AI analyzes the requirements and, if anything is unclear, asks you to confirm through follow-up prompts. It then outputs a detailed implementation plan, including the tech stack, file structure, and task list. You don’t need to understand every technical term it mentions—just skim it and see whether it feels reasonable.

![](https://pic.yupi.icu/1/image-20260604162743435.png)



### Agent Autonomous Development

Once the plan looks fine, click the “Build” button in the conversation, and AI starts executing the plan on its own.

It automatically creates project files, writes the frontend page, writes the backend API, and configures the AI model integration. If multiple steps can proceed in parallel, Cursor may even launch multiple sub-Agents to speed things up.

![](https://pic.yupi.icu/1/image-20260604162815059.png)

After a few minutes, AI finishes the implementation. It will also automatically run the project and open the webpage in Cursor’s built-in browser panel, so you can preview the result directly without switching to an external browser.

![](https://pic.yupi.icu/1/image-20260604162844304.png)



### Testing and Verification

Once the project is running, AI tells you what you still need to prepare. Since our project uses the DeepSeek model API for summarization, you first need to go to the DeepSeek Open Platform, get an API Key, and fill it into the project’s environment variable file.

![](https://pic.yupi.icu/1/image-20260604162915371.png)

Then let’s test the effect. I input a URL for an article, click the summarize button, and AI quickly gives a pretty solid summary.

![](https://pic.yupi.icu/1/image-20260604162946718.png)

But I noticed that some websites could not be extracted and summarized correctly...

![](https://pic.yupi.icu/1/image-20260604163108311.png)

Testing them one by one manually is too troublesome, so we can let AI test and fix the issue itself.

Use `@Browser` to invoke Cursor’s built-in Browser Use capability:

```plain
请你自主测试和修复 AI 提取和总结功能，确保兼容大多数网站
比如当我输入 https://ai.codefather.cn 时，报错：未提取到足够正文
```

![](https://pic.yupi.icu/1/image-20260604163149159.png)

AI first analyzes the current code, then uses terminal commands to reproduce the bug, fixes the code, and even launches a sub-Agent to open the browser and verify the result automatically.

![](https://pic.yupi.icu/1/image-20260604163216526.png)

After the fix, try again—and this time it can summarize correctly.

![](https://pic.yupi.icu/1/image-20260604163242010.png)

After each task execution is complete, you can review the code changes and keep or revert specific modifications as needed, or simply click Keep to keep all changes. I recommend clicking Keep after each verified feature.

![](https://pic.yupi.icu/1/image-20260604163307654.png)



### Iterative Optimization

The core mindset of AI programming is **build first, then iterate**. Once version one is done, keep adjusting through multiple rounds of conversation until you’re satisfied.

In this process, there are several important Cursor tips worth highlighting.



#### Use `@` to Provide Precise Context

Type `@` in the chat box, and you can precisely reference what you want AI to use. For example, `@filename` references a project file, `@Docs` references indexed official docs, and `@Terminals` references current terminal error output.

![](https://pic.yupi.icu/1/image-20260604163359832.png)

For example, if you want to beautify the site using the Ant Design component library, you can use `@Docs` to provide Ant Design’s official documentation, and AI can then write code based on the latest docs instead of hallucinating outdated syntax.

You can also drag files directly into the chat box. For example, if I drag in my own product info document, then AI knows what information to show when generating the footer copyright recommendation section.

![](https://pic.yupi.icu/1/image-20260604163419853.png)

Cursor also supports dragging images directly into the chat. For example, if you like Apple’s design style, just paste in a screenshot and tell AI to use it as a reference.

![](https://pic.yupi.icu/1/image-20260604163438613.png)

After running prompts like these, the website gets optimized into something like the following—not bad, right~

![](https://pic.yupi.icu/1/image-20260604163550109.png)



#### Checkpoints for Snapshot Rollback

During iterative modification, it’s inevitable that AI sometimes makes things more and more chaotic, or gets stuck on a bug it just can’t solve.

That’s when Cursor’s snapshot rollback becomes useful. Every Agent modification automatically saves a snapshot. You just hover over an earlier message in the conversation history and click the rollback icon to instantly restore the code state from that moment.

![](https://pic.yupi.icu/1/image-20260604163729304.png)

It’s like a game save system—you can always reload when things go wrong.



#### View Usage

After all these operations, how much AI quota did we consume?

In the lower-right corner of the conversation panel, you can see current context usage, including how many Tokens were consumed and how different parts of the context are distributed.

![](https://pic.yupi.icu/1/image-20260604163751198.png)

You can also open the [Cursor dashboard](https://cursor.com/dashboard) to view detailed usage over time. I recommend setting a cap on monthly pay-as-you-go usage so you don’t go bankrupt.

![](https://pic.yupi.icu/1/image-20260604163907596.png)

Congratulations—by this point, you’ve already used AI to build a complete web app from scratch!



## 4. Make Cursor Stronger — Extending Its Capabilities

Cursor is already powerful on its own, but it also has an extension system that lets AI connect to external tools, fetch up-to-date information, and follow your coding conventions.

![Cursor plugin system](https://pic.yupi.icu/1/image-20260604163937041.png)



### MCP — Let AI Connect to the Outside World

MCP stands for Model Context Protocol. It sounds intimidating, but you can think of it as a universal plug for AI. Normally, AI can only answer and generate code based on training data. With MCP, it can connect to all kinds of external tools and data sources—such as checking the weather, operating a database, or planning travel routes.

![](https://pic.yupi.icu/1/mcp%E6%9E%B6%E6%9E%84%E5%9B%BE.png)

For example, to install the Amap MCP, you just need to apply for an API Key from the Amap open platform and configure it once in Cursor’s settings:

```json
{
  "mcpServers": {
    "amap-maps": {
      "url": "https://mcp.amap.com/mcp?key=你的API_KEY"
    }
  }
}
```

![](https://pic.yupi.icu/1/image-20260604164139668.png)

After configuration, you can see the list of tools provided by the MCP server inside Cursor’s settings panel:

![](https://pic.yupi.icu/1/image-20260604164305442.png)

Let’s try it. Tell AI directly: use Amap to help me plan a two-day weekend trip in Shanghai, check tomorrow’s weather, and recommend suitable attractions.

![](https://pic.yupi.icu/1/image-20260604164341317.png)

AI then automatically calls Amap’s tools and combines the results into a complete travel plan.

![](https://pic.yupi.icu/1/image-20260604164403560.png)

For example, when I analyze my own product data nowadays, I use a database MCP so AI can query the database directly for me, saving me from writing SQL manually.



### Skills — Install Skill Packs for AI

You can think of Skills as skill packs for AI. Once a certain skill is installed, AI can automatically follow that method whenever it encounters related tasks, so you no longer need to write long prompts every time. And Skills are loaded on demand, so they only consume context when actually needed.

![](https://pic.yupi.icu/1/04_Agent_Skills%E6%8A%80%E8%83%BD%E5%8C%85%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8A%AB%E9%9C%B2_original_v2%E5%A4%A7.jpeg)

Some commonly used skills in AI programming include Firecrawl for web search, Context7 for the latest technical documentation, and UI UX Pro Max for beautifying frontend pages.

Installing a skill is simple. Take Firecrawl as an example: just copy a one-line install command from its official site, run it in the terminal, and follow the authorization steps.

![](https://pic.yupi.icu/1/image-20260604164539466.png)

After installation, you can invoke it in a conversation with `/firecrawl`:

```plain
/firecrawl 鱼皮的 AI 导航有哪些资源？
```

You’ll notice that Firecrawl currently works better than Cursor’s built-in web search and returns more complete results.

![](https://pic.yupi.icu/1/image-20260604164606348.png)

Cursor also has a built-in `/create-skill` command so you can create your own skills. For example, if you just built a webpage summarizer tool and feel that workflow will be useful again in the future, you can ask AI to package that workflow into a skill.

![](https://pic.yupi.icu/1/image-20260604164634591.png)



### Rules — Constrain AI’s Behavior

When building projects with Cursor, you may notice that AI’s coding style does not always match your preferences. For example, maybe you want comments written in Chinese, but AI keeps writing them in English.

The simplest solution is to create an `AGENTS.md` file in the project root and write the rules you want AI to follow in Markdown:

```markdown
## 编码规范

- 所有代码注释使用中文
- 使用 TypeScript 而非 JavaScript
- 变量命名使用驼峰式（camelCase）
```

After saving it, AI will automatically follow these rules when working in the current project.

![](https://pic.yupi.icu/1/image-20260604164704104.png)

This file is not unique to Cursor. Mainstream tools such as Claude Code and Codex will read it too, so one set of rules can work across multiple tools.

If you need more precise control over when rules should apply, Cursor also has a dedicated rules system.

In the Rules settings panel, you can create rules for specific file types or let AI determine intelligently whether a rule is needed.

![](https://pic.yupi.icu/1/image-20260604164827576.png)

But for beginners, `AGENTS.md` is already more than enough.



## 5. Quick Tour of Advanced Features

At this point, you’ve already learned the most important everyday Cursor features.

In addition, Cursor has quite a few advanced capabilities. You don’t need to study them deeply yet—just know they exist, and come back to them when you run into relevant scenarios.

1) **Cloud Agent**: the Agents we used earlier all run on your own computer. Cursor also has a Cloud Agent that runs on cloud servers and can keep working even after you shut down your computer. It’s suitable for time-consuming jobs like large-scale refactoring. You can even open a webpage on your phone and check progress anytime.

![](https://pic.yupi.icu/1/image-20260604165027452.png)

2) **Automations**: you can set timed or event-triggered automated tasks. For example, ask AI to summarize project progress every morning at 9 a.m. and generate a report, or automatically perform code review whenever someone pushes code to a GitHub repository.

![](https://pic.yupi.icu/1/image-20260604165053532.png)

3) **Marketplace**: Cursor has its own official plugin marketplace, with plugins for turning Figma designs into code, deploying to AWS, integrating Notion knowledge bases, and much more. One-click install, then use.

![](https://pic.yupi.icu/1/image-20260604165114110.png)

4) **Code indexing**: Cursor automatically analyzes the whole repository and builds a semantic index, allowing you to quickly search any corner of the project through conversation. This is especially useful for learning open-source projects—just open the repo in Cursor and ask AI to analyze the architecture.

![](https://pic.yupi.icu/1/image-20260604165222081.png)

5) **Git integration**: Cursor comes with a built-in Git panel, where you can inspect code changes, commit history, and revert edits without opening the terminal.

For now, you don’t need to study Git deeply. Just think of it as the “undo pill” for code.

![](https://pic.yupi.icu/1/image-20260604165247952.png)

6) **VS Code extensions**: because Cursor is built on VS Code, it is compatible with all VS Code extensions. You can even install Claude Code and Codex extensions and use multiple AI programming tools inside the same editor.

![](https://pic.yupi.icu/1/image-20260604165333167.png)



If you want to systematically learn Cursor and multiple AI programming tools through video, and use AI to build several complete enterprise-grade projects from scratch, you can check out Yupi’s latest [AI Programming Practice for Complete Beginners](https://www.bilibili.com/cheese/play/ss475098271) video course. It contains a more complete beginner-friendly Cursor video tutorial plus multiple enterprise project practice courses.



## 6. My Experience Using Cursor

Finally, let me talk a bit about my own experience using Cursor.

First, Cursor’s feature set is extremely complete. From code completion, to Agent programming, to cloud management—it has basically every capability you’d want for AI programming. It also supports many models, so you can switch between Claude, GPT, and Gemini freely. Since it’s based on VS Code, its plugin ecosystem is also mature, which makes it easy to find solutions when something goes wrong.

If there’s a downside, it’s that the price really isn’t cheap. The Pro plan is $20 per month, and for heavy users like me, actual spending is often well above that. But for people who are serious about building projects, the efficiency improvement is worth the investment.

Because Cursor updates its interface relatively frequently, don’t worry if what you see looks a little different from my screenshots. The core operations are the same. Just poke around and explore a bit.

There are plenty of similar AI editors on the market now, but their core working style is quite similar. Once you learn Cursor, you’ll be able to pick up the others much more easily too.



## Final Words

That’s the full Cursor tutorial from installation to practice, covering the most commonly used features and techniques in everyday AI programming.

Once you learn these, you’ll be able to use Cursor independently through the entire flow—from requirement analysis and code development to testing and deployment.

If you want to continue learning more AI programming tools and practical techniques, you can read the other articles in this tutorial’s programming tools section.
