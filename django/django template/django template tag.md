Django Template Language (DTL)-এ কিছু **Template Tags** প্রতিদিন ব্যবহার করা হয়। একজন Django Developer হিসেবে নিচের tag-গুলো অবশ্যই জানতে হবে।

---

# 1. `{% load %}`

Static file বা custom template tag load করতে ব্যবহৃত হয়।

```html
{% load static %}
```

### Example

```html
{% load static %}

<link rel="stylesheet" href="{% static 'css/style.css' %}">
<img src="{% static 'images/logo.png' %}">
```

---

# 2. `{% extends %}`

Parent template inherit করার জন্য।

### base.html

```html
<!DOCTYPE html>
<html>
<body>

{% block content %}
{% endblock %}

</body>
</html>
```

### home.html

```html
{% extends "base.html" %}

{% block content %}
<h1>Home Page</h1>
{% endblock %}
```

---

# 3. `{% block %}`

Child template যে অংশ পরিবর্তন করবে সেটা define করে।

```html
<title>

{% block title %}
My Website
{% endblock %}

</title>
```

Child

```html
{% block title %}
Home
{% endblock %}
```

---

# 4. `{% include %}`

একটি template-এর ভিতরে আরেকটি template যোগ করে।

```html
{% include "includes/navbar.html" %}
```

অথবা

```html
{% include "products/card.html" %}
```

---

# 5. `{% url %}` ⭐⭐⭐

Hardcode URL না লিখে URL name ব্যবহার করা।

### urls.py

```python
urlpatterns = [
    path("", home, name="home"),
    path("products/", products, name="products"),
]
```

Template

```html
<a href="{% url 'home' %}">Home</a>

<a href="{% url 'products' %}">Products</a>
```

Dynamic parameter

```html
<a href="{% url 'product_detail' product.id %}">
```

Multiple parameter

```html
<a href="{% url 'order_detail' order.id customer.id %}">
```

---

# 6. `{% static %}` ⭐⭐⭐

Static file load করার জন্য।

```html
{% load static %}

<link rel="stylesheet" href="{% static 'css/output.css' %}">
```

JS

```html
<script src="{% static 'js/app.js' %}"></script>
```

Image

```html
<img src="{% static 'images/logo.png' %}">
```

---

# 7. `{% if %}`

Condition check করার জন্য।

```html
{% if user.is_authenticated %}

Welcome {{ user.username }}

{% endif %}
```

---

## if else

```html
{% if products %}

Products Found

{% else %}

No Product

{% endif %}
```

---

## if elif

```html
{% if age >= 18 %}

Adult

{% elif age >= 13 %}

Teenager

{% else %}

Child

{% endif %}
```

---

# 8. `{% for %}` ⭐⭐⭐

Loop

```html
{% for product in products %}

{{ product.name }}

{% endfor %}
```

---

## Empty

```html
{% for product in products %}

{{ product.name }}

{% empty %}

No Products

{% endfor %}
```

---

# 9. `forloop`

Loop information।

```html
{% for product in products %}

{{ forloop.counter }}

{{ product.name }}

{% endfor %}
```

Output

```
1 Laptop
2 Phone
3 TV
```

Useful variables

```html
{{ forloop.counter }}
{{ forloop.counter0 }}
{{ forloop.first }}
{{ forloop.last }}
{{ forloop.revcounter }}
```

---

# 10. `{% csrf_token %}` ⭐⭐⭐

POST form-এর জন্য বাধ্যতামূলক।

```html
<form method="POST">

{% csrf_token %}

<input type="text">

<button>Save</button>

</form>
```

---

# 11. `{% comment %}`

Comment

```html
{% comment %}

This is comment

{% endcomment %}
```

---

# 12. `{% with %}`

Temporary variable তৈরি করা।

```html
{% with total=cart.items.count %}

Total Item : {{ total }}

{% endwith %}
```

---

# 13. `{% regroup %}`

Data group করার জন্য।

```html
{% regroup products by category as grouped_products %}
```

তারপর

```html
{% for group in grouped_products %}

<h2>{{ group.grouper }}</h2>

{% for product in group.list %}

{{ product.name }}

{% endfor %}

{% endfor %}
```

---

# 14. `{% cycle %}`

Alternate value দেওয়ার জন্য।

```html
{% for product in products %}

<tr class="{% cycle 'odd' 'even' %}">

...

</tr>

{% endfor %}
```

---

# 15. `{% now %}`

Current Date/Time

```html
{% now "Y" %}
```

Output

```
2026
```

Another

```html
{% now "d M Y" %}
```

Output

```
26 Jun 2026
```

---

# 16. `{% spaceless %}`

Extra HTML whitespace remove করে।

```html
{% spaceless %}

<div>
    <span>Hello</span>
</div>

{% endspaceless %}
```

---

# 17. `{% verbatim %}`

JavaScript framework-এর `{{ }}` syntax escape করতে।

```html
{% verbatim %}

{{ message }}

{% endverbatim %}
```

---

# Most Used Template Filters

Filters variable-এর value পরিবর্তন করে।

```html
{{ user.username|upper }}
```

---

## Default

```html
{{ name|default:"Guest" }}
```

---

## Length

```html
{{ products|length }}
```

---

## Lower

```html
{{ username|lower }}
```

---

## Upper

```html
{{ username|upper }}
```

---

## Title

```html
{{ username|title }}
```

---

## Date

```html
{{ product.created_at|date:"d M Y" }}
```

---

## Truncate

```html
{{ description|truncatewords:20 }}
```

---

## YesNo

```html
{{ product.is_active|yesno:"Yes,No" }}
```

---

# Real Project Example

```html
{% extends "base.html" %}
{% load static %}

{% block content %}

{% include "includes/navbar.html" %}

{% if products %}

    {% for product in products %}

        <h3>{{ forloop.counter }}. {{ product.name }}</h3>

        <img src="{% static 'images/product.png' %}">

    {% empty %}

        <p>No Product Found</p>

    {% endfor %}

{% endif %}

{% endblock %}
```

# সবচেয়ে বেশি ব্যবহৃত Template Tags (Interview + Real Project)

|Tag|Usage|Frequency|
|---|---|---|
|`{% load static %}`|Static files|⭐⭐⭐⭐⭐|
|`{% static %}`|CSS/JS/Image|⭐⭐⭐⭐⭐|
|`{% url %}`|URL generation|⭐⭐⭐⭐⭐|
|`{% extends %}`|Template inheritance|⭐⭐⭐⭐⭐|
|`{% block %}`|Child content|⭐⭐⭐⭐⭐|
|`{% include %}`|Reusable partials|⭐⭐⭐⭐⭐|
|`{% if %}`|Conditions|⭐⭐⭐⭐⭐|
|`{% for %}`|Loops|⭐⭐⭐⭐⭐|
|`{% csrf_token %}`|Forms|⭐⭐⭐⭐⭐|
|`{% with %}`|Temporary variable|⭐⭐⭐⭐|
|`{% cycle %}`|Alternate row styles|⭐⭐⭐|
|`{% regroup %}`|Group data|⭐⭐|
|`{% now %}`|Current date/time|⭐⭐|
|`{% comment %}`|Template comments|⭐⭐|
|`{% verbatim %}`|Escape `{{ }}`|⭐|

এই ৮–১০টি tag (`load`, `static`, `url`, `extends`, `block`, `include`, `if`, `for`, `csrf_token`, `with`) ভালোভাবে শিখে নিলে Django Template-এর প্রায় ৯০% কাজ সহজেই করতে পারবে।

--------------

