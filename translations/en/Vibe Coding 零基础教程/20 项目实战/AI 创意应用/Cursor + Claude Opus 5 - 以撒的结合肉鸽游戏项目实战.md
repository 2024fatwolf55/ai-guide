# Cursor + Claude Opus 5 - The Binding of Isaac Roguelike Game Project Practice

This project is a top-down roguelike dungeon web game that recreates the core gameplay of *The Binding of Isaac*. It includes 12 dungeon floors, 13 bosses, 11 enemy types, and 55 items, with more than 7,900 lines of vanilla JavaScript, zero dependencies, zero build steps, and all art assets drawn entirely in code without using any external image resources. The whole thing was developed with Cursor + Claude Opus 5. I only talked to AI for two rounds and didn’t write a single line of code myself.

Project code is open source for free: [https://github.com/liyupi/binding-of-isaac-webgame](https://github.com/liyupi/binding-of-isaac-webgame)

Play online (it also works on phones): [https://yisa.codefather.cn](https://yisa.codefather.cn)

⭐️ I recommend watching the video version—the demo looks even better there: [https://bilibili.com/video/BV1sQGA6EEjp](https://bilibili.com/video/BV1sQGA6EEjp)

![](https://pic.yupi.icu/1/image-20260730215626570.png)



## Project Overview

This was my favorite game when I was a kid. I never could have imagined that now I’d build it from 0 all by myself—and with only 10 minutes of input from me.

![](https://pic.yupi.icu/1/image-20260730215906823.png)

When I was little, I dreamed of making my own game, but at that time it was completely impossible: no skills, no time.

It wasn’t even mainly because I couldn’t code. The real barriers to making a game hide elsewhere: you need to draw assets, understand level design, tune game balance, and playtest over and over to get the feel right. For a programmer who only knows how to write business code, just the step of “drawing a character that doesn’t look terrible” is enough to make you give up.

What makes *The Binding of Isaac* so addictive is its randomly generated dungeons, build synergies that keep getting stronger, and boss fights at the end of every floor. Once you start a run, it’s hard to stop.

Earlier, when I was evaluating Kimi K3, I had already tried asking AI to recreate this game. The result back then had a pretty rough interface, but the basic gameplay worked—you could move around and shoot enemies—and I was already quite satisfied with that:

![Kimi K3 当时开发的版本](https://pic.yupi.icu/1/1784190076766-03662fe2-7400-4938-87d1-422f3d992bd7-20260717144628318-20260728104643161.png)

Later, after Claude Opus 5 was released, I ran the exact same prompt again in Cursor. The combination of those two together completely blew my mind.

![](https://pic.yupi.icu/1/image-20260730222704353.png)

In this article, I don’t just want to show you the finished result. More than that, I want to make one thing clear: **AI writing code is no longer the bottleneck. The thing that really takes time is figuring out whether it wrote the right thing.** The most valuable lessons from this project are all in the validation phase.

I’ll also share the complete prompt with you, so you can absolutely reproduce it yourself.



## Feature Demo

First, take a look at what the final product became, and you’ll immediately understand the level AI has reached.

1) Random dungeon generation and combat

Every dungeon floor is randomly generated and includes combat rooms, treasure rooms, shops, and a boss room. The character fires tears to attack enemies, and you can only move to the next room after clearing the current one.

![](https://pic.yupi.icu/1/1785146642381-79f6906f-4e68-4427-b72e-0aa3115e8233.png)

2) 11 kinds of enemies, each with different behavior patterns

It’s not just a simple matter of changing color or HP. Every enemy has different movement and attack behavior. For example, Horf never moves and only spits fan-shaped bullet patterns; Attack Fly dashes quickly and erratically, bouncing off walls; Knight has 92% frontal damage reduction, so you have to flank it from behind; Globin collapses into a puddle the first time it dies and then reassembles itself 2.4 seconds later; Vis charges up for 0.85 seconds and then fires a bloody laser that pierces across the whole room.

3) 55 stackable items

Items fall into four categories: changing attack style, changing survivability, changing stats, and changing the character’s appearance—and they can all stack with each other. For example, after picking up Brimstone, normal tear shots become charge-up bloody lasers; after picking up Ipecac, tears explode when they land, but can also damage you; Holy Mantle makes you immune to the first hit in each room and even gives you a visible shield bubble.

The character stats panel stays pinned to the bottom-left corner. Stats higher than the baseline are shown in blue, lower ones in red, and beneath them is a row of icons for picked-up items.

![](https://pic.yupi.icu/1/1785146850442-e539fdbd-b359-4769-a65c-22b4638885c7.png)

4) 12 dungeon floors, each with a completely different art style

Starting from the brown stone tiles of BASEMENT on Floor 1, the game gradually descends all the way to the fleshy ground of WOMB on Floor 7 (where the tile grid disappears and is replaced by layered flesh, crawling blood vessels, and pores), then the charred black ground and ember glows of SHEOL on Floor 10, and finally the white marble and stained-glass arches of CATHEDRAL on Floor 11.

The key point is that every single one of those visual assets was drawn entirely in code—without using even one image file.

5) 13 bosses, each with its own state machine

Every boss has its own attack patterns and phase changes. For example, MONSTRO charges up by flattening itself and then leaps into a slam, with a red circle warning for the landing spot during high jumps, and enters an enraged state at 50% HP. SCOLEX can only be damaged on its flashing tail segment and spends most of the time burrowing underground invulnerably. SATAN has three phases, and in the final phase it rises off the ground to stomp and summon explosive flies.

![](https://pic.yupi.icu/1/1785146825259-76b4c935-67a7-46e3-9ede-3d0659eed806.png)

6) Shops, death summary, and mobile adaptation

Starting from Floor 2, shops begin to appear, with three shelves and prices that scale with dungeon depth, so coins finally have a purpose. The death screen summarizes kills, picked-up items, survival time, deepest floor reached, rooms explored, and bosses defeated. When opened on a phone, the game automatically shows a virtual joystick. It works in portrait mode, and the screen is bigger in landscape.

![手机上也能爽玩](https://pic.yupi.icu/1/image-20260801104922776.png)

By the way, if you compare the character design with the original game, you’ll find the recreation is actually quite faithful:

![原版游戏形象](https://pic.yupi.icu/1/1785146563523-6fed4f0b-08d8-4c82-bf24-343a46a418d4.png)

I only included a few screenshots above. The full appearances of all 12 dungeon floors, 13 bosses, and 11 enemies are in the open-source repo’s [screenshot gallery](https://github.com/liyupi/binding-of-isaac-webgame/blob/main/docs/GALLERY.md), or you can just open the [online demo](https://yisa.codefather.cn) and experience it for yourself.



## Full Prompt

You’re probably curious: it was done in one round of conversation? Then the prompt must have been insanely good, right?

Alright, let me show you the full prompt. It’s long and messy, but most of it was actually generated by AI. The original requirement was only about two short paragraphs, and then I had AI iteratively optimize and expand it step by step until it became what it is now.

![](https://pic.yupi.icu/1/image-20260731084717923.png)

I used Cursor’s `/goal` command to execute it. The full content is below, and you can reuse it directly:

```plain
开发一个完全复刻「以撒的结合」核心玩法的肉鸽地牢网页游戏。俯视角，玩家操控角色在随机生成的房间中探索，用射击消灭敌人，清完一个房间后门打开进入下一个房间，每层有若干个房间和一个 Boss 房。

请先用 Firecrawl 联网搜索以撒的结合的游戏机制、美术风格、角色设计等资料，尽可能还原原作的视觉风格和游戏体验。游戏中的角色、敌人、道具、房间等图形素材用代码绘制，风格要贴近原作的暗黑卡通风。开发时用 Context7 查询所用游戏框架或库的最新文档。

核心系统包括：随机地牢生成（每层 5-8 个房间，房间之间有门连接）、射击战斗（玩家发射眼泪/子弹攻击敌人，敌人有不同的移动和攻击模式）、道具系统（击杀敌人或开宝箱随机掉落道具，道具能改变攻击方式、属性数值或角色外观）、属性系统（生命值、攻击力、射速、移动速度、射程）、至少 3 种普通敌人和 1 个 Boss。

操控方式：WASD 移动，方向键发射子弹（对应四个方向），桌面端键盘操控，移动端有虚拟摇杆和射击按钮。包含开始界面、死亡界面（显示本次探索统计：击杀数、拾取道具数、存活时间）、通关界面。

用 Loop Engineering 方式推进：先做一个房间 + 角色移动射击 + 一种敌人，确认战斗手感；然后加多房间连接和地牢生成；再加道具掉落和属性系统；最后做 Boss 和完整的游戏流程。每完成一步自己试玩验证，截图查看游戏画面渲染效果，根据截图判断角色、敌人、房间的视觉表现是否贴近原作风格，确保战斗手感好、敌人行为正常、道具效果生效、房间切换流畅，发现问题就自主修复。
```

If you study this prompt carefully, you’ll notice several highlights:

- The requirements are written clearly and concretely, spelling out the core systems, control scheme, and interface flow
- It tells AI to use web search to look up the original game’s mechanics and visual style as reference, instead of just making things up from memory
- It uses the Loop Engineering mindset, making AI test and verify after every step, fix issues by itself, and keep iterating until it delivers a finished product

That third point is the key reason this project succeeded. If you only say “make a Binding of Isaac game,” AI will most likely give you a demo that technically runs but isn’t actually fun. But once you explicitly require it to playtest itself, take screenshots, check the visuals, and fix issues on its own, the whole development process turns into a self-propelling loop (for the full method, you can read *A Complete Beginner’s Guide to Loop Engineering* in the practical tips section of this tutorial series).



## AI’s Execution Process

You’re probably also curious: could it be that AI searched online for the original game’s source code and just copied and modified it a bit?

Come on, let me show you what actually happened.

AI searched for the original game’s mechanics and visual style, then wrote more than 5,000 lines of code entirely from scratch. All graphical assets were drawn in code.

![](https://pic.yupi.icu/1/image-20260730221935982.png)

After that, AI opened the browser by itself to run the game, checked the results through screenshots, and even wrote a bot to playtest its own game. Then it realized the difficulty was way too high and the game wasn’t actually playable, so it located the problems and spent several hours fixing and tuning them before finally delivering the product.

![](https://pic.yupi.icu/1/image-20260730222246277.png)

That’s the terrifying engineering capability of Opus 5. It may be a bit slow, but the whole process required zero time from me. I literally went to sleep and woke up to a finished game.

![](https://pic.yupi.icu/1/image-20260730222754659.png)

The first round of conversation delivered a 3-floor dungeon version. After that, I opened a new conversation and asked AI to expand the game further, still requiring it to test and verify everything autonomously and deliver a finished product directly.

![](https://pic.yupi.icu/1/image-20260801105224986.png)

When I woke up, AI had completed the task and expanded the game to 12 dungeon floors, 13 bosses, and 55 items. Excited heart, trembling hands—let’s go play it.

![](https://pic.yupi.icu/1/image-20260801105258287.png)

It’s still not on the same level as the original game, but for AI to independently reach this level of completion really exceeded my expectations. I personally played it for half an hour and couldn’t stop.

![](https://pic.yupi.icu/1/image-20260801105325549.png)



## Tech Stack

The tech-stack choices in this project are very interesting, because almost every one of them was forced by the requirements rather than chosen arbitrarily.

| Choice | Reason |
|---|---|
| Native Canvas 2D with a handwritten game loop | The requirements said all assets had to be drawn in code. Procedural drawing was the core workload, and a game framework would only add size without really helping |
| Vanilla JavaScript with no build step | The deliverable had to be directly playable in the browser, using plain `<script>` tags rather than ES modules, so `index.html` could be opened by double-clicking |
| Fixed 900×540 logical resolution + CSS scaling adaptation | It matches the room proportions of the original game, so all coordinates can be hardcoded without resolution-independent logic |
| `mulberry32` seeded random number generator | The same seed can reproduce an entire dungeon floor, which is essential for testing and bug reproduction |
| Procedurally synthesized sound effects with WebAudio | Also to avoid external resources: shooting, taking damage, dying, pickup sounds, and boss roars are all synthesized in real time |
| Python Playwright + in-page debugging interface | Uses real keyboard and real touch input, combined with assertable game state for automation |

The code structure is also very clear, split into several files by responsibility:

```plain
js/util.js      常量、数学、播种随机、粒子系统、屏幕震动、程序化音效
js/art.js       全部程序化绘图（2513 行，是最大的一个文件）
js/dungeon.js   楼层平面生成 + 12 层章节表 + 13 种房间布局
js/items.js     55 件道具及各自的程序化图标和效果
js/entities.js  玩家、眼泪模板、11 种敌人 AI、13 个 Boss 状态机
js/game.js      状态机、房间生命周期、碰撞、掉落、HUD、小地图、商店
js/main.js      输入、缩放适配、界面流程、调试接口
test/           自动化测试
```

The game itself is 7,921 lines, of which procedural drawing alone takes 2,513 lines. That ratio says a lot: **when all the assets must be drawn in code, drawing becomes the main workload.** The test code adds another 1,604 lines.



## AI Autonomously Iterated for 4 Rounds

Earlier, I said AI “kept adjusting things for several hours.” So what exactly was it doing during that time?

I went through the development report AI left behind. In total, it autonomously iterated through 4 rounds, and each round had something worth learning from.



### Round 1: Get the Full Pipeline Running First, Then Get Rejected by Screenshots

AI didn’t build features one by one. Instead, it assembled the full skeleton in one go, then immediately wrote a test script to drive the entire thing from start to finish.

The result was that on the first run, all 52 assertions passed, there were no console errors, and the frame rate hit 106fps. Movement, shooting, enemy HP loss, clearing rooms to open doors, room transitions, item effects, the boss state machine, death, and victory screens all ran end to end on the first attempt.

But after checking screenshots, it found a whole pile of visual problems: the boss was too small and almost the same size as normal enemies, while also blending into the floor; an open door looked like a pure black rectangle, as if the scene had a hole punched in it; rocks were flat pentagons; the floor looked too much like a checkerboard and obviously felt procedurally drawn; and when the character faced upward, the back of his head looked like a featureless white egg.

The biggest lesson from this round is: **all-green assertions do not mean the game looks good.** Logical correctness and visual correctness are two different things. The former can be asserted by AI, but the latter still needs screenshots and human eyes.



### Round 2: Fix Hit Feedback and Remove Hidden Coupling Along the Way

In the second round, more screenshot review uncovered several feel-related problems. The most typical one was that when the player took damage, a giant pink circle covered the whole body because the game used a blended solid ellipse. The fix was to replace “cover the whole body with a color blob” with “a red outline that fits the character shape + outer glow + a very low-opacity overlay.”

There was also a technical detail here that’s really worth learning. After AI globally increased the size of five enemy types, it found that their faces and bodies no longer matched, because the offsets for facial features had been hardcoded based on the old radius. Its solution was to introduce a unified scaling function: **draw at a fixed reference radius first, then scale the whole thing.** That way, later adjustments to collision radius won’t break the proportions again.

This kind of problem is very typical. AI often leaves behind this sort of hidden coupling in code, and once you change one number, everything collapses. Asking it to abstract one extra layer is much more cost-effective than waiting for the bug to happen and then manually patching it every time.



### Round 3: Let a Robot Playtest for You — This Was the Most Valuable Round

Screenshots can prove whether something “looks good,” but they can’t prove whether it’s actually fun to play.

So in this round, AI wrote an in-page bot that controlled the game only through the exact same input interfaces as a human player, then ran multiple cheat-free playthroughs.

On the first bot playtest, all 6 runs died violently in the second room within 20 to 34 seconds, averaging only 2.7 kills.

**A game with all-green assertions was, in practice, completely unplayable.**

The most critical reason was that knockback was fake. The code applied a velocity impulse when hit, but the movement logic was pulling speed back toward the target value every frame, canceling the impulse within two frames. The result was that once invincibility frames ended, the enemy was still stuck to the player and immediately landed another hit, creating a death spiral. The fix was to add 0.2 seconds of hard stun during which player input could not take over movement. AI also added a 0.55-second spawn protection window for enemies so they couldn’t deal unavoidable damage the instant a door opened, plus a spawn-in animation so the player could read what was happening. It also added hit stop (a few frozen frames on impact). That change is cheap, but the “I landed the hit” feeling depends heavily on it.

On the second bot playtest, the bot no longer died immediately, but all 6 runs got stuck in the same room and stopped moving. After dumping state logs frame by frame, it found two real bugs: room-clear rewards could fall into pits and become permanently unreachable (because rewards always spawned at the room center, and that pit layout happened to occupy that exact tile), and diagonal gaps in the pit pattern were only 9.5 pixels wide, so if the player squeezed in, the collision normals canceled each other and the character got stuck.

There was also a third problem that was especially representative: **the bot itself also had a bug**. Its four-direction shooting could only hit if it aligned on one axis first, but it kept firing diagonally. If you didn’t investigate that, you might think the problem was game difficulty and keep weakening enemies more and more, only to drift farther from the real issue. Your test tool itself can be wrong.

On the third bot playtest, there were 0 deadlocks, but still 0 boss kills. After tagging all sources of damage, the conclusion was very clean: each run cleared 4 to 5 normal rooms, only lost 3 to 4 HP along the way, and then died to the boss, with 90% of damage coming from the boss’s contact damage.

That meant the normal-room difficulty had already been tuned well—the problem was 100% in the boss fights. So AI made a series of fairness adjustments, the most important being: **the boss’s body only deals damage when it is actually lunging.** Standing next to an idle boss no longer continuously drains your HP. That’s also closer to the original game, where the threat should come from attacks with telegraphing, not just touching the boss’s sprite.

This round also exposed a trap in the testing method itself. I was running 7 Agents simultaneously on my local machine, so the page couldn’t maintain 60fps. In the worst case, 905 seconds of wall-clock time only advanced 8.3 seconds of in-game time, meaning 8 runs took 90 minutes, and most of them were cut off by timeout rather than actually lost. The fix was to budget tests by in-game time instead of wall-clock time, and to write a separate script that directly dropped the bot into a boss room, which could determine boss-fight winnability in 80 seconds.



### Round 4: Real Mobile Viewport Recheck

In the final round, AI took screenshots in a mobile viewport and found that the canvas was compressed and cropped, showing only a small portion of the room.

The reason was that the container holding the canvas was a flex child. Its fixed width of 900px got squeezed by flex inside a 414px viewport, then scaled again, causing overflow to be cropped. On desktop, because the viewport was wider than 900px, the issue never appeared, so none of the previous tests caught it.

After fixing it, AI added two regression assertions: the canvas size must equal the proportional scaling value, and the canvas must fit fully within the viewport.

**Add an assertion every time you fix a bug—this is the key habit for having AI maintain a project over the long term.**



## How to Verify That AI Wrote It Correctly

In the end, the full validation approach solidified into 6 layers, and I think this is the most worth copying from the entire project:

1. Structural smoke tests: 11 checks to confirm the file structure and entry points are correct
2. Functional assertion tests: 70 checks using real keyboard and real touch input to drive the page, covering movement, shooting, room clearing, item stacking, boss fights, death/victory, mobile touch, dungeon generation robustness, performance, and more
3. Boss fight winnability tests: 13 bosses tested one by one in live combat, with 10 ultimately killed and all 13 brought below 78% HP
4. Full-playthrough bot testing: push through real multi-floor dungeon runs to check for deadlocks and errors
5. Difficulty calibration: measure DPS curves per floor and use them to fit the HP growth curve
6. Art review: generate one screenshot per floor and per boss, then inspect manually

Among these, point 5 is especially worth talking about. Player output grows multiplicatively—each item adds to or multiplies the result of the previous one. In real tests, the bot’s DPS increased by roughly 20x from Floor 1 to Floor 12. So enemy HP also had to scale multiplicatively; otherwise late-game bosses would melt in seconds. In the first version, which used linear scaling, the Floor 12 boss survived only 5.9 seconds.

The final growth exponent was fitted from the real measured DPS curve—not chosen by gut feeling. In the past, this kind of work required a dedicated balancing designer. Now AI can calculate it after a few rounds of testing.



## One-Sentence Deployment

Once the game was done, I wanted everyone to be able to play it. What should I do?

I just had to say one more sentence to AI and let it use EdgeOne Makers’ website deployment skill to launch it directly.

![](https://pic.yupi.icu/1/image-20260801105431134.png)

AI handled it quickly, and it can even bind your own custom domain.

![](https://pic.yupi.icu/1/image-20260801105408341.png)

Alright—now everyone can play.

![](https://pic.yupi.icu/1/image-20260801110429404.png)

If you want to learn more deployment methods, you can read *Project Deployment Tutorial* in this section of the course.



## One-Sentence Open Sourcing

Still not done. What if I want more people to help me expand the game together?

Again, I only need to say one sentence to AI—ask it to generate a project introduction document with screenshots, and use the GitHub MCP extension to fully open-source the code directly.

![](https://pic.yupi.icu/1/image-20260801105508040.png)

Done. Now everyone can take it and build on it.

![](https://pic.yupi.icu/1/image-20260801105554475.png)

From development to testing to deployment to open sourcing, I never left the chat window even once.



## What You’ll Gain from This Project

This project is suitable for people who can already use AI to build simple webpages and want to challenge more complex projects. If you follow along and finish it, you’ll gain:

- how to use the mindset of Loop Engineering to let AI iterate autonomously instead of manually directing every single step
- why “all assertions green” does not mean “it’s correct,” and why logical validation and visual validation require different methods
- how to use automated testing bots to verify interaction effects, an approach that can be transferred to any project requiring real operational validation
- why it’s more cost-effective to make AI abstract away hidden coupling than to patch problems manually every time they appear
- an appreciation that AI can now even handle background research, such as reconstructing the original dungeon-generation algorithm
- a complete end-to-end workflow from development to deployment to open sourcing

Let me add one more note about background research. The dungeon-generation algorithm in this project is a true recreation of the original game’s real algorithm. Through web search, AI found reverse-engineering analyses of the original source code and then implemented it 1:1. One of the rules is especially clever: if a candidate grid cell already has more than 1 filled neighbor, generation is rejected. That rule is exactly why the original game’s dungeons have “corridors but no loops.”

This kind of work used to require digging through wikis and forums yourself. Now you can just hand it to AI with web search.



## How Much Did It Cost?

Finally, let’s reveal the cost of developing this game: it was a bit over 400 RMB. Do you think that’s expensive?

If this were the old days and I hired a programmer to make it, it would easily cost tens of thousands at minimum, and probably take more than a month.

That said, Opus 5 really is expensive. Not every task needs a model at this level, so everyone should still choose the right model based on the specific job.

![7 个大模型的选择建议一览](https://pic.yupi.icu/1/01_7%E4%B8%AA%E5%A4%A7%E6%A8%A1%E5%9E%8B%E7%9A%84%E9%80%89%E6%8B%A9%E5%BB%BA%E8%AE%AE%E4%B8%80%E8%A7%88_compressed_v3.png)

In simple terms: give 90-point-quality tasks to Opus 5; give 80-point tasks to GPT, Kimi K3, GLM-5, and similar models; and use the extremely cost-effective DeepSeek for tasks where “passing grade is enough.” For a more detailed selection method, you can read *AI Model Selection Guide* in the programming tools section of this tutorial series.



## Final Thoughts

Playing a game I made myself really stirred up a lot of emotions.

![](https://pic.yupi.icu/1/image-20260801111112520.png)

Something I most wanted to do as a child has finally become reality. To be honest, it’s not that I became stronger—AI became stronger.

But what I want to emphasize is that this project wasn’t simply “say one sentence and let AI make a game.” What turned it from a toy into a product was every verification step in those 4 rounds of iteration: screenshot review to catch visual issues, bot playtesting to catch playability issues, DPS calibration to catch balance issues, and real-device viewport checks to catch adaptation issues.

**AI is responsible for writing; you are responsible for designing how to verify.** That may be the core division of labor in Vibe Coding at this stage.

And to be honest, if I spent a little more time, I could absolutely use AI to polish it into a commercial-grade product—maybe even one where you couldn’t tell it was AI-made. So at this point, stop thinking AI can’t handle complex projects.

![](https://pic.yupi.icu/1/image-20260801110514866.png)

I’m sure everyone has something they’ve always wanted to build but never could—whether it’s a product, a game, or a tool to improve your own efficiency. Now you really can try boldly.

Don’t chase perfection right from the start. First get the smallest working path running, then design the right validation methods, and let AI iterate round after round.

If you want to learn more about the model capabilities used in this development, you can read *Real-World Claude Opus 5 Coding Capability Test - 7 Project Case Studies* in the model updates section of this tutorial series. This game was one of those 7 test projects.
