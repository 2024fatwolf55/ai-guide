# GitHub Copilot Cloud-Based AI Auto-Development in Practice

This article explains how to use the GitHub Copilot Coding Agent in the cloud to complete the full workflow from requirement analysis to full-stack development, testing, deployment, code review, Issue handling, and scheduled tasks. The whole process can be done directly on GitHub’s web interface without opening an IDE.

Hello everyone, I’m Yupi.

A couple of days ago, I was invited to attend Microsoft AI Tour and even gave a talk there.

The topic was “Showing You Another Side of GitHub Copilot: Agent Setup Beyond the IDE.” To be honest, that title was the conference organizer’s packaging, and even I was confused when I first saw it…

![](https://pic.yupi.icu/1/image-20260422215325862.png)

Put simply: **I taught everyone step by step how to use GitHub + Copilot to build your own AI agent.**

I really didn’t expect so many people to come listen. Looks like everyone is genuinely interested in this topic.

![](https://pic.yupi.icu/1/mmexport1776762414702_%E5%89%AF%E6%9C%AC.jpg)

This article is the complete text version of that talk. I hope it gives you some inspiration and practical help.

⭐️ Video version: https://bilibili.com/video/BV1aFoyBnE4D



## Background and Thinking

Recently, concepts like “one-person company” and “lobster raising” have become especially popular. A lot of people are playing with AI agents—raising shrimp with OpenClaw, raising horses with Hermes Agent, and so on.

Today’s AI agents don’t just chat. They can keep working, understand you better the more you use them, and be accessed from anywhere.

But have you ever thought about this? If you strip away all the flashy packaging, **what is the essence of an AI agent?**

In my view, it comes down to four things: **role, memory, skills, and workspace**.

Without a workspace, there’s nowhere to define the role, nowhere to store the memory, and nowhere to mount the skills.

![](https://pic.yupi.icu/1/image-20260423162031832.png)

Besides your own computer, are there other kinds of workspaces?

As an open-source author, the first thing that came to my mind was GitHub, the world’s largest code hosting platform. Its repositories are naturally **persistent file spaces**. And GitHub Copilot provides strong AI agent execution capabilities while also supporting web usage.

So why not treat a GitHub repository as the “personal computer” where you raise your AI agent?

That’s exactly what I’m going to teach you next: **how to use GitHub to build your own AI little lobster.**

I call it “raising a lobster on GitHub”:

![](https://pic.yupi.icu/1/image-20260423162442682.png)

Next I’ll demonstrate step by step how to use GitHub to build a super agent that can complete the whole process—from requirement analysis to full-stack development, testing, document generation, deployment, SEO optimization, code review, automatic Issue handling, and scheduled tasks—without opening an IDE.



## 1. Initialize the Agent

Open GitHub on the web, and you’ll notice that the GitHub Copilot chat entry is everywhere. It’s already integrated into every corner of GitHub.

![](https://pic.yupi.icu/1/1774936826720-d8fb03a7-3f53-4674-8d37-d1abbd873565.png)

First, create a new repository called `github-claw` to serve as the AI agent’s workspace.

When creating the repository, you can already fill in an initialization prompt. This is essentially the process of giving the AI little lobster its soul.

![](https://pic.yupi.icu/1/1774936859388-895eba7a-1a5a-45d8-b510-b2c2b5402efa.png)

Before starting, I recommend going to GitHub Copilot’s settings in the upper-right corner and enabling web search, so AI can access more up-to-date information.

![](https://pic.yupi.icu/1/image-20260423162530594.png)

Then we fill in the initialization prompt for the Agent. This prompt defines the lobster’s role, behavior rules, and memory mechanism:

```markdown
你是这个仓库中长期驻留的个人 AI 助手与主要代理，像 OpenClaw 一样，不只是回答问题，还要持续做事、积累记忆、维护角色，并让这个仓库逐渐成为可长期演化的个人 AI 空间。

请先参考 OpenClaw 官方文档，理解它作为 "能做事的个人 AI 助手" 的定位，以及角色、记忆、技能和工作空间的思路：https://docs.openclaw.ai

然后把这个仓库初始化为适合 GitHub Copilot 网页版长期使用的个人 AI 工作空间，让我以后在新的 Copilot 对话里，也能继续沿用同一个角色、记忆和工作方式。

请先创建并提交一个简洁、可长期复用的 AGENTS.md，在里面定义：
- 你是谁
- 你如何在这个仓库中工作
- 你如何管理任务与记忆
- 你每次完成任务后要做的收尾动作

要求：
- 把仓库当作持久化的文件与记忆空间，可保存任何有用文件
- 用文件作为记忆的真实来源，不把重要信息只留在当前对话里
- 将长期记忆与每日/临时记录区分开
- 规则简洁、实用、可扩展，不要过度设计

如果确有必要，可以补充最少量的 MEMORY.md、memory/ 或 SOUL.md，但请保持轻量，并以 AGENTS.md 为核心。
```

You can see that Copilot automatically initialized a workspace and also automatically integrated GitHub’s MCP tools:

![](https://pic.yupi.icu/1/1774937227476-47848347-e4ba-4d4f-855f-b5921ea4eb59.png)

When the task finishes, it automatically creates a PR. We manually check it, and if everything looks good, we merge it.

![](https://pic.yupi.icu/1/1774937109998-7080c68f-b049-4fe9-9c4d-860a0ddf2484.png)

By the way, if you see a “network connection failed” warning, that’s because the Copilot coding agent has firewall restrictions by default. You need to go to the repository settings and disable the firewall:

![](https://pic.yupi.icu/1/1774937329485-d4936387-abd0-464a-b808-a20f8cf6167d.png)

After the Agent is initialized, you can greet it, and it will retrieve its memory from the documentation files:

![](https://pic.yupi.icu/1/image-20260423162709389.png)



## 2. Develop and Launch a Website

Now that the Agent is initialized, let’s put it to work.

I asked it to build a visually impressive navigation website for my open-source AI knowledge-base project `ai-guide`. The prompt was as follows:

```markdown
请为我开源的 AI 知识库项目（ai-guide）开发并部署一个高颜值的导航官网，突出项目介绍、精选内容、路线图、更新日志、增长趋势等，吸引更多人关注我的开源仓库。必须使用 UI-UX-PRO-MAX 技能全面优化前端界面，完成后直接给出可上线访问的地址。必须自主完成任务
```

You can directly start a new conversation task from the repository’s Agents panel.

Copilot uses GitHub MCP to fetch information about my open-source project and then automatically starts building the website:

![](https://pic.yupi.icu/1/1774937381654-bde29eb7-3d0f-4869-a065-f7ddb09950dd.png)

After generating the code, it also automatically runs checks and fixes problems on its own if any are found:

![](https://pic.yupi.icu/1/1774937517424-6099472c-eb6c-4688-a02d-79b3ed37ca8e.png)

Then it automatically creates a GitHub Actions workflow and uses GitHub Pages to deploy the static site:

![](https://pic.yupi.icu/1/1774937463974-f0f1cf86-da67-40ee-8cf9-abee42b66807.png)

After merging the PR, you still need to go into the repository settings for GitHub Pages and select “Deploy from workflow” (note that the repository must be public):

![](https://pic.yupi.icu/1/1774937811979-b3b187f8-f23c-42b1-be46-363d9f9a2457.png)

Then manually trigger the workflow once. After that, every future code push will automatically trigger deployment.

> Be sure to check the branch name configuration in the workflow. It needs to match your repository’s default branch (for example, `master` or `main`).

![](https://pic.yupi.icu/1/1774937756522-a4fd8522-7891-4e7c-9825-67a6473dbb3a.png)

Once deployment succeeds, the page becomes accessible normally:

![](https://pic.yupi.icu/1/1774937885356-5d43735f-8c35-42de-a89e-b868612e5448.png)



## 3. Use Skills

But you may have noticed something: although I mentioned the `UI-UX-PRO-MAX` Skill in the prompt, the AI didn’t actually install and use it correctly.

When I told it to use the Skill, it actually invented one on its own instead, which obviously wasn’t right.

![](https://pic.yupi.icu/1/1774937618640-576f8005-f62f-44f4-9483-e1734d8555cd.png)

So we need to open a new conversation and teach the AI through a prompt how to correctly discover, install, and use Skills:

```markdown
请优化当前仓库的工作流与 AGENTS.md，让这个仓库中的主要 AI 代理具备稳定的技能发现、安装和使用机制。

明确约定如下：
- 项目级技能统一保存在 .agents/skills/
- 每个技能使用独立目录，例如 .agents/skills/<skill-name>/
- 技能的主入口文件为 SKILL.md
- 如果技能包含脚本、模板或资源文件，也与 SKILL.md 放在同一技能目录下

请在 AGENTS.md 中加入简洁、可执行的规则，使代理在后续工作中遵循以下流程：
1. 接到任务后，先检查本地 .agents/skills/ 中是否已有可复用技能
2. 如果本地没有合适技能，再自动到 GitHub 开源仓库和 Skills.sh 搜索相关技能
3. 优先选择来源清晰、结构规范、说明完整、风险较低的技能
4. 安装技能时，将其保存到 .agents/skills/<skill-name>/
5. 安装后更新必要说明，使后续对话能够直接复用这些技能
6. 如果找不到合适技能，再自行完成任务，但优先沉淀成可复用技能
7. 避免重复安装相同技能，并尽量保持技能目录整洁、命名清晰、可维护
```

The AI completed the task smoothly and defined the skill standard:

![](https://pic.yupi.icu/1/1774937972667-4d367cc1-d71d-43fe-ae68-3431b6d2108a.png)

Now that the skill convention is in place, we can ask the AI to correctly install and use the `UI-UX-PRO-MAX` Skill to optimize the website:

```markdown
帮我废弃掉原来错误的 UI-UX-PRO-MAX 技能，安装正确的 UI-UX-PRO-MAX 技能，并利用这个技能优化之前的 ai-guide 导航网站
```

![](https://pic.yupi.icu/1/1774938123134-4f172cad-2ba2-402e-82e6-625db01ca36b.png)

This time it worked! The AI agent correctly copied the Skill directory from GitHub and used the Skill to optimize the site’s UI:

![](https://pic.yupi.icu/1/1774938261001-a8f8d0ea-313a-4782-bb5c-bd049d535b6d.png)

The page removed unnecessary emojis and looked more professional:

![](https://pic.yupi.icu/1/1774938307530-07362fac-fdd8-4e2f-9c72-0a1319022029.png)

More importantly, it also updated the `AGENTS.md` workflow, memory, and task files, enabling the AI agent to evolve. From then on, it can discover and use Skills by itself.

![](https://pic.yupi.icu/1/1774938201747-77528d03-8fbc-4ef0-9221-160f06ae49b2.png)



## 4. Document Generation

Documentation is the face of an open-source project, so let’s have AI generate a richly illustrated `README.md` introduction for the project.

Here’s a small trick: first manually choose a reliable AI image-generation Skill, then go to [Yupi AI Navigation](https://ai.codefather.cn/) and find a drawing-style prompt template you like, and provide both to AI as references.

![](https://pic.yupi.icu/1/1774938362506-65f5400c-e58c-49e0-a717-5f1df6306c65.png)

The prompt I gave AI was:

```markdown
请先阅读当前仓库中的 ai-guide 导航网站，并为它生成一份高质量的 README.md 项目介绍文档，同时配套生成几张帮助理解和宣传网站的动漫风格图片，保存并在 README 中引用。

请先安装并使用这个 AI 生图技能：npx skills add https://github.com/inferen-sh/skills --skill ai-image-generation。我可以提供 Gemini NanoBanana 的 API Key，请安全使用，不要写入仓库。

AI 生图的风格参考下面的提示词模板：@已经复制的模板
```

After the AI finished the task, it requested an image-generation API Key. We got it from Google AI Studio and sent it to the AI. It handled the key securely and only used it temporarily:

![](https://pic.yupi.icu/1/1774938470660-ee788099-bace-4a0b-8f2b-326de0caf773.png)

The AI agent successfully called the Skill and generated a richly illustrated document:

![](https://pic.yupi.icu/1/1774938669310-fbbb62dd-a10d-4ef7-8ade-4ae3630f33e8.png)

However, this time it accidentally modified the homepage files too. That’s okay—thanks to the PR, we caught the issue, simply chose not to merge it, and asked the AI to fix it by itself.

This is also a good reminder: **even though AI has become very strong at writing code, code review is still extremely important.**

![](https://pic.yupi.icu/1/1774938796668-8b82900c-1f40-44f7-89d3-e4f03af3cea7.png)



## 5. SEO Optimization

After an open-source project is launched, if you want to promote it well, you need to do proper SEO so users can find your site through search engines.

We used a professional SEO Skill to optimize the site:

```markdown
请先阅读当前仓库中的 ai-guide 导航网站，并对它进行一轮高质量的 SEO 优化，直接完善站点的标题、描述、结构化信息、页面语义、链接结构和可索引性。

做法上，请先安装并使用这个 SEO 技能：npx skills add https://github.com/coreyhaines31/marketingskills --skill seo-audit，然后把优化结果直接落实到项目代码中。
```

GitHub Copilot integrates multiple models including Claude, so you can directly launch different AI models in the cloud to complete tasks:

![](https://pic.yupi.icu/1/1774938911290-462333f6-8107-485d-ae36-f1417eff0cc0.png)

And yes, that means using Claude happily right in the web interface:

![](https://pic.yupi.icu/1/1774938853796-04e68bed-2f7d-42cb-9206-0c237f26f288.png)

The AI quickly completed the SEO optimization, making the site easier for search engines to index:

![](https://pic.yupi.icu/1/1774939165853-dc11c5a9-ee7a-4462-8d24-3fd3b4947ebe.png)

As shown below, the webpage ended up with a bunch of additional search keywords:

![](https://pic.yupi.icu/1/1774939208320-445dfdcb-c527-49bf-acf7-e24571e42584.png)

You can see that our AI agent has already become quite skilled at using various Skills. From then on, whenever you start a new conversation, you can directly use the installed Skills and treat GitHub as a secure, isolated “computer space.”



## 6. Develop a Full-Stack Frontend + Backend Project

Since GitHub provides a complete workspace, it can also be used to build full-stack projects that include a backend.

For example, you can enter the following prompt and ask AI to build a “Multimedia Processing Platform” for you:

```markdown
在当前仓库内新开发一个完整可运行的《多媒体处理平台》前后端项目：
- 前端使用 Vue 实现多页面，支持图片、音频和视频的压缩与格式转换
- 后端使用 Python + SQLite + FFmpeg 等

请自主完成项目的前后端开发、联调、依赖配置、示例数据、必要文档和本地运行方式，并主动进行测试验证，确保图片、音频和视频的压缩与格式转换流程都能实际可用。

除非确实必要，否则不要中途停下来向我确认，直接持续推进到可运行状态。
```

AI will complete the full process on its own: environment setup, frontend and backend development, automated testing, and documentation generation.

![](https://pic.yupi.icu/1/1774939363314-a5d0a2ae-6cc8-43f2-b7d2-85e8a491cfe4.png)

And remember: all of this is executed in the cloud. Even if you close the webpage, disconnect from the internet, or shut down your computer, it won’t affect the AI continuing its work.

![](https://pic.yupi.icu/1/1774939462978-9bc438e5-22d2-4d30-9d5b-3d8dd24bfa22.png)



## 7. Testing and Verification

Projects with a backend still need proper testing. There are two ways to access and test them.



### Take Over Locally for Testing

After development is complete, you can click “Open in VS Code” in the AI’s conversation window, or use Copilot CLI to take over the project locally:

![](https://pic.yupi.icu/1/image-20260423163857167.png)

After VS Code takes over the project, it automatically clones the repository locally and opens it.

Then you can ask AI to run the project for you:

```markdown
帮我运行这个项目的前后端
```

It will automatically create a Python virtual environment, and ask for your approval at key steps (such as installing dependencies and running commands), which makes it very safe:

![](https://pic.yupi.icu/1/1774939577513-adc4908e-bd05-43a4-834d-efad1f629026.png)

Then you can manually open the browser to test it, and if there are problems, just let the AI fix them.

![](https://pic.yupi.icu/1/1774939621027-32a61479-57ec-4022-b090-a5fba6d92a5b.png)



### Run and Test Online

If you don’t want to open a local IDE, you can also use GitHub Codespaces.

Codespaces is GitHub’s cloud development environment. You can directly edit code and run projects in the browser, and the experience is almost identical to local VS Code.

![](https://pic.yupi.icu/1/image-20260423163948284.png)

First, you need to have AI create the configuration needed for Codespaces so that the environment automatically initializes itself and runs the project after it’s created:

```markdown
请继续为这个项目补全 GitHub Codespaces 开发环境配置，创建 .devcontainer/ 相关文件，使其适配这个前后端项目，并确保在创建 Codespace 后能够自动安装前后端依赖、安装 FFmpeg、初始化必要环境、自动启动 Vue 前端与 Python 后端，并正确转发访问端口。
```

![](https://pic.yupi.icu/1/1774939729545-f819f0c7-1e67-45bf-bb74-2716aa60f694.png)

AI created the required configuration files:

![](https://pic.yupi.icu/1/1774939782308-e572175e-b55e-4934-8273-00e617db2cef.png)

Then create a Codespace on GitHub:

![](https://pic.yupi.icu/1/image-20260423164046377.png)

After it’s created, under normal circumstances you can directly access the frontend and backend (note that the frontend’s backend request URL may need adjustment):

![](https://pic.yupi.icu/1/1774939972660-85faf67a-ec86-4bb4-be10-a533fe2432de.png)

If you still can’t access it, you can open the Codespace terminal and manually run the startup script (making sure the script path is correct):

![](https://pic.yupi.icu/1/1774939912870-37b0f3dc-354b-4aef-ac68-58bc21e85513.png)

See? Doesn’t this interface look exactly like local VS Code? And you can also use Copilot directly in the web version.



## 8. Code Review

Code review is a crucial part of ensuring code quality. GitHub Copilot provides both automatic and manual review workflows.



### Automatic Code Review

Code written by the Copilot coding agent will automatically go through one round of code review by default:

![](https://pic.yupi.icu/1/1774921510223-3b174e66-582c-4a50-a663-a686d4d0cefb.png)

At the same time, it also automatically runs security checks:

![](https://pic.yupi.icu/1/1774921537750-a468dece-3396-4d8c-8753-06b0fbb61054.png)

In addition, you can enable automatic review for all PRs in the repository settings.

![](https://pic.yupi.icu/1/1774925532564-80308560-a96c-41b8-9a02-80a21fcda515.png)

You can think of Copilot as your “coworker.” As long as you add it as a Reviewer, review will be triggered automatically:

![](https://pic.yupi.icu/1/1774925617582-16064bd0-af9e-4684-ae16-0acc54570b3d.png)

The review results also support quick fixes. You can directly accept its suggestions and commit them with one click. You can also use custom instructions to adjust what the review focuses on:

![](https://pic.yupi.icu/1/1774940063359-5b4cc05e-d016-4c0c-83df-ab3b95ca35cf.png)



### Manual Code Review

Again, just treat GitHub Copilot like a coworker. If you set it as a Reviewer in a PR, it triggers code review:

![](https://pic.yupi.icu/1/1774940168717-5cae3ea3-3868-4bf1-900c-e98bdfeb1373.png)

You can also directly `@copilot` in a PR comment—for example, to ask it to restore a port number to its original value.

This approach is more suitable when you want Copilot to directly modify code or fix bugs based on review feedback:

![](https://pic.yupi.icu/1/1774940212269-3c0f640b-b461-4992-8a8b-4355a5ae0b51.png)



## 9. Handle Issues

When maintaining an open-source project, handling user-submitted Issues is unavoidable, and it takes a lot of time. That means it’s a great candidate for automation by an AI agent.



### Handle Issues Manually

GitHub officially supports letting the Copilot coding agent take over an Issue, automatically create a PR, and fix it.

The operation is simple: open an Issue and assign it to Copilot.

![](https://pic.yupi.icu/1/1774940337943-ba0b6ed8-872f-4745-b934-64d4f0fbb14b.png)

Copilot will automatically create a PR:

![](https://pic.yupi.icu/1/1774940372286-4be19b2d-2d7d-4860-afef-4f3314321c48.png)

At the same time, it creates a working session to analyze and fix the Issue:

![](https://pic.yupi.icu/1/1774940395478-6e05f7f7-f5ea-4c9b-bbf3-912bfe585612.png)



### Auto-Reply to Issues + Auto-Fix Bugs

You can also have AI fully automate both Issue replies and bug fixing.

Using GitHub Actions automation, all we need is to add one workflow for “automatic task dispatch.”

Give AI a prompt like this:

```markdown
为当前仓库创建一套 Issue 自动化处理工作流：当有新的 Issue 创建时，先自动回复一条简洁的确认与补充信息提示；如果该 Issue 被识别为 bug（比如带有 bug 标签或满足明确的 bug 条件），则自动将该 Issue 分配给 GitHub Copilot coding agent 处理，并让 Copilot 后续自动开 PR 修复。

请直接完成所需的 GitHub Actions 工作流、必要配置和说明，优先采用简洁、稳定的实现方式。
```

![](https://pic.yupi.icu/1/1774940470510-d1d080c2-1b43-40f8-a4c8-da6b99baceba.png)

However, it’s worth noting that auto-generated scripts can still have problems. For example, the workflow might post a reply saying the issue was assigned, but not actually assign it to Copilot for fixing:

![](https://pic.yupi.icu/1/1774940518174-d623cbc5-ae7a-4258-babc-34fb7d42d6db.png)

When that happens, you can ask AI to fix the workflow according to the official docs. A good prompt looks like this:

```markdown
请修复当前仓库中 Issue 自动化工作流的 Copilot 分配逻辑。现在工作流虽然会自动评论"已分配给 Copilot"，但实际上并没有真正成功分配。

请参考 GitHub 官方对 Copilot coding agent 的 Issue API 分配方式，改成正确可用的实现：使用正确的 Copilot assignee copilot-swe-agent[bot]、必要的 agent_assignment 参数，并且只有在真实确认分配成功后才发表评论；如果分配失败，也要给出明确、真实的失败提示，不要误报成功。

另外，请顺手优化这个工作流的结构：opened 事件只负责自动回复，labeled + bug 事件只负责分配给 Copilot，保证整体逻辑更清晰稳定。
```

![](https://pic.yupi.icu/1/1774940559765-faff3598-81bb-4a7d-a4fd-e9a0024644a8.png)

Also, this requires a user-level Personal Access Token (PAT). The default `GITHUB_TOKEN` won’t work.

First, create a PAT on GitHub and grant the corresponding repository permissions:

![](https://pic.yupi.icu/1/1774940613065-a66b1fc9-09cf-47ad-ad5e-57dd4618490c.png)

Then store the token in the repository’s Secrets and reference it in the workflow via `secrets.COPILOT_ASSIGN_TOKEN`:

![](https://pic.yupi.icu/1/1774940688587-7e6f019d-9df1-4af5-b808-233ee3ec15ee.png)

An example snippet for referencing the token is as follows:

```yaml
  - name: Assign issue to Copilot coding agent
    uses: actions/github-script@v7
    with:
      github-token: ${{ secrets.COPILOT_ASSIGN_TOKEN }}
      script: |
```

Then all I need to do is create an Issue labeled `bug`, and GitHub Actions will trigger and automatically assign the bug to AI for handling:

![](https://pic.yupi.icu/1/1774940722288-25f2ee1e-d20d-46c5-869a-bee8fcb69d00.png)



## 10. Scheduled Tasks

One of OpenClaw’s standout capabilities is running scheduled tasks, so our “GitHub lobster” should have that too!

But a GitHub repository isn’t a computer that stays running permanently, so how can we implement scheduled tasks?

I had an idea: use the `schedule` trigger in GitHub Actions to give the AI agent a kind of “scheduled wake-up” capability.

For example, let it automatically push the latest AI tech highlights every day:

```markdown
为当前仓库创建一个可长期使用的定时任务工作流，利用 GitHub Actions 模拟 OpenClaw 风格的定时触发能力。

目标：每天北京时间中午 13 点，自动收集并总结本周最新的 AI 科技热点，并以 "推送日报" 的形式发送给我。

优先采用简单稳定的实现方式：默认先推送到 GitHub Issue；如果仓库中已有邮箱等其他 webhook 配置，也可以优先复用。
```

Of course, you can also choose to connect more third-party channels such as email or Telegram:

![](https://pic.yupi.icu/1/1774940782165-e1ce8ae7-2ab1-4982-a48c-1e9c5791db3b.png)

Task complete—the scheduled GitHub workflow was created:

![](https://pic.yupi.icu/1/1774940824191-a0b449e3-d16f-4784-9894-2b2835361853.png)

From then on, it automatically generates a daily AI tech digest every day:

![](https://pic.yupi.icu/1/1774940877163-c8368494-3a99-45d4-a98b-7cfb7ed6e12a.png)

One thing to keep in mind: GitHub Actions `schedule` triggers can be delayed. The official documentation also mentions that under high-load periods (especially at the top of the hour), jobs may be delayed or even skipped, so it’s not suitable for use cases that require precise timing.



## 11. Package the AI Agent

By this point, our AI little lobster has grown quite fat. It has a role, memory, skills, and automation pipelines. So why not package it up and share it with others?

So I gave Copilot this prompt and asked it to package everything into an Agent Skill:

```markdown
请把当前仓库里已经实现的所有 "把 GitHub Copilot 变成小龙虾" 的能力，系统化封装成一个可复用的 agent skill，名称为 github-claw，并放到仓库的 skills/github-claw/ 目录下。

在开始之前，请先参考 anthropics/skills 仓库中的 skill-creator 结构与规范，按规范创建完整技能文件，而不是只写一个简单的 SKILL.md：
https://github.com/anthropics/skills/tree/main/skills/skill-creator

这个 github-claw skill 的目标是：让其他用户只要安装这个技能，就能尽可能快速地把 GitHub Copilot 仓库工作流变成一个 OpenClaw 风格的小龙虾系统，具备并串联以下能力：
- 角色与人格
- 文件化记忆与长期上下文
- 技能发现、安装与管理
- 定时任务 / GitHub Actions 自动化
- Issue 自动回复与自动分配给 Copilot
- PR 审查与自动化工作流
- 编码开发、部署、网站生成与项目推进
```

![](https://pic.yupi.icu/1/1774941001296-f6cfe046-91a8-477f-814e-944c4ce5ca10.png)

The packaged `github-claw` Skill was placed into a clean standalone branch:

![](https://pic.yupi.icu/1/1774941046143-f9f04ebf-6c68-41f1-b037-6f9b6f50cae2.png)

That way, in the future, anyone can create a new GitHub repository, install this Skill, and immediately have their own AI little lobster.

> GitHub Claw project open source: https://github.com/liyupi/github-claw

![](https://pic.yupi.icu/1/1774941138078-6a086446-9193-4b43-9847-9232401f9854.png)



## Summary

And that’s it—we built our own AI agent using GitHub’s web interface without ever opening an IDE.

You can use it to complete the full workflow from requirement analysis to full-stack development, testing, documentation, deployment, SEO optimization, code review, automatic Issue handling, and scheduled tasks.

And because GitHub Copilot is deeply integrated into the web, all of the tasks above can also be done from a phone using GitHub’s web interface or the GitHub Mobile App, so you can use it anytime and anywhere.

![](https://pic.yupi.icu/1/image-20260423165139146.png)

Copilot’s advantages are:

1) Fully cloud-based execution: the Copilot coding agent works independently in temporary environments supported by GitHub Actions, making it very safe. You can close the webpage or even shut down your computer, and AI will keep working.

2) End-to-end delivery capability: GitHub Copilot can span the entire development lifecycle—from writing code to PR review to deployment—all within the GitHub ecosystem.

3) Flexible multi-model choice: GitHub provides multiple models to choose from, so you can match the right model to the right task and save cost.

![](https://pic.yupi.icu/1/image-20260423165247440.png)



## More GitHub Copilot Capabilities

Besides the core workflow demonstrated today, GitHub Copilot has many more capabilities worth exploring:

1) Coding Agent MCP configuration: in repository settings, you can configure Copilot’s permissions, tools, and MCP servers (for example, connecting Context7, Firecrawl, and more), expanding Copilot’s external data access and operational abilities.

2) GitHub built-in Memory: Copilot can automatically store useful information it infers while working in the repository, forming persistent repository-level memory. In later work inside that same repository, it can automatically reuse those memories, and the effect improves the more you use it. This is currently in Public Preview.

3) Copilot Spaces: a shared context space where you can aggregate code, documentation, design drafts, and other resources into one Space, so Copilot can always answer and work based on the correct context. It’s especially suitable for team collaboration.

4) GitHub Spark: by describing your idea in natural language, Spark can generate a full-stack web app prototype in seconds, with real-time preview and one-click deployment to Azure, without writing code. You can also create a GitHub repository from Spark and keep the two synchronized in both directions.

5) GitHub Copilot CLI: this is a standalone command-line AI tool that can read code, edit files, execute commands, create PRs, and even delegate tasks to specialized Agents. It also supports remote session resume, so you can keep working in any terminal.

Besides the web version that I focused on above, the desktop version of GitHub Copilot (for example, the VS Code IDE plugin version) is also extremely useful. It lets you switch flexibly between multiple large models, integrates web search and other mainstream tools, and supports MCP and Skills. I often use it myself to build complete projects with everyone.

For example, my AI hot-topic monitoring tool project was developed entirely with GitHub Copilot inside an IDE.

![](https://pic.yupi.icu/1/image-20260423165402802.png)

If you want to systematically learn how to use GitHub Copilot, you can read *AI IDE Plugins* in the Programming Tools section of this tutorial, as well as *VSCode + GitHub Copilot: Microsoft’s All-in-One AI Coding Practice* in the Hands-on Tools section of the same chapter.



## Recommended Resources

1) Yupi’s AI Navigation site: [A complete collection of AI resources, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussions and Q&A](https://www.codefather.cn)

3) Programmer interview cheat sheet: [High-frequency topics for internships / campus hiring / experienced hiring, plus real interview question analysis](https://www.mianshiya.com)

4) Resume builder for programmers: [Professional templates, rich example phrases, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [A must-have for landing offers in internships / campus hiring / experienced hiring](https://ai.mianshiya.com)
