অবশ্যই। এবার আমরা **Django REST Framework + Redis** একদম zero থেকে production-oriented level পর্যন্ত **৫টি lesson**-এ শিখব। প্রতিটি lesson-এ theory-এর পাশাপাশি বাস্তব implementation থাকবে।

# DRF + Redis — ৫ Lesson Complete Course

### আমাদের Project

আমরা একটা ছোট **E-commerce API** ধরে এগোব:

```text
E-commerce API
│
├── Authentication
├── Products
├── Search
├── Orders
└── Notifications
```

Redis আমরা বিভিন্ন জায়গায় ব্যবহার করব:

```text
                    Redis
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
     Cache         Throttle        Celery
       │              │              │
       ↓              ↓              ↓
    Products        API Limit      Background
    Search          Rate Limit       Tasks
```

---

# Lesson 1 — Redis Fundamentals + Django Connection

প্রথম lesson-এ শিখবে:

- Redis কী
    
- Redis কেন ব্যবহার করি
    
- Redis install
    
- Docker দিয়ে Redis চালানো
    
- Django-এর সাথে Redis connect করা
    
- `django-redis`
    
- `cache.set()`
    
- `cache.get()`
    
- `cache.delete()`
    
- TTL
    

### আমরা বানাব

```text
Django
  ↓
Django Cache API
  ↓
Redis
```

Example:

```python
from django.core.cache import cache

cache.set("username", "rahim", 60)

value = cache.get("username")

print(value)
```

Output:

```text
rahim
```

তারপর:

```python
cache.delete("username")
```

এ lesson-এর শেষে তুমি Django থেকে Redis-এ data রাখা এবং বের করা পারবে।

---

# Lesson 2 — DRF API Caching

এবার Redis-এর সবচেয়ে common use case:

> Database query কমিয়ে API response দ্রুত করা।

ধরো:

```text
GET /api/products/
```

Normally:

```text
Client
  ↓
DRF
  ↓
PostgreSQL
  ↓
Serializer
  ↓
Response
```

Redis cache করলে:

```text
Client
  ↓
DRF
  ↓
Redis
  │
  ├── Cache HIT → Response
  │
  └── Cache MISS
          ↓
      PostgreSQL
          ↓
        Redis
          ↓
       Response
```

Example:

```python
from django.core.cache import cache


class ProductListView(APIView):

    def get(self, request):

        products = cache.get("products")

        if products is not None:
            return Response(products)

        queryset = Product.objects.all()

        serializer = ProductSerializer(
            queryset,
            many=True
        )

        products = serializer.data

        cache.set(
            "products",
            products,
            timeout=300
        )

        return Response(products)
```

এখানে:

```text
300 seconds = 5 minutes
```

শিখবে:

- Cache key
    
- Cache hit
    
- Cache miss
    
- TTL
    
- API response caching
    
- Query optimization-এর সাথে caching-এর relationship
    

---

# Lesson 3 — Cache Invalidation + Advanced Caching

এটা Redis শেখার **সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি**।

ধরো Redis-এ:

```text
products
    ↓
Old product data
```

তারপর database-এ product update হলো।

```text
Database
    ↓
New data
```

কিন্তু Redis-এ:

```text
Old data
```

তখন API ভুল/পুরনো data দিতে পারে।

তাই শিখব:

### Cache invalidation

```python
cache.delete("products")
```

Product update:

```text
PUT /products/10/
      ↓
Database update
      ↓
Delete cache
      ↓
Next GET
      ↓
Database
      ↓
Fresh cache
```

এরপর advanced caching:

```text
products:all
products:10
products:20
products:category:5
products:search:laptop
```

শিখবে:

- Dynamic cache keys
    
- Object-level caching
    
- List caching
    
- Search caching
    
- Cache invalidation strategy
    
- Cache timeout strategy
    
- Cache stampede-এর basic concept
    

---

# Lesson 4 — DRF Throttling + Redis

এবার আমাদের আগের throttling lessons-এর সাথে Redis connect করব।

ধরো:

```text
Anonymous → 10/minute
User      → 100/minute
```

`settings.py`:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "10/minute",
        "user": "100/minute",
    },
}
```

Redis:

```text
DRF
 ↓
Throttle
 ↓
Django Cache
 ↓
Redis
```

তারপর scoped throttle:

```text
/login/
    ↓
5/minute

/search/
    ↓
30/minute

/products/
    ↓
100/minute
```

তারপর custom throttle:

```text
Normal user
    ↓
20/minute

Premium user
    ↓
100/minute
```

এই lesson-এ শিখবে:

- Redis-backed throttling
    
- `AnonRateThrottle`
    
- `UserRateThrottle`
    
- Scoped throttling
    
- Custom throttling
    
- Distributed server-এর ক্ষেত্রে shared Redis কেন দরকার
    
- `429 Too Many Requests`
    

---

# Lesson 5 — Redis + Celery + Production

শেষ lesson-এ Redis-এর সবচেয়ে powerful practical usage-এর একটা দেখব:

**Background tasks।**

ধরো:

```text
POST /api/orders/
```

Order create হওয়ার পর:

- Email পাঠাতে হবে
    
- Invoice generate করতে হবে
    
- Notification পাঠাতে হবে
    

সব request-এর মধ্যে করলে:

```text
Client
 ↓
DRF
 ↓
Order
 ↓
Email
 ↓
Invoice
 ↓
Notification
 ↓
Response
```

API slow হতে পারে।

Celery ব্যবহার করলে:

```text
Client
 ↓
DRF
 ↓
Create Order
 ↓
Response
 │
 └────→ Celery
           ↓
         Redis
           ↓
        Worker
           ↓
      Email/Invoice
```

এখানে Redis Celery-এর broker হিসেবে কাজ করতে পারে।

---

# Lesson 5-এর Project Architecture

শেষে আমাদের project হবে:

```text
                         Client
                           │
                           ▼
                         DRF
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
       API Cache       Throttling        Celery
          │                │                │
          └────────────────┼────────────────┘
                           ▼
                         Redis
                           │
                           ▼
                       PostgreSQL
```

Production-এ:

```text
                         Internet
                            │
                            ▼
                       Nginx / CDN
                            │
                            ▼
                     Django / DRF
                     /           \
                    /             \
                   ▼               ▼
                Redis          PostgreSQL
                  │
          ┌───────┴────────┐
          ▼                ▼
       Cache            Celery
                           │
                           ▼
                        Worker
```

এখানে শিখবে:

- Redis + Celery
    
- Background tasks
    
- Docker Compose
    
- Django + PostgreSQL + Redis + Celery
    
- Environment variables
    
- Production Redis configuration
    
- Redis security basics
    
- Shared Redis
    
- Monitoring-এর basic ধারণা
    
- কোন data Redis-এ রাখা উচিত/উচিত না
    

---

# পুরো Course-এর Practical Flow

আমরা একই E-commerce project-এ পাঁচটা lesson complete করব:

```text
LESSON 1
Redis + Django
     │
     ▼
Connection + Cache API
     │
     ▼
LESSON 2
DRF API Caching
     │
     ▼
Fast API responses
     │
     ▼
LESSON 3
Cache Invalidation
     │
     ▼
Correct + Fresh data
     │
     ▼
LESSON 4
DRF Throttling
     │
     ▼
Rate limiting
     │
     ▼
LESSON 5
Celery + Production
     │
     ▼
Background jobs
     │
     ▼
Production architecture
```

### শেষে তুমি এই ধরনের project বুঝতে পারবে

```text
                    E-COMMERCE API
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
        ▼                 ▼                 ▼
    Products           Search             Auth
        │                 │                 │
        └──────────┬──────┴─────────────────┘
                   ▼
                 Redis
             ┌─────┼─────┐
             │     │     │
             ▼     ▼     ▼
           Cache Throttle Celery
             │     │     │
             └─────┼─────┘
                   ▼
              PostgreSQL
```

**আমরা Lesson 1 → 2 → 3 → 4 → 5 এই order-এই করব।** Lesson 1-এ প্রথমে Redis install, Docker setup, Django configuration এবং `cache.set/get/delete` দিয়ে একটা working API বানানো দিয়ে শুরু করব।

---
# Lesson 1 — Redis + Django: Zero থেকে Connection

আজকের lesson-এ আমরা **Redis install → Django connect → Redis-এ data save/read/delete → TTL test** পর্যন্ত করব।

শেষে তোমার project-এর flow হবে:

```text
Django
   ↓
Django Cache API
   ↓
Redis
```

---

## 1. Redis আসলে কী?

Redis হলো খুব দ্রুত একটি **in-memory data store**।

Django সাধারণত database-এর জন্য PostgreSQL/MySQL ব্যবহার করে:

```text
Django → PostgreSQL
```

Redis যোগ করলে:

```text
Django → Redis
       → PostgreSQL
```

Redis সাধারণত ব্যবহার করা হয়:

* Cache
* Throttling/rate limiting
* Session
* Celery broker
* Temporary data
* Frequently accessed data

আজ আমরা **Cache** দিয়ে শুরু করব।

---

# 2. Project তৈরি করি

যদি নতুন project হয়:

```bash
mkdir drf_redis
cd drf_redis

python -m venv venv
```

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

তারপর:

```bash
pip install django djangorestframework django-redis redis
```

Project:

```bash
django-admin startproject config .
python manage.py startapp api
```

Structure:

```text
drf_redis/
│
├── manage.py
├── config/
│   ├── settings.py
│   └── urls.py
│
└── api/
    ├── views.py
    └── ...
```

---

# 3. Redis চালু করি

Development-এর জন্য Docker ব্যবহার করলে সবচেয়ে সহজ:

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:7
```

Check:

```bash
docker ps
```

তারপর Redis-এর ভিতরে ping:

```bash
docker exec -it redis redis-cli ping
```

Expected:

```text
PONG
```

এটার অর্থ Redis successfully চলছে।

---

# 4. Django-তে Redis configure

`config/settings.py`-তে:

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        },
    },
}
```

এখন Django জানে:

```text
Cache
  ↓
django-redis
  ↓
Redis
  ↓
127.0.0.1:6379
```

---

# 5. Django থেকে Redis test করি

Terminal:

```bash
python manage.py shell
```

তারপর:

```python
from django.core.cache import cache
```

এখন একটা value save করি:

```python
cache.set("name", "Rahim", 60)
```

এখানে:

```text
"name"
   ↓
"Rahim"
```

এবং `60` হচ্ছে TTL:

```text
60 seconds
```

---

# 6. Redis থেকে data read

```python
cache.get("name")
```

Output:

```text
'Rahim'
```

অর্থাৎ:

```text
Django
  ↓
cache.get()
  ↓
Redis
  ↓
Rahim
```

---

# 7. TTL কী?

TTL = **Time To Live**

আমরা লিখেছি:

```python
cache.set("name", "Rahim", 60)
```

মানে value সর্বোচ্চ 60 seconds থাকবে।

Check করতে পারো:

```python
cache.ttl("name")
```

কিছু ক্ষেত্রে remaining seconds-এর কাছাকাছি value পাবে।

60 seconds পরে:

```python
cache.get("name")
```

হলে:

```text
None
```

কারণ cache expire হয়ে গেছে।

---

# 8. Data delete করা

```python
cache.delete("name")
```

তারপর:

```python
cache.get("name")
```

Result:

```text
None
```

---

# 9. এবার একটা API বানাই

`api/views.py`:

```python
from django.core.cache import cache
from rest_framework.views import APIView
from rest_framework.response import Response


class RedisTestView(APIView):

    def get(self, request):

        cache.set(
            "message",
            "Hello from Redis",
            60
        )

        message = cache.get("message")

        return Response({
            "message": message
        })
```

`config/urls.py`:

```python
from django.contrib import admin
from django.urls import path
from api.views import RedisTestView


urlpatterns = [
    path("admin/", admin.site.urls),
    path("redis-test/", RedisTestView.as_view()),
]
```

Server:

```bash
python manage.py runserver
```

তারপর:

```text
GET http://127.0.0.1:8000/redis-test/
```

Response:

```json
{
    "message": "Hello from Redis"
}
```

---

# 10. কিন্তু এটা এখনো খুব useful example না

কারণ প্রতিবার API call করলে আমরা আবার:

```python
cache.set(...)
```

করছি।

Real application-এ সাধারণত pattern হবে:

```text
Request
   ↓
Cache আছে?
  / \
Yes  No
 |    |
 ↓    ↓
Return Database
      ↓
    Cache
      ↓
    Return
```

অর্থাৎ:

```python
data = cache.get("some_key")

if data is not None:
    return data

# Database থেকে data আনো

cache.set("some_key", data, 300)

return data
```

এই pattern-টাই **Lesson 2-এর মূল বিষয়: DRF API caching**।

---

# 11. Redis সরাসরি দেখতে চাইলে

Docker container-এর Redis CLI:

```bash
docker exec -it redis redis-cli
```

তারপর:

```text
KEYS *
```

তুমি Django থেকে তৈরি করা key দেখতে পারো।

যেমন:

```text
1) "name"
```

তারপর:

```text
GET name
```

যদি value এখনো থাকে:

```text
"Rahim"
```

TTL:

```text
TTL name
```

এতে remaining seconds দেখাবে।

---

# 12. একটা গুরুত্বপূর্ণ বিষয়: `KEYS *`

Development-এ:

```text
KEYS *
```

দিয়ে দেখতে সমস্যা নেই।

কিন্তু বড় production Redis-এ অনেক key থাকলে `KEYS *` ব্যবহার করা উচিত নয়, কারণ এটা potentially expensive হতে পারে।

Production debugging/inspection-এর ক্ষেত্রে Redis-এর `SCAN` family ব্যবহার করা বেশি উপযুক্ত।

এটা এখন শুধু concept হিসেবে মনে রাখো।

---

# 13. Redis connection test করার complete flow

তোমার এখন এই flow কাজ করা উচিত:

```text
                 Django
                   │
                   ▼
             cache.set()
                   │
                   ▼
                 Redis
                   │
                   ▼
             cache.get()
                   │
                   ▼
                Django
                   │
                   ▼
                Response
```

---

# 14. আজকের code summary

### Install

```bash
pip install django djangorestframework django-redis redis
```

### Redis

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:7
```

### Django settings

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        },
    },
}
```

### Python

```python
from django.core.cache import cache

cache.set("name", "Rahim", 60)

print(cache.get("name"))

cache.delete("name")
```

---

## Lesson 1 শেষে তোমার যা clear হওয়া উচিত

```text
Redis
 ↓
Fast in-memory data store

Django Cache
 ↓
Redis-এর সাথে সহজ interface

cache.set()
 ↓
Data save

cache.get()
 ↓
Data read

cache.delete()
 ↓
Data remove

TTL
 ↓
কতক্ষণ data থাকবে
```

### ছোট Practice

নিজে এই তিনটা test করো:

```python
cache.set("course", "DRF", 120)
cache.get("course")
cache.delete("course")
```

তারপর Redis CLI থেকে key দেখতে চেষ্টা করো।

**Lesson 2-তে আমরা এই foundation ব্যবহার করে `GET /products/` API-কে Redis cache করব—প্রথম request database থেকে data নেবে, পরের request Redis থেকে নেবে।**

---
# Lesson 2 — DRF API Caching with Redis

Lesson 1-এ আমরা Django ↔ Redis connection করেছি। এবার সেটাকে **বাস্তব DRF API-তে ব্যবহার** করব।

আজকের লক্ষ্য:

```text
GET /api/products/

First request
    ↓
Redis MISS
    ↓
Database
    ↓
Redis-এ save
    ↓
Response

Second request
    ↓
Redis HIT
    ↓
Response
```

অর্থাৎ একই data বারবার database থেকে আনতে হবে না।

---

# 1. আমরা কী বানাব?

একটা simple Product API:

```text
GET /api/products/
```

Database:

```text
Product
├── id
├── name
└── price
```

Redis:

```text
products:list
       ↓
cached product data
```

---

# 2. Product model তৈরি করি

`api/models.py`

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    def __str__(self):
        return self.name
```

Migration:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# 3. কিছু product তৈরি করি

সহজভাবে Django shell:

```bash
python manage.py shell
```

```python
from api.models import Product

Product.objects.create(
    name="Laptop",
    price=80000
)

Product.objects.create(
    name="Keyboard",
    price=3000
)

Product.objects.create(
    name="Mouse",
    price=1500
)
```

Check:

```python
Product.objects.all()
```

---

# 4. Serializer তৈরি করি

`api/serializers.py`

```python
from rest_framework import serializers
from .models import Product


class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
        ]
```

---

# 5. প্রথমে normal API বানাই

`api/views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .models import Product
from .serializers import ProductSerializer


class ProductListView(APIView):

    def get(self, request):

        products = Product.objects.all()

        serializer = ProductSerializer(
            products,
            many=True
        )

        return Response(serializer.data)
```

URL:

```python
from django.urls import path
from api.views import ProductListView


urlpatterns = [
    path(
        "products/",
        ProductListView.as_view()
    ),
]
```

এখন:

```text
GET /products/
```

Response:

```json
[
    {
        "id": 1,
        "name": "Laptop",
        "price": "80000.00"
    },
    {
        "id": 2,
        "name": "Keyboard",
        "price": "3000.00"
    }
]
```

কিন্তু প্রতিবার:

```text
Request
   ↓
PostgreSQL
   ↓
Serializer
   ↓
Response
```

হচ্ছে।

এবার Redis যোগ করি।

---

# 6. Redis cache যোগ করি

`views.py`:

```python
from django.core.cache import cache

from rest_framework.views import APIView
from rest_framework.response import Response

from .models import Product
from .serializers import ProductSerializer


class ProductListView(APIView):

    def get(self, request):

        cached_products = cache.get(
            "products:list"
        )

        if cached_products is not None:

            return Response(cached_products)

        products = Product.objects.all()

        serializer = ProductSerializer(
            products,
            many=True
        )

        data = serializer.data

        cache.set(
            "products:list",
            data,
            timeout=300
        )

        return Response(data)
```

এখানে:

```python
cached_products = cache.get("products:list")
```

প্রথমে Redis-এ খুঁজবে।

---

# 7. First request কী হবে?

ধরো Redis একদম empty।

```text
GET /products/
        ↓
Redis
        ↓
MISS
        ↓
PostgreSQL
        ↓
Serializer
        ↓
Redis SET
        ↓
Response
```

Redis-এ তখন:

```text
products:list
      ↓
[
   Laptop,
   Keyboard,
   Mouse
]
```

save হবে।

---

# 8. Second request

এবার আবার:

```text
GET /products/
```

Flow:

```text
Request
   ↓
Redis
   ↓
HIT
   ↓
Return cached data
```

Database query হবে না।

এটাই caching-এর মূল benefit।

---

# 9. Cache Hit / Cache Miss

দুইটা শব্দ খুব ভালোভাবে মনে রাখো।

### Cache MISS

Redis-এ data নেই:

```text
Redis
 ↓
❌ No data
 ↓
Database
```

### Cache HIT

Redis-এ data আছে:

```text
Redis
 ↓
✅ Data found
 ↓
Return
```

Flow:

```text
             GET /products/
                    │
                    ▼
                 Redis
                /     \
             HIT       MISS
              │          │
              ▼          ▼
          Response    Database
                         │
                         ▼
                       Redis
                         │
                         ▼
                      Response
```

---

# 10. TTL কীভাবে কাজ করছে?

আমরা লিখেছি:

```python
cache.set(
    "products:list",
    data,
    timeout=300
)
```

মানে:

```text
300 seconds
=
5 minutes
```

৫ মিনিট পরে Redis cache automatically expire করবে।

তারপর:

```text
GET /products/
      ↓
Redis MISS
      ↓
Database
      ↓
New cache
```

---

# 11. Redis থেকে verify করি

Redis CLI:

```bash
docker exec -it redis redis-cli
```

তারপর:

```text
SCAN 0
```

তোমার key দেখতে পারো:

```text
products:list
```

তারপর TTL:

```text
TTL products:list
```

যেমন:

```text
287
```

মানে প্রায় 287 seconds বাকি।

---

# 12. কিন্তু একটা বড় সমস্যা আছে

ধরো Redis-এ:

```text
products:list
    ↓
Laptop
Keyboard
Mouse
```

এখন database-এ নতুন product যোগ করলাম:

```text
Monitor
```

Database:

```text
Laptop
Keyboard
Mouse
Monitor
```

কিন্তু Redis:

```text
Laptop
Keyboard
Mouse
```

তাহলে API এখনও পুরনো data দিতে পারে।

এটাকে বলে **stale cache**।

এখানে আসে:

# Cache Invalidation

এটা আমরা Lesson 3-এ বিস্তারিত করব।

---

# 13. এখন basic invalidation বুঝে রাখো

Product create/update/delete হলে:

```python
cache.delete("products:list")
```

যেমন:

```python
product = Product.objects.create(
    name="Monitor",
    price=20000
)

cache.delete("products:list")
```

এরপর next GET:

```text
GET /products/
     ↓
Redis MISS
     ↓
Database
     ↓
Monitor সহ নতুন data
     ↓
Redis
```

---

# 14. Cache key কেন important?

আমরা ব্যবহার করছি:

```python
"products:list"
```

এটাকে **cache key** বলে।

Different data হলে different key:

```text
products:list
products:1
products:2
products:category:5
products:search:laptop
```

Example:

```python
cache.set(
    "products:1",
    product_data,
    300
)
```

এতে product ID 1-এর data রাখা হচ্ছে।

---

# 15. User-specific data হলে সাবধান

ধরো:

```text
GET /profile/
```

এখানে যদি blindly:

```python
cache.get("profile")
```

ব্যবহার করো, তাহলে বিপজ্জনক সমস্যা হতে পারে।

কারণ:

```text
User A
  ↓
profile
  ↓
Redis

User B
  ↓
same "profile" key
  ↓
User A-এর data পেয়ে যেতে পারে
```

তাই user-specific cache key:

```python
key = f"profile:{request.user.id}"
```

যেমন:

```text
profile:10
profile:25
profile:51
```

এটা খুব গুরুত্বপূর্ণ production concept।

---

# 16. Query parameter থাকলে?

ধরো:

```text
/products/?category=5
```

আর:

```text
/products/?category=10
```

দুইটা আলাদা result।

তাই একই key:

```text
products:list
```

ব্যবহার করা যাবে না।

Dynamic key করতে হবে:

```python
category = request.query_params.get("category")

cache_key = f"products:category:{category}"
```

তাহলে:

```text
/products/?category=5
```

হবে:

```text
products:category:5
```

আর:

```text
/products/?category=10
```

হবে:

```text
products:category:10
```

---

# 17. Production-এ আরেকটা important issue

ধরো একই সময়ে 100টা request এলো এবং cache empty:

```text
Request 1 ─┐
Request 2 ─┤
Request 3 ─┤
Request 4 ─┤
...        ├──→ Redis MISS
Request 100┘
```

সবগুলো database query করতে পারে।

এ ধরনের সমস্যাকে broadly **cache stampede / thundering herd** বলা হয়।

Basic project-এ এখন এটা নিয়ে implementation করার দরকার নেই, কিন্তু production-level Redis শেখার সময় conceptটা জানা গুরুত্বপূর্ণ।

---

# 18. API caching কখন ব্যবহার করবে?

সব API cache করা উচিত না।

### ভালো candidate:

```text
GET /products/
GET /categories/
GET /public-settings/
GET /popular-products/
```

যেখানে:

* একই data বারবার আসে
* data frequently পরিবর্তন হয় না
* database query expensive

### সাবধানতার সাথে:

```text
GET /profile/
GET /orders/
GET /dashboard/
```

এগুলো user-specific এবং frequently changing হতে পারে।

Cache key ও invalidation strategy carefully design করতে হবে।

---

# 19. আজকের complete flow

```text
                  GET /products/
                         │
                         ▼
                      Django
                         │
                         ▼
                       Redis
                     /       \
                  HIT         MISS
                   │            │
                   │            ▼
                   │        PostgreSQL
                   │            │
                   │            ▼
                   │         Serializer
                   │            │
                   │            ▼
                   │          Redis
                   │            │
                   └──────┬─────┘
                          ▼
                       Response
```

---

# 20. আজকের গুরুত্বপূর্ণ code

```python
from django.core.cache import cache


class ProductListView(APIView):

    def get(self, request):

        cached_products = cache.get(
            "products:list"
        )

        if cached_products is not None:
            return Response(cached_products)

        products = Product.objects.all()

        serializer = ProductSerializer(
            products,
            many=True
        )

        data = serializer.data

        cache.set(
            "products:list",
            data,
            timeout=300
        )

        return Response(data)
```

এটাই তোমার **basic Redis-backed DRF caching pattern**।

---

## Lesson 2 শেষে তোমার যা পরিষ্কার হওয়া উচিত

```text
cache.get()
    ↓
Cache আছে?

YES → return

NO
 ↓
Database
 ↓
Serializer
 ↓
cache.set()
 ↓
return
```

এবং এই concepts:

* Cache hit
* Cache miss
* Cache key
* TTL
* Stale cache
* Dynamic cache key
* User-specific cache key
* Basic cache stampede concept

**Lesson 3-এ আমরা এই API-টাকে properভাবে production-friendly করব: Product Create/Update/Delete-এর পর কীভাবে cache invalidate করতে হয়, object-level cache, dynamic keys, query-parameter cache এবং cache consistency কীভাবে manage করতে হয়।**


---
# Lesson 3 — Cache Invalidation + Advanced Caching

Lesson 2-এ আমরা শিখেছি:

```text
GET /products/

Redis HIT  → cached data
Redis MISS → Database → Redis → Response
```

আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়:

> **Database-এর data পরিবর্তন হলে Redis-এর পুরোনো data কীভাবে ঠিক রাখবে?**

এটাকেই বলে **Cache Invalidation**।

---

# 1. Cache Invalidation কী?

ধরো Redis-এ আছে:

```text
products:list
    ↓
Laptop
Keyboard
Mouse
```

এখন database-এ নতুন product তৈরি করলে:

```text
Database:
Laptop
Keyboard
Mouse
Monitor
```

কিন্তু Redis এখনও:

```text
Laptop
Keyboard
Mouse
```

তাহলে API পুরোনো data দিতে পারে।

তাই database পরিবর্তনের পরে:

```python
cache.delete("products:list")
```

করতে হবে।

Flow:

```text
CREATE Product
     ↓
Database updated
     ↓
Delete old cache
     ↓
Next GET
     ↓
Redis MISS
     ↓
Database
     ↓
New cache
```

---

# 2. Product Create API

আমরা একটা complete CRUD example বানাব।

`api/views.py`

```python
from django.core.cache import cache

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .models import Product
from .serializers import ProductSerializer
```

তারপর:

```python
class ProductCreateView(APIView):

    def post(self, request):

        serializer = ProductSerializer(
            data=request.data
        )

        serializer.is_valid(raise_exception=True)

        product = serializer.save()

        # Old product list cache remove
        cache.delete("products:list")

        return Response(
            ProductSerializer(product).data,
            status=status.HTTP_201_CREATED
        )
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

```python
cache.delete("products:list")
```

Product create হওয়ার পর পুরোনো list cache আর রাখা হচ্ছে না।

---

# 3. Product Update

এবার ধরো:

```text
Laptop
price = 80000
```

Update করে:

```text
Laptop
price = 75000
```

Redis-এ পুরোনো price থাকতে পারে।

তাই update-এর পর cache delete করতে হবে।

```python
class ProductDetailView(APIView):

    def put(self, request, pk):

        try:
            product = Product.objects.get(pk=pk)

        except Product.DoesNotExist:
            return Response(
                {"detail": "Product not found"},
                status=status.HTTP_404_NOT_FOUND
            )

        serializer = ProductSerializer(
            product,
            data=request.data
        )

        serializer.is_valid(
            raise_exception=True
        )

        product = serializer.save()

        cache.delete("products:list")
        cache.delete(f"product:{pk}")

        return Response(
            ProductSerializer(product).data
        )
```

এখানে দুইটা cache delete করছি:

```python
cache.delete("products:list")
cache.delete(f"product:{pk}")
```

কারণ আমাদের list cache এবং individual product cache—দুটোই থাকতে পারে।

---

# 4. Individual Product Cache

Lesson 2-এ আমরা শুধু:

```text
products:list
```

cache করেছিলাম।

এবার individual product cache করি।

API:

```text
GET /products/1/
```

Cache key:

```text
product:1
```

View:

```python
class ProductDetailView(APIView):

    def get(self, request, pk):

        cache_key = f"product:{pk}"

        cached_product = cache.get(cache_key)

        if cached_product is not None:
            return Response(cached_product)

        try:
            product = Product.objects.get(pk=pk)

        except Product.DoesNotExist:
            return Response(
                {"detail": "Product not found"},
                status=status.HTTP_404_NOT_FOUND
            )

        serializer = ProductSerializer(product)

        data = serializer.data

        cache.set(
            cache_key,
            data,
            timeout=300
        )

        return Response(data)
```

এখন flow:

```text
GET /products/1/
        ↓
Redis
        ↓
product:1
    ┌───────┴───────┐
   HIT             MISS
    ↓                ↓
Response          Database
                     ↓
                   Redis
                     ↓
                  Response
```

---

# 5. List cache + Detail cache

এখন আমাদের Redis-এ থাকতে পারে:

```text
products:list

product:1
product:2
product:3
```

ধরো Product 1 update হলো।

তাহলে শুধু:

```python
cache.delete("product:1")
```

করলে হবে না।

কারণ:

```text
products:list
```

এর মধ্যেও Product 1-এর পুরোনো data থাকতে পারে।

তাই:

```python
cache.delete("product:1")
cache.delete("products:list")
```

দুটোই invalidate করা উচিত।

---

# 6. DELETE-এর ক্ষেত্রে কী হবে?

Product delete:

```python
class ProductDeleteView(APIView):

    def delete(self, request, pk):

        try:
            product = Product.objects.get(pk=pk)

        except Product.DoesNotExist:
            return Response(
                {"detail": "Product not found"},
                status=status.HTTP_404_NOT_FOUND
            )

        product.delete()

        cache.delete(f"product:{pk}")
        cache.delete("products:list")

        return Response(
            status=status.HTTP_204_NO_CONTENT
        )
```

Flow:

```text
DELETE Product 1
       ↓
Database delete
       ↓
Redis delete
       ↓
product:1 ❌
products:list ❌
```

---

# 7. Cache Invalidation-এর একটা rule

খুব গুরুত্বপূর্ণ pattern:

```text
WRITE
 ↓
Database
 ↓
Invalidate cache
```

অর্থাৎ:

### Create

```python
database create
      ↓
cache.delete(...)
```

### Update

```python
database update
      ↓
cache.delete(...)
```

### Delete

```python
database delete
      ↓
cache.delete(...)
```

আর GET:

```text
Redis
 ↓
HIT → return

MISS
 ↓
Database
 ↓
Redis SET
 ↓
return
```

এটা মনে রাখলে Redis caching-এর বড় একটা অংশ clear হয়ে যাবে।

---

# 8. Dynamic Cache Key

এখন ধরো API:

```text
/products/?category=5
```

এবং:

```text
/products/?category=10
```

দুটোর result আলাদা।

তাই:

```python
category = request.query_params.get("category")

cache_key = f"products:category:{category}"
```

Example:

```text
products:category:5
products:category:10
products:category:20
```

---

# 9. Search API cache

ধরো:

```text
GET /products/?search=laptop
```

Cache key:

```python
search = request.query_params.get(
    "search",
    ""
).strip().lower()

cache_key = f"products:search:{search}"
```

তাহলে:

```text
products:search:laptop
products:search:keyboard
products:search:mouse
```

আলাদা cache হবে।

---

# 10. কিন্তু একটা সমস্যা

ধরো:

```text
products:search:laptop
products:search:phone
products:search:keyboard
products:category:5
products:category:10
...
```

একটা নতুন Product তৈরি হলে কোন কোন cache delete করবে?

সবগুলো manually track করা কঠিন।

এখানে আমরা **cache versioning** বা **key pattern strategy** ব্যবহার করতে পারি।

---

# 11. Cache Namespace

একটা common prefix ব্যবহার করা ভালো:

```text
product:v1:list
product:v1:1
product:v1:2
product:v1:search:laptop
```

এতে application-এর cache keys organized থাকে।

Example:

```python
CACHE_PREFIX = "product:v1"
```

তারপর:

```python
cache_key = f"{CACHE_PREFIX}:list"
```

Individual:

```python
cache_key = f"{CACHE_PREFIX}:{pk}"
```

Search:

```python
cache_key = f"{CACHE_PREFIX}:search:{search}"
```

এতে বড় project-এ key management সহজ হয়।

---

# 12. Cache Versioning

ধরো:

```text
product:v1:list
```

পরে cache structure পরিবর্তন করলে:

```text
product:v2:list
```

ব্যবহার করতে পারো।

তখন পুরোনো:

```text
product:v1:*
```

তাৎক্ষণিকভাবে application-এর নতুন code আর ব্যবহার করবে না।

এটা বড় application-এ useful technique।

---

# 13. `cache.get_or_set()`

Django cache API-তে একটা useful method আছে:

```python
cache.get_or_set()
```

যখন:

```text
GET
 ↓
cache.get()
 ↓
None?
 ↓
database
 ↓
cache.set()
```

এই pattern বারবার লিখতে না চাইলে `get_or_set()` ব্যবহার করা যায়।

Example:

```python
data = cache.get_or_set(
    "products:list",
    lambda: ProductSerializer(
        Product.objects.all(),
        many=True
    ).data,
    timeout=300
)
```

তারপর:

```python
return Response(data)
```

Conceptually:

```text
Cache আছে?
   ↓
 YES → return cache

 NO
 ↓
lambda execute
 ↓
Database
 ↓
Cache
 ↓
return
```

তবে complex query/business logic হলে explicit `get()` + `set()` অনেক সময় বেশি readable।

---

# 14. Object-level caching

List:

```text
products:list
```

Individual:

```text
product:1
```

Category:

```text
products:category:5
```

Search:

```text
products:search:laptop
```

এগুলো বিভিন্ন **cache granularity**।

অর্থাৎ কোন level-এর data cache করবে সেটা application অনুযায়ী ঠিক করতে হবে।

---

# 15. TTL নির্বাচন

সব cache-এর TTL একই হওয়া দরকার নেই।

Example:

```text
Product list
    ↓
5 minutes

Product detail
    ↓
10 minutes

Category list
    ↓
1 hour

Static configuration
    ↓
Several hours
```

এগুলো fixed rule নয়—তোমার application's data-change frequency অনুযায়ী TTL ঠিক করবে।

---

# 16. `cache.delete_many()`

একাধিক known key delete করতে চাইলে:

```python
cache.delete_many([
    "products:list",
    "product:1",
    "product:2",
])
```

এটা useful যখন তুমি একসাথে কয়েকটা cache invalidate করতে জানো।

---

# 17. Redis-এ cache manually inspect

Docker Redis:

```bash
docker exec -it redis redis-cli
```

তারপর development environment-এ:

```text
SCAN 0
```

Key-এর value inspect করার জন্য data type অনুযায়ী Redis command লাগে। Django cache backend-এর implementation/serialization-এর কারণে raw value সবসময় human-readable নাও হতে পারে।

TTL:

```text
TTL products:list
```

---

# 18. `KEYS *` কেন avoid করব?

Development-এ:

```text
KEYS *
```

দিয়ে সব key দেখা যায়।

কিন্তু বড় production Redis-এ অনেক key থাকলে `KEYS *` expensive হতে পারে।

Production debugging-এর জন্য সাধারণত:

```text
SCAN
```

ব্যবহার করা safer approach।

---

# 19. সবচেয়ে গুরুত্বপূর্ণ architecture

এখন আমাদের Product API:

```text
                 Client
                   │
                   ▼
              Django REST
                   │
             ┌─────┴─────┐
             │           │
            GET        WRITE
             │           │
             ▼           ▼
           Redis      Database
          /     \         │
       HIT      MISS      ▼
        │         │    Invalidate
        │         ▼         │
        │      Database     │
        │         │         │
        │         ▼         │
        │       Redis ◄─────┘
        │
        ▼
     Response
```

এই architecture-টাই Lesson 2 + Lesson 3-এর মূল বিষয়।

---

# 20. একটি Complete Example

একটা list endpoint:

```python
from django.core.cache import cache

from rest_framework.views import APIView
from rest_framework.response import Response

from .models import Product
from .serializers import ProductSerializer


class ProductListView(APIView):

    def get(self, request):

        cache_key = "products:list"

        data = cache.get(cache_key)

        if data is not None:
            return Response(data)

        products = Product.objects.all()

        serializer = ProductSerializer(
            products,
            many=True
        )

        data = serializer.data

        cache.set(
            cache_key,
            data,
            timeout=300
        )

        return Response(data)

    def post(self, request):

        serializer = ProductSerializer(
            data=request.data
        )

        serializer.is_valid(
            raise_exception=True
        )

        product = serializer.save()

        # Invalidate list cache
        cache.delete("products:list")

        return Response(
            ProductSerializer(product).data,
            status=201
        )
```

এখানে খুব সুন্দর একটা pattern দেখতে পাচ্ছ:

```text
GET
 ↓
Cache first
 ↓
MISS হলে DB
 ↓
Cache set


POST
 ↓
DB write
 ↓
Cache invalidate
```

---

# 21. আজকের Golden Rule ⭐

Redis caching-এর সবচেয়ে গুরুত্বপূর্ণ rule:

```text
READ  → Cache first
WRITE → Database first + invalidate cache
```

অর্থাৎ:

```text
GET
Cache → DB fallback


POST/PUT/PATCH/DELETE
DB → Cache invalidation
```

এটা ভালোভাবে বুঝে গেলে DRF + Redis caching-এর foundation অনেক strong হয়ে যাবে।

---

# Lesson 3 Summary

আজ আমরা শিখলাম:

```text
1. Cache Invalidation
2. Create-এর পর cache delete
3. Update-এর পর cache delete
4. Delete-এর পর cache delete
5. Individual object cache
6. Dynamic cache key
7. Search cache
8. Cache namespace
9. Cache versioning
10. get_or_set()
11. delete_many()
12. TTL strategy
13. Cache stampede concept
14. Redis key inspection
```

### পুরো Redis caching pattern:

```text
              READ
               ↓
             Redis
           /       \
        HIT         MISS
         ↓            ↓
      Response      Database
                       ↓
                     Redis
                       ↓
                    Response


             WRITE
               ↓
            Database
               ↓
       Invalidate Cache
```

**Lesson 4-এ আমরা Redis দিয়ে DRF Throttling করব**—অর্থাৎ `AnonRateThrottle`, `UserRateThrottle`, scoped throttle এবং multiple Django server-এর ক্ষেত্রে Redis কীভাবে shared rate-limit storage হিসেবে কাজ করে সেটা হাতে-কলমে করব।

---
# Lesson 4 — DRF Throttling + Redis

এখন পর্যন্ত আমরা শিখেছি:

```text
Lesson 1 → Django ↔ Redis connection
Lesson 2 → DRF API caching
Lesson 3 → Cache invalidation
```

আজকের Lesson 4-এ আমরা Redis-কে **DRF throttling-এর shared storage** হিসেবে ব্যবহার করব।

---

# 1. কেন Redis + DRF Throttling?

DRF-এর throttling সাধারণত Django-এর **cache system** ব্যবহার করে।

আমরা যদি cache backend হিসেবে Redis configure করি:

```text
DRF Throttle
     ↓
Django Cache
     ↓
Redis
```

তাহলে throttle state Redis-এ রাখা যাবে।

এটা বিশেষ করে গুরুত্বপূর্ণ যখন তোমার একাধিক Django server থাকে:

```text
                Load Balancer
                 /          \
                ↓            ↓
           Django #1     Django #2
                \            /
                 \          /
                    Redis
```

দুই server-ই একই Redis ব্যবহার করলে তারা একই rate-limit state দেখতে পারে।

---

# 2. আগে Redis configuration

Lesson 1-এ করা configuration-টাই থাকবে।

`settings.py`

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        },
    },
}
```

DRF:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "5/minute",
        "user": "20/minute",
    },
}
```

এখন:

```text
Anonymous → 5 requests/minute
User       → 20 requests/minute
```

---

# 3. এই flow-টা বুঝো

একজন anonymous user request করল:

```text
GET /products/
      ↓
DRF
      ↓
Throttle check
      ↓
Django Cache
      ↓
Redis
```

Redis দেখে:

```text
এই client কতবার request করেছে?
```

যদি limit-এর মধ্যে থাকে:

```text
ALLOW
```

না হলে:

```text
429 Too Many Requests
```

---

# 4. Simple API তৈরি করি

`api/views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response


class ProductListView(APIView):

    def get(self, request):
        return Response({
            "message": "Products returned"
        })
```

Global throttle settings থাকার কারণে আলাদা করে throttle লিখতে হবে না।

Request:

```text
GET /products/
```

Anonymous user হলে প্রথম কয়েকটি request allow হবে।

---

# 5. 429 কী?

Limit cross করলে response:

```http
HTTP 429 Too Many Requests
```

Example:

```json
{
    "detail": "Request was throttled. Expected available in 42 seconds."
}
```

মানে server বলছে:

> এখন আর request করা যাবে না; কিছুক্ষণ পরে আবার চেষ্টা করো।

---

# 6. Scoped Throttling + Redis

এবার real-world API বানাই।

ধরো:

```text
Login
Search
Product
```

সব endpoint-এর একই limit দরকার নেই।

আমরা তৈরি করব:

```text
login  → 5/minute
search → 30/minute
product → 100/minute
```

---

# 7. Custom scoped throttle

`api/throttles.py`

```python
from rest_framework.throttling import (
    AnonRateThrottle,
    UserRateThrottle,
)


class LoginThrottle(AnonRateThrottle):
    scope = "login"


class SearchThrottle(UserRateThrottle):
    scope = "search"


class ProductThrottle(UserRateThrottle):
    scope = "product"
```

---

# 8. Settings

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_RATES": {
        "login": "5/minute",
        "search": "30/minute",
        "product": "100/minute",
    }
}
```

এখানে একটা গুরুত্বপূর্ণ বিষয়:

```python
LoginThrottle(AnonRateThrottle)
```

ব্যবহার করেছি কারণ login করার আগে সাধারণত user authenticated থাকে না।

---

# 9. Login API

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .throttles import LoginThrottle


class LoginView(APIView):

    throttle_classes = [
        LoginThrottle
    ]

    def post(self, request):

        return Response({
            "message": "Login endpoint"
        })
```

Flow:

```text
POST /login/
      ↓
LoginThrottle
      ↓
Redis
      ↓
limit check
```

---

# 10. Search API

```python
from .throttles import SearchThrottle


class SearchView(APIView):

    throttle_classes = [
        SearchThrottle
    ]

    def get(self, request):

        query = request.query_params.get(
            "q",
            ""
        )

        return Response({
            "query": query
        })
```

এখন:

```text
GET /search/?q=laptop
```

এর জন্য:

```text
30 requests/minute
```

---

# 11. Product API

```python
from .throttles import ProductThrottle


class ProductView(APIView):

    throttle_classes = [
        ProductThrottle
    ]

    def get(self, request):

        return Response({
            "message": "Product data"
        })
```

Limit:

```text
100 requests/minute
```

---

# 12. Redis কোথায় কাজ করছে?

Conceptually:

```text
                    Django
                       │
                       ▼
                  DRF Throttle
                       │
                       ▼
                 Django Cache API
                       │
                       ▼
                     Redis
                       │
              ┌────────┴────────┐
              │                 │
           request count     expiry/TTL
```

DRF নিজে সরাসরি Redis API লিখছে না।

বরং:

```text
DRF
 ↓
Django cache
 ↓
Redis backend
```

এই architecture ব্যবহার করছে।

---

# 13. Multiple Django Server হলে আসল benefit

ধরো তোমার দুইটা server:

```text
Server 1
Server 2
```

### Redis ছাড়া local cache হলে

একজন user:

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 1
Request 4 → Server 2
```

Server দুটো যদি আলাদা local cache/state ব্যবহার করে, rate-limit state আলাদা হতে পারে।

ফলে distributed environment-এ consistent throttling কঠিন হতে পারে।

### Redis shared হলে

```text
             Load Balancer
              /         \
             ↓           ↓
        Django #1    Django #2
             \           /
              \         /
                 Redis
```

দুই server একই Redis state দেখে।

এটাই Redis-backed distributed throttling-এর বড় সুবিধা।

---

# 14. Rate Limit Design

সব endpoint-এ একই rate দেওয়া ভালো strategy নাও হতে পারে।

Example:

```text
Endpoint             Rate

Login                5/minute
Search               30/minute
Product list         100/minute
Expensive report     10/minute
```

কেন?

কারণ API endpoint-এর resource cost আলাদা হতে পারে।

যেমন:

```text
GET /health/
```

এবং:

```text
POST /expensive-report/
```

একই ধরনের resource usage তৈরি করে না।

---

# 15. Authentication + Throttling

ধরো:

```text
Anonymous
→ 5/minute

Authenticated
→ 100/minute
```

Settings:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "5/minute",
        "user": "100/minute",
    },
}
```

Flow:

```text
Anonymous request
      ↓
AnonRateThrottle
      ↓
5/min


Authenticated request
      ↓
UserRateThrottle
      ↓
100/min
```

---

# 16. গুরুত্বপূর্ণ: Throttle ≠ Security System

এটা খুব ভালোভাবে মনে রাখবে।

DRF throttling:

```text
API usage control
```

কিন্তু এটা একা:

```text
DDoS protection
WAF
Firewall
Bot protection
```

এর replacement নয়।

Production architecture-এ অনেক সময়:

```text
Internet
   ↓
CDN / WAF / Reverse Proxy
   ↓
Load Balancer
   ↓
Django
   ↓
Redis
   ↓
PostgreSQL
```

ব্যবহার করা হয়।

---

# 17. `wait()` কী?

Custom throttle লিখলে `wait()` method ব্যবহার করে client-কে আনুমানিক কতক্ষণ অপেক্ষা করতে হবে সেটা জানানো যায়।

Example:

```python
from rest_framework.throttling import BaseThrottle


class CustomThrottle(BaseThrottle):

    def allow_request(self, request, view):
        # custom logic
        return True

    def wait(self):
        return 30
```

তবে production-grade custom rate limiter বানানোর সময় concurrency, atomicity এবং distributed behavior carefully consider করতে হবে।

DRF-এর built-in throttles সাধারণ use-case-এর জন্য অনেক বেশি convenient।

---

# 18. Redis TTL

Throttle state সাধারণত নির্দিষ্ট সময়ের জন্য রাখা হয়।

ধরো:

```text
5 requests / minute
```

তাহলে rate-limit state-এর lifecycle-এর সঙ্গে time window সম্পর্কিত।

Conceptually:

```text
Request
   ↓
Redis state
   ↓
Time passes
   ↓
state expires/updates
```

Redis-এর fast in-memory nature এখানে useful।

---

# 19. Cache এবং Throttle একই Redis ব্যবহার করতে পারে

এটা খুব interesting architecture:

```text
                    Redis
                  /       \
                 /         \
             Cache        Throttle
               ↑             ↑
               │             │
          DRF API        DRF Throttle
```

একই Redis instance হলেও key namespace আলাদা রাখা ভালো।

Conceptually:

```text
cache:products:list

cache:product:1

throttle:...

```

তোমার application-এর naming convention অনুযায়ী namespace আরও পরিষ্কার করা যায়।

---

# 20. Redis memory নিয়ে সতর্কতা

Production Redis unlimited না।

তাই:

```text
TTL
Memory policy
Key design
Cache size
Eviction strategy
```

গুরুত্বপূর্ণ।

বিশেষ করে cache এবং throttling একই Redis instance-এ থাকলে capacity planning দরকার।

বড় production system-এ প্রয়োজন অনুযায়ী আলাদা Redis instance/DB/service ব্যবহার করা হতে পারে।

---

# 21. Practical Project Structure

এখন project structure এমন হতে পারে:

```text
drf_redis/
│
├── config/
│   ├── settings.py
│   └── urls.py
│
├── api/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── throttles.py
│   └── urls.py
│
└── manage.py
```

`throttles.py`:

```python
from rest_framework.throttling import (
    AnonRateThrottle,
    UserRateThrottle,
)


class LoginThrottle(AnonRateThrottle):
    scope = "login"


class SearchThrottle(UserRateThrottle):
    scope = "search"


class ProductThrottle(UserRateThrottle):
    scope = "product"
```

---

# 22. Complete Flow

এখন পুরো system:

```text
                        Client
                           │
                           ▼
                        Django
                           │
                    ┌──────┴──────┐
                    │             │
                   GET          POST
                    │             │
                    ▼             ▼
                 Redis         Database
              cache/throttle      │
                    │             │
                    ▼             ▼
                 Response      Invalidate
                                  │
                                  ▼
                                Redis
```

আর throttling:

```text
Request
   ↓
DRF Throttle
   ↓
Django Cache
   ↓
Redis
   ↓
Allowed?
  / \
Yes  No
 |    |
API  429
```

---

# 23. আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়গুলো

### ① Redis নিজে throttle নয়

```text
DRF Throttle
     ↓
Django Cache
     ↓
Redis
```

### ② Scoped throttling

```text
login   → 5/min
search  → 30/min
product → 100/min
```

### ③ Authentication অনুযায়ী rate

```text
Anonymous      → lower limit
Authenticated  → higher limit
```

### ④ Multiple server

```text
Django #1 ─┐
           ├── Redis
Django #2 ─┘
```

Shared Redis distributed throttling-এর জন্য useful।

### ⑤ 429

Limit exceed হলে:

```text
HTTP 429 Too Many Requests
```

---

# Mini Practice

নিজে হাতে এই তিনটা endpoint বানাও:

```text
POST /login/
GET  /search/?q=laptop
GET  /products/
```

এবং rate রাখো:

```text
login    → 5/minute
search   → 20/minute
products → 50/minute
```

তারপর test করো:

```text
1. Redis চালু
2. Django চালু
3. Login endpoint কয়েকবার call
4. Limit cross করো
5. 429 দেখো
6. Search-এর limit আলাদাভাবে test করো
7. Redis restart করলে behavior observe করো
```

**Lesson 5-এ আমরা Redis + Celery + production architecture দেখব**—background task, email/notification processing, worker, Redis broker, এবং Django + Redis + Celery কীভাবে একসাথে কাজ করে।


---
# Lesson 5 — Redis + Celery + Production Setup

এটা আমাদের **Redis course-এর final lesson**। আজকে Redis-কে শুধু cache বা throttle হিসেবে নয়, **background task system-এর অংশ** হিসেবে ব্যবহার করব।

আজকের flow:

```text
Django
  │
  ├── Cache ───────→ Redis
  │
  ├── Throttle ────→ Redis
  │
  └── Celery ──────→ Redis ─────→ Celery Worker
                                      │
                                      ▼
                                  Background Task
```

---

# 1. Celery কী?

ধরো user একটা order করল:

```text
POST /orders/
```

Order create করার পরে তোমাকে:

* email পাঠাতে হবে
* notification পাঠাতে হবে
* invoice generate করতে হবে
* কিছু heavy processing করতে হবে

সবকিছু Django request-এর মধ্যে করলে:

```text
Client
  ↓
Django
  ↓
Create Order
  ↓
Send Email
  ↓
Generate Invoice
  ↓
Notification
  ↓
Response
```

তাহলে response slow হতে পারে।

Celery দিয়ে heavy/background কাজ আলাদা worker-এ পাঠাতে পারি:

```text
Client
  ↓
Django
  ↓
Create Order
  ↓
Task Queue
  ↓
Response দ্রুত ফিরে যায়

              Redis
                ↓
          Celery Worker
                ↓
        Background Task
```

---

# 2. Redis এখানে কী করছে?

Celery-এর architecture-এ Redis **message broker** হিসেবে কাজ করতে পারে।

```text
Django
   │
   │ task পাঠায়
   ▼
 Redis
   │
   │ task নেয়
   ▼
Celery Worker
```

অর্থাৎ Redis এখানে:

> "কোন background task execute করতে হবে" — সেই message রাখার মধ্যবর্তী system হিসেবে কাজ করছে।

---

# 3. Package install

তোমার virtual environment activate করে:

```bash
pip install celery redis
```

আগের lesson-এর:

```bash
pip install django djangorestframework django-redis redis
```

থাকলে শুধু Celery install করলেই হবে।

---

# 4. Project structure

আমাদের project:

```text
drf_redis/
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── celery.py
│   └── urls.py
│
├── api/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── tasks.py
│
└── manage.py
```

---

# 5. Celery configuration

`config/celery.py`

```python
import os

from celery import Celery


os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "config.settings"
)

app = Celery("config")

app.config_from_object(
    "django.conf:settings",
    namespace="CELERY"
)

app.autodiscover_tasks()
```

এখানে:

```python
app.autodiscover_tasks()
```

মানে Django apps-এর মধ্যে `tasks.py` খুঁজে Celery tasks discover করবে।

---

# 6. `config/__init__.py`

এই file-এ:

```python
from .celery import app as celery_app

__all__ = ("celery_app",)
```

এতে Django project-এর সাথে Celery app properly load হতে পারে।

---

# 7. Redis broker configure করি

`settings.py`

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

আমরা আগের lesson-এ cache-এর জন্য ব্যবহার করছিলাম:

```text
redis://127.0.0.1:6379/1
```

এখানে:

```text
/0 → Celery broker
/1 → Django cache
```

এইভাবে আলাদা Redis logical database ব্যবহার করা যায়।

---

# 8. First Celery task

`api/tasks.py`

```python
from celery import shared_task


@shared_task
def add_numbers(a, b):
    return a + b
```

এটা একটা simple background task।

---

# 9. Task কীভাবে call করব?

Django shell:

```bash
python manage.py shell
```

তারপর:

```python
from api.tasks import add_numbers

result = add_numbers.delay(10, 20)
```

এখানে:

```python
.delay()
```

খুব গুরুত্বপূর্ণ।

এটা task-টা সরাসরি execute না করে Celery queue-তে পাঠায়।

---

# 10. Worker চালাতে হবে

অন্য terminal খুলে:

```bash
celery -A config worker --loglevel=info
```

Worker output-এ task discover হয়েছে কিনা দেখতে পারবে।

তারপর Django shell থেকে:

```python
add_numbers.delay(10, 20)
```

Flow:

```text
Django
  ↓
add_numbers.delay()
  ↓
Redis
  ↓
Celery Worker
  ↓
add_numbers(10, 20)
```

---

# 11. Result কীভাবে পাব?

```python
result = add_numbers.delay(10, 20)
```

`result` হচ্ছে একটি task result reference।

যদি result backend configure করো, তাহলে task result retrieve করতে পারবে।

Example:

```python
CELERY_RESULT_BACKEND = "redis://127.0.0.1:6379/2"
```

তাহলে:

```text
Redis DB 0 → Broker
Redis DB 1 → Django Cache
Redis DB 2 → Celery Result Backend
```

তবে সব application-এ task result সংরক্ষণ করা প্রয়োজন হয় না। প্রয়োজন অনুযায়ী result backend ব্যবহার করবে।

---

# 12. Real-world example — Order API

এখন একটা realistic example দেখি।

ধরো:

```text
POST /orders/
```

User order তৈরি করল।

Django:

```text
Create Order
     ↓
Send confirmation email
```

Email sending যদি request-এর মধ্যে করো:

```python
send_email()
```

তাহলে user-কে email sending শেষ হওয়া পর্যন্ত অপেক্ষা করতে হতে পারে।

বরং:

```python
send_order_email.delay(order.id)
```

করতে পারো।

---

# 13. Order task

`api/tasks.py`

```python
from celery import shared_task


@shared_task
def send_order_email(order_id):

    print(
        f"Sending email for order {order_id}"
    )

    return True
```

এখন View:

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .tasks import send_order_email


class OrderCreateView(APIView):

    def post(self, request):

        # এখানে বাস্তবে order create করবে
        order_id = 101

        send_order_email.delay(order_id)

        return Response({
            "message": "Order created",
            "order_id": order_id
        })
```

Flow:

```text
Client
  │
  ▼
POST /orders/
  │
  ▼
Django
  │
  ├── Create Order
  │
  └── Queue Email Task
          │
          ▼
        Redis
          │
          ▼
    Celery Worker
          │
          ▼
     Send Email
```

User-এর request-টা email sending-এর জন্য unnecessarily wait করতে হয় না।

---

# 14. Celery + Redis + Django

এখন পুরো architecture:

```text
                         Client
                           │
                           ▼
                      Django / DRF
                     /      |       \
                    /       |        \
                   ▼        ▼         ▼
                Redis     Redis      Redis
                Cache    Throttle    Broker
                                      │
                                      ▼
                                Celery Worker
                                      │
                            ┌─────────┼─────────┐
                            ▼         ▼         ▼
                          Email    Reports   Notifications
```

একই Redis service-এর different logical databases বা আলাদা Redis deployments ব্যবহার করা যায়—deployment অনুযায়ী।

---

# 15. Redis-এর তিনটা বড় ব্যবহার

এই course-এর সবচেয়ে important summary:

### 1. Cache

```text
Django
  ↓
Redis
```

ব্যবহার:

```text
Product list
Category
Frequently accessed data
```

---

### 2. Throttle

```text
DRF
 ↓
Django Cache
 ↓
Redis
```

ব্যবহার:

```text
5 requests/min
100 requests/min
```

---

### 3. Celery Broker

```text
Django
 ↓
Redis
 ↓
Celery Worker
```

ব্যবহার:

```text
Email
Notification
Report
Background processing
```

---

# 16. Production Architecture

এখন একটা realistic architecture:

```text
                         Internet
                            │
                            ▼
                       CDN / WAF
                            │
                            ▼
                      Load Balancer
                       /          \
                      ▼            ▼
                 Django #1     Django #2
                    │              │
          ┌─────────┼──────────────┤
          │         │              │
          ▼         ▼              ▼
       Redis     PostgreSQL      Redis
       Cache       Database       Broker
          │                        │
          │                        ▼
          │                  Celery Worker
          │                        │
          │              ┌─────────┼─────────┐
          │              ▼         ▼         ▼
          │            Email    Reports   Notifications
          │
          ▼
      Fast API reads
```

বাস্তবে infrastructure অনুযায়ী Redis আলাদা service/cluster-এও রাখা হতে পারে।

---

# 17. Environment variables

Production-এ Redis URL code-এর মধ্যে hardcode না করাই ভালো।

Bad:

```python
CELERY_BROKER_URL = (
    "redis://127.0.0.1:6379/0"
)
```

বরং environment variable:

```python
import os


CELERY_BROKER_URL = os.getenv(
    "CELERY_BROKER_URL"
)
```

Cache:

```python
REDIS_URL = os.getenv("REDIS_URL")
```

তারপর:

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": REDIS_URL,
    }
}
```

Production-এ credentials/configuration source code-এর বাইরে রাখা গুরুত্বপূর্ণ।

---

# 18. Redis password / authentication

Production Redis publicly expose করা উচিত নয়।

Architecture ideally:

```text
Internet
   │
   ▼
Django
   │
   ▼
Private Network
   │
   ▼
Redis
```

Redis-এর network access restricted রাখা উচিত।

যদি managed Redis service ব্যবহার করো, তারা সাধারণত authentication/TLS/network access-এর জন্য configuration দেয়।

---

# 19. Redis connection pooling

Production-এ অনেক Django request একই Redis server-এর সাথে কাজ করতে পারে।

`django-redis` connection pooling support করে।

উদাহরণ:

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": REDIS_URL,
        "OPTIONS": {
            "CLIENT_CLASS":
                "django_redis.client.DefaultClient",
        },
    }
}
```

High-traffic application-এ connection limits এবং Redis capacity monitor করা গুরুত্বপূর্ণ।

---

# 20. Redis failure হলে কী হবে?

এটা production-এর গুরুত্বপূর্ণ প্রশ্ন।

ধরো:

```text
Django
  ↓
Redis ❌
```

তাহলে:

### Cache-এর ক্ষেত্রে

Application design অনুযায়ী cache unavailable হলে database fallback করা যেতে পারে।

```text
Redis unavailable
      ↓
Database
```

### Throttling-এর ক্ষেত্রে

Throttle state-এর জন্য Redis unavailable হলে behavior carefully design/test করতে হবে।

### Celery-এর ক্ষেত্রে

Redis broker unavailable হলে background task queueing কাজ করবে না।

তাই Redis production infrastructure-এর গুরুত্বপূর্ণ dependency হতে পারে।

---

# 21. Monitoring

Production Redis-এর জন্য monitor করবে:

```text
Memory usage
CPU
Connections
Latency
Hit/miss ratio
Evictions
Commands/sec
Errors
```

Celery-এর জন্য:

```text
Worker status
Task failures
Task duration
Queue length
Retry count
```

Django-এর জন্য:

```text
API latency
5xx
429
Database queries
Request rate
```

---

# 22. Cache vs Celery

দুটোকে গুলিয়ে ফেলবে না।

### Redis Cache

প্রশ্ন:

> "এই data আগে থেকে রাখা আছে?"

```text
GET
 ↓
Redis
 ↓
Data
```

### Celery

প্রশ্ন:

> "এই কাজটা background-এ execute করতে হবে?"

```text
Task
 ↓
Redis
 ↓
Worker
 ↓
Execute
```

Redis দুই জায়গাতেই থাকতে পারে, কিন্তু **উদ্দেশ্য আলাদা**।

---

# 23. কখন Celery ব্যবহার করবে?

ভালো use cases:

```text
Send email
Send notification
Generate report
Process uploaded files
Periodic jobs
Long-running calculations
External API processing
```

যে কাজ user response-এর আগে শেষ করা জরুরি নয়, সেটাকে background task করার candidate হিসেবে ভাবতে পারো।

---

# 24. Retry

ধরো email service temporary failure করল।

Celery task retry করতে পারে।

Conceptual example:

```python
from celery import shared_task


@shared_task(
    autoretry_for=(Exception,),
    retry_backoff=True,
    max_retries=3,
)
def send_email_task():

    # email sending logic
    pass
```

এতে temporary failure-এর ক্ষেত্রে retry mechanism ব্যবহার করা যায়।

Production-এ কোন exception retry করবে এবং কতবার করবে সেটা carefully define করা উচিত।

---

# 25. Periodic Tasks

Celery দিয়ে periodic কাজও করা যায়।

যেমন:

```text
প্রতি রাত ১২টায়
    ↓
Old cache/data cleanup
```

অথবা:

```text
প্রতি ১ ঘণ্টায়
    ↓
Generate report
```

এক্ষেত্রে Celery ecosystem-এর scheduler/beat ব্যবহার করা হয়।

Architecture:

```text
Celery Beat
    ↓
Redis
    ↓
Celery Worker
```

---

# 26. Docker Compose Architecture

Development environment-এ একটা simple setup এমন হতে পারে:

```text
docker-compose
│
├── redis
├── postgres
├── django
└── celery
```

Conceptually:

```text
             ┌───────────┐
             │  Django   │
             └─────┬─────┘
                   │
             ┌─────▼─────┐
             │   Redis   │
             └─────┬─────┘
                   │
             ┌─────▼─────┐
             │  Celery   │
             │  Worker   │
             └───────────┘

             PostgreSQL
                 ▲
                 │
               Django
```

---

# 27. একটা গুরুত্বপূর্ণ production distinction

Redis-এর logical database:

```text
/0
/1
/2
```

ব্যবহার করা যায়, কিন্তু production isolation-এর জন্য সবসময় এগুলোকে আলাদা physical Redis service-এর equivalent ভাববে না।

যদি workload অনেক বড় হয়:

```text
Redis Cache Cluster
Redis Celery Broker
```

আলাদা করা হতে পারে।

এতে এক workload অন্য workload-কে বেশি প্রভাবিত করার risk কমে।

---

# 28. আমাদের পুরো ৫ Lesson-এর Journey

এখন পুরো course একসাথে:

```text
Lesson 1
Redis Fundamentals
      ↓
Django ↔ Redis
      ↓

Lesson 2
DRF API Caching
      ↓
Cache HIT / MISS
      ↓

Lesson 3
Cache Invalidation
      ↓
Create / Update / Delete
      ↓

Lesson 4
DRF Throttling
      ↓
Redis-backed rate limiting
      ↓

Lesson 5
Celery + Redis
      ↓
Background Tasks
      ↓
Production Architecture
```

---

# 29. Final Architecture

তোমার future DRF project-এ architecture এমন হতে পারে:

```text
                         Client
                           │
                           ▼
                     CDN / WAF
                           │
                           ▼
                    Load Balancer
                     /         \
                    ▼           ▼
               Django #1    Django #2
                    │           │
        ┌───────────┼───────────┤
        │           │           │
        ▼           ▼           ▼
      Cache      Throttle    PostgreSQL
        │           │
        └─────┬─────┘
              ▼
            Redis
              │
              │
              ▼
        Celery Broker
              │
              ▼
        Celery Workers
          /    |     \
         ▼     ▼      ▼
      Email  Report  Notification
```

এখন Redis তোমার project-এ তিনটি গুরুত্বপূর্ণ role পালন করছে:

```text
┌──────────────────────────────┐
│            REDIS             │
├──────────────────────────────┤
│  1. API Cache                │
│  2. DRF Throttle Storage     │
│  3. Celery Message Broker    │
└──────────────────────────────┘
```

---

## তোমার জন্য Final Practice Project

এখন সবচেয়ে ভালো হবে এই ৫টা lesson একসাথে একটা mini **E-commerce DRF API**-তে implement করা:

```text
Authentication
     ↓
Products
     ↓
Categories
     ↓
Orders
     ↓
Redis Cache
     ↓
Redis Throttling
     ↓
Celery Email
     ↓
Production-style Docker setup
```

Minimum Redis implementation:

```text
GET /products/
    → Redis Cache

POST /products/
    → DB + Cache Invalidation

GET /products/1/
    → Object Cache

POST /login/
    → Scoped Throttle

GET /search/
    → Scoped Throttle + Cache

POST /orders/
    → DB + Celery Email Task
```

এই projectটা নিজে implement করতে পারলে **DRF + Redis-এর practical foundation অনেক শক্ত হবে**।


----
হ্যাঁ, অবশ্যই। 👍 **এই ৫টা lesson-এর Redis concepts তুমি প্রায় যেকোনো Django/DRF project-এ apply করতে পারবে।** তবে সব project-এ Redis-এর সব feature লাগবে না।

### কোন project-এ কীভাবে ব্যবহার করবে?

| Project type       | Redis-এর useful অংশ       |
| ------------------ | ------------------------- |
| E-commerce         | Cache + Throttle + Celery |
| Blog API           | Cache + Throttle          |
| Social Media API   | Cache + Throttle + Celery |
| LMS / Course API   | Cache + Throttle + Celery |
| Booking API        | Cache + Throttle + Celery |
| News API           | Cache + Throttle          |
| Chat/Notification  | Redis + Celery            |
| Admin/Business API | Cache + Celery            |

### সহজ rule মনে রাখো

**1. Data বারবার read হচ্ছে?**

```text
Database → Redis Cache
```

যেমন:

```text
/products/
/categories/
/popular-products/
```

**2. API request limit করতে হবে?**

```text
DRF Throttle → Redis
```

যেমন:

```text
/login/
/search/
/api/
```

**3. কোনো কাজ background-এ করতে হবে?**

```text
Django → Redis → Celery Worker
```

যেমন:

```text
Email
Notification
Report generation
File processing
```

### কিন্তু একটা জিনিস গুরুত্বপূর্ণ

প্রতিটা project-এ Redis **অবশ্যই লাগবে**—এমন না।

ছোট CRUD API:

```text
Django + DRF + PostgreSQL
```

দিয়েই যথেষ্ট হতে পারে।

Project বড় হলে বা performance/background processing-এর প্রয়োজন হলে:

```text
Django/DRF
   +
PostgreSQL
   +
Redis
   +
Celery
```

খুব useful architecture হতে পারে।

**তুমি এখন Redis-এর basic থেকে production concepts পর্যন্ত শিখে ফেলেছ।** পরের সবচেয়ে ভালো step হবে একটা **real DRF project-এ zero থেকে Redis + Celery integrate করা**, যাতে এই ৫টা lesson practically একসাথে apply করতে পারো।


---
