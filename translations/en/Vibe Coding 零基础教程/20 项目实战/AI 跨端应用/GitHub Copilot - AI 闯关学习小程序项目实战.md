# GitHub Copilot - AI Level-Based Learning Mini Program Project in Action

This is a project tutorial centered on hands-on AI programming. Based on Taro + Python FastAPI + LangChain + LangGraph + DeepSeek, it takes you from 0 to 1 to build an "AI Level-Based Learning WeChat Mini Program" through AI programming, and walks through the entire deployment and launch process, letting you personally experience the complete workflow of AI Vibe Coding and learn how to build a mini program product that can go live, spread, and monetize!

Project code is open source for free: https://github.com/liyupi/yu-ai-learn

Full video tutorial + written tutorial (estimated 3–7 days to complete): https://www.codefather.cn/course/2037104890135748610

![](https://pic.yupi.icu/1/1-project-demo-overview.png)

## Project Introduction

When it comes to learning, the biggest enemy is boredom. You read docs and watch videos, but before long your mind drifts, and even after finishing, you still can’t remember much.

But people naturally love games. They like clearing levels, answering questions, and earning rewards. So now that we have AI, why not let AI automatically turn **any knowledge I want to learn** into a game-like challenge?

That’s the starting point of this project: the user types a single sentence describing what they want to learn, the AI automatically searches the web for the latest materials and generates a set of challenge questions, and the user learns while answering them. After each question, the system immediately gives the answer and explanation, and after clearing the level, the user also gets an AI-generated review report.

Why make it a WeChat Mini Program instead of an app or website? Because users often learn small bits of knowledge in fragmented moments. WeChat Mini Programs require no installation, can be opened anytime and anywhere, benefit from WeChat’s traffic ecosystem, and are easy to share with friends to keep each other motivated. For a learning product, it’s almost the ideal form.

More importantly, the skeleton of this project can be directly reused in any vertical domain. Swap out the knowledge source and it becomes a new product—for example, a driving theory quiz app, interview question bank, enterprise internal training and assessment system, professional certification exam review tool, English vocabulary challenge game, and so on.

![](https://pic.yupi.icu/1/2-driving-theory-quiz-flow.png)

## Project Feature Demo

1) Enter the knowledge you want to learn, and the AI automatically creates questions

In the input box on the home page, describe what you want to learn in one sentence or a paragraph, choose the question difficulty and quantity, then click “Start Generating Questions.” The AI will automatically search the web for relevant materials and generate a set of challenge questions containing single-choice, multiple-choice, and true/false question types.

![](https://pic.yupi.icu/1/3-vibecoding-web-search-and-correct-answer.png)

2) Answer level-based questions and get explanations immediately

Once the questions are generated, you enter the challenge page. At the top, there’s a progress bar and coin count. After each question, the system immediately tells you whether you were right or wrong, and gives the explanation and corresponding knowledge point so you can learn while playing.

![](https://pic.yupi.icu/1/4-vibecoding-wrong-answer-and-submit.png)

3) AI generates a post-level review report

After finishing a set of questions, the AI generates a review report based on your answers, including a mastery score, weak knowledge points based on incorrect answers, a knowledge summary, and next-step study suggestions. It also calculates the experience points earned in this round.

![](https://pic.yupi.icu/1/5-vibecoding-report-and-question-review.png)

4) AI web search keeps the questions from going out of date

Large models have knowledge cutoffs. If you ask them to generate questions directly, it’s easy to end up with outdated or even wrong questions. So in this project, the question-generation stage is connected to web search, allowing the AI to first decide for itself whether to search and what keywords to search, then generate questions after obtaining up-to-date materials.

Essentially, this upgrades “question generation” from a simple single LLM call into an AI Agent that can search the web for materials on its own. It also includes a full fallback strategy: if search is unavailable, it automatically falls back to using the model’s own knowledge to generate questions, so the main flow is not disrupted.

![](https://pic.yupi.icu/1/6-yupi-ai-nav-search-and-quiz.png)

5) Upload your own knowledge base and generate questions from private documents

On the “Me” page, you can enter the knowledge base and upload documents in PDF, Word, Markdown, or TXT format. The system will automatically split the documents into chunks, convert them into vectors, and store them in a vector database. After that, you can choose a document and generate questions entirely based on your private materials.

This capability expands the project from “learning public knowledge” to “testing yourself on your own materials,” making it useful for scenarios like enterprise internal training, targeted question-bank review, and exam cramming.

![](https://pic.yupi.icu/1/7-knowledge-base-upload-and-quiz.png)

6) AI adds images to questions for a more intuitive learning experience

When generating questions, you can check “Generate Illustrations,” and the AI will generate an image for each question based on its knowledge point. For example, when reviewing English vocabulary, the question “What is the English word for apple?” can come with an apple image, making the experience much more intuitive and fun.

The generated images are automatically copied into object storage to obtain permanent access links, preventing image failures caused by expiring temporary links returned by AI image-generation APIs. The project also includes daily quota limits and multi-question concurrency control to balance user experience and cost.

![](https://pic.yupi.icu/1/8-ai-generated-illustration-quiz.png)

7) One-click WeChat login and always-available challenge history

The mini program uses WeChat silent login, so users can get an account through seamless authorization. Challenge records, experience points, and answer history are all persistently stored. On the “Me” page, users can view their total experience points and challenge history list, and can click into any record to review the AI report from that session.

At the same time, the project adopts an “optional login” design. Users can still experience question generation and answering without logging in, but their records won’t be saved, minimizing the barrier for new users.

![](https://pic.yupi.icu/1/9-profile-and-history.png)

8) Actually goes live and can be found in WeChat search

This project is not something you just build and leave locally. The tutorial will take you through containerizing and deploying the backend to a container hosting platform, replacing local MySQL with a cloud database, and completing the entire mini program release process so anyone can search for and use the mini program you built in WeChat.

![](https://pic.yupi.icu/1/image-20260811183313570.png)

## Feature Breakdown

This project is feature-rich, covering 6 major modules—challenge answering, AI question generation, review reports, user system, knowledge base, and AI illustrations—with 30+ feature points that cover the core business scenarios of a real live mini program.

![](https://pic.yupi.icu/1/image-20260811155000927.png)

Challenge answering module:

- Freely enter the knowledge you want to learn (a sentence or a paragraph)
- Optional difficulty selection (easy / medium / hard / mixed)
- Optional number of questions (3 to 10)
- Three question types: single-choice, multiple-choice, and true/false
- Instant scoring after each question, with the correct answer shown
- Explanations and corresponding knowledge points for each question
- Level progress, correct answer count, and coin display

AI question generation module:

- DeepSeek LLM generates the questions
- Tavily web search supplements the latest knowledge
- Search Agent independently decides what to retrieve
- Prompt constraints make the LLM output structured JSON
- Question structure parsing and field validation
- Asynchronous task creation and status transitions
- Frontend polling to get question-generation progress
- Automatic fallback when search is unavailable

Review report module:

- AI-generated post-level review report
- Mastery score and progress bar display
- Weak knowledge point identification
- Three-sentence knowledge summary
- Next-step study recommendations
- Share-text generation
- Experience reward calculation

User system module:

- WeChat silent login (exchange for `openid`)
- JWT token issuance and validation
- Optional login mode (usable even without login)
- Personal center (nickname, avatar, experience points)
- Edit personal profile
- Challenge history list (pagination)
- Challenge detail review

Knowledge base module:

- Upload PDF, Word, Markdown, and TXT documents
- Parse documents and split them into text chunks
- Vectorize the text chunks and write them into a vector database
- User-isolated vector collections
- Document parsing status polling
- Document list and deletion
- Document count and single-file size quotas
- RAG-based question generation from a specified document

AI illustration module:

- Build image prompts based on each question’s knowledge point
- Call image-generation models to create illustrations for questions
- Copy images to object storage for permanent links
- Multi-question concurrent image generation (semaphore controlled)
- Daily image-generation quota limits
- Image-generation failures do not affect the main question-generation flow

## Project Takeaways

This project has a fresh topic and keeps pace with the AI programming era. Unlike overused CRUD projects, you’ll start from a single idea, practice the most mainstream AI programming methods, and launch a real product that people actually want to use.

The project content is streamlined and can be finished in less than a week. You’ll quickly master the core workflow of AI programming: requirement research → solution design → UI prototyping → frontend and backend development → testing and acceptance → bug fixing → feature iteration → deployment and launch, letting you truly experience the full process of enterprise-grade AI programming.

From this project, you can learn:

- How to use AI for requirement research and competitor analysis, and draw the boundary between MVP and extended features?
- How to configure MCP and Agent Skills to fully expand the capabilities of AI programming tools?
- How to let multiple AI tools “race” to produce UI prototypes and create polished interfaces?
- How to use AI to build a WeChat Mini Program from scratch, including cross-platform framework selection, scaffold initialization, and page development?
- How to orchestrate LLMs with LangChain so the AI can stably output structured JSON question data?
- How to use LangGraph to build a ReAct agent and upgrade a single LLM call into an AI Agent that can actively search the web for materials?
- How to implement a full RAG knowledge base from scratch, including document parsing, chunking, vectorization, and retrieval-augmented question generation?
- How to integrate AI image generation with object storage to turn temporary image links into permanent usable assets?
- How to use OpenSpec for specification-driven development so AI can produce stable outputs in long-running projects?
- What is Harness Engineering? How do you build scaffolding for AI?
- How to containerize and deploy the project with Docker and complete the full mini program release process?

This project is especially suitable for:

- People who want to learn AI programming (Vibe Coding) but don’t know which project to start with
- People who want to build their own WeChat Mini Program and turn an idea into a product that can spread and monetize
- People who want systematic hands-on practice with core AI app development capabilities (Agent, RAG, structured output, AI image generation)
- People who want a complete project that covers the full process from requirements to launch and can even be used directly as a graduation project
- Students who want to learn Python backend and mini-program frontend development and quickly fill in their full-stack skills

## AI Programming Development Workflow

This project follows the most mainstream AI programming project development workflow, using GitHub Copilot as the main AI programming tool, paired with Claude Code for UI prototyping, and managing the long-running project through OpenSpec specification-driven development.

Step 1: Requirements analysis. First, manually analyze requirements, clarify the target users, core pain points, and MVP boundaries, then use Gemini Deep Research for AI-powered requirement research and competitor analysis. After cross-validation, confirm the requirements document.

Step 2: Solution design. Let AI assist with technology selection, then manually review and revise it to finalize the tech stack (Taro + FastAPI + LangChain), design the question-generation prompt and structured output format, and produce the solution design document.

Step 3: UI prototyping. Let Claude Code and GitHub Copilot “race,” each producing an HTML prototype. Then deeply optimize by combining the strengths of both approaches, and finalize the UI style and design system as the visual baseline for subsequent development.

Step 4: Core feature development. Write development prompts to let AI generate frontend and backend code, integrate the DeepSeek model for AI question generation, and get the core business flow of “input → question generation → answering → report” running.

Step 5: Continuous iteration. Gradually complete modules such as the user system, web search Agent, RAG knowledge base, and AI illustration generation. After each feature is completed, commit the code with Git. When the context gets too long, open a new conversation window, and use OpenSpec to archive documents so the AI can recover its memory.

Step 6: Deployment and launch. Containerize and deploy with Docker to WeChat Cloud Hosting, then complete the full mini program release process.

![](https://pic.yupi.icu/1/image-20260811154816415.png)

## Core Business Flow

### User Flow

The entire user flow is very simple: open the mini program → enter the knowledge you want to learn → wait for the AI to generate questions → answer and clear the level → view the review report. A complete learning loop takes just a few minutes.

![](https://pic.yupi.icu/1/01_%E7%94%A8%E6%88%B7%E4%BD%BF%E7%94%A8%E6%B5%81%E7%A8%8B_compressed_v1.png)

### AI Asynchronous Question Generation Flow

AI question generation first requires web search and then LLM reasoning, so the entire process may take dozens of seconds. But WeChat Mini Programs have timeout limits for a single request. So instead of waiting for the result directly, the question-generation API creates a background task and immediately returns a task ID, while the frontend polls for progress.

![](https://pic.yupi.icu/1/02_AI%E5%BC%82%E6%AD%A5%E5%87%BA%E9%A2%98%E6%B5%81%E7%A8%8B_compressed_v2.png)

If exceptions occur during search or image generation, they will not cause the entire task to fail. If search fails, the system falls back to using the model’s own knowledge to generate questions. If image generation fails, it simply generates questions without images, ensuring that the core path always remains available.

### Knowledge Base RAG Question Generation Flow

After a document is uploaded, the system completes parsing, chunking, and vectorization in the background. After that, it can generate questions based on that document. The retrieval stage uses Agentic RAG, meaning the AI itself decides what to retrieve and how many times to retrieve it.

![](https://pic.yupi.icu/1/03_%E7%9F%A5%E8%AF%86%E5%BA%93RAG%E5%87%BA%E9%A2%98%E6%B5%81%E7%A8%8B_compressed_v1.png)

## Technology Stack

This project centers on a Taro WeChat Mini Program + Python FastAPI + LangChain / LangGraph, with frontend-backend separation and a combination of multiple mainstream mini-program and AI application development technologies.

![](https://pic.yupi.icu/1/image-20260811155041400.png)

Mini-program frontend: Taro 4 cross-platform framework, React 18 + Hooks, TypeScript, Sass, unified request encapsulation with Taro.request, WeChat Developer Tools

Backend: Python 3.11+, FastAPI web framework, Pydantic v2 data validation, Uvicorn ASGI server, asyncio asynchronous background tasks, aiomysql async connection pool, PyJWT login tokens, pytest testing

AI-related: LangChain AI app development framework, LangGraph ReAct Agent, Tavily web search API, Chroma vector database, DeepSeek LLM, Alibaba Bailian Embedding model, Tongyi Qianwen image-generation model, structured output (prompt constraints + JSON parsing + model validation)

Data and storage: MySQL 8, Chroma local persistence, Tencent Cloud COS object storage, WeChat `code2Session` API, JWT stateless login state

Deployment and launch: WeChat Cloud Hosting Docker container hosting, cloud MySQL database, mini-program service category application, ICP filing, code review and public release

AI programming tools: GitHub Copilot as the main AI programming tool (including free plan), Claude Code CLI AI programming tool, OpenSpec specification-driven development, MCP plugins (Firecrawl web search, Context7 latest technical docs, Playwright browser automation), Agent Skills (frontend design, image understanding), Harness Engineering, Gemini Deep Research

## Architecture Design

This project adopts a frontend-backend separated architecture. The frontend is a WeChat Mini Program compiled by Taro, and the backend is a FastAPI service communicating over HTTPS APIs.

Inside the backend, it is layered into the routing layer, business service layer, and data access layer. Time-consuming AI tasks are managed through in-process asynchronous tasks plus database state tables, and the frontend polls for the result.

Capabilities such as retrieval enhancement and AI-generated illustrations are connected to multiple external services, while data is stored separately in a relational database, vector database, and object storage.

![](https://pic.yupi.icu/1/image-20260811155136853.png)

Full video tutorial + written tutorial (estimated 3–7 days to complete): https://www.codefather.cn/course/2037104890135748610

## Recommended Resources

1) Yupi's AI navigation site: [AI resource collection, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning circle: [Learning paths, programming tutorials, hands-on projects, career guides, Q&A](https://www.codefather.cn)

3) Programmer interview cheatsheet: [Internship/campus/social recruitment key points, enterprise question analysis](https://www.mianshiya.com)

4) Programmer resume tool: [Professional templates, rich examples, direct to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [Essential for internship/campus/social recruitment interviews to get offers](https://ai.mianshiya.com)
