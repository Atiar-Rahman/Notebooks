চমৎকার। DRF-এর জন্য Redis শেখার সবচেয়ে কার্যকর উপায় হলো **project-based roadmap**। একবারে সব শেখার চেষ্টা না করে ধাপে ধাপে এগোন।

# Phase 1: Redis Basics (Day 1)

## Goal

Redis কী এবং কীভাবে data store করে বুঝা।

### Redis install

Docker:

```bash
docker run -d --name redis -p 6379:6379 redis
```

Check:

```bash
docker exec -it redis redis-cli
```

Test:

```bash
PING
```

Output:

```text
PONG
```

---

## Redis Commands

Set value:

```bash
SET name rakib
```

Get value:

```bash
GET name
```

Delete:

```bash
DEL name
```

Expiration:

```bash
SET otp 1234 EX 60
```

Meaning:

```text
60 seconds later auto delete
```

---

# Phase 2: Django + Redis Integration (Day 2)

Install:

```bash
pip install redis django-redis
```

settings.py

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS":
                "django_redis.client.DefaultClient",
        },
    }
}
```

---

Test:

```bash
python manage.py shell
```

```python
from django.core.cache import cache

cache.set("name", "Rakib", 60)

cache.get("name")
```

Output:

```python
'Rakib'
```

---

# Phase 3: First DRF Cache (Day 3)

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

Every request:

```text
API
 ↓
DB
```

---

Add cache:

```python
from django.core.cache import cache

class UserViewSet(ModelViewSet):

    def list(self, request):

        cache_key = "users"

        data = cache.get(cache_key)

        if data:
            return Response(data)

        users = User.objects.all()

        serializer = UserSerializer(
            users,
            many=True
        )

        data = serializer.data

        cache.set(
            cache_key,
            data,
            timeout=300
        )

        return Response(data)
```

Now:

```text
Request #1 → DB
Request #2 → Redis
Request #3 → Redis
```

---

# Phase 4: Cache Invalidation (Day 4)

Biggest beginner mistake:

```python
cache.set("users", data)
```

But after creating new user:

```python
POST /users/
```

Cache still old.

---

Fix:

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

Same for:

```python
update()
destroy()
```

---

# Phase 5: Dynamic Cache Keys (Day 5)

Wrong:

```python
cache_key = "profile"
```

Every user gets same profile.

---

Correct:

```python
cache_key = (
    f"profile_{request.user.id}"
)
```

Example:

```python
profile_1
profile_2
profile_3
```

---

# Phase 6: Queryset Cache (Day 6)

Cache query result:

```python
users = cache.get("active_users")

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
        "active_users",
        users,
        300
    )
```

---

# Phase 7: Dashboard Cache (Day 7)

Expensive stats:

```python
User.objects.count()

Order.objects.count()

Order.objects.aggregate(...)
```

Cache them:

```python
stats = cache.get(
    "dashboard_stats"
)

if stats is None:

    stats = {
        "users":
            User.objects.count(),

        "orders":
            Order.objects.count(),
    }

    cache.set(
        "dashboard_stats",
        stats,
        600
    )
```

---

# Phase 8: Decorator Cache (Week 2)

Function View:

```python
from django.views.decorators.cache import cache_page

@cache_page(60 * 5)
@api_view(["GET"])
def users(request):
    ...
```

---

Class View:

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

# Phase 9: Redis Monitoring

Redis CLI:

```bash
redis-cli
```

Keys:

```bash
KEYS *
```

Count:

```bash
DBSIZE
```

Memory:

```bash
INFO memory
```

TTL:

```bash
TTL users
```

---

# Phase 10: Redis + Celery (Very Important)

Install:

```bash
pip install celery
```

celery.py

```python
CELERY_BROKER_URL = (
    "redis://127.0.0.1:6379/0"
)
```

Use for:

- Email sending
    
- PDF generation
    
- Notifications
    
- Image processing
    

Flow:

```text
User Request
 ↓
DRF
 ↓
Celery
 ↓
Redis Queue
 ↓
Worker
```

---

# Phase 11: Advanced Redis

শিখবেন:

### Lock

```python
from django_redis import get_redis_connection

redis_conn = get_redis_connection(
    "default"
)

with redis_conn.lock(
    "users_lock"
):
    ...
```

### Prevent Cache Stampede

```text
1000 users
cache miss
1000 DB queries
```

Lock দিয়ে একবার query হবে।

---

# Real Production Order

DRF developer হিসেবে এই order follow করুন:

1. Redis install
    
2. Django cache config
    
3. cache.get()
    
4. cache.set()
    
5. cache.delete()
    
6. Cache key design
    
7. Cache invalidation
    
8. Queryset cache
    
9. Dashboard cache
    
10. Redis monitoring
    
11. Celery + Redis
    
12. Redis locks
    

এই ১২টা step শেষ করলে Redis caching-এর মাধ্যমে DRF API optimization-এর প্রায় ৮০–৯০% practical use case আপনি handle করতে পারবেন।