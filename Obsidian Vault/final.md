অবশ্যই। তুমি যেহেতু **Next.js interview preparation** করছো, নিচের ৩০টা প্রশ্নকে আমি **Beginner → Intermediate → Advanced** order-এ দিলাম। এগুলো interview-তে খুব common এবং practical।

# Next.js — 30 Most Important Interview Questions & Answers

## 🟢 Beginner — 1–10

### 1. What is Next.js?

**Answer:**  
Next.js is a React framework for building modern full-stack web applications.

It provides features like:

- Server-Side Rendering (SSR)
    
- Static Site Generation (SSG)
    
- Server Components
    
- API/Route Handlers
    
- File-based routing
    
- Image optimization
    
- Metadata/SEO
    
- Middleware
    

**Short interview answer:**

> Next.js is a React framework that provides routing, server rendering, API routes, optimization, and other features needed to build production-ready web applications.

---

### 2. What is the difference between React and Next.js?

|React|Next.js|
|---|---|
|UI library|React framework|
|Routing needs extra library|Built-in routing|
|Mostly client-side|Server + client rendering|
|SEO requires extra setup|Better built-in SEO support|
|No built-in backend API|Route Handlers available|
|More configuration|More conventions|

**Interview answer:**

> React is primarily a UI library, while Next.js is a framework built on React that provides routing, rendering, backend capabilities, optimization, and production features.

---

### 3. What is App Router in Next.js?

**Answer:**

App Router is the modern routing system introduced in Next.js 13.

It uses the `app` directory.

Example:

```text
app/
├── page.js
├── about/
│   └── page.js
└── dashboard/
    └── page.js
```

Routes:

```text
/
/about
/dashboard
```

---

### 4. What is file-based routing?

In Next.js, routes are created based on the folder and file structure.

Example:

```text
app/
├── page.js
├── about/
│   └── page.js
└── products/
    └── page.js
```

This creates:

```text
/
/about
/products
```

You don't need to manually configure routes like traditional React Router.

---

### 5. What is `page.js`?

`page.js` defines the UI for a route.

Example:

```jsx
export default function HomePage() {
  return <h1>Home Page</h1>;
}
```

Located at:

```text
app/page.js
```

It represents:

```text
/
```

---

### 6. What is `layout.js`?

`layout.js` is used to create shared UI around pages.

Example:

```jsx
export default function RootLayout({ children }) {
  return (
    <html>
      <body>
        <nav>Navbar</nav>

        {children}

        <footer>Footer</footer>
      </body>
    </html>
  );
}
```

The layout can persist while navigating between pages.

---

### 7. What is nested layout?

A layout inside another route segment is called a nested layout.

Example:

```text
app/
├── layout.js
├── page.js
└── dashboard/
    ├── layout.js
    ├── page.js
    └── settings/
        └── page.js
```

Dashboard pages can share the dashboard layout while also inheriting the root layout.

---

### 8. What is a Dynamic Route?

Dynamic routes allow route parameters.

Example:

```text
app/products/[id]/page.js
```

URL:

```text
/products/123
/products/456
```

The `id` is dynamic.

Example:

```jsx
export default async function ProductPage({ params }) {
  const { id } = await params;

  return <h1>Product {id}</h1>;
}
```

---

### 9. What is a Client Component?

A Client Component is a component that can use client-side features such as:

- `useState`
    
- `useEffect`
    
- event handlers
    
- browser APIs
    

You mark it using:

```jsx
"use client";
```

Example:

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

---

### 10. What is a Server Component?

In the App Router, components are Server Components by default.

They execute on the server and can directly perform server-side work such as fetching data.

Example:

```jsx
export default async function UsersPage() {
  const response = await fetch("https://api.example.com/users");
  const users = await response.json();

  return (
    <div>
      {users.map(user => (
        <p key={user.id}>{user.name}</p>
      ))}
    </div>
  );
}
```

---

# 🟡 Intermediate — 11–20

### 11. Server Component vs Client Component?

|Server Component|Client Component|
|---|---|
|Default|Requires `"use client"`|
|Runs on server|Runs in browser|
|Can fetch server-side data|Can use browser APIs|
|Cannot use `useState`|Can use `useState`|
|Cannot use `onClick`|Can use event handlers|
|Good for data fetching|Good for interaction|

**Important interview point:**

> Keep components as Server Components by default and use Client Components only when client-side interactivity is required.

---

### 12. Can a Server Component import a Client Component?

**Yes.**

Example:

```jsx
// Server Component

import Button from "./Button";

export default function Page() {
  return (
    <div>
      <h1>Hello</h1>
      <Button />
    </div>
  );
}
```

But a Client Component cannot freely import a Server Component.

Instead, you can pass Server Component UI through `children` or props patterns designed for composition.

---

### 13. What is SSR?

SSR means **Server-Side Rendering**.

The page's HTML is generated on the server for a request and then sent to the browser.

Benefits:

- Better initial rendering
    
- SEO benefits
    
- Server-side data access
    

Conceptually:

```text
Browser
   ↓
Server
   ↓
Generate HTML
   ↓
Browser
```

---

### 14. What is SSG?

SSG means **Static Site Generation**.

The page is generated ahead of time and can be served as static content.

Useful for:

- Blogs
    
- Documentation
    
- Marketing pages
    
- Product pages that don't change frequently
    

---

### 15. What is ISR?

ISR means **Incremental Static Regeneration**.

It allows statically generated content to be updated after a specific period without rebuilding the entire application.

Example:

```jsx
const response = await fetch(
  "https://api.example.com/products",
  {
    next: {
      revalidate: 60,
    },
  }
);
```

The data can be revalidated approximately every 60 seconds.

---

### 16. How do you fetch data in Next.js?

A Server Component can use `fetch()` directly:

```jsx
export default async function Products() {
  const response = await fetch(
    "https://api.example.com/products"
  );

  const products = await response.json();

  return (
    <div>
      {products.map(product => (
        <p key={product.id}>
          {product.name}
        </p>
      ))}
    </div>
  );
}
```

This is one of the major advantages of the App Router.

---

### 17. How do you create an API in Next.js?

With App Router, you can use **Route Handlers**.

Example:

```text
app/api/users/route.js
```

```js
export async function GET() {
  return Response.json({
    message: "Users API",
  });
}
```

Endpoint:

```text
/api/users
```

---

### 18. What HTTP methods can Route Handlers support?

Common methods include:

```text
GET
POST
PUT
PATCH
DELETE
```

Example:

```js
export async function POST(request) {
  const body = await request.json();

  return Response.json({
    message: "User created",
    data: body,
  });
}
```

---

### 19. What is Middleware in Next.js?

Middleware allows you to execute logic before a request is completed.

Common use cases:

- Authentication
    
- Authorization
    
- Redirects
    
- Rewrites
    
- Request processing
    

Example:

```js
import { NextResponse } from "next/server";

export function middleware(request) {
  return NextResponse.next();
}
```

---

### 20. How do you protect a dashboard route?

A common approach is checking authentication information on the server/middleware and redirecting unauthenticated users.

Conceptually:

```text
User
 ↓
/dashboard
 ↓
Authenticated?
 ├── Yes → Dashboard
 └── No  → /login
```

For example, middleware can inspect a session/token and redirect:

```js
return NextResponse.redirect(
  new URL("/login", request.url)
);
```

For sensitive authorization, the server should **also** verify access when handling the actual data/API request; middleware alone should not be treated as the only security boundary.

---

# 🔴 Advanced — 21–30

### 21. What is Hydration?

Hydration is the process where React attaches its client-side behavior to HTML that was already rendered.

Conceptually:

```text
Server
 ↓
HTML
 ↓
Browser
 ↓
React hydration
 ↓
Interactive UI
```

For example, a server-rendered page can become interactive after React hydrates the client-side components.

---

### 22. What is `"use client"`?

`"use client"` tells Next.js that the module is a Client Component boundary.

Example:

```jsx
"use client";

import { useState } from "react";

export default function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={e => setName(e.target.value)}
    />
  );
}
```

Without `"use client"`, you cannot use client-only features such as `useState` in that component.

---

### 23. What are Server Actions?

Server Actions allow you to define server-side functions that can be invoked from supported client interactions.

Example:

```js
"use server";

export async function createUser(formData) {
  const name = formData.get("name");

  // database operation
}
```

They are useful for operations such as:

- Form submissions
    
- Database mutations
    
- Server-side actions
    

You should still perform proper validation and authorization on the server.

---

### 24. What is the difference between Route Handler and Server Action?

**Route Handler:**

```text
/api/users
```

Designed around HTTP requests and API endpoints.

**Server Action:**

```text
createUser()
```

A server-side function designed for invoking server logic, especially from React/Next.js interactions and forms.

Simple interview answer:

> Route Handlers are useful for building HTTP APIs, while Server Actions are useful for invoking server-side functions, particularly for mutations and form actions.

---

### 25. What is `loading.js`?

`loading.js` provides a loading UI for a route segment.

Example:

```text
app/
├── dashboard/
│   ├── loading.js
│   └── page.js
```

Example:

```jsx
export default function Loading() {
  return <p>Loading...</p>;
}
```

It can provide an immediate loading state while the route's content is being rendered.

---

### 26. What is `error.js`?

`error.js` is used to handle errors within a route segment.

Example:

```jsx
"use client";

export default function Error({ reset }) {
  return (
    <div>
      <h2>Something went wrong!</h2>

      <button onClick={() => reset()}>
        Try again
      </button>
    </div>
  );
}
```

---

### 27. What is `not-found.js`?

It defines the UI shown when a resource isn't found.

Example:

```text
app/
├── products/
│   ├── [id]/
│   │   ├── page.js
│   │   └── not-found.js
```

You can trigger it using:

```js
import { notFound } from "next/navigation";

notFound();
```

---

### 28. What is the difference between `Link` and `<a>`?

Next.js provides:

```jsx
import Link from "next/link";
```

Use:

```jsx
<Link href="/about">
  About
</Link>
```

`Link` enables Next.js client-side navigation and prefetching behavior.

A normal:

```html
<a href="/about">
```

performs standard browser navigation.

**Interview answer:**

> For internal Next.js navigation, `Link` is generally preferred because it integrates with Next.js routing and client-side navigation.

---

### 29. How do you optimize images in Next.js?

Next.js provides the `Image` component:

```jsx
import Image from "next/image";

export default function Profile() {
  return (
    <Image
      src="/profile.jpg"
      alt="Profile"
      width={500}
      height={500}
    />
  );
}
```

Benefits include:

- Image optimization
    
- Responsive behavior
    
- Lazy loading where appropriate
    
- Size optimization
    

---

### 30. How would you build a production Next.js application?

This is a **very important senior/intermediate interview question**.

A good answer:

> I would structure the application using the App Router, keep Server Components as the default, use Client Components only where interactivity is required, implement authentication and authorization on the server, fetch and cache data appropriately, use Route Handlers or a separate backend API when needed, validate user input, optimize images and fonts, handle loading and errors, configure environment variables securely, and deploy with proper monitoring and performance optimization.

A typical architecture could be:

```text
Next.js Frontend
       │
       ├── Server Components
       ├── Client Components
       ├── Server Actions
       ├── Route Handlers
       │
       ↓
Backend API
       │
       ↓
Database
```

---

# ⭐ Most Important 10 to Memorize First

যদি interview খুব কাছাকাছি হয়, আগে এই ১০টা ভালোভাবে শিখো:

1. **What is Next.js?**
    
2. **React vs Next.js**
    
3. **App Router**
    
4. **File-based routing**
    
5. **Server Component**
    
6. **Client Component**
    
7. **Server vs Client Component**
    
8. **SSR vs SSG vs ISR**
    
9. **Route Handlers**
    
10. **Middleware & Authentication**
    

এরপর এগুলো practicalভাবে code করে practice করলে interview-তে শুধু definition না, **"how would you implement it?"** ধরনের প্রশ্নেরও উত্তর দিতে পারবে।

----
অবশ্যই। React.js interview-এর জন্য নিচে **সবচেয়ে গুরুত্বপূর্ণ ৩০টি প্রশ্ন ও সহজ interview-ready answer** দিলাম। তোমার Full Stack Developer preparation-এর জন্য এগুলো ভালোভাবে জানা দরকার।

# React.js — 30 Most Important Interview Questions & Answers

## 🟢 Beginner — 1–10

### 1. What is React.js?

**Answer:**

> React.js is a JavaScript library for building user interfaces, especially single-page applications. It uses reusable components and a virtual DOM to efficiently update the UI.

মূল বিষয়:

- Component-based
    
- Reusable UI
    
- Virtual DOM
    
- Declarative
    
- JavaScript library
    

---

### 2. What are the main features of React?

Important features:

- Component-based architecture
    
- Virtual DOM
    
- JSX
    
- One-way data flow
    
- Reusable components
    
- Hooks
    
- Declarative UI
    

---

### 3. What is JSX?

JSX stands for **JavaScript XML**.

It allows us to write HTML-like syntax inside JavaScript.

```jsx
const element = <h1>Hello React</h1>;
```

JSX ultimately gets transformed into JavaScript.

---

### 4. What is a Component?

A component is a reusable piece of UI.

Example:

```jsx
function Button() {
  return <button>Click Me</button>;
}
```

You can use it multiple times:

```jsx
<Button />
<Button />
```

---

### 5. What are Functional Components?

A functional component is a JavaScript function that returns JSX.

```jsx
function Welcome() {
  return <h1>Welcome</h1>;
}
```

Modern React primarily uses functional components with Hooks.

---

### 6. What are Props?

Props are data passed from a parent component to a child component.

```jsx
function User({ name }) {
  return <h1>Hello {name}</h1>;
}
```

Parent:

```jsx
<User name="Atiar" />
```

Props are **read-only**.

---

### 7. What is State?

State is data managed inside a component that can change over time.

Example:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

When state changes, React can re-render the component.

---

### 8. Props vs State?

|Props|State|
|---|---|
|Passed from parent|Managed by component|
|Read-only|Can be updated|
|Used to pass data|Used for changing data|
|Parent controls value|Component controls value|

**Interview answer:**

> Props are used to pass data between components, while state is used to manage data that changes within a component.

---

### 9. What is Virtual DOM?

The Virtual DOM is an in-memory representation of the UI.

When state or props change, React determines what needs to change and updates the real DOM accordingly.

Simple concept:

```text
State changes
     ↓
React creates new UI representation
     ↓
Compare with previous representation
     ↓
Update necessary DOM parts
```

---

### 10. What is the difference between Real DOM and Virtual DOM?

**Real DOM:**

Browser's actual DOM.

**Virtual DOM:**

React's in-memory representation of the UI.

The important point is that React uses reconciliation to determine the necessary DOM updates rather than manually updating every affected element yourself.

---

# 🟡 Intermediate — 11–20

### 11. What is `useState()`?

`useState` is a React Hook used to add state to a functional component.

```jsx
const [name, setName] = useState("");
```

Here:

```text
name     → current state
setName  → function to update state
""       → initial value
```

---

### 12. What is `useEffect()`?

`useEffect` lets you synchronize a component with external systems.

Common examples:

- API requests
    
- Event listeners
    
- Timers
    
- Subscriptions
    

Example:

```jsx
useEffect(() => {
  console.log("Component mounted");
}, []);
```

The empty dependency array means the effect does not re-run just because the component re-renders.

---

### 13. What is the dependency array in `useEffect`?

Example:

```jsx
useEffect(() => {
  console.log("Effect");
}, [count]);
```

The effect re-runs when `count` changes.

Common patterns:

```jsx
useEffect(() => {
  // ...
}, []);
```

Runs after the initial mount.

```jsx
useEffect(() => {
  // ...
}, [count]);
```

Runs when `count` changes.

```jsx
useEffect(() => {
  // ...
});
```

Runs after every completed render.

---

### 14. What are Hooks?

Hooks are functions that allow functional components to use React features.

Common Hooks:

```text
useState
useEffect
useContext
useRef
useMemo
useCallback
useReducer
```

Example:

```jsx
const [count, setCount] = useState(0);
```

---

### 15. What are the Rules of Hooks?

Two important rules:

**Rule 1:** Don't call Hooks inside loops, conditions, or nested functions.

Wrong:

```jsx
if (loggedIn) {
  useState(0);
}
```

Correct:

```jsx
const [count, setCount] = useState(0);

if (loggedIn) {
  // use count
}
```

**Rule 2:** Call Hooks only from:

- React function components
    
- Custom Hooks
    

---

### 16. What is Conditional Rendering?

Showing different UI based on a condition.

```jsx
{isLoggedIn ? (
  <Dashboard />
) : (
  <Login />
)}
```

Another example:

```jsx
{isLoading && <p>Loading...</p>}
```

---

### 17. How do you render a list in React?

Usually with `.map()`:

```jsx
const users = [
  { id: 1, name: "Atiar" },
  { id: 2, name: "Rahman" }
];

return (
  <div>
    {users.map(user => (
      <p key={user.id}>{user.name}</p>
    ))}
  </div>
);
```

---

### 18. Why is `key` important in React?

Keys help React identify which list items have changed, been added, or removed.

Good:

```jsx
users.map(user => (
  <p key={user.id}>{user.name}</p>
))
```

Avoid using array indexes as keys when list items can be reordered, inserted, or deleted.

---

### 19. What is Event Handling in React?

React uses event handlers such as:

```jsx
function Button() {
  function handleClick() {
    console.log("Clicked");
  }

  return (
    <button onClick={handleClick}>
      Click
    </button>
  );
}
```

Notice:

```jsx
onClick={handleClick}
```

not:

```jsx
onClick={handleClick()}
```

because the latter calls the function during rendering.

---

### 20. What is a Controlled Component?

A controlled form input has its value controlled by React state.

```jsx
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={e => setName(e.target.value)}
    />
  );
}
```

Here React state is the source of truth.

---

# 🔴 Advanced — 21–30

### 21. What is an Uncontrolled Component?

An uncontrolled component lets the DOM maintain the input's current value.

You can access it using `useRef`.

```jsx
const inputRef = useRef();

function handleSubmit() {
  console.log(inputRef.current.value);
}

return <input ref={inputRef} />;
```

**Interview answer:**

> In a controlled component, React state controls the input value. In an uncontrolled component, the DOM manages the value and React accesses it through a ref when needed.

---

### 22. What is `useRef()`?

`useRef` stores a mutable value that persists across renders without causing a re-render when changed.

Example:

```jsx
const inputRef = useRef(null);

<input ref={inputRef} />
```

Then:

```jsx
inputRef.current.focus();
```

Common uses:

- DOM references
    
- Storing timer IDs
    
- Keeping mutable values between renders
    

---

### 23. What is `useContext()`?

`useContext` allows components to access shared context without manually passing props through every level.

Example:

```jsx
const AuthContext = createContext(null);
```

Provider:

```jsx
<AuthContext.Provider value={user}>
  <App />
</AuthContext.Provider>
```

Consumer:

```jsx
const user = useContext(AuthContext);
```

Common uses:

- Authentication
    
- Theme
    
- Language
    
- Global UI settings
    

---

### 24. What is Prop Drilling?

Prop drilling means passing props through intermediate components that don't actually need the data.

Example:

```text
App
 ↓ user
Dashboard
 ↓ user
Profile
 ↓ user
UserInfo
```

If many levels are involved, you might consider:

- Context
    
- State management library
    
- Better component composition
    

---

### 25. What is `useMemo()`?

`useMemo` memoizes a calculated value.

```jsx
const result = useMemo(() => {
  return expensiveCalculation(data);
}, [data]);
```

It can help avoid repeating expensive calculations when dependencies haven't changed.

**Important:**

Don't use `useMemo` everywhere automatically. It has its own overhead.

---

### 26. What is `useCallback()`?

`useCallback` memoizes a function reference.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

It's mainly useful when function identity matters, such as when passing callbacks to memoized child components.

---

### 27. `useMemo` vs `useCallback`?

Very common interview question.

|useMemo|useCallback|
|---|---|
|Memoizes a value|Memoizes a function|
|Returns calculated result|Returns function reference|

Example:

```jsx
const value = useMemo(() => calculate(), []);
```

vs:

```jsx
const fn = useCallback(() => doSomething(), []);
```

**Easy trick:**

> `useMemo` → remember the **result**  
> `useCallback` → remember the **function**

---

### 28. What is `React.memo()`?

`React.memo()` can prevent a component from re-rendering when its props haven't changed according to its comparison.

Example:

```jsx
const User = React.memo(function User({ name }) {
  return <h1>{name}</h1>;
});
```

It's useful when avoiding unnecessary child renders is actually beneficial.

---

### 29. What is Reconciliation?

Reconciliation is the process React uses to determine how the UI should be updated when state or props change.

React compares the previous rendered tree with the new one and determines the necessary updates.

Keys are especially important when reconciling lists.

---

### 30. What is the difference between `useEffect` and `useLayoutEffect`?

`useEffect` generally runs after the browser has painted the updated UI.

`useLayoutEffect` runs synchronously after DOM mutations but before the browser paints.

Use `useLayoutEffect` when you need to measure or synchronously adjust layout before the user sees it.

Example use case:

```jsx
useLayoutEffect(() => {
  // measure DOM/layout
}, []);
```

For normal API calls, subscriptions, and other side effects, `useEffect` is generally preferred.

---

# ⭐ Interview-এ সবচেয়ে বেশি গুরুত্ব দাও

তোমার জন্য এই **15টা অবশ্যই strong** করা উচিত:

1. What is React?
    
2. React vs JavaScript
    
3. JSX
    
4. Components
    
5. Props
    
6. State
    
7. Props vs State
    
8. Virtual DOM
    
9. `useState`
    
10. `useEffect`
    
11. Controlled vs Uncontrolled Components
    
12. `useContext`
    
13. Prop Drilling
    
14. `useMemo` vs `useCallback`
    
15. `React.memo`
    

### বিশেষ করে এগুলো শুধু মুখস্থ না করে code করে শিখবে:

```text
Props
   ↓
State
   ↓
useEffect
   ↓
API Fetch
   ↓
Form
   ↓
Context API
   ↓
Custom Hook
   ↓
useMemo / useCallback
   ↓
React.memo
   ↓
Performance Optimization
```

**Interview-এ শুধু "What is X?" আসে না।** অনেক সময় interviewer জিজ্ঞেস করবে **"Why do you use it?", "When do you use it?", "Show me with code", "What problem does it solve?"** — তাই প্রতিটি topic-এর **definition + use case + code example + common mistake** জানতে হবে।

---
অবশ্যই। JavaScript interview-এর জন্য **সবচেয়ে গুরুত্বপূর্ণ ৩০টি প্রশ্ন ও interview-ready answer** নিচে দিলাম। React/Next.js interview-এর আগে এগুলো strong করা খুব জরুরি।

# JavaScript — 30 Most Important Interview Questions

## 🟢 Beginner — 1–10

### 1. What is JavaScript?

> JavaScript is a high-level, dynamically typed programming language mainly used to make web applications interactive and dynamic.

এটি browser এবং server-side environment যেমন Node.js-এও ব্যবহার করা যায়।

---

### 2. What are `var`, `let`, and `const`?

||var|let|const|
|---|---|---|---|
|Scope|Function|Block|Block|
|Reassign|✅|✅|❌|
|Redeclare same scope|✅|❌|❌|
|Hoisting|Yes|Yes, TDZ|Yes, TDZ|

Example:

```js
let age = 24;
age = 25;

const name = "Atiar";
// name = "Rahman"; ❌
```

**Interview answer:**

> In modern JavaScript, I generally prefer `const` by default and use `let` when reassignment is required. I avoid `var` in modern code.

---

### 3. What is the difference between `==` and `===`?

`==` performs type coercion.

`===` checks value and type without implicit coercion.

```js
5 == "5"     // true
5 === "5"    // false
```

**Interview answer:**

> `===` is generally preferred because it avoids unexpected type coercion.

---

### 4. What are primitive data types?

JavaScript primitive types are:

```text
string
number
bigint
boolean
undefined
symbol
null
```

Example:

```js
let name = "Atiar";     // string
let age = 24;           // number
let active = true;      // boolean
let value;              // undefined
let data = null;        // null
```

---

### 5. What is the difference between `null` and `undefined`?

`undefined` usually means a value hasn't been assigned.

```js
let x;
console.log(x); // undefined
```

`null` is an intentional empty value.

```js
let user = null;
```

**Easy answer:**

> `undefined` generally means missing/unassigned, while `null` is an explicitly assigned empty value.

---

### 6. What is hoisting?

Hoisting refers to JavaScript's behavior where declarations are processed before the code executes.

Example:

```js
console.log(x);

var x = 10;
```

Output:

```text
undefined
```

`let` and `const` are also hoisted in the language's execution model, but accessing them before initialization results in the **Temporal Dead Zone (TDZ)** error.

---

### 7. What is scope?

Scope determines where a variable can be accessed.

Types include:

- Global scope
    
- Function scope
    
- Block scope
    

Example:

```js
let globalValue = 10;

function test() {
  let localValue = 20;

  console.log(globalValue); // ✅
  console.log(localValue);  // ✅
}
```

Outside the function:

```js
console.log(localValue); // ❌
```

---

### 8. What is a function?

A function is a reusable block of code.

```js
function add(a, b) {
  return a + b;
}

console.log(add(10, 20));
```

Output:

```text
30
```

---

### 9. What is an arrow function?

Arrow functions provide a shorter function syntax.

```js
const add = (a, b) => {
  return a + b;
};
```

Short version:

```js
const add = (a, b) => a + b;
```

One important difference is that arrow functions don't have their own `this`.

---

### 10. Function declaration vs function expression?

Function declaration:

```js
function greet() {
  console.log("Hello");
}
```

Function expression:

```js
const greet = function () {
  console.log("Hello");
};
```

A declaration can be called before its declaration because of function declaration hoisting.

---

# 🟡 Intermediate — 11–20

### 11. What is a callback function?

A callback is a function passed to another function to be called later.

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

greet("Atiar", () => {
  console.log("Welcome!");
});
```

Callbacks are common in:

- Event handling
    
- Array methods
    
- Async operations
    

---

### 12. What is a higher-order function?

A higher-order function either:

1. Takes a function as an argument, or
    
2. Returns a function.
    

Example:

```js
function calculate(a, b, operation) {
  return operation(a, b);
}

const result = calculate(10, 20, (a, b) => a + b);

console.log(result);
```

---

### 13. What is a closure?

A closure occurs when a function remembers and can access variables from its surrounding lexical scope even after the outer function has finished executing.

```js
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
```

Here the inner function retains access to `count`.

**Very important interview topic.**

---

### 14. What is lexical scope?

Lexical scope means a function's accessible variables are determined by where the function is written in the source code.

```js
let x = 10;

function outer() {
  let y = 20;

  function inner() {
    console.log(x);
    console.log(y);
  }

  inner();
}
```

`inner()` can access variables from its outer lexical environments.

---

### 15. What is `this` in JavaScript?

`this` refers to a value determined by how a function is called.

Example:

```js
const user = {
  name: "Atiar",

  greet() {
    console.log(this.name);
  }
};

user.greet();
```

Output:

```text
Atiar
```

The behavior of `this` depends on the invocation context.

---

### 16. What is the difference between normal function and arrow function regarding `this`?

Normal function:

```js
const user = {
  name: "Atiar",

  greet: function () {
    console.log(this.name);
  }
};
```

Arrow function:

```js
const user = {
  name: "Atiar",

  greet: () => {
    console.log(this.name);
  }
};
```

Arrow functions **do not create their own `this`**. They capture `this` from their surrounding lexical scope.

This is one reason arrow functions behave differently in object methods.

---

### 17. What is a Promise?

A Promise represents the eventual result of an asynchronous operation.

It has three states:

```text
pending
fulfilled
rejected
```

Example:

```js
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise.then(result => {
  console.log(result);
});
```

---

### 18. What is `async/await`?

`async/await` provides a cleaner syntax for working with Promises.

```js
async function getUser() {
  const response = await fetch(
    "https://api.example.com/users"
  );

  const data = await response.json();

  return data;
}
```

Usually, `try/catch` is used for error handling:

```js
async function getUser() {
  try {
    const response = await fetch(url);
    return await response.json();
  } catch (error) {
    console.error(error);
  }
}
```

---

### 19. What is the Event Loop?

JavaScript uses an event loop to coordinate synchronous code with asynchronous callbacks/tasks.

Basic idea:

```text
Call Stack
    ↓
Web APIs / runtime
    ↓
Queues
    ↓
Event Loop
    ↓
Call Stack
```

JavaScript executes synchronous code first, then processes queued asynchronous work according to the relevant queue rules.

---

### 20. What is the difference between synchronous and asynchronous JavaScript?

**Synchronous:**

Code executes sequentially.

```js
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

**Asynchronous:**

Some work can complete later without blocking the rest of the program.

```js
console.log("A");

setTimeout(() => {
  console.log("B");
}, 1000);

console.log("C");
```

Output:

```text
A
C
B
```

---

# 🔴 Advanced — 21–30

### 21. What is the difference between `map()`, `filter()`, and `reduce()`?

### `map()`

Creates a new array by transforming each element.

```js
const numbers = [1, 2, 3];

const result = numbers.map(n => n * 2);

console.log(result);
// [2, 4, 6]
```

### `filter()`

Creates a new array containing elements that pass a condition.

```js
const result = numbers.filter(n => n > 1);

// [2, 3]
```

### `reduce()`

Reduces an array to a single accumulated value.

```js
const result = numbers.reduce(
  (total, n) => total + n,
  0
);

// 6
```

---

### 22. What is destructuring?

Destructuring extracts values from arrays or objects.

Object:

```js
const user = {
  name: "Atiar",
  age: 24
};

const { name, age } = user;
```

Array:

```js
const numbers = [10, 20];

const [a, b] = numbers;
```

React-এ props destructuring খুব common:

```jsx
function User({ name, age }) {
  return <h1>{name}</h1>;
}
```

---

### 23. What is the spread operator?

Spread syntax expands elements.

Array:

```js
const a = [1, 2];
const b = [3, 4];

const result = [...a, ...b];

console.log(result);
// [1, 2, 3, 4]
```

Object:

```js
const user = {
  name: "Atiar",
  age: 24
};

const updatedUser = {
  ...user,
  age: 25
};
```

React state updates-এ এটি খুব common।

---

### 24. What is the rest parameter?

Rest syntax collects remaining arguments into an array.

```js
function sum(...numbers) {
  return numbers.reduce(
    (total, n) => total + n,
    0
  );
}

console.log(sum(1, 2, 3, 4));
```

Output:

```text
10
```

**Difference:**

```text
Spread → expands
Rest   → collects
```

---

### 25. What is shallow copy vs deep copy?

**Shallow copy** copies the outer structure, but nested objects can still be shared.

```js
const user = {
  name: "Atiar",
  address: {
    city: "Dhaka"
  }
};

const copy = { ...user };
```

`copy.address` and `user.address` refer to the same nested object.

A deep copy creates independent nested data.

One modern approach for cloneable data is:

```js
const copy = structuredClone(user);
```

---

### 26. What is the difference between `forEach()` and `map()`?

`forEach()` is mainly used for performing an action for each element.

```js
numbers.forEach(n => {
  console.log(n);
});
```

`map()` creates and returns a new array.

```js
const result = numbers.map(n => n * 2);
```

**Interview answer:**

> Use `map()` when I need a transformed array. Use `forEach()` when I simply want to perform an operation for each item.

---

### 27. What is optional chaining?

Optional chaining `?.` safely accesses nested properties when a value may be `null` or `undefined`.

```js
const user = {};

console.log(user.profile?.name);
```

Instead of throwing an error, it returns:

```text
undefined
```

Very common when working with API responses.

---

### 28. What is nullish coalescing (`??`)?

It provides a fallback only when the left side is `null` or `undefined`.

```js
const name = null ?? "Guest";

console.log(name);
// Guest
```

Important difference:

```js
0 || 10   // 10
0 ?? 10   // 0
```

So `??` is useful when `0`, `false`, or `""` are valid values and should not trigger the fallback.

---

### 29. What is debouncing and throttling?

**Debouncing:** waits until events stop occurring for a specified period before running the function.

Common use:

```text
Search input
User types → wait → API request
```

**Throttling:** limits how often a function can run during a period.

Common use:

```text
Scroll
Resize
Mouse movement
```

Simple difference:

> Debounce = run after activity stops.  
> Throttle = run at a limited frequency while activity continues.

---

### 30. What is the difference between shallow equality and deep equality?

**Shallow equality** compares values at the top level.

For objects, references matter:

```js
const a = { name: "Atiar" };
const b = { name: "Atiar" };

console.log(a === b);
// false
```

They contain similar data, but they are different object references.

Deep equality compares nested contents as well.

This concept is important for understanding React rendering, memoization, and state updates.

---

# ⭐ তোমার React/Next.js Interview-এর জন্য Top 15

তুমি যদি **Full Stack Developer interview** দাও, তাহলে JavaScript-এর এই topics-গুলো সবচেয়ে ভালোভাবে practice করো:

```text
1. var / let / const
2. == vs ===
3. Scope
4. Hoisting
5. Closure ⭐
6. this ⭐
7. Arrow Function
8. Callback
9. Promise ⭐
10. async/await ⭐
11. Event Loop ⭐
12. map/filter/reduce
13. Destructuring
14. Spread/Rest
15. Debounce/Throttle
```

বিশেষ করে **Closure + `this` + Promise + async/await + Event Loop** interview-এ code দিয়ে জিজ্ঞেস করা হতে পারে। এগুলো শুধু definition মুখস্থ না করে **output কী হবে এবং কেন হবে**—এভাবে practice করলে অনেক বেশি ভালো হবে।

