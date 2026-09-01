# A Beginner-Friendly Guide to Loop Engineering

> From manual prompting to automatic loops: the next paradigm of AI coding

Hello everyone, I’m Yupi.

The AI coding world has yet another new concept...

This time, it started because Boris Cherny, the father of Claude Code, said in a recent interview:

> I no longer prompt Claude directly. I have a bunch of loops running. They are the ones prompting Claude and deciding what to do next. My job has become writing loops.

![](https://pic.yupi.icu/1/loop%20engineering.png)

Right after that, Peter Steinberger, the father of OpenClaw, also posted:

> You shouldn’t be writing prompts for coding agents anymore. You should be designing loop mechanisms, so those loops can prompt your agent.

![](https://pic.yupi.icu/1/peter%20loopengineering.png)

When heavyweight figures from Anthropic and OpenAI are both saying the same thing, it means one thing: **the AI coding paradigm is upgrading again—from manually writing prompts to designing loop systems.**

This new paradigm is called **Loop Engineering**.

Honestly, I can’t even keep up. Harness Engineering only started getting popular back in February this year, and now there’s already another new concept?

There’s no end to studying, really no end...

![](https://pic.yupi.icu/1/image-20260616104758125.png)

But don’t worry. In this article, I’ll explain Loop Engineering from beginning to end. First I’ll tell you what it is and how it relates to earlier AI coding approaches, then I’ll use Claude Code, Codex, and Cursor for hands-on examples so you can feel what Loop is like in practice, and finally I’ll talk about its methodology framework and the pitfalls I’ve learned.



## 1. What Is Loop Engineering?

Loop Engineering literally means building loops. In simple terms, you design an automatically running system that replaces you in instructing AI, checking AI’s output, recording progress, and deciding what to do next. It keeps repeating that cycle until it reaches the goal you set.

![](https://pic.yupi.icu/1/01_Loop_Engineering%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5%EF%BC%9A%E4%BD%A0%E8%AE%BE%E8%AE%A1%E7%B3%BB%E7%BB%9F%E8%AE%A9%E5%AE%83%E4%BB%A3%E6%9B%BF%E4%BD%A0%E7%BB%99AI%E4%B8%8B%E6%8C%87%E4%BB%A4_compressed_v1.png)

The old AI coding style was like driving a manual-transmission car. Accelerating, shifting gears, turning—every step depended on you operating it manually. You gave AI one prompt, AI returned one chunk of code, and then it stopped to wait for your next instruction. **If you said nothing, it did nothing.**

Loop Engineering is more like autopilot. You set the destination and safety rules in advance, and then the car drives itself. It stops at red lights, reroutes when the road changes, and parks automatically when it arrives. You only need to glance at the dashboard once in a while and make sure it’s headed in the right direction.

In other words, you move from being the operator who “manually prompts AI sentence by sentence” to being the manager who “designs the loop rules.”

![](https://pic.yupi.icu/1/02_%E6%89%8B%E5%8A%A8%E6%8F%90%E7%A4%BAAI_vs_%E8%AE%BE%E8%AE%A1%E5%BE%AA%E7%8E%AF%E8%A7%84%E5%88%99%E7%9A%84%E5%AF%B9%E6%AF%94_compressed_v1.png)



### The 3 Core Elements of Loop

Some people may ask: isn’t Loop just a scheduled task? Just have the model keep repeating the same operation, right?

Absolutely not!

Without judgment ability, a loop may treat mistakes as correct answers and keep running further and further off track. That’s no different from a cron script. It doesn’t count as Loop Engineering.

A truly reliable loop needs three core ingredients:

1) Clear goals and stopping conditions

You need to tell the loop what counts as “done,” and that completion standard must be **verifiable**. For example, all tests passing, lint reporting zero errors, or all files being processed are good stopping conditions. But something vague like “optimize the code a bit” doesn’t work, because nobody knows when “optimization” is finished.

2) A feedback loop

At the end of every iteration, the loop must check the result and decide whether to continue into the next round or stop. The most common approach is to automatically run tests after coding. If the tests fail, it keeps fixing. If they pass, it stops.

3) State memory

AI conversation windows are limited. Once closed, they’re gone. A loop needs an external file to record the current progress, such as which tasks are done, which aren’t done yet, and what conclusion the previous round produced. That way, even if the process breaks and restarts, it doesn’t start from zero.

![](https://pic.yupi.icu/1/03_Loop%E7%9A%843%E5%A4%A7%E6%A0%B8%E5%BF%83%E8%A6%81%E7%B4%A0%EF%BC%9A%E7%9B%AE%E6%A0%87%E5%81%9C%E6%AD%A2%E6%9D%A1%E4%BB%B6%E3%80%81%E5%8F%8D%E9%A6%88%E9%97%AD%E7%8E%AF%E3%80%81%E7%8A%B6%E6%80%81%E8%AE%B0%E5%BF%86_compressed_v2.png)

You’ll keep seeing these three things in the practical examples later, so just keep the idea in mind for now.



## 2. The Evolution of AI Coding

Loop didn’t appear out of nowhere. It evolved step by step from earlier generations of AI coding methodology. Only by understanding that development path can you see what problem Loop actually solves and why it’s needed.

Here’s a simple overview of that evolution:

![](https://pic.yupi.icu/1/04_AI%E7%BC%96%E7%A8%8B%E8%BF%9B%E5%8C%964%E9%98%B6%E6%AE%B5%EF%BC%9APrompt%E2%86%92Context%E2%86%92Harness%E2%86%92Loop_compressed_v3.png)



**1. Prompt Engineering (2022 ~ 2024)**

This stage focused on how to make AI understand your requirements through conversation. For example, assigning AI a role, constraining output format, or using chain-of-thought prompting to make it reason step by step.

The core problem prompt engineering solved was “AI answers the wrong question.” Once you master prompt-writing techniques, output quality improves dramatically.

![](https://pic.yupi.icu/1/4_prompt_engineer.png)



**2. Context Engineering (2025)**

Good prompts alone weren’t enough. AI also needed to understand your project background to give reliable answers.

Context engineering focuses on **feeding the right information to AI at the right time**.

For example, writing an `AGENTS.md` rule file so AI understands project background, using RAG so AI can retrieve relevant materials, and building cross-conversation memory mechanisms.

The core problem context engineering solved was “AI gives answers detached from reality.” Only with good context management can AI’s output fit the actual situation of your project.

![](https://pic.yupi.icu/1/5_context_engineering.png)



**3. Harness Engineering (early 2026)**

With context, AI could understand your project. But to make it truly work well, you still needed to build a reliable working environment around it.

Besides giving AI proper context information, you also need to equip it with tools, break down tasks, set up tests, and prevent code rot.

Once the Harness is well set up, AI can produce stable and reliable output within an environment that has tools, tests, and constraints.

![](https://pic.yupi.icu/1/6_harness_engineering.png)



**4. Loop Engineering (mid-2026)**

This stage focuses on how to let AI form its own working loop.

Once the previous three steps are done, AI can already work in a reliable environment, but you still need to keep pushing it forward step by step. Loop solves exactly that problem. You hand over the tasks of “prompting, checking, and deciding the next step” to a system that repeatedly executes them. You only need to define the goal and stopping conditions, and AI can keep running by itself until the goal is reached.

These four layers contain one another. Prompt techniques, context management, and Harness construction are all still needed inside Loop. Loop simply adds one extra layer on top: **automatic iteration + a closed feedback loop**.

![](https://pic.yupi.icu/1/05_Loop%E5%9C%A8%E5%89%8D%E4%B8%89%E8%80%85%E5%9F%BA%E7%A1%80%E4%B8%8A%E5%8A%A0%E4%BA%86%E8%87%AA%E5%8A%A8%E5%BE%AA%E7%8E%AF+%E5%8F%8D%E9%A6%88%E9%97%AD%E7%8E%AF_compressed_v3.png)

Many people easily confuse Harness and Loop.

If AI is a horse, then Harness is the reins, saddle, and fence you put on the horse, and you ride it manually. Loop, on the other hand, is when you design a patrol route and let the horse run around it by itself without you even mounting it. After each lap, it automatically checks whether anything is abnormal, handles problems if it finds any, and then runs the next lap. You move from being the rider to being the route designer.

![](https://pic.yupi.icu/1/07_Harness_vs_Loop%E5%AF%B9%E6%AF%94%EF%BC%9A%E9%AA%91%E9%A9%AC_vs_%E8%AE%BE%E8%AE%A1%E5%B7%A1%E9%80%BB%E8%B7%AF%E7%BA%BF_compressed_v2.png)

That said, Loop Engineering is still a very early concept. The industry does not yet have unified standards or best practices. I recommend first building a solid Harness foundation—once that’s in place, learning Loop becomes much easier.



## 3. Hands-On Loop Practice

Now that we understand the basics, let’s jump directly into practical examples and experience what Loop feels like in real development using three AI tools.

Right now, both Claude Code and Codex already have built-in Loop-related commands, so you can use them directly. Cursor doesn’t yet have native Loop commands, but you can still implement the same ideas through prompt design. Let’s go through them one by one.



### Loop Practice in Claude Code

Claude Code provides two Loop-related slash commands: `/goal` and `/loop`, each corresponding to different scenarios.

#### The `/goal` Command

The purpose of `/goal` is to keep AI working until the goal you set has been achieved.

You provide a verifiable goal condition, and AI starts working. At the end of each round, an independent smaller model checks whether “the goal has been achieved.” If not, AI automatically starts the next round and continues. If yes, it stops and reports completion.

Note that the model judging whether the goal has been reached is separate from the model doing the work, which helps avoid bias from relying on a single model.

For example, if I want Claude Code to fix the entire project, I can write:

```bash
/goal 修复整个项目的代码，直到全部测试通过且没有报错
```

![](https://pic.yupi.icu/1/image-20260519191842661.png)

After execution, Claude immediately starts working and keeps going until all tests pass and no errors remain, without any intervention from you.

There’s also a small trick: you can add a fuse-like limit after the condition, such as “stop after 20 rounds if it still isn’t fixed,” which prevents AI from falling into a dead loop and burning tokens like crazy.

`/goal` is suitable for scenarios with a clear end condition where manual supervision is time-consuming—for example module migration, batch refactoring, fixing a test case until it passes, or processing a batch of Issues with a certain label.

If you want to check progress midway, just type `/goal` without any parameters. It will show you how long the current task has been running and how many tokens it has consumed.

![](https://pic.yupi.icu/1/image-20260519192117090.png)


If you want to stop it early, just use `/goal clear`:

![](https://pic.yupi.icu/1/image-20260519192203259.png)



#### The `/loop` Command

The purpose of `/loop` is to let AI repeatedly execute an operation at fixed time intervals.

For example, checking every five minutes whether deployment has completed:

```bash
/loop 5m 检查项目前后端的部署状态
```

![](https://pic.yupi.icu/1/image-20260519184353594.png)

`/loop` is suitable for tasks that need periodic watching—for example, automatically notifying you once deployment is finished, checking at intervals whether an online service has errors, or regularly scanning the codebase for newly introduced security vulnerabilities. Once the task is complete, remember to stop the Loop, otherwise it will keep running in the background and consuming resources.

To summarize the difference between these two commands: `/goal` means “run until completion,” which is suitable for one-off tasks with a clear endpoint; `/loop` means “run repeatedly on a schedule,” which is suitable for continuous monitoring tasks without a clear endpoint. Both are implementations of Loop Engineering, just for different scenarios.

![](https://pic.yupi.icu/1/08_goal_vs_loop_%E5%91%BD%E4%BB%A4%E5%AF%B9%E6%AF%94_compressed_v2.png)



#### The `/schedule` Command

`/loop` has one limitation: it runs on your local computer, so if your computer is turned off, it stops too.

If you want the loop to continue running in the cloud without depending on your local environment, you can use `/schedule` to create a cloud Routine scheduled task (currently in Research Preview).

For example, if you want Claude to check bug feedback once an hour:

```plaintext
/schedule 每小时检查一次 #project-feedback 频道的 Bug 反馈。
```

The difference between `/schedule` and `/loop` is that the former runs in the cloud and does not depend on your computer, while the latter runs locally and stops the moment you close your laptop. If you need 24/7 continuous monitoring, `/schedule` is the better choice.



### Loop Practice in Codex

The Codex desktop app also has similar Loop capabilities, mainly achieved in two ways.



#### Setting a Goal

In the Codex app’s chat box, you can input `/目标` to set a persistent goal. The effect is similar to Claude Code’s `/goal`: AI keeps working until the goal is reached.

For example, if I want AI to perform a full internationalization pass on my “programmer personality test” project and translate every Chinese UI element into English:

```
/目标 将 cbti-test 项目完整国际化为英文版。逐个文件替换所有中文文案为英文，每处理完一个文件就运行构建验证，直到项目能正常编译运行且界面无中文残留。
```

After about 15 minutes, AI completed the goal and even output the token usage. Compared with simply asking AI to do everything in one shot, setting a goal and letting it work step by step with automatic validation at every stage produces much more stable quality.

![](https://pic.yupi.icu/1/image-20260616135706979.png)



#### Automations

The Codex desktop app also includes an “Automations” panel, similar to Claude Code’s `/loop`, where you can configure scheduled automation tasks.

Open the Automations panel on the left, and you’ll see that Codex already includes some built-in templates, such as scheduled code-change summaries and code-issue checks.

![](https://pic.yupi.icu/1/1779342339487-c3e44a10-f14c-4d56-aa29-6c34d0a732f5.png)

You can also create your own. For example, ask AI to collect trending AI coding news every morning:

![](https://pic.yupi.icu/1/1779342400695-dd591098-4926-41ee-8cc4-966ec17e5dd6.png)

Once created successfully, Codex will automatically open a conversation at the scheduled time and execute the task. You can also run it manually once first to preview the effect:

![](https://pic.yupi.icu/1/1779327739060-7dcbe0b5-0671-4a3a-95d9-7110dde594b5.png)

Clicking the task lets you view its detailed information:

![](https://pic.yupi.icu/1/1779327610752-f322467e-2498-48c2-9ca0-09ee5534720b.png)

If you click a specific run history entry, you can even inspect the conversation for the currently executing task. I recommend observing task behavior often and continuously iterating on the prompt to improve it.

![](https://pic.yupi.icu/1/1779327672984-5d151560-bc4b-4143-b9f1-02e7f3b00b78.png)



### Implementing Loop Thinking Yourself in Cursor

Cursor does not yet have native `/goal` or `/loop` commands. But as long as you design a loop mechanism in the prompt and let AI execute commands autonomously, you can still achieve a Loop-like effect.

For example, suppose I want to use Cursor to build from scratch a desktop app called “装了吗”, which helps people learning programming install various development environments with one click. This project includes an Electron desktop app, a Python server, and a web admin dashboard, so it’s fairly complex.

![](https://pic.yupi.icu/1/01_%E8%A3%85%E4%BA%86%E5%90%97%E4%BA%A7%E5%93%81%E6%A6%82%E5%BF%B5%E5%9B%BE%EF%BC%9A%E7%94%A8%E6%88%B7%E8%BE%93%E5%85%A5%E8%BD%AF%E4%BB%B6%E5%90%8D%E2%86%92AI%E7%94%9F%E6%88%90%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC%E2%86%92%E4%B8%80%E9%94%AE%E6%89%A7%E8%A1%8C_compressed_v1.png)

I deliberately designed an autonomous development loop in the prompt so AI would not stop and wait for my confirmation, but keep running until the whole system was usable.

![](https://pic.yupi.icu/1/image-20260611162938865.png)

The key part of the prompt looked like this:

```markdown
## 自主开发循环

全程自主开发，不要停下来等我确认，除非遇到无法自行解决的阻塞问题。遵循以下循环机制：

1. 状态追踪：在项目根目录维护 PROGRESS.md，记录当前阶段、已完成事项、进行中事项、问题及解决方案。每完成一个模块就更新
2. 开发-验证闭环：每完成一个模块，立即编译运行验证，有报错就修复，通过后再推进下一个模块
3. 端到端验证：全部功能完成后，以用户视角做一次完整的端到端测试
4. 防死循环：同一个问题修复超过 5 次仍未解决，记录到 PROGRESS.md 后跳过，继续推进其他任务
```

You’ll notice that these rules map perfectly onto the three core elements of Loop we discussed earlier:

- Goal and stopping condition → “end-to-end test passes” is the stopping condition
- Feedback loop → “development-validation loop” makes AI automatically check every step
- State memory → the `PROGRESS.md` file persistently records progress

Once executed, AI began its autonomous loop. It first configured the environment, then developed the server side, desktop side, and admin dashboard in sequence. I barely intervened during the whole process. AI maintained `PROGRESS.md` itself to record progress, automatically ran tests after finishing each module, fixed errors when they appeared, and then continued.

![](https://pic.yupi.icu/1/image-20260611160046322.png)

In the end, AI spent nearly 50 minutes independently completing the entire system’s development and validation without me needing to step in halfway. All three services started normally, and the core functions ran successfully.

![](https://pic.yupi.icu/1/1781159120778-312597e0-112b-432a-9973-cc829fcbe013.png)

Open the desktop app and take a look. The main interface has an AI chat box, and below it are quick entries for common development environments:

![](https://pic.yupi.icu/1/1781154426901-1d864350-c541-4d80-8b0b-f52265aeddb9.png)

After choosing the software and version you want to install, AI automatically generates a complete installation script and solution, including Chinese comments, environment checks, and validation commands, which you can either copy and execute directly or install with one click:

![](https://pic.yupi.icu/1/1781155941607-2cdae4aa-c738-4f9d-976b-fe4572b6ecc5.png)

The web admin dashboard also runs normally. You can view installation statistics, manage all generated installation plans, and inspect user feedback data:

![](https://pic.yupi.icu/1/1781161686984-f1473317-8173-4ed6-bee0-e3f373aff1d3.png)

Pretty good, right?

This is how you can implement Loop Engineering thinking through prompt design even in a tool that has no built-in Loop commands. The core is writing **state memory + feedback loop + anti-dead-loop protection** into the prompt so AI forms the loop itself.

For the full tutorial of this project, you can read *Cursor + Claude Fable 5 - “Installed Yet?” Desktop App Project in Practice* in the “AI Cross-Platform Applications” category of this tutorial’s project practice section.



## 4. The Official Four Types of Loops

After seeing practical examples of `/goal`, `/loop`, and `/schedule`, you might start wondering: how exactly are all these things related?

In the blog post [Getting started with loops](https://claude.com/blog/getting-started-with-loops), the Claude Code team gave a very clear classification framework. They divided loops into four types according to degree of automation, from low to high:

| Loop Type | What You Hand Over | Suitable Scenarios | Tool |
|---------|-----------|------------|----------|
| Manual Loop | The validation step | Short tasks with non-fixed flows | Custom Skills |
| Goal Loop | The stopping condition | Tasks with clear completion standards | /goal |
| Scheduled Loop | The trigger timing | Periodic tasks dependent on external systems | /loop, /schedule |
| Proactive Loop | The entire prompt | Continuous, process-oriented work | All of the above + Dynamic Workflows |

Going from top to bottom, you manage less and less, and hand more and more over to AI.

![](https://pic.yupi.icu/1/05_4%E7%A7%8D%E5%BE%AA%E7%8E%AF%E9%80%92%E8%BF%9B%E5%85%B3%E7%B3%BB%E5%8F%AF%E8%A7%86%E5%8C%96%E6%80%BB%E8%A7%88%E5%9B%BE_compressed_v1.png)

The most advanced type, the “proactive loop,” combines all previous capabilities into one fully automated pipeline. For example, in a user-feedback handling scenario, you could design something like this:

```plaintext
/schedule 每小时检查一次 #project-feedback 频道的 Bug 反馈。
/goal 这一轮发现的每条反馈都要分类、处理、回复，全部搞定才能停。
修复 Bug 时，用 workflow 在并行工作树中探索三种方案，
再让一个评审 Agent 对每个方案做对抗性审查。
```

This prompt strings everything together—new feedback arrives, gets automatically categorized, bugs are fixed automatically, another agent reviews the code after the fix, and once everything passes review, the user gets an automatic reply.

The Dynamic Workflows mentioned here are an advanced Claude Code feature that lets AI write its own orchestration scripts and split large tasks across dozens or even hundreds of parallel sub-agents. For a complete introduction and technical explanation, you can read *A Detailed Explanation of AI Dynamic Workflows* in this tutorial’s AI concepts section.

At the moment, both `/schedule` and Dynamic Workflows are still in Research Preview. But from this direction, you can clearly see what the Claude Code team is trying to do: enable AI to take on larger and larger pieces of the engineering process.

That doesn’t mean you need to jump straight to proactive loops. It’s enough to start with the simplest `/goal` and choose the appropriate level according to your needs.



## 5. A Deeper Understanding of Loop’s Core Modules

From the practical examples above, you can see that getting started with Loop isn’t actually hard. Set a goal, enter one command, and it starts running.

But if you want to design a more complex and more reliable loop system—such as multiple agents collaborating in parallel, automatically connecting to external tools, or running continuously across sessions—then you need to understand the more complete methodology framework of Loop Engineering.

At present, one of the more mainstream ways the industry breaks down Loop Engineering is into five core modules, plus one layer of state memory that runs through the entire process.

![](https://pic.yupi.icu/1/09_Loop%E6%A0%B8%E5%BF%83%E6%A8%A1%E5%9D%97%E6%9E%B6%E6%9E%84%E5%9B%BE%EF%BC%9A5%E6%A8%A1%E5%9D%97+%E7%8A%B6%E6%80%81%E8%AE%B0%E5%BF%86_compressed_v2.png)



### 1. Automatic Scheduling

This is the heartbeat of Loop. Without it, the loop doesn’t run.

You set the trigger conditions and execution frequency, and the loop automatically runs at that rhythm.

For example, you can set a `/goal` that asks AI to fix every error in the project, or a `/loop` that checks once an hour whether the code repository has any new Issues to handle. The former is a one-off task, the latter is a continuous task, but both are fundamentally driven by automatic scheduling rather than manual intervention.

![](https://pic.yupi.icu/1/10_%E8%87%AA%E5%8A%A8%E8%B0%83%E5%BA%A6%EF%BC%9ALoop%E7%9A%84%E5%BF%83%E8%B7%B3%EF%BC%8C%E5%AE%9A%E6%97%B6%E6%88%96%E7%9B%AE%E6%A0%87%E9%A9%B1%E5%8A%A8_compressed_v3.png)



### 2. Work Isolation

When you want multiple AIs to work on the same project at the same time, problems can appear.

For example, suppose one agent is building the search module and another agent is building the product list module, but they both edit the homepage file at the same time. The code will conflict and turn into a mess.

The solution is to use Git WorkTree, assigning each agent its own independent working directory and branch, so they develop separately without interfering with each other and then merge back into the main branch later.

![](https://pic.yupi.icu/1/11_%E5%B7%A5%E4%BD%9C%E9%9A%94%E7%A6%BB%EF%BC%9AGit_WorkTree%E8%AE%A9%E5%A4%9A%E4%B8%AAAgent%E4%BA%92%E4%B8%8D%E5%B9%B2%E6%89%B0_compressed_v2.png)

Claude Code can launch independent worktrees through the `--worktree` parameter, and the agent panels of Cursor and Codex also include built-in support for WorkTree, so they can automatically create and manage worktrees for multiple AIs to work in parallel.

![](https://pic.yupi.icu/1/image-20260410150251832.png)



### 3. Skill Accumulation

If every new Loop has to make AI relearn your project background, coding standards, and build process from scratch, that’s a huge waste of time.

Skills turn that project knowledge and workflow into reusable `SKILL.md` documents that the loop loads automatically each time it starts. AI no longer needs to relearn everything every time—it can read the document and get to work quickly.

![](https://pic.yupi.icu/1/12_%E6%8A%80%E8%83%BD%E6%B2%89%E6%B7%80%EF%BC%9ASKILL.md%E8%AE%A9AI%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B_compressed_v2.png)

It’s just like maintaining a “project development document” inside a company so new team members can start working after reading it. The only difference is that the one reading the doc now is AI.



### 4. Tool Connectivity

A large language model is only the brain. It can think and plan, but if you don’t connect hands, feet, and tools to it, there are many things it simply cannot do.

Through the MCP protocol and various connectors, a loop can be linked to your issue tracker, database, Slack, CI/CD system, and so on. That way, if CI fails, it can inspect the error logs itself; when an issue arrives, it can classify and process it; and after the fix is done, it can even open a PR and send you a notification automatically.

Only with tool connectivity can Loop move from “only able to change code” to a full closed loop that can “discover problems, solve problems, and notify you of the result.”

![](https://pic.yupi.icu/1/13_%E5%B7%A5%E5%85%B7%E8%BF%9E%E6%8E%A5%EF%BC%9A%E9%80%9A%E8%BF%87MCP%E8%AE%A9Loop%E8%BF%9E%E6%8E%A5%E5%A4%96%E9%83%A8%E5%B7%A5%E5%85%B7%E5%BD%A2%E6%88%90%E5%AE%8C%E6%95%B4%E9%97%AD%E7%8E%AF_compressed_v2.png)



### 5. Sub-Agent Cross-Review

If you let one model generate code and then ask that same model whether the code is good, it will most likely say yes. It’s like a student grading their own exam paper—they’re bound to go easy on themselves.

So in a loop, you generally assign at least two roles. One agent writes the code, and another agent is dedicated to running tests and reviewing the code. The second agent operates with completely different context and instructions from the first. It only cares whether the code has bugs and whether the logic is correct, so it isn’t influenced by the thinking path of the code-writing agent.

![](https://pic.yupi.icu/1/14_%E5%AD%90%E4%BB%A3%E7%90%86%E4%BA%92%E5%AE%A1%EF%BC%9A%E5%86%99%E4%BB%A3%E7%A0%81%E7%9A%84%E5%92%8C%E6%A3%80%E6%9F%A5%E4%BB%A3%E7%A0%81%E7%9A%84%E5%88%86%E5%BC%80_compressed_v1.png)



### State Memory

During operation, a loop produces a lot of intermediate state, such as which files have already been processed, what the conclusion of the previous round was, and what step the current progress has reached.

That information cannot exist only in the AI conversation window, because conversation windows are limited and disappear once closed.

You can record progress in an external file such as `PROGRESS.md`. Each time an agent starts a new round of the loop, it first reads the progress to understand the current state, then updates it after finishing the work. Even if the process breaks and restarts midway, it won’t need to start from zero.

![](https://pic.yupi.icu/1/15_%E7%8A%B6%E6%80%81%E8%AE%B0%E5%BF%86%EF%BC%9APROGRESS.md%E6%8C%81%E4%B9%85%E5%8C%96%E8%AE%B0%E5%BD%95%E8%BF%9B%E5%BA%A6_compressed_v3.png)

Among these five modules, **automatic scheduling** and **state memory** are the most fundamental and the ones we already touched in the practical examples. The other modules—work isolation, skill accumulation, tool connectivity, and sub-agent cross-review—are more advanced optimizations that become useful after the basic loop is already running. Use them as needed; you don’t need to configure everything from the very beginning.



## 6. Notes and Learning Advice

Every time a new technology appears, people start saying things like “XX is dead.” This time is no different. Plenty of people are shouting that prompt engineering is dead and Loop Engineering is the future!

But the truth is that Loop does not replace prompts. It is built on top of prompts, context, and Harness.

If the basics are not solid, running a loop only amplifies the problems.

Let’s talk about several things you need to watch out for when using Loop in practice.



### Token Consumption Can Be High

Every loop iteration is a full prompt execution. If you set it to run once per minute for 24 hours straight, that means 1,440 AI calls.

Think about the two big names strongly recommending Loop Engineering: one is an Anthropic engineer, and the other has OpenAI-level resources behind him. They experiment with their own company’s models and get the token bill reimbursed, so the cost is basically zero. But for ordinary developers, a $20-per-month subscription plan simply can’t support high-frequency loops.

**It’s not the loop that’s running—it’s your wallet!**

Someone in the comments once challenged Peter: you people have unlimited token supply, but I don’t!

Peter replied: true, but is your time really worthless?

That line reminds us to think in terms of **cost-performance ratio**. If a `/goal` task costs 30 yuan in tokens but saves you 3 hours of manual work, that’s probably worth it. But if it burns 100 yuan and still fails, forcing you to rework everything manually, then you simply wasted money.

So before starting a loop, think clearly: can the goal be quantified? Is it worth running? Don’t let your AI employee work for nothing.

The Claude Code team also gave some very practical money-saving advice:

1. **Choose the right tools and models**: simple tasks do not need multiple agents or complex loops, and some tasks are fine with cheaper, faster models. Routine tasks can be routed to smaller and faster models, reserving the strongest model for critical stages that need judgment.
2. **Write specific stopping conditions**: the clearer the condition, the faster AI can converge on the correct result. Fewer detours means less cost.
3. **Trial on a small scale before rolling out fully**: Dynamic Workflows can launch hundreds of agents at once, but if you run everything at full scale immediately, the token cost will be terrifying. Try a small subset first.
4. **If a script can handle it, don’t spend AI reasoning on it**: deterministic operations such as batch renaming files, formatting JSON, or running data migrations are better done by letting AI execute a script directly instead of having it re-reason from scratch every time.
5. **Don’t set the loop frequency too high**: the interval should match how often the monitored thing actually changes. There’s no point checking every minute for something that only updates once a day.
6. **Use the `/usage` command to see where the money went**: this command breaks recent usage down by Skills, Subagents, and MCPs. If one agent is burning money too aggressively, you can stop it at any time.



### Debugging Is 10 Times Harder Than Debugging a Prompt

Some developers say: everyone is rushing toward loops, but debugging a state machine that has already run for 47 rounds is 10 times harder than fixing one prompt!

That’s true. Once a loop goes off track, it’s hard to locate which round caused the issue. So in the beginning, always start with simple loops. Set smaller goals and write clearer stopping conditions. In each round, have AI clearly record what it did and what result it got so you can trace things afterward.



### Overbaking

If a loop runs too long and the goal constraints are too loose, AI may start “adding drama.” For example, it may add encryption features nobody needs, over-split the file structure, or even delete test cases just to make the tests pass.

This phenomenon was first discovered by the community in early Ralph Wiggum Loop practices. Ralph was a predecessor of Loop Engineering. Some people used it to keep letting AI refactor a codebase in a loop, and after it ran too long, AI began adding random features and deleting tests. The community vividly called this phenomenon Overbaking.

A more stable approach is to write a clear requirement document that explicitly lists what the loop should do and what it should not do. You should also set a reasonable upper limit on the number of loop iterations, and after it finishes, review the result manually rather than merging blindly.



### Maintain Code Quality

Even if the loop runs beautifully, if the quality of code produced in each round is poor, then all the token spending is wasted. The Claude Code team summarized several practical points:

1) **Keep the repository itself clean and tidy.** AI imitates the patterns and standards already present in the codebase. If your repository is a mess, the code it writes won’t be much better.

2) **Use Skills to give AI a way to verify its own work.** The more quantifiable the checking standard, the better. Ideally it should run scripts, inspect screenshots, test performance, and so on, instead of just “feeling” that the code is fine. AI’s feelings are not reliable.

3) **Place framework and library documentation somewhere AI can find it.** It may not know the latest best practices, but if you provide the docs, it can refer to them while writing. This is exactly why web-search capability and MCP plugins like Context7, which can automatically fetch up-to-date documentation, are becoming more and more important.

4) **Use a second agent for code review.** Let different agents write and review the code. The reviewer gets a fresh context and won’t be influenced by the thinking path of the coding agent. Claude Code even includes a built-in `/code-review` skill that you can use directly. And if your code is hosted on GitHub, you can also combine it with GitHub’s own Code Review feature for double checking.

There’s also one very important principle: when the result of a certain loop is not up to standard, don’t just fix that one issue and move on. Encode the lesson from that failure back into the system, for example by updating a Skill or rule file, so future iterations no longer make the same mistake. Over time, quality becomes more and more stable.

![](https://pic.yupi.icu/1/10_AI%E7%BA%A0%E9%94%99%E6%B2%89%E6%B7%80%E6%AD%A3%E5%90%91%E5%BE%AA%E7%8E%AF_compressed_v2.png)



### Learning Path

If you’ve just started with AI coding and are still using Vibe Coding-style conversations to let AI write code, then don’t rush into Loop yet. First, practice your prompt skills and learn how to use `AGENTS.md` to give AI enough context. That is the most basic and most important step.

Once you can use AI to complete full features but often still need to manually steer it back on track, then it’s time to learn Harness Engineering. Equip AI with tools, write tests, and set up architecture constraints so it can work in a reliable environment.

Once those foundations are in place, if you really want to start using Loop, it’s enough to begin with a lightweight method like `/goal`. Give AI a small goal and let it run one round on its own, so you can feel the effect and the token consumption. After confirming that it behaves as expected, you can gradually add scheduled loops, anti-dead-loop mechanisms, tool connectivity, and other advanced capabilities, step by step, until you have a more complete loop system.

If you want to systematically learn the knowledge from the earlier stages, you can read *A Beginner-Friendly Guide to Harness Engineering* in this tutorial’s experience and tips section. It gives a complete explanation from concept to practice.



## Final Thoughts

To sum up, from prompt engineering to Loop Engineering, AI coding is becoming more and more automated, and it really is freeing up our hands and attention step by step.

In the past, one whole afternoon might be spent staring at AI while it completed one feature. Now, once you start `/goal`, you can go do more valuable things—like getting a bit more sleep. By the time you come back, AI may already have finished several hours of work for you.

But no matter how powerful the tool becomes, you are still fundamentally the one making the decisions. Whether the loop is well designed, whether the goals are clearly broken down, and whether the feedback mechanisms are reliable enough—all of that depends on your own engineering ability and understanding of the project.

Loop is an amplifier. It can amplify your ability, and it can also amplify your laziness.

**Use it to accelerate work you truly understand. Don’t use it to escape thinking itself.**
