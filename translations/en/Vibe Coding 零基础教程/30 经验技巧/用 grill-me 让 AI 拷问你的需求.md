# Use grill-me to Let AI Grill Your Requirements

> A god-tier Skill ranked top 3 in installs across the internet, and its core content is only a few sentences

Hello everyone, I’m Yupi.

Recently, a Skill has become extremely popular. It has already been installed more than 600,000 times and even reached No. 3 on the “Skill Installation Leaderboard.”

**But can you believe that the core content of this Skill is literally just a few sentences?**

It’s `/grill-me`, a skill that lets AI question you in reverse.

![](https://pic.yupi.icu/1/image-20260723152045658.png)

At a time when new Skills are appearing nonstop and competition is as intense as the state of my hairline, how did a Skill with only a few lines manage to stand out?

In this article, I’ll first introduce the skill, then show you what it can do through a real project example, and finally analyze the thinking behind it. I think it’ll give you some inspiration for AI coding.



## What grill-me Is

What people call a Skill is basically a set of operating instructions written for AI. Once installed, it lets AI carry out tasks according to a specified process. If you’re not yet familiar with Skills, I recommend first reading *Agent Skills: A General AI Skill Library* in the “Tool Practice” section of this tutorial’s programming tools module.

The grill-me skill has **only one file**, and the entire content of that file is exactly what you see below.

![](https://pic.yupi.icu/1/image-20260723152345728.png)

Translated, it means this:

> For my plan, keep asking about every detail until we reach a shared understanding. Walk down every branch of the decision tree and sort out the dependencies between decisions one by one. Some choices can only be answered after the previous question is settled, and the AI should ask them in that order. Every question should include your recommended answer.
>
> Ask only one question at a time, and wait for my answer before asking the next. Throwing a pile of questions at once overwhelms people.
>
> If facts can be found by checking the environment (file system, tools, etc.), go look them up directly instead of asking me. But decisions are mine to make, and every decision needs my approval.
>
> Do not begin acting until we confirm that both sides understand each other.

You might be wondering: can something this short really count as a Skill? Isn’t it basically just a prompt? Can it really work?

Come on, let’s try it on a real project.



## A Real-World Trial

First, install grill-me. Open a terminal and run one command:

```bash
npx skills add https://github.com/mattpocock/skills --skill grill-me
```

![](https://pic.yupi.icu/1/image-20260723153039655.png)

After installing it, open any AI coding tool you like. I’ll use Cursor here as an example.

I gave AI a very vague requirement and used the `/grill-me` skill:

![](https://pic.yupi.icu/1/image-20260723163922362.png)

Run it! AI thought for a moment, then started grilling me step by step.

First, AI asked what exactly I meant by the thing I wanted to build, and it also gave me its suggestion. I didn’t even need to organize the requirement myself. I could just reply, “Your suggestion is correct.”

![](https://pic.yupi.icu/1/image-20260723160208826.png)

Then AI asked what form I wanted the thing to take and provided several options. I felt a web app would be more convenient, so I just entered option 3.

![](https://pic.yupi.icu/1/image-20260723160307350.png)

Next, AI asked what features I needed. Normally, it would make sense to start with the core features first, but I felt these requirements weren’t too complicated and AI could probably handle them all in one go, so I got greedy: I wanted everything!

![](https://pic.yupi.icu/1/image-20260723160350655.png)

Once the requirements were clear, AI began asking about the technical solution. Here I chose an Electron desktop app, because it can directly access local files and is more convenient to use.

![](https://pic.yupi.icu/1/image-20260723160407860.png)

After that, AI started confirming specific technical details with me one by one, such as which development framework to use, which component library to pick, how to store data, and so on.

![](https://pic.yupi.icu/1/image-20260723160433659.png)

If you don’t understand the technologies AI mentions, or you don’t have any strong opinion, just follow AI’s recommendation.

“I accept your suggestion” may have been the sentence I said most often during the whole process.

![](https://pic.yupi.icu/1/image-20260723160454385.png)

After more than ten rounds of Q&A, AI had forced me to think through a lot of details I hadn’t considered at all before. In the end, it gave me a complete solution summary, and once I confirmed it, development started.

![](https://pic.yupi.icu/1/image-20260723160528631.png)

After confirming, I told AI to start writing code directly. Because the requirements and solution had already been discussed clearly enough beforehand, the coding process was much smoother than simply asking it to guess my needs from the start.

![](https://pic.yupi.icu/1/image-20260723160626764.png)

In about 10 minutes, a desktop app for managing Skills was done.

![](https://pic.yupi.icu/1/image-20260723161102168.png)

Looking back at the whole process, you’ll notice that this is basically the classic enterprise development workflow:

Start from a vague idea, clarify the requirements first, list the feature points, confirm the technical choices and design plan, and only then begin development.

The difference is that before, this process required product managers, architects, and developers to sit down and discuss together. Now AI handles the whole thing, and the experience feels like having an experienced technical mentor guiding you step by step until everything is clear.



## The Thinking Behind It

Now that you’ve seen the experience, let’s break down the design of grill-me. It may only be a few short sentences, but there are actually several layers of thinking hidden inside. That’s the real reason it became so popular.

**First, it targets the most critical stage in AI coding.**

AI is already very capable at writing code. If you give it a clear requirement, most of the time it can build it. But when most people ask AI to write code, they themselves haven’t really thought through what they want. So AI can only guess, and if it guesses wrong, everyone ends up reworking things again and again. What grill-me does is force the requirements to become clear before development starts.

**Second, the way it asks follow-up questions is highly structured.**

It follows the logic of a decision tree. A decision tree means breaking one big problem into a series of choices, confirming one answer first and then using that answer to determine the next question. Each step connects to the next, which greatly reduces the chance of missing important details. It also insists on asking only one question at a time, instead of dumping a whole pile on you and leaving you lost.

**On top of that, the division of labor between human and AI is very clear.**

If something can be found in the project files or tools, AI looks it up itself instead of wasting your time. It only stops to ask when the answer involves a design decision that you need to make.

The requirement to “give a recommended answer” was something the author intentionally added later. If AI gives no suggestion, you still have to think for quite a while about how to answer. But once a recommended answer is included, if you agree, you can just say yes, which makes the conversation much more efficient.

![grill-me 的四层设计思想](https://pic.yupi.icu/1/01_grill-me%E5%9B%9B%E5%B1%82%E8%AE%BE%E8%AE%A1%E6%80%9D%E6%83%B3%E5%85%A8%E6%99%AF%E5%9B%BE_compressed_v2.png)

This skill reminds me of the classic “rubber duck debugging” method in programming, where you place a rubber duck on your desk and explain your thinking to it step by step. As you talk, you often discover the holes in your own reasoning. grill-me is like giving you a smart cyber duck that asks follow-up questions, makes recommendations, and can even look things up on its own.



## Final Thoughts

**No matter what you’re doing, the act of clearly explaining your thinking is itself the most valuable part**, and grill-me turns that into an executable process.

It’s useful not only for AI coding, but also for any everyday scenario where you need to make decisions: planning a learning path, choosing a computer setup, making a health plan, and so on. You can use the same way of thinking and let AI grill you there too.

![比如鱼皮用它来研究怎么让脑袋长毛](https://pic.yupi.icu/1/image-20260723170216222.png)

Trust me, once you use it enough, you’ll fall in love with the feeling, and it’ll also make your logical thinking much clearer.

grill-me comes from an open-source Skills repository with 180,000 stars. It also contains equally useful skills for test-driven development, bug diagnosis, large-project planning, and more. If you’re interested, you can read *Matt Pocock Skills: A Real Engineering Skill Library* in the “Tool Practice” section of this tutorial’s programming tools module.
