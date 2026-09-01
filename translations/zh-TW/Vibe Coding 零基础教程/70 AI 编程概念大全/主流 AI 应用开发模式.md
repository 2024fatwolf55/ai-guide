# 面試官問「AI 應用怎麼開發」，別說只會調 API！

最近有個學員跟我說，他去面試的時候，面試官問了一個問題：如果讓你開發一個 AI 應用，你會怎麼做？

他自信滿滿地回答：那還不簡單？調個 API 就行了唄。

面試官追問：就這一種方式？你確定嗎？

他直接懵了，場面一度非常尷尬。

其實這個問題很有代表性。很多同學對 AI 應用開發的認知還停留在「調 API」這個層面，覺得能發個 HTTP 請求拿到 AI 的回答就完事兒了。

但實際上，調 API 只是最基礎的一種方式。從最底層的 HTTP 請求，到官方 SDK 封裝，到功能齊全的開發框架，再到拖拽式的低程式碼平臺，還有一種鮮為人知的隱藏模式，AI 應用開發的模式已經非常豐富了。

![](https://pic.yupi.icu/1/01_%E5%B0%81%E9%9D%A2%E5%9B%BE-5%E7%A7%8DAI%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%A8%A1%E5%BC%8F%E6%A6%82%E8%A7%88_compressed_v1.png)

今天魚皮就給大家一次性講清楚，目前主流的 **5 種 AI 應用開發模式** 到底是什麼、怎麼用、各自適合什麼場景。每種模式我都會給一段簡單的程式碼示例，幫你快速理解。搞懂這些，不僅面試的時候能應對自如，用 AI 程式設計做專案的時候也能知道該往技術棧里加什麼。

![](https://pic.yupi.icu/1/%E9%B1%BC%E7%9A%AE%E7%9A%84AI%E5%AF%BC%E8%88%AA-AI%E5%B7%A5%E5%85%B7%E7%94%A8%E6%B3%95%E5%A4%A7%E5%85%A8.png)



## 一、HTTP API 直接呼叫

最原始、最直接的方式，就是透過 HTTP 請求呼叫大模型的 API 介面。

簡單來說，就是你的程式給大模型傳送一條訊息，大模型處理完之後把結果返回給你。

這就像打電話給一個專家諮詢問題。你得自己撥號碼（拼接 API 地址）、報上身份（傳入金鑰）、把問題描述清楚（構造請求體），然後等專家回答完再自己記錄下來（解析響應）。**雖然每一步都得自己來，但你對整個過程有完全的掌控。**

![](https://pic.yupi.icu/1/02_HTTP_API%E7%9B%B4%E6%8E%A5%E8%B0%83%E7%94%A8-%E6%89%93%E7%94%B5%E8%AF%9D%E7%B1%BB%E6%AF%94_compressed_v1.png)

不管你用什麼程式語言，只要能發 HTTP 請求，就能呼叫 AI 大模型。所以這是所有大模型服務商都支援的最基本的呼叫方式。

無論是國外的 OpenAI 和 Anthropic、國內的 DeepSeek 和通義千問，還是本地用 Ollama 部署的開源模型，甚至是 OpenRouter 這類一個 API Key 就能呼叫多家模型的聚合平臺，都支援透過 HTTP API 來呼叫。

目前 HTTP API 呼叫主要有兩種協議格式。

**1）OpenAI 相容格式**

這套格式最初是 OpenAI 定義的，但因為用的人多，現在已經成了各家預設遵循的標準。DeepSeek、通義千問、Kimi、Ollama 等絕大多數大模型服務商都相容這套格式。

有統一標準的好處是，你寫一套呼叫大模型的程式碼，只需要換個 API 地址和金鑰，就能無縫切換到不同廠商的模型，不用重新適配格式。

舉個例子，我用 HTTP 請求工具 curl，發一個 OpenAI 相容格式的請求，呼叫 DeepSeek 大模型：

```bash
curl https://api.deepseek.com/chat/completions \
  -H "Authorization: Bearer 你的API金鑰" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek-v4-pro",
    "messages": [
      {"role": "system", "content": "你是一個有用的助手"},
      {"role": "user", "content": "用一句話介紹什麼是AI應用開發"}
    ]
  }'
```

如果換成呼叫 OpenAI 的模型，只需要把 URL 請求地址和 model 模型名稱換一下就行，請求格式完全一樣。

**2）Anthropic Messages API 格式**

Anthropic（Claude 模型的開發商）用的是自己獨立的一套協議，請求結構和 OpenAI 不太一樣。

比如系統提示詞是放在頂層的 `system` 引數裡，而不是作為一條訊息傳入。如果你要呼叫 Claude 系列模型，就得按它的格式來。

```bash
curl https://api.anthropic.com/v1/messages \
  -H "x-api-key: 你的API金鑰" \
  -H "content-type: application/json" \
  -d '{
    "model": "claude-sonnet-4-6",
    "max_tokens": 1024,
    "system": "你是一個有用的助手",
    "messages": [
      {"role": "user", "content": "用一句話介紹什麼是AI應用開發"}
    ]
  }'
```

實際開發 AI 應用的時候，你還需要了解請求和響應中各個欄位的含義。最核心的是 `messages` 欄位，也就是你跟 AI 的對話訊息列表；此外還有 `temperature` 控制回答的隨機性、`max_tokens` 限制回答長度、響應裡的 `usage` 欄位能告訴你這次呼叫消耗了多少 Token 等等。各家平臺一般都會提供詳細的 API 文件，照著文件來就行。

![](https://pic.yupi.icu/1/image-20260511153354301.png)

大模型的 API 一般會提供兩種呼叫方式。一種是普通請求，一問一答，等 AI 生成完整個回答後一次性返回。另一種是流式請求，如果你想實現一個字一個字往外蹦的打字機效果，就需要用到 **SSE（Server-Sent Events）** 流式傳輸協議，讓服務端把生成的內容一段一段地推送給你。用法也不復雜，一般只需要在請求引數裡把 `stream` 設定為 `true` 就行了。

下面我用 Python 寫一個流式呼叫的例子，感受一下打字機效果是怎麼實現的：

```python
import requests

response = requests.post(
    "https://api.deepseek.com/chat/completions",
    headers={
        "Authorization": "Bearer 你的API金鑰",
        "Content-Type": "application/json"
    },
    json={
        "model": "deepseek-chat",
        "stream": True,  # 開啟流式輸出
        "messages": [
            {"role": "system", "content": "你是一個有用的助手"},
            {"role": "user", "content": "用一句話介紹什麼是AI應用開發"}
        ]
    },
    stream=True  # 開啟流式接收
)

# 逐行讀取服務端推送的內容
for line in response.iter_lines():
    if line:
        print(line.decode())
```



## 二、官方 SDK 呼叫

寫過上面那段程式碼的同學應該能感受到，直接用 HTTP 呼叫還是挺麻煩的。填寫 URL、設定請求頭、構造 JSON、解析響應、處理錯誤碼、流式資料逐行解析…… 這些跟你的業務邏輯壓根兒沒關係，但每一個都得自己處理。

所以各大模型廠商都提供了 **SDK（Software Development Kit 軟體開發工具包）**，幫你把這些底層細節封裝好了。

如果 HTTP API 是自己撥號打電話，那 SDK 就像裝了一個智慧通訊 APP。你只管說話，APP 幫你自動撥號、接通、錄音、整理成文字，你拿到手的直接就是現成的答案。

![](https://pic.yupi.icu/1/03_%E5%AE%98%E6%96%B9SDK%E8%B0%83%E7%94%A8-%E6%99%BA%E8%83%BD%E9%80%9A%E8%AE%AFAPP%E7%B1%BB%E6%AF%94_compressed_v2.png)

目前 OpenAI、Anthropic、Google、阿里雲百鍊、智譜等主流大模型服務商都提供了多語言的 SDK，覆蓋 Python、Java 等常用語言。

![](https://pic.yupi.icu/1/image-20260511153849051.png)

SDK 的本質就是對 HTTP 請求的封裝，所以前面提到的 OpenAI 相容格式在 SDK 層面同樣適用。比如 DeepSeek 相容 OpenAI 的協議，那你直接用 OpenAI 的 SDK，改個引數就能呼叫 DeepSeek 模型了。

比如我用 OpenAI 的 Python SDK 來呼叫 GPT 模型，程式碼如下：

```python
# 引入 OpenAI 官方 SDK
from openai import OpenAI

client = OpenAI(api_key="你的API金鑰")

completion = client.chat.completions.create(
    model="gpt-5",
    messages=[
        {"role": "system", "content": "你是一個有用的助手"},
        {"role": "user", "content": "用一句話介紹什麼是AI應用開發"}
    ]
)

print(completion.choices[0].message.content)
```

不用填寫 URL、不用設定請求頭、不用手動解析 JSON，幾行程式碼就搞定了。而且 SDK 還內建了錯誤重試、型別提示、流式處理等功能，讓開發效率更高、程式碼更簡潔、系統也更穩定。

如果你用的是 DeepSeek 模型，程式碼幾乎一模一樣，只需要改一下 base_url 請求地址和 model 模型名稱就行：

```python
client = OpenAI(
    api_key="你的DeepSeek金鑰",
    base_url="https://api.deepseek.com"
)

# 呼叫時把 model 換成 DeepSeek 的模型名
completion = client.chat.completions.create(
    model="deepseek-chat",
    messages=[...]
)
```



## 三、AI 開發框架

SDK 解決了 **怎麼方便地調模型** 的問題，但企業中的 AI 應用遠不止調一下模型那麼簡單。

你可能還需要讓 AI 記住之前聊過什麼（會話記憶）、讓 AI 先去知識庫裡查資料再回答（RAG 檢索增強生成）、讓 AI 能呼叫外部工具比如查天氣、搜網頁（工具呼叫）、透過 MCP 協議接入更多外部服務、甚至讓多個 AI 協同工作完成複雜任務……

這些能力如果每個都自己從零開始寫，工作量巨大。所以就有人在 SDK 的基礎上又封裝了一層，做成了 **AI 開發框架**。

打個比方，SDK 相當於給你提供了發動機、輪胎、方向盤這些零件，你得自己一個一個裝配；AI 開發框架相當於直接給你一輛半成品車，底盤、車架、電路都搭好了，你只需要決定外觀和內飾就能上路。

![](https://pic.yupi.icu/1/04_AI%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6-%E6%B1%BD%E8%BD%A6%E7%BB%84%E8%A3%85%E7%B1%BB%E6%AF%94_compressed_v1.png)

下面以 Python 和 Java 為例，列舉幾個主流的 AI 開發框架，之後你在 AI 程式設計時看到這些技術名詞，就不會感到陌生了。

Python 生態中，**LangChain** 是目前最主流的 AI 應用開發框架，提供了大量整合元件，涵蓋模型呼叫、RAG 知識庫、工具呼叫、MCP 整合等常用能力。

**LangGraph** 是 LangChain 團隊推出的進階框架，用圖的結構來編排複雜的 AI 工作流，適合構建有狀態的、需要迴圈和分支邏輯的 AI 智慧體。

舉個例子，用 LangChain 呼叫模型的程式碼長這樣：

```python
from langchain.chat_models import init_chat_model
from langchain.messages import HumanMessage, SystemMessage

model = init_chat_model("gpt-5")

messages = [
    SystemMessage("你是一個有用的助手"),
    HumanMessage("用一句話介紹什麼是AI應用開發")
]

response = model.invoke(messages)
print(response.content)
```

看起來和 SDK 差不多對吧？

但 LangChain 的價值在於，當你需要加上記憶、工具呼叫這些高階能力時，只需要幾行配置就能搞定，不用自己從零實現。

比如建立一個帶工具呼叫能力的 AI Agent：

```python
from langchain.agents import create_agent
from langchain.tools import tool

# 定義一個工具，讓 AI 能查天氣
@tool
def get_weather(city: str) -> str:
    """查詢指定城市的天氣"""
    return f"{city}今天晴，25°C"

# 一行程式碼建立帶工具呼叫能力的 Agent
agent = create_agent(model="gpt-4o", tools=[get_weather])

# 呼叫 Agent，它會自動判斷是否需要呼叫工具
result = agent.invoke(
    {"messages": [{"role": "user", "content": "北京今天天氣怎麼樣？"}]}
)
```

這樣 AI 就能主動呼叫工具去查天氣了，你只需要定義好工具函式，LangChain 幫你搞定剩下的。

而且很多其他語言生態的 AI 開發框架，在設計上幾乎都參考了 LangChain 的思路，比如 Java 的 LangChain4j、Go 的 LangChainGo，功能上和 Python 版基本對齊，學會一個版本切到其他語言也很容易上手。

Java 生態還有 Spring 官方推出的 Spring AI 以及阿里的 Spring AI Alibaba，深度融入 Spring Boot 生態，適合 Java 後端開發者快速上手。

![](https://pic.yupi.icu/1/image-20260511154445018.png)

另外我覺得 **Vercel AI SDK** 也值得大家關注，它是 TypeScript 生態的 AI 開發框架，提供了 20 多個模型供應商的統一介面，特別適合前端和全棧開發者。



## 四、低程式碼 AI 開發平臺

框架雖然功能強大，但寫程式碼終歸是有門檻的。特別是業務人員或者不太會程式設計的同學，光是搭個開發環境就夠頭疼的了。

這時 **低程式碼 AI 開發平臺** 就派上用場了，不用寫程式碼也能搭出 AI 應用。

打個比方，低程式碼平臺就像搭積木。大模型是一塊積木，知識庫是一塊積木，工具呼叫是一塊積木，每塊積木都是現成的，你只需要決定怎麼拼接、拼成什麼形狀就好了。

![](https://pic.yupi.icu/1/05_%E4%BD%8E%E4%BB%A3%E7%A0%81%E5%B9%B3%E5%8F%B0-%E6%90%AD%E7%A7%AF%E6%9C%A8%E7%B1%BB%E6%AF%94_compressed_v1.png)

Dify 是典型的低程式碼 AI 開發平臺，它支援透過視覺化介面搭建 AI 聊天助手、工作流、知識庫問答等應用，還能一鍵接入各種大模型。

它最大的優勢是開源、可私有化部署，企業想把資料放在自己伺服器上也沒問題。

![](https://pic.yupi.icu/1/1743564064922-03f6365b-a712-47d9-be55-4867b848a269.png)

在 Dify 上搭一個 AI 聊天助手，大概就這麼幾步：

1. 選擇一個大模型（比如 GPT-5.5 或 DeepSeek）
2. 寫一段系統提示詞，告訴 AI 它的角色
3. 配置知識庫（可選），上傳你的文件資料
4. 點選發布，就能得到一個可呼叫的 API 或者直接分享的聊天連結

整個過程不需要寫一行程式碼。

類似的平臺還有不少，比如位元組跳動的 Coze（釦子）也支援視覺化搭建 AI 應用，容易上手；阿里雲百鍊是一站式的大模型應用構建平臺，整合了模型呼叫、智慧體編排、知識庫管理等能力；還有開源的工作流自動化平臺 n8n，擅長做跨系統的 AI 自動化流程。



## 五、AI 程式設計工具的 SDK

前面 4 種模式覆蓋了從手動寫程式碼、到完全不寫程式碼的各種方案。但還有一種很多同學不知道的模式。。。

2026 年，Cursor、Claude Code、GitHub Copilot 等 AI 程式設計工具紛紛推出了自己的 SDK。你可以在自己的程式碼裡直接呼叫這些 AI 程式設計工具的 Agent，它們能幫你讀程式碼、改程式碼、跑命令，而且你在 AI 程式設計工具裡配置好的 MCP 服務、Skills、專案規則這些能力，透過 SDK 呼叫時同樣能生效。

如果說前面那些方式都是你自己動手幹活，那麼使用 AI 程式設計工具的 SDK 相當於你僱了一個會寫程式碼的 AI 程式設計師。你只需要告訴它做什麼，它會自動讀檔案、分析程式碼、完成開發。

![](https://pic.yupi.icu/1/06_AI%E7%BC%96%E7%A8%8B%E5%B7%A5%E5%85%B7SDK-%E9%9B%87%E4%BD%A3AI%E7%A8%8B%E5%BA%8F%E5%91%98%E7%B1%BB%E6%AF%94_compressed_v3.png)

以 Cursor SDK 為例，允許你在 TypeScript / Node.js 程式碼中直接呼叫 Cursor 的 AI Agent。

先新建專案資料夾，然後開啟終端，在該目錄下輸入一行命令安裝 SDK：

```bash
npm install @cursor/sdk
```

![](https://pic.yupi.icu/1/image-20260511141833488.png)

然後登入 [Cursor Dashboard](https://cursor.com/dashboard/integrations)，在 Integrations 頁面生成一個 API Key 並儲存下來，後面程式碼裡需要用它來驗證身份。

![](https://pic.yupi.icu/1/image-20260511141405454.png)

假設我本地有一個「創作選題獲取器」專案，裡面用 AGENTS.md 定義了選題獲取的工作流規則，還安裝了 frontend-design 前端設計技能。

![](https://pic.yupi.icu/1/image-20260511154340593.png)

現在我想讓 AI 幫我獲取今天的熱門選題，並生成一個漂亮的網頁報告。

新建一個 JavaScript 檔案，比如 `main.js`，寫入以下程式碼：

```javascript
import { Agent } from "@cursor/sdk";

// 建立 AI Agent，指向「創作選題獲取器」專案
const agent = await Agent.create({
  apiKey: '你的 API Key',
  model: { id: "gpt-5.5" },
  local: { cwd: "/Users/yupi/workflow/創作選題獲取器" },
});

// 一句話下達指令
const run = await agent.send("幫我獲取今日 AI 領域的熱門選題，並生成一個網頁報告");

// 收集所有事件，列印到終端的同時儲存到檔案
const events = [];
for await (const event of run.stream()) {
  console.log(event);
  events.push(event);
}

// 把完整的事件記錄儲存為 JSON 檔案，方便事後分析
const fs = await import("fs");
fs.writeFileSync("agent-output.json", JSON.stringify(events, null, 2));
```
然後在終端執行：

```bash
node main.js
```

執行後你會在終端看到一連串事件輸出，比如 Agent 開始執行。

![](https://pic.yupi.icu/1/image-20260511151359126.png)

從日誌裡可以清晰地看到 Agent 的整個執行過程：它先用 `glob` 工具掃描了專案目錄，然後用 `read` 工具依次讀取了 AGENTS.md 工作流規則和 frontend-design 的 SKILL.md 技能說明，接著透過 `shell` 工具呼叫了專案裡的熱點獲取指令碼進行聯網搜尋，從 GitHub、Hacker News 等 6 個平臺採集了 70 條熱門話題，再透過 `edit` 命令生成了一個近千行程式碼的 HTML 網頁報告。

![](https://pic.yupi.icu/1/image-20260511151132128.png)

最後 Agent 還自動開啟了瀏覽器，讓你直接檢視生成的選題報告。

![](https://pic.yupi.icu/1/image-20260511150909122.png)

你會發現，整個過程和在 Cursor 編輯器裡跟 AI 對話一模一樣。但區別在於，現在你是用程式碼來呼叫它的，這意味著你可以把它嵌入到 CI/CD 流水線、自動化指令碼、甚至自己的產品裡。普通的大模型 SDK 只能幫你生成文字，而 AI 程式設計工具的 SDK 能幫你直接操作程式碼庫、呼叫工具、生成檔案。

如果只是一次性的簡單任務，還有更簡潔的寫法：

```typescript
const result = await Agent.prompt(
  "給這個專案寫一個 README.md",
  {
    apiKey: process.env.CURSOR_API_KEY!,
    model: { id: "composer-2" },
    local: { cwd: process.cwd() },
  }
);
```

前面演示的是本地執行模式，Agent 直接在你自己的電腦上跑，適合開發除錯。除此之外，Cursor SDK 還支援 Cursor 託管雲模式，Cursor 幫你在雲端開一臺隔離的虛擬機器來執行任務，適合同時跑多個 Agent 並行處理；以及自託管雲模式，你自己管理伺服器，適合企業內部使用。

有了 AI 程式設計工具的 SDK 後，你甚至可以把 AI 程式設計工具當成一種開發環境，就像部署專案需要配置資料庫一樣，在伺服器上配好 AI 程式設計工具的環境，然後在程式碼中透過 SDK 來呼叫，實現自動化的程式碼生成、審查、重構等任務。

除了 Cursor，Anthropic 的 Claude Agent SDK 和 GitHub 的 Copilot SDK 也提供了類似的能力，用法大同小異。



## 怎麼選擇？

講完了 5 種 AI 應用開發模式，那實際開發的時候到底該選哪種呢？

這裡我幫大家做了一個簡單的對比：

| 模式 | 一句話總結 | 適合誰 |
|------|-----------|--------|
| HTTP API | 自己拼請求調模型，最底層最靈活 | 想了解底層原理、或 SDK 不支援的語言 |
| 官方 SDK | 用官方封裝好的工具包調模型 | 大多數開發者的日常開發 |
| AI 開發框架 | 記憶、RAG、工具呼叫等能力開箱即用 | 需要開發完整 AI 應用的團隊 |
| 低程式碼平臺 | 拖拽搭建，不用寫程式碼 | 非技術人員、快速驗證想法 |
| AI 程式設計工具 SDK | 讓 AI Agent 幫你寫程式碼 | 想把 AI 程式設計能力整合到自動化流程中 |

注意，這 5 種模式之間並不是互相排斥的，實際開發中經常會混著用。比如用低程式碼平臺快速搭個原型驗證想法，驗證透過後再用開發框架重寫成正式版本；或者在框架搭好的專案裡，某些模組直接用 HTTP API 調一個特殊介面。

**選擇的核心原則是：用最少的成本解決當前的問題。** 能拖拽解決的，就別寫程式碼；能用框架搞定的，就別自己造輪子；能用 SDK 的，就別手擼 HTTP。

![](https://pic.yupi.icu/1/07_5%E7%A7%8D%E6%A8%A1%E5%BC%8F%E5%AF%B9%E6%AF%94%E6%80%BB%E7%BB%93-%E9%87%91%E5%AD%97%E5%A1%94%E5%9B%BE_compressed_v1.png)

不過如果你是在學習階段，我建議反過來，從 HTTP API 開始，一步步往上走。這樣對每一層的原理都能有清晰的理解，後面用更高層的工具也不會一頭霧水。



## 寫在最後

AI 應用開發這個領域變化太快了，新框架、新工具幾乎每個月都在冒出來。

但萬變不離其宗，底層就是這幾種模式。搞懂了這些，不管未來出什麼新工具，你都能快速定位它屬於哪一層、解決什麼問題。

回到開頭那個面試場景，如果你能把這 5 種模式的適用場景和優劣講清楚，面試官大機率會對你刮目相看。

想做 AI 實戰專案的話，[程式設計導航](https://www.codefather.cn/) 上有多套 AI 專案教程，手把手帶你從 0 到 1 做出完整的 AI 應用，加油！
