In **ES6 JavaScript**, `let` and `const` were introduced as new ways to declare variables (along with the older `var`).

### `var`

- Old way of declaring variables (before ES6)
    
- Function-scoped
    
- Can be **redeclared** and **reassigned**
    
- Hoisted (initialized with `undefined`)
    

```javascript
var name = "Alex";
var name = "John"; // allowed
name = "Mike";     // allowed

console.log(name); // Mike
```

---

### `let`

- Introduced in ES6
    
- Block-scoped (`{ }`)
    
- Can be **reassigned**
    
- Cannot be **redeclared in the same scope**
    
- Hoisted but not initialized (Temporal Dead Zone)
    

```javascript
let age = 20;

age = 21; // allowed

// let age = 25; // Error: already declared

if (true) {
  let score = 100;
}

console.log(score); // Error: score is not defined
```

---

### `const`

- Introduced in ES6
    
- Block-scoped
    
- Cannot be reassigned
    
- Cannot be redeclared
    
- Must be initialized when declared
    

```javascript
const country = "Bangladesh";

// country = "India"; // Error

console.log(country);
```

For objects/arrays, the reference cannot change, but contents can:

```javascript
const user = {
  name: "Alex"
};

user.name = "John"; // allowed

console.log(user.name); // John
```

---

### Quick Comparison

|Feature|var|let|const|
|---|---|---|---|
|ES6|No|Yes|Yes|
|Scope|Function|Block|Block|
|Reassign|Yes|Yes|No|
|Redeclare|Yes|No|No|
|Must initialize|No|No|Yes|
|Hoisted|Yes|Yes (TDZ)|Yes (TDZ)|

**Modern JavaScript practice:** Prefer `const` by default, use `let` when the value needs to change, and avoid `var` in new code.

-------------
# In **ES6 JavaScript**, a **default parameter** lets a function use a default value when an argument is **not provided**.

Syntax:

```javascript
function functionName(parameter = defaultValue) {
  // code
}
```

### Example:

```javascript
function greet(name = "Guest") {
  console.log("Hello " + name);
}

greet("Alex");  // Hello Alex
greet();        // Hello Guest
```

Here, if no value is passed, `"Guest"` is used.

### Multiple default parameters:

```javascript
function add(a = 0, b = 0) {
  return a + b;
}

console.log(add(5, 10)); // 15
console.log(add(5));     // 5
console.log(add());      // 0
```

### Default parameter with expression:

```javascript
function multiply(a = 2, b = a * 3) {
  return a * b;
}

console.log(multiply()); // 12
```

### Note:

Default values apply when the argument is `undefined`:

```javascript
function test(x = 10) {
  console.log(x);
}

test();          // 10
test(undefined); // 10
test(null);      // null
```

`=` in function parameters means: **"use this value if no argument is supplied."**

-----------

# In **ES6 JavaScript**, **Template Strings** use **backticks ( )** instead of quotes. They allow **multiple lines** and **dynamic values** using `${}`.

### 1. Template String ( )

Old way:

```javascript
let name = "Alex";

console.log("Hello " + name);
```

ES6 way:

```javascript
let name = "Alex";

console.log(`Hello ${name}`);
```

Output:

```
Hello Alex
```

---

### 2. Multiple Line String

Using normal strings:

```javascript
let text = "Hello\nWorld";
```

Using template strings:

```javascript
let text = `
Hello
World
`;

console.log(text);
```

Output:

```
Hello
World
```

---

### 3. Dynamic String with `${}`

You can insert variables and expressions:

```javascript
let user = "John";
let age = 20;

let message = `My name is ${user} and I am ${age} years old.`;

console.log(message);
```

Output:

```
My name is John and I am 20 years old.
```

---

### 4. Dynamic Calculation

```javascript
let a = 10;
let b = 5;

console.log(`Total = ${a + b}`);
```

Output:

```
Total = 15
```

---

### Summary

|Feature|Syntax|
|---|---|
|Template String|`` `text` ``|
|Variable insert|`${variable}`|
|Multiple lines|Use backticks|
|Expression|`${expression}`|

Template strings make JavaScript strings easier to read and build dynamically.

----
# In **ES6 JavaScript**, an **Arrow Function (`=>`)** is a shorter way to write functions.

### 1. Normal Function

```javascript
function greet() {
  return "Hello";
}

console.log(greet());
```

### Arrow Function

```javascript
const greet = () => {
  return "Hello";
};

console.log(greet());
```

---

### 2. Arrow Function with One Parameter

```javascript
const square = x => {
  return x * x;
};

console.log(square(5)); // 25
```

Parentheses are optional for one parameter.

---

### 3. Multiple Parameters

For multiple parameters, use parentheses:

```javascript
const add = (a, b) => {
  return a + b;
};

console.log(add(10, 5)); // 15
```

---

### 4. Arrow Function Short Body (Implicit Return)

If the function has only one expression, you can remove `{}` and `return`.

```javascript
const multiply = (a, b) => a * b;

console.log(multiply(4, 3)); // 12
```

---

### 5. Function Body with `{ }`

When using `{ }`, you need `return`:

```javascript
const checkAge = (age) => {
  if (age >= 18) {
    return "Adult";
  } else {
    return "Minor";
  }
};

console.log(checkAge(20));
```

---

### Summary

|Type|Example|
|---|---|
|No parameter|`() => {}`|
|One parameter|`x => {}`|
|Multiple parameters|`(a,b) => {}`|
|Short return|`(a,b) => a+b`|
|Function body|`(a,b) => { return a+b }`|

Arrow functions make ES6 code shorter and cleaner.

-------------

# An **Anonymous Function** in JavaScript is a function **without a name**.

It is usually used when a function is needed only once or passed as a value.

### 1. Anonymous Function Example

```javascript
const greet = function() {
  console.log("Hello");
};

greet();
```

Output:

```
Hello
```

Here `function() {}` has no name, so it is anonymous.

---

### 2. Anonymous Function with Parameters

```javascript
const add = function(a, b) {
  return a + b;
};

console.log(add(5, 3));
```

Output:

```
8
```

---

### 3. Anonymous Function as Callback

```javascript
setTimeout(function() {
  console.log("Done");
}, 2000);
```

The function runs after 2 seconds.

---

### 4. Anonymous Function vs Arrow Function

Anonymous function:

```javascript
const square = function(x) {
  return x * x;
};
```

Arrow function (ES6 shorter way):

```javascript
const square = (x) => x * x;
```

Both do the same thing.

### Summary:

- **Named function:**
    

```javascript
function hello() {}
```

- **Anonymous function:**
    

```javascript
function() {}
```

- Commonly used for callbacks and one-time operations.

----------

# More About Arrow Functions (`=>`) in ES6 JavaScript

An **arrow function** is a shorter syntax for writing functions.

### 1. Basic Arrow Function

Normal function:

```javascript
function hello() {
  return "Hello";
}
```

Arrow function:

```javascript
const hello = () => {
  return "Hello";
};

console.log(hello());
```

Output:

```text
Hello
```

---

### 2. Arrow Function with One Parameter

Parentheses are optional:

```javascript
const square = x => {
  return x * x;
};

console.log(square(4)); // 16
```

---

### 3. Multiple Parameters

Multiple parameters need parentheses:

```javascript
const add = (a, b) => {
  return a + b;
};

console.log(add(10, 20)); // 30
```

---

### 4. Short Arrow Function (Implicit Return)

No `{}` and no `return` needed:

```javascript
const multiply = (a, b) => a * b;

console.log(multiply(5, 3)); // 15
```

---

### 5. Returning an Object

Use parentheses around the object:

```javascript
const user = () => ({
  name: "Alex",
  age: 20
});

console.log(user());
```

Output:

```javascript
{
  name: "Alex",
  age: 20
}
```

---

### 6. Arrow Function with Array Methods

Example with `map()`:

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.map(num => num * 2);

console.log(result);
```

Output:

```javascript
[2, 4, 6, 8]
```

---

### 7. Arrow Function as Callback

```javascript
setTimeout(() => {
  console.log("Hello after 2 seconds");
}, 2000);
```

---

### 8. Arrow Function with Multiple Lines

Use `{}`:

```javascript
const check = (age) => {
  if (age >= 18) {
    return "Adult";
  }

  return "Minor";
};

console.log(check(20));
```

---

### 9. Important Difference: `this`

Arrow functions **do not have their own `this`**.

Example:

```javascript
const person = {
  name: "John",

  normalFunction: function() {
    console.log(this.name);
  },

  arrowFunction: () => {
    console.log(this.name);
  }
};

person.normalFunction(); // John
person.arrowFunction();  // undefined
```

---

### Arrow Function Quick Cheat Sheet

```javascript
() => "Hello"

x => x * 2

(a, b) => a + b

(a, b) => {
  return a + b;
}
```

`=>` means: **"this is a function"**.

-----------
# Spread Operator (`...`) in ES6 JavaScript

The **spread operator** (`...`) expands elements from an array or object.

---

### 1. Copy Arrays

Without spread:

```javascript
let arr1 = [1, 2, 3];
let arr2 = arr1;

arr2.push(4);

console.log(arr1); // [1, 2, 3, 4]
```

Both variables point to the same array.

Using spread:

```javascript
let arr1 = [1, 2, 3];

let arr2 = [...arr1];

arr2.push(4);

console.log(arr1); // [1, 2, 3]
console.log(arr2); // [1, 2, 3, 4]
```

---

### 2. Combine Arrays

```javascript
let a = [1, 2];
let b = [3, 4];

let result = [...a, ...b];

console.log(result);
```

Output:

```javascript
[1, 2, 3, 4]
```

---

### 3. Array Max with Spread

`Math.max()` does not work directly with arrays:

```javascript
let numbers = [10, 5, 20];

console.log(Math.max(numbers));
```

Output:

```text
NaN
```

Use spread:

```javascript
let numbers = [10, 5, 20];

let max = Math.max(...numbers);

console.log(max);
```

Output:

```text
20
```

---

### 4. Copy Object

```javascript
let user = {
  name: "Alex",
  age: 20
};

let copyUser = { ...user };

console.log(copyUser);
```

Output:

```javascript
{
  name: "Alex",
  age: 20
}
```

---

### 5. Add New Values While Copying

```javascript
let numbers = [1, 2, 3];

let newNumbers = [...numbers, 4, 5];

console.log(newNumbers);
```

Output:

```javascript
[1, 2, 3, 4, 5]
```

---

### 6. Spread in Function Arguments

```javascript
function add(a, b, c) {
  return a + b + c;
}

let nums = [5, 10, 15];

console.log(add(...nums));
```

Output:

```text
30
```

---

### Summary

|Use|Example|
|---|---|
|Copy array|`[...arr]`|
|Merge arrays|`[...a, ...b]`|
|Array max|`Math.max(...arr)`|
|Copy object|`{...obj}`|
|Pass arguments|`func(...arr)`|

`...` means **expand / unpack values**.

----------------
# Advanced Object and Array Destructuring (ES6)

**Destructuring** lets you extract values from objects and arrays into variables.

---

## 1. Basic Array Destructuring

```javascript
const numbers = [10, 20, 30];

const [a, b, c] = numbers;

console.log(a); // 10
console.log(b); // 20
```

---

## 2. Skip Array Values

```javascript
const colors = ["red", "green", "blue"];

const [first, , third] = colors;

console.log(first); // red
console.log(third); // blue
```

---

## 3. Default Values

```javascript
const [x = 5, y = 10] = [1];

console.log(x); // 1
console.log(y); // 10
```

---

## 4. Rest Operator with Arrays

```javascript
const numbers = [1, 2, 3, 4, 5];

const [first, second, ...rest] = numbers;

console.log(first); // 1
console.log(second); // 2
console.log(rest); // [3,4,5]
```

---

# Object Destructuring

## 5. Basic Object Destructuring

```javascript
const user = {
  name: "Alex",
  age: 20
};

const { name, age } = user;

console.log(name); // Alex
console.log(age);  // 20
```

---

## 6. Rename Variables

```javascript
const user = {
  name: "Alex",
  age: 20
};

const { name: userName, age: userAge } = user;

console.log(userName); // Alex
console.log(userAge);  // 20
```

---

## 7. Default Values in Objects

```javascript
const user = {
  name: "John"
};

const { name, city = "Dhaka" } = user;

console.log(city); // Dhaka
```

---

## 8. Object Rest Operator

```javascript
const user = {
  name: "Alex",
  age: 20,
  country: "Bangladesh"
};

const { name, ...details } = user;

console.log(name);

console.log(details);
```

Output:

```javascript
Alex

{
  age: 20,
  country: "Bangladesh"
}
```

---

## 9. Nested Object Destructuring

```javascript
const person = {
  name: "Alex",
  address: {
    city: "Dhaka",
    zip: 1200
  }
};

const {
  address: { city, zip }
} = person;

console.log(city); // Dhaka
console.log(zip);  // 1200
```

---

## 10. Destructuring Function Parameters

Instead of:

```javascript
function showUser(user) {
  console.log(user.name);
}
```

Use:

```javascript
function showUser({ name, age }) {
  console.log(name);
  console.log(age);
}

showUser({
  name: "Alex",
  age: 20
});
```

---

## 11. Swapping Variables

```javascript
let a = 10;
let b = 20;

[a, b] = [b, a];

console.log(a); // 20
console.log(b); // 10
```

---

## 12. Combined Object + Array Destructuring

```javascript
const users = [
  {
    name: "Alex",
    skills: ["JS", "React"]
  }
];

const [
  {
    name,
    skills: [skill1, skill2]
  }
] = users;

console.log(name);  // Alex
console.log(skill1); // JS
console.log(skill2); // React
```

---

### Quick Cheat Sheet

```javascript
// Array
const [a, b] = array;

// Object
const {x, y} = object;

// Rename
const {x: newName} = object;

// Rest
const [a, ...rest] = array;
const {x, ...rest} = object;

// Default
const {x = value} = object;
```

Destructuring is commonly used with **ES6 modules, React, APIs, and modern JavaScript code**.

-------------

# Object Methods: `keys`, `values`, `entries`, `delete`, `seal`, `freeze` (ES6 JavaScript)

These are used to work with **objects**.

---

## 1. `Object.keys()`

Returns an array of object **property names (keys)**.

```javascript
const user = {
  name: "Alex",
  age: 20,
  city: "Dhaka"
};

console.log(Object.keys(user));
```

Output:

```javascript
["name", "age", "city"]
```

---

## 2. `Object.values()`

Returns an array of object **values**.

```javascript
const user = {
  name: "Alex",
  age: 20,
  city: "Dhaka"
};

console.log(Object.values(user));
```

Output:

```javascript
["Alex", 20, "Dhaka"]
```

---

## 3. `Object.entries()`

Returns an array of **key-value pairs**.

```javascript
const user = {
  name: "Alex",
  age: 20
};

console.log(Object.entries(user));
```

Output:

```javascript
[
  ["name", "Alex"],
  ["age", 20]
]
```

Example with loop:

```javascript
for (let [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

Output:

```text
name Alex
age 20
```

---

# Delete Property

`delete` removes a property from an object.

```javascript
const user = {
  name: "Alex",
  age: 20
};

delete user.age;

console.log(user);
```

Output:

```javascript
{
  name: "Alex"
}
```

---

# Object.seal()

`seal()` prevents:

- Adding new properties ❌
    
- Deleting properties ❌
    

But allows changing existing values ✅

```javascript
const user = {
  name: "Alex",
  age: 20
};

Object.seal(user);

user.age = 25; // allowed

user.city = "Dhaka"; // not allowed

delete user.name; // not allowed

console.log(user);
```

Output:

```javascript
{
  name: "Alex",
  age: 25
}
```

---

# Object.freeze()

`freeze()` makes an object completely unchangeable.

Prevents:

- Adding properties ❌
    
- Deleting properties ❌
    
- Changing values ❌
    

```javascript
const user = {
  name: "Alex",
  age: 20
};

Object.freeze(user);

user.age = 30; // not allowed
delete user.name; // not allowed

console.log(user);
```

Output:

```javascript
{
  name: "Alex",
  age: 20
}
```

---

## Seal vs Freeze

|Feature|seal()|freeze()|
|---|---|---|
|Add property|❌|❌|
|Delete property|❌|❌|
|Update value|✅|❌|
|Lock object|Partial|Complete|

---

### Quick Example

```javascript
const obj = {
  a: 1,
  b: 2
};

console.log(Object.keys(obj));   // ["a","b"]
console.log(Object.values(obj)); // [1,2]
console.log(Object.entries(obj));// [["a",1],["b",2]]

delete obj.a;

Object.seal(obj);
Object.freeze(obj);
```

These methods are widely used when handling **API data, configurations, and state management**.

------
# Access Value, Nested Object, Optional Chaining, Dot vs Bracket Notation (JavaScript)

## 1. Access Object Values

Objects store data as **key-value pairs**.

```javascript
const user = {
  name: "Alex",
  age: 20
};

console.log(user.name);
console.log(user.age);
```

Output:

```text
Alex
20
```

---

# 2. Dot Notation (`.`)

Use dot notation when the property name is a simple word.

```javascript
const person = {
  name: "John",
  city: "Dhaka"
};

console.log(person.name);
console.log(person.city);
```

Output:

```text
John
Dhaka
```

---

# 3. Bracket Notation (`[]`)

Use bracket notation when:

- Key is stored in a variable
    
- Key contains spaces/special characters
    

```javascript
const person = {
  name: "John",
  "phone number": "12345"
};

console.log(person["name"]);
console.log(person["phone number"]);
```

Output:

```text
John
12345
```

---

## Dot vs Bracket

```javascript
const key = "age";

const user = {
  name: "Alex",
  age: 20
};

console.log(user.key);     // undefined
console.log(user[key]);    // 20
```

Because:

- `user.key` looks for a property named **key**
    
- `user[key]` uses the value inside `key`
    

---

# 4. Nested Objects

An object can contain another object.

```javascript
const user = {
  name: "Alex",
  address: {
    city: "Dhaka",
    country: "Bangladesh"
  }
};

console.log(user.address.city);
```

Output:

```text
Dhaka
```

---

# 5. Nested Array Inside Object

```javascript
const student = {
  name: "Alex",
  skills: ["JavaScript", "React"]
};

console.log(student.skills[0]);
```

Output:

```text
JavaScript
```

---

# 6. Optional Chaining (`?.`)

Optional chaining prevents errors when a value does not exist.

Without optional chaining:

```javascript
const user = {};

console.log(user.address.city);
```

Error:

```text
Cannot read properties of undefined
```

With optional chaining:

```javascript
const user = {};

console.log(user.address?.city);
```

Output:

```text
undefined
```

---

## Optional Chaining Examples

### Object:

```javascript
const user = {
  profile: {
    name: "Alex"
  }
};

console.log(user.profile?.name);
```

Output:

```text
Alex
```

---

### Missing Object:

```javascript
const user = {};

console.log(user.profile?.name);
```

Output:

```text
undefined
```

---

### With Functions

```javascript
const user = {
  sayHello() {
    return "Hello";
  }
};

console.log(user.sayHello?.());
```

Output:

```text
Hello
```

---

### Quick Cheat Sheet

```javascript
// Dot notation
object.key

// Bracket notation
object["key"]

// Variable key
object[key]

// Nested object
object.child.key

// Safe access
object?.child?.key
```

Optional chaining (`?.`) is commonly used when working with **API responses and uncertain data**.

------------

# 🔥 Array `map()` — One-Line Loop Magic in JavaScript

`map()` is a powerful ES6 array method used to **loop through an array and return a NEW array**.

---

## 1. Basic Idea

Instead of writing loops:

```javascript
const numbers = [1, 2, 3, 4];
const result = [];

for (let i = 0; i < numbers.length; i++) {
  result.push(numbers[i] * 2);
}

console.log(result);
```

👉 You can use `map()` (one-line magic)

---

## 2. One-Line `map()` Example

```javascript
const numbers = [1, 2, 3, 4];

const result = numbers.map(n => n * 2);

console.log(result);
```

Output:

```text
[2, 4, 6, 8]
```

---

## 3. String Transformation

```javascript
const names = ["alex", "john", "mike"];

const upper = names.map(name => name.toUpperCase());

console.log(upper);
```

Output:

```text
["ALEX", "JOHN", "MIKE"]
```

---

## 4. Object Transformation (Very Important)

```javascript
const users = [
  { name: "Alex", age: 20 },
  { name: "John", age: 25 }
];

const names = users.map(user => user.name);

console.log(names);
```

Output:

```text
["Alex", "John"]
```

---

## 5. Returning Objects (Need Parentheses)

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(n => ({
  value: n,
  square: n * n
}));

console.log(result);
```

Output:

```text
[
  { value: 1, square: 1 },
  { value: 2, square: 4 },
  { value: 3, square: 9 }
]
```

---

## 6. Index in `map()`

```javascript
const items = ["A", "B", "C"];

const result = items.map((item, index) => {
  return `${index}: ${item}`;
});

console.log(result);
```

Output:

```text
["0: A", "1: B", "2: C"]
```

---

## 7. One-Line Power Version 🚀

```javascript
const nums = [2, 4, 6];

const doubled = nums.map(n => n * 2);
```

---

## ⚡ Key Idea

|Feature|map()|
|---|---|
|Returns new array|✅|
|Modifies original|❌|
|One-line possible|✅|
|Used for transformation|✅|

---

## 💡 Final Summary

```javascript
// Basic
arr.map(x => x * 2)

// With index
arr.map((x, i) => i + x)

// Return object
arr.map(x => ({ value: x }))
```

👉 `map()` = **loop + transform + return new array in one line** 🚀

------

# 🔁 `forEach`, `filter`, `find` — Array Methods in JavaScript (and Differences)

These are ES6 array methods used instead of traditional loops.

---

# 1. `forEach()` — Just Loop (No Return)

### 👉 Used for: running code for each element

```javascript
const numbers = [1, 2, 3];

numbers.forEach(num => {
  console.log(num * 2);
});
```

Output:

```text
2
4
6
```

### ⚠️ Important:

- Does NOT return a new array
    
- Only executes a function
    

---

# 2. `filter()` — Select Multiple Items

### 👉 Used for: getting a NEW array with matching conditions

```javascript
const numbers = [1, 2, 3, 4, 5];

const even = numbers.filter(num => num % 2 === 0);

console.log(even);
```

Output:

```text
[2, 4]
```

### ✔️ Key Idea:

- returns **array**
    
- keeps ALL items that match condition
    

---

# 3. `find()` — Get First Match Only

### 👉 Used for: getting the FIRST matching element

```javascript
const numbers = [1, 2, 3, 4, 5];

const firstEven = numbers.find(num => num % 2 === 0);

console.log(firstEven);
```

Output:

```text
2
```

### ✔️ Key Idea:

- returns **single value**
    
- stops when first match is found
    

---

# 🔥 REAL DIFFERENCE TABLE

|Method|Returns|Stops Early?|Use Case|
|---|---|---|---|
|`forEach()`|nothing (undefined)|No|just loop / side effects|
|`filter()`|array|No|multiple matches|
|`find()`|single value|Yes|first match|

---

# ⚡ Visual Understanding

### Array:

```javascript
const arr = [1, 2, 3, 4, 5];
```

### forEach:

👉 "Do something with each item"

```javascript
arr.forEach(x => console.log(x));
```

---

### filter:

👉 "Give me ALL even numbers"

```javascript
arr.filter(x => x % 2 === 0);
// [2, 4]
```

---

### find:

👉 "Give me FIRST even number"

```javascript
arr.find(x => x % 2 === 0);
// 2
```

---

# 💡 BONUS: Common Confusion

### ❌ Wrong thinking:

```javascript
const result = arr.forEach(x => x * 2); // undefined
```

### ✔️ Correct:

```javascript
const result = arr.map(x => x * 2); // [2,4,6,8,10]
```

---

# 🚀 Final Summary

- `forEach()` → loop only (no return)
    
- `filter()` → multiple results (array)
    
- `find()` → first match (single value)
    

---

If you want next level, I can also explain:  
👉 `map vs filter vs reduce (advanced interview level)`


---

### 🔥 `reduce()` in JavaScript (ES6)

`reduce()` is the **most powerful array method**.  
It is used to **reduce an array into a single value**.

---

# 🧠 Basic Idea

Instead of:

- looping
    
- adding manually
    
- building variables
    

You “reduce” everything into one result.

---

# 1. Basic Syntax

```javascript
array.reduce((accumulator, currentValue) => {
  return updatedAccumulator;
}, initialValue);
```

---

# 2. Sum of Numbers (Most Common Example)

### Without reduce:

```javascript
const nums = [1, 2, 3, 4];

let sum = 0;

for (let i = 0; i < nums.length; i++) {
  sum += nums[i];
}

console.log(sum);
```

---

### With reduce:

```javascript
const nums = [1, 2, 3, 4];

const sum = nums.reduce((acc, curr) => {
  return acc + curr;
}, 0);

console.log(sum);
```

Output:

```text
10
```

---

# 3. One-Line Reduce Magic ✨

```javascript
const nums = [1, 2, 3, 4];

const sum = nums.reduce((acc, curr) => acc + curr, 0);

console.log(sum);
```

---

# 4. Find Maximum Value

```javascript
const nums = [10, 5, 30, 8];

const max = nums.reduce((acc, curr) => {
  return curr > acc ? curr : acc;
}, nums[0]);

console.log(max);
```

Output:

```text
30
```

---

# 5. Count Occurrences

```javascript
const fruits = ["apple", "banana", "apple", "orange"];

const count = fruits.reduce((acc, fruit) => {
  acc[fruit] = (acc[fruit] || 0) + 1;
  return acc;
}, {});

console.log(count);
```

Output:

```text
{
  apple: 2,
  banana: 1,
  orange: 1
}
```

---

# 6. Convert Array → Object

```javascript
const users = [
  { id: 1, name: "Alex" },
  { id: 2, name: "John" }
];

const obj = users.reduce((acc, user) => {
  acc[user.id] = user.name;
  return acc;
}, {});

console.log(obj);
```

Output:

```text
{
  1: "Alex",
  2: "John"
}
```

---

# 🔥 How Reduce Works (Step-by-Step)

Example:

```javascript
[1, 2, 3].reduce((acc, curr) => acc + curr, 0);
```

|Step|acc|curr|Result|
|---|---|---|---|
|1|0|1|1|
|2|1|2|3|
|3|3|3|6|

Final output = **6**

---

# ⚡ Key Terms

|Term|Meaning|
|---|---|
|accumulator|stored result|
|currentValue|current array item|
|initialValue|starting value|

---

# 💥 Reduce vs Others

|Method|Purpose|Output|
|---|---|---|
|map|transform|array|
|filter|select|array|
|find|first match|value|
|reduce|combine|single value|

---

# 🚀 Final Summary

```javascript
// Sum
arr.reduce((a, b) => a + b, 0);

// Max
arr.reduce((a, b) => a > b ? a : b);

// Count
arr.reduce((acc, item) => {
  acc[item] = (acc[item] || 0) + 1;
  return acc;
}, {});
```

---

👉 `reduce()` = **turn an array into anything (number, object, array, logic, even map)** 🚀

------------
## 🧱 Introduction to Class and Objects (JavaScript OOP Basics)

JavaScript uses **Object-Oriented Programming (OOP)** to organize code using **classes and objects**.

---

# 1. What is an Object?

An **object** is a collection of **properties (data)** and **methods (functions)**.

### Example:

```javascript
const user = {
  name: "Alex",
  age: 20,
  greet: function () {
    console.log("Hello!");
  }
};

console.log(user.name);
user.greet();
```

### Output:

```text
Alex
Hello!
```

---

# 2. What is a Class?

A **class** is a **blueprint** for creating objects.

👉 Think of it like a **template**.

---

# 3. Basic Class Syntax

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log("Hello " + this.name);
  }
}
```

---

# 4. Creating Objects from Class

```javascript
const p1 = new Person("Alex", 20);
const p2 = new Person("John", 25);

console.log(p1.name);
console.log(p2.name);
```

### Output:

```text
Alex
John
```

---

# 5. Calling Methods

```javascript
p1.greet();
p2.greet();
```

### Output:

```text
Hello Alex
Hello John
```

---

# 6. Constructor (Very Important)

The **constructor()** runs automatically when an object is created.

```javascript
class Car {
  constructor(brand) {
    this.brand = brand;
  }
}

const car1 = new Car("Toyota");

console.log(car1.brand);
```

---

# 7. Class vs Object

|Class|Object|
|---|---|
|Blueprint|Real instance|
|Template|Created from class|
|No memory|Takes memory|
|Defined once|Many objects|

---

# 8. Multiple Objects from One Class

```javascript
class Student {
  constructor(name) {
    this.name = name;
  }
}

const s1 = new Student("Alex");
const s2 = new Student("John");
const s3 = new Student("Mike");

console.log(s1.name, s2.name, s3.name);
```

---

# 9. Why Use Classes?

✔ Organize code  
✔ Reuse logic  
✔ Easy to manage large applications  
✔ Used in frameworks (React, Angular, Node.js)

---

# 🚀 Real-Life Example

```javascript
class BankAccount {
  constructor(name, balance) {
    this.name = name;
    this.balance = balance;
  }

  deposit(amount) {
    this.balance += amount;
  }

  withdraw(amount) {
    this.balance -= amount;
  }
}

const acc = new BankAccount("Alex", 1000);

acc.deposit(500);
acc.withdraw(200);

console.log(acc.balance);
```

---

# ⚡ Final Summary

```javascript
// Class (blueprint)
class Person {}

// Object (instance)
const p = new Person();

// Constructor initializes data
constructor() {}

// Methods = functions inside class
methodName() {}
```

---

👉 In simple words:

- **Class = Design / Blueprint**
    
- **Object = Real thing created from that design**
    

---


## 🧬 Inheritance & Prototypical Inheritance (JavaScript OOP)

Inheritance lets one class or object **reuse properties and methods** from another.

---

# 1. What is Inheritance?

👉 Inheritance = **child gets features from parent**

Example idea:

- Parent: Animal
    
- Child: Dog → gets Animal features + its own
    

---

# 2. Class Inheritance (ES6)

### Parent Class

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(this.name + " makes a sound");
  }
}
```

---

### Child Class (`extends`)

```javascript
class Dog extends Animal {
  bark() {
    console.log(this.name + " barks");
  }
}
```

---

### Using It

```javascript
const d1 = new Dog("Tommy");

d1.speak(); // inherited
d1.bark();  // own method
```

### Output:

```text
Tommy makes a sound
Tommy barks
```

---

# 3. `super()` Keyword

Used to call parent constructor.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Cat extends Animal {
  constructor(name, color) {
    super(name); // call parent
    this.color = color;
  }
}
```

---

# 🧠 Prototypical Inheritance (Core JavaScript Concept)

JavaScript uses **prototypes behind the scenes**.

👉 Every object has a hidden link called:

```text
[[Prototype]]
```

---

# 4. Prototype Example

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log("Hello " + this.name);
};

const p1 = new Person("Alex");

p1.greet();
```

### Output:

```text
Hello Alex
```

---

# 5. How Prototype Works

```javascript
p1 → Person.prototype → Object.prototype → null
```

If JS does NOT find a method in object, it looks in prototype chain.

---

# 6. Class = Syntactic Sugar

This:

```javascript
class Dog {
  bark() {
    console.log("Woof");
  }
}
```

Is actually:

```javascript
function Dog() {}

Dog.prototype.bark = function () {
  console.log("Woof");
};
```

👉 So **classes use prototypes internally**

---

# 7. Prototype Chain Example

```javascript
const arr = [1, 2, 3];

console.log(arr.push(4));
```

Why `.push()` works?

Because:

```text
arr → Array.prototype → Object.prototype
```

---

# 8. Inheritance Types

|Type|Meaning|
|---|---|
|Class inheritance|`extends` keyword|
|Prototypal inheritance|objects linking via prototype|
|Method reuse|shared functions|

---

# 🔥 Real-Life Example

```javascript
class Vehicle {
  start() {
    console.log("Vehicle started");
  }
}

class Car extends Vehicle {
  drive() {
    console.log("Car is driving");
  }
}

const c = new Car();

c.start();
c.drive();
```

---

# ⚡ Key Differences

|Class Inheritance|Prototype Inheritance|
|---|---|
|Modern syntax|Old JS system|
|Uses `class`, `extends`|Uses `.prototype`|
|Easier to read|More internal logic|
|Built on prototypes|Core mechanism|

---

# 🚀 Final Summary

```javascript
// Class inheritance
class B extends A {}

// Call parent
super()

// Prototype method
Constructor.prototype.method = function() {}

// Prototype chain
object → prototype → prototype → null
```

---

👉 Simple meaning:

- **Inheritance = reuse code**
    
- **Prototype = how JS actually does inheritance under the hood**
    

---

## 🔒 Encapsulation & `this` Keyword (JavaScript OOP)

These are two core ideas in Object-Oriented Programming (OOP).

---

# 1. What is Encapsulation?

👉 **Encapsulation = hiding data + controlling access**

It means:

- Keep data safe inside a class
    
- Only allow access through methods
    
- Prevent direct modification (in proper design)
    

---

## 2. Basic Encapsulation Example (Without Protection)

```javascript
class BankAccount {
  constructor(balance) {
    this.balance = balance;
  }
}

const acc = new BankAccount(1000);

acc.balance = 5000; // ❌ direct change (not safe)

console.log(acc.balance);
```

Problem:  
👉 Anyone can change the value directly

---

# 3. Encapsulation with Methods (Better Way)

```javascript
class BankAccount {
  constructor(balance) {
    this.balance = balance;
  }

  deposit(amount) {
    this.balance += amount;
  }

  withdraw(amount) {
    this.balance -= amount;
  }

  getBalance() {
    return this.balance;
  }
}
```

Usage:

```javascript
const acc = new BankAccount(1000);

acc.deposit(500);
acc.withdraw(200);

console.log(acc.getBalance());
```

---

# 4. True Encapsulation (Private Fields `#`)

ES6 introduced **real private variables**.

```javascript
class BankAccount {
  #balance; // private

  constructor(balance) {
    this.#balance = balance;
  }

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}
```

### Usage:

```javascript
const acc = new BankAccount(1000);

acc.deposit(500);

console.log(acc.getBalance());
```

### ❌ Not allowed:

```javascript
// acc.#balance = 5000; ❌ Error
```

---

# 🧠 What is `this` Keyword?

👉 `this` refers to the **current object**

---

# 5. `this` in Object

```javascript
const user = {
  name: "Alex",
  greet: function () {
    console.log("Hello " + this.name);
  }
};

user.greet();
```

Output:

```text
Hello Alex
```

👉 `this.name` = `user.name`

---

# 6. `this` in Class

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  show() {
    console.log(this.name);
  }
}

const p = new Person("John");
p.show();
```

Output:

```text
John
```

---

# 7. `this` in Different Contexts

## Inside object method

```javascript
this → object itself
```

## Inside class

```javascript
this → instance of class
```

## Outside function

```javascript
console.log(this); // window (browser) or undefined (strict mode)
```

---

# 8. Arrow Function and `this`

Arrow functions **do NOT have their own `this`**

```javascript
const user = {
  name: "Alex",
  greet: () => {
    console.log(this.name);
  }
};

user.greet();
```

Output:

```text
undefined
```

👉 Because arrow function inherits `this` from outside scope.

---

# ⚡ Difference Table

|Feature|Encapsulation|`this`|
|---|---|---|
|Purpose|Protect data|Refer current object|
|Tool|private fields (`#`)|keyword|
|Usage|data security|object access|
|Example|`#balance`|`this.balance`|

---

# 🔥 Real-Life Example

```javascript
class User {
  #password;

  constructor(name, password) {
    this.name = name;
    this.#password = password;
  }

  checkPassword(pass) {
    return this.#password === pass;
  }
}

const u1 = new User("Alex", "1234");

console.log(u1.checkPassword("1234"));
```

---

# 🚀 Final Summary

```javascript
// Encapsulation
class A {
  #privateValue;
}

// Access via methods
getValue()

// this keyword
this → current object

// Problem with arrow function
() => this  // no own this
```

---

👉 Simple meaning:

- **Encapsulation = hide data, protect it**
    
- **this = refers to current object**
    

---

## 🧠 Polymorphism in JavaScript (OOP Concept)

👉 **Polymorphism = “many forms”**

It means:

> The same method name can behave differently in different situations.

---

# 1. Simple Idea

One method → different behavior

Example:

- Animal speaks differently
    
- Dog barks
    
- Cat meows
    

---

# 2. Polymorphism using Class Inheritance

## Parent Class

```javascript
class Animal {
  speak() {
    console.log("Animal makes a sound");
  }
}
```

---

## Child Classes (Different Behavior)

```javascript
class Dog extends Animal {
  speak() {
    console.log("Dog barks");
  }
}

class Cat extends Animal {
  speak() {
    console.log("Cat meows");
  }
}
```

---

## Using Polymorphism

```javascript
const animals = [new Animal(), new Dog(), new Cat()];

animals.forEach(animal => animal.speak());
```

---

### Output:

```text
Animal makes a sound
Dog barks
Cat meows
```

👉 Same method name: `speak()`  
👉 Different behavior depending on object

---

# 3. Real-Life Example

```javascript
class Shape {
  draw() {
    console.log("Drawing shape");
  }
}

class Circle extends Shape {
  draw() {
    console.log("Drawing circle");
  }
}

class Square extends Shape {
  draw() {
    console.log("Drawing square");
  }
}
```

Usage:

```javascript
const shapes = [new Shape(), new Circle(), new Square()];

shapes.forEach(shape => shape.draw());
```

---

# 4. Polymorphism Without Classes

Even simple functions show polymorphism:

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(2, 3));      // numbers
console.log(add("2", "3"));  // strings
```

Output:

```text
5
23
```

👉 Same function, different behavior

---

# 5. Types of Polymorphism

## 1. Compile-time (not in JS much)

- Method overloading (not supported directly in JS)
    

## 2. Run-time (MOST IMPORTANT in JS)

- Method overriding (class inheritance)
    

---

# 6. Method Overriding (Key Concept)

Child class **replaces** parent method:

```javascript
class Parent {
  show() {
    console.log("Parent method");
  }
}

class Child extends Parent {
  show() {
    console.log("Child method");
  }
}

const obj = new Child();
obj.show();
```

Output:

```text
Child method
```

---

# 7. Why Polymorphism is Useful

✔ Cleaner code  
✔ Easy to extend  
✔ Same interface, different behavior  
✔ Used in frameworks (React, Node, etc.)

---

# 8. Real-Life Analogy

👉 “Play button”

- Music app → plays song 🎵
    
- Video app → plays video 🎬
    
- Game → starts game 🎮
    

Same action → different behavior

---

# ⚡ Quick Summary

```javascript
// Same method name, different behavior
class A {
  speak() {}
}

class B extends A {
  speak() {}
}

class C extends A {
  speak() {}
}
```

---

# 🚀 Final Definition

👉 **Polymorphism = one interface, multiple behaviors**

---

