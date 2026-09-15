
### 1. Creating a variable

JavaScript mainly uses `let`, `const`, and sometimes `var`.

```js
let age = 15;
const name = "Alex";
var city = "Dhaka";
```

Here:

- `age` → variable name
    
- `15` → value stored in it
    
- `=` → assigns the value
    

### 2. `let`

Use `let` when the value **can change**.

```js
let score = 10;

score = 20;

console.log(score);
```

Output:

```text
20
```

The value of `score` changed from `10` to `20`.

### 3. `const`

Use `const` when you **don't want to reassign** the variable.

```js
const pi = 3.14;

console.log(pi);
```

You can't do:

```js
pi = 4; // Error
```

### 4. Different types of values

A variable can hold different types of data:

```js
let name = "Rahim";       // String
let age = 16;             // Number
let isStudent = true;     // Boolean
let nothing = null;       // Null
```

### 5. A simple real example

```js
let name = "Rahim";
let age = 16;

console.log("My name is " + name);
console.log("I am " + age + " years old");
```

Output:

```text
My name is Rahim
I am 16 years old
```

**Easy way to remember:**

`let` → value can change  
`const` → value shouldn't be reassigned  
`var` → older way; generally use `let` or `const` instead.

----
todays JavaScript topic হলো **Understanding Operators & Expressions**। এটা JavaScript-এর খুব গুরুত্বপূর্ণ foundation, কারণ condition, loop, function, calculation—সব জায়গাতেই operator ব্যবহার হবে।

---

# 1. Operator কী?

**Operator** হলো এমন একটি symbol বা keyword যেটা কোনো value-এর উপর নির্দিষ্ট operation করে।

Example:

```javascript
let a = 10;
let b = 5;

console.log(a + b);
```

এখানে:

- `a` → operand
    
- `b` → operand
    
- `+` → operator
    
- `a + b` → expression
    
- Result → `15`
    

সহজভাবে:

```text
Operand + Operator + Operand

10      +     5
```

---

# 2. Expression কী?

**Expression** হলো এমন একটি combination যেটা JavaScript একটি value-তে evaluate করতে পারে।

Example:

```javascript
10 + 5
```

Result:

```text
15
```

আরেকটি:

```javascript
age >= 18
```

Result হতে পারে:

```text
true
```

আরেকটি:

```javascript
name + " Rahman"
```

Result:

```text
"Atiar Rahman"
```

অর্থাৎ:

> **Expression এমন কিছু যা একটি value produce করে।**

---

# 3. Arithmetic Operators

Arithmetic operator দিয়ে mathematical calculation করা হয়।

|Operator|কাজ|Example|Result|
|---|---|---|---|
|`+`|Addition|`10 + 5`|`15`|
|`-`|Subtraction|`10 - 5`|`5`|
|`*`|Multiplication|`10 * 5`|`50`|
|`/`|Division|`10 / 5`|`2`|
|`%`|Remainder|`10 % 3`|`1`|
|`**`|Power|`2 ** 3`|`8`|

Example:

```javascript
let a = 10;
let b = 3;

console.log(a + b);  // 13
console.log(a - b);  // 7
console.log(a * b);  // 30
console.log(a / b);  // 3.333...
console.log(a % b);  // 1
console.log(a ** b); // 1000
```

### `%` খুব গুরুত্বপূর্ণ

```javascript
console.log(10 % 3);
```

Result:

```text
1
```

কারণ:

```text
10 ÷ 3 = 3 remainder 1
```

Even/odd check করতে `%` অনেক ব্যবহার হয়।

```javascript
let number = 10;

console.log(number % 2 === 0);
```

Result:

```text
true
```

---

# 4. Assignment Operators

Assignment operator দিয়ে variable-এর মধ্যে value assign বা update করা হয়।

সবচেয়ে basic:

```javascript
let age = 25;
```

এখানে:

```text
= → assignment operator
```

আরও কিছু:

```javascript
let x = 10;

x += 5;

console.log(x);
```

Result:

```text
15
```

এটা:

```javascript
x += 5;
```

এর equivalent:

```javascript
x = x + 5;
```

একইভাবে:

```javascript
x -= 3;
```

মানে:

```javascript
x = x - 3;
```

```javascript
x *= 2;
```

মানে:

```javascript
x = x * 2;
```

```javascript
x /= 2;
```

মানে:

```javascript
x = x / 2;
```

---

# 5. Comparison Operators

Comparison operator দুইটা value compare করে এবং সাধারণত `true` অথবা `false` return করে।

```javascript
let age = 20;

console.log(age > 18);
```

Result:

```text
true
```

প্রধান operators:

| Operator | Meaning               |
| -------- | --------------------- |
| `>`      | Greater than          |
| `<`      | Less than             |
| `>=`     | Greater than or equal |
| `<=`     | Less than or equal    |
| `===`    | Strictly equal        |
| `!==`    | Strictly not equal    |

Example:

```javascript
let a = 10;
let b = 5;

console.log(a > b);   // true
console.log(a < b);   // false
console.log(a >= 10); // true
console.log(b <= 5);  // true
```

---

# 6. `==` vs `===`

এটা খুব গুরুত্বপূর্ণ।

### `==`

শুধু value compare করে এবং প্রয়োজন হলে type conversion করতে পারে।

```javascript
console.log(5 == "5");
```

Result:

```text
true
```

কারণ JavaScript এখানে `"5"` কে number `5` হিসেবে consider করে।

### `===`

Value এবং type—দুটোই compare করে।

```javascript
console.log(5 === "5");
```

Result:

```text
false
```

কারণ:

```text
5     → number
"5"   → string
```

### Best practice

সাধারণত JavaScript code-এ:

```javascript
===
```

এবং

```javascript
!==
```

ব্যবহার করা ভালো।

---

# 7. Logical Operators

Logical operators একাধিক condition combine করতে ব্যবহৃত হয়।

মূল তিনটি:

```text
&&
||
!
```

---

## `&&` — AND

দুইটি condition-ই `true` হতে হবে।

```javascript
let age = 25;
let hasID = true;

console.log(age >= 18 && hasID);
```

Result:

```text
true
```

কিন্তু:

```javascript
let age = 25;
let hasID = false;

console.log(age >= 18 && hasID);
```

Result:

```text
false
```

কারণ:

```text
true && false
     ↓
   false
```

---

# 8. `||` — OR

যেকোনো একটি condition `true` হলেই result `true`।

```javascript
let isStudent = false;
let isEmployee = true;

console.log(isStudent || isEmployee);
```

Result:

```text
true
```

কারণ:

```text
false || true
      ↓
    true
```

---

# 9. `!` — NOT

`true` কে `false` এবং `false` কে `true` করে।

```javascript
let isLoggedIn = true;

console.log(!isLoggedIn);
```

Result:

```text
false
```

আর:

```javascript
let isLoggedIn = false;

console.log(!isLoggedIn);
```

Result:

```text
true
```

---

# 10. Increment Operator `++`

একটি value 1 বাড়ায়।

```javascript
let count = 5;

count++;

console.log(count);
```

Result:

```text
6
```

Equivalent:

```javascript
count = count + 1;
```

---

# 11. Decrement Operator `--`

একটি value 1 কমায়।

```javascript
let count = 5;

count--;

console.log(count);
```

Result:

```text
4
```

Equivalent:

```javascript
count = count - 1;
```

---

# 12. `++x` vs `x++`

এটা একটু advanced কিন্তু খুব গুরুত্বপূর্ণ।

### Post-increment

```javascript
let x = 5;

let y = x++;

console.log(x);
console.log(y);
```

Result:

```text
6
5
```

কারণ আগে `x`-এর পুরোনো value ব্যবহার হয়েছে, তারপর increment হয়েছে।

### Pre-increment

```javascript
let x = 5;

let y = ++x;

console.log(x);
console.log(y);
```

Result:

```text
6
6
```

কারণ আগে increment হয়েছে, তারপর value ব্যবহার হয়েছে।

সহজভাবে:

```text
x++ → আগে use, পরে increase

++x → আগে increase, পরে use
```

---

# 13. String-এর সাথে `+`

`+` শুধু mathematical addition-এর জন্য নয়।

String concatenate করতেও ব্যবহার হয়।

```javascript
let firstName = "Md.";
let lastName = "Atiar";

let fullName = firstName + " " + lastName;

console.log(fullName);
```

Result:

```text
Md. Atiar
```

আরও modern way:

```javascript
let name = "Atiar";
let age = 25;

console.log("My name is " + name + " and I am " + age);
```

---

# 14. Template Literal

এটার আরও clean version:

```javascript
let name = "Atiar";
let age = 25;

console.log(`My name is ${name} and I am ${age}`);
```

Result:

```text
My name is Atiar and I am 25
```

এখানে:

```javascript
${name}
```

একটি expression।

Example:

```javascript
let a = 10;
let b = 20;

console.log(`Total = ${a + b}`);
```

Result:

```text
Total = 30
```

---

# 15. Ternary Operator

Ternary operator ছোট `if-else` লেখার জন্য ব্যবহার করা যায়।

Syntax:

```javascript
condition ? valueIfTrue : valueIfFalse
```

Example:

```javascript
let age = 20;

let result = age >= 18 ? "Adult" : "Minor";

console.log(result);
```

Result:

```text
Adult
```

এটা:

```javascript
if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
```

এর short version।

---

# 16. Operator Precedence

একাধিক operator থাকলে JavaScript নির্দিষ্ট priority অনুযায়ী calculation করে।

Example:

```javascript
let result = 10 + 5 * 2;

console.log(result);
```

অনেকে ভাবতে পারে:

```text
10 + 5 = 15
15 * 2 = 30
```

কিন্তু result হবে:

```text
20
```

কারণ multiplication আগে হবে:

```text
5 * 2 = 10

10 + 10 = 20
```

### Parentheses ব্যবহার করলে

```javascript
let result = (10 + 5) * 2;

console.log(result);
```

Result:

```text
30
```

তাই complex expression-এ `()` ব্যবহার করলে code অনেক পরিষ্কার হয়।

---

# 17. Real-world Example

ধরো একটি website-এ user-এর age এবং login status check করতে হবে।

```javascript
let age = 22;
let isLoggedIn = true;

let canAccess = age >= 18 && isLoggedIn;

console.log(canAccess);
```

Result:

```text
true
```

এখানে পুরো:

```javascript
age >= 18 && isLoggedIn
```

একটি **expression**।

এখানে:

```text
>=  → comparison operator
&&  → logical operator
```

---

# 18. আরেকটি Real Example

Shopping cart:

```javascript
let price = 1000;
let quantity = 3;
let discount = 200;

let total = price * quantity - discount;

console.log(total);
```

Calculation:

```text
1000 × 3 = 3000

3000 - 200 = 2800
```

Result:

```text
2800
```

এখানে:

```javascript
price * quantity - discount
```

একটি expression।

---

# 19. সব Operator একসাথে

একটি example দেখি:

```javascript
let price = 500;
let quantity = 3;
let discount = 100;

let total = price * quantity;

total -= discount;

let isExpensive = total > 1000;

console.log(total);
console.log(isExpensive);
```

Output:

```text
1400
true
```

এখানে আমরা ব্যবহার করেছি:

```text
*   Arithmetic
-=  Assignment
>   Comparison
```

---

# 20. সবচেয়ে গুরুত্বপূর্ণ Concept

তুমি এই distinction-টা পরিষ্কারভাবে মনে রাখবে:

```javascript
let a = 10;
let b = 20;

let result = a + b;
```

এখানে:

```text
a এবং b
↓
Operands

+
↓
Operator

a + b
↓
Expression

result
↓
Variable
```

আর:

```javascript
a + b
```

evaluate হয়ে:

```text
30
```

produce করে।

---

## Operator Cheat Sheet

```text
Arithmetic
+  -  *  /  %  **

Assignment
=  +=  -=  *=  /=

Comparison
>  <  >=  <=  ===  !==

Logical
&&  ||  !

Increment / Decrement
++  --

Ternary
? :

String
+
```

### তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ learning order

```text
1. Arithmetic Operators
        ↓
2. Assignment Operators
        ↓
3. Comparison Operators
        ↓
4. Logical Operators
        ↓
5. Increment / Decrement
        ↓
6. Ternary Operator
        ↓
7. Operator Precedence
        ↓
8. Expressions
        ↓
9. Real-world conditions
```

**পরের step হিসেবে `Operator Precedence + Truthy/Falsy + Short-Circuit Evaluation` ভালোভাবে শিখলে JavaScript condition-এর foundation অনেক strong হবে।**

---

JavaScript-এর **String** ভালোভাবে শেখা খুব গুরুত্বপূর্ণ, কারণ frontend development-এ প্রায় প্রতিদিনই string নিয়ে কাজ করতে হয়।

# JavaScript String — বিস্তারিত

## 1. String কী?

String হলো **text/data-এর sequence of characters**।

```javascript
let name = "Atiar";
let country = "Bangladesh";
let message = "Hello World!";
```

এখানে:

```javascript
"Atiar"
"Bangladesh"
"Hello World!"
```

সবগুলোই String।

JavaScript-এ String লেখার ৩টি common way আছে:

```javascript
let a = "Hello";
let b = 'Hello';
let c = `Hello`;
```

তিনটিই String।

---

# 2. Double quote, Single quote, Backtick

### Double quote

```javascript
let name = "Atiar";
```

### Single quote

```javascript
let name = 'Atiar';
```

### Backtick

```javascript
let name = `Atiar`;
```

Backtick-এর সবচেয়ে বড় সুবিধা হলো **template literal** ব্যবহার করা যায়।

```javascript
let name = "Atiar";
let age = 25;

let message = `My name is ${name} and I am ${age} years old.`;

console.log(message);
```

Output:

```text
My name is Atiar and I am 25 years old.
```

এখানে:

```javascript
${name}
${age}
```

কে বলা হয় **interpolation**।

---

# 3. String-এর length

String-এর কতগুলো character আছে সেটা জানতে `.length` ব্যবহার করি।

```javascript
let name = "Atiar";

console.log(name.length);
```

Output:

```text
5
```

আরেকটি:

```javascript
let text = "Hello World";

console.log(text.length);
```

Output:

```text
11
```

কারণ:

```text
Hello = 5
space = 1
World = 5

Total = 11
```

### Important

Space-ও character হিসেবে count হয়।

```javascript
let text = "Hi Atiar";

console.log(text.length);
```

Output:

```text
8
```

---

# 4. String indexing

String-এর প্রতিটি character-এর একটি index থাকে।

Index শুরু হয় **0 থেকে**।

```javascript
let name = "Atiar";
```

এটা:

```text
A t i a r
0 1 2 3 4
```

তাই:

```javascript
console.log(name[0]);
```

Output:

```text
A
```

```javascript
console.log(name[2]);
```

Output:

```text
i
```

```javascript
console.log(name[4]);
```

Output:

```text
r
```

---

# 5. Negative indexing — at()

Modern JavaScript-এ `at()` ব্যবহার করে reverse direction থেকেও character নেওয়া যায়।

```javascript
let name = "Atiar";

console.log(name.at(-1));
```

Output:

```text
r
```

```javascript
console.log(name.at(-2));
```

Output:

```text
a
```

অর্থাৎ:

```text
A t i a r
↑       ↑
0       -1
```

---

# 6. charAt()

Character পাওয়ার আরেকটি method:

```javascript
let name = "Atiar";

console.log(name.charAt(0));
```

Output:

```text
A
```

```javascript
console.log(name.charAt(3));
```

Output:

```text
a
```

Difference:

```javascript
name[10]
```

returns:

```text
undefined
```

কিন্তু:

```javascript
name.charAt(10)
```

returns:

```text
""
```

---

# 7. toUpperCase()

String-এর সব character uppercase করতে:

```javascript
let name = "atiar";

console.log(name.toUpperCase());
```

Output:

```text
ATIAR
```

Example:

```javascript
let email = "Atiar@Gmail.com";

console.log(email.toUpperCase());
```

Output:

```text
ATIAR@GMAIL.COM
```

---

# 8. toLowerCase()

সব character lowercase করতে:

```javascript
let name = "ATIAR";

console.log(name.toLowerCase());
```

Output:

```text
atiar
```

### Real-world example

Login/email comparison-এর সময়:

```javascript
let email = "ATIAR@GMAIL.COM";

let normalizedEmail = email.toLowerCase();

console.log(normalizedEmail);
```

Output:

```text
atiar@gmail.com
```

---

# 9. trim()

User input-এর শুরু এবং শেষের unnecessary spaces remove করতে `trim()` ব্যবহার করি।

```javascript
let username = "   Atiar   ";

console.log(username.trim());
```

Output:

```text
Atiar
```

এটা form handling-এ অনেক important।

```javascript
let email = "   atiar@gmail.com   ";

email = email.trim();

console.log(email);
```

Output:

```text
atiar@gmail.com
```

---

# 10. trimStart()

শুধু শুরু থেকে space remove:

```javascript
let text = "   Hello World   ";

console.log(text.trimStart());
```

Result:

```text
"Hello World   "
```

---

# 11. trimEnd()

শুধু শেষের space remove:

```javascript
let text = "   Hello World   ";

console.log(text.trimEnd());
```

Result:

```text
"   Hello World"
```

---

# 12. includes()

String-এর মধ্যে কোনো text আছে কিনা check করতে:

```javascript
let text = "I love JavaScript";

console.log(text.includes("JavaScript"));
```

Output:

```text
true
```

```javascript
console.log(text.includes("Python"));
```

Output:

```text
false
```

### Real-world example

```javascript
let email = "user@gmail.com";

if (email.includes("@")) {
    console.log("Valid email format");
}
```

---

# 13. startsWith()

String কোনো নির্দিষ্ট text দিয়ে শুরু হয়েছে কিনা:

```javascript
let url = "https://example.com";

console.log(url.startsWith("https"));
```

Output:

```text
true
```

```javascript
console.log(url.startsWith("http"));
```

Output:

```text
true
```

---

# 14. endsWith()

String কোনো নির্দিষ্ট text দিয়ে শেষ হয়েছে কিনা:

```javascript
let file = "profile.jpg";

console.log(file.endsWith(".jpg"));
```

Output:

```text
true
```

আর:

```javascript
console.log(file.endsWith(".png"));
```

Output:

```text
false
```

---

# 15. indexOf()

কোনো substring প্রথম কোথায় আছে সেটা জানতে:

```javascript
let text = "I love JavaScript";

console.log(text.indexOf("JavaScript"));
```

Output:

```text
7
```

কারণ:

```text
I love JavaScript
01234567890123456
      ↑
      7
```

যদি না থাকে:

```javascript
console.log(text.indexOf("Python"));
```

Output:

```text
-1
```

### তাই খুব important:

```javascript
if (text.indexOf("JavaScript") !== -1) {
    console.log("Found");
}
```

তবে modern code-এ simple existence check-এর জন্য `includes()` বেশি readable।

---

# 16. lastIndexOf()

একই text একাধিকবার থাকলে শেষ occurrence-এর index দেয়।

```javascript
let text = "hello hello hello";

console.log(text.lastIndexOf("hello"));
```

Output:

```text
12
```

---

# 17. search()

String-এর মধ্যে pattern search করতে:

```javascript
let text = "I love JavaScript";

console.log(text.search("JavaScript"));
```

Output:

```text
7
```

Regex-এর সাথেও ব্যবহার করা যায়:

```javascript
let text = "Hello 123";

console.log(text.search(/[0-9]/));
```

Output:

```text
6
```

---

# 18. slice()

String-এর একটি অংশ বের করতে `slice()` সবচেয়ে important methods-এর একটি।

```javascript
let text = "JavaScript";

console.log(text.slice(0, 4));
```

Output:

```text
Java
```

কারণ:

```text
J a v a S c r i p t
0 1 2 3 4 ...
```

`slice(0, 4)` মানে:

```text
start = 0
end = 4
```

End index included হয় না।

---

## Negative slice

```javascript
let text = "JavaScript";

console.log(text.slice(-6));
```

Output:

```text
Script
```

শেষের 6 characters।

---

# 19. substring()

```javascript
let text = "JavaScript";

console.log(text.substring(0, 4));
```

Output:

```text
Java
```

Basic use-এর ক্ষেত্রে `slice()` এবং `substring()` একই রকম মনে হতে পারে।

কিন্তু negative index-এর behavior আলাদা।

```javascript
let text = "JavaScript";

console.log(text.slice(-6));
```

Result:

```text
Script
```

কিন্তু:

```javascript
console.log(text.substring(-6));
```

negative value-কে `0` হিসেবে treat করে।

তাই সাধারণভাবে আমি recommend করব:

```javascript
slice()
```

---

# 20. replace()

String-এর একটি অংশ replace করতে:

```javascript
let text = "I love Python";

let result = text.replace("Python", "JavaScript");

console.log(result);
```

Output:

```text
I love JavaScript
```

---

# 21. replaceAll()

একাধিক occurrence replace করতে:

```javascript
let text = "apple apple apple";

let result = text.replaceAll("apple", "orange");

console.log(result);
```

Output:

```text
orange orange orange
```

---

# 22. split()

String-কে Array-তে convert করতে `split()` ব্যবহার করি।

```javascript
let text = "apple,banana,mango";

let fruits = text.split(",");

console.log(fruits);
```

Output:

```javascript
["apple", "banana", "mango"]
```

এটা খুব important method।

---

## Space দিয়ে split

```javascript
let text = "I love JavaScript";

let words = text.split(" ");

console.log(words);
```

Output:

```javascript
["I", "love", "JavaScript"]
```

---

# 23. String → Array → String

এটা খুব common pattern।

```javascript
let text = "apple,banana,mango";

let arr = text.split(",");

console.log(arr);
```

Output:

```text
["apple", "banana", "mango"]
```

আবার:

```javascript
let result = arr.join(",");
```

Output:

```text
apple,banana,mango
```

---

# 24. concat()

দুই বা তার বেশি String join করতে:

```javascript
let firstName = "Md.";
let lastName = "Atiar";

let fullName = firstName.concat(" ", lastName);

console.log(fullName);
```

Output:

```text
Md. Atiar
```

কিন্তু modern JavaScript-এ সাধারণত `+` অথবা template literal বেশি ব্যবহার করা হয়:

```javascript
let fullName = firstName + " " + lastName;
```

অথবা:

```javascript
let fullName = `${firstName} ${lastName}`;
```

---

# 25. repeat()

একটি String নির্দিষ্ট সংখ্যক বার repeat করতে:

```javascript
let text = "Hi ";

console.log(text.repeat(3));
```

Output:

```text
Hi Hi Hi
```

আরেকটি:

```javascript
console.log("*".repeat(10));
```

Output:

```text
**********
```

---

# 26. padStart()

String-এর শুরুতে character যোগ করে নির্দিষ্ট length তৈরি করে।

```javascript
let number = "5";

console.log(number.padStart(3, "0"));
```

Output:

```text
005
```

আর:

```javascript
let id = "25";

console.log(id.padStart(5, "0"));
```

Output:

```text
00025
```

---

# 27. padEnd()

শেষে character যোগ করে:

```javascript
let number = "5";

console.log(number.padEnd(3, "0"));
```

Output:

```text
500
```

---

# 28. String comparison

```javascript
let a = "apple";
let b = "banana";

console.log(a === b);
```

Output:

```text
false
```

```javascript
console.log(a === "apple");
```

Output:

```text
true
```

---

# 29. Case-sensitive comparison

JavaScript String comparison case-sensitive।

```javascript
console.log("hello" === "Hello");
```

Output:

```text
false
```

কারণ:

```text
h ≠ H
```

Case-insensitive comparison করতে:

```javascript
let a = "HELLO";
let b = "hello";

console.log(
    a.toLowerCase() === b.toLowerCase()
);
```

Output:

```text
true
```

---

# 30. Escape characters

String-এর মধ্যে special character লেখার জন্য `\` ব্যবহার করা হয়।

### New line

```javascript
let text = "Hello\nWorld";

console.log(text);
```

Output:

```text
Hello
World
```

### Tab

```javascript
let text = "Hello\tWorld";

console.log(text);
```

### Quote

```javascript
let text = "He said \"Hello\"";

console.log(text);
```

Output:

```text
He said "Hello"
```

---

# 31. Template literal

Modern JavaScript-এর খুব important feature।

```javascript
let name = "Atiar";
let age = 25;
let profession = "Developer";

let message = `
Name: ${name}
Age: ${age}
Profession: ${profession}
`;

console.log(message);
```

এটা React-এ অনেক ব্যবহার করবে।

---

# 32. String immutability

এটা খুব important concept।

String-এর individual character directly change করা যায় না।

```javascript
let name = "Atiar";

name[0] = "B";

console.log(name);
```

Result:

```text
Atiar
```

`A` পরিবর্তন হয়নি।

কারণ JavaScript String **immutable**।

নতুন String তৈরি করতে হবে:

```javascript
let name = "Atiar";

name = "B" + name.slice(1);

console.log(name);
```

Output:

```text
Btiar
```

---

# 33. String methods original String পরিবর্তন করে না

উদাহরণ:

```javascript
let name = "atiar";

let result = name.toUpperCase();

console.log(name);
console.log(result);
```

Output:

```text
atiar
ATIAR
```

Original:

```javascript
name
```

পরিবর্তন হয়নি।

---

# 34. String থেকে character Array

Spread operator ব্যবহার করা যায়:

```javascript
let name = "Atiar";

let chars = [...name];

console.log(chars);
```

Output:

```javascript
["A", "t", "i", "a", "r"]
```

---

# 35. String reverse করা

JavaScript-এ সরাসরি `reverse()` String-এর জন্য নেই।

তাই:

```javascript
let text = "hello";

let reversed = text
    .split("")
    .reverse()
    .join("");

console.log(reversed);
```

Output:

```text
olleh
```

Flow:

```text
"hello"

   ↓ split("")

["h", "e", "l", "l", "o"]

   ↓ reverse()

["o", "l", "l", "e", "h"]

   ↓ join("")

"olleh"
```

---

# 36. Practical Example — Username cleaning

ধরো user input দিয়েছে:

```javascript
let username = "   ATIAR   ";
```

আমরা চাই:

```text
atiar
```

তাহলে:

```javascript
username = username
    .trim()
    .toLowerCase();

console.log(username);
```

Output:

```text
atiar
```

---

# 37. Practical Example — Email validation basic

```javascript
let email = "  ATIAR@GMAIL.COM  ";

email = email.trim().toLowerCase();

if (email.includes("@")) {
    console.log("Email format looks valid");
} else {
    console.log("Invalid email");
}
```

এটা শুধু **basic check**, complete email validation নয়।

---

# 38. Practical Example — File extension

ধরো:

```javascript
let fileName = "profile.jpg";
```

Check:

```javascript
if (fileName.endsWith(".jpg")) {
    console.log("JPG image");
}
```

আর:

```javascript
if (
    fileName.endsWith(".jpg") ||
    fileName.endsWith(".png")
) {
    console.log("Image file");
}
```

---

# 39. Practical Example — Search

```javascript
let title = "Learn JavaScript String Methods";

let keyword = "javascript";

if (title.toLowerCase().includes(keyword.toLowerCase())) {
    console.log("Found");
}
```

Output:

```text
Found
```

এটা search/filter functionality-তে খুব useful।

---

# 40. সবচেয়ে গুরুত্বপূর্ণ String Methods

তোমার আগে এগুলো mastery করা উচিত:

| Method           | কাজ                    |
| ---------------- | ---------------------- |
| `.length`        | String length          |
| `[index]`        | Character access       |
| `.at()`          | Character access       |
| `.charAt()`      | Character access       |
| `.toUpperCase()` | Uppercase              |
| `.toLowerCase()` | Lowercase              |
| `.trim()`        | দুই পাশের space remove |
| `.includes()`    | Text আছে কিনা          |
| `.startsWith()`  | শুরু check             |
| `.endsWith()`    | শেষ check              |
| `.indexOf()`     | প্রথম position         |
| `.lastIndexOf()` | শেষ position           |
| `.slice()`       | String-এর অংশ নেওয়া    |
| `.substring()`   | String-এর অংশ নেওয়া    |
| `.replace()`     | Text replace           |
| `.replaceAll()`  | সব occurrence replace  |
| `.split()`       | String → Array         |
| `.concat()`      | String join            |
| `.repeat()`      | Repeat                 |
| `.padStart()`    | শুরুতে padding         |
| `.padEnd()`      | শেষে padding           |

### তোমার জন্য সবচেয়ে important mental model

String নিয়ে কাজ করার সময় সাধারণত এই ৫টা category মনে রাখবে:

```text
STRING
  │
  ├── Read
  │    ├── length
  │    ├── []
  │    └── at()
  │
  ├── Search
  │    ├── includes()
  │    ├── indexOf()
  │    ├── startsWith()
  │    └── endsWith()
  │
  ├── Modify
  │    ├── replace()
  │    ├── replaceAll()
  │    ├── trim()
  │    └── toUpperCase()
  │
  ├── Extract
  │    ├── slice()
  │    └── substring()
  │
  └── Convert
       ├── split()   → Array
       └── join()    → String
```

**Frontend/React-এর জন্য বিশেষভাবে** `trim()`, `toLowerCase()`, `includes()`, `startsWith()`, `endsWith()`, `split()`, `slice()`, `replace()`, `replaceAll()`, এবং template literals ভালোভাবে mastery করো।


----
todays JavaScript-এর **Conditional Statement** খুব গুরুত্বপূর্ণ, কারণ program-কে decision নিতে হয়—**“যদি এটা হয়, তাহলে এটা করো; না হলে অন্যটা করো।”**

# JavaScript Conditional Statements

ধরো:

```javascript
let age = 20;
```

আমরা চাই:

> যদি age 18 বা তার বেশি হয় → `"You can vote"`
> না হলে → `"You cannot vote"`

এখানেই Conditional Statement দরকার।

---

# 1. `if` Statement

সবচেয়ে basic conditional:

```javascript
if (condition) {
    // code
}
```

Example:

```javascript
let age = 20;

if (age >= 18) {
    console.log("You can vote");
}
```

Output:

```text
You can vote
```

কারণ:

```text
20 >= 18
```

এর result:

```javascript
true
```

তাই `if` block execute হয়েছে।

---

# 2. `if` কীভাবে কাজ করে?

```javascript
if (age >= 18) {
    console.log("You can vote");
}
```

Flow:

```text
          age >= 18
              |
        +-----+-----+
        |           |
      true        false
        |           |
      execute      skip
        |
   You can vote
```

অর্থাৎ `if` শুধু condition `true` হলে code execute করে।

---

# 3. `if...else`

যখন দুইটি possibility থাকে:

```javascript
if (condition) {
    // true হলে
} else {
    // false হলে
}
```

Example:

```javascript
let age = 15;

if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}
```

Output:

```text
Minor
```

কারণ:

```text
15 >= 18
```

→ `false`

তাই `else` execute হবে।

---

# 4. Real-world Example

Login system:

```javascript
let isLoggedIn = true;

if (isLoggedIn) {
    console.log("Welcome to dashboard");
} else {
    console.log("Please login first");
}
```

Output:

```text
Welcome to dashboard
```

Frontend/React-এ এই ধরনের condition প্রচুর ব্যবহার করবে।

---

# 5. `if...else if...else`

যখন একাধিক condition থাকে:

```javascript
if (condition1) {

} else if (condition2) {

} else if (condition3) {

} else {

}
```

Example:

```javascript
let marks = 75;

if (marks >= 80) {
    console.log("A+");
} else if (marks >= 70) {
    console.log("A");
} else if (marks >= 60) {
    console.log("A-");
} else if (marks >= 50) {
    console.log("B");
} else {
    console.log("Fail");
}
```

Output:

```text
A
```

কারণ:

```text
75 >= 80  → false
75 >= 70  → true
```

তাই `A` পাওয়ার পর JavaScript আর নিচের condition check করবে না।

---

# 6. Condition-এর Order খুব গুরুত্বপূর্ণ

এই code দেখো:

```javascript
let marks = 85;

if (marks >= 50) {
    console.log("Pass");
} else if (marks >= 80) {
    console.log("A+");
}
```

Output:

```text
Pass
```

কিন্তু আমরা চাইছিলাম `A+`।

কারণ প্রথম condition:

```javascript
marks >= 50
```

already `true`।

তাই সঠিক order:

```javascript
let marks = 85;

if (marks >= 80) {
    console.log("A+");
} else if (marks >= 70) {
    console.log("A");
} else if (marks >= 60) {
    console.log("A-");
} else if (marks >= 50) {
    console.log("B");
} else {
    console.log("Fail");
}
```

### Rule

**Specific / বড় condition আগে, general condition পরে।**

---

# 7. Comparison Operators

Conditional statement-এর ভিতরে comparison operator অনেক ব্যবহার করবে।

### `>` Greater than

```javascript
let age = 20;

if (age > 18) {
    console.log("Adult");
}
```

---

### `<` Less than

```javascript
let age = 15;

if (age < 18) {
    console.log("Minor");
}
```

---

### `>=` Greater than or equal

```javascript
let age = 18;

if (age >= 18) {
    console.log("Eligible");
}
```

---

### `<=` Less than or equal

```javascript
let age = 18;

if (age <= 18) {
    console.log("Eligible");
}
```

---

### `===` Strict equality

```javascript
let age = 18;

if (age === 18) {
    console.log("Age is 18");
}
```

---

### `!==` Not equal

```javascript
let age = 20;

if (age !== 18) {
    console.log("Age is not 18");
}
```

---

# 8. `==` vs `===`

এটা খুব গুরুত্বপূর্ণ।

```javascript
5 == "5"
```

Result:

```javascript
true
```

কারণ `==` type conversion করতে পারে।

কিন্তু:

```javascript
5 === "5"
```

Result:

```javascript
false
```

কারণ:

```text
5     → number
"5"   → string
```

তাই JavaScript development-এ সাধারণত:

```javascript
===
```

ব্যবহার করাই ভালো।

---

# 9. Logical AND `&&`

যখন **দুইটা condition-ই true** হতে হবে।

Example:

```javascript
let age = 25;
let hasNID = true;

if (age >= 18 && hasNID === true) {
    console.log("You are eligible");
}
```

দুইটা condition:

```text
age >= 18       → true
hasNID === true → true
```

তাই:

```text
true && true
```

→ `true`

---

## একটা false হলে

```javascript
let age = 25;
let hasNID = false;

if (age >= 18 && hasNID === true) {
    console.log("Eligible");
} else {
    console.log("Not eligible");
}
```

Output:

```text
Not eligible
```

কারণ:

```text
true && false
```

→ `false`

### মনে রাখবে

```text
&& = AND = সব condition true হতে হবে
```

---

# 10. Logical OR `||`

যখন **যেকোনো একটি condition true হলেই হবে।**

Example:

```javascript
let isAdmin = false;
let isModerator = true;

if (isAdmin || isModerator) {
    console.log("You can manage content");
}
```

এখানে:

```text
false || true
```

→ `true`

তাই code execute হবে।

### মনে রাখবে

```text
|| = OR = যেকোনো একটি true হলেই true
```

---

# 11. Logical NOT `!`

কোনো boolean value উল্টে দেয়।

```javascript
let isLoggedIn = false;

if (!isLoggedIn) {
    console.log("Please login");
}
```

এখানে:

```text
isLoggedIn = false

!false = true
```

তাই:

```text
Please login
```

---

# 12. AND + OR একসাথে

Example:

```javascript
let age = 25;
let isStudent = true;
let isEmployee = false;

if (age >= 18 && (isStudent || isEmployee)) {
    console.log("Eligible");
}
```

এখানে:

```text
age >= 18
```

→ `true`

এবং:

```text
isStudent || isEmployee
```

→ `true`

তাই:

```text
true && true
```

→ `true`

---

# 13. Nested `if`

একটি `if`-এর ভিতরে আরেকটি `if` থাকতে পারে।

```javascript
let isLoggedIn = true;
let isAdmin = true;

if (isLoggedIn) {

    if (isAdmin) {
        console.log("Admin Dashboard");
    }

}
```

Flow:

```text
Logged in?
   |
  Yes
   |
Admin?
   |
  Yes
   |
Admin Dashboard
```

তবে nested `if` বেশি ব্যবহার করলে code complicated হতে পারে।

অনেক ক্ষেত্রে `&&` দিয়ে সহজ করা যায়:

```javascript
if (isLoggedIn && isAdmin) {
    console.log("Admin Dashboard");
}
```

এটা cleaner।

---

# 14. Ternary Operator

ছোট `if...else`-এর জন্য **ternary operator** ব্যবহার করা যায়।

Syntax:

```javascript
condition ? trueValue : falseValue
```

Example:

```javascript
let age = 20;

let result = age >= 18
    ? "Adult"
    : "Minor";

console.log(result);
```

Output:

```text
Adult
```

Equivalent `if...else`:

```javascript
let age = 20;
let result;

if (age >= 18) {
    result = "Adult";
} else {
    result = "Minor";
}
```

### কখন ternary ব্যবহার করবে?

Simple condition:

```javascript
let isLoggedIn = true;

let message = isLoggedIn
    ? "Welcome"
    : "Please login";
```

কিন্তু complex logic হলে normal `if...else` ব্যবহার করো।

---

# 15. Multiple ternary — Avoid করা ভালো

এটা technically possible:

```javascript
let marks = 75;

let grade =
    marks >= 80 ? "A+" :
    marks >= 70 ? "A" :
    marks >= 60 ? "A-" :
    "Fail";
```

কাজ করবে, কিন্তু beginner হিসেবে readability-এর জন্য `if...else if` বেশি ভালো:

```javascript
if (marks >= 80) {
    grade = "A+";
} else if (marks >= 70) {
    grade = "A";
} else if (marks >= 60) {
    grade = "A-";
} else {
    grade = "Fail";
}
```

---

# 16. Truthy এবং Falsy

JavaScript-এ সব value strictly `true` বা `false` না হলেও condition-এর মধ্যে ব্যবহার করা যায়।

### Falsy values

সবচেয়ে গুরুত্বপূর্ণ falsy values:

```javascript
false
0
""
null
undefined
NaN
```

Example:

```javascript
let username = "";

if (username) {
    console.log("Username exists");
} else {
    console.log("Username is empty");
}
```

Output:

```text
Username is empty
```

কারণ:

```text
"" → falsy
```

---

# 17. Truthy Example

```javascript
let username = "Atiar";

if (username) {
    console.log("Username exists");
}
```

Output:

```text
Username exists
```

কারণ non-empty string truthy।

---

# 18. `null` এবং `undefined`

```javascript
let user = null;

if (user) {
    console.log("User exists");
} else {
    console.log("No user");
}
```

Output:

```text
No user
```

আর:

```javascript
let user;

if (user) {
    console.log("User exists");
} else {
    console.log("No user");
}
```

এখানে `user` হলো `undefined`, তাই `else` execute হবে।

---

# 19. `switch` Statement

যখন একটি variable-এর অনেকগুলো fixed value check করতে হয়, `switch` useful।

Syntax:

```javascript
switch (value) {

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

Example:

```javascript
let day = "Sunday";

switch (day) {

    case "Saturday":
        console.log("Weekend");
        break;

    case "Sunday":
        console.log("Weekend");
        break;

    case "Monday":
        console.log("Working day");
        break;

    default:
        console.log("Unknown day");
}
```

Output:

```text
Weekend
```

---

# 20. `break` কেন দরকার?

```javascript
let day = "Sunday";

switch (day) {

    case "Sunday":
        console.log("Sunday");
        break;

    case "Monday":
        console.log("Monday");
        break;

    default:
        console.log("Unknown");
}
```

`break` switch থেকে বের হয়ে যায়।

`break` না দিলে পরের case-ও execute হতে পারে।

---

# 21. Multiple case একসাথে

যদি Saturday এবং Sunday একই result দেয়:

```javascript
let day = "Sunday";

switch (day) {

    case "Saturday":
    case "Sunday":
        console.log("Weekend");
        break;

    default:
        console.log("Working day");
}
```

এটা useful pattern।

---

# 22. `if` নাকি `switch`?

### `if` ব্যবহার করো যখন:

Conditions complex:

```javascript
if (age >= 18 && hasNID) {
    console.log("Eligible");
}
```

বা:

```javascript
if (marks >= 80) {
    ...
} else if (marks >= 70) {
    ...
}
```

### `switch` ব্যবহার করো যখন:

একটি variable-এর fixed values:

```javascript
switch (role) {
    case "admin":
    case "seller":
    case "buyer":
}
```

---

# 23. Real-world Login Example

```javascript
let email = "atiar@gmail.com";
let password = "123456";

let correctEmail = "atiar@gmail.com";
let correctPassword = "123456";

if (
    email === correctEmail &&
    password === correctPassword
) {
    console.log("Login successful");
} else {
    console.log("Invalid email or password");
}
```

এখানে:

```text
email correct?
      +
password correct?
      ↓
দুটোই true
      ↓
Login successful
```

---

# 24. Real-world E-commerce Example

ধরো product-এর stock:

```javascript
let stock = 5;
let price = 1000;

if (stock === 0) {
    console.log("Out of stock");

} else if (price < 500) {
    console.log("Budget product");

} else {
    console.log("Product available");
}
```

Output:

```text
Product available
```

---

# 25. React-এ Conditional Rendering

তুমি যেহেতু React শিখছো, এটা খুব important।

```javascript
let isLoggedIn = true;
```

React JSX-এ:

```jsx
{isLoggedIn && <h1>Welcome back!</h1>}
```

`isLoggedIn` true হলে:

```text
Welcome back!
```

দেখাবে।

---

### Login / Logout

```jsx
{isLoggedIn ? (
    <button>Logout</button>
) : (
    <button>Login</button>
)}
```

এটা React-এ খুব common pattern।

---

# 26. React Example — Loading

```jsx
{isLoading ? (
    <p>Loading...</p>
) : (
    <p>Data loaded</p>
)}
```

এটা API call-এর সময় প্রচুর ব্যবহার করবে।

---

# 27. Conditional Statement-এর পুরো structure

তোমার মাথায় এই structure রাখো:

```text
Conditional Statements
│
├── if
│
├── if...else
│
├── if...else if...else
│
├── nested if
│
├── switch
│
└── ternary operator
```

আর condition তৈরি করার জন্য:

```text
Comparison
│
├── >
├── <
├── >=
├── <=
├── ===
└── !==

Logical
│
├── &&
├── ||
└── !
```

---

# সবচেয়ে গুরুত্বপূর্ণ ৫টি Pattern

### Pattern 1 — Simple condition

```javascript
if (age >= 18) {
    console.log("Adult");
}
```

### Pattern 2 — True/False

```javascript
if (age >= 18) {
    console.log("Adult");
} else {
    console.log("Minor");
}
```

### Pattern 3 — Multiple conditions

```javascript
if (marks >= 80) {
    console.log("A+");
} else if (marks >= 70) {
    console.log("A");
} else {
    console.log("Below A");
}
```

### Pattern 4 — AND/OR

```javascript
if (isLoggedIn && isAdmin) {
    console.log("Admin");
}
```

### Pattern 5 — Short condition

```javascript
let message = isLoggedIn
    ? "Welcome"
    : "Please login";
```

**Learning order:** আগে `if → if/else → else if → comparison operators → && / || / ! → truthy/falsy → ternary → switch → React conditional rendering` এই order-এ practice করলে conditional statement খুব strong হবে।

---
# Understanding Truthy & Falsy Values in JavaScript

JavaScript-এর conditional statement বুঝতে হলে **Truthy & Falsy** খুব ভালোভাবে বুঝতে হবে।

মূল idea:

> JavaScript যখন কোনো value-কে `if`, `while`, `&&`, `||` ইত্যাদির মধ্যে দেখে, তখন সেই value-কে Boolean হিসেবে evaluate করে।

অর্থাৎ:

```javascript
if (value) {
    // value truthy হলে
}
```

আর:

```javascript
if (!value) {
    // value falsy হলে
}
```

---

# 1. Truthy কী?

যে value Boolean context-এ গেলে `true` হিসেবে behave করে, তাকে **truthy value** বলে।

Example:

```javascript
let name = "Atiar";

if (name) {
    console.log("Name exists");
}
```

Output:

```text
Name exists
```

কারণ:

```javascript
Boolean("Atiar")
```

result:

```javascript
true
```

---

# 2. Falsy কী?

যে value Boolean context-এ গেলে `false` হিসেবে behave করে, তাকে **falsy value** বলে।

JavaScript-এর সবচেয়ে গুরুত্বপূর্ণ falsy values:

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

এগুলো মনে রাখা খুব important।

---

# 3. Boolean() দিয়ে check করা

কোনো value truthy নাকি falsy সরাসরি দেখতে:

```javascript
Boolean(value)
```

Example:

```javascript
console.log(Boolean("Hello"));
```

Output:

```text
true
```

```javascript
console.log(Boolean(""));
```

Output:

```text
false
```

---

# 4. Falsy Value: `false`

```javascript
let value = false;

console.log(Boolean(value));
```

Output:

```text
false
```

Conditional:

```javascript
if (value) {
    console.log("True");
} else {
    console.log("False");
}
```

Output:

```text
False
```

---

# 5. Falsy Value: `0`

```javascript
let age = 0;

if (age) {
    console.log("Age exists");
} else {
    console.log("Age is zero");
}
```

Output:

```text
Age is zero
```

কারণ:

```javascript
Boolean(0)
```

→ `false`

### কিন্তু এখানে একটা practical problem আছে

ধরো:

```javascript
let quantity = 0;

if (quantity) {
    console.log("Quantity:", quantity);
}
```

কিছুই print হবে না।

কারণ `0` falsy।

তাই যদি তোমার specifically `0` valid কিনা check করতে হয়, তখন:

```javascript
if (quantity === 0) {
    console.log("Quantity is zero");
}
```

ব্যবহার করা উচিত।

---

# 6. Falsy Value: Empty String `""`

```javascript
let username = "";

if (username) {
    console.log("Username provided");
} else {
    console.log("Username is empty");
}
```

Output:

```text
Username is empty
```

কারণ:

```javascript
Boolean("")
```

→ `false`

এটা form validation-এ অনেক ব্যবহার হয়।

---

# 7. Falsy Value: `null`

`null` সাধারণত বোঝায়:

> এখানে কোনো value নেই / intentionally empty।

```javascript
let user = null;

if (user) {
    console.log("User exists");
} else {
    console.log("No user");
}
```

Output:

```text
No user
```

---

# 8. Falsy Value: `undefined`

```javascript
let username;

console.log(username);
```

Output:

```text
undefined
```

এবং:

```javascript
if (username) {
    console.log("Username exists");
} else {
    console.log("Username does not exist");
}
```

Output:

```text
Username does not exist
```

---

# 9. Falsy Value: `NaN`

`NaN` = **Not a Number**

Example:

```javascript
let result = Number("hello");

console.log(result);
```

Output:

```text
NaN
```

এটা falsy:

```javascript
console.log(Boolean(NaN));
```

Output:

```text
false
```

---

# 10. Empty Array `[]` কি Falsy?

এখানে beginner-রা সবচেয়ে বেশি ভুল করে।

```javascript
let arr = [];

if (arr) {
    console.log("Truthy");
} else {
    console.log("Falsy");
}
```

Output:

```text
Truthy
```

### কেন?

কারণ JavaScript-এ:

```javascript
Boolean([])
```

→ `true`

যদিও Array empty।

---

# 11. Empty Object `{}` কি Falsy?

এটাও **truthy**।

```javascript
let user = {};

if (user) {
    console.log("Truthy");
}
```

Output:

```text
Truthy
```

কারণ:

```javascript
Boolean({})
```

→ `true`

---

# 12. সবচেয়ে গুরুত্বপূর্ণ বিষয়

এগুলো:

```javascript
[]
{}
```

**truthy**

কিন্তু:

```javascript
""
```

**falsy**

অর্থাৎ:

```text
""      → false
" "     → true
"hello" → true

[]      → true
{}      → true

0       → false
1       → true
-1      → true
```

---

# 13. Empty String vs Space

এটা খুব important:

```javascript
console.log(Boolean(""));
```

→ `false`

কিন্তু:

```javascript
console.log(Boolean(" "));
```

→ `true`

কারণ `" "`-এর মধ্যে একটি space character আছে।

তাই form validation-এ:

```javascript
let username = "   ";
```

শুধু:

```javascript
if (username) {
}
```

ব্যবহার করলে সমস্যা হতে পারে।

বরং:

```javascript
if (username.trim()) {
    console.log("Username exists");
} else {
    console.log("Username is empty");
}
```

এটা ভালো।

---

# 14. Truthy Numbers

শুধু `0` falsy।

```javascript
Boolean(1);       // true
Boolean(10);      // true
Boolean(-1);      // true
Boolean(1000);    // true
```

অর্থাৎ:

```text
0       → false
1       → true
-1      → true
100     → true
```

---

# 15. Truthy Strings

Empty string ছাড়া সাধারণত string truthy।

```javascript
Boolean("Hello");   // true
Boolean("0");       // true
Boolean("false");   // true
Boolean(" ");       // true
```

খেয়াল করো:

```javascript
Boolean("false")
```

→ `true`

কারণ `"false"` একটি **non-empty string**।

এটা Boolean `false` না।

```javascript
false       // boolean
"false"     // string
```

দুটো completely different।

---

# 16. `"0"` বনাম `0`

এটাও খুব important:

```javascript
Boolean(0);
```

→ `false`

কিন্তু:

```javascript
Boolean("0");
```

→ `true`

কারণ:

```text
0     → number
"0"   → non-empty string
```

---

# 17. `if`-এ Truthy/Falsy

```javascript
let username = "Atiar";

if (username) {
    console.log("Logged in");
}
```

JavaScript internally প্রায় এমনভাবে দেখে:

```javascript
if (Boolean(username)) {
}
```

যেহেতু:

```javascript
Boolean("Atiar") === true
```

তাই block execute হয়।

---

# 18. `!` দিয়ে উল্টে দেওয়া

`!` truthy/falsy-এর opposite দেয়।

```javascript
let username = "";

console.log(!username);
```

Output:

```text
true
```

কারণ:

```text
username = ""
Boolean("") = false
!false = true
```

আর:

```javascript
let username = "Atiar";

console.log(!username);
```

Output:

```text
false
```

---

# 19. Double NOT `!!`

`!!` কোনো value-কে actual Boolean-এ convert করার একটি common technique।

```javascript
let username = "Atiar";

console.log(!!username);
```

Output:

```text
true
```

আর:

```javascript
let username = "";

console.log(!!username);
```

Output:

```text
false
```

Conceptually:

```text
!!value
   ↓
Boolean(value)
```

---

# 20. `&&` এর সাথে Truthy/Falsy

এটা খুব important।

```javascript
let username = "Atiar";

console.log(username && "Welcome");
```

Output:

```text
Welcome
```

কারণ:

```text
"Atiar" → truthy
```

তাই second value evaluate হয়েছে।

আর:

```javascript
let username = "";

console.log(username && "Welcome");
```

Output:

```text
""
```

কারণ প্রথম value falsy হওয়ায় JavaScript সেখানেই থেমে যায়।

এটাকে **short-circuit evaluation** বলে।

---

# 21. React-এ `&&` খুব common

React-এ:

```jsx
{isLoggedIn && <Dashboard />}
```

যদি:

```javascript
isLoggedIn = true
```

তাহলে:

```jsx
<Dashboard />
```

render হবে।

যদি:

```javascript
isLoggedIn = false
```

তাহলে Dashboard render হবে না।

---

# 22. `||` এর সাথে Truthy/Falsy

`||` সাধারণত প্রথম truthy value খুঁজে।

```javascript
let username = "";

let displayName = username || "Guest";

console.log(displayName);
```

Output:

```text
Guest
```

কারণ:

```text
username = ""
```

falsy।

তাই `"Guest"` নেওয়া হয়েছে।

---

আর:

```javascript
let username = "Atiar";

let displayName = username || "Guest";

console.log(displayName);
```

Output:

```text
Atiar
```

কারণ `"Atiar"` truthy।

---

# 23. Default value-এর জন্য `||`

খুব common pattern:

```javascript
let name = userName || "Guest";
```

মানে:

> `userName` truthy হলে সেটা নাও, না হলে `"Guest"` নাও।

---

# 24. কিন্তু `||`-এর একটা সমস্যা আছে

ধরো:

```javascript
let quantity = 0;

let result = quantity || 10;

console.log(result);
```

Output:

```text
10
```

কিন্তু হয়তো তুমি চেয়েছিলে `0`-ই valid value।

এখানে `||` সমস্যার কারণ:

```text
0 = falsy
```

এই situation-এ `??` অনেক useful।

---

# 25. `??` Nullish Coalescing

`??` শুধু `null` এবং `undefined` check করে।

```javascript
let quantity = 0;

let result = quantity ?? 10;

console.log(result);
```

Output:

```text
0
```

কারণ `0` null বা undefined নয়।

তুলনা:

```javascript
0 || 10
```

→ `10`

কিন্তু:

```javascript
0 ?? 10
```

→ `0`

---

# 26. `||` vs `??`

মনে রাখো:

```text
|| 
↓
Falsy value check করে
```

যেখানে:

```text
false
0
""
null
undefined
NaN
```

ইত্যাদি সমস্যা করতে পারে।

আর:

```text
??
↓
শুধু null / undefined check করে
```

---

# 27. Practical API Example

ধরো API থেকে user এসেছে:

```javascript
let user = {
    name: "Atiar"
};
```

তুমি লিখলে:

```javascript
console.log(user.name || "Guest");
```

Output:

```text
Atiar
```

যদি:

```javascript
let user = {
    name: ""
};
```

তাহলে:

```javascript
console.log(user.name || "Guest");
```

Output:

```text
Guest
```

আর null/undefined ছাড়া অন্য falsy value preserve করতে চাইলে:

```javascript
console.log(user.name ?? "Guest");
```

---

# 28. Truthy/Falsy মনে রাখার সবচেয়ে সহজ নিয়ম

### Falsy

এই list মুখস্থ করো:

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

### Almost everything else → Truthy

বিশেষ করে:

```javascript
"hello"   // truthy
"0"       // truthy
"false"   // truthy
" "       // truthy
[]        // truthy
{}        // truthy
1         // truthy
-1        // truthy
```

---

# 29. Quick Practice

প্রতিটির output predict করো:

```javascript
console.log(Boolean(false));
console.log(Boolean(0));
console.log(Boolean(""));
console.log(Boolean("Hello"));
console.log(Boolean("0"));
console.log(Boolean([]));
console.log(Boolean({}));
console.log(Boolean(null));
console.log(Boolean(undefined));
console.log(Boolean(NaN));
```

Expected:

```text
false
false
false
true
true
true
true
false
false
false
```

---

# 30. সবচেয়ে গুরুত্বপূর্ণ Real-world Patterns

### Form validation

```javascript
if (!username.trim()) {
    console.log("Username is required");
}
```

### Login check

```javascript
if (user) {
    console.log("User logged in");
}
```

### React conditional rendering

```jsx
{user && <Profile />}
```

### Default value

```javascript
let name = username || "Guest";
```

### Null/undefined default

```javascript
let name = username ?? "Guest";
```

### Convert to Boolean

```javascript
let isValid = !!value;
```

---

## 🧠 Final Mental Model

```text
                JavaScript Value
                       |
                Boolean(value)
                       |
             +---------+---------+
             |                   |
          Truthy               Falsy
             |                   |
          true                 false
             |                   |
      if block runs       if block skipped
```

সবচেয়ে important distinction:

```text
""       → falsy
" "      → truthy

0        → falsy
"0"      → truthy

false    → falsy
"false"  → truthy

null     → falsy
undefined→ falsy

[]       → truthy
{}       → truthy
```

**এগুলো ভালোভাবে বুঝে গেলে `if`, `&&`, `||`, `!`, React conditional rendering এবং পরে `??` অনেক সহজ হয়ে যাবে।**

---


# JavaScript Functions & Reusable Code

JavaScript-এ **Function** হলো এমন একটি reusable block of code, যেটা নির্দিষ্ট কাজ করার জন্য তৈরি করা হয়।

সহজভাবে:

> **একই code বারবার না লিখে, একবার function বানিয়ে প্রয়োজন অনুযায়ী অনেকবার ব্যবহার করা।**

---

# 1. কেন Function দরকার?

ধরো তোমাকে ৩ জনকে greeting দিতে হবে:

```javascript
console.log("Hello Atiar");
console.log("Hello Rahim");
console.log("Hello Karim");
```

এখানে একই logic বারবার লিখছি।

Function ব্যবহার করলে:

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}
```

এখন:

```javascript
greet("Atiar");
greet("Rahim");
greet("Karim");
```

Output:

```text
Hello Atiar
Hello Rahim
Hello Karim
```

এটাই **reusable code**।

---

# 2. Basic Function Syntax

```javascript
function functionName() {
    // code
}
```

Example:

```javascript
function sayHello() {
    console.log("Hello World");
}
```

কিন্তু function তৈরি করলেই code execute হয় না।

Function **call/invoke** করতে হবে:

```javascript
sayHello();
```

Output:

```text
Hello World
```

---

# 3. Function Declaration

এটাকে বলা হয় **Function Declaration**:

```javascript
function greet() {
    console.log("Hello");
}
```

তারপর call:

```javascript
greet();
```

---

# 4. Function Parameter

Function-এ বাইরে থেকে data পাঠানোর জন্য parameter ব্যবহার করি।

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}
```

এখানে:

```javascript
name
```

হলো **parameter**।

Call করার সময়:

```javascript
greet("Atiar");
```

এখানে:

```text
"Atiar"
```

হলো **argument**।

### Difference

```text
Parameter → function তৈরি করার সময়

Argument  → function call করার সময়
```

Example:

```javascript
function add(a, b) {
    console.log(a + b);
}

add(10, 20);
```

এখানে:

```text
a, b       → parameters
10, 20     → arguments
```

Output:

```text
30
```

---

# 5. Multiple Parameters

```javascript
function introduce(name, age, profession) {
    console.log(
        `My name is ${name}. I am ${age} years old. I am a ${profession}.`
    );
}

introduce("Atiar", 25, "Developer");
```

Output:

```text
My name is Atiar. I am 25 years old. I am a Developer.
```

---

# 6. `return`

Function-এর সবচেয়ে important concept হলো `return`।

```javascript
function add(a, b) {
    return a + b;
}
```

এখন:

```javascript
let result = add(10, 20);

console.log(result);
```

Output:

```text
30
```

### `return` কী করে?

Function থেকে result বাইরে পাঠায়।

```text
10, 20
  ↓
add()
  ↓
30
  ↓
result
```

---

# 7. `console.log()` vs `return`

এটা খুব ভালোভাবে বুঝতে হবে।

### `console.log()`

```javascript
function add(a, b) {
    console.log(a + b);
}

let result = add(10, 20);

console.log(result);
```

Output:

```text
30
undefined
```

কারণ function কিছু return করেনি।

---

### `return`

```javascript
function add(a, b) {
    return a + b;
}

let result = add(10, 20);

console.log(result);
```

Output:

```text
30
```

### সহজভাবে

```text
console.log()
→ screen-এ দেখায়

return
→ function থেকে value ফেরত দেয়
```

Reusable function-এর ক্ষেত্রে `return` অত্যন্ত important।

---

# 8. Return-এর পরে Code Execute হয় না

```javascript
function test() {
    return "Hello";

    console.log("World");
}
```

এখানে:

```javascript
console.log("World");
```

execute হবে না।

কারণ:

```text
return
 ↓
function শেষ
```

---

# 9. Function দিয়ে Calculation

```javascript
function calculateArea(width, height) {
    return width * height;
}

let area = calculateArea(10, 5);

console.log(area);
```

Output:

```text
50
```

এখন অন্য value:

```javascript
calculateArea(20, 10);
```

Output:

```text
200
```

একই logic reusable হয়েছে।

---

# 10. Default Parameter

কখনো argument না দিলে default value ব্যবহার করতে পারো।

```javascript
function greet(name = "Guest") {
    return `Hello ${name}`;
}
```

Call:

```javascript
console.log(greet());
```

Output:

```text
Hello Guest
```

আবার:

```javascript
console.log(greet("Atiar"));
```

Output:

```text
Hello Atiar
```

---

# 11. Multiple Default Parameters

```javascript
function createUser(
    name = "Guest",
    age = 18
) {
    return `Name: ${name}, Age: ${age}`;
}
```

```javascript
console.log(createUser());
```

Output:

```text
Name: Guest, Age: 18
```

---

# 12. Function Expression

Function variable-এর মধ্যে store করা যায়।

```javascript
const greet = function () {
    console.log("Hello");
};
```

Call:

```javascript
greet();
```

এটাকে **Function Expression** বলে।

---

# 13. Function Expression with Parameters

```javascript
const add = function (a, b) {
    return a + b;
};

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 14. Arrow Function

Modern JavaScript-এ সবচেয়ে বেশি ব্যবহার করবে **Arrow Function**।

Basic:

```javascript
const greet = () => {
    console.log("Hello");
};
```

Call:

```javascript
greet();
```

---

# 15. Arrow Function with Parameter

```javascript
const greet = (name) => {
    console.log(`Hello ${name}`);
};

greet("Atiar");
```

Output:

```text
Hello Atiar
```

একটি parameter হলে parentheses optional:

```javascript
const greet = name => {
    console.log(`Hello ${name}`);
};
```

---

# 16. Arrow Function with Multiple Parameters

```javascript
const add = (a, b) => {
    return a + b;
};

console.log(add(10, 20));
```

Output:

```text
30
```

---

# 17. Implicit Return

Arrow function-এর খুব useful feature।

এটা:

```javascript
const add = (a, b) => {
    return a + b;
};
```

short করে:

```javascript
const add = (a, b) => a + b;
```

এটাকে **implicit return** বলে।

```javascript
console.log(add(10, 20));
```

Output:

```text
30
```

---

# 18. Function কী Return করতে পারে?

Function শুধু number return করবে এমন নয়।

### String

```javascript
function getName() {
    return "Atiar";
}
```

### Boolean

```javascript
function isAdult(age) {
    return age >= 18;
}
```

### Array

```javascript
function getFruits() {
    return ["Apple", "Mango", "Banana"];
}
```

### Object

```javascript
function getUser() {
    return {
        name: "Atiar",
        age: 25
    };
}
```

---

# 19. Function Returning Object

```javascript
function createUser(name, age) {
    return {
        name: name,
        age: age
    };
}

const user = createUser("Atiar", 25);

console.log(user);
```

Output:

```javascript
{
    name: "Atiar",
    age: 25
}
```

Modern JavaScript-এ shorthand:

```javascript
function createUser(name, age) {
    return {
        name,
        age
    };
}
```

---

# 20. Function Calling Another Function

Function-এর ভিতর অন্য function call করা যায়।

```javascript
function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}

function calculate(a, b) {
    let sum = add(a, b);
    let product = multiply(a, b);

    return {
        sum,
        product
    };
}

console.log(calculate(10, 5));
```

Output:

```javascript
{
    sum: 15,
    product: 50
}
```

এভাবে বড় application-কে ছোট ছোট reusable function-এ ভাগ করা যায়।

---

# 21. Function Scope

Function-এর ভিতরের variable বাইরে থেকে access করা যায় না।

```javascript
function test() {
    let message = "Hello";

    console.log(message);
}

test();
```

কিন্তু:

```javascript
console.log(message);
```

করলে error হবে।

কারণ `message` function-এর **local variable**।

---

# 22. Global vs Local Variable

```javascript
let name = "Atiar";

function greet() {
    let message = "Hello";

    console.log(name);
    console.log(message);
}
```

এখানে:

```text
name
→ global scope

message
→ function/local scope
```

---

# 23. Function-এর ভিতরে বাইরে একই নাম

```javascript
let name = "Atiar";

function test() {
    let name = "Rahim";

    console.log(name);
}

test();

console.log(name);
```

Output:

```text
Rahim
Atiar
```

Function-এর ভিতরের `name` local variable।

---

# 24. Function as a Value

JavaScript-এ function একটি value-এর মতো ব্যবহার করা যায়।

```javascript
function greet() {
    console.log("Hello");
}

const myFunction = greet;

myFunction();
```

Output:

```text
Hello
```

খেয়াল করো:

```javascript
const myFunction = greet;
```

এখানে `()` নেই।

কারণ আমরা function **assign** করছি।

---

# 25. Callback Function

Function-কে অন্য function-এর argument হিসেবে পাঠানো যায়।

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}

function processUser(callback) {
    callback("Atiar");
}

processUser(greet);
```

Output:

```text
Hello Atiar
```

এখানে:

```javascript
greet
```

হলো callback function।

এটা JavaScript-এর খুব important concept।

---

# 26. `setTimeout()` Example

```javascript
setTimeout(() => {
    console.log("Hello after 2 seconds");
}, 2000);
```

এখানে:

```javascript
() => {
    console.log("Hello after 2 seconds");
}
```

একটি callback function।

---

# 27. Array Methods + Functions

Function শেখার পর Array methods অনেক সহজ হবে।

```javascript
let numbers = [1, 2, 3, 4, 5];

let result = numbers.map(function (number) {
    return number * 2;
});

console.log(result);
```

Output:

```javascript
[2, 4, 6, 8, 10]
```

Arrow function দিয়ে:

```javascript
let result = numbers.map(number => number * 2);
```

এটাই modern JavaScript style।

---

# 28. Reusable Validation Function

ধরো বারবার age check করতে হবে:

```javascript
function isAdult(age) {
    return age >= 18;
}
```

এখন:

```javascript
console.log(isAdult(20));
console.log(isAdult(15));
console.log(isAdult(30));
```

Output:

```text
true
false
true
```

এটাই reusable code।

---

# 29. Reusable Email Validation

Basic example:

```javascript
function isValidEmail(email) {
    return email.includes("@");
}

console.log(isValidEmail("atiar@gmail.com"));
console.log(isValidEmail("atiargmail.com"));
```

Output:

```text
true
false
```

---

# 30. Function Composition

একটা function-এর result আরেকটা function-এ পাঠানো যায়।

```javascript
function add(a, b) {
    return a + b;
}

function double(number) {
    return number * 2;
}

let result = double(add(10, 20));

console.log(result);
```

Flow:

```text
add(10, 20)
     ↓
    30
     ↓
double(30)
     ↓
    60
```

Output:

```text
60
```

---

# 31. Pure Function

একটি function যদি একই input দিলে সবসময় একই output দেয় এবং বাইরের data পরিবর্তন না করে, তাকে সাধারণভাবে **pure function** বলা হয়।

```javascript
function add(a, b) {
    return a + b;
}
```

```text
add(2, 3) → 5
add(2, 3) → 5
add(2, 3) → 5
```

এটা predictable।

---

# 32. Impure Function

যদি function বাইরের state/data-এর ওপর depend করে বা পরিবর্তন করে:

```javascript
let count = 0;

function increase() {
    count++;
}
```

এখানে function বাইরের `count` পরিবর্তন করছে।

এটা pure function নয়।

React শেখার সময় pure function concept অনেক কাজে আসবে।

---

# 33. Real-world E-commerce Example

ধরো product price calculate করতে হবে:

```javascript
function calculateDiscount(price, discount) {
    return price - (price * discount / 100);
}
```

Use:

```javascript
let finalPrice = calculateDiscount(1000, 20);

console.log(finalPrice);
```

Output:

```text
800
```

এখন:

```javascript
calculateDiscount(5000, 15);
```

Output:

```text
4250
```

একই business logic বারবার ব্যবহার করা যাচ্ছে।

---

# 34. Function Naming

Function-এর নাম দেখে function কী করে বোঝা উচিত।

❌ Bad:

```javascript
function x(a, b) {
    return a + b;
}
```

Better:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}
```

আরও examples:

```javascript
getUser()
createUser()
updateUser()
deleteUser()
calculateTotal()
validateEmail()
isLoggedIn()
formatPrice()
fetchProducts()
```

Common convention:

```text
get...
create...
update...
delete...
calculate...
validate...
check...
is...
has...
```

---

# 35. Function ছোট রাখো

❌ অনেক কাজ এক function-এ:

```javascript
function processOrder() {
    // validate user
    // calculate price
    // calculate tax
    // create invoice
    // send email
    // update stock
}
```

Better:

```javascript
function validateOrder() {
}

function calculateTotal() {
}

function calculateTax() {
}

function createInvoice() {
}

function sendEmail() {
}

function updateStock() {
}
```

তারপর:

```javascript
function processOrder() {
    validateOrder();
    calculateTotal();
    calculateTax();
    createInvoice();
    sendEmail();
    updateStock();
}
```

এতে code maintain করা সহজ হয়।

---

# 36. Function-এর তিনটি প্রধান ধরন

তোমার এখন এগুলো ভালোভাবে বুঝতে হবে:

### Function Declaration

```javascript
function add(a, b) {
    return a + b;
}
```

### Function Expression

```javascript
const add = function (a, b) {
    return a + b;
};
```

### Arrow Function

```javascript
const add = (a, b) => {
    return a + b;
};
```

Short version:

```javascript
const add = (a, b) => a + b;
```

---

# 37. কোনটা কখন ব্যবহার করবে?

Modern JavaScript/React-এ সাধারণত:

```javascript
const add = (a, b) => a + b;
```

অনেক ব্যবহার করবে।

তবে function declaration-ও খুব common:

```javascript
function calculateTotal(price, quantity) {
    return price * quantity;
}
```

React code-এ arrow functions প্রচুর দেখবে:

```javascript
const handleClick = () => {
    console.log("Clicked");
};
```

---

# 🧠 Final Mental Model

Function-কে এভাবে ভাবো:

```text
             INPUT
          /          \
       arg1          arg2
         \             /
          \           /
           FUNCTION
               |
             LOGIC
               |
             RETURN
               |
             OUTPUT
```

Example:

```javascript
const calculateTotal = (price, quantity) => {
    return price * quantity;
};

const total = calculateTotal(500, 3);

console.log(total);
```

Flow:

```text
price = 500
quantity = 3
      ↓
calculateTotal()
      ↓
500 × 3
      ↓
1500
      ↓
total
```

### এখন Function mastery-এর জন্য এই sequence follow করো:

```text
1. Function Declaration
        ↓
2. Function Call
        ↓
3. Parameters & Arguments
        ↓
4. return
        ↓
5. Default Parameters
        ↓
6. Function Expression
        ↓
7. Arrow Function
        ↓
8. Implicit Return
        ↓
9. Scope
        ↓
10. Callback Function
        ↓
11. Higher-order Functions
        ↓
12. Pure Functions
        ↓
13. Reusable Business Logic
```

**সবচেয়ে গুরুত্বপূর্ণ:** Function শুধু syntax হিসেবে শিখবে না। প্রতিবার ভাববে—**“এই logic কি আমি অন্য জায়গায় আবার ব্যবহার করতে পারব? পারলে এটাকে function বানানো উচিত।”**



---
# JavaScript Scope & Variable Accessibility

JavaScript-এর **Scope** বুঝতে পারলে তুমি পরিষ্কারভাবে বুঝতে পারবে:

> **কোন variable কোথা থেকে access করা যাবে এবং কোথা থেকে করা যাবে না।**

এটা Function, `let`, `const`, `var`, React component, callback—সব জায়গাতেই গুরুত্বপূর্ণ।

---

# 1. Scope কী?

**Scope = কোনো variable কোথায় accessible, তার boundary।**

Example:

```javascript
let name = "Atiar";

function greet() {
    console.log(name);
}
```

এখানে `name` function-এর বাইরে declare করা হয়েছে, কিন্তু function-এর ভিতর থেকে access করা যাচ্ছে।

কারণ `name` outer scope-এ আছে।

---

# 2. Scope-এর প্রধান ধরন

JavaScript-এ এখন তোমার মূলত এগুলো বুঝতে হবে:

```text
Scope
│
├── Global Scope
│
├── Function Scope
│
├── Block Scope
│
└── Lexical Scope
```

এর সাথে **Scope Chain**-ও খুব গুরুত্বপূর্ণ।

---

# 3. Global Scope

যে variable সবচেয়ে বাইরের scope-এ declare করা হয়, সেটা global scope-এর variable।

```javascript
let name = "Atiar";

console.log(name);
```

এখানে:

```javascript
name
```

global scope-এ আছে।

Function-এর ভিতর থেকেও access করা যায়:

```javascript
let name = "Atiar";

function greet() {
    console.log(name);
}

greet();
```

Output:

```text
Atiar
```

---

# 4. Global Variable কোথা থেকে access করা যায়?

সাধারণভাবে global variable অনেক জায়গা থেকেই access করা যায়:

```javascript
let username = "Atiar";

function test() {
    console.log(username);
}

if (true) {
    console.log(username);
}

console.log(username);
```

সব জায়গা থেকেই `username` access করা যাচ্ছে।

---

# 5. Function Scope

Function-এর ভিতরে declare করা variable সাধারণত সেই function-এর বাইরে access করা যায় না।

```javascript
function greet() {
    let message = "Hello";

    console.log(message);
}

greet();
```

এটা কাজ করবে।

কিন্তু:

```javascript
console.log(message);
```

এটা কাজ করবে না।

কারণ `message` function-এর local scope-এ আছে।

---

# 6. সহজ উদাহরণ

```javascript
function test() {
    let age = 25;

    console.log(age);
}
```

এখানে:

```text
Global Scope
│
└── test()
      │
      └── age
```

`age` শুধু `test()`-এর ভিতরের scope-এ accessible।

---

# 7. Function-এর বাইরে থেকে ভিতরের variable access করা যায় না

```javascript
function test() {
    let message = "Hello";
}

console.log(message);
```

Result:

```text
ReferenceError
```

কারণ `message` global scope-এ নেই।

---

# 8. Function-এর ভিতর থেকে Outer Variable Access

এখানে উল্টো ঘটনা:

```javascript
let name = "Atiar";

function greet() {
    console.log(name);
}

greet();
```

কাজ করবে।

কারণ function প্রথমে নিজের scope-এ `name` খুঁজবে।

না পেলে outer scope-এ যাবে।

---

# 9. Scope Chain

এটাই **Scope Chain**।

Example:

```javascript
let country = "Bangladesh";

function outer() {

    let city = "Dhaka";

    function inner() {

        let area = "Mirpur";

        console.log(area);
        console.log(city);
        console.log(country);
    }

    inner();
}

outer();
```

`inner()` function-এর কাছে তিনটা variable accessible:

```text
inner scope
    ↓
outer scope
    ↓
global scope
```

Flow:

```text
Global
  │
  │ country
  ↓
outer()
  │
  │ city
  ↓
inner()
  │
  │ area
  ↓
```

`inner()`:

```javascript
console.log(area);      // নিজের scope
console.log(city);      // outer scope
console.log(country);   // global scope
```

সব access করা যাবে।

---

# 10. কিন্তু Outer Function Inner Variable Access করতে পারে না

```javascript
function outer() {

    function inner() {
        let message = "Hello";
    }

    console.log(message);
}
```

এটা কাজ করবে না।

কারণ:

```text
outer
  ↓
inner
  ↓
message
```

`message` inner scope-এর।

Outer scope ভিতরের scope-এর variable দেখতে পারে না।

### Rule

> **Inner scope → outer scope access করতে পারে।**

কিন্তু:

> **Outer scope → inner scope access করতে পারে না।**

---

# 11. Block Scope

`let` এবং `const` **block scoped**।

Block হলো `{ }` দিয়ে তৈরি অংশ।

Example:

```javascript
if (true) {
    let message = "Hello";

    console.log(message);
}
```

এখানে `message` block-এর ভিতরে accessible।

কিন্তু:

```javascript
if (true) {
    let message = "Hello";
}

console.log(message);
```

এটা error হবে।

কারণ `message` শুধু `if` block-এর ভিতরে accessible।

---

# 12. Block Scope with `const`

```javascript
if (true) {
    const age = 25;

    console.log(age);
}
```

কাজ করবে।

কিন্তু:

```javascript
if (true) {
    const age = 25;
}

console.log(age);
```

কাজ করবে না।

---

# 13. `let` এবং `const` Block Scoped

এই concept মনে রাখো:

```javascript
if (true) {
    let a = 10;
    const b = 20;
}
```

`a` এবং `b` block-এর বাইরে accessible নয়।

---

# 14. `var` বনাম `let`

এখানে JavaScript-এর একটি important difference আছে।

### `var`

```javascript
if (true) {
    var name = "Atiar";
}

console.log(name);
```

এটা কাজ করবে।

Output:

```text
Atiar
```

কারণ `var` block scoped নয়।

---

### `let`

```javascript
if (true) {
    let name = "Atiar";
}

console.log(name);
```

এটা error হবে।

কারণ `let` block scoped।

---

# 15. `var` Function Scoped

যদিও `var` block scoped নয়, কিন্তু function scoped।

```javascript
function test() {

    var name = "Atiar";

    console.log(name);
}

test();
```

কাজ করবে।

কিন্তু:

```javascript
function test() {

    var name = "Atiar";
}

console.log(name);
```

কাজ করবে না।

---

# 16. `let`, `const`, `var` Scope Comparison

| Keyword | Global | Function | Block |
| ------- | ------ | -------- | ----- |
| `var`   | Yes    | Yes      | ❌     |
| `let`   | Yes    | Yes      | Yes   |
| `const` | Yes    | Yes      | Yes   |

সবচেয়ে important:

```text
var   → function scoped
let   → block scoped
const → block scoped
```

Modern JavaScript-এ সাধারণত:

```javascript
let
const
```

ব্যবহার করবে।

---

# 17. একই নামের Variable

Different scopes-এ একই নাম থাকতে পারে।

```javascript
let name = "Atiar";

function test() {
    let name = "Rahim";

    console.log(name);
}

test();

console.log(name);
```

Output:

```text
Rahim
Atiar
```

কেন?

Function-এর ভিতরে নিজের `name` আছে।

তাই outer `name` shadow হয়ে গেছে।

---

# 18. Variable Shadowing

একটি inner scope-এর variable যদি outer scope-এর একই নামের variable-কে hide করে, তাকে **shadowing** বলে।

```javascript
let name = "Atiar";

function greet() {

    let name = "Rahim";

    console.log(name);
}
```

এখানে:

```text
Global name → Atiar

Function name → Rahim
```

Function-এর ভিতরে `name` বললে:

```text
Rahim
```

পাবে।

---

# 19. Nested Block Shadowing

```javascript
let age = 30;

if (true) {

    let age = 20;

    console.log(age);
}

console.log(age);
```

Output:

```text
20
30
```

Inner `age` outer `age`-কে shadow করেছে।

---

# 20. Scope Chain দিয়ে Variable Search

JavaScript যখন এই code দেখে:

```javascript
let name = "Atiar";

function outer() {

    let city = "Dhaka";

    function inner() {

        console.log(name);
        console.log(city);
    }

    inner();
}
```

`inner()` যখন:

```javascript
console.log(city);
```

দেখে, তখন JavaScript roughly:

```text
1. inner scope-এ city আছে?
       ↓
      No

2. outer scope-এ city আছে?
       ↓
      Yes

3. value ব্যবহার করো
```

আর:

```javascript
console.log(name);
```

এর ক্ষেত্রে:

```text
inner scope
   ↓
outer scope
   ↓
global scope
   ↓
name পাওয়া গেল
```

এটাই Scope Chain।

---

# 21. Lexical Scope

JavaScript-এর scope **code কোথায় লেখা হয়েছে** তার ওপর নির্ভর করে।

Example:

```javascript
let name = "Atiar";

function outer() {

    function inner() {
        console.log(name);
    }

    inner();
}
```

`inner()` কোথায় লেখা হয়েছে সেটা গুরুত্বপূর্ণ।

এখানে `inner()` `outer()`-এর ভিতরে লেখা হয়েছে, তাই outer এবং global scope access করতে পারে।

এটাই **Lexical Scope**।

সহজভাবে:

> Function যেখানে লেখা হয়েছে, সেই জায়গার surrounding scope সে access করতে পারে।

---

# 22. Closure-এর সাথে Scope-এর সম্পর্ক

Closure এখনই deep শেখার দরকার নেই, তবে scope বুঝতে এই example দেখো:

```javascript
function outer() {

    let message = "Hello";

    function inner() {
        console.log(message);
    }

    return inner;
}

const greet = outer();

greet();
```

Output:

```text
Hello
```

খেয়াল করো:

`outer()` execution শেষ হয়ে যাওয়ার পরেও `inner()` `message` access করতে পারছে।

এটাই closure-এর basic idea।

পরবর্তীতে callback, React hooks এবং advanced JavaScript-এ এটা খুব গুরুত্বপূর্ণ হবে।

---

# 23. `if` Block Scope

```javascript
let isLoggedIn = true;

if (isLoggedIn) {

    let message = "Welcome";

    console.log(message);
}
```

এখানে `message` শুধু `if` block-এর মধ্যে।

---

# 24. `for` Loop Scope

```javascript
for (let i = 0; i < 3; i++) {
    console.log(i);
}
```

এখানে `i` loop-এর scope-এর মধ্যে।

তাই:

```javascript
console.log(i);
```

loop-এর বাইরে করলে error হবে।

---

# 25. `const` Object Scope

```javascript
const user = {
    name: "Atiar"
};
```

এখানে `user` variable reassign করা যাবে না:

```javascript
user = {};
```

error হবে।

কিন্তু object-এর property পরিবর্তন করা যায়:

```javascript
user.name = "Rahim";
```

এটা scope-এর বিষয় নয়; এটা `const` এবং object mutability-এর বিষয়।

---

# 26. Function Parameter-এর Scope

Function parameter-ও local scope-এর মধ্যে থাকে।

```javascript
function greet(name) {
    console.log(name);
}
```

এখানে:

```javascript
name
```

function-এর ভিতরে accessible।

কিন্তু বাইরে:

```javascript
console.log(name);
```

accessible নয়।

---

# 27. Practical Example

ধরো:

```javascript
const appName = "ShopHub";

function loginUser(email) {

    const isValid = email.includes("@");

    if (isValid) {

        const message = "Login successful";

        console.log(appName);
        console.log(email);
        console.log(isValid);
        console.log(message);
    }
}
```

এখানে scope:

```text
Global Scope
│
├── appName
│
└── loginUser()
      │
      ├── email
      ├── isValid
      │
      └── if block
            │
            └── message
```

`if` block-এর ভিতরে:

```javascript
appName
email
isValid
message
```

সব access করা যাবে।

কিন্তু `message` block-এর বাইরে access করা যাবে না।

---

# 28. React-এ Scope

React component মূলত function।

```jsx
function UserProfile() {

    const name = "Atiar";

    return (
        <h1>{name}</h1>
    );
}
```

এখানে `name` component/function-এর local scope-এ।

আরেক component:

```jsx
function Dashboard() {

    console.log(name);
}
```

এখানে `name` directly access করা যাবে না।

তাই React-এ data share করার জন্য:

* props
* state
* context
* external state management

ইত্যাদি ব্যবহার করা হয়।

---

# 29. Common Mistake

### ভুল:

```javascript
if (true) {
    let username = "Atiar";
}

console.log(username);
```

কারণ `username` block-এর বাইরে নেই।

### সঠিক:

```javascript
let username;

if (true) {
    username = "Atiar";
}

console.log(username);
```

এখানে `username` outer scope-এ declare করা হয়েছে।

---

# 30. Another Common Mistake

```javascript
function calculate() {

    let total = 100;
}

console.log(total);
```

এটা কাজ করবে না।

যদি বাইরে দরকার হয়:

```javascript
function calculate() {
    return 100;
}

const total = calculate();

console.log(total);
```

এখানে `return` ব্যবহার করে function-এর result বাইরে আনা হয়েছে।

---

# 31. Scope-এর Golden Rules

এই rules কয়েকবার পড়ো:

### Rule 1

> **Outer scope-এর variable inner scope access করতে পারে।**

❌ এই direction কাজ করে না।

```text
inner → outer  ✅
outer → inner  ❌
```

---

### Rule 2

`let` এবং `const` block scoped।

```javascript
if (true) {
    let x = 10;
}
```

`x` বাইরে নেই।

---

### Rule 3

`var` block scoped নয়।

```javascript
if (true) {
    var x = 10;
}

console.log(x); // 10
```

কিন্তু function-এর বাইরে যেতে পারে না।

---

### Rule 4

Inner scope outer variable shadow করতে পারে।

```javascript
let x = 10;

if (true) {
    let x = 20;

    console.log(x); // 20
}

console.log(x); // 10
```

---

### Rule 5

Function parameter local।

```javascript
function test(value) {
    console.log(value);
}
```

`value` function-এর বাইরে নেই।

---

# 32. Scope Diagram

সবচেয়ে সহজভাবে:

```text
                    GLOBAL SCOPE
                         │
                ┌────────┴────────┐
                │                 │
             name             function()
                                  │
                           FUNCTION SCOPE
                                  │
                           ┌──────┴──────┐
                           │             │
                         age          if block
                                       │
                                    BLOCK SCOPE
                                       │
                                    message
```

`message` access:

```text
if block       ✅
function       ❌
global         ❌
```

`age` access:

```text
function       ✅
if block       ✅
global         ❌
```

`name` access:

```text
global         ✅
function       ✅
if block       ✅
```

---

# 33. Scope Mastery-এর জন্য এই Codeটা Analyze করো

```javascript
let a = 10;

function outer() {

    let b = 20;

    if (true) {

        let c = 30;

        console.log(a);
        console.log(b);
        console.log(c);
    }
}

outer();
```

`console.log()` তিনটিই কাজ করবে।

কারণ:

```text
c → নিজের block
b → outer function
a → global
```

এটাই Scope Chain।

কিন্তু:

```javascript
console.log(c);
```

`if` block-এর বাইরে করলে কাজ করবে না।

আর:

```javascript
console.log(b);
```

`outer()`-এর বাইরে করলে কাজ করবে না।

---

# 🧠 Final Mental Model

```text
             GLOBAL
               │
               ↓
            FUNCTION
               │
               ↓
             BLOCK
               │
               ↓
            INNER BLOCK
```

Variable search সবসময়:

```text
নিজের scope
    ↓
outer scope
    ↓
আরও outer scope
    ↓
global scope
    ↓
না পেলে ReferenceError
```

এটাই **Scope Chain**।

আর সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
var   → Function Scope

let   → Block Scope

const → Block Scope
```

JavaScript/React development-এর জন্য `let` ও `const`-এর scope ভালোভাবে বোঝা সবচেয়ে জরুরি।



---
# *Thanks*
----

# JavaScript Arrays — Complete Guide

JavaScript-এ **Array** হলো একাধিক value একসাথে store করার একটি data structure।

যেমন, ৫টা product আলাদা variable-এ রাখার বদলে:

```javascript
const product1 = "Laptop";
const product2 = "Mouse";
const product3 = "Keyboard";
const product4 = "Monitor";
const product5 = "Headphone";
```

Array ব্যবহার করলে:

```javascript
const products = [
    "Laptop",
    "Mouse",
    "Keyboard",
    "Monitor",
    "Headphone"
];
```

এটাই Array-এর মূল উদ্দেশ্য:

> **একটি variable-এর মধ্যে multiple values রাখা এবং সেগুলো efficiently manipulate করা।**

---

# 1. Array তৈরি করা

সবচেয়ে common way:

```javascript
const fruits = ["Apple", "Mango", "Banana"];
```

আরেকটি way:

```javascript
const numbers = new Array(10, 20, 30);
```

Modern JavaScript-এ সাধারণত:

```javascript
const numbers = [10, 20, 30];
```

ব্যবহার করবে।

---

# 2. Array Index

Array-এর প্রতিটি element-এর একটি **index** থাকে।

Index শুরু হয় `0` থেকে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];
```

```text
Value       Index

Apple         0
Mango         1
Banana        2
```

তাই:

```javascript
console.log(fruits[0]);
```

Output:

```text
Apple
```

```javascript
console.log(fruits[1]);
```

Output:

```text
Mango
```

---

# 3. Last Element

Array-এর last element পেতে:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits[fruits.length - 1]);
```

Output:

```text
Banana
```

Modern JavaScript-এ:

```javascript
console.log(fruits.at(-1));
```

Output:

```text
Banana
```

---

# 4. `length`

Array-তে কয়টি element আছে জানতে:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.length);
```

Output:

```text
3
```

মনে রাখবে:

```text
length = number of elements

last index = length - 1
```

---

# 5. Array-এর Value পরিবর্তন

Array mutable, তাই element পরিবর্তন করা যায়।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

fruits[1] = "Orange";

console.log(fruits);
```

Output:

```javascript
["Apple", "Orange", "Banana"]
```

খেয়াল করো `const` হলেও array-এর element পরিবর্তন করা যাচ্ছে।

কারণ:

```javascript
fruits = [];
```

এটা করা যাবে না।

কিন্তু:

```javascript
fruits[0] = "Grape";
```

করা যাবে।

---

# 6. Array-তে নতুন Element যোগ করা

## `push()`

শেষে element যোগ করে।

```javascript
const fruits = ["Apple", "Mango"];

fruits.push("Banana");

console.log(fruits);
```

Output:

```javascript
["Apple", "Mango", "Banana"]
```

`push()` নতুন array length return করে:

```javascript
const result = fruits.push("Orange");

console.log(result);
```

---

# 7. `unshift()`

Array-এর শুরুতে element যোগ করে।

```javascript
const fruits = ["Mango", "Banana"];

fruits.unshift("Apple");

console.log(fruits);
```

Output:

```javascript
["Apple", "Mango", "Banana"]
```

### মনে রাখো

```text
push()    → শেষে যোগ
unshift() → শুরুতে যোগ
```

---

# 8. Array থেকে Element Remove

## `pop()`

শেষ element remove করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const removed = fruits.pop();

console.log(fruits);
console.log(removed);
```

Output:

```text
["Apple", "Mango"]
Banana
```

---

# 9. `shift()`

প্রথম element remove করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const removed = fruits.shift();

console.log(fruits);
console.log(removed);
```

Output:

```text
["Mango", "Banana"]
Apple
```

### মনে রাখো

```text
pop()    → শেষ থেকে remove
shift()  → শুরু থেকে remove
```

---

# 10. Four Basic Operations

এই চারটা অবশ্যই মুখস্থ:

```text
push()     → add at end
pop()      → remove from end

unshift()  → add at beginning
shift()    → remove from beginning
```

Diagram:

```text
             ARRAY
               |
      ┌────────┴────────┐
      ↓                 ↓
    START              END
      │                 │
   unshift              push
      │                 │
    shift               pop
```

---

# 11. `splice()` — সবচেয়ে Important

`splice()` দিয়ে array-এর **মাঝখান থেকে add/remove/replace** করা যায়।

Syntax:

```javascript
array.splice(start, deleteCount, item1, item2, ...);
```

---

## Remove

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana",
    "Orange"
];

fruits.splice(1, 1);

console.log(fruits);
```

Output:

```javascript
["Apple", "Banana", "Orange"]
```

এখানে:

```text
1 → start index
1 → কয়টি remove করবে
```

---

# 12. Multiple Elements Remove

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana",
    "Orange"
];

fruits.splice(1, 2);

console.log(fruits);
```

Output:

```javascript
["Apple", "Orange"]
```

কারণ index `1` থেকে ২টা remove করেছে:

```text
Mango
Banana
```

---

# 13. `splice()` দিয়ে Add

Delete না করে add:

```javascript
const fruits = ["Apple", "Banana"];

fruits.splice(1, 0, "Mango");

console.log(fruits);
```

Output:

```javascript
["Apple", "Mango", "Banana"]
```

এখানে:

```text
1 → index
0 → কিছু remove করবে না
"Mango" → add করবে
```

---

# 14. `splice()` দিয়ে Replace

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

fruits.splice(1, 1, "Orange");

console.log(fruits);
```

Output:

```javascript
["Apple", "Orange", "Banana"]
```

---

# 15. `slice()` — Array-এর অংশ Copy করা

`slice()` original array পরিবর্তন করে না।

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana",
    "Orange"
];

const result = fruits.slice(1, 3);

console.log(result);
```

Output:

```javascript
["Mango", "Banana"]
```

এখানে:

```text
start = 1
end   = 3
```

End index `3` include হয় না।

---

# 16. `slice()` vs `splice()`

এটা খুব important:

|Method|কাজ|Original array|
|---|---|---|
|`slice()`|অংশ copy করে|পরিবর্তন করে না|
|`splice()`|add/remove/replace|পরিবর্তন করে|

Example:

```javascript
const arr = [1, 2, 3, 4];

const a = arr.slice(1, 3);
```

Original:

```javascript
[1, 2, 3, 4]
```

কিন্তু:

```javascript
arr.splice(1, 2);
```

Original পরিবর্তন হবে:

```javascript
[1, 4]
```

---

# 17. `concat()`

দুই বা তার বেশি array combine করে।

```javascript
const fruits = ["Apple", "Mango"];
const vegetables = ["Potato", "Carrot"];

const food = fruits.concat(vegetables);

console.log(food);
```

Output:

```javascript
["Apple", "Mango", "Potato", "Carrot"]
```

Modern JavaScript-এ spread operator দিয়েও:

```javascript
const food = [...fruits, ...vegetables];
```

---

# 18. Spread Operator `...`

Array copy করার জন্য:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const newFruits = [...fruits];

console.log(newFruits);
```

আরও value যোগ:

```javascript
const newFruits = [
    ...fruits,
    "Orange"
];
```

---

# 19. Array Copy

```javascript
const original = [1, 2, 3];

const copy = [...original];

copy.push(4);

console.log(original);
console.log(copy);
```

Output:

```text
[1, 2, 3]
[1, 2, 3, 4]
```

---

# 20. `includes()`

Array-এর মধ্যে কোনো value আছে কিনা check করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.includes("Mango"));
```

Output:

```text
true
```

```javascript
console.log(fruits.includes("Orange"));
```

Output:

```text
false
```

---

# 21. `indexOf()`

কোনো element-এর index বের করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.indexOf("Mango"));
```

Output:

```text
1
```

না থাকলে:

```javascript
console.log(fruits.indexOf("Orange"));
```

Output:

```text
-1
```

---

# 22. `lastIndexOf()`

একই value একাধিকবার থাকলে শেষ occurrence-এর index দেয়।

```javascript
const numbers = [10, 20, 10, 30, 10];

console.log(numbers.lastIndexOf(10));
```

Output:

```text
4
```

---

# 23. `join()`

Array-এর elements string হিসেবে combine করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.join(", "));
```

Output:

```text
Apple, Mango, Banana
```

আর:

```javascript
console.log(fruits.join(" - "));
```

Output:

```text
Apple - Mango - Banana
```

---

# 24. `toString()`

Array-কে string-এ convert করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.toString());
```

Output:

```text
Apple,Mango,Banana
```

`join()` বেশি flexible।

---

# 25. `reverse()`

Array-এর order reverse করে।

```javascript
const numbers = [1, 2, 3, 4];

numbers.reverse();

console.log(numbers);
```

Output:

```javascript
[4, 3, 2, 1]
```

⚠️ `reverse()` original array পরিবর্তন করে।

---

# 26. Modern Non-mutating Reverse

Original পরিবর্তন না করতে চাইলে:

```javascript
const numbers = [1, 2, 3, 4];

const reversed = numbers.toReversed();

console.log(reversed);
console.log(numbers);
```

Output:

```text
[4, 3, 2, 1]
[1, 2, 3, 4]
```

---

# 27. `sort()`

Array sort করে।

String-এর ক্ষেত্রে:

```javascript
const fruits = [
    "Mango",
    "Apple",
    "Banana"
];

fruits.sort();

console.log(fruits);
```

Output:

```javascript
["Apple", "Banana", "Mango"]
```

---

# 28. Number Sort-এর Important Problem

এটা:

```javascript
const numbers = [10, 5, 100, 20];

numbers.sort();

console.log(numbers);
```

Unexpected হতে পারে:

```javascript
[10, 100, 20, 5]
```

কারণ default `sort()` values-কে string হিসেবে compare করে।

---

# 29. Number Ascending Sort

```javascript
const numbers = [10, 5, 100, 20];

numbers.sort((a, b) => a - b);

console.log(numbers);
```

Output:

```javascript
[5, 10, 20, 100]
```

Logic:

```text
a - b < 0 → a আগে
a - b > 0 → b আগে
```

---

# 30. Number Descending Sort

```javascript
numbers.sort((a, b) => b - a);
```

Output:

```javascript
[100, 20, 10, 5]
```

---

# 31. `map()` — সবচেয়ে Important

`map()` প্রতিটি element-এর ওপর operation করে **নতুন array return করে**।

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => {
    return number * 2;
});

console.log(doubled);
```

Output:

```javascript
[2, 4, 6, 8]
```

Original:

```javascript
[1, 2, 3, 4]
```

পরিবর্তন হয়নি।

---

# 32. `map()` Practical Example

```javascript
const prices = [100, 200, 300];

const discountedPrices = prices.map(
    price => price * 0.9
);

console.log(discountedPrices);
```

Output:

```javascript
[90, 180, 270]
```

---

# 33. Object Array-এ `map()`

Real-world application-এ এটা খুব common।

```javascript
const users = [
    { name: "Atiar", age: 25 },
    { name: "Rahim", age: 30 },
    { name: "Karim", age: 22 }
];

const names = users.map(user => user.name);

console.log(names);
```

Output:

```javascript
["Atiar", "Rahim", "Karim"]
```

React-এ API data render করার সময় `map()` অনেক ব্যবহার করবে।

---

# 34. `filter()`

Condition অনুযায়ী elements select করে **নতুন array** দেয়।

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(
    number => number % 2 === 0
);

console.log(evenNumbers);
```

Output:

```javascript
[2, 4, 6]
```

---

# 35. `filter()` Object-এর সাথে

```javascript
const users = [
    { name: "Atiar", age: 25 },
    { name: "Rahim", age: 17 },
    { name: "Karim", age: 30 }
];

const adults = users.filter(
    user => user.age >= 18
);

console.log(adults);
```

Result:

```javascript
[
    { name: "Atiar", age: 25 },
    { name: "Karim", age: 30 }
]
```

---

# 36. `find()`

Condition match করা **প্রথম element** return করে।

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find(
    number => number > 20
);

console.log(result);
```

Output:

```text
30
```

---

# 37. `find()` Object-এর সাথে

```javascript
const users = [
    { id: 1, name: "Atiar" },
    { id: 2, name: "Rahim" },
    { id: 3, name: "Karim" }
];

const user = users.find(
    user => user.id === 2
);

console.log(user);
```

Output:

```javascript
{
    id: 2,
    name: "Rahim"
}
```

না পেলে:

```text
undefined
```

---

# 38. `findIndex()`

Match করা প্রথম element-এর index return করে।

```javascript
const numbers = [10, 20, 30, 40];

const index = numbers.findIndex(
    number => number > 20
);

console.log(index);
```

Output:

```text
2
```

---

# 39. `some()`

কমপক্ষে **একটি element** condition satisfy করে কিনা check করে।

```javascript
const numbers = [1, 3, 5, 8];

const result = numbers.some(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

কারণ `8` even।

---

# 40. `every()`

**সবগুলো element** condition satisfy করে কিনা check করে।

```javascript
const numbers = [2, 4, 6, 8];

const result = numbers.every(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

কিন্তু:

```javascript
const numbers = [2, 4, 5, 8];
```

তাহলে:

```text
false
```

---

# 41. `reduce()` — Very Important

`reduce()` অনেকগুলো value-কে একটি final value-তে convert করে।

Example:

```javascript
const numbers = [10, 20, 30, 40];

const total = numbers.reduce(
    (sum, number) => {
        return sum + number;
    },
    0
);

console.log(total);
```

Output:

```text
100
```

Flow:

```text
0 + 10 = 10
10 + 20 = 30
30 + 30 = 60
60 + 40 = 100
```

---

# 42. `reduce()` দিয়ে Product Total

```javascript
const cart = [
    { name: "Laptop", price: 80000 },
    { name: "Mouse", price: 1000 },
    { name: "Keyboard", price: 3000 }
];

const total = cart.reduce(
    (sum, product) => {
        return sum + product.price;
    },
    0
);

console.log(total);
```

Output:

```text
84000
```

E-commerce application-এ এটা খুব useful।

---

# 43. `reduce()` দিয়ে Quantity × Price

```javascript
const cart = [
    { price: 100, quantity: 2 },
    { price: 200, quantity: 3 },
    { price: 50, quantity: 4 }
];

const total = cart.reduce(
    (sum, item) => {
        return sum + item.price * item.quantity;
    },
    0
);

console.log(total);
```

Calculation:

```text
100 × 2 = 200
200 × 3 = 600
50 × 4  = 200

Total = 1000
```

---

# 44. `forEach()`

Array-এর প্রতিটি element-এর জন্য function execute করে।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

fruits.forEach(fruit => {
    console.log(fruit);
});
```

Output:

```text
Apple
Mango
Banana
```

---

# 45. `forEach()` vs `map()`

### `forEach()`

```javascript
const numbers = [1, 2, 3];

numbers.forEach(number => {
    console.log(number * 2);
});
```

সাধারণত নতুন array তৈরি করার জন্য নয়।

### `map()`

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(
    number => number * 2
);
```

Output:

```javascript
[2, 4, 6]
```

### মনে রাখো

```text
forEach() → শুধু iterate / side effect
map()     → transform করে new array
```

---

# 46. `flat()`

Nested array flatten করে।

```javascript
const numbers = [
    [1, 2],
    [3, 4],
    [5, 6]
];

console.log(numbers.flat());
```

Output:

```javascript
[1, 2, 3, 4, 5, 6]
```

---

# 47. `flat()` Depth

```javascript
const numbers = [
    [1, [2, 3]],
    [4, 5]
];

console.log(numbers.flat());
```

Output:

```javascript
[1, [2, 3], 4, 5]
```

আর:

```javascript
console.log(numbers.flat(2));
```

Output:

```javascript
[1, 2, 3, 4, 5]
```

---

# 48. `flatMap()`

`map()` + `flat()` একসাথে করার মতো।

```javascript
const numbers = [1, 2, 3];

const result = numbers.flatMap(
    number => [number, number * 2]
);

console.log(result);
```

Output:

```javascript
[1, 2, 2, 4, 3, 6]
```

---

# 49. Destructuring

Array থেকে value সহজে বের করা যায়।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const [first, second, third] = fruits;

console.log(first);
console.log(second);
console.log(third);
```

Output:

```text
Apple
Mango
Banana
```

---

# 50. Skip Elements

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

const [first, , third] = fruits;

console.log(first);
console.log(third);
```

Output:

```text
Apple
Banana
```

---

# 51. Rest Operator with Array

```javascript
const numbers = [1, 2, 3, 4, 5];

const [first, second, ...rest] = numbers;

console.log(first);
console.log(second);
console.log(rest);
```

Output:

```text
1
2
[3, 4, 5]
```

---

# 52. Array থেকে Duplicate Remove

Modern JavaScript-এর সহজ technique:

```javascript
const numbers = [1, 2, 2, 3, 3, 4];

const unique = [...new Set(numbers)];

console.log(unique);
```

Output:

```javascript
[1, 2, 3, 4]
```

---

# 53. Array Check

কোনো value Array কিনা:

```javascript
const numbers = [1, 2, 3];

console.log(Array.isArray(numbers));
```

Output:

```text
true
```

আর:

```javascript
console.log(Array.isArray("Hello"));
```

Output:

```text
false
```

---

# 54. `Array.from()`

Iterable বা array-like data থেকে array তৈরি করতে পারে।

```javascript
const text = "HELLO";

const letters = Array.from(text);

console.log(letters);
```

Output:

```javascript
["H", "E", "L", "L", "O"]
```

---

# 55. `Array.of()`

Values দিয়ে নতুন array তৈরি করে:

```javascript
const numbers = Array.of(10, 20, 30);

console.log(numbers);
```

Output:

```javascript
[10, 20, 30]
```

---

# 56. `fill()`

একই value দিয়ে array fill করে।

```javascript
const numbers = [1, 2, 3, 4, 5];

numbers.fill(0);

console.log(numbers);
```

Output:

```javascript
[0, 0, 0, 0, 0]
```

Specific range:

```javascript
const numbers = [1, 2, 3, 4, 5];

numbers.fill(0, 1, 4);

console.log(numbers);
```

Output:

```javascript
[1, 0, 0, 0, 5]
```

---

# 57. `at()`

Index দিয়ে element access করার modern way:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

console.log(fruits.at(1));
```

Output:

```text
Mango
```

Negative index:

```javascript
console.log(fruits.at(-1));
```

Output:

```text
Banana
```

---

# 58. `entries()`

Index এবং value একসাথে পাওয়া যায়।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const [index, fruit] of fruits.entries()) {
    console.log(index, fruit);
}
```

Output:

```text
0 Apple
1 Mango
2 Banana
```

---

# 59. `keys()`

Array-এর indexes পাওয়া যায়।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const index of fruits.keys()) {
    console.log(index);
}
```

Output:

```text
0
1
2
```

---

# 60. `values()`

Values পাওয়া যায়:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const fruit of fruits.values()) {
    console.log(fruit);
}
```

Output:

```text
Apple
Mango
Banana
```

---

# 61. Traditional `for` Loop

Array iterate করার classic way:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

---

# 62. `for...of`

Modern এবং clean:

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const fruit of fruits) {
    console.log(fruit);
}
```

যদি শুধু values দরকার হয়, এটা খুব ভালো।

---

# 63. `for...in`

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const index in fruits) {
    console.log(index, fruits[index]);
}
```

এটা কাজ করলেও Array-এর জন্য সাধারণত `for...of` prefer করা ভালো।

```text
for...of → values
for...in → keys/indexes
```

---

# 64. `Array.from()` দিয়ে Range

```javascript
const numbers = Array.from(
    { length: 5 },
    (_, index) => index + 1
);

console.log(numbers);
```

Output:

```javascript
[1, 2, 3, 4, 5]
```

---

# 65. Mutating vs Non-Mutating Methods

এটা professional JavaScript-এর জন্য খুব important।

### Original Array পরিবর্তন করে

```text
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
fill()
```

### সাধারণত নতুন value/array return করে, original পরিবর্তন করে না

```text
slice()
concat()
map()
filter()
reduce()
find()
findIndex()
some()
every()
includes()
join()
flat()
flatMap()
```

Modern non-mutating alternatives:

```text
toSorted()
toReversed()
toSpliced()
```

---

# 66. `toSorted()`

Original array পরিবর্তন না করে sorted array দেয়।

```javascript
const numbers = [30, 10, 20];

const sorted = numbers.toSorted(
    (a, b) => a - b
);

console.log(sorted);
console.log(numbers);
```

Output:

```text
[10, 20, 30]
[30, 10, 20]
```

---

# 67. `toSpliced()`

`splice()`-এর non-mutating version।

```javascript
const fruits = ["Apple", "Mango", "Banana"];

const result = fruits.toSpliced(
    1,
    1,
    "Orange"
);

console.log(result);
console.log(fruits);
```

Output:

```text
["Apple", "Orange", "Banana"]
["Apple", "Mango", "Banana"]
```

---

# 68. Array Chaining

একাধিক method একসাথে ব্যবহার করা যায়।

ধরো:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
```

প্রথমে even number:

```javascript
.filter(number => number % 2 === 0)
```

তারপর double:

```javascript
.map(number => number * 2)
```

তারপর total:

```javascript
.reduce((sum, number) => sum + number, 0)
```

একসাথে:

```javascript
const total = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 2)
    .reduce((sum, number) => sum + number, 0);

console.log(total);
```

Flow:

```text
[1,2,3,4,5,6]
      ↓
filter
[2,4,6]
      ↓
map
[4,8,12]
      ↓
reduce
24
```

এটা modern JavaScript-এর খুব important pattern।

---

# 69. Real-world E-commerce Example

ধরো:

```javascript
const products = [
    {
        id: 1,
        name: "Laptop",
        price: 80000,
        category: "electronics"
    },
    {
        id: 2,
        name: "Mouse",
        price: 1000,
        category: "electronics"
    },
    {
        id: 3,
        name: "Shirt",
        price: 1500,
        category: "fashion"
    }
];
```

### শুধু product names:

```javascript
const names = products.map(
    product => product.name
);
```

Result:

```javascript
["Laptop", "Mouse", "Shirt"]
```

### Electronics products:

```javascript
const electronics = products.filter(
    product => product.category === "electronics"
);
```

### নির্দিষ্ট product:

```javascript
const product = products.find(
    product => product.id === 2
);
```

### সব product-এর total price:

```javascript
const total = products.reduce(
    (sum, product) => sum + product.price,
    0
);
```

এই চারটি method:

```text
map()
filter()
find()
reduce()
```

**Frontend/React development-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।**

---

# 70. সবচেয়ে গুরুত্বপূর্ণ Array Methods — Cheat Sheet

|Method|কাজ|
|---|---|
|`push()`|শেষে add|
|`pop()`|শেষে remove|
|`unshift()`|শুরুতে add|
|`shift()`|শুরুতে remove|
|`splice()`|add/remove/replace|
|`slice()`|অংশ copy|
|`concat()`|array combine|
|`includes()`|value আছে?|
|`indexOf()`|index খোঁজা|
|`lastIndexOf()`|শেষ index|
|`join()`|array → string|
|`reverse()`|reverse|
|`sort()`|sort|
|`map()`|transform|
|`filter()`|condition অনুযায়ী select|
|`find()`|প্রথম matching element|
|`findIndex()`|প্রথম matching index|
|`some()`|অন্তত একটি match?|
|`every()`|সবগুলো match?|
|`reduce()`|অনেক value → এক value|
|`forEach()`|প্রতিটি element iterate|
|`flat()`|nested array flatten|
|`flatMap()`|map + flat|
|`fill()`|value দিয়ে fill|
|`at()`|index দিয়ে access|
|`Array.isArray()`|array কিনা|
|`Array.from()`|array তৈরি|
|`Array.of()`|values দিয়ে array|
|`toSorted()`|non-mutating sort|
|`toReversed()`|non-mutating reverse|
|`toSpliced()`|non-mutating splice|

---

# 🧠 Array শেখার Priority

সব method একসাথে মুখস্থ করার দরকার নেই। এই order-এ master করো:

```text
                    ARRAY
                      │
          ┌───────────┴───────────┐
          │                       │
      Basic CRUD              Iteration
          │                       │
   push/pop/shift/          forEach()
   unshift/splice           map()
                            filter()
                            find()
                            some()
                            every()
                            reduce()
          │
          ↓
     Manipulation
          │
   slice / concat
   sort / reverse
   includes / indexOf
          │
          ↓
      Advanced
          │
   flat / flatMap
   destructuring
   spread
   chaining
   toSorted / toSpliced
```

### বিশেষভাবে এগুলো আগে master করো:

```javascript
push()
pop()
shift()
unshift()
splice()
slice()

forEach()
map()
filter()
find()
some()
every()
reduce()

includes()
indexOf()
sort()
reverse()
concat()
```

তারপর:

```javascript
flat()
flatMap()
destructuring
spread
array chaining
toSorted()
toReversed()
toSpliced()
```

**React শেখার সময় `map()`, `filter()`, `find()`, `some()`, `reduce()`, spread (`...`) এবং destructuring সবচেয়ে বেশি কাজে লাগবে।**

---
# JavaScript Objects & Properties — Complete Guide

JavaScript-এর **Object** হলো এমন একটি data structure যেখানে আমরা related data-কে **key-value pair** হিসেবে store করি।

যেমন একজন user-এর:

```text
name
email
age
is_active
```

এসব আলাদা variable না রেখে একটি object-এর মধ্যে রাখা যায়।

```javascript
const user = {
    name: "Atiar",
    email: "atiar@example.com",
    age: 25,
    is_active: true
};
```

এখানে:

```text
key            value
-------------------------
name       →   "Atiar"
email      →   "atiar@example.com"
age        →   25
is_active  →   true
```

> **Object = collection of key-value pairs**

---

# 1. Object তৈরি করা

সবচেয়ে common way:

```javascript
const user = {
    name: "Atiar",
    age: 25,
    country: "Bangladesh"
};
```

এখানে:

```javascript
name
age
country
```

হলো **properties/keys**।

আর:

```javascript
"Atiar"
25
"Bangladesh"
```

হলো তাদের **values**।

---

# 2. Object-এর Property কী?

```javascript
const user = {
    name: "Atiar",
    age: 25
};
```

এখানে:

```text
name → property
age  → property
```

আর:

```text
"Atiar" → name-এর value
25      → age-এর value
```

---

# 3. Object Property Access

Object-এর data access করার প্রধান দুইটি way আছে।

## Dot Notation

```javascript
const user = {
    name: "Atiar",
    age: 25
};

console.log(user.name);
console.log(user.age);
```

Output:

```text
Atiar
25
```

এটাই সবচেয়ে common।

---

# 4. Bracket Notation

```javascript
const user = {
    name: "Atiar",
    age: 25
};

console.log(user["name"]);
console.log(user["age"]);
```

Output:

```text
Atiar
25
```

---

# 5. Dot vs Bracket

```javascript
user.name
```

same as:

```javascript
user["name"]
```

তবে bracket notation-এর কিছু extra power আছে।

---

# 6. Dynamic Property Access

ধরো:

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};

const property = "email";

console.log(user[property]);
```

Output:

```text
atiar@example.com
```

এখানে:

```javascript
user[property]
```

মানে:

```javascript
user["email"]
```

কিন্তু:

```javascript
user.property
```

মানে `"property"` নামে property খুঁজবে।

তাই dynamic key-এর জন্য:

```javascript
user[property]
```

ব্যবহার করবে।

---

# 7. নতুন Property Add করা

Object তৈরি করার পরেও property add করা যায়।

```javascript
const user = {
    name: "Atiar"
};

user.age = 25;

console.log(user);
```

Output:

```javascript
{
    name: "Atiar",
    age: 25
}
```

Bracket দিয়েও:

```javascript
user["email"] = "atiar@example.com";
```

---

# 8. Property Update করা

Existing property-এর value change করতে পারো।

```javascript
const user = {
    name: "Atiar",
    age: 25
};

user.age = 26;

console.log(user.age);
```

Output:

```text
26
```

---

# 9. Property Delete করা

`delete` operator ব্যবহার করে property remove করা যায়।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};

delete user.age;

console.log(user);
```

Result:

```javascript
{
    name: "Atiar",
    email: "atiar@example.com"
}
```

---

# 10. Property আছে কিনা Check করা

## `in` Operator

```javascript
const user = {
    name: "Atiar",
    age: 25
};

console.log("name" in user);
```

Output:

```text
true
```

```javascript
console.log("email" in user);
```

Output:

```text
false
```

---

# 11. `hasOwnProperty()`

Object-এর নিজের property আছে কিনা check করতে:

```javascript
const user = {
    name: "Atiar",
    age: 25
};

console.log(
    user.hasOwnProperty("name")
);
```

Output:

```text
true
```

Modern safer pattern:

```javascript
Object.hasOwn(user, "name");
```

---

# 12. Property না থাকলে কী হয়?

```javascript
const user = {
    name: "Atiar"
};

console.log(user.age);
```

Output:

```text
undefined
```

Error হবে না; value হবে `undefined`।

---

# 13. `undefined` vs Property Doesn't Exist

```javascript
const user = {
    name: "Atiar",
    age: undefined
};
```

এখন:

```javascript
console.log(user.age);
```

এবং property না থাকলে:

```javascript
console.log(user.email);
```

দুটিই `undefined` দিতে পারে।

তাই property exist করে কিনা জানতে:

```javascript
console.log("age" in user);
console.log("email" in user);
```

---

# 14. Object-এর মধ্যে বিভিন্ন Data Type

Object-এর property-এর value যেকোনো valid JavaScript value হতে পারে।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    is_active: true,
    salary: null,
    skills: ["Python", "Django", "JavaScript"],
    address: {
        city: "Dhaka",
        country: "Bangladesh"
    }
};
```

এখানে:

```text
string
number
boolean
null
array
object
```

সব আছে।

---

# 15. Nested Object

Object-এর ভিতরে আরেকটি object থাকতে পারে।

```javascript
const user = {
    name: "Atiar",

    address: {
        city: "Dhaka",
        country: "Bangladesh"
    }
};
```

Access:

```javascript
console.log(user.address.city);
```

Output:

```text
Dhaka
```

আর:

```javascript
console.log(user.address.country);
```

Output:

```text
Bangladesh
```

---

# 16. Nested Object + Bracket

```javascript
console.log(
    user["address"]["city"]
);
```

Output:

```text
Dhaka
```

---

# 17. Object-এর মধ্যে Array

```javascript
const user = {
    name: "Atiar",

    skills: [
        "Python",
        "Django",
        "JavaScript",
        "React"
    ]
};
```

Access:

```javascript
console.log(user.skills[0]);
```

Output:

```text
Python
```

```javascript
console.log(user.skills[2]);
```

Output:

```text
JavaScript
```

---

# 18. Array-এর মধ্যে Object

এটা frontend/API development-এ খুব important।

```javascript
const users = [
    {
        id: 1,
        name: "Atiar"
    },
    {
        id: 2,
        name: "Rahim"
    },
    {
        id: 3,
        name: "Karim"
    }
];
```

প্রথম user:

```javascript
console.log(users[0]);
```

Output:

```javascript
{
    id: 1,
    name: "Atiar"
}
```

প্রথম user's name:

```javascript
console.log(users[0].name);
```

Output:

```text
Atiar
```

---

# 19. Object Method

Object-এর property-এর value function হলে তাকে সাধারণত **method** হিসেবে ব্যবহার করি।

```javascript
const user = {
    name: "Atiar",

    greet: function () {
        console.log("Hello");
    }
};

user.greet();
```

Output:

```text
Hello
```

---

# 20. Method-এর ভিতরে `this`

Object-এর নিজের property access করতে `this` ব্যবহার করা যায়।

```javascript
const user = {
    name: "Atiar",

    greet: function () {
        console.log("Hello " + this.name);
    }
};

user.greet();
```

Output:

```text
Hello Atiar
```

এখানে:

```javascript
this.name
```

মানে current object-এর `name` property।

---

# 21. Shorthand Method Syntax

Modern JavaScript-এ:

```javascript
const user = {
    name: "Atiar",

    greet() {
        console.log("Hello " + this.name);
    }
};

user.greet();
```

এটা cleaner syntax।

---

# 22. Property Shorthand

ধরো:

```javascript
const name = "Atiar";
const age = 25;
```

Object:

```javascript
const user = {
    name: name,
    age: age
};
```

এটা shorthand করে:

```javascript
const user = {
    name,
    age
};
```

JavaScript বুঝবে:

```javascript
{
    name: name,
    age: age
}
```

---

# 23. Computed Property Names

Dynamic key দিয়ে object তৈরি করা যায়।

```javascript
const key = "name";

const user = {
    [key]: "Atiar"
};

console.log(user);
```

Output:

```javascript
{
    name: "Atiar"
}
```

আর:

```javascript
const field = "email";

const user = {
    [field]: "atiar@example.com"
};
```

---

# 24. Object Destructuring

Object থেকে property সহজে বের করা যায়।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};

const { name, age } = user;

console.log(name);
console.log(age);
```

Output:

```text
Atiar
25
```

React এবং modern JavaScript-এ এটা অত্যন্ত গুরুত্বপূর্ণ।

---

# 25. Destructuring-এর Rename

```javascript
const user = {
    name: "Atiar",
    age: 25
};

const {
    name: userName,
    age: userAge
} = user;

console.log(userName);
console.log(userAge);
```

Output:

```text
Atiar
25
```

---

# 26. Destructuring Default Value

```javascript
const user = {
    name: "Atiar"
};

const {
    name,
    age = 18
} = user;

console.log(age);
```

Output:

```text
18
```

কারণ object-এ `age` নেই।

---

# 27. Nested Destructuring

```javascript
const user = {
    name: "Atiar",

    address: {
        city: "Dhaka",
        country: "Bangladesh"
    }
};

const {
    address: {
        city,
        country
    }
} = user;

console.log(city);
console.log(country);
```

Output:

```text
Dhaka
Bangladesh
```

---

# 28. Rest Operator with Object

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};

const {
    name,
    ...otherInfo
} = user;

console.log(name);
console.log(otherInfo);
```

Output:

```text
Atiar

{
    age: 25,
    email: "atiar@example.com"
}
```

---

# 29. Spread Operator with Object

Object copy করতে:

```javascript
const user = {
    name: "Atiar",
    age: 25
};

const copy = {
    ...user
};
```

এখন:

```javascript
console.log(copy);
```

Output:

```javascript
{
    name: "Atiar",
    age: 25
}
```

---

# 30. Object-এর সাথে নতুন Property Add

Spread খুব useful:

```javascript
const user = {
    name: "Atiar",
    age: 25
};

const updatedUser = {
    ...user,
    city: "Dhaka"
};
```

Result:

```javascript
{
    name: "Atiar",
    age: 25,
    city: "Dhaka"
}
```

---

# 31. Object Property Update with Spread

```javascript
const user = {
    name: "Atiar",
    age: 25
};

const updatedUser = {
    ...user,
    age: 26
};
```

Result:

```javascript
{
    name: "Atiar",
    age: 26
}
```

এখানে original object পরিবর্তন হয়নি।

এটা React state update-এ খুব important।

---

# 32. Multiple Objects Combine

```javascript
const personal = {
    name: "Atiar",
    age: 25
};

const professional = {
    role: "Developer",
    company: "ABC"
};

const user = {
    ...personal,
    ...professional
};
```

Result:

```javascript
{
    name: "Atiar",
    age: 25,
    role: "Developer",
    company: "ABC"
}
```

---

# 33. Same Property হলে কী হবে?

```javascript
const user1 = {
    name: "Atiar",
    age: 25
};

const user2 = {
    name: "Rahim",
    city: "Dhaka"
};

const user = {
    ...user1,
    ...user2
};
```

Result:

```javascript
{
    name: "Rahim",
    age: 25,
    city: "Dhaka"
}
```

শেষের object-এর property value overwrite করে।

---

# 34. `Object.keys()`

Object-এর সব keys-এর array দেয়।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    city: "Dhaka"
};

console.log(Object.keys(user));
```

Output:

```javascript
["name", "age", "city"]
```

---

# 35. `Object.values()`

সব values-এর array:

```javascript
console.log(Object.values(user));
```

Output:

```javascript
["Atiar", 25, "Dhaka"]
```

---

# 36. `Object.entries()`

Key এবং value pair-এর array দেয়।

```javascript
console.log(Object.entries(user));
```

Output:

```javascript
[
    ["name", "Atiar"],
    ["age", 25],
    ["city", "Dhaka"]
]
```

এটা object iterate করতে খুব useful।

---

# 37. Object Iterate করা

```javascript
const user = {
    name: "Atiar",
    age: 25,
    city: "Dhaka"
};

for (const [key, value] of Object.entries(user)) {
    console.log(key, value);
}
```

Output:

```text
name Atiar
age 25
city Dhaka
```

---

# 38. `for...in`

Object-এর properties iterate করার জন্য:

```javascript
for (const key in user) {
    console.log(key);
}
```

Output:

```text
name
age
city
```

Value:

```javascript
for (const key in user) {
    console.log(user[key]);
}
```

---

# 39. `Object.assign()`

একটি object-এর properties অন্য object-এ copy/merge করতে পারে।

```javascript
const user = {
    name: "Atiar"
};

Object.assign(user, {
    age: 25,
    city: "Dhaka"
});

console.log(user);
```

Result:

```javascript
{
    name: "Atiar",
    age: 25,
    city: "Dhaka"
}
```

---

# 40. `Object.assign()` দিয়ে নতুন Object

Original পরিবর্তন না করে:

```javascript
const user = {
    name: "Atiar"
};

const updatedUser = Object.assign(
    {},
    user,
    { age: 25 }
);
```

Result:

```javascript
{
    name: "Atiar",
    age: 25
}
```

Modern code-এ spread সাধারণত cleaner:

```javascript
const updatedUser = {
    ...user,
    age: 25
};
```

---

# 41. `Object.freeze()`

Object freeze করলে properties add/update/delete করা যাবে না।

```javascript
const user = {
    name: "Atiar",
    age: 25
};

Object.freeze(user);

user.age = 30;
```

Strict mode-এ error হতে পারে; otherwise assignment silently fail করতে পারে।

---

# 42. `Object.seal()`

Seal করলে:

* নতুন property add করা যাবে না
* property delete করা যাবে না
* existing property update করা যায়

```javascript
const user = {
    name: "Atiar",
    age: 25
};

Object.seal(user);

user.age = 30;   // allowed
```

কিন্তু:

```javascript
user.city = "Dhaka"; // not allowed
```

---

# 43. `Object.isFrozen()`

Object frozen কিনা:

```javascript
console.log(Object.isFrozen(user));
```

---

# 44. `Object.isSealed()`

```javascript
console.log(Object.isSealed(user));
```

---

# 45. `Object.create()`

একটি নির্দিষ্ট prototype থেকে object তৈরি করা যায়।

```javascript
const person = {
    greet() {
        console.log("Hello");
    }
};

const user = Object.create(person);

user.name = "Atiar";

user.greet();
```

Output:

```text
Hello
```

এটা prototype concept বোঝার জন্য গুরুত্বপূর্ণ।

---

# 46. Optional Chaining `?.`

Nested object access করার সময় property missing হলে error এড়াতে:

```javascript
const user = {
    name: "Atiar"
};

console.log(user.address?.city);
```

Output:

```text
undefined
```

সরাসরি:

```javascript
user.address.city
```

করলে error হতে পারে, কারণ `address` নেই।

---

# 47. Nullish Coalescing `??`

Value `null` বা `undefined` হলে default value দিতে:

```javascript
const user = {
    name: "Atiar"
};

const city = user.city ?? "Dhaka";

console.log(city);
```

Output:

```text
Dhaka
```

---

# 48. Optional Chaining + Nullish Coalescing

API data-এর ক্ষেত্রে খুব common:

```javascript
const user = {
    name: "Atiar"
};

const city = user.address?.city ?? "Unknown";

console.log(city);
```

Output:

```text
Unknown
```

React/API development-এ এটা অনেক কাজে লাগবে।

---

# 49. Object Property Rename

ধরো API থেকে:

```javascript
const user = {
    first_name: "Atiar",
    email_address: "atiar@example.com"
};
```

Destructuring:

```javascript
const {
    first_name: firstName,
    email_address: email
} = user;
```

এখন:

```javascript
console.log(firstName);
console.log(email);
```

---

# 50. Object থেকে Property বাদ দেওয়া

Modern JavaScript-এ destructuring + rest ব্যবহার করা যায়।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};

const { email, ...publicUser } = user;

console.log(publicUser);
```

Result:

```javascript
{
    name: "Atiar",
    age: 25
}
```

এটা API response বা data transformation-এ useful।

---

# 51. Object-এর মধ্যে Function

```javascript
const calculator = {
    add(a, b) {
        return a + b;
    },

    subtract(a, b) {
        return a - b;
    },

    multiply(a, b) {
        return a * b;
    }
};

console.log(calculator.add(10, 5));
console.log(calculator.subtract(10, 5));
console.log(calculator.multiply(10, 5));
```

Output:

```text
15
5
50
```

---

# 52. Real-world User Object

একটি realistic example:

```javascript
const user = {
    id: 1,
    name: "Atiar",
    email: "atiar@example.com",
    age: 25,
    is_active: true,

    skills: [
        "Python",
        "Django",
        "JavaScript",
        "React"
    ],

    address: {
        city: "Dhaka",
        country: "Bangladesh"
    },

    greet() {
        return `Hello, ${this.name}`;
    }
};
```

Access:

```javascript
user.name
```

```javascript
user.skills[0]
```

```javascript
user.address.city
```

```javascript
user.greet()
```

---

# 53. API Response-এর মতো Object

Backend থেকে React-এ এমন data আসতে পারে:

```javascript
const response = {
    id: 1,
    name: "Laptop",
    price: 80000,

    category: {
        id: 5,
        name: "Electronics"
    },

    images: [
        "image1.jpg",
        "image2.jpg"
    ]
};
```

Product name:

```javascript
response.name
```

Category:

```javascript
response.category.name
```

First image:

```javascript
response.images[0]
```

এখানে Object + Array একসাথে কাজ করছে।

---

# 54. Object Equality — Important

এই দুই object দেখতে একই:

```javascript
const user1 = {
    name: "Atiar"
};

const user2 = {
    name: "Atiar"
};
```

কিন্তু:

```javascript
console.log(user1 === user2);
```

Output:

```text
false
```

কারণ দুইটি আলাদা object reference।

---

# 55. Reference Concept

```javascript
const user1 = {
    name: "Atiar"
};

const user2 = user1;

user2.name = "Rahim";

console.log(user1.name);
```

Output:

```text
Rahim
```

কারণ `user1` এবং `user2` একই object reference করছে।

```text
user1 ─────┐
           ↓
        Object
           ↑
user2 ─────┘
```

---

# 56. Object Copy — Shallow Copy

```javascript
const user1 = {
    name: "Atiar",
    age: 25
};

const user2 = {
    ...user1
};

user2.name = "Rahim";

console.log(user1.name);
console.log(user2.name);
```

Output:

```text
Atiar
Rahim
```

কিন্তু nested object থাকলে বিষয়টি একটু different।

---

# 57. Shallow Copy-এর Nested Problem

```javascript
const user1 = {
    name: "Atiar",

    address: {
        city: "Dhaka"
    }
};

const user2 = {
    ...user1
};

user2.address.city = "Chittagong";

console.log(user1.address.city);
```

Output:

```text
Chittagong
```

কারণ spread শুধু **shallow copy** করে।

---

# 58. Deep Copy

Simple JSON-compatible data-এর ক্ষেত্রে:

```javascript
const user2 = JSON.parse(
    JSON.stringify(user1)
);
```

Modern JavaScript-এ:

```javascript
const user2 = structuredClone(user1);
```

এতে nested object-ও আলাদা copy হয়।

---

# 59. Object-এর সবচেয়ে Important Operations

একটা object নিয়ে সাধারণ CRUD:

### Create

```javascript
const user = {
    name: "Atiar",
    age: 25
};
```

### Read

```javascript
console.log(user.name);
```

### Update

```javascript
user.age = 26;
```

### Delete

```javascript
delete user.age;
```

অর্থাৎ:

```text
Create
  ↓
Read
  ↓
Update
  ↓
Delete
```

---

# 60. Object Methods Cheat Sheet

| Operation                 | Method / Syntax         |
| ------------------------- | ----------------------- |
| Create                    | `{}`                    |
| Read                      | `obj.name`              |
| Dynamic Read              | `obj[key]`              |
| Add                       | `obj.key = value`       |
| Update                    | `obj.key = newValue`    |
| Delete                    | `delete obj.key`        |
| Check property            | `"key" in obj`          |
| Own property check        | `Object.hasOwn()`       |
| Get keys                  | `Object.keys()`         |
| Get values                | `Object.values()`       |
| Get entries               | `Object.entries()`      |
| Merge                     | `{ ...obj1, ...obj2 }`  |
| Copy                      | `{ ...obj }`            |
| Merge/copy                | `Object.assign()`       |
| Freeze                    | `Object.freeze()`       |
| Seal                      | `Object.seal()`         |
| Clone                     | `structuredClone()`     |
| Create from prototype     | `Object.create()`       |
| Iterate                   | `for...in`              |
| Iterate pairs             | `Object.entries()`      |
| Destructure               | `const { name } = obj`  |
| Remove during destructure | `{ name, ...rest }`     |
| Safe nested access        | `obj?.address?.city`    |
| Default value             | `value ?? defaultValue` |

---

# 🧠 Array vs Object

এই distinction খুব ভালোভাবে বুঝবে।

### Array

একই ধরনের multiple data-এর collection:

```javascript
const skills = [
    "Python",
    "Django",
    "React"
];
```

Access:

```javascript
skills[0]
```

---

### Object

একটি entity-এর বিভিন্ন properties:

```javascript
const user = {
    name: "Atiar",
    age: 25,
    email: "atiar@example.com"
};
```

Access:

```javascript
user.name
```

---

# 🔥 সবচেয়ে গুরুত্বপূর্ণ 15টি Object Concept

তোমার JavaScript mastery-এর জন্য এগুলো অবশ্যই practice করবে:

```text
1. Object creation
2. Properties & values
3. Dot notation
4. Bracket notation
5. Dynamic property access
6. Add / Update / Delete
7. Nested objects
8. Objects + Arrays
9. Methods
10. this
11. Destructuring
12. Spread / Rest
13. Object.keys()
14. Object.values()
15. Object.entries()
```

তারপর advanced:

```text
16. Optional chaining
17. Nullish coalescing
18. Object.assign()
19. Object.freeze()
20. Object.seal()
21. Shallow vs Deep Copy
22. References
23. Prototype / Object.create()
```

### সবচেয়ে গুরুত্বপূর্ণ mental model

```text
Object
│
├── Properties
│     ├── key
│     └── value
│
├── Methods
│     └── function
│
├── Nested Object
│
├── Array
│
└── Operations
      ├── Create
      ├── Read
      ├── Update
      ├── Delete
      ├── Destructure
      ├── Copy
      ├── Merge
      └── Iterate
```

এগুলো ভালোভাবে আয়ত্ত করলে **React-এর props, state, API response, form data, JSON এবং Django REST Framework থেকে আসা data** বোঝা অনেক সহজ হয়ে যাবে।

---
# JavaScript: Working With Nested Arrays & Objects

এখন আমরা **Array + Object একসাথে nested অবস্থায় কীভাবে কাজ করে** সেটা শিখব।

এটা JavaScript এবং React-এর জন্য খুব গুরুত্বপূর্ণ, কারণ Django REST API থেকে সাধারণত এমন data আসে:

```javascript
const response = {
    id: 1,
    name: "Laptop",
    price: 80000,
    category: {
        id: 5,
        name: "Electronics"
    },
    images: [
        "laptop-1.jpg",
        "laptop-2.jpg"
    ]
};
```

এখানে একসাথে আছে:

```text
Object
├── Object → category
└── Array  → images
```

---

# 1. Nested Object কী?

একটি object-এর ভিতরে আরেকটি object থাকলে তাকে nested object বলা হয়।

```javascript
const user = {
    name: "Atiar",

    address: {
        city: "Dhaka",
        country: "Bangladesh"
    }
};
```

এখানে:

```text
user
 ├── name
 └── address
       ├── city
       └── country
```

---

# 2. Nested Object Access

প্রথমে `address`:

```javascript
console.log(user.address);
```

Output:

```javascript
{
    city: "Dhaka",
    country: "Bangladesh"
}
```

City:

```javascript
console.log(user.address.city);
```

Output:

```text
Dhaka
```

Country:

```javascript
console.log(user.address.country);
```

Output:

```text
Bangladesh
```

---

# 3. Multiple Level Nested Object

Object আরও গভীরভাবে nested হতে পারে।

```javascript
const user = {
    name: "Atiar",

    address: {
        location: {
            city: "Dhaka",
            area: "Mirpur"
        }
    }
};
```

Access:

```javascript
console.log(user.address.location.city);
```

Output:

```text
Dhaka
```

Structure:

```text
user
 │
```


---
# JavaScript Loops & Iteration — Complete Guide

JavaScript-এ **loop** ব্যবহার করি যখন একই ধরনের কাজ বারবার করতে হয়।

যেমন:

```javascript
console.log("Hello");
console.log("Hello");
console.log("Hello");
console.log("Hello");
console.log("Hello");
```

এভাবে না লিখে:

```javascript
for (let i = 0; i < 5; i++) {
    console.log("Hello");
}
```

এটাই loop-এর মূল কাজ।

---

# 1. কেন Loop ব্যবহার করব?

ধরো আমাদের 100 জন user আছে:

```javascript
const users = [
    "Atiar",
    "Rahim",
    "Karim",
    // আরও 97 জন
];
```

প্রত্যেক user-এর নাম print করতে loop ব্যবহার করব:

```javascript
for (const user of users) {
    console.log(user);
}
```

---

# 2. JavaScript-এ প্রধান Loops

JavaScript-এ গুরুত্বপূর্ণ loopগুলো:

```text
1. for
2. while
3. do...while
4. for...of
5. for...in
```

আর array-এর ক্ষেত্রে iteration-এর জন্য:

```text
6. forEach()
7. map()
8. filter()
9. find()
10. some()
11. every()
12. reduce()
```

শেষেরগুলো technically সব loop syntax না হলেও **iteration/data processing**-এর জন্য খুব গুরুত্বপূর্ণ।

---

# 3. `for` Loop

সবচেয়ে basic এবং গুরুত্বপূর্ণ loop।

Syntax:

```javascript
for (initialization; condition; increment) {
    // code
}
```

Example:

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

Output:

```text
0
1
2
3
4
```

### Flow

```text
let i = 0
    ↓
i < 5 ?
    ↓
Yes
    ↓
code execute
    ↓
i++
    ↓
condition check
```

---

# 4. `for` Loop-এর তিনটি অংশ

```javascript
for (
    let i = 0;      // initialization
    i < 5;          // condition
    i++             // update
) {
    console.log(i);
}
```

### Initialization

Loop শুরু হওয়ার আগে একবার execute হয়।

```javascript
let i = 0;
```

### Condition

প্রতিবার check হয়।

```javascript
i < 5
```

### Update

প্রতিবার loop body শেষ হওয়ার পর execute হয়।

```javascript
i++;
```

---

# 5. 1 থেকে 10 পর্যন্ত Print

```javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);
}
```

Output:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# 6. Reverse Loop

10 থেকে 1:

```javascript
for (let i = 10; i >= 1; i--) {
    console.log(i);
}
```

Output:

```text
10
9
8
...
1
```

---

# 7. Even Numbers

```javascript
for (let i = 1; i <= 10; i++) {

    if (i % 2 === 0) {
        console.log(i);
    }

}
```

Output:

```text
2
4
6
8
10
```

---

# 8. Odd Numbers

```javascript
for (let i = 1; i <= 10; i++) {

    if (i % 2 !== 0) {
        console.log(i);
    }

}
```

Output:

```text
1
3
5
7
9
```

---

# 9. Array-এর সাথে `for`

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

Output:

```text
Apple
Mango
Banana
```

এখানে:

```javascript
fruits.length
```

ব্যবহার করার কারণে array যত বড়ই হোক loop কাজ করবে।

---

# 10. Array Index সহ Loop

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

for (let i = 0; i < fruits.length; i++) {
    console.log(i, fruits[i]);
}
```

Output:

```text
0 Apple
1 Mango
2 Banana
```

---

# 11. Nested `for` Loop

একটি loop-এর ভিতরে আরেকটি loop থাকলে nested loop।

```javascript
for (let i = 1; i <= 3; i++) {

    for (let j = 1; j <= 3; j++) {
        console.log(i, j);
    }

}
```

Output:

```text
1 1
1 2
1 3
2 1
2 2
2 3
3 1
3 2
3 3
```

Nested loop সাধারণত:

- matrix
    
- table
    
- grid
    
- nested data
    

এর জন্য ব্যবহার হয়।

---

# 12. Multiplication Table

```javascript
const number = 5;

for (let i = 1; i <= 10; i++) {
    console.log(`${number} × ${i} = ${number * i}`);
}
```

Output:

```text
5 × 1 = 5
5 × 2 = 10
5 × 3 = 15
...
5 × 10 = 50
```

---

# 13. `while` Loop

যখন condition true থাকবে, তখন loop চলবে।

Syntax:

```javascript
while (condition) {
    // code
}
```

Example:

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);

    i++;
}
```

Output:

```text
1
2
3
4
5
```

---

# 14. `while` Loop-এর Flow

```text
        condition
           ↓
       true ?
      /       \
    yes        no
     ↓          ↓
   execute     stop
     ↓
   update
     ↓
 condition
```

⚠️ `while` loop-এ update ভুলে গেলে infinite loop হতে পারে।

ভুল:

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
}
```

এখানে `i` কখনো change হচ্ছে না।

---

# 15. `while` কখন ব্যবহার করব?

যখন iteration-এর exact সংখ্যা আগে থেকে জানা নেই।

Example:

```javascript
let password = "";

while (password !== "1234") {
    // password নেওয়ার logic
}
```

অর্থাৎ:

> "কতবার চলবে জানি না, কিন্তু যতক্ষণ condition true থাকবে ততক্ষণ চলবে।"

---

# 16. `do...while`

`do...while`-এর বিশেষত্ব হলো **কমপক্ষে একবার execute হবেই**।

Syntax:

```javascript
do {
    // code
} while (condition);
```

Example:

```javascript
let i = 1;

do {
    console.log(i);

    i++;
} while (i <= 5);
```

Output:

```text
1
2
3
4
5
```

---

# 17. `while` vs `do...while`

### while

```javascript
let i = 10;

while (i < 5) {
    console.log(i);
}
```

কিছুই print হবে না।

কারণ শুরুতেই:

```text
10 < 5 → false
```

### do...while

```javascript
let i = 10;

do {
    console.log(i);
} while (i < 5);
```

Output:

```text
10
```

কারণ body আগে execute হয়েছে।

### মনে রাখো:

```text
while       → condition first
do...while  → code first
```

---

# 18. `for...of`

Array বা iterable-এর **values** পাওয়ার জন্য খুব useful।

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

for (const fruit of fruits) {
    console.log(fruit);
}
```

Output:

```text
Apple
Mango
Banana
```

এটা:

```javascript
for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
```

এর cleaner version হিসেবে অনেক সময় ব্যবহার করা যায়।

---

# 19. `for...of` with String

String-ও iterable:

```javascript
const name = "Atiar";

for (const character of name) {
    console.log(character);
}
```

Output:

```text
A
t
i
a
r
```

---

# 20. `for...of` with Set

```javascript
const numbers = new Set([10, 20, 30]);

for (const number of numbers) {
    console.log(number);
}
```

Output:

```text
10
20
30
```

---

# 21. `for...in`

`for...in` সাধারণত **object-এর keys/properties** iterate করার জন্য ব্যবহার করা হয়।

```javascript
const user = {
    name: "Atiar",
    age: 25,
    city: "Dhaka"
};

for (const key in user) {
    console.log(key);
}
```

Output:

```text
name
age
city
```

---

# 22. `for...in` দিয়ে Value

```javascript
for (const key in user) {
    console.log(key, user[key]);
}
```

Output:

```text
name Atiar
age 25
city Dhaka
```

খেয়াল করো:

```javascript
user[key]
```

এখানে bracket notation ব্যবহার করা হয়েছে।

---

# 23. `for...in` vs `for...of`

এটা খুব ভালোভাবে বুঝবে।

### `for...in`

```javascript
const fruits = ["Apple", "Mango", "Banana"];

for (const index in fruits) {
    console.log(index);
}
```

Output:

```text
0
1
2
```

### `for...of`

```javascript
for (const fruit of fruits) {
    console.log(fruit);
}
```

Output:

```text
Apple
Mango
Banana
```

### সহজভাবে:

```text
for...in → keys / indexes
for...of → values
```

Object:

```javascript
for (const key in user) {
    console.log(key);
}
```

Array:

```javascript
for (const fruit of fruits) {
    console.log(fruit);
}
```

---

# 24. `forEach()`

Array-এর প্রতিটি element-এর জন্য function execute করে।

```javascript
const numbers = [10, 20, 30];

numbers.forEach(function(number) {
    console.log(number);
});
```

Output:

```text
10
20
30
```

Arrow function:

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

---

# 25. `forEach()` Index সহ

```javascript
const fruits = [
    "Apple",
    "Mango",
    "Banana"
];

fruits.forEach((fruit, index) => {
    console.log(index, fruit);
});
```

Output:

```text
0 Apple
1 Mango
2 Banana
```

Callback-এর parameters:

```text
(element, index, array)
```

Example:

```javascript
fruits.forEach((fruit, index, array) => {
    console.log(fruit);
    console.log(index);
    console.log(array);
});
```

---

# 26. `forEach()` কী Return করে?

```javascript
const numbers = [1, 2, 3];

const result = numbers.forEach(number => {
    return number * 2;
});

console.log(result);
```

Output:

```text
undefined
```

তাই নতুন array তৈরি করতে `forEach()` নয়, `map()` ব্যবহার করবে।

---

# 27. `map()`

প্রতিটি element transform করে **নতুন array return** করে।

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => {
    return number * 2;
});

console.log(doubled);
```

Output:

```text
[2, 4, 6, 8]
```

---

# 28. `forEach()` vs `map()`

### forEach

```javascript
numbers.forEach(number => {
    console.log(number * 2);
});
```

মূল উদ্দেশ্য:

```text
iterate / side effect
```

### map

```javascript
const result = numbers.map(
    number => number * 2
);
```

মূল উদ্দেশ্য:

```text
transform → new array
```

---

# 29. `filter()`

Condition অনুযায়ী elements select করে।

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(
    number => number % 2 === 0
);

console.log(evenNumbers);
```

Output:

```text
[2, 4, 6]
```

---

# 30. `find()`

Condition satisfy করা **প্রথম element** return করে।

```javascript
const numbers = [10, 20, 30, 40];

const result = numbers.find(
    number => number > 20
);

console.log(result);
```

Output:

```text
30
```

শুধু প্রথম match:

```text
10 ❌
20 ❌
30 ✅ → return
40 → আর check করে না
```

---

# 31. `findIndex()`

প্রথম matching element-এর index return করে।

```javascript
const numbers = [10, 20, 30, 40];

const index = numbers.findIndex(
    number => number > 20
);

console.log(index);
```

Output:

```text
2
```

---

# 32. `some()`

কমপক্ষে একটি element condition satisfy করলে `true`।

```javascript
const numbers = [1, 3, 5, 8];

const result = numbers.some(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

কারণ `8` even।

---

# 33. `every()`

সব element condition satisfy করলে `true`।

```javascript
const numbers = [2, 4, 6, 8];

const result = numbers.every(
    number => number % 2 === 0
);

console.log(result);
```

Output:

```text
true
```

---

# 34. `reduce()`

অনেকগুলো value থেকে একটি final value তৈরি করে।

```javascript
const numbers = [10, 20, 30, 40];

const total = numbers.reduce(
    (sum, number) => {
        return sum + number;
    },
    0
);

console.log(total);
```

Output:

```text
100
```

Flow:

```text
0 + 10 = 10
10 + 20 = 30
30 + 30 = 60
60 + 40 = 100
```

---

# 35. Nested Array Loop

```javascript
const matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];
```

Nested `for`:

```javascript
for (let i = 0; i < matrix.length; i++) {

    for (let j = 0; j < matrix[i].length; j++) {
        console.log(matrix[i][j]);
    }

}
```

Output:

```text
1
2
3
4
5
6
7
8
9
```

---

# 36. Nested Array with `for...of`

আরও clean:

```javascript
for (const row of matrix) {

    for (const number of row) {
        console.log(number);
    }

}
```

---

# 37. Nested Objects

```javascript
const user = {
    name: "Atiar",

    address: {
        city: "Dhaka",
        country: "Bangladesh"
    }
};
```

`for...in` দিয়ে:

```javascript
for (const key in user.address) {
    console.log(
        key,
        user.address[key]
    );
}
```

Output:

```text
city Dhaka
country Bangladesh
```

---

# 38. Array of Objects

Real-world application-এ সবচেয়ে বেশি দেখা যাবে:

```javascript
const users = [
    {
        id: 1,
        name: "Atiar",
        age: 25
    },
    {
        id: 2,
        name: "Rahim",
        age: 30
    },
    {
        id: 3,
        name: "Karim",
        age: 22
    }
];
```

---

# 39. Array of Objects with `for...of`

```javascript
for (const user of users) {
    console.log(user.name);
}
```

Output:

```text
Atiar
Rahim
Karim
```

---

# 40. Array of Objects with `forEach()`

```javascript
users.forEach(user => {
    console.log(user.name);
});
```

---

# 41. Array of Objects with `map()`

শুধু names:

```javascript
const names = users.map(
    user => user.name
);

console.log(names);
```

Output:

```text
["Atiar", "Rahim", "Karim"]
```

---

# 42. Array of Objects with `filter()`

যাদের age 25-এর বেশি:

```javascript
const result = users.filter(
    user => user.age > 25
);

console.log(result);
```

Result:

```javascript
[
    {
        id: 2,
        name: "Rahim",
        age: 30
    }
]
```

---

# 43. Array of Objects with `find()`

```javascript
const user = users.find(
    user => user.id === 2
);

console.log(user);
```

Output:

```javascript
{
    id: 2,
    name: "Rahim",
    age: 30
}
```

---

# 44. `break`

Loop সম্পূর্ণভাবে stop করতে `break` ব্যবহার করি।

```javascript
for (let i = 1; i <= 10; i++) {

    if (i === 5) {
        break;
    }

    console.log(i);
}
```

Output:

```text
1
2
3
4
```

`5` এ পৌঁছে loop বন্ধ।

---

# 45. `continue`

Current iteration skip করে next iteration-এ যায়।

```javascript
for (let i = 1; i <= 5; i++) {

    if (i === 3) {
        continue;
    }

    console.log(i);
}
```

Output:

```text
1
2
4
5
```

`3` skip হয়েছে।

---

# 46. `break` vs `continue`

```text
break
 ↓
পুরো loop বন্ধ
```

```text
continue
 ↓
শুধু current iteration skip
 ↓
next iteration
```

---

# 47. `break` with `while`

```javascript
let i = 1;

while (i <= 10) {

    if (i === 5) {
        break;
    }

    console.log(i);

    i++;
}
```

Output:

```text
1
2
3
4
```

---

# 48. `continue` with `while`

```javascript
let i = 0;

while (i < 5) {

    i++;

    if (i === 3) {
        continue;
    }

    console.log(i);
}
```

Output:

```text
1
2
4
5
```

---

# 49. Labeled Loop

Nested loop থেকে outer loop break করতে label ব্যবহার করা যায়।

```javascript
outerLoop:
for (let i = 1; i <= 3; i++) {

    for (let j = 1; j <= 3; j++) {

        if (i === 2 && j === 2) {
            break outerLoop;
        }

        console.log(i, j);
    }
}
```

`outerLoop` পুরো outer loop বন্ধ করে দেয়।

এটা সাধারণ code-এ খুব কম লাগে, তবে concept জানা ভালো।

---

# 50. Infinite Loop

এই code dangerous:

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
}
```

কারণ `i` update হচ্ছে না।

সঠিক:

```javascript
let i = 1;

while (i <= 5) {
    console.log(i);
    i++;
}
```

---

# 51. Loop-এর ভিতরে Function

```javascript
function greet(name) {
    console.log(`Hello ${name}`);
}

const users = [
    "Atiar",
    "Rahim",
    "Karim"
];

for (const user of users) {
    greet(user);
}
```

Output:

```text
Hello Atiar
Hello Rahim
Hello Karim
```

---

# 52. Real-world Cart Example

```javascript
const cart = [
    {
        name: "Laptop",
        price: 80000,
        quantity: 1
    },
    {
        name: "Mouse",
        price: 1000,
        quantity: 2
    },
    {
        name: "Keyboard",
        price: 3000,
        quantity: 1
    }
];
```

প্রতিটি product-এর total:

```javascript
cart.forEach(item => {
    const total = item.price * item.quantity;

    console.log(
        `${item.name}: ${total}`
    );
});
```

Output:

```text
Laptop: 80000
Mouse: 2000
Keyboard: 3000
```

---

# 53. Cart-এর Grand Total

`reduce()`:

```javascript
const total = cart.reduce(
    (sum, item) => {
        return sum + item.price * item.quantity;
    },
    0
);

console.log(total);
```

Output:

```text
85000
```

---

# 54. React-এ সবচেয়ে Common Loop

React-এ API থেকে products এলে:

```javascript
const products = [
    {
        id: 1,
        name: "Laptop"
    },
    {
        id: 2,
        name: "Mouse"
    }
];
```

Render:

```jsx
{products.map(product => (
    <div key={product.id}>
        {product.name}
    </div>
))}
```

Output:

```text
Laptop
Mouse
```

তাই React শেখার জন্য:

```text
map()
filter()
find()
some()
every()
reduce()
```

খুব ভালোভাবে জানতে হবে।

---

# 55. Method Chaining

Multiple iteration methods একসাথে ব্যবহার করা যায়।

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 2)
    .reduce((sum, number) => sum + number, 0);

console.log(result);
```

Flow:

```text
[1,2,3,4,5,6]
       ↓
filter
[2,4,6]
       ↓
map
[4,8,12]
       ↓
reduce
24
```

---

# 56. কোন Loop কখন ব্যবহার করব?

এটা সবচেয়ে গুরুত্বপূর্ণ অংশ।

|Situation|Best Choice|
|---|---|
|নির্দিষ্ট সংখ্যক বার loop|`for`|
|condition-এর উপর নির্ভর|`while`|
|অন্তত একবার execute দরকার|`do...while`|
|Array-এর values|`for...of`|
|Object-এর keys|`for...in`|
|শুধু প্রতিটি item-এর কাজ|`forEach()`|
|নতুন array তৈরি/transform|`map()`|
|কিছু item select|`filter()`|
|প্রথম matching item|`find()`|
|প্রথম matching index|`findIndex()`|
|অন্তত একটি match|`some()`|
|সবগুলো match|`every()`|
|total/aggregate|`reduce()`|

---

# 57. `for` vs `for...of` vs `forEach`

ধরো:

```javascript
const numbers = [10, 20, 30];
```

### `for`

```javascript
for (let i = 0; i < numbers.length; i++) {
    console.log(numbers[i]);
}
```

**Index দরকার হলে ভালো।**

---

### `for...of`

```javascript
for (const number of numbers) {
    console.log(number);
}
```

**শুধু value দরকার হলে clean।**

---

### `forEach`

```javascript
numbers.forEach(number => {
    console.log(number);
});
```

**Array-এর প্রতিটি item-এর উপর side effect চালাতে ভালো।**

---

# 58. `forEach()`-এর একটি গুরুত্বপূর্ণ Limitation

`break` করা যায় না:

```javascript
numbers.forEach(number => {

    if (number === 20) {
        break; // ❌ SyntaxError
    }

});
```

যদি early stop দরকার হয়:

```javascript
for (const number of numbers) {

    if (number === 20) {
        break;
    }

    console.log(number);
}
```

---

# 59. `map()`-এ `break` করা যায়?

না।

```javascript
numbers.map(number => {
    // break ❌
});
```

যদি condition অনুযায়ী কিছু item বাদ দিতে চাও:

```javascript
filter()
```

ব্যবহার করবে।

যদি প্রথম match পেলেই stop করতে চাও:

```javascript
find()
```

ব্যবহার করবে।

---

# 60. Array Iteration-এর Mental Model

এই diagram-টা মনে রাখো:

```text
                    ARRAY
                      │
          ┌───────────┼───────────┐
          │           │           │
       Iterate      Select      Transform
          │           │           │
      forEach()    filter()     map()
      for...of       find()      
      for            some()
                     every()
          │
          └──────────────┐
                         ↓
                     Aggregate
                         │
                      reduce()
```

---

# 🔥 Most Important Concepts

তোমার JavaScript mastery-এর জন্য এই sequence follow করো:

### Level 1 — Basic Loops

```javascript
for
while
do...while
```

### Level 2 — Modern Iteration

```javascript
for...of
for...in
```

### Level 3 — Array Methods

```javascript
forEach()
map()
filter()
find()
findIndex()
some()
every()
reduce()
```

### Level 4 — Control

```javascript
break
continue
```

### Level 5 — Real-world Data

```javascript
Array of Objects
Nested Arrays
Nested Objects
API Response
Object + Array combination
Method chaining
```

---

# 🧠 One Example That Combines Everything

ধরো Django API থেকে products এসেছে:

```javascript
const products = [
    {
        id: 1,
        name: "Laptop",
        price: 80000,
        category: {
            name: "Electronics"
        }
    },
    {
        id: 2,
        name: "Mouse",
        price: 1000,
        category: {
            name: "Electronics"
        }
    },
    {
        id: 3,
        name: "Shirt",
        price: 1500,
        category: {
            name: "Fashion"
        }
    }
];
```

### সব product name:

```javascript
const names = products.map(
    product => product.name
);
```

### শুধু Electronics:

```javascript
const electronics = products.filter(
    product =>
        product.category.name === "Electronics"
);
```

### 5000-এর বেশি price:

```javascript
const expensive = products.filter(
    product => product.price > 5000
);
```

### ID 2-এর product:

```javascript
const product = products.find(
    product => product.id === 2
);
```

### কোনো product-এর price 50000-এর বেশি কিনা:

```javascript
const exists = products.some(
    product => product.price > 50000
);
```

### সব product-এর price 500-এর বেশি কিনা:

```javascript
const allExpensive = products.every(
    product => product.price > 500
);
```

### সব product-এর total price:

```javascript
const total = products.reduce(
    (sum, product) => sum + product.price,
    0
);
```

এখানেই তুমি **Object + Nested Object + Array + Iteration + Array Methods** একসাথে ব্যবহার করছ।

---

## 🎯 Final Cheat Sheet

```text
FOR
→ নির্দিষ্ট iteration

WHILE
→ condition true থাকা পর্যন্ত

DO...WHILE
→ অন্তত একবার execute

FOR...OF
→ values

FOR...IN
→ object keys

forEach()
→ প্রতিটি item-এর উপর কাজ

map()
→ নতুন array তৈরি

filter()
→ matching items

find()
→ first matching item

findIndex()
→ first matching index

some()
→ অন্তত একটি true?

every()
→ সবগুলো true?

reduce()
→ multiple values → one value

break
→ পুরো loop বন্ধ

continue
→ current iteration skip
```

**JavaScript → React যাওয়ার জন্য সবচেয়ে বেশি গুরুত্ব দাও:**  
`for...of`, `forEach()`, `map()`, `filter()`, `find()`, `some()`, `every()`, `reduce()` এবং **Array of Objects**। এগুলো আয়ত্ত করলে API data নিয়ে কাজ করা অনেক সহজ হয়ে যাবে।


----
### 1. Named Export

`add.js`:

```js
export const add = (a, b) => {
  return a + b;
};
```

Import:

```js
import { add } from './add.js';

console.log(add(2, 4));
```

এখানে `{ add }` দিতে হবে, কারণ এটা **named export**।

---

### 2. Default Export

`add.js`:

```js
const add = (a, b) => {
  return a + b;
};

export default add;
```

Import:

```js
import add from './add.js';

console.log(add(2, 4));
```

এখানে `{ }` লাগবে না।

আর default export-এর ক্ষেত্রে import করার সময় **নাম নিজের ইচ্ছামতো দিতে পারো**:

```js
import sum from './add.js';

console.log(sum(2, 4));
```

এটাও valid।

---

### 3. একই file-এ Named + Default দুটোই

`math.js`:

```js
export const add = (a, b) => a + b;

const multiply = (a, b) => a * b;

export default multiply;
```

Import:

```js
import multiply, { add } from './math.js';

console.log(add(2, 4));
console.log(multiply(2, 4));
```

অর্থাৎ shortcut মনে রাখো:

```js
// Named
export { add };
import { add } from './file.js';

// Default
export default add;
import add from './file.js';

// Both
import add, { subtract, multiply } from './file.js';
```

**Rule:** `default` → `{}` নেই  
**named** → `{}` আছে।

---


# Dom (Dcument Object Model)

----

অবশ্যই। এবার আমরা **JavaScript DOM (Document Object Model)** একদম beginner থেকে advanced পর্যন্ত শিখব। DOM ভালোভাবে বুঝলে vanilla JavaScript দিয়ে webpage dynamically control করতে পারবে এবং পরে React-এর concept যেমন state, event, rendering বুঝতেও সুবিধা হবে।

# JavaScript DOM — Complete Tutorial

---

# 1. DOM কী?

**DOM = Document Object Model**

Browser যখন একটি HTML page load করে, তখন HTML document-কে একটি **tree structure** হিসেবে memory-তে তৈরি করে।

ধরো HTML:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>

<body>
    <h1>Hello Atiar</h1>

    <p>Welcome to JavaScript</p>

    <button>Click Me</button>
</body>
</html>
```

Browser এটাকে roughly এভাবে দেখে:

```text
Document
   │
   └── html
       │
       ├── head
       │   └── title
       │
       └── body
           ├── h1
           ├── p
           └── button
```

এই tree-এর প্রতিটি HTML element হলো একটি **DOM Node**।

---

# 2. DOM কেন দরকার?

JavaScript দিয়ে HTML:

* select
* change
* add
* delete
* style
* attribute modify
* event handle
* form data read
* dynamically generate

করতে DOM ব্যবহার করি।

উদাহরণ:

```html
<h1 id="title">Hello</h1>
```

JavaScript:

```javascript
const title = document.getElementById("title");

title.textContent = "Hello JavaScript";
```

Browser-এ:

```text
Hello
```

থেকে:

```text
Hello JavaScript
```

হয়ে যাবে।

---

# 3. `document` কী?

DOM-এর main entry point হলো:

```javascript
document
```

যেমন:

```javascript
console.log(document);
```

এটা পুরো HTML document represent করে।

---

# 4. DOM-এর Important Objects

```text
window
  │
  └── document
       │
       ├── html
       ├── head
       └── body
```

Common:

```javascript
window
document
document.body
document.head
```

---

# 5. Element Select করা

DOM-এর সবচেয়ে important অংশ হলো **element selection**।

প্রধান methods:

```text
getElementById()
getElementsByClassName()
getElementsByTagName()
querySelector()
querySelectorAll()
```

---

# 6. `getElementById()`

HTML:

```html
<h1 id="title">Hello</h1>
```

JavaScript:

```javascript
const title = document.getElementById("title");

console.log(title);
```

ID-এর আগে `#` দিতে হবে না।

```javascript
document.getElementById("title");
```

---

# 7. Element-এর Text Change

```javascript
const title = document.getElementById("title");

title.textContent = "Welcome!";
```

HTML:

```html
<h1 id="title">Welcome!</h1>
```

---

# 8. `innerText`

```javascript
title.innerText = "Hello World";
```

এটাও visible text change করে।

Basic use-এর ক্ষেত্রে:

```text
textContent
innerText
```

দুটোই দেখবে।

তবে `textContent` DOM-এর text content নিয়ে কাজ করে এবং সাধারণত predictable; `innerText` rendered/visible text-এর behavior অনুসরণ করে।

---

# 9. `innerHTML`

HTML content insert করতে:

```javascript
const box = document.getElementById("box");

box.innerHTML = "<h2>Hello</h2>";
```

এখন `box`-এর ভিতরে সত্যিকারের `<h2>` element তৈরি হবে।

---

# 10. `textContent` vs `innerHTML`

```javascript
box.textContent = "<h2>Hello</h2>";
```

Browser দেখাবে:

```text
<h2>Hello</h2>
```

কিন্তু:

```javascript
box.innerHTML = "<h2>Hello</h2>";
```

Browser দেখাবে বড় heading:

```text
Hello
```

### মনে রাখবে:

```text
textContent → text
innerHTML   → HTML
```

---

# 11. `querySelector()`

CSS selector ব্যবহার করে element select করা যায়।

HTML:

```html
<h1 id="title">Hello</h1>
```

```javascript
const title = document.querySelector("#title");
```

Class:

```html
<p class="description">Hello</p>
```

```javascript
const paragraph = document.querySelector(".description");
```

Tag:

```javascript
const paragraph = document.querySelector("p");
```

---

# 12. `querySelector()`-এর বড় সুবিধা

CSS selector-এর মতো লিখতে পারো।

```javascript
document.querySelector("#title");

document.querySelector(".card");

document.querySelector("p");

document.querySelector("div.card");

document.querySelector("ul li");

document.querySelector("input[type='email']");
```

---

# 13. `querySelector()` শুধু প্রথম element দেয়

HTML:

```html
<p class="text">One</p>
<p class="text">Two</p>
<p class="text">Three</p>
```

```javascript
const paragraph = document.querySelector(".text");

console.log(paragraph.textContent);
```

Output:

```text
One
```

শুধু first match।

---

# 14. `querySelectorAll()`

সব matching element select করতে:

```javascript
const paragraphs = document.querySelectorAll(".text");

console.log(paragraphs);
```

এটি একটি **NodeList** return করে।

---

# 15. NodeList Iterate

```javascript
const paragraphs = document.querySelectorAll(".text");

paragraphs.forEach(paragraph => {
    console.log(paragraph.textContent);
});
```

Output:

```text
One
Two
Three
```

---

# 16. `getElementsByClassName()`

```html
<p class="text">One</p>
<p class="text">Two</p>
```

```javascript
const elements =
    document.getElementsByClassName("text");

console.log(elements);
```

এটি একটি **HTMLCollection** return করে।

---

# 17. `getElementsByTagName()`

```javascript
const paragraphs =
    document.getElementsByTagName("p");
```

সব `<p>` element পাবে।

---

# 18. Selector Cheat Sheet

| Selector             | Meaning          |
| -------------------- | ---------------- |
| `#title`             | ID               |
| `.card`              | class            |
| `p`                  | tag              |
| `div p`              | div-এর ভিতরের p  |
| `.card p`            | card-এর ভিতরের p |
| `input[type="text"]` | attribute        |
| `button`             | button           |

---

# 19. DOM Traversal

একটি element থেকে তার:

* parent
* children
* siblings

এর কাছে যাওয়া হলো **DOM traversal**।

---

# 20. `parentElement`

HTML:

```html
<div class="card">
    <h2>Product</h2>
</div>
```

```javascript
const heading = document.querySelector("h2");

console.log(heading.parentElement);
```

Output:

```html
<div class="card">
    <h2>Product</h2>
</div>
```

---

# 21. `children`

```javascript
const card = document.querySelector(".card");

console.log(card.children);
```

Card-এর direct child elements পাবে।

---

# 22. `firstElementChild`

```javascript
const card = document.querySelector(".card");

console.log(card.firstElementChild);
```

---

# 23. `lastElementChild`

```javascript
console.log(card.lastElementChild);
```

---

# 24. `nextElementSibling`

HTML:

```html
<p>One</p>
<p id="two">Two</p>
<p>Three</p>
```

```javascript
const second = document.getElementById("two");

console.log(second.nextElementSibling);
```

Output:

```html
<p>Three</p>
```

---

# 25. `previousElementSibling`

```javascript
console.log(second.previousElementSibling);
```

Output:

```html
<p>One</p>
```

---

# 26. DOM Traversal Example

```html
<div id="parent">

    <h2>Title</h2>

    <p>Paragraph</p>

    <button>Click</button>

</div>
```

```javascript
const parent = document.getElementById("parent");

console.log(parent.children);

console.log(parent.firstElementChild);

console.log(parent.lastElementChild);
```

---

# 27. Attributes

HTML:

```html
<img
    id="profile"
    src="profile.jpg"
    alt="Profile"
>
```

JavaScript দিয়ে attributes access করা যায়।

---

# 28. `getAttribute()`

```javascript
const image = document.getElementById("profile");

console.log(
    image.getAttribute("src")
);
```

Output:

```text
profile.jpg
```

---

# 29. `setAttribute()`

```javascript
image.setAttribute(
    "alt",
    "User Profile"
);
```

---

# 30. `removeAttribute()`

```javascript
image.removeAttribute("alt");
```

---

# 31. `hasAttribute()`

```javascript
console.log(
    image.hasAttribute("src")
);
```

Output:

```text
true
```

---

# 32. Direct Property দিয়ে Attribute

কিছু common attribute সরাসরি access করা যায়।

```javascript
image.src = "new-image.jpg";

image.alt = "New Image";
```

Input:

```javascript
input.value = "Atiar";
```

---

# 33. `className`

HTML:

```html
<div id="box" class="card active">
</div>
```

```javascript
const box = document.getElementById("box");

console.log(box.className);
```

Output:

```text
card active
```

---

# 34. `classList`

Modern DOM manipulation-এ সবচেয়ে useful।

```javascript
box.classList.add("highlight");
```

Remove:

```javascript
box.classList.remove("active");
```

Toggle:

```javascript
box.classList.toggle("dark");
```

Check:

```javascript
box.classList.contains("card");
```

---

# 35. `classList.replace()`

```javascript
box.classList.replace(
    "card",
    "product-card"
);
```

---

# 36. Dynamic Styling

JavaScript দিয়ে inline style change:

```javascript
const title =
    document.getElementById("title");

title.style.color = "red";

title.style.fontSize = "40px";

title.style.backgroundColor = "yellow";
```

---

# 37. Multiple Style Properties

```javascript
box.style.width = "300px";
box.style.padding = "20px";
box.style.border = "1px solid black";
```

---

# 38. Better Way: CSS Class

Instead of:

```javascript
box.style.color = "red";
box.style.backgroundColor = "black";
box.style.padding = "20px";
```

CSS:

```css
.highlight {
    color: red;
    background-color: black;
    padding: 20px;
}
```

JS:

```javascript
box.classList.add("highlight");
```

Real projects-এ class-based styling cleaner।

---

# 39. Creating Elements

এখন DOM-এর সবচেয়ে powerful অংশ।

```javascript
const heading =
    document.createElement("h2");
```

এখন একটি নতুন `<h2>` তৈরি হয়েছে, কিন্তু page-এ এখনো যোগ হয়নি।

---

# 40. Element-এর Text Add

```javascript
heading.textContent = "Hello JavaScript";
```

---

# 41. Element Page-এ Add

```javascript
document.body.appendChild(heading);
```

এখন page-এ:

```html
<h2>Hello JavaScript</h2>
```

যোগ হবে।

---

# 42. `append()`

```javascript
const p = document.createElement("p");

p.textContent = "Hello";

document.body.append(p);
```

`append()` text এবং multiple nodes নিয়েও কাজ করতে পারে।

---

# 43. `prepend()`

Parent-এর শুরুতে add:

```javascript
document.body.prepend(p);
```

---

# 44. `before()`

```javascript
title.before(p);
```

Title-এর আগে paragraph insert হবে।

---

# 45. `after()`

```javascript
title.after(p);
```

Title-এর পরে paragraph insert হবে।

---

# 46. `appendChild()` vs `append()`

```javascript
parent.appendChild(child);
```

একটি Node append করে।

আর:

```javascript
parent.append(
    child,
    "Hello"
);
```

multiple content handle করতে পারে।

---

# 47. Remove Element

Modern:

```javascript
element.remove();
```

Example:

```javascript
const button =
    document.querySelector("button");

button.remove();
```

---

# 48. `removeChild()`

Parent থেকে child remove:

```javascript
parent.removeChild(child);
```

Modern code-এ সরাসরি:

```javascript
child.remove();
```

সাধারণত সহজ।

---

# 49. Replace Element

```javascript
oldElement.replaceWith(newElement);
```

---

# 50. `innerHTML` দিয়ে Dynamic HTML

```javascript
const container =
    document.getElementById("container");

container.innerHTML = `
    <h2>Product</h2>
    <p>Laptop</p>
    <button>Buy</button>
`;
```

---

# ⚠️ 51. `innerHTML` Security

User-এর raw input সরাসরি `innerHTML`-এ বসানো dangerous হতে পারে।

যেমন:

```javascript
container.innerHTML =
    userInput;
```

Untrusted input-এর ক্ষেত্রে XSS vulnerability তৈরি হতে পারে।

Text হলে:

```javascript
container.textContent =
    userInput;
```

ব্যবহার করা safer।

---

# 52. Events কী?

User বা browser-এর কোনো action হলো **event**।

Examples:

```text
click
dblclick
mouseover
mouseout
keydown
keyup
input
change
submit
focus
blur
load
scroll
```

---

# 53. `onclick`

HTML:

```html
<button onclick="sayHello()">
    Click
</button>
```

JS:

```javascript
function sayHello() {
    alert("Hello!");
}
```

কাজ করবে, কিন্তু modern JavaScript-এ HTML-এর মধ্যে JS না রাখাই ভালো।

---

# 54. `addEventListener()`

Recommended:

```html
<button id="btn">
    Click Me
</button>
```

```javascript
const button =
    document.getElementById("btn");

button.addEventListener(
    "click",
    function () {
        alert("Button clicked!");
    }
);
```

---

# 55. Arrow Function দিয়ে Event

```javascript
button.addEventListener(
    "click",
    () => {
        console.log("Clicked");
    }
);
```

---

# 56. Event Object

```javascript
button.addEventListener(
    "click",
    (event) => {
        console.log(event);
    }
);
```

`event` object-এর মধ্যে event সম্পর্কিত information থাকে।

---

# 57. `event.target`

```javascript
button.addEventListener(
    "click",
    (event) => {
        console.log(event.target);
    }
);
```

যে element-এ event হয়েছে সেটি পাওয়া যায়।

---

# 58. Mouse Events

### Click

```javascript
button.addEventListener(
    "click",
    () => {
        console.log("Clicked");
    }
);
```

### Double Click

```javascript
button.addEventListener(
    "dblclick",
    () => {
        console.log("Double clicked");
    }
);
```

### Mouse Enter

```javascript
box.addEventListener(
    "mouseenter",
    () => {
        console.log("Mouse entered");
    }
);
```

### Mouse Leave

```javascript
box.addEventListener(
    "mouseleave",
    () => {
        console.log("Mouse left");
    }
);
```

---

# 59. Keyboard Events

```javascript
document.addEventListener(
    "keydown",
    (event) => {
        console.log(event.key);
    }
);
```

যদি `A` চাপো:

```text
a
```

যদি Enter:

```text
Enter
```

---

# 60. `keyup`

```javascript
document.addEventListener(
    "keyup",
    (event) => {
        console.log(event.key);
    }
);
```

Key release করার সময় execute হবে।

---

# 61. Input Event

HTML:

```html
<input id="username">
```

JS:

```javascript
const input =
    document.getElementById("username");

input.addEventListener(
    "input",
    (event) => {
        console.log(event.target.value);
    }
);
```

User যা type করবে তা পাওয়া যাবে।

---

# 62. `change` Event

```javascript
input.addEventListener(
    "change",
    (event) => {
        console.log(event.target.value);
    }
);
```

`input` event সাধারণত typing-এর সময় বারবার fire করে।

`change` সাধারণত value change করে field থেকে বের হওয়া/selection commit করার মতো পরিস্থিতিতে fire করে।

---

# 63. Focus & Blur

```javascript
input.addEventListener(
    "focus",
    () => {
        console.log("Focused");
    }
);
```

```javascript
input.addEventListener(
    "blur",
    () => {
        console.log("Blurred");
    }
);
```

---

# 64. Form Submit

HTML:

```html
<form id="loginForm">

    <input
        id="email"
        type="email"
    >

    <input
        id="password"
        type="password"
    >

    <button type="submit">
        Login
    </button>

</form>
```

JS:

```javascript
const form =
    document.getElementById("loginForm");

form.addEventListener(
    "submit",
    (event) => {

        event.preventDefault();

        console.log("Form submitted");

    }
);
```

---

# 65. `preventDefault()`

Browser-এর default behavior বন্ধ করে।

Form-এর ক্ষেত্রে:

```javascript
event.preventDefault();
```

দিলে browser page reload করে form submit করবে না।

React form handling-এর concept-এর সাথেও এটা related।

---

# 66. Form Data Read

```javascript
const email =
    document.getElementById("email");

console.log(email.value);
```

Password:

```javascript
const password =
    document.getElementById("password");

console.log(password.value);
```

---

# 67. Form Validation

```javascript
form.addEventListener(
    "submit",
    (event) => {

        event.preventDefault();

        const email =
            document.getElementById("email")
                .value.trim();

        if (!email) {
            alert("Email is required");
            return;
        }

        console.log("Valid");

    }
);
```

---

# 68. DOM Event Bubbling

ধরো:

```html
<div id="parent">
    <button id="child">
        Click
    </button>
</div>
```

Event button-এ ঘটলে সেটা parent-এর দিকেও bubble করতে পারে।

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Parent");
    }
);

child.addEventListener(
    "click",
    () => {
        console.log("Child");
    }
);
```

Button click করলে:

```text
Child
Parent
```

---

# 69. `stopPropagation()`

Parent-এ event যেতে না দিতে:

```javascript
child.addEventListener(
    "click",
    (event) => {

        event.stopPropagation();

        console.log("Child");

    }
);
```

এখন parent handler fire করবে না।

---

# 70. Event Capturing

Event propagation-এর তিনটি phase:

```text
Capturing
    ↓
Target
    ↓
Bubbling
```

Default event listener সাধারণত bubbling phase-এ কাজ করে।

Capturing:

```javascript
parent.addEventListener(
    "click",
    handler,
    true
);
```

---

# 71. Event Delegation

ধরো:

```html
<ul id="users">

    <li>Atiar</li>
    <li>Rahim</li>
    <li>Karim</li>

</ul>
```

প্রতিটি `li`-তে আলাদা listener না দিয়ে parent-এ listener:

```javascript
const users =
    document.getElementById("users");

users.addEventListener(
    "click",
    (event) => {

        if (event.target.tagName === "LI") {
            console.log(
                event.target.textContent
            );
        }

    }
);
```

এটাই **event delegation**।

Dynamic elements-এর জন্য খুব useful।

---

# 72. `data-*` Attributes

HTML:

```html
<button
    data-id="101"
    data-name="Laptop"
>
    Buy
</button>
```

JS:

```javascript
const button =
    document.querySelector("button");

console.log(button.dataset.id);
console.log(button.dataset.name);
```

Output:

```text
101
Laptop
```

---

# 73. `dataset`

HTML:

```html
<div
    id="product"
    data-product-id="10"
    data-category="electronics"
>
</div>
```

JS:

```javascript
const product =
    document.getElementById("product");

console.log(
    product.dataset.productId
);

console.log(
    product.dataset.category
);
```

---

# 74. DOM দিয়ে List তৈরি

ধরো:

```javascript
const users = [
    "Atiar",
    "Rahim",
    "Karim"
];
```

HTML:

```html
<ul id="userList"></ul>
```

JS:

```javascript
const list =
    document.getElementById("userList");

users.forEach(user => {

    const li =
        document.createElement("li");

    li.textContent = user;

    list.append(li);

});
```

Result:

```html
<ul>
    <li>Atiar</li>
    <li>Rahim</li>
    <li>Karim</li>
</ul>
```

---

# 75. Array of Objects থেকে DOM

এটা খুব important।

```javascript
const products = [
    {
        id: 1,
        name: "Laptop",
        price: 80000
    },
    {
        id: 2,
        name: "Mouse",
        price: 1000
    }
];
```

HTML:

```html
<div id="products"></div>
```

JS:

```javascript
const container =
    document.getElementById("products");

products.forEach(product => {

    const card =
        document.createElement("div");

    card.classList.add("card");

    card.innerHTML = `
        <h2>${product.name}</h2>
        <p>Price: ${product.price}</p>
    `;

    container.append(card);

});
```

এখানে:

```text
Array
  ↓
forEach
  ↓
Object
  ↓
DOM element
  ↓
Browser UI
```

এটা বুঝতে পারলে frontend-এর fundamental concept অনেক পরিষ্কার হবে।

---

# 76. `cloneNode()`

একটি DOM element copy করতে:

```javascript
const copy =
    element.cloneNode(true);
```

`true` দিলে descendants-ও clone হয়।

```javascript
const copy =
    card.cloneNode(true);

container.append(copy);
```

---

# 77. `insertAdjacentHTML()`

HTML insert করার useful method:

```javascript
container.insertAdjacentHTML(
    "beforeend",
    "<p>Hello</p>"
);
```

Positions:

```text
beforebegin
afterbegin
beforeend
afterend
```

---

# 78. DOM Content Loaded

JavaScript যদি HTML element-এর আগে execute হয়, element না-ও পাওয়া যেতে পারে।

তাই:

```javascript
document.addEventListener(
    "DOMContentLoaded",
    () => {
        console.log("DOM ready");
    }
);
```

এটি DOM parsing complete হওয়ার পর execute হবে।

আর script যদি `<body>`-র শেষে রাখো বা modern `defer` ব্যবহার করো, অনেক ক্ষেত্রে আলাদা করে এটা প্রয়োজন হয় না।

---

# 79. Script `defer`

HTML:

```html
<script
    src="app.js"
    defer>
</script>
```

`defer` script HTML parsing-এর সাথে interfere না করে document parse হওয়ার পরে execute করে।

Modern external JS-এর জন্য খুব useful।

---

# 80. Window vs Document

### `window`

Browser window-এর global object।

```javascript
console.log(window);
```

### `document`

Current webpage-এর DOM document।

```javascript
console.log(document);
```

Hierarchy:

```text
Window
  │
  └── Document
       │
       └── HTML
```

---

# 81. Browser Window Events

```javascript
window.addEventListener(
    "load",
    () => {
        console.log("Page loaded");
    }
);
```

Scroll:

```javascript
window.addEventListener(
    "scroll",
    () => {
        console.log("Scrolling");
    }
);
```

Resize:

```javascript
window.addEventListener(
    "resize",
    () => {
        console.log("Window resized");
    }
);
```

---

# 82. DOM Dimensions

Element-এর dimensions:

```javascript
const box =
    document.querySelector(".box");

console.log(box.offsetWidth);
console.log(box.offsetHeight);
```

আর:

```javascript
box.clientWidth;
box.clientHeight;
```

---

# 83. `getBoundingClientRect()`

Element-এর position এবং dimensions:

```javascript
const rect =
    box.getBoundingClientRect();

console.log(rect);
```

পেতে পারো:

```text
x
y
width
height
top
right
bottom
left
```

---

# 84. Scroll

Page scroll:

```javascript
window.scrollTo({
    top: 0,
    behavior: "smooth"
});
```

Element scroll:

```javascript
element.scrollIntoView({
    behavior: "smooth"
});
```

---

# 85. Local Storage — DOM-এর সাথে Frequently Used

Technically `localStorage` DOM-এর অংশ নয়; এটি Web Storage API-এর অংশ। তবে frontend JavaScript-এ DOM-এর সাথে খুব বেশি ব্যবহার হয়।

Save:

```javascript
localStorage.setItem(
    "username",
    "Atiar"
);
```

Read:

```javascript
const username =
    localStorage.getItem("username");

console.log(username);
```

Remove:

```javascript
localStorage.removeItem("username");
```

সব clear:

```javascript
localStorage.clear();
```

---

# 86. Session Storage

```javascript
sessionStorage.setItem(
    "token",
    "abc123"
);
```

Read:

```javascript
sessionStorage.getItem("token");
```

---

# 87. DOM দিয়ে Dark Mode

HTML:

```html
<button id="themeBtn">
    Toggle Theme
</button>
```

CSS:

```css
.dark {
    background: black;
    color: white;
}
```

JS:

```javascript
const button =
    document.getElementById("themeBtn");

button.addEventListener(
    "click",
    () => {
        document.body.classList.toggle("dark");
    }
);
```

---

# 88. Complete Todo Example

HTML:

```html
<input id="todoInput">

<button id="addBtn">
    Add
</button>

<ul id="todoList"></ul>
```

JS:

```javascript
const input =
    document.getElementById("todoInput");

const addButton =
    document.getElementById("addBtn");

const list =
    document.getElementById("todoList");


addButton.addEventListener(
    "click",
    () => {

        const text =
            input.value.trim();

        if (!text) {
            return;
        }

        const li =
            document.createElement("li");

        li.textContent = text;

        list.append(li);

        input.value = "";

    }
);
```

Flow:

```text
User types
    ↓
input.value
    ↓
Button click
    ↓
createElement()
    ↓
textContent
    ↓
append()
    ↓
DOM update
    ↓
Browser UI update
```

---

# 89. Todo Delete

```javascript
list.addEventListener(
    "click",
    (event) => {

        if (event.target.tagName === "LI") {
            event.target.remove();
        }

    }
);
```

এখানে event delegation ব্যবহার করেছি।

---

# 90. Todo Complete + Delete

```javascript
list.addEventListener(
    "click",
    (event) => {

        if (event.target.tagName === "LI") {

            event.target.classList.toggle(
                "completed"
            );

        }

    }
);
```

CSS:

```css
.completed {
    text-decoration: line-through;
}
```

---

# 91. DOM-এর Full Architecture

এখন পুরো DOM concept একসাথে দেখো:

```text
                    Browser
                       │
                     Window
                       │
                    Document
                       │
                    HTML DOM
                       │
          ┌────────────┴────────────┐
          │                         │
        Element                    Node
          │
    ┌─────┼──────┐
    │     │      │
  Select  Modify Events
    │     │      │
    │     │      ├── click
    │     │      ├── input
    │     │      ├── submit
    │     │      ├── keydown
    │     │      └── change
    │     │
    │     ├── text
    │     ├── HTML
    │     ├── attributes
    │     ├── classes
    │     ├── styles
    │     ├── create
    │     ├── append
    │     ├── remove
    │     └── replace
    │
    ├── getElementById()
    ├── querySelector()
    └── querySelectorAll()
```

---

# 🔥 DOM-এর সব গুরুত্বপূর্ণ Topics — Checklist

তোমার DOM mastery-এর জন্য এই checklist follow করো:

### 1. DOM Fundamentals

```text
✓ DOM কী
✓ Document
✓ Window
✓ Node
✓ Element
✓ DOM Tree
```

### 2. Selecting Elements

```text
✓ getElementById()
✓ getElementsByClassName()
✓ getElementsByTagName()
✓ querySelector()
✓ querySelectorAll()
```

### 3. Traversing

```text
✓ parentElement
✓ children
✓ childNodes
✓ firstElementChild
✓ lastElementChild
✓ nextElementSibling
✓ previousElementSibling
```

### 4. Content

```text
✓ textContent
✓ innerText
✓ innerHTML
```

### 5. Attributes

```text
✓ getAttribute()
✓ setAttribute()
✓ removeAttribute()
✓ hasAttribute()
✓ dataset
```

### 6. Classes

```text
✓ className
✓ classList.add()
✓ classList.remove()
✓ classList.toggle()
✓ classList.contains()
✓ classList.replace()
```

### 7. Styling

```text
✓ element.style
✓ CSS classes
```

### 8. Creating / Removing

```text
✓ createElement()
✓ append()
✓ appendChild()
✓ prepend()
✓ before()
✓ after()
✓ remove()
✓ removeChild()
✓ replaceWith()
✓ cloneNode()
✓ insertAdjacentHTML()
```

### 9. Events

```text
✓ addEventListener()
✓ click
✓ dblclick
✓ mouseenter
✓ mouseleave
✓ keydown
✓ keyup
✓ input
✓ change
✓ focus
✓ blur
✓ submit
✓ load
✓ scroll
✓ resize
```

### 10. Event Concepts

```text
✓ event object
✓ event.target
✓ preventDefault()
✓ stopPropagation()
✓ bubbling
✓ capturing
✓ event delegation
```

### 11. Forms

```text
✓ input.value
✓ form submit
✓ preventDefault()
✓ validation
✓ checkbox
✓ radio
✓ select
✓ textarea
```

### 12. Browser APIs

```text
✓ localStorage
✓ sessionStorage
✓ window
✓ scroll
✓ dimensions
✓ getBoundingClientRect()
```

---

# 🧠 DOM শেখার সবচেয়ে গুরুত্বপূর্ণ Mental Model

যেকোনো DOM problem-এ প্রথমে এই 5টা প্রশ্ন করবে:

```text
1. কোন element দরকার?
          ↓
2. কীভাবে select করব?
          ↓
3. কী change করতে চাই?
          ↓
4. কখন change হবে?
          ↓
5. কোন event trigger করবে?
```

Example:

**"Button click করলে heading change হবে"**

```text
Element
↓
button + heading

Select
↓
querySelector()

Event
↓
click

Action
↓
textContent

Result
↓
heading changes
```

Code:

```javascript
const button =
    document.querySelector("#btn");

const heading =
    document.querySelector("#title");

button.addEventListener(
    "click",
    () => {
        heading.textContent =
            "Hello JavaScript";
    }
);
```

এই pattern-টাই DOM-এর core:

```text
SELECT
  ↓
LISTEN
  ↓
CHANGE
  ↓
UPDATE UI
```

আর তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ হলো **DOM → Events → Forms → API/Fetch → Dynamic UI** এই sequence-এ practice করা। এরপর React-এ গেলে তুমি বুঝতে পারবে কেন React সরাসরি বারবার DOM manipulate না করে **state → render** approach ব্যবহার করে।


---

 