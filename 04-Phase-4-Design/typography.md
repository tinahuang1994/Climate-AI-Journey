# Typography & AI Web Design

*Created: March 2026 | Source: Introduction to Typography — California Institute of the Arts (CalArts, Coursera)*

**🌟 Introduction: Why Typography Matters in AI Coding**

Welcome! As developers using tools like Claude Code, we often rely on AI's "Front-end Design Skills" to build interfaces. The biggest issue? **AI defaults to generic, safe templates.** Everything looks like a standard Bootstrap or Tailwind demo.

In this course, we will learn that **Typography is not just about making things "look pretty" -- it is the visual voice of your product.** By understanding the technical rules (the math) of typography, you can command AI to build websites that feel professional, bespoke, and emotionally resonant.

To make these concepts concrete, we will analyze two real-world AI projects:

1.  🔥 **Smoke Story** ([https://smokestory.onrender.com/](https://smokestory.onrender.com/)) - A climate tracking and storytelling tool.

2.  🛡️ **No Thanks** ([https://nothanks-xi.vercel.app/](https://nothanks-xi.vercel.app/)) - A professional boundary-setting and communication coach.

**🏛️ Part 1: Core Concepts from CalArts**

*(Note: The following principles are derived directly from the CalArts Coursera curriculum.)*

**1. Type as Image**

The most important lesson from CalArts is that before a user reads a single word, they perceive the text block as an image. The shape of the letters instantly communicates a "vibe."

-   **Serif (衬线体):** Letters with small "feet" or decorative strokes at the ends (e.g., Times New Roman, Georgia). They communicate tradition, authority, luxury, and serious editorial journalism.

-   **Sans-Serif (无衬线体):** Letters without feet (e.g., Arial, Helvetica). They communicate modernity, cleanliness, tech, and efficiency.

**2. The Math of Comfort: Leading & Measure**

If your website feels "tiring" to read it violates these two geometric rules taught at CalArts:

-   **Leading (行距):** The vertical space between lines of text. AI usually sets this too tight. Good typography requires generous leading (e.g., 1.5 to 1.6 times the font size) to let the text "breathe."

-   **The Measure (行宽):** The length of a line of text. The human eye gets fatigued if a line is too long. The optimal measure is **45 to 75 characters per line**. AI often spans text across the entire width of the screen, which destroys readability.

**🔍 Part 2: Case Studies & Diagnosis**

*(Note: This section is your Professor's analysis of your specific projects.)*

**Case Study 1: Smoke Story**

-   **The Goal:** A mix of urgent climate data mapping and "luxurious newspaper" storytelling.

-   **The Problem:** Currently, the site likely relies on default system sans-serif fonts. This makes it look like a generic dashboard, completely missing the "newspaper" authority you want.

-   **Professor's Prescription:** \* **Headers:** Use a high-contrast, dramatic **Serif** font (like Playfair Display or Merriweather). This instantly creates the "New York Times" luxurious feel.

    -   **Body Text:** Use a highly readable Serif (like Lora or Georgia) for the generated stories.

    -   **Data/UI Elements:** Keep the small data points (like PM2.5 numbers) in a clean Sans-Serif (Inter or Roboto) to maintain clarity.

**Case Study 2: No Thanks**

-   **The Goal:** A professional tool that helps people say "no," balancing a corporate SaaS feel with the warmth of a therapy tool.

-   **The Problem:** Finding the right "temperature." A standard Sans-Serif (like Helvetica) feels too cold and robotic. A Serif feels too old-fashioned.

-   **Professor's Prescription:** \* Use a **Humanist Sans-Serif** (人文主义无衬线体). Fonts like Nunito, DM Sans, or Lato. These fonts have the clean lines of modern tech, but the letterforms have subtle curves that mimic natural human handwriting. They feel approachable, safe, and empathetic---perfect for a tool dealing with workplace anxiety.

**🛠️ Part 3: Best Practices to Break the "Generic AI" Mold**

*(Note: These are advanced industry tips from your Professor to elevate your web design.)*

How do you stop your AI from building boring websites? By forcing it to use **Extreme Contrast (极端的反差)**.

1.  **The Rule of Two (双字体法则):** Never use more than two font families. Pair a bold, expressive font for your Headers with a neutral, highly readable font for your Body.

2.  **Scale Contrast (字号比例反差):** AI defaults to boring sizes (e.g., 24px header, 16px body). To look like a premium designer, push the extremes. Make your H1 massive (e.g., 64px or text-6xl in Tailwind) and keep your secondary text small and subtle (14px in a muted gray).

**💻 Part 4: Prompt for Math, Not Vibes**

As discussed in your previous notes, Claude Code is a brilliant but literal intern. If you ask for a "vibe," it will guess poorly. You must translate CalArts theory into code instructions.

**❌ Amateur Prompt (Vibe-based):**

"Update the Smoke Story website to make the typography look like a luxurious newspaper and make it less tiring to read. Make it look professional."

**✅ Professional Prompt (Math-based):**

"I want to apply strict typography rules to the Smoke Story UI. Update the CSS/Tailwind:

1.  Set all H1 and H2 headers to the 'Playfair Display' font family to establish a luxurious editorial aesthetic.

2.  Set the main story body text to 'Lora' or 'Georgia'.

3.  Enforce the CalArts rule for 'Measure' by limiting the width of the story container to a maximum of 65 characters (max-w-prose in Tailwind).

4.  Increase the 'Leading' of the body text to 1.6 (leading-relaxed) to reduce reading fatigue.

5.  Create extreme scale contrast: Make the main title text extremely large (text-5xl) and the UI labels small and muted (text-sm text-gray-500)."

**Part 5: Typography Psychology (The Visual Tone of Voice) \-\--**

### 1. 衬线体 (Serif)

-   **The Vibe:** Authority, tradition, elegance, luxury, and editorial credibility.

-   **The Subtext:** "This is a serious, thoroughly researched report" or "This is a premium, high-end product."

-   **Best For:** Serious journalism (like your *Smoke Story* project), premium brands, and long-form reading experiences.

-   **Classic Examples:** Playfair Display, Merriweather, Lora, Georgia.

### 2. 无衬线体 (Sans-Serif)

在现代设计中，无衬线体需要被细分为三种完全不同的性格：

**A. 几何无衬线 (Geometric Sans)**

-   **The Vibe:** Objective, cold, futuristic, and mathematically perfect.

-   **Best For:** Tech startup landing pages, avant-garde art, or hard data dashboards.

-   **Classic Examples:** Futura, Montserrat.

**B. 人文无衬线 (Humanist Sans)**

-   **The Vibe:** Warm, empathetic, approachable, and conversational. The letterforms mimic natural human handwriting.

-   **Best For:** Coaching tools, therapy-like applications (like your *No Thanks* project), or any UI where you want the user to feel safe, understood, and unpressured.

-   **Classic Examples:** Nunito, Lato, DM Sans.

**C. 新无衬线 / 中立无衬线 (Neo-Grotesque)**

-   **The Vibe:** Neutral, efficient, invisible, and utility-focused. It doesn't distract the user with personality.

-   **Best For:** SaaS dashboards, system menus, and complex data tables. (Note: AI defaults to this, which is why AI websites often feel "generic").

-   **Classic Examples:** Inter, Helvetica, Roboto.

### 3. 等宽字体 (Monospace)

-   **The Vibe:** Geeky, raw data, absolute transparency, and "behind-the-scenes" authenticity.

-   **The Subtext:** "You are looking at the raw, unfiltered truth."

-   **Best For:** Presenting code blocks, hard scientific metrics, or terminal-like developer tools.

-   **Classic Examples:** JetBrains Mono, Fira Code, Space Mono.

### 4. 圆体 (Rounded)

-   **The Vibe:** Extremely safe, friendly, harmless, and playful.

-   **Best For:** Habit trackers, children's education apps, or mental health check-ins.

-   **Classic Examples:** Quicksand, Varela Round.

**Professor's Final Note:** By understanding the anatomy of type (CalArts) and combining it with deterministic AI prompting (Math, not Vibes), you are no longer just a coder generating templates---you are an **Art Director** building bespoke digital experiences.

\-\-\-\-\-\-\-\-\-\-\--Chinese\-\-\-\-\-\-\-\--

这是一个极其核心且专业的问题。欢迎来到排版学最迷人的部分：**字体心理学（Typography Psychology）**。

正如我们在之前的笔记中提到的，**字体不仅仅是文字的外壳，它是文字的"视觉表情"和"语气"**。用户在读懂字面意思之前，潜意识就已经接收到了字体传递的情绪。

作为你的 AI 教授，我为你全面总结了现代 Web 设计中最常用的五大字体家族，以及它们各自给用户带来的潜意识感受：

**1. 衬线体 (Serif) ------ "穿西装的学者与贵族"**

衬线体就是字母笔画末尾有"小尾巴"或"装饰角"的字体。

-   **给人带来的感觉：** 权威、可信、传统、优雅、奢华、充满历史底蕴与文学性。

-   **用户潜意识：** "这是一篇严肃的报道"、"这个品牌很有底蕴"、"这是一个高端/昂贵的产品"。

-   **适用场景：** 报纸型媒体、严肃文学、高端奢侈品、深度阅读的长文。

-   **对你的项目启发：** 你的 **Smoke Story** 讲述的是严肃的气候与灾难故事，使用高对比度的衬线体（如 Playfair Display）做标题，能瞬间赋予它《纽约时报》般的历史厚重感和权威感。

-   **经典代表：** Georgia, Playfair Display, Merriweather, Lora

**2. 无衬线体 (Sans-Serif) ------ "穿高领毛衣的科技精英"**

无衬线体去掉了所有多余的装饰，线条干净利落。但在现代设计中，它被细分为了三种截然不同的性格：

-   **A. 几何无衬线 (Geometric Sans)：绝对理性**

    -   **感觉：** 冰冷、客观、极简、未来感、几何学上的完美。

    -   **代表字体：** Futura, Montserrat

    -   **适用场景：** 科技公司的宣发、前卫艺术博物馆、硬核数据看板。

-   **B. 人文无衬线 (Humanist Sans)：温暖的对话**

    -   **感觉：** 亲和力、同理心、人类手写的温度、平易近人。

    -   **代表字体：** Lato, Nunito, DM Sans

    -   **对你的项目启发：** 你的 **No Thanks** 既是工具又是"教练"。如果你用几何字体会显得太冷漠；如果你用人文无衬线体（比如带点圆润感的 Nunito），就能让用户在拒绝别人时感到被理解、没有心理压力。

-   **C. 新无衬线 (Neo-Grotesque)：绝对中立**

    -   **感觉：** 高效、透明、不存在感、工具属性极强。

    -   **代表字体：** Inter, Helvetica, Roboto

    -   **适用场景：** SaaS 后台界面、系统菜单。AI 经常默认用这种字体，这就是为什么很多 AI 网站看起来像"毫无感情的通用模板"。

**3. 等宽字体 (Monospace) ------ "硬核工程师与打字机"**

每个字母占据绝对相同的宽度（比如 i 和 w 一样宽）。

-   **给人带来的感觉：** 极客、原始数据、绝对的透明、未经修饰的真实感、机密文件。

-   **用户潜意识：** "这是幕后的真实数据"、"这是黑客或程序员看到的东西"。

-   **适用场景：** 呈现代码、展示非常硬核的技术指标或图表坐标系。

-   **经典代表：** JetBrains Mono, Fira Code, Space Mono

**4. 圆体 (Rounded) ------ "无害的守护者"**

字母的端点被做成了圆角处理。

-   **给人带来的感觉：** 极度安全、友好、无害、活泼、甚至是稚气。

-   **用户潜意识：** "这里很安全，你不会犯错"。

-   **适用场景：** 儿童教育产品、习惯打卡 App、心理疗愈类轻量级产品。

-   **经典代表：** Quicksand, Varela Round

**5. 手写体/展示体 (Script / Display) ------ "舞台上的表演者"**

模仿人类书法、毛笔或签名的字体，或者造型极其夸张的字体。

-   **给人带来的感觉：** 强烈的个人化、独特、手工定制感、或者极具情绪张力。

-   **使用警告：** **永远不要用于正文！** 这类字体辨识度极低，只适合用作网站 Logo 或者一句非常短的 Slogan 点缀。

-   **经典代表：** Pacifico, Dancing Script

**🎓 教授的排版心法 (Professor's Rule of Thumb)**

当你下次使用 Claude Code 设计网页时，不要再让 AI 随便选字体了。你可以像一个真正的 Art Director（艺术总监）一样思考：

1.  **设定主角与配角：** 一个网站最多只需要**两种**情绪。比如，**Smoke Story** 可以用 Playfair Display（衬线体/权威主角）作为大标题，用 Inter（无衬线体/高效配角）作为小字号的数据说明。

2.  **用 Prompt 描述情绪：** 以后给 AI 写代码指令时，你可以直接说：

*"Claude, I want the heading to feel historical, luxurious, and authoritative. Please use a serif font like 'Playfair Display'. For the interactive UI buttons, I want them to feel neutral and modern, so use a neo-grotesque sans-serif like 'Inter'."*

你现在是不是对如何给你的两个项目"定调子"有更清晰的想法了？
