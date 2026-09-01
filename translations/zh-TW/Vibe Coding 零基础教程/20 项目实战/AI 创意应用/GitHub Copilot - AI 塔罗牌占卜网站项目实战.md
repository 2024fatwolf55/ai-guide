# GitHub Copilot - AI 塔羅牌占卜專案實戰

這是一個利用 VSCode + GitHub Copilot 的 Plan 模式 + Agent 模式，從 0 到 1 開發的 AI 塔羅牌占卜網站。透過這個專案，你可以快速體驗 GitHub Copilot 的核心 AI 程式設計能力，幾分鐘就能做出一個有翻牌動畫、AI 占卜解讀、神秘華麗介面的小專案。

預計 30 分鐘學完，適合零基礎入門 VSCode + GitHub Copilot 的 AI 程式設計。

如果你想了解 GitHub Copilot 的更多核心特性（MCP、Agent Skills、自定義智慧體等），可以閱讀本教程程式設計工具板塊「工具實戰」中的《VSCode + GitHub Copilot：微軟全家桶的 AI 程式設計實戰》。



## 專案介紹

使用者輸入一個問題（比如 “我最近的愛情運勢如何”），點選「開始占卜」後，展示 3 張塔羅牌的翻牌動畫，翻牌完成後呼叫 DeepSeek 大模型 API，根據抽到的牌生成 AI 占卜解讀。

介面採用深紫色主題配金色紋理，星空背景，搭配流暢的翻牌動畫效果，響應式佈局手機也能用。

技術棧很簡單：HTML + CSS + JavaScript，呼叫 DeepSeek API 生成占卜解讀。

![](https://pic.yupi.icu/1/image-20260305151413007.png)



## 安裝 VSCode + GitHub Copilot

在開始做專案之前，需要先安裝好開發工具。

1）進入 [VSCode 官網](https://code.visualstudio.com/) 下載安裝包，直接傻瓜式安裝。

![](https://pic.yupi.icu/1/image-20260305141229310.png)

2）開啟 VSCode，點選左側「擴充套件市場」圖示，搜尋 "GitHub Copilot"，安裝官方的 AI 程式設計外掛。

![](https://pic.yupi.icu/1/image-20260305141416199.png)

你還可以根據需要，選擇安裝 Chinese 漢化外掛：

![](https://pic.yupi.icu/1/image-20260305153013870.png)

3）安裝完後，點選 VSCode 底部狀態列的 Copilot 圖示，按照提示登入 GitHub 賬號就行了。

![](https://pic.yupi.icu/1/setup-copilot-status-bar.png)

如果你還沒有 Copilot 訂閱，會自動進入 **Copilot Free 免費計劃**，每月有一定的 AI 對話和程式碼補全額度，零門檻上手。想體驗完整功能的話，Copilot Pro 支援新使用者免費試用 30 天。如果你是在校學生，還可以透過 [GitHub Education](https://education.github.com/pack) 申請學生認證，認證透過後 Copilot Pro 直接免費用。

安裝配置搞定後，就可以開始做專案了。



## 開發流程

這個專案完美展示了 GitHub Copilot 的 Plan + Agent 工作流。

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

你只要像聊天一樣把自己的想法告訴 AI 就好，比如希望呼叫 DeepSeek 大模型的 API：

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

幾分鐘後，Agent 不僅完成了開發任務，還用 Python 啟動了個 Web 伺服器，幫忙執行了網站。

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

Agent 會自動定位到對應的程式碼並精準修改，改完重新整理預覽就好。

![](https://pic.yupi.icu/1/image-20260305152037670.png)

整個過程，從寫需求到出成品，也就幾分鐘。擱以前，我要是自己從零寫這麼個帶動畫的占卜網站，怎麼著也得搞一下午。

你還可以繼續跟 AI 對話來增加功能，整個過程中一定要注意 **上下文的用量**，如果滿了 AI 可能會斷片兒失憶，開始亂改。

![](https://pic.yupi.icu/1/image-20260305152200805.png)

因此，在上下文快滿的時候，最好讓 AI 把當前專案的資訊沉澱為文件。這樣之後每次開啟新的 AI 對話方塊時，只要把歷史文件交給 AI，就能快速找回記憶。 



## 專案收穫

透過這個小專案，你可以學到：

- 如何使用 GitHub Copilot 的 Plan 模式進行需求分析和方案設計
- 如何使用 Agent 模式讓 AI 自主完成程式碼開發
- 如何呼叫 DeepSeek 大模型 API
- 如何用 CSS 實現翻牌動畫和星空背景效果
- 如何在 AI 程式設計中進行人工插手和精細調整
- 如何管理上下文用量，避免 AI 斷片兒

這個專案雖然小巧，但完整展示了 Vibe Coding 的核心工作流 —— 用自然語言描述需求，AI 幫你設計方案和編寫程式碼，人工稽核和調整細節。掌握了這個流程，你就可以用同樣的方式去做更復雜的專案了。
