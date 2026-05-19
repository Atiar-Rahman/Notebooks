
---

# 📅 Day 1 – ES6 Core (FULL DEEP GUIDE)

---

## 1️⃣ `let` / `const` (Scope – DEEP)

---

### 🔹 WHAT?

`let` ও `const` হল **block-scoped variable**।

```js
{
  let x = 10;
  const y = 20;
}
```

❌ বাইরে থেকে `x`, `y` পাওয়া যাবে না

---

### 🔹 WHY not `var`?

`var` **function scoped**, bug তৈরি করে।

```js
if (true) {
  var a = 5;
}
console.log(a); // 5 😱
```

➡️ React-এ এটা **dangerous**

---

### 🔹 HOW `let` works?

- Re-assign করা যায়
    
- Re-declare করা যায় না (same scope)
    

```js
let count = 1;
count = 2; // ✅
```

---

### 🔹 HOW `const` works?

- Re-assign ❌
    
- **Mutation allowed** (important!)
    

```js
const user = { name: "Rahman" };
user.name = "Atiar"; // ✅
```

❌

```js
user = {} // error
```

---

### 🔹 WHERE in React?

```jsx
const [count, setCount] = useState(0);
```

👉 `count` কখনো reassigned হয় না → তাই `const`

---

### ❓ Interview Q

**Q:** Why React uses `const` mostly?  
**A:** Because React follows immutability & reference safety.

---

## 2️⃣ Arrow Function (this issue – MOST IMPORTANT)

---

### 🔹 WHAT?

Arrow function হলো **short syntax function** যা নিজের `this` তৈরি করে না।

```js
const add = (a, b) => a + b;
```

---

### 🔹 HOW `this` works in normal function?

```js
const obj = {
  name: "React",
  show: function () {
    console.log(this.name);
  }
}
```

✔️ works

---

### 🔹 Arrow function breaks `this`?

```js
const obj = {
  name: "React",
  show: () => {
    console.log(this.name);
  }
}
```

❌ undefined

➡️ Arrow function **lexical this** নেয় (parent scope থেকে)

---

### 🔹 WHY React prefers arrow?

React functional component এ `this` দরকারই হয় না।

```jsx
const Button = () => {
  return <button>Click</button>;
};
```

✔️ Simple  
✔️ No binding  
✔️ Clean code

---

### 🔹 WHERE in React?

- Components
    
- Event handlers
    
- Callbacks
    

```jsx
<button onClick={() => setCount(count + 1)}>+</button>
```

---

### ❓ Interview Q

**Q:** Why arrow function is best for React?  
**A:** No `this` confusion + shorter syntax.

---

## 3️⃣ Template Literal (Dynamic UI Builder)

---

### 🔹 WHAT?

Backtick `` ` ``, dynamic string build করা যায়।

```js
`Hello ${name}`
```

---

### 🔹 WHY not `" "`?

```js
"Hello " + name + "!"
```

❌ ugly  
❌ unreadable

---

### 🔹 HOW?

```js
const user = "Atiar";
const msg = `Welcome ${user}`;
```

---

### 🔹 WHERE in React?

```jsx
<h1>{`Hello ${user.name}`}</h1>
```

```jsx
className={`btn ${isActive ? "active" : ""}`}
```

🔥 VERY COMMON

---

### ❓ Interview Q

**Q:** Why template literal is important in JSX?  
**A:** Dynamic className & text rendering.

---

## 4️⃣ Default Parameter (Safe Function)

---

### 🔹 WHAT?

Parameter না দিলে default value নেয়।

```js
function add(a = 0, b = 0) {
  return a + b;
}
```

---

### 🔹 WHY needed?

React component props sometimes missing।

---

### 🔹 HOW?

```js
const greet = (name = "Guest") => {
  return `Hello ${name}`;
};
```

---

### 🔹 WHERE in React?

```jsx
const Button = ({ text = "Click" }) => {
  return <button>{text}</button>;
};
```

➡️ UI break হয় না

---

### ❓ Interview Q

**Q:** Default parameter vs props default?  
**A:** Both prevent undefined error.

---

## 🧠 COMMON CONFUSION (IMPORTANT)

### ❓ const + object change = how?

Because **reference same থাকে**, value mutate হয়।

```js
const a = {};
const b = a;
b.name = "X";
```

---

## 🔥 MINI PRACTICE (Must Do)

```js
const user = {
  name: "Atiar",
  greet: () => `Hello ${this.name}`
};
console.log(user.greet());
```

❓ Output কেন undefined?

---

## 🎯 React Mapping Summary

|ES6|React Use|
|---|---|
|let|loop / temp variable|
|const|state, props|
|arrow|component|
|template literal|JSX|
|default param|safe props|

---

## ✅ Day 1 COMPLETE

তুমি এখন পারবে:

- React code বুঝতে
    
- Interview প্রশ্ন handle করতে
    
- Bug avoid করতে
    

---

👉 **Next:**  
**Day 2 – Array & Object (map, filter, reduce, spread, destructuring)**  
বললেই আমি same level deep এ করে দিচ্ছি 🔥