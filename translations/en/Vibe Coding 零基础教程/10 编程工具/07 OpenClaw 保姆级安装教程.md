# OpenClaw Beginner-Friendly Installation Tutorial

> OpenClaw installation + QQ chat integration, explained step by step



Hello, I’m Yupi.

In previous articles, we learned about various AI programming tools such as AI code editors, command-line programming tools, and IDE plugins. Those tools are all meant to help you write code and build projects. But there’s one category that’s more special—it’s not just a coding assistant, but an AI digital employee that can operate your computer.

Recently, “raising a lobster” has become especially popular—not a real lobster, but an AI assistant called OpenClaw.

![](https://pic.yupi.icu/1/openclaw%E7%8E%B0%E8%B1%A1.jpg)

You can think of it as an AI employee living inside your computer. Unlike ordinary AI chatbots that can only talk, this one can actually help you do things: reading and writing files, operating the browser, executing commands, and even building websites.

![](https://pic.yupi.icu/1/image-20260310160613289.png)

OpenClaw’s popularity far exceeded my expectations. Since its launch in November 2025, it took only about 120 days to become **the No.1 most-starred project in GitHub history**, reaching over 290,000 Stars and even surpassing giants like Linux and React!

![](https://pic.yupi.icu/1/image-20260310161116303.png)

I originally thought it was just a tech-circle toy, but it actually went mainstream.

In China, there are even in-home installation services charging several hundred yuan. You heard that right—**people will come to your house to install an open-source software package for a few hundred yuan**.

![](https://pic.yupi.icu/1/openclaw_setup_ondoor.jpeg)

Even more ridiculously, there was a free offline “install your lobster” event outside Tencent Tower in Shenzhen. Nearly a thousand people lined up, from fourth-grade elementary students to elderly uncles close to 70. The scene looked like seniors lining up for free eggs.

![](https://pic.yupi.icu/1/openclaw%E4%B8%8A%E9%97%A8%E5%AE%89%E8%A3%85%E6%9C%8D%E5%8A%A1.jpeg)

But personally, I feel that if something needs another person to operate your computer and install it for you, then you probably don’t really need that thing—and even if you install it, you probably won’t know how to use it.

In reality, installing OpenClaw on your own computer is very simple. Today, Yupi is bringing you a **super beginner-friendly OpenClaw local installation + QQ integration tutorial**. Even if you’ve never learned programming, as long as you follow along, you can successfully raise your own lobster 🦞~

Bookmark this and let’s begin.

⭐️ Recommended video tutorial: https://www.bilibili.com/video/BV1D4wcz6EVV

> Note: this article is mainly written for absolute beginners, so I won’t cover more advanced use cases. Yupi has previously shared [an OpenClaw cloud deployment tutorial](https://mp.weixin.qq.com/s/DZYc92rLzhX95L6OBEQUyQ), as well as [how to build an AI companion that can chat on mobile QQ with OpenClaw](https://mp.weixin.qq.com/s/GSwZE74o5-wq0_UOXL8AyA). If you’re interested, feel free to learn those later.



## Preparation Before You Start

Before installation, you only need two things:

1. 10 minutes of your time  
2. A computer that can turn on and access the internet (Windows is fine, Mac is even better. If possible, I recommend using a virtual machine, a spare device, or a cloud server—**safety really matters!!!**)

Other than that, you need nothing else.

**You don’t need to know programming, you don’t need any computer background, and you don’t even need to spend 1 cent!**



## Installation Tutorial Overview

The whole process has four steps:

1. Install the runtime environment  
2. Install and configure OpenClaw  
3. Connect QQ for chatting from your phone  
4. Uninstall

I know some people install OpenClaw and then realize they don’t know how to use it—or want to clean it out completely—so yes, Yupi even included the uninstall steps. Thoughtful enough, right?



## 1. Install the Runtime Environment

Open the [OpenClaw official website](https://openclaw.ai/), and you’ll see that the official team provides a one-line install command.

![](https://pic.yupi.icu/1/image-20260310161617619.png)

**If you’re on Mac or Linux**, you can directly open the terminal (press `Command + Space` and search for “Terminal”), paste the following command, and press Enter:

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

This command automatically installs all dependencies and OpenClaw itself in one shot. After that, you can jump directly to **Step 2 – Install and Configure OpenClaw**.

![](https://pic.yupi.icu/1/image-20260310161704012.png)

**But if you’re a Windows user, do not directly run the one-line install command! The failure rate is extremely high!!!**

Yupi personally tested multiple installation methods and stepped on a lot of landmines. Below I’ll walk you through the most stable installation method for Windows, step by step.



### 1. Install Node.js

First, we need to install Node.js.

What is Node.js?

You can think of it as OpenClaw’s **engine**. OpenClaw is written in JavaScript, and Node.js is the runtime environment that lets JavaScript run on your computer. Without it, OpenClaw can’t start.

Open the [Node.js official site](https://nodejs.org/), download the installer that matches your operating system, and pay attention to the version number: **choose version 22 or above**. Below that, your lobster-catching mission may fail.

![](https://pic.yupi.icu/1/image-20260310144506886.png)

After the download finishes, run the installer. You don’t need to change anything—just keep clicking Next:

![](https://pic.yupi.icu/1/image-20260310144530251.png)

Once Node.js is installed successfully, it also installs a tool called npm. You can think of npm as Node.js’s app store. We’ll use it later to install OpenClaw.



### 2. Install Git

Next, install Git.

Git is a code version management tool. OpenClaw needs it during installation to download some dependency packages from the internet.

You do **not** need to learn how to use Git right now. You only need to install it.

Open the [Git official site](https://git-scm.com/downloads/win) and download the Windows installer:

![](https://pic.yupi.icu/1/image-20260310144749069.png)

Again, run the installer and keep all options at their default values while clicking Next:

![](https://pic.yupi.icu/1/image-20260310144843659.png)



### 3. Install OpenClaw

Now that the environment is ready, let’s install OpenClaw itself.

First, open PowerShell as administrator. PowerShell is the command-line tool built into Windows—the equivalent of the terminal on Mac/Linux.

Type “PowerShell” into the Windows search bar, right-click it, and choose **Run as administrator**:

![](https://pic.yupi.icu/1/image-20260310144953360.png)

First try the official one-click installation command:

```bash
iwr -useb https://openclaw.ai/install.ps1 | iex
```

There’s a high chance, just like Yupi, that you’ll immediately get an error saying you lack permission to run scripts:

![](https://pic.yupi.icu/1/image-20260310145038140.png)

No problem. Run the following command to enable PowerShell script execution:

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

If a confirmation prompt appears, type `A` and press Enter. This command allows scripts from trusted sources to run—similar to allowing installation of third-party apps on a phone.

![](https://pic.yupi.icu/1/image-20260310145148127.png)

Then run the one-click installation command again. If you’re lucky, it may succeed directly. But if you’re unlucky like me, it may fail again during installation!

![](https://pic.yupi.icu/1/image-20260310145208509.png)

The error message indicates that npm installation failed, so let’s try installing it manually with npm:

```bash
npm install -g openclaw
```

![](https://pic.yupi.icu/1/image-20260310145316319.png)

As expected, it also failed, because the one-click script uses npm under the hood anyway, so the root cause is the same.

![](https://pic.yupi.icu/1/image-20260310145349762.png)

Don’t panic. In fact, you just need to switch package managers and use pnpm instead.

pnpm is similar to npm—it’s also an app store / package manager—but it has better compatibility and faster installation speed.

First use npm to install pnpm globally:

```bash
npm install -g pnpm
```

After installation, check pnpm’s version to confirm it was installed successfully:

```bash
pnpm -v
```

![](https://pic.yupi.icu/1/image-20260310145555384.png)

Then run `pnpm setup`. This command automatically configures pnpm’s global install path so that tools installed by pnpm can be used from anywhere:

![](https://pic.yupi.icu/1/image-20260310145624520.png)

Important! After running `pnpm setup`, **you must close the current PowerShell window and reopen a new PowerShell window as administrator**. This is so the environment variables you just configured can take effect.

In the new PowerShell window, use pnpm to install OpenClaw:

```powershell
pnpm add -g openclaw@latest
```

![](https://pic.yupi.icu/1/image-20260310145706609.png)

Wait a little while, and the installation will succeed! But you may see a message saying that some build scripts were ignored:

![](https://pic.yupi.icu/1/image-20260310145800342.png)

That’s because pnpm, for security reasons, does not automatically execute third-party package build scripts by default. You need to manually approve them.

According to OpenClaw’s official instructions, you should run this command to approve those build scripts:

```bash
pnpm approve-builds -g
```

![](https://pic.yupi.icu/1/image-20260310145842863.png)

However, this command may fail:

![](https://pic.yupi.icu/1/image-20260310145930863.png)

Yupi searched all over the internet for a solution and still couldn’t fix this issue, so hopefully the official team will patch it later. The good news is that **not running this command usually does not affect normal usage much**, so you can simply ignore it.

Finally, verify whether OpenClaw was installed successfully by running:

```bash
openclaw -v
```

If you can see the version number, then congratulations—you’re done!

![](https://pic.yupi.icu/1/image-20260310143618461.png)



## 2. Install and Configure OpenClaw

Now that the environment is ready, let’s enter OpenClaw’s onboarding flow and customize your little lobster 🦞.

Run the following command in PowerShell (Windows) or the terminal (Mac/Linux):

```bash
openclaw onboard --install-daemon
```

`onboard` means the guided onboarding flow, and `--install-daemon` means “install the background service while you’re at it,” so OpenClaw can continue running in the background even if you close the terminal.

After executing it, you’ll enter an interactive wizard that walks you through the setup step by step.

![](https://pic.yupi.icu/1/image-20260310150045929.png)

The first thing it shows is a user agreement that you need to confirm.

![](https://pic.yupi.icu/1/image-20260310150214119.png)

One reminder here: OpenClaw is an AI tool that can operate your computer, so in theory it can execute any terminal command, including sensitive ones like deleting files. **So if possible, I strongly recommend playing with it inside a virtual machine or on a spare device** to avoid accidental damage to important data.

If you’re okay with that, choose Yes and move to the next step.



### 1. Choose the Installation Mode

The wizard will ask whether you want Quickstart or Manual mode.

For beginners, I recommend choosing Quickstart directly. It uses default configurations to get you going fast. Manual mode is better suited for people who already have some lobster-raising experience.

![](https://pic.yupi.icu/1/image-20260310150255760.png)



### 2. Configure the AI Model

This is the most important step. You need to tell OpenClaw which AI model to use for thinking—in other words, you’re choosing your lobster’s brain.

The wizard will list several AI platforms for you to choose from, such as Anthropic (Claude), OpenAI (GPT), Qwen, and so on.

Yupi recommends that beginners choose Qwen, because it supports OAuth login. A webpage pops up automatically for you to scan and authorize, so you don’t need to manually apply for and fill in an API Key, and you can start using it for free. The downside is that heavy usage may hit rate limits, so it’s best suited for getting started quickly.

![](https://pic.yupi.icu/1/image-20260310150423382.png)

After selecting Qwen, the wizard will automatically open your browser for login authorization:

![](https://pic.yupi.icu/1/image-20260310150610423.png)

After logging in and authorizing successfully, choose the default coding model:

![](https://pic.yupi.icu/1/image-20260310150731894.png)

Of course, you can also choose other model platforms. If you want to understand how different models perform in OpenClaw scenarios, check out the [PinchBench](https://pinchbench.com/) ranking, a benchmark site specifically designed to test models on OpenClaw-style tasks. At the moment, Claude Opus 4.8 has the highest success rate (82.5%), while the cheapest is Google’s `gemini-2.5-flash-lite`, costing only about 0.1 yuan per task.

![](https://pic.yupi.icu/1/image-20260310164932093.png)

I don’t really recommend that beginners jump straight into foreign models for OpenClaw. They’re very expensive, especially when you let AI perform complex work—the token burn can get brutal. Domestic models like Zhipu and Kimi are also solid choices.



### 3. Configure Chat Channels

The wizard will ask whether you want to connect Telegram, WhatsApp, Discord, Feishu, and other chat platforms, so it’s easier to talk to your lobster.

I recommend skipping this for now. Let’s first use the web interface for chatting. Manually connecting QQ afterward is actually more convenient for us.

![](https://pic.yupi.icu/1/image-20260310150813561.png)

Next it will also ask whether you want to configure a search service provider (such as Brave Search). I also recommend skipping that for now, because those options all require applying for additional API Keys. You can set them up later if needed.

![](https://pic.yupi.icu/1/image-20260310150917416.png)



### 4. Install Skills

Skills are capability expansion packs for AI. OpenClaw itself is just a framework. After installing Skills, AI can unlock concrete abilities such as web search, browser control, PPT creation, and more.

First, enable skill configuration:

![](https://pic.yupi.icu/1/image-20260310150959049.png)

Then the wizard will show you some recommended skill packs. Here I suggest adding at least **ClawHub**. ClawHub is OpenClaw’s official skill marketplace. Once installed, your little lobster can search and install thousands of community skill packs at any time, making it very easy to expand its capabilities. The other skills can be chosen as needed.

![](https://pic.yupi.icu/1/image-20260310151036714.png)

After choosing the skills, you also need to choose which tool to use for installing them. Just pick npm:

![](https://pic.yupi.icu/1/image-20260310151118779.png)

After that, the wizard may ask some extra service configuration questions, such as whether to configure AI image-generation models. If you’re a beginner, just mindlessly choose No for all of them:

![](https://pic.yupi.icu/1/image-20260310151157689.png)



### 5. Start the Gateway Service

Next, OpenClaw will automatically install and start its Gateway service. You can think of the gateway as OpenClaw’s central dispatcher. It receives messages from different channels (web, QQ, Feishu, etc.), sends them to the AI for processing, and then returns the results to you.

![](https://pic.yupi.icu/1/image-20260310151301625.png)

At this point, Windows may pop up a firewall prompt asking whether to allow access on public and private networks. **Be sure to click Allow!** Otherwise, the gateway service won’t work correctly.

![](https://pic.yupi.icu/1/image-20260310151324961.png)

After it starts successfully, the wizard will ask whether you want to use OpenClaw in the terminal interface (TUI) or the web browser.

TUI means chatting with AI directly in the command line, which suits people who like typing commands and already have some programming background. Beginners should of course choose the Web UI:

![](https://pic.yupi.icu/1/image-20260310151428919.png)



### Start Using It

After you choose, the browser automatically opens the OpenClaw web control panel. Congratulations—your Lobster No.1 is ready!

Say hello to it first and ask who it is. It will also proactively guide you through setting up things like identity and responsibilities through conversation:

![](https://pic.yupi.icu/1/image-20260310151625528.png)

OpenClaw comes with many built-in tools, such as file read/write, terminal command execution, and web search.

Try asking it to read files from your computer—for example, to see what’s in your Downloads folder:

![](https://pic.yupi.icu/1/image-20260310151946903.png)

That said, having to open the web control panel on your computer every time you want to chat with AI still isn’t convenient enough. So next, we’re going to connect OpenClaw to a QQ bot, with the goal of raising your lobster from your phone anytime, anywhere~



## 3. Connect QQ for Mobile Chat

In the past, connecting OpenClaw to QQ required applying on the QQ bot open platform yourself, getting whitelisted, and obtaining credentials. It was a bit troublesome.

Now Tencent has stepped in and created a fast-track integration route specifically for OpenClaw, so you can get it done in just a few steps!

Open the [QQ Bot OpenClaw integration page](https://q.qq.com/qqbot/openclaw/index.html) and log in by scanning with QQ:

> Link: https://q.qq.com/qqbot/openclaw/index.html

![](https://pic.yupi.icu/1/image-20260310152123827.png)

Click “Create Bot,” and it’s created instantly!

![](https://pic.yupi.icu/1/image-20260310152325274.png)

As soon as creation is complete, your mobile QQ will immediately receive a greeting message from your little lobster:

![](https://pic.yupi.icu/1/image-20260310153005879.png)

Then you can modify the bot’s avatar, nickname, and other information. Give your lobster a nice name~

![](https://pic.yupi.icu/1/image-20260310152409339.png)

Next comes the most important step. The page will display three configuration commands. You only need to **copy these 3 commands into the terminal (PowerShell) and execute them one by one**.

Be careful: the commands contain your secret credentials, so do not share them with anyone!

![](https://pic.yupi.icu/1/image-20260310152443829.png)

Execute the commands in the terminal one by one:

![](https://pic.yupi.icu/1/image-20260310152544861.png)

After successful integration, you can see the QQ bot channel inside the “Channels” section of the OpenClaw web console:

![](https://pic.yupi.icu/1/image-20260310152846134.png)

Now take out your phone and try it!

Send tasks directly to your little lobster in QQ—for example, ask it to check your computer specs or help you write an article. It completes tasks quite quickly, and it also supports Markdown output, which gives a pretty good reading experience:

![](https://pic.yupi.icu/1/image-20260310153115908.png)

If you’re curious what it was doing behind the scenes, you can inspect the full conversation history with the QQ bot in OpenClaw’s web console. After connecting the QQ bot channel, OpenClaw also knows how to send images, voice messages, and other QQ content:

![](https://pic.yupi.icu/1/image-20260310152754120.png)

Besides basic chatting and computer operation, you can explore more advanced uses too. For example, see Yupi’s earlier article [GLM-5 + OpenClaw: Build Your AI Companion](https://mp.weixin.qq.com/s/GSwZE74o5-wq0_UOXL8AyA), which teaches you how to create an AI companion that can send images, send voice messages, and even help you work. You can also read [OpenClaw Beginner-Friendly Deployment Tutorial](https://mp.weixin.qq.com/s/DZYc92rLzhX95L6OBEQUyQ) to deploy OpenClaw on a cloud server for 24/7 operation.

Of course, I suspect many people will tinker with it for a while and then feel discouraged:

**What do I even need this lobster for?!**

Exactly. You may not need OpenClaw at all.

So next, caretaker Yupi will also teach everyone how to uninstall OpenClaw and delete it completely—leaving not even a trace of shrimp shell behind.



## 4. Uninstall

Actually, it only takes one line to uninstall OpenClaw:

```bash
openclaw uninstall
```

But do pay attention to the output after running the command, because some things may not be deleted automatically:

![](https://pic.yupi.icu/1/image-20260307105935932.png)

If you want to make absolutely sure everything is removed cleanly, just copy and run all the commands below for your operating system in one shot.

For Mac / Linux users:

```bash
openclaw gateway stop
openclaw gateway uninstall
rm -rf "${OPENCLAW_STATE_DIR:-$HOME/.openclaw}"
npm rm -g openclaw || pnpm remove -g openclaw
rm -rf /Applications/OpenClaw.app
```

For Windows users (run in PowerShell):

```powershell
openclaw gateway stop
openclaw gateway uninstall
schtasks /Delete /F /TN "OpenClaw Gateway"
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw"
Remove-Item -Force "$env:USERPROFILE\.openclaw\gateway.cmd" -ErrorAction SilentlyContinue
npm rm -g openclaw
# 如果你是用 pnpm 安装的，改为执行：pnpm remove -g openclaw
```

After this combo finishes, it’ll be as if nothing ever happened.



## Final Words

OpenClaw really is a cool project. It turns the entry point for using an AI agent into the everyday mobile chat software you already use, letting AI seamlessly blend into your existing communication habits. Right now, every company is trying to seize the AI entry point and get closer to users.

But even though OpenClaw is great, it still has to be used in the right place.

I’ve seen many people hyping “remote AI office control from your phone,” but honestly, how many people truly need that?

When you relax and pick up your phone, do you really want to command AI to work—or do you just want to watch videos and check your social feed?

If you only install it to try something trendy, the most likely ending is that it collects dust and eventually gets uninstalled.

And if you’re already working in front of your computer, your automation needs can often be handled much more simply and directly by AI programming tools like Claude Code / Cursor or AI desktop assistants. They’re easier than OpenClaw, don’t require you to tinker with the environment or configure API Keys yourself, and are ready to use out of the box. **Instead of chasing trends by installing a tool you don’t actually need, it’s better to think about how to use AI to strengthen your own workflow.** The real path is to find the AI tools that truly improve your efficiency and keep using them consistently.

I think OpenClaw is better suited for workplace business users who want to improve productivity, or for technical enthusiasts who enjoy tinkering and want to deeply customize AI behavior. Not everyone can raise a lobster better than the polished versions packaged by big-company professional teams. And very soon, every company will roll out its own OpenClaw—well, actually, that has already started.

Of course, I’ll keep following OpenClaw’s development and exploring more ways to use it productively.

At this point, we’ve finished learning all the major types of mainstream AI programming tools. In the next article, I’ll introduce AI auxiliary tools, including version management, project deployment, and more, to help you complete your development toolchain.

Keep going!



## Recommended Resources

1) Yupi AI Navigation site: [complete AI resources, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning community: [learning roadmaps, programming tutorials, hands-on projects, job hunting guides, discussion and Q&A](https://www.codefather.cn)

3) Programmer interview cheat sheets: [high-frequency interview points for internships, campus hiring, and experienced hires, plus real company question analysis](https://www.mianshiya.com)

4) Resume-writing tool for programmers: [professional templates, rich example sentences, and direct paths to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [essential for landing offers in internships, campus hiring, and experienced-hire interviews](https://ai.mianshiya.com)
