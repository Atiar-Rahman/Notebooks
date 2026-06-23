 # CSS3 Complete Learning Guide (Basic → Advanced)

CSS (Cascading Style Sheets) ব্যবহার করা হয় HTML elements কে সুন্দরভাবে ডিজাইন করার জন্য।

---

# 1. CSS Syntax

```css
selector {
    property: value;
}
```

Example:

```css
h1 {
    color: blue;
}
```

---

# 2. Ways to Add CSS

## Inline CSS

```html
<h1 style="color:red;">Hello</h1>
```

## Internal CSS

```html
<style>
h1{
    color:red;
}
</style>
```

## External CSS (Recommended)

```html
<link rel="stylesheet" href="style.css">
```

style.css

```css
h1{
    color:red;
}
```

---

# 3. Selectors

## Element Selector

```css
h1{
    color:red;
}
```

## Class Selector

```css
.title{
    color:green;
}
```

```html
<h1 class="title">Hello</h1>
```

## ID Selector

```css
#heading{
    color:blue;
}
```

```html
<h1 id="heading">Hello</h1>
```

## Universal Selector

```css
*{
    margin:0;
    padding:0;
}
```

---

# 4. Colors

```css
h1{
    color:red;
}
```

Hex

```css
color:#ff0000;
```

RGB

```css
color:rgb(255,0,0);
```

RGBA

```css
color:rgba(255,0,0,0.5);
```

---

# 5. Background

```css
body{
    background-color:lightblue;
}
```

Image

```css
body{
    background-image:url(bg.jpg);
}
```

Cover

```css
body{
    background-size:cover;
}
```

---

# 6. Typography

```css
p{
    font-size:20px;
    font-family:Arial;
    font-weight:bold;
}
```

Text Alignment

```css
text-align:center;
```

Line Height

```css
line-height:1.8;
```

Letter Spacing

```css
letter-spacing:2px;
```

---

# 7. Box Model

Every element contains:

```
Margin
Border
Padding
Content
```

Example:

```css
.box{
    width:300px;
    padding:20px;
    border:5px solid black;
    margin:30px;
}
```

---

# 8. Width & Height

```css
div{
    width:300px;
    height:200px;
}
```

---

# 9. Border

```css
border:2px solid red;
```

```css
border-radius:10px;
```

Circle

```css
border-radius:50%;
```

---

# 10. Margin

```css
margin:20px;
```

```css
margin-top:20px;
```

Center Div

```css
margin:auto;
```

---

# 11. Padding

```css
padding:20px;
```

```css
padding:10px 20px;
```

---

# 12. Display Property

### Block

```css
display:block;
```

### Inline

```css
display:inline;
```

### Inline Block

```css
display:inline-block;
```

### None

```css
display:none;
```

---

# 13. Position

## Static

```css
position:static;
```

## Relative

```css
position:relative;
left:20px;
```

## Absolute

```css
position:absolute;
top:0;
right:0;
```

## Fixed

```css
position:fixed;
```

## Sticky

```css
position:sticky;
top:0;
```

---

# 14. Flexbox

Most Important Topic

Container:

```css
.container{
    display:flex;
}
```

Direction

```css
flex-direction:row;
```

Column

```css
flex-direction:column;
```

Center

```css
justify-content:center;
align-items:center;
```

Space Between

```css
justify-content:space-between;
```

Example:

```css
.container{
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}
```

---

# 15. CSS Grid

```css
.container{
    display:grid;
    grid-template-columns:1fr 1fr 1fr;
}
```

Gap

```css
gap:20px;
```

Example

```css
.container{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:20px;
}
```

---

# 16. Overflow

```css
overflow:hidden;
```

```css
overflow:scroll;
```

```css
overflow:auto;
```

---

# 17. Z-Index

```css
.box{
    z-index:10;
}
```

Works with positioned elements.

---

# 18. Pseudo Classes

Hover

```css
button:hover{
    background:red;
}
```

Focus

```css
input:focus{
    border:2px solid blue;
}
```

First Child

```css
li:first-child{
    color:red;
}
```

Last Child

```css
li:last-child{
    color:green;
}
```

---

# 19. Pseudo Elements

```css
p::first-letter{
    font-size:40px;
}
```

```css
p::first-line{
    color:red;
}
```

```css
::selection{
    background:yellow;
}
```

---

# 20. CSS Variables

```css
:root{
    --main-color:blue;
}
```

Use

```css
h1{
    color:var(--main-color);
}
```

---

# 21. Transform

Rotate

```css
transform:rotate(45deg);
```

Scale

```css
transform:scale(1.2);
```

Translate

```css
transform:translateX(50px);
```

---

# 22. Transition

```css
button{
    transition:0.5s;
}
```

```css
button:hover{
    background:red;
}
```

---

# 23. Animation

```css
@keyframes move{
    from{
        left:0;
    }
    to{
        left:200px;
    }
}
```

Use

```css
.box{
    position:relative;
    animation:move 3s infinite;
}
```

---

# 24. Media Queries (Responsive Design)

Mobile

```css
@media(max-width:768px){

    h1{
        font-size:20px;
    }

}
```

Tablet

```css
@media(max-width:992px){

}
```

---

# 25. CSS Functions

Calc

```css
width:calc(100% - 50px);
```

Clamp

```css
font-size:clamp(1rem,3vw,3rem);
```

---

# 26. Object Fit

```css
img{
    object-fit:cover;
}
```

---

# 27. Filter

Blur

```css
filter:blur(5px);
```

Brightness

```css
filter:brightness(150%);
```

---

# 28. Box Shadow

```css
box-shadow:0 4px 10px rgba(0,0,0,.3);
```

---

# 29. Text Shadow

```css
text-shadow:2px 2px 5px gray;
```

---

# 30. Modern Card Example

HTML

```html
<div class="card">
    <h2>CSS3 Course</h2>
    <p>Learn CSS from basic to advanced</p>
    <button>Enroll</button>
</div>
```

CSS

```css
.card{
    width:300px;
    padding:20px;
    border-radius:10px;
    box-shadow:0 5px 15px rgba(0,0,0,.2);
    transition:.3s;
}

.card:hover{
    transform:translateY(-10px);
}
```

---

# Advanced Topics (Must Learn for Jobs)

### Flexbox

* justify-content
* align-items
* flex-wrap
* gap

### Grid

* grid-template-columns
* auto-fit
* auto-fill
* minmax()

### Responsive Design

* Media Queries
* Mobile First

### CSS Variables

### Animations

### Transforms

### Transitions

### BEM Naming

Example:

```css
.card{}
.card__title{}
.card__button{}
```

### CSS Specificity

```css
Inline > ID > Class > Element
```

---

# CSS Learning Roadmap (15 Days)

### Day 1-2

* Syntax
* Selectors
* Colors
* Typography

### Day 3-4

* Box Model
* Margin
* Padding
* Border

### Day 5-6

* Position
* Display

### Day 7-8

* Flexbox

### Day 9-10

* Grid

### Day 11

* Responsive Design

### Day 12

* Transform
* Transition

### Day 13

* Animation

### Day 14

* Variables
* Shadows
* Filters

### Day 15

* Build:

  * Landing Page
  * Portfolio
  * E-commerce Homepage

যেহেতু তুমি Frontend Development শিখছ, HTML5 শেষ করার পর **Flexbox + Grid + Responsive Design** সবচেয়ে বেশি প্র্যাকটিস করো। চাকরির ইন্টারভিউতে CSS-এর ৭০% প্রশ্ন এই তিনটি টপিক থেকেই আসে।


--------------

# Day 12: Transform & Transition

## 1. CSS Transform

`transform` ব্যবহার করে element-এর shape, size, position, rotation পরিবর্তন করা যায়।

---

### Rotate

```css
.box{
    transform: rotate(45deg);
}
```

genui{"math_block_widget_always_prefetch_v2":{"content":"y=x"}}

এখানে element 45° rotate হবে।

---

### Scale

Element বড় বা ছোট করা।

```css
.box{
    transform: scale(1.5);
}
```

* `1` = original size
* `1.5` = 150% size
* `0.5` = 50% size

---

### Translate

Element move করানো।

```css
.box{
    transform: translateX(100px);
}
```

```css
.box{
    transform: translateY(50px);
}
```

```css
.box{
    transform: translate(100px, 50px);
}
```

---

### Skew

Element কে বাঁকা করা।

```css
.box{
    transform: skewX(20deg);
}
```

```css
.box{
    transform: skewY(20deg);
}
```

---

### Multiple Transform

```css
.box{
    transform:
        translateX(100px)
        rotate(45deg)
        scale(1.2);
}
```

---

## Real Example

```html
<div class="card">
    Hover Me
</div>
```

```css
.card{
    width:200px;
    padding:20px;
    background:lightblue;
}

.card:hover{
    transform:
        scale(1.1)
        rotate(3deg);
}
```

---

# 2. CSS Transition

Transition animation কে smooth করে।

Without transition:

```css
button:hover{
    background:red;
}
```

Instant change হবে।

---

### With Transition

```css
button{
    transition:0.5s;
}

button:hover{
    background:red;
}
```

Smooth change হবে।

---

### Syntax

```css
transition:
    property
    duration
    timing-function
    delay;
```

Example:

```css
transition:
    background-color
    0.5s
    ease;
```

---

### Timing Functions

```css
ease
linear
ease-in
ease-out
ease-in-out
```

Example:

```css
transition: all 0.5s ease;
```

---

### Professional Hover Button

```css
.btn{
    background:blue;
    color:white;
    padding:10px 20px;

    transition:0.3s;
}

.btn:hover{
    background:black;
    transform:translateY(-5px);
}
```

---

# Day 13: CSS Animation

Transition user interaction-এর উপর নির্ভর করে।

Animation automatically চলতে পারে।

---

## Keyframes

```css
@keyframes move{

    from{
        left:0;
    }

    to{
        left:200px;
    }

}
```

---

## Using Animation

```css
.box{

    position:relative;

    animation:
        move
        2s
        infinite;

}
```

---

## Full Example

```html
<div class="box"></div>
```

```css
.box{

    width:100px;
    height:100px;

    background:red;

    position:relative;

    animation:move 3s infinite;
}

@keyframes move{

    0%{
        left:0;
    }

    50%{
        left:200px;
    }

    100%{
        left:0;
    }

}
```

---

## Animation Properties

### Duration

```css
animation-duration:2s;
```

### Delay

```css
animation-delay:1s;
```

### Iteration Count

```css
animation-iteration-count:infinite;
```

### Direction

```css
animation-direction:alternate;
```

### Timing

```css
animation-timing-function:ease;
```

---

## Loading Spinner Example

```html
<div class="loader"></div>
```

```css
.loader{

    width:50px;
    height:50px;

    border:5px solid gray;
    border-top:5px solid blue;

    border-radius:50%;

    animation:spin 1s linear infinite;
}

@keyframes spin{

    from{
        transform:rotate(0deg);
    }

    to{
        transform:rotate(360deg);
    }

}
```

---

## Floating Animation

```css
.card{
    animation:float 2s infinite;
}

@keyframes float{

    0%{
        transform:translateY(0);
    }

    50%{
        transform:translateY(-20px);
    }

    100%{
        transform:translateY(0);
    }

}
```

---

# Day 14: CSS Variables

Variables reusable values store করে।

---

## Define Variable

```css
:root{

    --primary-color: blue;
    --secondary-color: green;

}
```

---

## Use Variable

```css
h1{
    color:var(--primary-color);
}
```

```css
button{
    background:var(--primary-color);
}
```

---

## Theme Example

```css
:root{

    --bg:#fff;
    --text:#222;

}

body{

    background:var(--bg);
    color:var(--text);

}
```

---

## Variable Fallback

```css
color:var(--main-color, red);
```

যদি variable না থাকে, red ব্যবহার হবে।

---

# Box Shadow

Shadow দিয়ে card বা button কে modern look দেওয়া হয়।

---

## Basic Shadow

```css
box-shadow:
0 4px 10px rgba(0,0,0,.3);
```

Meaning:

```text
0   = X axis
4px = Y axis
10px = Blur
rgba(...) = Color
```

---

## Card Example

```css
.card{

    width:300px;
    padding:20px;

    box-shadow:
    0 10px 25px rgba(0,0,0,.15);

}
```

---

## Hover Shadow

```css
.card{

    transition:.3s;
}

.card:hover{

    box-shadow:
    0 20px 40px rgba(0,0,0,.2);

}
```

---

## Multiple Shadows

```css
box-shadow:

0 2px 5px rgba(0,0,0,.2),

0 10px 20px rgba(0,0,0,.1);
```

---

# Text Shadow

```css
h1{

    text-shadow:
    2px 2px 5px gray;

}
```

---

# CSS Filters

Filter image বা element-এর appearance পরিবর্তন করে।

---

## Blur

```css
img{

    filter:blur(5px);

}
```

---

## Brightness

```css
img{

    filter:brightness(150%);

}
```

---

## Contrast

```css
img{

    filter:contrast(200%);

}
```

---

## Grayscale

Black & White image

```css
img{

    filter:grayscale(100%);

}
```

---

## Sepia

Old photo effect

```css
img{

    filter:sepia(100%);

}
```

---

## Invert

```css
img{

    filter:invert(100%);

}
```

---

## Drop Shadow

```css
img{

    filter:
    drop-shadow(
        0 0 10px black
    );

}
```

---

## Multiple Filters

```css
img{

    filter:
        grayscale(100%)
        blur(2px)
        brightness(120%);

}
```

---

# Real Project Example (Modern Card)

```css
.card{

    width:300px;

    padding:20px;

    border-radius:15px;

    background:white;

    box-shadow:
        0 10px 30px rgba(0,0,0,.1);

    transition:.3s;
}

.card:hover{

    transform:
        translateY(-10px);

    box-shadow:
        0 20px 40px rgba(0,0,0,.2);

}
```

এই ৫টা টপিক (Transform, Transition, Animation, Variables, Shadow/Filter) ভালোভাবে শিখলে তুমি আধুনিক Portfolio Website, Landing Page, Dashboard UI, E-commerce Homepage-এর 90% visual effects তৈরি করতে পারবে। এরপরের গুরুত্বপূর্ণ ধাপ হলো **Flexbox + Grid + Responsive Design + CSS Architecture (BEM)** গভীরভাবে প্র্যাকটিস করা।


----------
# CSS Interview & Practice Questions (50 Questions with Answers)

## Basic CSS

### 1. What is CSS?

**Answer:** CSS (Cascading Style Sheets) is used to style and design HTML elements.

---

### 2. What does CSS stand for?

**Answer:** Cascading Style Sheets.

---

### 3. How many ways can CSS be added to HTML?

**Answer:** Three ways:

* Inline CSS
* Internal CSS
* External CSS

---

### 4. Which CSS method is recommended?

**Answer:** External CSS.

---

### 5. What is a CSS Selector?

**Answer:** A selector targets HTML elements to apply styles.

Example:

```css
p {
    color: red;
}
```

---

### 6. Difference between Class and ID?

**Answer:**

| Class    | ID     |
| -------- | ------ |
| Reusable | Unique |
| .class   | #id    |

---

### 7. What does the Universal Selector do?

**Answer:**

```css
*{
    margin:0;
    padding:0;
}
```

Selects all elements.

---

### 8. What is the default position property?

**Answer:** `static`

---

### 9. What is CSS Specificity?

**Answer:**

Priority order:

```text
Inline > ID > Class > Element
```

---

### 10. What is the Box Model?

**Answer:**

```text
Content
Padding
Border
Margin
```

---

# Colors & Typography

### 11. How many color formats are commonly used?

**Answer:**

* Name
* HEX
* RGB
* RGBA
* HSL

---

### 12. Difference between RGB and RGBA?

**Answer:**

RGBA includes opacity.

```css
rgba(255,0,0,0.5)
```

---

### 13. What property changes text color?

**Answer:**

```css
color:red;
```

---

### 14. What property changes font size?

**Answer:**

```css
font-size:20px;
```

---

### 15. What property makes text bold?

**Answer:**

```css
font-weight:bold;
```

---

# Margin, Padding, Border

### 16. Difference between Margin and Padding?

**Answer:**

| Margin        | Padding      |
| ------------- | ------------ |
| Outside Space | Inside Space |

---

### 17. How to center a block element?

**Answer:**

```css
margin:auto;
```

---

### 18. How to create a circle?

**Answer:**

```css
border-radius:50%;
```

---

### 19. What is border shorthand?

**Answer:**

```css
border:2px solid red;
```

---

### 20. What does box-sizing:border-box do?

**Answer:**

Includes padding and border inside width.

```css
box-sizing:border-box;
```

---

# Display & Position

### 21. Difference between Block and Inline?

**Answer:**

Block:

* Takes full width
* Starts new line

Inline:

* Takes content width
* No new line

---

### 22. What does display:none do?

**Answer:**

Hides the element completely.

---

### 23. Difference between visibility:hidden and display:none?

**Answer:**

`display:none`

* Removes element

`visibility:hidden`

* Keeps space reserved

---

### 24. What is Relative Position?

**Answer:**

Moves element relative to its normal position.

---

### 25. What is Absolute Position?

**Answer:**

Positions element relative to nearest positioned parent.

---

### 26. What is Fixed Position?

**Answer:**

Element stays fixed during scrolling.

---

### 27. What is Sticky Position?

**Answer:**

Acts relative then fixed after scroll threshold.

---

# Flexbox

### 28. What is Flexbox?

**Answer:**

One-dimensional layout system.

```css
display:flex;
```

---

### 29. Main Axis in Flexbox?

**Answer:**

Controlled by:

```css
flex-direction
```

---

### 30. How to center items using Flexbox?

**Answer:**

```css
display:flex;
justify-content:center;
align-items:center;
```

---

### 31. Difference between justify-content and align-items?

**Answer:**

| Property        | Controls   |
| --------------- | ---------- |
| justify-content | Main Axis  |
| align-items     | Cross Axis |

---

### 32. What does flex-wrap do?

**Answer:**

Allows items to move to next line.

```css
flex-wrap:wrap;
```

---

# CSS Grid

### 33. What is CSS Grid?

**Answer:**

Two-dimensional layout system.

---

### 34. Create 3 equal columns.

**Answer:**

```css
grid-template-columns:
1fr 1fr 1fr;
```

---

### 35. What does gap do?

**Answer:**

Adds spacing between grid items.

---

### 36. Difference between Flexbox and Grid?

**Answer:**

| Flexbox    | Grid           |
| ---------- | -------------- |
| 1D         | 2D             |
| Row/Column | Rows + Columns |

---

# Transform & Transition

### 37. What is Transform?

**Answer:**

Changes shape, position, rotation, scale.

---

### 38. Rotate element 45 degrees.

**Answer:**

```css
transform:rotate(45deg);
```

---

### 39. Enlarge element.

**Answer:**

```css
transform:scale(1.2);
```

---

### 40. What is Transition?

**Answer:**

Creates smooth animation between states.

---

### 41. Example of Transition.

**Answer:**

```css
button{
    transition:.3s;
}
```

---

# Animation

### 42. What is @keyframes?

**Answer:**

Defines animation steps.

```css
@keyframes move{
}
```

---

### 43. Infinite animation?

**Answer:**

```css
animation-iteration-count:infinite;
```

---

### 44. Difference between Transition and Animation?

**Answer:**

Transition:

* Needs trigger

Animation:

* Can run automatically

---

# Responsive Design

### 45. What is Responsive Design?

**Answer:**

Website adapts to different screen sizes.

---

### 46. What is a Media Query?

**Answer:**

Applies styles for specific screen sizes.

```css
@media(max-width:768px)
```

---

### 47. What is Mobile First Design?

**Answer:**

Design for mobile first, then larger screens.

---

# Variables & Modern CSS

### 48. What is a CSS Variable?

**Answer:**

Reusable CSS value.

```css
:root{
    --primary:blue;
}
```

---

### 49. Use a CSS Variable.

**Answer:**

```css
color:var(--primary);
```

---

### 50. Difference between Box Shadow and Drop Shadow?

**Answer:**

**Box Shadow**

```css
box-shadow:0 5px 10px gray;
```

Applies shadow to the whole box.

**Drop Shadow**

```css
filter:drop-shadow(0 5px 10px gray);
```

Applies shadow based on the actual shape/content.

---

# Most Important Interview Topics

If you're preparing for Frontend interviews, focus heavily on:

1. Box Model
2. Specificity
3. Position
4. Display
5. Flexbox
6. Grid
7. Responsive Design
8. Transform
9. Transition
10. Animation
11. CSS Variables
12. Pseudo Classes & Pseudo Elements
13. z-index
14. Overflow
15. Media Queries

These topics account for the majority of CSS interview questions for junior frontend roles.
