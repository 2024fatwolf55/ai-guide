# Claude Code - AI Pelvic Floor Training Assistant Project Case Study

This project is an AI-powered pelvic floor exercise assistant website that provides scientific tiered training programs, animated guidance, voice prompts, and also supports camera-based posture detection and AI correction advice. The whole thing was built using Claude Code + DeepSeek V4.

Hello everyone, I’m Yupi.

Sigh, sitting for long periods without moving is practically every programmer’s chronic problem. I’m busy out of my mind every day and have no time to exercise, but I also don’t want to just let my body keep deteriorating. So what should I do?

That’s when I asked AI and learned about “pelvic floor exercises.” By strengthening the pelvic floor muscles and improving local blood circulation, they can effectively help prevent hemorrhoids, improve bowel and urinary incontinence, and enhance the health of the anus and related pelvic organs.

The key point is that you can do this anytime, anywhere. It’s way too suitable for me!

![](https://pic.yupi.icu/1/ybzj.jpg)

But I’m personally a total “exercise idiot,” so I started wondering whether I could use AI coding to build a “pelvic floor assistant” that helps everyone train scientifically, so even an absolute dummy can do it right.

Let’s do it!

Next, I’ll use Claude Code + DeepSeek V4 from start to finish to build a complete project, taking you through installation, configuration, development, and testing step by step. After reading this, you’ll learn a beginner-friendly way to use Claude Code, get a feel for DeepSeek V4’s real coding ability, and also pick up a lot of practical AI coding tricks.

Save it first—let’s begin~



## Requirement Analysis

This project is called `tgang-helper`, “Pelvic Floor Assistant,” and its core functions actually aren’t that complicated.

1) It should provide scientific, tiered training programs differentiated by gender and difficulty, covering multiple exercise types such as quick contractions, sustained contractions, and ladder contractions.

2) During training, it needs animated rhythm guidance, including a breathing-circle animation and posture demonstration animation, so users can instantly understand what to do.

3) At the same time, the browser’s speech synthesis should broadcast instructions in real time, so users can follow along with their eyes closed.

4) Another highlight is posture correction using the camera. It should detect in real time whether your standing or sitting posture is correct—for example, whether you’re hunching, shrugging, or leaning to one side—and when posture problems are detected, AI should provide personalized correction suggestions.

5) It should also let users view a training check-in calendar and statistical charts.

![](https://pic.yupi.icu/1/image-20260429104714827.png)



## Solution Design

If you have absolutely no technical background at all, you can let AI help design the solution for you.

But here, to save time and tokens, I directly told AI how to do it.

Although it includes posture detection, this project can be done almost entirely as a **front-end project**! No complicated back end is needed.

For the tech stack, I chose Next.js + TypeScript. Posture detection uses MediaPipe Pose running fully on the front end. AI calls are proxied through a Next.js API Route to the DeepSeek V4 model. Animation uses CSS animation + Framer Motion.

Why not use a Python back end?

Because the only server-side piece needed in this project is proxying the AI API call. A Next.js API Route can handle that perfectly well, so there’s no need to split the project into a separate front end and back end. The simpler, the better.

![](https://pic.yupi.icu/1/tgang-helper-design.jpg)



## Environment Setup

### Installing Claude Code

Let me briefly introduce Claude Code. It’s an AI coding tool released by Anthropic that runs directly in the terminal. You chat with it and describe your requirements, and it can autonomously analyze the project, write code, run commands, and fix bugs from start to finish.

Besides basic code generation, it can also use tools and Skill packages, connect MCP external services, extend its abilities with Plugins, and even do multi-agent collaboration. It’s highly extensible.

![](https://pic.yupi.icu/1/image-20260429110454017.png)

Installing Claude Code is simple.

First, make sure your computer has Node.js and npm. If not, just go to the [official Node website](https://nodejs.org/en/download) and download the easy installer:

![](https://pic.yupi.icu/1/1777341714221-67b76f0e-c816-410b-adc0-e445074efc46.png)

No matter which operating system you use, you can install Claude Code with a single npm command:

```bash
npm install -g @anthropic-ai/claude-code
```

![](https://pic.yupi.icu/1/1777341807032-be0f1d99-4e97-4be6-80de-de7c32846d41.png)

After installation, type `claude` to enter the conversation interface. The first time, you’ll need to log in before you can use it normally:

![](https://pic.yupi.icu/1/1777341971646-93bcacc7-143d-4f86-8d2a-bf17d288db9f.png)

But I’m guessing many people don’t have Anthropic overseas subscription accounts, so we need to switch to a domestic model.



### Switching Models

Claude Code itself supports switching models. You can connect other large-model APIs by modifying environment variables or editing configuration files.

Usually, whichever model API you’re using, you can just check the corresponding official documentation for integration instructions.

For example, the [DeepSeek API docs](https://api-docs.deepseek.com/zh-cn/guides/coding_agents) already provide a ready-made integration method:

![](https://pic.yupi.icu/1/1777342329147-99094795-9da9-40b7-aa25-a566fc762c54.png)

But I recommend an open-source tool called **CC Switch** even more. It can visually manage the configurations of AI coding tools like Claude Code, Codex, and Gemini CLI, and lets you switch model providers with one click. It has more than 50 built-in provider presets, so you don’t need to manually edit config files yourself.

> Open-source link: https://github.com/farion1231/cc-switch

Following the official Chinese docs, choose the installation method based on your operating system:

![](https://pic.yupi.icu/1/1777342571992-7b055f5f-3d27-4463-8247-4fe9bc315690.png)

Mac users can install it from the command line:

```bash
brew tap farion1231/ccswitch
brew install --cask cc-switch
```

![](https://pic.yupi.icu/1/1777342701813-0dc223c6-8c13-49ce-8434-aa00bfc6d08e.png)

After installation, run the software, enter the main interface, and add a model provider:

![](https://pic.yupi.icu/1/1777342816975-d7e89ce3-3b26-4237-a728-5478fbe86a47.png)

Choose DeepSeek:

![](https://pic.yupi.icu/1/1777342881212-d0591f6e-c88e-4912-8cf5-62b7f1bfac17.png)

Fill in the API Key, which you can obtain from the [DeepSeek Open Platform](https://platform.deepseek.com).

![](https://pic.yupi.icu/1/1777342981319-1e6c85a9-5063-42e2-bae9-0406886578d9.png)

Here I set the main model to DeepSeek-V4-Pro, which has stronger Agent ability and complex reasoning than DeepSeek-V4-Flash.

Then click Save in the lower right:

![](https://pic.yupi.icu/1/1777343299981-c370c8ff-b24a-460a-891e-e08bc1efcf54.png)

As you can see in the image above, Claude Code uses a JSON configuration file. CC Switch is basically helping you modify the config files of various AI tools visually, so you don’t have to edit JSON by hand.

Finally, enable the DeepSeek model:

![](https://pic.yupi.icu/1/1777343334412-73a61961-5d7e-4fbb-a0e0-691f5d867b48.png)

Then re-enter Claude Code. Type any sentence, and if the AI replies, the model switch was successful:

![](https://pic.yupi.icu/1/1777343427500-46c84648-4f92-4ed4-85ab-4af0b34f465e.png)



### Installing Extensions

Claude Code already includes basic abilities like reading and writing files, running terminal commands, and searching code. But to build a complete project well, that’s still not enough.

We need the following 3 extensions:

1. Frontend Design: a front-end beautification skill that makes generated pages look more polished
2. Firecrawl: web search and page scraping so AI can get the latest technical information
3. Context7: lookup of the latest technical documentation and API usage, reducing AI hallucinations

Let’s install them one by one.



#### 1. Installing Frontend Design

Frontend Design is Anthropic’s official front-end beautification skill. It can make AI-generated pages feel much more designed.

In Claude Code, first use the `/plugin` command to add the official skill marketplace. This is basically like installing a skill store:

```bash
/plugin marketplace add anthropics/skills
```

![](https://pic.yupi.icu/1/1777344066799-72c95f99-82bc-46ff-92f5-02cf6d21b1b9-20260429113524910.png)

Type `/plugins`, then in the Discover menu select `example-skills` and press Enter to install the official example skill bundle:

![](https://pic.yupi.icu/1/1777344221815-19f8cc7d-e608-4cf6-a8a9-05fa3dafab04.png)

Type `/reload-plugins` to reload the plugins:

![](https://pic.yupi.icu/1/1777344303461-6af1d179-4328-4892-83b4-a48f1af3c32d.png)

Type `/skills` to view the installed skills, and you’ll see that `frontend-design` is already in place:

![](https://pic.yupi.icu/1/1777344408094-9d8e06b5-a216-443e-a7ec-70dd78cb80d0.png)

After that, typing `/frontend-design` in the chat box will actively trigger this skill and let AI beautify the page. It also automatically installs the `webapp-testing` automation testing skill, which will be useful later.



#### 2. Installing Firecrawl

Firecrawl is a web search and page scraping tool that lets AI search for the latest technical information before development.

Installation is very simple. Open a terminal and enter this one-line command:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

![](https://pic.yupi.icu/1/1777258212308-8c83d23e-338e-4ec2-b1c0-05f54a22a36e-20260429113525121.png)

After running it, a browser window will pop up and you need to click authorize on the page:

![](https://pic.yupi.icu/1/1777258069152-2d7fdb02-64e2-440b-bcbd-6254b07fb74e-20260429113525154.png)

After installation, it automatically registers 12 Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777258235867-0f6f08f5-4791-4b66-84b7-50936912540d-20260429113525186.png)

In Claude Code’s skill manager, you’ll then be able to see the newly added Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777344739629-f15409cf-6a43-4f96-a9bd-be72f7c0f795.png)



#### 3. Installing Context7

Context7 is a technical documentation lookup tool that gives AI access to the latest official docs for various frameworks and libraries, helping it avoid writing code with outdated APIs.

First, enter this one-line terminal command to install it:

```bash
npx ctx7@latest setup
```

It will ask whether to install an MCP service or CLI + Skills. I chose CLI + Skills here. You’ll notice that more and more tools are shifting from MCP toward the CLI + Skills approach:

![](https://pic.yupi.icu/1/1777258448310-41f86ec3-26e1-476e-aed5-4913c8116d21-20260429113525253.png)

You also authorize it through a pop-up webpage, without needing to fetch or enter an API Key yourself. Super convenient!

![](https://pic.yupi.icu/1/1777258547209-dc872280-09eb-4bd9-ad45-2e412382002d-20260429113525305.png)

Then choose which AI coding tool to install it for. I chose Claude Code:

![](https://pic.yupi.icu/1/1777344820438-9397de28-5658-4f0c-8cbe-8ed350beb84a.png)

After installation succeeds, you’ll see the `find-docs` skill in the skill manager:

![](https://pic.yupi.icu/1/1777344978229-17483cf7-a0fd-4a5f-93cf-5865f96eab41.png)

Of course, you can also choose the MCP Server installation method:

![](https://pic.yupi.icu/1/1777345106455-e31fd005-3cc6-45ac-a9d5-7dfafd30c7f4.png)

After installation, type `/mcp` in Claude Code and you’ll see the installed MCP there. It’s far more convenient than configuring it manually yourself!

![](https://pic.yupi.icu/1/1777345145401-72377bd2-2388-4f3b-bd8f-a31a76ecc676.png)

At this point, the environment setup is complete! Next time you build a project, you won’t need to repeat all this prep work~



## Development and Coding

Create a new project folder named `tgang-helper`, `cd` into it in the terminal, then type `claude` to open Claude Code:

![](https://pic.yupi.icu/1/1777346556569-10234894-8a0e-4efe-98cb-a9d14b122279.png)

Then enter the prompt. Here I’ll share the complete prompt I actually used, for reference:

```markdown
## 角色

你是一个前端全栈工程师，擅长 Next.js + TypeScript 开发。

## 任务

开发一个叫 tgang-helper 提肛助手的 Web 应用，帮助用户科学地练习盆底肌训练（提肛 / 凯格尔运动），傻子也能练对。

提供科学的分级训练课程，区分男女和难度，涵盖快速收缩、持续收缩、阶梯收缩等多种动作类型。训练过程中通过动画引导节奏，包括呼吸圈动画（收缩时缩小、放松时扩大）和人体姿势示范动画（用 SVG 或 Lottie 展示每个动作的正确体位和发力部位），让用户一看就知道该怎么做。同时使用浏览器语音合成（Web Speech API）实时播报指令，让用户闭着眼睛也能跟练。

支持开启摄像头进行体位校正，使用 MediaPipe Pose 在浏览器端实时检测用户的站姿 / 坐姿是否正确（如驼背、耸肩、身体歪斜），所有检测纯本地运行，摄像头画面不上传服务器。当检测到持续的姿势问题时，将姿势数据（非图像）发送给 DeepSeek V4 模型，获取个性化的纠正建议并语音播报。

训练记录保存在本地 localStorage，展示打卡日历和简单的统计图表。

## 技术栈

- 框架：Next.js + TypeScript
- 姿态检测：MediaPipe Pose（纯前端）
- AI 对话：通过 Next.js API Route 代理调用 DeepSeek V4 模型（兼容 OpenAI SDK 格式）
- 动画：CSS 动画 + Framer Motion

## 要求

1. 页面美观专业，使用 frontend-design 技能美化页面，配色健康积极
2. 开发前，先通过 Firecrawl 联网搜索 MediaPipe Pose 浏览器端用法，通过 Context7 查询最新技术文档和用法
3. 必须生成完整可运行的代码，每步完成后必须自主测试验证
```

Here’s a simple interpretation of a few key points in that prompt:

- **Role definition** comes first to put the AI into the mindset of a front-end/full-stack engineer
- **Task description** clearly explains the requirements in natural language
- **Tech stack** lists only the key choices, leaving implementation details up to AI
- The last two requirements are crucial: ask AI to check documentation before writing code so it doesn’t hallucinate implementation details, and require it to self-test after development to reduce failures

Before sending the prompt, I pressed Shift + Tab to enter auto-accept edit mode, so the AI could create, modify, and delete files and execute commands without asking me for confirmation one by one. It’s more convenient, but there is some risk, so use it as needed:

![](https://pic.yupi.icu/1/1777346788040-741dcad6-7e89-416d-ba95-7d603ad697b6.png)

After sending the prompt, the next step was a long wait.

The AI started developing autonomously: first searching technical docs, then planning the project structure, creating files, and writing code.

During the process, the AI may ask to confirm tool calls. For example, when it wanted to use Context7 to get the latest MediaPipe documentation, you can choose “Yes, and don’t ask again,” so you won’t have to keep confirming repeatedly later:

![](https://pic.yupi.icu/1/1777346850967-af94d579-7bb7-4e15-a250-d54dd513a593.png)

After more than 20 minutes, the AI finished the development on its own and even automatically ran the project:

![](https://pic.yupi.icu/1/1777348979066-ad363834-ffea-424e-89e7-d581a933105e.png)

Then the AI used the `webapp-testing` skill to write automated test scripts and automatically opened the browser to test the app:

![](https://pic.yupi.icu/1/1777349013499-cef79455-9bb9-4e0c-8c0e-8ee4c6a64f25.png)

After 31 minutes, the task was finally complete—nearly twice as slow as the last time I used GPT-5.5 to build a project of the same scale. During that time, I not only finished one round of pelvic floor exercises, I also ate a meal.

![](https://pic.yupi.icu/1/1777349057921-d3174644-8481-4505-9640-4853f8f905fd.png)

From AI’s summary, you can see that it implemented the full feature set, including 7 training programs, breathing-circle animation, SVG human figure, voice guidance, posture detection, AI suggestions, training records, and statistical charts—all in one go.

Typing `/context` lets you check current context usage. It had already used 94,000 tokens, which was 47% of the total capacity:

![](https://pic.yupi.icu/1/1777349331672-bfbc8216-5edb-4645-866c-76ac1a36c36a.png)

You might wonder: DeepSeek V4 officially says it supports a 1 million token context window, so why does Claude Code show only a 200K limit?

That’s probably because Claude Code itself has its own context-window limit, which is different from the model’s own upper bound. So I recommend checking context usage regularly. Once it fills up, the AI may start “blacking out” and randomly rewriting code.



## Testing and Verification

Next comes testing and verification. Since the project uses DeepSeek V4 for AI functionality, I first asked the AI to create an environment variable file for me:

```
帮我创建 .env.local 文件
```

The AI created it quickly and also thoughtfully checked `.gitignore` to confirm that the `.env` file would not be committed to Git:

![](https://pic.yupi.icu/1/1777349272456-95ce7d9c-6e91-48f9-ba76-cb96c6cec3f5.png)

Then I opened the `.env.local` file and filled in the API Key from the DeepSeek Open Platform:

![](https://pic.yupi.icu/1/1777349474695-3ded1d25-8709-461b-81d9-051520e7adac.png)

Then I opened the page in the browser.

You know what? I actually like this style a lot. It’s very clean and refreshing, and the color scheme also feels healthy and positive. I just honestly don’t quite understand that logo—someone please explain it to me...

![](https://pic.yupi.icu/1/1777349549522-a0bcefd1-754d-4af3-b89c-6ca67e1d76b7.png)

I first selected male, beginner difficulty, and turned on voice guidance plus camera posture detection.

Good grief—even the beginner courses have more than one option. There are “Pelvic Floor Activation” and “Daily Quick · 3-Minute Wake-Up.” Let’s start with the male beginner one:

![](https://pic.yupi.icu/1/1777358526114-0db8c685-376b-4bc1-8c52-f19cc07182ea.png)

After entering the training screen, there’s a stick-figure animation guiding my posture. There’s also a breathing animation so I can follow the rhythm—tighten, relax, and alternate between them:

![](https://pic.yupi.icu/1/1777358544658-ed5ad867-29cb-4e70-8dc5-7d637abfa74e.png)

Once the camera is on, MediaPipe Pose detects my posture in real time and sends posture data to the DeepSeek model when it finds issues. Here’s a small trick: simple posture-correction advice doesn’t need the Pro model. Using V4-Flash is faster and cheaper.

![](https://pic.yupi.icu/1/1777358609700-a6f75a7d-0d7e-4f05-a48a-87c63538318c-20260429113525969.png)

For example, when it detected that my body was tilted, it gave correction advice like: “A tilted body will affect force generation. First square your pelvis. Imagine a string gently lifting the top of your head so the spine naturally stays upright.” It honestly felt like I had hired a private fitness coach...

![](https://pic.yupi.icu/1/1777358872878-89017863-7920-4a60-9876-d390f8075e36.png)

I tried adjusting my posture, and it immediately gave new feedback: “Try planting both feet firmly on the ground and square your pelvis. Gently contract the pelvic floor and keep the spine neutral.”

![](https://pic.yupi.icu/1/1777358938592-94465606-6470-4400-82f4-a8816f7d96ee.png)

During the sustained-contraction phase, it reminded me to relax my shoulders, saying: “Relax your shoulders and let them drop. Imagine your shoulder blades sliding toward your lower back. Exhale gently and feel the pelvic floor lift naturally.”

![](https://pic.yupi.icu/1/1777358994159-34179e8a-ac7b-4f51-9433-4e02784e8728.png)

During the testing process, I ended up doing several more rounds of pelvic floor exercises. This is no longer Vibe Coding. I call it **TGang Coding**—coding while doing pelvic floor exercises, making both body and work progress at the same time. Beautiful, isn’t it?

At this point, I can already challenge the “Male Advanced · Strength Enhancement” mode: 7 sets in 10 minutes. Even in this mode, the AI can still accurately detect issues like body tilt and unstable center of gravity:

![](https://pic.yupi.icu/1/1777359368736-475ff9a5-b6c6-4032-a330-c57946095f7e.png)

![](https://pic.yupi.icu/1/1777359434842-5d4caa9e-66b0-43cd-bfde-4c50b1e4121f.png)

After finishing the training, you can view a check-in heatmap and statistical data on the training records page. Persistence wins!

![](https://pic.yupi.icu/1/1777359021697-c7dd735b-76dc-41da-9416-136fb22d7681-20260429113526343.png)

Honestly, getting AI to one-shot the entire project from a single prompt, with the core functions basically usable, means DeepSeek V4’s result is pretty good.

That said, there were still some small bugs when it actually ran. For example, the breathing animation’s contraction/relaxation rhythm didn’t match the real training movements, the quick-contraction mode kept showing “contract” without switching to “relax,” and the timing for calling AI posture suggestions wasn’t controlled well, causing overly frequent requests.

![](https://pic.yupi.icu/1/1777357933266-a1f1febe-edc3-4710-8504-8ddf440a8ddc.png)

These were all gradually discovered during testing. The effects shown above are actually the result after I had about 10 more rounds of conversation with the AI and fixed those issues.

Let me share one of my own lessons here. During testing, if a problem affects core functionality, fix it immediately. For example, if the animation rhythm is wrong, describe the behavior directly to AI and let it correct it.

If the issue doesn’t affect core functionality—say, something on the interface just doesn’t look good enough—my suggestion is to write it down first and handle it in a batch after the core flow is working end to end.

Also, throughout the process, you must keep an eye on context capacity. After I fixed these several rounds of bugs, context usage had already risen to 62%:

![](https://pic.yupi.icu/1/1777358465249-dbc18a92-6c77-471d-a15e-4f79a7837a67-20260429113526400.png)

Once the context gets close to full, AI may forget what it changed earlier and even write code that contradicts previous changes.

When that happens, I recommend first asking AI to consolidate the project’s current information and progress into a document (for example, writing it into `CLAUDE.md`), then starting a new conversation to continue development. That both saves tokens and avoids losing important context.



## My Take

Finally, let me talk about my real feelings after this hands-on project with Claude Code + DeepSeek V4.

First, let’s talk about DeepSeek V4’s actual performance. **A single prompt producing a complete project in one go, with the core functions usable**—it almost gave me the same kind of surprise I once felt from Opus.

The front end doesn’t have particularly stunning innovation, but the layout is basically correct and the colors are not bad at all. That said, as mentioned earlier, there are still shortcomings in the logic details, so a few rounds of manual intervention were needed to polish things properly. And DeepSeek V4 is also a bit slower at code generation—it took 31 minutes just to get the core functions running.

Besides the effect, let’s also look at the **cost** everyone cares about.

How much did this project actually cost?

First, I used the `/usage` command inside Claude Code to check token usage:

![](https://pic.yupi.icu/1/1777359631006-6a630d28-fda7-426d-9b7d-e188b8fdf9b5.png)

Claude Code’s statistics showed that this development cost a total of 18.13 USD and used several hundred thousand tokens.

You can also go into the Stats trend analysis view to look at your usage habits:

![](https://pic.yupi.icu/1/1777359683244-29aecdd9-9ce9-4ff0-b072-71e58338fbf0.png)

What? A project like this cost over 100 RMB?!

Claude Code’s built-in cost statistics may not be very accurate, so I recommend checking the real consumption directly on the DeepSeek Open Platform.

When I checked, I saw that after hundreds of requests, it had consumed over 25 million tokens!

![](https://pic.yupi.icu/1/1777359821224-7aa241e7-c2a3-4740-8808-289422131b76.png)

But in reality, it only cost **5.44 RMB**. Very nice~

![](https://pic.yupi.icu/1/1777359775291-dca79c0d-6053-4721-ab50-6a2bb2895d04.png)

Most of those tokens were cache-hit input tokens. Because every time Claude Code talks to the model, it resends earlier context along with the new message—but if the content is unchanged from the previous turn, DeepSeek hits the cache, and cached input is billed at only a small fraction of normal input.

That’s why the token count looks scary, but the real cost stays low.

**5 RMB to build a complete project with AI capability**—I think that’s a pretty good deal. What do you think?




## Final Thoughts

5 RMB to build a complete project with AI capability really is a strong value proposition.

This project shows the potential of combining Claude Code with domestic large models. Although a few rounds of manual bug fixing were needed along the way, the core functionality worked in one shot, which is already more than enough for individual developers.

If you also want to use Claude Code to build projects, you can read *AI Command-Line Coding Tools* in the Coding Tools section of this tutorial to learn more about Claude Code usage and model-switching techniques.



## Recommended Resources

1) Yupi AI Navigation: [A complete collection of AI resources, the latest AI news, and free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussion and Q&A](https://www.codefather.cn)

3) Programmer Interview Cheat Sheets: [High-frequency topics for internships, campus hiring, and experienced hiring, plus real company question analysis](https://www.mianshiya.com)

4) Resume-writing tool for programmers: [Professional templates, rich example sentences, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships, campus hiring, and experienced hiring](https://ai.mianshiya.com)
