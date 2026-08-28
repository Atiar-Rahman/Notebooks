হ্যাঁ, **React-এ Lottie animation ব্যবহার করা খুব সহজ**। Lottie মূলত JSON-based animation, তাই website-এ lightweight animated illustration ব্যবহার করতে পারো।

### 1. Package install

React/Vite হলে:

```bash
npm install lottie-react
```

### 2. Animation JSON রাখো

ধরো:

```text
src/
├── assets/
│   └── animation.json
├── App.jsx
└── main.jsx
```

### 3. Component-এ ব্যবহার

```jsx
import Lottie from "lottie-react";
import animationData from "./assets/animation.json";

function App() {
  return (
    <div>
      <Lottie
        animationData={animationData}
        loop={true}
      />
    </div>
  );
}

export default App;
```

এটাই basic setup।

### 4. Width/height control

Tailwind ব্যবহার করলে:

```jsx
<Lottie
  animationData={animationData}
  loop={true}
  className="w-64 h-64"
/>
```

অথবা:

```jsx
<div className="w-80 h-80">
  <Lottie
    animationData={animationData}
    loop
  />
</div>
```

### 5. Autoplay বন্ধ করতে চাইলে

```jsx
<Lottie
  animationData={animationData}
  loop={false}
  autoplay={false}
/>
```

### 6. React state দিয়ে control

```jsx
import { useState } from "react";
import Lottie from "lottie-react";
import animationData from "./assets/animation.json";

function App() {
  const [play, setPlay] = useState(false);

  return (
    <div>
      <Lottie
        animationData={animationData}
        play={play}
        loop={false}
      />

      <button onClick={() => setPlay(true)}>
        Play
      </button>
    </div>
  );
}
```

তবে `lottie-react`-এর API অনুযায়ী animation control করার জন্য `lottieRef` ব্যবহার করে `play()`, `pause()`, `stop()` ইত্যাদিও করা যায়।

---

## Next.js হলে একটু আলাদা ⚠️

Next.js App Router-এ component-টি client-side হওয়া দরকার:

```jsx
"use client";

import Lottie from "lottie-react";
import animationData from "@/assets/animation.json";

export default function Animation() {
  return (
    <Lottie
      animationData={animationData}
      loop
    />
  );
}
```

তারপর:

```jsx
import Animation from "@/components/Animation";

export default function Home() {
  return (
    <main>
      <Animation />
    </main>
  );
}
```

### 🧠 সহজ architecture

```text
Lottie JSON
    ↓
lottie-react
    ↓
React Component
    ↓
Tailwind CSS
    ↓
Website UI
```

**Next.js + TypeScript + Tailwind** ব্যবহার করলে চাইলে আমি তোমাকে একটি **professional Lottie component** বানিয়ে দেখাতে পারি—যেখানে `width`, `height`, `loop`, `autoplay`, `speed`, `className` সব props দিয়ে control করা যাবে।


install lottie react from this site.

```
https://www.npmjs.com/package/lottie-react
```

[https://www.npmjs.com/package/lottie-react](https://www.npmjs.com/package/lottie-react)



