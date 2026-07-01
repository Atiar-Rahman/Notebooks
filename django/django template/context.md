## Django Context কী?

**Context** হলো একটি **Python Dictionary**, যা View থেকে Template-এ data পাঠানোর জন্য ব্যবহার করা হয়।

সহজভাবে:

> **View → Context → Template**

```text
Browser
    │
    ▼
View
    │
    ▼
Context (Dictionary)
    │
    ▼
Template (HTML)
```

---

# Basic Example

## View

```python
from django.shortcuts import render

def home(request):
    context = {
        "name": "Atiar",
        "age": 25,
    }

    return render(request, "home.html", context)
```

---

## Template

```html
<h1>{{ name }}</h1>
<p>{{ age }}</p>
```

Output

```text
Atiar

25
```

---

# Context is a Dictionary

```python
context = {
    "title": "Home",
    "username": "Atiar",
    "is_login": True,
}
```

Template

```html
{{ title }}

{{ username }}

{{ is_login }}
```

---

# Sending Model Data

## View

```python
def product_list(request):
    products = Product.objects.all()

    context = {
        "products": products,
    }

    return render(request, "products/list.html", context)
```

---

## Template

```html
{% for product in products %}
    {{ product.name }}
    {{ product.price }}
{% endfor %}
```

---

# Multiple Data

```python
context = {
    "products": Product.objects.all(),
    "categories": Category.objects.all(),
    "brands": Brand.objects.all(),
}
```

Template

```html
<h2>Categories</h2>

{% for category in categories %}
    {{ category.name }}
{% endfor %}

<hr>

<h2>Products</h2>

{% for product in products %}
    {{ product.name }}
{% endfor %}
```

---

# Dynamic Value

```python
context = {
    "user": request.user,
}
```

Template

```html
{{ user.username }}
```

---

# Class-Based View (CBV)

```python
from django.views.generic import TemplateView

class HomeView(TemplateView):
    template_name = "home.html"

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)

        context["products"] = Product.objects.all()
        context["categories"] = Category.objects.all()

        return context
```

---

# Update Context

```python
context = {}

context["products"] = Product.objects.all()

context["categories"] = Category.objects.all()
```

অথবা

```python
context.update({
    "products": Product.objects.all(),
    "categories": Category.objects.all(),
})
```

---

# Merge Multiple Context

```python
product_context = {
    "products": Product.objects.all()
}

category_context = {
    "categories": Category.objects.all()
}

context = {}

context.update(product_context)
context.update(category_context)
```

Output

```python
{
    "products": ...,
    "categories": ...
}
```

---

# Context Processor

যদি সব template-এ `categories` দরকার হয়।

```python
# context_processors.py

def category_context(request):
    return {
        "categories": Category.objects.all()
    }
```

`settings.py`

```python
TEMPLATES = [
    {
        ...
        "OPTIONS": {
            "context_processors": [
                ...
                "shop.context_processors.category_context",
            ]
        }
    }
]
```

এখন সব template-এ

```html
{{ categories }}
```

available থাকবে।

---

# Passing Context to Include

```html
{% include "products/card.html" with products=featured_products %}
```

`card.html`

```html
{% for product in products %}
    {{ product.name }}
{% endfor %}
```

---

# Nested Context

```python
context = {
    "user": {
        "name": "Atiar",
        "email": "atiar@example.com",
    }
}
```

Template

```html
{{ user.name }}

{{ user.email }}
```

---

# Real Example (E-commerce)

```python
def home(request):
    context = {
        "categories": Category.objects.all(),
        "featured_products": Product.objects.filter(is_featured=True),
        "new_products": Product.objects.order_by("-created_at")[:10],
        "cart_count": Cart.objects.count(),
    }

    return render(request, "home.html", context)
```

Template

```html
<h2>Featured Products</h2>

{% for product in featured_products %}
    {{ product.name }}
{% endfor %}

<hr>

Cart: {{ cart_count }}
```

---

# Best Practice (Large Project)

বড় project-এ View-এর ভিতরে সব query না লিখে Service বা Context Builder ব্যবহার করা ভালো।

```python
# services.py

class HomeContext:

    @staticmethod
    def get_context():
        return {
            "categories": Category.objects.all(),
            "products": Product.objects.filter(is_active=True),
        }
```

View

```python
class HomeView(TemplateView):
    template_name = "home.html"

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        context.update(HomeContext.get_context())
        return context
```

---

# Summary

|Context Type|কখন ব্যবহার করবেন|
|---|---|
|Simple Dictionary|একটি view-এর data template-এ পাঠাতে|
|`get_context_data()`|Class-Based View-এ|
|`context.update()`|একাধিক source-এর context merge করতে|
|Context Processor|সব template-এ common data (যেমন navbar categories, site settings) দিতে|
|`{% include ... with %}`|Include করা template-এ নির্দিষ্ট context পাঠাতে|

### Context মনে রাখার সহজ সূত্র

```text
Python Data
      │
      ▼
Context (Dictionary)
      │
      ▼
Template (HTML)
      │
      ▼
User sees the data
```

Django-তে **Context** মূলত View এবং Template-এর মধ্যে **data exchange-এর bridge** হিসেবে কাজ করে।