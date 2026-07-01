React-এর **Virtual DOM** আর **Diffing Algorithm** একসাথে কাজ করে fast UI update করার জন্য।

---

# DOM কী?

DOM = **Document Object Model**

Browser HTML কে tree structure বানায়।

Example:

```html
<div>
  <h1>Hello</h1>
  <button>Save</button>
</div>
```

DOM tree:

```text
div
 ├── h1
 └── button
```

Real DOM update expensive কারণ:

- repaint
    
- reflow
    
- layout recalculation
    

---

# Virtual DOM কী?

Virtual DOM হলো **Real DOM-এর lightweight JavaScript copy**।

React memory-তে একটা object tree রাখে।

Example:

```jsx
<h1>Hello</h1>
```

Approx internal object:

```js
{
  type: "h1",
  props: {
    children: "Hello"
  }
}
```

এটা browser DOM না—just JS object।

---

# কেন দরকার?

ধরো counter app:

```jsx
<h1>Count: 0</h1>
```

button click:

```jsx
<h1>Count: 1</h1>
```

Naive approach:

- পুরো DOM rebuild
    

React করে না।

সে compare করে:

Old Virtual DOM:

```text
Count: 0
```

New Virtual DOM:

```text
Count: 1
```

Difference detect করে।

---

# Diffing Algorithm কী?

Diffing algorithm = **old virtual DOM vs new virtual DOM compare করা**

Goal:

> Minimum number of real DOM updates

---

## Render cycle

### Step 1

State change

```jsx
setCount(count + 1)
```

↓

### Step 2

Component re-render

New virtual DOM তৈরি

↓

### Step 3

Diffing

Old vs New compare

↓

### Step 4

Reconciliation

Only changed part real DOM-এ patch

---

# Example 1: Text Change

Old:

```jsx
<h1>Hello</h1>
```

New:

```jsx
<h1>Hi</h1>
```

React sees:

- Tag same (`h1`)
    
- Text changed
    

Only text update.

---

# Example 2: Attribute Change

Old:

```jsx
<button className="blue">
```

New:

```jsx
<button className="red">
```

React updates only class attribute।

---

# Example 3: Element Type Changed

Old:

```jsx
<div>Hello</div>
```

New:

```jsx
<span>Hello</span>
```

Type different:

- div ≠ span
    

React subtree destroy + recreate।

---

# React Diffing Rules

React O(n³) tree comparison করে না (too slow)।

Heuristics use করে → প্রায় O(n)

Main assumptions:

---

## Rule 1: Different types = replace subtree

```jsx
<div />
```

→

```jsx
<span />
```

Replace everything.

---

## Rule 2: Same type = compare props

```jsx
<input value="a" />
```

↓

```jsx
<input value="b" />
```

Only prop update.

---

## Rule 3: Children compare by order + key

List-এ important।

---

# Key কেন লাগে?

ধরো list:

Old:

```jsx
<li>A</li>
<li>B</li>
```

New:

```jsx
<li>X</li>
<li>A</li>
<li>B</li>
```

Without key React confuse হতে পারে।

With key:

```jsx
items.map(item =>
  <li key={item.id}>{item.name}</li>
)
```

React বুঝে:

- A same
    
- B same
    
- X new
    

---

# Reconciliation

Diff শেষে actual DOM patch process = **Reconciliation**

React decides:

- create
    
- delete
    
- move
    
- update
    

---

# Virtual DOM কি সবসময় fast?

সবসময় না।

Misconception:

> “Virtual DOM মানেই fastest”

না।

Extra work হয়:

- create virtual tree
    
- diff tree
    

কিছু framework (যেমন Svelte) compile-time optimize করে।

React fast কারণ:

- batching
    
- scheduling
    
- selective updates
    

---

# Simple Flow

```text
State changes
    ↓
Component re-render
    ↓
New Virtual DOM
    ↓
Diff algorithm
    ↓
Minimal DOM update
```

---

# Real Example

```jsx
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

Button click করলে:

Re-render হয়, কিন্তু:

- button unchanged
    
- div unchanged
    
- only `<h1>` text updated
    

---

এক লাইনে:

**Virtual DOM = UI-এর JS copy**  
**Diff Algorithm = old vs new compare করে minimal DOM update বের করা**  
**Reconciliation = সেই update real DOM-এ apply করা**

----------

**Actual DOM / Real DOM** হলো browser-এর আসল DOM — যেটা browser render করে এবং user screen-এ দেখে।

সহজভাবে:

> HTML parse করে browser যে live tree বানায়, সেটাই Actual DOM।

Example:

```html
<body>
  <div>
    <h1>Hello</h1>
    <button>Click</button>
  </div>
</body>
```

Browser internally tree বানায়:

```text
Document
 └── body
      └── div
           ├── h1
           └── button
```

এটাই Real / Actual DOM।

---

## Actual DOM-এর properties

### 1) Mutable (directly change করা যায়)

JavaScript দিয়ে:

```js
document.querySelector("h1").innerText = "Hi";
```

Real DOM immediately update।

---

### 2) Live object

DOM static copy না—live structure।

যদি নতুন element add করো:

```js
const p = document.createElement("p");
document.body.appendChild(p);
```

DOM tree change হয়ে যায়।

---

### 3) Browser rendering-এর সাথে connected

DOM change ⇒ browser often করে:

- Style recalculation
    
- Layout (Reflow)
    
- Paint
    
- Composite
    

এই steps costly হতে পারে।

---

# Problem: কেন slow হতে পারে?

ধরো 5000 item list আছে।

তুমি repeatedly:

```js
element.style.width = "100px";
element.style.height = "200px";
```

অনেক DOM manipulation করলে:

- CPU usage বাড়ে
    
- UI lag করতে পারে
    

কারণ browser বারবার recalculate করে।

---

# React context

Without React:

```js
document.getElementById("counter").innerText = count;
```

সব manually manage করতে হয়।

React with Virtual DOM:

- memory-তে compare
    
- changed part only update
    
- Actual DOM-এ minimal patch
    

---

## Actual DOM vs Virtual DOM

|Feature|Actual DOM|Virtual DOM|
|---|---|---|
|Exists where?|Browser|JS memory|
|Speed|Slow updates|Faster diff|
|Update|Direct|Indirect|
|Cost|High|Lower|

---

Example:

Actual DOM node:

```html
<h1>Hello</h1>
```

Virtual DOM representation:

```js
{
  type: "h1",
  props: {
    children: "Hello"
  }
}
```

---

এক লাইনে:

**Actual DOM = browser-এর আসল live UI tree, যেটা directly screen render করে।**


-------
