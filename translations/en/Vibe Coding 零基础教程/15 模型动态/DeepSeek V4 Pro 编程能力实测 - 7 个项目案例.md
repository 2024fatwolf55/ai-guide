# DeepSeek V4 Pro Coding Benchmark - 7 Real Project Case Studies

> From front-end animation to full-stack products, using 7 real projects to test the official release of DeepSeek V4 Pro.

Hello everyone, I’m Yupi.

DeepSeek has just quietly released the official version of the DeepSeek V4 Pro model, and it can already be called through the API.

![Announcement from the official DeepSeek group](https://pic.yupi.icu/1/deepseek%20v4%20pro%20%E5%8F%91%E5%B8%83%E7%BE%A4%E8%81%8A.jpg)

The new version supports a 1M context window and up to 384K output, further strengthens Agent capabilities, and supports the Responses API, making it easy to connect to Codex.

Let’s first look at the benchmark chart released by DeepSeek:

![Official benchmark comparison for the DeepSeek V4 Pro release](https://pic.yupi.icu/1/deepseek%20v4%20pro%20%E8%B7%91%E5%88%86%E5%9B%BE.jpeg)

The most eye-catching one is Terminal Bench 2.1, which tests whether a model can independently complete a full programming task in the terminal.

The official DeepSeek V4 Pro release scored 87.9, while Claude Fable 5, one of the top foreign models, scored 88.0.

**Only 0.1 apart!**

![](https://pic.yupi.icu/1/image-20260813145727335.png)

Compared with the previously released DeepSeek V4 Preview, the gains on several other metrics are also dramatic: DeepSWE rose from 12.8 to 62.7, Cybergym from 52.7 to 83.3, and NL2Repo from 38.5 to 61.5. These benchmarks are really testing the same thing: can the model enter a real environment with tools and carry a multi-step job all the way from start to finish?

There are also weaker areas. For example, on HLE, a pure knowledge exam, DeepSeek V4 Pro scored 42.7, while Claude Opus 4.8 scored 49.8 and Claude Fable 5 scored 53.3. The gap is still quite obvious. But HLE tests encyclopedic knowledge and general reasoning, which doesn’t relate that much to everyday coding. What really determines the AI coding experience are the Agent and Coding benchmarks above.

Benchmark scores are just benchmark scores. Whether a model is actually good to use still has to be tested on real projects.

So this time I prepared **7 different types of projects**, ranging from simple front-end animation to complex full-stack products, to comprehensively evaluate DeepSeek V4 Pro’s programming ability.

![Summary chart of the 7 test projects (from easy to hard)](https://pic.yupi.icu/1/01_7%25E4%25B8%25AA%25E6%25B5%258B%25E8%25AF%2584%25E9%25A1%25B9%25E7%259B%25AE%25E6%25B1%2587%25E6%2580%25BB%25E5%259B%25BE%25EF%25BC%2588%25E7%2594%25B1%25E6%25B5%2585%25E5%2585%25A5%25E6%25B7%25B1%25EF%25BC%2589_compressed_v1.png)

Worth mentioning: for this test, I specifically topped up 300 RMB into my DeepSeek account.

![](https://pic.yupi.icu/1/9b1f5e5fa70dc82f190bf0d3818a92ad.jpg)

Want to guess whether those 300 RMB were enough?

I’ll reveal the answer at the end~



## First, Build a Harness for DeepSeek V4 Pro

For this test, I used Codex, a mainstream AI coding tool, to run all the tasks.

Connecting DeepSeek V4 Pro to Codex CLI isn’t difficult. This time, the official release specifically adapted to the Responses API and Codex, so you can run it just by tweaking the configuration file. For the detailed steps, you can read *Connecting Domestic Models to Codex* in the “Codex” directory under the Coding Tools section of this tutorial and just follow along.

![](https://pic.yupi.icu/1/image-20260803114842807.png)

The real trouble came from two other things.

DeepSeek V4 Pro is a text-only model, so it can’t see images. That means it can’t do what Kimi K3 or Claude Opus 5 can do—finish a page and then take a screenshot to check whether the result looks right. It also means it can’t be compared under completely fair conditions with earlier models that have visual understanding.

Also, those official benchmark numbers weren’t produced by the raw model alone. For the Code Agent tasks in the public benchmarks, they used **DeepSeek Harness minimal mode**, and at the max reasoning tier.

Harness refers to the engineering layer that brings model capability into a real environment. It handles tool invocation, file reading and writing, context management, and error handling, allowing the model to carry a task from start to finish.

The problem is that the official Harness still hasn’t been released.

So I built one for it myself~

This Harness isn’t complicated. It mainly does 4 things:

1. Unified execution environment: all tasks use the same startup script, the same reasoning tier, and each task gets its own directory and port so they don’t interfere with each other
2. Playwright verifier: since the model can’t see images, let scripts capture console errors, network requests, and DOM assertions for it, while also saving screenshots for manual review
3. Token cost reconciliation: save the event stream during task execution as JSON files, calculate cost using official pricing, and cross-check by checking account balance before and after the test
4. 90-minute watchdog: once time is up, force-stop the task; failed tasks are not rerun, keeping the data clean

Once the prep work was done, I used Cursor to throw out all 8 executions in parallel in one shot. No manual intervention was needed at all, and I reviewed them one by one after everything finished.

![Cursor parallel scheduling of 8 subtasks](https://pic.yupi.icu/1/image-20260813150439721.png)



## Project Benchmarking in Practice

This time I prepared **7 projects** to test DeepSeek V4 Pro’s coding ability, ranging from simple front-end animation to complex full-stack products, going from easy to hard.

1. Interactive animated explainer website
2. 3D animated knowledge explainer
3. Bamboo cicada simulation web game
4. Web PPT generator tool (with built-in AI model)
5. Online lottery system
6. The Binding of Isaac roguelike game
7. Full-stack AI coding tool (a Cursor clone)

Let’s go through them one by one.



### 1. Interactive Animated Explainer Website

For the first project, I asked the model to build a website that explains knowledge through interactive animation, focusing on “attention residuals.”

In the prompt, I required it to first use Firecrawl to search online for technical details to ensure the explanation was accurate, then verify the result on its own after finishing. If it wasn’t satisfied, it had to adjust autonomously until the result looked right before delivering.

![](https://pic.yupi.icu/1/1786602835584-bcee4f23-f247-4daf-825e-b3fede5336e8.png)

Let’s first look at the opening screen.

You can already see the problems: not only is the animation very simple, but the text inside the animated blocks is already overflowing the borders...

![](https://pic.yupi.icu/1/1786598739739-3e7bd75c-7b0a-4b70-90c7-df48b6352442.png)

Scrolling down to the AI’s explanation of the core mechanism, the connecting lines in the diagram in the middle are obviously wrong, and the nodes are visibly misaligned.

![](https://pic.yupi.icu/1/1786598800323-d83866da-24d8-4d07-9de8-72468e9102e8.png)

Further down in the interactive demo section, the text overflow and connector misalignment become even more obvious. On top of that, the animation feels perfunctory and isn’t very interactive at all.

![](https://pic.yupi.icu/1/1786598853316-6b7bf7aa-79df-447d-8e02-8f69f75fa79b.png)

Now compare it with what other models produced earlier using the exact same prompt.

Kimi K3 explained the problem clearly with the analogy of “100 chefs taking turns adding seasoning,” with smooth animation and solid aesthetics:

![Interactive animation built by Kimi K3](https://pic.yupi.icu/1/1784181755536-d293e9bf-8eb5-4ad8-af7f-4eef6da47067-20260717144614356-20260813162823259.png)

Claude Opus 5 did even more. It added floating light particles in the background and even included a few in-class quiz questions to check whether users had learned the concept, making it feel more like a systematic educational website.

![Interactive animation built by Claude Opus 5](https://pic.yupi.icu/1/1785144666553-66077ab6-a75d-4730-84d7-963dc05f8a50-20260813162823373.png)

Looking back at DeepSeek V4 Pro’s version, the text overflow, misaligned connectors, and perfunctory animation make the front-end result clearly underwhelming.

My verdict: **weak**.



### 2. 3D Animated Knowledge Explainer

Still the same knowledge point, but this time presented in a 3D scene.

Besides web search, I also required it in the prompt to use Context7 to look up the latest documentation for the 3D library it used, so it wouldn’t write code with outdated APIs.

![](https://pic.yupi.icu/1/1786602849416-8d6307ed-32b5-49ae-8558-340cc5a4c6c0.png)

Looking at the result, the overall website uses a tech-style color scheme, with flying particle effects in the background. The layout is clear, and you can learn the concept and control the animation steps through the panel in the lower left.

![](https://pic.yupi.icu/1/1786599058417-3f7f71fc-de84-4beb-acf3-8873ddaf0deb.png)

The 3D animation rotates and zooms properly, with no obvious misalignment and no stuttering at all. The engineering idea of chunked attention residuals is also visualized with golden connector lines.

![](https://pic.yupi.icu/1/1786599132799-f2c6662c-1def-4f3a-9a32-07b68602dfc6.png)

But compared with the earlier models, there’s still a gap.

Kimi K3’s version was clean and direct, with the focus entirely on the 3D animation demo, and the 3D effects were more vivid:

![Kimi K3’s 3D version](https://pic.yupi.icu/1/1784181948833-d092b7b8-abc2-42c4-9c8c-bfcd38cef470-20260717144616007-20260813162823984.png)

Then look at Claude Opus 5’s version: I was blown away the moment I opened the webpage. The tech vibe was explosive, and it could even compare multiple residual patterns side by side:

![Claude Opus 5’s 3D version](https://pic.yupi.icu/1/1785145067089-c8c05cfb-e1a3-4f3c-abe8-e3c30aa1390e-20260813162824079.png)

By comparison, DeepSeek V4 Pro’s 3D animation feels much simpler and didn’t really wow me.

My verdict: **NPC**.



### 3. Bamboo Cicada Simulation Web Game

The bamboo cicada is a traditional Chinese bamboo toy: a thin bamboo blade is threaded onto a bamboo stick. You rub the stick with your hands to spin the blade at high speed. As it cuts through the air, it creates vibrations that make a “wa-wu wa-wu” sound like a summer cicada.

![](https://pic.yupi.icu/1/1786602860735-55ee064d-1521-4501-847d-c12a0cfe9fc4.png)

This task simultaneously tests front-end visuals, a physics engine, and real-time sound synthesis. And whether the result is good can only be judged by listening and by feel while playing it—pretty code alone is useless.

Let’s first look at what DeepSeek V4 Pro produced. The interface is fairly ordinary. It symbolically drew a few little bamboo stalks, but there isn’t much atmosphere.

![](https://pic.yupi.icu/1/1786599373401-a561d583-aeca-46c3-9895-d55c9356e731.png)

The gameplay is simple: drag with the mouse to spin the bamboo cicada. The page also supports motion-control mode, where shaking your phone or rotating your wrist can drive the blade.

![](https://pic.yupi.icu/1/1786599484181-ade4c638-69c4-443a-8f04-d579cbf4562d.png)

But the sound it makes is more like “buzz buzz buzz,” which doesn’t match the “wa wa wa” cicada-like sound I wanted at all. It doesn’t deserve to be called the best toy under 10 million!

For this task, I also ran DeepSeek V4 Flash with the same prompt for comparison, and the result was surprisingly interesting. The structure of the bamboo cicada changed, and the sound was actually closer to the kind of “wa wa” sound I wanted.

![](https://pic.yupi.icu/1/1786599660114-de1a0f89-2070-41ae-a3a8-5894c88dd2a2.png)

What’s going on? It somehow feels like this version’s front-end result is actually better than the Pro version???

But overall, both versions are just so-so. No real surprises.

My verdict: **NPC**.



### 4. Web PPT Generator Tool (with Built-in AI)

The first three were just appetizers. Now it’s time to test its full-stack engineering ability.

The user pastes a long piece of text into the webpage, the back end calls a large model to break it down into a multi-page PPT structure, and the front end renders it into a web PPT that supports full-screen presentation and keyboard page-turning. It also needs to support switching color themes and exporting an HTML file. The back end should stream output, and the front end should display generation progress in real time.

![](https://pic.yupi.icu/1/1786602871186-1801d617-e049-4a66-93d9-a37a3b25367f.png)

This task is effectively a double test for DeepSeek V4 Pro. The project code was written by it, and the built-in large-model API inside the project also points to itself—killing two birds with one stone by testing both its coding ability and its content-generation ability.

Let’s look at the result. The overall layout and style are fairly standard: the left side is for pasting long text to generate a PPT, and the right side previews the finished slides.

![](https://pic.yupi.icu/1/1786600053816-123fed97-aac5-4e5f-9fa0-f65682ff1978.png)

Paste in a long piece of text and click Generate. In the lower left, you can see the generation progress and the real-time output from the AI model.

![](https://pic.yupi.icu/1/1786600127701-07016adb-59dc-4db9-8fe1-ee167bedd00a.png)

But this “real-time output” isn’t really real-time... After waiting a long while, it seemed like the AI had already finished generating everything before the streaming output began. That’s a pretty obvious bug.

![](https://pic.yupi.icu/1/1786600231061-4224dcb2-ee36-4916-be4d-ee66de73f18c.png)

Now let’s look at the final PPT result. Uh... hard to rate.

![](https://pic.yupi.icu/1/1786600257499-75fdc7f7-740c-4c27-8979-34683f66afcd.png)

The text content is basically all piled up on the left. What’s all that blank space on the right for?

You can switch PPT themes and export as a standalone HTML file, and those features work normally.

![](https://pic.yupi.icu/1/1786600293676-689e0378-6c3d-4bb5-8e4d-b19437d8ab23.png)

Now compare it with the earlier models.

Kimi K3’s version was rather rough:

![Kimi K3’s PPT tool](https://pic.yupi.icu/1/1784182758933-6b75a1c9-f922-437b-8c85-0115cdea665e-20260717144619030-20260813162825827.png)

Claude Opus 5’s version felt much more like a mature tool product. It gave the color themes evocative names like Aurora and Ivory, and even added a feature for “entering extra generation requirements” on its own:

![Claude Opus 5’s PPT tool](https://pic.yupi.icu/1/1785146087244-153c15ee-6ffe-4f7b-8c8d-8224fe272074-20260813162825918.png)

By comparison, the front-end result made by DeepSeek V4 Pro is only average and still some distance away from being truly deliverable.

But at least it did run through a complete front-end + back-end AI generation workflow. My verdict is: **top-tier (budget version)**.



### 5. Online Lottery System

Next, I asked AI to build an online lottery system that anyone could use—for company annual meetings, community events, livestream giveaways, and so on.

The admin should be able to create a lottery event, configure prize quotas for each tier, generate a participation link and QR code; participants should be able to open the link and sign up with a nickname; and when the time comes, the admin clicks Draw, and the winning list rolls across the big screen.

![](https://pic.yupi.icu/1/1786602887504-679a0212-cd94-43e3-983c-6d1503d5b705.png)

The earlier questions tested aesthetics and creativity. This one tests engineering rigor.

- Quotas must never be exceeded: if there is 1 first prize, then only 1 person can win it, even if massive concurrent requests arrive at the exact same moment
- The same participant can win at most once in the same event
- The draw operation must be idempotent: even if the admin nervously clicks the Draw button five times in a row, it must still produce only one round of results

Let’s look at the result.

Just from seeing this interface, my expectations immediately dropped. It’s way too ugly! At minimum I thought it would give me a spinning wheel.

![](https://pic.yupi.icu/1/1786600763380-af0f9dd5-7cb5-4046-9669-8b356f720298.png)

Testing the features, the admin backend can successfully create events and configure prize quotas.

![](https://pic.yupi.icu/1/1786600802250-6f303738-7f6f-4b0c-8520-6e4279033d1c.png)

Participants can register by scanning the QR code, which is actually pretty convenient.

![](https://pic.yupi.icu/1/1786600853785-67afb787-6fb6-4554-8122-96b87d8d4029.png)

After the admin runs the draw, participants can see the results in real time:

![](https://pic.yupi.icu/1/1786600931033-5aae5f42-04bd-4311-b977-7efc6ce97fa9.png)

I had other AI help verify the back-end logic: with 1,000 people competing for 100 slots, the total number of winners was exactly 100—no over-allocation and no duplicate winners. So the back-end idempotency and concurrency control were solid.

As a small utility tool, it’s enough. Its one fatal flaw is that it’s just too ugly, too rigid, like a front end produced by a 2024 model. But the back-end logic is sound, so overall I’d rate it **top-tier (budget version)**.



### 6. The Binding of Isaac Roguelike Game

Next comes a more challenging game project.

The Binding of Isaac was a roguelike game I loved as a kid, where the player explores randomly generated rooms, shoots enemies, clears a room to open the door to the next one, and each floor has several rooms plus a Boss room.

![](https://pic.yupi.icu/1/image-20260730215626570.png)

I asked AI to recreate the core gameplay, including random dungeon generation, shooting combat, an item system, a stat system, at least 3 types of normal enemies, and 1 Boss. All visual assets had to be drawn entirely with code.

![](https://pic.yupi.icu/1/1786602896622-3e913641-85d9-4515-8ae9-cb36a6077af9.png)

Since all the visual assets in this task must be drawn stroke by stroke using code, the model itself actually has no clear idea what the result will look like. That’s exactly why this task most clearly exposes the skill gap between different models.

Now let’s look at DeepSeek V4 Pro’s version. The game is called “Basement: Corridor of Tears.” Good grief, even the game title has that unmistakable AI flavor.

![](https://pic.yupi.icu/1/1786601275633-79bedc9a-a388-4038-b489-12cf0c8f3656.png)

Entering the game, it hits hard right away. Just look at this character design—wearing a mask. What am I, a thief? That said, the little tear symbol on the character does pay homage to the original.

![](https://pic.yupi.icu/1/1786601311551-f9bc962b-ab7c-45cf-be16-c325ab7295b2-20260813162826909.png)

But you know what—the game is actually playable, and the experience is surprisingly decent. The monsters also have a bit of the flavor of the original Isaac, and the stat system and treasure chest mechanics are there too.

![](https://pic.yupi.icu/1/1786601335883-7af4e7a2-4a73-4074-b96d-e8633d02561e.png)

You can even fight a Boss, and the difficulty is moderate:

![](https://pic.yupi.icu/1/1786601561806-b4b73523-93f7-4bbe-81c6-161fa903ee25.png)

But the game has only 1 floor. Once you beat the Boss, it ends. It’s very monotonous and still far from a finished product.

Let’s compare it with what earlier models made. Kimi K3’s earlier version looked rough, but the gameplay loop was fully connected—you could shoot bullets, kill monsters, and pick up items:

![Isaac game built by Kimi K3](https://pic.yupi.icu/1/1784184823083-d46122a9-8b45-4719-a69d-c8eeda7906aa-20260717144631052-20260813162826980.png)

Now look at the game Claude Opus 5 made. The moment I opened the homepage, my DNA moved. Many of the small monsters were straight out of the original, and the Boss mechanics were strikingly similar too:

![Isaac game built by Claude Opus 5](https://pic.yupi.icu/1/image-20260801105325549.png)

You can see that DeepSeek V4 Pro is noticeably better than Kimi K3. The monster behavior logic and combat feel are on another level. But the gap between it and Claude Opus 5 is still huge.

My verdict: **top-tier**.



### 7. Full-Stack AI Coding Tool

For the final project, I turned the difficulty all the way up.

I asked it to clone the open-source code of VS Code and build a web AI coding tool on top of that that recreates Cursor’s core experience. It had to support both Editor Window code editing mode and Agents Window conversation workspace mode, allow free switching between the two, and the Agent also had to be able to read files, edit code, and execute terminal commands autonomously.

![](https://pic.yupi.icu/1/1786602907526-9df019bc-5fc8-480b-a26f-abfdcdb50f0c.png)

This was the only long-horizon task among the 7. It tests whether the model can stay stable and avoid drifting when facing a codebase with hundreds of thousands of lines.

Let’s look at the final product. Although it’s still far from the real Cursor, the overall layout is reasonable. In Editor Window mode, it can smoothly open and edit files, with code suggestions and syntax highlighting.

![](https://pic.yupi.icu/1/1786602228169-31beaebe-3162-4d6a-a34f-7e2aef9399c9.png)

Switch to Agents Window and create a new AI conversation, then ask it to help me build a Sokoban game.

![](https://pic.yupi.icu/1/1786602275433-113cbb01-223b-4e62-bfa2-da1448889741.png)

You can see the AI executing commands, calling tools to inspect files, and then writing code on its own. After waiting for a while, the AI finished the development.

![](https://pic.yupi.icu/1/1786602317068-9b7a7666-1f0e-4465-a4b4-a1b3ed8391ad.png)

Once development was done, I directly asked the AI to run the website.

![](https://pic.yupi.icu/1/1786602366637-0640c8f9-d1b1-4c4b-916b-ba5fdae4d289.png)

Now let’s look at the Sokoban game built by my AI coding tool powered by AI. The result is pretty good and fully playable:

![](https://pic.yupi.icu/1/1786602398632-5f0f7f2d-3722-4732-b1cd-75b7e082af65.png)

There’s one detail worth mentioning. Although the prompt required the AI to develop based on the VS Code source code, and the AI really did clone more than 400,000 lines of VS Code code, in practice it turned around and used the `monaco-editor` npm package to start fresh with an independent React app.

From an engineering perspective, that’s actually a reasonable choice. Directly modifying the VS Code source would cost a lot. Still, the AI didn’t exactly ask me first.

Now let’s compare it with earlier models.

First, look at the Cursor clone built by Kimi K3. Its dual-window core capability also worked end to end:

![AI coding tool built by Kimi K3](https://pic.yupi.icu/1/1784190810038-c3d24d7d-f500-46ff-bb62-b2c9205005f2-20260717144633410-20260813162827309.png)

Claude Opus 5’s version almost fully preserved the essence of VS Code—code highlighting, minimap, management panels—the whole thing was a total dimensionality reduction attack!

![AI coding tool built by Claude Opus 5](https://pic.yupi.icu/1/1785147362813-894c3d8b-cb1b-48cf-96ca-9eefd572b4c3-20260813162827347.png)

DeepSeek V4 Pro’s version has both the Editor and Agent windows working, and there are no obvious problems in the interaction experience.

It didn’t crash while developing such a complex long-horizon task, so I can give it a **top-tier** rating.



## My Take

All 7 projects are done, so let me talk about my real impressions.

First, in terms of AI coding ability, DeepSeek V4 Pro’s front-end performance was far below my expectations. The text overflow in the interactive animation, the unbalanced PPT layout, and the stiff visual style of the lottery system were all clearly behind what Claude Opus 5 and Kimi K3 produced.

But its back-end ability is pretty good. The PPT generator ran through a full AI generation workflow, the lottery system handled concurrency control and idempotency properly, and the Agent mode of the full-stack AI coding tool also worked normally.

And most importantly, all 7 projects ran successfully. There were no cases where dependencies failed to install or services failed to start and needed manual rescue.

Overall, in AI coding ability, DeepSeek V4 Pro still has a very obvious gap compared with the top foreign models. You can safely hand back-end logic to it, but if you care about front-end results, you still need a model at Claude’s level.

Another major weakness that strongly affects its AI coding performance is that DeepSeek V4 Pro has no visual understanding. After finishing a page, it cannot take a screenshot and check whether it looks right by itself—whether the layout is misaligned, whether the colors look good, and so on. For this test, I specifically built a Playwright Harness to validate for it, but Harness can only catch errors and do DOM assertions. Judging whether something “looks good” still requires a human.

For example, when it was developing *The Binding of Isaac* game, the floor color logic in the code was technically correct, and the color really was drawn—but it chose a dark color almost indistinguishable from pure black, so to the human eye the whole screen just looked pitch black. The model couldn’t detect that problem at all.

![](https://pic.yupi.icu/1/1786601311551-f9bc962b-ab7c-45cf-be16-c325ab7295b2-20260813162827387.png)

Now for the total amount I spent on this test.

Can you believe it? After running so many projects, it only cost **about 5 RMB**???

I have to say, DeepSeek’s price-performance ratio is genuinely excellent.

![DeepSeek spending panel](https://pic.yupi.icu/1/1786602606582-f5c74b1b-aeaa-4a42-a491-a3d624856ec6.png)

It’s so cheap mainly because DeepSeek’s cache hit rate is insanely high, averaging 99%, which means the billing for most input tokens is almost negligible.

Earlier, when I used Claude Opus 5 to run the same 7 projects, it cost me more than 900 RMB (for the detailed review, you can read *Claude Opus 5 Coding Benchmark - 7 Real Project Case Studies* in this tutorial’s Model Updates section). DeepSeek V4 Pro cost only 5 RMB—**a 180x difference!**

That said, DeepSeek officially said it will soon raise API prices across the board, and by a large margin, so cherish the current price while it lasts and squeeze a little more out of AI first.

![](https://pic.yupi.icu/1/image-20260813154806089.png)

I also did a simple comparison between DeepSeek V4 Pro and V4 Flash. When building the bamboo cicada game, Flash ran for 15 minutes and cost 0.7 RMB, while Pro ran for 11 minutes and cost 0.4 RMB. The completion level and final quality of the two versions weren’t very different.

Honestly, I still haven’t clearly felt a major difference between DeepSeek V4 Pro and V4 Flash. From my own hands-on experience, they feel like models in the same tier, both capable of independently finishing full-stack development tasks.

**But whether it’s front-end quality or the quality of delivered results, there’s still a gap compared with the top foreign large models.**

Still, because time was limited, my testing here wasn’t extensive enough. If you’re interested, you can try it yourself too.

My suggestion is this: while learning AI coding, or for daily small tools, internal systems, and quick idea validation tasks where front-end polish isn’t that important, DeepSeek is completely fine and saves money. If you’re building a user-facing product, you can first use DeepSeek to generate a demo, refine the prompt, and clarify features and business flow, then switch to a model at Claude’s level for systematic development. That way, you save money and stay efficient.

![](https://pic.yupi.icu/1/woquandouyao.jpeg)



## Final Thoughts

At least for me, DeepSeek V4 Pro fell short of expectations. After waiting so long, the official release didn’t really surprise me in terms of AI coding experience.

![](https://pic.yupi.icu/1/620cb309a8d1aaeda1364a6f34c90f25.jpg)

But DeepSeek probably still hasn’t played all its cards.

According to their official formula, **Model + Harness = Agent**. One half—the model—is already delivered, and their in-house Harness framework is probably not far behind.

Once Harness is officially released, DeepSeek V4 Pro’s Agent capability may improve by another level.

Overall, DeepSeek V4 Pro’s strengths are reliable back-end logic and extremely high cost-effectiveness, but its front-end results still lag noticeably behind the top overseas models. If you want a deeper look at the coding capability differences across AI models, you can read the other hands-on benchmark articles in this tutorial’s Model Updates section and find the model that best fits your own scenario.
