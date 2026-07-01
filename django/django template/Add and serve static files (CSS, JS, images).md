
Django-তে **Static Files** বলতে CSS, JavaScript, Images, Fonts ইত্যাদি বোঝায়। এগুলো সঠিকভাবে configure করা খুবই গুরুত্বপূর্ণ।

---

# 1. Static Folder Structure

ছোট Project

```text
project/
│
├── static/
│   ├── css/
│   │   └── style.css
│   │
│   ├── js/
│   │   └── app.js
│   │
│   └── images/
│       └── logo.png
│
├── templates/
├── manage.py
└── settings.py
```

---

## বড় Project (Recommended)

```text
project/
│
├── static/
│   ├── css/
│   ├── js/
│   ├── images/
│   ├── fonts/
│   └── vendor/
│
├── products/
│   └── static/
│       └── products/
│           ├── css/
│           ├── js/
│           └── images/
│
├── users/
│   └── static/
│       └── users/
│           └── profile.css
```

প্রতিটি app নিজের static file রাখতে পারে।

---

# 2. Configure `settings.py`

```python
STATIC_URL = "static/"
```

যদি project-level static folder থাকে

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

Production-এর জন্য

```python
STATIC_ROOT = BASE_DIR / "staticfiles"
```

### Summary

```python
STATIC_URL = "static/"

STATICFILES_DIRS = [
    BASE_DIR / "static",
]

STATIC_ROOT = BASE_DIR / "staticfiles"
```

---

# 3. Load Static in Template

প্রতিটি template-এর শুরুতে

```html
{% load static %}
```

---

# CSS

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

# JavaScript

```html
<script src="{% static 'js/app.js' %}"></script>
```

---

# Image

```html
<img src="{% static 'images/logo.png' %}" alt="Logo">
```

---

# Tailwind Output

```html
<link rel="stylesheet" href="{% static 'css/output.css' %}">
```

---

# 4. Example

### base.html

```html
{% load static %}

<!DOCTYPE html>
<html>

<head>

    <link rel="stylesheet" href="{% static 'css/output.css' %}">

</head>

<body>

<h1>Hello Django</h1>

<img src="{% static 'images/logo.png' %}">

<script src="{% static 'js/app.js' %}"></script>

</body>

</html>
```

---

# 5. App Static Files

```
products/
    static/
        products/
            css/
                product.css
```

Template

```html
{% load static %}

<link rel="stylesheet" href="{% static 'products/css/product.css' %}">
```

**কেন `products/` যোগ করা হয়?**

যদি দুইটি app-এ `style.css` থাকে:

```
products/static/products/css/style.css
users/static/users/css/style.css
```

তাহলে conflict হবে না।

---

# 6. Development Server

```
python manage.py runserver
```

Development mode-এ Django নিজেই static files serve করে (`DEBUG=True` হলে)।

---

# 7. Production

Production-এ

```bash
python manage.py collectstatic
```

চালালে সব static file `STATIC_ROOT`-এ কপি হবে।

```
static/
      │
      ▼
collectstatic
      │
      ▼
staticfiles/
```

এরপর সাধারণত **Nginx** বা **Apache** `staticfiles/` folder serve করে।

---

# 8. Common Mistakes

❌ `load static` লিখতে ভুলে যাওয়া

```html
{% load static %}
```

---

❌ `STATICFILES_DIRS` configure না করা

```python
STATICFILES_DIRS = [
    BASE_DIR / "static",
]
```

---

❌ Hardcode path ব্যবহার করা

```html
<!-- ভুল -->
<link rel="stylesheet" href="/static/css/style.css">
```

✔️

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

# Best Practice (Django + Tailwind)

```
project/
│
├── static/
│   ├── css/
│   │   ├── output.css
│   │   └── custom.css
│   │
│   ├── js/
│   │   └── app.js
│   │
│   └── images/
│
├── templates/
│   ├── base.html
│   └── includes/
│
├── products/
│   └── static/
│       └── products/
│
└── users/
    └── static/
        └── users/
```

এই structure-টি Django-এর documentation এবং production project—দুই ক্ষেত্রেই বহুল ব্যবহৃত।