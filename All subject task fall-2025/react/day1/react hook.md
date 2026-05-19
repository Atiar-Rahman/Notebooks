React শিখতে গেলে সব hook মুখস্থ করার দরকার নেই — **daily use হয় এমন কিছু important hook** ভালোভাবে জানলেই 80% কাজ হয়ে যায়।

আমি তোমাকে **real project perspective** থেকে explain করছি 👇

---

# 🔥 Most Important React Hooks (Daily Use)

## 1️⃣ `useState` — (Must Know ⭐)

👉 Component এর data/state handle করার জন্য

### কখন ব্যবহার করবা?

* Form input
* Toggle (open/close)
* Counter
* UI change

```js
const [count, setCount] = useState(0);
```

✔ Example:

* button click → count increase
* modal open/close

---

## 2️⃣ `useEffect` — (Very Important ⭐)

👉 Side effect handle করার জন্য

### কখন ব্যবহার করবা?

* API call
* Data fetch
* Component load হলে কিছু run করা
* Event listener add/remove

```js
useEffect(() => {
  fetchData();
}, []);
```

✔ Example:

* page load → data load
* dependency change → re-run

---

## 3️⃣ `useContext` — (Medium but useful)

👉 Global data share করার জন্য (prop drilling avoid)

### কখন ব্যবহার করবা?

* User authentication
* Theme (dark/light)
* Language

```js
const user = useContext(UserContext);
```

---

## 4️⃣ `useRef` — (Underrated but powerful 🔥)

👉 DOM access + value store (without re-render)

### কখন ব্যবহার করবা?

* Input focus করা
* Timer/store previous value
* Scroll control

```js
const inputRef = useRef();
```

✔ Example:

```js
inputRef.current.focus();
```

---

## 5️⃣ `useReducer` — (Advanced State 🔥)

👉 Complex state management

### কখন ব্যবহার করবা?

* Large form
* Multiple state logic
* Redux alternative (small project)

```js
const [state, dispatch] = useReducer(reducer, initialState);
```

---

## 6️⃣ `useMemo` — (Performance Optimization)

👉 Expensive calculation cache করার জন্য

### কখন ব্যবহার করবা?

* Heavy calculation
* Filter/sort large data

```js
const result = useMemo(() => calculate(data), [data]);
```

---

## 7️⃣ `useCallback` — (Optimization)

👉 Function re-create হওয়া prevent করে

### কখন ব্যবহার করবা?

* Child component re-render prevent করতে
* useMemo/useEffect এর সাথে

```js
const handleClick = useCallback(() => {}, []);
```

---

## 8️⃣ `useNavigate` (React Router)

👉 Page change/navigation

```js
const navigate = useNavigate();
navigate('/home');
```

✔ Example:

* login → dashboard redirect

---

# 🧠 Real Project Use Map

| Situation     | Hook                  |
| ------------- | --------------------- |
| Form input    | useState              |
| API call      | useEffect             |
| Global user   | useContext            |
| DOM access    | useRef                |
| Complex logic | useReducer            |
| Performance   | useMemo / useCallback |
| Routing       | useNavigate           |

---

# 🚀 Beginner → Pro Strategy

👉 **Step 1 (Must learn first):**

* useState
* useEffect

👉 **Step 2:**

* useContext
* useRef

👉 **Step 3 (Advanced):**

* useReducer
* useMemo
* useCallback

---

# ⚠️ Common Mistake (Important)

❌ সব জায়গায় useMemo/useCallback use করা
✔ Only when needed (performance issue হলে)

❌ useEffect dependency ভুল দেওয়া
✔ dependency array বুঝতে হবে

---

# 🔥 Simple Rule (Golden)

👉 UI change → `useState`
👉 Side effect → `useEffect`
👉 Global data → `useContext`
👉 Performance → `useMemo/useCallback`

---

চাও হলে আমি তোমাকে 👇 এগুলা next level এ নিতে পারি:

* Real project example (login system + dashboard)
* Custom hook বানানো
* Interview question + answer (React hooks)

বললেই step-by-step advanced level এ নিয়ে যাব 🚀

--------
ঠিক আছে! আমি **Custom Hook** ধাপে ধাপে explain করি। 😎

React এ **Custom Hook** হল একটি normal function যা hook এর logic reuse করার জন্য বানানো হয়। নিয়ম: **নাম `use` দিয়ে শুরু করতে হবে।**

---

# 1️⃣ Custom Hook এর Basic Structure

```js
import { useState, useEffect } from "react";

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);
  const decrement = () => setCount(count - 1);

  return { count, increment, decrement };
}

export default useCounter;
```

### ব্যবহার:

```js
import useCounter from "./useCounter";

function App() {
  const { count, increment, decrement } = useCounter(5);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
}
```

✅ Result:

* Count value **reuse করা possible**
* Logic component থেকে **separate**

---

# 2️⃣ Custom Hook for API Call

```js
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => {
        setData(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err);
        setLoading(false);
      });
  }, [url]);

  return { data, loading, error };
}

export default useFetch;
```

### ব্যবহার:

```js
import useFetch from "./useFetch";

function App() {
  const { data, loading, error } = useFetch("https://jsonplaceholder.typicode.com/posts");

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error.message}</p>;

  return (
    <div>
      {data.map(post => <h3 key={post.id}>{post.title}</h3>)}
    </div>
  );
}
```

✅ Benefit:

* API call logic **reuse** করা যায় multiple components এ
* Component clean থাকে

---

# 3️⃣ Rule of Custom Hook

1. Name must start with `use`
2. Custom hook can use **built-in hooks** (`useState`, `useEffect`, `useContext` …)
3. Avoid side effect outside hooks
4. Return whatever you want: state, function, object

---

# 4️⃣ Advanced Example (Form Input Hook)

```js
import { useState } from "react";

function useInput(initialValue) {
  const [value, setValue] = useState(initialValue);

  const onChange = (e) => setValue(e.target.value);
  const reset = () => setValue("");

  return { value, onChange, reset };
}

export default useInput;
```

### ব্যবহার:

```js
import useInput from "./useInput";

function Form() {
  const name = useInput("");
  const email = useInput("");

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(name.value, email.value);
    name.reset();
    email.reset();
  };

  return (
    <form onSubmit={handleSubmit}>
      <input placeholder="Name" {...name} />
      <input placeholder="Email" {...email} />
      <button>Submit</button>
    </form>
  );
}
```

✅ Advantage:

* Input handling **reuse possible**
* Component short এবং clean থাকে

---

💡 **Tip:**
Custom hooks are perfect when you see **same logic repeated** in multiple components.

---

আমি চাইলে তোমার জন্য **real project example** বানাতে পারি যেখানে:

* API call
* Form handling
* Authentication
  সব কিছুর জন্য **custom hooks** থাকবে।

চাও আমি সেটা বানাই?
হ্যাঁ, React এ **multiple context** একসাথে use করা যায়, কিন্তু সরাসরি `useContext` একাধিকবার call করতে হবে। 😎 আমি step-by-step দেখাচ্ছি।

---

# 1️⃣ Multiple Context তৈরি করা

```js
import { createContext, useState } from "react";

// 1. User Context
export const UserContext = createContext();

// 2. Theme Context
export const ThemeContext = createContext();

export const AppProvider = ({ children }) => {
  const [user, setUser] = useState({ name: "Atiar", loggedIn: true });
  const [theme, setTheme] = useState("dark");

  return (
    <UserContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        {children}
      </ThemeContext.Provider>
    </UserContext.Provider>
  );
};
```

✅ এখানে **nested provider** ব্যবহার করা হয়েছে।

---

# 2️⃣ Component এ Multiple Context ব্যবহার করা

```js
import { useContext } from "react";
import { UserContext, ThemeContext } from "./AppProvider";

function Dashboard() {
  const { user, setUser } = useContext(UserContext);
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>
    </div>
  );
}
```

---

# 3️⃣ Cleaner Approach — Custom Hook ব্যবহার করা

```js
// useAppContext.js
import { useContext } from "react";
import { UserContext, ThemeContext } from "./AppProvider";

export const useAppContext = () => {
  const userContext = useContext(UserContext);
  const themeContext = useContext(ThemeContext);

  return { ...userContext, ...themeContext };
};
```

### ব্যবহার:

```js
import { useAppContext } from "./useAppContext";

function Dashboard() {
  const { user, setUser, theme, setTheme } = useAppContext();

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>
    </div>
  );
}
```

✅ Benefit:

* Component এ multiple `useContext` call **একটা জায়গায় wrap করা**
* Cleaner & reusable

---

# 4️⃣ Shortcut — Object Merge করে Provider Wrap করা

```js
// combinedProviders.js
import { UserContext, ThemeContext } from "./AppProvider";

export const CombinedProviders = ({ children, userValue, themeValue }) => (
  <UserContext.Provider value={userValue}>
    <ThemeContext.Provider value={themeValue}>
      {children}
    </ThemeContext.Provider>
  </UserContext.Provider>
);
```

> Large project এ nested context অনেক হলে, **wrapper + custom hook** ব্যবহার করা clean approach।

---

💡 **Pro Tip:**

* Context should be used **for global state** (like auth, theme, language).
* Local state → `useState` preferred.

---

যদি চাও আমি তোমার জন্য **3–4 context একসাথে handle করা real project pattern** দেখাতে পারি যেখানে:

* Auth
* Theme
* Notification
* Cart

সব কিছুর context + custom hook ready থাকবে।

চাও আমি সেটা বানাই?
চল, আমি তোমার জন্য একটি **real project pattern** বানাচ্ছি যেখানে আমরা **4টি context একসাথে handle** করব:

1. **AuthContext** – user login/logout info
2. **ThemeContext** – dark/light mode
3. **NotificationContext** – global toast/message
4. **CartContext** – shopping cart state

এখানে আমরা **nested provider + single custom hook** use করব, যাতে component এ শুধু একবার hook call করলেই সব context access করা যায়।

---

## 1️⃣ Context Setup

```js
// contexts/AppContext.js
import { createContext, useState } from "react";

// 1. Auth
export const AuthContext = createContext();
// 2. Theme
export const ThemeContext = createContext();
// 3. Notification
export const NotificationContext = createContext();
// 4. Cart
export const CartContext = createContext();

export const AppProvider = ({ children }) => {
  // Auth state
  const [user, setUser] = useState({ name: "Atiar", loggedIn: true });

  // Theme state
  const [theme, setTheme] = useState("dark");

  // Notification state
  const [notification, setNotification] = useState(null);

  // Cart state
  const [cart, setCart] = useState([]);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        <NotificationContext.Provider value={{ notification, setNotification }}>
          <CartContext.Provider value={{ cart, setCart }}>
            {children}
          </CartContext.Provider>
        </NotificationContext.Provider>
      </ThemeContext.Provider>
    </AuthContext.Provider>
  );
};
```

---

## 2️⃣ Custom Hook for Multiple Contexts

```js
// hooks/useAppContext.js
import { useContext } from "react";
import { AuthContext, ThemeContext, NotificationContext, CartContext } from "../contexts/AppContext";

export const useAppContext = () => {
  const auth = useContext(AuthContext);
  const theme = useContext(ThemeContext);
  const notification = useContext(NotificationContext);
  const cart = useContext(CartContext);

  return { ...auth, ...theme, ...notification, ...cart };
};
```

✅ এবার component এ **single hook call** করলেই সব access করা যাবে।

---

## 3️⃣ Example Component

```js
// components/Dashboard.js
import { useAppContext } from "../hooks/useAppContext";

function Dashboard() {
  const { user, setUser, theme, setTheme, notification, setNotification, cart, setCart } = useAppContext();

  const addToCart = (item) => {
    setCart([...cart, item]);
    setNotification(`Added ${item} to cart!`);
  };

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000", padding: "20px" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>

      <h2>Cart Items: {cart.length}</h2>
      <button onClick={() => addToCart("Apple")}>Add Apple</button>

      {notification && <p style={{ marginTop: "10px", color: "green" }}>{notification}</p>}
    </div>
  );
}

export default Dashboard;
```

---

## 4️⃣ App Wrapper

```js
// App.js
import { AppProvider } from "./contexts/AppContext";
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <AppProvider>
      <Dashboard />
    </AppProvider>
  );
}

export default App;
```

---

### ✅ Advantages of this pattern:

1. **Single source of truth** – সব global state এক জায়গায়।
2. **Custom hook** – component এ cleaner access।
3. **Scalable** – নতুন context লাগলে সহজে add করা যাবে।
4. **Reusability** – multiple components এ same hook use করা যায়।

---

যদি চাও, আমি তোমার জন্য **আরেকটি উন্নত version বানাতে পারি** যেখানে:

* **useReducer + context combination**
* বড় project এ state management আরও scalable হবে।

চাও আমি সেটা দেখাই?
ঠিক আছে, এই nested provider structure এ **প্রতিটা Provider এর value আলাদাভাবে দিতে হবে**, কারণ **প্রতিটা context নিজস্ব state/share করে**।

আমি step by step দেখাচ্ছি:

---

## 1️⃣ প্রতিটা Provider এ value

```js
<AuthContext.Provider value={{ user, setUser }}>
  <ThemeContext.Provider value={{ theme, setTheme }}>
    <NotificationContext.Provider value={{ notification, setNotification }}>
      <CartContext.Provider value={{ cart, setCart }}>
        {children}
      </CartContext.Provider>
    </NotificationContext.Provider>
  </ThemeContext.Provider>
</AuthContext.Provider>
```

✅ এখানে:

1. **AuthContext** → `{ user, setUser }`
2. **ThemeContext** → `{ theme, setTheme }`
3. **NotificationContext** → `{ notification, setNotification }`
4. **CartContext** → `{ cart, setCart }`

> প্রতিটা Provider কে আলাদা object পাঠানো হয়।

---

## 2️⃣ Example Full Provider Component

```js
import { createContext, useState } from "react";

export const AuthContext = createContext();
export const ThemeContext = createContext();
export const NotificationContext = createContext();
export const CartContext = createContext();

export const AppProvider = ({ children }) => {
  const [user, setUser] = useState({ name: "Atiar", loggedIn: true });
  const [theme, setTheme] = useState("dark");
  const [notification, setNotification] = useState(null);
  const [cart, setCart] = useState([]);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        <NotificationContext.Provider value={{ notification, setNotification }}>
          <CartContext.Provider value={{ cart, setCart }}>
            {children}
          </CartContext.Provider>
        </NotificationContext.Provider>
      </ThemeContext.Provider>
    </AuthContext.Provider>
  );
};
```

---

## 3️⃣ Component এ ব্যবহার

```js
import { useContext } from "react";
import { AuthContext, ThemeContext, NotificationContext, CartContext } from "./AppProvider";

function Dashboard() {
  const { user } = useContext(AuthContext);
  const { theme, setTheme } = useContext(ThemeContext);
  const { notification, setNotification } = useContext(NotificationContext);
  const { cart, setCart } = useContext(CartContext);

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>
      <p>{notification}</p>
      <button onClick={() => setCart([...cart, "Apple"])}>Add Apple</button>
    </div>
  );
}
```

---

💡 **Tip:**

* Nested provider structure **clean separation** দেয়।
* প্রতিটা provider এর value **state + setter** object পাঠানো হয়।
* Component এ `useContext` একে একে call করা যায়।
* চাইলে **Custom hook** বানিয়ে সব context একসাথে access করানো যায়।

---

যদি চাও আমি তোমার জন্য **nested provider + custom hook** version বানিয়ে দেব, যাতে component এ **single hook call** করলেই সব context access করা যায়।

চাও আমি সেটা বানাই?


চল, আমি তোমার জন্য **nested provider + custom hook** version বানাচ্ছি, যাতে component এ **একবার hook call** করলেই সব context access করা যায়।

---

## 1️⃣ Context Setup (Nested Providers)

```js
// contexts/AppContext.js
import { createContext, useState } from "react";

// 1️⃣ Create Contexts
export const AuthContext = createContext();
export const ThemeContext = createContext();
export const NotificationContext = createContext();
export const CartContext = createContext();

// 2️⃣ Provider Component
export const AppProvider = ({ children }) => {
  // Auth State
  const [user, setUser] = useState({ name: "Atiar", loggedIn: true });

  // Theme State
  const [theme, setTheme] = useState("dark");

  // Notification State
  const [notification, setNotification] = useState(null);

  // Cart State
  const [cart, setCart] = useState([]);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        <NotificationContext.Provider value={{ notification, setNotification }}>
          <CartContext.Provider value={{ cart, setCart }}>
            {children}
          </CartContext.Provider>
        </NotificationContext.Provider>
      </ThemeContext.Provider>
    </AuthContext.Provider>
  );
};
```

---

## 2️⃣ Custom Hook for All Contexts

```js
// hooks/useAppContext.js
import { useContext } from "react";
import { AuthContext, ThemeContext, NotificationContext, CartContext } from "../contexts/AppContext";

export const useAppContext = () => {
  const auth = useContext(AuthContext);
  const theme = useContext(ThemeContext);
  const notification = useContext(NotificationContext);
  const cart = useContext(CartContext);

  return { ...auth, ...theme, ...notification, ...cart };
};
```

✅ এভাবে component এ **single hook call** করলেই সব context access করা যাবে।

---

## 3️⃣ Example Component

```js
// components/Dashboard.js
import { useAppContext } from "../hooks/useAppContext";

function Dashboard() {
  const { user, setUser, theme, setTheme, notification, setNotification, cart, setCart } = useAppContext();

  const addToCart = (item) => {
    setCart([...cart, item]);
    setNotification(`Added ${item} to cart!`);
  };

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000", padding: "20px" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>

      <h2>Cart Items: {cart.length}</h2>
      <button onClick={() => addToCart("Apple")}>Add Apple</button>

      {notification && <p style={{ marginTop: "10px", color: "green" }}>{notification}</p>}
    </div>
  );
}

export default Dashboard;
```

---

## 4️⃣ App Wrapper

```js
// App.js
import { AppProvider } from "./contexts/AppContext";
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <AppProvider>
      <Dashboard />
    </AppProvider>
  );
}

export default App;
```

---

### ✅ Advantages

1. Component এ **clean & simple access** – `useAppContext` একবার call করলেই সব state + setter পাওয়া যায়।
2. Nested provider এর benefit – **state separation + re-render control**।
3. Scalable – নতুন context সহজেই add করা যায়।
4. Component clean – provider logic থেকে separate।

---

যদি চাও, আমি তোমার জন্য এই setup **useReducer + context combination** দিয়ে upgrade করতে পারি, যাতে **state management বড় project এ আরও efficient** হয়।

চাও আমি সেটা দেখাই?


ঠিক আছে! তুমি যদি এই **nested context provider** ব্যবহার করো, তাহলে তোমার `main.jsx` (React 18+ project, Vite বা CRA) এ **AppProvider দিয়ে wrap** করতে হবে, যাতে **সারা app এ context access করা যায়**।

নিচে full setup দেখাচ্ছি step-by-step:

---

## 1️⃣ main.jsx setup (Vite project ধরেই নিচ্ছি)

```js
// main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { AppProvider } from "./contexts/AppContext";
import "./index.css"; // Tailwind বা normal CSS

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    {/* Wrap the entire app with AppProvider */}
    <AppProvider>
      <App />
    </AppProvider>
  </React.StrictMode>
);
```

✅ এখানে:

* `AppProvider` wrap করলে **nested providers active হবে**।
* এখন app এর **যেকোন component** থেকে `useContext` বা custom hook দিয়ে context access করা যাবে।

---

## 2️⃣ App.jsx Example

```js
// App.jsx
import Dashboard from "./components/Dashboard";

function App() {
  return (
    <div className="App">
      <Dashboard />
    </div>
  );
}

export default App;
```

---

## 3️⃣ Dashboard.jsx Example (context use)

```js
import { useContext } from "react";
import { AuthContext, ThemeContext, NotificationContext, CartContext } from "./contexts/AppContext";

function Dashboard() {
  const { user, setUser } = useContext(AuthContext);
  const { theme, setTheme } = useContext(ThemeContext);
  const { notification, setNotification } = useContext(NotificationContext);
  const { cart, setCart } = useContext(CartContext);

  return (
    <div style={{ background: theme === "dark" ? "#333" : "#fff", color: theme === "dark" ? "#fff" : "#000", padding: "20px" }}>
      <h1>Welcome, {user.name}</h1>
      <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>Toggle Theme</button>
      <button onClick={() => setCart([...cart, "Apple"])}>Add Apple to Cart</button>
      {notification && <p>{notification}</p>}
    </div>
  );
}

export default Dashboard;
```

---

## ✅ Key Notes

1. **AppProvider** সব component এর parent হতে হবে।
2. Nested providers automatically wrap children।
3. চাইলে `useAppContext` custom hook বানিয়ে সব context একসাথে access করা যেতে পারে।

---

যদি চাও, আমি তোমার জন্য **main.jsx + custom hook version** বানিয়ে দেখাতে পারি, যাতে `Dashboard` এ **একবার hook call** করলেই সব context access করা যায়।

চাও আমি সেটা বানাই?
React এ **multiple context** থাকলে, **custom hook বানানোর সময় তুমি দুইটা approach নিতে পারো**, কিন্তু practical & clean approach হলো **একটাই hook বানানো**, যেটা সব context একসাথে access দেয়। 😎

আমি clear করে explain করি:

---

## 1️⃣ One Custom Hook for All Contexts (Recommended ✅)

```js
// hooks/useAppContext.js
import { useContext } from "react";
import { AuthContext, ThemeContext, NotificationContext, CartContext } from "../contexts/AppContext";

export const useAppContext = () => {
  const auth = useContext(AuthContext);
  const theme = useContext(ThemeContext);
  const notification = useContext(NotificationContext);
  const cart = useContext(CartContext);

  // return merged object
  return { ...auth, ...theme, ...notification, ...cart };
};
```

### ব্যবহার:

```js
import { useAppContext } from "../hooks/useAppContext";

function Dashboard() {
  const { user, setUser, theme, setTheme, cart, setCart, notification, setNotification } = useAppContext();

  // code clean & simple
}
```

✅ **Benefits:**

* Component এ **single hook call**
* Cleaner & less boilerplate
* Scalable – নতুন context add করলে hook update করতে হবে, component change করার দরকার নেই

---

## 2️⃣ Separate Hook for Each Context (Optional ❌)

```js
export const useAuth = () => useContext(AuthContext);
export const useTheme = () => useContext(ThemeContext);
export const useNotification = () => useContext(NotificationContext);
export const useCart = () => useContext(CartContext);
```

### ব্যবহার:

```js
const { user, setUser } = useAuth();
const { theme, setTheme } = useTheme();
```

❌ **Drawbacks:**

* Component এ একাধিক hook call করতে হবে
* Nested providers structure same থাকলেও code verbose হয়ে যায়
* বড় project এ manage করা কঠিন

---

### ✅ Conclusion

* **Small to Medium project:** একটাই hook (useAppContext) **best practice**
* **Large project with huge state & performance optimization:** দরকার হলে **separate hooks** ব্যবহার করা যায়, কিন্তু একটাই hook দিয়ে clean & readable structure বানানো সবচেয়ে সহজ

---

যদি চাও আমি তোমার আগের **nested provider example + main.jsx** কে **single custom hook version** দিয়ে **ready-to-use project skeleton** বানিয়ে দেখাই।
এতে তুমি copy-paste করলেই কাজ করবে।

চাও আমি সেটা বানাই?
React এ **multiple contexts** নিয়ে **custom hook** design করার সময়, context size এবং project structure এর উপর নির্ভর করে “which is better” নির্ধারণ করা হয়। আমি সহজ করে তুলনা করি:

---

## **Option 1 — Single Custom Hook (useAppContext)** ✅

**Example:**

```js
export const useAppContext = () => {
  const auth = useContext(AuthContext);
  const theme = useContext(ThemeContext);
  const notification = useContext(NotificationContext);
  const cart = useContext(CartContext);

  return { ...auth, ...theme, ...notification, ...cart };
};
```

### Pros

1. **Clean & Simple** – Component এ একবার call করলে সব context access হয়।
2. **Reusable** – নতুন context add করলে শুধু hook update করতে হবে।
3. **Readability** – Component code clutter-free থাকে।
4. **Best for small-medium projects** – যেটাতে state change frequent না।

### Cons

* **Minor re-render issue**: যদি এক state change হয়, সব component re-render হতে পারে যেগুলো hook use করছে।

---

## **Option 2 — Separate Hook for Each Context** ❌

**Example:**

```js
export const useAuth = () => useContext(AuthContext);
export const useTheme = () => useContext(ThemeContext);
export const useNotification = () => useContext(NotificationContext);
export const useCart = () => useContext(CartContext);
```

### Pros

1. **Re-render optimization** – শুধু যেই state change হয়েছে, সেটার hook ব্যবহার করা component re-render হবে।
2. **Better control** – Large projects এ performance sensitive হলে useful।

### Cons

* Component এ একাধিক hook call করতে হয় → verbose
* Small-medium project এ unnecessary complexity

---

## **✅ Recommendation**

* **Small / Medium projects** → **Single custom hook (`useAppContext`)** ✅
* **Large / Enterprise projects** যেখানে performance & fine-grained re-render control দরকার → **Separate hooks per context**

---

💡 **Rule of Thumb:**

> যদি তুমি **readability + simplicity** চাও → single hook।
> যদি তুমি **performance optimization & huge state tree** চাও → separate hooks।

---

যদি চাও, আমি তোমার **nested provider + single custom hook** setup কে একদম **ready-to-use skeleton** বানিয়ে দিতে পারি, যাতে তুমি copy-paste করলেই project কাজ করবে।

চাও আমি সেটা বানাই?
না 😅, সবসময় **nested provider** থাকা আবশ্যক নয়। সেটা নির্ভর করে **context design & project structure** এর উপর।

চল স্পষ্ট করে বুঝাই:

---

## **1️⃣ Nested Provider Approach** ✅

**যেখানে প্রয়োজন: প্রতিটা context আলাদা provider।**

```js
<AuthContext.Provider value={{ user, setUser }}>
  <ThemeContext.Provider value={{ theme, setTheme }}>
    <NotificationContext.Provider value={{ notification, setNotification }}>
      <CartContext.Provider value={{ cart, setCart }}>
        {children}
      </CartContext.Provider>
    </NotificationContext.Provider>
  </ThemeContext.Provider>
</AuthContext.Provider>
```

* Advantage: **state separation**
* Component যেকোনো context use করতে পারে
* Re-render control করা সহজ

---

## **2️⃣ Single Combined Provider Approach** ✅

**যেখানে সব state এক context object এ merge করা হয়।**

```js
<AppContext.Provider value={{ user, setUser, theme, setTheme, notification, setNotification, cart, setCart }}>
  {children}
</AppContext.Provider>
```

* Advantage: **simpler structure**

* Component এ একবার hook call → সব state access

* Small/medium project এ best practice

* Caveat: **state change হলে সব subscribers re-render হবে**

---

## **3️⃣ Recommendation**

| Project Size     | Provider Style                    |
| ---------------- | --------------------------------- |
| Small/Medium     | Single combined provider          |
| Large/Enterprise | Nested provider (state별 separate) |

💡 Tip:

* Nested provider বেশি হলে code verbose হয়, তাই **custom hook** ব্যবহার করে component এ cleaner access করো।
* যদি context সংখ্যা অনেক হয় → **nested provider + custom hook** combination ideal।

---

যদি চাও, আমি তোমার জন্য **6-7 context + nested provider + single custom hook** structure বানিয়ে দেখাতে পারি,
যেটা **production-ready skeleton** হবে।

চাও আমি সেটা বানাই?
ঠিক আছে, আমি **context API কখন use করা উচিত** এবং কখন না করা উচিত, step-by-step explain করি। এটা বোঝা খুব গুরুত্বপূর্ণ কারণ React এ **unnecessary context** use করলে performance degrade হতে পারে। 😎

---

## **1️⃣ Context API Use করার Ideal Case**

Context API use করা উচিত যখন:

### **a) Truly Global State**

* State যেটা **multiple, distant components** share করবে।
  **Example:**

  * Auth (user login/logout)
  * Theme (dark/light mode)
  * Language / i18n
  * Notification / Toast
  * Shopping Cart

> যদি state শুধুমাত্র parent → child বা sibling component এ লাগে, **context দরকার নেই**, useState বা props ব্যবহার করো।

---

### **b) Multiple Component Access**

* একই state অনেক component এ দরকার।
  **Example:**

  * Navbar, Sidebar, Dashboard সবখানে **user info** show করা।
  * Footer, Header, Modal সবখানে **theme info** use করা।

---

### **c) Avoid Prop Drilling**

* অনেক layer এর component hierarchy এ props pass করা কঠিন হলে।
  **Example:**

```text
<App>
  <Header>
    <Navbar>
      <Profile /> → needs user info
```

* Props drilling এ problem → Context solves it

---

### **d) State That Rarely Changes**

* Context ব্যবহার করার জন্য ideal state হলো **rarely changing global state**।
* Frequent changing state (like typing in input, animation frames) → Context use করলে **unnecessary re-renders** হবে।

---

## **2️⃣ Context API Avoid করা উচিত যখন**

* **Local component state** → শুধু parent-child scope।
* **High-frequency changing state** → typing, slider, live counter.
* **Performance sensitive UI** → frequent re-render impact কমাতে।
* **Small component tree** → props drilling সহজে manageable।

---

## **3️⃣ Quick Guidelines**

| Situation          | Use Context? | Notes                                                   |
| ------------------ | ------------ | ------------------------------------------------------- |
| User auth status   | ✅            | Needed in Navbar, Dashboard, Profile                    |
| Theme (dark/light) | ✅            | Needed in multiple components                           |
| Input typing state | ❌            | Keep local useState                                     |
| Modal open/close   | ✅            | If modal used in multiple layers                        |
| API fetched data   | ❌ / ✅        | If only one component → local state, multiple → context |

---

💡 **Rule of Thumb:**

* **“If many components need it and it’s global, use context”**
* **“If local or high-frequency changing, don’t use context”**

---

যদি চাও, আমি তোমার জন্য **একটি decision chart** বানিয়ে দিতে পারি, যেখানে তুমি সহজে দেখতে পারবে **কোন state context এ যাবে আর কোনটা local state**।

চাও আমি সেটা বানাই?
ঠিক আছে! আমি তোমার জন্য **Context Use Decision Chart** বানিয়ে দিলাম, যাতে তুমি সহজে বুঝতে পারো **কোন state context এ রাখবে আর কোনটা local state হবে।** 😎

---

# **React Context Decision Chart**

```
Start
  |
  |--> State is needed by multiple components across the app?
         |
        Yes
         |
  |--> Does the state change very frequently (typing, slider, animation)?
         |      
        No
         |
  |--> Is it truly global (auth, theme, language, cart, modal)?
         |
        Yes
         |
      ✅ Use Context API
         |
        End
         |
        No
         |
      ❌ Keep it Local (useState/useReducer)
         |
        End
         |
        Yes
         |
      ❌ Keep Local & pass props if needed
         |
        End
```

---

## **Quick Examples**

| State Type                             | Context? | Notes                                  |
| -------------------------------------- | -------- | -------------------------------------- |
| User login/auth                        | ✅        | Needed in Navbar, Dashboard, Profile   |
| Theme (dark/light)                     | ✅        | Needed in multiple components          |
| Language/i18n                          | ✅        | Multi-component access required        |
| Notification / Toast                   | ✅        | Global access & trigger                |
| Shopping Cart                          | ✅        | Many components need it                |
| Input typing state                     | ❌        | Keep local state in input component    |
| Modal open/close (single modal)        | ❌        | Keep local unless shared across layers |
| API fetched data (single component)    | ❌        | Local state enough                     |
| API fetched data (multiple components) | ✅        | Use context to avoid multiple fetches  |

---

💡 **Summary Tips:**

1. Context API = **global, rarely changing state**
2. Local state = **component-specific, frequent-changing state**
3. Avoid “just for convenience” context → unnecessary re-renders
4. Large apps → combine **context + useReducer + custom hooks** for better performance

---

যদি চাও, আমি এখন তোমার জন্য **real project example** বানিয়ে দেখাই যেখানে:

* Auth, Theme, Notification, Cart সব **context use করা হবে**
* Input typing, modal local state → context ব্যবহার করা হবে না
* Custom hook + nested provider structure থাকবে
* Copy-paste ready

চাও আমি সেটা বানাই?


