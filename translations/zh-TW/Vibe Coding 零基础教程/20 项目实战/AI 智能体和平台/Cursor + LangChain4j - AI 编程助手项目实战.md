# Cursor + LangChain4j - AI 程式設計助手專案實戰

這是一套完整的全棧 AI 程式設計助手專案教程。本專案採用人工編碼 + Vibe Coding 結合的方式開發，透過寫 Java 程式碼來呼叫 AI、使用 Cursor 等 AI 工具輔助編碼。重點在於學習如何在 Java 專案中整合 AI 能力，帶你係統學習 LangChain4j 框架的幾乎所有主流用法和特性。適合有一定 Java 後端開發基礎的同學，快速入門 AI 應用開發，並且在簡歷上新增 AI 專案。

預計要學習 1 ~ 5 小時。



---



大家好，我是程式設計師魚皮。現在 AI 應用開發可以說是程式設計師必備的技能了，求職時能夠大幅增加競爭力。之前我用 Spring AI 帶大家做過一個 [開源的 AI 超級智慧體專案](https://github.com/liyupi/yu-ai-agent)，這次我來帶大家快速掌握另一個主流的 Java AI 應用開發框架 LangChain4j。

這個教程也是我精心設計，拒絕枯燥的理論，而是用一個程式設計小助手專案帶大家在實戰中依次學習 LangChain 幾乎所有主流的用法和特性。看完這個教程，你不僅學會了 LangChain，還直接多了一段專案經歷，豈不美哉？

**文章近一萬字，有點長，建議收藏，觀看影片版體驗更佳~**

> 完整影片教程：https://bilibili.com/video/BV1X4GGziEyr
>
> 專案程式碼開源：https://github.com/liyupi/ai-code-helper



## 需求分析

我們要實現一個 AI 程式設計小助手，可以幫助使用者答疑解惑，並且給出程式設計學習的指導建議，比如：

- 程式設計學習路線
- 專案學習建議
- 程式設計師求職指南
- 程式設計師常見面試題



![](https://pic.yupi.icu/1/1752027043776-cd6d17ed-175f-4c7e-8b25-aee81a5296b2-20250710114302208.png)



要實現這個需求，我們首先要能夠呼叫 AI 完成 **基礎對話**，而且要支援實現 **多輪對話記憶**。此外，如果想進一步增強 AI 的能力，需要讓它能夠 **使用工具** 來聯網搜尋內容；還可以讓 AI 基於我們自己的 **知識庫回答**，給使用者提供我們在程式設計領域沉澱的資源和經驗。

![](https://pic.yupi.icu/1/1752028612444-351672a3-3725-4850-82b5-57d63d0ba866.png)

如果要從 0 開始實現上述功能，還是很麻煩的，因此我們要使用 AI 開發框架來提高效率。

## 什麼是 LangChain4j？

目前主流的 Java AI 開發框架有 [Spring AI](https://spring.io/projects/spring-ai) 和 [LangChain4j](https://docs.langchain4j.dev/intro)，它們都提供了很多 **開箱即用的 API** 來幫你呼叫大模型、實現 AI 開發常用的功能，比如我們今天要學的：

- 對話記憶
- 結構化輸出
- RAG 知識庫
- 工具呼叫
- MCP
- SSE 流式輸出

就我個人體驗下來，這兩個框架的很多概念和用法都是類似的，也都提供了很多外掛擴充套件，都支援和 Spring Boot 專案整合。雖然有一些編碼上的區別，但孰好孰壞，使用感受也是因人而異的。

**實際開發中應該如何選擇呢？**

我想先帶你用 LangChain4j 開發完一個專案，最後再揭曉答案，因為那個時候你自己也會有一些想法。

## AI 應用開發

### 新建專案

開啟 IDEA 開發工具，新建一個 Spring Boot 專案，**Java 版本選擇 21**（因為 LangChain4j 最低支援 17 版本）：

![](https://pic.yupi.icu/1/1751944012715-3ac04ad2-42e9-4c41-b998-a5318050e27c.png)

選擇依賴，使用 3.5.x 版本的 Spring Boot，引入 Spring MVC 和 Lombok 註解庫：

![](https://pic.yupi.icu/1/1751944035875-83da11bb-e5fa-4a19-ae57-9c214cc0f523.png)

新建專案後，先修改配置檔案字尾為 `yml`，便於後面填寫配置。

![](https://pic.yupi.icu/1/1751944110301-93054763-76d8-4686-ac6e-971e81b4acd4.png)

這裡我會建議大家建立一個 `application-local.yml` 配置檔案，將開發時用到的敏感配置寫到這裡，並且新增到 `.gitignore` 中，防止不小心開源出來。

### AI 對話 - ChatModel

ChatModel 是最基礎的概念，負責和 AI 大模型互動。

首先需要引入至少一個 [AI 大模型依賴](https://mvnrepository.com/artifact/dev.langchain4j/langchain4j-community-dashscope-spring-boot-starter)，這裡選擇國內的阿里雲大模型，提供了和 Spring Boot 專案的整合依賴包，比較方便：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-community-dashscope-spring-boot-starter</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

需要到 [阿里雲百鍊平臺](https://bailian.console.aliyun.com/?tab=model#/api-key) 獲取大模型呼叫 key，注意不要洩露！

![](https://pic.yupi.icu/1/1752030336360-af14dd92-7708-45dd-8420-fe87727726f3.png)

回到專案，在配置檔案中新增大模型配置，指定模型名稱和 API Key：

```yaml
langchain4j:
  community:
    dashscope:
      chat-model:
        model-name: qwen-max
        api-key: <You API Key here>
```

可以 [按需選擇模型名稱](https://bailian.console.aliyun.com/?tab=doc#/doc/?type=model)，追求效果可以用 qwen-max，否則可以選擇效果、速度、成本均衡的 qwen-plus。

![](https://pic.yupi.icu/1/1752030577658-2b939caa-cf27-4065-aac5-e4f3234646b6.png)

除了編寫配置讓 Spring Boot 自動構建 ChatModel 外，也可以透過構造器自己建立 ChatModel 物件。這種方式更靈活，在 LangChain4j 中我們會經常用到這種方式來構造物件。

```java
ChatModel qwenModel = QwenChatModel.builder()
                    .apiKey("You API key here")
                    .modelName("qwen-max")
                    .enableSearch(true)
                    .temperature(0.7)
                    .maxTokens(4096)
                    .stops(List.of("Hello"))
                    .build();
```

有了 ChatModel 後，建立一個 AiCodeHelper 類，引入自動注入的 qwenChatModel，編寫簡單的對話程式碼，並利用 Lombok 註解列印輸出結果日誌：

```java
@Service
@Slf4j
public class AiCodeHelper {

    @Resource
    private ChatModel qwenChatModel;

    public String chat(String message) {
        UserMessage userMessage = UserMessage.from(message);
        ChatResponse chatResponse = qwenChatModel.chat(userMessage);
        AiMessage aiMessage = chatResponse.aiMessage();
        log.info("AI 輸出：" + aiMessage.toString());
        return aiMessage.text();
    }
}
```

編寫單元測試，向 AI 打個招呼吧：

```java
@SpringBootTest
class AiCodeHelperTest {

    @Resource
    private AiCodeHelper aiCodeHelper;

    @Test
    void chat() {
        aiCodeHelper.chat("你好，我是程式設計師魚皮");
    }
}
```

以 Debug 模式執行單元測試，成功執行並檢視輸出：

![](https://pic.yupi.icu/1/1751947565712-9e3c0a68-930b-4968-8a54-19eb8beb48c9.png)

如果遇到找不到符號的 lombok 報錯：

![](https://pic.yupi.icu/1/1751947096901-ca5ec0a7-ecd1-4447-9f7e-b679ad56dcde.png)
可以修改 IDEA 的註解處理器配置，改為使用專案中的 lombok：

![](https://pic.yupi.icu/1/1751947494173-01ebf704-c87b-4c6b-96a3-58aafccd5458.png)



### 多模態 - Multimodality

多模態是指能夠同時處理、理解和生成多種不同型別資料的能力，比如文字、影象、音訊、影片、PDF 等等。

![](https://pic.yupi.icu/1/1752051068307-72038162-f759-4fce-a0d8-0b5eec4cc59e.png)

LangChain4j 中使用多模態的方法很簡單，使用者訊息中是可以新增圖片、音影片、PDF 等媒體資源的。

![](https://pic.yupi.icu/1/1752031262335-7dda9965-faa8-44e9-8a18-f748549299fa.png)

我們先編寫一個支援傳入自定義 UserMessage 的方法：

```java
public String chatWithMessage(UserMessage userMessage) {
    ChatResponse chatResponse = qwenChatModel.chat(userMessage);
    AiMessage aiMessage = chatResponse.aiMessage();
    log.info("AI 輸出：" + aiMessage.toString());
    return aiMessage.text();
}
```

然後編寫單元測試，傳入一張圖片：

```java
@Test
void chatWithMessage() {
    UserMessage userMessage = UserMessage.from(
            TextContent.from("描述圖片"),
            ImageContent.from("https://www.codefather.cn/logo.png")
    );
    aiCodeHelper.chatWithMessage(userMessage);
}
```

但是效果不理想，qwen-max 模型無法直接檢視或分析圖片：

![](https://pic.yupi.icu/1/1751948068455-4a25e7b7-9186-4148-bf42-de66b10ecef1.png)

![](https://pic.yupi.icu/1/1751949077879-32103f89-88f4-45b0-8609-77bc9ad8403d.png)



這也是目前多模態開發最關鍵的問題，雖然編碼不難，但需要大模型本身支援多模態。可以在 LangChain 官網看到 [大模型能力支援表](https://docs.langchain4j.dev/integrations/language-models/)，不過一切以實際測試為準。

![](https://pic.yupi.icu/1/1752031226164-9a0cf728-a4d7-4005-8bbf-3f43c0479c01.png)



目前框架對多模態的適配度也沒有那麼好，一不留神就報錯了，所以我們先了解這種用法就好了，感興趣的同學也可以用 OpenAI 等其他模型實現多模態。



### 系統提示詞 - SystemMessage

系統提示詞是設定 AI 模型行為規則和角色定位的隱藏指令，使用者通常不能直接看到。系統 Prompt 相當於給 AI 設定人格和能力邊界，也就是告訴 AI “你是誰？你能做什麼？”。

根據我們的需求，編寫一段系統提示詞：

```markdown
你是程式設計領域的小助手，幫助使用者解答程式設計學習和求職面試相關的問題，並給出建議。重點關注 4 個方向：
1. 規劃清晰的程式設計學習路線
2. 提供專案學習建議
3. 給出程式設計師求職全流程指南（比如簡歷最佳化、投遞技巧）
4. 分享高頻面試題和麵試技巧
請用簡潔易懂的語言回答，助力使用者高效學習與求職。
```

程式設計導航的同學可以看 [AI 超級智慧體專案第 3 期](https://www.codefather.cn/course/1915010091721236482/section/1916676331948027906)，有講解過提示詞最佳化技巧。

![](https://pic.yupi.icu/1/1752031662526-ffba01f1-3358-4d6b-a6e3-e293781cc77c.png)

想要使用系統提示詞，最直接的方法是建立一個系統訊息，把它和使用者訊息一起傳送給 AI。

修改 chat 方法，程式碼如下：

```java
private static final String SYSTEM_MESSAGE = """
        你是程式設計領域的小助手，幫助使用者解答程式設計學習和求職面試相關的問題，並給出建議。重點關注 4 個方向：
        1. 規劃清晰的程式設計學習路線
        2. 提供專案學習建議
        3. 給出程式設計師求職全流程指南（比如簡歷最佳化、投遞技巧）
        4. 分享高頻面試題和麵試技巧
        請用簡潔易懂的語言回答，助力使用者高效學習與求職。
        """;

public String chat(String message) {
    SystemMessage systemMessage = SystemMessage.from(SYSTEM_MESSAGE);
    UserMessage userMessage = UserMessage.from(message);
    ChatResponse chatResponse = qwenChatModel.chat(systemMessage, userMessage);
    AiMessage aiMessage = chatResponse.aiMessage();
    log.info("AI 輸出：" + aiMessage.toString());
    return aiMessage.text();
}
```

再次執行單元測試和 AI 對話，顯然系統預設生效了：

![](https://pic.yupi.icu/1/1751949397794-26716439-7ccb-46f2-add4-ff299989b10e.png)



### AI 服務 - AI Service

在學習更多特性前，我們要了解 LangChain4j 最重要的開發模式 —— AI Service，提供了很多高層抽象的、用起來更方便的 API，把 AI 應用當做服務來開發。

#### 使用 AI Service

首先引入 langchain4j 依賴：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j</artifactId>
    <version>1.1.0</version>
</dependency>
```

然後建立一個程式設計助手 AI Service 服務，採用宣告式開發方法，編寫一個對話方法，然後可以直接透過 `@SystemMessage` 註解定義系統提示詞。

```java
public interface AiCodeHelperService {

    @SystemMessage("你是一位程式設計小助手")
    String chat(String userMessage);
}
```

不過由於我們提示詞較長，寫到註解裡很不優雅，所以單獨在 resources 目錄下新建檔案 `system-prompt.txt` 來儲存系統提示詞。

`@SystemMessage` 註解支援從檔案中讀取系統提示詞：

```java
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);
}
```

然後我們需要編寫工廠類，用於建立 AI Service：

```java
@Configuration
public class AiCodeHelperServiceFactory {

    @Resource
    private ChatModel qwenChatModel;

    @Bean
    public AiCodeHelperService aiCodeHelperService() {
        return AiServices.create(AiCodeHelperService.class, qwenChatModel);
    }
}
```

呼叫 `AiServices.create` 方法就可以建立出 AI Service 的實現類了，背後的原理是利用 Java 反射機制建立了一個實現介面的代理物件，代理物件負責輸入和輸出的轉換，比如把 String 型別的使用者訊息引數轉為 UserMessage 型別並呼叫 ChatModel，再將 AI 返回的 AiMessage 型別轉換為 String 型別作為返回值。

但我們不用關心這麼多，直接寫介面和註解來開發就好。你喜歡這種開發方式麼？

編寫單元測試，呼叫我們開發的 AI Service：

```java
@SpringBootTest
class AiCodeHelperServiceTest {

    @Resource
    private AiCodeHelperService aiCodeHelperService;

    @Test
    void chat() {
        String result = aiCodeHelperService.chat("你好，我是程式設計師魚皮");
        System.out.println(result);
    }
}
```

Debug 執行，發現生成了 AI Service 的代理類，並且系統提示詞生效了。是不是比之前自己拼接系統訊息要方便多了？

![](https://pic.yupi.icu/1/1751953464452-273ae8c5-4354-467e-b14b-668d64c3b1f3.png)

#### Spring Boot 專案中使用

如果你覺得手動呼叫 create 方法來建立 Service 比較麻煩，在 Spring Boot 專案中可以引入依賴：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-spring-boot-starter</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

然後給 AI Service 加上 `@AiService` 註解，就能自動建立出服務例項了：

```java
@AiService
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);
}
```

記得註釋掉之前工廠類的 @Configuration 註解，否則會出現 Bean 衝突

再次執行單元測試，也是可以正常對話的：

![](https://pic.yupi.icu/1/1751953748624-64447a00-d43c-4f8e-9fd1-805efa910753.png)

這種方式雖然更方便了，但是缺少了自主構建的靈活性（可以自由設定很多引數），所以我建議還是採用自主構建。之後的功能特性，我們也會基於這種 AI Service 開發模式來實現。

### 會話記憶 - ChatMemory

會話記憶是指讓 AI 能夠記住使用者之前的對話內容，並保持上下文連貫性，這是實現 AI 應用的核心特性。

怎麼實現對話記憶？最傳統的方式是自己維護訊息列表，不僅要手動新增訊息，訊息多了還要考慮淘汰、不同使用者的訊息還要隔離，想想都頭疼！

```java
// 自己實現會話記憶
Map<String, List<Message>> conversationHistory = new HashMap<>();

public String chat(String message, String userId) {
    // 獲取使用者歷史記錄
    List<Message> history = conversationHistory.getOrDefault(userId, new ArrayList<>());
    
    // 新增使用者新訊息
    Message userMessage = new Message("user", message);
    history.add(userMessage);
    
    // 構建完整歷史上下文
    StringBuilder contextBuilder = new StringBuilder();
    for (Message msg : history) {
        contextBuilder.append(msg.getRole()).append(": ").append(msg.getContent()).append("\n");
    }
    
    // 呼叫 AI API
    String response = callAiApi(contextBuilder.toString());
    
    // 儲存 AI 回覆到歷史
    Message aiMessage = new Message("assistant", response);
    history.add(aiMessage);
    conversationHistory.put(userId, history);
    
    return response;
}
```

#### 使用會話記憶

LangChain4j 為我們提供了開箱即用的 `MessageWindowChatMemory` 會話記憶，最多儲存 N 條訊息，多餘的會自動淘汰。建立會話記憶後，在構造 AI Service 設定 chatMemory：

```java
@Configuration
public class AiCodeHelperServiceFactory {

    @Resource
    private ChatModel qwenChatModel;

    @Bean
    public AiCodeHelperService aiCodeHelperService() {
        // 會話記憶
        ChatMemory chatMemory = MessageWindowChatMemory.withMaxMessages(10);
        AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
                .chatModel(qwenChatModel)
                .chatMemory(chatMemory)
                .build();
        return aiCodeHelperService;
    }
}
```

編寫單元測試，測試會話記憶是否生效：

```java
@Test
void chatWithMemory() {
    String result = aiCodeHelperService.chat("你好，我是程式設計師魚皮");
    System.out.println(result);
    result = aiCodeHelperService.chat("你好，我是誰來著？");
    System.out.println(result);
}
```

Debug 執行單元測試，可以看到會話記憶儲存的訊息列表：

![](https://pic.yupi.icu/1/1751954519469-e2f60419-ad5d-41fd-945d-c13d9861fe0f.png)

檢視輸出結果，會話記憶生效：

![](https://pic.yupi.icu/1/1751954654615-b4efd4d5-b87a-4980-9c65-0e252c4dd379.png)

#### 進階用法

會話記憶預設是儲存在記憶體的，重啟後會丟失，可以透過自定義 [ChatMemoryStore](https://docs.langchain4j.dev/tutorials/chat-memory#persistence) 介面的實現類，將訊息儲存到 MySQL 等其他資料來源中。

![](https://pic.yupi.icu/1/1752040734375-fa8362f4-c2d2-4ecd-9f3d-f328f0459b58.png)

如果有多個使用者，希望每個使用者之間的訊息隔離，可以透過給對話方法增加 memoryId 引數和註解，在呼叫對話時傳入 memoryId 即可（類似聊天室的房間號）：

```java
String chat(@MemoryId int memoryId, @UserMessage String userMessage);
```

構造 AI Service 時，可以透過 chatMemoryProvider 來指定 **每個 memoryId 單獨建立會話記憶**：

```java
// 構造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemoryProvider(memoryId -> MessageWindowChatMemory.withMaxMessages(10))
        .build();
```



### 結構化輸出

結構化輸出是指將大模型返回的文字輸出轉換為結構化的資料格式，比如一段 JSON、一個物件、或者是複雜的物件列表。

![](https://pic.yupi.icu/1/1752051496139-a403e8ad-9b0d-4b1c-924a-cd572f872b05.png)

結構化輸出有 3 種實現方式：

- 利用大模型的 JSON schema
- 利用 Prompt + JSON Mode
- 利用 Prompt

預設是 Prompt 模式，也就是在原本的使用者提示詞下 **拼接一段內容** 來指定大模型強制輸出包含特定欄位的 JSON 文字。

```markdown
你是一個專業的資訊提取助手。請從給定文字中提取人員資訊，
並嚴格按照以下 JSON 格式返回結果：

{
    "name": "人員姓名",
    "age": 年齡數字,
    "height": 身高（米），
    "married": true/false,
    "occupation": "職業"
}

重要規則：
1. 只返回 JSON 格式，不要新增任何解釋
2. 如果資訊不明確，使用 null
3. age 必須是數字，不是字串
4. married 必須是布林值
```

感興趣的同學可以 [閱讀這篇文章](https://glaforge.dev/posts/2024/11/18/data-extraction-the-many-ways-to-get-llms-to-spit-json-content/) 瞭解更多，不過我們開發時無需關心這些，只要修改對話方法的返回值，框架就會自動幫我們實現結構化輸出，非常爽！

![](https://pic.yupi.icu/1/1752051189479-456a7016-ab27-4a18-8927-088724ac5ddb.png)

比如我們增加一個 **讓 AI 生成學習報告** 的方法，AI 需要輸出學習報告物件，包含名稱和建議列表：

```java
@SystemMessage(fromResource = "system-prompt.txt")
Report chatForReport(String userMessage);

// 學習報告
record Report(String name, List<String> suggestionList){}
```

編寫單元測試：

```java
@Test
void chatForReport() {
    String userMessage = "你好，我是程式設計師魚皮，學程式設計兩年半，請幫我制定學習報告";
    AiCodeHelperService.Report report = aiCodeHelperService.chatForReport(userMessage);
    System.out.println(report);
}
```

執行單元測試，效果很不錯：

![](https://pic.yupi.icu/1/1751955304297-a26adf70-eda0-4ebc-ae2e-aa5a8e67cf02.png)

如果你發現 AI 有時無法生成準確的 JSON，那麼可以採用 JSON Schema 模式，直接在請求中約束 LLM 的輸出格式。這是目前最可靠、精確度最高的結構化輸出實現。

```java
ResponseFormat responseFormat = ResponseFormat.builder()
        .type(JSON)
        .jsonSchema(JsonSchema.builder()
                .name("Person")
                .rootElement(JsonObjectSchema.builder()
                        .addStringProperty("name")
                        .addIntegerProperty("age")
                        .addNumberProperty("height")
                        .addBooleanProperty("married")
                        .required("name", "age", "height", "married") 
                        .build())
                .build())
        .build();
ChatRequest chatRequest = ChatRequest.builder()
        .responseFormat(responseFormat)
        .messages(userMessage)
        .build();
```



### 檢索增強生成 - RAG

RAG（Retrieval-Augmented Generation，檢索增強生成）是一種結合資訊檢索技術和 AI 內容生成的混合架構，可以解決大模型的知識時效性限制和幻覺問題。

簡單來說，RAG 就像給 AI 配了一個 “小抄本”，讓 AI 回答問題前先查一查特定的知識庫來獲取知識，確保回答是基於真實資料而不是憑空想象。很多企業也基於 RAG 搭建了自己的智慧客服，可以用自己積累的領域知識回覆使用者。

RAG 的完整工作流程如下：

![](https://pic.yupi.icu/1/1752052410659-f9a142b9-0c2a-4a99-9c8c-8339970c96eb.png)

讓我們來實操一下，首先我準備了 4 個文件，放在了 `resources/docs` 目錄下：

![](https://pic.yupi.icu/1/1752041906112-ac985734-3a43-44a7-b13d-a1632e426828.png)

LangChain 提供了 3 種 RAG 的實現方式，我把它稱為：極簡版、標準版、進階版。

#### 極簡版 RAG

**極簡版適合快速檢視效果**，首先需要引入額外的依賴，裡面包含了內建的離線 Embedding 模型，開箱即用：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-easy-rag</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

示例程式碼如下，使用內建的文件載入器讀取文件，然後利用內建的 Embedding 模型將文件轉換成向量，並儲存在內建的 Embedding 記憶體儲存中，最後給 AI Service 繫結預設的內容檢索器。

```java
// RAG
// 1. 載入文件
List<Document> documents = FileSystemDocumentLoader.loadDocuments("src/main/resources/docs");
// 2. 使用內建的 EmbeddingModel 轉換文字為向量，然後儲存到自動注入的記憶體 embeddingStore 中
EmbeddingStoreIngestor.ingest(documents, embeddingStore);
// 構造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        // RAG：從記憶體 embeddingStore 中檢索匹配的文字片段
        .contentRetriever(EmbeddingStoreContentRetriever.from(embeddingStore))
        .build();
```

可以看到，極簡版的特點是 “一切皆預設”，實際開發中，為了更好的效果，建議採用標準版或進階版。

#### 標準版 RAG

下面來試試標準版 RAG 實現，為了更好地效果，我們需要：

- 載入 Markdown 文件並按需切割
- Markdown 文件補充檔名資訊
- 自定義 Embedding 模型
- 自定義內容檢索器

在 Spring Boot 配置檔案中新增 Embedding 模型配置，使用阿里雲提供的 `text-embedding-v4` 模型：

```yaml
langchain4j:
  community:
    dashscope:
      chat-model:
        model-name: qwen-max
        api-key: <You API Key here>
      embedding-model:
        model-name: text-embedding-v4
        api-key: <You API Key here>
```

新建 `rag.RagConfig`，編寫 RAG 相關的程式碼，執行 RAG 的初始流程並返回了一個定製的內容檢索器 Bean：

```java
/**
 * 載入 RAG
 */
@Configuration
public class RagConfig {

    @Resource
    private EmbeddingModel qwenEmbeddingModel;

    @Resource
    private EmbeddingStore<TextSegment> embeddingStore;

    @Bean
    public ContentRetriever contentRetriever() {
        // ------ RAG ------
        // 1. 載入文件
        List<Document> documents = FileSystemDocumentLoader.loadDocuments("src/main/resources/docs");
        // 2. 文件切割：將每個文件按每段進行分割，最大 1000 字元，每次重疊最多 200 個字元
        DocumentByParagraphSplitter paragraphSplitter = new DocumentByParagraphSplitter(1000, 200);
        // 3. 自定義文件載入器
        EmbeddingStoreIngestor ingestor = EmbeddingStoreIngestor.builder()
                .documentSplitter(paragraphSplitter)
                // 為了提高搜尋質量，為每個 TextSegment 新增文件名稱
                .textSegmentTransformer(textSegment -> TextSegment.from(
                        textSegment.metadata().getString("file_name") + "\n" + textSegment.text(),
                        textSegment.metadata()
                ))
                // 使用指定的向量模型
                .embeddingModel(qwenEmbeddingModel)
                .embeddingStore(embeddingStore)
                .build();
        // 載入文件
        ingestor.ingest(documents);
        // 4. 自定義內容查詢器
        ContentRetriever contentRetriever = EmbeddingStoreContentRetriever.builder()
                .embeddingStore(embeddingStore)
                .embeddingModel(qwenEmbeddingModel)
                .maxResults(5) // 最多 5 個檢索結果
                .minScore(0.75) // 過濾掉分數小於 0.75 的結果
                .build();
        return contentRetriever;
    }
}
```

然後在構建 AI Service 時繫結內容檢索器：

```java
@Resource
private ContentRetriever contentRetriever;

@Bean
public AiCodeHelperService aiCodeHelperService() {
    // 會話記憶
    ChatMemory chatMemory = MessageWindowChatMemory.withMaxMessages(10);
    // 構造 AI Service
    AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
            .chatModel(qwenChatModel)
            .chatMemory(chatMemory)
            .contentRetriever(contentRetriever) // RAG 檢索增強生成
            .build();
    return aiCodeHelperService;
}
```

編寫單元測試：

```java
@Test
void chatWithRag() {
    Result<String> result = aiCodeHelperService.chatWithRag("怎麼學習 Java？有哪些常見面試題？");
    System.out.println(result.content());
    System.out.println(result.sources());
}
```

Debug 執行，能夠看到分割的文件片段，部分文件片段有內容重疊：

![](https://pic.yupi.icu/1/1751962218145-1291831b-be55-44d8-9d73-af3e4bbe3dff.png)

可以在對話記憶中看到實際傳送的、增強後的 Prompt：

![](https://pic.yupi.icu/1/1751962545347-a358cb1b-94d8-47ec-b9e1-c72234aeff4a.png)

![](https://pic.yupi.icu/1/1751962597654-e87d90cc-3240-4982-9c8e-a5228468b1e7.png)

回答效果也是符合預期的：

![](https://pic.yupi.icu/1/1751962714819-a74a07e9-2f0b-44ce-b4ee-db4a4041966c.png)



#### 獲取引用源文件

如果能夠給 AI 的回答下面展示回答來源，更容易增加內容的可信度：

![](https://pic.yupi.icu/1/1752042954244-609fbce6-beb7-4d4b-87a5-c26cd3b8bb9a.png)

在 LangChain4j 中，實現這個功能很簡單。在 AI Service 中新增方法，在原本的返回型別外封裝一層 Result 類，就可以獲得封裝後的結果，從中能夠獲取到 RAG 引用的源文件、以及 Token 的消耗情況等等。

```java
@SystemMessage(fromResource = "system-prompt.txt")
Result<String> chatWithRag(String userMessage);
```

修改單元測試，輸出更多資訊：

```java
@Test
void chatWithRag() {
    Result<String> result = aiCodeHelperService.chatWithRag("怎麼學習 Java？有哪些常見面試題？");
    String content = result.content();
    List<Content> sources = result.sources();
    System.out.println(content);
    System.out.println(sources);
}
```

執行效果如圖，獲取到了引用的源文件資訊：

![](https://pic.yupi.icu/1/1751973326587-f0a61ddc-a0b7-4eb8-949b-d19e257262fc.png)

#### 進階版 RAG

這就是一套標準的 RAG 實現了，大多數時候，使用標準版就夠了。進階版會更加靈活，額外支援查詢轉換器、查詢路由、內容聚合器、內容注入器等特性，將整個 RAG 的流程流水線化（RAG pipeline）。

![](https://pic.yupi.icu/1/1752043947317-362c8de1-26e4-4657-ada0-fb414a2dab13.png)

定義好 RAG 流程後，最後透過 RetrievalAugmentor 提供給 AI Service：

```java
AiServices.builder(xxx.class)
    ...
    .retrievalAugmentor(retrievalAugmentor)
    .build();
```

此外，之前我們使用的是記憶體向量儲存，每次啟動都要重新載入文件、呼叫嵌入模型，比較耗時，所以實際開發中建議使用獨立的儲存，[官方支援很多第三方儲存](https://docs.langchain4j.dev/integrations/embedding-stores/)，但是個人比較推薦 PG Vector，在原有關係庫的基礎上安裝外掛來支援向量儲存，而且支援的特性很多。

![](https://pic.yupi.icu/1/1752044157711-6b5a9190-93ff-4a97-aa43-c42c519a2a0b.png)

### 工具呼叫 - Tools

工具呼叫（Tool Calling）可以理解為讓 AI 大模型 **借用外部工具** 來完成它自己做不到的事情。

跟人類一樣，如果只憑手腳完成不了工作，那麼就可以利用工具箱來完成。

工具可以是任何東西，比如網頁搜尋、對外部 API 的呼叫、訪問外部資料、或執行特定的程式碼等。

比如使用者提問 “幫我查詢上海最新的天氣”，AI 本身並沒有這些知識，它就可以呼叫 “查詢天氣工具”，來完成任務。

需要注意的是，工具呼叫的本質 **並不是 AI 伺服器自己呼叫這些工具、也不是把工具的程式碼傳送給 AI 伺服器讓它執行**，它只能提出要求，表示 “我需要執行 XX 工具完成任務”。而真正執行工具的是我們自己的應用程式，執行後再把結果告訴 AI，讓它繼續工作。

![](https://pic.yupi.icu/1/1752051591909-adecdfe5-87d0-4801-b556-58beea244ebe.png)



我們需要的網路搜尋能力，就可以透過工具呼叫來實現。這裡我們細化下需求：讓 AI 能夠透過我的 [面試鴨刷題網站](https://www.mianshiya.com/) 來搜尋面試題。

實現方案很簡單，因為面試鴨網站的搜尋頁面 **支援透過 URL 引數傳入不同的搜尋關鍵詞**，我們只需要利用 **Jsoup 庫** 抓取面試鴨搜尋頁面的題目列表就可以了。

好傢伙，我爬我自己？不過大家不要嘗試，很容易被封號。

![](https://pic.yupi.icu/1/1752044504400-9b3b8719-dff6-4071-a084-e1236434b0c0.png)



先引入 Jsoup 庫：

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.20.1</version>
</dependency>
```

然後在 `tools` 包下編寫工具，透過 `@Tool` 註解就能宣告工具了，注意 **要認真編寫工具和工具引數的描述**，這直接決定了 AI 能否正確地呼叫工具。

```java
@Slf4j
public class InterviewQuestionTool {

    /**
     * 從面試鴨網站獲取關鍵詞相關的面試題列表
     *
     * @param keyword 搜尋關鍵詞（如"redis"、"java多執行緒"）
     * @return 面試題列表，若失敗則返回錯誤資訊
     */
    @Tool(name = "interviewQuestionSearch", value = """
            Retrieves relevant interview questions from mianshiya.com based on a keyword.
            Use this tool when the user asks for interview questions about specific technologies,
            programming concepts, or job-related topics. The input should be a clear search term.
            """
    )
    public String searchInterviewQuestions(@P(value = "the keyword to search") String keyword) {
        List<String> questions = new ArrayList<>();
        // 構建搜尋URL（編碼關鍵詞以支援中文）
        String encodedKeyword = URLEncoder.encode(keyword, StandardCharsets.UTF_8);
        String url = "https://www.mianshiya.com/search/all?searchText=" + encodedKeyword;
        // 傳送請求並解析頁面
        Document doc;
        try {
            doc = Jsoup.connect(url)
                    .userAgent("Mozilla/5.0")
                    .timeout(5000)
                    .get();
        } catch (IOException e) {
            log.error("get web error", e);
            return e.getMessage();
        }
        // 提取面試題
        Elements questionElements = doc.select(".ant-table-cell > a");
        questionElements.forEach(el -> questions.add(el.text().trim()));
        return String.join("\n", questions);
    }
}
```

給 AI Service 繫結工具：

```java
// 構造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        .contentRetriever(contentRetriever) // RAG 檢索增強生成
        .tools(new InterviewQuestionTool()) // 工具呼叫
        .build();
```

編寫單元測試，驗證工具的效果：

```java
@Test
void chatWithTools() {
    String result = aiCodeHelperService.chat("有哪些常見的計算機網路面試題？");
    System.out.println(result);
}
```

Debug 執行，發現 AI 呼叫了工具：

![](https://pic.yupi.icu/1/1751964854933-395ecc9e-0fb6-4788-b8e2-ae5ef1d094a7.png)

工具檢索到了題目列表：

![](https://pic.yupi.icu/1/1751964893075-84d0ac23-fe02-47c0-95c3-e422d1305448.png)

可以透過 Debug 看到 AI Service 載入了工具：

![](https://pic.yupi.icu/1/1751964979312-65f04b40-9554-438b-83ff-025009f30a1c.png)

可以透過會話記憶檢視工具的呼叫過程：

![](https://pic.yupi.icu/1/1751965074185-165ed1b9-a50f-4d21-ae85-b8c439f5065c.png)

輸出結果符合預期：

![](https://pic.yupi.icu/1/1751965104933-af4b3181-4dc0-40bb-9ef9-5e1c0e26b389.png)

前面只演示了最簡單的工具定義方法 —— 宣告式，LangChain4j 也提供了程式設計式的工具定義方法，不過我相信你不會想這麼做的（除非是動態建立工具）。

![](https://pic.yupi.icu/1/1752045043475-a61743d1-e1ea-4912-bfac-d77ce6e43858.png)

除了聯網搜尋外，還有一些經典的工具，比如檔案讀寫、PDF 生成、呼叫終端、輸出圖表等等。這些工具我們可以自己開發，也可以透過 MCP 直接使用別人開發好的工具。



### 模型上下文協議 - MCP

MCP（Model Context Protocol，模型上下文協議）是一種開放標準，目的是增強 AI 與外部系統的互動能力。MCP 為 AI 提供了與外部工具、資源和服務互動的標準化方式，讓 AI 能夠訪問最新資料、執行復雜操作，並與現有系統整合。

可以將 MCP 想象成 AI 應用的 USB 介面。就像 USB 為裝置連線各種外設和配件提供了標準化方式一樣，MCP 為 AI 模型連線不同的資料來源和工具提供了標準化的方法。

![](https://pic.yupi.icu/1/1752051649523-398e66d6-87fa-4cc4-8c9d-951939844405.png)

簡單來說，透過 MCP 協議，AI 應用可以輕鬆接入別人提供的服務來實現更多功能，比如查詢地理位置、運算元據庫、部署網站、甚至是支付等等。

剛剛我們透過工具呼叫實現了面試題的搜尋，下面我們利用 MCP 實現 **全網搜尋內容**，這也是一個典型的 MCP 應用場景了。

首先從 MCP 服務市場搜尋 Web Search 服務，推薦 [下面這個](https://mcp.so/server/zhipu-web-search/BigModel?tab=content)，因為它提供了 SSE 線上呼叫服務，不用我們自己在本地安裝啟動，很方便。

![](https://pic.yupi.icu/1/1752045285371-fd70d350-80bd-4037-9b57-ff8d3a37ccf5.png)

但也要注意，用別人的服務可能是需要 API Key 的，一般是按量付費。

需要先去 [平臺官方獲取 API Key](https://www.bigmodel.cn/usercenter/proj-mgmt/apikeys)，等會兒會用到：

![](https://pic.yupi.icu/1/1752045399400-4e8fe95f-5d5c-47dc-aa6e-4225f2df23aa.png)

然後我們要在程式中使用這個 MCP 服務。比較坑的是，感覺 LangChain 對 MCP 的支援沒有那麼好，官方文件甚至都沒有提到要引入的 MCP 依賴包。我還是從開源倉庫中找到的依賴：

![](https://pic.yupi.icu/1/1751967113982-099b0b9a-d5a3-43e0-bdf1-1ccfb8d093b2.png)

引入依賴：

```xml
<!-- https://mvnrepository.com/artifact/dev.langchain4j/langchain4j-mcp -->
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-mcp</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

在配置檔案中新增 API Key 的配置：

```yaml
bigmodel:
  api-key: <Your Api Key>
```

新建 `mcp.McpConfig`，按照官方的開發方式，初始化和 MCP 服務的通訊，並建立 McpToolProvider 的 Bean：

```java
@Configuration
public class McpConfig {

    @Value("${bigmodel.api-key}")
    private String apiKey;

    @Bean
    public McpToolProvider mcpToolProvider() {
        // 和 MCP 服務通訊
        McpTransport transport = new HttpMcpTransport.Builder()
                .sseUrl("https://open.bigmodel.cn/api/mcp/web_search/sse?Authorization=" + apiKey)
                .logRequests(true) // 開啟日誌，檢視更多資訊
                .logResponses(true)
                .build();
        // 建立 MCP 客戶端
        McpClient mcpClient = new DefaultMcpClient.Builder()
                .key("yupiMcpClient")
                .transport(transport)
                .build();
        // 從 MCP 客戶端獲取工具
        McpToolProvider toolProvider = McpToolProvider.builder()
                .mcpClients(mcpClient)
                .build();
        return toolProvider;
    }
}
```

注意，上面我們是透過 SSE 的方式呼叫 MCP。如果你是透過 npx 或 uvx 本地啟動 MCP 服務，需要先安裝對應的工具，並且利用下面的配置建立通訊：

```java
McpTransport transport = new StdioMcpTransport.Builder()
    .command(List.of("/usr/bin/npm", "exec", "@modelcontextprotocol/server-everything@0.6.2"))
    .logEvents(true) // only if you want to see the traffic in the log
    .build();
```

在 AI Service 中應用 MCP 工具：

```java
@Resource
private McpToolProvider mcpToolProvider;

// 構造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        .contentRetriever(contentRetriever) // RAG 檢索增強生成
        .tools(new InterviewQuestionTool()) // 工具呼叫
        .toolProvider(mcpToolProvider) // MCP 工具呼叫
        .build();
```

編寫單元測試：

```java
@Test
void chatWithMcp() {
    String result = aiCodeHelperService.chat("什麼是程式設計師魚皮的程式設計導航？");
    System.out.println(result);
}
```

執行單元測試，透過日誌檢視到了搜尋過程：

![](https://pic.yupi.icu/1/1751967601320-5242e432-ea07-4038-bc6f-7364aefe3d6a.png)

MCP 服務生效，從網上檢索到了內容作為答案：

![](https://pic.yupi.icu/1/1751967705158-c4591073-858c-4584-a5ee-7d2ecb5261d6.png)

目前，文件中並沒有提到利用 LangChain4j 開發 MCP 的方法，不過目前也不建議用 Java 開發 MCP。

### 護軌 - Guardrail

其實我感覺護軌這個名字起的不太好，其實我們把它理解為攔截器就好了。分為輸入護軌（input guardrails）和輸出護軌（output guardrails），可以在請求 AI 前和接收到 AI 的響應後執行一些額外操作，比如呼叫 AI 前鑑權、呼叫 AI 後記錄日誌。

![](https://pic.yupi.icu/1/1752051765814-ca0a709d-216e-4f84-8a05-0a8b9a3a6b66.png)

讓我們小試一把，在呼叫 AI 前進行敏感詞檢測，如果使用者提示詞包含敏感詞，則直接拒絕。

新建 `guardrail.SafeInputGuardrail`，實現 InputGuardrail 介面：

```java
/**
 * 安全檢測輸入護軌
 */
public class SafeInputGuardrail implements InputGuardrail {

    private static final Set<String> sensitiveWords = Set.of("kill", "evil");

    /**
     * 檢測使用者輸入是否安全
     */
    @Override
    public InputGuardrailResult validate(UserMessage userMessage) {
        // 獲取使用者輸入並轉換為小寫以確保大小寫不敏感
        String inputText = userMessage.singleText().toLowerCase();
        // 使用正規表示式分割輸入文字為單詞
        String[] words = inputText.split("\\W+");
        // 遍歷所有單詞，檢查是否存在敏感詞
        for (String word : words) {
            if (sensitiveWords.contains(word)) {
                return fatal("Sensitive word detected: " + word);
            }
        }
        return success();
    }
}
```

LangChain4j 提供了幾種快速返回的方法，簡單來說，想繼續呼叫 AI 就返回 success、否則就返回 fatal。

![](https://pic.yupi.icu/1/1751968291132-96a670ce-6551-4726-8c62-045021303af1.png)

修改 AI Service，使用輸入護軌：

```java
@InputGuardrails({SafeInputGuardrail.class})
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);

    @SystemMessage(fromResource = "system-prompt.txt")
    Report chatForReport(String userMessage);

    // 學習報告
    record Report(String name, List<String> suggestionList) {
    }
}
```

編寫單元測試，寫一個包含敏感詞的提示詞：

```java
@Test
void chatWithGuardrail() {
    String result = aiCodeHelperService.chat("kill the game");
    System.out.println(result);
}
```

執行並檢視效果，會觸發輸入檢測，直接丟擲異常：

![](https://pic.yupi.icu/1/1751968796339-ebf23753-55ad-4123-a4dc-e599859a28a1.png)

如果不包含敏感詞，則會順利透過。

![](https://pic.yupi.icu/1/1751968877451-3ac9f488-0b78-4c04-a227-3c89b54847c8.png)

當然，除了輸入護軌，也可以編寫輸出護軌，對 AI 的響應結果進行檢測。

### 日誌和可觀測性

之前我們都是透過 Debug 檢視執行資訊，不僅不便於除錯，而且生產環境肯定不能這麼做。

官方提供了 [日誌](https://docs.langchain4j.dev/tutorials/logging) 和 [可觀測性](https://docs.langchain4j.dev/tutorials/observability)，來幫我們更好地除錯程式、發現問題。

#### 日誌

開啟日誌的方法很簡單，直接構造模型時指定開啟、或者直接編寫 Spring Boot 配置，支援列印 AI 請求和響應日誌。

```java
OpenAiChatModel.builder()
    ...
    .logRequests(true)
    .logResponses(true)
    .build();
langchain4j.open-ai.chat-model.log-requests = true
langchain4j.open-ai.chat-model.log-responses = true
logging.level.dev.langchain4j = DEBUG
```

但並不是所有的 ChatModel 都支援，比如我測試下來 QwenChatModel 就不支援。這時只能把希望交給可觀測性了。

#### 可觀測性

可以透過自定義 Listener 獲取 ChatModel 的呼叫資訊，比較靈活。

新建 `listener.ChatModelListenerConfig`，輸出請求、響應、錯誤資訊：

```java
@Configuration
@Slf4j
public class ChatModelListenerConfig {
    
    @Bean
    ChatModelListener chatModelListener() {
        return new ChatModelListener() {
            @Override
            public void onRequest(ChatModelRequestContext requestContext) {
                log.info("onRequest(): {}", requestContext.chatRequest());
            }

            @Override
            public void onResponse(ChatModelResponseContext responseContext) {
                log.info("onResponse(): {}", responseContext.chatResponse());
            }

            @Override
            public void onError(ChatModelErrorContext errorContext) {
                log.info("onError(): {}", errorContext.error().getMessage());
            }
        };
    }
}
```

但是隻定義 Listener 好像對 QwenChatModel 不起作用，所以我們需要手動構造自定義的 QwenChatModel。

新建 `model.QwenChatModelConfig`，構造 ChatModel 物件並繫結 Listener：

```java
@Configuration
@ConfigurationProperties(prefix = "langchain4j.community.dashscope.chat-model")
@Data
public class QwenChatModelConfig {

    private String modelName;

    private String apiKey;

    @Resource
    private ChatModelListener chatModelListener;

    @Bean
    public ChatModel myQwenChatModel() {
        return QwenChatModel.builder()
                .apiKey(apiKey)
                .modelName(modelName)
                .listeners(List.of(chatModelListener))
                .build();
    }
}
```

然後，可以將原本引用 ChatModel 的名稱改為 `myQwenChatModel`，防止和 Spring Boot 自動注入的 ChatModel 衝突。

再次呼叫 AI，就能看到很多資訊了：

![](https://pic.yupi.icu/1/1751974020940-84059541-3935-4505-b114-6fcc809b04f5.png)

### AI 服務化

至此，AI 的能力基本開發完成，但是目前只支援本地執行，需要編寫一個介面提供給前端呼叫，讓 AI 能夠成為一個服務。

我們平時開發的大多數介面都是同步介面，也就是等後端處理完再返回。但是對於 AI 應用，特別是響應時間較長的對話類應用，可能會讓使用者失去耐心等待，因此推薦使用 SSE（Server-Sent Events）技術實現實時流式輸出，類似打字機效果，大幅提升使用者體驗。

#### SSE 流式介面開發

LangChain 提供了 2 種方式來支援流式響應（注意，流式響應不支援結構化輸出）。

一種方法是 [TokenStream](https://docs.langchain4j.dev/tutorials/ai-services#streaming)，先讓 AI 對話方法返回 TokenStream，然後建立 AI Service 時指定流式對話模型 StreamingChatModel：

```java
interface Assistant {

    TokenStream chat(String message);
}

StreamingChatModel model = OpenAiStreamingChatModel.builder()
    .apiKey(System.getenv("OPENAI_API_KEY"))
    .modelName(GPT_4_O_MINI)
    .build();

Assistant assistant = AiServices.create(Assistant.class, model);

TokenStream tokenStream = assistant.chat("Tell me a joke");

tokenStream.onPartialResponse((String partialResponse) -> System.out.println(partialResponse))
    .onRetrieved((List<Content> contents) -> System.out.println(contents))
    .onToolExecuted((ToolExecution toolExecution) -> System.out.println(toolExecution))
    .onCompleteResponse((ChatResponse response) -> System.out.println(response))
    .onError((Throwable error) -> error.printStackTrace())
    .start();
```

我個人會更喜歡另一種方法，[使用 Flux](https://docs.langchain4j.dev/tutorials/ai-services/#flux) 代替 TokenStream，熟悉響應式程式設計的同學應該對 Flux 不陌生吧？讓 AI 對話方法返回 Flux 響應式物件即可。示例程式碼：

```java
interface Assistant {

  Flux<String> chat(String message);
}
```

讓我們試一下，首先需要引入響應式包依賴：

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-reactor</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

然後給 AI Service 增加流式對話方法，這裡順便支援下多使用者的會話記憶：

```java
// 流式對話
Flux<String> chatStream(@MemoryId int memoryId, @UserMessage String userMessage);
```

由於要用到流式模型，需要增加流式模型配置：

```yaml
langchain4j:
  community:
    dashscope:
      streaming-chat-model:
        model-name: qwen-max
        api-key: <Your Api Key>
```

構造 AI Service 時指定流式對話模型（自動注入即可），並且補充會話記憶提供者：

```java
@Resource
private StreamingChatModel qwenStreamingChatModel;

AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(myQwenChatModel)
        .streamingChatModel(qwenStreamingChatModel)
        .chatMemory(chatMemory)
        .chatMemoryProvider(memoryId ->
                MessageWindowChatMemory.withMaxMessages(10)) // 每個會話獨立儲存
        .contentRetriever(contentRetriever) // RAG 檢索增強生成
        .tools(new InterviewQuestionTool()) // 工具呼叫
        .toolProvider(mcpToolProvider) // MCP 工具呼叫
        .build();
```

最後，編寫 Controller 介面。為了方便測試，這裡使用 Get 請求：

```java
@RestController
@RequestMapping("/ai")
public class AiController {

    @Resource
    private AiCodeHelperService aiCodeHelperService;

    @GetMapping("/chat")
    public Flux<ServerSentEvent<String>> chat(int memoryId, String message) {
        return aiCodeHelperService.chatStream(memoryId, message)
                .map(chunk -> ServerSentEvent.<String>builder()
                        .data(chunk)
                        .build());
    }
}
```

增加伺服器配置，指定後端埠和介面路徑字首：

```yaml
server:
  port: 8081
  servlet:
    context-path: /api
```

啟動伺服器，用 CURL 工具測試呼叫：

```bash
curl -G 'http://localhost:8081/api/ai/chat' \
  --data-urlencode 'message=我是程式設計師魚皮' \
  --data-urlencode 'memoryId=1'
```

可以看到流式的輸出結果：

![](https://pic.yupi.icu/1/1751975773168-c4ddd770-abd7-4555-90b6-8d487630aee4.png)



#### 後端支援跨域

為了讓前端專案能夠順利呼叫後端介面，我們需要在後端配置跨域支援。在 config 包下建立跨域配置類，程式碼如下：

```java
/**
 * 全域性跨域配置
 */
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        // 覆蓋所有請求
        registry.addMapping("/**")
                // 允許傳送 Cookie
                .allowCredentials(true)
                // 放行哪些域名（必須用 patterns，否則 * 會和 allowCredentials 衝突）
                .allowedOriginPatterns("*")
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                .allowedHeaders("*")
                .exposedHeaders("*");
    }
}
```

注意，如果 `.allowedOrigins("*")` 與 `.allowCredentials(true)` 同時配置會導致衝突，因為出於安全考慮，跨域請求不能同時允許所有域名訪問和傳送認證資訊（比如 Cookie）。



## AI 生成前端

由於這個專案不需要很複雜的頁面，我們可以利用 AI 來快速生成前端程式碼，極大提高開發效率。這裡魚皮使用 [主流 AI 開發工具 Cursor](https://www.cursor.com/)，挑戰不寫一行程式碼，生成符合要求的前端專案。

### 提示詞

首先準備一段詳細的 Prompt，一般要包括需求、技術選型、後端介面資訊，還可以提供一些原型圖、後端程式碼等。

```markdown
你是一位專業的前端開發，請幫我根據下列資訊來生成對應的前端專案程式碼。

## 需求

應用為《AI 程式設計小助手》，幫助使用者解答程式設計學習和求職面試相關的問題，並給出建議。

只有一個頁面，就是主頁：頁面風格為聊天室，上方是聊天記錄（使用者資訊在右邊，AI 資訊在左邊），下方是輸入框，進入頁面後自動生成一個聊天室 id，用於區分不同的會話。透過 SSE 的方式呼叫 chat 介面，實時顯示對話內容。

## 技術選型

1. Vue3 專案
2. Axios 請求庫

## 後端介面資訊

介面地址字首：http://localhost:8081/api

## SpringBoot 後端介面程式碼

@RestController
@RequestMapping("/ai")
public class AiController {

    @GetMapping("/chat")
    public Flux<ServerSentEvent<String>> chat(int memoryId, String message) {
        return aiCodeHelperService.chatStream(memoryId, message)
                .map(chunk -> ServerSentEvent.<String>builder()
                        .data(chunk)
                        .build());
    }
}
```

注意，如果使用的是 Windows 系統，最好在 prompt 中補充“你應該使用 Windows 支援的命令來完成任務”。



### 開發

在專案根目錄下建立新的前端專案資料夾 `ai-code-helper-frontend`，使用 Cursor 工具開啟該目錄，輸入 Prompt 執行。注意要選擇 Agent 模式、Thinking 深度思考模型（推薦 Claude）：

![](https://pic.yupi.icu/1/1751976145149-beefc903-31e1-4a4f-8bbe-edf41a3a4806.png)

除了原始碼外，魚皮這裡連專案介紹文件 `README.md` 都生成了，確實很爽！

![](https://pic.yupi.icu/1/1752025773338-e87a94c7-db0b-4213-9cc8-f643b14f5182.png)

生成完程式碼後，開啟終端執行 `npm run dev` 命令，或者開啟 `package.json` 檔案並利用 Debug 按鈕啟動專案：

![](https://pic.yupi.icu/1/1752026474929-cd4a7225-1e48-4e95-a08e-6f69ea256d45.png)

### 檢視效果

執行前端專案後，首先驗證功能是否正常，再驗證樣式。如果發現功能不可用（比如傳送訊息後沒有回覆），可以按 F12 開啟瀏覽器控制檯檢視前端錯誤資訊、或者看後端專案控制檯的錯誤資訊，具體報錯資訊具體分析。這塊就會涉及到一些前端相關的知識了，不懂前端的同學儘量多問 AI，讓它幫忙修復 Bug 就好。**如果實在搞不定，也別瞎折騰了！**用魚皮的程式碼就好。

比如我遇到了連線後端 SSE 服務報錯的問題，直接複製報錯資訊給 AI 解決：

![](https://pic.yupi.icu/1/1752025968566-ab2c2d53-59e4-4519-bf55-e07b095f1e5d.png)

成功執行，檢視效果：

![](https://pic.yupi.icu/1/1752026740589-5b4670c8-3f5c-470e-afba-4cfd469c31ee.png)

![](https://pic.yupi.icu/1/1752026767000-6599f85f-5926-4174-a06e-55e30e4df667.png)

確保功能和樣式沒問題後，記得先提交程式碼（防止後續被 AI 生成的程式碼汙染），然後你可以按需增加更多功能，比如用 Markdown 展示 AI 的回覆訊息。

![](https://pic.yupi.icu/1/1752027043776-cd6d17ed-175f-4c7e-8b25-aee81a5296b2-20250710114303496.png)



## 總結

OK，以上就是 LangChain4j 實戰專案教程，怎麼樣，大家學會了還是學廢了？

回到開頭的那個問題：**實際開發中應該如何選擇 AI 開發框架呢？**

就拿 Spring AI 和 LangChain4j 來說，不知道大家更喜歡哪個框架？我其實會更喜歡 Spring AI 的開發模式，而且 Spring AI 目前支援的能力更多，還有國內 Spring AI Alibaba 的巨頭加持，生態更好，遇到問題更容易解決；LangChain4j 的優勢在於可以獨立於 Spring 專案使用，更自由靈活一些。

不過這類框架大家重點學習一個就好了，很多概念和用法是相通的：

![](https://pic.yupi.icu/1/1752050425995-3b2b8cf4-ad48-41ec-a1e5-154ae6cd8526.png)




## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)
