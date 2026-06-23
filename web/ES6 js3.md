## ⚙️ JavaScript Engine (V8), Execution Context & Call Stack

These 3 concepts explain **how JavaScript actually runs your code behind the scenes**.

---

# 🚀 1. JavaScript Engine (V8)

👉 A **JavaScript engine** is a program that runs JS code.

### 💡 Most popular engine:

## ⚡ V8 Engine (used in Chrome & Node.js)

---

## 🧠 What V8 does:

- Reads JavaScript code
    
- Converts it into machine code (very fast)
    
- Executes it
    

---

## 🔥 V8 Components:

### 1. Parser

👉 Breaks code into tokens

### 2. AST (Abstract Syntax Tree)

👉 Structured version of code

### 3. Compiler (JIT)

👉 Converts JS → machine code

### 4. Memory Heap

👉 Stores objects

### 5. Call Stack

👉 Executes functions (VERY IMPORTANT)

---

# 🧠 Simple Flow:

```text
JS Code → Parser → AST → Compiler → Machine Code → Runs
```

---

# 📦 2. Execution Context

👉 Execution Context = **environment where JS code runs**

Every time JS runs code, it creates an execution context.

---

## 🧠 Types of Execution Context:

### 1. Global Execution Context (GEC)

👉 Created when program starts

### 2. Function Execution Context (FEC)

👉 Created when function is called

---

# ⚡ Example:

```javascript
let x = 10;

function add() {
  let y = 20;
  console.log(x + y);
}

add();
```

---

## 🧠 What happens:

### Step 1: Global Execution Context created

- x = 10
    
- add() function stored
    

---

### Step 2: Function call creates new context

- add() runs
    
- y = 20
    
- prints result
    

---

# 🔥 Execution Context Phases:

## 1. Creation Phase

- Memory allocated
    
- Variables set to `undefined`
    

## 2. Execution Phase

- Code runs line by line
    

---

# 📚 Example:

```javascript
console.log(a);

var a = 5;
```

### Behind the scenes:

```javascript
var a; // creation phase
console.log(a); // undefined
a = 5; // execution phase
```

---

# 📦 3. Call Stack

👉 Call Stack = **stack of function calls**

It follows:

> LIFO (Last In, First Out)

---

# 🧠 Example:

```javascript
function first() {
  second();
}

function second() {
  console.log("Hello");
}

first();
```

---

## 🔥 Call Stack Flow:

```text
1. Global Context pushed
2. first() pushed
3. second() pushed
4. second() finished → removed
5. first() finished → removed
6. Global removed
```

---

# 📊 Visual Stack:

```text
Top →
second()
first()
Global
Bottom ↓
```

---

# ⚡ Real-Life Analogy

👉 Stack of plates 🍽️

- You add plate → push
    
- You remove top plate → pop
    
- Last plate added is removed first
    

---

# 🔥 How Everything Works Together

```text
Code → V8 Engine → Execution Context → Call Stack → Output
```

---

# 🧠 Key Concepts Summary

## ⚙️ V8 Engine

- Runs JavaScript
    
- Converts JS → machine code
    

---

## 📦 Execution Context

- Environment where code runs
    
- Has memory + execution phases
    

---

## 📚 Call Stack

- Manages function execution order
    
- Last in → first out (LIFO)
    

---

# 🚀 Final Simple Meaning

```javascript
// V8 = brain that runs JS

// Execution Context = workspace for code

// Call Stack = manager of function execution order
```

---

# 🔥 One-Line Memory

👉 **V8 runs JS, Execution Context prepares it, Call Stack executes it**

---


## 🧠 Single-Threaded, Synchronous vs Asynchronous (JavaScript)

These concepts explain **how JavaScript executes code step by step and handles waiting tasks**.

---

# 🧵 1. Single-Threaded JavaScript

👉 JavaScript runs on **one thread only**

### 💡 Meaning:

- Only **one task at a time**
    
- No parallel execution inside JS engine
    

---

## 🧠 Simple Idea:

```text
One line at a time → like a single-lane road 🚗
```

---

## 🔥 Example:

```javascript
console.log("A");
console.log("B");
console.log("C");
```

### Output:

```text
A
B
C
```

👉 Always runs in order

---

# ⏱️ 2. Synchronous (Sync)

👉 Code runs **line by line, in order**

👉 Next line waits for previous line to finish

---

## Example:

```javascript
console.log("Start");

console.log("Middle");

console.log("End");
```

### Output:

```text
Start
Middle
End
```

---

## 🧠 Real-Life Analogy:

👉 Queue at a ticket counter 🎟️

- One person at a time
    
- Others must wait
    

---

# ⚡ 3. Asynchronous (Async)

👉 Some tasks run **in background**  
👉 JS does NOT wait for them

---

## Example:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Inside Timeout");
}, 2000);

console.log("End");
```

---

### Output:

```text
Start
End
Inside Timeout
```

---

## 🧠 Why this happens?

👉 Because `setTimeout` runs in background (Web APIs)

---

# 🔥 Sync vs Async Comparison

|Feature|Synchronous|Asynchronous|
|---|---|---|
|Execution|One by one|Non-blocking|
|Waiting|Yes|No|
|Speed|Slower|Faster (overall UX)|
|Example|loops, console.log|setTimeout, fetch|

---

# 🧠 Real-Life Analogy

## Sync:

👉 Cooking step by step 🍳

- Wait for rice to cook before next step
    

## Async:

👉 Ordering food 🍔

- You order and wait
    
- Meanwhile you do other things
    

---

# ⚙️ 4. How Async Works (Behind the Scenes)

Even though JS is single-threaded:

👉 It uses:

- **Browser Web APIs**
    
- **Callback Queue**
    
- **Event Loop**
    

---

## Example Flow:

```text
JS Code → Web API → Callback Queue → Event Loop → Call Stack
```

---

## Example:

```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

### Output:

```text
A
C
B
```

---

## 🧠 Why B comes last?

Even with `0ms`, it goes to queue first.

---

# 🔥 Key Insight

👉 JavaScript is:

> Single-threaded BUT asynchronous via browser APIs

---

# ⚡ Simple Breakdown

## 🧵 Single-threaded:

- One task at a time
    

## ⏱️ Synchronous:

- Waits for each line
    

## ⚡ Asynchronous:

- Runs tasks in background
    

---

# 🚀 Final Summary

```javascript
// Single-threaded → one execution at a time

// Synchronous → line-by-line execution

// Asynchronous → non-blocking background tasks
```

---

# 🧠 One-line memory

👉 **JS is single-threaded but behaves asynchronously using browser power**

---

## 🔥 Promises in JavaScript (Simple Explanation)

A **Promise** is an object that represents a value that will be available **in the future**.

👉 Think of it like:

> “I promise I will give you data later” 📦

---

# 🧠 1. Promise States

A Promise has 3 states:

|State|Meaning|
|---|---|
|pending|still working ⏳|
|fulfilled|success ✅|
|rejected|failed ❌|

---

# ⚡ 2. Basic Promise Example

```javascript
const promise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("Data loaded successfully");
  } else {
    reject("Error loading data");
  }
});
```

---

## Using `.then()` and `.catch()`

```javascript
promise
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

---

# 🧠 Output:

```text
Data loaded successfully
```

---

# 🔥 3. Real-Life Promise Example (API-like)

```javascript
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("User Data Received");
    }, 2000);
  });
}

fetchData().then(data => console.log(data));
```

---

### Output (after 2 seconds):

```text
User Data Received
```

---

# ⚡ 4. Async/Await (Modern Way)

```javascript
async function getData() {
  const result = await fetchData();
  console.log(result);
}

getData();
```

---

# 🔥 5. Promise Chain

```javascript
fetchData()
  .then(data => {
    console.log(data);
    return "Next Step";
  })
  .then(step => {
    console.log(step);
  });
```

---

# 🚀 6. Promise.all()

👉 Used to run **multiple promises together**

---

## 🧠 Definition:

> Wait for ALL promises to complete, then return results.

---

# ⚡ Example:

```javascript
const p1 = Promise.resolve("User Data");
const p2 = Promise.resolve("Posts Data");
const p3 = Promise.resolve("Comments Data");

Promise.all([p1, p2, p3])
  .then(results => {
    console.log(results);
  });
```

---

### Output:

```text
["User Data", "Posts Data", "Comments Data"]
```

---

# 🧠 Real API Example

```javascript
const users = fetch("https://api.com/users");
const posts = fetch("https://api.com/posts");
const comments = fetch("https://api.com/comments");

Promise.all([users, posts, comments])
  .then(async (responses) => {
    const data = await Promise.all(responses.map(r => r.json()));
    console.log(data);
  });
```

---

# ⚠️ Important Rule of Promise.all

👉 If ONE fails → whole Promise.all fails ❌

```javascript
Promise.all([
  Promise.resolve("A"),
  Promise.reject("Error"),
  Promise.resolve("C")
])
.catch(err => console.log(err));
```

---

### Output:

```text
Error
```

---

# 🔥 7. Promise.allSettled()

👉 Waits for ALL results (success + failure)

```javascript
Promise.allSettled([
  Promise.resolve("A"),
  Promise.reject("Error"),
  Promise.resolve("C")
]).then(console.log);
```

---

### Output:

```text
[
  { status: "fulfilled", value: "A" },
  { status: "rejected", reason: "Error" },
  { status: "fulfilled", value: "C" }
]
```

---

# ⚡ Promise Methods Summary

|Method|Meaning|
|---|---|
|Promise.resolve()|instantly success|
|Promise.reject()|instantly fail|
|Promise.all()|all must succeed|
|Promise.allSettled()|wait for all results|
|Promise.race()|first finished wins|

---

# 🧠 Real-Life Analogy

## Promise:

👉 You order food 🍔

- You get result later
    

---

## Promise.all:

👉 Order food, drink, dessert 🍔🥤🍰

- Wait for ALL items together
    

---

# 🚀 Final Summary

```javascript
// Promise = future result

// then → success
// catch → error

// Promise.all → wait for all promises
```

---

# 🧠 One-line memory:

👉 **Promise = async result  
Promise.all = wait for multiple async results**

---

## ⚡ Async / Await in JavaScript (In Detail)

👉 `async/await` is a modern way to work with **Promises** in a cleaner, more readable style.

It helps you write **asynchronous code that looks like synchronous code**.

---

# 🧠 1. Why Async/Await?

Before async/await, we used:

- `.then()`
    
- `.catch()`
    

### Problem:

```javascript
fetchData()
  .then(data => {
    return processData(data);
  })
  .then(result => {
    console.log(result);
  })
  .catch(err => console.log(err));
```

👉 This becomes messy for big chains.

---

# 🚀 2. Async/Await Syntax

## ✨ Basic Rule:

- `async` → used before function
    
- `await` → waits for Promise result
    

---

## Example:

```javascript
async function getData() {
  const result = await fetch("https://api.example.com/users");
  const data = await result.json();

  console.log(data);
}

getData();
```

---

# 🧠 What is happening?

1. `async function` → always returns a Promise
    
2. `await` → pauses execution until Promise resolves
    
3. Code looks synchronous but runs asynchronously
    

---

# 🔥 3. Async Function Always Returns Promise

```javascript
async function test() {
  return "Hello";
}

console.log(test());
```

### Output:

```text
Promise { "Hello" }
```

---

## Correct way:

```javascript
test().then(data => console.log(data));
```

---

# ⚡ 4. Await Example (Step-by-Step)

```javascript
function delay() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve("Done!");
    }, 2000);
  });
}

async function run() {
  console.log("Start");

  const result = await delay();

  console.log(result);
  console.log("End");
}

run();
```

---

### Output:

```text
Start
(2 seconds delay)
Done!
End
```

---

# 🧠 Key Idea:

👉 `await` **pauses only inside async function**

---

# 🔥 5. Async vs Then Comparison

## Using `.then()`:

```javascript
fetch(url)
  .then(res => res.json())
  .then(data => console.log(data));
```

---

## Using async/await:

```javascript
async function get() {
  const res = await fetch(url);
  const data = await res.json();
  console.log(data);
}
```

👉 Async/await is cleaner and easier to read.

---

# ⚡ 6. Error Handling in Async/Await

We use `try...catch`

```javascript
async function getData() {
  try {
    const res = await fetch("https://api.com/data");
    const data = await res.json();

    console.log(data);
  } catch (error) {
    console.log("Error:", error);
  }
}
```

---

# 🧠 7. Multiple Awaits (Sequential)

```javascript
async function run() {
  const a = await Promise.resolve("A");
  const b = await Promise.resolve("B");

  console.log(a, b);
}
```

---

👉 This runs one after another (slow if independent)

---

# ⚡ 8. Parallel Execution (Better Way)

```javascript
async function run() {
  const [a, b] = await Promise.all([
    Promise.resolve("A"),
    Promise.resolve("B")
  ]);

  console.log(a, b);
}
```

---

# 🔥 9. Real API Example

```javascript
async function getUsers() {
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    const users = await res.json();

    users.forEach(user => {
      console.log(user.name);
    });
  } catch (error) {
    console.log("Failed to fetch users");
  }
}

getUsers();
```

---

# 🧠 10. Behind the Scenes

```text
Async function → returns Promise
Await → pauses function execution
Event Loop → resumes when Promise resolves
```

---

# ⚡ 11. Important Rules

✔ `await` only works inside `async` function  
✔ `async` always returns a Promise  
✔ Use `try/catch` for errors  
✔ Use `Promise.all()` for parallel tasks

---

# 🔥 Real-Life Analogy

## Async/Await = Restaurant 🍔

- You order food (request)
    
- You wait without blocking other tasks
    
- Food arrives later (await result)
    

---

# 🚀 Final Summary

```javascript
// async → makes function return Promise
// await → waits for Promise result

async function example() {
  const data = await fetch(url);
}
```

---

# 🧠 One-line memory:

👉 **Async/Await = clean way to handle Promises like synchronous code**

---

## ⏱️ `setInterval()` and `clearInterval()` in JavaScript

These are used for **repeated execution of code over time**.

---

# 🔁 1. `setInterval()`

👉 Runs a function **again and again after a fixed time interval**

---

## 🧠 Syntax:

```javascript
setInterval(function, timeInMilliseconds);
```

---

## ⚡ Example:

```javascript
setInterval(() => {
  console.log("Hello every 1 second");
}, 1000);
```

---

### Output:

```text
Hello every 1 second
Hello every 1 second
Hello every 1 second
...
```

👉 Runs infinitely until stopped

---

# 🧠 Real-Life Example:

👉 Clock ticking ⏰  
👉 Notification checker 🔔  
👉 Live updates 📡

---

# 🆔 2. Storing Interval ID

`setInterval()` returns an ID.

```javascript
const id = setInterval(() => {
  console.log("Running...");
}, 1000);
```

👉 This ID is used to stop it later

---

# 🛑 3. `clearInterval()`

👉 Stops a running interval

---

## Syntax:

```javascript
clearInterval(intervalId);
```

---

## Example:

```javascript
const id = setInterval(() => {
  console.log("Running...");
}, 1000);

// stop after 5 seconds
setTimeout(() => {
  clearInterval(id);
  console.log("Stopped");
}, 5000);
```

---

### Output:

```text
Running...
Running...
Running...
Running...
Stopped
```

---

# 🔥 4. Full Working Example

```javascript
let count = 0;

const intervalId = setInterval(() => {
  count++;
  console.log("Count:", count);

  if (count === 5) {
    clearInterval(intervalId);
    console.log("Interval Stopped");
  }
}, 1000);
```

---

# 🧠 How It Works

```text
setInterval → schedules repeated task
clearInterval → stops scheduled task
```

---

# ⚡ 5. Difference Between `setTimeout` and `setInterval`

|Feature|setTimeout|setInterval|
|---|---|---|
|Runs|once|repeatedly|
|Usage|delayed execution|repeated execution|
|Stop|no need|clearInterval|

---

# 🧠 Example Comparison

## setTimeout:

```javascript
setTimeout(() => {
  console.log("Runs once");
}, 2000);
```

## setInterval:

```javascript
setInterval(() => {
  console.log("Runs forever");
}, 2000);
```

---

# 🔥 6. Common Use Cases

✔ Live clock  
✔ Game timers  
✔ Animation loops  
✔ Auto-refresh data  
✔ Countdown timers

---

# ⚠️ Important Warning

👉 Always clear intervals when not needed

Otherwise:

- memory leak ❌
    
- performance issues ❌
    

---

# 🚀 Final Summary

```javascript
// start repeating task
const id = setInterval(fn, time);

// stop repeating task
clearInterval(id);
```

---

# 🧠 One-line memory:

👉 **setInterval = repeat task  
clearInterval = stop repeat**

---

## 🔁 JavaScript Event Loop & Concurrency (Simple but Deep Understanding)

These concepts explain **how JavaScript handles async tasks even though it is single-threaded**.

---

# 🧵 1. JavaScript is Single-Threaded

👉 JS can execute **only one thing at a time**

But still it handles:

- timers ⏱️
    
- API calls 🌐
    
- events 🖱️
    

👉 How?  
➡️ **Event Loop system**

---

# ⚙️ 2. Main Components

JavaScript runtime has 4 main parts:

## 1. Call Stack 📚

👉 Executes functions (LIFO)

## 2. Web APIs 🌐

👉 Browser features (setTimeout, fetch, DOM events)

## 3. Callback Queue 📥

👉 Stores finished async callbacks

## 4. Event Loop 🔁

👉 Moves tasks from queue → call stack

---

# 🧠 3. Simple Flow

```text
Code → Call Stack → Web APIs → Callback Queue → Event Loop → Call Stack
```

---

# 🔥 4. Example: setTimeout

```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

console.log("C");
```

---

### Output:

```text
A
C
B
```

---

# 🧠 Why does B come last?

Even with `0ms`, this happens:

1. `setTimeout` goes to **Web API**
    
2. callback goes to **Callback Queue**
    
3. Event Loop waits for Call Stack to be empty
    
4. then pushes callback
    

---

# 🔁 5. Event Loop Step-by-Step

### Code:

```javascript
function first() {
  console.log("First");
}

function second() {
  console.log("Second");
}

first();
second();
```

---

### Execution:

```text
1. first() → call stack → execute → removed
2. second() → call stack → execute → removed
```

---

# ⚡ 6. With Async Example

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 2000);

console.log("End");
```

---

### Flow:

```text
Start → Call Stack
setTimeout → Web API
End → Call Stack
(after 2s)
Timeout → Callback Queue → Event Loop → Call Stack
```

---

# 🔥 7. Microtask vs Macrotask Queue (VERY IMPORTANT)

JS has TWO queues:

---

## 🟡 Macrotask Queue

- setTimeout
    
- setInterval
    
- DOM events
    

---

## 🟢 Microtask Queue (Higher priority)

- Promises (.then)
    
- async/await
    

---

# 🧠 Priority Rule:

👉 Microtasks ALWAYS run before Macrotasks

---

## Example:

```javascript
console.log("A");

setTimeout(() => {
  console.log("B");
}, 0);

Promise.resolve().then(() => {
  console.log("C");
});

console.log("D");
```

---

### Output:

```text
A
D
C
B
```

---

# 🧠 Why?

Order of execution:

1. Sync code → A, D
    
2. Microtask → C (Promise)
    
3. Macrotask → B (setTimeout)
    

---

# ⚡ 8. Concurrency in JavaScript

👉 Concurrency = handling multiple tasks “at the same time” (not actually parallel)

---

## 🧠 JS is:

- ❌ Not parallel
    
- ✅ Concurrent (via event loop)
    

---

# 🔥 Example:

```javascript
console.log("1");

setTimeout(() => console.log("2"), 0);

setTimeout(() => console.log("3"), 0);

console.log("4");
```

---

### Output:

```text
1
4
2
3
```

---

# 🧠 9. Real-Life Analogy

## 🏭 Restaurant System:

|Component|Real Life|
|---|---|
|Call Stack|Chef cooking now|
|Web APIs|Waiter taking orders|
|Queue|Orders waiting list|
|Event Loop|Manager assigning tasks|

---

# ⚡ 10. Why Event Loop is Important

✔ Handles async JS  
✔ Makes non-blocking behavior possible  
✔ Powers:

- APIs
    
- timers
    
- UI events
    
- promises
    

---

# 🚀 Final Summary

```javascript
// JS is single-threaded

// Event Loop manages async execution

// Microtasks (Promises) run before Macrotasks (setTimeout)
```

---

# 🧠 One-line memory:

👉 **Event Loop = system that moves async tasks into execution when stack is empty**

---

