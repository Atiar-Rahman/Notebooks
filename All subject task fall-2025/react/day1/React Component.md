ঠিক আছে 😎 — এবার React এ **Component কী এবং কিভাবে তৈরি করে** সেটা step by step দেখাই।

---

# 🎯 **React Component কী?**

* React component হলো **reusable UI block**
* এটা function বা class হতে পারে
* Component এর মধ্যে **UI (JSX) + logic (state, handler)** থাকে
* React এ component দুইভাবে বানানো হয়:

  1. **Function Component (Modern & Recommended)**
  2. **Class Component (পুরানো, কম ব্যবহৃত)**

---

# 🔥 **1️⃣ Function Component**

```js
// Hello.jsx
function Hello() {
  return <h1>Hello World</h1>;
}

export default Hello;
```

* `Hello` নামের component তৈরি হল
* এটা JSX return করে → ব্রাউজারে render হবে
* `export default` দিলে অন্য file এ import করা যাবে

---

### ✅ **Use in another component**

```js
import Hello from "./Hello";

function App() {
  return (
    <div>
      <Hello />   {/* Component use করা হলো */}
    </div>
  );
}

export default App;
```

---

# 🔥 **2️⃣ Function Component with Props**

```js
// Card.jsx
function Card({ title, content }) {
  return (
    <div style={{ border: "1px solid gray", padding: "10px" }}>
      <h2>{title}</h2>
      <p>{content}</p>
    </div>
  );
}

export default Card;
```

```js
// App.jsx
import Card from "./Card";

function App() {
  return (
    <div>
      <Card title="Card 1" content="This is card 1" />
      <Card title="Card 2" content="This is card 2" />
    </div>
  );
}

export default App;
```

* Props দিয়ে dynamic content পাঠানো যায়
* Component reuse করা যায়

---

# 🔥 **3️⃣ Function Component with State & Event Handler**

```js
import { useState } from "react";

function ToggleCard({ title }) {
  const [isOpen, setIsOpen] = useState(false);

  const handleToggle = () => {
    setIsOpen(!isOpen);
  };

  return (
    <div style={{ border: "1px solid gray", padding: "10px", margin: "10px" }}>
      <h2>{title}</h2>
      <button onClick={handleToggle}>
        {isOpen ? "Hide" : "Show"}
      </button>
      {isOpen && <p>Details about {title}</p>}
    </div>
  );
}

export default ToggleCard;
```

---

# 🔑 **Key Points**

1. Component **function** / **class** হতে পারে
2. JSX return করে UI render করে
3. Props দিয়ে **dynamic data** পাঠানো যায়
4. State & handler দিয়ে **interactive component** বানানো যায়
5. অন্য component এ import + use করা যায়

---

💡 **Tip:**

* সব modern React project **Function Component + Hooks (useState, useEffect)** use করে
* Class Component খুব কমই লাগে

---
# **React built-in components** কখন, কোন পরিস্থিতিতে এবং কিভাবে ব্যবহার করতে হয়। আমি step-by-step explain করি:

---

# 1️⃣ **`<Fragment>` (<> </>)**

**Purpose:**

* Multiple elements group করতে হবে কিন্তু extra DOM node (div/span) তৈরি না করতে চাইলে

**Use Case:**

* Parent element ছাড়া multiple JSX return করতে চাইলে

**Example:**

```js
function App() {
  return (
    <>
      <h1>Title</h1>
      <p>Paragraph</p>
    </>
  );
}
```

✅ **Use When:** Multiple child elements return করতে হবে, কিন্তু extra `<div>` avoid করতে হবে

---

# 2️⃣ **`<StrictMode>`**

**Purpose:**

* Development mode এ warnings, deprecated methods detect করার জন্য

**Use Case:**

* App এর root এ wrap করে development এ code safety check করতে

**Example:**

```js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

✅ **Use When:** Development environment, production এ optional

---

# 3️⃣ **`<Suspense>`**

**Purpose:**

* Lazy loaded component (React.lazy) render করার সময় fallback দেখানোর জন্য

**Use Case:**

* Big component / module split করতে চাইলে, load time এ spinner বা loading text দেখাতে

**Example:**

```js
import React, { Suspense, lazy } from "react";

const LazyComponent = lazy(() => import("./LazyComponent"));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

✅ **Use When:** Component dynamically load হবে → loading UI দিতে হবে

---

# 4️⃣ **`<Profiler>`**

**Purpose:**

* Performance measure (render time, re-renders)

**Use Case:**

* Large app optimization এর সময়

**Example:**

```js
import React, { Profiler } from "react";

function App() {
  const onRenderCallback = (
    id, phase, actualDuration, baseDuration, startTime, commitTime
  ) => {
    console.log({ id, phase, actualDuration });
  };

  return (
    <Profiler id="App" onRender={onRenderCallback}>
      <MyComponent />
    </Profiler>
  );
}
```

✅ **Use When:** App optimization / performance profiling

---

# 5️⃣ **`<Activity>`**

**Purpose:**

* Mostly React Native / concurrent mode feature
* Track user activity or manage concurrent updates

**Use Case:**

* Mobile app / experimental concurrent React feature

---

# 6️⃣ **`<ViewTransition>`**

**Purpose:**

* Experimental feature for page/view transition
* Smooth animation between views

**Use Case:**

* App with dynamic page transitions

---

# ⚡ **Summary Table**

| Component          | Use Case / When            | Example / Note          |
| ------------------ | -------------------------- | ----------------------- |
| `<Fragment>`       | Multiple JSX, no extra div | `<>...</>`              |
| `<StrictMode>`     | Development, warnings      | Wrap root `<App>`       |
| `<Suspense>`       | Lazy loading               | fallback spinner        |
| `<Profiler>`       | Performance check          | Measure render time     |
| `<Activity>`       | React Native / concurrent  | Experimental            |
| `<ViewTransition>` | Page transitions           | Experimental / advanced |

---

💡 **Rule of Thumb:**

* **Daily React web app:** mostly `<Fragment>`, `<StrictMode>`, `<Suspense>`
* **Performance debug:** `<Profiler>`
* **Advanced / experimental:** `<Activity>`, `<ViewTransition>`

---

যদি চাও আমি তোমার জন্য **একটা mini project example** বানিয়ে দেখাই যেখানে:

* `<Fragment>`, `<StrictMode>`, `<Suspense>` use হবে
* Multiple card map + toggle + parent state + child show/hide ready
* একদম **React best practice** follow করে

চাও আমি বানাই?
