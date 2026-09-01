# Codex - AI Open-Source Project Learning Website Project Practice

This project is an AI-driven open-source project learning assistant. Users enter a GitHub repository URL, and the system automatically analyzes the source code and generates a plain-English report that’s easy to understand. It also supports interactive Q&A about the source code. The whole project was developed using Codex + GPT-5.5, with the backend connected to the DeepSeek V4 API.

Hello everyone, I’m Yupi.

The AI world has really been wild lately. On April 23, OpenAI released GPT-5.5, and then DeepSeek followed the very next day with V4. Two heavyweight models launched back to back.

![](https://pic.yupi.icu/1/image-20260428152723505.png)

Looking only at benchmark scores isn’t that meaningful. Whether a model is actually useful has to be tested with real projects.

Coincidentally, OpenAI’s Codex desktop app has been updating aggressively lately. It has already evolved from a pure AI coding tool into a “super app” with Computer Use, a plugin marketplace, and a built-in browser.

So in this article, I’ll use Codex + GPT-5.5 from start to finish to build a complete full-stack project, with the backend connected to DeepSeek V4’s API for the AI capabilities.

By the end of this episode, you’ll learn how to use Codex, get a feel for the real capabilities of the new model, and pick up practical AI coding techniques—three wins in one.

Hit save, and let’s begin~



## Requirement Analysis

The project we’re building this time is called **Project Learning Assistant** (`project-helper`), and the core requirement is simple:

The user enters a GitHub repository URL, and the system automatically clones the project and analyzes the source code, generating a complete analysis report in plain language that’s easy to understand. The report covers the project overview, tech stack, directory structure, core modules, data flow, design patterns, reading suggestions, and more—truly making it “understandable even for a beginner.” The analysis process pushes progress in real time, and projects that have already been analyzed are cached so they don’t need to be analyzed again.

![](https://pic.yupi.icu/1/image-20260427152036161.png)

In addition, users can ask interactive questions about the source code. AI autonomously searches the code and reads files to answer questions, and supports streaming output.

That way, you can quickly learn any open-source project. Even if you’re facing a repo with tens of thousands of lines of code, you won’t be intimidated.



## Solution Design

If you have absolutely no technical background, you can let AI help you design the solution.

But here, to save time and tokens, I directly told AI how to do it.

The project uses a separated frontend-backend architecture:

- backend with Python FastAPI + LangChain + SQLite
- frontend with Vue
- AI capabilities connected to the DeepSeek V4 API

There are also a few tricks to implementing AI analysis and AI Q&A. If a code repository has tens of thousands of lines, are you really going to dump the entire thing into AI and let it analyze everything blindly?

My approach is to use AI Tool Use. I provide AI with tools for reading files, searching code, and getting the repository structure, then leave it to AI to decide which files to inspect and how to organize the answer. This is also exactly the kind of Agentic scenario that DeepSeek V4 has been specially optimized for.

![](https://pic.yupi.icu/1/image-20260427143741108.png)



## Environment Setup

### Codex Configuration

Open Codex and first make sure GPT-5.5 appears in the model list. If you can’t see it, it’s probably an account issue, and you may need a higher-tier subscription. I’m using the Plus plan here.

![](https://pic.yupi.icu/1/1777256418373-5682599c-2367-4f94-951a-43bab6f0f861.png)

You can see that GPT-5.5 is already available in the interface, and it also supports adjusting the intelligence level (low / medium / high / very high). I chose **High**.

Go into settings from the bottom-left corner and switch the work mode to **for programming**. That makes AI’s responses more professional and better suited to development scenarios:

![](https://pic.yupi.icu/1/1777259578973-cbe093c8-ea7d-4d5e-897a-afd81222dd30.png)



### Install AI Extensions

Codex’s AI extensions mainly fall into three categories:

- MCP services, used to connect to external tools
- Agent Skills, which teach AI specific professional skills
- Plugins, which give AI even more abilities

The official app already comes with some built-in plugins and skills, such as Computer Use, Browser Use, PDF processing, presentation editing, and more:

![](https://pic.yupi.icu/1/1777257188480-f3405539-10b4-49bf-b612-10f6e4f5fb50.png)

![](https://pic.yupi.icu/1/1777257208664-88183795-3fb8-4862-92fe-bb2d877430e3.png)

However, the few extensions needed for this project are not included by default in Codex, so you need to install them yourself.

We need these 3 extensions:

1. Firecrawl: web search and webpage scraping, so AI can get the latest technical information
2. Context7: query the latest technical documentation and API usage, reducing hallucinated code
3. UI UX Pro Max: a frontend beautification skill that makes generated pages look more polished

You can manually add MCP services in Codex settings:

![](https://pic.yupi.icu/1/1777257301111-de539209-39d3-4956-86ba-9e43c7991cad.png)

But you have to fill in a whole pile of parameters by hand. What a pain.

![](https://pic.yupi.icu/1/1777257751584-4842f03a-fa07-4cbe-94ad-dce017977b66.png)

Although you can also directly edit the `~/.codex/config.toml` file to add MCP services, that’s still a hassle.

In this regard, Codex’s experience is not as smooth as Copilot and Cursor, both of which support more visual installation. Copilot even integrates MCP directly into the VSCode extension marketplace, where you can just search and install in one click.

Fortunately, there’s another way: use the commands provided by each AI service to install them quickly.

#### 1. Install Firecrawl

Firecrawl is a web search and webpage scraping tool. It lets AI search for the latest technical information and docs before development begins. In this project, we need it to look up the latest API usage for DeepSeek V4.

Open the terminal and enter the following command:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

![](https://pic.yupi.icu/1/1777258212308-8c83d23e-338e-4ec2-b1c0-05f54a22a36e.png)

After execution, the browser opens automatically. You need to click authorize on the popup page:

![](https://pic.yupi.icu/1/1777258069152-2d7fdb02-64e2-440b-bcbd-6254b07fb74e.png)

Once installation is complete, it automatically registers 12 related skills:

![](https://pic.yupi.icu/1/1777258235867-0f6f08f5-4791-4b66-84b7-50936912540d.png)

Then, in Codex’s skill management, you can see the newly added Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777258331237-182161c5-d21b-4a9b-9c6a-855d99312b5e.png)



#### 2. Install Context7

Context7 is a technical documentation query tool that lets AI access the latest official docs for various frameworks and libraries, avoiding outdated APIs when writing code.

First, install it by entering a single command in the terminal:

```bash
npx ctx7@latest setup
```

It will ask whether to install the MCP service or CLI + Skills. Here I chose CLI + Skills. You’ll notice that more and more tools are shifting from MCP to a CLI + Skills approach:

![](https://pic.yupi.icu/1/1777258448310-41f86ec3-26e1-476e-aed5-4913c8116d21.png)

As before, authorize it in the webpage that pops up. There’s no need to manually obtain and enter an API Key—super convenient!

![](https://pic.yupi.icu/1/1777258547209-dc872280-09eb-4bd9-ad45-2e412382002d.png)

Then choose which AI coding tool to install it for. I chose Codex:

![](https://pic.yupi.icu/1/1777258572107-f494c3bb-01a9-443d-ba1d-6b1a3b3fab9a.png)

Installation successful:

![](https://pic.yupi.icu/1/1777258672897-259f035a-f365-46ce-bc5d-e33fbc839f34.png)

Confirm the installed skills inside Codex:

![](https://pic.yupi.icu/1/1777258710387-4b47a05d-dcb1-43ce-9761-f5d28976731e.png)

Of course, you can also choose the MCP Server installation method:

![](https://pic.yupi.icu/1/1777259105649-99e28db3-c43e-4c49-a3b3-c567fa592d1f.png)

After installation, you’ll see Context7 MCP in Codex’s MCP server settings. Isn’t that much easier than filling in parameters manually yourself?

![](https://pic.yupi.icu/1/1777259122962-393ac901-870c-4b8b-bcf4-742e39a90c5a.png)



#### 3. Install UI UX Pro Max

This is a frontend beautification skill package that makes AI-generated pages feel more designed and avoids stuffing them with a ton of Emojis.

Enter one command:

```bash
uipro init
```

Choose to install the Skill for Codex:

![](https://pic.yupi.icu/1/image-20260427143633213.png)

Installation successful:

![](https://pic.yupi.icu/1/1777258832043-8a3230db-2a76-47f7-a32a-5113a0487631.png)

In Codex’s skill management, you can see the new skill:

![](https://pic.yupi.icu/1/1777258847545-ba145ccf-2ab3-4a37-948a-4bb48d228fe4.png)

At this point, the environment setup is complete! The next time you build a project, you won’t need to repeat all this preparation~



## Development

Create a new project folder named `project-helper` and open it in Codex:

![](https://pic.yupi.icu/1/1777259374913-7c4ecded-191b-4010-820a-fe8c31ab3da9.png)

Then enter your prompt. I’ll share the actual prompt I used here for reference:

```markdown
## 角色

你是一个全栈工程师，擅长 Python + FastAPI + LangChain 开发。

## 任务

开发一个叫 project-helper（项目学习助手）的 Web 应用，帮助用户快速读懂任意开源项目的源码，傻子也能懂。

用户输入一个 GitHub 仓库地址，系统自动克隆项目并分析源码，生成一份通俗易懂的完整分析报告，涵盖项目概述、技术栈、目录结构、核心模块、数据流、设计模式、阅读建议等。分析过程实时推送进度，已分析过的项目自动缓存，无需重复分析。

用户还可以针对源码进行交互式问答，给 Agent 提供读取文件、搜索代码等工具，让 AI 自主查找代码来回答问题，支持流式输出。

## 技术栈

- 后端：Python FastAPI + LangChain + SQLite + 对接 DeepSeek V4 模型
- 前端：Vue，前后端分离

## 要求

1. 页面需要阅读舒适，具有科技感，代码块有语法高亮，使用 UI UX Pro Max 技能美化页面
2. 开发前，先通过 Firecrawl 联网搜索信息，通过 Context7 查询最新技术文档和用法
3. 必须生成完整可运行的代码，每步完成后必须自主测试验证
```

A quick breakdown of the key points in this prompt:

- Put the **role definition** first, so AI enters the mindset of a full-stack engineer
- Use **task description** to explain the requirements clearly in natural language
- In the **tech stack** section, only list the key choices and let AI decide the implementation details
- The last two requirements are crucial: make AI check docs before writing code to avoid hallucinations, and make it test by itself after development to reduce failures

I chose GPT-5.5 as the model, set intelligence to **High**, and gave it full access permissions (mostly for convenience):

![](https://pic.yupi.icu/1/1777259547435-755d715a-4233-4779-a198-a2d38d94c92c.png)

Note that if you want AI to test more completely, you can first obtain a DeepSeek API Key and write it directly into the prompt. Otherwise, without an API Key, AI can’t fully test the large-model integration.

After sending the prompt above to AI, all that’s left is the long wait.

I waited 9 minutes this time, and during that period I kept doing pelvic floor exercises. Thanks to AI coding, I’m getting more exercise too~

AI generated the full frontend and backend project code and also automatically wrote the project documentation:

![](https://pic.yupi.icu/1/1777260859705-cb84bd29-ca01-4da7-a75f-1e8f7224e653.png)

Click the top right to view all generated code files. In total, it produced 19 files and 1,644 lines of code:

![](https://pic.yupi.icu/1/1777261007438-29de19fd-b3f8-4268-a6a1-3b05966cb85d.png)

Click the top right to view the project overview, where you can see the progress, generation results, and information sources.

Look carefully at the **Sources** column—you’ll see that AI used all 3 Skills we provided. Firecrawl was used to search for information, UI UX Pro Max was used to beautify the page, and Context7 was used to look up documentation:

![](https://pic.yupi.icu/1/1777260929224-57f9b68c-5642-4d5a-8d89-990a4158253f.png)

If you’re interested, check out the core code AI generated. For example, the Q&A module uses LangChain to implement an Agent with 3 tools: `read_file` (read files), `grep_code` (search code), and `repo_map` (get repository structure). AI then decides for itself which tools to call to answer the user’s question.

![](https://pic.yupi.icu/1/1777262292586-f5557d4f-ce46-495e-9f7f-48b239cabd53.png)



## Testing and Verification

Next, you need to obtain a DeepSeek API Key. Go to the [DeepSeek Open Platform](https://platform.deepseek.com), create an API Key, and remember not to leak it!

![](https://pic.yupi.icu/1/1777261129697-2ad16c21-6d70-4e87-879c-df2dd7e888b2.png)

Whenever you use an AI large model, remember to pay attention to pricing. For example, at the moment DeepSeek V4-Flash costs only 1 RMB per million input tokens and 2 RMB per million output tokens, while V4-Pro costs 3 RMB input and 6 RMB output (temporarily discounted to 25% until May 5). If the cache hits, it’s even cheaper—V4-Flash input can go as low as 0.02 RMB per million tokens.

![](https://pic.yupi.icu/1/1777261160054-a4d31930-44d6-4bcb-a3d0-72b533793cb7.png)

However, DeepSeek currently still doesn’t have a Coding Plan, so I don’t especially recommend using it for AI coding itself. The token consumption would probably be too much for many people. But using it as the brain of an AI application is very suitable and highly cost-effective.

Following the guidance AI gave, open the terminal in Codex and set the environment variables, replacing the API Key with your own:

```bash
export DEEPSEEK_API_KEY=你的_key
export DEEPSEEK_MODEL=deepseek-v4-pro
```

![](https://pic.yupi.icu/1/1777261353853-35e38b40-6f56-4d02-b2f1-90bfed1755be.png)

But this `export` approach is temporary. Once the terminal is closed, it’s gone.

A better approach is to ask AI to create an environment-variable configuration file, and then you can just fill it in manually.

AI quickly finished the task and added `.env` and `.env.example` environment variable files:

![](https://pic.yupi.icu/1/1777261704240-13861afc-d888-46cb-b2ff-594d3acd3dd7.png)

Note that if your project is going to be open source, you must remember to ignore `.env` in `.gitignore` to avoid leaking your API Key to GitHub.

Then just open the `.env` file directly in the editor and fill in the API Key:

![](https://pic.yupi.icu/1/1777261752700-19c79ce9-9589-476d-a728-369353e279ff.png)

After configuring the environment variables, ask AI to restart the project:

![](https://pic.yupi.icu/1/1777261872346-c8224d36-f3a4-446f-9055-de3fb1f7988f.png)

Next, do a manual test. Open the webpage and enter a GitHub repository URL—for example, the [AI zero-code app generation platform](https://github.com/liyupi/yu-ai-code-mother) project I previously built with everyone:

![](https://pic.yupi.icu/1/1777262004830-4f2fb828-e4eb-4bb6-95e4-d3fa190fd13b.png)

Although the layout and styling are fairly standard, the functionality works completely fine. The analysis result generated by DeepSeek V4 is quite reliable, including the project overview and tech stack analysis:

![](https://pic.yupi.icu/1/image-20260427143606586.png)

It also includes explanations of core modules, data flow analysis, reading suggestions for beginners, and so on. The content is accurate, and the generation speed is pretty fast:

![](https://pic.yupi.icu/1/1777262420380-cfac00d4-9116-47cb-ab65-189db056104a-20260427143538208.png)

Let’s test the source-code Q&A feature too. Ask it: *What design patterns does this project use?*

AI called tools and searched through the code on its own, quickly listing patterns such as the Facade pattern and Strategy pattern, and annotating each one with the corresponding source-code file path:

![](https://pic.yupi.icu/1/1777262689897-d57b786b-2196-4369-86d7-c2d29fb190fe.png)

The core functionality passed testing. But if you want to launch the project formally, you still need to test a bunch of edge cases: what if the repo doesn’t exist? What if the network drops? Is the cache-hit logic correct?

Testing them one by one manually is too much trouble, so I just let AI do it.

Codex has a built-in Browser Use plugin. Type `@Browser Use` to use the plugin and let AI test autonomously:

```markdown
自主测试所有功能，出了问题自动修复，确保所有功能正常可用
```

![](https://pic.yupi.icu/1/1777262810965-5c656c56-627e-482f-8d5d-865a867d123e.png)

You can see AI opening a browser inside Codex, clicking around by itself, entering repository URLs, checking the analysis result, and testing the Q&A feature—all autonomously. During that time, I did a little more pelvic floor training. My legs almost went numb.

![](https://pic.yupi.icu/1/1777262956188-5e7cc9e6-7c98-402c-adee-79956abf7630.png)

After about 9 minutes, AI completed the end-to-end autonomous testing and also fixed several bugs it discovered on its own:

![](https://pic.yupi.icu/1/1777265795106-dfdc2945-e0e4-4653-a79f-814302226667.png)

At this point, the project is done. Pretty simple, right?

You can also continue asking AI to optimize the frontend layout, add Mermaid flowcharts to the report, support report export, and more. Use your imagination and extend it however you like~



## My Thoughts

Finally, let me talk a bit about my real impressions of Codex, GPT-5.5, and DeepSeek V4.

First, Codex. Codex’s interface is all about simplicity. At first glance, it doesn’t even look like an AI coding tool—it looks more like an AI chat assistant. But its features are actually fairly complete. It has MCP and Skills extensions, a plugin marketplace, automation, Git integration, Browser Use, Computer Use, and most of the engineering capabilities needed for AI programming.

But its drawbacks are also obvious. The default set of available models is limited. Unlike Cursor and Copilot, it doesn’t natively integrate Claude, GPT, Gemini, and other models that you can switch between freely. Its usability is also a bit worse, and you probably already felt that from the MCP setup section. Copilot lets you search and install MCP in one click through the extension marketplace, and Cursor supports visual editing of JSON config. On the Codex side, you still have to wrestle with the command line or hand-write TOML.

![](https://pic.yupi.icu/1/1777266857576-e240c700-e113-4d3d-8f4d-44512175986f.png)

Now let’s talk about GPT-5.5. Honestly, after testing several full-stack projects, I didn’t feel any obvious gap between GPT-5.5 and Claude Opus. As long as the prompt is good, it can usually handle both the frontend and backend of a full-stack project in one shot, and the core business workflow will most likely run successfully on the first try. Its frontend performance is decent too—responsive and functional—but the UI wasn’t especially stunning...

![](https://pic.yupi.icu/1/1777267657382-9f026e06-9984-42f6-b371-c998a41d2af9.png)

Now let’s look at the cost of GPT-5.5. For the project above, it consumed 130,000 tokens and used 50% of the context window. Codex desktop currently has a 258K context capacity, which is fine for simple full-stack projects, but more complex engineering projects may feel some pressure.

![](https://pic.yupi.icu/1/1777268009237-7136c440-d7f9-4fec-8949-9c7fbc3deeb9.png)

At the moment I’m using a GPT Plus subscription, which costs $20 a month (about 150 RMB), with rate limits per 5 hours and per week. After finishing this project, my 5-hour quota was basically used up. Without counting extended features, I could probably build around 5 complete projects per week.

![](https://pic.yupi.icu/1/1777266442906-7ccad38c-40d0-488e-a891-27dafc3876ef.png)

Finally, DeepSeek V4.

Our team previously integrated DeepSeek V3 into some business scenarios, and I also used V3 in projects I built with everyone. This time, after plugging V4 into the project, the generation speed was still pretty fast, and the quality was clearly improved over V3, especially in code understanding and analysis. On top of that, with support for a 1-million-token long context, we can build heavier AI applications such as deep research and global analysis of complex project codebases.

Looking at the actual API cost, the testing process used 27 requests, consumed more than 50,000 tokens, and cost 0.15 RMB. Based on normal user traffic, 1,000 requests per day would cost about 5.5 RMB, which is very cost-effective.

![](https://pic.yupi.icu/1/1777266027113-1126052d-a9a6-4049-ab3a-b75291612a87.png)

Overall, I probably won’t keep using Codex for day-to-day AI coding, and for complex projects I’d still choose GPT-5.5 or Claude Opus. But when building AI applications, I’d prioritize integrating the DeepSeek V4 API, because it’s cheap and effective.



## Final Thoughts

From requirements to launch, this project was developed entirely with Codex + GPT-5.5, with the backend connected to the DeepSeek V4 API, and the whole process took less than 20 minutes.

Although Codex still isn’t as convenient as Cursor and Copilot when it comes to MCP setup, its overall feature completeness is already pretty good. More importantly, this project shows us that it’s entirely possible to build full-stack projects with different AI coding tools. If you want to learn more about how to use and compare AI coding tools, you can read the related articles in the programming tools section of this tutorial series.



## Recommended Resources

1) Yupi AI Navigation Website: [Comprehensive AI Resources, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Paths, Programming Tutorials, Practical Projects, Job Hunting Guide, Q&A](https://www.codefather.cn)

3) Programmer Interview Cheatsheet: [High-Frequency Topics for Internships / Campus Hiring / Experienced Hiring, Plus Real Interview Question Analysis](https://www.mianshiya.com)

4) Programmer Resume Writing Tool: [Professional Templates, Rich Example Sentences, Direct to Interview](https://www.laoyujianli.com)

5) 1-on-1 Mock Interview: [A Must-Have for Internship / Campus Hiring / Experienced Hiring Interviews to Land Offers](https://ai.mianshiya.com)
