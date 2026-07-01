`aspect-ratio` CSS property দিয়ে element-এর **width : height ratio fixed** রাখা হয়।

সহজভাবে:

> Width change হলেও height automatically ratio maintain করবে।

Example:

`1:1` → square
`16:9` → video
`4:3` → old monitor

---

### Pure CSS

```css id="xw80ae"
.box {
  aspect-ratio: 1 / 1;
  width: 300px;
}
```

Result:

* width = 300px
* height = 300px

আরেকটা:

```css id="b0z4cr"
.video {
  aspect-ratio: 16 / 9;
  width: 500px;
}
```

Height auto হবে:

```text
500 × 9 / 16 = 281.25px
```

---

### Tailwind এ

[Tailwind Aspect Ratio Docs](https://tailwindcss.com/docs/aspect-ratio?utm_source=chatgpt.com)

```html id="6yr7gc"
<div class="aspect-square"></div>
```

Equivalent:

```css id="n6s6y1"
aspect-ratio: 1 / 1;
```

Common classes:

```html id="l95m0m"
aspect-square   → 1/1
aspect-video    → 16/9
```

Custom ratio:

```html id="lrkftn"
<div class="aspect-[4/3]"></div>
```

---

### Ecommerce project এ কোথায় useful?

#### Product Image same size রাখতে

Different image dimensions:

* Shoe → tall
* Laptop → wide
* Watch → square

Problem: card layout uneven।

Solution:

```html id="qmq6k0"
<div class="aspect-square overflow-hidden">
   <img class="w-full h-full object-cover" src="..." />
</div>
```

সব image square দেখাবে।

---

### `object-cover` সাথে use কেন?

```html id="vhp49j"
<img class="w-full h-full object-cover" />
```

* `aspect-ratio` container shape fix করে
* `object-cover` image crop/fit করে

Without `object-cover`, image stretch হতে পারে।

---

### Example Product Card

```html id="ulklit"
<div class="w-72 rounded-lg shadow">
  <div class="aspect-square">
    <img
      src="product.jpg"
      class="w-full h-full object-cover"
    />
  </div>
</div>
```

---

### কখন use করবে?

✅ Product cards
✅ YouTube/video embed
✅ Gallery grid
✅ Banner
✅ Avatar

Use না করলেও হয় যখন height manually fixed:

```html id="e9w0nk"
h-64
```

Difference:

* `h-64` → fixed height
* `aspect-ratio` → proportional height

এক লাইনে:

**aspect-ratio = width বদলালেও element-এর shape (ratio) same রাখা।**
