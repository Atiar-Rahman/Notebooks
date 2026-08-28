React-এ **Google Fonts** ব্যবহার করার কয়েকটি সহজ উপায় আছে। তুমি যদি সাধারণ React (Vite) ব্যবহার করো, সবচেয়ে সহজ হলো CSS `@import` অথবা HTML `<link>`।

### ✅ Method 1: CSS `@import`

`src/index.css`-এ:

```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

body {
  font-family: 'Poppins', sans-serif;
}
```

তারপর `main.jsx`-এ CSS import করা আছে কিনা নিশ্চিত করো:

```jsx
import "./index.css";
```

---

### ✅ Method 2: `index.html`-এ `<link>` — Recommended

Vite React project-এর `index.html`:

```html
<head>
  <link
    rel="preconnect"
    href="https://fonts.googleapis.com"
  />
  <link
    rel="preconnect"
    href="https://fonts.gstatic.com"
    crossorigin
  />

  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap"
    rel="stylesheet"
  />
</head>
```

তারপর CSS:

```css
body {
  font-family: "Poppins", sans-serif;
}
```

### 🎯 যদি Tailwind CSS ব্যবহার করো

Google Font load করার পর:

```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

@theme {
  --font-poppins: "Poppins", sans-serif;
}
```

তারপর:

```jsx
<h1 className="font-poppins">
  Hello React
</h1>
```

**Next.js হলে পদ্ধতিটা আলাদা এবং আরও ভালো:** `next/font/google` ব্যবহার করা যায়।

----
Next.js-এ Google Font ব্যবহার করার **সবচেয়ে recommended উপায় হলো `next/font/google`**। এতে আলাদা করে Google Fonts-এর `<link>` বা CSS `@import` করার দরকার হয় না।

### 1. `app/layout.tsx`

ধরো তুমি **Poppins** font ব্যবহার করতে চাও:

```tsx
import { Poppins } from "next/font/google";
import "./globals.css";

const poppins = Poppins({
  subsets: ["latin"],
  weight: ["400", "500", "600", "700"],
});

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body className={poppins.className}>
        {children}
      </body>
    </html>
  );
}
```

এখন তোমার পুরো application-এ Poppins ব্যবহার হবে।

---

### 2. শুধু নির্দিষ্ট component-এ ব্যবহার করতে চাইলে

```tsx
import { Poppins } from "next/font/google";

const poppins = Poppins({
  subsets: ["latin"],
  weight: ["400", "600", "700"],
});

export default function Home() {
  return (
    <div className={poppins.className}>
      <h1>Hello Next.js</h1>
      <p>This uses Poppins.</p>
    </div>
  );
}
```

---

### 3. Variable font হলে

কিছু Google Font variable weight support করে। তখন:

```tsx
import { Inter } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
});
```

তারপর:

```tsx
<body className={inter.className}>
  {children}
</body>
```

---

### 🧠 React বনাম Next.js

**React/Vite:**

```css
@import url("https://fonts.googleapis.com/...");
```

**Next.js:**

```tsx
import { Poppins } from "next/font/google";
```

তারপর:

```tsx
<body className={poppins.className}>
```

👉 Next.js project হলে **`next/font/google` ব্যবহার করাই ভালো**, কারণ font loading Next.js নিজেই optimize করতে পারে।
যদি তুমি জানতে চাও **“সব ধরনের মানুষের জন্য কোন font সবচেয়ে ভালো?”**, তাহলে একটাই universally best font নেই। তবে website/UI-এর জন্য কিছু font খুব জনপ্রিয় ও readable।

### ⭐ আমার recommendation

| Font          | কোথায় ভালো                       | আমার rating |
| ------------- | --------------------------------- | ----------: |
| **Inter**     | Modern website, dashboard, SaaS   |       ⭐⭐⭐⭐⭐ |
| **Poppins**   | Modern/creative website           |       ⭐⭐⭐⭐⭐ |
| **Roboto**    | General website, Android-style UI |       ⭐⭐⭐⭐⭐ |
| **Open Sans** | Long text, general websites       |        ⭐⭐⭐⭐ |
| **Noto Sans** | বহু ভাষা/Unicode support          |       ⭐⭐⭐⭐⭐ |

### 🥇 যদি একটি বেছে নিতে বলো

**Inter** → Modern website/UI-এর জন্য আমার প্রথম পছন্দ।

Next.js:

```tsx
import { Inter } from "next/font/google";

const inter = Inter({
  subsets: ["latin"],
});
```

তারপর:

```tsx
<html lang="en">
  <body className={inter.className}>
    {children}
  </body>
</html>
```

### 🇧🇩 বাংলা + English website হলে

তোমার জন্য **Noto Sans Bengali + Noto Sans** ভালো choice হতে পারে, কারণ বাংলা এবং English দুটোই সুন্দরভাবে handle করা গুরুত্বপূর্ণ।

উদাহরণ:

```tsx
import { Noto_Sans, Noto_Sans_Bengali } from "next/font/google";

const english = Noto_Sans({
  subsets: ["latin"],
});

const bengali = Noto_Sans_Bengali({
  subsets: ["bengali"],
});
```

**Short answer:**
👉 English UI → **Inter**
👉 Bangla + English → **Noto Sans family**
👉 Stylish/modern landing page → **Poppins**
হ্যাঁ, **Google Font-এর weight ব্যবহার হবে**, যদি font-টি সঠিকভাবে load করা থাকে। তবে একটা বিষয় পরিষ্কার করি:

### তোমার Google Sans Flex

তুমি যদি এটা ব্যবহার করো:

```css
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Flex:opsz,wght@6..144,1..1000&display=swap');
```

তাহলে `wght@1..1000` হলো **variable weight range**।

Tailwind দিয়ে:

```jsx
<h1 className="font-[400]">Normal</h1>
<h1 className="font-[500]">Medium</h1>
<h1 className="font-[600]">Semi Bold</h1>
<h1 className="font-[700]">Bold</h1>
<h1 className="font-[800]">Extra Bold</h1>
<h1 className="font-[900]">Black</h1>
```

এগুলো Google Sans Flex-এর weight ব্যবহার করবে।

এমনকি:

```jsx
<h1 className="font-[550]">Google Sans Flex</h1>
```

এটাও ব্যবহার করতে পারবে।

### ⚠️ কিন্তু `font-[700]` একা যথেষ্ট নয়

Tailwind-কে আগে বলতে হবে যে **Google Sans Flex-ই font family**।

উদাহরণ:

```css
@import url('https://fonts.googleapis.com/css2?family=Google+Sans+Flex:opsz,wght@6..144,1..1000&display=swap');

@theme {
  --font-google: "Google Sans Flex", sans-serif;
}
```

তারপর:

```jsx
<h1 className="font-google font-[700]">
  Hello World
</h1>
```

এখানে:

```text
font-google → Google Sans Flex
font-[700]  → weight 700
```

### সংক্ষেপে

**হ্যাঁ ✅ Google Font-এর weight কাজ করবে।**

```text
Google Sans Flex
      ↓
wght 1–1000
      ↓
Tailwind
      ↓
font-[400]
font-[500]
font-[550]
font-[700]
font-[900]
...
```

তবে বাস্তবে সাধারণ UI-তে `400, 500, 600, 700`-এর মতো weight-ই বেশি ব্যবহার করা হয়।
