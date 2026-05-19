**JavaScript Core topics**, here’s a solid list of foundational topics to learn:

1. **Introduction to JavaScript**
## Introduction to JavaScript

**JavaScript** is a high-level, lightweight, interpreted programming language used to make websites interactive and dynamic. It is one of the three core technologies of web development, alongside:

* HTML → Structure of a webpage
* CSS → Style/design of a webpage
* JavaScript → Behavior/interactivity of a webpage

### What JavaScript Can Do

With JavaScript, you can:

✅ Change webpage content dynamically
✅ Show alerts / notifications
✅ Validate forms
✅ Create animations
✅ Build games
✅ Fetch data from servers without reloading the page
✅ Create full-stack applications (frontend + backend with Node.js)

### Example

```javascript
console.log("Hello World!");
alert("Welcome to JavaScript");
```

**Output:**

* Prints **Hello World!** in the browser console
* Shows a popup message

### Why Learn JavaScript?

* Very popular language
* Runs in every modern browser
* Used for web, mobile, backend, and desktop apps
* Huge ecosystem and community

### Where JavaScript Runs

1. **Browser** → Chrome, Firefox, Edge, Safari
2. **Server** → Using Node.js
3. **Mobile Apps** → Using frameworks like React Native
4. **Desktop Apps** → Using Electron

### Key Features

* Easy to learn
* Dynamic typing
* Object-oriented
* Functional programming support
* Event-driven
* Asynchronous programming





## Variables in JavaScript (`var`, `let`, `const`)

A **variable** is a container used to store data in memory.

Example:

```javascript id="92txjy"
let name = "Rahim";
console.log(name);
```

Output:

```javascript id="5xv5dn"
Rahim
```

Here, `name` stores the value `"Rahim"`.

---

## 1) `var`

`var` is the old way to declare variables in JavaScript.

Example:

```javascript id="g0k6to"
var age = 25;
console.log(age);
```

### Features of `var`

✅ Can be **redeclared**

```javascript id="yy3scx"
var x = 10;
var x = 20;
console.log(x); // 20
```

✅ Can be **updated**

```javascript id="27cps0"
var city = "Dhaka";
city = "Chittagong";
console.log(city);
```

✅ **Function scoped** (not block scoped)

Example:

```javascript id="ufow3o"
if (true) {
  var test = "Hello";
}
console.log(test); // Works
```

⚠️ Because of redeclaration and scope issues, `var` is less preferred now.

---

## 2) `let`

`let` is the modern way to declare variables.

Example:

```javascript id="d03iij"
let age = 22;
console.log(age);
```

### Features of `let`

❌ Cannot be redeclared in same scope

```javascript id="p7rllg"
let x = 10;
let x = 20; // Error
```

✅ Can be updated

```javascript id="5jx0s7"
let score = 50;
score = 80;
console.log(score);
```

✅ **Block scoped**

```javascript id="6aez1n"
if (true) {
  let msg = "Hi";
}
console.log(msg); // Error
```

Use `let` when value may change.

---

## 3) `const`

`const` is used for constant values.

Example:

```javascript id="fml5qq"
const pi = 3.1416;
console.log(pi);
```

### Features of `const`

❌ Cannot be redeclared

❌ Cannot be updated

```javascript id="h3h39p"
const x = 10;
x = 20; // Error
```

✅ Block scoped

✅ Must initialize immediately

```javascript id="2ht0pc"
const name = "JavaScript";
```

Wrong:

```javascript id="uvzclh"
const name; // Error
```

Use `const` when value should not change.

---

## Difference Table

| Feature   | `var`    | `let`       | `const`     |
| --------- | -------- | ----------- | ----------- |
| Redeclare | ✅ Yes    | ❌ No        | ❌ No        |
| Update    | ✅ Yes    | ✅ Yes       | ❌ No        |
| Scope     | Function | Block       | Block       |
| Hoisted   | ✅ Yes    | ✅ Yes (TDZ) | ✅ Yes (TDZ) |

---

## Best Practice

Use:

* **`const`** → default choice
* **`let`** → when value changes
* Avoid **`var`** in modern code

Example:

```javascript id="4dvs0k"
const country = "Bangladesh";
let age = 25;
age = 26;
```

This is the common modern JavaScript style.

# **Data Types** (String, Number, Boolean, Null, Undefined, Object, Symbol, BigInt)


## Data Types in JavaScript

A **data type** tells JavaScript what kind of value a variable holds.

Example:

```javascript id="g7h24p"
let name = "Rahim";   // String
let age = 25;         // Number
let isStudent = true; // Boolean
```

JavaScript has **8 main data types**:

### Primitive Types (7)

1. String
2. Number
3. Boolean
4. Null
5. Undefined
6. Symbol
7. BigInt

### Non-Primitive Type (1)

8. Object

---

## 1) String

A **String** is text inside quotes.

Example:

```javascript id="t8o78u"
let name = "Rahim";
let city = 'Dhaka';
```

Output:

```javascript id="iq0kec"
console.log(name); // Rahim
```

Used for:
✅ Names
✅ Messages
✅ Text data

---

## 2) Number

Represents numbers (integer or decimal).

Example:

```javascript id="0jl58y"
let age = 25;
let price = 99.99;
```

Output:

```javascript id="8f5e4c"
console.log(age); // 25
```

Used for:
✅ Age
✅ Price
✅ Calculations

---

## 3) Boolean

Boolean has only **two values**:

* `true`
* `false`

Example:

```javascript id="6n2g9g"
let isLoggedIn = true;
let hasMoney = false;
```

Used for:
✅ Conditions
✅ Checking status
✅ Logic operations

---

## 4) Null

`null` means **empty / no value intentionally assigned**.

Example:

```javascript id="gtp1sl"
let user = null;
```

Meaning:

> "There is no value now."

Example:

```javascript id="vwbj6q"
let selectedColor = null;
```

---

## 5) Undefined

A variable declared but not assigned gets `undefined`.

Example:

```javascript id="a5l1an"
let age;
console.log(age);
```

Output:

```javascript id="2u2n0u"
undefined
```

Meaning:

> Value not assigned yet.

---

## 6) Object

Object stores multiple values in **key:value pairs**.

Example:

```javascript id="g4rm1w"
let person = {
  name: "Rahim",
  age: 25,
  city: "Dhaka"
};
```

Access:

```javascript id="jlwmcw"
console.log(person.name);
```

Output:

```javascript id="hfx85v"
Rahim
```

Used for:
✅ User data
✅ Complex data structures

---

## 7) Symbol

A **Symbol** creates a unique value.

Example:

```javascript id="whbj0m"
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2);
```

Output:

```javascript id="9v0i3x"
false
```

Even with same description, Symbols are unique.

Used for:
✅ Unique object keys
✅ Internal identifiers

---

## 8) BigInt

Used for very large integers beyond normal Number limit.

Example:

```javascript id="3u7zy0"
let bigNumber = 123456789012345678901234567890n;
```

Notice `n` at the end.

Used for:
✅ Huge calculations
✅ Large IDs / precise integers

---

## Check Type with `typeof`

Use `typeof` to know data type:

```javascript id="cdygl0"
console.log(typeof "Hello"); // string
console.log(typeof 100);     // number
console.log(typeof true);    // boolean
```

---

## Summary Table

| Type      | Example          |
| --------- | ---------------- |
| String    | `"Hello"`        |
| Number    | `100`            |
| Boolean   | `true`           |
| Null      | `null`           |
| Undefined | `undefined`      |
| Object    | `{name:"Rahim"}` |
| Symbol    | `Symbol("id")`   |
| BigInt    | `123n`           |

These are the core building blocks of JavaScript values.

# **Operators** (Arithmetic, Comparison, Logical, Assignment)
## Operators in JavaScript

**Operators** are symbols used to perform operations on values and variables.

Example:

```javascript id="8ffk12"
let a = 10;
let b = 5;

console.log(a + b); // 15
```

Here `+` is an operator.

There are **4 important types**:

1. Arithmetic Operators
2. Comparison Operators
3. Logical Operators
4. Assignment Operators

---

## 1) Arithmetic Operators

Used for math calculations.

| Operator | Meaning             | Example  | Result |
| -------- | ------------------- | -------- | ------ |
| `+`      | Add                 | `10 + 5` | `15`   |
| `-`      | Subtract            | `10 - 5` | `5`    |
| `*`      | Multiply            | `10 * 5` | `50`   |
| `/`      | Divide              | `10 / 5` | `2`    |
| `%`      | Modulus (remainder) | `10 % 3` | `1`    |
| `**`     | Power               | `2 ** 3` | `8`    |

Example:

```javascript id="vynx8j"
let a = 10;
let b = 3;

console.log(a + b); // 13
console.log(a - b); // 7
console.log(a * b); // 30
console.log(a / b); // 3.33
console.log(a % b); // 1
console.log(a ** b); // 1000
```

### Increment / Decrement

Increase or decrease by 1.

```javascript id="h8p4v1"
let x = 5;
x++;
console.log(x); // 6

x--;
console.log(x); // 5
```

---

## 2) Comparison Operators

Used to compare values.

Result is always **true** or **false**.

| Operator | Meaning          |
| -------- | ---------------- |
| `==`     | Equal            |
| `===`    | Strict Equal     |
| `!=`     | Not Equal        |
| `!==`    | Strict Not Equal |
| `>`      | Greater than     |
| `<`      | Less than        |
| `>=`     | Greater or equal |
| `<=`     | Less or equal    |

Example:

```javascript id="cqx0kp"
console.log(5 > 3);    // true
console.log(5 < 3);    // false
console.log(5 == "5"); // true
console.log(5 === "5");// false
```

### Difference:

`==` checks value only
`===` checks value + type

Example:

```javascript id="tgt90p"
10 == "10"   // true
10 === "10"  // false
```

---

## 3) Logical Operators

Used for combining conditions.

| Operator | Meaning |   |    |
| -------- | ------- | - | -- |
| `&&`     | AND     |   |    |
| `        |         | ` | OR |
| `!`      | NOT     |   |    |

### AND (`&&`)

Both must be true.

```javascript id="zv9gh0"
console.log(true && true);   // true
console.log(true && false);  // false
```

### OR (`||`)

One true is enough.

```javascript id="l5ax02"
console.log(true || false); // true
console.log(false || false);// false
```

### NOT (`!`)

Reverse value.

```javascript id="u6dc8l"
console.log(!true);  // false
console.log(!false); // true
```

Example:

```javascript id="0ngw2h"
let age = 20;
let hasID = true;

console.log(age >= 18 && hasID); // true
```

---

## 4) Assignment Operators

Used to assign values.

| Operator | Example  | Same As     |
| -------- | -------- | ----------- |
| `=`      | `x = 5`  | assign      |
| `+=`     | `x += 2` | `x = x + 2` |
| `-=`     | `x -= 2` | `x = x - 2` |
| `*=`     | `x *= 2` | `x = x * 2` |
| `/=`     | `x /= 2` | `x = x / 2` |

Example:

```javascript id="67i7i0"
let x = 10;

x += 5;
console.log(x); // 15

x -= 3;
console.log(x); // 12
```

---

## Summary

* **Arithmetic** → Math (`+ - * / %`)
* **Comparison** → Compare (`== === > <`)
* **Logical** → Combine conditions (`&& || !`)
* **Assignment** → Assign/update (`= += -=`)

Operators are essential because almost every JavaScript program uses them.

# **Type Conversion & Type Coercion**

## Type Conversion & Type Coercion in JavaScript

In JavaScript, values can change from one data type to another.

Example:

* Number → String
* String → Number
* Boolean → Number

There are **2 ways** this happens:

1. **Type Conversion (Explicit)** → You do it manually
2. **Type Coercion (Implicit)** → JavaScript does it automatically

---

# 1) Type Conversion (Explicit)

Manual conversion by programmer.

## Convert to String

Use `String()`.

Example:

```javascript id="1jvok6"
let num = 100;
let text = String(num);

console.log(text);        // "100"
console.log(typeof text); // string
```

Number became String.

---

## Convert to Number

Use `Number()`.

Example:

```javascript id="r7x8vx"
let text = "250";
let num = Number(text);

console.log(num);         // 250
console.log(typeof num);  // number
```

String became Number.

If invalid:

```javascript id="mjlwm1"
Number("Hello");
```

Output:

```javascript id="6owh2r"
NaN
```

`NaN` = Not a Number

---

## Convert to Boolean

Use `Boolean()`.

Example:

```javascript id="46r3q0"
console.log(Boolean(1));      // true
console.log(Boolean(0));      // false
console.log(Boolean("Hi"));   // true
console.log(Boolean(""));     // false
console.log(Boolean(null));   // false
```

---

## Quick Conversion Tricks

```javascript id="s7v6j6"
+"100"      // 100
!!"Hello"   // true
100 + ""    // "100"
```

These are shortcuts.

---

# 2) Type Coercion (Implicit)

Automatic conversion by JavaScript.

JavaScript changes type when needed.

---

## String Coercion

If one value is string, result often becomes string.

Example:

```javascript id="jlwm5s"
console.log("5" + 2);
```

Output:

```javascript id="f8w6yv"
"52"
```

Why?
Number `2` converted to string `"2"`.

Then:

```javascript id="7n2k7m"
"5" + "2"
```

Result:

```javascript id="54kfg1"
"52"
```

---

## Number Coercion

Math operators convert strings to numbers.

Example:

```javascript id="gvx2a8"
console.log("10" - 5); // 5
console.log("10" * 2); // 20
console.log("10" / 2); // 5
```

String `"10"` becomes number `10`.

---

## Boolean Coercion

In conditions, JavaScript converts values to true/false.

Example:

```javascript id="b8w0gn"
if ("Hello") {
  console.log("True");
}
```

Output:

```javascript id="57b3t7"
True
```

Non-empty string = truthy.

---

# Truthy Values

Behave like `true`:

```javascript id="mpjlwm"
"Hello"
1
100
[]
{}
true
```

Example:

```javascript id="sglb1x"
if ([]) {
  console.log("Truthy");
}
```

Runs successfully.

---

# Falsy Values

Behave like `false`:

```javascript id="w4w2br"
false
0
""
null
undefined
NaN
```

Example:

```javascript id="hm52dz"
if (0) {
  console.log("Run");
}
```

Will not run.

---

# `==` vs `===`

Important coercion example:

## Loose Equality (`==`)

Allows coercion.

```javascript id="wnjlwm"
console.log(5 == "5");
```

Output:

```javascript id="p0zv6t"
true
```

String converted to number.

---

## Strict Equality (`===`)

No coercion.

```javascript id="ry60q9"
console.log(5 === "5");
```

Output:

```javascript id="mavf5u"
false
```

Different types.

---

# Best Practice

Use:

✅ `===` instead of `==`
✅ Convert types manually when needed
✅ Avoid relying on automatic coercion too much

This makes code clearer and safer.

# **Conditionals** (`if`, `else`, `switch`)

## Conditionals in JavaScript (`if`, `else`, `switch`)

**Conditionals** are used to make decisions in a program.

Example:

> If condition is true → run code
> If false → run another code

---

# 1) `if` Statement

Runs code only when condition is true.

### Syntax:

```javascript id="2w1m9u"
if (condition) {
   // code
}
```

### Example:

```javascript id="0o6h3r"
let age = 20;

if (age >= 18) {
   console.log("You can vote");
}
```

Output:

```javascript id="8n5k2f"
You can vote
```

Condition is true, so code runs.

---

# 2) `if...else`

Runs one block if true, another if false.

### Syntax:

```javascript id="r7g1vl"
if (condition) {
   // true block
} else {
   // false block
}
```

### Example:

```javascript id="g4u8ya"
let age = 15;

if (age >= 18) {
   console.log("Adult");
} else {
   console.log("Minor");
}
```

Output:

```javascript id="p2z7de"
Minor
```

---

# 3) `else if`

Checks multiple conditions.

### Syntax:

```javascript id="r0q5km"
if (condition1) {
   // code
} else if (condition2) {
   // code
} else {
   // code
}
```

### Example:

```javascript id="6y3a8j"
let marks = 85;

if (marks >= 80) {
   console.log("A+");
} else if (marks >= 60) {
   console.log("A");
} else if (marks >= 40) {
   console.log("Pass");
} else {
   console.log("Fail");
}
```

Output:

```javascript id="z7u1pt"
A+
```

---

# Nested `if`

`if` inside another `if`.

Example:

```javascript id="n3w7cx"
let age = 20;
let hasID = true;

if (age >= 18) {
   if (hasID) {
      console.log("Allowed");
   }
}
```

Output:

```javascript id="1k8xve"
Allowed
```

---

# 4) `switch`

Used when checking many exact values.

Cleaner than many `else if`.

### Syntax:

```javascript id="3m4xpa"
switch(value) {
   case value1:
      // code
      break;

   case value2:
      // code
      break;

   default:
      // code
}
```

### Example:

```javascript id="4v2dqa"
let day = 3;

switch(day) {
   case 1:
      console.log("Saturday");
      break;

   case 2:
      console.log("Sunday");
      break;

   case 3:
      console.log("Monday");
      break;

   default:
      console.log("Invalid");
}
```

Output:

```javascript id="9j1xsr"
Monday
```

---

# Why `break`?

Without `break`, next cases also run.

Example:

```javascript id="w8t4lm"
let x = 1;

switch(x) {
   case 1:
      console.log("One");
   case 2:
      console.log("Two");
}
```

Output:

```javascript id="m6q2bz"
One
Two
```

Because no `break`.

---

# Ternary Operator (Short `if...else`)

Short way to write condition.

Syntax:

```javascript id="5f7knd"
condition ? trueValue : falseValue
```

Example:

```javascript id="x2v9hc"
let age = 20;

let result = age >= 18 ? "Adult" : "Minor";

console.log(result);
```

Output:

```javascript id="v1n4qy"
Adult
```

---

# Summary

### Use `if`

When checking one condition.

### Use `if...else`

Two possible results.

### Use `else if`

Multiple conditions.

### Use `switch`

Many exact values.

### Use ternary

Short simple conditions.

Conditionals control the flow of your JavaScript program.


# **Loops** (`for`, `while`, `do...while`, `for...of`, `for...in`)


## Loops in JavaScript

A **loop** is used to run the same block of code repeatedly until a condition becomes false.

Example:
Instead of writing:

```javascript id="a1"
console.log("Hello");
console.log("Hello");
console.log("Hello");
```

Use loop:

```javascript id="a2"
for (let i = 1; i <= 3; i++) {
  console.log("Hello");
}
```

Output:

```javascript id="a3"
Hello
Hello
Hello
```

JavaScript has several loops:

1. `for` loop
2. `while` loop
3. `do...while` loop
4. `for...of` loop
5. `for...in` loop

---

# 1) `for` Loop

Used when you know how many times to repeat.

### Syntax:

```javascript id="a4"
for (initialization; condition; update) {
   // code
}
```

Example:

```javascript id="a5"
for (let i = 1; i <= 5; i++) {
   console.log(i);
}
```

Output:

```javascript id="a6"
1
2
3
4
5
```

### How it works:

* `let i = 1` → start
* `i <= 5` → check condition
* `i++` → increase by 1

---

# 2) `while` Loop

Runs while condition is true.

### Syntax:

```javascript id="a7"
while (condition) {
   // code
}
```

Example:

```javascript id="a8"
let i = 1;

while (i <= 5) {
   console.log(i);
   i++;
}
```

Output:

```javascript id="a9"
1
2
3
4
5
```

Condition checked first.

---

# 3) `do...while` Loop

Runs code **at least once**, then checks condition.

### Syntax:

```javascript id="a10"
do {
   // code
} while (condition);
```

Example:

```javascript id="a11"
let i = 1;

do {
   console.log(i);
   i++;
} while (i <= 5);
```

Output:

```javascript id="a12"
1
2
3
4
5
```

Even if condition is false initially, it runs once.

Example:

```javascript id="a13"
let x = 10;

do {
   console.log("Run once");
} while (x < 5);
```

Output:

```javascript id="a14"
Run once
```

---

# 4) `for...of`

Used for **iterating values** of arrays, strings, etc.

Example with array:

```javascript id="a15"
let fruits = ["Apple", "Banana", "Mango"];

for (let fruit of fruits) {
   console.log(fruit);
}
```

Output:

```javascript id="a16"
Apple
Banana
Mango
```

Example with string:

```javascript id="a17"
let name = "JS";

for (let char of name) {
   console.log(char);
}
```

Output:

```javascript id="a18"
J
S
```

---

# 5) `for...in`

Used for **iterating object keys**.

Example:

```javascript id="a19"
let person = {
   name: "Rahim",
   age: 25,
   city: "Dhaka"
};

for (let key in person) {
   console.log(key);
}
```

Output:

```javascript id="a20"
name
age
city
```

Get values:

```javascript id="a21"
for (let key in person) {
   console.log(person[key]);
}
```

Output:

```javascript id="a22"
Rahim
25
Dhaka
```

---

# `break`

Stops loop immediately.

Example:

```javascript id="a23"
for (let i = 1; i <= 5; i++) {
   if (i === 3) break;
   console.log(i);
}
```

Output:

```javascript id="a24"
1
2
```

---

# `continue`

Skips current iteration.

Example:

```javascript id="a25"
for (let i = 1; i <= 5; i++) {
   if (i === 3) continue;
   console.log(i);
}
```

Output:

```javascript id="a26"
1
2
4
5
```

---

# Summary

| Loop         | Use                         |
| ------------ | --------------------------- |
| `for`        | Known number of times       |
| `while`      | Repeat while condition true |
| `do...while` | Run at least once           |
| `for...of`   | Array / string values       |
| `for...in`   | Object keys                 |

Loops save time and make code cleaner.

# **Functions** (Declaration, Expression, Arrow Function)


## Functions in JavaScript

(**Declaration, Expression, Arrow Function**)

A **function** is a reusable block of code that performs a specific task.

Example:

```javascript id="f1"
function greet() {
  console.log("Hello");
}

greet();
```

Output:

```javascript id="f2"
Hello
```

Why use functions?
✅ Reuse code
✅ Keep code organized
✅ Make programs easier to manage

---

# 1) Function Declaration

The standard way to create a function.

### Syntax:

```javascript id="f3"
function functionName(parameters) {
   // code
}
```

Example:

```javascript id="f4"
function sayHello() {
  console.log("Hello World");
}

sayHello();
```

Output:

```javascript id="f5"
Hello World
```

### With Parameters

Parameters receive values.

Example:

```javascript id="f6"
function greet(name) {
  console.log("Hello " + name);
}

greet("Rahim");
greet("Karim");
```

Output:

```javascript id="f7"
Hello Rahim
Hello Karim
```

Here:

* `name` → parameter
* `"Rahim"` → argument

---

### Return Value

Function can return data.

Example:

```javascript id="f8"
function add(a, b) {
  return a + b;
}

let result = add(5, 3);
console.log(result);
```

Output:

```javascript id="f9"
8
```

`return` sends value back.

---

# 2) Function Expression

Store function in a variable.

Example:

```javascript id="f10"
const greet = function() {
  console.log("Hello");
};

greet();
```

Output:

```javascript id="f11"
Hello
```

With parameters:

```javascript id="f12"
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(2, 3));
```

Output:

```javascript id="f13"
6
```

---

# 3) Arrow Function

Modern ES6 function syntax.

Syntax:

```javascript id="f14"
const functionName = (parameters) => {
   // code
};
```

Example:

```javascript id="f15"
const greet = () => {
  console.log("Hello");
};

greet();
```

Output:

```javascript id="f16"
Hello
```

With parameters:

```javascript id="f17"
const add = (a, b) => {
  return a + b;
};

console.log(add(10, 5));
```

Output:

```javascript id="f18"
15
```

---

## Short Arrow Function

If one line:

```javascript id="f19"
const add = (a, b) => a + b;

console.log(add(5, 2));
```

Output:

```javascript id="f20"
7
```

No `return` needed.

---

## Single Parameter

Parentheses optional:

```javascript id="f21"
const square = x => x * x;

console.log(square(4));
```

Output:

```javascript id="f22"
16
```

---

# Difference Table

| Type        | Syntax                      | Hoisted |
| ----------- | --------------------------- | ------- |
| Declaration | `function test(){}`         | ✅ Yes   |
| Expression  | `const test = function(){}` | ❌ No    |
| Arrow       | `const test = ()=>{}`       | ❌ No    |

---

# Important: `this`

Arrow functions handle `this` differently than normal functions.
This becomes important later when learning objects and classes.

---

# Summary

### Function Declaration

Best for normal reusable functions.

### Function Expression

Useful when storing function in variable.

### Arrow Function

Modern, short, clean syntax.

Functions are one of the most important concepts in JavaScript.



# **Scope** (Global, Local, Block)


## Scope in JavaScript

(**Global, Local, Block**)

**Scope** means:

> **Where a variable can be accessed in code.**

Some variables can be used anywhere, while others only inside a specific area.

There are **3 main scopes**:

1. Global Scope
2. Local / Function Scope
3. Block Scope

---

# 1) Global Scope

A variable declared outside any function or block is **global**.

It can be accessed from anywhere.

Example:

```javascript id="s1"
let name = "Rahim";

function greet() {
  console.log(name);
}

console.log(name);
greet();
```

Output:

```javascript id="s2"
Rahim
Rahim
```

Because `name` is global.

### Global variables:

✅ Accessible everywhere
❌ Too many globals can create bugs

Use carefully.

---

# 2) Local / Function Scope

Variables declared inside a function are **local**.

Only accessible inside that function.

Example:

```javascript id="s3"
function test() {
  let age = 25;
  console.log(age);
}

test();
console.log(age);
```

Output:

```javascript id="s4"
25
ReferenceError
```

`age` exists only inside `test()`.

Outside → not accessible.

---

## Function creates its own scope

Example:

```javascript id="s5"
function one() {
  let x = 10;
  console.log(x);
}

function two() {
  let y = 20;
  console.log(y);
}

one();
two();
```

`x` only in `one()`
`y` only in `two()`

Separate scopes.

---

# 3) Block Scope

Anything inside `{ }` is a block.

Variables declared with:

* `let`
* `const`

are block scoped.

Example:

```javascript id="s6"
if (true) {
  let message = "Hello";
  console.log(message);
}

console.log(message);
```

Output:

```javascript id="s7"
Hello
ReferenceError
```

Because `message` exists only inside block.

---

## `const` is also block scoped

Example:

```javascript id="s8"
{
  const pi = 3.14;
  console.log(pi);
}

console.log(pi);
```

Outside block → Error.

---

## `var` is NOT block scoped

Important:

Example:

```javascript id="s9"
if (true) {
  var x = 100;
}

console.log(x);
```

Output:

```javascript id="s10"
100
```

`var` ignores block scope.

This is why modern code prefers:
✅ `let`
✅ `const`

instead of `var`.

---

# Scope Chain

Inner scope can access outer scope.

Example:

```javascript id="s11"
let country = "Bangladesh";

function outer() {
  let city = "Dhaka";

  function inner() {
    console.log(country);
    console.log(city);
  }

  inner();
}

outer();
```

Output:

```javascript id="s12"
Bangladesh
Dhaka
```

Inner function accesses outer variables.

This is called **Scope Chain**.

---

# Shadowing

Inner variable can replace outer variable name.

Example:

```javascript id="s13"
let name = "Global";

function test() {
  let name = "Local";
  console.log(name);
}

test();
console.log(name);
```

Output:

```javascript id="s14"
Local
Global
```

Inner variable shadows outer one.

---

# Summary

| Scope            | Accessible Where     |
| ---------------- | -------------------- |
| Global           | Everywhere           |
| Local / Function | Inside function only |
| Block            | Inside `{ }` only    |

Best practice:

* Use **const** by default
* Use **let** when value changes
* Avoid **var** in modern JavaScript

Understanding scope is essential before learning **closures** and **hoisting**.


# **Hoisting**
## Hoisting in JavaScript

**Hoisting** is a behavior where JavaScript moves **declarations** (not initializations) to the top of their scope before executing the code.

In simple words:

> You can use some variables/functions before writing them in code.

---

# 1) Function Hoisting

Function declarations are fully hoisted.

Example:

```javascript id="h1"
sayHello();

function sayHello() {
  console.log("Hello");
}
```

Output:

```javascript id="h2"
Hello
```

✔ Works because function is hoisted completely.

---

# 2) Variable Hoisting with `var`

Only the declaration is hoisted, not the value.

Example:

```javascript id="h3"
console.log(x);

var x = 10;
```

Internally JavaScript behaves like:

```javascript id="h4"
var x;
console.log(x);
x = 10;
```

Output:

```javascript id="h5"
undefined
```

So:

* Declaration → moved up
* Value → stays down

---

# 3) Hoisting with `let` and `const`

They are also hoisted, but **NOT initialized**.

This creates a **Temporal Dead Zone (TDZ)**.

Example:

```javascript id="h6"
console.log(a);

let a = 10;
```

Output:

```javascript id="h7"
ReferenceError
```

Same for `const`:

```javascript id="h8"
console.log(b);

const b = 20;
```

---

# What is Temporal Dead Zone (TDZ)?

It is the time between:

* variable creation (hoisting)
* and variable initialization

During this period → you cannot access it.

---

# 4) Function Expression Hoisting

Not fully hoisted.

Example:

```javascript id="h9"
greet();

var greet = function() {
  console.log("Hi");
};
```

Output:

```javascript id="h10"
TypeError: greet is not a function
```

Because:

```javascript id="h11"
var greet; // hoisted
greet();   // undefined()
greet = function() {}
```

---

# 5) Arrow Functions Hoisting

Same behavior as function expressions.

Example:

```javascript id="h12"
sayHi();

const sayHi = () => {
  console.log("Hi");
};
```

Output:

```javascript id="h13"
ReferenceError
```

---

# Summary Table

| Type                 | Hoisted? | Value Accessible Before Declaration? |
| -------------------- | -------- | ------------------------------------ |
| Function Declaration | ✅ Yes    | ✅ Yes                                |
| var                  | ✅ Yes    | ⚠️ undefined                         |
| let                  | ⚠️ Yes   | ❌ No (TDZ)                           |
| const                | ⚠️ Yes   | ❌ No (TDZ)                           |
| Function Expression  | ❌ No     | ❌ No                                 |
| Arrow Function       | ❌ No     | ❌ No                                 |

---

# Key Points to Remember

✔ Only **declarations are hoisted**, not values
✔ Functions are fully hoisted
✔ `var` gives `undefined`
✔ `let` and `const` cause TDZ error
✔ Best practice: declare variables before using them

---

Hoisting is one of the most important core concepts in JavaScript interviews and debugging.

# **Closures**
## Closures in JavaScript

A **closure** is when a function “remembers” variables from its outer scope even after the outer function has finished executing.

Simple meaning:

> A function + its lexical environment (surrounding variables) = Closure

---

# Basic Example

```javascript id="c1"
function outer() {
  let name = "Rahim";

  function inner() {
    console.log(name);
  }

  return inner;
}

const fn = outer();
fn();
```

### Output:

```javascript id="c2"
Rahim
```

### Why?

* `outer()` finishes execution
* But `inner()` still remembers `name`
* That memory is called a **closure**

---

# How Closure Works

Step-by-step:

1. `outer()` runs
2. `name = "Rahim"` is created
3. `inner()` is returned
4. `outer()` is gone from memory
5. `inner()` still accesses `name` → closure is formed

---

# Another Example (Counter)

```javascript id="c3"
function counter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const add = counter();

add();
add();
add();
```

### Output:

```javascript id="c4"
1
2
3
```

### Why it works?

* `count` is not lost
* Inner function keeps it alive
* That is closure in action

---

# Real-Life Example

Closures are used in:

* Data privacy
* Event handlers
* Callbacks
* SetTimeout / asynchronous code

Example:

```javascript id="c5"
function bankAccount() {
  let balance = 1000;

  return function withdraw(amount) {
    balance -= amount;
    console.log("Remaining:", balance);
  };
}

const withdrawMoney = bankAccount();

withdrawMoney(200);
withdrawMoney(300);
```

### Output:

```javascript id="c6"
Remaining: 800
Remaining: 500
```

---

# Data Privacy Using Closure

```javascript id="c7"
function secret() {
  let password = "1234";

  return function showPassword() {
    console.log(password);
  };
}

const access = secret();
access();
```

✔ `password` cannot be accessed directly from outside
✔ Only inner function can access it

This is **encapsulation using closure**

---

# Why Closures Are Important

Closures are used to:

* Maintain state without global variables
* Create private variables
* Build reusable functions
* Handle async operations

---

# Common Interview Definition

> A closure is a function that retains access to its outer scope even after the outer function has finished execution.

---

# Summary

| Concept        | Meaning                             |
| -------------- | ----------------------------------- |
| Outer Function | Creates variables                   |
| Inner Function | Uses outer variables                |
| Closure        | Memory of outer variables preserved |

---

✔ Closures = one of the most important concepts in JavaScript
✔ Used heavily in real-world applications and frameworks
✔ Core topic for interviews

If you want, I can next explain **Execution Context + Call Stack** (this connects directly with closures).

# **Callbacks**
## Callbacks in JavaScript

A **callback** is a function that is passed as an argument to another function and is executed later.

Simple meaning:

> “Call me back later when you are done.”

---

# Basic Example

```javascript id="cb1"
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

function sayBye() {
  console.log("Bye!");
}

greet("Rahim", sayBye);
```

### Output:

```javascript id="cb2"
Hello Rahim
Bye!
```

✔ `sayBye` is passed as a callback
✔ It runs after `greet` finishes

---

# How Callback Works

Step-by-step:

1. `greet()` is called
2. It prints `"Hello Rahim"`
3. Then it calls `callback()`
4. `sayBye()` executes

---

# Anonymous Callback Function

You don’t always need a named function.

```javascript id="cb3"
function greet(name, callback) {
  console.log("Hello " + name);
  callback();
}

greet("Karim", function () {
  console.log("Goodbye!");
});
```

### Output:

```javascript id="cb4"
Hello Karim
Goodbye!
```

---

# Real-Life Example (Asynchronous Behavior)

Callbacks are often used in **timers**:

```javascript id="cb5"
console.log("Start");

setTimeout(function () {
  console.log("This runs after 2 seconds");
}, 2000);

console.log("End");
```

### Output:

```javascript id="cb6"
Start
End
This runs after 2 seconds
```

✔ Callback runs later (not immediately)

---

# Why Callbacks Are Used

Callbacks help in:

* Handling asynchronous tasks
* API calls
* File reading
* Event handling
* Timers

---

# Example: Array Method Callback

```javascript id="cb7"
let numbers = [1, 2, 3];

numbers.forEach(function (num) {
  console.log(num * 2);
});
```

### Output:

```javascript id="cb8"
2
4
6
```

✔ Function passed into `forEach` is a callback

---

# Callback in Event Handling

```javascript id="cb9"
document.addEventListener("click", function () {
  console.log("Clicked!");
});
```

✔ Function runs when click event happens

---

# Callback Problem (Callback Hell)

When callbacks are nested too much:

```javascript id="cb10"
doTask1(function () {
  doTask2(function () {
    doTask3(function () {
      console.log("Done");
    });
  });
});
```

This becomes:
❌ Hard to read
❌ Hard to maintain

---

# Solution (Modern Approach)

Callbacks were later improved using:

* Promises
* Async / Await

---

# Summary

| Concept      | Meaning                               |
| ------------ | ------------------------------------- |
| Callback     | Function passed into another function |
| When it runs | After or during another function      |
| Use case     | Async tasks, events, timers           |
| Problem      | Callback hell (nested callbacks)      |

---

✔ Callbacks are a core concept in JavaScript
✔ They are the foundation of asynchronous programming
✔ Understanding them helps with Promises and Async/Await

If you want, next I can explain **Promises (very important upgrade of callbacks)**.

# **Objects**
## Objects in JavaScript

An **object** is a data structure that stores multiple related values using **key–value pairs**.

Simple meaning:

> Object = a collection of properties (and methods)

---

# Basic Object Example

```javascript id="o1"
let person = {
  name: "Rahim",
  age: 25,
  city: "Dhaka"
};

console.log(person);
```

### Output:

```javascript id="o2"
{ name: 'Rahim', age: 25, city: 'Dhaka' }
```

---

# Accessing Object Properties

## 1) Dot Notation

```javascript id="o3"
console.log(person.name);
```

Output:

```javascript id="o4"
Rahim
```

## 2) Bracket Notation

```javascript id="o5"
console.log(person["age"]);
```

Output:

```javascript id="o6"
25
```

Use bracket notation when:

* Key has spaces
* Key is dynamic

---

# Updating Object Values

```javascript id="o7"
person.age = 30;

console.log(person.age);
```

Output:

```javascript id="o8"
30
```

---

# Adding New Properties

```javascript id="o9"
person.country = "Bangladesh";

console.log(person);
```

Output:

```javascript id="o10"
{ name: 'Rahim', age: 30, city: 'Dhaka', country: 'Bangladesh' }
```

---

# Deleting Properties

```javascript id="o11"
delete person.city;

console.log(person);
```

Output:

```javascript id="o12"
{ name: 'Rahim', age: 30, country: 'Bangladesh' }
```

---

# Objects with Functions (Methods)

Objects can also store functions (called methods).

```javascript id="o13"
let person = {
  name: "Karim",
  greet: function () {
    console.log("Hello!");
  }
};

person.greet();
```

Output:

```javascript id="o14"
Hello!
```

---

# `this` Keyword in Objects

`this` refers to the current object.

```javascript id="o15"
let person = {
  name: "Rahim",
  greet: function () {
    console.log("Hello " + this.name);
  }
};

person.greet();
```

Output:

```javascript id="o16"
Hello Rahim
```

---

# Nested Objects

Objects inside objects.

```javascript id="o17"
let user = {
  name: "Rahim",
  address: {
    city: "Dhaka",
    country: "Bangladesh"
  }
};

console.log(user.address.city);
```

Output:

```javascript id="o18"
Dhaka
```

---

# Looping Through Objects

## for...in loop

```javascript id="o19"
let person = {
  name: "Rahim",
  age: 25
};

for (let key in person) {
  console.log(key + ":", person[key]);
}
```

Output:

```javascript id="o20"
name: Rahim
age: 25
```

---

# Object Methods

## 1) Object.keys()

```javascript id="o21"
console.log(Object.keys(person));
```

Output:

```javascript id="o22"
["name", "age"]
```

## 2) Object.values()

```javascript id="o23"
console.log(Object.values(person));
```

Output:

```javascript id="o24"
["Rahim", 25]
```

## 3) Object.entries()

```javascript id="o25"
console.log(Object.entries(person));
```

Output:

```javascript id="o26"
[["name","Rahim"], ["age",25]]
```

---

# Object vs Primitive

| Feature | Object           | Primitive    |
| ------- | ---------------- | ------------ |
| Stores  | Multiple values  | Single value |
| Type    | Reference type   | Value type   |
| Example | `{name:"Rahim"}` | `"Rahim"`    |

---

# Summary

✔ Objects store data in key–value pairs
✔ Used to represent real-world things
✔ Can contain properties + methods
✔ Can be nested
✔ Can be looped using `for...in`

---

# Real-Life Example

```javascript id="o27"
let car = {
  brand: "Toyota",
  model: "Corolla",
  start: function () {
    console.log("Car started");
  }
};

car.start();
```

Objects are one of the most important concepts in JavaScript and are heavily used in frameworks, APIs, and real applications.

# **Arrays & Array Methods**
## Arrays & Array Methods in JavaScript

An **array** is a special variable that stores multiple values in a single place.

Simple meaning:

> Array = ordered list of items

---

# 1) Creating an Array

```javascript id="ar1"
let fruits = ["Apple", "Banana", "Mango"];
console.log(fruits);
```

Output:

```javascript id="ar2"
["Apple", "Banana", "Mango"]
```

---

# 2) Accessing Array Elements

Array index starts from **0**

```javascript id="ar3"
let fruits = ["Apple", "Banana", "Mango"];

console.log(fruits[0]); // Apple
console.log(fruits[1]); // Banana
console.log(fruits[2]); // Mango
```

---

# 3) Changing Values

```javascript id="ar4"
let fruits = ["Apple", "Banana", "Mango"];

fruits[1] = "Orange";

console.log(fruits);
```

Output:

```javascript id="ar5"
["Apple", "Orange", "Mango"]
```

---

# 4) Array Methods

## ➤ push()

Adds item at the end.

```javascript id="ar6"
let fruits = ["Apple", "Banana"];

fruits.push("Mango");

console.log(fruits);
```

Output:

```javascript id="ar7"
["Apple", "Banana", "Mango"]
```

---

## ➤ pop()

Removes last item.

```javascript id="ar8"
let fruits = ["Apple", "Banana", "Mango"];

fruits.pop();

console.log(fruits);
```

Output:

```javascript id="ar9"
["Apple", "Banana"]
```

---

## ➤ shift()

Removes first item.

```javascript id="ar10"
let fruits = ["Apple", "Banana", "Mango"];

fruits.shift();

console.log(fruits);
```

Output:

```javascript id="ar11"
["Banana", "Mango"]
```

---

## ➤ unshift()

Adds item at the beginning.

```javascript id="ar12"
let fruits = ["Banana", "Mango"];

fruits.unshift("Apple");

console.log(fruits);
```

Output:

```javascript id="ar13"
["Apple", "Banana", "Mango"]
```

---

## ➤ length

Gets number of elements.

```javascript id="ar14"
let fruits = ["Apple", "Banana", "Mango"];

console.log(fruits.length);
```

Output:

```javascript id="ar15"
3
```

---

## ➤ includes()

Checks if item exists.

```javascript id="ar16"
let fruits = ["Apple", "Banana"];

console.log(fruits.includes("Apple"));
```

Output:

```javascript id="ar17"
true
```

---

## ➤ indexOf()

Finds index of item.

```javascript id="ar18"
let fruits = ["Apple", "Banana", "Mango"];

console.log(fruits.indexOf("Mango"));
```

Output:

```javascript id="ar19"
2
```

---

## ➤ slice()

Returns a part of array (does NOT change original).

```javascript id="ar20"
let fruits = ["Apple", "Banana", "Mango", "Orange"];

let newFruits = fruits.slice(1, 3);

console.log(newFruits);
```

Output:

```javascript id="ar21"
["Banana", "Mango"]
```

---

## ➤ splice()

Removes or adds elements (changes original array).

### Remove:

```javascript id="ar22"
let fruits = ["Apple", "Banana", "Mango"];

fruits.splice(1, 1);

console.log(fruits);
```

Output:

```javascript id="ar23"
["Apple", "Mango"]
```

---

### Add:

```javascript id="ar24"
let fruits = ["Apple", "Mango"];

fruits.splice(1, 0, "Banana");

console.log(fruits);
```

Output:

```javascript id="ar25"
["Apple", "Banana", "Mango"]
```

---

## ➤ forEach()

Runs function for each element.

```javascript id="ar26"
let fruits = ["Apple", "Banana", "Mango"];

fruits.forEach(function (fruit) {
  console.log(fruit);
});
```

Output:

```javascript id="ar27"
Apple
Banana
Mango
```

---

## ➤ map()

Creates new array by modifying elements.

```javascript id="ar28"
let numbers = [1, 2, 3];

let doubled = numbers.map(n => n * 2);

console.log(doubled);
```

Output:

```javascript id="ar29"
[2, 4, 6]
```

---

## ➤ filter()

Returns elements that match condition.

```javascript id="ar30"
let numbers = [1, 2, 3, 4, 5];

let even = numbers.filter(n => n % 2 === 0);

console.log(even);
```

Output:

```javascript id="ar31"
[2, 4]
```

---

## ➤ reduce()

Reduces array to single value.

```javascript id="ar32"
let numbers = [1, 2, 3, 4];

let sum = numbers.reduce((a, b) => a + b);

console.log(sum);
```

Output:

```javascript id="ar33"
10
```

---

# Summary

| Method    | Purpose          |
| --------- | ---------------- |
| push()    | Add at end       |
| pop()     | Remove last      |
| shift()   | Remove first     |
| unshift() | Add first        |
| slice()   | Copy part        |
| splice()  | Add/remove items |
| map()     | Transform array  |
| filter()  | Select items     |
| reduce()  | Combine values   |

---

✔ Arrays are used to store lists
✔ Array methods help manipulate data easily
✔ Very important for real-world JavaScript apps

If you want next, I can explain **DOM Manipulation (most important for frontend)**.
#  **Strings & String Methods

## Strings & String Methods in JavaScript

A **string** is a sequence of characters used to represent text.

Example:

```javascript id="st1"
let name = "Rahim";
let message = 'Hello World';
```

Both `" "` and `' '` are valid.

---

# 1) String Indexing

Strings work like arrays (index starts from 0)

```javascript id="st2"
let text = "JavaScript";

console.log(text[0]); // J
console.log(text[4]); // S
```

---

# 2) String Length

Find number of characters.

```javascript id="st3"
let text = "Hello";

console.log(text.length);
```

Output:

```javascript id="st4"
5
```

---

# 3) toUpperCase()

Converts text to uppercase.

```javascript id="st5"
let name = "rahim";

console.log(name.toUpperCase());
```

Output:

```javascript id="st6"
RAHIM
```

---

# 4) toLowerCase()

Converts text to lowercase.

```javascript id="st7"
let name = "RAHIM";

console.log(name.toLowerCase());
```

Output:

```javascript id="st8"
rahim
```

---

# 5) trim()

Removes extra spaces.

```javascript id="st9"
let text = "   Hello   ";

console.log(text.trim());
```

Output:

```javascript id="st10"
Hello
```

---

# 6) includes()

Checks if text exists.

```javascript id="st11"
let text = "I love JavaScript";

console.log(text.includes("JavaScript"));
```

Output:

```javascript id="st12"
true
```

---

# 7) indexOf()

Finds position of text.

```javascript id="st13"
let text = "I love JS";

console.log(text.indexOf("JS"));
```

Output:

```javascript id="st14"
7
```

---

# 8) slice()

Extracts part of string.

```javascript id="st15"
let text = "JavaScript";

console.log(text.slice(0, 4));
```

Output:

```javascript id="st16"
Java
```

---

# 9) substring()

Similar to slice (no negative index support).

```javascript id="st17"
let text = "JavaScript";

console.log(text.substring(4, 10));
```

Output:

```javascript id="st18"
Script
```

---

# 10) replace()

Replaces text.

```javascript id="st19"
let text = "I love Python";

console.log(text.replace("Python", "JavaScript"));
```

Output:

```javascript id="st20"
I love JavaScript
```

---

# 11) replaceAll()

Replaces all matches.

```javascript id="st21"
let text = "JS JS JS";

console.log(text.replaceAll("JS", "JavaScript"));
```

Output:

```javascript id="st22"
JavaScript JavaScript JavaScript
```

---

# 12) concat()

Joins strings.

```javascript id="st23"
let a = "Hello";
let b = "World";

console.log(a.concat(" ", b));
```

Output:

```javascript id="st24"
Hello World
```

---

# 13) charAt()

Returns character at index.

```javascript id="st25"
let text = "JavaScript";

console.log(text.charAt(1));
```

Output:

```javascript id="st26"
a
```

---

# 14) split()

Converts string into array.

```javascript id="st27"
let text = "a,b,c";

console.log(text.split(","));
```

Output:

```javascript id="st28"
["a", "b", "c"]
```

---

# 15) Template Literals (Modern Strings)

Uses backticks `` ` `` and supports variables.

```javascript id="st29"
let name = "Rahim";
let age = 25;

let msg = `My name is ${name} and I am ${age} years old`;

console.log(msg);
```

Output:

```javascript id="st30"
My name is Rahim and I am 25 years old
```

---

# Summary Table

| Method        | Purpose          |
| ------------- | ---------------- |
| length        | Get size         |
| toUpperCase() | Uppercase        |
| toLowerCase() | Lowercase        |
| trim()        | Remove spaces    |
| includes()    | Check text       |
| indexOf()     | Find position    |
| slice()       | Extract part     |
| replace()     | Replace text     |
| split()       | Convert to array |
| concat()      | Join strings     |

---

✔ Strings are used everywhere in JavaScript
✔ String methods help manipulate text easily
✔ Very important for real-world apps (forms, APIs, UI text)

If you want next, I can explain **DOM Manipulation (very important for frontend development)**.

# **Date & Math Objects**
## Date & Math Objects in JavaScript

JavaScript provides built-in objects to work with **time, dates, and mathematical operations**:

* `Date` → handles dates and time
* `Math` → handles mathematical operations

---

# 1) Date Object

The **Date object** is used to work with dates and time.

---

## Create a Date

```javascript id="d1"
let now = new Date();
console.log(now);
```

Output (example):

```javascript id="d2"
2026-05-07T...
```

---

## Get Date Values

```javascript id="d3"
let date = new Date();

console.log(date.getFullYear());  // Year
console.log(date.getMonth());     // Month (0–11)
console.log(date.getDate());      // Day
console.log(date.getDay());       // Weekday (0–6)
```

### Example Output:

```javascript id="d4"
2026
4
7
4
```

📌 Note:

* Months start from **0 (January)**
* Days start from **0 (Sunday)**

---

## Get Time Values

```javascript id="d5"
let time = new Date();

console.log(time.getHours());
console.log(time.getMinutes());
console.log(time.getSeconds());
```

---

## Set Date Values

```javascript id="d6"
let date = new Date();

date.setFullYear(2030);
console.log(date);
```

---

## Custom Date

```javascript id="d7"
let customDate = new Date("2025-12-25");

console.log(customDate);
```

---

# 2) Math Object

The **Math object** is used for mathematical calculations.

---

## Math.PI

Value of π (pi)

```javascript id="m1"
console.log(Math.PI);
```

Output:

```javascript id="m2"
3.141592653589793
```

---

## Math.round()

Rounds to nearest integer

```javascript id="m3"
console.log(Math.round(4.6));
console.log(Math.round(4.3));
```

Output:

```javascript id="m4"
5
4
```

---

## Math.floor()

Always rounds down

```javascript id="m5"
console.log(Math.floor(4.9));
```

Output:

```javascript id="m6"
4
```

---

## Math.ceil()

Always rounds up

```javascript id="m7"
console.log(Math.ceil(4.1));
```

Output:

```javascript id="m8"
5
```

---

## Math.sqrt()

Square root

```javascript id="m9"
console.log(Math.sqrt(16));
```

Output:

```javascript id="m10"
4
```

---

## Math.pow()

Power (exponent)

```javascript id="m11"
console.log(Math.pow(2, 3));
```

Output:

```javascript id="m12"
8
```

---

## Math.abs()

Absolute value (removes negative sign)

```javascript id="m13"
console.log(Math.abs(-10));
```

Output:

```javascript id="m14"
10
```

---

## Math.min() & Math.max()

```javascript id="m15"
console.log(Math.min(2, 5, 1));
console.log(Math.max(2, 5, 1));
```

Output:

```javascript id="m16"
1
5
```

---

## Math.random()

Generates random number (0 to 1)

```javascript id="m17"
console.log(Math.random());
```

Example Output:

```javascript id="m18"
0.7342
```

### Random integer (1–10):

```javascript id="m19"
let random = Math.floor(Math.random() * 10) + 1;

console.log(random);
```

---

# Summary

## Date Object:

| Method        | Use   |
| ------------- | ----- |
| getFullYear() | Year  |
| getMonth()    | Month |
| getDate()     | Day   |
| getHours()    | Hours |

## Math Object:

| Method        | Use           |
| ------------- | ------------- |
| Math.round()  | Round number  |
| Math.floor()  | Round down    |
| Math.ceil()   | Round up      |
| Math.sqrt()   | Square root   |
| Math.pow()    | Power         |
| Math.random() | Random number |

---

✔ Date = time & calendar operations
✔ Math = calculations & numbers
✔ Both are heavily used in real-world JavaScript apps

If you want next, I can explain **DOM Manipulation (most important for frontend development)**.


# **DOM Manipulation**

## DOM Manipulation in JavaScript

**DOM (Document Object Model)** is a way JavaScript interacts with HTML pages.

Simple meaning:

> DOM = JavaScript’s bridge to access and change webpage content

---

# 1) What is DOM?

When a webpage loads, the browser creates a tree-like structure:

* HTML becomes a **DOM tree**
* Each element becomes a **node**
* JavaScript can read and modify these nodes

---

# 2) Selecting Elements

To change something, first you must select it.

## ➤ getElementById

```javascript id="d1"
let title = document.getElementById("heading");
console.log(title);
```

---

## ➤ getElementsByClassName

```javascript id="d2"
let items = document.getElementsByClassName("item");
console.log(items);
```

---

## ➤ getElementsByTagName

```javascript id="d3"
let paragraphs = document.getElementsByTagName("p");
console.log(paragraphs);
```

---

## ➤ querySelector (most used)

Selects first match.

```javascript id="d4"
let element = document.querySelector(".box");
```

---

## ➤ querySelectorAll

Selects all matches.

```javascript id="d5"
let elements = document.querySelectorAll(".box");
console.log(elements);
```

---

# 3) Changing Content

## ➤ innerText

Changes visible text.

```javascript id="d6"
document.getElementById("heading").innerText = "Hello JS";
```

---

## ➤ innerHTML

Changes HTML content.

```javascript id="d7"
document.getElementById("box").innerHTML = "<h2>New Content</h2>";
```

---

# 4) Changing Styles

```javascript id="d8"
let box = document.getElementById("box");

box.style.color = "red";
box.style.backgroundColor = "yellow";
box.style.fontSize = "20px";
```

---

# 5) Adding & Removing Classes

## Add class

```javascript id="d9"
document.getElementById("box").classList.add("active");
```

## Remove class

```javascript id="d10"
document.getElementById("box").classList.remove("active");
```

## Toggle class

```javascript id="d11"
document.getElementById("box").classList.toggle("active");
```

---

# 6) Creating Elements

```javascript id="d12"
let newDiv = document.createElement("div");
newDiv.innerText = "Hello World";

document.body.appendChild(newDiv);
```

---

# 7) Removing Elements

```javascript id="d13"
let element = document.getElementById("box");

element.remove();
```

---

# 8) Event Handling

Events = user actions (click, input, etc.)

## Click Event

```javascript id="d14"
document.getElementById("btn").addEventListener("click", function() {
  console.log("Button clicked!");
});
```

---

## Mouse Events

```javascript id="d15"
element.addEventListener("mouseover", function() {
  console.log("Mouse over!");
});
```

---

## Input Event

```javascript id="d16"
document.getElementById("input").addEventListener("input", function(e) {
  console.log(e.target.value);
});
```

---

# 9) DOM Traversing

## Parent element

```javascript id="d17"
element.parentElement
```

## Children

```javascript id="d18"
element.children
```

## Next sibling

```javascript id="d19"
element.nextElementSibling
```

## Previous sibling

```javascript id="d20"
element.previousElementSibling
```

---

# Example Mini Project

```javascript id="d21"
let btn = document.getElementById("btn");
let text = document.getElementById("text");

btn.addEventListener("click", function() {
  text.innerText = "Button Clicked!";
  text.style.color = "green";
});
```

---

# Summary

| Feature          | Purpose         |
| ---------------- | --------------- |
| Selectors        | Get elements    |
| innerText        | Change text     |
| innerHTML        | Change HTML     |
| style            | Change CSS      |
| classList        | Manage classes  |
| createElement    | Create elements |
| remove           | Delete elements |
| addEventListener | Handle events   |

---

✔ DOM = connects JavaScript with HTML
✔ Used to build interactive websites
✔ Core skill for frontend development

If you want next, I can explain **Events in depth or Mini Projects (like calculator, to-do app)**.



# **Events & Event Handling**

## Events & Event Handling in JavaScript

**Events** are actions that happen in the browser, and **event handling** is the way JavaScript responds to those actions.

Simple meaning:

> Event = Something happens (click, type, scroll)
> Event Handler = Code that reacts to it

---

# 1) What is an Event?

Common events:

* Click
* Mouse over
* Key press
* Input change
* Page load

Example:
👉 Clicking a button = event

---

# 2) Event Handling with `addEventListener`

This is the most common way to handle events.

```javascript id="e1"
document.getElementById("btn").addEventListener("click", function () {
  console.log("Button clicked!");
});
```

✔ When button is clicked → function runs

---

# 3) Click Event

```javascript id="e2"
let button = document.getElementById("btn");

button.addEventListener("click", function () {
  alert("You clicked me!");
});
```

---

# 4) Mouse Events

## mouseover

```javascript id="e3"
let box = document.getElementById("box");

box.addEventListener("mouseover", function () {
  console.log("Mouse is over the box");
});
```

## mouseout

```javascript id="e4"
box.addEventListener("mouseout", function () {
  console.log("Mouse left the box");
});
```

---

# 5) Keyboard Events

## keydown

```javascript id="e5"
document.addEventListener("keydown", function (event) {
  console.log("Key pressed: " + event.key);
});
```

---

## keyup

```javascript id="e6"
document.addEventListener("keyup", function (event) {
  console.log("Key released: " + event.key);
});
```

---

# 6) Input Event

Used for text fields.

```javascript id="e7"
let input = document.getElementById("input");

input.addEventListener("input", function (event) {
  console.log(event.target.value);
});
```

✔ Runs every time user types

---

# 7) Change Event

Runs when value is changed and focus is lost.

```javascript id="e8"
let select = document.getElementById("select");

select.addEventListener("change", function () {
  console.log("Value changed");
});
```

---

# 8) Event Object

Every event gives an **event object**.

```javascript id="e9"
document.getElementById("btn").addEventListener("click", function (event) {
  console.log(event);
});
```

Important properties:

* `event.target` → element that triggered event
* `event.type` → event name
* `event.key` → key pressed

---

# 9) Prevent Default Behavior

Stops default browser action.

Example: stop form submission

```javascript id="e10"
document.getElementById("form").addEventListener("submit", function (e) {
  e.preventDefault();
  console.log("Form submitted blocked");
});
```

---

# 10) Stop Event Bubbling

Stops event from going to parent elements.

```javascript id="e11"
element.addEventListener("click", function (e) {
  e.stopPropagation();
});
```

---

# 11) Inline Event Handling (Not Recommended)

```html id="e12"
<button onclick="alert('Clicked!')">Click</button>
```

❌ Not recommended in modern JavaScript
✔ Use `addEventListener` instead

---

# 12) Event Bubbling (Important Concept)

Event moves from child → parent.

Example:

* Button inside div
* Click button → div also gets event

---

# Summary

| Event Type | Example         |
| ---------- | --------------- |
| click      | Button click    |
| mouseover  | Hover effect    |
| keydown    | Keyboard press  |
| input      | Typing in field |
| change     | Select dropdown |

---

# Key Takeaways

✔ Events = user actions
✔ Event handling = responding to actions
✔ `addEventListener` is best practice
✔ Event object gives useful info
✔ Used everywhere in real web apps

---

If you want next, I can teach you **DOM Mini Projects (To-Do App / Calculator / Form Validation)** to practice everything together.

# **ES6 Features** (Template literals, Destructuring, Spread/Rest, Modules)

## ES6 Features in JavaScript

**ES6 (ECMAScript 2015)** introduced modern features that make JavaScript cleaner, shorter, and more powerful.

We’ll cover:

1. Template Literals
2. Destructuring
3. Spread / Rest Operators
4. Modules

---

# 1) Template Literals

Template literals use **backticks (`` ` ``)** instead of quotes.

They allow:

* Multi-line strings
* Variable embedding

### Example:

```javascript id="es1"
let name = "Rahim";
let age = 25;

let message = `My name is ${name} and I am ${age} years old`;

console.log(message);
```

### Output:

```
My name is Rahim and I am 25 years old
```

✔ Cleaner than string concatenation

---

# 2) Destructuring

Destructuring allows you to **extract values easily** from arrays or objects.

---

## Array Destructuring

```javascript id="es2"
let fruits = ["Apple", "Banana", "Mango"];

let [a, b, c] = fruits;

console.log(a);
console.log(b);
console.log(c);
```

### Output:

```
Apple
Banana
Mango
```

---

## Object Destructuring

```javascript id="es3"
let person = {
  name: "Rahim",
  age: 25,
  city: "Dhaka"
};

let { name, age, city } = person;

console.log(name);
console.log(age);
console.log(city);
```

### Output:

```
Rahim
25
Dhaka
```

---

# 3) Spread Operator (`...`)

Used to **expand** elements.

---

## Copy array

```javascript id="es4"
let arr1 = [1, 2, 3];
let arr2 = [...arr1];

console.log(arr2);
```

### Output:

```
[1, 2, 3]
```

---

## Merge arrays

```javascript id="es5"
let a = [1, 2];
let b = [3, 4];

let result = [...a, ...b];

console.log(result);
```

### Output:

```
[1, 2, 3, 4]
```

---

## Spread in objects

```javascript id="es6"
let user = { name: "Rahim" };
let updatedUser = { ...user, age: 25 };

console.log(updatedUser);
```

---

# 4) Rest Operator (`...`)

Used to **collect multiple values into one array**.

```javascript id="es7"
function sum(...numbers) {
  let total = 0;

  for (let num of numbers) {
    total += num;
  }

  return total;
}

console.log(sum(1, 2, 3, 4));
```

### Output:

```
10
```

✔ Rest gathers values
✔ Spread expands values

---

# 5) Modules (Import / Export)

Modules help you split code into multiple files.

---

## Export

```javascript id="es8"
// file: math.js

export function add(a, b) {
  return a + b;
}
```

---

## Import

```javascript id="es9"
// file: main.js

import { add } from "./math.js";

console.log(add(5, 3));
```

### Output:

```
8
```

---

## Default Export

```javascript id="es10"
// file: greet.js

export default function greet() {
  console.log("Hello!");
}
```

```javascript id="es11"
import greet from "./greet.js";

greet();
```

---

# Summary Table

| Feature           | Purpose                |
| ----------------- | ---------------------- |
| Template Literals | Easy string formatting |
| Destructuring     | Extract values quickly |
| Spread (`...`)    | Expand values          |
| Rest (`...`)      | Collect values         |
| Modules           | Organize code files    |

---

# Key Takeaways

✔ ES6 makes JavaScript modern and cleaner
✔ Template literals improve strings
✔ Destructuring simplifies data access
✔ Spread/Rest are powerful for arrays & functions
✔ Modules help organize large projects

---

If you want next, I can teach **Promises + Async/Await (very important for real-world JavaScript & API calls)**.


# **Promises**

## Promises in JavaScript

A **Promise** is an object used to handle **asynchronous operations** (tasks that take time), like:

* API calls
* Database requests
* File loading
* Timers

Simple meaning:

> A Promise is a *promise that something will happen in the future*.

---

# 1) Promise States

A Promise has 3 states:

1. **Pending** → initial state (waiting)
2. **Fulfilled** → success
3. **Rejected** → error/failure

---

# 2) Creating a Promise

```javascript id="p1"
let promise = new Promise(function(resolve, reject) {
  let success = true;

  if (success) {
    resolve("Task completed");
  } else {
    reject("Task failed");
  }
});
```

---

# 3) Handling a Promise

## ➤ `.then()` for success

## ➤ `.catch()` for error

```javascript id="p2"
promise
  .then(function(result) {
    console.log(result);
  })
  .catch(function(error) {
    console.log(error);
  });
```

### Output (if success):

```
Task completed
```

---

# 4) Real Example with Delay

```javascript id="p3"
let promise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve("Data loaded successfully");
  }, 2000);
});

promise.then(function(result) {
  console.log(result);
});
```

### Output (after 2 seconds):

```
Data loaded successfully
```

---

# 5) Promise with Error Handling

```javascript id="p4"
let promise = new Promise(function(resolve, reject) {
  let error = true;

  if (!error) {
    resolve("Success");
  } else {
    reject("Something went wrong");
  }
});

promise
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

---

# 6) Promise Chaining

You can run multiple steps one after another.

```javascript id="p5"
let promise = new Promise(resolve => {
  resolve(2);
});

promise
  .then(num => {
    console.log(num);
    return num * 2;
  })
  .then(num => {
    console.log(num);
    return num * 2;
  })
  .then(num => {
    console.log(num);
  });
```

### Output:

```
2
4
8
```

---

# 7) Promise vs Callback

| Feature        | Callback               | Promise        |
| -------------- | ---------------------- | -------------- |
| Readability    | Low                    | High           |
| Structure      | Nested (callback hell) | Clean chaining |
| Error handling | Hard                   | Easy (.catch)  |

---

# 8) Real-world Example (Fake API)

```javascript id="p6"
function fetchData() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve("User data received");
    }, 1500);
  });
}

fetchData().then(data => {
  console.log(data);
});
```

---

# 9) Promise States Visualization

```
Pending → Fulfilled (then)
        → Rejected (catch)
```

---

# 10) Key Takeaways

✔ Promises handle async operations
✔ Prevent callback hell
✔ Have 3 states: pending, fulfilled, rejected
✔ Use `.then()` and `.catch()`
✔ Can be chained

---

# Next Step (Important)

If you understand Promises, the next topic is:

👉 **Async / Await** (modern and easiest way to handle Promises)

It makes async code look like normal synchronous code.

# **Async / Await**

## Async / Await in JavaScript

**Async / Await** is a modern way to handle asynchronous code (like Promises) in a simpler, cleaner style.

Simple meaning:

> It lets you write async code like normal (synchronous) code.

It is built on top of **Promises**.

---

# 1) `async` Function

When you add `async`, the function always returns a **Promise**.

```javascript id="a1"
async function hello() {
  return "Hello World";
}

hello().then(result => console.log(result));
```

### Output:

```
Hello World
```

✔ Even though we return a string, it becomes a Promise automatically.

---

# 2) `await` Keyword

`await` pauses execution until a Promise is resolved.

It only works inside an `async` function.

---

## Example:

```javascript id="a2"
function getData() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve("Data received");
    }, 2000);
  });
}

async function showData() {
  let result = await getData();
  console.log(result);
}

showData();
```

### Output (after 2 seconds):

```
Data received
```

---

# 3) Without Async/Await (Promise way)

```javascript id="a3"
getData().then(result => {
  console.log(result);
});
```

✔ Works, but can become messy in complex code

---

# 4) Async/Await vs Promises

| Feature        | Promises   | Async/Await   |
| -------------- | ---------- | ------------- |
| Readability    | Medium     | High          |
| Code style     | Chaining   | Sequential    |
| Error handling | `.catch()` | `try...catch` |

---

# 5) Error Handling with Try/Catch

```javascript id="a4"
async function fetchData() {
  try {
    let response = await fakeAPI();
    console.log(response);
  } catch (error) {
    console.log("Error:", error);
  }
}
```

✔ Clean way to handle errors

---

# 6) Real Example (Simulated API)

```javascript id="a5"
function fakeAPI() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve("User data loaded");
    }, 1500);
  });
}

async function loadUser() {
  console.log("Loading...");

  let data = await fakeAPI();

  console.log(data);
  console.log("Done");
}

loadUser();
```

### Output:

```
Loading...
User data loaded
Done
```

---

# 7) Multiple Await Calls

```javascript id="a6"
function step1() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Step 1 done"), 1000);
  });
}

function step2() {
  return new Promise(resolve => {
    setTimeout(() => resolve("Step 2 done"), 1000);
  });
}

async function runSteps() {
  let a = await step1();
  console.log(a);

  let b = await step2();
  console.log(b);
}

runSteps();
```

---

# 8) Parallel Execution (Better Performance)

If tasks are independent:

```javascript id="a7"
async function run() {
  let [a, b] = await Promise.all([step1(), step2()]);

  console.log(a);
  console.log(b);
}

run();
```

✔ Faster because both run together

---

# 9) Key Rules

✔ `async` makes a function return a Promise
✔ `await` pauses execution until Promise resolves
✔ `await` only works inside `async` functions
✔ Use `try...catch` for errors

---

# 10) Why Async/Await is Important

* Makes code easier to read
* Avoids callback hell
* Cleaner than `.then()` chains
* Used in real-world APIs (fetch, database, servers)

---

# Final Summary

👉 Promises = foundation of async JS
👉 Async/Await = cleaner way to use Promises

---

If you want next, I can teach:
👉 **Fetch API (real-world API calling in JavaScript)**


# **Error Handling** (`try...catch`)

## Error Handling in JavaScript (`try...catch`)

**Error handling** is used to manage unexpected problems in code so the program doesn’t crash.

Simple meaning:

> “Try to run code, and if something goes wrong, catch the error and handle it.”

---

# 1) Basic `try...catch`

```javascript id="e1"
try {
  console.log("Start");

  let x = y + 10; // Error (y is not defined)

  console.log("End");
} catch (error) {
  console.log("Something went wrong");
}
```

### Output:

```javascript id="e2"
Start
Something went wrong
```

✔ Code inside `try` runs first
✔ If error happens → `catch` runs

---

# 2) Understanding How It Works

Flow:

1. JavaScript runs `try`
2. If no error → skip `catch`
3. If error → jump to `catch`

---

# 3) Getting Error Details

You can see the actual error:

```javascript id="e3"
try {
  let result = undefinedVariable + 5;
} catch (error) {
  console.log(error.name);
  console.log(error.message);
}
```

### Output:

```javascript id="e4"
ReferenceError
undefinedVariable is not defined
```

---

# 4) `finally` Block

`finally` always runs (error or not).

```javascript id="e5"
try {
  console.log("Trying...");
} catch (error) {
  console.log("Error occurred");
} finally {
  console.log("Always runs");
}
```

### Output:

```javascript id="e6"
Trying...
Always runs
```

---

# 5) Example: Safe Division

```javascript id="e7"
function divide(a, b) {
  try {
    if (b === 0) {
      throw new Error("Cannot divide by zero");
    }

    console.log(a / b);
  } catch (error) {
    console.log("Error:", error.message);
  }
}

divide(10, 2);
divide(10, 0);
```

### Output:

```javascript id="e8"
5
Error: Cannot divide by zero
```

---

# 6) Using `throw`

You can create custom errors.

```javascript id="e9"
throw new Error("Custom error message");
```

---

# 7) Error Types in JavaScript

Common errors:

| Type           | Meaning            |
| -------------- | ------------------ |
| ReferenceError | Variable not found |
| TypeError      | Wrong type usage   |
| SyntaxError    | Wrong syntax       |

---

# 8) Real-World Example (User Input)

```javascript id="e10"
function checkAge(age) {
  try {
    if (age < 0) {
      throw new Error("Age cannot be negative");
    }

    console.log("Valid age:", age);
  } catch (error) {
    console.log("Error:", error.message);
  }
}

checkAge(25);
checkAge(-5);
```

### Output:

```javascript id="e11"
Valid age: 25
Error: Age cannot be negative
```

---

# 9) Error Handling with Async Code

```javascript id="e12"
async function fetchData() {
  try {
    let data = await fakeAPI();
    console.log(data);
  } catch (error) {
    console.log("Failed:", error);
  }
}
```

✔ Very important in real API calls

---

# Summary

| Block   | Purpose             |
| ------- | ------------------- |
| try     | Code that may fail  |
| catch   | Handles error       |
| finally | Always runs         |
| throw   | Create custom error |

---

# Key Takeaways

✔ Prevents program crashes
✔ Helps debug code easily
✔ Essential for APIs and async operations
✔ Used everywhere in real applications

---

If you want next, I can teach:
👉 **Execution Context & Call Stack (very important for interviews and understanding how JS really works)**

# **Classes & OOP**

## Classes & OOP in JavaScript

**OOP (Object-Oriented Programming)** is a programming style based on **objects**. It helps you organize code into reusable structures.

Simple meaning:

> OOP = writing code using “real-world objects”

Example: Car, Person, Bank Account

---

# 1) Class

A **class** is a blueprint for creating objects.

```javascript id="c1"
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}
```

✔ `class` defines structure
✔ `constructor` initializes values

---

# 2) Creating Objects from Class

```javascript id="c2"
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

let p1 = new Person("Rahim", 25);
let p2 = new Person("Karim", 30);

console.log(p1);
console.log(p2);
```

### Output:

```javascript id="c3"
Person { name: 'Rahim', age: 25 }
Person { name: 'Karim', age: 30 }
```

---

# 3) Methods in Class

You can add functions inside a class.

```javascript id="c4"
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hello " + this.name);
  }
}

let user = new Person("Rahim");
user.greet();
```

### Output:

```javascript id="c5"
Hello Rahim
```

---

# 4) OOP Principles

## 1. Encapsulation

> Keeping data and methods inside a class

```javascript id="c6"
class BankAccount {
  constructor(balance) {
    this.balance = balance;
  }

  showBalance() {
    console.log(this.balance);
  }
}
```

---

## 2. Inheritance

> One class inherits another class

```javascript id="c7"
class Animal {
  speak() {
    console.log("Animal sound");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Woof!");
  }
}

let d = new Dog();
d.speak();
d.bark();
```

### Output:

```javascript id="c8"
Animal sound
Woof!
```

---

## 3. Polymorphism

> Same method, different behavior

```javascript id="c9"
class Animal {
  sound() {
    console.log("Some sound");
  }
}

class Cat extends Animal {
  sound() {
    console.log("Meow");
  }
}

class Dog extends Animal {
  sound() {
    console.log("Bark");
  }
}

let a = new Cat();
let b = new Dog();

a.sound();
b.sound();
```

### Output:

```javascript id="c10"
Meow
Bark
```

---

## 4. Abstraction

> Hide complex details, show only essential features

```javascript id="c11"
class Car {
  start() {
    this._engineStart();
    console.log("Car started");
  }

  _engineStart() {
    console.log("Engine running...");
  }
}

let myCar = new Car();
myCar.start();
```

---

# 5) `this` Keyword in Classes

`this` refers to current object.

```javascript id="c12"
class User {
  constructor(name) {
    this.name = name;
  }

  show() {
    console.log(this.name);
  }
}

let u = new User("Rahim");
u.show();
```

---

# 6) Getters & Setters

Used to control access to properties.

```javascript id="c13"
class Person {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  set name(value) {
    this._name = value;
  }
}

let p = new Person("Rahim");

console.log(p.name);
p.name = "Karim";
console.log(p.name);
```

---

# 7) Static Methods

Belong to class, not object.

```javascript id="c14"
class MathUtil {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathUtil.add(5, 3));
```

### Output:

```javascript id="c15"
8
```

---

# Summary

| Concept       | Meaning                         |
| ------------- | ------------------------------- |
| Class         | Blueprint of objects            |
| Object        | Instance of class               |
| Encapsulation | Data hiding inside class        |
| Inheritance   | Reusing class features          |
| Polymorphism  | Same method, different behavior |
| Abstraction   | Hide complexity                 |
| this          | Current object                  |

---

# Key Takeaways

✔ Classes simplify object creation
✔ OOP organizes large applications
✔ Used heavily in frameworks (React, Node.js)
✔ Makes code reusable and scalable

---

If you want next, I can teach:
👉 **Prototype & Inheritance (low-level JavaScript OOP concept used internally)**

# **Prototype & Prototype Inheritance**

## Prototype & Prototype Inheritance in JavaScript

In JavaScript, every object has a hidden property called a **prototype**. It is used to share methods and properties between objects.

Simple meaning:

> Prototype = a backup object that other objects can use

---

# 1) What is a Prototype?

When you create an object, JavaScript automatically attaches a prototype to it.

```javascript id="p1"
let person = {
  name: "Rahim"
};

console.log(person);
```

Internally, `person` has a hidden prototype.

---

# 2) Adding Methods using Prototype

Instead of adding methods inside every object, we can use prototype.

```javascript id="p2"
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log("Hello " + this.name);
};

let p1 = new Person("Rahim");
let p2 = new Person("Karim");

p1.greet();
p2.greet();
```

### Output:

```javascript id="p3"
Hello Rahim
Hello Karim
```

✔ One method shared by all objects
✔ Saves memory

---

# 3) Prototype Chain

If a property is not found in the object, JavaScript looks in its prototype.

Example:

```javascript id="p4"
let arr = [1, 2, 3];

console.log(arr.push); // built-in method
```

✔ `push()` comes from Array prototype

---

# 4) Prototype Inheritance

One object can inherit from another through prototype.

```javascript id="p5"
let animal = {
  eats: true
};

let dog = {
  bark: true
};

dog.__proto__ = animal;

console.log(dog.eats);
```

### Output:

```javascript id="p6"
true
```

✔ `dog` inherits from `animal`

---

# 5) Function Constructor + Prototype Inheritance

```javascript id="p7"
function Animal(name) {
  this.name = name;
}

Animal.prototype.eat = function () {
  console.log(this.name + " is eating");
};

function Dog(name) {
  Animal.call(this, name);
}

Dog.prototype = Object.create(Animal.prototype);

Dog.prototype.bark = function () {
  console.log("Barking");
};

let d = new Dog("Tommy");

d.eat();
d.bark();
```

### Output:

```javascript id="p8"
Tommy is eating
Barking
```

---

# 6) Prototype Chain Flow

```
Object → Prototype → Prototype → null
```

JavaScript searches step by step until it finds the property.

---

# 7) Built-in Prototypes

## Arrays

```javascript id="p9"
let arr = [1, 2, 3];

arr.map(x => x * 2);
```

✔ `map`, `filter`, `reduce` come from Array prototype

---

## Strings

```javascript id="p10"
let str = "hello";

str.toUpperCase();
```

✔ Methods come from String prototype

---

# 8) Why Prototype is Important

✔ Saves memory (methods not duplicated)
✔ Enables inheritance
✔ Core of JavaScript OOP system
✔ Used in all frameworks and libraries

---

# 9) Prototype vs Class (Modern JS)

| Feature         | Prototype     | Class              |
| --------------- | ------------- | ------------------ |
| Style           | Old (core JS) | Modern syntax      |
| Internal system | Yes           | Built on prototype |
| Performance     | Same          | Same               |

👉 Classes in JavaScript are just **syntactic sugar over prototypes**

---

# 10) Key Takeaways

✔ Every object has a prototype
✔ Prototypes allow sharing methods
✔ Prototype chain is used for lookup
✔ Inheritance happens via prototype
✔ Classes internally use prototypes

---

If you want next, I can explain:
👉 **Execution Context & Call Stack (most important for understanding how JavaScript runs internally)**


# **`this` Keyword**

## `this` Keyword in JavaScript

The `this` keyword refers to the **current context (owner of the code being executed)**.

Simple meaning:

> `this` = “who is calling me?”

---

# 1) `this` in Global Scope

In the browser:

```javascript id="t1"
console.log(this);
```

✔ Refers to **window object** (in browser)

---

# 2) `this` in Object

Inside an object, `this` refers to that object.

```javascript id="t2"
let person = {
  name: "Rahim",
  show: function () {
    console.log(this.name);
  }
};

person.show();
```

### Output:

```javascript id="t3"
Rahim
```

✔ `this` = `person`

---

# 3) `this` in Function

Normal function behaves differently.

```javascript id="t4"
function test() {
  console.log(this);
}

test();
```

✔ In browser → `window` (or `undefined` in strict mode)

---

# 4) `this` in Strict Mode

```javascript id="t5"
"use strict";

function test() {
  console.log(this);
}

test();
```

### Output:

```javascript id="t6"
undefined
```

---

# 5) `this` in Arrow Function

Arrow functions do NOT have their own `this`.

They take `this` from outer scope.

```javascript id="t7"
let person = {
  name: "Karim",
  show: () => {
    console.log(this.name);
  }
};

person.show();
```

✔ `this` is NOT `person`

Output:

```javascript id="t8"
undefined
```

---

# 6) Correct Way with Arrow Function

```javascript id="t9"
let person = {
  name: "Rahim",
  show: function () {
    let arrow = () => {
      console.log(this.name);
    };
    arrow();
  }
};

person.show();
```

### Output:

```javascript id="t10"
Rahim
```

✔ Arrow function inherits `this` from `show()`

---

# 7) `this` in Constructor Function

```javascript id="t11"
function Person(name) {
  this.name = name;
}

let p1 = new Person("Rahim");

console.log(p1.name);
```

### Output:

```javascript id="t12"
Rahim
```

✔ `this` refers to new object

---

# 8) `this` in Classes

In JavaScript classes:

```javascript id="t13"
class Person {
  constructor(name) {
    this.name = name;
  }

  show() {
    console.log(this.name);
  }
}

let p = new Person("Karim");
p.show();
```

### Output:

```javascript id="t14"
Karim
```

✔ `this` = instance of class

---

# 9) `this` in Event Handlers

```javascript id="t15"
document.getElementById("btn").addEventListener("click", function () {
  console.log(this);
});
```

✔ `this` = clicked element

---

# 10) Summary Table

| Context        | `this` refers to                 |
| -------------- | -------------------------------- |
| Global         | window / undefined (strict mode) |
| Object         | object itself                    |
| Function       | window / undefined               |
| Arrow Function | outer scope                      |
| Class          | instance of class                |
| Event          | HTML element                     |

---

# Key Takeaways

✔ `this` depends on **how function is called**
✔ Arrow functions do NOT have their own `this`
✔ Objects/classes use `this` heavily
✔ Important for interviews and real apps

---

If you want next, I can explain:
👉 **Execution Context & Call Stack (this will make everything like hoisting, scope, this fully clear)**


# **Execution Context**
## Execution Context in JavaScript

**Execution Context** is the environment in which JavaScript code is executed.

Simple meaning:

> It is the “box” where JavaScript code runs, stores variables, and keeps track of everything.

---

# 1) Types of Execution Context

There are **3 main types**:

### 1. Global Execution Context (GEC)

* Created first when program starts
* Runs the whole script

### 2. Function Execution Context (FEC)

* Created whenever a function is called

### 3. Eval Execution Context

* Rarely used (not important for beginners)

---

# 2) Global Execution Context (GEC)

When JS runs, it first creates:

✔ Global object (`window` in browser)
✔ `this` keyword
✔ Memory for variables and functions

Example:

```javascript id="ex1"
let a = 10;

function show() {
  console.log("Hello");
}

show();
```

✔ First step: Global Execution Context is created

---

# 3) Two Phases of Execution Context

## Phase 1: Memory Creation Phase

JavaScript:

* Allocates memory
* Variables = `undefined`
* Functions = stored fully

Example:

```javascript id="ex2"
console.log(a);

var a = 5;
```

Internally:

```javascript id="ex3"
var a = undefined;
console.log(a);
a = 5;
```

Output:

```javascript id="ex4"
undefined
```

---

## Phase 2: Execution Phase

Now code runs line by line.

---

# 4) Function Execution Context

Every function call creates a new context.

```javascript id="ex5"
function add(a, b) {
  let result = a + b;
  return result;
}

add(5, 3);
```

Steps:

1. Function called → new execution context created
2. Memory allocated for `a`, `b`, `result`
3. Code executes
4. Context is removed after return

---

# 5) Call Stack

Execution contexts are managed using a **stack (LIFO)**.

Example:

```javascript id="ex6"
function first() {
  second();
}

function second() {
  console.log("Inside second");
}

first();
```

### Call Stack Flow:

```
Global Context
→ first()
→ second()
→ back to first()
→ back to Global
```

---

# 6) Visual Flow

```id="ex7"
Global Execution Context
        ↓
Function Call → New Context Created
        ↓
Execute Code
        ↓
Context Removed
```

---

# 7) Real Example (Step-by-Step)

```javascript id="ex8"
var x = 10;

function multiply(y) {
  var result = x * y;
  return result;
}

multiply(5);
```

### Execution Steps:

1. Global context created
2. `x = undefined` → then `10`
3. Function stored
4. `multiply(5)` called
5. New function context created
6. `result = 10 * 5`
7. Return `50`
8. Function context destroyed

---

# 8) Relation with Other Concepts

Execution Context is directly related to:

✔ Hoisting
✔ Scope
✔ Call Stack
✔ Closures
✔ `this` keyword

All of them work inside execution contexts.

---

# 9) Key Takeaways

✔ Every JS code runs inside an execution context
✔ First is Global Execution Context
✔ Each function call creates a new context
✔ Managed using Call Stack
✔ Has 2 phases: Memory + Execution

---

# Final Simple Definition

> Execution Context is the environment where JavaScript code is executed and managed step-by-step.

---

If you want next, I can explain:
👉 **Call Stack in depth + real animation-style explanation (very important for interviews)**


# **Call Stack**

## Call Stack in JavaScript

The **Call Stack** is a data structure used by JavaScript to keep track of function execution.

Simple meaning:

> Call Stack = a “stack of functions” that tells JavaScript which function is running right now.

It follows **LIFO (Last In, First Out)** rule:

> The last function added is the first one removed.

---

# 1) Basic Idea

Think of it like a stack of plates:

* You add a plate on top → push
* You remove from top → pop

Same happens with functions.

---

# 2) Simple Example

```javascript id="cs1"
function first() {
  console.log("First function");
}

function second() {
  first();
  console.log("Second function");
}

second();
```

---

## Call Stack Flow:

1. Global Execution Context → pushed
2. `second()` → pushed
3. `first()` → pushed
4. `first()` finishes → popped
5. `second()` continues → popped
6. Global context ends

---

# 3) Step-by-Step Visualization

```id="cs2"
Call Stack:

1. Global Context
2. second()
3. first()
4. first() removed
5. second() removed
6. Global removed
```

---

# 4) Another Example

```javascript id="cs3"
function a() {
  b();
}

function b() {
  c();
}

function c() {
  console.log("Inside C");
}

a();
```

### Call Stack Flow:

```id="cs4"
Global → a → b → c → b → a → Global
```

---

# 5) Stack Overflow

If functions keep calling each other infinitely → stack fills up.

```javascript id="cs5"
function test() {
  test();
}

test();
```

### Result:

```id="cs6"
RangeError: Maximum call stack size exceeded
```

✔ This is called **Stack Overflow**

---

# 6) Why Call Stack is Important

Call Stack helps JavaScript:

✔ Track function execution order
✔ Manage nested function calls
✔ Handle return values properly
✔ Work with asynchronous behavior (along with Event Loop)

---

# 7) Call Stack vs Execution Context

| Concept           | Meaning                           |
| ----------------- | --------------------------------- |
| Execution Context | Environment where code runs       |
| Call Stack        | Stores and manages those contexts |

---

# 8) Real-Life Analogy

Imagine a restaurant kitchen:

* Chef starts dish A
* Dish A needs dish B
* Dish B needs dish C

Order:

1. C is made first
2. Then B
3. Then A

✔ This is exactly how Call Stack works

---

# 9) Key Takeaways

✔ Call Stack = manages function execution
✔ Works in LIFO order
✔ Every function call creates a stack entry
✔ Removes function after execution ends
✔ Too many calls → stack overflow

---

# Final Simple Definition

> Call Stack is a mechanism in JavaScript that keeps track of function calls in the order they are executed.

---

If you want next, I can explain:
👉 **Event Loop (this connects Call Stack + Async JS like Promises & setTimeout)**

#  **Event Loop**

## Event Loop in JavaScript

The **Event Loop** is the mechanism that allows JavaScript to handle **asynchronous code** (like `setTimeout`, Promises, API calls) even though it runs on a single thread.

Simple meaning:

> Event Loop = the system that decides when async code should run.

---

# 1) Why Event Loop is Needed

JavaScript is **single-threaded**, meaning:

* It can do only one thing at a time

But we still have:

* Timers (`setTimeout`)
* Promises
* API calls

👉 Event Loop helps manage these without blocking the main thread.

---

# 2) Main Parts Involved

## 1. Call Stack

* Runs synchronous code

## 2. Web APIs (Browser)

* Handles async tasks like timers

## 3. Callback Queue (Task Queue)

* Stores finished async callbacks

## 4. Event Loop

* Moves tasks from queue → call stack

---

# 3) Simple Flow

```id="el1"
Call Stack → Web APIs → Callback Queue → Event Loop → Call Stack
```

---

# 4) Example with setTimeout

```javascript id="el2"
console.log("Start");

setTimeout(() => {
  console.log("Inside Timeout");
}, 2000);

console.log("End");
```

### Output:

```id="el3"
Start
End
Inside Timeout
```

---

## Why this order?

Step-by-step:

1. `"Start"` → runs in Call Stack
2. `setTimeout` → sent to Web API
3. `"End"` → runs immediately
4. After 2 seconds → callback goes to queue
5. Event Loop sends it to Call Stack
6. `"Inside Timeout"` runs

---

# 5) Event Loop Visualization

```id="el4"
Call Stack
   ↓
Web API (timer)
   ↓
Callback Queue
   ↓
Event Loop
   ↓
Call Stack
```

---

# 6) Promises & Microtask Queue

Promises do NOT go to normal queue.

They go to **Microtask Queue**, which has higher priority.

---

## Example:

```javascript id="el5"
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

---

### Output:

```id="el6"
Start
End
Promise
Timeout
```

---

# 7) Why Promise runs before setTimeout?

Because:

| Queue Type                  | Priority |
| --------------------------- | -------- |
| Microtask Queue (Promises)  | High     |
| Callback Queue (setTimeout) | Low      |

👉 Event Loop always clears microtasks first.

---

# 8) Real-Life Analogy

Think of a restaurant:

* Chef = Call Stack
* Waiters = Web APIs
* Orders list = Queues
* Manager = Event Loop

Process:

1. Orders placed
2. Waiters prepare them
3. Manager brings finished orders back to chef

---

# 9) Key Rules

✔ JavaScript is single-threaded
✔ Async tasks go to Web APIs
✔ Call Stack runs sync code
✔ Event Loop moves tasks to stack
✔ Promises run before timers

---

# 10) Final Simple Definition

> Event Loop is a mechanism in JavaScript that continuously checks the Call Stack and queues, and moves tasks to be executed when the stack is empty.

---

# Key Takeaways

✔ Enables async programming in JavaScript
✔ Works with Call Stack + Queues + Web APIs
✔ Promises have higher priority than setTimeout
✔ Core concept for understanding modern JavaScript

---

If you want next, I can explain:
👉 **Microtasks vs Macrotasks (deep interview-level concept)**




# **Local Storage / Session Storage**


## Local Storage & Session Storage in JavaScript

Both **Local Storage** and **Session Storage** are part of the browser’s **Web Storage API**. They let you store data in the browser as **key–value pairs**.

Simple meaning:

> They store data in the browser so you don’t lose it on page reload (or even after closing the tab, depending on type).

---

# 1) Local Storage

### ✔ Features:

* Data is stored **permanently** (until manually deleted)
* Survives browser restart
* Same origin (same website)

---

## Save data

```javascript id="ls1"
localStorage.setItem("name", "Rahim");
```

## Get data

```javascript id="ls2"
console.log(localStorage.getItem("name"));
```

### Output:

```id="ls3"
Rahim
```

## Remove data

```javascript id="ls4"
localStorage.removeItem("name");
```

## Clear all

```javascript id="ls5"
localStorage.clear();
```

---

# 2) Session Storage

### ✔ Features:

* Data is stored **only for one tab session**
* Deleted when tab is closed
* Same origin

---

## Save data

```javascript id="ss1"
sessionStorage.setItem("city", "Dhaka");
```

## Get data

```javascript id="ss2"
console.log(sessionStorage.getItem("city"));
```

### Output:

```id="ss3"
Dhaka
```

---

## Remove data

```javascript id="ss4"
sessionStorage.removeItem("city");
```

---

# 3) Difference Between Local & Session Storage

| Feature      | Local Storage      | Session Storage  |
| ------------ | ------------------ | ---------------- |
| Lifetime     | Permanent          | Until tab closes |
| Tab support  | Shared across tabs | Only current tab |
| Storage size | ~5–10 MB           | ~5 MB            |
| Use case     | Login, settings    | Temporary data   |

---

# 4) Storing Objects

Storage only supports **strings**, so we use JSON.

---

## Save object

```javascript id="st1"
let user = {
  name: "Rahim",
  age: 25
};

localStorage.setItem("user", JSON.stringify(user));
```

---

## Get object

```javascript id="st2"
let data = JSON.parse(localStorage.getItem("user"));

console.log(data.name);
```

### Output:

```id="st3"
Rahim
```

---

# 5) Real Use Cases

✔ Login session info
✔ Dark mode settings
✔ Shopping cart data
✔ User preferences
✔ Temporary form data

---

# 6) Example: Dark Mode Toggle

```javascript id="ex1"
let mode = localStorage.getItem("mode");

if (mode === "dark") {
  document.body.style.background = "black";
  document.body.style.color = "white";
}

function toggleMode() {
  let current = localStorage.getItem("mode");

  if (current === "dark") {
    localStorage.setItem("mode", "light");
  } else {
    localStorage.setItem("mode", "dark");
  }
}
```

---

# 7) Important Notes

✔ Data is stored as **strings only**
✔ Same-origin policy applies
✔ Not secure for sensitive data (like passwords)
✔ Easily accessible via browser dev tools

---

# 8) When to Use What?

## Use Local Storage when:

* Data should persist long-term
* Example: theme, settings, saved items

## Use Session Storage when:

* Data is temporary
* Example: form steps, temporary login state

---

# 9) Key Takeaways

✔ Local Storage = permanent storage in browser
✔ Session Storage = temporary storage per tab
✔ Both store key–value pairs
✔ Must use JSON for objects
✔ Common in real-world web apps

---

If you want next, I can explain:
👉 **Cookies vs Local Storage (important for interviews & authentication)**


# **Fetch API / AJAX**

## Fetch API / AJAX in JavaScript

**AJAX** and **Fetch API** are used to send and receive data from a server without reloading the page.

Simple meaning:

> They let JavaScript talk to a server in the background.

---

# 1) What is AJAX?

**AJAX (Asynchronous JavaScript and XML)** is an old technique used to:

* Send requests to server
* Get data without refreshing page

👉 Today, we mostly use **Fetch API** instead of old AJAX (XMLHttpRequest).

---

# 2) Fetch API (Modern Way)

The **Fetch API** is the modern way to make HTTP requests.

---

## Basic GET Request

```javascript id="f1"
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(response => response.json())
  .then(data => console.log(data));
```

✔ Fetch gets data from server
✔ `.json()` converts response into JavaScript object

---

# 3) Same Example using async/await

```javascript id="f2"
async function getData() {
  let response = await fetch("https://jsonplaceholder.typicode.com/posts/1");

  let data = await response.json();

  console.log(data);
}

getData();
```

---

# 4) Output Example

```json id="f3"
{
  "userId": 1,
  "id": 1,
  "title": "sample title",
  "body": "sample body"
}
```

---

# 5) POST Request (Send Data)

```javascript id="f4"
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    title: "Hello",
    body: "World",
    userId: 1
  })
})
  .then(res => res.json())
  .then(data => console.log(data));
```

---

# 6) Using async/await (POST)

```javascript id="f5"
async function sendData() {
  let response = await fetch("https://jsonplaceholder.typicode.com/posts", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({
      title: "Hi",
      body: "Test",
      userId: 1
    })
  });

  let data = await response.json();
  console.log(data);
}

sendData();
```

---

# 7) Fetch Error Handling

```javascript id="f6"
async function getData() {
  try {
    let response = await fetch("https://invalid-url.com");

    if (!response.ok) {
      throw new Error("Network error");
    }

    let data = await response.json();
    console.log(data);
  } catch (error) {
    console.log("Error:", error.message);
  }
}
```

---

# 8) Fetch Workflow

```id="f7"
Request → Server → Response → JSON → JavaScript Data
```

---

# 9) AJAX (Old Method - XMLHttpRequest)

```javascript id="f8"
let xhr = new XMLHttpRequest();

xhr.open("GET", "https://jsonplaceholder.typicode.com/posts/1");

xhr.onload = function () {
  console.log(JSON.parse(xhr.response));
};

xhr.send();
```

✔ Works but complex
✔ Mostly replaced by Fetch API

---

# 10) Fetch vs AJAX

| Feature     | AJAX (XHR) | Fetch API |
| ----------- | ---------- | --------- |
| Syntax      | Complex    | Simple    |
| Modern      | ❌ Old      | ✔ Modern  |
| Promises    | ❌ No       | ✔ Yes     |
| Readability | Low        | High      |

---

# 11) Real Use Cases

✔ Loading API data
✔ Social media feeds
✔ Weather apps
✔ Login systems
✔ E-commerce products

---

# 12) Key Takeaways

✔ Fetch API is modern way to handle HTTP requests
✔ AJAX is older method (still works)
✔ Fetch returns a Promise
✔ Use async/await for clean code
✔ Essential for real-world web apps

---

# Final Simple Definition

> Fetch API is a modern JavaScript tool used to send and receive data from servers asynchronously.

---

If you want next, I can explain:
👉 **HTTP Methods (GET, POST, PUT, DELETE) in detail + real API examples**


# **Modules (Import / Export)**

## Modules (Import / Export) in JavaScript

**Modules** allow you to split code into multiple files and reuse them easily.

Simple meaning:

> Module = a separate file of code that can be shared and reused

---

# 1) Why Modules are Important?

Without modules:

* Code becomes messy
* Hard to maintain
* No reuse

With modules:
✔ Clean structure
✔ Reusable code
✔ Easy to manage large projects

---

# 2) Export (Send Code from a File)

You use `export` to make functions/variables available outside a file.

---

## Named Export

```javascript id="m1"
// file: math.js

export function add(a, b) {
  return a + b;
}

export function multiply(a, b) {
  return a * b;
}
```

---

# 3) Import (Use Code in Another File)

```javascript id="m2"
// file: main.js

import { add, multiply } from "./math.js";

console.log(add(5, 3));
console.log(multiply(2, 4));
```

### Output:

```id="m3"
8
8
```

---

# 4) Default Export

A file can have **only one default export**.

```javascript id="m4"
// file: greet.js

export default function greet() {
  console.log("Hello!");
}
```

---

## Import Default

```javascript id="m5"
// file: main.js

import greet from "./greet.js";

greet();
```

### Output:

```id="m6"
Hello!
```

---

# 5) Mixed Export

```javascript id="m7"
// file: utils.js

export const name = "Rahim";

export function sayHi() {
  console.log("Hi");
}

export default function welcome() {
  console.log("Welcome!");
}
```

---

## Import Mixed

```javascript id="m8"
import welcome, { name, sayHi } from "./utils.js";

console.log(name);
sayHi();
welcome();
```

---

# 6) Rename Imports / Exports

```javascript id="m9"
import { add as sum } from "./math.js";

console.log(sum(2, 3));
```

---

# 7) Import Everything

```javascript id="m10"
import * as math from "./math.js";

console.log(math.add(2, 3));
console.log(math.multiply(2, 3));
```

---

# 8) Types of Modules

## 1. ES Modules (Modern)

✔ Used in modern JavaScript
✔ Uses `import/export`
✔ Works in browser & Node.js

---

## 2. CommonJS (Old Node.js)

```javascript id="m11"
const math = require("./math");
```

---

# 9) Module Rules

✔ Each file is a module
✔ Variables are scoped to file
✔ Must explicitly export what you need
✔ Imports must be at top

---

# 10) Real-Life Example

## math.js

```javascript id="m12"
export function add(a, b) {
  return a + b;
}
```

## app.js

```javascript id="m13"
import { add } from "./math.js";

console.log(add(10, 20));
```

---

# 11) Why Modules Matter

✔ Clean code structure
✔ Better teamwork in large projects
✔ Reusability
✔ Used in frameworks like React, Node.js

---

# 12) Key Takeaways

✔ `export` → send code out
✔ `import` → use code in another file
✔ Named export → multiple exports
✔ Default export → one main export
✔ ES Modules are modern standard

---

# Final Simple Definition

> Modules in JavaScript allow you to split code into separate files and reuse them using import and export.

---

If you want next, I can explain:
👉 **JavaScript Project Structure (how real-world apps are organized using modules)**


#  **JSON Handling**

## JSON Handling in JavaScript

**JSON (JavaScript Object Notation)** is a lightweight format used to store and exchange data between a client and a server.

Simple meaning:

> JSON = text format used to represent data (like objects, arrays)

---

# 1) What JSON looks like

```json id="j1"
{
  "name": "Rahim",
  "age": 25,
  "city": "Dhaka"
}
```

✔ Looks like an object
✔ But it is actually **string data format**

---

# 2) JSON vs JavaScript Object

| Feature   | JSON                   | JavaScript Object |
| --------- | ---------------------- | ----------------- |
| Format    | String                 | Object            |
| Keys      | Must use double quotes | Quotes optional   |
| Functions | Not allowed            | Allowed           |
| Usage     | Data exchange          | Code usage        |

---

# 3) Convert Object → JSON (`stringify`)

```javascript id="j2"
let user = {
  name: "Rahim",
  age: 25
};

let jsonData = JSON.stringify(user);

console.log(jsonData);
```

### Output:

```id="j3"
{"name":"Rahim","age":25}
```

✔ Object → JSON string

---

# 4) Convert JSON → Object (`parse`)

```javascript id="j4"
let jsonString = '{"name":"Rahim","age":25}';

let obj = JSON.parse(jsonString);

console.log(obj.name);
```

### Output:

```id="j5"
Rahim
```

✔ JSON → JavaScript object

---

# 5) JSON in Arrays

```javascript id="j6"
let users = [
  { "name": "Rahim" },
  { "name": "Karim" }
];

console.log(users[0].name);
```

---

# 6) Sending JSON to Server (POST)

```javascript id="j7"
fetch("https://example.com/api", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify({
    name: "Rahim",
    age: 25
  })
});
```

✔ Data must be converted to JSON before sending

---

# 7) Receiving JSON from API

```javascript id="j8"
fetch("https://jsonplaceholder.typicode.com/users/1")
  .then(res => res.json())
  .then(data => console.log(data));
```

✔ `.json()` converts response into object

---

# 8) Pretty JSON Formatting

```javascript id="j9"
let user = {
  name: "Rahim",
  age: 25
};

console.log(JSON.stringify(user, null, 2));
```

### Output:

```json id="j10"
{
  "name": "Rahim",
  "age": 25
}
```

---

# 9) Common JSON Rules

✔ Keys must be in double quotes
✔ No functions allowed
✔ No comments allowed
✔ Only data (string, number, boolean, array, object, null)

---

# 10) Real-World Use Cases

✔ APIs (frontend ↔ backend communication)
✔ Database responses
✔ Configuration files
✔ LocalStorage data storage
✔ Mobile apps

---

# 11) JSON Methods Summary

| Method           | Purpose       |
| ---------------- | ------------- |
| JSON.stringify() | Object → JSON |
| JSON.parse()     | JSON → Object |

---

# 12) Key Takeaways

✔ JSON is a data format (not code)
✔ Used for server communication
✔ Must convert using `stringify` and `parse`
✔ Essential for APIs and modern web apps

---

# Final Simple Definition

> JSON is a text-based format used to store and exchange data between systems, especially between a browser and a server.

---

If you want next, I can explain:
👉 **API Integration Project (Real-world example using Fetch + JSON + DOM)**

#  **Regular Expressions**

## Regular Expressions (RegEx) in JavaScript

A **Regular Expression (RegEx)** is a pattern used to **search, match, and manipulate text**.

Simple meaning:

> RegEx = a “search rule” for strings

---

# 1) Creating a Regular Expression

You can create RegEx in two ways:

## Literal way

```javascript id="r1"
let pattern = /hello/;
```

## Constructor way

```javascript id="r2"
let pattern = new RegExp("hello");
```

---

# 2) Basic Match

```javascript id="r3"
let text = "Hello world";

let result = /Hello/.test(text);

console.log(result);
```

### Output:

```id="r4"
true
```

✔ `.test()` checks if pattern exists

---

# 3) Match Method

```javascript id="r5"
let text = "I love JavaScript";

let result = text.match(/JavaScript/);

console.log(result);
```

---

# 4) Flags in RegEx

Flags change how matching works:

| Flag | Meaning              |
| ---- | -------------------- |
| g    | global (all matches) |
| i    | case-insensitive     |
| m    | multiline            |

---

## Example: case-insensitive

```javascript id="r6"
let text = "Hello hello";

console.log(text.match(/hello/i));
```

✔ matches "Hello" and "hello"

---

## Global match

```javascript id="r7"
let text = "hi hi hi";

console.log(text.match(/hi/g));
```

### Output:

```id="r8"
["hi", "hi", "hi"]
```

---

# 5) Common RegEx Patterns

## Digits

```javascript id="r9"
let pattern = /\d/; // any digit
```

## Words

```javascript id="r10"
let pattern = /\w/; // letters, numbers, underscore
```

## Spaces

```javascript id="r11"
let pattern = /\s/; // whitespace
```

---

# 6) Email Validation Example

```javascript id="r12"
let email = "test@gmail.com";

let pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

console.log(pattern.test(email));
```

### Output:

```id="r13"
true
```

---

# 7) Phone Number Example

```javascript id="r14"
let phone = "01712345678";

let pattern = /^01[0-9]{9}$/;

console.log(pattern.test(phone));
```

✔ Validates Bangladeshi number format

---

# 8) Replace Using RegEx

```javascript id="r15"
let text = "I like JavaScript JavaScript";

let newText = text.replace(/JavaScript/g, "JS");

console.log(newText);
```

### Output:

```id="r16"
I like JS JS
```

---

# 9) Split Using RegEx

```javascript id="r17"
let text = "apple, banana; mango";

let result = text.split(/[,;]/);

console.log(result);
```

### Output:

```id="r18"
["apple", " banana", " mango"]
```

---

# 10) Common RegEx Symbols

| Symbol | Meaning         |
| ------ | --------------- |
| .      | any character   |
| ^      | start of string |
| $      | end of string   |
| *      | 0 or more       |
| +      | 1 or more       |
| ?      | optional        |
| []     | character set   |
| {}     | quantity        |

---

# 11) Example: Password Check

```javascript id="r19"
let password = "Pass1234";

let pattern = /^(?=.*[A-Z])(?=.*\d).{6,}$/;

console.log(pattern.test(password));
```

✔ At least 1 uppercase
✔ At least 1 number
✔ Minimum 6 characters

---

# 12) Real Use Cases

✔ Form validation
✔ Search functionality
✔ Text filtering
✔ Data cleaning
✔ Pattern matching in APIs

---

# 13) Key Takeaways

✔ RegEx = pattern matching tool
✔ Used with strings in JavaScript
✔ `.test()` → true/false
✔ `.match()` → get matches
✔ `.replace()` → modify text
✔ Very powerful for validation

---

# Final Simple Definition

> Regular Expressions are patterns used to search, match, and manipulate text efficiently.

---

If you want next, I can explain:
👉 **Form Validation Project (using RegEx + DOM + Events together)**

# **Debouncing & Throttling**

## Debouncing & Throttling in JavaScript

Both **debouncing** and **throttling** are techniques used to control how often a function runs when events happen repeatedly (like typing, scrolling, resizing).

Simple meaning:

> They help improve performance by limiting function calls.

---

# 1) Debouncing

### Idea:

👉 Run the function **only after the event stops for a certain time**

Example:

* User typing in search box
* Wait until user stops typing → then call API

---

## Debouncing Example

```javascript id="d1"
function debounce(func, delay) {
  let timer;

  return function () {
    clearTimeout(timer);

    timer = setTimeout(() => {
      func();
    }, delay);
  };
}

function search() {
  console.log("Searching...");
}

let optimizedSearch = debounce(search, 1000);

optimizedSearch();
optimizedSearch();
optimizedSearch();
```

---

### How it works:

* Every keystroke resets timer
* Function runs only after 1 second of inactivity

---

### Real Output:

```
Searching...
```

(only once after typing stops)

---

# 2) Throttling

### Idea:

👉 Run the function **at fixed intervals**, no matter how many times event fires

Example:

* Scroll event
* Execute function every 1 second

---

## Throttling Example

```javascript id="d2"
function throttle(func, limit) {
  let inThrottle = false;

  return function () {
    if (!inThrottle) {
      func();

      inThrottle = true;

      setTimeout(() => {
        inThrottle = false;
      }, limit);
    }
  };
}

function scrollHandler() {
  console.log("Scrolling...");
}

let optimizedScroll = throttle(scrollHandler, 2000);

optimizedScroll();
optimizedScroll();
optimizedScroll();
```

---

### How it works:

* Function runs immediately
* Then ignores calls for 2 seconds

---

### Output:

```
Scrolling...
```

(only once every 2 seconds)

---

# 3) Debouncing vs Throttling

| Feature      | Debouncing               | Throttling            |
| ------------ | ------------------------ | --------------------- |
| When it runs | After delay (user stops) | At fixed intervals    |
| Best for     | Search input, typing     | Scroll, resize        |
| Behavior     | Delays execution         | Limits execution rate |

---

# 4) Real-Life Examples

## Debouncing:

✔ Search bar (Google search)
✔ Form validation
✔ API calls on typing

## Throttling:

✔ Scroll events
✔ Button spam clicks
✔ Window resize

---

# 5) Visual Difference

## Debouncing:

```id="v1"
Typing → Typing → Typing → STOP → Run function
```

## Throttling:

```id="v2"
Run → wait → Run → wait → Run
```

---

# 6) Why They Are Important

✔ Improve performance
✔ Reduce API calls
✔ Prevent lag in UI
✔ Optimize heavy events

---

# 7) Key Takeaways

✔ Debouncing = wait until user stops
✔ Throttling = run at intervals
✔ Both optimize event-heavy operations
✔ Very important in real-world web apps

---

# Final Simple Definition

> Debouncing delays function execution until activity stops, while throttling limits how often a function runs during continuous activity.

---

If you want next, I can explain:
👉 **JavaScript Interview Questions (Core + Advanced roadmap from all topics you learned)**

# **Memory Management & Garbage Collection**


## Memory Management & Garbage Collection in JavaScript

Memory management is how JavaScript stores, uses, and removes data while your program runs.

Simple meaning:

> Memory management = allocating memory + freeing unused memory automatically

---

# 1) Memory in JavaScript

When code runs, memory is used for:

* Variables
* Objects
* Functions
* Arrays

---

## Two main memory areas:

### 1. Stack Memory

* Stores **primitive values** (number, string, boolean)
* Stores function calls (execution context)

Example:

```javascript id="m1"
let a = 10;
let b = "Hello";
```

---

### 2. Heap Memory

* Stores **objects, arrays, functions**
* Dynamic memory (can grow/shrink)

Example:

```javascript id="m2"
let obj = {
  name: "Rahim",
  age: 25
};
```

---

# 2) What is Garbage Collection?

Garbage Collection is the process where JavaScript automatically:

> Removes unused memory to prevent memory leaks

You don’t control it manually.

---

# 3) How Garbage Collection Works

JavaScript uses a system called:

👉 **Mark and Sweep Algorithm**

---

## Step-by-step:

### Step 1: Mark

JavaScript marks all **reachable objects**

### Step 2: Sweep

It removes all **unreachable objects**

---

# 4) Example of Garbage Collection

```javascript id="g1"
function test() {
  let data = {
    name: "Rahim"
  };

  console.log(data);
}

test();
```

After function ends:
✔ `data` is no longer needed
✔ It becomes unreachable
✔ Garbage collector removes it

---

# 5) Unreachable Memory Example

```javascript id="g2"
let user = {
  name: "Karim"
};

user = null;
```

✔ Original object has no reference
✔ It becomes garbage
✔ Memory is freed

---

# 6) Memory Leak (Bad Practice)

Memory leak happens when memory is NOT released.

```javascript id="g3"
let arr = [];

function addData() {
  arr.push(new Array(1000).fill("data"));
}
```

✔ If this runs repeatedly → memory keeps increasing

---

# 7) Common Causes of Memory Leaks

### ❌ 1. Unused variables still referenced

### ❌ 2. Forgotten event listeners

### ❌ 3. Global variables

### ❌ 4. Timers not cleared

---

## Example: Event Listener Leak

```javascript id="g4"
let button = document.getElementById("btn");

button.addEventListener("click", function () {
  console.log("Clicked");
});
```

If not removed → memory may stay occupied

---

# 8) Fixing Memory Issues

## Remove event listener

```javascript id="g5"
button.removeEventListener("click", handler);
```

## Clear timers

```javascript id="g6"
clearInterval(intervalId);
clearTimeout(timeoutId);
```

---

# 9) Stack vs Heap

| Feature    | Stack            | Heap              |
| ---------- | ---------------- | ----------------- |
| Stores     | Primitive values | Objects, arrays   |
| Size       | Small            | Large             |
| Speed      | Fast             | Slower            |
| Management | Automatic        | Garbage collected |

---

# 10) Why Garbage Collection is Important

✔ Prevents memory overflow
✔ Improves performance
✔ Frees unused resources
✔ Makes JavaScript easier to use

---

# 11) Key Takeaways

✔ Memory is split into stack and heap
✔ JavaScript automatically manages memory
✔ Garbage collector removes unused objects
✔ Developers must avoid memory leaks
✔ No manual memory management needed

---

# Final Simple Definition

> Memory management in JavaScript is the automatic process of allocating and freeing memory, and Garbage Collection removes unused data to optimize performance.

---

If you want next, I can explain:
👉 **JavaScript Engine (V8) + How code actually runs internally step-by-step**


------------
## JavaScript Engine (V8) & How Code Runs Internally in JavaScript

A **JavaScript Engine** is the program that executes JavaScript code inside the browser or server.

The most popular engine is **V8**, used in Google Chrome and Node.js.

Simple meaning:

> V8 = the “machine” that reads JavaScript and turns it into fast machine code.

---

# 1) What Happens When You Run JavaScript?

When you write:

```javascript id="v1"
let x = 10;
console.log(x);
```

It does NOT run directly. Instead, V8 processes it step-by-step.

---

# 2) High-Level Architecture of V8

V8 has 2 main parts:

### 1. Parser

* Reads JavaScript code
* Converts it into **Abstract Syntax Tree (AST)**

### 2. Compiler + Execution Engine

* Converts AST into machine code
* Executes it

---

# 3) Step-by-Step Execution Flow

## Step 1: Code is received

You write JavaScript code.

---

## Step 2: Parsing

V8 reads code and checks syntax.

Example:

```javascript id="v2"
let a = 5;
```

✔ Parser checks:

* Is syntax correct?
* Are variables valid?

Then creates **AST (tree structure)**.

---

## Step 3: AST (Abstract Syntax Tree)

Code is converted into a structured format:

```id="ast"
VariableDeclaration
 └── a = 5
```

✔ This helps engine understand code logically.

---

## Step 4: Interpreter (Ignition)

V8 uses an interpreter called **Ignition**:

* Converts AST → bytecode
* Executes quickly

---

## Step 5: Execution Starts

Example:

```javascript id="v3"
console.log("Hello");
```

✔ Ignition runs bytecode line by line

---

## Step 6: Optimization (TurboFan)

V8 observes code and finds:

* Repeated functions
* Heavy operations

Then:
👉 Converts them into **optimized machine code**

This is done by **TurboFan**

---

## Step 7: Machine Code Execution

Now code runs directly on CPU:

* Very fast execution
* No interpretation needed anymore

---

# 4) Full Flow Diagram

```id="flow1"
JavaScript Code
      ↓
Parser
      ↓
AST (Tree)
      ↓
Ignition (Bytecode)
      ↓
Execution
      ↓
TurboFan Optimization
      ↓
Machine Code (Fast Execution)
```

---

# 5) Call Stack & Engine Connection

Inside V8:

* Call Stack manages function execution
* Heap stores objects
* Engine runs everything inside these structures

---

Example:

```javascript id="v4"
function add(a, b) {
  return a + b;
}

add(2, 3);
```

Flow:

1. Function goes to Call Stack
2. Ignition executes it
3. If repeated → TurboFan optimizes it

---

# 6) Memory Inside V8

## Stack

* Primitive values
* Function calls

## Heap

* Objects
* Arrays
* Functions

---

# 7) Why V8 is Fast

✔ Uses Just-In-Time (JIT) compilation
✔ Converts JS → machine code
✔ Optimizes frequently used code
✔ Removes unused code paths

---

# 8) Hidden Optimization Tricks

### 1. Inline Caching

Stores repeated property access for speed.

### 2. Hidden Classes

Helps objects behave like structured C++ objects.

Example:

```javascript id="v5"
let obj = { name: "Rahim" };
```

V8 assigns a hidden structure for fast access.

---

# 9) Real-World Analogy

Think of V8 like a restaurant:

| Component | Role                              |
| --------- | --------------------------------- |
| Parser    | Reads order                       |
| AST       | Prepares recipe                   |
| Ignition  | Cooks food quickly                |
| TurboFan  | Improves recipe for future orders |
| CPU       | Final serving                     |

---

# 10) Key Takeaways

✔ V8 is the JavaScript engine used in Chrome & Node.js
✔ It converts JavaScript into machine code
✔ Uses parsing → AST → bytecode → optimization → execution
✔ Uses JIT compilation for speed
✔ Makes JavaScript very fast in modern apps

---

# Final Simple Definition

> The V8 engine is a high-performance JavaScript engine that parses, compiles, optimizes, and executes JavaScript code using a combination of interpreter and JIT compiler techniques.

---

If you want next, I can explain:
👉 **Event Loop vs V8 Engine (how browser + engine + async system work together in real time)**


_______________
# NULISH  = null/ undefined

In many programming languages, `null` and `undefined` are treated as “no value” states.

So if someone writes:

```js
NULISH = null / undefined
```

they usually mean **“nullish”** values — values that are either:

```js
null
undefined
```

In JavaScript, this concept appears in:

### Nullish coalescing operator (`??`)

```js
const value = input ?? "default";
```

This uses `"default"` only when `input` is `null` or `undefined`.

Examples:

```js
null ?? "x"        // "x"
undefined ?? "x"   // "x"
0 ?? "x"           // 0
false ?? "x"       // false
```

So “nullish” is different from “falsy”.

Falsy values:

```js
false, 0, "", NaN, null, undefined
```

Nullish values:

```js
null, undefined
```
