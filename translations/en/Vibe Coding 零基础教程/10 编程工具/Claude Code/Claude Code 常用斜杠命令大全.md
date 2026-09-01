# Claude Code Common Slash Commands: Use Them Well and Double Your Efficiency!

More and more people are using Claude Code now, but I’ve noticed that many still use it like a pure chat tool—they just type their needs directly in natural language every time.

That’s not wrong. AI models are already very capable and can generally understand what you mean.

But Claude Code actually has a lot of built-in slash commands. Type `/` and you’ll see the full command list. These commands cover session management, context control, parallel collaboration, and more. If you use them well, they can save you a lot of work.

![](https://pic.yupi.icu/1/image-20260519171514784.png)

Although Claude Code already has more than 50 commands, you don’t need to memorize them. In day-to-day use, you can simply tell Claude your needs in plain language—for example, “compress the context,” “switch to planning mode,” or “run this task in the background”—and it will often execute the corresponding command automatically.

But understanding what these commands are, what they’re used for, and when to use them helps you understand Claude Code’s capability boundaries, open up your thinking, and work more efficiently.

Below, I’ll go through the common commands by category and explain what each one is, how to use it, and when it makes sense.

Where demonstrations are helpful, I’ll provide demo prompts that you can directly try in Claude Code.

Save this article and let’s begin~

💡 If you haven’t used Claude Code yet, take a look at [this practical tutorial of mine](https://mp.weixin.qq.com/s/PHPtZcS2sX62O3Szj-mWsw), where I walk you through setting it up and building a complete project.



## Claude Code Slash Commands Encyclopedia

### 1. Session Management

#### /clear

Clears the current conversation and starts a brand-new session.

When you’ve finished one task and **need to switch to another**, `/clear` removes all previous context so old information doesn’t interfere with the new task.

The cleared conversation is not lost. You can still recover it later using `/resume`.

![](https://pic.yupi.icu/1/image-20260519172239175.png)

One thing to note: if you only feel that the context is getting too long but you’re still working on the same task, don’t use `/clear`. In that case, `/compact`, which I’ll explain next, is the better choice.



#### /compact

Compresses the current conversation to free up context space.

Claude Code’s context window is limited. As the conversation gets longer, it eventually fills up. Once the context nears its upper limit, AI’s attention starts to scatter, it becomes easier for it to miss earlier details, and answer quality drops noticeably.

`/compact` condenses the earlier conversation into a summary, freeing space to keep working while preserving the key information. After compression, there are fewer turns in the conversation, and each future request sends fewer tokens too—so it indirectly saves you money.

![](https://pic.yupi.icu/1/image-20260519192717120.png)

Claude Code will automatically trigger compression when context usage reaches around 95%, but I don’t recommend waiting that long. The timing of automatic compression is out of your control, and it may happen right when you’re implementing some key logic, which can cause important details to get compressed away.

A better habit is to proactively run `/compact` after each major stage is completed—for example, after debugging a bug or finishing a feature—so that you can better control what information gets preserved.

You can also append a short instruction telling it what to focus on while compressing.

For example, if you’re designing APIs, you can do this:

```bash
/compact 重点保留 API 接口的设计决策和参数定义
```

![](https://pic.yupi.icu/1/image-20260519172504841.png)

My own habit is to run compact once `/context` shows that usage has gone beyond 80%.



#### /resume

Restores a previous session.

If you want to continue a half-finished task from yesterday, or revisit a conversation you just cleared with `/clear`, use `/resume`.

After you enter it, a session picker will pop up, listing all your recent sessions. Choose one and it will be restored.

![](https://pic.yupi.icu/1/image-20260519172815216.png)

By default, it only shows sessions from the current workspace (project directory). If you want to view the history across all projects, press `Ctrl+A` to switch to the full list.

![](https://pic.yupi.icu/1/image-20260519172945037.png)

If you remember the session name or ID, you can specify it directly:

```bash
/resume 昨天的重构任务
```



#### /branch and /fork

These two commands do the same thing: they branch off a new session from the current conversation.

When you want to explore another direction based on the current discussion, but don’t want to disturb the progress of the current conversation, this is exactly what they’re for.

After executing one of them, you’ll switch to a new branch while the original conversation remains untouched. You can go back at any time with `/resume`.

For example, if you are discussing an architecture plan and want to try another implementation idea, but you’re worried you may lose track of the original one, you can `/branch` first, explore, and come back if needed.

```bash
/branch 试试用 Redis 替代内存缓存的方案
```

![](https://pic.yupi.icu/1/image-20260519173209261.png)



#### /rewind

Rolls back both the conversation and the code to a previous checkpoint.

Claude automatically saves checkpoints during work. In other words, every state before you press Enter to let it execute something is recorded.

If Claude changed a lot of code but you feel it went in the wrong direction, `/rewind` lets you jump back to any previous checkpoint, rolling back both the conversation history and the file changes together.

After execution, a checkpoint picker pops up. You simply choose where you want to rewind to.

![](https://pic.yupi.icu/1/image-20260519173628854.png)

You can think of it like Undo in Word, or version rollback in Git. It rewinds both the conversation and the file modifications together.



#### /recap

Generates a one-sentence summary of the current session.

If you step away for a while and come back forgetting where you left off, `/recap` gives you a quick reminder.

Claude Code will also automatically show a recap when you return after being away for a long time. This command just lets you trigger one manually whenever you want.

![](https://pic.yupi.icu/1/image-20260519174322674.png)



#### /btw

`btw` is short for “by the way.” It lets you quickly ask a side question **without polluting the current conversation context**.

Sometimes while working on a task, you suddenly want to ask something only loosely related—like: how do you set default values in a Python dataclass again?

If you ask directly, that piece of conversation gets added to the context. It takes up space and may interfere with the later task.

With `/btw`, that doesn’t happen. It’s like opening a temporary little side window, asking your question, and then closing it:

![](https://pic.yupi.icu/1/image-20260519174229758.png)



#### /copy

Copies Claude’s most recent reply to the clipboard.

Typing `/copy` by itself copies the latest response.

![](https://pic.yupi.icu/1/image-20260519174511609.png)

If the reply contains code blocks, a selector appears so you can choose which block to copy.

![](https://pic.yupi.icu/1/image-20260519174550215.png)

You can also add a number to copy the Nth most recent reply. For example, `/copy 2` copies the second most recent reply.

![](https://pic.yupi.icu/1/image-20260519174717159.png)

This feature is simple, but I find it very useful, because selecting and copying directly in the terminal often causes trouble.



#### /export

Exports the entire current conversation as a plain text file.

If you want to save a conversation record or share it with a coworker, use this command. By default, it asks whether you want to copy to clipboard or save to a file.

![](https://pic.yupi.icu/1/image-20260519174853832.png)

If you add a filename after the command, it saves directly:

```bash
/export 开发记录.txt
```

![](https://pic.yupi.icu/1/image-20260519174946874.png)



#### /exit

Nothing fancy here—it exits the Claude Code session. Pressing `Ctrl+C` twice also works.

![](https://pic.yupi.icu/1/image-20260519175031641.png)

But there is one detail to note: if subagents or background tasks are still running, Claude Code will ask whether you also want to close them when you exit.



### 2. Information and Diagnostics

#### /usage

Shows the token usage and estimated cost for the current session.

The scariest thing about using Claude Code is silently burning money without noticing. `/usage` tells you how many tokens this session has used, how much that roughly translates to in USD, and how far you still are from your plan’s usage limit. It’s a good idea to check it periodically during long working sessions.

![](https://pic.yupi.icu/1/1777359631006-6a630d28-fda7-426d-9b7d-e188b8fdf9b5.png)

That said, one caveat: if you connect Claude Code to a third-party model via API Key (for example, a domestic model like DeepSeek), `/usage` may not display the cost accurately, because it estimates using Claude’s official pricing. For the real cost, always trust the billing page of your actual model provider.



#### /context

Visualizes how your current context window is being used.

After running it, you’ll see a color grid that intuitively shows what is filling the context space—is it the conversation history, too many loaded files, or an overly large system prompt? If it’s close to full, it will even give optimization suggestions.

![](https://pic.yupi.icu/1/1777358465249-dbc18a92-6c77-471d-a15e-4f79a7837a67-20260429113526400.png)

If you add `all`, it expands the detailed information for each item:

```bash
/context all
```

![](https://pic.yupi.icu/1/image-20260519175443232.png)

I usually use it together with `/compact`: first inspect the context pressure with `/context`, then decide whether it’s time to compact.



#### /diff

Opens an interactive diff viewer so you can see exactly what Claude changed.

This command shows all current uncommitted code changes. You can use the left and right arrow keys to switch between the overall Git diff and Claude’s individual round-by-round changes, and use the up and down arrow keys to browse different files.

![](https://pic.yupi.icu/1/image-20260519175542291.png)

After Claude has modified many files, it’s a good habit to run `/diff` before committing. But honestly, reading diffs inside a black terminal window is still painful. If the changes are large, I recommend combining it with VS Code’s Git extension or another IDE with visual diff support.



#### /status

Opens the status tab of the settings interface, showing the current version, selected model, account info, and connection status.

![](https://pic.yupi.icu/1/image-20260519175729482.png)

One nice thing about this command is that you can use it even before Claude finishes its current reply. If Claude is running a very long task, you can type `/status` anytime to check what’s going on.



#### /help

Displays a list of all available commands and a short description of each. Whenever you forget a command, just run `/help`.

![](https://pic.yupi.icu/1/image-20260519175817191.png)

This is actually a common command-line convention. Almost every CLI tool supports `--help` or some equivalent command. Build the habit now: when you encounter an unfamiliar command-line tool later, type help first and see what it can do.



#### /insights

Generates an analysis report about how you use Claude Code, including which project directories you work in most often, what your interaction patterns look like, and where problems tend to appear.

If you want to reflect on your AI programming habits and find room for improvement, it’s worth running from time to time.

![](https://pic.yupi.icu/1/image-20260519180603438.png)

The generated report is in English by default. You can feed that report file back into AI and ask it to analyze and summarize it further for you.

![](https://pic.yupi.icu/1/image-20260519180701112.png)



#### /doctor

Runs a health check on your project configuration. It also has the alias `/checkup`.

It automatically scans your Skills, `CLAUDE.md`, and other configuration files to see whether they contain redundant information that the model could already infer from the repo, such as directory structure or dependency lists. It can also find unused Skills and MCP services, detect duplicated or conflicting `CLAUDE.md` rules between your local environment and the repo, and suggest moving content that doesn’t need to be loaded every time into on-demand Skills.

![](https://pic.yupi.icu/1/1785830100705-ba0f3f43-ba78-43e0-bf59-5dabcf2f2c61.png)

It will always show you a report first and only make changes after your confirmation, so you don’t need to worry about it messing up your config on its own.

This command was introduced alongside the “prompt subtraction” mindset for newer models, because the official team found that too many rules actually distract the model from doing the real work. If you want to understand the principle behind that, read *Anthropic’s Official Prompt Simplification Method* in the practical tips section of this tutorial.



### 3. Model and Mode Control

#### /plan

When developing a full-stack project or making a large change, I don’t recommend letting AI jump directly into writing code.

Using `/plan` enters planning mode, where AI first creates an execution plan for you to review. Once the plan looks good, it starts implementing.

You can directly describe the task after the command:

```bash
/plan 重构整个项目，增加用户系统和 JWT 认证
```

![](https://pic.yupi.icu/1/image-20260519180528043.png)

AI may ask interactive follow-up questions to confirm more details:

![](https://pic.yupi.icu/1/image-20260519180823098.png)

Then it outputs a detailed implementation plan. Only after you confirm it does it begin execution. This is ideal for large-scope tasks or tasks where the best solution isn’t obvious yet.

![](https://pic.yupi.icu/1/image-20260519181940794.png)



#### /goal

This is what I personally consider the most powerful Claude Code command at the moment.

Normally, after each round of work, Claude Code stops and waits for your confirmation or next instruction.

But for some tasks, you don’t actually need to watch it step by step. You only care about **what final state counts as complete**, and want it to keep grinding until it gets there. It’s especially suitable for giving Claude a task before going to bed and then checking the result the next morning.

That’s what `/goal` is for. You define a completion condition, and Claude Code keeps working automatically without needing you to press Enter every round. Once a goal is set, a lightweight evaluation model checks after each round whether the condition has been met. If not, Claude automatically starts the next round. It only stops when the goal is satisfied.

Let’s first look at the basic usage. Suppose I want Claude Code to fix the whole project:

```bash
/goal 修复整个项目的代码，直到全部测试通过且没有报错
```

After you run it, Claude immediately gets to work and keeps going until all tests pass and there are no errors, without any intervention from you.

![](https://pic.yupi.icu/1/image-20260519191842661.png)

But whether this command works well depends on how you write the completion condition. The evaluator only reads what appears in the conversation—it does not run commands by itself. So your condition must be something Claude Code can demonstrate through its own execution process, such as the result of a specific command.

Here are a few examples:

- ✅ `npm test` exits with code 0, and `git status` shows no uncommitted changes  
- ✅ there are no more TODO comments under `src/`  
- ❌ code quality should be good

If the condition is poorly written, or the task itself is hard to converge, Claude may loop forever and keep burning tokens. So I recommend adding a circuit breaker to the condition, for example:

```bash
/goal 把所有 API 调用迁移到 v2 格式，直到测试通过，如果 20 轮还没搞定就停下来
```

That way, even if the task fails to finish, it will stop after 20 rounds.

Although the goal command is powerful, it can consume a lot of tokens because it may run many rounds automatically. So it isn’t suitable for every task. It’s best used when there is a clear stopping condition and manually babysitting the task would be tedious. For example:

- module migration: migrate all old API calls to a new version until compilation passes  
- batch refactoring: split large files until each file stays under a specified line count  
- bug fixing: fix a failing test case until it turns green  
- backlog cleanup: process all issues with a certain label until none remain

If you want to check progress midway, just type `/goal` without arguments and it will show you how long the task has been running and how many tokens it has consumed.

![](https://pic.yupi.icu/1/image-20260519192117090.png)

If you want to stop it early, use `/goal clear`.

![](https://pic.yupi.icu/1/image-20260519192203259.png)



#### /model, /effort, /fast

These three commands all control model behavior, so I’ll talk about them together briefly.

- `/model` switches the AI model and opens a selector for you to choose from  
- `/effort` adjusts how hard the model thinks, from `low` to `max` across five levels. Lower it for simple tasks to save tokens, and raise it for complex tasks. I usually keep it at `high` or `xhigh`.  
- `/fast` toggles fast mode. When enabled, the response speed becomes about 2.5 times faster without lowering quality. But the token unit price is higher, so it’s suitable for simple changes that need quick iteration. For long complex tasks, it’s usually not worth turning on. Personally, I’m too poor to leave it on all the time anyway (

![image-20260519181459065](https://pic.yupi.icu/1/image-20260519181459065.png)

In general, most people don’t really need to use these commands much. I personally rarely adjust them by hand. If you want an easier experience, try the open-source CC Switch tool, which gives you a visual interface for switching models and tuning parameters.

![](https://pic.yupi.icu/1/image-20260519181417445.png)



### 4. Configuration and Extensions

#### /config

Opens Claude Code’s settings interface, where you can adjust preferences such as theme, model, output style, and more.

It’s basically a master control panel. If you can’t remember a specific command, you can just go into `/config` and look around. It also supports searching configuration items.

![](https://pic.yupi.icu/1/image-20260519181629699.png)



#### /mcp, /skills, /plugin

These three commands are used to manage MCP server connections, Skills lists, and plugins respectively.

MCP is the protocol that lets AI connect to external tools and services, such as databases or browsers.

Skills are reusable custom commands. You can package a common workflow into a skill so you can complete the same kind of task more quickly and consistently next time.

A Plugin can be understood as a packaged collection of capabilities—it may include multiple skills, custom themes, hooks, and more, making it easier to share and install.

I don’t use these commands very often myself. In most cases, you configure them once and rarely touch them again. If command-line management feels too abstract, tools like CC Switch can also provide visual management for MCP, Skills, and plugin configuration.

![](https://pic.yupi.icu/1/image-20260519181902887.png)



### 5. Code Review

#### /review

Asks Claude to review the Pull Request corresponding to the current branch.

Once you enter `/review`, AI automatically detects the PR associated with the current branch and starts the review:

![](https://pic.yupi.icu/1/image-20260519182317653.png)

You can also specify a PR number to review a specific PR:

```bash
/review 42
```

During the review, Claude launches multiple subagents in parallel to inspect the code, focusing mainly on bugs and logic errors. It’s a good fit for running your own AI review before asking coworkers to review or before merging.

![](https://pic.yupi.icu/1/image-20260519182358586.png)

If you want a deeper cloud-based multi-agent review, you can try `/ultrareview`, but that consumes additional usage credits. Pro and Max users get 3 free uses.



#### /simplify

Although the command is called simplify, what it does is not limited to simply simplifying code.

Its core job is to review your recently modified files and directly fix issues from three angles: code reuse (whether there is duplicated logic that can be extracted), code quality (whether there are hacky implementations or redundant state), and execution efficiency (whether there are unnecessary calculations or places where concurrency could be used).

It’s probably called simplify because after working through those three areas, the code really does become more concise.

Unlike `/review`, `/simplify` doesn’t just give you suggestions—it directly modifies the code. It launches three review agents in parallel, one for each of the three perspectives mentioned above, then aggregates the issues and applies fixes.

![](https://pic.yupi.icu/1/image-20260519183027485.png)

You can also append a short description to make it focus on a particular direction:

```bash
/simplify 重点关注内存效率
```

![](https://pic.yupi.icu/1/image-20260519183241226.png)



### 6. Subagents and Parallelism

#### /agents

Claude Code can delegate some subtasks to subagents to run in parallel. The `/agents` command lets you view and configure those subagents.

However, for most people, there’s no need to configure them manually. Claude Code automatically enables them when needed. This command is more for checking which agents are currently running and what their status is.

![](https://pic.yupi.icu/1/image-20260519183337674.png)



#### /tasks

Views and manages the background tasks currently running in the session.

When Claude executes complex operations, it may launch multiple subagents in parallel to handle different subtasks. `/tasks` lets you see what each one is doing and how its progress looks.

![](https://pic.yupi.icu/1/image-20260519183357190.png)

If you select a task and press Enter, you can even inspect the full execution process and detailed output of that subagent:

![](https://pic.yupi.icu/1/image-20260519183444151.png)



#### /background

Pushes the current whole session into the background so your terminal is freed up.

I think this is pretty practical. For example, if I’ve told Claude to run a long task—like refactoring a large module—and I don’t want to keep the terminal open waiting for it, I can throw it into the background with `/background`.

After executing it, the current session detaches from the terminal and continues running in the background, leaving your terminal free for other things. Later, if you want to check the progress again, you can attach back to it.

You can also add one last instruction before detaching:

```bash
/background 编写单元测试并运行，执行失败则自动修复
```

![](https://pic.yupi.icu/1/image-20260519183834248.png)

Later, if you want to check progress, use the `claude agents` command to monitor the status of all background sessions.

![](https://pic.yupi.icu/1/image-20260519183917357.png)

Select a background session and press the right arrow key to enter its conversation view:

![](https://pic.yupi.icu/1/image-20260519184129719.png)



#### /loop

With `/loop`, you can set a time interval so Claude performs an operation periodically—in other words, a scheduled task.

For example, check every 5 minutes whether frontend and backend deployment has finished:

```bash
/loop 5m 检查项目前后端的部署状态
```

![](https://pic.yupi.icu/1/image-20260519184353594.png)

If you don’t specify an interval, Claude decides the rhythm based on the task. If you don’t even specify a prompt, it reads the contents of `.claude/loop.md` in the project and executes that instead (if the file exists). If there is no such file, it performs one round of autonomous maintenance checking.

This is suitable for scenarios that need ongoing monitoring, such as waiting for deployment to finish, waiting for CI to complete, or periodically checking whether logs contain anomalies.

Personally, though, I don’t like using `/loop` for long-running scheduled tasks. If you set one and forget to turn it off, it can keep running in the background forever and quietly consume resources.



## Final Rambling

Those are the slash commands I use most often in my day-to-day work with Claude Code.

Let me emphasize again: you do **not** need to memorize them. It’s enough to read through them once and leave yourself a general impression. When you need one, just type `/` and search. And as I mentioned earlier, for most operations you can simply describe the task in Chinese and let Claude execute it—it usually knows which command to use.

In the AI era, it’s time to lighten the burden on your own brain a bit~



## Final Words

This article sorted out the most commonly used slash commands in Claude Code by category—from session management and context control to subagent collaboration—so you can get a full picture of Claude Code’s capability boundaries.

Once you learn these, you’ll be able to use Claude Code more efficiently and save a lot of time and energy in day-to-day development.

If you want to continue learning more practical AI programming techniques, you can read the other articles in the practical tips section of this tutorial.
