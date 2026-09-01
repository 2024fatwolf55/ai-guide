# Vercel AI 网关 - AI Stress-Relief Helper Project Practice

This article is not mainly about development itself, but about learning the concept and usage of an AI gateway. Through comic-style explanations and a Vibe Coding project, you can learn how to flexibly switch between different models in AI applications with Vercel AI Gateway, reducing development costs and maintenance difficulty. It’s suitable for anyone who wants to learn AI gateway technology and quickly connect multiple AI models.



---



You are Xiao Aba, a newly hired AI application development engineer.

![](https://pic.yupi.icu/1/1761152281564-61073333-da43-4ac2-b6ca-09460e87331a.png)

Your sketchy boss says: The company wants to build an intelligent customer service system recently. Xiao Aba, you’re the newcomer, so this important mission is yours! Truly, when heaven is about to place a great responsibility on someone, it starts with the new hire~

![](https://pic.yupi.icu/1/1761645372915-7d9df0cf-f44a-4643-8d67-3e7103fb03db.png)

You think to yourself: Isn’t it just calling an API? What’s so hard about that?

So you roll up your sleeves and start writing code, first integrating OpenAI’s GPT model.

Just as you finish, your sketchy boss says: We also need to add the Claude model. I heard it performs better in certain scenarios.

So you write another pile of code for calling the Claude model.

And right after you finish that, your sketchy boss says again: Hmm, I heard the domestic Tongyi Qianwen is also pretty good. Let’s integrate that too!

![](https://pic.yupi.icu/1/1761645406716-99acb82f-2f1f-4a62-a3c6-076ac17b1e6d.png)

You frown and think: Now I have to write code for this model too? Boss, are you going a bit too far...

Your sketchy boss seems to hear your inner thoughts:

- Oh, by the way, calling AI costs money, so we need proper user authentication
- Oh oh, to prevent malicious users from spamming AI calls, we also need rate limiting
- Oh oh oh, AI-generated content may have issues, so we also need content safety checks
- Oh oh oh oh! We also need to keep the system stable—if one model goes down, the entire service can’t go down with it
- Oh oh oh oh oh!! This project is definitely going to blow up, so we also need to think about how AI can handle massive traffic
- Oh oh oh oh oh oh!!! We also need to observe AI call counts and costs to improve efficiency and reduce expenses
- Oh oh oh oh oh oh oh...

Watching your boss gradually lose their mind, you start questioning life itself: why is calling an AI API this complicated?

![](https://pic.yupi.icu/1/1761645432489-6e2f67db-40f5-40fe-a6f0-c18ead6e6d8a.png)



⭐️ Video version of this article: [https://bilibili.com/video/BV14NyrBTEeB](https://www.bilibili.com/video/BV14NyrBTEeB)



## What Is an AI Gateway?

At this moment, Yupi—who calls himself the “Little AI Prince”—walks over. Seeing your miserable expression, he smiles and says: What, is this hard?

You’re a little annoyed: Easy for you to say. With this many requirements, don’t I have to write a giant mountain of code?

Yupi: All the scenarios your boss mentioned can be solved through an **AI gateway**~

You ask in confusion: Gateway? What’s that?

Yupi: A gateway is like the ticket gate at a train station. All passengers must first go through the ticket gate, where the staff check your ticket and direct you to the right platform.

![](https://pic.yupi.icu/1/1761645506547-26d820e6-cda3-482e-a7e9-dcadcbbb0445.png)

In system architecture, requests from frontend users first pass through the gateway. The gateway handles things like user authentication, blocking malicious requests, traffic control, monitoring, and request statistics in a unified way, then forwards the requests to backend servers for processing.

![](https://pic.yupi.icu/1/1761645542774-a2da29dc-3d2c-4e1b-adcf-dc5dd59d0881.png)

You nod: Wow, in that case, if I have multiple backend services, I don’t need to implement those features separately for each one.

Yupi: Exactly. And if one backend service goes down, the gateway can automatically forward the request to another service.

![](https://pic.yupi.icu/1/1761645571947-8cb4a141-7d6f-4add-a82b-7a70716f23e7.png)

Now you’re curious: So what exactly is the AI gateway you just mentioned?

Yupi: Traditional API gateways are usually placed between your application and various backend services. An AI gateway, on the other hand, is specifically designed for AI applications and sits between your app and different AI model services (such as OpenAI, Tongyi Qianwen, DeepSeek, and so on).

![](https://pic.yupi.icu/1/1761645615469-787296d8-1fb6-4452-b406-c79ef537f193.png)

Your application only needs to send a **standard request** to the AI gateway. It then automatically handles a whole series of complex tasks for you, such as user authentication, rate limiting, security protection, failover, load balancing, monitoring, and statistics, before forwarding the request to the AI large model.

![](https://pic.yupi.icu/1/1761645642401-683e786e-3e06-420a-abce-cd43f7bfa901.png)

If you want to connect different large models, you only need to change the model name in the standard request. The AI gateway handles the routing for you, so you don’t need to write a separate integration layer for every model~

![](https://pic.yupi.icu/1/1761645657980-b463d0b2-eecd-4635-99ee-fed9f121bf4e.png)

You cheer: This is insanely powerful! With an AI gateway, all the problems the boss mentioned can be solved! So what AI gateway products are available right now?

![](https://pic.yupi.icu/1/1761645679096-3ceb73df-a858-4410-abc1-041222b497f4.png)



## AI Gateway Options

For many AI enthusiasts, the first AI gateway they encounter may be [OpenRouter](https://openrouter.ai/). It’s more like an aggregation platform for AI models, supporting unified access to hundreds of models through one interface.

![](https://pic.yupi.icu/1/1761645719834-eadcde16-711c-474c-9838-5ea5f01be452.png)

A lot of AI tools support configuring OpenRouter. For everyday AI users, it provides access to more large models and more stable services.

![](https://pic.yupi.icu/1/1761645743475-53493cb1-5be9-4b0b-8b9a-a497ac13d7c7.png)



You ask: Are there also AI gateway products specifically aimed at developers?

Yupi nods: Of course. There are already quite a few mature AI gateway products on the market. For example, if you search online, some of the top ones include:

1) [Vercel AI Gateway](https://vercel.com/ai-gateway): a very popular new product lately. Its biggest strengths are how easy it is to get started and its **zero markup** pricing. If you use your own API Key, the gateway itself doesn’t charge extra. It’s suitable for frontend developers who want to quickly build full-stack AI apps.

2) [Cloudflare AI Gateway](https://www.cloudflare.com/zh-cn/developer-platform/products/ai-gateway/): since Cloudflare is one of the world’s largest CDN providers, its AI Gateway mainly benefits from broad global node coverage and strong security protection.

3) [Kong AI Gateway](https://konghq.com/products/kong-ai-gateway): Kong itself is already a very mature API gateway, and now it has been enhanced specifically for AI scenarios with fairly complete enterprise-level features.

![](https://pic.yupi.icu/1/image-20251018111819481.png)

4) [Higress AI](https://higress.ai/): an open-source AI gateway from Alibaba Cloud that supports unified protocol conversion for more than 100 large models and provides enterprise-level features such as semantic caching, token rate limiting, and MCP conversion. It’s suitable for companies with complex AI integration needs.

![](https://pic.yupi.icu/1/image-20251019163817976-20251028181254777.png)



You scratch your head: This still looks way too complicated. How should I get started with AI gateways?

Yupi: Don’t worry. We can start with the relatively simple Vercel AI Gateway. Talk is cheap—give me 2 minutes and I’ll show you how to learn Vercel AI Gateway through hands-on practice~



## Vercel AI Gateway Hands-on Practice

#### 1. Register and Get an API Key

First, go to the [Vercel official website](https://vercel.com/) and register an account. If you bind a bank card, you can get a free $5 usage credit, which is enough for learning and testing.

![](https://pic.yupi.icu/1/1760687990497-90720fbb-0df6-4ede-87b8-64b8702994e9-20251028181254840.png)



Then create an API Key in the console. Be careful not to leak it:

![](https://pic.yupi.icu/1/1760688078133-7b91b6f3-2fc4-4bb4-b2c1-d517699f0968-20251028181254879.png)



#### 2. Official Demo

Next, you can follow the official quick start guide to create a project and run an AI chat demo:

![](https://pic.yupi.icu/1/image-20251019160232722.png)



In short, there are 4 steps:

1. Create a new project
2. Install the dependencies for AI SDK and AI Gateway
3. Configure environment variables and fill in the API Key information
4. Write the sample demo code



#### 3. Stress-Relief Helper Project

But the official demo is a bit too simple. Why not use AI to build a **Stress-Relief Helper** website project, where users can chat with an AI specifically designed to help them relieve stress?

Here I chose Cursor as the AI development tool and directly asked AI to generate the full frontend + backend code that meets the requirements.

![](https://pic.yupi.icu/1/1761645829262-bd9950ef-6334-410f-ab27-140873cb56a4.png)

Since Vercel AI Gateway is relatively new, AI might not understand how to use it. So I directly fed the official Vercel AI Gateway documentation into Cursor and let it learn from the docs.

![](https://pic.yupi.icu/1/1761645854330-54b6ab38-7f1f-45a5-ac34-463ee63477a7.png)



The full prompt is as follows:

```markdown
你是一位专业的程序员，请帮我开发《减压小能手》网站，用户可以通过和专门帮人减压的 AI 聊天来缓解压力。

## 开发要求

1. 需要包含完整的前端和后端，后端使用 Node.js
2. 使用 Vercel 的 AI Gateway 实现 AI 能力，需要先通过官方文档来获取尽可能多的用法：https://vercel.com/docs/ai-gateway/getting-started
3. 以完成核心功能为目标，确保项目可以正常运行，不用输出文档、也不要做任何多余的功能
4. 整体网站界面采用让人放松的浅色，响应式适配各种尺寸的设备
```



After clicking run, AI first called an MCP tool to fetch information from the web page. Here I used `Firecrawl MCP`:

![](https://pic.yupi.icu/1/1760690503357-7412db47-4389-49e2-b42c-dc6eabdc283b-20251028181255024.png)



After about 6 minutes, AI finished generating all the code. Unfortunately, AI wasn’t very obedient here and still generated a bunch of documentation, which took even more time than the code generation itself!

![](https://pic.yupi.icu/1/image-20251019161322770.png)



Then create a `.env` environment variable configuration file in the root directory and fill in the AI Gateway API Key:

![](https://pic.yupi.icu/1/1760689844332-79459841-46e3-4356-9fe7-76062a90464c-20251028181255097.png)



Finally, install dependencies and run the startup script:

![](https://pic.yupi.icu/1/1760690024471-f89bf1e3-3d9e-4857-8a68-a236ffa0af14-20251028181255125.png)



Visit `localhost:3000` and you’ll see the project:

![](https://pic.yupi.icu/1/1760690223277-56f89c2a-b4c5-43d6-a61d-3f744bcd9aef-20251028181255161.png)



Honestly, the result is really nice. It even gave me a bit more motivation to write a few more words, haha:

![](https://pic.yupi.icu/1/1760690245830-e877986b-1bb6-4c6a-96ad-92b738a57fed-20251028181255188.png)



You exclaim: With this AI + AI gateway combo, building AI projects is ridiculously fast!

Yupi nods: Exactly. And through the whole process, we don’t need to worry about one model going down—the gateway automatically handles those issues.

![](https://pic.yupi.icu/1/1761645903883-94c22619-2cac-41a4-87c3-d51ec96586e0.png)



#### 4. More Features

On top of that, Vercel AI Gateway supports a huge number of domestic and international large models, each with different pricing standards:

![](https://pic.yupi.icu/1/image-20251019165234650.png)



You can also configure your own model API Key:

![](https://pic.yupi.icu/1/image-20251019162655475.png)



It also provides enterprise-level features such as **observability**, helping you understand AI usage and analyze costs:

![](https://pic.yupi.icu/1/1760691345180-9ce7ec43-c651-4c19-a918-90b87034b7fe-20251028181255384.png)



Your eyes light up: Wow, then I’ll use this for all my future AI projects!

Yupi shakes his head helplessly: Xiao Aba, remember this—**there is no silver bullet**.

If your personal project only needs to call a single AI model, calling the API directly is enough. If your personal or team’s small project needs AI gateway features (such as integrating multiple models), then Vercel AI Gateway is a good choice. But if you’re building enterprise-grade applications with high requirements for security and stability, then a more professional gateway like Higress or Kong is more suitable—and can help you write a little less spaghetti code 💩!

![](https://pic.yupi.icu/1/1761645922466-4284b8ac-7928-424e-a0eb-09629e7e66a1.png)



## The Ending

A few months later, you used an AI gateway to refactor the company’s intelligent customer service system, and the results were excellent.

You sigh: This really is what it means to stand on the shoulders of giants. Sure enough, don’t reinvent the wheel—lazy people drive the world forward!

![](https://pic.yupi.icu/1/1761645939970-276a3391-2f40-4b85-8d23-d36c5a491f8c.jpeg)

Yupi complains coquettishly: So *that’s* your excuse for being too lazy to give me a like???

![](https://pic.yupi.icu/1/1761646182922-0edead80-b8e9-4b8f-a90d-e35fa8712f3b.png)


## Recommended Resources

1) Yupi AI Navigation Website: [Comprehensive AI Resources, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Paths, Programming Tutorials, Practical Projects, Job Hunting Guide, Q&A](https://www.codefather.cn)

3) Programmer Interview Cheatsheet: [High-Frequency Topics for Internships / Campus Hiring / Experienced Hiring, Plus Real Interview Question Analysis](https://www.mianshiya.com)

4) Programmer Resume Writing Tool: [Professional Templates, Rich Example Sentences, Direct to Interview](https://www.laoyujianli.com)

5) 1-on-1 Mock Interview: [A Must-Have for Internship / Campus Hiring / Experienced Hiring Interviews to Land Offers](https://ai.mianshiya.com)
