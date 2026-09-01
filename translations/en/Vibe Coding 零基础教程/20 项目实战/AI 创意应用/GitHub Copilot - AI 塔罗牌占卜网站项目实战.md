# GitHub Copilot - AI Tarot Reading Website Project Practice

This is an AI tarot reading website developed from 0 to 1 using VSCode + GitHub Copilot’s Plan mode + Agent mode. Through this project, you can quickly experience GitHub Copilot’s core AI coding capabilities and build a small project with card-flipping animations, AI-generated tarot interpretations, and a mysterious, gorgeous interface in just a few minutes.

Estimated learning time: 30 minutes. It’s great for complete beginners getting started with AI programming in VSCode + GitHub Copilot.

If you want to learn more core GitHub Copilot features (MCP, Agent Skills, custom agents, and more), you can read *VSCode + GitHub Copilot: AI Programming Practice with Microsoft’s Full Toolkit* in the programming tools section of this tutorial series.



## Project Overview

The user enters a question (for example, “How is my love life looking recently?”). After clicking **Start Reading**, the site shows a card-flipping animation for 3 tarot cards. Once the cards are revealed, it calls the DeepSeek large-model API to generate an AI tarot interpretation based on the drawn cards.

The interface uses a dark purple theme with golden textures and a starry-sky background, paired with smooth card-flipping animations. It also uses a responsive layout so it works on mobile too.

The tech stack is very simple: HTML + CSS + JavaScript, plus a call to the DeepSeek API to generate the reading.

![](https://pic.yupi.icu/1/image-20260305151413007.png)



## Install VSCode + GitHub Copilot

Before starting the project, you need to install the development tools first.

1) Go to the [VSCode official website](https://code.visualstudio.com/) to download the installer, then just go through the normal installation.

![](https://pic.yupi.icu/1/image-20260305141229310.png)

2) Open VSCode, click the **Extensions Marketplace** icon on the left, search for `GitHub Copilot`, and install the official AI coding extension.

![](https://pic.yupi.icu/1/image-20260305141416199.png)

You can also install the Chinese language pack if needed:

![](https://pic.yupi.icu/1/image-20260305153013870.png)

3) After installation, click the Copilot icon in the VSCode status bar at the bottom and follow the prompts to sign in to your GitHub account.

![](https://pic.yupi.icu/1/setup-copilot-status-bar.png)

If you don’t already have a Copilot subscription, it will automatically put you on the **Copilot Free** plan, which includes a certain monthly quota for AI chat and code completion, making it easy to get started with zero barriers. If you want the full experience, Copilot Pro offers a 30-day free trial for new users. If you’re a student, you can also apply for verification through [GitHub Education](https://education.github.com/pack), and once approved, Copilot Pro is completely free.

Once installation and setup are done, you’re ready to build the project.



## Development Workflow

This project is a perfect demonstration of GitHub Copilot’s Plan + Agent workflow.

### Step 1: Use Plan to Make a Proposal

Create a new empty project folder (for example, `ai-diviner`) and open it in VSCode. The Chat panel should open by default.

![新建项目](https://pic.yupi.icu/1/image-20260305144504583.png)

In the agent selector in the chat area, choose Plan mode and select a model (for example, Claude Opus), then enter your requirements:

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

![Plan模式执行AI](https://pic.yupi.icu/1/image-20260305144551103.png)

After selecting Plan mode, AI won’t start writing code right away.

It will first study your requirements and may ask a few questions, such as whether the AI interpretation should “call a large-model API” or “randomly generate from a preset copy library.”

You just need to tell AI your thoughts as if you were chatting normally. For example, you can say you want to call the DeepSeek large-model API:

![](https://pic.yupi.icu/1/image-20260305144900988.png)

If you aren’t sure yourself, you can ask AI to analyze the pros and cons of different approaches, or just let it decide on its own.

Once AI understands your requirements, it will provide a structured implementation plan.

![](https://pic.yupi.icu/1/image-20260305145315374.png)

The plan will list which files need to be created, what each file is responsible for, the order of implementation steps, and how to verify the results. At this stage, you can keep discussing and adjusting the plan with AI until you’re satisfied.

![](https://pic.yupi.icu/1/image-20260305145352874.png)

The essence of Plan mode is a 4-stage iterative workflow: requirement research → question alignment → solution design → iterative refinement. AI first uses read-only tools to deeply study your codebase, then removes ambiguity through interactive Q&A, and only then produces a proposal draft.

This is actually the standard process of software development. Even if you don’t use Copilot’s built-in Plan mode, you can still guide AI with prompts to design a plan first, manually confirm it, and only then start implementation—building the good habit of **thinking things through before you start coding**.



### Step 2: Use Agent to Execute the Plan

Once the plan looks good, click the **Start Implementation** button below the plan and let AI automatically carry it out until the solution is implemented.

![](https://pic.yupi.icu/1/image-20260305145604534.png)

During execution, the Agent automatically manages a Todos task list to track progress. You can clearly see what the Agent is doing, such as creating `index.html`, `style.css`, and `script.js`, writing code into them, and even opening the terminal to run commands automatically.

![](https://pic.yupi.icu/1/image-20260305145807776.png)

If AI needs to run terminal commands or use certain tools, it will pop up a confirmation dialog for your approval, so security is protected.

![](https://pic.yupi.icu/1/image-20260305150107141.png)

You can also keep sending messages while the Agent is working, choosing whether to queue them, interrupt immediately, or guide AI to adjust direction.

If you’re new to AI coding, I recommend spending some time observing how AI works. If you notice it going in the wrong direction, step in early. That can save Tokens and avoid rework.



### Step 3: Check the Result

A few minutes later, the Agent not only completed the development task, but also started a Web server with Python and helped run the site.

![](https://pic.yupi.icu/1/image-20260305150430976.png)

Good grief—it really doesn’t want me to do even one extra step. At this rate, sooner or later I’m going to regress to the `Hello World` level.

Still, I prefer testing in Chrome, so I copied the URL into my browser and entered the large-model API Key I got from the [DeepSeek Open Platform](https://platform.deepseek.com/api_keys):

![](https://pic.yupi.icu/1/image-20260305150858949.png)

![](https://pic.yupi.icu/1/image-20260305150957888.png)

Then I entered a question to test my love luck this year and clicked **Start Reading**:

![](https://pic.yupi.icu/1/image-20260305151027082.png)

The three tarot cards flipped over one by one, and below them appeared the AI-generated reading. The dark purple starry-sky background, golden borders, and smooth card-flipping animation really do make it feel convincing.

![](https://pic.yupi.icu/1/image-20260305151413007.png)

I feel like I could open my own little tarot booth now. Probably not an illusion...

![](https://pic.yupi.icu/1/image-20260305151303905.png)

If you aren’t happy with some details on the page, you can click the **element selector** button in the built-in browser, click whatever bothers you, and then write a prompt in the Chat box, for example:

```
改为鱼皮塔罗
```

![](https://pic.yupi.icu/1/image-20260305151754685.png)

The Agent will automatically locate the corresponding code and make a precise change. After that, just refresh the preview.

![](https://pic.yupi.icu/1/image-20260305152037670.png)

The whole process—from writing the requirements to getting a finished product—only took a few minutes. Back in the day, if I had written a tarot site with animations like this from scratch by myself, it would’ve taken at least an entire afternoon.

You can keep talking with AI to add more features. Throughout the process, be sure to watch your **context usage**. If the context gets full, AI may lose track and start editing randomly.

![](https://pic.yupi.icu/1/image-20260305152200805.png)

So when the context is getting close to full, it’s best to have AI consolidate the current project information into documentation. That way, whenever you open a new AI chat window later, you can just hand the historical docs to AI and help it quickly recover its memory.



## What You’ll Gain from This Project

Through this small project, you can learn:

- how to use GitHub Copilot’s Plan mode for requirement analysis and solution design
- how to use Agent mode to let AI autonomously complete code development
- how to call the DeepSeek large-model API
- how to use CSS to build card-flipping animations and a starry-sky background
- how to intervene manually and make fine-grained adjustments during AI coding
- how to manage context usage and avoid AI memory loss

Although this project is small, it fully demonstrates the core Vibe Coding workflow: describe requirements in natural language, let AI help design the plan and write the code, then manually review and refine the details. Once you master this workflow, you can use the same approach for more complex projects.
