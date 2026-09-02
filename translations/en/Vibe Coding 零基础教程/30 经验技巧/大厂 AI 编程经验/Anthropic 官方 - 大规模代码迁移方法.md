# Anthropic Official - Method for Large-Scale Code Migration

> Learn Anthropic’s official six-step migration method and use AI to complete large-scale code migrations efficiently

Hello everyone, I’m programmer Yupi.

A few days ago, Anthropic published [a blog post](https://claude.com/blog/ai-code-migration) explaining how they internally use Claude Code to run large-scale code migrations.

This article is incredibly valuable, because the two case studies in it are absolutely mind-blowing!

![](https://pic.yupi.icu/1/image-20260720133130758.png)

In the first case, Jarred Sumner, the founder of Bun—a hugely popular tool in the frontend world, and now also an Anthropic engineer—used Claude Code to rewrite Bun from Zig to Rust. A full 530,000 lines of code were migrated in just 11 days, then merged and launched after passing tests 100%.

In the second case, Mike Krieger, co-head of Anthropic Labs, spent just one weekend migrating a Python project into 165,000 lines of TypeScript, reducing full-platform build time from 30 minutes to around 2 seconds.

**Refactoring 165,000 lines of code in one weekend—just think about that.**

In the past, even the strongest team would have needed one or two years for a project of this scale, and still might not have achieved 100% compatibility. Now, one person plus one AI can get it done in a few days.

Naturally, everyone is curious: how did they do it? Is there some method or technique behind all this?

Below, I’ll combine the official blog post with Bun’s official technical blog and my own experience using AI for programming to give you a complete in-depth explanation in Chinese.

Once you learn this method, you can use the same thinking to efficiently handle refactoring large projects with tens of thousands of lines, upgrading tech stacks, and refreshing legacy systems.

## The Core Idea Behind AI Code Migration

When using AI to migrate code, your job is not to modify the code itself—it’s to set up the **process that produces the code**.

The traditional migration mindset is to translate files one by one, check them one by one after translation, and then fix problems one by one.

That approach is still workable at the scale of dozens of files, but once the number grows into the hundreds or thousands, it basically becomes impossible.

The correct way to think is to **focus your attention on the process**.

When you notice that AI keeps making the same kind of mistake in a certain type of translation, don’t fix those bad outputs one by one. Instead, fix the rulebook so that all future translations stop making that mistake. As the rules improve, the number of times you need to intervene manually will keep decreasing.

![](https://pic.yupi.icu/1/01_%E4%BF%AE%E6%B5%81%E7%A8%8B%E4%B8%8D%E4%BF%AE%E4%BB%A3%E7%A0%81%EF%BC%9A%E6%A0%B8%E5%BF%83%E6%80%9D%E8%B7%AF%E5%AF%B9%E6%AF%94_compressed_v1.png)

When I first started using AI for programming, I often fixed bugs one by one. AI made a mistake, I corrected it once, then it made the same mistake again next time, and I corrected it again. Over and over—very inefficient.

Later, I started writing the pitfalls I had encountered into `CLAUDE.md`, `AGENTS.md`, or Rules files. Every time I corrected an AI mistake, I also turned it into a rule.

Here’s a simple example. I noticed that when AI generated Spring Boot APIs, it often forgot to add parameter validation annotations, so I added this rule:

```markdown
所有 Controller 层的请求参数必须使用 @Valid + DTO 校验，禁止在 Service 层手动 if 判空
```

From then on, that problem never came up again.

So whether you’re migrating millions of lines of code or just doing everyday Vibe Coding projects, you should keep this mindset: **when something goes wrong, don’t just stare at the problem itself—fix the source that produces the problem**.

## The Six-Step Migration Method

Anthropic summarized a complete workflow for large-scale code migration in six steps.

One diagram to start, and you’ll immediately see how powerful this methodology is.

![Overview of the six-step migration process](https://pic.yupi.icu/1/07_%E5%85%AD%E6%AD%A5%E8%BF%81%E7%A7%BB%E6%B5%81%E7%A8%8B%E6%80%BB%E8%A7%88%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89_compressed_v1.png)

### 0. Set Up the Validation Mechanism

Before you start migrating, you must have a reliable validation mechanism. Without it, you won’t even know when you can call the job done.

The ideal case is like Bun: you already have a complete test suite, and the tests are written in a third-party language (Bun’s tests use TypeScript), so they don’t depend on the source language being migrated.

But what if your tests are written in the same language as the source code?

The recommendation is to classify the tests first. Which tests validate behavior through external interfaces? Which ones depend on internal implementation details?

Tests based on external interfaces can be reused directly. Tests tied to internal implementation details need to be rewritten into a language-agnostic form.

In the example mentioned earlier, Mike’s project didn’t have an existing test suite. His solution was to let Claude create a **comparison script** that ran 7 real scenarios and diffed the outputs of the Python version and the TypeScript version. Any behavioral difference counted as a bug.

This idea works perfectly well for small projects too. Even if you’re only migrating a Python script to TypeScript, you can still let AI help you prepare a few sets of real input/output samples, then run them after migration and compare whether the results are the same.

### 1. Create the Rulebook and Dependency Graph

This step is the most labor-intensive part of the whole process.

![](https://pic.yupi.icu/1/08_%E7%AC%AC1%E6%AD%A5%EF%BC%9A%E5%88%B6%E5%AE%9A%E8%A7%84%E5%88%99%E6%89%8B%E5%86%8C%E5%92%8C%E4%BE%9D%E8%B5%96%E5%9B%BE%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89_compressed_v2.png)

Jarred, the founder of Bun, spent 3 full hours just discussing with Claude how to map Zig patterns into Rust. The final output was a 576-line rulebook that specified in detail how each type should be mapped and how each idiom should be converted.

The content of the rulebook depends on one key strategy: **should the new code preserve the original architecture and be translated line by line, or should it be completely redesigned?**

Jarred chose a mechanical translation while keeping the architecture unchanged, so his rulebook mainly became a mapping table. He also had Claude run a workflow to analyze the lifecycle of every struct field in the codebase and output a `LIFETIMES.tsv` file for later translation reference.

![](https://pic.yupi.icu/1/image-20260720171445547.png)

Mike, on the other hand, chose to redesign the architecture, so his rulebook looked more like a design document describing what the new system should look like.

Besides the rulebook, the dependency graph is also important. You need to know which files depend on which other files so you can determine migration order and decide which files can be processed in the same batch.

For languages like Python, where dependencies are not declared explicitly, you can let Claude write a script to analyze and generate the dependency graph. Anthropic also open-sourced a [code migration toolkit](https://github.com/anthropics/code-migration-kit-with-claude-code) that already includes ready-to-use dependency analysis scripts—just use them directly.

![](https://pic.yupi.icu/1/image-20260720171538243.png)

On top of that, you should also create a “difference checklist” listing the parts where the source language and target language cannot be translated directly.

For example, the core difference from Zig to Rust is going from manual memory management to an ownership system, while the core difference from Python to TypeScript is going from dynamic typing to explicit interface declarations. These are exactly the areas where AI is most likely to make mistakes, so they must be highlighted in the rulebook.

### 2. Do a Small-Scale Trial Run

Once the rulebook is ready, don’t rush into a full migration. Start by testing the waters with 3 files.

![](https://pic.yupi.icu/1/09_%E7%AC%AC2%E6%AD%A5%EF%BC%9A%E5%8E%8B%E5%8A%9B%E6%B5%8B%E8%AF%95%E8%A7%84%E5%88%99%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89_compressed_v1.png)

I think Jarred’s approach was very clever. He had one Claude instance translate 3 files according to the rulebook, while another Claude instance translated the same 3 files in the role of a “senior Rust engineer.” Then he opened a completely fresh Claude conversation dedicated to comparing the differences between the two versions and extracting new translation rules from those differences.

At this step, he discovered 2 critical problems. If they had been rolled out across all 1,448 files directly, the consequences would have been disastrous.

For projects that redesign the architecture, the approach is a bit different. Mike had multiple Claude instances critique the design document from different angles to find logical gaps or overlooked issues. Then he ran a complete end-to-end translation to see whether the design held up in practice. If problems were found, he revised the rules and ran it again.

What’s interesting is that he actually ran the full migration three times. **The first two outputs were thrown away entirely, keeping only the improvements to the rules, and only the third run’s result was kept officially.**

![](https://pic.yupi.icu/1/02_%E8%AF%95%E8%B7%91%E5%93%B2%E5%AD%A6%EF%BC%9A%E5%89%8D%E4%B8%A4%E6%AC%A1%E4%B8%A2%E5%BC%83%E5%8F%AA%E4%BF%9D%E7%95%99%E8%A7%84%E5%88%99%E6%94%B9%E8%BF%9B_compressed_v1.png)

When I saw that, my first reaction was: throwing away the first two runs outright—doesn’t that waste tokens?

But actually, for complex projects, this is reasonable. The goal of the trial-run stage is to refine the rules. The code generated during the trial run may not necessarily be correct or usable. If you apply it directly, it could affect the entire migration.

This is also very enlightening for ordinary developers. When many people use AI to build projects, they always want to get everything right in one shot. But in reality, it can be smarter to let AI first produce a rough version, see what’s wrong, improve the prompts and rules, and then start for real. Sharpening the axe does not delay the chopping of wood.

### 3. Full-Scale Translation

After the rules have been validated through trial runs, you can begin the full migration.

The core architecture of this step can be understood as a pipeline with 3 roles: a translation Agent, a fault-finding Agent, and a repair Agent.

![](https://pic.yupi.icu/1/10_%E7%AC%AC3%E6%AD%A5%EF%BC%9A%E5%85%A8%E9%87%8F%E7%BF%BB%E8%AF%91%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89_compressed_v1.png)

Each translated file is inspected by 2 independent “fault-finding Agents,” whose sole job is to look for problems. Once issues are found, they are handed off to the “repair Agent” for processing.

![Three-role Agent pipeline](https://pic.yupi.icu/1/03_%E4%B8%89%E8%A7%92%E8%89%B2Agent%E6%B5%81%E6%B0%B4%E7%BA%BF%EF%BC%9A%E7%BF%BB%E8%AF%91%E3%80%81%E6%89%BE%E8%8C%AC%E3%80%81%E4%BF%AE%E5%A4%8D_compressed_v2.png)

The fault-finding Agent here is what was mentioned earlier as an “adversarial review.”

Why is it called adversarial?

Because the reviewer is explicitly told to **assume this code has bugs, and your task is to find where the bugs are**.

This mindset is exactly the same as human code review. A reviewer cannot begin with the assumption that “their code is probably fine, right?” Instead, they have to review with a skeptical attitude in order to find real issues.

![Adversarial review](https://pic.yupi.icu/1/04_%E5%AF%B9%E6%8A%97%E6%80%A7%E5%AE%A1%E6%9F%A5%EF%BC%9A%E6%80%80%E7%96%91%E5%BF%83%E6%80%81_vs_%E4%BF%A1%E4%BB%BB%E5%BF%83%E6%80%81_compressed_v3.png)

It sounds simple, but there are several practical details to watch out for.

1) The work queue should be mechanical. For example, whether a file has been translated can be determined by checking whether the target file exists on disk. That makes the whole process naturally resumable—you can just restart after interruption without maintaining extra state.

2) The conversations of the translation Agent and review Agent must be isolated. The AI writing the code always tends to think its own code is fine, so the reviewer must work in a completely fresh conversation, seeing only the translated result and not the reasoning process behind it.

3) Models should be used in layers. Not every step needs the strongest model. High-concurrency work like translation can use relatively cheaper models (such as Claude Sonnet), while review and rule-making should use the strongest models (such as Claude Fable or Claude Opus). Mike used 12 Sonnet subagents in parallel during the full-translation stage.

If there’s anything uncertain during translation, just mark it with `// TODO(port): <原因>`. Don’t get stuck on it at this step—the compiler and tests will tell you later whether it’s right or wrong.

### 4–6. Compile + Run + Align Behavior

The next 3 steps all follow the same pattern: run once to get an error list, then let a batch of repair Agents fix those errors in parallel, then run again, repeating until there are no errors left. The amount of human intervention keeps decreasing.

![Error-driven repair loop](https://pic.yupi.icu/1/05_%E9%94%99%E8%AF%AF%E9%A9%B1%E5%8A%A8%E4%BF%AE%E5%A4%8D%E5%BE%AA%E7%8E%AF_compressed_v3.png)

1) During the compilation phase, collect all compiler errors into a to-fix list, then let AI fix them one by one according to the list.

Jarred’s approach was to let the orchestration script run the compiler once across the entire workspace, group the errors by module into files, and then let 64 “repair Agents” process the error lists in parallel. Each repair Agent was watched by 2 adversarial reviewers. After repairs, the project was compiled again, and the cycle repeated.

He ran into one major issue here.

The original Zig code was compiled as one giant lump, but he wanted to split the Rust code into 100 independent modules to speed up compilation. That introduced a huge number of circular dependency problems.

So he ran a dedicated workflow to classify which code should be moved where. After fixing the circular dependencies, about 16,000 compilation errors were exposed. For a human, 16,000 errors is astronomical. For 64 parallel Claudes, it’s just a matter of a few hours.

2) During the smoke-test phase, collect all crash information into a to-fix list.

After compilation passes, start by running each subcommand and saving every crash message together with the corresponding subcommand into files, then process them with the same “repair + review” loop.

3) During the behavior-alignment phase, collect all failed tests into a to-fix list.

Run the test suite in shards. Each failing test is handed to a repair Agent, and after repair, an adversarial reviewer checks it.

![](https://pic.yupi.icu/1/11_%E7%AC%AC4-6%E6%AD%A5%EF%BC%9A%E7%BC%96%E8%AF%91%E3%80%81%E8%BF%90%E8%A1%8C%E3%80%81%E8%A1%8C%E4%B8%BA%E5%AF%B9%E9%BD%90%EF%BC%88%E4%B8%AD%E6%96%87%E7%89%88%EF%BC%89_compressed_v1.png)

Jarred also had a clever design: only one dedicated build daemon was allowed to compile the whole project. Repair Agents only submitted code, and the daemon periodically compiled all patches in batches, ran the affected tests, and fed the results back. This avoided multiple Agents each triggering their own compilation, which would have caused resource conflicts and duplicated work.

Throughout the process, Bun’s CI went from 972 failing test files to all green, taking about 4 days. Linux turned green first, and Windows was last. After merging, there were 19 regression bugs in total, all of which were fixed.

![](https://pic.yupi.icu/1/image-20260720165511010.png)

In fact, Airbnb had done something similar before. They used AI to migrate 3,500 React component tests from Enzyme to React Testing Library. What had originally been estimated to take a year and a half was finished in 6 weeks using a similar approach.

## My Thoughts

After reading Anthropic’s six-step migration method, here are a few points that really resonated with me.

First is the idea of adversarial review. This is something everyone can absolutely do in everyday AI programming. For example, after one Agent finishes writing code, you can open a new conversation and let another Agent do a code review. In Claude Code, you can directly use the built-in `/code-review` command, or use a Subagent for review. Even if you’re not doing code migration, this is a habit worth building.

Then there’s the cost issue. Can you believe it? Bun’s migration cost **$165,000** in API fees!

![](https://pic.yupi.icu/1/image-20260720182903395.png)

At first glance, that number sounds terrifying, but compared with the salaries and opportunity cost of 3 senior engineers working for a year, it’s far cheaper.

For individual developers, migrating a project with tens of thousands of lines usually only requires a Pro or Max subscription allowance. As for whether the money is worth it, just calculate it against labor cost yourself.

But don’t blindly follow the trend and migrate everything. If your existing code is running fine and isn’t hard to maintain, there’s no need to toss it around.

**Migration only makes sense when you really have an ongoing pain point that needs solving.**

For example, during the few days when Claude Fable 5 had limited-time availability, I went crazy optimizing my own workflow. But in the end, it was optimization for optimization’s sake and didn’t really achieve much, mainly because Opus had already been doing a good job before that.

Another crucial point is that **human judgment is still irreplaceable**.

Throughout the migration, Jarred monitored workflow outputs every day, manually checked AI behavior, and adjusted the process whenever he discovered systematic problems.

AI may have strong execution power, but decision-making authority still remains with humans.

AI can save costs, but that doesn’t mean people are no longer needed at all.

## Final Words

Let me summarize the method from this article for you so you can use it immediately:

1) Before doing any somewhat large refactor or migration, first talk with AI to produce a rules document. Clearly define “what should be changed and how.” Don’t jump straight into coding.

2) First do a trial run with 3 files and see what mistakes the AI makes. Don’t fix the generated code one by one—add the discovered issues into the rules document, then regenerate.

3) The AI writing the code and the AI reviewing the code must be separated. You can use Claude Code’s `/code-review` command or open a new conversation for an independent review.

4) Make good use of the idea that “errors are your checklist.” Compilation errors, failed tests, lint warnings—these are all natural task lists. Just let AI fix them one by one from the list.

Think about it: if AI can migrate hundreds of thousands or even millions of lines of code, then what do we have to fear when refactoring our everyday projects with a few thousand or tens of thousands of lines?

The key is not how smart the AI is. Today’s models are already capable enough. What matters more is whether the process you design for the AI is good enough.

I hope this article helps you build that confidence and learn how to truly harness AI!
