# Connecting Claude Code and Codex to Domestic Models

A lot of people want to learn AI programming and try out the most popular tools right now, Claude Code and Codex, but they get stuck at step one.

Either they don’t have an overseas subscription account and can’t even log in, or they finally get access only to discover that the official quota is ridiculously expensive and gets used up after just a few conversations. On top of that, there’s always the risk of account bans, which makes people nervous the whole time.

We can’t let something as silly as “I can’t use the tool” kill our enthusiasm for learning AI programming!

In fact, both Claude Code and Codex support switching models. We can simply use domestic large models like DeepSeek, Qwen, or Zhipu GLM to power them instead—plenty of quota, no VPN tricks, and no fear of bans.

In this article, I’ll walk you through connecting domestic models to Claude Code and Codex step by step. I’ll use DeepSeek as the example. Once you get through it, the whole workflow will make sense, and switching to any other provider is basically the same.

Save this article and let’s get started~



## Why I Recommend DeepSeek

Before we dive in, let me first explain why I’m using DeepSeek as the example.

DeepSeek-V4-Flash is all about cost performance. Input costs 1 yuan per million tokens, output costs 2 yuan per million tokens, which is about one-tenth the price of V4-Pro.

![](https://pic.yupi.icu/1/image-20260803152949072.png)

More importantly, it has been significantly strengthened in Agent capabilities. On Terminal-Bench, which specifically tests AI’s ability to autonomously execute terminal tasks, it scored 82.7—surprisingly beating its own V4-Pro preview version at 72.1. It’s genuinely strong at coding, using tools, and autonomously executing tasks.

![](https://pic.yupi.icu/1/HOiZba2aYAAozFz.jpeg)

Strong Agent capabilities plus a low price makes it one of the best-value options for using Claude Code and Codex to learn AI programming.

**And the best part is that it natively supports the Responses API, so it can connect directly to Codex without any protocol conversion at all.** You’ll feel how convenient this is when we get to the configuration section later.

Of course, if you’ve already bought a plan from another platform—such as Zhipu GLM, Qwen, Kimi, or MiniMax—the logic is exactly the same. Just replace the Base URL and API Key with the ones from your own provider.



## What Is CC Switch?

Claude Code, Codex, and similar command-line tools all use different configuration formats. If you want to switch them to another model provider, you usually have to dig through docs, manually edit JSON, TOML, or `.env` files, and fill in a bunch of parameters like Base URL, API Key, and model name. One wrong character and the whole thing breaks. And switching back and forth between several models is even more annoying...

CC Switch exists to solve exactly this pain point. It’s a free open-source cross-platform desktop tool that gives you a visual interface to manage the configurations of multiple AI programming tools, including Claude Code, Codex, Gemini CLI, and OpenCode.

> Open-source repo: [https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)

![](https://pic.yupi.icu/1/1780312934749-a570e124-074c-40fe-924b-5f9719e45e56.png)

CC Switch comes with more than 50 built-in provider presets, including DeepSeek, Qwen, Kimi, Zhipu GLM, and MiniMax. You don’t need to edit config files manually anymore. Just click a few times to switch models with one click, and you can even switch quickly from the system tray.

![](https://pic.yupi.icu/1/image-20260601193909067.png)

Next, I’ll walk everyone through it in practice.



## Install CC Switch

Go to the [CC Switch official website](https://ccswitch.io) or the [GitHub Releases page](https://github.com/farion1231/cc-switch/releases/latest), and choose the installation method for your operating system.

![](https://pic.yupi.icu/1/1780310254037-fb0cd631-17e9-45cf-b1c2-963d18cbf99d.png)

For Mac users, I recommend installing it directly with a single Homebrew command:

```bash
brew install --cask cc-switch
```

![](https://pic.yupi.icu/1/1780310254160-ed387f10-f656-429f-a41d-8e288b8e3be2.png)

Windows users can download the `.msi` installer from the Releases page and double-click to run it. Linux users can choose `.deb`, `.rpm`, or `.AppImage` depending on their distro.

After installation, launch CC Switch. Its main interface will appear on your desktop or in the system tray.

Next, we’ll connect DeepSeek to Claude Code and Codex respectively. But before that, we need to prepare a DeepSeek API Key.



## Prepare a Large-Model API Key

No matter which tool you want to connect, you first need a DeepSeek API Key.

Go to the [DeepSeek Open Platform](https://platform.deepseek.com), sign up and log in, enter the API keys page, and create a new key.

![](https://pic.yupi.icu/1/image-20260601194058029.png)

Be careful: the key will only be shown in full once when it’s created. Copy and save it right away, because you’ll need it shortly in CC Switch.



## Connect DeepSeek to Claude Code

Let’s start with the simpler one: Claude Code.



### First, Install Claude Code

Let me briefly introduce Claude Code. It’s an AI programming tool launched by Anthropic that runs directly in the terminal. You chat with it and describe requirements, and it can autonomously analyze the project, write code, run commands, and fix bugs—all on its own.

![](https://pic.yupi.icu/1/1780310254072-69c9a86c-ede2-40e7-807c-13684461d4c2.png)

Installing Claude Code is simple. First, make sure your computer has Node.js installed. If not, download the beginner-friendly installer from the [Node official site](https://nodejs.org/en/download). Then one command does the job:

```bash
npm install -g @anthropic-ai/claude-code
```

Once installed, type `claude` in the terminal to enter the chat interface. The first time you use it, you need to log in. But many people don’t have an official Anthropic account, so they get stuck right there and can’t use it directly at all.

Don’t worry. Next, we’ll use CC Switch to swap it over to DeepSeek.



### Switch Models with CC Switch

Open CC Switch, choose **Claude** in the app bar at the top, then click “Add Provider”:

![](https://pic.yupi.icu/1/1780310658228-ffa4ff69-342c-4244-82e3-2204dad61e97.png)

From the list of preset model providers, choose **DeepSeek**:

![](https://pic.yupi.icu/1/1780310679329-e280982b-da09-4f4e-8861-d943f39f17ed.png)

Then fill in the API Key you just created on the DeepSeek Open Platform:

![](https://pic.yupi.icu/1/1780310750547-43515207-6f23-45b7-a62f-56370070da4f.png)

You usually don’t need to change the other fields. The DeepSeek preset in CC Switch already comes with the models configured for you, including both DeepSeek-V4-Pro and DeepSeek-V4-Flash. The main model defaults to Pro (corresponding to Claude Code’s Opus slot), and the small model defaults to Flash (corresponding to the Haiku slot).

If you want to save money while still getting solid performance, it’s totally fine to use V4-Flash for everything. Its Agent capabilities are already very strong.

If you want to use DeepSeek V4’s 1 million-token ultra-long context, you can also directly enable 1M mode here. That tells Claude Code the model can handle that much context, without you having to edit configs manually.

![](https://pic.yupi.icu/1/1780310818585-ecfe1960-f1cd-4a31-a1e7-f1da199c17d9.png)

After filling everything in, click the “Add” button in the lower-right corner. Here you can even see Claude Code’s JSON config file—CC Switch’s whole job is to let you modify it visually, saving you from manual editing.

![](https://pic.yupi.icu/1/1780310894533-0153954b-e19f-4e96-93a5-de8208e08c01.png)

Finally, click to enable the DeepSeek model:

![](https://pic.yupi.icu/1/1780310914775-338bbb35-872d-46ad-9cbf-5731341a3942.png)

Restart Claude Code. In the upper-left corner, you’ll be able to see the currently active model. Ask it to identify itself with a line like: “What model are you?”

If the AI replies normally, that means the switch was successful:

![](https://pic.yupi.icu/1/1780311048597-711eca09-fe5c-4d0a-bb01-7c9bbfcb033c.png)

You may notice that connecting DeepSeek to Claude Code through CC Switch is especially simple. That’s because DeepSeek provides an Anthropic-compatible API, and Claude Code already speaks that protocol. CC Switch just writes the configuration into `settings.json`, and everything works.



## Connect DeepSeek to Codex

Now that Claude Code is set up, let’s look at Codex. It’s OpenAI’s AI programming tool, and its recent popularity has been absolutely explosive. OpenAI often gives out refreshed quota, so there’s a ton of usage to burn through.

![](https://pic.yupi.icu/1/1780311345253-521a8636-47ec-4d53-bb1a-e350748e2085-20260601194352039.png)

Codex comes in two forms: the command-line Codex CLI and the desktop APP with a graphical interface.

The CLI version is installed similarly to Claude Code—just one command:

```bash
npm install -g @openai/codex
```

After installation, type `codex` in the terminal to enter the chat interface. The first time you use it, you also need to log in to an OpenAI account. If you don’t have one, then you’ll need to do a bit of tinkering to switch models.

![](https://pic.yupi.icu/1/1780311431037-8b655299-d1f1-4ff5-a845-988c0980c4ca.png)

As for installing and using the Codex desktop APP, I recently published a full *video + illustrated tutorial* on it. If you need it, just grab it from my [Yupi AI Navigation](https://ai.codefather.cn/library/2058749249474023425):

![](https://pic.yupi.icu/1/image-20260601194545597.png)

There are three ways to connect DeepSeek to Codex. I’ll go through them in recommended order.



### Method 1: Official One-Click Script (Recommended)

DeepSeek officially provides a configuration script. Run it once, and it handles everything.

Before running it, make sure you have already installed the Codex CLI or the ChatGPT desktop APP and launched it at least once so that the `~/.codex` config directory has been created. The script needs to write files there.

> Official docs: [https://api-docs.deepseek.com/quick_start/agent_integrations/codex/](https://api-docs.deepseek.com/quick_start/agent_integrations/codex/)

On Windows, run this in PowerShell:

```powershell
irm https://cdn.deepseek.com/api-docs/codex-deepseek-setup-en.ps1 | iex
```

On Mac or Linux, run this in the terminal:

```bash
bash <(curl -fsSL https://cdn.deepseek.com/api-docs/codex-deepseek-setup.sh)
```

After the script starts, it will ask you which model you want to use. Currently, DeepSeek-V4-Flash can be selected directly—just enter `1`:

![](https://pic.yupi.icu/1/image-20260803114529569.png)

The first time you run it, it will also ask you to enter your API Key:

![](https://pic.yupi.icu/1/image-20260803114842807.png)

Then hit Enter and let it run. In just a few moments, the script will wire DeepSeek into Codex for you.

![](https://pic.yupi.icu/1/image-20260803114928055.png)

To elaborate a bit more, the script automatically does the following:

1. Backs up your existing Codex configuration into the `~/.codex/backup-deepseek/` directory so you can restore it anytime  
2. Generates a `~/.codex/models.json` file that tells Codex the metadata for DeepSeek models, such as context window size and supported reasoning levels  
3. Modifies `~/.codex/config.toml` to write in DeepSeek’s API configuration while preserving your previous MCP servers and project settings  
4. Automatically validates the config syntax and aborts if there’s an error, so your files won’t be corrupted

After configuration is complete, reopen Codex. If the startup banner shows `deepseek-v4-flash`, it means everything has been configured successfully:

![](https://pic.yupi.icu/1/image-20260803120531949.png)

If you’re using the ChatGPT desktop APP or the Codex VS Code plugin, you don’t need separate configuration. Just open them and they’ll also use DeepSeek, because they share the same config files as the CLI.

![](https://pic.yupi.icu/1/image-20260803141956962.png)

If you want to switch back to the official models, just rerun the script and choose the restore option from the menu.

![](https://pic.yupi.icu/1/image-20260803115518337.png)



### Method 2: Edit the Config Files Manually

If you don’t want to run the script, you can modify the config files yourself. It only takes two steps.

Step one: locate the `.codex` folder in your user directory (`~/.codex/` on Mac/Linux, `%USERPROFILE%\\.codex\\` on Windows), and create a `models.json` file. You can copy the file content directly from the [official DeepSeek docs](https://api-docs.deepseek.com/zh-cn/quick_start/agent_integrations/codex/).

![](https://pic.yupi.icu/1/image-20260803113859064.png)

The purpose of this file is to tell Codex about DeepSeek’s model parameters, such as support for a 1 million-token context window and support for `low` / `high` / `max` reasoning levels.

Step two: edit the `config.toml` file in the same directory and add the following config:

```toml
model = "deepseek-v4-flash"
model_provider = "deepseek"
preferred_auth_method = "apikey"
forced_login_method = "api"
model_reasoning_effort = "high"
model_catalog_json = "~/.codex/models.json"

[model_providers.deepseek]
name = "deepseek"
base_url = "https://api.deepseek.com/"
wire_api = "responses"
experimental_bearer_token = "<你的 DeepSeek API Key>"
```

Just replace `experimental_bearer_token` with your own API Key.

The key line here is `wire_api = "responses"`. It tells Codex to talk to DeepSeek using the Responses API protocol. Since DeepSeek-V4-Flash supports that protocol natively, it works directly.

After saving the file, reopen Codex and you’ll be able to use DeepSeek-V4-Flash.



### Method 3: Use CC Switch for Protocol Conversion

The first two methods are so convenient because DeepSeek provides native support. But if the model you want to connect is something like Zhipu GLM, Kimi, or MiniMax, which still don’t support the Responses API, then changing only the `base_url` will most likely fail with a 404 error.

The problem lies in the protocol. Codex uses OpenAI’s **Responses API**, while most domestic models use the **Chat Completions API**. They are simply not the same thing. It’s like making a phone call: the number connects, but you speak Chinese and the other side only understands French. You still can’t communicate.

![](https://pic.yupi.icu/1/01_%E7%94%B5%E8%AF%9D%E6%AF%94%E5%96%BB-%E5%8D%8F%E8%AE%AE%E6%A0%BC%E5%BC%8F%E4%B8%8D%E9%80%9A_compressed_v2.png)

So in this situation, the key is having a **translator** in the middle to convert the requests Codex sends into a format the model can understand.

Fortunately, CC Switch has already handled this for us. Its **local routing** feature starts a lightweight proxy service on your own computer. The request flow looks like this:

```plain
Codex → CC Switch → 大模型 → CC Switch → Codex
```

The forwarding is completely transparent to Codex. Codex still thinks it’s talking to OpenAI’s official API. That means you get the original Codex experience while using low-cost domestic models underneath. Pretty nice, right?

![](https://pic.yupi.icu/1/02_CC_Switch%E6%9C%AC%E5%9C%B0%E8%B7%AF%E7%94%B1%E5%8D%8F%E8%AE%AE%E8%BD%AC%E6%8D%A2%E6%B5%81%E7%A8%8B_compressed_v3.png)

I’ll still use DeepSeek to demonstrate the flow below (since I already have the screenshots), but the steps are the same for any other provider.



#### 1. Add a Provider in CC Switch

Open CC Switch, switch to **Codex** in the top app bar, and click “Add Provider”:

![](https://pic.yupi.icu/1/1780311605982-1c994d40-c7f4-48df-817c-bed2b6c31fab.png)

Search for and select **DeepSeek** from the presets, just like when we configured Claude Code earlier:

![](https://pic.yupi.icu/1/1780311659008-be813d0f-d761-435f-a7cb-a74899214864.png)

Fill in your DeepSeek API Key and leave the other fields at their default values:

![](https://pic.yupi.icu/1/1780311678381-5d244f5c-6943-43ba-a6c3-a2a29960d907.png)

Just like with Claude Code, CC Switch has already preset the model information for you, so you generally don’t need to touch the other fields.

One especially important point: at this step you must **enable “Local Route Mapping”**, then click the “Add” button in the lower-right corner to save.

![](https://pic.yupi.icu/1/1780311713574-2317e9a2-ece4-4c4d-a188-4d6735402c6a.png)

Back on the home page, choose to enable DeepSeek:

![](https://pic.yupi.icu/1/1780311910051-908552fe-d168-4df1-9a08-3c9e6f1e4d0d.png)

But at this point, you still can’t use DeepSeek normally in Codex. If you try chatting, you’ll get the 404 error mentioned earlier:

![](https://pic.yupi.icu/1/1780311879234-642050c1-2333-4d8e-866d-1abc9197d7dd.png)



#### 2. Turn On Local Routing

After switching to DeepSeek, the system will prompt you to enable routing. Click the “Settings” button in the upper-left corner to enter the settings page:

![](https://pic.yupi.icu/1/1780311968017-bf4e43f6-736e-4ba7-9ce9-5a9ca2763910.png)

Find the routing settings menu, turn on the main local routing switch, and then enable Codex routing:

![](https://pic.yupi.icu/1/1780312030888-cdfafb55-0a3f-4fd7-bdc5-785eb3cd9bc8.png)

This step is what lets CC Switch’s local proxy officially take over Codex’s requests. The protocol conversion we discussed earlier depends entirely on it.

And that’s it!

Reopen Codex CLI and you’ll see it has switched to the DeepSeek model. Again, ask it to identify itself. If it can chat normally, the switch was successful:

![](https://pic.yupi.icu/1/1780312108872-2c760023-290a-4e7a-b8d0-be36159900da.png)

You may notice that the AI still says it is Codex based on GPT-5. That’s because Codex injects its own system prompt into the model, causing it to assume it’s the official model by default. But the actual model doing the work underneath has already been swapped to DeepSeek.

Now let’s also try the Codex desktop APP. Since it shares the same `~/.codex` configuration as the CLI version, once CC Switch has changed it, you can open the app directly and use it. Ask what model it is, and the underlying model will also be DeepSeek:

![](https://pic.yupi.icu/1/1780312248394-f117f7bb-1372-4a73-91e7-2b6c171cef6f.png)

If you want to switch back later, just reverse the steps: turn off routing and re-enable the default configuration.

![](https://pic.yupi.icu/1/1780312343473-b43668a4-cb80-4f60-8fce-e7aa93e7753e.png)

So, not nearly as hard as you imagined, right?

Switching to other providers follows the exact same flow: choose the corresponding preset in CC Switch (or create a custom one if there isn’t a preset), fill in the provider’s Base URL and API Key, and don’t forget to enable local routing.



## Add Image Understanding to Text-Only Models

After configuration, there’s one more pitfall I need to mention.

Although DeepSeek-V4-Flash has strong Agent capabilities, it is a **text-only model**. It cannot understand images. So if you ask it in Codex or Claude Code to analyze a screenshot or look at what a UI page looks like, it simply can’t do that.

Fortunately, there’s a ready-made solution: install a **Vision Skill** for your AI programming tool, and let a separate multimodal vision model handle the image understanding for it.

For example, this general-purpose [multimodal vision recognition Skill](https://github.com/asuojun/claude-vision-skill) is designed specifically for models like DeepSeek that lack vision capabilities. And because Skills follow a general standard, tools like Codex and Claude Code can both install and use it.

You first need to prepare a vision model that supports image understanding, such as Tongyi Qianwen’s Qwen3.8-Max, and get an API Key from the corresponding model platform.

![](https://pic.yupi.icu/1/image-20260803154236012.png)

Then simply send a prompt inside your AI programming tool and let AI handle the installation and configuration of the Skill for you:

```plain
全局安装 Vision Skill（https://github.com/asuojun/claude-vision-skill），按照 README 的说明进行配置。
- 视觉模型用通义千问的 qwen3.8-max
- API Key 为 <改为你自己的 API Key>
```

![](https://pic.yupi.icu/1/image-20260803155552049.png)

Once installed, whenever the AI encounters a task that requires looking at an image, the Vision Skill will automatically send the image to the vision model, convert the image content into text descriptions, and then hand that description back to DeepSeek for continued reasoning.

![](https://pic.yupi.icu/1/image-20260803155836402.png)

If you don’t often need AI to look at images while coding, you can skip this for now and install it later when you actually need it. If you want to learn more about Skills, you can read *Agent Skills: Universal AI Skill Library* in the “Tool Practice” section of this tutorial’s programming tools chapter.



## Final Words

In this article, I walked you step by step through connecting domestic large models—using DeepSeek as the example—to Claude Code and Codex.

For connecting DeepSeek to Codex, the official one-click script is the best choice, because DeepSeek natively supports the Responses API and doesn’t need any protocol conversion. If the model you want to connect does not support that protocol, then use CC Switch’s local routing for conversion. Connecting a model to Claude Code is even simpler, because mainstream domestic models generally provide Anthropic-compatible APIs, so a few clicks in CC Switch are enough.

By now, you’ve probably realized that the barrier to learning AI programming today is truly lower than ever. Million-token context windows, strong Agent capabilities, and ridiculously low prices—the cost may be just a fraction of official subscriptions.

**Tools and models should never become roadblocks on your learning journey.**

So stop using “I don’t have an account” or “I can’t afford it” as excuses. Set up your environment and start using the tools—that’s what matters. As for which model is best for which kind of task, you can read *AI Model Selection Guide* in the programming tools section of this tutorial. And if you want to understand why Claude Code gets accounts banned and what alternatives exist, read *Claude Code Account Ban Mechanism and Response Strategies* in this same directory.
