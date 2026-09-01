# If an Interviewer Asks “How Do You Build AI Applications?”, Don’t Just Say You Know How to Call APIs!

Recently, one of my students told me about an interview where the interviewer asked: if you were asked to build an AI application, how would you do it?

He replied confidently: isn’t that easy? Just call an API.

The interviewer followed up: is that the only way? Are you sure?

He froze on the spot. It got awkward very quickly.

This question is actually very representative. A lot of people still understand AI application development only at the level of “calling an API.” They think as long as they can send an HTTP request and get an AI answer back, the job is done.

But in reality, calling an API is only the most basic method. From raw HTTP requests at the lowest level, to official SDK wrappers, to fully featured development frameworks, to drag-and-drop low-code platforms, and even a lesser-known hidden mode, AI application development has already become extremely rich in form.

![](https://pic.yupi.icu/1/01_%E5%B0%81%E9%9D%A2%E5%9B%BE-5%E7%A7%8DAI%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%A8%A1%E5%BC%8F%E6%A6%82%E8%A7%88_compressed_v1.png)

Today, I’m going to explain all **five mainstream AI application development modes** clearly in one go: what they are, how they work, and what scenarios each one is best suited for. For every mode, I’ll also include a simple code example so you can understand it quickly. Once you get these, not only will you be able to handle interview questions more confidently, but when you build projects with AI coding, you’ll also know what technologies to add to your stack.

![](https://pic.yupi.icu/1/%E9%B1%BC%E7%9A%AE%E7%9A%84AI%E5%AF%BC%E8%88%AA-AI%E5%B7%A5%E5%85%B7%E7%94%A8%E6%B3%95%E5%A4%A7%E5%85%A8.png)



## 1. Direct HTTP API Calls

The most primitive and direct method is calling the large model’s API through HTTP requests.

Simply put, your program sends a message to the model, the model processes it, and then returns the result to you.

It’s like calling an expert on the phone to ask a question. You have to dial the number yourself (assemble the API URL), prove your identity (pass the key), clearly describe the question (build the request body), and then wait for the expert to finish answering before recording the result yourself (parse the response). **You have to do every step manually, but in return you have complete control over the whole process.**

![](https://pic.yupi.icu/1/02_HTTP_API%E7%9B%B4%E6%8E%A5%E8%B0%83%E7%94%A8-%E6%89%93%E7%94%B5%E8%AF%9D%E7%B1%BB%E6%AF%94_compressed_v1.png)

No matter what programming language you use, as long as it can send HTTP requests, it can call an AI large model. That makes this the most basic calling method supported by all model providers.

Whether it’s overseas providers like OpenAI and Anthropic, domestic providers like DeepSeek and Qwen, open-source models deployed locally through Ollama, or aggregated platforms like OpenRouter where one API key can access many providers, all of them support HTTP API calls.

At present, there are two main protocol formats for HTTP API calls.

**1) OpenAI-compatible format**

This format was originally defined by OpenAI, but because so many people use it, it has now become the de facto standard followed by most providers. DeepSeek, Qwen, Kimi, Ollama, and most other large model providers are compatible with it.

The advantage of having a unified standard is that you can write one set of model-calling code and switch seamlessly between vendors by changing only the API address and key, without having to re-adapt the format.

For example, here I use the HTTP request tool `curl` to send an OpenAI-compatible request to call the DeepSeek model:

```bash
curl https://api.deepseek.com/chat/completions \
  -H "Authorization: ******" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-v4-pro",
    "messages": [
      {"role": "system", "content": "你是一个有用的助手"},
      {"role": "user", "content": "用一句话介绍什么是AI应用开发"}
    ]
  }'
```

If you switch to an OpenAI model, you only need to change the request URL and the `model` name. The request format is otherwise exactly the same.

**2) Anthropic Messages API format**

Anthropic, the company behind Claude, uses its own separate protocol, and the request structure is somewhat different from OpenAI’s.

For example, the system prompt is passed in a top-level `system` parameter rather than being included as just another message. So if you want to call Claude models, you have to follow Anthropic’s format.

```bash
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: 你的API密钥" \
  -H "content-type: application/json" \
  -d '{
    "model": "claude-sonnet-4-6",
    "max_tokens": 1024,
    "system": "你是一个有用的助手",
    "messages": [
      {"role": "user", "content": "用一句话介绍什么是AI应用开发"}
    ]
  }'
```

When you actually develop an AI application, you also need to understand what the fields in the request and response mean. The most important one is the `messages` field, which represents the message history between you and AI. There’s also `temperature`, which controls how random the answer is; `max_tokens`, which limits answer length; and the `usage` field in the response, which tells you how many Tokens this call consumed. Most platforms provide detailed API docs, so in practice you can just follow the documentation.

![](https://pic.yupi.icu/1/image-20260511153354301.png)

Large-model APIs generally provide two calling methods. One is the normal request mode: one question, one answer, and the full response is returned at once after generation is complete. The other is streaming mode. If you want to implement a typewriter-style effect where the answer appears piece by piece, you need to use **SSE (Server-Sent Events)** so the server can continuously push chunks of generated content to you. It’s not hard to use either. In most cases, you simply set `stream` to `true` in the request parameters.

Below is a Python example of streaming output so you can feel how that typewriter effect is implemented:

```python
import requests

response = requests.post(
    "https://api.deepseek.com/chat/completions",
    headers={
        "Authorization": "******",
        "Content-Type": "application/json"
    },
    json={
        "model": "deepseek-chat",
        "stream": True,  # 开启流式输出
        "messages": [
            {"role": "system", "content": "你是一个有用的助手"},
            {"role": "user", "content": "用一句话介绍什么是AI应用开发"}
        ]
    },
    stream=True  # 开启流式接收
)

# 逐行读取服务端推送的内容
for line in response.iter_lines():
    if line:
        print(line.decode())
```



## 2. Official SDK Calls

Anyone who has written the code above can probably feel that direct HTTP calling is still a bit cumbersome. Filling in URLs, setting headers, constructing JSON, parsing responses, handling error codes, parsing streaming data line by line... none of that has anything to do with your business logic, yet you still have to handle every part yourself.

That’s why all major model vendors provide **SDKs (Software Development Kits)** to wrap those low-level details for you.

If using raw HTTP APIs is like dialing a phone number yourself, then using an SDK is like having a smart communication app installed. You just speak, and the app dials, connects, records, and converts everything into text for you. What you receive is already the ready-to-use answer.

![](https://pic.yupi.icu/1/03_%E5%AE%98%E6%96%B9SDK%E8%B0%83%E7%94%A8-%E6%99%BA%E8%83%BD%E9%80%9A%E8%AE%AFAPP%E7%B1%BB%E6%AF%94_compressed_v2.png)

At present, mainstream large-model providers such as OpenAI, Anthropic, Google, Alibaba Cloud Bailian, and Zhipu all provide multilingual SDKs covering common languages like Python and Java.

![](https://pic.yupi.icu/1/image-20260511153849051.png)

The essence of an SDK is wrapping HTTP requests, so the OpenAI-compatible format we just discussed also works at the SDK layer. For example, DeepSeek is compatible with OpenAI’s protocol, which means you can directly use OpenAI’s SDK and just change a few parameters to call DeepSeek.

For example, here’s how to call a GPT model using OpenAI’s Python SDK:

```python
# 引入 OpenAI 官方 SDK
from openai import OpenAI

client = OpenAI(api_key="你的API密钥")

completion = client.chat.completions.create(
    model="gpt-5",
    messages=[
        {"role": "system", "content": "你是一个有用的助手"},
        {"role": "user", "content": "用一句话介绍什么是AI应用开发"}
    ]
)

print(completion.choices[0].message.content)
```

No need to fill in the URL, no need to set headers, no need to manually parse JSON. A few lines of code and you’re done. On top of that, SDKs often include built-in retries, type hints, and streaming support, which improves development efficiency, keeps the code cleaner, and makes the system more stable.

If you’re using DeepSeek, the code is almost identical. You only need to change the `base_url` and `model` name:

```python
client = OpenAI(
    api_key="你的DeepSeek密钥",
    base_url="https://api.deepseek.com"
)

# 调用时把 model 换成 DeepSeek 的模型名
completion = client.chat.completions.create(
    model="deepseek-chat",
    messages=[...]
)
```



## 3. AI Development Frameworks

SDKs solve the problem of **how to call models conveniently**, but enterprise AI applications are much more than just calling a model once.

You may also need AI to remember previous conversation content, look up information in a knowledge base before answering through RAG, call external tools such as weather or web search, connect to more services through MCP, or even coordinate multiple AIs to complete complex tasks...

If you had to implement each of these abilities from scratch, the workload would be enormous. So on top of SDKs, people added another abstraction layer and turned it into **AI development frameworks**.

To use an analogy, SDKs are like being handed engine parts, tires, and a steering wheel—you still need to assemble them one by one. AI development frameworks are like being given a semi-finished car with the chassis, frame, and circuitry already in place. You just decide on the exterior and interior, and then drive off.

![](https://pic.yupi.icu/1/04_AI%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6-%E6%B1%BD%E8%BD%A6%E7%BB%84%E8%A3%85%E7%B1%BB%E6%AF%94_compressed_v1.png)

Let me list a few mainstream AI development frameworks using Python and Java as examples. That way, when you encounter these technical terms during AI coding, they won’t feel unfamiliar.

In the Python ecosystem, **LangChain** is currently the most mainstream AI application development framework. It provides a large number of integration components covering common capabilities such as model calls, RAG knowledge bases, tool use, and MCP integration.

**LangGraph** is a more advanced framework launched by the LangChain team. It uses graph structures to orchestrate complex AI workflows and is suitable for building stateful AI agents with loops and branching logic.

For example, this is what calling a model through LangChain looks like:

```python
from langchain.chat_models import init_chat_model
from langchain.messages import HumanMessage, SystemMessage

model = init_chat_model("gpt-5")

messages = [
    SystemMessage("你是一个有用的助手"),
    HumanMessage("用一句话介绍什么是AI应用开发")
]

response = model.invoke(messages)
print(response.content)
```

Looks similar to using an SDK, right?

But the value of LangChain is that when you want to add advanced capabilities like memory or tool use, you can do it with just a few lines of configuration instead of building everything from scratch.

For example, you can create an AI agent with tool-calling capability like this:

```python
from langchain.agents import create_agent
from langchain.tools import tool

# 定义一个工具，让 AI 能查天气
@tool
def get_weather(city: str) -> str:
    """查询指定城市的天气"""
    return f"{city}今天晴，25°C"

# 一行代码创建带工具调用能力的 Agent
agent = create_agent(model="gpt-4o", tools=[get_weather])

# 调用 Agent，它会自动判断是否需要调用工具
result = agent.invoke(
    {"messages": [{"role": "user", "content": "北京今天天气怎么样？"}]}
)
```

This way, AI can proactively call a tool to check the weather. You only need to define the tool function, and LangChain handles the rest.

What’s more, many AI development frameworks in other language ecosystems basically follow the same design ideas as LangChain—for example, Java’s LangChain4j and Go’s LangChainGo. Their functionality is largely aligned with the Python version, so once you learn one version, switching to another language is quite easy.

In the Java ecosystem, there is also Spring’s official **Spring AI** and Alibaba’s **Spring AI Alibaba**, both deeply integrated into the Spring Boot ecosystem and very suitable for Java backend developers to pick up quickly.

![](https://pic.yupi.icu/1/image-20260511154445018.png)

I also think **Vercel AI SDK** is worth watching. It’s an AI development framework in the TypeScript ecosystem that provides a unified interface for more than 20 model providers, making it especially suitable for frontend and full-stack developers.



## 4. Low-Code AI Development Platforms

Frameworks are powerful, but writing code still has a learning barrier. For business users or people who aren’t very comfortable with programming, just setting up a development environment can already be a headache.

That’s where **low-code AI development platforms** come in. They let you build AI applications without writing code.

You can think of a low-code platform as building with blocks. The large model is one block, the knowledge base is another block, and tool calling is another block. Every block is ready-made—you only need to decide how to connect them and what shape to build.

![](https://pic.yupi.icu/1/05_%E4%BD%8E%E4%BB%A3%E7%A0%81%E5%B9%B3%E5%8F%B0-%E6%90%AD%E7%A7%AF%E6%9C%A8%E7%B1%BB%E6%AF%94_compressed_v1.png)

Dify is a classic example of a low-code AI development platform. It lets you visually build AI chat assistants, workflows, knowledge-base Q&A apps, and more, and can connect to various large models with one click.

Its biggest advantage is that it is open-source and can be privately deployed. If a company wants to keep data on its own servers, that’s no problem.

![](https://pic.yupi.icu/1/1743564064922-03f6365b-a712-47d9-be55-4867b848a269.png)

To build an AI chat assistant on Dify, the process is roughly:

1. Choose a large model (for example GPT-5.5 or DeepSeek)
2. Write a system prompt that defines AI’s role
3. Configure a knowledge base if needed by uploading your documents
4. Click publish, and you get either a callable API or a directly shareable chat link

The whole process requires not a single line of code.

There are also many similar platforms. For example, ByteDance’s Coze supports visual AI app building and is easy to get started with. Alibaba Cloud Bailian is an all-in-one large-model application building platform that integrates model calls, agent orchestration, and knowledge-base management. There is also the open-source workflow automation platform n8n, which is especially good for building AI automation flows across multiple systems.



## 5. SDKs for AI Coding Tools

The four modes above cover everything from fully manual coding to completely no-code approaches. But there is another mode many people don’t know about...

In 2026, AI coding tools such as Cursor, Claude Code, and GitHub Copilot all launched their own SDKs. You can directly call the agents of these AI coding tools from within your own code. They can help you read code, modify code, and run commands. And all the MCP services, Skills, and project rules you configured inside the AI coding tool can also take effect when called through the SDK.

If the earlier methods are all ways of doing the work yourself, then using the SDK of an AI coding tool is like hiring an AI programmer who already knows how to code. You only need to tell it what to do, and it automatically reads files, analyzes code, and completes development.

![](https://pic.yupi.icu/1/06_AI%E7%BC%96%E7%A8%8B%E5%B7%A5%E5%85%B7SDK-%E9%9B%87%E4%BD%A3AI%E7%A8%8B%E5%BA%8F%E5%91%98%E7%B1%BB%E6%AF%94_compressed_v3.png)

Take the Cursor SDK as an example. It allows you to directly call Cursor’s AI agent in TypeScript or Node.js code.

First create a project folder, then open a terminal and run one command in that directory to install the SDK:

```bash
npm install @cursor/sdk
```

![](https://pic.yupi.icu/1/image-20260511141833488.png)

Then log in to the [Cursor Dashboard](https://cursor.com/dashboard/integrations), generate an API key on the Integrations page, and save it. You’ll need it later in code for authentication.

![](https://pic.yupi.icu/1/image-20260511141405454.png)

Suppose I have a local project called “content topic fetcher,” where `AGENTS.md` defines the workflow rules for topic generation, and the `frontend-design` skill has also been installed.

![](https://pic.yupi.icu/1/image-20260511154340593.png)

Now I want AI to help me find today’s trending topics and generate a beautiful web report.

Create a new JavaScript file, for example `main.js`, and write the following code:

```javascript
import { Agent } from "@cursor/sdk";

// 创建 AI Agent，指向「创作选题获取器」项目
const agent = await Agent.create({
  apiKey: '你的 API Key',
  model: { id: "gpt-5.5" },
  local: { cwd: "/Users/yupi/workflow/创作选题获取器" },
});

// 一句话下达指令
const run = await agent.send("帮我获取今日 AI 领域的热门选题，并生成一个网页报告");

// 收集所有事件，打印到终端的同时保存到文件
const events = [];
for await (const event of run.stream()) {
  console.log(event);
  events.push(event);
}

// 把完整的事件记录保存为 JSON 文件，方便事后分析
const fs = await import("fs");
fs.writeFileSync("agent-output.json", JSON.stringify(events, null, 2));
```

Then run this in the terminal:

```bash
node main.js
```

After it runs, you’ll see a long stream of events printed in the terminal, such as the agent beginning execution.

![](https://pic.yupi.icu/1/image-20260511151359126.png)

From the logs, you can clearly see the entire execution process of the agent: it first uses the `glob` tool to scan the project directory, then uses the `read` tool to read the `AGENTS.md` workflow rules and the `SKILL.md` instructions for `frontend-design`, then uses the `shell` tool to call the project’s own topic-fetching script for internet search, collects 70 trending topics from six platforms including GitHub and Hacker News, and finally uses the `edit` command to generate an HTML web report containing nearly a thousand lines of code.

![](https://pic.yupi.icu/1/image-20260511151132128.png)

At the end, the agent even opens a browser automatically so you can directly inspect the generated report.

![](https://pic.yupi.icu/1/image-20260511150909122.png)

You’ll notice that this entire process feels exactly like talking to AI inside the Cursor editor. The difference is that now you’re calling it through code, which means you can embed it into CI/CD pipelines, automation scripts, or even your own products. A normal large-model SDK can only help generate text, but an AI coding tool’s SDK can directly operate a codebase, call tools, and generate files.

If the task is just a simple one-off request, there’s an even shorter way to write it:

```typescript
const result = await Agent.prompt(
  "给这个项目写一个 README.md",
  {
    apiKey: process.env.CURSOR_API_KEY!,
    model: { id: "composer-2" },
    local: { cwd: process.cwd() },
  }
);
```

The example above demonstrated local runtime mode, where the agent runs directly on your own computer, making it suitable for development and debugging. In addition, the Cursor SDK also supports Cursor-hosted cloud mode, where Cursor spins up an isolated virtual machine in the cloud for task execution, which is suitable for running multiple agents in parallel; and self-hosted cloud mode, where you manage the server yourself, which is suitable for enterprise internal use.

Once you have an SDK for an AI coding tool, you can even treat the AI coding tool itself as a kind of development environment. Just as deploying a project requires configuring a database, you can configure an AI coding environment on a server and then call it through the SDK in your code to automate tasks like code generation, review, and refactoring.

Besides Cursor, Anthropic’s Claude Agent SDK and GitHub’s Copilot SDK also provide similar capabilities, and the usage patterns are broadly alike.



## How Should You Choose?

Now that we’ve covered the five AI application development modes, which one should you choose in real development?

Here’s a simple comparison I made for you:

| Mode | One-Sentence Summary | Best For |
|------|-----------|--------|
| HTTP API | Manually assemble requests to call the model; lowest-level and most flexible | People who want to understand low-level principles, or languages unsupported by SDKs |
| Official SDK | Call the model through officially wrapped toolkits | Daily development for most developers |
| AI Development Framework | Memory, RAG, tool use, and more available out of the box | Teams building complete AI applications |
| Low-Code Platform | Drag and drop to build, no coding needed | Non-technical users and fast idea validation |
| AI Coding Tool SDK | Let an AI agent write code for you | People who want to integrate AI coding power into automation workflows |

Keep in mind that these five modes are not mutually exclusive. In actual development, they’re often mixed together. For example, you might use a low-code platform to quickly build a prototype and validate an idea, then rewrite it as a formal version using a development framework once validated. Or inside a framework-based project, you might still call a special interface directly through raw HTTP API for certain modules.

**The core principle for choosing is: solve the current problem with the lowest cost possible.** If drag-and-drop can solve it, don’t write code. If a framework can handle it, don’t reinvent the wheel. If an SDK can handle it, don’t hand-write raw HTTP calls.

![](https://pic.yupi.icu/1/07_5%E7%A7%8D%E6%A8%A1%E5%BC%8F%E5%AF%B9%E6%AF%94%E6%80%BB%E7%BB%93-%E9%87%91%E5%AD%97%E5%A1%94%E5%9B%BE_compressed_v1.png)

That said, if you’re still in the learning phase, I actually recommend the opposite order: start with raw HTTP APIs, then move upward layer by layer. That way, you’ll gain a clear understanding of the principles behind each abstraction, and later when you use higher-level tools, you won’t feel lost.



## Final Thoughts

The field of AI application development changes extremely fast. New frameworks and new tools seem to pop up almost every month.

But no matter how much things change, the underlying patterns are still these few modes. Once you understand them, no matter what new tool appears in the future, you’ll be able to quickly identify which layer it belongs to and what problem it solves.

Going back to the interview scenario at the start: if you can clearly explain the applicable scenarios, strengths, and weaknesses of these five modes, the interviewer will very likely see you in a whole new light.

If you want to build real AI projects, [Programming Navigation](https://www.codefather.cn/) has multiple AI project tutorials that guide you step by step from 0 to 1 in building complete AI applications. Keep going!
