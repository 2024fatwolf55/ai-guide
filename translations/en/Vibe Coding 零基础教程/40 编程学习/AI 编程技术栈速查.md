# Which Technologies Must You Understand in the AI Coding Era?

When you build projects with AI coding, you’ll definitely run into all kinds of technical terms you’ve never seen before.

For example, AI might tell you: use Next.js for the frontend, Prisma for the database, and deploy to Vercel.

And you’re just staring at it like: what are these things? Forget it, let AI handle everything, I don’t need to care...

![](https://pic.yupi.icu/1/%E5%95%A5%E5%95%A5%E5%95%A5%E8%A1%A8%E6%83%85%E5%8C%85.jpg)

But here’s the problem: if you have zero idea what these technologies are, you won’t be able to clearly communicate what you want to AI, and if AI chooses the wrong direction, you won’t even know how to judge it.

I ran into this before on a project. AI used a very niche database solution for me, and since I didn’t understand it, I just accepted it. Later, when I wanted to add new features, I found the ecosystem was terrible and there were no ready-made solutions for many things, so I had to scrap it and start over.

That’s why I wrote this article: to help you sort out the core technologies of the AI coding era. You don’t need to deeply learn every single one, but at minimum, you should know what they do, when to use them, and what to keep in mind when making technical choices.



## 1. Programming Languages

First, you need to understand the two most commonly used programming language stacks in AI coding.

#### 1. JavaScript / TypeScript

JavaScript was originally a language for browsers, responsible for all kinds of interactive effects on web pages. Later, with the arrival of Node.js, it could also run on servers for backend development, so JS became a true full-stack language that works on both frontend and backend.

![](https://pic.yupi.icu/1/article-images/tech-stack/01_JavaScript%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80_compressed_v3.png)

TypeScript is an enhanced version of JavaScript that adds types to variables, allowing the editor to help catch mistakes while you code.

Nowadays, AI prefers to generate TypeScript by default, because with type information, AI can understand code context more accurately and the quality of generated code is higher.

If you want to build web-related projects, JS/TS is basically a must.

![](https://pic.yupi.icu/1/article-images/tech-stack/02_TypeScript%E7%B1%BB%E5%9E%8B%E7%B3%BB%E7%BB%9F%E5%A2%9E%E5%BC%BA_compressed_v3.png)



#### 2. Python

Python syntax is close to English and reads almost like pseudocode, so many total beginners learn Python as their first language.

It dominates fields like AI, machine learning, data analysis, and automation scripts. A huge number of AI frameworks and tools are written in Python.

If you want to build AI applications, process data, or write crawlers, Python is an excellent choice.

![](https://pic.yupi.icu/1/article-images/tech-stack/03_Python%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80_compressed_v2.png)

Simply put, choose JS/TS for websites and Python for AI applications. Knowing both is even better.



## 2. The Frontend Trio

The frontend is the part users can see and interact with—in other words, everything you see in the browser.

In AI coding, the frontend is the easiest part to handle, because after changing code, you just refresh and immediately see the result.

The traditional frontend trio is HTML + CSS + JavaScript. But in the AI era, I’d call React + Next.js + Tailwind CSS the new frontend trio, because this is the combination AI coding tools love most.

#### 1. React

React is a frontend framework developed by Meta. Its core idea is to split a page into reusable components.

For example, a button is one component, and a navigation bar is another. Put them together like building blocks, and you get a complete page.

According to developer survey data, React’s usage rate exceeds 80%, making it the most mainstream frontend framework in the world. AI has seen more React code than anything else during training, so it also generates React code with the highest quality. Most of our team’s products are built with React.

![](https://pic.yupi.icu/1/article-images/tech-stack/07_React%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6_compressed_v1.png)



#### 2. Next.js

Next.js is a full-stack framework based on React and developed by Vercel.

What makes it powerful is that it can handle not only frontend pages, but also backend APIs in the same project, truly letting one project cover both frontend and backend. It also supports server-side rendering, which is very friendly for search engine indexing.

Many AI no-code platforms generate projects in Next.js by default. Create a folder inside the `app` directory, and it automatically maps to a page route. Backend APIs live under `app/api`, so frontend and backend code can stay in the same project while remaining logically separate.

And it can be deployed to Vercel very easily. Just push the code to GitHub, connect the repository, and every push will automatically build and go live. Very convenient.

![](https://pic.yupi.icu/1/article-images/tech-stack/09_Next.js%E5%85%A8%E6%A0%88%E6%A1%86%E6%9E%B6_compressed_v1.png)



#### 3. Tailwind CSS

Tailwind CSS is a utility-first styling framework.

In traditional web development, you first write HTML structure, then write CSS files to define styles. Tailwind takes a different approach: it turns commonly used styles into small class names that you can combine directly in HTML. For example, if you want an element centered both horizontally and vertically, writing `flex justify-center items-center` gets the job done.

At first, you might feel those long strings of class names look ugly, but once you get used to it, it’s hard to go back.

AI-generated frontend code also loves using Tailwind by default, because it doesn’t require maintaining separate CSS files, and each style class has only one standard way to write it, which makes AI’s generation accuracy especially high.

![](https://pic.yupi.icu/1/article-images/tech-stack/11_Tailwind_CSS%E5%8E%9F%E5%AD%90%E5%8C%96%E6%A1%86%E6%9E%B6_compressed_v1.png)

But you may have noticed that AI-generated pages often end up with blue-purple gradient color schemes. That’s because Tailwind’s default palette includes lots of blue and purple, so AI finds it especially easy to use, and the results end up all looking the same... If you want to avoid that, remember to clearly specify the color style you want in your prompt.

Why do React + Next.js + Tailwind CSS always show up together?

Because AI models learn from massive amounts of code on the internet, and React, Next.js, and Tailwind CSS happen to be one of the most commonly used combinations in open-source projects over the past few years. AI knows them best, so it generates the most reliable code with them. This creates a flywheel effect: the more AI recommends them, the more people use them; the more people use them, the more training data they generate; and the more training data there is, the more AI recommends them.



## 3. Backend Frameworks

The backend is the part users can’t see. It handles business logic, stores data, and manages user identities.

When you click the “Register” button on a website, the frontend sends the information you entered to the backend, and the backend validates the data, stores it in the database, and returns the result.

If you use Next.js, you can actually write backend APIs directly in the same project, without creating a separate backend project. But if you need a more independent and more powerful backend service, then you need to choose a backend framework.



#### 1. Spring Boot

Spring Boot is the standard framework for Java backend development, and most enterprise backend systems in China are built with it.

Its philosophy is “convention over configuration,” helping simplify all kinds of tedious setup and making it usable out of the box.

If you want to learn AI coding while also improving your backend employability, Spring Boot is a must-learn. And with the launch of the Spring AI framework, Java developers can now build AI applications very conveniently too.

![](https://pic.yupi.icu/1/article-images/tech-stack/24_Spring_Boot%E6%A1%86%E6%9E%B6_compressed_v2.png)



#### 2. FastAPI

FastAPI is the fastest-growing backend framework in the Python ecosystem, and nearly 40% of Python developers now use it. It has built-in support for async and type checking, and API documentation is generated automatically after you write the interface—no extra maintenance needed.

One of the best things about FastAPI is that after startup, visiting the `/docs` path shows an interactive API documentation page where you can test the interface directly in the browser. If you ask AI to generate a Python backend project, there’s a high chance it will choose FastAPI.

![](https://pic.yupi.icu/1/article-images/tech-stack/25_FastAPI%E6%A1%86%E6%9E%B6_compressed_v1.png)

Simply put, choose Spring Boot for the Java route, FastAPI for the Python route, and if you want convenience, use Next.js API Routes to handle frontend and backend in one shot.



## 4. Data Storage

Data that needs to be queried repeatedly on a website—such as user information, article content, and order records—needs to be stored in a database.

#### 1. MySQL / PostgreSQL

Relational databases are like Excel spreadsheets: data is arranged in rows and columns, and relationships can be built between different pieces of data.

![](https://pic.yupi.icu/1/1769046133583-18e6b389-b3b7-4c56-b5f3-7482a3897bd3.png)

MySQL and PostgreSQL are the two most mainstream relational databases, and both are open-source and free.

![](https://pic.yupi.icu/1/1769046291097-2dea6cb4-76e5-45ef-8799-e187324eee46.png)

MySQL is the most widely used in China, and for almost any problem you encounter, you can usually find a solution online. PostgreSQL is more powerful overall: it supports JSON data types, geospatial data, full-text search, and even vector search through the `pgvector` extension. That makes it especially suitable for AI applications, and many overseas SaaS products and AI projects use PostgreSQL.

By the way, in code, people usually don’t operate databases by writing SQL directly. Instead, they use ORM tools. For example, Node.js projects often use Prisma, Java projects often use MyBatis-Plus, and Python projects often use SQLAlchemy. With an ORM, working with data in code becomes as convenient as working with normal objects.



#### 2. Supabase

If you don’t want to maintain a database yourself, there’s also an easier option.

Supabase is an open-source backend-as-a-service platform built on top of PostgreSQL, offering features such as databases, authentication, file storage, and real-time subscriptions.

You can use it just by registering an account, and the free quota is enough for personal projects.

You can tell AI, “Use Supabase for the database and authentication,” and it can generate the full integration code for you.

![](https://pic.yupi.icu/1/article-images/tech-stack/36_Supabase%E5%90%8E%E7%AB%AF%E6%9C%8D%E5%8A%A1_compressed_v1.png)



## 5. Deployment

Once the code is written, how do you make your website accessible to people all over the world?

You need to deploy the code to a server.

#### 1. Vercel

The easiest way is to use Vercel.

It’s the company behind Next.js, so it offers the best support for Next.js projects. You just push your code to GitHub, and Vercel automatically builds and deploys it for you. It can go live in minutes, and it comes with HTTPS and CDN acceleration built in. The free quota is more than enough for personal projects, making it especially suitable for small projects built with AI coding.

![](https://pic.yupi.icu/1/article-images/tech-stack/44_Vercel%E9%83%A8%E7%BD%B2%E5%B9%B3%E5%8F%B0_compressed_v3.png)



#### 2. Linux Cloud Servers

However, Vercel’s servers are overseas, and it’s more suitable for frontend and full-stack projects. If you want to build a commercial product for users in China, or if your backend is an independent Java or Python service, then you’ll need to buy your own Linux cloud server.

Domestic cloud providers include Alibaba Cloud, Tencent Cloud, and others. New users usually get free trials or large discounts, and a 2-core 4GB machine is enough for personal projects.

The operating systems on servers are basically all Linux, so it’s useful to know some basic Linux commands such as using `cd` to enter directories and `ls` to list files. But for most operations, AI can help generate the commands, so you don’t need to memorize them.



#### 3. Docker

Docker can package your code, runtime environment, and dependency libraries into a “container,” so it runs the same way on any machine.

In the past, people often ran into the problem of “it works on my computer but fails on the server.” With Docker, that issue disappears.

Packaging an application with Docker is simple. Just let AI help you write the Dockerfile. There’s no need to memorize Docker file syntax yourself.

![](https://pic.yupi.icu/1/article-images/tech-stack/46_Docker%E5%AE%B9%E5%99%A8%E5%8C%96_compressed_v2.png)

If your project involves multiple services, such as frontend + backend + database, you can also use `docker-compose` to start them all with one command.



## 6. Code Management

#### 1. Git

When building projects with AI coding, I recommend using Git to manage your code. For example, before asking AI to modify code, first commit one version. If AI breaks something, you can roll back. It’s like making a save point in a game before fighting the boss, so if you die, you can start over.

You don’t need to memorize Git commands, because AI can help you perform Git operations. But you should understand several core concepts, such as `commit` meaning saving a version, `branch` meaning creating a branch, and `push` meaning sending code to a remote repository.

![](https://pic.yupi.icu/1/07_Git%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86%E5%90%8E%E6%82%94%E8%8D%AF_compressed_v3.png)



#### 2. GitHub

GitHub is the world’s largest code hosting platform, and people used to joke that it was a kind of social platform for programmers. It contains a huge number of open-source projects and is a treasure trove of programming learning resources.

You can push your code to GitHub for backup, sharing, and collaboration. The Vercel deployment mentioned earlier works by connecting your GitHub repository for automatic release.

![](https://pic.yupi.icu/1/article-images/tech-stack/71_GitHub%E4%BB%A3%E7%A0%81%E6%89%98%E7%AE%A1%E5%B9%B3%E5%8F%B0_compressed_v1.png)



## 7. Calling AI Large Models

With AI coding plus AI model services, you can easily build your own AI applications, such as an AI customer service bot, an AI writing assistant, or an AI data analysis tool.

To do those things, the first step is understanding how to call large models from code.



#### 1. OpenAI API

The OpenAI API is currently the most universal way to call large models.

OpenAI provides a standard API that you can use for chat, text generation, code generation, image generation, and more. You can install the SDK for your programming language, initialize the client with an API key, and then call the model.

Many other AI providers also support an OpenAI-compatible API format, such as DeepSeek and Qwen. So once you learn how to call the OpenAI API, switching to other models becomes easy.

![](https://pic.yupi.icu/1/article-images/tech-stack/72_OpenAI_API%E8%B0%83%E7%94%A8GPT%E5%A4%A7%E6%A8%A1%E5%9E%8B_compressed_v2.png)

If you want to switch flexibly among different models within a project, you can also use a unified interface service like OpenRouter, where one key lets you call hundreds of large models.



#### 2. LangChain

Once you know the basics of calling large models, if you want to build more complex AI applications—such as letting AI use tools autonomously or orchestrating multi-step workflows—then you’ll need an AI application development framework.

LangChain is arguably the most popular AI application development framework. You can think of it as “building blocks” for AI app development. It includes a large number of integration components out of the box, such as connectors for various large models, vector databases, tool calling, and more. For quickly building AI application prototypes, LangChain can save you a huge amount of boilerplate code.

But one thing to keep in mind: LangChain is more suitable for prototype development and complex multi-model orchestration scenarios. If your application is relatively simple, using OpenAI or each provider’s SDK directly will be lighter-weight.

![](https://pic.yupi.icu/1/article-images/tech-stack/76_LangChain_AI%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6_compressed_v1.png)



## 8. Vector Databases and RAG

When building AI applications, you often run into one problem: large models have a knowledge cutoff date, and they also lack your own private knowledge.

For example, if you want AI to answer employee questions based on internal company documents, asking a large model directly won’t work.

That’s when you need RAG.

RAG stands for Retrieval-Augmented Generation. Its core idea is **search first, answer later**: before answering, the large model first searches for relevant materials, then organizes an answer based on what it finds. It’s basically like an open-book exam—if you don’t know something, you flip through the book first.

![](https://pic.yupi.icu/1/1776332850706-68cb05fe-7022-445c-9c3d-944f74f48dee.png)

But how do you search for relevant materials?

If you rely on keyword matching, it’s easy to run into cases where the wording in the question doesn’t match the wording in the document. That’s why you need the concept of **vectors**.

Simply put, a vector represents a piece of text as a sequence of numbers so that a computer can compare semantic similarity. The model that converts text into vectors is called an embedding model, and the database that stores those vectors and supports fast similarity search is called a vector database.

![](https://pic.yupi.icu/1/1769046928023-6111fd54-4926-4ef0-b67b-e10f3af57d52.png)

The RAG process is really just two steps:

1. Split your documents into small chunks, convert them into vectors, and store them in a vector database.
2. When a user asks a question, convert the question into a vector as well, search the vector database for the most similar document chunks, and then pass those chunks together with the user’s question to the large model to generate an answer.

![](https://pic.yupi.icu/1/1776650476421-3bfb3c26-575d-4cc4-9538-f74a4589b42d.png)

In the AI era, vector databases are being used more and more widely. They’re needed for AI knowledge bases, semantic search, and recommendation systems. Mainstream vector databases include Milvus, Chroma, and Qdrant, and PostgreSQL can also support vector search through the `pgvector` extension.

![](https://pic.yupi.icu/1/1769047066536-0ef08cd3-b86b-4c97-9016-7add32a710b8.png)

If you want to understand more advanced RAG approaches, I previously wrote a panoramic science-style article on [from Naive RAG to Agentic RAG](https://mp.weixin.qq.com/s/r_HwTfIyShV5Ke0UY6b-4g), and you can check it out if you’re interested.



## Final Thoughts

This article is a streamlined introduction to the AI coding tech stack. In Yupi’s video course [AI Coding in Practice for Complete Beginners](https://ai.codefather.cn/course/2087008226460565505), I also included the full version of the *AI Coding Tech Stack Quick Reference Manual*, which covers many more technologies in detail so you can quickly look up and understand any unfamiliar tool.

I’ve helped you sort through the core technologies of the AI coding era, from programming languages to frontend and backend frameworks, from databases to deployment, and from calling AI large models to RAG knowledge bases.

With AI-assisted programming, you don’t need to study every technology deeply. As long as you know what it is and when it should be used, AI can handle the concrete code implementation for you.

**Technology serves products. Don’t study technology just for the sake of studying technology.**

That said, if you want a programmer-related job, you still need to learn these technologies systematically—but you don’t need to master every single one. In the real process of building projects, learn what you encounter and look up what you need. Keep going!
