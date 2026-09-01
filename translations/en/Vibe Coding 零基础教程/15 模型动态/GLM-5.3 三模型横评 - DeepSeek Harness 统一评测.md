# GLM-5.3 Three-Model Comparison - Unified Evaluation with DeepSeek Harness

> Use DeepSeek Harness as a unified toolchain environment to fairly compare the coding ability of GLM-5.3, DeepSeek V4 Pro, and Kimi K3.

Hello everyone, I’m Yupi.

The AI world has really been celebrating lately. DeepSeek V4 Pro official release and DeepSeek Harness came out together, and then Zhipu followed up with the brand-new GLM-5.3 model.

![](https://pic.yupi.icu/1/image-20260817145539750.png)

I heard that GLM-5.3 uses exactly the same base model as GLM-5.2—still 743B parameters—and improved performance by 50% purely through post-training.

**There’s no way I can finish testing all of these...**

Since GLM, DeepSeek, and Kimi are all fighting so fiercely among domestic models right now, why not put them in the same ring and let them battle it out?

I’m sure you all want to see that too, right~

![](https://pic.yupi.icu/1/Gemini_Generated_Image_t1h6xtt1h6xtt1h6.jpg)

And since the recently popular DeepSeek Harness (DSH) supports third-party models, I decided to use DSH as a unified evaluation tool and test the latest models from all three vendors in an identical toolchain environment. The only difference would be the model itself, making the comparison as fair as possible.

![DeepSeek Harness tool](https://pic.yupi.icu/1/image-20260814133452050.png)



## Connecting Models to DeepSeek Harness

The first step is connecting GLM-5.3 and Kimi K3 to DeepSeek Harness. I’ll use GLM-5.3 as the example here.

If you haven’t installed or used DeepSeek Harness before, you can read *A Complete Beginner’s Guide to DeepSeek Harness* in the “DeepSeek Harness” directory under the Coding Tools section of this tutorial. It only takes a few minutes from installation to getting started.

> Video tutorial: https://www.bilibili.com/video/BV1VkgK6NEZS

Here I’ll only explain how to connect third-party models to an existing DeepSeek Harness setup.

1) Open the DSH web interface and click the **Settings** button in the lower left.

![](https://pic.yupi.icu/1/1786932507970-41599bc0-493b-43be-b23a-06167310714e.png)

2) Go to the **Models** tab and click **Add Provider**.

![](https://pic.yupi.icu/1/1786932573401-dc4b2cba-6e89-490e-986e-45b62c49258a.png)

3) Choose `zai-coding-cn` as the model provider, then go to the [Zhipu Open Platform](https://bigmodel.cn/coding-plan/personal/overview) and get your API Key to fill in.

![](https://pic.yupi.icu/1/1786932690701-74c2d894-8922-40f3-ac8d-43b0cb3d3b07.png)

4) Expand the custom settings and click **Fetch Available Models**. But because GLM-5.3 is so new, it won’t be pulled automatically by default.

So you need to manually click **Add Model**, enter `glm-5.3`, and save it.

![](https://pic.yupi.icu/1/1786933645912-f2d165ea-cef1-41d1-b34f-9e244e85c6cb.png)

Done! Now you can select and use the GLM-5.3 model directly in the chat box~

![](https://pic.yupi.icu/1/1786933520324-c3de8492-bfb7-4b9e-bd5a-47af4ac36add.png)

Use the same method to add Kimi K3. DeepSeek V4 Pro is connected by default once DSH is installed successfully, so it doesn’t need extra configuration.

With all three models in place, let the showdown begin.



## Test Notes

To keep the comparison fair, all three models were run in DeepSeek Harness standard mode, using each model’s default reasoning tier, with the exact same toolchain and the exact same prompt. And I made no manual intervention at any point—once I gave the prompt, I let the AI run all the way through on its own.

DSH automatically scans the skills directory installed on my machine. For example, I have Firecrawl web search skills and Context7 documentation lookup skills installed, so all three models could use them while running tasks.

![](https://pic.yupi.icu/1/image-20260817151814146.png)



## Case Study 1. A 3D Parkour Game Inspired by *Niu Lai*

Recently there was a Chinese animated movie called *Niu Lai*. Because its modeling was extremely rough and its plot bizarre to the point of abstraction, it went viral on social media in reverse.

Its box office on opening day was only 3,420 RMB, but because people kept going out of curiosity, it shot past 9 million in just a little over ten days.

As Banfo Teacher put it:

- If you spend more than an hour learning about this movie, you’ve wasted an hour of your life.
- But if you paid 30 RMB to actually watch *Niu Lai*, that proves you really do have 30 RMB.

![](https://pic.yupi.icu/1/%25E7%2589%259B%25E6%259D%25A5%25E5%259B%25BE%25E7%2589%2587.jpg)

I decided to have the 3 models pay tribute to this movie by making a **3D web parkour game**.

In the prompt, I deliberately avoided too many functional constraints or technical restrictions. I wanted to see how far the models could go on their own and whether they could recreate elements from the movie. One thing worth noting is that I required the AI to use a Loop Engineering workflow: finish one step, verify one step, and fix problems by itself when they appear.

![](https://pic.yupi.icu/1/1786934842850-22be3935-b9b6-43ad-8a7f-16c163795b57-20260817183037814.png)

OK, let’s run!



### GLM-5.3 Final Result

Let’s start with GLM-5.3’s result.

On the main screen, you can see a short story description.

Has anyone here actually seen *Niu Lai*? This description matches the movie’s plot surprisingly well: the little calf Niu Lai, following the skylark, falls into a great dream, passes through mist, wolf packs, and a roaring logging yard, and only by running forward can he learn courage... honestly, it’s kind of inspiring.

![](https://pic.yupi.icu/1/1786941444587-f86f52c2-2cbc-48c7-a543-2dfefb190781.png)

Entering the first level, “Dawn Prairie”—I have to say, this cow model really is abstract, especially with the cow’s face staring straight at you...

And there’s even a skylark companion running alongside the calf, which does somewhat capture the movie’s flavor.

![](https://pic.yupi.icu/1/1786941685678-78fab2ee-5643-4d9d-aa62-19bbde4742d4.png)

The controls support moving left and right, jumping, and sliding. The feel is pretty smooth, and it’s actually quite playable.

![](https://pic.yupi.icu/1/1786941720452-1e3d231b-975d-4682-b613-32d40bdd4531.png)

After collecting enough lucky grass, you can trigger a special move and enter the “Bao La Rush” state: full-screen acceleration plus invincibility.

To explain: Bao La is Niu Lai’s good friend in the movie, so the name of this special move is actually pretty funny.

![](https://pic.yupi.icu/1/1786941781966-0fbbe03c-8818-4c9e-afbf-7e0b64374624.png)

The game has several levels, and each one has a different theme and mechanics. For example, in the “Wolf Pack Night Raid” level, there really are wolves chasing you from behind, and there’s even a story-fitting skill called “Mother’s Protection.” That one really hit me.

![](https://pic.yupi.icu/1/1786942149069-541e5b46-b1e2-4f9e-99af-a8f765149284.png)

Unfortunately, my little calf fell in the fourth level.

And when I looked at the death screen, I completely lost it. Why is there even a burst of blood spraying out?

![](https://pic.yupi.icu/1/1786942206513-b212f83e-7e25-4c03-b008-b527f827d264.png)

Details. Real details...



### DeepSeek V4 Pro Final Result

Now let’s look at DeepSeek V4 Pro’s version.

The main screen actually looks decent enough, and it also recreates the story background of the skylark and Niu Lai.

![](https://pic.yupi.icu/1/1786942470229-08dcb397-2b7f-458b-9f9c-2f32e476ec99.png)

Enter the game.

Uh... how do I put this?

The interface is really clean to an absurd degree!

That said, it did include the skylark and the friend Bao La, who run alongside the calf.

![](https://pic.yupi.icu/1/1786942537635-7e98120c-5761-42cf-be5e-a7ea370fa4e4.png)

Movement, jumping, and sliding all work properly—but I absolutely lost it when I saw the sliding effect... Good grief, did that just shovel my eyeballs out?

![](https://pic.yupi.icu/1/1786942708594-261a7ca0-de4c-4cfe-9fa6-77a1b3b1b8bb.png)

If you look closely, the icons on both sides of the road are clearly floating above the grass. Also, the game pace is too slow: it takes forever before the first obstacle appears, and there are basically no skills or special level mechanics, so the gameplay is pretty weak.

![](https://pic.yupi.icu/1/1786942635722-bb121640-3419-4c5d-b542-3262a5059232.png)

The calf only has one life, so after hitting a rock it goes straight to the death settlement screen:

![](https://pic.yupi.icu/1/1786942990402-af6dc75b-652b-497c-b474-a2eff1526e3c.png)

Overall, I’d say it’s decent but unremarkable.



### Kimi K3 Final Result

Finally, let’s look at Kimi K3’s version.

The color scheme on the main screen is pretty plain, and like the other models, it also summarizes the movie’s plot.

![](https://pic.yupi.icu/1/1786943144669-112d3b61-a136-46aa-813b-d1b58050254c.png)

Enter the game. The interface style is okay, and the distant mountains are drawn quite nicely. But the main character, the calf, is pretty ordinary—not abstract enough. It just looks like a group of normal blocks.

![](https://pic.yupi.icu/1/1786943246265-ed550bfe-c9b2-4298-9a29-24daf04894fa.png)

Although the calf has 3 lives and can collect coins, there aren’t any real skills or special mechanics. The whole game is basically just run, run, run.

Where is my leopard friend? Where is the skylark?

And this rain effect—a full-screen grid? That feels a bit lazy...

![](https://pic.yupi.icu/1/1786943334061-a01c90c7-5038-4c26-b4e8-60036ebadf20.png)

The most fatal issue is that the whole game stutters noticeably from time to time. The frame rate just isn’t stable enough.

![](https://pic.yupi.icu/1/1786943521676-4e775bcf-850c-4d1d-88f9-aa3ba08cbff8.png)

And finally, the end screen is also pretty plain. Nothing special.

![](https://pic.yupi.icu/1/1786943584423-9095cd16-3916-445b-b6d7-ee30bb4c1f6d.png)



### Case Study 1 Comparison

All three versions are done, and the winner should already be obvious.

GLM-5.3’s version has the highest completion level: multiple levels, multiple skills, strong faithfulness to the story, and far stronger gameplay than the other two.

DeepSeek V4 Pro implemented the basic gameplay, but the pacing is slow and the details are rough.

Kimi K3’s scene visuals are decent, but the mechanics are too simple and there are stuttering problems.

Overall:

- Front-end effect: GLM ≈ Kimi > DeepSeek
- Playability: GLM > DeepSeek > Kimi
- Degree of abstraction in the visuals: GLM > DeepSeek > Kimi

In terms of overall game completion, GLM 5.3 is far ahead.



## Case Study 2. AI Diagramming Tool

The previous task was a front-end game, so of course the second task had to switch directions and test full-stack engineering ability.

I asked the 3 models to build an **AI diagramming tool**. The user enters natural-language requirements, the back end calls a large model to generate a diagram in draw.io format, and the front end embeds the open-source draw.io editor so users can directly edit and modify the generated diagram online.

This task simultaneously tests understanding of draw.io’s open-source code, back-end AI invocation workflow design, front-end integration of complex components, and the overall rationality of product design.

To make testing easier, I directly provided the API Key in the prompt so the AI wouldn’t need a manual environment-variable setup step.

![](https://pic.yupi.icu/1/1786935817947-28512ebd-63a7-45bf-9282-89bb4807bfbf.png)



### GLM-5.3 Final Result

Let’s first look at GLM-5.3’s result.

The whole page feels very high-tech. The left side is the AI chat box, and the right side is the canvas editor.

The product onboarding is also well done: it tells you that you can draw professional diagrams with a single sentence, and it even provides several example types.

![](https://pic.yupi.icu/1/1786947000691-52c43b54-e03d-41bc-a419-2f9e0b150548.png)

I asked the AI to draw the architecture diagram of DeepSeek Harness. You can see its deep thinking process and XML generation in real time, while a flashy loading animation appears on the right.

![](https://pic.yupi.icu/1/1786946651555-aa4f9a37-59c0-4f66-b691-dfae0ba85280.png)

Once generation was finished, the right side immediately rendered a complete architecture diagram. The layers were clear, and it preserved draw.io’s native element-editing capability, so you could directly drag and edit elements.

![](https://pic.yupi.icu/1/1786946757859-0ff24615-3e22-4fe9-8ebb-0d3a35f74d72.png)

Even stronger: it supports continuous conversational editing. For example, if I say “change DeepSeek Harness Core here to red,” the AI can accurately locate the corresponding element, modify the style, and update the canvas in real time.

![](https://pic.yupi.icu/1/1786946921119-ae9fcde6-f3bb-4da2-8244-70652b4a71c7.png)

Overall, the result is excellent, and the image export feature also works properly.

And you’ll notice that GLM-5.3 deeply integrated draw.io’s editing capability into its own interface design, making it feel like a complete product rather than a clumsy third-party embed.



### DeepSeek V4 Pro Final Result

Now let’s look at DeepSeek V4 Pro’s performance.

When I opened the interface, the right-hand canvas was just a blank area with a huge Loading icon?

And the helper text in the lower left was overflowing too. This really shows that DeepSeek V4 Pro’s front-end work is weak.

![](https://pic.yupi.icu/1/1786947686035-f5dce2a4-5bc2-49b5-a4aa-ac592a06a214.png)

The AI chart-generation function itself works properly, but it has no capability to show the AI’s thinking process in real time. You have to wait until generation is completely finished before you see the result.

![](https://pic.yupi.icu/1/1786947674690-a291172a-4f39-4db1-8e0f-4d6f867da64e.png)

Most importantly, DeepSeek V4 Pro very obviously just embedded the entire draw.io editor directly into the front-end page without doing any deep integration. It feels stiff and unnatural, with a clear gap compared with GLM’s more organic integration of draw.io into its own interface.



### Kimi K3 Final Result

Finally, let’s look at Kimi K3.

This time, Kimi K3 generated an interface layout similar to GLM’s, and it also integrated draw.io naturally into the project. The overall interface style is very nice.

But draw.io’s original icons and menu bar were still preserved intact, so its integration is slightly weaker than GLM’s.

![](https://pic.yupi.icu/1/1786947935320-b6974f42-7680-490d-9c86-c938007a0c42.png)

The AI chart-generation function works normally and also supports continuous conversational editing.

![](https://pic.yupi.icu/1/1786948128170-e63bfe84-3e37-48be-ad72-2c16099debce.png)

However, its back-end logic clearly didn’t do a good enough job constraining prompts and validating tool output. Sometimes the AI’s generated result breaks and pastes raw XML code onto the interface instead of rendering it as a diagram.

![](https://pic.yupi.icu/1/1786948418039-419ad351-70b1-4e5a-9e14-0378b904a7b9.png)

Overall, Kimi K3’s front-end design ability is on par with GLM-5.3, but its back-end stability is noticeably worse.



### Case Study 2 Comparison

On this task, GLM-5.3 delivered the best overall performance. Interface design, real-time display of AI deep thinking, continuous conversational editing, and deep draw.io integration—it got every link right.

Kimi K3 has very strong front-end design ability, but its back end occasionally breaks.

DeepSeek V4 Pro also implemented the core functionality successfully, but its interface is rough and its integration is stiff, making it the weakest performer.



## My Take

Both projects are done, so let me talk about my real impressions.

Clearly, even inside DeepSeek Harness—DeepSeek’s own “signature weapon” environment—GLM-5.3 still performed very well.

The two tasks I picked covered two completely different directions: a pure front-end 3D game and a full-stack AI application. From that, you can see GLM-5.3 is clearly ahead in task understanding, code generation quality, and product design awareness.

Now let’s talk about the cost question everyone cares about. Guess how much money I spent?

Since I used the coding package for GLM-5.3, it’s hard to directly calculate the exact monetary spend, so I can only count by points.

The two projects consumed a total of 1,151 points. Since I subscribed to the Pro package (538 RMB/month), which gives 60,000 points per week, this test used less than 2% of the weekly quota. Converted into money, it’s not even 3 RMB.

![](https://pic.yupi.icu/1/image-20260817154109537.png)

My Kimi K3 package had expired and I couldn’t get a new one, so I connected it directly using an API Key, which cost a total of 31.07 RMB. DeepSeek V4 Pro, after the price increase, cost 13.99 RMB.

Based purely on my actual spending, GLM-5.3 is the most cost-effective when calculated through the package plan. With 60,000 points per week, you can run as much as you want, and judging from the types of tasks in this test, building dozens of small projects wouldn’t be a problem.

And GLM-5.3 will open-source its weights two weeks after release.

**In the open-source world, GLM-5.3 can currently be called the ceiling of coding ability.**

![](https://pic.yupi.icu/1/%25E6%25BB%2591%25E5%258A%25A8%25E5%258F%2598%25E5%2594%2590%25E5%2599%25A8%25E4%25B8%25AD.jpeg)

Zhipu also mentioned in its release article that when Hugging Face previously suffered a security attack, Anthropic’s Mythos model was only available to around 150 large institutions. At the moment when help was most needed, many smaller companies and open-source projects couldn’t actually access the strongest defense tool.

When offensive capability is spreading, defensive capability can’t remain in the hands of only a few. GLM-5.3 being open-source gives everyone a shield for defense, and that significance may be even more important than benchmark scores.



## Final Thoughts

This comparison gave me more confidence in the coding ability of domestic models. GLM-5.3, Kimi K3, and DeepSeek V4 Pro are fighting fiercely, and that’s a good thing for us users—at least it means we have more choices.

But models are evolving too quickly. Today’s number one may be surpassed by a new model next week. Instead of agonizing over which model to choose, it’s better to test them hands-on and find the one that best matches your own scenario.

If you want to learn more real-world comparisons of AI coding models, you can read the other articles in this tutorial’s Model Updates section, or read *AI Model Selection Guide* in the Coding Tools section.
