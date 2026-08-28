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
# Lesson 2 — Django REST Framework SearchFilter: Advanced Search

Lesson 1-এ আমরা basic `SearchFilter` দেখেছি। এখন আমরা **real-world search** শিখব।

আজকের মূল বিষয়:

1. Related model search
2. Nested relationship search
3. Search prefixes
4. Partial vs exact search
5. Multiple search terms
6. Practical e-commerce example

---

# 1. Related Model Search

ধরো আমাদের model:

```python
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

এখানে:

```text
Product
   |
   | ForeignKey
   ↓
Category
```

Product-এর নিজের field:

```python
name
description
brand
price
```

কিন্তু Category-এর field:

```python
name
```

---

## Category name দিয়ে Product search

এভাবে লিখবে:

```python
search_fields = [
    "name",
    "description",
    "brand",
    "category__name",
]
```

খেয়াল করো:

```python
"category__name"
```

এখানে:

```text
category
   ↓
Category model
   ↓
name
```

---

## API

```http
GET /api/products/?search=electronics
```

এখন Product-এর:

```text
name
description
brand
category.name
```

সবগুলোতেই search হবে।

---

# 2. Multiple Relationship Search

ধরো Product-এর সাথে Brand model-ও আছে।

```python
class Brand(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    brand = models.ForeignKey(
        Brand,
        on_delete=models.CASCADE
    )

    name = models.CharField(max_length=200)
```

তাহলে:

```python
search_fields = [
    "name",
    "category__name",
    "brand__name",
]
```

এখন:

```http
?search=samsung
```

search করবে:

```text
Product.name
Category.name
Brand.name
```

---

# 3. Nested Relationship Search

এখন আরও interesting ব্যাপার।

ধরো:

```text
Product
   ↓
Category
   ↓
ParentCategory
```

Models:

```python
class ParentCategory(models.Model):
    name = models.CharField(max_length=100)


class Category(models.Model):

    parent = models.ForeignKey(
        ParentCategory,
        on_delete=models.CASCADE
    )

    name = models.CharField(max_length=100)


class Product(models.Model):

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    name = models.CharField(max_length=200)
```

এখন ParentCategory-এর name দিয়ে Product search করতে চাই।

তাহলে:

```python
search_fields = [
    "name",
    "category__name",
    "category__parent__name",
]
```

এখানে:

```text
category
    ↓
parent
    ↓
name
```

অর্থাৎ Django ORM-এর relationship traversal ব্যবহার করছি।

---

# 4. Search Prefix

এখন SearchFilter-এর সবচেয়ে important অংশ।

তুমি `search_fields`-এ শুধু field name না দিয়ে কিছু special prefix ব্যবহার করতে পারো।

যেমন:

```python
search_fields = [
    "^name",
    "=brand",
    "$description",
    "@description",
]
```

এগুলোর প্রত্যেকটির আলাদা meaning আছে।

---

# 5. `^` — Starts With

```python
search_fields = [
    "^name"
]
```

এর অর্থ:

> Search text দিয়ে field শুরু হতে হবে।

ধরো database:

```text
iPhone 15
iPhone 14
Samsung Galaxy
Apple MacBook
```

Search:

```http
?search=iPhone
```

match করবে:

```text
iPhone 15
iPhone 14
```

কিন্তু:

```text
My iPhone
```

match করবে না।

Conceptually:

```sql
WHERE name LIKE 'iPhone%'
```

---

# 6. `=` — Exact Match

```python
search_fields = [
    "=brand"
]
```

এর অর্থ:

> Exact match search.

ধরো:

```text
Apple
Samsung
Xiaomi
```

Search:

```http
?search=Apple
```

তাহলে:

```text
Apple
```

match করবে।

কিন্তু:

```text
Apple Store
Apple Mac
```

সেগুলো exact match হিসেবে match করবে না।

এটি useful যখন field-এর exact value দিয়ে filter-like search করতে চাও।

---

# 7. `$` — Regex Search

```python
search_fields = [
    "$name"
]
```

`$` regex-based search ব্যবহার করে।

উদাহরণ:

```python
search_fields = [
    "$name"
]
```

এটি সাধারণ substring search-এর চেয়ে বেশি flexible।

তবে production application-এ regex search ব্যবহার করার আগে database performance সম্পর্কে সতর্ক থাকতে হবে।

বিশেষ করে বড় database-এ regex search expensive হতে পারে।

---

# 8. `@` — Full-Text Search

```python
search_fields = [
    "@description"
]
```

এটি full-text search-এর জন্য।

তবে গুরুত্বপূর্ণ বিষয়:

**এটি database backend dependent।**

তাই development environment-এ blindly `@` ব্যবহার করা উচিত না।

যদি তোমার project PostgreSQL ব্যবহার করে, advanced full-text search-এর জন্য Django-এর `SearchVector`, `SearchQuery`, `SearchRank` ইত্যাদি শেখা আরও useful হবে।

---

# 9. Default Search কী?

যদি তুমি লেখো:

```python
search_fields = [
    "name"
]
```

তাহলে এটি normal partial search।

ধরো:

```text
Wireless Headphone
Gaming Headphone
iPhone
```

Search:

```http
?search=phone
```

তাহলে:

```text
Wireless Headphone
Gaming Headphone
```

match করতে পারে।

অর্থাৎ সাধারণত:

```text
contains
```

type search।

---

# 10. Prefix Comparison

এটা খুব ভালোভাবে মনে রাখো:

| Prefix  | Meaning               |
| ------- | --------------------- |
| `name`  | Normal partial search |
| `^name` | Starts with           |
| `=name` | Exact match           |
| `$name` | Regex                 |
| `@name` | Full-text search      |

সবচেয়ে বেশি practical:

```python
"name"
"^name"
"=name"
```

---

# 11. Real E-commerce Example

ধরো তোমার Product API:

```python
class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter
    ]

    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]
```

এখন user লিখতে পারবে:

```http
/api/products/?search=iphone
```

অথবা:

```http
/api/products/?search=electronics
```

অথবা:

```http
/api/products/?search=apple
```

একই search endpoint থেকে multiple fields search হবে।

---

# 12. গুরুত্বপূর্ণ: Search vs Filter

এখানে একটা common mistake হয়।

### SearchFilter

User জানে না exact value কী, তাই search করছে:

```http
?search=iphone
```

### DjangoFilterBackend

User নির্দিষ্ট field/value দিয়ে filter করছে:

```http
?category=5
```

অথবা:

```http
?brand=Apple
```

অর্থাৎ:

```text
Search
    ↓
"কিছু একটা খুঁজছি"

Filter
    ↓
"এই নির্দিষ্ট condition অনুযায়ী data চাই"
```

Production API-তে দুটো একসাথে ব্যবহার করা খুব common।

উদাহরণ:

```http
/api/products/?search=phone&category=2
```

এখানে:

```text
search=phone
      +
category=2
```

দুটো condition apply হবে।

---

# 13. Important Concept — Model Field থাকা লাগবে?

হ্যাঁ।

যেমন:

```python
search_fields = [
    "name",
    "description",
]
```

তাহলে `name` এবং `description` এমন field হতে হবে যেগুলো queryset-এর model/relationship-এ resolve করা যায়।

যেমন:

```python
"category__name"
```

এর জন্য:

```text
Product
   ↓
category
   ↓
Category
   ↓
name
```

এই relationship থাকতে হবে।

---

# 14. Practical Challenge 🔥

এই models ধরো:

```python
class Author(models.Model):

    name = models.CharField(
        max_length=100
    )


class Category(models.Model):

    name = models.CharField(
        max_length=100
    )


class Book(models.Model):

    title = models.CharField(
        max_length=200
    )

    description = models.TextField()

    author = models.ForeignKey(
        Author,
        on_delete=models.CASCADE
    )

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

তোমার task:

### Book API-তে search করতে হবে:

```text
Book title
Book description
Author name
Category name
```

তাহলে `search_fields` কী হবে?

নিজে আগে চেষ্টা করো।

**Answer:**

```python
search_fields = [
    "title",
    "description",
    "author__name",
    "category__name",
]
```

🔥 এটাই DRF SearchFilter-এর সবচেয়ে important skill:

```text
local field
+
related field
+
nested related field
```

---

# Lesson 2 — Mastery Summary

আজকের core concepts:

```text
SearchFilter
    │
    ├── name
    │
    ├── category__name
    │
    ├── author__name
    │
    ├── ^name
    │
    ├── =name
    │
    ├── $name
    │
    └── @name
```

এখন তুমি basic থেকে intermediate SearchFilter ব্যবহার করতে পারবে।

### Lesson 3-এ

আমরা **SearchFilter + DjangoFilterBackend + OrderingFilter** একসাথে ব্যবহার করে একটা production-style Product API বানাব, যেমন:

```http
/api/products/
    ?search=phone
    &category=2
    &min_price=500
    &max_price=5000
    &ordering=-price
```

এখানেই SearchFilter-এর সাথে real-world filtering শুরু হবে।

----
# Lesson 3 — SearchFilter + DjangoFilterBackend + OrderingFilter

এখন আমরা **SearchFilter mastery-এর সবচেয়ে practical অংশে** যাব।

Real-world API-তে শুধু:

```http
?search=phone
```

দেওয়া হয় না।

একজন user চাইতে পারে:

```http
?search=phone&category=2&min_price=500&max_price=5000&ordering=-price
```

অর্থাৎ একই API-তে:

* Search
* Exact filtering
* Range filtering
* Sorting

সব একসাথে কাজ করবে।

---

# 1. আমাদের Target API

শেষে আমরা এমন API বানাব:

```http
GET /api/products/
```

### Search

```http
?search=iphone
```

### Category filter

```http
?category=2
```

### Price range

```http
?min_price=500
```

```http
?max_price=5000
```

### Ordering

```http
?ordering=price
```

```http
?ordering=-price
```

### সব একসাথে

```http
?search=phone&category=2&min_price=500&max_price=5000&ordering=-price
```

---

# 2. Model

```python
from django.db import models


class Category(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE,
        related_name="products"
    )

    name = models.CharField(
        max_length=200
    )

    description = models.TextField()

    brand = models.CharField(
        max_length=100
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

# 3. Serializer

```python
from rest_framework import serializers

from .models import Product


class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Product
        fields = "__all__"
```

---

# 4. Install django-filter

যদি আগে install না করে থাকো:

```bash
pip install django-filter
```

---

# 5. settings.py

`INSTALLED_APPS`:

```python
INSTALLED_APPS = [

    # Django apps

    "django_filters",

    # DRF apps
]
```

---

# 6. SearchFilter

আমরা আগে এটা শিখেছি:

```python
from rest_framework.filters import SearchFilter
```

তারপর:

```python
filter_backends = [
    SearchFilter
]
```

এবং:

```python
search_fields = [
    "name",
    "description",
    "brand",
    "category__name",
]
```

এখন Search API:

```http
/api/products/?search=iphone
```

---

# 7. DjangoFilterBackend

এখন exact filtering-এর জন্য:

```python
from django_filters.rest_framework import DjangoFilterBackend
```

তারপর:

```python
filter_backends = [
    SearchFilter,
    DjangoFilterBackend,
]
```

কিন্তু এখানে একটা গুরুত্বপূর্ণ বিষয়:

**শুধু `DjangoFilterBackend` add করলেই arbitrary `?category=2` বা `?min_price=500` কাজ করবে না।**

আমাদের filter configuration তৈরি করতে হবে।

---

# 8. FilterSet তৈরি করি

`filters.py`:

```python
import django_filters

from .models import Product


class ProductFilter(
    django_filters.FilterSet
):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    class Meta:

        model = Product

        fields = [
            "category",
            "brand",
        ]
```

এখানে:

```python
min_price
```

মানে:

```text
price >= min_price
```

আর:

```python
max_price
```

মানে:

```text
price <= max_price
```

---

# 9. FilterSet কেন দরকার?

ধরো user পাঠাল:

```http
?min_price=500
```

আমরা চাই:

```python
Product.objects.filter(
    price__gte=500
)
```

`ProductFilter` আমাদের এই mapping তৈরি করে।

```text
min_price
    ↓
price
    ↓
gte
```

অর্থাৎ:

```text
min_price=500
       ↓
price__gte=500
```

---

# 10. View সম্পূর্ণ করি

```python
from rest_framework import generics

from rest_framework.filters import (
    SearchFilter,
    OrderingFilter,
)

from django_filters.rest_framework import (
    DjangoFilterBackend
)

from .models import Product

from .serializers import ProductSerializer

from .filters import ProductFilter


class ProductListAPIView(
    generics.ListAPIView
):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]

    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]

    filterset_class = ProductFilter

    ordering_fields = [
        "price",
        "name",
        "created_at",
    ]

    ordering = [
        "-created_at"
    ]
```

এখন আমাদের API অনেক powerful।

---

# 11. Search

Request:

```http
GET /api/products/?search=iphone
```

Search হবে:

```text
name
description
brand
category.name
```

---

# 12. Category Filter

Request:

```http
GET /api/products/?category=2
```

এটা equivalent:

```python
Product.objects.filter(
    category=2
)
```

---

# 13. Brand Filter

```http
GET /api/products/?brand=Apple
```

এটা:

```python
Product.objects.filter(
    brand="Apple"
)
```

---

# 14. Minimum Price

Request:

```http
GET /api/products/?min_price=500
```

Filter:

```python
price__gte=500
```

অর্থাৎ:

```text
price >= 500
```

---

# 15. Maximum Price

```http
GET /api/products/?max_price=5000
```

Equivalent:

```python
price__lte=5000
```

অর্থাৎ:

```text
price <= 5000
```

---

# 16. Price Range

এখন দুটো একসাথে:

```http
GET /api/products/?min_price=500&max_price=5000
```

Conceptually:

```python
Product.objects.filter(
    price__gte=500,
    price__lte=5000
)
```

অর্থাৎ:

```text
500 <= price <= 5000
```

---

# 17. OrderingFilter

এখন sorting।

Import:

```python
from rest_framework.filters import OrderingFilter
```

View:

```python
filter_backends = [
    SearchFilter,
    DjangoFilterBackend,
    OrderingFilter,
]
```

Allowed fields:

```python
ordering_fields = [
    "price",
    "name",
    "created_at",
]
```

---

# 18. Price Ascending

```http
?ordering=price
```

Result:

```text
500
1000
1500
3000
5000
```

---

# 19. Price Descending

```http
?ordering=-price
```

Result:

```text
5000
3000
1500
1000
500
```

`-` মানে descending।

---

# 20. Multiple Ordering

তুমি চাইলে:

```http
?ordering=-price,name
```

মানে:

```text
প্রথমে price descending
তারপর একই price হলে name ascending
```

---

# 21. Default Ordering

আমরা লিখেছি:

```python
ordering = [
    "-created_at"
]
```

তাই user যদি কোনো ordering না দেয়:

```http
/api/products/
```

তাহলে newest products আগে আসবে।

---

# 22. সবচেয়ে গুরুত্বপূর্ণ অংশ 🔥

এখন এই request দেখো:

```http
/api/products/
?search=phone
&category=2
&min_price=500
&max_price=5000
&ordering=-price
```

এখানে পাঁচটা কাজ হচ্ছে:

```text
                    Product API
                        │
        ┌───────────────┼────────────────┐
        ↓               ↓                ↓
     Search          Filter           Ordering
        │               │                │
     phone          category=2       -price
        │               │
        │          price >= 500
        │          price <= 5000
        │
        ↓
   Final QuerySet
```

এটাই real-world API pattern।

---

# 23. Search + Filter + Ordering একসাথে

ধরো database:

| Product     | Category |  Price |
| ----------- | -------- | -----: |
| iPhone 15   | Mobile   |  70000 |
| iPhone 14   | Mobile   |  60000 |
| Samsung A55 | Mobile   |  45000 |
| MacBook     | Laptop   | 120000 |
| Dell Laptop | Laptop   |  80000 |

Request:

```http
?search=phone&category=2&min_price=50000&ordering=-price
```

প্রথমে search:

```text
phone
```

তারপর category:

```text
category=2
```

তারপর:

```text
price >= 50000
```

শেষে:

```text
price descending
```

ফলাফল logically:

```text
iPhone 15    70000
iPhone 14    60000
```

---

# 24. খুব গুরুত্বপূর্ণ Difference

SearchFilter:

```python
search_fields = [
    "name",
    "description",
]
```

এখানে user-এর query:

```http
?search=phone
```

---

DjangoFilterBackend:

```python
filterset_class = ProductFilter
```

এখানে user-এর structured condition:

```http
?category=2
&min_price=500
```

---

OrderingFilter:

```python
ordering_fields = [
    "price",
    "name",
]
```

এখানে:

```http
?ordering=-price
```

তিনটা আলাদা responsibility:

```text
SearchFilter
     ↓
Text search

DjangoFilterBackend
     ↓
Conditions

OrderingFilter
     ↓
Sorting
```

---

# 25. Production API Structure

আমি সাধারণত এভাবে organize করব:

```text
products/
│
├── models.py
│
├── serializers.py
│
├── filters.py
│
├── views.py
│
├── urls.py
│
└── admin.py
```

`filters.py`:

```python
class ProductFilter(django_filters.FilterSet):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    class Meta:
        model = Product
        fields = [
            "category",
            "brand",
        ]
```

এভাবে `views.py` clean থাকবে।

---

# 26. Common Mistake ❌

অনেকে এভাবে করে:

```python
filter_backends = [
    SearchFilter
]

search_fields = [
    "name",
    "price",
]
```

তারপর:

```http
?price=500
```

দিয়ে exact price filtering expect করে।

এটা **SearchFilter-এর কাজ না**।

যদি তুমি structured price filtering চাও:

```text
DjangoFilterBackend
```

ব্যবহার করো।

---

# 27. আরেকটি Common Mistake ❌

এটা:

```python
search_fields = [
    "category"
]
```

দেওয়া এবং category-এর name search করতে চাওয়া ঠিক approach নয়।

যদি:

```python
Product.category = ForeignKey(Category)
```

এবং তুমি Category-এর name search করতে চাও:

```python
search_fields = [
    "category__name"
]
```

---

# 28. Lesson 3 Challenge 🔥

একটা `ProductFilter` তৈরি করো যেখানে থাকবে:

```text
category
brand
min_price
max_price
```

এবং Product API-তে থাকবে:

```text
SearchFilter
DjangoFilterBackend
OrderingFilter
```

Search fields:

```text
name
description
brand
category__name
```

Ordering fields:

```text
price
name
created_at
```

তারপর এই URL কাজ করাতে হবে:

```http
/api/products/
?search=phone
&category=2
&brand=Samsung
&min_price=1000
&max_price=50000
&ordering=-price
```

---

## Lesson 3 Mastery Checklist

আজ তোমার এই architecture পরিষ্কার হওয়া উচিত:

```text
                 Product API
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
 SearchFilter    DjangoFilter    OrderingFilter
       │           Backend             │
       ↓              ↓                ↓
    search       conditions         sorting
       │              │                │
       └──────────────┼────────────────┘
                      ↓
                  QuerySet
                      ↓
                  Response
```

**Lesson 4**-এ আমরা SearchFilter-এর আরও advanced/production side করব—custom search behavior, `Q()` queries, custom `FilterSet`, `icontains`/lookup control, performance considerations এবং একটা complete product search API বানিয়ে mastery finish করব।
# Lesson 3 — SearchFilter: Production-Level Usage

আগের Lesson 3-এ আমরা SearchFilter-এর সাথে `DjangoFilterBackend` এবং `OrderingFilter` একসাথে ব্যবহার দেখেছি। এবার **Lesson 3-কে আরও গভীরভাবে** বুঝি—বিশেষ করে request কীভাবে QuerySet-এ transform হয়।

---

## 1. তিনটা Filter Backend-এর কাজ আলাদা

একটি Product API:

```python
class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]
```

এখানে:

```text
SearchFilter
    ↓
Text search

DjangoFilterBackend
    ↓
Structured filtering

OrderingFilter
    ↓
Sorting
```

---

# 2. SearchFilter

```python
search_fields = [
    "name",
    "description",
    "brand",
    "category__name",
]
```

Request:

```http
GET /api/products/?search=iphone
```

SearchFilter এই `search` parameter পড়বে।

Conceptually:

```text
name contains "iphone"
OR
description contains "iphone"
OR
brand contains "iphone"
OR
category.name contains "iphone"
```

---

# 3. Related Field Search

এটাই SearchFilter-এর খুব গুরুত্বপূর্ণ feature।

Model:

```python
class Product(models.Model):

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    name = models.CharField(
        max_length=200
    )
```

Category:

```python
class Category(models.Model):

    name = models.CharField(
        max_length=100
    )
```

Product-এর category name search করতে:

```python
search_fields = [
    "name",
    "category__name",
]
```

এখানে:

```text
Product
   │
   └── category
          │
          └── name
```

তাই:

```http
?search=electronics
```

দিলে `Category.name`-এর মধ্যেও search হবে।

---

# 4. Nested Relationship

আরও গভীরে যাওয়া যায়।

```text
Product
   ↓
Category
   ↓
ParentCategory
   ↓
name
```

তাহলে:

```python
search_fields = [
    "name",
    "category__parent__name",
]
```

Django ORM relationship traversal:

```text
category
    ↓
parent
    ↓
name
```

---

# 5. Search Prefix

SearchFilter-এ prefix ব্যবহার করা যায়।

### Normal

```python
"name"
```

### Starts with

```python
"^name"
```

### Exact

```python
"=name"
```

### Regex

```python
"$name"
```

### Full text

```python
"@description"
```

---

# 6. Normal Search

```python
search_fields = [
    "name"
]
```

Request:

```http
?search=phone
```

এটি সাধারণ text matching করবে।

উদাহরণ:

```text
Wireless Phone
Phone Cover
Smartphone
```

এর মধ্যে matching result পাওয়া যেতে পারে।

---

# 7. Starts With

```python
search_fields = [
    "^name"
]
```

Request:

```http
?search=phone
```

এখানে search মূলত field-এর শুরুতে `phone` থাকার দিকে লক্ষ্য করবে।

উদাহরণ:

```text
Phone Cover       ✅
Phone Case        ✅
Smartphone        ❌
```

---

# 8. Exact Search

```python
search_fields = [
    "=name"
]
```

Request:

```http
?search=iPhone
```

এখানে exact value matching-এর জন্য ব্যবহার করা যায়।

উদাহরণ:

```text
iPhone        ✅
iPhone 15     ❌
```

---

# 9. Regex Search

```python
search_fields = [
    "$name"
]
```

Regex-based matching করা যায়।

কিন্তু বড় production database-এ regex search ব্যবহার করার আগে performance বিবেচনা করা উচিত।

---

# 10. Full-Text Search

```python
search_fields = [
    "@description"
]
```

এটি full-text search-এর জন্য।

তবে এটি database backend-এর উপর নির্ভরশীল। Advanced PostgreSQL search দরকার হলে Django-এর PostgreSQL full-text search tools আলাদাভাবে শেখা ভালো।

---

# 11. DjangoFilterBackend

Search আর filtering এক জিনিস নয়।

ধরো:

```http
?search=phone
```

এটি text search।

অন্যদিকে:

```http
?category=2
```

এটি structured filtering।

তাই:

```python
filter_backends = [
    SearchFilter,
    DjangoFilterBackend,
]
```

---

# 12. Custom FilterSet

`filters.py`:

```python
import django_filters

from .models import Product


class ProductFilter(
    django_filters.FilterSet
):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    class Meta:

        model = Product

        fields = [
            "category",
            "brand",
        ]
```

---

# 13. `min_price` কী করছে?

Request:

```http
?min_price=500
```

আমাদের filter:

```python
min_price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="gte"
)
```

মানে:

```python
price__gte=500
```

অর্থাৎ:

```text
price >= 500
```

---

# 14. `max_price`

```python
max_price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="lte"
)
```

Request:

```http
?max_price=5000
```

মানে:

```python
price__lte=5000
```

অর্থাৎ:

```text
price <= 5000
```

---

# 15. Price Range

একসাথে:

```http
?min_price=500&max_price=5000
```

Conceptually:

```python
Product.objects.filter(
    price__gte=500,
    price__lte=5000
)
```

---

# 16. OrderingFilter

Import:

```python
from rest_framework.filters import OrderingFilter
```

View:

```python
filter_backends = [
    SearchFilter,
    DjangoFilterBackend,
    OrderingFilter,
]
```

Allowed fields:

```python
ordering_fields = [
    "price",
    "name",
    "created_at",
]
```

---

# 17. Ascending

```http
?ordering=price
```

ফলাফল:

```text
500
1000
2000
5000
```

---

# 18. Descending

```http
?ordering=-price
```

ফলাফল:

```text
5000
2000
1000
500
```

`-` মানে descending।

---

# 19. Multiple Ordering

```http
?ordering=-price,name
```

মানে:

```text
প্রথমে price descending
তারপর name ascending
```

---

# 20. Complete Product API

```python
from rest_framework import generics

from rest_framework.filters import (
    SearchFilter,
    OrderingFilter,
)

from django_filters.rest_framework import (
    DjangoFilterBackend
)

from .models import Product

from .serializers import ProductSerializer

from .filters import ProductFilter


class ProductListAPIView(
    generics.ListAPIView
):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]

    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]

    filterset_class = ProductFilter

    ordering_fields = [
        "price",
        "name",
        "created_at",
    ]

    ordering = [
        "-created_at"
    ]
```

---

# 21. এখন Real API Request

```http
GET /api/products/
```

Default ordering হবে:

```text
newest → oldest
```

---

Search:

```http
GET /api/products/?search=iphone
```

---

Category:

```http
GET /api/products/?category=2
```

---

Price:

```http
GET /api/products/?min_price=500
```

---

Price range:

```http
GET /api/products/?min_price=500&max_price=5000
```

---

Ordering:

```http
GET /api/products/?ordering=-price
```

---

সব একসাথে:

```http
GET /api/products/?search=phone&category=2&min_price=500&max_price=5000&ordering=-price
```

---

# 22. Request Flow বুঝে রাখো

এই request:

```http
?search=phone
&category=2
&min_price=500
&max_price=5000
&ordering=-price
```

কে এভাবে চিন্তা করো:

```text
Request
   │
   ├── search=phone
   │       ↓
   │   SearchFilter
   │
   ├── category=2
   │       ↓
   │   DjangoFilterBackend
   │
   ├── min_price=500
   │       ↓
   │   price >= 500
   │
   ├── max_price=5000
   │       ↓
   │   price <= 5000
   │
   └── ordering=-price
           ↓
       OrderingFilter
           │
           ↓
      Final QuerySet
```

এটাই production API-তে খুব common pattern।

---

# 23. SearchFilter বনাম DjangoFilterBackend

এটা interview-এও আসতে পারে।

### SearchFilter

```http
?search=laptop
```

ব্যবহার:

> General text searching

---

### DjangoFilterBackend

```http
?category=2
&brand=Apple
```

ব্যবহার:

> Structured filtering

---

### OrderingFilter

```http
?ordering=-price
```

ব্যবহার:

> Sorting

---

## মনে রাখার সহজ formula

```text
SEARCH
   ↓
SearchFilter

FILTER
   ↓
DjangoFilterBackend

SORT
   ↓
OrderingFilter
```

---

# Lesson 3 Practice 🔥

এই model-এর জন্য SearchFilter configure করো:

```python
class Book(models.Model):

    title = models.CharField(
        max_length=200
    )

    description = models.TextField()

    author = models.ForeignKey(
        Author,
        on_delete=models.CASCADE
    )

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

Search করতে হবে:

```text
title
description
author name
category name
```

সঠিক configuration:

```python
search_fields = [
    "title",
    "description",
    "author__name",
    "category__name",
]
```

এরপর API-তে এই request কাজ করাতে চেষ্টা করো:

```http
/api/books/
?search=python
&category=3
&min_price=300
&max_price=1500
&ordering=-price
```

**Lesson 4-এ** আমরা custom search, `Q()` object দিয়ে complex OR/AND search, custom `FilterSet`, lookup expressions এবং performance optimization দিয়ে SearchFilter mastery শেষ করব।
# Lesson 4 — SearchFilter Mastery: Custom Search + `Q()` + Performance

আজকের Lesson 4-এ আমরা SearchFilter-এর **advanced/production-level concepts** শিখব।

আজকের লক্ষ্য:

```text
SearchFilter
    ↓
Custom search
    ↓
Q()
    ↓
AND / OR logic
    ↓
Custom FilterSet
    ↓
Lookup expressions
    ↓
Performance
    ↓
Production API
```

---

# 1. SearchFilter-এর limitation

`SearchFilter` খুব convenient:

```python
search_fields = [
    "name",
    "description",
    "brand",
]
```

কিন্তু সবসময় business requirement এত simple হয় না।

ধরো requirement:

> User product name অথবা brand-এ search করবে, কিন্তু description-এ search করবে না।

অথবা:

> Search term অবশ্যই name এবং brand-এর যেকোনো একটিতে থাকতে হবে।

অথবা:

> Active products-এর মধ্যে search করতে হবে।

এ ধরনের complex logic-এর জন্য custom queryset logic প্রয়োজন হতে পারে।

---

# 2. `Q()` Object

Django-এর `Q()` object complex query তৈরি করতে ব্যবহার করা হয়।

Import:

```python
from django.db.models import Q
```

ধরো:

```python
Product.objects.filter(
    Q(name__icontains="phone") |
    Q(brand__icontains="phone")
)
```

এখানে:

```text
name contains phone
        OR
brand contains phone
```

---

# 3. `|` = OR

```python
Q(name__icontains="phone") |
Q(brand__icontains="phone")
```

মানে:

```text
name contains phone
OR
brand contains phone
```

---

# 4. `&` = AND

```python
Product.objects.filter(
    Q(name__icontains="phone") &
    Q(brand__icontains="Samsung")
)
```

মানে:

```text
name contains phone
AND
brand contains Samsung
```

---

# 5. `~` = NOT

```python
Product.objects.filter(
    ~Q(brand__icontains="Apple")
)
```

মানে:

```text
brand does NOT contain Apple
```

---

# 6. OR + AND একসাথে

এটা খুব important।

```python
Product.objects.filter(
    (
        Q(name__icontains="phone") |
        Q(description__icontains="phone")
    )
    &
    Q(is_active=True)
)
```

মানে:

```text
(
    name contains phone
    OR
    description contains phone
)
AND
is_active = True
```

এটাই complex search logic।

---

# 7. Custom SearchAPIView

ধরো আমরা SearchFilter ব্যবহার না করে নিজে search করতে চাই।

```python
from rest_framework import generics

from .models import Product
from .serializers import ProductSerializer

from django.db.models import Q


class ProductListAPIView(
    generics.ListAPIView
):

    serializer_class = ProductSerializer

    def get_queryset(self):

        queryset = Product.objects.all()

        search = self.request.query_params.get(
            "search"
        )

        if search:

            queryset = queryset.filter(
                Q(name__icontains=search) |
                Q(brand__icontains=search)
            )

        return queryset
```

এখন:

```http
GET /api/products/?search=phone
```

এটি:

```text
name
OR
brand
```

search করবে।

---

# 8. কিন্তু SearchFilter কেন ব্যবহার করব?

কারণ সাধারণ search-এর জন্য SearchFilter অনেক cleaner।

```python
filter_backends = [
    SearchFilter
]

search_fields = [
    "name",
    "brand",
]
```

এটা দিয়ে যদি requirement পূরণ হয়, তাহলে manually `get_queryset()` লিখে ফেলতে হবে না।

### Rule:

```text
Simple search
    ↓
SearchFilter

Complex business search
    ↓
Custom queryset / custom filter
```

---

# 9. Custom FilterSet

আমরা আগে করেছি:

```python
class ProductFilter(
    django_filters.FilterSet
):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )
```

এখন আরও advanced করি।

---

# 10. `icontains`

ধরো:

```python
name = django_filters.CharFilter(
    lookup_expr="icontains"
)
```

এখন:

```http
?name=phone
```

মানে:

```python
name__icontains="phone"
```

অর্থাৎ case-insensitive contains search।

---

# 11. `iexact`

```python
brand = django_filters.CharFilter(
    lookup_expr="iexact"
)
```

Request:

```http
?brand=apple
```

এটি case-insensitive exact matching করতে পারে:

```text
Apple
apple
APPLE
```

---

# 12. `startswith`

```python
name = django_filters.CharFilter(
    lookup_expr="startswith"
)
```

Request:

```http
?name=iphone
```

মানে:

```python
name__startswith="iphone"
```

---

# 13. `istartswith`

Case-insensitive version:

```python
name = django_filters.CharFilter(
    lookup_expr="istartswith"
)
```

---

# 14. Related Field Filter

এটাও খুব গুরুত্বপূর্ণ।

ধরো:

```python
class ProductFilter(
    django_filters.FilterSet
):

    category_name = django_filters.CharFilter(
        field_name="category__name",
        lookup_expr="icontains"
    )

    class Meta:
        model = Product
        fields = []
```

এখন:

```http
?category_name=elect
```

মানে:

```python
category__name__icontains="elect"
```

---

# 15. Search + Custom Filter

Production API:

```python
class ProductFilter(
    django_filters.FilterSet
):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    category_name = django_filters.CharFilter(
        field_name="category__name",
        lookup_expr="icontains"
    )

    class Meta:
        model = Product

        fields = [
            "brand",
        ]
```

View:

```python
class ProductListAPIView(
    generics.ListAPIView
):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]

    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]

    filterset_class = ProductFilter

    ordering_fields = [
        "price",
        "name",
        "created_at",
    ]

    ordering = [
        "-created_at"
    ]
```

---

# 16. এখন API অনেক powerful

### General search

```http
?search=phone
```

### Brand filter

```http
?brand=Samsung
```

### Category name filter

```http
?category_name=mobile
```

### Minimum price

```http
?min_price=500
```

### Maximum price

```http
?max_price=5000
```

### Sorting

```http
?ordering=-price
```

### সব একসাথে

```http
?search=phone
&brand=Samsung
&category_name=mobile
&min_price=500
&max_price=5000
&ordering=-price
```

---

# 17. SearchFilter-এর performance

এখন সবচেয়ে important production topic।

ধরো:

```python
search_fields = [
    "name",
    "description",
    "brand",
]
```

User:

```http
?search=phone
```

তাহলে multiple fields-এ text matching করতে হবে।

ছোট database:

```text
10,000 rows
```

সমস্যা কম।

কিন্তু:

```text
10 million rows
```

হলে generic substring search expensive হতে পারে।

---

# 18. Database Index

যে field-এ frequently filtering করা হয়, সেখানে appropriate indexing consider করা যায়।

যেমন:

```python
class Product(models.Model):

    brand = models.CharField(
        max_length=100,
        db_index=True
    )
```

এটি সাধারণ equality/filter query-তে useful হতে পারে।

কিন্তু একটা গুরুত্বপূর্ণ point:

**`icontains` search-এর জন্য সাধারণ B-tree index সবসময় যথেষ্ট helpful নয়।**

তাই শুধু `db_index=True` দিলেই search magically fast হয়ে যাবে—এটা ধরে নেওয়া ঠিক নয়।

---

# 19. PostgreSQL Full-Text Search

যদি application বড় হয় এবং sophisticated text search প্রয়োজন হয়, PostgreSQL full-text search বিবেচনা করতে পারো।

Django-তে tools আছে যেমন:

```python
SearchVector
SearchQuery
SearchRank
```

Concept:

```text
Normal SearchFilter
       ↓
Simple API search

PostgreSQL Full Text Search
       ↓
Advanced text search
       ↓
Ranking
       ↓
Large-scale search
```

এটি SearchFilter-এর replacement হিসেবে সবসময় দরকার হয় না; requirement অনুযায়ী ব্যবহার করবে।

---

# 20. `select_related()` ব্যবহার

আমাদের search field:

```python
"category__name"
```

এবং serializer-এও category information দরকার হলে query optimization দরকার হতে পারে।

যেমন:

```python
queryset = Product.objects.select_related(
    "category"
)
```

তারপর:

```python
filter_backends = [
    SearchFilter,
    DjangoFilterBackend,
    OrderingFilter,
]
```

এতে related foreign-key data access-এর ক্ষেত্রে unnecessary queries কমাতে সাহায্য করতে পারে।

---

# 21. `prefetch_related()`

যদি relation হয়:

```text
Product
   ↓
ManyToMany
```

বা reverse relationship, তখন অনেক ক্ষেত্রে:

```python
prefetch_related()
```

ব্যবহার করা হয়।

Rule:

```text
ForeignKey / OneToOne
        ↓
select_related()

ManyToMany / Reverse relation
        ↓
prefetch_related()
```

---

# 22. SearchFilter + Pagination

Production API-তে search-এর সাথে pagination খুব common:

```python
class ProductListAPIView(
    generics.ListAPIView
):

    pagination_class = ProductPagination

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]
```

Request:

```http
?search=phone&page=2
```

Flow:

```text
Search
   ↓
Filter
   ↓
Ordering
   ↓
Pagination
   ↓
Response
```

---

# 23. Complete Production Pattern

একটা clean architecture হতে পারে:

```text
products/
│
├── models.py
│
├── serializers.py
│
├── filters.py
│
├── pagination.py
│
├── views.py
│
└── urls.py
```

### `filters.py`

```python
import django_filters

from .models import Product


class ProductFilter(
    django_filters.FilterSet
):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    category_name = django_filters.CharFilter(
        field_name="category__name",
        lookup_expr="icontains"
    )

    class Meta:
        model = Product

        fields = [
            "brand",
        ]
```

### `views.py`

```python
from django_filters.rest_framework import (
    DjangoFilterBackend
)

from rest_framework.filters import (
    SearchFilter,
    OrderingFilter,
)

from rest_framework import generics

from .models import Product

from .serializers import ProductSerializer

from .filters import ProductFilter


class ProductListAPIView(
    generics.ListAPIView
):

    serializer_class = ProductSerializer

    queryset = Product.objects.select_related(
        "category"
    )

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]

    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]

    filterset_class = ProductFilter

    ordering_fields = [
        "price",
        "name",
        "created_at",
    ]

    ordering = [
        "-created_at"
    ]
```

---

# 24. Final API

এখন তোমার API support করবে:

```http
GET /api/products/
```

```http
GET /api/products/?search=phone
```

```http
GET /api/products/?brand=Samsung
```

```http
GET /api/products/?min_price=500
```

```http
GET /api/products/?max_price=5000
```

```http
GET /api/products/?category_name=mobile
```

```http
GET /api/products/?ordering=-price
```

এবং:

```http
GET /api/products/?search=phone&brand=Samsung&category_name=mobile&min_price=500&max_price=5000&ordering=-price
```

---

# 🔥 SearchFilter Mastery — পুরো 4 Lesson-এর Summary

```text
LESSON 1
│
├── SearchFilter
├── search_fields
└── ?search=
│
↓
LESSON 2
│
├── category__name
├── nested relationship
├── ^ startswith
├── = exact
├── $ regex
└── @ full-text
│
↓
LESSON 3
│
├── SearchFilter
├── DjangoFilterBackend
├── OrderingFilter
├── FilterSet
└── price range
│
↓
LESSON 4
│
├── Q()
├── OR / AND / NOT
├── custom search
├── lookup_expr
├── select_related
├── prefetch_related
├── pagination
└── performance
```

## 🧠 সবচেয়ে গুরুত্বপূর্ণ 5টা জিনিস

```python
# 1. Text search
search_fields = ["name", "description"]


# 2. Related search
search_fields = ["category__name"]


# 3. Structured filtering
filterset_class = ProductFilter


# 4. Sorting
ordering_fields = ["price", "created_at"]


# 5. Complex custom logic
Q(name__icontains=query) |
Q(brand__icontains=query)
```

### Mastery Test

একজন interviewer যদি জিজ্ঞেস করে:

> **"How would you implement a product API where users can search by product name/brand/category, filter by category and price range, sort by price, and paginate the result?"**

তোমার মাথায় এই architecture আসা উচিত:

```text
ListAPIView
    │
    ├── SearchFilter
    │      └── search_fields
    │
    ├── DjangoFilterBackend
    │      └── ProductFilter
    │
    ├── OrderingFilter
    │      └── ordering_fields
    │
    └── Pagination
```

এটাই **DRF Search + Filter-এর practical mastery level**।
অবশ্যই। **DjangoFilter (`DjangoFilterBackend`) আর DRF `SearchFilter`—দুটোই filtering-এর জন্য ব্যবহৃত হয়, কিন্তু তাদের উদ্দেশ্য আলাদা।**

## 1. `SearchFilter` কী?

`SearchFilter` ব্যবহার করা হয় **text search** করার জন্য।

ধরো Product model:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField()
    brand = models.CharField(max_length=100)
```

View:

```python
from rest_framework.filters import SearchFilter

class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [SearchFilter]

    search_fields = [
        "name",
        "description",
        "brand",
    ]
```

এখন:

```http
GET /api/products/?search=iphone
```

এটা খুঁজবে:

```text
name
description
brand
```

এর মধ্যে `iphone` আছে কি না।

### সহজভাবে:

> **SearchFilter = "আমি কিছু খুঁজছি, নাম/description/brand-এর মধ্যে search করো."**

---

# 2. DjangoFilter কী?

এখানে সাধারণত `django-filter` package-এর `DjangoFilterBackend` বোঝানো হচ্ছে।

এটা ব্যবহার করা হয় **structured/field-based filtering** করার জন্য।

যেমন:

```http
GET /api/products/?brand=Apple
```

অথবা:

```http
GET /api/products/?category=2
```

অথবা:

```http
GET /api/products/?min_price=500
```

এখানে user বলছে:

> "এই নির্দিষ্ট condition অনুযায়ী data দাও।"

---

# 3. Basic DjangoFilter Example

```python
import django_filters


class ProductFilter(django_filters.FilterSet):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    class Meta:
        model = Product

        fields = [
            "category",
            "brand",
        ]
```

View:

```python
from django_filters.rest_framework import DjangoFilterBackend


class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend
    ]

    filterset_class = ProductFilter
```

এখন:

```http
?category=2
```

মানে:

```python
Product.objects.filter(category=2)
```

আর:

```http
?min_price=500
```

মানে:

```python
Product.objects.filter(
    price__gte=500
)
```

---

# 4. Main Difference

| বিষয়                 | SearchFilter                  | DjangoFilterBackend                   |
| -------------------- | ----------------------------- | ------------------------------------- |
| Purpose              | Search                        | Filtering                             |
| Query parameter      | `search`                      | Custom field names                    |
| Example              | `?search=phone`               | `?category=2`                         |
| সাধারণত              | Text                          | Structured values                     |
| Multiple text fields | খুব সহজ                       | আলাদা configuration লাগে              |
| Price range          | সাধারণ SearchFilter-এর কাজ নয় | খুব ভালো                              |
| Exact category       | Search-এর উদ্দেশ্য নয়         | খুব ভালো                              |
| Related field        | `category__name`              | `category__name` দিয়েও filter করা যায় |
| Package              | DRF built-in                  | `django-filter` package               |

---

# 5. একটা Real Example

ধরো database:

| Name        | Brand   | Category |  Price |
| ----------- | ------- | -------- | -----: |
| iPhone 15   | Apple   | Mobile   |  70000 |
| iPhone 14   | Apple   | Mobile   |  60000 |
| Galaxy A55  | Samsung | Mobile   |  45000 |
| MacBook Air | Apple   | Laptop   | 100000 |

### SearchFilter

```http
?search=iphone
```

Result:

```text
iPhone 15
iPhone 14
```

কারণ user **text search** করছে।

---

### DjangoFilter

```http
?brand=Apple
```

Result:

```text
iPhone 15
iPhone 14
MacBook Air
```

কারণ user বলছে:

> brand অবশ্যই Apple হতে হবে।

---

### Price filter

```http
?min_price=50000
```

Result:

```text
iPhone 15
iPhone 14
MacBook Air
```

কারণ:

```text
price >= 50000
```

---

# 6. দুটো একসাথে ব্যবহার করা যায়

এটাই production API-তে খুব common।

```python
from rest_framework.filters import SearchFilter
from django_filters.rest_framework import DjangoFilterBackend


class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
    ]

    search_fields = [
        "name",
        "description",
        "brand",
    ]

    filterset_class = ProductFilter
```

এখন:

```http
/api/products/?search=iphone&brand=Apple&min_price=50000
```

এখানে:

```text
search=iphone
       ↓
SearchFilter

brand=Apple
       ↓
DjangoFilter

min_price=50000
       ↓
DjangoFilter
```

অর্থাৎ:

```text
Search
+
Filter
=
Powerful Product API
```

---

# 7. সবচেয়ে সহজে মনে রাখার উপায়

### SearchFilter

User বলে:

> **"phone খুঁজে দাও"**

```http
?search=phone
```

### DjangoFilter

User বলে:

> **"category 2-এর products দাও"**

```http
?category=2
```

User বলে:

> **"500 থেকে 5000 টাকার মধ্যে products দাও"**

```http
?min_price=500&max_price=5000
```

---

## 🔥 One-line Difference

> **SearchFilter হলো "text-এর মধ্যে খোঁজা", আর DjangoFilter হলো "নির্দিষ্ট field/condition অনুযায়ী data filter করা।"**

আর একটা important distinction:

```text
SearchFilter
    ↓
"Search"

DjangoFilterBackend
    ↓
"Filter"

OrderingFilter
    ↓
"Sort"
```

এই তিনটার relationship পরিষ্কার থাকলে DRF-এর list API design অনেক সহজ হয়ে যাবে।
হ্যাঁ। **একই API endpoint-এ `SearchFilter + DjangoFilterBackend + OrderingFilter` একসাথে ব্যবহার করা যায়।** Frontend থেকে শুধু query parameters পাঠাবে।

ধরো endpoint:

```text
GET /api/products/
```

## 1. Backend

### `filters.py`

```python
import django_filters

from .models import Product


class ProductFilter(django_filters.FilterSet):

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    class Meta:
        model = Product
        fields = [
            "category",
            "brand",
        ]
```

### `views.py`

```python
from rest_framework import generics
from rest_framework.filters import (
    SearchFilter,
    OrderingFilter,
)
from django_filters.rest_framework import (
    DjangoFilterBackend,
)

from .models import Product
from .serializers import ProductSerializer
from .filters import ProductFilter


class ProductListAPIView(generics.ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        SearchFilter,
        DjangoFilterBackend,
        OrderingFilter,
    ]

    # SearchFilter
    search_fields = [
        "name",
        "description",
        "brand",
        "category__name",
    ]

    # DjangoFilterBackend
    filterset_class = ProductFilter

    # OrderingFilter
    ordering_fields = [
        "price",
        "name",
        "created_at",
    ]

    ordering = ["-created_at"]
```

---

# 2. এখন একই API

একটা endpoint:

```text
/api/products/
```

কিন্তু query parameter অনুযায়ী কাজ আলাদা হবে।

### শুধু Search

```text
/api/products/?search=iphone
```

```text
search=iphone
       ↓
SearchFilter
```

---

### শুধু Category Filter

```text
/api/products/?category=2
```

```text
category=2
       ↓
DjangoFilterBackend
```

---

### শুধু Sorting

```text
/api/products/?ordering=-price
```

```text
ordering=-price
       ↓
OrderingFilter
```

---

# 3. Frontend থেকে সব একসাথে

ধরো user frontend-এ:

* Search: `phone`
* Category: `2`
* Brand: `Samsung`
* Min price: `500`
* Max price: `5000`
* Sort: highest price

তাহলে frontend থেকে request হবে:

```text
/api/products/?search=phone&category=2&brand=Samsung&min_price=500&max_price=5000&ordering=-price
```

Backend automatically বুঝবে:

```text
search=phone
    ↓
SearchFilter

category=2
brand=Samsung
min_price=500
max_price=5000
    ↓
DjangoFilterBackend

ordering=-price
    ↓
OrderingFilter
```

---

# 4. React থেকে `fetch`

সবচেয়ে simple way:

```javascript
const response = await fetch(
  "http://localhost:8000/api/products/?search=phone&category=2&brand=Samsung&min_price=500&max_price=5000&ordering=-price"
);

const data = await response.json();

console.log(data);
```

কিন্তু এভাবে URL manually বানানো ভালো practice না।

---

# 5. React-এ `URLSearchParams` ব্যবহার করো ⭐

```javascript
const params = new URLSearchParams();

params.append("search", "phone");
params.append("category", "2");
params.append("brand", "Samsung");
params.append("min_price", "500");
params.append("max_price", "5000");
params.append("ordering", "-price");

const response = await fetch(
  `http://localhost:8000/api/products/?${params.toString()}`
);

const data = await response.json();
```

এতে তৈরি হবে:

```text
/api/products/
?search=phone
&category=2
&brand=Samsung
&min_price=500
&max_price=5000
&ordering=-price
```

---

# 6. আরও ভালো — Object থেকে Dynamic Query

Frontend-এ সাধারণত filter state থাকবে:

```javascript
const filters = {
  search: "phone",
  category: 2,
  brand: "Samsung",
  min_price: 500,
  max_price: 5000,
  ordering: "-price",
};
```

তারপর:

```javascript
const params = new URLSearchParams();

Object.entries(filters).forEach(([key, value]) => {
  if (value !== "" && value !== null && value !== undefined) {
    params.append(key, value);
  }
});

const response = await fetch(
  `http://localhost:8000/api/products/?${params.toString()}`
);

const data = await response.json();
```

এটাই অনেক practical approach।

---

# 7. User শুধু Search করলে

ধরো:

```javascript
const filters = {
  search: "iphone",
  category: "",
  brand: "",
  min_price: "",
  max_price: "",
  ordering: "",
};
```

তাহলে request হবে:

```text
/api/products/?search=iphone
```

কারণ empty values আমরা বাদ দিয়েছি।

---

# 8. User শুধু Category select করলে

```javascript
const filters = {
  search: "",
  category: 2,
  brand: "",
  min_price: "",
  max_price: "",
  ordering: "",
};
```

Request:

```text
/api/products/?category=2
```

---

# 9. User Search + Sort করলে

```javascript
const filters = {
  search: "phone",
  ordering: "-price",
};
```

Request:

```text
/api/products/?search=phone&ordering=-price
```

---

# 10. React UI Example

ধরো frontend:

```text
┌────────────────────────────────────┐
│ Search: [ iphone              ]    │
│                                    │
│ Category: [ Mobile ▼ ]             │
│ Brand:    [ Apple ▼ ]              │
│                                    │
│ Min Price: [ 500  ]                │
│ Max Price: [ 5000 ]                │
│                                    │
│ Sort: [ Price: High → Low ▼ ]      │
└────────────────────────────────────┘
```

State:

```javascript
const [filters, setFilters] = useState({
  search: "",
  category: "",
  brand: "",
  min_price: "",
  max_price: "",
  ordering: "",
});
```

যখন user search করবে:

```javascript
setFilters({
  ...filters,
  search: "iphone",
});
```

Category select:

```javascript
setFilters({
  ...filters,
  category: 2,
});
```

Sort:

```javascript
setFilters({
  ...filters,
  ordering: "-price",
});
```

তারপর API call:

```javascript
const fetchProducts = async () => {

  const params = new URLSearchParams();

  Object.entries(filters).forEach(
    ([key, value]) => {

      if (
        value !== "" &&
        value !== null &&
        value !== undefined
      ) {
        params.append(key, value);
      }

    }
  );

  const response = await fetch(
    `http://localhost:8000/api/products/?${params.toString()}`
  );

  const data = await response.json();

  return data;
};
```

---

# 11. Axios হলে আরও সুন্দর

তুমি যেহেতু React/Next.js ব্যবহার করো, Axios দিয়ে:

```javascript
import axios from "axios";

const fetchProducts = async () => {

  const response = await axios.get(
    "http://localhost:8000/api/products/",
    {
      params: {
        search: "phone",
        category: 2,
        brand: "Samsung",
        min_price: 500,
        max_price: 5000,
        ordering: "-price",
      },
    }
  );

  console.log(response.data);
};
```

Axios নিজেই URL বানিয়ে দেবে:

```text
/api/products/
?search=phone
&category=2
&brand=Samsung
&min_price=500
&max_price=5000
&ordering=-price
```

### ⭐ আমি frontend-এ এই approach recommend করব:

```javascript
axios.get("/api/products/", {
  params: {
    search,
    category,
    brand,
    min_price,
    max_price,
    ordering,
  },
});
```

---

# 12. সবচেয়ে গুরুত্বপূর্ণ Concept

তোমার **API endpoint একটাই**:

```text
GET /api/products/
```

তুমি endpoint change করছো না।

শুধু query parameters change করছো:

```text
                    /api/products/
                           │
        ┌──────────────────┼─────────────────┐
        ↓                  ↓                 ↓
     search             filters           ordering
        ↓                  ↓                 ↓
   SearchFilter      DjangoFilter      OrderingFilter
```

তাই frontend থেকে:

```javascript
axios.get("/api/products/", {
  params: {
    search: "phone",
    category: 2,
    min_price: 500,
    max_price: 5000,
    ordering: "-price",
  },
});
```

**এই একটা request-এই তিনটা backend feature একসাথে কাজ করবে।**
হ্যাঁ, **frontend থেকে `params` হিসেবে pass করাই সবচেয়ে clean এবং recommended way**, বিশেষ করে Axios ব্যবহার করলে।

### Axios

```javascript
axios.get("/api/products/", {
  params: {
    search: "phone",
    category: 2,
    brand: "Samsung",
    min_price: 500,
    max_price: 5000,
    ordering: "-price",
  },
});
```

Axios এটাকে automatically বানাবে:

```text
/api/products/
?search=phone
&category=2
&brand=Samsung
&min_price=500
&max_price=5000
&ordering=-price
```

Backend-এ:

```text
search
   ↓
SearchFilter

category
brand
min_price
max_price
   ↓
DjangoFilterBackend

ordering
   ↓
OrderingFilter
```

### React state থেকে

আরও বাস্তবে:

```javascript
const [filters, setFilters] = useState({
  search: "",
  category: "",
  brand: "",
  min_price: "",
  max_price: "",
  ordering: "",
});
```

API call:

```javascript
axios.get("/api/products/", {
  params: filters,
});
```

এটাই মূল concept:

> **Frontend → `params` → Backend query parameters → DRF filters**

তোমাকে manually URL বানাতে হবে না।
