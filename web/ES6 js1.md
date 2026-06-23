## 🧠 Primitive and Non-Primitive Data Types (JavaScript)

JavaScript data types are mainly divided into **2 categories**:

---

# 1. Primitive Data Types

👉 **Primitive = single value, simple data**

They are:

- Stored directly in memory
    
- Immutable (cannot be changed)
    
- Compared by **value**
    

---

## 🔹 Types of Primitive Data

### 1. String

```javascript
let name = "Alex";
```

---

### 2. Number

```javascript
let age = 20;
```

---

### 3. Boolean

```javascript
let isActive = true;
```

---

### 4. Undefined

```javascript
let x;
```

---

### 5. Null

```javascript
let value = null;
```

---

### 6. BigInt

```javascript
let big = 123456789012345678901234567890n;
```

---

### 7. Symbol

```javascript
let id = Symbol("id");
```

---

## ⚡ Primitive Example (Value Copy)

```javascript
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

👉 They are independent

---

# 2. Non-Primitive Data Types

👉 **Non-Primitive = multiple values (complex data)**

They are:

- Stored as reference (memory address)
    
- Mutable (can be changed)
    
- Compared by **reference**
    

---

## 🔹 Types of Non-Primitive Data

### 1. Object

```javascript
let user = {
  name: "Alex",
  age: 20
};
```

---

### 2. Array

```javascript
let numbers = [1, 2, 3];
```

---

### 3. Function

```javascript
function greet() {
  console.log("Hello");
}
```

---

## ⚡ Non-Primitive Example (Reference Copy)

```javascript
let obj1 = { name: "Alex" };
let obj2 = obj1;

obj2.name = "John";

console.log(obj1.name);
console.log(obj2.name);
```

Output:

```text
John
John
```

👉 Both point to same memory

---

# 🔥 Key Differences

|Feature|Primitive|Non-Primitive|
|---|---|---|
|Value type|Simple|Complex|
|Stored as|Value|Reference|
|Mutable|❌ No|✅ Yes|
|Copy behavior|Copy value|Copy reference|
|Examples|string, number|object, array|

---

# 🧠 Memory Visualization

### Primitive:

```
a → 10
b → 10 (new copy)
```

### Non-Primitive:

```
obj1 → memory address → { name: "Alex" }
obj2 → same address
```

---

# 🚀 Real-Life Analogy

### Primitive:

👉 Photocopy of paper 📄  
(each copy is independent)

### Non-Primitive:

👉 Google Drive link 🔗  
(multiple people access same file)

---

# ⚡ Final Summary

```javascript
// Primitive
let a = 10;

// Non-primitive
let obj = { name: "Alex" };
let arr = [1, 2, 3];
```

---

👉 Simple meaning:

- **Primitive = single value (safe copy)**
    
- **Non-primitive = complex structure (shared reference)**
    

---

## 🧠 `null` vs `undefined` in JavaScript

Both mean **“no value”**, but they are NOT the same.

---

# 1. `undefined`

👉 Means: **value is not assigned yet**

JavaScript gives it automatically.

```javascript
let x;

console.log(x);
```

Output:

```text
undefined
```

---

# 2. `null`

👉 Means: **intentionally empty (set by developer)**

```javascript
let y = null;

console.log(y);
```

Output:

```text
null
```

---

# 🔥 Key Difference

|Feature|undefined|null|
|---|---|---|
|Meaning|Not assigned|Empty intentionally|
|Type|undefined|object (bug in JS)|
|Set by|JS|Developer|
|Value|automatic|manual|

---

# 🧠 Different Ways You Get `undefined`

## 1. Variable declared but not assigned

```javascript
let a;
console.log(a);
```

---

## 2. Function without return

```javascript
function test() {}

console.log(test());
```

---

## 3. Missing object property

```javascript
const user = {
  name: "Alex"
};

console.log(user.age);
```

---

## 4. Missing array element

```javascript
const arr = [1, 2, 3];

console.log(arr[5]);
```

---

## 5. Function parameter not passed

```javascript
function show(x) {
  console.log(x);
}

show();
```

---

## 6. Explicit `undefined`

```javascript
let x = undefined;

console.log(x);
```

---

## 7. Deleted object property

```javascript
const obj = { name: "Alex" };

delete obj.name;

console.log(obj.name);
```

---

# ⚡ Important Comparison

```javascript
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

👉 `==` ignores type  
👉 `===` checks type strictly

---

# 🧠 Real-Life Analogy

### undefined:

👉 “I didn’t get the value yet” 📦

### null:

👉 “I intentionally left it empty” 🗂️

---

# 🚀 Final Summary

```javascript
// undefined
let a;

// null
let b = null;

// common undefined cases:
function f() {}
obj.key;
arr[100];
missing parameter;
```

---

👉 Simple meaning:

- **undefined = not assigned**
    
- **null = intentionally empty**
    

---
## ⚡ Truthy vs Falsy Values in JavaScript

In JavaScript, every value is treated as either:

- **Truthy** → becomes `true` in conditions
    
- **Falsy** → becomes `false` in conditions
    

---

# ❌ 1. Falsy Values (ONLY 8 in JavaScript)

These are the **only values that become false**:

```javascript
false
0
-0
0n
""
null
undefined
NaN
```

---

## 🔥 Example of Falsy

```javascript
if (0) {
  console.log("Yes");
} else {
  console.log("No");
}
```

Output:

```text
No
```

---

## Other Falsy Examples

```javascript
if ("") console.log("Hello");     // ❌
if (null) console.log("Hi");     // ❌
if (undefined) console.log("Hi");// ❌
if (NaN) console.log("Hi");      // ❌
```

---

# ✅ 2. Truthy Values

👉 Everything that is NOT falsy is truthy.

---

## Common Truthy Values

### 1. Non-empty strings

```javascript
if ("hello") {
  console.log("Truthy");
}
```

---

### 2. Numbers (except 0)

```javascript
if (10) console.log("Truthy");
if (-5) console.log("Truthy");
```

---

### 3. Arrays

```javascript
if ([]) {
  console.log("Truthy");
}
```

---

### 4. Objects

```javascript
if ({}) {
  console.log("Truthy");
}
```

---

### 5. Functions

```javascript
if (function() {}) {
  console.log("Truthy");
}
```

---

# 🧠 Important Trick

```javascript
console.log(Boolean(0));        // false
console.log(Boolean("Hello"));  // true
console.log(Boolean([]));       // true
console.log(Boolean({}));       // true
```

---

# ⚡ Truthy vs Falsy Table

|Type|Value|Result|
|---|---|---|
|Falsy|0|false|
|Falsy|""|false|
|Falsy|null|false|
|Falsy|undefined|false|
|Falsy|NaN|false|
|Truthy|"text"|true|
|Truthy|[]|true|
|Truthy|{}|true|
|Truthy|123|true|

---

# 🔥 Real-Life Example

```javascript
let userName = "";

if (userName) {
  console.log("Welcome");
} else {
  console.log("Please enter name");
}
```

Output:

```text
Please enter name
```

---

# 🧠 Why It Matters

Used in:

- `if` conditions
    
- Form validation
    
- API checks
    
- React / frontend logic
    
- Authentication checks
    

---

# ⚡ Shortcut Thinking

```javascript
// falsy = empty / nothing / invalid
// truthy = everything else
```

---

# 🚀 Final Summary

- **Falsy (8 values)** → always false
    
- **Truthy (everything else)** → always true
    
- Used heavily in real-world JavaScript logic
    

---

## ⚖️ `==` vs `===` in JavaScript (with Implicit Conversion)

JavaScript has two equality operators:

- `==` → **loose equality**
    
- `===` → **strict equality**
    

---

# 1. `==` (Double Equal) → Type Coercion Happens

👉 It compares values **after converting types automatically**

This is called:

## ⚡ Implicit Conversion (Type Coercion)

---

### Example:

```javascript
console.log(5 == "5");
```

Output:

```text
true
```

👉 JS converts `"5"` → `5`

---

## More Examples:

```javascript
console.log(0 == false);   // true
console.log("" == false);   // true
console.log(null == undefined); // true
```

---

# 2. `===` (Triple Equal) → Strict Comparison

👉 No conversion happens  
👉 Checks **value + type**

---

### Example:

```javascript
console.log(5 === "5");
```

Output:

```text
false
```

---

## More Examples:

```javascript
console.log(0 === false);   // false
console.log("" === false);  // false
console.log(null === undefined); // false
```

---

# ⚡ Key Difference Table

|Feature|`==` (Loose)|`===` (Strict)|
|---|---|---|
|Type conversion|Yes|No|
|Compares value|Yes|Yes|
|Compares type|No|Yes|
|Safety|Low|High|

---

# 🧠 What is Implicit Conversion?

👉 JavaScript automatically changes types to match

---

## Example:

```javascript
console.log("10" + 5);
```

Output:

```text
"105"
```

👉 number → string conversion

---

## Another Example:

```javascript
console.log("10" - 5);
```

Output:

```text
5
```

👉 string → number conversion

---

# 🔥 Weird `==` Cases (Interview Favorite)

```javascript
console.log([] == false);     // true
console.log("" == 0);         // true
console.log([1] == "1");      // true
```

👉 Because JS converts both sides in strange ways

---

# 🧠 Best Practice

✔ Always use:

```javascript
===
```

❌ Avoid:

```javascript
==
```

---

# 🚀 Real-Life Analogy

### `==`

👉 “I will adjust and compare somehow” 🔄

### `===`

👉 “I check exactly as it is” 🎯

---

# ⚡ Final Summary

```javascript
// Loose equality (type conversion)
5 == "5"   // true

// Strict equality (no conversion)
5 === "5"  // false
```

---

👉 Simple meaning:

- `==` → compares after conversion (unsafe)
    
- `===` → compares exactly (safe)
    

---

## 🌍 Block Scope, Global Scope & Hoisting (Simple JavaScript Understanding)

These are 3 core concepts that explain **how JavaScript stores and runs variables**.

---

# 🌍 1. Global Scope

👉 A variable declared **outside any block or function**

✔ Accessible everywhere in the code

```javascript
let name = "Alex";

function show() {
  console.log(name);
}

show();
console.log(name);
```

Output:

```text
Alex
Alex
```

---

## 🧠 Global Scope Rule:

- Declared outside `{ }`
    
- Can be used anywhere
    
- Lives for whole program
    

---

# 📦 2. Block Scope

👉 A variable declared inside `{ }`

✔ Only accessible inside that block

### Works with `let` and `const`

```javascript
{
  let age = 20;
  console.log(age);
}

console.log(age); // ❌ Error
```

---

## Example with `if` block:

```javascript
if (true) {
  let x = 10;
  console.log(x);
}

console.log(x); // ❌ Error
```

---

## 🧠 Block Scope Rule:

- Inside `{ }`
    
- Cannot access outside
    
- Used in loops, if, functions
    

---

## ⚠️ `var` is NOT block scoped

```javascript
if (true) {
  var a = 100;
}

console.log(a); // 100 ❗
```

👉 `var` ignores block scope

---

# 🧠 3. Hoisting (Simple Understanding)

👉 JavaScript moves **declarations to the top** automatically

BUT only the declaration, NOT the value.

---

# 📌 Example with `var`

```javascript
console.log(x);

var x = 5;
```

Output:

```text
undefined
```

👉 JS treats it like:

```javascript
var x;
console.log(x);
x = 5;
```

---

# 📌 Example with `let` / `const`

```javascript
console.log(x);

let x = 10;
```

Output:

```text
ReferenceError
```

👉 Because of **Temporal Dead Zone (TDZ)**

---

# 🧠 Hoisting Rule:

|Variable|Hoisted?|Value available?|
|---|---|---|
|var|Yes|undefined|
|let|Yes|❌ No (TDZ)|
|const|Yes|❌ No (TDZ)|

---

# 🔥 Function Hoisting

### Works fully:

```javascript
greet();

function greet() {
  console.log("Hello");
}
```

Output:

```text
Hello
```

---

# ❗ But function expressions are NOT hoisted

```javascript
sayHi();

const sayHi = function () {
  console.log("Hi");
};
```

❌ Error

---

# ⚡ Quick Comparison

|Concept|Meaning|
|---|---|
|Global Scope|accessible everywhere|
|Block Scope|accessible only inside `{ }`|
|Hoisting|variables/functions moved to top|

---

# 🧠 Real-Life Analogy

### Global Scope 🌍

👉 Like public notice board (everyone can see)

### Block Scope 📦

👉 Like locked room (only inside access)

### Hoisting ⬆️

👉 Like JS preparing declarations before running code

---

# 🚀 Final Summary

```javascript
// Global scope
let a = 10;

// Block scope
{
  let b = 20;
}

// Hoisting
console.log(x); // undefined
var x = 5;
```

---

👉 Simple meaning:

- **Global scope = everywhere access**
    
- **Block scope = limited access**
    
- **Hoisting = JS lifts declarations upward**
    

---

## 🔁 Callback Function & Passing Different Functions (JavaScript)

A **callback function** is a function that is:

> passed as an argument into another function and executed later.

---

# 🧠 1. Basic Idea

👉 Function inside another function

```javascript
function greet(name) {
  console.log("Hello " + name);
}

function processUser(callback) {
  callback("Alex");
}

processUser(greet);
```

Output:

```text
Hello Alex
```

---

# 🔥 2. What is happening?

- `greet` → function
    
- `processUser` → accepts a function
    
- `callback("Alex")` → runs passed function
    

👉 So function is treated like a **value**

---

# ✨ 3. Using Anonymous Callback

```javascript
function processUser(callback) {
  callback("John");
}

processUser(function(name) {
  console.log("Hi " + name);
});
```

---

# 🚀 4. Arrow Function Callback (Modern Way)

```javascript
function processUser(callback) {
  callback("Mike");
}

processUser(name => {
  console.log("Welcome " + name);
});
```

---

# ⚡ 5. Passing Different Functions

👉 Same function, different behavior

```javascript
function calculate(a, b, operation) {
  return operation(a, b);
}

function add(x, y) {
  return x + y;
}

function multiply(x, y) {
  return x * y;
}

console.log(calculate(5, 3, add));
console.log(calculate(5, 3, multiply));
```

Output:

```text
8
15
```

---

# 🧠 6. Real-Life Example

```javascript
function greetUser(name, callback) {
  console.log("User: " + name);
  callback();
}

function sayWelcome() {
  console.log("Welcome!");
}

function sayBye() {
  console.log("Goodbye!");
}

greetUser("Alex", sayWelcome);
greetUser("John", sayBye);
```

Output:

```text
User: Alex
Welcome!
User: John
Goodbye!
```

---

# 🔁 7. Callback in Built-in Methods

## `setTimeout`

```javascript
setTimeout(function() {
  console.log("Executed after 2 seconds");
}, 2000);
```

---

## Array `map`

```javascript
const nums = [1, 2, 3];

nums.map(num => num * 2);
```

👉 `map()` uses callback internally

---

# ⚡ 8. Why Callbacks are Important

✔ Asynchronous code (timers, API calls)  
✔ Event handling  
✔ Array methods (`map`, `filter`, `reduce`)  
✔ Flexible function behavior

---

# 🧠 Simple Definition

```javascript
// callback = function passed into another function
```

---

# 🔥 Real-Life Analogy

👉 Restaurant example:

- You order food 🍔
    
- You give instructions (callback)
    
- Chef cooks and calls you when ready
    

---

# ⚡ Final Summary

|Concept|Meaning|
|---|---|
|Callback|function passed as argument|
|Execution|called inside another function|
|Use case|async tasks, array methods|
|Flexibility|different functions = different behavior|

---

👉 Simple meaning:

- **Callback = function as input**
    
- **Same function can behave differently depending on what you pass**
    

---
## 🧠 Function Arguments: Pass by Value vs Pass by Reference (JavaScript)

In JavaScript, when you pass data into a function, it behaves in **two different ways** depending on the data type:

---

# 1. Pass by Value (Primitive Types)

👉 Works with:

- number
    
- string
    
- boolean
    
- null
    
- undefined
    
- symbol
    
- bigint
    

### 💡 Idea:

A **copy of the value** is passed into the function.

---

## Example:

```javascript
function change(x) {
  x = 100;
  console.log("Inside:", x);
}

let a = 10;

change(a);

console.log("Outside:", a);
```

### Output:

```text
Inside: 100
Outside: 10
```

---

## 🧠 Meaning:

- Function gets a **copy**
    
- Original value does NOT change
    

---

# 2. Pass by Reference (Non-Primitive Types)

👉 Works with:

- objects
    
- arrays
    
- functions
    

### 💡 Idea:

A **reference (memory address)** is passed.

---

## Example (Object):

```javascript
function change(obj) {
  obj.name = "John";
}

const user = {
  name: "Alex"
};

change(user);

console.log(user.name);
```

### Output:

```text
John
```

---

## 🧠 Meaning:

- Function gets reference to same object
    
- Original object is modified
    

---

# 3. Array Example (Reference)

```javascript
function modify(arr) {
  arr.push(4);
}

let numbers = [1, 2, 3];

modify(numbers);

console.log(numbers);
```

### Output:

```text
[1, 2, 3, 4]
```

---

# 🔥 Key Difference Table

|Feature|Pass by Value|Pass by Reference|
|---|---|---|
|Data type|Primitive|Non-primitive|
|What is passed|Copy of value|Memory reference|
|Original changed?|❌ No|✅ Yes|
|Examples|number, string|object, array|

---

# 🧠 Important Truth (JavaScript Reality)

👉 JavaScript is actually:

> **Pass by Value ONLY**

BUT…

For objects:

- the **value passed is a reference**
    
- so it _acts like pass by reference_
    

---

# ⚡ Simple Mental Model

### Primitive:

```text
a → 10 (copy sent)
```

### Object:

```text
obj → memory address → { data }
```

---

# 🔥 Real-Life Analogy

### Pass by Value:

👉 Photocopy of document 📄  
(you change copy, original stays safe)

### Pass by Reference:

👉 Shared Google Doc 🔗  
(everyone edits same file)

---

# ⚡ Final Summary

```javascript
// Pass by value (primitive)
let a = 10;

// Pass by reference (object)
let obj = { name: "Alex" };
```

---

👉 Simple meaning:

- **Primitive → copied**
    
- **Object/Array → shared reference**
    

---

## 🧠 Deep Copy vs Shallow Copy in JavaScript

When you copy an object or array, JavaScript can copy it in **two ways**:

- **Shallow Copy** → copies only the first level
    
- **Deep Copy** → copies everything (including nested objects)
    

---

# 🟡 1. Shallow Copy

👉 Copies only the **top-level properties**  
👉 Nested objects are still shared (same reference)

---

## Example:

```javascript
const user1 = {
  name: "Alex",
  address: {
    city: "Dhaka"
  }
};

const user2 = { ...user1 };

user2.name = "John";
user2.address.city = "London";

console.log(user1.name);
console.log(user1.address.city);
```

### Output:

```text
Alex
London
```

---

## 🧠 What happened?

- `name` → copied (independent)
    
- `address` → shared reference ❗
    

```text
user1.address === user2.address → true
```

---

# 🔵 2. Deep Copy

👉 Copies **everything fully (no shared reference)**  
👉 Nested objects are also cloned

---

## Method 1: `JSON.parse(JSON.stringify())`

```javascript
const user1 = {
  name: "Alex",
  address: {
    city: "Dhaka"
  }
};

const user2 = JSON.parse(JSON.stringify(user1));

user2.address.city = "London";

console.log(user1.address.city);
```

### Output:

```text
Dhaka
```

---

## 🧠 Now objects are completely independent

---

# ⚡ Shallow Copy Methods

```javascript
// 1. Spread operator
const copy1 = { ...obj };

// 2. Object.assign
const copy2 = Object.assign({}, obj);

// 3. Array methods
const arrCopy = [...arr];
```

---

# ⚡ Deep Copy Methods

## 1. JSON method (simple but limited)

```javascript
const deep = JSON.parse(JSON.stringify(obj));
```

❌ Does NOT work with:

- functions
    
- undefined
    
- Date
    
- Map/Set
    

---

## 2. Modern method (best)

```javascript
const deep = structuredClone(obj);
```

✔ Works with nested objects  
✔ Works with arrays  
✔ Modern browsers & Node.js support

---

# 🔥 Comparison Table

|Feature|Shallow Copy|Deep Copy|
|---|---|---|
|Copy level|First level only|Full structure|
|Nested objects|Shared|Independent|
|Safety|Risk of bugs|Safe|
|Performance|Fast|Slower|
|Example|`{...obj}`|`structuredClone(obj)`|

---

# 🧠 Visual Understanding

## Shallow Copy:

```text
user1 → { name, address → shared }
user2 → { name, address → shared }
```

## Deep Copy:

```text
user1 → { name, address }
user2 → { name, address } (completely separate)
```

---

# 🚀 Real-Life Analogy

### Shallow Copy:

👉 Photocopy of document but same folder attachment is shared 📄🔗

### Deep Copy:

👉 Completely new document with all attachments duplicated 📄📄

---

# ⚡ When to Use

## Use Shallow Copy when:

✔ Simple objects  
✔ Performance matters  
✔ No nested mutation risk

## Use Deep Copy when:

✔ Nested objects exist  
✔ You want full independence  
✔ State management (React, Redux)

---

# 🚀 Final Summary

```javascript
// Shallow copy
const a = { ...obj };

// Deep copy
const b = structuredClone(obj);
```

---

👉 Simple meaning:

- **Shallow copy = partial copy (shared inner data)**
    
- **Deep copy = full independent copy**
    

---

## 🔒 Closure in JavaScript (Important Concept)

A **closure** is one of the most important and powerful concepts in JavaScript.

---

# 🧠 Simple Definition

👉 A **closure** is when a function “remembers” variables from its outer scope, even after the outer function has finished executing.

---

# 1. Basic Example

```javascript
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const counter = outer();

counter();
counter();
counter();
```

---

### Output:

```text
1
2
3
```

---

# 🧠 What is happening?

- `outer()` runs and finishes
    
- but `inner()` still remembers `count`
    
- that memory is called a **closure**
    

---

# 🔥 Key Idea

```text
inner function + outer variables = closure
```

---

# 2. Why Closure Works

When a function is created:  
👉 It keeps a link to its **lexical environment**

Even after outer function is gone.

---

# 3. Another Simple Example

```javascript
function greet(name) {
  return function () {
    console.log("Hello " + name);
  };
}

const sayHello = greet("Alex");

sayHello();
```

---

### Output:

```text
Hello Alex
```

---

# 🧠 Explanation

- `greet("Alex")` finishes
    
- but inner function still remembers `name`
    

👉 That memory is closure

---

# 4. Real-Life Example (Counter)

```javascript
function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter1 = createCounter();

console.log(counter1());
console.log(counter1());
```

---

### Output:

```text
1
2
```

---

# 🔥 5. Why Closures are Powerful

✔ Data privacy  
✔ Encapsulation  
✔ Function factories  
✔ Event handlers  
✔ Async programming

---

# 🔒 6. Data Privacy Example

```javascript
function bankAccount() {
  let balance = 1000;

  return {
    deposit(amount) {
      balance += amount;
      return balance;
    },
    getBalance() {
      return balance;
    }
  };
}

const account = bankAccount();

console.log(account.getBalance());
console.log(account.deposit(500));
```

---

👉 `balance` is private using closure

---

# ⚡ 7. Closure in Loops (Important Interview Topic)

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

### Output:

```text
4
4
4
```

---

## Fix using closure:

```javascript
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}
```

### Output:

```text
1
2
3
```

---

# 🧠 Difference: Scope vs Closure

|Concept|Meaning|
|---|---|
|Scope|Where variables exist|
|Closure|Function remembering outer variables|

---

# 🚀 Real-Life Analogy

👉 Closure is like:

📦 A backpack that a function carries

Even when outer function is gone, it still carries data inside.

---

# ⚡ Final Summary

```javascript
function outer() {
  let x = 10;

  return function inner() {
    console.log(x);
  };
}

const fn = outer();
fn(); // closure keeps x alive
```

---

👉 Simple meaning:

- **Closure = function + remembered variables**
    
- It allows functions to “remember” past data
    

---

