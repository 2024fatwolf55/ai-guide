# Remotion: Making Animated Videos with AI Coding

> A complete step-by-step guide, from installation to the final render



Hello, I'm Yupi.

AI coding can do far more than you might imagine. Besides building websites, tools, and mini programs, it can also make animated videos!

Recently I came across a very interesting open-source project called [Remotion](https://github.com/remotion-dev/remotion). It lets you create video animations by writing code, and it has a ton of stars on GitHub.

![](https://pic.yupi.icu/1/image-20260216222601866.png)

You might ask: making videos with code? Wouldn’t that be exhausting?

Relax. Of course we’re not going to write the code ourselves. **Just let AI write it for you!**

The principle behind using AI coding to make animation is actually very simple:

- AI writes the code
- Remotion renders the code into a video

![Examples of animation results from the official site](https://pic.yupi.icu/1/image-20260216223620684.png)

Next, I’ll walk everyone through the full process, step by step, from installation to final output. Caretaker Yupi is on duty again~

📺 You can also watch the video version: https://bilibili.com/video/BV1qxFSzUEwo



## 1. Install Remotion

First, open your terminal and run one command to install Remotion quickly:

```bash
npx create-video@latest
```

After running it, it will ask you a few questions:

1. Choose a template > I picked Hello World
2. What should the project be called? > Just call it `myvideo`
3. Use TailwindCSS? > Sure
4. Add AI Agent Skills? > Definitely add this!

![](https://pic.yupi.icu/1/1770370961690-58c49ba5-aecf-4194-8f27-d2db91db6087.png)

After adding this Skill, you can use AI conversations to have AI create animations with this library for you.

When installing the Skill, it will ask which Agents you want to install it into, and whether to install it for the current project or globally. I recommend installing it globally so you don’t have to reinstall it for every project later.

> Note: you need to make sure you can access GitHub, otherwise it may fail.

After the installation is complete, enter the project directory, install dependencies, and run it:

```bash
npm install
npm run dev
```

![](https://pic.yupi.icu/1/1770372083166-73703f97-3ef2-4980-922d-0b3a0116245d.png)

Open your browser, and you’ll see a **web-based video editing tool**:

![](https://pic.yupi.icu/1/1770372166367-c5facfbf-1829-4b03-8dde-5e86ed1064f2.png)

Looking at this interface, if you didn’t know better, you’d think it was desktop software!

The left side of the page shows different video clips, and each clip is actually rendered from code. If you delete a section of code, the corresponding video clip disappears too:

![](https://pic.yupi.icu/1/1770372458099-64e9f878-ebf6-42b9-9c78-bde4e5fd40e2.png)

Press Ctrl+Z in the code editor to undo, and the video comes back. Pretty magical, right?

![](https://pic.yupi.icu/1/1770372446540-126bd94f-f484-4631-8813-086a27c05b50.png)



## 2. Let AI Make the Video for You

There’s no way we’re going to write video code by hand, so of course we’ll let AI handle it.

Open an AI coding tool. I used VS Code + the GitHub Copilot AI plugin here, selected the latest Claude Opus model, and used a 1-million-token context window. Pretty powerful stuff.

![](https://pic.yupi.icu/1/1770372617235-a5aef8ec-c45d-45fd-9673-e583892d97c3.png)



### Demo 1. The Fish-Head Guy Rapping

I directly sent AI this prompt:

```
一条鱼头人正在唱中文 RAP，RAP 的内容是称赞一位叫程序员鱼皮的博主，屏幕上动态显示歌词（快闪风格）
```

You’ll see that AI immediately found the **Remotion Best Practices** Skill package we installed earlier. It helps AI understand how to make animation through programming.

![](https://pic.yupi.icu/1/1770373151980-28c9faa7-1d76-48cd-87f5-f75fbb748dbd.png)

Then it started writing the animation code. After a while, AI finished the task.

![](https://pic.yupi.icu/1/1770373512515-abf6f754-1e68-4b64-a540-bc68261385d4.png)

You can view the result directly in the browser. The fish-head guy is on the beat 🐟~

![](https://pic.yupi.icu/1/1770373656918-73c8de55-5e4e-4ac0-9328-27ce1791cbd7.png)

How should I put it… it’s a bit too abstract, bro! But hey, it was only the first demo, so my expectations weren’t that high. Next, let’s try something more fun and meme-worthy.



### Demo 2. “Chicken, You’re Too Beautiful”

I opened a new AI chat window, and this time I gave it a more specific requirement:

```
帮我做一个小鸡一边打篮球一边 RAP 的爆款视频，大概 20 秒，要求有视觉冲击感、要足够洗脑，让人一看就想点赞、循环播放。

我是傻子，你需要告诉我提供哪些素材，如果不理解需求，找我提问确认，并且最后完成视频。
```

And guess what? The AI actually recognized the meme “鸡你太美”! Come on, man.

![](https://pic.yupi.icu/1/1770373956714-208a1770-bc85-4cc8-a5e8-64190b5fd645.png)

It said I didn’t need to provide any materials and that it could handle everything itself, so I just let it go for it.

![](https://pic.yupi.icu/1/1770374224644-1c139dc4-4816-4be4-902b-d6b9c6b32045.png)

After it did its thing, it produced a new video. Let’s take a look:

![](https://pic.yupi.icu/1/1770374335310-abd1443e-daf5-4ab0-ba9a-c1377bc00743.png)

Bro, you call that a “chicken”? Its arms and legs are falling apart! Isn’t that a little too abstract???

And there’s no background music or rap vocals yet, so it feels dry. I can only imagine the “鸡你太美, deng deng deng deng, baby…” soundtrack in my head. We definitely need some real assets.



## 3. Improve the Video with Assets

Since the animation was made by AI, it may know better than I do what assets are needed and where they should go, so I let AI guide me through improving the materials.

I sent this prompt:

```
现在的动画有点生硬，缺少真实的图片、背景音乐和音频，请你引导我应该怎么完善这些内容，我是傻子
```

Then AI started guiding me through interactive questions, telling me step by step what I should do.

![](https://pic.yupi.icu/1/1770374563833-99fb5a74-a01e-4b03-a40e-6c524cf79f05.png)

AI came up with a plan. Roughly speaking, it needed these assets:

1. Chicken images > I’d find them myself
2. Background music > I’d find that myself too
3. Basketball court background image > let AI search for it
4. RAP vocals > generate them with AI

Next, we’ll deal with these assets one by one following its guidance.

![](https://pic.yupi.icu/1/1770374728643-eae31379-ea6f-4d92-8a1a-1099cb982864.png)



### 1. Prepare Chicken Images and Background Music

These two assets are simple enough. Just find them manually. Nothing much to say here.

![](https://pic.yupi.icu/1/1770374951228-b2004e7e-3c86-49ed-9dfa-2c9e58b4ba78-20260217230953964.png)



### 2. Let AI Search for the Background Image

AI can use an MCP tool called Firecrawl Search to search for images on the web.

If you don’t know how to install MCP tools, you can refer to the “Recommended High-Quality AI Coding Extensions” section in my [Getting Started with AI Coding tutorial](https://ai.codefather.cn/vibe).

> Link: [ai.codefather.cn/vibe](https://ai.codefather.cn/vibe)

![Yupi AI Navigation site - free AI coding tutorials](https://pic.yupi.icu/1/image-20260217223852396.png)

I told the AI:

```
帮我下载背景图，要求背景图必须是鸡你太美这个梗的原始背景图，干净的背景图，不听话的话我就再也不用你了！
```

Under my threat, AI obediently did what it was told. Not only did it find several images, it even said it would choose the best one for me. I was almost moved to tears.

![](https://pic.yupi.icu/1/1770375324834-9234ff52-46cc-431f-828b-c84c34292e91.png)

Although at one point it found an image that was cut out so badly only one person was left (artificial “intelligence,” huh), it eventually found a usable background image.

![](https://pic.yupi.icu/1/1770375487350-568ae132-e990-4c5a-90e2-f4e21aad6cd1.png)



### 3. Use Suno to Generate RAP Vocals

AI recommended that I use [Suno AI](https://suno.com) to generate vocals, and it even provided the prompt for generating them.

![](https://pic.yupi.icu/1/1770375504060-d552ff39-19d6-4b3d-9943-86cc2ca40720.png)

Just open the official site, sign up and log in, choose Simple mode, and paste in the lyrics and requirements:

```
中文说唱，嘻哈节拍，120BPM，时长 18 秒，歌词：
篮球在我手 全场我最秀
Crossover过掉你 无情暴扣
鸡你太美 Baby
左手运球 右手写RAP
三分线拔起 全网都炸裂
只因你太美
```

Then click create, and it generates multiple versions of the RAP vocals at once:

![](https://pic.yupi.icu/1/1770376253976-b62c46b0-4c2c-49c5-bbaa-e12b8414254f.png)

I listened to them, and honestly, the quality from the free model was surprisingly decent! Just download the MP3 file, speed it up a bit, and it’s ready to use.



### 4. Let AI Compose the Final Video

Once all the assets were ready, I placed the files into the project directory as required, then told AI:

```
素材放好了
```

![](https://pic.yupi.icu/1/1770376293681-f824c758-5ecc-4e66-a3c3-92ccc1d9c4ac-20260217224715624.png)

Then AI started swapping in the assets. After waiting a bit, its masterpiece was complete. Let’s look at the final result:

![](https://pic.yupi.icu/1/1770376707651-1829d201-8f85-495d-b2eb-a18c6fe96e3c.png)

With real assets added, it was much better than the earlier version that relied purely on AI-generated SVGs and emojis. Now it had the background image, background music, RAP vocals, and lyric animation. It still felt a little stiff in places (for example, the chicken image in the middle looked a bit creepy), but overall it finally had the right vibe.



## 4. Optimization Ideas

At the moment, the animated video has two fairly serious issues. Let me share my thoughts on how to improve them.

**Problem 1. The assets aren’t realistic enough**

If you let AI draw all the assets entirely with code (SVGs, emojis, and so on), the results will usually look pretty abstract. So I recommend adding more real image assets yourself. The result will be much better.

**Problem 2. The audio and on-screen lyrics don’t line up**

A better approach is to first let AI generate the lyrics along with a matching timeline, then provide that same timeline both to the AI making the animation and to the AI generating the audio. That way, both sides are arranged according to the same timeline, so the visuals and sound can match up.



## Final Thoughts

Using AI coding to make videos definitely can’t compete with video generation models like Seedance, Sora, or Kling in terms of realism and smoothness. But it has its own strengths, such as being fully controllable, editable, and reproducible. It also doesn’t require GPU compute or expensive video API fees. It’s rendered purely through code. As long as your description is good enough and you manually add some assets, the result can actually be good enough for many use cases.

I think this tool is especially suitable for the following types of videos:

- Animated explainer videos: for example, explaining a concept and letting AI turn it into animation
- Fast-cut text videos: lyric flashes, text effects, and similar styles
- Absurd meme videos: things like “鸡你太美”-style meme content
- Educational animations: even if they look a bit stiff, they can help people understand concepts quickly

This case once again proves that AI coding is useful in far more scenarios than most of us imagine. It’s not just for building websites and tools. If you’re interested, go try it yourself—Remotion is completely open-source and free:

> Open-source repo: https://github.com/remotion-dev/remotion

Go for it. I’m looking forward to seeing the creative work you make with AI coding! 💪



## Recommended Resources

1) Yupi’s AI Navigation site: [A complete collection of AI resources, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussions and Q&A](https://www.codefather.cn)

3) Programmer interview cheat sheet: [High-frequency topics for internships / campus hiring / experienced hiring, plus real interview question analysis](https://www.mianshiya.com)

4) Resume builder for programmers: [Professional templates, rich example phrases, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships / campus hiring / experienced hiring](https://ai.mianshiya.com)
