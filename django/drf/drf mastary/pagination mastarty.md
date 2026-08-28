দারুণ। Django REST Framework-এর **Pagination** এমন একটি বিষয় যা প্রায় সব Production API-তে ব্যবহৃত হয়। শুধু `PageNumberPagination` জানলেই হবে না—কখন কোন pagination ব্যবহার করতে হবে, performance, customization, frontend integration—সব জানতে হবে।

আমি এটাকে **৫টি লেসনে** ভাগ করছি, যাতে শেষে আপনি নিজের pagination class তৈরি করতে পারেন এবং যেকোনো DRF project-এ confidently ব্যবহার করতে পারেন।

---

# Django REST Framework Pagination Mastery

## Lesson 1 — Pagination Fundamentals (Why & How)

### Goal

Pagination কী, কেন দরকার, DRF কীভাবে কাজ করে—এগুলো বুঝবেন।

---

## Problem

ধরুন আপনার Product টেবিলে

```
1,000,000 Products
```

API

```
GET /api/products/
```

যদি সব ডাটা একবারে পাঠায়—

```
[
   {...},
   {...},
   {...},
   .....
   1000000 items
]
```

Problems

* Slow Response
* Huge Memory Usage
* Browser Hang
* Mobile Crash
* Database Load
* Network Cost

তাই Pagination দরকার।

---

## Pagination কী?

Pagination মানে

```
সব ডাটা না পাঠিয়ে

অল্প অল্প করে পাঠানো।
```

Example

```
Page 1

1-10
```

```
Page 2

11-20
```

```
Page 3

21-30
```

---

## DRF Pagination Flow

```
Client

↓

GET /products?page=2

↓

View

↓

Queryset

↓

Paginator

↓

Serializer

↓

Response
```

Paginator মাঝখানে queryset কাটে।

---

## Without Pagination

```python
queryset = Product.objects.all()
```

Response

```
100000 rows
```

---

## With Pagination

```python
queryset = Product.objects.all()
```

Paginator

```
LIMIT 10
OFFSET 20
```

Database-ই মাত্র ১০টি row ফেরত দেয়।

এটাই pagination-এর বড় সুবিধা।

---

## Built-in Pagination Types

DRF-এ প্রধানত ৩ ধরনের pagination রয়েছে।

### 1. Page Number Pagination

```
GET /products?page=3
```

---

### 2. Limit Offset Pagination

```
GET /products?limit=20&offset=40
```

---

### 3. Cursor Pagination

```
GET /products?cursor=abcxyz
```

Production-এ বড় dataset-এর জন্য বেশি ব্যবহৃত হয়।

---

## Pagination Response

Default response সাধারণত এমন হয়:

```json
{
    "count": 120,

    "next": ".../?page=3",

    "previous": ".../?page=1",

    "results": [
        ...
    ]
}
```

Meaning

```
count
```

মোট object সংখ্যা।

---

```
next
```

পরবর্তী page।

---

```
previous
```

আগের page।

---

```
results
```

বর্তমান page-এর data।

---

## Pagination কোথায় কাজ করে?

Pagination শুধু queryset-এর উপর কাজ করে।

যেমন

```python
queryset = Product.objects.filter(is_active=True)
```

Paginator প্রথমে queryset পায়।

তারপর

```
LIMIT

OFFSET
```

যোগ করে।

---

## SQL Behind the Scene

Page Size

```
10
```

Page

```
3
```

Generated SQL

```sql
SELECT *

FROM product

LIMIT 10

OFFSET 20;
```

অর্থাৎ

```
OFFSET

(page - 1) × page_size
```

---

## DRF Components

```
APIView

↓

GenericAPIView

↓

ListAPIView

↓

Pagination Class

↓

Serializer
```

`ListAPIView` এবং `ModelViewSet` pagination স্বয়ংক্রিয়ভাবে ব্যবহার করতে পারে।

---

## Global Pagination

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 10,
}
```

এখন সব List API-তে pagination কাজ করবে।

---

## Per View Pagination

```python
class ProductList(ListAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = PageNumberPagination
```

---

## Pagination Lifecycle

```
Request

↓

View

↓

get_queryset()

↓

Paginator.paginate_queryset()

↓

Serializer

↓

Paginator.get_paginated_response()

↓

JSON Response
```

---

# Real Project Example

ধরুন

```
50000 Products
```

User

```
GET /products?page=1
```

Response

```
10 products
```

User Scroll

```
GET /products?page=2
```

Response

```
next 10 products
```

React, Next.js বা Flutter frontend এইভাবেই Infinite Scroll বা Pagination UI তৈরি করে।

---

# Best Practices

✅ Pagination সব List API-তে ব্যবহার করুন।

✅ Page size খুব বড় রাখবেন না (সাধারণত ১০–৫০)।

✅ Detail API (`/products/5/`) তে pagination প্রয়োজন নেই।

✅ Pagination database query কমায় এবং response time উন্নত করে।

---

# Interview Questions

**১. Pagination কেন ব্যবহার করা হয়?**

বড় queryset ছোট ছোট অংশে ভাগ করে দ্রুত response, কম memory usage এবং ভালো performance নিশ্চিত করার জন্য।

**২. Pagination কোথায় কাজ করে?**

QuerySet-এর উপর।

**৩. Pagination কি Serializer-এর আগে নাকি পরে কাজ করে?**

Serializer-এর আগে। প্রথমে queryset slice করা হয়, তারপর সেই slice serialize হয়।

**৪. Pagination-এর মূল সুবিধা কী?**

* Faster API
* Lower memory usage
* Better database performance
* Improved user experience

---

## Assignment

একটি `Book` model তৈরি করুন এবং ৫০টি dummy record insert করুন। তারপর:

1. Global pagination (`PAGE_SIZE = 10`) চালু করুন।
2. `GET /books/` কল করুন এবং response-এ `count`, `next`, `previous`, `results` কীভাবে পরিবর্তন হয় তা লক্ষ্য করুন।
3. `?page=2` ও `?page=5` পরীক্ষা করুন।

---

**Lesson 2-এ** আমরা **PageNumberPagination** নিয়ে গভীরভাবে শিখব—`page_size`, `page_query_param`, `page_size_query_param`, `max_page_size`, custom response format এবং production-ready customization।


# Django REST Framework Pagination Mastery

# Lesson 2 — PageNumberPagination Deep Dive

আজ আমরা DRF-এর সবচেয়ে বেশি ব্যবহৃত Pagination শিখব।

শেষে আপনি শিখবেন—

* ✅ Global Pagination
* ✅ Per View Pagination
* ✅ Custom Page Size
* ✅ User Controlled Page Size
* ✅ Max Page Size
* ✅ Custom Query Parameter
* ✅ Custom Response Format
* ✅ Production Best Practices

---

# Recap

ধরুন Database এ

```text
100 Products
```

User Request

```http
GET /api/products/?page=3
```

Paginator হিসাব করবে

```text
Page Size = 10

Offset = (3-1) × 10

Offset =20
```

SQL

```sql
SELECT *
FROM product
LIMIT 10
OFFSET 20;
```

---

# What is PageNumberPagination?

এটি Page Number ভিত্তিক Pagination।

Example

```http
GET /products?page=1
```

```http
GET /products?page=2
```

```http
GET /products?page=3
```

সবচেয়ে Human Friendly Pagination।

---

# Step 1 — Global Configuration

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_PAGINATION_CLASS":
        "rest_framework.pagination.PageNumberPagination",

    "PAGE_SIZE":10

}
```

এখন

যেকোনো

```python
ListAPIView
```

অথবা

```python
ModelViewSet
```

Automatically paginate হবে।

---

# Example View

```python
from rest_framework.generics import ListAPIView

class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

এখানে

Pagination Automatically কাজ করবে।

---

# Response

```json
{
    "count":100,

    "next":"http://localhost:8000/api/products/?page=2",

    "previous":null,

    "results":[

        ...

    ]
}
```

---

# Request Page 5

```http
GET /products?page=5
```

Response

```json
{
    "count":100,

    "next":"...?page=6",

    "previous":"...?page=4",

    "results":[]
}
```

results এ থাকবে

Page 5 এর Data।

---

# Internally What Happens?

Flow

```text
Request

↓

View

↓

Queryset

↓

Paginator

↓

Serializer

↓

Response
```

Paginator

প্রথমে

```python
queryset = Product.objects.all()
```

নেয়।

তারপর

```python
queryset[40:50]
```

শুধু এটুকু Serializer এ পাঠায়।

---

# Per View Pagination

Global Pagination Override করা যায়।

Example

```python
from rest_framework.pagination import PageNumberPagination

class ProductPagination(PageNumberPagination):

    page_size = 20
```

View

```python
class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = ProductPagination
```

এখন

এই View

২০টি Data দিবে।

---

# page_size Attribute

```python
class ProductPagination(PageNumberPagination):

    page_size = 5
```

Response

```text
5 Products
```

---

```python
page_size = 20
```

Response

```text
20 Products
```

---

```python
page_size = 100
```

Response

```text
100 Products
```

---

# page_query_param

Default

```http
?page=2
```

আপনি Change করতে পারেন।

```python
class ProductPagination(PageNumberPagination):

    page_query_param="p"
```

এখন

```http
GET /products?p=3
```

---

আগেরটি

```http
?page=3
```

আর কাজ করবে না।

---

# page_size_query_param

অনেক Website এ

User নিজেই Page Size Change করতে পারে।

Example

```http
GET /products?page=1&page_size=25
```

এটা Enable করতে হবে।

```python
class ProductPagination(PageNumberPagination):

    page_size=10

    page_size_query_param="page_size"
```

এখন

User

```http
GET /products?page_size=30
```

দিলে

৩০টি Data পাবে।

---

# Problem

যদি User

```http
page_size=1000000
```

দেয়?

Server Crash হতে পারে।

তাই

---

# max_page_size

```python
class ProductPagination(PageNumberPagination):

    page_size=10

    page_size_query_param="page_size"

    max_page_size=100
```

এখন

```http
?page_size=500
```

User Request

↓

Actual Response

```text
100 records
```

এর বেশি দিবে না।

---

# Complete Pagination Class

```python
from rest_framework.pagination import PageNumberPagination


class ProductPagination(PageNumberPagination):

    page_size = 10

    page_query_param = "page"

    page_size_query_param = "page_size"

    max_page_size = 100
```

Production এ এটিই সবচেয়ে Common।

---

# Custom Response

অনেকে

Default Response পছন্দ করেন না।

Default

```json
{
    "count":100,

    "next":"...",

    "previous":"...",

    "results":[]
}
```

আপনি Customize করতে পারেন।

---

# Override get_paginated_response()

```python
from rest_framework.pagination import PageNumberPagination
from rest_framework.response import Response


class ProductPagination(PageNumberPagination):

    page_size = 10

    def get_paginated_response(self, data):

        return Response({

            "success": True,

            "total": self.page.paginator.count,

            "page": self.page.number,

            "total_pages": self.page.paginator.num_pages,

            "next": self.get_next_link(),

            "previous": self.get_previous_link(),

            "results": data

        })
```

Response

```json
{
    "success":true,

    "total":100,

    "page":2,

    "total_pages":10,

    "next":"...",

    "previous":"...",

    "results":[]
}
```

---

# Reusable Pagination Folder

Production Project

```text
common/

    pagination.py

products/

orders/

accounts/

payments/
```

common/pagination.py

```python
class DefaultPagination(PageNumberPagination):

    page_size=10

    page_size_query_param="page_size"

    max_page_size=100
```

সব View

```python
pagination_class = DefaultPagination
```

ব্যবহার করবে।

---

# Common Mistakes

### ❌ Mistake 1

```python
page_size = 1000
```

খুব বড় Page Size দেবেন না।

---

### ❌ Mistake 2

```python
max_page_size=None
```

User

১০ লাখ Row চাইতে পারবে।

---

### ❌ Mistake 3

Pagination Class লিখে

```python
pagination_class =
```

ব্যবহার না করা।

---

### ❌ Mistake 4

Detail API তে Pagination ব্যবহার করা।

```http
/products/5/
```

এখানে Pagination-এর দরকার নেই।

---

# Real Project Example

E-commerce

```http
GET /api/products/?page=2&page_size=20
```

News Portal

```http
GET /api/articles/?page=5
```

Blog

```http
GET /api/posts/?page_size=12
```

Admin Dashboard

```http
GET /api/orders/?page=8
```

সব ক্ষেত্রেই PageNumberPagination ব্যবহার করা যায়।

---

# Interview Questions

### ১. `page_size` কী?

প্রতি page-এ কতটি object থাকবে তা নির্ধারণ করে।

---

### ২. `page_query_param` কী?

Page number-এর query parameter-এর নাম পরিবর্তন করতে ব্যবহৃত হয়।

---

### ৩. `page_size_query_param` কী?

User-কে request-এর মাধ্যমে page size পরিবর্তনের সুযোগ দেয়।

---

### ৪. `max_page_size` কেন দরকার?

Server-কে বড় request থেকে সুরক্ষিত রাখতে এবং performance বজায় রাখতে।

---

### ৫. `get_paginated_response()` কেন override করা হয়?

API response-এর format customize করার জন্য।

---

# Assignment

একটি `Article` API তৈরি করুন।

1. `ArticlePagination(PageNumberPagination)` class বানান।
2. `page_size = 5` সেট করুন।
3. `page_size_query_param = "size"` ব্যবহার করুন।
4. `max_page_size = 20` সেট করুন।
5. `get_paginated_response()` override করে নিচের format দিন:

```json
{
    "success": true,
    "page": 1,
    "total_pages": 10,
    "total_items": 50,
    "results": []
}
```

এই Assignment শেষ করতে পারলে আপনি **PageNumberPagination**-এ বেশ স্বচ্ছন্দ হয়ে যাবেন।

**Lesson 3**-এ আমরা **LimitOffsetPagination** শিখব—এটি কীভাবে SQL-এর `LIMIT` এবং `OFFSET` ব্যবহার করে, কখন PageNumberPagination-এর চেয়ে ভালো, এবং বড় ডেটাসেটে এর সুবিধা ও সীমাবদ্ধতা কী।
# Django REST Framework Pagination Mastery

# Lesson 3 — LimitOffsetPagination Deep Dive

আজ আমরা DRF-এর দ্বিতীয় Pagination Type শিখব।

এটি Backend Engineer Interview এবং Production API-তে অনেক ব্যবহৃত হয়।

শেষে আপনি শিখবেন—

* ✅ LimitOffsetPagination কী
* ✅ SQL-এর সাথে সম্পর্ক
* ✅ limit এবং offset কীভাবে কাজ করে
* ✅ Custom LimitOffsetPagination
* ✅ Frontend Integration
* ✅ Performance Issues
* ✅ কখন এটি ব্যবহার করবেন

---

# Recap

আগের Lesson-এ আমরা Page Number ব্যবহার করেছি।

```http
GET /products?page=3
```

এখানে User Page Number জানে।

---

আজ

User Page জানবে না।

বরং বলবে

```http
GET /products?limit=10&offset=20
```

---

# What is LimitOffsetPagination?

Database-এর LIMIT এবং OFFSET ব্যবহার করে Pagination।

Example

```text
Products

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
...
```

Request

```http
GET /products?limit=5&offset=10
```

মানে

```text
প্রথম ১০টি Skip করো

তারপর ৫টি দাও
```

Result

```text
11
12
13
14
15
```

---

# SQL Behind the Scene

Request

```http
GET /products?limit=10&offset=20
```

SQL

```sql
SELECT *
FROM product
LIMIT 10
OFFSET 20;
```

Database শুধুমাত্র

```text
21-30
```

Row Return করবে।

---

# Why use Offset?

ধরুন

```text
10000 Products
```

আপনি

```http
GET /products?page=3
```

করলেন।

Paginator নিজেই হিসাব করবে।

কিন্তু

```http
GET /products?offset=20
```

করলে

Backend-কে Page Number Calculate করতে হবে না।

---

# Enable Globally

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_PAGINATION_CLASS":
        "rest_framework.pagination.LimitOffsetPagination",

    "PAGE_SIZE":10

}
```

---

# Or Per View

```python
from rest_framework.pagination import LimitOffsetPagination


class ProductPagination(LimitOffsetPagination):

    default_limit = 10
```

View

```python
class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = ProductPagination
```

---

# default_limit

```python
class ProductPagination(LimitOffsetPagination):

    default_limit = 10
```

User যদি

```http
GET /products/
```

দেয়

তাহলে

```text
10 records
```

পাবে।

---

# limit

User চাইলে

```http
GET /products?limit=20
```

করতে পারে।

Result

```text
20 Records
```

---

# offset

```http
GET /products?limit=10&offset=30
```

মানে

```text
Skip

30

Take

10
```

Result

```text
31-40
```

---

# Response

Default Response

```json
{
    "count":100,

    "next":"...?limit=10&offset=10",

    "previous":null,

    "results":[]
}
```

---

Second Page

```http
GET /products?limit=10&offset=10
```

Response

```json
{
    "count":100,

    "next":"...?limit=10&offset=20",

    "previous":"...?limit=10&offset=0",

    "results":[]
}
```

---

# limit_query_param

Default

```http
?limit=20
```

Change করতে পারেন।

```python
class ProductPagination(LimitOffsetPagination):

    limit_query_param = "size"
```

এখন

```http
GET /products?size=20
```

---

# offset_query_param

Default

```http
?offset=40
```

Change

```python
class ProductPagination(LimitOffsetPagination):

    offset_query_param = "start"
```

Request

```http
GET /products?size=20&start=40
```

---

# max_limit

Production এ

```http
limit=100000
```

Allow করা উচিত না।

তাই

```python
class ProductPagination(LimitOffsetPagination):

    default_limit = 10

    max_limit = 100
```

---

User

```http
?limit=1000
```

Actual

```text
100
```

---

# Complete Pagination Class

```python
from rest_framework.pagination import LimitOffsetPagination


class ProductPagination(LimitOffsetPagination):

    default_limit = 10

    max_limit = 100

    limit_query_param = "limit"

    offset_query_param = "offset"
```

---

# Custom Response

```python
from rest_framework.pagination import LimitOffsetPagination
from rest_framework.response import Response


class ProductPagination(LimitOffsetPagination):

    default_limit = 10

    def get_paginated_response(self, data):

        return Response({

            "success": True,

            "total_items": self.count,

            "limit": self.limit,

            "offset": self.offset,

            "next": self.get_next_link(),

            "previous": self.get_previous_link(),

            "results": data

        })
```

Response

```json
{
    "success":true,

    "total_items":100,

    "limit":10,

    "offset":20,

    "results":[]
}
```

---

# Frontend Example

React

প্রথম Load

```http
GET /products?limit=10&offset=0
```

Load More Button

```http
GET /products?limit=10&offset=10
```

Next

```http
GET /products?limit=10&offset=20
```

এভাবে Infinite Scroll বানানো যায়।

---

# Real SQL Example

```python
Product.objects.all()[20:30]
```

Equivalent SQL

```sql
SELECT *
FROM product
LIMIT 10
OFFSET 20;
```

Python Slice এবং SQL LIMIT/OFFSET একে অপরের সাথে সম্পর্কিত।

---

# Performance Problem

ধরুন

```text
5 Million Rows
```

Request

```http
GET /products?offset=4000000
```

Database কী করবে?

```text
প্রথমে

৪০ লক্ষ Row Skip করবে

তারপর

১০টি Row দিবে।
```

এতে Query Slow হয়ে যায়।

---

# When Not to Use LimitOffsetPagination

যদি

* কোটি কোটি Row থাকে
* Infinite Scroll থাকে
* Live Feed থাকে
* Frequently Insert/Delete হয়

তাহলে

**CursorPagination** ব্যবহার করা ভালো।

---

# PageNumber vs LimitOffset

| Feature                  | PageNumber | LimitOffset           |
| ------------------------ | ---------- | --------------------- |
| Query                    | `?page=2`  | `?limit=10&offset=10` |
| Easy for Users           | ✅          | ❌                     |
| SQL Friendly             | ✅          | ✅                     |
| Infinite Scroll          | ⚠️         | ✅                     |
| Large Offset Performance | ❌          | ❌                     |

---

# Production Use Cases

### E-commerce

```http
GET /products?limit=20&offset=40
```

---

### Search API

```http
GET /search?limit=15&offset=30
```

---

### Admin Panel

```http
GET /orders?limit=50&offset=100
```

---

### Analytics Dashboard

```http
GET /logs?limit=100&offset=500
```

---

# Common Mistakes

### ❌ max_limit না দেওয়া

User বড় limit পাঠাতে পারবে।

---

### ❌ Huge Offset

```http
offset=5000000
```

Slow Query হতে পারে।

---

### ❌ limit=10000

Response বড় হয়ে যাবে।

---

# Interview Questions

### ১. LimitOffsetPagination কী?

Database-এর `LIMIT` এবং `OFFSET` ব্যবহার করে queryset-এর নির্দিষ্ট অংশ ফেরত দেয়।

---

### ২. `default_limit` কী?

User limit না দিলে ডিফল্ট কতটি object ফেরত দেওয়া হবে।

---

### ৩. `max_limit` কেন ব্যবহার করা হয়?

অতিরিক্ত বড় request থেকে API এবং Database-কে সুরক্ষিত রাখতে।

---

### ৪. Offset বেশি হলে সমস্যা কী?

Database-কে অনেক row skip করতে হয়, ফলে query ধীর হয়ে যায়।

---

### ৫. LimitOffsetPagination-এর সবচেয়ে বড় সুবিধা কী?

Infinite Scroll এবং API consumer-দের জন্য এটি খুব flexible, কারণ তারা সরাসরি `limit` ও `offset` নিয়ন্ত্রণ করতে পারে।

---

# Assignment

একটি `Order` API তৈরি করুন।

1. `OrderPagination(LimitOffsetPagination)` class তৈরি করুন।
2. `default_limit = 20`
3. `max_limit = 100`
4. `limit_query_param = "size"`
5. `offset_query_param = "start"`
6. `get_paginated_response()` override করে নিচের format দিন:

```json
{
    "success": true,
    "total_items": 500,
    "size": 20,
    "start": 40,
    "results": []
}
```

---

## Lesson 4 Preview

পরের লেসনে আমরা **CursorPagination** শিখব, যা Facebook, Instagram, Twitter (X), YouTube Feed-এর মতো বড় এবং frequently changing dataset-এর জন্য ব্যবহৃত হয়। এটি কেন `LIMIT/OFFSET`-এর performance problem সমাধান করে, সেটা গভীরভাবে দেখব।
# Django REST Framework Pagination Mastery

# Lesson 4 — CursorPagination Deep Dive (Production Level)

আজ আমরা DRF-এর সবচেয়ে Advanced Pagination শিখব।

**Facebook, Instagram, Twitter (X), YouTube, LinkedIn**-এর Feed-এর মতো API-তে Cursor Pagination ব্যবহার করা হয়।

শেষে আপনি শিখবেন—

* ✅ CursorPagination কী
* ✅ কেন Offset Pagination-এর থেকে ভালো
* ✅ Cursor কী
* ✅ Cursor Generate কীভাবে হয়
* ✅ Ordering-এর গুরুত্ব
* ✅ Custom CursorPagination
* ✅ Infinite Scroll
* ✅ Performance Analysis
* ✅ Real-world Use Cases

---

# Lesson Recap

আমরা ইতিমধ্যে দুইটি Pagination শিখেছি।

### PageNumberPagination

```http
GET /products?page=3
```

---

### LimitOffsetPagination

```http
GET /products?limit=10&offset=20
```

---

এখন সমস্যা দেখি।

ধরুন Database-এ

```text
10 Million Products
```

User Request

```http
GET /products?limit=20&offset=9000000
```

Database কী করবে?

```text
১ম Row

↓

২য় Row

↓

৩য় Row

↓

....

↓

৯০,০০,০০০ Row Skip

↓

তারপর ২০টি Return
```

এটি খুব ধীর (Slow Query)।

---

# CursorPagination কী?

CursorPagination Page Number বা Offset ব্যবহার করে না।

এটি একটি **Encoded Cursor** ব্যবহার করে।

Request

```http
GET /products?cursor=cD0yMDI2LTA3LTE0KzEw
```

Cursor-এর ভিতরে থাকে

```text
Last Seen Record
```

Database সরাসরি সেখান থেকেই পরের Data নিয়ে আসে।

---

# Cursor Flow

```text
Client

↓

GET /posts?cursor=abc123

↓

CursorPagination

↓

Decode Cursor

↓

Find Last Record

↓

Fetch Next Items

↓

Response

↓

New Cursor
```

---

# Example

Database

```text
ID

1

2

3

4

5

6

7

8

9

10
```

Page Size

```text
3
```

---

First Request

```http
GET /posts/
```

Response

```json
{
    "next":"...?cursor=abcxyz",

    "previous":null,

    "results":[

        1,
        2,
        3

    ]
}
```

---

Next Request

```http
GET /posts?cursor=abcxyz
```

Response

```json
{
    "next":"...?cursor=qwerty",

    "results":[

        4,
        5,
        6

    ]
}
```

User কখনো জানেই না

```text
Offset কত

Page কত
```

---

# Why is it Fast?

Offset

```sql
OFFSET 9000000
```

Database-কে Skip করতে হয়।

Cursor

```sql
WHERE id > 9000000
LIMIT 20
```

Database Index ব্যবহার করতে পারে।

এটাই Cursor Pagination-এর সবচেয়ে বড় সুবিধা।

---

# DRF Configuration

```python
from rest_framework.pagination import CursorPagination


class ProductCursorPagination(CursorPagination):

    page_size = 10

    ordering = "-created_at"
```

---

View

```python
class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = ProductCursorPagination
```

---

# ordering Attribute

সবচেয়ে গুরুত্বপূর্ণ Property।

```python
ordering = "-created_at"
```

মানে

```text
Newest First
```

---

আর

```python
ordering = "created_at"
```

মানে

```text
Oldest First
```

---

আরও Example

```python
ordering = "-id"
```

---

```python
ordering = "price"
```

---

```python
ordering = "-published_at"
```

---

# Important Rule

Ordering Field অবশ্যই

* Indexed হওয়া ভালো
* Stable হওয়া উচিত
* Unique হওয়া ভালো

Best Choices

```text
id

created_at

published_at

uuid
```

Avoid

```text
name

title

description
```

কারণ Duplicate Value থাকতে পারে।

---

# page_size

```python
page_size = 20
```

মানে

```text
২০টি করে Result
```

---

# cursor_query_param

Default

```http
?cursor=
```

Change করতে পারেন।

```python
cursor_query_param = "next"
```

Request

```http
GET /posts?next=abcxyz
```

---

# Complete CursorPagination

```python
from rest_framework.pagination import CursorPagination


class ProductCursorPagination(CursorPagination):

    page_size = 20

    ordering = "-created_at"

    cursor_query_param = "cursor"
```

---

# Response

```json
{
    "next":"...?cursor=cD0yMDI2LTA4",

    "previous":null,

    "results":[

        ...

    ]
}
```

Cursor দেখতে

```text
cD0yMDI2LTA4
```

এরকম হয়।

এটি Base64-এর মতো Encoded Value।

User সাধারণত এটি বুঝতে পারে না।

---

# Infinite Scroll

Instagram

```text
Load

↓

Scroll

↓

Next Cursor

↓

More Posts

↓

Next Cursor

↓

More Posts
```

কোন Page Number নেই।

---

# SQL Comparison

LimitOffset

```sql
SELECT *
FROM product
LIMIT 20
OFFSET 5000000;
```

---

Cursor

```sql
SELECT *
FROM product
WHERE created_at < '2026-07-14'
ORDER BY created_at DESC
LIMIT 20;
```

Cursor Query অনেক Efficient।

---

# Performance Comparison

| Dataset         | PageNumber | LimitOffset | Cursor |
| --------------- | ---------- | ----------- | ------ |
| 1,000 Rows      | ✅          | ✅           | ✅      |
| 100,000 Rows    | ✅          | ⚠️          | ✅      |
| 10 Million Rows | ❌          | ❌           | ✅      |
| Live Feed       | ❌          | ⚠️          | ✅      |

---

# Real-world Examples

### Instagram Feed

```http
GET /posts?cursor=abcxyz
```

---

### Twitter Timeline

```http
GET /tweets?cursor=xyz123
```

---

### YouTube Comments

```http
GET /comments?cursor=qwe456
```

---

### Notification API

```http
GET /notifications?cursor=aaaa
```

---

### Chat Messages

```http
GET /messages?cursor=bbbb
```

---

# Common Mistakes

## ❌ Mistake 1

```python
ordering = "name"
```

Duplicate হতে পারে।

---

## ❌ Mistake 2

Ordering Field-এ Index না রাখা।

Query Slow হবে।

---

## ❌ Mistake 3

Frequently Updated Field ব্যবহার করা।

যেমন

```python
ordering = "updated_at"
```

এতে Record-এর Position বারবার বদলে যেতে পারে।

---

## ❌ Mistake 4

CursorPagination দিয়ে

```text
Page 50
```

এ যেতে চাওয়া।

CursorPagination Sequential Navigation-এর জন্য, Random Page Jump-এর জন্য নয়।

---

# Which Pagination Should You Use?

| Situation         | Best Choice           |
| ----------------- | --------------------- |
| Admin Dashboard   | PageNumberPagination  |
| Product List      | PageNumberPagination  |
| Search Results    | LimitOffsetPagination |
| Mobile App Feed   | CursorPagination      |
| Social Media Feed | CursorPagination      |
| Notifications     | CursorPagination      |
| Chat Messages     | CursorPagination      |

---

# Production Folder Structure

```text
common/
    pagination.py

products/
orders/
posts/
notifications/
```

`common/pagination.py`

```python
from rest_framework.pagination import CursorPagination


class DefaultCursorPagination(CursorPagination):

    page_size = 20

    ordering = "-created_at"
```

---

# Interview Questions

### ১. CursorPagination কী?

CursorPagination একটি pagination mechanism যা page number বা offset-এর পরিবর্তে encoded cursor ব্যবহার করে পরবর্তী data fetch করে।

---

### ২. CursorPagination কেন Fast?

এটি বড় `OFFSET` skip করে না। বরং indexed ordering field ব্যবহার করে সরাসরি পরবর্তী record থেকে query শুরু করে।

---

### ৩. CursorPagination-এর জন্য কোন field ভালো?

* `id`
* `created_at`
* `published_at`
* `uuid`

---

### ৪. CursorPagination-এর অসুবিধা কী?

নির্দিষ্ট page (যেমন page 10) এ সরাসরি যাওয়া যায় না।

---

### ৫. Social Media Feed-এ CursorPagination কেন ব্যবহার করা হয়?

কারণ Feed সব সময় পরিবর্তিত হয় (নতুন post যোগ হয়), এবং CursorPagination duplicate বা missing item-এর সমস্যা কমায় এবং বড় dataset-এ দ্রুত কাজ করে।

---

# Assignment

একটি `News` API তৈরি করুন।

1. `NewsCursorPagination(CursorPagination)` class তৈরি করুন।
2. `page_size = 15`
3. `ordering = "-published_at"`
4. `cursor_query_param = "next_cursor"`
5. `ListAPIView`-এ এটি ব্যবহার করুন।
6. ১০০টি Dummy News Insert করে API কল করুন এবং `next_cursor` ব্যবহার করে পরবর্তী data আনুন।

---

## Lesson 5 Preview

শেষ লেসনে আমরা **Custom Pagination (Production Ready)** শিখব। সেখানে একটি reusable `DefaultPagination` তৈরি করব, custom response format, metadata (`current_page`, `total_pages`, `has_next`, `has_previous`), pagination + filtering + searching + ordering একসাথে ব্যবহার করা, এবং বড় DRF project-এর best practices দেখব। এটি production-grade API design-এর জন্য সবচেয়ে গুরুত্বপূর্ণ অংশ।
# Django REST Framework Pagination Mastery

# Lesson 5 — Production Ready Custom Pagination (Master Level)

এখন পর্যন্ত আমরা শিখেছি—

* ✅ PageNumberPagination
* ✅ LimitOffsetPagination
* ✅ CursorPagination

আজ শিখব **Production Ready Pagination Architecture**।

এটাই বড় কোম্পানির Django Project-এ বেশি দেখা যায়।

---

# Goal

শেষে আপনি পারবেন—

* Production Ready Pagination Class বানাতে
* Common Pagination Reuse করতে
* Custom Response Format বানাতে
* Pagination Metadata Add করতে
* Filtering + Searching + Ordering + Pagination একসাথে ব্যবহার করতে
* Performance Optimize করতে
* কোন Project-এ কোন Pagination ব্যবহার করতে

---

# Production Folder Structure

ছোট Project

```text
products/
    pagination.py
```

বড় Project

```text
core/

    pagination.py

accounts/

products/

orders/

payments/

blogs/
```

সকল App একই Pagination ব্যবহার করবে।

---

# Step 1 — Base Pagination

```python
# core/pagination.py

from rest_framework.pagination import PageNumberPagination


class DefaultPagination(PageNumberPagination):

    page_size = 10

    page_size_query_param = "page_size"

    max_page_size = 100
```

এখন

```python
pagination_class = DefaultPagination
```

সব View-তে ব্যবহার করা যাবে।

---

# Step 2 — Better Response

Production API সাধারণত

এমন Response দেয় না

```json
{
    "count":100,
    "next":"...",
    "previous":"...",
    "results":[]
}
```

বরং

```json
{
    "success": true,

    "message": "Products fetched successfully",

    "data": [],

    "pagination": {}
}
```

---

# Step 3 — Override Response

```python
from rest_framework.pagination import PageNumberPagination
from rest_framework.response import Response


class DefaultPagination(PageNumberPagination):

    page_size = 10

    page_size_query_param = "page_size"

    max_page_size = 100


    def get_paginated_response(self, data):

        return Response({

            "success": True,

            "message": "Data fetched successfully",

            "pagination": {

                "current_page":
                    self.page.number,

                "page_size":
                    self.get_page_size(self.request),

                "total_pages":
                    self.page.paginator.num_pages,

                "total_items":
                    self.page.paginator.count,

                "has_next":
                    self.page.has_next(),

                "has_previous":
                    self.page.has_previous(),

                "next":
                    self.get_next_link(),

                "previous":
                    self.get_previous_link()

            },

            "data": data

        })
```

---

# Response

```json
{
    "success": true,

    "message":"Data fetched successfully",

    "pagination":{

        "current_page":2,

        "page_size":10,

        "total_pages":15,

        "total_items":145,

        "has_next":true,

        "has_previous":true,

        "next":"...",

        "previous":"..."

    },

    "data":[]
}
```

এটি Production Level Response।

---

# Step 4 — Use in View

```python
from core.pagination import DefaultPagination


class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = DefaultPagination
```

---

# Step 5 — Filtering + Pagination

```python
class ProductListAPIView(ListAPIView):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = DefaultPagination

    filter_backends = [

        DjangoFilterBackend

    ]

    filterset_fields = [

        "category",

        "brand"

    ]
```

Request

```http
GET /products/?category=phone&page=2
```

Flow

```text
Request

↓

Filter

↓

Pagination

↓

Serializer

↓

Response
```

**মনে রাখবেন:** Pagination সবসময় Filter হওয়া QuerySet-এর উপর কাজ করে।

---

# Step 6 — Search + Pagination

```python
filter_backends = [

    SearchFilter

]
```

```python
search_fields = [

    "title",

    "description"

]
```

Request

```http
GET /products/?search=iphone&page=2
```

Flow

```text
Search

↓

Matching QuerySet

↓

Pagination

↓

Serializer
```

---

# Step 7 — Ordering + Pagination

```python
filter_backends = [

    OrderingFilter

]
```

```python
ordering_fields = [

    "price",

    "created_at"

]
```

Request

```http
GET /products/?ordering=-price&page=3
```

Flow

```text
Ordering

↓

Pagination

↓

Serializer
```

---

# Step 8 — Combined Example

```http
GET /products/

?category=laptop

&search=asus

&ordering=-price

&page=2

&page_size=20
```

DRF Flow

```text
All Products

↓

Category Filter

↓

Search

↓

Ordering

↓

Pagination

↓

Serializer

↓

JSON
```

এটাই Production Flow।

---

# Different Pagination Classes

এক Project-এ

একাধিক Pagination থাকতে পারে।

```text
core/

    pagination.py

        DefaultPagination

        SmallPagination

        LargePagination

        FeedPagination
```

Example

```python
class SmallPagination(PageNumberPagination):

    page_size = 5
```

---

```python
class LargePagination(PageNumberPagination):

    page_size = 50
```

---

```python
class FeedPagination(CursorPagination):

    page_size = 20

    ordering = "-created_at"
```

---

View

```python
pagination_class = SmallPagination
```

অথবা

```python
pagination_class = FeedPagination
```

---

# When to Use Which?

| API           | Pagination            |
| ------------- | --------------------- |
| Products      | PageNumberPagination  |
| Categories    | PageNumberPagination  |
| Orders        | PageNumberPagination  |
| Admin Panel   | PageNumberPagination  |
| Search        | LimitOffsetPagination |
| News Feed     | CursorPagination      |
| Notifications | CursorPagination      |
| Chat Messages | CursorPagination      |
| Activity Logs | CursorPagination      |

---

# Pagination + ViewSet

```python
from rest_framework.viewsets import ModelViewSet


class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    pagination_class = DefaultPagination
```

List Action

```http
GET /products/
```

Pagination হবে।

---

Retrieve

```http
GET /products/5/
```

Pagination হবে না।

---

# Pagination with get_queryset()

```python
class ProductListAPIView(ListAPIView):

    serializer_class = ProductSerializer

    pagination_class = DefaultPagination


    def get_queryset(self):

        return Product.objects.filter(

            is_active=True

        )
```

Flow

```text
get_queryset()

↓

Pagination

↓

Serializer
```

---

# Performance Tips

## ✅ Always Order QuerySet

```python
Product.objects.order_by("-created_at")
```

---

## ✅ Select Related

```python
Product.objects.select_related("category")
```

---

## ✅ Prefetch Related

```python
Product.objects.prefetch_related("images")
```

---

## ✅ Only Required Fields

```python
Product.objects.only(

    "id",

    "title",

    "price"

)
```

---

## ✅ Never

```python
page_size = 5000
```

---

# Common Mistakes

### ❌ Mistake 1

```python
pagination_class=None
```

List API-তে Pagination না দেওয়া।

---

### ❌ Mistake 2

```python
page_size=1000
```

Response Slow হবে।

---

### ❌ Mistake 3

```python
max_page_size=None
```

Security Risk।

---

### ❌ Mistake 4

Filtering-এর আগে Manual Slice করা।

```python
Product.objects.all()[:20]
```

এতে Pagination-এর সাথে সমস্যা হতে পারে।

---

# Interview Questions

### ১. বড় Project-এ Pagination কোথায় রাখবেন?

`core/pagination.py` বা `common/pagination.py`-এর মতো shared module-এ।

---

### ২. Pagination-এর সাথে Filtering-এর Order কী?

```
QuerySet
   ↓
Filtering
   ↓
Searching
   ↓
Ordering
   ↓
Pagination
   ↓
Serialization
```

---

### ৩. কেন `get_paginated_response()` Override করবেন?

API-এর Response Structure Customize করার জন্য।

---

### ৪. ViewSet-এর কোন Action-এ Pagination কাজ করে?

শুধু `list()` Action-এ।

---

### ৫. CursorPagination কবে ব্যবহার করবেন?

যখন বড় Dataset, Infinite Scroll, Live Feed বা Frequent Insert/Delete থাকে।

---

# Production Architecture

```text
Client

↓

Request

↓

Authentication

↓

Permission

↓

get_queryset()

↓

Filtering

↓

Searching

↓

Ordering

↓

Pagination

↓

Serializer

↓

Custom Response

↓

JSON
```

এটাই একটি Production-grade DRF API-এর সাধারণ Request Lifecycle।

---

# Final Project Challenge

একটি **E-commerce API** তৈরি করুন যেখানে থাকবে:

* `ProductViewSet`
* `CategoryFilter`
* `SearchFilter`
* `OrderingFilter`
* `DefaultPagination`
* Custom Pagination Response
* `page_size` User Control (`page_size_query_param`)
* `max_page_size = 100`

Example Request:

```http
GET /api/products/

?category=electronics

&search=laptop

&ordering=-price

&page=2

&page_size=20
```

Expected Response:

```json
{
  "success": true,
  "message": "Products fetched successfully",
  "pagination": {
    "current_page": 2,
    "page_size": 20,
    "total_pages": 8,
    "total_items": 156,
    "has_next": true,
    "has_previous": true
  },
  "data": [
    {
      "id": 21,
      "title": "Gaming Laptop",
      "price": 1200
    }
  ]
}
```

---

## Pagination Mastery Summary

এই ৫টি লেসনের পর আপনি DRF-এর Pagination-এর পুরো ecosystem শিখেছেন:

* ✅ Pagination-এর মৌলিক ধারণা
* ✅ `PageNumberPagination`
* ✅ `LimitOffsetPagination`
* ✅ `CursorPagination`
* ✅ Production-ready Custom Pagination
* ✅ Filtering, Searching, Ordering-এর সাথে Pagination Integration
* ✅ Performance Optimization
* ✅ Interview Questions ও Best Practices

এই জ্ঞান দিয়ে আপনি Production-grade Django REST Framework API-তে Pagination আত্মবিশ্বাসের সাথে ডিজাইন ও Implement করতে পারবেন।

# i use pagination but i don't want pagination in detail page how skip detaul page pagination



ভালো প্রশ্ন। **DRF-এ Detail API (`retrieve`) তে Pagination কখনোই apply হয় না।** Pagination শুধুমাত্র **list endpoint**-এ কাজ করে।

যদি আপনি `ModelViewSet`, `ListAPIView` বা `ListModelMixin` ব্যবহার করেন, তাহলে DRF নিজেই Detail page-এ pagination skip করে।

## Example

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = DefaultPagination
```

### List API

```http
GET /products/
```

Response

```json
{
    "count": 100,
    "next": "...",
    "previous": "...",
    "results": [
        ...
    ]
}
```

---

### Detail API

```http
GET /products/5/
```

Response

```json
{
    "id": 5,
    "title": "iPhone 16",
    "price": 1200
}
```

এখানে pagination থাকবে না।

---

# যদি Detail API-তে Pagination দেখেন

তাহলে সাধারণত নিচের দুইটি কারণের একটি হয়।

## Problem 1: আপনি `paginate_queryset()` manually call করেছেন

❌ ভুল

```python
def retrieve(self, request, *args, **kwargs):
    queryset = self.paginate_queryset(self.get_queryset())   # ভুল
    serializer = ProductSerializer(queryset, many=True)
    return self.get_paginated_response(serializer.data)
```

এটা করবেন না।

✔️ সঠিক

```python
def retrieve(self, request, *args, **kwargs):
    instance = self.get_object()
    serializer = ProductSerializer(instance)
    return Response(serializer.data)
```

---

## Problem 2: Nested Data Paginate করতে চাইছেন

যদি Detail API-তে Related Objects (যেমন comments) paginate করতে চান, তাহলে সেটা DRF automatic করে না। আলাদা logic লিখতে হবে।

---

# যদি নির্দিষ্ট Action-এ Pagination বন্ধ করতে চান

উদাহরণ:

```python
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = DefaultPagination

    def paginate_queryset(self, queryset):
        if self.action == "retrieve":
            return None
        return super().paginate_queryset(queryset)
```

তবে **এটা সাধারণত দরকার হয় না**, কারণ `retrieve()` pagination ব্যবহারই করে না।

---

## প্রশ্ন আপনার জন্য

আপনি কোনটা ব্যবহার করছেন?

1. `ModelViewSet`
2. `ReadOnlyModelViewSet`
3. `ListAPIView` + `RetrieveAPIView`
4. `APIView`
5. `GenericAPIView`

আর যদি আপনার `views.py` কোড শেয়ার করেন, আমি দেখিয়ে দেব কেন আপনার Detail API-তে pagination আসছে।
কারণ **DRF-এর design-ই এমন**।

Global pagination (`DEFAULT_PAGINATION_CLASS`) **শুধুমাত্র collection/list endpoints-এর জন্য**। Detail endpoint একটি মাত্র object return করে, তাই সেখানে pagination-এর কোনো অর্থ নেই।

### List API

```http
GET /api/products/
```

Flow:

```text
QuerySet (1000 products)
        ↓
Pagination
        ↓
10 products
        ↓
Serializer (many=True)
        ↓
Response
```

---

### Detail API

```http
GET /api/products/5/
```

Flow:

```text
get_object()
      ↓
Single Product
      ↓
Serializer (many=False)
      ↓
Response
```

এখানে paginate করার মতো **QuerySet** নেই, একটি মাত্র object আছে।

---

## DRF-এর ভিতরে কী হয়?

`ListModelMixin`-এর `list()` method-এ pagination call করা হয়।

সরলভাবে:

```python
queryset = self.filter_queryset(self.get_queryset())

page = self.paginate_queryset(queryset)

if page is not None:
    serializer = self.get_serializer(page, many=True)
    return self.get_paginated_response(serializer.data)
```

অর্থাৎ `list()`-এ `paginate_queryset()` call হয়।

---

কিন্তু `RetrieveModelMixin`-এর `retrieve()` method-এ:

```python
instance = self.get_object()
serializer = self.get_serializer(instance)

return Response(serializer.data)
```

এখানে `paginate_queryset()` একেবারেই call হয় না।

---

## তাই Global Pagination থাকলেও

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "core.pagination.DefaultPagination",
    "PAGE_SIZE": 10,
}
```

এটি কাজ করবে:

```http
GET /products/
```

কিন্তু কাজ করবে না:

```http
GET /products/5/
```

এবং এটিই DRF-এর expected behavior।

---

### Interview Question

**Q:** Why doesn't DRF apply pagination on detail endpoints even when global pagination is enabled?

**A:** Because pagination is only applied inside the `list()` action (`ListModelMixin`) where a queryset containing multiple objects is returned. The `retrieve()` action (`RetrieveModelMixin`) returns a single object via `get_object()`, so there is nothing to paginate.
DRF-এ **default pagination** ব্যবহার করার দুটি উপায় আছে।

---

# 1. Global Default Pagination (Recommended)

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 10,
}
```

এখন সব `ListAPIView` এবং `ModelViewSet`-এ automatically pagination কাজ করবে।

---

# 2. নিজের Custom Pagination Class

`core/pagination.py`

```python
from rest_framework.pagination import PageNumberPagination

class DefaultPagination(PageNumberPagination):
    page_size = 10
    page_size_query_param = "page_size"
    max_page_size = 100
```

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "core.pagination.DefaultPagination",
}
```

এখন সব List API-তে এই class ব্যবহার হবে।

---

# Built-in Pagination Types

## 1. PageNumberPagination

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 10,
}
```

Request

```http
GET /products/?page=2
```

---

## 2. LimitOffsetPagination

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.LimitOffsetPagination",
    "PAGE_SIZE": 20,
}
```

Request

```http
GET /products/?limit=20&offset=40
```

---

## 3. CursorPagination

CursorPagination-এর `ordering` property দরকার, তাই এটিকে সরাসরি global default হিসেবে ব্যবহার করা যায় না।

প্রথমে একটি class বানান।

```python
from rest_framework.pagination import CursorPagination

class DefaultCursorPagination(CursorPagination):
    page_size = 20
    ordering = "-created_at"
```

তারপর

```python
REST_FRAMEWORK = {
    "DEFAULT_PAGINATION_CLASS": "core.pagination.DefaultCursorPagination",
}
```

Request

```http
GET /posts/?cursor=cD0yMDI2...
```

---

# Per View Override

যদি Global `PageNumberPagination` থাকে, কিন্তু একটি API-তে `CursorPagination` ব্যবহার করতে চান:

```python
from core.pagination import DefaultCursorPagination

class PostViewSet(ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
    pagination_class = DefaultCursorPagination
```

---

# Disable Pagination for One View

```python
class CategoryViewSet(ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer
    pagination_class = None
```

---

# Summary

| Requirement                        | Configuration                                                                       |
| ---------------------------------- | ----------------------------------------------------------------------------------- |
| Global Page Number                 | `DEFAULT_PAGINATION_CLASS = PageNumberPagination`                                   |
| Global Limit Offset                | `DEFAULT_PAGINATION_CLASS = LimitOffsetPagination`                                  |
| Global Cursor                      | Create a custom `CursorPagination` class, then set it as `DEFAULT_PAGINATION_CLASS` |
| One view uses different pagination | Set `pagination_class` on that view                                                 |
| Disable pagination for one view    | `pagination_class = None`                                                           |

### Production Recommendation

* **Admin dashboard / CRUD APIs:** `PageNumberPagination`
* **Search APIs:** `LimitOffsetPagination`
* **Social feed, notifications, chat:** `CursorPagination`

এটাই DRF-এ pagination configure করার standard এবং production-ready পদ্ধতি।
