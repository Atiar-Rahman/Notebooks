- overflow
- text-overflow:ellipises
- ## CSS3 Features (Overview)

**CSS3** introduced many modern styling capabilities that made web design more flexible and powerful. Some key features include:

### 1. Selectors & Pseudo-classes

CSS3 added advanced selectors:

* `:nth-child()`
* `:not()`
* `:first-of-type`, `:last-of-type`

### 2. Rounded Corners

```css
box {
  border-radius: 10px;
}
```

### 3. Shadows

```css
box {
  box-shadow: 2px 2px 10px rgba(0,0,0,0.3);
}
```

### 4. Gradients

```css
background: linear-gradient(to right, red, blue);
```

### 5. Transitions

```css
button {
  transition: all 0.3s ease;
}
```

### 6. Transforms

```css
div {
  transform: rotate(45deg);
}
```

### 7. Animations

```css
@keyframes slide {
  from { left: 0; }
  to { left: 100px; }
}
```

---

## CSS Overflow

The **overflow property** controls what happens when content is too large for its container.

### Syntax

```css
overflow: visible | hidden | scroll | auto;
```

### Values

* **visible (default):** Content spills outside box
* **hidden:** Extra content is clipped
* **scroll:** Scrollbars always appear
* **auto:** Scrollbars appear only when needed

### Example

```css
.box {
  width: 200px;
  height: 100px;
  overflow: auto;
}
```

---

## CSS Text Overflow

The **text-overflow property** handles how hidden text is displayed when it overflows a container.

⚠️ Important: It works only when:

* `white-space: nowrap;`
* `overflow: hidden;`

---

## Ellipsis (…) Effect

The most common use of `text-overflow` is showing `...` when text is too long.

### Syntax

```css
text-overflow: clip | ellipsis;
```

---

## Example: CSS Ellipsis with Overflow

### HTML

```html
<div class="box">
  This is a very long text that will not fit inside the container.
</div>
```

### CSS

```css
.box {
  width: 200px;
  border: 1px solid black;

  white-space: nowrap;      /* Prevent line break */
  overflow: hidden;         /* Hide extra text */
  text-overflow: ellipsis;  /* Show ... */
}
```

### Output Behavior

* Text stays on one line
* Extra content is hidden
* Shows:

```
This is a very long text that will...
```

---

## Summary

* **CSS3** adds modern design features like transitions, animations, gradients.
* **overflow** controls content outside a box.
* **text-overflow: ellipsis** shows “...” when text is too long.
* Must combine with `white-space: nowrap` + `overflow: hidden`.

---

If you want, I can also show:

* Real website UI examples
* Interview questions on CSS overflow
* Differences between `overflow: auto` vs `scroll` with visuals

-----
## CSS Transform: Rotate, Scale, Translate

The CSS **`transform`** property lets you change the shape, size, and position of an element without affecting the normal document flow.

It is commonly used for animations, UI effects, and interactive design.

---

# 1. Rotate

### What it does:

Rotates an element clockwise or counterclockwise.

### Syntax:

```css
transform: rotate(angle);
```

### Example:

```css
.box {
  transform: rotate(45deg);
}
```

### Result:

* The element rotates **45 degrees clockwise**

---

# 2. Scale

### What it does:

Increases or decreases the size of an element.

### Syntax:

```css
transform: scale(x, y);
```

* `x` → horizontal scaling
* `y` → vertical scaling

### Example 1 (uniform scaling):

```css
.box {
  transform: scale(1.5);
}
```

➡️ Increases size by 1.5 times

### Example 2 (different width & height):

```css
.box {
  transform: scale(2, 0.5);
}
```

➡️ Width becomes 2x, height becomes half

---

# 3. Translate

### What it does:

Moves an element from its original position.

### Syntax:

```css
transform: translate(x, y);
```

* `x` → horizontal movement
* `y` → vertical movement

### Example:

```css
.box {
  transform: translate(50px, 20px);
}
```

### Result:

* Moves **50px right**
* Moves **20px down**

---

# 4. Combining Transformations

You can apply multiple effects together.

### Example:

```css
.box {
  transform: rotate(30deg) scale(1.2) translate(40px, 10px);
}
```

### Order matters:

CSS applies transforms **from right to left**.

---

# 5. Hover Effect Example (Real Use)

```css
.box {
  width: 100px;
  height: 100px;
  background: blue;
  transition: 0.3s;
}

.box:hover {
  transform: scale(1.2) rotate(10deg);
}
```

### Effect:

* When mouse hovers:

  * Box grows slightly
  * Rotates a bit

---

# Summary

| Function    | Purpose        |
| ----------- | -------------- |
| rotate()    | Spins element  |
| scale()     | Changes size   |
| translate() | Moves position |

---

If you want, I can also explain:

* `skew()` transform
* 3D transforms (`rotateX`, `rotateY`)
* Real animation projects using transform + transition


--------------


https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform

