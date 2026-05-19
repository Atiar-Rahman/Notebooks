ভালো প্রশ্ন 🔥 — **TanStack Query (React Query)** কেন use করা হয়, এটা বুঝলে তুমি frontend এ একদম next level এ চলে যাবে।

---

# 🧠 🔥 TanStack Query কী?

👉 TanStack Query হলো একটা **data fetching + caching library**

👉 সহজভাবে:
**API data manage করার smart system**

---

# 😵 Problem Without TanStack Query

React + Axios দিয়ে তুমি normally এমন করো:

```javascript
const [data, setData] = useState([]);
const [loading, setLoading] = useState(false);

useEffect(() => {
  setLoading(true);

  axios.get("/api/todos/")
    .then(res => setData(res.data))
    .finally(() => setLoading(false));
}, []);
```

---

## ❌ Problem গুলো

* বারবার same API call 😓
* manual loading state 😓
* error handle manually 😓
* caching নাই 😓
* refetch control নাই 😓

👉 বড় project এ এটা nightmare 😵

---

# 🚀 TanStack Query Solution

```javascript
import { useQuery } from "@tanstack/react-query";

const { data, isLoading, error } = useQuery({
  queryKey: ["todos"],
  queryFn: () => api.get("/api/todos/").then(res => res.data),
});
```

---

## 😍 Magic কী?

👉 TanStack Query automatically:

✅ API call করে
✅ loading handle করে
✅ error handle করে
✅ caching করে
✅ refetch manage করে

---

# ⚡ Key Benefits (Real SaaS)

## 🔁 1. Auto Caching

👉 same API বারবার call করবে না

---

## 🔄 2. Auto Refetch

👉 tab change করলে আবার data fresh হবে

---

## ⚡ 3. Background Update

👉 user কিছু বুঝে না — silently update হয়

---

## 🧠 4. Server State Management

👉 Redux লাগবে না অনেক ক্ষেত্রে

---

# 📊 Before vs After

| Feature    | Axios only | TanStack Query |
| ---------- | ---------- | -------------- |
| Loading    | manual     | auto           |
| Error      | manual     | auto           |
| Cache      | ❌          | ✅              |
| Refetch    | ❌          | ✅              |
| Clean code | ❌          | ✅              |

---

# 🧩 Mutation (POST / DELETE)

👉 শুধু GET না — create/update/delete ও handle করে

```javascript
import { useMutation } from "@tanstack/react-query";

const mutation = useMutation({
  mutationFn: (newTodo) => api.post("/api/todos/", newTodo),
});
```

---

# 🔥 Example: File Upload

```javascript
const uploadMutation = useMutation({
  mutationFn: (formData) =>
    api.post("/upload/", formData),

  onSuccess: () => {
    alert("Uploaded!");
  },
});
```

---

# 🎯 When You Should Use It

👉 Use TanStack Query when:

* API heavy app
* dashboard / SaaS
* real-time data
* multiple API calls

---

# ❌ When NOT needed

👉 small project হলে দরকার নাই

---

# 🧠 Simple Analogy

👉 Axios = bike 🏍️
👉 TanStack Query = Tesla 🚗⚡

👉 দুটোই যায়, কিন্তু one is smart system

---

# 💥 Final Summary

👉 TanStack Query use করা হয়:

✔ API call সহজ করতে
✔ loading/error auto handle করতে
✔ caching improve করতে
✔ clean scalable code বানাতে

---

# 🚀 Next Step (Highly Recommended)

👉 তুমি যদি serious frontend dev হও:

* TanStack Query + Axios integrate
* Query invalidation (very important)
* Pagination + infinite scroll

---

ঠিক আছে 🔥 — আমি তোমাকে **TanStack Query (React Query) একদম beginner থেকে full production-ready example** দেখাচ্ছি, step by step, যাতে তুমি সব বুঝো।

আমরা ধরে নিই **React + Axios + DRF backend** (JWT auth included)।

---

# 1️⃣ Install Required Packages

```bash
npm install @tanstack/react-query axios
```

---

# 2️⃣ Axios Setup (api.js)

```javascript
// api.js
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:8000",
});

// Add JWT automatically
api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

export default api;
```

---

# 3️⃣ React Query Provider Setup

TanStack Query ব্যবহার করতে হলে **QueryClientProvider** দরকার:

```javascript
// main.jsx
import React from "react";
import ReactDOM from "react-dom";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import App from "./App";

const queryClient = new QueryClient();

ReactDOM.render(
  <QueryClientProvider client={queryClient}>
    <App />
  </QueryClientProvider>,
  document.getElementById("root")
);
```

---

# 4️⃣ Basic GET Query Example (Fetch Todos)

```javascript
// Todos.jsx
import React from "react";
import { useQuery } from "@tanstack/react-query";
import api from "./api";

const fetchTodos = async () => {
  const res = await api.get("/api/todos/");
  return res.data;
};

export default function Todos() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodos,
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error occurred!</p>;

  return (
    <ul>
      {data.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}
```

✅ Automatic caching, loading, error handling included.

---

# 5️⃣ POST / Mutation Example (Add Todo)

```javascript
import React, { useState } from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";
import api from "./api";

export default function AddTodo() {
  const [title, setTitle] = useState("");
  const queryClient = useQueryClient();

  const addTodo = useMutation({
    mutationFn: (newTodo) => api.post("/api/todos/", newTodo),
    onSuccess: () => {
      // Refetch todos automatically
      queryClient.invalidateQueries(["todos"]);
    },
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    addTodo.mutate({ title });
    setTitle("");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={title}
        onChange={(e) => setTitle(e.target.value)}
        placeholder="New Todo"
      />
      <button type="submit">Add</button>
    </form>
  );
}
```

---

# 6️⃣ DELETE Mutation Example

```javascript
export default function DeleteTodo({ todoId }) {
  const queryClient = useQueryClient();

  const deleteTodo = useMutation({
    mutationFn: () => api.delete(`/api/todos/${todoId}/`),
    onSuccess: () => {
      queryClient.invalidateQueries(["todos"]);
    },
  });

  return <button onClick={() => deleteTodo.mutate()}>Delete</button>;
}
```

---

# 7️⃣ File Upload with Mutation

```javascript
import React from "react";
import { useMutation, useQueryClient } from "@tanstack/react-query";
import api from "./api";

export default function UploadFile() {
  const queryClient = useQueryClient();

  const upload = useMutation({
    mutationFn: (file) => {
      const formData = new FormData();
      formData.append("file", file);
      return api.post("/upload/", formData);
    },
    onSuccess: () => {
      queryClient.invalidateQueries(["files"]);
      alert("Uploaded!");
    },
  });

  const handleUpload = (e) => {
    upload.mutate(e.target.files[0]);
  };

  return <input type="file" onChange={handleUpload} />;
}
```

---

# 8️⃣ Infinite / Pagination Example (Advanced)

```javascript
import { useInfiniteQuery } from "@tanstack/react-query";

const fetchTodos = ({ pageParam = 1 }) =>
  api.get(`/api/todos/?page=${pageParam}`).then((res) => res.data);

const { data, fetchNextPage, hasNextPage } = useInfiniteQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
  getNextPageParam: (lastPage, pages) => lastPage.nextPage ?? false,
});
```

✅ Automatically handles pages, refetch, caching.

---

# 9️⃣ Key Benefits Recap

* 🔹 **Auto caching**
* 🔹 **Loading & error state automatically**
* 🔹 **Easy refetch / invalidation**
* 🔹 **Mutation handling (POST/DELETE/UPDATE)**
* 🔹 **Infinite scroll / pagination**
* 🔹 **Cleaner, maintainable code**

---

# 10️⃣ Pro Tip (SaaS-ready)

1. Create **api.js** for Axios + JWT
2. Wrap app in **QueryClientProvider**
3. Use `useQuery` for GET
4. Use `useMutation` for POST/PUT/DELETE/Upload
5. Use `invalidateQueries` after mutation
6. Add loading spinners & error UI

---

💡 **TL;DR:**
TanStack Query + Axios = **fully reactive, cached, clean API system** for React.

---

