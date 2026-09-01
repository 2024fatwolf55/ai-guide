# Kimi K2 - AI Document Reading Assistant Project Practice

This project is an AI document reading assistant website that helps you quickly understand all kinds of complex documents (papers, technical docs, PDFs, and more), while also helping you manage your documents.

The project includes a complete frontend and backend. The whole thing was developed through conversations with AI without writing a single line of code, making it suitable for anyone who wants to quickly practice the full Vibe Coding workflow and learn how to use AI to build practical tools.



---



Hello everyone, I’m programmer Yupi. The school season is here, and I’m sure many of you are about to start collecting and reading papers. I also read docs when learning new technical knowledge, and I know exactly how painful it can be. You understand every word individually, but once they’re put together, somehow you can’t understand the text anymore.

![](https://pic.yupi.icu/1/1757559057843-b9d37369-49bf-4eec-878a-c70ac945cbd9.png)

To spare everyone from the suffering of reading documents, I used AI to build an AI document assistant website that helps you quickly understand all kinds of complex documents and also manage them.

![](https://pic.yupi.icu/1/1757561248387-205bf672-7a6c-452a-a283-698fb526601c.png)

The website is completely free, and the code is fully open source!

Open-source repository: [github.com/liyupi/literature-assistant](https://github.com/liyupi/literature-assistant)

![](https://pic.yupi.icu/1/1757829143308-d5bfdac6-847a-4061-9194-4821bdf3d3dc.png)

Next, I’ll first show everyone how to use the website, then share how this site was built, as well as how to use Claude Code in China.

⭐️ I recommend watching the video version—learn it in 2 minutes: [bilibili.com/video/BV1MnpVzdETW](https://www.bilibili.com/video/BV1MnpVzdETW/)



## How to Use It?

First, download the open-source code to your computer, then directly run the quick start script I provided. Open the webpage and you’ll see the result.

💡 Make sure your computer has Node.js and Java installed. You can refer to the `README.md` document for installation instructions.

![](https://pic.yupi.icu/1/1757567928358-ad506045-faaf-47b1-b742-190c83c94ad3.png)



When you want to read a document, click the **Single Import** button, upload the document file, and then fill in the Kimi AI API Key.

![](https://pic.yupi.icu/1/1757560732751-de713284-c039-41c1-b9f4-0af34e4c703c.png)



I chose Kimi because they had just released the new K2 model, which performs very well in coding, reasoning, and document understanding;

and it supports a 256K context window, so even papers with hundreds of thousands of words are no problem.

![](https://pic.yupi.icu/1/1757560219469-2eab0801-a9b3-49dd-b680-d1d27c1850cf.png)



In benchmark tests like SWE-bench Verified, which emphasize real software engineering tasks, the new Kimi K2 model also performs quite well:

![](https://pic.yupi.icu/1/1757560161782-1c78bd3c-a3a5-42f9-b79b-a0b07d808e6b.png)



Just log in to the [Kimi developer console](https://platform.moonshot.cn/), then go to API Key management to get a key for calling the large model.

![](https://pic.yupi.icu/1/1757560312832-cfd4158d-8c31-4c22-8b42-573551334863.png)



Although new users get free credits, don’t leak your key!

![](https://pic.yupi.icu/1/1757560674974-180d8475-e83e-4b35-ba9b-2ded866aa730.png)



After filling in the API Key, you can generate a document reading guide, and it’s very fast.

![](https://pic.yupi.icu/1/1757560771758-4c3df93e-889d-4c74-afa2-90e69347f286.png)



The AI-generated result is pretty good, combining text and images to help you understand complex documents more quickly.

![](https://pic.yupi.icu/1/1757560820325-87111dd8-cd82-49d0-9385-24ea9a33e885.png)



You can also import multiple documents in batches and call AI to generate reading guides at the same time, improving efficiency.

![](https://pic.yupi.icu/1/1757560886812-1706415c-cff5-4475-872f-ba66891563f7.png)



In addition, you can use this website as your own smart document bookmark folder. You can categorize and search imported documents, download the original files, and view document reading guides at any time. **Don’t let the documents you saved disappear on you again~**

![](https://pic.yupi.icu/1/1757560925975-079ad961-7cc8-498b-99e2-84a4a534023f.png)



## How Was It Built?

In the past, a site like this might have taken several days to build. But now AI coding technology is already quite mature. I chose Claude Code as the AI development tool and finished it easily in one day without writing a single line of code myself.

First, enter one command in the terminal to install Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

Then run the `claude` command and you can start asking it questions~

But as a result, it threw an error!

![](https://pic.yupi.icu/1/1756451588360-37620a0b-bc2f-4ad5-adf9-4efde87f17ed.png)

**Damn, this thing still doesn’t support use in China!**

But that’s okay—we can switch to Kimi. Enter the following commands in the terminal to configure environment variables (be sure to distinguish between operating systems):

```bash
# Linux/macOS 启动高速版 kimi-k2-turbo-preview 模型
export ANTHROPIC_BASE_URL=https://api.moonshot.cn/anthropic
export ANTHROPIC_AUTH_TOKEN=<你的 API 密钥>
export ANTHROPIC_MODEL=kimi-k2-turbo-preview
export ANTHROPIC_SMALL_FAST_MODEL=kimi-k2-turbo-preview

# Windows Powershell 启动高速版 kimi-k2-turbo-preview 模型
$env:ANTHROPIC_BASE_URL="https://api.moonshot.cn/anthropic";
$env:ANTHROPIC_AUTH_TOKEN=<你的 API 密钥>
$env:ANTHROPIC_MODEL="kimi-k2-turbo-preview"
$env:ANTHROPIC_SMALL_FAST_MODEL="kimi-k2-turbo-preview"
```



Then you can happily use Claude Code to generate code~

![](https://pic.yupi.icu/1/1756451713145-29e5ba15-76b2-4848-903a-f098b942e2f9.png)



For a website that includes a full frontend and backend, it’s hard to get AI to generate a satisfying result with just one prompt. So we need to **break the work into steps** like in real enterprise development: backend first, then frontend, then frontend-backend integration and joint debugging. It’s also best to develop one feature at a time and adjust promptly when problems appear.

Here are some reference prompts:

![](https://pic.yupi.icu/1/1757567728565-5724de3e-7863-457b-9866-368c1535bd2c.png)



------



That’s all for this round of sharing. I hope this tool is helpful to everyone, and don’t forget to support Yupi with likes, shares, and comments. Thank you all~

![](https://pic.yupi.icu/1/1757829315038-73ef4fd7-7fef-4fa2-859d-11bb28381933.webp)


## Recommended Resources

1) Yupi AI Navigation Website: [Comprehensive AI Resources, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Paths, Programming Tutorials, Practical Projects, Job Hunting Guide, Q&A](https://www.codefather.cn)

3) Programmer Interview Cheatsheet: [High-Frequency Topics for Internships / Campus Hiring / Experienced Hiring, Plus Real Interview Question Analysis](https://www.mianshiya.com)

4) Programmer Resume Writing Tool: [Professional Templates, Rich Example Sentences, Direct to Interview](https://www.laoyujianli.com)

5) 1-on-1 Mock Interview: [A Must-Have for Internship / Campus Hiring / Experienced Hiring Interviews to Land Offers](https://ai.mianshiya.com)
