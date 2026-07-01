যদি **Tailwind CSS v4.3** Django-তে ব্যবহার করতে চাও, তাহলে **Tailwind CLI** ব্যবহার করাই সবচেয়ে সহজ এবং official উপায়। `django-tailwind` package এখনও মূলত v3 workflow-এর জন্য বেশি পরিচিত।

---

# Project Structure

```text
myproject/
│
├── static/
│   ├── src/
│   │   └── input.css
│   └── css/
│       └── output.css
│
├── templates/
├── manage.py
├── package.json
└── tailwind.config.js (optional)
```

---

# Step 1: Install Node.js

Check version:

```bash
node -v
npm -v
```

Node.js **20+** হলে ভালো।

---

# Step 2: Initialize npm

Project root-এ

```bash
npm init -y
```

---

# Step 3: Install Tailwind 4.3

```bash
npm install tailwindcss @tailwindcss/cli
```

---

# Step 4: Create CSS Source

Create

```text
static/src/input.css
```

Add

```css
@import "tailwindcss";
```

Tailwind v4-এ আর `@tailwind base`, `@tailwind components`, `@tailwind utilities` লাগে না।

---

# Step 5: Add Build Script

`package.json`

```json
{
  "scripts": {
    "dev": "tailwindcss -i ./static/src/input.css -o ./static/css/output.css --watch",
    "build": "tailwindcss -i ./static/src/input.css -o ./static/css/output.css --minify"
  }
}
```

---

# Step 6: Run Tailwind

Development

```bash
npm run dev
```

Production

```bash
npm run build
```

---

# Step 7: Configure Django Static

`settings.py`

```python
STATIC_URL = "static/"

STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

---

# Step 8: Load CSS in Template

```html
{% load static %}

<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="{% static 'css/output.css' %}">
</head>

<body>

<h1 class="text-4xl font-bold text-blue-600">
    Hello Django + Tailwind 4
</h1>

</body>
</html>
```

---

# Step 9: Start Django

Terminal 1

```bash
python manage.py runserver
```

Terminal 2

```bash
npm run dev
```

Tailwind এখন file change হলেই CSS rebuild করবে।

---

# Optional: Auto Scan Templates

Tailwind v4-এ সাধারণত আলাদা `tailwind.config.js` ছাড়াও কাজ করা যায়। যদি custom configuration দরকার হয়, তৈরি করতে পারো।

উদাহরণ:

```javascript
export default {
  content: [
    "./templates/**/*.html",
    "./**/templates/**/*.html",
    "./**/*.py",
]
}
```

---

# Final Folder Structure

```text
project/
│
├── static/
│   ├── css/
│   │   └── output.css
│   └── src/
│       └── input.css
│
├── templates/
│   └── base.html
│
├── package.json
├── manage.py
└── requirements.txt
```

---

## আমি তোমাকে **2026 সালের Django + Tailwind CSS 4.3 production-ready setup** recommend করব:

- ✅ Django 5.x
    
- ✅ Tailwind CSS 4.3
    
- ✅ Tailwind CLI (`@tailwindcss/cli`)
    
- ✅ No `django-tailwind` package
    
- ✅ Vite ব্যবহার না করলে CLI workflow
    
- ✅ HTMX (যদি dynamic UI দরকার হয়)
    

এটি বর্তমানে নতুন Django project-এর জন্য পরিষ্কার, দ্রুত এবং maintainable setup।

https://www.youtube.com/watch?v=XQECGEjOo4M

