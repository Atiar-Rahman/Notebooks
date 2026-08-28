

তুমি DRF ভালোই জানো, তাই আমি **production-level** ভাবে শেখাবো। ৪টি লেসন শেষে তুমি যেকোনো API-তে filtering confidently implement করতে পারবে।

---

# Django Filter Mastery

## Lesson 1 — Introduction & Setup

### Django Filter কী?

`django-filter` হলো Django/DRF-এর official filtering package।

Without Filter:

```
GET /products/
```

সব product return করবে।

Filter ব্যবহার করলে

```
GET /products/?category=mobile
```

শুধু mobile category return করবে।

আরও example

```
GET /products/?price=1000

GET /products/?brand=Apple

GET /products/?is_active=true
```

---

## Installation

```bash
pip install django-filter
```

requirements.txt

```
django-filter==25.1
```

---

## settings.py

```python
INSTALLED_APPS = [
    ...
    "django_filters",
]
```

---

## DRF Settings

```python
REST_FRAMEWORK = {
    "DEFAULT_FILTER_BACKENDS": [
        "django_filters.rest_framework.DjangoFilterBackend",
    ]
}
```

এখন project-wide filter enable হয়ে গেল।

---

## Example Model

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    category = models.CharField(max_length=100)
    brand = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()
    is_active = models.BooleanField(default=True)
```

---

## Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = "__all__"
```

---

## View

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductListAPIView(ListAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,
    ]

    filterset_fields = [
        "category",
        "brand",
        "is_active",
    ]
```

---

## Test

### Category

```
GET /products/?category=Laptop
```

---

### Brand

```
GET /products/?brand=Apple
```

---

### Boolean

```
GET /products/?is_active=true
```

---

### Multiple Filter

```
GET /products/?category=Laptop&brand=Apple
```

SQL

```sql
WHERE
category='Laptop'
AND
brand='Apple'
```

---

## Generated SQL

Python

```python
Product.objects.filter(
    category="Laptop",
    brand="Apple",
)
```

DRF automatically এই query execute করবে।

---

## Common Mistakes

### ❌ Forgot App

```python
INSTALLED_APPS = [
]
```

Error

```
No module named django_filters
```

---

### ❌ Forgot Backend

```python
filterset_fields = [
    "category"
]
```

কিন্তু

```python
filter_backends = [
]
```

Filtering কাজ করবে না।

---

### ❌ Wrong Field

```
GET /products/?categories=Laptop
```

Model-এ field হলো

```
category
```

তাই result আসবে না।

---

## Best Practice

Global backend use করো

```python
REST_FRAMEWORK = {
    "DEFAULT_FILTER_BACKENDS": [
        "django_filters.rest_framework.DjangoFilterBackend",
    ]
}
```

তারপর View-এ শুধু

```python
filterset_fields = [
    "category",
    "brand",
]
```

---

## Project Exercise

নিচের API তৈরি করো।

```
GET /products/?category=Shoes
```

```
GET /products/?brand=Nike
```

```
GET /products/?is_active=true
```

```
GET /products/?category=Shoes&brand=Nike
```

---

# Lesson 2 — Filtering with Relationships

এখানে শিখবে:

* ForeignKey filtering
* ManyToMany filtering
* Slug filtering
* Nested relationship filtering
* Production examples

---

# Lesson 3 — Custom FilterSet

এখানে শিখবে:

* `FilterSet` class
* `NumberFilter`
* `CharFilter`
* `BooleanFilter`
* `DateFilter`
* `DateFromToRangeFilter`
* `Lookup Expressions`

---

# Lesson 4 — Advanced & Production Filtering

শেষ লেসনে শিখবে:

* Price Range Filter
* Date Range Filter
* Custom Method Filter
* Dynamic Filter
* Search + Ordering + Django Filter একসাথে ব্যবহার
* E-commerce production filtering (category, brand, price, stock, rating, availability)

এই ৪টি লেসন শেষ করলে তুমি **production-grade DRF filtering** implement করতে পারবে।

# Django Filter Mastery — Lesson 2

## Filtering with Relationships (ForeignKey, ManyToMany, Reverse Relations)

আগের লেসনে আমরা simple fields (`category`, `brand`, `is_active`) filter করেছি।

Production project-এ বেশিরভাগ সময় relationship-এর উপর filter করতে হয়।

যেমন:

* Category অনুযায়ী Product
* Seller অনুযায়ী Product
* Tag অনুযায়ী Product
* Company অনুযায়ী Employee
* Author অনুযায়ী Book

আজ এগুলো শিখব।

---

# Example Project

ধরি আমাদের E-commerce project আছে।

## Category

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)

    def __str__(self):
        return self.name
```

---

## Brand

```python
class Brand(models.Model):
    name = models.CharField(max_length=100)

    def __str__(self):
        return self.name
```

---

## Tag

```python
class Tag(models.Model):
    name = models.CharField(max_length=100)

    def __str__(self):
        return self.name
```

---

## Product

```python
class Product(models.Model):
    name = models.CharField(max_length=200)

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE,
        related_name="products"
    )

    brand = models.ForeignKey(
        Brand,
        on_delete=models.CASCADE,
        related_name="products"
    )

    tags = models.ManyToManyField(
        Tag,
        related_name="products"
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

---

# View

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductListAPIView(ListAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,
    ]
```

---

# 1. ForeignKey Filter

Category id দিয়ে filter

```python
filterset_fields = [
    "category",
]
```

API

```
GET /products/?category=2
```

SQL

```sql
WHERE category_id = 2
```

Equivalent ORM

```python
Product.objects.filter(category=2)
```

---

# 2. Brand Filter

```python
filterset_fields = [
    "brand",
]
```

API

```
GET /products/?brand=5
```

ORM

```python
Product.objects.filter(
    brand=5
)
```

---

# 3. Multiple ForeignKey Filter

```python
filterset_fields = [
    "category",
    "brand",
]
```

API

```
GET /products/?category=2&brand=3
```

ORM

```python
Product.objects.filter(
    category=2,
    brand=3
)
```

---

# 4. Filter by Related Field

অনেক সময় id না, related model-এর field দিয়ে filter করতে হয়।

যেমন:

```
Category

id=1

name="Laptop"

slug="laptop"
```

আমরা slug দিয়ে filter করতে চাই।

এর জন্য `FilterSet` ব্যবহার করতে হয় (Lesson 3-এ বিস্তারিত), তবে ধারণা হিসেবে:

```python
class ProductFilter(FilterSet):

    category = CharFilter(
        field_name="category__slug",
        lookup_expr="exact"
    )

    class Meta:
        model = Product
        fields = ["category"]
```

View

```python
filterset_class = ProductFilter
```

API

```
GET /products/?category=laptop
```

ORM

```python
Product.objects.filter(
    category__slug="laptop"
)
```

---

# 5. Filter Using Category Name

```python
category = CharFilter(
    field_name="category__name"
)
```

API

```
GET /products/?category=Electronics
```

ORM

```python
Product.objects.filter(
    category__name="Electronics"
)
```

---

# 6. ManyToMany Filter

Product-এর অনেক Tag আছে।

```
Laptop

Tags

Gaming

SSD

Intel
```

Filter

```python
filterset_fields = [
    "tags",
]
```

API

```
GET /products/?tags=4
```

ORM

```python
Product.objects.filter(
    tags=4
)
```

---

# 7. ManyToMany by Name

Tag name দিয়ে filter

```python
class ProductFilter(FilterSet):

    tag = CharFilter(
        field_name="tags__name"
    )

    class Meta:
        model = Product
        fields = ["tag"]
```

API

```
GET /products/?tag=Gaming
```

ORM

```python
Product.objects.filter(
    tags__name="Gaming"
)
```

---

# 8. Reverse Relation Filter

Category Model

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
```

Product

```python
category = models.ForeignKey(
    Category,
    related_name="products",
    on_delete=models.CASCADE
)
```

Category API-তে filter করতে চাই, যেসব category-তে Apple brand-এর product আছে।

```python
Category.objects.filter(
    products__brand=1
)
```

এখানে `products` এসেছে `related_name` থেকে।

---

# 9. Nested Relationship

ধরি

```
Company

↓

Seller

↓

Product
```

Models

```python
class Company(models.Model):
    name = models.CharField(max_length=100)


class Seller(models.Model):
    company = models.ForeignKey(
        Company,
        on_delete=models.CASCADE
    )


class Product(models.Model):
    seller = models.ForeignKey(
        Seller,
        on_delete=models.CASCADE
    )
```

Filter

```python
Product.objects.filter(
    seller__company=1
)
```

API (FilterSet ব্যবহার করে)

```
GET /products/?company=1
```

---

# 10. Multiple Relationship

```python
Product.objects.filter(
    category__slug="laptop",
    brand__name="Apple",
)
```

Equivalent API

```
GET /products/?category=laptop&brand=Apple
```

---

# Real Production Example

E-commerce

```
GET /products/

?category=laptop

&brand=Apple

&tag=Gaming
```

Equivalent ORM

```python
Product.objects.filter(
    category__slug="laptop",
    brand__name="Apple",
    tags__name="Gaming"
)
```

---

# Common Mistakes

## ❌ Wrong

```
GET /products/?category=Laptop
```

যদি `filterset_fields = ["category"]` হয়, তাহলে এটি `category_id` খুঁজবে, `category.name` নয়।

---

## ✅ Correct

```
GET /products/?category=1
```

অথবা `FilterSet` ব্যবহার করে

```
GET /products/?category=laptop
```

---

## ❌ Wrong Lookup

```python
Product.objects.filter(
    category="Laptop"
)
```

ForeignKey field string accept করবে না (যদি primary key string না হয়)।

---

## ✅ Correct

```python
Product.objects.filter(
    category__name="Laptop"
)
```

---

# Best Practice

* `filterset_fields` ব্যবহার করো যখন primary key বা simple field দিয়ে filter করবে।
* Related model-এর `name`, `slug`, `email` ইত্যাদি দিয়ে filter করতে হলে `FilterSet` ব্যবহার করো।
* Public API-তে `slug` ব্যবহার করা `id`-এর চেয়ে বেশি user-friendly এবং SEO-friendly।

---

# Practice

নিচের API-গুলো implement করার চেষ্টা করো:

```text
GET /products/?category=1
```

```text
GET /products/?brand=2
```

```text
GET /products/?tags=3
```

```text
GET /products/?category=laptop
```

```text
GET /products/?brand=Apple
```

```text
GET /products/?tag=Gaming
```

### আগামী Lesson 3-এ শিখবে `FilterSet` সম্পূর্ণভাবে:

* `filterset_class`
* `CharFilter`
* `NumberFilter`
* `BooleanFilter`
* `DateFilter`
* `ModelChoiceFilter`
* `lookup_expr`
* Custom filters (production-ready)

# Django Filter Mastery — Lesson 3

# FilterSet Complete Guide (Production Level)

আগের দুই লেসনে আমরা `filterset_fields` ব্যবহার করেছি।

এটা ছোট project-এর জন্য ভালো।

কিন্তু Production Project-এ সবাই `FilterSet` ব্যবহার করে।

কারণ এতে তুমি—

* Custom filter বানাতে পারবে
* Range filter করতে পারবে
* Date filter করতে পারবে
* Slug filter করতে পারবে
* Multiple lookup ব্যবহার করতে পারবে
* Complex business logic লিখতে পারবে

---

# Why FilterSet?

আগে আমরা লিখেছিলাম

```python
filterset_fields = [
    "category",
    "brand",
]
```

এতে শুধু equality filter হয়।

```
category = 1
```

কিন্তু যদি চাই

```
price > 500
```

বা

```
price < 1000
```

বা

```
name contains iphone
```

তাহলে `FilterSet` লাগবে।

---

# Create filters.py

Project Structure

```
products/

    filters.py

    models.py

    views.py

    serializers.py
```

---

# Product Model

```python
from django.db import models


class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)


class Product(models.Model):
    name = models.CharField(max_length=200)

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.IntegerField()

    is_active = models.BooleanField(default=True)

    created_at = models.DateTimeField(auto_now_add=True)
```

---

# Basic FilterSet

```python
import django_filters

from .models import Product


class ProductFilter(django_filters.FilterSet):

    class Meta:

        model = Product

        fields = [
            "category",
            "is_active",
        ]
```

---

View

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,
    ]

    filterset_class = ProductFilter
```

---

API

```
GET /products/?category=2
```

---

# CharFilter

Search by name

```python
class ProductFilter(FilterSet):

    name = django_filters.CharFilter()

    class Meta:

        model = Product

        fields = [
            "name",
        ]
```

API

```
GET /products/?name=iPhone
```

ORM

```python
Product.objects.filter(
    name="iPhone"
)
```

---

# contains Lookup

Production-এ exact match কম লাগে।

আমরা লিখি

```python
name = django_filters.CharFilter(
    lookup_expr="icontains"
)
```

API

```
GET /products/?name=phone
```

ORM

```python
Product.objects.filter(
    name__icontains="phone"
)
```

Return করবে

```
iPhone 15

Phone Cover

Gaming Phone
```

---

# NumberFilter

Price

```python
price = django_filters.NumberFilter()
```

API

```
GET /products/?price=500
```

---

# Greater Than

```python
price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="gt"
)
```

API

```
GET /products/?price=1000
```

ORM

```python
Product.objects.filter(
    price__gt=1000
)
```

---

# Less Than

```python
price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="lt"
)
```

```
GET /products/?price=500
```

---

# Greater Than or Equal

```python
price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="gte"
)
```

```
GET /products/?price=500
```

---

# Less Than or Equal

```python
price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="lte"
)
```

---

# BooleanFilter

```python
is_active = django_filters.BooleanFilter()
```

API

```
GET /products/?is_active=true
```

ORM

```python
Product.objects.filter(
    is_active=True
)
```

---

# DateFilter

Suppose

```
created_at
```

Filter

```python
created_after = django_filters.DateFilter(
    field_name="created_at",
    lookup_expr="gte"
)
```

API

```
GET /products/?created_after=2026-07-01
```

---

# Date Range

```python
created_before = django_filters.DateFilter(
    field_name="created_at",
    lookup_expr="lte"
)
```

API

```
GET /products/

?created_after=2026-07-01

&created_before=2026-07-10
```

---

# ModelChoiceFilter

Category slug দিয়ে filter

```python
category = django_filters.ModelChoiceFilter(
    field_name="category",
    queryset=Category.objects.all()
)
```

সাধারণত ID-এর জন্য এটি ব্যবহার করা হয়। যদি slug দিয়ে filter করতে চাও, তাহলে নিচের `CharFilter` পদ্ধতি আরও উপযুক্ত।

---

# Slug Filter

Production-এ সবচেয়ে common

```python
category = django_filters.CharFilter(
    field_name="category__slug",
    lookup_expr="exact"
)
```

API

```
GET /products/?category=laptop
```

ORM

```python
Product.objects.filter(
    category__slug="laptop"
)
```

---

# Multiple Filters

```python
class ProductFilter(FilterSet):

    name = django_filters.CharFilter(
        lookup_expr="icontains"
    )

    category = django_filters.CharFilter(
        field_name="category__slug"
    )

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    is_active = django_filters.BooleanFilter()

    class Meta:

        model = Product

        fields = []
```

API

```
GET /products/

?category=laptop

&name=pro

&min_price=500

&max_price=2000

&is_active=true
```

ORM

```python
Product.objects.filter(

    category__slug="laptop",

    name__icontains="pro",

    price__gte=500,

    price__lte=2000,

    is_active=True
)
```

---

# Lookup Expressions

সবচেয়ে বেশি ব্যবহৃত lookup

| Lookup     | Meaning                   | Example       |
| ---------- | ------------------------- | ------------- |
| exact      | Equal                     | `price=500`   |
| iexact     | Case-insensitive equal    | `name=iphone` |
| contains   | Contains                  | `name=Phone`  |
| icontains  | Case-insensitive contains | `name=phone`  |
| startswith | Starts with               | `iP`          |
| endswith   | Ends with                 | `Pro`         |
| gt         | Greater than              | `price>100`   |
| gte        | Greater than or equal     | `price>=100`  |
| lt         | Less than                 | `price<100`   |
| lte        | Less than or equal        | `price<=100`  |
| in         | Value in list             | `1,2,3`       |
| range      | Between two values        | `100-500`     |

---

# Production Example

Amazon-এর মতো Filter

```
GET /products/

?category=laptop

&name=hp

&min_price=400

&max_price=1200

&is_active=true
```

একটি API call-এ user category, name, price range এবং active status অনুযায়ী product filter করতে পারবে।

---

# Best Practices

✅ `filterset_fields` ব্যবহার করো যখন filtering খুব simple।

✅ Production API-তে সবসময় `filterset_class` ব্যবহার করো।

✅ URL-এ `slug` ব্যবহার করা `id`-এর চেয়ে user-friendly।

✅ Filter-এর নাম descriptive রাখো, যেমন `min_price`, `max_price`, `created_after`, `created_before`।

---

# Practice

নিচের FilterSet নিজে বানাও:

```
GET /products/?name=iphone
```

```
GET /products/?category=mobile
```

```
GET /products/?min_price=500
```

```
GET /products/?max_price=5000
```

```
GET /products/?is_active=true
```

```
GET /products/?created_after=2026-07-01
```

```
GET /products/?created_before=2026-07-10
```

---

## Lesson 4 Preview (Advanced & Production)

পরের লেসনে আমরা শিখব:

* `BaseInFilter` (`?ids=1,2,3`)
* `RangeFilter`
* `DateFromToRangeFilter`
* Custom Method Filter
* Dynamic Filter
* Search + Ordering + Django Filter একসাথে ব্যবহার
* E-commerce production filtering (price, rating, stock, availability, category, brand)
# Django Filter Mastery — Lesson 4

# Advanced & Production Filtering

এখন পর্যন্ত তুমি শিখেছো:

* ✅ `filterset_fields`
* ✅ `FilterSet`
* ✅ `CharFilter`
* ✅ `NumberFilter`
* ✅ `BooleanFilter`
* ✅ `DateFilter`

এখন আমরা Production-level filtering শিখবো।

---

# Final Architecture

```text
Request

↓

Filter Backend

↓

ProductFilter

↓

QuerySet

↓

Database

↓

Response
```

---

# 1. BaseInFilter (Multiple IDs)

ধরো user একসাথে অনেক category filter করতে চায়।

```
Category

1

2

5
```

API

```text
GET /products/?categories=1,2,5
```

---

## Filter

```python
import django_filters


class NumberInFilter(
    django_filters.BaseInFilter,
    django_filters.NumberFilter,
):
    pass
```

---

```python
class ProductFilter(FilterSet):

    categories = NumberInFilter(
        field_name="category",
        lookup_expr="in"
    )

    class Meta:
        model = Product
        fields = []
```

---

ORM

```python
Product.objects.filter(
    category__in=[1,2,5]
)
```

---

SQL

```sql
WHERE category_id IN (1,2,5)
```

---

# 2. Multiple Brand Filter

```
GET /products/?brands=1,3,7
```

```python
brands = NumberInFilter(
    field_name="brand",
    lookup_expr="in"
)
```

---

# 3. RangeFilter

Price Between

```
500

↓

1000
```

Filter

```python
price = django_filters.RangeFilter()
```

API

```
GET /products/?price_min=500&price_max=1000
```

Equivalent ORM

```python
Product.objects.filter(
    price__range=(500,1000)
)
```

> নোট: `RangeFilter`-এর parameter naming একটু ভিন্ন হতে পারে। Production-এ অনেক developer `min_price` এবং `max_price` নামে দুটি `NumberFilter(gte/lte)` ব্যবহার করেন কারণ এটি API-কে আরও readable করে।

---

# 4. DateFromToRangeFilter

Filter

```python
created = django_filters.DateFromToRangeFilter(
    field_name="created_at"
)
```

API

```
GET /products/

?created_after=2026-01-01

&created_before=2026-02-01
```

---

# 5. OrderingFilter

User price অনুযায়ী sort করবে।

Filter

```python
ordering = django_filters.OrderingFilter(

    fields=(

        ("price", "price"),

        ("created_at", "created"),

        ("name", "name"),

    )
)
```

---

API

Ascending

```
GET /products/?ordering=price
```

Descending

```
GET /products/?ordering=-price
```

Newest

```
GET /products/?ordering=-created
```

Alphabetical

```
GET /products/?ordering=name
```

---

# 6. Custom Method Filter

সবচেয়ে powerful feature।

ধরি

```
?available=true
```

মানে

```
stock > 0
```

---

Filter

```python
class ProductFilter(FilterSet):

    available = django_filters.BooleanFilter(
        method="filter_available"
    )

    class Meta:

        model = Product

        fields = []

    def filter_available(
        self,
        queryset,
        name,
        value
    ):

        if value:

            return queryset.filter(
                stock__gt=0
            )

        return queryset
```

---

API

```
GET /products/?available=true
```

ORM

```python
Product.objects.filter(
    stock__gt=0
)
```

---

# 7. Rating Filter

```
?rating=4
```

```python
rating = django_filters.NumberFilter(
    lookup_expr="gte"
)
```

API

```
GET /products/?rating=4
```

ORM

```python
Product.objects.filter(
    rating__gte=4
)
```

---

# 8. Discounted Product

Suppose

```python
discount_price
```

exists.

Filter

```python
discount = django_filters.BooleanFilter(
    method="filter_discount"
)
```

```python
def filter_discount(
    self,
    queryset,
    name,
    value
):

    if value:

        return queryset.exclude(
            discount_price=None
        )

    return queryset
```

---

# 9. Search + Filter + Ordering Together

Production API

```text
GET /products/

?name=iphone

&category=mobile

&min_price=500

&max_price=1500

&available=true

&ordering=-price
```

একটি request-এ

* Search
* Category
* Price
* Availability
* Sorting

সব হবে।

---

# View

```python
from django_filters.rest_framework import DjangoFilterBackend
from rest_framework.filters import SearchFilter
from rest_framework.filters import OrderingFilter


class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [

        DjangoFilterBackend,

        SearchFilter,

        OrderingFilter,

    ]

    filterset_class = ProductFilter

    search_fields = [

        "name",

        "description",

    ]

    ordering_fields = [

        "price",

        "created_at",

        "rating",

    ]
```

---

# API Examples

Search

```
GET /products/?search=iphone
```

Ordering

```
GET /products/?ordering=-price
```

Filter

```
GET /products/?category=laptop
```

Everything

```
GET /products/

?search=mac

&category=laptop

&min_price=1000

&max_price=5000

&ordering=-rating
```

---

# 10. Complete Production Filter

```python
import django_filters


class ProductFilter(django_filters.FilterSet):

    name = django_filters.CharFilter(
        lookup_expr="icontains"
    )

    category = django_filters.CharFilter(
        field_name="category__slug"
    )

    brand = django_filters.CharFilter(
        field_name="brand__name"
    )

    min_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="gte"
    )

    max_price = django_filters.NumberFilter(
        field_name="price",
        lookup_expr="lte"
    )

    available = django_filters.BooleanFilter(
        method="filter_available"
    )

    class Meta:

        model = Product

        fields = []

    def filter_available(
        self,
        queryset,
        name,
        value
    ):

        if value:
            return queryset.filter(stock__gt=0)

        return queryset
```

---

# Production API

```
GET /products/

?name=iphone

&category=mobile

&brand=Apple

&min_price=500

&max_price=2000

&available=true
```

Equivalent ORM

```python
Product.objects.filter(

    name__icontains="iphone",

    category__slug="mobile",

    brand__name="Apple",

    price__gte=500,

    price__lte=2000,

    stock__gt=0

)
```

---

# Common Mistakes

### ❌ Mistake 1

```python
lookup_expr="great"
```

Correct

```python
lookup_expr="gte"
```

---

### ❌ Mistake 2

```python
field_name="categories"
```

Model field

```python
category
```

---

### ❌ Mistake 3

```python
category__slug
```

কিন্তু Model-এ slug নেই।

---

### ❌ Mistake 4

`SearchFilter` আর `django-filter`-কে একই কাজের জন্য ব্যবহার করা।

* `SearchFilter` → keyword search (`search=iphone`)
* `django-filter` → exact/range/business filtering (`category`, `price`, `available`)

---

# Best Practices

✅ `filters.py` আলাদা ফাইলে রাখো।

✅ `filterset_class` ব্যবহার করো, `filterset_fields` নয়, যখন API বড় হবে।

✅ ForeignKey-এর জন্য `slug` বা অন্য human-readable field expose করো।

✅ `min_price` / `max_price` naming ব্যবহার করো।

✅ Business logic (`available`, `discount`, `featured`) `method=` filter দিয়ে implement করো।

✅ `SearchFilter`, `OrderingFilter` এবং `DjangoFilterBackend` একসাথে ব্যবহার করো।

---

# Real E-commerce Example

একটি production endpoint:

```text
GET /api/products/

?search=iphone
&category=mobile
&brand=Apple
&min_price=500
&max_price=1500
&available=true
&ordering=-rating
&page=1
```

এই একটি endpoint-এই user করতে পারবে:

* 🔍 Product search
* 📂 Category filter
* 🏷️ Brand filter
* 💰 Price range
* 📦 In-stock only
* ⭐ Rating অনুযায়ী sorting
* 📄 Pagination

এটাই production-grade filtering pattern, এবং বেশিরভাগ DRF e-commerce বা marketplace project-এ এই ধরনের architecture ব্যবহার করা হয়।
না। **সব field-এর জন্য Filter বানানো দরকার নেই।**

----


Production-এ **যে field দিয়ে user filter করতে পারবে, শুধু সেই field-গুলোর জন্য filter তৈরি করা হয়।**

ধরো তোমার `Product` model:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    slug = models.SlugField()
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()
    rating = models.DecimalField(max_digits=2, decimal_places=1)
    is_active = models.BooleanField(default=True)

    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    brand = models.ForeignKey(Brand, on_delete=models.CASCADE)

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

Model-এ ১০টি field আছে।

কিন্তু FilterSet হতে পারে মাত্র ৫টি field-এর জন্য।

```python
class ProductFilter(django_filters.FilterSet):

    name = django_filters.CharFilter(lookup_expr="icontains")

    category = django_filters.CharFilter(
        field_name="category__slug"
    )

    brand = django_filters.CharFilter(
        field_name="brand__name"
    )

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
        fields = []
```

এখন API হবে

```text
GET /products/?name=iphone
GET /products/?category=mobile
GET /products/?brand=Apple
GET /products/?min_price=500
GET /products/?max_price=2000
```

কিন্তু নিচের field-গুলোর জন্য filter নেই:

* `slug`
* `description`
* `stock`
* `created_at`
* `updated_at`

কারণ business requirement-এ এগুলোর প্রয়োজন নেই।

---

## তাহলে কোন field-এ filter বানাব?

সাধারণত user যেগুলো দিয়ে data খুঁজবে, সেগুলো।

**E-commerce**

* ✅ Category
* ✅ Brand
* ✅ Price
* ✅ Rating
* ✅ Availability
* ✅ Name

**Blog**

* ✅ Author
* ✅ Category
* ✅ Published Date
* ✅ Tag
* ✅ Status

**Job Portal**

* ✅ Company
* ✅ Location
* ✅ Salary
* ✅ Experience
* ✅ Job Type

---

### Rule of Thumb

**Model-এর সব field filter করতে হবে না।**

শুধু যেসব field দিয়ে **API consumer (React, Mobile App, Frontend)** filter করবে, সেগুলোর জন্যই `django-filter`-এ filter define করবে। এতে API পরিষ্কার, দ্রুত এবং maintain করা সহজ হয়।
হ্যাঁ, **`field_name` যেটা দিচ্ছো, সেটা শেষ পর্যন্ত Model-এর field (বা Model relationship-এর field) হতে হবে।**

---

### Example 1: Model field (Direct)

Model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

Filter

```python
price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="gte"
)
```

এখানে `price` **Product model-এ আছে**, তাই ঠিক।

---

## Example 2: Related Model Field

Model

```python
class Category(models.Model):
    slug = models.SlugField()


class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

Filter

```python
category = django_filters.CharFilter(
    field_name="category__slug"
)
```

এখানে:

* `category` → Product model-এর ForeignKey field ✅
* `slug` → Category model-এর field ✅

তাই `category__slug` valid।

---

## Example 3: Wrong

Product model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
```

Filter

```python
category = django_filters.CharFilter(
    field_name="category__slug"
)
```

❌ Error হবে, কারণ `Product` model-এ `category` field-ই নেই।

---

## Example 4: Filter name ≠ Model field

এটা অনেকেই confuse হয়।

```python
min_price = django_filters.NumberFilter(
    field_name="price",
    lookup_expr="gte"
)
```

এখানে

* `min_price` → **API parameter name** (Model-এ থাকতে হবে না)
* `field_name="price"` → **Model-এর field**, এটা অবশ্যই থাকতে হবে।

API

```text
GET /products/?min_price=500
```

এটি ভিতরে execute করবে

```python
Product.objects.filter(price__gte=500)
```

---

## সহজ Rule

```python
filter_variable = django_filters.Filter(
    field_name="model_field"
)
```

* `filter_variable` → যেকোনো নাম হতে পারে (`min_price`, `max_price`, `available`, `q`)
* `field_name` → **Model-এর field** অথবা **related model-এর field** (`category__slug`, `brand__name`) হতে হবে।

**সুতরাং উত্তর:** `field_name`-এ যে field দেবে, সেটি অবশ্যই model-এ (বা related model-এ) থাকতে হবে। Filter-এর variable name model-এর field হওয়া বাধ্যতামূলক নয়।


