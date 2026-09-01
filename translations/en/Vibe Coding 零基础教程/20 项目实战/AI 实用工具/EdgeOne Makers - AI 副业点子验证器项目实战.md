# EdgeOne Makers - AI Side Hustle Idea Validator Project Practice

> Use AI coding + EdgeOne Makers to build and launch an AI Agent app in 20 minutes

Hello everyone, I’m Yupi.

In the AI era, more and more people are thinking about using AI to make money on the side, and all kinds of ideas are flying around.

But the problem is that most ideas stay at the stage of “this feels like it could make money.” Only after you really try to do them do you realize either the space is already crowded with competitors or nobody is willing to pay at all, and all your time and effort were wasted.

So I thought: could I build an **AI investor Agent** that specializes in checking whether side-hustle ideas are actually靠谱?

Describe your side-hustle idea to it, and it will search the web for competitors, analyze the market, evaluate feasibility, and then judge it like a real investor: how much would it be willing to invest? Or is it something it wouldn’t even take for free?

If you feel your idea has been undervalued, you can keep asking follow-up questions and adjust the plan. It will remember what you said before and dynamically update its valuation.

This way, you can quickly filter out bad ideas and save your time for the things that are truly worth doing.

⭐️ Video version for this episode: [https://bilibili.com/video/BV1jU756mE1x/](https://bilibili.com/video/BV1jU756mE1x/)



## Solution Design
To build an AI app like this, you need to think about a lot of things:

- How do you connect to AI models?
- How do you use web search capabilities?
- How do you isolate chat history across multiple users?
- How do you let the Agent remember context and handle follow-up questions?

Even if you let AI help you solve these, it would still cost a lot of time and tokens.

Tencent Cloud’s [EdgeOne Makers](https://pages.edgeone.ai/zh/document/product-introduction) recently launched Agent hosting capabilities, which happen to solve these problems.

![](https://pic.yupi.icu/1/image-20260629150206869.png)

You only need to focus on writing the Agent’s business logic (for example, how to evaluate a side-hustle idea). Once you deploy it, the platform automatically handles all the rest—web search, conversation memory, model integration, and so on.

![](https://pic.yupi.icu/1/01_%E4%B8%93%E6%B3%A8%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91%E5%B9%B3%E5%8F%B0%E6%90%9E%E5%AE%9A%E5%85%B6%E4%BD%99_compressed_v3.png)

Next, I’ll take everyone from 0 to launch using AI coding + EdgeOne Makers to build this AI investor Agent.

But before we get started, I’ll first quickly deploy an official template through the EdgeOne Makers console so everyone can get a feel for how this platform actually works.



## Quick Experience with EdgeOne Makers

Open the Agent panel in EdgeOne Makers and you’ll see that it provides many Agent app templates by default, supporting mainstream frameworks like OpenAI SDK, Claude SDK, LangGraph, CrewAI, and more. Both JS and Python are supported.

![](https://pic.yupi.icu/1/image-20260629150435803.png)

Here I choose to create an OpenAI Agent template:

![](https://pic.yupi.icu/1/image-20260629150459022.png)

After linking a GitHub repository, you don’t need to change anything. Just click Create and Deploy.

![](https://pic.yupi.icu/1/image-20260629150531427.png)

The system quickly creates a project repository for you, then automatically completes initialization, dependency installation, build, and deployment.

![](https://pic.yupi.icu/1/image-20260629150614707.png)

Click Preview, and you’ll see the temporary testing domain provided by the platform:

![](https://pic.yupi.icu/1/image-20260629150844802.png)

Open it directly, and an AI Agent project is already live and usable. You can chat with AI normally, and the response speed is pretty good too.

![](https://pic.yupi.icu/1/image-20260629151024765.png)

You might be wondering: I didn’t fill in any large-model API Key, so how is it already working?

Open the [Models panel](https://console.cloud.tencent.com/edgeone/makers?tab=models&subTab=models) in the Makers console and you’ll find that EdgeOne Makers already connects mainstream large models for us by default, and for a limited time each user gets 500,000 Tokens per month for free.

![](https://pic.yupi.icu/1/image-20260629151052733.png)

It also automatically creates a default key for calling large models, and when creating a project, it injects that key into the program’s environment variables—so you can use it directly without manually entering a key.

![](https://pic.yupi.icu/1/image-20260629151301325.png)

By this point, you should already have a basic understanding of EdgeOne Makers. You can think of it as a hosting platform built specifically for AI Agents. It already prepares models, tools, memory, monitoring, and more—you just focus on the business logic.

![](https://pic.yupi.icu/1/02_EdgeOne_Makers%E6%98%AFAI_Agent%E6%89%98%E7%AE%A1%E5%B9%B3%E5%8F%B0_compressed_v3.png)

Now let’s get to the main topic. I’ll walk everyone through the full workflow: environment setup → prompt design → AI development → deployment → iterative optimization.

![](https://pic.yupi.icu/1/03_%E5%AE%8C%E6%95%B4%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%E4%BA%94%E6%AD%A5%E8%B5%B0_compressed_v2.png)



## Environment Setup

Before development, install the official Skills bundle provided by EdgeOne. Once installed, AI will automatically know how to write code according to EdgeOne Makers’ requirements (such as where project files should go, how the entry function should be written, and how to call the platform’s built-in web search and conversation memory), so you don’t need to feed it docs manually.

![](https://pic.yupi.icu/1/04_Skills%E6%8A%80%E8%83%BD%E5%8C%85%E8%AE%A9AI%E8%87%AA%E5%8A%A8%E6%87%82%E8%A7%84%E8%8C%83_compressed_v1.png)

Referring to the [official docs](https://cloud.tencent.com/document/product/1552/129329), open the terminal and enter one command:

```bash
npx skills add TencentEdgeOne/edgeone-makers-tools
```

Follow the instructions and choose the Skills you want to install, such as the Agent development skill `/makers-agents` and the deployment skill `/makers-deploy` that we’ll use here.

![](https://pic.yupi.icu/1/image-20260629151510758.png)

Choose global installation scope so all future projects can use it.

Once everything is ready, it’s time to write the prompt.



## Prompt Design

My requirements weren’t complicated, and I had already thought through which framework to use and where to deploy it, so I didn’t ask AI to organize the plan for me. I directly wrote the full prompt myself.

The complete prompt is as follows:

```markdown
帮我开发「AI 投资人」副业验证 Agent，部署在 EdgeOne Makers 平台上。

明确的技术方案：
1. 使用 OpenAI Agents SDK 框架
2. 前端和 Agent 共存在同一个项目里，之后我会一次部署到 EdgeOne Makers
 
开发要求：
1. 体现 Loop Engineering 的思想，自主开发、自主测试验证，最终交付一个完全可用的产品
2. 如果有不明确的地方，先问我再动手

需求描述：
Agent 的设定是见过太多项目的资深投资人，说话毒舌、判断犀利。用户描述自己的副业想法后，它会联网搜索竞品和市场信息，给出愿意投资多少钱的判断（或者「白送都不要」），并说明理由和改进建议。支持多轮对话，用户可以根据反馈调整方案继续追问，Agent 要记住之前聊过的内容。前端采用 Q 版风格，多端适配。
```

To explain it simply, the Loop Engineering idea in the development requirements means that after AI writes the code, it should test and verify it on its own instead of requiring a human to watch every step.

However, note that code deployed to EdgeOne Makers must follow the platform’s conventions, otherwise it won’t run.

So before execution, I first use the slash command to invoke the `/makers-agents` Skill. Then AI automatically writes the code according to the platform’s required entry-function style and its integration approach for web search and conversation memory.

![](https://pic.yupi.icu/1/image-20260629151608806.png)



## Autonomous AI Development
After making sure the `/makers-agents` Skill is in use, I send the prompt and AI starts developing autonomously.

It first loads the Agent development rules from the Skill (if you’re interested, you can read the [official docs](https://pages.edgeone.ai/zh/document/agents) for details), then creates the project and writes the Agent logic and frontend page.

![](https://pic.yupi.icu/1/image-20260629152402163.png)

A few minutes later, AI completed the development of the core functionality and also compiled, verified, and self-checked the code.

![](https://pic.yupi.icu/1/image-20260629152440563.png)

But since no large-model API Key was configured locally, it couldn’t fully test the conversation flow.

That’s okay. Next we’ll deploy it to EdgeOne Makers, configure the keys there, and it’ll be able to run.



## Deployment
Earlier, when we created a template project **through the console**, EdgeOne Makers automatically injected the two environment variables `AI_GATEWAY_API_KEY` and `AI_GATEWAY_BASE_URL` for us.

But if you create the project locally by yourself, you need to **manually** get the values of those two environment variables from the Makers console.

![](https://pic.yupi.icu/1/image-20260629152524645.png)

In addition, since my AI investor Agent needs to search the web for competitor information, I also need to enable Tencent Cloud’s [Web Search API service](https://console.cloud.tencent.com/wsapi/index):

![](https://pic.yupi.icu/1/image-20260629152619126.png)

Just choose the cheapest package first, then get the web search API key.

![](https://pic.yupi.icu/1/image-20260629152752119.png)

After getting these keys, I directly provide the information to AI and use the `/makers-deploy` Skill to let it deploy for me:

```markdown
帮我部署上线：
AI_GATEWAY_BASE_URL 是 https://ai-gateway.edgeone.link/v1
AI_GATEWAY_API_KEY 是 sk-xxxxx
联网搜索 API Key 是 sk-xxxxx
```

![](https://pic.yupi.icu/1/image-20260629152818209.png)

AI automatically sets the environment variables and performs the deployment. On the first deployment, it will remind you to log in and authorize—just follow AI’s prompts.

![](https://pic.yupi.icu/1/image-20260629152852444.png)

Deployment finishes quickly, and you immediately get an online URL you can access. Super convenient!

![](https://pic.yupi.icu/1/image-20260629152913807.png)

Let’s open it and try an idea: build a mini app where AI writes social-media captions for you.

The Agent performed web search, found several competitors, and then gave the evaluation result—*wouldn’t even take it for free*!

![](https://pic.yupi.icu/1/image-20260629153002380.png)

What a brutally honest investor. Absolutely ruthless. I like it.

Although the functionality is working, the default model’s output quality is average. Next let’s switch to a stronger one.



## Switching Models
Open the Models panel in Makers, add a new model—say, the domestic powerhouse DeepSeek—and click Add.

![](https://pic.yupi.icu/1/image-20260629153351219.png)

You need to get a key from the [DeepSeek API Open Platform](https://platform.deepseek.com/api_keys), create a temporary key, copy and paste it into Makers, save it, and then you can use the DeepSeek V4 Pro model.

![](https://pic.yupi.icu/1/image-20260629153416288.png)

So how do you make the Agent use this new model? Do you have to change the code?

**Actually, not at all.**

Take a quick look at the code and you’ll find that model configuration reads `AI_GATEWAY_MODEL` first.

![](https://pic.yupi.icu/1/image-20260629153542980.png)

So we only need to ask AI to set this environment variable and redeploy:

```markdown
设置 AI_GATEWAY_MODEL 环境变量为 deepseek/deepseek-v4-pro
重新部署
```

![](https://pic.yupi.icu/1/image-20260629153614603.png)

After deployment succeeds, open the Makers console and you can see the environment variable has taken effect. Pretty convenient, right?

![](https://pic.yupi.icu/1/image-20260629153737524.png)

Now let’s try the same idea again: build a mini app where AI writes social-media captions for you.

This time the Agent performed multiple rounds of web search, and in the end it delivered another painfully sharp verdict—*I wouldn’t even take it for free.*

![](https://pic.yupi.icu/1/image-20260629153817738.png)

Looking at this analysis, it’s obviously much better than before the model switch, right? It even told me to research a vertical niche...

Alright then, I followed up: I’m a programmer and a UP主—how exactly should I go vertical?

![](https://pic.yupi.icu/1/image-20260629153910912.png)

Wow, this thing would invest 300,000 in me?

![](https://pic.yupi.icu/1/image-20260629153948785.png)

This track analysis is actually kind of interesting. What do you mean the programming education niche has already been completely dominated by the top players—who the heck is this **Yupi**?!

Then looking further down at the key monetization path, isn’t it pretty much what everyone was already thinking?

![](https://pic.yupi.icu/1/image-20260629154052346.png)

In short: **take ads, sell courses, run training**.

Come on, man, does it really have to be this real?

![](https://pic.yupi.icu/1/image-20260629153948785.png)



## Iterative Optimization
At this point, the functionality is already working, but I noticed one problem: multi-turn conversation memory didn’t seem to be working. The Agent didn’t remember what had been discussed earlier.

![](https://pic.yupi.icu/1/image-20260629154338029.png)

So next, it’s time to do some optimization.

First, I asked AI to commit one version with Git. That way, if something goes wrong during the changes, it’s easy to roll back in time:

![](https://pic.yupi.icu/1/image-20260629154359603.png)

Then I asked AI to optimize further, update the deployed website, verify the result autonomously through Browser Use, and fix any bugs:

```markdown
优化项目、更新部署、自主验证并修复 Bug
1. 必须支持多轮对话，用户可以根据反馈调整方案继续追问，Agent 要记住之前聊过的内容
2. 优化前端页面，禁止使用 Emoji，对标商业产品，保持 Q 版风格
3. 优化 Markdown 格式的展示
```

![](https://pic.yupi.icu/1/image-20260629154415031.png)

AI quickly fixed the code, used the `makers-deploy` Skill to update the live site, and then opened the browser to verify the conversation flow on its own.

![](https://pic.yupi.icu/1/image-20260629154440381.png)

Let’s look at the final result. The Markdown rendering looks much more elegant now.

![](https://pic.yupi.icu/1/image-20260629154501108.png)

And this time, the multi-turn conversation memory worked successfully too!

![](https://pic.yupi.icu/1/image-20260629154512485.png)

You’ll notice that throughout the whole process, we never enabled any database or storage service. EdgeOne Makers handled the conversation memory for us. Under the hood, it manages each user’s conversation history, and different users don’t interfere with one another.

![](https://pic.yupi.icu/1/image-20260629154621230.png)

Together with the web search and model gateway shown earlier, all these capabilities become available automatically once deployed—we don’t need to worry about them at all.

![](https://pic.yupi.icu/1/05_EdgeOne_Makers%E7%BB%BC%E5%90%88%E8%83%BD%E5%8A%9B%E4%B8%8EAgent%E5%85%B3%E7%B3%BB_compressed_v2.png)

In addition, if you open the call-chain tracing panel in the Makers console, you can view data such as Agent invocation counts and Token consumption.

![](https://pic.yupi.icu/1/image-20260629154709800.png)

You can even see the full chain log for a single invocation. Every detail of AI generation and tool calls is clearly visible, which makes optimizing the Agent and troubleshooting much easier.

![](https://pic.yupi.icu/1/image-20260629154738024.png)



## Finished Product Experience
At this point, my AI investor Agent is finished, and I can happily use it to validate all kinds of side-hustle ideas.

For example, what if I take freelance orders on Xianyu:

```markdown
在闲鱼上接单，帮人用 AI 写文案/简历/小红书笔记，收费 30 ~ 100 一单
```

Well, looks like that won’t work.

![](https://pic.yupi.icu/1/image-20260629154800071.png)

What if I build an AI API relay service:

```markdown
搭一个 AI API 中转站，帮国内用户方便地调用 GPT/Claude，赚差价
```

Yep, looks like that won’t work either!

![](https://pic.yupi.icu/1/image-20260629154828473.png)

What if I build an AI English speaking practice app:

```markdown
做一个 AI 英语口语陪练 App，用语音对话的方式帮用户练口语，按月订阅 29.9 元
```

Welp, looks like that still won’t work!!

![](https://pic.yupi.icu/1/image-20260629154922290.png)

What if I set up a stall selling programmer fried rice:

```markdown
我要摆摊卖程序员炒饭，通过线上拍短视频营销
```

Ugh... apparently coming up with a genuinely good project idea isn’t easy!

![](https://pic.yupi.icu/1/image-20260629154950801.png)

Forget it, maybe I should just sell courses:

```markdown
我有流量基础，录制编程教程，在自己的平台上卖课，收费几百到几千不等
```

My Chovy!!! Even selling courses isn’t easy.

![](https://pic.yupi.icu/1/image-20260629155029876.png)

Sigh, money is hard to earn and life is hard to swallow.

After that, I tried many more ideas, and every single one got rejected by AI.

![](https://pic.yupi.icu/1/image-20260629155623574.png)

Hmph, I refuse to believe there’s no way to come up with an S-tier idea!

![](https://pic.yupi.icu/1/image-20260629155749578.png)

One person’s power is limited, so I decided to open-source this project. Everyone can directly ask AI to help deploy it to EdgeOne Makers, then use it anytime and anywhere to validate their own ideas. I’ll just sit back and wait for a batch of A-tier and S-tier ideas.

> Open-source link: https://github.com/liyupi/ai-investor

![](https://pic.yupi.icu/1/image-20260629155812766.png)



## Final Thoughts

From writing the code to launching it, the whole process took less than 20 minutes. Looking back, I only focused on the Agent’s business logic, while [EdgeOne Makers](https://cloud.tencent.com/act/pro/edgeone-makers-agent?from=30133) handled everything else for me—web search, conversation memory, model gateway, call-chain tracing, all of that engineering stuff.

In the AI era, the capability of large models is important, but the whole set of supporting capabilities around them is just as important. No matter how strong the model is, without solid engineering support, an Agent can only stay at the local-demo stage. A platform that lets developers focus entirely on business logic instead of constantly reinventing the wheel is incredibly valuable.
