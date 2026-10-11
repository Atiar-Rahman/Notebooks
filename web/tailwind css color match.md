অবশ্যই। Tailwind CSS-এ **color opacity modifier** যেমন `/50`, `/60`, `/20` কোথায় কোথায় ব্যবহার করা যায়—এক জায়গায় পুরো cheat sheet দিলাম।

## Tailwind Color Opacity — Complete Summary

মূল syntax:

```html
{color}-{shade}/{opacity}
```

উদাহরণ:

```html
bg-red-500/60
text-blue-500/50
border-gray-500/30
```

এখানে `/60`, `/50`, `/30` হলো **color opacity**।

---

### 1. Background — `bg-*` ✅

সবচেয়ে বেশি ব্যবহার হয়।

```html
bg-red-500/50
bg-blue-600/60
bg-black/20
bg-white/80
```

**কাজ:** শুধু background color transparent করবে।

---

### 2. Text — `text-*` ✅

```html
text-red-500/50
text-black/60
text-white/70
```

**কাজ:** text color-এর opacity কমাবে।

---

### 3. Border — `border-*` ✅

```html
border-red-500/50
border-black/20
border-gray-500/30
```

**কাজ:** border-এর color transparent করবে।

---

### 4. Ring — `ring-*` ✅

```html
ring-blue-500/50
ring-red-500/30
ring-black/20
```

যেমন:

```html
<button class="ring-2 ring-blue-500/50">
```

Ring-এর color-এর opacity কমবে।

---

### 5. Divide — `divide-*` ✅

```html
divide-gray-500/30
divide-black/20
```

যেমন:

```html
<div class="divide-y divide-gray-500/30">
```

Child elements-এর মাঝের divider-এর color transparent হবে।

---

### 6. Placeholder — `placeholder-*` ✅

```html
placeholder-gray-500/50
placeholder-red-500/40
```

যেমন:

```html
<input
  class="placeholder-gray-500/50"
  placeholder="Enter your name"
/>
```

Placeholder text হালকা হবে।

---

### 7. Decoration — `decoration-*` ✅

Text decoration/underline-এর color-এর ক্ষেত্রে:

```html
decoration-red-500/50
decoration-blue-500/60
```

যেমন:

```html
<p class="underline decoration-red-500/50">
  Hello
</p>
```

---

### 8. Accent — `accent-*` ✅

Form controls-এর accent color:

```html
accent-blue-500/70
accent-red-500/50
```

যেমন checkbox/radio:

```html
<input type="checkbox" class="accent-blue-500/70">
```

---

### 9. Caret — `caret-*` ✅

Input-এর typing cursor:

```html
caret-blue-500/70
caret-red-500/50
```

```html
<input class="caret-blue-500/70">
```

---

### 10. Outline — `outline-*` ✅

```html
outline-blue-500/50
outline-red-500/60
```

যেমন:

```html
<input class="outline-2 outline-blue-500/50">
```

---

## গুরুত্বপূর্ণ: `opacity-*` আলাদা জিনিস

এটা color opacity modifier-এর মতো নয়।

```html
opacity-50
```

এটা **পুরো element**-এর opacity কমায়।

ধরো:

```html
<div class="bg-red-500 opacity-50">
  <p class="text-white">Hello</p>
</div>
```

এখানে `div`-এর **background + text + ভিতরের সবকিছু** 50% opacity হবে।

কিন্তু:

```html
<div class="bg-red-500/50">
  <p class="text-white">Hello</p>
</div>
```

এখানে শুধু **background red-এর opacity** 50% হবে। Text স্বাভাবিক থাকবে।

---

# এক নজরে Cheat Sheet

| কোথায়       | Syntax                   | কাজ                              |
| ----------- | ------------------------ | -------------------------------- |
| Background  | `bg-red-500/50`          | Background transparent           |
| Text        | `text-red-500/50`        | Text color transparent           |
| Border      | `border-red-500/50`      | Border transparent               |
| Ring        | `ring-red-500/50`        | Ring transparent                 |
| Divide      | `divide-red-500/50`      | Divider transparent              |
| Placeholder | `placeholder-red-500/50` | Placeholder transparent          |
| Decoration  | `decoration-red-500/50`  | Underline/decoration transparent |
| Accent      | `accent-red-500/50`      | Form accent transparent          |
| Caret       | `caret-red-500/50`       | Cursor transparent               |
| Outline     | `outline-red-500/50`     | Outline transparent              |

### আরেকটা useful জিনিস

Opacity modifier-এর সাথে state modifier-ও ব্যবহার করতে পারো:

```html
hover:bg-blue-500/80
hover:text-white/80
hover:border-blue-500/50
focus:ring-blue-500/50
```

অর্থাৎ `/50` বা `/60` মূলত **color-এর transparency control করার একটি modifier**। আর `opacity-50` হলো **পুরো element-এর opacity control**।

For Tailwind opacity

* Compare color and element opacity
* Use opacity with hover and focus


---
# Hover use korle 

অবশ্যই। Tailwind-এ **color opacity modifier (`/50`, `/60`, etc.)**-কে `hover:`, `focus:`, `active:`, `disabled:` এবং `dark:`-এর সাথে খুব সহজেই combine করা যায়।

## 1. `hover:` + opacity

Mouse hover করলে background-এর opacity পরিবর্তন:

```html
<button class="bg-blue-500/50 hover:bg-blue-500/80">
  Hover me
</button>
```

- Normal → `blue` 50%
    
- Hover → `blue` 80%
    

আরও example:

```html
hover:bg-red-500/60
hover:text-white/80
hover:border-blue-500/50
```

---

## 2. `focus:` + opacity

Input focus করলে:

```html
<input
  class="border border-gray-500/40 focus:border-blue-500/80 focus:ring-2 focus:ring-blue-500/30"
  placeholder="Your name"
/>
```

এখানে:

- Normal border → gray 40%
    
- Focus border → blue 80%
    
- Focus ring → blue 30%
    

---

## 3. `active:` + opacity

Button press করার সময়:

```html
<button class="bg-blue-500/80 active:bg-blue-500/50">
  Click me
</button>
```

- Normal → 80%
    
- Mouse click/press → 50%
    

আরও বাস্তব example:

```html
<button
  class="bg-black/80 hover:bg-black/70 active:bg-black/50"
>
  Submit
</button>
```

---

## 4. `disabled:` + opacity

Disabled button-এর background হালকা করে দিতে:

```html
<button
  disabled
  class="bg-blue-500 disabled:bg-blue-500/30 disabled:text-gray-500/60"
>
  Disabled
</button>
```

সাধারণত disabled অবস্থায় `cursor-not-allowed`-ও দেওয়া হয়:

```html
<button
  disabled
  class="bg-blue-500/80 hover:bg-blue-500 disabled:bg-blue-500/30 disabled:cursor-not-allowed"
>
  Submit
</button>
```

---

# 5. `dark:` + opacity

Dark mode-এ আলাদা color + opacity দিতে পারো:

```html
<div class="bg-white/80 dark:bg-black/60">
  Content
</div>
```

Light mode:

```text
white → 80%
```

Dark mode:

```text
black → 60%
```

Text-এর ক্ষেত্রেও:

```html
<p class="text-black/80 dark:text-white/80">
  Hello World
</p>
```

---

# 6. সবগুলো একসাথে 🚀

একটা বাস্তব button:

```html
<button
  class="
    bg-blue-500/80
    hover:bg-blue-500/90
    focus:bg-blue-500/80
    focus:ring-2
    focus:ring-blue-500/40
    active:bg-blue-500/60
    disabled:bg-blue-500/30
    dark:bg-blue-400/70
    dark:hover:bg-blue-400/80
    dark:active:bg-blue-400/50
  "
>
  Submit
</button>
```

এখানে প্রত্যেক state-এর জন্য আলাদা opacity দেওয়া হয়েছে।

### Mental model

এই pattern-টা মনে রাখলেই হবে:

```text
[state]:[color]-[shade]/[opacity]
```

যেমন:

```text
hover:bg-red-500/80
focus:border-blue-500/50
active:bg-green-500/60
disabled:text-gray-500/40
dark:bg-black/70
dark:hover:bg-black/80
```

### আরও advanced combination

একাধিক variant একসাথে chain করা যায়:

```html
dark:hover:bg-blue-400/80
dark:focus:ring-blue-400/50
dark:disabled:bg-gray-500/30
```

অর্থাৎ:

```text
dark + hover + background + color + opacity
```

=

```html
dark:hover:bg-blue-400/80
```

**সবচেয়ে গুরুত্বপূর্ণ rule:** `/80` এখানে `opacity-80` নয়। এটি **শুধু ওই color-এর opacity**। তাই `dark:hover:bg-blue-400/80` মানে dark mode-এ hover অবস্থায় `blue-400` background-এর opacity 80%।

For Tailwind state variants

- Combine opacity with group-hover
    
- Use opacity with gradients


---

# **Group Hover use kora **

অবশ্যই। এখানে মূল idea হলো:

```text
[variant]:[color]-[shade]/[opacity]
```

এখন `group-hover`, `peer-focus`, আর `data-*` variant-এর সাথে কীভাবে ব্যবহার করবে দেখি।

---

## 1. `group-hover:` + color opacity

Parent element-এ `group` দাও:

```html id="2u4z4q"
<div class="group">
  <div class="bg-blue-500/30 group-hover:bg-blue-500/80">
    Hello
  </div>
</div>
```

এখানে:

* সাধারণ অবস্থায় → `blue-500` **30%**
* Parent-এর ওপর hover করলে → `blue-500` **80%**

### Practical example

```html id="9n5e6x"
<div class="group rounded-xl bg-gray-100 p-6">
  <h2 class="text-black/60 group-hover:text-black/100">
    Card Title
  </h2>

  <p class="text-black/40 group-hover:text-black/70">
    Card description
  </p>
</div>
```

Parent card hover করলে ভিতরের text আরও visible হবে।

---

# 2. `peer-focus:` + color opacity

এখানে আগে একটি element-এ `peer` দিতে হয়।

```html id="vuzd9h"
<div>
  <input
    class="peer border border-gray-500/40"
    placeholder="Your name"
  />

  <p class="text-gray-500/50 peer-focus:text-blue-500/100">
    Enter your name
  </p>
</div>
```

Input focus করলে:

```text
normal → gray 50%
focus  → blue 100%
```

### আরও practical example

```html id="u3e3u6"
<div>
  <input
    class="peer w-full rounded border border-gray-500/40 p-3
           focus:border-blue-500/70"
    placeholder="Email"
  />

  <label class="text-gray-500/50 peer-focus:text-blue-500/80">
    Email address
  </label>
</div>
```

**Important:** সাধারণত `peer` element-টি `peer-focus:` target-এর **আগে** থাকতে হবে।

---

# 3. `data-*` variant

Tailwind-এ element-এর `data-*` attribute-এর value অনুযায়ী style দিতে পারো।

ধরো:

```html id="krkpx4"
<button data-state="open" class="bg-blue-500/50 data-[state=open]:bg-blue-500/90">
  Menu
</button>
```

এখানে:

```text
data-state="open"
        ↓
data-[state=open]:
        ↓
bg-blue-500/90
```

অর্থাৎ `data-state="open"` হলে background opacity **90%** হবে।

---

## 4. `data-state="closed"`

```html id="y7q8w7"
<div
  data-state="closed"
  class="bg-black/30 data-[state=closed]:bg-black/20"
>
  Content
</div>
```

এখানে closed state-এ black-এর opacity 20%।

---

# 5. `data-state` + hover

দুটো একসাথেও করা যায়:

```html id="v7j6e8"
<button
  data-state="open"
  class="
    bg-blue-500/50
    hover:bg-blue-500/70
    data-[state=open]:bg-blue-500/90
    data-[state=open]:hover:bg-blue-500/100
  "
>
  Open Menu
</button>
```

State অনুযায়ী:

```text
Normal
→ blue 50%

Hover
→ blue 70%

Open
→ blue 90%

Open + Hover
→ blue 100%
```

---

# 6. `data-[state=active]`

Tabs-এর ক্ষেত্রে খুব useful:

```html id="d4z4ja"
<button
  data-state="inactive"
  class="text-black/50 data-[state=active]:text-blue-500/100"
>
  Profile
</button>
```

যদি:

```html id="j8y9ef"
data-state="active"
```

হয়, তাহলে:

```text
text-blue-500/100
```

apply হবে।

---

# 7. `group` + `data-state` একসাথে

আরও powerful combination:

```html id="m93e1s"
<div class="group" data-state="open">
  <span
    class="
      text-black/40
      group-hover:text-black/60
      group-data-[state=open]:text-blue-500/90
    "
  >
    Menu
  </span>
</div>
```

এখানে তিনটা state আছে:

```text
Normal
→ black 40%

Group hover
→ black 60%

Group data-state=open
→ blue 90%
```

---

# 8. `peer` + `data-state`

```html id="4g5q6s"
<input
  type="checkbox"
  data-state="checked"
  class="peer"
/>

<span
  class="
    text-gray-500/50
    peer-checked:text-green-500/90
  "
>
  Accepted
</span>
```

এখানে checkbox checked হলে:

```text
text-green-500/90
```

হবে।

---

# 9. `dark` + `group-hover` + opacity

Real-world card example:

```html id="gq48t5"
<div class="group bg-white/80 dark:bg-gray-900/80">
  <h2
    class="
      text-black/60
      group-hover:text-black/90
      dark:text-white/60
      dark:group-hover:text-white/90
    "
  >
    Card title
  </h2>
</div>
```

এখানে:

```text
Light + normal
→ black 60%

Light + hover
→ black 90%

Dark + normal
→ white 60%

Dark + hover
→ white 90%
```

---

# Quick Cheat Sheet 🧠

### `group-hover`

```html id="k5y2py"
group-hover:bg-blue-500/80
```

Parent hover → child-এর color opacity change।

### `peer-focus`

```html id="6q4yrg"
peer-focus:text-blue-500/80
```

Peer element focus → target-এর color opacity change।

### `data-state`

```html id="t8kqf8"
data-[state=open]:bg-blue-500/90
```

`data-state="open"` → background opacity 90%।

### `group-data`

```html id="4x9v7m"
group-data-[state=open]:bg-blue-500/90
```

Parent-এর `data-state="open"` → child-এর style change।

### একসাথে

```html id="9t5p8w"
dark:group-hover:bg-blue-400/80
```

মানে:

**Dark mode + parent hover → blue-400 background 80% opacity।**

আর:

```html id="m2v7c4"
data-[state=active]:text-blue-500/90
```

মানে:

**data-state active → blue text 90% opacity।**

এই patternটা মনে রাখো:

```text
variant + color + shade + opacity
```

যেমন:

```text
hover:bg-blue-500/80
group-hover:text-white/90
peer-focus:border-blue-500/70
data-[state=open]:bg-black/60
dark:group-hover:bg-white/20
group-data-[state=active]:text-blue-500/90
```

এগুলো দেখলেই বুঝবে **কোন state/condition-এ কোন color কত opacity-তে apply হচ্ছে।**

For these Tailwind variants

* Compare variant precedence
* Add arbitrary data variants



----
একদম। এগুলো Tailwind-এর **state/relationship-based styling** বুঝতে সাহায্য করে। একসাথে দেখলে ব্যাপারটা অনেক পরিষ্কার হবে।

## 1. `group` — Parent-এর state দিয়ে child style করা

Parent-এ `group`:

```html id="8v7q5k"
<div class="group">
  <h2 class="text-gray-500 group-hover:text-blue-500">
    Hover the card
  </h2>
</div>
```

Parent hover করলে child-এর color বদলাবে।

```text
group
  ↓
group-hover:
```

### Real example

```html id="u3s8b1"
<div class="group rounded-xl bg-gray-100 p-6">
  <h2 class="text-gray-700 group-hover:text-blue-600">
    Product
  </h2>

  <p class="text-gray-500 group-hover:text-gray-700">
    Description
  </p>
</div>
```

---

# 2. `peer` — Sibling-এর state দিয়ে অন্য sibling style করা

এখানে `peer` সাধারণত input/form UI-তে খুব useful।

```html id="6t1m2a"
<input class="peer" type="checkbox">

<span class="text-gray-400 peer-checked:text-green-500">
  Accepted
</span>
```

Checkbox checked হলে `span` green হবে।

```text
peer
 ↓
peer-checked:
```

### Input focus example

```html id="1c7n9q"
<input
  class="peer border-gray-300 focus:border-blue-500"
  placeholder="Email"
/>

<label class="text-gray-400 peer-focus:text-blue-500">
  Email
</label>
```

Input focus → label blue।

---

# 3. `data-*` — Custom state/attribute দিয়ে style

HTML-এ নিজের data attribute রাখতে পারো:

```html id="p3v9j2"
<button
  data-state="active"
  class="data-[state=active]:bg-blue-500 data-[state=active]:text-white"
>
  Profile
</button>
```

`data-state="active"` হলে:

```text
bg-blue-500
text-white
```

apply হবে।

এটা tabs, dropdown, modal, accordion ইত্যাদিতে অনেক useful।

---

# 4. `aria-*` — Accessibility state দিয়ে style

ARIA attribute accessibility-এর জন্য ব্যবহৃত হয়।

যেমন:

```html id="9g4k2v"
<button
  aria-expanded="true"
  class="aria-expanded:bg-blue-500"
>
  Menu
</button>
```

যখন:

```html
aria-expanded="true"
```

তখন Tailwind:

```text
aria-expanded:bg-blue-500
```

apply করবে।

আরও example:

```html id="6v5x3r"
<button
  aria-pressed="true"
  class="aria-pressed:bg-blue-500 aria-pressed:text-white"
>
  Like
</button>
```

---

# 5. `has-*` — ভিতরে কিছু আছে কিনা দেখে Parent style করা

এটা খুব interesting। 😄

ধরো:

```html id="8q2w5k"
<label class="has-[:focus]:border-blue-500 border">
  <input class="outline-none">
</label>
```

Input-এর ভিতরে কোনো element focus হলে **parent label-এর border blue** হবে।

```text
Parent
  ↓
has-[condition]
  ↓
Child-এর condition check
```

### Checkbox example

```html id="n2f8v4"
<div class="has-[:checked]:bg-green-100 p-4">
  <input type="checkbox">
  <span>Accept terms</span>
</div>
```

Checkbox checked হলে পুরো `div` green-ish background পাবে।

---

# একসাথে তুলনা করলে

| Variant   | কী দেখে?             | Typical use           |
| --------- | -------------------- | --------------------- |
| `group-*` | Parent-এর state      | Card hover            |
| `peer-*`  | Sibling-এর state     | Input → label         |
| `data-*`  | `data-*` attribute   | Tabs, modal, dropdown |
| `aria-*`  | ARIA state           | Accessible UI         |
| `has-*`   | ভিতরের element/state | Parent based on child |

---

## একটা UI-তে সবগুলো 😎

ধরো একটা custom dropdown:

```html id="z8x3f1"
<div
  class="
    group
    relative
    rounded-lg
    border
    border-gray-300
    bg-white
    p-4
    has-[:focus]:border-blue-500
    data-[state=open]:border-blue-500
  "
  data-state="open"
>
  <button
    aria-expanded="true"
    class="
      text-gray-500/70
      group-hover:text-gray-900
      aria-expanded:text-blue-500
    "
  >
    Select option
  </button>

  <input
    class="
      peer
      mt-2
      border
      border-gray-300
      peer-focus:border-blue-500
    "
  >

  <span class="text-gray-400 peer-focus:text-blue-500">
    Search...
  </span>
</div>
```

এখানে:

```text
group
  → parent hover করলে child change

peer
  → input focus করলে sibling change

data-*
  → custom state অনুযায়ী style

aria-*
  → accessibility state অনুযায়ী style

has-*
  → ভিতরের element-এর state দেখে parent change
```

### সবচেয়ে important mental model

Tailwind-এর এই পাঁচটা এভাবে মনে রাখো:

```text
group  → "আমার parent কী করছে?"
peer   → "আমার পাশের element কী করছে?"
data   → "আমার custom state কী?"
aria   → "আমার accessibility state কী?"
has    → "আমার ভিতরে কী হচ্ছে?"
```

এই mental modelটা ধরতে পারলে Tailwind-এর interactive UI অনেক বেশি সহজ হয়ে যাবে।

For these Tailwind variants

* Build one interactive component



---
হ্যাঁ, এখানে মূল confusion হলো **`:` আর `::`**। সহজভাবে মনে রাখো:

## `:` → Pseudo-class

Element-এর **state বা condition** বোঝায়।

```css
:hover
:focus
:active
:checked
:disabled
:first-child
```

Tailwind-এ এগুলো সাধারণত:

```html
hover:bg-blue-500
focus:border-blue-500
active:bg-blue-700
disabled:bg-gray-400
```

### Example

```html
<button class="bg-blue-500 hover:bg-blue-700">
  Click Me
</button>
```

এখানে `hover:` মানে:

> Mouse hover করলে এই style apply করো।

---

## `::` → Pseudo-element

Element-এর **একটা অংশ বা virtual element** target করে।

```css
::before
::after
::placeholder
::marker
::first-letter
::selection
```

Tailwind-এ:

```html
before:content-['Hi']
after:content-['!']
placeholder:text-gray-400
marker:text-red-500
first-letter:text-3xl
selection:bg-blue-200
```

---

### সহজ পার্থক্য

| CSS              | কী বোঝায়            | Tailwind        |
| ---------------- | ------------------- | --------------- |
| `:hover`         | hover state         | `hover:`        |
| `:focus`         | focus state         | `focus:`        |
| `:active`        | active state        | `active:`       |
| `:checked`       | checked state       | `checked:`      |
| `:disabled`      | disabled state      | `disabled:`     |
| `:first-child`   | প্রথম child         | `first:`        |
| `::before`       | আগে virtual element | `before:`       |
| `::after`        | পরে virtual element | `after:`        |
| `::placeholder`  | placeholder অংশ     | `placeholder:`  |
| `::marker`       | list marker         | `marker:`       |
| `::first-letter` | প্রথম letter        | `first-letter:` |
| `::selection`    | selected text       | `selection:`    |

### মনে রাখার সবচেয়ে সহজ rule 🧠

**একটা `:` → element-এর অবস্থা/state**

```text
:hover
:focus
:checked
:disabled
```

**দুইটা `::` → element-এর ভিতরের special অংশ/virtual অংশ**

```text
::before
::after
::placeholder
::marker
```

আর Tailwind-এ সরাসরি `::` লিখবে না—Tailwind-এর variant ব্যবহার করবে:

```html
hover:bg-red-500
before:content-['']
after:bg-blue-500
placeholder:text-gray-400
```

**Shortcut:**
`:` = **"কখন?"**
`::` = **"কোন special অংশ?"**


---
হ্যাঁ, **web design-এ pseudo-class (`:`) অনেক বেশি important**, আর pseudo-element (`::`) তুলনামূলকভাবে একটু কম—but real-world design-এ দুটোই কাজে লাগে।

### 🔥 Priority হিসেবে ধরো

| বিষয়             | Importance | কোথায় বেশি ব্যবহার             |
| ---------------- | ---------- | ------------------------------ |
| `:hover`         | ⭐⭐⭐⭐⭐      | Button, card, link             |
| `:focus`         | ⭐⭐⭐⭐⭐      | Input, form                    |
| `:active`        | ⭐⭐⭐        | Button interaction             |
| `:disabled`      | ⭐⭐⭐⭐       | Form/button                    |
| `:checked`       | ⭐⭐⭐⭐       | Checkbox, toggle               |
| `::before`       | ⭐⭐⭐⭐       | Decoration, overlay, icon      |
| `::after`        | ⭐⭐⭐⭐       | Decoration, underline, overlay |
| `::placeholder`  | ⭐⭐⭐⭐       | Input                          |
| `::selection`    | ⭐⭐         | Selected text styling          |
| `::marker`       | ⭐⭐         | List styling                   |
| `::first-letter` | ⭐          | Special typography             |

### Beginner হলে আগে এগুলো শেখো

**Step 1 — অবশ্যই:**

```text
hover:
focus:
active:
disabled:
```

**Step 2 — তারপর:**

```text
group-hover:
peer-checked:
```

**Step 3 — এরপর pseudo-element:**

```text
before:
after:
placeholder:
```

### Real design example

একটা button:

```html
<button class="
  bg-blue-500
  text-white
  px-5 py-2
  rounded-lg
  hover:bg-blue-700
  active:scale-95
  disabled:bg-gray-400
  focus:ring-2
">
  Submit
</button>
```

এখানে `hover`, `active`, `disabled`, `focus`—সবই **real website-এ খুব common**।

আর `before/after` দিয়ে যেমন decorative line বানাতে পারো:

```html
<h2 class="
  relative
  after:absolute
  after:left-0
  after:-bottom-2
  after:h-1
  after:w-10
  after:bg-blue-500
">
  About Us
</h2>
```

**Bottom line:**
👉 `:` pseudo-class = **আগে ভালোভাবে শেখো**
👉 `::` pseudo-element = **তারপর শেখো**
👉 Tailwind জানার জন্য দুটোই important, কিন্তু শুরুতে `hover`, `focus`, `group-hover`, `before`, `after` ভালোভাবে পারলেই অনেক design করতে পারবে।

For Tailwind pseudo-selectors

* Compare pseudo-class and pseudo-element use
* See a practical selector cheat sheet



----
অবশ্যই — নিচেরটা **practical Tailwind cheat sheet** হিসেবে save করে রাখতে পারো। এগুলো জানলে everyday UI design-এর অনেক interaction handle করতে পারবে।

## 🔥 Tailwind Pseudo Cheat Sheet

| Variant        | কখন কাজ করে                    | Example                     |
| -------------- | ------------------------------ | --------------------------- |
| `hover:`       | Mouse hover করলে               | `hover:bg-blue-700`         |
| `focus:`       | Input/button focus করলে        | `focus:border-blue-500`     |
| `active:`      | Click/press করার সময়           | `active:scale-95`           |
| `disabled:`    | Element disabled হলে           | `disabled:bg-gray-400`      |
| `group-hover:` | Parent hover করলে child change | `group-hover:text-blue-500` |
| `before:`      | `::before` style করতে          | `before:content-['']`       |
| `after:`       | `::after` style করতে           | `after:content-['']`        |

---

## 1. `hover:` — Mouse রাখলে

```html
<button class="bg-blue-500 px-5 py-2 text-white hover:bg-blue-700">
  Hover Me
</button>
```

Normal:

```text
blue-500
```

Hover:

```text
blue-700
```

একই সাথে অনেক property change করতে পারো:

```html
<button class="
  bg-blue-500
  text-white
  border border-blue-500
  px-5 py-2
  hover:bg-white
  hover:text-blue-500
  hover:border-blue-700
">
  Hover Me
</button>
```

---

## 2. `focus:` — Input focus করলে

Form-এর জন্য খুব important।

```html
<input
  type="text"
  placeholder="Your name"
  class="
    border
    border-gray-300
    rounded-lg
    px-4 py-2
    outline-none
    focus:border-blue-500
    focus:ring-2
    focus:ring-blue-200
  "
/>
```

Input-এ click করলে:

```text
border → blue
ring → appear
```

---

## 3. `active:` — Click/press করার সময়

Button চাপার মুহূর্তে ছোট করে দিতে পারো:

```html
<button class="
  bg-blue-500
  px-5 py-2
  text-white
  rounded-lg
  active:scale-95
">
  Click Me
</button>
```

আর smooth করতে:

```html
<button class="
  transition
  duration-150
  active:scale-95
">
  Click Me
</button>
```

---

## 4. `disabled:` — Button disabled হলে

```html
<button
  disabled
  class="
    bg-blue-500
    text-white
    px-5 py-2
    rounded-lg
    disabled:bg-gray-400
    disabled:cursor-not-allowed
  "
>
  Submit
</button>
```

এখানে button disabled হলে:

```text
background → gray
cursor → not-allowed
```

---

# 5. `group-hover:` — Parent hover করলে Child change

এটা **খুব important**।

Parent-এ `group`:

```html
<div class="group p-5 border rounded-xl">
```

Child-এ:

```html
<h2 class="group-hover:text-blue-500">
```

Full example:

```html
<div class="
  group
  p-5
  border
  rounded-xl
  hover:bg-gray-50
">
  <h2 class="
    text-gray-800
    group-hover:text-blue-600
  ">
    My Card
  </h2>

  <p class="
    text-gray-500
    group-hover:text-gray-700
  ">
    This is a card.
  </p>
</div>
```

### Mental model 🧠

```text
Parent = group

Parent hover
      ↓
Child changes
```

```html
<div class="group">
    <h2 class="group-hover:text-blue-500">
```

---

# 6. `before:` — `::before`

কোনো element-এর **আগে** decorative content দিতে পারো।

Example: heading-এর আগে ছোট dot:

```html
<h2 class="
  before:content-['']
  before:inline-block
  before:w-3
  before:h-3
  before:bg-blue-500
  before:rounded-full
  before:mr-2
">
  About Us
</h2>
```

Visual idea:

```text
🔵 About Us
```

---

# 7. `after:` — `::after`

Element-এর **পরে** কিছু add করতে পারো।

```html
<h2 class="
  after:content-['→']
  after:ml-2
">
  Learn More
</h2>
```

Result:

```text
Learn More →
```

---

# 🔥 Real-world Card Example

এখানে প্রায় সবগুলো একসাথে:

```html
<div class="
  group
  relative
  p-6
  border
  rounded-xl
  transition
  duration-300
  hover:-translate-y-1
  hover:shadow-xl
">
  <h2 class="
    text-xl
    font-bold
    text-gray-800
    group-hover:text-blue-600
  ">
    Web Development
  </h2>

  <p class="
    mt-2
    text-gray-500
    group-hover:text-gray-700
  ">
    Learn modern web development.
  </p>

  <button class="
    mt-4
    bg-blue-500
    px-4
    py-2
    text-white
    rounded-lg
    transition
    hover:bg-blue-700
    active:scale-95
  ">
    Learn More
  </button>

  <span class="
    absolute
    top-4
    right-4
    before:content-['★']
    before:text-yellow-500
  "></span>
</div>
```

এখানে:

```text
hover:        → নিজে hover হলে
focus:        → focus হলে
active:       → press করলে
disabled:     → disabled হলে
group-hover:  → parent hover হলে
before:       → ::before
after:        → ::after
```

### 🧠 এক লাইনের memory trick

```text
hover   → আমি hover করলে
focus   → আমি focus হলে
active  → আমাকে press করলে
disabled → আমি disabled হলে
group-hover → আমার parent hover করলে
before  → আমার আগে
after   → আমার পরে
```

এই ৭টা ভালোভাবে আয়ত্ত করলে Tailwind-এর **interactive UI** বানানোর foundation অনেকটাই তৈরি হয়ে যাবে।
