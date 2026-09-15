# Context API-কে সহজভাবে মনে রাখার জন্য তোমাকে শুধু **৪টা step** মনে রাখতে হবে:

> **Create → Provider → Wrap → Consume**

## Context API — সহজ Complete Summary

ধরো, আমরা একটা **Counter** বানাবো যেটা অনেক component থেকে access করা যাবে।

### Step 1: Context তৈরি করো

একটা `CounterProvider.jsx` file বানাও:

CounterProvider.jsx

```
import { createContext, useState } from "react";

// 1. Context তৈরি
export const CounterContext = createContext(null);

// 2. Provider তৈরি
const CounterProvider = ({ children }) => {
  const [counter, setCounter] = useState(0);

  return (
    <CounterContext.Provider value={{ counter, setCounter }}>
      {children}
    </CounterContext.Provider>
  );
};

export default CounterProvider;
```

এখানে সবচেয়ে important অংশ:

```
createContext(null);
```

এটা Context তৈরি করছে।

আর:

```
<CounterContext.Provider value={{ counter, setCounter }}>
```

এটা Context-এর মধ্যে data পাঠাচ্ছে।

---

# Step 2: Provider দিয়ে App-কে Wrap করো

`main.jsx` বা `App.jsx`-এ:

main.jsx

```
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App";
import CounterProvider from "./context/CounterProvider";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <CounterProvider>
      <App />
    </CounterProvider>
  </StrictMode>
);
```

এখন `App` এবং `App`-এর ভিতরের সব child component Context access করতে পারবে।

এটাকে এভাবে ভাবো:

```
CounterProvider
      │
      └── App
           │
           ├── Counter
           │
           ├── Display
           │
           └── OtherComponent
```

`CounterProvider` হচ্ছে একটা **data container**।

---

# Step 3: Component-এর মধ্যে Context-এর data নাও

React 19 হলে তুমি `use()` ব্যবহার করতে পারো।

```
import { use } from "react";
import { CounterContext } from "../context/CounterProvider";

const Counter = () => {
  const { counter, setCounter } = use(CounterContext);

  return (
    <div>
      <h1>{counter}</h1>

      <button onClick={() => setCounter(prev => prev + 1)}>
        Increase
      </button>

      <button onClick={() => setCounter(prev => prev - 1)}>
        Decrease
      </button>
    </div>
  );
};

export default Counter;
```

আর traditional way:

```
import { useContext } from "react";

const { counter, setCounter } = useContext(CounterContext);
```

দুটোর কাজ এখানে একই।

---

# Step 4: Props আর লাগবে না

Context ব্যবহার করার বড় সুবিধা হলো **prop drilling করতে হয় না**।

Context ছাড়া:

```
App
 ↓ counter
Parent
 ↓ counter
Child
 ↓ counter
Counter
```

অনেক জায়গায় props পাঠাতে হচ্ছে।

Context ব্যবহার করলে:

```
        CounterProvider
              │
        ┌─────┼─────┐
        ↓     ↓     ↓
      App  Counter Display
             ↑
             │
          Context
```

যে component-এর দরকার, সে সরাসরি Context থেকে data নিতে পারে।

তাই এটা লিখতে হবে না:

```
<Counter counter={counter} setCounter={setCounter} />
```

এবং এটাও না:

```
const Counter = ({ counter, setCounter }) => {};
```

বরং:

```
const Counter = () => {
  const { counter, setCounter } = use(CounterContext);
};
```

---

# `createContext()`-এ কী দিতে হবে?

এটা খুব important।

```
createContext(defaultValue)
```

এখানে `defaultValue` হলো **fallback value**।

### Simple example

```
const ThemeContext = createContext("light");
```

Provider-এর বাইরে কেউ Context access করলে:

```
"light"
```

পাবে।

তোমার Counter-এর ক্ষেত্রে:

```
const CounterContext = createContext(null);
```

দিতে পারো।

কারণ actual value Provider থেকে আসছে:

```
<CounterContext.Provider
  value={{ counter, setCounter }}
>
```

### মনে রাখো:

```
createContext(null)
        ↓
Default / fallback

Provider value={...}
        ↓
Actual data
```

---

# `value` কেন দিতে হয়?

এটাই Context-এর মূল জায়গা।

```
<CounterContext.Provider
  value={{ counter, setCounter }}
>
```

এখানে তুমি বলছো:

> "এই Provider-এর ভিতরের component-গুলো `counter` এবং `setCounter` access করতে পারবে।"

তারপর component-এ:

```
const { counter, setCounter } = use(CounterContext);
```

তুমি সেই data পেয়ে যাচ্ছো।

---

# `children` কী?

এটাও খুব সহজ।

```
const CounterProvider = ({ children }) => {
```

যখন তুমি লিখো:

```
<CounterProvider>
  <App />
</CounterProvider>
```

তখন:

```
children = <App />
```

অর্থাৎ:

```
<CounterContext.Provider>
  {children}
</CounterContext.Provider>
```

মানে essentially:

```
<CounterContext.Provider>
  <App />
</CounterContext.Provider>
```

---

# পুরো Flow একবার দেখো

### 1. State তৈরি

```
const [counter, setCounter] = useState(0);
```

↓

### 2. Context তৈরি

```
const CounterContext = createContext(null);
```

↓

### 3. Provider-এর মাধ্যমে data পাঠানো

```
<CounterContext.Provider value={{ counter, setCounter }}>
```

↓

### 4. App-কে Provider দিয়ে wrap করা

```
<CounterProvider>
  <App />
</CounterProvider>
```

↓

### 5. যেকোনো child থেকে data নেওয়া

React 19:

```
const { counter, setCounter } = use(CounterContext);
```

অথবা:

```
const { counter, setCounter } = useContext(CounterContext);
```

---

# একটা Golden Template মনে রাখো

যেকোনো Context বানানোর সময় এই pattern follow করতে পারো:

Context API Golden Template

```
// ContextName.jsx

import { createContext, useState } from "react";

// 1. Create Context
export const MyContext = createContext(null);

// 2. Create Provider
const MyProvider = ({ children }) => {

  // 3. State / Data
  const [data, setData] = useState();

  return (
    // 4. Provide data
    <MyContext.Provider value={{ data, setData }}>
      {children}
    </MyContext.Provider>
  );
};

export default MyProvider;
```

Then in `main.jsx`:

```
<MyProvider>
  <App />
</MyProvider>
```

Then in any child component:

```
import { use } from "react";
import { MyContext } from "./MyContext";

const Component = () => {
  const { data, setData } = use(MyContext);

  // use data...
};
```

## এক লাইনে পুরো Context API

**Context তৈরি করো → Provider বানাও → Provider দিয়ে App wrap করো → `value` দিয়ে data পাঠাও → child component-এ `use()`/`useContext()` দিয়ে data নাও।**

এই flow-টা মাথায় থাকলে Context API-এর ৮০–৯০% basic use case সহজেই করতে পারবে।


---
