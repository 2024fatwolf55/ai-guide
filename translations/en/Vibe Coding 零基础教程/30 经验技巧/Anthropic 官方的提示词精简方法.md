# Anthropic’s Official Method for Streamlining Prompts

> The official team cut 80% of Claude Code’s system prompts, and the benchmark score didn’t even drop

Hello everyone, I’m Yupi.

Some time ago, Anthropic published a post on its official blog saying that for the two new models, Claude Opus 5 and Fable 5, they removed **more than 80%** of Claude Code’s system prompts, yet its performance on coding evaluations did not decline.

![](https://pic.yupi.icu/1/1785753504253-ca87d006-a35e-475f-bdb4-7a4b241e3856.png)

My first reaction was: so all those prompts I spent so much effort writing before were for nothing?

But after thinking about it carefully, it also felt perfectly reasonable. A lot of the rules we used to write were essentially there to compensate for the weaker judgment of older models. Once the model’s capabilities catch up, those rules can actually become constraints instead.

It’s like teaching a beginner how to drive. You need to tell them to stop at red lights, go at green lights, and use the turn signal before turning. But you wouldn’t repeat those things to a veteran driver with ten years of experience, because those rules are already internalized. Saying them again would only distract them.

In this article, I’ll show you exactly how Anthropic made those cuts, explain the principles behind them, compare long and short prompts in a practical test so you can feel the difference, and finally talk about how we should simplify our own prompts.



## Why Prompts Need Subtraction

In Anthropic’s blog series on context engineering, they introduced two concepts that explain this very well.

The first is called **Attention Budget**. AI models are like people: working memory is limited. The more contextual rules you give them, the more attention they have to spend balancing those rules, leaving less attention for the actual work.

The second is the **law of diminishing returns in context**. The more tokens there are in the context, the worse the model becomes at recalling information precisely. It’s like handing someone 100 pages of documents at once and expecting them to remember every detail from every page. That’s simply unrealistic.

![](https://pic.yupi.icu/1/01_%E6%B3%A8%E6%84%8F%E5%8A%9B%E9%A2%84%E7%AE%97%E4%B8%8E%E8%BE%B9%E9%99%85%E9%80%92%E5%87%8F%E6%95%88%E5%BA%94_compressed_v2.png)

You can probably see now why Anthropic decided to cut so many system prompts.

So what exactly did they change?



## What Anthropic Changed Specifically

The official blog summarized several key shifts. I’ll focus on the ones I think are most valuable.



### 1. From Hardcoded Rules to Letting the Model Judge for Itself

In the early days, to prevent Claude from deleting code by mistake or adding comments everywhere, the team wrote very rigid rules into the system prompt, like this:

```markdown
默认不写注释。永远不要写多行文档字符串或多行注释块，最多一行简短注释。除非用户要求，否则不要创建规划、决策或分析文档。
```

This kind of one-size-fits-all rule is obviously not flexible enough. Some complex code really does need multi-line comments, and some users also have their own documentation preferences.

But back then, there was no better option. Older models didn’t have strong enough judgment, so without those constraints they were more likely to go off the rails. The team had to accept that tradeoff.

With the new generation of models, that long rule was simplified into a single sentence:

```markdown
写出来的代码要像周围的代码，匹配它的注释密度、命名方式和惯用法。
```

This way, the model adapts automatically to the style of the existing codebase instead of having its choices locked down by upfront rules.

![](https://pic.yupi.icu/1/02_%E4%BB%8E%E5%AE%9A%E6%AD%BB%E8%A7%84%E5%88%99%E5%88%B0%E8%AE%A9%E6%A8%A1%E5%9E%8B%E8%87%AA%E5%B7%B1%E5%88%A4%E6%96%AD_compressed_v1.png)



### 2. From Giving Examples to Designing Better Interfaces

There used to be a classic prompt technique called few-shot prompting: give AI examples. For instance, if AI didn’t know how to call a certain tool, you could show it three examples.

But Anthropic found that with newer models, examples can actually limit the model’s room to explore. The new models often understand more than the examples you provide, so the examples end up boxing them in.

Their suggestion is that instead of writing a bunch of examples to teach AI how to use a tool, it’s better to make the tool itself clearer to use.

They used the Todo tool in Claude Code as an example. This tool has three statuses: pending, in progress, and completed, and the parameter names are `pending`, `in_progress`, and `completed`. AI can understand what those mean at a glance, so there’s no need to teach it with extra examples.

A well-designed interface explains its own usage. Only badly designed interfaces need a thick instruction manual.



### 3. From Stuffing Everything In to Loading on Demand

Previously, Claude Code’s system prompt included a lot of detailed guidance about code review, verification, and similar tasks. Those instructions weren’t needed every time, but they were important when they were needed, so everything got stuffed in at once.

Now Anthropic has split that content into separate Skills packages that the model loads only when necessary. Even some tool definitions now follow a “lazy loading” pattern: the model fetches the full tool description through ToolSearch only when it needs to use the tool, so the context stays uncluttered the rest of the time.

This strategy is called **Progressive Disclosure**. If you’ve read the article *Agent Skills: A General AI Skill Library* in the “Tool Practice” section of this tutorial’s programming tools module, the term should already be familiar.

![](https://pic.yupi.icu/1/03_%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8A%AB%E9%9C%B2%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v3.png)

This idea also applies to the `CLAUDE.md` and Skills files we write ourselves. A lot of people like to turn `CLAUDE.md` into an encyclopedia packed with every possible detail, thinking that if they don’t write everything down, the model won’t find it.

But Anthropic recommends splitting the content into multiple files arranged in a tree structure. It’s like organizing your computer files: you wouldn’t pile every document onto your desktop. You’d sort them into folders by category and open what you need when you need it.



### 4. From Manual Memory to Automatic Memory

In the past, users had to manually press the `#` shortcut to save important information into `CLAUDE.md`. Now Claude automatically saves memories related to your work.

That also changes the role of `CLAUDE.md`. Anthropic recommends keeping it lightweight and focusing on the project’s “gotchas” and special conventions that the model cannot infer just by reading the code. Information like the directory structure or dependency list can already be read from the repository, so there’s no need to write it down manually anymore.

![](https://pic.yupi.icu/1/04_%E4%BB%8E%E6%89%8B%E5%8A%A8%E8%AE%B0%E5%BF%86%E5%88%B0%E8%87%AA%E5%8A%A8%E8%AE%B0%E5%BF%86_compressed_v2.png)



### 5. Reducing Conflicting Instructions

Anthropic also found an interesting issue when reviewing conversation logs from its own team using Claude Code.

In the same request, the system prompt might say “add documentation when appropriate,” while a Skill might also say “do not add comments.” Those two instructions conflict with each other.

Although the model can usually guess the user’s real intent from context, it still has to spend extra effort resolving those conflicts, which wastes attention budget for no reason.

So they removed redundant rules, and naturally there were far fewer contradictions of this kind.

![](https://pic.yupi.icu/1/05_%E7%9F%9B%E7%9B%BE%E6%8C%87%E4%BB%A4%E8%AE%A9%E6%A8%A1%E5%9E%8B%E5%9B%B0%E6%83%91_compressed_v3.png)



## A Practical Comparison: Long Prompts vs. Short Prompts

That covers the theory. To get a more intuitive feel for how new models perform with short prompts, I ran a practical comparison test.

I used Cursor + Claude Opus 5. The task was to have AI recreate a web version of Cursor, using two completely different prompt styles.

The first was a long, rule-heavy prompt packed with specific technical requirements and development steps:

![](https://pic.yupi.icu/1/1785921294571-9f9acde0-232f-4571-8f39-8f8c8f1a464f.png)

The second was a short prompt, just five lines long, only stating what to build and how to do the research:

```plain
基于 VS Code 开源生态做一个类似 Cursor 的 Web AI 编程工具，
支持 Editor Window 和 Agents Window。
先用 Firecrawl 搜 Cursor 3 的产品设计，
再用 Context7 查 monaco-vscode-api 的 Web 集成方案，
调研完先出技术方案，确认后再写代码。
```

Interestingly, the two prompts already behaved differently before any code was written.

During the research and planning phase, the short-prompt version proactively entered Plan mode and created a complete Todo list before starting work. The long-prompt version, on the other hand, did not enter Plan mode and started coding immediately after receiving the instruction.

![短提示词规划后的 Todo 列表](https://pic.yupi.icu/1/1785908352580-d2cafcaf-d694-40a9-98e7-3ea556571265.png)

In terms of code volume, the short-prompt version produced 12,984 lines of code in total, while the long-prompt version produced only 8,384 lines, nearly one-third less.

Our normal intuition might be that the longer the prompt and the more information it contains, the more code should be generated. But the result was exactly the opposite, which shows that with short prompts, AI was actually more willing to explore and generate freely.

Looking at the final result, the code generated from the short prompt ran successfully on the first try and was quite feature-complete.

It could switch normally between Edit and Agent mode windows, the directory tree loaded correctly, file CRUD worked, syntax highlighting and autocomplete were present, and even git features were implemented. On top of that, it supported theme switching, the terminal worked properly, search and keyboard shortcuts were all there, and most importantly, Agent mode could successfully connect to a model to generate code.

![短提示词版本](https://pic.yupi.icu/1/1785913712132-b278c6d8-521a-4d60-9a64-5cb90fef59a0.png)

The long-prompt result, unfortunately, was a bit of a disaster. I’ll just leave a screenshot here so you can judge the gap for yourself.

![长提示词版本](https://pic.yupi.icu/1/1785942480484-bdb66780-bc13-4d2c-8da3-dc88a18aaa55.png)

Thanks to the intelligence of Opus 5, both web versions of Cursor could successfully call an AI Agent to generate code. I connected both of them to the DeepSeek API and had each one write a Snake game using the DeepSeek V4 Flash model. The generation process was very smooth.

The Cursor built with the short prompt displayed a chain of thought and showed which tools were being called before generating code, making the whole interaction feel more complete.

![](https://pic.yupi.icu/1/1785981173449-df6ee5ce-64aa-456c-87cf-dea06f4dac33.png)

The Cursor built with the long prompt just started coding directly, without showing its chain of thought.

![](https://pic.yupi.icu/1/1785981359513-9ece52c4-c252-406f-be73-08ca1f401ec9.png)

In the end, the Snake games generated by both versions ran normally. AI has progressed to the point where I can casually use an AI coding tool to build an AI coding tool, and then let that AI coding tool do AI coding again.

![](https://pic.yupi.icu/1/1785913338340-fa358bbe-5512-4ba6-b2b3-d6366573c3f3.png)

At this point, the conclusion of the test was already obvious. The Cursor built with the short prompt clearly outperformed the long-prompt version in feature completeness, code quality, and first-pass success rate.

The core reason is that the long prompt boxed the model in. It only dared to act within the boundaries you drew for it. The short prompt gave the model enough room to explore, so based on its own understanding of what Cursor as a product should be, it proactively filled in many features it believed should exist.



## How We Should Simplify Our Own Prompts

In the past, model capabilities were not strong enough, and their understanding of many products and technologies was still fuzzy, so you had to handhold them through every detail. Now that new models have richer training data, stronger reasoning ability, and tools like MCP and Skills that give them more freedom to explore, those repetitive rules have become a burden instead. They waste tokens, consume the model’s attention while it works, and can easily conflict with rules from other Skills.

So how should we decide whether a certain prompt is worth writing at all?

This is how I judge it: **if something is common sense naturally implied by the task, you don’t need to write it down.** For example, if you ask AI to build a REST API, you don’t need to remind it to handle errors or return JSON. The model already knows that.

**If something is a special requirement of the task and differs from standard practice, then you do need to tell the model explicitly.** For example, if your project requires all APIs to use snake_case naming or all error codes to follow an internal standard, those are the kinds of rules worth writing down.

From another angle, your code repository itself is already a great prompt. The project structure, coding style, and test cases are all things the model can read and understand on its own. What you need to do is design the project architecture well, not turn your rules into a miniature essay.



## Automatically Optimize with the `/doctor` Command

To help developers keep up with this shift, Claude Code also includes a built-in `/doctor` command (you can also use `/checkup`) that automatically scans configuration files such as your Skills and `CLAUDE.md`, and helps detect what is redundant and what can be simplified.

![](https://pic.yupi.icu/1/1785830100705-ba0f3f43-ba78-43e0-bf59-5dabcf2f2c61.png)

Specifically, it does things like:

- Check whether `CLAUDE.md` contains information the model can already read from the repository, such as the directory structure or dependency list, and suggest removing it
- Find unused Skills and MCP services
- Detect duplicate or conflicting content between local and repository `CLAUDE.md` files
- Suggest moving content that doesn’t need to be loaded every time into Skills that can be loaded on demand

And it shows you a report before making any changes. It only executes after you confirm, so you don’t need to worry about it messing up your configuration.

I tested it on one of my own projects. It helped me optimize part of the configuration, but it didn’t make major changes to `CLAUDE.md`, which suggests the rules in that project are still in pretty healthy shape.

![](https://pic.yupi.icu/1/1785830217113-f4cf3ca0-4d3b-42f7-9dae-a0d8f590bc5b.png)



## Final Thoughts

The AI coding world is changing incredibly fast. Just a few months ago, I was still thinking about how to make prompts more and more perfect, and I felt that the more detailed the project rules were, the more accurately AI would follow the intended direction. But now the official conclusion is that many of those carefully polished rules were actually constraints all along.

At the end of the official blog, Anthropic summed it up with a sentence I think is especially brilliant: **find the smallest, highest-signal set of tokens that maximizes the outcome you want.**

From now on, when writing prompts, less really is more. Less is More. A lot of your prompts genuinely can be thrown away.

Of course, simplifying doesn’t mean writing nothing at all. Clearly describing your requirements and goals is still the most important part. You just no longer need to specify every single step in exhaustive detail. If you want to learn more about how to describe requirements clearly, you can continue reading *Vibe Coding Conversation Engineering Techniques* and *Use grill-me to Let AI Grill Your Requirements* in this section.
