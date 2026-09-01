# Vibe Coding Website Beautification Tips

> 7 Methods to Remove the AI Flavor from Your Website

Hello, I'm Yupi.

Let's start with a small test. Can you tell which of the following websites were made by AI?

![](https://pic.yupi.icu/1/1769600749428-08e8524c-c71c-4ef0-b72f-feec296f5684.png)

![](https://pic.yupi.icu/1/1769600766773-a2f0782c-704f-4b17-a91a-bce1f3ee4b49.png)

![](https://pic.yupi.icu/1/1769600778173-2c16a9e4-4b3b-4d5e-9bfa-2c3f1450ab04.png)

The answer: **All of them were made by AI!**

![](https://pic.yupi.icu/1/1769600732342-59517bbf-7b63-4a3c-9979-76529d846259.png)

Surprised?

"Why does the website I made with AI have such a strong AI flavor, while these websites look much cleaner?"

This is exactly what I'm going to share next:

- What is the AI flavor in AI programming?
- Why do websites have an AI flavor?
- How to remove the AI flavor from websites?

After mastering these techniques, you can also make more beautiful websites with AI.

⭐️ Recommended to watch the video version of this article for a clearer effect:
https://bilibili.com/video/BV1QF6EBiErM

## What is the AI Flavor?

The so-called AI flavor refers to websites that are easily recognizable as AI-generated, with uniform interface styles and content.

![](https://pic.yupi.icu/1/1769600840225-3990db3e-7527-436e-a5bc-2a716fd287ab.png)

1) Rigid color schemes: Overused blue-purple gradients.

2) Rigid layouts: A large title on the first screen, followed by three cards in a row.

3) Rigid fonts: Mostly fixed fonts like Inter and Roboto.

4) Emoji overload: 🐟4️⃣🐶 and other emojis everywhere.

5) Hollow content: Mostly lacks real images, and the text style is also quite rigid.

Users feel like they're chatting with a robot when viewing these websites.

![](https://pic.yupi.icu/1/1769600858180-10f1ed0d-f92d-47bd-b88d-9f708c3d1b09.png)

## Why Do Websites Have an AI Flavor?

So why does this happen?

The core reason is two words: **Play it safe**.

For example, why does AI love blue-purple gradients so much?

Because in AI's training data, many modern websites use the Tailwind style library, whose default primary color is blue-purple. When AI learns billions of lines of code, these colors appear most frequently, so AI concludes that "modern websites ≈ blue-purple gradients."

![](https://pic.yupi.icu/1/1769600882890-89e4170f-00bf-44b5-9f17-1ebde2d3351f.png)

Moreover, AI has learned a survival rule: **Using the most common = least likely to make mistakes**.

So when you ask AI to "develop a modern website," AI plays it safe by choosing blue-purple gradients.

**How to break this pattern?**

Simple, shift from being a "requester" to a "commander."

Don't just say: Make me a website.

Instead, specify: Use a dark gray background, hand-drawn icons, asymmetric layout, and reject blue-purple.

Use strong constraints to push AI out of its comfort zone.

![](https://pic.yupi.icu/1/1769600923212-e36b1723-7a7d-4772-a757-3f513a96407c.jpeg)

## How to Remove the AI Flavor from Websites?

Here are 7 methods I've summarized to ensure your website sheds its AI flavor.

### Method 1: Let AI Reference Real Websites

The simplest and most direct approach: When you see a good-looking website, let AI learn from it.

There are 4 specific ways to do this:

1) If you use AI programming tools like Cursor or Claude Code, or utilize [Firecrawl MCP](https://www.firecrawl.dev/), let AI directly read the webpage.

![](https://pic.yupi.icu/1/1769600968915-1e80b6a6-53d2-40dd-9458-b5f8b11459c4.png)

Just tell AI:

```markdown
Please visit ai.codefather.cn, extract its color scheme, font selection, and layout structure, then generate a website in a similar style.
```

AI will visit the website and learn from it.

![](https://pic.yupi.icu/1/1769601048258-79c99e12-f960-460d-b66f-b0420bc4619a.png)

2) If the AI model supports image understanding, you can also provide a screenshot of the webpage to AI, which, combined with text, allows AI to recreate the website more accurately.

![](https://pic.yupi.icu/1/1769601076313-ac8b9644-1dc1-484a-b9ea-94d0828bb8a3.png)

The effect is as follows:

![](https://pic.yupi.icu/1/1769601123122-81bd55a5-5408-4472-b70a-e0b98fa68547.png)

3) If your AI model doesn't support image understanding and pure text understanding isn't sufficient, you can first use **screenshot-to-code** tools like [Screenshot to Code](https://github.com/abi/screenshot-to-code).

![](https://pic.yupi.icu/1/1769601172971-c6d47b5d-49c9-4b8e-86f2-55b2c3267e75.png)

Take a screenshot of your favorite website, upload it, and it will convert it into code.

![](https://pic.yupi.icu/1/1769601152959-ac25b585-b1e0-4b95-94a3-07acc9a2eb4e.png)

Then feed the code to AI and let it reference it.

![](https://pic.yupi.icu/1/1769601184992-01d76651-b0c7-4987-bf51-fc3f515bd917.png)

The accuracy will be much higher; copying styles is not as direct as copying code.

![](https://pic.yupi.icu/1/1769601222476-2dcde723-c897-4c6c-9d56-1e3ab50ac05f.png)

4) Additionally, you can directly use existing website templates or open-source projects on GitHub.

Here are some great website template resources:

- [HTML5 UP](https://html5up.net/): Free responsive website collection, minimalist style
- [WordPress Official Theme Library](https://cn.wordpress.org/themes/): Over 10,000 free themes, covering all types
- [Start Bootstrap](https://startbootstrap.com/): Free website template library for Bootstrap ecosystem
- [Colorlib](https://colorlib.com/wp/free-wordpress-themes/): Many free website templates with beautiful designs

These website templates come with source code. Download a good one, throw the code to AI, and let it modify the content. The style will be accurately reproduced.

![](https://pic.yupi.icu/1/1769601317176-fc548cbf-fecb-4ae7-aa9e-6f573a20d59a.png)

### Method 2: Design-First Development

This method is particularly suitable for large projects.

Simply put, **don't let AI go all-in on the entire project at once**.

For example, the traditional approach is: Help me build a complete SaaS platform including a user system and backend management.

Then AI generates dozens of files for you, only to find that the page style is wrong, requiring rework and wasting Tokens.

![](https://pic.yupi.icu/1/1769601339363-dcbc5190-fdfe-4a1c-b231-885545a855bc.png)

The recommended approach is **breaking it into steps**. First, let AI create a frontend website demo, just a static page. Once satisfied with the design, let AI develop the complete project based on the demo code.

If AI generates something like this, definitely don't let it continue!

![](https://pic.yupi.icu/1/1769601353690-2df4bbca-7140-446c-af0e-f7111bc9ea98.png)

Here’s a powerful AI design tool recommendation: [Google Stitch](https://stitch.withgoogle.com/).

Just input a description, and it can generate professional interface prototypes.

![](https://pic.yupi.icu/1/1769601399879-e2a70816-4e5a-4da3-b5a5-397e9c9f596f.png)

You can even sketch on paper, take a photo, upload it, and it will recognize and convert it into code.

![](https://pic.yupi.icu/1/1769601433733-0fa47423-cb67-4860-993d-17fb4a463d69.png)

You can manually modify the design theme or annotate parts to be adjusted, letting AI quickly make changes.

![](https://pic.yupi.icu/1/1769601453928-09f4b942-4cb6-4df6-a2f8-047008f6011d.png)

After design completion, export the file or download the code, then feed it to AI programming tools like Cursor for further development. This way, the style is set and won't deviate.

![](https://pic.yupi.icu/1/1769601475052-01de6924-0e89-4ad2-b0bc-cd45e778509e.png)

Of course, if you can use more professional design tools like [Figma](https://www.figma.com/), you can first design the website clearly in Figma.

![](https://pic.yupi.icu/1/1769601491432-a98ef003-f613-43e8-9333-b709df447703.png)

Then, with the [Figma MCP](https://github.com/GLips/Figma-Context-MCP) extension, let AI directly read your Figma design files and generate code based on the design.

![](https://pic.yupi.icu/1/1769601504433-d43ef9b4-ca40-49c0-977c-170ab43af4f8.png)

Additionally, there’s a tool called [Onlook](https://www.onlook.ai/), dubbed the Cursor for designers, allowing designers to visually edit web code, seamlessly integrating design and development.

![](https://pic.yupi.icu/1/1769518652135-ad6e4342-4a01-483e-8d42-bd5e38c53550.png)

### Method 3: Enrich Website Images

Generally, AI-generated websites lack images. We can make the website more personalized by adding images.

No need to let AI generate images from scratch; just tell AI to actively find images and where to find them.

Image resources mainly include illustrations, icons, real photos, and placeholders.

1) Illustration library [unDraw](https://undraw.co/): Many free SVG illustrations, customizable colors.

![](https://pic.yupi.icu/1/1769601537109-69845405-15c2-49c8-be61-ab07d9dd60ab.png)

2) Icon library [Iconify](https://iconify.design/): Over 200,000 free vector icons.

![](https://pic.yupi.icu/1/1769601552661-0984adc0-a931-434f-bf6b-bebdcfcf7585.png)

3) Real photos [Pexels](https://www.pexels.com/): Free high-quality photo library, also provides API for quick image searches.

![](https://pic.yupi.icu/1/1769601563667-0d0ee4ec-6b47-403c-ae3b-fef23771b47a.png)

4) Placeholder images [Picsum Photos](https://picsum.photos/): Use URL to specify image size, refreshing with different real photos each time.

![](https://pic.yupi.icu/1/1769601577827-353e909f-344c-4807-aae4-4a5d075953c9.png)

If your AI programming tool supports web reading, directly let AI search for images from these websites:

```markdown
I’m developing a photography portfolio website.
Please search and integrate image resources as needed:
1. Illustrations: Use undraw.co, search for illustrations related to the website content.
2. Icons: Use Iconify icon library.
3. Real photos: Use Pexels to search for real photos.
4. Placeholder images: Use Picsum Photos as temporary placeholders.
```

Now, the generated website looks much more mature, right?

![](https://pic.yupi.icu/1/1769601635196-ea757546-bd01-4b6d-a0c7-382b315f564a.png)

### Method 4: Prompt Constraints

Even without fancy tools, just clearly stating your requirements when talking to AI can make the website more professional.

Claude’s official Cookbook has an article [Frontend Aesthetics](https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics) (Frontend Aesthetics), specifically discussing how to avoid AI-generated generic designs.

![](https://pic.yupi.icu/1/1769601710440-6f8ffae7-3a7c-4b7f-afb9-2b0bca8008d5.png)

Here are some prompt techniques I commonly use.

#### 1) Reverse Prompts

Don’t just say "what you want," but also "what you don’t want."

```plain
Design Prohibitions:
❌ Purple/indigo gradients
❌ Flat background colors (must have noise or gradients)
❌ Hero + three-card layout
❌ Perfect center alignment
❌ High-sounding professional jargon and meaningless phrases
❌ Emojis as functional icons
❌ Linear animations ease-in-out
```

Clearly stating these prohibitions prevents AI from going rogue.

#### 2) Role Setting

Give AI a persona, for example:

```markdown
You are a senior independent designer specializing in "anti-mainstream" web aesthetics.
You despise cookie-cutter SaaS templates, believing software interfaces should have texture and soul.
Your creative boundaries:
- "Modern but not purple" → Try dark gray + orange
- "Minimalist but warm" → Use generous whitespace + hand-drawn illustrations
- "Techy but not cold" → Use dark + warm accents
```

This way, AI knows it’s not making standard answers but creating designs with personality.

#### 3) Reject Hollow Copy

AI loves writing "sounds impressive but says nothing" copy.

You need to clearly state copy requirements:

```plain
Website text must:
- Be specific: "Save 2 hours of repetitive work daily" (don’t say "increase productivity")
- Be conversational: "Use it as naturally as breathing" (don’t say "excellent user experience")
- Have emotion: "No more searching through 10 groups for files" (don’t say "efficient collaboration")
- Even provoke: "Stop pretending you’ll read those PPTs"
```

This makes the copy more human-like.

#### 4) Context Injection

AI often generates generic designs because it doesn’t know what "feeling" you want to convey.

So we can try **feeding AI emotions first, then requesting designs**.

For example, if you want to create a techy blog website, say:

```markdown
First, read this passage: "Hackers & Painters" - Programming languages are for thinking.

Now design the blog homepage based on this calm, rational emotion:
- Color scheme: Dark gray + cool blue
- Layout: Rational, orderly
- Feeling: Thoughtful, focused
```

AI aligns visual parameters (color, spacing, fonts) with textual emotional features (calm, rational), generating designs with a specific atmosphere.

![](https://pic.yupi.icu/1/1769601745340-d621e29c-76f7-4a8f-af01-7271d88c5272-20260128202014218.png)

Like directing an actor, don’t tell them to act happy; let them recall a happy memory, and the emotion naturally emerges.

#### 5) Reuse Prompts

With so many constraints, you can’t manually write them every time.

So save prompts as project rule files [AGENTS.md](https://agents.md/), facilitating reuse.

[AGENTS.md](https://agents.md/) is an open standard allowing different AI tools to read the same rule file, supported by mainstream AI programming tools (Cursor, Claude Code, Windsurf, etc.).

![](https://pic.yupi.icu/1/1769601770744-9db9fb73-1210-4807-8c41-3e1248a88455.png)

For example, here’s a prompt template I prepared, including all the techniques mentioned:

```markdown
# Project Design Rules (AGENTS.md)

## Role Setting
You are a senior independent designer specializing in "anti-mainstream" web aesthetics.
You despise cookie-cutter SaaS templates, pursuing warmth in every pixel.

## ❌ Absolute Prohibitions

### Color Prohibitions
- Purple/indigo/blue-purple gradients (#6366F1, #8B5CF6)
- Flat background colors (must have noise or gradients)
- Tailwind default color palette

### Layout Prohibitions
- Hero + three-card layout
- Perfect center alignment
- Equal-width columns (must be asymmetric)

### Copy Prohibitions
- High-sounding professional jargon and meaningless phrases
- Lorem Ipsum placeholder text
- Passive voice and long sentences

### Component Prohibitions
- Shadcn/Material UI default components (must be deeply customized)
- Emojis as functional icons
- Linear animations (ease-in-out)

## ✅ Must-Follow Rules

### Copy Style
- Conversational, like chatting with a friend
- Specific, with numbers and scenarios
- Can be humorous, self-deprecating, even provocative
- No sentence over 15 words

### Image System
- Icons: Use Iconify icon library (https://iconify.design)
- Placeholder images: Use Picsum Photos (https://picsum.photos)
- Real photos: Search on Pexels (https://www.pexels.com)
- Illustrations: Use unDraw (https://undraw.co)
```

Save this file as `AGENTS.md` and put it in your project root. From then on, every time you talk to the AI, it will automatically read this file and work according to your requirements.

![](https://pic.yupi.icu/1/1769601809476-e38cc355-3b1d-4b5c-af19-733829e0628c.png)

For example, give it the exact same prompt as before — "Help me build an anime video website." With the rule file in place, the difference is immediate!

![](https://pic.yupi.icu/1/1769601868173-f9e1ff80-8bd6-468a-bdf3-4d1ebbea7552.png)



### Method 5: Agent Skills

If writing prompts yourself feels too troublesome, there’s an even easier option — **Agent Skills**.

Simply put, Agent Skills are professional skill packs packaged by other people. You can install them directly into AI coding tools so the AI learns all kinds of specialized abilities, like making PPTs, organizing Excel sheets, and more.

![](https://pic.yupi.icu/1/1769601927834-226e857f-9dbb-4eca-a1d3-255fd1e0638d.jpeg)

If you want AI to build prettier and more distinctive websites, try these 2 Skills.

#### Frontend-design

This is Anthropic’s official [frontend design skill](https://github.com/anthropics/skills/tree/main/skills/frontend-design), which teaches AI to generate websites with a professional design feel.

Using it is simple. Take Claude Code as an example.

First, open Claude Code and run this command to add the official skill marketplace:

```plain
/plugin marketplace add anthropics/skills
```

![](https://pic.yupi.icu/1/1769307009465-4e04d585-3f68-4fcb-a3b0-ba43ad70139a-20260127164823520-20260128201603535.png)

This is basically like opening a skill store inside your AI assistant. After that, you can start installing skills from the store.

![](https://pic.yupi.icu/1/1769307026089-70a117da-b18e-4c7d-992b-1d08e30a7a0b-20260127164823553-20260128201603572.png)

Then run this command in Claude Code to install the official skill pack:

```plain
/plugin install example-skills@anthropic-agent-skills
```

![](https://pic.yupi.icu/1/1769307063576-10e2ce68-b5cd-41c7-8d6c-da0781298929-20260127164823605-20260128201603607.png)

This `example-skills` package contains a bunch of official demo skills, including frontend design, webpage testing, animated image creation, and more.

![](https://pic.yupi.icu/1/1769307079120-6aaf2999-fee5-4fdb-a5e3-2ba66824b4de-20260127164823637-20260128201603651.png)

Once it’s installed, you can directly ask AI to use those skills.

For example, if you type: help me build a personal portfolio website.

The AI will proactively ask: I noticed you installed the frontend design skill. Would you like me to use it to generate a more design-oriented page?

![](https://pic.yupi.icu/1/1769307135496-aa2a1e4e-4e8a-43e5-a138-9a148410b52e-20260127164911476-20260128201603748.png)

After you confirm, the AI will use the skill to generate the code, say goodbye to blue-purple gradients, and create a beautiful page with a unique style.

![](https://pic.yupi.icu/1/1769307161745-c81ca221-9902-49dd-96de-a99d50a17684-20260127164929260-20260128201603790.png)

No need to type the same huge pile of prompts to the AI every time. Install the skill once and you’re done.



#### UI UX Pro Max

[UI UX Pro MAX](https://ui-ux-pro-max-skill.nextlevelbuilder.io/) is the anti-AI-flavor skill I currently find the most practical. It’s specifically built to improve AI’s design ability.

![](https://pic.yupi.icu/1/1769601961428-9c2501f0-1d85-4911-932f-714396b5e06a.png)

It supports almost all mainstream AI coding tools right now, including Claude Code, Cursor, VS Code, Codex, and more.

Using it is also very simple. First, follow the instructions in the [open-source repository docs](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) to install the official CLI tool:

```bash
npm install -g uipro-cli
```

![](https://pic.yupi.icu/1/1769307627168-c682f14b-4517-4325-ad4a-33e88661e714-20260127165342236-20260128201604037.png)

Then go into your project directory and run the corresponding command based on the AI tool you use. For example, here I’m using Cursor:

```bash
uipro init --ai cursor
```

![](https://pic.yupi.icu/1/1769307641070-2138ef02-8f26-460a-8cdd-979c59b725de-20260127165352453-20260128201604091.png)

It will automatically install the skill into Cursor’s config directory.

Next, when you ask the AI to build a website, you can either trigger the skill manually with a slash command or let the AI recognize the skill automatically.

![](https://pic.yupi.icu/1/1769307707968-1545cef4-b8e2-4bf9-b0a7-98130afc78ba-20260127165405230-20260128201604126.png)

1) The AI first identifies the product type and the kinds of pages needed based on your requirements

![](https://pic.yupi.icu/1/1769307720984-a6afcae8-a5e8-4577-be7c-8356b42832ee-20260127165431384-20260128201604166.png)

2) Then it calls the `search.py` search script to run multi-dimensional searches in the data directory and find suitable color schemes, fonts, and layout styles

![](https://pic.yupi.icu/1/1769307768048-ef58645a-6188-4af7-9865-8033602126f7-20260127165431494-20260128201604217.png)

3) Based on the search results, it generates a complete design plan, including the main color palette, font combinations, spacing rules, and so on

![](https://pic.yupi.icu/1/1769307782038-59ea2231-b43d-45e3-a39f-6c36b0c7f645-20260127165431536-20260128201604239.png)

4) Finally, it generates the code according to that design plan

![](https://pic.yupi.icu/1/1769307794443-ffc76a7e-24e9-4e4d-b973-ef97285fd32b-20260127165431613-20260128201604303.png)

That way, the generated interface looks both professional and design-driven.

![](https://pic.yupi.icu/1/1769307819333-fef63881-90b7-4248-8ca7-35354f8a7a7a-20260127165431745-20260128201604458.png)

AI doesn’t have to memorize every rule. It can look up what it needs when it needs it — that’s the essence of Agent Skills.



### Method 6: Anti-AI-Flavor Component Libraries

As mentioned earlier, to play it safe, AI will usually default to the most mainstream component libraries, such as Tailwind CSS and Shadcn UI.

These libraries are professional, but they’re also the most likely to produce that AI flavor.

So we can do the opposite and explicitly tell AI to use some **niche but distinctive** component libraries.

For example, [Aceternity UI](https://ui.aceternity.com/) specializes in flashy effects — sparkles, aurora backgrounds, meteors, and other visually heavy components.

![](https://pic.yupi.icu/1/1769601991258-c39a8b17-c707-4fb5-ab92-73abe8eb6d35.png)

AI would struggle to write effects like this from scratch, but if you directly tell it to use this library, it can do it with just a few lines of code.

One thing to note: for these relatively niche component libraries, AI may not be very familiar with the latest usage. I recommend installing the Context7 plugin so it can look up the latest docs in real time.

![](https://pic.yupi.icu/1/1769602022954-c4712a60-e6e3-4818-b599-ca83fa41fdd3.png)

Or just send the official docs URL directly to the AI for reference:

```plain
You must use Aceternity UI to design the website
You need to read the official docs to understand the latest usage: https://ui.aceternity.com/components
```

The site’s style level instantly goes way up. It no longer looks AI-generated at all.

![](https://pic.yupi.icu/1/1769602042077-97940429-7324-4ba9-938a-5897095115c8.png)

There are lots of other UI component libraries I think have strong character:

- [Magic UI](https://magicui.design/): 150+ animated components for micro-interactions, glowing borders, text gradients
- [DaisyUI](https://daisyui.com/): 30+ themes, including cyberpunk, retro, cupcake, and more
- [Brutalist UI](https://brutalistui.site/): brutalist style, thick borders, hard shadows, high contrast
- [Glass UI](https://ui.glass/): glassmorphism effects, translucent layers, blurred backgrounds
- [ikun-ui](https://github.com/ikun-svelte/ikun-ui): a component library based on Svelte.js and UnoCSS
- [Radix UI](https://www.radix-ui.com/): unstyled primitive components for full customization
- [Mantine](https://mantine.dev/): 100+ rich-featured components

After two and a half years of practice, my personal favorite is still [ikun-ui](https://github.com/ikun-svelte/ikun-ui)~

![](https://pic.yupi.icu/1/1769602061209-92ee57f0-76aa-412e-a4bb-c700094688b2.png)



### Method 7: Custom Color Schemes (Advanced Tip)

If you want your website to be even more unique and fully go your own way, then you’ll need to manually design the color scheme.

This method is suitable for friends with some design background. You can use a few tools that quickly generate personalized palettes, such as:

- [Coolors](https://coolors.co/): a mainstream color palette generator; press the space bar for random palettes and export in multiple formats
- [Adobe Color](https://color.adobe.com/): Adobe’s official professional color tool

![](https://pic.yupi.icu/1/1769602205633-22850346-ee55-4ab3-916d-c54e0f66fae2.png)

Once you generate a palette, give the color values to the AI and tell it to strictly follow your scheme. The resulting website colors will definitely be unique.



## Practical Cases

The methods I introduced above can be combined. Below are a few real examples so you can feel the difference.

### Case 1: Personal Tech Blog

#### Before Optimization

Just enter this prompt:

```markdown
Build a homepage for a personal tech blog
```

The result looks like this. One glance and you know it’s AI...

![](https://pic.yupi.icu/1/1769602233437-c2df5654-4dc2-407d-86f8-c95888c446fd.png)



#### After Optimization

Use the `AGENTS.md` prompt rules + the UI UX Pro Max skill:

```markdown
Build a homepage for a personal tech blog
```

The resulting site feels geekier and the content is much richer.

![](https://pic.yupi.icu/1/1769602249372-66ac1c3f-7aaa-4890-be04-5a3615226d49.png)

![](https://pic.yupi.icu/1/1769602300430-f710cad3-dedb-4035-869c-42ef76467e95.png)



### Case 2: SaaS Product Landing Page

#### Before Optimization

Just enter this prompt:

```markdown
Build a landing page for the SaaS product "Server Operations Monitoring Platform"
```

The result looks like this — blue-purple colors again, instantly screams AI...

![](https://pic.yupi.icu/1/1769602314736-88e9b6e7-a14a-4ea3-99f4-5a2626c0d880.png)



#### After Optimization

Use the `AGENTS.md` prompt rules + the UI UX Pro Max skill + context injection + an anti-AI-flavor component library:

```markdown
Build a landing page for the SaaS product "Server Operations Monitoring Platform"

Read this sentence first to feel the atmosphere: In The Matrix, would you choose the blue pill or the red pill?
You must use Aceternity UI to design the website
You need to read the official docs to understand the latest usage: https://ui.aceternity.com/components
```

The background turns into code rain, and the page looks much more like a professional product landing page:

![](https://pic.yupi.icu/1/1769602346623-9d0988bb-5904-4328-9e87-9698bd9476f0.png)

![](https://pic.yupi.icu/1/1769602360859-110bfa1e-e0e5-4276-8074-883f7c7ddae9.png)



### Case 3: Fitness App Landing Page (Mobile)

#### Before Optimization

Just enter this prompt:

```markdown
Build a fitness app landing page (mobile)
```

The result... well, what even is this? No comment...

![](https://pic.yupi.icu/1/1769602385367-1a74cdeb-7452-471d-b13b-3afdddb6fb81.png)



#### After Optimization

Use the `AGENTS.md` prompt rules + the UI UX Pro Max skill + an anti-AI-flavor component library:

```markdown
Build a fitness app landing page (mobile)

You must use IKun UI to design the website
You need to read the official docs to understand the latest usage: https://ikun-ui.netlify.app
```



This time the page looks much more real and usable. The contrast is pretty obvious, right?

![](https://pic.yupi.icu/1/1769602473561-48f4ba99-d41a-462d-a7d3-6ea8613c43ba.png)



## Final Words

By this point, you should realize that AI is already extremely capable at building websites.

Some friends think the results AI generates aren’t ideal, but often that’s simply because they didn’t give it clear enough instructions.

It’s like a chef: if you just say “make something tasty,” to be safe they’ll cook the most generic home-style dish. But if you say “add more chili, skip the Sichuan peppercorns, add more doubanjiang,” they can make the exact flavor you want.

**Remember, AI is the tool. You are the one in charge.**

If you learned something — or unlearned something — give this a like~



## Recommended Resources

1) Yupi AI Navigation Website: [AI Resource Collection, Latest AI News, Free AI Tutorials](https://ai.codefather.cn)

2) Programming Navigation Learning Circle: [Learning Path, Programming Tutorials, Practical Projects, Job Hunting Guide, Q&A](https://www.codefather.cn)

3) Programmer Interview Eight-Part Essay: [Internship/Campus Recruitment/Social Recruitment High-Frequency Test Points, Enterprise Real Questions Analysis](https://www.mianshiya.com)

4) Programmer Resume Writing Tool: [Professional Templates, Rich Examples, Direct to Interview](https://www.laoyujianli.com)

5) 1-on-1 Mock Interview: [Internship/Campus Recruitment/Social Recruitment Interview Essential for Getting Offers](https://ai.mianshiya.com)