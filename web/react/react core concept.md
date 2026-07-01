### What is a Component?

A **component** is a small, reusable piece of UI (User Interface) in an application.

Think of a website as a collection of small parts:

```
Website
 |
 |-- Navbar
 |-- Sidebar
 |-- Product Card
 |-- Footer
 |-- Button
```

Each part can be a **component**.

A component has its own:

- UI (HTML)
    
- Logic (JavaScript)
    
- Style (CSS)
    

---

## Real Life Example

Imagine an e-commerce website:

```
Amazon
 |
 |-- Header
 |-- SearchBar
 |-- ProductCard
 |-- CartButton
 |-- Footer
```

The product card is a component.

Instead of writing:

```html
<div>
  <img>
  <h2>Phone</h2>
  <p>$500</p>
</div>
```

100 times, create one component and reuse it.

---

# React Component Example

### ProductCard Component

```jsx
function ProductCard() {
  return (
    <div>
      <img src="phone.jpg" />

      <h2>iPhone 15</h2>

      <p>Price: $800</p>

      <button>
        Buy Now
      </button>

    </div>
  );
}

export default ProductCard;
```

This is a component.

---

## Use Component

App.jsx

```jsx
import ProductCard from "./ProductCard";


function App(){

  return (
    <div>

      <ProductCard />

      <ProductCard />

      <ProductCard />

    </div>
  )

}

export default App;
```

Output:

```
iPhone 15
Price: $800
Buy Now


iPhone 15
Price: $800
Buy Now


iPhone 15
Price: $800
Buy Now
```

Same component multiple times.

---

# Component with Props

Props are data passed into a component.

Example:

ProductCard.jsx

```jsx
function ProductCard(props){

 return (
   <div>

    <h2>
      {props.name}
    </h2>

    <p>
      Price: {props.price}
    </p>

   </div>
 )

}

export default ProductCard;
```

---

App.jsx

```jsx
function App(){

return (

 <>
  <ProductCard 
     name="Laptop"
     price="70000"
  />


  <ProductCard
     name="Mobile"
     price="30000"
  />

 </>

)

}
```

Output:

```
Laptop
Price: 70000


Mobile
Price: 30000
```

Same component, different data.

---

# Component Types

## 1. Functional Component (Modern)

```jsx
function Header(){

 return (
   <h1>
    My Website
   </h1>
 )

}
```

Most used.

---

## 2. Class Component (Old)

```jsx
class Header extends React.Component{

 render(){

  return (
   <h1>
    My Website
   </h1>
  )

 }

}
```

Now rarely used.

---

# Component Tree

React app structure:

```
App
 |
 |-- Header
 |
 |-- Main
 |    |
 |    |-- ProductCard
 |    |-- ProductCard
 |
 |-- Footer
```

Each component controls its own part.

---

### Simple definition:

**Component = A reusable building block of UI.**

Like LEGO blocks. You create small pieces and combine them to build a big application.

---------
# What is JSX?

**JSX (JavaScript XML)** is a syntax extension of JavaScript that allows us to write **HTML-like code inside JavaScript** in React.

Normally JavaScript:

```javascript
const element = document.createElement("h1");
element.textContent = "Hello";
```

With JSX:

```jsx
const element = <h1>Hello</h1>;
```

React converts JSX into normal JavaScript.

---

## Example

```jsx
function App(){

  return (
    <div>
      <h1>Hello React</h1>
      <p>This is JSX</p>
    </div>
  )

}

export default App;
```

Here:

```jsx
<h1>Hello React</h1>
```

is JSX.

---

# Why use JSX?

Without JSX:

```javascript
React.createElement(
  "h1",
  null,
  "Hello React"
);
```

With JSX:

```jsx
<h1>Hello React</h1>
```

JSX makes React code easier to write and read.

---

# JSX Rules

## Rule 1: Return one parent element

❌ Wrong:

```jsx
function App(){

 return (
   <h1>Hello</h1>
   <p>React</p>
 )

}
```

Because two elements are returned.

✅ Correct:

```jsx
function App(){

 return (
   <div>

    <h1>Hello</h1>
    <p>React</p>

   </div>
 )

}
```

or use Fragment:

```jsx
function App(){

return (
 <>
   <h1>Hello</h1>
   <p>React</p>
 </>
)

}
```

---

# Rule 2: Close all tags

HTML:

```html
<img>
```

JSX:

```jsx
<img />
```

HTML:

```html
<input>
```

JSX:

```jsx
<input />
```

Every tag must close.

---

# Rule 3: Use camelCase for attributes

HTML:

```html
<button onclick="">
```

JSX:

```jsx
<button onClick="">
```

Examples:

|HTML|JSX|
|---|---|
|class|className|
|onclick|onClick|
|tabindex|tabIndex|
|onchange|onChange|

---

# Rule 4: JavaScript inside JSX uses `{ }`

Example:

```jsx
function App(){

const name = "AtiAR";

return (
  <h1>
    Hello {name}
  </h1>
)

}
```

Output:

```
Hello AtiAR
```

---

# Rule 5: Use className instead of class

❌

```jsx
<div class="box">
 Hello
</div>
```

✅

```jsx
<div className="box">
 Hello
</div>
```

Because `class` is a JavaScript keyword.

---

# Rule 6: JSX expressions must return something

Correct:

```jsx
const age = 20;

return (
 <p>
  Age: {age}
 </p>
)
```

---

# Rule 7: Use quotes for strings

```jsx
<img 
 src="image.png"
/>
```

---

# Rule 8: Use {} for dynamic values

Static:

```jsx
<h1>Hello World</h1>
```

Dynamic:

```jsx
<h1>{username}</h1>
```

---

# Rule 9: Cannot write if statement directly

❌

```jsx
return(
{
 if(age > 18){
  <h1>Adult</h1>
 }
}
)
```

Use ternary:

✅

```jsx
return(
 <>
 {
  age > 18 
  ? <h1>Adult</h1>
  : <h1>Child</h1>
 }
 </>
)
```

---

# Rule 10: Components must start with Capital Letter

❌

```jsx
function button(){

}
```

React thinks it is HTML.

✅

```jsx
function Button(){

}
```

---

## JSX + Component Example

```jsx
function User(){

const name = "Rahim";
const age = 22;

return (
 <div>

  <h1>
    Name: {name}
  </h1>

  <p>
    Age: {age}
  </p>

  <button>
    Click
  </button>

 </div>
)

}
```

---

### Short Summary

JSX rules:

1. One parent element
    
2. Close every tag
    
3. Use `className`
    
4. Use camelCase events (`onClick`)
    
5. JavaScript uses `{ }`
    
6. Component name starts uppercase
    
7. Use ternary instead of if
    
8. Return valid JSX
    

JSX = **HTML + JavaScript together in React**.

-----------
## What are Props in React?

**Props (Properties)** are used to **pass data from one component to another component**.

Usually data flows:

```
Parent Component
        |
        | props
        ↓
Child Component
```

Props are **read-only** (child cannot directly change them).

---

## Basic Example

### Parent Component

```jsx
function App(){

  return (
    <div>

      <User name="AtiAR" age={22}/>

    </div>
  )

}
```

Here:

```jsx
name="AtiAR"
age={22}
```

are props.

---

### Child Component

```jsx
function User(props){

  return (
    <div>

      <h1>
        Name: {props.name}
      </h1>

      <p>
        Age: {props.age}
      </p>

    </div>
  )

}
```

Output:

```
Name: AtiAR
Age: 22
```

---

# How Props Work?

Think:

```jsx
<User name="AtiAR" />
```

React creates an object:

```javascript
{
 name: "AtiAR"
}
```

and sends it to:

```jsx
function User(props)
```

So:

```jsx
props.name
```

gets:

```
AtiAR
```

---

# Multiple Props

Parent:

```jsx
function App(){

return (

 <Product
   title="Laptop"
   price={70000}
   stock={5}
 />

)

}
```

Child:

```jsx
function Product(props){

return (

 <div>

  <h2>{props.title}</h2>

  <p>
   Price: {props.price}
  </p>

  <p>
   Stock: {props.stock}
  </p>

 </div>

)

}
```

Output:

```
Laptop
Price: 70000
Stock: 5
```

---

# Props Destructuring (Common)

Instead of:

```jsx
function User(props){

 return (
  <h1>
   {props.name}
  </h1>
 )

}
```

You can write:

```jsx
function User({name, age}){

return (

 <>
  <h1>{name}</h1>
  <p>{age}</p>
 </>

)

}
```

Cleaner.

---

# Passing Array with Props

Parent:

```jsx
function App(){

const users=[
 "Rahim",
 "Karim",
 "John"
]


return (
 <User data={users}/>
)

}
```

Child:

```jsx
function User({data}){

return (

 <div>

 {
  data.map(user=>
    <p>{user}</p>
  )
 }

 </div>

)

}
```

Output:

```
Rahim
Karim
John
```

---

# Passing Function as Props

Parent:

```jsx
function App(){

function sayHello(){

 alert("Hello")

}


return (

 <Button click={sayHello}/>

)

}
```

Child:

```jsx
function Button({click}){

return (

<button onClick={click}>
 Click
</button>

)

}
```

When button click:

```
Hello
```

---

# Props vs State

|Props|State|
|---|---|
|Comes from parent|Inside component|
|Read-only|Can change|
|Used to pass data|Used to store data|
|Controlled by parent|Controlled by component|

Example:

```jsx
// props
<User name="Rahim"/>


// state
const [count,setCount]=useState(0)
```

---

## Simple Definition

**Props = Component's input data**

Like a function:

```javascript
function add(a,b){

}
```

`a` and `b` are like props.

React:

```jsx
<User name="Rahim"/>
```

`name` is a prop.

-----------
## Props Types in React

Props can contain **any type of JavaScript data**.

Common prop types:

1. String
    
2. Number
    
3. Boolean
    
4. Array
    
5. Object
    
6. Function
    
7. React Component / JSX
    
8. Children
    

---

# 1. String Props

### Pass

```jsx
<User name="Rahim" />
```

### Read

```jsx
function User(props){

 return (
   <h1>
    {props.name}
   </h1>
 )

}
```

Output:

```
Rahim
```

---

# 2. Number Props

### Pass

```jsx
<User age={22} />
```

Note:

- String uses quotes `" "`
    
- Number uses `{ }`
    

### Read

```jsx
function User({age}){

return (
 <p>
  Age: {age}
 </p>
)

}
```

Output:

```
Age: 22
```

---

# 3. Boolean Props

Boolean means true/false.

### Pass

```jsx
<User isAdmin={true}/>
```

or short form:

```jsx
<User isAdmin />
```

Short form means:

```javascript
isAdmin={true}
```

---

### Read

```jsx
function User({isAdmin}){

return (

<div>

{
 isAdmin 
 ? <h1>Admin</h1>
 : <h1>User</h1>
}

</div>

)

}
```

---

# 4. Array Props

### Pass

```jsx
<Product 
 items={["Phone","Laptop","Tablet"]}
/>
```

---

### Read

```jsx
function Product({items}){

return (

<div>

{
 items.map(item=>
   <p>{item}</p>
 )
}

</div>

)

}
```

Output:

```
Phone
Laptop
Tablet
```

---

# 5. Object Props

### Pass

```jsx
<User 
 info={{
   name:"Rahim",
   age:25
 }}
/>
```

---

### Read

```jsx
function User({info}){

return (

<div>

<h1>
 {info.name}
</h1>

<p>
 {info.age}
</p>

</div>

)

}
```

Output:

```
Rahim
25
```

---

# 6. Function Props

Used for sending actions/events.

### Parent

```jsx
function App(){

function handleClick(){

 alert("Clicked")

}


return (
 <Button click={handleClick}/>
)

}
```

---

### Child

```jsx
function Button({click}){

return (

<button onClick={click}>
 Click
</button>

)

}
```

Flow:

```
Parent function
       |
       | props
       ↓
Child button
```

---

# 7. JSX / Component Props

You can pass UI.

### Pass

```jsx
<Card>

<h1>Hello</h1>

</Card>
```

---

### Read using children

```jsx
function Card({children}){

return (

<div>

 {children}

</div>

)

}
```

Output:

```
Hello
```

---

# 8. Default Props

Give default value.

```jsx
function User({name="Guest"}){

return (

<h1>
{name}
</h1>

)

}
```

Usage:

```jsx
<User />
```

Output:

```
Guest
```

---

# Reading Props Ways

## Method 1: props object

```jsx
function User(props){

return (
 <h1>
 {props.name}
 </h1>
)

}
```

---

## Method 2: Destructuring (Most used)

```jsx
function User({name,age}){

return (
 <>
  <h1>{name}</h1>
  <p>{age}</p>
 </>
)

}
```

---

# Passing Multiple Props

Parent:

```jsx
<Product
 name="Laptop"
 price={80000}
 available={true}
 tags={["HP","Dell"]}
/>
```

Child:

```jsx
function Product({
 name,
 price,
 available,
 tags
}){

return (

<div>

<h2>{name}</h2>

<p>{price}</p>

<p>{available}</p>

{
 tags.map(tag=>
  <span>{tag}</span>
 )
}

</div>

)

}
```

---

# Props Rule

✅ Can pass:

- String
    
- Number
    
- Boolean
    
- Array
    
- Object
    
- Function
    
- JSX
    

❌ Cannot modify props:

```jsx
props.name="New"
```

Wrong.

Props are **read-only**.

---

## Simple Mental Model

```jsx
<Component 
 data="hello"
/>
```

means:

```javascript
{
 data:"hello"
}
```

Child receives:

```jsx
function Component(props){

}
```

Props = **data transfer system between React components**.

--------
## 1. Props are Read-Only (Immutable)

In React, **props cannot be changed by the child component**.

Data flow:

```
Parent Component
        |
        | props
        ↓
Child Component
```

Parent owns the data. Child only reads it.

---

### Example

Parent:

```jsx
function App(){

  const name = "Rahim";

  return (
    <User name={name}/>
  )

}
```

Child:

```jsx
function User(props){

  props.name = "Karim"; // ❌ Wrong

  return (
    <h1>{props.name}</h1>
  )

}
```

This is not allowed because props are read-only.

---

## Why Read-Only?

Because React follows **one-way data flow**:

```
Data
 ↓
Parent
 ↓
Child
```

This makes the application easier to debug.

---

# 2. Two-Way Data Binding

React does **not** have automatic two-way binding like Angular.

Wrong idea:

```
Child changes value
        ↑↓
Parent value changes automatically
```

React uses a controlled approach.

You achieve two-way behavior using:

- State
    
- Props
    
- Callback function
    

---

## Two-Way Communication Example

Parent:

```jsx
import {useState} from "react";


function App(){

 const [name,setName] = useState("Rahim");


 return (
   <User
     name={name}
     changeName={setName}
   />
 )

}
```

---

Child:

```jsx
function User({name,changeName}){


return (

<div>

<h1>
{name}
</h1>


<button onClick={()=>changeName("Karim")}>

Change Name

</button>


</div>

)

}
```

Flow:

```
Parent state
      |
      | props
      ↓
Child


Child event
      |
      | function props
      ↓
Parent updates state
```

Output:

Before:

```
Rahim
```

After click:

```
Karim
```

This is React's "two-way" pattern.

---

# 3. Conditional Rendering

Conditional rendering means:

**Show different UI based on condition.**

Like normal JavaScript:

```javascript
if(condition){

}
```

---

## Method 1: if statement

```jsx
function App(){

const login = true;


if(login){

 return <h1>Welcome</h1>

}

return <h1>Please Login</h1>

}
```

Output:

```
Welcome
```

---

## Method 2: Ternary Operator (Most used)

Syntax:

```javascript
condition ? true : false
```

Example:

```jsx
function App(){

const isAdmin = true;


return (

<div>

{
 isAdmin
 ?
 <h1>Admin Panel</h1>
 :
 <h1>User Panel</h1>
}


</div>

)

}
```

Output:

```
Admin Panel
```

---

## Method 3: Logical AND (&&)

When you only want to show something if true.

Example:

```jsx
function App(){

const show = true;


return (

<div>

{
 show && <h1>Hello React</h1>
}

</div>

)

}
```

If:

```javascript
show = true
```

Output:

```
Hello React
```

If:

```javascript
show = false
```

Nothing shows.

---

# Conditional Rendering with Props

Example:

Parent:

```jsx
<User isLoggedIn={true}/>
```

Child:

```jsx
function User({isLoggedIn}){


return (

<div>

{
isLoggedIn
?
<h1>Dashboard</h1>
:
<h1>Login</h1>
}

</div>

)

}
```

---

## Summary

### Props

```
Parent → Child
(read only)
```

### React two-way pattern

```
Child
 |
 | function props
 ↓
Parent state update
```

### Conditional rendering

```jsx
if

ternary ?

&&
```

These three concepts are the foundation of React component communication.

-----------

React এ **conditional rendering** করার কয়েকটি common way আছে। মূলত JavaScript logic ব্যবহার করেই UI দেখানো/লুকানো হয়।

## 1. if Statement

সবচেয়ে basic way.

```jsx
function App(){

  const isLogin = true;

  if(isLogin){
    return <h1>Welcome User</h1>;
  }

  return <h1>Please Login</h1>;

}
```

যদি `isLogin = true`

Output:

```
Welcome User
```

---

## 2. if...else

```jsx
function App(){

 const age = 20;

 if(age >= 18){
   return <h1>Adult</h1>;
 }
 else{
   return <h1>Child</h1>;
 }

}
```

---

## 3. Ternary Operator `? :` (Most Used)

Syntax:

```javascript
condition ? true : false
```

Example:

```jsx
function App(){

 const login = true;

 return (
   <div>

    {
      login 
      ? <h1>Dashboard</h1>
      : <h1>Login Page</h1>
    }

   </div>
 )

}
```

Output:

```
Dashboard
```

---

## 4. Logical AND `&&`

যখন শুধু true হলে কিছু দেখাবো।

Example:

```jsx
function App(){

 const show = true;

 return (
   <div>

    {
      show && <h1>Hello React</h1>
    }

   </div>
 )

}
```

`show=true`

Output:

```
Hello React
```

`show=false`

Nothing render হবে।

---

## 5. Logical OR `||`

Default value দেওয়ার জন্য।

Example:

```jsx
function App(){

 const username = "";

 return (
   <h1>
    {username || "Guest"}
   </h1>
 )

}
```

Output:

```
Guest
```

কারণ username empty।

---

## 6. Switch Case

Multiple condition এর জন্য ভালো।

```jsx
function App(){

 const role = "admin";


 switch(role){

  case "admin":
    return <h1>Admin Panel</h1>;


  case "user":
    return <h1>User Dashboard</h1>;


  default:
    return <h1>Guest</h1>;

 }

}
```

Output:

```
Admin Panel
```

---

# Real Example

Login system:

```jsx
function Navbar(){

const user = true;


return (

<nav>

{
 user
 ?
 <button>Logout</button>
 :
 <button>Login</button>
}


</nav>

)

}
```

---

## Quick Comparison

|Method|Use Case|
|---|---|
|if|Big condition|
|if else|Two cases|
|ternary|UI switch (most common)|
|&&|Show/hide|
|||
|switch|Many conditions|

React এ সবচেয়ে বেশি ব্যবহার হয়:

1. `ternary ? :`
    
2. `&&`
    
3. `if` return pattern
    
4. `switch` (large conditions)


------------

## Rendering List of Users with `map()` in React

In React, when you have an **array of data** and want to show it in UI, we use JavaScript `map()`.

Example:

```javascript
const users = [
  {
    id: 1,
    name: "Rahim",
    age: 25
  },
  {
    id: 2,
    name: "Karim",
    age: 30
  },
  {
    id: 3,
    name: "John",
    age: 22
  }
];
```

---

## Basic map Example

```jsx
function App(){

const users = [
  {
    id:1,
    name:"Rahim",
    age:25
  },
  {
    id:2,
    name:"Karim",
    age:30
  },
  {
    id:3,
    name:"John",
    age:22
  }
];


return (

<div>

{
 users.map(user => (

   <div>

    <h2>
      {user.name}
    </h2>

    <p>
      Age: {user.age}
    </p>

   </div>

 ))
}

</div>

)

}

export default App;
```

Output:

```
Rahim
Age:25

Karim
Age:30

John
Age:22
```

---

# How map works?

This:

```jsx
users.map(user => {

})
```

means:

Take each user one by one.

First:

```javascript
user = {
 id:1,
 name:"Rahim",
 age:25
}
```

Second:

```javascript
user = {
 id:2,
 name:"Karim",
 age:30
}
```

---

# Using Component

Usually we create a separate component.

## UserCard.jsx

```jsx
function UserCard({user}){

return (

<div>

<h2>
 {user.name}
</h2>

<p>
 Age: {user.age}
</p>

</div>

)

}

export default UserCard;
```

---

## App.jsx

```jsx
import UserCard from "./UserCard";


function App(){

const users = [
 {
  id:1,
  name:"Rahim",
  age:25
 },

 {
  id:2,
  name:"Karim",
  age:30
 },

 {
  id:3,
  name:"John",
  age:22
 }

];


return (

<div>

{
 users.map(user => (

   <UserCard
     key={user.id}
     user={user}
   />

 ))
}

</div>

)

}

export default App;
```

---

# Why use `key`?

React needs a unique identifier.

Good:

```jsx
<UserCard
 key={user.id}
 user={user}
/>
```

Bad:

```jsx
<UserCard
 key={index}
/>
```

Because React uses `key` to know:

- which item changed
    
- which item removed
    
- which item updated
    

---

# Using index

If no id:

```jsx
{
 users.map((user,index)=>(

  <h1 key={index}>
    {user.name}
  </h1>

 ))
}
```

---

# List with condition

Example: only show adults

```jsx
{
users
.filter(user=>user.age>=18)
.map(user=>(

 <p key={user.id}>
   {user.name}
 </p>

))
}
```

Output:

```
Rahim
Karim
John
```

---

## Short Formula

List rendering:

```jsx
array.map(item => UI)
```

Example:

```jsx
users.map(user => (
 <UserCard user={user}/>
))
```

**Array → map → Component → UI** ✅

-----------
