# Vibe Coding AI Application Development

Hello, I'm Yupi.

Today, AI is no longer a distant high-tech concept but a tool that every developer can easily use. By calling AI APIs, you can quickly create various intelligent applications, such as chat assistants, writing assistants, image generators, and more. These projects are not only fun but also highly practical. You can use them directly or showcase them as portfolio projects.

In this article, I will guide you through building 4 popular AI applications: an AI Chat Assistant, a Smart Writing Assistant, an AI Image Generator, and a Speech Recognition App.

Before we start, it's important to note that this tutorial focuses more on guiding you through the thought process and project development workflow. The goal is to help you learn how to develop projects using Vibe Coding. You will need to practice on your own. If you need more comprehensive Vibe Coding tutorials with images and videos, you can check out Yupi's original project实战 section.

## 1. Basics of AI Application Development

Before diving into the projects, let's first understand the basics of AI application development.

An AI application leverages AI capabilities (such as text generation, image generation, speech recognition, etc.) to solve real-world problems. You don't need to train AI models; you just need to call existing AI APIs. It's like driving a car—you don't need to know how the engine works; you just need to know how to drive.

Currently, there are many mainstream AI API services. For text generation, there's OpenAI's GPT-4, Anthropic's Claude, Google's Gemini, and domestic models like Tongyi Qianwen, Wenxin Yiyan, and Zhipu AI. For image generation, there's DALL-E 3, Midjourney, Stable Diffusion, and domestic models like Wenxin Yige. For speech recognition, there's OpenAI's Whisper, Google Speech-to-Text, and iFlytek's speech recognition.

The development process for AI applications is similar to that of regular applications, with the added step of calling AI APIs. The overall workflow is: User Input → Process Input → Call AI API → Process AI Response → Display Results.

Sounds simple, right? Indeed, the barrier to entry for AI application development is now very low.

![](https://pic.yupi.icu/1/aiapp-workflow%E5%A4%A7.jpeg)

When developing AI applications, there are a few things to keep in mind.

First, API Key security: Do not expose your API Key in front-end code, as others can misuse it. Second, cost control: AI APIs charge based on usage, so manage costs to avoid waste. Third, error handling: API calls can fail, so handle errors gracefully and provide user-friendly prompts. Lastly, user experience: AI responses may take a few seconds, so provide loading indicators to let users know processing is underway.

## 2. Project实战 - AI Chat Assistant

The AI Chat Assistant is the most basic yet practical AI application. Through this project, you will learn how to quickly develop a complete AI conversation application using Vibe Coding.

This project aims to implement a complete chat interface where users can input questions, and the AI provides answers. It should support multi-turn conversations, allowing the AI to remember previous content for coherent dialogue. For a better user experience, the AI's responses should be displayed character by character rather than all at once, known as streaming output. Conversation history should be saved locally, so it doesn't disappear on page refresh. Additionally, there should be a clear conversation function to start new topics easily.

![](https://pic.yupi.icu/1/demoweb6.png)

For the tech stack, we'll use React + TypeScript + Vite as the front-end framework and Tailwind CSS for styling. AI capabilities will be implemented by calling large model APIs, conversation history will be saved using LocalStorage, and AI responses will be rendered using react-markdown to support features like code highlighting.

### Development Steps

1) Preparation

The first step in development is preparation. You need to obtain an API Key to call the AI model. Visit the [Zhipu AI Open Platform](https://bigmodel.cn), enter the user console, and click on API Key to get one. Zhipu AI's GLM model performs well and offers free quotas, making it suitable for learning.

2) Write the Requirements Document

With the API Key, you can start writing the requirements document. Create a `PRD.md` file to clearly define what you want to achieve:

```markdown
# AI Chat Assistant PRD

## Core Features
1. Users can input questions, and the AI provides answers
2. Supports multi-turn conversations; the AI remembers previous dialogue
3. AI responses are displayed character by character, not all at once
4. Conversation history is saved locally and persists on page refresh
5. Users can clear conversations to start new topics
6. AI responses support Markdown formatting, including code highlighting

## UI Requirements
- Chat interface similar to WeChat
- User messages on the right, AI messages on the left
- Input box and send button at the bottom
- Clean and modern design style
```

This document clearly outlines the functionality and interface requirements.

3) Write the Technical Design Document

Next, write the technical design document `TECH_DESIGN.md`:

```markdown
# Technical Design

## Tech Stack
- React + TypeScript + Vite
- Tailwind CSS
- Zhipu AI API
- LocalStorage for conversation history
- react-markdown for Markdown rendering

## Data Structure
- Message: role (user or assistant), content, timestamp
- Conversation history stored in LocalStorage

## API Calls
- Use Zhipu AI Chat Completions API
- Enable stream mode for streaming output
- Store API Key in environment variables
```

This document specifies the technologies used, the data structure, and how API calls will be made.

4) Write the AGENTS.md File

Next, create an `AGENTS.md` file to outline development guidelines for the AI:

```markdown
# AI Chat Assistant Development Instructions

## Project Overview
An AI Chat Assistant developed using React + TypeScript, leveraging Zhipu AI API for dialogue functionality.

## Development Guidelines
- Use TypeScript for type safety
- Use Tailwind CSS for styling
- Read API Key from environment variables; do not hardcode
- Provide friendly error messages

## Feature Requirements
- Implement streaming output; AI responses should be displayed character by character
- Support multi-turn conversations; send historical messages to the API
- Save conversation history in LocalStorage
- Support Markdown rendering and code highlighting

## Notes
- Handle API call failures
- Provide clear loading indicators
- Disable the input box during sending to prevent duplicate submissions
```

This file serves as the development guideline for the AI, informing it how the code should be written.

5) Develop with AI Dialogue

With these three documents in place, you can start developing with AI dialogue. Open Cursor and place these three documents in the project root directory.

The first step is to initialize the project:

```
Please initialize a React + TypeScript + Vite project based on the requirements in PRD.md, TECH_DESIGN.md, and AGENTS.md, and install necessary dependencies: Tailwind CSS, react-markdown, react-syntax-highlighter.
```

This prompt tells the AI what project to create and which dependencies to install. The AI will read these three documents and create the project structure, install dependencies, and configure Tailwind CSS accordingly.

The second step is to create data types and API wrappers:

```
Create a types.ts file to define the Message type. Then create an api.ts file to wrap the Zhipu AI API calls, supporting streaming output and reading parameters from environment variables.
```

This step lays the foundation for subsequent development by encapsulating data structures and API calls, making them easier to use later.

The third step is to implement the chat interface:

```
Create a ChatInterface component to implement the chat interface. Requirements:
1. Display the message list at the top, with user messages on the right and AI messages on the left
2. Include an input box and send button at the bottom
3. Use Tailwind CSS to achieve a WeChat-like chat interface style
4. Messages should support Markdown rendering
```

This prompt specifies the layout and styling requirements for the interface. The AI will create a complete chat interface component.

The fourth step is to implement the conversation functionality:

```
Implement the message sending functionality:
1. Add user messages to the message list after input
2. Call the API to get the AI's response
3. Use streaming output to display the AI's response character by character
4. Send historical messages to the API to enable multi-turn conversations
5. Disable the input box during loading and display "Thinking..."
```

This prompt includes all the requirements for the conversation functionality. Streaming output is key, as it makes the AI's response appear character by character like typing, enhancing the user experience. Multi-turn conversations are also important; sending previous dialogue history to the API allows the AI to remember earlier content.

The fifth step is to add data persistence:

```
Use LocalStorage to save conversation history:
1. Automatically save after each conversation update
2. Read historical records on page load
3. Add a "Clear Conversation" button to delete history
```

This ensures that users' previous conversations remain intact even after refreshing the page.

The sixth step is to optimize the user experience:

```
Optimize the user experience:
1. Automatically scroll to the bottom when new messages appear
2. Add a copy button to easily copy the AI's response
3. Enable syntax highlighting for code blocks
4. Display friendly error messages when API calls fail
```

These small details can significantly enhance the user experience.

### Development Tips

During development, there are a few tips to help you work more efficiently. First, don't ask the AI to implement all features at once. Break it down into smaller steps, testing each step as you go. This makes it easier to locate and fix issues if they arise.

Second, provide sufficient context when conversing with the AI. Clearly tell it what functionality to implement, specific requirements, and guidelines to follow. The clearer the context, the higher the quality of the code generated by the AI.

If you encounter issues with the code, share the complete error message with the AI so it can analyze and fix the problem. Don't just say "the code has an error"; paste the specific error message.

### Extension Ideas

Once the basic version is complete, you can extend its functionality.

For example, add system prompt settings to let the AI play different roles (e.g., programming assistant, writing assistant, psychological counselor); support multiple conversation sessions to handle multiple topics simultaneously; add voice input functionality to converse with the AI via voice; integrate image recognition to allow the AI to answer questions based on images; support exporting conversation history to save important dialogues.

## 3. Project实战 - Smart Writing Assistant

After mastering the basic workflow of AI dialogue, let's build a more professional application—the Smart Writing Assistant. Writing assistants are one of the most practical use cases for AI. Through this project, you will learn how to use prompt engineering to have the AI complete different writing tasks.

This project will support various writing modes, such as article continuation, content rewriting, copywriting generation, email drafting, and more. Users can adjust parameters like creativity level and output length to control the AI's generation results. Additionally, users can optimize text grammar and expression with a single click to make the text more professional. For convenience, multiple versions can be generated at once, allowing users to choose the most satisfactory one. Generated content should be saved to a history log for easy review and management.

![](https://pic.yupi.icu/1/demoweb7.png)

The tech stack is similar to the chat assistant, using React + TypeScript + Vite with Tailwind CSS. The core functionality still relies on calling the Zhipu AI API, with data saved in LocalStorage.

### Development Steps

1) Design Prompt Templates

The first step in development is to design prompt templates. Before writing code, design prompts for different writing tasks. Create a `prompts.md` file to define prompts for various writing modes:

```markdown
# Writing Assistant Prompt Templates

## Article Continuation
Please continue the following article, maintaining consistent style and coherent content:
[User input]

## Content Rewriting
Please rewrite the following content to make it more fluent and professional:
[User input]

## Content Expansion
Please expand the following content by adding more details and examples:
[User input]

## Content Summarization
Please summarize the following content, extracting key points:
[User input]

## Email Drafting
Please write a [formal/friendly] email with the subject: [Subject]

## Copywriting Generation
Please write a [style] marketing copy for [Product Name]
```

Prompts are the core of AI applications. Good prompts lead to better AI-generated results. A good prompt typically includes three elements: a clear task description, sufficient context, and clear output format requirements.

![](https://pic.yupi.icu/1/promptcompare%E5%A4%A7.jpeg)

For example, if you want the AI to write an article, don't just say "help me write an article." Instead, specify the topic, target audience, word count, and content to include. For example:

```markdown
Please write a popular science article about AI programming, targeting beginners, with easy-to-understand language and plenty of examples. The article should be 800-1000 words and cover what AI programming is, why to learn it, and how to get started.
```

This way, the AI knows exactly what to write.

If you're rewriting content, provide context for the AI. For example:

```markdown
This is the opening paragraph of a technical blog. Please rewrite it to be more engaging while maintaining professionalism.
```

This helps the AI understand the direction to take.

Specifying the output format is also important. If you want the AI to summarize an article, clearly state the format:

```markdown
Please summarize this article in the following format:
1. Key points (3-5)
2. Key data (if any)
3. Conclusion (one sentence)
```

This ensures the generated result is structured and meets your needs.

Sometimes, providing examples can yield better results. For instance, if you want the AI to write marketing copy, provide a few examples for it to reference. This approach, known as Few-shot Learning, is effective in many scenarios.

2) Write the Requirements Document

After designing the prompt templates, write the requirements document. Create a `PRD.md` file:

```markdown
# Smart Writing Assistant PRD

## Core Features
1. Split layout with input on the left and generated results on the right
2. Supports 6 writing modes: continuation, rewriting, expansion, summarization, email, and copywriting
3. Allows adjusting creativity level (temperature) and output length
4. Generated content should be displayed via streaming
5. Includes an "Optimize Prompt" button for the AI to refine user descriptions
6. Saves generation history

## UI Requirements
- Top: Large title
- Input Area: Large text box (multi-line)
- Parameter Area: Size selection, style selection
- Button Area: Optimize Prompt, Generate Content
- Display Area: Shows generated content + Copy button
- Sidebar: History log
```

3) Develop with AI Dialogue

With the documents ready, you can start developing with AI dialogue.

First, create the basic interface:

```
Please create the Smart Writing Assistant interface based on PRD.md:
1. Split layout
2. Left: Mode selection dropdown + Input text box + Generate button
3. Right: Display generated content
4. Use Tailwind CSS for a visually appealing interface
```

Second, implement the prompt templates:

```
Create a promptTemplates.ts file to implement prompt functions for the 6 writing modes based on the templates in prompts.md. Each function should take user input and return a complete prompt.
```

This encapsulates the prompt logic, with different writing modes using different prompts.

Third, implement the content generation functionality:

```
Implement the content generation functionality:
1. User selects a mode, inputs content, and clicks Generate
2. Generate the corresponding prompt based on the selected mode
3. Call the Zhipu AI API with streaming output
4. Display the generated content in real-time on the right
5. Support Markdown rendering
```

Fourth, add parameter adjustments:

```
Add an advanced settings panel:
1. Creativity slider (temperature: 0-1)
2. Output length slider (max_tokens: 100-2000)
3. Pass these parameters to the API call
4. Allow collapsing/expanding advanced settings
```

The temperature value affects the creativity of the output.

- 0-0.3: Conservative, suitable for factual content
- 0.4-0.7: Balanced, suitable for most scenarios
- 0.8-1.0: Highly creative, suitable for creative writing

Fifth, add history logging:

```
Implement the history logging functionality:
1. Save each generation to LocalStorage
2. Save content: Prompt, generated result, generation time
3. Display the history log list on the left
4. Clicking a history log allows viewing previous content
5. Support deleting history logs
```

### Prompt Optimization Tips

If you're unsure whether your prompt is good enough, let the AI optimize it for you. For example, you can ask:

```
I want the AI to help me rewrite an article to make it more professional. My current prompt is: "Please rewrite this paragraph." Please optimize this prompt to help the AI generate better results.
```

The AI will provide a more detailed and effective prompt, such as:

```markdown
This is the opening paragraph of a technical blog. Please rewrite it to be more engaging while maintaining professionalism. Requirements:
1. Use more vivid language
2. Maintain technical accuracy
3. Keep the word count around 200
```

### Extension Ideas

Once the basic version is complete, you can extend its functionality. For example, add more writing templates to support different types of writing like essays, reports, and novels; allow custom prompt templates for users to create their own; add multi-language translation functionality for one-click translation; implement batch generation to produce multiple versions for selection; add text comparison functionality to compare differences between versions.

## 4. Project实战 - AI Image Generator

Moving from text generation to image generation, let's build an even cooler AI application. AI image generation is one of the most exciting AI applications, allowing you to generate stunning images with simple text descriptions. This project will teach you how to call image generation APIs.

The core of this project is text-to-image generation. Users input a description, select size and style, and click Generate to get an image. To help users write better prompts, include an "Optimize Prompt" feature where the AI expands simple descriptions into detailed prompts. Generated images should be saved to a history log and support downloading.

![](https://pic.yupi.icu/1/demoweb8.png)

The tech stack is similar to previous projects, primarily calling image generation APIs. Zhipu AI also provides image generation capabilities, and you can use the same API Key. [Visit the official site to get it](https://bigmodel.cn).

### Development Steps

1) Understand Image Generation APIs

The first step in development is to understand image generation APIs. The main parameters for image generation APIs include:

- prompt: Image description (most important)
- size: Image size (e.g., 1024x1024)
- quality: Quality (standard or high)
- style: Style (photorealistic or artistic)

Different parameter combinations will generate images with different effects.

2) Write a Requirements Document

Then write a requirements document `PRD.md`:

```markdown
# AI 图片生成器 PRD

## 核心功能
1. 用户输入图片描述，点击生成
2. 可以选择图片尺寸和风格
3. 生成过程显示加载动画（通常需要 10-30 秒）
4. 生成后显示图片，可以下载
5. 有"优化提示词"按钮，AI 帮用户优化描述
6. 保存生成历史

## 界面要求
- 顶部：大标题
- 输入区：大文本框（多行）
- 参数区：尺寸选择、风格选择
- 按钮区：优化提示词、生成图片
- 展示区：显示生成的图片 + 下载按钮
- 侧边栏：历史记录
```

3) Develop Through AI Conversation

Once the document is ready, you can start developing by talking with the AI.

First, create the basic interface:

```
请根据 PRD.md 创建 AI 图片生成器的界面：
1. 输入框：用户输入图片描述
2. 参数选择：尺寸（3 个选项）、风格（2 个选项）
3. 两个按钮：优化提示词、生成图片
4. 图片展示区
使用 Tailwind CSS，界面要美观。
```

Second, implement image generation:

```
实现图片生成功能：
1. 调用智谱 AI 图片生成 API
2. 发送 prompt、size、style 参数
3. 生成过程显示加载动画和提示文字
4. 生成成功后显示图片
5. 错误时显示友好提示
```

Image generation usually takes 10 to 30 seconds, so loading feedback is very important. Users need to know the app is generating, not frozen.

Third, implement prompt optimization:

```
实现提示词优化功能：
当用户点击"优化提示词"按钮时：
1. 把用户输入的简单描述发送给 AI
2. 让 AI 扩展成详细的图片生成提示词
3. 提示词要包含：主体、风格、光线、色彩、构图等细节
4. 把优化后的提示词填回输入框
```

This feature is extremely practical, because it helps users who don't know how to write prompts generate better images.

Fourth, add history logging:

```
实现历史记录功能：
1. 每次生成成功后，保存到 LocalStorage
2. 保存内容：提示词、图片 URL、生成时间
3. 左侧显示历史记录列表（缩略图 + 提示词）
4. 点击历史记录可以查看大图
5. 支持删除历史记录
```

Fifth, add download support:

```
实现图片下载功能：
点击下载按钮时，下载当前显示的图片。
文件名格式：ai-image-[时间戳].png
```



### Prompt Tips for Image Generation

The quality of generated images depends heavily on the prompt. A good prompt usually includes these elements: the subject (what to draw), the action or state (what it is doing), the environment/background (where it is), the style, the lighting, the color palette, and quality descriptors (such as HD / 4K).

For example, if you want to generate an image of a cat, you can describe it like this:

```markdown
一只可爱的橘猫，坐在窗台上看着外面的雨，温暖的室内光线，柔和的色调，细腻的毛发质感，景深效果，高清画质，4K。
```

This kind of description includes all the key elements, so the generated image quality will usually be better.

For style, you can use keywords to specify it. For photorealistic styles, use words like `photorealistic`, `realistic`, `detailed`; for cartoon styles, use `cartoon style`, `anime style`, `cute`; for oil painting styles, use `oil painting`, `artistic`, `impressionist`; for watercolor styles, use `watercolor`, `soft colors`; and for cyberpunk styles, use `cyberpunk`, `neon lights`, `futuristic`.

Quality descriptors are also important, such as `high quality`, `detailed`, `4K`, `8K`, `professional`, and `masterpiece`. These words can help the AI generate more refined images.

If you're not sure how to write prompts, you can let AI help you. For example, if you want to generate an image of a programmer coding in a café, you can tell the AI:

```
我想生成一张图片，内容是：一个程序员在咖啡厅写代码。请帮我把这个描述扩展成详细的图片生成提示词。
```

The AI will give you a detailed description covering the scene, lighting, color palette, composition, and more. For example:

```markdown
一位年轻的程序员坐在温馨的咖啡厅靠窗位置，专注地在笔记本电脑上写代码，桌上放着一杯热气腾腾的拿铁咖啡，温暖的下午阳光透过窗户洒在桌面上，背景是模糊的咖啡厅环境，柔和的光线，温暖的色调，电影感构图，景深效果，高清画质，专业摄影。
```

💡 If you're using an overseas AI image model, English prompts may work even better.



### Cost Control Suggestions

One thing to keep in mind is that image generation is much more expensive than text generation, so you need to control costs carefully. During development and testing, standard quality is enough—you don't need HD quality. Optimize the prompt before generating to avoid repeated trial and error wasting your quota. If your budget is limited, you can also consider cheaper alternatives.



### Extension Ideas

After finishing the basic version, you can continue expanding the app. For example, add image editing based on existing images; support batch generation to generate multiple images at once; add style presets so users can pick common styles with one click; implement image zooming to inspect details; or even add community sharing so users can share the images they've generated.



## 5. Project Practice - Speech Recognition App

Finally, let's build an AI application involving audio processing. Speech recognition can give your application voice input support and greatly improve the user experience. This project will help you learn how to process audio data and call speech recognition APIs.

This project needs to implement voice recording and recognition. The user clicks a button to start recording, clicks again to stop, and then converts the speech into text. It should support multiple languages, allow the recognition result to be edited, and save the results to a history log.

![](https://pic.yupi.icu/1/demoweb9.png)

The recording feature uses the browser's built-in MediaRecorder API, so no extra library is required. Speech recognition calls Zhipu AI's speech recognition capability—[visit the official site to get an API Key](https://bigmodel.cn/). The rest of the tech stack is similar to the earlier projects.



### Development Steps

1) Understand the Speech Recognition API

The first step in development is to understand the speech recognition API. Calling a speech recognition API is very straightforward: upload an audio file, specify the language (optional), and get back the recognized text.

2) Write a Requirements Document

Then write a requirements document `PRD.md`:

```markdown
# 语音识别应用 PRD

## 核心功能
1. 大大的录音按钮，点击开始录音，再点击停止
2. 录音时按钮变红色，有动画效果
3. 停止后显示"开始识别"按钮
4. 识别过程显示加载提示
5. 识别结果显示在下方，可以编辑
6. 保存识别历史

## 界面要求
- 简洁的单页面
- 中央大圆形录音按钮
- 识别结果区域
- 底部历史记录列表
```

3) Develop Through AI Conversation

Once the document is ready, you can start developing by talking with the AI.

First, implement recording:

```
请实现浏览器录音功能：
1. 使用 MediaRecorder API 录制音频
2. 需要请求麦克风权限
3. 点击按钮开始录音，再点击停止
4. 录音时按钮变红色，有脉冲动画
5. 停止后保存音频数据（Blob 格式）
```

This prompt explains what technology to use and what functionality to build. MediaRecorder API is a browser-provided recording interface, so no additional library installation is needed, which makes it very convenient.

Second, implement speech recognition:

```
实现语音识别功能：
1. 调用智谱 AI 语音识别 API
2. 上传录音的音频文件
3. 指定语言为中文
4. 显示识别结果
5. 错误时显示友好提示
```

Third, optimize the interface and experience:

```
优化界面和用户体验：
1. 录音按钮要大且醒目（直径 120px）
2. 识别结果区域要支持编辑
3. 添加复制按钮，方便复制识别结果
4. 识别过程显示加载动画和提示文字
5. 整体使用简洁现代的设计
```

Fourth, add history logging:

```
实现历史记录功能：
1. 每次识别成功后保存到 LocalStorage
2. 保存内容：识别文本、时间戳
3. 底部显示历史记录列表
4. 点击历史记录可以查看详情
5. 支持删除历史记录
```



### Development Tips

During development, there are several tips worth noting. First is microphone permission handling. The first time a user uses the feature, the browser will ask whether to allow microphone access. If the user denies it, show a friendly message such as: "Microphone permission is required for recording. Please allow microphone access in your browser settings," and provide a button to request permission again.

Second is audio format handling. The format recorded by MediaRecorder may be `webm`, and most speech recognition APIs support this format. If not, you can ask AI to help you convert the format.

Third is limiting recording duration. To avoid files becoming too large and recognition taking too long, you can limit recording length—for example, to a maximum of 60 seconds. Show a countdown during recording and stop automatically when the time is reached. You can also display the recording duration in real time so users know how long they have been recording.



### Extension Ideas

After completing the basic version, you can continue expanding its functionality. For example, add voice translation so recognized speech is automatically translated into other languages; support real-time recognition so speech is transcribed while the user is speaking; add keyword extraction to automatically extract important information; support multi-speaker conversation recognition and distinguish between different speakers; add subtitle generation to create subtitles for videos; or even integrate the feature into other apps, such as a chat assistant that supports voice input.



## Final Thoughts

Through these 4 AI application projects, you've already learned the basic workflow of AI application development: from a simple chat assistant, to a professional writing assistant, to a cool image generator, and finally to a practical speech recognition app. Each project helps you master a different AI capability.

The barrier to AI application development is already very low. You don't need to understand complicated machine learning algorithms—as long as you know how to call APIs and design good prompts, you can build really cool applications. If you want to learn more AI application development techniques and best practices, you can refer to the **Tips & Tricks** section of this tutorial.

After mastering AI application development, in the next article I'll take you on to more complex full-stack application development, where you'll learn how to handle the front end, back end, and database together. Let's keep moving forward!



## Recommended Resources

1) Yupi AI Navigation Website: [AI Resource Directory, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Paths, Programming Tutorials, Hands-on Projects, Job-Hunting Guide, Community Q&A](https://www.codefather.cn)

3) Programmer Interview Cheat Sheets: [High-Frequency Topics for Internships / Campus Hiring / Experienced Hiring, Real Company Interview Analysis](https://www.mianshiya.com)

4) Resume Tool for Programmers: [Professional Templates, Rich Example Sentences, Direct Access to Interviews](https://www.laoyujianli.com)

5) 1-on-1 Mock Interviews: [Essential for Landing Offers in Internships / Campus Hiring / Experienced Hiring](https://ai.mianshiya.com)