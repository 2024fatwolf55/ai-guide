# VSCode + GitHub Copilot：微軟全家桶的 AI 程式設計實戰

> 從安裝到實戰，手把手教你用 VSCode + GitHub Copilot 進行 AI 程式設計



你好，我是程式設計師魚皮。

AI 程式設計工具現在是真的百花齊放，Cursor、Claude Code、OpenCode、…… 每隔一段時間就冒出來一個新選手。

之前我一直沉迷於 Cursor 和 Claude Code，直到最近做新專案時認真體驗了一把 GitHub Copilot， 才發現這玩意兒真夯啊！

![](https://pic.yupi.icu/1/13c2a89f183a7161be27361ce4908ed6.png)

先簡單介紹一下主角。**VSCode** 是微軟出品的全球最流行的程式碼編輯器，裝機量破億；**GitHub Copilot** 則是 GitHub 官方出品的 AI 程式設計助手外掛，直接安裝在 VSCode 中使用。

個人體驗下來，相比其他 AI 程式設計工具有 4 大優勢：

1. 支援最新 AI 大模型，Opus、GPT、Gemini、Claude 隨便切，實測程式設計質量嘎嘎好，全棧專案一把梭
2. 支援本地、後臺 CLI、雲端、Claude Code 等多種執行模式，相容性賊強
3. 支援 MCP、Skills、工具呼叫的視覺化管理，既靈活又方便，不用自己手動編寫配置了
4. 支援子智慧體、和 AI 的每一步互動都清晰可見，Agent 執行體驗巨好

啥啥啥，這都是啥？

![](https://pic.yupi.icu/1/image-20260305141036239.png)

即使你看不懂我說的這些也沒關係，這篇文章就帶大家從 0 開始上手 VSCode + GitHub Copilot，從安裝到實戰、從基礎到核心特性，一條龍服務。

乾貨密集，建議先收藏，然後沐浴更衣、找個安靜的地方放空自己，慢慢食用，助眠效果極佳~



## 安裝和配置

1）首先進入 [VSCode 官網](https://code.visualstudio.com/) 下載安裝包，直接傻瓜式安裝。

![](https://pic.yupi.icu/1/image-20260305141229310.png)

2）開啟 VSCode，點選左側「擴充套件市場」圖示，搜尋 "GitHub Copilot"，安裝官方的 AI 程式設計外掛。

![](https://pic.yupi.icu/1/image-20260305141416199.png)

你還可以根據需要，選擇安裝 Chinese 漢化外掛，適合國內的寶寶們：

![](https://pic.yupi.icu/1/image-20260305153013870.png)

3）安裝完後，點選 VSCode 底部狀態列的 Copilot 圖示，按照提示登入 GitHub 賬號就行了。

![](https://pic.yupi.icu/1/setup-copilot-status-bar.png)

如果你還沒有 Copilot 訂閱，會自動進入 **Copilot Free 免費計劃**，每月有一定的 AI 對話和程式碼補全額度，零門檻上手。想體驗完整功能的話，Copilot Pro 支援新使用者免費試用 30 天，申請一張國內銀行的 Visa 卡就能開通。

我白票了 30 天的高階會員，最近能省一點其他 AI 程式設計工具的額度了哈哈~ 🤣

到這裡，安裝配置就全部搞定了，比折騰 Claude Code 那套網路受限 + 賬號受限 + 命令列小黑框的組合拳簡單多了。

![](https://pic.yupi.icu/1/1766562559951-d1371bb9-99d3-467a-aeec-421cd12eb3bb.png)



## 基本使用

裝好之後，先來感受一下最基本的 AI 程式設計體驗。



### AI 對話

點選 VSCode 上方的「聊天按鈕」，開啟 Chat 對話面板，你就可以和 AI 愉快地聊天了。讓它分析需求、寫程式碼、改 Bug，啥都行。

![](https://pic.yupi.icu/1/image-20260305142129090.png)

對話方塊區域有一個 **智慧體選擇器**，可以在 3 種內建模式之間切換：

- Agent 全自主模式：AI 自己分析、寫程式碼、跑命令，一條龍完成任務（用的最多）
- Plan 規劃模式：AI 先出方案再動手，適合複雜任務
- Ask 純問答模式：只回答問題，不改程式碼，適合探索和學習（我用的比較少）

![](https://pic.yupi.icu/1/image-20260305142244467.png)

除了 Chat 面板，還有兩種更輕量的 AI 對話方式。

1）按 `Ctrl+I`（Mac 是 `Cmd+I`）開啟行內對話，直接在程式碼中跟 AI 互動：

![](https://pic.yupi.icu/1/image-20260305142602604.png)

2）按 `Ctrl+Shift+Alt+L`（Mac 是 `Cmd+Shift+Option+L`）開啟 Quick Chat 彈窗，適合快問快答。

![](https://pic.yupi.icu/1/image-20260305143009366.png)



### AI 程式碼補全

寫程式碼的時候，Copilot 會自動給你淺色的補全建議，按一下 `Tab` 就能接受。比如你寫了一個計算日期的函式名 plusDate，它能直接幫你把整個函式體補全出來。

![](https://pic.yupi.icu/1/image-20260305143231950.png)

更智慧的是 Next Edit Suggestions（NES），也就是「下一步編輯建議」。它不光補全當前位置的程式碼，還能預測你接下來要改哪裡！

編輯器左側會出現一個小箭頭，按 Tab 就能跳過去並應用建議。

![](https://pic.yupi.icu/1/image-20260305143512348.png)

比如你把一個類名從 `Point` 改成了 `Point3D`，它會自動建議你在下面加個 `z` 變數，這個體驗像禿嚕魚皮一般絲滑~

![](https://pic.yupi.icu/1/nes-point.png)

這兩個功能用 Cursor 的同學應該不陌生，體驗上差不多，但 Copilot 的 NES 預測精度個人感覺略勝一籌。

好了，基本功能就是這些，看到這裡，你已經超過了 70% 的同學！

接下來進入正題，AI Agent 程式設計實戰。



## AI Agent 程式設計實戰

前面的對話和程式碼補全只是開胃菜，Agent 模式才是 GitHub Copilot 的大殺器。

什麼是 Agent？

簡單來說，你給它一個需求，它會自己分析專案、制定計劃、建立檔案、寫程式碼、跑命令、裝依賴，遇到報錯還會自動修復，全程自主執行。

其實 Manus、OpenClaw、各種 AI 程式設計工具裡的 Agent 模式，本質上都是 Agent，就是 AI 自主規劃、呼叫工具、執行任務的能力。

現在各家 AI 程式設計工具都在卷 Agent 能力，比如 Cursor 可以在子 Agent 裡操作瀏覽器進行自主驗證，Claude Code 搞出了 Agent Teams 讓多個 AI 組隊協作。GitHub Copilot 也不甘示弱，除了 Agent 模式之外，也提供了各家都支援的 **Plan 模式**。先讓 AI 幫你出方案、拆步驟，確認沒問題後再動手，適合稍微複雜一點的專案，減少 AI 一上來就瞎寫導致翻車的機率。

下面我帶大家實戰一把，結合 Plan 模式 + Agent 模式做個**「AI 占卜師網站」**，使用者輸入一個問題，讓 AI 抽取塔羅牌並生成占卜解讀。



### 第一步、用 Plan 制定方案

新建一個空的專案資料夾（比如 ai-diviner），在 VSCode 中開啟該資料夾，應該會預設開啟 Chat 對話面板。

![新建專案](https://pic.yupi.icu/1/image-20260305144504583.png)

在對話區域的智慧體選擇器中選擇 Plan 模式、並選擇大模型（比如 Claude Opus），然後輸入需求：

```
幫我用 HTML + CSS + JavaScript 做一個 AI 塔羅牌占卜網站。

功能描述：
1. 使用者輸入一個問題（比如「我最近事業運如何」）
2. 點選「開始占卜」後，展示 3 張塔羅牌的翻牌動畫
3. 翻牌完成後，根據抽到的牌生成 AI 占卜解讀
4. 介面要神秘華麗，深紫色主題配金色紋理，星空背景
5. 有流暢的翻牌動畫效果
6. 響應式佈局，手機也能用
```

![Plan模式執行AI](https://pic.yupi.icu/1/image-20260305144551103.png)

選擇 Plan 模式後，AI 不會直接開始寫程式碼。

它會先研究你的需求，可能還會問你幾個問題，比如 AI 解讀是 “呼叫 AI 大模型介面” 還是 “從預設文案庫隨機生成”？

你只要像聊天一樣把自己的想法告訴 AI 就好，比如我希望呼叫 DeepSeek 大模型的 API：

![](https://pic.yupi.icu/1/image-20260305144900988.png)

如果你自己也拿不準，可以讓 AI 幫你分析不同方案的優缺點，或者交給它自主決定。

AI 理解你的需求後，會給出一份結構化的實施方案。

![](https://pic.yupi.icu/1/image-20260305145315374.png)

方案裡會列出要建立哪些檔案、每個檔案負責什麼、實現步驟的先後順序，以及怎麼驗證效果。你可以在這一步跟 AI 反覆討論、調整方案，直到滿意為止。

![](https://pic.yupi.icu/1/image-20260305145352874.png)

Plan 模式的本質是採用 4 個階段的迭代工作流：需求研究 → 問題對齊 → 方案設計 → 迭代細化。AI 會先用只讀工具深入研究你的程式碼庫，再透過互動式問答來消除歧義，最後才給出方案草稿。

其實這也是軟體開發的標準步驟。即使你不用 Copilot 內建的 Plan 模式，也可以透過提示詞引導 AI 先設計方案、人工確認後再開發執行，養成 **先想清楚再動手** 的好習慣。



### 第二步、用 Agent 執行方案

確認方案沒問題後，點選方案下方的「Start Implementation」按鈕，讓 AI 開始自動執行，直到實現方案。

![](https://pic.yupi.icu/1/image-20260305145604534.png)

執行過程中，Agent 會自動管理一個 Todos 任務列表來跟蹤進度。你可以清楚地看到 Agent 在做什麼，比如建立 `index.html`、`style.css`、`script.js` 檔案，往裡面寫程式碼，甚至可能會自動開啟終端執行命令。

![](https://pic.yupi.icu/1/image-20260305145807776.png)

如果 AI 要跑終端命令或者呼叫某些工具，會彈出確認框讓你審批，安全性有保障。

![](https://pic.yupi.icu/1/image-20260305150107141.png)

你也可以在 Agent 工作時繼續發訊息，選擇排隊等待、立即打斷、或者引導 AI 調整方向。

建議剛開始 AI 程式設計的朋友多觀察一下 AI 的工作，發現不對勁的時候趕緊人工插手，可以節約 Tokens 並避免返工。



### 第三步、檢視效果

幾分鐘後，Agent 不僅完成了開發任務，還用 Python 啟動了個 Web 伺服器，幫我執行了網站。

![](https://pic.yupi.icu/1/image-20260305150430976.png)

好傢伙，這是多一步都不想讓我做啊？照這個趨勢，早晚我得退化到 Hello World 水平。

不過我還是喜歡在 Chrome 瀏覽器中測試，複製網址到瀏覽器中開啟，然後輸入從 [DeepSeek 開放平臺](https://platform.deepseek.com/api_keys) 獲取到的大模型  API Key：

![](https://pic.yupi.icu/1/image-20260305150858949.png)

![](https://pic.yupi.icu/1/image-20260305150957888.png)

輸入一個問題，測測俺今年的愛情運勢，然後點選「開始占卜」：

![](https://pic.yupi.icu/1/image-20260305151027082.png)

三張塔羅牌依次翻開，下方出現 AI 生成的占卜解讀。深紫色的星空背景，搭配金色邊框，再加上流暢的翻牌動畫，效果還真挺唬人的。

![](https://pic.yupi.icu/1/image-20260305151413007.png)

我感覺自己也可以開一個塔羅占卜小攤兒了，應該不是錯覺。。。

![](https://pic.yupi.icu/1/image-20260305151303905.png)

如果你對頁面的某些細節不滿意，可以在內建瀏覽器中點選「元素選擇」按鈕，哪裡不爽點哪裡，然後在 Chat 框裡編寫提示詞就行，比如：

```
改為魚皮塔羅
```

![](https://pic.yupi.icu/1/image-20260305151754685.png)

Agent 會自動定位到對應的程式碼並精準修改，改完你再重新整理預覽就好。

![](https://pic.yupi.icu/1/image-20260305152037670.png)

整個過程，從寫需求到出成品，也就幾分鐘。擱以前，我要是自己從零寫這麼個帶動畫的占卜網站，怎麼著也得搞一下午。

你還可以繼續跟 AI 對話來增加功能，整個過程中一定要注意 **上下文的用量**，如果滿了 AI 可能會斷片兒失憶，開始亂改。

![](https://pic.yupi.icu/1/image-20260305152200805.png)

因此，在上下文快滿的時候，最好讓 AI 把當前專案的資訊沉澱為文件。這樣之後每次開啟新的 AI 對話方塊時，只要把歷史文件交給 AI，就能快速找回記憶。 

OK，實戰體驗完了，看到這裡你就超過了 90% 的同學！

接下來帶大家看看 GitHub Copilot 的核心特性，這些才是它真正拉開差距的地方。



## 核心特性

### Tools - 給 AI 的工具箱

Agent 之所以能自主幹活，靠的就是工具呼叫（Tool Use）。

工具就是 AI 在執行任務時可以呼叫的各種能力，比如搜尋程式碼、讀寫檔案、跑終端命令、抓取網頁內容等等。沒有工具，AI 就只能動嘴皮子教你做事；有了工具，AI 才能真正動手幫你幹活。

VSCode 給 AI 提供了三種型別的工具：

- 內建工具：開箱即用，包括程式碼搜尋、檔案讀寫、終端執行、問題診斷等常用能力
- MCP 工具：透過 MCP 協議接入的外部工具（下面會詳細講）
- 擴充套件工具：VSCode 外掛提供的工具，裝了對應外掛就自動可用

所有工具都可以透過 Chat 對話區域的「配置工具」按鈕進行視覺化管理，很方便：

![](https://pic.yupi.icu/1/image-20260305152856918.png)

你可以自由開啟或關閉工具，不需要寫任何配置檔案，比其他 AI 程式設計工具方便不少。

開啟工具後，大多數情況下 AI 會自動判斷該呼叫哪些工具。你也可以在對話中用 `#` 號手動引用特定工具，比如 `#codebase` 搜尋整個程式碼庫、`#fetch codefather.cn` 抓取某個網頁的內容、`#problems` 檢視當前專案的所有報錯。

![](https://pic.yupi.icu/1/image-20260305153343950.png)

Agent 執行終端命令時，還有一套安全審批機制。前面實戰中我們也看到了，預設會彈確認框等待人工確認；你也可以配置自動審批規則，甚至開啟終端沙箱（目前支援 macOS 和 Linux）來限制檔案和網路訪問，安全性拉滿。

![](https://pic.yupi.icu/1/image-20260305153647365.png)

還有一個實用功能叫 Tool Sets（工具集），你可以把多個相關工具打包成一組，在對話中用 `#工具集名稱` 一次性引用。

比如建立一個叫 `reader` 的工具集，包含 `codebase` 程式碼搜尋、`problems` 問題診斷、`usages` 引用查詢等只讀工具，做程式碼審查的時候就很方便。

先在對話面板的設定中開啟「工具集」，點選建立新的工具集檔案並輸入名稱：

![](https://pic.yupi.icu/1/image-20260306104630540.png)

然後會自動彈出工具集的配置檔案，新增下列程式碼並儲存即可：

```json
{
  "reader": {
    "tools": ["codebase", "problems", "usages", "search"],
    "description": "只讀工具集，適合程式碼審查",
    "icon": "book"
  }
}
```

![](https://pic.yupi.icu/1/image-20260306104906332.png)

配置好之後，在對話中輸入 `#reader` 就能一次性啟用這組只讀工具了：

![](https://pic.yupi.icu/1/image-20260306105151652.png)



### MCP - 讓 AI 連線外部能力

MCP（Model Context Protocol）是一種開放標準協議，作用是讓 AI 能夠連線外部工具和服務。你可以把它想象成給 AI 裝了一個萬能介面，透過這個介面，AI 就能運算元據庫、呼叫 API、控制瀏覽器等等。

MCP 在 AI 圈已經非常火了，各種 AI 程式設計工具都已支援。但 GitHub Copilot 在管理 MCP 的體驗上真是讓我眼前一亮，微軟竟然直接把 MCP 整合到了 VSCode 的擴充套件市場裡！

你只需要開啟 VSCode 擴充套件市場，開啟 MCP 服務市場，就能看到一堆熱門的 MCP 服務，哪還需要到什麼 MCP 資源網站上自己安裝啊？！

![](https://pic.yupi.icu/1/image-20260305154025676.png)

比如我想使用 Context7 這個獲取最新技術文件的 MCP，點選安裝後，會自動彈窗讓我輸入 API Key：

![](https://pic.yupi.icu/1/image-20260305154459227.png)

確認之後，就可以正常使用了。AI 在執行任務時會自動呼叫 MCP 提供的工具，你也可以用 `#` 號主動引用。

比如剛才裝好了 Context7，之後讓 AI 寫程式碼時它就會自動去拉取最新的技術文件作為參考，減少 AI 瞎編 API 用法的情況。

![](https://pic.yupi.icu/1/image-20260306110049012.png)

整個過程不需要手寫 JSON 配置，全程視覺化選擇和安裝，對新手特別友好。以前在 Cursor 裡配 MCP 還得自己找 JSON 貼上，這裡點點滑鼠就搞定了~

當然，如果你是老手，也可以透過 `.vscode/mcp.json` 檔案手動配置 MCP 服務。

```json
{
  "servers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp"
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@microsoft/mcp-server-playwright"]
    }
  }
}
```

這個檔案不會自動生成，需要你自己建立，或者透過 VSCode 的命令面板執行 `MCP: Open Workspace Folder Configuration` 命令來開啟：

![](https://pic.yupi.icu/1/image-20260306110305648.png)

MCP 服務除了提供工具之外，還支援 Resources（資源）和 MCP Apps（互動式應用）。Resources 可以給 AI 提供資料庫表、API 響應等上下文；MCP Apps 則能在對話中渲染表單、儀表盤等互動式 UI 元件，體驗拉滿。

![](https://pic.yupi.icu/1/mcp-apps-flame-graph.png)

此外，VSCode 還能自動發現其他應用中已配置的 MCP 服務，省去重複配置的麻煩，在 VSCode 聊天設定中搜尋 `chat.mcp.discovery.enabled` 即可開啟。

![](https://pic.yupi.icu/1/image-20260306110930161.png)

MCP 配置也支援透過 Settings Sync 跨裝置同步，在同步設定中勾選「MCP 伺服器」選項，換電腦不用重新配一遍。

![](https://pic.yupi.icu/1/image-20260306110740774.png)



### Agent Skills - 給 AI 的技能包

Agent Skills 是給 AI 準備的能力擴充套件包。和前面提到的 Tools 不同，Skills 更像是一份詳細的工作手冊，裡面包含操作指南、指令碼、示例程式碼等資源，讓 AI 在特定任務上表現更專業。

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

比如你給 AI 裝個「Web 應用測試」的 Skill，裡面寫好了用 Playwright 寫測試的標準流程、示例模板、最佳實踐。之後你讓 AI 幫你寫測試，它就會自動按照這套標準來，而不是每次都瞎寫一通。

注意，Skills 是一個 [開放標準](https://agentskills.io/)，不僅在 Github Copilot 裡能用，Claude Code、Cursor 等 AI 程式設計工具中也能用，一套 Skill 多處複用，這也是它能火的原因之一。

從哪兒搞到 SKills 呢？

大多數情況下，直接從網上安裝別人開發好的 SKills 就可以了。比如 [魚皮 AI 導航的 Skills 大全](https://ai.codefather.cn/skills) 裡有我給大家精選的技能包，也可以去 GitHub 上的 [awesome-copilot](https://github.com/github/awesome-copilot) 倉庫逛逛，社群貢獻了不少實用的 Skills，拿來就能用。

![](https://pic.yupi.icu/1/image-20260306111855649.png)

在 VSCode 中，你可以透過對話方塊的 Skills 設定按鈕，檢視和管理本地已有的 SKills：

![](https://pic.yupi.icu/1/image-20260306111219014.png)

當然，你也可以自己建立 Skills，可以透過視覺化介面選擇安裝位置，比如安裝在當前專案下（僅本專案能用），還是安裝到使用者目錄下（整個電腦的所有專案都能用）：

![](https://pic.yupi.icu/1/image-20260306112025446.png)

建立技能的核心是編寫 `SKILL.md` 技能描述檔案，比如建立一個「Web 應用測試」技能，文件內容示例如下：

```markdown
---
name: webapp-testing
description: 使用 Playwright 測試 Web 應用的指南，當需要建立或執行瀏覽器測試時使用
---

# Web 應用測試指南

## 建立測試
1. 參考 [測試模板](./test-template.js)
2. 確定要測試的使用者流程
3. 在 tests/ 目錄建立新的測試檔案
4. 使用 Playwright 的定位器來查詢元素

## 執行測試
執行命令：npx playwright test

## 最佳實踐
- 為動態內容使用 data-testid 屬性
- 保持測試獨立和原子化
- 使用 Page Object Model 組織複雜頁面的測試
```

![](https://pic.yupi.icu/1/image-20260306112358350.png)

Skill 建立好之後，你可以在對話區域裡用 `/webapp-testing` 斜槓命令手動呼叫它，也可以讓 AI 根據任務自動匹配載入。

![](https://pic.yupi.icu/1/image-20260306112515795.png)

Skills 採用漸進式披露的設計，AI 只在需要時才載入相關 Skill 的內容，不會一次性把所有資訊都塞進上下文，既節省 Token 又保持靈活。即使裝了幾十個 Skill 也不用擔心上下文爆炸。



### 多種 Agent 執行方式

前面實戰中，我們用的是本地 Agent，但其實 GitHub Copilot 支援 4 種 Agent 執行方式，適合不同的使用場景：

| 執行方式           | 特點                                         | 適用場景                                 |
| ------------------ | -------------------------------------------- | ---------------------------------------- |
| Local 本地         | 在 VSCode 中互動式執行，實時反饋             | 探索性任務、需要即時反饋的開發           |
| Background 後臺    | 在本地後臺自主執行，使用 Git worktree 隔離   | 需求明確的任務，你想邊幹別的邊讓 AI 幹活 |
| Cloud 雲端         | 在遠端伺服器執行，完成後自動提 PR            | 團隊協作、不想佔用本地資源的任務         |
| Third-party 第三方 | 接入 Anthropic Claude、OpenAI 等第三方 Agent | 想用特定 AI 廠商的能力                   |

你可以在 Chat 對話區域底部的下拉選單中隨時切換不同的執行方式：

![](https://pic.yupi.icu/1/image-20260306094253979.png)

有個騷操作是，你可以在不同的 Agent 之間移交任務。比如先用本地 Agent 做個 Plan，覺得方案沒問題了，一鍵移交給 Cloud Agent 去執行，它會自動建立分支、寫程式碼、跑測試、最後提一個 Pull Request 給你的團隊審查。

你還可以同時開多個 Agent Session，每個 Session 處理不同的任務，在 Chat 面板的 Sessions 列表中統一管理、檢視狀態、切換任務。

就像 Claude Code 可以同時開多個終端 Tab 一樣，Copilot 的 Sessions 列表讓你在一個面板裡統一管理所有 AI 任務的狀態，這是 GitHub 官方文件中重點推薦的工作流。

![](https://pic.yupi.icu/1/image-20260306112932393.png)



### Hooks - 自動觸發的指令碼

Hooks 允許你在 Agent 執行的關鍵節點自動執行自定義指令碼。簡單來說，就是在 Agent 工作流程的特定時機，自動執行你預設好的命令。

你可以在 VSCode 設定中檢視和管理已配置的 Hooks：

![](https://pic.yupi.icu/1/image-20260306094814153.png)

目前支援的生命週期事件包括：

- PreToolUse：Agent 呼叫工具前觸發，比如攔截 `rm -rf` 等危險命令
- PostToolUse：Agent 呼叫工具後觸發，比如自動跑 Prettier 格式化程式碼
- SessionStart / Stop：Agent 會話開始和結束時觸發（官方事件名分別是 SessionStart 和 Stop），比如在會話開始時自動注入專案上下文，會話結束時生成工作報告
- UserPromptSubmit：使用者提交提示詞時觸發，比如審計使用者請求、注入系統上下文
- SubagentStart / SubagentStop：子智慧體啟動和完成時觸發，比如跟蹤子任務的執行情況和資源消耗

舉個例子，在專案的 `.github/hooks/` 目錄下建立 JSON 配置檔案，填入下列程式碼：

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "type": "command",
        "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
      }
    ]
  }
}
```

![](https://pic.yupi.icu/1/image-20260306113256929.png)

這樣每次 Agent 呼叫工具修改了程式碼檔案，都會自動跑一遍 Prettier 程式碼美化工具，保證程式碼風格統一。

Hooks 的應用場景很多，比如自動格式化程式碼、攔截危險命令（`rm -rf` 和 `DROP TABLE`，防止刪庫跑路）、記錄每一次工具呼叫便於排查問題。而且 Hooks 的配置格式和 Claude Code 是相容的，如果你之前在 Claude Code 裡配過 Hooks，可以直接複用。



### Custom Instructions - 讓 AI 遵循你的規範

自定義指令就是給 AI 定規矩。

你把編碼規範、技術偏好、專案約定寫到一個 Markdown 檔案裡，AI 在每次對話時都會自動遵循這些規則，不需要每次都重複說 “用 TypeScript 寫”、“變數名不要用 a b c” 之類的。

其實這個概念和 AGENTS.md 類似，都是透過檔案來告訴 AI 專案的規範和約定。區別在於 Copilot 的指令檔案路徑是 `.github/copilot-instructions.md`，而且支援更細粒度的檔案模式匹配（類似 Cursor 的 Rules）。

建立指令的方式很簡單，在對話區域的設定中開啟「聊天指令」，然後選擇建立位置：

![](https://pic.yupi.icu/1/image-20260306113751454.png)

或者手動在專案根目錄下新建 `.github/copilot-instructions.md` 檔案，填入內容即可，比如：

```markdown
# 專案編碼規範

## 程式碼風格
- 使用語義化 HTML5 元素
- 優先使用 ES6+ 語法（const/let、箭頭函式、模板字串）
- 變數命名使用 camelCase，元件命名使用 PascalCase

## 技術偏好
- 前端框架優先用 React + TypeScript
- CSS 使用 Tailwind CSS
- 測試使用 Vitest

## 程式碼質量
- 函式和變數名要有意義，能自解釋
- 複雜邏輯要加註釋
- 使用者輸入和 API 呼叫要加錯誤處理
```

![](https://pic.yupi.icu/1/image-20260306114223424.png)

VSCode 支援兩種指令型別。一種是全域性生效的指令（Always-on），所有對話都會自動應用；另一種是基於檔案模式匹配的指令（File-based），比如 `.tsx` 檔案用 React 元件規範，`.test.ts` 檔案用測試規範，只有匹配到對應檔案時才生效。

像下面這種帶 YAML 頭部的結構，就是 File-based 指令的標準寫法，透過 `description` 欄位描述何時生效、`applyTo` 欄位指定匹配的檔案模式：

![](https://pic.yupi.icu/1/image-20260306121336765.png)

還有個小技巧，在對話區域裡輸入 `/init`，AI 會自動分析你的專案結構和程式碼風格，幫你生成一份自定義指令檔案，省得自己從零寫起。這個命令特別適合接手老專案、或者在已有專案上擴充套件功能的場景，AI 能幫你快速梳理出專案已有的編碼習慣。

![](https://pic.yupi.icu/1/image-20260306100241500.png)



### Custom Agents - 給 AI 分配角色

自定義智慧體就是給 AI 分配不同的角色。比如你可以建立一個安全審查員、測試工程師、架構師等角色，每個角色有自己的指令、工具許可權和行為規則。

跟 Custom Instructions 自定義指令不一樣的是，Instructions 是全域性規則，不管你跟 AI 聊什麼它都會遵循；而 Custom Agents 是角色切換，你選了某個角色後，AI 就只按那個角色的設定來工作，包括能用哪些工具、不能做哪些操作，都由角色定義。

建立自定義智慧體的方式有兩種。

一種是在對話區域的設定中開啟「自定義智慧體」，選擇建立位置（當前專案或使用者目錄），VSCode 會自動建立對應的檔案：

![](https://pic.yupi.icu/1/image-20260306114509869.png)

另一種方法是手動寫一個 `.agent.md` 檔案放在 `.github/agents/` 目錄下。比如建立一個寫作助手 `article.agent.md`：

```markdown
---
name: 寫作助手
description: 幫助撰寫和最佳化技術文章、專案文件
tools: ['search', 'codebase', 'fetch', 'editFiles']
---

# 寫作助手

你是一位經驗豐富的技術寫作者，擅長把複雜的技術概念講得通俗易懂。

## 寫作風格
- 用口語化的表達，像跟朋友聊天一樣
- 段落要短，避免大段文字堆砌
- 適當加入類比和例子幫助理解

## 重要規則
- 先列大綱，確認後再寫正文
- 每段都要有明確的主題
- 技術術語第一次出現時要解釋
```

![](https://pic.yupi.icu/1/image-20260306121541349.png)

儲存後，在對話區域的智慧體下拉選單中就能看到這個寫作助手了，選中它 AI 就會按照你定義的角色來工作。

![](https://pic.yupi.icu/1/image-20260306121613414.png)

自定義智慧體還有一個更強大的玩法，叫 Handoffs（移交）。你可以在 Agent 檔案中定義「下一步動作」按鈕，實現智慧體之間的任務接力。

比如 Plan 智慧體出完方案後，底部出現一個「開始實現」按鈕，點一下就自動切換到 Agent 模式開始編碼，把方案的上下文完整傳遞過去：

```yaml
handoffs:
  - label: 開始實現        # 按鈕上顯示的文字
    agent: agent           # 移交給哪個智慧體
    prompt: 按照上面的方案開始編碼  # 自動填入的提示詞
    send: false            # false 表示不自動傳送，等你確認後再發
```

除了 Handoffs，你還可以編排多個專業智慧體的協作流程。

假設你在做一個新功能，需要先調研專案裡已有的程式碼模式，再動手寫程式碼。你可以建立一個「功能開發」主智慧體，讓它先呼叫一個只讀的「調研員」子智慧體來分析程式碼庫中的相關模組和設計模式，拿到分析結果後，再呼叫「編碼員」子智慧體按照分析出的模式來寫新程式碼。這種多智慧體編排在做複雜功能時特別實用，每個角色各司其職，比單個 AI 亂寫一氣靠譜得多。

VSCode 還支援 Claude 格式的 Agent 檔案（放在 `.claude/agents` 目錄），如果你之前用 Claude Code 建立過自定義 Agent，可以直接拿過來用，無縫相容。



### Prompt Files - 可複用的提示詞模板

Prompt Files（提示詞檔案）可以把你常用的任務封裝成 **斜槓命令**，在對話中隨時複用。

比如你經常需要生成 React 元件、執行安全審查、編寫單元測試，每次都得重複輸入類似的提示詞，而有了 Prompt Files 之後就不用了。

跟自定義指令的區別是，自定義指令會自動應用到所有對話，而 Prompt Files 需要你手動在對話中輸入 `/命令名` 來觸發，更適合特定任務場景。

建立方式跟自定義指令完全類似，在對話區域的設定中開啟「提示檔案」，在彈出的對話方塊中選擇「新建提示檔案」：

![](https://pic.yupi.icu/1/image-20260306122919311.png)

然後選擇建立位置（當前專案或使用者目錄），VSCode 會自動建立對應的檔案：

![](https://pic.yupi.icu/1/image-20260306123109760.png)

你也可以直接在 `.github/prompts/` 目錄下建立 `.prompt.md` 檔案。舉個例子，建立一個 `/gen-test` 命令來自動生成單元測試：

```markdown
---
description: 為當前檔案生成單元測試
agent: agent
tools: ['search', 'search/codebase', 'edit/editFiles']
---
為 [${fileBasename}](${file}) 生成單元測試。

- 測試檔案放在同目錄下：${fileDirname}
- 命名為：${fileBasenameNoExtension}.test.ts
- 測試框架：${input:framework:jest or vitest}
- 參考專案的測試規範：[testing.md](../docs/testing.md)
```

這裡面用到了一些變數，比如 `${file}` 會自動替換為當前開啟的檔案路徑，`${input:framework}` 是指要從使用者在對話方塊中輸入的內容來獲取值。

![](https://pic.yupi.icu/1/image-20260306123242156.png)

儲存後，在對話方塊中輸入 `/gen-test` 就能觸發。你還可以在後面追加額外資訊，比如 `/gen-test 只測試登入相關的函式`。

![](https://pic.yupi.icu/1/image-20260306123816437.png)



### Smart Actions - AI 快捷操作 

除了上面這些核心特性，Copilot 還在 VSCode 的各個角落埋了不少 AI 快捷操作，叫 Smart Actions。你不需要寫提示詞，右鍵選單就能觸發。

常用的有以下這些，可以先跳過，等需要的時候再回來看：

- 自動生成 Commit Message：在 Source Control 面板點一下小星星圖示，AI 就根據你的程式碼改動自動生成提交資訊
- 程式碼解釋：選中一段程式碼，右鍵「Explain」，AI 幫你解釋這段程式碼在幹啥
- 生成測試：選中程式碼，右鍵「Generate Tests」，AI 幫你寫單元測試
- 生成文件：選中程式碼，右鍵「Generate Docs」，AI 幫你寫註釋文件
- 修復錯誤：程式碼有報錯時，AI 會自動彈出修復建議
- 程式碼審查：選中程式碼，右鍵「Review」，AI 給你做 Code Review
- 語義搜尋：在搜尋面板中啟用 AI 搜尋，按語義而非文字精確匹配來搜尋程式碼
- AI 輔助重新命名：重新命名變數時，AI 會根據上下文給出建議的新名字

我自己平時用的最多的就是自動生成 Commit Message，再也不用絞盡腦汁想提交資訊怎麼寫了。

![](https://pic.yupi.icu/1/image-20260306121819177.png)

這些小功能單個看起來不起眼，但用起來真的能省不少事。

恭喜，看到這裡你就超過了 99% 的同學！



## 寫在最後

總結一下，VSCode + GitHub Copilot 給我最大的感覺就是 **全面**。

實話說，論 Agent 程式設計的極致體驗，Claude Code 還是更強一些；論新功能推出的速度和迭代節奏，Cursor 也一直走在前面。

但 Copilot 勝在它是 “六邊形戰士”，從程式碼補全到 AI 對話、從 Agent 程式設計到 MCP 生態、從自定義指令到智慧體編排，AI 程式設計該有的能力它基本都有了，而且每個方面的體驗都很絲滑。

此外，我估計很多同學在 AI 流行之前就一直在用 VSCode，現在裝個外掛就能無縫升級到 AI 程式設計，不用換編輯器、不用重新學操作、不用遷移配置，使用門檻是最低的。

感興趣的同學可以去試試，記得先白票 30 天的 Pro 試用~ 而且如果你是在校學生，還可以透過 [GitHub Education](https://education.github.com/pack) 申請學生認證，認證透過後 Copilot Pro 直接免費用，不限時！我在學校的時候咋沒有這種好事？

對了，如果你想用 GitHub Copilot 做更復雜的全棧專案實戰，可以跟著魚皮最新的 [AI 熱點監控專案](https://www.codefather.cn/course/2026625439052627970) 練手，我幫大家測過了，企業級大專案 Copilot 也完全能 hold 住。

![](https://pic.yupi.icu/1/image-20260304102630302.png)

就寫到這，覺得有用的話記得收藏這篇文章，也歡迎在評論區聊聊你喜歡用哪款 AI 程式設計工具，幫到更多同學做選擇。



## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)