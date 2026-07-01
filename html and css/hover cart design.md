```jsx

```


`group-hover:` হলো একটা **variant prefix** — এর পরে প্রায় যেকোনো Tailwind utility class বসানো যায়।

মানে `group-hover:underline` শুধু একটা example। `underline` এর জায়গায় অনেক কিছু use করা যায়:

### Text related

```html
group-hover:text-red-500
group-hover:underline
group-hover:font-bold
group-hover:text-xl
```

Effect:

- text color change
    
- underline
    
- font bold
    
- text size change
    

---

### Background

```html
group-hover:bg-blue-500
group-hover:bg-gray-100
```

Hover এ background change।

---

### Border / Ring

```html
group-hover:border-red-500
group-hover:ring-2
```

---

### Visibility / Display style

```html
group-hover:opacity-100
group-hover:visible
group-hover:block
group-hover:flex
```

Button show/hide এ useful।

---

### Transform / Animation

```html
group-hover:scale-110
group-hover:rotate-6
group-hover:translate-y-2
```

Image zoom বা movement।

---

### Shadow / Effects

```html
group-hover:shadow-xl
group-hover:blur-sm
```

---

Example:

```html
<div class="group">
   <img class="group-hover:scale-110 transition" />
   <p class="group-hover:text-blue-500">
      Product
   </p>
</div>
```

এখানে parent hover করলে:

- image zoom
    
- text blue
    

[Tailwind Hover States Docs](https://tailwindcss.com/docs/hover-focus-and-other-states?utm_source=chatgpt.com)

Short rule:

> `group-hover:` + **যে utility class normally লিখতে পারো**, তার বেশিরভাগই use করা যায়।  
> যেমন `bg-*`, `text-*`, `opacity-*`, `scale-*`, `flex`, `hidden`, `shadow-*` etc.