
# ✅ HTML (COMPLETE GUIDE)

## 🔹 1. HTML কী?

**HTML (HyperText Markup Language)** হলো ওয়েবপেজের **structure তৈরির ভাষা**।

👉 HTML দিয়ে:

- Text দেখানো
    
- Image, video যুক্ত করা
    
- Form বানানো
    
- Page layout তৈরি করা
    

👉 HTML programming language না, এটা **markup language**।

---

## 🔹 2. HTML File Structure (Must Know)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My Website</title>
</head>
<body>

    <h1>Hello World</h1>

</body>
</html>
```

### Explanation:

|Tag|কাজ|
|---|---|
|`<!DOCTYPE html>`|HTML5|
|`<html>`|Root element|
|`<head>`|Meta info|
|`<body>`|Visible content|

---

## 🔹 3. HTML Tags & Elements

```html
<p>This is paragraph</p>
```

- `<p>` → Opening tag
    
- `</p>` → Closing tag
    
- Whole thing = **Element**
    

### Self-closing tags

```html
<br>
<hr>
<img>
<input>
```

---

## 🔹 4. Headings (SEO Important)

```html
<h1>Main Title</h1>
<h2>Sub Title</h2>
<h3></h3>
<h4></h4>
<h5></h5>
<h6>Smallest</h6>
```

📌 Rule:  
✔️ One `<h1>` per page  
✔️ Proper hierarchy

---

## 🔹 5. Paragraph & Text Formatting

```html
<p>This is paragraph</p>

<b>Bold</b>
<strong>Important</strong>

<i>Italic</i>
<em>Emphasis</em>

<u>Underline</u>
<mark>Highlight</mark>

<small>Small text</small>
<del>Deleted</del>
<sup>2</sup>
<sub>2</sub>
```

---

## 🔹 6. Line Break & Horizontal Line

```html
Hello <br> World
<hr>
```

---

## 🔹 7. HTML Attributes

```html
<tag attribute="value">Content</tag>
```

Example:

```html
<a href="https://google.com">Google</a>
```

Common attributes:

- id
    
- class
    
- href
    
- src
    
- style
    
- title
    

---

## 🔹 8. Links (Anchor)

```html
<a href="about.html">About</a>
<a href="https://google.com" target="_blank">Google</a>
```

---

## 🔹 9. Images

```html
<img src="img.jpg" alt="Profile Photo" width="200">
```

📌 `alt` is **mandatory** (SEO + accessibility)

---

## 🔹 10. Lists

### Unordered

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
</ul>
```

### Ordered

```html
<ol>
  <li>Python</li>
  <li>Java</li>
</ol>
```

### Description List

```html
<dl>
  <dt>HTML</dt>
  <dd>Markup language</dd>
</dl>
```

---

## 🔹 11. Tables

```html
<table border="1">
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Rahim</td>
    <td>20</td>
  </tr>
</table>
```

Table tags:

- `<table>`
    
- `<tr>` row
    
- `<th>` heading
    
- `<td>` data
    

---

## 🔹 12. Forms (VERY IMPORTANT)

```html
<form>
  <label>Name:</label>
  <input type="text"><br>

  <label>Email:</label>
  <input type="email"><br>

  <label>Password:</label>
  <input type="password"><br>

  <input type="submit">
</form>
```

### Input Types

|Type|Use|
|---|---|
|text|name|
|email|email|
|password|password|
|number|age|
|date|date|
|radio|choice|
|checkbox|multiple|
|file|upload|

---

## 🔹 13. Form Attributes

```html
<form action="submit.php" method="post">
```

- `action` → where data goes
    
- `method` → GET / POST
    

---

## 🔹 14. Div & Span

```html
<div>This is block</div>
<span>This is inline</span>
```

|div|span|
|---|---|
|Block|Inline|
|Full width|Content width|

---

## 🔹 15. Semantic HTML (ADVANCED 🔥)

Semantic = meaningful tags

```html
<header></header>
<nav></nav>
<main></main>
<section></section>
<article></article>
<aside></aside>
<footer></footer>
```

📌 Benefits:

- SEO friendly
    
- Clean code
    
- Accessibility
    

---

## 🔹 16. Meta Tags

```html
<meta charset="UTF-8">
<meta name="description" content="My website">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## 🔹 17. Audio & Video

```html
<audio controls>
  <source src="song.mp3">
</audio>

<video controls width="300">
  <source src="video.mp4">
</video>
```

---

## 🔹 18. iframe

```html
<iframe src="https://example.com"></iframe>
```

---

## 🔹 19. HTML Entities

```html
&lt;   <!-- < -->
&gt;   <!-- > -->
&amp;  <!-- & -->
&nbsp; <!-- space -->
```

---

## 🔹 20. Accessibility (A11Y)

```html
<img src="img.jpg" alt="Boy playing football">

<label for="email">Email</label>
<input id="email">
```

---

## 🔹 21. HTML Best Practices

✅ Use semantic tags  
✅ Proper indentation  
✅ Alt attribute  
✅ One h1  
❌ Inline style avoid  
❌ Table layout avoid

---

## 🔹 22. HTML Interview Questions (Short)

**Q: HTML vs HTML5?**  
→ HTML5 supports audio, video, semantic tags

**Q: div vs span?**  
→ div block, span inline

**Q: GET vs POST?**  
→ GET visible, POST secure

---

## 🔹 23. Mini Projects (Practice)

✔️ Personal Profile Page  
✔️ Login / Signup Form  
✔️ Student Table  
✔️ Blog Layout  
✔️ Resume Website

---

## 🔹 24. HTML Learning Complete ✔️

Next Step Roadmap:  
1️⃣ CSS  
2️⃣ JavaScript  
3️⃣ Frontend Framework  
4️⃣ Backend (Django / Node)

---

যদি চাও, আমি দিতে পারি 👇  
✅ **HTML 50 practice problems**  
✅ **HTML real project source code**  
✅ **HTML exam questions (short + long)**  
✅ **HTML + CSS full course**

👉 বলো, পরেরটা কোনটা করবে? 💪