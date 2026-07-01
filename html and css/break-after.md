`break-after` হলো CSS property যেটা **element-এর পরে page / column / region break হবে কিনা** control করে।

সহজভাবে:

> “এই element শেষ হওয়ার পর নতুন page/column শুরু হবে কি?”

এটা বেশি use হয়:

* Printing / PDF
* Multi-column layout
* Magazine style layout

---

### Pure CSS

```css id="6qzyvb"
.chapter {
  break-after: page;
}
```

মানে:

এই element শেষ হলে **new page** শুরু হবে।

---

### Common values

#### `break-after: auto`

Default behavior

```css id="jts30p"
break-after: auto;
```

Browser নিজে decide করবে।

---

#### `break-after: page`

Next page এ যাবে

```css id="8pp70y"
break-after: page;
```

Example:

```html id="5zz57g"
<h1>Chapter 1</h1>
```

Chapter 1 শেষ → Chapter 2 new page

---

#### `break-after: column`

Next column এ যাবে

```css id="xryrrd"
break-after: column;
```

Useful in newspaper layout।

---

#### `break-after: avoid`

Break avoid করবে

```css id="suk9y9"
break-after: avoid;
```

যেখানে page break চাই না।

---

### Tailwind CSS

[Tailwind Break After Docs](https://tailwindcss.com/docs/break-after?utm_source=chatgpt.com)

Classes:

```html id="udx4h5"
break-after-auto
break-after-avoid
break-after-page
break-after-column
```

Example:

```html id="1k0dlh"
<div class="break-after-page">
   Chapter 1
</div>
```

---

### Ecommerce project এ লাগে?

সাধারণ UI-তে **প্রায় লাগে না**।

Mostly use হয়:

* invoice print
* report export
* PDF generation

Example invoice:

```html id="6h9m9e"
<section class="break-after-page">
   Order Summary
</section>
```

Next section new page।

---

Tailwind-এর `break-*` family তিনটা:

* `break-before`
* `break-inside`
* `break-after`

Difference:

* `before` → element-এর আগে break
* `inside` → element-এর ভিতরে break allow?
* `after` → element-এর পরে break

এক লাইনে:

**`break-after` = current element শেষ হওয়ার পর layout break control করা।**
