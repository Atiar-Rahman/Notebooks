Tailwind CSS-এ **Preflight** হলো একটা built-in **CSS reset / base style layer**।

সহজভাবে:

> Browser (Chrome/Firefox) যেসব default style দেয় (margin, padding, button style, heading size), Tailwind সেগুলো reset করে একটা clean starting point বানায়।

Think like this:

Without Preflight:

```html
<h1>Hello</h1>
```

Browser automatically style দেয়:

- font-size বড়
    
- bold
    
- margin top/bottom
    

With Tailwind Preflight:

```html
<h1>Hello</h1>
```

এখন `<h1>` প্রায় plain text এর মতো behave করবে যতক্ষণ না তুমি নিজে class দাও:

```html
<h1 class="text-3xl font-bold">Hello</h1>
```

---

# কেন দরকার?

Different browser এ default style different হতে পারে।

Example:

- Chrome button একরকম
    
- Safari button আরেকরকম
    
- Firefox margin different
    

Preflight এগুলো normalize করে।

Benefits:

✅ Cross-browser consistency  
✅ Utility-first design easy  
✅ Predictable spacing/layout

[Tailwind Preflight Docs](https://tailwindcss.com/docs/preflight?utm_source=chatgpt.com)

---

# Preflight কী কী reset করে?

### 1. Margin remove

Browser default:

```css
h1, p {
   margin: something;
}
```

Preflight:

```css
* {
   margin: 0;
}
```

Example:

```html
<p>hello</p>
<p>world</p>
```

দুইটার মাঝে auto gap থাকবে না।

---

### 2. `box-sizing: border-box`

সব element এ:

```css
* {
   box-sizing: border-box;
}
```

এটা খুব important।

Without:

Width calculation messy:

```text
width + padding + border
```

With border-box:

```text
final width = exactly width
```

Example:

```html
<div class="w-64 p-4 border"></div>
```

Width overflow করবে না।

---

### 3. Headings reset

Normally:

```html
<h1>Title</h1>
```

Browser এটাকে bold + huge করে।

Preflight পরে:

```css
h1,h2,h3 {
   font-size: inherit;
   font-weight: inherit;
}
```

So তুমি control করবে:

```html
<h1 class="text-4xl font-bold">
```

---

### 4. List style remove

Browser:

```html
<ul>
  <li>A</li>
</ul>
```

Bullet থাকবে।

Preflight:

bullet remove.

তাই list চাইলে manually:

```html
<ul class="list-disc pl-6">
```

---

### 5. Image responsive

```css
img {
   max-width: 100%;
   height: auto;
}
```

Benefit:

Image container overflow করবে না।

---

### 6. Border reset

সব element এ:

```css
border: 0 solid;
```

তাই Tailwind border class দিলে clean কাজ করে:

```html
<div class="border border-gray-300"></div>
```

---

### 7. Form elements reset

Button / input browser-specific look remove:

Before:

```html
<button>Save</button>
```

Browser নিজে style দেয়।

After Preflight:

Almost plain.

তাই তুমি style দাও:

```html
<button class="bg-blue-500 text-white px-4 py-2 rounded">
```

---

# Preflight কোথায় inject হয়?

Tailwind v3:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Preflight `base` layer-এ inject হয়। ([runebook.dev](https://runebook.dev/en/docs/tailwindcss/preflight?utm_source=chatgpt.com "tailwindcss - Understanding and Overriding Tailwind's Base Styles (Preflight)"))

Tailwind v4:

```css
@import "tailwindcss";
```

---

# নিজের base style add করতে

```css
@layer base {
  h1 {
    @apply text-4xl font-bold;
  }
}
```

এটা Preflight-এর উপর বসবে।

---

# Disable করা যায়?

হ্যাঁ।

যখন:

- existing legacy project
    
- bootstrap + tailwind together
    
- third-party UI break করছে
    

v3:

```js
module.exports = {
  corePlugins: {
    preflight: false,
  },
}
```

([tailwindcss.cn](https://www.tailwindcss.cn/docs/preflight?utm_source=chatgpt.com "Preflight - TailwindCSS中文文档 | TailwindCSS中文网"))

---

# Common confusion

**“আমার button style disappear করল কেন?”**

কারণ Preflight browser default button style remove করেছে 😄

Example:

Before Tailwind:

```html
<button>Click</button>
```

Looks like button.

After Tailwind:

```html
<button>Click</button>
```

May look plain text.

Solution:

নিজে style দাও।

---

এক লাইনে:

**Preflight = Tailwind-এর global reset CSS, যা browser default style remove করে clean canvas দেয়।**

---------

