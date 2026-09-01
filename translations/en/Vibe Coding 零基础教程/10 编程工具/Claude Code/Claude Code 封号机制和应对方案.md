# Claude Code Account Ban Mechanism and Response Strategies

> Understand how Anthropic identifies users, and what to do if your account gets nuked

Hello, I’m programmer Yupi.

If you’ve been learning AI programming, chances are you’ve heard about Claude Code account bans. A lot of people had accounts that worked steadily for a year and then suddenly got wiped out. Some companies with hundreds of employees were reportedly taken out almost all at once.

As everyone knows, Anthropic has been banning users in mainland China for a long time. But for a while, nobody really understood this: even if you were physically routing yourself through the U.S., how exactly was Anthropic still able to drag you out?

It wasn’t until foreign developers reverse-engineered Claude Code that they discovered a hidden user-tagging system built into the client.

![](https://pic.yupi.icu/1/image-20260701120931639.png)

In this article, I’ll explain three things in the simplest possible way: how Claude Code identifies users, how that earlier wave of large-scale bans happened, and what realistic options you have if you still want stable access to strong models.

This isn’t just drama-watching. Once you understand the mechanism behind it, you’ll have a much clearer idea of how to choose tools and models.



## 1. How Claude Code Identifies You

Here’s the simple summary: Claude Code reads local information from your computer, then uses a completely invisible method to stamp every request you send to the server with a hidden tag saying “this person is a Chinese user,” and sends that back to Anthropic’s servers.

![](https://pic.yupi.icu/1/02_%E6%95%B4%E4%BD%93%E6%A3%80%E6%B5%8B%E6%9C%BA%E5%88%B6%E6%A6%82%E8%A7%88%EF%BC%9AClaude_Code%E5%A6%82%E4%BD%95%E6%A0%87%E8%AE%B0%E4%B8%AD%E5%9B%BD%E7%94%A8%E6%88%B7_compressed_v3.png)

According to verification by multiple independent researchers, this detection mechanism has a trigger condition: you must have set an environment variable called `ANTHROPIC_BASE_URL`, redirecting Claude Code’s requests to a non-official API endpoint. In other words, if you are directly connecting to the official `api.anthropic.com`, the tagging mechanism does not activate.

![](https://pic.yupi.icu/1/03_%E8%A7%A6%E5%8F%91%E6%9D%A1%E4%BB%B6%EF%BC%9AANTHROPIC_BASE_URL%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F_compressed_v3.png)

But the problem is that most users in China need a relay endpoint to use Claude Code, so many Chinese developers have set this variable—and all of them end up being checked by this mechanism.



### Two Identification Paths

Under that condition, Claude Code uses two paths to judge whether you are a Chinese user.

**Path one: read your system time zone.**

If your system time zone is `Asia/Shanghai` or `Asia/Urumqi`, Claude Code tags you as a Chinese user.

Most Chinese developers may switch networks, but they usually don’t bother changing their computer’s time zone, because they still need their clock and calendar to work normally. So this path hits almost everyone.

![](https://pic.yupi.icu/1/04_%E8%AF%86%E5%88%AB%E8%B7%AF%E5%BE%84%E4%B8%80%EF%BC%9A%E7%B3%BB%E7%BB%9F%E6%97%B6%E5%8C%BA%E6%A3%80%E6%B5%8B_compressed_v2.png)

**Path two: compare your relay address against a domain blacklist.**

Because users in China can’t directly access Claude’s official API, many developers and companies use relay services. Claude Code extracts the address you put into `ANTHROPIC_BASE_URL` and matches it against a built-in domain list.

![](https://pic.yupi.icu/1/05_%E8%AF%86%E5%88%AB%E8%B7%AF%E5%BE%84%E4%BA%8C%EF%BC%9A%E5%9F%9F%E5%90%8D%E9%BB%91%E5%90%8D%E5%8D%95%E5%8C%B9%E9%85%8D%E6%9C%BA%E5%88%B6_compressed_v3.png)

The list itself is also obfuscated and encrypted. After reverse engineering, researchers found that it contains **147 domains**.

I looked through that list myself, and honestly, it was absurd.

It starts right off with the Chinese top-level domain `cn`, basically wiping everything out. Then come domains from major Chinese companies such as Baidu, Alibaba, and ByteDance, and even some internal Alibaba and Baidu domains didn’t get spared. On top of that, domains and keywords for almost every domestic AI company, such as DeepSeek and Zhipu, are on the list too. The rest is mostly made up of relay API service domains.

![](https://pic.yupi.icu/1/image-20260701122013567.png)



### Sending the Tag Back with Steganography

So that explains how Claude Code identifies Chinese users. The truly eye-opening part is what comes next: once it identifies the result, how does it send that information back to the server?

Every time you type a prompt in Claude Code, it prepends a system prompt before sending the request to the server. Inside that prompt is a completely ordinary-looking line with the date, like this:

```plain
Today's date is 2026-06-30.
```

That innocent-looking line is exactly where Claude Code makes two subtle modifications before sending the request.

First, it changes the date separator. If your time zone is identified as Chinese, the date format changes from `2026-06-30` to `2026/06/30`, replacing hyphens with slashes.

Second, it changes the Unicode encoding of the apostrophe in `Today's`. Depending on how your relay address matches, the apostrophe is replaced with different Unicode characters representing different meanings:

- `'` (U+0027, normal ASCII apostrophe) means nothing matched  
- `’` (U+2019, right single quotation mark) means the domain list matched  
- `ʼ` (U+02BC, modifier letter apostrophe) means an AI lab keyword matched  
- `ʹ` (U+02B9, modifier letter prime) means both matched

These four characters look identical to the human eye. In editors and terminals, you can’t tell them apart at all. But at the machine level, they are entirely different encoded values.

![](https://pic.yupi.icu/1/09_%E9%9A%90%E5%86%99%E6%9C%AF%E6%89%8B%E6%B3%95%E4%BA%8C%EF%BC%9A%E5%9B%9B%E7%A7%8DUnicode%E5%8D%95%E5%BC%95%E5%8F%B7%E7%9A%84%E5%8C%BA%E5%88%AB_compressed_v2.png)

This technique is called **steganography**—hiding secret information inside content that looks completely normal. It’s like writing an ordinary letter, except a few letters use ink from different brands. The recipient can scan it with a special device and read the hidden signal, while to you it looks totally normal.

After the server receives the request, it only needs to inspect which Unicode apostrophe was used and whether the date uses hyphens or slashes. That’s enough to immediately determine whether the request came from a Chinese user, whether it went through a relay service, and whether it is related to a Chinese AI company.

And the entire process requires no extra network requests and leaves no suspicious traffic trace, because visually those modified characters look exactly the same as normal ones. That’s why nobody noticed for so long, until someone reverse-engineered the program files.

Some people may ask: if they want to block relay users, why not just ban all of them directly? Why make it so complicated?

Because many overseas companies and developers also use custom API gateways for security and compliance reasons. If Anthropic banned all relay users with one blunt rule, it would hit a huge number of legitimate users too. So the official side chose a “smarter” method: quietly tag users first, keep collecting signals, and only make targeted banning decisions on the server side after enough data has accumulated.

One more warning: if you really receive a ban email and want to appeal, be careful even when opening the email. Some people found that Anthropic embedded tracking pixels in the email. The moment you open it, it can obtain your real IP address—basically confirming a second time that you’re in China.



## 2. The Full Story Behind the Large-Scale Ban Wave

Now that we understand the identification mechanism, let’s revisit that earlier giant ban wave. It’s the key to understanding why even innocent users ended up getting banned.

Here’s what happened. One day, a method started spreading in online communities, claiming that you could get a Claude Max 20x subscription for free. That’s Anthropic’s most expensive plan, costing $200 per month.

The news spread rapidly across Twitter, WeChat groups, and all kinds of tech communities. People were even selling tutorials on Xianyu.

![](https://pic.yupi.icu/1/image-20260729100925685.png)

So what exactly was going on?

In short, there was a security flaw in Claude’s official payment page. Someone wrote a browser extension script that, after running, could tamper with the checkout page and force-open a hidden European bank transfer payment channel that was not originally exposed to normal users. Then users only needed to generate a fake set of bank card numbers and address information online, fill it in, click subscribe, and the system would treat the payment as successful—instantly granting the highest-tier membership.

The root cause was that the backend server trusted the frontend too much.

Under normal circumstances, if a user selects a plan and a payment method on the webpage, the server should validate it independently. But Claude’s system skipped that step. If the frontend said it was paid, the backend believed it. On top of that, the European bank transfer channel itself worked in an asynchronous settlement mode, so the system granted membership privileges before the funds were actually confirmed.

Those two vulnerabilities stacked together and turned into a free-shopping exploit.

![](https://pic.yupi.icu/1/01_%E4%B8%A4%E4%B8%AA%E6%BC%8F%E6%B4%9E%E5%8F%A0%E5%8A%A0%E5%AF%BC%E8%87%B4%E9%9B%B6%E5%85%83%E8%B4%AD%E7%9A%84%E5%8E%9F%E7%90%86%E5%9B%BE_compressed_v1.png)

It’s like a buffet restaurant whose payment gate at the entrance starts opening without payment because of a bug. Of course a crowd will rush in for a free meal. I even heard that several relay API stations immediately started offering insane discounts that day—after all, if everyone could get the official subscription for free, who would still pay a middleman?

Unfortunately, the good times didn’t last long. The day after the exploit was exposed, Anthropic’s engineers shipped an emergency fix and the script became completely useless.

**But patching the vulnerability was only the first step. What came next was a massive ban wave.**

This ban wave was brutal. Anthropic didn’t just ban the accounts that used the exploit—they banned everything connected to them. If your device had ever logged into an account involved in the exploit, then even your older, fully paid normal account could be banned too if it had ever been used on the same computer. The device’s hardware information could also be permanently marked, making it very difficult to register a new account afterward.

Even crazier, some people had never used the exploit at all. They just happened to share the same proxy node as someone who did, and they got banned too.

The vulnerability itself was clearly Anthropic’s own technical failure. But after fixing it, they chose the most aggressive possible way to cut losses: not only banning exploit accounts, but also blacklisting linked devices and IPs. As for how many legitimate users got caught in the blast radius, judging from the previously reported 3.3% appeal success rate, they didn’t seem to care very much.



## 3. How Should We View This?

The foreign developer who reverse-engineered Claude Code directly accused Anthropic of embedding **spyware** in the client.

Some people argue that it isn’t spyware, just an anti-abuse compliance measure. But many more believe that silently tagging users without their knowledge is simply wrong.

![](https://pic.yupi.icu/1/image-20260701121820094.png)

My view is this: Claude Code is not an ordinary chat app. It runs in your terminal, has file system access, can read and write your code and configuration, and can even execute shell commands. Developers are placing a huge amount of trust in it. If it’s secretly stuffing hidden signals into every request behind your back, then once that gets exposed, people will always have a thorn in their mind when using it in the future, wondering whether it’s doing other hidden things too.

**If today it can report your time zone, tomorrow it can secretly report all of your data.**

There’s also a very practical issue here: for people truly doing large-scale resale or model distillation, this mechanism is actually not that hard to bypass. Just change the time zone and switch the domain, and you’re done. The people who end up getting precisely hit are instead ordinary developers who paid normally and used the product legitimately.

This also reminds us of one thing: no matter whose AI you use, your account, your conversation history, and your workflow can all be reset to zero after a single email.

By the way, bans and price hikes aren’t just a Claude problem. OpenAI’s Codex has also gone through several ban waves, including $200 accounts getting shut down without any warning. Cursor has always had regional restrictions. Even on the domestic side, there are peak/off-peak pricing models, limited availability, paid pro editions, and all kinds of other changes.

**AI capabilities are indeed getting stronger and stronger—but the barrier to stable access is also getting higher and higher.**



## 4. Realistic Response Strategies

After talking through all that, the most practical question is still this: what should we do next, and what model should we use?

**Option 1: Change the model, not the tool.**

If you like Claude Code’s interaction style and autonomy, you can absolutely keep the tool and only swap the underlying model. Connect it to domestic models such as DeepSeek, Kimi, or Zhipu GLM, and you get plenty of quota, no VPN gymnastics, and no fear of bans. For the exact steps, read *Connecting Claude Code and Codex to Domestic Models* in this directory. You can get it working in just a few minutes.

What you need to understand is that using a relay service together with an official Anthropic account is the highest-risk combination. But if you switch directly to a domestic model’s official API, that problem disappears, because you don’t need an Anthropic account at all.

**Option 2: Switch to Codex + the GPT series.**

If your budget is limited, Codex plus the GPT family is currently a pretty balanced choice in terms of both cost performance and intelligence. OpenAI often gives out refreshed quota, and its completion quality for many tasks like office automation and website development is quite solid.

![](https://pic.yupi.icu/1/image-20260729102157381.png)

**Option 3: Use domestic models, and don’t be biased against them.**

Domestic models have improved incredibly fast over the past year, and in many scenarios they’re no worse than foreign ones. For example, Kimi K3 is very strong at frontend development and visual effects. DeepSeek V4 has excellent cost performance and is especially suitable as a base model for AI app development projects. The GLM-5 series is also very competitive in full-stack development. If you want guidance on how to choose, read *AI Model Selection Guide* in the programming tools section of this tutorial.

![Frontend site built with Kimi K3](https://pic.yupi.icu/1/1784181917700-09e53717-bbf1-42c1-9f4e-c17413ace9f1-20260717144616347.png)

**Option 4: If you have the budget, use an official partner.**

If you have enough budget and still want to use Claude-family models, I recommend going through an official partner such as Cursor. It’s much more stable than subscribing to Claude directly. After all, Claude Opus 5 really is very strong at coding. I’ve already verified that in detail in *Claude Opus 5 Programming Capability Test – 7 Project Case Studies* in the model updates section of this tutorial. Why spend your days playing cat-and-mouse with Anthropic?



## Final Words

This article showed you Claude Code’s account-ban mechanism clearly: it uses the `ANTHROPIC_BASE_URL` environment variable as the trigger, identifies users through two paths—system time zone and domain blacklist—and then quietly sends the tag back to the server using Unicode steganography. We also reviewed that large-scale collateral ban wave caused by the payment vulnerability.

For us, the most valuable conclusion is actually this one: **critical workflows must always have a backup plan.**

Don’t bind all your productivity to one company and one account. If something can run locally, run it locally whenever possible. Keep models and tools replaceable whenever you can. That way, if one company suddenly loses its mind one day, you can switch immediately without affecting your work.

At the end of the day, tools and models are only means. What truly belongs to you is your ability to break down requirements, your engineering methodology, and your product thinking. Those things will not be reset to zero by a ban email.
