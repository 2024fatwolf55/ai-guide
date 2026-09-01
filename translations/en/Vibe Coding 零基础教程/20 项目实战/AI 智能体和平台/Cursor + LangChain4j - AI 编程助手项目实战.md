# Cursor + LangChain4j - AI Programming Assistant Project in Action

This is a complete full-stack AI programming assistant project tutorial. The project is developed using a combination of manual coding and Vibe Coding: we write Java code to call AI and use AI tools like Cursor to assist with coding. The focus is on learning how to integrate AI capabilities into Java projects, while systematically going through almost all mainstream usages and features of the LangChain4j framework. It’s suitable for students who already have some Java backend development foundation, want to quickly get started with AI application development, and add an AI project to their resume.

Estimated learning time: 1–5 hours.

---

Hello everyone, I’m programmer Yupi. Nowadays, AI application development can be said to be a must-have skill for programmers, and it can significantly boost your competitiveness in job hunting. Earlier, I used Spring AI to lead everyone through building an [open-source AI super agent project](https://github.com/liyupi/yu-ai-agent). This time, I’ll help everyone quickly master another mainstream Java AI application development framework: LangChain4j.

This tutorial is also carefully designed by me. Instead of drowning you in boring theory, I’ll use a small AI programming assistant project to guide everyone through almost all mainstream LangChain usage patterns and features step by step in real practice. By the end of it, not only will you have learned LangChain, you’ll also gain a concrete project experience to put on your resume. Isn’t that beautiful?

**This article is nearly ten thousand Chinese characters long, so it’s a bit lengthy. I recommend bookmarking it. The video version is even better for learning~**

> Full video tutorial: https://bilibili.com/video/BV1X4GGziEyr
>
> Project code open source: https://github.com/liyupi/ai-code-helper

## Requirements Analysis

We want to build an AI programming assistant that can help users answer questions and give guidance for programming study, such as:

- Programming learning roadmaps
- Project study suggestions
- Programmer job-hunting guidance
- Common programmer interview questions

![](https://pic.yupi.icu/1/1752027043776-cd6d17ed-175f-4c7e-8b25-aee81a5296b2-20250710114302208.png)

To achieve this, we first need to be able to call AI to complete **basic conversations**, and it also needs to support **multi-turn conversation memory**. On top of that, if we want to further enhance the AI’s capabilities, we need to let it **use tools** to search the web; we can also have the AI answer based on our own **knowledge base**, so it can provide users with the resources and experience we’ve accumulated in the programming field.

![](https://pic.yupi.icu/1/1752028612444-351672a3-3725-4850-82b5-57d63d0ba866.png)

If we implemented all of that from scratch, it would still be pretty troublesome, so we need to use an AI development framework to improve efficiency.

## What Is LangChain4j?

At present, the mainstream Java AI development frameworks are [Spring AI](https://spring.io/projects/spring-ai) and [LangChain4j](https://docs.langchain4j.dev/intro). Both provide many **out-of-the-box APIs** to help you call large models and implement common AI-development capabilities, including what we’re going to learn today:

- Conversation memory
- Structured output
- RAG knowledge bases
- Tool calling
- MCP
- SSE streaming output

From my personal experience, these two frameworks share many similar concepts and usage patterns. Both also provide lots of plugin-based extensions and support integration with Spring Boot projects. Of course, there are differences in coding style, but which one is better is ultimately a matter of personal preference.

**So how should you choose in real development?**

I’d like to first take you through building a project with LangChain4j, and then reveal the answer at the end—because by then, you’ll also have your own thoughts.

## AI Application Development

### Create a New Project

Open IDEA, create a new Spring Boot project, and **choose Java version 21** (because LangChain4j requires at least version 17):

![](https://pic.yupi.icu/1/1751944012715-3ac04ad2-42e9-4c41-b998-a5318050e27c.png)

Select dependencies, use Spring Boot 3.5.x, and include Spring MVC and the Lombok annotation library:

![](https://pic.yupi.icu/1/1751944035875-83da11bb-e5fa-4a19-ae57-9c214cc0f523.png)

After creating the project, first change the config file extension to `yml`, which will make later configuration easier.

![](https://pic.yupi.icu/1/1751944110301-93054763-76d8-4686-ac6e-971e81b4acd4.png)

Here I recommend creating an `application-local.yml` configuration file, putting sensitive configuration used during development there, and then adding it to `.gitignore` so you don’t accidentally open-source it.

### AI Conversation - ChatModel

`ChatModel` is the most basic concept. It’s responsible for interacting with the AI model.

First, you need to introduce at least one [AI model dependency](https://mvnrepository.com/artifact/dev.langchain4j/langchain4j-community-dashscope-spring-boot-starter). Here I chose Alibaba Cloud’s domestic model, because it provides a Spring Boot integration package, which is relatively convenient:

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-community-dashscope-spring-boot-starter</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

You need to get the model invocation key from the [Alibaba Cloud Bailian platform](https://bailian.console.aliyun.com/?tab=model#/api-key). Be careful not to leak it!

![](https://pic.yupi.icu/1/1752030336360-af14dd92-7708-45dd-8420-fe87727726f3.png)

Back in the project, add the model configuration to the config file, specifying the model name and API Key:

```yaml
langchain4j:
  community:
    dashscope:
      chat-model:
        model-name: qwen-max
        api-key: <You API Key here>
```

You can [choose the model name as needed](https://bailian.console.aliyun.com/?tab=doc#/doc/?type=model). If you want stronger output quality, use `qwen-max`; otherwise, you can choose `qwen-plus` for a better balance between quality, speed, and cost.

![](https://pic.yupi.icu/1/1752030577658-2b939caa-cf27-4065-aac5-e4f3234646b6.png)

Besides writing configuration and letting Spring Boot automatically construct the `ChatModel`, you can also create the `ChatModel` object yourself through a constructor. This approach is more flexible, and in LangChain4j we’ll often use this way of constructing objects.

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

Once you have a `ChatModel`, create an `AiCodeHelper` class, inject the auto-wired `qwenChatModel`, write some simple chat code, and use a Lombok annotation to print the result log:

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
        log.info("AI 输出：" + aiMessage.toString());
        return aiMessage.text();
    }
}
```

Write a unit test and say hello to the AI:

```java
@SpringBootTest
class AiCodeHelperTest {

    @Resource
    private AiCodeHelper aiCodeHelper;

    @Test
    void chat() {
        aiCodeHelper.chat("你好，我是程序员鱼皮");
    }
}
```

Run the unit test in Debug mode, and after it succeeds, inspect the output:

![](https://pic.yupi.icu/1/1751947565712-9e3c0a68-930b-4968-8a54-19eb8beb48c9.png)

If you run into a Lombok “cannot find symbol” error:

![](https://pic.yupi.icu/1/1751947096901-ca5ec0a7-ecd1-4447-9f7e-b679ad56dcde.png)

You can modify IDEA’s annotation processor settings so it uses the project’s Lombok:

![](https://pic.yupi.icu/1/1751947494173-01ebf704-c87b-4c6b-96a3-58aafccd5458.png)

### Multimodality

Multimodality refers to the ability to simultaneously process, understand, and generate different types of data, such as text, images, audio, video, PDFs, and so on.

![](https://pic.yupi.icu/1/1752051068307-72038162-f759-4fce-a0d8-0b5eec4cc59e.png)

Using multimodality in LangChain4j is simple. User messages can include media resources such as images, audio, video, and PDFs.

![](https://pic.yupi.icu/1/1752031262335-7dda9965-faa8-44e9-8a18-f748549299fa.png)

First, let’s write a method that accepts a custom `UserMessage`:

```java
public String chatWithMessage(UserMessage userMessage) {
    ChatResponse chatResponse = qwenChatModel.chat(userMessage);
    AiMessage aiMessage = chatResponse.aiMessage();
    log.info("AI 输出：" + aiMessage.toString());
    return aiMessage.text();
}
```

Then write a unit test and pass in an image:

```java
@Test
void chatWithMessage() {
    UserMessage userMessage = UserMessage.from(
            TextContent.from("描述图片"),
            ImageContent.from("https://www.codefather.cn/logo.png")
    );
    aiCodeHelper.chatWithMessage(userMessage);
}
```

But the result is not ideal. The `qwen-max` model cannot directly view or analyze images:

![](https://pic.yupi.icu/1/1751948068455-4a25e7b7-9186-4148-bf42-de66b10ecef1.png)

![](https://pic.yupi.icu/1/1751949077879-32103f89-88f4-45b0-8609-77bc9ad8403d.png)

This is also the key issue in multimodal development right now: the coding itself is not difficult, but the model must support multimodality. You can see a [capability support matrix for models](https://docs.langchain4j.dev/integrations/language-models/) on the LangChain site, but in practice, actual testing is what really matters.

![](https://pic.yupi.icu/1/1752031226164-9a0cf728-a4d7-4005-8bbf-3f43c0479c01.png)

The framework’s multimodal adaptation also isn’t that robust yet, and it’s easy to hit errors if you’re not careful. So for now, just understand this usage pattern. If you’re interested, you can also use OpenAI or other models to implement multimodal capabilities.

### System Prompt - SystemMessage

A system prompt is a hidden instruction used to define the AI model’s behavior rules and role positioning. Users usually can’t see it directly. In other words, the System Prompt defines the AI’s personality and capability boundaries—it tells the AI: “Who are you? What can you do?”

Based on our requirements, let’s write a system prompt:

```markdown
你是编程领域的小助手，帮助用户解答编程学习和求职面试相关的问题，并给出建议。重点关注 4 个方向：
1. 规划清晰的编程学习路线
2. 提供项目学习建议
3. 给出程序员求职全流程指南（比如简历优化、投递技巧）
4. 分享高频面试题和面试技巧
请用简洁易懂的语言回答，助力用户高效学习与求职。
```

Students from Programming Navigation can check [Phase 3 of the AI Super Agent project](https://www.codefather.cn/course/1915010091721236482/section/1916676331948027906), where I already explained prompt optimization techniques.

![](https://pic.yupi.icu/1/1752031662526-ffba01f1-3358-4d6b-a6e3-e293781cc77c.png)

To use a system prompt, the most direct approach is to create a system message and send it to the AI together with the user message.

Modify the `chat` method as follows:

```java
private static final String SYSTEM_MESSAGE = """
        你是编程领域的小助手，帮助用户解答编程学习和求职面试相关的问题，并给出建议。重点关注 4 个方向：
        1. 规划清晰的编程学习路线
        2. 提供项目学习建议
        3. 给出程序员求职全流程指南（比如简历优化、投递技巧）
        4. 分享高频面试题和面试技巧
        请用简洁易懂的语言回答，助力用户高效学习与求职。
        """;

public String chat(String message) {
    SystemMessage systemMessage = SystemMessage.from(SYSTEM_MESSAGE);
    UserMessage userMessage = UserMessage.from(message);
    ChatResponse chatResponse = qwenChatModel.chat(systemMessage, userMessage);
    AiMessage aiMessage = chatResponse.aiMessage();
    log.info("AI 输出：" + aiMessage.toString());
    return aiMessage.text();
}
```

Run the unit test again and talk with the AI. Obviously, the system preset is now taking effect:

![](https://pic.yupi.icu/1/1751949397794-26716439-7ccb-46f2-add4-ff299989b10e.png)

### AI Service

Before learning more features, we need to understand LangChain4j’s most important development pattern: **AI Service**. It provides many higher-level abstractions and more convenient APIs, allowing you to develop AI applications as services.

#### Using AI Service

First, introduce the `langchain4j` dependency:

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j</artifactId>
    <version>1.1.0</version>
</dependency>
```

Then create an AI Service for the programming assistant. Use a declarative development style: define a chat method, and directly use the `@SystemMessage` annotation to define the system prompt.

```java
public interface AiCodeHelperService {

    @SystemMessage("你是一位编程小助手")
    String chat(String userMessage);
}
```

But since our prompt is relatively long, putting it directly in the annotation is not elegant. So create a separate file called `system-prompt.txt` under the `resources` directory to store the system prompt.

The `@SystemMessage` annotation supports loading the system prompt from a file:

```java
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);
}
```

Then we need to write a factory class to create the AI Service:

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

Calling `AiServices.create` creates the implementation class of the AI Service. Under the hood, it uses Java reflection to create a proxy object implementing the interface. That proxy object is responsible for converting inputs and outputs—for example, turning a `String` user-message parameter into a `UserMessage`, calling the `ChatModel`, and converting the returned `AiMessage` into a `String`.

But we don’t need to care about those internals. Just write interfaces and annotations to develop with it. Do you like this development style?

Write a unit test and call the AI Service we developed:

```java
@SpringBootTest
class AiCodeHelperServiceTest {

    @Resource
    private AiCodeHelperService aiCodeHelperService;

    @Test
    void chat() {
        String result = aiCodeHelperService.chat("你好，我是程序员鱼皮");
        System.out.println(result);
    }
}
```

Run it in Debug mode, and you’ll see that the proxy class for AI Service has been generated, and the system prompt is taking effect. Isn’t that much more convenient than manually stitching together system messages as before?

![](https://pic.yupi.icu/1/1751953464452-273ae8c5-4354-467e-b14b-668d64c3b1f3.png)

#### Using It in a Spring Boot Project

If you find it troublesome to manually call `create` to build the Service, then in a Spring Boot project you can introduce the dependency:

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-spring-boot-starter</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

Then add the `@AiService` annotation to the AI Service, and the service instance will be created automatically:

```java
@AiService
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);
}
```

Remember to comment out the `@Configuration` annotation in the earlier factory class, otherwise you’ll get a Bean conflict.

If you run the unit test again, the conversation still works normally:

![](https://pic.yupi.icu/1/1751953748624-64447a00-d43c-4f8e-9fd1-805efa910753.png)

Although this approach is more convenient, it lacks the flexibility of manual construction (you can freely set many parameters there), so I still recommend constructing it yourself. The later features in this article will also be implemented based on this AI Service development pattern.

### Conversation Memory - ChatMemory

Conversation memory means allowing AI to remember the user’s previous conversation content and maintain contextual coherence. This is a core feature for AI applications.

How do you implement conversation memory? The most traditional way is to maintain the message list yourself. Not only do you need to manually add messages, but when the number of messages grows, you also need to think about eviction, and messages from different users need isolation. Just thinking about it is already a headache!

```java
// 自己实现会话记忆
Map<String, List<Message>> conversationHistory = new HashMap<>();

public String chat(String message, String userId) {
    // 获取用户历史记录
    List<Message> history = conversationHistory.getOrDefault(userId, new ArrayList<>());
    
    // 添加用户新消息
    Message userMessage = new Message("user", message);
    history.add(userMessage);
    
    // 构建完整历史上下文
    StringBuilder contextBuilder = new StringBuilder();
    for (Message msg : history) {
        contextBuilder.append(msg.getRole()).append(": ").append(msg.getContent()).append("\n");
    }
    
    // 调用 AI API
    String response = callAiApi(contextBuilder.toString());
    
    // 保存 AI 回复到历史
    Message aiMessage = new Message("assistant", response);
    history.add(aiMessage);
    conversationHistory.put(userId, history);
    
    return response;
}
```

#### Using Conversation Memory

LangChain4j provides the ready-to-use `MessageWindowChatMemory`, which keeps up to N messages and automatically evicts the excess. After creating the conversation memory, set `chatMemory` when constructing the AI Service:

```java
@Configuration
public class AiCodeHelperServiceFactory {

    @Resource
    private ChatModel qwenChatModel;

    @Bean
    public AiCodeHelperService aiCodeHelperService() {
        // 会话记忆
        ChatMemory chatMemory = MessageWindowChatMemory.withMaxMessages(10);
        AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
                .chatModel(qwenChatModel)
                .chatMemory(chatMemory)
                .build();
        return aiCodeHelperService;
    }
}
```

Write a unit test to verify whether the conversation memory takes effect:

```java
@Test
void chatWithMemory() {
    String result = aiCodeHelperService.chat("你好，我是程序员鱼皮");
    System.out.println(result);
    result = aiCodeHelperService.chat("你好，我是谁来着？");
    System.out.println(result);
}
```

Run the unit test in Debug mode and you’ll be able to see the message list stored in memory:

![](https://pic.yupi.icu/1/1751954519469-e2f60419-ad5d-41fd-945d-c13d9861fe0f.png)

Looking at the output, conversation memory is clearly taking effect:

![](https://pic.yupi.icu/1/1751954654615-b4efd4d5-b87a-4980-9c65-0e252c4dd379.png)

#### Advanced Usage

By default, conversation memory is stored in memory, so it is lost after a restart. By implementing a custom [ChatMemoryStore](https://docs.langchain4j.dev/tutorials/chat-memory#persistence), you can persist messages into MySQL or other data sources.

![](https://pic.yupi.icu/1/1752040734375-fa8362f4-c2d2-4ecd-9f3d-f328f0459b58.png)

If there are multiple users and you want their messages to be isolated from each other, you can add a `memoryId` parameter and annotation to the conversation method, and then pass in the `memoryId` when calling it (similar to a chat-room room number):

```java
String chat(@MemoryId int memoryId, @UserMessage String userMessage);
```

When constructing the AI Service, you can use `chatMemoryProvider` to specify **creating a separate conversation memory for each `memoryId`**:

```java
// 构造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemoryProvider(memoryId -> MessageWindowChatMemory.withMaxMessages(10))
        .build();
```

### Structured Output

Structured output means converting the text returned by the large model into a structured data format, such as a JSON string, an object, or even a complex object list.

![](https://pic.yupi.icu/1/1752051496139-a403e8ad-9b0d-4b1c-924a-cd572f872b05.png)

There are 3 ways to implement structured output:

- Use the model’s JSON schema capability
- Use Prompt + JSON Mode
- Use Prompt only

The default is Prompt mode. In other words, the framework **appends a piece of content** to the original user prompt to force the model to output JSON text containing specific fields.

```markdown
你是一个专业的信息提取助手。请从给定文本中提取人员信息，
并严格按照以下 JSON 格式返回结果：

{
    "name": "人员姓名",
    "age": 年龄数字,
    "height": 身高（米），
    "married": true/false,
    "occupation": "职业"
}

重要规则：
1. 只返回 JSON 格式，不要添加任何解释
2. 如果信息不明确，使用 null
3. age 必须是数字，不是字符串
4. married 必须是布尔值
```

Interested students can [read this article](https://glaforge.dev/posts/2024/11/18/data-extraction-the-many-ways-to-get-llms-to-spit-json-content/) to learn more. But in actual development, we don’t need to care too much about that. As long as we change the return type of the conversation method, the framework automatically helps us implement structured output. It feels great!

![](https://pic.yupi.icu/1/1752051189479-456a7016-ab27-4a18-8927-088724ac5ddb.png)

For example, let’s add a method that **has the AI generate a learning report**. The AI needs to output a report object containing a name and a list of suggestions:

```java
@SystemMessage(fromResource = "system-prompt.txt")
Report chatForReport(String userMessage);

// 学习报告
record Report(String name, List<String> suggestionList){}
```

Write a unit test:

```java
@Test
void chatForReport() {
    String userMessage = "你好，我是程序员鱼皮，学编程两年半，请帮我制定学习报告";
    AiCodeHelperService.Report report = aiCodeHelperService.chatForReport(userMessage);
    System.out.println(report);
}
```

Run the unit test. The result is pretty good:

![](https://pic.yupi.icu/1/1751955304297-a26adf70-eda0-4ebc-ae2e-aa5a8e67cf02.png)

If you find that the AI sometimes can’t generate accurate JSON, then you can use JSON Schema mode to directly constrain the LLM output format in the request. This is currently the most reliable and most accurate way to implement structured output.

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

### Retrieval-Augmented Generation - RAG

RAG (Retrieval-Augmented Generation) is a hybrid architecture that combines information retrieval and AI content generation. It helps solve the limitations of model knowledge cutoff and hallucination.

Simply put, RAG is like giving the AI a “cheat sheet.” Before answering a question, the AI first checks a specific knowledge base to gather information, ensuring that the answer is based on real materials instead of made-up guesses. Many enterprises also use RAG to build intelligent customer service systems that answer users with their own accumulated domain knowledge.

The complete RAG workflow looks like this:

![](https://pic.yupi.icu/1/1752052410659-f9a142b9-0c2a-4a99-9c8c-8339970c96eb.png)

Let’s practice it. First, I prepared 4 documents and placed them under the `resources/docs` directory:

![](https://pic.yupi.icu/1/1752041906112-ac985734-3a43-44a7-b13d-a1632e426828.png)

LangChain provides 3 ways to implement RAG. I call them: the ultra-simple version, the standard version, and the advanced version.

#### Ultra-Simple RAG

**The ultra-simple version is suitable for quickly seeing the effect.** First, you need to introduce an extra dependency. It includes a built-in offline Embedding model and works out of the box:

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-easy-rag</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

The sample code is as follows: use the built-in document loader to read documents, use the built-in Embedding model to convert documents into vectors, store them in the built-in Embedding in-memory store, and finally bind the default content retriever to the AI Service.

```java
// RAG
// 1. 加载文档
List<Document> documents = FileSystemDocumentLoader.loadDocuments("src/main/resources/docs");
// 2. 使用内置的 EmbeddingModel 转换文本为向量，然后存储到自动注入的内存 embeddingStore 中
EmbeddingStoreIngestor.ingest(documents, embeddingStore);
// 构造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        // RAG：从内存 embeddingStore 中检索匹配的文本片段
        .contentRetriever(EmbeddingStoreContentRetriever.from(embeddingStore))
        .build();
```

As you can see, the ultra-simple version is characterized by “everything is default.” In real development, for better results, I recommend using the standard or advanced version instead.

#### Standard RAG

Now let’s try the standard RAG implementation. To get better results, we need to:

- Load Markdown documents and split them as needed
- Add filename information to the Markdown documents
- Customize the Embedding model
- Customize the content retriever

Add Embedding model configuration to the Spring Boot config file, using Alibaba Cloud’s `text-embedding-v4` model:

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

Create `rag.RagConfig`, write the RAG-related code, execute the initial RAG flow, and return a customized content retriever Bean:

```java
/**
 * 加载 RAG
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
        // 1. 加载文档
        List<Document> documents = FileSystemDocumentLoader.loadDocuments("src/main/resources/docs");
        // 2. 文档切割：将每个文档按每段进行分割，最大 1000 字符，每次重叠最多 200 个字符
        DocumentByParagraphSplitter paragraphSplitter = new DocumentByParagraphSplitter(1000, 200);
        // 3. 自定义文档加载器
        EmbeddingStoreIngestor ingestor = EmbeddingStoreIngestor.builder()
                .documentSplitter(paragraphSplitter)
                // 为了提高搜索质量，为每个 TextSegment 添加文档名称
                .textSegmentTransformer(textSegment -> TextSegment.from(
                        textSegment.metadata().getString("file_name") + "\n" + textSegment.text(),
                        textSegment.metadata()
                ))
                // 使用指定的向量模型
                .embeddingModel(qwenEmbeddingModel)
                .embeddingStore(embeddingStore)
                .build();
        // 加载文档
        ingestor.ingest(documents);
        // 4. 自定义内容查询器
        ContentRetriever contentRetriever = EmbeddingStoreContentRetriever.builder()
                .embeddingStore(embeddingStore)
                .embeddingModel(qwenEmbeddingModel)
                .maxResults(5) // 最多 5 个检索结果
                .minScore(0.75) // 过滤掉分数小于 0.75 的结果
                .build();
        return contentRetriever;
    }
}
```

Then bind the content retriever when building the AI Service:

```java
@Resource
private ContentRetriever contentRetriever;

@Bean
public AiCodeHelperService aiCodeHelperService() {
    // 会话记忆
    ChatMemory chatMemory = MessageWindowChatMemory.withMaxMessages(10);
    // 构造 AI Service
    AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
            .chatModel(qwenChatModel)
            .chatMemory(chatMemory)
            .contentRetriever(contentRetriever) // RAG 检索增强生成
            .build();
    return aiCodeHelperService;
}
```

Write a unit test:

```java
@Test
void chatWithRag() {
    Result<String> result = aiCodeHelperService.chatWithRag("怎么学习 Java？有哪些常见面试题？");
    System.out.println(result.content());
    System.out.println(result.sources());
}
```

Run it in Debug mode, and you can see the split document chunks, with some overlapping content between certain segments:

![](https://pic.yupi.icu/1/1751962218145-1291831b-be55-44d8-9d73-af3e4bbe3dff.png)

You can also inspect the actual enhanced Prompt sent to the model in the conversation memory:

![](https://pic.yupi.icu/1/1751962545347-a358cb1b-94d8-47ec-b9e1-c72234aeff4a.png)

![](https://pic.yupi.icu/1/1751962597654-e87d90cc-3240-4982-9c8e-a5228468b1e7.png)

And the answer quality is also in line with expectations:

![](https://pic.yupi.icu/1/1751962714819-a74a07e9-2f0b-44ce-b4ee-db4a4041966c.png)

#### Obtain Referenced Source Documents

If you can display the answer’s sources underneath the AI response, it becomes much easier to increase the credibility of the content:

![](https://pic.yupi.icu/1/1752042954244-609fbce6-beb7-4d4b-87a5-c26cd3b8bb9a.png)

In LangChain4j, implementing this is very simple. Add a new method to the AI Service, and wrap the original return type inside a `Result` class. This gives you access to the wrapped result, where you can obtain the RAG source documents, Token usage, and more.

```java
@SystemMessage(fromResource = "system-prompt.txt")
Result<String> chatWithRag(String userMessage);
```

Modify the unit test to print more information:

```java
@Test
void chatWithRag() {
    Result<String> result = aiCodeHelperService.chatWithRag("怎么学习 Java？有哪些常见面试题？");
    String content = result.content();
    List<Content> sources = result.sources();
    System.out.println(content);
    System.out.println(sources);
}
```

The execution result is shown below: you can now obtain the referenced source document information:

![](https://pic.yupi.icu/1/1751973326587-f0a61ddc-a0b7-4eb8-949b-d19e257262fc.png)

#### Advanced RAG

At this point, you already have a standard RAG implementation, and most of the time that’s enough. The advanced version is even more flexible. It additionally supports query transformers, query routing, content aggregators, content injectors, and other features, turning the entire RAG workflow into a pipeline.

![](https://pic.yupi.icu/1/1752043947317-362c8de1-26e4-4657-ada0-fb414a2dab13.png)

After defining the RAG flow, pass it to the AI Service through `RetrievalAugmentor`:

```java
AiServices.builder(xxx.class)
    ...
    .retrievalAugmentor(retrievalAugmentor)
    .build();
```

Also, earlier we used in-memory vector storage, which means every startup requires reloading documents and calling the embedding model again, which is time-consuming. So in real development, I recommend using independent storage. [The official docs support many third-party stores](https://docs.langchain4j.dev/integrations/embedding-stores/), but personally I recommend PG Vector. It adds vector storage support as a plugin on top of an existing relational database and supports many powerful features.

![](https://pic.yupi.icu/1/1752044157711-6b5a9190-93ff-4a97-aa43-c42c519a2a0b.png)

### Tool Calling - Tools

Tool Calling can be understood as allowing the large AI model to **borrow external tools** to accomplish tasks it cannot complete on its own.

Just like humans: if you can’t finish a job with just your hands and feet, then you use tools from the toolbox.

A tool can be almost anything: web search, calling an external API, accessing external data, or executing specific code.

For example, if the user asks, “Help me check the latest weather in Shanghai,” the AI itself doesn’t have that knowledge, so it can call a “weather lookup tool” to complete the task.

One thing to note is that the essence of tool calling **is not that the AI server calls those tools by itself, nor that the tool code is sent to the AI server for execution**. The AI can only make a request, saying “I need to execute tool XX to finish the task.” The actual execution of the tool is done by our own application, and then the result is returned to the AI so it can continue working.

![](https://pic.yupi.icu/1/1752051591909-adecdfe5-87d0-4801-b556-58beea244ebe.png)

The web search capability we need can be implemented through tool calling. Let’s refine the requirement a bit here: let the AI search interview questions through my [Mianshiya interview practice site](https://www.mianshiya.com/).

The implementation plan is simple. Because the Mianshiya search page **supports passing different search keywords through URL parameters**, we only need to use the **Jsoup library** to scrape the list of interview questions from the search page.

Wow, so I’m scraping my own site? Don’t copy that, though—you could get yourself banned easily.

![](https://pic.yupi.icu/1/1752044504400-9b3b8719-dff6-4071-a084-e1236434b0c0.png)

First, introduce the Jsoup library:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.20.1</version>
</dependency>
```

Then write the tool under the `tools` package. With the `@Tool` annotation, you can declare a tool directly. Pay attention here: **you must write the descriptions of the tool and its parameters carefully**, because that directly determines whether the AI can call the tool correctly.

```java
@Slf4j
public class InterviewQuestionTool {

    /**
     * 从面试鸭网站获取关键词相关的面试题列表
     *
     * @param keyword 搜索关键词（如"redis"、"java多线程"）
     * @return 面试题列表，若失败则返回错误信息
     */
    @Tool(name = "interviewQuestionSearch", value = """
            Retrieves relevant interview questions from mianshiya.com based on a keyword.
            Use this tool when the user asks for interview questions about specific technologies,
            programming concepts, or job-related topics. The input should be a clear search term.
            """
    )
    public String searchInterviewQuestions(@P(value = "the keyword to search") String keyword) {
        List<String> questions = new ArrayList<>();
        // 构建搜索URL（编码关键词以支持中文）
        String encodedKeyword = URLEncoder.encode(keyword, StandardCharsets.UTF_8);
        String url = "https://www.mianshiya.com/search/all?searchText=" + encodedKeyword;
        // 发送请求并解析页面
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
        // 提取面试题
        Elements questionElements = doc.select(".ant-table-cell > a");
        questionElements.forEach(el -> questions.add(el.text().trim()));
        return String.join("\n", questions);
    }
}
```

Bind the tool to the AI Service:

```java
// 构造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        .contentRetriever(contentRetriever) // RAG 检索增强生成
        .tools(new InterviewQuestionTool()) // 工具调用
        .build();
```

Write a unit test to verify the effect of the tool:

```java
@Test
void chatWithTools() {
    String result = aiCodeHelperService.chat("有哪些常见的计算机网络面试题？");
    System.out.println(result);
}
```

Run it in Debug mode and you’ll find that the AI called the tool:

![](https://pic.yupi.icu/1/1751964854933-395ecc9e-0fb6-4788-b8e2-ae5ef1d094a7.png)

The tool retrieved the list of questions:

![](https://pic.yupi.icu/1/1751964893075-84d0ac23-fe02-47c0-95c3-e422d1305448.png)

Through Debug you can also see that the AI Service loaded the tool:

![](https://pic.yupi.icu/1/1751964979312-65f04b40-9554-438b-83ff-025009f30a1c.png)

You can inspect the tool-calling process through conversation memory:

![](https://pic.yupi.icu/1/1751965074185-165ed1b9-a50f-4d21-ae85-b8c439f5065c.png)

And the output result is in line with expectations:

![](https://pic.yupi.icu/1/1751965104933-af4b3181-4dc0-40bb-9ef9-5e1c0e26b389.png)

Earlier, we only demonstrated the simplest way to define tools—the declarative approach. LangChain4j also provides a programmatic way to define tools, but I believe you won’t want to do that (unless you need to create tools dynamically).

![](https://pic.yupi.icu/1/1752045043475-a61743d1-e1ea-4912-bfac-d77ce6e43858.png)

Besides web search, there are many classic tools as well, such as file reading/writing, PDF generation, terminal invocation, chart output, and more. We can either develop these ourselves or use tools already developed by others directly through MCP.

### Model Context Protocol - MCP

MCP (Model Context Protocol) is an open standard whose purpose is to enhance interaction between AI and external systems. It provides a standardized way for AI to interact with external tools, resources, and services, allowing AI to access the latest data, execute complex operations, and integrate with existing systems.

You can think of MCP as the USB port of AI applications. Just as USB provides a standardized way for devices to connect to peripherals and accessories, MCP provides a standardized way for AI models to connect to different data sources and tools.

![](https://pic.yupi.icu/1/1752051649523-398e66d6-87fa-4cc4-8c9d-951939844405.png)

Simply put, through MCP, AI applications can easily access services provided by others to implement more functionality, such as querying locations, operating databases, deploying websites, or even handling payments.

We just used tool calling to implement interview-question search. Next, let’s use MCP to implement **searching content across the whole web**, which is a classic MCP use case.

First, search the MCP service marketplace for a Web Search service. I recommend [this one](https://mcp.so/server/zhipu-web-search/BigModel?tab=content), because it provides an SSE online invocation service, so we don’t need to install and start it locally ourselves.

![](https://pic.yupi.icu/1/1752045285371-fd70d350-80bd-4037-9b57-ff8d3a37ccf5.png)

But note that using someone else’s service may require an API Key, and it’s generally billed by usage.

You need to first obtain the API Key from the [official platform](https://www.bigmodel.cn/usercenter/proj-mgmt/apikeys), because we’ll need it later:

![](https://pic.yupi.icu/1/1752045399400-4e8fe95f-5d5c-47dc-aa6e-4225f2df23aa.png)

Then we need to use this MCP service in the program. One frustrating thing is that LangChain’s MCP support doesn’t feel very polished. The official docs don’t even mention which MCP dependency package to include. I had to find the dependency from the open-source repository myself:

![](https://pic.yupi.icu/1/1751967113982-099b0b9a-d5a3-43e0-bdf1-1ccfb8d093b2.png)

Add the dependency:

```xml
<!-- https://mvnrepository.com/artifact/dev.langchain4j/langchain4j-mcp -->
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-mcp</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

Add the API Key configuration to the config file:

```yaml
bigmodel:
  api-key: <Your Api Key>
```

Create `mcp.McpConfig`, follow the official development style, initialize communication with the MCP service, and create a Bean of `McpToolProvider`:

```java
@Configuration
public class McpConfig {

    @Value("${bigmodel.api-key}")
    private String apiKey;

    @Bean
    public McpToolProvider mcpToolProvider() {
        // 和 MCP 服务通讯
        McpTransport transport = new HttpMcpTransport.Builder()
                .sseUrl("https://open.bigmodel.cn/api/mcp/web_search/sse?Authorization=" + apiKey)
                .logRequests(true) // 开启日志，查看更多信息
                .logResponses(true)
                .build();
        // 创建 MCP 客户端
        McpClient mcpClient = new DefaultMcpClient.Builder()
                .key("yupiMcpClient")
                .transport(transport)
                .build();
        // 从 MCP 客户端获取工具
        McpToolProvider toolProvider = McpToolProvider.builder()
                .mcpClients(mcpClient)
                .build();
        return toolProvider;
    }
}
```

Note that above we’re calling MCP through SSE. If you start the MCP service locally through `npx` or `uvx`, you need to first install the corresponding tool and establish communication with a configuration like the following:

```java
McpTransport transport = new StdioMcpTransport.Builder()
    .command(List.of("/usr/bin/npm", "exec", "@modelcontextprotocol/server-everything@0.6.2"))
    .logEvents(true) // only if you want to see the traffic in the log
    .build();
```

Apply the MCP tool in the AI Service:

```java
@Resource
private McpToolProvider mcpToolProvider;

// 构造 AI Service
AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(qwenChatModel)
        .chatMemory(chatMemory)
        .contentRetriever(contentRetriever) // RAG 检索增强生成
        .tools(new InterviewQuestionTool()) // 工具调用
        .toolProvider(mcpToolProvider) // MCP 工具调用
        .build();
```

Write a unit test:

```java
@Test
void chatWithMcp() {
    String result = aiCodeHelperService.chat("什么是程序员鱼皮的编程导航？");
    System.out.println(result);
}
```

Run the unit test and inspect the logs. You’ll see the search process:

![](https://pic.yupi.icu/1/1751967601320-5242e432-ea07-4038-bc6f-7364aefe3d6a.png)

The MCP service takes effect and retrieves content from the web as part of the answer:

![](https://pic.yupi.icu/1/1751967705158-c4591073-858c-4584-a5ee-7d2ecb5261d6.png)

At present, the documentation doesn’t mention how to develop MCP with LangChain4j, but to be honest, I also don’t recommend using Java to develop MCP for now.

### Guardrails

Actually, I don’t think the term “guardrail” is very well named. It’s easier to just think of it as an interceptor. There are input guardrails and output guardrails, which can execute extra logic before sending a request to the AI or after receiving the AI’s response—for example, authenticating before calling AI or writing logs after receiving the result.

![](https://pic.yupi.icu/1/1752051765814-ca0a709d-216e-4f84-8a05-0a8b9a3a6b66.png)

Let’s try a simple example: perform sensitive-word detection before calling the AI. If the user’s prompt contains sensitive words, reject it directly.

Create `guardrail.SafeInputGuardrail` and implement the `InputGuardrail` interface:

```java
/**
 * 安全检测输入护轨
 */
public class SafeInputGuardrail implements InputGuardrail {

    private static final Set<String> sensitiveWords = Set.of("kill", "evil");

    /**
     * 检测用户输入是否安全
     */
    @Override
    public InputGuardrailResult validate(UserMessage userMessage) {
        // 获取用户输入并转换为小写以确保大小写不敏感
        String inputText = userMessage.singleText().toLowerCase();
        // 使用正则表达式分割输入文本为单词
        String[] words = inputText.split("\\W+");
        // 遍历所有单词，检查是否存在敏感词
        for (String word : words) {
            if (sensitiveWords.contains(word)) {
                return fatal("Sensitive word detected: " + word);
            }
        }
        return success();
    }
}
```

LangChain4j provides several quick-return methods. Put simply, return `success` if you want to continue calling AI; otherwise return `fatal`.

![](https://pic.yupi.icu/1/1751968291132-96a670ce-6551-4726-8c62-045021303af1.png)

Modify the AI Service to use the input guardrail:

```java
@InputGuardrails({SafeInputGuardrail.class})
public interface AiCodeHelperService {

    @SystemMessage(fromResource = "system-prompt.txt")
    String chat(String userMessage);

    @SystemMessage(fromResource = "system-prompt.txt")
    Report chatForReport(String userMessage);

    // 学习报告
    record Report(String name, List<String> suggestionList) {
    }
}
```

Write a unit test with a prompt that contains a sensitive word:

```java
@Test
void chatWithGuardrail() {
    String result = aiCodeHelperService.chat("kill the game");
    System.out.println(result);
}
```

Run it and inspect the effect. It triggers input detection and directly throws an exception:

![](https://pic.yupi.icu/1/1751968796339-ebf23753-55ad-4123-a4dc-e599859a28a1.png)

If the prompt doesn’t contain sensitive words, then it passes smoothly:

![](https://pic.yupi.icu/1/1751968877451-3ac9f488-0b78-4c04-a227-3c89b54847c8.png)

Of course, besides input guardrails, you can also write output guardrails to inspect the AI’s response.

### Logging and Observability

Earlier, we were inspecting runtime information through Debug. That’s not only inconvenient for debugging, but also unrealistic in production.

The official docs provide [logging](https://docs.langchain4j.dev/tutorials/logging) and [observability](https://docs.langchain4j.dev/tutorials/observability) to help us better debug programs and identify problems.

#### Logging

Enabling logging is very simple. You can either specify it directly when constructing the model or write Spring Boot configuration to support printing AI request and response logs.

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

But not every `ChatModel` supports this. For example, based on my testing, `QwenChatModel` does not. In that case, you have to place your hopes on observability.

#### Observability

You can get invocation information from `ChatModel` by writing a custom Listener, which is more flexible.

Create `listener.ChatModelListenerConfig` and output request, response, and error information:

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

But defining the Listener alone doesn’t seem to work for `QwenChatModel`, so we need to manually construct a customized `QwenChatModel`.

Create `model.QwenChatModelConfig`, construct the `ChatModel`, and bind the Listener:

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

Then you can change the original referenced `ChatModel` name to `myQwenChatModel` to avoid conflicts with the Spring Boot auto-wired one.

If you call the AI again, you’ll be able to see a lot more information:

![](https://pic.yupi.icu/1/1751974020940-84059541-3935-4505-b114-6fcc809b04f5.png)

### Turning AI into a Service

At this point, the AI capability is basically complete, but it currently only supports local execution. We need to write an interface for the frontend to call so the AI can become a service.

Most APIs we normally write are synchronous, meaning the backend processes everything first and only then returns the response. But for AI applications—especially chat applications with longer response times—that can easily make users lose patience. So I recommend using SSE (Server-Sent Events) to implement real-time streaming output similar to a typewriter effect, which can greatly improve user experience.

#### Developing an SSE Streaming API

LangChain provides 2 ways to support streaming responses (note that streaming responses do not support structured output).

One way is to use [TokenStream](https://docs.langchain4j.dev/tutorials/ai-services#streaming): have the AI conversation method return `TokenStream`, and specify a streaming chat model `StreamingChatModel` when creating the AI Service:

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

Personally, I prefer the other method—[using Flux](https://docs.langchain4j.dev/tutorials/ai-services/#flux) instead of `TokenStream`. Anyone familiar with reactive programming should already know `Flux`, right? You only need the AI conversation method to return a reactive `Flux` object. Example code:

```java
interface Assistant {

  Flux<String> chat(String message);
}
```

Let’s try it. First, we need to introduce the reactive dependency package:

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-reactor</artifactId>
    <version>1.1.0-beta7</version>
</dependency>
```

Then add a streaming conversation method to the AI Service. While we’re at it, let’s also support multi-user conversation memory:

```java
// 流式对话
Flux<String> chatStream(@MemoryId int memoryId, @UserMessage String userMessage);
```

Since we need to use a streaming model, add the streaming model configuration:

```yaml
langchain4j:
  community:
    dashscope:
      streaming-chat-model:
        model-name: qwen-max
        api-key: <Your Api Key>
```

When constructing the AI Service, specify the streaming chat model (auto-wiring is enough), and also add a conversation-memory provider:

```java
@Resource
private StreamingChatModel qwenStreamingChatModel;

AiCodeHelperService aiCodeHelperService = AiServices.builder(AiCodeHelperService.class)
        .chatModel(myQwenChatModel)
        .streamingChatModel(qwenStreamingChatModel)
        .chatMemory(chatMemory)
        .chatMemoryProvider(memoryId ->
                MessageWindowChatMemory.withMaxMessages(10)) // 每个会话独立存储
        .contentRetriever(contentRetriever) // RAG 检索增强生成
        .tools(new InterviewQuestionTool()) // 工具调用
        .toolProvider(mcpToolProvider) // MCP 工具调用
        .build();
```

Finally, write the Controller interface. For easier testing, we’ll use a GET request here:

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

Add the server configuration to specify the backend port and API path prefix:

```yaml
server:
  port: 8081
  servlet:
    context-path: /api
```

Start the server and test it with CURL:

```bash
curl -G 'http://localhost:8081/api/ai/chat' \
  --data-urlencode 'message=我是程序员鱼皮' \
  --data-urlencode 'memoryId=1'
```

You’ll be able to see the streaming output result:

![](https://pic.yupi.icu/1/1751975773168-c4ddd770-abd7-4555-90b6-8d487630aee4.png)

#### Enable CORS Support in the Backend

To let the frontend project call the backend API smoothly, we need to configure cross-origin support on the backend. Create a cross-origin config class under the `config` package with the following code:

```java
/**
 * 全局跨域配置
 */
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        // 覆盖所有请求
        registry.addMapping("/**")
                // 允许发送 Cookie
                .allowCredentials(true)
                // 放行哪些域名（必须用 patterns，否则 * 会和 allowCredentials 冲突）
                .allowedOriginPatterns("*")
                .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS")
                .allowedHeaders("*")
                .exposedHeaders("*");
    }
}
```

Note that if `.allowedOrigins("*")` and `.allowCredentials(true)` are configured at the same time, it will cause a conflict, because for security reasons, cross-origin requests cannot both allow all origins and also allow sending authentication information (such as Cookies).

## AI-Generated Frontend

Because this project doesn’t need very complex pages, we can use AI to quickly generate the frontend code and significantly improve development efficiency. Here, Yupi uses the [mainstream AI development tool Cursor](https://www.cursor.com/) and challenges himself to build the frontend project without writing a single line of code.

### Prompt

First prepare a detailed Prompt. It should generally include the requirements, technology selection, and backend API information. You can also provide prototype diagrams, backend code, and so on.

```markdown
你是一位专业的前端开发，请帮我根据下列信息来生成对应的前端项目代码。

## 需求

应用为《AI 编程小助手》，帮助用户解答编程学习和求职面试相关的问题，并给出建议。

只有一个页面，就是主页：页面风格为聊天室，上方是聊天记录（用户信息在右边，AI 信息在左边），下方是输入框，进入页面后自动生成一个聊天室 id，用于区分不同的会话。通过 SSE 的方式调用 chat 接口，实时显示对话内容。

## 技术选型

1. Vue3 项目
2. Axios 请求库

## 后端接口信息

接口地址前缀：http://localhost:8081/api

## SpringBoot 后端接口代码

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

Note that if you’re using Windows, it’s best to add something like “you should use Windows-supported commands to complete the task” into the prompt.

### Development

Create a new frontend project folder called `ai-code-helper-frontend` under the project root, open that directory with Cursor, and execute the Prompt. Be sure to choose Agent mode and a Thinking/deep-thinking model (Claude is recommended):

![](https://pic.yupi.icu/1/1751976145149-beefc903-31e1-4a4f-8bbe-edf41a3a4806.png)

Besides the source code, in my case Yupi even had it generate the project intro doc `README.md`, which really feels great!

![](https://pic.yupi.icu/1/1752025773338-e87a94c7-db0b-4213-9cc8-f643b14f5182.png)

After the code is generated, open the terminal and run `npm run dev`, or open the `package.json` file and start the project using the Debug button:

![](https://pic.yupi.icu/1/1752026474929-cd4a7225-1e48-4e95-a08e-6f69ea256d45.png)

### View the Result

After running the frontend project, first verify that the functionality works, then verify the styling. If you find that the functionality is broken (for example, there’s no response after sending a message), you can press F12 to open the browser console and inspect frontend error information, or check the backend project’s console for errors. Analyze the specific error based on the specific error message. At this point, some frontend-related knowledge is involved, so if you’re not familiar with frontend development, ask AI as much as possible and let it help you fix the bug. **And if you truly can’t get it working, don’t blindly keep messing with it!** Just use Yupi’s code.

For example, I ran into an error when connecting to the backend SSE service, so I directly copied the error message to the AI and let it solve it:

![](https://pic.yupi.icu/1/1752025968566-ab2c2d53-59e4-4519-bf55-e07b095f1e5d.png)

It ran successfully. Let’s look at the result:

![](https://pic.yupi.icu/1/1752026740589-5b4670c8-3f5c-470e-afba-4cfd469c31ee.png)

![](https://pic.yupi.icu/1/1752026767000-6599f85f-5926-4174-a06e-55e30e4df667.png)

After confirming that both functionality and style are fine, remember to commit the code first (to prevent later AI-generated code from polluting it). Then you can add more features as needed, such as rendering AI responses with Markdown.

![](https://pic.yupi.icu/1/1752027043776-cd6d17ed-175f-4c7e-8b25-aee81a5296b2-20250710114303496.png)

## Summary

OK, that’s the full hands-on LangChain4j project tutorial. So, how was it—did everyone learn it, or did everyone just get wrecked by it?

Back to the question at the beginning: **how should you choose an AI development framework in real development?**

Take Spring AI and LangChain4j as examples. Which one do you personally prefer? As for me, I actually prefer Spring AI’s development model. Spring AI currently supports more capabilities, and with the backing of a giant like Spring AI Alibaba in China, its ecosystem is stronger and problems are easier to solve. LangChain4j’s strength is that it can be used independently of Spring projects, making it a bit more flexible and free.

But the key point is that you only really need to learn one of these frameworks in depth, because many concepts and usage patterns are shared across them:

![](https://pic.yupi.icu/1/1752050425995-3b2b8cf4-ad48-41ec-a1e5-154ae6cd8526.png)

## Recommended Resources

1) Yupi's AI navigation site: [AI resource collection, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning circle: [Learning paths, programming tutorials, hands-on projects, career guides, Q&A](https://www.codefather.cn)

3) Programmer interview cheatsheet: [Internship/campus/social recruitment key points, enterprise question analysis](https://www.mianshiya.com)

4) Programmer resume tool: [Professional templates, rich examples, direct to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [Essential for internship/campus/social recruitment interviews to get offers](https://ai.mianshiya.com)
