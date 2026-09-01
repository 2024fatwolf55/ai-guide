# Use CLAUDE.md Well and Double Your AI Programming Efficiency!

> One Markdown file that lets AI automatically understand your project

Hello everyone, I’m programmer Yupi.

Recently I’ve noticed something: a lot of people have started using AI programming tools like Claude Code and Cursor, but after using them for a while, they begin to complain: why is AI always so disobedient? You ask it to fix one bug and it introduces three more. You ask it to add a feature and it swaps out your whole tech stack.

![](https://pic.yupi.icu/1/image-20260622164228939.png)

The root cause of these problems usually isn’t that AI is stupid—it’s that you didn’t give it enough context.

Every time AI starts a new session, it begins as a blank sheet. It doesn’t know your project’s tech stack, your team’s coding conventions, or the decisions you made earlier.

If you don’t tell it, it guesses. If it guesses right, you got lucky. If it guesses wrong, you get rework, your tokens disappear, and your memories turn to dust~

So is there a way to let AI automatically understand your project before it starts working each time?

Absolutely. That’s exactly what today’s topic is about: **CLAUDE.md**.

![](https://pic.yupi.icu/1/image-20260320152009626.png)



## 1. What Is CLAUDE.md?

`CLAUDE.md` is a Markdown file in Claude Code that lives in the project root directory.

Every time Claude Code starts a session, it automatically reads this file and treats its contents as background knowledge about the project.

You can think of it as **an onboarding handbook written for AI**. Just like when a new employee joins on day one, you’d give them a document explaining what technologies the company uses, how code should be written, how tests are run, and what pitfalls to watch out for. That’s exactly what `CLAUDE.md` does.

![](https://pic.yupi.icu/1/01_CLAUDE.md%E6%98%AFAI%E7%9A%84%E5%85%A5%E8%81%8C%E6%89%8B%E5%86%8C_compressed_v1.png)

For example, the simplest `CLAUDE.md` might look like this:

```markdown
# 我的博客系统

Next.js 16 + TypeScript + Tailwind CSS + Supabase

## 常用命令
- npm run dev        # 启动开发服务器
- npm run test       # 跑测试
- npm run build      # 生产构建

## 代码规范
- 使用函数式组件，不用 class 组件
- 样式只用 Tailwind CSS，不写自定义 CSS
- 所有组件必须有 TypeScript 类型定义
```

AI reads it before every work session, and all generated code will automatically follow these conventions, so you don’t need to repeat them every time.

But one thing is important: to AI, `CLAUDE.md` is **advice**, not an **enforced configuration**. Its effectiveness depends on how specific and concise you write it. The more precise the instructions, the better AI will follow them. If you write a big pile of vague requirements, AI may selectively ignore them.



## 2. The More Universal `AGENTS.md`

You might be thinking: is this a Claude Code-only feature? What if I use Cursor?

In fact, almost all mainstream AI programming tools have a similar mechanism. For example, Cursor also supports `.cursor/rules/` and `AGENTS.md` for the same purpose.

What you absolutely need to know is `AGENTS.md`. It is an open cross-tool standard jointly introduced by OpenAI, Google, Cursor, and others. It is already used by tens of thousands of open-source projects and supported by more than 30 AI programming tools.

![](https://pic.yupi.icu/1/image-20260622190311465.png)

Although Claude Code only reads `CLAUDE.md` by default, you can import `AGENTS.md` into it using a single line like `@AGENTS.md`, which makes the two work together.

At their core, all of these Markdown files are the same thing: **a project manual written for AI**. Once you learn how to write this manual well, you can use the skill with any AI programming tool.

And `AGENTS.md` isn’t limited to project development guidance. It can also serve as a workflow document for guiding AI to do work. For example, I personally use `AGENTS.md` to define various workflows such as image-and-text content creation, product customer service, and data analysis. A single Markdown file can lock in how AI should work and be auto-loaded every time, saving you from repeating yourself.

Below I’ll use `CLAUDE.md` as the main term, but the techniques apply to all tools.



## 3. Why Must This File Be Written Well?

You might think: isn’t it just a config file? Can’t I just write something casually?

Absolutely not! The quality of your `CLAUDE.md` directly determines how efficiently and accurately AI can help you work.

From my own everyday experience using AI for programming, a good `CLAUDE.md` solves at least three problems:

**First, it reduces repeated communication.**

Without `CLAUDE.md`, I have to repeatedly explain the tech stack, coding conventions, and project structure every time I start a new session. With it, AI already knows all of that automatically.

**Second, it improves code consistency.**

Previously, AI would sometimes use React functional components and sometimes randomly give me class components. Sometimes it used CSS Modules, sometimes inline styles. Once I wrote the conventions into `CLAUDE.md`, those problems basically disappeared.

**Third, it reduces error rates.**

For example, one of my projects has a special API response format: `{ success, data, error }`. If I don’t write that into the rules, AI uses whatever format it feels like each time. Once it’s written in, Claude follows it automatically and I no longer need to correct it every time.

![](https://pic.yupi.icu/1/03_%E6%B2%A1%E6%9C%89vs%E6%9C%89CLAUDE.md%E7%9A%84%E5%AF%B9%E6%AF%94_compressed_v1.png)

I mentioned in another article that when a rules file is around 50 lines long, compliance can reach 94%. But if you dump everything into a 400-line monster, compliance falls to 71%.

**So `CLAUDE.md` is not better when it’s longer—it has to be precise.**

That leads us to the core topic of this article: how do you write `CLAUDE.md` well?



## 4. How to Write CLAUDE.md Well?

The following tips are drawn from lots of community practice and my own verification. I suggest reading them carefully and really thinking them through.



### 1. Keep It Within 200 Lines

This is the recommendation given in the official Claude Code docs.

The contents of `CLAUDE.md` are loaded into AI’s context window every time a session starts. That window is limited. The longer your rules file is, the less room remains for the actual work.

Also, AI’s ability to follow instructions is negatively correlated with the number of instructions. Some people in the community cited research suggesting that AI can reasonably follow around 150 to 200 instructions. Beyond that, compliance quality declines evenly—not just for the newly added ones, but across the board.

**So writing `CLAUDE.md` should be like writing a resume: refine it again and again.**

![](https://pic.yupi.icu/1/08_%E6%8C%87%E4%BB%A4%E6%95%B0%E9%87%8Fvs%E9%81%B5%E5%BE%AA%E7%8E%87%E6%9B%B2%E7%BA%BF_compressed_v3.png)

For every single line, ask yourself one question: if I delete this line, will AI make mistakes?

If the answer is no, delete it without hesitation.



### 2. Only Write Things AI Can’t Guess

The official documentation even provides a list of what should and shouldn’t go into `CLAUDE.md`, and it’s extremely worth referencing.

Things that should go in:

- build and test commands AI cannot possibly guess  
- code style rules that differ from defaults  
- the team’s Git conventions (branch naming, PR format)  
- project-specific architectural decisions  
- special development environment requirements (such as required environment variables)  
- places where it’s easy to fall into pitfalls

Things that should not go in:

- things AI can already infer by reading the code  
- general language conventions (AI already knows these)  
- detailed API documentation (put it elsewhere and only link to it from `CLAUDE.md`)  
- fluff like “write clean code” or “pay attention to performance”

![](https://pic.yupi.icu/1/09_%E8%AF%A5%E5%86%99vs%E4%B8%8D%E8%AF%A5%E5%86%99%E5%88%86%E7%B1%BB%E7%AD%9B%E9%80%89%E5%9B%BE_compressed_v2.png)

For example, when I worked on the Programming Navigation project, I wrote into `CLAUDE.md` some conventions that are easy to miss even if you read the code, such as always wrapping API responses with `BaseResponse` and always throwing exceptions through `BusinessException`. AI could theoretically infer these patterns through deep code analysis, but writing them into the rules saves it from having to rediscover them each time, which is much more efficient.



### 3. Use Positive Instructions Instead of Negative Ones

This tip is a little counterintuitive.

There’s research showing that 87.5% of AI rule violations come from the same cause: negative phrasing actually activates the prohibited concept. If you write “do not use semicolons,” AI sees the concept of semicolons and becomes more likely to generate them later.

It’s exactly like the white bear effect in psychology. Tell someone not to think about a white bear, and suddenly their whole mind is full of white bears.

So the correct approach is to rephrase instructions positively:

- ❌ Don’t use class components → ✅ Use functional components and Hooks  
- ❌ Don’t use the `any` type → ✅ All variables must have explicit TypeScript types  
- ❌ Don’t commit directly to the main branch → ✅ All changes must be submitted through a feature branch PR

![](https://pic.yupi.icu/1/04_%E7%99%BD%E7%86%8A%E6%95%88%E5%BA%94%E4%B8%8E%E6%AD%A3%E9%9D%A2%E6%8C%87%E4%BB%A4_compressed_v2.png)



### 4. Make Instructions Specific and Verifiable

Vague instructions are basically no instructions at all. AI is very good at handling specific rules, but when you give it abstract requirements, it will improvise on its own.

For example:

- ❌ Format the code correctly → ✅ Use 2-space indentation  
- ❌ Test your changes → ✅ Run `npm test` before submitting  
- ❌ Keep files organized → ✅ Put API handlers under `src/api/handlers/`

The more specific the instruction, the easier it is for AI to know whether it has followed it—and the easier it is to detect when it hasn’t.



### 5. Use Hooks for Enforcement

`CLAUDE.md` is fundamentally just a suggestion, not a 100%-effective prohibition.

For things like code formatting, running tests before committing, or blocking dangerous commands, you should use deterministic automation scripts instead.

Claude Code provides a Hooks mechanism that automatically runs your preset scripts at key points in AI operations.

For example, if you want ESLint to run automatically after every file edit, you can do it with a Hook configuration. AI is not involved at all, so it will execute 100% of the time.

**In one sentence: `CLAUDE.md` gives recommendations, while Hooks enforce actions.**

![](https://pic.yupi.icu/1/05_CLAUDE.md%E5%BB%BA%E8%AE%AEvs_Hooks%E5%BC%BA%E5%88%B6%E6%89%A7%E8%A1%8C_compressed_v3.png)



### 6. Use Path Rules for Large Projects

If your project is large, 200 lines won’t be enough to hold all the conventions. In that case, don’t force everything into `CLAUDE.md`. Instead, split it up using the `.claude/rules/` directory.

Each rule file can use YAML frontmatter to specify that it only applies to files under certain paths:

```yaml
---
paths:
  - "src/api/**/*.ts"
---

# API 开发规范
- 所有 API 端点必须包含输入验证
- 使用标准的错误响应格式
- 添加 OpenAPI 文档注释
```

That way, these rules are only loaded into context when Claude works on TypeScript files under `src/api/`. This saves context space and also prevents unrelated rules from interfering with AI.



### 7. Use `@import` for Progressive Disclosure

One of the most highly praised advanced community techniques is called **progressive disclosure**. The core idea is not to stuff everything into `CLAUDE.md`, but instead tell AI where to find the information it needs.

The method is simple. Create a `docs/` directory in your project, store various topical documents there, and reference them from `CLAUDE.md` using a short description plus a trigger condition:

```markdown
## 参考文档

### API 架构 — @docs/api-architecture.md
何时阅读：添加或修改 API 端点时

### 数据库设计 — @docs/database-design.md
何时阅读：创建或修改数据模型时
```

This way, Claude only reads the relevant document when it actually needs it, instead of occupying context space all the time.

![](https://pic.yupi.icu/1/06_%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8A%AB%E9%9C%B2%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v2.png)

The `@path` import syntax in `CLAUDE.md` supports both relative and absolute paths, and can be nested up to 4 levels deep.

This idea is actually very similar to the context engineering and Agent Skills concepts I discussed before. AI programming tools have limited context windows, so you can’t just shove everything in at once. Anthropic officially calls this strategy **just-in-time**—let AI fetch information on demand instead of loading everything upfront.



### 8. Let AI Help Maintain It

`CLAUDE.md` is not something you write once and forget. It should be a living document that keeps evolving along with the project.

The founder of Claude Code recommends one habit: **every time Claude makes a mistake, don’t just correct the mistake—also ask it to write the correction into `CLAUDE.md`.**

I do the same. For example, if Claude used the wrong import path, after fixing it I simply tell it: update this rule in `CLAUDE.md` so you don’t make the same mistake next time.

Claude is especially good at writing rules for itself. Over time, your `CLAUDE.md` becomes a complete knowledge base for the project, and the error rate drops significantly.

Also, Claude Code now has an **Auto Memory** feature. Claude automatically records patterns and preferences it discovers during work into the `~/.claude/projects/<项目>/memory/` directory. These notes are auto-loaded in future sessions, basically serving as AI’s own memo system.

You can view and edit those memories at any time with the `/memory` command.

![](https://pic.yupi.icu/1/image-20260622182614045.png)



## 5. How Can You Create It Quickly?

At this point, you may be thinking: okay, I understand the techniques, but writing a complete `CLAUDE.md` from scratch still feels a bit painful.

Don’t worry. There are several quick ways to get started.



### Use the `/init` Command to Auto-Generate One

Type `/init` in Claude Code, and Claude will automatically analyze your repository and generate a `CLAUDE.md` containing build commands, test instructions, and project conventions. If the file already exists, it will suggest improvements instead of overwriting it.

![](https://pic.yupi.icu/1/image-20260622182756786.png)

That said, automatically generated content may not be precise enough, because AI can only see the current shape of your code, not the reasoning behind it.

Someone in the community once said that `CLAUDE.md` affects every stage of your workflow and every file it produces, so one bad instruction can be more destructive than one bad line of code. That’s why after auto-generation, you must still review it yourself—delete what should be deleted, and add what should be added.



### Let AI Distill It from Conversations

One method I personally use often is not to rush to write `CLAUDE.md` first. Instead, I collaborate normally with AI on one or two tasks. After that, I ask AI to review the entire conversation, summarize the project conventions and caveats worth remembering, and write them directly into `CLAUDE.md`.

The result is far more precise than trying to imagine everything from scratch, because those rules are distilled from real practice.

When I lead projects with my own team, every time we discover an AI mistake during code review, we ask Claude to append the correction into `CLAUDE.md`. After a month, the file has usually accumulated dozens of highly targeted rules, and new teammates can onboard much faster when using Claude Code.

![](https://pic.yupi.icu/1/10_AI%E7%BA%A0%E9%94%99%E6%B2%89%E6%B7%80%E6%AD%A3%E5%90%91%E5%BE%AA%E7%8E%AF_compressed_v2.png)



### Reference Great Open-Source Projects

There’s a GitHub repository called awesome-claude-md that collects over 100 real `CLAUDE.md` examples from real projects, covering different tech stacks and project types—including Anthropic’s own examples and Cloudflare’s monorepo setup.

There’s also another repository called awesome-claude-code, which organizes ecosystem tools such as Skills, Hooks, and slash commands. That one is worth bookmarking too.

![](https://pic.yupi.icu/1/image-20260622184038586.png)

If you have time, you can even ask AI to help analyze those examples and find one that matches your own tech stack closely. That’s much faster than starting from zero.

**Remember: when it comes to `CLAUDE.md`, less is more.**

Start with the most important 20 lines, and keep adding to it gradually in real use.



## 6. Multi-Level Configuration and Team Collaboration

If you use Claude Code in a team, or work on multiple projects at the same time, there are some more advanced patterns worth knowing.



### Four Levels of Scope

`CLAUDE.md` doesn’t only belong in the project root. It supports four levels, loaded in this order:

1) Organization level: company-wide rules deployed by IT and enforced for everyone  
2) User level: `~/.claude/CLAUDE.md`, which applies to all projects on your machine  
3) Project level: `./CLAUDE.md`, which applies only to the current project and can be committed to Git  
4) Local level: `./CLAUDE.local.md`, which applies only to the current project and is not committed to Git

The later the content is loaded, the more AI tends to prioritize following it. So the precedence is local > project > user. But the organization level is special: even though it is loaded first, it **cannot be excluded by personal or project settings**, making it the company-enforced bottom line.

My recommendation is to put team-shared conventions at the project level, and personal preferences at the local level, so the two don’t interfere with each other.



### Co-Build `CLAUDE.md` as a Team

The founder of Claude Code recommends managing `CLAUDE.md` with Git and maintaining it collaboratively as a team.

Whenever someone discovers an AI mistake during code review, append the correction to `CLAUDE.md`. Over time, the file accumulates the team’s development experience and conventions, becoming the team’s AI usage handbook.

That’s exactly how our own team works too. For example, in the AGENTS.md file for our Mianshiya backend project, we’ve accumulated conventions such as tech stack choices, Spring Boot layering rules, unified response format, exception handling, and database naming standards. New teammates can start much faster by reading that one file, and Claude can automatically follow those rules when generating code, saving a lot of communication cost.

![](https://pic.yupi.icu/1/image-20260622183444669.png)



### Important Rules Must Be Stored in Files

When you use `/compact` in a conversation to compress context, the root `CLAUDE.md` file gets reread and reinjected. But verbal instructions you casually mentioned in the conversation—such as “use async/await in all the code from now on”—will disappear after compression.

So for any rule that truly matters, write it into `CLAUDE.md`. Don’t just say it in the chat. This is the same principle I talked about earlier in context engineering: if information needs to persist, put it in a file instead of relying only on AI’s short-term memory.



## 7. Troubleshooting When It Doesn’t Take Effect

If you feel like AI is not following the rules in `CLAUDE.md`, troubleshoot in this order:

1) Run the `/memory` command to check whether your `CLAUDE.md` has actually been loaded correctly  
2) Check whether the instructions are too vague. For example, “format the code well” is not actionable. Change it to “use 2-space indentation and keep each line under 80 characters”  
3) Check whether different files contain conflicting instructions. If `CLAUDE.md` says to use MyBatis Plus but a rules file says to use MyBatis Flex, AI may arbitrarily choose one  
4) If an action must happen at a specific moment, such as running lint before every commit, then don’t rely on `CLAUDE.md` at all—use Hooks instead

![](https://pic.yupi.icu/1/11_%E8%A7%84%E5%88%99%E4%B8%8D%E7%94%9F%E6%95%88%E6%8E%92%E6%9F%A5%E5%86%B3%E7%AD%96%E6%A0%91_compressed_v1.png)



## Final Words

Surprised? A single Markdown file like this is actually one of the most important pieces of infrastructure in the AI programming era.

In the past, we wrote `README.md` for humans. Now we write `CLAUDE.md` for AI. But the essence is the same: organize the important information about your project and communicate it clearly. The difference is that instructions written for AI must be more concise, more specific, and more executable.

One more piece of good news: the “if I delete this line, will AI make mistakes?” standard I mentioned earlier can now be checked by a tool. Claude Code includes a built-in `/doctor` command that automatically scans your `CLAUDE.md` and Skills, identifies redundant content and conflicting instructions, and points them out. If you want to learn how to use that command, read *Claude Code Common Slash Commands Encyclopedia* in this directory.

If you still haven’t written a `CLAUDE.md` for your own project, you can start right now. Begin with the simplest 20 lines: write down your tech stack, build commands, and the few rules AI keeps getting wrong. You’ll feel its power immediately.
