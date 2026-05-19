Here’s a clean way to **store a token in localStorage and use it in fetch requests** (React / Next.js client side).

---

# 🔐 1. Save token after login

Example after API response:

```js id="t1"
const res = await fetch("/api/login", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
});

const result = await res.json();

// save token
localStorage.setItem("token", result.token);
```

---

# 📤 2. Use token in future fetch requests

```js id="t2"
const token = localStorage.getItem("token");

const res = await fetch("/api/protected-route", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
});

const data = await res.json();
console.log(data);
```

---

# 🧠 3. POST request with token

```js id="t3"
const token = localStorage.getItem("token");

await fetch("/api/register", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
  },
  body: JSON.stringify(payload),
});
```

---

# ⚠️ Important notes

## ❌ localStorage is client-only

* Works only in browser
* NOT available in server components (Next.js SSR)

---

## ❌ Security warning

localStorage is:

* readable by JS
* vulnerable to XSS attacks

👉 Better for simple apps
👉 For secure apps: use **httpOnly cookies**

---

# 🧠 Best practice structure

### 1. Create helper function

```js id="t4"
export const getToken = () => {
  return localStorage.getItem("token");
};
```

---

### 2. Reusable fetch wrapper

```js id="t5"
export const authFetch = async (url, options = {}) => {
  const token = localStorage.getItem("token");

  return fetch(url, {
    ...options,
    headers: {
      "Content-Type": "application/json",
      Authorization: `Bearer ${token}`,
      ...options.headers,
    },
  });
};
```

---

### Usage:

```js id="t6"
const res = await authFetch("/api/user");
const data = await res.json();
```

---

# 🚀 Final answer

✔ Store token → `localStorage.setItem()`
✔ Get token → `localStorage.getItem()`
✔ Send token → `Authorization: Bearer <token>`

---

If you want next step, I can show:
✔ Axios interceptor version (cleaner than fetch)
✔ Next.js secure auth with httpOnly cookies (production-grade)
✔ or Django JWT backend setup for this flow
