## Event Handling in React

An **event** is an action that happens in the UI:

Examples:

- Button click
    
- Input typing
    
- Form submit
    
- Mouse movement
    
- Keyboard press
    

React handles events using **event handlers**.

---

# 1. Inline Event Handler

Write function directly inside JSX.

```jsx
function App(){

return (
  <button onClick={() => alert("Clicked")}>
    Click Me
  </button>
)

}
```

When click:

```
Clicked
```

---

# 2. Function Reference (Most Common)

Create a function and pass it.

```jsx
function App(){

function handleClick(){

 alert("Button clicked")

}


return (

<button onClick={handleClick}>
 Click
</button>

)

}
```

Important:

Correct:

```jsx
onClick={handleClick}
```

Wrong:

```jsx
onClick={handleClick()}
```

Because `()` runs immediately.

---

# 3. Event Object

React automatically sends an event object.

```jsx
function App(){

function handleClick(event){

 console.log(event)

}


return (

<button onClick={handleClick}>
 Click
</button>

)

}
```

You get information about:

- target
    
- type
    
- mouse position
    

---

Example:

```jsx
function App(){

function handleClick(e){

 console.log(e.type)

}


return (

<button onClick={handleClick}>
Click
</button>

)

}
```

Output:

```
click
```

---

# 4. Passing Arguments to Event Handler

Sometimes you need extra data.

Example:

```jsx
function App(){


function deleteUser(id){

 console.log(id)

}


return (

<button
 onClick={()=>deleteUser(5)}
>
 Delete
</button>

)


}
```

Output:

```
5
```

---

# 5. Handling Input Change Event

Using `onChange`.

```jsx
function App(){

function handleChange(e){

 console.log(e.target.value)

}


return (

<input 
 onChange={handleChange}
/>

)

}
```

If you type:

```
Hello
```

Console:

```
Hello
```

---

# 6. Form Submit Event

Use `onSubmit`.

```jsx
function App(){


function handleSubmit(e){

 e.preventDefault();

 console.log("Submitted")

}


return (

<form onSubmit={handleSubmit}>

<input />

<button>
Submit
</button>

</form>

)

}
```

`preventDefault()` stops page reload.

---

# 7. Mouse Events

## onMouseEnter

```jsx
<div 
 onMouseEnter={()=>console.log("Enter")}
>
 Hover me
</div>
```

---

## onMouseLeave

```jsx
<div
onMouseLeave={()=>console.log("Leave")}
>
Box
</div>
```

---

# 8. Keyboard Events

## onKeyDown

```jsx
<input

onKeyDown={(e)=>{

 console.log(e.key)

}}

/>
```

Press:

```
Enter
```

Output:

```
Enter
```

---

# 9. Using State with Events

Most common React pattern.

```jsx
import {useState} from "react";


function App(){

const [count,setCount]=useState(0);


function increase(){

 setCount(count+1)

}


return (

<div>

<h1>
 {count}
</h1>


<button onClick={increase}>
 +
</button>


</div>

)

}
```

Click button:

```
0 → 1 → 2 → 3
```

---

# 10. Event Handler as Props

Parent:

```jsx
function App(){


function hello(){

 alert("Hello")

}


return (
 <Button click={hello}/>
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

---

# Common React Events

|Event|Usage|
|---|---|
|onClick|Button click|
|onChange|Input change|
|onSubmit|Form submit|
|onMouseEnter|Mouse enter|
|onMouseLeave|Mouse leave|
|onKeyDown|Keyboard|
|onFocus|Input focus|
|onBlur|Input lost focus|

---

## Summary

React event handling styles:

1. Inline function
    

```jsx
onClick={()=>{}}
```

2. Function reference
    

```jsx
onClick={handleClick}
```

3. Event object
    

```jsx
function handle(e){}
```

4. Pass arguments
    

```jsx
onClick={()=>fn(id)}
```

5. Use state update
    

```jsx
setState()
```

6. Pass events through props
    

These patterns cover almost all React event handling.

----------

