# DeepSeek Harness 精選外掛推薦

> 一次性鑑賞 DSH 社群熱門外掛，從實用工具到整活神器，量大管飽。

大家好，我是程式設計師魚皮。

DeepSeek Harness 是 DeepSeek 官方最新開源的 AI Agent 執行環境，簡稱 DSH。

你可以把它理解成一個高度可定製的 AI 程式設計工具，對標 Claude Code 和 Codex，核心理念是「一切皆外掛」。

![](https://pic.yupi.icu/1/image-20260814133452050-20260819135304416.png)

DSH 整套架構是建立在一個叫 Cordis 的元框架上的。模型介面卡、工具登錄檔、會話日誌、Agent 迴圈，甚至 Web 介面本身，全都是可以熱插拔的外掛。你想換模型、換工具、換互動方式，改一下配置就行，不用動原始碼。

雖然目前 DSH 自帶的能力還不夠豐富，但正因為這種徹底的外掛化設計，社群補能力的速度非常快。才短短一週多，GitHub 的 `dsh-plugin` 標籤下已經冒出了數千個社群外掛，有給 Agent 補充能力的、有改進 UI 介面的、也有很多奇奇怪怪的抽象藝術作品……

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

這篇文章我就來帶大家鑑賞一大波 DeepSeek Harness 熱門外掛，有實用的、也有好看的。

![](https://pic.yupi.icu/chengfang/02.png)

魚皮甄選，量大管飽。建議收藏，讓你的鯨魚變得更強！



## 發現優質 DSH 外掛

首先，到哪裡去找 DeepSeek Harness 的優質外掛呢？

最直接的方法是看 GitHub 的 [dsh-plugin 主題專區](https://github.com/topics/dsh-plugin)。很多開發者釋出外掛後都會給倉庫打上 `dsh-plugin` 這個標籤，新出的外掛基本都能在這裡看到。

這個方法的優點是更新快、數量多；缺點就是魚龍混雜，因為誰都可以給倉庫加這個標籤，不代表這些外掛經過稽核，也不能按照質量來排序。

![](https://pic.yupi.icu/chengfang/03DSH.png)

如果懶得一個個翻倉庫，可以看看 [Awesome DSH Plugin](https://awesome-dsh-plugin.com/zh/)。它是社群整理出來的一份優質外掛清單，按照用途做分類，便於你快速發現一些熱門外掛。不過它同樣屬於社群維護，適合拿來找外掛、看熱度，不能當做是官方推薦的。

![](https://pic.yupi.icu/chengfang/004DSH.png)

有趣的是，DSH 外掛多起來以後，連「找外掛」這件事本身都被做成外掛了。

比如我後面會提到的 dsh-market 外掛，把它裝進 DeepSeek Harness 後就相當於多了一個外掛市場。

在這裡你不僅能夠直接瀏覽和搜尋外掛，還能看到根據你當前已安裝的外掛繼續推薦的相關專案。

舉個例子，我不用提前知道 dsh-pocket 這個外掛叫什麼名字，只要搜尋「遠端」兩個字，dsh-market 外掛就會匹配到對應的專案。

![](https://pic.yupi.icu/chengfang/007DSH.png)

那怎麼安裝外掛呢？

其實不用自己折騰命令，我基本都是直接把 GitHub 倉庫地址丟給 DeepSeek Harness，讓 AI 自己讀取倉庫的 README 專案介紹檔案、查詢安裝方式、執行安裝命令，裝完以後按照 AI 的提示重啟 `dsh web` 就行。

![](https://pic.yupi.icu/1/image-20260814145412556.png)



## 優質 DSH 外掛推薦

接下來正式進入外掛推薦環節。我把這次測試過的外掛分成了 3 類，分別是擴充套件 DSH 技能的、增強面板體驗的，以及社群整活的。

下面先來看第一類，能直接給 DSH 補能力的外掛。



### DSH 技能擴充套件



#### ModLens 讓 DeepSeek 理解圖片

這是我個人最看好的一個外掛，給原本只能看文字的 AI 模型補了一雙慧眼。

> 開源倉庫：https://github.com/liustack/modlens

![](https://pic.yupi.icu/chengfang/033DSH1.png)

DeepSeek V4 系列模型只能處理純文字。雖然 DeepSeek 官方 APP 裡已經灰度上線了識圖模式，但在 DSH 裡呼叫的是 API 介面，如果你直接貼上一張截圖進對話，AI 根本看不懂。

ModLens 解決的就是這個問題。當你貼上圖片後，外掛會自動把圖片轉發給一個外部的視覺模型（比如 Qwen），由視覺模型把圖片內容解析成結構化的 JSON 資訊，包括 OCR 識別出的文字、頁面的佈局區域，以及圖片裡的語義內容，然後再把這些資訊作為上下文餵給 DeepSeek，讓它能夠基於圖片內容繼續推理。

![](https://pic.yupi.icu/chengfang/027DSH.png)

和普通的 OCR 工具不一樣，ModLens 保留的不只是文字，還有元素之間的位置關係和語義。所以對於經常用 AI 做前端的朋友來說非常實用，頁面做完以後直接把截圖丟給 DSH，讓它自己檢查還原度就行了。



#### ModSearch 擴充套件搜尋源

ModSearch 是一個搜尋增強外掛，可以給 DSH 接入 Firecrawl、Tavily、Exa 等不同搜尋源，還能繼續擴充套件 Twitter 搜尋的能力。

> 開源倉庫：https://github.com/liustack/modsearch

![](https://pic.yupi.icu/chengfang/034DSH1.png)

雖然 DSH 原生就自帶聯網搜尋，但是搜尋範圍有限。

比如我讓 AI 搜尋當天 Twitter 上關於 DeepSeek Harness 的討論，AI 明確告訴我當前搜尋工具拿不到 Twitter 的實時原帖，只能從媒體和社群文章裡找到一些轉述內容。

![](https://pic.yupi.icu/chengfang/23DSH.png)

裝上 ModSearch 後，我故意沒有配置 API Key，又讓 AI 搜尋同一個問題。這一次 AI 直接搜到了一條 Twitter 上的原帖，點開連結就能驗證。

![](https://pic.yupi.icu/chengfang/25DSH.png)

不過 Twitter 搜尋到這一步並沒有完全跑通，更完整的搜尋能力還需要額外配置對應服務的 API Key 才能用。如果你平時需要在全網範圍深度檢索資料，配好之後會很香。



#### dsh-browser 操作瀏覽器

dsh-browser 可以讓 DSH 直接操作你正在用的 Chrome 瀏覽器，比如讀取網頁內容、點選連結、填寫表單、跳轉頁面等等。

> 開源倉庫：https://github.com/Lum1104/dsh-browser

![](https://pic.yupi.icu/chengfang/035DSH.png)

和一般的無頭瀏覽器方案不同，dsh-browser 連線的是你電腦上真實的 Chrome 標籤頁。瀏覽器裡的 Cookie、Session、登入狀態全都能直接複用，不需要給 AI 單獨再登入一次。

它的技術方案是一個 DSH 橋接外掛加一個 Chrome MV3 擴充套件，兩邊透過本地 WebSocket 通訊。外掛把網頁內容轉成結構化的文字描述（帶編號的可互動元素列表）發給 DeepSeek，DeepSeek 不需要「看圖」就能理解頁面結構並執行操作。

這個外掛的安裝會稍微麻煩一點。除了安裝 dsh-browser 外掛本身，還得額外在 Chrome 里載入一個本地擴充套件。

![](https://pic.yupi.icu/chengfang/010DSH.png)

我直接讓 DSH 按照外掛的 README 文件自動安裝。AI 把原始碼、依賴和擴充套件都構建好了，最後只需要我在 Chrome 的 `chrome://extensions` 頁面手動載入本地擴充套件目錄。

![](https://pic.yupi.icu/chengfang/26DSH.png)

擴充套件開啟後，看到 `Connected` 就說明連線成功了。

![](https://pic.yupi.icu/chengfang/28DSH.png)

我先拿 GitHub 做了一輪測試，把自己的開源專案主頁丟給它，讓它找到頁面裡的置頂倉庫，再點進去繼續檢視詳情。

從讀取頁面、定位倉庫，到點選進入並讀取專案資訊，整套流程全部跑通。

![](https://pic.yupi.icu/chengfang/821DSH.png)

接下來我又讓 AI 透過 Twitter 頁面搜尋 DSH 相關內容。結果它真的在 Twitter 的搜尋框裡自動輸入關鍵詞、執行搜尋，再切到最新結果檢視剛釋出的帖子。

![](https://pic.yupi.icu/chengfang/012DSH.png)

這和前面的 ModSearch 外掛定位不同。ModSearch 更適合從搜尋引擎渠道查詢資料，而 dsh-browser 是讓 AI 直接操作你已經登入的真實網站，適合填表、發帖、查詢後臺這種需要帶登入態的操作。

不過 dsh-browser 並不會完全放任 Agent 隨便操作。點選、輸入、頁面跳轉這些動作預設都會彈確認框讓你過目。手動切換標籤頁後，它也會停下來詢問是繼續控制原頁面還是跟隨當前頁面。

實際使用時還有一個小細節值得注意。dsh-browser 預設繫結當前活動標籤頁，如果直接在 DSH 頁面裡讓它開啟 GitHub，當前聊天頁面可能也會被跳走。後來我改成先開啟目標網站的標籤頁，再從 Chrome 側邊欄發起對話，用起來就順手多了。

![](https://pic.yupi.icu/chengfang/062DSH.png)



#### Agent Teams 組一支 Agent 團隊

Agent Teams 是一個多 Agent 協作外掛，可以讓 DSH 同時拉起多個 Agent 各自幹活，結果統一彙總到一個 Captain（隊長）節點。

> 開源倉庫：https://github.com/NanmiCoder/dsh-agent-teams

![](https://pic.yupi.icu/chengfang/036DSH.png)

Captain 負責拆分任務、分配工作並做最終彙總，下面的成員 Agent 則各自處理不同方向的問題。

我拿它檢查了一個前端專案，建立了 3 個成員分別負責不同維度：

```
前端 Agent：檢查頁面結構、互動邏輯、響應式和明顯的前端問題
程式碼質量 Agent：檢查專案結構、依賴管理和程式碼可維護性
安全 Agent：檢查敏感資訊洩露、依賴風險和明顯的安全隱患
```

任務跑起來以後，右邊的活動面板能直接看到 3 個 Agent 同時在工作。等它們各自檢查完成，結果會統一回到 Captain，由 Captain 彙總並給出最終報告。

![](https://pic.yupi.icu/chengfang/14DSH.png)

**更牛的是，這支 Agent 團隊做完一次任務後不會馬上消失，後面還能繼續複用。**

![](https://pic.yupi.icu/chengfang/013DSH.png)

這一輪檢查結束後，我又追問了一個 WebGL 降級的問題，並且指定只讓 frontend 成員繼續處理。結果活動面板裡真的只有它重新進入了工作狀態，另外兩個成員沒有被重複排程。

![](https://pic.yupi.icu/chengfang/014DSH.png)

所以它和臨時開多個 Agent 還是有區別的。建立好的團隊和成員會一直保留，後續可以按需指派任務。

對於程式碼審查、多維度調研這類能拆成多個方向的任務，用 Agent Teams 比較合適。但如果任務本身很簡單，就沒必要特意拉一支隊伍，反而會增加排程時間和 Token 消耗。



### DSH 實用工具與介面

接下來是第二類，這些外掛主要增強 DSH 的面板能力和使用體驗，日常用起來更順手。



#### dsh-market 給 DSH 裝個外掛市場

前面說過，DSH 外掛越來越多以後，光靠自己翻 GitHub 找外掛其實挺麻煩的。

dsh-market 相當於在 DSH 裡內建了一個外掛市場，不用離開 DSH 就能瀏覽、搜尋和安裝外掛，還會根據你已經安裝的外掛推薦相關專案。

> 開源倉庫：https://github.com/2BingLing/dsh-market

![](https://pic.yupi.icu/chengfang/050DSH.png)

常用的功能有 2 個，第一個是個性化推薦。外掛知道你已經裝了什麼，推薦的東西會越來越對味兒，不用每次都自己尋找新的外掛。

![](https://pic.yupi.icu/chengfang/35DSH.png)

第二個是按功能關鍵詞搜尋外掛。比如我想找一個可以用手機遠端控制 DSH 的外掛，只要搜「遠端」兩個字就能匹配到相關專案，不需要提前記住外掛名字。

![](https://pic.yupi.icu/chengfang/007DSH.png)



#### dsh-web-ui 網站功能增強

dsh-web-ui 是一個 Web 端增強外掛，整合了任務看板、Git 管理、工作臺、狀態資訊、皮膚主題和桌寵等一系列功能，裝完以後整個頁面會更像一個完整的開發工具。

> 開源倉庫：https://github.com/zhu1090093659/dsh-web-ui

![](https://pic.yupi.icu/chengfang/038DSH1.png)

我一開始看到它的名字，還以為只是簡單改改介面樣式。結果裝完才發現，這東西簡直是一個超級全家桶！

![](https://pic.yupi.icu/chengfang/016DSH.png)

我最先試的功能是任務看板。你可以直接新建任務，寫清楚要讓 Agent 做什麼，任務從開始到完成的進度都會顯示在看板裡，而且點進去還能找到真正執行這個任務的 DSH 會話。

![](https://pic.yupi.icu/chengfang/06DSH.png)

它把 Git 相關功能做得也很完整。可以直接搜尋、切換和新建分支，還能把之前的程式碼提交記錄畫成一張 Git 圖譜，把每次提交和不同分支之間的關係都清晰地展示出來。

![](https://pic.yupi.icu/chengfang/08DSH.png)

我裝的是 `dsh-web-ui` 的全家桶版本，它還會一起安裝 `dsh-better-sidebar`，所以右邊會直接多出一套類似 VS Code 的開發工具欄。

![](https://pic.yupi.icu/chengfang/017DSH.png)

全家桶整合的 better-sidebar 裡，檔案列表還帶了 `@檔案` 按鈕，看到需要的檔案可以直接引用到當前對話裡，不用再自己手動複製路徑。

![](https://pic.yupi.icu/chengfang/019DSH.png)

怎麼樣，這個外掛是不是挺強的？感覺官方沒做的很多功能都被它實現了。



#### DSH-better-sidebar 加強側邊欄

DSH-better-sidebar 是一個側邊欄增強外掛，把檔案樹、終端、Git 狀態這些開發時常用的面板集中到 DSH 右側，減少來回切視窗的麻煩。

> 開源倉庫：https://github.com/omdsh-dev/DSH-better-sidebar

![](https://pic.yupi.icu/chengfang/039DSH.png)

和前面的 `dsh-web-ui` 相比，它沒有任務看板、皮膚中心、桌寵這些額外功能，更專注於側邊欄本身，介面也更簡潔。

![](https://pic.yupi.icu/chengfang/018DSH.png)

如果你覺得全家桶功能太多用不上，也可以只裝這一個，單獨用更輕量。



#### dsh-context 上下文增強

dsh-context 是一個上下文視覺化外掛，可以直接檢視當前會話裡上下文的組成情況、佔用比例和變化記錄。

> 開源倉庫：https://github.com/bowenliang123/dsh-context

![](https://pic.yupi.icu/chengfang/040DSH.png)

用 AI 程式設計聊久了以後，經常會發現對話越來越慢、上下文越堆越大。但到底是歷史訊息、檔案內容還是工具呼叫結果佔了大頭，平時其實很難直觀看出來。

`dsh-context` 做的就是把這些原本藏在後臺的資料直接攤開給你看。點一下上下文按鈕，就能看到當前上下文的體檢報告，每一類資訊佔了多少 Token 一目瞭然。

![](https://pic.yupi.icu/chengfang/38DSH.png)

如果你經常跑長會話或者頻繁呼叫工具，它會很實用。至少上下文快頂滿的時候，你能知道該清理什麼，不用再盲目地直接開一個新會話。



#### dsh-TUI 終端操作介面

dsh-TUI 是一個終端互動介面外掛，適合更習慣 Claude Code 那種終端操作風格的使用者。

> 開源倉庫：https://github.com/ccch1mneyyy/dsh-TUI

![](https://pic.yupi.icu/chengfang/041DSH.png)

裝好執行以後，會直接進入一套全屏終端介面，底部實時顯示當前模型、推理強度、上下文佔用百分比等資訊，簡單粗暴。

![](https://pic.yupi.icu/chengfang/020DSH.png)

但是我不太建議新手直接裝這個，因為 dsh-TUI 對 DSH 的介面和互動改動比較大，而 DSH 官方還在快速迭代中，後續如果新增了什麼能力或者改了介面，這個外掛不見得能第一時間跟上，到時候出了相容問題排查起來會比較頭疼。



#### dsh-genui 介面渲染

dsh-genui 是一個生成式 UI 外掛，可以讓 DSH 的回覆不再侷限於文字和 Markdown，而是直接在對話裡渲染卡片、圖表、選項按鈕等互動介面。

> 開源倉庫：https://github.com/omdsh-dev/dsh-genui

![](https://pic.yupi.icu/chengfang/042DSH.png)

我新開了一個對話，讓它生成一個「AI 程式設計工具對比面板」，包含資訊卡片和柱狀圖。結果真的直接在 DSH 的聊天視窗裡渲染了出來，而且是實實在在可以互動的元件。

![](https://pic.yupi.icu/chengfang/37DSH.png)

如果你經常讓 AI 做資料展示或者方案對比，覺得純文字回答太單調，這個外掛值得一試。



#### dsh-pocket 手機遠端操控

dsh-pocket 可以把電腦上正在執行的 DSH 連線到手機上，掃一下二維碼就能在手機瀏覽器裡繼續檢視 Agent 的工作狀態、傳送訊息。

> 開源倉庫：https://github.com/shaobeichen/dsh-pocket

![](https://pic.yupi.icu/chengfang/043DSH.png)

這個外掛支援區域網和公網兩種模式，我都測試過了。

區域網模式很簡單，手機和電腦連同一個 WiFi，掃描二維碼後就能直接開啟 DSH 介面。

![](https://pic.yupi.icu/chengfang/021DSH.png)

公網模式更通用，手機不需要和電腦在同一個網路裡，隨時隨地可以訪問。第一次開啟會要求輸入一個訪問密碼，每次重新開啟公網訪問時密碼會自動更換。

![](https://pic.yupi.icu/chengfang/044DSH.png)

最關鍵的是，公網訪問不需要你自己額外買伺服器！dsh-pocket 會透過 Cloudflare Quick Tunnel 建立一個臨時的公網通道，把外部請求轉發到電腦本地執行的 DSH。手機端和電腦端之間的流式輸出透過 WebSocket 全程透傳，電腦上正在輸出的內容手機上也能實時滾動。

也就是說，以後 DSH 在電腦上跑一個耗時較長的任務，出去吃飯的時候掏出手機還能繼續看進度、發訊息。

不過方便的同時，也要注意安全。遠端二維碼、公網地址和訪問密碼別隨便分享給別人，畢竟 DSH 本身可以操作本機檔案和程式碼，暴露的後果可想而知……



### DSH 整活玩法

前面兩類外掛多少還在認真地給 DSH 補充能力、最佳化體驗。

接下來，外掛的畫風就開始逐漸跑偏。。。

![](https://pic.yupi.icu/1/e02764373d3605e8c6b758e546b52410500385529.jpg)



#### dsh-deep-whale 鯨魚娘皮膚

deep-whale 是一個主題外掛，裝上以後，整個 Web 介面會直接換成鯨魚娘風格。

> 開源倉庫：https://github.com/Small-tailqwq/dsh-deep-whale

![](https://pic.yupi.icu/chengfang/045DSH1.png)

裝上以後的效果，直接看圖：

![](https://pic.yupi.icu/1/image-20260814133452050.png)

效果不錯吧，是不是突然更有開啟 DSH 的動力了？

雖然它並沒有給 DSH 增加新功能，但不得不說，這種東西確實很適合社群傳播，誰看了這個圖不想裝一個？



#### whale-girl 互動更強的桌寵

whale-girl 是一個桌寵外掛，可以直接在 DSH 裡養一隻萌萌噠鯨魚娘桌寵。

> 開源倉庫：https://github.com/vlln/whale-girl

![](https://pic.yupi.icu/chengfang/046DSH.png)

前面的 dsh-web-ui 外掛也帶了桌寵功能，不過我實際對比下來，兩邊體驗差別還挺明顯的。

dsh-web-ui 自帶的桌寵更像一個「工作狀態提示器」，Agent 幹活時會告訴你正在整理資料、任務完成了之類的。

而 whale-girl 更像以前的 QQ 寵物。滑鼠懸浮上去可以看到等級和當前狀態，點開選單還能投餵、玩耍。

![](https://pic.yupi.icu/chengfang/41DSH.png)

它還會跟著 Agent 的工作狀態做不同動作，比如思考的時候歪頭、等待的時候打哈欠、完成任務後歡呼、空閒久了就開始睡覺。

雖然實際上沒什麼用，但是能提升使用 AI 的情緒價值，還要什麼腳踏車？



#### dsh-liang-skin 滑動變祖器

dsh-liang-skin 是一個 DSH 皮膚外掛，直接把推理強度滑塊做成了「滑動變祖器」。

> 開源倉庫：https://github.com/kingOfSoySauce/dsh-liang-skin

![](https://pic.yupi.icu/chengfang/047DSH.png)

來試試看，拖動推理強度的時候，你能夠見證人物從樑子一路進化到梁祖的過程。

![](https://pic.yupi.icu/chengfang/%E6%B5%8B%E9%87%8F%E4%BB%AA.png)

這真的是碳基生物能想到的創意嗎？？？

![](https://pic.yupi.icu/1/image-20260821101545031.png)



#### dsh-deepcel 把 DSH 偽裝成 Excel

dsh-deepcel 是一個 Excel 風格的主題外掛，裝上以後整個頁面會變成經典的表格介面。

> 開源倉庫：https://github.com/Small-tailqwq/dsh-deepcel

![](https://pic.yupi.icu/chengfang/048DSH.png)

看下效果，還原度還是很高的吧？

![Excel 風格的 deepseek harness](https://pic.yupi.icu/1/Excel%20%E9%A3%8E%E6%A0%BC%E7%9A%84%20deepseek%20harness.jpeg)

感覺這玩意很適合經常用 Excel 辦公的同學，當成一個摸魚神器應該挺好的。



#### dsh-ads 把廣告塞進 DSH

dsh-ads 是一個專門給 DSH 塞復古廣告的整活外掛。裝上以後，整個頁面會冒出各種 2005 年中文網際網路風格的彈窗廣告。

> 開源倉庫：https://github.com/Nagi-ovo/dsh-ads

![](https://pic.yupi.icu/chengfang/066DSH.png)

資訊流廣告、彈窗、假防毒、假遊戲，還有各種花裡胡哨的橫幅，全都能往 DSH 裡塞。

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

抽象，太抽象了！你管這叫 AI 工具？



## 寫在最後

最後，我把這次測試過的精選 DSH 外掛按照使用場景整理成了一張圖，供大家參考：

![](https://pic.yupi.icu/chengfang/032DSH.jpg)

多說兩句，雖然 DeepSeek Harness 一切皆外掛的設計給了大家無限的定製空間，但外掛畢竟是第三方程式碼，尤其是會操作瀏覽器、Shell、檔案和遠端訪問的外掛，一定要注意安全，安裝前最好去看一下倉庫來源和它宣告的許可權範圍。

而且 DSH 自身也還在快速迭代，很多外掛不一定能做到完美相容。像我這次測試過程中就遇到過因為外掛版本不相容導致 Web 無法正常啟動的情況。所以我建議只安裝有剛需的外掛，而且要利用 Git 版本控制工具來管理本地的 DSH，出了問題也好回滾到之前正常的版本。

如果你想系統學習 DeepSeek Harness 的基礎用法，可以閱讀本教程程式設計工具板塊 DeepSeek Harness 目錄中的《DeepSeek Harness 保姆級入門教程》，從安裝到實戰一篇搞定。
