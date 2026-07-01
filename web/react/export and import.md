In JavaScript (ES6+), **import** and **export** are used to share code between different files.

- **export** → makes variables, functions, classes available outside a file.
    
- **import** → brings exported code into another file.
    

Example project:

```
src/
 ├── math.js
 └── app.js
```

## 1. Named Export

A file can export multiple things.

### math.js

```javascript
export const add = (a, b) => {
  return a + b;
};

export const multiply = (a, b) => {
  return a * b;
};

export const name = "Calculator";
```

### app.js

```javascript
import { add, multiply, name } from "./math.js";

console.log(add(5, 3));        // 8
console.log(multiply(5, 3));   // 15
console.log(name);             // Calculator
```

### Rules:

- Same name required
    
- Use `{ }`
    

---

## 2. Import with Alias (Rename)

If you want another name:

```javascript
import { add as sum } from "./math.js";

console.log(sum(10, 20));
```

Output:

```
30
```

---

## 3. Default Export

A file can have **only one default export**.

### user.js

```javascript
const user = {
  name: "Atiar",
  age: 22
};

export default user;
```

### app.js

```javascript
import user from "./user.js";

console.log(user.name);
```

Output:

```
Atiar
```

Notice:

```javascript
import user
```

No `{ }` needed.

---

## 4. Export Default Function

### message.js

```javascript
export default function greet() {
  console.log("Hello World");
}
```

### app.js

```javascript
import greet from "./message.js";

greet();
```

Output:

```
Hello World
```

---

## 5. Export at the End

Instead of:

```javascript
export const x = 10;
export function test(){}
```

You can do:

```javascript
const x = 10;

function test(){
  console.log("Testing");
}


export { x, test };
```

Import:

```javascript
import { x, test } from "./file.js";
```

---

## 6. Import Everything (*)

Import all exports:

### math.js

```javascript
export const add = (a,b)=>a+b;
export const sub = (a,b)=>a-b;
```

### app.js

```javascript
import * as math from "./math.js";


console.log(math.add(10,5));
console.log(math.sub(10,5));
```

Output:

```
15
5
```

Here:

```
math.add()
math.sub()
```

---

## 7. Mixed Export

### data.js

```javascript
export const age = 22;


export default function user(){
  return "Atiar";
}
```

### app.js

```javascript
import user, { age } from "./data.js";


console.log(user());
console.log(age);
```

Output:

```
Atiar
22
```

---

## Real React Example

### Button.jsx

```jsx
function Button(){
  return (
    <button>
      Click
    </button>
  );
}


export default Button;
```

### App.jsx

```jsx
import Button from "./Button";


function App(){

  return (
    <>
      <h1>Hello React</h1>
      <Button/>
    </>
  )
}


export default App;
```

---

## Difference Summary

|Export|Import|
|---|---|
|Sends code out|Receives code|
|`export` keyword|`import` keyword|
|Written in source file|Written where used|
|Can have many named exports|Named imports use `{}`|
|Default only one|Default no `{}`|

Short memory:

```
export = give
import = take
```

Example:

```javascript
// give.js
export const x = 10;


// take.js
import {x} from "./give.js";
```


-------------
