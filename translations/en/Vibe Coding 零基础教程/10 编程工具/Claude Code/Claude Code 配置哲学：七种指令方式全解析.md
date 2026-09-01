# Claude Code Configuration Philosophy: Anthropic Officially Teaches You How to “Steer” AI

> Anthropic officially teaches you how to “train” Claude Code

Hello everyone, I’m programmer Yupi.

Recently, Anthropic published an official blog post titled *Steering Claude Code*, which explains Claude Code’s entire configuration system—from the underlying logic to real usage scenarios—in a very thorough way.

Since it was written by the official team itself, it’s basically like the person who wrote the exam handing you the answer key. So the practical value of the article is extremely high.

Today I’m going to combine the official content with my own experience using Claude Code and give everyone a complete Chinese-style breakdown.

> Original article: https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more

![](https://pic.yupi.icu/1/image-20260625173136998.png)



## Ways to Steer Claude Code

There are seven ways to steer Claude Code: the `CLAUDE.md` file, Rules, Skills, Subagents, Hooks, Output Styles, and Append System Prompt.

The core differences between these methods come down to three things:

1. When they get loaded into context  
2. Whether they get dropped during long-conversation compression  
3. How many tokens they consume

If you put instructions in the wrong place, AI may ignore them entirely, wasting your tokens for nothing.

Let’s go through them one by one.

![Overview of Claude Code's seven steering methods](https://pic.yupi.icu/1/01_%E4%B8%83%E7%A7%8D%E8%B0%83%E6%95%99%E6%96%B9%E5%BC%8F%E6%80%BB%E8%A7%88%E5%AF%B9%E6%AF%94%E5%9B%BEv2_compressed_v1.png)



## 1. `CLAUDE.md` — The Project Handbook for AI

`CLAUDE.md` is a Markdown file placed in the project root directory. It is loaded at the start of a session and stays resident in the context for the entire conversation.

So what kind of content belongs in `CLAUDE.md`?

Things like build commands, directory structure, coding conventions, and team agreements—factual information that AI needs to **remember at all times**.

In my [AI Programming Tutorial](https://ai.codefather.cn/vibe), I’ve emphasized many times that `CLAUDE.md` is like the project documentation you’d write for a new teammate. You don’t need to explain the tech stack or project rules to AI every single time. Write it once, and it keeps working.

There are two ways `CLAUDE.md` gets loaded.

The root-level `CLAUDE.md` is always loaded, and it will even be reread after context compression, so it won’t get lost.

Subdirectory `CLAUDE.md` files—such as `app/api/CLAUDE.md`—are only loaded when Claude reads files under that directory. That makes them suitable for conventions that apply only to a specific module.

![CLAUDE.md loading mechanism](https://pic.yupi.icu/1/02_CLAUDE.md%E5%8A%A0%E8%BD%BD%E6%9C%BA%E5%88%B6v2_compressed_v3.png)

Anthropic explicitly recommends keeping `CLAUDE.md` **within 200 lines whenever possible**.

The reason is simple: every line in `CLAUDE.md` consumes tokens, whether the current task needs it or not.

If you stuff 500 lines into it, then even for a tiny frontend style tweak, AI still has to load all your backend deployment rules too. That’s pure waste.

I’ve personally fallen into this trap. I used to dump everything into `CLAUDE.md`, and later I noticed that AI’s instruction-following got noticeably worse, especially in long conversations. Once I trimmed it down and moved process-oriented content into Skills, the improvement was immediate.

So just remember one principle: **put “facts” in `CLAUDE.md`, not “processes.”**

![Facts vs. processes comparison](https://pic.yupi.icu/1/03_%E4%BA%8B%E5%AE%9Evs%E6%B5%81%E7%A8%8B-CLAUDE.md%E5%86%85%E5%AE%B9%E5%88%86%E7%B1%BB%E5%AF%B9%E6%AF%94_compressed_v1.png)

Build commands, tech stack, directory structure, and naming conventions are facts. Deployment procedures, code review checklists, and release steps are processes, and should be packaged as Skills.



## 2. Rules — Precise Path-Level Constraints

Rules are Markdown files placed in the `.claude/rules/` directory and are used to define specific constraints or coding conventions for Claude.

Their most powerful feature is support for path-based scope. If you add a `paths` field at the top of the rule file, the rule will only take effect when Claude reads files under those specific paths.

For example, I might have a rule saying “all API handlers must use Zod for input validation,” and I scope it to `src/api/**`. That way, if I’m only editing frontend pages, the rule won’t even load, which means no wasted tokens.

```yaml
---
paths:
  - "src/api/**"
  - "**/*.handler.ts"
---
所有 API 处理器必须使用 Zod 进行输入验证。
```

That’s exactly how I use it in my own projects. I scope database-related rules to `src/db/**`, frontend rules to `src/components/**`, and let each area handle its own business.

So when should you use a Rule instead of a subdirectory `CLAUDE.md`?

The answer is: when one convention needs to apply **across multiple directories**.

For example, if all `.test.ts` files must follow a certain testing rule, then a path-scoped Rule is more appropriate. A subdirectory `CLAUDE.md` can only govern files under that one directory.



## 3. Skills — Workflows Loaded on Demand

Skills live under `.claude/skills/`, where each skill is a folder whose core file is a `SKILL.md` description.

The progressive loading design of Skills is extremely elegant. At the start of a session, Claude only reads each Skill’s name and short description. The full skill content is loaded into context **only when it is triggered**.

![Skills progressive loading design](https://pic.yupi.icu/1/04_Skills%E6%B8%90%E8%BF%9B%E5%BC%8F%E5%8A%A0%E8%BD%BD%E8%AE%BE%E8%AE%A1%E5%9B%BEv2_compressed_v3.png)

That means you can define dozens of Skills without them consuming many tokens in normal use. Only when you explicitly call one—such as typing `/code-review`—or when AI automatically matches the task to a needed Skill, does the full instruction content get loaded.

In my `.claude/skills/` directory, I keep things like deployment procedures, code review checklists, standard steps for creating new components, and so on. If all of that were placed in `CLAUDE.md`, then even if you only said “hello,” you’d waste who-knows-how-many tokens. With Skills, they load only when needed.

There’s another important detail. During conversation compression, already triggered Skills get reinjected according to an overall budget. If the budget isn’t enough, the earliest triggered Skills get discarded first. So don’t trigger too many Skills in a single session—stay focused on what matters most for the current task.



## 4. Subagents — Isolated Independent Assistants

Subagents live under `.claude/agents/`, with each file defining an independent AI assistant.

The biggest difference between Subagents and Skills is that a Subagent runs in its own isolated context window. Only the final result is returned to the main conversation. None of the intermediate process consumes your main conversation context.

![Subagents isolated context execution mechanism](https://pic.yupi.icu/1/05_Subagents%E9%9A%94%E7%A6%BB%E4%B8%8A%E4%B8%8B%E6%96%87%E8%BF%90%E8%A1%8C%E6%9C%BA%E5%88%B6%E5%9B%BEv2_compressed_v1.png)

What kinds of scenarios are suitable for Subagents?

For example: deeply searching a codebase for the root cause of a bug, analyzing log files to locate a performance bottleneck, or performing dependency audits to check which packages have security vulnerabilities. These kinds of tasks can generate tens of thousands of tokens of intermediate content. If all of that is piled into the main conversation, the context will blow up quickly.

Subagents can also be nested up to 5 levels deep. Combined with dynamic workflows, that allows you to orchestrate dozens or even hundreds of background Agents in parallel.

I previously used Claude Code’s `/batch` command to migrate API versions in bulk. Under the hood, that was essentially Subagents at work. It automatically split the job into more than ten subtasks, each running in its own isolated worktree without interfering with the others.

So how do you choose between Skills and Subagents?

Very simply: if you want to **see the execution process** and be able to intervene at any time, use a Skill. If you only care about the final result and don’t want the intermediate noise, use a Subagent.



## 5. Hooks — Deterministic Automation

Hooks are the most special of the seven methods.

The things we discussed earlier—`CLAUDE.md`, Rules, and Skills—are all essentially **suggestions** to the AI. The AI may follow them or may not, especially in long conversations or complex scenarios.

Hooks are different. They are not instructions, but automation code. **Once the trigger condition is reached, they will definitely run.** AI does not get to decide whether to do it.

Hooks are registered through `settings.json` and bound to specific lifecycle events in Claude Code, such as before tool usage (`PreToolUse`), after tool usage (`PostToolUse`), or before context compression (`PreCompact`).

![Hooks lifecycle event triggers](https://pic.yupi.icu/1/06_Hooks%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E4%BA%8B%E4%BB%B6%E8%A7%A6%E5%8F%91%E5%9B%BEv2_compressed_v2.png)

The classic use case is automatically running Prettier after every file edit.

If you put that requirement in `CLAUDE.md`, AI will probably follow it most of the time, but it may also forget.

With a Hook, there’s no such problem. The moment a file is edited, Prettier runs automatically, completely independent of the model.

And Hooks have nearly zero context cost, because their configuration does not sit inside the main context at all.



### “Never do X” Is Not Safe Enough as an Instruction

This is the point from the official article that I think is the most worth remembering.

You can write in `CLAUDE.md`, “Never delete database migration files,” and Claude will obey most of the time. But in long conversations, during context compression, or when encountering prompt injection from some file, AI can still violate that instruction.

A real security boundary needs **Hooks + permissions** working together. For example, you can use a `PreToolUse` Hook to inspect every tool call, and if it detects an attempt to delete a database migration file, it can directly block it with exit code 2. Then combine that with Managed Settings to enforce organization-level restrictions on certain actions. That’s how you actually make it safe.

This mindset is very similar to the fail-closed design I previously saw when analyzing Claude Code’s source. Internally, Claude Code’s tool system treats all tools as “dangerous operations” by default unless the tool explicitly declares itself read-only.

**You cannot rely on AI’s self-discipline for security.**

![Instructions vs. hooks security comparison](https://pic.yupi.icu/1/07_%E6%8C%87%E4%BB%A4vs%E9%92%A9%E5%AD%90-%E5%AE%89%E5%85%A8%E9%98%B2%E7%BA%BF%E5%AF%B9%E6%AF%94%E5%9B%BE_compressed_v3.png)



## 6. Output Styles and Append System Prompt

I personally use these last two less often, so I’ll cover them together.

Output Styles are used to define Claude’s output style and behavior mode. They live in the `.claude/output-styles/` directory, get injected into the system prompt, and are never lost during compression.

But there’s one very important caveat: a custom output style **replaces** Claude Code’s default system prompt.

That means all of Claude Code’s built-in key behaviors—how it determines modification scope, when it adds comments, how it handles security issues, and so on—will disappear once you replace the default prompt.

So Anthropic’s recommendation is to first check whether the built-in styles are enough for you, and not rush into creating custom ones. Right now there are three built-in modes: **Proactive**, **Explanatory**, and **Learning**, which already cover most use cases.

![](https://pic.yupi.icu/1/image-20260625182514344.png)

Append System Prompt is another way to adjust Claude’s behavior. It lets you temporarily append a piece of instruction without modifying any files.

You use it through the CLI parameter `--append-system-prompt`, and it only applies to that one invocation.

The difference from Output Style is that it **appends rather than replaces**, so it doesn’t affect Claude Code’s default behavior. It’s suitable for lightweight temporary needs such as adjusting tone or output format.

![](https://pic.yupi.icu/1/image-20260625182914705.png)

However, the official article also mentions a limitation: the more appended instructions you add, the lower the model’s compliance with each one tends to become, especially when the instructions conflict.



## When Should You Use Which One?

After seeing all seven methods in one shot, you may feel a little dizzy.

That’s okay. The official team gave a few decision guidelines, and it’s enough just to remember the general idea.

![Decision flow for choosing configuration methods](https://pic.yupi.icu/1/08_%E9%85%8D%E7%BD%AE%E6%96%B9%E5%BC%8F%E9%80%89%E6%8B%A9%E5%86%B3%E7%AD%96%E6%B5%81%E7%A8%8B%E5%9B%BE_compressed_v3.png)

First: put **facts** in `CLAUDE.md`, and put **processes** in Skills.

If your `CLAUDE.md` contains more than 30 lines of step-by-step procedural content—such as a deployment runbook or a security review checklist—it should be moved into `.claude/skills/`.

Second: if your need looks like “after every X, do Y,” then you should use a Hook, not an instruction.

For example, running Prettier after every edit, checking lint before every commit, or sending a Slack notification after a task is completed. These things should not depend on AI’s memory. A model deciding to do something and something happening automatically are two entirely different concepts.

Third: for hard rules like “absolutely never do X,” you need the double protection of Hooks plus permissions.

Instructions alone can only make AI obey most of the time. A real safety boundary must be enforced through deterministic mechanisms. It’s the same principle as programming—you wouldn’t rely on comments to prevent a function from being misused. You’d rely on the type system and permission checks.



## My Practical Experience

Let me also share a few personal lessons from configuring Claude Code.

First, `CLAUDE.md` should be written with an **index mindset**. Don’t treat it like an encyclopedia. Treat it like a table of contents. Tell Claude the project basics, then point it to more detailed files.

For example, you can write: frontend component conventions are in `docs/FRONTEND.md`, and the deployment process uses the `/deploy` skill.

That way, `CLAUDE.md` stays concise, and Claude can read the more detailed files only when needed.

![Progressive disclosure and on-demand loading](https://pic.yupi.icu/1/06_%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8A%AB%E9%9C%B2%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v2.png)

Then there are Skills, which I think are currently one of the most underrated features. I’ve now packaged many repetitive workflows into Skills—things like AI trend collection, animated video production, and image-and-text content creation workflows.

I mostly use Subagents for research-oriented tasks, such as investigating whether a library has alternatives, gathering information, or analyzing the cause of a bug. These tasks have long intermediate processes, but in the end you only need one conclusion. Subagents keep the main conversation clean. That said, many AI tools today can already create and manage Subagents automatically.



## Final Words

Claude Code’s configuration system is designed with a lot of care: facts and processes are separated, on-demand loading reduces cost, deterministic guarantees are better than probabilistic instructions, and isolated execution prevents context pollution.

Whether you want to use Claude Code deeply or build your own AI Agent system, these design ideas are worth studying carefully.

By the way, here’s one more thing that supports this design philosophy: after releasing a new model, Anthropic cut more than 80% of Claude Code’s system prompt, yet its programming benchmark scores didn’t drop at all. What they cut away was exactly the kind of content that should either be left to the model’s own judgment or turned into on-demand-loaded material. If you want to learn more about this “prompt subtraction” approach, you can read *Anthropic’s Official Prompt Simplification Method* in the practical tips section of this tutorial.
