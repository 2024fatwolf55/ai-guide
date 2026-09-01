# Codex Theme Customization Tutorial

> Use an open-source project + AI to give Codex a personalized theme skin with zero barrier

Hello everyone, I’m programmer Yupi.

Today I saw something pretty interesting in an AI group chat: someone was actually selling Codex themes on Xianyu?

The price could even go as high as 199 yuan??

And quite a few people were actually buying them???

![](https://pic.yupi.icu/1/1784208749956-7d531c30-1965-49b6-8ea1-b4bfb9614cd2.png)

That reminded me of how Sogou once made hundreds of millions from input-method skins. I didn’t expect the same business logic to be applied so quickly once the AI programming tool Codex became popular.

But the truth is, customizing a Codex theme is not difficult at all, and you definitely don’t need to pay for it!

Because some talented devs have already turned Codex skinning into an open-source project called **Codex Dream Skin**. It was just launched on GitHub, and in only 1 day it had already collected thousands of Stars!

> Open-source repo: https://github.com/Fei-Away/Codex-Dream-Skin

![](https://pic.yupi.icu/1/image-20260716214544049.png)

The purpose of this project is to turn Codex from its default black text on white background into whatever style you want. It doesn’t just let you customize the background image—you can also change the color scheme, decorative elements, sidebar, input box, suggestion cards, and more.

The open-source author shared several custom theme effects, and the variety is actually pretty rich.

First up is the beautiful-girl theme. Who wouldn’t get dizzy looking at this?

![](https://pic.yupi.icu/1/1784208357649-d460e25e-e0e2-44e7-a725-eb87040de868.png)

Then there’s the God of Wealth theme. You’d probably feel extra motivated to work with this skin on, right?

![](https://pic.yupi.icu/1/1784208375262-951cb396-a283-4ec6-b3b9-cec4e9b450be.png)

There’s also a Hatsune Miku theme. It’s hard to imagine this is even an AI tool.

![](https://pic.yupi.icu/1/1784208390753-d02b6c7d-58dc-4183-a397-03bbe073cf19.png)

And my personal absolute favorite: brother Kun. Vibe Coding with your idol—what a beautiful life~

![](https://pic.yupi.icu/1/1784208397884-4677f133-2cb7-49f8-853b-ee034a03021d.png)

And note: all native controls—sidebar, input box, project selector—remain fully clickable and usable. This is not some fake screenshot slapped on top to fool people.

That said, because the project was only recently open-sourced, it still has some usage barriers for people with zero programming background. The README contains a bunch of scripts and technical terms, and I’m guessing many people still wouldn’t know where to start after reading it.

So below, standing on the shoulders of giants, I’ll directly teach you a “simple enough for anyone” way to customize a Codex theme.

The core steps are actually just three, and AI handles the whole process for you.



## Codex Theme Customization in Practice

I personally used Codex + GPT 5.6 to make a Naruto Uchiha Sasuke theme. Let me share the whole process with everyone.

![](https://pic.yupi.icu/1/1784207621768-328cf53a-9040-4aff-ab34-31345f1cbb5b-20260716221035511.png)

First, open Codex and tell AI directly:

```markdown
使用这个开源项目，帮我更换 Codex 的主题 https://github.com/Fei-Away/Codex-Dream-Skin
```

AI will automatically clone the repository, inspect your runtime environment (Node.js version, operating system, etc.), and then execute the installation script.

![](https://pic.yupi.icu/1/1784207655690-1954481c-4005-4f35-b79d-54ef80ea605b.png)

After installation, AI first runs the default built-in theme from the project to make sure the environment works properly.

Then you’ll see that the Codex interface has already changed, which means the skinning engine has taken effect.

Next, you can directly ask AI to generate fully personalized assets for you.

For example, I told AI:

```markdown
帮我生成火影忍者宇智波佐助的背景图，以及脚本支持的一些额外的定制元素图片，我要进行全方位的替换。
```

GPT 5.6 can generate images directly (though it’s relatively slow). It created a complete Sasuke-themed asset pack for me, including a widescreen background of Sasuke with Susanoo, a transparent Uchiha crest, dark sidebar textures, Chidori lightning corner decorations, and most importantly, the Mangekyō Sharingan.

![](https://pic.yupi.icu/1/1784207704853-20f3956a-9e10-49e7-b1d0-e5e1a3cac81a.png)

After generating the assets, AI automatically applies them to Codex.

However, because there are so many theme elements that can be customized, the first generated version will very likely still have places that don’t feel quite right.

For example, I noticed that some text colors were hard to read on the dark background, so I just told AI directly what looked wrong:

```markdown
好像还有些文字显示的配色是有问题的
```

![](https://pic.yupi.icu/1/1784207724134-00b62172-2e55-49f8-bc75-d27e46427461.png)

From start to finish, going from zero to a complete custom theme involved almost no barrier. It was basically just chatting with AI. The only downside is that it’s a bit slow—most of the time is spent waiting for AI to generate images and tweak the color scheme.



## How Does It Work?

Some of you may be wondering: Codex doesn’t even have an official theming API, so how does this project manage to reskin it?

The principle is actually not complicated. The Codex desktop app is essentially an Electron application, and its interface is rendered using web technologies. This project uses CDP (Chrome DevTools Protocol) to inject custom CSS and JavaScript into the local loopback address `127.0.0.1`, effectively layering decorations on top of the Codex interface.

The whole injection process only goes through your own computer’s local address. It does not involve any external network communication, nor does it modify Codex’s official `.app` installer package or code signature. It only adds a visual layer at the interface level. And if you want to restore the original appearance, you can simply ask AI to run the project’s built-in Restore script. One command brings everything back to normal and doesn’t affect future updates.

![](https://pic.yupi.icu/1/01_Codex%E6%8D%A2%E8%82%A4%E5%8E%9F%E7%90%86%EF%BC%9AElectron%E5%BA%94%E7%94%A8%E9%80%9A%E8%BF%87CDP%E5%9C%A8%E6%9C%AC%E6%9C%BA%E6%B3%A8%E5%85%A5CSS_JS%E5%AE%9E%E7%8E%B0%E6%8D%A2%E8%82%A4_compressed_v1.png)



## Final Words

Besides theme skinning, Codex’s desktop pets also support customization. If you’re interested, you can check out [this tutorial](https://mp.weixin.qq.com/s/i9iLg_AG7rODCFa34vCVfA). Do it yourself and you’ll have everything you need~

![](https://pic.yupi.icu/1/1777952393166-c0044771-8017-4e51-a4b5-9ac9a8905a71-20260716221036540.png)

The Codex ecosystem is developing rapidly, and theme customization is just one of many ways to play with it. If you want to learn more ways to use Codex, you can read *Codex: AI Desktop App Beginner-Friendly Tutorial* in the Codex section of this tutorial’s programming tools chapter. It contains a complete guide from installation to real practice.

I hope everyone can build their own personalized AI programming environment and have fun with it!
