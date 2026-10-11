হ্যাঁ। Django-তে `name` বা `title` থেকে **automatically slug generate** করার সবচেয়ে সহজ এবং clean উপায় হলো `pre_save` signal বা model-এর `save()` override করা।

তুমি যেহেতু Signals শিখেছ, আগে **Signal দিয়ে** দেখাই।

### 1. Model

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)

    slug = models.SlugField(
        max_length=220,
        unique=True,
        blank=True
    )

    def __str__(self):
        return self.name
```

ধরো:

```text
name = "Gaming Laptop"
```

আমরা চাই:

```text
slug = "gaming-laptop"
```

---

### 2. `signals.py`

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver
from django.utils.text import slugify

from .models import Product


@receiver(pre_save, sender=Product)
def generate_product_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = slugify(instance.name)
```

এখন:

```python
Product.objects.create(
    name="Gaming Laptop"
)
```

Database-এ হবে:

```text
name: Gaming Laptop
slug: gaming-laptop
```

### Flow

```text
Product.objects.create()
        ↓
Product.save()
        ↓
pre_save
        ↓
slugify("Gaming Laptop")
        ↓
"gaming-laptop"
        ↓
Database INSERT
```

---

## 3. `apps.py`-তে signal register

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):

    default_auto_field = "django.db.models.BigAutoField"
    name = "products"

    def ready(self):
        from . import signals
```

`settings.py`:

```python
INSTALLED_APPS = [
    # ...
    "products.apps.ProductsConfig",
]
```

---

## 4. কিন্তু একটা সমস্যা আছে — duplicate slug

ধরো:

```text
Product 1:
name = Gaming Laptop
slug = gaming-laptop
```

আবার:

```text
Product 2:
name = Gaming Laptop
```

তাহলে দুটোর slug হবে:

```text
gaming-laptop
gaming-laptop
```

কিন্তু আমরা করেছি:

```python
unique=True
```

তাই database error হবে।

আমাদের দরকার:

```text
gaming-laptop
gaming-laptop-2
gaming-laptop-3
```

---

# 5. Production-friendly slug generator

একটা reusable function বানাতে পারো:

```python
from django.utils.text import slugify


def generate_unique_slug(instance, value):
    base_slug = slugify(value)
    slug = base_slug

    Model = instance.__class__

    counter = 2

    while Model.objects.filter(slug=slug).exclude(
        pk=instance.pk
    ).exists():

        slug = f"{base_slug}-{counter}"
        counter += 1

    return slug
```

তারপর signal:

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

from .models import Product
from .utils import generate_unique_slug


@receiver(pre_save, sender=Product)
def generate_product_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = generate_unique_slug(
            instance,
            instance.name
        )
```

এখন:

```text
Gaming Laptop
       ↓
gaming-laptop

Gaming Laptop
       ↓
gaming-laptop-2

Gaming Laptop
       ↓
gaming-laptop-3
```

---

# 6. `title` হলে একইভাবে

ধরো `Blog`:

```python
class Blog(models.Model):

    title = models.CharField(
        max_length=255
    )

    slug = models.SlugField(
        max_length=280,
        unique=True,
        blank=True
    )
```

Signal:

```python
@receiver(pre_save, sender=Blog)
def generate_blog_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = generate_unique_slug(
            instance,
            instance.title
        )
```

তাহলে:

```text
title:
"Django Signals Complete Guide"

slug:
"django-signals-complete-guide"
```

---

## 7. একটা গুরুত্বপূর্ণ সিদ্ধান্ত

এই condition:

```python
if not instance.slug:
```

এর মানে:

> **শুধু প্রথমবার slug তৈরি হবে।**

যেমন:

```text
name = "Gaming Laptop"
slug = "gaming-laptop"
```

পরে name change করলাম:

```text
name = "Gaming Laptop Pro"
```

তখন slug থাকবে:

```text
gaming-laptop
```

অর্থাৎ automatically change হবে না।

এটা অনেক সময় **ভালো behavior**, কারণ URL change হলে পুরোনো links ভেঙে যেতে পারে।

---

### যদি তুমি চাও name/title change হলে slug-ও change হবে

তাহলে logic আলাদা:

```python
@receiver(pre_save, sender=Product)
def generate_product_slug(sender, instance, **kwargs):

    instance.slug = generate_unique_slug(
        instance,
        instance.name
    )
```

কিন্তু production-এ URL slug সাধারণত **stable রাখা ভালো**।

### আমার recommendation

E-commerce Product-এর জন্য:

```text
name → প্রথমবার slug generate
slug → পরে stable
```

যেমন:

```text
Product:
name = "iPhone 17 Pro Max"
slug = "iphone-17-pro-max"
```

পরে name পরিবর্তন হলেও slug পরিবর্তন না করাই ভালো।

**আর একটা বিষয়:** `unique=True` থাকলেও concurrent requests-এর ক্ষেত্রে শুধু `while exists()` যথেষ্ট নয়; database `IntegrityError` handling দরকার হতে পারে। Production-grade slug generator বানাতে গেলে সেটাও আমরা পরে করতে পারি।
