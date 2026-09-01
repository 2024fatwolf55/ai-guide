# Cursor + Claude Fable 5 - Is It Installed Yet? Desktop APP Project in Action

> Use Cursor + Claude Fable 5 + Loop Engineering to build an Electron app + admin backend in one go

Hello everyone, I’m programmer Yupi.

Anthropic has just released the mythic-level model Claude Fable 5. Its AI programming benchmark scores crush the competition, scoring 80.3% on SWE-bench Pro—far ahead of GPT-5.5’s 58.6% and Opus 4.8’s 69.2%.

I tried using it to refactor the leaked Claude Code source code, and it ran perfectly. It’s absurdly strong!

![](https://pic.yupi.icu/1/1781056792310-48d8afe0-128a-4e65-905d-23136cdc61a9-20260611164929073.png)

But it’s also currently the most expensive model in the world: $10 input / $50 output per million tokens—twice the price of Opus 4.8 and 50 times that of DeepSeek V4!

![](https://pic.yupi.icu/1/01_%25E4%25B8%25BB%25E6%25B5%2581AI%25E6%25A8%25A1%25E5%259E%258B%25E5%25AE%259A%25E4%25BB%25B7%25E5%25AF%25B9%25E6%25AF%2594%25E8%25A1%25A8%25E6%25A0%25BC_compressed_v2.png)

Now that model capability has reached this level, some of my old ideas can finally start becoming reality, hehe...

I remember last year, programming beginners often asked me how to install certain software or environments. So I thought: why not let AI help me build a website that automatically installs software? I even gave it a cool name: “Is It Installed Yet?”

But back then, after talking with AI for several hours, all I got was a pile of bugs, and I had to abandon it in frustration.

Now Claude Fable 5 has given me much more confidence. This time I don’t just want it to help me build the “Is It Installed Yet?” desktop APP—I also want it to build the web admin backend in one shot, taking it from 0 to fully usable, just to see whether it can really handle a complex project like this.

And this time I also incorporated the recently popular idea of **Loop Engineering**. Boris, the father of Claude Code, and Peter, the father of OpenClaw, have both been strongly promoting this concept. The core idea is that instead of manually prompting AI line by line, you design a loop mechanism so AI can execute, validate, and repair by itself until the goal is achieved.

![](https://pic.yupi.icu/1/01_Loop_Engineering%25E6%25A0%25B8%25E5%25BF%2583%25E6%25A6%2582%25E5%25BF%25B5%25E5%25BE%25AA%25E7%258E%25AF%25E5%259B%25BE_compressed_v2.png)

Next, I’ll take everyone through the complete hands-on process, using Claude Fable 5 in Cursor the whole way.

## 1. Prompt Design

Let me first briefly explain what “Is It Installed Yet?” is supposed to do.

Users enter the name of the software they want to install (for example, MySQL or Node.js), and the system uses an AI model to automatically generate a complete installation script and plan, with support for one-click execution. It’s meant to completely solve the pain of setting up environments for programming beginners.

### First, Let AI Help Me Write the Prompt

My requirements were fairly scattered. If I didn’t organize the prompt clearly first and just threw it directly at Claude Fable 5, that would basically be a waste of tokens.

So I first used an AI conversation to feed Claude Opus 4.6 my scattered ideas and rough materials, and asked it to organize everything into one complete prompt.

```markdown
我想通过一条提示词，让 Claude Fable 5 + Cursor 帮我自主开发一个「装了吗」桌面 APP，兼容 Mac 和 Windows 系统。同时我要求它通过联网搜索调研 Loop Engineering 的最新理念，在提示词中体现出循环自主的感觉，确保 AI 能自主完成任务。

@需求描述
```

![](https://pic.yupi.icu/1/1781162074833-0d4935e4-fc59-4aee-b226-81220132a1ef.png)

To let the AI autonomously test AI-related functionality during development, I also needed to give it the model API Key in advance. But I didn’t want to put the Key directly into the prompt—if it leaked, that would be a problem.

A better approach is to let the AI read an existing local config file. For example, I had it read my Claude Code config at `~/.claude/settings.json`, so it could get the API Key and Base URL from there.

### Prompt Breakdown

After several rounds of conversation, the AI helped me generate a complete prompt with a very clear structure:

![](https://pic.yupi.icu/1/image-20260611162938865.png)

Let me briefly explain the structure of this prompt.

1) Role definition: a full-stack engineer skilled in Python + Electron + React development.

2) Task description: build a complete system called “Is It Installed Yet?” to help programming learners install software with one click.

It includes three parts:

- Electron desktop APP: the user enters the software they want to install, chooses a version and platform, and the AI generates an installation plan with one-click install support
- Python server: centrally handles AI-generated plans, stores data, and provides APIs
- Web admin backend: lets administrators manage all plans and user feedback

3) For the tech stack, the desktop side uses the **Electron** framework. Electron is a framework for building cross-platform desktop apps with JavaScript, HTML, and CSS. One codebase can be packaged for both Mac and Windows, and familiar apps like QQ, VS Code, and Notion are all built with it.

4) The core highlight is the final “autonomous development loop,” which is where the Loop Engineering idea shows up:

1. The AI maintains a `PROGRESS.md` file in the project root to record the current phase, completed items, and items in progress
2. Every time it completes a module, it immediately compiles and runs validation; if there’s an error, it fixes it before moving on to the next module
3. After all features are finished, it performs a complete end-to-end test from the user’s perspective
4. If the same problem is repaired more than 5 times and still isn’t solved, skip it to avoid an infinite loop

This way, the AI won’t stop after writing code and wait for me to validate it manually. Instead, it keeps running in a loop by itself, validating and repairing as needed until the whole system is usable.

💡 The full prompt and more hands-on tutorials are included in my free open-source [AI Programming Beginner Tutorial](https://ai.codefather.cn/vibe), with thousands of images and hundreds of thousands of words to help you learn AI programming from scratch.

> Open-source link: https://github.com/liyupi/ai-guide

![](https://pic.yupi.icu/1/image-20260610121356925-20260611164929915.png)

## 2. Environment Preparation

Create a new project folder and open it in Cursor.

Next, get several key AI extensions ready:

1. Context7 MCP: queries the latest technical docs and API usage to keep AI from using outdated patterns
2. Firecrawl MCP: gives AI web-search capability so it can obtain the latest technical information
3. Frontend Design Skill: a frontend beautification skill pack that makes generated interfaces more polished

![](https://pic.yupi.icu/1/image-20260611155828400.png)

Once everything is ready, choose Claude Fable 5 and set it to High Thinking mode. Before executing, remember to review the prompt one more time—after all, one press of Enter here could cost well over a hundred yuan...

![](https://pic.yupi.icu/1/image-20260611155724141.png)

## 3. AI Autonomous Development

After execution, the AI started its autonomous loop.

It first read my local Claude Code config file, got the API Key and Base URL, and wrote them into the server-side `.env` file.

![](https://pic.yupi.icu/1/image-20260611155938897.png)

Then it started developing the server, desktop app, and admin backend in sequence.

I barely intervened during the entire process. The AI maintained `PROGRESS.md` by itself to track progress, automatically ran tests after finishing each module, and repaired errors on its own before continuing. It even opened the desktop APP and browser by itself to simulate user actions and do end-to-end validation.

![](https://pic.yupi.icu/1/image-20260611160046322.png)

The only downside was that it was a bit slow. I finished an entire meal and came back, and it was still working.

In the end, the AI spent nearly **50 minutes** independently completing the development and validation of the entire system without any intervention from me in the middle. That’s the power of Loop Engineering.

## 4. Demo Showcase

After development was complete, I asked the AI to help start the backend server, desktop app, and web admin page:

![](https://pic.yupi.icu/1/1781159120778-312597e0-112b-432a-9973-cc829fcbe013.png)

All three services came up. Let’s take a look at the result~

### APP Main Interface

When you open the desktop APP, there’s a big AI input box, and it automatically detects the current operating system. The overall style is lively and playful, and the slogan is actually not bad:

![](https://pic.yupi.icu/1/1781154426901-1d864350-c541-4d80-8b0b-f52265aeddb9.png)

### Built-In Popular Software

In the “Everyone’s Installing” section on the homepage, you can see a lot of mainstream environments and dependencies—many of them are things we often use while AI programming. See any familiar faces?

![](https://pic.yupi.icu/1/1781154509574-873c06ea-1b60-404e-8ead-77461d9da544.png)

### Version Selection + Installation Plan Generation

For example, if I want to install a MySQL database, after clicking in, I can see a list of version numbers and the operating system selector:

![](https://pic.yupi.icu/1/1781155910167-23be4d63-aaa5-4f92-92b5-2a90ebb3d105.png)

After making a selection and clicking “Generate Installation Plan,” the result appears instantly because a cached plan already exists. You can see that the AI generated a complete installation script, including Chinese comments, environment checks, installation steps, and verification commands. You can directly copy the script into the terminal and execute it:

![](https://pic.yupi.icu/1/1781155941607-2cdae4aa-c738-4f9d-976b-fe4572b6ecc5.png)

The AI also thoughtfully provides script explanations, including how to run it after installation and how to configure startup-on-boot:

![](https://pic.yupi.icu/1/1781155971044-5438c73f-7613-46b0-9f9a-11382ed1abab.png)

### One-Click Installation

Besides copying the script to install manually, you can also directly click the “One-Click Install” button, and the APP will pop up a terminal window to execute the script.

In my case, it detected that MySQL had already been installed, so it didn’t install it again:

![](https://pic.yupi.icu/1/1781156016550-50eee8c1-17bc-47a4-bfb7-a30c00e41d37.png)

Then I had it install PostgreSQL:

![](https://pic.yupi.icu/1/1781155852519-e4e36097-6e93-42cc-971f-a2b37a6c9e62.png)

Same process—and this time the new installation succeeded. The experience was actually really nice~

![](https://pic.yupi.icu/1/1781156068861-ccdfcd5f-2837-4fc8-b15c-6f005112cb23.png)

I then ran the `psql` command in the terminal to verify it, and sure enough, the database had been installed:

![](https://pic.yupi.icu/1/1781156128628-7e58c83d-bc6d-4923-b123-519127ba10fc.png)

### AI Recommendation Capability

This APP can do more than select existing software—it also has AI recommendation capability. Suppose I know nothing and simply type a problem I’m facing into the dialog box, like: I want a more convenient way to view PHP files.

![](https://pic.yupi.icu/1/1781158124727-14b31295-09c8-4282-a126-7d932675c63a.png)

The AI then recommends installing a PHP environment, and I can freely choose the version and operating system:

![](https://pic.yupi.icu/1/1781158148427-c70c8c7d-4085-4fb4-922f-14398cf96185.png)

Then the AI quickly generates the installation script:

![](https://pic.yupi.icu/1/1781158164398-ef99afc4-9868-4296-9258-02f753eef9f1.png)

After clicking one-click install and waiting for a while, it installs successfully too:

![](https://pic.yupi.icu/1/1781160624363-e90ae369-d72d-4c0a-ad32-fb616488b640.png)

### Web Admin Backend

Now let’s look at the web admin backend. After logging in with the default admin password, you can clearly see data statistics, including software installation rankings and version selection rankings:

![](https://pic.yupi.icu/1/1781161686984-f1473317-8173-4ed6-bee0-e3f373aff1d3.png)

You can also manage all generated software installation plans:

![](https://pic.yupi.icu/1/1781161721881-2af8af96-8cb8-4688-a9fa-e65060475868.png)

Click Edit to manually adjust problematic installation scripts, or let the AI regenerate them:

![](https://pic.yupi.icu/1/1781161740467-a89719ca-933a-4073-bf13-6370d1f20d39.png)

You can also view user feedback, such as which installation plans worked and which didn’t, making it easier to manually adjust and optimize invalid plans:

![](https://pic.yupi.icu/1/1781161764424-9529c563-b2d1-4cee-8700-cf5e7ddda345.png)

At this point, all the core features are working smoothly. The next time someone asks me how to install an environment, I can just throw this APP at them and call it a day. Solid or not?

## 5. Iteration and Optimization

Although the core features were working, did you notice any issues during use?

I found 2 problems:

1) The version-number information search capability wasn’t strong enough. For example, if I wanted to install Scala, the returned version list was wrong.

2) On Mac systems, the project relied too heavily on the package manager homebrew. But the versions available in homebrew aren’t always comprehensive. For example, Scala really does have version 3.4.2, but trying to install it through homebrew would fail.

![](https://pic.yupi.icu/1/1781160489542-c6aafe61-8aa7-4f35-8744-d775009ebe48.png)

So I gave the AI a repair instruction and asked it to autonomously fix these two issues and perform test validation.

```markdown
自主修复 2 个问题，并进行测试验证。
1）安装软件时，版本号列表获取错误。必须优化信息搜索能力，优先从官方信息源获取版本号列表和安装方式，如果没有官方信息源，才降级为通过联网搜索获取版本号信息，最后才是完全交给 AI 推断版本号。
2）Mac 系统默认使用 homebrew 来安装，但是 homebrew 的版本不一定全面，有时可能会安装失败，你需要优先通过官方获取安装方式，homebrew 作为一种备选方案，且要为 homebrew 安装失败时考虑降级方案。
```

About 20 minutes later, the AI finished the repair task.

For the version-number problem, it designed a four-level fallback chain:

![](https://pic.yupi.icu/1/1781160384730-8666f951-40c9-4d0c-ac1a-6cb5334002f3.png)

For the macOS installation problem, it rewrote the installation strategy:

![](https://pic.yupi.icu/1/1781160436753-3b383f87-5bd9-46eb-a866-fa9411e7f792.png)

After the fixes, I restarted the services and tested again by installing the Codex command-line tool. This time, the version numbers were correct and matched the versions on the official npm package:

![](https://pic.yupi.icu/1/1781161517802-901203e0-ecc1-4251-a691-15748dd066e2.png)

The installation script also became much more detailed: it now tries the official GitHub Release download first, and only falls back to homebrew afterward:

![](https://pic.yupi.icu/1/1781161497577-8ca853ea-c6d1-4b97-9d1a-d11bc5d61210.png)

Of course, there may still be a few edge cases not yet covered, but at the moment, the result is already more than usable enough. I can keep polishing it gradually in real use later.

## 6. Cost Summary

By now, everyone is probably very concerned about the cost, right?

Open the Cursor dashboard and let’s see how much money got burned this time:

![](https://pic.yupi.icu/1/1781161895686-954a36ff-0669-49c5-aca0-ac0a01e435e2.png)

The first full development pass cost 27 dollars (about 200 RMB), and the bug-fixing round cost 14 dollars (about 100 RMB), for a total of roughly 300 RMB.

What do you think—was it worth spending that much to produce a system like this?

Sure, it isn’t cheap. But from another angle, the AI produced 3 complete modules in one shot: the desktop APP, the server side, and the admin backend. After just two rounds of interaction, it already reached a usable state. If a human were to develop this manually, the workload would probably take around a month, right?

---

By the way, after finishing the project, I casually used GitHub MCP and had the AI open-source the whole project on GitHub for me. This kind of simple task doesn’t need Fable 5—any cheap model can handle it.

```markdown
帮我开源整个项目到 GitHub，注意忽略敏感信息的提交
```

![](https://pic.yupi.icu/1/image-20260611162129698.png)

The project has already been open-sourced. If you’re interested, you can pull the code down for secondary development—and while you’re at it, please give me a star~

![](https://pic.yupi.icu/1/image-20260611162417346.png)

## Final Thoughts

Looking back, why was Claude Fable 5 able to produce something usable in one go and reach a satisfying result after just two rounds of interaction?

Besides the fact that the model itself is indeed very strong, there are two other key factors:

1. The supporting **Harness Engineering** setup, including the MCP tools we prepared in advance, the frontend skill pack, the API Key configuration method, and Cursor’s built-in Browser Use browser-operation capabilities—these all helped build the scaffolding for the AI.
2. The project adopted the **Loop Engineering** mindset by designing an autonomous development loop inside the prompt, so the AI didn’t stop and wait for me, but instead kept running, validating, and repairing by itself.

Now I understand why both the father of Claude Code and the father of OpenClaw have been strongly backing Loop Engineering. This experience is genuinely awesome.

If you want to master the complete playbook of Loop Engineering in depth, you can read the "Loop Engineering Beginner-Friendly Tutorial" in the tips and tricks section of this course.

But having said that, if you just toss one or two casual prompts at the AI, there’s a good chance you’re simply wasting money. The stronger the model, the higher the requirements on prompt quality and engineering support. That’s also why after Claude Fable 5 came out, many students told me they felt they couldn’t really control the model yet—their AI programming experience and methods still weren’t strong enough.

At least for me, I’ve already run several projects with Claude Fable 5, and it honestly feels absurdly powerful. Its delivery certainty for long-horizon complex tasks is the best I’ve seen so far—just please don’t secretly downgrade it to Opus 4.8 on me (
