# AI Creative Application - Distilling Yourself into a Skill Project

This project is an interesting AI creative application: “distilling” your own knowledge, experience, and thinking style into an AI Skill package, so AI can think and answer questions in your style. The whole process requires no coding at all—if you can use your hands, you can do it.

This article does not involve a complex development process. I’m simply sharing a typical AI creative application case to help broaden your thinking.

Project code is free and open-source: https://github.com/liyupi/yupi-skill



---



Hello everyone, I’m Yupi.

Recently, a wave of “distillation” has taken off on GitHub.

Not distilled liquor—distilled people.

`colleague.skill`, `ex.skill`, `nuwa.skill`, `boss.skill`, `myself.skill`... all kinds of weird distillation projects keep popping up, with people “packaging” those around them into AI Skill packs.

![](https://pic.yupi.icu/1/image-20260409163428725.png)

Some people distill former coworkers so AI can keep doing their jobs; some distill their exes so they can chat with an AI version of them and reminisce; there’s even a “anti-distillation.skill” made specifically to stop yourself from being distilled.

Good grief—cyber crossfire?!

I’ve been surviving on the internet for 6 years, written thousands of articles, recorded hundreds of videos, answered countless student questions, and accumulated quite a lot of material and language data. Seeing this trend, I started wondering: would someone distill *me* into a Skill too?

No way. Rather than waiting for others to distill me, I’d better do it myself!

So I decided to distill myself and see what my digital clone would look like.

After a whole round of operations, my “Yupi.Skill” was open-sourced:

> Open-source link: https://github.com/liyupi/yupi-skill

![](https://pic.yupi.icu/1/image-20260409175224601.png)

Next I’ll show you step by step how I distilled myself into a Skill. You can follow the same process to distill yourself or the people around you (legally, please). The whole process requires no coding at all—if you can use your hands, you can do it.

> Simply put, Skills are AI “skill packs.” A Skill is a directory containing a `SKILL.md` file that defines how AI should behave in a specific scenario through Markdown instructions. Once installed, AI can think and answer questions according to the rules in that Skill pack. Mainstream AI coding tools like Claude Code, Cursor, and Codex all support this now.



## Preparation

First, create a new `yupi-skill` directory and open it with your AI coding tool. All of our distillation work will happen inside this directory.

It’s best to use the strongest model you have, ideally with a longer context window, because the distillation result will be better. I used Claude Opus here.

![](https://pic.yupi.icu/1/image-20260409142017010.png)



## Step 1: Collect Raw Materials

AI doesn’t know you. It needs “raw materials” to extract your thinking style, expression habits, and professional judgment.

This step is the foundation of the entire process. The more real and richer your materials are, the more the distilled “you” will actually resemble you.

You can provide these kinds of materials:

| Material Type | Example | What It Can Distill |
|---------|------|-------------|
| Self-introduction / resume | My name is XXX, I’ve worked in XXX for X years, my MBTI is ISTJ... | Your identity positioning and personality traits |
| Personal experiences | Key stories from school, work, and career switching | Your values and growth path |
| Chat records | Exported conversations from WeChat / Feishu / DingTalk | Your real speaking style and catchphrases |
| Work documents | Weekly reports, technical plans, code review comments | Your professional judgment and working style |
| Creative content | Blogs, video scripts, posts, social media | Your viewpoints and expression style |
| Other people’s evaluations of you | Coworker feedback, friends’ comments | Your blind spots (traits you can’t see yourself) |

Using myself as an example, the materials I threw in included my resume and self-introduction, viral articles I had written (to distill my content style), personal-experience documents, work documents, and chats with students.

Just dump these files into the project’s `references/` folder. Any format is fine—articles, screenshots, PDFs, chat exports, notes... no need to categorize them first, just throw them all in.

![](https://pic.yupi.icu/1/image-20260409144409055.png)



### Collect Public Materials from the Web

If you already have public content online—blogs, videos, social media, etc.—you can also let AI help gather it online so you don’t have to hunt it down one by one yourself.

The prerequisite is that your AI tool supports web search, whether through built-in search, page scraping tools, Firecrawl MCP, or similar options.

Here’s a template prompt for collecting materials:

```
我想把自己蒸馏成一个 Agent Skill，现在需要先收集关于我的素材。

我已经在 references/ 文件夹里放了一些本地素材，请先阅读这些文件，再结合联网搜索补充更多信息。

我的基本信息：
- 名字：[你的名字]
- 身份：[比如程序员、产品经理、独立开发者]

我的公开内容渠道（请逐一访问并整理关键内容）：
- [平台1]：[链接]
- [平台2]：[链接]
- ...

同时请联网搜索更多关于我的公开信息（文章、采访、产品、他人评价、大事件等）。

要求：
1. 只整理，不分析。记录原始信息，不要提炼观点或下结论
2. 按来源类型分成几个文件存到 references/ 目录下（如个人内容、他人评价、产品与项目、经历与事件等，可根据内容量灵活调整）
3. 每条信息标注来源链接和信息类型（本人原话/本人文章/他人评价/媒体报道）
4. 整理完后告诉我：收集了多少条信息、覆盖了哪些方面、哪些方面信息不足
```

Just replace the template content with your own information. For example, the prompt I actually sent was:

```markdown
我的基本信息：
- 名字：程序员鱼皮
- 身份：AI + 编程知识博主、教育创业者、全栈开发者

我的公开内容渠道：
- B 站主页：https://space.bilibili.com/12890453
- 公众号：程序员鱼皮（搜索相关文章）
- 掘金博客：https://juejin.cn/user/2444938365386621
- GitHub 主页：https://github.com/liyupi
- 公司主页：https://yuyuanweb.com
- 个人产品大全：https://dogyupi.com
- 个人经历和编程学习路线：https://github.com/liyupi/codefather
```

![](https://pic.yupi.icu/1/image-20260409153025082.png)

The AI completed the material collection and created multiple categorized files:

![](https://pic.yupi.icu/1/image-20260409160036931.png)

If AI tells you that some kinds of materials are missing, you can manually add more.



## Step 2: Analyze the Materials and Generate a Profile

At this point, the materials are organized, but they’re still just a pile of scattered raw ingredients.

In this step, you ask AI to read through everything and extract a structured **Character Analysis Report**, including your core viewpoints, expression style, way of doing things, and key experiences, all condensed into one document.

This report becomes the foundation for all later steps.

Send AI the following prompt:

```
references/ 里的素材已经整理好了。

现在请你通读所有素材，对我进行全面分析，生成一份「人物分析报告」，
保存为 references/人物分析报告.md，包含以下维度：

1. 身份概要：我是谁、做什么的、关键背景
2. 核心观点和方法论：我反复在说的、真正相信的东西
3. 表达风格：句式偏好、口头禅、幽默方式、说话节奏
4. 做事方式：我怎么做决策、推荐什么、反对什么
5. 关键经历时间线：按时间排列的重大节点
6. 他人评价：别人怎么看我

每个结论标注依据来源（来自哪个文件/链接），信息不足的维度直接说明。
```

![](https://pic.yupi.icu/1/image-20260409160843491.png)

The AI generated a detailed character analysis report. For example, it extracted my expression style as: conclusion first → expand in points → one-sentence summary; self-deprecating humor; short paragraphs with lots of whitespace; blunt when giving advice, but ending warmly.

![](https://pic.yupi.icu/1/image-20260409161228612.png)

If you want the distillation result to be better, you can also look at AI’s suggestions. For example, it asked me to provide transcripts of my spoken style from Bilibili videos and original student evaluations, so I fed it some more video scripts.

The AI then added more analysis of my speaking style to the report:

![](https://pic.yupi.icu/1/image-20260409162017577.png)



## Step 3: Let AI Ask Follow-Up Questions to Dig Out Deep Thinking

The materials you collected earlier can show what you’ve said and done, but a good Skill needs something deeper: how you think, why you make certain judgments, and under what conditions you change your mind.

The goal of this step is to let AI ask follow-up questions that uncover your mental models, decision logic, and internal contradictions, so the final Skill won’t just “sound like you,” but will “think like you.”

Tell the AI:

```markdown
基于你刚才的人物分析报告，现在我需要你更深入地了解我，
目标是提炼出我的「思维操作系统」，包括我看问题的方式、做判断的逻辑、表达的习惯。

请你先告诉我你初步提炼出的：我的核心心智模型、决策规则、表达特征。
然后追问我 10 ~ 15 个问题，重点挖掘：
- 我反复强调的观点，背后更深的原因和适用边界
- 我做判断的具体标准，以及做错过的决策
- 我说的和做的不一致的地方
- 我绝对不会做的事

问题要根据分析报告中的具体内容来问，不要问通用问题，用聊天的语气。
```

The AI gave me my core mental model, but the terminology was so dense I almost couldn’t understand it:

![](https://pic.yupi.icu/1/image-20260409163556431.png)

Then the AI asked me 12 follow-up questions. These weren’t generic templates—they were customized based on the materials I provided, and every question was sharp:

![](https://pic.yupi.icu/1/image-20260409163641942.png)

You can just answer in your normal everyday way of speaking. For example, the first question:

> You say “if you keep going, you’ll definitely succeed,” but you also said you cut losses on Yuzhihui AI after just one month, and your murder-mystery game store also shut down. How do you distinguish between “I should keep going” and “I should cut losses immediately”? Do you have a concrete judgment standard—time, money, or some kind of feeling?

My answer: persistence doesn’t mean stubbornly going down one road no matter what. It means doing what you currently believe is most worth doing as well as you possibly can. First judge the direction based on the situation, then go all in on the direction you believe is right.

It’s best to save both the questions and your answers into a separate document so you don’t lose them. After finishing all the answers, send them back to AI and let it merge them into the analysis report:

```markdown
请你把我的回答整合到分析报告中，更新心智模型和决策逻辑的提炼。
@你的回答
```

![](https://pic.yupi.icu/1/image-20260409165326778.png)

Through my answers, the AI came to understand me better. It made 6 key corrections and deepened the mental model:

![](https://pic.yupi.icu/1/image-20260409165739285.png)



## Step 4: Add Capabilities (Optional)

At this point, the AI already understands you quite well. But a good Skill shouldn’t just “sound like you”—it should also *do things* like you. When facing a concrete problem, it should be able to research first and then give advice like a real person would.

This step upgrades the Skill from “parroting your style” to “actually helping people.”

You can tell AI what special abilities your Skill should have.

Using myself as an example, since I have a lot of resources related to learning programming, job hunting, and learning AI spread across different websites, I wanted the Skill to automatically fetch the latest information from those sites when answering related questions.

Here is the prompt I prepared for AI:

```markdown
之后生成最终 Skill 时，请加入以下能力：

1）联网搜索：遇到需要具体信息的问题时（比如最新技术趋势、某个工具的用法），先用联网搜索工具查资料，再用我的风格和判断框架回答。

2）指定信息源：回答跟我相关的问题时，优先去这些地方获取最新信息：
- https://dogyupi.com ：用户问"鱼皮有什么产品"或想了解我的整体业务时，去这里查产品大全
- https://www.codefather.cn ：用户问编程学习路线、项目教程、技术知识时，去这里查最新教程
- https://ai.codefather.cn ：用户问 AI 相关的工具、教程、资讯时，去这里查 AI 导航和知识库
- https://mianshiya.com ：用户问面试题、刷题、求职准备时，去这里查面试题库
- https://laoyujianli.com ：用户问怎么写简历、改简历时，推荐这个工具
- https://github.com/liyupi ：用户问我的开源项目或想看源码时，去这里查

3）持续进化：支持通过补充新素材来持续更新和优化 Skill
```

You can also add a `scripts` directory and place some Python scripts there to automate operations, or even connect APIs to fetch data from your own products.

But since many AI coding tools now already come with built-in web search and page scraping, I didn’t bother writing extra scripts here.

After sending the prompt, AI confirmed that it understood the task:

![](https://pic.yupi.icu/1/image-20260409170756966.png)



## Step 5: Start Distilling

The previous four steps already collected all the information. This step asks AI to assemble everything into a standard `SKILL.md` file.

First install the `skill-creator` skill provided by Anthropic. It’s basically “a skill for creating skills,” guiding AI to automatically generate a Skill structure that follows the spec.

You can install it with a one-line command:

```bash
npx skills add https://github.com/anthropics/skills --skill skill-creator
```

![](https://pic.yupi.icu/1/image-20260409180936318.png)

Once it’s installed, state in your prompt that you want to use skill-creator (or directly use the slash command `/skill-creator`):

```markdown
现在你已经通过素材整理、分析报告、追问访谈全面了解了我。
请使用 skill-creator 为我创建一个完整的 Skill。
要求：
1. 以我的身份和口吻说话，像我本人在回答一样
2. 提炼出我看问题的方式、做判断的规则、说话的习惯
3. 如果上一步配置了联网搜索和信息源，也写进 Skill 里
4. 写明这个 Skill 做不到什么、以及怎么用新素材更新它
生成完成后，自己想 3 个用户最可能问的问题，用 Skill 回答并评估是否像我。
```

![](https://pic.yupi.icu/1/image-20260409171938570.png)

The AI completed the development and testing of the entire Skill. The generated `yupi-skill` directory is already a directly usable Skill package:

![](https://pic.yupi.icu/1/image-20260409172607113.png)

Mission accomplished!



## Try the Result

Open a new AI conversation and let’s see whether the distilled “Yupi” is any good.

First, ask a question about learning direction:

```markdown
/yupi-skill 我想自学 AI 编程，怎么办？
```

The AI’s reply was very pragmatic. It not only recommended a self-study approach, but also automatically checked my Programming Navigation website and recommended my beginner AI coding tutorial:

![](https://pic.yupi.icu/1/image-20260409173135021.png)

Then ask a question related to Yupi’s personal experience:

```markdown
/yupi-skill 鲏哥，你大学是怎么学编程的啊
```

The AI’s answer fit my style pretty well. In one word: just do it!

![](https://pic.yupi.icu/1/image-20260409173902297.png)

Then ask an interview-related question:

```markdown
/yupi-skill 鲏儿，我要面试 AI 应用开发岗位了，怎么准备啊！
```

The AI not only gave a time plan and preparation advice, but also automatically recommended Yupi’s tutorials and interview question bank resources:

![](https://pic.yupi.icu/1/image-20260409174132048.png)

The result is pretty good. At least the speaking style and recommended resources both feel a lot like me~



## Open-Source Release

Once testing looks good, you can open-source the whole `yupi-skill` directory.

Be careful not to open-source all the source material files used during Skill creation—things like chat logs, personal-experience documents, and character analysis reports are best left out. Especially if you’re distilling yourself or someone around you, those materials may expose private information.

That said, to be safe, you should still confirm that the generated Skill does not depend on those build-time documents. Of course, if privacy isn’t a concern and you want better results and more accurate answers, you can keep some reference files as needed.

![](https://pic.yupi.icu/1/image-20260409172930076.png)

Then ask AI to generate an attractive README.md introduction document for the project:

```markdown
参考 GitHub 上知名的 Skill 仓库：https://github.com/titanwings/colleague-skill/

帮我给 @yupi-skill 生成完备的、有吸引力的 README.md 文档。

然后把这个目录开源到 https://github.com/liyupi/yupi-skill
```

![](https://pic.yupi.icu/1/image-20260409174544926.png)

Alright, now everyone can use the distilled Yupi.

> Open-source link: https://github.com/liyupi/yupi-skill

![](https://pic.yupi.icu/1/image-20260409175224601.png)

But honestly, something will inevitably be lost in the distillation process. No matter how similar the digital clone is, it’s still only a “shadow.” It still doesn’t have the warmth of the real Yupi.

Mm, I choose to believe that’s true. Don’t optimize yourself out of existence...



## Final Thoughts

The entire distillation process isn’t complicated. In summary, it has five steps: collect raw materials → generate a profile → AI follow-up questioning → add capabilities → start distilling.

The whole process requires no coding at all—if you can use your hands, you can do it.

Today, anyone can be distilled into digital life. You can distill yourself and let AI complete tasks in your style.

But I still want to remind you: before distilling someone else, it’s best to get their consent first. After all, this involves their way of speaking, thinking habits, and even private conversations. Distilling them without permission is inappropriate and may also create privacy and legal risks.

Technology itself is neutral. The key is how you use it.

This project may look like a meme on the surface, but it demonstrates an important AI coding use case: using AI to preserve and pass on personal knowledge. Whether it’s a technical expert on your team, an industry specialist, or your own unique experience, all of it can be turned into reusable AI Skill packages this way.

I hope this case gives you some inspiration. Maybe you can try distilling yourself into a Skill too and see what the AI version of you looks like.



## Recommended Resources

1) Yupi AI Navigation: [A complete collection of AI resources, the latest AI news, and free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussion and Q&A](https://www.codefather.cn)

3) Programmer Interview Cheat Sheets: [High-frequency topics for internships, campus hiring, and experienced hiring, plus real company question analysis](https://www.mianshiya.com)

4) Resume-writing tool for programmers: [Professional templates, rich example sentences, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships, campus hiring, and experienced hiring](https://ai.mianshiya.com)
