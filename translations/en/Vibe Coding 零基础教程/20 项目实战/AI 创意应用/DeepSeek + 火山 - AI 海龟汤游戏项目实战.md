# DeepSeek + 火山 - AI Turtle Soup Game Project Practice

This project is an AI Turtle Soup game website where you play Turtle Soup through conversations with AI.

It’s a fast Vibe Coding project. From requirement analysis to the finished product, it took just over 2 hours. The frontend was generated with AI, while the backend code that calls the AI API was written by hand. The focus is on learning a fast development workflow, Prompt engineering, and how to add AI capabilities to a program.

Project code is open source for free: https://github.com/liyupi/yuhaigui-ai-game

Project text + video tutorial: https://www.codefather.cn/course/1898973113527894017

Below is a brief introduction to the finished project and a demo of the results.



---



Hello everyone, I’m Yupi. Now that we’re in the 全民 AI era, as programmers we should be thinking about how to squeeze as much value as possible out of AI and really put it to work. A few days ago, on a whim, I spent a little over 2 hours on a livestream starting from requirement analysis and building an AI Turtle Soup game project with everyone.

[I’ve also open-sourced the code for everyone](https://github.com/liyupi/yuhaigui-ai-game) to play with and learn from:

![](https://pic.yupi.icu/1/image-20250311173906981.png)

Below is a quick introduction to the project~



## AI Turtle Soup Project

This is an AI-native project you can learn in just a few hours. By building an AI Turtle Soup game website, it helps everyone quickly practice the development workflow of AI projects and keep up with the cutting edge of the times.

Some of you may never have heard of Turtle Soup. It’s a party game suitable for all ages. It consists of the “surface” of the story and the “truth” behind it. The host tells a story premise, and players keep asking questions to gradually uncover and reconstruct the real truth.

For example: a man invited his friends to a birthday party. After he blew out the candles, he killed everyone there. Why?

![](https://pic.yupi.icu/1/image-20250311174206256.png)

You can let AI replace the traditional Turtle Soup host. Players only need to chat with AI to play the game on their own.

The image below shows the website generated with AI. Of course, it could still be polished further to make it even prettier~

![](https://pic.yupi.icu/1/1741583369760-09fd9c45-2093-4ab0-8148-ec83ad61fc6b.png)



Through this small project, you can actually learn quite a lot:

1. Learn a standard enterprise project development workflow: requirement analysis => solution design => backend development + frontend development => testing => deployment (optional)
2. Learn how to quickly initialize frontend and backend projects
3. Learn how to integrate AI large models into programs
4. Learn how to encapsulate your own AI utility classes
5. Learn how to optimize Prompts
6. Learn how to maintain conversation context and pass it to AI
7. Learn how to use AI to complete code
8. Learn how to build a frontend website entirely with AI



![接入 AI 并调试优化 Prompt 提示词](https://pic.yupi.icu/1/1741248993412-8e92e068-5192-46ad-81bc-bf046de4c005.png)



### Tech Stack

#### Frontend

- Vue 3: suitable for quickly building single-page applications
- Ant Design Vue: a mainstream component library compatible with both desktop and responsive mobile layouts
- Vue Router: frontend routing component
- Axios: a mainstream request library

#### Backend

- Java + Spring Boot framework
- MySQL database
- MyBatis + MyBatis Plus framework
- Hutool utility library
- Swagger + Knife4j for API documentation
- AI large model integration, using the currently very popular DeepSeek



![快速初始后端 + 运行接口文档调试接口](https://pic.yupi.icu/1/1741247574417-a53861c4-35c6-488d-90a1-aa2cea31cee0.png)



### Business Flow

1. The player enters the page and clicks **Start Game** to enter the chat room page
2. When entering the chat room page, AI immediately sends a greeting message (the story premise)
3. After that, the user can chat with the AI host
4. The user can end the game actively, or AI can end it actively
5. The user can view past conversation records at any time

The flow is shown below. This diagram was also generated with AI:

![](https://pic.yupi.icu/1/image-20250310135157204.png)



## Final Thoughts

The full livestream replay of this project has already been released in episodes on the [Programming Navigation website](https://mp.weixin.qq.com/s/jHy2EjdOZPJDN_Lrs7qAUA). Besides the project above, I’ve recently also added quite a few AI features to Programming Navigation’s [intelligent interview prep platform project](https://mp.weixin.qq.com/s/jHy2EjdOZPJDN_Lrs7qAUA), such as AI-generated questions and solutions, AI mock interviews, and more. These can all help you add highlights to your resume and improve your job-hunting competitiveness.

![AI 模拟面试](https://pic.yupi.icu/1/image-20250311175611501.png)

Programming Navigation also has [more than 20 project tutorials](https://www.codefather.cn/post/1797431216467001345) that I’ve built with everyone, taking you hands-on through full-stack project development from 0 to 1. Many people have landed great offers through my projects, and the feedback has been amazing~

![](https://pic.yupi.icu/1/de62f4cc-32cb-4814-aca7-03c232d0e2d2.png)




## Recommended Resources

1) Yupi AI Navigation Website: [Comprehensive AI Resources, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Paths, Programming Tutorials, Practical Projects, Job Hunting Guide, Q&A](https://www.codefather.cn)

3) Programmer Interview Cheatsheet: [High-Frequency Topics for Internships / Campus Hiring / Experienced Hiring, Plus Real Interview Question Analysis](https://www.mianshiya.com)

4) Programmer Resume Writing Tool: [Professional Templates, Rich Example Sentences, Direct to Interview](https://www.laoyujianli.com)

5) 1-on-1 Mock Interview: [A Must-Have for Internship / Campus Hiring / Experienced Hiring Interviews to Land Offers](https://ai.mianshiya.com)
