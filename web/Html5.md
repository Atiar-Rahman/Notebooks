HTML5 হলো ওয়েব পেজ তৈরির জন্য ব্যবহৃত সর্বশেষ স্ট্যান্ডার্ড মার্কআপ ভাষা। Frontend Development শেখার জন্য HTML5 ভালোভাবে জানা খুবই গুরুত্বপূর্ণ।

# HTML5 Overview

HTML = HyperText Markup Language

HTML5 এর মূল উদ্দেশ্য:

* Web page structure তৈরি করা
* Multimedia support (Audio, Video)
* Semantic elements
* Forms উন্নত করা
* Browser APIs support করা

---

# Basic HTML5 Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Website</title>
</head>
<body>

    <h1>Hello World</h1>

</body>
</html>
```

---

# HTML5 Semantic Elements

Semantic tags page-এর meaning বোঝায়।

| Tag            | Purpose             |
| -------------- | ------------------- |
| `<header>`     | Website Header      |
| `<nav>`        | Navigation Menu     |
| `<main>`       | Main Content        |
| `<section>`    | Content Section     |
| `<article>`    | Independent Content |
| `<aside>`      | Sidebar             |
| `<footer>`     | Footer              |
| `<figure>`     | Image Container     |
| `<figcaption>` | Image Caption       |

Example:

```html
<header>
    <h1>My Blog</h1>
</header>

<nav>
    <a href="#">Home</a>
    <a href="#">About</a>
</nav>

<main>
    <section>
        <article>
            <h2>Post Title</h2>
            <p>Content...</p>
        </article>
    </section>
</main>

<footer>
    Copyright 2026
</footer>
```

---

# Headings

```html
<h1>Main Heading</h1>
<h2>Sub Heading</h2>
<h3>Sub Heading</h3>
<h4>Sub Heading</h4>
<h5>Sub Heading</h5>
<h6>Sub Heading</h6>
```

---

# Text Formatting

```html
<p>Paragraph</p>

<b>Bold</b>

<strong>Important Text</strong>

<i>Italic</i>

<em>Emphasized</em>

<u>Underline</u>

<mark>Highlighted</mark>

<small>Small Text</small>

<del>Deleted</del>

<ins>Inserted</ins>

<sup>Superscript</sup>

<sub>Subscript</sub>
```

---

# Links

```html
<a href="https://google.com">Google</a>
```

New Tab:

```html
<a href="https://google.com" target="_blank">
    Open Google
</a>
```

---

# Images

```html
<img src="image.jpg" alt="Image">
```

Width:

```html
<img src="image.jpg" width="300">
```

---

# Lists

## Ordered List

```html
<ol>
    <li>Python</li>
    <li>JavaScript</li>
</ol>
```

## Unordered List

```html
<ul>
    <li>Apple</li>
    <li>Mango</li>
</ul>
```

## Description List

```html
<dl>
    <dt>HTML</dt>
    <dd>Markup Language</dd>
</dl>
```

---

# Tables

```html
<table border="1">
    <tr>
        <th>Name</th>
        <th>Age</th>
    </tr>

    <tr>
        <td>Atiar</td>
        <td>24</td>
    </tr>
</table>
```

---

# Forms

```html
<form>

    <label>Name</label>
    <input type="text">

    <br><br>

    <label>Email</label>
    <input type="email">

    <br><br>

    <button>Submit</button>

</form>
```

---

# HTML5 Input Types

```html
<input type="text">
<input type="email">
<input type="password">
<input type="number">
<input type="date">
<input type="datetime-local">
<input type="time">
<input type="month">
<input type="week">
<input type="color">
<input type="range">
<input type="search">
<input type="url">
<input type="tel">
<input type="file">
<input type="checkbox">
<input type="radio">
<input type="hidden">
<input type="submit">
<input type="reset">
```

---

# Form Validation

```html
<input type="email" required>
```

```html
<input type="text"
       minlength="3"
       maxlength="20">
```

```html
<input type="number"
       min="1"
       max="100">
```

---

# Select Dropdown

```html
<select>
    <option>Dhaka</option>
    <option>Chittagong</option>
</select>
```

---

# Textarea

```html
<textarea rows="5" cols="30">
</textarea>
```

---

# Audio

```html
<audio controls>
    <source src="song.mp3">
</audio>
```

---

# Video

```html
<video width="500" controls>
    <source src="video.mp4">
</video>
```

---

# iframe

```html
<iframe
src="https://example.com"
width="500"
height="300">
</iframe>
```

---

# HTML5 APIs

## Geolocation API

```javascript
navigator.geolocation.getCurrentPosition(
    position => {
        console.log(position.coords.latitude);
    }
);
```

---

## Local Storage

```javascript
localStorage.setItem("name", "Atiar");

let name =
localStorage.getItem("name");
```

---

## Session Storage

```javascript
sessionStorage.setItem("user", "Atiar");
```

---

# Meta Tags

```html
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0">
<meta name="description"
      content="Website Description">
<meta name="keywords"
      content="html, css, js">
```

---

# HTML Entities

```html
&lt;   <
&gt;   >
&amp;  &
&nbsp; Space
&copy; ©
```

---

# Common HTML5 Elements

```html
<div></div>
<span></span>
```

### Block Element

```html
<div>
<p>
<h1>
<section>
```

### Inline Element

```html
<span>
<a>
<strong>
<img>
```

---

# HTML5 Interview Questions

### 1. HTML5 কী?

HTML-এর latest version যা semantic tags, multimedia এবং modern web features support করে।

### 2. Semantic Tag কী?

যে tag content-এর meaning প্রকাশ করে।

Example:

```html
<header>
<nav>
<section>
<footer>
```

### 3. div এবং span এর পার্থক্য?

| div           | span            |
| ------------- | --------------- |
| Block Element | Inline Element  |
| New line নেয়  | New line নেয় না |

### 4. LocalStorage vs SessionStorage

| LocalStorage | SessionStorage           |
| ------------ | ------------------------ |
| Permanent    | Browser close হলে delete |
| 5-10 MB      | 5 MB                     |

---

# Frontend Developer Roadmap (তোমার জন্য)

1. HTML5 (100%)
2. CSS3
3. Flexbox
4. CSS Grid
5. Responsive Design
6. JavaScript ES6+
7. DOM
8. Async JS
9. React
10. Git & GitHub
11. REST API
12. TypeScript
13. Next.js

তুমি যেহেতু Frontend Development শেখার জন্য ৩ ঘণ্টার রুটিন চেয়েছিলে, HTML5-এর জন্য আমি চাইলে **৫০টি practice project + ১০০টি interview question + complete HTML5 notes PDF**-ও দিতে পারি।
