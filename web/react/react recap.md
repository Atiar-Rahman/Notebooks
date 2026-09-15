
# 🚀 Complete React Tutorial: Beginner → Advanced

## React শেখার পুরো Roadmap

```text
1. React কী?
2. React কেন ব্যবহার করি?
3. Project Setup
4. JSX
5. Components
6. Props
7. State
8. Events
9. Conditional Rendering
10. Lists & Keys
11. Forms
12. useState
13. useEffect
14. useRef
15. useMemo
16. useCallback
17. React.memo
18. Component Communication
19. Lifting State Up
20. Context API
21. useReducer
22. Custom Hooks
23. API Fetching
24. Loading / Error Handling
25. CRUD
26. React Router
27. Authentication
28. Protected Routes
29. LocalStorage
30. Performance Optimization
31. Error Boundaries
32. React Query / TanStack Query
33. State Management
34. TypeScript + React
35. Testing
36. Security Basics
37. Project Architecture
38. Advanced Patterns
39. Production Project
40. Interview Preparation
```

---

# PART 1 — React কী?

React হলো একটি **JavaScript library**, যেটা মূলত user interface তৈরি করার জন্য ব্যবহার করা হয়।

React তৈরি করেছে Meta।

ধরো তুমি একটা e-commerce website বানাচ্ছো:

```text
Navbar
 ↓
Products
 ↓
Product Card
 ↓
Cart
 ↓
Checkout
```

সাধারণ HTML-এ পুরো UI এক জায়গায় লিখলে project বড় হওয়ার সাথে সাথে maintain করা কঠিন হয়।

React UI-কে ছোট ছোট **component**-এ ভাগ করে।

```text
App
├── Navbar
├── Sidebar
├── ProductList
│   ├── ProductCard
│   ├── ProductCard
│   └── ProductCard
└── Footer
```

---

# PART 2 — React কেন ব্যবহার করি?

React-এর সবচেয়ে গুরুত্বপূর্ণ ধারণা:

### Component-based UI

একটা বড় website:

```text
Website
```

কে ভেঙে:

```text
Navbar
Hero
Card
Button
Footer
```

এভাবে component বানানো যায়।

তারপর একই component বারবার ব্যবহার করা যায়।

উদাহরণ:

```jsx
function Button() {
  return <button>Click Me</button>;
}
```

তারপর:

```jsx
function App() {
  return (
    <div>
      <Button />
      <Button />
      <Button />
    </div>
  );
}
```

একটা `Button` component তিনবার ব্যবহার হলো।

---

# PART 3 — React Project তৈরি

বর্তমানে React শেখার জন্য Vite দিয়ে শুরু করা সহজ।

```bash
npm create vite@latest my-react-app
```

তারপর:

```bash
cd my-react-app
npm install
npm run dev
```

React + JavaScript select করবে।

Project structure:

```text
my-react-app
│
├── src
│   ├── App.jsx
│   ├── main.jsx
│   └── ...
│
├── public
├── package.json
└── index.html
```

---

# PART 4 — JSX

React-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়গুলোর একটি হলো **JSX**।

JSX দেখতে HTML-এর মতো হলেও এটা HTML নয়।

```jsx
function App() {
  return <h1>Hello React</h1>;
}
```

এখানে:

```jsx
<h1>Hello React</h1>
```

হলো JSX।

---

## JavaScript ব্যবহার করা যায়

JSX-এর ভিতরে `{}` ব্যবহার করে JavaScript expression লিখতে পারো।

```jsx
function App() {
  const name = "Atiar";

  return <h1>Hello {name}</h1>;
}
```

Output:

```text
Hello Atiar
```

আরেকটা:

```jsx
function App() {
  const age = 25;

  return <p>Your age is {age}</p>;
}
```

---

# ⚠️ Beginner Mistake #1

অনেকে লেখে:

```jsx
<h1>Hello {name}</h1>
```

কিন্তু `name` define করে না।

```jsx
function App() {
  return <h1>Hello {name}</h1>;
}
```

এতে error হবে।

সঠিক:

```jsx
function App() {
  const name = "Atiar";

  return <h1>Hello {name}</h1>;
}
```

---

# PART 5 — JSX-এ class

HTML:

```html
<div class="container">
```

React JSX:

```jsx
<div className="container">
```

### ভুল:

```jsx
<div class="container">
```

### সঠিক:

```jsx
<div className="container">
```

কারণ JSX-এ `class` নয়, `className` ব্যবহার করা হয়।

---

# PART 6 — Component

React-এর সবচেয়ে important concept:

> **Component হলো UI-এর reusable অংশ।**

উদাহরণ:

```jsx
function Welcome() {
  return <h1>Welcome to React</h1>;
}
```

তারপর:

```jsx
function App() {
  return (
    <div>
      <Welcome />
    </div>
  );
}
```

---

# Component naming

Component-এর নাম সাধারণত **Capital letter** দিয়ে শুরু করতে হয়।

সঠিক:

```jsx
function Navbar() {
  return <nav>Navbar</nav>;
}
```

ভুল:

```jsx
function navbar() {
  return <nav>Navbar</nav>;
}
```

React component naming convention:

```text
Navbar
ProductCard
UserProfile
LoginForm
Footer
```

---

# PART 7 — Props

এখন ধরো ProductCard component আছে।

```jsx
function ProductCard() {
  return (
    <div>
      <h2>iPhone</h2>
      <p>$999</p>
    </div>
  );
}
```

কিন্তু আমরা চাই component-কে different product data দিতে।

এখানে আসে **Props**।

```jsx
function ProductCard({ name, price }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>${price}</p>
    </div>
  );
}
```

তারপর:

```jsx
function App() {
  return (
    <div>
      <ProductCard name="iPhone" price={999} />
      <ProductCard name="Samsung" price={799} />
      <ProductCard name="Pixel" price={699} />
    </div>
  );
}
```

Output:

```text
iPhone
$999

Samsung
$799

Pixel
$699
```

একটা component → multiple data.

---

# Props-এর সহজ ধারণা

```text
Parent
   |
   | props
   ↓
Child
```

উদাহরণ:

```jsx
<ProductCard
  name="iPhone"
  price={999}
/>
```

এখানে:

```text
name
price
```

হলো props।

---

# ⚠️ Beginner Mistake #2 — Props পরিবর্তন করা

Props সাধারণত child component-এর ভিতর থেকে পরিবর্তন করা উচিত নয়।

যেমন:

```jsx
function Product({ name }) {
  name = "Samsung"; // ❌
}
```

Props-কে read-only হিসেবে ভাবো।

---

# PART 8 — Event Handling

React-এ event:

```jsx
function App() {
  function handleClick() {
    console.log("Button clicked");
  }

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}
```

### Beginner mistake

অনেকে করে:

```jsx
<button onClick={handleClick()}>
```

এটা ভুল।

সঠিক:

```jsx
<button onClick={handleClick}>
```

কারণ:

```jsx
handleClick
```

মানে React-কে function দেওয়া।

আর:

```jsx
handleClick()
```

মানে function এখনই execute করা।

---

# PART 9 — State

এখন React-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি:

# `useState`

ধরো counter বানাবো।

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>

      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

এখানে:

```jsx
const [count, setCount] = useState(0);
```

দুটি জিনিস:

```text
count       → current value
setCount    → value পরিবর্তনের function
```

Initial value:

```text
0
```

---

# State কীভাবে কাজ করে?

প্রথমে:

```text
count = 0
```

button click:

```jsx
setCount(count + 1)
```

তারপর:

```text
count = 1
```

আবার click:

```text
count = 2
```

React component আবার render করে।

---

# ⚠️ Beginner Mistake #3

অনেকে সরাসরি state পরিবর্তন করে:

```jsx
count = count + 1;
```

এটা করা উচিত নয়।

সঠিক:

```jsx
setCount(count + 1);
```

---

# PART 10 — State + Input

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("");

  return (
    <div>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
      />

      <h1>Hello {name}</h1>
    </div>
  );
}
```

তুমি input-এ লিখলে:

```text
A
```

state:

```text
name = "A"
```

তারপর:

```text
At
```

তারপর:

```text
Atiar
```

React UI update করে।

এটাকে বলে:

# Controlled Component

---

# PART 11 — Conditional Rendering

ধরো user login করেছে কিনা:

```jsx
function App() {
  const isLoggedIn = true;

  return (
    <div>
      {isLoggedIn ? (
        <h1>Dashboard</h1>
      ) : (
        <h1>Please Login</h1>
      )}
    </div>
  );
}
```

এটা:

```text
if true
    Dashboard
else
    Login
```

---

## `&&` দিয়ে

```jsx
{isLoggedIn && <button>Logout</button>}
```

`isLoggedIn` true হলে button দেখাবে।

---

# PART 12 — List Rendering

ধরো:

```jsx
const users = [
  { id: 1, name: "Atiar" },
  { id: 2, name: "Rahim" },
  { id: 3, name: "Karim" }
];
```

Render:

```jsx
function App() {
  const users = [
    { id: 1, name: "Atiar" },
    { id: 2, name: "Rahim" },
    { id: 3, name: "Karim" }
  ];

  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </div>
  );
}
```

---

# `key` কেন লাগে?

React list-এর কোন item পরিবর্তন হয়েছে সেটা track করতে `key` ব্যবহার করে।

সাধারণত:

```jsx
key={user.id}
```

ব্যবহার করো।

---

# ⚠️ Beginner Mistake #4

এটা avoid করো:

```jsx
{users.map((user, index) => (
  <p key={index}>{user.name}</p>
))}
```

বিশেষ করে list-এর order পরিবর্তন হলে index key সমস্যা তৈরি করতে পারে।

Better:

```jsx
key={user.id}
```

---

# PART 13 — Forms

React-এ form খুব গুরুত্বপূর্ণ।

```jsx
import { useState } from "react";

function App() {
  const [email, setEmail] = useState("");

  function handleSubmit(e) {
    e.preventDefault();

    console.log(email);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />

      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

---

# PART 14 — useEffect

`useEffect` React-এর খুব গুরুত্বপূর্ণ hook।

এটা সাধারণত side effects-এর জন্য ব্যবহার করা হয়।

যেমন:

```text
API request
Browser title update
Event listener
Timer
External system interaction
```

Example:

```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>Hello</h1>;
}
```

---

# API Fetch

```jsx
import { useEffect, useState } from "react";

function App() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://example.com/users")
      .then((res) => res.json())
      .then((data) => {
        setUsers(data);
      });
  }, []);

  return (
    <div>
      {users.map((user) => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

এখানে:

```text
Component render
       ↓
useEffect
       ↓
API request
       ↓
Data আসে
       ↓
setUsers
       ↓
Re-render
       ↓
UI update
```

---

# ⚠️ Beginner Mistake #5 — useEffect dependency

অনেকে লিখে:

```jsx
useEffect(() => {
  fetchData();
});
```

এতে প্রতিবার render-এর পর effect run করতে পারে।

API fetching-এর ক্ষেত্রে সাধারণত:

```jsx
useEffect(() => {
  fetchData();
}, []);
```

ব্যবহার করা হয় যদি effect-টি initial mount-এর পর একবার চালানো উদ্দেশ্য হয়।

---

# PART 15 — Loading State

API request করলে শুধু data state যথেষ্ট নয়।

তোমার দরকার:

```text
loading
error
data
```

Example:

```jsx
const [data, setData] = useState([]);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);
```

তারপর:

```jsx
useEffect(() => {
  async function fetchData() {
    try {
      const res = await fetch("/api/users");

      if (!res.ok) {
        throw new Error("Failed to fetch");
      }

      const result = await res.json();

      setData(result);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  }

  fetchData();
}, []);
```

UI:

```jsx
if (loading) {
  return <p>Loading...</p>;
}

if (error) {
  return <p>{error}</p>;
}

return (
  <div>
    {data.map((item) => (
      <p key={item.id}>{item.name}</p>
    ))}
  </div>
);
```

---

# PART 16 — Component Communication

React-এ data সাধারণত:

```text
Parent
   ↓
Child
```

যায়।

Example:

```jsx
function Parent() {
  const name = "Atiar";

  return <Child name={name} />;
}

function Child({ name }) {
  return <h1>{name}</h1>;
}
```

---

# Child → Parent

এখানে function prop ব্যবহার করা হয়।

```jsx
function Parent() {
  function handleMessage(message) {
    console.log(message);
  }

  return <Child onMessage={handleMessage} />;
}
```

Child:

```jsx
function Child({ onMessage }) {
  return (
    <button onClick={() => onMessage("Hello Parent")}>
      Send
    </button>
  );
}
```

এটা খুব গুরুত্বপূর্ণ interview concept।

---

# PART 17 — Lifting State Up

ধরো:

```text
Parent
├── Input
└── Display
```

Input-এর data Display-তে লাগবে।

তাহলে state Parent-এ নিয়ে আসি।

```jsx
function Parent() {
  const [name, setName] = useState("");

  return (
    <>
      <Input name={name} setName={setName} />
      <Display name={name} />
    </>
  );
}
```

এটাকে বলে:

# Lifting State Up

---

# PART 18 — useRef

`useRef` দিয়ে এমন value রাখা যায় যেটা পরিবর্তন হলেও সাধারণত component re-render করার জন্য ব্যবহৃত হয় না।

আর DOM element reference করার জন্যও খুব ব্যবহার হয়।

```jsx
import { useRef } from "react";

function App() {
  const inputRef = useRef(null);

  function focusInput() {
    inputRef.current.focus();
  }

  return (
    <>
      <input ref={inputRef} />

      <button onClick={focusInput}>
        Focus
      </button>
    </>
  );
}
```

Button click করলে input focus হবে।

---

# PART 19 — Context API

ধরো:

```text
App
 ↓
Navbar
 ↓
UserProfile
 ↓
Avatar
```

যদি user data অনেক level নিচে পাঠাতে হয়:

```text
App
 ↓ props
Navbar
 ↓ props
UserProfile
 ↓ props
Avatar
```

এটাকে বলা হয়:

# Prop Drilling

Context API দিয়ে কিছু ক্ষেত্রে এটা কমানো যায়।

```jsx
const UserContext = createContext();
```

Provider:

```jsx
<UserContext.Provider value={user}>
  <App />
</UserContext.Provider>
```

Child:

```jsx
const user = useContext(UserContext);
```

---

# PART 20 — useReducer

যখন state logic complex হয় তখন `useReducer` useful।

Example:

```jsx
const initialState = {
  count: 0
};
```

Reducer:

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return {
        ...state,
        count: state.count + 1
      };

    case "decrement":
      return {
        ...state,
        count: state.count - 1
      };

    default:
      return state;
  }
}
```

তারপর:

```jsx
const [state, dispatch] = useReducer(
  reducer,
  initialState
);
```

Dispatch:

```jsx
dispatch({ type: "increment" });
```

---

# PART 21 — Custom Hook

নিজের reusable hook তৈরি করতে পারো।

যেমন:

```jsx
function useCounter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount((prev) => prev + 1);
  };

  return {
    count,
    increment
  };
}
```

ব্যবহার:

```jsx
function App() {
  const { count, increment } = useCounter();

  return (
    <>
      <h1>{count}</h1>
      <button onClick={increment}>
        +
      </button>
    </>
  );
}
```

---
হ্যাঁ, এখানে প্রথমবার দেখলে একটু confusing লাগে। মূল ব্যাপারটা হলো:

```
setCount((prev) => prev + 1);
```

এখানে `prev` **তুমি `increment()` function-কে দিচ্ছ না**। বরং **React নিজে `prev` value-টা callback function-এর argument হিসেবে দেয়।**

ধাপে ধাপে দেখি।

### ১. তুমি `increment()` call করছ

```
<button onClick={increment}>
```

এখানে React যখন button-এ click detect করে, তখন effectively:

```
increment();
```

এর মতো করে function-টা চালায়।

তাই `increment` function-এর নিজের কোনো argument দরকার নেই:

```
const increment = () => {
   ...
}
```

---

### ২. কিন্তু ভেতরে তুমি `setCount()`-কে একটা function দিচ্ছ

```
setCount((prev) => prev + 1);
```

এখানে খেয়াল করো:

```
(prev) => prev + 1
```

এটা একটা **callback function**।

React এই callback function-টাকে পরে call করার সময় **বর্তমান state value** argument হিসেবে পাঠায়।

ধরো:

```
count = 0
```

তখন React internally conceptually এমন কিছু করে:

```
const newValue = callback(0);
```

অর্থাৎ:

```
(prev) => prev + 1
```

এর ক্ষেত্রে:

```
prev = 0
```

তাই:

```
0 + 1
// 1
```

---

### পরেরবার click করলে

এখন:

```
count = 1
```

আবার:

```
setCount((prev) => prev + 1);
```

React callback-কে বর্তমান state দিয়ে call করবে:

```
callback(1)
```

তাই:

```
prev = 1
1 + 1
// 2
```

তারপর:

```
click
 ↓
increment()
 ↓
setCount(prev => prev + 1)
 ↓
React prev = current count
 ↓
new count = prev + 1
```

### তাহলে `prev` কোথা থেকে আসে?

**React-এর `setCount` updater mechanism থেকে।**

এই:

```
setCount((prev) => prev + 1);
```

এর মানে অনেকটা:

> "React, তুমি যখন state update করবে, তখন আমাকে সেই মুহূর্তের latest state value `prev` হিসেবে দাও। আমি তার সাথে 1 যোগ করে নতুন state বানিয়ে দেব।"

এজন্য `increment` call করার সময়:

```
increment()
```

কোনো argument দিতে হয় না।

কারণ `prev` হলো **`increment`-এর parameter না**, এটা হলো `setCount`-এর কাছে দেওয়া **callback-এর parameter**।

একটা analogy:

```
function setState(callback) {
    const currentState = 10;

    const newState = callback(currentState);

    // newState = 11
}

setState((prev) => prev + 1);
```

এখানে তুমি `setState`-কে `10` পাঠাওনি। `setState` নিজেই callback-কে `10` দিয়েছে।

React-এর ক্ষেত্রেও conceptually একই ব্যাপার।
# PART 22 — State Update-এর গুরুত্বপূর্ণ বিষয়

এটা:

```jsx
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);
```

তিনবার update করার intention থাকলেও তুমি যেভাবে ভাবছো সেভাবে সবসময় হবে না, কারণ updates batching এবং current render-এর `count` value নিয়ে কাজ করতে পারে।

Better:

```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

এখানে প্রত্যেক update আগের state-এর উপর নির্ভর করে।

এটা **খুব গুরুত্বপূর্ণ beginner concept**।

---

# PART 23 — Immutable State

ধরো:

```jsx
const [user, setUser] = useState({
  name: "Atiar",
  age: 25
});
```

এভাবে করা উচিত নয়:

```jsx
user.age = 26;
```

Better:

```jsx
setUser({
  ...user,
  age: 26
});
```

Array-এর ক্ষেত্রেও:

```jsx
setUsers([
  ...users,
  newUser
]);
```

Delete:

```jsx
setUsers(
  users.filter(user => user.id !== id)
);
```

---

# PART 24 — CRUD

React project-এ CRUD খুব গুরুত্বপূর্ণ।

```text
C → Create
R → Read
U → Update
D → Delete
```

Example:

```text
Product Management
```

### Create

```http
POST /products
```

### Read

```http
GET /products
```

### Update

```http
PATCH /products/:id
```

### Delete

```http
DELETE /products/:id
```

তুমি যেহেতু REST API-ও শিখছো, React শেখার সময় CRUD project করা তোমার জন্য খুব useful হবে।

---

# PART 25 — React Router

একটা application:

```text
/
/products
/products/10
/login
/register
/dashboard
```

React Router দিয়ে route করা যায়।

Concept:

```text
URL
 ↓
Route
 ↓
Component
```

Example:

```jsx
<Route path="/" element={<Home />} />
<Route path="/products" element={<Products />} />
<Route path="/login" element={<Login />} />
```

---

# PART 26 — Authentication

Real application-এ:

```text
Register
   ↓
Login
   ↓
Token / Session
   ↓
Authenticated User
   ↓
Dashboard
```

React frontend সাধারণত backend API-এর সাথে communicate করে।

Example:

```text
React
  ↓
REST API
  ↓
Django / Node / Laravel
  ↓
Database
```

---

# PART 27 — Protected Route

ধরো:

```text
/dashboard
```

শুধু logged-in user দেখতে পারবে।

Concept:

```jsx
if (!user) {
  return <Navigate to="/login" />;
}

return <Dashboard />;
```

---

# PART 28 — LocalStorage

Browser-এ কিছু non-sensitive client-side data রাখা যায়:

```jsx
localStorage.setItem(
  "name",
  "Atiar"
);
```

Get:

```jsx
const name = localStorage.getItem("name");
```

Remove:

```jsx
localStorage.removeItem("name");
```

তবে authentication/security-sensitive data কোথায় রাখা হবে সেটা backend/auth architecture-এর উপর নির্ভর করে; শুধু localStorage-কে সব সমস্যার সমাধান ভাববে না।

---

# PART 29 — Performance

Advanced React-এ তিনটা concept খুব গুরুত্বপূর্ণ:

```text
React.memo
useMemo
useCallback
```

### React.memo

Unnecessary child re-render কমাতে সাহায্য করতে পারে।

```jsx
const User = React.memo(function User({ name }) {
  return <h1>{name}</h1>;
});
```

---

# useMemo

Expensive calculation-এর result memoize করতে ব্যবহার করা যায়।

```jsx
const result = useMemo(() => {
  return expensiveCalculation(data);
}, [data]);
```

---

# useCallback

Function reference memoize করতে পারে।

```jsx
const handleClick = useCallback(() => {
  console.log("clicked");
}, []);
```

### Important

Beginner অবস্থায় এগুলো everywhere ব্যবহার করবে না।

আগে বুঝবে:

```text
কেন re-render হচ্ছে?
কোথায় performance problem?
```

তারপর optimization।

---

# PART 30 — React Architecture

Beginner project:

```text
src/
├── App.jsx
├── components/
└── pages/
```

বড় project:

```text
src/
├── components/
├── pages/
├── hooks/
├── services/
├── context/
├── utils/
├── types/
├── assets/
└── features/
```

আর feature-based structure:

```text
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── pages/
│   │
│   └── products/
│       ├── components/
│       ├── hooks/
│       └── services/
│
├── components/
└── app/
```

বড় application-এর জন্য এটা বেশি scalable হতে পারে।

---

# PART 31 — Advanced React

React ভালোভাবে শেখার পর এগুলো শিখবে:

```text
useReducer
Context API
Custom Hooks
Compound Components
Render Props
Higher-Order Components
Error Boundaries
Code Splitting
Lazy Loading
Suspense
Performance Optimization
Server/Client concepts
State management
Data fetching
Testing
TypeScript
```

সবগুলো একসাথে মুখস্থ করার দরকার নেই।

---

# PART 32 — Data Fetching

Beginner:

```jsx
fetch()
```

তারপর:

```text
Axios
```

তারপর production-level application-এ:

```text
TanStack Query
```

শিখতে পারো।

TanStack Query বিশেষভাবে useful:

```text
Caching
Fetching
Refetching
Loading
Error
Mutation
Pagination
Infinite Query
```

---

# PART 33 — TypeScript + React

JavaScript React:

```jsx
function User({ name, age }) {
```

TypeScript:

```tsx
type UserProps = {
  name: string;
  age: number;
};

function User({ name, age }: UserProps) {
  return (
    <h1>
      {name} - {age}
    </h1>
  );
}
```

Professional React development-এর জন্য TypeScript শেখা খুব useful।

---

# PART 34 — Testing

React application test করা শেখা দরকার।

Concept:

```text
Component Test
Integration Test
End-to-End Test
```

Common tools:

```text
Vitest
React Testing Library
Playwright
```

---

# 🔥 Beginner-এর সবচেয়ে Common Mistakes

তুমি এগুলো বিশেষভাবে খেয়াল রাখবে।

### 1. State সরাসরি পরিবর্তন

❌

```jsx
count++;
```

✅

```jsx
setCount(prev => prev + 1);
```

---

### 2. Event-এ function immediately call করা

❌

```jsx
onClick={handleClick()}
```

✅

```jsx
onClick={handleClick}
```

---

### 3. Array index-কে সবসময় key ব্যবহার করা

❌

```jsx
key={index}
```

✅

```jsx
key={user.id}
```

---

### 4. Props mutate করা

❌

```jsx
props.name = "X";
```

---

### 5. State mutate করা

❌

```jsx
user.name = "X";
```

✅

```jsx
setUser({
  ...user,
  name: "X"
});
```

---

### 6. সব জায়গায় useEffect ব্যবহার

`useEffect` দেখলেই API বা calculation ঢুকিয়ে দেবে না।

আগে বুঝবে:

> এটা কি সত্যিই external side effect?

---

### 7. সবকিছু Context-এ রাখা

Context useful, কিন্তু সব state Context-এ রাখার দরকার নেই।

---

### 8. সব জায়গায় useMemo/useCallback

Optimization-এর আগে problem identify করো।

---

### 9. Component অনেক বড় করা

যেমন:

```text
App.jsx
1000 lines
```

এর বদলে:

```text
Navbar.jsx
ProductList.jsx
ProductCard.jsx
Cart.jsx
Footer.jsx
```

ভেঙে ফেলো।

---

### 10. API code component-এর ভিতরে সব লিখে ফেলা

Beginner:

```jsx
function Products() {

  fetch(...)
  fetch(...)
  fetch(...)

  // 500 lines...
}
```

Advanced project-এ API logic আলাদা service/hook layer-এ নেওয়া ভালো।

---

# 🎯 তোমার জন্য React শেখার Practical Course

তোমার existing JavaScript knowledge অনুযায়ী আমি এভাবে এগোতে বলব:

```text
PHASE 1 — Foundation
│
├── React concept
├── Vite
├── JSX
├── Component
├── Props
├── Events
└── Conditional rendering

PHASE 2 — Core React
│
├── useState
├── Forms
├── Lists
├── Keys
├── State update
├── Immutable state
└── Component communication

PHASE 3 — Hooks
│
├── useEffect
├── useRef
├── useContext
├── useReducer
└── Custom Hooks

PHASE 4 — API
│
├── Fetch
├── Axios
├── Loading
├── Error
├── CRUD
├── Pagination
└── Search / Filter

PHASE 5 — Routing
│
├── React Router
├── Nested routes
├── Dynamic routes
├── Protected routes
└── Authentication

PHASE 6 — Advanced
│
├── Context
├── Reducer
├── Performance
├── memo
├── useMemo
├── useCallback
└── Lazy loading

PHASE 7 — Professional
│
├── TanStack Query
├── TypeScript
├── Testing
├── Architecture
└── Security basics

PHASE 8 — Projects
│
├── Todo App
├── Expense Tracker
├── Blog
├── E-commerce
└── Admin Dashboard
```

## 🧠 সবচেয়ে গুরুত্বপূর্ণ কথা

React শেখার সময় **শুধু tutorial দেখবে না**।

প্রতিটি topic-এর পরে নিজে code করবে।

যেমন:

```text
useState
   ↓
Counter বানাও

Props
   ↓
ProductCard বানাও

useEffect
   ↓
API থেকে users আনো

Forms
   ↓
Registration form বানাও

CRUD
   ↓
Product management বানাও

Router
   ↓
Multi-page SPA বানাও

Authentication
   ↓
Login + Dashboard বানাও
```

**তোমার জন্য সবচেয়ে ভালো হবে এই tutorial-টা আমরা একেকটা Phase ধরে করি।** প্রতিটি Phase-এ আমি **concept → syntax → real example → beginner mistake → exercise → mini project → interview question** দেব। এতে React শুধু বুঝবে না, নিজে project-ও বানাতে পারবে।


---
