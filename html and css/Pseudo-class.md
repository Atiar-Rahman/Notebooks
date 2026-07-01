Pseudo-class (CSS) হলো element-এর **special state** target করার উপায়—মানে HTML change না করেই element-এর নির্দিষ্ট অবস্থায় style apply করা।

Syntax:

```css
selector:pseudo-class {
   /* styles */
}
```

বা Tailwind-এ:

```html id="4k2qgp"
hover:bg-blue-500
```

Common pseudo-class গুলো:

---

### Hover (`:hover`)

Mouse element-এর উপর গেলে।

```css id="2s51cx"
button:hover {
   background: red;
}
```

Use:

* button color change
* card animation
* dropdown show

---

### Active (`:active`)

Click করার মুহূর্তে।

```css id="k03nlr"
button:active {
   transform: scale(0.95);
}
```

Use:

* pressed effect

---

### Focus (`:focus`)

Input/button keyboard/tab বা click এ selected হলে।

```css id="hlkfrc"
input:focus {
   border: 2px solid blue;
}
```

Use:

* form UI
* accessibility

---

### Disabled (`:disabled`)

Disabled form element।

```css id="kk9qxu"
button:disabled {
   opacity: 0.5;
}
```

Use:

* unavailable action

---

### Checked (`:checked`)

Checkbox / radio selected।

```css id="xvjlwm"
input:checked {
   accent-color: green;
}
```

Use:

* toggle switch
* custom checkbox

---

### First Child (`:first-child`)

Parent-এর first child select করে।

```css id="kr43jl"
li:first-child {
   color: red;
}
```

Use:

* first item highlight

---

### Last Child (`:last-child`)

শেষ child।

```css id="wgcb2e"
li:last-child {
   border: none;
}
```

---

### Nth Child (`:nth-child()`)

Specific position।

```css id="n8k6zy"
li:nth-child(2) {
   color: blue;
}
```

Use:

* even/odd rows
* zebra table

---

### Not (`:not()`)

কিছু exclude করতে।

```css id="b6r8f6"
button:not(.primary) {
   opacity: 0.7;
}
```

---

### Empty (`:empty`)

যে element-এর ভিতরে content নেই।

```css id="s5df7z"
div:empty {
   display: none;
}
```

---

### Tailwind equivalents

[Tailwind Pseudo-class Variants](https://tailwindcss.com/docs/hover-focus-and-other-states?utm_source=chatgpt.com)

| CSS               | Tailwind    |
| ----------------- | ----------- |
| `:hover`          | `hover:`    |
| `:focus`          | `focus:`    |
| `:active`         | `active:`   |
| `:disabled`       | `disabled:` |
| `:checked`        | `checked:`  |
| `:first-child`    | `first:`    |
| `:last-child`     | `last:`     |
| `:nth-child(odd)` | `odd:`      |

এক লাইনে:

**Pseudo-class = “element এখন কোন state-এ আছে?” সেটা detect করে style apply করা।**
