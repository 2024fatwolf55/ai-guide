# Matt Pocock Skills: A Real Engineering Skill Library

> An open-source Skills repository with 180k stars that packs software engineering methodology into AI

Hello, I'm Yupi.

GitHub is truly magical these days. There’s an AI-related project that is almost entirely made of Markdown text files, yet in less than half a year it has gained **180k stars**.

The repository is called [skills](https://github.com/mattpocock/skills). Its author, Matt Pocock, is a very well-known educator in the TypeScript frontend world with hundreds of thousands of followers on YouTube. He summarized his daily AI coding workflow into a set of Skills—in other words, a group of instruction sets that can be directly installed into AI coding tools like Claude Code and Codex—and then open-sourced them.

![](https://pic.yupi.icu/1/image-20260721175958152.png)

So what exactly is in this set of Skills, and why has it become so popular?

In this article, I’ll walk you through this repository, show you how to install and use it, and point out the AI coding techniques inside that are especially worth learning.



## 1. What’s Special About This Repository?

The repository’s slogan is “Skills for Real Engineers,” which means this is not for vibe coding—it’s for people who genuinely want to do engineering.

Put simply, it provides a **standard operating workflow** for AI coding.

If you’ve used Claude Code, you probably know that you can create a `CLAUDE.md` file to tell AI how to work. But what most people write there tends to be either scattered notes or generic prompts copied from the internet, and the results are usually mediocre.

What Matt Pocock did was condense real software engineering methodologies—things like test-driven development, code review, and domain modeling—into individual Skill files. After installing them on your computer, you can type slash commands like `/grill-me` or `/tdd` inside AI coding tools, and AI will work according to the corresponding engineering method instead of just coding wherever its thoughts happen to wander.

![Conceptual comparison of CLAUDE.md and Skills](https://pic.yupi.icu/1/01_Skills%E6%A6%82%E5%BF%B5%E5%AF%B9%E6%AF%94%EF%BC%9A%E6%99%AE%E9%80%9ACLAUDE.md_vs_Skills%E7%B3%BB%E7%BB%9F_compressed_v1.png)

At the time I wrote this article, the repository contained dozens of Skill files. Among them, 22 were officially recommended for use, while the rest were still under development, for the author’s personal use, or already deprecated.

![](https://pic.yupi.icu/1/image-20260721213003965.png)

These 22 official Skills are divided into two major categories. One is engineering-oriented Skills, such as TDD, code review, and bug diagnosis—things directly related to writing code. The other is productivity-oriented Skills, such as brainstorming, context handoff, and even one that teaches AI to help you learn.

If you still don’t know what Skills are or how they work internally, I recommend first reading *Agent Skills: A General AI Skill Library* in this same section.



## 2. Install and Use in 30 Seconds

Installing this repository is very simple. Open your terminal and run one command:

```bash
npx skills@latest add mattpocock/skills
```

![](https://pic.yupi.icu/1/image-20260721181513539.png)

After you run it, it asks which Skills you want and which AI coding tool you want to install them into. Once you finish selecting, the corresponding Skill files are copied into your project directory or into the local configuration directory of the AI tool (for example, `~/.claude/skills/`).

![](https://pic.yupi.icu/1/image-20260721181722123.png)

I recommend selecting the `/setup-matt-pocock-skills` initialization Skill. After installation, run it once inside your AI coding tool. For example, I ran it in Claude Code:

![](https://pic.yupi.icu/1/image-20260721181838820.png)

AI will ask you a few questions to adapt the setup to your project, such as what tool you use to manage Issues and where your project documentation is stored.

For simplicity, I chose to manage Issues with local Markdown files, store documentation in the default `docs/` directory, and save rules into `CLAUDE.md`.

![](https://pic.yupi.icu/1/image-20260721182034789.png)

If you don’t want to manually manage the Skill files installed into the project, you can also install them as a Claude Code plugin. That way they stay up to date automatically, though you won’t be able to modify them yourself.

![](https://pic.yupi.icu/1/image-20260721190007313.png)

Now that it’s installed, let me show you a few of the most practical Skills in this repository.



## 3. grill-me: Requirement Interrogation

This is the hottest Skill in the entire repository and one that Matt Pocock himself strongly recommends over and over again. Its purpose is to let AI “interrogate your soul” in reverse, helping you fully think through your requirements and design *before* AI starts writing code.

**But amazingly, its core content is only three sentences long!**

Translated roughly, it says this:

> Ask me one question at a time about my plan or design until we reach alignment. Walk down each branch of the decision tree and resolve dependencies between branches one by one. For every question, provide your recommended answer.
>
> Only ask one question at a time, and wait for my answer before asking the next. Dumping a pile of questions at once overwhelms people.
>
> If facts can be discovered by inspecting the environment (files, tools, etc.), go check them directly instead of asking me. But decisions are mine to make, and every decision must wait for my approval.

![](https://pic.yupi.icu/1/image-20260721182742452.png)

It’s that simple and blunt, but once you actually use it, you’ll realize the effect is genuinely very good.

One user shared that the first time they used `/grill-me`, the AI asked 38 questions in one go. By the time it finished, they realized AI had forced them to think through a lot of design details they had never considered before.

![](https://pic.yupi.icu/1/image-20260721183248245.png)

I actually wrote a full hands-on article just about this Skill and the ideas behind it. You can read *Use grill-me to Let AI Cross-Examine Your Requirements* in the Tips and Techniques section of this tutorial.

If you’re working on a project with a code repository, you can also use the upgraded `/grill-with-docs` Skill. While grilling you with questions, it also records the terms and decisions confirmed during the discussion into `CONTEXT.md` and architecture decision record files, building a dedicated glossary for your project.

So what’s the point of that glossary?

I’m sure everyone has had this experience: every time you describe a certain operation in your project to AI, you have to write a whole paragraph explaining it, because AI doesn’t know your team’s internal terminology.

Matt Pocock’s solution is to define those terms in advance inside `CONTEXT.md`. For example, he has a course-management project, and for the operation “create a lesson from a course chapter into the file system,” he defined a term called “materialization cascade.” After that, when talking to AI, he only needs to say that phrase and AI immediately understands what he means.

Because AI reads `CONTEXT.md` in every conversation, the more terminology you accumulate there, the more accurately AI understands the project—and the more efficient your communication becomes.

![CONTEXT.md creates a shared language that makes communication increasingly efficient](https://pic.yupi.icu/1/03_CONTEXT.md%E5%85%B1%E4%BA%AB%E8%AF%AD%E8%A8%80%E8%AE%A9%E6%B2%9F%E9%80%9A%E8%B6%8A%E6%9D%A5%E8%B6%8A%E9%AB%98%E6%95%88_compressed_v3.png)



## 4. tdd: Test-Driven Development

Have you ever run into this situation? When you ask AI to develop in a test-driven way, it writes all the tests first in one big batch, and only afterward writes all the code.

That might *look* efficient, but it hides a nasty pitfall. While AI is writing the tests, the code doesn’t exist yet, so it can only imagine what the structure should look like. Once it starts writing the real implementation, the actual API may be completely different from what it imagined, and then a whole pile of tests has to be torn down and rewritten.

The `/tdd` Skill exists specifically to solve that problem. It forces AI to work in **vertical slices**: first write one test and make it fail, then write only enough code to make that one test pass, and only then move on to the next test. This is the classic Red-Green-Refactor loop, taking one small verified step at a time.

![Comparison of TDD vertical slicing and batch mode](https://pic.yupi.icu/1/04_TDD%E5%9E%82%E7%9B%B4%E5%88%87%E7%89%87vs%E6%89%B9%E9%87%8F%E6%96%B9%E5%BC%8F%E5%AF%B9%E6%AF%94_compressed_v1.png)

Beyond the loop itself, the Skill also contains a few rules worth paying attention to.

For example, it requires **testing only at pre-agreed seams**. A seam is a public interface in the code, such as a function’s inputs and return values. Before writing any tests, AI first confirms with you *which seams* should be tested, instead of spraying tests everywhere. That way, the test coverage stays focused on what actually matters.

![](https://pic.yupi.icu/1/image-20260721190924720.png)

The Skill also lists several anti-patterns that AI commonly falls into when writing tests. It’s basically laying down rules for the AI: if it discovers that it has written one of these bad kinds of tests, it must fix it.

The most typical example is “tautological testing,” where the test just re-implements the logic of the code being tested—for example, `expect(add(a, b)).toBe(a + b)`. Tests like that are meaningless because they’ll always pass. The correct approach is to use an independent source for the expected value, such as a literal constant or a manually calculated example.

For team projects, having AI write code in a TDD style leads to a very noticeable improvement in code quality.



## 5. diagnosing-bugs: Bug Diagnosis

When people run into a bug, their first reaction is often to inspect the code, guess a possible cause, and try changing something. AI tends to behave the same way. I’m sure many of you have experienced this: you ask AI to fix a bug, and it keeps hacking at the code until the situation gets even messier.

Matt Pocock believes the root cause is that AI skips the most important step: establishing a **reliable feedback loop that can consistently reproduce the bug**.

So what is a feedback loop? Simply put, it’s a command that can reliably reproduce the bug. It might be a failing test case, a `curl` request, or even a Playwright browser automation script. As long as you can run it with one command and it clearly tells you whether the bug has occurred, it counts.

The `/diagnosing-bugs` Skill breaks the debugging process into six stages, and “establishing the feedback loop” is the very first step—and the core of the whole workflow.

![](https://pic.yupi.icu/1/image-20260721191701894-20260721191719297-20260721191756770.png)

**Until this step is complete, AI is not allowed to move on to “guess the cause.”** If AI starts analyzing code before it has a command that can reproduce the bug, the Skill will interrupt it directly.

Once there is a reliable reproduction command, the later steps become more conventional: minimize the reproduction case, propose hypotheses and verify them one by one, then fix the bug and write a regression test.

![Six-stage bug diagnosis flowchart](https://pic.yupi.icu/1/05_Bug%E8%AF%8A%E6%96%AD6%E9%98%B6%E6%AE%B5%E6%B5%81%E7%A8%8B%E5%9B%BE%EF%BC%88%E5%8F%8D%E9%A6%88%E5%BE%AA%E7%8E%AF%E4%BC%98%E5%85%88%EF%BC%89_compressed_v2.png)

This idea feels somewhat similar to Cursor’s built-in Debug mode. Both approaches locate problems by automatically detecting and analyzing errors instead of letting AI guess wildly and patch things randomly from the start (you can read *Cursor Debug Mode Explained* in the Cursor section of this tutorial’s Programming Tools chapter).

That said, `/diagnosing-bugs` is more about process discipline. It constrains AI’s debugging behavior with a strict staged methodology.



## 6. teach: Learning with AI Assistance

The previous Skills were all related to writing code, but this repository also includes more general productivity tools. One example is the `/teach` Skill, which turns AI into your personal teacher.

Judging by the style of `/grill-me`, I originally thought this Skill would also be just a few lines long. But it actually has a pretty complete teaching methodology behind it.

When you run `/teach` and tell AI what you want to learn, it first asks *why* you want to learn it, then records your learning goal in a file called `MISSION.md`.

![](https://pic.yupi.icu/1/image-20260721202928545.png)

Next, it searches for high-quality learning resources and organizes them into a `RESOURCES.md` file.

![](https://pic.yupi.icu/1/image-20260721203009683.png)

Finally, based on the resources it gathered, it designs lessons for you. Each lesson is a polished HTML file stored in the `lessons/` directory.

![](https://pic.yupi.icu/1/image-20260721203410326.png)

One particularly interesting point is that AI distinguishes between two different kinds of learning outcomes: “fluency” and “storage strength.” Fluency is the feeling that you can recall something right now, but that doesn’t necessarily mean you’ve really remembered it. Storage strength is what leads to genuine long-term memory. So it deliberately designs exercises with some difficulty and uses methods like spaced repetition and interleaved practice to deepen your memory, instead of giving you the illusion that “I’ve already learned this.”

Another clever design is the “zone of proximal development,” a classic concept from educational theory. AI uses your past learning records to estimate your current level, then designs course content that goes just a little beyond what you can already do—not so easy that you get bored, and not so hard that you give up.

And because your whole learning process is stored in the current directory, the next time you open the same directory and continue learning, AI can pick up right where you left off.



## 7. wayfinder: Planning Large Projects

This Skill is designed to solve one very specific problem: what do you do when a project becomes too big to fit into a single AI conversation?

Anyone who has used AI for coding has probably felt this already: if you try to force everything into one very long conversation, the quality of AI’s thinking declines noticeably as the context grows. Matt Pocock calls the context range where AI performs best its “intelligence zone,” which is roughly within 120K tokens.

The approach of `/wayfinder` is to turn a big requirement into a “decision map.” When you’re facing a large, fuzzy requirement, AI first works with you to define the end goal clearly, then creates a map in your Issue management tool listing the sequence of decisions that need to be made, where each decision is an independent Issue.

![](https://pic.yupi.icu/1/image-20260721204043039.png)

These decisions have dependencies between them, so the Skill automatically marks which ones can be done first and which ones must wait for prerequisite decisions to finish. Every time you open a new AI conversation to handle a decision, the context starts clean, without being polluted by previous discussions.

![](https://pic.yupi.icu/1/image-20260721204132899.png)

There’s also a very interesting concept here called the “fog of war,” just like unexplored areas in strategy games. The decisions you can currently see are only part of the whole picture. As earlier decisions are completed, later ones gradually become clearer. This prevents over-planning things that you aren’t ready to understand yet.

![Wayfinder fog-of-war decision map](https://pic.yupi.icu/1/06_Wayfinder%E6%88%98%E4%BA%89%E8%BF%B7%E9%9B%BE%E5%86%B3%E7%AD%96%E5%9C%B0%E5%9B%BE_compressed_v1.png)

That said, this Skill has a relatively high barrier to entry and is more suitable for developers with some engineering experience. If your project isn’t especially large, the `/grill-me` Skill mentioned earlier is already enough.



## 8. Other Practical Skills

Besides the Skills above, there are two more that I think are especially worth mentioning.

1) `/improve-codebase-architecture` — Codebase architecture improvement

Matt Pocock recommends running this Skill every few days, almost like giving your codebase a regular health check. It deeply scans your repository, identifies structural areas that can be improved, and then generates a visual HTML report. The report uses Tailwind for styling and Mermaid for architecture diagrams. Each optimization suggestion is presented as a card showing the relevant files, the current problem, and the recommended improvement plan.

![](https://pic.yupi.icu/1/image-20260721204942049.png)

The core idea behind this Skill comes from the book *A Philosophy of Software Design*. To use an analogy, a good module is like a microwave oven: you only need to press a few buttons to heat your food, and you don’t need to care at all about the electromagnetic principles inside. That’s called a “deep” module—simple interface, complex implementation. But if using a module is almost as troublesome as implementing it yourself, then it’s a “shallow” module. This Skill tries to find shallow modules in your codebase and help turn them into deep ones.

![The difference between deep and shallow modules](https://pic.yupi.icu/1/07_%E6%B7%B1%E6%A8%A1%E5%9D%97vs%E6%B5%85%E6%A8%A1%E5%9D%97%EF%BC%88%E5%BE%AE%E6%B3%A2%E7%82%89%E6%AF%94%E5%96%BB%EF%BC%89_compressed_v1.png)

2) `/handoff` — Context handoff

Anyone who uses AI for coding has likely run into this problem: you discuss a lot in one conversation and accumulate tons of context, but when it’s time to start a new conversation, all of that prior discussion is gone. You can manually copy and paste it, but that’s inconvenient and easy to mess up.

`/handoff` solves that problem. Before the current conversation ends, it tells AI to compress the core content of the entire conversation into a handoff document and save it as a Markdown file. The next time you start a new conversation, you can simply ask AI to read that file, and it can continue working from where you left off.

![](https://pic.yupi.icu/1/image-20260721205244844.png)

This handoff document also suggests which Skills are recommended for the next conversation, and it automatically strips out sensitive information like API keys.



## Final Thoughts

After studying this repository, the strongest feeling I came away with is this: these Skills are not fundamentally about prompt tricks. They are about packaging classic software engineering methodologies into a format that AI can execute.

Things like test-driven development, domain modeling, and architecture review have existed in software engineering for more than twenty years. In the past, you had to rely on team collaboration and code reviews to enforce them. Now, with Skill files, you can make AI automatically work according to those methods.

And through this repository, you can also see that it has never been easier to do open source in the AI era. At the end of the day, Matt Pocock just shared the working methods from the `.agents` directory on his own computer, kept iterating and polishing them, and that turned into a project with more than a hundred thousand stars.

Maybe you can do the same—organize the AI coding workflows or prompt templates you’ve accumulated, open-source them, and keep improving them. You might end up helping a lot of people too. **Action is the primary productive force.**

If you want to explore more skill libraries like this, you can continue reading *Superpowers: The Core Skill Library* in this section, or browse *Recommended High-Quality AI Coding Extensions* in this tutorial’s Programming Tools chapter to find Skills that suit you.
