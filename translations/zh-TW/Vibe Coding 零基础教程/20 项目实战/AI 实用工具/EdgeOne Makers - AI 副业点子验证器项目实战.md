# EdgeOne Makers - AI 副業點子驗證器專案實戰

> 用 AI 程式設計 + EdgeOne Makers，20 分鐘開發上線一個 AI Agent 應用

大家好，我是程式設計師魚皮。

AI 時代，越來越多人開始琢磨用 AI 搞副業賺錢，各種想法滿天飛。

但問題是，大多數想法都停留在「感覺能賺錢」的階段，真正去做之後才發現，要麼競品已經一堆了，要麼根本沒人願意付費，時間精力全浪費了。

所以我就想，能不能做一個 **AI 投資人 Agent**，專門幫我驗證副業想法靠不靠譜？

跟它描述你的副業想法，它會聯網搜競品、分析市場、評估可行性，然後像真正的投資人一樣給出判斷：願意投多少錢？還是白送都不要？

如果你覺得自己的想法被低估了，可以繼續追問、調整方案，它會記住你之前說的內容，動態更新估值。

這樣就能快速過濾掉那些不靠譜的想法，把時間省下來花在真正值得做的事上。

⭐️ 本期對應影片版：[https://bilibili.com/video/BV1jU756mE1x/](https://bilibili.com/video/BV1jU756mE1x/)



## 方案設計
想做這樣一個 AI 應用，你要考慮很多事情：

- 怎麼對接 AI 模型？
- 怎麼使用聯網搜尋能力？
- 怎麼隔離多個使用者的對話記錄？
- 怎麼讓 Agent 記住上下文，應對使用者的追問？

哪怕讓 AI 幫你搞定這些，也會花很多時間和 tokens。

最近騰訊雲的 [EdgeOne Makers](https://pages.edgeone.ai/zh/document/product-introduction) 剛上線了 Agent 託管能力，正好解決了這些問題。

![](https://pic.yupi.icu/1/image-20260629150206869.png)

你只需要專注寫 Agent 的業務邏輯（比如怎麼評估一個副業想法），剩下那些聯網搜尋、對話記憶、模型對接之類的活兒，部署上去之後平臺自動幫你搞定。

![](https://pic.yupi.icu/1/01_%E4%B8%93%E6%B3%A8%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91%E5%B9%B3%E5%8F%B0%E6%90%9E%E5%AE%9A%E5%85%B6%E4%BD%99_compressed_v3.png)

接下來我會從 0 帶大家用 AI 程式設計 + EdgeOne Makers，把這個 AI 投資人 Agent 開發上線。

不過在動手之前，我先帶大家用 EdgeOne Makers 控制檯快速部署一個官方模板，感受一下這個平臺到底是怎麼玩的。



## 快速體驗 EdgeOne Makers

進入 EdgeOne Makers 的 Agent 面板，可以看到預設提供了很多 Agent 應用模板，支援 OpenAI SDK、Claude SDK、LangGraph、CrewAI 等主流框架，JS 和 Python 都能用。

![](https://pic.yupi.icu/1/image-20260629150435803.png)

我這裡選擇建立一個 OpenAI Agent 模板：

![](https://pic.yupi.icu/1/image-20260629150459022.png)

關聯 GitHub 倉庫後，什麼資訊都不用改，直接點選建立部署。

![](https://pic.yupi.icu/1/image-20260629150531427.png)

系統會幫你快速建立一個專案倉庫，然後自動完成整個專案的初始化、安裝依賴和構建部署。

![](https://pic.yupi.icu/1/image-20260629150614707.png)

點選預覽，可以看到平臺提供了一個臨時測試域名：

![](https://pic.yupi.icu/1/image-20260629150844802.png)

直接訪問，一個 AI Agent 專案就上線可用了。能夠正常和 AI 對話，響應速度也不錯。

![](https://pic.yupi.icu/1/image-20260629151024765.png)

你可能會好奇：我沒填大模型的 API Key，怎麼就能用了？

進入 Makers 控制檯的 [Models 模型面板](https://console.cloud.tencent.com/edgeone/makers?tab=models&subTab=models)，你會發現 EdgeOne Makers 預設幫我們對接了主流大模型，限時贈送每個使用者 50 萬 Token / 月。

![](https://pic.yupi.icu/1/image-20260629151052733.png)

還自動建立了一個呼叫大模型的預設金鑰，並且在建立專案時，把這個金鑰注入到了程式的環境變數中，所以你不用填 Key 就能直接用。

![](https://pic.yupi.icu/1/image-20260629151301325.png)

看到這裡，相信你對 EdgeOne Makers 有了基本認識，你可以把它理解為一個專門給 AI Agent 準備的託管平臺，模型、工具、記憶、監控這些能力它都幫你備好了，你只管寫業務邏輯。

![](https://pic.yupi.icu/1/02_EdgeOne_Makers%E6%98%AFAI_Agent%E6%89%98%E7%AE%A1%E5%B9%B3%E5%8F%B0_compressed_v3.png)

下面進入正題，我會帶大家走一遍完整流程：環境準備 → 設計提示詞 → AI 開發 → 部署上線 → 迭代最佳化。

![](https://pic.yupi.icu/1/03_%E5%AE%8C%E6%95%B4%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B%E4%BA%94%E6%AD%A5%E8%B5%B0_compressed_v2.png)



## 環境準備

開發之前，要先安裝 EdgeOne 官方提供的 Skills 技能包，裝上之後 AI 就自動知道怎麼按照 EdgeOne Makers 的要求來寫程式碼（比如專案檔案往哪放、入口函式怎麼寫、平臺提供的聯網搜尋和對話記憶怎麼呼叫），不需要你手動喂文件。

![](https://pic.yupi.icu/1/04_Skills%E6%8A%80%E8%83%BD%E5%8C%85%E8%AE%A9AI%E8%87%AA%E5%8A%A8%E6%87%82%E8%A7%84%E8%8C%83_compressed_v1.png)

參考 [官方文件](https://cloud.tencent.com/document/product/1552/129329)，開啟終端，輸入一行命令：

```bash
npx skills add TencentEdgeOne/edgeone-makers-tools
```

根據指引，選擇要安裝的 Skill，比如我們要用到的智慧體開發 `/makers-agents` 和部署 `/makers-deploy` 技能。

![](https://pic.yupi.icu/1/image-20260629151510758.png)

安裝範圍選擇全域性安裝，這樣之後所有專案都能用。

準備就緒，下面開始寫提示詞。



## 設計提示詞
我的需求並不複雜，而且用什麼框架、部署到哪裡我已經想清楚了，就沒讓 AI 幫我整理，直接編寫完整的提示詞。

完整的提示詞如下：

```markdown
幫我開發「AI 投資人」副業驗證 Agent，部署在 EdgeOne Makers 平臺上。

明確的技術方案：
1. 使用 OpenAI Agents SDK 框架
2. 前端和 Agent 共存在同一個專案裡，之後我會一次部署到 EdgeOne Makers
 
開發要求：
1. 體現 Loop Engineering 的思想，自主開發、自主測試驗證，最終交付一個完全可用的產品
2. 如果有不明確的地方，先問我再動手

需求描述：
Agent 的設定是見過太多專案的資深投資人，說話毒舌、判斷犀利。使用者描述自己的副業想法後，它會聯網搜尋競品和市場資訊，給出願意投資多少錢的判斷（或者「白送都不要」），並說明理由和改進建議。支援多輪對話，使用者可以根據反饋調整方案繼續追問，Agent 要記住之前聊過的內容。前端採用 Q 版風格，多端適配。
```

簡單解釋一下，開發要求裡的 Loop Engineering 思想是讓 AI 自己寫完程式碼後自主測試驗證，不用人工盯著。

不過注意，部署到 EdgeOne Makers 上的程式碼得遵循平臺的規範，不然跑不起來。

所以執行的時候，我要先透過斜槓命令呼叫 `/makers-agents` 技能，AI 就會自動按照平臺要求的入口函式寫法、聯網搜尋和對話記憶的接入方式來寫程式碼。

![](https://pic.yupi.icu/1/image-20260629151608806.png)



## AI 自主開發
確保使用了 `/makers-agents` 技能後，傳送提示詞，AI 就開始自主開發了。

它先載入了 Skill 中關於 Agent 開發的規範（感興趣可以看 [官方文件](https://pages.edgeone.ai/zh/document/agents) 瞭解詳情），然後建立專案、編寫 Agent 邏輯和前端頁面。

![](https://pic.yupi.icu/1/image-20260629152402163.png)

幾分鐘後，AI 完成了核心功能的開發，並且對程式碼進行了編譯驗證和自檢。

![](https://pic.yupi.icu/1/image-20260629152440563.png)

不過由於本地沒有配置 AI 大模型的 API Key，沒辦法完整測試對話流程。

沒關係，接下來部署到 EdgeOne Makers 上，配好金鑰就能跑了。



## 部署上線
前面體驗 **透過控制檯** 建立模板專案時，EdgeOne Makers 自動幫我們注入了 `AI_GATEWAY_API_KEY` 和 `AI_GATEWAY_BASE_URL` 這兩個環境變數。

但如果是自己本地建立專案，需要 **手動** 到 Makers 控制檯獲取這兩個環境變數的值。

![](https://pic.yupi.icu/1/image-20260629152524645.png)

此外，由於我的 AI 投資 Agent 需要聯網搜尋競品資訊，還要開通騰訊雲的 [Web Search API 服務](https://console.cloud.tencent.com/wsapi/index)：

![](https://pic.yupi.icu/1/image-20260629152619126.png)

先選個最便宜的套餐就行，然後獲取到聯網搜尋 API 金鑰。

![](https://pic.yupi.icu/1/image-20260629152752119.png)

拿到這些金鑰後，直接把資訊提供給 AI，使用 `/makers-deploy` 技能讓它幫我部署：

```markdown
幫我部署上線：
AI_GATEWAY_BASE_URL 是 https://ai-gateway.edgeone.link/v1
AI_GATEWAY_API_KEY 是 sk-xxxxx
聯網搜尋 API Key 是 sk-xxxxx
```

![](https://pic.yupi.icu/1/image-20260629152818209.png)

AI 自動設定好環境變數並進行部署。首次部署時會提醒你登入授權，跟著 AI 的提示操作就好。

![](https://pic.yupi.icu/1/image-20260629152852444.png)

很快部署完成，直接拿到了可以訪問的線上地址，太方便了！

![](https://pic.yupi.icu/1/image-20260629152913807.png)

開啟試試，給它發個 IDEA：做一個 AI 幫你寫朋友圈文案的小程式。

Agent 進行了聯網搜尋，找到了好幾個競品，然後給出了評估結果 —— 白送都不要！

![](https://pic.yupi.icu/1/image-20260629153002380.png)

不愧是毒蛇金主，絲毫不留情面，我喜歡。

雖然功能跑通了，但預設模型的輸出效果一般，下面咱們來換個更強的。



## 切換模型
進入 Makers 的模型面板，新增一個新模型，比如國產之光 DeepSeek，點選新增。

![](https://pic.yupi.icu/1/image-20260629153351219.png)

需要到 [DeepSeek 的 API 開放平臺](https://platform.deepseek.com/api_keys) 獲取金鑰，建立一個臨時金鑰，複製貼上到 Makers 中儲存，就可以使用 DeepSeek V4 Pro 模型了。

![](https://pic.yupi.icu/1/image-20260629153416288.png)

怎麼讓 Agent 用上這個新模型呢？是要改程式碼麼？

**其實完全不需要。**

簡單看下程式碼，你會發現，模型配置優先讀取 `AI_GATEWAY_MODEL` 這個環境變數。

![](https://pic.yupi.icu/1/image-20260629153542980.png)

所以我們只需要讓 AI 設定一下這個變數，然後重新部署就好了：

```markdown
設定 AI_GATEWAY_MODEL 環境變數為 deepseek/deepseek-v4-pro
重新部署
```

![](https://pic.yupi.icu/1/image-20260629153614603.png)

部署成功後進入 Makers 控制檯，可以看到環境變數已經生效了，很方便吧！

![](https://pic.yupi.icu/1/image-20260629153737524.png)

我們再來試一下同樣的 IDEA：做一個 AI 幫你寫朋友圈文案的小程式。

這次 Agent 進行了多輪聯網搜尋，最後又給出了扎心的銳評 —— 白送我都不要。

![](https://pic.yupi.icu/1/image-20260629153817738.png)

看看這通分析，明顯比切換模型前的效果好多了吧？它還讓我研究垂直方向……

好，那我就接著追問：我是個程式設計師和 UP 豬，怎麼垂直？

![](https://pic.yupi.icu/1/image-20260629153910912.png)

好傢伙，這能給我投 30 萬？

![](https://pic.yupi.icu/1/image-20260629153948785.png)

這個賽道分析還是有點意思的，什麼叫程式設計教學賽道已經被頭部吃幹抹淨，這個 ** 魚皮是誰啊？！

再往下看關鍵的變現路徑，是不是跟大家想的差不多？

![](https://pic.yupi.icu/1/image-20260629154052346.png)

總結一下就是 **接廣告、賣課、搞培訓**。

不是哥們，這麼真實嗎？

![](https://pic.yupi.icu/1/image-20260629153948785.png)



## 迭代最佳化
到目前為止功能已經跑通了，但我發現一個問題：多輪對話記憶好像沒有生效，Agent 不記得之前聊過什麼。

![](https://pic.yupi.icu/1/image-20260629154338029.png)

所以接下來要做一些最佳化。

先讓 AI 用 Git 提交一版程式碼，萬一改出問題也好及時回滾：

![](https://pic.yupi.icu/1/image-20260629154359603.png)

然後讓 AI 進一步最佳化、更新已部署的網站、並透過 Browser Use 自主驗證效果、修復 Bug：

```markdown
最佳化專案、更新部署、自主驗證並修復 Bug
1. 必須支援多輪對話，使用者可以根據反饋調整方案繼續追問，Agent 要記住之前聊過的內容
2. 最佳化前端頁面，禁止使用 Emoji，對標商業產品，保持 Q 版風格
3. 最佳化 Markdown 格式的展示
```

![](https://pic.yupi.icu/1/image-20260629154415031.png)

AI 很快修復了程式碼，利用 `makers-deploy` 技能更新了線上的網站，然後自己開啟瀏覽器對話驗證。

![](https://pic.yupi.icu/1/image-20260629154440381.png)

來看看最終的效果，Markdown 的展示格式優雅多了。

![](https://pic.yupi.icu/1/image-20260629154501108.png)

而且這次多輪對話記憶也成功生效了！

![](https://pic.yupi.icu/1/image-20260629154512485.png)

你會發現，我們全程沒有開通任何資料庫或儲存服務，對話記憶是 EdgeOne Makers 平臺幫我們搞定的，它在底層管理了每個使用者的對話歷史，不同使用者之間互不干擾。

![](https://pic.yupi.icu/1/image-20260629154621230.png)

加上之前演示的聯網搜尋、模型閘道器，這些能力都是部署上去自動就有的，我們自己完全不用操心。

![](https://pic.yupi.icu/1/05_EdgeOne_Makers%E7%BB%BC%E5%90%88%E8%83%BD%E5%8A%9B%E4%B8%8EAgent%E5%85%B3%E7%B3%BB_compressed_v2.png)

此外，進入 Makers 控制檯的呼叫鏈路追蹤面板，你可以看到 Agent 呼叫次數和 Token 消耗等資料。

![](https://pic.yupi.icu/1/image-20260629154709800.png)

甚至能夠看到某一次呼叫的完整鏈路日誌，每一次 AI 生成和工具呼叫的細節都一目瞭然，便於最佳化 Agent 和排查問題。

![](https://pic.yupi.icu/1/image-20260629154738024.png)



## 成品體驗
到這裡，我的 AI 投資人 Agent 就開發完成了，我可以愉快地用它來驗證各種副業想法。

比如我要在閒魚上接單：

```markdown
在閒魚上接單，幫人用 AI 寫文案/簡歷/小紅書筆記，收費 30 ~ 100 一單
```

得，看來不行。

![](https://pic.yupi.icu/1/image-20260629154800071.png)

我要搭 AI 的 API 中轉站：

```markdown
搭一個 AI API 中轉站，幫國內使用者方便地呼叫 GPT/Claude，賺差價
```

得，看來又不行！

![](https://pic.yupi.icu/1/image-20260629154828473.png)

我要做個 AI 英語口語陪練 App：

```markdown
做一個 AI 英語口語陪練 App，用語音對話的方式幫使用者練口語，按月訂閱 29.9 元
```

得，看來又又不行！！

![](https://pic.yupi.icu/1/image-20260629154922290.png)

我要擺攤賣程式設計師炒飯：

```markdown
我要擺攤賣程式設計師炒飯，透過線上拍短影片營銷
```

呃啊，看來想搞一個好的專案 IDEA 不容易啊！

![](https://pic.yupi.icu/1/image-20260629154950801.png)

算了，還是賣課吧：

```markdown
我有流量基礎，錄製程式設計教程，在自己的平臺上賣課，收費幾百到幾千不等
```

我 Chovy！！！賣課也不容易啊。

![](https://pic.yupi.icu/1/image-20260629155029876.png)

唉，錢難賺，屎難吃。

接下來，我又試了很多個 IDEA，全部都被 AI 否定了。

![](https://pic.yupi.icu/1/image-20260629155623574.png)

哼，我就不信沒有辦法搞出 S 級想法！

![](https://pic.yupi.icu/1/image-20260629155749578.png)

一個人的力量是渺小的，所以我決定把這個專案開源出來，大家可以直接讓 AI 幫你部署到 EdgeOne Makers 上，就能隨時隨地驗證自己的想法了，坐等一批 A 級和 S 級想法。

> 開源指路：https://github.com/liyupi/ai-investor

![](https://pic.yupi.icu/1/image-20260629155812766.png)



## 寫在最後

從寫程式碼到上線，整個過程不到 20 分鐘。回過頭來想想，我只關注了 Agent 的業務邏輯，其他的聯網搜尋、對話記憶、模型閘道器、鏈路追蹤這些工程化的東西，[EdgeOne Makers](https://cloud.tencent.com/act/pro/edgeone-makers-agent?from=30133) 全幫我搞定了。

AI 時代，大模型的能力很重要，但給大模型提供的這一系列配套能力同樣重要。模型再強，沒有靠譜的工程化支撐，Agent 也只能停留在本地 Demo 階段。能讓開發者把精力全部放在業務邏輯上，而不是重複造輪子，這是非常有價值的事。
