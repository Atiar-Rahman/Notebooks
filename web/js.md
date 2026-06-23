**JavaScript (JS)** is a programming language used to make websites and applications **interactive, dynamic, and functional**. It runs mainly in web browsers (like Chrome, Firefox, Edge) and also on servers using environments like Node.js.

For example:

- HTML → creates the structure of a webpage
    
- CSS → designs the webpage
    
- JavaScript → adds behavior and logic
    

A button click, form validation, animations, live updates, games, and many web apps use JavaScript.

---

# JavaScript Learning Path: Basic → Advanced

## 1. JavaScript Basics

### What is a variable?

A variable stores information.

```javascript
let name = "Alex";
let age = 15;

console.log(name);
console.log(age);
```

Output:

```
Alex
15
```

### Variable types

```javascript
let text = "Hello";     // String
let number = 100;       // Number
let active = true;      // Boolean
let empty = null;       // Null
let value;              // Undefined
```

---
In JavaScript, **`toFixed()`** is a method used to **format a number and keep a specific number of decimal places**.

### Syntax

```javascript
number.toFixed(decimalPlaces)
```

- `decimalPlaces` → how many digits you want after the decimal point
    
- It returns a **string**, not a number
    

---

### Example 1: Basic use

```javascript
let num = 5.6789;

console.log(num.toFixed(2));
```

Output:

```
5.68
```

It keeps **2 decimal places**.

---

### Example 2: Removing extra decimals

```javascript
let price = 99.999;

console.log(price.toFixed(1));
```

Output:

```
100.0
```

It rounds the number.

---

### Example 3: No decimal places

```javascript
let value = 12.75;

console.log(value.toFixed(0));
```

Output:

```
13
```

---

### Example 4: Adding zeros

```javascript
let number = 10;

console.log(number.toFixed(3));
```

Output:

```
10.000
```

---

### Important: It returns a string

```javascript
let x = 12.34;

let result = x.toFixed(2);

console.log(typeof result);
```

Output:

```
string
```

If you need a number:

```javascript
let num = Number(x.toFixed(2));
```

or

```javascript
let num = +x.toFixed(2);
```

---

### Common use cases

**Currency display:**

```javascript
let price = 25.5;

console.log("$" + price.toFixed(2));
```

Output:

```
$25.50
```

**Math calculations:**

```javascript
let average = 10 / 3;

console.log(average.toFixed(2));
```

Output:

```
3.33
```

---

### Difference between `toFixed()` and `toPrecision()`

```javascript
let num = 123.456;

num.toFixed(2);
// 123.46

num.toPrecision(2);
// 1.2e+2
```

`toFixed()` controls **decimal places**.  
`toPrecision()` controls **total significant digits**.
## 2. Operators

### Math operators

```javascript
let a = 10;
let b = 5;

console.log(a + b); // 15
console.log(a - b); // 5
console.log(a * b); // 50
console.log(a / b); // 2
```

### Comparison

```javascript
10 > 5     // true
10 == "10" // true
10 === "10" // false
```

`===` checks both value and type.

---

# 3. Conditions (Decision Making)

```javascript
let age = 18;

if(age >= 18){
    console.log("Adult");
}
else{
    console.log("Not adult");
}
```

---

# 4. Loops

Repeat code.

### For loop

```javascript
for(let i = 1; i <= 5; i++){
    console.log(i);
}
```

Output:

```
1
2
3
4
5
```

### While loop

```javascript
let i = 0;

while(i < 3){
    console.log(i);
    i++;
}
```

---

# 5. Functions

A function is reusable code.

```javascript
function greet(){
    console.log("Hello!");
}

greet();
```

With parameters:

```javascript
function add(a,b){
    return a+b;
}

console.log(add(5,3));
```

---

# 6. Arrays

Store multiple values.

```javascript
let fruits = [
    "Apple",
    "Banana",
    "Orange"
];

console.log(fruits[0]);
```

Useful methods:

```javascript
fruits.push("Mango");

fruits.pop();

fruits.length;
```

---
In JavaScript, a **String** is a sequence of characters. You can work with strings from **first character to last character** using different methods.

### 1. Create a string

```javascript
let text = "JavaScript";
```

Positions (index):

```
J a v a S c r i p t
0 1 2 3 4 5 6 7 8 9
```

---

## Access characters

### First character

```javascript
let text = "JavaScript";

console.log(text[0]);
```

Output:

```
J
```

### Last character

```javascript
console.log(text[text.length - 1]);
```

Output:

```
t
```

---

# String length

```javascript
let text = "Hello";

console.log(text.length);
```

Output:

```
5
```

---

# Loop from first to last character

```javascript
let text = "Hello";

for(let i = 0; i < text.length; i++){
    console.log(text[i]);
}
```

Output:

```
H
e
l
l
o
```

---

# Reverse a string (last to first)

```javascript
let text = "Hello";

for(let i = text.length - 1; i >= 0; i--){
    console.log(text[i]);
}
```

Output:

```
o
l
l
e
H
```

---

# Common JavaScript String Methods

## 1. `charAt()`

```javascript
let name = "Alex";

console.log(name.charAt(0));
```

Output:

```
A
```

---

## 2. `toUpperCase()`

```javascript
let text = "hello";

console.log(text.toUpperCase());
```

Output:

```
HELLO
```

---

## 3. `toLowerCase()`

```javascript
let text = "HELLO";

console.log(text.toLowerCase());
```

Output:

```
hello
```

---

## 4. `includes()`

Checks if text exists:

```javascript
let text = "JavaScript";

console.log(text.includes("Script"));
```

Output:

```
true
```

---

## 5. `startsWith()`

```javascript
let text = "JavaScript";

console.log(text.startsWith("Java"));
```

Output:

```
true
```

---

## 6. `endsWith()`

```javascript
let text = "JavaScript";

console.log(text.endsWith("ipt"));
```

Output:

```
true
```

---

## 7. `indexOf()`

Find position:

```javascript
let text = "JavaScript";

console.log(text.indexOf("S"));
```

Output:

```
4
```

---

## 8. `slice()`

Cut part of a string:

```javascript
let text = "JavaScript";

console.log(text.slice(0,4));
```

Output:

```
Java
```

From index 4:

```javascript
console.log(text.slice(4));
```

Output:

```
Script
```

---

## 9. `substring()`

```javascript
let text = "JavaScript";

console.log(text.substring(0,4));
```

Output:

```
Java
```

---

## 10. `replace()`

```javascript
let text = "Hello World";

console.log(text.replace("World","JS"));
```

Output:

```
Hello JS
```

---

## 11. `split()`

Convert string to array:

```javascript
let text = "a,b,c";

console.log(text.split(","));
```

Output:

```javascript
["a","b","c"]
```

---

## 12. `trim()`

Remove spaces:

```javascript
let text = "  Hello  ";

console.log(text.trim());
```

Output:

```
Hello
```

---

## 13. Template literals

```javascript
let name = "Sam";

console.log(`Hello ${name}`);
```

Output:

```
Hello Sam
```

---

## 14. Compare strings

```javascript
console.log("apple" === "apple");
```

Output:

```
true
```

---

## 15. Count characters example

```javascript
let text = "banana";
let count = 0;

for(let i=0;i<text.length;i++){
    if(text[i]=="a"){
        count++;
    }
}

console.log(count);
```

Output:

```
3
```

---

### String learning order:

1. length
    
2. index access
    
3. loops
    
4. slice / substring
    
5. replace
    
6. split
    
7. search methods
    
8. template literals
    
9. regex
    
10. advanced string processing
# 7. Objects

Store related data.

```javascript
let person = {
    name:"John",
    age:20,
    city:"Dhaka"
};

console.log(person.name);
```

---

# 8. DOM (Changing Websites)

DOM lets JavaScript control HTML.

HTML:

```html
<h1 id="title">
Hello
</h1>
```

JavaScript:

```javascript
document.getElementById("title")
.innerHTML = "Welcome!";
```

Now the text changes.

---

# 9. Events

React when users do something.

Example:

```javascript
button.onclick = function(){
    alert("Clicked!");
}
```

Common events:

- click
    
- mouseover
    
- keydown
    
- submit
    

---

# 10. Modern JavaScript (ES6+)

## let and const

```javascript
let age = 20;
const name = "Sam";
```

---

## Arrow functions

Old:

```javascript
function hello(){
 console.log("Hi");
}
```

New:

```javascript
const hello = () => {
 console.log("Hi");
}
```

---

## Template strings

```javascript
let name = "Tom";

console.log(`Hello ${name}`);
```

---

# Intermediate JavaScript

## 11. Array Methods

### map()

Changes every item:

```javascript
let nums = [1,2,3];

let doubled = nums.map(
x => x * 2
);

console.log(doubled);
```

Result:

```
[2,4,6]
```

---

### filter()

```javascript
let ages=[12,18,20];

let adults =
ages.filter(
age => age >=18
);

console.log(adults);
```

---

### reduce()

```javascript
let numbers=[1,2,3];

let total =
numbers.reduce(
(a,b)=>a+b
);

console.log(total);
```

---

# 12. Asynchronous JavaScript

JavaScript can do tasks without stopping the program.

Example:

```javascript
console.log("Start");

setTimeout(()=>{
 console.log("Later");
},2000);

console.log("End");
```

Output:

```
Start
End
Later
```

---

# 13. Promises

Used for future results.

```javascript
let promise =
new Promise((resolve,reject)=>{

resolve("Success");

});
```

---

# 14. Async / Await

Modern way to handle promises.

```javascript
async function getData(){

let response =
await fetch(
"https://api.example.com"
);

let data =
await response.json();

console.log(data);

}

getData();
```

---

# Advanced JavaScript

## 15. Object-Oriented Programming

Classes:

```javascript
class User{

constructor(name){
 this.name=name;
}

sayHello(){
 console.log(
 "Hello "+this.name
 );
}

}

let user =
new User("Alex");

user.sayHello();
```

---

# 16. Closures

A function remembering its environment.

```javascript
function counter(){

let count=0;

return function(){
 count++;
 return count;
}

}

let c = counter();

console.log(c());
console.log(c());
```

---

# 17. Callbacks

A function passed into another function.

```javascript
function process(callback){

callback();

}

process(
()=>{
 console.log("Done");
}
);
```

---

# 18. Modules

Split code into files.

Export:

```javascript
export function add(a,b){
return a+b;
}
```

Import:

```javascript
import {add}
from "./math.js";
```

---

# 19. Error Handling

```javascript
try{

let x = y;

}
catch(error){

console.log(error);

}
```

---

# 20. JavaScript Frameworks

After JavaScript basics, learn:

- React → Frontend apps
    
- Vue.js → Frontend
    
- Angular → Large applications
    
- Express.js → Backend
    

---

# Advanced Topics to Master

✅ Scope  
✅ Hoisting  
✅ Event loop  
✅ Call stack  
✅ Prototypes  
✅ Object inheritance  
✅ Memory management  
✅ Web APIs  
✅ REST APIs  
✅ JSON  
✅ Security  
✅ Performance optimization  
✅ Design patterns

---

# Suggested Learning Order

**Beginner**

1. Variables
    
2. Data types
    
3. Operators
    
4. Conditions
    
5. Loops
    
6. Functions
    
7. Arrays
    
8. Objects
    

**Intermediate**  
9. DOM  
10. Events  
11. ES6  
12. Async JS  
13. APIs

**Advanced**  
14. OOP  
15. Closures  
16. Prototypes  
17. Event loop  
18. Frameworks  
19. Backend JavaScript

With consistent practice, you can go from beginner to building full web applications.