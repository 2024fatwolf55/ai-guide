# Agent Skills：通用 AI 技能庫

> 讓 AI 快速學會新技能



你好，我是程式設計師魚皮。

在前面的文章中，我們學習瞭如何用 AI 生成程式碼。但你可能會發現一些問題：

- AI 生成的介面總是千篇一律的藍紫漸變色
- 每次都要輸入一大段相同的提示詞，太麻煩了
- AI 在某些特定任務上表現不夠專業

有沒有辦法讓 AI 快速學會新技能，變得更專業呢？

這篇文章，我會介紹 **Agent Skills**，Anthropic 推出的 AI 技能系統，可以讓 AI 快速掌握各種專業技能。

⭐️ 推薦觀看影片動畫版，更通俗易懂：[https://bilibili.com/video/BV1T7zzBQEaA](https://www.bilibili.com/video/BV1T7zzBQEaA/)



## 一、沒有 Agent Skills 之前

在瞭解 Agent Skills 之前，讓我們先看看以前是怎麼解決這些問題的。

假設你正在用 AI 開發網站，為了讓 AI 生成的效果更好，你告訴 AI：

- 介面不要使用藍紫漸變色
- 不要生成一大堆沒用的文件
- 你要遵循公司的程式碼規範

阿巴阿巴，洋洋灑灑幾百字。

![](https://pic.yupi.icu/1/1769306620114-3ddb877f-7e14-4e89-abbe-bcd19c33c9ff.png)

之後每次開發網站時，你都要寫這麼一段又臭又長的提示詞，太麻煩了！

於是聰明的你開始想辦法。

先把常用的提示詞儲存到單獨的檔案（比如 `prompts.md`），每次手動投餵給 AI。

![](https://pic.yupi.icu/1/1769306653314-5b3a0f47-eff0-4c1c-9b9c-26139abfee80.png)

然後建立了資原始檔夾，把公司的程式碼規範、設計素材都塞進去，告訴 AI 參考這些寫。

![](https://pic.yupi.icu/1/1769306679682-3f1a3eae-893e-4860-b97d-c7f91b111a8b.png)

接著你還寫了一些指令碼，讓 AI 生成程式碼後自動執行格式化、執行測試、提交程式碼到 Git。

![](https://pic.yupi.icu/1/1769306691846-4dcf892d-1969-40ae-8e73-b7c5c5c5d018.png)

最後再寫個 `AGENTS.md` 檔案，把所有規範和工作流程都寫進去，讓 AI 自動讀取。

你沾沾自喜：嘿嘿，俺這套工作流，堪稱完美！

![](https://pic.yupi.icu/1/1769306725742-e3c9a7e4-f18b-469c-b3d3-78f38ea8a37e.png)

但很快，你發現了問題，隨著規範越寫越多，文件越來越臃腫，每次對話都要佔用很多 AI 上下文空間，浪費 tokens。

![](https://pic.yupi.icu/1/1769306754832-fad954ff-b289-4e02-a714-e5ca7dafc9cc.png)

這時候，Agent Skills 就該登場了！



## 二、什麼是 Agent Skills？

[Agent Skills](https://claude.com/blog/skills) 是 Anthropic 推出的 [一套開放標準](https://platform.claude.com/docs/zh-CN/agents-and-tools/agent-skills/overview)，目的是讓 AI 能夠學習使用各種專業技能，而不用每次都重複輸入提示詞。

![](https://pic.yupi.icu/1/1769306883902-94de7351-58e4-43ae-86da-e017725d59cc.png)

它定義了一種 **封裝 AI 工作流** 的標準：開發者可以把複雜的任務指令、指令碼和資源打包成一個 **技能（Skill）**；作為使用者，你只需要安裝這些技能，AI 就能立刻學會這項本事，不用重複造輪子。

簡單來說，它就是給 AI 裝備的 **技能包**。技能包裡有精心設計的提示詞、程式碼指令碼、還有各種資原始檔。

![](https://pic.yupi.icu/1/1769306811193-2ee3acbc-5e36-46c2-8d08-b2682494fb56.png)

把 AI 想象成一個職場小白，給他裝上 `文件處理技能`，它就立刻知道怎麼生成 PPT、處理 Excel 表格；裝上 `程式碼規範技能`，它就知道怎麼按照公司標準寫程式碼。

![](https://pic.yupi.icu/1/1769306900359-2a2b73da-a366-411d-ad3b-2ae61f6b5bc4.png)

你可能會想：等等，這不就是把教 AI 做事的文件和 AI 要用到的檔案打包成資料夾嗎？

![](https://pic.yupi.icu/1/1769306918453-1b2d34df-db49-4932-88cd-89eec0c9f773.png)

沒錯，差不多就是這個意思。但 Anthropic 把它做成了一個通用標準，而且在實現原理上有一些新花樣。下面我們先來實戰使用一下 Agent Skills，再揭秘其中的奧秘。



## 三、Agent Skills 入門實戰

目前對 Agent Skills 支援最完善的工具是 Anthropic 官方的 [Claude Code](https://claude.com/product/claude-code)，我們就以此為例，安裝並使用 Skills。

![](https://pic.yupi.icu/1/1769306959992-8489754c-6a63-4685-b804-f27836e92df8.png)



### 1、安裝 Skills 技能

先開啟 Claude Code 並輸入命令，新增官方技能市場：

```plain
/plugin marketplace add anthropics/skills
```

![](https://pic.yupi.icu/1/1769307009465-4e04d585-3f68-4fcb-a3b0-ba43ad70139a.png)

這就像是在你的 AI 助手裡開通了一個技能商店，接下來你就可以從商店中獲取技能了。

![](https://pic.yupi.icu/1/1769307026089-70a117da-b18e-4c7d-992b-1d08e30a7a0b.png)

在 Claude Code 中輸入命令，安裝官方提供的技能包：

```plain
/plugin install example-skills@anthropic-agent-skills
```

![](https://pic.yupi.icu/1/1769307063576-10e2ce68-b5cd-41c7-8d6c-da0781298929.png)

這個 example-skills 包含了一堆官方示例技能，包括前端設計、網頁測試、動圖製作等等。

![](https://pic.yupi.icu/1/1769307079120-6aaf2999-fee5-4fdb-a5e3-2ba66824b4de.png)

裝完之後，你就可以直接讓 AI 使用這些技能了。

還有另外一種安裝方式，也可以在 Claude Code 中輸入一行命令來安裝 [frontend-design](https://www.claudeskill.site/en/skills/anthropic-agent-skills:frontend-design) 技能。

```markdown
skill install anthropic-agent-skills:frontend-design
```



### 2、前端設計技能

比如你要做一個網站，以前沒裝技能的時候，AI 生成的程式碼又是那個熟悉的藍紫漸變色，千篇一律的 AI 審美。

![](https://pic.yupi.icu/1/1769307096370-df6a9ece-2720-4e1d-b725-431eb4e54afa.png)

現在安裝了 frontend-design 這個 **教 AI 生成專業設計感網站** 的技能後，你輸入：“幫我開發個人作品集網站”。

AI 會主動問你：我發現你安裝了前端設計技能，需要用它來生成更具設計感的頁面嗎？

![](https://pic.yupi.icu/1/1769307135496-aa2a1e4e-4e8a-43e5-a138-9a148410b52e.png)

確認之後，AI 會利用技能生成程式碼，告別藍紫漸變，生成獨特風格的精美頁面。

![](https://pic.yupi.icu/1/1769307161745-c81ca221-9902-49dd-96de-a99d50a17684.png)

我們不用每次都給 AI 輸入一大堆相同的提示詞，裝一次技能就行了。



### 3、文件處理技能

除了程式碼相關的技能，官方還提供了文件處理技能包。

![](https://pic.yupi.icu/1/1769307180929-3b2d4bcf-c1a7-40e0-831d-336c78b9ccb8.png)

同樣在 Claude Code 中輸入一行命令安裝：

```plain
/plugin install document-skills@anthropic-agent-skills
```

![](https://pic.yupi.icu/1/1769307200501-48c05a43-75d0-4cf9-bc4f-3f89554f6295.png)

這個技能包裡有 PPT 製作、Word 文件生成、Excel 資料分析、PDF 解析等技能。

![](https://pic.yupi.icu/1/1769307220369-c4c7889b-6ddc-4f29-8247-9fe02af6d3eb.png)

接下來如果你讓 AI 做個 PPT，它會自動呼叫 PPT 製作技能，直接生成排版好的 PPT 檔案，幫你節省幾個小時。

![](https://pic.yupi.icu/1/1769141161384-f52f68b1-9260-4ae2-bf92-f418673660e6.png)

![](https://pic.yupi.icu/1/1769307245673-c64d081e-09c5-4cee-a3a2-7eaa0e1c98ad.png)



## 四、揭秘 Agent Skills 內部原理

你可能會好奇：為什麼 Skills 能做到安裝即用？技能包裡面到底有啥？AI 又是怎麼知道該用哪個技能的？

[技能](https://agentskills.io/what-are-skills) 其實就是一個包含 `SKILL.md` 技能說明檔案的資料夾，還可以包含可執行指令碼、資源和參考文件。

![](https://pic.yupi.icu/1/1769307275438-55f0f5fb-b429-43cc-9964-c48486af404e.png)

```markdown
my-skill/
├── SKILL.md          # 必需：指令和後設資料
├── scripts/          # 可選：可執行指令碼
├── references/       # 可選：參考文件
└── assets/           # 可選：模板和資源
```

由於每個技能的複雜度不同，結構也會存在區別。我們可以在本地目錄中找到已安裝的技能資料夾。

![](https://pic.yupi.icu/1/1769141068658-ef05e94f-380b-4784-b78c-2c588289832a.png)

以官方的 PPT 製作技能為例，它的結構是這樣的：

```plain
skills/pptx/
├── SKILL.md          # 技能說明書（必需）
├── ooxml/            # OOXML 相關資源
├── scripts/          # 處理指令碼
├── html2pptx.md      # HTML 轉 PPT 說明
├── ooxml.md          # OOXML 格式說明
└── LICENSE.txt       # 許可證
```

包含一個核心的技能說明文件 `SKILL.md`，還有指令碼、參考文件和各種資原始檔。

![](https://pic.yupi.icu/1/1769307298133-872126c8-e0b4-4264-8914-33ddea77c83d.png)

而 frontend-design 前端設計技能只有一個 `SKILL.md` 檔案。

![](https://pic.yupi.icu/1/1769307312566-e868eead-6723-42e1-80ba-fbffd9976cf2.png)



### SKILL.md 檔案結構

`SKILL.md` 檔案是每個技能的核心，它包含兩個關鍵部分。

第一部分是 **後設資料**，用 YAML 格式寫在檔案開頭：

```yaml
---
name: frontend-design
description: 生成具有專業設計感的前端程式碼，避免千篇一律的 AI 審美
---
```

其中 `name` 是技能的名字。`description` 是技能的描述，告訴 AI 什麼時候應該使用這個技能。描述寫得越清晰，AI 就越容易在合適的時機呼叫它。

![](https://pic.yupi.icu/1/1769307333844-a1c504a9-0bf9-41b0-ac0b-364e4edf881d.png)

第二部分是 **指令內容**，就是一套經過精心設計的提示詞，指導 AI 具體怎麼做。

以 [frontend-design](https://github.com/anthropics/skills/blob/main/skills/frontend-design/SKILL.md) 技能為例，它的指令內容包括：

- 設計思考：在寫程式碼前，先分析產品目的、使用者群體、技術約束，然後選擇一個大膽的美學方向（極簡、復古未來、工業風、有機自然、奢華精緻等）
- 前端美學指南：包括字型選擇（避免 Arial、Inter 等爛大街字型，選擇有個性的組合）、配色主題（主色調配鮮明點綴色）、動效設計、空間構成、背景和視覺細節
- 避坑指南：明確禁止紫色漸變、系統字型、千篇一律的佈局等 AI 審美陷阱

![](https://pic.yupi.icu/1/1769307344477-48419e65-53ea-4cfe-a495-f70be84b2afe.png)



### 漸進式披露機制

如果有多個 Skills，AI 怎麼知道該用哪個技能呢？如果把每個技能說明文件都塞給 AI，不是很佔用上下文麼？

這就要說到 **漸進式披露（Progressive Disclosure）** 這個核心機制了。

當你讓 AI 執行任務時，它會先掃描技能目錄，但不會把所有內容都載入到上下文中。而是隻讀取每個技能的後設資料（名字和描述），發現描述和任務相關，就知道該用這個技能了。

![](https://pic.yupi.icu/1/1769307378437-dce56ae8-4336-47c1-9ac6-dc39776222c7.png)

然後才把完整的技能說明文件讀進來，按照裡面的指令執行：

![](https://pic.yupi.icu/1/1769307391204-f81c2a91-e21e-46bb-a49f-205196aa7774.png)

並根據需要載入技能包中的其他資源：

![](https://pic.yupi.icu/1/1769307417577-6c55f619-9bf2-43d5-bc76-80f65c3db3c4.png)

**用到哪個查哪個**，既精準匹配又節省上下文，這就是漸進式披露的精髓。

所以 Agent Skills 的本質就是 **把專業知識打包成一個資料夾，讓 AI 按需讀取並使用**。

![](https://pic.yupi.icu/1/1769307432541-5753722e-ba96-404a-b042-c130afb4378f.png)



## 五、跨工具使用 Agent Skills

除了 Claude Code 之外，其他 AI 工具支援 Agent Skills 嗎？

當然！[Agent Skills](https://agentskills.io/) 已經成為通用標準，Cursor、VS Code、Codex 等工具都支援。

![](https://pic.yupi.icu/1/1769307453878-b670716c-f2c7-4eb4-9986-671a7b42b480.png)

Skills 的社群也非常活躍，你可以在 [Claude Skills Hub 市場](https://www.claudeskill.site/zh/skills)、開源的 [Awesome Claude Skills](https://github.com/ComposioHQ/awesome-claude-skills) 等地方找到很多現成的技能。

![](https://pic.yupi.icu/1/1769307598569-a61f88f7-5b26-41fe-a302-652034ed655c.png)

比如有個叫 [UI UX Pro MAX](https://ui-ux-pro-max-skill.nextlevelbuilder.io/) 的技能特別火，專門用於提升 AI 的設計能力。

![](https://pic.yupi.icu/1/1769307611502-fa3224d8-9e04-41cd-848a-de9619edf762.png)



### 在 Cursor 中使用 Agent Skills

用法很簡單，首先按照 [開源倉庫文件](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) 的指引，安裝官方提供的命令列工具：

```bash
npm install -g uipro-cli
```

![](https://pic.yupi.icu/1/1769307627168-c682f14b-4517-4325-ad4a-33e88661e714.png)

然後進入到你的專案目錄下，根據使用的 AI 工具執行對應的命令。比如我這裡用 Cursor：

```bash
uipro init --ai cursor
```

![](https://pic.yupi.icu/1/1769307641070-2138ef02-8f26-460a-8cdd-979c59b725de.png)

它會自動把技能安裝到 Cursor 的配置目錄裡。

![](https://pic.yupi.icu/1/1769307669797-86215fbf-b9de-436f-9864-460eb307c5c5.png)

安裝完成後，可以看到它的檔案結構：

![](https://pic.yupi.icu/1/1769307694431-c4ad6aa0-b559-4ae5-8573-0687948551f2.png)

接下來，當你讓 AI 開發一個網站時，可以使用斜槓命令手動觸發技能，或者讓 AI 自動識別技能。

![](https://pic.yupi.icu/1/1769307707968-1545cef4-b8e2-4bf9-b0a7-98130afc78ba.png)

AI 會根據你的需求識別出產品型別和需要的頁面型別：

![](https://pic.yupi.icu/1/1769307720984-a6afcae8-a5e8-4577-be7c-8356b42832ee.png)

然後呼叫 `search.py` 搜尋指令碼，在 data 目錄裡進行多維度搜尋，找到適合的配色、字型、佈局風格：

![](https://pic.yupi.icu/1/1769307768048-ef58645a-6188-4af7-9865-8033602126f7.png)

綜合搜尋結果，生成完整的設計方案（主色調、字型組合、間距規範等）：

![](https://pic.yupi.icu/1/1769307782038-59ea2231-b43d-45e3-a39f-6c36b0c7f645.png)

最後，再按照設計方案生成程式碼：

![](https://pic.yupi.icu/1/1769307794443-ffc76a7e-24e9-4e4d-b973-ef97285fd32b.png)

這樣一來，生成的介面既專業又有設計感。

![](https://pic.yupi.icu/1/1769307819333-fef63881-90b7-4248-8ca7-35354f8a7a7a.png)

AI 不需要把所有規則都背下來，而是用到哪個查哪個，這就是 Agent Skills 的精髓。



## 六、技能倉庫

目前 [Anthropic 官方技能倉庫](https://github.com/anthropics/skills) 已經提供了豐富的技能集合，涵蓋程式設計相關的前端設計、網頁測試，還有辦公相關的 PPT 製作、Excel 處理、Word 文件、PDF 生成等各個方面。

Skills 的社群也非常活躍，你可以在以下地方找到很多現成的技能：

- ⭐️ [魚皮 AI 導航 - Skills 大全](https://ai.codefather.cn/skills)：持續更新優質技能，釋放 AI 執行潛力
- [Claude Skills Hub 市場](https://www.claudeskill.site/zh/skills)：社群技能市場
- [Awesome Claude Skills](https://github.com/ComposioHQ/awesome-claude-skills)：開源技能列表
- [mattpocock/skills](https://github.com/mattpocock/skills)：18 萬 Star 的個人技能庫，把測試驅動開發、Bug 診斷等軟體工程方法論封裝成了 Skill，詳細介紹可以閱讀本目錄中的《Matt Pocock Skills：真實工程技能庫》

![](https://pic.yupi.icu/1/image-20260201150711260.png)



## 七、建立自己的 Agent Skills

用了很多別人的技能後，你可能會想：能不能把公司的週報格式封裝成一個技能？以後推薦給新來的同事，還能賣個幾塊錢，嘿嘿嘿~

當然可以！建立自己的 Agent Skills 其實很簡單。



### 方法 1、手動建立

你可以發揮程式設計師最擅長的事情 —— 複製貼上！

![](https://pic.yupi.icu/1/1769307876115-a6e9c6ce-df5a-48c0-9330-120441bd5e28.jpeg)

先複製一個官方的技能包，修改目錄名稱為自己的。

然後修改技能說明文件 `SKILL.md` 的後設資料、指令內容這些關鍵部分。

![](https://pic.yupi.icu/1/1769307911844-3b48f4ab-6aa4-4c96-8bcf-8d30bd1475a3.png)

示例 `SKILL.md` 檔案：

```markdown
---
name: company-weekly-report
description: 生成符合公司規範的專案週報，包含進度彙總、問題跟蹤和下週計劃
---

# 公司週報生成技能

當使用者要求生成周報時，請按以下步驟執行：

## 1. 收集資訊
- 詢問本週完成的主要工作
- 詢問遇到的問題和解決方案
- 詢問下週計劃

## 2. 格式規範
- 使用公司藍色主題
- 標題使用微軟雅黑加粗
- 每個模組不超過 5 個要點

## 3. 輸出格式
- 預設輸出 Markdown
- 如需 PPT，呼叫 pptx 技能
```

最後，把公司的 Logo、PPT 模板、報告樣例放在子資料夾裡就行了。媽媽再也不用擔心我的週報了~

![](https://pic.yupi.icu/1/1769307957544-4bcb77d5-71f4-48c5-a51e-a830b7ef4f36.png)



### 方法 2、使用 Skill Creator

其實有更簡單規範的方法。

在前面安裝的 example-skills 官方示例技能包裡，有一個叫 `Skill Creator` 的技能，專門用來幫你建立新技能。

![](https://pic.yupi.icu/1/1769307969338-97a16e2a-6581-4215-b399-7aa30f715ad1.png)

你只需要跟 AI 說：“幫我建立一個專門生成公司週報的技能”

接下來 AI 會問你幾個問題，一步一步回答就好：

- 你希望週報包含哪些主要部分？
- 你希望週報以什麼格式輸出？
- 你通常會如何使用這個週報技能？
- 希望週報的語言風格是什麼？

![](https://pic.yupi.icu/1/1769307998192-27ac24c2-c732-401d-a19e-ebe07086d73b.png)

很快，一個完整的技能包就生成了，你會看到一個 `.skill` 為字尾的檔案，本質上是一個 zip 壓縮包。

![](https://pic.yupi.icu/1/1769308022759-0eb5bf27-e953-4a32-85e0-9524c0ff5ab0.png)



### 技能的安裝位置

建立好技能後，你可以：

1）個人全域性使用：解壓到個人技能目錄（`~/.claude/skills/`）下，你的所有專案都能用

![](https://pic.yupi.icu/1/1769308081516-c52a79cc-0251-42d4-aaac-f08b1e38ef9e.png)

![](https://pic.yupi.icu/1/1769144854626-88c27a17-fa9d-4f6a-ba94-3747d61e0129.png)



2）專案內使用：放到專案的 `.claude/skills/` 目錄下，並且利用 Git 同步給專案組其他成員

![](https://pic.yupi.icu/1/1769308107094-ea5207a7-e231-45ee-a449-b42e13410f74.png)

![](https://pic.yupi.icu/1/1769144884089-6766753a-d945-446b-99ac-06dcd041a205.png)



3）分享給社群：把它開源到 GitHub，或者上傳到 [Claude Skills Hub](https://www.claudeskill.site/zh/skills) 這樣的社群平臺，讓所有使用者都能用

![](https://pic.yupi.icu/1/1769308134560-8cea0cba-cd0f-4610-aff0-38165872b586.png)



## 八、Skills / MCP / 斜槓命令的區別

你可能會好奇：Agent Skills 和 MCP、斜槓命令有什麼區別？

**MCP 就像給 AI 裝上了 “手和眼睛”**，讓 AI 能夠連線外部工具和資料來源，比如搜尋網頁、讀取程式碼倉庫、查詢資料庫。適合需要獲取資料或操作外部系統的場景。

![](https://pic.yupi.icu/1/1769308152531-a3770991-fc9c-4c44-b401-12c39a661d73.png)

**而 Agent Skills 更像是給 AI 發了一本 “工作手冊”**，把專業知識和工作流程打包起來，教 AI 在特定領域該怎麼做。

![](https://pic.yupi.icu/1/1769308164192-a35405c9-b8e0-480a-900b-6503b81f440a.png)

至於斜槓命令，它就像是快捷鍵，是需要你手動輸入 `/command` 命令來觸發的固定操作；而 Skills 的特點是 AI 可以自動識別該用什麼技能，不需要你顯式呼叫。

![](https://pic.yupi.icu/1/1769308180272-b4e2ecf6-7577-407d-99df-156f44c34c9b.png)

其實 MCP 和 Skills 是可以結合起來的。舉個例子，如果你想讓 AI 幫你發週報：

- MCP 負責獲取資料：從任務管理資料庫拉取這周的任務列表
- Skills 負責加工資料：把獲取到的原始資料整理成老闆愛看的格式

一個提供食材，一個提供配方。

![](https://pic.yupi.icu/1/1769308199144-45b3b07a-b27d-45e1-91ce-ca0afaced11c.png)



## 九、Agent Skills 憑什麼大火？

你可能會想：等等，這不就是我們程式設計師玩爛的 “封裝、複用、模組化、懶載入” 那一套嗎？

![](https://pic.yupi.icu/1/1769308235063-6469135d-6e72-4698-b040-0b9019fe29cd.png)

寫幾個程式碼檔案、打個包、發到網上，讓其他程式設計師下載下來用，不是一回事兒麼？

![](https://pic.yupi.icu/1/1769308248099-97a33447-0873-436a-b923-a15fd489bdc8.png)

為什麼 Agent Skills 能突然讓整個 AI 圈為之瘋狂？？？

從技術的角度來看，它並沒有發明什麼驚天動地的演算法。在我看來，它能火主要是 2 個原因。

第一，它是 **開放標準**，封裝一次技能包後就能在各種 AI 工具裡複用，還能透過社群共享。

![](https://pic.yupi.icu/1/1769308267503-7e42f21e-a9f3-46ad-b64e-eb389536194e.png)

更重要的是，Skills 能立刻讓 AI 的工作更專業可靠，讓普通人 “無感” 地享受技術帶來的價值。以前想讓 AI 變聰明，你得學提示詞工程、配置各種工具鏈。現在只需要像裝 APP 一樣安裝技能包，AI 就立刻變專業了。一項技術的成功，不在於它有多複雜，而在於它能讓普通使用者不關注技術細節的情況下，感受到技術的價值。

![](https://pic.yupi.icu/1/1769308278928-c64c92b1-6530-43e7-a35e-cfb6eeec975d.png)

**降低門檻，才是技術走向大眾的鑰匙。**

總結一下，Agent Skills 最大的優勢是：

1. 可複用性：安裝一次技能，以後就能直接使用，不用重複輸入提示詞
2. 跨工具通用：你在 Claude Code 中安裝的技能，以後在 Cursor 等其他工具中也能用
3. 社群驅動：任何人都可以建立和分享技能，整個社群的智慧都能為你所用
4. 降低門檻：像裝 APP 一樣簡單，讓普通使用者也能讓 AI 變得更專業



## 寫在最後

看到這裡，相信你已經對 Agent Skills 有了全面的瞭解。

**Agent Skills 讓 AI 能夠快速學會新技能，不用每次都重複輸入提示詞。** 它的本質是把專業知識和工作流程封裝成可複用的技能包，透過漸進式披露機制讓 AI 按需載入，既提升了 AI 的專業性，又節省了上下文空間。

Agent Skills 不僅僅是個技術概念，更是一種新的工作方式。你可以把它融入到自己的日常工作中，比如把重複的任務封裝成技能、把團隊的最佳實踐固化成技能，讓 AI 真正成為你的得力助手。

建議你：

1. 先安裝幾個官方技能，體驗一下 Agent Skills 的便利性
2. 嘗試在 Cursor 等其他工具中使用社群技能
3. 把工作中重複的任務封裝成自己的技能
4. 分享你的技能到社群，幫助更多人

在 Vibe Coding 時代，技術的門檻正在崩塌，而想象力的邊界正在無限擴張。

讓我們一起探索 Agent Skills 的更多可能性吧！

💡 想獲取更多優質 Skills 資源？可以閱讀《優質 AI 程式設計擴充套件推薦》中的 Agent Skills 技能類章節，裡面有 Skills 安裝管理工具、Skills 資源平臺和必裝推薦的彙總。



## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）魚皮的 Vibe Coding 教程：[免費開源的 AI 程式設計零基礎入門教程](https://github.com/liyupi/ai-guide)

3）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

4）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

5）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

6）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)
