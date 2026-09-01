# Using AI for Coding in IDEA

> Even though AI coding tools are evolving rapidly, many students and teams still develop with JetBrains IDEA. The good news is that IDEA can also be connected to AI coding capabilities. Below are a few ways to do it.



## 1. Run AI in the Terminal

Open IDEA’s built-in terminal, and you’ll find quick-launch entries for AI tools like Claude Code and Codex right on the right side of the terminal (as long as you’ve already installed those tools). Besides that, JetBrains’ own Junie CLI can also run in the terminal.

![](https://pic.yupi.icu/1/image-20260515124926235.png)

Essentially, IDEA is just helping you run those tools’ commands in the terminal. It’s no different from using them in an external terminal, except you don’t have to keep switching windows.



## 2. Install Third-Party AI Plugins

Although standalone AI coding tools are developing very quickly now, AI plugins on JetBrains Marketplace are also being updated and iterated on continuously, and there are plenty of choices.

![](https://pic.yupi.icu/1/image-20260515125149230.png)

Personally, I recommend Tongyi Lingma and Cline. Tongyi Lingma is more friendly for users in China, with simple registration and enough free quota. Cline has strong Agent capabilities and is a good fit for students who like tinkering.

![](https://pic.yupi.icu/1/cline.png)



## 3. Connect AI Through the ACP Protocol

In January 2026, JetBrains and Zed jointly launched the ACP (Agent Client Protocol).

Simply put, ACP is a standard protocol that allows different AI coding Agents to plug into different IDEs in a unified way. Whether it’s Claude Code or Gemini CLI, as long as it supports ACP, it can be installed and used in JetBrains IDEs with one click.

![](https://pic.yupi.icu/1/01_ACP%E5%8D%8F%E8%AE%AE%E7%BB%9F%E4%B8%80%E8%BF%9E%E6%8E%A5AI_Agent%E5%92%8CIDE_compressed_v2.png)

They also launched a supporting ACP Agent Registry, which already offers more than 40 AI Agents that can be installed with one click.

The setup is simple too. First install the official AI Assistant plugin provided by JetBrains:

![](https://pic.yupi.icu/1/image-20260515125439230.png)

Then open the AI Chat panel. If it’s your first time using it, you can try it for free:

![](https://pic.yupi.icu/1/image-20260515125540920.png)

Or click “Add ACP Agents” to add Agents yourself. After clicking it, you’ll see a whole list of Agents like Claude Agent, Gemini CLI, Codex, Cursor, GitHub Copilot, and Cline. Just choose the one you need and click install.

![](https://pic.yupi.icu/1/image-20260515125748615.png)

By choosing the Agent yourself, you don’t need a JetBrains AI subscription. Once installed, you can use it right away. Pretty sweet~

![](https://pic.yupi.icu/1/image-20260515130149064.png)

Also worth mentioning: Claude Code has a [dedicated plugin](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-) for JetBrains called `Claude Code [Beta]`. Compared with running it directly in the terminal, it adds a few extra features, such as viewing diff previews directly in the IDE, automatically sending your selected code to Claude, and sharing IDE error information automatically. That said, the plugin is still basically a wrapper around the terminal version, so the overall experience isn’t as mature as the VS Code plugin. Better than nothing, I guess.

![](https://pic.yupi.icu/1/image-20260515131157123.png)



## Final Thoughts

Those are several ways to bring AI coding capabilities into IDEA: running tools directly in the terminal, installing plugins, or using the ACP protocol for unified integration. One of them is bound to suit you.

Once you’ve learned these, you can enjoy the productivity boost of AI coding without leaving IDEA.

If you want to keep learning more AI coding tools and hands-on techniques, check out the other articles in the Programming Tools section of this tutorial.
