## 💾 Local Storage in JavaScript (Set & Read Simple Values)

👉 **Local Storage** is a browser feature used to store data **permanently (until manually cleared)**.

---

# 🧠 Key Features

- Stores data in **key-value pairs**
    
- Data stays even after page refresh 🔄
    
- Only stores **strings**
    
- Works in browser only 🌐
    

---

# 📥 1. Set Value in Local Storage

👉 Use `setItem()`

```javascript
localStorage.setItem("name", "Alex");
```

---

## 🧠 Syntax:

```javascript
localStorage.setItem("key", "value");
```

---

# 📤 2. Read Value from Local Storage

👉 Use `getItem()`

```javascript
const name = localStorage.getItem("name");

console.log(name);
```

### Output:

```text
Alex
```

---

# 🧠 3. Simple Full Example

```javascript
localStorage.setItem("city", "Dhaka");

const city = localStorage.getItem("city");

console.log(city);
```

---

# 🔁 4. Update Value

👉 Just overwrite it

```javascript
localStorage.setItem("name", "John");
localStorage.setItem("name", "Mike");

console.log(localStorage.getItem("name"));
```

### Output:

```text
Mike
```

---

# ❌ 5. Remove Item

👉 Use `removeItem()`

```javascript
localStorage.removeItem("name");
```

---

# 🧹 6. Clear All Storage

```javascript
localStorage.clear();
```

---

# 🧠 7. Important Rule

👉 Local storage only stores **strings**

### Wrong:

```javascript
localStorage.setItem("user", { name: "Alex" });
```

👉 becomes:

```text
[object Object]
```

---

## ✅ Correct way (use JSON)

### Store object:

```javascript
const user = {
  name: "Alex",
  age: 20
};

localStorage.setItem("user", JSON.stringify(user));
```

---

### Read object:

```javascript
const data = localStorage.getItem("user");

const userObj = JSON.parse(data);

console.log(userObj.name);
```

### Output:

```text
Alex
```

---

# ⚡ 8. Local Storage Methods Summary

|Method|Purpose|
|---|---|
|setItem()|Save data|
|getItem()|Read data|
|removeItem()|Delete one item|
|clear()|Delete all|

---

# 🧠 9. Real-Life Analogy

👉 Local Storage = notebook 📒

- Write data → storeItem
    
- Read data → getItem
    
- Erase page → removeItem
    

---

# 🚀 Final Summary

```javascript
// Save data
localStorage.setItem("key", "value");

// Read data
localStorage.getItem("key");

// Delete data
localStorage.removeItem("key");

// Clear all
localStorage.clear();
```

---

# 🧠 One-line memory:

👉 **LocalStorage = browser memory that stores key-value data permanently**

---

# **localStorage-এ array রাখা যায়**। তবে সরাসরি array রাখা যায় না, কারণ `localStorage` শুধু **string** হিসেবে data store করে।

তাই `JSON.stringify()` ব্যবহার করবে।

### Array save করা

```js
const users = ["Rahim", "Karim", "Hasan"];

localStorage.setItem("users", JSON.stringify(users));
```

### Array বের করা

```js
const users = JSON.parse(
  localStorage.getItem("users")
);

console.log(users);
```

Output:

```js
["Rahim", "Karim", "Hasan"]
```

### Object-এর array-ও রাখা যায়

```js
const users = [
  { id: 1, name: "Rahim" },
  { id: 2, name: "Karim" }
];

localStorage.setItem("users", JSON.stringify(users));
```

পরে:

```js
const users = JSON.parse(
  localStorage.getItem("users")
);

console.log(users[0].name);
```

Output:

```text
Rahim
```

### 🧠 শুধু এই pattern মনে রাখো

```text
JavaScript Array
      ↓
JSON.stringify()
      ↓
localStorage
```

আর বের করার সময়:

```text
localStorage
      ↓
JSON.parse()
      ↓
JavaScript Array
```

**একটা common mistake:**

```js
localStorage.setItem("users", users); // ❌
```

এতে array সাধারণত string হিসেবে `"Rahim,Karim,Hasan"` হয়ে যাবে।

সঠিক:

```js
localStorage.setItem("users", JSON.stringify(users)); // ✅
```

---
# **Second time-এ existing array বের করে `push()` করে আবার `localStorage`-এ save করতে হবে।**

ধরো প্রথমবার:

```js
const users = ["Rahim", "Karim"];

localStorage.setItem("users", JSON.stringify(users));
```

এখন second time-এ `"Hasan"` add করতে চাও:

```js
const users = JSON.parse(
  localStorage.getItem("users")
);

users.push("Hasan");

localStorage.setItem(
  "users",
  JSON.stringify(users)
);
```

এখন localStorage-এ থাকবে:

```js
["Rahim", "Karim", "Hasan"]
```

### আরও clean করে function বানাতে পারো

```js
function addUser(user) {
  const users = JSON.parse(
    localStorage.getItem("users") || "[]"
  );

  users.push(user);

  localStorage.setItem(
    "users",
    JSON.stringify(users)
  );
}
```

তারপর:

```js
addUser("Rahim");
addUser("Karim");
addUser("Hasan");
```

শেষে:

```js
console.log(
  JSON.parse(localStorage.getItem("users"))
);
```

Output:

```js
["Rahim", "Karim", "Hasan"]
```

### 🧠 পুরো process

```text
localStorage
     ↓
JSON.parse()
     ↓
Array
     ↓
push()
     ↓
JSON.stringify()
     ↓
localStorage
```

**Important:** `localStorage.getItem()` থেকে পাওয়া value সরাসরি `.push()` করতে পারবে না, কারণ সেটা string। আগে `JSON.parse()` করতে হবে।

----
# `sessionStorage`-কে অনেকটা `localStorage`-এর **temporary version** ভাবতে পারো।

API methods প্রায় একই:

```js
localStorage.setItem()
localStorage.getItem()
localStorage.removeItem()
localStorage.clear()
```

এর জায়গায়:

```js
sessionStorage.setItem()
sessionStorage.getItem()
sessionStorage.removeItem()
sessionStorage.clear()
```

Array-এর ক্ষেত্রেও একই:

```js
const users = JSON.parse(
  sessionStorage.getItem("users") || "[]"
);

users.push("Hasan");

sessionStorage.setItem(
  "users",
  JSON.stringify(users)
);
```

### শুধু মূল difference 🧠

```text
localStorage
→ Data persist করে
→ Tab/browser বন্ধ করলেও সাধারণত থাকে

sessionStorage
→ Current tab/session-এর জন্য
→ Tab বন্ধ করলে data চলে যায়
```

তাই তুমি চাইলে মনে রাখতে পারো:

> **sessionStorage = localStorage-এর same API, কিন্তু temporary storage।** ✅

একটা ছোট nuance: `sessionStorage` **প্রতিটি browser tab-এর জন্য আলাদা**, তাই এক tab-এর sessionStorage অন্য tab-এ automatically share হয় না।


----
# Browser devtool niye describe
হ্যাঁ 👍 তোমার screenshot-এ Chrome DevTools-এর **Application → Storage** section দেখা যাচ্ছে। এগুলোর প্রত্যেকটার আলাদা কাজ আছে।

### সবচেয়ে important ৫টা আগে বুঝো

|Storage|কী কাজে use হয়|Data কতক্ষণ থাকে|
|---|---|---|
|**Local Storage**|ছোট persistent data|সাধারণত browser থেকে manually clear না করা পর্যন্ত|
|**Session Storage**|temporary/tab-specific data|Tab বন্ধ করলে চলে যায়|
|**Cookies**|ছোট data, বিশেষ করে authentication/session|expiry অনুযায়ী|
|**IndexedDB**|বড়/complex structured data|persistent|
|**Cache Storage**|HTTP response/assets cache করা|cache policy অনুযায়ী|

---

### 1. Local Storage ⭐

Frontend-এ ছোট data রাখতে খুব common।

```js
localStorage.setItem("theme", "dark");

const theme = localStorage.getItem("theme");
```

যেমন:

- Theme preference
    
- Language preference
    
- কিছু user settings
    
- ছোট JSON/array
    

```js
localStorage.setItem(
  "cart",
  JSON.stringify(cart)
);
```

---

### 2. Session Storage

`localStorage`-এর মতো API, কিন্তু **current browser tab/session-এর জন্য**।

```js
sessionStorage.setItem("step", "2");

const step = sessionStorage.getItem("step");
```

যেমন:

- Multi-step form-এর temporary data
    
- Current tab-এর temporary state
    
- কিছু temporary UI information
    

Tab বন্ধ করলে সাধারণত data চলে যায়।

---

### 3. Cookies 🍪

Cookies-এর সবচেয়ে important use হলো **server-এর সাথে ছোট data পাঠানো**।

বিশেষ করে authentication/session-এর ক্ষেত্রে cookies খুব common।

```text
Browser
   ↓ Cookie
Server
```

Cookie-তে options থাকে যেমন:

- `HttpOnly`
    
- `Secure`
    
- `SameSite`
    
- `Expires / Max-Age`
    

Authentication architecture-এ **HttpOnly cookie** ব্যবহার করলে JavaScript সরাসরি সেই cookie পড়তে পারে না—এটা security-এর জন্য গুরুত্বপূর্ণ।

---

### 4. IndexedDB

এটা `localStorage`-এর তুলনায় অনেক বেশি powerful।

ব্যবহার করতে পারো:

- বড় amount of structured data
    
- Offline applications
    
- অনেক records
    
- complex objects
    
- client-side database-এর মতো কাজ
    

Example concept:

```text
IndexedDB
 ├── users
 ├── products
 ├── orders
 └── messages
```

সাধারণ beginner React app-এ শুরুতেই IndexedDB দরকার হয় না।

---

### 5. Cache Storage

এটা মূলত **network response/assets cache** করার জন্য।

বিশেষ করে:

```text
Service Worker
      ↓
Cache Storage
      ↓
Cached API responses / files
```

PWA/offline web app-এ বেশি দেখা যায়।

---

### Screenshot-এর বাকি যেগুলো আছে

**Extension storage**  
Chrome extension-এর নিজস্ব storage। Normal React website-এর জন্য সাধারণত দরকার নেই।

**Shared Storage**  
Web-এর কিছু privacy-focused use case-এর জন্য। Beginner হিসেবে এখন ignore করতে পারো।

**Cache Storage**  
উপরের ৫ নম্বরটাই।

**Storage Buckets**  
Browser storage-কে আলাদা bucket হিসেবে organize/manage করার newer browser capability। Beginner React-এর জন্য এখন priority না।

---

### 🧠 তোমার জন্য এখন এই mapping-টাই মনে রাখো

```text
ছোট persistent data
        ↓
   localStorage

শুধু current tab-এর temporary data
        ↓
   sessionStorage

Server ↔ Browser ছোট data / auth session
        ↓
     Cookies

বড় structured client-side data
        ↓
     IndexedDB

Network response / offline cache
        ↓
   Cache Storage
```

**React developer হিসেবে শুরুতে:** `localStorage` + `sessionStorage` + `cookies` ভালোভাবে শেখো। তারপর `IndexedDB` এবং `Cache Storage` শেখা যথেষ্ট।

