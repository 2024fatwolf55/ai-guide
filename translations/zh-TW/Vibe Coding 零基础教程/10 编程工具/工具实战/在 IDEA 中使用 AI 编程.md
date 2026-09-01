# 在 IDEA 中使用 AI 程式設計

> 雖然 AI 程式設計工具快速發展，但很多同學和團隊仍然在使用 JetBrains IDEA 進行開發。好訊息是，IDEA 同樣可以接入 AI 程式設計能力，下面介紹幾種方式。



## 1、在終端裡執行 AI

開啟 IDEA 內建的終端，你會發現終端右側直接就有 Claude Code、Codex 等 AI 工具的快捷入口（前提是你已經提前安裝好了這些工具）。除此之外，JetBrains 自家的 Junie CLI 也可以在終端裡執行。

![](https://pic.yupi.icu/1/image-20260515124926235.png)

本質上就是幫你在終端裡執行了執行這些工具的命令，跟你在外部終端用沒什麼區別，只是不用來回切視窗了。



## 2、安裝第三方 AI 外掛

雖然現在獨立的 AI 程式設計工具發展很快，但 JetBrains Marketplace 上的 AI 外掛也一直在更新迭代，選擇很多。

![](https://pic.yupi.icu/1/image-20260515125149230.png)

我個人比較推薦通義靈碼和 Cline。通義靈碼對國內使用者比較友好，註冊簡單，免費額度也夠用。Cline 的 Agent 能力強，適合喜歡折騰的同學。

![](https://pic.yupi.icu/1/cline.png)



## 3、透過 ACP 協議接入 AI

2026 年 1 月，JetBrains 和 Zed 聯合推出了 ACP（Agent Client Protocol）協議。

簡單來說，ACP 就是一套標準規範，讓各種 AI 程式設計 Agent 能夠統一接入不同的 IDE，不管是 Claude Code 還是 Gemini CLI，只要支援 ACP 協議，就能在 JetBrains IDE 裡一鍵安裝使用。

![](https://pic.yupi.icu/1/01_ACP%E5%8D%8F%E8%AE%AE%E7%BB%9F%E4%B8%80%E8%BF%9E%E6%8E%A5AI_Agent%E5%92%8CIDE_compressed_v2.png)

他們還配套上線了一個 ACP Agent Registry，目前已經有 40 多個 AI Agent 可以一鍵安裝。

操作也很簡單，先安裝好 JetBrains 官方提供的 AI Assistant 外掛：

![](https://pic.yupi.icu/1/image-20260515125439230.png)

然後開啟 AI Chat 面板，第一次使用的話你可以免費試用：

![](https://pic.yupi.icu/1/image-20260515125540920.png)

或者點選「Add ACP Agents」自主新增智慧體，點選後就能看到 Claude Agent、Gemini CLI、Codex、Cursor、GitHub Copilot、Cline 等一堆 Agent，選擇你需要的，點選安裝就行了。

![](https://pic.yupi.icu/1/image-20260515125748615.png)

透過自主選擇 Agent，不需要 JetBrains AI 訂閱，裝完就能用，美滋滋~

![](https://pic.yupi.icu/1/image-20260515130149064.png)

另外提一下，Claude Code 在 JetBrains 裡還有一個 [專屬外掛](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-) 叫 `Claude Code [Beta]`，比直接在終端跑多了幾個功能，比如在 IDE 裡直接看 diff 預覽、自動把你選中的程式碼發給 Claude、自動共享 IDE 的報錯資訊等。不過目前這個外掛還是以終端為基礎的包裝，整體體驗不如 VS Code 的外掛成熟，聊勝於無吧。

![](https://pic.yupi.icu/1/image-20260515131157123.png)



## 寫在最後

以上就是在 IDEA 中接入 AI 程式設計能力的幾種方式，從終端直接執行、到安裝外掛、再到透過 ACP 協議統一接入，總有一種適合你。

學會了這些內容，你就能在不離開 IDEA 的前提下享受到 AI 程式設計帶來的效率提升。

如果你想繼續學習更多 AI 程式設計工具和實戰技巧，可以閱讀本教程程式設計工具板塊的其他文章。
