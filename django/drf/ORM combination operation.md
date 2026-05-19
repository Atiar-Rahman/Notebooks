
# 🔥 Main combination operations in Django ORM

## 1. ✅ `get_or_create()`

```python
obj, created = Model.objects.get_or_create(field=value)
```

👉 কাজ:

- আগে **get (SELECT)** করে
    
- না পেলে **create (INSERT)** করে
    

✔️ Use case:

- “না থাকলে বানাও”
    

---

## 2. ✅ `update_or_create()` ⭐ (most powerful)

```python
obj, created = Model.objects.update_or_create(
    field=value,
    defaults={'name': 'new'}
)
```

👉 কাজ:

- আগে **get (SELECT)**
    
- থাকলে **update (UPDATE)**
    
- না থাকলে **create (INSERT)**
    

✔️ Use case:

- “থাকলে update, না থাকলে create”
    

---

## 3. ✅ `bulk_create()`

```python
Model.objects.bulk_create([...])
```

👉 কাজ:

- একসাথে অনেকগুলো **create (INSERT)**
    

✔️ Use case:

- performance optimization
    

❗ এটা combination না technically, কিন্তু batch operation

---

## 4. ✅ `bulk_update()`

```python
Model.objects.bulk_update(objs, ['field'])
```

👉 কাজ:

- একসাথে অনেকগুলো **update**
    

---

## 5. ⚠️ `update()`

```python
Model.objects.filter(...).update(field=value)
```

👉 কাজ:

- direct **UPDATE query** (no get, no save())
    

✔️ efficient  
❗ signals trigger হয় না

---

## 6. ⚠️ `create()`

```python
Model.objects.create(...)
```

👉 শুধু create (INSERT)  
👉 combination না, but often used with others

---

# 🧠 Important conclusion

👉 Django-তে **true combination helper মাত্র ২টা:**

### 🔑 Core combination methods:

1. ✅ `get_or_create()`
    
2. ✅ `update_or_create()`
    

---

# 🔥 তোমার use case অনুযায়ী

For **RecentlyViewed**:

|Situation|Best Method|
|---|---|
|First time view|`create()`|
|Avoid duplicate|`get_or_create()`|
|Always refresh/update|⭐ `update_or_create()`|

---

# ⚡ Pro tip (interview level)

👉 Difference:

- `get_or_create()` → **safe insert**
    
- `update_or_create()` → **upsert (update + insert)**
    

---

# 🧾 Final answer (short)

👉 Django ORM-এ **combination operation আসলে ২টা:**

- `get_or_create()`
    
- `update_or_create()`
    

---

# 🔍 `get_object_or_404()` কী?

```python id="b8n3u9"
from django.shortcuts import get_object_or_404

obj = get_object_or_404(Model, id=1)
```

---

# ✅ এটা কী ধরনের operation?

👉 এটা শুধু:

> 🔎 **SELECT (get)** + ❌ **Exception handling**

---

# 🧠 ভিতরে কী হয়?

Internally এটা basically এই কাজটাই করে:

```python id="l8n9z2"
try:
    obj = Model.objects.get(id=1)
except Model.DoesNotExist:
    raise Http404
```

---

# ⚙️ So operation breakdown

| Step | Operation           |
| ---- | ------------------- |
| 1    | SELECT (get)        |
| 2    | না পেলে → raise 404 |

---

# ❗ Important: এটা combination না

👉 এটা:

* ❌ create করে না
* ❌ update করে না
* ❌ multiple DB operation না

👉 শুধু:
✔️ **get + error handling shortcut**

---

# 🔥 Difference from others

| Method                | Operation Type         |
| --------------------- | ---------------------- |
| `get()`               | শুধু SELECT            |
| `get_object_or_404()` | SELECT + 404 error     |
| `get_or_create()`     | SELECT + INSERT        |
| `update_or_create()`  | SELECT + UPDATE/INSERT |

---

# 🧠 কখন ব্যবহার করবা?

### ✔️ Django views / APIs-তে

```python id="zv2pzt"
product = get_object_or_404(Product, slug=slug)
```

👉 যদি না থাকে:
➡️ automatically 404 response

---

# ⚠️ Common mistake

❌ এটা দিয়ে duplicate handle করা যায় না

```python id="4p8o1y"
get_object_or_404(Model, field=value)
```

👉 যদি multiple object থাকে:
💣 `MultipleObjectsReturned` error হবে

---

# ✅ Safe version (if multiple possible)

```python id="pbb9mn"
obj = Model.objects.filter(field=value).first()
```

---

# 🧾 Final summary

👉 `get_object_or_404()` হলো:

> ✔️ SELECT operation
> ✔️ + built-in 404 error handling

👉 এটা **combination operation না**,
বরং একটা **shortcut helper function**

---

# 🔥 1. `get()` → একটাই object

```python
obj = Model.objects.get(id=1)
```

👉 কাজ:

* **exactly 1 object** return করবে
* না পেলে → `DoesNotExist` ❌
* বেশি পেলে → `MultipleObjectsReturned` ❌

✔️ Use when: তুমি নিশ্চিত ১টাই object আছে

---

# 🔥 2. `filter()` → multiple object

```python
qs = Model.objects.filter(name='abc')
```

👉 কাজ:

* 0, 1 বা multiple object return করতে পারে
* কখনো error দেয় না

✔️ Use when: multiple result expected

---

# 🔥 3. `first()` → প্রথম object

```python
obj = Model.objects.filter(name='abc').first()
```

👉 কাজ:

* প্রথম object return করে
* না পেলে → `None`

✔️ Safe alternative to `get()`

---

# 🔥 4. `last()` → শেষ object

```python
obj = Model.objects.filter(name='abc').last()
```

---

# 🔥 5. `get_object_or_404()` ⭐

```python
from django.shortcuts import get_object_or_404

obj = get_object_or_404(Model, id=1)
```

👉 কাজ:

* object পেলে return
* না পেলে → **404 error**

✔️ Django views / DRF-এ খুব ব্যবহার হয়

---

# 🔥 6. `get_or_create()`

```python
obj, created = Model.objects.get_or_create(name='abc')
```

👉 কাজ:

* আগে খোঁজে
* না পেলে create করে

---

# 🔥 7. `update_or_create()`

```python
obj, created = Model.objects.update_or_create(
    name='abc',
    defaults={'age': 20}
)
```

👉 কাজ:

* থাকলে update
* না থাকলে create

---

# 🔥 8. `all()` → সব object

```python
qs = Model.objects.all()
```

---

# 🔥 9. `values()` / `values_list()`

```python
qs = Model.objects.values('name', 'id')
```

👉 object না, dictionary/tuple return করে

---

# 🔥 10. `only()` / `defer()`

```python
qs = Model.objects.only('name')
```

👉 partial data load করে (performance optimization)

---

# 🔥 11. DRF specific → `get_object()` (ViewSet)

```python
def get_object(self):
    return super().get_object()
```

👉 internally:

* queryset থেকে object নেয়
* permission check করে
* lookup_field ব্যবহার করে (e.g. `slug`, `id`)

---

# 🔥 12. `select_related()` / `prefetch_related()`

```python
qs = Model.objects.select_related('category')
```

👉 related object efficiently fetch করে

---

# 🧠 Quick comparison

| Method                | Return      | Error? | Use               |
| --------------------- | ----------- | ------ | ----------------- |
| `get()`               | single      | ❌ yes  | strict            |
| `filter()`            | queryset    | ❌ no   | flexible          |
| `first()`             | single/None | ❌ no   | safe              |
| `get_object_or_404()` | single      | ✅ 404  | API/View          |
| `get_or_create()`     | single      | ❌ no   | create if missing |
| `update_or_create()`  | single      | ❌ no   | upsert            |

---

# 🔑 Best practice (important)

👉 Avoid:

```python
Model.objects.get(...)
```

👉 Prefer:

```python
Model.objects.filter(...).first()
```

👉 API-তে:

```python
get_object_or_404()
```

---

# 🚀 তোমার case (RecentlyViewed)

✔️ Best:

```python
RecentlyViewed.objects.update_or_create(
    user=request.user,
    product=product
)
```

---

# 🧾 Final summary

👉 Django-তে object পাওয়ার main way:

* `get()` (strict)
* `filter()` (flexible)
* `first()` (safe)
* `get_object_or_404()` (API friendly)
* `get_or_create()` (create if not found)
* `update_or_create()` (update or create)

---

# 🔥 Basic rule

👉 `get()` এর ভিতরে তুমি দাও:

> **filter conditions (lookup fields)**

```python id="a1b2c3"
obj = Model.objects.get(field1=value1, field2=value2)
```

---

# 🧠 কতগুলো field ব্যবহার করা যায়?

👉 **Unlimited (as many as needed)**

Django এর কোনো fixed limit নেই।

---

# 🔍 Example 1: 1 field

```python id="x1"
obj = Product.objects.get(id=1)
```

---

# 🔍 Example 2: multiple fields

```python id="x2"
obj = Product.objects.get(id=1, is_active=True)
```

---

# 🔍 Example 3: complex filters

```python id="x3"
obj = Product.objects.get(
    id=1,
    is_active=True,
    category__slug='electronics',
    user__is_staff=True
)
```

👉 এখানে 4টা field ব্যবহার করা হয়েছে

---

# ⚠️ Important rules

## 1. Must return ONLY ONE object

```python id="e1"
Product.objects.get(name="phone")
```

👉 যদি multiple match করে:
💣 `MultipleObjectsReturned`

---

## 2. If no object:

💣 `DoesNotExist`

---

## 3. Field types can be:

### ✔️ direct fields

```python id="f1"
id, name, price
```

### ✔️ related fields (double underscore)

```python id="f2"
category__name
user__email
```

### ✔️ lookups

```python id="f3"
price__gt=100
name__icontains='phone'
created_at__year=2026
```

---

# 🧠 So final answer

👉 তুমি ব্যবহার করতে পারো:

> 🔥 **as many fields as needed (no limit)**

BUT:

* result must be **exactly 1 object**
* otherwise error

---

# 💡 Best practice (important)

❌ risky:

```python id="b1"
get(name="phone")
```

✔️ safer:

```python id="b2"
filter(name="phone").first()
```

---

# 🧾 Summary

| Question              | Answer           |
| --------------------- | ---------------- |
| কত field use করা যায়? | Unlimited        |
| limit আছে?            | No               |
| condition কি হয়?      | AND logic        |
| result কতটা?          | Exactly 1 object |

---

#  ৬টা method একদম practical example + simple explanation দিয়ে বুঝি 👇

ধরি তোমার model:

```python id="m1"
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
    is_active = models.BooleanField(default=True)
```

---

# 🔥 1. `get()` (STRICT)

```python id="g1"
product = Product.objects.get(id=1)
```

### 🧠 কী করে?

* ঠিক ১টা object খুঁজে আনে
* না পেলে ❌ error
* বেশি পেলে ❌ error

### ⚠️ সমস্যা:

```python id="g2"
Product.objects.get(name="phone")
```

👉 যদি 2টা phone থাকে → 💣 crash

---

# 🔥 2. `filter()` (FLEXIBLE)

```python id="f1"
products = Product.objects.filter(is_active=True)
```

### 🧠 কী করে?

* অনেকগুলো object return করে (QuerySet)
* কখনো error দেয় না

### output:

```python id="f2"
<QuerySet [Product1, Product2, Product3]>
```

---

# 🔥 3. `first()` (SAFE)

```python id="fi1"
product = Product.objects.filter(is_active=True).first()
```

### 🧠 কী করে?

* প্রথম object দেয়
* না থাকলে → `None`

### use case:

👉 “একটা দরকার, কিন্তু নিশ্চিত না আছে কিনা”

---

# 🔥 4. `get_object_or_404()` (API FRIENDLY)

```python id="o1"
from django.shortcuts import get_object_or_404

product = get_object_or_404(Product, id=1)
```

### 🧠 কী করে?

* object পেলে return
* না পেলে → **404 page / API response**

### DRF example:

👉 user ভুল id দিলেও crash না হয়ে 404 যাবে

---

# 🔥 5. `get_or_create()` (SAFE CREATE)

```python id="c1"
product, created = Product.objects.get_or_create(
    name="iPhone",
    defaults={"price": 1000}
)
```

### 🧠 কী করে?

👉 যদি থাকে:

* শুধু object return করবে

👉 যদি না থাকে:

* নতুন create করবে

### output:

```python id="c2"
(product_object, True/False)
```

---

# 🔥 6. `update_or_create()` (UPSERT ⭐)

```python id="u1"
product, created = Product.objects.update_or_create(
    name="iPhone",
    defaults={"price": 1200}
)
```

### 🧠 কী করে?

👉 যদি থাকে:

* price update করবে

👉 যদি না থাকে:

* নতুন create করবে

---

### 🔥 real example:

#### আগে ছিল:

```python id="u2"
iPhone, price=1000
```

#### code চালালে:

```python id="u3"
price=1200
```

👉 result:

* existing → update

---

# 🧾 FINAL COMPARISON

| Method                | কাজ              | Error? | Return         |
| --------------------- | ---------------- | ------ | -------------- |
| `get()`               | exact 1 object   | ❌ yes  | object         |
| `filter()`            | multiple objects | ❌ no   | queryset       |
| `first()`             | first object     | ❌ no   | object/None    |
| `get_object_or_404()` | safe get + 404   | ❌ no   | object         |
| `get_or_create()`     | get or insert    | ❌ no   | (obj, created) |
| `update_or_create()`  | update or insert | ❌ no   | (obj, created) |

---

# 🚀 সহজ মনে রাখার trick

* `get()` → strict boss 😤
* `filter()` → flexible friend 🙂
* `first()` → safe picker 👍
* `404()` → web-safe guard 🛡️
* `get_or_create()` → “না থাকলে বানাও” 🏗️
* `update_or_create()` → “থাকলে আপডেট করো” 🔄

---

