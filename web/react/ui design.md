
## 🚀 7-Day Modern UI Design Roadmap

### 🟢 Day 1 — Design Fundamentals

আজ শুধু এগুলো শিখবে:

- Spacing
- Typography
- Colors
- Border radius
- Shadows
- Alignment
- Visual hierarchy
- `8px spacing system`

উদাহরণ:

```
Heading
↓ 8px
Description
↓ 24px
Button
```

Tailwind-এ:

```
<h1 className="text-3xl font-bold">
  Build faster
</h1>

<p className="mt-2 text-gray-500">
  Create beautiful interfaces.
</p>

<button className="mt-6 rounded-xl px-6 py-3">
  Get Started
</button>
```

**আজকের project:**  
একটা simple Hero Section বানাবে।

---

### 🔵 Day 2 — Modern Color + Typography

শিখবে:

- Primary / Secondary color
- Neutral colors
- Background
- Text hierarchy
- Font weight
- Gradient
- Dark UI

একটা সাধারণ rule:

```
Background → #f8fafc
Heading    → #0f172a
Body       → #64748b
Primary    → #2563eb
Border     → #e2e8f0
```

Tailwind:

```
<div className="bg-slate-50 text-slate-900">
```

**Project:**  
👉 SaaS Hero Section

---

### 🟣 Day 3 — Cards & Components

আজ তোমার আগের প্রশ্নের জিনিসগুলো।

শিখবে:

- Card
- Button
- Badge
- Avatar
- Input
- Navbar
- Feature section

বিশেষ করে:

```
Normal
Hover
Active
Focus
Disabled
```

যেমন:

```
<button
  className="
    rounded-xl
    bg-blue-600
    px-5 py-3
    text-white
    transition
    hover:-translate-y-1
    hover:bg-blue-700
    hover:shadow-lg
  "
>
  Get Started
</button>
```

**Project:**  
👉 3টা Feature Card + CTA

---

### 🟠 Day 4 — Layout Mastery

এটা খুব important।

শিখবে:

- Flexbox
- Grid
- Container
- Responsive design
- `gap`
- `max-w`
- `grid-cols`

যেমন:

```
<div className="
  grid
  gap-6
  sm:grid-cols-2
  lg:grid-cols-3
">
```

তারপর:

```
Mobile
   ↓
Tablet
   ↓
Desktop
```

একই design তিনটা screen-এ সুন্দর রাখতে হবে।

**Project:**  
👉 Pricing Section

---

### 🔴 Day 5 — Modern Effects

এখানে তুমি তোমার আগের animated border-এর মতো effects শিখবে।

শিখবে:

- Gradient
- Blur
- Glow
- Glassmorphism
- Gradient border
- Hover animation
- Transform
- Transition
- `::before`
- `::after`

যেমন:

```
<div className="
  rounded-2xl
  border border-white/10
  bg-white/5
  backdrop-blur-xl
  shadow-2xl
">
```

আর animated border:

```
background: conic-gradient(
  #3b82f6,
  #8b5cf6,
  #06b6d4,
  #3b82f6
);
```

**Project:**  
👉 Modern AI Card

---

### 🟡 Day 6 — Real Website Copy

আজ tutorial দেখে বানাবে না।

একটা modern website দেখে **নিজে recreate করবে**।

যেমন:

```
Navbar
   ↓
Hero
   ↓
Features
   ↓
Stats
   ↓
Pricing
   ↓
CTA
   ↓
Footer
```

প্রথমে screenshot দেখবে।

তারপর নিজেকে প্রশ্ন করবে:

> “এই spacing কেন এমন?”

> “এই font size কেন এমন?”

> “এই color কোথায় ব্যবহার হয়েছে?”

> “Card-এর hierarchy কী?”

তারপর Tailwind দিয়ে বানাবে।

**এটাই তোমার সবচেয়ে গুরুত্বপূর্ণ দিন।**

---

# 🔥 Day 7 — Full UI Challenge

শেষ দিনে একটা complete project বানাবে।

আমি হলে তোমাকে এই project দিতাম:

### **Modern Developer Portfolio**

```
┌──────────────────────────────────┐
│ Logo       Home Work About  ☼    │
├──────────────────────────────────┤
│                                  │
│        Hey, I'm Developer        │
│        I build modern web apps   │
│                                  │
│    [ View Work ] [ Contact ]     │
│                                  │
├──────────────────────────────────┤
│                                  │
│        Featured Projects         │
│                                  │
│   ┌──────┐ ┌──────┐ ┌──────┐    │
│   │ Card │ │ Card │ │ Card │    │
│   └──────┘ └──────┘ └──────┘    │
│                                  │
├──────────────────────────────────┤
│          My Skills               │
│                                  │
│ HTML  CSS  JS  React  Tailwind   │
│                                  │
├──────────────────────────────────┤
│                                  │
│       Let's work together        │
│          [ Contact Me ]           │
│                                  │
└──────────────────────────────────┘
```

## ⏰ প্রতিদিন কতক্ষণ?

প্রতিদিন **৩–৪ ঘণ্টা** দিলে যথেষ্ট।

আমি এইভাবে ভাগ করতাম:

```
45 min → শেখা
30 min → অন্যের design observe
90 min → নিজে coding
30 min → নিজের design improve
15 min → কী শিখলে লিখে রাখা
```

### সবচেয়ে গুরুত্বপূর্ণ rule

**Tutorial দেখে শুধু copy করবে না।**

এই cycle follow করো:

> 👀 **Observe → 🧠 Analyze → 💻 Build → 🔧 Improve → 🔁 Repeat**

আর একটা জিনিস—**প্রতিদিন নতুন নতুন effect শেখার চেষ্টা না করে একই component বারবার polish করো।** Modern UI আসলে অনেকটা `spacing + typography + color + hierarchy + consistency`-এর খেলা।

তুমি চাইলে আমি তোমার জন্য **Day 1 থেকে Day 7 পর্যন্ত প্রতিদিনের exact task + Tailwind practice + mini project + checklist** দিয়ে একটা সম্পূর্ণ ৭ দিনের course বানিয়ে দিতে পারি।

  
----
অবশ্যই। আমরা **Day 1 → Day 7** এভাবে ধাপে ধাপে যাব। তুমি যখন `Day 1` বলবে, আমি সেই দিনের প্রতিটা topic **কেন লাগে + কখন ব্যবহার করতে হয় \+ Tailwind code + ছোট practice** সহ বুঝিয়ে দেব।

 # 🟢 Day 1 — Modern UI Design Fundamentals

 আজকের লক্ষ্য:

 > **একটা UI সুন্দর দেখানোর পেছনে আসলে কী কাজ করে সেটা বোঝা।**

 আজ ৬টা জিনিস শিখবে:

 1. Spacing
2. Typography
3. Color
4. Border Radius
5. Shadow
6. Visual Hierarchy

---

 # 1️⃣ Spacing — সবচেয়ে গুরুত্বপূর্ণ

 Modern UI-এর অনেকটাই **ঠিক spacing**-এর উপর নির্ভর করে।

 ধরো:

```
❌ খারাপ

Title
Description
Button
```

 সবকিছু যদি গায়ে গায়ে থাকে, UI cramped লাগবে।

 বরং:

```
✅ ভালো

Title

Description

Button
```

 Tailwind:

```
<h1 className="text-3xl font-bold">
  Build faster
</h1>

<p className="mt-3 text-gray-500">
  Create beautiful websites faster.
</p>

<button className="mt-6 rounded-xl bg-blue-600 px-5 py-3 text-white">
  Get Started
</button>
```

 এখানে:

```
mt-3 → Description-এর উপরে spacing
mt-6 → Button-এর উপরে বেশি spacing
```

 ### Golden Rule

 Tailwind-এ spacing হিসেবে সাধারণত:

```
4
8
12
16
24
32
48
64
```

 এই ধরনের consistent spacing ব্যবহার করলে design অনেক clean হয়।

---

 # 2️⃣ Typography

 Typography মানে শুধু font সুন্দর হওয়া না।

 এর মধ্যে আছে:

 - Font size
- Font weight
- Line height
- Letter spacing
- Text hierarchy

 ধরো:

```
BIG TITLE

ছোট description

Button
```

 Tailwind:

```
<h1 className="text-4xl font-bold leading-tight">
  Build modern websites
</h1>

<p className="mt-4 text-lg leading-7 text-gray-500">
  Create beautiful interfaces using Tailwind CSS.
</p>
```

 এখানে:

```
text-4xl    → বড় heading
font-bold   → গুরুত্ব বেশি
leading-tight → line height
text-lg     → paragraph একটু বড়
text-gray-500 → secondary text
```

 ### একটা গুরুত্বপূর্ণ rule

 সব text একই size করলে UI boring হয়ে যায়।

 বরং:

```
Heading      → 36px / 48px
Subheading   → 20px
Body         → 16px
Small text   → 14px
```

 এভাবে hierarchy তৈরি করো।

---

 # 3️⃣ Color

 একটা modern UI-তে অনেকগুলো random color ব্যবহার করা উচিত না।

 একটা simple palette রাখো:

```
Background → Slate-50
Heading    → Slate-900
Body       → Slate-600
Border     → Slate-200
Primary    → Blue-600
```

 Tailwind:

```
<div className="bg-slate-50 text-slate-900">

  <h1 className="text-4xl font-bold">
    Build faster
  </h1>

  <p className="text-slate-600">
    Create modern websites.
  </p>

</div>
```

 ### Color hierarchy

```
████████  Primary
██████    Secondary
████      Body
██        Muted
```

 সব জায়গায় blue ব্যবহার করার দরকার নেই।

 **Color দিয়ে গুরুত্ব বোঝাতে হয়।**

---

 # 4️⃣ Border Radius

 Modern UI-তে rounded corner অনেক বেশি ব্যবহার হয়।

 Tailwind:

```
<div className="rounded-xl">
```

 আরও:

```
rounded-lg
rounded-xl
rounded-2xl
rounded-3xl
```

 উদাহরণ:

```
<div className="rounded-2xl bg-white p-6">
  Card
</div>
```

 ### কিন্তু সবকিছু অতিরিক্ত round করো না

 যেমন:

```
Card       → rounded-2xl
Button     → rounded-xl
Input      → rounded-lg
```

 Consistency গুরুত্বপূর্ণ।

---

 # 5️⃣ Shadow

 Shadow-এর কাজ হলো element-কে background থেকে আলাদা করা।

```
<div className="
  rounded-2xl
  bg-white
  p-6
  shadow-lg
">
  Card
</div>
```

 Tailwind shadows:

```
shadow-sm
shadow
shadow-md
shadow-lg
shadow-xl
shadow-2xl
```

 ### Modern UI-তে subtle shadow ভালো

 ❌

```
box-shadow: 0 20px 50px black;
```

 অনেক dark shadow UI-কে heavy করে।

 ✅

```
shadow-xl shadow-blue-500/10
```

 এটা অনেক subtle।

---


হ্যাঁ, Tailwind CSS-এ **shadow-এর color** দিতে পারো। 🔥

 ### সহজভাবে

 তোমার code:

```
<div className="
  rounded-2xl
  bg-white
  p-6
  shadow-lg
">
  Card
</div>
```

 এখানে `shadow-lg`-এর সাথে color:

```
<div className="
  rounded-2xl
  bg-white
  p-6
  shadow-lg
  shadow-blue-500/30
">
  Card
</div>
```

 এখানে:

```
shadow-lg          → shadow কতটা বড়
shadow-blue-500    → shadow-এর color
/30                → 30% opacity
```

 ### কিছু সুন্দর combination

 **Blue glow:**

```
shadow-xl shadow-blue-500/30
```

 **Purple:**

```
shadow-xl shadow-purple-500/30
```

 **Green:**

```
shadow-xl shadow-green-500/25
```

 **Pink:**

```
shadow-xl shadow-pink-500/30
```

 **Black subtle shadow:**

```
shadow-lg shadow-black/10
```

---

 ### 🔥 Modern card-এর জন্য আমার পছন্দ

```
<div className="
  rounded-2xl
  border border-slate-200
  bg-white
  p-6
  shadow-xl shadow-blue-500/10
  transition-all duration-300
  hover:-translate-y-1
  hover:shadow-xl hover:shadow-blue-500/20
">
  Card
</div>
```

 এতে normal অবস্থায় **হালকা blue shadow**, আর hover করলে shadow একটু বেশি visible হবে।

 আর যদি **নিজের custom hex color** দিতে চাও, সেটাও Tailwind-এ করা যায়:

```
shadow-[0_10px_40px_#3b82f640]
```

 এখানে `#3b82f640` হলো blue color \+ transparency।

 **Modern UI-তে সাধারণত shadow খুব subtle রাখাই ভালো**—`/10`, `/20`, `/30` দিয়ে শুরু করে দেখো।


---

 # 6️⃣ Visual Hierarchy ⭐

 এটা আজকের সবচেয়ে গুরুত্বপূর্ণ concept।

 User যেন দেখেই বুঝতে পারে:

```
1. কী গুরুত্বপূর্ণ?
2. কী পড়তে হবে?
3. কোথায় click করতে হবে?
```

 যেমন:

```
        Build Your Future
          ↑ সবচেয়ে বড়

  Learn modern web development
          ↑ secondary

       [ Get Started ]
          ↑ action
```

 Tailwind:

```
<div className="text-center">

  <h1 className="text-5xl font-bold text-slate-900">
    Build Your Future
  </h1>

  <p className="mt-4 text-lg text-slate-500">
    Learn modern web development.
  </p>

  <button className="
    mt-8
    rounded-xl
    bg-blue-600
    px-6 py-3
    font-semibold
    text-white
  ">
    Get Started
  </button>

</div>
```

 এখানে চোখ প্রথমে যাবে:

 **Heading → Description → Button**

 এটাই Visual Hierarchy।

---

 # 🧪 Day 1 Practice

 এখন তুমি **এই Hero Section নিজে বানাবে**:

```
              ┌──────────────────────────┐

                   Build Better UI

              Create modern interfaces
                 with Tailwind CSS.

                 [ Get Started ]

              └──────────────────────────┘
```

 ### Requirements

 ব্যবহার করবে:

 - `max-w`
- `mx-auto`
- `text-*`
- `font-*`
- `leading-*`
- `mt-*`
- `px-*`
- `py-*`
- `rounded-*`
- `bg-*`
- `text-*`
- `shadow-*`

 **কোনো animation ব্যবহার করবে না।**

 কারণ আজকের লক্ষ্য হলো আগে **basic design sense** তৈরি করা।

---

 ## 🎯 Day 1-এর Challenge

 এই design-টা নিজের মতো করে বানাও:

```
<div className="min-h-screen bg-slate-50">

  {/* তোমার Hero এখানে */}

</div>
```

 তারপর নিজের চোখে দেখো এবং ৩টা প্রশ্ন করো:

 **① Heading কি সবচেয়ে বেশি চোখে পড়ছে?**

 **② Description আর heading-এর মধ্যে যথেষ্ট spacing আছে?**

 **③ Button কি clearly clickable মনে হচ্ছে?**

 এই ৩টা ঠিক করতে পারলে তুমি আজকের মূল lesson বুঝে ফেলেছো।

 **পরের ধাপে Day 2 হবে → Color + Typography আরও গভীরভাবে, এবং একটা real SaaS Hero বানাবো।**

----
# 🟣 Day 2 — Color \+ Typography

 আজকের লক্ষ্য হলো **UI-তে কোন color কোথায় এবং কোন text কতটা prominent হবে**—এটা বুঝতে শেখা।

 Day 1-এ আমরা spacing, hierarchy ইত্যাদি দেখেছি। আজ এগুলোকে আরও professional করব।

---

 ## 1️⃣ Color Palette কী?

 একটা website-এ ২০টা color ব্যবহার করার দরকার নেই।

 Modern UI-তে সাধারণত একটা **ছোট color system** থাকে।

 ধরো:

```
Background  → Slate 50
Card        → White
Heading     → Slate 900
Body        → Slate 600
Muted       → Slate 400
Border      → Slate 200
Primary     → Blue 600
```

 Tailwind:

```
<div className="bg-slate-50">
```

 Heading:

```
<h1 className="text-slate-900">
```

 Paragraph:

```
<p className="text-slate-600">
```

 Border:

```
<div className="border border-slate-200">
```

---

 # 2️⃣ 60–30–10 Rule

 Color balance বোঝার জন্য একটা useful rule:

```
60% → Background
30% → Secondary color
10% → Primary / Accent
```

 উদাহরণ:

```
████████████████████  Slate background
██████████            White/card
██                    Blue accent
```

 ধরো একটা SaaS website:

```
<body className="bg-slate-50">

  <div className="bg-white">

    <h1 className="text-slate-900">
      Build faster
    </h1>

    <p className="text-slate-600">
      Create beautiful products.
    </p>

    <button className="bg-blue-600 text-white">
      Get Started
    </button>

  </div>

</body>
```

 এখানে blue শুধু **important action**-এর জন্য।

 এটাই ভালো practice।

---

 # 3️⃣ একই Color-এর Shade ব্যবহার করো

 ধরো Blue ব্যবহার করছো।

 এভাবে random blue না:

```
#0000ff
#00aaff
#0088ff
#1234ff
```

 বরং Tailwind-এর shade ব্যবহার করো:

```
blue-50
blue-100
blue-200
blue-400
blue-500
blue-600
blue-700
blue-900
```

 উদাহরণ:

```
<div className="bg-blue-50">
```

```
<button className="bg-blue-600 hover:bg-blue-700">
```

```
<span className="text-blue-600">
```

 এতে পুরো website-এর color consistent থাকে।

---

 # 4️⃣ Dark UI-তে Color

 Modern dark UI-তে pure black সবসময় ভালো লাগে না।

 ❌

```
<div className="bg-black">
```

 বরং:

```
<div className="bg-slate-950">
```

 তারপর:

```
<h1 className="text-white">
```

 Body:

```
<p className="text-slate-400">
```

 Border:

```
border border-white/10
```

 একটা সুন্দর dark card:

```
<div className="
  rounded-2xl
  border border-white/10
  bg-slate-900
  p-6
">
  <h2 className="text-xl font-semibold text-white">
    TypeScript
  </h2>

  <p className="mt-2 text-slate-400">
    Learn TypeScript from basics to advanced.
  </p>
</div>
```

---

 # 5️⃣ Typography Hierarchy ⭐

 এবার text।

 একটা website-এ সব text যদি একই রকম হয়:

```
Title
Description
Button
Footer
```

 তাহলে user বুঝতে পারবে না কোনটা important।

 তাই hierarchy:

```
H1      → সবচেয়ে বড়
H2      → বড়
H3      → medium
Body    → normal
Caption → ছোট
```

 Tailwind example:

```
<h1 className="text-5xl font-bold">
  Build modern websites
</h1>

<h2 className="text-3xl font-semibold">
  Powerful features
</h2>

<h3 className="text-xl font-semibold">
  Fast development
</h3>

<p className="text-base text-slate-600">
  Build beautiful interfaces with Tailwind CSS.
</p>

<span className="text-sm text-slate-400">
  Updated today
</span>
```

---

 # 6️⃣ Font Weight

 শুধু font-size দিয়ে hierarchy তৈরি হয় না।

 Weight-ও গুরুত্বপূর্ণ।

 Tailwind:

```
font-normal
font-medium
font-semibold
font-bold
font-extrabold
```

 সাধারণত:

```
H1       → font-bold
H2       → font-semibold
Body     → font-normal
Button   → font-medium / semibold
```

 উদাহরণ:

```
<h1 className="text-4xl font-bold">
  Build faster
</h1>

<p className="font-normal text-slate-600">
  Create amazing websites.
</p>

<button className="font-semibold">
  Get Started
</button>
```

---

 # 7️⃣ Line Height — খুবই গুরুত্বপূর্ণ

 এইটা beginner-রা অনেক সময় ignore করে।

 ধরো:

```
This is a very long paragraph that
contains multiple lines and becomes
hard to read.
```

 Line অনেক কাছাকাছি হলে uncomfortable।

 Tailwind:

```
<p className="leading-7">
```

 Heading-এর জন্য:

```
<h1 className="leading-tight">
```

 সাধারণ pattern:

```
Heading     → leading-tight
Paragraph   → leading-6 / leading-7
```

---

 # 8️⃣ Letter Spacing

 Tailwind-এ:

```
tracking-tight
tracking-normal
tracking-wide
tracking-wider
```

 Large heading-এ:

```
<h1 className="
  text-5xl
  font-bold
  tracking-tight
">
  Build better products
</h1>
```

 এতে বড় heading আরও polished লাগে।

---

 # 🧩 এখন সব একসাথে

 একটা modern Hero:

```
<section className="min-h-screen bg-slate-50">

  <div className="mx-auto max-w-5xl px-6 py-24">

    <span className="
      rounded-full
      bg-blue-50
      px-4 py-2
      text-sm
      font-medium
      text-blue-600
    ">
      ✨ Modern Development
    </span>

    <h1 className="
      mt-6
      max-w-3xl
      text-5xl
      font-bold
      leading-tight
      tracking-tight
      text-slate-900
    ">
      Build beautiful websites faster.
    </h1>

    <p className="
      mt-5
      max-w-2xl
      text-lg
      leading-7
      text-slate-600
    ">
      Create modern, responsive and beautiful
      interfaces using Tailwind CSS.
    </p>

    <button className="
      mt-8
      rounded-xl
      bg-blue-600
      px-6 py-3
      font-semibold
      text-white
      shadow-lg shadow-blue-600/20
      transition
      hover:bg-blue-700
    ">
      Get Started →
    </button>

  </div>

</section>
```

 এখানে লক্ষ্য করো:

```
Color
 ↓
Typography
 ↓
Hierarchy
 ↓
Spacing
 ↓
Button
```

 সবকিছু একসাথে কাজ করছে।

---

 # 🎯 Day 2 Challenge

 নিজে একটা **SaaS Hero Section** বানাও।

 তোমার UI-তে থাকবে:

```
[ ✨ New Feature ]

Build your next
great product.

Short description goes here.

[ Get Started ]  [ Learn More ]
```

 ### Rules

 শুধু এইগুলো ব্যবহার করবে:

 - `slate-*`
- `blue-*`
- `text-*`
- `font-*`
- `leading-*`
- `tracking-*`
- `max-w-*`
- `mt-*`
- `px-*`
- `py-*`
- `rounded-*`
- `shadow-*`

 **কোনো gradient, animation, glassmorphism ব্যবহার করবে না।**

 কারণ Day 2-এর আসল skill হলো **simple color + typography দিয়েই সুন্দর UI বানাতে পারা।**

 ### 🧠 আজকের ৩টা জিনিস মনে রাখবে

 > **কম color = বেশি consistency**

 > **Typography = শুধু font-size না**

 > **Good UI = Hierarchy \+ Contrast + Spacing**

 Day 3-এ আমরা **Cards + Buttons + Inputs \+ Badges + Hover/Focus states** দিয়ে proper component design শিখব।

----
# 🔵 Day 3 — Components: Card, Button, Badge & Input

 আজকের লক্ষ্য:

 > **একটা সুন্দর UI না, বরং reusable সুন্দর UI component বানানো।**

 Day 1 → Spacing + Hierarchy\
 Day 2 → Color + Typography\
 **Day 3 → Components + Interaction**

 আজ আমরা ৫টা component শিখব:

 1. Button
2. Card
3. Badge
4. Input
5. Hover / Focus state

---

 # 1️⃣ Button Design

 Beginnerরা অনেক সময় button শুধু এভাবে বানায়:

```
<button className="bg-blue-600 text-white px-5 py-3">
  Click Me
</button>
```

 কাজ করবে, কিন্তু modern UI-এর জন্য কিছু জিনিস দরকার:

 - Border radius
- Font weight
- Shadow
- Transition
- Hover
- Active state
- Focus

 ### Modern Button

```
<button
  className="
    rounded-xl
    bg-blue-600
    px-5 py-3
    font-semibold
    text-white

    shadow-lg
    shadow-blue-600/20

    transition-all
    duration-200

    hover:-translate-y-0.5
    hover:bg-blue-700
    hover:shadow-xl

    active:translate-y-0
  "
>
  Get Started →
</button>
```

 ### এখানে কী হচ্ছে?

```
rounded-xl
```

 Button-এর corner round করছে।

```
shadow-blue-600/20
```

 Blue-এর subtle glow।

```
transition-all duration-200
```

 Animation smooth করছে।

```
hover:-translate-y-0.5
```

 Mouse নিলে button একটু উপরে উঠবে।

```
active:translate-y-0
```

 Click করলে আবার নিচে আসবে।

---

 # 2️⃣ Button সবসময় একই রকম হবে না

 Modern website-এ সাধারণত কয়েক ধরনের button থাকে।

 ### Primary

```
<button className="
  rounded-xl
  bg-blue-600
  px-5 py-3
  font-semibold
  text-white
  hover:bg-blue-700
">
  Get Started
</button>
```

 ### Secondary

```
<button className="
  rounded-xl
  border border-slate-200
  bg-white
  px-5 py-3
  font-semibold
  text-slate-700
  hover:bg-slate-50
">
  Learn More
</button>
```

 ### Ghost

```
<button className="
  rounded-xl
  px-5 py-3
  font-medium
  text-slate-600
  hover:bg-slate-100
">
  View Docs
</button>
```

 এভাবে hierarchy তৈরি হয়:

```
Primary    → সবচেয়ে গুরুত্বপূর্ণ
Secondary  → দ্বিতীয় গুরুত্বপূর্ণ
Ghost      → কম গুরুত্বপূর্ণ
```

---

 # 3️⃣ Card Design ⭐

 এখন আসি Card-এ।

 একটা ভালো card-এর সাধারণ structure:

```
┌─────────────────────────┐
│                         │
│  Icon                   │
│                         │
│  Title                  │
│                         │
│  Description            │
│                         │
│  Action                 │
│                         │
└─────────────────────────┘
```

 Tailwind:

```
<div className="
  max-w-sm
  rounded-2xl
  border border-slate-200
  bg-white
  p-6
  shadow-sm
">

  <div className="
    flex h-12 w-12
    items-center justify-center
    rounded-xl
    bg-blue-50
    text-blue-600
  ">
    TS
  </div>

  <h2 className="
    mt-5
    text-xl
    font-semibold
    text-slate-900
  ">
    TypeScript
  </h2>

  <p className="
    mt-2
    leading-6
    text-slate-600
  ">
    Build scalable applications with
    powerful type safety.
  </p>

  <button className="
    mt-5
    font-semibold
    text-blue-600
    transition
    hover:text-blue-700
  ">
    Learn more →
  </button>

</div>
```

---

 # 4️⃣ Card-এর Border

 Basic:

```
border border-slate-200
```

 Dark UI:

```
border border-white/10
```

 Hover করলে:

```
hover:border-blue-300
```

 এভাবে:

```
<div className="
  rounded-2xl
  border border-slate-200
  bg-white
  p-6
  transition-all
  duration-300

  hover:-translate-y-1
  hover:border-blue-300
  hover:shadow-xl
">
```

 এখন card hover করলে:

```
      ↑
   Card উঠে যাবে

Border → blue
Shadow → বাড়বে
```

 এটাই modern card interaction।

---

 # 5️⃣ Badge

 Badge ছোট information highlight করার জন্য।

 যেমন:

```
NEW
PRO
POPULAR
BETA
FEATURED
```

 Tailwind:

```
<span className="
  inline-flex
  items-center
  rounded-full
  bg-blue-50
  px-3 py-1
  text-xs
  font-semibold
  text-blue-600
">
  NEW
</span>
```

 ### কেন `inline-flex`?

 কারণ badge-এর width যেন পুরো parent-এর width না নেয়।

---

 # 6️⃣ Input Design

 Modern input:

```
<input
  type="email"
  placeholder="Enter your email"
  className="
    w-full
    rounded-xl
    border border-slate-200
    bg-white
    px-4 py-3
    text-slate-900

    outline-none

    placeholder:text-slate-400

    transition

    focus:border-blue-500
    focus:ring-4
    focus:ring-blue-500/10
  "
/>
```

 এখানে সবচেয়ে গুরুত্বপূর্ণ:

```
focus:border-blue-500
```

 Input select করলে border blue হবে।

 আর:

```
focus:ring-4
focus:ring-blue-500/10
```

 একটা subtle blue glow তৈরি করবে।

---

 # 7️⃣ Hover বনাম Focus

 এটা খুব ভালোভাবে বুঝবে।

 ### Hover

 Mouse element-এর উপর গেলে:

```
hover:bg-blue-700
```

 ### Focus

 Input/button keyboard বা click দিয়ে active হলে:

```
focus:ring-4
```

 ### Active

 Click করার মুহূর্ত:

```
active:scale-95
```

 উদাহরণ:

```
<button className="
  rounded-xl
  bg-blue-600
  px-5 py-3
  text-white
  transition

  hover:bg-blue-700
  focus:outline-none
  focus:ring-4
  focus:ring-blue-500/30

  active:scale-95
">
  Click Me
</button>
```

---

 # 8️⃣ Group Hover 🔥

 এটা খুব important modern UI technique।

 ধরো Card-এর ভিতরের icon-ও hover করলে change করবে।

```
<div className="
  group
  rounded-2xl
  border border-slate-200
  p-6
  transition
  hover:-translate-y-1
">

  <div className="
    flex h-12 w-12
    items-center justify-center
    rounded-xl
    bg-blue-50
    text-blue-600
    transition

    group-hover:bg-blue-600
    group-hover:text-white
  ">
    TS
  </div>

  <h2 className="
    mt-5
    font-semibold
    text-slate-900
    transition
    group-hover:text-blue-600
  ">
    TypeScript
  </h2>

</div>
```

 এখানে:

```
Card hover
    ↓
Icon change
    ↓
Title change
```

 কারণ parent-এ:

```
group
```

 এবং child-এ:

```
group-hover:*
```

---

 # 9️⃣ তোমার Animated Border Card

 এবার আগের lesson-এর জিনিসটা Day 3-এর component-এর সাথে combine করি।

```
<div className="
  group
  relative
  overflow-hidden
  rounded-3xl
  p-[2px]
">

  {/* Animated border */}
  <div className="
    absolute
    inset-[-150%]
    bg-[conic-gradient(from_0deg,#3b82f6,#06b6d4,#8b5cf6,#3b82f6)]
    opacity-0
    transition
    duration-500
    group-hover:animate-spin
    group-hover:opacity-100
  " />

  {/* Content */}
  <div className="
    relative
    z-10
    rounded-[22px]
    bg-white
    p-6
  ">

    <span className="
      rounded-full
      bg-blue-50
      px-3 py-1
      text-xs
      font-semibold
      text-blue-600
    ">
      FEATURED
    </span>

    <h2 className="
      mt-5
      text-2xl
      font-bold
      text-slate-900
    ">
      TypeScript
    </h2>

    <p className="
      mt-3
      leading-7
      text-slate-600
    ">
      Build scalable and type-safe
      applications with TypeScript.
    </p>

    <button className="
      mt-6
      rounded-xl
      bg-blue-600
      px-5 py-3
      font-semibold
      text-white
      transition
      hover:bg-blue-700
      active:scale-95
    ">
      Learn More →
    </button>

  </div>
</div>
```

 এখানে আমরা Day 1 + Day 2 + Day 3 একসাথে ব্যবহার করছি:

```
Day 1
Spacing + Hierarchy
       ↓
Day 2
Color + Typography
       ↓
Day 3
Components + Interaction
       ↓
Modern Card
```

---

 # 🧪 Day 3 Challenge

 আজ তোমার কাজ:

 ### একটা **3-card Feature Section** বানাও।

```
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│     TS      │  │     ⚡      │  │     🔒      │
│             │  │             │  │             │
│ Type Safety │  │ Fast Build  │  │ Secure      │
│             │  │             │  │             │
│ Description │  │ Description │  │ Description │
│             │  │             │  │             │
│ Learn More  │  │ Learn More  │  │ Learn More  │
└─────────────┘  └─────────────┘  └─────────────┘
```

 ### Must use:

```
✓ rounded-2xl
✓ border
✓ shadow
✓ hover
✓ transition
✓ group
✓ group-hover
✓ badge
✓ button
✓ typography hierarchy
```

 **Animated border এখন optional**—আগে normal card-এর hover interaction ঠিকভাবে বানাও।

---

 ## 🧠 আজকের মূল lesson

 Modern component design-এর formula মনে রাখো:

```
Base
 ↓
Hover
 ↓
Focus
 ↓
Active
 ↓
Transition
 ↓
Consistency
```

 আর সবচেয়ে গুরুত্বপূর্ণ:

 > **UI শুধু সুন্দর static screenshot না। User যখন interact করবে তখন কী হবে—সেটাও design-এর অংশ।**

 **Day 4 → Layout Mastery:** `Flexbox + Grid + Container + Responsive Design`। এখান থেকেই তোমার cardগুলোকে proper full website layout-এ বসানো শুরু করব।


----
# 🟠 Day 4 — Layout Mastery: Flexbox + Grid \+ Responsive

 আজকের দিনটা খুব গুরুত্বপূর্ণ। কারণ তুমি যদি **layout ঠিকভাবে না জানো**, তাহলে সুন্দর card, button বানালেও পুরো website professional দেখাবে না।

 আজ শিখবে:

 1. `container` / `max-w`
2. Flexbox
3. Grid
4. `gap`
5. Responsive design
6. `justify-*`
7. `items-*`
8. Mobile-first thinking

---

 # 1️⃣ Container — Content কতটুকু জায়গা নেবে?

 ধরো desktop screen অনেক বড়:

```
|--------------------------------------------------------|
|                                                        |
|             Website Content                            |
|                                                        |
|--------------------------------------------------------|
```

 Content যদি পুরো screen জুড়ে থাকে, দেখতে ভালো লাগে না।

 তাই আমরা একটা maximum width রাখি:

```
<div className="mx-auto max-w-6xl px-6">
  Content
</div>
```

 এখানে:

```
mx-auto
```

 মানে horizontal center।

 আর:

```
max-w-6xl
```

 মানে content একটা maximum width-এর মধ্যে থাকবে।

 ### Common:

```
max-w-md
max-w-lg
max-w-xl
max-w-2xl
max-w-4xl
max-w-6xl
max-w-7xl
```

 Modern website-এ অনেক সময়:

```
<div className="mx-auto max-w-7xl px-6">
```

 দেখবে।

---

 # 2️⃣ Flexbox 🔥

 Flexbox ব্যবহার করো যখন elements এক direction-এ সাজাতে চাও।

 যেমন Navbar:

```
Logo                     Home  About  Contact
```

 Tailwind:

```
<nav className="flex items-center justify-between">
  <div>Logo</div>

  <div className="flex items-center gap-6">
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </div>
</nav>
```

 এখানে:

 ### `flex`

```
flex
```

 Children-গুলোকে flex layout-এ নেয়।

 ### `items-center`

```
items-center
```

 Vertical alignment center করে।

 ### `justify-between`

```
justify-between
```

 দুই পাশে space দেয়।

---

 # 3️⃣ `justify-*` বুঝে নাও

 Horizontal direction হলে:

```
justify-start
justify-center
justify-end
justify-between
justify-around
```

 সবচেয়ে বেশি ব্যবহার করবে:

```
justify-between
```

 এবং:

```
justify-center
```

---

 # 4️⃣ `items-*`

 Vertical alignment:

```
items-start
items-center
items-end
```

 সবচেয়ে common:

```
flex items-center
```

 Navbar:

```
<nav className="flex items-center justify-between">
```

---

 # 5️⃣ `gap` ⭐

 আগে আমরা `mt-*` দিয়ে spacing করতাম।

 কিন্তু multiple elements-এর মধ্যে spacing হলে `gap` অনেক clean।

```
<div className="flex gap-4">
  <button>One</button>
  <button>Two</button>
  <button>Three</button>
</div>
```

 এখন:

```
Button 1    16px    Button 2    16px    Button 3
```

 কারণ:

```
gap-4
```

 ### Common:

```
gap-2
gap-4
gap-6
gap-8
gap-12
```

---

 # 6️⃣ Flex Direction

 Default:

```
flex
```

 মানে row:

```
A  B  C
```

 Column:

```
flex flex-col
```

 তখন:

```
A
B
C
```

 Mobile layout-এ এটা খুব কাজে লাগে।

---

 # 7️⃣ Grid — Cards-এর জন্য ⭐⭐⭐

 তোমার 3টা card আছে:

```
┌──────┐ ┌──────┐ ┌──────┐
│ Card │ │ Card │ │ Card │
└──────┘ └──────┘ └──────┘
```

 Grid:

```
<div className="grid grid-cols-3 gap-6">

  <div>Card 1</div>
  <div>Card 2</div>
  <div>Card 3</div>

</div>
```

 `grid-cols-3` মানে:

```
| Card | Card | Card |
```

---

 # 8️⃣ Responsive Grid 🔥🔥

 এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ অংশ।

 Mobile-এ 3টা card পাশাপাশি রাখা যাবে না।

 তাই:

```
<div className="
  grid
  grid-cols-1
  gap-6
  md:grid-cols-2
  lg:grid-cols-3
">
```

 এর মানে:

```
Mobile
┌──────────┐
│ Card     │
├──────────┤
│ Card     │
├──────────┤
│ Card     │
└──────────┘

Tablet
┌──────┐ ┌──────┐
│ Card │ │ Card │
├──────┤ ├──────┤
│ Card │
└──────┘

Desktop
┌──────┐ ┌──────┐ ┌──────┐
│ Card │ │ Card │ │ Card │
└──────┘ └──────┘ └──────┘
```

 Tailwind-এর চিন্তাটা হলো:

```
Mobile first
    ↓
md:
    ↓
lg:
```

---

 # 9️⃣ Mobile First ⭐

 Tailwind-এ এটা খুব গুরুত্বপূর্ণ।

 এটা:

```
text-2xl md:text-4xl lg:text-6xl
```

 মানে:

```
Mobile  → text-2xl
Tablet  → text-4xl
Desktop → text-6xl
```

 আর:

```
px-4 md:px-8 lg:px-12
```

 মানে screen বড় হলে padding বাড়বে।

---

 # 🔟 Responsive Hero

 এবার সব combine করি।

```
<section className="bg-slate-50">

  <div className="
    mx-auto
    max-w-7xl
    px-6
    py-20
    lg:py-28
  ">

    <div className="
      grid
      items-center
      gap-12
      lg:grid-cols-2
    ">

      {/* Left */}
      <div>

        <span className="
          rounded-full
          bg-blue-50
          px-3 py-1
          text-sm
          font-semibold
          text-blue-600
        ">
          ✨ Modern UI
        </span>

        <h1 className="
          mt-6
          text-4xl
          font-bold
          leading-tight
          tracking-tight
          text-slate-900
          sm:text-5xl
        ">
          Build beautiful
          digital products.
        </h1>

        <p className="
          mt-5
          max-w-xl
          text-lg
          leading-7
          text-slate-600
        ">
          Create modern and responsive
          interfaces using Tailwind CSS.
        </p>

        <div className="
          mt-8
          flex
          flex-col
          gap-3
          sm:flex-row
        ">
          <button className="
            rounded-xl
            bg-blue-600
            px-6 py-3
            font-semibold
            text-white
          ">
            Get Started
          </button>

          <button className="
            rounded-xl
            border border-slate-200
            bg-white
            px-6 py-3
            font-semibold
            text-slate-700
          ">
            Learn More
          </button>
        </div>

      </div>

      {/* Right */}
      <div className="
        rounded-3xl
        border
        border-slate-200
        bg-white
        p-8
        shadow-xl
      ">
        Preview
      </div>

    </div>

  </div>

</section>
```

---

 # 🧠 এই code-টা বুঝো

 সবচেয়ে important অংশ:

```
grid
lg:grid-cols-2
```

 Mobile:

```
Text
 ↓
Preview
```

 Desktop:

```
Text       Preview
```

---

 # 1️⃣1️⃣ Responsive Card Section

 এবার তোমার TypeScript cardগুলো:

```
<section className="py-20">

  <div className="mx-auto max-w-7xl px-6">

    <div className="mx-auto max-w-2xl text-center">

      <h2 className="
        text-3xl
        font-bold
        tracking-tight
        text-slate-900
        sm:text-4xl
      ">
        Powerful Features
      </h2>

      <p className="
        mt-4
        text-slate-600
      ">
        Everything you need to build modern applications.
      </p>

    </div>

    <div className="
      mt-12
      grid
      grid-cols-1
      gap-6
      md:grid-cols-2
      lg:grid-cols-3
    ">

      <div className="rounded-2xl border p-6">
        Type Safety
      </div>

      <div className="rounded-2xl border p-6">
        Fast Development
      </div>

      <div className="rounded-2xl border p-6">
        Scalable
      </div>

    </div>

  </div>

</section>
```

 এখানে তুমি Day 1, 2, 3 এবং 4 একসাথে ব্যবহার করছো।

---

 # 🎯 Day 4-এর সবচেয়ে গুরুত্বপূর্ণ Cheat Sheet

 এগুলো মুখস্থ না করে **বারবার ব্যবহার করো**:

```
Layout
────────────────────

flex
flex-col
flex-row

items-center
items-start
items-end

justify-center
justify-between
justify-end

gap-4
gap-6
gap-8

Grid
────────────────────

grid
grid-cols-1
grid-cols-2
grid-cols-3

md:grid-cols-2
lg:grid-cols-3

Container
────────────────────

mx-auto
max-w-7xl
px-6

Responsive
────────────────────

sm:
md:
lg:
xl:
```

---

 # 🧪 Day 4 Challenge — Responsive Pricing Section

 আজ একটা **Pricing Section** বানাবে।

 Desktop:

```
        Pricing

 ┌────────┐ ┌────────┐ ┌────────┐
 │ Basic  │ │  Pro   │ │Enterprise│
 │        │ │ ⭐     │ │        │
 │ $10    │ │ $25    │ │ $50    │
 │        │ │        │ │        │
 │ Button │ │ Button │ │ Button │
 └────────┘ └────────┘ └────────┘
```

 Mobile:

```
┌──────────────┐
│ Basic        │
│ $10          │
│ Button       │
└──────────────┘

┌──────────────┐
│ Pro ⭐       │
│ $25          │
│ Button       │
└──────────────┘

┌──────────────┐
│ Enterprise   │
│ $50          │
│ Button       │
└──────────────┘
```

 ### Must use:

```
✓ max-w-7xl
✓ mx-auto
✓ px-6
✓ grid
✓ grid-cols-1
✓ md:grid-cols-2
✓ lg:grid-cols-3
✓ gap-6
✓ flex
✓ items-center
✓ justify-between
✓ responsive text
```

 **আজ animation নিয়ে চিন্তা করবে না।** তোমার লক্ষ্য হলো একই UI-কে **mobile → tablet → desktop** তিন জায়গায় সুন্দরভাবে বসানো।

---

 ## 🧠 আজকের Golden Rule

 > **আগে Mobile layout বানাও → তারপর `md:` → তারপর `lg:` দিয়ে বড় screen ঠিক করো।**

 আর একটা জিনিস খুব ভালোভাবে practice করো:

```
flex → one-dimensional layout
grid → multiple cards / two-dimensional layout
```

 **Day 5-এ যাব আমরা Modern Effects-এ — Gradient, Glow, Glassmorphism, Animated Border, Hover Animation এবং `before/after`।**

----

# 🟣 Day 5 — Modern UI Effects

 আজকের দিনটা একটু fun 😎

 Day 1 → Fundamentals\
 Day 2 → Color \+ Typography\
 Day 3 → Components\
 Day 4 → Layout\
 **Day 5 → Modern Effects ✨**

 আজ শিখবে:

 1. Gradient
2. Glow
3. Glassmorphism
4. Animated border
5. Hover animation
6. `before` / `after`
7. এগুলো কখন ব্যবহার করবে

---

 # 1️⃣ Gradient

 Modern UI-তে gradient খুব common।

 সবচেয়ে basic:

```
<div className="bg-gradient-to-r from-blue-500 to-purple-500">
```

 এর মানে:

```
Blue ───────────────→ Purple
```

 ### Text gradient

 এটা খুব popular:

```
<h1 className="
  bg-gradient-to-r
  from-blue-600
  to-purple-600
  bg-clip-text
  text-transparent
  text-5xl
  font-bold
">
  Build Something Amazing
</h1>
```

 ### এখানে কী হচ্ছে?

```
bg-gradient-to-r
```

 Left → Right gradient।

```
from-blue-600
to-purple-600
```

 Color শুরু ও শেষ।

```
bg-clip-text
text-transparent
```

 Gradient শুধু text-এর ভিতরে দেখা যাচ্ছে।

---

 # 2️⃣ Glow Effect 🔥

 Modern AI / SaaS website-এ glow অনেক দেখা যায়।

```
<div className="
  rounded-2xl
  bg-blue-600
  p-6
  shadow-[0_0_40px_rgba(37,99,235,0.35)]
">
  Glow Card
</div>
```

 আর Tailwind-এর built-in shadow দিয়েও:

```
shadow-xl shadow-blue-500/20
```

 এটা subtle glow।

 ### Button:

```
<button className="
  rounded-xl
  bg-blue-600
  px-6 py-3
  font-semibold
  text-white
  shadow-lg
  shadow-blue-600/30
">
  Get Started
</button>
```

---

 # 3️⃣ Glassmorphism 🧊

 এটা modern UI-র খুব popular effect।

 Basic idea:

```
Background
    ↓
Blur
    ↓
Semi-transparent card
```

 Tailwind:

```
<div className="
  rounded-2xl
  border border-white/20
  bg-white/10
  p-6
  backdrop-blur-xl
">
  Glass Card
</div>
```

 কিন্তু glass effect ভালোভাবে দেখতে background-এ কিছু color থাকা দরকার।

```
<div className="
  min-h-screen
  bg-gradient-to-br
  from-blue-600
  via-purple-600
  to-pink-500
  p-10
">

  <div className="
    mx-auto
    max-w-sm
    rounded-3xl
    border border-white/20
    bg-white/10
    p-8
    text-white
    backdrop-blur-xl
  ">
    <h2 className="text-2xl font-bold">
      Glass Card
    </h2>

    <p className="mt-3 text-white/70">
      Modern glassmorphism UI.
    </p>
  </div>

</div>
```

---

 # 4️⃣ Animated Border ⭐⭐⭐

 এটাই তুমি শুরুতে জানতে চেয়েছিলে।

 Concept:

```
Gradient
   ↓
Rotate
   ↓
Border-এর মধ্যে দেখা যাবে
```

 ### Basic version:

```
<div className="
  relative
  overflow-hidden
  rounded-2xl
  p-[2px]
">

  <div className="
    absolute
    inset-[-150%]
    animate-spin
    bg-[conic-gradient(#3b82f6,#8b5cf6,#06b6d4,#3b82f6)]
  " />

  <div className="
    relative
    z-10
    rounded-[14px]
    bg-slate-950
    p-6
    text-white
  ">
    Animated Border
  </div>

</div>
```

 ### Visual idea:

```
╭══════════════════════╮
║                      ║
║   Animated Border    ║
║                      ║
╰══════════════════════╯
        ↻
```

---

 # 5️⃣ `conic-gradient()` কী?

 এটা বুঝে ফেললে animated border অনেক সহজ।

 সাধারণ gradient:

```
linear-gradient(...)
```

 মানে:

```
──────→
```

 Conic gradient:

```
conic-gradient(...)
```

 মানে circular:

```
      ↑
   ↗  |  ↖
 ←────●────→
   ↘  |  ↙
      ↓
```

 তাই rotate করলে:

```
conic-gradient
       ↓
rotate()
       ↓
Animated border
```

---

 # 6️⃣ Hover Animation

 Static UI আর interactive UI-এর মধ্যে পার্থক্য এখানেই।

 ধরো card:

```
<div className="
  rounded-2xl
  border border-slate-200
  bg-white
  p-6
  transition-all
  duration-300

  hover:-translate-y-2
  hover:shadow-xl
">
```

 Mouse নিলে:

```
Card
 ↓
উপরে উঠবে
 ↓
Shadow বাড়বে
```

---

 # 7️⃣ Scale

 Image/card একটু বড় করতে:

```
hover:scale-105
```

 যেমন:

```
<div className="
  transition-transform
  duration-300
  hover:scale-105
">
  Card
</div>
```

 তবে খুব বেশি scale করো না।

 ❌

```
hover:scale-125
```

 সাধারণত subtle:

```
hover:scale-[1.02]
hover:scale-105
```

---

 # 8️⃣ `before` / `after` কেন লাগে?

 এটা খুব গুরুত্বপূর্ণ।

 ধরো একটা card-এর ভিতরে extra decorative glow দিতে চাও।

 HTML-এ আলাদা element না বানিয়েও pseudo-element ব্যবহার করতে পারো:

```
::before
::after
```

 Tailwind-এ:

```
<div className="
  relative
  before:absolute
  before:-inset-1
  before:rounded-2xl
  before:bg-blue-500/20
  before:blur-xl
">
```

 কিন্তু content যেন উপরে থাকে:

```
<div className="
  relative
  z-10
">
```

---

 # 9️⃣ Glow + Card

 একটা practical example:

```
<div className="
  group
  relative
  max-w-sm
">

  {/* Glow */}
  <div className="
    absolute
    -inset-1
    rounded-3xl
    bg-gradient-to-r
    from-blue-500
    to-purple-500
    opacity-20
    blur-xl

    transition
    duration-500

    group-hover:opacity-50
  " />

  {/* Card */}
  <div className="
    relative
    rounded-2xl
    border border-slate-200
    bg-white
    p-6
    shadow-sm
    transition-all
    duration-300

    group-hover:-translate-y-1
  ">

    <h2 className="text-xl font-bold">
      Modern Card
    </h2>

    <p className="mt-2 text-slate-600">
      Beautiful UI with subtle glow.
    </p>

  </div>

</div>
```

 এখানে:

```
Card hover
    ↓
Glow বাড়ে
    ↓
Card একটু উপরে ওঠে
```

 খুব nice effect।

---

 # 🔟 সব Effects একসাথে ব্যবহার করবে না ❌

 এটা খুব important।

 Beginner mistake:

```
Gradient
+ Glow
+ Glass
+ Shadow
+ Border animation
+ Scale
+ Blur
+ Neon
```

 সব একসাথে দিলে:

 **Modern UI ❌**

 বরং:

```
Simple Card
     +
Subtle Hover
     +
Small Glow
```

 = **Professional UI ✅**

---

 # 🧠 কোন effect কোথায়?

 | Effect | কোথায় ভালো |
| --- | --- |
| Gradient | Hero, heading, CTA |
| Glow | CTA, featured card |
| Glass | Navbar, modal, dashboard |
| Animated Border | Featured card/button |
| Hover lift | Cards |
| Scale | Image/card |
| Blur | Background decoration |
| `before/after` | Decorative effects |

---

 # 🔥 আজকের Final Project

 আজ একটা **Modern AI Feature Card** বানাবে।

 Design:

```
       ✨ AI POWERED

   ┌─────────────────────┐
   │                     │
   │       ✦ AI          │
   │                     │
   │   Smart Assistant   │
   │                     │
   │   Work smarter with │
   │   AI-powered tools. │
   │                     │
   │  [ Try AI → ]       │
   │                     │
   └─────────────────────┘
          ✨ glow
```

 ### Must use:

```
✓ gradient
✓ glow
✓ hover
✓ transition
✓ group
✓ group-hover
✓ rounded
✓ shadow
✓ backdrop-blur (optional)
```

 **Animated border optional।**

---

 # 🎯 Day 5-এর Golden Rule

 আজকের সবচেয়ে গুরুত্বপূর্ণ lesson:

 > **Effect design-এর মূল বিষয় না; effect design-কে enhance করার জন্য।**

 একটা card যদি effect ছাড়া সুন্দর না হয়, effect দিয়ে সেটাকে সুন্দর করার চেষ্টা করো না।

 আগে:

```
Layout ✅
Spacing ✅
Typography ✅
Color ✅
```

 তারপর:

```
Effect ✨
```

---

 ### 📚 Day 5 Cheat Sheet

```
Gradient
bg-gradient-to-r

Text Gradient
bg-clip-text
text-transparent

Glow
shadow-blue-500/20

Glass
bg-white/10
backdrop-blur-xl
border-white/20

Animation
animate-spin

Hover
hover:scale-105
hover:-translate-y-1

Transition
transition-all
duration-300

Pseudo
before:
after:

Parent interaction
group
group-hover:
```

 **Day 6 হবে সবচেয়ে practical দিন:** কোনো tutorial copy না করে একটা **real website screenshot দেখে নিজে পুরো UI reverse-engineer করে বানানো** শিখব।

----
# 🔴 Day 6 — Real Website Reverse Engineering

 আজকের দিনটা **সবচেয়ে important**।

 এতদিন আমরা আলাদা আলাদা জিনিস শিখেছি:

```
Day 1 → Spacing
Day 2 → Color + Typography
Day 3 → Components
Day 4 → Layout
Day 5 → Effects
```

 আজ এগুলো **একসাথে ব্যবহার করবে**।

 আজকের skill:

 > **একটা সুন্দর website দেখে সেটা কীভাবে ভেঙে ভেঙে নিজের code-এ বানাতে হয়।**

 এটাকে আমি বলি **UI Reverse Engineering**।

---

 # 1️⃣ Screenshot দেখেই code লিখবে না ❌

 ধরো screenshot:

```
┌───────────────────────────────────────┐
│ Logo     Home Work About    [Contact] │
│                                       │
│                                       │
│      Build Digital Products           │
│      That People Love                 │
│                                       │
│      Description goes here...         │
│                                       │
│      [Get Started]                    │
│                                       │
│ ┌──────────┐ ┌──────────┐ ┌────────┐ │
│ │ Feature  │ │ Feature  │ │Feature │ │
│ └──────────┘ └──────────┘ └────────┘ │
└───────────────────────────────────────┘
```

 তুমি সরাসরি:

```
<div>
...
</div>
```

 লেখা শুরু করবে না।

 আগে **design breakdown** করবে।

---

 # 2️⃣ প্রথমে Sections বের করো

 Screenshot দেখে বলবে:

```
Website
│
├── Navbar
│
├── Hero
│
├── Features
│
├── Testimonials
│
├── CTA
│
└── Footer
```

 তারপর code:

```
App
│
├── Navbar
├── Hero
├── Features
├── Testimonials
├── CTA
└── Footer
```

 React হলে:

```
function App() {
  return (
    <>
      <Navbar />
      <Hero />
      <Features />
      <Testimonials />
      <CTA />
      <Footer />
    </>
  );
}
```

 এভাবে project organized থাকবে।

---

 # 3️⃣ দ্বিতীয় ধাপ — Container বের করো

 প্রথমে দেখো content কতটুকু wide।

 সাধারণ modern website:

```
<div className="mx-auto max-w-7xl px-6">
```

 এটাই তোমার main container হতে পারে।

 তারপর প্রতিটা section:

```
<section className="py-24">
  <div className="mx-auto max-w-7xl px-6">
    ...
  </div>
</section>
```

---

 # 4️⃣ তৃতীয় ধাপ — Layout identify করো

 নিজেকে প্রশ্ন করো:

 ### এটা Flex নাকি Grid?

 Navbar:

```
Logo                Links
```

 → `flex`

```
<nav className="flex items-center justify-between">
```

 Cards:

```
Card   Card   Card
```

 → `grid`

```
<div className="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
```

 Hero:

```
Text             Image
```

 → সাধারণত `grid` বা `flex`

```
<div className="grid items-center gap-12 lg:grid-cols-2">
```

---

 # 5️⃣ Fourth — Spacing measure করো

 Screenshot দেখে approximate spacing ধরো।

 যেমন:

```
Navbar
   ↓ 80px
Hero heading
   ↓ 24px
Description
   ↓ 32px
Button
```

 Tailwind:

```
<h1 className="text-5xl font-bold">
```

```
<p className="mt-6 text-lg text-slate-600">
```

```
<button className="mt-8 ...">
```

 Pixel-perfect হওয়ার জন্য প্রথমেই `17px`, `23px`, `37px` নিয়ে চিন্তা করো না।

 আগে:

```
16
24
32
48
64
```

 এর মতো consistent spacing ব্যবহার করো।

---

 # 6️⃣ Typography Identify করো

 Screenshot দেখে:

 ### Heading

```
বড়?
Bold?
Tight?
```

 তাহলে:

```
text-5xl font-bold tracking-tight
```

 ### Paragraph

```
text-lg leading-7 text-slate-600
```

 ### Small text

```
text-sm text-slate-500
```

---

 # 7️⃣ Color বের করার Technique

 Screenshot দেখে প্রথমে শুধু **৫টা color** ধরো।

```
Background → #f8fafc
Heading    → #0f172a
Body       → #64748b
Border     → #e2e8f0
Primary    → #2563eb
```

 তারপর Tailwind-এর কাছাকাছি color ব্যবহার করো:

```
bg-slate-50
text-slate-900
text-slate-600
border-slate-200
bg-blue-600
```

 **Exact color প্রথম attempt-এ না মিললেও সমস্যা নেই।**

 আগে visual relationship ঠিক করো।

---

 # 8️⃣ Component চিনতে শেখো

 Screenshot:

```
┌─────────────────┐
│  ⚡             │
│                 │
│  Fast Build     │
│                 │
│  Description    │
│                 │
│  Learn More →   │
└─────────────────┘
```

 এটা একটা:

```
FeatureCard
```

 তাই React:

```
function FeatureCard({ title, description }) {
  return (
    <div className="
      rounded-2xl
      border border-slate-200
      bg-white
      p-6
      transition
      hover:-translate-y-1
      hover:shadow-xl
    ">
      <h3 className="text-xl font-semibold">
        {title}
      </h3>

      <p className="mt-3 text-slate-600">
        {description}
      </p>

      <button className="mt-5 font-semibold text-blue-600">
        Learn More →
      </button>
    </div>
  );
}
```

 তারপর:

```
<div className="grid gap-6 md:grid-cols-3">

  <FeatureCard
    title="Fast Build"
    description="Build applications faster."
  />

  <FeatureCard
    title="Type Safe"
    description="Write safer code."
  />

  <FeatureCard
    title="Scalable"
    description="Grow your application."
  />

</div>
```

 🔥 **এটাই professional frontend thinking।**

 একই design ৩ বার copy না করে component বানাও।

---

 # 9️⃣ Responsive চিন্তা করবে আগে থেকেই

 Desktop screenshot:

```
┌────────┐ ┌────────┐ ┌────────┐
│ Card 1 │ │ Card 2 │ │ Card 3 │
└────────┘ └────────┘ └────────┘
```

 Mobile:

```
┌──────────────┐
│ Card 1       │
└──────────────┘

┌──────────────┐
│ Card 2       │
└──────────────┘

┌──────────────┐
│ Card 3       │
└──────────────┘
```

 Code:

```
<div className="
  grid
  grid-cols-1
  gap-6
  md:grid-cols-2
  lg:grid-cols-3
">
```

---

 # 🔟 এখন একটা Real Workflow

 যখন কোনো website recreate করবে, এই order follow করবে:

```
1. Screenshot দেখো
       ↓
2. Sections identify করো
       ↓
3. Container ঠিক করো
       ↓
4. Layout → flex/grid
       ↓
5. Typography
       ↓
6. Colors
       ↓
7. Spacing
       ↓
8. Components
       ↓
9. Responsive
       ↓
10. Effects
```

 **এই order খুব important।**

 Effects দিয়ে শুরু করবে না।

---

 # 🔥 Day 6 Mini Project

 আজ বানাবে:

 ## Modern SaaS Landing Page

 Structure:

```
Navbar
──────────────────────────────

Logo          Home Pricing Docs
                         [Login]

Hero
──────────────────────────────

        Build Better Products

   Ship modern products faster
   with a beautiful workflow.

      [Get Started] [Learn More]

Features
──────────────────────────────

┌─────────┐ ┌─────────┐ ┌─────────┐
│   ⚡    │ │   🔒    │ │   🚀    │
│  Fast   │ │ Secure  │ │ Scalable│
│         │ │         │ │         │
└─────────┘ └─────────┘ └─────────┘

CTA
──────────────────────────────

        Ready to build?

          [Get Started]

Footer
──────────────────────────────
```

---

 # 🧪 কিন্তু আজ একটা কঠিন Rule

 আজ **কোনো tutorial follow করবে না।**

 Google/YouTube দেখে exact code copy করবে না।

 বরং:

```
Screenshot
    ↓
নিজে চিন্তা
    ↓
নিজে Tailwind
    ↓
Browser
    ↓
Compare
    ↓
Fix
```

 প্রথমবার যদি ৫০% match হয়, সেটাই ভালো।

 তারপর:

```
50%
 ↓
70%
 ↓
85%
 ↓
95%
```

 এভাবে UI চোখ develop হবে।

---

 # 👁️ UI চোখ Develop করার Exercise

 একটা website দেখলে নিজেকে এই ১০টা প্রশ্ন করবে:

```
1. Main container কত wide?
2. Background কোন color?
3. Heading কত বড়?
4. Body text কত বড়?
5. Section-এর vertical spacing কত?
6. Flex নাকি Grid?
7. Card-এর radius কতটা?
8. Border আছে?
9. Shadow কতটা subtle?
10. Mobile-এ layout কীভাবে বদলাবে?
```

 এই প্রশ্নগুলো করতে করতে কিছুদিন পর তুমি screenshot দেখে **code-এর structure মাথায় imagine করতে পারবে।**

---

 # 🎯 Day 6-এর Final Challenge

 একটা landing page বানাও যেখানে অবশ্যই থাকবে:

```
✓ Navbar
✓ Hero
✓ 3 Feature Cards
✓ CTA
✓ Footer

✓ Responsive
✓ Proper spacing
✓ Typography hierarchy
✓ Hover states
✓ Consistent colors
```

 **আজ animated border বা fancy effect দরকার নেই।**

 আগে পুরো website-এর **structure + spacing + hierarchy** ঠিক করো।

---

 ## 🧠 আজকের সবচেয়ে বড় lesson

 > **Good frontend developer screenshot দেখে শুধু “সুন্দর” বলে না—সে design-টাকে ছোট ছোট rules-এ ভেঙে ফেলে।**

 যেমন:

```
Screenshot
    ↓
Sections
    ↓
Components
    ↓
Layout
    ↓
Spacing
    ↓
Typography
    ↓
Color
    ↓
Interaction
    ↓
Code
```

 এটা আয়ত্ত করতে পারলে তুমি শুধু tutorial-এর design copy করবে না—**নিজে নতুন modern UI design করতেও পারবে।**

 **Day 7 হবে তোমার Final Project Day — শুরু থেকে শেষ পর্যন্ত একটা complete Modern Developer Portfolio বানাবো এবং Day 1–6-এর সব skill একসাথে ব্যবহার করব।**


-----

# 🟢 Day 7 — Final Project: Modern Developer Portfolio

 আজকে আমরা **Day 1–6-এর সবকিছু একসাথে** ব্যবহার করব।

 আজকের লক্ষ্য শুধু একটা design বানানো না—বরং এমনভাবে বানানো যাতে তুমি পরে যেকোনো website দেখে নিজে recreate করতে পারো।

---

 # 🎯 আজকের Project

 আমরা বানাবো:

```
Modern Developer Portfolio
```

 Structure:

```
Navbar
   ↓
Hero
   ↓
Skills
   ↓
Projects
   ↓
About
   ↓
CTA
   ↓
Footer
```

---

 # 1️⃣ প্রথমে পুরো UI চিন্তা করো

 Final design roughly এমন:

```
┌──────────────────────────────────────────────┐
│ Logo       Home Skills Projects    [Contact] │
├──────────────────────────────────────────────┤
│                                              │
│              👋 Hello, I'm                  │
│                                              │
│           Frontend Developer                │
│                                              │
│     I build modern digital experiences.     │
│                                              │
│       [ View Projects ] [ Contact ]         │
│                                              │
├──────────────────────────────────────────────┤
│                  Skills                      │
│                                              │
│   ┌────────┐ ┌────────┐ ┌────────┐          │
│   │ React  │ │   TS   │ │Tailwind│          │
│   └────────┘ └────────┘ └────────┘          │
│                                              │
├──────────────────────────────────────────────┤
│                 Projects                     │
│                                              │
│   ┌──────────┐ ┌──────────┐ ┌──────────┐    │
│   │ Project  │ │ Project  │ │ Project  │    │
│   └──────────┘ └──────────┘ └──────────┘    │
│                                              │
├──────────────────────────────────────────────┤
│             Let's work together              │
│                [ Contact ]                   │
├──────────────────────────────────────────────┤
│                  Footer                      │
└──────────────────────────────────────────────┘
```

---

 # 2️⃣ Navbar

 Day 4-এর Flexbox ব্যবহার করো।

```
<nav className="
  border-b
  border-slate-200
  bg-white/80
  backdrop-blur
">
  <div className="
    mx-auto
    flex
    max-w-7xl
    items-center
    justify-between
    px-6
    py-4
  ">

    <div className="text-xl font-bold text-slate-900">
      Dev<span className="text-blue-600">.</span>
    </div>

    <div className="hidden items-center gap-8 md:flex">
      <a className="text-sm text-slate-600 hover:text-slate-900">
        Home
      </a>

      <a className="text-sm text-slate-600 hover:text-slate-900">
        Skills
      </a>

      <a className="text-sm text-slate-600 hover:text-slate-900">
        Projects
      </a>
    </div>

    <button className="
      rounded-xl
      bg-slate-900
      px-4 py-2
      text-sm
      font-semibold
      text-white
      transition
      hover:bg-slate-700
    ">
      Contact
    </button>

  </div>
</nav>
```

 ### এখানে কোন Day-এর concept?

```
Day 1 → spacing
Day 2 → typography/color
Day 3 → button
Day 4 → flex/responsive
Day 5 → backdrop blur
```

---

 # 3️⃣ Hero Section ⭐

 এটাই website-এর সবচেয়ে important অংশ।

```
<section className="
  overflow-hidden
  bg-slate-50
">

  <div className="
    mx-auto
    max-w-7xl
    px-6
    py-24
    lg:py-32
  ">

    <div className="mx-auto max-w-4xl text-center">

      <span className="
        inline-flex
        rounded-full
        border
        border-blue-200
        bg-blue-50
        px-4 py-2
        text-sm
        font-medium
        text-blue-600
      ">
        👋 Hello, I'm a Developer
      </span>

      <h1 className="
        mt-6
        text-5xl
        font-bold
        leading-tight
        tracking-tight
        text-slate-900
        sm:text-6xl
        lg:text-7xl
      ">
        I build
        <span className="
          bg-gradient-to-r
          from-blue-600
          to-purple-600
          bg-clip-text
          text-transparent
        ">
          {" "}modern
        </span>
        digital experiences.
      </h1>

      <p className="
        mx-auto
        mt-6
        max-w-2xl
        text-lg
        leading-8
        text-slate-600
      ">
        Frontend developer focused on building
        beautiful, fast and accessible web experiences.
      </p>

      <div className="
        mt-8
        flex
        flex-col
        justify-center
        gap-3
        sm:flex-row
      ">

        <button className="
          rounded-xl
          bg-blue-600
          px-6 py-3
          font-semibold
          text-white
          shadow-lg
          shadow-blue-600/20
          transition-all
          hover:-translate-y-0.5
          hover:bg-blue-700
        ">
          View Projects →
        </button>

        <button className="
          rounded-xl
          border
          border-slate-200
          bg-white
          px-6 py-3
          font-semibold
          text-slate-700
          transition
          hover:bg-slate-50
        ">
          Contact Me
        </button>

      </div>

    </div>

  </div>

</section>
```

 এখানে তোমার **Day 5-এর gradient + glow + hover** চলে এসেছে।

---

 # 4️⃣ Skills Section

 এখানে Grid ব্যবহার করো।

```
<section className="bg-white py-24">

  <div className="mx-auto max-w-7xl px-6">

    <div className="mx-auto max-w-2xl text-center">

      <span className="text-sm font-semibold text-blue-600">
        SKILLS
      </span>

      <h2 className="
        mt-3
        text-3xl
        font-bold
        tracking-tight
        text-slate-900
        sm:text-4xl
      ">
        Technologies I work with
      </h2>

      <p className="mt-4 text-slate-600">
        Tools and technologies I use to build modern products.
      </p>

    </div>

    <div className="
      mx-auto
      mt-12
      grid
      max-w-4xl
      grid-cols-2
      gap-4
      md:grid-cols-4
    ">

      <div className="rounded-2xl border border-slate-200 p-6 text-center transition hover:-translate-y-1 hover:shadow-lg">
        <div className="text-2xl">⚛️</div>
        <h3 className="mt-3 font-semibold">React</h3>
      </div>

      <div className="rounded-2xl border border-slate-200 p-6 text-center transition hover:-translate-y-1 hover:shadow-lg">
        <div className="text-2xl">TS</div>
        <h3 className="mt-3 font-semibold">TypeScript</h3>
      </div>

      <div className="rounded-2xl border border-slate-200 p-6 text-center transition hover:-translate-y-1 hover:shadow-lg">
        <div className="text-2xl">TW</div>
        <h3 className="mt-3 font-semibold">Tailwind</h3>
      </div>

      <div className="rounded-2xl border border-slate-200 p-6 text-center transition hover:-translate-y-1 hover:shadow-lg">
        <div className="text-2xl">JS</div>
        <h3 className="mt-3 font-semibold">JavaScript</h3>
      </div>

    </div>

  </div>

</section>
```

---

 # 5️⃣ Projects — এখানে তোমার Day 3 Card ব্যবহার করো

 এখানে **একই card তিনবার copy করবে না।**

 একটা reusable component বানাবে:

```
type ProjectCardProps = {
  title: string;
  description: string;
  tag: string;
};

function ProjectCard({
  title,
  description,
  tag,
}: ProjectCardProps) {
  return (
    <article className="
      group
      overflow-hidden
      rounded-2xl
      border
      border-slate-200
      bg-white
      transition-all
      duration-300
      hover:-translate-y-1
      hover:border-blue-200
      hover:shadow-xl
    ">

      <div className="
        h-48
        bg-gradient-to-br
        from-slate-100
        to-blue-50
      " />

      <div className="p-6">

        <span className="
          rounded-full
          bg-blue-50
          px-3 py-1
          text-xs
          font-semibold
          text-blue-600
        ">
          {tag}
        </span>

        <h3 className="
          mt-4
          text-xl
          font-bold
          text-slate-900
          transition
          group-hover:text-blue-600
        ">
          {title}
        </h3>

        <p className="
          mt-2
          leading-6
          text-slate-600
        ">
          {description}
        </p>

        <button className="
          mt-5
          font-semibold
          text-blue-600
          transition
          hover:text-blue-700
        ">
          View Project →
        </button>

      </div>

    </article>
  );
}
```

 তারপর:

```
<div className="
  grid
  gap-6
  md:grid-cols-2
  lg:grid-cols-3
">

  <ProjectCard
    title="Dashboard UI"
    tag="React"
    description="A modern analytics dashboard interface."
  />

  <ProjectCard
    title="E-commerce App"
    tag="Next.js"
    description="A responsive shopping experience."
  />

  <ProjectCard
    title="AI Assistant"
    tag="TypeScript"
    description="An intelligent productivity application."
  />

</div>
```

 🔥 **এটাই Day 6-এর reverse engineering skill-এর practical use।**

 Design একবার → component একবার → data আলাদা।

---

 # 6️⃣ Featured Card-এ Animated Border

 সব project-এ animated border দেবে না।

 শুধু **একটা featured project** highlight করতে পারো।

```
<div className="
  relative
  overflow-hidden
  rounded-3xl
  p-[2px]
">

  <div className="
    absolute
    inset-[-150%]
    animate-spin
    bg-[conic-gradient(#3b82f6,#8b5cf6,#06b6d4,#3b82f6)]
  " />

  <div className="
    relative
    z-10
    rounded-[22px]
    bg-white
    p-6
  ">
    <span className="text-sm font-semibold text-blue-600">
      ⭐ FEATURED PROJECT
    </span>

    <h3 className="mt-4 text-2xl font-bold">
      My Best Project
    </h3>

    <p className="mt-3 text-slate-600">
      This project uses modern UI patterns
      and a scalable architecture.
    </p>
  </div>

</div>
```

 **Tip:** এটা subtle রাখবে। প্রতিটা card-এ দিলে design noisy হয়ে যাবে।

---

 # 7️⃣ CTA Section

 শেষে user-কে একটা clear action দিতে হবে।

```
<section className="px-6 py-24">

  <div className="
    relative
    mx-auto
    max-w-5xl
    overflow-hidden
    rounded-3xl
    bg-slate-950
    px-6 py-16
    text-center
    text-white
  ">

    <div className="
      absolute
      left-1/2
      top-0
      h-64
      w-64
      -translate-x-1/2
      rounded-full
      bg-blue-600/30
      blur-3xl
    " />

    <div className="relative z-10">

      <h2 className="
        text-3xl
        font-bold
        sm:text-4xl
      ">
        Have a project in mind?
      </h2>

      <p className="
        mx-auto
        mt-4
        max-w-xl
        text-slate-400
      ">
        Let's build something beautiful together.
      </p>

      <button className="
        mt-8
        rounded-xl
        bg-white
        px-6 py-3
        font-semibold
        text-slate-900
        transition
        hover:bg-slate-100
      ">
        Let's Talk →
      </button>

    </div>

  </div>

</section>
```

 এখানে Day 5-এর **glow + blur** ব্যবহার হয়েছে।

---

 # 8️⃣ Footer

 Simple রাখবে।

```
<footer className="border-t border-slate-200">

  <div className="
    mx-auto
    flex
    max-w-7xl
    flex-col
    gap-4
    px-6 py-8
    text-sm
    text-slate-500
    sm:flex-row
    sm:items-center
    sm:justify-between
  ">

    <p>
      © 2026 Dev. All rights reserved.
    </p>

    <div className="flex gap-6">
      <a className="hover:text-slate-900">
        GitHub
      </a>

      <a className="hover:text-slate-900">
        LinkedIn
      </a>

      <a className="hover:text-slate-900">
        Email
      </a>
    </div>

  </div>

</footer>
```

---

 # 🧩 পুরো Architecture

 React/Next.js project হলে এভাবে structure করতে পারো:

```
src/
│
├── components/
│   ├── Navbar.tsx
│   ├── Hero.tsx
│   ├── SkillCard.tsx
│   ├── ProjectCard.tsx
│   ├── CTA.tsx
│   └── Footer.tsx
│
├── app/
│   └── page.tsx
│
└── ...
```

 `page.tsx`:

```
export default function Home() {
  return (
    <>
      <Navbar />
      <Hero />
      <Skills />
      <Projects />
      <CTA />
      <Footer />
    </>
  );
}
```

---

 # 🧠 এখন সবচেয়ে গুরুত্বপূর্ণ — তোমার 7-Day Skill Map

 তুমি এই ৭ দিনে আসলে এগুলো শিখেছো:

```
DAY 1
│
├── Spacing
├── Typography
├── Color
├── Radius
├── Shadow
└── Hierarchy
        ↓
DAY 2
│
├── Color System
├── Typography System
└── Contrast
        ↓
DAY 3
│
├── Button
├── Card
├── Badge
├── Input
└── Interaction
        ↓
DAY 4
│
├── Flex
├── Grid
├── Gap
├── Container
└── Responsive
        ↓
DAY 5
│
├── Gradient
├── Glow
├── Glass
├── Hover
├── Animated Border
└── Pseudo Elements
        ↓
DAY 6
│
├── Screenshot Analysis
├── Sections
├── Components
└── Reverse Engineering
        ↓
DAY 7
│
└── Complete Website 🚀
```

---

 # 🔥 এখন তোমার আসল পরীক্ষা

 এবার আমি তোমাকে একটা **design challenge** দিচ্ছি।

 ## Screenshot না দেখে নিজে বানাবে:

```
                ✨ FRONTEND DEVELOPER

          Build interfaces people love.

       I create fast, accessible and
       beautiful digital experiences.

        [ View Work ]  [ Contact Me ]

                 MY SKILLS

      ┌────────┐ ┌────────┐ ┌────────┐
      │ React  │ │   TS   │ │Tailwind│
      └────────┘ └────────┘ └────────┘

               FEATURED WORK

   ┌──────────┐ ┌──────────┐ ┌──────────┐
   │ Project  │ │ Project  │ │ Project  │
   │          │ │          │ │          │
   │  View →  │ │  View →  │ │  View →  │
   └──────────┘ └──────────┘ └──────────┘

          ┌──────────────────────┐
          │  Let's work together │
          │     [ Contact ]      │
          └──────────────────────┘
```

 ### Requirements:

 **Layout**

```
✓ max-w-7xl
✓ Flex
✓ Grid
✓ Responsive
```

 **Design**

```
✓ Typography hierarchy
✓ Consistent spacing
✓ 4–5 colors maximum
✓ Rounded cards
✓ Subtle shadows
```

 **Interaction**

```
✓ Button hover
✓ Card hover
✓ Link hover
✓ Transition
```

 **Modern effect**

```
✓ একটি gradient
✓ একটি glow
✓ একটি featured/animated border
```

---

 # 🏆 7 দিনের পর কী করবে?

 এখানে থেমে গেলে skill খুব দ্রুত ভুলে যাবে।

 পরের **14 দিন** এই process follow করো:

```
Day 8–10
→ 3টা SaaS landing page recreate

Day 11–13
→ 3টা Dashboard UI recreate

Day 14–16
→ 3টা Pricing page

Day 17–19
→ 3টা Portfolio

Day 20–21
→ নিজের original design
```

 প্রতিটা project-এ প্রথমে:

```
Screenshot
    ↓
Breakdown
    ↓
Layout
    ↓
Components
    ↓
Responsive
    ↓
Interaction
    ↓
Polish
```

 এই process-টাই তোমার সবচেয়ে বড় skill হবে।

---

 ## 🎯 শেষ কথা

 **Tailwind class মুখস্থ করা তোমার goal না।**

 তোমার goal হলো একটা design দেখে বলতে পারা:

 > “এখানে container লাগবে, এখানে grid, এখানে `gap-6`, heading-এর hierarchy এমন হবে, card-এ subtle border থাকবে, hover-এ সামান্য lift হবে, mobile-এ এক column হবে।”

 যেদিন screenshot দেখে **code-এর structure মাথায় চলে আসবে**, সেদিন থেকেই তুমি সত্যিকারের **modern UI developer** হিসেবে এগোতে শুরু করবে। 🚀

---
হ্যাঁ। **Modern UI idea/inspiration নেওয়ার জন্য** কিছু resource নিয়মিত দেখলে তোমার design sense অনেক দ্রুত improve করবে। আমি এগুলোকে priority অনুযায়ী সাজিয়ে দিচ্ছি।

 ## ⭐ আমার Top Resources

 ### 1\.  Dribbble

 **কী জন্য:** নতুন visual ideas, cards, buttons, dashboard, landing page।

 Search করতে পারো:

```
SaaS dashboard
modern landing page
developer portfolio
pricing page
dark dashboard
AI website
```

 👉 **Idea নেওয়ার জন্য সবচেয়ে ভালো।**

---

 ### 2\.  Behance

 **কী জন্য:** Complete website design এবং বড় UI project দেখতে।

 Dribbble যেখানে অনেক সময় ছোট shot দেখায়, Behance-এ পুরো project/case study পাওয়া যায়।

 👉 **Complete website structure শেখার জন্য ভালো।**

---

 ### 3\.  Mobbin

 **কী জন্য:** Real-world product UI এবং user flow।

 যেমন:

```
Login
Signup
Dashboard
Settings
Checkout
Profile
Onboarding
```

 এখানে বাস্তব product-এর screen pattern দেখতে পারবে। SaaS/product UI শেখার জন্য খুব useful।  saasui.design

---

 ### 4\.  SaaSUI

 তুমি যেহেতু **modern SaaS UI** শিখছো, এটা বিশেষভাবে recommend করব।

 Dashboard, pricing, onboarding, settings ইত্যাদি screen type অনুযায়ী inspiration পাওয়া যায়।  saasui.design

---

 ### 5\.  Land-book

 **Landing page inspiration-এর জন্য।**

 বিশেষ করে:

```
Hero
Navbar
Feature section
Pricing
CTA
Footer
```

 এগুলো কীভাবে arrange করা হয় সেটা observe করো।

---

 ### 6\.  Awwwards

 **High-end website design** দেখতে।

 এখানে একটু বেশি experimental/creative design দেখতে পাবে।

 ⚠️ Beginner হিসেবে সব design copy করার চেষ্টা করো না। বরং observe করো:

 - typography
- layout
- animation
- whitespace
- visual storytelling

---

 # 💻 Tailwind শেখার জন্য সবচেয়ে গুরুত্বপূর্ণ

 ### 7\.  Tailwind Plus / UI Blocks

 এটা তোমার জন্য **must bookmark**।

 Tailwind CSS-এর creators-এর তৈরি। এখানে 500+ professionally designed UI blocks আছে—Hero, Feature, Pricing, CTA, Navbar, Cards, Forms, Dashboard ইত্যাদি।  Tailwind CSS+1

 বিশেষ করে এগুলো দেখো:

 - Hero Sections
- Feature Sections
- Pricing Sections
- Cards
- Buttons

 Tailwind-এর official examples দেখে **কেন একটা class ব্যবহার করেছে সেটা বোঝার চেষ্টা করবে**, শুধু copy-paste করবে না।  Tailwind CSS+1

---

 # 🎨 Inspiration নেওয়ার সঠিক Method

 শুধু website খুলে:

 > "ওয়াও সুন্দর!" 😅

 বললে লাভ কম।

 এরকম observe করবে:

```
Screenshot
    ↓
Navbar কীভাবে?
    ↓
Container কত wide?
    ↓
Hero alignment?
    ↓
Heading size?
    ↓
Color palette?
    ↓
Card structure?
    ↓
Spacing?
    ↓
Hover?
    ↓
Mobile layout?
```

---

 # 🔥 তোমার জন্য Daily Routine

 প্রতিদিন **১ ঘণ্টা** দিলেই শুরু করতে পারো:

 ### 15 মিনিট → Inspiration

 Dribbble  /  Land-book

 একটা design save করো।

 ### 15 মিনিট → Breakdown

 কাগজে বা মনে মনে:

```
Container
Colors
Typography
Spacing
Grid/Flex
Cards
Buttons
```

 ### 30 মিনিট → Code

 Screenshot না দেখে **নিজে recreate করো**।

 তারপর original-এর সাথে compare করো।

---

 ## 🏆 তোমার Bookmark List

 আমি হলে তোমার জায়গায় এগুলোই আগে bookmark করতাম:

 | Resource | মূল উদ্দেশ্য |
| --- | --- |
| Dribbble | Visual ideas |
| Behance | Complete designs |
| Mobbin | Real product UI |
| SaaSUI | SaaS UI |
| Land-book | Landing pages |
| Awwwards | Creative websites |
| Tailwind UI Blocks | **Tailwind implementation** |

**তোমার বর্তমান 7-day learning-এর জন্য সবচেয়ে বেশি সময় দাও:**\
 **SaaSUI + Land-book + Tailwind UI Blocks**-এ। তারপর Dribbble/Mobbin দিয়ে variety বাড়াও।  saasui.design+1

  Sources



-----
হ্যাঁ ❤️ **তুমি ৭ দিনের কোর্সটা complete করেছো।** 🎉

 এখন তোমার সবচেয়ে বড় কাজ হলো **শেখা জিনিসগুলো দিয়ে নিজে design করার practice করা।**

 ### তোমার 7-day journey

```
Day 1 → UI Fundamentals
Day 2 → Color + Typography
Day 3 → Components
Day 4 → Flex + Grid + Responsive
Day 5 → Modern Effects
Day 6 → UI Reverse Engineering
Day 7 → Complete Portfolio
```

 এখন তোমার next level হবে:

 ### 🚀 Phase 2 — UI Idea Training

 এখানে আর আমি শুধু Tailwind class শেখাবো না।

 তুমি একটা design দেখবে → **নিজে analyze করবে → নিজের idea বানাবে → তারপর code করবে।**

 Practice করবে:

```
Design দেখলাম
      ↓
কী ভালো লেগেছে?
      ↓
কোন pattern ব্যবহার করেছে?
      ↓
আমি কী পরিবর্তন করতে পারি?
      ↓
নিজের layout
      ↓
নিজের color
      ↓
নিজের components
      ↓
Tailwind code
      ↓
Responsive
      ↓
Final polish
```

 **এটাই তোমাকে “Tailwind জানে” এমন developer থেকে “নিজে modern UI design করতে পারে” এমন developer বানাবে।** 🔥

 তুমি চাইলে এখন থেকেই **Day 8 — UI Idea Training #1** শুরু করতে পারো।

----
