# DeepSeek Harness Agent Presets Explained

> How do you choose among the four built-in modes? And how do you create your own custom Agent preset? This article explains it all.

Hello everyone, I’m programmer Yupi.

DeepSeek Harness is DeepSeek’s latest open-source AI Agent runtime environment. You can think of it as a highly customizable AI programming tool positioned against Claude Code and Codex. Its core philosophy is: **everything is a plugin**.

![](https://pic.yupi.icu/1/image-20260814133452050.png)

In *DeepSeek Harness Beginner-Friendly Tutorial* in this tutorial’s DeepSeek Harness section, I already walked everyone through getting started from scratch, covering installation, hands-on usage, community plugins, and even the basics of writing your own plugin.

Now we’re moving into the advanced part of the series, where I’ll break down DeepSeek Harness’s deeper usage patterns one by one.

This article starts with Agent presets.



## What Is an Agent Preset?

Many AI programming tools support mode switching. If you’ve used Cursor before, then Agent, Ask, and Plan modes should already sound familiar:

![](https://pic.yupi.icu/1/image-20260819094426555.png)

DeepSeek Harness has a similar capability too. Officially, it calls these **Agent presets**.

An Agent preset is basically the complete configuration of which tools the AI can use in a session, what system prompt it follows, and how it works overall. Different preset combinations create AIs with very different working styles.

DeepSeek Harness comes with four built-in presets, corresponding to four runtime modes, and you can switch between them directly from the mode selector above the chat box.

![](https://pic.yupi.icu/1/image-20260814145323400.png)

Choosing the right preset really matters. Writing code, testing, fixing bugs—different tasks are suited to different modes. Pick the wrong one, and you may get half the result for twice the effort.

Let me first walk you through the four built-in modes, and then I’ll show you how to create your own.



## The Four Built-In Modes



### Standard Mode

Standard mode is the default option when you first open DeepSeek Harness.

It loads the full capability set you’d expect from an AI programming tool, including file reading and writing, terminal commands, web search, task planning, Skills, sub-Agents, todo management, and more—over 20 tools in total.

![](https://pic.yupi.icu/1/image-20260818210034485.png)

In the vast majority of cases, standard mode is enough. It has broad enough coverage to handle almost any task you throw at it.

See? In standard mode, DeepSeek Harness actually looks a lot like AI programming tools such as Codex.

![](https://pic.yupi.icu/1/image-20260814143812878.png)

Exactly—just treat standard mode as the domestic version of Codex. AI programming, office automation, and similar tasks can all be handled this way.

But having more tools also comes with a cost. Every time the model takes a step, it first has to choose among more than 20 tools. Just making that choice already consumes part of its reasoning capacity. And all of the tool descriptions are stuffed into the context, which means less attention is left for solving your actual task.

In standard mode, even saying something as simple as “hello” to the AI already consumes more than 10,000 tokens of context!

![](https://pic.yupi.icu/1/image-20260818210415241.png)



### Minimal Mode

Minimal mode is much more stripped down. The official configuration keeps only two tools: a persistent terminal and a file editor. Everything else is turned off.

![](https://pic.yupi.icu/1/image-20260818210623289.png)

Not only are there fewer tools, but the system prompt is also reduced to a single line: `You are a helpful software engineer assistant`. Context compression, task planning, Skills, and sub-Agents are all removed.

If you say the same “hello” to AI, minimal mode only consumes a little over 1,000 tokens—10 times less than standard mode!

With fewer tool manuals in the context, naturally more of the model’s attention can be focused on the task itself.

![](https://pic.yupi.icu/1/image-20260818210911159.png)

In this mode, AI is like a seasoned craftsman who just keeps his head down and works. It doesn’t report progress to you or create fancy plans. It gets the task and starts hacking away immediately.

![](https://pic.yupi.icu/1/image-20260815122619221.png)

The official positioning of this mode is very clear: it is mainly used for model benchmark testing. Strip the environment down to the cleanest possible form and compare different models fairly under the same standard.

DeepSeek V4 Pro’s benchmark results were run using minimal mode. If you look closely at the small note at the bottom of the benchmark image, it says that V4-Pro was tested using DeepSeek Harness minimal mode as the framework.

![](https://pic.yupi.icu/1/HPmOJZlbUAAOgVt-20260818211001128.jpeg)

So what happens if you take this “exam mode” and use it for real work? If you want the full comparison, read *DeepSeek Harness Minimal Mode Evaluation* in this tutorial’s DeepSeek Harness section.



### PTC Mode

PTC stands for **Programmatic Tool Call**.

In standard mode, AI calls tools step by step—execute one tool, then decide what to do next. That means lots of back-and-forth between the model and the tools.

PTC mode changes the approach. Instead of calling tools one at a time, the model directly generates a piece of TypeScript code that chains multiple tool calls together and executes them all in one go.

For example, suppose you want to batch rename 128 photos, and the renaming tool can only handle one photo at a time. In standard mode, AI would need to call the rename tool one image after another, waiting on each round-trip. In PTC mode, AI could just write 5 lines of TypeScript with a loop and rename all 128 files in one execution.

> Note: in reality, standard mode probably wouldn’t literally do it this way either. This is just a simplified example to make the difference easier to understand.

![](https://pic.yupi.icu/1/image-20260818211153120.png)

PTC mode is especially suitable for tasks with many steps but clear logic—for example, batch renaming files or running a long automation process. It is much more efficient than confirming each step one by one.

Interestingly, the configuration difference between PTC mode and standard mode is basically just one line: switching the tool presentation mode from the default `native` to `code`. In essence, it has the full tool capability set of standard mode—the only difference is how the model invokes those tools.

![](https://pic.yupi.icu/1/image-20260818214210342.png)



### Creation Mode

Creation mode is the most special of the four presets.

It inherits all the abilities of standard mode, and on top of that it provides a special set of tools for operating the Cordis plugin system. That allows AI to inspect which plugins are currently running, experiment with new plugin combinations in memory, and even create an entirely new mode preset by itself.

![](https://pic.yupi.icu/1/image-20260819102346095.png)

Put simply, this mode is for transforming DeepSeek Harness itself.

In the beginner tutorial, I used creation mode to develop a desktop-pet plugin for Harness.

![](https://pic.yupi.icu/1/image-20260814135037195.png)

However, creation mode has very high privileges. As the official wording puts it, you should treat its permission scope with the same caution as Shell access.

So for day-to-day work, I don’t recommend leaving this mode on all the time. Only switch into it when you need to develop plugins or customize presets.



## Which Mode Should You Choose?

Now that we’ve gone through all four modes, let’s summarize their core differences.

At the end of the day, these modes are just different combinations of **which tools and configurations are loaded into the current session**.

Minimal mode keeps only two tools. Standard mode equips the full set. PTC mode changes the tool-calling approach. Creation mode additionally lets AI inspect and modify the current plugin configuration.

![](https://pic.yupi.icu/1/image-20260814150646065.png)

Some people in the community previously discovered that switching to minimal mode actually improved model speed and performance on pure coding tasks. So I ran a dedicated experiment using the same 3D shooter game task in both standard and minimal mode.

First, here’s what the standard mode result looked like:

![](https://pic.yupi.icu/1/image-20260815123745988.png)

And here’s the result from minimal mode. The difference in the final product isn’t huge.

![](https://pic.yupi.icu/1/image-202608151243407956.png)

But standard mode took 33 minutes, while minimal mode only took 23 minutes—nearly 10 minutes faster!

That said, minimal mode also has obvious weaknesses: no web search, no context compression, no task planning. The higher your quality expectations are for the finished product, the more likely minimal mode is to disappoint.

For the full comparison review, read *DeepSeek Harness Minimal Mode Evaluation* in this tutorial’s DeepSeek Harness section.

I also ran the same task in PTC mode. It was 7 minutes faster than standard mode, and the whole task only took 1 round with 18 steps—much leaner than standard mode. Token usage was also much lower: input was only 1.5 million tokens, less than one-third of standard mode’s 5.2 million.

Personally, I also think the finished result from PTC mode was the best among the three:

![](https://pic.yupi.icu/1/image-20260818215427583.png)

So the summary is simple: if you care about speed, use minimal mode; if you care about stability, use standard mode; and for step-heavy automation tasks, try PTC mode.



## Custom Agent Presets

Besides the four built-in modes, if you have a specific working habit or frequently perform a certain kind of task, you can create a custom Agent preset tailored for yourself.

For example, Cursor has a very popular Debug mode. It makes AI first generate hypotheses, insert logs, ask you to reproduce the bug, and then use runtime data to locate the root cause. The whole debugging process is methodical.

![](https://pic.yupi.icu/1/image-20260707183325681.png)

That exact workflow can be recreated in DeepSeek Harness.

DeepSeek Harness supports custom presets. You can switch into **creation mode** and ask AI to create the preset you want.

For example, if I want AI to create a “Debug mode,” I only need to provide the official documentation for Cursor Debug mode as reference and ask AI to write a preset based on it.

The prompt can look like this:

```markdown
基于标准模式创建一个自定义 Agent 预设，名称为「Debug 模式」。
要求复刻 Cursor IDE 的 Debug 模式工作方式。
必须参考 Cursor 官方文档来设计：https://cursor.com/docs/agent/debug-mode
```

After submitting the task, you can see that AI automatically loads the preset-editing skill, fetches Cursor’s official Debug mode docs through the terminal, and extracts the core workflow.

![](https://pic.yupi.icu/1/image-20260819105013846.png)

A few minutes later, AI completes the task. It copies the standard-mode preset, then modifies two files: `preset.yml`, which stores the preset’s name and description, and `agent.cordis.yml`, which defines the Agent’s tools and persona. Into those files, it writes the six-step Debug mode workflow and the hard rules.

![](https://pic.yupi.icu/1/image-20260819105116895.png)

After creation, you can see the new custom “Debug Mode” in the mode selector.

![](https://pic.yupi.icu/1/image-20260819114556459.png)

In the future, when you hit difficult bugs that can be reproduced but whose cause is unclear, just switch to this mode. AI will then investigate using the flow **hypothesis → instrumentation → reproduction → analysis → fix → cleanup**, which is much more reliable than letting AI randomly patch things based only on prior experience.

![](https://pic.yupi.icu/1/image-20260819114746666.png)



## More Ways to Use It

You can use the exact same approach to recreate all kinds of specialized modes.

For example, create a **code review mode** that only performs review without making changes, checking code from the perspectives of security, performance, and readability, and then outputting a review report.

Or create a **documentation mode** that focuses only on writing code comments, generating API docs, and updating the `README` project documentation.

Or even create a **refactoring mode**, where AI first analyzes redundant code and duplicated logic in the project, then creates a refactoring plan, and finally executes it step by step—only moving on after the tests pass at each stage.

At its core, a custom preset is simply a fixed **working SOP** for AI. You write your best practices for handling a certain type of task into the system prompt, and then AI follows that process every time. If you’ve used `AGENTS.md` or `CLAUDE.md` before, this should feel familiar—it’s the same idea: use configuration files to constrain how AI behaves.



## Final Words

Agent presets are one of the most practical features in DeepSeek Harness. Choosing the right mode can easily double your work efficiency.

For everyday development, standard mode is usually enough. For pure coding tasks where speed matters, switch to minimal mode. For batch automation tasks, try PTC mode. And when you need to develop plugins or customize presets, use creation mode.

If you often do a certain type of repetitive task, I strongly recommend spending a few minutes creating a custom preset for it. Configure once, benefit for a long time.

If you want to explore more advanced DeepSeek Harness usage, keep reading the other articles in this tutorial’s DeepSeek Harness section.
