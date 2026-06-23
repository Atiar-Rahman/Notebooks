**DOM** stands for **Document Object Model**. It is a way that a web browser represents an **HTML page as a tree of objects** so that programming languages like JavaScript can read and change the page.

In simple words:

> The DOM is the browser's "map" of a webpage that JavaScript can use to modify content, style, and structure.

### Example HTML:

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Page</title>
</head>
<body>

  <h1 id="title">Hello World</h1>
  <p>This is a paragraph.</p>
  <button>Click Me</button>

</body>
</html>
```

The browser converts this into a DOM tree like:

```
Document
 └── html
      ├── head
      │    └── title
      │          └── "My Page"
      │
      └── body
           ├── h1
           │    └── "Hello World"
           │
           ├── p
           │    └── "This is a paragraph."
           │
           └── button
                └── "Click Me"
```

Each HTML element becomes a **node** (object) in the DOM.

---

### Using JavaScript with DOM

Suppose we want to change the heading text.

HTML:

```html
<h1 id="title">Hello World</h1>
```

JavaScript:

```javascript
let heading = document.getElementById("title");

heading.innerHTML = "Welcome!";
```

Before:

```
Hello World
```

After JavaScript runs:

```
Welcome!
```

The DOM allowed JavaScript to find the `<h1>` and change it.

---

### Another Example: Button Click

HTML:

```html
<button onclick="changeText()">Click</button>

<p id="message">Waiting...</p>
```

JavaScript:

```javascript
function changeText() {
  document.getElementById("message").innerHTML = "Button clicked!";
}
```

When the user clicks the button, the DOM updates the paragraph.

---

### Common DOM actions

|Action|Example|
|---|---|
|Find element|`document.getElementById("id")`|
|Change text|`element.innerHTML = "new text"`|
|Change style|`element.style.color = "red"`|
|Add element|`document.createElement()`|
|Remove element|`element.remove()`|

So, the DOM is basically the **bridge between HTML and JavaScript** that lets a webpage become interactive.


-------------
# `getElementsByTagName()` is a DOM method used to **select HTML elements by their tag name** (like `p`, `h1`, `div`, `button`, etc.).

### Syntax

```javascript
document.getElementsByTagName("tagName")
```

It returns a **collection (HTMLCollection)** of all matching elements.

---

### Example

HTML:

```html
<h1>My Website</h1>

<p>First paragraph</p>
<p>Second paragraph</p>

<button>Click</button>
```

JavaScript:

```javascript
let paragraphs = document.getElementsByTagName("p");

console.log(paragraphs);
```

Output:

```
HTMLCollection(2) [p, p]
```

It found both `<p>` elements.

---

### Access a specific element

Because it returns multiple elements, use an index:

```javascript
let paragraphs = document.getElementsByTagName("p");

console.log(paragraphs[0].innerHTML);
```

Output:

```
First paragraph
```

---

### Change all elements

Example: change all paragraphs to red:

```javascript
let paragraphs = document.getElementsByTagName("p");

for (let i = 0; i < paragraphs.length; i++) {
    paragraphs[i].style.color = "red";
}
```

Now both paragraphs become red.

---

### Example with buttons

HTML:

```html
<button>One</button>
<button>Two</button>
<button>Three</button>
```

JavaScript:

```javascript
let buttons = document.getElementsByTagName("button");

buttons[1].innerHTML = "Changed";
```

Result:

```
One
Changed
Three
```

---

### Difference from `getElementById()`

|Method|Selects|Returns|
|---|---|---|
|`getElementById()`|One element by id|Single element|
|`getElementsByTagName()`|Many elements by tag|HTMLCollection|

Example:

```javascript
document.getElementById("title");     // one element

document.getElementsByTagName("p");   // many paragraphs
```

Note: The method name is **`getElementsByTagName`** (plural "Elements"), not `getElementByTagName`.

-----------

# There are two common DOM methods:

1. `getElementById()` → finds **one element** using its `id`
    
2. `getElementsByClassName()` → finds **multiple elements** using their `class`
    

(Notice: `getElementsByClassName` has **Elements** plural.)

---

## 1. `getElementById()`

### HTML:

```html
<h1 id="title">Hello World</h1>
<p id="text">This is a paragraph</p>
```

### JavaScript:

```javascript
let heading = document.getElementById("title");

heading.innerHTML = "Welcome!";
```

Result:

Before:

```
Hello World
```

After:

```
Welcome!
```

Because JavaScript found:

```html
<h1 id="title">
```

and changed its content.

---

## 2. `getElementsByClassName()`

Used when multiple elements have the same class.

### HTML:

```html
<p class="message">First message</p>
<p class="message">Second message</p>
<p class="message">Third message</p>
```

### JavaScript:

```javascript
let messages = document.getElementsByClassName("message");

messages[0].innerHTML = "Changed first";
```

Result:

```
Changed first
Second message
Third message
```

---

### Change all class elements

```javascript
let messages = document.getElementsByClassName("message");

for (let i = 0; i < messages.length; i++) {
    messages[i].style.color = "blue";
}
```

All paragraphs with class `message` become blue.

---

## Difference

|Method|Example|Finds|Returns|
|---|---|---|---|
|`getElementById()`|`"title"`|One element|Element|
|`getElementsByClassName()`|`"message"`|Many elements|HTMLCollection|

Example:

```javascript
document.getElementById("box");
```

Finds:

```html
<div id="box"></div>
```

---

```javascript
document.getElementsByClassName("box");
```

Finds:

```html
<div class="box"></div>
<div class="box"></div>
<div class="box"></div>
```

A quick rule:

- **id = unique → use `getElementById`**
    
- **class = reusable → use `getElementsByClassName`**

---------------
# `querySelector()` and `querySelectorAll()` are DOM methods that let you select elements using **CSS selectors**.

They are more flexible than `getElementById()` and `getElementsByClassName()`.

---

## 1. `querySelector()`

`querySelector()` returns the **first matching element**.

### HTML:

```html
<h1 class="title">Hello</h1>
<h1 class="title">Welcome</h1>
```

### JavaScript:

```javascript
let heading = document.querySelector(".title");

heading.innerHTML = "Changed!";
```

Result:

```html
<h1 class="title">Changed!</h1>
<h1 class="title">Welcome</h1>
```

Only the **first** `.title` is changed.

---

## Using ID with `querySelector()`

HTML:

```html
<p id="text">Hello</p>
```

JavaScript:

```javascript
let para = document.querySelector("#text");

para.style.color = "red";
```

`#` means **id**.

---

## Using tag name

HTML:

```html
<p>First</p>
<p>Second</p>
```

JavaScript:

```javascript
let p = document.querySelector("p");

p.innerHTML = "Changed";
```

Only the first `<p>` changes.

---

# 2. `querySelectorAll()`

`querySelectorAll()` returns **all matching elements**.

Example:

HTML:

```html
<p class="item">Apple</p>
<p class="item">Banana</p>
<p class="item">Orange</p>
```

JavaScript:

```javascript
let items = document.querySelectorAll(".item");

console.log(items);
```

Output:

```
NodeList(3)
```

---

### Change all elements

```javascript
let items = document.querySelectorAll(".item");

for (let i = 0; i < items.length; i++) {
    items[i].style.color = "green";
}
```

All three paragraphs become green.

---

## Difference

|Method|Returns|Example|
|---|---|---|
|`querySelector()`|First matching element|`document.querySelector(".box")`|
|`querySelectorAll()`|All matching elements|`document.querySelectorAll(".box")`|

---

## CSS selector examples

```javascript
document.querySelector("p");        // tag

document.querySelector(".box");     // class

document.querySelector("#header");  // id

document.querySelector("div p");    // p inside div

document.querySelectorAll("li");    // all list items
```

A simple memory trick:

- **querySelector → one**
    
- **querySelectorAll → many**
-----------

# These are common DOM properties/methods used to **change HTML, CSS styles, and attributes** using JavaScript.

---

## 1. Dynamic Style (`element.style`)

Used to change CSS using JavaScript.

### HTML:

```html
<p id="text">Hello</p>
```

### JavaScript:

```javascript
let para = document.getElementById("text");

para.style.color = "red";
para.style.backgroundColor = "yellow";
para.style.fontSize = "30px";
```

Result:

```html
<p style="color:red; background-color:yellow; font-size:30px;">
Hello
</p>
```

You can change any CSS property dynamically.

---

## 2. `getAttribute()`

Used to **get the value of an HTML attribute**.

### HTML:

```html
<img id="photo" src="cat.jpg" alt="Cat image">
```

JavaScript:

```javascript
let image = document.getElementById("photo");

let value = image.getAttribute("src");

console.log(value);
```

Output:

```
cat.jpg
```

It reads the attribute.

---

## 3. `setAttribute()`

Used to **add or change an attribute**.

### HTML:

```html
<p id="message">Hello</p>
```

JavaScript:

```javascript
let text = document.getElementById("message");

text.setAttribute("class", "box");
```

Now HTML becomes:

```html
<p id="message" class="box">
Hello
</p>
```

---

Example changing image:

```javascript
let image = document.getElementById("photo");

image.setAttribute("src", "dog.jpg");
```

Before:

```html
<img src="cat.jpg">
```

After:

```html
<img src="dog.jpg">
```

---

# 4. `innerText`

Gets or changes **only the visible text** inside an element.

HTML:

```html
<h1 id="title">
Hello <span>World</span>
</h1>
```

JavaScript:

```javascript
let h = document.getElementById("title");

console.log(h.innerText);
```

Output:

```
Hello World
```

Change text:

```javascript
h.innerText = "New Text";
```

HTML becomes:

```html
<h1 id="title">
New Text
</h1>
```

---

# 5. `innerHTML`

Gets or changes the **HTML content inside an element**.

Example:

```javascript
let h = document.getElementById("title");

h.innerHTML = "Hello <b>JavaScript</b>";
```

Result:

```html
<h1>
Hello <b>JavaScript</b>
</h1>
```

The `<b>` tag works because `innerHTML` reads HTML.

---

## Difference: `innerText` vs `innerHTML`

HTML:

```html
<div id="box">
Hello <b>World</b>
</div>
```

### innerText:

```javascript
box.innerText
```

Output:

```
Hello World
```

Only text.

---

### innerHTML:

```javascript
box.innerHTML
```

Output:

```html
Hello <b>World</b>
```

HTML tags included.

---

## Quick summary

|Feature|Purpose|
|---|---|
|`style`|Change CSS|
|`getAttribute()`|Read attribute|
|`setAttribute()`|Change/add attribute|
|`innerText`|Get/set text|
|`innerHTML`|Get/set HTML|

Example together:

```javascript
let box = document.querySelector("#box");

box.style.color = "blue";

box.setAttribute("class", "container");

box.innerText = "Hello";

box.innerHTML = "<h2>Welcome</h2>";
```

These are some of the most used DOM tools in JavaScript.


# In JavaScript, you can style DOM elements in two main ways:

1. **Using DOM style properties**
    
2. **Adding/removing CSS classes**
    

---

## 1. Styling DOM using `style` property

HTML:

```html
<div id="box">Hello</div>
```

JavaScript:

```javascript
let box = document.getElementById("box");

box.style.color = "white";
box.style.backgroundColor = "black";
box.style.fontSize = "25px";
box.style.padding = "20px";
```

The browser changes the inline CSS:

```html
<div id="box" style="color:white; background-color:black;">
Hello
</div>
```

---

## 2. Changing multiple styles

```javascript
let box = document.querySelector("#box");

box.style.width = "200px";
box.style.height = "100px";
box.style.border = "2px solid black";
```

---

## 3. Add CSS Class using JavaScript

Usually, we write CSS separately.

### CSS:

```css
.box {
    background-color: blue;
    color: white;
    padding: 20px;
}
```

### HTML:

```html
<div id="card">Hello</div>
```

### JavaScript:

```javascript
let card = document.getElementById("card");

card.classList.add("box");
```

Now the element becomes:

```html
<div id="card" class="box">
Hello
</div>
```

---

# 4. Remove CSS Class

```javascript
card.classList.remove("box");
```

The class disappears.

Before:

```html
<div class="box">
```

After:

```html
<div>
```

---

# 5. Toggle CSS Class

`toggle()` adds the class if it does not exist, and removes it if it exists.

CSS:

```css
.active {
    color: green;
}
```

JavaScript:

```javascript
let text = document.querySelector("#text");

text.classList.toggle("active");
```

First click:

```html
<p class="active">
```

Second click:

```html
<p>
```

---

# 6. Check if class exists

```javascript
if (text.classList.contains("active")) {
    console.log("Class exists");
}
```

Returns:

```
true
```

or

```
false
```

---

## Example: Button changes style

HTML:

```html
<button id="btn">Change</button>

<p id="message">Hello</p>
```

CSS:

```css
.highlight {
    background: yellow;
    color: red;
}
```

JavaScript:

```javascript
let btn = document.getElementById("btn");
let message = document.getElementById("message");

btn.onclick = function() {
    message.classList.add("highlight");
};
```

Clicking the button adds the CSS class.

---

## Summary

|Method|Use|
|---|---|
|`element.style.color`|Change one CSS property|
|`classList.add()`|Add a class|
|`classList.remove()`|Remove a class|
|`classList.toggle()`|Add/remove automatically|
|`classList.contains()`|Check class|

For larger projects, `classList` is usually preferred because your CSS stays separate from JavaScript.

---------------

# These are important **DOM concepts** in JavaScript. They help you work with elements, their parents, children, and create new elements.

---

# 1. NodeList

A **NodeList** is a collection of nodes returned by methods like:

```javascript
querySelectorAll()
```

Example:

HTML:

```html
<p>One</p>
<p>Two</p>
<p>Three</p>
```

JavaScript:

```javascript
let items = document.querySelectorAll("p");

console.log(items);
```

Output:

```
NodeList(3) [p, p, p]
```

Access items:

```javascript
console.log(items[0].innerText);
```

Output:

```
One
```

Loop:

```javascript
items.forEach(function(item) {
    item.style.color = "blue";
});
```

---

# 2. HTMLCollection

An **HTMLCollection** is a collection of HTML elements.

Commonly returned by:

```javascript
getElementsByClassName()
getElementsByTagName()
```

Example:

HTML:

```html
<div class="box">A</div>
<div class="box">B</div>
```

JavaScript:

```javascript
let boxes = document.getElementsByClassName("box");

console.log(boxes);
```

Output:

```
HTMLCollection(2) [div.box, div.box]
```

Access:

```javascript
boxes[1].innerText = "Changed";
```

---

## NodeList vs HTMLCollection

|NodeList|HTMLCollection|
|---|---|
|From `querySelectorAll()`|From `getElements...()`|
|Can use `forEach()`|Older collection|
|Can contain any node|Only HTML elements|
|Usually static|Often live|

---

# 3. ParentNode

`parentNode` gives the **parent element** of a node.

HTML:

```html
<div id="parent">
    <p id="child">Hello</p>
</div>
```

JavaScript:

```javascript
let child = document.getElementById("child");

console.log(child.parentNode);
```

Output:

```html
<div id="parent">
```

You can change parent:

```javascript
child.parentNode.style.backgroundColor = "yellow";
```

---

# 4. ChildNodes

`childNodes` gives all children of an element.

Example:

HTML:

```html
<div id="box">
    <p>Hello</p>
    <button>Click</button>
</div>
```

JavaScript:

```javascript
let box = document.getElementById("box");

console.log(box.childNodes);
```

Output:

```
NodeList
[p, button]
```

Access child:

```javascript
console.log(box.childNodes[0]);
```

---

## Important

`childNodes` can include text spaces and line breaks.

Example:

```html
<div>
   Hello
</div>
```

may include:

```
#text
```

For only elements use:

```javascript
box.children
```

---

# 5. CreateElement()

`createElement()` creates a new HTML element using JavaScript.

Example:

```javascript
let newText = document.createElement("p");
```

Now add content:

```javascript
newText.innerText = "New paragraph";
```

Add it to the page:

```javascript
document.body.appendChild(newText);
```

Result:

```html
<p>New paragraph</p>
```

---

## Complete Example

HTML:

```html
<div id="container">
    <h1>Hello</h1>
</div>
```

JavaScript:

```javascript
let container = document.getElementById("container");

// create element
let p = document.createElement("p");

// add text
p.innerText = "Welcome to DOM";

// add to HTML
container.appendChild(p);
```

Result:

```html
<div id="container">
    <h1>Hello</h1>
    <p>Welcome to DOM</p>
</div>
```

---

### Quick memory:

- **NodeList** → group of nodes
    
- **HTMLCollection** → group of HTML elements
    
- **parentNode** → go upward
    
- **childNodes** → go downward
    
- **createElement()** → make new HTML element
    
- **appendChild()** → put it into the page
------------

# In JavaScript, you can **create new HTML elements** using `createElement()` and add them to the page using `appendChild()`.

---

## 1. `createElement()`

`createElement()` creates a new HTML element.

Syntax:

```javascript
document.createElement("tagName")
```

Example:

```javascript
let heading = document.createElement("h1");
```

Now JavaScript created:

```html
<h1></h1>
```

but it is not visible yet because it is not added to the page.

---

## 2. Add text using `innerText`

```javascript
let heading = document.createElement("h1");

heading.innerText = "Hello JavaScript";
```

Now it contains:

```html
<h1>Hello JavaScript</h1>
```

---

## 3. Add element using `appendChild()`

HTML:

```html
<body>
    <div id="container"></div>
</body>
```

JavaScript:

```javascript
let heading = document.createElement("h1");

heading.innerText = "Hello JavaScript";

let container = document.getElementById("container");

container.appendChild(heading);
```

Result:

```html
<div id="container">
    <h1>Hello JavaScript</h1>
</div>
```

---

# Example: Create a paragraph

HTML:

```html
<div id="box"></div>
```

JavaScript:

```javascript
let paragraph = document.createElement("p");

paragraph.innerText = "This is a new paragraph";

document.getElementById("box")
        .appendChild(paragraph);
```

Output:

```html
<div id="box">
    <p>This is a new paragraph</p>
</div>
```

---

# Example: Create a list

HTML:

```html
<ul id="list"></ul>
```

JavaScript:

```javascript
let li = document.createElement("li");

li.innerText = "Apple";

let list = document.getElementById("list");

list.appendChild(li);
```

Output:

```html
<ul id="list">
    <li>Apple</li>
</ul>
```

---

# Adding multiple elements

```javascript
let list = document.getElementById("list");

let fruits = ["Apple", "Banana", "Orange"];

fruits.forEach(function(fruit){

    let item = document.createElement("li");

    item.innerText = fruit;

    list.appendChild(item);

});
```

Result:

```html
<ul>
    <li>Apple</li>
    <li>Banana</li>
    <li>Orange</li>
</ul>
```

---

# Add class and style to created element

```javascript
let box = document.createElement("div");

box.innerText = "New Box";

box.classList.add("box");

document.body.appendChild(box);
```

---

## Difference:

|Method|Purpose|
|---|---|
|`createElement()`|Creates a new HTML element|
|`innerText`|Adds text|
|`appendChild()`|Adds element to the webpage|

Think of it like:

**Create → Fill → Attach**

```javascript
createElement()
      ↓
innerText / style
      ↓
appendChild()
```


---------------

# What is an Event in JavaScript?

An **event** is an action or occurrence that happens in a webpage, which JavaScript can detect and respond to.

Examples:

- A user clicks a button
    
- A keyboard key is pressed
    
- A mouse moves
    
- A page loads
    
- A form is submitted
    

JavaScript uses events to make webpages **interactive**.

---

## Basic Event Example

HTML:

```html
<button id="btn">Click Me</button>
```

JavaScript:

```javascript
let button = document.getElementById("btn");

button.onclick = function() {
    alert("Button clicked!");
};
```

When the user clicks the button, the event runs.

---

# Types of Events in Web

## 1. Mouse Events

Events caused by mouse actions.

### `click`

Runs when an element is clicked.

```javascript
button.onclick = function() {
    console.log("Clicked");
};
```

---

### `dblclick`

Runs on double click.

```javascript
button.ondblclick = function() {
    console.log("Double clicked");
};
```

---

### `mouseover`

Runs when mouse enters an element.

```javascript
box.onmouseover = function() {
    box.style.background = "yellow";
};
```

---

### `mouseout`

Runs when mouse leaves.

```javascript
box.onmouseout = function() {
    box.style.background = "white";
};
```

---

## 2. Keyboard Events

Events from keyboard actions.

### `keydown`

Runs when a key is pressed.

```javascript
document.onkeydown = function() {
    console.log("Key pressed");
};
```

---

### `keyup`

Runs when a key is released.

```javascript
document.onkeyup = function() {
    console.log("Key released");
};
```

---

## 3. Form Events

Used with forms.

### `submit`

Runs when a form is submitted.

```javascript
form.onsubmit = function() {
    console.log("Form submitted");
};
```

---

### `change`

Runs when input value changes.

```javascript
input.onchange = function() {
    console.log("Changed");
};
```

---

### `focus`

Runs when an input is selected.

```javascript
input.onfocus = function() {
    input.style.background = "lightblue";
};
```

---

### `blur`

Runs when input loses focus.

```javascript
input.onblur = function() {
    console.log("Left input");
};
```

---

## 4. Window Events

Related to the browser window.

### `load`

Runs when page finishes loading.

```javascript
window.onload = function() {
    console.log("Page loaded");
};
```

---

### `resize`

Runs when browser size changes.

```javascript
window.onresize = function() {
    console.log("Window resized");
};
```

---

### `scroll`

Runs when scrolling.

```javascript
window.onscroll = function() {
    console.log("Scrolling");
};
```

---

## 5. Clipboard Events

Copy/paste actions.

### Copy

```javascript
text.oncopy = function() {
    console.log("Copied");
};
```

### Paste

```javascript
text.onpaste = function() {
    console.log("Pasted");
};
```

---

## 6. Touch Events (Mobile)

For touch screens.

### `touchstart`

```javascript
box.ontouchstart = function() {
    console.log("Touch started");
};
```

### `touchend`

```javascript
box.ontouchend = function() {
    console.log("Touch ended");
};
```

---

## Modern Way: `addEventListener()`

Instead of `onclick`, we usually use:

```javascript
let btn = document.getElementById("btn");

btn.addEventListener("click", function() {
    alert("Hello");
});
```

---

## Common Events Summary

|Event|Happens when|
|---|---|
|`click`|User clicks|
|`dblclick`|Double click|
|`mouseover`|Mouse enters|
|`mouseout`|Mouse leaves|
|`keydown`|Key pressed|
|`keyup`|Key released|
|`submit`|Form sent|
|`change`|Input changed|
|`focus`|Input selected|
|`blur`|Input loses focus|
|`load`|Page loaded|
|`scroll`|Page scrolling|

Events are what make a webpage respond to user actions.

--------
# There are **two main ways** to handle a click event in JavaScript:

1. **Inline `onclick` in HTML**
    
2. **Using JavaScript (recommended way)**
    

---

# 1. Add `onclick` directly in HTML (Inline Handler)

### HTML:

```html
<button onclick="sayHello()">Click Me</button>
```

### JavaScript:

```javascript
function sayHello() {
    alert("Hello from inline onclick!");
}
```

### How it works:

- You write the event directly inside HTML
    
- When user clicks, it calls the function
    

### Output:

👉 Click button → alert appears

---

## Example with parameter:

```html
<button onclick="greet('Ali')">Greet</button>
```

```javascript
function greet(name) {
    alert("Hello " + name);
}
```

---

# 2. Add `onclick` using JavaScript (Better way)

### HTML:

```html
<button id="btn">Click Me</button>
```

### JavaScript:

```javascript
let button = document.getElementById("btn");

button.onclick = function() {
    alert("Clicked using JavaScript!");
};
```

---

## Another modern way: `addEventListener()`

```javascript
let button = document.getElementById("btn");

button.addEventListener("click", function() {
    alert("Clicked using addEventListener!");
});
```

---

# Difference Between Them

|Method|Where written|Best use|Problem|
|---|---|---|---|
|Inline `onclick`|HTML|Small projects|Not clean, mixes HTML + JS|
|`onclick` in JS|JavaScript file|Better|Can overwrite previous handler|
|`addEventListener()`|JavaScript|**Best practice**|None (modern standard)|

---

# Important Difference

### ❌ Problem with direct `onclick` in JS:

```javascript
button.onclick = function() {
    console.log("First");
};

button.onclick = function() {
    console.log("Second");
};
```

👉 Only **"Second" runs** (first is overwritten)

---

### ✅ Solution: `addEventListener`

```javascript
button.addEventListener("click", function() {
    console.log("First");
});

button.addEventListener("click", function() {
    console.log("Second");
});
```

👉 Both will run ✔️

---

# Final Summary

- **Inline onclick** → quick but outdated
    
- **JS onclick property** → simple but replaces old handlers
    
- **addEventListener()** → best, modern, flexible
    

---

👉 Best practice: Always use **`addEventListener()`** for real projects.

-----------


# Here’s how **Events + innerText/textContent + DOM update** work together in JavaScript.

The idea is simple:

> When an event happens (like click), we update text inside an element.

---

# 1. Basic Example: Change text on click

### HTML:

```html
<button id="btn">Click Me</button>
<p id="text">Old Text</p>
```

### JavaScript:

```javascript
let button = document.getElementById("btn");
let text = document.getElementById("text");

button.addEventListener("click", function() {
    text.innerText = "Text Updated!";
});
```

### What happens:

- User clicks button
    
- Event fires (`click`)
    
- Paragraph text changes
    

---

# 2. Toggle Text using Event

### HTML:

```html
<button id="btn">Toggle</button>
<p id="msg">Hello</p>
```

### JavaScript:

```javascript
let button = document.getElementById("btn");
let msg = document.getElementById("msg");

button.addEventListener("click", function() {
    if (msg.innerText === "Hello") {
        msg.innerText = "Goodbye";
    } else {
        msg.innerText = "Hello";
    }
});
```

### Result:

- Click → "Hello" → "Goodbye"
    
- Click again → back to "Hello"
    

---

# 3. Counter Example (Very Important)

### HTML:

```html
<button id="increase">+</button>
<p id="count">0</p>
```

### JavaScript:

```javascript
let btn = document.getElementById("increase");
let countText = document.getElementById("count");

let count = 0;

btn.addEventListener("click", function() {
    count++;
    countText.innerText = count;
});
```

### Output:

- Click → 1, 2, 3, 4...
    

---

# 4. Change Text + Style on Event

### HTML:

```html
<button id="btn">Change</button>
<p id="text">Original Text</p>
```

### JavaScript:

```javascript
let button = document.getElementById("btn");
let text = document.getElementById("text");

button.addEventListener("click", function() {
    text.innerText = "Updated Text!";
    text.style.color = "red";
    text.style.fontSize = "30px";
});
```

---

# 5. Input Event → Live Text Update

### HTML:

```html
<input type="text" id="inputBox">
<p id="output">Type something...</p>
```

### JavaScript:

```javascript
let input = document.getElementById("inputBox");
let output = document.getElementById("output");

input.addEventListener("input", function() {
    output.innerText = input.value;
});
```

### Result:

👉 Whatever you type shows instantly

---

# 6. Button adds new text (Append style)

### HTML:

```html
<button id="add">Add Text</button>
<p id="list"></p>
```

### JavaScript:

```javascript
let btn = document.getElementById("add");
let list = document.getElementById("list");

btn.addEventListener("click", function() {
    list.innerText = list.innerText + " New Item";
});
```

---

# Key Concepts Together

|Concept|Purpose|
|---|---|
|Event (`click`, `input`)|Detect user action|
|`innerText`|Change visible text|
|`textContent`|Similar to innerText (faster, no HTML parsing)|
|`addEventListener()`|Attach event safely|

---

# Simple Formula

> **Event → Function runs → DOM text updates**

```javascript
element.addEventListener("event", function() {
    element.innerText = "New Value";
});
```

---

