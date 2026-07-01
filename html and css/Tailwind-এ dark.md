Tailwind-এ `dark:` use করো যখন **Dark Mode** এর জন্য আলাদা style দিতে চাও।

Example:

```html id="l6xv6v"
<div class="bg-white text-black dark:bg-gray-900 dark:text-white">
  Hello
</div>
```

মানে:

* Light mode → white background + black text
* Dark mode → dark background + white text

---

### কখন use করবে?

#### 1) Full website dark mode support

যেমন:

* e-commerce
* dashboard
* admin panel

```html id="rqy7u8"
<div class="bg-gray-100 dark:bg-gray-800">
```

---

#### 2) User theme toggle (Light / Dark switch)

React এ state দিয়ে class toggle করতে পারো:

```jsx id="povfr5"
<html className="dark">
```

`dark` class থাকলে সব `dark:*` class active হবে।

---

#### 3) System theme detect

User OS dark হলে auto apply।

Tailwind config এ:

```js id="2b6uwl"
darkMode: 'media'
```

or manually:

```js id="39g8od"
darkMode: 'class'
```

---

### Example Product Card

```html id="g2ikz0"
<div class="bg-white text-black dark:bg-gray-900 dark:text-white p-4 rounded">
  Product Name
</div>
```

---

### Tailwind এ কিছু common dark variants

```html id="xqluq2"
dark:bg-black
dark:text-white
dark:border-gray-700
dark:hover:bg-gray-700
```

[Tailwind Dark Mode Docs](https://tailwindcss.com/docs/dark-mode?utm_source=chatgpt.com)

Shortly:

> `hover:` = mouse hover
> `disabled:` = disabled state
> `dark:` = dark theme active হলে style apply
