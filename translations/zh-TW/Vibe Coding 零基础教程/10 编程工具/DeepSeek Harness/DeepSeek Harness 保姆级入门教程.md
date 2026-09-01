# DeepSeek Harness 保姆級入門教程

> 從安裝到實戰再到外掛開發，手把手帶你玩轉 DeepSeek 官方開源的 AI 程式設計工具。

大家好，我是程式設計師魚皮。

DeepSeek 在釋出 V4 Pro 正式版的同時，還開源了萬眾矚目的 DeepSeek Harness。

![](https://pic.yupi.icu/1/image-20260814125428438.png)

DeepSeek Harness 開源的 [GitHub 倉庫](https://github.com/deepseek-ai/deepseek-harness) 上線不到 1 天，就衝到了 7 萬多 Star，AI 屆的頂流果然名不虛傳。

![](https://pic.yupi.icu/1/image-20260814142939760.png)

這篇文章我會從安裝開始，手把手帶你體驗 DeepSeek Harness 的核心玩法，小白可懂，建議收藏~



## 一、DeepSeek Harness 是什麼？

Harness 這個詞翻譯過來就是「駕馭」，如果把 AI 模型比作一匹馬，那 Harness 就是你駕馭 AI 模型這匹馬所需要的一切工程。

所謂 Harness 工程，就是研究怎麼讓 AI 模型這匹馬跑得更快、更穩，順利完成任務。

你給 AI 寫的專案規則檔案、配置的各種工具、安排的任務拆分和執行順序、設計的測試檢查流程，這‌些統統都算 Harness。

![](https://pic.yupi.icu/1/2_harness_horse.png)

有一個很精妙的公式：**Agent = Model + Harness**

模型負責思考和生成，Harness 負責把這些能力接入檔案系統、終端、網頁、工具鏈，讓 AI 真正能在現實環境裡幹活。

![](https://pic.yupi.icu/1/8_agent_queals.png)

之前 DeepSeek 只開源了模型這一半，Harness 一直沒動靜，這次終於補齊了。

你可以把 DeepSeek Harness 理解成一個 **可以高度定製的 AI 程式設計工具**，對標 Claude Code 和 Codex。

但它的野心比這些工具更大，不只是一個程式設計 Agent，而是一套可配置、可重組的 Agent 執行環境，官方口號是「一切皆外掛」。

![](https://pic.yupi.icu/1/image-20260814130507825.png)

看到這裡，你已經超過了 50% 的同學。

接下來只需要 1 分鐘，你就能把它裝到自己電腦上。



## 二、安裝

安裝 DeepSeek Harness 真的非常簡單，進入到 [DeepSeek Harness 官網](https://www.deepseek.com/harness/) 。

你會看到一行安裝命令：

![](https://pic.yupi.icu/1/image-20260814094053180.png)

在執行這行命令之前，首先要確保你的電腦已經安裝了 Node.js 環境，沒有的話去 [Node 官網](https://nodejs.org/zh-cn) 下載安裝包，傻瓜式安裝就行。

![](https://pic.yupi.icu/1/image-20260814095005547.png)

有了環境後，複製這行命令，然後開啟你電腦上的終端，輸入這行命令並執行：

```bash
npx @deepseek-ai/dsh web
```

稍等一會兒，你會看到終端輸出了一個網址，開啟它就能進入到 DeepSeek Harness 的 Web 介面。

![](https://pic.yupi.icu/1/image-20260814095037727.png)

第一次使用時，需要填入 DeepSeek 的 API Key：

![](https://pic.yupi.icu/1/image-20260814130304526.png)

到 [DeepSeek 開放平臺](https://platform.deepseek.com) 建立一個 API Key，注意不要洩露，把得到的 Key 複製貼上過來就行。

![](https://pic.yupi.icu/1/image-20260814130139004.png)

到這裡，DeepSeek Harness 就安裝成功了，是不是很簡單？

![](https://pic.yupi.icu/1/image-20260814130332224.png)

看到這裡，你已經超過了 60% 的同學，接下來我帶大家實戰體驗一下它的能力。



## 三、Harness 實戰

進入 Web 介面後，選擇一個你想讓 AI 操作的專案資料夾，就可以正式開始幹活了。

可以在對話方塊中選擇模型、以及模型的推理等級，還能設定 Agent 對檔案系統和終端的操作許可權，按需調整就好。

![](https://pic.yupi.icu/1/image-20260814143734964.png)

預設使用的是「標準模式」，它具備了一個 AI 程式設計工具應有的全部能力，大多數情況下用這個就夠了，後面我會詳細介紹各種模式的區別。

你看，是不是跟 Codex 這種 AI 程式設計工具很像？

![](https://pic.yupi.icu/1/image-20260814143812878.png)

沒錯，你就把它當成國產版的 Codex 來用就好了，AI 程式設計、自動化辦公等任務，都能搞定。

下面我們跑幾個任務試試看。



### 任務 1、分析程式碼倉庫，繪製架構圖

第一個任務，讓 DeepSeek Harness 分析它自己的原始碼倉庫，繪製一張傻子都能看懂的架構圖。

DeepSeek Harness 的程式碼倉庫還挺大的，裡面模組也多，用來測試 AI 的程式碼理解能力剛好合適。

![](https://pic.yupi.icu/1/image-20260814143958846.png)

給 AI 傳送下列提示詞：

```
分析當前專案的程式碼倉庫結構，繪製一張清晰的架構圖。
要求用 Mermaid 語法輸出，讓完全不懂程式碼的人也能一眼看明白各模組的關係。
```

可以看到 AI 開始自動讀取檔案、分析專案結構，執行速度非常快，而且每一步在做什麼都清晰地展示在介面上。

![](https://pic.yupi.icu/1/image-20260814135407082.png)

很快任務完成了，能夠看到 AI 輸出了 Mermaid 文字繪圖語法，不過 DeepSeek Harness 預設是不會把這塊渲染成圖形的。

![](https://pic.yupi.icu/1/image-20260814135445191.png)

我要把這段程式碼複製到 Mermaid 渲染工具中，可以看到完整的架構圖，雖然效果中規中矩吧，但內容還是比較完整的。

![](https://pic.yupi.icu/1/image-20260814135528564.png)

你可以在下方看到任務消耗的 Tokens、當前的上下文佔用、以及整個對話的 Tokens 消耗資訊。

![](https://pic.yupi.icu/1/image-20260814135615629.png)

你還可以進入上方的「軌跡」面板，清晰地檢視到整個對話中每一次的對話和工具呼叫記錄。

![](https://pic.yupi.icu/1/image-20260814135652086.png)

這是 DeepSeek Harness 的特色，讓每一次執行都有跡可循。



### 任務 2、開發一個知識講解網站

第二個任務，讓它從零開發一個用互動式動畫講解知識的網站。

要講解的知識點是「注意力殘差」，跟我之前測評 Codex + DeepSeek V4 Pro 的時候用的是一模一樣的提示詞。

![](https://pic.yupi.icu/1/image-20260814125730242.png)

大概過了 20 分鐘，AI 完成了任務，這個速度確實不算快，主要的時間花在了 AI 的自檢上。

值得關注的是，本次任務的快取命中率達到了 99%，也就是說絕大多數的費用都按快取來計算，實際花費極低，這點很厲害啊！

![](https://pic.yupi.icu/1/image-20260814111941126.png)

看下效果，不錯，動畫還是很生動的：

![](https://pic.yupi.icu/1/image-20260814112144980.png)

而且點線之間的連線非常準確：

![](https://pic.yupi.icu/1/image-20260814112210801.png)

更讓我驚喜的是，跟之前 Claude Opus 5 開發的效果一樣，這次 DeepSeek 開發的版本也提供了總結和小測驗功能，讓整個知識講解更加全面了：

![](https://pic.yupi.icu/1/image-20260814112320399.png)

整體來看，相比於我之前用 DeepSeek V4 Pro + Codex 跑的效果要好多了！

之前的版本連線都對不齊，相信你們能明顯感受到區別。

![DeepSeek V4 Pro + Codex 的版本](https://pic.yupi.icu/1/1786598800323-d83866da-24d8-4d07-9de8-72468e9102e8.png)

單看這一個例子，我真有種感覺 DeepSeek V4 Pro 可以對標 Claude 了，看來 Harness 真的很重要。



### 任務 3、開發一個 3D 遊戲

第三個任務難度升級，讓它開發一個 3D 網頁小遊戲。

這次做的是千萬元以內最好的玩具「竹知了」，不過這次比之前測評的 2D 版本複雜多了，還要支援攝像頭識別手勢來控制竹知了旋轉。

![](https://pic.yupi.icu/1/image-20260814125744391.png)

可以看到 AI 在開發過程中，會自己檢查驗證程式是否正常：

![](https://pic.yupi.icu/1/image-20260814125858778.png)

這次跑了將近 40 分鐘，AI 完成了任務，快取命中率竟然接近 100%！

![](https://pic.yupi.icu/1/image-20260814124010293.png)

看下成品效果，還是不錯的吧，可以透過滑鼠拖拽來旋轉角度：

![](https://pic.yupi.icu/1/image-20260814124039419.png)

按住竹籤來回移動滑鼠就可以控制竹知了旋轉，注意看圖片中的影子，細節做的非常好！

![](https://pic.yupi.icu/1/image-20260814124144273.png)

而且還可以開啟攝像頭，透過搓手來控制竹知了旋轉，這個互動體驗非常有趣：

![](https://pic.yupi.icu/1/image-20260814124348140.png)

整體來說，功能都是正常的，程式沒有明顯的問題，細節做的也很到位，我的評價是非常優秀。

相比之前用 DeepSeek V4 Pro + Codex 搓的 2D 版本強了太多了：

![之前 DeepSeek V4 Pro + Codex 做的 2D 版本](https://pic.yupi.icu/1/1786599373401-a561d583-aeca-46c3-9895-d55c9356e731.png)



### 任務 4、開發全棧 AI 應用

最後一個任務，讓它開發一個內建 AI 大模型呼叫能力的全棧應用「AI 網頁 PPT 生成器」。

使用者貼上一段長文案進去，後端呼叫 DeepSeek 大模型把文案拆解成多頁 PPT，前端渲染成可以全屏演示的網頁 PPT。

這次我特意在提示詞裡讓 AI 自己從我電腦上獲取 DeepSeek 的 API Key，看看它能不能自己搞定。

![](https://pic.yupi.icu/1/image-20260814125805219.png)

執行過程中，AI 可能會向你確認許可權，比如要不要允許讀取某個檔案、要不要執行某條命令，安全性這塊還是挺到位的。

![](https://pic.yupi.icu/1/image-20260814124930962.png)

大概半小時左右，AI 完成了任務，來看下效果。

這個介面風格還可以哈，也是有點兒科技感的，來貼上一段要製作 PPT 的文章。

這裡有驚喜！我們可以自己定義生成 PPT 的風格，還可以選擇是否開啟推理模式。

![](https://pic.yupi.icu/1/image-20260814145140404.png)

然後點選生成 PPT。

生成過程中，是可以實時檢視到生成進度和輸出資訊的，這個互動感比之前的老版本好太多了。

![](https://pic.yupi.icu/1/image-20260814145225002.png)

而且生成速度很快，看起來效果不錯，點選全屏檢視。

這次生成的 PPT 充滿了科技感，而且佈局也挺合理的，主次分明。

![](https://pic.yupi.icu/1/image-20260814145103287.png)

相比之前用 DeepSeek V4 Pro + Codex 做出來的版本好多了，佈局更加合理，配色也更優雅。

![之前 DeepSeek V4 Pro + Codex 做的 PPT](https://pic.yupi.icu/1/1786600257499-75fdc7f7-740c-4c27-8979-34683f66afcd.png)

你還可以切換幾種主題配色，也都是比較經典的風格了。

![](https://pic.yupi.icu/1/image-20260814145015136.png)

看到這次做出來的版本，我覺得真的可以和 Claude Opus 5 媲美了，給到頂級。

![Claude Opus 5 做的 PPT 工具](https://pic.yupi.icu/1/1785146087244-153c15ee-6ffe-4f7b-8c8d-8224fe272074-20260813162825918.png)



### 實測感受

幾個任務跑下來，DeepSeek Harness 給我的感受是速度還行。優點是快取命中率很高，而且執行過程非常清晰透明。你能看到 AI 每一步在做什麼、呼叫了哪些工具、讀了哪些檔案，不像有些工具暗箱操作，辜負使用者的信任。

單從我這幾次測試來看，DeepSeek V4 Pro 配合自家 Harness 的 AI 程式設計能力確實可以和 Claude Opus 5 對標了，官方那個只差 0.1 的跑分誠不欺我。

**看來用 DeepSeek 模型，還是得用自家的 Harness 工具啊。**

![deepseek v4 pro 跑分圖](https://pic.yupi.icu/1/deepseek%20v4%20pro%20%E8%B7%91%E5%88%86%E5%9B%BE.jpeg)

再說下費用，大家猜猜這幾個任務跑下來花了多少錢？

**答案是不到 5 塊錢！**

因為快取命中率基本都在 99% 以上，實際花費極低。

![](https://pic.yupi.icu/1/image-20260814131247833.png)

不過要提醒大家的是，DeepSeek 已經宣佈 8 月 17 日起漲價，而且漲了好幾倍。

![DeepSeek 漲價](https://pic.yupi.icu/1/DeepSeek%E6%B6%A8%E4%BB%B7%E5%9B%BE.jpeg)

但即便是漲價之後，跟 Claude 比起來還是便宜很多的，而且快取命中的價格依然非常低。

總的來說，自己的模型配自己的 Harness 工具，真的強。

![](https://pic.yupi.icu/1/image-20260814144904693.png)

看到這裡，你已經超過了 70% 的同學。

接下來我們瞭解一下 DeepSeek Harness 的幾種執行模式，看看它還有什麼用法。



## 四、4 種執行模式

DeepSeek Harness 提供了四種執行模式，適配不同的使用場景。

![](https://pic.yupi.icu/1/image-20260814145323400.png)

**標準模式** 就是我們前面實戰一直在用的那個。它載入了完整的工具組合，包括檔案編輯、Shell 命令、網頁搜尋、子 Agent、Skills 技能等等，覆蓋了日常開發的所有需求。絕大多數情況下用它就好了。

**極簡模式** 只保留了 Bash 和檔案編輯這兩件最基礎的工具，其他能力全部關掉。這個模式主要是官方拿來跑模型基準測試用的，在最小環境下考驗模型的純程式設計能力，普通使用者基本用不到。

**PTC 模式** 全稱是「程式化工具呼叫」。普通模式下 AI 是一步一步呼叫工具的，每步執行完才能決定下一步做什麼。但在 PTC 模式下，模型可以直接生成一段 TypeScript 程式碼，把多步工具呼叫串聯起來一次性執行完。適合那種步驟很多但邏輯清晰的任務，比如批次重新命名檔案、跑一整套自動化流程，效率比一步步確認要高得多。

**創造模式** 適合想要開發外掛、創造新工具或者定製模式預設的同學。它繼承了標準模式的全部能力，在此基礎上還讓 AI 可以檢查當前執行時有哪些外掛在跑、在記憶體裡試驗新的外掛組合、甚至自己創作出一個全新的模式預設。後面我們會用這個模式來開發自己的外掛。

總結一下，這四種模式的本質區別就是「當前會話載入了哪些工具外掛」。極簡模式只留兩件工具，標準模式疊滿全套能力，創造模式還能讓 AI 自己檢視和改裝當前的外掛配置。

![](https://pic.yupi.icu/1/image-20260814150646065.png)

看到這裡，你已經超過了 80% 的同學，但 DeepSeek Harness 真正讓我興奮的地方才剛剛開始。



## 五、外掛

接下來要聊 DeepSeek Harness 跟 Codex、Claude Code 這些工具最大的區別了，就是它的外掛系統。



### 一切皆外掛

DeepSeek Harness 中的一切皆外掛。

模型、工具、技能、會話、沙箱、UI，甚至 Agent 的執行迴圈本身，都是外掛，都可以拔掉換成別的。

![](https://pic.yupi.icu/1/image-20260814135129452.png)

也就是說，如果你對這個工具哪個地方不滿意，隨時可以自己替換或者安裝外掛來擴充套件，不需要改框架原始碼。

Codex 和 Claude Code 雖然也有一定的擴充套件能力，但遠沒有做到這種級別的開放，DeepSeek Harness 的定製化能力要強得多。

![](https://pic.yupi.icu/1/image-20260814135203770.png)

接下來我先帶大家使用社群外掛，再帶大家開發屬於自己的外掛。



### 使用社群外掛

在 DeepSeek Harness 官網中，點選「社群外掛」，就可以看到所有 [社群開發的外掛](https://github.com/topics/dsh-plugin) 了。

其實就是 GitHub 上打了 `dsh-plugin` 這個主題標籤的專案：

![](https://pic.yupi.icu/1/image-20260814131851843.png)

不過這個頁面的外掛又多又雜，我更建議直接去看 GitHub 上的 [Awesome 倉庫](https://github.com/awesome-dsh-plugin/awesome-dsh-plugin)，裡面有分類整理好的精選外掛列表，每個外掛都經過了驗證，目前已經收錄了 300 多個可安裝外掛，上線一天就這麼多，生態起飛的速度確實誇張。

![](https://pic.yupi.icu/1/image-20260814132201186.png)

安裝一個社群外掛也非常簡單，比如我看上了這個鯨魚娘皮膚美化外掛：

![](https://pic.yupi.icu/1/image-20260814133548484.png)

我只需要進入 DeepSeek Harness 網頁中，隨便選一個工作目錄，然後把外掛開源地址提供給 AI，讓它幫我裝就好了。

想省事的話，可以先把 Agent 的操作許可權改為全放開，這樣 AI 執行命令的時候就不用你一個個確認了。

```markdown
幫我安裝外掛 https://github.com/Small-tailqwq/dsh-deep-whale
```

![](https://pic.yupi.icu/1/image-20260814145412556.png)

很快，AI 完成了安裝。我們按它說的，開啟終端輸入命令，重新啟動一下 DeepSeek Harness 網頁：

```bash
npx @deepseek-ai/dsh web
```

重新整理，怎麼樣？！

![](https://pic.yupi.icu/1/image-20260814133452050.png)

效果不錯吧，是不是使用 AI 的念頭更強了呢？

如果你不想要這個皮膚了，直接再跟 AI 說一句話，把外掛解除安裝掉就好了：

```markdown
幫我取消掉這個外掛，回到最開始的設定
```

![](https://pic.yupi.icu/1/image-20260814133846899.png)

還有一些比較有意思的皮膚類外掛，比如 [dsh-deepcel](https://github.com/Small-tailqwq/dsh-deepcel) 把介面做成了 Excel 表格的樣子，摸魚神器啊這不是？

![Excel 風格的 deepseek harness](https://pic.yupi.icu/1/Excel%20%E9%A3%8E%E6%A0%BC%E7%9A%84%20deepseek%20harness.jpeg)

還有 [dsh-tianshu-tui](https://github.com/huiliyi37/dsh-tianshu-tui) 直接把 Web 介面換成了 TUI 終端風格：

![](https://pic.yupi.icu/1/tui-screenshot.jpg)

最離譜的是 [dsh-ads](https://github.com/dsh-external/dsh-ads) 這個外掛，它給你的 Web 介面加上了 2005 年中文網站風格的側欄廣告、對話內資訊流和角落彈窗，純粹的抽象藝術。。。

![](https://pic.yupi.icu/1/deepseek%20ads.jpeg)

因為 DeepSeek Harness 本質上就是個跑在瀏覽器裡的 Web 應用嘛，所以定製皮膚這件事非常簡單。

不過皮膚外掛只是 DeepSeek Harness 生態的冰山一角，翻一翻外掛精選列表你會發現，很多真正實用的外掛其實都在往成熟的 AI 程式設計工具產品方向靠攏。

比如 [DSH-better-sidebar](https://github.com/omdsh-dev/DSH-better-sidebar) 最佳化了側邊欄的互動體驗，[dsh-at-file](https://github.com/omdsh-dev/dsh-at-file) 讓你可以用 @ 符號快速引用檔案。

![](https://pic.yupi.icu/1/dsh-better-sidebar.png)

我個人最看好的是 [modlens](https://github.com/liustack/modlens) 這個外掛，它是 DeepSeek Harness 的第一個視覺外掛，你把圖片貼上進去，它會幫模型把圖片解析成結構化的 JSON 文字資訊，包括 OCR 文字、頁面佈局、語義內容。

![](https://pic.yupi.icu/1/demo-dsh-paste.jpg)

這個外掛解決的正是 DeepSeek V4 Pro 純文字模型看不了圖的痛點。寫完頁面沒辦法自己截圖檢查效果對不對，前端佈局有沒有錯位它全都判斷不了。現在社群直接用一個外掛把這個短板給補上了。

這些外掛補齊了 DeepSeek Harness 在互動細節和能力上的不足，也側面說明了「一切皆外掛」這個架構有多靈活，靠社群自己就能把產品體驗補上來，使用者也有了更多選擇。



### 自己創造外掛

光裝別人的外掛不過癮，其實自己開發一個外掛也很容易，因為可以直接讓 AI 幫你寫。

切換到「創造模式」，在這個模式下 AI 可以幫你檢查當前外掛樹、試驗新外掛、最終打包釋出。

![](https://pic.yupi.icu/1/image-20260814150335461.png)

比如我之前給 Codex 裝了一個桌寵外掛，現在想搬到 DeepSeek Harness 上來。

![](https://pic.yupi.icu/1/image-20260814134128295.png)

直接在創造模式下跟 AI 提需求：

```
幫我開發一個 DSH 桌寵外掛，在 Web 介面右下角顯示一個小寵物。
你需要直接把我本地的 Codex 目錄下的 Kun Like 桌寵素材移植過來，不用自己重新設計形象。
它會根據當前 Agent 的工作狀態做出不同動作。
當任務完成後，還會發出「你幹嘛~」的聲音
音訊檔案路徑在：/Users/yupi/Downloads/你幹嘛哎呦.mp3
```

![](https://pic.yupi.icu/1/image-20260814135037195.png)

AI 開發好外掛之後，會先找你人工審批，確認沒問題之後才會正式安裝，安全性很有保障。

![](https://pic.yupi.icu/1/image-20260814150406161.png)

很快開發完成，打籃球的小雞就出現在螢幕上啦！

隨便跟 AI 對話一次，就能聽到「你幹嘛~哎喲」的聲音，可謂提神醒腦、如聽仙樂耳暫明~

![](https://pic.yupi.icu/1/image-20260814143216935.png)

除了桌寵之外，你還可以發揮想象力做各種有意思的外掛，比如提醒你定時喝水的健康助手、實時展示模型賬戶餘額的懸浮窗、定製你自己的主題皮膚等等。

如果想把外掛分享給其他人，只需要讓 AI 透過 GitHub MCP 外掛，把程式碼推送到 GitHub：

![](https://pic.yupi.icu/1/image-20260814143547057.png)

很快就開源完成了：

![](https://pic.yupi.icu/1/image-20260814145634209.png)

然後給倉庫打上 `dsh-plugin` 的 topic 標籤就行了：

![](https://pic.yupi.icu/1/image-20260814145913770.png)

AI 甚至幫我給 README 專案介紹文件中新增了效果截圖，太貼心了吧！這下大家都可以一起來做小黑子了~

> 開源指路：https://github.com/liyupi/dsh-kun-like-pet

![](https://pic.yupi.icu/1/image-20260814145958050.png)



## 寫在最後

恭喜你，DeepSeek Harness 才釋出了一天，你就已經掌握了 DeepSeek Harness 的基礎用法，至少超過了 90% 的同學！

時間原因，還有很多 DeepSeek Harness 的進階玩法我沒有展開，比如用命令列模式批次跑任務、接入和切換其他大模型、自定義 Agent 預設來適配不同的工作場景、甚至把它部署到伺服器上讓整個團隊共享等等。這些內容我會在後續的進階教程裡詳細講解。

我非常看好這個專案，因為「開源 + 一切皆外掛」，讓 DeepSeek Harness 做到了極致的開放，它的可能性是無限的。

**也許用不了多久，我們每個人手裡的 AI 程式設計工具都長得不一樣，因為每個人都可以根據自己的需求自由組裝，我覺得這是一件很酷的事情~**

如果你想更系統地學習 AI 程式設計，可以閱讀本教程程式設計工具板塊中的其他文章，從安裝配置到專案實戰，一步步帶你成長。

加油，期待你用 DeepSeek Harness 做出更多有意思的東西！
