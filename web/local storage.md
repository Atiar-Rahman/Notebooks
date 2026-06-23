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

