# Claude Code 和 Codex 對接國內模型教程

很多人想學 AI 程式設計，想耍一耍目前最流行的 Claude Code 和 Codex 程式設計工具，結果一上手就卡在了第一步。

要麼沒有國外的訂閱賬號，登入都登入不上；要麼好不容易開通了，發現官方額度死貴，對話一會兒額度就耗光了；再加上時不時還有封號的風險，整的提心吊膽。

咱們怎麼能因為「用不了工具」這種事，就把學 AI 程式設計的勁頭給澆滅了呢！

其實 Claude Code 和 Codex 都支援切換模型，咱們用國內的大模型（比如 DeepSeek、Qwen、智譜 GLM）來驅動它們就行，量大管飽，不用魔法，也不怕封號。

這篇文章我就手把手教你把國內模型接到 Claude Code 和 Codex 裡。我會以 DeepSeek 為例，看完你就能跑通整套流程，想換哪家模型都是一樣的操作。

點個收藏，咱們開始~



## 為什麼推薦 DeepSeek

在動手之前，先說說為什麼我拿 DeepSeek 來舉例。

DeepSeek-V4-Flash 這個模型主打價效比，輸入 1 元 / 百萬 token、輸出 2 元 / 百萬 token，大概只有 V4-Pro 十分之一的價格。

![](https://pic.yupi.icu/1/image-20260803152949072.png)

重點是它在 Agent 能力上做了大幅強化，在專門測試 AI 自主執行終端任務的 Terminal-Bench 上拿到了 82.7 分，竟然反超了自家的 V4-Pro 預覽版（72.1 分），寫程式碼、調工具、自主執行任務都很能打。

![](https://pic.yupi.icu/1/HOiZba2aYAAozFz.jpeg)

Agent 能力強、價格又便宜，用來驅動 Claude Code 和 Codex 學習 AI 程式設計，價效比是最高的。

**而且更香的是，它原生支援了 Responses API，可以直接接入 Codex，不需要任何協議轉換。** 這一點後面配置的時候你會體會到有多省事。

當然，如果你已經買了其他平臺的套餐，比如智譜 GLM、Qwen、Kimi、MiniMax，操作思路完全一樣，把 Base URL 和 API Key 換成對應平臺的就行。



## CC Switch 是什麼

Claude Code、Codex 這些命令列工具，每一個的配置格式都不一樣。如果你想給它們換個模型供應商，得自己去翻文件，手動編輯 JSON、TOML 或者 `.env` 檔案，填一堆 Base URL、API Key、模型名之類的引數。說不定改錯一個字元就跑不起來，想在幾個模型之間來回切換就更麻煩了。。。

CC Switch 就是來解決這個痛點的。它是一個免費開源的跨平臺桌面工具，用一個視覺化介面統一管理 Claude Code、Codex、Gemini CLI、OpenCode 等多個 AI 程式設計工具的配置。

> 開源指路：[https://github.com/farion1231/cc-switch](https://github.com/farion1231/cc-switch)

![](https://pic.yupi.icu/1/1780312934749-a570e124-074c-40fe-924b-5f9719e45e56.png)

CC Switch 內建了 50 多個供應商預設，DeepSeek、Qwen、Kimi、智譜 GLM、MiniMax 這些都有，你不用自己手動改配置檔案，點幾下就能一鍵切換模型，還能從系統托盤裡快速切換。

![](https://pic.yupi.icu/1/image-20260601193909067.png)

下面我就用它來帶大家實操一遍。



## 安裝 CC Switch

到 [CC Switch 官網](https://ccswitch.io) 或者 [GitHub Releases 頁面](https://github.com/farion1231/cc-switch/releases/latest)，根據你的作業系統選擇對應的安裝方式。

![](https://pic.yupi.icu/1/1780310254037-fb0cd631-17e9-45cf-b1c2-963d18cbf99d.png)

Mac 使用者推薦直接用 Homebrew 一行命令安裝，裝完直接就能用：

```bash
brew install --cask cc-switch
```

![](https://pic.yupi.icu/1/1780310254160-ed387f10-f656-429f-a41d-8e288b8e3be2.png)

Windows 使用者從 Releases 頁面下載 `.msi` 安裝包，雙擊執行即可；Linux 使用者根據發行版選擇 `.deb`、`.rpm` 或 `.AppImage`。

安裝完成後啟動 CC Switch，主介面會出現在桌面或者系統托盤裡。

下面我們就分別給 Claude Code 和 Codex 接上 DeepSeek 了。不過在那之前，得先把 DeepSeek 的 API Key 準備好。



## 準備大模型 API Key

不管接哪個工具，都得先有一個 DeepSeek 的 API Key。

到 [DeepSeek 開放平臺](https://platform.deepseek.com) 註冊登入，進入 API keys 頁面，點選建立一個新的 key。

![](https://pic.yupi.icu/1/image-20260601194058029.png)

注意，key 只會在建立時完整顯示這一次，記得當場複製儲存好，後面在 CC Switch 裡要用到它。



## 把 DeepSeek 接入 Claude Code

我們先從簡單的 Claude Code 開始。



### 先裝好 Claude Code

簡單介紹一下 Claude Code。它是 Anthropic 推出的 AI 程式設計工具，直接在終端裡執行，你跟它聊天描述需求，它就能自主分析專案、寫程式碼、跑命令、修 Bug，全程自主執行。

![](https://pic.yupi.icu/1/1780310254072-69c9a86c-ede2-40e7-807c-13684461d4c2.png)

安裝 Claude Code 很簡單，先確保電腦裡有 Node.js 環境，沒有的話去 [Node 官網](https://nodejs.org/en/download) 下個傻瓜式安裝包。然後一行命令搞定：

```bash
npm install -g @anthropic-ai/claude-code
```

裝好後在終端輸入 `claude` 就能進入對話介面，首次使用需要登入。但很多同學沒有 Anthropic 的官方賬號，登入這步就卡住了，根本沒法直接用。

別急，下面就用 CC Switch 把它切換成 DeepSeek。



### 用 CC Switch 切換模型

開啟 CC Switch，在頂部應用欄選擇 **Claude**，然後點選「新增供應商」：

![](https://pic.yupi.icu/1/1780310658228-ffa4ff69-342c-4244-82e3-2204dad61e97.png)

在預設的模型供應商列表裡選擇 **DeepSeek**：

![](https://pic.yupi.icu/1/1780310679329-e280982b-da09-4f4e-8861-d943f39f17ed.png)

接下來填寫剛才在 DeepSeek 開放平臺建立好的 API Key：

![](https://pic.yupi.icu/1/1780310750547-43515207-6f23-45b7-a62f-56370070da4f.png)

其餘欄位基本不用動，CC Switch 的 DeepSeek 預設已經幫你把模型都配好了，裡面內建了 DeepSeek-V4-Pro 和 DeepSeek-V4-Flash 兩個版本。主模型預設是 Pro（對應 Claude Code 裡的 Opus 位），小模型是 Flash（對應 Haiku 位）。

如果你想省錢又夠用，直接全部用 V4-Flash 也完全沒問題，它的 Agent 能力已經很強了。

如果你想用上 DeepSeek V4 的百萬 tokens 超長上下文，還能在這裡直接勾選開啟 1M 模式，告訴 Claude Code 這個模型能吃下這麼長的上下文，不用自己去改配置。

![](https://pic.yupi.icu/1/1780310818585-ecfe1960-f1cd-4a31-a1e7-f1da199c17d9.png)

填完點右下角的「新增」按鈕。這裡能看到 Claude Code 的 JSON 配置檔案，CC Switch 乾的活兒就是幫你視覺化地修改它，省去手動編輯的麻煩。

![](https://pic.yupi.icu/1/1780310894533-0153954b-e19f-4e96-93a5-de8208e08c01.png)

最後點選啟用 DeepSeek 模型：

![](https://pic.yupi.icu/1/1780310914775-338bbb35-872d-46ad-9cbf-5731341a3942.png)

重新進入 Claude Code，左上角能看到當前用的模型。我們讓它自報家門，輸入一句：你是什麼模型？

AI 能正常給出回覆，就說明切換成功了：

![](https://pic.yupi.icu/1/1780311048597-711eca09-fe5c-4d0a-bb01-7c9bbfcb033c.png)

你可能會發現，用 CC Switch 給 Claude Code 接 DeepSeek，整套流程格外簡單。這是因為 DeepSeek 提供了相容 Anthropic 協議的介面，而 Claude Code 本身就是按這個協議來通訊的，CC Switch 直接把配置寫進 `settings.json` 就能用了。



## 把 DeepSeek 接入 Codex

搞定 Claude Code，我們再來看 Codex。它是 OpenAI 推出的 AI 程式設計工具，最近的熱度堪稱炸裂，經常贈送重置額度，使勁蹬都蹬不完。

![](https://pic.yupi.icu/1/1780311345253-521a8636-47ec-4d53-bb1a-e350748e2085-20260601194352039.png)

Codex 有兩種形態，一種是在終端裡跑的命令列版 Codex CLI，一種是帶圖形介面的桌面 APP。

命令列版的安裝方式跟 Claude Code 類似，一行命令就能搞定：

```bash
npm install -g @openai/codex
```

裝好後在終端輸入 `codex` 就能進入對話介面，首次使用同樣需要登入 OpenAI 賬號。沒有賬號的話，就要自己折騰一下切換個模型。

![](https://pic.yupi.icu/1/1780311431037-8b655299-d1f1-4ff5-a845-988c0980c4ca.png)

至於 Codex 桌面 APP 的安裝和基礎玩法，前段時間我剛出過一套《保姆級的影片 + 圖文教程》，需要的同學直接到我的 [魚皮 AI 導航](https://ai.codefather.cn/library/2058749249474023425) 自取：

![](https://pic.yupi.icu/1/image-20260601194545597.png)

給 Codex 接 DeepSeek 有 3 種方法，我按推薦程度依次介紹。



### 方法 1、官方一鍵指令碼（推薦）

DeepSeek 官方提供了一個配置指令碼，跑一下就能全部搞定。

在執行之前，確保你已經安裝了 Codex CLI 或者 ChatGPT 桌面 APP，並且至少啟動過一次，讓它生成好 `~/.codex` 配置目錄，指令碼要往裡面寫東西。

> 官方文件參考：[https://api-docs.deepseek.com/quick_start/agent_integrations/codex/](https://api-docs.deepseek.com/quick_start/agent_integrations/codex/)

Windows 使用者在 PowerShell 執行：

```powershell
irm https://cdn.deepseek.com/api-docs/codex-deepseek-setup-en.ps1 | iex
```

Mac 或 Linux 使用者在終端執行：

```bash
bash <(curl -fsSL https://cdn.deepseek.com/api-docs/codex-deepseek-setup.sh)
```

指令碼啟動後會讓你選擇要用的模型，目前 DeepSeek-V4-Flash 已經可以直接選了，輸入「1」就好：

![](https://pic.yupi.icu/1/image-20260803114529569.png)

首次執行時，它還會讓你輸入 API Key：

![](https://pic.yupi.icu/1/image-20260803114842807.png)

然後按回車鍵執行，唰唰唰，指令碼就幫我們把 DeepSeek 接入到 Codex 中了。

![](https://pic.yupi.icu/1/image-20260803114928055.png)

多說幾句，這個指令碼會自動完成下面幾件事：

1. 把你現有的 Codex 配置備份到 `~/.codex/backup-deepseek/` 目錄，隨時可以恢復
2. 生成一個 `~/.codex/models.json` 檔案，告訴 Codex 關於 DeepSeek 模型的後設資料（上下文視窗大小、支援的推理等級等等）
3. 修改 `~/.codex/config.toml`，寫入 DeepSeek 的介面配置，你之前設定的 MCP 伺服器和專案配置都會保留
4. 自動校驗配置語法，如果有錯就中止，不會損壞你的檔案

配置完成後，重新開啟 Codex，啟動橫幅如果顯示 `deepseek-v4-flash`，就說明配好了：

![](https://pic.yupi.icu/1/image-20260803120531949.png)

如果你用的是 ChatGPT 桌面 APP 或者 Codex 的 VS Code 外掛，不用單獨配置，直接開啟就能用 DeepSeek 模型了，因為它們和 CLI 版共用同一套配置檔案。

![](https://pic.yupi.icu/1/image-20260803141956962.png)

想切換回官方模型的話，重新跑一遍指令碼，在選單裡選恢復選項就行。

![](https://pic.yupi.icu/1/image-20260803115518337.png)



### 方法 2、手動編輯配置檔案

如果你不想跑指令碼，也可以自己手動修改配置檔案，兩步就能搞定。

第一步，在電腦的使用者目錄下找到 `.codex` 資料夾（Mac / Linux 路徑是 `~/.codex/`，Windows 是 `%USERPROFILE%\.codex\`），建立一個 `models.json` 檔案，檔案中的內容可以到 [DeepSeek 官方文件](https://api-docs.deepseek.com/zh-cn/quick_start/agent_integrations/codex/) 複製。

![](https://pic.yupi.icu/1/image-20260803113859064.png)

這個檔案的作用是告訴 Codex 關於 DeepSeek 模型的各種引數資訊，比如支援 100 萬 token 的上下文視窗、支援 low / high / max 三檔推理深度等。

第二步，在同一個目錄下編輯 `config.toml` 檔案，新增下面這段配置：

```toml
model = "deepseek-v4-flash"
model_provider = "deepseek"
preferred_auth_method = "apikey"
forced_login_method = "api"
model_reasoning_effort = "high"
model_catalog_json = "~/.codex/models.json"

[model_providers.deepseek]
name = "deepseek"
base_url = "https://api.deepseek.com/"
wire_api = "responses"
experimental_bearer_token = "<你的 DeepSeek API Key>"
```

把其中的 `experimental_bearer_token` 換成你自己的 API Key 就行。

這裡的關鍵是 `wire_api = "responses"`，它告訴 Codex 用 Responses API 協議跟 DeepSeek 通訊，而 DeepSeek-V4-Flash 原生就支援這個協議，所以能直接跑通。

儲存檔案後重新開啟 Codex，就能用 DeepSeek-V4-Flash 了。



### 方法 3、用 CC Switch 做協議轉換

前面兩種方法之所以這麼省事，全靠 DeepSeek 官方做了原生適配。但如果你想接的是智譜 GLM、Kimi、MiniMax 這些還不支援 Responses API 的模型，只改 `base_url` 大機率會翻車，直接給你報一個 404 錯誤。

問題出在協議上。Codex 用的是 OpenAI 的 **Responses API**，而大多數國內模型走的是 **Chat Completions API**，這倆壓根兒不是一套東西。就好比你打電話，號碼是撥通了，可你說中文、對方只懂法語，照樣聊不到一塊兒去。

![](https://pic.yupi.icu/1/01_%E7%94%B5%E8%AF%9D%E6%AF%94%E5%96%BB-%E5%8D%8F%E8%AE%AE%E6%A0%BC%E5%BC%8F%E4%B8%8D%E9%80%9A_compressed_v2.png)

所以這種情況下，關鍵在於中間得有個「翻譯」，把 Codex 發出的請求轉換成模型能聽懂的格式。

好在 CC Switch 已經把這件事給我們辦妥了。它的「本地路由」功能會在你電腦上起一個輕量級的代理服務，請求的流轉過程是這樣的：

```plain
Codex → CC Switch → 大模型 → CC Switch → Codex
```

整個轉發對 Codex 完全透明，它自己還以為在訪問 OpenAI 官方介面呢。這樣既保留了 Codex 的原汁原味體驗，又能用上便宜的國內模型，豈不美哉？

![](https://pic.yupi.icu/1/02_CC_Switch%E6%9C%AC%E5%9C%B0%E8%B7%AF%E7%94%B1%E5%8D%8F%E8%AE%AE%E8%BD%AC%E6%8D%A2%E6%B5%81%E7%A8%8B_compressed_v3.png)

下面還是用 DeepSeek 來演示這個流程（截圖現成），你換成其他供應商的操作步驟完全一樣。



#### 1、在 CC Switch 裡新增供應商

開啟 CC Switch，在頂部應用欄切換到 **Codex**，點選「新增供應商」：

![](https://pic.yupi.icu/1/1780311605982-1c994d40-c7f4-48df-817c-bed2b6c31fab.png)

在預設裡搜尋並選擇 **DeepSeek**，跟前面給 Claude Code 配置時的步驟一樣：

![](https://pic.yupi.icu/1/1780311659008-be813d0f-d761-435f-a7cb-a74899214864.png)

填入你的 DeepSeek API Key，其餘欄位保持預設：

![](https://pic.yupi.icu/1/1780311678381-5d244f5c-6943-43ba-a6c3-a2a29960d907.png)

跟 Claude Code 一樣，模型這些 CC Switch 都已經預設好了，其他欄位不用動。

要特別注意的是，這一步的關鍵是得 **開啟「本地路由對映」**，然後點右下角的「新增」按鈕儲存就好。

![](https://pic.yupi.icu/1/1780311713574-2317e9a2-ece4-4c4d-a188-4d6735402c6a.png)

回到主頁後，選擇啟用 DeepSeek：

![](https://pic.yupi.icu/1/1780311910051-908552fe-d168-4df1-9a08-3c9e6f1e4d0d.png)

但是到目前為止，我們還不能在 Codex 中正常使用 DeepSeek，對話會直接報前面說的 404 錯誤：

![](https://pic.yupi.icu/1/1780311879234-642050c1-2333-4d8e-866d-1abc9197d7dd.png)



#### 2、開啟本地路由

切換到 DeepSeek 後，系統會提示你開啟路由。點選左上角的「設定」按鈕進入設定頁面：

![](https://pic.yupi.icu/1/1780311968017-bf4e43f6-736e-4ba7-9ce9-5a9ca2763910.png)

找到路由設定選單，把本地路由的「路由總開關」開啟，然後選擇啟用 Codex 路由：

![](https://pic.yupi.icu/1/1780312030888-cdfafb55-0a3f-4fd7-bdc5-785eb3cd9bc8.png)

這一步就是讓 CC Switch 的本地代理正式接管 Codex 的請求，前面說的協議轉換全靠它。

大功告成！

重新開啟 Codex CLI，就能看到已經切換為 DeepSeek 模型了。同樣讓它自報家門，能正常對話就說明切換成功了：

![](https://pic.yupi.icu/1/1780312108872-2c760023-290a-4e7a-b8d0-be36159900da.png)

你會發現，AI 嘴上還說自己是基於 GPT-5 的 Codex。這是因為 Codex 會給模型注入一套自己的系統提示詞，讓它預設以為自己是官方模型，但實際幹活的底層已經換成 DeepSeek 了。

再來試試 Codex 桌面 APP。因為它和命令列版共用 `~/.codex` 這套配置，CC Switch 切換之後直接開啟就能用，同樣問它是什麼模型，底層跑的也是 DeepSeek：

![](https://pic.yupi.icu/1/1780312248394-f117f7bb-1372-4a73-91e7-2b6c171cef6f.png)

如果想改回來，反向操作即可，把路由關掉、再啟用預設配置就行：

![](https://pic.yupi.icu/1/1780312343473-b43668a4-cb80-4f60-8fce-e7aa93e7753e.png)

怎麼樣，是不是比想象中簡單多了？

換成其他供應商也是這套流程，在 CC Switch 裡選對應的預設（沒有預設就自定義一個），把人家給你的專屬 Base URL 和 API Key 填進去，別忘了開啟本地路由。



## 給純文字模型加上看圖能力

配置完成之後，還有一個坑要提醒你。

DeepSeek-V4-Flash 雖然 Agent 能力很強，但它是純文字模型，不能理解圖片。如果你在 Codex 或 Claude Code 中讓它分析一張截圖、看一下 UI 介面長什麼樣，它是做不到的。

不過這個問題也有現成的解決方案，就是給你的 AI 程式設計工具裝一個 **Vision Skill**，用另一個多模態視覺模型來幫它看圖。

比如這個通用的 [多模態視覺識別 Skill](https://github.com/asuojun/claude-vision-skill)，專門就是為 DeepSeek 這類沒有視覺能力的模型設計的。而且由於 Skill 是通用標準，Codex 和 Claude Code 等各種 AI 程式設計工具都能安裝使用。

你需要先準備一個支援圖片理解的視覺模型，比如通義千問的 Qwen3.8-Max，並且到對應的大模型平臺獲取到 API Key。

![](https://pic.yupi.icu/1/image-20260803154236012.png)

然後直接在 AI 程式設計工具中發一段提示詞，讓 AI 幫你完成 Skill 的安裝和配置：

```plain
全域性安裝 Vision Skill（https://github.com/asuojun/claude-vision-skill），按照 README 的說明進行配置。
- 視覺模型用通義千問的 qwen3.8-max
- API Key 為 <改為你自己的 API Key>
```

![](https://pic.yupi.icu/1/image-20260803155552049.png)

安裝好之後，當 AI 遇到需要看圖的任務時，Vision Skill 就會自動把圖片發給視覺模型，讓它把圖片內容轉成文字描述，再交給 DeepSeek 繼續推理。

![](https://pic.yupi.icu/1/image-20260803155836402.png)

如果你平時寫程式碼不怎麼需要 AI 看圖，這一步可以先跳過，等用到的時候再裝也來得及。想深入瞭解 Skills 的用法，可以閱讀本教程程式設計工具板塊「工具實戰」目錄中的《Agent Skills：通用 AI 技能庫》。



## 寫在最後

這篇文章手把手帶大家把國內大模型（以 DeepSeek 為例）接入了 Claude Code 和 Codex。

給 Codex 接 DeepSeek 首選官方一鍵指令碼，因為 DeepSeek 原生支援了 Responses API，不需要任何協議轉換；如果要接的模型不支援這個協議，就用 CC Switch 的本地路由來做轉換。給 Claude Code 接模型更簡單，因為國內主流模型基本都提供了相容 Anthropic 協議的介面，用 CC Switch 點幾下就好。

看到這裡你會發現，現在學 AI 程式設計的門檻真的低到不能再低了。百萬 token 上下文、Agent 能力拉滿、價格還便宜到離譜，成本可能只是官方訂閱的零頭。

**工具和模型，都不該成為你學習路上的攔路虎。**

所以別再用「我沒賬號、用不起」當藉口了，配好環境，趕緊上手把工具用起來才是。至於該選哪個模型來幹哪種活，可以閱讀本教程程式設計工具板塊中的《AI 模型選擇指南》；如果你想搞清楚 Claude Code 為什麼會封號、有哪些替代方案，可以閱讀本目錄中的《Claude Code 封號機制和應對方案》。
