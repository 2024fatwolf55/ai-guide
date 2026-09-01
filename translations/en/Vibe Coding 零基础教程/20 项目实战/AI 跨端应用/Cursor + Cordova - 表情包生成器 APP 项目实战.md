# Cursor + Cordova - Meme Generator APP Project in Action

This project will take you through building an APP that can run on a phone entirely through Vibe Coding, without writing a single line of code.

This is a classic Vibe Coding project. Yupi will explain how to use AI to generate a website and then package it into an APP with tools. The focus is on learning how to use Cordova and understanding the APP packaging workflow, making it perfect for students who want to build an APP quickly.

---

The APP you’re seeing now was generated completely by AI—I didn’t write a single line of code! So how did I do it?

![](https://pic.yupi.icu/1/image-20250612190219936.png)

Hello everyone, I’m programmer Yupi. AI is developing fast, and now it’s easy to generate a website. But how can you use only AI to build an APP that runs on a phone? There are basically no complete tutorials online. So I stepped in. In just a few minutes, I’ll teach you how to use AI to generate an APP—still a **step-by-step tutorial** as always.

⭐️ Video version of this article, highly recommended: [https://bilibili.com/video/BV17HMcziEye](https://www.bilibili.com/video/BV17HMcziEye/)

Now, let’s welcome our main character: `Cordova`!

## 1. What Is Cordova?

Apache Cordova is an open-source mobile application development framework that allows developers to build **cross-platform** mobile apps using web technologies such as HTML, CSS, and JavaScript. By packaging web technologies inside a native container, it allows developers to write code once and run it on Android, iOS, Windows, and other platforms.

![](https://pic.yupi.icu/1/1749628169384-9f90fa60-e328-46c8-99eb-6f4f343b8aeb.png)

Cordova is mainly implemented based on the following core components. If you’re interested, you can take a look:

![](https://pic.yupi.icu/1/image-20250612190256834.png)

In other words, if you want to build an APP, all you need to do is hand your website files to Cordova, install a few plugins as needed, tweak some configuration, and then use its build tools to package the web app into a native APP (for example, an APK file)! It almost doesn’t involve any coding or development at all.

Sounds easy, right? Like anyone can do it? But if you want to use Cordova to build an APP, you **must** install the corresponding environment on your computer, such as Android and iOS. And honestly, the difficulty of setting up that environment is **explosively painful**.

If you try to figure it out on your own, it might take you several days. You’ll probably hit a lot of pitfalls, search all kinds of solutions online, and still not necessarily get it working. That’s exactly why I made this tutorial—I’ve already stepped on the mines for you. I’ll **help you get the environment set up in the shortest time possible and teach you how to use AI + Cordova to generate an APP**. Before we begin, don’t forget to like, bookmark, and engage, okay? Please—I really don’t have much hair left!

![](https://pic.yupi.icu/1/1749628109290-90dc8199-664a-4994-8dfe-716b4f8b5b71.png)

## 2. Environment Preparation

### Install Cordova

First, we need to install Cordova. Cordova depends on the Node.js and NPM frontend tools. Just download them from the [Node.js official site](https://nodejs.org/zh-cn), and NPM will be installed automatically.

![](https://pic.yupi.icu/1/1749628757935-a1f29765-c0e8-4c3a-9486-e113f3814e8d.png)

You can think of NPM as a little tool for quickly installing various kinds of software. After it’s installed, open a terminal and run the following command to install Cordova:

```bash
npm install -g cordova
```

Cordova supports packaging websites into Android and iOS mobile apps as well as Electron desktop apps. Next, Yupi will walk everyone through installing what I personally think is the hardest environment: **the Android environment**. Note that every step from here on is not actually difficult—but you must read carefully! Miss one small detail, and you might run into an error.

### Install the Android Environment

First, we need to determine the required environment and tool versions based on the version of Cordova. Since we’re installing the latest version of Cordova, we can directly read the [latest official documentation](https://cordova.apache.org/docs/en/dev/guide/platforms/android/index.html). For example, the dependencies I needed were as follows:

![](https://pic.yupi.icu/1/1749470136150-38d5fe30-e3e3-4994-8c06-ada90cc3deb7.png)

Among them, the most important ones are:

- Java 17
- Gradle 8.13
- Android API level >= 24

Now let’s install these dependencies one by one.

#### 1. Install Java

The Java version must be 17. It’s best to find a ready-made [Java installer for Windows](https://www.azul.com/downloads/?version=java-17-lts&os=windows&package=jdk#zulu):

![](https://pic.yupi.icu/1/1749629753199-b8458627-2a44-4d5b-8786-74bc1d5b83bc.png)

When installing Java, I recommend choosing **automatic environment variable configuration** (including Path and `JAVA_HOME`), so you don’t have to configure them manually.

![](https://pic.yupi.icu/1/1748604000379-99f42d77-7198-4c44-989c-914f21175452.png)

After installation, open a terminal and run `java -version` to check the version number. If you see the following output, it means success:

![](https://pic.yupi.icu/1/1748604045327-9e78c03d-dff8-4823-a6f8-221b1c288b77.png)

If the command can’t be executed, it’s very likely that the Path environment variable was not configured correctly.

![](https://pic.yupi.icu/1/1749715203575-d424aa3d-9be3-4e55-936e-8c99211a10a9.png)

#### 2. Install Gradle

According to the version requirements above, Gradle must be 8.13. Just download the binary zip package directly from the [official site](https://gradle.org/releases/).

![](https://pic.yupi.icu/1/1749470207621-4d12c5fa-6849-49eb-807a-46512cbd7011.png)

Extract the downloaded archive, move it to a **path that does not contain Chinese characters**, and then configure the environment variables, including Path and `GRADLE_HOME`:

![](https://pic.yupi.icu/1/1749470552544-1d872d78-933d-404e-a5d3-95071f98f72c.png)

![](https://pic.yupi.icu/1/1749471051766-77ad3676-a1f4-449a-9c6c-3db9adaf5484.png)

Open a terminal and run `gradle -v` to check the version:

![](https://pic.yupi.icu/1/1749470606188-7af15756-34de-4f77-b469-6b88afc5e6bd.png)

If the command cannot be executed, the Path environment variable is probably configured incorrectly.

#### 3. Install Android

I recommend installing the Android development tool [Android Studio](https://developer.android.com/studio?hl=zh-cn) directly. It will automatically install the Android SDK and runtime environment.

Download Android Studio from the official site, run the installer, and follow the steps:

![](https://pic.yupi.icu/1/1748600319317-775ad570-b84d-441e-9538-3f654e0c0280.png)

After installation, the first time you open Android Studio, it will remind you to install the Android SDK environment:

![](https://pic.yupi.icu/1/1748600394690-c64893b5-28f2-439e-afc2-302b616c2cb6.png)

Be careful not to install the SDK components into a directory containing Chinese characters. Fortunately, the installer itself warns you about this, or a whole lot more people would trip over it...

![](https://pic.yupi.icu/1/1748601041213-24016b9f-a6ce-4e8e-afba-a412cdee7dab.png)

After that, just follow the installer without overthinking it. It will automatically install various commonly used Android development tools, as well as the Android device emulator:

![](https://pic.yupi.icu/1/1748601061577-19061773-bea7-4f90-8fd4-588a99049611.png)

This step can be a little painful. Friends in some regions may need certain special network support—you know what I mean.

![](https://pic.yupi.icu/1/1748601238964-92c8754e-7c98-4c5d-9b4d-d1a1ede316ed.png)

![](https://pic.yupi.icu/1/1748601268568-8e5e99b1-0792-49f3-9bd1-d8073282743a.png)

After a long wait, the Android SDK is finally installed. Then you need to configure the Android environment variable `ANDROID_HOME`:

![](https://pic.yupi.icu/1/1749469684248-b1c77491-ca2b-49bd-a4e4-fffcef962868.png)

You also need to add `platform-tools` to Path, because it contains some command-line tools:

![](https://pic.yupi.icu/1/1749469743427-c052d689-2746-4522-a37d-4ba5513cf857.png)

After the configuration is complete, open Android Studio, go into SDK Manager from the top-right settings, and install the SDK versions required by the Cordova version—for example, I installed versions 34 and 35 here.

![](https://pic.yupi.icu/1/1748604140186-2cfeee7a-5cce-4647-8dc6-98afc4c7e980.png)

This step may also be slow, so just be patient while it installs~

![](https://pic.yupi.icu/1/1748604151163-82381d25-9824-446c-b418-54e758de9a5f.png)

After the SDK is installed, go into the SDK Tools tab and install the Command-line Tools, which may be needed later when running Android APKs on your computer:

![](https://pic.yupi.icu/1/1749607562141-66bfc793-a918-4359-b574-a8d52bc250a1.png)

Likewise, add Command-line Tools to the Path environment variable. The path is `%ANDROID_HOME%\cmdline-tools\latest\bin`. This makes many tools directly usable in the terminal, such as `apkanalyzer`.

![](https://pic.yupi.icu/1/1749607796266-a0dbb7b1-62ab-4b43-abcb-796b7261d45a.png)

#### 4. Install the Android Device Emulator

Next, we’ll try running an Android phone emulator on our computer, which makes debugging much easier.

Open the Device Manager in Android Studio and add a new device:

![](https://pic.yupi.icu/1/1749609766461-16befd69-65e1-4c07-bb6a-7e5ee2500dc4.png)

Choose a device model. I recommend selecting one with a relatively high API version. I chose Pixel 7:

![](https://pic.yupi.icu/1/1749610449536-edf49ed9-852c-425f-b3a0-a7e7bcc95d90.png)

Install the recommended system image:

![](https://pic.yupi.icu/1/1749609929190-ad696301-b3d1-4642-98b1-56e303f0856a.png)

After patiently waiting, the virtual phone will be created successfully. Just run it:

![](https://pic.yupi.icu/1/1749610968230-15d4f951-0407-49c1-9453-d8d2035f9a6d.png)

And... error!

![](https://pic.yupi.icu/1/1749610958509-4da79a4e-781a-48e5-bf97-93383de6b4ff.png)

If you run into the same issue, you can **enter the Android emulator directory** in the terminal and launch the virtual device manually. That way you can see detailed error information, which helps with troubleshooting.

![](https://pic.yupi.icu/1/1749611297041-de408f6c-6acc-425e-bd7f-646c3c41fcb4.png)

For example, in my case, it was obviously caused by the path containing Chinese characters! Damn it—I was young and reckless and carelessly used a Chinese path...

![](https://pic.yupi.icu/1/1749611342058-e78e5020-2a11-4403-8bdb-28c1788d4287.png)

The solution is simple: manually create an `avd` virtual device directory that does not contain Chinese characters, then set the environment variable `ANDROID_SDK_HOME`:

![](https://pic.yupi.icu/1/1749612398190-b65661c4-b4c3-4d64-aeb1-491ec40ac55b.png)

Then use Android Studio to create a device and run it again. This time it starts successfully—congratulations, you now own another phone!

![](https://pic.yupi.icu/1/1749612554480-2514015b-1592-49ee-83dd-fae7af6a6918.png)

At this point, the environment is finally ready. Next, let’s get into the hands-on AI + Cordova APP development.

## 3. AI + Cordova in Practice

### Create the Project

Open a terminal, go to the directory where you want to create the project, and first run the `cordova create` command:

```bash
cordova create <你的项目英文名称>
```

When creating a project for the first time, you may see a prompt like this:

![](https://pic.yupi.icu/1/1748595666543-fd4ae41b-7edc-4443-bab6-3e6ff8eeb819.png)

### Generate the Code

There are 2 generation modes here:

1. First create the Cordova project, then generate AI code inside that project. Tell the AI you want to create a website compatible with a Cordova APP, and directly ask it to generate APP-compatible code. The advantage is that the generated code **can use Cordova plugins to call native system capabilities**, such as using the camera to take photos.
2. Independently generate the website project with AI outside the Cordova project. The AI won’t care whether you plan to turn it into a Cordova APP, and then you move the generated website into the Cordova project afterward. The advantage is that the generated website code is easier to run, and it is also **suitable if you already have an existing website project**.

I’ll demonstrate both methods below. Let’s start with the first one: directly having AI generate a Cordova APP for a “meme generator.”

Open the newly created Cordova project directory with Cursor, and give the AI the following prompt. The prompt needs to include Cordova and mention **compatibility**:

```shell
请帮我开发一个【移动端表情包生成器】Web APP，使用纯前端技术 + Cordova 实现。
如果需要，你可以通过 Cordova 调用系统原生功能。

请生成完整的项目代码，确保功能完整可用，而且所有功能都需要同时兼容网页端和移动设备。

## 📋 功能需求
### 1. 图片获取
- 支持摄像头拍照
- 支持从本地选择图片文件
- 自动缩放图片到合适尺寸

### 2. 表情包模板
- 提供8-10个常用表情包模板（惊呆了、无语、赞、点赞、emo了等）
- 网格布局展示模板，点击选择应用

### 3. 文字编辑
- 输入自定义文字内容
- 调整字体大小（20px-50px）
- 选择文字颜色（白色、黑色、红色等基础色彩）
- 添加文字描边效果
- 拖拽移动文字位置

### 4. 贴纸功能
- 提供常用emoji表情贴纸（😂🤣😭😍🤔等5-10个）
- 提供简单装饰贴纸（星星、爱心、箭头等）
- 支持拖拽移动和简单缩放

### 5. 保存功能
- 将编辑后的表情包导出为图片
- 支持下载保存到本地

## 🎨 界面要求
- 移动端优先：适配手机屏幕，大按钮设计
- 页面布局：
  - 主页：拍照按钮、选择图片按钮
  - 编辑页：顶部工具栏 + 中央画布 + 底部功能区
- 操作简单：实时预览效果，一键保存

## 📱 操作流程
1. 拍照或选择图片
2. 选择表情包模板
3. 编辑文字内容和样式
4. 添加emoji或装饰贴纸
5. 预览效果并保存图片 
```

The website files generated by AI will be placed in the `www` directory. After the code is generated, the AI may automatically remind you of the commands to package and run the APP. In order, you’ll need to add the Android platform, install plugins, package, and run.

![](https://pic.yupi.icu/1/1748596578547-e99a9448-e4a3-421c-907f-5e85c3b24ea2.png)

We’ll use these commands in a moment, but don’t execute them automatically yet. The generated code may not be directly usable, so we need to debug it in the web version first.

### Web Preview

You can directly double-click the generated HTML file `www/index.html` to view the result. Of course, I more strongly recommend adding a platform and running it through Cordova commands.

First add the browser platform:

```shell
cordova platform add browser
```

If you run into an error when executing the command, just ask AI directly. For example, Yupi encountered an error about lacking permission to execute commands:

![](https://pic.yupi.icu/1/1748597149478-5d93aa00-a15d-41a7-b7b3-6011c9098420.png)

The solution is to run the following command to modify PowerShell’s execution policy:

```bash
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

After successfully adding the platform, you can run the platform using `cordova run`:

```bash
cordova run browser
```

Then you’ll be able to view the running effect of the website. Note that because of the special nature of the Cordova Browser platform, the result when running through this command may differ from double-clicking the file directly or running it through a local server.

![](https://pic.yupi.icu/1/1749632376309-d49aa1f5-15fa-47ac-8ecc-34fafa453a17.png)

In addition to the above command, if you want to quickly debug multiple different platforms, you can run the following command to preview them in a unified way:

```bash
cordova serve --port 8000
```

![](https://pic.yupi.icu/1/1749632540888-2c8274ca-b2bc-488b-9d55-da8999b57a87.png)

### Add the Android Platform

Next, run a similar command to add the Android platform:

```bash
cordova platform add android
```

As shown, the Android platform was added successfully. Be sure to **make sure the output Target SDK and Compile SDK versions are consistent**:

![](https://pic.yupi.icu/1/1749554296373-e755253d-c2e9-4367-87a4-9c9e24402f20.png)

If they are inconsistent, it may affect how the APP runs. You can modify the `config.xml` `targetSdkVersion` to change the version number:

![](https://pic.yupi.icu/1/1749548403555-9eb701bd-bd9f-469f-a672-b56d033c8b91.png)

### Add Plugins

Since my project needs to use the camera, I need to add the corresponding plugin. Run the following command:

```bash
cordova plugin add cordova-plugin-camera
```

Plugin added successfully:

![](https://pic.yupi.icu/1/1748597252238-9c9d7da6-1b6e-42b1-ad5e-714498f21b67.png)

### Package and Run the Android APP

#### Package

After installing the plugin, run the `cordova build` command to package the Android APK:

```bash
cordova build android
```

If you see the following message, the packaging succeeded:

![](https://pic.yupi.icu/1/1749554490277-687fea6b-175e-4097-92e0-37090d4f3c63.png)

After obtaining the APK package, there are 2 ways to run it:

#### Run on a Phone

You can directly send the APK package to your phone and install it:

![](https://pic.yupi.icu/1/1749608745115-c35207fa-a32c-4dc2-a74f-10244b993e51.png)

The running result looks like this:

![](https://pic.yupi.icu/1/1749609325122-30c51d37-aeaa-4e4e-95a1-6565dc212266.jpeg)

![](https://pic.yupi.icu/1/1749609327998-acbfdfbd-6982-4be4-9f77-d116046194a0.jpeg)

#### Run on a Computer

First open Android Studio and start the Android virtual device, then run the `cordova run` command:

```bash
cordova run android
```

This will install the APK into the virtual device and run the APP. The effect is shown below:

![](https://pic.yupi.icu/1/1749612728673-2c8f7bd0-ecc5-46c4-b24c-573498a70e63.png)

### Common Errors

Packaging and running is where you are most likely to run into errors. You may encounter many kinds of issues, such as missing plugins, missing files, failure to install dependencies, inability to run, and so on. I recommend directly sending the error message to AI and letting it help you solve it.

Below, Yupi shares a few pitfalls I personally encountered.

#### 1. Missing Files in the Project

For example, Yupi’s project was missing the icon file:

![](https://pic.yupi.icu/1/1748597545640-7b26e31f-4c7e-4f57-999f-adbf5b2994ad.png)

The AI tried to help me create the icon:

![](https://pic.yupi.icu/1/1748597699107-c363caa4-1e59-4fd6-ba4a-3004414b2c7c.png)

Or, more simply and brutally, you can remove the icon reference from the config file:

![](https://pic.yupi.icu/1/1748597731494-234f4827-eef8-4a1d-9f00-0ed01b61d66d.png)

#### 2. Missing Environment Variables

If the environment setup doesn’t go smoothly, you may encounter the following kinds of errors. Just configure things according to the error message:

![](https://pic.yupi.icu/1/1748599524081-e2121c56-11bc-4504-bd2d-6a5fff26f4fb.png)

#### 3. Command Execution Failure

If `cordova run` fails with a command execution error, it may be because `cmdline-tools` was not added to the Path environment variable.

![](https://pic.yupi.icu/1/1749607603308-b1dac4af-1505-4e15-b2ab-25ffd9abf3a5.png)

#### 4. Gradle Cannot Be Installed

Even if Gradle is already installed, Cordova may still try to install Gradle by itself, and the download may fail due to network issues:

![](https://pic.yupi.icu/1/1749469918640-07f5eca4-5651-4e35-91a5-222c43363004.png)

At this point, we can configure the environment variable `CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL` to specify using a locally downloaded Gradle package. Set the value of the environment variable to the path of the Gradle archive we downloaded ourselves.

![](https://pic.yupi.icu/1/1749471697598-c7dd5754-4e58-4b01-9787-5889a0f9df52.png)

If packaging still fails after changing the configuration, I recommend deleting the `platforms/android/.gradle` cache inside the project and trying again.

## 4. Package an Existing Project into an APP

Just now, we practiced directly generating a Cordova APP project with AI. If you already have an existing website project, you can also package it into an APP very conveniently.

For example, Yupi currently has a matching-game web project. Let’s package it into an APP:

![](https://pic.yupi.icu/1/1749614057458-74ba49c0-d249-43ab-9946-631c8783cc75.png)

1) First create the Cordova project:

```bash
cordova create yu-game-web-app
```

2) Copy the existing website files into the `www` directory:

![](https://pic.yupi.icu/1/1749614211678-13686f0e-7921-4abe-9ed2-beaf031ff38d.png)

3) Run the Cordova command to add the Android platform:

```bash
cordova platform add android
```

4) Finally, package or run it directly:

```bash
cordova run android
```

If it runs successfully, the result looks like this—pretty nice indeed~

![](https://pic.yupi.icu/1/1749614429684-50917cff-d0fc-4c0f-be7d-c356e7827410.png)

## Final Words

OK, that’s the end of the tutorial. Since I’m missing the necessary devices and other conditions, I won’t demonstrate iOS for everyone this time.

Let me leave you with a few suggestions. Cordova is more suitable for small to medium-sized website projects, especially if you already have a website project and want to turn it into an APP quickly. But if you need to build a large and complex project that depends on a lot of native mobile-device capabilities, Cordova is not that suitable—Flutter would be a better choice. Especially for students without programming ability, I don’t recommend directly using AI to generate a complex Cordova APP, because you may end up with code problems you can’t solve. But for small games and utility tools, it’s still very good. I hope my sharing was helpful. If you want more programming and AI goodies, remember to follow Yupi. Bye-bye~

## Recommended Resources

1) Yupi's AI navigation site: [AI resource collection, latest AI news, free AI tutorials](https://ai.codefather.cn)

2) Programming Navigation learning circle: [Learning paths, programming tutorials, hands-on projects, career guides, Q&A](https://www.codefather.cn)

3) Programmer interview cheatsheet: [Internship/campus/social recruitment key points, enterprise question analysis](https://www.mianshiya.com)

4) Programmer resume tool: [Professional templates, rich examples, direct to interviews](https://www.laoyujianli.com)

5) 1-on-1 mock interviews: [Essential for internship/campus/social recruitment interviews to get offers](https://ai.mianshiya.com)
