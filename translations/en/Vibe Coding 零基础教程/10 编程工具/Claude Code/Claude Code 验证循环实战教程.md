# Claude Code Verification Loop Practical Tutorial

> Let AI verify its own code after writing it: the principles and hands-on practice of the verification loop

Hello everyone, I’m programmer Yupi.

Recently, Claude’s official team published a blog post specifically about how to let Claude Code check the code it writes itself. Officially, they call this the **Verification Loop**.

Simply put, after AI finishes writing code, it doesn’t immediately turn it in. Instead, it first runs a round of checks on its own work. If there are problems, it keeps fixing them, checks again after each fix, and forms a loop—only delivering the result to you after everything passes.

> Original article: [https://claude.com/blog/building-verification-loops-in-claude-code-with-skills](https://claude.com/blog/building-verification-loops-in-claude-code-with-skills)

![](https://pic.yupi.icu/chengfang/1786413234706-10e92ec5-2867-4fc4-bdc7-207583033002.png?imageSlim)

That said, AI really does write code fast now. But every time it confidently tells me “done,” I still have to open the page myself, test each feature one by one, switch to mobile view, and then open the browser console to see whether there are errors.

The code is written by AI, so why does final acceptance still end up being my job?

So I wanted to try it for real and see whether Claude’s official verification loop can actually reduce the amount of work I personally have to do.

![](https://pic.yupi.icu/chengfang/2.jpeg?imageSlim)



## What Is a Verification Loop?

During development, Claude Code already performs some basic checks by default, such as:

- type checking, to confirm that variable types are correct  
- code style checks, such as whether you forgot semicolons or made similar low-level mistakes  
- automated tests, by running the preset test cases  
- runtime errors, to see whether the code can actually run stably

All of these checks can produce clear pass/fail results, so AI can keep modifying the code based on those results.

However, these basic checks can’t cover every final effect. For example, whether the mobile layout is broken, whether a button is actually clickable, or whether some part of the page is badly overlapped—these issues can’t be discovered just by running code-checking tools. In the end, someone still has to open the page and look at it directly.

So when I normally develop with AI, my workflow is usually this: first let AI finish the code and run some basic checks, then I personally operate the product once. If I discover issues, I tell AI what is wrong, and it keeps fixing it.

But with a Verification Loop, even that later manual acceptance part can be handed over to AI. Let AI verify it, let AI modify it, and only after everything passes does it hand the result to me.

![](https://pic.yupi.icu/chengfang/01-AI.png?imageSlim)

Of course, just telling AI “check it yourself” is not enough. It needs to know **what exactly to check**, and it also needs a clear result that can tell it whether the outcome is really pass or fail.

On this point, Claude’s official team mentioned several built-in verification approaches:

+ the `/verify` skill, which lets AI build the project, run it, and observe whether the changes have issues  
+ the toolchain, meaning the project’s existing tools such as linters and other checks, so AI can directly read the errors and warnings those tools return  
+ Code Review, an automated multi-Agent review service that can run a review automatically on a PR  
+ GitHub Actions, which triggers checks automatically when code is committed  
+ Spec validation, which verifies changes against the project’s specification documents  
+ Rubrics, which score the result according to evaluation criteria and send it back for rework if it fails

You don’t need to memorize these names. The core idea is the same in all cases: **give AI a clear verification result so it can tell whether the attempt passed or failed.** Whether the program can run correctly, whether tests pass, and whether a code submission has issues all fall into this kind of clearly judgeable outcome.

Even project-specific rules can be turned into acceptance conditions.

You might ask: what exactly are project-specific rules?

Here’s an example. Suppose a database migration needs to delete a column, but the data was not backed up beforehand. Then the change should directly be judged as a failure.

This kind of rule is defined by your own project. General code-checking tools have no idea about it, but it can still be written into the verification flow so that AI always checks against it.

![](https://pic.yupi.icu/chengfang/02-AI.png?imageSlim)



## Fix the Verification Loop into a Skill

If what you need to repeat each time is not just one or two rules but an entire set of checks, then you can organize them into a Skill.

A Skill is essentially a Markdown file. Inside it, you describe the checking process clearly in natural language and put it under the project’s `.claude/skills/` directory. The next time a similar task appears, AI can follow that process directly without you having to teach it all over again.

The official recommended path for getting started looks like this:

1. Start with the single manual check you repeat most often. For example, try Claude Code’s built-in `/verify` skill. After you enter that command, AI will build the project, run it, and check whether the changes have any problems.  
2. If that still isn’t enough, write your own. You can describe the checking process in natural language and hand it over to the `skill-creator` plugin, which will understand your workflow and automatically generate the corresponding Skill file. Of course, you can also just write a Markdown file by hand and put it in the skills directory.  
3. Try it out on a new task. Wherever it feels awkward, keep iterating. Once a single check becomes stable, then try chaining multiple checks together.

![](https://pic.yupi.icu/chengfang/03-AI.png?imageSlim)

A simple Skill file looks like this:

```yaml
# .claude/skills/verify-log-hygiene/SKILL.md
---
name: verify-log-hygiene
description: 检查错误日志是否包含请求 ID，并且不能泄露请求体内容。
---
读取当前代码改动中的错误处理路径。

对于每一个错误路径上的日志调用，确认它包含了请求 ID，
并且没有把请求体、请求头、或用户提交的任何数据写进日志。

逐条报告违规项（标注文件名:行号），然后修复它。
```

The Skill above checks logging conventions. As you can see, it’s just a YAML header (name and summary) plus a few natural-language instructions explaining what AI should inspect, how it should judge correctness, and what it should do when it finds a problem. It’s not as complicated as it sounds. At its core, you’re just writing down in text the checking process that already exists in your own head.

For example, when I review frontend pages, I repeatedly check page loading, core interactions, mobile adaptation, and the browser console. It’s always the same workflow. So this time I simply wrote them into a `verify-frontend` Skill and let AI accept its own work against that checklist.

![](https://pic.yupi.icu/chengfang/6.png?imageSlim)

But note that **Verification Loop is the core idea; Skill is only one way to implement it**. You can also use Hooks (scripts automatically triggered at specific moments) to achieve similar effects, or even use the `/goal` command to define an end condition so AI keeps looping until the condition is satisfied.



## Practical Test — Does the Loop Actually Help?

After all that talking, does this thing actually work?

I decided to design a comparison experiment and find out.

Using the same project and the same requirements, in the first round I let AI develop normally and then I performed manual acceptance. In the second round, after AI finished development, I made it run a Verification Loop to accept its own work. Then I compared whether this verification loop could actually save me effort in real development.

Originally I wanted to run the experiment in Claude Code using Claude’s own model, but my Claude account had long since been banned...

<img src="https://pic.yupi.icu/chengfang/1786431474389-948c82a1-921e-44b1-8e42-54b26a412b93.jpeg?imageSlim" style="zoom:50%;" />

So this time I had no choice but to connect Claude Code to DeepSeek for the test. If you want to know how that connection is done, read *Connecting Claude Code and Codex to Domestic Models* in the Claude Code directory of this tutorial’s programming tools section. I won’t expand on that here.

As for the project, I chose the recently popular bamboo cicada toy.

I directly gave AI a few reference images and asked it to build a 3D cyber-style bamboo cicada.

The initial version of the page only had the bamboo cicada model itself, slow auto-rotation, and a title.

![Initial version of the bamboo cicada](https://pic.yupi.icu/chengfang/%E7%AB%B9%E7%9F%A5%E4%BA%86%E5%88%9D%E5%A7%8B%E7%89%88%E6%9C%AC.png?imageSlim)

Then I gave AI five requirements:

```plain
1. 鼠标拖动控制竹知了的旋转和朝向
2. 普通 / 狂暴模式切换
3. 狂暴粒子光效
4. 375px 移动端适配
5. 整体视觉完善
```

To keep things as fair as possible, both rounds started from the exact same initial version, used the same DeepSeek model and tool environment, and each round was run in a completely new Claude Code session.

At the same time, to ensure fairness, before the first round even started I had already fixed the six categories of acceptance checks that I would use in round two, so I wouldn’t be tempted to add rules afterward based on what I saw in round one.

![Left: normal development, right: verify-frontend Skill](https://pic.yupi.icu/chengfang/1786418711345-bfcfaef7-69ea-490a-8991-117f9b730138.png?imageSlim)



### Round 1: Normal Development

In this round, I used my usual workflow. I didn’t tell AI to perform any extra testing, and I didn’t ask it to run the `verify-frontend` Skill.

After 5 minutes and 33 seconds, Claude Code declared the task complete. All five requirements had corresponding implementations, and the AI even proactively checked whether the project could build successfully.

![](https://pic.yupi.icu/chengfang/11.png?imageSlim)

Let’s look at the result AI created.

The “dragging the bamboo cicada” effect I had in mind was like swinging the stick in your hand, with the string responding to gravity and inertia, so the bamboo cicada below sways along with it, maybe with a fun “wah wah wah” sound effect too. Lovely.

![Round 1 bamboo cicada in normal mode](https://pic.yupi.icu/chengfang/%E7%AC%AC%E4%B8%80%E8%BD%AE%E6%99%AE%E9%80%9A%E7%8A%B6%E6%80%81%E4%B8%8B%E7%AB%B9%E7%9F%A5%E4%BA%86.png?imageSlim)

But AI completely misunderstood it. What it built was direct control over the whole cicada model when you held down the mouse and dragged.

I was about to complain, but then I looked back at my own requirement.

![](https://pic.yupi.icu/chengfang/12.png?imageSlim)

Fair enough. That one really wasn’t AI’s fault.

I only wrote “use mouse dragging to control the bamboo cicada’s rotation and orientation.” I never mentioned the string, gravity, inertia, or any of that.

![](https://pic.yupi.icu/chengfang/13.png?imageSlim)

After AI declared it complete, I still manually accepted it the old-fashioned way. Most features basically worked, but the berserk mode effect still didn’t match my expectations. The rotation really did get faster, but the particle and lighting effects were not obvious enough. If you only looked at the screenshot, it hardly looked different from the previous one.

![Round 1 bamboo cicada in berserk mode](https://pic.yupi.icu/chengfang/14.png?imageSlim)

I also found two yellow warnings sitting in the browser console. In simple terms, the 3D rendering library Three.js was warning that two old usages are no longer recommended. The project could still run for now, so they didn’t affect this acceptance pass.

![](https://pic.yupi.icu/chengfang/15.png?imageSlim)

So to summarize this round: AI spent 5 minutes and 33 seconds writing the code, and then I spent about 2 more minutes manually accepting it—clicking interactions, switching modes, testing 375px mobile view, and finally opening the browser console to check for errors.



### Round 2: Let AI Handle Acceptance Too

For round two, I rolled the code all the way back to the original bamboo cicada version—the one with only the model and slow auto-rotation—so that both rounds had exactly the same starting point.

The original five functional requirements were left unchanged. I only added one extra sentence:

```plain
开发完成后必须执行 verify-frontend Skill，全部通过后才能宣布完成。
```

This time, AI not only had to write the code, it also had to carry out the acceptance work that I would normally do myself.

Remember the six categories of checks I fixed before the experiment started?

+ whether the project can build successfully  
+ whether the page opens correctly  
+ whether core interactions work  
+ whether 375px mobile layout has issues  
+ whether the browser console has errors  
+ whether the page has obvious misalignment, overlap, or clipping

![](https://pic.yupi.icu/chengfang/16.png?imageSlim)

To let AI actually operate the page, I gave it two tools this time.

1. Playwright is a browser automation testing framework. You can think of it as AI’s **hands**, helping it open pages, drag the model, click buttons, and perform real interactions.  
2. Vision capability is AI’s **eyes**, allowing it to take screenshots and understand what the page looks like, including whether there is obvious misalignment, overlap, or clipping. You can use the open-source [multimodal vision recognition Skill](https://github.com/asuojun/claude-vision-skill) from GitHub.

![](https://pic.yupi.icu/1/image-20260803155552049.png)

After AI finished writing the code, it automatically ran the acceptance flow.

There was a small hiccup in the middle: Playwright initially failed because some dependencies weren’t installed correctly. But this kind of small problem didn’t require any human intervention. AI found the cause itself, fixed the dependencies, and continued with acceptance.

![](https://pic.yupi.icu/chengfang/17.png?imageSlim)

In the end, according to the rules I had defined before the experiment, all six categories of checks passed.

![](https://pic.yupi.icu/chengfang/18.png?imageSlim)

This round took a total of 9 minutes and 48 seconds. And from the quality perspective, the particle effects in round two’s berserk mode really were much cooler than in round one.

![Round 2 bamboo cicada in “berserk” mode](https://pic.yupi.icu/chengfang/%E7%AC%AC%E4%BA%8C%E8%BD%AE%E3%80%8C%E7%8B%82%E6%9A%B4%E3%80%8D%E6%A8%A1%E5%BC%8F%E4%B8%8B%E7%9A%84%E7%AB%B9%E7%9F%A5%E4%BA%86.png?imageSlim)

In the final acceptance report, AI also recorded a build warning saying the bundled file size exceeded 500 KB. Pretty attentive, honestly.

![](https://pic.yupi.icu/chengfang/20.png?imageSlim)

However, just like in round one, when I opened the browser console myself, those same two warning messages were still there.

![](https://pic.yupi.icu/chengfang/19.png?imageSlim)

That reminded me of something: if you really want to hand acceptance over to AI, it’s not enough just to tell it **what** to check. You also need to clearly specify **how** it should check it—for example, whether it should inspect screenshots or read console logs—how it should categorize and record abnormalities, and how it should report them completely in the final report. If any part of that chain is underspecified, you may end up with blind spots where problems exist but are never reported.



## Comparison Results of the Two Rounds

According to the rules fixed before the experiment, both rounds passed acceptance, and neither round found any business bug that affected functionality.

What truly changed was **who performed the acceptance work**.

In round one, after AI finished writing the code, I personally clicked, looked, and tested everything myself.

In round two, before AI declared the task complete, I did not intervene in the acceptance process at all. It ran the entire workflow by itself.

The cost was that round two took over 4 minutes longer in total. But during those 4 extra minutes, I didn’t need to sit there clicking the screen manually one by one. I could go drink some water, slack off for a bit, or even do a set of pelvic floor exercises, then come back and directly read the result. That, to me, is where the Verification Loop really becomes valuable.

Of course, “passing acceptance” and “fully matching expectations” are still two different things. Like the berserk mode in round one: the feature technically existed, but whether it felt berserk enough and whether the visual effect was satisfying still required human judgment.

So I think the things best suited to being handed to AI first are the tasks that have clear right-or-wrong outcomes and are repeated every single time—such as whether the project builds, whether core interactions work, whether the mobile version has adaptation issues, and whether there are browser console errors.

As for whether an animation is too fast, whether the page is attractive enough, or whether the bamboo cicada really has that childhood feeling when you swing it around—those are subjective matters of aesthetics and product feel, and in the end humans still need to make the call.

In the AI era, aesthetics and judgment are the scarcest human abilities.



## What Else Can You Do with a Verification Loop?

This time, I only ran acceptance once after AI finished development. But a Verification Loop doesn’t have to sit only at the last step.

Once this acceptance method has been tried on real tasks several times and proven reliable enough, it can be embedded directly into your daily development workflow—or even chained together with other checks into a full pipeline.

Claude’s official team summarizes these uses into four run modes:

![](https://pic.yupi.icu/chengfang/04-AI.png?imageSlim)

1) **Standalone**

Trigger it manually when needed. For example, run a security scan right before submitting code.

2) **Embedded inside another Skill**

Write the verification step directly at the end of a production Skill. For example, if you have a Skill that automatically creates React components, you can add one line at the end: “After creation, run an eslint check.” Then every time that Skill is used, verification happens automatically too.

3) **Chained**

Connect multiple Skills end to end so that once one finishes, the next one automatically starts.

This is actually how Anthropic’s own Claude Code team uses it internally. First they run `/code-review` to find bugs, then `/simplify` to clean up the code, then `/verify` to confirm functionality is correct, and if the change involves UI, they finally use a custom `/design` Skill to compare it against design guidelines.

Once those four steps finish, you have a fully automated code quality assurance workflow. Developers only get notified when one of the steps fails and human intervention is required.

![](https://pic.yupi.icu/chengfang/05-AI.png?imageSlim)

4) **Run automatically on every PR**

Once the chained workflow runs stably in your own development, you can attach it to GitHub Actions. That’s GitHub’s automation pipeline service.

Then anytime anyone on the team submits a pull request, the same verification checks run automatically. You no longer need to rely on every individual developer remembering to run them manually, and code quality gets a unified minimum standard.

By the way, Boris Cherny, the creator of Claude Code, said something in June this year that really stuck with me: *I no longer manually write prompts for AI. My job now is to design loops, and let the loops instruct AI what to do.*

![](https://pic.yupi.icu/1/loop%20engineering.png)

This idea is called **Loop Engineering** in the developer community. The core idea is that humans move from “telling AI what to do one instruction at a time” to “designing a system that lets AI operate on its own,” and the Verification Loop is one of the most important parts of that system.

![](https://pic.yupi.icu/1/01_Loop_Engineering%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5%EF%BC%9A%E4%BD%A0%E8%AE%BE%E8%AE%A1%E7%B3%BB%E7%BB%9F%E8%AE%A9%E5%AE%83%E4%BB%A3%E6%9B%BF%E4%BD%A0%E7%BB%99AI%E4%B8%8B%E6%8C%87%E4%BB%A4_compressed_v1.png)

For more on Loop Engineering, you can read *Loop Engineering Beginner-Friendly Tutorial* in the practical tips section of this tutorial.



## Final Words

By this point, you should have a good feel for what the Verification Loop is useful for.

If you want to use AI to build large complete projects, my suggestion is: besides giving AI a requirements list, also give it an acceptance checklist.

For the kinds of checks you repeat every single time, if AI can run them once first, then there’s no need for you to manually start over from scratch each time.

Thanks to this method, I’ve recently used AI to build quite a few complete works with ease, and I’ve already recommended it to a lot of people~

For example, the game-tracking tool below:

![](https://pic.yupi.icu/1/image-20260812144301650.png)

If you also have a repeated post-coding checklist that you run every time, try turning it into a Skill. If you’re too lazy to write it from scratch, you can use the official `skill-creator` plugin. It interviews you about your usual workflow and then generates it automatically.

That said, if AI can check code by itself now, what do we still need programmers for?

The answer is simple: **taking the blame** (kidding... kind of).

AI passing acceptance does not mean everything is fine. It can only cover the parts with clearly judgeable outcomes. If something goes wrong after release, who defined the requirements, who wrote the acceptance criteria, and who made the final launch decision—AI is not taking responsibility for those.

AI is a great executor and inspector, but it is not the decision-maker, and certainly not the accountable party.

So don’t imagine that a “one-person company” is all effortless. You just don’t see the human behind the scenes getting tortured by AI over and over again and yelling at the screen.

A person who can make judgments and take responsibility, plus an AI that never gets tired and executes relentlessly—that is still the most reliable combination we have right now.
