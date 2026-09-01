# Kimi K3 Coding Benchmark - 7 Real Project Case Studies

> I used Kimi Code to run 7 real projects, from front-end animation to full-stack products, to see what K3’s coding ability is really worth.

Hello everyone, I’m Yupi.

Kimi has just released its strongest model to date: K3, the world’s first open-source large model at the 3T scale, focused on coding ability.

Its highlights include 2.8 trillion parameters, a million-token context window, native multimodality, and it will be **open-sourced** on July 27.

![](https://pic.yupi.icu/1/image-20260717092743195-20260717144612283.png)

At first I was pretty calm, because I had just been bombarded by Claude Fable 5 and GPT-5.6 one after another, so I’d become numb to new models lately.

**But this K3 doesn’t seem that simple...**

Today when I opened Twitter, my whole feed was flooded with Kimi K3.

The most surprising part was that K3 took **the number one spot** on the Arena.ai front-end coding arena, even surpassing Claude Fable 5 and GPT-5.6 Sol!

This is the first time an open-source model has topped that leaderboard. Kimi really made us proud!

![](https://pic.yupi.icu/1/image-36-scaled-20260717144612360.png)

Now let’s look at the other benchmark scores. On Terminal-Bench 2.1, which tests terminal coding and Agent workflow ability, K3 scored 88.3%, close to GPT-5.6 Sol’s 88.8% and ahead of Fable 5’s 84.6%. On Program Bench, which tests completion of multi-step coding tasks, K3 scored 77.8%, beating GPT-5.6 Sol’s 77.6% and Fable 5’s 76.8%!

Still, on more complex engineering benchmarks like DeepSWE and FrontierSWE, it still trails Fable 5 and Sol.

![Kimi K3 benchmark comparison](https://pic.yupi.icu/1/1d9chlgn6rtp4tqfnnmjg-20260717144612482.png)

But benchmarks are just benchmarks. Whether a model is actually useful still has to be tested with real projects.

In this article, I’ll use Kimi’s own AI coding tool, Kimi Code, and test K3’s real coding ability through **7 different types of projects**, ranging from simple front-end animation to complex full-stack products, step by step.

My heart is racing, my hands are shaking—let’s begin~



## Installing Kimi Code

First, go to the [Kimi Code official website](https://www.kimi.com/code) and copy the installation command, then run it in your terminal:

![](https://pic.yupi.icu/1/1784171620008-ffaf4ccb-8b91-4559-94e7-b8bf142c3a0f-20260717144613039.png)

After installation, type `kimi` in the terminal to enter Kimi Code, then run the `/login` command to log in through the web:

![](https://pic.yupi.icu/1/1784211829361-e461a0d2-76c7-4033-b417-3d201343ac94-20260717144613127.png)

After logging in successfully, type `/model` to switch the model to K3. At the moment, K3’s thinking mode only supports `max`, with `low` and `high` coming later:

![](https://pic.yupi.icu/1/1784211934461-a4897b78-aa9a-423c-b461-c2177b7bff4c-20260717144613240.png)

Once the switch succeeds, you can see below that the current model is now K3, and the context window shows 1M. Now we can really let it rip~

![](https://pic.yupi.icu/1/1784211973313-458de0b1-1f05-41d7-b0b3-6c99f5a66811-20260717144613435.png)

Like Claude Code, Kimi Code supports Skills extensions. Since I had already installed many skills in the common AI coding tools directory `~/.agents/skills/`, Kimi Code automatically scanned and loaded them, so I didn’t need to reinstall them.

Type `/skill` in Kimi Code to view the installed skills:

![](https://pic.yupi.icu/1/1784172987287-9e55701a-3045-467e-b093-02a4a98db463-20260717144613497.png)

In the following tests, I’ll use Context7 for documentation search, Firecrawl for web search and page scraping, browser-use for browser control, and more.

The environment is ready. Next comes the real benchmarking.



## Project Benchmarking in Practice

This time, I prepared **7 projects** to test K3’s coding ability, gradually moving from simple front-end pages to complex full-stack products:

1. Interactive animated explainer website
2. 3D animated knowledge explainer
3. Turning copy into a web PPT
4. Web PPT generator tool (with built-in AI model)
5. Soccer battle web game (cross-model comparison)
6. The Binding of Isaac roguelike game
7. Full-stack AI coding tool (a Cursor clone)

Let’s go through them one by one.



### 1. Interactive Animated Explainer Website

For the first project, I asked K3 to generate a website that explains knowledge through interactive animation.

Using the “attention residual” mechanism introduced in K3 itself as the example, I asked the model to explain its own core technology through animation.

In the prompt, I told the AI to first use the Firecrawl skill to search the web for technical details about attention residuals, making sure the explanation was accurate rather than hallucinated due to outdated training data:

![](https://pic.yupi.icu/1/image-20260717111349321-20260717144613538.png)

After K3 finished the task, I could see that it really had used Firecrawl to search related papers and explanations online. It also verified both desktop and mobile rendering through screenshots, then fixed layout issues on its own when it found them.

This is actually K3’s multimodal engineering ability at work. In the official blog, they call it “vision in the loop”: after coding, the AI takes a screenshot to check whether the result looks right, and if not, it fixes it. It’s like the AI has its own pair of eyes to inspect its work.

![](https://pic.yupi.icu/1/1784182068361-f421d08f-a157-42f0-8cc3-606e69afa6f7-20260717144613862.png)

Now let’s look at the final result. K3 breaks the principle of attention residuals into several stages, with each stage paired with an interactive animation.

The first part uses the analogy of “cooking soup” to explain the problem. In a standard Transformer, residual connections add the output of each layer into the information flow with equal weight. Once there are many layers, the signal from the early layers gets drowned out by the later ones. The website compares this to 100 chefs taking turns adding seasoning to one giant pot, until the original broth added by the first chef is almost impossible to taste.

Users can control the rate of adding ingredients with a slider and watch the information being diluted in real time:

![](https://pic.yupi.icu/1/1784181755536-d293e9bf-8eb5-4ad8-af7f-4eef6da47067-20260717144614356.png)

The second part moves into an interactive demo of the core mechanism. Users can drag sliders to assign attention weights to different layers and see the normalized attention distribution change in real time after softmax:

![](https://pic.yupi.icu/1/1784181771104-8becb2f1-a011-4d45-9741-3daf5bc35a50-20260717144614853.png)

Finally, it also visualizes the engineering implementation of chunked attention residuals. Users can adjust the total number of layers and chunks to directly feel how the chunking strategy affects memory usage:

![](https://pic.yupi.icu/1/1784181796772-02fc0cdb-545f-431b-a2c7-f64a0db97847-20260717144614997.png)

All of that was done with a single prompt in under 5 minutes.

I’m very satisfied with the result. The connections between points and lines are accurate, the animation transitions are smooth, and the aesthetics are solid.

Previously I usually used Claude for this kind of interactive animation website, and it would often have element misalignment issues. K3 really does have some serious front-end skills. No wonder it ranked first on the Arena front-end leaderboard. From now on, I can confidently hand this kind of animation work over to it.



### 2. 3D Animated Knowledge Explainer

This time I used the same knowledge point as in the first test, but presented it in a 3D scene instead.

In the prompt, besides telling the AI to search the web, I also required it to use Context7 to look up the latest documentation for the 3D library it used, avoiding outdated APIs:

![](https://pic.yupi.icu/1/image-20260717111408539-20260717144615047.png)

Before running this task, I first enabled `/yolo` mode.

Once enabled, the AI automatically approves safe tool calls, so I don’t have to manually confirm them one by one. It’s suitable for known-safe development tasks like this:

![](https://pic.yupi.icu/1/1784212052027-a60efe1d-787b-4e1c-9ff3-3f6618947f21-20260717144615340.png)

Now let’s look at the final result. The interface has no unnecessary elements; the focus is entirely on the 3D animation demo. There’s a step-control panel in the lower left, so the explanation can progress stage by stage:

![](https://pic.yupi.icu/1/1784181948833-d092b7b8-abc2-42c4-9c8c-bfcd38cef470-20260717144616007.png)

I can drag the mouse to freely adjust the view, and the nodes and connecting lines in 3D space clearly show how information flows through each Transformer layer:

![](https://pic.yupi.icu/1/1784181917700-09e53717-bbf1-42c1-9f4e-c17413ace9f1-20260717144616347.png)

Both animated explainer websites were completed with a single prompt. The speed was fast and the results were good.

This kind of front-end creative project is exactly the sort of scenario AI coding is best at, and Kimi has always had a good reputation for front-end generation. K3 continues that advantage.



### 3. Turning Copy into a Web PPT

When I make video tutorials, I sometimes need to turn article content into presentation slides.

But making PPTs by hand is too slow...

So this time I simply threw a technical article directly to K3 and asked it to break the content down into a full-screen web PPT following the article’s explanation order, so I could later use it as on-screen material for video recording.

The prompt was very simple:

![](https://pic.yupi.icu/1/image-20260717111421384-20260717144616722.png)

The AI finished it quickly. The result has a strong tech vibe. You can see that K3 automatically identified the article’s structure hierarchy, marked the key points on each PPT page, and even highlighted code blocks:

![](https://pic.yupi.icu/1/1784182284219-2a17237b-b739-4def-ac14-4361bc39fd3d-20260717144617743.png)

From now on, when I need to explain something to others, this kind of PPT is much clearer than throwing a wall of article text at them.

The page-turning animation is also fairly smooth, supporting the left and right arrow keys as well as the space bar. The mobile layout is reasonable too:

![](https://pic.yupi.icu/1/1784182350543-fb631ebf-e7aa-4bdc-9d69-4988b5869e1b-20260717144617905.png)

If you want images in the PPT, just tell the AI to place the images from the article into appropriate positions.



### 4. Web PPT Generator Tool (with Built-in AI)

The first three were just appetizers, mainly testing K3’s front-end creativity and content-structuring ability.

Now it’s time to test its full-stack engineering ability by asking AI to build a complete application integrated with a large model.

In the last example, it generated a PPT from a given article. But can that ability be turned into a general-purpose tool?

The user pastes any piece of text, the back end calls an AI large model to break down the content, the front end renders it into a presentable web PPT, and it also supports switching themes and exporting HTML.

This time I used Kimi Code’s built-in `/goal` command to execute it. The full prompt was:

![](https://pic.yupi.icu/1/image-20260717111459584-20260717144618089.png)

This command puts the AI into autonomous goal mode, letting it keep working across multiple rounds until the task is complete without human intervention. It’s perfect for complex long-horizon development tasks like this.

Note that I directly wrote Kimi Code’s API Key into the prompt, so the AI could autonomously connect the large-model interface and finish testing:

![](https://pic.yupi.icu/1/1784212180951-43c52af1-007f-4f1b-8582-78edd9c7defc-20260717144618309.png)

After K3 finished, the logs showed that it ran two sets of end-to-end Playwright tests, both desktop and mobile passed, and it thoughtfully wrote the API Key into `.env` while also adding it to `.gitignore`, so it wouldn’t leak into version control:

![](https://pic.yupi.icu/1/1784182502815-67d51dcf-29fc-438a-a725-88357a126380-20260717144618858.png)

Now let’s look at the final interface. It’s extremely minimal, centered around a single input box for pasting text. I pasted in the Loop Engineering tutorial I wrote earlier and clicked Generate PPT:

![](https://pic.yupi.icu/1/1784182758933-6b75a1c9-f922-437b-8c85-0115cdea665e-20260717144619030.png)

The AI split the text into 11 PPT pages, each with a title and key points:

![](https://pic.yupi.icu/1/1784182820142-e3568d65-e8d9-4f9d-80a6-e35fb240f07e-20260717144619691.png)

You can switch the built-in theme colors at any time, and both full-screen presentation and HTML export work properly:

![](https://pic.yupi.icu/1/1784182924437-2dfeda13-6f0f-4979-85ca-515c6286a63f-20260717144620501.png)

The only downside is that the application it developed is rather simple. It didn’t add tool-calling or other Agent-like capabilities to the large model, so the resulting PPT is a bit too minimal.

But at least the core business workflow is fully running end to end. From pasting text to generation, preview, theme switching, and export, every link works properly. As a first demo, it’s already enough. You can just let AI keep iterating on it later.



### 5. Soccer Battle Web Game

When GPT-5.6 was released earlier, I wrote an article called *Comparison of Top Overseas Models*, where I used the same prompt to have GPT-5.6 Sol, Claude Fable 5, and Grok 4.5 build a soccer game called “2066 World Cup Showdown” at the same time.

This time I used the exact same prompt for K3 and did a direct side-by-side comparison to see whether a domestic model could take the crown.

I also executed it in `/goal` mode. The prompt required it to follow a Loop Engineering workflow: first build a minimally playable version, self-test each feature after finishing it, fix problems when they appear, and do full acceptance testing before delivery.

![](https://pic.yupi.icu/1/1784212215001-dd8b856c-c210-458a-9028-fbab5050ace4-20260717144620566.png)

After about 17 minutes, K3 finished the goal.

For the technical stack, it chose Node.js + Express + SQLite for the back end, and handwrote the physics engine on the front end with Canvas. This choice matches GPT-5.6 Sol’s earlier thinking, and it’s reasonable for a game of this size:

![](https://pic.yupi.icu/1/1784182979895-6c1425b5-1b1e-49a8-8e7a-cd4e25cbd3d7-20260717144620711.png)

Now let’s play a match—Spain vs. Argentina!

The pre-match setup screen is decent enough. You can choose difficulty, match duration, team name, and colors:

![](https://pic.yupi.icu/1/1784183295400-9db9775e-5666-400f-994e-0eeb6b77b4f8-20260717144620787.png)

Once you enter the match, the field layout is fairly standard, and switching players and kicking the ball both work properly.

But the AI-opponent algorithm is a bit simple. Only the player I currently control charges forward alone, while my other teammates all stand in the back watching like bystanders. Meanwhile, the AI’s tactic is basically to form a human wall and block me:

![](https://pic.yupi.icu/1/1784183345124-cfa1e19d-6ee3-4487-b31b-c164d1f53d00-20260717144621824.png)

The goalkeeper’s defense is practically watertight and always manages to stay in the path of my shots. As a result, I played several matches on medium difficulty and every single one ended 0:0:

![](https://pic.yupi.icu/1/1784183683653-faafeeba-b8fd-46df-8182-fee7303188c2-20260717144622038.png)

Let’s compare it with the other models I tested earlier.

Starting with the good part: K3’s controls and physics engine have no obvious bugs. The ball doesn’t teleport and doesn’t clip through objects. Compare that with Claude Fable 5, whose physics engine broke down and made the ball constantly teleport, leaving the game basically unplayable.

![](https://pic.yupi.icu/1/1783648857986-4d1edca9-1496-494c-80b1-096690b34bc4-20260717144622560.png)

Compared with Grok 4.5, which had serious field-rendering flaws and awkward player-switching logic that often switched to the teammate farthest from the ball:

![](https://pic.yupi.icu/1/1783648020795-d1809bda-6c3c-4e36-babf-a3f6e9e494e1-20260717144623018.png)

K3 clearly passes the basic test of “can you actually play it normally,” and the experience is better than both Fable 5 and Grok 4.5.

But compared with GPT-5.6 Sol, there’s still a gap. GPT-5.6 Sol finished the whole development in only 9 minutes, and although its AI wasn’t that smart either, at least there were some scoring opportunities.

![](https://pic.yupi.icu/1/1783647330206-bb64786d-95d9-41e5-9d53-4fb42ffdd9da-20260717144623818.png)

K3’s tactical intelligence on the AI-opponent side is clearly weaker than Sol’s. From a gameplay perspective, it’s still some distance away from being truly “fun.”

Overall, K3 ranks in the upper-middle tier on this project. For a domestic model to perform like this already exceeded my expectations.



### 6. The Binding of Isaac Roguelike Game

Next comes a more challenging game project.

The Binding of Isaac was a roguelike game I loved as a kid, and this time I asked K3 to recreate its core gameplay, including random dungeon generation, shooting combat, an item system, multiple enemies, and Bosses.

The prompt required it to first use Firecrawl to search for information about The Binding of Isaac’s gameplay mechanics and art style, and then use Context7 to look up the game framework documentation:

![](https://pic.yupi.icu/1/1784212259593-16d5f314-9b40-4651-851b-c61dcf8d8c7c-20260717144625002.png)

After K3 finished the goal, it reported that it had used Firecrawl to study the game mechanics and art style, used Context7 to check the latest docs for the chosen game engine, and automatically played and validated the result with Playwright screenshots after each step, fixing multiple issues along the way. In the final test, it successfully implemented a full gameplay loop from the start through defeating the third-floor Boss:

![](https://pic.yupi.icu/1/1784185068039-17f4980f-618e-46eb-a1c2-68f752637f5f-20260717144627576.png)

Now let’s play it.

Although the interface looks rough, the core gameplay loop works perfectly—you can shoot bullets and hit monsters:

![](https://pic.yupi.icu/1/1784190076766-03662fe2-7400-4938-87d1-422f3d992bd7-20260717144628318.png)

Those who’ve played the original game will probably notice a small detail: the AI-generated character has tears, which is a nod to the original Isaac character design:

![](https://pic.yupi.icu/1/1784184670536-65377053-11ea-4c54-b0f6-e48318b1d955-20260717144629472.png)

In the game you can kill monsters, pick up items, and open treasure chests. After picking up an item, stats like attack power and fire rate change in real time, and the current status is displayed at the top of the screen:

![](https://pic.yupi.icu/1/1784184864353-d099812b-21e7-4cdc-a0e6-43fe80b45a24-20260717144630414.png)

It also created multiple enemy types: some chase you, some shoot from range, some charge straight at you, and there’s even a Boss that fires bullet patterns and summons little monsters!

![](https://pic.yupi.icu/1/1784184823083-d46122a9-8b45-4719-a69d-c8eeda7906aa-20260717144631052.png)

Overall, the entire gameplay loop is already fully connected. From starting the game to clearing rooms, picking up items, and fighting Bosses, everything works.

**And don’t forget—we only used one round of prompting, with no follow-up iteration at all.**

If I wanted to seriously turn this into a proper game later, all I’d need to do is provide more art assets and add more items, monsters, and level designs.



### 7. Full-Stack AI Coding Tool

For the final project, I cranked the difficulty all the way up!

I asked K3 to build a web AI coding tool similar to Cursor based on VS Code’s open-source code, supporting both Editor Window code editor mode and Agents Window conversation workspace mode.

In the prompt, I required it to first use Firecrawl to search for the product design of Cursor 3, then use Context7 to look up VS Code extension API documentation:

![](https://pic.yupi.icu/1/1784212308866-3738611f-e9c5-4546-a161-d96611a13d68-20260717144631641.png)

This task ran for over half an hour. K3 first cloned the VS Code source as reference, used Firecrawl to study Cursor’s official blog and third-party guides to understand the product design, then built a complete web IDE step by step, validating each step with browser screenshots along the way:

![](https://pic.yupi.icu/1/1784190241907-868bceef-a1b5-4fe6-80b9-536ffc0d0738-20260717144632037.png)

Now let’s look at the final product.

By default it opens in Editor Window, which is the code editor interface. It has a file tree, multiple tabs, and syntax highlighting, and it can browse and edit code normally:

![](https://pic.yupi.icu/1/1784190810038-c3d24d7d-f500-46ff-bb62-b2c9205005f2-20260717144633410.png)

Switch to Agents Window, and this becomes the familiar AI conversation workspace.

I asked it to build a Snake game, and you can see the AI calling the `RUN_COMMAND` tool to first run `ls -la` and understand the current project structure:

![](https://pic.yupi.icu/1/1784190877508-637d8580-e58d-4810-b54a-d740da2b6be6-20260717144634958.png)

Next, the AI runs more commands, analyzes the project’s current file structure, and completes the development task on top of the existing workspace:

![](https://pic.yupi.icu/1/1784190957997-f207d1e5-3b65-4005-9a6e-392ecd25f328-20260717144635325.png)

Although there’s still a big gap compared with a mature product like Cursor, the core dual-window Editor + Agent capability is running end to end.

This was the most complex long-horizon task among the 7 cases. K3 was able to understand a huge codebase like VS Code, search online for product design, consult API docs, and independently complete the development, all without freezing or drifting off course during more than half an hour of work. That demands a lot from a model’s long-context stability and autonomous planning ability.



## Final Thoughts

All 7 projects are done, so let me share my real impressions.

First of all, **the thing that surprised me most about K3 is its stability**. All 7 projects ran successfully right away. Both the front end and back end started without errors, and the core features all worked.

When I tested other domestic models before, I often ran into cases where dependencies wouldn’t install, services failed to start, and I had to ask AI to fix things in another round before the project could run.

K3 is clearly much more stable in that respect. It reminded me of when Claude Opus first came out—it firmly passed the “usable” threshold.

The model’s execution speed is also quite good. Simple projects were generally finished within a few minutes, while the most complex AI IDE project took a bit over half an hour.

**Front-end ability is K3’s strongest direction.** Judging from the Arena front-end leaderboard data, K3 really has surpassed Fable 5 and Sol in front-end work. Based on my own hands-on testing, I feel the same way: the aesthetics and accuracy of its animated websites were even better than what I used to get with Claude, and its PPT layout and color design also had a solid sense of design.

**However, its overall task completion still lags behind the top overseas models.**

For example, if you ask it to make a game, it may be playable, but it’s still some distance away from a publishable finished product. To build those blockbuster games shown in Kimi’s official demos, it still needs several more rounds of iterative optimization.

![](https://pic.yupi.icu/1/image-20260717111152646.png)

Now let’s look at the cost, which everyone cares about most. [K3’s official blog](https://www.kimi.com/zh-cn/blog/kimi-k3) published the following API pricing:

| Model | Input (cache hit) | Input (cache miss) | Output |
| ----- | ----------------- | ------------------ | ------ |
| Kimi K3 | $0.30 / million tokens | $3.00 / million tokens | $15.00 / million tokens |
| Claude Fable 5 | $2.50 / million tokens | $10.00 / million tokens | $50.00 / million tokens |

Because Kimi’s Mooncake disaggregated inference architecture achieves over 90% cache hit rate in coding scenarios, most input is effectively billed at only $0.30, making it an order of magnitude cheaper than Fable 5.

I personally use Kimi Code’s top-tier Vivace plan, and after running all 7 of these projects—including the half-hour AI IDE build, the 17-minute soccer game, and all kinds of front-end animations and full-stack apps—this week’s usage only consumed **2%** of my quota. From now on, I can really Vibe Code as much as I want. Million-token context, use it freely.

![](https://pic.yupi.icu/1/image-20260717141420121-20260717144636656.png)

For developers in China, there’s no need to deal with overseas payments or worry about account bans. You can just subscribe directly and use a million-context coding model. And most everyday development tasks don’t need a model like Claude Fable 5 anyway. For writing tools, building websites, prototyping, or office automation, K3 is more than capable enough.

By the way, K3 can be used not only inside Kimi Code, but also through a VS Code plugin, or by connecting it to Claude Code and Codex with CC Switch.

![](https://pic.yupi.icu/1/image-20260717102305034-20260717144636779.png)

And finally, a few honest words.

I’ve tested a lot of domestic models. Most of the time my feeling has been, “usable enough, but still missing something.” But with K3, this is the first time I’ve truly felt that a domestic coding model is something I can use in my daily work—and use comfortably.

It’s stable enough, its front-end ability even surpasses top overseas models, its cost is only a fraction of Claude’s, and it also supports million-token context and multimodal ability.

Although it still trails Fable 5 and Sol in fine-grained quality on complex tasks, K3’s release gave us real confidence: **domestic models have finally stood up in the coding field!**

If you’re also interested in AI coding, try different models and tools for yourself. Use real projects to feel the differences in their capabilities. The world of AI coding changes fast—stay curious, keep experimenting, and you’ll definitely find the programming partner that suits you best!
