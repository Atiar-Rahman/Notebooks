**Template Inheritance** হলো Django Template-এর সবচেয়ে গুরুত্বপূর্ণ feature। এর মাধ্যমে একটি **base template** তৈরি করে অন্য template-গুলো সেই layout reuse করতে পারে।

এতে একই HTML (navbar, footer, CSS, JS) বারবার লিখতে হয় না।

---

# Without Template Inheritance ❌

`home.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>Home</title>
</head>
<body>

<nav>Navbar</nav>

<h1>Home</h1>

<footer>Footer</footer>

</body>
</html>
```

`about.html`

```html
<!DOCTYPE html>
<html>
<head>
    <title>About</title>
</head>
<body>

<nav>Navbar</nav>

<h1>About</h1>

<footer>Footer</footer>

</body>
</html>
```

👉 এখানে Navbar এবং Footer বারবার লিখতে হচ্ছে।

---

# With Template Inheritance ✅

## Project Structure

```text
templates/
│
├── base.html
├── home.html
├── about.html
└── includes/
    ├── navbar.html
    └── footer.html
```

---

## base.html

```html
{% load static %}

<!DOCTYPE html>
<html>
<head>

    <title>
        {% block title %}
            My Website
        {% endblock %}
    </title>

    <link rel="stylesheet" href="{% static 'css/output.css' %}">

</head>

<body>

    {% include "includes/navbar.html" %}

    <main>

        {% block content %}
        {% endblock %}

    </main>

    {% include "includes/footer.html" %}

</body>
</html>
```

এখানে দুটি block আছে

- `title`
    
- `content`
    

---

## home.html

```html
{% extends "base.html" %}

{% block title %}
Home
{% endblock %}

{% block content %}

<h1>Home Page</h1>

<p>Welcome to Django.</p>

{% endblock %}
```

---

## about.html

```html
{% extends "base.html" %}

{% block title %}
About
{% endblock %}

{% block content %}

<h1>About Us</h1>

<p>About Page</p>

{% endblock %}
```

---

## navbar.html

```html
<nav>

<a href="/">Home</a>

<a href="/about/">About</a>

</nav>
```

---

## footer.html

```html
<footer>

Copyright 2026

</footer>
```

---

# Output

যখন `home.html` render হবে

```
base.html
        │
        ├── navbar.html
        │
        ├── Home Page Content
        │
        └── footer.html
```

যখন `about.html` render হবে

```
base.html
        │
        ├── navbar.html
        │
        ├── About Content
        │
        └── footer.html
```

---

# Multiple Blocks

```html
{% block css %}
{% endblock %}

{% block title %}
{% endblock %}

{% block content %}
{% endblock %}

{% block javascript %}
{% endblock %}
```

Child template

```html
{% extends "base.html" %}

{% block css %}
<style>
h1{
    color:red;
}
</style>
{% endblock %}

{% block content %}

<h1>Hello Django</h1>

{% endblock %}
```

---

# Nested Template Inheritance (Large Project)

```
base.html
      │
      ▼
dashboard_base.html
      │
      ▼
dashboard/home.html
```

### base.html

```
Navbar
Footer
```

↓

### dashboard_base.html

```html
{% extends "base.html" %}

{% block content %}

<div class="flex">

    {% include "includes/sidebar.html" %}

    <div>

        {% block dashboard_content %}
        {% endblock %}

    </div>

</div>

{% endblock %}
```

↓

### dashboard/home.html

```html
{% extends "dashboard_base.html" %}

{% block dashboard_content %}

<h2>Dashboard</h2>

{% endblock %}
```

এভাবে Dashboard-এর সব page একই layout ব্যবহার করবে।

---

# Best Practice (Large Project)

```text
templates/
│
├── base.html
│
├── layouts/
│   ├── dashboard_base.html
│   ├── auth_base.html
│   └── admin_base.html
│
├── includes/
│   ├── navbar.html
│   ├── sidebar.html
│   ├── footer.html
│   ├── messages.html
│   └── pagination.html
│
├── dashboard/
├── users/
├── products/
└── orders/
```

---

## `extends` বনাম `include`

| Feature                               | `{% extends %}`                                                       | `{% include %}`               |
| ------------------------------------- | --------------------------------------------------------------------- | ----------------------------- |
| Purpose                               | Parent layout inherit করা                                             | ছোট template যোগ করা          |
| Use case                              | পুরো page layout                                                      | Navbar, Footer, Sidebar, Card |
| এক template-এ কতবার ব্যবহার করা যায়? | **শুধু একবার**, এবং এটি template-এর **প্রথম template tag** হওয়া উচিত | যতবার দরকার ততবার             |

### Rule of Thumb

- **`extends`** → Page layout-এর জন্য।

- **`include`** → Reusable components-এর জন্য।
    

এটাই Django-র standard template inheritance pattern এবং বড় project-এ সবচেয়ে বেশি ব্যবহৃত হয়।

-------------
হ্যাঁ, **Django Template-এ Multilevel Inheritance সম্পূর্ণ support করে** এবং বড় project-এ এটি খুবই common।

তবে একটা গুরুত্বপূর্ণ rule আছে:

> **একটি template শুধুমাত্র একটি template-কে `extends` করতে পারে।** কিন্তু সেই parent template আবার আরেকটি template-কে `extends` করতে পারে। এভাবেই multilevel inheritance তৈরি হয়।

---

# Example

## Folder Structure

```text
templates/
│
├── base.html
├── layouts/
│   ├── dashboard_base.html
│   └── admin_base.html
│
├── dashboard/
│   ├── home.html
│   └── profile.html
│
└── includes/
    ├── navbar.html
    ├── sidebar.html
    └── footer.html
```

---

# Level 1 (Root)

## base.html

```html
<!DOCTYPE html>
<html>

<head>
    <title>
        {% block title %}
        My Website
        {% endblock %}
    </title>
</head>

<body>

    {% include "includes/navbar.html" %}

    {% block body %}
    {% endblock %}

    {% include "includes/footer.html" %}

</body>
</html>
```

---

# Level 2

## layouts/dashboard_base.html

```html
{% extends "base.html" %}

{% block body %}

<div class="flex">

    {% include "includes/sidebar.html" %}

    <div class="content">

        {% block dashboard_content %}
        {% endblock %}

    </div>

</div>

{% endblock %}
```

---

# Level 3

## dashboard/home.html

```html
{% extends "layouts/dashboard_base.html" %}

{% block title %}
Dashboard
{% endblock %}

{% block dashboard_content %}

<h1>Dashboard Home</h1>

{% endblock %}
```

---

## Render Flow

```text
dashboard/home.html
        │
        ▼
dashboard_base.html
        │
        ▼
base.html
        │
        ▼
Final HTML
```

---

# Even More Levels

```text
base.html
     │
     ▼
dashboard_base.html
     │
     ▼
employee_base.html
     │
     ▼
employee/profile.html
```

এটাও Django support করে।

---

## Example

### employee_base.html

```html
{% extends "layouts/dashboard_base.html" %}

{% block dashboard_content %}

<div class="employee-layout">

    {% block employee_content %}
    {% endblock %}

</div>

{% endblock %}
```

---

### employee/profile.html

```html
{% extends "employee_base.html" %}

{% block employee_content %}

<h2>Employee Profile</h2>

{% endblock %}
```

---

# Block Override

Parent

```html
{% block title %}
Website
{% endblock %}
```

Child

```html
{% block title %}
Dashboard
{% endblock %}
```

Output

```html
<title>Dashboard</title>
```

---

# `block.super`

যদি parent block-এর content রাখতে চাও এবং তার সাথে নতুন content যোগ করতে চাও।

### Parent

```html
{% block css %}
<link rel="stylesheet" href="base.css">
{% endblock %}
```

### Child

```html
{% block css %}
{{ block.super }}
<link rel="stylesheet" href="dashboard.css">
{% endblock %}
```

Output

```html
<link rel="stylesheet" href="base.css">
<link rel="stylesheet" href="dashboard.css">
```

---

# Professional Structure

```text
templates/
│
├── base.html
│
├── layouts/
│   ├── auth_base.html
│   ├── dashboard_base.html
│   ├── admin_base.html
│   └── email_base.html
│
├── includes/
│   ├── navbar.html
│   ├── sidebar.html
│   ├── footer.html
│   └── messages.html
│
├── dashboard/
│   ├── home.html
│   ├── profile.html
│   └── settings.html
│
├── users/
├── products/
└── orders/
```

---

# Rules

✅ Allowed

```text
base.html
    ↓
dashboard_base.html
    ↓
dashboard/home.html
```

✅ Allowed

```text
base.html
    ↓
admin_base.html
    ↓
admin/product/list.html
```

❌ Not Allowed

```html
{% extends "base.html" %}
{% extends "dashboard_base.html" %}
```

একটি template-এ **দুটি `extends`** ব্যবহার করা যায় না।

---

## Industry Practice

বড় Django project-এ সাধারণত ৩–৪ level inheritance-এর বেশি করা হয় না।

```text
base.html
    ↓
layout.html
    ↓
feature_base.html
    ↓
page.html
```

এর বেশি level হলে template structure জটিল হয়ে যায় এবং maintain করা কঠিন হয়। সাধারণত **২–৪ level** inheritance-ই যথেষ্ট এবং এটিই industry standard।

-----------
