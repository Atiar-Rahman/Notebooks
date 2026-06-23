Redis caching DRF-এর performance বাড়ানোর সবচেয়ে কার্যকর উপায়গুলোর একটি। নিচে beginner → advanced ধাপে দেখাচ্ছি।

# Redis কী?

Redis হলো একটি in-memory key-value database।

সাধারণ flow:

```text
Client
  ↓
DRF API
  ↓
PostgreSQL
```

Redis cache ব্যবহার করলে:

```text
Client
  ↓
DRF API
  ↓
Redis Cache (Fast)
  ↓
PostgreSQL (Slow)
```

যদি data cache-এ থাকে, database query লাগবে না।

---

# Step 1: Redis Install

### Docker (recommended)

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis
```

Check:

```bash
docker ps
```

---

### Ubuntu

```bash
sudo apt update
sudo apt install redis-server
```

Check:

```bash
redis-cli ping
```

Output:

```text
PONG
```

---

# Step 2: Required Packages

```bash
pip install redis django-redis
```

---

# Step 3: Django Configuration

`settings.py`

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS":
                "django_redis.client.DefaultClient",
        }
    }
}
```

---

# Step 4: Test Redis

Django shell:

```bash
python manage.py shell
```

```python
from django.core.cache import cache

cache.set("name", "rakib", timeout=60)

cache.get("name")
```

Output:

```python
"rakib"
```

---

# Step 5: Basic API Cache

Without cache:

```python
class UserViewSet(ModelViewSet):

    def list(self, request):
        users = User.objects.all()

        serializer = UserSerializer(
            users,
            many=True
        )

        return Response(serializer.data)
```

Every request hits DB.

---

With cache:

```python
from django.core.cache import cache

class UserViewSet(ModelViewSet):

    def list(self, request):

        data = cache.get("users")

        if data:
            return Response(data)

        users = User.objects.all()

        serializer = UserSerializer(
            users,
            many=True
        )

        data = serializer.data

        cache.set(
            "users",
            data,
            timeout=300
        )

        return Response(data)
```

---

# Step 6: Cache Timeout

```python
cache.set(
    "users",
    data,
    timeout=300
)
```

Meaning:

```text
300 sec = 5 min
```

Common values:

```text
60      = 1 min
300     = 5 min
3600    = 1 hour
86400   = 1 day
```

---

# Step 7: Delete Cache

When user changes data:

```python
cache.delete("users")
```

Example:

```python
def create(self, request):

    serializer = UserSerializer(
        data=request.data
    )

    serializer.is_valid(
        raise_exception=True
    )

    serializer.save()

    cache.delete("users")

    return Response(serializer.data)
```

---

# Step 8: Cache Per User

Bad:

```python
cache_key = "profile"
```

Every user gets same data.

Good:

```python
cache_key = (
    f"profile_{request.user.id}"
)
```

Example:

```python
profile = cache.get(cache_key)
```

---

# Step 9: Cache Query Result

```python
cache_key = "active_users"
```

```python
users = cache.get(cache_key)

if users is None:

    users = list(
        User.objects.filter(
            is_active=True
        ).values(
            "id",
            "name"
        )
    )

    cache.set(
        cache_key,
        users,
        300
    )
```

---

# Step 10: Cache Expensive Statistics

Example:

```python
total_users = User.objects.count()
```

```python
stats = cache.get("dashboard_stats")

if stats is None:

    stats = {
        "users":
            User.objects.count(),

        "orders":
            Order.objects.count(),

        "sales":
            Order.objects.aggregate(...)
    }

    cache.set(
        "dashboard_stats",
        stats,
        600
    )
```

Perfect use case.

---

# Step 11: View Cache Decorator

Function View:

```python
from django.views.decorators.cache import cache_page

@cache_page(60 * 5)
@api_view(["GET"])
def users(request):
    ...
```

---

Class Based View:

```python
from django.utils.decorators import method_decorator
from django.views.decorators.cache import cache_page

@method_decorator(
    cache_page(60 * 5),
    name="list"
)
class UserViewSet(ModelViewSet):
    ...
```

---

# Step 12: Low-Level Cache API

### Get

```python
cache.get(key)
```

### Set

```python
cache.set(key, value)
```

### Delete

```python
cache.delete(key)
```

### Exists

```python
cache.has_key(key)
```

### Clear All

```python
cache.clear()
```

⚠️ Production-এ `cache.clear()` সাবধানে ব্যবহার করুন।

---

# Step 13: Cache Versioning

```python
cache.set(
    "users_v1",
    data
)
```

New release:

```python
cache.set(
    "users_v2",
    data
)
```

পুরনো cache invalidation নিয়ে চিন্তা কমে।

---

# Step 14: Redis Direct Access

```python
from django_redis import get_redis_connection

redis_conn = get_redis_connection(
    "default"
)
```

Set:

```python
redis_conn.set(
    "hello",
    "world"
)
```

Get:

```python
redis_conn.get(
    "hello"
)
```

---

# Step 15: Cache Stampede Protection

সমস্যা:

```text
1000 request
cache miss
1000 DB queries
```

Solution:

```python
cache.add(
    "lock_users",
    "1",
    timeout=10
)
```

অথবা distributed lock:

```python
with redis_conn.lock(
    "users_lock"
):
    ...
```

Advanced systems-এ খুব গুরুত্বপূর্ণ।

---

# Step 16: What Should Be Cached?

✅ User profile

✅ Product list

✅ Dashboard stats

✅ Category list

✅ Settings

✅ Public APIs

✅ External API responses

---

# Don't Cache

❌ Password

❌ OTP

❌ Highly dynamic financial data (unless carefully managed)

❌ Per-request temporary sensitive data

---

# Production Setup

সাধারণ production stack:

```text
Nginx
   ↓
Gunicorn/Uvicorn
   ↓
Django DRF
   ↓
Redis Cache
   ↓
PostgreSQL
```

এবং DRF optimization-এর জন্য একসাথে ব্যবহার করুন:

- Redis Cache
    
- `select_related()`
    
- `prefetch_related()`
    
- Database indexes
    
- Pagination
    
- Celery + Redis (background jobs)
    

এগুলো মিলিয়ে অনেক ক্ষেত্রে API response 500–1000ms থেকে 20–100ms এর মধ্যে নামিয়ে আনা যায়, workload-এর উপর নির্ভর করে।