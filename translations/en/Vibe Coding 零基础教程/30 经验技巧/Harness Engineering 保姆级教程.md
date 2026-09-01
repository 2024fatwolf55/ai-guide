# A Beginner-Friendly Guide to Harness Engineering

> Build a complete, reliable working environment for AI so it can keep delivering projects dependably



Hello everyone, I’m Yupi.

Anyone who has used AI for coding has probably run into these problems:

- You ask AI to tweak a page’s styling, but it doesn’t really understand what you want and ends up rebuilding the entire layout.
- You clearly said earlier that no single file should exceed 200 lines of code, but after more than ten rounds of conversation, AI forgets the constraint and writes a huge 1,000-line file.
- And the most painful one: you ask AI to fix one bug in a project, and it creates three new bugs instead. The project no longer runs, and the code gets messier and messier.

![](https://pic.yupi.icu/1/1_harness_problem.png)

There are already quite a few ways to solve the first two problems, such as writing better prompts and giving AI enough information. But the third problem is much trickier.

**If you want AI to do a complete project well, you also need to build a full set of reliable working environments and workflows around it.**

That’s what the AI world has recently been calling Harness Engineering.

![](https://pic.yupi.icu/1/17_harness_concept.png)

Before making this article, I read many Harness tutorials from both China and abroad. A lot of them spent huge amounts of space talking about AI history and dry theory that people forget right after reading. So I took a different approach: first explain Harness in a simple, easy-to-understand way, then show you how to use Harness in a real large-project workflow, and finally tell you the fastest way to get started with it.

⭐️ Video version of this article: https://bilibili.com/video/BV1cW9xB3Ec1



## 1. A Quick Understanding of Harness Engineering

### What Is a Harness?

The word “Harness” literally refers to horse tack. If you compare the AI model to a horse, then the harness is everything you need to control that horse: reins, route planning, fences, and so on.

What we’re trying to do is make that horse run faster and more steadily, so it can complete the task smoothly.

More specifically, a harness is the complete working environment and workflow built around an AI model. The project rule files you write for AI, the tools you configure, the way you break down tasks and arrange execution order, and the testing and checking processes you design—all of these count as part of the harness.

![](https://pic.yupi.icu/1/2_harness_horse.png)



### Why Did It Suddenly Become Popular?

The well-known AI framework LangChain ran an experiment: using the same AI model, they optimized only the Harness built around the model, and their coding benchmark ranking jumped from outside the top 30 straight into the top 5!

![](https://pic.yupi.icu/1/3_langchain_exp.png)

The OpenAI team made similar attempts as well. A small three-person team used Harness alone to guide AI into generating over a million lines of code, and the final product was officially put into internal use.

After results like these appeared, many famous AI companies and tech leaders started writing blog posts about Harness, which helped push the concept into the spotlight.

With endorsements from these big names, the industry has now reached a consensus: **the bottleneck in AI coding is not how smart the model is, but whether the environment and workflow you build around it are good enough.**

![](https://pic.yupi.icu/1/18_model_and_harness.png)



### The Evolution of Harness

Many people think Harness is some brand-new thing that popped up in 2026. But in fact, people had already been doing Harness since ChatGPT appeared in 2022—they just weren’t calling it that yet.

To help you understand it better, let me quickly review how AI engineering has evolved over the past few years.

![](https://pic.yupi.icu/1/19_harness_develop.png)



#### 1. Prompt Engineering (2022 ~ 2024)

Simply put, this is about **how to make AI understand your requirements through conversation**.

We learned to assign roles to AI, constrain its output format, use chain-of-thought prompting to make it think step by step, and provide examples for it to imitate. These techniques are simple, but they genuinely improved output quality a lot.

![](https://pic.yupi.icu/1/4_prompt_engineer.png)

#### 2. Context Engineering (2025)

This goes one step further on top of prompt engineering. The core idea is **feeding AI the right information at the right time**.

For example, you can write an `AGENTS.md` rule file so AI understands the project background, use RAG so AI can retrieve relevant materials, compress and summarize overlong context, or even build cross-conversation memory so it doesn’t lose track halfway through a discussion.

![](https://pic.yupi.icu/1/5_context_engineering.png)

#### 3. Harness Engineering (2026)

This pushes things another step forward beyond context engineering. It’s not just about what information to give AI, but also what tools to equip it with, how to break large tasks into small batches, how it should check and repair its own mistakes, and how to stop code quality from slowly degrading over time. The goal is no longer just to have AI answer questions, but to make it **reliably complete an entire task over time**.

![](https://pic.yupi.icu/1/6_harness_engineering.png)

You’ll notice that these three layers contain one another:

- Prompts are the innermost layer, focusing on “how to give AI instructions”
- Context wraps around prompts, focusing on “how to provide information to AI”
- Harness wraps around all of that, focusing on “how to make AI reliably finish an entire task”

![](https://pic.yupi.icu/1/7_harness_layers.png)

The industry often summarizes it with a formula: **Agent = model + Harness**.

In other words, all the tools, rules, workflows, and checking mechanisms built around the AI model belong to the scope of Harness.

![](https://pic.yupi.icu/1/8_agent_queals.png)



## 2. The Five Core Modules of Harness

At this point, Harness may sound big and abstract.

But in reality, it isn’t that complicated. Harness is simply about solving a few core problems AI runs into while doing work.

Next, I’ll explain them one by one. If you’re a programmer, or if you’ve done project work before, you’ll realize these methods are actually very familiar.

![](https://pic.yupi.icu/1/20_harness_modules.png)



### 1. Context Architecture: Help AI Understand the Project Background and Rules

> `AGENTS.md` rule files, layered documentation, context compression, progressive loading

What’s the first step in doing a project?

Obviously, it’s understanding the requirements, the project background, and the development standards. Projects built with AI are no different—you need to feed that information to it.

We can write rule files like `AGENTS.md` to tell AI what tech stack the project uses, what coding standards it follows, and what is forbidden. This is just like writing requirement documents and solution design documents in traditional development.

But one thing to note is that AI’s context capacity is limited. The OpenAI team ran into this exact pitfall. They tried stuffing thousands of lines of rules into one big file, and AI actually became more likely to ignore the important information inside. Later, they changed `AGENTS.md` into more of a **directory index**: it contained only about 100 lines of summary and navigation, while detailed design documents were placed under `docs/`. `AGENTS.md` clearly pointed to things like “see `docs/FRONTEND.md` for frontend standards” and “see `docs/SECURITY.md` for security-related content.” AI would read the specific file only when needed. This idea of **loading on demand** is the core of context architecture.

![](https://pic.yupi.icu/1/9_agents_ondemand.png)



### 2. Execution Capability: Give AI Hands, Feet, and Tools

> Tool calling, Bash terminal, file system, MCP, Browser Use, Skills packages

An AI model by itself can only output text. If you want AI to genuinely help build a project, you need to give it computer-operating ability through tools—for example, a terminal environment for running commands, a file system for reading and writing code, and a browser for testing webpages.

On top of that, MCP can further expand AI’s operating range, letting it read and write databases, search the web, fetch up-to-date content, and more.

Then there are Agent Skills, which package complete complex workflows into reusable skill packs, allowing AI to quickly learn all kinds of professional abilities, such as automatically generating PPT slides or processing Excel spreadsheets. In short, the more tools AI can use, the more work it can do for you.

![](https://pic.yupi.icu/1/10_harness_execute.png)



### 3. Task Orchestration: Arrange a Proper Work Plan for AI

> Plan Mode, task decomposition, incremental development, documentation, parallel SubAgents

If you throw one huge requirement at AI, it may try to do everything in one shot. But AI’s context space is limited. Halfway through development, the context may no longer fit, and the earlier decisions and constraints gradually get diluted, leaving behind a pile of broken code that doesn’t run.

![](https://pic.yupi.icu/1/21_context_full.png)

So how do you solve this?

The most basic approach is to split large tasks into small tasks and only do one feature at a time. Before starting, you can use Plan Mode to let AI produce a plan first, then confirm it manually, and only then begin writing code.

After every completed feature, it’s best to produce some documentation that records what has been implemented, what technical solution was used, and what still remains to be done. That way, even if you open a brand-new AI conversation later, AI can quickly understand what was done before by reading the docs instead of starting from scratch.

If there are multiple small tasks that do not depend on one another, you can also use SubAgents to execute them in parallel for higher efficiency. This is the same idea as task splitting and frontend/backend parallel development in traditional projects.

![](https://pic.yupi.icu/1/11_harness_task_split.png)



### 4. Feedback Mechanisms: Let AI Check Its Own Work

> Linter checks, automated tests, Browser Use end-to-end testing, agent peer review

After AI writes code, it may confidently tell you the task is complete—but when you actually run it, everything is full of bugs.

So we need AI to be able to inspect its own work after coding. For example, it can run a linter to check for syntax and style issues, run automated tests to verify functionality, or even open a browser and operate the feature itself. Only if it works normally should the task count as truly complete.

If the tests fail, AI can automatically read the error messages, analyze the cause, and attempt a fix. Of course, we can also inspect things manually and then provide AI with the issues, error messages, or screenshots so it can fix them.

You can even let another AI review the code and create a “multi-agent peer review” mechanism, which is basically the same as having multiple colleagues do code review in a traditional project.

![](https://pic.yupi.icu/1/12_auto_fix.png)



### 5. Architectural Guardrails: Prevent the Codebase from Getting Messier and Messier

> Architecture-constrained lints, pre-commit hooks, garbage collection mechanisms, Git checkpoints

One characteristic of AI-generated code is that it imitates the coding style already present in the repository—even if that existing code is bad. For example, the same page code may be written multiple times without being split into reusable components, which means if one place changes, the other duplicated places are easily forgotten. Over time, technical debt snowballs.

![](https://pic.yupi.icu/1/22_tech_debt.png)

How do you prevent that?

A common approach is to write a batch of specialized linters that enforce architecture-level constraints. Note that this is slightly different from the linters mentioned in the feedback mechanism above. Those focus on code style and syntax issues, while these focus on architectural rules, such as the UI layer not being allowed to call the database layer directly, or dependencies between modules needing to stay one-way only. Once AI violates those rules, it gets blocked automatically. You can also use pre-commit hooks to intercept non-compliant code at commit time.

OpenAI also built a mechanism called “garbage collection,” where AI periodically scans the codebase, checks for deviations from architectural rules, and automatically submits fix PRs to continuously pay down technical debt.

I also recommend committing code with Git after every completed feature. Git is a version control tool that records every historical version of your code, essentially giving your project a save point. If later changes introduce problems, you can always restore an earlier state.

![](https://pic.yupi.icu/1/13_arch_safety.png)



---



At this point, you’ve probably noticed something: writing rule files, equipping tools, splitting tasks, running tests, defining architecture rules... these are all common methods programmers already use in project development. Put into the AI coding context, that becomes Harness.

![](https://pic.yupi.icu/1/14_harness_arch.png)

**Harness is not some brand-new technology. At its core, it is simply the systematic application of our existing engineering experience to AI.**

So if you already have project experience, your accumulated engineering ability is still just as useful in the AI coding era. I also recommend that everyone spend more time doing complete projects and building engineering experience. The more you understand engineering, the better you can control AI.



## 3. A Harness Project in Practice

Now that the concepts are out of the way, let me show you how Harness actually lands in real development through a real project.

This project is the AI full-stack project “Universal Video Download Summarizer” that I built live from start to finish in [Programming Navigation](https://www.codefather.cn). Using AI, I developed from scratch a website that can download videos from major platforms, summarize video content with AI, and also includes SEO / GEO optimization and Stripe international payments.

![](https://pic.yupi.icu/1/image-20260414185727869.png)

Looking back, the whole development process was essentially a complete Harness practice.

Next, I’ll walk through it according to the typical stages of enterprise project development and show you which Harness methods were used at each step.



### 1. Solution Design Phase

Before touching any code, I did one very important thing: **I first thought through the core solution myself**.

What kind of frontend interface does this project need? Does it need a backend? How should the core video download capability be implemented?

I first thought these through on my own, and also used AI to research across the internet. In the end, I decided to use the open-source project `yt-dlp` as the core implementation for downloading, with Python as the main tech stack.

Then I wrote those ideas into documents and attached them for AI, so it could add details based on my plan.

![](https://pic.yupi.icu/1/1772104502180-1c03c0ee-e122-45f9-ab57-b6f80ba68769.png)

Notice that I deliberately **enabled Plan Mode**, so AI would first propose a plan for my confirmation instead of jumping straight into coding.

AI generated a technical solution document, and after I read it carefully, I noticed it had included some later-stage features in the initial plan. So I told it, “Let’s complete the core video download feature first,” and move step by step.

![](https://pic.yupi.icu/1/1772105641205-3b10ce44-984a-4a0a-8164-e6bf9238008b-20260414190723769.png)

This is exactly how **task orchestration** and **context architecture** are applied in the solution phase. Plan first, then execute. Give AI enough background information, and constrain it so it doesn’t try to do everything at once from the very beginning.



### 2. Coding and Development Phase

Once the plan was confirmed, AI entered the development phase. During this stage, I did several very important things.

First, I **gave AI internet access**. I configured Firecrawl MCP so AI could fetch webpage content, and Context7 MCP so AI could obtain the latest technical documentation.

![](https://pic.yupi.icu/1/1772104408697-5266b0fe-962d-4f1c-9651-f6f23e178881.png)

This way, if AI was unsure about how an API should be used during development, it could look up the latest docs itself instead of relying on outdated patterns.

![](https://pic.yupi.icu/1/1772102457113-a31b056a-bfd8-4458-a8b1-194e3a8ca648.png)

After the core video downloading feature was completed, I **had AI summarize the current state into documentation**, recording the implemented features, architecture, and technical details, and then commit them to Git.

![](https://pic.yupi.icu/1/1772528547362-5763b40e-ef99-4abb-96c3-a21411c6456f.png)

This step is crucial, because when I later work on new features, I open a new conversation window and attach these documents. AI can then quickly recover its memory instead of starting over.

![](https://pic.yupi.icu/1/1772528792609-cc1739e6-21eb-4909-8967-80f03d3e8a99.png)

Why open a new conversation for new features?

Because if you keep talking too long in the same AI conversation, the context gets dirtier and dirtier, and AI’s performance drops. Opening a new conversation is like giving AI a clean environment, and then using documentation to restore the information it needs.

These operations are fundamentally all about building **context architecture** and **execution capability**: equipping AI with tools and maintaining the context information properly.



### 3. Testing and Validation Phase

AI can do more than write code. It can also **open the browser and test by itself**.

In this project, through Cursor’s built-in Browser Use feature, AI launched a browser, entered a video link, clicked the parse button, and then checked whether the result was displayed normally. It was far more convenient than testing everything manually.

![](https://pic.yupi.icu/1/1772182233654-f0155f39-9a20-475c-b6ab-65144ae88add.png)

Of course, AI’s self-testing isn’t all-powerful. When it runs into a problem it cannot solve, humans still need to step in.

For example, in manual testing I found that downloading Bilibili videos threw a `403` error. I pasted the error message directly to AI and let it analyze and fix the issue on its own. It quickly realized the problem was anti-leech protection and solved it.

![](https://pic.yupi.icu/1/1772183079662-6a6c95ea-a666-4ff5-98aa-c28640cfde72.png)

Sometimes AI gets stuck on the same issue and keeps failing to fix it. For instance, there was a Markdown rendering problem that I discussed with AI over several rounds, but it still didn’t get it right.

![](https://pic.yupi.icu/1/1772620145879-c410ef48-e0b5-4a1a-b72c-9abb3d5ec292.png)

Later, I described the issue from a different angle and told it: shouldn’t you be changing the backend Python code instead? If the backend `SSE` response content is being lost, then of course the frontend will parse it incorrectly.

![](https://pic.yupi.icu/1/1772621509450-1b167ee7-e8c6-4aa2-a0d7-08b645d39df3.png)

Only then did AI suddenly understand, and after changing the backend logic, the issue was fixed.

![](https://pic.yupi.icu/1/1772621492366-d5a020a8-290f-4c84-82ac-c92a27c6be0c.png)

Another small trick is not to go through the entire flow of “input link → parse → summarize” every time you test—it’s too slow. I had AI directly simulate a piece of Markdown data and test only the rendering effect, which made the feedback much faster.

![](https://pic.yupi.icu/1/1772618934073-fac1cb70-5793-4c56-a353-1893483b231a.png)

All of these are manifestations of the **feedback mechanism**: providing AI with feedback signals so it can self-repair, and letting humans step in to correct its direction only when AI can’t solve it on its own.

Harness does not mean completely letting go. It means using human energy on the most critical parts.



### 4. Feature Expansion Phase

After the core video download functionality was working, I added three more small requirements: improve Markdown typography, support fullscreen + download for mind maps, and support subtitle file downloads.

These three requirements were independent of one another, so I guided AI in the prompt to plan them reasonably and **develop them in parallel**. AI used SubAgents to execute multiple subtasks simultaneously.

![](https://pic.yupi.icu/1/1772616016270-9d4e5537-e7da-4f7c-8242-5b4db2e5d79b.png)

After each feature was completed, I had AI commit the code and update the documentation as a checkpoint. If a later change caused problems, I could roll back at any time.

![](https://pic.yupi.icu/1/1772613546285-f7291f45-8f72-49aa-b501-09169cb13aa5.png)

Later, when I did SEO optimization for the project, I also used an SEO Audit skill so AI could automatically analyze the website and generate an optimization plan.

![](https://pic.yupi.icu/1/1773740490974-4416b5e7-79bf-472f-bae5-b54cc7ea0b20.png)

After SEO was done, GEO optimization still remained. I directly reused the existing SEO conversation context, so AI already understood the project background and code and didn’t need to read everything again from scratch, which saved a lot of time.

![](https://pic.yupi.icu/1/1773744551802-fff25d1e-bccd-475d-a7b8-2510566221d7.png)

These actions involve **task orchestration** (parallel development), **architectural guardrails** (Git checkpoints), and **execution capability** (Skills-based extension)—all of which are important Harness practices.



## 4. How to Get Started with Harness Quickly

Harness itself is not complicated, and there isn’t really any theory you need to specially grind through. Many of the operations in the project above are Harness techniques you can start using right away.

Following the normal project workflow, I’ve summarized a few practical Harness methods for you:

1) Before starting a project, write an `AGENTS.md` rule file to tell AI the project background, tech stack, and coding standards

2) First let AI propose a solution and confirm it manually, then start writing code

3) Use MCP and Skills to equip AI with tools so it can search the web and retrieve the latest information

4) After completing a feature, always have AI run tests and validate the result itself to ensure it really works

5) After every completed feature, have AI document the result and commit the code as a kind of “save point” for AI

![](https://pic.yupi.icu/1/23_harness_tips.png)



### Harness Tools

If you lack project experience, or feel that building your own Harness is too troublesome, you can also directly use some ready-made open-source tools.

For example, the Spec Kit tool follows the SDD (Spec-Driven Development) approach. It first guides you to break requirements down into detailed spec documents, then has AI develop step by step according to those specs, with clear acceptance criteria at every stage.

![](https://pic.yupi.icu/1/15_sdd.png)

There is also an Agent Skills framework like Superpowers, which comes with a complete development workflow built in, including enforced TDD (Test-Driven Development), meaning tests are written before code, as well as two-stage code review and sub-agent collaboration. It’s basically like directly installing a full project-management process into AI.

![](https://pic.yupi.icu/1/16_superpowers.png)

Although tools like these can help you get started quickly, in the long run, **understanding the thinking behind Harness is more important than mastering any single tool**.

After all, tools keep changing, but the idea of “how to systematically control AI” is universal. If you want to truly master Harness, the best way is still to experience it in real project practice.

In [Programming Navigation](https://www.codefather.cn), I’ve led people through multiple AI full-stack projects. Besides the Universal Video Download Summarizer mentioned above, there are also the AI Hot Topic Monitoring Tool, the GitHub Document Translator, the AI Gamified Learning Mini Program, and more. In fact, all of them are complete Harness Engineering practices. Every project starts from requirement analysis, then goes through solution design, AI coding development, testing and validation, and feature expansion, completing the full process. If you want to learn AI coding and Harness while building real projects step by step, feel free to check them out.

![](https://pic.yupi.icu/1/image-20260414172537171.png)



## Final Rambling

In the past, the core job of engineers was writing code. Now AI can help us write more and more code, but that also means we need to spend more energy on requirement analysis, solution design, task decomposition, and quality control.

Whether or not you can use AI well depends on how strong your own engineering ability is.

That’s why I always recommend doing more complete projects and walking through the full process from 0 to 1. The engineering experience you accumulate along the way is the best Harness you can possibly build for controlling AI.
