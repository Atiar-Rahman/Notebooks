# Django REST Framework SearchFilter Mastery Course (4 Lessons)

এই কোর্স শেষে তুমি Production-level API-তে `SearchFilter` confidently ব্যবহার করতে পারবে।

SearchFilter হলো DRF-এর built-in filter backend, যা `?search=` query parameter ব্যবহার করে এক বা একাধিক text field-এ search করতে দেয়। এটি ব্যবহার করতে `filter_backends`-এ `SearchFilter` এবং `search_fields` সেট করতে হয়। ([Django Rest Framework][1])

---

# Lesson 1 — SearchFilter Basics

## কী শিখবে

* SearchFilter কী
* কেন ব্যবহার করা হয়
* Basic implementation
* Multiple fields search

---

## Project Structure

```
products/
    models.py
    serializers.py
    views.py
```

---

## Model

```python
from django.db import models


class Category(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    name = models.CharField(max_length=200)

    description = models.TextField()

    brand = models.CharField(max_length=100)

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

---

## Serializer

```python
from rest_framework import serializers

from .models import Product


class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = "__all__"
```

---

## View

```python
from rest_framework import generics
from rest_framework.filters import SearchFilter

from .models import Product
from .serializers import ProductSerializer


class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [SearchFilter]

    search_fields = [
        "name",
        "description",
    ]
```

---

## URL

```
GET

/api/products/?search=iphone
```

Generated SQL (conceptually):

```sql
WHERE

name ILIKE '%iphone%'

OR

description ILIKE '%iphone%'
```

---

## Multiple Field Search

```python
search_fields = [

    "name",

    "description",

    "brand"

]
```

Now

```
?search=samsung
```

matches

* name
* description
* brand

---

## Practice

Search

```
?search=apple
```

Search

```
?search=laptop
```

Search

```
?search=wireless
```

---

## Assignment

Create a Book API.

Search by

* title
* author
* description

---

# Lesson 2 Preview

পরের লেসনে শিখবে:

* Related model search (`category__name`)
* Nested field search
* Search prefixes (`^`, `=`, `$`, `@`)
* Exact vs Partial search

[1]: https://www.django-rest-framework.org/api-guide/filtering/?utm_source=chatgpt.com "Filtering - Django REST framework"
