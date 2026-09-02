# Claude Code 配置哲學：官方親自教你怎麼「調教」AI

> Anthropic 官方教你怎麼「調教」Claude Code

大家好，我是程式設計師魚皮。

最近 Anthropic 官方發了一篇博文，標題叫《Steering Claude Code》，把 Claude Code 的整套配置體系從底層邏輯到使用場景講了個透。

由於是官方團隊親自寫的，相當於出題人告訴你標準答案，因此整篇文章的乾貨價值非常高。

今天我結合官方內容加上我自己使用 Claude Code 的經驗，給大家做一個完整的中文解讀。

> 原文指路：https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more

![](https://pic.yupi.icu/1/image-20260625173136998.png)



## Claude Code 的調教方式

Claude Code 的調教方式共有 7 種：CLAUDE.md 檔案、Rules 規則、Skills 技能、Subagents 子智慧體、Hooks 鉤子、Output Styles 輸出風格，以及 Append System Prompt 系統提示詞追加。

每種方式的核心區別在於 3 點：

1. 什麼時候載入到上下文
2. 長對話壓縮時會不會被丟掉
3. 佔用多少 token

如果你把指令放錯了地方，AI 可能直接忽略掉你的指令，白白浪費 tokens。

接下來咱們挨個兒學習。

![Claude Code 七種調教方式總覽](https://pic.yupi.icu/1/01_%E4%B8%83%E7%A7%8D%E8%B0%83%E6%95%99%E6%96%B9%E5%BC%8F%E6%80%BB%E8%A7%88%E5%AF%B9%E6%AF%94%E5%9B%BEv2_compressed_v1.png)



## 1、CLAUDE.md - AI 的專案手冊

CLAUDE.md 是放在專案根目錄的 Markdown 檔案，會話一開始就載入，全程常駐在上下文中。

那 CLAUDE.md 裡適合放什麼內容呢？

像構建命令、目錄結構、程式碼規範、團隊約定這些 AI 需要 **時刻記住** 的事實性資訊。

我在自己的 [《AI 程式設計教程》](https://ai.codefather.cn/vibe) 中多次強調，CLAUDE.md 就像給新同事寫的專案文件。你不需要每次都跟 AI 解釋專案用的是什麼技術、有什麼規矩，只要寫一次，之後都會生效。

CLAUDE.md 的載入分兩種方式。

根目錄的 CLAUDE.md 是始終載入的，壓縮對話時也會重新讀取，不會丟失。

子目錄的 CLAUDE.md 比如 `app/api/CLAUDE.md`，只有當 Claude 讀取該目錄下的檔案時才會載入，適合放只跟特定模組相關的約定。

![CLAUDE.md 載入機制](https://pic.yupi.icu/1/02_CLAUDE.md%E5%8A%A0%E8%BD%BD%E6%9C%BA%E5%88%B6v2_compressed_v3.png)

官方明確建議，**CLAUDE.md 儘量控制在 200 行以內**。

原因很簡單，CLAUDE.md 的每一行都佔 token，不管當前任務會不會用到。

如果你塞了 500 行進去，哪怕做一個簡單的前端樣式調整，也得帶著那些後端部署規範一起載入，純屬浪費。

我自己就踩過這個坑，之前把所有東西都往 CLAUDE.md 裡堆，後來發現 AI 的指令遵循度明顯下降了，特別是在長對話裡。後來精簡了一波，把流程性的內容移到了 Skills 裡，效果立竿見影。

所以記住一個原則就好：**CLAUDE.md 只放「事實」，不放「流程」。**

![事實和流程對比](https://pic.yupi.icu/1/03_%E4%BA%8B%E5%AE%9Evs%E6%B5%81%E7%A8%8B-CLAUDE.md%E5%86%85%E5%AE%B9%E5%88%86%E7%B1%BB%E5%AF%B9%E6%AF%94_compressed_v1.png)

構建命令、技術棧、目錄結構、命名規範是事實。部署流程、程式碼審查清單、釋出步驟是流程，應該封裝為 Skills。



## 2、Rules 規則 - 路徑級的精準約束

Rules 是放在 `.claude/rules/` 目錄下的 Markdown 檔案，用來給 Claude 設定具體的約束或編碼規範。

它最強大的地方在於支援路徑作用域。你在規則檔案的頭部加一個 `paths` 欄位，就能讓這條規則只在 Claude 讀取特定路徑下的檔案時才生效。

比如我有一條規則是「所有 API 處理器必須使用 Zod 進行輸入驗證」，我把它的作用域設為 `src/api/**`。這樣當我只是在改前端頁面的時候，這條規則壓根不會載入，也就不浪費 token。

```yaml
---
paths:
  - "src/api/**"
  - "**/*.handler.ts"
---
所有 API 處理器必須使用 Zod 進行輸入驗證。
```

我自己在專案中就是這麼用的，把資料庫相關的規範限定在 `src/db/**` 下面，前端相關的限定在 `src/components/**` 下面，各管各的。

什麼時候該用 Rule，而不是子目錄 CLAUDE.md 呢？

答案是：當一條規範需要跨目錄生效的時候。

比如所有 `.test.ts` 檔案都要遵守某個測試規則，用路徑作用域的 Rule 更合適。子目錄 CLAUDE.md 只能管它所在那個目錄下面的檔案。



## 3、Skills 技能 - 按需載入的工作流

Skills 放在 `.claude/skills/` 目錄下，每個技能是一個資料夾，核心是一個 `SKILL.md` 描述檔案。

Skills 的漸進式載入設計非常優雅。會話開始時，Claude 只會讀取每個 Skill 的名稱和簡短描述，完整的技能內容只有在被觸發時才載入到上下文中。

![Skills漸進式載入設計](https://pic.yupi.icu/1/04_Skills%E6%B8%90%E8%BF%9B%E5%BC%8F%E5%8A%A0%E8%BD%BD%E8%AE%BE%E8%AE%A1%E5%9B%BEv2_compressed_v3.png)

這意味著你可以定義幾十個 Skills，但平時它們幾乎不佔 token。只有當你主動呼叫（比如輸入 `/code-review`），或者 AI 自動匹配到當前任務需要某個技能時，完整的指令內容才會載入進來。

我在 `.claude/skills/` 下面放了部署流程、程式碼審查清單、建立新元件的標準步驟等等。這些流程性的東西如果全寫在 CLAUDE.md 裡，哪怕你只是說個「你好」，就得白白浪費不知道多少 tokens。放在 Skills 裡就不一樣了，需要時才載入。

還有個很重要的細節。壓縮對話時，已觸發的 Skills 會按總預算重新注入，如果預算不夠，最早觸發的技能會被優先丟棄。所以一次會話裡別觸發太多 Skills，聚焦當前任務最重要。



## 4、Subagents 子智慧體 - 隔離的獨立助手

Subagents 放在 `.claude/agents/` 目錄下，每個檔案定義一個獨立的 AI 助手。

跟 Skills 最大的區別在於，Subagent 執行在自己獨立的上下文視窗裡，只有最終結果會返回給主會話。所有中間過程完全不佔用你主對話的上下文空間。

![Subagents 隔離上下文執行機制](https://pic.yupi.icu/1/05_Subagents%E9%9A%94%E7%A6%BB%E4%B8%8A%E4%B8%8B%E6%96%87%E8%BF%90%E8%A1%8C%E6%9C%BA%E5%88%B6%E5%9B%BEv2_compressed_v1.png)

什麼場景適合用 Subagent 呢？

比如深度搜尋程式碼庫找某個 Bug 的根因、分析日誌檔案定位效能瓶頸、做依賴審計檢查哪些包有安全漏洞。這類任務的中間過程可能產生幾萬 token 的內容，如果都堆在主對話裡，很快就會把上下文撐爆。

Subagent 還支援巢狀，最多可以巢狀 5 層深，配合動態工作流可以編排幾十甚至上百個後臺 Agent 並行工作。

我之前用 Claude Code 的 `/batch` 命令批次遷移 API 版本，本質上就是在用 Subagent。它會自動把任務拆成十幾個子任務，每個在獨立工作樹中執行，互不干擾。

那 Skills 和 Subagents 怎麼選呢？

很簡單，如果你想看到 AI 的執行過程並隨時干預，用 Skill。如果你只關心最終結果、不想被中間資訊干擾，用 Subagent。



## 5、Hooks 鉤子 - 確定性的自動化

Hooks 是 7 種方式裡最特殊的一個。

前面講的 CLAUDE.md、Rules、Skills 本質上都是給 AI 的「建議」，AI 可能遵循也可能不遵循，特別是在長會話或複雜場景下。

但 Hooks 不一樣，它不是指令，而是自動化程式碼。**到了觸發條件就一定會執行**，不需要 AI 來決定要不要做。

Hooks 透過 `settings.json` 註冊，繫結到 Claude Code 生命週期中的特定事件，比如工具呼叫前（PreToolUse）、工具呼叫後（PostToolUse）、壓縮對話前（PreCompact）等等。

![Hooks生命週期事件觸發](https://pic.yupi.icu/1/06_Hooks%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E4%BA%8B%E4%BB%B6%E8%A7%A6%E5%8F%91%E5%9B%BEv2_compressed_v2.png)

最經典的用法就是：每次編輯檔案後自動跑 Prettier 格式化。

這件事如果寫在 CLAUDE.md 裡，AI 大機率會遵循，但也可能會忘掉。

用 Hook 就不存在這個問題，檔案一編輯，Prettier 就自動執行，跟 AI 模型本身無關。

而且 Hook 的上下文成本幾乎為零，因為配置資訊壓根不在主上下文裡。



### 「永遠不要做 X」靠指令是不夠的

這是官方博文裡我覺得最值得記住的一個觀點。

你在 CLAUDE.md 裡寫「永遠不要刪除資料庫遷移檔案」，Claude 大部分時候確實會遵守。但是在長會話、上下文壓縮、或者遇到某個檔案裡的 prompt 注入時，AI 是有可能違反這條指令的。

真正的安全防線需要 **Hook + 許可權** 雙重保障。你可以用 `PreToolUse` Hook 檢查每一次工具呼叫，一旦發現要刪除資料庫遷移檔案，就直接 exit code 2 攔截掉。再配合 Managed Settings 從組織層面強制禁止某些操作，這樣才能真正做到萬無一失。

這個思路跟我之前分析 Claude Code 原始碼時看到的 fail-closed 設計是類似的。Claude Code 內部的工具系統預設把所有工具當作「危險操作」處理，除非工具明確宣告自己是隻讀的。

**安全這件事，不能指望 AI 的自覺性。**

![指令和鉤子-安全防線對比](https://pic.yupi.icu/1/07_%E6%8C%87%E4%BB%A4vs%E9%92%A9%E5%AD%90-%E5%AE%89%E5%85%A8%E9%98%B2%E7%BA%BF%E5%AF%B9%E6%AF%94%E5%9B%BE_compressed_v3.png)



## 6、Output Styles 和 Append System Prompt

最後兩種方式我用的相對較少，所以放在一起講。

Output Styles 是用來定義 Claude 輸出風格和行為模式的。它放在 `.claude/output-styles/` 目錄下，會被注入到系統提示詞中，永遠不會被壓縮丟掉。

但有一點要特別注意，自定義輸出風格會替換掉 Claude Code 的預設系統提示詞。

也就是說，Claude Code 原本內建的那些關鍵行為，比如怎麼確定修改範圍、什麼時候加註釋、遇到安全問題怎麼處理，自定義之後就全沒了。

所以官方的建議是先看看內建的幾種風格夠不夠用，別輕易去自定義。目前內建了 Proactive 主動執行、Explanatory 詳細解釋、Learning 協作學習這 3 種模式，基本覆蓋了大多數使用場景。

![](https://pic.yupi.icu/1/image-20260625182514344.png)

Append System Prompt 是另一種調整 Claude 行為的方式，它允許你在不修改任何檔案的情況下，臨時給 Claude 追加一段指令。

具體用法是透過 CLI 的 `--append-system-prompt` 引數傳入，只對當次呼叫生效。

跟 Output Style 的區別在於，它是追加而非替換，不會影響 Claude Code 的預設行為。適合臨時調整語氣、輸出格式這些輕量需求。

![](https://pic.yupi.icu/1/image-20260625182914705.png)

不過官方也提到了一個限制，追加的指令越多，AI 對每條指令的遵循度就越低，特別是指令之間有衝突的時候。



## 什麼時候該用什麼？

一口氣看完 7 種方式，你可能會有點蒙。

沒關係，官方給了幾條判斷標準，有個印象就行。

![配置方式選擇決策流程](https://pic.yupi.icu/1/08_%E9%85%8D%E7%BD%AE%E6%96%B9%E5%BC%8F%E9%80%89%E6%8B%A9%E5%86%B3%E7%AD%96%E6%B5%81%E7%A8%8B%E5%9B%BE_compressed_v3.png)

第一，CLAUDE.md 放「事實」，Skills 放「流程」。

如果你的 CLAUDE.md 裡有超過 30 行的步驟性內容，比如部署 runbook、安全審查清單，就應該把它移到 `.claude/skills/` 裡面去。

第二，「每次 X 後做 Y」這類需求應該用 Hook，不要寫在指令裡。

比如每次編輯後跑 Prettier、提交前檢查 lint、完成任務後發 Slack 通知，這些都不應該依賴 AI 的記憶力。模型選擇做某件事，和某件事自動發生，這完全是兩回事。

第三，「絕對不能做 X」這種硬性要求需要 Hook + 許可權雙保險。

光靠指令只能做到 AI 大部分時候遵守，真正的安全邊界必須用確定性機制來保證。這跟寫程式碼一個道理，你不會靠註釋來防止某個函式被錯誤呼叫，你會用型別系統和許可權檢查來兜底。



## 我的實踐經驗

再分享幾個我自己配置 Claude Code 的心得。

首先是 CLAUDE.md 要有「索引」思維。不要把它當百科全書，把它當目錄就好。告訴 Claude 專案的基本資訊，然後用指標指向更詳細的檔案。

比如寫上：前端元件規範見 docs/FRONTEND.md、部署流程用 /deploy 技能。

這樣 CLAUDE.md 保持精簡，Claude 需要詳細資訊的時候會自己去讀對應檔案。

![漸進式披露按需載入](https://pic.yupi.icu/1/06_%E6%B8%90%E8%BF%9B%E5%BC%8F%E6%8A%AB%E9%9C%B2%E6%8C%89%E9%9C%80%E5%8A%A0%E8%BD%BD_compressed_v2.png)

然後是 Skills，我覺得這是目前最被低估的功能。我現在把很多重複性的工作流程都封裝成了 Skill，什麼 AI 熱點蒐集、影片動畫製作、圖文創作工作流等等。

Subagent 我主要用來做調研型任務。比如：幫我調研一下這個庫有沒有替代方案、蒐集資訊、分析一下這個 Bug 的原因，這類任務中間過程很長，但最終只需要一個結論，用 Subagent 可以讓主對話保持乾淨。不過很多 AI 工具現在都能自動建立和管理 Subagent 了。



## 寫在最後

Claude Code 的配置體系設計得很講究：事實和流程分離、按需載入降低成本、確定性保障優於機率性指令、隔離執行避免上下文汙染。

這些設計思想不管你是想深度使用 Claude Code，還是想自己搭建 AI Agent 系統，都值得好好學一學。

順便說個能佐證這套設計的事：Anthropic 自己在新模型釋出後，把 Claude Code 的系統提示詞砍掉了 80% 以上，而程式設計跑分一點沒掉。他們砍掉的正是那些本該交給模型自己判斷、或者本該做成按需載入的內容。想了解這套「提示詞減法」的具體做法，可以閱讀本教程經驗技巧板塊中的《Anthropic 官方 - 提示詞精簡方法》。
