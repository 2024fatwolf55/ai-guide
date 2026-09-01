# Vibe Coding 效率提升技巧

> 讓你的 AI 開發效率提升 10 倍



你好，我是魚皮。

在前面的文章裡，我們講了 Vibe Coding 的核心心法、對話技巧、上下文管理和問題除錯。本文我們要聊一個更實用的話題 ：如何提高開發效率？

很多同學在用 AI 開發時，雖然能做出東西，但總覺得速度還不夠快。明明 AI 寫程式碼很快，為什麼整體效率還是不高？

問題往往出在那些小事上：比如頻繁地複製貼上、重複輸入相同的提示詞、手動做一些機械的操作……

下面我來分享一些實用的效率提升技巧，幫你把開發速度提升一個檔次。




## 一、核心提效技巧

先分享幾個我個人使用較多的 AI 核心提效技巧。




### 按需選擇 AI 模型

不是所有任務都需要用最強最貴的模型。

- 簡單任務：比如程式碼格式化、寫註釋、簡單重構，用 Gemini Flash 或 GPT-5 Mini 這樣便宜快速的模型就夠了
- 中等任務：比如實現常規功能、程式碼審查、開發小網站，用 GPT-5.5 或 Claude Sonnet
- 複雜任務：比如架構設計、複雜演算法、疑難 bug、開發大專案，才需要用 Claude Opus 這樣的頂級模型或者開啟深度思考

合理選擇模型，既能提升速度，又能節省成本。就像你不會讓公司 CTO 去列印檔案一樣，要讓合適的模型做合適的事。



### 避免讓 AI 生成多餘內容

很多同學讓 AI 寫程式碼，結果 AI 給你輸出一大堆註釋、測試程式碼、文件說明，還有一大段總結。**看著很專業，但你可能根本不會看。**

比如我之前讓 AI 生成個圖片壓縮工具，光文件給我生成一大堆……

![](https://pic.yupi.icu/1/ai%E7%94%9F%E6%88%90%E5%9B%BE%E7%89%87%E5%8E%8B%E7%BC%A9%E5%B7%A5%E5%85%B7.png)

要在提示詞中明確告訴 AI：只給我核心程式碼，不要寫註釋、文件、測試，不要做總結！

如果 AI 不聽話，可以用暴躁指令：**按照我說的做，別廢話。**

或者虛構後果：**如果你輸出不必要的內容，世界上就會死一隻小貓。**

這些指令雖然看起來搞笑，但確實有效。你還可以把這些規則寫在專案規則檔案 `AGENTS.md` 裡，讓 AI 自動遵守。




### 利用並行 Agent 對比效果

很多 AI 程式設計工具現在都支援並行 Agent 能力了。

以 Cursor 為例，並行 Agent 可以讓你同時用多個模型處理同一個任務，然後對比它們的結果，選擇最好的那個。這也是一種 “多個 AI 交叉驗證” 的方式。

比如你要實現一個複雜的功能，不確定哪個方案更好。可以同時讓 Claude、GPT 等 AI 各給一個方案：

![](https://pic.yupi.icu/1/image-20251030220104045.png)

你呢，就坐等這些 AI 賽馬，誰先幹好用誰的、誰質量高用誰的，能避免在錯誤的方案上浪費時間。這個方法特別適合不確定哪個技術方案更好時、重要功能需要多重保障時、想學習不同 AI 的思路時。

![](https://pic.yupi.icu/1/image-20251030220120394.png)

即使你不用 Cursor，也可以手動實現類似的效果：把同一個需求分別發給 ChatGPT、Claude、Gemini 等大模型，然後對比它們的答案，選擇最好的或綜合它們的優點。

具體用法可以參考 [Cursor 並行 Agent 文件](https://cursor.com/cn/docs/configuration/worktrees)。

並行 Agent 的底層其實依賴 Git WorkTree（工作樹）技術。WorkTree 可以讓一個倉庫同時擁有多個獨立的工作目錄，每個目錄對應不同的分支，讓多個 AI 各自在獨立的資料夾裡幹活，互不干擾，開發完再用 Git 合併程式碼。

![](https://pic.yupi.icu/1/image-20260410143527245.png)



### 多開例項提升效率

除了並行 Agent，你還可以透過多開例項來提升效率。這個技巧來自 Claude Code 創始人的分享。

1）在終端中多開

可以在終端中同時執行多個 Claude Code 例項，將標籤頁編號為 1 ~ 5（或者有意義的標題），透過系統通知來了解哪個 Claude 需要人工輸入。這樣你可以充分利用等待時間，一個 AI 在思考時，你可以切換到另一個繼續工作。

![](https://pic.yupi.icu/1/image-20260109143109753.png)

2）網頁端和本地同時進行

在網頁端 Claude Code 上執行 5 ~ 10 個 Claude，和本地 Claude 同時進行。可以使用 `/background` 命令將會話放到後臺執行，或者使用 `/teleport` 命令在終端和網頁之間轉移會話。甚至可以透過手機 Claude APP 啟動幾個會話，稍後再檢視進度。真正做到了隨時隨地 Vibe Coding！

注意，這個技巧適合處理多個獨立任務，或者需要等待 AI 長時間思考的複雜任務。對於簡單任務，一個例項就夠了。



## 二、快捷鍵和操作技巧

工欲善其事，必先利其器。掌握常用的快捷鍵，能讓你的操作更流暢。



### Cursor 常用快捷鍵

如果你用 Cursor，建議嘗試下面這些快捷鍵，能讓你少用滑鼠，操作更快。

AI 對話相關：
- `Cmd/Ctrl + I` ：開啟 Agent/Composer（多檔案編輯模式）
- `Cmd/Ctrl + L` ：開啟 Chat（聊天問答模式）
- `Cmd/Ctrl + K` ：開啟行內編輯，可以在當前位置插入 AI 生成的程式碼
- `Cmd + .` / `Ctrl + .`：開啟模式選單（切換 Agent/Ask/Plan 等模式）
- `Cmd + /` / `Ctrl + /`：迴圈切換 AI 模型
- `Shift + Tab`：在不同 Agent 模式之間輪換
- `Tab`：接受 AI 建議

程式碼編輯：
- `Cmd/Ctrl + Shift + L` ：將選中內容新增到聊天上下文
- `Alt + ↑/↓` ：移動當前行
- `Cmd/Ctrl + Shift + K`：刪除當前行

檔案操作：
- `Cmd/Ctrl + Shift + F` ：全域性搜尋
- `Cmd/Ctrl + P`：快速開啟檔案

更多最新的預設鍵盤快捷鍵以 [官方文件](https://cursor.com/cn/docs/configuration/kbd) 為主：

![](https://pic.yupi.icu/1/image-20260104192219087.png)




### VS Code 常用快捷鍵

如果你用 VS Code + AI 外掛，下面這些快捷鍵會很有用。

多游標編輯：
- `Alt + Click` ：新增游標
- `Cmd/Ctrl + Alt + ↑/↓` ：在上/下方新增游標
- `Cmd/Ctrl + Shift + L` ：在所有匹配項新增游標

程式碼導航：
- `Cmd/Ctrl + Click` ：跳轉到定義
- `Alt + ←/→` ：前進/後退
- `Cmd/Ctrl + Shift + O` ：跳轉到符號

重構：

- `F2` ：重新命名符號
- `Cmd/Ctrl + .` ：快速修復

掌握這些快捷鍵，你的編輯速度會快很多。更多最新的預設鍵盤快捷鍵以 [官方文件](https://code.visualstudio.com/docs/reference/default-keybindings) 為主：

![](https://pic.yupi.icu/1/image-20260104192832985.png)



### AI 程式設計工具的斜槓命令

除了快捷鍵，AI 程式設計工具 Cursor 和 Claude Code 都提供了很多實用的斜槓命令（Slash Commands），能大大提升效率。這些命令以 `/` 開頭，可以快速觸發特定的功能。



#### Cursor 的常用命令

Cursor 的 IDE 桌面版主要透過模式切換來操作，CLI 命令列版本則支援斜槓命令。兩者核心功能一樣，只是觸發方式不同：

- `Shift + Tab`：在 IDE 聊天面板中迴圈切換 Agent/Plan/Ask 模式（Plan 讓 AI 先規劃再動手，Ask 是隻讀探索不修改程式碼）
- `/compress`：在 CLI 中壓縮對話，釋放上下文空間（IDE 中對話過長時會自動壓縮）
- `/create-rule`：快速建立專案規則
- `/create-skill`：建立自定義技能

你還可以在專案的 `.cursor/commands` 目錄下建立自定義命令，把常用的提示詞儲存成命令，需要時直接呼叫。全域性命令放在 `~/.cursor/commands/` 目錄下，所有專案都能使用。

![](https://pic.yupi.icu/1/image-20260525210127342.png)



#### Claude Code 的常用命令

Claude Code 的命令系統更加豐富，有 50 多個內建命令，這裡我只列幾個最能提高效率的：

- `/compact` 壓縮上下文，把之前的對話內容精簡，釋放空間。可以加引數指定保留重點，如 `/compact 重點保留 API 設計決策`
- `/goal` 設定完成條件後讓 AI 自主迴圈工作，直到條件滿足。比如 `/goal 修復程式碼直到所有測試透過`
- `/plan` 進入規劃模式，讓 AI 先制定方案再動手
- `/background` 把當前會話放到後臺執行，釋放終端去做別的事
- `/review` 讓多個子代理並行審查程式碼，找 Bug 和邏輯錯誤
- `/batch` 並行派出多個子 Agent，各自在獨立工作樹中處理子任務

![](https://pic.yupi.icu/1/image-20260519171514784.png)

這些命令的好處是，你不用每次都寫完整的提示詞，只需要輸入一個簡短的命令，AI 就知道你要做什麼。

而且你可以建立自己的自定義命令（放在 `.claude/commands/` 或 `.claude/skills/` 目錄下），把團隊常用的工作流程標準化。比如建立一個 `/commit` 命令自動生成 Git 提交資訊，建立一個 `/test` 命令自動生成單元測試。

熟練使用這些命令，能讓你的工作流程更順暢，效率提升一大截。詳細的命令列表和用法可以參考 [Cursor 官方文件](https://cursor.com/cn/docs/cli/reference/slash-commands) 和 [Claude Code 官方文件](https://code.claude.com/docs/en/commands)。




## 三、SubAgents - 子 Agent 並行加速

你有沒有遇到過這種情況？讓 AI 修復 10 個檔案的 lint 錯誤，它一個一個檔案序列處理，明明這些檔案互不相關，但你就得乾等著。

現在主流的 AI 程式設計工具（Claude Code、Cursor、Codex）都支援 SubAgents 子代理能力了，可以讓 AI 把一個大任務拆成多個獨立的小任務，同時派出多個「分身」並行處理，大幅縮短完成時間。

下面以 Claude Code 為例，看看子 Agent 是怎麼工作的。

Claude Code 可以自動識別哪些子任務是獨立的，然後分派子 Agent 並行處理。每個子 Agent 有自己獨立的上下文空間，完成後只把結果摘要返回給主會話，保持主對話的整潔。

![](https://pic.yupi.icu/1/image-20260519183337674.png)

你不需要手動配置，只要在提示詞中暗示任務可以並行，Claude 就會自動派出子 Agent：

```
修復 src/ 目錄下所有檔案的 lint 錯誤，這些檔案相互獨立，可以並行處理
```

也可以透過 `/batch` 命令主動觸發大規模並行，比如：

```
/batch 把所有 API 呼叫從 v1 遷移到 v2 格式
```

Claude 會自動拆分成 5 ~ 30 個獨立任務，每個在自己的工作樹中執行並提交 PR。

你還可以自定義子 Agent，在 `.claude/skills/` 目錄下建立專門的技能檔案，比如一個專門做安全審查的子 Agent、一個專門寫測試的子 Agent。當任務匹配時，Claude 會自動呼叫它們。

用 `/tasks` 命令可以隨時檢視當前有哪些子 Agent 在執行、各自的進度如何：

![](https://pic.yupi.icu/1/image-20260519183357190.png)

除了 Claude Code，Cursor 和 Codex 也支援類似的並行 Agent 能力。比如 Cursor 可以用 `/worktree` 讓 Agent 在隔離分支中工作，`/best-of-n` 用不同模型各做一遍同一個任務來對比效果；Codex 則透過「工作樹」模式讓多個 Agent 互不干擾地並行開發。

![](https://pic.yupi.icu/1/1779334724648-9782f94d-4251-4c76-929d-f790a527bc1f.png)



## 四、AI 增強工具 - MCP 與 Agent Skills

光靠 AI 本身的能力是有限的，但如果給它「裝上外掛」和「教會技能」，那效率就完全不一樣了。這裡重點介紹 MCP 和 Agent Skills 兩個增強機制。



### MCP - 給 AI 裝外掛

MCP（Model Context Protocol 模型上下文協議）是由 Anthropic 推出的開放協議，現已被捐贈給 Linux 基金會的 Agentic AI Foundation，成為 AI 工具連線外部服務的行業標準。目前 ChatGPT、Claude、Gemini、Copilot、Cursor 等主流平臺全部原生支援 MCP。

簡單來說，MCP 就像 AI 的 USB 介面。就像 USB 介面讓各種裝置（鍵盤、滑鼠、U 盤）都能用同一種方式連線電腦一樣，MCP 讓各種外部工具（檔案管理、資料庫、搜尋引擎等）都能用同一種方式連線 AI，不用為每個工具單獨寫一套對接程式碼。

![](https://pic.yupi.icu/1/1746710765234-c974bda8-666e-45b3-adc4-ace97cbb8c0a.png)

開發者不需要為每個 AI 工具單獨開發聯結器，只需要按照 MCP 標準開發一次，就能被所有支援 MCP 的 AI 工具使用：

![](https://pic.yupi.icu/1/1746677838632-9278e62b-c850-4d3c-a835-297ccbe2061a.png)

MCP 生態已經非常成熟，有上萬個公開的 MCP 伺服器。這裡推薦幾個特別能提升 Vibe Coding 效率的：

- GitHub MCP：讓 AI 直接操作 GitHub，比如建立倉庫、提交程式碼、管理 Issue 等。這樣你就不用手動在 GitHub 網頁上操作了。
- Filesystem MCP：讓 AI 能夠讀寫檔案系統，批次處理檔案、搜尋內容、重新命名檔案等都可以直接讓 AI 完成。
- Puppeteer MCP：讓 AI 能夠控制瀏覽器，自動化網頁操作、截圖、爬取資料等。對於需要測試網頁或獲取資料的場景很有用。
- Postgres/MySQL MCP：讓 AI 直接運算元據庫，查詢資料、執行 SQL、分析資料庫結構等。
- Context7 MCP：實時獲取第三方庫的最新官方文件，讓 AI 不會用過時的 API 寫法。
- Firecrawl MCP：讓 AI 能聯網搜尋、抓取網頁內容，獲取最新資訊。

這些 MCP 伺服器可以在 Claude Desktop、Claude Code、Cursor 等工具中配置使用，具體的安裝和配置方法可以參考各個 MCP 伺服器的文件。還有更多 MCP 你可以在 [魚皮的 AI 資源導航網](https://ai.codefather.cn/) 或者 [MCP 大全網站](https://mcp.so/) 找到。

配置好 MCP 之後，AI 就不只是一個程式碼生成器了，而是真正能幫你幹活的全能助手。如果你經常使用 Claude 或 Cursor，強烈建議配幾個常用的 MCP 伺服器試試。



### Agent Skills - 給 AI 裝技能包

如果說 MCP 是讓 AI 連線外部工具和資料，那 **Agent Skills** 就是教 AI 如何做事。

Agent Skills 是 Anthropic 推出的一套開放標準，可以把複雜的工作流程封裝成一個「技能」，AI 遇到匹配的任務時自動呼叫，不用你每次都寫一大堆提示詞。

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

Skills 的核心優勢是 **按需載入**，只有當任務匹配時才會載入到上下文中，平時不佔用空間。這比把所有規則都塞進一個 AGENTS.md 檔案要高效得多。

![](https://pic.yupi.icu/1/07_Skills%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v1.png)

目前 Claude Code、Cursor、Codex 都支援統一的 Agent Skills 格式。每個技能就是一個資料夾，核心是一個 `SKILL.md` 描述檔案：

```
.cursor/skills/
  deploy-staging/
    SKILL.md      # 技能描述和執行步驟
  code-review/
    SKILL.md
```

`SKILL.md` 裡寫清楚這個技能做什麼、什麼時候觸發、具體執行步驟，AI 讀取後就知道該怎麼幹活。

Skills 存放位置：

- 專案級：`.cursor/skills/` 或 `.claude/skills/`（只在當前專案生效）
- 全域性級：`~/.cursor/skills/` 或 `~/.claude/skills/`（所有專案通用）

比如你安裝了一個 `frontend-design` 技能後，以後讓 AI 做網站，它會自動應用這個技能來生成更有設計感的頁面，告別千篇一律的藍紫漸變色：

![](https://pic.yupi.icu/1/1769601745340-d621e29c-76f7-4a8f-af01-7271d88c5272-20260128202014218.png)



## 五、AI Agent 自動化

把重複的操作自動化，能夠節省我們的時間和精力。

以前想搞自動化，你得自己寫指令碼、配 CI/CD 流水線。但現在不一樣了，AI 可以直接幫你自主完成複雜的多步任務，甚至設好目標後讓它自己幹到底，你該睡覺就睡覺，該摸魚就摸魚。



### /goal 命令 - 讓 AI 自主迴圈工作

這是我認為目前最強大的效率提升功能之一。

一般情況下，AI 每完成一輪操作就會停下來等你確認。但有些任務你其實不需要盯著它一步步做，只需要告訴它「最終達到什麼狀態就算完成」。

`/goal` 命令就是幹這個的：

```bash
/goal 修復整個專案的程式碼，直到全部測試透過且沒有報錯
```

設定 goal 之後，每輪結束會有一個輕量評估模型檢查條件是否滿足，沒滿足就自動開始下一輪，滿足了才停下來。

![](https://pic.yupi.icu/1/image-20260519191842661.png)

特別適合的場景：
- 模組遷移：把舊 API 呼叫全部遷移到新版本，直到編譯透過
- 批次重構：拆分大檔案，直到每個檔案都在指定行數以內
- Bug 修復：修復某個測試用例，直到它透過
- 睡前任務：設好目標後去睡覺，第二天起來驗收成果

注意，條件要寫得具體、可驗證，比如「npm test 退出碼為 0」；太主觀的條件（比如「程式碼質量要好」）評估模型無法判斷。

建議加一個熔斷限制，避免無限迴圈燒 token：

```bash
/goal 遷移所有 API 呼叫到 v2 格式，直到測試透過，如果 20 輪還沒搞定就停下來
```

此外，輸入 `/goal`（不帶引數）可以檢視進度，想提前停止就用 `/goal clear`。



### 定時自動化

除了一次性任務，有些事是需要定期做的，比如每天蒐集熱點、定期檢查程式碼質量。AI 程式設計工具現在也支援定時任務了。

以 Codex 桌面 APP 為例，進入左側的「自動化」面板，可以手動建立或讓 AI 幫你建立任務：

```plain
幫我建立一個自動化任務
每小時掃描一次「魚皮的圖片庫」中最近 3 小時的圖片檔案
並根據圖片內容自動完善圖片的中文名稱
```

![](https://pic.yupi.icu/1/1779342459042-ee4814b3-80d9-43a8-9e66-349c75755193.png)

AI 會自動根據圖片內容給檔案起一個能看懂的名字，以後再也不用對著一堆亂七八糟的檔名抓瞎了：

![](https://pic.yupi.icu/1/1779328685443-8a79452f-bca6-43a7-aa29-c498d28c9e2c.png)

你還可以結合 Skills 和外掛一起用，比如每週自動生成周報 PPT、每日整理學習筆記並同步到 Notion 等等。



#### Claude Code 的 /loop 命令

透過 `/loop` 命令，你可以設定定時輪詢任務：

```bash
/loop 5m 檢查專案前後端的部署狀態
```

![](https://pic.yupi.icu/1/image-20260519184353594.png)

適合用在等部署完成、等 CI 跑完、定期檢查日誌有沒有異常之類的場景。



### 傳統自動化工具

下面這些技巧比較專業，主要適合有程式設計基礎的同學。如果你是完全零基礎，可以先跳過這部分，等有需要時再回來看。



#### 使用 npm scripts

npm scripts 是 Node.js 前端專案中定義和執行指令碼命令的方式。簡單來說，就是把常用的命令儲存在配置檔案裡，需要時用一個簡短的命令就能執行。比如啟動專案、構建專案、執行測試等，都可以定義成 npm script。

可以在 `package.json` 中定義常用的指令碼（讓 AI 幫你做這件事就好）：

```json
{
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint . --ext ts,tsx",
    "lint:fix": "eslint . --ext ts,tsx --fix",
    "format": "prettier --write \"src/**/*.{ts,tsx}\"",
    "type-check": "tsc --noEmit",
    "clean": "rm -rf dist node_modules",
    "fresh": "npm run clean && npm install"
  }
}
```

這樣配置後，執行 `npm run lint:fix` 就能自動修復程式碼格式問題，不用輸入老長一段命令。



#### Git 工作流自動化

Git 是目前最主流的分散式版本控制系統（Version Control System），是團隊協作開發不可或缺的工具。它可以儲存和管理檔案的所有更新記錄、並且使用 **版本號** 進行區分。從而支援將編輯後的文件恢復到修改前的狀態（歷史版本）、對比不同版本的檔案差異、防止舊版本覆蓋新版本等功能。

可以建立一些 Git 命令的別名，簡化常用命令：

```bash
# 在 ~/.gitconfig 中新增
[alias]
  st = status
  co = checkout
  br = branch
  ci = commit
  pl = pull
  ps = push
  lg = log --oneline --graph --decorate
  save = !git add -A && git commit -m 'WIP: save progress'
  undo = reset HEAD~1 --soft
```

這樣，`git st` 就等於 `git status`，`git save` 就能快速儲存進度。



#### 使用 GitHub Actions

GitHub Actions 是 GitHub 提供的自動化工作流工具，可以在程式碼提交、Pull Request 等事件觸發時自動執行任務。比如每次推送程式碼時自動執行測試、自動部署到伺服器、自動釋出新版本等，這樣就不用每次都手動操作了。

![利用 GitHub Actions 自動部署網站](https://pic.yupi.icu/1/1774937463974-f0f1cf86-da67-40ee-8cf9-abee42b66807.png)

配置 GitHub Actions 很簡單，只需要在專案的 `.github/workflows` 目錄下建立一個 YAML 配置檔案，編寫 GitHub Actions 自動化 CI/CD（持續整合/持續部署）的指令碼程式碼：

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '22'
      - run: npm install
      - run: npm run build
      - run: npm run test
      - name: Deploy to Vercel
        run: vercel --prod
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```

這個指令碼的作用是，當你推送程式碼到 main 分支時，GitHub 會自動檢出程式碼、安裝 Node.js 環境、安裝專案依賴、構建專案、執行測試、部署到 Vercel。整個過程全自動，你只需要推送程式碼就行了。

GitHub Actions 還有更多玩法，比如魚皮開源的 [AI 知識庫專案](https://github.com/liyupi/ai-guide) 利用它自動把文章的修改同步到網站。

![](https://pic.yupi.icu/1/image-20260104221153167.png)



### 適合所有人的效率工作流

上面講的都是比較技術性的自動化方法。其實，對於非程式設計師或初學者，也有一些通用的效率工作流。

1）使用零程式碼平臺：如果你不想處理這些複雜的配置，可以直接使用 Lovable 等零程式碼平臺。它們會自動處理構建、測試、部署等流程，你只需要專注於功能開發。

![](https://pic.yupi.icu/1/lovable.png)

2）利用 AI 生成配置：如果需要配置檔案，直接讓 AI 幫你生成。

比如：請幫我生成一個 GitHub Actions 配置，自動修復倉庫的 Issues。

AI 會給你完整的配置，你複製貼上就行。

![](https://pic.yupi.icu/1/1774940470510-d1d080c2-1b43-40f8-a4c8-da6b99baceba.png)

3）使用一鍵部署：很多平臺（比如 Vercel、Netlify、EdgeOne Pages）支援一鍵部署專案，連線 GitHub 倉庫後，每次推送程式碼就會自動觸發部署，不需要額外配置。甚至還可以利用 MCP 讓 AI 幫你直接完成部署，連部署平臺都不用自己登入。

![](https://pic.yupi.icu/1/1752212029384-16cfba8f-babb-49c0-9d41-3b76ee78eecf.png)



## 六、程式碼複用和模組化

把常用的程式碼封裝成可複用的模組，不要重複造輪子，還能讓 AI 更快速地定位到要修改的內容。



### 建立元件庫

如果你經常做類似的專案，可以建立一個自己的元件庫。

比如，你可能經常需要這些元件：
- 按鈕（Button）
- 輸入框（Input）
- 卡片（Card）
- 模態框（Modal）
- 載入動畫（Loading）

把這些元件做成通用的，放在一個單獨的資料夾裡：

```
/components
  /ui
    - Button.tsx
    - Input.tsx
    - Card.tsx
    - Modal.tsx
    - Loading.tsx
```

每個元件都要：
- 有清晰的 Props 介面
- 支援自定義樣式
- 有使用示例

這樣，下次做新專案時，直接複製這個資料夾就行了。



### 封裝常用函式

把常用的工具函式封裝起來，避免每次都重新寫或讓 AI 生成。比如日期格式化、防抖函式、生成 ID、複製到剪貼簿這些功能，幾乎每個專案都會用到。把它們整理成一個工具函式庫，需要時直接匯入使用，比每次都讓 AI 重新生成要快得多。

```typescript
// lib/utils.ts

// 格式化日期
export function formatDate(date: Date): string {
  return date.toLocaleDateString('zh-CN');
}

// 防抖
export function debounce<T extends (...args: any[]) => any>(
  fn: T,
  delay: number
): (...args: Parameters<T>) => void {
  let timer: NodeJS.Timeout;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => fn(...args), delay);
  };
}

// 生成隨機 ID
export function generateId(): string {
  return Math.random().toString(36).substring(2, 9);
}

// 複製到剪貼簿
export async function copyToClipboard(text: string): Promise<boolean> {
  try {
    await navigator.clipboard.writeText(text);
    return true;
  } catch {
    return false;
  }
}
```




### 使用程式碼片段（Snippets）

在編輯器中建立程式碼片段，快速插入常用程式碼。

比如在 VS Code 中，你可以建立一個前端 React 元件的片段。具體方法是：

1）按 `Cmd/Ctrl + Shift + P` 開啟命令面板，輸入 "Snippets"，選擇 "Configure Snippets"：

![](https://pic.yupi.icu/1/image-20260104214112119.png)

2）然後選擇對應的語言（如 typescriptreact.json），就可以新增自定義片段了。

比如：

```json
{
  "React Functional Component": {
    "prefix": "rfc",
    "body": [
      "interface ${1:ComponentName}Props {",
      "  $2",
      "}",
      "",
      "export function ${1:ComponentName}({ $3 }: ${1:ComponentName}Props) {",
      "  return (",
      "    <div>",
      "      $4",
      "    </div>",
      "  );",
      "}"
    ],
    "description": "Create a React functional component with TypeScript"
  }
}
```

![](https://pic.yupi.icu/1/image-20260104214219382.png)

配置完成後，輸入 `rfc` 再按 Tab，就能快速生成元件模板。

![](https://pic.yupi.icu/1/image-20260104214331581.png)




### 建立程式碼庫

把你做過的好的程式碼儲存起來，建立一個專屬於你的程式碼庫。

舉個例子，可以用這樣的結構：

```
/my-code-library
  /react
    /hooks
      - useLocalStorage.ts
      - useDebounce.ts
      - useFetch.ts
    /components
      - Button.tsx
      - Modal.tsx
    /utils
      - format.ts
      - validate.ts
  /node
    /middleware
      - auth.ts
      - cors.ts
    /utils
      - db.ts
      - email.ts
```

需要時，直接從這裡複製就好。




## 七、模板專案的建立

如果你經常做某一類專案，可以建立一個模板專案。




### 什麼是模板專案？

模板專案是一個預先配置好的專案骨架，包含了：

- 基本的目錄結構
- 常用的依賴包
- 配置檔案（如 tsconfig.json 等）
- 基礎元件和工具函式
- README 和文件模板

有了模板專案，開始新專案時就不用從零配置了。

就像我自己，做了幾十個專案後，積累了不少模板。現在每次開始新專案，我會先找一個類似的老專案，然後告訴 AI：“請參考這個專案的技術棧和目錄結構來建立新專案。” 這樣 AI 就能生成一個和我習慣一致的專案結構，省去了很多配置的時間。

下面舉幾個例子，不懂前端技術的朋友可以直接跳過。




### 建立 React 專案模板

比如，你可以建立一個 React + TypeScript + Tailwind 的模板：

```bash
my-react-template/
├── src/
│   ├── components/
│   │   └── ui/          # 基礎 UI 元件
│   ├── lib/
│   │   ├── api.ts       # API 呼叫封裝
│   │   └── utils.ts     # 工具函式
│   ├── hooks/           # 自定義 Hooks
│   ├── types/           # TypeScript 型別
│   ├── App.tsx
│   └── main.tsx
├── public/
├── .cursor/rules/       # Cursor 專案規則
├── AGENTS.md            # AI Agent 指令
├── tsconfig.json
├── package.json
└── README.md
```

開始新專案時，複製這個模板，改個名字就能用。



### 建立 Next.js 專案模板

如果你常用 Next.js，也可以建立一個模板：

```bash
my-nextjs-template/
├── app/
│   ├── (auth)/          # 認證相關頁面
│   ├── (dashboard)/     # 後臺頁面
│   ├── api/             # API 路由
│   ├── layout.tsx
│   └── page.tsx
├── components/
├── lib/
├── public/
├── .env.example         # 環境變數模板
├── next.config.ts
└── README.md
```

`.env.example` 裡列出需要的環境變數：

```
# 資料庫
DATABASE_URL=

# 認證
NEXTAUTH_SECRET=
NEXTAUTH_URL=

# API Keys
OPENAI_API_KEY=
```

這樣新專案開始時，就知道需要配置哪些環境變數。



### 使用 GitHub 模板倉庫

可以把你的模板專案放在 GitHub 上，設定為 `Template repository` 模板倉庫。

![](https://pic.yupi.icu/1/image-20260104215020646.png)

這樣建立新專案時，點選 `Use this template` 就能快速復刻專案模板了：

![](https://pic.yupi.icu/1/image-20260104215101657.png)

除了自己建立模板，你還可以使用別人的模板。在 GitHub 上搜尋 "react template"、"nextjs starter" 等關鍵詞，能找到很多優秀的模板專案。優先選擇 Star 數多、更新活躍的專案。

![](https://pic.yupi.icu/1/image-20260104215329685.png)

然後點選 "Use this template" 就能基於它建立自己的專案。這樣能站在巨人的肩膀上，節省大量配置時間。



## 八、提示詞模板庫

建立自己的提示詞模板庫，常用的對話可以直接複用。

除了自己整理，還可以參考一些現成的資源：

- [魚皮的 AI 資源導航](https://ai.codefather.cn/prompt)：收錄了大量提示詞模板，涵蓋各種場景。
- [Cursor Directory](https://cursor.directory/rules)：社群貢獻的 Cursor Rules 集合，有各種語言和框架的規則模板。
- [GitHub awesome-prompts](https://github.com/f/awesome-chatgpt-prompts)：收錄了大量優質提示詞，雖然不是專門針對程式設計的，但很多思路可以借鑑。

這些資源都可以直接拿來用，或者根據自己的需求改改。站在巨人的肩膀上，能節省大量摸索的時間。

下面給大家舉幾個例子。

1）功能開發模板

```
我要開發一個【功能名稱】功能。

需求：
1. 【需求 1】
2. 【需求 2】
3. 【需求 3】

技術棧：【技術棧】

請幫我：
1. 分析實現方案
2. 列出需要的元件和函式
3. 給出核心程式碼
```



2）程式碼審查模板

```
請審查這段程式碼：

【程式碼】

請從以下角度分析：
1. 程式碼質量（可讀性、可維護性）
2. 效能問題
3. 潛在的 bug
4. 改進建議
```



3）除錯問題模板

```
我遇到了一個問題：

問題描述：【問題描述】

報錯資訊：
【錯誤資訊】

相關程式碼：
【程式碼】

技術棧：【技術棧】

請幫我：
1. 分析問題原因
2. 給出解決方案
3. 解釋為什麼會出現這個問題
```



4）效能最佳化模板

```
這段程式碼的效能不夠好：

【程式碼】

場景：【使用場景和資料規模】

請幫我：
1. 分析效能瓶頸
2. 給出最佳化方案
3. 說明最佳化後的效能提升
```



5）文件生成模板

```
請為這個【元件/函式】生成文件：

【程式碼】

文件應該包括：
1. 功能說明
2. 引數說明
3. 返回值說明
4. 使用示例
5. 注意事項
```

把這些模板儲存在一個檔案裡，需要時直接複製貼上，並填入具體內容。



## 九、時間管理技巧

效率不只是技術問題，也是時間管理問題。很多時候，不是你技術不行，而是時間沒管理好。

分享幾個我自己在用的方法吧：

1）番茄工作法：設定 25 分鐘的專注時間，在這段時間內只做一件事，不看手機、不刷社交媒體。時間到了就休息 5 分鐘，起來走走、喝口水。這樣工作 4 個番茄鍾後，休息 15 ~ 30 分鐘。這個方法能讓你保持高效，又不會太累。

2）把大任務分解成小任務：比如 “完成使用者系統” 這個任務太大了，不知道從哪裡開始。但如果拆成實現使用者登錄檔單、實現表單驗證、連線註冊 API、新增錯誤提示、測試註冊流程這樣的小任務，每個都很具體，很容易完成、也更有成就感。

3）批次處理：把相似的任務放在一起做，比如一次性寫完所有元件的基本結構、一次性新增所有的型別定義、一次性處理所有的樣式問題。這樣能減少上下文切換，大腦不用頻繁在不同型別的工作間切換，效率會更高。

4）最後，不要在 MVP 階段就追求完美。先讓功能能用，再考慮最佳化；先完成核心功能，再新增輔助功能；先透過測試，再重構程式碼。

**記住，完成比完美更重要！**



## 寫在最後

效率提升不是一蹴而就的，而是透過無數個小改進積累起來的。每個快捷鍵、每個模板、每個自動化指令碼，都能為你節省一點時間。積少成多，你的開發速度就會有質的飛躍。

建議你定期記錄自己的工作流程，看看哪些步驟最耗時、哪些操作重複最多、哪些地方可以自動化，然後針對性地改進。同時保持對新工具的關注，關注技術部落格和社群，嘗試新的 AI 工具，學習新的快捷鍵和技巧。但也不要盲目追新，雖然 AI 工具的迭代更新非常快，但真正好用的、適合自己的也就那麼幾個，還是要選擇真正能提高效率的工具。

向他人學習也很重要，比如看別人的直播或影片、參加技術分享會、加入開發者社群等等，多觀察其他開發者的工作方式，學習他們的效率技巧，你的效率也會越來越高。

當然，咱不能為了追求效率丟失掉程式碼質量。下一篇文章，我會講解程式碼質量保障，教你如何保證 AI 生成的程式碼質量。

休息片刻，讓我們再繼續征程吧！




## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)
