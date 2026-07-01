Django-তে **templates** add করার জন্য নিচের ধাপগুলো অনুসরণ করো।

---

# Step 1: Templates Folder তৈরি করো

Project root-এ একটি `templates` folder তৈরি করো।

```text
myproject/
│
├── manage.py
├── myproject/
│   ├── settings.py
│   └── urls.py
│
├── templates/
│   ├── base.html
│   ├── home.html
│   └── includes/
│       ├── navbar.html
│       └── footer.html
│
└── app/
```

---

# Step 2: `settings.py` Configure করো

`settings.py`

```python
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",

        "DIRS": [
            BASE_DIR / "templates",
        ],

        "APP_DIRS": True,

        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]
```

👉 **`DIRS`-এ `BASE_DIR / "templates"` যোগ করাই সবচেয়ে গুরুত্বপূর্ণ।**

---

# Step 3: Template তৈরি করো

`templates/home.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Home</title>
</head>
<body>

<h1>Hello Django</h1>

</body>
</html>
```

---

# Step 4: View তৈরি করো

```python
from django.shortcuts import render

def home(request):
    return render(request, "home.html")
```

---

# Step 5: URL Add করো

```python
from django.urls import path
from .views import home

urlpatterns = [
    path("", home, name="home"),
]
```

এখন browser-এ

```text
http://127.0.0.1:8000/
```

open করলে `home.html` দেখাবে।

---

# App-এর ভিতরে Template রাখার নিয়ম (Recommended)

বড় project-এ এই structure ব্যবহার করা হয়।

```text
project/
│
├── products/
│   ├── templates/
│   │   └── products/
│   │       ├── list.html
│   │       └── detail.html
│   └── views.py
│
├── users/
│   ├── templates/
│   │   └── users/
│   │       └── profile.html
│   └── views.py
```

View

```python
return render(request, "products/list.html")
```

এভাবে template name conflict হয় না।

---

# Base Template ব্যবহার

`templates/base.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Site{% endblock %}</title>
</head>
<body>

{% include "includes/navbar.html" %}

{% block content %}
{% endblock %}

</body>
</html>
```

`templates/home.html`

```html
{% extends "base.html" %}

{% block title %}
Home
{% endblock %}

{% block content %}
<h1>Welcome Home</h1>
{% endblock %}
```

---

# Final Project Structure (Professional)

```text
project/
│
├── manage.py
├── myproject/
│
├── templates/
│   ├── base.html
│   └── includes/
│       ├── navbar.html
│       └── footer.html
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── products/
│   ├── templates/
│   │   └── products/
│   │       ├── list.html
│   │       └── detail.html
│   └── views.py
│
└── users/
    ├── templates/
    │   └── users/
    │       └── profile.html
    └── views.py
```

###### আমি একটি **Django 5 + Tailwind CSS 4.3**-এর complete project structure (templates, static, partials, layouts, includes, app-wise templates) দেখাতে পারি, যা production-level project-এ ব্যবহার করা হয়।

---------

হ্যাঁ, **base template project root-এর `templates/` folder-এ রাখাই best practice**। বিশেষ করে বড় project-এর জন্য।

## Recommended Structure

```text
project/
│
├── manage.py
├── project/
│   ├── settings.py
│   └── urls.py
│
├── templates/
│   ├── base.html          ✅ Root Base Template
│   ├── dashboard_base.html
│   ├── auth_base.html
│   └── includes/
│       ├── navbar.html
│       ├── sidebar.html
│       ├── footer.html
│       └── messages.html
│
├── static/
│
├── apps/
│   ├── products/
│   │   └── templates/
│   │       └── products/
│   │           ├── list.html
│   │           └── detail.html
│   │
│   ├── users/
│   │   └── templates/
│   │       └── users/
│   │           └── profile.html
│   │
│   └── orders/
│       └── templates/
│           └── orders/
│               └── checkout.html
```

---

## `base.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Website{% endblock %}</title>
</head>
<body>

    {% include "includes/navbar.html" %}

    {% block content %}
    {% endblock %}

    {% include "includes/footer.html" %}

</body>
</html>
```

---

## App Template

`products/templates/products/list.html`

```html
{% extends "base.html" %}

{% block title %}
Products
{% endblock %}

{% block content %}
<h1>Product List</h1>
{% endblock %}
```

---

## কখন একাধিক Base Template রাখবেন?

বড় project-এ প্রায়ই একাধিক base template থাকে।

```text
templates/
│
├── base.html            # Main website
├── dashboard_base.html  # Admin/User Dashboard
├── auth_base.html       # Login/Register
└── email_base.html      # Email templates
```

উদাহরণ:

```html
{% extends "dashboard_base.html" %}
```

---

## আমি বড় Project-এ যেভাবে করি

```text
templates/
│
├── base.html
├── layouts/
│   ├── dashboard.html
│   ├── admin.html
│   └── auth.html
│
├── includes/
│   ├── navbar.html
│   ├── sidebar.html
│   ├── footer.html
│   ├── breadcrumb.html
│   └── pagination.html
```

এখানে:

- `base.html` → সবচেয়ে common layout
    
- `layouts/` → বিভিন্ন section-এর base template
    
- `includes/` → reusable partial templates
    

এটি maintain করা সহজ এবং বড় project-এর জন্য খুবই scalable।

**তুমি যেহেতু Job Portal / E-commerce-এর মতো বড় project বানাতে চাচ্ছো, আমি app-wise template organization + root `base.html` + reusable `includes/` pattern-টাই recommend করব।**

------------
