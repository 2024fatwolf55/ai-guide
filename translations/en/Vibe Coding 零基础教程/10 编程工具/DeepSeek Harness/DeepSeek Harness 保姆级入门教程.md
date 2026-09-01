# DeepSeek Harness Beginner-Friendly Tutorial

> From installation to hands-on practice to plugin development, this guide walks you through DeepSeek’s open-source AI programming tool step by step.

Hello everyone, I’m programmer Yupi.

At the same time that DeepSeek released the official version of V4 Pro, it also open-sourced the much-anticipated **DeepSeek Harness**.

![](https://pic.yupi.icu/1/image-20260814125428438.png)

The open-source [GitHub repository](https://github.com/deepseek-ai/deepseek-harness) for DeepSeek Harness hit more than 70,000 Stars in less than a day. The AI world’s top star really is as powerful as people say.

![](https://pic.yupi.icu/1/image-20260814142939760.png)

In this article, I’ll start from installation and walk you through DeepSeek Harness’s core usage step by step. Absolute beginners can understand it too, so I recommend bookmarking it~



## 1. What Is DeepSeek Harness?

The word **Harness** can be translated as “tackle” or “rigging.” If you compare an AI model to a horse, then the Harness is all the engineering you need in order to control and direct that horse.

Harness engineering is about figuring out how to make the AI horse run faster, more steadily, and complete tasks more reliably.

Your project rules files, the tools you configure for AI, the way you arrange task decomposition and execution order, the testing and verification processes you design—**all of that counts as the Harness**.

![](https://pic.yupi.icu/1/2_harness_horse.png)

There’s a very elegant formula:

**Agent = Model + Harness**

The model is responsible for thinking and generation. The Harness is responsible for connecting those capabilities to the file system, the terminal, the browser, and the toolchain so AI can truly work in the real world.

![](https://pic.yupi.icu/1/8_agent_queals.png)

Previously, DeepSeek had only open-sourced the “model” half. The Harness side remained quiet the whole time. This release finally completes the picture.

You can think of DeepSeek Harness as a **highly customizable AI programming tool** positioned against Claude Code and Codex.

But its ambition goes beyond being just another coding Agent. It aims to be a configurable, recomposable Agent runtime environment, with the official slogan: **everything is a plugin**.

![](https://pic.yupi.icu/1/image-20260814130507825.png)

If you’ve made it this far, you’ve already passed 50% of readers.

And now, with just one more minute, you can install it on your own computer.



## 2. Installation

Installing DeepSeek Harness is genuinely very simple. Go to the [DeepSeek Harness official site](https://www.deepseek.com/harness/).

There you’ll see a one-line installation command:

![](https://pic.yupi.icu/1/image-20260814094053180.png)

Before running it, first make sure your computer already has Node.js installed. If not, go to the [Node official site](https://nodejs.org/zh-cn) and download the installer. Just use the beginner-friendly default installation.

![](https://pic.yupi.icu/1/image-20260814095005547.png)

Once the environment is ready, copy the command, open the terminal on your computer, and run:

```bash
npx @deepseek-ai/dsh web
```

Wait a moment, and the terminal will output a URL. Open it, and you’ll enter the DeepSeek Harness web interface.

![](https://pic.yupi.icu/1/image-20260814095037727.png)

The first time you use it, you need to fill in a DeepSeek API Key:

![](https://pic.yupi.icu/1/image-20260814130304526.png)

Go to the [DeepSeek Open Platform](https://platform.deepseek.com), create an API Key, and be careful not to leak it. Then just copy and paste it here.

![](https://pic.yupi.icu/1/image-20260814130139004.png)

At this point, DeepSeek Harness is successfully installed. Pretty simple, right?

![](https://pic.yupi.icu/1/image-20260814130332224.png)

If you’ve read this far, you’re already ahead of 60% of readers. Next, let’s try it in practice.



## 3. Harness in Practice

After entering the web interface, choose a project folder that you want AI to operate on, and you can officially start working.

In the chat box, you can choose the model, adjust the model’s reasoning level, and set the Agent’s permissions for file system and terminal operations as needed.

![](https://pic.yupi.icu/1/image-20260814143734964.png)

By default, it uses **standard mode**, which provides the full set of capabilities expected from an AI programming tool. In most cases, that’s enough. I’ll explain the differences between the modes in detail later.

See? Doesn’t it look quite a lot like Codex and similar AI programming tools?

![](https://pic.yupi.icu/1/image-20260814143812878.png)

Exactly—just treat it as a domestic version of Codex. AI programming, office automation, and similar tasks can all be handled with it.

Let’s try a few tasks.



### Task 1: Analyze a Code Repository and Draw an Architecture Diagram

For the first task, I asked DeepSeek Harness to analyze **its own source code repository** and draw an architecture diagram simple enough for anyone to understand.

The DeepSeek Harness repository is quite large and has lots of modules, so it’s a good test of AI’s code-understanding ability.

![](https://pic.yupi.icu/1/image-20260814143958846.png)

Send AI this prompt:

```
分析当前项目的代码仓库结构，绘制一张清晰的架构图。
要求用 Mermaid 语法输出，让完全不懂代码的人也能一眼看明白各模块的关系。
```

You can see that AI immediately starts reading files, analyzing the project structure, and executing very quickly. Even better, every step it takes is clearly displayed in the interface.

![](https://pic.yupi.icu/1/image-20260814135407082.png)

Very soon the task is complete. AI outputs the architecture in Mermaid syntax, although DeepSeek Harness does not render Mermaid diagrams automatically by default.

![](https://pic.yupi.icu/1/image-20260814135445191.png)

After copying that code into a Mermaid rendering tool, you can see the full architecture diagram. The visual effect is only average, but the content is still fairly complete.

![](https://pic.yupi.icu/1/image-20260814135528564.png)

Below the output, you can also see the task’s Token consumption, the current context usage, and the overall Token usage of the conversation.

![](https://pic.yupi.icu/1/image-20260814135615629.png)

You can also open the **Trajectory** panel at the top to clearly inspect every message and tool invocation in the conversation.

![](https://pic.yupi.icu/1/image-20260814135652086.png)

That’s one of DeepSeek Harness’s distinctive features: every run leaves a visible trail.



### Task 2: Build a Knowledge Explanation Website

For the second task, I asked it to build a website that uses interactive animations to explain a concept.

The concept I chose was “attention residual,” using exactly the same prompt I previously used when evaluating Codex + DeepSeek V4 Pro.

![](https://pic.yupi.icu/1/image-20260814125730242.png)

After about 20 minutes, AI finished the task. It wasn’t especially fast, to be honest—the main delay came from AI checking its own work.

What was impressive, though, was that the cache hit rate reached 99%. In other words, almost all of the cost was billed as cached usage, so the actual expense was extremely low. That part was really strong.

![](https://pic.yupi.icu/1/image-20260814111941126.png)

As for the result, it looked pretty good. The animation was lively:

![](https://pic.yupi.icu/1/image-20260814112144980.png)

And the connections between the lines and points were very accurate:

![](https://pic.yupi.icu/1/image-20260814112210801.png)

What surprised me even more was that, just like the version previously built by Claude Opus 5, this DeepSeek-built version also included a summary and quiz section, making the explanation much more complete.

![](https://pic.yupi.icu/1/image-20260814112320399.png)

Overall, compared with the result I previously got using DeepSeek V4 Pro + Codex, this version was much better.

The old version didn’t even align the connection lines properly, so I think you can clearly feel the difference.

![Version built with DeepSeek V4 Pro + Codex](https://pic.yupi.icu/1/1786598800323-d83866da-24d8-4d07-9de8-72468e9102e8.png)

Based on this example alone, I genuinely felt that DeepSeek V4 Pro could stand up to Claude. The Harness really matters.



### Task 3: Build a 3D Game

For the third task, I increased the difficulty and asked it to develop a 3D web game.

This time the project was the bamboo cicada toy—arguably the best toy under ten million yuan. But compared with the earlier 2D version I tested before, this one was much more complex, because it also needed to support camera-based gesture recognition to control the bamboo cicada’s rotation.

![](https://pic.yupi.icu/1/image-20260814125744391.png)

You can see that while developing, AI also checks and verifies by itself whether the program is working correctly:

![](https://pic.yupi.icu/1/image-20260814125858778.png)

This run took nearly 40 minutes. Once the task finished, the cache hit rate was almost 100%!

![](https://pic.yupi.icu/1/image-20260814124010293.png)

As for the final result, it was pretty good. You could drag the mouse to rotate the viewing angle:

![](https://pic.yupi.icu/1/image-20260814124039419.png)

If you grabbed the bamboo stick and moved the mouse back and forth, the bamboo cicada rotated accordingly. Just look at the shadow in the screenshot—the attention to detail was excellent.

![](https://pic.yupi.icu/1/image-20260814124144273.png)

It could also turn on the camera, letting you rub your hands together to control the bamboo cicada’s rotation. The interaction felt genuinely fun:

![](https://pic.yupi.icu/1/image-20260814124348140.png)

Overall, the functionality worked, there were no obvious program issues, and the details were handled very well. My evaluation: excellent.

Compared with the 2D version I previously made with DeepSeek V4 Pro + Codex, this was a huge leap forward:

![Earlier 2D version built with DeepSeek V4 Pro + Codex](https://pic.yupi.icu/1/1786599373401-a561d583-aeca-46c3-9895-d55c9356e731.png)



### Task 4: Build a Full-Stack AI App

For the final task, I asked it to build a full-stack app with built-in large-model integration: an **AI Web PPT Generator**.

The user pastes in a long block of text, the backend calls the DeepSeek model to split it into multiple PPT slides, and the frontend renders them into a fullscreen web-based presentation.

This time, I even deliberately included a requirement in the prompt telling AI to fetch my DeepSeek API Key from my own computer, just to see whether it could handle that itself.

![](https://pic.yupi.icu/1/image-20260814125805219.png)

During execution, AI may ask you to confirm permissions—for example, whether to allow reading a certain file or running a command. The security aspect was handled fairly well.

![](https://pic.yupi.icu/1/image-20260814124930962.png)

After about half an hour, AI finished the task. Let’s look at the result.

The interface style was pretty nice and had a tech feel to it. I pasted in an article to turn into a PPT.

There was even a nice surprise: we could choose the generated PPT’s style ourselves, and also choose whether to turn reasoning mode on.

![](https://pic.yupi.icu/1/image-20260814145140404.png)

Then click generate.

During generation, you can watch the progress and output information in real time. That interactive feel is much better than the old version.

![](https://pic.yupi.icu/1/image-20260814145225002.png)

The generation speed was also quite fast. The result looked good, so I opened it in fullscreen view.

This generated PPT was full of a futuristic feel, and the layout was pretty reasonable too, with clear visual hierarchy.

![](https://pic.yupi.icu/1/image-20260814145103287.png)

Compared with the version I previously built using DeepSeek V4 Pro + Codex, this one was much better: the layout was more reasonable and the color scheme more elegant.

![PPT previously built with DeepSeek V4 Pro + Codex](https://pic.yupi.icu/1/1786600257499-75fdc7f7-740c-4c27-8979-34683f66afcd.png)

You could also switch among several theme color schemes, all of them fairly classic styles.

![](https://pic.yupi.icu/1/image-20260814145015136.png)

Looking at this version, I honestly feel it can compete with Claude Opus 5. Top tier.

![PPT tool built with Claude Opus 5](https://pic.yupi.icu/1/1785146087244-153c15ee-6ffe-4f7b-8c8d-8224fe272074-20260813162825918.png)



### My Evaluation After Testing

After running through all these tasks, my overall feeling is that DeepSeek Harness is reasonably fast. Its strengths are the extremely high cache hit rate and the fact that its execution process is very transparent. You can see exactly what the AI is doing at every step, which tools it is calling, and which files it is reading. It doesn’t feel like some black-box operation that betrays user trust.

From my own testing so far, DeepSeek V4 Pro paired with its own Harness really does seem capable of standing alongside Claude Opus 5 for AI programming. That official benchmark gap of only 0.1 was not a lie.

**Looks like if you’re using a DeepSeek model, you really should be using DeepSeek’s own Harness tool with it.**

![DeepSeek V4 Pro benchmark image](https://pic.yupi.icu/1/deepseek%20v4%20pro%20%E8%B7%91%E5%88%86%E5%9B%BE.jpeg)

And now, guess how much all of these tasks cost in total?

**The answer is: less than 5 RMB!**

Because the cache hit rate was basically above 99% the whole time, the actual cost stayed extremely low.

![](https://pic.yupi.icu/1/image-20260814131247833.png)

That said, one thing to note is that DeepSeek has already announced a price increase starting August 17, and the price increased by several times.

![DeepSeek price increase](https://pic.yupi.icu/1/DeepSeek%E6%B6%A8%E4%BB%B7%E5%9B%BE.jpeg)

Even so, after the price hike it’s still much cheaper than Claude, and cached usage remains very inexpensive.

Overall, using a model together with its own Harness tool is seriously powerful.

![](https://pic.yupi.icu/1/image-20260814144904693.png)

If you’ve read this far, you’re already ahead of 70% of readers.

Next, let’s look at DeepSeek Harness’s different runtime modes and see what else it can do.



## 4. The Four Runtime Modes

DeepSeek Harness provides four runtime modes for different usage scenarios.

![](https://pic.yupi.icu/1/image-20260814145323400.png)

**Standard mode** is the one we used throughout the practical demos above. It loads the full toolset, including file editing, shell commands, web search, sub-Agents, Skills, and more, covering essentially all everyday development needs. In most cases, just use this one.

**Minimal mode** keeps only the two most basic tools: Bash and file editing. Everything else is turned off. This mode is mainly used by the official team for model benchmark testing, where they want to evaluate pure coding ability in the smallest possible environment. Normal users usually won’t need it.

**PTC mode**, short for Programmatic Tool Call, allows the model to generate a piece of TypeScript code that chains multiple tool calls together in one execution, instead of calling tools step by step. It is especially good for tasks with many steps but clear logic, such as batch renaming or full automation pipelines.

**Creation mode** is designed for people who want to develop plugins, create new tools, or customize their own presets. It inherits the full capabilities of standard mode while additionally allowing AI to inspect which plugins are currently running, experiment with new combinations, and even create brand-new mode presets. Later, we’ll use this mode to develop our own plugin.

So to summarize, the essential difference among the four modes is simply **which plugins and tools are loaded into the current session**. Minimal mode keeps only two tools, standard mode gives you the full loadout, and creation mode even lets AI inspect and modify its own plugin configuration.

![](https://pic.yupi.icu/1/image-20260814150646065.png)

If you’ve made it this far, you’re already ahead of 80% of readers—but the part of DeepSeek Harness that excites me most is only just beginning.



## 5. Plugins

Now we’re getting to the biggest difference between DeepSeek Harness and tools like Codex or Claude Code: the plugin system.



### Everything Is a Plugin

In DeepSeek Harness, **everything is a plugin**.

Models, tools, skills, sessions, sandboxes, the UI, and even the Agent runtime loop itself are all plugins. Any of them can be unplugged and replaced.

![](https://pic.yupi.icu/1/image-20260814135129452.png)

That means if there is any part of the tool you don’t like, you can replace it or extend it by installing plugins, without changing the framework’s source code.

Codex and Claude Code also have some extension capabilities, but they are nowhere near this level of openness. DeepSeek Harness is much more customizable.

![](https://pic.yupi.icu/1/image-20260814135203770.png)

Next I’ll first show you how to use community plugins, and then how to build your own.



### Using Community Plugins

On the DeepSeek Harness official site, click **Community Plugins** and you can view all [community-developed plugins](https://github.com/topics/dsh-plugin).

In practice, these are just GitHub projects tagged with the `dsh-plugin` topic:

![](https://pic.yupi.icu/1/image-20260814131851843.png)

That said, the official page is a bit messy because there are too many plugins mixed together. I’d actually recommend going straight to the curated [Awesome repository](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin), which organizes high-quality plugins by category. Each one has been verified, and even though the ecosystem had only been online for one day, it already had more than 300 installable plugins. The growth speed is honestly wild.

![](https://pic.yupi.icu/1/image-20260814132201186.png)

Installing a community plugin is also very simple. For example, I liked this whale-girl skin beautification plugin:

![](https://pic.yupi.icu/1/image-20260814133548484.png)

All I need to do is open the DeepSeek Harness web page, pick any working directory, and give the plugin’s GitHub URL to AI so it can install it for me.

If you want to save time, you can first switch the Agent’s permission setting to full access, so AI won’t ask you for confirmation on every command it runs.

```markdown
帮我安装插件 https://github.com/Small-tailqwq/dsh-deep-whale
```

![](https://pic.yupi.icu/1/image-20260814145412556.png)

AI finishes the installation quickly. Then, just as it tells us, open the terminal and restart the DeepSeek Harness web interface:

```bash
npx @deepseek-ai/dsh web
```

Refresh—and how’s that?!

![](https://pic.yupi.icu/1/image-20260814133452050.png)

Pretty nice, right? Makes you feel even more like using AI.

If you don’t want the skin anymore, just tell AI to remove it and restore the original setup:

```markdown
帮我取消掉这个插件，回到最开始的设置
```

![](https://pic.yupi.icu/1/image-20260814133846899.png)

There are some other fun skin plugins too. For example, [dsh-deepcel](https://github.com/Small-tailqwq/dsh-deepcel) turns the interface into an Excel-style layout. Isn’t this the ultimate slacking-off tool?

![Excel-style deepseek harness](https://pic.yupi.icu/1/Excel%20%E9%A3%8E%E6%A0%BC%E7%9A%84%20deepseek%20harness.jpeg)

There’s also [dsh-tianshu-tui](https://github.com/huiliyi37/dsh-tianshu-tui), which directly transforms the web interface into a TUI terminal style:

![](https://pic.yupi.icu/1/tui-screenshot.jpg)

And the most outrageous one is [dsh-ads](https://github.com/dsh-external/dsh-ads), which adds 2005-style Chinese website sidebar ads, conversation feed ads, and popup windows to your web interface. Pure abstract art...

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

Because DeepSeek Harness is basically a web app running in the browser, customizing skins is actually very easy.

But skin plugins are only the tip of the iceberg in the DeepSeek Harness ecosystem. If you browse the curated list, you’ll notice that many truly practical plugins are moving toward becoming mature AI programming product features.

For example, [DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar) improves the sidebar interaction experience, and [dsh-at-file](https://github.com/omdsh-dev/dsh-at-file) lets you quickly reference files using the `@` symbol.

![](https://pic.yupi.icu/1/dsh-better-sidebar.png)

The plugin I’m personally most optimistic about is [modlens](https://github.com/liustack/modlens), the first vision plugin for DeepSeek Harness. You can paste in an image, and it will parse the image into structured JSON text information for the model, including OCR text, page layout, and semantic content.

![](https://pic.yupi.icu/1/demo-dsh-paste.jpg)

This plugin solves exactly the biggest weakness of DeepSeek V4 Pro as a text-only model: it can’t see images. After AI writes a page, it can’t take a screenshot and judge whether the layout looks right or whether frontend elements are misaligned. Now the community has already filled that gap with a plugin.

These plugins fill in many of DeepSeek Harness’s weaker spots in interaction details and capabilities, which also proves how flexible the “everything is a plugin” architecture really is. The community itself can improve product experience, and users gain more choice.



### Creating Your Own Plugin

Simply installing other people’s plugins isn’t satisfying enough. The truth is, building your own plugin is also quite easy—because you can let AI write it for you.

Switch to **creation mode**. In this mode, AI can inspect the current plugin tree, experiment with new plugins, and finally package and publish them.

![](https://pic.yupi.icu/1/image-20260814150335461.png)

For example, I had previously installed a desktop-pet plugin in Codex, and now I wanted to port it over to DeepSeek Harness.

![](https://pic.yupi.icu/1/image-20260814134128295.png)

So in creation mode, I simply gave AI this requirement:

```
帮我开发一个 DSH 桌宠插件，在 Web 界面右下角显示一个小宠物。
你需要直接把我本地的 Codex 目录下的 Kun Like 桌宠素材移植过来，不用自己重新设计形象。
它会根据当前 Agent 的工作状态做出不同动作。
当任务完成后，还会发出「你干嘛~」的声音
音频文件路径在：/Users/yupi/Downloads/你干嘛哎呦.mp3
```

![](https://pic.yupi.icu/1/image-20260814135037195.png)

After AI develops the plugin, it first asks for your approval before installing it officially, so the safety is pretty well handled.

![](https://pic.yupi.icu/1/image-20260814150406161.png)

Very soon the plugin is complete, and the little basketball-playing chicken appears on the screen!

Just talk to AI once and you’ll hear the “What are you doing~ ow” sound effect. Truly refreshing and spiritually cleansing~

![](https://pic.yupi.icu/1/image-20260814143216935.png)

Besides desktop pets, you can use your imagination to build all kinds of interesting plugins—for example, a health assistant that reminds you to drink water on schedule, a floating window showing your model account balance in real time, or your own custom theme skin.

If you want to share your plugin with others, you only need to let AI push the code to GitHub using the GitHub MCP plugin:

![](https://pic.yupi.icu/1/image-20260814143547057.png)

And very quickly, it’s open-sourced:

![](https://pic.yupi.icu/1/image-20260814145634209.png)

Then just add the `dsh-plugin` topic tag to the repository:

![](https://pic.yupi.icu/1/image-20260814145913770.png)

AI even helped me add screenshots to the `README` introduction file. So considerate, right? Now everyone can join me in becoming little black fans~

> Open-source repo: https://github.com/liyupi/dsh-kun-like-pet

![](https://pic.yupi.icu/1/image-20260814145958050.png)



## Final Words

Congratulations. DeepSeek Harness had only been released for one day, and you’ve already mastered its basic usage—putting you ahead of at least 90% of people!

Because of time, I didn’t expand on many advanced use cases, such as batch-running tasks in command-line mode, integrating and switching other large models, customizing Agent presets for different work scenarios, or even deploying it to a server for shared team usage. I’ll explain those in detail in future advanced tutorials.

I’m extremely optimistic about this project, because **open source + everything is a plugin** gives DeepSeek Harness an incredible level of openness. Its possibilities are practically unlimited.

**Maybe before long, every one of us will be using AI programming tools that look different from everyone else’s, because each person will be able to freely assemble their own setup based on their needs. I think that’s very cool~**

If you want to learn AI programming more systematically, keep reading the other articles in the programming tools section of this tutorial. They’ll take you step by step from setup to project practice.

Keep going—I’m looking forward to seeing the interesting things you build with DeepSeek Harness!
