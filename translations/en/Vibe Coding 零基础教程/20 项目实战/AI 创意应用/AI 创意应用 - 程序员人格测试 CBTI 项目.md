# AI Creative Application - Programmer Personality Test CBTI Project

This project is a programmer-exclusive personality test website called CBTI (Coder Behavior Type Indicator). It uses 30 fun programming-related questions to determine your coding personality type. The whole thing was built with Cursor + Claude through Vibe Coding and finished and launched within an hour.

Online demo: https://cbti.codefather.cn

Project code is free and open-source: https://github.com/liyupi/cbti-test

Hello everyone, I’m Yupi.

You’ve probably heard of the MBTI personality test, right?

Unexpectedly, in the last few days, a website imitating MBTI suddenly went viral. It’s called “SBTI.”

It also uses 30 multiple-choice questions to determine your personality type, except the results are... much more abstract.

For example, I tested as “Holy-Crap Guy.” Maybe I’m still not abstract enough? I couldn’t even understand the explanation for that personality type...

![](https://pic.yupi.icu/1/image-20260413134621011.png)

After seeing it, my first thought was: what the heck? Why did this site go viral? Isn’t making a little quiz website like this with AI coding easy now? Why don’t I make one too?

So I got to work immediately. In about an hour, I used AI coding to build a programmer-exclusive **CBTI (Coder Behavior Type Indicator)** programmer behavior test.

👉🏻 Online demo: https://cbti.codefather.cn

![](https://pic.yupi.icu/1/image-20260413135126605.png)

It uses 30 questions to determine your coding personality, and the code is fully open-source.

👉🏻 Open-source repo: https://github.com/liyupi/cbti-test

![](https://pic.yupi.icu/1/image-20260413135149352.png)



## What Is CBTI?

First, let me officially declare that CBTI is a serious test with scientific grounding, not just some abstract meme project!

I had AI deeply analyze MBTI and SBTI question banks, scoring logic, and the MBTI 16personalities personality system, then used that as the basis for designing CBTI’s dimensional model. The full test covers 5 major directions—code quality, bug handling, teamwork, tech-driven behavior, and attitude toward AI—with a total of 15 dimensions.

Let me show you a few sample questions so you can get the idea:

1) Product says: “Ship it first, optimize later.” What are you thinking?

- Later means which lifetime? Fine, just patch it in for now
- Write a TODO, even though it’ll probably become my last words
- Write a technical proposal and schedule it into an iteration

![](https://pic.yupi.icu/1/image-20260413135743602.png)

2) Friday 5:59 PM, a message pops up in the group chat: production is down. You?

- Pretend I didn’t see it, mute my phone, disappear from the planet
- First check how serious it is
- Instantly reply “I’ll take a look” and open the monitoring panel

![](https://pic.yupi.icu/1/image-20260413135805157.png)

And since AI coding is so hot right now, I also kept up with the times and added related questions. For example: Cursor/Copilot expired and the company won’t reimburse it. You?

- If it expires, it expires. Handwriting code isn’t impossible
- Look for a free alternative
- Renew immediately! Please, just give me more tokens!

![](https://pic.yupi.icu/1/image-20260413135847877.png)

My own result was HACK Wild Hacker, with the motto “It works, doesn’t it.jpg.” Personally, I think it’s pretty accurate. In the age of AI coding, I’ve built many Vibe Coding side projects, and I really do have that “anything goes, if it runs it’s fine, then move on to the next one” mindset.

![](https://pic.yupi.icu/1/image-20260413140345748.png)

There are 28 personality results in total, and all the names are programming-related: things like SUDO Universal Admin, NULL Null Pointer, CTRL-C Copy-Paste Engineer, 996 Overtime King of Kings, 404 Invisible Person, VIBE Vibe Programmer, and more. There’s even a hidden personality, ☕ JAVA Caffeine-Driven Developer. Anyone who can trigger that one probably has something special going on...

![](https://pic.yupi.icu/1/image-20260413135603390.png)



## Full Development Process

I only spent about an hour getting this project online, using Vibe Coding the whole way with Cursor + Claude.

There was no complicated methodology, and I didn’t need Harness Engineering either. I just kept talking to AI, stating requirements, and giving feedback.

Here’s the key process.

**1. Analyze reference projects and extract the product essence**

The initial prompt you give AI is very important. I first found a complete SBTI question bank and scoring-logic report online, then threw that together with the SBTI official site and the MBTI 16personalities official site at AI, asking it to deeply analyze the personality systems, scoring methods, and viral spread mechanisms behind those tests.

At the same time, I defined CBTI’s direction: it should be programming-oriented, have scientific grounding and practical value, while also having meme appeal and viral potential.

![](https://pic.yupi.icu/1/image-20260413140817081.png)

Then AI directly completed the development and testing of the initial website:

![](https://pic.yupi.icu/1/image-20260413141043674.png)



**2. Repeatedly iterate on the content**

The personality codes in AI’s first draft all looked similar and had no distinctiveness at all, so I asked it to search the whole web for programmer-related memes and remake the personality system again and again.

![](https://pic.yupi.icu/1/image-20260413141131319.png)

I revised this stage many times. In the end, I expanded the personality system from a dozen-plus types to 27 types, introduced a new AI-coding dimension, and changed the question tone from overly serious to something more conversational and relatable.

![](https://pic.yupi.icu/1/image-20260413141241183.png)



**3. Optimize the UI design**

At first, the homepage AI generated looked like a B-end management dashboard—ugly and overly complicated.

So I told it directly that the homepage should be as simple as possible: one slogan and one “Start Test” button is enough.

![](https://pic.yupi.icu/1/image-20260413141547295.png)

Then I changed the color scheme to orange and used the `frontend-design` Agent Skill to optimize the overall visual effect. On the quiz page, I also added interaction details like an answer card, a progress bar, and quick question jumping.

![](https://pic.yupi.icu/1/image-20260413141630018.png)



**4. Create personality images**

In the past, creating image assets for a website would definitely take a lot of time.

But now, with AI, it can be done in just a few minutes.

I asked AI to reference the low-poly character style used on the official MBTI website, then generate prompts for the AI image tool Nano Banana.

Here’s a small trick: I didn’t ask AI to generate one prompt for each of the 28 characters, because that would waste both time and money. Instead, I split them into 2 batches, putting 14 characters in **the same image** per batch. That way, I only needed 2 prompts and 2 generated images.

![](https://pic.yupi.icu/1/image-20260413141753739.png)

The result wasn’t bad at all:

![](https://pic.yupi.icu/1/image-20260413142143210.png)

Then I asked AI to interpret the full image itself and write a Python script to cut the image into separate pieces, compress and resize them, remove blank backgrounds, and so on. In the end, I got 28 character images.

![](https://pic.yupi.icu/1/image-20260413142347871.png)



**5. Add more features**

After confirming that both the question content and the website functionality worked properly, I further optimized many details of the site, adding share copy, Canvas-rendered share posters, a five-dimension radar chart, hidden personality Easter eggs, and other features.

![](https://pic.yupi.icu/1/image-20260413142811945.png)

Since the site itself wasn’t very functionally complex, I more or less let AI generate every feature without overthinking, so I naturally ran into some issues. For example, the share poster text was too small at first, then the QR code didn’t render, then later it got too large. I had to tweak it through several rounds before I was satisfied.

![](https://pic.yupi.icu/1/image-20260413142903376.png)



**6. Deploy online and verify**

Since the site doesn’t rely on a back end, deployment is incredibly simple.

I used the EdgeOne Pages MCP. I only needed to talk to AI, and it automatically ran the Next.js build command, exported the code as a static HTML site, and deployed it to Tencent Cloud EdgeOne Pages—all within a minute.

![](https://pic.yupi.icu/1/image-20260413143449058.png)

You can view the deployed project in the Tencent Cloud EdgeOne Pages console, and you can also customize the domain:

![](https://pic.yupi.icu/1/image-20260413143532414.png)

After it went live, I had AI autonomously run through the whole process again, confirming that the deployed functionality also worked properly and that the 30 questions could cover all 28 personality types.

Mission accomplished!



## Final Thoughts

Technically, this project really isn’t that difficult. It’s just a pure front-end static website with no back end, no database, and a core algorithm that basically just computes scores and does vector-distance matching.

Now that AI coding exists, projects like this really are something anyone can build. In just one hour, you can turn an idea into a website you can share with friends. If you also have a fun creative idea, give it a try—maybe the next viral hit will be yours!



## Recommended Resources

1) Yupi AI Navigation: [A complete collection of AI resources, the latest AI news, and free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussion and Q&A](https://www.codefather.cn)

3) Programmer Interview Cheat Sheets: [High-frequency topics for internships, campus hiring, and experienced hiring, plus real company question analysis](https://www.mianshiya.com)

4) Resume-writing tool for programmers: [Professional templates, rich example sentences, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships, campus hiring, and experienced hiring](https://ai.mianshiya.com)
