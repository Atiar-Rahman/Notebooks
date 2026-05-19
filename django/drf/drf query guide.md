# Complete Django & DRF Query Guide (Apply to Any Project)

This guide is a **practical, end‑to‑end reference** you can apply to **any Django / DRF project**—from CRUD apps to large production APIs. Use it as a checklist while building features.

---

## 1) Core Concepts (Must Know)

### What is a QuerySet (WHEN & WHY)

**When:** Every time you read data from DB
**Why:** QuerySet lets you build queries step‑by‑step before hitting DB

```python
qs = User.objects.filter(is_active=True)
```

### Lazy Evaluation (HOW it helps)

**How:** Query is NOT executed immediately
**Why:** You can chain filters without performance cost

**DB hit happens when:**

* loop
* list(qs)
* len(qs)
* bool(qs)

---

## 2) CRUD Queries (Daily Use)

### Create

```python
User.objects.create(username='john')
```

### Read

```python
User.objects.all()
User.objects.get(id=1)
User.objects.filter(is_active=True)
```

### Update

```python
User.objects.filter(id=1).update(is_active=False)
user.is_active = False
user.save()
```

### Delete

```python
User.objects.filter(id=1).delete()
```

---

## 3) Filtering (Most Used)

### WHEN to use filtering

* Search page
* Dashboard list
* Admin panel
* Any GET API

### HOW filtering works

Django converts lookup into SQL WHERE clause

```python
price__gte=100        # price >= 100
name__icontains='ph'  # LIKE %ph%
created_at__date=today
```

### WHERE to apply filtering

✅ View / ViewSet (`get_queryset`)
❌ Serializer

### exclude()

```python
User.objects.exclude(is_staff=True)
```

### Q Objects (Complex Logic)

**WHEN:** OR / NOT needed

```python
from django.db.models import Q
User.objects.filter(Q(role='admin') | Q(role='manager'))
```

---

## 4) Sorting & Limiting

```python
User.objects.order_by('-created_at')
User.objects.all()[:10]
```

---

## 5) Selecting Fields (Optimization)

### values / values_list

```python
User.objects.values('id','username')
User.objects.values_list('id','username', flat=False)
```

### only / defer

```python
User.objects.only('username')
User.objects.defer('password')
```

---

## 6) Relationships (CRITICAL)

### WHY relationships cause performance issues

Nested serializers trigger extra queries (N+1 problem)

---

### select_related

**WHEN:** ForeignKey / OneToOne
**HOW:** SQL JOIN
**WHERE:** queryset / get_queryset

```python
Order.objects.select_related('user')
```

---

### prefetch_related

**WHEN:** ManyToMany / reverse FK
**HOW:** Separate query + Python join

```python
Order.objects.prefetch_related('items')
```

---

### N+1 Fix Pattern (REAL USE)

```python
Post.objects.select_related('author').prefetch_related('comments')
```

---

## 7) Aggregation & Annotation

### aggregate()

**WHEN:** Dashboard stats, reports
**RESULT:** Single dictionary

```python
Product.objects.aggregate(avg_price=Avg('price'))
```

---

### annotate()

**WHEN:** Per‑row computed field
**RESULT:** Adds virtual field to each row

```python
Product.objects.annotate(review_count=Count('reviews'))
```

---

## 8) Advanced Expressions

### F Expressions

```python
from django.db.models import F
Product.objects.update(stock=F('stock')-1)
```

### Case / When

```python
from django.db.models import Case, When, Value, IntegerField
User.objects.annotate(
    role=Case(
        When(is_superuser=True, then=Value(1)),
        default=Value(0),
        output_field=IntegerField()
    )
)
```

---

## 9) Performance Tools

### count vs len

```python
qs.count()   # DB level
len(qs)      # loads all rows
```

### exists

```python
User.objects.filter(email=email).exists()
```

### bulk operations

```python
User.objects.bulk_create(users)
```

---

## 10) DRF Query Integration

### WHERE queries belong in DRF

✅ View / ViewSet
❌ Serializer

---

### Base ViewSet Pattern

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

### Dynamic Queryset (MOST IMPORTANT)

**WHEN:** User‑specific data, filtering, permission

```python
def get_queryset(self):
    qs = Product.objects.all()
    if not self.request.user.is_staff:
        qs = qs.filter(is_public=True)
    return qs
```

---

## 11) DRF Filtering / Search / Ordering

```python
from django_filters.rest_framework import DjangoFilterBackend
from rest_framework.filters import SearchFilter, OrderingFilter

filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
filterset_fields = ['status','price']
search_fields = ['name','description']
ordering_fields = ['price','created_at']
```

---

## 12) Pagination (Always Use)

```python
from rest_framework.pagination import PageNumberPagination

class DefaultPagination(PageNumberPagination):
    page_size = 10
```

---

## 13) Security‑Aware Querying

### User‑Scoped Data

```python
def get_queryset(self):
    return Order.objects.filter(user=self.request.user)
```

---

## 14) Common Project Patterns

### Soft Delete

**WHEN:** Data should not be permanently removed

```python
objects.filter(is_deleted=False)
```

---

### Date Range Filter

**WHEN:** Reports, history page

```python
created_at__range=[start, end]
```

---

### Role‑Based Query

**WHEN:** Admin vs User data access

```python
if user.is_staff:
    qs = Order.objects.all()
else:
    qs = Order.objects.filter(user=user)
```

---

## 15) When to Use Raw SQL

* Complex reporting
* DB‑specific feature
* Extreme performance need

```python
Model.objects.raw("SELECT * FROM table")
```

---

## 16) Debug & Optimize

* Django Debug Toolbar
* print(connection.queries)
* add DB indexes

---

## 17) Golden Rules (Interview + Production)

1. Filter early
2. Paginate always
3. select_related / prefetch_related
4. Avoid SerializerMethodField queries
5. count() > len()

---

## 18) Universal Checklist (Any Project)

* [ ] Pagination enabled
* [ ] Query optimized
* [ ] User‑scoped data
* [ ] Index on heavy filters
* [ ] No N+1 issue

---

**You can apply this guide to:**

* E‑commerce
* LMS
* Scholarship system
* Blog / Social app
* Admin dashboards

---

If you want next:

* Convert this into **PDF / cheat‑sheet**
* **Project‑specific query design** (e‑commerce / scholarship)
* **Interview mock test**
