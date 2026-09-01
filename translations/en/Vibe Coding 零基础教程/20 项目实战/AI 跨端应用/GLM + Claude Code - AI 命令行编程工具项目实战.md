# GLM + Claude Code - AI Command-Line Programming Tool Project in Action

This project will take you through using pure Vibe Coding to build an AI command-line programming tool called Yupi Code, benchmarked against Claude Code, with Claude Code itself.

The project is developed entirely through conversations with AI, without writing a single line of code. It’s suitable for students who want to quickly practice the complete Vibe Coding development workflow and learn how to use AI to build AI tools.

---

Hello everyone, I’m programmer Yupi. Recently, a friend of mine started learning AI programming (thanks to my influence), and she heard that Claude Code was an awesome AI programming tool. But when she tried it, she found out that it requires a foreign Claude account to log in.

![](https://pic.yupi.icu/1/1766562559951-d1371bb9-99d3-467a-aeec-421cd12eb3bb.png)

Then she started ranting to me about it.

So I jokingly said: Don’t be sad—how about I just make you a Claude Code instead?

![](https://pic.yupi.icu/1/1766562773776-4a34c38c-c95b-4eb9-8b02-81ca86133188.png)

And she actually took it seriously!

Me ↓

![](https://pic.yupi.icu/1/1766562833168-97c7d4fc-bfe5-4a09-9215-dcfbdb546cb4.png)

Well, no choice now—I had to give it a shot.

As luck would have it, the domestic AI model GLM-4.7 had just been released in the past two days. I saw tons of bloggers online hyping it up as “the strongest coding model in China,” “the strongest open-source model,” “the best Claude replacement,” and even saying it surpassed GPT-5.2 and Claude Sonnet 4.5.

![](https://pic.yupi.icu/1/1766563074181-1ee8e12d-2868-4b23-b993-c0e61800565e.png)

Calling it the strongest domestic model is one thing—but stronger than Claude? You expect me to believe that?

Perfect then. I’ll try using GLM-4.7 to build my own AI programming tool, benchmarked against Claude Code, and see how much GLM-4.7 is really worth.

![](https://pic.yupi.icu/1/1766551074508-575a037d-174a-43d2-bbfe-e223082fc665.png)

So next, let’s **use GLM-4.7 + Claude Code together** to build an **AI programming tool powered by GLM-4.7 that imitates Claude Code**.

Before starting the project, let’s give it a loud and memorable name: `Yupi Code`!

Next, we’ll follow this “Yupi AI Vibe Coding Workflow for Building a Claude Code-Like Yupi Code” step by step, without writing a single line of code, to gradually build our very own “Claude Code”!

- Environment preparation => install tools and configure the environment so we can do Vibe Coding
- Technical research => confirm that the requirements can actually be met
- Design and development => including solution design, code generation, and bug fixing, resulting in an MVP
- Version control => prevent later modifications from breaking things
- Capability enhancement => support more Claude Code-like features such as web search, streaming output, deep thinking, and so on

![](https://pic.yupi.icu/1/1766549738919-9e627293-954a-4f39-8625-d1dcb1835cbc.jpeg)

## Environment Preparation

Zhipu’s GLM-4.7 is compatible with multiple coding tools. In addition to Claude Code, it also supports major tools such as Cursor and Cline, making it flexible across different development scenarios.

Connecting GLM to Claude Code is also very simple—it takes just 1 minute.

First, open a terminal and run one command to install Claude Code:

```shell
npm install -g @anthropic-ai/claude-code
```

Then run the `claude` command to open the program. By default, you need to log into a Claude account before you can use it:

![](https://pic.yupi.icu/1/1764145940075-ace6fd24-a09c-41c0-b400-1cffc394fc8a.png)

But that’s okay. Let’s swap the AI model behind it to the domestic GLM-4.7. First, go into the `{user directory}/.claude` directory and create a `settings.json` configuration file:

![](https://pic.yupi.icu/1/1764146110361-06e13de5-7de4-4fc5-9533-3651447d5e19.png)

Then modify the contents of the config file as follows, and remember to replace them with your own API Key:

![](https://pic.yupi.icu/1/1764146125955-3029843c-26b8-4628-b2b7-a9d8abb2aef1.png)

You can get the API Key directly from the Zhipu development platform:

Link: https://bigmodel.cn/

![](https://pic.yupi.icu/1/1766552195823-7f90ead2-3e07-4eb4-92e2-7ef12c591e61.png)

After that, you can happily start using it~

![](https://pic.yupi.icu/1/1766549578200-7189d326-db17-4edd-9e27-2d9da3af06cf.png)

Besides this approach, the official documentation also provides an even simpler option: just use the automation assistant and follow the guidance to complete the environment setup.

![](https://pic.yupi.icu/1/1766552079851-2cd903df-febb-4860-98fc-51c1143b4105.png)

## Technical Research

If you want to build a project entirely with AI, there are several difficulties:

1. The project needs to include both a complete frontend and backend, so the LLM must have strong **coding ability**
2. The backend needs to integrate with an AI model, and each model has different integration and development methods, so the AI needs to **read documentation** to understand the latest way to implement it
3. If you want to optimize the UI, you also need **image understanding ability**, so that just by giving the AI an image, it can reproduce it

Before formal development, we need to confirm that the combination of GLM-4.7 and Claude Code can satisfy these capability requirements.

According to Zhipu’s official introduction, Claude Code has Zhipu-specific MCP tools built in, so developers don’t need to install them manually. These include **search and webpage reading** capabilities, as well as **visual understanding** that can directly interpret screenshots, design drafts, and error images.

Let’s test them one by one. First, the web search capability, keeping up with current events:

![](https://pic.yupi.icu/1/1766541771159-00bcb3ee-422b-4895-9ab6-15e5ad44937e.png)

Then test webpage reading by having it read information from our Programming Navigation website:

![](https://pic.yupi.icu/1/1766485091937-8555eddf-7301-4161-92d9-4f19251cf9d1.png)

Then test image understanding. I uploaded a background image called “Ranking from Solid to Trash”:

![](https://pic.yupi.icu/1/1766552716828-cc3c5015-a220-44c4-9c99-9ea6e6cc9a2e.png)

The AI’s understanding was quite accurate, and it even extracted the specific text.

OK, all of the key capabilities meet the requirements. Next, let’s move into the design and development phase.

## Design and Development

First, create a clean project directory called `yupi-code`, open a terminal, and enter that directory:

![](https://pic.yupi.icu/1/1766545100781-86907b5b-56df-42de-a36f-21b2738102cd.png)

Then enter the prompt:

```markdown
帮我开发一个类似 Claude Code 的终端 AI 编程工具，能够使用 GLM-4.7 模型帮用户回答问题和生成代码
```

Generally speaking, the very first prompt of an entire project is the most important. If I were developing a complex commercial project, I would definitely polish that prompt carefully, probably writing several hundred words (students who have seen my [AI Programmer Training Ground project](https://mp.weixin.qq.com/s/cd7K9WQiOkP7AJglZ1b1Ng) should know what I mean).

![](https://pic.yupi.icu/1/1766553004293-19edef3f-ab54-4275-83fa-d5d78ed1a8ce.png)

But when testing an AI model, I like to do the opposite. I deliberately enter a simple one-line prompt from the perspective of an average user to see whether the AI can guide me toward generating a project that actually satisfies the requirement.

Sure enough, the AI judged this to be a complex project and wanted to enter **planning mode**—first clarify the requirements, then design the solution, and only then start development.

![](https://pic.yupi.icu/1/1766545143400-e5909edc-d015-4ed8-8a98-c1428a5807e4.png)

Next, we need to clarify the requirements through selections and let the AI generate a solution.

Claude Code’s interaction design is actually quite good. First it asks you to choose a programming language. I suggest honestly choosing the first one recommended by the AI:

![](https://pic.yupi.icu/1/1766545700277-0a92c7af-af6a-4bf3-b045-b35a8810fe82.png)

Next comes selecting the features the project should have. In the past, I might have first asked AI to develop only the basic chat functionality, get the flow running, and then add other features later.

But now I have more confidence in AI—**let’s just select all the features and go for it!**

![](https://pic.yupi.icu/1/1766545748726-b5bcf0c2-1650-409d-9cfb-56874d80e7aa.png)

I won’t go over the other settings in detail:

![](https://pic.yupi.icu/1/1766545906676-50ffc0ba-404a-42e0-af0e-c4797a5d5d77.png)

After the selections are complete, the AI gives a detailed implementation plan. Be sure to read it carefully:

![](https://pic.yupi.icu/1/1766546189349-27a4a8d7-92c0-4cf4-931e-e98e304736c9.png)

You can execute it directly, or give the AI further guidance. For example, I had the AI-generated app call the Base URL of Zhipu’s Coding Plan package to save some cost, and I also gave the AI an official API document so it could generate more accurate code.

![](https://pic.yupi.icu/1/1766546246817-adc95f50-246d-4c9c-b0cd-35f6433c9b40.png)

After confirmation, execution begins. The AI first calls its built-in tools to search and parse documentation:

![](https://pic.yupi.icu/1/1766546433884-517bb8d9-8eb0-4a44-bd9c-0b0591af4184.png)

Then the AI lists a Todo List and generates code and documentation step by step:

![](https://pic.yupi.icu/1/1766546471145-170595b6-05b5-440e-a208-671c362eb002.png)

During this process, if you notice a serious problem—such as the AI-generated code clearly going completely off track—then pause it or manually give it prompts to guide it as early as possible. But if the issue is only that one small section of code is wrong, my suggestion is to tolerate it for now, because in the end the AI will most likely discover and fix the problem by itself.

After about a dozen minutes, the AI finished generating everything and even told me how to use it:

![](https://pic.yupi.icu/1/1766546800949-d8f28864-141e-477e-af98-a25bf02d99e7.png)

Unfortunately, I couldn’t be bothered to read any of that. Why not just hand the API Key to the AI and let it run it for me?

In the Vibe Coding development model, every extra thing I do myself is a form of disrespect to the AI.

![](https://pic.yupi.icu/1/1766553290398-ad4d9c90-f804-4f46-b040-c65f821897d0.png)

Enter the prompt:

```markdown
我的 API key 是 xxxxxxx，请你帮我运行
```

And then... it crashed.

![](https://pic.yupi.icu/1/1766546943625-ae073ada-da33-429a-bbf8-a642f50204dd.png)

No panic—just let the AI inspect and fix the errors itself. And for convenience, it should also provide a quick-launch script so I can start the AI programming tool with a single command, just like running Claude Code.

Prompt:

```markdown
帮我检查并修复项目中的错误，并创建一个可以像 Claude 一样让用户在命令行输入 "yupicode" 就能启动程序的快捷脚本
```

A few minutes later, the AI finished the repair and provided a `yupicode` script:

![](https://pic.yupi.icu/1/1766547157316-1e78081d-7d98-43c2-8fc6-37f40dcd1d81.png)

I opened a new terminal, ran the `yupicode` script, and tried chatting with the AI:

![](https://pic.yupi.icu/1/1766488187720-0dedd977-3663-4146-8fc6-bd5e8d65a7ea.png)

And honestly, it worked pretty well!

Just like Claude Code, it also provides some commands such as clearing conversation history and viewing help:

![](https://pic.yupi.icu/1/1766488215355-476254ae-1fdd-44fe-94a7-939621a5b3f3.png)

At this point, I felt that the project was basically usable. I recommend putting the project under Git version control to prevent later modifications from breaking things.

What? You don’t know what Git is?

No worries—just leave it to the AI:

```markdown
现在项目已经基本可用了，帮我提交一个 git 版本，防止后续改动出问题
```

![](https://pic.yupi.icu/1/1766547719776-e4ca2495-158d-441e-b995-d2e3b475187b.png)

After testing, the current Yupi Code still has some shortcomings—for example, it doesn’t support search:

![](https://pic.yupi.icu/1/1766488309079-9e05324c-b780-4476-b7a1-09e0b0a12ed4.png)

So next, let’s optimize the project and add more capabilities supported by Claude Code.

## Capability Enhancement

1) First, let’s add web search capability. We can simply throw the official Zhipu documentation at it. The prompt is as follows:

```markdown
现在好像不支持网络搜索，请参考
  https://docs.bigmodel.cn/api-reference/%E5%B7%A5%E5%85%B7-api/%E7%BD%91%E7%BB%9C%E6%90%9C%E7%B4%A2
  文档，增加网络搜索工具调用能力
```

![](https://pic.yupi.icu/1/1766547400820-047db1e2-dee7-4bb3-875c-3c3d03d7bf60.png)

Very quickly, the AI added the new feature. After reopening `yupicode` to validate it, it worked correctly:

![](https://pic.yupi.icu/1/1766542072968-2a635280-4f04-41c7-9e72-b149b503b18e.png)

2) Next, let’s optimize the AI response experience. Right now it freezes for a moment and then dumps the full reply all at once. It should be changed into a typewriter-like streaming output effect.

Prompt:

```markdown
我希望在等待 AI 回复时，有一个转圈的小图标；并且 AI 的回复可以实时流式输出
```

The AI quickly got it done:

![](https://pic.yupi.icu/1/1766547560315-96b3044c-21d4-4017-b3b2-8e6c599fdfac.png)

3) GLM-4.7 further strengthens interleaved reasoning by introducing **retained thinking** and **turn-level thinking**, making complex-task execution more stable and controllable. We should also have Yupi Code output the model’s reasoning information, tool-calling information, and so on, so users can understand what’s happening.

Enter the prompt:

```markdown
帮我输出模型思考的信息、以及工具调用信息，你可以通过官方文档来了解如何开发
```

![](https://pic.yupi.icu/1/1766547838246-0de4e1a6-46e7-4fa0-9f69-2cc6c137d941.png)

Let’s test the optimized effect—for example, by asking “Introduce Yupi’s AI navigation website.” You can see the reasoning process very clearly:

![](https://pic.yupi.icu/1/1766491085646-e55d65e2-f1f4-4de5-9b2e-a580f6671fab.png)

## Mission Accomplished

At this point, Yupi Code—the tool built in imitation of Claude Code—is complete. Let’s use it to build a small website.

For example, let’s make a demo website that teaches sorting algorithms with animation. Prompt:

```markdown
帮我开发一个学习冒泡排序算法的动画网站，使用 Q 版动漫的风格和吉伊卡哇感觉的配色
```

![](https://pic.yupi.icu/1/1766491627903-c7a8401b-a029-4f60-86c2-583459f60098.png)

As shown, the visual style is pretty good. But if the LLM could automatically generate illustrations and add them into the site in the future, that would be even better.

![](https://pic.yupi.icu/1/1766492330648-78beb8fe-20f5-4577-9a5a-9c6844b15ba1.png)

Let’s build another one—a realistic electronic blackboard. Prompt:

```markdown
帮我开发一个仿真的电子黑板，用户可以在上面画画并导出为图片
```

![](https://pic.yupi.icu/1/1766543009945-1be675f7-2cb1-43ce-9794-36cfa3cf9f87.png)

It’s Christmas, so Yupi drew everyone a Christmas tree and even included a little gift. How is that not programmer romance?~

![](https://pic.yupi.icu/1/1766548114861-81c8b4d2-b7fc-4134-8722-264edf56f229.png)

------

OK, that’s the whole process of how I **used the domestic AI model GLM-4.7 + Claude Code** to build **Yupi Code based on GLM-4.7**.

From my own experience, compared with previous domestic models, GLM-4.7 has improved in stability when handling complex tasks. Even when it encounters problems, it can automatically repair them, making the final generated code runnable.

On top of that, GLM-4.7’s tool-calling ability has also been strengthened. When paired with AI programming tools like Claude Code, it directly includes common capabilities used in AI programming—such as web search, webpage reading, and image explanation—so you no longer need to look for MCP tools yourself to enhance it.

Honestly, as a loyal developer who has been following Zhipu AI for a long time, I can genuinely feel how much effort they’ve put into AI programming over the last few months. I’m sure everyone can see it too.

That said, the current Yupi Code was still built in one big AI sweep, so there are many places that can still be optimized and improved. If I get time later and everyone is interested, maybe I’ll really polish this tool and open-source it properly. My ultimate goal is for the programming tool **Yupi Code based on GLM-4.7**, which itself was built with **the AI model GLM-4.7 + Claude Code**, to be able to build another **GLM-4.7-based** programming tool—something like Yupi Son Code. I believe a truly good AI tool should be able to recurse infinitely and self-bootstrap like crazy!

![](https://pic.yupi.icu/1/1766549948743-c5e1340a-5b3d-4419-b5df-c2fd4a5c2c7f.jpeg)

If you get it, clap~

## Recommended Resources

1) Yupi's AI navigation site: [AI resource collection, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning circle: [Learning paths, programming tutorials, hands-on projects, career guides, Q&A](https://www.codefather.cn)

3) Programmer interview cheatsheet: [Internship/campus/social recruitment key points, enterprise question analysis](https://www.mianshiya.com)

4) Programmer resume tool: [Professional templates, rich examples, direct to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [Essential for internship/campus/social recruitment interviews to get offers](https://ai.mianshiya.com)
