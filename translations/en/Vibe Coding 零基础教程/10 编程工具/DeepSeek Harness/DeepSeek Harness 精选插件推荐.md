# DeepSeek Harness Selected Plugin Recommendations

> A one-stop showcase of popular DSH community plugins, from practical tools to pure meme magic.

Hello everyone, I’m Yupi.

DeepSeek Harness is DeepSeek’s latest open-source AI Agent runtime environment, abbreviated as DSH.

You can think of it as a highly customizable AI coding tool, comparable to Claude Code and Codex, built around one core idea: **everything is a plugin**.

![](https://pic.yupi.icu/1/image-20260814133452050-20260819135304416.png)

The entire DSH architecture is built on a meta-framework called Cordis. Model adapters, tool registries, session logs, the Agent loop, and even the web UI itself are all hot-swappable plugins. If you want to change the model, change the tools, or change the interaction mode, you just tweak the configuration—no need to touch the source code.

Although DSH’s built-in capabilities still aren’t especially rich, this fully plugin-based design is exactly why the community has been filling in missing capabilities at lightning speed. In just a little over a week, the `dsh-plugin` tag on GitHub has already spawned thousands of community plugins—some expand the Agent’s abilities, some improve the UI, and some are just bizarre abstract art projects…

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

In this article, I’m going to walk everyone through a big wave of popular DeepSeek Harness plugins—some practical, some beautiful.

![](https://pic.yupi.icu/chengfang/02.png)

Hand-picked by Yupi, and there’s plenty to go around. I recommend bookmarking this so you can make your whale even stronger!



## Discovering High-Quality DSH Plugins

So first of all, where do you even find good DeepSeek Harness plugins?

The most direct way is to check GitHub’s [dsh-plugin topic page](https://github.com/topics/dsh-plugin). After publishing a plugin, many developers tag their repositories with `dsh-plugin`, so you can see most newly released plugins there.

The advantage of this approach is speed and quantity. The downside is that quality varies a lot, because anyone can add that tag to a repository. It doesn’t mean the plugin has been reviewed, and there’s no reliable quality-based sorting.

![](https://pic.yupi.icu/chengfang/03DSH.png)

If you don’t want to browse repositories one by one, you can check out [Awesome DSH Plugin](https://awesome-dsh-plugin.com/zh/). It’s a community-curated list of quality plugins, categorized by use case, which makes it easier to quickly discover popular options. But it’s still community-maintained, so it’s good for discovering plugins and checking popularity—not something you should treat as an official recommendation.

![](https://pic.yupi.icu/chengfang/004DSH.png)

Interestingly, once there were enough DSH plugins, even the act of **finding plugins** became a plugin itself.

For example, the `dsh-market` plugin that I’ll mention later effectively adds a plugin marketplace directly into DeepSeek Harness.

There, you can not only browse and search plugins directly, but also get related recommendations based on the plugins you already have installed.

For instance, I don’t need to know in advance that a plugin is called `dsh-pocket`. I can simply search for the word “remote,” and the `dsh-market` plugin will match the corresponding project for me.

![](https://pic.yupi.icu/chengfang/007DSH.png)

So how do you install plugins?

Honestly, I usually don’t bother messing with commands myself. I just give the GitHub repository URL to DeepSeek Harness and let AI read the repo’s `README`, figure out the installation method, and run the install commands itself. After it’s done, I just restart `dsh web` as instructed by the AI.

![](https://pic.yupi.icu/1/image-20260814145412556.png)



## Recommended High-Quality DSH Plugins

Now we’re officially entering the recommendations section. I grouped the plugins I tested this time into three categories: plugins that expand DSH’s capabilities, plugins that improve the panel experience, and pure community meme creations.

Let’s start with the first category: plugins that directly give DSH new abilities.



### DSH Capability Extensions



#### ModLens Gives DeepSeek Eyes for Images

This is personally the plugin I’m most optimistic about. It gives an AI model that originally could only read text a pair of sharp eyes.

> Open-source repo: https://github.com/liustack/modlens

![](https://pic.yupi.icu/chengfang/033DSH1.png)

The DeepSeek V4 series models can only process plain text. Although DeepSeek’s official app has already rolled out image understanding in limited release, DSH uses the API interface. So if you directly paste a screenshot into the conversation, the AI won’t understand it at all.

ModLens solves exactly that problem. After you paste an image, the plugin automatically forwards it to an external vision model (such as Qwen). The vision model parses the image into structured JSON information, including OCR-recognized text, page layout regions, and semantic content inside the image. That information is then fed back to DeepSeek as context, allowing it to keep reasoning based on the image content.

![](https://pic.yupi.icu/chengfang/027DSH.png)

Unlike ordinary OCR tools, ModLens preserves not just text but also position relationships and semantics between elements. So for people who often use AI for frontend work, it’s extremely practical. After finishing a page, you can just throw a screenshot into DSH and let it check the visual fidelity by itself.



#### ModSearch Expands Search Sources

ModSearch is a search enhancement plugin that lets DSH connect to different search providers such as Firecrawl, Tavily, and Exa, and it can also continue expanding into Twitter search.

> Open-source repo: https://github.com/liustack/modsearch

![](https://pic.yupi.icu/chengfang/034DSH1.png)

Although DSH already has built-in web search, its search scope is limited.

For example, I asked AI to search for discussions about DeepSeek Harness on Twitter from that very day, and the AI explicitly told me that the current search tool couldn’t access real-time original Twitter posts. It could only find secondhand references from media and community articles.

![](https://pic.yupi.icu/chengfang/23DSH.png)

After installing ModSearch, I deliberately left the API Key unconfigured and asked AI to search for the same question again. This time it directly found an original Twitter post, and I could verify it by clicking the link.

![](https://pic.yupi.icu/chengfang/25DSH.png)

That said, Twitter search still didn’t work fully end to end at this stage. More complete search capabilities still require configuring the corresponding service API Keys. If you regularly need deep research across the whole web, it’s definitely worth setting up.



#### dsh-browser Lets DSH Operate the Browser

dsh-browser allows DSH to directly operate the Chrome browser you’re currently using—for example, reading webpage content, clicking links, filling forms, navigating pages, and so on.

> Open-source repo: https://github.com/Lum1104/dsh-browser

![](https://pic.yupi.icu/chengfang/035DSH.png)

Unlike typical headless-browser solutions, `dsh-browser` connects to real Chrome tabs on your own computer. Cookies, sessions, and login states inside the browser can all be reused directly, so AI doesn’t need to log in separately again.

Its technical solution consists of a DSH bridge plugin plus a Chrome MV3 extension, with both sides communicating over a local WebSocket. The plugin converts webpage content into structured text descriptions (including a numbered list of interactive elements) and sends that to DeepSeek. DeepSeek doesn’t need to “see screenshots” to understand page structure and perform operations.

Installing this plugin is a little more complicated. Besides installing the `dsh-browser` plugin itself, you also need to load a local extension in Chrome.

![](https://pic.yupi.icu/chengfang/010DSH.png)

I simply let DSH follow the plugin’s `README` and install everything automatically. AI built the source code, dependencies, and extension. In the end, I only had to manually load the local extension directory from Chrome’s `chrome://extensions` page.

![](https://pic.yupi.icu/chengfang/26DSH.png)

Once the extension is open, seeing `Connected` means the connection succeeded.

![](https://pic.yupi.icu/chengfang/28DSH.png)

I first ran a test using GitHub. I gave it my open-source project homepage and asked it to find the pinned repository on the page, then click into it and continue reading the details.

From reading the page, locating the repository, clicking into it, and reading the project information, the whole workflow worked end to end.

![](https://pic.yupi.icu/chengfang/821DSH.png)

Next, I asked AI to search for DSH-related content through the Twitter page. It actually typed keywords into the Twitter search box automatically, ran the search, and then switched to the latest results to inspect newly posted tweets.

![](https://pic.yupi.icu/chengfang/012DSH.png)

This is positioned differently from ModSearch. ModSearch is better for searching information via search-engine channels, while `dsh-browser` lets AI directly operate real websites where you’re already logged in. It’s better for things like filling forms, posting content, or checking admin dashboards that require a logged-in state.

That said, `dsh-browser` doesn’t let the Agent do absolutely anything without restriction. Actions like clicking, typing, and page navigation will, by default, pop up a confirmation box for your review. If you manually switch tabs, it will also pause and ask whether it should keep controlling the original page or follow the current one.

There’s also one small usability detail worth noting. By default, `dsh-browser` binds to the currently active tab. If you ask it to open GitHub directly from the DSH page, the chat page itself may get navigated away. Later I changed my workflow to first open the target site’s tab, then start the conversation from the Chrome sidebar, which felt much smoother.

![](https://pic.yupi.icu/chengfang/062DSH.png)



#### Agent Teams Builds an Agent Team

Agent Teams is a multi-Agent collaboration plugin that allows DSH to launch multiple Agents at once, each doing its own work, while all results are summarized into a single Captain node.

> Open-source repo: https://github.com/NanmiCoder/dsh-agent-teams

![](https://pic.yupi.icu/chengfang/036DSH.png)

The Captain is responsible for breaking down the task, assigning work, and producing the final summary. The member Agents underneath each handle different directions of the problem.

I used it to inspect a frontend project and created three members responsible for different dimensions:

```
前端 Agent：检查页面结构、交互逻辑、响应式和明显的前端问题
代码质量 Agent：检查项目结构、依赖管理和代码可维护性
安全 Agent：检查敏感信息泄露、依赖风险和明显的安全隐患
```

Once the task started running, the activity panel on the right directly showed all three Agents working at the same time. After each one finished its own inspection, the results were routed back to the Captain, who then summarized everything into a final report.

![](https://pic.yupi.icu/chengfang/14DSH.png)

**What’s even better is that this Agent team doesn’t disappear immediately after finishing one task—it can be reused later.**

![](https://pic.yupi.icu/chengfang/013DSH.png)

After that inspection round, I followed up with a question about a WebGL fallback issue and specifically asked only the frontend member to handle it. Sure enough, only that member re-entered working state in the activity panel, while the other two were not scheduled again.

![](https://pic.yupi.icu/chengfang/014DSH.png)

So it’s different from temporarily opening multiple Agents. The created team and its members remain in place and can be assigned tasks later as needed.

For tasks like code review or multi-dimensional research that can be split into different directions, Agent Teams is a good fit. But if the task itself is simple, there’s no need to assemble a whole squad—it just adds scheduling time and token cost.



### Practical DSH Tools and UI Enhancements

Next is the second category. These plugins mainly improve the DSH panel and everyday usability, making it much smoother to use.



#### dsh-market Adds a Plugin Marketplace to DSH

As mentioned earlier, once DSH plugins became numerous enough, browsing GitHub manually to find plugins started getting pretty annoying.

dsh-market is basically a built-in plugin marketplace inside DSH. You can browse, search, and install plugins without leaving DSH, and it even recommends related projects based on what you already have installed.

> Open-source repo: https://github.com/2BingLing/dsh-market

![](https://pic.yupi.icu/chengfang/050DSH.png)

There are two particularly useful features. The first is personalized recommendations. The plugin knows what you’ve already installed, so its recommendations gradually get more relevant, and you don’t need to keep searching for new plugins manually every time.

![](https://pic.yupi.icu/chengfang/35DSH.png)

The second is keyword-based plugin search. For example, if I want a plugin that lets me remotely control DSH from my phone, I can just search for “remote” and it will match related projects. I don’t need to remember plugin names in advance.

![](https://pic.yupi.icu/chengfang/007DSH.png)



#### dsh-web-ui Enhances Website Features

dsh-web-ui is a web enhancement plugin that integrates a task board, Git management, a workspace, status information, skin themes, desktop pets, and a whole bunch of other features. After installing it, the entire page feels much more like a complete development tool.

> Open-source repo: https://github.com/zhu1090093659/dsh-web-ui

![](https://pic.yupi.icu/chengfang/038DSH1.png)

At first, when I saw the name, I assumed it was just some light UI restyling. But after installing it, I realized this thing is basically a super all-in-one package.

![](https://pic.yupi.icu/chengfang/016DSH.png)

The first feature I tried was the task board. You can create tasks directly and clearly describe what you want the Agent to do. Progress from start to finish is shown on the board, and you can even click in to find the actual DSH session executing that task.

![](https://pic.yupi.icu/chengfang/06DSH.png)

It also does Git-related features very thoroughly. You can directly search, switch, and create branches, and it can visualize previous commit history into a Git graph that clearly shows the relationship between commits and branches.

![](https://pic.yupi.icu/chengfang/08DSH.png)

I installed the all-in-one version of `dsh-web-ui`, which also installs `dsh-better-sidebar`, so the right side gains a full VS Code–like developer toolbar.

![](https://pic.yupi.icu/chengfang/017DSH.png)

Inside that bundled better-sidebar, the file list even includes an `@file` button, so you can directly reference needed files into the current conversation instead of manually copying paths yourself.

![](https://pic.yupi.icu/chengfang/019DSH.png)

Pretty strong plugin, right? It feels like it implemented a lot of features the official product hasn’t built yet.



#### DSH-better-sidebar Strengthens the Sidebar

DSH-better-sidebar is a sidebar enhancement plugin that gathers common development panels like the file tree, terminal, and Git status into the right side of DSH, reducing the annoyance of constantly switching windows.

> Open-source repo: https://github.com/omdsh-dev/DSH-better-sidebar

![](https://pic.yupi.icu/chengfang/039DSH.png)

Compared with the earlier `dsh-web-ui`, it doesn’t include extra features like the task board, skin center, or desktop pet. It’s more focused on the sidebar itself, and the interface is also cleaner.

![](https://pic.yupi.icu/chengfang/018DSH.png)

If you feel the all-in-one package includes too many features you won’t use, you can just install this one by itself for a lighter setup.



#### dsh-context Enhances Context Visibility

dsh-context is a context visualization plugin that lets you directly inspect the composition, usage ratio, and change history of the current session context.

> Open-source repo: https://github.com/bowenliang123/dsh-context

![](https://pic.yupi.icu/chengfang/040DSH.png)

When you’ve been chatting with AI for coding for a long time, conversations often get slower and the context grows larger and larger. But in normal use, it’s hard to see at a glance whether history messages, file contents, or tool-call results are taking up most of the space.

`dsh-context` exposes that hidden data directly. Click the context button, and you’ll see a health report for the current context, making it obvious how many tokens each type of information is occupying.

![](https://pic.yupi.icu/chengfang/38DSH.png)

If you often run long sessions or call tools frequently, this is very useful. At the very least, when the context is about to fill up, you’ll know what to clean up instead of blindly starting a new session.



#### dsh-TUI Terminal UI

dsh-TUI is a terminal interaction plugin suitable for users who are more comfortable with a Claude Code–style terminal workflow.

> Open-source repo: https://github.com/ccch1mneyyy/dsh-TUI

![](https://pic.yupi.icu/chengfang/041DSH.png)

After installation and launch, it goes directly into a fullscreen terminal UI. At the bottom, it displays information like the current model, reasoning intensity, and context usage percentage in real time—simple and brutal.

![](https://pic.yupi.icu/chengfang/020DSH.png)

That said, I don’t recommend beginners install this right away, because `dsh-TUI` makes relatively large changes to DSH’s interface and interaction patterns, while the official DSH product itself is still evolving rapidly. If new capabilities or interface changes appear later, this plugin may not keep up immediately, and troubleshooting compatibility issues could become a headache.



#### dsh-genui UI Rendering

dsh-genui is a generative UI plugin that allows DSH responses to go beyond plain text and Markdown by directly rendering cards, charts, option buttons, and other interactive interfaces inside the conversation.

> Open-source repo: https://github.com/omdsh-dev/dsh-genui

![](https://pic.yupi.icu/chengfang/042DSH.png)

I opened a new conversation and asked it to generate an “AI coding tool comparison dashboard” containing info cards and a bar chart. It really rendered them directly inside DSH’s chat window, and they were genuinely interactive components.

![](https://pic.yupi.icu/chengfang/37DSH.png)

If you often ask AI to present data or compare plans and feel that plain-text answers are too dull, this plugin is worth trying.



#### dsh-pocket Remote Control from Phone

dsh-pocket lets you connect the DSH currently running on your computer to your phone. Just scan a QR code and you can continue viewing the Agent’s status and sending messages from your phone browser.

> Open-source repo: https://github.com/shaobeichen/dsh-pocket

![](https://pic.yupi.icu/chengfang/043DSH.png)

This plugin supports both LAN mode and public-network mode, and I tested both.

LAN mode is very simple. Just connect your phone and computer to the same Wi-Fi, scan the QR code, and the DSH interface opens directly.

![](https://pic.yupi.icu/chengfang/021DSH.png)

Public-network mode is more universal. Your phone doesn’t need to be on the same network as your computer, so you can access it anytime, anywhere. The first time you open it, it asks for an access password. Every time you restart public-network access, the password changes automatically.

![](https://pic.yupi.icu/chengfang/044DSH.png)

Most importantly, public access does **not** require you to buy a separate server! `dsh-pocket` uses Cloudflare Quick Tunnel to create a temporary public tunnel that forwards external requests to the DSH running locally on your computer. Streaming output between the phone and computer is transparently relayed via WebSocket, so if the computer is outputting something, the phone can see it scrolling in real time too.

That means in the future, if DSH is running a long task on your computer, you can still pull out your phone while you’re out eating and keep checking progress or sending messages.

But convenience comes with security responsibilities. Don’t casually share the remote QR code, public URL, or access password with others. After all, DSH can operate local files and code on your machine, so the consequences of exposure are obvious…



### DSH Meme Gameplay

The first two categories were at least seriously trying to add capabilities or improve the experience.

From here on out, the plugin scene starts to go gloriously off the rails…

![](https://pic.yupi.icu/1/e02764373d3605e8c6b758e546b52410500385529.jpg)



#### dsh-deep-whale Whale Girl Skin

deep-whale is a theme plugin. After installation, the whole web UI switches directly into a whale-girl style.

> Open-source repo: https://github.com/Small-tailqwq/dsh-deep-whale

![](https://pic.yupi.icu/chengfang/045DSH1.png)

Just look at the effect after installing it:

![](https://pic.yupi.icu/1/image-20260814133452050.png)

Looks nice, right? Doesn’t it suddenly make you more motivated to open DSH?

Although it doesn’t add any new functionality, I have to admit that this kind of thing is perfect for community spread. Who sees that screenshot and *doesn’t* want to install it?



#### whale-girl A More Interactive Desktop Pet

whale-girl is a desktop pet plugin that lets you raise an adorable whale-girl pet directly inside DSH.

> Open-source repo: https://github.com/vlln/whale-girl

![](https://pic.yupi.icu/chengfang/046DSH.png)

The earlier `dsh-web-ui` plugin also includes desktop pet functionality, but after comparing them in practice, the experience is quite different.

The pet built into `dsh-web-ui` feels more like a “work status indicator.” When the Agent is working, it tells you things like it’s organizing materials or that the task is complete.

`whale-girl`, on the other hand, feels more like the old QQ Pet. Hovering over it shows the level and current status, and opening the menu lets you feed it and play with it.

![](https://pic.yupi.icu/chengfang/41DSH.png)

It also changes its actions based on the Agent’s work state—for example, tilting its head while thinking, yawning while waiting, cheering after completing a task, and falling asleep after being idle for too long.

It’s not actually useful in a practical sense, but it absolutely improves the emotional value of using AI. What more could you want?



#### dsh-liang-skin The “Slide Into Ancestor Form” Meter

dsh-liang-skin is a DSH skin plugin that turns the reasoning intensity slider into a “slide into ancestor form” meme widget.

> Open-source repo: https://github.com/kingOfSoySauce/dsh-liang-skin

![](https://pic.yupi.icu/chengfang/047DSH.png)

Try it yourself. When you drag the reasoning intensity slider, you get to witness the character evolve all the way from Liangzi to Liangzu.

![](https://pic.yupi.icu/chengfang/%E6%B5%8B%E9%87%8F%E4%BB%AA.png)

Is this really the kind of creativity carbon-based lifeforms are capable of???

![](https://pic.yupi.icu/1/image-20260821101545031.png)



#### dsh-deepcel Disguises DSH as Excel

dsh-deepcel is an Excel-style theme plugin. After installation, the whole page becomes a classic spreadsheet interface.

> Open-source repo: https://github.com/Small-tailqwq/dsh-deepcel

![](https://pic.yupi.icu/chengfang/048DSH.png)

Take a look—the resemblance is pretty impressive, right?

![Excel-style deepseek harness](https://pic.yupi.icu/1/Excel%20%E9%A3%8E%E6%A0%BC%E7%9A%84%20deepseek%20harness.jpeg)

This honestly feels perfect for people who use Excel all the time at work. It should make a great sneaky-at-work tool.



#### dsh-ads Shoves Ads Into DSH

dsh-ads is a pure meme plugin dedicated to stuffing retro-style ads into DSH. After installation, the page fills up with all kinds of pop-up ads styled like the Chinese internet in 2005.

> Open-source repo: https://github.com/Nagi-ovo/dsh-ads

![](https://pic.yupi.icu/chengfang/066DSH.png)

Feed ads, pop-ups, fake antivirus windows, fake games, flashy banners—basically every chaotic thing can be shoved into DSH.

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

Absurd. Truly absurd. And you call this an AI tool?



## Final Thoughts

Finally, I organized the selected DSH plugins I tested this time into one diagram based on use scenarios for everyone’s reference:

![](https://pic.yupi.icu/chengfang/032DSH.jpg)

Let me say two extra things. Although DeepSeek Harness’s “everything is a plugin” design gives everyone nearly unlimited room for customization, plugins are still third-party code. Especially for plugins that can operate browsers, Shell, files, and remote access, you really need to pay attention to security. Before installing, it’s best to check the repository source and the permissions it declares.

Also, DSH itself is still evolving rapidly, and many plugins may not be perfectly compatible. During my tests this time, I ran into situations where incompatible plugin versions caused the web UI to fail to start properly. So my recommendation is to install only the plugins you truly need, and to use Git version control to manage your local DSH setup, so that if anything breaks you can easily roll back to a previously working version.

If you want to systematically learn the basic usage of DeepSeek Harness, you can read *DeepSeek Harness Beginner-Friendly Starter Tutorial* in the DeepSeek Harness section of this tutorial’s Programming Tools chapter. It covers everything from installation to real-world use in one article.
