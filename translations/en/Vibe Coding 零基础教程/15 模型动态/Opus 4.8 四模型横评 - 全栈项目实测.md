# Opus 4.8 Four-Model Comparison - Full-Stack Project Benchmark

Anthropic has just released another new model, Claude Opus 4.8. From Opus 4.6 in February to Opus 4.7 in April, they’ve iterated three versions in just three months!

![](https://pic.yupi.icu/1/image-20260529132455116.png)

Every time a large model gets updated, the whole internet just reposts the official benchmark charts and translates the release notes, then calls it a day.

But high benchmark scores don’t necessarily mean it’s actually useful in practice. I still want to test it myself—even if my hair is already falling like rain...

![](https://pic.yupi.icu/1/%25E5%25A4%25B4%25E7%25A7%25833%25E6%25A0%25B9.jpeg)

Since the latest Claude Opus 4.8 is already available in Cursor, I decided to put the last three generations of Opus (4.6, 4.7, and 4.8) together with the popular GPT-5.5, let them build the same full-stack project with the same prompt, and see which one really performs best.

Before we start, let me first introduce what changed in Opus 4.8—and feel free to guess the final test result too~



## What Changed in Opus 4.8?

Opus 4.8 is priced the same as Opus 4.7: $5 input and $25 output per million tokens, with the context window still at 1 million tokens.

Honestly, I was almost too lazy to look at the benchmark charts, because Opus improves every time anyway. But the comparison with GPT-5.5 is still worth noting. In coding ability, SWE-bench Pro (Agent coding ability) improved from 64.3% in 4.7 to 69.2%, clearly ahead of GPT-5.5’s 58.6%. However, on Terminal-Bench 2.1 (terminal coding ability), GPT-5.5 still leads Opus 4.8 with 78.2% versus 74.6%.

![](https://pic.yupi.icu/1/image-20260529130434887.png)

There are 3 updates this time that I think are especially worth paying attention to:

1) Dynamic workflow: in Claude Code, you can dispatch hundreds of parallel sub-agents at once, with up to 16 running simultaneously and a single-task upper limit of 1,000 agents. It’s perfect for hard jobs like large-scale code migration.

Still, most users probably won’t need this. It’s like running a company—you don’t need to hire hundreds of people at once for everyday work.

2) Huge jump in code self-checking ability: officially, Opus 4.8 is 4 times less likely than 4.7 to miss code defects. In other words, after writing code, the AI can find more bugs on its own, making one-shot success much more likely.

3) Big price cut for Fast Mode: Fast mode can double the processing speed of the same model, and it’s 3 times cheaper than the previous Fast Mode.

Looking at data is one thing, but whether an AI coding model is actually good still has to be tested with real projects.

Before the official test starts, though, let me share a recent funny thing about Claude.

Someone found that if you call Claude directly through Anthropic’s official API (note: **official API**, not a relay service) and ask it in Chinese, “What model are you?”, it can seriously answer, “I am Tongyi Qianwen.” Apparently, if you phrase it differently, it may even say it’s DeepSeek.

![](https://pic.yupi.icu/1/HJbHfIubYAAPU8F-20260529140327405.jpeg)

My blind guess is that API calls don’t have the same kind of identity-anchoring system prompt as the web client, and in Chinese internet training data, “I am Tongyi Qianwen / DeepSeek” appears much more often than “I am Claude.” So without an identity prompt, the model simply outputs the highest-probability answer.

But maybe Claude was distilled from domestic models in the first place—what a boomerang that would be~

![](https://pic.yupi.icu/1/HJbtnTCaMAEBJpr-20260529140327435.jpeg)

Alright, back to the point. How do these top models actually perform in real coding?



## Let Cursor Run the Parallel Test Automatically

If you had to compare the coding ability of 4 models, how would you do it? Run them one by one manually?

That would be way too tiring. I chose to let AI test AI instead.

AI coding tools like Cursor now already have built-in **sub-Agent** capability, which can launch multiple independent AI tasks in parallel, and each task can use a different model.

In other words, Cursor acts like a contractor. I give one instruction, and it dispatches 4 different “workers” at the same time.

All I had to do was send one prompt, and Cursor automatically launched 4 sub-agents for me using Opus 4.6, 4.7, 4.8, and GPT-5.5, all set to High thinking mode, all building the same project in their own directories with the same prompt.

The project I asked AI to build was a full-stack **TaskFlow task management board**, similar to a simplified Feishu board, with 7 functional requirements: user registration and login, three-column drag-and-drop board, task CRUD, data dashboard, search and filtering, dark/light theme switching, and responsive design. The tech stack was a React + TypeScript front end, Python FastAPI back end, SQLite database, and front-end/back-end separation.

![](https://pic.yupi.icu/1/1780023443848-2d39ddfb-8739-4e80-a723-514b71c3bda9-20260529140327470.png)

Once again: all 4 models used the exact same prompt, and there was zero manual intervention throughout. The main things I focused on were UI design quality, feature completion, code quality, and architectural soundness.



## Front-End UI Comparison

Let’s start with the login page.

Opus 4.6 and Opus 4.7 are similar. Both made a very clean centered card-style login form:

![Opus 4.7 login page](https://pic.yupi.icu/1/1780029270428-9e9a1e95-f188-45b0-b643-a6dc0055ceaf.png)

Opus 4.8 is similar too, but it adds Register / Login tab switching and thoughtfully displays the demo account and password right at the bottom of the page:

![Opus 4.8 login page](https://pic.yupi.icu/1/1780029273042-d3f331eb-d1ed-47ec-8365-35cac284364d.png)

GPT-5.5’s style is completely different, and at a glance it feels very GPT. The left side is packed with promotional copy, while the login form sits on the right. It perfectly matches my stereotype of GPT—it loves stuffing pages with information:

![GPT-5.5 login page](https://pic.yupi.icu/1/1780029293656-2648ba99-dd96-41e2-bc9a-0e46458b0b17.png)

After logging in, let’s look at the task board page.

Opus 4.6 has neat layout but no background color. Pretty standard:

![Opus 4.6 board page](https://pic.yupi.icu/1/1780029557786-c608446a-de14-4cee-948b-e53309ee8cb8.png)

Opus 4.7 adds a gradient background and color-coded column headers, making the overall result more elegant:

![Opus 4.7 board page](https://pic.yupi.icu/1/1780029417776-1044a907-5a56-435a-9733-e635e55f2d61.png)

Opus 4.8’s board looks fairly close to 4.6. It feels a bit plain:

![Opus 4.8 board page](https://pic.yupi.icu/1/1780029463336-ac3e9396-e39c-4dd2-86bd-79f570dd7300.png)

GPT-5.5 simply merged the board and the data dashboard into a single page, with charts on top and the three task columns below, doing the most work with the fewest pages. But the task-column titles are in English, which is a bit careless in the details.

![GPT-5.5 board + data dashboard](https://pic.yupi.icu/1/1780029520120-9b73316b-cebd-4587-967e-36ccc7fb2e7f.png)

Now let’s look at the data dashboard page.

Opus 4.6’s data dashboard is relatively simple, with three charts arranged in one row and no extra decoration:

![Opus 4.6 data dashboard](https://pic.yupi.icu/1/1780029569404-58f0e634-5282-43dc-ac50-4460fb62fd30.png)

Opus 4.7’s summary cards use rounded gradient icons, making them more vivid:

![Opus 4.7 data dashboard](https://pic.yupi.icu/1/1780029454060-245701a0-e588-49e0-943a-a6c9b1d63947.png)

Opus 4.8’s data dashboard style is similar to 4.6—actually, no, it’s even plainer than 4.6:

![Opus 4.8 data dashboard](https://pic.yupi.icu/1/1780029479354-a9c39f80-abe6-4353-8240-b29bf884b672.png)

Now let’s look at dark mode, where the difference between the 4 models becomes even more obvious.

When Opus 4.6 switches to dark mode, the overall colors are still reasonably coordinated, but the contrast between the background and cards is low, so it looks a bit gray and dull:

![Opus 4.6 dark mode](https://pic.yupi.icu/1/1780029710334-7c088ac9-ea6b-4726-86c3-0ea8039e2188.png)

Opus 4.7’s dark mode is very different. The gradient background looks more premium against the dark base, and the colors of the cards and charts are very unified:

![Opus 4.7 dark mode](https://pic.yupi.icu/1/1780029722961-b522c32f-4d51-42e0-882c-76bd78290840.png)

Opus 4.8’s dark mode is pretty standard. No big surprises, but no serious flaws either. It’s quite close to 4.6:

![Opus 4.8 dark mode](https://pic.yupi.icu/1/1780029730688-20d35b84-c419-49ae-85a6-7a9ce47260b7.png)

GPT-5.5’s dark mode feels a bit like Opus 4.6 as well—a big patch of gray, just slightly lacking...

![GPT-5.5 dark mode](https://pic.yupi.icu/1/1780029756025-7259116f-f01b-45b9-9921-53a024d16f2e.png)

Which one do you think looks best?

Personally, I vote for Opus 4.7. That gradient background in dark mode feels really comfortable.



## Feature Implementation Comparison

I won’t show all the features one by one. All 4 models successfully implemented the 7 required features: registration/login, drag-and-drop board, task management, charts, search, theme switching, and responsive design. Everything worked normally.

After all, one-shot full-stack projects from mainstream models aren’t exactly new anymore. None of these features are particularly complex, so it’s hard for them to create much separation here.



## Code Quality Comparison

Since the features are the same and UI preference is somewhat subjective, the real place where differences emerge is code quality.

I had AI help analyze the code structure of the 4 projects, and the differences are quite noticeable.

First of all, the project structures of all 4 models are surprisingly similar—even the filenames are almost identical. On one hand, that’s probably because my prompt constrained the technical framework. On the other hand, it also suggests that these top models’ coding approaches are converging heavily toward the same set of best practices.

![](https://pic.yupi.icu/1/1780029867213-f06ef0ec-8f8e-4287-b94c-5932dca00be6.png)

Let’s look at the code size they generated:

| Model | Source File Count | Lines of Code |
| ----- | ----------------- | ------------- |
| Opus 4.6 | 25 | 1,865 |
| Opus 4.7 | 32 | 2,259 |
| Opus 4.8 | 33 | 2,701 |
| GPT-5.5 | 13 | 1,221 |

Clearly, Opus 4.8 produced the most code, while GPT-5.5 was the most concise.

But more code doesn’t necessarily mean better, and less doesn’t necessarily mean worse. What matters is whether the architecture is clear and whether there are obvious bugs. Let’s go through them one by one.

1) **Opus 4.7 has the clearest architecture**

On the back end, it split things into 3 routers (`auth`, `tasks`, `stats`). On the front end, state management uses a dedicated store file, registration and login are separate pages, there’s a dedicated `AppLayout` layout component, and axios requests are centrally wrapped. The layering is very tidy and would be perfectly fine for a team project.

2) **Opus 4.8 split things most finely**

It has a dedicated `context` directory, a `FilterBar` component, and separate utility modules, resulting in the largest code volume. It also directly configured CORS with `allow_origins=["*"]`, which shows somewhat weak security awareness.

3) **GPT-5.5 took an ultra-minimal path**

It used only about half as many lines as Opus 4.8 and still implemented all features, but the downside is that every back-end route is written in a single `main.py` file, with 300+ lines crammed together. It runs, sure, but it would be painful to maintain later.

4) **Opus 4.6 has complete features, but also 2 bugs**

One bug is a missing React import that causes a white screen. The other is a Tailwind v4 CSS layer conflict, which shows that 4.6 still isn’t adapting well enough to the latest framework versions.



## Overall Ranking

In the end, the final ranking of the 4 models in this test is:

| Rank | Model | One-line Verdict |
| ---- | ----- | ---------------- |
| 🏅 1 | **Opus 4.7** | Clearest architecture, best-looking UI, zero code defects, ready to use out of the box |
| 🥈 2 | **Opus 4.8** | Most detailed and largest codebase, but with missing files and CORS issues |
| 🥉 3 | **GPT-5.5** | Cleared everything with an ultra-lean 1,221 lines, but its monolithic back-end file hurts maintainability |
| 4 | **Opus 4.6** | Complete features but 2 white-screen bugs, and weaker adaptation to newer frameworks |

Is this result a little surprising?

The newest Opus 4.8 didn’t even take first place. Was this update all for nothing?

![](https://pic.yupi.icu/1/image-20260529135020413.png)

My interpretation is that the focus of 4.8’s update wasn’t “writing prettier code,” but rather Agent reliability and long-duration unsupervised task execution. Features like dynamic workflow and code self-checking may be more valuable in large projects and enterprise scenarios, but in a scenario like “one-shot build me a full-stack project,” 4.7 actually performed more steadily.

**So don’t blindly chase the newest model. You still need to choose based on your actual needs.**

Time is limited, so I’ll stop here for now. Based on my own hands-on experience, my suggestions are:

- For daily development and one-shot small projects: choose Opus 4.7 or 4.8. 4.7 has the better UI, while 4.8 is more worry-free because of its stronger self-checking ability.
- For terminal operations and command-line automation: choose GPT-5.5. When I made my Codex tutorial earlier, GPT-5.5 worked great as an office AI.
- For large-scale code migration and refactoring: choose Opus 4.8. Its dynamic workflow is the killer feature.

And I’ve noticed a trend: Opus 4.8 is getting more and more like GPT-5.5. Both are moving toward “get the job done in the most practical way possible,” and paying less attention to extra bonus points like UI aesthetics.

But I honestly don’t want Claude to keep moving in that direction. I’d rather large models become more differentiated, strengthen their own unique advantages in different directions, and give users more choices.



## Final Thoughts

This comparison shows that different models each have their own strengths and weaknesses in AI coding. You shouldn’t blindly chase the newest release—you should choose based on real needs.

Once you understand this, you’ll be able to choose and combine AI models more rationally in real projects and improve your development efficiency.

If you want to keep learning more AI coding tools and practical techniques, you can read the other articles in the Coding Tools section of this tutorial.
