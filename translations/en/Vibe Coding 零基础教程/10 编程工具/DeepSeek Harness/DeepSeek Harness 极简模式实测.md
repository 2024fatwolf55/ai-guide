# DeepSeek Harness Minimal Mode Hands-on Test

> Can minimal mode actually be used for real work? I ran two real projects and now I can tell you the answer.

Hello everyone, I’m Yupi.

The AI world blew up again this week. DeepSeek dropped two major bombs at the same time: the official release of the DeepSeek V4 Pro model, plus the open-sourcing of the DeepSeek Harness tool.

![](https://pic.yupi.icu/1/image-20260814125428438.png)

I immediately published a hands-on review of DeepSeek V4 Pro and a beginner-friendly tutorial on DeepSeek Harness.

**I’m honestly numb at this point. I open my eyes every day and I’m already writing. By the time I finish the video, it’s almost time to sleep.**

Can these hot topics stop coming back-to-back for once? I’m Chovy here!

![](https://pic.yupi.icu/1/i2Q42-2h5cZaT3cSq4-po.jpg)

Back to the point. After testing it, my strongest feeling was this: **whether DeepSeek is paired with its own Harness or not makes a ridiculously huge difference.**

The exact same DeepSeek V4 Pro model couldn’t even draw lines properly when used raw with Codex, but once switched to its own Harness, it somehow started benchmarking against Claude???

It turned me into a true “master of changing expressions”!

![](https://pic.yupi.icu/1/09bdf5c0e4b2738acfb6af05e7764e253461565210692083.jpg)

Looks like Harness really is DeepSeek’s signature weapon. Without it, DeepSeek is basically a bare-bones character.

An independent overseas evaluator named sentdex got an even more dramatic result. Using the same DeepSeek V4 Flash model weights, his own crude tool passed only 44 out of 89 tasks. After switching to the community’s full Harness, it reached 64 out of 89—20 more tasks passed.

**Agent = Model + Harness**

As models get stronger, the Harness provided to the model becomes more and more important.

![](https://pic.yupi.icu/1/8_agent_queals.png)

That’s also why DeepSeek V4 Pro shows this bizarre “god-or-ghost duality.” Whether the same model actually performs well depends heavily on what tool and what environment you run it with.

And over the past two days, the community’s most-discussed claim has revolved around a seemingly unremarkable mode inside DeepSeek Harness.



## The Dark Art of Minimal Mode

Some people found that simply switching DeepSeek Harness into “minimal mode” caused model performance to skyrocket instantly, supposedly reproducing the level of the gray-release test version and even reaching Fable 5–level performance.

As soon as that claim came out, dozens of hands-on test videos popped up on Bilibili, each title more outrageous than the last.

So what exactly is this “minimal mode”?

After installing DeepSeek Harness, the default is “standard mode.” It equips all the capabilities you’d expect from an AI coding tool: file read/write, terminal commands, web search, task planning, Skills, sub-Agents, and more—a total of over 20 tools.

![](https://pic.yupi.icu/1/image-20260814143734964.png)

Minimal mode, on the other hand, is much more stripped down. Officially, it keeps only two tools: one long-running terminal and one file editor. Everything else is disabled.

![](https://pic.yupi.icu/1/image-20260815154823126.png)

The official positioning is very clear: it exists specifically for running model benchmark tests. So the environment is cut down to the cleanest possible state to ensure different models can be compared fairly under the same standard.

In other words, minimal mode was never meant for real work. It was made for testing models.

So if you take exam mode and use it for work, does it actually become stronger?

Enough talking—let’s test it directly!



## Hands-on Test 1. A 3D First-Person Shooter Game

For the first test, I had DeepSeek V4 Pro build a 3D first-person CS-style shooting game.

Full prompt:

```
用 Three.js 开发一个 3D 第一人称射击游戏，做成一个单页面项目，打开浏览器直接能玩。
要求第一人称视角，WASD 控制移动，鼠标控制瞄准和射击；
场景里至少有 3 个敌人会自己巡逻，发现玩家后会追击，被打中后消失；
界面上要显示准星、血量和得分。
```

Why choose this task?

Because 3D FPS games are a classic among classics in game development. Tutorials for them are everywhere online, so the model must have seen this kind of task countless times in training data. This kind of task purely tests coding ability—it doesn’t require searching documentation or checking APIs. If the model has the knowledge in its head, it can just start coding away.

Using the exact same prompt, I first ran it once in standard mode, then once in minimal mode.

![](https://pic.yupi.icu/1/image-20260815122357248.png)

First, let’s look at the difference in execution logs between the two modes.

Standard mode invoked Skills and produced a lot of text output along the way. It told you what it was thinking and what it planned to do—the exact kind of experience we normally get from AI coding tools.

![](https://pic.yupi.icu/1/image-20260815122503107.png)

Minimal mode only used thinking, terminal, and string replacement. There was no extra chatter at all. The AI felt like a mute worker with its head down just doing the job.

![](https://pic.yupi.icu/1/image-20260815122619221.png)

Standard mode finished in 50 steps. The AI detected and fixed bugs on its own. Model reasoning took 21 minutes, tool calls took 12 minutes, and the total was just over 33 minutes. It used 5.2 million input tokens and 105k output tokens.

![](https://pic.yupi.icu/1/image-20260815123130636.png)

Minimal mode ran for 77 steps. Model reasoning took 17 minutes, tool calls took only 6 minutes, and the total was just over 23 minutes—almost 10 minutes faster than standard mode! Even the final summary it gave me was extremely concise.

![](https://pic.yupi.icu/1/image-20260815123106268.png)

But there’s one counterintuitive thing here: minimal mode actually used more input tokens, reaching 5.9 million.

The reason isn’t hard to understand. Minimal mode has no context compression, and it used half again as many steps as standard mode. At every step, it had to resend the full previous history, so naturally the input accumulated. Fortunately, both modes had nearly 100% cache hit rates, so the cost difference from that gap was basically negligible.

Now for the main event: the final result.

The game built in standard mode felt very smooth. Movement, jumping, sprinting, shooting, and killing enemies all worked fine. It even supported a double jump like in CrossFire.

But the enemies couldn’t shoot bullets. They could only chase you around, so the pressure was pretty weak. And there was a bug: after chasing you for a while, the enemies would just walk away by themselves. I never asked for that in the prompt—how is that reasonable?

![](https://pic.yupi.icu/1/image-20260815123745988.png)

One nice detail: if you got beaten to death by the bot, it triggered a collapse effect, and the viewpoint looked just like a real person falling to the ground.

![](https://pic.yupi.icu/1/image-20260815123510893.png)

Now look at the result from minimal mode. The interface was cleaner than standard mode’s, the background wall looked more realistic, and movement, jumping, sprinting, shooting, and killing enemies all worked normally as well.

What’s more, the enemies in minimal mode could actually fire bullets. They felt smarter, and the gameplay pressure was stronger.

![](https://pic.yupi.icu/1/image-202608151243407956.png)

However, when I got knocked down, my character’s body was still standing upright. Compared with the falling-to-the-ground perspective in standard mode, it definitely felt a bit less convincing.

![](https://pic.yupi.icu/1/image-20260815124017407.png)

Judging only from the finished products, the two were pretty evenly matched, each with its own strengths and weaknesses.

But in terms of time spent, minimal mode was a full 10 minutes faster. Even though it used slightly more input tokens, nearly all of them were served from cache, so the difference can basically be ignored.

So in this round, I’d say minimal mode won by a slight margin.



## Why Does Minimal Mode Perform Better?

The logic is actually simple. Here’s an analogy.

If I ask you to tighten a screw and hand you a screwdriver, you’ll just do it directly. But if I give you a whole toolbox—with wrenches, pliers, a power drill, and a screwdriver—you might first rummage around, hesitate over which tool to use, and then still end up picking the screwdriver.

AI works the same way. The default standard mode gives the model more than 20 tools. At each step, the model has to decide which tool to use, and that decision-making alone takes up part of its reasoning capacity. On top of that, the instructions for those 20-plus tools also have to be stuffed into the context. Naturally, the amount of attention the model can devote to the actual task gets diluted.

Minimal mode cuts away all of those capabilities and leaves only a terminal and a file editor. The AI can just start writing code directly, without analysis paralysis, so it becomes naturally faster and more accurate.

![](https://pic.yupi.icu/1/image-20260814150646065.png)

In fact, DeepSeek’s official benchmark tests are run in minimal mode. If you look at the tiny text at the bottom of the benchmark image, it says V4-Pro was tested using DeepSeek Harness minimal mode as the framework.

![](https://pic.yupi.icu/1/HPmOJZlbUAAOgVt.jpeg)

And one developer ran a very strict controlled experiment. He used his own engineering-maintenance benchmark set, kept the same machine, the same model, and the same reasoning level, and changed only the Harness mode. The result was 91 points in standard mode, 92 in PTC mode, and 99 in minimal mode. So yes, the gap is real.

![](https://pic.yupi.icu/1/image-20260815140617668.png)



## Can Minimal Mode Be Used for Real Work?

Important: minimal mode does not make the model itself stronger. It just prevents the model from getting distracted inside an extremely restricted environment.

And the price is obvious too: web search, task planning, Skills, sub-Agents, and context compression are all gone.

Minimal mode only leaves the model with a terminal and a file editor. It can still create files, install dependencies, and execute commands, but it can’t quickly look up external information through tools, and the longer the conversation goes, the more likely it is to forget earlier context.

There’s another big issue for usability: it barely reports back to you. All you see is a long sequence of terminal commands and file replacements. What the AI is thinking, what step it’s on, and whether it has hit a roadblock—you have no idea. So it’s actually more suitable for tasks where you only care about the final outcome and don’t care about the intermediate process.

![](https://pic.yupi.icu/1/image-20260815122619221.png)

Have you noticed that this state feels a lot like the early 2023–2024 days when we first started using AI to write code? Back then, AI could only hard-code things from the knowledge it had in its head, and as soon as it encountered an unfamiliar framework, it would start confidently making up APIs and coding patterns.

Later we got tool use, MCP, Skills, and context management, which gradually evolved into today’s Harness systems. Step by step, AI was transformed from a model that could only chat into an “engineer” that can research documentation, edit code, and run tests on its own.

![](https://pic.yupi.icu/1/2_harness_horse.png)

Minimal mode is basically like stripping away more than half of the equipment we’ve built up over the years.

So what happens if we switch to a task that *must* rely on web search to be completed? Can minimal mode still fight?

Let’s try it.



## Hands-on Test 2. AI Pet Adoption System

For the second test, I switched to a more complex task and asked AI to build an “AI Pet Adoption System.”

Full prompt:

```
开发一个 AI 宠物领养系统，前后端都要能跑起来。
先联网搜索 DeepSeek 鲸鱼娘的图片，下载至少 20 张存到项目里，作为默认的待领养宠物；
后端从我电脑的环境变量里读取 DeepSeek 的 API Key，调用大模型给每只宠物生成一段领养文案；
前端展示宠物列表和 AI 写的介绍，点击可以领养。
```

This task was completely different from the previous one. It needed to read a local environment variable to get the API key, search and download images from the web, coordinate frontend and backend APIs, and call an AI model.

Here’s what happened. Standard mode ran for 59 steps. Model reasoning took 10 minutes, tool calls took 38 minutes, for a total of 49 minutes. It used 4.2 million input tokens and 54k output tokens.

The key point is that it successfully found my local `DEEPSEEK_API_KEY` and delivered the finished result end to end without any intervention from me.

![](https://pic.yupi.icu/1/image-20260815125822195.png)

Minimal mode ran for 87 steps. Model reasoning took 11 minutes, tool calls took only 16 minutes, and the total was under 28 minutes—again 21 minutes faster than standard mode! Token usage was about the same too.

But it failed to read `DEEPSEEK_API_KEY` from my computer, so in the end I still had to fill it in myself. That made it less deliverable.

![](https://pic.yupi.icu/1/image-20260815125937243.png)

Let’s first look at the result from standard mode. The overall layout was pretty good. The pet cards were nicely arranged, though not stunning, and the text in the upper right wasn’t aligned quite correctly.

![](https://pic.yupi.icu/1/image-20260815130513161.png)

Still, AI successfully completed the tasks of crawling Whale Girl images and calling the AI model to generate descriptions:

![](https://pic.yupi.icu/1/image-20260815130539711.png)

You could click to adopt the Whale Girl you wanted.

![](https://pic.yupi.icu/1/image-20260815130623520.png)

The filtering feature also worked normally. You could switch between “All / Available / Adopted.” Adopted whale cards turned gray and showed the adopter’s name, so it was obvious at a glance which pets already had owners.

![](https://pic.yupi.icu/1/image-20260815130727937.png)

Now look at minimal mode. I first had to manually obtain the DeepSeek API Key, then ask AI to fill the environment variable and run the program.

The main page looked okay too—pretty similar to what standard mode produced, which makes sense because it was the same model.

But in terms of practical functionality, it was clearly weaker. There was no filtering at all. And the cards only showed a name, an ID, and a short blurb. Breed, age, personality tags—none of that was there. Compared with standard mode, where every card included things like “gray whale, 2 years old, #humorous #snarky,” that one looked like a real adoption site.

And that little badge in the upper right saying “AI description: DeepSeek generated”—no matter how you look at it, it didn’t feel like a product for normal users. It felt more like a debug label.

![](https://pic.yupi.icu/1/image-20260815131240270.png)

Minimal mode also allowed clicking to adopt and entering the adopter’s nickname:

![](https://pic.yupi.icu/1/image-20260815131636284.png)

After successful adoption, the pet could no longer be adopted by anyone else, so the functional logic was correct. But because there was no filtering, you couldn’t tell which pets you yourself had adopted. You had to scroll down one by one to find them.

![](https://pic.yupi.icu/1/image-20260815131748359.png)

By the way, can you guess how much all four tasks above cost in total?

The answer is 3.13 yuan. Do you think that’s expensive? (My final stubbornness before the price hike.)

![](https://pic.yupi.icu/1/image-20260815131901668.png)



## Pros and Cons of Minimal Mode

Now that both projects are done, let me share my take on minimal mode.

First, its biggest strength is speed. It was 10 minutes faster on one task and 21 minutes faster on the other, while costing about the same. It’s also extremely direct. You tell it what to do, and it just does it. It doesn’t spend a long time discussing a plan with you first.

Its weaknesses are equally obvious. It barely reports anything during the whole process, so you don’t know what the AI is doing. It can’t directly access the web through tools and has to rely on workarounds through scripts. Although the final features it delivers can run, the level of detail and completeness is clearly worse.

So the summary in one sentence is this: **the higher your quality expectations for the finished product, the worse minimal mode performs**.

If all you need is a playable game demo, it’s completely fine. But if you want a polished product that can be delivered directly to users, that’s where it starts to drop the ball.

Also, if your task strongly depends on a specific tool, the gap becomes even wider. For example, DeepSeek V4 Pro itself can’t look at images, so it needs Harness to mount a vision plugin to compensate for that weakness. Tasks like that become much more troublesome in minimal mode.



## Wait—There’s an Even Better Player?

At first I thought the story would end there. Minimal mode is amazing for benchmark scores, but not very practical. If you want good delivery quality, standard mode still seems like the honest choice.

But last night, Bilibili creator “小明XBright” dropped a bombshell discovery.

While fully retaining the 20-plus tools in standard mode, he used a self-written two-stage plugin called `dsh-anchored-standard` and ran his engineering-maintenance benchmark twice. He got 98 and 99 points, averaging 98.5—not only matching minimal mode but even slightly surpassing it.

![](https://pic.yupi.icu/1/image-20260815172540939.png)

That’s wild. How did he do it?

The principle is this: DeepSeek V4 Pro is extremely sensitive to the tool structure in the very first request. If you dump all 20-plus tools on it right away in round one, it gets confused and drops to 91 points. But if the first round uses the same system prompt as minimal mode and only provides two tools—the terminal and file reading—so the model enters the task with a minimal-mode style of reasoning, and then immediately restores the full toolset after the first tool call is completed, the score shoots straight to 98.

You can also see the difference directly from the model’s reasoning process. In standard mode, the reasoning trace contains 208 instances of “let me” and 55 intermediate replies, which shows it’s constantly hesitating, planning, and self-confirming. Under guidance from this two-stage plugin, it starts with “We need,” and the entire trace adopts a “what do *we* need to do” tone. Across two runs, the word “we” appears more than 300 times.

![](https://pic.yupi.icu/1/image-20260815185225654.png)

Same model. Completely different thinking style.

He also dug through the official DeepSeek Harness source code and found hard evidence. There’s a test file in the repository literally named “sends the exact RL prompt and schemas,” which basically means “send the exact reinforcement-learning prompt and tool definitions.” DeepSeek officially admitted it themselves: minimal mode uses the same format the model saw during training.

![](https://pic.yupi.icu/1/image-20260815184558652.png)

So when you temporarily swap in a different tool list that it hasn’t really seen before, it gets a little lost.

Even more interestingly, DeepSeek V4 Flash has no such problem at all. Flash stays stable between 90 and 95 points across different Harness setups, and switching to minimal mode makes little difference. So this makes it look even more like V4 Pro has overfit to DeepSeek’s own format during training. That basically confirms it: Harness really is DeepSeek’s signature weapon.

This discovery is more valuable than the simple claim that “minimal mode massively boosts performance.” It reveals a deeper issue: the extent to which current AI models can fully unleash their abilities depends heavily on whether they can recall the state they were in during training. The future direction of Harness optimization may not be adding more tools or removing tools, but figuring out how to align with the training distribution during startup—waking up the model’s strongest execution state first, and only then releasing full capabilities.

If you’re interested, give it a try.

Open-source plugin repo: https://github.com/xiaobright/dsh-anchored-standard

![](https://pic.yupi.icu/1/image-20260815172819422.png)



## Final Thoughts

That’s it for my testing of this minimal-mode strategy.

**The conclusion is simple: use it when you want speed, use standard mode when you want stability.**

That said, the idea behind that two-stage plugin really impressed me. Once the Harness plugin ecosystem matures further, we may see more plugins focused specifically on tuning the model into its optimal state first and only then handing over the full toolset. If that happens, the real-world experience of using DeepSeek may climb yet another level.

If you want to understand DeepSeek Harness more systematically, you can read *DeepSeek Harness Beginner-Friendly Starter Tutorial* in the DeepSeek Harness section of this tutorial’s Programming Tools chapter. It walks you through everything step by step, from installation to real-world use.
