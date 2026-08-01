In **HTML**, **attributes** are special properties added to HTML elements that provide extra information or modify how the element behaves.

Attributes are written **inside the opening tag** and usually have the format:

```html
attribute="value"
```

### Example 1: `href` attribute

```html
<a href="https://example.com">Visit Example</a>
```

* `<a>` = anchor (link) element
* `href` = attribute
* `"https://example.com"` = attribute value

### Example 2: `src` and `alt` attributes

```html
<img src="cat.jpg" alt="A cute cat">
```

* `src` specifies the image file.
* `alt` provides alternative text if the image cannot be displayed.

### Example 3: `id` and `class` attributes

```html
<p id="intro" class="highlight">
  Welcome to HTML!
</p>
```

* `id` uniquely identifies the element.
* `class` groups elements for CSS styling or JavaScript.

### Common HTML attributes

| Attribute | Purpose                                        |
| --------- | ---------------------------------------------- |
| `id`      | Gives an element a unique identifier           |
| `class`   | Assigns one or more CSS classes                |
| `href`    | Specifies the URL of a link                    |
| `src`     | Specifies the source of an image, script, etc. |
| `alt`     | Alternative text for images                    |
| `style`   | Adds inline CSS styles                         |
| `title`   | Displays extra information as a tooltip        |
| `width`   | Sets the width of an element                   |
| `height`  | Sets the height of an element                  |

### Summary

An HTML element consists of:

* **Tag** → Defines the element (e.g., `<img>`, `<a>`, `<p>`).
* **Attribute** → Provides additional information about the element.
* **Value** → The setting assigned to the attribute.

For example:

```html
<input type="text" placeholder="Enter your name" required>
```

Here:

* `type="text"` is an attribute.
* `placeholder="Enter your name"` is an attribute.
* `required` is a **boolean attribute**, meaning it works by its presence alone and doesn't need a value like `required="required"`.

**List** means a **collection or sequence of items** written one after another.

### General examples

* A **shopping list**: milk, eggs, bread
* A **to-do list**: study, exercise, clean room

### In HTML

A **list** is used to display related items in an organized way.

There are three main types of lists:

1. **Unordered List (`<ul>`)** – displays items with bullets.

   ```html
   <ul>
     <li>Apple</li>
     <li>Banana</li>
     <li>Orange</li>
   </ul>
   ```

   Output:

   * Apple
   * Banana
   * Orange

2. **Ordered List (`<ol>`)** – displays items with numbers.

   ```html
   <ol>
     <li>Wake up</li>
     <li>Brush teeth</li>
     <li>Go to school</li>
   </ol>
   ```

   Output:

   3. Wake up
   4. Brush teeth
   5. Go to school

6. **Description List (`<dl>`)** – displays terms and their descriptions.

   ```html
   <dl>
     <dt>HTML</dt>
     <dd>A markup language for creating web pages.</dd>

     <dt>CSS</dt>
     <dd>A language used to style web pages.</dd>
   </dl>
   ```

### Simple definition

**List = A group of related items displayed together in an organized way.**



In **HTML**, a **table** is used to display data in **rows and columns**, similar to a spreadsheet.

### Basic structure

```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Alice</td>
    <td>25</td>
  </tr>
  <tr>
    <td>Bob</td>
    <td>30</td>
  </tr>
</table>
```

### Output

| Name  | Age |
| ----- | --: |
| Alice |  25 |
| Bob   |  30 |

### HTML table tags

| Tag       | Meaning      | Purpose                                              |
| --------- | ------------ | ---------------------------------------------------- |
| `<table>` | Table        | Creates the table                                    |
| `<tr>`    | Table Row    | Creates a row                                        |
| `<th>`    | Table Header | Creates a header cell (bold and centered by default) |
| `<td>`    | Table Data   | Creates a regular data cell                          |

### How it works

```html
<table>
  <tr>
    <th>Subject</th>
    <th>Marks</th>
  </tr>
  <tr>
    <td>Math</td>
    <td>90</td>
  </tr>
</table>
```

* `<table>` starts the table.
* `<tr>` creates a row.
* `<th>` creates header cells.
* `<td>` creates data cells.

### Simple definition

**Table = A way to organize and display information in rows and columns.**



`<thead>`, `<tbody>`, and `<tfoot>` are HTML elements used to **organize different sections of a table**. They don't change the appearance by themselves, but they make tables easier to read, style, and manage.

| Element   | Purpose                    | Contains                         |
| --------- | -------------------------- | -------------------------------- |
| `<thead>` | Groups the table header    | Header rows (`<tr>` with `<th>`) |
| `<tbody>` | Groups the main table data | Data rows (`<tr>` with `<td>`)   |
| `<tfoot>` | Groups the table footer    | Summary or total rows            |

### Example

```html
<table>
  <thead>
    <tr>
      <th>Product</th>
      <th>Price</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Laptop</td>
      <td>$800</td>
    </tr>
    <tr>
      <td>Mouse</td>
      <td>$20</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <td>Total</td>
      <td>$820</td>
    </tr>
  </tfoot>
</table>
```

### What each section does

#### 1. `<thead>`

* Contains the **column headings**.
* Usually uses `<th>` cells.

```html
<thead>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
</thead>
```

#### 2. `<tbody>`

* Contains the **main data** of the table.
* Usually uses `<td>` cells.

```html
<tbody>
  <tr>
    <td>Alice</td>
    <td>25</td>
  </tr>
</tbody>
```

#### 3. `<tfoot>`

* Contains **summary information**, such as totals or averages.
* Often placed at the bottom of the table.

```html
<tfoot>
  <tr>
    <td>Total</td>
    <td>100</td>
  </tr>
</tfoot>
```

### Visual layout

```
+----------------------+
|      <thead>         |
| Product | Price      |
+----------------------+
|      <tbody>         |
| Laptop  | $800       |
| Mouse   | $20        |
+----------------------+
|      <tfoot>         |
| Total   | $820       |
+----------------------+
```

### Why use them?

* Makes your HTML more **organized** and easier to understand.
* Helps with **CSS styling** (you can style headers, body, and footers separately).
* Improves **accessibility** for screen readers.
* Some browsers and printing tools can keep the table header or footer visible on each printed page for long tables.

### Summary

* **`<thead>`** → Header (column names)
* **`<tbody>`** → Main table data
* **`<tfoot>`** → Footer (totals, summaries, notes)



In **HTML**, an **anchor tag** (`<a>`) is used to create **links (hyperlinks)** that connect one page to another page, a file, an email address, or a location within the same page.

### Basic syntax

```html
<a href="URL">Link Text</a>
```

* `<a>` = anchor tag
* `href` = attribute that specifies the destination
* `Link Text` = clickable text

### Example

```html
<a href="https://www.google.com">Visit Google</a>
```

Output:
[Visit Google] (clickable link)

### Common anchor tag attributes

| Attribute  | Purpose                                | Example               |
| ---------- | -------------------------------------- | --------------------- |
| `href`     | Specifies the link destination         | `href="page.html"`    |
| `target`   | Specifies where to open the link       | `target="_blank"`     |
| `title`    | Shows extra information on hover       | `title="Go to home"`  |
| `download` | Downloads a file instead of opening it | `download="file.pdf"` |

### Opening a link in a new tab

```html
<a href="https://www.example.com" target="_blank">
  Open Example
</a>
```

* `target="_blank"` opens the link in a new browser tab.

### Linking to another page in the same website

```html
<a href="about.html">About Us</a>
```

### Creating an email link

```html
<a href="mailto:example@email.com">Send Email</a>
```

### Creating a link to a section on the same page

```html
<a href="#contact">Go to Contact</a>

<h2 id="contact">Contact Section</h2>
```

Clicking the link jumps to the element with `id="contact"`.

### Simple definition:

**Anchor tag (`<a>`) = An HTML tag used to create clickable links.**


In **HTML**, the **`<img>` tag** is used to **display images** on a web page.

### Basic syntax

```html
<img src="image.jpg" alt="Description of image">
```

- `<img>` = image tag
    
- `src` = specifies the image location (source)
    
- `alt` = alternative text shown if the image cannot load
    

### Example

```html
<img src="cat.jpg" alt="A cute cat">
```

This displays the image **cat.jpg** on the webpage.

### Common `<img>` attributes

|Attribute|Purpose|Example|
|---|---|---|
|`src`|Specifies the image path or URL|`src="photo.png"`|
|`alt`|Provides alternative text|`alt="Profile picture"`|
|`width`|Sets image width|`width="300"`|
|`height`|Sets image height|`height="200"`|
|`title`|Shows text when hovering|`title="My image"`|

### Example with size

```html
<img src="flower.jpg" alt="A flower" width="400" height="300">
```

### Using an image from a website

```html
<img src="https://example.com/image.jpg" alt="Example image">
```

### Important points

- The `<img>` tag is a **self-closing (empty) tag**, meaning it does not need a closing tag like `</img>`.
    
- It only displays the image; it does not create a copy of the image.
    
- The `alt` attribute is important for **accessibility** and when images fail to load.
    

**Simple definition:**  
**`<img>` tag = An HTML tag used to add images to a webpage.**

### Difference between HTML and XHTML

|HTML|XHTML|
|---|---|
|**HTML (HyperText Markup Language)** is used to create and structure web pages.|**XHTML (Extensible HyperText Markup Language)** is a stricter version of HTML based on XML rules.|
|HTML has more flexible syntax.|XHTML follows strict XML syntax rules.|
|Tags and attributes are not always required to be written in lowercase.|All tags and attributes **must be written in lowercase**.|
|Closing tags may sometimes be omitted in HTML.|Every opened tag **must have a closing tag**.|
|Attribute values may sometimes be written without quotes.|All attribute values **must be inside quotes**.|
|HTML allows improper nesting of elements in many cases.|XHTML requires proper nesting of elements.|
|HTML is more forgiving when errors occur.|XHTML is stricter and may not work if there are syntax errors.|

### Example of HTML (allowed)

```html
<HTML>
<BODY>
<p>Hello World
</BODY>
</HTML>
```

### Example of XHTML (correct)

```html
<html>
<body>
<p>Hello World</p>
</body>
</html>
```

### Key XHTML rules

1. All tags must be lowercase:
    

```html
<p>Hello</p>
```

2. All tags must be closed:
    

```html
<br />
<img src="image.jpg" alt="Image" />
```

3. Attributes must be quoted:
    

```html
<input type="text" name="username" />
```

### Simple summary:

- **HTML = Flexible language for creating web pages.**
    
- **XHTML = Stricter, XML-based version of HTML with more rules.**


### Difference between `id` and `class` in HTML

Both **`id`** and **`class`** are HTML attributes used to **identify and style elements**, but they are used differently.

| `id`                                                        | `class`                                                          |
| ----------------------------------------------------------- | ---------------------------------------------------------------- |
| Used to identify **one unique element** on a page.          | Used to group **multiple elements** together.                    |
| An element should have only **one unique id**.              | Multiple elements can have the same class.                       |
| In CSS, it is selected using `#`.                           | In CSS, it is selected using `.`.                                |
| Commonly used for unique elements and JavaScript targeting. | Commonly used for applying the same styles to multiple elements. |

### Example of `id`

```html id="2f7e6m"
<h1 id="title">Welcome to my website</h1>
```

CSS:

```css id="nq4qg9"
#title {
  color: blue;
}
```

Here, only the element with `id="title"` gets the style.

---

### Example of `class`

```html id="1h4s6q"
<p class="text">First paragraph</p>
<p class="text">Second paragraph</p>
```

CSS:

```css id="w6m3zg"
.text {
  color: green;
}
```

Both paragraphs with `class="text"` get the style.

---

### Using both together

```html id="h9c4z0"
<div id="header" class="box">
  Header content
</div>
```

* `id="header"` → uniquely identifies this element.
* `class="box"` → applies common styling that other elements can also use.

### Simple summary:

* **`id` = Unique name for one element.**
* **`class` = Shared name for multiple elements.**
### Difference between GET and POST (HTTP Methods)

| GET                                                    | POST                                                                           |
| ------------------------------------------------------ | ------------------------------------------------------------------------------ |
| Used to **request data** from a server.                | Used to **send data** to a server.                                             |
| Data is sent through the **URL** (query string).       | Data is sent in the **request body**.                                          |
| Data is visible in the browser address bar.            | Data is not shown in the URL.                                                  |
| Has limited data length because URLs have size limits. | Can send larger amounts of data.                                               |
| Can be bookmarked and cached.                          | Usually cannot be bookmarked or cached in the same way.                        |
| Less suitable for sensitive information.               | More suitable for sending sensitive information (but HTTPS is still required). |
| Mainly used for searching or retrieving information.   | Mainly used for submitting forms, uploading files, or creating data.           |

### GET example

HTML form:

```html id="z7yq2k"
<form method="GET">
  <input type="text" name="search">
  <button type="submit">Search</button>
</form>
```

When submitted, the URL may look like:

```
example.com/search?search=html
```

The data (`search=html`) is visible in the URL.

---

### POST example

HTML form:

```html id="s3bq8w"
<form method="POST">
  <input type="text" name="username">
  <input type="password" name="password">
  <button type="submit">Login</button>
</form>
```

The data is sent in the request body, not displayed in the URL.

---

### When to use?

**Use GET when:**

* Searching on a website
* Loading information
* Filtering or sorting data

Example:

```
Search products → GET /products?category=phone
```

**Use POST when:**

* Submitting a login form
* Creating a new account
* Sending large data
* Uploading files

Example:

```
Create account → POST /users
```

### Simple summary:

* **GET = Get data from the server.**
* **POST = Send data to the server.**
### Difference between `<strong>` and `<b>` in HTML

Both `<strong>` and `<b>` make text appear **bold**, but they have different meanings.

| `<strong>`                                                                          | `<b>`                                                        |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| Indicates that the text is **important or has strong importance**.                  | Only makes text **visually bold** without adding importance. |
| Has **semantic meaning** (helps browsers and screen readers understand importance). | Has **no special meaning**; it is only for appearance.       |
| Preferred for important content.                                                    | Used for styling or highlighting text without importance.    |

### Example of `<strong>`

```html id="g5qk1m"
<p><strong>Warning:</strong> Save your work before closing.</p>
```

The word "Warning" is important, so `<strong>` is used.

### Example of `<b>`

```html id="v8r2kq"
<p>This is a <b>bold</b> word.</p>
```

The word is only bold for visual effect.

### Visual output:

Both may look like:

**Bold text**

But their purpose is different.

### Simple summary:

* **`<strong>` = Important text (meaning + bold appearance).**
* **`<b>` = Bold text only (appearance).**

For modern HTML, use **`<strong>`** when the content is important and use **`<b>`** only when you need bold styling without extra meaning.
### Difference between `<em>` and `<i>` in HTML

Both `<em>` and `<i>` usually make text appear **italic**, but they have different meanings.

| `<em>`                                                               | `<i>`                                                                    |
| -------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Indicates **emphasis** or stressed importance in text.               | Indicates text that is visually different from normal text.              |
| Has **semantic meaning** (helps screen readers understand emphasis). | Mainly used for presentation or special text styles.                     |
| Browsers usually display it in italic style.                         | Browsers usually display it in italic style.                             |
| Preferred when you want to stress a word or phrase.                  | Used for things like foreign words, technical terms, names, or thoughts. |

### Example of `<em>`

```html
<p>I <em>really</em> like HTML.</p>
```

Meaning: The word **"really"** is emphasized.

Output:

> I *really* like HTML.

---

### Example of `<i>`

```html
<p>The word <i>bonjour</i> means hello in French.</p>
```

Meaning: "bonjour" is a foreign word, not necessarily emphasized.

Output:

> The word *bonjour* means hello in French.

---

### Simple summary:

* **`<em>` = Emphasized text (meaning + italic style).**
* **`<i>` = Italic text (mainly visual/style purpose).**

In modern HTML, use **`<em>`** when the reader should put stress on the word, and use **`<i>`** when the text is simply set apart from the surrounding content.
In CSS, the **`position`** property controls **how an element is placed on a webpage**.

There are **5 main position values**:

1. `static` (default)
2. `relative`
3. `absolute`
4. `fixed`
5. `sticky`

---

# 1. `position: static` (Default)

* This is the **default position** of every HTML element.
* The element appears in the normal document flow.
* `top`, `right`, `bottom`, and `left` **do not work**.

### Example

```html
<div class="box">Box</div>
```

```css
.box {
  position: static;
  background: lightblue;
  width: 100px;
  height: 100px;
}
```

Output:

```
+--------+
|  Box   |
+--------+
```

The element stays in its normal place.

---

# 2. `position: relative`

* The element **keeps its original space**.
* You can move it using `top`, `left`, `right`, or `bottom`.
* Other elements **do not move into its original space**.

### Example

```html
<div class="box">Box</div>
```

```css
.box {
  position: relative;
  top: 30px;
  left: 50px;

  width: 100px;
  height: 100px;
  background: orange;
}
```

Output

Original position

```
[Box]
```

After moving

```
          [Box]
```

Notice:

* The box moves.
* Its original space is still reserved.

---

# 3. `position: absolute`

* Removes the element from the normal document flow.
* Positions it relative to the **nearest positioned ancestor** (an ancestor with `position: relative`, `absolute`, `fixed`, or `sticky`).
* If there is no positioned ancestor, it is positioned relative to the page (`<body>`/viewport).

### Example

```html
<div class="parent">
    <div class="child">Box</div>
</div>
```

```css
.parent{
    position: relative;
    width:300px;
    height:200px;
    background:lightgray;
}

.child{
    position:absolute;
    top:20px;
    left:40px;

    width:100px;
    height:100px;
    background:red;
}
```

Output

```
+----------------------+
|                      |
|    [Box]             |
|                      |
+----------------------+
```

The red box is positioned relative to `.parent`.

---

# 4. `position: fixed`

* Removes the element from the normal flow.
* Positioned relative to the **browser window (viewport)**.
* It stays in the same place even when you scroll.

### Example

```html
<div class="menu">
    Menu
</div>
```

```css
.menu{
    position:fixed;
    top:0;
    right:0;

    background:black;
    color:white;
    padding:15px;
}
```

Output

```
----------------------------
|                    Menu   |
----------------------------
```

When you scroll the page:

```
↓ Scroll ↓

----------------------------
|                    Menu   |
----------------------------
```

The menu stays fixed.

Common uses:

* Navigation bar
* Chat button
* Back-to-top button

---

# 5. `position: sticky`

* Acts like `relative` until you scroll to a specified point.
* Then it behaves like `fixed`.
* Requires a value like `top: 0`.

### Example

```html
<h2 class="title">CSS Tutorial</h2>
```

```css
.title{
    position:sticky;
    top:0;

    background:yellow;
    padding:10px;
}
```

Before scrolling

```
CSS Tutorial
Content...
Content...
```

After scrolling

```
CSS Tutorial
-------------
Content...
Content...
```

The heading sticks to the top.

Common uses:

* Table headers
* Sticky navigation bars
* Section titles

---

# Position Comparison Table

| Position   | Normal Flow             | Can Move with `top`/`left`? | Relative To                 | Scroll Behavior                            |
| ---------- | ----------------------- | --------------------------- | --------------------------- | ------------------------------------------ |
| `static`   | ✅ Yes                   | ❌ No                        | Normal document flow        | Scrolls normally                           |
| `relative` | ✅ Yes                   | ✅ Yes                       | Its original position       | Scrolls normally                           |
| `absolute` | ❌ No                    | ✅ Yes                       | Nearest positioned ancestor | Scrolls with the page                      |
| `fixed`    | ❌ No                    | ✅ Yes                       | Browser viewport            | Stays fixed while scrolling                |
| `sticky`   | ✅ Yes (until it sticks) | ✅ Yes                       | Scroll container/viewport   | Sticks after reaching the specified offset |

## Quick example showing all positions

```html
<!DOCTYPE html>
<html>
<head>
<style>
body {
  height: 1500px;
  margin: 0;
}

.static {
  position: static;
  background: lightblue;
}

.relative {
  position: relative;
  left: 30px;
  background: orange;
}

.parent {
  position: relative;
  width: 300px;
  height: 150px;
  background: lightgray;
}

.absolute {
  position: absolute;
  top: 20px;
  right: 20px;
  background: red;
  color: white;
}

.fixed {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: green;
  color: white;
  padding: 10px;
}

.sticky {
  position: sticky;
  top: 0;
  background: yellow;
  padding: 10px;
}
</style>
</head>
<body>

<div class="sticky">Sticky Header</div>

<div class="static">Static Box</div>

<div class="relative">Relative Box</div>

<div class="parent">
  Parent
  <div class="absolute">Absolute Box</div>
</div>

<div class="fixed">Fixed Button</div>

</body>
</html>
```

### Easy way to remember

* **`static`** → Normal position.
* **`relative`** → Move from its original position.
* **`absolute`** → Position relative to the nearest positioned parent.
* **`fixed`** → Stay fixed on the screen while scrolling.
* **`sticky`** → Scroll normally, then stick at the specified position.
## CSS `float` কী?

`float` হলো একটি CSS property যা কোনো element-কে **বাম (`left`) বা ডান (`right`) দিকে সরিয়ে দেয়**, যাতে অন্য content (যেমন text) তার চারপাশে **wrap** করতে পারে।

আগে webpage layout তৈরির জন্য `float` অনেক ব্যবহার হতো। এখন layout-এর জন্য **Flexbox** এবং **Grid** বেশি ব্যবহার করা হয়। তবে **image-এর চারপাশে text wrap** করার জন্য `float` এখনও উপকারী।

---

# Syntax

```css
float: left;
float: right;
float: none;
```

---

# float: left

Element বাম পাশে চলে যায় এবং অন্য content তার ডান দিকে wrap হয়।

### Example

```html id="t0u9nd"
<img src="cat.jpg" class="image">

<p>
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
  Lorem ipsum dolor sit amet consectetur adipisicing elit.
</p>
```

```css id="2c6m1w"
.image {
  float: left;
  width: 150px;
  margin-right: 15px;
}
```

Output:

```text
+-------+  Lorem ipsum dolor sit amet...
| Image |  Lorem ipsum dolor sit amet...
|       |  Lorem ipsum dolor sit amet...
+-------+
```

Image বাম পাশে থাকবে এবং text ডান পাশে ঘিরে থাকবে।

---

# float: right

Element ডান পাশে চলে যায়।

```css id="4fqksm"
.image {
    float: right;
}
```

Output:

```text
Lorem ipsum dolor sit amet...

                 +-------+
                 | Image |
                 +-------+
```

---

# float: none

এটি default value।

```css id="v8fjzu"
.image{
    float:none;
}
```

Element স্বাভাবিক অবস্থায় থাকবে।

---

# float কিভাবে কাজ করে?

ধরুন,

```html id="p7ww8m"
<div class="box"></div>

<p>
  This is a paragraph.
</p>
```

```css id="7f5kq4"
.box{
    float:left;
}
```

তখন

```text
+-----+ This is a paragraph...
| Box |
+-----+
```

Text box-এর চারপাশে চলে আসে।

---

# Problem with float

ধরুন

```html id="a1jpyu"
<div class="parent">
    <div class="box"></div>
</div>
```

```css id="5q0l9i"
.box{
    float:left;
    width:100px;
    height:100px;
}
```

এখন parent-এর height অনেক সময় **collapse** হয়ে যায়, কারণ floated element স্বাভাবিক document flow-এর বাইরে চলে যায়।

---

# Solution: clear

```css id="93kgpz"
.clear{
    clear:both;
}
```

Example

```html id="9ts6bq"
<div class="parent">

    <div class="box"></div>

    <div class="clear"></div>

</div>
```

---

# Better Solution: clearfix

```css id="m0ut3p"
.parent::after{
    content:"";
    display:block;
    clear:both;
}
```

এতে parent আবার floated children-এর height ধরতে পারে।

---

# float vs Flexbox

### Float

```css id="7zgvq0"
.box{
    float:left;
}
```

* Image wrapping-এর জন্য ভালো।
* পুরোনো layout technique।
* Responsive layout তৈরি করা কঠিন।

### Flexbox

```css id="cmcgnw"
.parent{
    display:flex;
}
```

* Modern layout।
* Responsive।
* সহজে alignment করা যায়।

আজকাল layout-এর জন্য **Flexbox** এবং **Grid** ব্যবহার করা হয়।

---

# float Values

| Value          | কাজ                                            |
| -------------- | ---------------------------------------------- |
| `left`         | Element বাম দিকে যায়                          |
| `right`        | Element ডান দিকে যায়                          |
| `none`         | Float বন্ধ (default)                           |
| `inline-start` | লেখার শুরুর দিকে float (writing mode অনুযায়ী) |
| `inline-end`   | লেখার শেষের দিকে float (writing mode অনুযায়ী) |

---

# Interview Answer

**What is float in CSS?**

> **`float`** is a CSS property that moves an element to the **left** or **right** of its container, allowing surrounding content like text to wrap around it. It was commonly used for page layouts in the past, but today **Flexbox** and **CSS Grid** are preferred for layouts, while `float` is mainly used for wrapping text around images.

### মনে রাখার সহজ নিয়ম

* **`float: left`** → Element বামে, text ডানে wrap হবে।
* **`float: right`** → Element ডানে, text বামে wrap হবে।
* **`float`** মূলত **text wrapping**-এর জন্য।
* **Layout** বানানোর জন্য **Flexbox** বা **Grid** ব্যবহার করুন।
