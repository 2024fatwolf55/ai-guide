# The Complete Vibe Coding Glossary

> Understand all the core terms of AI coding in one article



Hello, I’m Yupi, a former full-stack developer at Tencent, an [AI coding blogger](https://space.bilibili.com/12890453) with 2 million followers across the internet, and the creator of 10+ self-developed products such as [AI Navigation](https://ai.codefather.cn) and [Programming Navigation](https://www.codefather.cn).

As you learn Vibe Coding, you’ll definitely run into all kinds of unfamiliar terms and jargon. What is a Token? What is a context window? What is RAG? These concepts may sound intimidating, but they’re actually not hard to understand.

Think of this article as your **AI coding dictionary**. I’ll use the most grounded, beginner-friendly language possible to explain the most common and most important concepts in Vibe Coding. I strongly recommend bookmarking it and coming back whenever you run into a term you don’t understand.



## Basic AI Concepts


### Artificial Intelligence (AI)

Artificial Intelligence (AI) is technology that enables computers to simulate human intelligence. Put simply, it means getting machines to think, learn, and solve problems in ways that resemble humans.

In Vibe Coding, AI is your programming assistant. You just tell it what you want, and it can happily help you design solutions, write code, and fix bugs. It’s like having a programmer friend who stays online 24/7 and is always ready to help.




### Large Language Model (LLM)

A Large Language Model (LLM) is an AI system that can understand and generate human language. ChatGPT, Claude, Gemini, and DeepSeek are all large language models.

Why is it called a “large” model? Because these models have **huge numbers of parameters**, often in the billions or even trillions. In general, the more parameters a model has, the smarter it tends to be—but it also consumes more compute resources.

You can think of an LLM as a super top student who has read massive amounts of books and code. It has seen countless programming cases, so it can help you write code, explain code, and fix bugs.

![](https://pic.yupi.icu/1/%E5%A4%A7%E6%A8%A1%E5%9E%8B%E6%98%AF%E4%BB%80%E4%B9%88%E5%A4%A7.jpeg)

Besides text-based LLMs, the AI world also has vision models that specialize in images (such as Stable Diffusion), audio models that specialize in speech (such as Whisper), and multimodal models that can handle text, images, and audio together (such as GPT-4o and Gemini). In AI coding, what we mainly interact with is the text-based large language model.



### Token

A Token is the basic unit that AI models use to process text. In simple terms, you can think of it as a “chunk of text,” the smallest unit after language has been split up by the model.

This is a concept you absolutely need to understand, because AI services usually charge by Token. Both the text you input and the text AI outputs consume Tokens. The more Tokens you use, the more money you spend.

In English, one Token is usually about one word or part of a word. In Chinese, one character is often about 1 to 2 Tokens. Different models use different tokenizers, so the same passage may correspond to different Token counts in different models.

It’s worth mentioning that Chinese large models such as Qwen and DeepSeek are specially optimized for Chinese, so one Token can represent about 1.5 to 1.8 Chinese characters, which is much more efficient than early English-first models.

For example:

- "Hello World" is about 2 Tokens
- “你好世界” is about 4 to 6 Tokens

![](https://pic.yupi.icu/1/image-20260112112612434.png)

Many current AI coding tools, such as Cursor and Claude Code, also provide real-time Token usage statistics so you can keep track of usage and cost at any time.



### Input Tokens and Output Tokens

When AI services charge you, they usually calculate input Tokens and output Tokens separately.

- Input Tokens: what you send to AI, such as prompts, code, and files
- Output Tokens: what AI sends back to you, such as replies, generated code, and tool-calling instructions

Generally speaking, output Tokens are more expensive than input Tokens. Taking Claude Sonnet 4 as an example, input is priced at $3 per million Tokens, while output is $15 per million Tokens—five times more expensive. That’s because generating content consumes more compute than understanding content.

One of the simplest Token-saving tips is this: **write concise and clear prompts carefully**, so AI understands your needs in one shot and you avoid repeated conversations. For more Token-saving tricks, you can watch Yupi’s video: [AI Coding Money-Saving Tips](https://www.bilibili.com/video/BV1pAy5BXE5z)



### Token Caching

Token caching is a mechanism that can save you a lot of money. Put simply, when a large model processes your prompt, it has to do a large amount of computation. If you have multiple consecutive conversations, much of the content—such as the system prompt or referenced code files—is repeated. Recomputing it every time would be wasteful. Caching stores those intermediate computation results so that when the same prefix appears again, it can be reused directly, making things both faster and cheaper.

There are two kinds of cache-related Tokens:

- Cache write Tokens: when AI processes your context for the first time and stores the computation result, this is slightly more expensive than ordinary input
- Cache read Tokens: when the same context is used later, the cached result is reused directly, and the price can be as low as **one-tenth of normal input**

![](https://pic.yupi.icu/1/Token%E7%BC%93%E5%AD%98%E6%9C%BA%E5%88%B6%E5%A4%A7.jpeg)

So when chatting with AI, try to keep your context stable. For example, don’t frequently change referenced files or rule files. That way, you can keep benefiting from the cache discount. Sometimes you’ll notice that continuing a conversation is cheaper than starting a new one, and caching is the reason why.



### Model Parameters

Parameters are the “bits of knowledge” a model learns during training, stored internally as numbers.

Here’s an easy example: during training, if the model repeatedly sees phrases like “the sky is blue,” it gradually stores the association between “sky” and “blue” inside its parameters. The more parameters there are, the richer the knowledge and associations the model can store.

Parameter count directly affects both model capability and cost. More parameters generally mean a smarter model, but they also require more compute resources such as GPUs, so the model becomes more expensive to run.

Among today’s mainstream models, some publicly disclosed parameter counts include:

- DeepSeek-V4-Pro: 1.6 trillion parameters (MoE architecture, with 49 billion actually activated)
- DeepSeek-V4-Flash: 284 billion parameters (13 billion activated)
- Qwen3.8-Max: 2.4 trillion parameters (Qwen’s latest flagship model, also using MoE, with 95 billion activated—only about 4% of total parameters)
- Llama 4 Scout: 109 billion parameters (Meta’s open-source model, with 17 billion activated)

It’s also worth noting that even within the same model family, vendors often offer multiple versions with different parameter sizes.

![](https://pic.yupi.icu/1/image-20260302162302260.png)




### Model Training and Inference

Training is the process by which an AI model learns knowledge from massive amounts of data. This requires enormous computational resources and time, and is generally done by AI companies. In almost all cases, you do not need to train a model yourself—you can just use a finished model directly.

Inference is what happens after the model has already been trained and has knowledge. It is the process of using that learned knowledge to answer questions and generate content. When we use AI tools every day—chatting with ChatGPT, asking Cursor to write code—we are essentially using the model in inference mode.

To use an analogy, training is like a student going to school and studying, while inference is like that student taking an exam and answering questions.

![](https://pic.yupi.icu/1/%E6%A8%A1%E5%9E%8B%E8%AE%AD%E7%BB%83%E5%92%8C%E6%8E%A8%E7%90%86%E5%A4%A7.jpeg)




### Fine-tuning

Fine-tuning means continuing to train an existing model on data from a specific domain so it performs better in that domain.

For example, you could fine-tune a model with a large amount of medical material so it becomes a medical expert. Or you could fine-tune it using your company’s codebase so it better understands your project style.

For ordinary users, fine-tuning is relatively expensive, so in most cases there’s no need to do it yourself. Using ready-made models is enough. That said, many AI application development platforms—such as Alibaba Cloud Bailian and Volcano Engine—already provide fine-tuning capabilities, lowering the barrier significantly.

![](https://pic.yupi.icu/1/image-20260302163159965.png)



### Model Distillation

Model distillation, also called Knowledge Distillation, is a technique for “compressing” the knowledge of a large model into a smaller model.

It’s like an experienced senior engineer mentoring a junior. The senior engineer (the teacher model) doesn’t just give the final answer, but also shares their reasoning process and thought patterns. The junior (the student model) learns those ways of thinking and can then make similar decisions at much lower cost.

The core of distillation lies in “soft labels.” For example, when a large model identifies an image of an animal, it may not simply say “this is a dog,” but instead output probabilities such as dog 92%, cat 5%, wolf 3%. That 5% for “cat” contains valuable information, because it shows the image shares some features with a cat. By learning this probability distribution, a smaller model can learn subtle relationships between categories. This often works far better than using only hard labels like right or wrong.

Distillation has many advantages: costs can drop by 5 to 30 times, inference speed can increase by 4 times, and performance retention can stay above 95%. A classic example is a distilled version of DeepSeek-R1, where a 67.1-billion-parameter teacher model trained a 3.2-billion-parameter student model that still performed very strongly. The latest DeepSeek-V4 series continues the same idea, using MoE so that a 1.6-trillion-parameter model only activates 49 billion parameters while still achieving powerful reasoning.

So what’s the difference between distillation and fine-tuning?

Fine-tuning keeps training an existing model on domain-specific data so it becomes more specialized in that domain; distillation transfers knowledge from a large model into a smaller one so the smaller model becomes lighter and cheaper.



### Context Window

The context window refers to the maximum amount of content an AI model can “remember” at one time, measured in Tokens.

Different models have different context window sizes:

- GPT-4o: 128K Tokens (about 100,000 Chinese characters)
- GPT-5.5: 1M Tokens (about 750,000 Chinese characters)
- Claude Opus 4.8: standard 200K Tokens, expandable to 1M Tokens (about 750,000 Chinese characters)
- Gemini 3.1 Pro: 1M Tokens (about 750,000 Chinese characters), and it can simultaneously process text, images, audio, and video
- DeepSeek-V4-Pro: 1M Tokens (about 750,000 Chinese characters)

The larger the context window, the more code AI can process and the longer the conversation history it can retain. If your project contains a lot of code, or you’re unsure whether AI can finish the task in one conversation, choosing a model with a larger context window is usually more suitable.

But remember: the larger the context window, the more Tokens each request consumes, and the higher the cost. For example, in Cursor, when using Claude Sonnet, if a single request exceeds 200,000 Tokens, the input price doubles.



## Prompt-Related Concepts


### Prompt

A prompt is the instruction or question you give to AI. In AI coding, a prompt is your requirement expressed in natural language.

The quality of your prompt directly determines the quality of AI’s output. A good prompt should:

- Be specific and clear
- Include the necessary background information
- Explain the expected output format

For example, “build a website” is vague, while “use React to build an expense-tracking website with three functions: add expenses, view the list, and calculate the total, using a blue-themed interface” is a much better prompt.

In AI conversation, messages are generally divided into three roles:

- System prompt: sets AI’s role and behavioral rules, and is not visible to the user
- User prompt: the message you send to AI
- Assistant prompt: the message AI sends back to you

Understanding these three roles helps you use AI better. For example, many AI coding tools let you set system prompts to define AI behavior, while whatever you type in the chat box is the user prompt.

![](https://pic.yupi.icu/1/1745462990451-6f2b5727-d47b-436c-9da2-50dac64fb790.png)



### System Prompt

A system prompt is the instruction given to AI before the conversation begins, used to define its role, behavior, and constraints.

For example, you might set a system prompt like: “You are a senior Java backend expert. Please answer with a concise and clear coding style.”

The system prompt remains effective throughout the whole conversation, making it one of the most important ways to customize AI behavior.

Do you remember how, a few years ago when AI first became popular, a huge number of AI assistant websites suddenly appeared? Many of them were basically just wrappers around the same underlying large model, but each one set a different system prompt, such as “you are a translation expert” or “you are a legal consultant.”

![](https://pic.yupi.icu/1/%E4%B8%BB%E9%A1%B5.png)



### Prompt Engineering

Prompt Engineering is the technique of designing and optimizing prompts so AI can better understand your intent and generate results that match your expectations more closely.

This is one of the core skills of Vibe Coding. A good prompt engineer can use fewer rounds of conversation and lower Token cost to get much higher-quality code from AI.

If you want to learn practical prompt-writing techniques, you can check out Yupi’s free *AI Coding Tutorial*: [Prompt Writing Techniques](https://ai.codefather.cn/library/2010974716125712386)

![](https://pic.yupi.icu/1/image-20260302164120604.png)



### Zero-shot

Zero-shot prompting means giving AI a task without providing any examples—just directly describing what you want it to do.

For example: “Please translate this English sentence into Chinese.”

AI completes the task based on what it learned during training.

For simple tasks, zero-shot prompting is usually enough. There is no need to provide extra examples, and it saves some Token cost as well.



### Few-shot

Few-shot prompting means giving AI a task along with a few input-output examples, so AI can learn the format or style you want and complete the task more accurately.

For example:

```
请按以下格式翻译：
英文：Hello → 中文：你好
英文：Thank you → 中文：谢谢
英文：Good morning → 中文：
```

By giving examples, AI can understand your requirements more precisely and produce more consistent output.

![](https://pic.yupi.icu/1/image-20260302164402338.png)



### Chain-of-Thought

Chain-of-Thought prompting, often abbreviated as CoT, is a technique that guides AI to show its reasoning process and think step by step rather than immediately jumping to the final answer. It is especially effective for complex reasoning tasks, such as multi-step math problems, code logic analysis, and system architecture design.

Triggering chain-of-thought prompting is simple. Many reasoning models, such as DeepSeek-R1, and many AI coding tools already have built-in chain-of-thought capability and automatically display reasoning. You can also manually add a phrase like “please think step by step” to your prompt. In many cases, this leads to more accurate answers.

In AI coding, when a project involves complex business logic, multi-module interaction, or tradeoffs between multiple technical options, it is especially suitable to rely on reasoning models and chain-of-thought prompting so AI thinks things through before acting.

![](https://pic.yupi.icu/1/chainofthought.png)



### Markdown

Markdown is a lightweight markup language that uses simple symbols to represent formatting. For example, `#` indicates a heading, `**text**` indicates bold, and `-` indicates a list.

![](https://pic.yupi.icu/1/image-20260302164811601.png)

Markdown is very important in AI coding because:

- Most AI-generated replies are in Markdown format
- Project documents such as `README` files are written in Markdown
- Rule files for AI agents are also written in Markdown

Learning Markdown helps you communicate better with AI and write more standardized project documentation. More importantly, structured content—such as heading hierarchy, lists, and code blocks—helps AI understand your intent more accurately, while also helping you build stronger structured thinking of your own. That is very useful for writing good prompts.



## AI Coding Modes


### Vibe Coding

Vibe Coding is a concept proposed by computer scientist Andrej Karpathy in February 2025. It describes a brand-new way of programming: talk to AI in natural language, let AI help you write code, and focus yourself on describing requirements, test results, and direction.

You do not need to be an expert in programming syntax. You only need to express your ideas clearly, and AI is responsible for turning those ideas into runnable code.

So the key point of Vibe Coding is not writing code. It is clarifying needs and expressing them clearly. The clearer your description is, the more reliable the result AI gives you will be.

It’s like ordering takeout: you tell the app what you want to eat, and the restaurant makes it and sends it to you. You do not need to know how to cook, but you do need to know what you want to eat.



### Agentic Engineering

Agentic Engineering is a new concept proposed in February 2026 by Andrej Karpathy, the same person who proposed Vibe Coding. You can think of it as the standardized version of Vibe Coding.

Vibe Coding is coding by feel: you give AI one sentence, AI spits out some code, and if it runs, great. If it doesn’t, you paste the error back and let AI revise it. It’s extremely fast for building small tools, but once the project gets large, it’s easy for things to go off the rails.

Agentic Engineering takes a different approach: first think clearly about what you want to do, write the plan, break the task down, then hand the work to AI to execute. After it finishes, you still need to review and accept the result. If the quality is poor, you send it back for rework.

To use an analogy, in Vibe Coding you’re a DJ, choosing songs by pure feeling. In Agentic Engineering, you’re a foreman who decides the workflow, quality standards, and acceptance process. **One follows intuition, the other follows process.**

Of course, this doesn’t mean Vibe Coding is outdated. Vibe Coding helps you discover possibilities, while Agentic Engineering helps you turn those possibilities into something truly usable. They fit different scenarios: Vibe Coding is great for small tools, while enterprise-grade projects require the mindset of Agentic Engineering.

![](https://pic.yupi.icu/1/agentic%20engineering.jpeg)



### Agentic Coding

Agentic Coding means letting AI work like an autonomous “agent,” capable of planning tasks, executing operations, and verifying results by itself rather than just passively answering questions.

The difference between this and Agentic Engineering is that Agentic Coding emphasizes AI’s autonomous execution ability—what AI can do—while Agentic Engineering emphasizes the human methodology for managing AI—how humans should manage it.

Today, almost all mainstream AI coding tools provide agentic coding capabilities. For example, in Cursor’s Agent mode, AI can:

- Automatically read and analyze multiple files
- Plan an implementation approach
- Execute code modifications
- Run tests for verification
- Automatically fix problems

This is much more powerful than traditional Q&A-style AI, because it can autonomously complete complex multi-step tasks. You could say AI is no longer just a sidekick in programming—it is becoming one of the core driving forces in project development.

![](https://pic.yupi.icu/1/agent-in-cursor.png)



### Harness Engineering

Harness Engineering is a new AI engineering paradigm that rose in 2026. Its core idea is **humans steer, agents execute**. It does not optimize the AI model itself, but instead builds a complete system of constraints, feedback loops, and workflow management around AI agents, allowing inherently unpredictable AI to run steadily and efficiently in a highly reliable environment.

The word Harness originally means “horse tack.” Just as reins and saddles guide a powerful but unpredictable horse, Harness Engineering is the whole “runtime environment” built around AI coding agents to ensure they work the way you expect.

![](https://pic.yupi.icu/1/2_harness_horse.png)

Why is this concept becoming more and more important?

Because in the era of AI coding, **the model itself is already becoming a commodity. The real competitive advantage lies in the engineering system you build around the model.** The same large model can produce wildly different code quality under different Harness setups. The role of programmers is shifting from “writing code themselves” to “designing systems that allow AI to write code reliably.”

![](https://pic.yupi.icu/1/8_agent_queals.png)

From an evolutionary perspective, Harness Engineering is a further development on top of prompt engineering and context engineering. Prompt engineering focuses on “how to instruct AI,” context engineering focuses on “how to provide information to AI,” and Harness Engineering focuses on “how to make AI reliably finish a whole task over time.” These layers contain one another.

![](https://pic.yupi.icu/1/7_harness_layers.png)

The core modules of Harness include:

- Context architecture (help AI understand project background and rules)
- Execution capability (give AI tools and MCP)
- Task orchestration (Plan Mode, parallel SubAgents, and so on)
- Feedback mechanisms (linter, automated tests, Browser Use)
- Architectural guardrails (stop the codebase from becoming a mess)

![](https://pic.yupi.icu/1/20_harness_modules.png)




### Loop Engineering

Loop Engineering is a new AI coding paradigm that emerged in mid-2026. Its core idea is **design an automatic loop system so AI can execute, verify, and repair by itself until the goal is achieved**.

Older AI coding felt like driving a manual-transmission car—every step depended on you. Loop Engineering is more like autopilot: you set the destination and safety rules in advance, and AI executes, checks, and fixes on its own until the task is complete.

![](https://pic.yupi.icu/1/01_Loop_Engineering%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5%EF%BC%9A%E4%BD%A0%E8%AE%BE%E8%AE%A1%E7%B3%BB%E7%BB%9F%E8%AE%A9%E5%AE%83%E4%BB%A3%E6%9B%BF%E4%BD%A0%E7%BB%99AI%E4%B8%8B%E6%8C%87%E4%BB%A4_compressed_v1.png)

A reliable Loop needs three core elements:

- **Clear goals and stopping conditions**: for example, “all tests pass” is a good stopping condition
- **A feedback loop**: automatically check the result after each iteration and decide whether to continue or stop
- **State memory**: use an external file such as `PROGRESS.md` to record progress, so restart does not mean starting from zero

![](https://pic.yupi.icu/1/03_Loop%E7%9A%843%E5%A4%A7%E6%A0%B8%E5%BF%83%E8%A6%81%E7%B4%A0%EF%BC%9A%E7%9B%AE%E6%A0%87%E5%81%9C%E6%AD%A2%E6%9D%A1%E4%BB%B6%E3%80%81%E5%8F%8D%E9%A6%88%E9%97%AD%E7%8E%AF%E3%80%81%E7%8A%B6%E6%80%81%E8%AE%B0%E5%BF%86_compressed_v2.png)

From the perspective of development history, Loop Engineering is a further evolution built on top of prompt engineering, context engineering, and Harness Engineering. The earlier layers make it possible for AI to work in a reliable environment, while Loop adds one more layer on top—**automatic iteration + a closed feedback loop**—turning you from the operator who manually prompts AI sentence by sentence into the manager who designs loop rules.

![](https://pic.yupi.icu/1/04_AI%E7%BC%96%E7%A8%8B%E8%BF%9B%E5%8C%964%E9%98%B6%E6%AE%B5%EF%BC%9APrompt%E2%86%92Context%E2%86%92Harness%E2%86%92Loop_compressed_v3.png)



### Multi-Agent Collaboration

Multi-Agent collaboration refers to multiple AI agents dividing work and cooperating to complete complex tasks together.

For example, one agent may design the architecture, one may write frontend code, one may write backend code, and one may review the code. They work together like a real software development team.

Over the past two years, multi-agent systems have become an important trend in AI coding. Their advantage is not just handling more complex projects, but also dramatically improving efficiency through parallel work, allowing tasks that used to take hours to be finished in minutes.

![](https://pic.yupi.icu/1/%E5%A4%9A%E6%99%BA%E8%83%BD%E4%BD%93%E5%8D%8F%E4%BD%9C%E5%A4%A7.jpeg)



### Agent Orchestration

Orchestration is the process of coordinating and managing multiple AI agents or AI tasks, ensuring they work in the right order and in the right way.

If multi-agent collaboration focuses on “which roles are involved,” then orchestration focuses on “who works first, who works next, and how the results are combined.” It is the command center of a multi-agent system.

Like a conductor leading an orchestra, the orchestrator decides which agent does what, at what time, how information is passed, and how results are aggregated.

![](https://pic.yupi.icu/1/image-20260112112854174.png)



### Subagents

Subagents are a mechanism by which a main AI agent delegates part of a task to independent child agents that process subtasks in parallel.

You can think of them as AI subordinates, like a manager distributing work to several employees at the same time. When the main AI encounters a large task, it can split independent subtasks across several subagents while continuing to handle other work itself.

The benefits of Subagents include:

- Parallel handling of multiple independent tasks, greatly improving efficiency
- The main agent’s context stays clean and is not polluted by subtask details
- Each subagent can focus on its own task, improving accuracy

For example, you can have several subagents review different modules of the same codebase at the same time, which is much faster.

![](https://pic.yupi.icu/1/%E5%AD%90%E4%BB%A3%E7%90%86%E6%BC%AB%E7%94%BB%E5%A4%A7.jpeg)

In Claude Code, AI automatically creates subagents through the built-in Task tool, so you don’t need extra configuration. You can also create custom subagents under the `.claude/agents/` directory using Markdown files, giving them dedicated role descriptions, tool permissions, and behavior rules.

But subagents also have limitations. Each subagent has its own independent context, and they cannot directly share information with one another, so they are not suitable for tasks with strong mutual dependencies. In addition, running multiple subagents at the same time consumes more Tokens, so the cost increases accordingly. It’s like hiring more people for a company—work does go faster, but salary expense rises too, and coordination becomes more costly.



### Agent Teams

[Agent Teams](https://code.claude.com/docs/en/agent-teams) is a new multi-agent coding mode that rose in 2026, first introduced by Claude Code. It allows 3 to 5 independent AI agents to form a team and work in parallel on the same project.

Unlike the traditional single-AI conversation, Agent Teams has a Team Lead who breaks down tasks and coordinates work, while the other Teammates independently take tasks and execute them. They can also communicate with one another through a messaging system.

![](https://pic.yupi.icu/1/subagents-vs-agent-teams-light.png)

To use an analogy, coding with AI used to feel like you personally managing one intern. Agent Teams is more like directly managing a small team, with frontend, backend, and testing all happening at once, multiplying efficiency several times over. Anthropic’s engineering team once used 16 agents working simultaneously to produce 100,000 lines of Rust code, compressing what used to take days into only a few hours.

Of course, the tradeoff is that Token usage can be much higher, so Agent Teams is not something you should use in every situation.

In practice, the agents in an Agent Team usually need physical isolation to avoid code conflicts. The most mainstream approach is to use Git WorkTree to allocate an independent working directory to each agent, letting them develop on separate branches.

![](https://pic.yupi.icu/1/image-20260410145744619.png)

Cursor already has built-in support for this through Parallel Agents mode, automatically creating and managing WorkTrees so multiple AIs can work in parallel and then merge the code with one click.

![](https://pic.yupi.icu/1/image-20260410150251832.png)



### Hermes Agent

[Hermes Agent](https://github.com/NousResearch/hermes-agent) is a self-improving open-source AI agent released by Nous Research in February 2026. Its biggest feature is that it can learn from the tasks it completes and become smarter the more you use it.

Ordinary AI agents start from zero in every conversation and do not learn from past experience. Hermes Agent, by contrast, includes a built-in closed-loop learning mechanism:

1. After completing a task, it automatically refines the solution into a reusable Skill Document
2. The next time it encounters a similar task, it retrieves existing skill documents first
3. It continuously improves those skills based on new practice

Official data shows that Hermes Agent, when using previously accumulated skills, completes similar tasks 40% faster than a fresh instance.

Hermes Agent uses a three-layer memory system: session memory (current conversation context), skill documents (reusable knowledge refined from tasks), and a user profile (persistent user preferences and habits). It supports Telegram, Slack, Discord, WeChat, and many other platforms, is compatible with more than 200 AI models, and is fully free and open source.



### Background Agent

A Background Agent is the ability to let AI run autonomously in the background and notify you when it finishes.

Traditional AI coding requires you to keep staring at the screen while AI works step by step, and you often can’t even shut your computer. A Background Agent lets you hand the task to AI and then go do something else. AI finishes the work independently in the cloud, and you can even shut your computer!

For example, you can ask AI to fix a batch of bugs in the background, run one round of code review, or complete an entire feature module, and then notify you when it’s ready for acceptance.

At present, tools such as Claude Code and Cursor already support Background Agent capability. In the future, AI coding may feel like sending a WeChat message: you send the requirement from your phone, go live your life, and AI comes back to you when it’s done.

![](https://pic.yupi.icu/1/cursor%20agent%E5%90%8E%E5%8F%B0%E8%83%BD%E5%8A%9B_%E5%89%AF%E6%9C%AC.jpg)



### Agent Loop

An Agent Loop is the core working mechanism of an AI agent. Simply put, AI repeatedly goes through a cycle of **perceive → think → act → observe** in order to complete a task step by step.

A typical Agent Loop includes:

1. Perceive: obtain information from the current environment, such as reading files or checking errors
2. Think: analyze the situation and decide the next action
3. Act: perform a concrete operation, such as writing code or running commands
4. Observe: inspect the result of the action
5. Loop: decide whether to continue based on the result

This cycle continues until the task is finished or a stopping condition is reached.

Understanding the Agent Loop helps you plan tasks better and manage AI’s workflow more effectively. One important thing to remember is that the number of loop iterations in AI coding should not be too high. Many tools impose a maximum loop count, and too many loops not only reduce effectiveness, but also burn Tokens like crazy. Some people have gone to sleep and woken up to find their quota gone, simply because they let AI fall into an infinite loop...

The Claude Code source code is one of the best engineering examples of an Agent Loop. Its core conversation loop is essentially a simple `while(true)` infinite loop: on each iteration, it first compresses context, then calls the large model to get a response, and if the model says “I want to use a tool,” it executes that tool, appends the result to the conversation history, and enters the next round.

![](https://pic.yupi.icu/1/image-20260401140913171.png)



### Ralph Wiggum Loop

The Ralph Wiggum Loop is a relatively popular AI coding pattern from 2026, named after Ralph Wiggum, the famously persistent character from *The Simpsons*.

This pattern already has multiple open-source implementations, such as [wiggumdev/ralph](https://github.com/wiggumdev/ralph). Its core idea is simple: **put AI inside a loop and keep executing until every checklist item in the PRD is completed.**

The workflow roughly looks like this:

1. First write a PRD (Product Requirement Document), breaking the features down into clear checklist items
2. Let the AI agent start executing, taking one unfinished task at a time from the checklist
3. After AI completes one task, it commits the code with Git and records progress
4. Start a fresh new iteration with a clean context and continue processing the remaining tasks
5. Keep looping until all checklist items are completed

The clever part of this pattern is that each round starts with a clean context, while Git and files are used to persist progress. This avoids the problem of AI “losing the thread” in long conversations. It can also run unattended—you write the PRD, go to sleep, and check the results the next day.

But be careful to set iteration limits and a Token budget, otherwise AI may fall into an infinite loop and burn money wildly.



### ReAct

ReAct (Reasoning and Acting) is a technical paradigm that lets AI agents alternate between reasoning and action. Its core idea is simple: let AI think first, then act, then look at the result, and then think about what to do next.

Traditional AI either only thinks without acting, or only acts without thinking. ReAct enables AI to:

1. Reason first: think about the current situation and make a plan
2. Then act: perform a concrete operation
3. Observe the result: see what effect the action had
4. Continue reasoning: adjust strategy based on the result

This loop of “think → act → observe” allows AI to complete complex tasks more reliably, and it is one of the core technologies in modern AI coding tools.

![](https://pic.yupi.icu/1/ReAct%E6%8E%A8%E7%90%86%E4%B8%8E%E8%A1%8C%E5%8A%A8%E5%A4%A7.jpeg)



### Deep Thinking

Deep Thinking is the ability of AI to perform internal reasoning before answering. It is also called “extended thinking” or “thinking mode.”

So how is it different from Chain-of-Thought?

Chain-of-Thought is a prompting technique—you guide AI through prompts to display its reasoning process. Deep Thinking is a built-in model capability—AI performs deep internal reasoning automatically, even without you explicitly asking for it in the prompt.

In normal mode, AI receives a question and directly generates an answer. Once Deep Thinking is enabled, AI first carries out a series of internal reasoning steps, such as analyzing the problem, considering multiple options, and evaluating pros and cons, and only then outputs the final answer. Sometimes you can even see a “thinking...” process in the reply—that is Deep Thinking at work.

![](https://pic.yupi.icu/1/image-20260215104649777.png)

Deep Thinking is especially suitable for complex programming tasks, such as designing system architecture, debugging hard-to-locate issues, and optimizing algorithms. The tradeoff is slower speed and higher Token consumption.

At present, mainstream AI models and AI coding tools all support Deep Thinking, and you can choose whether or not to enable it.




### Adaptive Thinking

Adaptive Thinking is the smarter version of Deep Thinking. It allows AI to automatically judge how deeply the current problem needs to be thought through.

In the past, deep reasoning mode could only be manually turned on or off. If you turned it on, even simple questions would be thought about for ages, wasting both time and money; if you turned it off, complex questions were more likely to fail.

Once AI has Adaptive Thinking, it can instantly answer simple questions while automatically entering deep-thinking mode for complex ones. This preserves quality while also saving time and cost.

![](https://pic.yupi.icu/1/%E8%87%AA%E9%80%82%E5%BA%94%E6%80%9D%E8%80%83%E6%BC%AB%E7%94%BB%E5%A4%A7.jpeg)

Anthropic was the first to introduce Adaptive Thinking in Claude Opus 4.6, and then optimized it further in Opus 4.8. Developers can also choose different thinking intensity levels to balance quality and cost.




### Tool Use

Tool Use, also called Function Calling, is the technology that enables AI to use external tools and functions.

By itself, AI can only generate text. But with Tool Use, it can read and write files, search the web, execute commands and scripts, call APIs, operate databases, and more.

![](https://pic.yupi.icu/1/1746590338968-0240c12b-2956-47f4-b8ff-5b5f831221f6.png)

The workflow of Tool Use can be divided into four steps:

1. Identify the need: AI determines that a tool is needed for the current task
2. Select the tool: choose the appropriate tool from the available set
3. Execute the call: invoke the tool with the correct parameters
4. Integrate the result: incorporate the returned result into the answer and continue the task

For example, if a user wants to retrieve popular articles from the [Programming Navigation site](https://www.codefather.cn), the image below clearly shows the full Tool Use process:

![](https://pic.yupi.icu/1/%E5%B7%A5%E5%85%B7%E8%B0%83%E7%94%A8%E6%B5%81%E7%A8%8B.png)

One thing to note is that the AI model itself does not directly execute tools. Instead, it generates an instruction like “I want to call this tool with these parameters,” and then an external system executes the tool and returns the result to AI.

With Tool Use, AI changes from “only being able to talk” to “being able to take action.” Without Tool Use, AI can only tell you how to modify code and you still have to copy and paste everything yourself. With Tool Use, AI can directly read files, modify code, and run commands for you end to end. Cursor’s Agent mode, for example, is implemented through Tool Use.



### MCP

MCP, short for Model Context Protocol, is an open standard launched by Anthropic at the end of 2024 for safely connecting AI models to external data sources and tools.

You can think of MCP as the “USB interface” of the AI world. Just as USB lets all kinds of hardware devices—keyboards, mice, flash drives—connect to computers in one standardized way, MCP lets all kinds of external tools—file management, databases, search engines, and so on—connect to AI in one standardized way, without requiring each tool to build a separate custom integration.

![](https://pic.yupi.icu/1/1746710765234-c974bda8-666e-45b3-adc4-ace97cbb8c0a.png)

The core value of MCP is **standardization**. Developers do not need to build a separate connector for every AI tool. They only need to implement MCP once, and then any MCP-compatible AI tool can use it. At present, mainstream AI coding tools such as Claude Code, Cursor, and Windsurf, as well as various web AI agent applications, already support MCP.

![](https://pic.yupi.icu/1/1746677838632-9278e62b-c850-4d3c-a835-297ccbe2061a.png)

In Vibe Coding, MCP allows AI to connect to more external tools and data sources, greatly expanding its capability boundary. For example, with Figma MCP, AI can directly read design drafts and generate corresponding webpage code; with GitHub MCP, AI can operate code repositories and create PRs; with database MCP, AI can query and analyze business data.

![](https://pic.yupi.icu/1/image-20260116123701822.png)

💡 Want to discover more useful MCP services? Visit [Yupi AI Navigation - MCP Collection](https://ai.codefather.cn/mcp), where high-quality MCPs are continually updated to help reshape your AI workflow.



### Agent Skills

Agent Skills are [an open standard](https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview) launched by Anthropic in October 2025. The goal is to let AI learn and use all kinds of professional skills, so it can quickly expand its expertise in specific domains.

Simply put, Agent Skills are **skill packs** prepared for AI. A skill pack can contain carefully designed prompts, scripts, and all kinds of resource files.

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

Imagine AI as a workplace beginner. If you install a `文档处理技能`, it immediately knows how to generate PPT slides and process Excel spreadsheets. If you install a `代码规范技能`, it knows how to write code according to your company’s standards.

![](https://pic.yupi.icu/1/1769306900359-2a2b73da-a366-411d-ad3b-2ae61f6b5bc4.png)

At its core, a Skill is a folder containing a `SKILL.md` file. That folder can also include instruction documents, script code, reference materials, and so on. When AI encounters a related task, it automatically loads the corresponding Skill to enhance its ability.

![](https://pic.yupi.icu/1/agent%2520skills.jpeg)

The core design idea of Skills is **progressive disclosure**. AI loads only the relevant content when needed rather than stuffing all information into context at once, which saves Tokens and keeps things flexible.

![](https://pic.yupi.icu/1/agent%20skills%20bundling.jpeg)

💡 Want to discover more useful Agent Skills? Visit [Yupi AI Navigation - Skills Collection](https://ai.codefather.cn/skills), where high-quality skills are continuously updated so AI can help you do even more work.



### Hooks

Hooks are automated triggers in AI coding tools. When AI completes a certain action—such as generating code, committing code, or running a command—a Hook automatically executes the script or checking process you configured in advance.

Mainstream AI coding tools all support Hooks. For example, in Claude Code, Hooks can be used to:

- Automatically run a formatter after code generation
- Automatically run tests after a file is modified
- Automatically judge whether a permission request is safe and approve it
- Automatically check coding standards before a commit

![](https://pic.yupi.icu/1/image-20260215105006734.png)

Hooks make your AI workflow more automated and reduce manual work. But you should also be careful—if Hooks are misconfigured, they can block AI’s normal workflow. It’s best to test them on a small scale first before rolling them out across the entire project.



### Slash Commands

Slash Commands are shortcut commands triggered by typing `/` in the chat box of an AI coding tool. They let you quickly execute common operations.

You can think of Slash Commands as keyboard shortcuts for operating AI. Mainstream AI coding tools such as Cursor and Claude Code all support them. For example, Claude Code includes these common built-in slash commands:

- `/help`: view available commands
- `/compact`: compress the context of the current conversation
- `/config`: modify configuration
- `/skills`: view installed skills

![](https://pic.yupi.icu/1/image-20260215105146492.png)

You can also customize Slash Commands and package common workflows for reuse. For example, create a `/commit-push-pr` command to complete code commit, push, and PR creation in one shot; or make a `/techdebt` command that cleans duplicated code at the end of every session.

Under the hood, a custom command is basically just a Markdown file. In Cursor, you only need to create a `.md` file under `.cursor/commands/`, write the instruction you want AI to execute inside it, and that filename becomes a slash command. You can also use Git to version-control those custom command files and reuse them across projects.

![](https://pic.yupi.icu/1/image-20260302171806320.png)



### A2A

A2A, short for Agent-to-Agent, is a protocol or communication method that lets AI agents talk to and cooperate with one another. It is one of the foundational technologies of multi-agent systems.

Just as people need language to communicate, AI agents also need standardized ways to exchange information, assign tasks, and report results.

The A2A protocol allows different AI agents to form teams and cooperate on complex tasks. It was introduced by Google in 2025, and more than 150 companies have already joined in supporting it.

![](https://pic.yupi.icu/1/a2a-agent.png)

Do not confuse A2A with MCP! They are complementary. MCP solves the problem of AI connecting to tools, while A2A solves the problem of AI agents communicating and collaborating with each other.



### ACP

In the AI world, ACP actually has two meanings, which makes it easy to confuse, so let’s clarify both.

**The first is Agent Communication Protocol**, introduced by IBM Research. It allows AI agents built by different frameworks and different companies to cooperate seamlessly, just like phones from different brands can all call one another.

It is based on lightweight HTTP REST interfaces, supports multiple content formats such as text, code, files, and images, is not tied to any specific programming language, and is very easy to get started with.

![](https://pic.yupi.icu/1/%E6%99%BA%E8%83%BD%E4%BD%93ACP%E5%8D%8F%E8%AE%AE%E5%A4%A7.jpeg)

Note that ACP and the A2A mentioned earlier are two separate protocols. Both solve the problem of cross-framework communication between agents, but their communication formats and capability-discovery mechanisms are still two different systems. These protocols are mainly aimed at programmers building AI applications and help them construct systems where multiple agents collaborate.

**The second is Agent Client Protocol**, introduced jointly by JetBrains and Zed. It solves a completely different problem: allowing any AI coding agent to run inside any IDE.

You can think of it as a “universal adapter” for AI coding tools. In the past, every AI coding plugin had to build one version for IDEA, another for VS Code, and so on. With ACP, Claude Code only needs to implement the ACP interface once, and IDEA can directly integrate it. That means you can happily use Claude Code inside IDEA and use Gemini CLI inside the Zed editor too, without being tied to a single IDE.

JetBrains has also launched an ACP Agent Registry, making it possible to install all kinds of AI coding agents with one click, which is becoming more and more convenient~

![](https://pic.yupi.icu/1/image-20260328131101270.png)



### BMAD

[BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD), short for Breakthrough Method of Agile AI-Driven Development, is a systematic AI agent development framework whose goal is to turn messy AI coding processes into something structured and reusable.

BMAD organizes the development process around **role-based agents**, with each agent playing a specific role:

- Analyst Agent: creates the project brief, including market analysis and user personas
- PM Agent: turns the brief into a detailed PRD
- Architect Agent: designs the technical implementation plan and system architecture

There are two types of agents in BMAD:

- Simple Agents: single-file and self-contained, suitable for focused tasks such as code review and document generation
- Expert Agents: have persistent memory across sessions and dedicated folders for resources, suitable for complex multi-step workflows

Every agent has standardized components, including persona (role, identity, communication style, principles), a list of capabilities, an interaction menu, and optional key actions.

![](https://pic.yupi.icu/1/BMAD%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%E5%A4%A7.jpeg)

BMAD has received tens of thousands of Stars on GitHub, which shows that this structured AI development method is being recognized by more and more developers.

![](https://pic.yupi.icu/1/image-20260201143945594.png)




### Browser Use

Browser Use is the capability that allows AI agents to operate web browsers autonomously. With Browser Use, AI can browse webpages, click buttons, fill out forms, and extract data just like a human.

Typical use cases of Browser Use include:

- Automated research: let AI search and organize information across multiple websites
- Data collection: extract structured data from webpages
- Form filling: automatically complete tedious online forms
- Cross-platform operations: complete multi-step tasks across different websites

A well-known open-source project is [Browser-Use](https://github.com/browser-use/browser-use), which supports controlling a browser through various large models in Python. In addition, mainstream AI coding tools such as Cursor and Claude Code also have Browser Use capability built in, allowing AI to automatically open a browser to preview pages and execute tests during development.

![](https://pic.yupi.icu/1/image-20251030220841383.png)

One key advantage of Browser Use is that AI can make use of your existing browser sessions and login state, without requiring you to separately build API integrations for every website. In other words, AI can access sites that do not even have public APIs, greatly expanding the scope of automation.



### Computer Use

Computer Use is an AI capability introduced by Anthropic in 2024 that lets Claude operate an entire computer desktop like a human.

Unlike Browser Use, which only operates inside a browser, Computer Use can control any desktop application, for example:

- View screenshots and understand interface elements
- Move the mouse cursor and click buttons
- Type text with the keyboard
- Execute command-line operations

Computer Use works through a continuous feedback loop:

1. Screenshot analysis: AI captures and analyzes the current screen
2. Decision planning: determine the next action based on the task goal
3. Execute operation: send mouse or keyboard input
4. Observe result: inspect the effect of the action and adjust the strategy

💡 For safety reasons, Computer Use usually runs inside a virtual machine or container rather than directly controlling your real computer.

Computer Use represents a major leap from “AI that can only generate text” to “AI that can operate software,” fundamentally changing the way humans and machines interact.

Based on Computer Use, Anthropic launched [Claude Cowork](https://claude.com/product/cowork) in 2026, a desktop AI assistant that can directly access files and folders on your computer and help with office tasks such as organizing your Downloads folder, extracting data from screenshots into spreadsheets, and preparing brand reports.

![](https://pic.yupi.icu/1/975b77da-9bb4-436e-bdf4-cd6318fd593c.png)




## Context Management


### Context

Context is all the information AI can refer to when answering a question, including:

- The history of the current conversation
- The code files you currently have open
- The project’s structure and configuration
- The reference materials you provide

The richer and more relevant the context is to the current task, the more the code AI generates will match your needs. It’s like handing off work to a new colleague: the more background information you provide, the faster they can get started.

In Cursor, you can roughly understand the size of the current context through the Token usage indicator near the chat box. In Claude Code, you can use the `/context` command to inspect context usage.

![](https://pic.yupi.icu/1/image-20260302172312528.png)



### Context Engineering

Context Engineering is the technique of strategically managing and optimizing the context information provided to AI.

Its core goal is **to give AI just the right amount of information**—not too little, so AI remains clueless, and not too much, so information overload and unnecessary cost appear.

Good context engineering includes:

- Selecting the most relevant files
- Providing the necessary background explanation
- Using rule files to define project standards
- Cleaning up irrelevant conversation history at the right time

Context Engineering is currently one of the hottest research directions in AI. The 2026 trend is moving from simple context management toward a more complex **memory architecture**—letting AI have short-term memory (current conversation context), long-term memory (knowledge accumulated across sessions), and external memory (vector databases, knowledge graphs, and so on).

For example, Claude Opus 4.5 introduced the [Memory Tool](https://console.anthropic.com/docs/en/agents-and-tools/tool-use/memory-tool), which allows AI to remember important information through filesystem-like persistent storage even when the context window is exceeded. According to Anthropic’s official data, this reduced Token consumption in long-running workflows by 84%!

You could say that whoever solves the problem of context and memory better will gain an advantage in the field of AI coding.

Claude Code’s three-layer memory architecture is a classic example of Context Engineering in practice:

- The first layer is `MEMORY.md` (hot data), like a book’s table of contents. It is loaded in every conversation, but is strictly limited to 200 lines and 25KB.
- The second layer is topic files (warm data), which store coding preferences, project conventions, and so on. When a new conversation begins, AI loads only the five most relevant files.
- The third layer is historical conversations (cold data), stored as files and searched with grep when needed. Different “temperature” levels of data are managed differently—hot data stays resident, warm data is loaded on demand, and cold data is searched.

![](https://pic.yupi.icu/1/image-20260401141550843.png)

One especially interesting design choice is that Claude Code’s memory stores people’s preferences and judgments, but not code facts. Code changes, while memory does not automatically update. If memory says “function X is on line 30,” that becomes misleading after a refactor. Code facts should always be read live from source. This design eliminates inconsistency between cached memory and real data at the root.



### Context Compaction

Context Compaction is the technique of automatically compressing and summarizing earlier conversation content, solving the problem of context overflow in long-running tasks.

In the past, when AI was handling long tasks, it often hit the ceiling of context length. Once earlier conversation content was squeezed out, AI effectively developed amnesia, and the code it generated no longer matched earlier decisions and conventions. With Context Compaction, once the context is about to fill up, AI automatically summarizes earlier conversation into a more compact form, preserving the key information while freeing space. That allows it to keep working much longer without forgetting everything.

You can think of it as a project manager writing meeting minutes. After a three-hour meeting, nobody can record every single sentence, but the key decisions, action items, and important conclusions are written down. AI’s Context Compaction works in a similar way, condensing a long conversation history into key information.

![](https://pic.yupi.icu/1/%25E4%25B8%258A%25E4%25B8%258B%25E6%2596%2587%25E5%258E%258B%25E7%25BC%25A9%25E6%25BC%25AB%25E7%2594%25BB%25E5%25A4%25A7.jpeg)

Claude Opus 4.8 already has built-in Context Compaction. Combined with its 1-million-Token context window, this makes long-running coding tasks much more stable.

In its source code, Claude Code implements an elegant five-level compaction strategy, filtering things layer by layer like a funnel:

1. Snip: the lightest cut, where old tool-call results keep only their structure but not their content
2. Microcompact: large tool execution results are unloaded into cache. Note that they are unloaded into cache rather than thrown away directly, because sub-agents may still need them later
3. Context Collapse: fold and summarize conversation content in the middle, preserving only key information
4. Autocompact: when context usage exceeds a threshold, trigger full-summary compaction
5. Reactive Compact: the emergency fallback, triggered when the API returns a 413 “prompt too long” error

These five levels are triggered from light to heavy: trim what can be trimmed first, and only use the heavier methods if necessary.

![](https://pic.yupi.icu/1/image-20260401142212163.png)




### Rules File

A Rules File is a configuration file placed inside a project to tell AI about your project standards, tech stack, coding style, and related information. With a Rules File, AI can refer to those rules every time it generates code, making the output more aligned with your project style and saving you from repeating the same instructions again and again.

Different AI coding tools use different Rules File formats:

- Cursor: previously used the single-file `.cursorrules` format, and now recommends the multi-file `.cursor/rules/*.mdc` format
- Claude Code: uses `CLAUDE.md`
- GitHub Copilot: uses `.github/copilot-instructions.md`

Taking Cursor as an example, `.mdc` rule files support YAML metadata (frontmatter), allowing you to define the scope where a rule applies. According to Cursor’s official docs, the format looks like this:

```yaml
---
description: React 组件开发规范
globs: src/components/**/*.tsx
alwaysApply: false
---
# React 规范
- 使用函数式组件
- 优先使用 hooks
```

There are multiple ways to activate a rule file, such as:

- Always active: set `alwaysApply: true`
- Pattern matching: automatically activate when referencing files that match `globs`
- Manual invocation: reference it in chat with `@rule-name`
- AI self-selection: AI automatically loads it according to task relevance

💡 Note that as tool versions continue to evolve, the names and standards of these files may change. Always treat the official documentation of the tool as the source of truth.



### AGENTS.md

[AGENTS.md](https://agents.md/) is an open file format specifically used for giving project instructions to AI coding agents. At its core, it is also a kind of Rules File, but one that serves as an open standard across tools.

![](https://pic.yupi.icu/1/image-20260201145003244.png)

The traditional `README.md` is written for humans and mainly explains what the project is and how to use it. `AGENTS.md` is written for AI and contains the technical details AI needs while working:

- The project’s build and startup commands
- How to run tests
- Coding style and standards
- Explanations of project structure

A typical `AGENTS.md` file looks something like this:

```markdown
# 项目设置
- 安装依赖：npm install
- 启动开发：npm run dev
- 运行测试：npm test

# 代码规范
- 使用 TypeScript 严格模式
- 组件文件使用 PascalCase 命名
- 工具函数使用 camelCase 命名
```

The advantage of `AGENTS.md` is that it is an open standard used by tens of thousands of open-source projects. When you use an AI coding tool that supports the standard—such as Claude Code, Codex, Cursor, or GitHub Copilot—it automatically detects the `AGENTS.md` file in the project root and sends its instructions to AI. You don’t need to reference it manually.



### SDD

SDD, short for Spec-Driven Development, is a new development methodology for the AI era. It emphasizes creating clear specification documents that AI can directly understand and execute **before** coding begins.

The traditional development flow often looks like this: write whatever comes to mind, revise while coding, and fill in the documentation later. That easily leads to unclear requirements and mismatches between code and docs.

SDD takes the exact opposite approach: **write the requirements into specification documents first, and treat those documents as the single source of truth for the code.**

You can think of the specification document as the “constitution” of the project. It contains detailed requirement descriptions, system design, and interface definitions. AI must follow those rules strictly when generating code, so the output aligns with expectations.

![](https://pic.yupi.icu/1/%25E6%25BC%25AB%25E7%2594%25BB%25E5%259B%25BE4%25E5%25A4%25A7.jpeg)

Why is SDD getting more and more attention?

Because the quality of AI-generated code depends directly on how clear the context is, not just on prompt tricks. A clear specification document can reduce errors more effectively than any prompt “black magic.”

The typical SDD workflow is:

1. Constitution: define the project’s basic principles, coding standards, and performance standards
2. Specify: describe what features need to be built, why they are needed, and what the user needs are
3. Clarify: let AI ask structured questions to clarify edge cases and error handling
4. Plan: determine the tech stack, system architecture, data model, and APIs
5. Tasks: break the plan down into an executable task list, marking dependencies and priorities
6. Implement: AI generates code according to the task list, and humans validate the result

This is actually very similar to the standard project-development workflow used by programmers in companies—the only difference is that now the executor is AI instead of a human.

![](https://pic.yupi.icu/1/%2525E6%2525BC%2525AB%2525E7%252594%2525BB%2525E5%25259B%2525BE5%2525E5%2525A4%2525A7.jpeg)

In September 2025, GitHub released the open-source [Spec Kit](https://github.com/github/spec-kit), which helps developers practice the SDD methodology in AI coding. It supports mainstream programming tools such as Claude Code and GitHub Copilot, guiding you through the flow above via a set of slash commands. Even if you are not a software development expert, AI can guide you through a proper project-development workflow with ease.

![](https://pic.yupi.icu/1/image-20260116164612533.png)



### RAG

RAG, short for Retrieval-Augmented Generation, is a technique that lets AI retrieve from an external knowledge base first and then generate an answer based on the retrieved result. Its goal is to make AI’s answers more accurate and more grounded.

Ordinary AI can only rely on the knowledge it learned during training, and that knowledge may already be outdated. RAG allows AI to first retrieve relevant information from your documents, codebase, or knowledge base before answering, and then generate its answer based on that information.

![](https://pic.yupi.icu/1/1776650476421-3bfb3c26-575d-4cc4-9538-f74a4589b42d-20260430230436685.png)

This is especially useful for Vibe Coding in enterprises, because AI can refer to the existing code in your project and generate new code in a consistent style.

The workflow of RAG is shown in the image below. If you are a programmer building AI applications, it’s worth understanding in depth:

![](https://pic.yupi.icu/1/1745810809620-15c36bc0-5130-47fc-aaca-7d2a6ce6e3ce.png)

In practical engineering, RAG has already evolved into many advanced variants.

![](https://pic.yupi.icu/1/1776651602499-afc9fc4b-6105-4b96-a3cd-a6681bf69480-20260430230542027.png)

For example:

- Multi-Query RAG: retrieve using multiple phrasings and then merge the results
- HyDE: let AI generate a hypothetical answer first and then use the vector of that answer for retrieval
- Hybrid Search: combine vector search and keyword search, then fuse and rerank the results
- Reranking: after retrieval, use a reranking model to rescore and filter noise
- GraphRAG: turn documents into a knowledge graph to support cross-document multi-hop reasoning
- Agentic RAG: equip an Agent with a set of retrieval tools and let it schedule them itself, deciding autonomously what to do at each step

There are many more variants, and different approaches fit different scenarios. You can combine them according to your actual needs.

![](https://pic.yupi.icu/1/1776652755436-d1f52895-b98a-4e33-8c86-6ce0322ace05-20260430230713947.png)

If you’re a programmer interested in RAG, you can read *An Introductory Guide to AI Coding Technology* in this tutorial’s programming-learning section, where I explain implementation choices and design suggestions in more detail.



### Agentic RAG

Agentic RAG is the evolved version of traditional RAG. It upgrades the fixed “retrieve → generate” pipeline into a closed-loop system controlled by an AI agent.

Traditional RAG is like a librarian who only knows how to follow a fixed procedure: you ask a question, it searches the shelf once, brings back something, and gives you an answer without caring whether it found the right thing.

Agentic RAG is more like an experienced researcher: it first thinks about where to search, judges whether the information found is relevant, retries with a different angle if the result is poor, and can even search multiple data sources at the same time, repeatedly verifying until it is satisfied.

![](https://pic.yupi.icu/1/1776652755436-d1f52895-b98a-4e33-8c86-6ce0322ace05.png)

The core capabilities of Agentic RAG include:

- Multi-round retrieval: retrieve multiple times as needed instead of searching only once
- Dynamic query rewriting: if the first attempt finds poor results, AI automatically rephrases and searches again
- Multi-source coordination: retrieve from vector databases, APIs, webpages, SQL databases, and other sources at the same time
- Self-correction: evaluate retrieval quality, and retry if unsatisfied

Typical patterns include CRAG (Corrective RAG, which adds a retrieval evaluator), Self-RAG (reflection steps embedded in the generation process), and Adaptive RAG (which chooses different retrieval strategies according to question type).

The cost is higher latency and several times higher Token consumption, so it is more suitable for complex, high-accuracy scenarios such as legal, medical, and compliance questions. For simple single-source queries, traditional RAG is usually enough.



### Vector Database

A Vector Database is a database specifically used for storing and querying “vectors,” which are numerical representations of things. In AI, it is often used to store the semantic representation of text.

So what is a vector?

Simply put, a vector is an array of numbers, such as `[0.1, 0.5, 0.3, 0.8]`, where each number represents one feature dimension. AI can convert a piece of text, an image, or a piece of code into this kind of vector, and semantically similar content gets converted into vectors that are numerically close to one another.

Once you store code or documents inside a Vector Database, AI can quickly find semantically similar content, even if the search words do not exactly match the original text.

![](https://pic.yupi.icu/1/1769047066536-0ef08cd3-b86b-4c97-9016-7add32a710b8.png)

For example, if you search for “user login,” it may still find a function called `"handleAuth"` because they are semantically related.

As AI has exploded, many databases that support vector storage have appeared on the market:

![](https://pic.yupi.icu/1/1745813546910-9b39355a-85ab-4673-b52b-7f11349a55d7.jpeg)




### Embedding

Embedding is the process of converting text, code, and other content into numeric vectors. Those vectors capture semantic information.

Inside vector space, semantically similar content ends up physically closer together. That is the principle behind why Vector Databases can perform semantic search.

![](https://pic.yupi.icu/1/1745812543781-8ef377d0-2dac-4d17-a504-35de13fbaad0.png)

You don’t need to deeply understand the technical details of embeddings. It’s enough to know that embeddings are one of the foundational technologies behind RAG and semantic code search.




## AI Output-Related Concepts


### AI Hallucination

AI Hallucination means AI outputs content that does not match reality. It may invent APIs that do not exist, give incorrect function usage, recommend libraries that do not exist, or simply fabricate information that sounds plausible but is completely wrong.

For example, in the conversation below, I asked AI to introduce programmer Yupi, and it confidently made things up. That’s not even my real name...

![](https://pic.yupi.icu/1/image-20260104184328898.png)

This is an inherent issue of large language models, because they generate content based on probability and may sometimes “fill in” nonexistent things.

When doing AI coding, we can reduce the impact of hallucination in several ways:

- Ask AI to provide documentation links for verification
- Check official documentation yourself
- Try another model
- Start a new conversation and describe the problem again
- Use MCP extensions such as Context7 to fetch the latest technical documentation

For programmers building AI applications, reducing hallucination is one of the most important challenges to overcome. The RAG technique mentioned earlier is currently one of the most mainstream solutions: by making AI retrieve real data before answering, the probability of hallucination drops significantly.




### Temperature

Temperature is the parameter that controls the randomness of AI output. Its value is usually between 0 and 2, although the exact range may differ between models and tools.

- Low temperature (such as 0.1): output is more deterministic and conservative, making it suitable for coding
- High temperature (such as 1.0): output is more random and creative, making it suitable for brainstorming

In programming scenarios, people generally use a lower temperature so AI generates more stable and predictable code. In scenarios that require creativity—such as naming, writing copy, or brainstorming product ideas—you can increase the temperature a bit so AI gives more diverse suggestions.

For example, in the image below, after I increased the temperature, the structure of the output became completely different:

![](https://pic.yupi.icu/1/image-20260302173616073.png)



### Streaming

Streaming means AI displays content to the user in real time as it is being generated, rather than waiting until the whole answer is finished before showing it.

It’s like watching a livestream instead of a recording. You can see AI’s generation process live, and if you realize it’s going in the wrong direction, you can interrupt it early and avoid wasting Tokens.

Most AI coding tools support streaming, which makes the interaction feel much smoother.

At the implementation level, streaming is generally based on SSE (Server-Sent Events), where the server continuously pushes chunks of data to the client for real-time display.

![](https://pic.yupi.icu/1/image-20260302173858827.png)



## Development Tool Concepts


### IDE

IDE stands for Integrated Development Environment. It is the all-in-one software programmers use to write code, usually including a code editor, debugger, terminal, extension marketplace, and more.

VS Code is currently the most popular lightweight IDE. It was developed and open-sourced by Microsoft. Cursor and Windsurf are AI code editors built on top of VS Code, inheriting its interface and functions while greatly expanding AI capabilities.

![](https://pic.yupi.icu/1/image-20260112113710320.png)




### Code Editor

A code editor is a tool used to write and modify code. It provides functions such as syntax highlighting, code completion, and error hints, helping you code more efficiently.

Common code editors include Sublime Text and Vim. Compared with a full IDE, they are lighter and launch faster, making them better for quickly editing individual files. IDEs, on the other hand, have more complete built-in features such as debuggers, terminals, and version control, making them more suitable for professional developers and large projects.

![](https://pic.yupi.icu/1/image-20260302174013740.png)

In the age of Vibe Coding, code editors have integrated AI capabilities. They can automatically generate code, explain code, and fix errors based on your prompt. Early Cursor, for example, was powerful, but at its core it was still an AI-enhanced code editor.



### CLI

CLI stands for Command Line Interface. It is the “small black box” where you type text commands to operate a computer. Its counterpart is the GUI, or Graphical User Interface, meaning the icons, buttons, and windows we use every day.

![](https://pic.yupi.icu/1/image-20260407150349886.png)

In the AI era, the CLI is experiencing a revival. It is no longer just a programmer’s special skill—it is becoming the natural interface between AI and tools.

Why has the CLI suddenly become so popular?

Because large AI models have been learning massive amounts of code and command-line operations since the day they were born. Asking AI to read one command and perform one operation is about as natural as drinking water. Asking AI to operate a graphical interface is much harder—it has to analyze screenshots, locate elements, simulate clicks, and the whole process is slower and more error-prone. Some tests have shown that AI’s success rate at completing tasks through a browser is only 35.8%, while using the CLI pushes it close to 100%.

![](https://pic.yupi.icu/1/image-20260407123223554.png)

That’s why major companies are now open-sourcing CLI tools for their own products, such as Google, Feishu, DingTalk, and WeCom. At its core, they are giving AI an interface for operating their products.

In the past, product teams only thought about how human users would use the product. Now they also need to think about how AI will use it. So products of the future may end up having two frontends: a GUI for humans, and a CLI for AI.

If you want to learn more about how to use and build CLI tools, you can read *AI Command-Line Programming Tools* in this tutorial’s programming-tools section.



### No-Code Platform

A No-Code Platform is a platform that lets you create applications without writing code. Closely related are Low-Code Platforms, which let you build applications through a small amount of code plus visual drag-and-drop, offering a bit more flexibility.

In the AI era, platforms such as Bolt.new, Lovable, v0.dev, and Baidu Miaoda combine no-code with AI. You can describe requirements in natural language, and the platform automatically generates a complete application that can be accessed online.

No-Code Platforms are especially suitable for complete beginners who have no programming experience at all, or for scenarios where you want to quickly build a prototype. The downside is also obvious: when problems happen, they are harder to debug, hard to customize deeply, and once a project gets large, bottlenecks are easy to hit.

![](https://pic.yupi.icu/1/image-20260104141512389.png)




### Code Completion

Code Completion means AI automatically predicts what you are likely to write next based on the current code context and offers suggestions.

As you code, AI infers your intent from context and presents candidate code snippets for you to choose from. Pressing the Tab key accepts the suggestion, dramatically increasing coding speed.

![](https://pic.yupi.icu/1/image-20260302174238835.png)

As early as 2021, GitHub launched Copilot and pioneered AI code completion. But nobody expected that only a few years later, AI would evolve from “completing a few lines of code” to “autonomously building an entire project.” Today, all major AI coding tools support code completion, but more and more developers are no longer satisfied with line-by-line completion. Instead, they directly use Agent mode to have AI write an entire feature in one go.



### Code Review

Code Review is the process of checking code quality, discovering problems, and proposing improvements.

Without Code Review, bugs are often discovered only after launch, when fixing them is much more expensive. With Code Review, many problems can be discovered and fixed before the code is merged.

In traditional development, Code Review is usually done by colleagues or supervisors. In Vibe Coding, you can let AI help review code. It can point out potential bugs, security issues, and performance problems, and provide revision suggestions.

![](https://pic.yupi.icu/1/image-20260112114023226.png)

That said, AI review can never completely replace human review—especially for important production code.




### Linter

A Linter is an automated tool for checking code problems. It can detect syntax errors, style issues, potential bugs, and more.

Common linters include ESLint for frontend code, Pylint for Python, and golint for Go. They act like strict grammar teachers who help keep your code standardized.

In Vibe Coding, linters help you quickly discover issues in AI-generated code. And many times, when AI helps you create a frontend project, it will automatically integrate linters such as ESLint for you, saving you the trouble of configuring them manually.

![](https://pic.yupi.icu/1/image-20260116131356553.png)




### Debug

Debugging is the process of finding and fixing errors in code. When the running result does not match expectations, you need debugging to locate the issue.

Common debugging methods include:

- Setting breakpoints and stepping through the code
- Inspecting variable values
- Reading error messages and stack traces
- Adding log output

![](https://pic.yupi.icu/1/image-20251027214825243.png)

When doing AI coding, you can directly send error messages to AI and ask it to analyze the cause, provide a fix, or even fix it autonomously.



### OpenClaw

[OpenClaw](https://github.com/openclaw/openclaw) is one of the most phenomenal open-source AI projects of 2026. In just over 100 days, it climbed to the top of GitHub’s all-time star rankings and gained more than 300,000 Stars.

You can think of it as an AI digital employee that can operate your computer. It is not just a chatbot. It can actually open software, operate browsers, process files, and execute code for you. More importantly, you can issue tasks to it anytime and anywhere through chat apps on your phone—such as Feishu, QQ, or WeChat—and AI will automatically complete those tasks on your computer.

![](https://pic.yupi.icu/1/1773231001520-f08121d8-de2c-4586-9af2-42cb0c728961-20260311204057246.png)

The features of OpenClaw include:

- Actually executes tasks: can operate browsers, process files, write code, manage schedules, and more
- Multi-channel access: supports WeChat, QQ, Feishu, Telegram, Discord, and others
- Skill ecosystem: extends AI capabilities by installing different skill packs
- Multi-model support: supports Anthropic, OpenAI, and Chinese large models
- Fully open source: MIT license, supports local deployment, and keeps data in your own hands

But OpenClaw has very broad permissions, so you must pay attention to safety when using it. If you want to learn more about installation, usage, and precautions, you can read *OpenClaw Beginner-Friendly Installation Tutorial* in this tutorial’s programming-tools section, or *The Complete OpenClaw Beginner-Friendly Tutorial* in Yupi’s AI knowledge base.



## Project Management Concepts


### MVP

MVP stands for Minimum Viable Product. It refers to a product version that satisfies the core requirement with the minimum possible feature set—in simple terms, the smallest version that “runs” and whose core function already works.

When many people first start building products, they come up with all kinds of wild ideas and want to implement every feature at once. As a result, they spend huge amounts of time on unnecessary features, the project gets more and more complex, and in the end they give up because it feels too hard. They basically scare themselves away. The MVP mindset is the opposite: first use the smallest feature set to validate the core value quickly, then gather user feedback and iterate from there.

For example, if you are building an expense-tracking app, the MVP may include only “record expense” and “view list,” with all advanced features added later.



### Iterative Development

Iterative Development is a development method that splits a large project into multiple small cycles, with each cycle completing part of the functionality.

Each iteration cycle includes: plan → develop → test → release → feedback → improve.

This method is especially suitable for Vibe Coding, because you can let AI first implement the core functionality, test it, and then gradually add new features after the core works.

By the way, iterative development is also one of the core practices of Agile Development. Agile emphasizes moving fast in small steps, rapid feedback, and embracing change—all of which fit the working rhythm of AI coding very well.

![](https://pic.yupi.icu/1/%E8%BF%AD%E4%BB%A3%E5%BC%80%E5%8F%91%E5%A4%A7.jpeg)



### Refactoring

Refactoring is the process of improving code structure and quality without changing the functionality.

The goal of refactoring is to make code clearer, easier to maintain, and more efficient. Common refactoring actions include:

- Extracting repeated code into functions
- Improving variable and function names
- Simplifying complex logic
- Splitting overly long files

In Vibe Coding, you can ask AI to help refactor code, but you should do it in small steps and test after each refactor.

One thing to remember: if you are just using AI to quickly build a small tool, it may be enough that the code simply runs, and there is no need to spend extra time refactoring. But for a long-term enterprise project, code quality directly determines the efficiency and stability of future iterations, so regular refactoring becomes very important.



### Technical Debt

Technical Debt refers to temporary solutions adopted to quickly complete functionality, which will require time to fix and improve later.

It is like credit-card debt: spending now is convenient, but sooner or later you still have to pay it back, and usually with interest.

In Vibe Coding, AI-generated code may not always be the best solution. If you accumulate too much Technical Debt, the project becomes harder and harder to maintain. Regular refactoring is an effective way to repay Technical Debt and prevent the codebase from turning into a giant mess.

![](https://pic.yupi.icu/1/v2-806707f0f72072f1db481c237fc035ea_1440w-20260112114757928.png)



### Version Control

Version Control is a system that records the history of code changes, allowing you to track each modification, compare different versions, and roll back to previous states.

Git is the most popular Version Control tool. Be careful not to confuse it with GitHub: Git is the tool that runs on your own computer, while GitHub is an online code-hosting platform used to store and share the code you manage with Git.

In Vibe Coding, Version Control is especially important. Because AI may generate problematic code, Version Control lets you roll back at any time to an earlier working version.

![](https://pic.yupi.icu/1/image-20260112114940228.png)



### Git WorkTree

Git WorkTree is one of Git’s hidden superpowers. It allows a single repository to have multiple independent working directories at the same time, with each directory corresponding to a different branch.

Under normal circumstances, one Git repository has only one working directory, so you can only work on one branch at a time. If you want to switch branches, you usually have to save your current work and keep jumping back and forth. But once you use WorkTree, you can create “clones of yourself” and work on different branches at the same time without interference.

![](https://pic.yupi.icu/1/image-20260410143507942.png)

The difference from manually copying the project folder is this: manual copying duplicates the full `.git` directory and history, wasting more disk space and making code merging troublesome. WorkTrees, by contrast, only create linked working directories pointing to the same `.git` directory, sharing the same commit history, which saves space and makes merging easier.

![](https://pic.yupi.icu/1/image-20260410143527245.png)

In the era of AI coding, the most enjoyable use of WorkTree is letting multiple AIs develop in parallel. For example, if you have three features to build—homepage, search, and personal center—you can create three worktrees, assign each one to a different AI, let them work independently, and then merge the code with Git afterward.

![三个 AI 同时干活](https://pic.yupi.icu/1/vscode%E4%B8%89%E4%B8%AA%E5%90%8C%E6%97%B6%E5%B9%B2%E6%B4%BB.png)

AI coding tools such as Cursor already have built-in WorkTree support. You can directly enable Parallel Agents mode and let the tool automatically create and manage worktrees.

One thing to remember: when assigning tasks, try to make different AIs modify different files. If two AIs modify the same file, merge conflicts will occur and you’ll need to resolve them manually.



### Deployment

Deployment means publishing a developed application to a server so users can access and use it.

The most primitive deployment method is logging into a server yourself, packaging and uploading code files, and then starting things manually. It’s troublesome and easy to make mistakes. Fortunately, there are now many automated deployment platforms that make deployment foolproof—just a few clicks and your project goes live. Common ones include:

- Vercel: suitable for frontend and full-stack applications
- Netlify: suitable for static websites and frontend applications
- Railway and Render: suitable for backend services

![](https://pic.yupi.icu/1/image-20260302175217005.png)

Many no-code platforms, such as Bolt.new, also support one-click deployment. Press a button and your app is online.

In addition, MCP can also be used for smarter deployment. For example, through EdgeOne Pages MCP, you only need to talk to AI, and AI can automatically package and deploy the website for you—you don’t even need to log in to the deployment platform yourself~

![](https://pic.yupi.icu/1/1752212029384-16cfba8f-babb-49c0-9d41-3b76ee78eecf.png)



### GEO

GEO stands for Generative Engine Optimization. You can think of it as SEO for the AI era.

Traditional SEO focuses on “how to make a webpage rank high in Baidu or Google search results,” while GEO focuses on “how to make your content get cited and recommended by AI large models such as ChatGPT, DeepSeek, and Doubao.”

![](https://pic.yupi.icu/1/image-20260327155157265-20260328131543764.png)

To use an analogy, SEO is like fighting for the best shelf position in a supermarket, while GEO is like getting the store clerk to proactively recommend your product when a customer asks.

![](https://pic.yupi.icu/1/image-20260327163145093.png)

As more and more people use AI search instead of traditional search engines, GEO is becoming increasingly important. Some data shows that traffic conversion from AI search can reach more than five times that of traditional search!

The core strategies of GEO include:

- Give the conclusion first: answer the core question directly at the beginning, because AI especially likes extracting content that gives the answer up front
- Structured writing: use clear heading hierarchy, Q&A formats, and comparison tables to make AI parsing and citation easier
- Build authoritative content: use concrete data and authoritative citations rather than vague descriptions, because AI trusts verifiable content more
- Publish more on authoritative platforms: content posted on high-authority platforms such as Zhihu, WeChat Official Accounts, and GitHub is easier for AI to crawl
- Technical optimization: make sure `robots.txt` allows AI crawlers and use SSR or SSG to ensure the page can actually be crawled

It’s worth noting that GEO itself is a neutral technology. Like SEO, it is simply a content optimization method. And doing SEO well also helps GEO. The two do not conflict.

For developers who want more people to discover their products, both SEO and GEO are valuable promotion skills worth learning. If you want to go deeper, you can read *SEO Search Engine Optimization in Practice* and *GEO Generative Engine Optimization in Practice* in this tutorial’s product-monetization section.



## Frontend and Backend Concepts


### Frontend

Frontend is the part users can directly see and interact with, including webpage interfaces, buttons, forms, animations, and so on. To put it bluntly, everything you see in the browser is frontend!

The frontend tech stack usually includes:

- HTML: page structure
- CSS: styling and layout
- JavaScript: interaction logic
- React / Vue / Next.js: modern frontend frameworks

In Vibe Coding, frontend is the part AI is best at generating, because the result can be directly seen, making it easy to verify and adjust. You can also use Agent Skills and carefully written prompts to beautify AI-generated frontend pages and remove that obvious “AI vibe.” For practical tips, you can watch Yupi’s video: [How to Remove the AI Smell from a Website](https://www.bilibili.com/video/BV1QF6EBiErM/)




### Backend

Backend is the part users cannot see. It is responsible for business logic, data storage, user authentication, and so on.

For example, when you click the “Place Order” button on an e-commerce site, the frontend sends your order information to the backend. The backend checks inventory, calculates price, deducts payment, creates the order, and then returns the result to the frontend for display.

The backend tech stack usually includes:

- Node.js / Python / Java: programming languages
- Express / FastAPI / Spring: web frameworks
- MySQL / PostgreSQL / MongoDB: databases

Backend is usually more complex than frontend, because it must consider issues such as security, performance, and data consistency. So AI-generated backend code needs more careful review.

![](https://pic.yupi.icu/1/%E5%89%8D%E7%AB%AF%E5%92%8C%E5%90%8E%E7%AB%AF%E4%BA%A4%E4%BA%92%E5%A4%A7.jpeg)




### Full-stack

Full-stack means a complete application that includes both frontend and backend. A full-stack developer is a programmer who can handle both frontend and backend work.

In Vibe Coding, AI coding tools such as Cursor and Bolt.new can generate full-stack applications in one shot, writing both the frontend and backend code for you.

If you want to further understand what a full-stack programmer is and how to become one, you can read Yupi’s article: [What Is a Full-stack Programmer?](https://www.bilibili.com/opus/534338036646820466)




### API

API stands for Application Programming Interface. It is the interface through which different programs communicate.

You can think of an API as a restaurant menu. The menu tells you what dishes can be ordered, how to order them, and what you will get afterward. You do not need to know how the kitchen cooks the food—you just order according to the menu.

In web development, the frontend communicates with the backend through APIs in order to fetch data or submit operations.

![](https://pic.yupi.icu/1/1766718929375-35cd24d6-077e-4a5e-8cbb-7725edf8098f-20260112120508019.png)

If you want to understand APIs and standard API design specifications more deeply, you can watch [Yupi’s animated science video about APIs](https://www.bilibili.com/video/BV1WFBXBmExs).




### Database

A Database is a system for storing and managing data. User information, content, settings, and other application data are all stored inside databases.

Common database types include:

- Relational databases (MySQL, PostgreSQL): data stored in table form
- Document databases (MongoDB): data stored as JSON-like documents
- Key-value databases (Redis): suitable for caching and rapid lookup

![](https://pic.yupi.icu/1/1764309581505-2ff17977-695f-4d7c-a779-b5d35ad99d6b.png)

![](https://pic.yupi.icu/1/1764309606178-1af81d82-b320-4bed-9c97-5dfe3847d8d3.png)

In Vibe Coding, you can use ready-made cloud database services such as Supabase or Firebase instead of building and managing databases yourself.

If you want to systematically learn database fundamentals, you can check out Yupi’s beginner tutorial: [Database Beginner Tutorial](https://www.bilibili.com/video/BV1iJSLBbEyD/)



### BaaS

BaaS stands for Backend as a Service. It refers to cloud services that provide ready-made backend functionality, including databases, user authentication, file storage, and so on.

Before BaaS, you had to buy servers, install databases, write backend APIs, and deal with all kinds of operational tasks yourself. Even setting up the environment took a long time. With BaaS, all of those things are already prepared. You don’t need to write backend code yourself or manage servers—just create an account and start using it. That can dramatically speed up development, making it especially suitable for Vibe Coding scenarios.

Common BaaS services include:

- Supabase: an open-source alternative to Firebase
- Firebase: Google’s BaaS platform
- PlanetScale: a managed MySQL service

![](https://pic.yupi.icu/1/image-20260302175641346.png)



## Final Thoughts

This article covers the most common concepts and terms in Vibe Coding. Of course, the worlds of AI and programming keep producing new concepts all the time, so this glossary will continue to be updated.

You do not need to memorize everything at once. When you run into a term you don’t understand, just come back and look it up—or ask AI about it. As you keep practicing Vibe Coding, these concepts will gradually become familiar naturally.




## Recommended Resources

1) Yupi AI Navigation site: [AI resources, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning community: [learning paths, programming tutorials, practical projects, job-hunting guides, discussion and Q&A](https://www.codefather.cn)

3) Programmer interview knowledge base: [high-frequency topics for internships / campus recruiting / experienced hires, real company question analysis](https://www.mianshiya.com)

4) Resume-writing tool for programmers: [professional templates, rich sample sentences, direct path to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [essential for landing offers in internships / campus recruiting / experienced-hire interviews](https://ai.mianshiya.com)
