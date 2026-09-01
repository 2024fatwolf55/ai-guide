# Cursor + Cordova - 表情包生成器 APP 專案實戰

本專案將帶你用純 Vibe Coding 的方式，一行程式碼都不寫，開發一個可以在手機上執行的 APP。

這是一個典型的 Vibe Coding 專案，魚皮會講解如何用 AI 生成網頁、然後透過工具打包成 APP。重點在於學習 Cordova 工具的使用和 APP 打包流程，適合想快速做出 APP 的同學。



---



你現在看到的 APP，是我完全用 AI 生成的，一行程式碼都沒寫！怎麼做到的呢？

![](https://pic.yupi.icu/1/image-20250612190219936.png)

大家好，我是程式設計師魚皮。AI 發展很快，現在隨隨便便就能生成一個網站，但是怎麼純用 AI 開發能在手機上執行的 APP 呢？網上基本上沒有完整的教程。所以，我出手了，下面只用幾分鐘的時間，我會教大家如何利用 AI 生成 APP，依然是 **保姆級教程**。

⭐️ 本文對應影片，推薦觀看：[https://bilibili.com/video/BV17HMcziEye](https://www.bilibili.com/video/BV17HMcziEye/)



下面有請我們的主角 `Cordova`！

## 一、什麼是 Cordova？

Apache Cordova 是一個開源的移動應用開發框架，允許開發者使用 HTML、CSS 和 JavaScript 等 Web 技術開發 **跨平臺** 的移動應用。它透過將 Web 技術封裝在本地容器中，使得開發者可以編寫一次程式碼，然後在 Android、iOS、Windows 等多個平臺上執行。

![](https://pic.yupi.icu/1/1749628169384-9f90fa60-e328-46c8-99eb-6f4f343b8aeb.png)

Cordova 主要基於以下幾個核心元件實現，感興趣的同學可以瞭解一下：

![](https://pic.yupi.icu/1/image-20250612190256834.png)

也就是說，想要開發 APP，我們只需要把網站檔案交給 Cordova，根據需要裝一裝外掛、改一改配置，然後直接使用它提供的構建工具就能將 Web 應用打包成原生 APP 應用了（比如 APK 檔案）！幾乎不涉及任何程式碼編寫和開發。

聽起來很簡單，有手就行？但是想使用 Cordova 開發 APP，必須要在電腦上安裝對應的環境，比如 Android 和 IOS，而安裝環境的難度可以說是 **非常炸裂** 了！

如果你自己折騰，可能至少要花個幾天的時間，會踩很多坑，到網上搜各種方案還不一定能搞定。所以我才做了這個教程，該踩的坑我都幫大家踩完了，會 **用最短的時間帶你搞定環境，並且教你如何使用 AI + Cordova 生成 APP**。開始之前記得 **點贊收藏三連** 哦，拜託，我的頭髮真的不多啦！

![](https://pic.yupi.icu/1/1749628109290-90dc8199-664a-4994-8dfe-716b4f8b5b71.png)

## 二、環境準備

### 安裝 Cordova

首先我們要安裝 Cordova。Cordova 的執行依賴 Node.js 和 NPM 前端工具，到 [Node.js 官網](https://nodejs.org/zh-cn) 下載即可，會自動安裝 NPM。

![](https://pic.yupi.icu/1/1749628757935-a1f29765-c0e8-4c3a-9486-e113f3814e8d.png)

可以把 NPM 理解為快速安裝各種軟體的小工具，安裝完成後開啟終端，執行下列命令安裝 Cordova：

```bash
npm install -g cordova
```

Cordova 支援將網站打包為 Android 和 IOS 移動端、Electron 桌面端應用。下面魚皮帶大家安裝我個人認為難度最大的 **Android 環境**。注意，接下來的每一步，操作其實都不難，但是一定要仔細看！一個細節不注意可能就報錯了！



### 安裝 Android 環境

首先，我們要根據 Cordova 的版本來確定所需環境和工具的版本，由於我們安裝的 Cordova 是最新版本的，因此直接閱讀 [最新的官方文件](https://cordova.apache.org/docs/en/dev/guide/platforms/android/index.html) 即可，比如我這裡需要的依賴如下：

![](https://pic.yupi.icu/1/1749470136150-38d5fe30-e3e3-4994-8c06-ada90cc3deb7.png)

其中，最重要的是：

- Java 17
- Gradle 8.13
- Android API 級別 >= 24

下面我們分別安裝這些依賴。



#### 1、安裝 Java

Java 版本必須是 17，最好找個現成的 [Windows 系統的 Java 安裝包](https://www.azul.com/downloads/?version=java-17-lts&os=windows&package=jdk#zulu)：

![](https://pic.yupi.icu/1/1749629753199-b8458627-2a44-4d5b-8786-74bc1d5b83bc.png)

安裝 Java 時建議選擇 **自動配置環境變數**（包括 Path 和 JAVA_HOME），就不用自己手動配置環境變數了。

![](https://pic.yupi.icu/1/1748604000379-99f42d77-7198-4c44-989c-914f21175452.png)

安裝完成後，開啟終端執行 `java -version` 命令檢視版本號，看到下列輸出表示成功：

![](https://pic.yupi.icu/1/1748604045327-9e78c03d-dff8-4823-a6f8-221b1c288b77.png)

如果無法執行命令，大機率是沒有配置 Path 環境變數。

![](https://pic.yupi.icu/1/1749715203575-d424aa3d-9be3-4e55-936e-8c99211a10a9.png)



#### 2、安裝 Gradle

根據上面的版本號，Gradle 必須是 8.13，直接到 [官網](https://gradle.org/releases/) 下載二進位制壓縮包即可。

![](https://pic.yupi.icu/1/1749470207621-4d12c5fa-6849-49eb-807a-46512cbd7011.png)

解壓下載完成的壓縮包，移動到 **不包含中文的路徑** 中，然後配置環境變數，包括 Path 和 GRADLE_HOME：

![](https://pic.yupi.icu/1/1749470552544-1d872d78-933d-404e-a5d3-95071f98f72c.png)

![](https://pic.yupi.icu/1/1749471051766-77ad3676-a1f4-449a-9c6c-3db9adaf5484.png)

開啟終端執行 `gradle -v` 命令，檢視版本號：

![](https://pic.yupi.icu/1/1749470606188-7af15756-34de-4f77-b469-6b88afc5e6bd.png)

如果命令無法執行，大機率是 Path 環境變數配置錯誤。



#### 3、安裝 Android

建議直接安裝 Android 開發工具 [Android Studio](https://developer.android.com/studio?hl=zh-cn)，會自動安裝 Android 的開發 SDK 和執行環境。

到官網下載 Android studio，執行安裝包，按照步驟安裝即可：

![](https://pic.yupi.icu/1/1748600319317-775ad570-b84d-441e-9538-3f654e0c0280.png)

安裝完成後，第一次開啟 Android Studio 時，會提醒你安裝 Android SDK 環境：

![](https://pic.yupi.icu/1/1748600394690-c64893b5-28f2-439e-afc2-302b616c2cb6.png)

注意不要把 SDK 元件安裝到包含中文的目錄下，好在安裝包也給了限制，不然又得栽倒一片人。。。

![](https://pic.yupi.icu/1/1748601041213-24016b9f-a6ce-4e8e-afba-a412cdee7dab.png)

接下來無腦安裝即可，會自動安裝各種 Android 開發常用的工具、還有安卓裝置模擬器：

![](https://pic.yupi.icu/1/1748601061577-19061773-bea7-4f90-8fd4-588a99049611.png)

這一步可能會有點煎熬，有些地區的朋友可能需要一些特殊的網路支援，你懂的。

![](https://pic.yupi.icu/1/1748601238964-92c8754e-7c98-4c5d-9b4d-d1a1ede316ed.png)

![](https://pic.yupi.icu/1/1748601268568-8e5e99b1-0792-49f3-9bd1-d8073282743a.png)

經過了漫長的等待，Android SDK 終於安裝完成，然後需要配置 Android 的環境變數 ANDROID_HOME：

![](https://pic.yupi.icu/1/1749469684248-b1c77491-ca2b-49bd-a4e4-fffcef962868.png)

還要配置 platform-tools 到 Path 中，裡面有一些命令列工具：

![](https://pic.yupi.icu/1/1749469743427-c052d689-2746-4522-a37d-4ba5513cf857.png)



配置完成後，我們開啟 Android Studio，右上角進入 SDK Manager 的設定，根據 Cordova 的版本號要求，安裝對應 API Level 的 SDK，比如我這裡安裝了 34 和 35 版本。

![](https://pic.yupi.icu/1/1748604140186-2cfeee7a-5cce-4647-8dc6-98afc4c7e980.png)

這一步可能也會比較慢，耐心等待安裝吧~

![](https://pic.yupi.icu/1/1748604151163-82381d25-9824-446c-b418-54e758de9a5f.png)

安裝完 SDK 後，再進入 SDK 工具選項，安裝 Command-line Tools 命令列工具，之後在電腦上執行安卓 apk 包時可能會用到：

![](https://pic.yupi.icu/1/1749607562141-66bfc793-a918-4359-b574-a8d52bc250a1.png)

同樣，把 Command-line Tools 新增到環境變數 Path 中，路徑為 `%ANDROID_HOME%\cmdline-tools\latest\bin`，這樣一來，很多工具可以直接在終端中使用了，比如 apkanalyzer。

![](https://pic.yupi.icu/1/1749607796266-a0dbb7b1-62ab-4b43-abcb-796b7261d45a.png)



#### 4、安裝 Android 裝置模擬器

下面我們要嘗試在自己的電腦上執行 Android 手機模擬器，這樣除錯程式更方便。

開啟 Android Studio 的裝置管理器，新增一個新裝置：

![](https://pic.yupi.icu/1/1749609766461-16befd69-65e1-4c07-bb6a-7e5ee2500dc4.png)

選擇指定機型，建議選擇 API 版本高一點的，我這裡選擇 Pixel 7：

![](https://pic.yupi.icu/1/1749610449536-edf49ed9-852c-425f-b3a0-a7e7bcc95d90.png)

安裝推薦的系統映象：

![](https://pic.yupi.icu/1/1749609929190-ad696301-b3d1-4642-98b1-56e303f0856a.png)

耐心等待後手機就建立成功了，直接執行：

![](https://pic.yupi.icu/1/1749610968230-15d4f951-0407-49c1-9453-d8d2035f9a6d.png)

結果，報錯啦！

![](https://pic.yupi.icu/1/1749610958509-4da79a4e-781a-48e5-bf97-93383de6b4ff.png)

如果你也遇到這種情況，可以在終端 **進入 Android 模擬器目錄** 手動執行虛擬裝置，這樣能夠看到詳細的錯誤資訊，有利於排查問題。

![](https://pic.yupi.icu/1/1749611297041-de408f6c-6acc-425e-bd7f-646c3c41fcb4.png)

比如我這裡顯然是由於路徑包含了中文！可惡啊，當時年少輕狂不自卑一個沒注意用了中文路徑。。。

![](https://pic.yupi.icu/1/1749611342058-e78e5020-2a11-4403-8bdb-28c1788d4287.png)

解決方法很簡單，手動建立一個不包含中文路徑的 avd 虛擬裝置目錄，然後設定環境變數 ANDROID_SDK_HOME：

![](https://pic.yupi.icu/1/1749612398190-b65661c4-b4c3-4d64-aeb1-491ec40ac55b.png)

然後再利用 Android Studio 建立一個裝置並執行，這次成功執行了，恭喜你多了一個手機！

![](https://pic.yupi.icu/1/1749612554480-2514015b-1592-49ee-83dd-fae7af6a6918.png)

至此，環境終於搞定了，下面來實戰 AI + Cordova 開發 APP。

## 三、AI + Cordova 實戰

### 建立專案

開啟終端，進入你想要建立專案的目錄，先執行 `cordova create` 命令來建立專案：

```bash
cordova create <你的專案英文名稱>
```

首次建立專案可能會有提示：

![](https://pic.yupi.icu/1/1748595666543-fd4ae41b-7edc-4443-bab6-3e6ff8eeb819.png)



### 生成程式碼

此處有 2 種生成模式：

1. 先建立 Cordova 專案，然後在該專案內進行 AI 程式碼生成。告訴 AI 你要建立一個相容 Cordova APP 的網站，直接讓 AI 生成相容 APP 的程式碼。這樣做的好處是生成的程式碼 **可以使用 Cordova 外掛呼叫系統原生的能力**，比如呼叫相機進行拍照。
2. 在 Cordova 專案外單獨用 AI 生成網站專案，AI 不會關心你是否要把專案轉為 Cordova APP，然後再把生成好的網站移動到 Cordova 專案中。這樣做的好處是生成的網站程式碼更容易執行，同樣 **適合你已經有現成網站專案** 的場景。

下面兩種方式我都會給大家演示，先講第一種模式，直接讓 AI 生成一個【表情包生成器】的 Cordova APP。

用 Cursor 開啟剛剛建立的 Cordova 專案目錄，給 AI 輸入下列提示詞，提示詞中需要包含 Cordova，並且提到 **相容性**：

```shell
請幫我開發一個【移動端表情包生成器】Web APP，使用純前端技術 + Cordova 實現。
如果需要，你可以透過 Cordova 呼叫系統原生功能。

請生成完整的專案程式碼，確保功能完整可用，而且所有功能都需要同時相容網頁端和移動裝置。

## 📋 功能需求
### 1. 圖片獲取
- 支援攝像頭拍照
- 支援從本地選擇圖片檔案
- 自動縮放圖片到合適尺寸

### 2. 表情包模板
- 提供8-10個常用表情包模板（驚呆了、無語、贊、點贊、emo了等）
- 網格佈局展示模板，點選選擇應用

### 3. 文字編輯
- 輸入自定義文字內容
- 調整字型大小（20px-50px）
- 選擇文字顏色（白色、黑色、紅色等基礎色彩）
- 新增文字描邊效果
- 拖拽移動文字位置

### 4. 貼紙功能
- 提供常用emoji表情貼紙（😂🤣😭😍🤔等5-10個）
- 提供簡單裝飾貼紙（星星、愛心、箭頭等）
- 支援拖拽移動和簡單縮放

### 5. 儲存功能
- 將編輯後的表情包匯出為圖片
- 支援下載儲存到本地

## 🎨 介面要求
- 移動端優先：適配手機螢幕，大按鈕設計
- 頁面佈局：
  - 主頁：拍照按鈕、選擇圖片按鈕
  - 編輯頁：頂部工具欄 + 中央畫布 + 底部功能區
- 操作簡單：實時預覽效果，一鍵儲存

## 📱 操作流程
1. 拍照或選擇圖片
2. 選擇表情包模板
3. 編輯文字內容和樣式
4. 新增emoji或裝飾貼紙
5. 預覽效果並儲存圖片 
```

AI 生成的網站檔案會放到 `www` 目錄下。生成程式碼完成後，AI 可能會自動提醒你打包 APP 並且執行的命令，要依次新增安卓平臺、安裝外掛、打包、執行。

![](https://pic.yupi.icu/1/1748596578547-e99a9448-e4a3-421c-907f-5e85c3b24ea2.png)

這些命令我們等會兒就會用到，現在先不要自動執行，因為生成的程式碼不一定直接可用，我們需要先利用網頁端進行除錯。



### 網頁瀏覽

可以直接雙擊生成的 HTML 檔案 `www/index.html` 檢視效果；當然，更推薦的是透過 cordova 命令新增平臺並執行。

先新增瀏覽器平臺：

```shell
cordova platform add browser
```

如果你在執行命令時遇到了報錯，可以直接問 AI，比如魚皮遇到了缺少命令執行許可權的錯誤：

![](https://pic.yupi.icu/1/1748597149478-5d93aa00-a15d-41a7-b7b3-6011c9098420.png)

解決方案是，執行下列命令來修改 PowerShell 的執行策略：

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

新增平臺成功後，可以輸入 `cordova run` 命令執行平臺：

```bash
cordova run browser
```

然後就能夠檢視到網站的執行效果了。需要注意的是，因為 Cordova Browser 平臺的特殊性，透過這個命令執行的網頁效果可能和直接雙擊、或者啟動本地伺服器執行有區別。

![](https://pic.yupi.icu/1/1749632376309-d49aa1f5-15fa-47ac-8ecc-34fafa453a17.png)

除了上面的命令外，如果你想快速除錯多個不同的平臺，可以執行下列命令，統一檢視各個平臺：

```bash
cordova serve --port 8000
```

![](https://pic.yupi.icu/1/1749632540888-2c8274ca-b2bc-488b-9d55-da8999b57a87.png)

### 新增安卓平臺

接下來執行類似的命令來新增安卓平臺：

```bash
cordova platform add android
```

如圖，新增安卓平臺成功，注意要 **確保輸出的 Target SDK 和 Compile SDK 版本一致**：

![](https://pic.yupi.icu/1/1749554296373-e755253d-c2e9-4367-87a4-9c9e24402f20.png)

如果不一致，可能會影響 APP 的執行。可以修改 `config.xml` 的 targetSdkVersion 來修改版本號：

![](https://pic.yupi.icu/1/1749548403555-9eb701bd-bd9f-469f-a672-b56d033c8b91.png)

### 新增外掛

由於我的專案需要呼叫攝像頭，所以要新增對應的外掛，執行下列命令：

```bash
cordova plugin add cordova-plugin-camera
```

新增外掛成功：

![](https://pic.yupi.icu/1/1748597252238-9c9d7da6-1b6e-42b1-ad5e-714498f21b67.png)



### 打包執行安卓 APP

#### 打包

安裝完外掛後，執行 `cordova build` 命令可以打包 Android apk：

```bash
cordova build android
```

看到下列資訊表示打包成功：

![](https://pic.yupi.icu/1/1749554490277-687fea6b-175e-4097-92e0-37090d4f3c63.png)

得到 apk 包後，有 2 種執行方式：

#### 手機執行

可以直接將 apk 包傳送到手機安裝執行：

![](https://pic.yupi.icu/1/1749608745115-c35207fa-a32c-4dc2-a74f-10244b993e51.png)

執行效果如圖：

![](https://pic.yupi.icu/1/1749609325122-30c51d37-aeaa-4e4e-95a1-6565dc212266.jpeg)

![](https://pic.yupi.icu/1/1749609327998-acbfdfbd-6982-4be4-9f77-d116046194a0.jpeg)



#### 電腦執行

先開啟 Android Studio 並啟動安卓虛擬裝置，然後執行 `cordova run` 命令：

```bash
cordova run android
```

就可以將 apk 安裝到虛擬裝置中，並且執行 APP 了，效果如圖：

![](https://pic.yupi.icu/1/1749612728673-2c8f7bd0-ecc5-46c4-b24c-573498a70e63.png)



### 常見報錯

打包執行是最容易遇到報錯的地方，可能會遇到很多種報錯，比如缺少外掛、缺少檔案、無法安裝依賴、無法執行等等，建議直接把報錯資訊發給 AI，讓它幫你解決。

下面魚皮分享一些自己遇到的坑點。

#### 1、專案缺少檔案

比如魚皮的專案缺少了圖示檔案：

![](https://pic.yupi.icu/1/1748597545640-7b26e31f-4c7e-4f57-999f-adbf5b2994ad.png)

AI 嘗試幫我建立圖示：

![](https://pic.yupi.icu/1/1748597699107-c363caa4-1e59-4fd6-ba4a-3004414b2c7c.png)

或者簡單粗暴，移除配置檔案中對圖示的引用：

![](https://pic.yupi.icu/1/1748597731494-234f4827-eef8-4a1d-9f00-0ed01b61d66d.png)



#### 2、缺少環境變數

如果環境搭建不順利，可能會遇到下列報錯，根據報錯資訊去進行對應的配置即可：

![](https://pic.yupi.icu/1/1748599524081-e2121c56-11bc-4504-bd2d-6a5fff26f4fb.png)



#### 3、命令執行失敗

執行 `cordova run` 報錯命令執行失敗，可能是因為沒有配置 `cmdline-tools` 到環境變數 Path 中。

![](https://pic.yupi.icu/1/1749607603308-b1dac4af-1505-4e15-b2ab-25ffd9abf3a5.png)



#### 4、Gradle 無法安裝

明明已經安裝了 Gradle，但是 Cordova 仍然會安裝 Gradle，而且可能因為網路原因下載失敗：

![](https://pic.yupi.icu/1/1749469918640-07f5eca4-5651-4e35-91a5-222c43363004.png)

這時，我們可以配置環境變數 `CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL`，指定從本地下載 Gradle。環境變數的值設定為我們自己下載的 Gradle 壓縮包的路徑。

![](https://pic.yupi.icu/1/1749471697598-c7dd5754-4e58-4b01-9787-5889a0f9df52.png)

如果修改配置後再次執行打包命令還是報錯，建議刪除專案內的 `platforms/android/.gradle` 快取，然後重試。



## 四、已有專案打包為 APP

剛剛實戰了直接用 AI 生成 Cordova APP 專案的方式，如果我們已經有現成的網站專案，也能夠很方便地打包為 APP。

比如現在魚皮有一個消消樂網頁遊戲專案，讓我們來包裝為 APP：

![](https://pic.yupi.icu/1/1749614057458-74ba49c0-d249-43ab-9946-631c8783cc75.png)

1）先建立 cordova 專案：

```bash
cordova create yu-game-web-app
```

2）把已有的網頁檔案複製到 www 目錄下：

![](https://pic.yupi.icu/1/1749614211678-13686f0e-7921-4abe-9ed2-beaf031ff38d.png)

3）執行 cordova 命令新增 Android 平臺：

```bash
cordova platform add android
```

4）最後，打包或者直接執行：

```bash
cordova run android
```

執行成功的效果如圖，還是很 nice 的~

![](https://pic.yupi.icu/1/1749614429684-50917cff-d0fc-4c0f-be7d-c356e7827410.png)



## 最後

OK，教程到這裡就結束了，由於缺少裝置等原因，IOS 就先不給大家演示了。

最後給大家一些建議，Cordova 比較適合中小型網站專案，尤其適合已經有網站專案想快速轉為 APP 的場景；但如果你需要搞一個複雜的大專案，依賴很多移動裝置的原生能力，使用 Cordova 就不是很合適了，不如 Flutter。尤其是沒有程式設計能力的同學來說，建議不要直接用 AI 生成複雜的 Cordova APP，很可能出現你搞不定的程式碼問題，但是做些小遊戲、小工具還是很不錯的。也希望我的分享對大家有幫助吧，想獲取更多程式設計和 AI 乾貨的朋友記得關注魚皮哦，拜拜~


## 推薦資源

1）魚皮 AI 導航網站：[AI 資源大全、最新 AI 資訊、免費 AI 教程](https://ai.codefather.cn)

2）程式設計導航學習圈：[學習路線、程式設計教程、實戰專案、求職寶典、交流答疑](https://www.codefather.cn)

3）程式設計師面試八股文：[實習/校招/社招高頻考點、企業真題解析](https://www.mianshiya.com)

4）程式設計師寫簡歷神器：[專業模板、豐富例句、直通面試](https://www.laoyujianli.com)

5）1 對 1 模擬面試：[實習/校招/社招面試拿 Offer 必備](https://ai.mianshiya.com)
