CSS-এর `position` ভালোভাবে বুঝতে হলে আগে একটা জিনিস মনে রাখো:

> **`position` ঠিক করে একটি element normal document flow-তে থাকবে কি না এবং `top/right/bottom/left` দিয়ে তাকে কোন reference-এর তুলনায় সরানো হবে।**

CSS-এ মূলত **৫ ধরনের `position`** আছে:

```css
static
relative
absolute
fixed
sticky
```

চলো একদম basic থেকে বুঝি।

---

# 1. `position: static`

এটাই **default position**।

```css
.box {
  position: static;
}
```

তুমি `position` না দিলেও browser ধরে নেয়:

```css
position: static;
```

### Example

```html
<div class="box">Box</div>
```

```css
.box {
  position: static;
  top: 50px;
  left: 50px;
}
```

এখানে `top` এবং `left` কাজ করবে না।

কারণ `static` element-এর উপর:

```css
top
right
bottom
left
```

সাধারণত কাজ করে না।

### কখন ব্যবহার করবে?

সাধারণ layout-এ:

```text
Navbar
Heading
Paragraph
Card
Footer
```

যেখানে element স্বাভাবিক document flow-তে থাকবে।

---

# 2. `position: relative`

এটা খুব গুরুত্বপূর্ণ।

```css
.box {
  position: relative;
}
```

`relative` element **নিজের original position-এর relative** move করতে পারে।

```css
.box {
  position: relative;
  top: 20px;
  left: 30px;
}
```

মানে:

> নিজের original জায়গা থেকে 20px নিচে এবং 30px ডানে যাও।

### Important

Element move করলেও তার **original জায়গা document flow-তে reserved থাকে**।

ধরো:

```text
Before
Box
After
```

`Box`-কে `top: 30px` দিলে visualভাবে নিচে যাবে:

```text
Before


Box
After
```

কিন্তু browser তার original জায়গাটা ধরে রাখে।

---

# 3. `relative` কেন এত important?

একটা খুব গুরুত্বপূর্ণ use আছে:

> **`absolute` child-এর reference parent বানাতে।**

ধরো:

```html
<div class="card">
    <span class="badge">New</span>
</div>
```

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

এখানে:

```text
card
┌─────────────────────┐
│              New    │
│                     │
│      Content        │
│                     │
└─────────────────────┘
```

`badge`-এর `top/right` এখন `.card`-কে reference করবে।

এটা React project-এ **অনেক বেশি ব্যবহার করবে**।

---

# 4. `position: absolute`

এটা সবচেয়ে বেশি ভুল বোঝা হয়।

```css
.box {
  position: absolute;
}
```

`absolute` element সাধারণ document flow থেকে **বের হয়ে যায়**।

অর্থাৎ অন্য element তার জায়গা ধরে রাখে না।

### Example

```html
<div class="container">
    <div class="box">Box</div>
</div>
```

```css
.container {
  position: relative;
}

.box {
  position: absolute;
  top: 20px;
  right: 20px;
}
```

এখানে `.box` তার nearest positioned ancestor:

```css
.container {
  position: relative;
}
```

এর relative position হবে।

---

# 5. Absolute-এর সবচেয়ে গুরুত্বপূর্ণ rule

মনে রাখো:

> **Absolute element তার nearest ancestor যার `position` static নয়, তার relative position নেয়।**

Example:

```html
<div class="parent">
    <div class="child"></div>
</div>
```

```css
.parent {
  position: relative;
}

.child {
  position: absolute;
  top: 0;
  right: 0;
}
```

তাহলে:

```text
Parent
┌────────────────────────┐
│                    ┌──┐│
│                    │  ││
│                    └──┘│
│                        │
└────────────────────────┘
```

Child parent-এর top-right corner-এ যাবে।

---

# 6. `absolute` কোথায় ব্যবহার করবে?

### Badge

```css
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

### Notification count

```text
       🔔
        3
```

### Card-এর image-এর উপর text

```text
┌──────────────────────┐
│                      │
│      HOTEL IMAGE     │
│                      │
│   Luxury Hotel       │
└──────────────────────┘
```

### Overlay

```css
.overlay {
  position: absolute;
  inset: 0;
}
```

### Close button

```text
┌──────────────────────┐
│                  X   │
│                      │
│       Modal          │
│                      │
└──────────────────────┘
```

---

# 7. `position: fixed`

`fixed` element **viewport-এর relative** থাকে।

মানে browser screen-এর সাথে attach হয়ে যায়।

```css
.chat-button {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
```

এখন page scroll করলেও:

```text
       Page content


                    💬
```

💬 একই screen position-এ থাকবে।

---

## Fixed-এর common use

### Floating button

```css
.help-button {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
```

### Back to top

```css
.back-to-top {
  position: fixed;
  right: 20px;
  bottom: 20px;
}
```

### Fixed navbar

```css
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
```

তখন scroll করলেও navbar থাকবে।

---

# 8. `fixed`-এর সমস্যা

যদি navbar fixed করো:

```css
.navbar {
  position: fixed;
  top: 0;
}
```

তাহলে navbar document flow থেকে বের হয়ে যায়।

তাই নিচের content navbar-এর নিচে ঢুকে যেতে পারে।

তখন:

```css
main {
  padding-top: 70px;
}
```

দিতে হতে পারে।

---

# 9. `position: sticky`

`sticky` হচ্ছে **relative + fixed-এর মতো behavior**।

এটা initially normal flow-তে থাকে।

কিন্তু scroll করার সময় নির্দিষ্ট জায়গায় পৌঁছালে sticky হয়ে যায়।

```css
.navbar {
  position: sticky;
  top: 0;
}
```

ধরো:

```text
Before scroll

Navbar
────────────
Content
Content
Content
```

scroll করার পরে:

```text
Navbar
────────────  ← এখানে আটকে যাবে

Content
Content
Content
```

---

# 10. Sticky-এর common use

### Table header

```css
thead {
  position: sticky;
  top: 0;
}
```

### Sidebar

```css
.sidebar {
  position: sticky;
  top: 20px;
}
```

### Section heading

```css
.category-title {
  position: sticky;
  top: 0;
}
```

---

# 11. `sticky` কেন কাজ করে না কখনো কখনো?

এটা beginnerদের খুব common problem।

Parent/container-এর height এবং `overflow` sticky-এর behavior affect করতে পারে।

যেমন:

```css
.parent {
  overflow: hidden;
}
```

কিছু layout-এ এর কারণে sticky expectedভাবে কাজ নাও করতে পারে।

আর sticky-এর জন্য সাধারণত threshold দিতে হয়:

```css
top: 0;
```

শুধু:

```css
position: sticky;
```

দিলে তুমি expected sticky behavior নাও পেতে পারো।

---

# 12. পাঁচটা একসাথে compare করি

| Position   | Flow-তে থাকে? | Reference                   | Scroll করলে           |
| ---------- | ------------- | --------------------------- | --------------------- |
| `static`   | ✅             | normal flow                 | scroll করবে           |
| `relative` | ✅             | নিজের original position     | scroll করবে           |
| `absolute` | ❌             | nearest positioned ancestor | scroll করবে           |
| `fixed`    | ❌             | viewport                    | screen-এ থাকবে        |
| `sticky`   | ✅             | scroll container            | threshold-এ আটকে যাবে |

---

# 13. `top/right/bottom/left`

Position ব্যবহার করার সময় এগুলো অনেক গুরুত্বপূর্ণ।

```css
.box {
  position: absolute;
  top: 10px;
  right: 20px;
}
```

মানে:

```text
top → উপর থেকে
right → ডান থেকে
bottom → নিচ থেকে
left → বাম থেকে
```

---

# 14. `inset`

চারদিকে একসাথে দিতে পারো:

```css
.overlay {
  position: absolute;
  inset: 0;
}
```

এটার equivalent:

```css
.overlay {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

Overlay বানাতে এটা খুব useful।

---

# 15. Real React example

ধরো তুমি hotel card বানাচ্ছ:

```jsx
<div className="hotel-card">
  <img src="/hotel.jpg" />

  <span className="discount">
    20% OFF
  </span>

  <button className="favorite">
    ❤️
  </button>
</div>
```

CSS:

```css
.hotel-card {
  position: relative;
}

.discount {
  position: absolute;
  top: 10px;
  left: 10px;
}

.favorite {
  position: absolute;
  top: 10px;
  right: 10px;
}
```

Result:

```text
┌────────────────────────────┐
│  20% OFF              ❤️   │
│                            │
│        HOTEL IMAGE         │
│                            │
│                            │
└────────────────────────────┘
```

এখানে:

```text
hotel-card → relative
discount   → absolute
favorite   → absolute
```

এই pattern তুমি **e-commerce, hotel, hospital, job portal—সব project-এই** ব্যবহার করবে।

---

# 16. একটা খুব important mental model

`position` মনে রাখার জন্য:

### `static`

> "আমি normal জায়গায় থাকব।"

### `relative`

> "আমি আমার জায়গা ধরে রেখে একটু move করতে পারি।"

### `absolute`

> "আমি normal flow থেকে বের হয়ে যাব এবং positioned parent-এর ভিত্তিতে বসব।"

### `fixed`

> "আমি screen-এর সাথে আটকে থাকব।"

### `sticky`

> "আমি normalভাবেই থাকব, কিন্তু scroll করলে নির্দিষ্ট জায়গায় আটকে যাব।"

---

## কখন কোনটা ব্যবহার করবে?

```text
Normal layout
      ↓
   static

নিজের position থেকে সামান্য সরাতে
      ↓
   relative

Parent-এর ভিতরে নির্দিষ্ট জায়গায় বসাতে
      ↓
   absolute

Screen-এর সাথে সবসময় আটকে রাখতে
      ↓
   fixed

Scroll করার সময় নির্দিষ্ট জায়গায় আটকে রাখতে
      ↓
   sticky
```

**সবচেয়ে বেশি মনে রাখবে এই pairটা:**

```css
.parent {
  position: relative;
}

.child {
  position: absolute;
}
```

এটা বুঝে গেলে `position`-এর অনেক practical কাজ পরিষ্কার হয়ে যাবে।


---
# tailwind css use kore
Tailwind CSS-এ `position` ব্যবহার করা খুব সহজ, কারণ CSS লিখতে হয় না—utility class ব্যবহার করলেই হয়।

## 1. Tailwind-এর position classes

CSS:

```css
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;
```

Tailwind:

```text
static
relative
absolute
fixed
sticky
```

অর্থাৎ:

```jsx
<div className="relative">
```

মানে:

```css
position: relative;
```

---

## 2. `relative`

```jsx
<div className="relative">
  Content
</div>
```

Equivalent:

```css
position: relative;
```

সাধারণত `absolute` child-এর parent হিসেবে ব্যবহার করবে।

---

## 3. `absolute`

Tailwind:

```jsx
<div className="absolute">
  Content
</div>
```

তারপর position দিতে:

```jsx
<div className="absolute top-0 right-0">
  Badge
</div>
```

মানে:

```css
position: absolute;
top: 0;
right: 0;
```

---

# 4. Real example: Hotel Card

ধরো:

```jsx
<div className="relative">
  <img
    src="/hotel.jpg"
    className="w-full"
  />

  <span className="absolute top-2 left-2">
    20% OFF
  </span>

  <button className="absolute top-2 right-2">
    ❤️
  </button>
</div>
```

এখানে:

```text
relative
   ↓
parent

absolute top-2 left-2
   ↓
discount

absolute top-2 right-2
   ↓
favorite button
```

Visual:

```text
┌─────────────────────────────┐
│ 20% OFF                ❤️   │
│                             │
│        HOTEL IMAGE          │
│                             │
└─────────────────────────────┘
```

---

# 5. Tailwind-এ `top`, `right`, `bottom`, `left`

```jsx
<div className="absolute top-4 left-4">
```

মানে:

```css
top: 1rem;
left: 1rem;
```

Common values:

```text
top-0
top-1
top-2
top-4
top-6
top-8

right-0
right-2
right-4
right-8

bottom-0
bottom-4
bottom-8

left-0
left-4
left-8
```

Tailwind-এর spacing scale অনুযায়ী এগুলোর value নির্ধারিত হয়।

---

# 6. চারদিকে `0` দিতে চাইলে

আগে CSS-এ:

```css
position: absolute;
top: 0;
right: 0;
bottom: 0;
left: 0;
```

Tailwind-এ:

```jsx
<div className="absolute inset-0">
```

এটা খুব useful।

### Overlay example

```jsx
<div className="relative">
  <img src="/hotel.jpg" />

  <div className="absolute inset-0 bg-black/40">
  </div>
</div>
```

এখানে:

```text
absolute
   +
inset-0
   +
bg-black/40
```

পুরো image-এর উপর overlay তৈরি করবে।

---

# 7. `fixed`

Tailwind:

```jsx
<button className="fixed bottom-5 right-5">
  ↑
</button>
```

Equivalent:

```css
position: fixed;
bottom: 1.25rem;
right: 1.25rem;
```

এটা screen-এর সাথে থাকবে।

### Example

```jsx
<button className="fixed bottom-5 right-5 rounded-full">
  Chat
</button>
```

Scroll করলেও button screen-এর একই জায়গায় থাকবে।

---

# 8. Fixed Navbar

```jsx
<nav className="fixed top-0 left-0 w-full">
  Navbar
</nav>
```

সাধারণত production project-এ:

```jsx
<nav className="fixed top-0 left-0 z-50 w-full">
```

`z-50` দিলে navbar অন্য content-এর উপরে থাকার chance বেশি থাকে।

---

# 9. `sticky`

Tailwind:

```jsx
<div className="sticky top-0">
  Sidebar
</div>
```

Equivalent:

```css
position: sticky;
top: 0;
```

### Example

```jsx
<aside className="sticky top-5">
  Sidebar
</aside>
```

Scroll করার সময় sidebar নির্দিষ্ট জায়গায় আটকে থাকবে।

---

# 10. `z-index`

Position-এর সাথে `z-index` অনেক সময় দরকার হয়।

Tailwind:

```text
z-0
z-10
z-20
z-30
z-40
z-50
```

Example:

```jsx
<nav className="fixed top-0 z-50 w-full">
```

মানে:

```css
position: fixed;
top: 0;
z-index: 50;
```

---

# 11. Negative position

Tailwind-এ negative value-ও দিতে পারো:

```jsx
<div className="absolute -top-2">
```

মানে:

```css
top: -0.5rem;
```

আর:

```jsx
<div className="absolute -right-2">
```

মানে right দিকে container-এর বাইরে একটু চলে যাবে।

এটা badge-এর ক্ষেত্রে useful:

```jsx
<div className="relative">
  <button>🔔</button>

  <span className="absolute -top-2 -right-2">
    3
  </span>
</div>
```

---

# 12. `relative + absolute` সবচেয়ে important pattern

Tailwind-এ এই pattern বারবার দেখতে পাবে:

```jsx
<div className="relative">

  <div className="absolute top-0 right-0">
    ...
  </div>

</div>
```

**Parent:**

```text
relative
```

**Child:**

```text
absolute
```

এটা দিয়ে:

* badge
* notification
* image overlay
* favorite button
* close button
* dropdown indicator
* card label

অনেক কিছু বানানো যায়।

---

## Tailwind cheat sheet

| CSS                  | Tailwind               |
| -------------------- | ---------------------- |
| `position: static`   | `static`               |
| `position: relative` | `relative`             |
| `position: absolute` | `absolute`             |
| `position: fixed`    | `fixed`                |
| `position: sticky`   | `sticky`               |
| `top: 0`             | `top-0`                |
| `right: 0`           | `right-0`              |
| `bottom: 0`          | `bottom-0`             |
| `left: 0`            | `left-0`               |
| চারদিকে `0`          | `inset-0`              |
| `z-index`            | `z-10`, `z-20`, `z-50` |

### Practical rule

React + Tailwind project-এ যখন দেখবে:

```jsx
<div className="relative">
```

তখন নিজেকে প্রশ্ন করবে:

> **"এর ভিতরে কি কোনো element-কে নির্দিষ্ট জায়গায় বসাতে হবে?"**

যদি হয়, তখন সম্ভবত:

```jsx
<div className="absolute top-... right-...">
```

ব্যবহার করবে।

আর **`fixed` বনাম `sticky` কখন কোনটা নেবে**, সেটা বুঝতে চাইলে পরের ধাপে `navbar + sidebar + modal + dropdown` দিয়ে practical example করলে সবচেয়ে পরিষ্কার হবে।
তোমার code-এ `absolute` কাজ করছে, কিন্তু **তুমি `top/left/right/bottom` দাওনি**, তাই browser-এর default static position অনুযায়ী child-টা parent-এর শুরুতে বসছে। আর একটা বিষয় হলো `h-full` parent-এর height-এর সাথে কাজ করবে, যেটা image-এর height-এর সমান ধরে নেওয়া ঠিক নয়।

তোমার code:

```jsx
<div className="my-10 border-y-4 mx-3 relative">
  <img className="w-full h-[80vh]" src={img1} alt="" />

  <div className="absolute w-96 h-full border">
    ...
  </div>
</div>
```

### যদি তুমি image-এর উপর box বসাতে চাও

এভাবে লেখো:

```jsx
<div className="my-10 border-y-4 mx-3 relative">
  <img
    className="w-full h-[80vh] object-cover"
    src={img1}
    alt=""
  />

  <div className="absolute top-0 left-0 w-96 h-full border-4 border-red-500">
    <h1>
      Lorem ipsum, dolor sit amet consectetur adipisicing elit.
      Nihil aliquam ad esse pariatur consequatur dolorum, ratione
      iure ducimus autem.
    </h1>
  </div>
</div>
```

এখানে:

```text
relative
   ↓
parent

absolute top-0 left-0
   ↓
child
```

ফলে:

```text
┌────────────────────────────────────────────┐
│ ┌──────────────┐                            │
│ │ Lorem ipsum  │                            │
│ │              │          IMAGE             │
│ │              │                            │
│ └──────────────┘                            │
│                                             │
└─────────────────────────────────────────────┘
```

---

### যদি right side-এ বসাতে চাও

```jsx
<div className="absolute top-0 right-0 w-96 h-full border-4 border-red-500">
```

Result:

```text
┌────────────────────────────────────────────┐
│                            ┌──────────────┐ │
│                            │ Lorem ipsum  │ │
│           IMAGE            │              │ │
│                            │              │ │
│                            └──────────────┘ │
└────────────────────────────────────────────┘
```

### যদি একদম center-এ বসাতে চাও

```jsx
<div className="absolute inset-0 flex items-center justify-center">
  <div className="w-96 border-4 border-red-500">
    <h1>Lorem ipsum...</h1>
  </div>
</div>
```

এখানে `inset-0` মানে:

```css
top: 0;
right: 0;
bottom: 0;
left: 0;
```

তারপর:

```text
flex
items-center
justify-center
```

দিয়ে ভিতরের content center করা হয়েছে।

**তোমার মূল ভুল:** `absolute` দেওয়ার পর **কোথায় বসবে সেটা `top/left/right/bottom/inset` দিয়ে specify করোনি।** `relative` parent ঠিকই দিয়েছো।
