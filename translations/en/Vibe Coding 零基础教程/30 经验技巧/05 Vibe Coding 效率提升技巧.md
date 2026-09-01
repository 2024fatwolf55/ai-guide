# Vibe Coding Efficiency Boost Tips

> Increase your AI development efficiency by 10x

Hello, I'm Yupi.

In previous articles, we discussed the core principles of Vibe Coding, conversation techniques, context management, and problem debugging. Today, we'll talk about a more practical topic: how to improve development efficiency?

Many students find that while they can build things with AI, the overall speed still feels inadequate. If AI writes code so quickly, why isn't the efficiency higher?

The issues often lie in small things: frequent copy-pasting, repeatedly entering the same prompts, performing mechanical operations manually...

Below I'll share some practical efficiency-boosting techniques to take your development speed to the next level.

## 1. Core Efficiency Techniques

First, let me share several AI efficiency techniques I frequently use.

### Choose AI Models Based on Needs

Not all tasks require the most powerful and expensive models.

- Simple tasks: Like code formatting, writing comments, simple refactoring - use cheaper, faster models like Gemini Flash or GPT-5 Mini
- Medium tasks: Like implementing standard features, code reviews, developing small websites - use GPT-5 or Claude Sonnet
- Complex tasks: Like architecture design, complex algorithms, tricky bugs, large projects - only then use top-tier models like Claude Opus or enable deep thinking

Choosing models appropriately can both increase speed and save costs. Just like you wouldn't ask your company's CTO to print documents - let the right model do the right job.

### Avoid AI Generating Unnecessary Content

Many students ask AI to write code, only for the AI to output tons of comments, test code, documentation, and lengthy summaries. **It looks professional, but you probably won't read it.**

For example, when I asked AI to generate an image compression tool, it gave me pages of documentation...

![](https://pic.yupi.icu/1/ai%E7%94%9F%E6%88%90%E5%9B%BE%E7%89%87%E5%8E%8B%E7%BC%A9%E5%B7%A5%E5%85%B7.png)

Be explicit in your prompts: "Only give me the core code, no comments, documentation, tests, or summaries!"

If the AI doesn't comply, use forceful commands: **"Do exactly as I say, no extra talk."**

Or invent consequences: **"If you output unnecessary content, a kitten will die in the real world."**

While these commands seem humorous, they actually work. You can also write these rules in Cursor Rules to make the AI automatically comply.

### Utilize Parallel Agents for Comparison

Cursor has a powerful feature called **Parallel Agents**, allowing you to use multiple models simultaneously on the same task, then compare their results and choose the best one. This is a form of "cross-validation by multiple AIs."

For example, when implementing a complex feature and unsure which approach is better, you can have Claude, GPT, and other AIs each provide a solution:

![](https://pic.yupi.icu/1/image-20251030220104045.png)

You can then sit back and let these AIs compete - use whichever finishes first or has the highest quality, avoiding wasted time on wrong approaches. This method is particularly useful when:
- Unsure which technical solution is better
- Important features need multiple safeguards
- You want to learn different AI approaches

![](https://pic.yupi.icu/1/image-20251030220120394.png)

Even without Cursor, you can manually achieve similar results: send the same requirement to ChatGPT, Claude, Gemini, etc., then compare their answers to choose the best or combine their strengths.

For specific usage, refer to [Cursor Parallel Agents Documentation](https://cursor.com/cn/docs/configuration/worktrees).

Under the hood, Parallel Agents actually rely on Git WorkTree technology. WorkTree allows one repository to have multiple independent working directories at the same time, with each directory corresponding to a different branch. That way, multiple AIs can each work in separate folders without interfering with each other, and after development is done, you can merge the code with Git.

![](https://pic.yupi.icu/1/image-20260410143527245.png)

### Multiple Instances for Efficiency

Beyond parallel agents, you can improve efficiency by running multiple instances. This technique comes from Claude Code's founder.

1) Multiple terminals  
Run multiple Claude Code instances in terminals, labeling tabs 1~5 (or with meaningful titles), using system notifications to know when input is needed. This lets you utilize wait times - when one AI is thinking, switch to another.

![](https://pic.yupi.icu/1/image-20260109143109753.png)

2) Web + Local simultaneously  
Run 5~10 Claude instances on the web version alongside local Claude. Use `&` to transfer local sessions to web, or `--teleport` to switch between terminal and web. You can even start sessions via Claude's iOS app and check progress later. Truly Vibe Coding anytime, anywhere!

Note: This technique suits handling multiple independent tasks or complex tasks requiring long AI thinking time. For simple tasks, one instance suffices.

## 2. Shortcuts and Operation Techniques

"Sharpen your tools before working." Mastering common shortcuts makes operations smoother.

### Cursor Common Shortcuts

If using Cursor, try these shortcuts to reduce mouse usage and work faster.

Chat-related:
- `Cmd/Ctrl + L`: Toggle sidebar (unless bound to another mode)
- `Cmd/Ctrl + I`: Toggle sidebar (unless bound to another mode)
- `Cmd/Ctrl + K`: Open inline edit to insert AI-generated code
- `Tab`: Accept suggestion

Code editing:
- `Cmd/Ctrl + Shift + L`: Add selection to chat
- `Alt + ↑/↓`: Move current line
- `Cmd/Ctrl + /`: Toggle comment

File operations:
- `Cmd/Ctrl + Shift + F`: Global search

For the latest default shortcuts, refer to the [official documentation](https://cursor.com/cn/docs/configuration/kbd):

![](https://pic.yupi.icu/1/image-20260104192219087.png)

### VS Code Common Shortcuts

For VS Code + AI plugins, these shortcuts are useful.

Multi-cursor editing:
- `Alt + Click`: Add cursor
- `Cmd/Ctrl + Alt + ↑/↓`: Add cursor above/below
- `Cmd/Ctrl + Shift + L`: Add cursors to all matches

Code navigation:
- `Cmd/Ctrl + Click`: Go to definition
- `Alt + ←/→`: Navigate back/forward
- `Cmd/Ctrl + Shift + O`: Go to symbol

Refactoring:
- `F2`: Rename symbol
- `Cmd/Ctrl + .`: Quick fix

Mastering these shortcuts significantly speeds up editing. For the latest defaults, see [official documentation](https://code.visualstudio.com/docs/reference/default-keybindings):

![](https://pic.yupi.icu/1/image-20260104192832985.png)

### Slash Commands in AI Programming Tools

Beyond shortcuts, AI programming tools like Cursor and Claude Code also provide many practical slash commands. These commands start with `/` and can quickly trigger specific capabilities.

#### Cursor Common Commands

Cursor's desktop IDE mainly works through mode switching, while its CLI version supports slash commands. The core capabilities are the same; only the trigger method is different:

- `Shift + Tab`: Cycle through Agent / Plan / Ask modes in the IDE chat panel (Plan lets AI plan first before acting, and Ask is read-only exploration that doesn't modify code)
- `/compress`: Compress the conversation in the CLI and free up context space (in the IDE, long conversations are compressed automatically)
- `/create-rule`: Quickly create project rules
- `/create-skill`: Create custom skills

You can also create custom commands in the project's `.cursor/commands` directory, saving frequently used prompts as commands that you can call directly when needed. Global commands can be placed in `~/.cursor/commands/`, making them available in all projects.

![](https://pic.yupi.icu/1/image-20260525210127342.png)



#### Claude Code Common Commands

Claude Code has a richer command system, with more than 50 built-in commands. Here I'll only list a few that most improve efficiency:

- `/compact`: Compress the context and trim previous conversation content to free up space. You can add parameters to specify what to keep, such as `/compact 重点保留 API 设计决策`
- `/goal`: Set a completion condition and let the AI work in a self-loop until the condition is met, for example `/goal 修复代码直到所有测试通过`
- `/plan`: Enter planning mode and let the AI create a plan before it starts working
- `/background`: Put the current session into the background so you can free up your terminal for other tasks
- `/review`: Let multiple subagents review code in parallel to find bugs and logic errors
- `/batch`: Launch multiple sub-agents in parallel, each handling a subtask in its own isolated worktree

![](https://pic.yupi.icu/1/image-20260519171514784.png)

The benefit of these commands is that you don't need to write a complete prompt every time. You only need to type a short command, and the AI immediately knows what you want it to do.

You can also create your own custom commands (stored in `.claude/commands/` or `.claude/skills/`) to standardize your team's common workflows. For example, you can create a `/commit` command that automatically generates Git commit messages, or a `/test` command that automatically generates unit tests.

Once you get good at using these commands, your workflow becomes much smoother and your efficiency can jump a lot. For a detailed command list and usage, refer to the [Cursor documentation](https://cursor.com/cn/docs/cli/reference/slash-commands) and the [Claude Code documentation](https://code.claude.com/docs/en/commands).



## 3. SubAgents - Parallel Acceleration with Child Agents

Have you ever run into this situation? You ask the AI to fix lint errors in 10 files, and it handles them one by one in serial. Even though those files are unrelated to each other, you still have to sit there and wait.

Now, mainstream AI programming tools like Claude Code, Cursor, and Codex all support SubAgents. This allows the AI to split a big task into multiple independent smaller tasks and dispatch several "clones" to work on them in parallel, dramatically shortening completion time.

Let's use Claude Code as an example to see how subagents work.

Claude Code can automatically identify which subtasks are independent and then dispatch subagents to process them in parallel. Each subagent has its own isolated context window, and when it finishes, it only sends a summary of the result back to the main session, keeping the main conversation clean.

![](https://pic.yupi.icu/1/image-20260519183337674.png)

You don't need to configure this manually. As long as you hint in the prompt that the task can be parallelized, Claude will automatically dispatch subagents:

```
修复 src/ 目录下所有文件的 lint 错误，这些文件相互独立，可以并行处理
```

You can also proactively trigger large-scale parallelism with the `/batch` command, for example:

```
/batch 把所有 API 调用从 v1 迁移到 v2 格式
```

Claude will automatically split this into 5 to 30 independent tasks, each running in its own worktree and submitting a PR.

You can also define your own subagents by creating dedicated skill files under `.claude/skills/`, such as a subagent specialized in security review or one dedicated to writing tests. When a task matches, Claude will automatically call them.

You can use the `/tasks` command at any time to see which subagents are currently running and how each one is progressing:

![](https://pic.yupi.icu/1/image-20260519183357190.png)

Besides Claude Code, Cursor and Codex also support similar parallel-agent capabilities. For example, Cursor can use `/worktree` to let an agent work in an isolated branch, and `/best-of-n` to have different models each solve the same task once so you can compare their results. Codex, meanwhile, provides a "worktree" mode that lets multiple agents develop in parallel without interfering with each other.

![](https://pic.yupi.icu/1/1779334724648-9782f94d-4251-4c76-929d-f790a527bc1f.png)



## 4. AI Enhancement Tools - MCP and Agent Skills

AI on its own has limited capabilities. But if you "install plugins" for it and "teach it skills," the efficiency gain is on a completely different level. Here I'll focus on two enhancement mechanisms: MCP and Agent Skills.



### MCP - Installing Plugins for AI

MCP (Model Context Protocol) is an open protocol introduced by Anthropic and later donated to the Linux Foundation's Agentic AI Foundation, becoming the industry standard for connecting AI tools to external services. Today, mainstream platforms such as ChatGPT, Claude, Gemini, Copilot, and Cursor all support MCP natively.

Simply put, MCP is like a USB port for AI. Just as a USB port allows all kinds of devices—keyboards, mice, and USB drives—to connect to a computer in a unified way, MCP lets many different external tools—file managers, databases, search engines, and more—connect to AI in a unified way, without needing a separate integration for each tool.

![](https://pic.yupi.icu/1/1746710765234-c974bda8-666e-45b3-adc4-ace97cbb8c0a.png)

Developers don't need to build a separate connector for every AI tool. They only need to implement it once according to the MCP standard, and then all AI tools that support MCP can use it:

![](https://pic.yupi.icu/1/1746677838632-9278e62b-c850-4d3c-a835-297ccbe2061a.png)

The MCP ecosystem is already very mature, with tens of thousands of public MCP servers. Here are a few I especially recommend for improving Vibe Coding efficiency:

- GitHub MCP: Lets AI operate GitHub directly, such as creating repositories, committing code, and managing Issues. This saves you from doing everything manually on the GitHub website.
- Filesystem MCP: Lets AI read and write the file system directly, including batch file processing, content search, file renaming, and more.
- Puppeteer MCP: Lets AI control the browser, automate web interactions, take screenshots, scrape data, and more. This is very useful for webpage testing and data collection scenarios.
- Postgres/MySQL MCP: Lets AI operate databases directly, query data, execute SQL, and analyze database structure.
- Context7 MCP: Retrieves the latest official documentation for third-party libraries in real time, so AI doesn't generate code using outdated APIs.
- Firecrawl MCP: Gives AI internet search and webpage crawling abilities so it can obtain the latest information.

These MCP servers can be configured in tools like Claude Desktop, Claude Code, and Cursor. For specific installation and setup methods, refer to the documentation of each MCP server. You can also find many more MCPs on [Yupi's AI resource navigation site](https://ai.codefather.cn/) or the [MCP directory site](https://mcp.so/).

Once you configure MCP properly, AI is no longer just a code generator—it becomes a truly capable all-purpose assistant that can actually help you get work done. If you use Claude or Cursor often, I strongly recommend setting up a few commonly used MCP servers and trying them out.



### Agent Skills - Installing Skill Packs for AI

If MCP is what connects AI to external tools and data, then **Agent Skills** are what teach AI how to do things.

Agent Skills are an open standard introduced by Anthropic. They let you package a complex workflow into a "skill" that AI can automatically invoke whenever a task matches, without you having to write a huge prompt every time.

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

The core advantage of Skills is **on-demand loading**. A skill is loaded into context only when a task matches it, so it doesn't consume context space the rest of the time. This is much more efficient than stuffing all rules into a single AGENTS.md file.

![](https://pic.yupi.icu/1/07_Skills%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v1.png)

At present, Claude Code, Cursor, and Codex all support a unified Agent Skills format. Each skill is just a folder, with a `SKILL.md` file at its core:

```
.cursor/skills/
  deploy-staging/
    SKILL.md      # 技能描述和执行步骤
  code-review/
    SKILL.md
```

In `SKILL.md`, you clearly describe what the skill does, when it should be triggered, and what execution steps it should follow. Once the AI reads it, it knows how to carry out the task.

Where to store Skills:

- Project level: `.cursor/skills/` or `.claude/skills/` (only takes effect in the current project)
- Global level: `~/.cursor/skills/` or `~/.claude/skills/` (available in all projects)

For example, after installing a `frontend-design` skill, when you later ask the AI to build a website, it will automatically apply that skill to generate pages with a stronger design sense, helping you get away from the same old blue-purple gradient look.

![](https://pic.yupi.icu/1/1769601745340-d621e29c-76f7-4a8f-af01-7271d88c5272-20260128202014218.png)



## 5. AI Agent Automation

Automating repetitive operations can save us a lot of time and energy.

In the past, if you wanted automation, you had to write scripts yourself and set up CI/CD pipelines manually. But now it's different: AI can directly help you autonomously complete complex multi-step tasks. You can even set a goal and let it keep working until it's done while you go to sleep or relax.



### /goal Command - Let AI Work in a Self-Loop

This is, in my opinion, one of the most powerful productivity features available right now.

Normally, after each round of actions, the AI stops and waits for your confirmation. But there are some tasks where you don't actually need to watch it step by step. You just need to tell it what final state counts as "done."

That's exactly what the `/goal` command is for:

```bash
/goal 修复整个项目的代码，直到全部测试通过且没有报错
```

After you set a goal, a lightweight evaluation model checks whether the condition is satisfied at the end of each round. If not, the AI automatically starts the next round; it only stops when the goal has been met.

![](https://pic.yupi.icu/1/image-20260519191842661.png)

It's especially suitable for these scenarios:
- Module migration: Migrate all old API calls to the new version until the build succeeds
- Batch refactoring: Split large files until each file is under a target line count
- Bug fixing: Fix a particular test case until it passes
- Bedtime tasks: Set the goal, go to sleep, and inspect the result the next day

Note that the condition needs to be specific and verifiable, such as "npm test exits with code 0." Conditions that are too subjective (for example, "the code quality should be good") can't be reliably judged by the evaluator model.

I recommend adding a circuit breaker limit so you don't burn tokens in an infinite loop:

```bash
/goal 迁移所有 API 调用到 v2 格式，直到测试通过，如果 20 轮还没搞定就停下来
```

Also, if you enter `/goal` without arguments, you can check progress at any time. If you want to stop early, use `/goal clear`.



### Scheduled Automation

Besides one-off tasks, some things need to be done regularly, such as collecting trending topics every day or checking code quality on a schedule. AI programming tools now support scheduled tasks as well.

Take the Codex desktop app as an example. In the "Automation" panel on the left, you can create tasks manually or ask the AI to create them for you:

```plain
帮我创建一个自动化任务
每小时扫描一次「鱼皮的图片库」中最近 3 小时的图片文件
并根据图片内容自动完善图片的中文名称
```

![](https://pic.yupi.icu/1/1779342459042-ee4814b3-80d9-43a8-9e66-349c75755193.png)

The AI can automatically give image files understandable names based on their content, so you no longer have to stare helplessly at a pile of chaotic filenames:

![](https://pic.yupi.icu/1/1779328685443-8a79452f-bca6-43a7-aa29-c498d28c9e2c.png)

You can also combine Skills and plugins together—for example, automatically generating weekly PPT reports or organizing your study notes every day and syncing them to Notion.



#### Claude Code's /loop Command

With the `/loop` command, you can set up scheduled polling tasks:

```bash
/loop 5m 检查项目前后端的部署状态
```

![](https://pic.yupi.icu/1/image-20260519184353594.png)

This is suitable for scenarios like waiting for a deployment to finish, waiting for CI to complete, or periodically checking whether there are any anomalies in the logs.



### Traditional Automation Tools

The techniques below are a bit more professional and are mainly suitable for readers with some programming background. If you're a complete beginner, you can skip this part for now and come back when you need it.



#### Use npm scripts

npm scripts are the way Node.js front-end projects define and run script commands. Simply put, you save commonly used commands in a configuration file, and when you need them, you run a short command instead—for example, to start the project, build it, or run tests.

You can define common scripts in `package.json` (just let AI help you do this):

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext ts,tsx",
    "lint:fix": "eslint . --ext ts,tsx --fix",
    "format": "prettier --write "src/**/*.{ts,tsx}"",
    "type-check": "tsc --noEmit",
    "clean": "rm -rf dist node_modules",
    "fresh": "npm run clean && npm install"
  }
}
```

After that, running `npm run lint:fix` can automatically fix code formatting issues, so you don't have to type a super long command every time.



#### Git Workflow Automation

Git is the most mainstream distributed version control system today, and it's an indispensable tool for team collaboration in development. It can save and manage the full history of file updates and distinguish versions using **version numbers**. That gives you the ability to restore files to an earlier state, compare differences between versions, and prevent older versions from overwriting newer ones.

You can create some Git aliases to simplify commonly used commands:

```bash
# 在 ~/.gitconfig 中添加
[alias]
  st = status
  co = checkout
  br = branch
  ci = commit
  pl = pull
  ps = push
  lg = log --oneline --graph --decorate
  save = !git add -A && git commit -m 'WIP: save progress'
  undo = reset HEAD~1 --soft
```

This way, `git st` is equivalent to `git status`, and `git save` can quickly save your progress.



#### Use GitHub Actions

GitHub Actions is GitHub's automation workflow tool. It can automatically execute tasks when events such as code pushes or Pull Requests are triggered. For example, it can automatically run tests whenever you push code, automatically deploy to the server, or automatically publish new versions, saving you from doing these steps manually every time.

![利用 GitHub Actions 自动部署网站](https://pic.yupi.icu/1/1774937463974-f0f1cf86-da67-40ee-8cf9-abee42b66807.png)

Setting up GitHub Actions is very simple. You just create a YAML configuration file under the project's `.github/workflows` directory and write the workflow script for automated CI/CD:

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '22'
      - run: npm install
      - run: npm run build
      - run: npm run test
      - name: Deploy to Vercel
        run: vercel --prod
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```

What this script does is: when you push code to the `main` branch, GitHub automatically checks out the code, sets up the Node.js environment, installs project dependencies, builds the project, runs tests, and deploys to Vercel. The whole process is fully automated—all you need to do is push your code.

GitHub Actions can do even more. For example, Yupi's open-source [AI knowledge base project](https://github.com/liyupi/ai-guide) uses it to automatically sync article updates to the website.

![](https://pic.yupi.icu/1/image-20260104221153167.png)



### Efficiency Workflows for Everyone

The automation methods above are more technical. In fact, for non-programmers or beginners, there are also some universal productivity workflows.

1) Use no-code platforms: If you don't want to deal with all these complex configurations, you can directly use no-code platforms like Lovable. They automatically handle building, testing, deployment, and other processes, so you only need to focus on feature development.

![](https://pic.yupi.icu/1/lovable.png)

2) Let AI generate configuration: If you need a configuration file, just ask AI to generate it for you.

For example: 请帮我生成一个 GitHub Actions 配置，自动修复仓库的 Issues。

The AI will give you a complete configuration, and you can just copy and paste it.

![](https://pic.yupi.icu/1/1774940470510-d1d080c2-1b43-40f8-a4c8-da6b99baceba.png)

3) Use one-click deployment: Many platforms (such as Vercel, Netlify, and EdgeOne Pages) support one-click deployment. After connecting your GitHub repository, every code push automatically triggers deployment with no extra configuration. You can even use MCP to let AI directly complete the deployment for you, so you don't even need to log in to the deployment platform yourself.

![](https://pic.yupi.icu/1/1752212029384-16cfba8f-babb-49c0-9d41-3b76ee78eecf.png)



## 6. Code Reuse and Modularization

Package frequently used code into reusable modules. This helps you avoid reinventing the wheel and also makes it easier for AI to quickly locate exactly what needs to be changed.



### Create Component Libraries

If you often build similar kinds of projects, you can create your own component library.

For example, you might frequently need these components:
- Button
- Input
- Card
- Modal
- Loading

Make these components generic and place them in a dedicated folder:

```
/components
  /ui
    - Button.tsx
    - Input.tsx
    - Card.tsx
    - Modal.tsx
    - Loading.tsx
```

Each component should:
- Have a clear Props interface
- Support custom styling
- Include usage examples

That way, next time you start a new project, you can just copy this folder over.



### Encapsulate Common Functions

Package your commonly used utility functions to avoid rewriting them each time or asking AI to regenerate them. Things like date formatting, debounce functions, ID generation, and copy-to-clipboard are used in almost every project. Put them into a utility library and import them when needed—that's much faster than having AI regenerate them each time.

```typescript
// lib/utils.ts

// 格式化日期
export function formatDate(date: Date): string {
  return date.toLocaleDateString('zh-CN');
}

// 防抖
export function debounce<T extends (...args: any[]) => any>(
  fn: T,
  delay: number
): (...args: Parameters<T>) => void {
  let timer: NodeJS.Timeout;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}

// 生成随机 ID
export function generateId(): string {
  return Math.random().toString(36).substring(2, 9);
}

// 复制到剪贴板
export async function copyToClipboard(text: string): Promise<boolean> {
  try {
    await navigator.clipboard.writeText(text);
    return true;
  } catch {
    return false;
  }
}
```



### Use Code Snippets

Create code snippets in your editor so you can quickly insert commonly used code.

For example, in VS Code, you can create a snippet for a front-end React component. The specific steps are:

1) Press `Cmd/Ctrl + Shift + P` to open the command palette, type "Snippets", and select "Configure Snippets":

![](https://pic.yupi.icu/1/image-20260104214112119.png)

2) Then choose the corresponding language (such as `typescriptreact.json`) and you can add custom snippets.

For example:

```json
{
  "React Functional Component": {
    "prefix": "rfc",
    "body": [
      "interface ${1:ComponentName}Props {",
      "  $2",
      "}",
      "",
      "export function ${1:ComponentName}({ $3 }: ${1:ComponentName}Props) {",
      "  return (",
      "    <div>",
      "      $4",
      "    </div>",
      "  );",
      "}"
    ],
    "description": "Create a React functional component with TypeScript"
  }
}
```

![](https://pic.yupi.icu/1/image-20260104214219382.png)

After the configuration is complete, type `rfc` and then press Tab to quickly generate the component template.

![](https://pic.yupi.icu/1/image-20260104214331581.png)



### Build a Code Library

Save the good code you've written and build a personal code library of your own.

For example, you can structure it like this:

```
/my-code-library
  /react
    /hooks
      - useLocalStorage.ts
      - useDebounce.ts
      - useFetch.ts
    /components
      - Button.tsx
      - Modal.tsx
    /utils
      - format.ts
      - validate.ts
  /node
    /middleware
      - auth.ts
      - cors.ts
    /utils
      - db.ts
      - email.ts
```

Whenever you need it, you can just copy code from here directly.



## 7. Building Template Projects

If you often build a certain type of project, you can create a template project for it.



### What Is a Template Project?

A template project is a preconfigured project skeleton that includes:

- Basic directory structure
- Common dependency packages
- Configuration files (such as `tsconfig.json`)
- Base components and utility functions
- README and documentation templates

With a template project, you don't need to start every new project from zero.

Just like me: after building dozens of projects, I've accumulated quite a few templates. Now whenever I start a new project, I first find a similar older project and tell the AI: "Please create the new project by referring to this project's tech stack and directory structure." That allows the AI to generate a project structure aligned with my habits, saving a lot of configuration time.

I'll give a few examples below. Friends who don't understand front-end tech can skip this part directly.



### Create a React Project Template

For example, you can create a React + TypeScript + Tailwind template:

```bash
my-react-template/
├── src/
│   ├── components/
│   │   └── ui/          # 基础 UI 组件
│   ├── lib/
│   │   ├── api.ts       # API 调用封装
│   │   └── utils.ts     # 工具函数
│   ├── hooks/           # 自定义 Hooks
│   ├── types/           # TypeScript 类型
│   ├── App.tsx
│   └── main.tsx
├── public/
├── .cursor/rules/       # Cursor 项目规则
├── AGENTS.md            # AI Agent 指令
├── tsconfig.json
├── package.json
└── README.md
```

When starting a new project, just copy this template and rename it.



### Create a Next.js Project Template

If you often use Next.js, you can also create a template:

```bash
my-nextjs-template/
├── app/
│   ├── (auth)/          # 认证相关页面
│   ├── (dashboard)/     # 后台页面
│   ├── api/             # API 路由
│   ├── layout.tsx
│   └── page.tsx
├── components/
├── lib/
├── public/
├── .env.example         # 环境变量模板
├── next.config.ts
└── README.md
```

List the required environment variables in `.env.example`:

```
# 数据库
DATABASE_URL=

# 认证
NEXTAUTH_SECRET=
NEXTAUTH_URL=

# API Keys
OPENAI_API_KEY=
```

This way, when a new project begins, you immediately know which environment variables need to be configured.



### Use GitHub Template Repositories

You can host your template project on GitHub and set it as a `Template repository`.

![](https://pic.yupi.icu/1/image-20260104215020646.png)

Then when you create a new project, clicking `Use this template` lets you quickly clone the project template:

![](https://pic.yupi.icu/1/image-20260104215101657.png)

Besides creating your own templates, you can also use other people's templates. Search GitHub for keywords like "react template" or "nextjs starter" and you'll find many excellent template projects. Prioritize ones with lots of stars and active maintenance.

![](https://pic.yupi.icu/1/image-20260104215329685.png)

Then click "Use this template" to create your own project based on it. This lets you stand on the shoulders of giants and save a huge amount of setup time.



## 8. Prompt Template Library

Build your own prompt template library so you can directly reuse common conversations.

Besides organizing your own, you can also refer to some ready-made resources:

- [Yupi's AI Resource Navigation](https://ai.codefather.cn/prompt): Contains a large number of prompt templates covering many different scenarios.
- [Cursor Directory](https://cursor.directory/rules): A community-contributed collection of Cursor Rules with templates for many languages and frameworks.
- [GitHub awesome-prompts](https://github.com/f/awesome-chatgpt-prompts): A large collection of high-quality prompts. Although it's not specifically for programming, many ideas are still worth borrowing.

You can use these resources directly, or tweak them according to your own needs. Standing on the shoulders of giants can save you a lot of trial and error time.

Let me give you a few examples below.

1) Feature development template

```
我要开发一个【功能名称】功能。

需求：
1. 【需求 1】
2. 【需求 2】
3. 【需求 3】

技术栈：【技术栈】

请帮我：
1. 分析实现方案
2. 列出需要的组件和函数
3. 给出核心代码
```



2) Code review template

```
请审查这段代码：

【代码】

请从以下角度分析：
1. 代码质量（可读性、可维护性）
2. 性能问题
3. 潜在的 bug
4. 改进建议
```



3) Debugging issue template

```
我遇到了一个问题：

问题描述：【问题描述】

报错信息：
【错误信息】

相关代码：
【代码】

技术栈：【技术栈】

请帮我：
1. 分析问题原因
2. 给出解决方案
3. 解释为什么会出现这个问题
```



4) Performance optimization template

```
这段代码的性能不够好：

【代码】

场景：【使用场景和数据规模】

请帮我：
1. 分析性能瓶颈
2. 给出优化方案
3. 说明优化后的性能提升
```



5) Documentation generation template

```
请为这个【组件/函数】生成文档：

【代码】

文档应该包括：
1. 功能说明
2. 参数说明
3. 返回值说明
4. 使用示例
5. 注意事项
```

Save these templates in a file. Whenever you need one, just copy and paste it and fill in the specific details.



## 9. Time Management Tips

Efficiency is not only a technical problem; it's also a time management problem. Many times, it's not that your skills are lacking—it's that your time wasn't managed well.

Let me share a few methods I use myself:

1) The Pomodoro Technique: Set a 25-minute focus period, and during that time, do only one thing—don't look at your phone, and don't scroll social media. When the time is up, take a 5-minute break: stand up, walk around, drink some water. After 4 Pomodoros, take a 15 to 30 minute rest. This method helps you stay efficient without getting too tired.

2) Break large tasks into small tasks: For example, "complete the user system" is too big and it's hard to know where to start. But if you split it into small tasks such as implementing the registration form, implementing form validation, connecting the registration API, adding error prompts, and testing the registration flow, each task becomes concrete, easy to complete, and more satisfying.

3) Batch similar work: Group similar tasks together—for example, writing the basic structure of all components at once, adding all type definitions at once, or fixing all style issues at once. This reduces context switching, so your brain doesn't have to constantly jump between different kinds of work, and you'll be more efficient.

4) Finally, don't pursue perfection during the MVP stage. First make the feature usable, then think about optimization. First complete the core feature, then add supporting features. First get the tests passing, then refactor the code.

**Remember: done is more important than perfect!**



## Final Thoughts

Improving efficiency doesn't happen overnight. It's accumulated through countless small improvements. Every shortcut, every template, and every automation script can save you a little time. Over time, those small gains add up, and your development speed can make a qualitative leap.

I recommend regularly recording your own workflow and checking which steps consume the most time, which operations are repeated most often, and which areas can be automated—then improve them in a targeted way. At the same time, keep an eye on new tools: follow technical blogs and communities, try new AI tools, and learn new shortcuts and techniques. But don't blindly chase every new thing. AI tools iterate very quickly, but the ones that are truly useful and truly suit you are only a handful. You still need to choose the tools that genuinely improve your efficiency.

Learning from others is also important. For example, watch other people's livestreams or videos, attend technical sharing sessions, or join developer communities. Observe how other developers work and learn from their efficiency techniques—your own efficiency will keep improving too.

Of course, we can't sacrifice code quality just to pursue efficiency. In the next article, I'll talk about code quality assurance and teach you how to ensure the quality of AI-generated code.

Take a short break, and then let's continue the journey.



## Recommended Resources

1) Yupi's AI Navigation Site: [AI Resource Directory, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Codefather Learning Community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussions and Q&A](https://www.codefather.cn)

3) Programmer Interview Guide: [High-frequency topics for internships, campus recruiting, and social recruiting, plus real company problem analysis](https://www.mianshiya.com)

4) Resume Builder for Programmers: [Professional templates, rich sample phrases, direct access to interviews](https://www.laoyujianli.com)

5) 1-on-1 Mock Interviews: [A must-have for winning offers in internships, campus recruiting, and social recruiting](https://ai.mianshiya.com)
