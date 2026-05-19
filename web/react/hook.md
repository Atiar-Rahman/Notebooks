
### **1. What is `useState`?**

`useState` is a **Hook** in React that lets you add **state** to functional components. Before Hooks, only class components could have state. Now, functional components can manage state easily.

---

### **2. Syntax**

```javascript
const [state, setState] = useState(initialState);
```

- **`state`** → The current value of the state.
    
- **`setState`** → A function to update the state.
    
- **`initialState`** → The starting value of the state. It can be any type: number, string, boolean, object, array, etc.
    

---

### **3. Example with a Counter**

```javascript
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // initial state is 0

  const increment = () => {
    setCount(count + 1); // update state
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

**Explanation:**

- `count` holds the current count.
    
- `setCount` updates the count when the button is clicked.
    
- React automatically re-renders the component when state changes.
    

---

### **4. Lazy Initialization**

If the initial state is expensive to calculate, you can pass a function to `useState`:

```javascript
const [value, setValue] = useState(() => expensiveComputation());
```

- The function runs **only once** during the initial render.
    

---

### **5. Updating State**

You can update state in two ways:

1. **Directly (primitive types):**
    

```javascript
setCount(count + 1);
```

2. **Using a function (safer when depending on previous state):**
    

```javascript
setCount(prevCount => prevCount + 1);
```

- This is recommended when the new state depends on the previous state.
    

---

### **6. State Can Be Any Type**

- **String**
    

```javascript
const [name, setName] = useState("John");
```

- **Array**
    

```javascript
const [items, setItems] = useState([]);
```

- **Object**
    

```javascript
const [user, setUser] = useState({ name: "Alice", age: 25 });
```

- **Boolean**
    

```javascript
const [isLoggedIn, setIsLoggedIn] = useState(false);
```

> **Important:** When updating objects or arrays, always spread the previous state to avoid overwriting:

```javascript
setUser(prevUser => ({ ...prevUser, age: 26 }));
```

---

### **7. Rules of `useState`**

1. Only call Hooks **at the top level** (not inside loops or conditions).
    
2. Only call Hooks **from React functions** (components or custom hooks).
    
3. Keep the state logic simple and predictable.
    

---

### **8. Multiple State Variables**

You can use multiple `useState` calls for independent state values:

```javascript
const [count, setCount] = useState(0);
const [name, setName] = useState("Alice");
```

> React keeps them separate internally.

---

### ✅ **Key Takeaways**

- `useState` adds state to functional components.
    
- Returns `[state, setState]`.
    
- State updates trigger **re-renders**.
    
- Use functional updates when new state depends on old state.
    
- Works with **any data type**.
    

---

# **useEffect in React** 🔹

`useEffect` হলো **React hook** যা **component-এর side effects handle করতে** ব্যবহার হয়।

> Side effects = এমন কাজ যা **UI render-এর বাইরে ঘটে**, যেমন: API call, DOM manipulation, event listeners, timers ইত্যাদি।

---

## 1️⃣ Basic Syntax

```jsx
import { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("useEffect called! Count is: ", count);
  });

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

- **Effect callback** first argument
    
- **dependency array** second argument (optional)
    

✅ এখানে `useEffect` **component render হওয়ার পরে** call হয়

---

## 2️⃣ Dependency Array

```jsx
useEffect(() => {
  console.log("Count changed:", count);
}, [count]); // <-- dependency array
```

- `[count]` → শুধু তখনই run হবে যখন `count` change হয়
    
- `[]` → component **mount-only** effect (একবার মাত্র run)
    
- যদি dependency না দাও → **every render** এ run হবে
    

---

## 3️⃣ Cleanup Function

কিছু effect-এ cleanup দরকার, যেমন event listener বা timer:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Tick");
  }, 1000);

  return () => {
    clearInterval(timer); // cleanup on unmount
  };
}, []);
```

- Cleanup function return করা হয় callback থেকে
    
- Component unmount হলে cleanup run হয়
    

---

## 4️⃣ Common Use Cases

1. **Fetching API data**
    
2. **Subscribing to events** (scroll, resize)
    
3. **Setting timers / intervals**
    
4. **Updating document title / DOM outside React**
    

---

💡 **Tip:**

- **State update inside useEffect → watch dependencies carefully**, না হলে **infinite loop** হতে পারে
    
- UseEffect is **asynchronous** in effect, কিন্তু synchronous in render (run after render)
    

---

## **1. What is `useEffect`?**

`useEffect` is a **Hook** that lets you perform **side effects** in functional components.

- **Side effects** are anything that affects something outside the component, such as:
    
    - Fetching data from an API
        
    - Subscribing to events
        
    - Updating the DOM manually
        
    - Setting up timers
        

Before hooks, side effects were mostly handled in class component lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

---

## **2. Syntax**

```javascript
useEffect(() => {
  // code to run as side effect
  return () => {
    // optional cleanup code
  };
}, [dependencies]);
```

- **Effect function** → The code you want to run as a side effect.
    
- **Cleanup function** → Optional function to clean up (e.g., remove event listeners, clear timers).
    
- **Dependencies array** → Determines **when the effect runs**.
    

---

## **3. Example 1: Basic useEffect**

```javascript
import React, { useState, useEffect } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    }, 1000);

    return () => clearInterval(interval); // cleanup
  }, []); // empty array means this runs once on mount

  return <h1>Seconds: {seconds}</h1>;
}

export default Timer;
```

**Explanation:**

- Effect runs **once** when the component mounts (because of `[]` dependency array).
    
- Cleanup function runs when the component unmounts, stopping the timer.
    

---

## **4. Dependency Array Explained**

The **dependencies array** controls **when your effect runs**:

| Dependency Array | Behavior                                                         |
| ---------------- | ---------------------------------------------------------------- |
| `[]`             | Runs **once** after first render (componentDidMount).            |
| `[var1, var2]`   | Runs **after initial render and whenever var1 or var2 changes**. |
| _(omitted)_      | Runs **after every render** (not usually recommended).           |
|                  |                                                                  |

---

## **5. Example 2: Fetching Data**

```javascript
import React, { useState, useEffect } from "react";

function UsersList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []); // only fetch once on mount

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}

export default UsersList;
```

---

## **6. Cleanup in useEffect**

Some effects require **cleanup** to prevent memory leaks or unwanted behavior:

- Timers
    
- Event listeners
    
- Subscriptions
    

```javascript
useEffect(() => {
  const handleResize = () => console.log(window.innerWidth);
  window.addEventListener("resize", handleResize);

  return () => window.removeEventListener("resize", handleResize);
}, []);
```

- The **cleanup function** runs before the next effect (if dependencies changed) and on unmount.
    

---

## **7. Common Patterns**

### **Effect only on mount**

```javascript
useEffect(() => {
  console.log("Component mounted");
}, []);
```

### **Effect on state change**

```javascript
useEffect(() => {
  console.log("Count changed:", count);
}, [count]);
```

### **Effect on every render (rare)**

```javascript
useEffect(() => {
  console.log("Rendered");
}); // no dependency array
```

---

## ✅ **Key Takeaways**

- `useEffect` handles **side effects** in functional components.
    
- Dependencies array controls **when the effect runs**.
    
- Cleanup function prevents **memory leaks**.
    
- Replaces multiple lifecycle methods from class components.
    

---

## **1. What is `useRef`?**

`useRef` is a React hook that lets you **persist a value across renders** without causing a re-render when it changes. It can also be used to **access DOM elements directly**.

Think of it as a “box” that holds a value:

```jsx
const myRef = useRef(initialValue);
```

- `myRef.current` contains the value.
    
- Changing `myRef.current` **does not trigger a re-render**.
    

---

## **2. Basic Syntax**

```jsx
import React, { useRef } from "react";

function MyComponent() {
  const myRef = useRef(null);

  return <div ref={myRef}>Hello!</div>;
}
```

Here, `myRef` is now **pointing to the DOM element `<div>`**. You can access it later using `myRef.current`.

---

## **3. Common Use Cases**

### **A. Accessing DOM elements**

```jsx
import React, { useRef } from "react";

function FocusInput() {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus(); // Focus the input element
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}
```

✅ When the button is clicked, the input is focused. `useRef` lets you **directly manipulate the DOM**.

---

### **B. Persisting values across renders (without re-rendering)**

```jsx
import React, { useRef, useState, useEffect } from "react";

function Timer() {
  const [count, setCount] = useState(0);
  const timerId = useRef(null);

  useEffect(() => {
    timerId.current = setInterval(() => {
      setCount(prev => prev + 1);
    }, 1000);

    return () => clearInterval(timerId.current); // cleanup
  }, []);

  return <h1>{count}</h1>;
}
```

Here, `timerId` is **stored across renders** without triggering a re-render when updated.

---

### **C. Tracking previous state**

```jsx
import React, { useState, useEffect, useRef } from "react";

function PreviousValue() {
  const [count, setCount] = useState(0);
  const prevCount = useRef(0);

  useEffect(() => {
    prevCount.current = count;
  }, [count]);

  return (
    <div>
      <p>Current: {count}</p>
      <p>Previous: {prevCount.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

This is a neat trick to **remember the previous state** without triggering a re-render.

---

## **4. Key Points to Remember**

1. Changing `ref.current` does **not** trigger a re-render.
    
2. `useRef` is perfect for:
    
    - Accessing DOM nodes.
        
    - Storing mutable values between renders.
        
    - Tracking previous state.
        
3. Avoid overusing it for state—if you need a change to update the UI, use `useState` instead.
    

---

#  **React `useContext`** টা সহজ করে, exam-friendly example সহ বুঝি।

---

## 🔹 useContext কী?

`useContext` হলো **React Hook**, যেটা দিয়ে
👉 **props drilling ছাড়া** (মানে parent → child → grandchild বারবার props পাঠানো ছাড়াই)
👉 **direct data share** করা যায়।

---

## 🔹 Problem (props drilling)

ধরো,

```
App → Dashboard → Profile → UserName
```

`UserName` এ user data দরকার, কিন্তু data আছে `App` এ।
তাই সব জায়গায় props পাঠাতে হয় 😵

➡️ **Solution = Context API + useContext**

---

## 🔹 Step-by-Step Example

### 🎯 Goal:

একটা **User Context** বানাবো
যেখান থেকে যেকোনো component user name নিতে পারবে।

---

## 1️⃣ Create Context

```jsx
// UserContext.js
import { createContext } from "react";

const UserContext = createContext();

export default UserContext;
```

---

## 2️⃣ Provide Context (Parent component)

```jsx
// App.js
import UserContext from "./UserContext";
import Profile from "./Profile";

function App() {
  const user = {
    name: "Atiar",
    role: "Student"
  };

  return (
    <UserContext.Provider value={user}>
      <Profile />
    </UserContext.Provider>
  );
}

export default App;
```

📌 `value` এর ভেতরে যেটা দিবা → সেটাই সব child পাবে

---

## 3️⃣ Consume Context using useContext

```jsx
// Profile.js
import { useContext } from "react";
import UserContext from "./UserContext";

function Profile() {
  const user = useContext(UserContext);

  return (
    <div>
      <h2>Name: {user.name}</h2>
      <p>Role: {user.role}</p>
    </div>
  );
}

export default Profile;
```

🎉 **Done!**
কোনো props পাঠানো লাগে নাই।

---

## 🔹 Short Syntax (Most Used in Exam)

```jsx
const value = useContext(MyContext);
```

---

## 🔹 When to use useContext?

✔ Theme (dark / light)
✔ Logged-in user info
✔ Language (EN / BN)
✔ Global settings

❌ Huge data / frequent updates হলে → Redux / Zustand ভালো

---

## 🔹 Exam Tip 📝

> **useContext allows sharing data globally in a React app without passing props manually at every level.**

---

## ✅ You CAN create unlimited contexts

```jsx
UserContext
ThemeContext
AuthContext
LanguageContext
CartContext
```

React এতে কোনো restriction দেয় না।

---

## ⚠️ BUT — সব কিছুর জন্য আলাদা Context বানানো ভালো না

### ❌ Bad Practice

```jsx
NameContext
AgeContext
EmailContext
PhoneContext
```

এতে code messy হয়ে যায় 😵

---

## ✅ Best Practice (Logical grouping)

### 🎯 Example

```jsx
AuthContext → user, token, isLoggedIn
ThemeContext → theme, setTheme
SettingsContext → language, fontSize
```

---

## 🔹 Multiple Context Use Example

### 1️⃣ Contexts

```jsx
// AuthContext.js
export const AuthContext = createContext()

// ThemeContext.js
export const ThemeContext = createContext()
```

---

### 2️⃣ Providers (App.js)

```jsx
<AuthContext.Provider value={{ user: "Atiar" }}>
  <ThemeContext.Provider value={{ theme: "dark" }}>
    <Home />
  </ThemeContext.Provider>
</AuthContext.Provider>
```

✔️ একসাথে multiple context কাজ করবে

---

### 3️⃣ Consume in component

```jsx
const { user } = useContext(AuthContext)
const { theme } = useContext(ThemeContext)
```

---

## 🔥 Pro Tip (Real Project)

যদি দেখো:

* অনেক Context
* Deep nesting
* Frequent updates

👉 তখন **Redux / Zustand / Recoil** ভালো choice

---

## 📝 Exam Answer (Short)

> **There is no limit to how many contexts you can create in React, but contexts should be created based on logical grouping of shared state.**

---

Short answer: **যত খুশি ততগুলো object / value দিতে পারো** 😄
React কোনো limit দেয় না।

কিন্তু **কীভাবে দিবা**—এটাই আসল বিষয়।

---

## ✅ value-এর ভেতরে কতগুলো object দিতে পারো?

### ✔️ একটার বেশি হলে → **একটা object এর ভেতরে সব রাখবে**

```jsx
<UserContext.Provider
  value={{
    name: "atiar",
    bg: "CSE",
    age: 22,
    isLoggedIn: true
  }}
>
  <Home />
</UserContext.Provider>
```

👉 এখানে **৪টা value একসাথে পাঠানো হয়েছে**

---

## ❌ ভুল পদ্ধতি (Allowed না)

```jsx
<UserContext.Provider value={name, bg}>
```

🚫 React এটা নেয় না
`value` **একটাই জিনিস নেয়**

---

## ✅ Real-life pattern (state + function)

```jsx
const [user, setUser] = useState(null)

<UserContext.Provider
  value={{
    user,
    setUser,
    isLoggedIn: !!user
  }}
>
```

👉 **data + function দুটোই পাঠানো যায়**

---

## 🔹 useContext দিয়ে কীভাবে নেবে?

```jsx
const { user, setUser, isLoggedIn } = useContext(UserContext)
```

---

## 🔥 Advanced: Nested object

```jsx
value={{
  user: {
    name: "atiar",
    bg: "CSE"
  },
  settings: {
    theme: "dark",
    lang: "bn"
  }
}}
```

---

## ⚠️ Performance Tip (Important)

যদি `value` বারবার change হয় →
👉 সব consumer re-render হবে

### ✅ Solution

* Context split করো
* `useMemo` ব্যবহার করো

```jsx
const value = useMemo(() => ({
  user,
  setUser
}), [user])
```

---

## 📝 Exam-ready line

> **The value prop of Context.Provider can accept a single value, which is usually an object containing multiple properties.**

---


# 🎯 Example Goal

আমরা বানাবো:

1. **AuthContext** → user login info
2. **ThemeContext** → dark / light theme
3. **Home component** → দুইটা context একসাথে ব্যবহার করবে

---

## 📁 Folder Structure

```
src/
 ├─ context/
 │   ├─ AuthContext.js
 │   └─ ThemeContext.js
 ├─ Home.jsx
 └─ App.jsx
```

---

## 1️⃣ AuthContext.js

```jsx
import { createContext, useState } from "react"

const AuthContext = createContext(null)

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null)

  const login = () => {
    setUser({ name: "Atiar", bg: "CSE" })
  }

  const logout = () => {
    setUser(null)
  }

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  )
}

export default AuthContext
```

---

## 2️⃣ ThemeContext.js

```jsx
import { createContext, useState } from "react"

const ThemeContext = createContext("light")

export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light")

  const toggleTheme = () => {
    setTheme(prev => (prev === "light" ? "dark" : "light"))
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  )
}

export default ThemeContext
```

---

## 3️⃣ App.jsx (Multiple Providers)

```jsx
import Home from "./Home"
import { AuthProvider } from "./context/AuthContext"
import { ThemeProvider } from "./context/ThemeContext"

function App() {
  return (
    <AuthProvider>
      <ThemeProvider>
        <Home />
      </ThemeProvider>
    </AuthProvider>
  )
}

export default App
```

📌 **এখানেই multiple context একসাথে wrap করা হয়েছে**

---

## 4️⃣ Home.jsx (Using multiple useContext)

```jsx
import { useContext } from "react"
import AuthContext from "./context/AuthContext"
import ThemeContext from "./context/ThemeContext"

function Home() {
  const { user, login, logout } = useContext(AuthContext)
  const { theme, toggleTheme } = useContext(ThemeContext)

  return (
    <div style={{
      background: theme === "dark" ? "#222" : "#eee",
      color: theme === "dark" ? "white" : "black",
      padding: "20px"
    }}>
      <h1>Theme: {theme}</h1>
      <button onClick={toggleTheme}>Toggle Theme</button>

      <hr />

      {user ? (
        <>
          <h2>Welcome, {user.name}</h2>
          <p>Background: {user.bg}</p>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  )
}

export default Home
```

---

## ✅ What you learned here

✔️ Multiple context create
✔️ Multiple Provider wrap
✔️ Multiple `useContext` in one component
✔️ Data + function pass
✔️ Real project structure

---

## 📝 Exam-ready short answer

> **Multiple contexts can be used in a React application by wrapping components with multiple Context Providers and consuming them using useContext hook.**

---

## 🔥 Pro Tip

Real projects এ cleaner করার জন্য:

* `useAuth()`
* `useTheme()`
  custom hook বানানো হয়

------------

# 🔹 Custom Hook কী?

👉 **Custom Hook = নিজের বানানো Hook**
👉 যেটার নাম **`use` দিয়ে শুরু হবে**
👉 React এর built-in hooks (`useState`, `useContext`, `useEffect`) ব্যবহার করতে পারবে

📌 Goal: **logic reuse + clean code**

---

## 🔹 Basic Rule

✔ নাম `use` দিয়ে শুরু → `useAuth`, `useTheme`
✔ Normal function
✔ Hooks এর ভিতরে hooks ব্যবহার করা যায়

---

# 🟢 Example 1: Simple Custom Hook (Counter)

### 📁 useCounter.js

```jsx
import { useState } from "react"

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue)

  const increment = () => setCount(count + 1)
  const decrement = () => setCount(count - 1)

  return { count, increment, decrement }
}

export default useCounter
```

### 📁 Use it

```jsx
const { count, increment, decrement } = useCounter(5)
```

---

# 🟢 Example 2: Custom Hook for Context (REAL PROJECT)

👉 আগের **AuthContext** clean করবো

---

## 1️⃣ useAuth.js (Custom Hook)

```jsx
import { useContext } from "react"
import AuthContext from "../context/AuthContext"

function useAuth() {
  const context = useContext(AuthContext)

  if (!context) {
    throw new Error("useAuth must be used inside AuthProvider")
  }

  return context
}

export default useAuth
```

---

## 2️⃣ useTheme.js

```jsx
import { useContext } from "react"
import ThemeContext from "../context/ThemeContext"

function useTheme() {
  return useContext(ThemeContext)
}

export default useTheme
```

---

## 3️⃣ Home.jsx (Much cleaner 🔥)

```jsx
import useAuth from "./hooks/useAuth"
import useTheme from "./hooks/useTheme"

function Home() {
  const { user, login, logout } = useAuth()
  const { theme, toggleTheme } = useTheme()

  return (
    <div>
      <h1>{theme}</h1>
      <button onClick={toggleTheme}>Toggle</button>

      {user ? (
        <>
          <h2>{user.name}</h2>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <button onClick={login}>Login</button>
      )}
    </div>
  )
}
```

---

## 🔥 Why Custom Hook is Powerful?

❌ Before:

```jsx
useContext(AuthContext)
useContext(ThemeContext)
```

✅ After:

```jsx
useAuth()
useTheme()
```

✔ Cleaner
✔ Reusable
✔ Easy to test
✔ Industry standard

---

## ⚠️ Common Mistakes

❌ Hook নাম `auth()`
❌ Condition এর ভিতরে hook
❌ Loop এর ভিতরে hook

---

## 📝 Exam One-liner

> **A custom hook is a JavaScript function that starts with "use" and allows reuse of stateful logic across components.**

---
Nice 👍 তুমি **useContext + custom hook** একসাথে ঠিকই ব্যবহার করছো।
কিন্তু তোমার code-এ **একটা common mistake** আছে। চলো সেটা ঠিক করি + explain করি।

---

## ❌ Problem in your code

```jsx
<button onClick={()=>increment(count+1)}>increment</button>
<button onClick={()=>decrement(count-1)}>decrement</button>
```

👉 এখানে তুমি `increment` / `decrement` এ **argument পাঠাচ্ছো**,
কিন্তু তোমার `useCounter` hook-এ এগুলো **argument নেয় না**।

---

## ✅ Correct useCounter (Expected)

ধরি তোমার `useCounter` এমন:

```jsx
// useCounter.js
import { useState } from "react"

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue)

  const increment = () => setCount(prev => prev + 1)
  const decrement = () => setCount(prev => prev - 1)

  return { count, increment, decrement }
}

export default useCounter
```

---

## ✅ Fixed Home.jsx (Correct Way)

```jsx
import { useContext } from "react"
import UserContext from "./context/UserContext"
import useCounter from "./hook/useCounter"

function Home() {
  const user = useContext(UserContext)
  const { count, increment, decrement } = useCounter(5)

  return (
    <div>
      <div>
        <h1>{count}</h1>
        <button onClick={increment}>Increment</button>
        <button onClick={decrement}>Decrement</button>
      </div>

      <h1>Name: {user.name}</h1>
      <h2>Background: {user.bg}</h2>
    </div>
  )
}

export default Home
```

---

## 🔍 Why this is correct?

* `count` already hook এর ভিতরে manage হচ্ছে
* Button click → function call → state update
* Extra argument পাঠানোর দরকার নাই

---

## 🧠 If তুমি argument-based increment চাও (Advanced)

```jsx
const increment = (value = 1) => setCount(prev => prev + value)
```

Then use:

```jsx
<button onClick={() => increment(5)}>+5</button>
```

---

## 📝 Exam Tip (Important)

> **Custom hooks encapsulate stateful logic and expose state and functions without requiring direct state manipulation from components.**

---

## ✅ Custom Hook আসলে কী?

👉 **Custom hook = JavaScript function**
👉 যার নাম **`use` দিয়ে শুরু হয়**
👉 React hooks (`useState`, `useContext`, etc.) ব্যবহার করে

```js
function useCounter() {
  ...
}
```

✔ এটা **normal function syntax**
✔ কিন্তু React এটাকে **hook হিসেবে treat করে**

---

## 🔍 তাহলে normal function থেকে পার্থক্য কী?

### ❌ Normal function

```js
function counter() {
  let count = 0
  count++
}
```

* React state জানে না
* Re-render হয় না

---

### ✅ Custom hook (special function)

```js
function useCounter() {
  const [count, setCount] = useState(0)
  return { count }
}
```

* React state manage করে
* Re-render trigger হয়
* Component lifecycle এর সাথে connected

---

## ⚠️ কেন `use` দিয়ে শুরু করা বাধ্যতামূলক?

React internally check করে:

```txt
function name starts with "use"
```

তাহলেই:

* Hook rules enforce করে
* Lint warning দেয়

---

## 🧠 Important Rule

Custom hook:

* ❌ JSX return করে না
* ❌ Component না
* ✔ logic + state return করে

---

## 📝 Exam one-liner

> **A custom hook is a JavaScript function that starts with "use" and allows reuse of React stateful logic.**

---

## 🔥 Simple analogy

* Component = 🏠 (UI বানায়)
* Custom Hook = 🧠 (logic বানায়)

---

# 🔥 Component vs Hook (React)

## 🧱 React Component

👉 **UI তৈরি করে**
👉 JSX return করে
👉 App-এর visual part

### Example (Component)

```jsx
function Home() {
  return <h1>Hello World</h1>
}
```

---

## 🧠 React Hook (Custom Hook)

👉 **Logic + state reuse করে**
👉 JSX return করে না
👉 UI থেকে logic আলাদা করে

### Example (Hook)

```jsx
function useCounter() {
  const [count, setCount] = useState(0)
  return { count }
}
```

---

## 📊 Comparison Table

| Feature         | Component        | Hook                  |
| --------------- | ---------------- | --------------------- |
| Purpose         | UI render        | Logic reuse           |
| Returns         | JSX              | Data / functions      |
| Name rule       | Any name         | Must start with `use` |
| Uses hooks      | ✅ Yes            | ✅ Yes                 |
| Can render HTML | ✅ Yes            | ❌ No                  |
| Reusable logic  | ❌ Limited        | ✅ Very reusable       |
| Lifecycle       | Visual lifecycle | Logic lifecycle       |
| Used as         | `<Home />`       | `useCounter()`        |

---

## 🔁 How they work together

```jsx
function Home() {
  const { count, increment } = useCounter()

  return (
    <>
      <h1>{count}</h1>
      <button onClick={increment}>+</button>
    </>
  )
}
```

✔ Component = UI
✔ Hook = logic

---

## ⚠️ Common Mistakes

### ❌ Hook দিয়ে JSX return করা

```jsx
function useCounter() {
  return <h1>Wrong</h1>
}
```

🚫 Hook কখনো JSX return করে না

---

### ❌ Component নাম `useHome`

```jsx
function useHome() {
  return <div>UI</div>
}
```

🚫 এটা hook-এর naming rule ভাঙে

---

## 📝 Exam One-liners

**Component:**

> A React component is a function that returns JSX to render UI.

**Hook:**

> A React hook is a function that allows using React features like state and context without writing a class.

**Custom Hook:**

> A custom hook is a reusable function that encapsulates stateful logic and does not return JSX.

---

## 🧠 Easy Memory Trick

* **Component = UI**
* **Hook = Brain**
* **Context = Global data**

---

Good question 👍
**Basic level React শিখতে গেলে এই hook গুলো জানা থাকলেই তুমি solid হয়ে যাবে।**
আমি priority অনুযায়ী সাজিয়ে দিচ্ছি 👇

---

# ✅ Basic React Hooks (Must Know)

## 1️⃣ `useState` ⭐⭐⭐⭐⭐

👉 **State manage করার জন্য**

```jsx
const [count, setCount] = useState(0)
```

✔ counter
✔ form input
✔ toggle

---

## 2️⃣ `useEffect` ⭐⭐⭐⭐⭐

👉 **Side effects handle করার জন্য**

```jsx
useEffect(() => {
  console.log("component mounted")
}, [])
```

✔ API call
✔ event listener
✔ lifecycle logic

---

## 3️⃣ `useContext` ⭐⭐⭐⭐

👉 **Global data share করার জন্য**

```jsx
const value = useContext(MyContext)
```

✔ theme
✔ auth
✔ settings

---

## 4️⃣ `useRef` ⭐⭐⭐⭐

👉 **DOM access + value persist করার জন্য**

```jsx
const inputRef = useRef(null)
inputRef.current.focus()
```

✔ focus input
✔ previous value
✔ interval store

---

## 5️⃣ `useMemo` ⭐⭐⭐

👉 **Heavy calculation optimize করার জন্য**

```jsx
const result = useMemo(() => slowFunc(num), [num])
```

✔ performance boost

---

## 6️⃣ `useCallback` ⭐⭐⭐

👉 **Function memoization**

```jsx
const handleClick = useCallback(() => {
  setCount(c => c + 1)
}, [])
```

✔ prevent unnecessary re-render

---

## 7️⃣ `useReducer` ⭐⭐⭐

👉 **Complex state manage করার জন্য**

```jsx
const [state, dispatch] = useReducer(reducer, initialState)
```

✔ form
✔ cart
✔ auth logic

---

## 🧠 Absolute Beginner Priority (Roadmap)

### 🔰 First learn

1. `useState`
2. `useEffect`

### 🔰 Then

3. `useContext`
4. `useRef`

### 🔰 After that

5. `useReducer`
6. `useMemo`
7. `useCallback`

---

## 📝 Exam / Interview Tip

> If you know **useState, useEffect, useContext, useRef**, you are considered React-ready at a basic level.

---

## 🔥 Bonus (Optional but powerful)

* Custom Hook
* Context + Reducer combo

---

চাও তো আমি

* **one-by-one mini example**
* **MCQ practice**
* **real project roadmap**

যেটা চাও বলো 😄
Perfect 😄 চল একদম **useCallback** step-by-step বুঝি, plus exam-friendly example।

---

# 🔹 What is `useCallback`?

`useCallback` হলো **React Hook** যা **একটি function কে memoize করে রাখে**, মানে React **পরের re-render এ পুরনো function reuse করে**, নতুন function recreate করে না।

**Main purpose:**
✅ Prevent unnecessary re-renders in child components
✅ Optimize performance

---

## 🔹 Syntax

```jsx
const memoizedCallback = useCallback(
  () => {
    // function body
  },
  [dependencies] // only recreate function if these change
)
```

* `dependencies` → function তখনই update হবে যখন dependency change হবে
* `[]` → function কখনো recreate হবে না

---

## 🔹 Why `useCallback`?

React প্রতিবার parent re-render হলে, **সব function নতুন হয়ে যায়।**

* যদি child component সেই function receive করে → child আবার re-render হবে
* এটা prevent করার জন্য `useCallback` use করা হয়

---

## 🔹 Example: Counter + Child Component

### App.jsx

```jsx
import React, { useState, useCallback } from "react";
import Child from "./Child";

function App() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // Function without useCallback
  // const increment = () => setCount(count + 1);

  // Function with useCallback
  const increment = useCallback(() => {
    setCount(prev => prev + 1);
  }, []); // [] means never recreate

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={increment}>Increment</button>

      <input
        type="text"
        placeholder="Type something..."
        value={text}
        onChange={(e) => setText(e.target.value)}
      />

      <Child increment={increment} />
    </div>
  );
}

export default App;
```

---

### Child.jsx

```jsx
import React from "react";

function Child({ increment }) {
  console.log("Child rendered");
  return (
    <div>
      <button onClick={increment}>Increment from Child</button>
    </div>
  );
}

export default React.memo(Child);
```

---

## 🔹 What happens here

1. `React.memo(Child)` → child only re-render if **props change**
2. Without `useCallback` → parent re-render → function recreated → child re-render
3. With `useCallback` → function stays same → child **does not re-render unnecessarily**

Console log দেখলে বোঝা যাবে: **Child rendered** শুধু তখনই হয় যখন function or props change হয়।

---

## 🔹 When to use `useCallback`?

* Passing function to **memoized child components**
* Expensive functions that shouldn’t be recreated
* Event handlers in large lists

---

## 🔹 Quick Exam Notes

* `useCallback(fn, deps)` → returns **memoized function**
* Prevents **unnecessary re-renders**
* Often used with `React.memo`

---

💡 **Memory Trick:**

> `useMemo` → memoize **value**
> `useCallback` → memoize **function**

---

If you want, I can make a **tiny live counter project** using:

* `useState` + `useEffect` + `useCallback` + `useMemo`

It’s super clear for exam + real project.

Do you want me to make that?
