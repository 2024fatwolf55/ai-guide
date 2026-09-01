# Claude Opus 5 Coding Benchmark - 7 Real Project Case Studies

> Claimed to match a flagship model at half the price—let’s use 7 real projects to see what Opus 5 is really made of.

Hello everyone, I’m Yupi.

A few days ago, Anthropic released Claude Opus 5. Officially, they claim it can match the capabilities of their most expensive flagship model, Claude Fable 5, at only half the price.

Its benchmark scores are indeed impressive. For example, on Frontier-Bench, which specifically tests whether a model can independently finish a full programming task in the command line, Opus 5 scored 43.3%. The previous-generation Opus 4.8 scored only 18.7%, the top-tier Fable 5 scored 33.7%, and OpenAI’s GPT-5.6 Sol scored 37.5%.

![](https://pic.yupi.icu/1/HOAffmCWsAA1D_X-20260728104640570.png)

But you can’t fully trust benchmark scores. Whether a model is actually useful still has to be tested with real projects.

So in this article, I’ll use **7 different types of projects** to test Opus 5’s programming ability. To compare it fairly with other models, I used exactly the same prompt I used when I previously tested Kimi K3 (you can read *Kimi K3 Coding Benchmark - 7 Real Project Case Studies* in the Model Updates section of this tutorial to learn about that test).

The testing method is simple: I opened multiple sub-agents in Cursor at the same time, assigned each agent an independent project directory and an independent port, and let everything run with no manual intervention. After they finished, I checked the results one by one.

![](https://pic.yupi.icu/1/image-20260728101254851.png)

My heart is racing, my hands are shaking—let’s begin~



## 7 Test Projects

The 7 projects I prepared this time go from simple front-end animation to complex full-stack products, progressing from easy to hard:

1. Interactive animated explainer website
2. 3D animated knowledge explainer
3. Turn copy into a web PPT
4. Web PPT generator tool (with built-in AI model)
5. Soccer battle web game (cross-model comparison)
6. The Binding of Isaac roguelike game
7. Full-stack AI coding tool (a Cursor clone)

Want to guess how much it cost to run all these tasks? I’ll reveal the answer at the end.



### 1. Interactive Animated Explainer Website

For the first project, I asked the model to build a website that explains knowledge through interactive animation. The topic was “attention residuals.”

In the prompt, I required it to first use Firecrawl to search the web for technical details, then open the finished result itself, take screenshots to verify the effect, and keep adjusting on its own until it was satisfied before delivering.

![](https://pic.yupi.icu/1/image-20260717111349321-20260717144613538-20260728104640628.png)

Let’s look at the final result. The interface feels very high-tech, and the background even has floating light-particle effects.

The whole site is also very clear and well-structured. Readers can learn the concept smoothly like following a tutorial, or use the chapter navigation on the left to quickly jump around and fill in gaps.

![](https://pic.yupi.icu/1/1785144666553-66077ab6-a75d-4730-84d7-963dc05f8a50.png)

In the first section, it introduces the problem with the metaphor of “a sticky note getting more and more scribbled over.” That analogy is vivid. You can drag a slider to increase the number of stacked layers and directly see how the first sentence contributes less and less to the final result until it becomes almost unreadable.

![](https://pic.yupi.icu/1/1785144739223-15eb9fb7-2cd2-440e-824c-3e44e9e10b37.png)

That said, there are still some flaws on the page, such as text getting covered in some areas. On this point, its front-end result is a bit worse than Kimi K3’s.

![](https://pic.yupi.icu/1/1785144789542-88677a5c-d92a-4a8d-8be9-cc13e3bce750.png)

But most of the animation effects and element positions are accurate, and the experience is far, far better than Opus 4.8 when it came to making animated websites.

![](https://pic.yupi.icu/1/1785144946281-9a41c9f8-f0ab-4b60-864e-28c26c6b65fb.png)

It even included a few quiz questions to test learning outcomes. If you choose the wrong answer, it tells you why. The attention to detail is excellent.

![](https://pic.yupi.icu/1/1785144892860-fed3bc03-d72a-4b79-aa9d-f904fec855d3.png)



### 2. 3D Animated Knowledge Explainer

Still using the same topic, this time I switched to a 3D scene for the presentation.

Besides web search, I also required it in the prompt to use Context7 to look up the latest documentation for the 3D library it used, so it wouldn’t code with outdated APIs.

![](https://pic.yupi.icu/1/image-20260717111408539-20260717144615047-20260728104641704.png)

Looking at the final product, I was amazed the moment I opened the page. The tech vibe is off the charts, and the animation is very smooth and lively.

![](https://pic.yupi.icu/1/1785145006075-8be31bfa-8f84-466c-ae7d-b58366524c51.png)

You can freely switch perspectives, zoom in and out, and even compare multiple different residual patterns side by side.

![](https://pic.yupi.icu/1/1785145067089-c8c05cfb-e1a3-4f3c-abe8-e3c30aa1390e.png)

Friends working in education are in luck—AI can turn boring knowledge points into vivid animations and present them clearly, helping students understand faster.

From a front-end perspective alone, I honestly can’t find any fault with it.



### 3. Turning Copy into a Web PPT

When I make video tutorials, I sometimes need to turn article content into presentation slides, but making PPTs by hand is too slow.

So this time I simply threw it a technical article and asked it to break the content into a full-screen web PPT following the article’s explanation order. Later, I can use it as presentation material for recording videos.

![](https://pic.yupi.icu/1/image-20260717111421384-20260717144616722-20260728104642024.png)

Let’s look at the cover first. This big title... why does Claude now also have that strong GPT flavor?

![](https://pic.yupi.icu/1/1785145163594-b863aa42-a51d-4440-988e-585ce57ef50e.png)

The overall PPT result is similar to other models. After all, I didn’t provide any image assets or other materials to the AI, so there are only so many layouts it could choose from.

![](https://pic.yupi.icu/1/1785145204715-e3eaf964-6677-426f-976c-7e3fb229e831.png)

Still, the tech vibe is strong enough, and it’s more than usable for many presentation scenarios. For example, if you’re working on a graduation project, you can just throw your project to AI and have your thesis defense PPT basically done.

![](https://pic.yupi.icu/1/1785145242391-0e506acc-4b23-4167-9d5c-e52a400cb7e8.png)



### 4. Web PPT Generator Tool

The first three were just appetizers. Now it’s time to test its full-stack engineering ability.

In the previous case, it generated a PPT from a given article. But can this capability be turned into a general-purpose tool?

The user pastes any piece of text, the back end calls a large model to break down the content, the front end renders it into a presentable web PPT, and it also needs to support switching color themes and exporting as a standalone HTML file.

Once the requirements were clear, the prompt itself was simple. Since this involved AI capability, I used the newly released Kimi K3 model as the model called by the back end. Note that the project code itself was still generated by Opus 5.

![](https://pic.yupi.icu/1/image-20260717111459584-20260717144618089-20260728104642413.png)

When I previously used Kimi K3 to generate a PPT tool, the final result was extremely minimal, with basically only a text input box and a button on the homepage.

![](https://pic.yupi.icu/1/1784182758933-6b75a1c9-f922-437b-8c85-0115cdea665e-20260717144619030-20260728104642459.png)

But Claude Opus 5 built something much more like a mature product. Just look at that row of color themes in the lower left: Aurora, Ivory, Dusk, Cyan Mist. The names are pretty literary, and each theme even comes with its own positioning description.

It also supports entering extra requirements for PPT generation. Note that I never mentioned this in the prompt—the AI added that extra touch on its own.

![](https://pic.yupi.icu/1/1785145527106-4c6d9e30-ba47-47c2-a8a6-d1c9e4cd0d48.png)

I casually used one of my earlier articles to generate a PPT, and I could see the generation progress in real time. The quality was high.

![](https://pic.yupi.icu/1/1785146087244-153c15ee-6ffe-4f7b-8c8d-8224fe272074.png)

Try switching the theme—the effect is pretty nice, right? You can also present it full screen directly or export it as HTML:

![](https://pic.yupi.icu/1/1785146169709-34ce614b-115b-4713-8a42-e165e9c1205e.png)

Overall, both the front-end details and back-end generation logic were done very well. One prompt, and out came a usable product.



### 5. Soccer Battle Web Game

If you often read my articles, you should know this project is an old friend.

When GPT-5.6 was released, I used the same prompt to have GPT-5.6 Sol, Claude Fable 5, and Grok 4.5 simultaneously develop a soccer game called “2066 World Cup Showdown” (you can read *GPT-5.6 Three-Model Comparison - Full-Stack Project Benchmark* in this tutorial’s Model Updates section). This time the prompt was exactly the same, so it’s perfect for comparison.

First, let’s look at the pre-match settings screen. The light green theme matches the soccer field nicely.

![](https://pic.yupi.icu/1/1785145627018-69826233-8f03-4610-8ab7-ae4a152bfa05.png)

Passing, shooting, and substitutions all work properly and feel very smooth. And did you notice the detail? There’s a red charge bar under player number 9, which gives players more room for control.

![](https://pic.yupi.icu/1/1785145802068-9d828079-9355-4afd-95d9-65d3d4e38cba.png)

The AI opponent is also very smart—not like the AI in other models’ versions that only knows how to defend. This time the computer can even coordinate plays. And as a human player, you’re not completely doomed either—you still have a real chance to beat it. The gameplay experience is very good.

Compare this with the earlier models. In the GPT-5.6 Sol version, the AI never attacked proactively. I played a full match on medium difficulty and could only end with a 0:0 draw.

![](https://pic.yupi.icu/1/1783647330206-bb64786d-95d9-41e5-9d53-4fb42ffdd9da-20260717144623818-20260728104642909.png)

In the Grok 4.5 version, the field rendering had serious flaws, and the substitution logic was clunky—it often switched me to the teammate farthest from the ball.

![](https://pic.yupi.icu/1/1783648020795-d1809bda-6c3c-4e36-babf-a3f6e9e494e1-20260717144623018-20260728104642942.png)

In the Claude Fable 5 version, the ball physics engine was a disaster. The ball often teleported, making the game basically unplayable.

![](https://pic.yupi.icu/1/1783648857986-4d1edca9-1496-494c-80b1-096690b34bc4-20260717144622560-20260728104642988.png)

Opus 5 not only made a breakthrough in AI-opponent intelligence, but also added a live match status panel on the left, which none of the previous models managed to do.

![](https://pic.yupi.icu/1/1785145881584-df6c0f0a-5868-4ebd-9d3a-fec99e57ba88.png)

The only small issue is that there’s a problem with the white field markings—the ends of the penalty arc in front of the box curve inward into the penalty area.



### 6. The Binding of Isaac Roguelike Game

Next comes a more challenging game project.

The Binding of Isaac was a roguelike game I loved playing as a kid. It includes randomly generated dungeons, shooting combat, an item system, various enemies, and Bosses.

Earlier, I had Kimi K3 develop this game. In the prompt, I required it to first use Firecrawl to search for information on The Binding of Isaac’s gameplay mechanics and art style, and to use Context7 to look up the documentation for the game framework it used:

![](https://pic.yupi.icu/1/1784212259593-16d5f314-9b40-4651-851b-c61dcf8d8c7c-20260717144625002-20260728104643132.png)

Back then, K3 produced something like this. The interface looked rough, but the core gameplay loop worked completely—you could shoot bullets and hit monsters:

![](https://pic.yupi.icu/1/1784190076766-03662fe2-7400-4938-87d1-422f3d992bd7-20260717144628318-20260728104643161.png)

Now let’s look at what Opus 5 built this time with the exact same prompt. Brace yourselves!

The moment I saw the game’s homepage, my DNA moved. Anyone who has played the game should be able to tell that the character looks pretty close to the original.

![](https://pic.yupi.icu/1/1785146456351-7ecb2861-e1b8-454e-9fd9-dc748b441262.png)

![Original game character](https://pic.yupi.icu/1/1785146563523-6fed4f0b-08d8-4c82-bf24-343a46a418d4.png)

I really didn’t expect it to turn out this well. Many of the little monsters are ones that actually exist in the original game.

![](https://pic.yupi.icu/1/1785146642381-79f6906f-4e68-4427-b72e-0aa3115e8233.png)

The character stats are clear, the items are varied, and you could say it really captures the essence of *The Binding of Isaac*.

I even got sucked into playing it, which delayed this article’s publication by 20 minutes.

![](https://pic.yupi.icu/1/1785146850442-e539fdbd-b359-4769-a65c-22b4638885c7.png)

The Boss mechanics are also strikingly similar to those in the original game.

![](https://pic.yupi.icu/1/1785146825259-76b4c935-67a7-46e3-9ede-3d0659eed806.png)

This completely exceeded my expectations. Later, I continued iterating on this project and expanded it into a full game with 12 dungeon floors, 13 Bosses, and 55 items, then open-sourced and published it. If you’re interested, you can read *Cursor + Claude Opus 5 - The Binding of Isaac Roguelike Project Case Study* in the “AI Creative Applications” category under the Project Practice section of this tutorial.



### 7. Full-Stack AI Coding Tool

For the last project, I cranked the difficulty all the way up.

I asked AI to build a web AI coding tool similar to Cursor based on the open-source code of VS Code. It needed to support both Editor Window code editing mode and Agents Window conversation workspace mode, and allow free switching between the two.

Take a look at the result. It almost fully preserves the essence of VS Code, including code highlighting, the code minimap, management panels, code search, and more.

![](https://pic.yupi.icu/1/1785147124049-912c793e-0915-4843-853b-9848a4611536.png)

I asked the AI to execute a task, and you can clearly see its reasoning information, tool calls, and so on.

![](https://pic.yupi.icu/1/1785147250942-846cdd2b-a6be-4848-b412-dc1d9e31e0b0.png)

The AI can even call the terminal, autonomously test the code it develops, and clearly show which files were changed this time.

![](https://pic.yupi.icu/1/1785147362813-894c3d8b-cb1b-48cf-96ca-9eefd572b4c3.png)

Can you believe I built my own Cursor after talking to AI just once?



## Final Thoughts

All 7 projects are done, so let me share my real impressions.

The thing that impressed me most is that Claude didn’t complete tasks in a fully mechanical, simplest-possible, straight-line way—where you tell it to do something and it does only that. Instead, it tends to add a bit of its own thinking on top of your requirements and tries its best to achieve the ideal effect.

Its back-end logic is strong, its front-end visual effect is strong, and it also pays a lot of attention to detail. It really is an all-round warrior. **At least for me, I honestly can’t think of any development task AI absolutely can’t do right now.** If there is one, it’s probably because I didn’t guide the AI well enough, or because I didn’t have enough tokens.

Another thing that impressed me is that Opus 5 really does love checking its own work, just like Anthropic said. Anthropic even specifically reminded developers to remove the sentence “remember to verify at the end” from prompts—the more you tell it to check, the more likely it is to become obsessed with checking. Later, they simply deleted over 80% of Claude Code’s system prompt, and its coding benchmark scores didn’t drop at all. If you want to know the specific method behind this prompt-reduction approach, you can read *Anthropic’s Official Prompt Simplification Method* in the Tips and Tricks section of this tutorial.

Of course, this characteristic is a double-edged sword. Opus 5 can easily make simple tasks more complicated than they need to be. That has always been Claude’s chronic issue, and it burns more tokens too.

So if you want to make better use of a model at Opus 5’s level, you still need to put some effort into your prompts. That doesn’t mean writing something bloated and overly long—**it means describing the requirements clearly and defining the AI’s boundaries well**. Otherwise, there’s a good chance it will go off track.

And now for the final reveal: bundled together, these 7 tasks cost me a total of more than 900 RMB.

That’s the price you pay for correspondingly strong results. When I previously used domestic models like Kimi K3 on the same projects, I only used up a tiny percentage of my package quota.

So you still need to choose models based on your actual needs:

- If you want 90-point results, assign the task to Opus 5
- If 80 points is enough, use GPT, Kimi K3, GLM-5, or similar models—they’re fast, stable, and cheap
- If just passing is enough, then use the extremely cost-effective DeepSeek

There’s no absolute best or worst model—only what’s suitable or unsuitable. Try more models and tools yourself, and use real projects to feel the differences in their capabilities. You’ll definitely find the programming partner that suits you best.
