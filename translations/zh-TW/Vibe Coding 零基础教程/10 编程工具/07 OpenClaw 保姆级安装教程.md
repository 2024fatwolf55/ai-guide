# OpenClaw 保姆級安裝教程

> OpenClaw 安裝 + 接入 QQ 對話，傻瓜式教程



你好，我是魚皮。

在前面的文章中，我們學習了 AI 程式碼編輯器、命令列程式設計工具、IDE 外掛等各種 AI 程式設計工具。這些工具的定位都是幫你寫程式碼、做專案，但有一類工具更特殊 —— 它不只是程式設計助手，而是一個能操作你電腦的 AI 數字員工。

最近特別流行養龍蝦，不是真的龍蝦，而是一個叫 OpenClaw 的 AI 智慧助手。

![](https://pic.yupi.icu/1/openclaw%E7%8E%B0%E8%B1%A1.jpg)

你可以把它理解成一個住在你電腦裡的 AI 員工，它不像普通的 AI 聊天機器人只能動嘴皮子，而是真的能幫你幹活，讀寫檔案、操作瀏覽器、執行命令、甚至搭建網站，通通不在話下。

![](https://pic.yupi.icu/1/image-20260310160613289.png)

OpenClaw 的火爆程度遠超我的想象，從 2025 年 11 月上線，僅用了大約 120 天就登頂 GitHub 星標 **歷史第一**，累計拿下 29 萬+ Stars，超過了 Linux、React 等一眾前輩！

![](https://pic.yupi.icu/1/image-20260310161116303.png)

本來以為只是個技術圈的玩意兒，結果竟然火出圈了！

國內出現了幾百塊的上門代裝服務，你沒聽錯，**上門幫你裝一個開源軟體，收費幾百**。

![](https://pic.yupi.icu/1/openclaw_setup_ondoor.jpeg)

更離譜的是，深圳騰訊大廈門口還搞了免費的線下 “裝龍蝦” 活動，近千人排隊，四年級小學生、快 70 歲的老大爺都來了，場面跟老年人排隊領雞蛋似的。

![](https://pic.yupi.icu/1/openclaw%E4%B8%8A%E9%97%A8%E5%AE%89%E8%A3%85%E6%9C%8D%E5%8A%A1.jpeg)

但我總覺著吧，如果這玩意需要讓別人操作你的電腦幫你安裝，大機率你也不需要這玩意，裝上後你也不會用。

實際上，在自己電腦上安裝 OpenClaw 非常簡單，魚皮今天就提供一個《保姆級 OpenClaw 本地安裝 + 接入 QQ 教程》，哪怕你完全沒學過程式設計，只要跟著做，也能成功養蝦 🦞~

建議收藏，我們開始。

⭐️ 推薦觀看影片教程：https://www.bilibili.com/video/BV1D4wcz6EVV

> 注意，本文主要是照顧零基礎的新手，不會講解複雜的玩法。之前魚皮已經分享過 [《OpenClaw 保姆級部署到雲伺服器的教程》](https://mp.weixin.qq.com/s/DZYc92rLzhX95L6OBEQUyQ)，以及 [《利用 OpenClaw 打造能在手機 QQ 上對話的 AI 伴侶》](https://mp.weixin.qq.com/s/GSwZE74o5-wq0_UOXL8AyA)，感興趣的朋友可以按需學習。



## 開始前的準備

在安裝之前，你只需要準備 2 樣東西：

1. 10 分鐘的時間
2. 一臺能開機上網的電腦（Windows 就行，Mac 更好，有條件的話建議用虛擬機器 / 備用機 / 雲伺服器，**一定要注意安全！！！**）

其他的，什麼都不需要！

**不需要你會程式設計，不需要你有計算機基礎，甚至不需要 1 分錢！**



## 安裝教程大綱

整個安裝過程分為 4 步：

1. 安裝執行環境
2. 安裝配置 OpenClaw
3. 接入 QQ 手機對話
4. 解除安裝

考慮到有些同學安裝完 OpenClaw 後不知道怎麼用、想要徹底清理掉，魚皮連解除安裝都給大家講解，夠貼心吧？



## 一、安裝執行環境

開啟 [OpenClaw 官網](https://openclaw.ai/)，你會看到官方提供了一行命令來安裝。

![](https://pic.yupi.icu/1/image-20260310161617619.png)

**如果你是 Mac / Linux 使用者**，可以直接開啟終端（按 `Command + 空格` 搜尋 “終端” 開啟），貼上下面這行命令並回車：

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

這行命令會自動幫你安裝所有依賴和 OpenClaw 本體，一步到位，裝完就可以直接跳到 **第二步 - 安裝配置 OpenClaw**。

![](https://pic.yupi.icu/1/image-20260310161704012.png)

**但如果你是 Windows 使用者，千萬不要直接執行一行命令安裝！失敗率極高！！！**

魚皮實測了多種安裝方式，踩了不少坑，下面手把手帶你走一遍 Windows 上最穩的安裝方式。



### 1、安裝 Node.js

首先，我們需要安裝 Node.js。

什麼是 Node.js？

你可以把它理解成 OpenClaw 的 “發動機”，OpenClaw 是用 JavaScript 語言寫的，而 Node.js 就是讓 JavaScript 在你電腦上跑起來的執行環境。沒有它，OpenClaw 就啟動不了。

開啟 [Node.js 官網](https://nodejs.org/)，選擇對應你作業系統的安裝包，並執行下載。注意版本號 **至少選 22 以上**，低於這個版本就會逮蝦失敗。

![](https://pic.yupi.icu/1/image-20260310144506886.png)

下載完成後，執行安裝包，什麼都不用改，一路點選下一步就好：

![](https://pic.yupi.icu/1/image-20260310144530251.png)

安裝 Node.js 成功後，會自動附帶安裝一個叫 npm 的工具，它是 Node.js 的應用商店，後面我們要用它來安裝 OpenClaw。



### 2、安裝 Git

接下來，安裝 Git。

Git 是一個程式碼版本管理工具，OpenClaw 在安裝過程中需要用它從網上下載一些依賴包。

你不需要學會怎麼用 Git，只需要把它裝上就行。

開啟 [Git 官網](https://git-scm.com/downloads/win)，下載 Windows 版本的安裝包：

![](https://pic.yupi.icu/1/image-20260310144749069.png)

同樣，執行安裝包，一路點選下一步，全都選擇預設配置就好：

![](https://pic.yupi.icu/1/image-20260310144843659.png)



### 3、安裝 OpenClaw

環境準備就緒，現在來安裝 OpenClaw 本體。

首先，以管理員身份開啟 PowerShell。PowerShell 是 Windows 自帶的命令列工具，相當於 Mac / Linux 系統的終端。

在電腦的搜尋欄中輸入 "PowerShell"，右鍵選擇 **以管理員身份執行**：

![](https://pic.yupi.icu/1/image-20260310144953360.png)

先試試官方提供的一鍵安裝命令：

```bash
iwr -useb https://openclaw.ai/install.ps1 | iex
```

大機率你會跟魚皮一樣，直接報錯，提示缺少執行指令碼的許可權：

![](https://pic.yupi.icu/1/image-20260310145038140.png)

沒關係，執行下面這行命令，開啟 PowerShell 的指令碼執行許可權：

```bash
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

如果彈出確認提示，輸入 `A` 然後按回車即可。這行命令的作用是允許執行來自可信來源的指令碼，類似手機上允許安裝第三方應用。

![](https://pic.yupi.icu/1/image-20260310145148127.png)

然後重新執行一鍵安裝命令，運氣好的話能直接成功。但像我這種倒黴蛋子，安裝過程中又報錯了！

![](https://pic.yupi.icu/1/image-20260310145208509.png)

報錯資訊顯示是 npm 安裝失敗，那我們手動輸入 npm 命令來安裝試試：

```bash
npm install -g openclaw
```

![](https://pic.yupi.icu/1/image-20260310145316319.png)

果不其然也報錯了，因為一鍵安裝指令碼預設就是用 npm 來裝的，根本原因一樣。

![](https://pic.yupi.icu/1/image-20260310145349762.png)

別慌，其實換一個包管理工具就行，用 pnpm 來安裝。

pnpm 和 npm 類似，也是一個軟體商店，但它的相容性更好、安裝速度也更快。

先用 npm 全域性安裝 pnpm，輸入命令：

```bash
npm install -g pnpm
```

安裝完成後，檢查一下 pnpm 的版本號，確認安裝成功：

```bash
pnpm -v
```

![](https://pic.yupi.icu/1/image-20260310145555384.png)

然後執行 `pnpm setup`，這個命令會自動配置 pnpm 的全域性安裝路徑，讓你之後透過 pnpm 安裝的工具能在任何地方直接使用：

![](https://pic.yupi.icu/1/image-20260310145624520.png)

注意！執行完 `pnpm setup` 後，**一定要關閉當前 PowerShell 視窗，重新以管理員身份開啟一個新的**。 這是為了讓剛才配置的環境變數生效。

在新的 PowerShell 視窗中，用 pnpm 來安裝 OpenClaw：

```powershell
pnpm add -g openclaw@latest
```

![](https://pic.yupi.icu/1/image-20260310145706609.png)

等待一段時間後，安裝成功！但你可能會看到一條提示，說忽略了一些包的構建指令碼（Ignored build scripts）：

![](https://pic.yupi.icu/1/image-20260310145800342.png)

這是因為 pnpm 出於安全考慮，預設不會自動執行第三方包的構建指令碼，需要你手動批准。

按照 OpenClaw 官方的指引，需要執行下面這條命令，來批准這些構建指令碼：

```bash
pnpm approve-builds -g
```

![](https://pic.yupi.icu/1/image-20260310145842863.png)

不過執行這條命令可能會報錯：

![](https://pic.yupi.icu/1/image-20260310145930863.png)

魚皮在網上搜了一大圈解決方案，也沒能解決這個問題，期待官方後續修復。但好訊息是，**這行命令不執行也幾乎不影響正常使用**，直接忽略就行。

最後，驗證一下 OpenClaw 是否安裝成功，執行：

```bash
openclaw -v
```

能夠看到版本號，表示大功告成！

![](https://pic.yupi.icu/1/image-20260310143618461.png)



## 二、安裝配置 OpenClaw

環境裝好了，接下來進入 OpenClaw 的新手載入程式，定製你的小龍蝦 🦞。

在 PowerShell（Windows 系統）或終端（Mac / Linux 系統）中執行下列命令：

```bash
openclaw onboard --install-daemon
```

`onboard` 就是新手引導的意思，`--install-daemon` 是指 “順便把後臺服務也裝上”，讓 OpenClaw 在後臺持續執行，關掉終端也不會停。

執行後，會進入一個互動式載入程式，一步步帶你完成配置。

![](https://pic.yupi.icu/1/image-20260310150045929.png)

首先會彈出一個使用協議，需要你確認同意。

![](https://pic.yupi.icu/1/image-20260310150214119.png)

這裡提醒一下，OpenClaw 是一個能操作你電腦的 AI 工具，理論上它可以執行任何終端命令，包括刪除檔案之類的敏感操作。**所以建議有條件的話在虛擬機器或備用機裡玩耍**，避免誤操作影響到重要資料。

確認沒問題，就選 Yes 進入下一步。



### 1、選擇安裝模式

載入程式會問你選擇 Quickstart（快速開始）還是 Manual（人工）。

建議新手直接選 Quickstart，它會幫你用預設配置快速搞定，人工模式適合有一定養蝦經驗的同學。

![](https://pic.yupi.icu/1/image-20260310150255760.png)



### 2、配置 AI 大模型

這是最重要的一步，你要告訴 OpenClaw 用哪個 AI 大模型來思考，也就是給龍蝦選腦子。

載入程式會列出一些 AI 平臺供你選擇，比如 Anthropic（Claude）、OpenAI（GPT）、Qwen（通義千問）等。

魚皮推薦新手選擇 Qwen，因為它支援 OAuth 授權登入，會自動彈出網頁讓你掃碼驗證，不用手動去申請和填寫 API Key，而且可以直接免費使用。缺點是呼叫太頻繁可能會被限流，所以只適合快速上手體驗。

![](https://pic.yupi.icu/1/image-20260310150423382.png)

選擇 Qwen 後，載入程式會自動開啟瀏覽器讓你登入授權：

![](https://pic.yupi.icu/1/image-20260310150610423.png)

完成登入授權後，選擇預設的程式設計大模型：

![](https://pic.yupi.icu/1/image-20260310150731894.png)

當然，你也可以選擇其他大模型平臺。如果你想了解各模型在 OpenClaw 場景下的實際表現，可以參考 [PinchBench](https://pinchbench.com/) 排行榜，這是一個專門測試大模型做 OpenClaw 任務的評測網站。目前成功率最高的是 Claude Opus 4.8（成功率 82.5%），最便宜的是 Google 的 gemini-2.5-flash-lite（每次任務只要 1 毛錢）。

![](https://pic.yupi.icu/1/image-20260310164932093.png)

不太建議新手一上來就用國外大模型來玩 OpenClaw，價格非常貴，尤其是你讓 AI 幹複雜的活時，Tokens 會燒得嘎嘎猛，要做好心理準備。國產的智譜、Kimi 也是不錯的選擇。



### 3、配置聊天渠道

載入程式會問你要不要連線 Telegram、WhatsApp、Discord、飛書等聊天平臺，更方便地跟龍蝦對話。

建議直接跳過，我們先用網頁介面聊天就好，後面手動接入 QQ 其實更方便。

![](https://pic.yupi.icu/1/image-20260310150813561.png)

接下來還會問你要不要配置搜尋服務提供者（比如 Brave Search），也建議先跳過，這些都需要額外申請 API Key，後面有需要再配：

![](https://pic.yupi.icu/1/image-20260310150917416.png)



### 4、安裝 Skills 技能包

Skills 是給 AI 裝的能力擴充套件包。OpenClaw 本身只是一個框架，裝了 Skills 之後 AI 才能解鎖各種具體的能力，比如搜尋網頁、操作瀏覽器、製作 PPT 等。

先開啟技能配置：

![](https://pic.yupi.icu/1/image-20260310150959049.png)

然後載入程式會列出一些推薦的技能包，這裡建議至少新增 **ClawHub** 這一個。ClawHub 是 OpenClaw 的官方技能市場，裝了它之後，你的小龍蝦就可以隨時搜尋和安裝社群裡上千個技能包，快速擴充套件自己的能力，非常方便。其他的技能按需選擇即可。

![](https://pic.yupi.icu/1/image-20260310151036714.png)

選擇完技能後，還要選擇安裝技能的工具，用 npm 就行：

![](https://pic.yupi.icu/1/image-20260310151118779.png)

之後還會詢問一些額外服務的配置，比如是否要配置 AI 生圖大模型等，新手直接無腦全部選 No：

![](https://pic.yupi.icu/1/image-20260310151157689.png)



### 5、啟動閘道器服務

接下來會自動安裝並啟動 OpenClaw 的 Gateway 閘道器服務。你可以把閘道器理解成 OpenClaw 的總排程中心，它負責接收你從各個渠道（網頁、QQ、飛書等）發來的訊息，分配給 AI 處理，再把結果返回給你。

![](https://pic.yupi.icu/1/image-20260310151301625.png)

這時候 Windows 可能會彈出防火牆提示，問你是否允許公共網路和專用網路訪問，**一定要點允許！** 否則閘道器服務無法正常工作。

![](https://pic.yupi.icu/1/image-20260310151324961.png)

啟動成功後，載入程式會問你是在終端介面（TUI）還是網頁瀏覽器中使用 OpenClaw。

TUI 就是直接在命令列裡跟 AI 聊天，適合喜歡敲命令、有一定程式設計基礎的同學。新手當然選 Web UI 網頁中使用：

![](https://pic.yupi.icu/1/image-20260310151428919.png)



### 開始使用

選擇之後，瀏覽器會自動開啟 OpenClaw 的網頁控制面板。恭喜，你的龍蝦 1 號準備就緒！

先跟它打個招呼吧，問問它是誰。它還會主動引導你透過對話來設定身份、職責等個性化資訊：

![](https://pic.yupi.icu/1/image-20260310151625528.png)

OpenClaw 內建了很多工具，比如檔案讀寫、終端命令執行、網頁搜尋等。

試試讓它幫你讀取電腦上的檔案，比如檢視下載目錄裡有什麼：

![](https://pic.yupi.icu/1/image-20260310151946903.png)

不過說實話，每次都要開啟電腦上的網頁控制面板才能跟 AI 對話，還是不夠方便。所以接下來，我們要把 OpenClaw 接入 QQ 機器人，目標是能夠隨時隨地用手機養蝦~



## 三、接入 QQ 手機對話

以前想把 OpenClaw 接入 QQ，需要自己到 QQ 機器人開放平臺申請、開白名單、獲取金鑰，還是有點兒麻煩的。

現在騰訊出手，專門為 OpenClaw 搞了一個快捷接入通道，幾步就能搞定！

開啟 [QQ 機器人 OpenClaw 接入頁面](https://q.qq.com/qqbot/openclaw/index.html)，用 QQ 掃碼登入：

> 指路：https://q.qq.com/qqbot/openclaw/index.html

![](https://pic.yupi.icu/1/image-20260310152123827.png)

點選「建立機器人」，直接秒出！

![](https://pic.yupi.icu/1/image-20260310152325274.png)

建立完成後，手機 QQ 立刻就會收到小龍蝦打招呼的訊息：

![](https://pic.yupi.icu/1/image-20260310153005879.png)

然後可以修改機器人的頭像、暱稱等資訊，給你的龍蝦起個好聽的名字吧~

![](https://pic.yupi.icu/1/image-20260310152409339.png)

接下來是最關鍵的一步。頁面上會顯示三條配置命令，你只需要 **依次複製這 3 條命令到終端（PowerShell）中執行** 就可以了。

注意命令中包含你的金鑰資訊，不要洩露給別人！

![](https://pic.yupi.icu/1/image-20260310152443829.png)

到終端中依次執行命令：

![](https://pic.yupi.icu/1/image-20260310152544861.png)

接入成功後，你可以在 OpenClaw 的網頁控制檯的「頻道」（Channels）板塊看到已經接入了 QQ 機器人渠道：

![](https://pic.yupi.icu/1/image-20260310152846134.png)

現在，掏出手機試試吧！

直接在 QQ 上給小龍蝦發訊息下達任務，比如讓它檢視電腦配置、或者幫你寫一篇文章。完成速度很快，而且支援 Markdown 格式輸出，閱讀體驗不錯：

![](https://pic.yupi.icu/1/image-20260310153115908.png)

如果你好奇它背後做了些什麼，可以在 OpenClaw 的網頁控制檯中檢視跟 QQ 機器人的完整對話記錄。接入 QQ 機器人頻道後，OpenClaw 能夠理解怎麼透過 QQ 傳送圖片、語音等內容：

![](https://pic.yupi.icu/1/image-20260310152754120.png)

除了基本對話和操作電腦之外，你還可以探索更多玩法。比如看魚皮之前寫的 [《GLM-5 + OpenClaw：打造你的 AI 伴侶》](https://mp.weixin.qq.com/s/GSwZE74o5-wq0_UOXL8AyA)，教你打造一個能發圖片、發語音、甚至幫你幹活的 AI 伴侶。還可以看 [《OpenClaw 保姆級部署教程》](https://mp.weixin.qq.com/s/DZYc92rLzhX95L6OBEQUyQ)，把 OpenClaw 部署到雲伺服器上 7 x 24 小時不間斷執行。

當然，我估計更多同學折騰一下之後，就會心生退意：**我要，這龍蝦有何用？！**

沒錯，你可能根本不需要 OpenClaw。

所以，接下來保姆皮還會教大家怎麼解除安裝 OpenClaw，把它刪的乾乾淨淨，蝦皮都不剩。



## 四、解除安裝

其實只需要執行一行命令，就能解除安裝 OpenClaw 了：

```bash
openclaw uninstall
```

但是要注意觀察執行命令後的輸出結果，有些內容可能不會自動刪除：

![](https://pic.yupi.icu/1/image-20260307105935932.png)

如果你想確保解除安裝得乾乾淨淨，直接複製下面對應你作業系統的所有命令，一把執行即可。

Mac / Linux 使用者：

```bash
openclaw gateway stop
openclaw gateway uninstall
rm -rf "${OPENCLAW_STATE_DIR:-$HOME/.openclaw}"
npm rm -g openclaw || pnpm remove -g openclaw
rm -rf /Applications/OpenClaw.app
```

Windows 使用者（在 PowerShell 中執行）：

```powershell
openclaw gateway stop
openclaw gateway uninstall
schtasks /Delete /F /TN "OpenClaw Gateway"
Remove-Item -Recurse -Force "$env:USERPROFILE\.openclaw"
Remove-Item -Force "$env:USERPROFILE\.openclaw\gateway.cmd" -ErrorAction SilentlyContinue
npm rm -g openclaw
# 如果你是用 pnpm 安裝的，改為執行：pnpm remove -g openclaw
```

這一梭子命令執行完，彷彿什麼都沒發生過。



## 寫在最後

OpenClaw 確實是一個很酷的專案，它把使用者操作 AI 智慧體的入口變成了你日常使用的手機聊天軟體，讓 AI 無縫融入你已有的溝通習慣。現在各家也都在搶佔 AI 入口，想方設法離使用者更近。

但是 OpenClaw 雖好，也要用在正地。

我看到很多人在吹 “用手機遠端操控 AI 辦公”，但說實話，有多少人真的需要呢？

當你放鬆拿起手機的時候，你是想指揮 AI 辦公，還是想刷個影片、看看朋友圈？

如果只是為了嚐鮮裝一個，最後的結局大機率是吃灰解除安裝。

而且如果你在電腦前工作，自動化的需求完全可以透過 AI 程式設計工具（比如 Claude Code / Cursor）或者 AI 桌面端助手來實現，比 OpenClaw 更簡單直接，還不用自己折騰環境、配置 API Key，開箱即用。**比起追熱點裝一個用不上的工具，不如想想怎麼用 AI 強化最佳化自己的工作流。** 找到真正能提升你效率的 AI 工具，堅持用起來，才是正道。

我覺得 OpenClaw 更適合想提高工作效率的職場商務人士，或者是喜歡折騰、想深度自定義 AI 行為的技術愛好者，不是人人都能養出比大廠專業團隊封裝地更好的龍蝦的。很快各家也會推出自己的 OpenClaw，哦不，已經來了。

當然，我也會持續關注 OpenClaw 的發展，探索更多提高效率的玩法。

到這裡，我們已經學完了主流 AI 程式設計工具的全部型別。在下一篇文章中，我會介紹 AI 輔助工具集，包括版本管理、專案部署等工具，幫你完善整個開發工具鏈。

加油！



## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)
