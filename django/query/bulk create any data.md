অবশ্যই। `Book` model-এ ২০টা sample data ঢোকানোর জন্য Django shell-এ এই code-টা চালাতে পারো।

```python

from books.models import Book
from datetime import date

books = [
    Book(title="Django Basics", author="Rahim", price=500, published_date=date(2024, 1, 10), is_available=True),
    Book(title="Python Fundamentals", author="Karim", price=650, published_date=date(2023, 5, 15), is_available=True),
    Book(title="Learning Django", author="Hasan", price=750, published_date=date(2024, 2, 20), is_available=True),
    Book(title="Advanced Python", author="Sakib", price=900, published_date=date(2022, 8, 12), is_available=False),
    Book(title="Web Development", author="Nayeem", price=550, published_date=date(2023, 3, 5), is_available=True),
    Book(title="Django REST Framework", author="Fahim", price=850, published_date=date(2024, 6, 18), is_available=True),
    Book(title="Python OOP", author="Tanvir", price=600, published_date=date(2022, 11, 25), is_available=False),
    Book(title="Database Design", author="Rafi", price=700, published_date=date(2023, 7, 8), is_available=True),
    Book(title="SQL for Beginners", author="Imran", price=450, published_date=date(2022, 4, 14), is_available=True),
    Book(title="Clean Code", author="Robert Martin", price=1000, published_date=date(2008, 8, 1), is_available=True),
    Book(title="JavaScript Basics", author="John Smith", price=550, published_date=date(2021, 9, 10), is_available=False),
    Book(title="React for Beginners", author="David Lee", price=800, published_date=date(2023, 10, 2), is_available=True),
    Book(title="API Development", author="Arif", price=720, published_date=date(2024, 3, 22), is_available=True),
    Book(title="Django Projects", author="Mahmud", price=950, published_date=date(2024, 7, 11), is_available=False),
    Book(title="Python Data Structures", author="Shuvo", price=680, published_date=date(2022, 6, 30), is_available=True),
    Book(title="Git and GitHub", author="Anik", price=400, published_date=date(2023, 1, 17), is_available=True),
    Book(title="Linux Basics", author="Jahid", price=500, published_date=date(2021, 12, 5), is_available=False),
    Book(title="Backend Development", author="Mehedi", price=880, published_date=date(2024, 5, 9), is_available=True),
    Book(title="Software Engineering", author="Martin Fowler", price=1100, published_date=date(2018, 3, 20), is_available=True),
    Book(title="Testing with Python", author="Nasir", price=620, published_date=date(2023, 11, 13), is_available=True),
]

Book.objects.bulk_create(books)
```


 ### Check করো

```
Book.objects.all()
```

 কতগুলো data আছে:

```
Book.objects.count()
```

 Expected:

```
20
```

 **ORM practice করার জন্য এখন এই ২০টা data দিয়েই query করা শুরু করতে পারো।** যেমন `price > 700`, `author` দিয়ে search, available books, cheapest/expensive book, date filtering ইত্যাদি।


----
# অবশ্যই। আমরা **৩টা আলাদা Django ORM class** হিসেবে করব:

1. **Class 120 — `bulk_create()`**
    
2. **Class 121 — `bulk_update()`**
    
3. **Class 122 — `bulk_delete()` / bulk deletion**
    

আমি প্রতিটাতে **Beginner → Real Project → Advanced usage → Beginner mistakes → Performance** দেখাব। একই `Product` model ব্যবহার করব, যাতে তিনটা concept একসাথে পরিষ্কার হয়।

---

# Class 120 — Django ORM `bulk_create()`

## 1. `bulk_create()` কী?

ধরো তোমাকে একসাথে 5,000টা product database-এ insert করতে হবে।

Normal way:

```python
for product in products:
    product.save()
```

এখানে 5,000টা object হলে প্রায় 5,000টা database query হতে পারে।

`bulk_create()`:

```python
Product.objects.bulk_create(products)
```

এতে Django একসাথে অনেকগুলো row insert করার চেষ্টা করে।

### সহজ ভাষায়

```text
save()
save()
save()
save()
save()
```

এর পরিবর্তে:

```text
bulk_create()
      ↓
একসাথে অনেক row INSERT
```

---

# 2. Model

ধরি আমাদের ecommerce application:

```python
# products/models.py

from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    sku = models.CharField(max_length=100, unique=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.PositiveIntegerField(default=0)
    is_active = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

---

# 3. Normal `create()`

```python
Product.objects.create(
    name="Laptop",
    sku="LAP-001",
    price=75000,
    stock=10
)

Product.objects.create(
    name="Mouse",
    sku="MOU-001",
    price=1200,
    stock=50
)
```

এখানে আলাদা create operation হচ্ছে।

---

# 4. `bulk_create()`

প্রথমে Python list:

```python
products = [
    Product(
        name="Laptop",
        sku="LAP-001",
        price=75000,
        stock=10
    ),
    Product(
        name="Mouse",
        sku="MOU-001",
        price=1200,
        stock=50
    ),
    Product(
        name="Keyboard",
        sku="KEY-001",
        price=2500,
        stock=30
    ),
]
```

তারপর:

```python
Product.objects.bulk_create(products)
```

ব্যস।

---

# 5. Complete Service Example

Professional project-এ এই ধরনের logic service layer-এ রাখা যায়।

```python
# products/services.py

from .models import Product


def import_products(product_data):

    products = []

    for data in product_data:
        products.append(
            Product(
                name=data["name"],
                sku=data["sku"],
                price=data["price"],
                stock=data["stock"],
            )
        )

    return Product.objects.bulk_create(products)
```

Call:

```python
data = [
    {
        "name": "Laptop",
        "sku": "LAP-001",
        "price": 75000,
        "stock": 10,
    },
    {
        "name": "Mouse",
        "sku": "MOU-001",
        "price": 1200,
        "stock": 50,
    },
    {
        "name": "Keyboard",
        "sku": "KEY-001",
        "price": 2500,
        "stock": 30,
    },
]

products = import_products(data)
```

---

# 6. কোথায় `bulk_create()` ব্যবহার করবে?

### খুব ভালো use case

### CSV import

```text
CSV
 ↓
10,000 products
 ↓
Python
 ↓
bulk_create()
 ↓
Database
```

### Excel import

```text
Excel → Python → bulk_create()
```

### API দিয়ে massive data import

```text
JSON
 ↓
1000 records
 ↓
bulk_create()
```

### Data migration

```python
Product.objects.bulk_create(products)
```

### Initial seed data

```python
categories = [
    Category(name="Electronics"),
    Category(name="Clothing"),
    Category(name="Books"),
]

Category.objects.bulk_create(categories)
```

---

# 7. `batch_size`

ধরো 100,000 records।

সব একবারে না পাঠিয়ে:

```python
Product.objects.bulk_create(
    products,
    batch_size=1000
)
```

মানে:

```text
1000
1000
1000
1000
...
```

এটা বড় dataset-এর ক্ষেত্রে useful।

---

# 8. Important limitation

`bulk_create()` normal `save()` এর মতো সব behavior trigger করে না।

বিশেষ করে:

```python
product.save()
```

এর custom logic থাকলে:

```python
def save(self, *args, **kwargs):
    ...
```

`bulk_create()` সেই `save()` method প্রতিটি object-এর জন্য call করে না।

তাই:

```python
class Product(models.Model):

    def save(self, *args, **kwargs):
        print("Custom logic")
        super().save(*args, **kwargs)
```

তারপর:

```python
Product.objects.bulk_create(products)
```

এখানে custom `save()` logic-এর উপর নির্ভর করা ঠিক হবে না।

---

# 9. Beginner Mistakes — `bulk_create()`

### ❌ Mistake 1

```python
products = []

for data in data_list:
    Product.objects.bulk_create(products)
```

এভাবে loop-এর ভিতরে bulk করা ঠিক না।

### ✅ Correct

```python
products = []

for data in data_list:
    products.append(Product(...))

Product.objects.bulk_create(products)
```

---

### ❌ Mistake 2 — huge list

```python
Product.objects.bulk_create(
    1_000_000_objects
)
```

সবসময় memory এবং database limits মাথায় রাখবে।

### Better

```python
Product.objects.bulk_create(
    products,
    batch_size=1000
)
```

---

### ❌ Mistake 3 — unique conflict ignore করা

ধরো:

```python
sku = models.CharField(
    max_length=100,
    unique=True
)
```

Duplicate SKU থাকলে database integrity error হতে পারে।

কিছু database/backend-এ conflict ignore করার option:

```python
Product.objects.bulk_create(
    products,
    ignore_conflicts=True
)
```

তবে এটা blindly ব্যবহার করবে না। Duplicate কেন হচ্ছে সেটা বুঝতে হবে।

---

# 10. Advanced Developer Pattern

ধরো external API থেকে 50,000 products এসেছে।

```python
def bulk_import_products(data):

    objects = [
        Product(
            name=item["name"],
            sku=item["sku"],
            price=item["price"],
            stock=item["stock"],
        )
        for item in data
    ]

    Product.objects.bulk_create(
        objects,
        batch_size=1000
    )
```

এটাই বাস্তব project-এ অনেক বেশি practical pattern।

---

# Class 120 Summary

|বিষয়|`bulk_create()`|
|---|---|
|কাজ|অনেক row INSERT|
|Use|Import/Seed/Migration|
|Performance|অনেক ভালো|
|`save()` call|প্রতি object-এ নয়|
|Custom save logic|সতর্ক|
|Large data|`batch_size`|
|Example|10,000 products|

---

# Class 121 — Django ORM `bulk_update()`

এবার ধরো database-এ already 10,000 products আছে।

সব product-এর price পরিবর্তন করতে হবে।

---

## 1. Normal way

```python
products = Product.objects.all()

for product in products:
    product.price += 100
    product.save()
```

এটা অনেক query তৈরি করতে পারে।

---

# 2. `bulk_update()`

প্রথমে objects retrieve:

```python
products = list(Product.objects.all())
```

তারপর Python-এ change:

```python
for product in products:
    product.price += 100
```

তারপর:

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

এটাই মূল concept।

```text
Database
   ↓
Fetch objects
   ↓
Python modification
   ↓
bulk_update()
   ↓
Database
```

---

# 3. Complete Example

ধরি:

```python
products = list(
    Product.objects.filter(is_active=True)
)
```

Price increase:

```python
for product in products:
    product.price = product.price * 1.10
```

তারপর:

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

সব active product-এর price update হবে।

---

# 4. একাধিক field update

```python
for product in products:
    product.price += 500
    product.stock += 10
    product.is_active = True
```

তারপর:

```python
Product.objects.bulk_update(
    products,
    ["price", "stock", "is_active"]
)
```

---

# 5. Real Project Example — Inventory

ধরো supplier থেকে নতুন stock এসেছে:

```python
updates = {
    "LAP-001": 20,
    "MOU-001": 50,
    "KEY-001": 30,
}
```

Products:

```python
products = list(
    Product.objects.filter(
        sku__in=updates.keys()
    )
)
```

Update:

```python
for product in products:
    product.stock = updates[product.sku]
```

তারপর:

```python
Product.objects.bulk_update(
    products,
    ["stock"]
)
```

এটা inventory system-এ খুব useful।

---

# 6. Real Project — Price Update

ধরো admin Excel upload করেছে:

```text
SKU       New Price

LAP-001   80000
MOU-001   1500
KEY-001   3000
```

Python:

```python
price_map = {
    "LAP-001": 80000,
    "MOU-001": 1500,
    "KEY-001": 3000,
}
```

Fetch:

```python
products = list(
    Product.objects.filter(
        sku__in=price_map.keys()
    )
)
```

Update:

```python
for product in products:
    product.price = price_map[product.sku]
```

Bulk update:

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

---

# 7. `bulk_update()` এর সবচেয়ে important rule

এইটা:

```python
Product.objects.bulk_update(
    products,
    ["price", "stock"]
)
```

মানে Django-কে বলছো:

> এই objects-এর `price` এবং `stock` field database-এ update করো।

কিন্তু:

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

তাহলে শুধু price update হবে।

---

# 8. Beginner Mistake

### ❌ এটা কাজ করবে না

```python
products = Product.objects.all()

for product in products:
    product.price += 100

Product.objects.bulk_update(
    products,
    ["price"]
)
```

কিছু ক্ষেত্রে QuerySet সরাসরি ব্যবহার করা যায়/iteration করা যায়, কিন্তু professional এবং predictable bulk-update workflow-এর জন্য আগে list materialize করা ভালো:

```python
products = list(Product.objects.all())
```

---

# 9. Beginner Mistake — save() আশা করা

```python
product.price = 5000
Product.objects.bulk_update(...)
```

এখানে প্রতি object-এর:

```python
save()
```

call হচ্ছে না।

তাই custom `save()` logic-এর উপর নির্ভর করবে না।

---

# 10. `auto_now`

ধরো:

```python
updated_at = models.DateTimeField(auto_now=True)
```

Bulk update করলে `save()` lifecycle bypass হওয়ায় `auto_now`-এর automatic behavior-এর উপর নির্ভর করা উচিত নয়।

প্রয়োজনে manually:

```python
from django.utils import timezone

now = timezone.now()

for product in products:
    product.price += 100
    product.updated_at = now
```

তারপর:

```python
Product.objects.bulk_update(
    products,
    ["price", "updated_at"]
)
```

---

# 11. Advanced Developer — batch update

Large dataset:

```python
Product.objects.bulk_update(
    products,
    ["price", "stock"],
    batch_size=1000
)
```

এটা production environment-এ useful।

---

# 12. কখন `bulk_update()` ব্যবহার করবে?

|Situation|Use|
|---|---|
|1 object|`save()`|
|5 objects|সাধারণত `save()` যথেষ্ট|
|10,000 objects|`bulk_update()`|
|Excel price update|`bulk_update()`|
|Inventory synchronization|`bulk_update()`|
|Mass status update|`bulk_update()`|

---

# Class 121 Summary

```python
products = list(Product.objects.filter(...))

for product in products:
    product.stock += 10
    product.price += 100

Product.objects.bulk_update(
    products,
    ["stock", "price"],
    batch_size=1000
)
```

**মূল idea:**

> Object আগে database থেকে আনবে → Python-এ পরিবর্তন করবে → একসাথে database-এ update করবে।

---

# Class 122 — Bulk Delete

এবার সবচেয়ে সহজটা।

ধরো:

```text
Product
1
2
3
4
5
```

তুমি inactive products delete করতে চাও।

---

# 1. Normal individual delete

```python
products = Product.objects.filter(
    is_active=False
)

for product in products:
    product.delete()
```

এটা প্রয়োজনের তুলনায় inefficient হতে পারে।

---

# 2. QuerySet `.delete()`

সরাসরি:

```python
Product.objects.filter(
    is_active=False
).delete()
```

এটাই Django ORM-এর bulk deletion pattern।

---

# 3. Complete Example

Inactive products:

```python
Product.objects.filter(
    is_active=False
).delete()
```

যেমন:

```text
Before:

Laptop     active
Mouse      inactive
Keyboard   inactive
Monitor    active

After:

Laptop
Monitor
```

---

# 4. Specific IDs

```python
Product.objects.filter(
    id__in=[10, 20, 30, 40]
).delete()
```

---

# 5. Date-based deletion

ধরো old temporary records:

```python
from datetime import timedelta
from django.utils import timezone

threshold = timezone.now() - timedelta(days=30)

Product.objects.filter(
    created_at__lt=threshold,
    is_active=False
).delete()
```

---

# 6. Real Project — Cart cleanup

ধরো abandoned carts:

```python
Cart.objects.filter(
    is_active=False,
    updated_at__lt=threshold
).delete()
```

---

# 7. Real Project — Soft Delete হলে?

এখানে খুব important distinction আছে।

তোমার model যদি:

```python
is_deleted = models.BooleanField(default=False)
```

হয়, তাহলে:

```python
Product.objects.filter(
    id__in=ids
).delete()
```

করলে **real database deletion** হতে পারে।

Soft delete চাইলে:

```python
Product.objects.filter(
    id__in=ids
).update(
    is_deleted=True
)
```

এক্ষেত্রে actual row database থেকে remove হচ্ছে না।

---

# 8. Hard Delete বনাম Soft Delete

### Hard delete

```python
Product.objects.filter(
    is_active=False
).delete()
```

```text
Database row
     ↓
Removed
```

### Soft delete

```python
Product.objects.filter(
    is_active=False
).update(
    is_deleted=True
)
```

```text
Database row
     ↓
Still exists
     ↓
is_deleted=True
```

Professional systems-এ অনেক সময় soft delete preferable, বিশেষ করে business/audit data-তে।

---

# 9. সবচেয়ে গুরুত্বপূর্ণ Beginner Mistake

অনেকে ভাবে:

```python
Product.objects.filter(...).delete()
```

মানে শুধু Product table-এর rows delete হবে।

কিন্তু Django relational database-এ related objects-এর উপর **cascade/protection/set-null ইত্যাদি `on_delete` behavior** কাজ করতে পারে।

যেমন:

```python
class OrderItem(models.Model):
    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE
    )
```

Product delete করলে related `OrderItem`-ও cascade হতে পারে।

তাই production-এ:

```python
Product.objects.filter(...).delete()
```

লিখার আগে relationships অবশ্যই check করবে।

---

# 10. `delete()` এর return value

```python
deleted_count, details = Product.objects.filter(
    is_active=False
).delete()
```

যেমন:

```python
print(deleted_count)
```

এতে কতগুলো object delete হয়েছে তার count পাওয়া যায়; related cascade-এর কারণে deleted object count একাধিক model-এর rows-ও অন্তর্ভুক্ত করতে পারে।

---

# 11. Advanced Developer Pattern

ধরো admin bulk delete করতে চাচ্ছে:

```python
product_ids = [10, 20, 30, 40]
```

Service:

```python
def delete_products(product_ids):

    queryset = Product.objects.filter(
        id__in=product_ids
    )

    deleted_count, _ = queryset.delete()

    return deleted_count
```

তারপর:

```python
count = delete_products([10, 20, 30])
```

---

# 12. API Example

DRF-এ admin bulk delete endpoint:

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .models import Product


class BulkDeleteProductView(APIView):

    def post(self, request):

        product_ids = request.data.get("ids", [])

        if not product_ids:
            return Response(
                {"detail": "No product IDs provided."},
                status=status.HTTP_400_BAD_REQUEST
            )

        deleted_count, _ = Product.objects.filter(
            id__in=product_ids
        ).delete()

        return Response({
            "deleted": deleted_count
        })
```

Request:

```json
{
    "ids": [10, 20, 30, 40]
}
```

এটা বাস্তব admin dashboard-এর bulk delete feature-এর basic architecture।

---

# তিনটার সবচেয়ে important comparison

|Operation|ORM|কাজ|
|---|---|---|
|Insert many|`bulk_create()`|অনেক row তৈরি|
|Update many|`bulk_update()`|অনেক existing row update|
|Delete many|`.delete()`|অনেক row delete|

---

# Real-world workflow

ধরো তোমার **Multi-Vendor Ecommerce** project।

## Supplier থেকে 10,000 products এসেছে

```python
Product.objects.bulk_create(
    products,
    batch_size=1000
)
```

### Result

```text
Supplier
   ↓
CSV/Excel/API
   ↓
Python
   ↓
bulk_create()
   ↓
Product table
```

---

## Supplier নতুন price পাঠাল

```python
products = list(
    Product.objects.filter(
        sku__in=price_map.keys()
    )
)

for product in products:
    product.price = price_map[product.sku]

Product.objects.bulk_update(
    products,
    ["price"],
    batch_size=1000
)
```

---

## পুরোনো temporary products remove করতে হবে

```python
Product.objects.filter(
    is_temporary=True,
    created_at__lt=threshold
).delete()
```

---

# ⭐ Beginner বনাম Professional Developer

### Beginner

```python
for product in products:
    product.save()
```

### Intermediate

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

### Advanced

```python
Product.objects.bulk_update(
    products,
    ["price", "stock"],
    batch_size=1000
)
```

সাথে:

- transaction
    
- validation
    
- permission
    
- database constraints
    
- indexing
    
- error handling
    
- logging
    
- audit trail
    
- batch processing
    

consider করবে।

---

# ⚠️ তিনটার Common Mistakes

### 1. Validation automatically ধরে নেওয়া

Bulk operations-এ individual model `save()` lifecycle-এর উপর নির্ভর করা উচিত নয়।

যদি business validation লাগে:

```python
for data in data_list:
    # validate first
    ...
```

তারপর bulk operation।

---

### 2. Signals-এর উপর blindly depend করা

Bulk operations-এ individual `save()`/`delete()` workflow-এর মতো behavior সবসময় পাওয়া যাবে—এমন assumption করা dangerous।

বিশেষ করে:

```python
post_save
pre_save
```

এর উপর business-critical logic রেখে bulk operation করলে সমস্যা হতে পারে।

---

### 3. সবসময় bulk operation ব্যবহার করা

এটাও ভুল।

একটা object হলে:

```python
product.save()
```

অনেক object হলে:

```python
bulk_update()
```

এই distinction মনে রাখবে।

---

# 🧠 সবচেয়ে সহজে মনে রাখার Formula

```text
NEW MANY ROWS
      ↓
bulk_create()
```

```text
EXISTING MANY ROWS
      ↓
bulk_update()
```

```text
REMOVE MANY ROWS
      ↓
QuerySet.delete()
```

আর একটা গুরুত্বপূর্ণ distinction:

```text
Many rows একই value দিয়ে update
             ↓
QuerySet.update()
```

যেমন:

```python
Product.objects.filter(
    is_active=True
).update(
    stock=0
)
```

কিন্তু প্রতিটি object-এর **আলাদা calculated value** থাকলে:

```python
bulk_update()
```

ব্যবহার করা যায়।

---

## 🔥 Professional decision tree

```text
কতগুলো object?
       │
       ├── 1-2
       │    └── save()/delete()
       │
       └── অনেক
            │
            ├── নতুন?
            │     └── bulk_create()
            │
            ├── existing update?
            │     │
            │     ├── একই value?
            │     │      └── QuerySet.update()
            │     │
            │     └── আলাদা আলাদা value?
            │            └── bulk_update()
            │
            └── remove?
                  └── QuerySet.delete()
```

**এই decision tree-টা Django ORM professional কাজের জন্য খুব গুরুত্বপূর্ণ।**


----

# Class 123 — `QuerySet.update()` vs `bulk_update()` — Professional Level

আগের ৩টা class-এ আমরা দেখেছি:

- `bulk_create()` → অনেক নতুন row insert
    
- `bulk_update()` → অনেক existing object-এর **ভিন্ন ভিন্ন value** update
    
- `QuerySet.delete()` → অনেক row delete
    

আজকের class-এ খুব important একটা confusion clear করব:

> **`update()` আর `bulk_update()` এর মধ্যে পার্থক্য কী? কোনটা কখন ব্যবহার করব?**

---

# 1. `QuerySet.update()` কী?

ধরো সব inactive product-এর stock `0` করতে হবে।

```python
Product.objects.filter(
    is_active=False
).update(
    stock=0
)
```

এখানে database-কে সরাসরি বলা হচ্ছে:

```text
যেসব product inactive
        ↓
stock = 0
```

---

# 2. Complete Example

Model:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    sku = models.CharField(max_length=100, unique=True)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
    stock = models.PositiveIntegerField(default=0)
    is_active = models.BooleanField(default=True)
```

এখন:

```python
Product.objects.filter(
    is_active=False
).update(
    stock=0
)
```

---

# 3. কেন `update()` এত fast?

ধরো 50,000 products আছে।

### ❌ Python loop

```python
products = Product.objects.filter(
    is_active=False
)

for product in products:
    product.stock = 0
    product.save()
```

এখানে Django-কে অনেক individual update করতে হতে পারে।

### ✅ `update()`

```python
Product.objects.filter(
    is_active=False
).update(stock=0)
```

Database সরাসরি matching rows update করে।

Conceptually:

```sql
UPDATE product
SET stock = 0
WHERE is_active = false;
```

---

# 4. `update()` বনাম `bulk_update()`

এটাই আজকের সবচেয়ে important অংশ।

### `update()`

সব selected row-তে একই expression/value দিতে পারো।

```python
Product.objects.filter(
    is_active=True
).update(
    stock=100
)
```

সবগুলোর:

```text
stock = 100
```

---

### `bulk_update()`

প্রতিটি object-এর value আলাদা হতে পারে।

```python
products = list(
    Product.objects.filter(
        sku__in=["LAP-001", "MOU-001", "KEY-001"]
    )
)

for product in products:

    if product.sku == "LAP-001":
        product.price = 80000

    elif product.sku == "MOU-001":
        product.price = 1500

    elif product.sku == "KEY-001":
        product.price = 3000

Product.objects.bulk_update(
    products,
    ["price"]
)
```

এখানে:

```text
LAP-001 → 80000
MOU-001 → 1500
KEY-001 → 3000
```

প্রতিটির value আলাদা।

---

# 5. Simple Comparison

|Situation|Best choice|
|---|---|
|সব row-তে same value|`update()`|
|প্রতিটি object-এর আলাদা value|`bulk_update()`|
|নতুন অনেক object|`bulk_create()`|
|অনেক row delete|`.delete()`|
|একটি object update|`.save()`|

---

# 6. `F()` Expression + `update()`

এটা professional Django ORM-এর খুব important technique।

ধরো সব product-এর price 10% increase করতে হবে।

### ❌ Python দিয়ে

```python
products = list(Product.objects.all())

for product in products:
    product.price = product.price * 1.10

Product.objects.bulk_update(
    products,
    ["price"]
)
```

কাজ করবে।

কিন্তু এখানে database থেকে objects Python-এ আনতে হচ্ছে।

---

### ✅ Better

```python
from django.db.models import F

Product.objects.update(
    price=F("price") * 1.10
)
```

Database নিজেই calculation করবে।

Conceptually:

```sql
UPDATE product
SET price = price * 1.10;
```

এটা অনেক efficient।

---

# 7. Inventory Example

ধরো 1000টা product-এর stock থেকে 5 কমাতে হবে।

### ❌ Python

```python
products = list(Product.objects.all())

for product in products:
    product.stock -= 5

Product.objects.bulk_update(
    products,
    ["stock"]
)
```

### ✅ Database-side calculation

```python
from django.db.models import F

Product.objects.filter(
    stock__gte=5
).update(
    stock=F("stock") - 5
)
```

এটা inventory system-এর জন্য খুব useful।

---

# 8. `F()` কেন গুরুত্বপূর্ণ?

ধরো দুইজন customer একই সময়ে product কিনছে।

Current stock:

```text
100
```

Customer A:

```text
100 → 99
```

Customer B:

```text
100 → 99
```

যদি naive read-modify-write করা হয়, concurrency issue হতে পারে।

Database-side expression:

```python
Product.objects.filter(
    id=product_id,
    stock__gt=0
).update(
    stock=F("stock") - 1
)
```

এখানে database-কে বলা হচ্ছে:

> stock-এর বর্তমান value থেকে 1 কমাও।

এটা concurrency-sensitive inventory logic-এর গুরুত্বপূর্ণ building block।

---

# 9. Update Result Check করা

`update()` কতগুলো row পরিবর্তন করেছে সেটা return করে।

```python
updated = Product.objects.filter(
    is_active=False
).update(
    stock=0
)

print(updated)
```

যদি:

```text
250
```

তাহলে 250 matching rows update হয়েছে।

এটা API response-এর জন্য useful:

```python
return Response({
    "updated": updated
})
```

---

# 10. Beginner Mistake — `update()` এর পরে object auto-refresh হবে ভাবা

```python
product = Product.objects.get(id=1)

Product.objects.filter(
    id=1
).update(
    price=5000
)

print(product.price)
```

এখানে Python object-এর `price` automatically refresh হয়েছে ধরে নেওয়া ঠিক না।

প্রয়োজনে:

```python
product.refresh_from_db()
```

তারপর:

```python
print(product.price)
```

---

# 11. Beginner Mistake — `save()` logic expect করা

```python
Product.objects.filter(
    is_active=True
).update(
    price=5000
)
```

এখানে প্রতি object-এর `save()` method manually call হচ্ছে না।

তাই এমন business logic থাকলে:

```python
def save(self, *args, **kwargs):
    # custom logic
    ...
```

`update()` ব্যবহার করার আগে সেই logic-এর প্রয়োজন আছে কিনা বুঝতে হবে।

---

# 12. `update()` + `Case/When`

এটা advanced ORM-এর খুব powerful feature।

ধরো:

```text
stock > 100 → price + 10%
stock 50-100 → price + 5%
stock < 50 → price unchanged
```

Python loop না করে database expression ব্যবহার করতে পারো।

```python
from django.db.models import F, Case, When, Value
from django.db.models import DecimalField

Product.objects.update(
    price=Case(
        When(
            stock__gt=100,
            then=F("price") * 1.10
        ),
        When(
            stock__gte=50,
            then=F("price") * 1.05
        ),
        default=F("price"),
        output_field=DecimalField(
            max_digits=10,
            decimal_places=2
        )
    )
)
```

এখানে database নিজেই decision নিচ্ছে।

---

# 13. `bulk_update()` কখন better?

ধরো external supplier পাঠিয়েছে:

```python
price_map = {
    "LAP-001": 80000,
    "MOU-001": 1500,
    "KEY-001": 3000,
}
```

প্রতিটি SKU-এর price আলাদা।

তখন:

```python
products = list(
    Product.objects.filter(
        sku__in=price_map.keys()
    )
)

for product in products:
    product.price = price_map[product.sku]

Product.objects.bulk_update(
    products,
    ["price"],
    batch_size=1000
)
```

এখানে `update()` সহজে এই per-object mapping handle করবে না।

---

# 14. Professional Rule

এই ৪টা pattern মাথায় রাখো:

### Pattern 1 — Same value

```python
Product.objects.filter(
    is_active=False
).update(
    stock=0
)
```

### Pattern 2 — Database calculation

```python
Product.objects.update(
    price=F("price") * 1.10
)
```

### Pattern 3 — Different values per object

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

### Pattern 4 — New objects

```python
Product.objects.bulk_create(
    products
)
```

---

# 15. Real Ecommerce Example

ধরো তোমার ecommerce admin panel-এ তিনটা operation আছে।

### Admin selects 500 products → deactivate

```python
Product.objects.filter(
    id__in=product_ids
).update(
    is_active=False
)
```

### Admin selects 500 products → প্রতিটির আলাদা price

```python
Product.objects.bulk_update(
    products,
    ["price"]
)
```

### Supplier → 10,000 new products

```python
Product.objects.bulk_create(
    products,
    batch_size=1000
)
```

এটাই বাস্তব project-এ তিনটার ব্যবহার।

---

# 🧠 আজকের Final Cheat Sheet

```text
                 MANY ROWS
                    │
        ┌───────────┼───────────┐
        │           │           │
      INSERT      UPDATE      DELETE
        │           │           │
bulk_create()      │        QuerySet.delete()
                    │
              ┌─────┴─────┐
              │           │
         SAME VALUE    DIFFERENT
              │           │
          update()   bulk_update()
```

### সবচেয়ে important:

> **`update()` = database-এ সরাসরি একই value/expression দিয়ে অনেক row update**

> **`bulk_update()` = Python objects-এর আলাদা আলাদা পরিবর্তন একসাথে database-এ পাঠানো**

> **`bulk_create()` = অনেক নতুন object insert**

> **`.delete()` = matching rows এবং সম্পর্কিত cascade behavior অনুযায়ী delete**

পরের logical class হবে **Class 124 — Django ORM Transactions (`transaction.atomic`)**, যেখানে দেখব bulk operations-এর সাথে **rollback, commit, partial failure, এবং real-world order/payment/inventory transaction** কীভাবে handle করতে হয়।


----
# Class 124 — Django ORM Transactions (`transaction.atomic`)

আজকের class-টা Django ORM-এর **খুব গুরুত্বপূর্ণ professional topic**। বিশেষ করে Ecommerce, Hotel Booking, Banking, Payment, Inventory, Order Management—এই ধরনের system বানাতে transaction ভালোভাবে বুঝতে হবে।

আজ আমরা শিখব:

1. Transaction কী?
    
2. `commit` কী?
    
3. `rollback` কী?
    
4. `transaction.atomic()` কী?
    
5. Partial failure কী?
    
6. Bulk operation + transaction
    
7. Real-world Order + Inventory example
    
8. Payment transaction
    
9. Nested `atomic()`
    
10. `atomic()` + exception handling
    
11. `select_for_update()` দিয়ে concurrency
    
12. Beginner mistakes
    
13. Advanced production pattern
    

---

# 1. Transaction কী?

সহজভাবে:

> **একাধিক database operation-কে একটি logical unit হিসেবে execute করাই transaction-এর মূল ধারণা।**

ধরো customer একটি product কিনল।

একটি order তৈরি করতে আমাদের ৪টা কাজ করতে হবে:

```text
1. Order তৈরি
2. OrderItem তৈরি
3. Product stock কমানো
4. Payment record তৈরি
```

ধরো:

```text
Order       ✅
OrderItem   ✅
Stock       ✅
Payment     ❌
```

এখন database-এ order আছে কিন্তু payment নেই।

এটা business-এর জন্য সমস্যা হতে পারে।

Transaction ব্যবহার করলে:

```text
Order       ✅
OrderItem   ✅
Stock       ❌
Payment     ❌
        ↓
ROLLBACK
        ↓
সব আগের অবস্থায়
```

অর্থাৎ পুরো operation সফল না হলে transaction rollback করা যায়।

---

# 2. ACID-এর সাথে সম্পর্ক

DBMS-এ তুমি আগে ACID পড়েছ।

Transaction-এর চারটি গুরুত্বপূর্ণ property:

|ACID|Meaning|
|---|---|
|Atomicity|সব হবে অথবা কিছুই হবে না|
|Consistency|Database valid state-এ থাকবে|
|Isolation|Concurrent transaction একে অপরকে কীভাবে দেখবে তা নিয়ন্ত্রণ|
|Durability|Commit হওয়ার পর data স্থায়ী থাকবে|

আজকের class-এ সবচেয়ে বেশি focus:

> **Atomicity**

---

# 3. Django-তে Transaction

Django দেয়:

```python
from django.db import transaction
```

তারপর:

```python
with transaction.atomic():
    ...
```

এটাই সবচেয়ে common pattern।

---

# 4. Basic Example

```python
from django.db import transaction

with transaction.atomic():

    Product.objects.create(
        name="Laptop",
        sku="LAP-001",
        price=75000,
        stock=10
    )

    Product.objects.create(
        name="Mouse",
        sku="MOU-001",
        price=1200,
        stock=50
    )
```

Block সফল হলে:

```text
COMMIT
```

---

# 5. Exception হলে কী হয়?

```python
from django.db import transaction

with transaction.atomic():

    Product.objects.create(
        name="Laptop",
        sku="LAP-001",
        price=75000
    )

    raise Exception("Something went wrong")
```

Exception বের হলে transaction rollback হবে।

Concept:

```text
BEGIN
 ↓
INSERT Laptop
 ↓
Exception ❌
 ↓
ROLLBACK
```

Laptop insertion-টাও rollback হবে।

---

# 6. Commit কী?

Transaction-এর সব operation সফল হলে database changes permanently save করার process হলো:

> **COMMIT**

Concept:

```text
BEGIN
 ↓
INSERT
 ↓
UPDATE
 ↓
INSERT
 ↓
COMMIT
```

Django-তে:

```python
with transaction.atomic():
    ...
```

block সফলভাবে শেষ হলে Django transaction commit করার ব্যবস্থা করে।

---

# 7. Rollback কী?

কোনো operation failure হলে transaction-এর পরিবর্তন বাতিল করে আগের consistent state-এ ফিরে যাওয়া হলো:

> **ROLLBACK**

Example:

```python
with transaction.atomic():

    order = Order.objects.create(...)

    item = OrderItem.objects.create(...)

    raise ValueError("Invalid order")
```

Result:

```text
Order       → rollback
OrderItem   → rollback
```

---

# 8. Partial Failure কী?

এটা খুব important।

ধরো:

```python
order = Order.objects.create(...)
```

সফল।

তারপর:

```python
order_item = OrderItem.objects.create(...)
```

সফল।

তারপর:

```python
payment = Payment.objects.create(...)
```

failure।

Transaction না থাকলে:

```text
Order       ✅
OrderItem   ✅
Payment     ❌
```

Database inconsistent হতে পারে।

Transaction থাকলে:

```text
Order       ✅
OrderItem   ✅
Payment     ❌
       ↓
ROLLBACK
       ↓
Order       ❌
OrderItem   ❌
Payment     ❌
```

---

# 9. Real Ecommerce Model

এখন একটা realistic example করি।

## Product

```python
class Product(models.Model):

    name = models.CharField(max_length=200)

    sku = models.CharField(
        max_length=100,
        unique=True
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.PositiveIntegerField(
        default=0
    )
```

---

## Order

```python
class Order(models.Model):

    class Status(models.TextChoices):
        PENDING = "pending"
        CONFIRMED = "confirmed"
        CANCELLED = "cancelled"

    user = models.ForeignKey(
        "auth.User",
        on_delete=models.CASCADE
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

## OrderItem

```python
class OrderItem(models.Model):

    order = models.ForeignKey(
        Order,
        on_delete=models.CASCADE,
        related_name="items"
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT
    )

    quantity = models.PositiveIntegerField()

    unit_price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )
```

---

## Payment

```python
class Payment(models.Model):

    class Status(models.TextChoices):
        PENDING = "pending"
        SUCCESS = "success"
        FAILED = "failed"

    order = models.OneToOneField(
        Order,
        on_delete=models.CASCADE,
        related_name="payment"
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )

    transaction_id = models.CharField(
        max_length=200,
        unique=True,
        null=True,
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

# 10. Complete Order Transaction

ধরো customer order করছে।

```python
from django.db import transaction
from django.shortcuts import get_object_or_404


@transaction.atomic
def create_order(user, product, quantity):

    if product.stock < quantity:
        raise ValueError("Insufficient stock")

    total = product.price * quantity

    order = Order.objects.create(
        user=user,
        total_amount=total,
        status=Order.Status.CONFIRMED
    )

    OrderItem.objects.create(
        order=order,
        product=product,
        quantity=quantity,
        unit_price=product.price,
        subtotal=total
    )

    product.stock -= quantity
    product.save(
        update_fields=["stock"]
    )

    Payment.objects.create(
        order=order,
        amount=total,
        status=Payment.Status.PENDING
    )

    return order
```

এখানে:

```text
create_order()
       │
       ├── Order
       ├── OrderItem
       ├── Stock update
       └── Payment
```

সব সফল হলে:

```text
COMMIT
```

কোনো exception হলে:

```text
ROLLBACK
```

---

# 11. `with transaction.atomic()` Version

Decorator-এর বদলে:

```python
def create_order(user, product, quantity):

    with transaction.atomic():

        if product.stock < quantity:
            raise ValueError(
                "Insufficient stock"
            )

        total = product.price * quantity

        order = Order.objects.create(
            user=user,
            total_amount=total,
            status=Order.Status.CONFIRMED
        )

        OrderItem.objects.create(
            order=order,
            product=product,
            quantity=quantity,
            unit_price=product.price,
            subtotal=total
        )

        product.stock -= quantity

        product.save(
            update_fields=["stock"]
        )

        Payment.objects.create(
            order=order,
            amount=total,
            status=Payment.Status.PENDING
        )

    return order
```

এটাও professional pattern।

---

# 12. Bulk Create + Transaction

এখন আগের class-এর knowledge ব্যবহার করি।

ধরো order-এর অনেক item আছে।

```python
with transaction.atomic():

    order = Order.objects.create(
        user=user,
        total_amount=total
    )

    items = []

    for item in cart_items:

        items.append(
            OrderItem(
                order=order,
                product=item.product,
                quantity=item.quantity,
                unit_price=item.product.price,
                subtotal=(
                    item.product.price *
                    item.quantity
                )
            )
        )

    OrderItem.objects.bulk_create(
        items,
        batch_size=1000
    )
```

এখানে:

```text
Order create
     ↓
Prepare items
     ↓
bulk_create
     ↓
Commit
```

কোনো failure হলে পুরো transaction rollback হতে পারে।

---

# 13. Bulk Update + Transaction

ধরো warehouse থেকে 1000 products-এর stock update হচ্ছে।

```python
with transaction.atomic():

    products = list(
        Product.objects.filter(
            sku__in=stock_map.keys()
        )
    )

    for product in products:
        product.stock = stock_map[
            product.sku
        ]

    Product.objects.bulk_update(
        products,
        ["stock"],
        batch_size=1000
    )
```

এটা useful যখন:

> Stock synchronization অবশ্যই পুরোটা সফল হতে হবে।

---

# 14. Bulk Delete + Transaction

```python
with transaction.atomic():

    Product.objects.filter(
        is_active=False
    ).delete()

    AuditLog.objects.create(
        action="inactive_products_deleted"
    )
```

যদি audit log creation failure করে:

```text
Product delete
      ↓
AuditLog ❌
      ↓
ROLLBACK
```

তাই business requirement অনুযায়ী delete-টাও rollback হতে পারে।

---

# 15. ⚠️ Important: `atomic()` Payment নিজে rollback করতে পারে না

এটা beginnerদের সবচেয়ে common confusion।

ধরো:

```python
with transaction.atomic():

    order = Order.objects.create(...)

    payment_gateway.charge(...)
```

External payment gateway যদি টাকা charge করে ফেলল, তারপর Django transaction rollback করলেও:

```text
Database → rollback
External payment → automatically rollback হবে না
```

কারণ external service তোমার database transaction-এর অংশ নয়।

---

# 16. Real Payment Architecture

সাধারণ pattern:

```text
Create Order
      ↓
Create Payment Pending
      ↓
Call Payment Gateway
      ↓
Gateway response
      │
      ├── Success
      │      ↓
      │   DB transaction
      │      ↓
      │   Payment = SUCCESS
      │   Order = CONFIRMED
      │
      └── Failed
             ↓
          Payment = FAILED
          Order = CANCELLED
```

Payment gateway-এর সাথে database transactionকে একই atomic transaction ধরে নেওয়া যাবে না।

---

# 17. `transaction.atomic()` + Exception Handling

এখানে সাবধান হতে হবে।

### Risky pattern

```python
try:

    with transaction.atomic():

        Order.objects.create(...)

        raise ValueError("Failed")

except ValueError:
    print("Error")
```

এটা ঠিকভাবে rollback করবে, কারণ exception atomic block-এর বাইরে বের হচ্ছে।

---

# 18. Dangerous Pattern

Atomic block-এর ভিতরে exception catch করে ফেললে সমস্যা হতে পারে:

```python
with transaction.atomic():

    try:
        Order.objects.create(...)
        raise ValueError("Error")

    except ValueError:
        print("Error")
```

এখানে exception block-এর ভিতরেই handle হয়ে যাচ্ছে।

তাই transaction failure semantics নিয়ে খুব সতর্ক হতে হবে।

### Better

```python
try:

    with transaction.atomic():

        Order.objects.create(...)

        raise ValueError("Error")

except ValueError:
    print("Order creation failed")
```

---

# 19. Nested `atomic()`

Django-তে nested atomic করা যায়।

```python
with transaction.atomic():

    order = Order.objects.create(...)

    with transaction.atomic():

        OrderItem.objects.create(...)

        Payment.objects.create(...)
```

এখানে inner atomic সাধারণত database savepoint ব্যবহার করে।

Concept:

```text
Outer transaction
       ↓
Order
       ↓
Savepoint
       ↓
OrderItem
Payment
       ↓
Savepoint release
       ↓
Commit
```

---

# 20. Nested Transaction-এর Practical Use

ধরো:

```python
with transaction.atomic():

    create_order()

    try:

        with transaction.atomic():
            create_optional_record()

    except Exception:
        pass
```

এখানে inner operation failure হলে inner savepoint rollback করা যেতে পারে, কিন্তু outer transaction চালিয়ে যাওয়া সম্ভব হতে পারে।

এটা advanced pattern।

---

# 21. `select_for_update()` — খুব গুরুত্বপূর্ণ

এখন আমরা transaction-এর সাথে concurrency problem দেখব।

ধরো product stock:

```text
stock = 1
```

একই সময়ে:

```text
Customer A → buys 1
Customer B → buys 1
```

দুইজন একই stock দেখতে পারে।

এখানে row locking দরকার হতে পারে।

---

# 22. `select_for_update()`

```python
with transaction.atomic():

    product = Product.objects.select_for_update().get(
        id=product_id
    )

    if product.stock < quantity:
        raise ValueError(
            "Insufficient stock"
        )

    product.stock -= quantity

    product.save(
        update_fields=["stock"]
    )
```

`select_for_update()` transaction চলাকালে selected database row-কে lock করার জন্য ব্যবহৃত হয়, যাতে concurrent transaction-এর সাথে race condition কমানো যায়।

---

# 23. Real Inventory Flow

```text
Customer A
     │
     ▼
BEGIN TRANSACTION
     │
     ▼
select_for_update()
     │
     ▼
Product Row LOCK
     │
     ▼
stock check
     │
     ▼
stock -= quantity
     │
     ▼
COMMIT
     │
     ▼
LOCK RELEASE
```

অন্য concurrent transaction-কে row lock-এর কারণে অপেক্ষা করতে হতে পারে, database/backend configuration অনুযায়ী।

---

# 24. Professional Order Function

এখন সব একসাথে:

```python
from django.db import transaction


@transaction.atomic
def create_order(user, product_id, quantity):

    product = (
        Product.objects
        .select_for_update()
        .get(id=product_id)
    )

    if product.stock < quantity:
        raise ValueError(
            "Insufficient stock"
        )

    total = (
        product.price *
        quantity
    )

    order = Order.objects.create(
        user=user,
        total_amount=total,
        status=Order.Status.CONFIRMED
    )

    OrderItem.objects.create(
        order=order,
        product=product,
        quantity=quantity,
        unit_price=product.price,
        subtotal=total
    )

    product.stock -= quantity

    product.save(
        update_fields=["stock"]
    )

    Payment.objects.create(
        order=order,
        amount=total,
        status=Payment.Status.PENDING
    )

    return order
```

এখানে তিনটি major concept:

```text
transaction.atomic()
        +
select_for_update()
        +
update_fields
```

---

# 25. `update_fields` কেন?

Instead of:

```python
product.save()
```

আমরা লিখেছি:

```python
product.save(
    update_fields=["stock"]
)
```

মানে শুধু `stock` field update করার intention প্রকাশ করছি।

Large models-এ এটা useful optimization এবং code clarity দিতে পারে।

---

# 26. Transaction Isolation

Database transaction-এর আরেকটি advanced topic হলো **isolation level**।

Common concepts:

```text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
```

সব database একই default ব্যবহার করে না।

Django application-এ সাধারণত database-এর configured isolation behavior বুঝে কাজ করতে হয়।

---

# 27. `atomic()` কি সব concurrency problem solve করে?

**না।**

এটা খুব important।

```python
with transaction.atomic():
    ...
```

মানে transaction boundary তৈরি হয়েছে।

কিন্তু race condition automatically সবসময় solve হবে না।

প্রয়োজনে:

```python
select_for_update()
```

বা database constraints/conditional updates ব্যবহার করতে হতে পারে।

---

# 28. Database Constraint + Transaction

ধরো booking system:

```python
class Booking(models.Model):

    room = models.ForeignKey(
        Room,
        on_delete=models.CASCADE
    )

    start_date = models.DateField()
    end_date = models.DateField()
```

শুধু:

```python
with transaction.atomic():
    ...
```

দিয়ে সব ধরনের double booking problem solve হবে না।

Business rule অনুযায়ী:

- locking
    
- constraints
    
- transaction
    
- proper validation
    

একসাথে design করতে হয়।

---

# 29. Beginner Mistake — পুরো function-কে transaction করা

এটা:

```python
@transaction.atomic
def huge_function():
    # 500 lines
    ...
```

সবসময় ভালো architecture নয়।

যদি function-এর মধ্যে:

- external API
    
- slow calculation
    
- file processing
    
- network request
    

থাকে, transaction unnecessarily দীর্ঘ হতে পারে।

Better:

```text
Validate
   ↓
Prepare
   ↓
Short DB transaction
   ↓
Commit
```

Transaction যত প্রয়োজন ততক্ষণই রাখার চেষ্টা করবে।

---

# 30. Beginner Mistake — External API transaction-এর ভিতরে

Avoid:

```python
with transaction.atomic():

    order = create_order()

    requests.post(
        "external-service"
    )

    update_payment()
```

Network request slow হলে database transaction দীর্ঘ সময় open থাকতে পারে।

Better architecture অনেক সময়:

```text
DB transaction
      ↓
Commit
      ↓
External processing
      ↓
Webhook/status update
```

Use case অনুযায়ী design করবে।

---

# 31. Beginner Mistake — `bulk_create()` + signals expect করা

```python
with transaction.atomic():

    Product.objects.bulk_create(
        products
    )
```

তারপর ধরে নেওয়া:

> প্রতিটি Product-এর `save()`/signal logic স্বাভাবিক individual-save flow-এর মতো চলেছে।

এটা ভুল assumption।

Bulk operation-এর lifecycle limitations মনে রাখবে।

---

# 32. Beginner Mistake — Rollback মানেই external side effect rollback

না।

যেমন:

```text
Database
Email
SMS
Payment
External API
File upload
```

সব একই transaction-এর মধ্যে নয়।

Database rollback করলে:

```text
Database → rollback
Email → already sent
SMS → already sent
Payment → may already be charged
```

তাই side effects-এর architecture আলাদাভাবে design করতে হয়।

---

# 33. Advanced Concept — `transaction.on_commit()`

এটা professional Django application-এ খুব useful।

ধরো order successfully commit হওয়ার পর email পাঠাতে চাও।

```python
from django.db import transaction


with transaction.atomic():

    order = Order.objects.create(
        ...
    )

    transaction.on_commit(
        lambda: send_order_email(order.id)
    )
```

এখন:

```text
Transaction সফল
      ↓
COMMIT
      ↓
send_order_email()
```

যদি transaction rollback হয়:

```text
ROLLBACK
      ↓
email callback execute হবে না
```

এটা side-effect handling-এর জন্য useful।

---

# 34. Celery-এর সাথে

Production application-এ:

```python
transaction.on_commit(
    lambda: send_order_email.delay(order.id)
)
```

Flow:

```text
Create Order
     ↓
Create OrderItem
     ↓
Commit
     ↓
Celery task
     ↓
Email
```

এটা খুব practical architecture।

---

# 35. Transaction + Bulk Operations — Complete Example

ধরো vendor একসাথে 5,000 inventory records update করেছে।

```python
from django.db import transaction


def sync_inventory(stock_map):

    with transaction.atomic():

        products = list(
            Product.objects.select_for_update().filter(
                sku__in=stock_map.keys()
            )
        )

        for product in products:
            product.stock = stock_map[
                product.sku
            ]

        Product.objects.bulk_update(
            products,
            ["stock"],
            batch_size=1000
        )
```

Architecture:

```text
BEGIN
  ↓
Lock rows
  ↓
Fetch products
  ↓
Modify Python objects
  ↓
bulk_update()
  ↓
COMMIT
```

---

# 36. Error হলে

ধরো 5,000 records-এর মধ্যে validation problem হলো:

```python
if product.stock < 0:
    raise ValueError("Invalid stock")
```

তাহলে:

```text
BEGIN
 ↓
Process
 ↓
Error
 ↓
ROLLBACK
```

আগের database state থাকবে।

---

# 37. কিন্তু সবসময় rollback চাইবে?

না।

কখনো তুমি চাইতে পারো:

```text
5000 records
   ↓
4900 valid
100 invalid
   ↓
4900 import
100 error report
```

এটা **partial success** design।

সেক্ষেত্রে পুরো import-কে একটি transaction-এ না রেখে batch-wise transaction করতে পারো:

```text
Batch 1 → COMMIT
Batch 2 → COMMIT
Batch 3 → ROLLBACK
Batch 4 → COMMIT
```

এটা business requirement-এর উপর নির্ভর করে।

---

# 38. Batch Transaction

```python
from django.db import transaction


for batch in batches:

    with transaction.atomic():

        Product.objects.bulk_create(
            batch,
            batch_size=1000
        )
```

এখানে প্রতিটি batch আলাদা transaction।

এটা huge import-এর ক্ষেত্রে useful হতে পারে।

---

# 39. Whole Import বনাম Batch Transaction

### Whole transaction

```text
10,000 records
      ↓
BEGIN
      ↓
all process
      ↓
one error
      ↓
ROLLBACK ALL
```

### Batch transaction

```text
1000 → COMMIT
1000 → COMMIT
1000 → COMMIT
1000 → ERROR → ROLLBACK
1000 → COMMIT
```

কোনটা ব্যবহার করবে সেটা business requirement-এর উপর নির্ভর করে।

---

# 40. Final Professional Example

একটা production-style simplified order service:

```python
from django.db import transaction


@transaction.atomic
def place_order(user, product_id, quantity):

    if quantity <= 0:
        raise ValueError(
            "Quantity must be positive"
        )

    product = (
        Product.objects
        .select_for_update()
        .get(id=product_id)
    )

    if product.stock < quantity:
        raise ValueError(
            "Insufficient stock"
        )

    total = (
        product.price *
        quantity
    )

    order = Order.objects.create(
        user=user,
        total_amount=total,
        status=Order.Status.PENDING
    )

    OrderItem.objects.create(
        order=order,
        product=product,
        quantity=quantity,
        unit_price=product.price,
        subtotal=total
    )

    product.stock -= quantity

    product.save(
        update_fields=["stock"]
    )

    payment = Payment.objects.create(
        order=order,
        amount=total,
        status=Payment.Status.PENDING
    )

    transaction.on_commit(
        lambda: process_payment.delay(
            payment.id
        )
    )

    return order
```

এখানে flow:

```text
                    place_order()
                         │
                         ▼
                 BEGIN TRANSACTION
                         │
                         ▼
                 Validate quantity
                         │
                         ▼
              select_for_update()
                         │
                         ▼
                  Check stock
                         │
                         ▼
                  Create Order
                         │
                         ▼
                Create OrderItem
                         │
                         ▼
                  Reduce Stock
                         │
                         ▼
                 Create Payment
                         │
                         ▼
                       COMMIT
                         │
                         ▼
                on_commit()
                         │
                         ▼
                  Celery Payment
```

এটা Django professional development-এর জন্য অনেক গুরুত্বপূর্ণ architecture pattern।

---

# 🧠 Class 124 — Final Cheat Sheet

### Basic transaction

```python
with transaction.atomic():
    ...
```

### Decorator

```python
@transaction.atomic
def create_order():
    ...
```

### Successful block

```text
COMMIT
```

### Exception

```text
ROLLBACK
```

### Bulk create + transaction

```python
with transaction.atomic():
    Product.objects.bulk_create(products)
```

### Bulk update + transaction

```python
with transaction.atomic():
    Product.objects.bulk_update(
        products,
        ["stock"]
    )
```

### Bulk delete + transaction

```python
with transaction.atomic():
    Product.objects.filter(...).delete()
```

### Concurrent inventory

```python
with transaction.atomic():

    product = Product.objects.select_for_update().get(
        id=product_id
    )

    product.stock -= quantity
    product.save(update_fields=["stock"])
```

### After successful commit

```python
transaction.on_commit(
    lambda: some_task.delay(...)
)
```

---

## ⭐ সবচেয়ে গুরুত্বপূর্ণ ৮টা rule

1. **Related multiple DB operations-এর consistency দরকার → `transaction.atomic()`**
    
2. **Failure হলে সব DB changes rollback করতে চাইলে → atomic block**
    
3. **একই value বহু row-তে → `update()`**
    
4. **প্রতিটি object-এর আলাদা value → `bulk_update()`**
    
5. **অনেক নতুন row → `bulk_create()`**
    
6. **Concurrent stock/seat/room booking → transaction + appropriate locking**
    
7. **External payment/API call-কে database transaction-এর অংশ মনে করবে না**
    
8. **Commit হওয়ার পর side effect চালাতে → `transaction.on_commit()`**
    

**পরের Class 125** হিসেবে সবচেয়ে logical topic হবে **Django ORM Concurrency & Race Conditions — `select_for_update()`, `F()` expressions, lost update, double booking, overselling এবং real Ecommerce/Hotel Booking implementation**।


----
