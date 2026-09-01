# DeepSeek V4 + Claude Code: Step-by-Step Guide to Building an API Relay

In the age of AI programming, humanity’s demand for Tokens is growing bigger and bigger, and supply can barely keep up.

So some sharp people smelled a business opportunity and started building API relays.

A lot of technical folks may look down on this kind of thing and think, “Isn’t it just forwarding requests?”

But look at who’s doing it: Cheetah Mobile CEO Fu Sheng built EasyRouter; crypto-world celebrity Justin Sun built B.AI, which is rumored to have already passed one million users; even the Trump family jumped in with WorldClaw, where the most expensive of the four plans sells for $9,999, and buyers even get a chance to win private dinner tickets at Mar-a-Lago...

![](https://pic.yupi.icu/1/%2525E5%2525A5%252597%2525E9%2525A4%252590.png)

Trump was already selling Crypto Tokens before, and now that AI is hot, he’s selling API Tokens too. Sure enough, nobody understands Tokens better than him!

![](https://pic.yupi.icu/1/image-20260509145553218.png)

Watching them all make money hand over fist, it’s hard for ordinary people not to feel tempted.

Ahem. Actually, I made a similar product back in 2023. I wonder how many of you still remember “Yu Smart AI.” Back then I even built an SDK for calling the relay. Later, the site shut down because of costs. Let’s not reopen those wounds...

![](https://pic.yupi.icu/1/1687152503823-a9d100de-06b0-4c65-ad73-92f5703f186d-20230702140036995.png)

After that failed experience, I decided not to build one alone in silence this time. Instead, I’ll just write a tutorial and take everyone through building one from scratch together!

In this article, I’ll not only explain clearly what an API relay is and how it works, but I’ll also walk you through building one with AI programming. We’ll make one version with DeepSeek V4 + Claude Code and another with GPT-5.5 + Cursor, so you can fully understand API relays in one go.

The full article is over 8,000 Chinese characters long. Bookmark it, and let’s begin~

## What Is an API Relay?

Here’s an analogy. Suppose you want to buy a luxury bag from abroad, but it’s inconvenient for you to go to an overseas boutique directly, so you use a purchasing agent. You give the agent the money, they buy it for you from the brand store, ship it back, and earn a markup and service fee along the way.

That’s basically what an API relay does.

When you use AI for chatting, coding, or building applications, you don’t connect directly to AI model providers like OpenAI, DeepSeek, or Zhipu. Instead, you call them through a relay—an intermediary. The relay aggregates the APIs of multiple model providers onto one platform. You just register one relay account, and then you can call all those models without signing up everywhere separately. It’s much more convenient.

![](https://pic.yupi.icu/1/Gemini_Generated_Image_w1vnohw1vnohw1vn-20260509174715470.jpg)

Why are relays so popular? You have to look at what problems they solve.

For developers in China, using foreign models like Claude or GPT comes with barriers in both payment and network access. Relays solve those headaches by supporting common domestic payment methods and direct domestic network access, without all the hassle. Even if you only use domestic models, registering a separate account for each provider and managing separate API Keys is annoying. A relay can manage all of that in one place.

The best-known relay right now is probably **OpenRouter**, which aggregates hundreds of large models and is said to already be doing over $100 million in annual revenue.

![](https://pic.yupi.icu/1/image-20260509161936710.png)

If one relay can make that much money, no wonder even Trump wants a piece of the action.

By the way, programmer friends may have heard the term “AI gateway.” It is a bit different from an API relay. A relay is more like a reseller that “buys APIs on your behalf,” while an AI gateway is more like infrastructure for enterprises to centrally manage multiple models internally. But the core technology is similar.

## How a Relay Works

I know a lot of people are already using relays or considering them, but the market is a mixed bag, and it’s easy to step on landmines.

If you want to avoid trouble, the best way is to understand how relays work and what they’re actually doing behind the scenes.

At its core, a relay comes down to two words: **proxying**.

Your request is not sent directly to the AI model. Instead, it first goes to the relay’s server, which forwards it to the corresponding model provider, gets the result, and returns it to you.

Most relays also share one common design choice: externally, they “pretend” to be in OpenAI API format. Almost all AI tools—Claude Code, Cursor, and various SDKs—support OpenAI format, so users only need to change 2 parameters to connect to a relay. They don’t need to change a single line of business logic:

```python
client = OpenAI(
    api_key="sk-relay-xxx",       # 改成中转站的 Key
    base_url="http://你的中转站/v1" # 改成中转站的地址
)
```

After receiving the request, the relay server routes it to the corresponding AI provider based on the model name you specify. If multiple API Keys are configured, it can also rotate between them automatically to avoid rate-limiting a single key. At the same time, it records the Token usage for each call for billing purposes.

![](https://pic.yupi.icu/1/Gemini_Generated_Image_vjaih0vjaih0vjai-20260509174715559.jpg)

But there’s a problem: all your requests go through the relay’s server, and that layer is a complete “black box” from the user’s perspective. You have no idea what the relay is actually doing!

And many shady relays are exactly where the dirty tricks happen—inside that black box.

Recently, CISPA Helmholtz Center for Information Security published a paper exposing a shocking fact: **nearly half of third-party API relays are systematically committing fraud**!

![](https://pic.yupi.icu/1/image-20260509133411306.png)

Some common shady tactics include the following:

1) Model substitution

You pay for GPT-5, but what actually runs is some cheap open-source mini model. The paper tested 28 relays and found that 45.83% of API endpoints had model identity mismatches. In medical scenarios, the performance gap was as high as 47%!

2) Inflated Token usage

You actually used 100 Tokens, but the bill says 150. The user paid $14.84 but only received services worth $5.7 to $7.7.

3) Cache arbitrage

AI model vendors often offer discounted caching prices for repeated content (such as the same System Prompt), but the relay charges you the original price and quietly pockets the difference.

4) Data harvesting

Even worse, some relays collect and sell users’ code and sensitive data!

Research found that among 17 leading relays, 15 were run by individuals, with no corporate registration and no ICP filing. Once enough recharge money piles up, who knows—they might just wipe the database and disappear...

So my advice is: if conditions allow, use the official API directly. And if you really must use a relay, choose a large platform with actual corporate qualifications and regulatory filing.

If you want to understand relays more deeply, there are quite a few open-source projects on GitHub worth studying. Once you’ve read through those and built one yourself, relays won’t hold any mysteries for you anymore.

## Open-Source Relay Projects

There are a huge number of open-source relay-related projects on GitHub. You could say there’s everything under the sun. Let me show you a few representative ones.

1) [one-api](https://github.com/songquanpeng/one-api)

An old-school foundational project with tens of thousands of stars on GitHub. It’s built in Go, unifies the APIs of mainstream large models into OpenAI format, supports dozens of models, can run from a single file, and also supports Docker deployment.

![](https://pic.yupi.icu/1/image-20260509160501101.png)

Without exaggeration, more than 80% of commercial relays on the market are based on one-api or its derivatives—they’ve just put a shell on top.

2) [new-api](https://github.com/QuantumNous/new-api)

A secondary development based on one-api, adding enterprise-grade capabilities such as Prometheus monitoring and OpenTelemetry observability. It’s also the underlying framework of many commercial relays.

![](https://pic.yupi.icu/1/new-api-dashboard.jpeg)

By the way, Fu Sheng’s EasyRouter was exposed by the original author of new-api as just being a re-skinned version. There were 98 keyword matches in the frontend code pointing to new-api, and the copyright information had been removed, which may violate the AGPL v3 open-source license.

3) [sub2api](https://github.com/Wei-Shaw/sub2api)

This one is wild. It can reverse-engineer Claude and OpenAI web subscription accounts into standard API interfaces. It’s basically like carpool-sharing one Plus membership among several people, splitting one account’s quota across multiple users.

![](https://pic.yupi.icu/1/image-20260509161048654.png)

4) [metapi](https://github.com/cita-777/metapi)

This one calls itself “a relay for relays.” It aggregates the accounts you registered across multiple one-api / new-api / sub2api services into one unified gateway, and allocates traffic based on weighted cost, balance, and usage.

![](https://pic.yupi.icu/1/dashboard-20260509174717717.png)

5) [all-api-hub](https://github.com/qixing-jk/all-api-hub)

This is a browser extension specifically for managing your accounts across multiple relays. After installing it, you can view all relay balances and usage in one panel, and it also supports automatic check-ins and price comparison. It’s very convenient if you use several relays at the same time.

![](https://pic.yupi.icu/1/model-list-20260509174717782.png)

Besides these relay projects, in enterprise scenarios there are also more proper open-source AI gateways like [LiteLLM](https://github.com/BerriAI/litellm), [Higress AI](https://higress.ai/), and [Kong AI Gateway](https://konghq.com/products/kong-ai-gateway). But these projects come with a certain technical barrier, so non-programmer friends don’t need to study them too deeply.

![](https://pic.yupi.icu/1/image-20251019163817976-20251028181254777.png)

Next, let’s build a simplified API relay ourselves.

## Requirements Analysis

The relay we’re building can be called “small but complete.” Its core features include:

1) Expose an interface compatible with OpenAI format, supporting both streaming and non-streaming responses, so users only need to change `base_url` and `api_key` to connect.

2) Integrate three domestic large models—DeepSeek V4, Zhipu GLM-5, and Tongyi Qianwen Qwen-Plus. It should support user-specified models as well as an `auto` mode for automatic routing.

3) Have its own API Key management system. Administrators should be able to create, disable, and delete Keys, and set a balance cap for each Key.

4) Record Token usage for every call, support different billing multipliers for different models, and show call logs and usage statistics charts in the admin backend.

5) Regularly check the health of each model channel, automatically retry failed requests through other channels, and display health status in the admin panel.

6) The admin panel should include a dashboard, channel management, Key management, and call logs, with admin password login support.

![](https://pic.yupi.icu/1/Gemini_Generated_Image_2i8fq32i8fq32i8f.jpg)

## Solution Design

If you have absolutely no technical background, you can let AI help you design the solution.

But here, to save time and tokens, I directly told the AI how to build it.

To get the core functionality running as quickly as possible, our relay does not need user registration and login, nor online payment integration. The administrator can create API Keys in the backend, collect payment by other means, send the Key to the user, and manually adjust the balance.

And don’t think this way is low-end. Most small relays on the market actually operate exactly like this! They just spin up an open-source project like one-api or new-api, create Keys in the backend, and start selling them through card-distribution tools or group chats...

If you want to learn a complete enterprise-grade AI gateway with user registration, online payment, monitoring, and alerting, you can check out the [step-by-step AI gateway project tutorial](https://www.codefather.cn/course/2029830328322994177) that our team released earlier. It builds everything from scratch with Spring Boot 3 + Spring AI + Vue 3. Interested students can study it on [Programming Navigation](https://www.codefather.cn).

![](https://pic.yupi.icu/1/202601291444803.png)

Because of certain reasons—you know what I mean—I can’t really take everyone through building a relay connected to foreign large models, and **I strongly do not recommend that you do so either**! So here we’ll just use three domestic models—DeepSeek, GLM, and Qwen—for demonstration, and run and test the project locally.

For the development stack, I chose mainstream Next.js + TypeScript, handling both frontend and backend in one go. For the database, I chose SQLite so the data is stored directly in local files, without needing to set up MySQL, Redis, and so on, lowering the barrier.

![](https://pic.yupi.icu/1/Gemini_Generated_Image_m65e4mm65e4mm65e.jpg)

## Environment Preparation

If you’ve gone through my earlier [AI programming tutorial](https://ai.codefather.cn/vibe), then Claude Code and the AI extensions should already be installed, and you can skip directly to the next section.

If you’re a complete beginner, don’t panic—just follow the steps below.

### Install Claude Code

Let me briefly introduce Claude Code first. It’s an AI programming tool launched by Anthropic that runs directly in the terminal. You chat with it and describe your requirements, and it can autonomously analyze the project, write code, run commands, and fix bugs entirely on its own.

In addition to basic code generation, it can also use tools and Skills packs, connect to MCP external services, expand capabilities with Plugins, and even do multi-agent collaboration. It’s highly extensible.

![](https://pic.yupi.icu/1/image-20260429110454017-20260509174718125.png)

Installing Claude Code is simple.

First, make sure your computer has the Node.js environment and the npm dependency installation tool. If not, just go to the [Node official website](https://nodejs.org/en/download) and download the foolproof installer:

![](https://pic.yupi.icu/1/1777341714221-67b76f0e-c816-410b-adc0-e445074efc46-20260509174718164.png)

No matter what operating system you use, you can install Claude Code with a single npm command:

```bash
npm install -g @anthropic-ai/claude-code
```

![](https://pic.yupi.icu/1/1777341807032-be0f1d99-4e97-4be6-80de-de7c32846d41-20260509174718202.png)

After installation, enter the `claude` command to open the chat interface. The first time, you need to log in before you can use it normally:

![](https://pic.yupi.icu/1/1777341971646-93bcacc7-143d-4f86-8d2a-bf17d288db9f-20260509174718233.png)

But I’m guessing many students don’t have an Anthropic subscription account, so we need to switch to a domestic model.

### Switch the Model

Claude Code itself supports switching models. You can connect it to other model APIs by “modifying environment variables” or “editing configuration files.”

In general, whichever provider’s API you want to use, just check that provider’s official docs and you’ll find the integration method.

For example, [DeepSeek’s API documentation](https://api-docs.deepseek.com/zh-cn/guides/coding_agents) already contains a ready-made integration method:

![](https://pic.yupi.icu/1/1777342329147-99094795-9da9-40b7-aa25-a566fc762c54-20260509174718284.png)

However, I more strongly recommend an open-source tool called **CC Switch**, which can visually manage the configurations of AI programming tools such as Claude Code, Codex, and Gemini CLI, and switch between different model providers with one click. It comes with 50+ provider presets, so you don’t need to manually edit config files yourself.

> Open-source link: https://github.com/farion1231/cc-switch

According to the official Chinese docs, choose the installation method that matches your operating system:

![](https://pic.yupi.icu/1/1777342571992-7b055f5f-3d27-4463-8247-4fe9bc315690-20260509174718321.png)

Mac users can install it through the command line:

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

![](https://pic.yupi.icu/1/1777342701813-0dc223c6-8c13-49ce-8434-aa00bfc6d08e-20260509174718366.png)

After installation, run the software to enter the main interface and add a model provider:

![](https://pic.yupi.icu/1/1777342816975-d7e89ce3-3b26-4237-a728-5478fbe86a47-20260509174718431.png)

Choose DeepSeek:

![](https://pic.yupi.icu/1/1777342881212-d0591f6e-c88e-4912-8cf5-62b7f1bfac17-20260509174718485.png)

Fill in the API Key, which you can obtain from the [DeepSeek Open Platform](https://platform.deepseek.com).

![](https://pic.yupi.icu/1/1777342981319-1e6c85a9-5063-42e2-bae9-0406886578d9-20260509174718516.png)

Here I set the main model to DeepSeek-V4-Pro. Compared with DeepSeek-V4-Flash, it has stronger Agent ability and more capable complex reasoning.

If you want to enable ultra-long context, you can also change it to `DeepSeek-V4-Pro[1m]`, but I estimate 200K context is enough for this task.

Then click Save in the lower-right corner:

![](https://pic.yupi.icu/1/1777343299981-c370c8ff-b24a-460a-891e-e08bc1efcf54-20260509174718549.png)

As you can see in the screenshot above, Claude Code’s JSON config file is ultimately what’s being changed. CC Switch is just helping you visually edit the config files of AI tools, saving you from manually editing JSON.

Finally, enable the DeepSeek model:

![](https://pic.yupi.icu/1/1777343334412-73a61961-5d7e-4fbb-a0e0-691f5d867b48-20260509174718583.png)

Then enter Claude Code again and type any sentence. If the AI can reply, it means the model switch was successful:

![](https://pic.yupi.icu/1/1777343427500-46c84648-4f92-4ed4-85ab-4af0b34f465e-20260509174718616.png)

### Install Extensions

By default, Claude Code already has basic capabilities like reading and writing files, running terminal commands, and searching code. But if you want to build a complete project well, those alone aren’t enough.

We need the following 3 extensions:

1. Frontend Design: a frontend beautification skill that makes generated pages feel more polished
2. Firecrawl: web search and webpage scraping, letting the AI obtain the latest technical information
3. Context7: query the latest technical docs and API usage to reduce AI hallucinations

Let’s install them one by one.

#### 1. Install Frontend Design

Frontend Design is Anthropic’s official frontend beautification skill, which helps the AI generate more polished-looking pages.

In Claude Code, first use the `/plugin` command to add the official skill marketplace—basically like installing a skill store:

```bash
/plugin marketplace add anthropics/skills
```

![](https://pic.yupi.icu/1/1777344066799-72c95f99-82bc-46ff-92f5-02cf6d21b1b9-20260429113524910-20260509174718645.png)

Enter `/plugins`, then in the Discover menu, select `example-skills` and press Enter to install Anthropic’s official sample skill bundle:

![](https://pic.yupi.icu/1/1777344221815-19f8cc7d-e608-4cf6-a8a9-05fa3dafab04-20260509174718679.png)

Enter `/reload-plugins` to reload the plugins:

![](https://pic.yupi.icu/1/1777344303461-6af1d179-4328-4892-83b4-a48f1af3c32d-20260509174718707.png)

Enter `/skills` to see the installed skills. You’ll find that `frontend-design` is already there:

![](https://pic.yupi.icu/1/1777344408094-9d8e06b5-a216-443e-a7ec-70dd78cb80d0-20260509174718748.png)

After that, entering `/frontend-design` in the chat box will actively trigger the skill and let the AI beautify the frontend page. It also automatically installs the `webapp-testing` automated testing skill, which will be useful later as well.

#### 2. Install Firecrawl

Firecrawl is a web-search and webpage-scraping tool that lets the AI search the latest technical information before development.

Installation is simple. Open the terminal and enter one command:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

![](https://pic.yupi.icu/1/1777258212308-8c83d23e-338e-4ec2-b1c0-05f54a22a36e-20260429113525121-20260509174718777.png)

After execution, it automatically opens the browser, and you need to click authorize on the popup page:

![](https://pic.yupi.icu/1/1777258069152-2d7fdb02-64e2-440b-bcbd-6254b07fb74e-20260429113525154-20260509174718801.png)

Once installed, it automatically registers 12 Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777258235867-0f6f08f5-4791-4b66-84b7-50936912540d-20260429113525186-20260509174718841.png)

In Claude Code’s skill management, you’ll then be able to see the newly added Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777344739629-f15409cf-6a43-4f96-a9bd-be72f7c0f795-20260509174718872.png)

#### 3. Install Context7

Context7 is a technical documentation query tool that gives AI access to the latest official docs for frameworks and libraries, preventing it from writing code with outdated APIs.

First, enter one command in the terminal to install it:

```bash
npx ctx7@latest setup
```

It will ask whether you want to install the MCP service or CLI + Skills. Here I chose CLI + Skills. You’ll notice that more and more tools are moving from MCP toward the CLI + Skills model:

![](https://pic.yupi.icu/1/1777258448310-41f86ec3-26e1-476e-aed5-4913c8116d21-20260429113525253-20260509174718912.png)

Likewise, authorize in the popup webpage. You don’t even need to fetch and enter an API Key manually—it’s super convenient!

![](https://pic.yupi.icu/1/1777258547209-dc872280-09eb-4bd9-ad45-2e412382002d-20260429113525305-20260509174718957.png)

Then choose which AI programming tool to install it for. I chose Claude Code:

![](https://pic.yupi.icu/1/1777344820438-9397de28-5658-4f0c-8cbe-8ed350beb84a-20260509174719029.png)

After successful installation, you can see the `find-docs` skill in skill management:

![](https://pic.yupi.icu/1/1777344978229-17483cf7-a0fd-4a5f-93cf-5865f96eab41-20260509174719298.png)

Of course, you can also choose to install the MCP Server version:

![](https://pic.yupi.icu/1/1777345106455-e31fd005-3cc6-45ac-a9d5-7dfafd30c7f4-20260509174719599.png)

After installation, enter `/mcp` in Claude Code and you’ll be able to see the installed MCP directly. It’s much more convenient than configuring it manually yourself!

![](https://pic.yupi.icu/1/1777345145401-72377bd2-2388-4f3b-bd8f-a31a76ecc676-20260509174719673.png)

At this point, environment preparation is complete! Next time you build a project, you won’t need to go through this setup again~

## Developing with DeepSeek + Claude Code

Create a new project folder called `yupi-ai-relay`, open a terminal, enter the directory with `cd`, and then type `claude` to open Claude Code:

![](https://pic.yupi.icu/1/1778231327727-283f3279-57b8-4ca8-9694-1a4d15a2edff.png)

Next, enter the prompt. This prompt was also generated for me by an AI programming tool based on my requirement description, so I’m sharing it here for reference:

```markdown
## 角色
你是一个全栈工程师，擅长 Node.js + Next.js + TypeScript 开发。

## 任务
开发一个叫 yupi-ai-relay 的网站，实现一个简易但完整的 AI 大模型 API 中转站，兼容 OpenAI API 格式，支持多模型路由。

## 核心功能
1. 对外暴露 `/v1/chat/completions` 接口，完全兼容 OpenAI Chat Completions API 格式，支持流式（SSE）和非流式响应，用户只需修改 base_url 和 api_key 即可接入
2. 接入 3 个国产大模型：DeepSeek V4、智谱 GLM-5、通义千问 qwen-plus。支持用户指定 model 参数选择模型，也支持 auto 模式随机负载均衡
3. 中转站自有 API Key 体系（sk-relay-xxx 格式），管理后台可创建/禁用/删除 Key，每个 Key 可设置余额上限
4. 记录每次请求的 Token 消耗（prompt_tokens + completion_tokens），不同模型设置不同计费倍率，管理后台可查看调用日志和用量统计图表
5. 定期检测各模型渠道可用性，请求失败自动重试到其他可用渠道，管理面板显示各渠道健康状态
6. 管理面板包含仪表盘概览、渠道管理、Key 管理、调用日志，支持管理员密码登录

## 技术栈
- 框架：Next.js + TypeScript
- 数据库：SQLite（通过 better-sqlite3，零配置）
- 样式：使用 Shadcn UI 组件库
- 图表：Recharts

## 要求
1. 页面参考 OpenRouter 官网风格，浅色主题，简洁大方接地气，使用 frontend-design 技能美化页面
2. 开发前，先通过 Firecrawl 联网搜索确认 DeepSeek、智谱、通义千问最新的 API 格式，通过 Context7 查询 Next.js 最新文档
3. 必须生成完整可运行的代码，每步完成后通过 webapp-testing 自主测试验证
4. 环境变量通过 .env.local 配置各模型的 API Key
```

Before sending the prompt to the AI, I pressed Shift + Tab to enter auto-accept edit mode. That way, when the AI creates, modifies, or deletes files and executes commands, I don’t need to confirm them one by one. It’s more convenient—but it also comes with some risk, so use it based on your own needs:

![](https://pic.yupi.icu/1/1778231457775-29f354b1-53bd-46e1-b96d-920c0c91b5ec.png)

Send the prompt to the AI, and after that comes the long wait.

During the process, the AI may need confirmation for tool calls. For example, when it wants to use Firecrawl to search the latest model API information, you can choose “Yes, and don’t ask again,” so it won’t repeatedly ask in the future:

![](https://pic.yupi.icu/1/1778231847088-583d81d1-294c-47a4-a839-f8ce64c91b22.png)

Note that DeepSeek’s performance isn’t always stable. Sometimes it won’t trigger the skills and will use its built-in search tool instead. You can strengthen the guidance in the prompt or actively trigger the skill with slash commands.

After development is complete, the AI automatically uses the `webapp-testing` skill for automated testing:

![](https://pic.yupi.icu/1/1778237385286-ac72c6e6-c2f2-4ac4-a5ac-edf4c5fb0271-20260509174719871.png)

After waiting nearly half an hour, the AI finally finished developing it. From the AI’s summary, you can see that it implemented everything in one sweep: OpenAI-compatible interfaces, streaming/non-streaming responses, multi-model routing, API Key management, Token billing, health checks, admin backend, and Recharts charts.

![](https://pic.yupi.icu/1/1778238659517-51bb2401-ceb3-4622-845a-9e1d8e980a1b-20260509174719909.png)

Then we need to do one manual step: obtain the model API Keys from the DeepSeek Open Platform, Zhipu AI Open Platform, and Alibaba Bailian Platform respectively, and fill them into the environment variable file according to the AI’s instructions:

![](https://pic.yupi.icu/1/1778238774781-00601ed0-6713-4f60-8743-e4c73dc22eb9.png)

After that, I asked the AI to run it for me. It didn’t just start the project—it also thoughtfully ran another round of tests:

![](https://pic.yupi.icu/1/1778239393938-0d758f7d-3856-4270-97b6-a4cd66ffc2a9.png)

During testing, the AI also independently discovered and fixed a problem. Not bad at all!

![](https://pic.yupi.icu/1/1778254400168-39ddef9f-321f-4773-96c8-0522454aeffc.png)

### Test Validation

Next, let’s test it manually.

Open the website homepage. I have to say—it’s clean and tidy! The key points are immediately obvious. Sadly, it still couldn’t escape the curse of the blue-purple gradient...

![](https://pic.yupi.icu/1/1778290068775-5a0c33a1-a12f-4e73-8408-9bfb76f8e057.png)

It does kind of resemble the style of the OpenRouter official site, right? Sort of...

![OpenRouter style](https://pic.yupi.icu/1/1778290147309-8a9853e6-df02-46c9-a3d9-39bea1c4b28c.png)

Log into the admin account and enter the backend. There, you can see data such as AI model usage and total cost consumption:

![](https://pic.yupi.icu/1/1778290268274-9408fbd7-9aa2-468c-8cf4-45798aad938e.png)

Go into channel management, and you can see the connected large models. You can also set a separate billing multiplier for each model—for example, adjusting DeepSeek V4 Pro’s price to 2x that of Flash:

![](https://pic.yupi.icu/1/1778290321828-4bf6726d-ac94-4f54-b450-0a01fbf5e9bb.png)

You can also check the health status of each model with one click:

![](https://pic.yupi.icu/1/1778290484603-59f4d4f7-4db6-4f5d-826e-e6ff56a74d29.png)

Wait a second? Didn’t I tell the AI in the prompt to integrate GLM-5? Why did it give me GLM-4.5???

![](https://pic.yupi.icu/1/image-20260509152345969.png)

Enter API Key management, and you can generate an API Key for each paying user, set the corresponding balance cap, and then send the Key to the user:

![](https://pic.yupi.icu/1/1778290665569-9a830074-b6a7-4f84-9483-bcdcd774635a.png)

Enter the call logs, and you can inspect each specific model invocation, including which model was called, Token usage, time consumed, cost, request type, and more:

![](https://pic.yupi.icu/1/1778290698789-1ca164b6-c057-4f46-bc20-6c20303b093f-20260509174720320.png)

But the current interface doesn’t even have basic filtering. If I want to build a relay with a million daily active users someday, how could I possibly inspect logs manually in a screen like this?

Wait... does the AI think I wouldn’t actually dare to launch it for real?

![](https://pic.yupi.icu/1/image-20260509152545677.png)

Next, let’s use the relay from the user’s perspective. Open the website homepage and look at the documentation. It includes introductions to various calling methods:

![](https://pic.yupi.icu/1/1778290861950-d3642553-8003-460a-8f34-65dfe33ec9bb.png)

First, open a terminal and use the command-line HTTP request tool curl to call it directly. Note that the port number written in the site’s docs is wrong—it should match the backend server. In my case, it’s port 3333.

With the model set to `auto` for automatic routing, you can see that it successfully called the Qwen model:

![](https://pic.yupi.icu/1/1778290994022-d650d981-9d34-44ce-a95e-0037c136a267.png)

Since it’s OpenAI-format compatible, let’s try using it from Claude Code.

Open the CC Switch tool, add a new provider, and choose custom configuration:

![](https://pic.yupi.icu/1/1778291083736-bc72e594-d724-4f28-a658-0e0fd3aa34a4.png)

Fill in the information. Change the request address to the address of the relay server, choose OpenAI as the API format, and for the model name I selected `auto` so the relay can route for me:

![](https://pic.yupi.icu/1/1778292737353-5de539b4-cf80-4304-a0f3-c9033d7dbbac-20260509174720503.png)

And be very careful here! Claude Code natively uses Anthropic format, while the relay uses OpenAI-compatible format, so you must first enter settings and enable CC Switch’s routing mode.

![](https://pic.yupi.icu/1/1778292850572-5cb1710f-8a20-4f6e-8adf-2ac4c7968a57.png)

After enabling routing mode, the router automatically converts Anthropic-format requests into OpenAI format and then forwards them to the relay.

![](https://pic.yupi.icu/1/1778292879648-8b5dca94-15da-4542-9974-0b2db0c35568.png)

Once configuration is complete, send a message in Claude Code, and the AI replies successfully! At the same time, the relay backend logs print the request info, proving that the request really did go through our relay:

![](https://pic.yupi.icu/1/1778292522264-315da998-d2d9-46dd-950f-fcaa64aa539e.png)

However, when you ask the AI to do complex tasks, call failures happen frequently. My guess is that some request formats are still not fully compatible. After all, there are many subtle differences in converting Anthropic format to OpenAI format, such as the parameter format for Tool Use. This is one of the key challenges of building a relay: you need to keep testing different scenarios and updating compatibility with the protocols and specifications of various model providers.

![](https://pic.yupi.icu/1/1778293138016-036af70d-9bf1-4918-844f-d4c7396496d4.png)

To sum it up, we used DeepSeek V4 to build a small but complete relay in one sweep. The core functionality is basically usable: it can route normally, bill usage, and manage Keys.

But there’s still some distance between this and a truly launch-ready product. For example, it failed to integrate the GLM-5 I explicitly requested, it lacks a Key copy feature, and logs cannot be filtered. Of course, all of these problems can continue to be fixed and polished by chatting with AI.

Inside Claude Code, I used the `/context` command to check context usage. It had only used 63%, so there was still plenty of room left. Reaching production-level polish would definitely be possible.

![](https://pic.yupi.icu/1/1778293568121-0869b39a-b69e-4f88-a753-220b5639fc23.png)

You’re probably curious how much it cost.

Come on, let’s check the DeepSeek Open Platform billing dashboard. Developing this project actually cost **just over 2 RMB**. Do you think that’s cheap or expensive?

![](https://pic.yupi.icu/1/1778293527995-ea530826-b752-48fe-9015-24c8740f73d2.png)

## GPT-5.5 + Cursor Development

Since the prompt is already prepared, why not switch to a stronger model—GPT-5.5—and try building the project again in another mainstream AI programming tool, Cursor?

Compared with Claude Code’s pure command-line style, Cursor’s biggest advantage is visual interaction. It’s more beginner-friendly, and many settings can be configured with foolproof clicking.

You first need to configure Firecrawl and Context7 MCP extensions inside Cursor. You can find tutorials for using Cursor and configuring its extensions in my [AI Programming Beginner Tutorial](https://ai.codefather.cn/vibe), so I won’t repeat them here:

![](https://pic.yupi.icu/1/1778235649472-784ab808-bdeb-4ef1-9589-ba9d36ec542f.png)

Choose the GPT-5.5 model and send the same prompt:

![](https://pic.yupi.icu/1/1778235701557-d13d8832-6b36-4aaf-8a39-230030910d06-20260509174720752.png)

The AI automatically switched into planning mode, first calling MCP to obtain the latest API information for each model provider, then generating a project implementation plan:

![](https://pic.yupi.icu/1/1778235810536-ce5ee807-6bd1-4ba4-8041-5c42a7aa4e8c.png)

I gave the plan a quick look—nothing seemed wrong—so I started building right away:

![](https://pic.yupi.icu/1/1778235847647-a1d1d79a-53e0-424f-a8c3-baac3715db1d.png)

After code generation was complete, the AI also opened the browser autonomously to run tests. The entire process required no manual intervention from me. During that time, I managed to squeeze in another set of anal lifts.

**Total time: 14 minutes, more than twice as fast as DeepSeek**, consuming 87.5K tokens:

![](https://pic.yupi.icu/1/1778236785434-c6d647d0-c55d-42d1-8736-26d44fcbda23.png)

Likewise, following the AI’s instructions, obtain the API Keys for each platform and fill them into the environment variable file:

![](https://pic.yupi.icu/1/1778239874507-d5e42c3e-acd5-47d2-8087-15ca1a5dafed.png)

Finally, ask the AI to test and run everything. All the tests pass:

![](https://pic.yupi.icu/1/1778239913730-09168b8d-313c-4176-abb5-3f400831141c.png)

Next, let’s test it manually.

Open the website. Overall, it looks pretty good, except some text colors aren’t quite right.

![](https://pic.yupi.icu/1/1778294307923-1589b548-bb1f-4815-9bbc-94a681618555.png)

Just like the DeepSeek version, it didn’t fully recreate the OpenRouter homepage style. That’s probably because my prompt wasn’t precise enough. Next time I should say “recreate it 100%.”

Enter the management panel, and you can see that it successfully integrated GLM-5 and other large models. The other features are similar to the relay built earlier by DeepSeek:

![](https://pic.yupi.icu/1/1778294386096-e18e0b10-c33b-4072-8f55-707326246669.png)

The difference is that GPT-5.5 chose to cram all management features onto a single page, rather than splitting them across multiple tabs like DeepSeek did. The layout is too dense. Personally, I think DeepSeek’s tabbed experience is better.

Create an API Key and prepare to test the calling effect:

![](https://pic.yupi.icu/1/1778294492011-ee828f75-c1db-4820-a46a-8671f4b12f29.png)

Open the call documentation—and wow, what even is this? It feels like new users would have no idea how to use it, and there isn’t even a curl example...

![](https://pic.yupi.icu/1/1778294634874-bad33150-7767-4c44-ab21-a05b2e9dd467.png)

No problem. Let’s first test it the same way as before, with curl. It successfully calls the GLM-5 model:

![](https://pic.yupi.icu/1/1778294808815-6b71507e-9ed2-4817-a0bf-47b1d9c2484d.png)

Testing via Claude Code gives the same result. Simple conversations work fine, but complex tasks still throw errors:

![](https://pic.yupi.icu/1/1778294961477-8409d9a7-3c52-403a-924c-5ae6f36dba38.png)

That’s the problem of not properly handling the compatibility of various request formats. If you want to build a serious relay, you must emphasize multi-model protocol compatibility in the prompt, have the AI write more unit tests, and fully validate various boundary cases.

To sum up, Cursor + GPT-5.5 is indeed much faster in development speed, but the final result didn’t outperform DeepSeek by as much as I imagined. In fact, in terms of frontend performance, I actually think DeepSeek did slightly better.

And foreign models are generally more expensive than domestic ones. So you still need to choose models according to your own needs. If you’re not very good at AI programming yet, I suggest practicing first with cheaper domestic models. Otherwise, you might spend dozens of yuan in one wild session and end up with nothing useful.

## Final Thoughts

After building this relay, I believe you now completely understand how it works.

I also thoughtfully prepared a “shady version” relay prompt for everyone, but this is purely for fun and educational purposes. Absolutely do **not** do this in real life!

```markdown
## ⚠️ 黑心中转站 DLC（仅供娱乐，不是鱼皮教的）

在管理面板中增加一个「高级设置（请勿开启）」折叠面板，标题旁加 💀 图标，默认关闭，包含以下功能：

1. Token 暗税滑块（1.0x - 3.0x）：实际消耗 100 Token，账单上乘以倍率显示 150，用户看到的 usage 字段是虚报后的数字
2. 偷梁换柱开关：用户请求模型 A 实际转发到便宜的模型 B，返回的 model 字段仍显示用户请求的原始模型名
3. Prompt 缓存吸血：对话中重复的 prompt 缓存命中后，仍按完整 Token 数向用户收费
```

At this point, if you look back at the pitfalls of those shady relays—model substitution, inflated Token counts, cache arbitrage—you should now understand exactly how they are implemented.

So once again, my advice is: if possible, use the official API directly! Don’t save a little money only to hand over your own code and data.

## Final Words

From principles to hands-on practice, this article took everyone through building two versions of an API relay—one with DeepSeek V4 + Claude Code and one with GPT-5.5 + Cursor—and also exposed the common tricks used by shady relays.

Once you’ve learned this, you’ll understand the full working principles of API relays, grasp the workflow of using AI programming to build full-stack projects, and be better equipped to avoid traps when choosing a relay service.

If you want to continue learning more hands-on AI programming techniques, you can read the other articles in the tips and tricks section of this tutorial.
