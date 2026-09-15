হ্যাঁ। **IndexedDB** প্রথমে একটু complicated মনে হয়, কারণ `localStorage`-এর মতো simple `setItem/getItem` API নেই। কিন্তু flow বুঝে গেলে সহজ।

সবচেয়ে আগে এই mental modelটা ধরো:

```text
IndexedDB
   ↓
Database
   ↓
Object Store
   ↓
Records
```

ধরো আমরা একটা `myAppDB` বানালাম:

```text
myAppDB
   └── users
        ├── { id: 1, name: "Rahim", age: 20 }
        ├── { id: 2, name: "Karim", age: 22 }
        └── { id: 3, name: "Hasan", age: 21 }
```

এখানে `users` হলো **Object Store** — অনেকটা database-এর table-এর মতো।

---

# 1. Database তৈরি / Open করা

```js
const request = indexedDB.open("myAppDB", 1);
```

এখানে:

- `"myAppDB"` → database name
    
- `1` → database version
    

প্রথমবার database তৈরি হলে `onupgradeneeded` চলে।

```js
const request = indexedDB.open("myAppDB", 1);

request.onupgradeneeded = (event) => {
  const db = event.target.result;

  db.createObjectStore("users", {
    keyPath: "id",
    autoIncrement: true
  });
};
```

এখন আমাদের structure:

```text
myAppDB
   └── users
```

`keyPath: "id"` মানে প্রতিটি user-এর `id` key হিসেবে ব্যবহার হবে।

---

# 2. Data Add করা — Create

ধরো:

```js
const user = {
  name: "Rahim",
  age: 20
};
```

প্রথমে database open করতে হবে:

```js
const request = indexedDB.open("myAppDB", 1);

request.onsuccess = (event) => {
  const db = event.target.result;

  const transaction = db.transaction(
    "users",
    "readwrite"
  );

  const store = transaction.objectStore("users");

  store.add({
    name: "Rahim",
    age: 20
  });
};
```

`autoIncrement: true` থাকার কারণে ID automatically হবে:

```js
{
  id: 1,
  name: "Rahim",
  age: 20
}
```

---

# 3. Data Read করা

একটা নির্দিষ্ট user:

```js
const request = indexedDB.open("myAppDB", 1);

request.onsuccess = (event) => {
  const db = event.target.result;

  const transaction = db.transaction("users", "readonly");

  const store = transaction.objectStore("users");

  const request = store.get(1);

  request.onsuccess = () => {
    console.log(request.result);
  };
};
```

Output:

```js
{
  id: 1,
  name: "Rahim",
  age: 20
}
```

---

# 4. সব Data Read করা

```js
const request = indexedDB.open("myAppDB", 1);

request.onsuccess = (event) => {
  const db = event.target.result;

  const transaction = db.transaction("users", "readonly");

  const store = transaction.objectStore("users");

  const request = store.getAll();

  request.onsuccess = () => {
    console.log(request.result);
  };
};
```

Output:

```js
[
  { id: 1, name: "Rahim", age: 20 },
  { id: 2, name: "Karim", age: 22 },
  { id: 3, name: "Hasan", age: 21 }
]
```

---

# 5. Data Update করা

ধরো `id: 1` এর age পরিবর্তন করবো।

```js
const request = indexedDB.open("myAppDB", 1);

request.onsuccess = (event) => {
  const db = event.target.result;

  const transaction = db.transaction(
    "users",
    "readwrite"
  );

  const store = transaction.objectStore("users");

  store.put({
    id: 1,
    name: "Rahim",
    age: 25
  });
};
```

`put()`:

```text
record না থাকলে → add
record থাকলে → update
```

---

# 6. Data Delete করা

```js
const request = indexedDB.open("myAppDB", 1);

request.onsuccess = (event) => {
  const db = event.target.result;

  const transaction = db.transaction(
    "users",
    "readwrite"
  );

  const store = transaction.objectStore("users");

  store.delete(1);
};
```

এতে `id: 1` user delete হবে।

---

# 7. পুরো Object Store clear করা

```js
store.clear();
```

মানে:

```text
users
 ↓
সব records delete
```

---

# CRUD মনে রাখো 🧠

IndexedDB-তে মূল operation:

```text
CREATE
   ↓
store.add()

READ
   ↓
store.get()
store.getAll()

UPDATE
   ↓
store.put()

DELETE
   ↓
store.delete()
```

---

# কিন্তু একটা important জিনিস আছে

IndexedDB-তে সাধারণত এই flow:

```text
indexedDB.open()
       ↓
    Database
       ↓
  transaction
       ↓
 Object Store
       ↓
    operation
```

যেমন:

```js
const transaction = db.transaction(
  "users",
  "readwrite"
);

const store = transaction.objectStore("users");

store.add(user);
```

এখানে `transaction` খুব important।

### `readonly`

শুধু data পড়বে:

```js
db.transaction("users", "readonly");
```

### `readwrite`

Data পরিবর্তন করবে:

```js
db.transaction("users", "readwrite");
```

---

# React-এ কি সরাসরি এভাবে লিখবে?

Technically পারো, কিন্তু raw IndexedDB API অনেক **verbose**।

বাস্তবে React project-এ অনেক developer wrapper library ব্যবহার করে, যেমন **Dexie**।

তখন একই কাজ অনেক সহজ হয়:

```js
import Dexie from "dexie";

const db = new Dexie("myAppDB");

db.version(1).stores({
  users: "++id,name"
});
```

Add:

```js
await db.users.add({
  name: "Rahim",
  age: 20
});
```

Get all:

```js
const users = await db.users.toArray();
```

Update:

```js
await db.users.update(1, {
  age: 25
});
```

Delete:

```js
await db.users.delete(1);
```

এটা অনেক cleaner।

---

## তোমার এখন কোনটা শেখা উচিত?

তুমি যেহেতু React + TanStack Query শিখছো, আমি এই order-টা recommend করবো:

```text
localStorage
     ↓
sessionStorage
     ↓
IndexedDB concept
     ↓
Dexie
     ↓
React + IndexedDB
     ↓
TanStack Query + IndexedDB
```

**Raw IndexedDB-এর CRUD একবার বুঝে নাও**, তারপর Dexie দিয়ে practical কাজ করো। এতে IndexedDB-এর ভিতরের mechanism-টাও বুঝবে, আবার React project-এ অযথা অনেক boilerplate-ও লিখতে হবে না।


----
**Dexie.js** হলো একটা **JavaScript library**, যেটা **IndexedDB ব্যবহার করা অনেক সহজ করে দেয়**।

সহজভাবে:

```text
Raw IndexedDB
     ↓
অনেক boilerplate code 😵

Dexie.js
     ↓
সহজ API 😎
     ↓
IndexedDB
```

### Raw IndexedDB

একটা data add করতেও বেশ কিছু code লাগে:

```js
const transaction = db.transaction("users", "readwrite");

const store = transaction.objectStore("users");

store.add({
  name: "Rahim",
  age: 20
});
```

### Dexie দিয়ে

অনেক সহজ:

```js
await db.users.add({
  name: "Rahim",
  age: 20
});
```

---

### Dexie কী করে?

Dexie নিজে আলাদা database না।

```text
React
  ↓
Dexie.js
  ↓
IndexedDB
  ↓
Browser storage
```

অর্থাৎ **Dexie হলো IndexedDB-এর উপর একটা wrapper/library**।

---

### CRUD খুব সহজ হয়ে যায়

```js
// Create
await db.users.add(user);

// Read
const users = await db.users.toArray();

// Update
await db.users.update(1, {
  name: "Karim"
});

// Delete
await db.users.delete(1);
```

### কখন Dexie use করবে?

যখন তোমার app-এ:

- অনেক local data রাখতে হবে
    
- offline support দরকার
    
- বড়/structured data browser-এ রাখতে হবে
    
- IndexedDB use করতে হবে কিন্তু raw API-এর complexity চাই না
    

তখন **Dexie খুব useful**।

এক লাইনে মনে রাখো:

> **IndexedDB = browser-এর database**  
> **Dexie = IndexedDB সহজে ব্যবহার করার library**


---
# অবশ্যই। 🔥 আমরা একটা **React + Dexie + IndexedDB CRUD Todo App** বানাবো। এতে তুমি practically বুঝবে:

```text
React UI
   ↓
Dexie.js
   ↓
IndexedDB
   ↓
Browser Storage
```

## আমাদের Project-এ যা থাকবে

- ✅ Create — নতুন Todo add
    
- ✅ Read — সব Todo দেখানো
    
- ✅ Update — Todo edit করা
    
- ✅ Delete — Todo delete করা
    
- ✅ Complete/Incomplete
    
- ✅ Search
    
- ✅ React hooks
    
- ✅ Dexie database setup
    
- ✅ পরে চাইলে TanStack Query-এর সাথে integration
    

---

# Step 1 — React Project তৈরি

Vite দিয়ে:

```bash
npm create vite@latest react-dexie-crud
```

তারপর:

```bash
cd react-dexie-crud
npm install
```

Run:

```bash
npm run dev
```

---

# Step 2 — Dexie install

```bash
npm install dexie
```

এখন আমাদের dependency:

```text
React
   +
Dexie
   ↓
IndexedDB
```

---

# Step 3 — Project structure

আমরা এভাবে রাখব:

```text
src/
│
├── db/
│   └── db.js
│
├── components/
│   ├── TodoForm.jsx
│   └── TodoList.jsx
│
├── App.jsx
└── main.jsx
```

শুরুতে বেশি file নিয়ে মাথা ঘামানোর দরকার নেই।

---

# Step 4 — Database তৈরি

`src/db/db.js`

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(1).stores({
  todos: "++id, title, completed"
});
```

এখানে খুব important:

```js
"++id, title, completed"
```

এর মানে:

```text
todos
 ├── id
 ├── title
 └── completed
```

`++id` মানে ID automatically increment হবে।

---

# Step 5 — প্রথম Todo Add করা

এখন `App.jsx`-এ:

```jsx
import { db } from "./db/db";

function App() {

  const addTodo = async () => {
    await db.todos.add({
      title: "Learn Dexie",
      completed: false
    });
  };

  return (
    <div>
      <button onClick={addTodo}>
        Add Todo
      </button>
    </div>
  );
}

export default App;
```

Button click করলে:

```text
Click
 ↓
addTodo()
 ↓
db.todos.add()
 ↓
Dexie
 ↓
IndexedDB
```

Database-এ data হবে:

```js
{
  id: 1,
  title: "Learn Dexie",
  completed: false
}
```

আবার click করলে:

```js
{
  id: 2,
  title: "Learn Dexie",
  completed: false
}
```

---

# Step 6 — Browser থেকে Database দেখবে কীভাবে?

Chrome DevTools খুলে:

```text
Application
   ↓
IndexedDB
   ↓
TodoDB
   ↓
todos
```

এখানে তোমার data দেখতে পাবে।

এটা দেখলে IndexedDB ব্যাপারটা অনেক পরিষ্কার হয়ে যাবে। 😎

---

# Step 7 — Data Read করা

এখন database থেকে সব Todo আনবো।

Dexie:

```js
const todos = await db.todos.toArray();
```

কিন্তু React-এর একটা problem আছে।

শুধু:

```js
const todos = await db.todos.toArray();
```

করলেই UI automatically update হবে না।

তাই React state ব্যবহার করতে পারি:

```jsx
import { useEffect, useState } from "react";
import { db } from "./db/db";

function App() {
  const [todos, setTodos] = useState([]);

  const loadTodos = async () => {
    const data = await db.todos.toArray();
    setTodos(data);
  };

  useEffect(() => {
    loadTodos();
  }, []);

  return (
    <div>
      {todos.map((todo) => (
        <p key={todo.id}>
          {todo.title}
        </p>
      ))}
    </div>
  );
}

export default App;
```

এখন:

```text
IndexedDB
   ↓
Dexie
   ↓
toArray()
   ↓
setTodos()
   ↓
React re-render
   ↓
UI
```

---

# Step 8 — Create পুরোপুরি করা

এখন একটা input বানাই:

```jsx
import { useEffect, useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");
  const [todos, setTodos] = useState([]);

  const loadTodos = async () => {
    const data = await db.todos.toArray();
    setTodos(data);
  };

  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title,
      completed: false
    });

    setTitle("");

    await loadTodos();
  };

  useEffect(() => {
    loadTodos();
  }, []);

  return (
    <div>
      <h1>Todo App</h1>

      <form onSubmit={addTodo}>
        <input
          value={title}
          onChange={(e) => setTitle(e.target.value)}
          placeholder="Enter todo"
        />

        <button type="submit">
          Add
        </button>
      </form>

      {todos.map((todo) => (
        <div key={todo.id}>
          {todo.title}
        </div>
      ))}
    </div>
  );
}

export default App;
```

এখন আমাদের **Create + Read** হয়ে গেছে। ✅

---

# Step 9 — Update

ধরো Todo complete করলে:

```js
const toggleTodo = async (id, completed) => {
  await db.todos.update(id, {
    completed: !completed
  });

  await loadTodos();
};
```

UI:

```jsx
{todos.map((todo) => (
  <div key={todo.id}>

    <input
      type="checkbox"
      checked={todo.completed}
      onChange={() =>
        toggleTodo(todo.id, todo.completed)
      }
    />

    {todo.title}

  </div>
))}
```

এখন:

```text
Checkbox click
     ↓
toggleTodo()
     ↓
db.todos.update()
     ↓
IndexedDB update
     ↓
loadTodos()
     ↓
React state update
```

---

# Step 10 — Delete

```js
const deleteTodo = async (id) => {
  await db.todos.delete(id);

  await loadTodos();
};
```

UI:

```jsx
<button onClick={() => deleteTodo(todo.id)}>
  Delete
</button>
```

ব্যস। Delete complete. ✅

---

# এখন আমাদের CRUD

```text
CREATE
db.todos.add()
       ↓
READ
db.todos.toArray()
       ↓
UPDATE
db.todos.update()
       ↓
DELETE
db.todos.delete()
```

এটাই **Dexie CRUD-এর core**। 🧠

---

## কিন্তু একটা জিনিস খেয়াল করো

এখন পর্যন্ত আমরা:

```text
React State
     +
Dexie
     ↓
IndexedDB
```

ব্যবহার করছি।

পরে আমরা এটাকে আরও professional করবো:

```text
React
  ↓
Custom Hooks
  ↓
Dexie
  ↓
IndexedDB
```

তারপর চাইলে:

```text
React
  ↓
TanStack Query
  ↓
Dexie
  ↓
IndexedDB
```

এবং শেষে **online + offline CRUD app** বানাতে পারি।

### আমাদের শেখার roadmap

```text
Part 1 → Dexie setup              ✅
Part 2 → Create + Read            ← এখন
Part 3 → Update
Part 4 → Delete
Part 5 → Edit Form
Part 6 → Search / Filter
Part 7 → Pagination
Part 8 → Dexie React hooks
Part 9 → Offline-first
Part 10 → TanStack Query + Dexie
```

**পরের ধাপে সবচেয়ে ভালো হবে `useLiveQuery()` শেখা**, কারণ তখন database-এর data পরিবর্তন হলে manually `loadTodos()` call না করেও React UI automatically update করতে পারবে।

----
# চলো **Part 2: Create + Read** ভালোভাবে করি। 🔥

আমরা একটা ছোট Todo app বানাবো যেখানে:

- **Create:** Todo add হবে IndexedDB-তে
    
- **Read:** IndexedDB থেকে Todo নিয়ে UI-তে দেখাবে
    

---

## 1. Database setup

`src/db/db.js`

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(1).stores({
  todos: "++id, title, completed"
});
```

এখানে:

```js
todos: "++id, title, completed"
```

মানে আমাদের `todos` object store-এ থাকবে:

```js
{
  id: 1,
  title: "Learn React",
  completed: false
}
```

---

# 2. App.jsx

এখন পুরো Create + Read:

```jsx
import { useEffect, useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");
  const [todos, setTodos] = useState([]);

  // READ
  const loadTodos = async () => {
    const data = await db.todos.toArray();

    setTodos(data);
  };

  // CREATE
  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title,
      completed: false
    });

    setTitle("");

    // নতুন data আসার পর আবার read
    loadTodos();
  };

  // App load হলে database থেকে data আনবে
  useEffect(() => {
    loadTodos();
  }, []);

  return (
    <div>
      <h1>Todo App</h1>

      <form onSubmit={addTodo}>
        <input
          type="text"
          placeholder="Enter todo"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />

        <button type="submit">
          Add Todo
        </button>
      </form>

      <hr />

      <h2>Todo List</h2>

      {todos.map((todo) => (
        <div key={todo.id}>
          <span>{todo.title}</span>
        </div>
      ))}
    </div>
  );
}

export default App;
```

---

# 3. এখন flow-টা বুঝো

তুমি যখন লিখবে:

```text
Learn Dexie
```

তারপর **Add Todo** চাপবে।

এটা যাবে:

```text
Input
  ↓
title state
  ↓
addTodo()
  ↓
db.todos.add()
  ↓
IndexedDB
```

Database-এ:

```js
{
  id: 1,
  title: "Learn Dexie",
  completed: false
}
```

---

# 4. তারপর Read হচ্ছে কীভাবে?

আমরা লিখেছি:

```js
const loadTodos = async () => {
  const data = await db.todos.toArray();

  setTodos(data);
};
```

`db.todos.toArray()` database-এর **সব Todo নিয়ে আসে**।

ধরো database-এ:

```js
[
  {
    id: 1,
    title: "Learn React",
    completed: false
  },
  {
    id: 2,
    title: "Learn Dexie",
    completed: false
  }
]
```

তাহলে:

```js
const data = await db.todos.toArray();
```

এর পরে `data` হবে:

```js
[
  {
    id: 1,
    title: "Learn React",
    completed: false
  },
  {
    id: 2,
    title: "Learn Dexie",
    completed: false
  }
]
```

তারপর:

```js
setTodos(data);
```

React state-এ data চলে যাবে।

---

# 5. `map()` দিয়ে UI

```jsx
{todos.map((todo) => (
  <div key={todo.id}>
    {todo.title}
  </div>
))}
```

যদি:

```js
todos = [
  { id: 1, title: "Learn React" },
  { id: 2, title: "Learn Dexie" }
];
```

তাহলে UI:

```text
Learn React
Learn Dexie
```

---

# 6. `useEffect` কেন?

```js
useEffect(() => {
  loadTodos();
}, []);
```

এর মানে component প্রথমবার load হলে:

```text
React App Start
      ↓
useEffect()
      ↓
loadTodos()
      ↓
IndexedDB
      ↓
todos
      ↓
UI
```

তাই browser refresh করলেও database-এর পুরনো Todo আবার UI-তে চলে আসবে।

এটাই IndexedDB-এর একটা বড় সুবিধা।

---

# 7. গুরুত্বপূর্ণ difference

এখানে:

```js
await db.todos.add(...)
```

**database-এ data save করছে।**

আর:

```js
setTodos(data)
```

**React UI update করছে।**

দুটো আলাদা জিনিস:

```text
              ┌──→ IndexedDB
              │
db.todos.add()
              │
              └──→ Database-এ save


setTodos()
   ↓
React state
   ↓
UI update
```

---

## 🔥 এখন একটা challenge

নিজে এই তিনটা Todo add করো:

```text
Learn React
Learn Dexie
Build CRUD App
```

তারপর Chrome DevTools:

```text
Application
 → IndexedDB
   → TodoDB
     → todos
```

এ গিয়ে দেখো data সত্যিই database-এ আছে কিনা।

**Part 3-এ আমরা Update + Delete করব**, অর্থাৎ Todo-তে checkbox দিয়ে complete করা এবং Delete button দিয়ে database থেকে permanently remove করা।

----
# চলো 🔥 **Part 3: Update + Delete** করি।

Part 2-তে আমরা করেছি:

```text
Create → db.todos.add()
Read   → db.todos.toArray()
```

এখন করবো:

```text
Update → db.todos.update()
Delete → db.todos.delete()
```

---

# 1. Update — Todo Complete/Incomplete

ধরো database-এ আছে:

```js
{
  id: 1,
  title: "Learn Dexie",
  completed: false
}
```

Checkbox click করলে আমরা `completed` পরিবর্তন করবো।

### Function:

```js
const toggleTodo = async (id, completed) => {
  await db.todos.update(id, {
    completed: !completed
  });

  loadTodos();
};
```

এখানে:

```js
completed: !completed
```

যদি:

```text
false → true
```

আর যদি:

```text
true → false
```

---

# 2. UI-তে Checkbox

`todos.map()` এর মধ্যে:

```jsx
{todos.map((todo) => (
  <div key={todo.id}>

    <input
      type="checkbox"
      checked={todo.completed}
      onChange={() =>
        toggleTodo(todo.id, todo.completed)
      }
    />

    <span>
      {todo.title}
    </span>

  </div>
))}
```

এখন checkbox click করলে:

```text
Checkbox
   ↓
toggleTodo()
   ↓
db.todos.update()
   ↓
IndexedDB
   ↓
loadTodos()
   ↓
setTodos()
   ↓
UI
```

---

# 3. Delete

এবার Todo delete করি।

Function:

```js
const deleteTodo = async (id) => {
  await db.todos.delete(id);

  loadTodos();
};
```

এখানে `id` দিয়ে নির্দিষ্ট record delete হচ্ছে।

---

# 4. Delete Button

Todo-এর পাশে:

```jsx
{todos.map((todo) => (
  <div key={todo.id}>

    <input
      type="checkbox"
      checked={todo.completed}
      onChange={() =>
        toggleTodo(todo.id, todo.completed)
      }
    />

    <span>
      {todo.title}
    </span>

    <button
      onClick={() => deleteTodo(todo.id)}
    >
      Delete
    </button>

  </div>
))}
```

এখন:

```text
Learn React    ☑    Delete
Learn Dexie    ☐    Delete
Build CRUD     ☐    Delete
```

Delete চাপলে সেই Todo IndexedDB থেকেও delete হবে।

---

# 5. পুরো `App.jsx`

এখন Part 2 + Part 3 একসাথে:

```jsx
import { useEffect, useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");
  const [todos, setTodos] = useState([]);

  // READ
  const loadTodos = async () => {
    const data = await db.todos.toArray();

    setTodos(data);
  };

  // CREATE
  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title,
      completed: false
    });

    setTitle("");

    loadTodos();
  };

  // UPDATE
  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed
    });

    loadTodos();
  };

  // DELETE
  const deleteTodo = async (id) => {
    await db.todos.delete(id);

    loadTodos();
  };

  // প্রথমবার database থেকে data load
  useEffect(() => {
    loadTodos();
  }, []);

  return (
    <div>
      <h1>Todo App</h1>

      {/* CREATE */}
      <form onSubmit={addTodo}>
        <input
          type="text"
          placeholder="Enter todo"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />

        <button type="submit">
          Add Todo
        </button>
      </form>

      <hr />

      <h2>Todo List</h2>

      {/* READ */}
      {todos.map((todo) => (
        <div key={todo.id}>

          {/* UPDATE */}
          <input
            type="checkbox"
            checked={todo.completed}
            onChange={() =>
              toggleTodo(todo.id, todo.completed)
            }
          />

          <span
            style={{
              textDecoration: todo.completed
                ? "line-through"
                : "none"
            }}
          >
            {todo.title}
          </span>

          {/* DELETE */}
          <button
            onClick={() => deleteTodo(todo.id)}
          >
            Delete
          </button>

        </div>
      ))}
    </div>
  );
}

export default App;
```

---

# 6. এখন পুরো CRUD বুঝো 🧠

```text
                React
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      CREATE     UPDATE    DELETE
        ↓         ↓         ↓
      add()     update()  delete()
        │         │         │
        └─────────┼─────────┘
                  ↓
               Dexie
                  ↓
              IndexedDB
```

আর Read:

```js
db.todos.toArray()
```

---

## CRUD Cheat Sheet

|কাজ|Dexie|
|---|---|
|Create|`db.todos.add()`|
|Read one|`db.todos.get(id)`|
|Read all|`db.todos.toArray()`|
|Update|`db.todos.update(id, data)`|
|Delete|`db.todos.delete(id)`|
|Delete all|`db.todos.clear()`|

---

### একটা গুরুত্বপূর্ণ বিষয়

আমাদের current code-এ update/delete করার পরে:

```js
loadTodos();
```

ম্যানুয়ালি আবার database থেকে data আনছি।

এটা কাজ করে, কিন্তু **Dexie-এর আরও সুন্দর একটা feature আছে — `useLiveQuery()`**।

ওটা ব্যবহার করলে:

```text
IndexedDB পরিবর্তন
      ↓
Dexie detect করবে
      ↓
React automatically re-render
```

তখন আর প্রতিবার `loadTodos()` manually call করতে হবে না।

**Part 4-এ আমরা `useLiveQuery()` দিয়ে এই CRUD-টাকে আরও clean এবং reactive করবো।**

---
# চলো 🔥 **Part 4: `useLiveQuery()`** করি।

এটা Dexie শেখার একটা **খুব important step**, কারণ এখন আর প্রত্যেক `add/update/delete`-এর পরে manually `loadTodos()` call করতে হবে না।

## 1. `useLiveQuery()` কী?

আগের code-এ আমাদের করতে হতো:

```js
await db.todos.add(todo);

loadTodos();
```

Update:

```js
await db.todos.update(id, data);

loadTodos();
```

Delete:

```js
await db.todos.delete(id);

loadTodos();
```

`useLiveQuery()` ব্যবহার করলে Dexie নিজেই database changes observe করবে।

```text
IndexedDB change
      ↓
    Dexie
      ↓
useLiveQuery()
      ↓
React re-render
      ↓
UI update
```

---

# 2. Install package

Dexie install করা থাকলে শুধু:

```bash
npm install dexie
```

`useLiveQuery` আসে:

```js
import { useLiveQuery } from "dexie-react-hooks";
```

তাই এটাও install করো:

```bash
npm install dexie-react-hooks
```

---

# 3. `loadTodos()` আর লাগবে না

আগে ছিল:

```js
const [todos, setTodos] = useState([]);

const loadTodos = async () => {
  const data = await db.todos.toArray();
  setTodos(data);
};

useEffect(() => {
  loadTodos();
}, []);
```

এগুলো এখন remove করতে পারো।

তার বদলে:

```js
const todos = useLiveQuery(
  () => db.todos.toArray(),
  []
);
```

এখন `todos` database-এর সাথে reactive হয়ে গেল।

---

# 4. Complete App.jsx

```jsx
import { useLiveQuery } from "dexie-react-hooks";
import { useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");

  // READ
  const todos = useLiveQuery(
    () => db.todos.toArray(),
    []
  );

  // CREATE
  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title.trim(),
      completed: false
    });

    setTitle("");
  };

  // UPDATE
  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed
    });
  };

  // DELETE
  const deleteTodo = async (id) => {
    await db.todos.delete(id);
  };

  return (
    <div>
      <h1>Todo App</h1>

      {/* CREATE */}
      <form onSubmit={addTodo}>
        <input
          type="text"
          placeholder="Enter todo"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />

        <button type="submit">
          Add Todo
        </button>
      </form>

      <hr />

      <h2>Todo List</h2>

      {/* Loading */}
      {!todos && <p>Loading...</p>}

      {/* READ */}
      {todos?.map((todo) => (
        <div key={todo.id}>

          {/* UPDATE */}
          <input
            type="checkbox"
            checked={todo.completed}
            onChange={() =>
              toggleTodo(
                todo.id,
                todo.completed
              )
            }
          />

          <span
            style={{
              textDecoration: todo.completed
                ? "line-through"
                : "none"
            }}
          >
            {todo.title}
          </span>

          {/* DELETE */}
          <button
            onClick={() => deleteTodo(todo.id)}
          >
            Delete
          </button>

        </div>
      ))}
    </div>
  );
}

export default App;
```

---

# 5. সবচেয়ে important পরিবর্তনটা দেখো

### আগে

```js
await db.todos.add(todo);

loadTodos();
```

### এখন

```js
await db.todos.add(todo);
```

**এইটুকুই।** 😎

কারণ:

```js
const todos = useLiveQuery(
  () => db.todos.toArray(),
  []
);
```

database change detect করে automatically নতুন data নিয়ে আসবে।

---

# 6. Update-এর ক্ষেত্রেও

আগে:

```js
const toggleTodo = async (id, completed) => {
  await db.todos.update(id, {
    completed: !completed
  });

  loadTodos();
};
```

এখন:

```js
const toggleTodo = async (id, completed) => {
  await db.todos.update(id, {
    completed: !completed
  });
};
```

`loadTodos()` নেই। 🔥

---

# 7. Delete-এর ক্ষেত্রেও

আগে:

```js
const deleteTodo = async (id) => {
  await db.todos.delete(id);

  loadTodos();
};
```

এখন:

```js
const deleteTodo = async (id) => {
  await db.todos.delete(id);
};
```

---

# 8. কেন automatic হচ্ছে?

ধরো বর্তমানে database:

```text
todos
├── 1 Learn React
├── 2 Learn Dexie
└── 3 Build CRUD
```

`useLiveQuery()` এটা observe করছে:

```js
useLiveQuery(
  () => db.todos.toArray(),
  []
);
```

এখন তুমি:

```js
await db.todos.delete(2);
```

করলে:

```text
Before
  ↓
1 Learn React
2 Learn Dexie
3 Build CRUD

      ↓ delete(2)

IndexedDB changed
      ↓
Dexie detects change
      ↓
useLiveQuery runs again
      ↓
React re-renders
      ↓

After
  ↓
1 Learn React
3 Build CRUD
```

তোমাকে `setTodos()` বা `loadTodos()` কিছুই করতে হচ্ছে না।

---

# 9. `useLiveQuery()`-এর basic syntax

মনে রাখো:

```js
const data = useLiveQuery(
  () => database operation,
  dependencies
);
```

আমাদের:

```js
const todos = useLiveQuery(
  () => db.todos.toArray(),
  []
);
```

একটা নির্দিষ্ট Todo:

```js
const todo = useLiveQuery(
  () => db.todos.get(id),
  [id]
);
```

Search-এর মতো query-ও করা যায়:

```js
const todos = useLiveQuery(
  () =>
    db.todos
      .where("completed")
      .equals(false)
      .toArray(),
  []
);
```

---

# 🧠 এখন পুরো architecture

আমাদের আগের approach:

```text
React
  ↓
db.add()
  ↓
IndexedDB

তারপর
  ↓
loadTodos()
  ↓
setTodos()
  ↓
React
```

`useLiveQuery()` approach:

```text
React
  ↓
useLiveQuery()
  ↓
Dexie
  ↓
IndexedDB
  ↑
  │
  └── changes automatically detected
          ↓
       React update
```

এটাই `useLiveQuery()`-এর main power। 💪

---

## Part 4 শেষে তোমার CRUD এখন এমন

```text
CREATE
db.todos.add()
       ↓
automatic UI update


READ
useLiveQuery()
       ↓
automatic


UPDATE
db.todos.update()
       ↓
automatic UI update


DELETE
db.todos.delete()
       ↓
automatic UI update
```

**Part 5-এ আমরা এটাকে আরও real-world করব: Edit button + Edit form + Update title**, অর্থাৎ checkbox দিয়ে শুধু `completed` update না করে পুরো Todo edit করা।


----
# চলো 🔥 **Part 5: Edit Todo + Update Title** করি।

এখন পর্যন্ত আমাদের CRUD:

```text
Create → Add Todo
Read   → useLiveQuery()
Update → Complete/Incomplete
Delete → Delete Todo
```

এবার Update-এর আরেকটা practical use করবো:

> **Edit button → Input-এ পুরনো title → পরিবর্তন → Save → IndexedDB update**

---

# 1. Edit করার জন্য state

`App.jsx`-এ নতুন state:

```jsx
const [editId, setEditId] = useState(null);
const [editTitle, setEditTitle] = useState("");
```

এখানে:

```text
editId
→ কোন Todo edit হচ্ছে?

editTitle
→ নতুন title কী হবে?
```

---

# 2. Edit button click

একটা function:

```jsx
const startEdit = (todo) => {
  setEditId(todo.id);
  setEditTitle(todo.title);
};
```

ধরো Todo:

```js
{
  id: 1,
  title: "Learn React",
  completed: false
}
```

Edit click করলে:

```text
editId = 1
editTitle = "Learn React"
```

---

# 3. Update function

এখন Save করলে database update করবো:

```jsx
const updateTodo = async (e) => {
  e.preventDefault();

  if (!editTitle.trim()) return;

  await db.todos.update(editId, {
    title: editTitle.trim()
  });

  setEditId(null);
  setEditTitle("");
};
```

খেয়াল করো:

```js
db.todos.update(editId, {
  title: editTitle
});
```

এখানে শুধু `title` update করছি।

---

# 4. `useLiveQuery()` থাকার কারণে

Update করার পর আমাদের:

```js
loadTodos();
```

লাগছে না। 😎

কারণ:

```text
db.todos.update()
       ↓
IndexedDB changes
       ↓
Dexie detects
       ↓
useLiveQuery()
       ↓
React re-render
       ↓
UI updated
```

---

# 5. UI-তে Edit button

Todo-এর পাশে:

```jsx
<button onClick={() => startEdit(todo)}>
  Edit
</button>
```

এখন:

```text
Learn React    Edit    Delete
Learn Dexie    Edit    Delete
```

---

# 6. Edit mode দেখানো

এখন যদি `editId === todo.id` হয়, তাহলে input দেখাবো।

```jsx
{todos?.map((todo) => (
  <div key={todo.id}>

    {editId === todo.id ? (
      <>
        <input
          value={editTitle}
          onChange={(e) =>
            setEditTitle(e.target.value)
          }
        />

        <button onClick={updateTodo}>
          Save
        </button>

        <button
          onClick={() => {
            setEditId(null);
            setEditTitle("");
          }}
        >
          Cancel
        </button>
      </>
    ) : (
      <>
        <span>{todo.title}</span>

        <button
          onClick={() => startEdit(todo)}
        >
          Edit
        </button>
      </>
    )}

  </div>
))}
```

---

# 7. Complete `App.jsx`

এখন সবকিছু একসাথে:

```jsx
import { useLiveQuery } from "dexie-react-hooks";
import { useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");

  const [editId, setEditId] = useState(null);
  const [editTitle, setEditTitle] = useState("");

  // READ
  const todos = useLiveQuery(
    () => db.todos.toArray(),
    []
  );

  // CREATE
  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title.trim(),
      completed: false
    });

    setTitle("");
  };

  // UPDATE COMPLETED
  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed
    });
  };

  // START EDIT
  const startEdit = (todo) => {
    setEditId(todo.id);
    setEditTitle(todo.title);
  };

  // UPDATE TITLE
  const updateTodo = async (e) => {
    e.preventDefault();

    if (!editTitle.trim()) return;

    await db.todos.update(editId, {
      title: editTitle.trim()
    });

    setEditId(null);
    setEditTitle("");
  };

  // DELETE
  const deleteTodo = async (id) => {
    await db.todos.delete(id);
  };

  return (
    <div>
      <h1>Todo App</h1>

      {/* CREATE */}
      <form onSubmit={addTodo}>
        <input
          type="text"
          placeholder="Enter todo"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
        />

        <button type="submit">
          Add Todo
        </button>
      </form>

      <hr />

      <h2>Todo List</h2>

      {!todos && <p>Loading...</p>}

      {todos?.map((todo) => (
        <div key={todo.id}>

          {editId === todo.id ? (
            /* EDIT MODE */
            <>
              <input
                value={editTitle}
                onChange={(e) =>
                  setEditTitle(e.target.value)
                }
              />

              <button onClick={updateTodo}>
                Save
              </button>

              <button
                onClick={() => {
                  setEditId(null);
                  setEditTitle("");
                }}
              >
                Cancel
              </button>
            </>
          ) : (
            /* NORMAL MODE */
            <>
              <input
                type="checkbox"
                checked={todo.completed}
                onChange={() =>
                  toggleTodo(
                    todo.id,
                    todo.completed
                  )
                }
              />

              <span
                style={{
                  textDecoration:
                    todo.completed
                      ? "line-through"
                      : "none"
                }}
              >
                {todo.title}
              </span>

              <button
                onClick={() => startEdit(todo)}
              >
                Edit
              </button>

              <button
                onClick={() =>
                  deleteTodo(todo.id)
                }
              >
                Delete
              </button>
            </>
          )}

        </div>
      ))}
    </div>
  );
}

export default App;
```

---

# 8. এখন Edit flow বুঝো 🧠

ধরো:

```text
Learn React
```

Edit চাপলে:

```text
Edit
 ↓
startEdit(todo)
 ↓
editId = 1
editTitle = "Learn React"
 ↓
React UI edit mode
```

তুমি পরিবর্তন করলে:

```text
Learn React
     ↓
Learn React + Dexie
```

Save:

```text
Save
 ↓
updateTodo()
 ↓
db.todos.update(1, {
   title: "Learn React + Dexie"
 })
 ↓
IndexedDB
 ↓
useLiveQuery()
 ↓
UI automatically update
```

---

# 9. `update()` খুব ভালোভাবে বুঝে রাখো

আমাদের database:

```js
{
  id: 1,
  title: "Learn React",
  completed: false
}
```

যদি:

```js
await db.todos.update(1, {
  title: "Learn React + Dexie"
});
```

দিই, তাহলে হবে:

```js
{
  id: 1,
  title: "Learn React + Dexie",
  completed: false
}
```

শুধু `title` change হয়েছে।

আর:

```js
await db.todos.update(1, {
  completed: true
});
```

দিলে:

```js
{
  id: 1,
  title: "Learn React + Dexie",
  completed: true
}
```

অর্থাৎ `update()`-এ **যে field পাঠাবে, সেই field update হবে**।

---

## 🔥 Part 5-এর মূল শিক্ষা

```text
Edit Button
    ↓
editId + editTitle
    ↓
User changes input
    ↓
db.todos.update()
    ↓
IndexedDB
    ↓
useLiveQuery()
    ↓
Automatic UI update
```

এখন তোমার Todo app-এ **full CRUD** practically complete:

```text
CREATE  → add()
READ    → useLiveQuery()
UPDATE  → update()
DELETE  → delete()
```

**Part 6-এ Search + Filter বানালে** তুমি Dexie দিয়ে database থেকে শুধু প্রয়োজনীয় records বের করা শিখবে—যেমন `completed = false`, title search ইত্যাদি।


---
# চলো 🔥 **Part 6: Search + Filter with Dexie** করি।

এখন আমাদের app পারে:

```text
Create → add()
Read   → useLiveQuery()
Update → update()
Delete → delete()
```

এবার আমরা করবো:

```text
🔎 Search
☑️ Completed filter
📋 All filter
```

---

# 1. Search-এর জন্য state

`App.jsx`-এ:

```jsx
const [search, setSearch] = useState("");
```

এটা user কী search করছে সেটা রাখবে।

আর filter-এর জন্য:

```jsx
const [filter, setFilter] = useState("all");
```

তাহলে:

```text
filter = "all"
filter = "active"
filter = "completed"
```

---

# 2. Search input

```jsx
<input
  type="text"
  placeholder="Search todo..."
  value={search}
  onChange={(e) => setSearch(e.target.value)}
/>
```

---

# 3. Filter buttons

```jsx
<div>
  <button onClick={() => setFilter("all")}>
    All
  </button>

  <button onClick={() => setFilter("active")}>
    Active
  </button>

  <button onClick={() => setFilter("completed")}>
    Completed
  </button>
</div>
```

UI হবে:

```text
[ Search todo........ ]

[ All ] [ Active ] [ Completed ]
```

---

# 4. এখন আসল Dexie query

এখানে `useLiveQuery()` একটু change করবো।

```jsx
const todos = useLiveQuery(
  async () => {
    let data = await db.todos.toArray();

    return data;
  },
  []
);
```

কিন্তু search/filter-এর state query-এর মধ্যে ব্যবহার করতে হবে।

```jsx
const todos = useLiveQuery(
  async () => {
    let data = await db.todos.toArray();

    // Search
    if (search.trim()) {
      data = data.filter((todo) =>
        todo.title
          .toLowerCase()
          .includes(search.toLowerCase())
      );
    }

    // Filter
    if (filter === "active") {
      data = data.filter(
        (todo) => !todo.completed
      );
    }

    if (filter === "completed") {
      data = data.filter(
        (todo) => todo.completed
      );
    }

    return data;
  },
  [search, filter]
);
```

খেয়াল করো:

```js
[search, filter]
```

এগুলো dependency।

Search বা filter change হলে query আবার run হবে।

---

# 5. পুরো flow

ধরো database:

```text
Learn React       ❌
Learn Dexie       ❌
Build CRUD App    ✅
Learn JavaScript  ❌
```

Search:

```text
search = "learn"
```

তাহলে:

```text
Learn React
Learn Dexie
Learn JavaScript
```

দেখাবে।

---

## Completed filter

যদি:

```js
filter = "completed"
```

তাহলে:

```text
Build CRUD App    ✅
```

শুধু এটা দেখাবে।

---

## Active filter

যদি:

```js
filter = "active"
```

তাহলে:

```text
Learn React       ❌
Learn Dexie       ❌
Learn JavaScript  ❌
```

দেখাবে।

---

# 6. কিন্তু এখানে একটা গুরুত্বপূর্ণ বিষয়

উপরের code:

```js
await db.todos.toArray();
```

প্রথমে **সব data browser-এ নিয়ে আসে**।

তারপর JavaScript:

```js
data.filter(...)
```

দিয়ে filtering করে।

ছোট Todo app-এর জন্য এটা ঠিক আছে। 👍

কিন্তু database যদি অনেক বড় হয়:

```text
100,000 records
```

তাহলে সব records এনে তারপর filter করা inefficient হতে পারে।

তখন Dexie-এর database query ব্যবহার করা ভালো।

---

# 7. Dexie দিয়ে Completed query

যেমন শুধু incomplete Todo চাই:

```js
const todos = useLiveQuery(
  () =>
    db.todos
      .where("completed")
      .equals(false)
      .toArray(),
  []
);
```

এখানে:

```text
db.todos
   ↓
where("completed")
   ↓
equals(false)
   ↓
toArray()
```

---

# 8. তবে Search একটু আলাদা

আমাদের schema:

```js
db.version(1).stores({
  todos: "++id, title, completed"
});
```

এখানে `title` indexed field।

তবে সাধারণ partial search:

```text
"react"
```

এর মধ্যে:

```text
"Learn React"
```

খোঁজার জন্য `filter()` বা Dexie-এর appropriate text-search approach ব্যবহার করা যায়।

Beginner হিসেবে আগে:

```js
const todos = useLiveQuery(
  async () => {
    let data = await db.todos.toArray();

    if (search.trim()) {
      data = data.filter((todo) =>
        todo.title
          .toLowerCase()
          .includes(search.toLowerCase())
      );
    }

    return data;
  },
  [search]
);
```

এটাই বুঝে নাও।

---

# 9. Complete `App.jsx`

এখন আমাদের Part 1–6-এর গুরুত্বপূর্ণ অংশ একসাথে:

```jsx
import { useLiveQuery } from "dexie-react-hooks";
import { useState } from "react";
import { db } from "./db/db";

function App() {
  const [title, setTitle] = useState("");

  const [editId, setEditId] = useState(null);
  const [editTitle, setEditTitle] = useState("");

  const [search, setSearch] = useState("");
  const [filter, setFilter] = useState("all");

  // READ + SEARCH + FILTER
  const todos = useLiveQuery(
    async () => {
      let data = await db.todos.toArray();

      // SEARCH
      if (search.trim()) {
        data = data.filter((todo) =>
          todo.title
            .toLowerCase()
            .includes(search.toLowerCase())
        );
      }

      // FILTER
      if (filter === "active") {
        data = data.filter(
          (todo) => !todo.completed
        );
      }

      if (filter === "completed") {
        data = data.filter(
          (todo) => todo.completed
        );
      }

      return data;
    },
    [search, filter]
  );

  // CREATE
  const addTodo = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await db.todos.add({
      title: title.trim(),
      completed: false
    });

    setTitle("");
  };

  // UPDATE COMPLETED
  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed
    });
  };

  // START EDIT
  const startEdit = (todo) => {
    setEditId(todo.id);
    setEditTitle(todo.title);
  };

  // UPDATE TITLE
  const updateTodo = async (e) => {
    e.preventDefault();

    if (!editTitle.trim()) return;

    await db.todos.update(editId, {
      title: editTitle.trim()
    });

    setEditId(null);
    setEditTitle("");
  };

  // DELETE
  const deleteTodo = async (id) => {
    await db.todos.delete(id);
  };

  return (
    <div>
      <h1>Todo App</h1>

      {/* CREATE */}
      <form onSubmit={addTodo}>
        <input
          type="text"
          placeholder="Enter todo"
          value={title}
          onChange={(e) =>
            setTitle(e.target.value)
          }
        />

        <button type="submit">
          Add Todo
        </button>
      </form>

      <hr />

      {/* SEARCH */}
      <input
        type="text"
        placeholder="Search todo..."
        value={search}
        onChange={(e) =>
          setSearch(e.target.value)
        }
      />

      {/* FILTER */}
      <div>
        <button
          onClick={() => setFilter("all")}
        >
          All
        </button>

        <button
          onClick={() => setFilter("active")}
        >
          Active
        </button>

        <button
          onClick={() => setFilter("completed")}
        >
          Completed
        </button>
      </div>

      <hr />

      {/* TODO LIST */}
      {!todos && <p>Loading...</p>}

      {todos?.map((todo) => (
        <div key={todo.id}>
          {editId === todo.id ? (
            <>
              <input
                value={editTitle}
                onChange={(e) =>
                  setEditTitle(e.target.value)
                }
              />

              <button onClick={updateTodo}>
                Save
              </button>

              <button
                onClick={() => {
                  setEditId(null);
                  setEditTitle("");
                }}
              >
                Cancel
              </button>
            </>
          ) : (
            <>
              <input
                type="checkbox"
                checked={todo.completed}
                onChange={() =>
                  toggleTodo(
                    todo.id,
                    todo.completed
                  )
                }
              />

              <span
                style={{
                  textDecoration:
                    todo.completed
                      ? "line-through"
                      : "none"
                }}
              >
                {todo.title}
              </span>

              <button
                onClick={() =>
                  startEdit(todo)
                }
              >
                Edit
              </button>

              <button
                onClick={() =>
                  deleteTodo(todo.id)
                }
              >
                Delete
              </button>
            </>
          )}
        </div>
      ))}
    </div>
  );
}

export default App;
```

---

# 🧠 Part 6-এর সবচেয়ে important concept

এখন তুমি বুঝলে যে Dexie শুধু:

```js
add()
get()
update()
delete()
```

এর জন্য না।

তুমি database-এর data **query**-ও করতে পারো।

```text
Dexie
 │
 ├── add()
 ├── get()
 ├── update()
 ├── delete()
 │
 └── Query
      ├── where()
      ├── equals()
      ├── filter()
      ├── toArray()
      └── ...
```

আর `useLiveQuery()` থাকার কারণে query-এর result-ও reactive থাকে।

### এখন পর্যন্ত আমাদের architecture:

```text
React
 │
 ├── Create
 ├── Search
 ├── Filter
 ├── Edit
 └── Delete
       ↓
   Dexie.js
       ↓
   IndexedDB
```

**Part 7-এ Pagination + Sorting করবো** — যেমন `Newest first`, `Oldest first`, প্রতি page-এ 5টা Todo ইত্যাদি।

----
# চলো 🔥 **Part 7: Pagination + Sorting with Dexie** করি।

এখন আমাদের Todo app পারে:

```text
Create
Read
Update
Delete
Search
Filter
```

এবার শিখবো:

```text
📄 Pagination
↕️ Sorting
```

---

# 1. Pagination কী?

ধরো database-এ 100টা Todo আছে।

সব একসাথে দেখালে:

```text
Todo 1
Todo 2
Todo 3
...
Todo 100
```

UI heavy হয়ে যেতে পারে।

আমরা চাই:

```text
Page 1
Todo 1
Todo 2
Todo 3
Todo 4
Todo 5

[Previous] [Next]
```

তারপর:

```text
Page 2
Todo 6
Todo 7
Todo 8
Todo 9
Todo 10
```

---

# 2. Pagination-এর দুইটা মূল concept

```text
page
pageSize
```

ধরো:

```js
const pageSize = 5;
const page = 1;
```

তাহলে:

```text
page 1 → 1-5
page 2 → 6-10
page 3 → 11-15
```

Formula:

```js
offset = (page - 1) * pageSize;
```

যেমন:

```text
page = 1
offset = 0

page = 2
offset = 5

page = 3
offset = 10
```

---

# 3. Dexie-তে pagination

Dexie-তে:

```js
.offset()
.limit()
```

ব্যবহার করতে পারি।

```js
const todos = await db.todos
  .offset(0)
  .limit(5)
  .toArray();
```

মানে:

```text
offset 0
↓
প্রথম 5টা
```

Page 2:

```js
const todos = await db.todos
  .offset(5)
  .limit(5)
  .toArray();
```

---

# 4. React state

`App.jsx`:

```js
const [page, setPage] = useState(1);

const pageSize = 5;
```

---

# 5. `useLiveQuery()` দিয়ে pagination

```js
const todos = useLiveQuery(
  () => {
    const offset = (page - 1) * pageSize;

    return db.todos
      .offset(offset)
      .limit(pageSize)
      .toArray();
  },
  [page]
);
```

এখন:

```text
page = 1
↓
offset = 0
↓
5 records
```

Page change হলে:

```text
page = 2
↓
offset = 5
↓
next 5 records
```

---

# 6. Previous / Next button

```jsx
<button
  disabled={page === 1}
  onClick={() => setPage(page - 1)}
>
  Previous
</button>

<span>
  Page {page}
</span>

<button
  onClick={() => setPage(page + 1)}
>
  Next
</button>
```

তবে এখানে একটা সমস্যা আছে।

শেষ page-এর পরে গেলেও `Next` click করা যাবে।

সেটা আমরা পরে ঠিক করবো।

---

# 7. Total count বের করা

Pagination properly করতে total কতগুলো Todo আছে সেটা জানতে হবে।

Dexie:

```js
const count = await db.todos.count();
```

যেমন:

```text
100 Todos
↓
count = 100
```

তারপর total page:

```js
const totalPages = Math.ceil(
  count / pageSize
);
```

যদি:

```text
100 todos
pageSize = 5
```

তাহলে:

```text
100 / 5 = 20 pages
```

---

# 8. কিন্তু `count`-ও reactive করতে চাই

`useLiveQuery()` দিয়ে:

```js
const totalCount = useLiveQuery(
  () => db.todos.count(),
  []
);
```

তারপর:

```js
const totalPages = Math.ceil(
  (totalCount || 0) / pageSize
);
```

---

# 9. Next button disable

```jsx
<button
  disabled={page >= totalPages}
  onClick={() => setPage(page + 1)}
>
  Next
</button>
```

এখন শেষ page-এ গেলে:

```text
Next → disabled
```

---

# 10. Sorting

এখন ধরো তুমি চাই:

```text
Newest first
Oldest first
```

এর জন্য database-এ `createdAt` রাখা ভালো।

আমাদের বর্তমান schema:

```js
todos: "++id, title, completed"
```

এটা পরিবর্তন করে:

```js
todos: "++id, title, completed, createdAt"
```

কিন্তু এখানে একটা important ব্যাপার আছে।

**Existing database-এর schema version change করলে নতুন version দিতে হবে।**

```js
db.version(2).stores({
  todos: "++id, title, completed, createdAt"
});
```

তবে beginner project-এ এখন cleanভাবে database reset করে আবার শুরু করাও সহজ হতে পারে।

---

# 11. Todo add করার সময় `createdAt`

```js
await db.todos.add({
  title: title.trim(),
  completed: false,
  createdAt: Date.now()
});
```

তাহলে data:

```js
{
  id: 1,
  title: "Learn React",
  completed: false,
  createdAt: 1750000000000
}
```

প্রতিটা Todo-এর creation time থাকবে।

---

# 12. Newest first

Dexie দিয়ে:

```js
const todos = await db.todos
  .orderBy("createdAt")
  .reverse()
  .toArray();
```

মানে:

```text
orderBy("createdAt")
        ↓
পুরনো → নতুন

reverse()
        ↓
নতুন → পুরনো
```

---

# 13. Oldest first

```js
const todos = await db.todos
  .orderBy("createdAt")
  .toArray();
```

---

# 14. Sorting state

```js
const [sort, setSort] = useState("newest");
```

Dropdown:

```jsx
<select
  value={sort}
  onChange={(e) => {
    setSort(e.target.value);
    setPage(1);
  }}
>
  <option value="newest">
    Newest
  </option>

  <option value="oldest">
    Oldest
  </option>
</select>
```

`setPage(1)` করছি কারণ sorting পরিবর্তন হলে প্রথম page-এ চলে যাওয়া sensible।

---

# 15. Pagination + Sorting একসাথে

```js
const todos = useLiveQuery(
  () => {
    const offset = (page - 1) * pageSize;

    let query = db.todos.orderBy("createdAt");

    if (sort === "newest") {
      query = query.reverse();
    }

    return query
      .offset(offset)
      .limit(pageSize)
      .toArray();
  },
  [page, sort]
);
```

এখন flow:

```text
sort
 ↓
orderBy()
 ↓
reverse() ?
 ↓
offset()
 ↓
limit()
 ↓
toArray()
```

---

# 16. একটা important Dexie concept

এখানে:

```js
db.todos.orderBy("createdAt")
```

ভালোভাবে কাজ করার জন্য `createdAt`-কে IndexedDB schema-তে indexed field হিসেবে define করা উচিত:

```js
db.version(2).stores({
  todos: "++id, title, completed, createdAt"
});
```

আর একটা ব্যাপার:

**`offset()` বড় dataset-এ perfect database pagination না।**

যেমন:

```text
10 records
→ offset(5) ঠিক আছে

1,000,000 records
→ offset(900000)
```

এক্ষেত্রে অনেক record skip করতে হতে পারে।

Real-world বড় dataset-এ **cursor/keyset pagination** বেশি efficient হতে পারে।

এটা আমরা advanced part-এ করবো।

---

# 17. Current project structure

এখন আমাদের:

```text
src/
│
├── db/
│   └── db.js
│
├── App.jsx
│
└── main.jsx
```

Database:

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(2).stores({
  todos: "++id, title, completed, createdAt"
});
```

---

# 18. Todo Add

```js
const addTodo = async (e) => {
  e.preventDefault();

  if (!title.trim()) return;

  await db.todos.add({
    title: title.trim(),
    completed: false,
    createdAt: Date.now()
  });

  setTitle("");
};
```

---

# 19. Paginated query

```js
const todos = useLiveQuery(
  () => {
    const offset = (page - 1) * pageSize;

    let query = db.todos.orderBy("createdAt");

    if (sort === "newest") {
      query = query.reverse();
    }

    return query
      .offset(offset)
      .limit(pageSize)
      .toArray();
  },
  [page, sort]
);
```

---

# 20. Complete Pagination UI

```jsx
<div>
  {todos?.map((todo) => (
    <div key={todo.id}>
      {todo.title}
    </div>
  ))}

  <button
    disabled={page === 1}
    onClick={() => setPage(page - 1)}
  >
    Previous
  </button>

  <span>
    Page {page} of {totalPages}
  </span>

  <button
    disabled={page >= totalPages}
    onClick={() => setPage(page + 1)}
  >
    Next
  </button>
</div>
```

---

# 🧠 Part 7-এর core concept

তোমাকে এখন এইগুলো মনে রাখতে হবে:

### Pagination

```js
.offset()
.limit()
```

### Total records

```js
.count()
```

### Sorting

```js
.orderBy()
```

### Reverse order

```js
.reverse()
```

### Reactive query

```js
useLiveQuery()
```

---

## এখন পুরো data flow

```text
                 React
                   ↓
          useLiveQuery()
                   ↓
              Dexie Query
                   ↓
        ┌──────────┴──────────┐
        ↓                     ↓
    orderBy()              count()
        ↓
    reverse()
        ↓
    offset()
        ↓
     limit()
        ↓
      toArray()
        ↓
     IndexedDB
```

এখন তুমি শুধু CRUD না—**local database query করা**ও শুরু করে দিয়েছো। 🔥

**Part 8-এ আমরা `useLiveQuery()`-কে আরও properly ব্যবহার করে `todos`-এর জন্য custom hook বানাবো—যেমন `useTodos()`, `useAddTodo()`, `useDeleteTodo()`। এতে `App.jsx` অনেক clean হবে এবং real React project-এর architecture-এর মতো হবে।**

---
চলো 🔥 **Part 8: Custom Hooks + Clean Architecture** করি।

এখন পর্যন্ত `App.jsx`-এর মধ্যে database-এর সব logic লিখছিলাম। Real project-এ এটা করলে `App.jsx` অনেক বড় হয়ে যায়।

আমরা এখন database logic আলাদা করব।

## আমাদের নতুন structure

```text
src/
│
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── components/
│   ├── TodoForm.jsx
│   └── TodoList.jsx
│
└── App.jsx
```

Flow:

```text
App
 ↓
Components
 ↓
Custom Hooks
 ↓
Dexie
 ↓
IndexedDB
```

---

# Step 1 — `useTodos.js`

`src/hooks/useTodos.js`

```js
import { useLiveQuery } from "dexie-react-hooks";
import { db } from "../db/db";

export const useTodos = () => {

  const todos = useLiveQuery(
    () => db.todos.toArray(),
    []
  );

  const addTodo = async (title) => {
    await db.todos.add({
      title: title.trim(),
      completed: false,
      createdAt: Date.now()
    });
  };

  const updateTodo = async (id, data) => {
    await db.todos.update(id, data);
  };

  const deleteTodo = async (id) => {
    await db.todos.delete(id);
  };

  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed
    });
  };

  return {
    todos,
    addTodo,
    updateTodo,
    deleteTodo,
    toggleTodo
  };
};
```

এখন database-এর সব কাজ এক জায়গায়।

---

# Step 2 — `App.jsx` অনেক ছোট হবে

```jsx
import { useState } from "react";
import { useTodos } from "./hooks/useTodos";

function App() {
  const [title, setTitle] = useState("");

  const {
    todos,
    addTodo,
    deleteTodo,
    toggleTodo
  } = useTodos();

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await addTodo(title);

    setTitle("");
  };

  return (
    <div>
      <h1>Todo App</h1>

      <form onSubmit={handleSubmit}>
        <input
          value={title}
          onChange={(e) =>
            setTitle(e.target.value)
          }
        />

        <button type="submit">
          Add
        </button>
      </form>

      <hr />

      {todos?.map((todo) => (
        <div key={todo.id}>

          <input
            type="checkbox"
            checked={todo.completed}
            onChange={() =>
              toggleTodo(
                todo.id,
                todo.completed
              )
            }
          />

          <span>{todo.title}</span>

          <button
            onClick={() =>
              deleteTodo(todo.id)
            }
          >
            Delete
          </button>

        </div>
      ))}
    </div>
  );
}

export default App;
```

দেখো, `App.jsx` এখন database সম্পর্কে প্রায় কিছুই জানে না।

---

# Step 3 — কেন Custom Hook?

আগে:

```text
App.jsx
 ├── useState
 ├── useLiveQuery
 ├── db.todos.add
 ├── db.todos.update
 ├── db.todos.delete
 ├── db.todos.toArray
 └── UI
```

অনেক responsibility। 😵

এখন:

```text
App.jsx
 └── UI
      ↓
   useTodos()
      ↓
   Dexie
      ↓
 IndexedDB
```

এটাই **separation of concerns**।

---

# Step 4 — আলাদা `TodoForm`

এখন আরও clean করি।

`src/components/TodoForm.jsx`

```jsx
import { useState } from "react";

function TodoForm({ onAdd }) {
  const [title, setTitle] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await onAdd(title);

    setTitle("");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={title}
        onChange={(e) =>
          setTitle(e.target.value)
        }
        placeholder="Enter todo"
      />

      <button type="submit">
        Add Todo
      </button>
    </form>
  );
}

export default TodoForm;
```

---

# Step 5 — `TodoList`

`src/components/TodoList.jsx`

```jsx
function TodoList({
  todos,
  onToggle,
  onDelete
}) {
  return (
    <div>
      {todos?.map((todo) => (
        <div key={todo.id}>

          <input
            type="checkbox"
            checked={todo.completed}
            onChange={() =>
              onToggle(
                todo.id,
                todo.completed
              )
            }
          />

          <span>
            {todo.title}
          </span>

          <button
            onClick={() =>
              onDelete(todo.id)
            }
          >
            Delete
          </button>

        </div>
      ))}
    </div>
  );
}

export default TodoList;
```

---

# Step 6 — Final `App.jsx`

```jsx
import TodoForm from "./components/TodoForm";
import TodoList from "./components/TodoList";
import { useTodos } from "./hooks/useTodos";

function App() {
  const {
    todos,
    addTodo,
    deleteTodo,
    toggleTodo
  } = useTodos();

  return (
    <div>
      <h1>Todo App</h1>

      <TodoForm onAdd={addTodo} />

      <hr />

      <TodoList
        todos={todos}
        onToggle={toggleTodo}
        onDelete={deleteTodo}
      />
    </div>
  );
}

export default App;
```

এখন architecture অনেক cleaner:

```text
                  App
                   │
          ┌────────┴────────┐
          ↓                 ↓
      TodoForm          TodoList
          │                 │
          └────────┬────────┘
                   ↓
               useTodos()
                   ↓
                 Dexie
                   ↓
               IndexedDB
```

---

# Step 7 — একটা গুরুত্বপূর্ণ concept

`useTodos()` একটা **custom hook**।

```js
const {
  todos,
  addTodo,
  deleteTodo,
  toggleTodo
} = useTodos();
```

এটা basically আমাদের database-related functionality-এর একটা reusable package।

অন্য component থেকেও চাইলে:

```js
const { todos } = useTodos();
```

ব্যবহার করতে পারবে।

---

# Step 8 — Update-ও hook-এর মধ্যে

আমরা আগে:

```js
const updateTodo = async (id, data) => {
  await db.todos.update(id, data);
};
```

hook-এ রেখেছি।

তাই Edit component থেকে সরাসরি IndexedDB নিয়ে চিন্তা করতে হবে না।

```js
await updateTodo(1, {
  title: "Learn React Advanced"
});
```

Component শুধু বলবে:

> "এই Todo update করো"

কীভাবে IndexedDB-তে update হবে সেটা component-এর concern না।

---

# 🧠 Part 8-এর সবচেয়ে important lesson

### Bad architecture

```text
Component
   ↓
Direct IndexedDB
```

### Better architecture

```text
Component
   ↓
Custom Hook
   ↓
Dexie
   ↓
IndexedDB
```

এটা বড় application-এ অনেক useful।

---

## এখন আমাদের project

```text
src/
│
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── components/
│   ├── TodoForm.jsx
│   └── TodoList.jsx
│
└── App.jsx
```

এখন একটা বড় improvement করার সময় এসেছে।

**Part 9 → Offline-first CRUD** 🔥

এখানে আমরা বুঝবো:

```text
Internet নেই
     ↓
User Todo add করলো
     ↓
IndexedDB-তে save
     ↓
UI update
     ↓
Internet এলে
     ↓
Server-এর সাথে sync
```

এখান থেকেই **real-world offline application architecture** শুরু হবে।

---
# চলো 🔥 **Part 9: Offline-First CRUD** শুরু করি।

এটা একটু advanced concept, কিন্তু আমাদের Todo app দিয়ে খুব সহজে বুঝবো।

## 🎯 Offline-first কী?

ধরো user-এর internet নেই।

তারপরও সে Todo add করতে পারবে:

```text
User
 ↓
Add Todo
 ↓
IndexedDB
 ↓
UI Update
```

Internet থাকার দরকার নেই।

পরে internet এলে চাইলে server-এর সাথে sync করা যাবে:

```text
              ┌──→ Server
              │
Todo → IndexedDB
              │
              └──→ UI
```

### Important

আমাদের বর্তমান app **local offline app** হিসেবে কাজ করছে।

কিন্তু **real offline-first sync architecture** করতে হলে সাধারণত backend/server-ও লাগবে।

তাই Part 9-এ আমরা প্রথমে **local offline-first foundation** বানাবো।

---

# Step 1 — কেন IndexedDB এখানে useful?

আমরা যদি শুধু React state ব্যবহার করি:

```js
const [todos, setTodos] = useState([]);
```

browser refresh করলে data চলে যাবে।

কিন্তু IndexedDB:

```text
React State
   ↓
temporary UI data

IndexedDB
   ↓
persistent browser data
```

তাই:

```text
Internet ❌
Browser refresh 🔄
App reopen 🚀
```

তারপরও Todo থাকবে।

---

# Step 2 — আমাদের `db.js`

আগের schema-তে `createdAt` যোগ করেছিলাম।

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(2).stores({
  todos: "++id, title, completed, createdAt"
});
```

এখানে:

```text
++id
```

মানে auto-increment primary key।

আর:

```text
title
completed
createdAt
```

হলো indexed fields।

---

# Step 3 — Todo তৈরি করার সময় timestamp

`useTodos.js`:

```js
const addTodo = async (title) => {
  await db.todos.add({
    title: title.trim(),
    completed: false,
    createdAt: Date.now()
  });
};
```

এখন একটা Todo দেখতে এমন হতে পারে:

```js
{
  id: 1,
  title: "Learn Dexie",
  completed: false,
  createdAt: 1750000000000
}
```

---

# Step 4 — Internet ছাড়াই test করি

Browser-এর DevTools খুলে Network tab-এ যাও।

তারপর:

```text
Network
 ↓
Offline
```

এখন internet বন্ধ করে Todo add করো।

```text
Add Todo
   ↓
db.todos.add()
   ↓
IndexedDB
```

Todo add হবে। কারণ এখানে আমরা server call করছি না।

---

# Step 5 — Refresh করে দেখো

Offline অবস্থাতেই:

```text
Ctrl + R
```

করো।

তারপরও Todo থাকলে বুঝবে:

```text
React state ❌
       ↓
IndexedDB ✅
```

থেকে data load হচ্ছে।

এটাই আমাদের offline foundation।

---

# Step 6 — `useLiveQuery()` এখানে magic করছে

আমাদের hook:

```js
const todos = useLiveQuery(
  () => db.todos.toArray(),
  []
);
```

ধরো:

```text
IndexedDB
    ↓
useLiveQuery()
    ↓
todos
    ↓
React UI
```

এখন database change হলে:

```text
db.todos.add()
      ↓
IndexedDB changes
      ↓
useLiveQuery detects
      ↓
React re-render
      ↓
UI updated
```

তাই manually:

```js
loadTodos();
```

করতে হচ্ছে না।

---

# Step 7 — Offline Delete

Delete-ও একইভাবে কাজ করবে।

```js
const deleteTodo = async (id) => {
  await db.todos.delete(id);
};
```

Internet লাগবে না।

```text
Click Delete
     ↓
Dexie
     ↓
IndexedDB
     ↓
useLiveQuery
     ↓
UI update
```

---

# Step 8 — Offline Update

```js
const toggleTodo = async (id, completed) => {
  await db.todos.update(id, {
    completed: !completed
  });
};
```

Internet ❌

তবুও কাজ করবে।

---

# 🧠 কিন্তু একটা বড় প্রশ্ন

এখন ধরো আমাদের app-এর backend আছে।

User offline অবস্থায়:

```text
Add Todo
"Learn React"
```

IndexedDB-তে save হলো।

তারপর internet ফিরে এলো।

আমাদের backend এখনো জানে না যে Todo তৈরি হয়েছে।

তাই real offline-first app-এ আমরা সাধারণত একটা **sync status** রাখি।

যেমন:

```js
{
  id: 1,
  title: "Learn React",
  completed: false,
  createdAt: Date.now(),
  synced: false
}
```

---

# Step 9 — `synced` field

তাহলে `addTodo()`:

```js
const addTodo = async (title) => {
  await db.todos.add({
    title: title.trim(),
    completed: false,
    createdAt: Date.now(),
    synced: false
  });
};
```

এখন:

```text
synced: false
```

মানে:

> "এই data এখনো server-এর সাথে sync হয়নি।"

Server-এ successfully পাঠানোর পরে:

```js
await db.todos.update(id, {
  synced: true
});
```

---

# Step 10 — আরও ভালো architecture

Real application-এ আমরা এমন structure করতে পারি:

```text
src/
│
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── services/
│   └── syncService.js
│
├── components/
│   ├── TodoForm.jsx
│   └── TodoList.jsx
│
└── App.jsx
```

Flow:

```text
              ┌──────────────┐
              │   React UI   │
              └──────┬───────┘
                     ↓
               useTodos()
                     ↓
                IndexedDB
                     ↓
             ┌───────┴───────┐
             ↓               ↓
         Local UI        Sync Service
                             ↓
                           API
                             ↓
                           Server
```

এখানে IndexedDB হলো **local source of truth** হিসেবে কাজ করতে পারে, আর sync service server-এর সাথে data synchronize করে।

---

# ⚠️ একটা গুরুত্বপূর্ণ distinction

**Offline CRUD** আর **Offline-first sync** এক জিনিস না।

### আমরা এখন যা করেছি:

```text
Offline CRUD
     ↓
IndexedDB
     ↓
Local app works offline
```

### Full offline-first:

```text
Offline action
      ↓
IndexedDB
      ↓
Queue pending changes
      ↓
Internet ফিরে আসে
      ↓
Sync API
      ↓
Server
      ↓
Mark synced
```

এটা অনেক বেশি advanced।

---

# 🎯 Part 9 recap

আজকের সবচেয়ে important concepts:

|Concept|কাজ|
|---|---|
|IndexedDB|Browser-এর persistent database|
|Dexie|IndexedDB সহজভাবে ব্যবহার করার library|
|`useLiveQuery()`|DB change হলে UI update|
|Offline CRUD|Internet ছাড়াই local CRUD|
|`synced`|Server sync status track|
|Sync service|Local ↔ Server synchronization|

Mental model:

```text
                 OFFLINE
                   ↓
User → React → Dexie → IndexedDB
                   ↓
                  UI
                   
                 ONLINE
                   ↓
User → React → IndexedDB
                   ↓
              Sync Service
                   ↓
                 API
                   ↓
                Server
```

**Part 10**-এ আমরা এই project-এ **TanStack Query + Dexie একসাথে** ব্যবহার করব—কোন data local হবে, কোন data server state হবে, `useQuery`, `useMutation`, cache invalidation, আর local DB-এর সাথে sync কীভাবে চিন্তা করতে হয় সেটা দেখব। 🔥

---
চলো 🔥 **Part 10: TanStack Query + Dexie একসাথে** করি।

এটা আমাদের Todo project-এর সবচেয়ে important architecture অংশগুলোর একটা।

এখন পর্যন্ত:

```text
React
 ↓
Dexie
 ↓
IndexedDB
```

এবার আমরা server যোগ করব:

```text
React
 ↓
TanStack Query
 ↓
API
 ↓
Server
```

আর offline/local data:

```text
React
 ↓
Dexie
 ↓
IndexedDB
```

শেষে দুইটা একসাথে:

```text
                 React UI
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
    TanStack Query          Dexie
          ↓                   ↓
        API                IndexedDB
          ↓
       Server
```

---

# 1. প্রথমে একটা খুব important distinction

### TanStack Query

এটা মূলত **server state** manage করবে।

```text
Server → API → TanStack Query → React
```

যেমন:

```js
todos from backend
users from backend
products from backend
```

### Dexie

এটা **local browser database** manage করবে।

```text
React → Dexie → IndexedDB
```

যেমন:

```text
offline todos
local drafts
pending sync operations
cached local data
```

---

# 2. Install TanStack Query

```bash
npm install @tanstack/react-query
```

Devtools চাইলে:

```bash
npm install @tanstack/react-query-devtools
```

---

# 3. `QueryClient` তৈরি করি

`main.jsx`

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import {
  QueryClient,
  QueryClientProvider
} from "@tanstack/react-query";

import App from "./App";

const queryClient = new QueryClient();

ReactDOM.createRoot(
  document.getElementById("root")
).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

এখন পুরো React app TanStack Query ব্যবহার করতে পারবে।

---

# 4. Server API ধরি

ধরি backend আছে:

```text
GET    /todos
POST   /todos
PATCH  /todos/:id
DELETE /todos/:id
```

একটা API function:

```js
const getTodos = async () => {
  const response = await fetch(
    "https://api.example.com/todos"
  );

  if (!response.ok) {
    throw new Error("Failed to fetch todos");
  }

  return response.json();
};
```

---

# 5. `useQuery()`

এখন:

```jsx
import { useQuery } from "@tanstack/react-query";

const { data, isPending, isError } = useQuery({
  queryKey: ["todos"],
  queryFn: getTodos
});
```

Flow:

```text
useQuery()
   ↓
queryKey ["todos"]
   ↓
queryFn()
   ↓
API
   ↓
Server
   ↓
TanStack Query Cache
   ↓
React
```

---

# 6. TanStack Query Cache vs IndexedDB

এখানে confusion হওয়া খুব normal।

### TanStack Query cache

```text
Memory/cache
```

এর primary purpose:

- server data caching
    
- loading/error state
    
- refetch
    
- background synchronization
    
- stale data management
    

### IndexedDB

```text
Persistent browser database
```

এর primary purpose:

- local persistence
    
- offline data
    
- large structured data
    
- local database operations
    

সহজভাবে:

```text
TanStack Query
= Server data manager

Dexie
= Browser database manager
```

---

# 7. তাহলে দুটো একসাথে কেন?

ধরো user online:

```text
Server
  ↓
TanStack Query
  ↓
React
```

কিন্তু user offline:

```text
IndexedDB
  ↓
React
```

তাই আমরা চাই:

```text
                Todo App
                   │
          ┌────────┴────────┐
          ↓                 ↓
       Server             Local
          ↓                 ↓
   TanStack Query         Dexie
          ↓                 ↓
          └───────┬─────────┘
                  ↓
                 UI
```

---

# 8. কিন্তু একটা mistake করা যাবে না

শুধু একই Todo data দুই জায়গায় রেখে দিলে problem হতে পারে।

ধরো:

```text
Server:
Todo A = completed

IndexedDB:
Todo A = not completed
```

এখন কোনটা সত্য?

😵

এটাই **data synchronization problem**।

তাই architecture আগে ঠিক করতে হবে।

---

# 9. একটা practical architecture

আমরা বলতে পারি:

### Server হলো source of truth

```text
Server
  ↓
TanStack Query
  ↓
React
```

আর Dexie হলো offline persistence/local working database:

```text
Server
  ↓
Dexie
  ↓
IndexedDB
  ↓
React
```

কিন্তু full offline-first app-এ sync logic দরকার।

---

# 10. Online Create

ধরো user Todo add করলো।

```js
const addTodo = async (todo) => {
  const response = await fetch(
    "https://api.example.com/todos",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(todo)
    }
  );

  if (!response.ok) {
    throw new Error("Failed to create todo");
  }

  return response.json();
};
```

তারপর mutation:

```jsx
import { useMutation } from "@tanstack/react-query";

const mutation = useMutation({
  mutationFn: addTodo
});
```

Call:

```js
mutation.mutate({
  title: "Learn TanStack Query",
  completed: false
});
```

---

# 11. Mutation-এর পরে query refresh

Todo create করার পরে cached list পুরোনো হয়ে গেছে।

তাই:

```js
const mutation = useMutation({
  mutationFn: addTodo,

  onSuccess: () => {
    queryClient.invalidateQueries({
      queryKey: ["todos"]
    });
  }
});
```

Flow:

```text
POST Todo
   ↓
Server success
   ↓
invalidateQueries()
   ↓
["todos"] stale
   ↓
Refetch
   ↓
Updated UI
```

এটা TanStack Query-এর সবচেয়ে important patterns-এর একটা।

---

# 12. Delete

```js
const deleteTodo = async (id) => {
  const response = await fetch(
    `https://api.example.com/todos/${id}`,
    {
      method: "DELETE"
    }
  );

  if (!response.ok) {
    throw new Error("Failed to delete");
  }
};
```

Mutation:

```js
const deleteMutation = useMutation({
  mutationFn: deleteTodo,

  onSuccess: () => {
    queryClient.invalidateQueries({
      queryKey: ["todos"]
    });
  }
});
```

---

# 13. এখন Dexie কোথায়?

এখানে আসল interesting part।

Offline অবস্থায়:

```text
mutation
   ↓
API request
   ↓
❌ Network Error
```

তখন আমরা local DB-তে save করতে পারি:

```text
User creates Todo
       ↓
Try API
       ↓
   Internet?
    /     \
  Yes      No
   ↓        ↓
Server    Dexie
            ↓
       synced:false
```

---

# 14. Pending sync data

Dexie schema আরও useful করা যায়:

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(3).stores({
  todos: "++id, title, completed, createdAt, synced"
});
```

Todo:

```js
{
  id: 1,
  title: "Learn React",
  completed: false,
  createdAt: Date.now(),
  synced: false
}
```

`false` মানে:

> এই local change এখনো server-এ যায়নি।

---

# 15. Sync service

আমরা একটা আলাদা file করতে পারি:

```text
src/
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── services/
│   └── syncService.js
│
├── components/
│   ├── TodoForm.jsx
│   └── TodoList.jsx
│
└── App.jsx
```

`syncService.js`:

```js
import { db } from "../db/db";

export const syncTodos = async () => {
  const pendingTodos = await db.todos
    .where("synced")
    .equals(false)
    .toArray();

  for (const todo of pendingTodos) {
    // এখানে API call হবে

    // success হলে
    await db.todos.update(todo.id, {
      synced: true
    });
  }
};
```

এখন conceptually:

```text
IndexedDB
   ↓
synced === false
   ↓
Pending todos
   ↓
API
   ↓
Success
   ↓
synced = true
```

---

# 16. Internet ফিরে এলে sync

Browser-এর:

```js
window.addEventListener(
  "online",
  () => {
    syncTodos();
  }
);
```

এভাবে online হলে sync trigger করা যায়।

React component-এ effect দিয়ে lifecycle manage করা যেতে পারে:

```jsx
useEffect(() => {
  const handleOnline = () => {
    syncTodos();
  };

  window.addEventListener(
    "online",
    handleOnline
  );

  return () => {
    window.removeEventListener(
      "online",
      handleOnline
    );
  };
}, []);
```

---

# 17. Full mental model

এখন পুরো project-টা দেখো:

```text
                         React
                           │
              ┌────────────┴────────────┐
              │                         │
              ↓                         ↓
       TanStack Query                Dexie
              │                         │
              ↓                         ↓
             API                   IndexedDB
              │                         │
              ↓                         ↓
           Server                  Local Data
              │                         │
              └────────────┬────────────┘
                           ↓
                       Sync Logic
```

### Online

```text
React
 ↓
TanStack Query
 ↓
API
 ↓
Server
```

### Offline

```text
React
 ↓
Dexie
 ↓
IndexedDB
```

### Back online

```text
IndexedDB
 ↓
Pending changes
 ↓
Sync Service
 ↓
API
 ↓
Server
 ↓
synced = true
```

---

# 🧠 Part 10-এর মূল শিক্ষা

তোমাকে এই ৩টা জিনিস আলাদা করে মনে রাখতে হবে:

```text
fetch / axios
     ↓
HTTP request করা

TanStack Query
     ↓
Server state manage করা

Dexie
     ↓
IndexedDB/local browser data manage করা
```

তাই:

```text
React
 ↓
TanStack Query
 ↓
Axios / fetch
 ↓
Backend
```

এবং offline-এর জন্য:

```text
React
 ↓
Dexie
 ↓
IndexedDB
```

দুটো একসাথে ব্যবহার করা **possible**, কিন্তু শুধু দু জায়গায় data রাখলেই offline-first হয় না—**sync strategy, conflict handling, retry, unique IDs, pending operations** ইত্যাদিও design করতে হয়।

---

## 🏁 আমাদের CRUD roadmap এখন

```text
✅ Part 1  → Dexie setup
✅ Part 2  → Create + Read
✅ Part 3  → Update + Delete
✅ Part 4  → useLiveQuery
✅ Part 5  → Edit Todo
✅ Part 6  → Search + Filter
✅ Part 7  → Pagination + Sorting
✅ Part 8  → Custom Hooks + Architecture
✅ Part 9  → Offline-first foundation
✅ Part 10 → TanStack Query + Dexie
```

এখন তুমি **basic Dexie CRUD থেকে real-world architecture**-এ চলে এসেছো। 🔥

পরের logical step হবে **Part 11: Production-level CRUD architecture** — `api/`, `services/`, `hooks/`, query keys, mutations, error handling, loading states, এবং TanStack Query + Dexie-এর clean folder structure একসাথে সাজানো।

---
হ্যাঁ। তুমি যেহেতু **React + Dexie + IndexedDB** দিয়ে application বানাতে চাচ্ছো, আমি শুরু থেকেই একটা clean, scalable structure রাখার পরামর্শ দেব।

### Recommended structure

```text
my-react-app/
│
├── public/
│
├── src/
│   │
│   ├── assets/
│   │   ├── images/
│   │   └── icons/
│   │
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.jsx
│   │   │   ├── Input.jsx
│   │   │   └── Modal.jsx
│   │   │
│   │   └── todos/
│   │       ├── TodoForm.jsx
│   │       ├── TodoList.jsx
│   │       └── TodoItem.jsx
│   │
│   ├── db/
│   │   ├── db.js
│   │   └── todoTable.js
│   │
│   ├── hooks/
│   │   ├── useTodos.js
│   │   └── useTodoActions.js
│   │
│   ├── pages/
│   │   ├── Home.jsx
│   │   └── Todos.jsx
│   │
│   ├── services/
│   │   └── todoService.js
│   │
│   ├── utils/
│   │   ├── date.js
│   │   └── helpers.js
│   │
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── .gitignore
├── package.json
├── vite.config.js
└── README.md
```

## প্রতিটা folder-এর কাজ

### `components/`

UI components থাকবে।

```text
components/
└── todos/
    ├── TodoForm.jsx
    ├── TodoList.jsx
    └── TodoItem.jsx
```

যেমন `TodoItem` শুধু একটা Todo দেখাবে।

```jsx
function TodoItem({ todo, onDelete }) {
  return (
    <div>
      <span>{todo.title}</span>

      <button onClick={() => onDelete(todo.id)}>
        Delete
      </button>
    </div>
  );
}
```

---

### `db/` ⭐

এটা তোমার **IndexedDB/Dexie layer**।

```text
db/
├── db.js
└── todoTable.js
```

`db.js`:

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(1).stores({
  todos: "++id, title, completed, createdAt"
});
```

এখানে database configuration থাকবে।

---

### `hooks/` ⭐

React-এর data/business logic থাকবে।

```text
hooks/
├── useTodos.js
└── useTodoActions.js
```

যেমন:

```js
import { useLiveQuery } from "dexie-react-hooks";
import { db } from "../db/db";

export function useTodos() {
  const todos = useLiveQuery(
    () => db.todos.toArray(),
    []
  );

  return todos;
}
```

Component তখন শুধু:

```jsx
const todos = useTodos();
```

করবে।

---

### `services/`

Database/API related reusable operations এখানে রাখতে পারো।

```text
services/
└── todoService.js
```

যেমন:

```js
import { db } from "../db/db";

export const todoService = {
  getAll: () => db.todos.toArray(),

  create: (todo) => db.todos.add(todo),

  update: (id, data) =>
    db.todos.update(id, data),

  remove: (id) =>
    db.todos.delete(id)
};
```

তাহলে component-কে Dexie-এর details জানতে হবে না।

---

### `pages/`

Application-এর বড় screen/page থাকবে।

```text
pages/
├── Home.jsx
└── Todos.jsx
```

যেমন:

```text
App
 │
 ├── Home
 │
 └── Todos
      ├── TodoForm
      └── TodoList
           └── TodoItem
```

---

### `utils/`

ছোট reusable helper functions।

```text
utils/
├── date.js
└── helpers.js
```

যেমন:

```js
export const formatDate = (date) => {
  return new Date(date).toLocaleDateString();
};
```

---

# সবচেয়ে important architecture

তোমার application-টা এভাবে ভাবো:

```text
                 React UI
                    │
                    ↓
                Components
                    │
                    ↓
                  Hooks
                    │
                    ↓
                Services
                    │
                    ↓
                  Dexie
                    │
                    ↓
                IndexedDB
```

মানে:

```text
UI
 ↓
Logic
 ↓
Data access
 ↓
Database
```

এতে একটা বড় সুবিধা হচ্ছে—কালকে যদি Dexie বাদ দিয়ে অন্য storage ব্যবহার করতে চাও, পুরো UI rewrite করতে হবে না।

---

## তবে শুরুতেই এত folder বানানোর দরকার নেই

তুমি এখন learning/project phase-এ থাকলে আমি এই structure দিয়ে শুরু করতাম:

```text
src/
│
├── components/
│   ├── TodoForm.jsx
│   ├── TodoList.jsx
│   └── TodoItem.jsx
│
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── pages/
│   └── Todos.jsx
│
├── App.jsx
└── main.jsx
```

তারপর application বড় হলে:

```text
services/
utils/
api/
features/
```

যোগ করবে।

**Rule of thumb:** ছোট project-এ simple structure, বড় project-এ feature/role অনুযায়ী separation। একেবারে শুরুতেই ২০টা folder বানালে বরং confusion বাড়ে।

---
অবশ্যই। 👍 Practice করার জন্য আমরা **একই Todo app**-টা এই structure অনুযায়ী পুরো code দিয়ে বানাই। আমি প্রতিটা file-এর দায়িত্বও বুঝিয়ে দিচ্ছি।

```text
src/
│
├── components/
│   ├── TodoForm.jsx
│   ├── TodoList.jsx
│   └── TodoItem.jsx
│
├── db/
│   └── db.js
│
├── hooks/
│   └── useTodos.js
│
├── pages/
│   └── Todos.jsx
│
├── App.jsx
└── main.jsx
```

আমাদের final flow হবে:

```text
main.jsx
   ↓
App.jsx
   ↓
Todos.jsx
   ↓
useTodos()
   ↓
Dexie
   ↓
IndexedDB
```

আর UI:

```text
Todos
 ├── TodoForm
 └── TodoList
      └── TodoItem
```

---

# 1️⃣ `db/db.js`

এটা হবে আমাদের **database configuration**।

```js
import Dexie from "dexie";

export const db = new Dexie("TodoDB");

db.version(1).stores({
  todos: "++id, title, completed, createdAt",
});
```

### এটা কী করছে?

```js
new Dexie("TodoDB")
```

একটা IndexedDB database তৈরি করছে।

আর:

```js
todos: "++id, title, completed, createdAt"
```

মানে `todos` নামে একটা table থাকবে।

একটা Todo দেখতে এমন:

```js
{
  id: 1,
  title: "Learn React",
  completed: false,
  createdAt: 17123456789
}
```

---

# 2️⃣ `hooks/useTodos.js`

এটা সবচেয়ে important fileগুলোর একটা।

এখানে আমরা **React + Dexie logic** রাখব।

```js
import { useLiveQuery } from "dexie-react-hooks";
import { db } from "../db/db";

export const useTodos = () => {
  // READ
  const todos = useLiveQuery(
    () => db.todos.toArray(),
    []
  );

  // CREATE
  const addTodo = async (title) => {
    if (!title.trim()) return;

    await db.todos.add({
      title: title.trim(),
      completed: false,
      createdAt: Date.now(),
    });
  };

  // UPDATE
  const toggleTodo = async (id, completed) => {
    await db.todos.update(id, {
      completed: !completed,
    });
  };

  // DELETE
  const deleteTodo = async (id) => {
    await db.todos.delete(id);
  };

  return {
    todos,
    addTodo,
    toggleTodo,
    deleteTodo,
  };
};
```

এখন আমাদের CRUD:

```text
CREATE → addTodo()
READ   → useLiveQuery()
UPDATE → toggleTodo()
DELETE → deleteTodo()
```

Component সরাসরি Dexie নিয়ে কাজ করবে না।

---

# 3️⃣ `components/TodoForm.jsx`

এটার কাজ শুধু **new Todo input নেওয়া**।

```jsx
import { useState } from "react";

function TodoForm({ onAdd }) {
  const [title, setTitle] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();

    if (!title.trim()) return;

    await onAdd(title);

    setTitle("");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        placeholder="Enter todo..."
      />

      <button type="submit">
        Add Todo
      </button>
    </form>
  );
}

export default TodoForm;
```

এখানে একটা important জিনিস:

```jsx
<TodoForm onAdd={addTodo} />
```

মানে parent থেকে `addTodo` function আসছে।

---

# 4️⃣ `components/TodoItem.jsx`

একটা single Todo কীভাবে দেখাবে সেটা এখানে থাকবে।

```jsx
function TodoItem({
  todo,
  onToggle,
  onDelete,
}) {
  return (
    <div>
      <input
        type="checkbox"
        checked={todo.completed}
        onChange={() =>
          onToggle(todo.id, todo.completed)
        }
      />

      <span
        style={{
          textDecoration: todo.completed
            ? "line-through"
            : "none",
        }}
      >
        {todo.title}
      </span>

      <button
        onClick={() => onDelete(todo.id)}
      >
        Delete
      </button>
    </div>
  );
}

export default TodoItem;
```

এই component শুধু **একটা Todo** জানে।

Database সম্পর্কে কিছু জানে না।

---

# 5️⃣ `components/TodoList.jsx`

এখানে সব Todo map হবে।

```jsx
import TodoItem from "./TodoItem";

function TodoList({
  todos,
  onToggle,
  onDelete,
}) {
  if (!todos) {
    return <p>Loading...</p>;
  }

  if (todos.length === 0) {
    return <p>No todos found.</p>;
  }

  return (
    <div>
      {todos.map((todo) => (
        <TodoItem
          key={todo.id}
          todo={todo}
          onToggle={onToggle}
          onDelete={onDelete}
        />
      ))}
    </div>
  );
}

export default TodoList;
```

এখানে:

```jsx
todos.map(...)
```

প্রতিটা Todo-এর জন্য:

```jsx
<TodoItem />
```

তৈরি করছে।

---

# 6️⃣ `pages/Todos.jsx`

এখন সবচেয়ে interesting part।

এই page সবকিছুকে connect করবে।

```jsx
import TodoForm from "../components/TodoForm";
import TodoList from "../components/TodoList";
import { useTodos } from "../hooks/useTodos";

function Todos() {
  const {
    todos,
    addTodo,
    toggleTodo,
    deleteTodo,
  } = useTodos();

  return (
    <div>
      <h1>My Todo App</h1>

      <TodoForm onAdd={addTodo} />

      <hr />

      <TodoList
        todos={todos}
        onToggle={toggleTodo}
        onDelete={deleteTodo}
      />
    </div>
  );
}

export default Todos;
```

এখানে আমরা প্রথমবার পুরো flow দেখতে পাচ্ছি।

```text
Todos.jsx
   │
   ├── useTodos()
   │      ↓
   │    Dexie
   │      ↓
   │   IndexedDB
   │
   ├── TodoForm
   │
   └── TodoList
```

---

# 7️⃣ `App.jsx`

এখন `App.jsx` খুব simple হবে।

```jsx
import Todos from "./pages/Todos";

function App() {
  return (
    <div>
      <Todos />
    </div>
  );
}

export default App;
```

`App` এখন শুধু application-এর main pages manage করবে।

---

# 8️⃣ `main.jsx`

এটা React application-এর **entry point**।

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

import App from "./App";

import "./index.css";

ReactDOM.createRoot(
  document.getElementById("root")
).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```

এখান থেকে:

```text
main.jsx
   ↓
App.jsx
   ↓
Todos.jsx
```

---

# ⚠️ একটা package লাগবে

যেহেতু আমরা `useLiveQuery()` ব্যবহার করছি:

```bash
npm install dexie dexie-react-hooks
```

---

# 🧩 এখন পুরো application flow

ধরো তুমি input-এ লিখলে:

```text
Learn Dexie
```

তারপর Add চাপলে:

```text
TodoForm
    ↓
onAdd(title)
    ↓
addTodo()
    ↓
db.todos.add()
    ↓
IndexedDB
    ↓
useLiveQuery()
    ↓
todos update
    ↓
TodoList
    ↓
TodoItem
    ↓
UI
```

এটা খুব ভালো করে মাথায় বসিয়ে নাও।

---

# 🔥 Delete করলে

```text
Delete button
      ↓
TodoItem
      ↓
onDelete(todo.id)
      ↓
deleteTodo()
      ↓
db.todos.delete(id)
      ↓
IndexedDB
      ↓
useLiveQuery()
      ↓
UI update
```

---

# 🔥 Checkbox click করলে

```text
Checkbox
   ↓
onToggle(id, completed)
   ↓
toggleTodo()
   ↓
db.todos.update()
   ↓
IndexedDB
   ↓
useLiveQuery()
   ↓
UI update
```

---

# 📁 Final structure

শেষে তোমার project হবে:

```text
react-dexie-crud/
│
├── node_modules/
│
├── public/
│
├── src/
│   │
│   ├── components/
│   │   ├── TodoForm.jsx
│   │   ├── TodoList.jsx
│   │   └── TodoItem.jsx
│   │
│   ├── db/
│   │   └── db.js
│   │
│   ├── hooks/
│   │   └── useTodos.js
│   │
│   ├── pages/
│   │   └── Todos.jsx
│   │
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
│
├── package.json
└── vite.config.js
```

## 🧠 সবচেয়ে গুরুত্বপূর্ণ rule

প্রতিটা file-এর একটা নির্দিষ্ট দায়িত্ব রাখো:

```text
db.js
→ Database

useTodos.js
→ Data + CRUD logic

TodoForm.jsx
→ Input

TodoItem.jsx
→ Single Todo UI

TodoList.jsx
→ Todo list UI

Todos.jsx
→ Components + Hook connect

App.jsx
→ Application structure

main.jsx
→ React entry point
```

এভাবে practice করলে শুধু **Dexie** না, একই সাথে **React component architecture, props, custom hooks, CRUD এবং separation of concerns**—সবগুলো একসাথে solid হবে।

---
