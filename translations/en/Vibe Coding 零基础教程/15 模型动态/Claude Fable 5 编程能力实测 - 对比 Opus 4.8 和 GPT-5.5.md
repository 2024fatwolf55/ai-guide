# Claude Fable 5 Coding Capability Hands-on Test - Compared with Opus 4.8 and GPT-5.5

> A real-world comparison of the world’s most expensive AI model: Fable 5 vs Opus 4.8 vs GPT-5.5

Hello everyone, I’m Yupi.

Just now, Anthropic released its new-generation model **Claude Fable 5**, and at the same time also released an “unlocked version” aimed at professional security personnel called Claude Mythos 5.

![](https://pic.yupi.icu/1/1781053123369-84164e0d-6682-48a1-bf69-98300e8ade11.png)

Officially, it’s being described as a “mythic-level” model whose abilities rise above the previous Opus series. It’s said that Stripe tested it on their 50-million-line Ruby codebase and completed a migration in a single day that would originally have taken the team two months.

In this article, I’ll first show you what exactly changed in Fable 5, then I’ll run two hardcore real-world test rounds with Fable 5, Opus 4.8, and GPT-5.5 competing side by side to see how strong the new model really is for AI coding.

Friendly reminder: this test got a bit expensive, so please have pity on my wallet and read to the end.



## What Changed in Claude Fable 5?

### 1. One Model, Two Names

This time, Anthropic released both Fable 5 and Mythos 5, but they are actually **the same underlying model** with exactly the same capabilities. The only difference is how tight the “safety guardrails” are.

Fable 5 is meant for everyone and can be used starting today. But it has an extra safety classifier layer. When it encounters requests involving cybersecurity, biochemistry, or model distillation (to prevent others from learning its capabilities and training competing models), it downgrades the response to Opus 4.8 and shows you a notice.

Mythos 5 is the “full form” with the guardrails removed. It’s only provided to cybersecurity organizations reviewed by Anthropic and to a small number of biological researchers. Ordinary users won’t get access to it.

As for Fable 5’s downgrade mechanism, the official claim is that fewer than 5% of conversations trigger it on average. But when I tested Fable 5 for article-writing capability, it actually triggered the safety filter and switched straight to Opus 4.8.

Come on, man. What’s unsafe about writing an article?!

![](https://pic.yupi.icu/1/1781053278660-299797cf-fc94-41d3-8418-c2d5b0c19a89-20260610123536602.png)

Some of you are probably wondering why this release didn’t continue the Opus line with something like Opus 4.9 and instead jumped straight to generation 5.

That’s because it’s no longer an Opus-level model at all. Internally at Anthropic, it belongs to a higher tier called the **Mythos class**, and its capabilities directly crush Opus.

> Interestingly, the word Fable itself comes from the Latin *fabula*, and it’s linguistically close to the Greek *Mythos*.

Put simply, it’s the same knife: one version is sharpened for professionals, the other is sheathed for the public.



### 2. The Most Expensive Pricing in the World

Claude Fable 5 and Mythos 5 are priced at $10 per million input tokens and $50 per million output tokens.

That may not sound like much at first, but compare it with the current mainstream model prices and you’ll immediately see how outrageous it is:

| Model               | Input / Output (per million tokens) | Total Cost |
| ------------------- | ----------------------------------- | ---------- |
| DeepSeek V4         | $0.4 / $0.8                         | $1.2       |
| Claude Opus 4.8     | $5 / $25                            | $30        |
| GPT-5.5             | $5 / $30                            | $35        |
| **Claude Fable 5** | **$10 / $50**                       | **$60**    |

Fable 5’s total cost is directly double that of Opus 4.8 and 50 times that of DeepSeek V4, firmly making it the most expensive mainstream model right now. Anthropic even specifically emphasized that this is already more than 50% cheaper than the previous Mythos Preview.

Good grief—even after getting cut in half, it’s still the most expensive. At this rate, future models may really become unaffordable for ordinary people…

Also note: the official announcement says that from today until June 22, plans like Pro, Max, and Team can use Fable 5 for free. But **after June 23, it will switch to charging separate “usage credits”**, until capacity improves. So if you want to try it for free, make good use of this two-week window.



### 3. Explosive Benchmark Scores

Every time a new model comes out, we have to look at the benchmark scores. Anthropic says Fable 5 is basically SOTA on almost every benchmark they tested, especially in coding, knowledge work, vision, and scientific research. And **the longer and more complex the task, the bigger the lead becomes**.

Honestly, I’m already getting numb because every company basically says its own model is SOTA these days…

But this time, Fable 5’s results really do deserve to be called explosive.

![](https://pic.yupi.icu/1/1781053155639-63c73b4b-f732-44e8-bf48-7efaeb314e11.png)

Let me call out a few especially eye-catching numbers:

- SWE-bench Pro (Agent coding ability): 80.3%, far above GPT-5.5’s 58.6% and Opus 4.8’s 69.2%
- FrontierCode (high-quality coding): 29.3%, while Opus 4.8 is only 13.4% and GPT-5.5 is 5.7%
- Vision capability (GDPpdf document reasoning): 29.8%, compared with GPT-5.5’s 24.9% and Opus 4.8’s 22.5%. Anthropic even had Fable 5 beat Pokémon FireRed using pure vision.

Good grief—that’s a true step-function improvement.

But benchmarks are only one side of the story. Whether it’s actually usable still has to be tested in real projects. So as usual, I brought the models into real hands-on tests and put Fable 5, Opus 4.8, and GPT-5.5 into direct competition.

Cursor also integrated Fable 5 immediately, which makes it super convenient to test every new model as soon as it launches.

![](https://pic.yupi.icu/1/image-20260610114528179.png)

I previously wrote a free open-source [AI Coding Beginner Tutorial](https://ai.codefather.cn/vibe), which includes a beginner-friendly Cursor hands-on guide. If you’re interested, feel free to take a look.

![](https://pic.yupi.icu/1/image-20260610121356925.png)

For this comparison, I prepared two rounds of real-world tests. The first round lets all three models tackle the same full-stack project in one shot. The second round is even more hardcore: having them refactor the leaked 500k+ lines of Claude Code source.

Alright then—time for my wallet to start burning.



## Hands-on Review 1. One-Shot Full-Stack Project

For the first review, I chose a representative full-stack project to test the models’ overall coding ability.

The project is called “TaskFlow Task Management Board,” something like a simplified Feishu kanban. It includes 7 functional requirements: user registration/login, drag-and-drop across three board columns, CRUD for tasks, a data dashboard, search and filtering, dark/light theme switching, and responsive design. The tech stack is React + TypeScript on the frontend, Python FastAPI on the backend, and SQLite for the database.

I chose this project because it includes both frontend and backend, with moderate interaction complexity, making it good for evaluating UI taste, engineering ability, and feature completeness at the same time.

The contestants this time were **Claude Fable 5**, **Claude Opus 4.8**, and **GPT-5.5**. All three models used the exact same prompt, all were set to High thinking mode, and there was zero manual intervention throughout.

After some time, all three models successfully finished the task, and both frontend and backend were able to run.

Let’s first look at what each of them produced.

Opus 4.8’s login page used the classic centered card layout. It could switch between register and login tabs, and thoughtfully displayed the demo account and password at the bottom of the page:

![Opus 4.8 login page](https://pic.yupi.icu/1/1780029273042-d3f331eb-d1ed-47ec-8365-35cac284364d-20260610123536894.png)

GPT-5.5 had a completely different style. The left side was packed with marketing copy, and only the right side contained the login form. It fits my stereotype of GPT pretty well—it loves stacking information onto the page:

![GPT-5.5 login page](https://pic.yupi.icu/1/1780029293656-2648ba99-dd96-41e2-bc9a-0e46458b0b17-20260610123536970.png)

Fable 5’s login page was clean and simple, stylistically consistent with Opus 4.8:

![Fable 5 login page](https://pic.yupi.icu/1/1781056255673-6848d90c-1ddf-4f57-90e6-9e62ac0f4662.png)

Now let’s look at the task board page.

Opus 4.8’s board was a bit plain. The layout was neat, but there wasn’t much background color:

![Opus 4.8 board page](https://pic.yupi.icu/1/1780029463336-ac3e9396-e39c-4dd2-86bd-79f570dd7300-20260610123537119.png)

GPT-5.5 combined the board and the data dashboard into a single page, trying to accomplish the most with the fewest screens. But the column titles were directly left in English, which made the details feel a bit rough:

![GPT-5.5 board + dashboard](https://pic.yupi.icu/1/1780029520120-9b73316b-cebd-4587-967e-36ccc7fb2e7f-20260610123537167.png)

Fable 5’s board page had much clearer state distinctions, richer and more vivid colors, and a more reasonable layout of information on the task cards.

![Fable 5 board page](https://pic.yupi.icu/1/1781056330256-6c82e2b1-269a-4984-a302-555e6d99e3aa.png)

Now look at the data dashboard. Fable 5 created a donut chart, a bar chart, and a line chart, and even used curved elements to add some decorative polish to the task cards:

![Fable 5 dashboard](https://pic.yupi.icu/1/1781056402506-6aba930b-6237-4d6f-b4e1-adb82a2b435c.png)

Opus 4.8’s dashboard, by contrast, was more plain and straightforward:

![Opus 4.8 dashboard](https://pic.yupi.icu/1/1780029479354-a9c39f80-abe6-4353-8240-b29bf884b672-20260610123537430.png)

In dark mode, Fable 5’s chart color scheme was very harmonious, and the overall result was the best of the three:

![Fable 5 dark mode](https://pic.yupi.icu/1/1781056514528-855b0bda-9019-4201-9266-ad6b95abed74.png)

Opus 4.8’s dark mode was decent and without major flaws, but there were no surprises either:

![Opus 4.8 dark mode](https://pic.yupi.icu/1/1780029730688-20d35b84-c419-49ae-85a6-7a9ce47260b7-20260610123537573.png)

GPT-5.5’s dark mode was the weakest of the bunch—a big slab of gray:

![GPT-5.5 dark mode](https://pic.yupi.icu/1/1780029756025-7259116f-f01b-45b9-9921-53a024d16f2e-20260610123537621.png)

Now that we’ve looked at the UI, let’s talk about where the real gap opened up.

Fable 5 was the only one of the three that achieved a “runs with zero fixes” result. Although all three models eventually got the project running, Opus 4.8 and GPT-5.5 both needed a few minor bug fixes, missing files added, or dependency versions adjusted. Fable 5’s code, by contrast, passed TypeScript compilation in one shot, started the backend successfully in one shot, and passed all API tests in one shot—truly usable right out of the box.

And its verification method was the most hardcore as well. It didn’t just test the API with `curl`; it also used CDP (Chrome DevTools Protocol) to synthesize real mouse drag events and verify drag-and-drop persistence in the browser, going much deeper in validation than the other models.

![](https://pic.yupi.icu/1/1781056605971-0891725a-797f-4ee9-b0c7-395bd7227eff.png)

Overall, Opus 4.8 had the most standardized architecture layering and a solid sense of UI design, but it needed a few minor fixes before it could run properly. GPT-5.5 behaved as usual: fast but rough, with a relatively crude interface. Fable 5’s main strength was engineering reliability—no defects, clean hook abstractions, and deep verification. This kind of “delivery certainty” has a huge impact on efficiency. Avoiding even one extra round of debugging can easily save half an hour.



## Hands-on Review 2. Refactoring the Claude Code Source

The second round was the true highlight of this test.

Anthropic repeatedly emphasized that **the longer and more complex the task, the larger Fable 5’s lead becomes**. A short and quick demo simply can’t reveal a generational gap. If you want to test properly, you need a real long-horizon task.

By the way, didn’t Claude Code leak more than 500,000 lines of its source not long ago?

That code is a real industrial-grade Agent architecture, which makes it perfect as a test case.

So I went for it. The concrete method was to provide the leaked Claude Code source package to each model and have it independently analyze the architecture inside, then refactor from scratch a runnable command-line AI coding assistant called “Yupi Code” in a new directory. No manual intervention at all—just see whether it could pull it off in one go.

The prompt was as follows:

```markdown
你是一个资深的 TypeScript 全栈工程师，精通 AI Agent 架构和命令行工具开发。

claude-code-origin 目录下是 Claude Code 泄露的部分源码，包含完整的实现逻辑，但无法运行。

你要先阅读并理解这份源码的核心设计，在此基础上重构一个命令行 AI 编程助手「Yupi Code」，放到新目录下。

要求必须能实际运行，各项功能正常可用。
```

I saved the outputs of the three models into separate directories and then compared how each one performed.



### Opus 4.8 Fell Short at the Last Mile

Opus 4.8 got the testing flow working by using a mock server, and it performed the most layered self-validation.

![](https://pic.yupi.icu/1/1781057084425-5ece0ecc-8b84-4ede-899a-fd1f0b75c045.png)

But when actually running it, it required an Anthropic API Key. Without the key, it couldn’t be used:

![](https://pic.yupi.icu/1/1781057061510-ed76e62d-a3e4-43cf-a9cc-df430920c174.png)

Sorry, I don’t have that key. So I had to ask AI to reuse my local Claude Code configuration and repair it once more.

After the fix, I tried it again, and it genuinely made me laugh.

Leaving aside the fact that the interface style was obviously different from the original Claude Code (look at that input box), the AI’s output content didn’t even display correctly. It flopped.

![](https://pic.yupi.icu/1/1781057348163-1ee80041-c8c7-419b-ac78-0994d4e7a268.png)



### GPT-5.5: The King of Cutting Corners

GPT-5.5 finished the task the fastest among the three models.

But here’s the problem: after generation, it also required an Anthropic API Key to run. Hmph—this guy really is the master of laziness. Even its output information was much more stripped down than Claude’s:

![](https://pic.yupi.icu/1/1781057204520-212741e2-5a43-4159-9da4-8f97cc4e1004.png)

Without the key, it couldn’t run either, so I asked AI to reuse the local Claude Code configuration and try again.

Although it could chat normally, that interface was way too bare-bones. Truly the king of cutting corners:

![](https://pic.yupi.icu/1/1781057756980-b68eabdf-4202-4371-bef7-d238db440a6d.png)

Then I asked it to read a local file, and it immediately threw an error. GG.

![](https://pic.yupi.icu/1/1781057791133-49ef87e2-d098-48e4-a3c0-97e5c942ab11.png)



### Fable 5: Usable Out of the Box

Fable 5 directly read my local Claude configuration and used the DeepSeek Chinese model I had previously configured. It didn’t require an Anthropic API Key at all.

![](https://pic.yupi.icu/1/1781056994142-6c07d9ec-a80d-4a7c-9e88-ddd0f215d311.png)

I tried it, and the experience was almost identical to Claude Code itself! Normal chat, Agent mode, tool calls—everything worked properly. **It was usable in a single delivery**, with no need for any second round of fixing.

![](https://pic.yupi.icu/1/1781056792310-48d8afe0-128a-4e65-905d-23136cdc61a9.png)

Haha, I guess I can now say I’ve “developed Claude Code” too—another bold line added to the resume~



### Development Process Comparison

After seeing the final results, I opened a new conversation and asked AI to analyze the conversation logs from each model’s development process, to see what exactly was different in how they worked.

The most important discovery was this: **Claude Fable 5 was the only model that performed interactive PTY terminal testing**.

![](https://pic.yupi.icu/1/1781058521904-b1f23509-52e4-4407-afaf-1105e49ed3e4.png)

Although Opus 4.8 wrote the most tests, all of its verification happened in non-interactive environments. It never validated the interactive experience in a real terminal. So when the product reached the user, output rendering problems appeared.

Fable 5, on the other hand, didn’t write a mock test suite, but it did something Opus didn’t do: **it repeatedly debugged the interaction in a real terminal using PTY** (simulating PTY with the `script` command and verifying the full flow of `/help`, `/cost`, permission dialogs, file writing, and more). It spent a large number of rounds solving PTY-specific issues like the `\r` → `\n` Enter key behavior and fixing API protocol bugs. Those extra efforts ultimately translated into the best user experience.

This gave me a very important insight: **there is a huge gap between “AI says its tests passed” and “the user can actually use it.”** In CLI scenarios, making interaction work in the real environment is far more important for final quality than merely running tests in an isolated environment.



### Cost Comparison

I’m sure everyone cares about the same question: how much money did this round of testing burn?

When I opened Cursor’s billing backend, my heart started bleeding!

![](https://pic.yupi.icu/1/1781058408651-6e0971c1-72f8-459b-b10f-fb5d07aec864.png)

The cost and token details for the three models were as follows:

| Model        | Total Cost | Total Tokens |
| ------------ | ---------- | ------------ |
| GPT-5.5      | $4.61      | 5.306 million |
| Opus 4.8     | $13.38     | 16.855 million |
| **Fable 5** | **$38.66** | **21.464 million** |

Fable 5 cost **three times** as much as Opus and **eight times** as much as GPT-5.5?! This one task alone cost me more than 200 RMB…

The main reason was the enormous consumption of thinking tokens, plus the many rounds spent debugging TUI interaction. But from another angle, that’s exactly why it became the only model able to deliver a truly usable product—it was willing to spend those rounds debugging real-environment interaction properly.



## Overall Data Comparison

After both rounds of testing, I asked AI to create a comprehensive visual analysis based on the full conversation logs and code outputs from the three models.

![](https://pic.yupi.icu/1/image-20260610115144315.png)

First, look at the bar chart of several core capability indicators. You can clearly see that Fable 5 is far ahead in verification depth and real-world usability, Opus 4.8 has a slight edge in engineering quality, and GPT-5.5 ranks last across the board:

![](https://pic.yupi.icu/1/1781059070475-27a525ba-ff55-46c1-a47b-d25c7d0e18e9.png)

The feature coverage matrix makes the gap even more intuitive. Fable 5 implemented things the other models didn’t, such as a full Ink TUI, context compression, and automatic reuse of local configuration. GPT-5.5, meanwhile, even failed on the most basic Read tool, leaving its functionality severely incomplete:

![](https://pic.yupi.icu/1/1781059044766-2644ca30-1003-4c6d-a559-c9453a649b34.png)

Scoring across five dimensions—architecture understanding, engineering execution, verification and usability, out-of-the-box readiness, and cost-effectiveness—Opus 4.8 was strongest in architecture understanding, but Fable 5 maxed out the verification and out-of-the-box categories, creating a clearly differentiated advantage:

![](https://pic.yupi.icu/1/1781059103060-40d41546-5c2f-4158-b0b6-2507246b7735.png)

In the final comprehensive score, Claude Fable 5 ranked first with 8.3 points. It wasn’t the best at every single metric, but the fact that it was **the only one capable of delivering a usable product** outweighed everything else. After all, when we use AI for coding, our goal is to directly get a usable result with minimal hassle—not a pile of half-finished artifacts that still require manual repair.

![](https://pic.yupi.icu/1/1781059149037-63336958-f848-42f7-a1fb-853d830f5c21.png)

Looking back at the three models’ strategies, it actually feels a lot like a classic impossible triangle.

**Speed, cost, quality: an impossible triangle.**

GPT-5.5 chose speed and cost, and the result wasn’t usable. Opus 4.8 chose code quality and cost, but had blind spots in verification. Fable 5 chose quality and user experience, and the price it paid was, well, price.

Of course, this was only one of my tests and doesn’t prove a universal rule. But it’s enough to reveal something important: when it comes to **delivering a usable product at the end of a long-horizon task**, Fable 5 really does represent a qualitative leap over the previous generation.

Based on this comparison, I can also offer a few suggestions for model selection.

If you’re doing large-scale refactoring or migration projects that are both long and complex, Fable 5 is the best choice—its high price has a reason. But for everyday one-shot small-to-medium projects, Opus 4.8 has higher code quality, a more complete architecture, and a much better cost-performance ratio. GPT-5.5 underperformed this time, but it still leads on benchmarks related to terminal automation and command-line tasks, so it’s suitable for speed-focused automation work. And if your budget is tight, Chinese domestic models are also fully capable of handling most scenarios.

In short, **don’t blindly chase the newest model—choose based on your real needs**. The most expensive one is not necessarily the best one for you.



## Final Ramble

OK, that’s it for this test. I think Fable 5’s performance this time matched my expectations for a new-generation model. AI coding ability is rapidly approaching the level where it can independently deliver complete projects—but at this price, most people genuinely can’t afford to use it. Whether it’s worth it depends on whether your time or your money is more expensive.

But honestly, what left the deepest impression on me this time wasn’t Fable 5’s raw ability—it was the way Anthropic released it.

The same model, wrapped in safety guardrails of different strictness, then split into a general version and an unlocked version for different audiences. When it encounters sensitive issues, it doesn’t directly refuse—it downgrades to the previous-generation model to answer instead. We’ve seen examples before of models downgrading under rate limits, but Anthropic seems to be the first to make this sort of “tiered release” a core product-level mechanism from the very design stage.

My judgment is that as models become more powerful, this pattern will probably be copied by more and more companies. In the future, the “latest and strongest model” you think you’re using might quietly switch into a different model midway through use.

**As users, the very least we should do is know that this is happening.**
