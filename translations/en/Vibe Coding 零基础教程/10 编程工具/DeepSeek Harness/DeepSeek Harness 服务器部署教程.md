# DeepSeek Harness Server Deployment Tutorial

> A step-by-step guide to deploying DSH on a cloud server for anytime, anywhere, multi-device access.

Hello everyone, I’m Yupi.

Recently, DeepSeek Harness (DSH for short) has absolutely exploded in popularity. It really feels like another OpenClaw moment from this year’s Spring Festival season.

As of the time of writing, DSH has only been out for one week, yet it has already reached 160k GitHub stars, and the plugin ecosystem is unbelievably lively. The community-curated `awesome-dsh-plugin` list already includes more than a thousand plugins.

![](https://pic.yupi.icu/1/image-20260820120154956.png)

Multi-model integration, scheduled tasks, code review, desktop pets, casual mini-games, stock tracking, and more—you’ll find all kinds of practical and entertaining plugins.

![](https://pic.yupi.icu/chengfang/02.png)

It really lives up to the official slogan: “everything is a plugin.” The freedom is kind of ridiculous.

But along with that freedom comes a pain point…

By default, only you can access DSH yourself. What if you carefully installed a bunch of plugins, tuned your workspace just right, and now want to share it with your team? Surely everyone doesn’t need to reinstall everything from scratch, right?

It would be great if the whole team could collaborate inside the same project space, with everyone directing AI together while project progress, session history, and the plugin environment all stay in sync.

There’s also a much more common scenario. Maybe you’re out and suddenly want to check how far your Vibe Coding project has progressed on your home computer, or see whether the AI has gone off the rails, so you can adjust the development direction in time.

Or maybe you’re on the subway, suddenly think of a great idea, and want AI to validate it right away—but all you have is your phone, so you have no choice but to jot it down first.

**Fortunately, DSH is web-based by nature. As long as you deploy it to a server and keep it running 24/7, all of these problems can be solved.**

In this article, I’ll show you step by step how to deploy DeepSeek Harness to a server so you can access it from anywhere and on any device.



## DSH Server Deployment Tutorial

First, we need a cloud server. The server used in this tutorial has a 2C2G configuration—2 CPU cores and 2 GB of memory—and runs Debian 12.15. In my tests, that was just enough to run DSH stably.

I recommend using a server with at least this configuration. If the specs are too low, DSH may run unstably.



### 1. Connect to the Server

If you’re using a mainstream cloud server provider such as Tencent Cloud, Alibaba Cloud, or Huawei Cloud, you can log in directly through the provider’s web console.

For example, Alibaba Cloud servers support remote connections via Workbench:

![](https://pic.yupi.icu/hackdeacon/62199223013191388358370042eb5134.png?imageSlim)

Besides logging in through the web, you can also connect to the server over SSH. Check your cloud provider’s official documentation for the specific steps.

Once you’re connected successfully, the next thing we need is a server management panel, so we don’t have to do everything in a black terminal window. Common options include Baota Panel and 1Panel.



### 2. Install 1Panel

Here we’ll use 1Panel as the example. 1Panel is a modern open-source Linux server operations panel with a clean and easy-to-use interface. It also comes with a built-in app store, so you can install various services with one click.

![](https://pic.yupi.icu/hackdeacon/20260819093905184.png?imageSlim)

In the server terminal, you can install 1Panel with a single command:

```
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```

The first step of installation asks you to choose a language. Enter `2` and press Enter to select Chinese.

![](https://pic.yupi.icu/hackdeacon/install.png?imageSlim)

Next, it asks you to choose an installation directory. Just press Enter and use the default path `/opt`.

Then the system asks whether to install Docker. Enter `y` to confirm. This step may be a little slow depending on your network environment, so just wait patiently for a few minutes.

![](https://pic.yupi.icu/hackdeacon/opt.png?imageSlim)

After Docker is installed, you’ll reach the last part of the panel installation: configuring the panel information.

![](https://pic.yupi.icu/hackdeacon/b4db65d99ef2a93454da26d7dd84af97.png?imageSlim)

First is **configuring image acceleration**. Accessing resources like GitHub and Docker can be slow from domestic networks in China, so it’s worth enabling mirrors. Just enter `y` and press Enter.

Next is **setting the 1Panel access port**. This port will be appended to your server IP address to access the management panel. For example, if your server IP is `114.51.41.xx` and you set the port to `9810`, then the panel address will be `114.51.41.xx:9810`.

You can press Enter to use a randomly generated port from 1Panel, or set an easy-to-remember number yourself. Just be careful to avoid ports already used by common services. I put together an image for reference:

![](https://pic.yupi.icu/hackdeacon/20260817171536312.png?imageSlim)

Then comes **setting the 1Panel security entry**, which is basically an extra token required when accessing the panel, also appended to the URL. For example, if you set it to `ikun`, then based on the example above, the full panel URL becomes `114.51.41.91:9810/ikun`. That way, even if someone knows your server IP and port, they still can’t get in without the security entry.

You can press Enter here as well to use a random entry, but I strongly recommend setting one you can actually remember.

Finally, you’ll **set the panel username and password**. No need to say much here—once that’s done, even if someone knows the security entry, they’ll still be blocked by the username and password. Triple protection. Max security.

![](https://pic.yupi.icu/hackdeacon/20260818094731552.png?imageSlim)



### 3. Open Firewall Ports

This step is also crucial. Only after opening the firewall ports will you be able to access services on the server from outside.

Using Alibaba Cloud as an example, go to the ECS management console, find “Security Groups,” and click “Add Rule” under “Inbound.” If you’re using another provider, look for a similar “Firewall” or “Security Group” settings page.

![](https://pic.yupi.icu/hackdeacon/f3f0b07035f44fb2cd0c9e7efcdd81ce.png?imageSlim)

For the source, choose `0.0.0.0/0 (anywhere)`, then enter the port number you set for 1Panel in the destination port field.

While you’re at it, you can also add the port DSH will use later—for example, `10443`. You can customize it too, as long as it doesn’t conflict with the avoidance list above.

After filling everything in, click submit.

Congratulations—if you’ve made it this far, you’ve already beaten 66.66% of the students!

![](https://pic.yupi.icu/1/image-20260820122944494.png)

All the preparation is done. Next, we’ll officially install DeepSeek Harness.



### 4. Install DSH

In your browser, enter `IP address:port/security-entry` to access the 1Panel admin panel.

After entering the homepage, you’ll be able to see the server’s current operating status and memory usage.

![](https://pic.yupi.icu/hackdeacon/6516be4bd4254146759ac9538ffbeef3.png?imageSlim)

Click the app store from the left-side menu, search for DeepSeek Harness, and you’ll see that 1Panel already includes it as a built-in app. Just click install.

![](https://pic.yupi.icu/hackdeacon/9f10e076076ef37cb62b3bcbe74c0629.png?imageSlim)

There are several configuration items in the installation screen worth paying attention to:

- HTTPS port: enter the port number you assigned to DSH in the firewall security group, for example `10443`
- Access address: enter your server’s public IP address
- Web username and password: these will be the login credentials required later when you access DSH

![](https://pic.yupi.icu/hackdeacon/ad4e2451202feae6ad4b7b9e685ab400.png?imageSlim)

A quick explanation here: DSH itself does not have built-in login authentication. Its web server even deliberately refuses to bind to `0.0.0.0` (that is, a publicly accessible address) precisely to prevent unauthorized access. The version in the 1Panel app store integrates a Caddy reverse proxy to provide HTTPS encryption and username/password authentication. All external access must pass Caddy authentication first before being forwarded to DSH, which gives you much better security.

Finally, check advanced settings, enable external port access, and click the confirm button in the bottom-right corner to start the installation.

![](https://pic.yupi.icu/hackdeacon/20260817183203204.png?imageSlim)

Once the installation finishes, you’ll be able to access DeepSeek Harness through `IP:10443`.

Since we haven’t configured our own domain name or a formal HTTPS certificate yet (1Panel uses a self-signed certificate), the browser will show a security warning. That’s normal—just ignore the risk and continue.

![](https://pic.yupi.icu/hackdeacon/20260817184102752.png?imageSlim)

Enter the Web username and password you set earlier to log in:

![](https://pic.yupi.icu/hackdeacon/20260817182501027.png?imageSlim)

After entering DSH, the first thing to do is configure the model. You can directly enter a DeepSeek API Key, or switch to other model providers in settings. DSH is compatible with the OpenAI interface format, so most model services on the market that support OpenAI-compatible APIs can be plugged in directly.

> Get your API Key from the DeepSeek Open Platform: https://platform.deepseek.com/api_keys

![](https://pic.yupi.icu/1/image-20260814130304526.png)

There’s one more thing to keep in mind. Because DSH is running on a cloud server, it can’t directly open project folders on your personal computer the way it can locally. You’ll need to manually create project directories in the workspace, or let DSH `git clone` projects from GitHub onto the server.

For your first try, I recommend using a test project rather than pointing it directly at a production code repository, since the Agent does have file read/write and command execution permissions.

![](https://pic.yupi.icu/hackdeacon/20260817185045890.png?imageSlim)

At this point, everything is ready, and you can start experiencing multi-device access.



### 5. Demo Experience

In theory, as long as the server can handle it, there’s no hard limit on how many devices can access it at the same time. I’ve personally used three or four devices simultaneously without any pressure, and project sessions, chat history, and plugin environments all stayed synced in real time.

Here I installed a Kun-themed skin, and you can see that whether I open DSH on my phone or computer, the skin stays perfectly synchronized.

![](https://pic.yupi.icu/hackdeacon/20260817192624023.png?imageSlim)

Even the streaming text output is fully synchronized. If one device is generating content, the other device can see it in real time as well.

For mobile use, I recommend installing a mobile UI adaptation plugin called `mexiaosqwq/dsh-web-mobile`. On narrow screens, it automatically turns the sidebar into a drawer and lets the session area fill the full width, making the interaction experience much better.

![](https://pic.yupi.icu/hackdeacon/20260819173700357.jpg?imageSlim)

You can install it with one command:

```bash
dsh plugin --profile web add github:mexiaosqwq/dsh-web-mobile
```

If you want to get started quickly with DeepSeek Harness and learn the basics, you can read *DeepSeek Harness Beginner-Friendly Starter Tutorial* in the DeepSeek Harness section of this tutorial’s Programming Tools chapter.



### 6. Bind a Domain Name

Using an IP address plus port number can access DSH, but it’s neither convenient nor especially secure. If you already have a domain name, I recommend binding a domain to DSH. It’s easier to remember, and you can also use a proper HTTPS certificate.

The operation isn’t difficult. First, go to the “Website” page in the left-side menu of 1Panel. 1Panel will prompt you to install OpenResty. Just click to install it from the store.

![](https://pic.yupi.icu/hackdeacon/20260818104728584.png?imageSlim)

Keep all settings at their defaults and click install directly.

![](https://pic.yupi.icu/hackdeacon/20260818105003532.png?imageSlim)

After the installation is complete, go back again to the “Website” page in the left-side menu and click create.

![](https://pic.yupi.icu/hackdeacon/20260819155642959.png?imageSlim)

Here, you can choose either “one-click deployment” or “reverse proxy” to complete the domain binding.

![](https://pic.yupi.icu/hackdeacon/20260818105639844.png?imageSlim)

![](https://pic.yupi.icu/hackdeacon/20260818105710699.png?imageSlim)

Configuring things only inside 1Panel isn’t enough. You also need to go to your cloud provider’s domain control console and configure DNS resolution for your server IP.

Add a record in the DNS settings, choose record type `A`, set the host record (name) to `dsh`, and set the record value to your server’s public IP.

![](https://pic.yupi.icu/hackdeacon/20260818170549641.png?imageSlim)

Save it, wait for the resolution to take effect, and then access the full domain name address to see DeepSeek Harness.

One important note: if DSH is deployed on a server located in mainland China, you’ll need to complete ICP filing before domain access will work normally. Without filing, the carrier will block the request and the page won’t open.

![](https://pic.yupi.icu/hackdeacon/20260818110235684.png?imageSlim)



## Why Choose Server Deployment?

At this point, some of you might ask: platforms like Vercel, Cloudflare, and Netlify are so convenient and don’t even require your own server—why not deploy DSH there?

Because DSH is not just a simple frontend webpage. It’s an “AI employee” that needs to stay alive for a long time, continuously read and write files, and constantly execute scripts and commands. It needs a stable environment to live in.

Meanwhile, platforms like Vercel, Cloudflare, and Netlify are built around Serverless architecture.

![](https://pic.yupi.icu/1/image-20260526190516543.png)

Note that Serverless doesn’t mean there are literally no servers. It means you only get temporary usage rights to servers managed and scheduled by the platform, so in practice you almost never need to operate the server manually from the command line. It’s more convenient.

Why call it temporary usage rights?

Because after your code is deployed to a Serverless platform, a runtime instance is started only when a request arrives, and it is destroyed after the request is handled. That’s the core design philosophy: “burn after use.”

This idea is great for APIs and static sites—scenarios where each request is handled independently—but it’s completely unsuitable for DSH.

DSH needs a persistent file system to save project code and session history, a real terminal to execute shell commands, and long-running processes to handle complex multi-step tasks. Serverless platforms usually offer only read-only or temporary file systems, no persistent terminal, and strict execution timeout limits. Once the function run ends, it’s destroyed, which simply can’t satisfy DSH’s requirements.

So it’s best to honestly deploy DSH on a server with a full operating system.



## LAN Deployment

If you don’t have a cloud server yet, or if you want all AI-generated output to stay local, LAN deployment is also a good option.

After deploying DSH on a local network, you can share it across devices at home. One main machine runs DSH, and you can lie in bed with a tablet and still connect to check AI’s progress. The whole household can share one environment.

If you set up a shared DSH in the office, coworkers on the same Wi-Fi can access it without everyone needing to install their own copy.

Sounds practical, right? So how do you do it?

Because the DSH plugin ecosystem is so rich, quite a few plugins already solve LAN access very well.

There’s a very popular all-in-one community plugin called [dsh-web-ui](https://github.com/zhu1090093659/dsh-web-ui). Besides built-in LAN remote access, it also provides a task board, Git graph, mobile remote control, skin center, and a whole suite of enhanced features. It already has several thousand stars on GitHub. If you’re interested, give it a try. If you want to learn more about DSH plugins, you can read *DeepSeek Harness Selected Plugin Recommendations* in the DeepSeek Harness section of this tutorial’s Programming Tools chapter.

![](https://pic.yupi.icu/1/13-hero-main.png?imageSlim)

If you don’t want the full all-in-one package and only need LAN access, you can also install just the corresponding plugin separately.

I organized the relevant plugins into an image based on different usage scenarios, so you can choose whatever fits your needs:

![](https://pic.yupi.icu/hackdeacon/20260818150215666.png?imageSlim)

Here’s one more technical detail. By default, DSH only listens on `127.0.0.1`, the local loopback address. At the CLI level, the official implementation deliberately rejects binding requests like `--host 0.0.0.0` in order to avoid directly exposing the Agent’s command execution capabilities to the network.

The plugins above that support LAN access work by patching the bundle at the plugin layer so the webserver binds to `0.0.0.0`, while also injecting a `crypto.randomUUID` polyfill to solve missing browser APIs in non-HTTPS environments. It’s convenient, but LAN access means any device on the same network can connect to your DSH, so I only recommend using it in trusted internal environments such as your home or company network.



## Final Thoughts

By this point, you should be able to feel just how open DeepSeek Harness is.

Besides “everything is a plugin,” DSH choosing a web form rather than a desktop client means it naturally supports remote access, multi-device sync, and team collaboration. That kind of openness is something Agent tools that can only run locally simply don’t have.

If you want to use DSH anytime and anywhere, share it with your team, or keep AI from messing with files on your own computer, try following this tutorial to set up cloud-based DSH.

If you want to get started quickly with DeepSeek Harness and learn the basics, you can read *DeepSeek Harness Beginner-Friendly Starter Tutorial* in the DeepSeek Harness section of this tutorial’s Programming Tools chapter.
