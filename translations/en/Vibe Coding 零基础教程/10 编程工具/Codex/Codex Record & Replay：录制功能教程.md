# Codex Record & Replay: Feature Tutorial

> Demonstrate an operation to AI once, and it learns it forever

Hello everyone, I’m programmer Yupi.

Recently, Codex launched a new feature called **Record & Replay**.

A lot of AI bloggers have been hyping this feature to the skies, and I was honestly getting pretty itchy to try it myself. My expectations were sky-high too.

![](https://pic.yupi.icu/1/image-20260624182546406.png)

In this article, I’ll take everyone through this new feature, then talk about when it’s useful and how it works under the hood.



## What Is Record & Replay Good For?

In the past, if you wanted AI to do something for you, you had to write a prompt and clearly describe each step.

If there are only a few steps, that’s fine. But if the process is more complex, writing the prompt takes a lot of time, and you’ll almost always miss some details.

The idea behind Record & Replay is this: first turn on **recording**, then perform the workflow normally on your computer. Codex uses Computer Use to analyze the recording and automatically distill your actions into a reusable Skill. After that, you can use that Skill to **replay** the whole process.

For example, Codex officially demonstrated using this feature to automate video upload and publishing:

![](https://pic.yupi.icu/1/image-20260624183321530.png)

It’s kind of like this: if I want to teach my kid how to assemble a building block set, it may be hard to explain it clearly in words, so I just build it once in front of them and let them watch. Then they learn it.

Unfortunately, I don’t have my own kid, so I can only raise Codex as a cyber child...

Let’s try it in practice.



## Record & Replay in Practice

One thing to note before starting: this feature currently only supports macOS. Windows users can’t use it yet. Also, you need to update the Codex App to the latest version and install the Computer Use plugin in advance.

I previously wrote a [beginner-friendly Codex desktop APP tutorial](https://mp.weixin.qq.com/s/Zlkom9qPhTxnW4WcroCxmg) covering everything from installation to hands-on usage, so if you’re not familiar with it yet, go read that first.

First, install the Record & Replay plugin:

![](https://pic.yupi.icu/1/image-20260624180222466.png)

Now that the preparation is done, let me record one and try it out.

What repetitive thing do I often do in daily work?

Got it. When making videos, I often need to find BGM tracks that can be downloaded and used directly. Every time, I manually open NetEase Cloud Music, search by mood or genre, download the file, and then check whether the format is usable.

Perfect. Let’s use that scenario as the test case and teach Codex how to download FLAC-format music of a specified style from NetEase Cloud Music.



### Step 1: Enter the Prompt

Go into the Record & Replay plugin page and click “Try in chat”:

![](https://pic.yupi.icu/1/image-20260624180346459.png)

Codex automatically jumps to a new chat page, and the input box is already pre-filled with the prompt: “Record my workflow and turn it into a reusable skill.”

I added one more line under it describing my own need: I want to automatically download specific music in FLAC format.

![](https://pic.yupi.icu/1/image-20260624180704842.png)

Then submit it.



### Step 2: Demonstrate the Operation

After AI reads the task, it will request screen recording permission. Once you approve it, you can begin demonstrating.

![](https://pic.yupi.icu/1/image-20260624181052771.png)

During recording, Codex observes your operations and the window contents, and continues doing so until you manually stop the recording.

Next, I simply operate as I normally would: open NetEase Cloud Music, search for the style I want, find the target song and download it, then check whether the format matches my expectations, and delete it if it doesn’t...



### Step 3: Stop Recording and Generate the Skill

After the operation is complete, click the stop recording button.

Codex then analyzes the actions I just recorded and automatically generates a “music download” Skill file.

This Skill contains several key pieces of information: when to use the skill, what input parameters it needs, the exact execution steps, and how to verify that the task was completed successfully.

![](https://pic.yupi.icu/1/image-20260624181345019.png)



### Step 4: Replay

Once the Skill has been generated, the fun part begins—you can actually use it.

Start a new chat, use the Skill that was just created, and simply describe your need. For example, I asked AI to autonomously download 3 goofy songs.

Codex follows the operational path I demonstrated earlier and automatically completes the entire workflow.

![](https://pic.yupi.icu/1/image-20260624181451666.png)



## What Scenarios Are Suitable for Record & Replay?

After trying it out, my personal feeling is that this feature isn’t that useful for me. It’s flashy, but not very practical.

On the one hand, it currently only supports macOS, AI still can’t operate some apps, it’s slow, and it occasionally performs the wrong action.

On the other hand, Record & Replay is built on top of Computer Use, and Computer Use itself can already control your computer through prompts. So if you can clearly describe the operation in one or two sentences, you can just write a prompt directly and let AI do it. There’s no need to record.

So when does Record & Replay become truly valuable?

I think it’s this: **when your workflow is hard to describe, but easy to demonstrate.**

For example, in internal enterprise OA systems or reimbursement platforms—interfaces AI has never seen before—you may not be able to explain the steps clearly with prompts, but if you record the process once, AI can learn it.

Or when organizing data reports, maybe you instinctively choose a certain sort order, a certain color scheme, or skip certain fields. These implicit preferences may be hard for you to enumerate completely, but recording captures them all. Likewise, for long multi-app workflows where you have to click through many layers of menus, writing a several-hundred-word prompt may be less efficient than just recording for 2 minutes.

![](https://pic.yupi.icu/1/article-images/codex-record-replay/01_%E5%A4%8D%E6%9D%82%E6%B5%81%E7%A8%8B%E7%94%B5%E8%84%91%E6%93%8D%E4%BD%9C%E5%9C%BA%E6%99%AF_compressed_v2.png)

Unfortunately, I personally have very few scenarios like that. Most of the things I need can be done by letting AI operate through CLI commands instead, which is much faster than operating a GUI.

There’s another pitfall too: I suspect most people won’t be able to record their workflow perfectly in one go. You’re bound to make some accidental mistakes, like clicking the wrong button. AI may not be able to tell which actions were mistakes, so the resulting Skill may include unnecessary operations too.

So in summary, Record & Replay **doesn’t change what AI can do—it changes how you tell AI how to do it.** For programmers like us, writing prompts is already a strength, so many scenarios can be handled just by writing a prompt. But for coworkers who aren’t good at prompt writing—operations, HR, admin, and so on—this feature may be much more useful.



## How Record & Replay Works

Finally, let’s talk about how Record & Replay works under the hood. If you’re interested in AI app development, this is worth understanding—just in case it comes up in an interview someday.

Have any of you used key-macro tools before? When I was a kid, I used them to make auto-grinding scripts in games.

![](https://pic.yupi.icu/1/500fd9f9d72a6059c02bbf832834349b033bba74.jpg)

Traditional macro tools record rigid mouse trajectories: click once at coordinate (320, 450), wait 500 milliseconds, then click again at coordinate (180, 600). Shift the window position a little and everything breaks.

**Record & Replay is fundamentally different from that kind of traditional macro recording.**

During the recording phase, Codex is mainly observing and capturing. It does not analyze your operational intent in real time. Only after you stop recording does it inspect and distill the full captured workflow.

As we already saw earlier, what Codex generates is a `SKILL.md` file. At its core, it is a human-readable Markdown document that records **semantic steps** such as “enter keywords into the search box,” “click the download button,” and “select FLAC format,” rather than pixel-level coordinates.

When replaying, it also does not mechanically reproduce the mouse trajectory. Codex loads the Skill as context and then executes it using tools like Computer Use, browser control, and installed plugins. Because it understands the semantics rather than coordinates, the same Skill can theoretically be reused across different environments and tool combinations.

![](https://pic.yupi.icu/1/article-images/codex-record-replay/02_Codex%E5%BD%95%E5%88%B6%E4%B8%A4%E9%98%B6%E6%AE%B5%E5%8E%9F%E7%90%86_compressed_v1.png)

Also, the generated Skill is editable. You can manually modify `SKILL.md`, or ask Codex to optimize it further until you’re satisfied.



## Final Words

Record & Replay doesn’t change what AI can do. What it changes is the way you tell AI how to do it. For those complex workflows that are “hard to explain, but easy to demonstrate,” recording once can be much more efficient than writing prompts.

That said, this feature is still at a relatively early stage. My suggestion is to understand its principles and suitable use cases first, then wait until it matures before adopting it on a larger scale.
