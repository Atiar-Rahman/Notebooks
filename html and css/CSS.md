
## **1️⃣ What is CSS?**

CSS is a style sheet language used to describe how HTML elements are displayed on the screen, paper, or other media.

* **HTML** = structure/content
* **CSS** = presentation/style
* **JavaScript** = behavior

**Example:**

```html
<p>Hello World!</p>

<style>
  p {
    color: blue;
    font-size: 18px;
  }
</style>
```

This makes the text blue and increases its size.

---

## **2️⃣ Ways to use CSS**

1. **Inline CSS** – inside an HTML element using `style` attribute

```html
<p style="color:red;">Hello</p>
```

2. **Internal CSS** – inside `<style>` tag in HTML `<head>`

```html
<head>
  <style>
    p { color: green; }
  </style>
</head>
```

3. **External CSS** – separate `.css` file linked to HTML

```html
<link rel="stylesheet" href="style.css">
```

```css
/* style.css */
p { color: purple; }
```

✅ Best practice: Use external CSS for maintainability.

---

## **3️⃣ CSS Syntax**

```css
selector {
  property: value;
}
```

* **Selector** → selects HTML element(s)
* **Property** → CSS feature to change
* **Value** → desired value for the property

**Example:**

```css
h1 {
  text-align: center;
  color: orange;
}
```

---

## **4️⃣ Selectors (Most Common for Daily Use)**

| Type           | Example         | Description                           |
| -------------- | --------------- | ------------------------------------- |
| Element        | `p`             | Targets all `<p>` tags                |
| Class          | `.btn`          | Targets elements with `class="btn"`   |
| ID             | `#header`       | Targets element with `id="header"`    |
| Group          | `h1, h2`        | Apply same style to multiple elements |
| Descendant     | `div p`         | Selects `<p>` inside `<div>`          |
| Child          | `div > p`       | Selects direct `<p>` child of `<div>` |
| Pseudo-class   | `a:hover`       | Style when mouse hovers on `<a>`      |
| Pseudo-element | `p::first-line` | Style first line of `<p>`             |

---

## **5️⃣ Common Properties**

### **Text & Font**

```css
p {
  color: #333;      /* text color */
  font-size: 16px;  /* size */
  font-family: Arial, sans-serif;  /* font */
  font-weight: bold; /* bold */
  text-align: center;
  text-decoration: underline; /* underline, none */
}
```

### **Background**

```css
div {
  background-color: lightblue;
  background-image: url('img.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
```

### **Box Model**

Every element is a rectangular box: **Content → Padding → Border → Margin**

```css
div {
  width: 200px;
  height: 100px;
  padding: 10px;
  border: 2px solid black;
  margin: 20px;
}
```

### **Display & Position**

```css
span {
  display: inline; /* inline, block, inline-block, none */
}

div {
  position: relative; /* relative, absolute, fixed, sticky */
  top: 10px;
  left: 20px;
}
```

### **Flexbox (Daily Layout Tool)**

```css
.container {
  display: flex;
  justify-content: space-between; /* left, center, right, space-between */
  align-items: center; /* top, center, bottom */
}
```

### **Grid (Advanced Layout)**

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 columns of equal width */
  gap: 10px;
}
```

---

## **6️⃣ CSS Units**

* **px** – pixels (fixed size)
* **em / rem** – relative to font size
* **%** – relative to parent element
* **vh / vw** – viewport height/width

---

## **7️⃣ Colors**

* Named: `red`, `blue`
* Hex: `#ff0000`
* RGB: `rgb(255,0,0)`
* RGBA: `rgba(255,0,0,0.5)` (with transparency)
* HSL: `hsl(0, 100%, 50%)`

---

## **8️⃣ CSS Specificity & Cascade**

* Inline > ID > Class > Element

```html
<p id="text" class="big" style="color: red;">Hello</p>
```

* Style applied: **red** (inline has highest priority)

---

## **9️⃣ CSS Meta Tags for `<head>`**

* Character set:

```html
<meta charset="UTF-8">
```

* Responsive design:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

* SEO & description:

```html
<meta name="description" content="My website description">
```

* Author & keywords:

```html
<meta name="author" content="Md. Atiar Rahman">
<meta name="keywords" content="HTML, CSS, Web Development">
```

---

## **10️⃣ Modern Tools & Features**

* **CSS Variables**:

```css
:root {
  --main-color: #3498db;
}
p { color: var(--main-color); }
```

* **Transitions & Animations**:

```css
button {
  transition: background 0.3s;
}
button:hover {
  background: green;
}
```

* **Media Queries (Responsive CSS)**:

```css
@media (max-width: 600px) {
  body { font-size: 14px; }
}
```

---

💡 **Tip for Daily Use:**
Focus on:

* Layout: `flex`, `grid`
* Typography: `font-size`, `font-family`, `color`
* Spacing: `margin`, `padding`
* Backgrounds & borders
* Hover/focus effects for buttons and links

---


Absolutely! Let’s dive deep into **CSS Flexbox** — one of the most powerful tools for layouts in modern web design. I’ll explain it clearly with examples so you can use it daily.

---

## **1️⃣ What is Flexbox?**

Flexbox (**Flexible Box**) is a layout module that makes it easier to design flexible and responsive layout structures without using floats or positioning.

* It works **in one direction** at a time: **row** (horizontal) or **column** (vertical).
* Parent container: `display: flex;`
* Children: automatically become **flex items**.

---

## **2️⃣ Basic Structure**

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex; /* Makes it a flex container */
  flex-direction: row; /* default: horizontal */
}

.item {
  background-color: lightblue;
  margin: 5px;
  padding: 20px;
  text-align: center;
}
```

✅ Result: 3 boxes in a row.

---

## **3️⃣ Flex Container Properties**

| Property          | Values      | Description |               |                                  |                    |                                 |                                  |
| ----------------- | ----------- | ----------- | ------------- | -------------------------------- | ------------------ | ------------------------------- | -------------------------------- |
| `flex-direction`  | `row        | row-reverse | column        | column-reverse`                  | Direction of items |                                 |                                  |
| `justify-content` | `flex-start | flex-end    | center        | space-between                    | space-around       | space-evenly`                   | Horizontal alignment (main axis) |
| `align-items`     | `flex-start | flex-end    | center        | baseline                         | stretch`           | Vertical alignment (cross axis) |                                  |
| `align-content`   | `flex-start | flex-end    | center        | space-between                    | space-around       | stretch`                        | Multi-line alignment             |
| `flex-wrap`       | `nowrap     | wrap        | wrap-reverse` | Allow items to wrap to next line |                    |                                 |                                  |

---

### **3a. Flex Direction**

```css
.container {
  flex-direction: column; /* items stacked vertically */
}
```

### **3b. Justify Content (Main axis)**

```css
.container {
  justify-content: space-between; /* space between items */
}
```

* `flex-start` → items at start
* `flex-end` → items at end
* `center` → items centered
* `space-between` → even space, edges touch container
* `space-around` → equal space around each item
* `space-evenly` → equal space between all items including edges

### **3c. Align Items (Cross axis)**

```css
.container {
  align-items: center; /* vertical center in a row */
}
```

* `flex-start` → top
* `flex-end` → bottom
* `center` → center
* `baseline` → align text baselines
* `stretch` → stretch items to container height (default)

### **3d. Flex Wrap**

```css
.container {
  flex-wrap: wrap; /* items move to next line if no space */
}
```

* `nowrap` → default, single line
* `wrap` → multiple lines
* `wrap-reverse` → multiple lines in reverse order

---

## **4️⃣ Flex Item Properties**

| Property      | Description                                            |
| ------------- | ------------------------------------------------------ |
| `flex`        | shorthand for `flex-grow`, `flex-shrink`, `flex-basis` |
| `flex-grow`   | how much an item grows relative to others              |
| `flex-shrink` | how much an item shrinks relative to others            |
| `flex-basis`  | default size of item before growing/shrinking          |
| `align-self`  | override `align-items` for individual item             |

**Example:**

```css
.item {
  flex: 1; /* items grow equally to fill container */
}

.item:nth-child(2) {
  flex: 2; /* second item takes double space */
}

.item:nth-child(3) {
  align-self: flex-end; /* only this item aligned at bottom */
}
```

---

## **5️⃣ Complete Example**

```html
<div class="container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
</div>
```

```css
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: space-around;
  align-items: center;
  height: 200px;
  border: 2px solid black;
}

.item {
  background-color: lightcoral;
  color: white;
  flex: 1;        /* grows equally */
  margin: 5px;
  text-align: center;
  padding: 20px;
}
```

✅ Result:

* 3 items, equal width
* Space evenly around
* Vertical center alignment
* Wraps if window is narrow

---

💡 **Tips for Daily Use:**

1. Use Flexbox for **navigation bars**, **cards layout**, **button groups**.
2. `flex: 1` is perfect for auto-sizing items.
3. Combine with **media queries** for responsive design.
4. Use `align-self` to override one item’s alignment if needed.

---
