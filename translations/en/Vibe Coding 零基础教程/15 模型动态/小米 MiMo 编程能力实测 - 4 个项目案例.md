# Xiaomi MiMo Coding Benchmark - 4 Real Project Case Studies

Recently the large-model world has been an all-out immortal battle, and I’m testing so much I’m practically going bald...

GPT-5.5 declared: I have the strongest comprehension!

Then DeepSeek V4 followed up with: I have the best price-performance ratio!

And right then, from some little corner came a weak voice: I... I’m giving away 1.6 billion tokens for free...

I looked closely. It was Xiaomi.

On April 23, Xiaomi officially released the MiMo-V2.5 series of large models. The flagship MiMo-V2.5-Pro is a trillion-parameter MoE architecture model with an ultra-long context of 1 million tokens.

The official selling points are **strong Agent coding ability and high token efficiency**. They claim that for the same coding task, it uses 40% to 60% fewer tokens than Claude Opus and Gemini Pro.

More importantly, Xiaomi simultaneously launched the “100 Trillion Token Creator Incentive Program,” giving developers free tokens. They really know how to appeal to freeloaders like us.

![](https://pic.yupi.icu/1/image-20260430152304332.png)

Just looking at parameters and benchmark scores isn’t very interesting. Whether a model is actually useful still has to be tested with real projects.

In this article, I’ll first show everyone how to claim 1.6 billion large-model tokens for free, then use Claude Code to test Xiaomi’s new open-source model in real coding scenarios. You can also treat this as a beginner-friendly Claude Code tutorial.

Save it first—let’s begin.



## Claim 1.6 Billion Tokens for Free

Open Xiaomi MiMo’s ORBIT incentive program page: [https://100t.xiaomimimo.com](https://100t.xiaomimimo.com/)

You can see the total pool is 100 trillion tokens, and distribution is currently underway:

![](https://pic.yupi.icu/1/1777476574146-be9955f2-bedf-4c10-9f7f-686e7c4c302d.png)

Applying is simple—just fill out a form. Mainly choose the AI coding tools and underlying models you commonly use, then describe what projects you’ve built with AI:

![](https://pic.yupi.icu/1/1777476951718-86711359-564e-426a-92e2-2031c8c4cf80.png)

After submitting, it says the review will be completed within about 3 business days:

![](https://pic.yupi.icu/1/1777477159587-db9b0ad4-ee2c-45e8-870f-9f3db6d24621.png)

But mine was approved instantly. I received the email notification very quickly. The email said that if you log in or register on the MiMo API open platform using the email address from your application, the benefits will be automatically credited within 24 hours after login.

> Open platform: [platform.xiaomimimo.com](https://platform.xiaomimimo.com/)

![](https://pic.yupi.icu/1/1777478864522-fa8044ef-8daa-4222-8341-cd45b9800c98.png)

**Important: it’s best to log in to this platform with the email you applied with first, and only then submit the application. Otherwise, the benefits may not arrive!**

After logging into the open platform, you can see the gifted plan under subscription management. For example, one of my coworkers casually let AI write some application text and got the Max monthly plan.

Seriously? They gave him 1.6 billion tokens?

From the plan information, it supports the full MiMo-V2.5 model lineup, including MiMo-V2.5-Pro and MiMo-V2.5, and is also compatible with mainstream coding tools like Claude Code and OpenCode:

![](https://pic.yupi.icu/1/1777515511662-c66151fe-15df-4c49-a5a0-b2f4110ddb21.png)

At first I thought I misread it and assumed it was 160 million, but it really was 1.6 billion. Now we can go wild!

Xiaomi’s official Max annual subscription costs nearly 7,000 RMB, so giving away one month is roughly like handing out about 600 RMB for free?

![](https://pic.yupi.icu/1/1777515591763-7d6c98ba-c569-43a6-a685-a81d07b9b297.png)

Whatever you think about Xiaomi’s model quality, if they’re giving away this much for free, what more could you ask for?

What annoyed me, though, is that my own account only got the Pro monthly plan (700 million tokens), even though I specifically wrote in the application that I was “programmer Yupi” and a content creator.

Come on, are you looking down on me? I got so mad I lost a few more hairs...

![](https://pic.yupi.icu/1/1777522578378-c6589e31-c916-4b81-a8bf-73cc8e09e420.png)

Now let’s get to the point and prepare the AI coding tool for the benchmark.



## Environment Setup

### Installing Claude Code

Let me briefly introduce Claude Code. It’s an AI coding tool released by Anthropic that runs directly in the terminal. You chat with it and describe your requirements, and it can autonomously analyze projects, write code, run commands, and fix bugs from start to finish.

Beyond basic code generation, it can also use tools and Skill packages, connect to MCP external services, extend its abilities with Plugins, and even do multi-agent collaboration. It’s highly extensible. The latest v2.1 version also added Skill hot reloading, session forking, custom themes, and more. The updates have been coming hard and fast.

![](https://pic.yupi.icu/1/1777516701789-b0eb659f-6674-46a4-bdc0-b2d50eda4503.png)

Installing Claude Code is simple.

First make sure your computer has Node.js and npm. If not, just go to the [official Node website](https://nodejs.org/en/download) and download the easy installer:

![](https://pic.yupi.icu/1/1777516701942-41e28c9d-4c6c-420f-b34a-3a771d840517.png)

No matter what operating system you use, you can install Claude Code with a single npm command:

```bash
npm install -g @anthropic-ai/claude-code
```

![](https://pic.yupi.icu/1/1777516701568-eb7eda2d-4b39-4eb6-ac05-98c7316f0fd8.png)

After installation, type `claude` to enter the conversation interface. The first time, you need to log in before you can use it normally:

![](https://pic.yupi.icu/1/1777516701608-fc857d89-e5d0-4ce0-8aa6-ff3e3be676fe.png)

But I’m guessing many people don’t have Anthropic overseas subscription accounts, so we need to switch to a domestic model.



### Switching Models

Claude Code itself supports switching models. You can connect it to other large-model APIs either by modifying environment variables or editing configuration files.

Usually, whichever API provider you use, you can just check that provider’s official docs for connection instructions.

For example, the [Xiaomi Open Platform API docs](https://platform.xiaomimimo.com/docs/zh-CN/integration/claudecode) already provide a ready-made integration guide, including how to create the config file and fill in environment variables:

![](https://pic.yupi.icu/1/1777516802254-f5e31401-fd22-4ade-9d79-9300e2aa23be.png)

But I recommend an open-source tool called **CC Switch** even more. It visually manages configurations for AI coding tools like Claude Code, Codex, and Gemini CLI, and lets you switch model providers with one click. It comes with over 50 built-in provider presets, so you don’t have to manually edit config files yourself.

> Open-source link: https://github.com/farion1231/cc-switch

Following the official Chinese docs, choose the installation method based on your operating system:

![](https://pic.yupi.icu/1/1777516702429-c35e4af9-a053-4b50-a4eb-732ee54ba83a.png)

Mac users can install it from the command line:

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

![](https://pic.yupi.icu/1/1777516702626-80669bdd-f79a-4eb7-8b50-c2761abd2e4f.png)

After installation, run the software, enter the main interface, and add a model provider:

![](https://pic.yupi.icu/1/1777516702459-9ec60a6b-3c67-4be6-ac68-05929b4c7e16.png)

You’ll see that CC Switch includes a huge number of built-in provider presets. Choose Xiaomi MiMo:

![](https://pic.yupi.icu/1/1777516868333-8935ba98-5740-4390-a91c-43726514d90c.png)

Then prepare to fill in the model configuration. First, get an API Key from the [Xiaomi Open Platform](https://platform.xiaomimimo.com/console/api-keys).

**Important: if you claimed or activated a Xiaomi model subscription plan for free, you must use the dedicated API Key and dedicated Base URL for that plan. Otherwise, either you won’t be able to access the model, or you’ll still be billed from your normal account balance.**

The dedicated Base URL can be found on the subscription page, and it supports both OpenAI and Anthropic-compatible protocols:

![](https://pic.yupi.icu/1/1777520404516-69102816-7223-47d6-9718-5c01695170e0.png)

Fill in the API Key and the plan-specific request URL in CC Switch:

![](https://pic.yupi.icu/1/1777519071552-5154a636-5ca3-4bec-8611-779d5d44577c.png)

Then set the model to use. Here I set the main model to MiMo-V2.5-Pro, Xiaomi’s flagship Agent model, optimized for long and difficult coding tasks with higher token efficiency.

Click Save in the lower right:

![](https://pic.yupi.icu/1/1777519244637-dee5554b-4a59-4d26-bdab-f1a9061b6ce2.png)

As you can see in the image above, Claude Code uses a JSON config file. CC Switch is essentially a visual editor for the config files of different AI tools, saving you the trouble of editing JSON manually.

Finally, enable the Xiaomi MiMo model:

![](https://pic.yupi.icu/1/1777517330499-3376bc13-1ddc-4f91-a383-e7289ee94613.png)

Then re-enter Claude Code, and in the upper left you’ll see the switched model name. Type any sentence, and if the AI replies, the model switch succeeded:

![](https://pic.yupi.icu/1/1777517445474-f87c4e7b-f5fe-40c4-9d94-bf03881537a4.png)



### Installing Extensions

Claude Code already has basic abilities like reading and writing files, running terminal commands, and searching code. But to build a complete project well, that’s not enough.

We need the following 3 extensions:

1. Frontend Design: a front-end beautification skill that makes generated pages look more polished
2. Firecrawl: web search and page scraping, so AI can fetch the latest technical information
3. Context7: lookup of the latest technical docs and API usage, reducing AI hallucinations

Let’s install them one by one.



#### 1. Installing Frontend Design

Frontend Design is Anthropic’s official front-end beautification skill. It can make the pages generated by AI feel much more designed.

Inside Claude Code, first add the official skill marketplace using the `/plugin` command. This is basically like installing a skill store:

```bash
/plugin marketplace add anthropics/skills
```

![](https://pic.yupi.icu/1/1777516703443-717324a1-5864-447b-a731-9e4a519b7c40.png)

Type `/plugins`, then in the Discover tab, select `example-skills` and press Enter to install Anthropic’s official example skill bundle:

![](https://pic.yupi.icu/1/1777516703538-4a99f67b-f288-4b8d-825e-0a2d6322a9f4.png)

Type `/reload-plugins` to reload plugins:

![](https://pic.yupi.icu/1/1777516703624-e34d36ab-a5e2-4487-9cf7-e7748a056b1a.png)

Type `/skills` to view installed skills, and you’ll see that `frontend-design` is already there:

![](https://pic.yupi.icu/1/1777516703673-3a14f336-7d1f-4796-8502-b74c61f47e16.png)

After that, you can actively trigger this skill by typing `/frontend-design` in the chat box and let AI beautify the page. It also automatically installs the `webapp-testing` automation testing skill, which will be useful later.



#### 2. Installing Firecrawl

Firecrawl is a web search and page scraping tool that lets AI search for up-to-date technical information before development.

Installation is very simple. Open the terminal and enter this one-line command:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

![](https://pic.yupi.icu/1/1777516703895-7e336a35-0dc6-4fae-8859-3f8c68f7bf5b.png)

After running it, the browser will open automatically, and you need to click authorize on the pop-up page:

![](https://pic.yupi.icu/1/1777516704155-c203bf1d-0b6a-4c5d-b5c7-82649ef398ed.png)

After installation, it will automatically register 12 Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777516704255-d77f6dd4-4366-4e4c-8d47-15c800539cab.png)

In Claude Code’s skill manager, you’ll then be able to see the newly added Firecrawl skills:

![](https://pic.yupi.icu/1/1777516704270-209e0bea-bc02-436f-80b0-9ccf7f19f48b.png)



#### 3. Installing Context7

Context7 is a technical documentation lookup tool that gives AI access to the latest official docs for frameworks and libraries, helping it avoid coding against outdated APIs.

First, install it with this one-line terminal command:

```bash
npx ctx7@latest setup
```

It will ask whether to install an MCP service or CLI + Skills. Here I chose CLI + Skills. You’ll notice that more and more tools are shifting from MCP to the CLI + Skills approach now:

![](https://pic.yupi.icu/1/1777516704783-e365125c-516f-4dab-b23a-491825737e13.png)

Authorize it in the web page that pops up as well—no need to manually obtain or enter an API Key. Super convenient!

![](https://pic.yupi.icu/1/1777516704558-12e8c7bf-608f-4cd6-88e8-d4201888ba27.png)

Then choose which AI coding tool to install it for. I chose Claude Code:

![](https://pic.yupi.icu/1/1777516704721-42a91222-a15f-4213-b9b6-99a108c3d72b.png)

After installation succeeds, you’ll see the `find-docs` skill in the skill manager:

![](https://pic.yupi.icu/1/1777516704847-83d065f0-1366-411f-819f-28601f74aae8.png)

Of course, you can also choose the MCP Server installation method:

![](https://pic.yupi.icu/1/1777516704900-044ae1bc-6565-41b4-9bb0-7c71a8925e8b.png)

After installation, type `/mcp` in Claude Code and you’ll be able to see the installed MCP directly. It’s much more convenient than manual configuration!

![](https://pic.yupi.icu/1/1777516705093-194d4d76-6279-4562-9030-6d111e9735c3.png)

At this point, environment setup is complete! Next time you develop a project, you won’t need to prepare all of this again~



## Project Benchmarking in Practice

Now that the environment is ready, it’s time for the main event.

I prepared 4 different types of projects to test Xiaomi MiMo-V2.5-Pro’s real coding ability across different dimensions:

1. Programmer Yupi’s personal website, testing front-end design and UI aesthetics
2. Website Analyzer, testing full-stack engineering ability and AI integration
3. QQ Tang mini-game, testing complex interaction logic and game programming
4. Claude Code source-code analysis website, testing information architecture and data visualization

To save time and keep things fair, I used the same prompt structure for each project and prepared the technical plan in advance before handing it to AI.

In real AI coding, if you’re a complete beginner, you can absolutely let AI think through the plan for you.

But here, what I wanted to test was the model’s **code generation ability**, not its planning ability, so I fed it the solution directly to reduce variables.

Now let’s go through them one by one.



### Programmer Yupi’s Personal Website

For the first project, I asked it to make a programmer’s personal homepage.

The requirement was simple: show personal information, tech stack, project portfolio, articles, and updates. But it had to use the Aceternity UI animation component library to see whether AI could create a techy-looking page. This mainly tests the model’s **front-end design ability and UI aesthetics**.

Each case needs its own project folder, opened in Claude Code:

![](https://pic.yupi.icu/1/1777517798429-58a4ae87-6db3-4941-adea-cddee5f05dd8.png)

Enter the prompt:

```markdown
## 角色

你是一个前端全栈工程师，擅长 Next.js + TypeScript 开发。

## 任务

开发「程序员鱼皮」的个人网站，一个程序员 / 自媒体创作者的个人主页。

包含以下模块：Hero 区（头像、一句话介绍、社交链接按钮）、关于我、技术栈展示、项目作品集（卡片式，支持分类筛选）、文章/视频动态（模拟数据）、联系方式 / Footer。

## 技术栈

- 框架：Next.js + TypeScript
- UI 组件：Aceternity UI（从官网复制组件代码集成，如 Hero Highlight、Bento Grid、Card Hover Effect、Floating Navbar 等）
- 动画：Framer Motion（Aceternity UI 内置依赖）

## 要求

1. 页面设计要现代、有科技感，深色主题为主，充分利用 Aceternity UI 的动画组件（如背景光效、卡片悬浮、文字渐显等）
2. 响应式适配手机和桌面端
3. 纯静态页面，数据用 JSON 文件或常量模拟
4. 开发前，先联网搜索 Aceternity UI 官网查看可用组件列表和用法
5. 必须生成完整可运行的代码，完成后自主验证
```

Here I pressed Shift + Tab to enter auto-accept edit mode, which automatically approves file changes so I don’t have to manually confirm every operation. It’s more convenient, but it does carry some risk, so use it as needed.

Pressing Shift + Tab once more also enters Plan Mode, but since I had already given it the solution, there was no need to plan—speed up, speed up, gogogo!

![](https://pic.yupi.icu/1/1777518046991-d35d894d-e766-487f-b4ff-f730f8763246.png)

During development, it may ask you whether to allow tool calls or Skill execution. You can choose not to be asked again.

After waiting nearly 10 minutes, the AI finished the task.

Almost 10 minutes for a purely static personal website?!

![](https://pic.yupi.icu/1/1777521529952-b778e4ee-4bfb-4c29-a2fb-42f0f690a7b0.png)

Now let’s look at the result. This is the hero section, and it actually looks pretty good with a strong tech feel:

![](https://pic.yupi.icu/1/1777528773469-a4bb592b-94b6-456a-bb44-17742f5215f3.png)

Then there’s a section with some of my personal information using a classic three-column layout, but because there are no images, the content feels pretty empty:

![](https://pic.yupi.icu/1/1777528814458-30fafe28-878d-495d-b925-11d598733319.png)

Then comes the project portfolio with that classic blue-purple gradient. But the key issue is that the information is wrong. Since when did I ever make a project called “Fish Pond” with everyone???

And the projects shown are all very old. It looks like the AI didn’t successfully call the search skill at all:

![](https://pic.yupi.icu/1/1777528876043-2cb4d49e-58cd-4755-adc3-3ea7e041a8ba.png)

Overall: information accuracy gets a **weak** because it fabricated a nonexistent project; development speed gets an **NPC** because it took nearly 10 minutes to build a static page; visual quality gets **top-tier**, thanks in large part to my requiring the Aceternity UI component library.



### Website Analyzer

The second project is a full-stack one.

The user enters a website URL, and the system automatically scrapes the site content, calls the DeepSeek V4 large model for a full analysis, and outputs a report covering product positioning, target users, inferred tech stack, SEO evaluation, and more.

This mainly tests the model’s **full-stack engineering ability and AI integration ability**, to see whether it can connect the whole chain of front end, back end, crawling, and large-model invocation.

Enter the prompt:

```markdown
## 角色

你是一个全栈工程师，擅长 React 前端 + Python 后端开发。

## 任务

开发一个「网站解读器」Web 应用。用户输入一个网站 URL，系统自动抓取该网站内容，调用 AI 大模型进行全面分析，输出：功能定位、目标用户、技术栈推测、内容结构、SEO 评估、优缺点总结。

## 技术栈

- 前端：React + TypeScript (Vite 构建)
- UI 组件：Ant Design（antd）
- 后端：Python FastAPI
- 网页抓取：后端使用 httpx + BeautifulSoup 抓取页面内容
- AI 分析：后端调用 DeepSeek 模型（兼容 OpenAI SDK），使用 SSE 流式返回结果
- 前后端通信：前端通过 fetch 消费 SSE 流

## 要求

1. 前端界面使用 Ant Design 组件（Input、Card、Spin、Steps 等），布局清晰专业
2. 支持流式输出，分析过程实时逐字显示
3. 后端做好错误处理（URL 无效、抓取超时、AI 调用失败等），前端友好展示错误信息
4. 前后端分离，分别提供启动命令
5. 必须生成完整可运行的代码，完成后自主验证
```

It took nearly 4 minutes to finish this task, which is a fairly normal speed:

![](https://pic.yupi.icu/1/1777521496300-a074220c-51cc-4505-af96-1439e9b731f2.png)

Following AI’s guidance, I filled in the DeepSeek API Key on the back end, started both front end and back end, and tested it.

The moment I opened the page, I was stunned:

![](https://pic.yupi.icu/1/1777529468600-e5e38e65-e79f-438e-83da-5a3ee3e4ed0e.png)

That’s it? It’s this crude?! No wonder it developed so quickly...

Now let’s try the feature. Enter a URL, for example my [Yupi AI Navigation](https://ai.codefather.cn/), and click Analyze.

The AI instantly produced a streaming analysis report, covering product positioning, target users, inferred tech stack, and so on:

![](https://pic.yupi.icu/1/1777529553650-ba87480b-472a-4afe-99ed-8040e4cb3d18.png)

And you know what—it actually works!

But judging from the output timing, it probably just scraped a single page and then handed it to the AI for analysis. That said, the report completeness is still quite high, so big credit to DeepSeek V4.

This project isn’t functionally very complicated, and it does count as one-shot full-stack development. For feature completion, I’d rate it **top-tier** since it finished successfully without obvious bugs; development speed also gets **top-tier**; visual quality gets **weak**, because it’s just too rough.



### QQ Tang Mini-Game

The third project sounds easy on the surface, but it’s actually a strong test of AI ability.

Build a front-end-only mini-game in the style of QQ Tang, where players move around a grid map, place water balloons, blow up obstacles and enemies, and face an AI-controlled opponent.

This project mainly tests the model’s **complex interaction logic and game programming ability**. Collision detection, state machines, and AI pathfinding are all tough nuts to crack.

Enter the prompt:

```markdown
## 角色

你是一个前端游戏开发工程师，擅长 Canvas / Web 游戏开发。

## 任务

用纯前端实现一个「QQ 堂」风格的单机小游戏。QQ 堂是一个俯视角的放置水球（类似炸弹人）对战游戏：玩家在网格地图中移动，放置水球，水球延时爆炸后产生水柱沿十字方向扩散，可以消除障碍物、击中对手。

核心功能：网格地图（含可破坏和不可破坏的障碍物）、玩家键盘操控移动和放置水球、水球定时爆炸 + 水柱扩散动画、AI 电脑对手（简单寻路和躲避逻辑）、道具掉落（增加水球数量、增加爆炸范围、加速）、胜负判定和重新开始。

## 技术栈

- 纯 HTML + Canvas + JavaScript（单 HTML 文件，不依赖任何框架或游戏引擎）
- 音效：Web Audio API

## 要求

1. 画面可爱卡通，用代码绘制角色和地图元素（不依赖外部图片资源），配色明快
2. 地图至少 13×11 格，每局随机生成障碍物布局
3. AI 对手要有基本智能：能主动放置水球、能躲避即将爆炸的水球
4. 包含开始界面和游戏结束界面
5. 必须生成完整可运行的代码，完成后自主验证
```

Five minutes later, the AI finished the task. It actually just generated an HTML page, so the speed was only average:

![](https://pic.yupi.icu/1/1777521192533-502cfe95-0595-4b10-9672-4a6281fd1045.png)

Then I opened the website and nearly spit out my food...

Seriously? You call this QQ Tang?! My youth is over!

![](https://pic.yupi.icu/1/1777530394058-654ef6b2-cdcc-4c2b-a257-c387ac9d8f78.png)

I played a round, and surprisingly, it really is playable—you can place bombs, blow up crates, and eliminate enemies:

![](https://pic.yupi.icu/1/1777530606534-e0862b78-e46a-41a1-a686-1f37ae5437b2.png)

But there are just too many bugs!

Movement speed is crazy fast, there’s clipping through objects, and you get stuck in walls. It reminded me of the cheaters I used to run into when playing QQ Tang back in the day...

The funniest part is that the enemy can’t even place bombs. It only follows behind me like an idiot. It might as well have the words “I’m dumb” written on its face.

![](https://pic.yupi.icu/1/1777530774001-d5c29cbe-ff16-4e17-93e3-079eca9780a1.png)

This project has way too many bugs. For feature completion, I’d rate it **completely broken**. Development speed gets an **NPC**, and visual quality gets **weak**.

I don’t even dare imagine what would happen if I asked it to build Plants vs. Zombies. I’ll leave that explosive possibility to you all to try~



### Claude Code Source-Code Analysis

The final project is a website that explains Claude Code’s architecture and implementation principles, including modules like project overview, architecture diagrams, detailed explanations of core modules, flowcharts, and source directory structure. It’s very information-dense.

This project mainly tests the model’s **information architecture ability and data visualization ability**, to see whether it can understand a complex system and present it clearly.

Enter the prompt, while also giving the AI the path to the Claude Code source bundle:

```markdown
## 角色

你是一个全栈工程师，擅长 React 前端 + Python 后端开发，同时精通代码架构分析和数据可视化。

## 任务

开发一个「Claude Code 源码分析」网站，系统性地展示 Claude Code（Anthropic 的命令行 AI 编程工具）的架构设计和实现原理。

包含以下模块：项目概览（一句话定位 + 关键指标）、架构总览图（交互式模块关系图，可点击展开详情）、核心模块详解（Agent 循环、Tool 系统、Context 管理、权限控制等，每个模块一个详情页）、关键流程图（用户输入→思考→工具调用→输出的完整链路）、源码目录结构（可展开的树形浏览 + 搜索过滤）。

## 技术栈

- 前端：React + TypeScript (Vite 构建)
- UI 组件：Mantine（使用其 AppShell、NavLink、Tabs、Accordion、Paper 等组件）
- 可视化：React Flow 绘制架构图和流程图
- 后端：Python Flask，提供分析数据的 API（架构信息、模块数据以 JSON 格式存储）
- 前后端通信：REST API

## 要求

1. 使用 Mantine 的 AppShell 做整体布局（侧边导航 + 主内容区），支持亮/暗色模式切换
2. 架构图使用 React Flow，支持节点点击展开详情、缩放拖拽
3. 后端用 Flask 提供静态 JSON 数据的 API，数据内容基于 Claude Code 的公开信息整理
4. 支持全站搜索，快速定位模块和关键概念
5. 前后端分离，分别提供启动命令
6. 必须生成完整可运行的代码，完成后自主验证
```

![](https://pic.yupi.icu/1/1777520746868-103983db-6df8-44ea-a5d0-1a71d468dc41.png)

The AI felt the task was complex and automatically entered planning mode: first unpack the source bundle and analyze the architecture, then plan the implementation:

![](https://pic.yupi.icu/1/1777521840681-614c5cca-d1f0-41b6-9cc7-3e67896836c1.png)

It took a full half hour to finish. I had planned to go out, but it kept me locked in place that whole time...

![](https://pic.yupi.icu/1/1777522886901-c4137b73-0554-4451-8abc-afe6205cf340.png)

Run it and test the result.

First is the Claude Code project overview. You know what? This time it actually looks fairly decent. It lists key metrics like source-file count, component count, tool count, and also marks the tech stack:

![](https://pic.yupi.icu/1/1777532046330-843e3723-8b8d-4de5-9e49-46cd3f1ba833.png)

Then we view the architecture overview. It provides an interactive architecture diagram drawn with React Flow, supporting drag and zoom, and the layout is actually fairly tidy. Not bad, not bad~

![](https://pic.yupi.icu/1/1777532098786-56438303-3599-4360-a039-4585e2cd8cc2.png)

Clicking a module lets you view its design in detail, including module positioning, architectural design, key files, and so on:

![](https://pic.yupi.icu/1/1777532216493-5b886dac-8bf6-4e5a-b875-7ceef52c60c9.png)

Then I checked the key flowchart. Come on, I praised you twice and now you got overconfident? You call this a flowchart?!

![](https://pic.yupi.icu/1/1777532247219-e7dbb415-952e-4d72-99d0-5cc621500094.png)

Finally, I checked the source directory structure and burst out laughing. There’s just an empty `src` directory. You can’t expand anything at all!

![](https://pic.yupi.icu/1/1777532331152-7965d0b7-d9d7-4ed7-a3a9-dec9a3a33670.png)

My verdict: I think the code-analysis ability itself is decent, and the project overview plus architecture overview are pretty good, so I’ll give it **top-tier** as encouragement. But the flowchart and directory structure both have obvious bugs, so feature completion gets **weak**, and development speed also gets **weak**—it simply didn’t deserve that half-hour wait.



## Summary

Finally, let me briefly share my real impressions of Xiaomi MiMo-V2.5-Pro after this round of testing.

First, capability-wise, it *can* complete full-stack projects. All 4 tasks did run successfully.

But the quality? Hard to put into words.

It feels like a pretty unmotivated AI that only completes my tasks in the simplest possible way, with a “as long as it runs, it’s fine” mentality, and zero interest in going beyond the bare minimum.

No wonder the official marketing emphasizes token efficiency. Is its way of saving tokens just... doing less work?

Judging from the actual results, its overall coding ability is weaker than DeepSeek V4, and it’s nowhere near Claude Opus.

I tested 4 tasks, and during execution it **never used any of the skills I had installed** (`Firecrawl`, `Context7`, `Frontend Design`). Instead, it used Claude Code’s built-in search and scraping tools. That shows MiMo-V2.5-Pro still isn’t very smart in its tool-selection decisions. Better tools were right there at hand, and it still ignored them.

![](https://pic.yupi.icu/1/1777521462310-5e04aced-087b-4b78-be7f-8972385cd10c.png)

Now let’s look at the cost. The 4 projects used a total of 23 million tokens, yet only 1% of my plan quota was consumed. That feels nice...

![](https://pic.yupi.icu/1/1777531135598-be7dbf70-d7e3-4dbd-a787-b0c821d71ae3.png)

I also tested usage without plan tokens. Developing a single blog-style static website cost about 1.6 RMB. Do you think that’s expensive or cheap?

![](https://pic.yupi.icu/1/1777531230941-56ed2f9e-bda1-4337-87c1-0c099685266a.png)

Even if the results aren’t that amazing, they gave away 1.6 billion tokens for free, so honestly, just say thank you. What more could you want?

I think right now it’s more suitable for building small utility projects or solving everyday coding problems. If you want to build a complex project, you still need to put more effort into the prompt—for example, explicitly guiding it to use skills, providing a more detailed solution design, and adding some human oversight.

Put plainly: when the model isn’t strong enough, the prompt and the Harness engineering need to be stronger.



## Final Thoughts

In this article, I showed everyone how to claim Xiaomi’s 1.6 billion free tokens and used Claude Code—from environment configuration to real project practice—to comprehensively test the coding ability of Xiaomi MiMo-V2.5-Pro.

Once you learn this, you’ll understand how to set up Claude Code, switch models, install extensions, and evaluate the coding level of different large models through real projects.

If you want to keep learning more practical AI coding techniques, you can read the other articles in the Tips and Tricks section of this tutorial.
