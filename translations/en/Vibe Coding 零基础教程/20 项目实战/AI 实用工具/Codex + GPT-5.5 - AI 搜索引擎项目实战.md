# Codex + GPT-5.5 in Action: Build an AI Search Engine Step by Step

You’ve probably already noticed that search engines have fully evolved now.

In the past, searching meant typing in keywords and then sifting through a pile of blue links yourself.

Now, you can just type in a question, and AI will search the web, aggregate and analyze the information, and give you a complete answer with citations.

For example, Perplexity, which focuses on AI search, is said to have surpassed 100 million monthly active users; Google, Baidu, and Bing have also all added AI summaries to their search results.

Search is shifting from **people looking for information** to **AI helping people find information**.

![](https://pic.yupi.icu/1/image-20260512151649430.png)

So how exactly is an AI search engine implemented?

In this article, I’ll use Codex + GPT-5.5 from start to finish to build an AI search engine, with the backend connected to DeepSeek V4 for AI-powered web search and intelligent summarization. After reading it, you’ll not only learn the workflow patterns of AI coding and get a feel for the capabilities of new development tools and models, but also pick up the development mindset behind AI Agent applications.

I recommend bookmarking this. Let’s begin~



## Requirement Analysis

The project we’re building this time is the `yupi-ai-search` AI search engine, modeled after Perplexity.

One thing to note is that an AI search engine is different from a normal AI chat application. If you only let AI answer a question, it uses old knowledge from its training data, so the answer may be outdated. The key to an AI search engine is **web search capability**—AI must first search online for the latest information and then answer based on that information so the result stays accurate and timely.

The specific requirement is: the user enters a question, the system automatically searches the web for the latest information, then hands it to an AI large model for combined analysis to generate an intelligent answer with cited sources. At the same time, it should also display a full list of search results like a traditional search engine. Users can also continue exploring through suggested related questions.

![](https://pic.yupi.icu/1/image-20260512142357593.png)



## Solution Design

This project uses a separated frontend-backend architecture, with Vue 3 on the frontend and Python FastAPI + LangChain on the backend.

However, traditional frontend and backend technologies aren’t the main point here. The real keys to building an AI search engine are two things: a search service that retrieves the latest information from the web, and an AI large model that understands the search results and generates a synthesized answer.

For the AI model, I chose DeepSeek V4 to test how it performs in a real business scenario.

The true core question of this project is: how should the search service be implemented?



### Search Service

Let’s first briefly talk about how search engines work.

A traditional search engine basically does 3 things:

1. Crawl web pages by sending crawlers all over the internet
2. Build indexes by organizing webpage content into a database
3. Rank and display the results based on relevance

Google, Baidu, and other major search engines run this system on hundreds of thousands of servers.

![](https://pic.yupi.icu/1/01_%25E6%2590%259C%25E7%25B4%25A2%25E5%25BC%2595%25E6%2593%258E%25E5%258E%259F%25E7%2590%2586%25E7%25A4%25BA%25E6%2584%258F%25E5%259B%25BE_compressed_v1.png)

If this were the old days and you had to build a search engine yourself, it would’ve felt impossible. Just the step of crawling the web would be enough to scare most people away.

But now things are different. With AI coding tools and ready-made search engine API services, you don’t need to crawl pages or build indexes yourself. Just call an API to get search results, then hand them to AI for summarization.

Nowadays there are already quite a few search services designed specifically for AI applications, such as Tavily Search, Firecrawl, and Brave Search API. They all return structured search results through APIs that can be used directly by AI.

![](https://pic.yupi.icu/1/image-20260512152607731.png)

Below, I’ll focus on the Tavily Search service used in this project.



### Tavily Search

Tavily Search is currently one of the most mainstream search APIs in AI application development. In fact, Tavily is also the search tool officially recommended first by the well-known AI application framework LangChain.

It has several advantages:

1. It returns structured search results (title, URL, content summary) instead of raw HTML, so you can hand them directly to AI and save tokens
2. Search is fast—results usually come back in about 3 seconds
3. LangChain has an official integration package, `langchain-tavily`, so it only takes a few lines of code to connect
4. It supports Chinese search, and you can optimize Chinese results by setting the `country` parameter to China

As for pricing, the free version gives you 1,000 API calls per month with no credit card required, which is more than enough for personal projects and MVP validation. Pay-as-you-go costs $0.008 per call, and the Growth plan is $500 per month for 100,000 calls, so if you go live at scale, you still need to pay attention to costs.

Let me give everyone a quick taste of it.

Go to the [Tavily official website](https://www.tavily.com), and you’ll see it offers four kinds of capabilities, including web search, webpage content extraction, crawling, and deep research.

![](https://pic.yupi.icu/1/1776256669936-290f2a07-4b99-4f2e-8917-5a8f5c8ee120.png)

After logging in, go to the admin panel and get your API Key:

![](https://pic.yupi.icu/1/1776256874935-687296a6-8edc-4732-9a8c-eab3682f1362.png)

Then open the [playground](https://app.tavily.com/playground), where you can verify the search effect.

For example, I searched for “programmer Yupi,” and you can see it returned structured JSON results. Each result contains a title, URL, and content summary. It found my blog, GitHub homepage, and more—pretty comprehensive.

![](https://pic.yupi.icu/1/1776257119230-8368e83e-ec3e-4e27-ac3e-62ec7c35d368.png)

It also supports many parameter settings, such as search depth, time range, whether to include webpage content, maximum number of results, country, and more.

For example, when I set the search country to China, it was able to find articles from Chinese platforms:

![](https://pic.yupi.icu/1/1776257191114-95ef71bb-b844-45ec-bd25-f0bf691fa5d1.png)

Once we confirm the search quality is good enough, let’s look at how to use it in code.



### LangChain Integration with Tavily

In this project, we use LangChain, a mainstream AI application development framework, to integrate Tavily.

LangChain already has an official integration package, `langchain-tavily`, which makes it very convenient to use. You only need to bind the TavilySearch tool to an Agent in your code, then create the Agent and start chatting with it directly:

```python
from langchain_tavily import TavilySearch
from langchain.agents import create_tool_calling_agent

tavily_search_tool = TavilySearch(
    max_results=5,
    topic="general",
)

# 创建 Agent，绑定搜索工具
agent = create_tool_calling_agent(model, [tavily_search_tool])
# 用户提问，Agent 自动判断是否需要搜索
response = agent.invoke({"messages": "最近有什么 AI 新闻？"})
```

Besides search, there’s also a TavilyExtract tool that can extract clean webpage content from a URL:

![](https://pic.yupi.icu/1/1776257649471-db04269f-1efd-4a96-b485-c762dc2d0b59.png)

If you don’t understand the code, don’t worry. Later we’ll just write these requirements into the prompt and let AI look up the docs and write the code itself.



### Firecrawl Search Service

Besides Tavily, Firecrawl is also a good choice. Firecrawl is better at webpage scraping and full-site crawling, and it also provides search functionality.

The two have slightly different positioning, so I made a quick comparison table:

| Dimension | Tavily Search | Firecrawl |
| -------------- | ------------------------------------ | ------------------------------------ |
| Positioning | AI-native search API, designed specifically for RAG/Agents | Web data API focused on webpage scraping and content extraction |
| Search speed | 1 ~ 3 seconds | ~7 seconds (including page scraping) |
| Return format | Structured summaries, saving Tokens | Markdown/HTML/JSON, with more complete content |
| LangChain integration | Officially recommended first, with a dedicated package | Has a Python SDK, but needs your own wrapper |
| Open source | No | Yes (AGPL-3.0, self-hostable) |
| Free quota | 1000 times/month | 1000 credits/month |
| Monthly cost at 100K scale | $500 | $83 |
| Best use case | AI Agent web search | Full-site crawling, data extraction |

For our AI search engine project, Tavily’s speed and structured results are a better fit, so I chose it as the main search engine.

In the later environment setup section, I’ll also show everyone how to install Firecrawl, but its role there is to help the AI coding tool search technical documentation online. That’s a different thing from the project’s built-in search capability.



### Core Business Workflow

Finally, let’s summarize the core flow of the AI search engine:

1. The user enters a question on the frontend
2. The backend receives the request and calls the Tavily Search API to search the web and obtain structured results
3. Those search results are injected into the Prompt as context and handed to the DeepSeek V4 large model
4. AI generates a synthesized answer with citation numbers based on the search results, then returns it to the frontend through SSE streaming
5. The frontend displays both the AI synthesized answer and the complete search result list at the same time
6. After the AI answer is complete, it automatically generates related question recommendations to help the user continue exploring

![AI搜索引擎核心业务流程图](https://pic.yupi.icu/1/02_AI%25E6%2590%259C%25E7%25B4%25A2%25E5%25BC%2595%25E6%2593%258E%25E6%25A0%25B8%25E5%25BF%2583%25E4%25B8%259A%25E5%258A%25A1%25E6%25B5%2581%25E7%25A8%258B%25E5%259B%25BE_compressed_v3.png)



## Environment Setup

### Codex Configuration

Open Codex and make sure GPT-5.5 appears in the model list. If you can’t see it, it’s probably an account issue, and you may need a higher-tier subscription. I’m using the Plus plan here.

![](https://pic.yupi.icu/1/1777256418373-5682599c-2367-4f94-951a-43bab6f0f861-20260512154050287.png)

You can see GPT-5.5 is already available in the interface, and it also supports adjusting the intelligence level (low / medium / high / very high). I usually choose **High**.

Go into settings from the bottom-left corner and switch the work mode to **for programming**, so AI’s responses become more professional and better suited to development scenarios:

![](https://pic.yupi.icu/1/image-20260512143515143.png)

Then, in settings, turn on **computer control** and install the Google Chrome browser extension. That way, later on AI can help you automatically operate the computer and browser for testing.

![](https://pic.yupi.icu/1/1778557131199-91ad72e5-024a-46a6-ae0f-3e59851f7327.png)



### Install AI Extensions

Codex’s AI extensions mainly include three categories:

- MCP services, used to connect to external tools
- Agent Skills, which teach AI specific professional skills
- Plugins, which give AI more abilities

The official app already includes some built-in plugins and skills, such as Computer Use, Browser Use, PDF processing, presentation editing, and so on:

![](https://pic.yupi.icu/1/image-20260512143730227.png)

![](https://pic.yupi.icu/1/image-20260512143751551.png)

However, several extensions needed for this project aren’t included by default in Codex, so you need to install them yourself.

We need these 3 extensions:

1. Firecrawl: web search and webpage scraping, so AI can get the latest technical information
2. Context7: query the latest technical documentation and API usage, reducing hallucinated code
3. UI UX Pro Max: a frontend beautification skill that makes the generated pages feel more designed

You can manually add MCP services directly in Codex settings, but that means manually filling in a lot of parameters, which is extremely annoying!

![](https://pic.yupi.icu/1/1777257751584-4842f03a-fa07-4cbe-94ad-dce017977b66-20260512143837549-20260512154050491.png)

Fortunately, we can take another route and use the commands provided by each AI service to install them quickly.



#### 1. Install Firecrawl

Firecrawl is a web search and webpage scraping tool that lets AI search for the latest technical information and docs before development begins. Although our project uses Tavily Search for its actual search feature, Firecrawl’s role here is to help the AI coding tool look up reference material.

Open the terminal and enter the following command:

```bash
npx -y firecrawl-cli@latest init --all --browser
```

![](https://pic.yupi.icu/1/1777258212308-8c83d23e-338e-4ec2-b1c0-05f54a22a36e-20260512154050521.png)

After running it, the browser opens automatically. On the popup page, click authorize:

![](https://pic.yupi.icu/1/1777258069152-2d7fdb02-64e2-440b-bcbd-6254b07fb74e-20260512154050549.png)

After installation, it automatically registers 12 related skills:

![](https://pic.yupi.icu/1/1777258235867-0f6f08f5-4791-4b66-84b7-50936912540d-20260512154050588.png)

Then, in Codex’s skill management, you’ll see the newly added Firecrawl-related skills:

![](https://pic.yupi.icu/1/1777258331237-182161c5-d21b-4a9b-9c6a-855d99312b5e-20260512154050621.png)



#### 2. Install Context7

Context7 is a technical documentation query tool that lets AI access the latest official docs for various frameworks and libraries, avoiding outdated APIs when writing code.

First, enter one command in the terminal to install it:

```bash
npx ctx7@latest setup
```

It will ask whether to install the MCP service or CLI + Skills. Here I choose CLI + Skills. You’ll notice that more and more tools are now moving from MCP toward CLI + Skills:

![](https://pic.yupi.icu/1/1777258448310-41f86ec3-26e1-476e-aed5-4913c8116d21-20260512154050653.png)

Authorize it in the popup webpage as well. No need to fetch and type in an API Key yourself—very convenient!

![](https://pic.yupi.icu/1/1777258547209-dc872280-09eb-4bd9-ad45-2e412382002d-20260512154050680.png)

Then choose which AI coding tool to install it for. I chose Codex:

![](https://pic.yupi.icu/1/1777258572107-f494c3bb-01a9-443d-ba1d-6b1a3b3fab9a-20260512154050707.png)

Installation successful:

![](https://pic.yupi.icu/1/1777258672897-259f035a-f365-46ce-bc5d-e33fbc839f34-20260512154050735.png)

Confirm the installed skills inside Codex:

![](https://pic.yupi.icu/1/1777258710387-4b47a05d-dcb1-43ce-9761-f5d28976731e-20260512154050771.png)



#### 3. Install UI UX Pro Max

This is a frontend beautification skill package that gives AI-generated pages more design polish and avoids a giant pile of Emojis.

Enter one command:

```bash
uipro init
```

Choose to install the Skill for Codex:

![](https://pic.yupi.icu/1/image-20260427143633213.png)

Installation successful:

![](https://pic.yupi.icu/1/1777258832043-8a3230db-2a76-47f7-a32a-5113a0487631-20260512154050883.png)

In Codex’s skill management, you can see the new skill:

![](https://pic.yupi.icu/1/1777258847545-ba145ccf-2ab3-4a37-948a-4bb48d228fe4-20260512154050912.png)

At this point, the environment setup is complete! Next time you build a project, you won’t need to prepare all of this again~



## Development Coding

Create a new project folder named `yupi-ai-search` and open it in Codex:

![](https://pic.yupi.icu/1/1778555023028-80d1f617-111e-4e19-815c-7f455101674a.png)

Then enter your prompt. I’ll share the actual prompt I used here for reference:

```markdown
## 角色

你是一个全栈工程师，擅长 Python + FastAPI + LangChain + Vue 开发。

## 任务

开发一个叫 yupi-ai-search 的 AI 搜索引擎网站。用户输入自然语言问题，系统自动联网搜索最新信息，再将搜索结果交给 DeepSeek V4 大模型综合分析，生成一份带引用来源的智能回答，同时展示完整的搜索结果列表。

核心功能：
1. 搜索主页：简洁的搜索框，输入问题后发起 AI 搜索
2. AI 联网搜索：调用 Tavily Search API 获取最新网页信息，将搜索结果作为上下文注入 Prompt，让 AI 生成综合回答
3. 引用来源展示：AI 回答中引用的信息必须标注来源编号，底部列出所有引用来源的标题和链接，用户可点击跳转原文
4. 搜索结果列表：除了 AI 综合回答外，还要像传统搜索引擎一样展示完整的搜索结果列表，包括 AI 未直接引用到的结果
5. 流式输出：AI 回答支持 SSE 流式输出，打字机效果实时显示
6. 搜索历史：本地存储搜索历史记录，支持快速重新搜索
7. 相关问题推荐：AI 回答完成后，自动生成 3-5 个相关问题供用户继续探索

## 技术栈

- 后端：Python FastAPI + LangChain
- 前端：Vue 3 前后端分离，支持 Markdown 渲染和代码高亮
- AI 模型：对接 DeepSeek V4（兼容 OpenAI SDK 格式，通过环境变量配置）
- 搜索：Tavily Search API（通过 langchain-tavily 集成）

## 要求

1. 页面参考 Perplexity 的简洁风格，搜索页面居中大搜索框，结果页面信息密度高，使用 UI UX Pro Max 技能美化
2. 开发前，先通过 Firecrawl 联网搜索相关信息，通过 Context7 查询 LangChain、FastAPI、Tavily Search、DeepSeek API 的最新文档
3. 必须生成完整可运行的代码，每步完成后必须自主测试验证
```

Although it looks long and messy, it was actually generated with AI. Let me briefly explain the key points in this prompt:

- Put the **role definition** first so AI enters the mindset of a full-stack engineer
- Use the **task description** to explain the requirements clearly in natural language
- In the **tech stack** section, only list key choices such as the LangChain + Tavily Search combination, and let AI decide the detailed implementation
- The last two requirements are the key: make AI check docs before writing code to avoid making things up, and make it test by itself after development to reduce failures

I chose GPT-5.5 as the model, set intelligence to **High**, and gave it full access permissions (mostly for convenience):

![](https://pic.yupi.icu/1/1778555200757-7240a8f9-cf77-465b-982e-f039e2b311c9.png)

Small tip: if you want AI to test more thoroughly, you can obtain the Tavily Search and DeepSeek API Keys in advance and provide them directly to AI. Otherwise, AI won’t be able to test the search and AI summarization capabilities.

After sending the prompt above to AI, the task is still fairly complex, so all that’s left is the long wait...

You can see that AI first used Firecrawl and Context7 to search for usage and documentation for Tavily Search, LangChain, FastAPI, and the DeepSeek API. Only after that research was done did it start writing code:

![](https://pic.yupi.icu/1/1778555536834-8dbc50c9-6038-42e9-90c2-261fe1f203bc.png)

After generating the code, AI automatically opens a browser to test the frontend:

![](https://pic.yupi.icu/1/1778556244139-48927bec-fe3c-41ff-92c5-cd8045480d63.png)

From development to test run, the whole process took 23 minutes. AI generated a complete frontend and backend codebase and also automatically wrote the project documentation:

![](https://pic.yupi.icu/1/1778556777014-9ff35308-377f-4e1f-9d32-be62c4749842.png)

If you move your mouse to the right side of Codex, you can view the full task results, background terminal, and information sources.

![](https://pic.yupi.icu/1/1778557426240-34c35fa6-6b77-4e55-befe-9ff04d8f02e3.png)

At the bottom of AI’s reply, you can view and review all generated code files:

![](https://pic.yupi.icu/1/1778556995353-16cf38fe-df3c-4f43-bf74-3c0053d16e93.png)

If you’re interested, check out the core code AI generated. The backend core is an SSE streaming endpoint: after receiving the user’s search request, it first calls Tavily Search to get webpage search results, then injects those search results into the Prompt and hands them to DeepSeek V4 to generate a synthesized answer with citations, and finally generates related question recommendations.

If search fails, there’s also a fallback strategy that tells the user the answer was not verified through web search:

![](https://pic.yupi.icu/1/1778559184004-3a017b1b-7ba1-4ab0-b385-d5ab5d17b584.png)



## Testing and Verification

Next, following AI’s guidance, you need to fill in the API Keys:

![](https://pic.yupi.icu/1/1778557518039-74f6c533-9922-40bf-8023-f175cef3afb7.png)

First go to the [DeepSeek Open Platform](https://platform.deepseek.com) to get a DeepSeek API Key. We already got the Tavily API Key earlier:

![](https://pic.yupi.icu/1/1778557575635-cd8140d2-5b18-4c36-a7a5-91a92cb1015f.png)

Then modify the environment configuration file in the project’s backend directory: rename `.env.example` to `.env` and fill in your own API Keys:

![](https://pic.yupi.icu/1/1778557702120-af92b45d-5f2a-46bd-8895-184063af520a.png)

Note that if your project is going to be open source, you must remember to ignore `.env` in `.gitignore` to avoid leaking your API Key to GitHub!

After configuring the environment variables, ask AI to restart the project:

![](https://pic.yupi.icu/1/1778558017324-2d4008af-99ba-4cfb-8595-018363622eb6.png)

### Manual Testing

Next, let’s test it manually.

Open the webpage, and wow—the homepage is unbelievably minimal!

AI really listened carefully to the prompt: a clean style + a large centered search box. It really does feel a bit like Perplexity 🐶:

![](https://pic.yupi.icu/1/1778558216223-bf3b6c1f-939e-4af2-b4ae-53318a62c90c.png)

Let’s enter a question: what is Yupi’s AI Programming Navigation?

Actually, my two websites are [Programming Navigation](https://codefather.cn/) and [Yupi AI Navigation](https://ai.codefather.cn/). Here I intentionally mixed the two products together to see how the search results and AI summary would perform~

After about 4 seconds, the interface displayed the search result list, and after about 20 seconds it produced the full AI summary. You can see that the left side shows AI’s synthesized answer with citation numbers, while the right side shows the complete search result list, including titles, summaries, and links, so you can browse each result just like in a traditional search engine:

![](https://pic.yupi.icu/1/1778558955839-01e86b7c-4a9e-4438-9c93-1157a53a59f4.png)

The search and generation speed is pretty fast, and AI did a good job clearly distinguishing my two different products. The content is accurate too.

At the bottom, you can see cited sources and related question suggestions. Click a citation to jump to the original source, or click a related question to quickly launch the next search:

![](https://pic.yupi.icu/1/1778559088680-6cd7d454-804d-45aa-b5d6-071d2126ec51.png)

On the Codex chat page, move your mouse to the right side and click to view the backend terminal. You’ll be able to see Python backend logs, with each search request recorded:

![](https://pic.yupi.icu/1/1778559813125-6cb03089-93ea-4db6-adeb-b616493cbc01.png)

Judging from the results, the default information sources are mainly domestic. But Tavily Search also supports foreign-source searching. For example, when I asked: how is Claude Code 4.7?

This time the search sources became a mix of Chinese and English, and quite a few English technical blog review articles appeared:

![](https://pic.yupi.icu/1/1778559369205-281eff4e-0fc6-4c0b-ad77-a3a6464b0216.png)

You can also specify the search source in your question. For example, I asked: what Claude Code tutorials has Yupi posted on X?

Then the search results included original pages from X:

![](https://pic.yupi.icu/1/1778559537963-ab13e987-8568-4bd4-a0d3-a51a5e291eca.png)

So, how about that? With very little effort, you can build your own AI search engine and have both domestic and international information right in your hands~



### Autonomous AI Testing

The core features already passed testing, but if you want to formally launch the project, you still need to test a lot of edge cases. For example: will it crash if the user enters blank input? What happens if the network times out? Will the page display correctly when there are no search results?

Testing those one by one manually is too much trouble, so I just let AI handle it.

Codex has built-in browser control. Type `@浏览器` to use the plugin and let AI test autonomously:

```markdown
@浏览器 打开浏览器，自主测试所有功能
出了问题自动修复，确保所有功能正常可用
```

![](https://pic.yupi.icu/1/1778561487978-700ae39e-627c-4b1c-817a-cfe7689936d9.png)

You can see AI opening a browser inside Codex, entering questions and running searches by itself, then checking whether the search result list, AI answer, citations, related questions, search history, and all other features are working correctly:

![](https://pic.yupi.icu/1/1778562027828-4a13a04d-d838-41b6-aa3a-466c528ba85d.png)

After waiting 18 minutes, AI completed end-to-end autonomous testing and even did a bit of extra optimization along the way:

![](https://pic.yupi.icu/1/1778562928716-5f9c866d-c14a-49b8-a20a-c623050062c1.png)

At this point, the project is finished. Pretty simple, right?



## Ideas for Extension

Although we quickly built a usable AI search engine, you should know that finishing development is only the first step. A mature search engine product still has a lot more to consider, and that’s exactly where the real gap opens up.

Here I’ll use AI to give everyone a few ideas:

1. Search-result caching: if multiple users search for the same question within a short time, there’s no need to call Tavily’s API every time. Caching can save a lot of money.
2. Search-result ranking optimization: results can be re-ranked based on source authority and content freshness rather than directly using Tavily’s original order.
3. Multimodal search: support searching images, videos, and files, not just text.
4. Observability: add logs, monitoring, and tracing so you know what steps each search request went through, how much time each step took, and where problems most often happen.
5. Cost control: both the search API and large-model API are billed by usage, so you need rate limiting and quota management to prevent abuse. Otherwise, one careless moment could mean a big bill.
6. Security protection: prompt-injection defense and filtering prohibited content are things you must think about before launch.

We should learn how to stand on the shoulders of giants and use ready-made tools to rapidly build prototypes, while still being able to see what’s missing behind the prototype. That’s real engineering ability.



## My Thoughts

Finally, let me talk about my real impressions of Codex, GPT-5.5, and DeepSeek V4.

First, Codex. Its interface is all about simplicity. At first glance, it doesn’t even look like an AI coding tool—it looks more like an AI chat assistant. But in fact, its feature set is pretty complete, including MCP and Skills extensions, a plugin marketplace, automation, Git integration, Browser Use, Computer Use, and most of the engineering capabilities needed for AI programming.

And lately its update speed has been insanely fast. It even had time to add an AI desktop pet to give us a little emotional support... though to be honest, I think some of the UI changes are not as nice as the old ones.

![](https://pic.yupi.icu/1/image-20260505182943304-20260512154052050.png)

But the drawbacks are also obvious. The default selection of models is limited. Unlike Cursor and Copilot, it doesn’t natively integrate Claude, GPT, Gemini, and other models that you can switch between freely. Usability is also a bit worse, and you probably already felt that from the MCP configuration section. Copilot can search and install MCP in one click through the extension marketplace, and Cursor supports visual editing of JSON config. On the Codex side, you still have to tinker with the command line or hand-write TOML.

![](https://pic.yupi.icu/1/1777266857576-e240c700-e113-4d3d-8f4d-44512175986f-20260512145745548-20260512154052085.png)

Now let’s talk about GPT-5.5. Besides this project, I’ve used GPT-5.5 multiple times in earlier tutorials and in my own projects. Overall, I feel it’s not quite as strong as Claude Opus 4.6. But its capability is still very strong. As long as the prompt is good enough, it can usually handle the frontend and backend of a full-stack project in one shot, and the core business workflow will most likely work end to end on the first try.

My feeling is that GPT-5.5’s standout trait is that it **listens to prompts very obediently**. Its frontend results are decent and steady, but it won’t usually surprise you with amazing UI. So if you want to make full use of a powerful large model, you still need to write prompts carefully, list the feature points clearly, and provide a bit of guidance on solution design and development workflow. Only then can AI give you a satisfying result.

Now let’s look at the cost of GPT-5.5. This development process consumed 134,000 tokens and used 52% of the context window. Codex desktop has a 258K context size, which is basically enough for building full-stack projects like this:

![](https://pic.yupi.icu/1/1778562964683-a8df5a46-5762-48f5-9593-4e89d21b739f.png)

At the moment I’m using a GPT Plus subscription, which costs $20 per month (about 150 RMB), with usage limits per 5 hours and per week. After finishing this project, I had used roughly half of the 5-hour quota. Not counting expansion features, that means I could probably build around 10 complete projects per week.

![](https://pic.yupi.icu/1/1778563016906-8653e48f-c417-44c6-8157-99f4e82b7a86.png)

Finally, let’s talk about DeepSeek V4. In this project, I used the V4-Flash model as the “brain” of the search engine. Its generation speed was pretty fast, and the results were quite good. For organizing search results, it’s already more than enough—you don’t need Pro.

The Flash model is very cheap. In my testing, it took 24 requests and only cost 0.09 RMB. Based on normal live traffic, 1,000 requests per day would cost about 3.75 RMB, which is very cost-effective. Some of our team’s business scenarios also connect to the DeepSeek API.

![](https://pic.yupi.icu/1/1778561258409-d0081f49-c868-49a8-80e5-f1342e83bde7.png)

Overall, the barrier to AI application development is already extremely low. In the past, building a search engine was something only big companies could do. Now, with a single prompt, you can create a usable prototype.

But after all, there’s still a huge distance between **being able to build it** and **building it well**. The engineering aspects I mentioned earlier—caching, security, cost control, and so on—are the places that truly test your fundamentals.



## Final Thoughts

In this article, I walked everyone through building an AI search engine from scratch with Codex + GPT-5.5, covering the full process from requirement analysis and solution design to Tavily Search integration, LangChain development, and testing.

Once you learn these things, you’ll understand how to build AI Agent applications, how AI search engines work, and how to apply Codex and GPT-5.5 to your own projects.

If you want to continue learning more hands-on AI programming techniques, you can read the other articles in the practical tips section of this tutorial series.
