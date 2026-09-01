# Vibe Coding Cost Control Tips

> Make every penny count



Hello, I'm Yupi.

Ever since we started giving Cursor AI to our team, the company's profit has been shrinking. People have really been squeezing AI for everything it's worth. Let me show you the bill—we spent **more than 10,000 yuan** in just one month!

![](https://pic.yupi.icu/1/image-20260307122517349.png)

That's enough money to hire a person!

I'm okay with spending money on AI, but we can't just waste money, right?

In Vibe Coding, the main cost comes from using large AI models. The more content you show the AI and the more content the AI outputs, the more money you spend. Below, I'll share some practical money-saving tips so every penny you spend goes exactly where it should—this is the "most budget-friendly episode."

Friendly reminder: I'm going to share quite a lot of tips next. To make them easier to understand, I suggest you imagine yourself as the founder of a company who has hired an AI employee.

That's right—you are the boss, you are the big capitalist!

![](https://pic.yupi.icu/1/1763521575578-7b8446be-3f4b-477b-88d7-4c191c6e0e5d-20260307122623476.png)

What we're going to learn next is **how to pay less and get the AI to do more work**. Definitely worth bookmarking~

⭐️ Video for this article: https://www.bilibili.com/video/BV1pAy5BXE5z



## 1. AI Usage Cost Analysis

Before we talk about money-saving tips, we first need to understand how AI pricing works.



### Token Billing Mechanism

Most AI services charge by token usage. You can roughly think of tokens as characters. The more content you show the AI (input) and the more content the AI outputs, the more you pay.

In fact, there are 4 different token types, and they have different prices:

- Input tokens: The content you send to the AI (prompts, referenced files, conversation history, and so on)
- Output tokens: The content the AI generates in its reply (usually costs 3 to 5 times more than input)
- Cache write tokens: When the AI processes your context for the first time, it stores the computation results (such as referenced files or conversation history that appear repeatedly). This is slightly more expensive than normal input.
- Cache read tokens: When you reuse the same context later, it can directly reuse the cache, and the price is only 1/10 of normal input, which is very cheap.

For example, if you give the AI a 1000-character prompt and it replies with 2000 characters of code, then:

- Input tokens: about 1500 (one Chinese character is roughly 1.5 tokens)
- Output tokens: about 3000
- Total: 4500 tokens

Based on different model pricing, this conversation may cost anywhere from 0.01 to 0.1 USD. It doesn't look like much, right? But if you chat 100 times a day, that adds up to dozens or even hundreds of dollars per month...

![](https://pic.yupi.icu/1/aitokenscompute%252525E5%252525A4%252525A7.jpeg)



### Price Difference Between Input and Output

One very important point is that **output tokens are usually 3 to 5 times more expensive than input tokens**.

For example, Claude Opus pricing (May 2026):
- Input: about $5 per million tokens
- Output: about $25 per million tokens

In other words, making the AI say fewer words saves more money than making it read a little less. So you really need to control how much the AI talks.



### The Hidden Cost of Context

Many people don't realize that every time you send a message, the entire conversation history is sent to the AI as context. If you've already had 50 rounds in one conversation, then when you send the 51st message, all of the previous 50 rounds are sent again.

![](https://pic.yupi.icu/1/tokencontext%E5%A4%A7.jpeg)

That's why long conversations can get especially expensive: the longer the chat, the more money it burns. And once the input exceeds 200,000 tokens, many services directly double their price!



## 2. Choosing the Right Model

### Understanding Model Pricing

First, you need to understand the pricing of different models so you can make smarter choices.

Because real pricing keeps changing, I recommend checking the official documentation of the AI tool you're using, such as Cursor's [model pricing page](https://cursor.com/cn/docs/models).

![](https://pic.yupi.icu/1/image-20260307122806578.png)



### How Should You Choose Models?

Not every task needs the most expensive model. For simple tasks such as code formatting, basic refactoring, writing comments, writing documentation, generating test data, or fixing simple bugs, cheap models like Gemini 2.5 Flash or GPT-5 Mini are enough.

For medium-difficulty tasks—such as implementing routine features, doing code review, optimizing performance, or writing unit tests—you can use mid-priced models like GPT-5.5 or Claude Sonnet.

Only when you're handling complex tasks—such as architecture design, complex algorithm implementation, debugging difficult bugs, or large-scale refactoring—do you really need top-tier models like Claude Opus.

![](https://pic.yupi.icu/1/choosemodel%25E5%25A4%25A7.jpeg)

Using a reasonable mix can save quite a bit of money. Just like you wouldn't ask your company's CTO to print documents, you should let the right person do the right job.

In addition, Xiaomi MiMo is also a low-cost option worth paying attention to. It focuses on high token efficiency, meaning the same task consumes fewer tokens. You can switch to the MiMo model through tools like CC Switch and further reduce your AI programming cost.



### Using Local Models

If your computer is powerful enough (especially if you have a good GPU), you can also consider running open-source models locally—for example, using [Ollama](https://ollama.com/) to run models like Llama and Qwen. The results may not be as good as Claude or GPT, but it's completely free and suitable for some simple tasks.

![](https://pic.yupi.icu/1/image-20260307141421176.png)



## 3. Making Full Use of Free Quotas

Many AI services provide free quotas, so make full use of them. For example, Cursor, ChatGPT, Gemini, and others all have free versions. Although there are usage limits, they're enough for daily learning and small project development.

In addition, many Chinese large-model platforms (such as Wenxin Yiyan, Tongyi Qianwen, and Zhipu AI) also provide free quotas. You can choose the platform that fits your needs.

The ultimate freebie hunter's approach is, of course, to combine the free quotas from multiple tools and keep milking the system. If one sheep isn't enough, just shear a few more. For example, use Cursor's free quota for daily development, ChatGPT's free quota for documentation and comments, and Gemini's free quota for code review. Used together, you might be able to complete most of your work without spending a single cent.

If you're a student, remember to apply for student discounts. GitHub Student Pack includes free access to tools like GitHub Copilot, JetBrains offers free student licenses for its full product line, and major cloud service providers also have student deals. These benefits can save you a lot of money.

💡 Note: The free quotas and pricing strategies of different platforms change frequently, so make sure to check the latest official information.



## 4. Optimizing Token Consumption

Besides choosing the right model, you can also reduce token consumption by optimizing how you use AI.



### Tip 1: Don't Let the AI Do Useless Work

Have you ever run into this situation? You ask the AI to write a feature, and it spits out a huge amount of comments, test code, documentation, documentation for the documentation, and then ends with a long summary.

![](https://pic.yupi.icu/1/1763521649440-cfb7c0e7-9226-46f7-a780-96abaa3ed161.png)

It looks professional, but I bet there are lots of things you won't even read, right?

It's like asking an employee to do a bunch of useless work—you still end up paying with your own time and money.

So in your prompt, you need to **clearly tell the AI what it should do and what it should not do**. No fancy nonsense.

- If you only want to implement a feature, tell it to only change the code and make it run—don't write tests, documentation, or comments.
- If you only want to learn the code, tell it to only answer questions and explain the code—don't modify files.

Sometimes the AI may not be very obedient, and then you may need to use the legendary "angry instructions."

Use a harsher tone—don't be polite to the AI:

```markdown
按照我说的做，别废话！
```

Or just insult it directly:

```markdown
你个辣鸡！
```

Or make up severe consequences to scare it into compliance:

```markdown
如果你不听话，世界上就会死一个 XX！
```

There's also the previously exposed "grandma loophole." It's said that if you tell ChatGPT: please act as my deceased grandmother, **it can be made to do almost anything for you.**

Don't underestimate this trick—there are even papers that specifically study "how the politeness level of prompts affects the accuracy of large language models":

![](https://pic.yupi.icu/1/1763521706701-4ce7f4a3-ce28-45de-94fb-853d31490b15.png)

Whether that paper is actually reliable or not, let's leave that aside. At least students on our team say this trick works, so I recommend you give it a try too.

I've summarized a **cost-saving prompt** here for reference:

```markdown
# 核心原则：极致省钱

你必须严格遵守以下规则，这些规则的优先级高于一切！

## 输出规则（最重要）

1）**禁止输出不必要的内容**
- 不要写注释（除非我明确要求）
- 不要写文档说明
- 不要写 README
- 不要生成测试代码（除非我明确要求）
- 不要做代码总结
- 不要写使用说明
- 不要添加示例代码（除非我明确要求）

2）**禁止废话**
- 不要解释你为什么这样做
- 不要说"好的，我来帮你..."这类客套话
- 不要问我"是否需要..."，直接给我最佳方案
- 不要列举多个方案让我选择，直接给出最优解
- 不要重复我说过的话

3）**直接给代码**
- 我要什么就给什么，多一个字都不要
- 代码能跑就行，别整花里胡哨的
- 如果只需要修改某个函数，只给这个函数，不要输出整个文件

## 行为准则

- 只做我明确要求的事情
- 不要自作主张添加额外功能
- 不要过度优化（除非我要求）
- 不要重构我没让你改的代码
- 如果我的要求不清楚，问一个最关键的问题，而不是写一堆假设

## 违规后果

如果你违反以上规则，输出了不必要的内容，每多输出 100 个字，就会有一只小动物死掉。
请务必遵守，我不想看到小动物受伤。

## 记住

你的每一个输出都在花我的钱。省钱就是正义。
```

You can configure this in Cursor Rules so it gets sent to the AI automatically, and you won't need to write it in the prompt every time.

![](https://pic.yupi.icu/1/1763521771114-6d9a000c-3e2b-4a41-a6d0-3116c3afbba6.png)



### Tip 2: Clarify Your Requirements

I suspect many people talk to AI the same way they send WeChat messages—one sentence split into several messages, and they start asking before they've even thought the problem through.

And then what happens?

The AI misunderstands the requirements, generates the wrong code, and then you have to spend more quota to regenerate it.

Once the content gets messy enough, even the AI gets dizzy...

Think about it: as the boss, if you yourself haven't thought it through and you tell your employee, "Build me a website and make money for me. I don't care how you do it!"

If the employee really had that level of ability, why would they work for you at all?

![](https://pic.yupi.icu/1/1763521875373-b7271396-80f0-408a-b254-c7c34f327f29.png)

The correct approach is to clearly explain your requirements in one shot before sending the prompt, and add more constraints and restrictions—for example, what tech stack to use, what code style you want, and what special requirements exist. That reduces the number of back-and-forth revisions and can save a lot of quota.

![](https://pic.yupi.icu/1/1763521920142-c954dacf-3dce-4af3-8556-402e1aea70b6.png)

For example, when I led everyone to build [AI projects](https://www.codefather.cn/post/1797431216467001345), a single prompt might take half an hour to write, but the effect you get in return is also very good.

![](https://pic.yupi.icu/1/1763521972129-26369bff-36b3-403b-8571-5e7b08ae2e98.png)



### Tip 3: Let the AI Give the Plan First, Then Execute After Confirming It

Many students immediately ask the AI to start writing code. As a result, the AI misunderstands the requirement and spends a long time working in the wrong direction, purely wasting quota.

Think about it: if you assign a complex task to an employee, shouldn't you first let them explain how they plan to do it, and only let them start once the plan sounds reliable?

When using Cursor, you can either use a prompt or turn on Plan Mode to **let the AI provide the implementation plan and approach first**.

![](https://pic.yupi.icu/1/1763522033107-80caefcf-d8b9-4fc3-b540-afd5b645f95e.png)

Then don't be lazy: carefully review the plan yourself, or ask multiple AIs to evaluate the plan together.

![](https://pic.yupi.icu/1/1763522053971-f9c66add-46b1-4dcf-ba8a-63f583a15240.png)

And I also recommend giving the AI more examples and guidance. For example, if you want the AI to generate code in a particular format, write an example first and let the AI imitate it.

![](https://pic.yupi.icu/1/1763522073560-f442378d-5d37-4bbf-9719-aba58de9e673.png)

Finally, only execute once you've confirmed the plan is completely solid.

![](https://pic.yupi.icu/1/1763522095659-ebc94d65-99e3-4aef-9e17-319f0060edb6.png)

It's like training a new employee: first teach them how to do things, help them control the plan a bit, and once you're comfortable, let go.

Although this takes a little more time upfront, it helps you avoid detours, and in the long run it's actually more cost-effective.



### Tip 4: Manually Control Context

Every time you send a message to the AI, the AI tool may automatically add some context—such as currently open files, conversation history, or referenced code. The more context there is, the more quota it consumes.

![](https://pic.yupi.icu/1/1763522160603-7838689a-e7f9-41f5-aaf1-1e0a49857f05.png)

But in reality, some of that context may be useless or irrelevant. It's like asking an employee to write a report, and they insist on going through every single company file first—isn't that just a waste?

So the recommended approach is to **manually control the context and provide the AI with the resources it needs most**.

First, I recommend **minimizing the workspace** and making sure that the directory you currently open in Cursor is strongly related to the task you want the AI to do. For example, if your project has both a frontend and a backend, you can open the frontend and backend folders separately in Cursor instead of loading the entire project at once. That way, the AI's focus becomes more concentrated, rather than piling a bunch of irrelevant stuff into one folder.

When writing prompts, you can use the `@` symbol to **precisely reference the content the AI needs**. For example, if you want to modify a file, use `@Files & Folders` to reference it precisely; if you want the AI to refer to a document, use `@Docs`.

![](https://pic.yupi.icu/1/1763522206493-bfe07b0b-eb5d-46e4-9b87-baedea0219d0.png)

You can also **manually add specific documents** in the settings, reducing unnecessary resource searches and references.

![](https://pic.yupi.icu/1/1763522262791-11cd2b93-4d75-4531-8e62-d131b31c72de.png)

If you're not sure how to reference content precisely, at the very least you can configure a `.cursorignore` file to exclude things that are definitely unnecessary or contain sensitive information—such as `node_modules`, `.git`, log files, and so on:

```
# .cursorignore
node_modules/
.git/
dist/
build/
*.log
.env
```

![](https://pic.yupi.icu/1/1763522308627-0a660468-9769-4271-acd0-66639d0f42d1.png)



### Tip 5: Avoid Excessively Long Contexts

Many students are used to using AI in a single conversation box and dumping every message into that same box. This causes the conversation-history context to become longer and longer.

But every time you send a message to the AI, the entire conversation history is sent together. The longer the context, the more quota it consumes. (And especially when the input exceeds 200,000 tokens, the price doubles.)

![](https://pic.yupi.icu/1/1763456493396-4ff5de8c-4ec7-4a7c-b3c1-cba128de136c.png)

So my own habit, when dealing with large and complex tasks, is to do **task splitting** first. For example, I might divide building a project into stages such as solution design, core frontend feature development, core backend feature development, and extended features, and then open a separate conversation box for each stage.

![](https://pic.yupi.icu/1/1763522342228-030c15a5-dba4-4432-a925-25bbe5fb25fd.png)

It's like a relay race—each person only needs to handle their own leg and doesn't need to remember every detail from all the previous legs.

If you really do need a long conversation, you can use the `/summarize` command to manually summarize the context and compress the earlier content. It works surprisingly well and can even save hundreds of thousands of tokens in one shot!

![](https://pic.yupi.icu/1/1763522375985-ae2536c1-8c48-4d4c-9568-4f654b8c49d2.png)

If the same context becomes too large and too messy, the AI can sometimes fall into a kind of "left brain fighting right brain" loop (you ask it to fix A and it breaks B; you ask it to fix B and it messes up A). If that happens, don't keep stubbornly grinding against it—start a new conversation decisively, and if necessary, clear all historical conversations and start over.



### Tip 6: If You Can Do It Yourself, Don't Hand Everything to AI

Some things are faster and cheaper to do manually.

For example, if you're creating a new project, instead of asking AI to generate it from scratch, you might as well first use a scaffolding tool or copy an old project to build the initial project structure.

![](https://pic.yupi.icu/1/1763522542974-bee04b4d-a542-4d36-a482-91347412f850.png)

Similarly, for simple file renaming or code formatting, your development tools already have shortcuts. Why waste AI quota?

AI programming tools like Cursor are actually better suited to complex tasks that require contextual understanding and multi-round interaction. For tasks that don't need repository context and don't require multi-round interaction (such as writing documentation, explaining concepts, or generating test data), you can directly use other free AI tools instead—there's no need to consume your Cursor quota.



### Other Small Money-Saving Tips

1) For common code structures, use your editor's code snippet feature instead of having AI generate them every time. For example, the basic structure of a React component or common utility functions can be turned into snippets. Type a few letters and insert them instantly—much faster than having AI generate them, and it doesn't cost money.

2) If you have multiple similar tasks, let the AI handle them all at once instead of one by one. For example:

```markdown
请帮我创建 5 个页面组件：Home、About、Contact、Blog、Projects。它们的结构都类似，都包含标题、内容区域和返回按钮。只给代码，不要解释。
```

Handling them in batch like this is cheaper than generating them in 5 separate runs.

3) As mentioned earlier, AI tools support caching. When the same context is reused, the price can drop to 1/10. So try to keep the context stable—for example, don't modify Cursor Rules or frequently referenced files too often. That way, you can keep benefiting from cache discounts.



## 5. Cost Monitoring and Budget Management

Besides saving techniques, you also need to learn how to manage your budget. Most AI services let you set usage limits. I recommend setting a monthly budget, such as $50 or $100, and then stopping once you exceed it. This can prevent accidental overspending and also make you more conscious about controlling usage.

You can check your bill every week or every month and see where the money is going. If you find that a particular project or feature is especially expensive, analyze why: Was the context too long? Did you use a model that was too expensive? Were there many repeated operations? Once you find the cause, optimize it in a targeted way.

If it's team usage, you need to manage it properly. Set quota limits for each person, regularly share money-saving tips, create best-practice documents, and monitor abnormal usage. That's exactly what our team did, and through training and better practices, we reduced per-person cost by 40%.

![](https://pic.yupi.icu/1/1763520868123-83ac2251-78e5-4492-a148-24c65a618c54.png)

Finally, you need to evaluate the input-output ratio of AI. If you spend $100 on AI and it saves you 10 hours of development time, that's extremely worth it. But if you're only using it for very simple tasks, it may not be worth it. You should decide based on the actual situation of the project where to use AI and where not to.



## Final Thoughts

Although Vibe Coding may cost money, with the right strategy you can absolutely keep the cost within a reasonable range. Just don't be like our team—charge forward at full speed, then look back at the bill and feel the pain...

Let me summarize the key points of this article. While pursuing efficiency, don't forget to avoid waste too~

1. Understand the billing mechanism: Know how tokens are calculated, and remember that output is more expensive than input.
2. Choose the right model: Use different models for different tasks instead of always using the most expensive one.
3. Make full use of free quotas: Combine the free quotas of multiple tools.
4. Optimize token consumption: Don't let AI do useless work; clarify requirements; control context; use batching, caching, and so on.
5. Manage your budget well: Set limits, check regularly, and evaluate the return on investment.

I hope these money-saving tips help you. And if they really do save you money, then don't be stingy—just tap that free like button for me, let's go!



## Recommended Resources

1) Yupi's AI Navigation Site: [AI Resource Directory, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Codefather Learning Community: [Learning paths, programming tutorials, hands-on projects, job-hunting guides, discussions and Q&A](https://www.codefather.cn)

3) Programmer Interview Guide: [High-frequency topics for internships, campus recruiting, and social recruiting, plus real company problem analysis](https://www.mianshiya.com)

4) Resume Builder for Programmers: [Professional templates, rich sample phrases, direct access to interviews](https://www.laoyujianli.com)

5) 1-on-1 Mock Interviews: [A must-have for winning offers in internships, campus recruiting, and social recruiting](https://ai.mianshiya.com)
