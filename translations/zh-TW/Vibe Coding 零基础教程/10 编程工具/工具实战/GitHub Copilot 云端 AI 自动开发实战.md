# GitHub Copilot 雲端 AI 自動開發實戰

本文介紹如何利用 GitHub Copilot Coding Agent 在雲端自動完成從需求分析到全棧開發、測試、部署上線、程式碼審查、Issue 處理、定時任務的全流程。全程不需要開啟 IDE，在 GitHub 網頁版即可完成。

大家好，我是程式設計師魚皮。

前兩天，我受邀參加了微軟 AI Tour 大會，還在會上做了一場演講。

主題是「帶你看 GitHub Copilot 的另一面：智慧體裝機，不只在 IDE」。這名字是大會方包裝的，說實話我自己看著都一頭霧水。。。

![](https://pic.yupi.icu/1/image-20260422215325862.png)

簡單來說就是：**手把手教大家如何用 GitHub + Copilot，打造屬於自己的 AI 智慧體。**

真沒想到有這麼多人來聽分享，看來大家對這個選題確實很感興趣。

![](https://pic.yupi.icu/1/mmexport1776762414702_%E5%89%AF%E6%9C%AC.jpg)

這篇文章就是演講的完整文字版，希望能給大家一些啟發和幫助。

⭐️ 影片版：https://bilibili.com/video/BV1aFoyBnE4D



## 背景和思考

最近「一人公司」和「龍蝦」的概念特別火，很多人都在玩 AI 智慧體，比如 OpenClaw 養蝦、Hermes Agent 養馬什麼的。

現在的 AI 智慧體不只是聊天，能持續幹活、越用越懂你、隨處使用。

但是，你有沒有想過，扒開所有花哨的包裝，**一個 AI 智慧體的本質到底是什麼？**

我覺得是四樣東西：**角色、記憶、技能、工作空間**。

沒有工作空間，角色無處定義、記憶無處儲存、技能無處掛載。

![](https://pic.yupi.icu/1/image-20260423162031832.png)

除了自己的電腦之外，還有其他的工作空間嗎？

作為一名開源作者，我本能地想到 GitHub 這個全球最大的程式碼託管平臺，它的倉庫天然就是 **持久化的檔案空間**；而 GitHub Copilot 又提供了強大的 AI 代理執行能力，還支援網頁版使用。

那乾脆把 GitHub 倉庫當成養 AI 智慧體的「個人電腦」，不就可以了麼？

所以下面我要手把手教大家：**怎麼用 GitHub 打造一隻你自己的 AI 小龍蝦。**

我把它稱為「給蝦」：

![](https://pic.yupi.icu/1/image-20260423162442682.png)

接下來我會一步步演示，如何利用 GitHub 搭建一個超級智慧體，不需要開啟 IDE，也能完成從需求分析到全棧開發、測試、文件生成、部署上線、SEO 最佳化、程式碼審查、自動處理 Issues、定時任務的全流程。



## 1、初始化 Agent

開啟 GitHub 網頁版，你會發現 GitHub Copilot 的對話入口隨處可見，已經融入到 GitHub 的各個角落了。

![](https://pic.yupi.icu/1/1774936826720-d8fb03a7-3f53-4674-8d37-d1abbd873565.png)

我們先新建一個叫 `github-claw` 的倉庫，作為 AI 智慧體的工作空間。

建立倉庫時就可以填入初始化的提示詞，這其實就是我們給這隻 AI 小龍蝦注入靈魂的過程。

![](https://pic.yupi.icu/1/1774936859388-895eba7a-1a5a-45d8-b510-b2c2b5402efa.png)

在開始之前，建議先從右上角進入 GitHub Copilot 的設定，開啟聯網搜尋功能，這樣 AI 能獲取更新的資訊。

![](https://pic.yupi.icu/1/image-20260423162530594.png)

然後我們填入初始化 Agent 的提示詞。這段提示詞定義了龍蝦的角色、行為規則和記憶機制：

```markdown
你是這個倉庫中長期駐留的個人 AI 助手與主要代理，像 OpenClaw 一樣，不只是回答問題，還要持續做事、積累記憶、維護角色，並讓這個倉庫逐漸成為可長期演化的個人 AI 空間。

請先參考 OpenClaw 官方文件，理解它作為 "能做事的個人 AI 助手" 的定位，以及角色、記憶、技能和工作空間的思路：https://docs.openclaw.ai

然後把這個倉庫初始化為適合 GitHub Copilot 網頁版長期使用的個人 AI 工作空間，讓我以後在新的 Copilot 對話裡，也能繼續沿用同一個角色、記憶和工作方式。

請先建立並提交一個簡潔、可長期複用的 AGENTS.md，在裡面定義：
- 你是誰
- 你如何在這個倉庫中工作
- 你如何管理任務與記憶
- 你每次完成任務後要做的收尾動作

要求：
- 把倉庫當作持久化的檔案與記憶空間，可儲存任何有用檔案
- 用檔案作為記憶的真實來源，不把重要資訊只留在當前對話裡
- 將長期記憶與每日/臨時記錄區分開
- 規則簡潔、實用、可擴充套件，不要過度設計

如果確有必要，可以補充最少量的 MEMORY.md、memory/ 或 SOUL.md，但請保持輕量，並以 AGENTS.md 為核心。
```

可以看到，Copilot 自動初始化了一個工作空間，還自動整合了 GitHub 的 MCP 工具：

![](https://pic.yupi.icu/1/1774937227476-47848347-e4ba-4d4f-855f-b5921ea4eb59.png)

任務完成後，它會自動建立一個 PR。我們人工檢查一下，沒問題就合併。

![](https://pic.yupi.icu/1/1774937109998-7080c68f-b049-4fe9-9c4d-860a0ddf2484.png)

對了，如果你發現有「網路連線失敗」的提示，是因為 Copilot coding agent 預設有防火牆限制。需要到倉庫設定裡關閉防火牆：

![](https://pic.yupi.icu/1/1774937329485-d4936387-abd0-464a-b808-a20f8cf6167d.png)

Agent 初始化完成後，你可以跟它打個招呼，它會透過文件獲取到記憶：

![](https://pic.yupi.icu/1/image-20260423162709389.png)



## 2、開發上線網站

Agent 初始化好了，接下來讓它幹活。

讓它幫我的開源 AI 知識庫專案 `ai-guide` 開發一個高顏值的導航官網，提示詞如下：

```markdown
請為我開源的 AI 知識庫專案（ai-guide）開發並部署一個高顏值的導航官網，突出專案介紹、精選內容、路線圖、更新日誌、增長趨勢等，吸引更多人關注我的開源倉庫。必須使用 UI-UX-PRO-MAX 技能全面最佳化前端介面，完成後直接給出可上線訪問的地址。必須自主完成任務
```

在倉庫的 Agents 面板中，可以直接發起新的對話任務。

Copilot 會透過 GitHub MCP 獲取我的開源專案資訊，然後自動開始開發網站：

![](https://pic.yupi.icu/1/1774937381654-bde29eb7-3d0f-4869-a065-f7ddb09950dd.png)

生成程式碼後，它還會自動執行程式碼檢查，發現問題就自主修復：

![](https://pic.yupi.icu/1/1774937517424-6099472c-eb6c-4688-a02d-79b3ed37ca8e.png)

接著它會自動建立 GitHub Actions 工作流，利用 GitHub Pages 完成靜態網站的部署：

![](https://pic.yupi.icu/1/1774937463974-f0f1cf86-da67-40ee-8cf9-abee42b66807.png)

合併 PR 後，還需要進入倉庫設定裡的 GitHub Pages，選擇「從工作流部署」（注意倉庫必須是公開的）：

![](https://pic.yupi.icu/1/1774937811979-b3b187f8-f23c-42b1-be46-363d9f9a2457.png)

然後手動觸發一次工作流，後續每次推送程式碼都會自動觸發部署：

> 注意檢查 workflow 裡的分支名配置，要和你倉庫的預設分支一致（比如 `master` 還是 `main`）。

![](https://pic.yupi.icu/1/1774937756522-a4fd8522-7891-4e7c-9825-67a6473dbb3a.png)

成功部署後，頁面就可以正常訪問了：

![](https://pic.yupi.icu/1/1774937885356-5d43735f-8c35-42de-a89e-b868612e5448.png)



## 3、使用技能

不過你可能注意到了，雖然我在提示詞裡提到了要用 `UI-UX-PRO-MAX` 技能，但 AI 並沒有真正安裝它。

當我命令它用技能時，它反而自己造了一個，這就不對了。

![](https://pic.yupi.icu/1/1774937618640-576f8005-f62f-44f4-9483-e1734d8555cd.png)

所以我們需要新開一個對話，透過提示詞教會 AI 如何正確發現、安裝和使用技能：

```markdown
請最佳化當前倉庫的工作流與 AGENTS.md，讓這個倉庫中的主要 AI 代理具備穩定的技能發現、安裝和使用機制。

明確約定如下：
- 專案級技能統一儲存在 .agents/skills/
- 每個技能使用獨立目錄，例如 .agents/skills/<skill-name>/
- 技能的主入口檔案為 SKILL.md
- 如果技能包含指令碼、模板或資原始檔，也與 SKILL.md 放在同一技能目錄下

請在 AGENTS.md 中加入簡潔、可執行的規則，使代理在後續工作中遵循以下流程：
1. 接到任務後，先檢查本地 .agents/skills/ 中是否已有可複用技能
2. 如果本地沒有合適技能，再自動到 GitHub 開源倉庫和 Skills.sh 搜尋相關技能
3. 優先選擇來源清晰、結構規範、說明完整、風險較低的技能
4. 安裝技能時，將其儲存到 .agents/skills/<skill-name>/
5. 安裝後更新必要說明，使後續對話能夠直接複用這些技能
6. 如果找不到合適技能，再自行完成任務，但優先沉澱成可複用技能
7. 避免重複安裝相同技能，並儘量保持技能目錄整潔、命名清晰、可維護
```

AI 順利完成了任務，制定了技能標準：

![](https://pic.yupi.icu/1/1774937972667-4d367cc1-d71d-43fe-ae68-3431b6d2108a.png)

搞定了技能規範，接下來讓 AI 正確安裝並使用 `UI-UX-PRO-MAX` 技能來最佳化網站：

```markdown
幫我廢棄掉原來錯誤的 UI-UX-PRO-MAX 技能，安裝正確的 UI-UX-PRO-MAX 技能，並利用這個技能最佳化之前的 ai-guide 導航網站
```

![](https://pic.yupi.icu/1/1774938123134-4f172cad-2ba2-402e-82e6-625db01ca36b.png)

這次成功了！AI 智慧體從 GitHub 上正確複製了技能目錄，並用技能最佳化了網站的 UI：

![](https://pic.yupi.icu/1/1774938261001-a8f8d0ea-313a-4782-bb5c-bd049d535b6d.png)

頁面移除了多餘的 Emoji，看起來更專業了：

![](https://pic.yupi.icu/1/1774938307530-07362fac-fdd8-4e2f-9c72-0a1319022029.png)

更重要的是，它還更新了 `AGENTS.md` 工作流、記憶和任務檔案，實現了 AI 智慧體的進化，之後它就能自己發現和使用技能了：

![](https://pic.yupi.icu/1/1774938201747-77528d03-8fbc-4ef0-9221-160f06ae49b2.png)



## 4、文件生成

文件是開源專案的牌面，我們讓 AI 幫忙生成一份圖文並茂的專案介紹文件 README.md。

這裡有個小技巧，先人工挑選一個靠譜的 AI 生圖技能，然後到 [魚皮 AI 導航](https://ai.codefather.cn/) 上找一個你喜歡的繪圖風格提示詞模板，一起提供給 AI 參考。

![](https://pic.yupi.icu/1/1774938362506-65f5400c-e58c-49e0-a717-5f1df6306c65.png)

給 AI 的提示詞：

```markdown
請先閱讀當前倉庫中的 ai-guide 導航網站，併為它生成一份高質量的 README.md 專案介紹文件，同時配套生成幾張幫助理解和宣傳網站的動漫風格圖片，儲存並在 README 中引用。

請先安裝並使用這個 AI 生圖技能：npx skills add https://github.com/inferen-sh/skills --skill ai-image-generation。我可以提供 Gemini NanoBanana 的 API Key，請安全使用，不要寫入倉庫。

AI 生圖的風格參考下面的提示詞模板：@已經複製的模板
```

AI 完成任務後會請求一個生圖 API Key，我們到 Google AI Studio 上獲取後發給 AI。它會注重安全性，僅臨時使用這個金鑰：

![](https://pic.yupi.icu/1/1774938470660-ee788099-bace-4a0b-8f2b-326de0caf773.png)

AI 智慧體成功呼叫技能，生成了圖文並茂的文件：

![](https://pic.yupi.icu/1/1774938669310-fbbb62dd-a10d-4ef7-8ade-4ae3630f33e8.png)

不過這次它誤改了網站首頁的檔案。沒關係，透過 PR 我們發現了這個問題，不合並就行，再讓 AI 自主修復。

這裡也提醒大家：**雖然 AI 寫程式碼能力很強了，但程式碼審查依然很重要。**

![](https://pic.yupi.icu/1/1774938796668-8b82900c-1f40-44f7-89d3-e4f03af3cea7.png)



## 5、SEO 最佳化

開源專案上線後，想把它推廣出去，需要做好 SEO 搜尋引擎最佳化，讓使用者能在搜尋引擎上搜尋到你的網站。

我們用一個專業的 SEO 技能來最佳化網站：

```markdown
請先閱讀當前倉庫中的 ai-guide 導航網站，並對它進行一輪高質量的 SEO 最佳化，直接完善站點的標題、描述、結構化資訊、頁面語義、連結結構和可索引性。

做法上，請先安裝並使用這個 SEO 技能：npx skills add https://github.com/coreyhaines31/marketingskills --skill seo-audit，然後把最佳化結果直接落實到專案程式碼中。
```

GitHub Copilot 整合了 Claude 等多個模型，可以直接在雲端啟動不同的 AI 來完成任務：

![](https://pic.yupi.icu/1/1774938911290-462333f6-8107-485d-ae36-f1417eff0cc0.png)

直接在網頁端爽用 Claude 模型：

![](https://pic.yupi.icu/1/1774938853796-04e68bed-2f7d-42cb-9206-0c237f26f288.png)

很快 AI 就完成了 SEO 最佳化，網站更容易被搜尋引擎收錄了：

![](https://pic.yupi.icu/1/1774939165853-dc11c5a9-ee7a-4462-8d24-3fd3b4947ebe.png)

效果如圖，網頁上增加了一堆搜尋關鍵詞：

![](https://pic.yupi.icu/1/1774939208320-445dfdcb-c527-49bf-acf7-e24571e42584.png)

可以看出，我們的 AI 智慧體已經能夠熟練運用各種技能了。之後你再新開一個對話，就可以直接使用已經安裝好的技能，把 GitHub 當成安全隔離的「電腦空間」來用。



## 6、開發前後端全棧專案

既然 GitHub 提供了完整的工作空間，那也可以用來開發包含後端的全棧專案。

比如輸入下面的提示詞，讓 AI 幫我開發個《多媒體處理平臺》：

```markdown
在當前倉庫內新開發一個完整可執行的《多媒體處理平臺》前後端專案：
- 前端使用 Vue 實現多頁面，支援圖片、音訊和影片的壓縮與格式轉換
- 後端使用 Python + SQLite + FFmpeg 等

請自主完成專案的前後端開發、聯調、依賴配置、示例資料、必要文件和本地執行方式，並主動進行測試驗證，確保圖片、音訊和影片的壓縮與格式轉換流程都能實際可用。

除非確實必要，否則不要中途停下來向我確認，直接持續推進到可執行狀態。
```

AI 會自己完成環境安裝、前後端開發、自動化測試、文件生成，全流程一條龍：

![](https://pic.yupi.icu/1/1774939363314-a5d0a2ae-6cc8-43f2-b7d2-85e8a491cfe4.png)

注意，這些全部都是在雲端執行的。哪怕你把網頁、網路甚至電腦都關了，也不影響它繼續工作。

![](https://pic.yupi.icu/1/1774939462978-9bc438e5-22d2-4d30-9d5b-3d8dd24bfa22.png)



## 7、測試驗證

涉及後端的專案還是得好好測試一下。有 2 種方式可以訪問和測試。



### 本地接管測試

開發完成後，你可以在 AI 工作的對話方塊中點選「Open in VS Code」，或者用 Copilot CLI 在本地接管專案：

![](https://pic.yupi.icu/1/image-20260423163857167.png)

VS Code 接管專案後，會自動克隆倉庫到本地並開啟。

然後你可以讓 AI 幫你執行專案：

```markdown
幫我執行這個專案的前後端
```

它會自動建立 Python 虛擬環境，關鍵步驟會找你確認（比如安裝依賴和執行命令），非常安全：

![](https://pic.yupi.icu/1/1774939577513-adc4908e-bd05-43a4-834d-efad1f629026.png)

然後人工開啟瀏覽器測試，有問題再讓 AI 修復就好：

![](https://pic.yupi.icu/1/1774939621027-32a61479-57ec-4022-b090-a5fba6d92a5b.png)



### 線上執行測試

如果不想開本地 IDE，還可以用 GitHub Codespaces。

Codespaces 是 GitHub 提供的雲端開發環境，可以在瀏覽器裡直接編輯程式碼、執行專案，體驗和本地 VS Code 幾乎一樣。

![](https://pic.yupi.icu/1/image-20260423163948284.png)

需要先讓 AI 幫忙建立 Codespaces 所需的配置，這樣建立環境後就會自動完成初始化並執行專案：

```markdown
請繼續為這個專案補全 GitHub Codespaces 開發環境配置，建立 .devcontainer/ 相關檔案，使其適配這個前後端專案，並確保在建立 Codespace 後能夠自動安裝前後端依賴、安裝 FFmpeg、初始化必要環境、自動啟動 Vue 前端與 Python 後端，並正確轉發訪問埠。
```

![](https://pic.yupi.icu/1/1774939729545-f819f0c7-1e67-45bf-bb74-2716aa60f694.png)

AI 建立了所需的配置檔案：

![](https://pic.yupi.icu/1/1774939782308-e572175e-b55e-4934-8273-00e617db2cef.png)

然後在 GitHub 上建立 Codespace：

![](https://pic.yupi.icu/1/image-20260423164046377.png)

建立完成後，正常情況下可以直接訪問前端和後端（注意前端請求後端的地址可能需要調整）：

![](https://pic.yupi.icu/1/1774939972660-85faf67a-ec86-4bb4-be10-a533fe2432de.png)

如果訪問不了，也可以進入 Codespace 的終端手動執行啟動指令碼（注意指令碼的執行路徑要正確）：

![](https://pic.yupi.icu/1/1774939912870-37b0f3dc-354b-4aef-ac68-58bc21e85513.png)

你看，這個操作介面是不是和本地的 VS Code 一樣？而且還能直接在網頁版裡使用 Copilot。



## 8、程式碼審查

程式碼審查是保障程式碼質量的關鍵環節。GitHub Copilot 提供了自動和手動兩種審查方式。



### 自動程式碼審查

Copilot coding agent 開發的程式碼，本身就會自動執行一輪程式碼審查：

![](https://pic.yupi.icu/1/1774921510223-3b174e66-582c-4a50-a663-a686d4d0cefb.png)

同時還會自動執行安全檢測：

![](https://pic.yupi.icu/1/1774921537750-a468dece-3396-4d8c-8753-06b0fbb61054.png)

此外，你還可以在倉庫設定中開啟對所有 PR 的自動審查。

![](https://pic.yupi.icu/1/1774925532564-80308560-a96c-41b8-9a02-80a21fcda515.png)

把 Copilot 當成你的「同事」就好，只要把它加為 Reviewer，就會自動觸發審查：

![](https://pic.yupi.icu/1/1774925617582-16064bd0-af9e-4684-ae16-0acc54570b3d.png)

審查結果還支援快捷修復，你可以根據它的建議直接採納修改，一鍵提交。也可以透過自定義指令來調整審查的側重點：

![](https://pic.yupi.icu/1/1774940063359-5b4cc05e-d016-4c0c-83df-ab3b95ca35cf.png)



### 手動程式碼審查

把 GitHub Copilot 當成你的同事，只要在 PR 中把它設定為 Reviewers，就會觸發程式碼審查：

![](https://pic.yupi.icu/1/1774940168717-5cae3ea3-3868-4bf1-900c-e98bdfeb1373.png)

你也可以在 PR 的評論裡直接 `@copilot`，比如讓它把埠號恢復成原樣。

這種方式更適合讓 Copilot 根據審查意見直接改程式碼、修復 Bug：

![](https://pic.yupi.icu/1/1774940212269-3c0f640b-b461-4992-8a8b-4355a5ae0b51.png)



## 9、處理 Issues

維護開源專案的過程中，肯定少不了處理使用者提的 Issues（問題），這也是很花時間的事情，可以讓 AI 智慧體自動完成。



### 手動處理 Issues

GitHub Copilot 官方支援讓 Copilot coding agent 接手 Issue、自動建立 PR 並修復。

操作很簡單，進入一個 Issue，把它分配給 Copilot 就行：

![](https://pic.yupi.icu/1/1774940337943-ba0b6ed8-872f-4745-b934-64d4f0fbb14b.png)

Copilot 會自動建立一個 PR：

![](https://pic.yupi.icu/1/1774940372286-4be19b2d-2d7d-4860-afef-4f3314321c48.png)

同時建立一個工作會話來分析和修復這個 Issue：

![](https://pic.yupi.icu/1/1774940395478-6e05f7f7-f5ea-4c9b-bbf3-912bfe585612.png)



### 自動回覆 Issues + 自動修復 Bug

還可以讓 AI 全自動幫我們回覆 Issues 並修復 Bug。

利用 GitHub Actions 的自動化能力，我們只需要補一個「自動派單」的工作流就行。

給 AI 一段提示詞：

```markdown
為當前倉庫建立一套 Issue 自動化處理工作流：當有新的 Issue 建立時，先自動回覆一條簡潔的確認與補充資訊提示；如果該 Issue 被識別為 bug（比如帶有 bug 標籤或滿足明確的 bug 條件），則自動將該 Issue 分配給 GitHub Copilot coding agent 處理，並讓 Copilot 後續自動開 PR 修復。

請直接完成所需的 GitHub Actions 工作流、必要配置和說明，優先採用簡潔、穩定的實現方式。
```

![](https://pic.yupi.icu/1/1774940470510-d1d080c2-1b43-40f8-a4c8-da6b99baceba.png)

不過需要注意的是，自動生成的指令碼可能會有問題，比如只回復了卻沒有真正分配給 Copilot 去修復：

![](https://pic.yupi.icu/1/1774940518174-d623cbc5-ae7a-4258-babc-34fb7d42d6db.png)

這時候可以再讓 AI 根據官方文件修復。核心要注意幾點：

```markdown
請修復當前倉庫中 Issue 自動化工作流的 Copilot 分配邏輯。現在工作流雖然會自動評論"已分配給 Copilot"，但實際上並沒有真正成功分配。

請參考 GitHub 官方對 Copilot coding agent 的 Issue API 分配方式，改成正確可用的實現：使用正確的 Copilot assignee copilot-swe-agent[bot]、必要的 agent_assignment 引數，並且只有在真實確認分配成功後才發表評論；如果分配失敗，也要給出明確、真實的失敗提示，不要誤報成功。

另外，請順手最佳化這個工作流的結構：opened 事件只負責自動回覆，labeled + bug 事件只負責分配給 Copilot，保證整體邏輯更清晰穩定。
```

![](https://pic.yupi.icu/1/1774940559765-faff3598-81bb-4a7d-a4fd-e9a0024644a8.png)

而且這裡需要使用者級別的 Personal Access Token（PAT），不能用預設的 GITHUB_TOKEN。

先到 GitHub 申請 PAT，開通相應的倉庫許可權：

![](https://pic.yupi.icu/1/1774940613065-a66b1fc9-09cf-47ad-ad5e-57dd4618490c.png)

然後把金鑰存放到倉庫的 Secrets 中，在工作流指令碼中透過 `secrets.COPILOT_ASSIGN_TOKEN` 引用：

![](https://pic.yupi.icu/1/1774940688587-7e6f019d-9df1-4af5-b808-233ee3ec15ee.png)

引用 token 的示例程式碼如下：

```yaml
  - name: Assign issue to Copilot coding agent
    uses: actions/github-script@v7
    with:
      github-token: ${{ secrets.COPILOT_ASSIGN_TOKEN }}
      script: |
```

然後我只要提一個打了 `bug`  標籤的 Issue，就會觸發 GitHub Actions，自動把 Bug 分配給 AI 處理：

![](https://pic.yupi.icu/1/1774940722288-25f2ee1e-d20d-46c5-869a-bee8fcb69d00.png)



## 10、定時任務

OpenClaw 的一大亮點是可以執行定時任務，那咱們的 “給蝦” 也要有！

但是 GitHub 倉庫不是一臺常駐執行的電腦，怎麼做定時任務呢？

我有個主意，利用 GitHub Actions 的 `schedule` 觸發器，就能給 AI 智慧體補上「定時觸發」的能力。

比如讓它每天自動推送最新的 AI 科技熱點：

```markdown
為當前倉庫建立一個可長期使用的定時任務工作流，利用 GitHub Actions 模擬 OpenClaw 風格的定時觸發能力。

目標：每天北京時間中午 13 點，自動收集並總結本週最新的 AI 科技熱點，並以 "推送日報" 的形式傳送給我。

優先採用簡單穩定的實現方式：預設先推送到 GitHub Issue；如果倉庫中已有郵箱等其他 webhook 配置，也可以優先複用。
```

當然，你還可以選擇對接更多第三方渠道，比如郵件、Telegram 等：

![](https://pic.yupi.icu/1/1774940782165-e1ce8ae7-2ab1-4982-a48c-1e9c5791db3b.png)

任務完成，建立了定時觸發的 GitHub 工作流：

![](https://pic.yupi.icu/1/1774940824191-a0b449e3-d16f-4784-9894-2b2835361853.png)

之後，每天會自動生成一份 AI 科技日報：

![](https://pic.yupi.icu/1/1774940877163-c8368494-3a99-45d4-a98b-7cfb7ed6e12a.png)

注意，GitHub Actions 的 schedule 定時觸發會有延遲，官方文件也說明了在高負載時段（尤其是每小時開頭）可能延遲甚至丟棄任務，所以不適合對執行時間要求精準的場景。



## 11、封裝 AI 智慧體

到這裡，我們的 AI 小龍蝦已經養得很肥了。它有了角色、記憶、技能、自動化流水線。不妨把它封裝起來，分享給別人用。

於是，我給 Copilot 這段提示詞，讓它幫我封裝成一個 Agent Skill：

```markdown
請把當前倉庫裡已經實現的所有 "把 GitHub Copilot 變成小龍蝦" 的能力，系統化封裝成一個可複用的 agent skill，名稱為 github-claw，並放到倉庫的 skills/github-claw/ 目錄下。

在開始之前，請先參考 anthropics/skills 倉庫中的 skill-creator 結構與規範，按規範建立完整技能檔案，而不是隻寫一個簡單的 SKILL.md：
https://github.com/anthropics/skills/tree/main/skills/skill-creator

這個 github-claw skill 的目標是：讓其他使用者只要安裝這個技能，就能儘可能快速地把 GitHub Copilot 倉庫工作流變成一個 OpenClaw 風格的小龍蝦系統，具備並串聯以下能力：
- 角色與人格
- 檔案化記憶與長期上下文
- 技能發現、安裝與管理
- 定時任務 / GitHub Actions 自動化
- Issue 自動回覆與自動分配給 Copilot
- PR 審查與自動化工作流
- 編碼開發、部署、網站生成與專案推進
```

![](https://pic.yupi.icu/1/1774941001296-f6cfe046-91a8-477f-814e-944c4ce5ca10.png)

封裝好的 `github-claw` 技能被單獨放到了一個乾淨的分支：

![](https://pic.yupi.icu/1/1774941046143-f9f04ebf-6c68-41f1-b037-6f9b6f50cae2.png)

這樣一來，以後任何人只要新建一個 GitHub 倉庫，安裝上這個技能，就能立刻擁有一隻自己的 AI 小龍蝦了。

> GitHub Claw 專案開源：https://github.com/liyupi/github-claw

![](https://pic.yupi.icu/1/1774941138078-6a086446-9193-4b43-9847-9232401f9854.png)



## 總結

至此，我們全程沒有開啟 IDE，利用 GitHub 網頁版就打造了自己的 AI 智慧體。

你可以讓它幫你完成從需求分析到全棧開發、測試、文件、部署上線、SEO 最佳化、程式碼審查、Issue 自動處理、定時任務的全流程。

而且因為 GitHub Copilot 深度融合在網頁端，以上所有任務都可以透過手機開啟 GitHub 網頁或 GitHub Mobile App 完成，隨時隨地使用。

![](https://pic.yupi.icu/1/image-20260423165139146.png)

Copilot 的優勢在於：

1）全程雲端執行：Copilot coding agent 在 GitHub Actions 支援的臨時環境中獨立工作，非常安全。你可以關掉網頁甚至關機，AI 會繼續幹活。

2）端到端交付能力：GitHub Copilot 能夠貫穿整個開發生命週期，從寫程式碼到 PR 審查到部署，全部在 GitHub 生態內閉環完成。

3）多模型靈活選擇：GitHub 提供了多個模型供選擇，可以根據不同任務型別適配最合適的模型，節省成本。

![](https://pic.yupi.icu/1/image-20260423165247440.png)



## GitHub Copilot 更多能力

除了今天演示的核心流程，GitHub Copilot 還有很多值得探索的能力：

1）Coding Agent MCP 配置：在倉庫設定中可以配置 Copilot 的許可權、工具和 MCP Server（比如接入 Context7、Firecrawl 等 MCP），擴充套件 Copilot 的外部資料獲取和操作能力。

2）GitHub 內建 Memory：Copilot 可以自動儲存它在倉庫工作中推斷出的有用資訊，形成持久化的倉庫級記憶。後續它在這個倉庫裡工作時會自動呼叫這些記憶，效果越用越好。目前處於 Public Preview 階段。

3）Copilot Spaces：一種上下文共享空間，你可以把程式碼、文件、設計稿等多種資源聚合到一個 Space 裡，讓 Copilot 在回答和工作時始終基於正確的上下文，適合團隊協作場景。

4）GitHub Spark：透過自然語言描述你的想法，Spark 可以秒出全棧 Web 應用原型，支援實時預覽和一鍵部署到 Azure，不需要寫程式碼。還可以從 Spark 建立 GitHub 倉庫，雙向同步。

5）GitHub Copilot CLI：這是一個獨立的命令列 AI 工具，可以閱讀程式碼、編輯檔案、執行命令、建立 PR，還能把任務委派給專門的 Agent。支援遠端會話恢復，在任何終端上都能接著幹。

除了前面主要展示的 Copilot 網頁端，桌面端的 GitHub Copilot（VS Code 等 IDE 外掛版本）也非常好用，能靈活切換多個大模型，還整合了網路搜尋等各種主流工具，支援 MCP 和 Skills，平時我也經常用它帶大家開發完整專案。

比如我的 AI 熱點監控工具專案，就是完全利用 GitHub Copilot 在 IDE 中開發出來的。

![](https://pic.yupi.icu/1/image-20260423165402802.png)

如果你想系統學習 GitHub Copilot 的使用方法，可以閱讀本教程程式設計工具板塊中的《AI IDE 外掛》和同板塊「工具實戰」中的《VSCode + GitHub Copilot：微軟全家桶的 AI 程式設計實戰》。



## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)

