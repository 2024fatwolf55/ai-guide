# AI 程式設計時代，哪些技術必須要了解？

用 AI 程式設計做專案的時候，你一定會遇到各種沒見過的技術名詞。

比如 AI 跟你說：用 Next.js 搭前端，Prisma 連資料庫，部署到 Vercel。

你一臉問號：這都是啥？算了，讓 AI 幹就完了，我不用管……

![](https://pic.yupi.icu/1/%E5%95%A5%E5%95%A5%E5%95%A5%E8%A1%A8%E6%83%85%E5%8C%85.jpg)

但問題是，如果你對這些技術完全沒概念，跟 AI 溝通時就說不清楚自己想要什麼，AI 選錯了方向你也判斷不出來。

我之前做專案就遇到過，AI 給我用了一個很冷門的資料庫方案，我不瞭解就直接用了，結果後面想加功能的時候發現生態太差，很多東西沒有現成方案，只能推翻重來。

所以我寫了這篇文章，幫你把 AI 程式設計時代最核心的技術梳理一遍。你不需要深入學習每一個技術，但至少要知道它們是幹嘛的？什麼時候該用？做技術選型的時候心裡有數就行。



## 一、程式語言

首先，你必須瞭解 AI 程式設計中最常用的 2 套程式語言。

#### 1、JavaScript / TypeScript

JavaScript 最早是給瀏覽器用的語言，負責網頁上的各種互動效果。後來 Node.js 的出現讓它也能跑在伺服器上寫後端，於是 JS 變成了前後端通吃的全棧語言。

![](https://pic.yupi.icu/1/article-images/tech-stack/01_JavaScript%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80_compressed_v3.png)

TypeScript 是 JavaScript 的增強版，給每個變數都標註了型別，寫程式碼時編輯器就能幫你檢查錯誤。

現在 AI 生成程式碼預設就會優先用 TypeScript，因為有了型別資訊後，AI 理解程式碼的上下文更準確，生成的程式碼質量也更高。

如果你想做網站相關的專案，JS/TS 幾乎是繫結的。

![](https://pic.yupi.icu/1/article-images/tech-stack/02_TypeScript%E7%B1%BB%E5%9E%8B%E7%B3%BB%E7%BB%9F%E5%A2%9E%E5%BC%BA_compressed_v3.png)



#### 2、Python

Python 的語法接近英語，讀起來像虛擬碼一樣直觀，所以很多零基礎的同學第一門語言就學 Python。

它在 AI、機器學習、資料分析、自動化指令碼這些領域有統治級的地位，大量 AI 框架和工具都是用 Python 寫的。

如果你要做 AI 應用開發、資料處理、爬蟲這些事情，Python 是非常好的選擇。

![](https://pic.yupi.icu/1/article-images/tech-stack/03_Python%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80_compressed_v2.png)

簡單來說，做網站選 JS / TS，做 AI 應用選 Python，兩者都會就更好了。



## 二、前端三件套

前端就是使用者能看到和互動的部分，也就是你在瀏覽器裡看到的一切。

AI 程式設計中，前端是最容易搞定的部分，因為改完程式碼重新整理一下就能看到效果。

傳統的前端三件套是 HTML + CSS + JavaScript，但是 AI 時代，我願稱 React + Next.js + Tailwind CSS 為全新的前端三件套，因為這是 AI 程式設計工具最愛用的前端組合。

#### 1、React

React 是 Meta 開發的前端框架，核心理念是把頁面拆分成一個個可複用的元件。

比如一個按鈕是一個元件，一個導航欄也是一個元件，像搭積木一樣拼起來就是一個完整的頁面。

根據開發者調查資料，React 的使用率超過了 80%，是全球最主流的前端框架。AI 訓練資料中 React 程式碼量最大，所以 AI 生成 React 程式碼的質量也是最高的。我們團隊的產品基本都是用 React 開發的。

![](https://pic.yupi.icu/1/article-images/tech-stack/07_React%E5%89%8D%E7%AB%AF%E6%A1%86%E6%9E%B6_compressed_v1.png)



#### 2、Next.js

Next.js 是基於 React 的全棧框架，由 Vercel 公司開發。

它的厲害之處在於不僅能寫前端頁面，還能在同一個專案裡寫後端介面，真正實現了一個專案搞定前後端。而且它支援服務端渲染，對搜尋引擎收錄非常友好。

很多 AI 零程式碼平臺生成的專案預設就是 Next.js。你在 app 目錄下建立一個資料夾就自動對應一個頁面路徑，後端介面寫在 app/api 目錄下，前後端程式碼能放在同一個專案裡，但邏輯上是分開的。

而且能夠輕鬆部署到 Vercel 平臺，只需要把程式碼推到 GitHub，連線倉庫後每次推送自動構建上線，非常省事。

![](https://pic.yupi.icu/1/article-images/tech-stack/09_Next.js%E5%85%A8%E6%A0%88%E6%A1%86%E6%9E%B6_compressed_v1.png)



#### 3、Tailwind CSS

Tailwind CSS 是一個原子化的樣式框架。

傳統開發網頁是先寫 HTML 結構，然後再寫 CSS 檔案定義樣式。而 Tailwind 的思路不同，它把常用樣式都變成了一個個小 class 名，直接在 HTML 裡拼就行。比如想讓一個元素水平垂直居中，寫 `flex justify-center items-center` 就搞定了。

剛開始你可能會覺得 class 名一大串有點醜，但用習慣之後真的回不去了。

AI 生成的前端程式碼預設就很喜歡用 Tailwind，因為它不需要額外維護 CSS 檔案，而且每個樣式類名只有一種寫法，AI 生成的準確率特別高。

![](https://pic.yupi.icu/1/article-images/tech-stack/11_Tailwind_CSS%E5%8E%9F%E5%AD%90%E5%8C%96%E6%A1%86%E6%9E%B6_compressed_v1.png)

不過你可能也注意到了，AI 生成的頁面經常是藍紫色漸變的配色，就是因為 Tailwind 的預設色板有藍色和紫色，AI 用起來特別順手，導致做出來的東西千篇一律…… 想避免這個問題，記得在提示詞裡明確你想要的配色風格。

React + Next.js + Tailwind CSS 這三個技術為什麼總是繫結出現呢？

因為 AI 模型是從網際網路上的大量程式碼中學習的，React、Next.js、Tailwind CSS 恰好是這幾年開源專案用得最多的組合，AI 對它們最熟悉，生成的程式碼最靠譜。這形成了一個飛輪效應，AI 越推薦，用的人越多，訓練資料越多，AI 就更推薦。



## 三、後端框架

後端是使用者看不見的部分，負責處理業務邏輯、儲存資料、管理使用者身份。

當你在網站上點選「註冊」按鈕，前端會把你填的資訊發給後端，後端負責校驗資料、存到資料庫、返回結果。

如果你用 Next.js，其實後端介面可以直接寫在同一個專案裡，不需要單獨搞一個後端專案。但如果你需要更獨立、更強大的後端服務，就得選一個後端框架了。



#### 1、Spring Boot

Spring Boot 是 Java 後端開發的標配框架，國內大部分企業的後端系統都是用它寫的。

它的理念是「約定大於配置」，幫你把各種繁瑣的配置都簡化了，開箱即用。

如果你學 AI 程式設計的同時也想提升後端就業競爭力，Spring Boot 是必學的。而且 Spring AI 框架的推出，讓 Java 程式設計師也能很方便地開發 AI 應用了。

![](https://pic.yupi.icu/1/article-images/tech-stack/24_Spring_Boot%E6%A1%86%E6%9E%B6_compressed_v2.png)



#### 2、FastAPI

FastAPI 是 Python 生態中增長最快的後端框架，目前已經有接近 40% 的 Python 開發者在使用。它天生支援非同步和型別檢查，寫完介面文件就自動生成了，不需要額外維護。

FastAPI 最爽的一點是，啟動後訪問 /docs 路徑就能看到一個互動式的介面文件頁面，可以直接在瀏覽器裡測試介面。如果你用 AI 生成 Python 後端專案，大機率就是 FastAPI。

![](https://pic.yupi.icu/1/article-images/tech-stack/25_FastAPI%E6%A1%86%E6%9E%B6_compressed_v1.png)

簡單來說，Java 方向選 Spring Boot，Python 方向選 FastAPI，想省事用 Next.js 的 API Routes 前後端一把梭。



## 四、資料儲存

網站上的使用者資訊、文章內容、訂單記錄等需要多次查詢的資料，都需要存在資料庫裡。

#### 1、MySQL / PostgreSQL

關係型資料庫就像 Excel 表格一樣，資料有行有列，資料之間可以建立關聯。

![](https://pic.yupi.icu/1/1769046133583-18e6b389-b3b7-4c56-b5f3-7482a3897bd3.png)

MySQL 和 PostgreSQL 是最主流的兩個關係型資料庫，都是開源免費的。

![](https://pic.yupi.icu/1/1769046291097-2dea6cb4-76e5-45ef-8799-e187324eee46.png)

MySQL 在國內用得最廣，遇到問題基本都能搜到解決方案。PostgreSQL 功能更強大，支援 JSON 資料型別、地理資訊、全文搜尋，還能透過 pgvector 外掛支援向量搜尋，適合開發 AI 應用，很多海外的 SaaS 產品和 AI 專案都在用 PostgreSQL。

順帶一提，在程式碼中運算元據庫一般不直接寫 SQL 語句，而是透過 ORM 工具來操作。比如 Node.js 專案常用 Prisma，Java 專案常用 MyBatis-Plus，Python 專案常用 SQLAlchemy。有了 ORM，你在程式碼裡運算元據就像操作普通物件一樣方便。



#### 2、Supabase

如果你不想自己維護資料庫，還有一個省事的選擇。

Supabase 是一個開源的後端即服務平臺，底層基於 PostgreSQL，提供了資料庫、使用者認證、檔案儲存、實時訂閱等功能。

註冊個賬號就能用，免費額度夠個人專案折騰了。

你可以跟 AI 說「用 Supabase 做資料庫和認證」，AI 就能幫你生成完整的整合程式碼。

![](https://pic.yupi.icu/1/article-images/tech-stack/36_Supabase%E5%90%8E%E7%AB%AF%E6%9C%8D%E5%8A%A1_compressed_v1.png)



## 五、部署上線

程式碼寫完了，怎麼讓全世界的人都能訪問到你的網站呢？

這就需要把程式碼部署到伺服器上。

#### 1、Vercel

最省事的方式是用 Vercel 平臺。

它是 Next.js 框架背後的公司，對 Next.js 專案的支援最好。你只需要把程式碼推送到 GitHub，Vercel 會自動幫你構建和部署，幾分鐘就能上線，還自帶 HTTPS 和 CDN 加速。免費額度對個人專案完全夠用，非常適合部署 AI 程式設計做出來的小專案。

![](https://pic.yupi.icu/1/article-images/tech-stack/44_Vercel%E9%83%A8%E7%BD%B2%E5%B9%B3%E5%8F%B0_compressed_v3.png)



#### 2、Linux 雲伺服器

不過 Vercel 的伺服器在海外，而且它更適合前端和全棧專案。如果你要做面向國內使用者的商業產品，或者後端是一個獨立的 Java / Python 服務，就需要自己買 Linux 雲伺服器了。

國內的雲服務商可以選阿里雲、騰訊雲等等，新使用者一般有免費試用或大額優惠，買一臺 2 核 4G 的配置就夠個人專案用了。

伺服器的作業系統基本都是 Linux，所以瞭解一些基本的 Linux 命令是有必要的，比如 cd 進目錄、ls 看檔案這些。不過大部分操作都可以讓 AI 幫你生成命令，不用死記。



#### 3、Docker

Docker 可以把你的程式碼、執行環境、依賴庫全部打包成一個「容器」，不管在什麼機器上執行，效果都一樣。

以前經常會遇到「在自己電腦上能跑，到伺服器上就報錯」的情況，用了 Docker 就不存在這個問題了。

把應用封裝為 Docker 很簡單，讓 AI 幫你寫 Dockerfile 配置檔案就行，不需要自己記 Docker 檔案的寫法。

![](https://pic.yupi.icu/1/article-images/tech-stack/46_Docker%E5%AE%B9%E5%99%A8%E5%8C%96_compressed_v2.png)

如果你的專案涉及多個服務，比如前端 + 後端 + 資料庫，還可以用 docker-compose 一鍵啟動所有服務。



## 六、程式碼管理

#### 1、Git

用 AI 程式設計做專案時，建議用 Git 來管理程式碼。比如讓 AI 改程式碼之前先提交一版，萬一改崩了還能回退。這就像遊戲裡的存檔，打 Boss 之前先存個檔，死了能重來。

你不需要死記 Git 命令，因為 AI 可以幫你執行 Git 操作。但幾個核心概念要知道，比如 commit 是儲存一個版本，branch 是建立一個分支，push 是把程式碼推送到遠端倉庫。

![](https://pic.yupi.icu/1/07_Git%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86%E5%90%8E%E6%82%94%E8%8D%AF_compressed_v3.png)



#### 2、GitHub

GitHub 是全球最大的程式碼託管平臺，也是曾經大家玩梗說的程式設計師社交平臺。上面有海量的開源專案，是程式設計學習資源的寶庫。

你可以把程式碼推送到 GitHub 上，便於備份、分享和協作。前面說的 Vercel 部署，就是連線你的 GitHub 倉庫來實現自動上線的。

![](https://pic.yupi.icu/1/article-images/tech-stack/71_GitHub%E4%BB%A3%E7%A0%81%E6%89%98%E7%AE%A1%E5%B9%B3%E5%8F%B0_compressed_v1.png)



## 七、呼叫 AI 大模型

藉助 AI 程式設計 + AI 大模型服務，你可以輕鬆開發出自己的 AI 應用，比如做一個 AI 客服、AI 寫作助手、AI 資料分析工具。

要做這些事情，首先得知道怎麼在程式碼裡呼叫大模型。



#### 1、OpenAI API

OpenAI API 是目前最通用的大模型呼叫方式。

OpenAI 提供了一套標準的 API，你可以用它來實現對話、文字生成、程式碼生成、圖片生成等功能。可以在程式碼中安裝對應語言的 SDK，然後用 API Key 初始化客戶端後就能呼叫模型了。

很多其他 AI 服務商的 API 也相容 OpenAI 的介面格式，比如 DeepSeek、通義千問等。所以學會呼叫 OpenAI API 後，切換到其他模型也很方便。

![](https://pic.yupi.icu/1/article-images/tech-stack/72_OpenAI_API%E8%B0%83%E7%94%A8GPT%E5%A4%A7%E6%A8%A1%E5%9E%8B_compressed_v2.png)

如果你想在一個專案中靈活切換不同的模型，還可以用 OpenRouter 這樣的統一介面服務，一個 Key 就能呼叫上百種大模型。



#### 2、LangChain

學會基本的呼叫大模型之後，如果你想做更復雜的 AI 應用，比如讓 AI 自主使用工具、編排多步驟的工作流，就需要 AI 應用開發框架了。

LangChain 可以說是最流行的 AI 應用開發框架，你可以把它理解成 AI 應用開發的「積木」，它內建了大量的整合元件，比如對接各種大模型、向量資料庫、工具呼叫等。對於快速搭建 AI 應用原型來說，LangChain 能幫你省下大量的樣板程式碼。

不過有一點要注意，LangChain 更適合原型開發和複雜的多模型編排場景。如果你的應用比較簡單，直接用 OpenAI 或者各家大模型的 SDK 會更輕量。

![](https://pic.yupi.icu/1/article-images/tech-stack/76_LangChain_AI%E5%BA%94%E7%94%A8%E5%BC%80%E5%8F%91%E6%A1%86%E6%9E%B6_compressed_v1.png)



## 八、向量資料庫和 RAG

做 AI 應用時，經常遇到一個問題：大模型的知識是有截止日期的，而且缺乏你自己的私有知識。

比如你想讓 AI 基於公司內部文件回答員工的提問，直接問大模型肯定答不上來。

這時候就需要 RAG 技術了。

RAG 的全稱是 Retrieval-Augmented Generation 檢索增強生成，核心思想就是 **先搜再答**，讓大模型在回答之前先去搜一遍相關資料，再基於搜到的知識來組織答案。就跟開卷考試差不多，遇到不會的先翻翻書。

![](https://pic.yupi.icu/1/1776332850706-68cb05fe-7022-445c-9c3d-944f74f48dee.png)

但怎麼搜到相關的資料呢？

如果用關鍵詞匹配，很容易出現問題和文件裡的用詞不一致的情況。所以需要用到 **向量** 的概念。

簡單來說，向量就是把一段文字用一串數字來表示，讓計算機可以比較語義上的相似度。負責把文字轉成向量的模型叫 Embedding 模型，儲存這些向量並支援快速相似度搜尋的資料庫就是向量資料庫。

![](https://pic.yupi.icu/1/1769046928023-6111fd54-4926-4ef0-b67b-e10f3af57d52.png)

RAG 的做法其實就 2 步。

1）把你的文件切成小塊，轉成向量存進向量資料庫。

2）使用者提問時，把問題也轉成向量，去向量庫裡搜最相似的幾個文件塊，再把這些塊連同使用者問題一起交給大模型生成回答。

![](https://pic.yupi.icu/1/1776650476421-3bfb3c26-575d-4cc4-9538-f74a4589b42d.png)

在 AI 時代，向量資料庫的應用越來越廣，做 AI 知識庫、語義搜尋、推薦系統都需要用到它。主流的向量資料庫有 Milvus、Chroma、Qdrant 這些，PostgreSQL 也可以透過 pgvector 外掛支援向量搜尋。

![](https://pic.yupi.icu/1/1769047066536-0ef08cd3-b86b-4c97-9016-7add32a710b8.png)

如果想深入瞭解 RAG 的各種進階方案，我之前寫過一篇 [從 Naive RAG 到 Agentic RAG 的全景科普文章](https://mp.weixin.qq.com/s/r_HwTfIyShV5Ke0UY6b-4g)，感興趣可以去看看。



## 寫在最後

本文是 AI 程式設計技術棧的精簡版介紹。魚皮的[《小白都能學的 AI 程式設計實戰》影片課](https://ai.codefather.cn/course/2087008226460565505)中配套了完整版的《AI 程式設計技術棧速查手冊》，覆蓋了更多技術的詳細講解，遇到新技術一查就懂。

我把 AI 程式設計時代最核心的技術給大家梳理了一遍，從程式語言到前後端框架，從資料庫到部署上線，從 AI 大模型呼叫到 RAG 知識庫。

有了 AI 輔助程式設計，很多技術你不需要深入學習，只要知道它是什麼、什麼時候該用，AI 就能幫你搞定具體的程式碼實現。

**技術是為產品服務的，別為了學技術而學技術。**

不過如果你想找程式設計師相關的工作，還是要系統學習這些技術的，但也不用面面俱到。實際做專案的過程中，遇到什麼學什麼，用到什麼查什麼，加油！
