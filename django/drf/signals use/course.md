চলো **PART 1: Django Signal Fundamentals** একদম zero থেকে করি। এখানে আমরা শুধু Signal-এর basic foundation শিখব—`signals.py`, `@receiver`, `sender`, `instance`, `created` এবং Django কীভাবে Signal trigger করে।

---

# PART 1 — Django Signal Fundamentals

## 1. Signal কেন দরকার?

ধরো আমাদের e-commerce project-এ `Product` তৈরি করলে আমরা automatically একটা কাজ করতে চাই।

```text
Product Created
      ↓
Automatically
      ↓
Inventory তৈরি
```

DRF View-এর মধ্যে সরাসরি লিখতে পারি:

```python
product = serializer.save()

Inventory.objects.create(
    product=product
)
```

কিন্তু অন্য জায়গা থেকেও যদি Product তৈরি হয়?

```python
Product.objects.create(...)
```

তখন inventory তৈরি হবে না।

Signal ব্যবহার করলে:

```text
যেখান থেকেই Product তৈরি হোক
          ↓
Product save
          ↓
Signal trigger
          ↓
Inventory create
```

এটাই Signal-এর মূল শক্তি।

---

# 2. Signal-এর basic architecture

আমাদের flow:

```text
DRF API
   ↓
Serializer
   ↓
Product.objects.create()
   ↓
Django Model.save()
   ↓
Signal
   ↓
Receiver Function
```

এখানে:

**Signal** = event notification

**Receiver** = event ঘটলে যে function execute হবে।

সহজ ভাষায়:

> "এই ঘটনা ঘটলে এই function চালাও।"

---

# 3. Project structure

ধরো app-এর নাম `products`:

```text
products/
│
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── serializers.py
├── views.py
├── urls.py
└── signals.py        ← আমরা তৈরি করব
```

`signals.py` Django automatically তৈরি করে না। আমাদের তৈরি করতে হবে।

---

# 4. প্রথম Signal তৈরি

`signals.py`:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver
```

এখন:

```python
@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):
    print("Product signal triggered")
```

কিন্তু এখানে `Product` import করতে হবে:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product


@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):
    print("Product signal triggered")
```

এখন আমরা একে একে বুঝি।

---

# 5. `@receiver()` কী?

এই অংশটা:

```python
@receiver(post_save, sender=Product)
```

সবচেয়ে গুরুত্বপূর্ণ।

এটা Django-কে বলছে:

> `Product` model-এর `post_save` event ঘটলে `product_signal()` function-টি execute করো।

অর্থাৎ:

```text
Product save
    ↓
post_save
    ↓
product_signal()
```

---

# 6. `post_save` কী?

`post_save` হলো Django-এর built-in signal।

এর অর্থ:

> কোনো Model database-এ save হওয়ার পরে এই signal trigger হবে।

যেমন:

```python
product = Product.objects.create(
    name="Laptop",
    price=50000
)
```

Product save হওয়ার পরে:

```text
post_save
   ↓
product_signal()
```

চলবে।

---

# 7. `sender=Product` কী?

```python
sender=Product
```

মানে:

> কোন model-এর event আমি শুনতে চাই?

আমরা বলেছি:

```python
sender=Product
```

তাই শুধু `Product` save হলে signal trigger হবে।

ধরো:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
```

Category তৈরি করলে আমাদের Product signal trigger হবে না।

কারণ:

```python
sender=Product
```

দেওয়া হয়েছে।

---

# 8. `instance` কী?

এটা খুব গুরুত্বপূর্ণ।

```python
def product_signal(sender, instance, created, **kwargs):
```

`instance` হলো **যে object-এর উপর event ঘটেছে**।

ধরো:

```python
product = Product.objects.create(
    name="iPhone",
    price=100000
)
```

Signal-এর মধ্যে:

```python
instance
```

হবে ওই Product object।

তাই:

```python
instance.name
```

দিলে:

```text
iPhone
```

পাবে।

আর:

```python
instance.price
```

দিলে:

```text
100000
```

পাবে।

---

# 9. `created` কী?

`post_save`-এর সবচেয়ে useful argument হলো:

```python
created
```

এটা Boolean value।

### নতুন object হলে:

```python
created == True
```

### পুরোনো object update হলে:

```python
created == False
```

উদাহরণ:

```python
@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):

    if created:
        print("New product created")

    else:
        print("Existing product updated")
```

---

# 10. এখন পুরো flow দেখি

প্রথমে:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

Django internally save করবে।

তারপর:

```text
Product created
       ↓
post_save
       ↓
product_signal()
       ↓
sender = Product
instance = Laptop object
created = True
```

আর যদি:

```python
product.price = 55000
product.save()
```

তাহলে:

```text
Product updated
       ↓
post_save
       ↓
product_signal()
       ↓
sender = Product
instance = Laptop object
created = False
```

---

# 11. `**kwargs` কেন থাকে?

আমরা লিখি:

```python
def product_signal(sender, instance, created, **kwargs):
```

`kwargs`-এর মধ্যে Django signal-এর অতিরিক্ত information থাকতে পারে।

তুমি এখন সবগুলো মুখস্থ করার দরকার নেই।

শুধু মনে রাখো:

```python
sender
instance
created
**kwargs
```

এই চারটা `post_save`-এর ক্ষেত্রে খুব গুরুত্বপূর্ণ।

---

# 12. এখন Signal load করাতে হবে

শুধু `signals.py` বানালেই হবে না।

`apps.py`:

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "products"

    def ready(self):
        import products.signals
```

এই:

```python
def ready(self):
    import products.signals
```

অংশটা গুরুত্বপূর্ণ।

এর মানে:

> Django যখন `products` app load করবে, তখন `signals.py`-ও load করবে।

তখন Django জানবে:

```text
Product → post_save → product_signal
```

---

# 13. `ready()` কেন দরকার?

ধরো Django project start হলো।

```text
Django Start
    ↓
Products App Load
    ↓
apps.py
    ↓
ready()
    ↓
signals.py import
    ↓
Signal registered
```

এখন Product save হলে Django জানে কোন function চালাতে হবে।

---

# 14. পুরো basic implementation

### `models.py`

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

### `signals.py`

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product


@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):

    if created:
        print("New Product Created:", instance.name)

    else:
        print("Product Updated:", instance.name)
```

### `apps.py`

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "products"

    def ready(self):
        import products.signals
```

---

# 15. এখন test করি

Django shell:

```bash
python manage.py shell
```

তারপর:

```python
from products.models import Product
```

নতুন Product:

```python
product = Product.objects.create(
    name="Laptop",
    price=50000
)
```

Signal:

```text
New Product Created: Laptop
```

এখন update:

```python
product.price = 55000
product.save()
```

Signal:

```text
Product Updated: Laptop
```

কারণ:

```text
প্রথম save
    ↓
created = True

দ্বিতীয় save
    ↓
created = False
```

---

# 16. DRF-এর সাথে সম্পর্ক

তোমার DRF API:

```text
POST /api/products/
```

যখন:

```python
serializer.save()
```

হয়, তখন শেষ পর্যন্ত Django model save করে।

তখন:

```text
DRF
 ↓
Serializer
 ↓
Product.save()
 ↓
post_save
 ↓
product_signal()
```

অর্থাৎ DRF project-এ আলাদা করে Signal call করার প্রয়োজন নেই।

---

# 17. খুব গুরুত্বপূর্ণ distinction

Signal **API-এর সাথে tied না**।

ধরো Product তৈরি হলো:

### DRF দিয়ে

```python
serializer.save()
```

### Django shell দিয়ে

```python
Product.objects.create(...)
```

### Admin দিয়ে

```text
Django Admin
```

### অন্য service দিয়ে

```python
Product.objects.create(...)
```

যদি Product save হয়, তাহলে `post_save` signal trigger হতে পারে।

এটাই Signal-এর বড় সুবিধা।

---

# 18. আজকের Part 1-এর mental model

এই diagram-টা মনে রাখো:

```text
                 Product.save()
                      │
                      ▼
                 post_save
                      │
                      ▼
              ┌───────────────┐
              │   Receiver    │
              │product_signal │
              └───────────────┘
                      │
             ┌────────┴────────┐
             ▼                 ▼
        created=True      created=False
             │                 │
             ▼                 ▼
       New Product         Product Update
```

আর Signal-এর basic syntax:

```python
@receiver(SIGNAL, sender=MODEL)
def receiver_function(
    sender,
    instance,
    **kwargs
):
    # কাজ
```

`post_save` হলে:

```python
@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):
    ...
```

**Part 1-এর মূল ৫টা জিনিস:**

| বিষয়         | অর্থ                                     |
| ------------ | ---------------------------------------- |
| `signals.py` | Signal রাখার জায়গা                       |
| `@receiver`  | কোন signal-এর সাথে function connect করবে |
| `sender`     | কোন model event পাঠাবে                   |
| `instance`   | যে object-এর উপর event ঘটেছে             |
| `created`    | নতুন object নাকি existing object         |

পরের ধাপে **PART 2: `pre_save` বনাম `post_save`** করব, যেখানে একই `Product` দিয়ে দেখব **database save হওয়ার আগে ও পরে ঠিক কী পরিবর্তন হয় এবং কখন কোনটা ব্যবহার করবে।**

----
অবশ্যই। এবার **PART 2: `pre_save` বনাম `post_save`** এমনভাবে দেখব যাতে দুটির পার্থক্য আর confusion না থাকে। আমরা একই `Product` example ব্যবহার করব।

# PART 2 — `pre_save` বনাম `post_save`

মূল পার্থক্য এক লাইনে:

```text
pre_save  → Database-এ save হওয়ার আগে
post_save → Database-এ save হওয়ার পরে
```

Flow:

```text
product.save()
     │
     ▼
  pre_save
     │
     ▼
Database-এ save
     │
     ▼
  post_save
```

---

## 1. আমাদের Product Model

ধরি:

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

এখন আমরা `pre_save` এবং `post_save` দুটোই ব্যবহার করব।

---

# 2. `pre_save` কী?

`pre_save` database-এ object save হওয়ার **ঠিক আগে** trigger হয়।

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

from .models import Product


@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):
    print("PRE SAVE")
    print(instance.name)
    print(instance.price)
```

ধরো:

```python
product = Product(
    name="Laptop",
    price=50000
)

product.save()
```

Flow:

```text
Product object তৈরি
        ↓
product.save()
        ↓
pre_save
        ↓
Database INSERT
```

অর্থাৎ `pre_save` database operation-এর **আগে** চলে।

---

# 3. `post_save` কী?

`post_save` database-এ save হওয়ার **পরে** trigger হয়।

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product


@receiver(post_save, sender=Product)
def product_post_save(sender, instance, created, **kwargs):
    print("POST SAVE")
    print(instance.name)
    print(instance.price)
```

Flow:

```text
Product object
      ↓
product.save()
      ↓
Database INSERT/UPDATE
      ↓
post_save
```

---

# 4. দুটো একসাথে দেখো

`signals.py`:

```python
from django.db.models.signals import pre_save, post_save
from django.dispatch import receiver

from .models import Product


@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):
    print("1. PRE SAVE")
    print("Product:", instance.name)


@receiver(post_save, sender=Product)
def product_post_save(sender, instance, created, **kwargs):
    print("3. POST SAVE")
    print("Product:", instance.name)
```

যখন:

```python
product.save()
```

হবে:

```text
1. PRE SAVE
       ↓
2. Database INSERT/UPDATE
       ↓
3. POST SAVE
```

এটাই সবচেয়ে গুরুত্বপূর্ণ concept।

---

# 5. Real example — Product price automatically change

ধরো business requirement:

> Product-এর price save করার আগে যদি negative হয়, তাহলে সেটা 0 করে দিতে হবে।

এখানে `pre_save` ভালো।

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):

    if instance.price < 0:
        instance.price = 0
```

এখন:

```python
product = Product(
    name="Laptop",
    price=-500
)

product.save()
```

Flow:

```text
price = -500
     ↓
pre_save
     ↓
price = 0
     ↓
Database save
```

Database-এ যাবে:

```text
price = 0
```

### কেন `pre_save`?

কারণ আমরা database-এ যাওয়ার **আগেই value পরিবর্তন করতে চাই**।

---

# 6. আরেকটা example — SKU তৈরি

ধরো Product-এর SKU automatically তৈরি করতে চাই।

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
    sku = models.CharField(
        max_length=100,
        unique=True,
        blank=True
    )
```

`pre_save`:

```python
@receiver(pre_save, sender=Product)
def generate_product_sku(sender, instance, **kwargs):

    if not instance.sku:
        instance.sku = f"PROD-{instance.name.upper()}"
```

Product:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

Save হওয়ার আগে:

```text
name = Laptop
sku = ""
       ↓
pre_save
       ↓
sku = PROD-LAPTOP
       ↓
Database save
```

এখানে `pre_save` logical কারণ আমরা **database-এ save হওয়ার আগে object modify করছি**।

---

# 7. এবার `post_save`-এর real e-commerce example

ধরো Product তৈরি হলে automatically Inventory তৈরি করতে চাই।

```python
class Inventory(models.Model):
    product = models.OneToOneField(
        Product,
        on_delete=models.CASCADE
    )
    quantity = models.PositiveIntegerField(
        default=0
    )
```

Signal:

```python
@receiver(post_save, sender=Product)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

এখন:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

Flow:

```text
Product.objects.create()
        ↓
Product save
        ↓
Database-এ Product তৈরি
        ↓
post_save
        ↓
Inventory তৈরি
```

এখানে `post_save` ব্যবহার করা logical কারণ:

> Inventory তৈরি করার আগে Product database-এ successfully তৈরি হওয়া দরকার।

---

# 8. `created` এখানে কেন দরকার?

`post_save` **নতুন object তৈরি এবং existing object update—দুই ক্ষেত্রেই** trigger হয়।

ধরো:

```python
product = Product.objects.create(
    name="Laptop",
    price=50000
)
```

তখন:

```python
created == True
```

কিন্তু:

```python
product.price = 55000
product.save()
```

তখন:

```python
created == False
```

তাই:

```python
@receiver(post_save, sender=Product)
def create_inventory(sender, instance, created, **kwargs):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

শুধু নতুন Product-এর সময় Inventory তৈরি করবে।

---

# 9. একটা common mistake

অনেকে এমন করে:

```python
@receiver(post_save, sender=Product)
def create_inventory(sender, instance, created, **kwargs):

    Inventory.objects.create(
        product=instance
    )
```

এটা বিপজ্জনক।

কারণ Product update করলেও `post_save` চলবে।

```text
Product create
   ↓
Inventory create

Product update
   ↓
Inventory আবার create ❌

Product update
   ↓
Inventory আবার create ❌
```

যেহেতু Inventory-এর `OneToOneField`, error-ও হতে পারে।

তাই:

```python
if created:
```

খুব গুরুত্বপূর্ণ।

---

# 10. `pre_save`-এ `created` থাকে?

না।

এটা:

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):
```

এখানে সাধারণভাবে `created` পাওয়া যায় না।

কারণ `created` value database save operation **শেষ হওয়ার পরে** নির্ধারিত হয়।

`post_save`:

```python
def product_post_save(
    sender,
    instance,
    created,
    **kwargs
):
```

এখানে `created` থাকে।

---

# 11. Existing Product-এর ক্ষেত্রে পার্থক্য

ধরি database-এ:

```text
Product
id = 1
name = Laptop
price = 50000
```

আমরা করি:

```python
product.price = 60000
product.save()
```

তখন:

```text
pre_save
   ↓
Database UPDATE
   ↓
post_save
```

`post_save`-এ:

```python
created == False
```

অর্থাৎ:

```python
if created:
    # নতুন
else:
    # update
```

---

# 12. কখন `pre_save` ব্যবহার করবে?

যখন database-এ save হওয়ার **আগে object-এর data modify/prepare** করতে হবে।

Examples:

### Price normalize

```python
if instance.price < 0:
    instance.price = 0
```

### SKU generate

```python
if not instance.sku:
    instance.sku = generate_sku()
```

### Slug generate

```python
if not instance.slug:
    instance.slug = slugify(instance.name)
```

তবে slug/SKU-এর মতো গুরুত্বপূর্ণ business logic অনেক production project-এ model/service layer-এ রাখাও বেশি পরিষ্কার হতে পারে।

---

# 13. কখন `post_save` ব্যবহার করবে?

যখন object successfully save হওয়ার পরে **side effect** করতে হবে।

Examples:

```text
Product created
     ↓
Create Inventory
```

```text
User created
     ↓
Create Profile
```

```text
Order created
     ↓
Create OrderHistory
```

```text
Payment successful
     ↓
Create AuditLog
```

---

# 14. সবচেয়ে সহজ comparison

| বিষয়                 | `pre_save`    | `post_save`       |
| -------------------- | ------------- | ----------------- |
| কখন চলে?             | Save-এর আগে   | Save-এর পরে       |
| Database save হয়েছে? | ❌ না          | ✅ হ্যাঁ           |
| `created` পাওয়া যায়? | ❌             | ✅                 |
| Object modify করা    | ভালো use-case | সাধারণত দরকার নেই |
| Inventory create     | সাধারণত না    | ভালো use-case     |
| SKU/slug prepare     | হতে পারে      | দেরি হয়ে যায়      |
| Side-effect          | সাধারণত না    | ভালো use-case     |

---

# 15. একটা গুরুত্বপূর্ণ production warning

Signal মানেই সব business logic Signal-এ রাখতে হবে—এমন না।

যেমন e-commerce-এ:

```text
Order
 ↓
Payment
 ↓
Inventory
 ↓
Shipment
 ↓
Refund
```

এগুলো খুব গুরুত্বপূর্ণ state transition।

এসবকে blindly Signals-এর মধ্যে ছড়িয়ে দিলে পরে বোঝা কঠিন হতে পারে:

```text
Order save
   ↓
Signal A
   ↓
Payment
   ↓
Signal B
   ↓
Inventory
   ↓
Signal C
   ↓
Notification
```

তাই production architecture-এ সাধারণত:

```text
Signal
→ ছোট automatic side-effect

Service Layer
→ গুরুত্বপূর্ণ business workflow
```

ব্যবহার করা ভালো।

---

## Part 2-এর মূল কথা

শুধু এই দুইটা diagram মনে রাখো:

### `pre_save`

```text
Product
  ↓
pre_save
  ↓
Database
```

**"Save করার আগে কিছু করতে চাই"**

### `post_save`

```text
Product
  ↓
Database
  ↓
post_save
```

**"Save হওয়ার পরে কিছু করতে চাই"**

এখন Part 3-এ গেলে আমরা **`pre_delete` বনাম `post_delete`** দিয়ে Product delete করার সময় database-এর আগে/পরে কী ঘটে এবং e-commerce-এ **Product → Inventory → Evidence/File cleanup** কীভাবে handle করা হয় সেটা দেখব।

---
চলো **PART 3 — `pre_delete` বনাম `post_delete`** করি। এবারও আমাদের `Product` example ব্যবহার করব।

# PART 3 — `pre_delete` বনাম `post_delete`

আগের Part 2-তে ছিল:

```text
save()
  ↓
pre_save
  ↓
Database
  ↓
post_save
```

এবার delete:

```text
delete()
  ↓
pre_delete
  ↓
Database DELETE
  ↓
post_delete
```

মূল পার্থক্য:

> **`pre_delete` = object delete হওয়ার আগে**
> **`post_delete` = object delete হওয়ার পরে**

---

# 1. আমাদের Product Model

ধরি:

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

এখন আমরা Product delete করব।

```python
product.delete()
```

তখন Django internally:

```text
Product.delete()
      ↓
pre_delete
      ↓
Database থেকে DELETE
      ↓
post_delete
```

---

# 2. `pre_delete` কী?

`pre_delete` হলো object delete হওয়ার **আগে** trigger হওয়া signal।

```python
from django.db.models.signals import pre_delete
from django.dispatch import receiver

from .models import Product


@receiver(pre_delete, sender=Product)
def product_pre_delete(sender, instance, **kwargs):
    print("Product is about to be deleted")
    print("Product:", instance.name)
```

এখন:

```python
product.delete()
```

হলে:

```text
Product is about to be deleted
Product: Laptop
```

তারপর database থেকে Product delete হবে।

---

# 3. `post_delete` কী?

`post_delete` database থেকে object delete হওয়ার **পরে** trigger হয়।

```python
from django.db.models.signals import post_delete
from django.dispatch import receiver

from .models import Product


@receiver(post_delete, sender=Product)
def product_post_delete(sender, instance, **kwargs):
    print("Product has been deleted")
    print("Product:", instance.name)
```

Flow:

```text
product.delete()
       ↓
Database DELETE
       ↓
post_delete
       ↓
product_post_delete()
```

---

# 4. দুটো একসাথে

```python
@receiver(pre_delete, sender=Product)
def product_pre_delete(sender, instance, **kwargs):
    print("1. PRE DELETE")


@receiver(post_delete, sender=Product)
def product_post_delete(sender, instance, **kwargs):
    print("3. POST DELETE")
```

`product.delete()` করলে:

```text
1. PRE DELETE
       ↓
2. Database DELETE
       ↓
3. POST DELETE
```

এটাই সবচেয়ে গুরুত্বপূর্ণ।

---

# 5. `instance` এখানে কী?

`pre_delete` এবং `post_delete`-এও:

```python
instance
```

হলো যে object delete হচ্ছে।

ধরো:

```python
product = Product.objects.get(id=1)
```

তারপর:

```python
product.delete()
```

Signal-এর মধ্যে:

```python
instance.name
instance.price
instance.id
```

access করা যায়।

যেমন:

```python
@receiver(pre_delete, sender=Product)
def product_pre_delete(sender, instance, **kwargs):

    print("Deleting:", instance.name)
```

---

# 6. Real e-commerce example — Inventory

ধরি Product-এর সাথে Inventory আছে।

```python
class Inventory(models.Model):
    product = models.OneToOneField(
        Product,
        on_delete=models.CASCADE
    )

    quantity = models.PositiveIntegerField(
        default=0
    )
```

এখন Product delete করলে:

```python
product.delete()
```

`on_delete=models.CASCADE` থাকার কারণে Inventory-ও delete হয়ে যাবে।

Flow:

```text
Product DELETE
      ↓
Product pre_delete
      ↓
Product deleted
      ↓
Inventory CASCADE delete
      ↓
Product post_delete
```

তবে এখানে একটা important বিষয় আছে:

**সব cleanup-এর জন্য Signal দরকার হয় না।**

Django-এর `on_delete` behavior অনেক relationship cleanup নিজেই handle করতে পারে।

---

# 7. `pre_delete`-এর practical example

ধরো Product delete হওয়ার আগে আমরা audit log রাখতে চাই।

```python
class ProductDeleteLog(models.Model):
    product_name = models.CharField(max_length=200)
    product_price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
    deleted_at = models.DateTimeField(
        auto_now_add=True
    )
```

Signal:

```python
@receiver(pre_delete, sender=Product)
def product_pre_delete(sender, instance, **kwargs):

    ProductDeleteLog.objects.create(
        product_name=instance.name,
        product_price=instance.price
    )
```

Flow:

```text
Product.delete()
      ↓
pre_delete
      ↓
DeleteLog তৈরি
      ↓
Product DELETE
```

এখানে `pre_delete` useful কারণ delete হওয়ার **আগেই আমরা Product-এর তথ্য ব্যবহার করছি**।

---

# 8. `post_delete` কখন useful?

ধরো Product-এর সাথে কোনো external file cleanup করতে হবে।

উদাহরণ:

```text
Product
   ↓
image
   ↓
media/products/laptop.jpg
```

Product delete হওয়ার পরে image cleanup করতে চাই।

Conceptually:

```python
@receiver(post_delete, sender=Product)
def delete_product_image(sender, instance, **kwargs):

    if instance.image:
        instance.image.delete(save=False)
```

Flow:

```text
Product DELETE
      ↓
Database DELETE
      ↓
post_delete
      ↓
Image cleanup
```

এটা `post_delete`-এর একটি common use case।

---

# 9. কিন্তু এখানে একটা important warning ⚠️

`post_delete` মানে এই না যে পুরো transaction permanently committed হয়ে গেছে।

যদি:

```python
transaction.atomic()
```

এর মধ্যে কাজ হয়, transaction পরে rollback হতে পারে।

তাই **critical external side-effect** সরাসরি `post_delete`-এ করা সবসময় নিরাপদ নয়।

Production application-এ transaction এবং `transaction.on_commit()` বুঝে ব্যবহার করা দরকার।

এটা আমরা পরে advanced section-এ করব।

---

# 10. `pre_delete` বনাম `post_delete`

| বিষয়                       | `pre_delete`                   | `post_delete`          |
| -------------------------- | ------------------------------ | ---------------------- |
| কখন চলে?                   | Delete-এর আগে                  | Delete-এর পরে          |
| Database record তখন আছে?   | ✅                              | ❌                      |
| `instance` পাওয়া যায়?      | ✅                              | ✅                      |
| Delete-এর আগে data ব্যবহার | ভালো                           | Record DB-তে নেই       |
| Audit/logging              | ভালো use-case                  | পরিস্থিতিভেদে          |
| File cleanup               | হতে পারে                       | ভালো use-case          |
| Related cleanup            | অনেক ক্ষেত্রে `CASCADE` যথেষ্ট | Signal সবসময় দরকার নেই |

---

# 11. একটা common mistake

অনেকে ভাবে:

```python
@receiver(post_delete, sender=Product)
def delete_product(sender, instance, **kwargs):

    Product.objects.get(id=instance.id)
```

এটা কাজ করবে না।

কারণ:

```text
post_delete
```

চলার সময় Product database থেকে already delete হয়ে গেছে।

তাই:

```python
Product.objects.get(id=instance.id)
```

করলে `Product.DoesNotExist` হতে পারে।

তবে `instance` object-এর memory-তে থাকা field values এখনও access করা যায়:

```python
instance.name
instance.price
```

---

# 12. `QuerySet.delete()`-এর গুরুত্বপূর্ণ বিষয়

এটাও জানা দরকার।

তুমি যদি করো:

```python
product.delete()
```

তাহলে individual instance deletion হচ্ছে।

কিন্তু:

```python
Product.objects.filter(
    price__lt=100
).delete()
```

এটা **QuerySet bulk deletion**।

Django-এর deletion mechanism এখানে related objects ও delete signals handle করতে পারে, কিন্তু performance/behavior বোঝা জরুরি—বিশেষ করে বড় dataset-এ।

তাই production code-এ blindly ধরে নেবে না যে:

```python
Product.objects.filter(...).delete()
```

আর:

```python
for product in products:
    product.delete()
```

একই performance/behavior-এর।

---

# 13. E-commerce-এ কোথায় ব্যবহার করতে পারি?

### Example 1 — Product deletion audit

```text
Product delete
     ↓
pre_delete
     ↓
ProductDeleteLog
```

### Example 2 — Product image cleanup

```text
Product delete
     ↓
post_delete
     ↓
Image/File cleanup
```

### Example 3 — Seller deletion

```text
Seller delete
     ↓
pre_delete
     ↓
audit information
```

কিন্তু:

```text
Order delete
     ↓
Refund
```

এটা Signal-এ করা উচিত কিনা—এটা আলাদা architectural decision।

কারণ **Refund একটি critical business operation**, সাধারণত Service Layer বেশি উপযুক্ত।

---

# 14. Save আর Delete একসাথে মনে রাখো

এখন পর্যন্ত আমরা চারটা signal জানি:

```text
SAVE
────────────────────

pre_save
    ↓
Database Save
    ↓
post_save
```

```text
DELETE
────────────────────

pre_delete
    ↓
Database Delete
    ↓
post_delete
```

আর basic purpose:

```text
pre_save
→ save-এর আগে data prepare/modify

post_save
→ save-এর পরে side-effect

pre_delete
→ delete-এর আগে data/action

post_delete
→ delete-এর পরে cleanup/side-effect
```

---

# 15. খুব সহজ একটা মনে রাখার trick

`pre` = **আগে**

`post` = **পরে**

তাই:

```text
pre_save    → save করার আগে
post_save   → save করার পরে

pre_delete  → delete করার আগে
post_delete → delete করার পরে
```

---

## Part 3-এর ছোট practical challenge

আমাদের e-commerce-এ:

```python
class Product(models.Model):
    name = ...
    price = ...
```

Requirement:

> Product delete হওয়ার **আগে** তার `name` এবং `price` `ProductDeleteLog`-এ save করতে হবে।

এখানে তোমার signal হবে:

```python
@receiver(__________, sender=Product)
def product_delete_log(sender, instance, **kwargs):

    ProductDeleteLog.objects.create(
        product_name=instance.name,
        product_price=instance.price
    )
```

এখানে blank-এ **`pre_delete` নাকি `post_delete`** হবে—এটাই Part 3-এর মূল concept।

----
চলো **PART 4 — `m2m_changed`** করি। এটা একটু আলাদা, কারণ এখানে `save()` বা `delete()` নয়—**Many-to-Many relationship পরিবর্তন হলে** Signal trigger হয়।

# PART 4 — `m2m_changed`

## 1. আগে Many-to-Many বুঝি

E-commerce-এ একটা Product একাধিক Category-তে থাকতে পারে, আবার একটা Category-তে অনেক Product থাকতে পারে।

```text
Product A ─────┐
Product B ─────┼──→ Electronics
Product C ─────┘

Product A ─────┐
Product D ─────┼──→ Accessories
```

Django:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):
    name = models.CharField(max_length=200)

    categories = models.ManyToManyField(
        Category,
        related_name="products"
    )
```

এখানে:

```python
Product.categories
```

হলো Many-to-Many relationship।

---

# 2. Database-এ আসলে কী হয়?

Django automatically একটি intermediate/join table তৈরি করে।

Conceptually:

```text
Product
---------
id
name


Category
---------
id
name


Product_Category
----------------
product_id
category_id
```

ধরো:

```text
Product
1 → iPhone

Category
1 → Electronics
2 → Mobile
```

তাহলে intermediate table:

```text
product_id | category_id
-----------|------------
1          | 1
1          | 2
```

অর্থাৎ iPhone দুইটা category-তে আছে।

---

# 3. `m2m_changed` কেন দরকার?

ধরো তুমি করছো:

```python
product.categories.add(
    electronics
)
```

এখানে Product-এর field-এর normal `save()` হচ্ছে না।

বরং Many-to-Many relationship পরিবর্তন হচ্ছে।

তাই এখানে:

```text
post_save ❌
pre_save  ❌
m2m_changed ✅
```

ব্যবহার করা হয়।

---

# 4. Basic syntax

```python
from django.db.models.signals import m2m_changed
from django.dispatch import receiver

from .models import Product


@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def product_categories_changed(
    sender,
    instance,
    action,
    **kwargs
):
    print("M2M changed")
```

এখানে নতুন বিষয়:

```python
sender=Product.categories.through
```

---

# 5. `.through` কী?

এটা খুব গুরুত্বপূর্ণ।

Django Many-to-Many-এর জন্য যে intermediate table/model তৈরি করে, সেটাকে access করা যায়:

```python
Product.categories.through
```

তাই:

```python
sender=Product.categories.through
```

মানে:

> এই Many-to-Many relationship-এর intermediate table পরিবর্তন হলে signal trigger করো।

---

# 6. `action` কী?

`m2m_changed`-এর সবচেয়ে গুরুত্বপূর্ণ argument হলো:

```python
action
```

এটা বলে **কী ধরনের Many-to-Many operation হয়েছে**।

প্রধান action:

```text
pre_add
post_add

pre_remove
post_remove

pre_clear
post_clear
```

এগুলো তিনটা operation-এর সাথে সম্পর্কিত:

```text
ADD
REMOVE
CLEAR
```

---

# 7. `add()` — `pre_add` এবং `post_add`

ধরো:

```python
product.categories.add(electronics)
```

Flow:

```text
product.categories.add()
        ↓
pre_add
        ↓
Database relationship INSERT
        ↓
post_add
```

তাই:

```python
@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def product_categories_changed(
    sender,
    instance,
    action,
    **kwargs
):

    if action == "pre_add":
        print("Category will be added")

    elif action == "post_add":
        print("Category has been added")
```

---

# 8. `instance` এখানে কী?

আগের Signal-এর মতো এখানেও:

```python
instance
```

হলো মূল object।

যদি:

```python
product.categories.add(electronics)
```

হয়, তাহলে:

```python
instance
```

হবে:

```text
Product object
```

অর্থাৎ:

```python
instance.name
```

দিয়ে Product-এর নাম পাবে।

---

# 9. `pk_set` কী?

`m2m_changed`-এর আরেকটা খুব গুরুত্বপূর্ণ argument:

```python
pk_set
```

এখানে যে related objects add/remove হচ্ছে, তাদের primary key থাকে।

ধরো:

```python
electronics.id = 1
mobile.id = 2
```

তুমি:

```python
product.categories.add(
    electronics,
    mobile
)
```

করলে:

```python
pk_set
```

এর মধ্যে conceptually থাকবে:

```text
{1, 2}
```

অর্থাৎ:

```python
def product_categories_changed(
    sender,
    instance,
    action,
    pk_set,
    **kwargs
):
```

---

# 10. Complete example

```python
from django.db.models.signals import m2m_changed
from django.dispatch import receiver

from .models import Product


@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def product_categories_changed(
    sender,
    instance,
    action,
    pk_set,
    **kwargs
):

    if action == "pre_add":

        print(
            "Categories will be added:",
            pk_set
        )

    elif action == "post_add":

        print(
            "Categories added:",
            pk_set
        )
```

---

# 11. এখন বাস্তবে দেখি

ধরো:

```python
product = Product.objects.get(id=1)

electronics = Category.objects.get(id=1)
mobile = Category.objects.get(id=2)
```

তারপর:

```python
product.categories.add(
    electronics,
    mobile
)
```

Signal:

```text
pre_add
   ↓
{1, 2}
   ↓
Database relationship INSERT
   ↓
post_add
   ↓
{1, 2}
```

---

# 12. `remove()`

এখন:

```python
product.categories.remove(
    mobile
)
```

Flow:

```text
product.categories.remove()
        ↓
pre_remove
        ↓
Database relationship DELETE
        ↓
post_remove
```

Signal:

```python
if action == "pre_remove":
    print("Category will be removed")

elif action == "post_remove":
    print("Category removed")
```

---

# 13. `clear()`

যদি:

```python
product.categories.clear()
```

করো, তাহলে Product-এর **সব category relationship remove** হবে।

Flow:

```text
clear()
  ↓
pre_clear
  ↓
Database relationships removed
  ↓
post_clear
```

Signal:

```python
if action == "pre_clear":
    print("All categories will be removed")

elif action == "post_clear":
    print("All categories removed")
```

---

# 14. সব action একসাথে

```python
@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def product_categories_changed(
    sender,
    instance,
    action,
    pk_set,
    **kwargs
):

    if action == "pre_add":
        print("Before adding")

    elif action == "post_add":
        print("After adding")

    elif action == "pre_remove":
        print("Before removing")

    elif action == "post_remove":
        print("After removing")

    elif action == "pre_clear":
        print("Before clearing")

    elif action == "post_clear":
        print("After clearing")
```

এটাই `m2m_changed`-এর basic structure।

---

# 15. E-commerce real example

ধরো requirement:

> কোনো Product-এর category change হলে সেটা audit করতে চাই।

আমাদের:

```python
class CategoryChangeLog(models.Model):
    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE
    )

    action = models.CharField(
        max_length=50
    )
```

Signal:

```python
@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def category_change_log(
    sender,
    instance,
    action,
    pk_set,
    **kwargs
):

    if action in {
        "post_add",
        "post_remove",
        "post_clear"
    }:

        CategoryChangeLog.objects.create(
            product=instance,
            action=action
        )
```

এখন:

```python
product.categories.add(category)
```

হলে:

```text
Product
   ↓
Category added
   ↓
post_add
   ↓
CategoryChangeLog
```

---

# 16. `m2m_changed` কখন ব্যবহার করবে?

এটা ব্যবহার করবে যখন তোমার requirement specifically **Many-to-Many relationship change** নিয়ে।

উদাহরণ:

```text
Product
  ↕
Category
```

```text
Product
  ↕
Tag
```

```text
User
  ↕
Group
```

```text
Product
  ↕
Collection
```

যেমন:

```python
product.tags.add(tag)
```

বা:

```python
product.tags.remove(tag)
```

বা:

```python
product.tags.clear()
```

---

# 17. একটি গুরুত্বপূর্ণ বিষয়

এটা:

```python
product.categories.add(category)
```

করলে `Product.save()` হচ্ছে না।

তাই:

```python
post_save
```

এখানে কাজ করবে না।

এখানে:

```python
m2m_changed
```

ব্যবহার করতে হবে।

এই distinction-টা খুব গুরুত্বপূর্ণ।

---

# 18. `m2m_changed` বনাম `post_save`

| Situation       | Signal        |
| --------------- | ------------- |
| Product তৈরি    | `post_save`   |
| Product update  | `post_save`   |
| Product delete  | `post_delete` |
| Category add    | `m2m_changed` |
| Category remove | `m2m_changed` |
| Category clear  | `m2m_changed` |

---

# 19. আরেকটা important concept — `through`

যদি custom intermediate model ব্যবহার করো:

```python
class ProductCategory(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

তাহলে:

```python
class Product(models.Model):
    categories = models.ManyToManyField(
        Category,
        through="ProductCategory"
    )
```

এক্ষেত্রেও `m2m_changed` ব্যবহার করার সময় relationship-এর `through` model গুরুত্বপূর্ণ।

---

# 20. পুরো Signal map এখন

আমরা এখন পর্যন্ত শিখেছি:

```text
                 Django Signals
                       │
        ┌──────────────┼──────────────┐
        │              │              │
       SAVE          DELETE          M2M
        │              │              │
   ┌────┴────┐    ┌────┴────┐    m2m_changed
   │         │    │         │
pre_save post_save pre_delete post_delete
```

### Save

```text
pre_save
   ↓
Database Save
   ↓
post_save
```

### Delete

```text
pre_delete
   ↓
Database Delete
   ↓
post_delete
```

### Many-to-Many

```text
pre_add
   ↓
Database M2M change
   ↓
post_add
```

অথবা:

```text
pre_remove
   ↓
Database M2M change
   ↓
post_remove
```

অথবা:

```text
pre_clear
   ↓
Database M2M change
   ↓
post_clear
```

---

## Part 4-এর সবচেয়ে গুরুত্বপূর্ণ ৪টি জিনিস

```python
action
```

→ কী operation হচ্ছে?

```python
instance
```

→ কোন Product/parent object?

```python
pk_set
```

→ কোন related objects add/remove হচ্ছে?

```python
Product.categories.through
```

→ কোন Many-to-Many relationship-এর change observe করছি?

---

### একটি ছোট challenge

ধরো:

```python
product.categories.add(
    electronics,
    mobile
)
```

তুমি চাও **category relationship database-এ successfully add হওয়ার পরে** একটা log তৈরি হবে।

তাহলে কোনটা ব্যবহার করবে?

```text
A. pre_save
B. post_save
C. pre_add
D. post_add
E. post_delete
```

**সঠিক উত্তর: `D. post_add`** — কারণ এটা Many-to-Many relation add হওয়ার পরে trigger হয়।

----
চলো এবার **PART 5 — Custom Signal** করি। এই অংশটা গুরুত্বপূর্ণ, কারণ এখানে আমরা Django-এর built-in `post_save`/`m2m_changed` না নিয়ে **নিজের business event তৈরি** করব।

# PART 5 — Custom Signal

## 1. Custom Signal কী?

এতক্ষণ আমরা Django-এর built-in signal ব্যবহার করেছি:

```text
pre_save
post_save
pre_delete
post_delete
m2m_changed
```

এখন আমরা নিজের event বানাব।

যেমন e-commerce-এ:

```text
Payment successful
       ↓
Custom Signal
       ↓
Notification
       ↓
Email
       ↓
Audit Log
```

এখানে **"Payment successful"** Django-এর built-in model event নয়।

তাই আমরা নিজের signal বানাতে পারি।

---

# 2. কেন Custom Signal দরকার?

ধরো আমাদের Order:

```python
class Order(models.Model):
    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    total = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    is_paid = models.BooleanField(
        default=False
    )
```

এখন payment successful হওয়ার পর:

```text
Order
 ↓
Payment successful
 ↓
Send notification
 ↓
Create audit log
```

আমরা চাই না payment code-এর মধ্যে সবকিছু লিখি:

```python
order.is_paid = True
order.save()

send_email(...)
send_notification(...)
create_audit_log(...)
```

বরং একটা event তৈরি করতে পারি:

```text
order_paid
```

তারপর অন্য functions সেই event শুনবে।

---

# 3. Custom Signal তৈরি করা

ধরো app:

```text
orders/
├── models.py
├── views.py
├── serializers.py
├── signals.py
└── apps.py
```

`signals.py`:

```python
from django.dispatch import Signal

order_paid = Signal()
```

এই:

```python
order_paid = Signal()
```

হলো আমাদের custom signal।

---

# 4. Signal-এর নাম তুমি নিজের মতো দিতে পারো

যেমন:

```python
order_paid = Signal()
```

অথবা:

```python
order_cancelled = Signal()
```

অথবা:

```python
payment_failed = Signal()
```

অথবা:

```python
product_stock_low = Signal()
```

এগুলো Django-এর built-in signal নয়।

এগুলো **আমাদের application event**।

---

# 5. এখন Receiver বানাব

ধরো payment successful হলে notification তৈরি করতে চাই।

```python
from django.dispatch import receiver

from .signals import order_paid


@receiver(order_paid)
def handle_order_paid(sender, order, **kwargs):

    print(
        f"Order {order.id} has been paid"
    )
```

Flow:

```text
order_paid
    ↓
handle_order_paid()
```

---

# 6. কিন্তু signal কোথায় send করব?

এটাই সবচেয়ে গুরুত্বপূর্ণ অংশ।

ধরো payment service:

```python
def mark_order_as_paid(order):

    order.is_paid = True
    order.save()

    order_paid.send(
        sender=Order,
        order=order
    )
```

এখানে:

```python
order_paid.send(...)
```

মানে:

> "Order paid event ঘটেছে। যারা এই event-এর receiver, তাদের execute করো।"

---

# 7. পুরো Flow

```text
Payment successful
       ↓
mark_order_as_paid()
       ↓
order.is_paid = True
       ↓
order.save()
       ↓
order_paid.send()
       ↓
Receiver
       ↓
Notification
```

---

# 8. `sender` কী?

Custom signal-এ:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

এখানে:

```python
sender=Order
```

হলো event-এর sender।

Receiver:

```python
@receiver(order_paid)
def handle_order_paid(sender, order, **kwargs):
```

এখানে:

```python
sender
```

হবে:

```python
Order
```

---

# 9. `order=order` কী?

Custom Signal-এ আমরা নিজের প্রয়োজন অনুযায়ী data পাঠাতে পারি।

```python
order_paid.send(
    sender=Order,
    order=order
)
```

এখানে:

```python
order=order
```

receiver-এ পাওয়া যাবে:

```python
def handle_order_paid(sender, order, **kwargs):
```

তাই:

```python
order.id
order.user
order.total
```

ব্যবহার করতে পারব।

---

# 10. আরও data পাঠানো যায়

ধরো payment gateway থেকেও কিছু তথ্য এসেছে:

```python
order_paid.send(
    sender=Order,
    order=order,
    payment_id="PAY123",
    amount=5000
)
```

Receiver:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    payment_id,
    amount,
    **kwargs
):

    print(order.id)
    print(payment_id)
    print(amount)
```

এখানে custom signal অনেকটা event message-এর মতো কাজ করছে।

---

# 11. E-commerce Example — Notification

ধরো:

```python
class Notification(models.Model):
    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    message = models.TextField()
```

Custom signal:

```python
order_paid = Signal()
```

Receiver:

```python
@receiver(order_paid)
def create_payment_notification(
    sender,
    order,
    **kwargs
):

    Notification.objects.create(
        user=order.user,
        message=f"Order #{order.id} payment successful."
    )
```

এখন payment successful হলে:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

Automatically:

```text
Payment successful
       ↓
order_paid
       ↓
create_payment_notification()
       ↓
Notification তৈরি
```

---

# 12. একই Signal-এর একাধিক Receiver

এটা Custom Signal-এর বড় সুবিধা।

একটা event-এর জন্য অনেক receiver থাকতে পারে।

```text
                 order_paid
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
 Notification    AuditLog       Email
```

### Receiver 1

```python
@receiver(order_paid)
def create_notification(sender, order, **kwargs):

    Notification.objects.create(
        user=order.user,
        message="Payment successful"
    )
```

### Receiver 2

```python
@receiver(order_paid)
def create_audit_log(sender, order, **kwargs):

    AuditLog.objects.create(
        action="ORDER_PAID",
        object_id=order.id
    )
```

### Receiver 3

```python
@receiver(order_paid)
def send_payment_email(sender, order, **kwargs):

    print("Payment email sent")
```

একবার:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

করলেই তিনটা receiver trigger হবে।

---

# 13. `signals.py` কীভাবে organize করবে?

Small project:

```text
orders/
├── signals.py
└── apps.py
```

বড় project হলে:

```text
orders/
├── signals/
│   ├── __init__.py
│   ├── payment.py
│   ├── notification.py
│   └── audit.py
```

তখন:

```text
order_paid
    ↓
payment.py
notification.py
audit.py
```

এভাবে organize করা যায়।

---

# 14. Signal register করতে হবে

Built-in signal-এর মতো custom signal-এর receiver-ও Django load করার সময় register করতে হবে।

`apps.py`:

```python
from django.apps import AppConfig


class OrdersConfig(AppConfig):

    default_auto_field = "django.db.models.BigAutoField"

    name = "orders"

    def ready(self):
        import orders.signals
```

যদি `signals.py`-এর মধ্যে:

```python
@receiver(order_paid)
```

থাকে, তাহলে `ready()`-এর মাধ্যমে সেটা load হবে।

---

# 15. Custom Signal-এর complete example

### `signals.py`

```python
from django.dispatch import Signal, receiver

from .models import Order, Notification


order_paid = Signal()


@receiver(order_paid)
def create_payment_notification(
    sender,
    order,
    **kwargs
):

    Notification.objects.create(
        user=order.user,
        message=f"Order #{order.id} payment successful."
    )
```

### Payment service

```python
from .models import Order
from .signals import order_paid


def mark_order_as_paid(order):

    order.is_paid = True
    order.save(
        update_fields=["is_paid"]
    )

    order_paid.send(
        sender=Order,
        order=order
    )
```

Flow:

```text
mark_order_as_paid()
       ↓
Order.is_paid = True
       ↓
Order.save()
       ↓
order_paid.send()
       ↓
create_payment_notification()
       ↓
Notification
```

---

# 16. Built-in Signal বনাম Custom Signal

এখন দুটো compare করি।

| Built-in Signal               | Custom Signal                    |
| ----------------------------- | -------------------------------- |
| Django আগে থেকেই দেয়          | আমরা তৈরি করি                    |
| `post_save`                   | `order_paid`                     |
| `pre_delete`                  | `order_cancelled`                |
| `m2m_changed`                 | `payment_failed`                 |
| Model event-এর সাথে connected | Business event-এর সাথে connected |

সহজভাবে:

```text
Django event
    ↓
Built-in Signal
```

আর:

```text
Business event
    ↓
Custom Signal
```

---

# 17. Custom Signal কি Model-এর সাথে tied?

না।

এটাই এর গুরুত্বপূর্ণ পার্থক্য।

`post_save`:

```python
@receiver(post_save, sender=Order)
```

মানে Order-এর save event-এর সাথে directly connected।

কিন্তু:

```python
@receiver(order_paid)
```

মানে **Order paid event**-এর সাথে connected।

তাই:

```text
Order.save()
```

হলেও necessarily:

```text
order_paid
```

trigger হবে না।

শুধু যেখানে আমরা explicitly লিখব:

```python
order_paid.send(...)
```

সেখানেই event trigger হবে।

---

# 18. খুব গুরুত্বপূর্ণ — Custom Signal নিজে থেকে trigger হয় না

এটা ভুল:

```python
order_paid = Signal()
```

এটা শুধু signal তৈরি করে।

এখনও কিছু ঘটেনি।

Event trigger করতে হবে:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

তারপর receiver execute হবে।

অর্থাৎ:

```text
Signal define
     ↓
Receiver register
     ↓
Signal send
     ↓
Receiver execute
```

---

# 19. `send()` বনাম `send_robust()`

Django custom signal-এ সাধারণত:

```python
order_paid.send(...)
```

ব্যবহার করা হয়।

আর:

```python
order_paid.send_robust(...)
```

ব্যবহার করলে receiver-এর exception-গুলো আলাদাভাবে collect করা যায়।

Conceptually:

```text
send()
→ receiver exception হলে propagation হতে পারে

send_robust()
→ exception capture করে result-এ রাখে
```

Production architecture-এ কোনটা ব্যবহার করবে সেটা event-এর reliability requirement-এর উপর নির্ভর করে।

---

# 20. Custom Signal কোথায় ব্যবহার করা ভালো?

ভালো use case:

```text
order_paid
order_cancelled
payment_failed
user_registered
seller_approved
stock_became_low
```

যেখানে একটা **meaningful application event** আছে এবং একাধিক independent side-effect থাকতে পারে।

যেমন:

```text
seller_approved
      ↓
Notification
      ↓
Email
      ↓
AuditLog
```

---

# 21. কোথায় Custom Signal ব্যবহার না করাই ভালো?

ধরো:

```python
def calculate_order_total(order):
    ...
```

এটার জন্য Signal বানানোর দরকার নেই।

অথবা:

```python
def cancel_order(order):
    ...
```

যদি cancellation-এর মধ্যে:

```text
Order
Payment
Inventory
Refund
```

সব state change করতে হয়, তাহলে শুধু Custom Signal দিয়ে workflow লুকিয়ে ফেলা ঠিক না।

বরং:

```text
OrderCancellationService
        ↓
Validate
        ↓
Change Order State
        ↓
Release Inventory
        ↓
Create Refund
        ↓
Audit
```

এই ধরনের critical workflow **Service Layer**-এ explicit রাখা বেশি maintainable।

---

# 22. সবচেয়ে গুরুত্বপূর্ণ architecture rule

এটা মনে রাখো:

```text
Signal
    ↓
Event-driven side effect
```

আর:

```text
Service
    ↓
Core business workflow
```

উদাহরণ:

```text
Payment successful
        ↓
PaymentService
        ↓
Order PAID
        ↓
order_paid signal
        ├── Notification
        ├── AuditLog
        └── Email
```

এটা সুন্দর architecture হতে পারে।

কিন্তু:

```text
order_paid signal
        ↓
Change Order
        ↓
Refund
        ↓
Change Inventory
        ↓
Create Shipment
        ↓
Change Payment
```

এভাবে পুরো business workflow Signal-এর মধ্যে ছড়িয়ে দেওয়া উচিত নয়।

---

# Part 5 — Mental Model

Custom Signal-এর পুরো flow:

```text
                 BUSINESS EVENT
                       │
                       ▼
                order_paid.send()
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
    Notification    AuditLog      Email
     receiver       receiver      receiver
```

আর syntax:

```python
from django.dispatch import Signal

order_paid = Signal()
```

Receiver:

```python
@receiver(order_paid)
def handle_order_paid(sender, order, **kwargs):
    ...
```

Trigger:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

### এক লাইনে:

> **Built-in Signal বলে Django-এর কোনো event ঘটেছে; Custom Signal দিয়ে আমরা নিজের application-এর meaningful event ঘোষণা করি।**

পরের **PART 6**-এ আমরা সবচেয়ে গুরুত্বপূর্ণ জায়গায় যাব: **DRF Serializer + Signals** — যেমন `POST /products/` করলে `post_save` কীভাবে trigger হয়, serializer-এর `create()`/`update()` আর signal-এর মধ্যে পার্থক্য কী, এবং **কোন logic serializer-এ, কোনটা signal-এ, আর কোনটা service layer-এ রাখা উচিত**।

----
চলো **PART 6 — DRF Serializer + Django Signals** করি। এই অংশটা তোমার জন্য খুব গুরুত্বপূর্ণ, কারণ বাস্তব DRF project-এ সবচেয়ে বেশি confusion হয়:

> **Logic কি Serializer-এ রাখব, Signal-এ রাখব, নাকি Service Layer-এ?**

আমরা একটা বাস্তব **Product → Inventory** example দিয়ে শুরু করব।

---

# PART 6 — DRF Serializer + Signals

## 1. পুরো DRF flow আগে বুঝি

ধরো frontend থেকে request এলো:

```http
POST /api/products/
```

```json
{
    "name": "Laptop",
    "price": 50000
}
```

DRF-এর flow:

```text
Frontend
   ↓
ViewSet
   ↓
Serializer
   ↓
serializer.save()
   ↓
Product.objects.create()
   ↓
Product.save()
   ↓
pre_save
   ↓
Database INSERT
   ↓
post_save
   ↓
Signal receiver
```

এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ flow।

---

# 2. Product Model

আমাদের model:

```python
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

Inventory:

```python
class Inventory(models.Model):
    product = models.OneToOneField(
        Product,
        on_delete=models.CASCADE,
        related_name="inventory"
    )

    quantity = models.PositiveIntegerField(
        default=0
    )
```

Relationship:

```text
Product
   │
   │ OneToOne
   ▼
Inventory
```

---

# 3. DRF Serializer

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

এখন frontend:

```http
POST /api/products/
```

দিলে:

```json
{
    "name": "Laptop",
    "price": 50000
}
```

---

# 4. `serializer.save()` কী করে?

এটা খুব গুরুত্বপূর্ণ।

আমরা লিখি:

```python
serializer.is_valid(raise_exception=True)

product = serializer.save()
```

নতুন object হলে `ModelSerializer` internally roughly:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

করবে।

তারপর Django:

```text
Product.objects.create()
        ↓
Product.save()
        ↓
pre_save
        ↓
Database
        ↓
post_save
```

তাই **DRF Serializer-এর `save()`-এর মাধ্যমে Model save হলে Signal automatically trigger হয়।**

---

# 5. `post_save` দিয়ে Inventory তৈরি

`signals.py`:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product, Inventory


@receiver(post_save, sender=Product)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

এখন frontend থেকে:

```http
POST /api/products/
```

```json
{
    "name": "Laptop",
    "price": 50000
}
```

Flow:

```text
DRF
 ↓
ProductSerializer
 ↓
serializer.save()
 ↓
Product.objects.create()
 ↓
Product saved
 ↓
post_save
 ↓
create_inventory()
 ↓
Inventory created
```

Frontend-কে Inventory আলাদাভাবে পাঠাতে হলো না।

---

# 6. ViewSet

```python
from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer


class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

এখন:

```text
POST /products/
```

করলে পুরো কাজ automatic।

---

# 7. Database-এ কী হবে?

Frontend পাঠালো:

```json
{
    "name": "Laptop",
    "price": 50000
}
```

Database:

### Product

```text
id | name   | price
---|--------|------
1  | Laptop | 50000
```

### Inventory

```text
id | product_id | quantity
---|------------|---------
1  | 1          | 0
```

একটা API request থেকেই দুইটা record তৈরি হয়েছে।

---

# 8. এখানে Signal কেন ভালো?

কারণ Product creation-এর সাথে Inventory creation একটা **automatic side effect** হিসেবে কাজ করছে।

যেখান থেকেই Product তৈরি হোক:

```python
Product.objects.create(...)
```

বা:

```python
serializer.save()
```

বা:

```text
Django Admin
```

সব ক্ষেত্রেই:

```text
Product created
     ↓
post_save
     ↓
Inventory created
```

---

# 9. তাহলে Serializer-এর `create()` দিয়ে করলে?

তুমিও চাইলে:

```python
class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
        ]

    def create(self, validated_data):

        product = Product.objects.create(
            **validated_data
        )

        Inventory.objects.create(
            product=product
        )

        return product
```

এটাও কাজ করবে।

কিন্তু এখন প্রশ্ন:

> Signal ব্যবহার করব, নাকি Serializer `create()`?

---

# 10. Serializer `create()` কখন?

যদি logicটা **এই API-এর input-এর সাথে directly related** হয়, Serializer-এর `create()` useful হতে পারে।

উদাহরণ:

Frontend পাঠাচ্ছে:

```json
{
    "name": "Laptop",
    "price": 50000,
    "initial_quantity": 10
}
```

এখন `initial_quantity` model-এর Product field না।

Serializer:

```python
class ProductSerializer(serializers.ModelSerializer):

    initial_quantity = serializers.IntegerField(
        write_only=True
    )

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
            "initial_quantity",
        ]
```

এখানে API input থেকে Product + initial inventory তৈরি করা হচ্ছে।

এক্ষেত্রে Serializer `create()` meaningful হতে পারে।

---

# 11. Serializer `create()` example

```python
def create(self, validated_data):

    quantity = validated_data.pop(
        "initial_quantity"
    )

    product = Product.objects.create(
        **validated_data
    )

    Inventory.objects.create(
        product=product,
        quantity=quantity
    )

    return product
```

Flow:

```text
API Input
   ↓
Serializer validation
   ↓
create()
   ↓
Product
   ↓
Inventory
```

---

# 12. কিন্তু Signal কখন বেশি appropriate?

ধরো requirement:

> Product তৈরি হলেই inventory record অবশ্যই তৈরি হবে—API, Admin, Shell, অন্য service যেখান থেকেই Product তৈরি হোক।

তাহলে:

```text
Product created
      ↓
post_save
      ↓
Inventory
```

Signal ভালো candidate।

কারণ এটি API-specific না।

---

# 13. একটা গুরুত্বপূর্ণ সমস্যা

ধরো Product creation:

```python
product = Product.objects.create(...)
```

Signal:

```python
@receiver(post_save, sender=Product)
def create_inventory(...):
    Inventory.objects.create(...)
```

কিন্তু তুমি Serializer-এও:

```python
Inventory.objects.create(...)
```

লিখে ফেললে:

```text
Product create
    ↓
Serializer → Inventory create
    ↓
post_save → Inventory create
```

ফলে duplicate হতে পারে।

যেমন:

```text
UNIQUE constraint failed
```

কারণ `OneToOneField`।

তাই একই business logic **দুই জায়গায় রেখো না।**

---

# 14. Serializer `update()` এবং Signal

ধরো:

```http
PATCH /api/products/1/
```

```json
{
    "price": 55000
}
```

Serializer:

```python
serializer.save()
```

শেষে Product save হবে:

```text
PATCH
 ↓
Serializer.update()
 ↓
Product.save()
 ↓
pre_save
 ↓
Database UPDATE
 ↓
post_save
```

এখানে:

```python
created == False
```

তাই:

```python
if created:
```

থাকলে Product update-এর সময় Inventory create হবে না।

---

# 15. একটা useful example — price change audit

ধরো requirement:

> Product-এর price পরিবর্তন হলে audit log তৈরি করতে হবে।

এখানে শুধু `post_save` যথেষ্ট নয়, কারণ `post_save` জানাবে object save হয়েছে, কিন্তু **আগের price কত ছিল** সেটা সরাসরি দেয় না।

তখন approach হতে পারে:

```text
pre_save
   ↓
old price বের করা
   ↓
post_save
   ↓
new price compare
```

অথবা আরও পরিষ্কারভাবে Service Layer ব্যবহার করা যায়।

এটা advanced topic, পরে বিস্তারিত করব।

---

# 16. Signal + Serializer + Service — তিনটার পার্থক্য

এটাই সবচেয়ে গুরুত্বপূর্ণ অংশ।

### Serializer

```text
API input/output
Validation
Representation
```

উদাহরণ:

```python
initial_quantity
```

validate করা।

---

### Signal

```text
Automatic side-effect
```

উদাহরণ:

```text
Product created
    ↓
Create basic Inventory
```

---

### Service

```text
Core business workflow
```

উদাহরণ:

```text
Place Order
   ↓
Check Inventory
   ↓
Reserve Stock
   ↓
Create Order
   ↓
Payment
   ↓
Confirm Order
```

এগুলো Service Layer-এ রাখা ভালো।

---

# 17. একটা real e-commerce example

ধরো:

```text
POST /orders/
```

Request:

```json
{
    "items": [
        {
            "product_id": 1,
            "quantity": 2
        }
    ]
}
```

এখানে তুমি ভাবতে পারো:

### Serializer

```text
Validate product_id
Validate quantity
```

### Service

```text
Check stock
Lock inventory
Create Order
Create OrderItem
Reserve inventory
Calculate total
```

### Signal

```text
Order created
   ↓
Create OrderHistory
```

এটা architecture-wise পরিষ্কার।

---

# 18. Signal দিয়ে Order create করলে

```python
@receiver(post_save, sender=Order)
def create_order_history(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        OrderHistory.objects.create(
            order=instance,
            status=instance.status
        )
```

Service:

```python
def create_order(...):

    # complex business logic

    order = Order.objects.create(
        ...
    )

    return order
```

Order তৈরি হওয়ার পর:

```text
Order Service
      ↓
Order.objects.create()
      ↓
post_save
      ↓
OrderHistory
```

এটা reasonable।

---

# 19. Signal কি Serializer bypass করলেও চলবে?

হ্যাঁ।

ধরো:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

এখানে Serializer নেই।

তবুও:

```text
Product.save()
 ↓
post_save
```

হবে।

এটাই Signal-এর শক্তি।

---

# 20. কিন্তু একটা গুরুত্বপূর্ণ exception

সব database operation Signal trigger করবে—এমন ধরে নিও না।

বিশেষ করে:

```python
QuerySet.update()
```

এটা individual model `save()` call করে না।

যেমন:

```python
Product.objects.filter(
    category=category
).update(
    price=60000
)
```

এখানে সাধারণ `save()` signal flow-এর মতো `pre_save`/`post_save` পাওয়া যাবে না।

তাই:

```text
Model.save()
   ↓
pre_save/post_save
```

কিন্তু:

```text
QuerySet.update()
   ↓
Direct SQL UPDATE
   ↓
model save signals নয়
```

এটা production Django-তে খুব গুরুত্বপূর্ণ বিষয়।

---

# 21. Transaction-এর সাথে Signal

এখন একটা advanced issue:

```python
@receiver(post_save, sender=Order)
def something(...):
    ...
```

ধরো Order save হলো, Signal কাজ করল, কিন্তু পরে transaction rollback হলো।

তখন database state এবং side effect-এর মধ্যে mismatch হতে পারে।

যেমন:

```text
Transaction
   ↓
Order created
   ↓
post_save
   ↓
Email sent
   ↓
Later error
   ↓
ROLLBACK
```

তাহলে:

```text
Email → গেছে
Order → database-এ নেই
```

এটা undesirable।

এজন্য transaction-sensitive side effect-এর ক্ষেত্রে:

```python
transaction.on_commit(...)
```

গুরুত্বপূর্ণ।

এটা আমরা production-level অংশে বিস্তারিত করব।

---

# 22. আজকের সবচেয়ে গুরুত্বপূর্ণ rule

DRF project-এ এই mental model রাখো:

```text
               DRF
                │
                ▼
           Serializer
                │
         Validation / API
                │
                ▼
        Service Layer
                │
         Business Logic
                │
                ▼
             Model
                │
                ▼
            Signals
                │
         Side Effects
```

সব project-এ ঠিক এই order বাধ্যতামূলক নয়, কিন্তু responsibility আলাদা রাখার জন্য এটা ভালো mental model।

---

# 23. কখন কোনটা?

| Requirement                       | কোথায়?            |
| --------------------------------- | ----------------- |
| Request validation                | Serializer        |
| API input transformation          | Serializer        |
| Simple automatic side-effect      | Signal            |
| Product created → basic Inventory | Signal হতে পারে   |
| Order placement                   | Service           |
| Stock reservation                 | Service           |
| Payment workflow                  | Service           |
| Refund workflow                   | Service           |
| Notification after event          | Signal/async task |
| Audit log                         | Signal হতে পারে   |
| Complex state transition          | Service           |

---

# 24. Complete mini architecture

আমাদের e-commerce project:

```text
POST /products/
       ↓
ProductSerializer
       ↓
Validation
       ↓
serializer.save()
       ↓
Product.objects.create()
       ↓
pre_save
       ↓
Database INSERT
       ↓
post_save
       ↓
create_inventory()
       ↓
Inventory
```

আর Order:

```text
POST /orders/
       ↓
OrderSerializer
       ↓
Validation
       ↓
OrderService
       ↓
Check Stock
       ↓
Reserve Stock
       ↓
Create Order
       ↓
post_save
       ↓
OrderHistory
```

---

## PART 6-এর মূল কথা

**Serializer** বলে:

> "API থেকে কী data আসছে এবং সেটা valid কি না?"

**Service** বলে:

> "Business operation কীভাবে সম্পন্ন হবে?"

**Signal** বলে:

> "কোন event ঘটার পরে automatically আর কী side-effect হবে?"

সবচেয়ে গুরুত্বপূর্ণ distinction:

```text
Serializer ≠ Signal ≠ Service
```

এগুলো একে অপরের replacement না; প্রত্যেকটার আলাদা responsibility আছে।

পরের **PART 7**-এ আমরা **Signal + Service Layer** নিয়ে production architecture করব—বিশেষ করে `Order → Payment → Inventory → Notification` flow-এ কোন কাজ Signal-এ রাখা উচিত এবং কোনটা Service-এ রাখা উচিত।

---
# PART 7 — Signal + Service Layer: Production Architecture

এবার আমরা সবচেয়ে গুরুত্বপূর্ণ জায়গায় আসছি। বাস্তব **e-commerce / DRF project**-এ Signal কোথায় ব্যবহার করবে আর কোথায় **Service Layer** ব্যবহার করবে—এটা বুঝতে পারলে architecture অনেক পরিষ্কার হয়ে যাবে।

---

## 1. প্রথমে একটা real scenario দেখি

ধরো customer order করল:

```text
POST /api/orders/
```

তারপর business flow:

```text
Order Create
    ↓
Check Inventory
    ↓
Reserve Stock
    ↓
Calculate Total
    ↓
Create Payment
    ↓
Payment Successful
    ↓
Order = PAID
    ↓
Inventory Confirm
    ↓
Notification
    ↓
Order History
```

এখন প্রশ্ন:

> এগুলো কি সব Signal দিয়ে করব?

**না।**

এখানেই Service Layer-এর প্রয়োজন।

---

# 2. Core Rule

একটা খুব সহজ rule মনে রাখো:

```text
Signal = "Something happened"

Service = "Make something happen"
```

উদাহরণ:

### Signal

```text
Order paid
   ↓
Send notification
```

### Service

```text
Pay Order
   ↓
Validate payment
   ↓
Update order
   ↓
Update inventory
   ↓
Create payment record
```

---

# 3. কেন পুরো Order workflow Signal-এ রাখা উচিত নয়?

ধরো:

```python
@receiver(post_save, sender=Order)
def process_order(...):
    ...
```

তার ভিতরে:

```text
Check stock
Create order items
Reserve inventory
Create payment
Calculate price
Update status
Send email
```

সব ঢুকিয়ে দিলে সমস্যা হবে।

তখন architecture হবে:

```text
Order.save()
   ↓
Signal
   ↓
500 lines business logic 😵
```

এটা maintain করা কঠিন।

---

# 4. Service Layer কী?

Service Layer হলো business operation-এর জন্য আলাদা Python module/class/function।

Structure:

```text
orders/
│
├── models.py
├── serializers.py
├── views.py
├── signals.py
├── services.py
└── urls.py
```

`services.py`:

```python
def create_order(...):
    ...
```

অথবা বড় project হলে:

```text
orders/
└── services/
    ├── order_service.py
    ├── payment_service.py
    └── refund_service.py
```

---

# 5. একটা Order Model

ধরি:

```python
class Order(models.Model):

    STATUS_CHOICES = (
        ("PENDING", "Pending"),
        ("PAID", "Paid"),
        ("CANCELLED", "Cancelled"),
        ("SHIPPED", "Shipped"),
        ("DELIVERED", "Delivered"),
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="PENDING"
    )

    total = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )
```

---

# 6. Inventory Model

```python
class Inventory(models.Model):

    product = models.OneToOneField(
        Product,
        on_delete=models.CASCADE
    )

    quantity = models.PositiveIntegerField(
        default=0
    )

    reserved_quantity = models.PositiveIntegerField(
        default=0
    )
```

এখানে:

```text
quantity = actual stock
reserved_quantity = reserved stock
```

---

# 7. Order creation Service

`services.py`:

```python
from django.db import transaction

from .models import Order


@transaction.atomic
def create_order(user, items):

    # 1. validate items

    # 2. check inventory

    # 3. reserve inventory

    # 4. calculate total

    # 5. create order

    order = Order.objects.create(
        user=user,
        total=total,
        status="PENDING"
    )

    # 6. create OrderItems

    return order
```

এখানে core business logic Service-এর মধ্যে।

---

# 8. View কী করবে?

View-এর কাজ খুব simple:

```python
class OrderViewSet(ModelViewSet):

    def create(self, request, *args, **kwargs):

        serializer = OrderSerializer(
            data=request.data
        )

        serializer.is_valid(
            raise_exception=True
        )

        order = create_order(
            user=request.user,
            items=serializer.validated_data["items"]
        )

        return Response(
            OrderSerializer(order).data
        )
```

Flow:

```text
View
 ↓
Serializer
 ↓
Service
 ↓
Models
```

এটা অনেক clean।

---

# 9. তাহলে Signal কোথায়?

ধরো Order create হওয়ার পরে আমরা history রাখতে চাই।

Model:

```python
class OrderHistory(models.Model):

    order = models.ForeignKey(
        Order,
        on_delete=models.CASCADE
    )

    status = models.CharField(
        max_length=20
    )
```

Signal:

```python
@receiver(
    post_save,
    sender=Order
)
def create_order_history(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        OrderHistory.objects.create(
            order=instance,
            status=instance.status
        )
```

এখানে Signal reasonable।

কারণ:

```text
Order created
      ↓
Automatically record history
```

---

# 10. Payment-এর ক্ষেত্রে কী হবে?

ধরো payment successful হয়েছে।

আমাদের Service:

```python
@transaction.atomic
def mark_order_paid(order, payment):

    # validate payment

    payment.status = "SUCCESS"
    payment.save()

    order.status = "PAID"
    order.save()

    # inventory confirmation
```

এটা **Service**।

কারণ এটা core business workflow।

---

# 11. তারপর Signal?

Order status `PAID` হওয়ার পরে:

```text
Order PAID
   ↓
Notify customer
```

এখানে custom signal ব্যবহার করা যায়।

`signals.py`:

```python
from django.dispatch import Signal


order_paid = Signal()
```

তারপর Service:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

Receiver:

```python
@receiver(order_paid)
def send_payment_notification(
    sender,
    order,
    **kwargs
):

    print(
        f"Order {order.id} is paid"
    )
```

---

# 12. পুরো architecture

এখন flow দেখো:

```text
Payment Gateway
      ↓
PaymentService
      ↓
Validate Payment
      ↓
Update Payment
      ↓
Update Order → PAID
      ↓
Update Inventory
      ↓
order_paid.send()
      ↓
      ├── Notification
      ├── Audit Log
      ├── Email
      └── Analytics
```

এটাই Signal + Service-এর সুন্দর ব্যবহার।

---

# 13. Signal-এর সবচেয়ে বড় সুবিধা

ধরো:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

একই event-এর জন্য multiple receiver থাকতে পারে।

```text
                 order_paid
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
 Notification     AuditLog      Analytics
```

Service-এর code:

```python
order_paid.send(...)
```

এইটুকুই জানে।

Service-কে জানতে হচ্ছে না:

```text
Notification কীভাবে হবে?
Audit কীভাবে হবে?
Analytics কীভাবে হবে?
```

এটাই decoupling।

---

# 14. কিন্তু একটা গুরুত্বপূর্ণ সমস্যা

ধরো:

```python
order_paid.send(...)
```

receiver:

```python
send_email()
```

Email পাঠাতে গেল।

কিন্তু email server unavailable।

তাহলে কী হবে?

Signal receiver exception দিলে main flow-এ সমস্যা হতে পারে।

এজন্য production system-এ notification/email-এর মতো কাজের জন্য সাধারণত:

```text
Signal
  ↓
Celery Task
  ↓
Email
```

ব্যবহার করা হয়।

যেমন:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )
```

এখানে Celery background worker email পাঠাবে।

---

# 15. Transaction-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়

এখন ধরো:

```python
@transaction.atomic
def mark_order_paid(order):

    order.status = "PAID"
    order.save()

    order_paid.send(
        sender=Order,
        order=order
    )

    raise Exception("Something failed")
```

তাহলে:

```text
Order = PAID
      ↓
Signal triggered
      ↓
Email/Task
      ↓
Exception
      ↓
ROLLBACK
```

সমস্যা হতে পারে:

```text
Database → Order PAID হয়নি
Email → PAID বলে চলে গেছে
```

তাই transaction-এর পরে external side effect trigger করার সময়:

```python
transaction.on_commit(...)
```

খুব গুরুত্বপূর্ণ।

---

# 16. `on_commit()` example

```python
from django.db import transaction


@transaction.atomic
def mark_order_paid(order):

    order.status = "PAID"
    order.save()

    transaction.on_commit(
        lambda: order_paid.send(
            sender=Order,
            order=order
        )
    )
```

এখন:

```text
Transaction
    ↓
Order update
    ↓
Everything successful?
    │
    ├── NO → Rollback
    │
    └── YES
         ↓
     COMMIT
         ↓
     order_paid
```

এটা production-এ অনেক বেশি নিরাপদ pattern।

---

# 17. আরও ভালো pattern

একটা সাধারণ architecture:

```text
Service
   │
   ├── Database business logic
   │
   └── transaction.on_commit()
               ↓
          Domain Event
               ↓
             Signal
               ↓
          Celery Task
               ↓
      Email / Notification
```

উদাহরণ:

```python
transaction.on_commit(
    lambda: order_paid.send(
        sender=Order,
        order=order
    )
)
```

Signal:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_notification.delay(
        order.id
    )
```

---

# 18. `post_save` বনাম Custom Signal

এখানেও distinction বুঝে রাখো।

### `post_save`

Model event:

```text
Order.save()
    ↓
post_save
```

### Custom Signal

Business event:

```text
Payment successful
    ↓
order_paid
```

অর্থাৎ:

```text
post_save
    =
"Database model saved"

custom signal
    =
"Business event happened"
```

---

# 19. Order status change-এর জন্য কি `post_save` ব্যবহার করব?

ধরো:

```text
PENDING → PAID
```

তুমি চাইলে `post_save` দিয়ে detect করতে পারো।

কিন্তু বড় system-এ এটা risky হতে পারে।

কারণ:

```python
order.status = "PAID"
order.save()
```

এটা কে করেছে?

```text
PaymentService?
Admin?
Management command?
Another API?
```

Signal শুধু জানে:

```text
Order saved
```

Business context জানে না।

তাই payment confirmation-এর মতো গুরুত্বপূর্ণ event-এর জন্য explicit service/domain event অনেক পরিষ্কার।

---

# 20. Production rule

এই ruleটা মনে রাখো:

### ❌ ভুল approach

```text
post_save(Order)
    ↓
Payment
    ↓
Inventory
    ↓
Refund
    ↓
Email
    ↓
Notification
    ↓
Shipping
```

সব Signal-এর মধ্যে।

---

### ✅ ভালো approach

```text
OrderService
    ↓
Create Order
    ↓
InventoryService
    ↓
PaymentService
    ↓
Order PAID
    ↓
Domain Event
    ↓
Signal
    ├── Notification
    ├── Audit
    └── Async Tasks
```

---

# 21. Responsibility table

| কাজ                    | কোথায় রাখবে   |
| ---------------------- | ------------- |
| Request validation     | Serializer    |
| Input transformation   | Serializer    |
| Create order workflow  | Service       |
| Check inventory        | Service       |
| Reserve inventory      | Service       |
| Payment processing     | Service       |
| Refund                 | Service       |
| Order state transition | Service       |
| Simple automatic audit | Signal        |
| Order created history  | Signal        |
| `order_paid` event     | Custom Signal |
| Email                  | Celery Task   |
| Push notification      | Celery Task   |
| Analytics event        | Signal → Task |

---

# 22. একটা সহজ mental model

তিনটা প্রশ্ন নিজেকে করবে:

### Question 1

> **User/API থেকে data আসছে?**

তাহলে:

```text
Serializer
```

### Question 2

> **Business decision নিতে হবে?**

যেমন:

```text
Stock আছে?
Payment valid?
Refund allowed?
Order cancel করা যাবে?
```

তাহলে:

```text
Service
```

### Question 3

> **কোনো event ঘটে যাওয়ার পরে automatically side-effect করতে হবে?**

যেমন:

```text
Order created
Payment completed
User registered
```

তাহলে:

```text
Signal / Event
```

---

# 23. আজকের পুরো architecture একসাথে

```text
                 HTTP Request
                      │
                      ▼
                    View
                      │
                      ▼
                 Serializer
                      │
                 Validation
                      │
                      ▼
                 Service Layer
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       Order       Inventory    Payment
          │           │           │
          └───────────┼───────────┘
                      │
                 Transaction
                      │
                    COMMIT
                      │
                      ▼
                Domain Event
                      │
                      ▼
                    Signal
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
       Audit       Celery       Analytics
                     │
                     ▼
               Notification
```

এটাই তুমি production-grade Django/DRF architecture শেখার সময় মাথায় রাখবে।

**PART 7-এর সবচেয়ে গুরুত্বপূর্ণ লাইন:**

> **Service business operation চালায়, Signal event-এর পরে side-effect trigger করে।**

পরের **PART 8**-এ আমরা আরও গুরুত্বপূর্ণ একটা বিষয় করব: **`transaction.atomic()` + Signal + `transaction.on_commit()`** — কেন signal transaction-এর মাঝখানে চালানো বিপজ্জনক হতে পারে, এবং production e-commerce-এ ঠিক কীভাবে implement করবে।

---
# PART 8 — `transaction.atomic()` + Signal + `transaction.on_commit()`

এটা Django Signals-এর **production-level** অংশ। এখানে আমরা বুঝব:

> **Database transaction সফল হওয়ার আগে Signal চালালে কী সমস্যা হতে পারে?**
> আর `transaction.on_commit()` কীভাবে সেই সমস্যা সমাধান করে?

বিশেষ করে **Order + Payment + Inventory** example দিয়ে দেখব।

---

# 1. প্রথমে Transaction বুঝি

ধরো customer order দিল:

```text
Order Create
     ↓
Inventory Reserve
     ↓
Payment Create
     ↓
Order = PAID
```

এই কাজগুলোর মধ্যে কোনো একটা fail করলে আমরা চাই:

```text
সব সফল → COMMIT
কোনো একটা fail → ROLLBACK
```

এটাই transaction-এর basic concept।

---

# 2. `transaction.atomic()`

Django:

```python
from django.db import transaction
```

তারপর:

```python
with transaction.atomic():

    order = Order.objects.create(
        user=user,
        status="PENDING"
    )

    payment = Payment.objects.create(
        order=order,
        amount=5000
    )
```

এর অর্থ:

```text
atomic block শুরু
      ↓
Order create
      ↓
Payment create
      ↓
সব সফল?
   ↓       ↓
 YES      NO
  ↓        ↓
COMMIT   ROLLBACK
```

---

# 3. Rollback example

```python
from django.db import transaction


def create_order():

    with transaction.atomic():

        order = Order.objects.create(
            status="PENDING"
        )

        payment = Payment.objects.create(
            order=order
        )

        raise Exception("Something went wrong")
```

শেষে:

```text
Order → rollback
Payment → rollback
```

Database-এ কোনোটাই থাকবে না।

---

# 4. এবার Signal-এর সমস্যা দেখি

ধরো:

```python
@receiver(post_save, sender=Order)
def order_created(sender, instance, created, **kwargs):

    if created:
        send_order_email(instance)
```

এখন:

```python
with transaction.atomic():

    order = Order.objects.create(
        status="PENDING"
    )

    # আরও business logic

    raise Exception("Payment failed")
```

Flow:

```text
transaction শুরু
      ↓
Order INSERT
      ↓
post_save
      ↓
Email sent
      ↓
Payment failed
      ↓
ROLLBACK
```

এখন সমস্যা:

```text
Database:
Order নেই ❌

Email:
"Your order was created" ✅
```

Customer এমন একটা email পেল যে order আসলে database-এ নেই।

---

# 5. কেন এমন হলো?

কারণ:

```text
post_save
```

মানে:

> Model database save operation সম্পন্ন করেছে।

এটা **transaction পুরোপুরি committed হয়েছে**—এমন নয়।

অর্থাৎ:

```text
post_save ≠ transaction committed
```

এটা খুব গুরুত্বপূর্ণ।

---

# 6. `transaction.on_commit()`

Django আমাদের দেয়:

```python
transaction.on_commit()
```

এর অর্থ:

> Transaction সফলভাবে commit হওয়ার পর এই function চালাও।

Example:

```python
from django.db import transaction


transaction.on_commit(
    lambda: send_order_email(order)
)
```

এখন flow:

```text
transaction
    ↓
Order save
    ↓
Register on_commit callback
    ↓
More operations
    ↓
COMMIT
    ↓
send_order_email()
```

যদি rollback হয়:

```text
ROLLBACK
    ↓
send_order_email()
```

**চলবে না।**

---

# 7. Basic example

```python
from django.db import transaction


with transaction.atomic():

    order = Order.objects.create(
        status="PENDING"
    )

    transaction.on_commit(
        lambda: print(
            f"Order {order.id} committed"
        )
    )
```

যদি transaction সফল হয়:

```text
Order created
   ↓
COMMIT
   ↓
print()
```

---

# 8. Rollback হলে?

```python
with transaction.atomic():

    order = Order.objects.create(
        status="PENDING"
    )

    transaction.on_commit(
        lambda: print("Order committed")
    )

    raise Exception("Failed")
```

Flow:

```text
Order INSERT
    ↓
on_commit registered
    ↓
Exception
    ↓
ROLLBACK
    ↓
callback execute হবে না
```

---

# 9. এবার Signal-এর সাথে ব্যবহার করি

আমাদের custom signal:

```python
from django.dispatch import Signal


order_created = Signal()
```

Service:

```python
from django.db import transaction


@transaction.atomic
def create_order(user):

    order = Order.objects.create(
        user=user,
        status="PENDING"
    )

    transaction.on_commit(
        lambda: order_created.send(
            sender=Order,
            order=order
        )
    )

    return order
```

Flow:

```text
create_order()
      ↓
atomic transaction
      ↓
Order created
      ↓
on_commit registered
      ↓
COMMIT
      ↓
order_created signal
```

---

# 10. Signal Receiver

```python
@receiver(order_created)
def handle_order_created(
    sender,
    order,
    **kwargs
):

    print(
        f"Order {order.id} created"
    )
```

এখন receiver transaction সফল হওয়ার পরে execute হবে।

---

# 11. Email-এর ক্ষেত্রে আরও ভালো pattern

Email সরাসরি Signal-এর মধ্যে পাঠানো ভালো না।

এভাবে:

```python
@receiver(order_created)
def handle_order_created(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )
```

এখানে:

```text
Signal
   ↓
Celery
   ↓
Email
```

---

# 12. Complete production flow

এখন পুরো flow:

```text
                    API
                     ↓
                  View
                     ↓
                Serializer
                     ↓
               OrderService
                     ↓
             transaction.atomic
                     ↓
          ┌──────────┼──────────┐
          ↓          ↓          ↓
        Order    Inventory    Payment
          │          │          │
          └──────────┼──────────┘
                     ↓
                  COMMIT
                     ↓
               on_commit()
                     ↓
              order_created
                  Signal
                     ↓
                Celery Task
                     ↓
                Notification
```

এটা production architecture-এর খুব useful pattern।

---

# 13. `post_save` কি তাহলে ব্যবহার করব না?

অবশ্যই করবে।

`post_save` এখনও useful।

যেমন:

```python
@receiver(post_save, sender=Product)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

এখানে Inventory creation database-side related operation।

কিন্তু যদি কাজটা হয়:

```text
Email
SMS
Push notification
Webhook
External API
Celery
```

তাহলে transaction boundary সম্পর্কে সচেতন হওয়া দরকার।

---

# 14. `post_save` + `on_commit`

তুমি চাইলে:

```python
@receiver(post_save, sender=Order)
def order_saved(
    sender,
    instance,
    created,
    **kwargs
):

    if created:

        transaction.on_commit(
            lambda: send_order_email.delay(
                instance.id
            )
        )
```

Flow:

```text
Order.save()
   ↓
post_save
   ↓
on_commit register
   ↓
Transaction commit
   ↓
Celery task
```

এটা আগের direct email-এর চেয়ে safer।

---

# 15. কিন্তু একটা subtle issue আছে

ধরো:

```python
@receiver(post_save, sender=Order)
def order_saved(...):

    transaction.on_commit(
        lambda: send_order_email.delay(
            instance.id
        )
    )
```

এখন Order যদি অনেকবার update হয়:

```python
order.save()
order.save()
order.save()
```

তাহলে callback একাধিকবার register হতে পারে।

ফলে:

```text
Email
Email
Email
```

হতে পারে।

তাই `post_save`-এ blindly external task trigger করা ঠিক না।

---

# 16. `created` check

যদি শুধু Order creation-এর সময় email দরকার:

```python
@receiver(post_save, sender=Order)
def order_saved(
    sender,
    instance,
    created,
    **kwargs
):

    if not created:
        return

    transaction.on_commit(
        lambda: send_order_email.delay(
            instance.id
        )
    )
```

এতে update-এর সময় email যাবে না।

---

# 17. কিন্তু Payment-এর ক্ষেত্রে?

ধরো:

```text
PENDING
   ↓
PAID
```

এখানে `created` যথেষ্ট নয়।

কারণ Payment status পরে পরিবর্তিত হচ্ছে।

তাই production system-এ explicit service/event ভালো:

```python
def mark_payment_success(payment):

    with transaction.atomic():

        payment.status = "SUCCESS"
        payment.save()

        order = payment.order

        order.status = "PAID"
        order.save()

        transaction.on_commit(
            lambda: order_paid.send(
                sender=Order,
                order=order
            )
        )
```

---

# 18. কেন এটা ভালো?

কারণ এখানে business intent পরিষ্কার:

```text
Payment successful
      ↓
Order PAID
      ↓
Commit successful
      ↓
order_paid event
```

Signal-এর ভিতরে guess করতে হচ্ছে না:

```text
"Order-এর status PAID হয়েছে কেন?"
```

Service নিজেই জানে।

---

# 19. `post_save` দিয়ে status change detect করা কেন risky?

ধরো:

```python
@receiver(post_save, sender=Order)
def detect_paid(...):

    if instance.status == "PAID":
        ...
```

এখন Order যদি already PAID থাকে:

```python
order.save()
```

তবুও:

```text
status == PAID
```

সত্য।

তাহলে signal আবার notification পাঠাতে পারে।

```text
PAID
 ↓
save
 ↓
email

PAID
 ↓
save
 ↓
email

PAID
 ↓
save
 ↓
email
```

তাই business event-কে explicit করা অনেক ভালো:

```python
order_paid.send(...)
```

---

# 20. Idempotency-এর সাথে সম্পর্ক

Production payment system-এ আরেকটা গুরুত্বপূর্ণ concept হলো:

> **একই event দুইবার এলে কী হবে?**

ধরো gateway callback দুইবার এলো:

```text
Payment SUCCESS
Payment SUCCESS
```

তাহলে:

```text
Order PAID
Order PAID
```

হয়ে গেলে সমস্যা হতে পারে।

তাই PaymentService-এ:

```python
if payment.status == "SUCCESS":
    return payment
```

এর মতো protection থাকতে পারে।

আর notification/task-এর ক্ষেত্রেও duplicate prevention দরকার হতে পারে।

---

# 21. Inventory example

ধরো stock:

```text
quantity = 10
reserved = 0
```

Customer 2টা order করল।

Service:

```text
quantity = 10
reserved = 2
```

তারপর payment successful।

```text
reserved = 0
quantity = 8
```

এই ধরনের inventory state transition:

**Signal-এর মধ্যে রাখবে না।**

এটা:

```text
InventoryService
```

এর দায়িত্ব হওয়া উচিত।

---

# 22. Golden Rule

Production e-commerce-এ:

### Business state change

```text
Service
```

### Database model event

```text
Signal
```

### Transaction সফল হওয়ার পর external event

```text
on_commit()
```

### Heavy/slow external work

```text
Celery
```

---

# 23. সবগুলো একসাথে

```text
                Order API
                    ↓
               Serializer
                    ↓
              OrderService
                    ↓
           transaction.atomic()
                    ↓
       ┌────────────┼────────────┐
       ↓            ↓            ↓
     Order       Inventory     Payment
       │            │            │
       └────────────┼────────────┘
                    ↓
                 COMMIT
                    ↓
             transaction.on_commit
                    ↓
              order_paid event
                    ↓
                 Signal
                    ↓
                Celery
             ┌──────┼──────┐
             ↓      ↓      ↓
           Email   Push   Audit
```

---

# 24. সবচেয়ে গুরুত্বপূর্ণ ৫টা কথা

### 1.

```text
post_save
```

মানে:

> Model save হয়েছে।

এটা মানেই transaction commit হয়েছে না।

### 2.

```text
transaction.atomic()
```

ব্যবহার করে related database operations এক transaction-এর মধ্যে রাখো।

### 3.

```text
transaction.on_commit()
```

ব্যবহার করো যখন কাজটা **successful commit-এর পরে** চালানো দরকার।

### 4.

```text
Service
```

এর মধ্যে রাখো:

> Order / Payment / Inventory-এর core business logic।

### 5.

```text
Signal
```

ব্যবহার করো:

> Event-এর পরে loosely-coupled side effects চালানোর জন্য।

---

## PART 8-এর Mental Model

এটা মুখস্থ না করে flow হিসেবে মনে রাখো:

```text
             BUSINESS OPERATION
                    ↓
              Service Layer
                    ↓
             atomic transaction
                    ↓
             Database changes
                    ↓
                 COMMIT
                    ↓
              on_commit()
                    ↓
                 Signal
                    ↓
             Async Task
                    ↓
        Email / Notification / Webhook
```

**এটাই production-grade Django/DRF-এ Signal ব্যবহারের সবচেয়ে গুরুত্বপূর্ণ pattern।**

পরের **PART 9**-এ আমরা **Signal + Celery + Redis** একসাথে করব—যেখানে `Order PAID → Signal → Celery → background email/notification` বাস্তবে কীভাবে structure করতে হয়, এবং duplicate task কীভাবে prevent করতে হয়।

---
# PART 9 — Signal + Celery + Redis

এবার আমরা Django Signal-এর সাথে **Celery + Redis** যুক্ত করব। এটা production project-এ খুব common pattern:

```text
Order PAID
    ↓
Signal
    ↓
Celery Task
    ↓
Redis Queue
    ↓
Celery Worker
    ↓
Email / Notification / Webhook
```

আজকের লক্ষ্য হবে **কেন দরকার → কীভাবে কাজ করে → project structure → code → duplicate handling → retry**—সব বোঝা।

---

## 1. কেন Celery দরকার?

ধরো payment successful হওয়ার পর তোমাকে:

* Email পাঠাতে হবে
* SMS পাঠাতে হবে
* Push notification পাঠাতে হবে
* Invoice PDF তৈরি করতে হবে
* External webhook call করতে হবে

যদি এগুলো সরাসরি API request-এর মধ্যে করো:

```text
POST /payment/
       ↓
Payment update
       ↓
Send email       ← slow
       ↓
Generate PDF     ← slow
       ↓
Webhook          ← slow
       ↓
Response
```

তাহলে user অনেকক্ষণ response-এর জন্য অপেক্ষা করতে পারে।

### Celery ব্যবহার করলে

```text
POST /payment/
       ↓
Payment update
       ↓
Queue task
       ↓
Response immediately
       ↓
Celery Worker
       ↓
Email / PDF / Webhook
```

---

# 2. Redis-এর কাজ কী?

এখানে Redis সাধারণত **message broker** হিসেবে কাজ করবে।

```text
Django
   ↓
Redis
   ↓
Celery Worker
```

Django বলে:

> "এই কাজটা পরে করে দাও।"

Redis task queue-তে রেখে দেয়।

Celery Worker বলে:

> "ঠিক আছে, আমি কাজটা করছি।"

---

# 3. পুরো architecture

```text
                 Django / DRF
                      │
                      │ .delay()
                      ▼
                   Redis
                 Queue
                      │
                      ▼
              Celery Worker
                      │
          ┌───────────┼───────────┐
          ▼           ▼           ▼
        Email       SMS       Webhook
```

---

# 4. Project structure

ধরি project:

```text
ecommerce/
│
├── manage.py
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── celery.py
│
├── orders/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── services.py
│   ├── signals.py
│   ├── tasks.py
│   └── apps.py
│
└── requirements.txt
```

---

# 5. Celery install

```bash
pip install celery redis
```

`requirements.txt`:

```text
celery
redis
```

---

# 6. Redis চালু করা

Docker ব্যবহার করলে সহজ:

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis
```

চেক:

```bash
docker ps
```

Redis:

```text
localhost:6379
```

---

# 7. Celery configuration

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

Django apps-এর `tasks.py` খুঁজে বের করবে।

---

# 8. `__init__.py`

`config/__init__.py`:

```python
from .celery import app as celery_app


__all__ = ("celery_app",)
```

এতে Django project load হলে Celery app-ও available থাকে।

---

# 9. Settings

`settings.py`:

```python
CELERY_BROKER_URL = "redis://localhost:6379/0"
```

অর্থাৎ:

```text
Django
   ↓
Redis DB 0
```

---

# 10. প্রথম Celery Task

`orders/tasks.py`:

```python
from celery import shared_task


@shared_task
def test_task():

    print("Celery task executed")

    return "Done"
```

এখন Django shell:

```bash
python manage.py shell
```

তারপর:

```python
from orders.tasks import test_task

test_task.delay()
```

`.delay()` মানে:

> Task queue-তে পাঠাও।

---

# 11. Worker চালু করতে হবে

আরেকটা terminal:

```bash
celery -A config worker -l info
```

এখন flow:

```text
test_task.delay()
       ↓
Redis
       ↓
Celery Worker
       ↓
test_task()
```

Worker terminal-এ দেখতে পাবে task execute হয়েছে।

---

# 12. `delay()` কী করে?

ধরো:

```python
send_email.delay(order.id)
```

এটা সরাসরি:

```python
send_email(order.id)
```

এর মতো না।

### Direct call

```text
Python
 ↓
Function executes immediately
```

### Celery

```text
Python
 ↓
Queue
 ↓
Worker
 ↓
Function executes later
```

---

# 13. এখন Order example

ধরি:

```python
class Order(models.Model):

    STATUS_CHOICES = (
        ("PENDING", "Pending"),
        ("PAID", "Paid"),
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="PENDING"
    )
```

Payment successful হওয়ার পরে:

```text
Order
status = PAID
```

---

# 14. Custom Signal

`orders/signals.py`:

```python
from django.dispatch import Signal


order_paid = Signal()
```

Receiver:

```python
from django.dispatch import receiver

from .signals import order_paid
from .tasks import send_order_email


@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )
```

এখানে Signal নিজে email পাঠাচ্ছে না।

Signal:

```text
order_paid
    ↓
Celery task queue
```

---

# 15. Celery Task

`orders/tasks.py`:

```python
from celery import shared_task


@shared_task
def send_order_email(order_id):

    print(
        f"Sending email for order {order_id}"
    )

    # email sending logic
```

এখন:

```text
Order PAID
    ↓
order_paid.send()
    ↓
Signal receiver
    ↓
send_order_email.delay()
    ↓
Redis
    ↓
Celery Worker
    ↓
Email
```

---

# 16. এখন `on_commit()` যোগ করি

এখানে Part 8-এর concept ব্যবহার হবে।

`services.py`:

```python
from django.db import transaction

from .models import Order
from .signals import order_paid


@transaction.atomic
def mark_order_paid(order):

    order.status = "PAID"
    order.save()

    transaction.on_commit(
        lambda: order_paid.send(
            sender=Order,
            order=order
        )
    )

    return order
```

এখন flow:

```text
mark_order_paid()
       ↓
atomic
       ↓
Order = PAID
       ↓
on_commit registered
       ↓
COMMIT
       ↓
order_paid
       ↓
Celery
       ↓
Redis
       ↓
Worker
       ↓
Email
```

এটাই আমাদের production pattern।

---

# 17. কেন `on_commit()` এখানে দরকার?

ধরো:

```python
order.status = "PAID"
order.save()

order_paid.send(...)
```

তারপর transaction rollback হলো।

Celery task ইতিমধ্যে queue-তে চলে যেতে পারে।

তখন:

```text
Database
Order = PENDING
```

কিন্তু:

```text
Email
"Payment successful"
```

চলে যেতে পারে।

তাই:

```python
transaction.on_commit(...)
```

ব্যবহার করলে:

```text
COMMIT successful
      ↓
Signal
      ↓
Celery
```

হবে।

---

# 18. এখন Email Task-এ Database থেকে Order নেব

Task-এ পুরো Order object পাঠানো উচিত নয়।

❌ Avoid:

```python
send_order_email.delay(order)
```

বরং:

```python
send_order_email.delay(order.id)
```

Task:

```python
@shared_task
def send_order_email(order_id):

    order = Order.objects.get(
        id=order_id
    )

    # send email
```

কারণ Celery message-এ ছোট serializable identifier পাঠানো cleaner।

---

# 19. Task failure হলে?

ধরো:

```python
@shared_task
def send_order_email(order_id):

    raise Exception("Email server failed")
```

তাহলে Celery task failed হিসেবে দেখাবে।

Production system-এ retry দরকার।

---

# 20. Celery Retry

```python
from celery import shared_task


@shared_task(
    bind=True,
    autoretry_for=(Exception,),
    retry_backoff=True,
    max_retries=3
)
def send_order_email(self, order_id):

    print(
        f"Sending email for {order_id}"
    )
```

এখন failure হলে Celery retry করতে পারবে।

Concept:

```text
Attempt 1
   ↓
Failed
   ↓
Wait
   ↓
Attempt 2
   ↓
Failed
   ↓
Wait
   ↓
Attempt 3
```

---

# 21. কেন `retry_backoff=True`?

ধরো email server সাময়িকভাবে down।

তখন:

```text
retry immediately
retry immediately
retry immediately
```

না করে কিছু সময় অপেক্ষা করা ভালো।

Backoff:

```text
1st retry → wait
2nd retry → longer wait
3rd retry → longer wait
```

এতে external service-এর ওপর চাপ কমে।

---

# 22. Duplicate Task সমস্যা

এটা production-এর খুব গুরুত্বপূর্ণ বিষয়।

ধরো:

```text
Payment Gateway
     ↓
Callback 1
     ↓
Payment SUCCESS
```

কিন্তু gateway একই callback আবার পাঠাল:

```text
Callback 2
     ↓
Payment SUCCESS
```

তাহলে:

```text
send_order_email.delay()
send_order_email.delay()
```

হতে পারে।

Customer:

```text
📧 Email 1
📧 Email 2
```

পেতে পারে।

---

# 23. তাই Idempotency দরকার

PaymentService:

```python
@transaction.atomic
def mark_order_paid(payment):

    if payment.status == "SUCCESS":
        return payment

    payment.status = "SUCCESS"
    payment.save()

    order = payment.order

    order.status = "PAID"
    order.save()

    transaction.on_commit(
        lambda: order_paid.send(
            sender=Order,
            order=order
        )
    )

    return payment
```

এখানে:

```text
SUCCESS
   ↓
already processed
   ↓
return
```

ফলে একই payment আবার process হবে না।

---

# 24. আরও ভালো: Event/Notification record

বড় system-এ event track করা যায়।

ধরো:

```python
class NotificationEvent(models.Model):

    order = models.ForeignKey(
        Order,
        on_delete=models.CASCADE
    )

    event_type = models.CharField(
        max_length=100
    )

    processed = models.BooleanField(
        default=False
    )
```

তারপর:

```text
ORDER_PAID
```

একবার process হয়েছে কি না track করা যায়।

এটা আরও advanced reliability pattern।

---

# 25. Signal কি সরাসরি Celery task চালাবে?

হ্যাঁ:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )
```

এটা সাধারণত ঠিক আছে।

কিন্তু মনে রাখবে:

```text
Signal = event hook
Celery = async execution
```

দুটোর responsibility আলাদা।

---

# 26. একাধিক Celery task

ধরো Order PAID:

```text
             order_paid
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      Email      SMS       Invoice
        ↓         ↓         ↓
      Celery    Celery    Celery
```

Signal:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )

    send_order_sms.delay(
        order.id
    )

    generate_invoice.delay(
        order.id
    )
```

এগুলো background-এ চলবে।

---

# 27. কিন্তু একটা সতর্কতা

Signal-এর মধ্যে **অনেক business logic লিখবে না**।

❌ এভাবে না:

```python
@receiver(order_paid)
def handle_order_paid(...):

    check_stock()

    calculate_tax()

    calculate_shipping()

    update_inventory()

    create_payment()

    generate_invoice()

    send_email()

    send_sms()
```

এতে Signal নিজেই একটা giant business service হয়ে যাবে।

---

# 28. ভালো architecture

```text
PaymentService
     ↓
Order PAID
     ↓
on_commit
     ↓
order_paid
     ↓
Signal
     ├── send_email.delay()
     ├── send_sms.delay()
     └── generate_invoice.delay()
```

Core business logic:

```text
PaymentService
InventoryService
OrderService
```

Async side effects:

```text
Celery
```

Event connection:

```text
Signal
```

---

# 29. Production project structure

তোমার e-commerce project-এর জন্য একটা clean structure হতে পারে:

```text
orders/
│
├── models.py
├── serializers.py
├── views.py
├── urls.py
│
├── services/
│   ├── order_service.py
│   ├── payment_service.py
│   └── refund_service.py
│
├── signals.py
├── tasks.py
└── apps.py
```

আর project level:

```text
config/
├── settings.py
├── celery.py
├── urls.py
└── __init__.py
```

---

# 30. Final production flow

এখন সবকিছু একসাথে দেখো:

```text
                    API
                     │
                     ▼
                Serializer
                     │
                     ▼
                View / Service
                     │
                     ▼
             PaymentService
                     │
             transaction.atomic
                     │
          ┌──────────┴──────────┐
          │                     │
       Payment              Order
       SUCCESS                PAID
          │                     │
          └──────────┬──────────┘
                     ▼
              transaction.commit
                     │
                     ▼
                on_commit()
                     │
                     ▼
               order_paid
                  Signal
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       Email       Invoice      SMS
       Task          Task       Task
          │          │          │
          └──────────┼──────────┘
                     ▼
                   Redis
                     │
                     ▼
              Celery Workers
```

---

# 31. আজকের ৭টা Golden Rule

### Rule 1

**Core business logic → Service**

```text
Order
Payment
Refund
Inventory
```

### Rule 2

**Event → Signal**

```text
order_paid
order_created
user_registered
```

### Rule 3

**Transaction → `atomic()`**

```python
with transaction.atomic():
    ...
```

### Rule 4

**Commit-এর পরে side-effect → `on_commit()`**

```python
transaction.on_commit(...)
```

### Rule 5

**Heavy/slow কাজ → Celery**

```text
Email
SMS
PDF
Webhook
```

### Rule 6

**Queue → Redis**

```text
Django → Redis → Celery
```

### Rule 7

**Payment/order event → Idempotency**

একই event দুইবার এলে যেন double processing না হয়।

---

## PART 9 Mental Model

শুধু এই flow-টা ভালোভাবে বুঝে রাখো:

```text
Service
   ↓
atomic()
   ↓
Database changes
   ↓
COMMIT
   ↓
on_commit()
   ↓
Signal
   ↓
Celery
   ↓
Redis
   ↓
Worker
   ↓
Email / SMS / Notification
```

এখন তুমি Django Signals-এর basic থেকে অনেকটাই **production architecture level**-এ চলে এসেছ।

**PART 10**-এ আমরা আরও গুরুত্বপূর্ণ বিষয় করব: **Signal-এর `weak`, `dispatch_uid`, receiver duplication, signal registration, `apps.py`, circular import এবং testing**—অর্থাৎ production project-এ Signal-এর hidden problems এবং সেগুলো কীভাবে ঠিকভাবে handle করতে হয়।


----
# PART 10 — Production Signal: Registration, Duplicate Receiver, `dispatch_uid`, Circular Import & Testing

এবার আমরা Signals-এর এমন কিছু বিষয় শিখব যেগুলো ছোট project-এ চোখে পড়ে না, কিন্তু **বড় Django/DRF project-এ খুব গুরুত্বপূর্ণ**।

আজকের মূল বিষয়:

```text
Signal
├── কোথায় register করব?
├── কেন duplicate execute হতে পারে?
├── dispatch_uid কী?
├── apps.py কেন গুরুত্বপূর্ণ?
├── circular import কীভাবে হয়?
├── testing কীভাবে করব?
└── signal কখন disable/avoid করব?
```

---

# 1. প্রথমে Signal Registration

আমরা আগে লিখেছিলাম:

```python
@receiver(post_save, sender=Product)
def create_inventory(sender, instance, created, **kwargs):
    ...
```

কিন্তু Django-কে জানতে হবে:

> "এই `signals.py` file load করো।"

এজন্য `apps.py` ব্যবহার করি।

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):

    default_auto_field = "django.db.models.BigAutoField"

    name = "products"

    def ready(self):
        import products.signals
```

---

# 2. `ready()` কখন চলে?

Django application initialize করার সময়:

```text
Django Start
    ↓
AppConfig
    ↓
ready()
    ↓
signals.py import
    ↓
Signal receiver registered
```

অর্থাৎ:

```python
def ready(self):
    import products.signals
```

এর উদ্দেশ্য হলো:

> Django startup-এর সময় signal receiver register করা।

---

# 3. `INSTALLED_APPS`-এ AppConfig

তোমার app:

```text
products/
```

থাকলে `settings.py`-এ:

```python
INSTALLED_APPS = [
    ...
    "products.apps.ProductsConfig",
]
```

দেওয়া ভালো।

তাহলে:

```text
Django
 ↓
ProductsConfig
 ↓
ready()
 ↓
products.signals
```

---

# 4. Signal registration-এর recommended structure

### `products/apps.py`

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):

    default_auto_field = "django.db.models.BigAutoField"

    name = "products"

    def ready(self):
        from . import signals
```

আমি এখানে:

```python
from . import signals
```

ব্যবহার করছি।

এটা সাধারণত clean এবং relative import হওয়ায় maintain করা সহজ।

---

# 5. Signal file

`products/signals.py`

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product, Inventory


@receiver(post_save, sender=Product)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

---

# 6. Duplicate Signal Problem

এখন একটা interesting problem।

ধরো একই receiver accidentally দুইবার connect হয়ে গেল।

```text
post_save
   │
   ├── create_inventory()
   └── create_inventory()
```

Product create:

```text
Product created
      ↓
post_save
      ↓
Receiver 1
      ↓
Receiver 2
```

ফলে একই কাজ দুইবার হতে পারে।

যেমন:

```text
Inventory
Inventory
```

---

# 7. `dispatch_uid`

Django Signal-এ receiver-এর unique identity দেওয়ার জন্য:

```python
@receiver(
    post_save,
    sender=Product,
    dispatch_uid="product_create_inventory"
)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

এখানে:

```text
dispatch_uid
```

মানে:

> এই receiver-এর একটা unique identifier।

---

# 8. `dispatch_uid` কেন useful?

ধরো receiver accidentally পুনরায় connect হলো।

Django একই:

```text
dispatch_uid
```

দেখলে duplicate registration prevent করতে পারে।

তাই reusable/complex project-এ:

```python
dispatch_uid="product_create_inventory"
```

দেওয়া useful হতে পারে।

---

# 9. `dispatch_uid` কি সব Signal-এ mandatory?

না।

ছোট project-এ:

```python
@receiver(post_save, sender=Product)
```

যথেষ্ট।

কিন্তু যদি:

* multiple registration-এর possibility থাকে
* dynamic signal connection থাকে
* testing-এ connect/disconnect করা হয়
* বড় project হয়

তখন `dispatch_uid` useful।

---

# 10. `signals.py`-তে model import

ধরো:

```python
from .models import Product
```

এটা normal।

কিন্তু circular dependency তৈরি করলে সমস্যা হতে পারে।

যেমন:

```text
models.py
   ↓
signals.py
   ↓
models.py
```

---

# 11. Circular Import Example

ধরো `models.py`:

```python
from .signals import something
```

আর `signals.py`:

```python
from .models import Product
```

তাহলে:

```text
models
 ↓
signals
 ↓
models
 ↓
signals
...
```

Python বলবে:

```text
ImportError
```

---

# 12. Solution

সাধারণভাবে:

### `models.py`

```python
# signals import করো না
```

### `signals.py`

```python
from .models import Product
```

### `apps.py`

```python
def ready(self):
    from . import signals
```

Architecture:

```text
models
   ↑
signals
   ↑
apps.ready()
```

এভাবে dependency clean থাকে।

---

# 13. Signal receiver-এ import problem

আরেকটা useful technique:

```python
@receiver(post_save, sender="products.Product")
def product_saved(...):
    ...
```

কখনো string sender ব্যবহার করা যায়।

তবে সাধারণভাবে:

```python
sender=Product
```

সবচেয়ে readable।

String sender বিশেষ পরিস্থিতিতে circular dependency কমাতে সাহায্য করতে পারে।

---

# 14. `weak=False` কী?

এখন Signals-এর একটু advanced option:

```python
post_save.connect(
    my_receiver,
    sender=Product,
    weak=False
)
```

Django signal receiver সাধারণত weak reference ব্যবহার করতে পারে।

`weak=False` দিলে receiver-এর strong reference রাখা হয়।

সাধারণ project-এ তোমার প্রায় কখনোই এটা দরকার হবে না।

তাই:

```python
weak=False
```

দেখলেই ধরে নেবে:

> বিশেষ use case ছাড়া এটা ব্যবহার করার প্রয়োজন নেই।

---

# 15. `@receiver` বনাম `.connect()`

দুইভাবে Signal connect করা যায়।

### Method 1 — Decorator

```python
@receiver(
    post_save,
    sender=Product
)
def product_saved(
    sender,
    instance,
    **kwargs
):
    ...
```

এটা সবচেয়ে readable।

---

### Method 2 — Manual connect

```python
def product_saved(
    sender,
    instance,
    **kwargs
):
    ...


post_save.connect(
    product_saved,
    sender=Product
)
```

দুটোই valid।

Production Django code-এ সাধারণত:

```python
@receiver(...)
```

বেশি readable।

---

# 16. Signal Disconnect

কখনো testing বা special case-এ:

```python
post_save.disconnect(
    product_saved,
    sender=Product
)
```

করতে পারো।

আবার:

```python
post_save.connect(
    product_saved,
    sender=Product
)
```

দিয়ে connect করা যায়।

---

# 17. Testing Signals

এটা খুব গুরুত্বপূর্ণ।

ধরো requirement:

> Product তৈরি হলে Inventory automatically তৈরি হবে।

Test লিখব:

```python
from django.test import TestCase

from products.models import Product, Inventory


class ProductSignalTest(TestCase):

    def test_inventory_created_when_product_created(self):

        product = Product.objects.create(
            name="Laptop",
            price=50000
        )

        self.assertTrue(
            Inventory.objects.filter(
                product=product
            ).exists()
        )
```

---

# 18. Test-এর flow

```text
Product.objects.create()
        ↓
post_save
        ↓
create_inventory()
        ↓
Inventory created
        ↓
assert
        ↓
PASS
```

এখানে আমরা শুধু test করছি না যে Product তৈরি হয়েছে।

আমরা test করছি:

> **Signal-এর expected side effect হয়েছে কি না।**

---

# 19. `created` behavior test

আরেকটা test:

```python
def test_inventory_not_duplicated_on_update(self):

    product = Product.objects.create(
        name="Laptop",
        price=50000
    )

    product.price = 55000
    product.save()

    self.assertEqual(
        Inventory.objects.filter(
            product=product
        ).count(),
        1
    )
```

এখানে:

```text
CREATE
 ↓
Inventory = 1

UPDATE
 ↓
Inventory = still 1
```

কারণ:

```python
if created:
```

---

# 20. Custom Signal Test

ধরো:

```python
order_paid = Signal()
```

আমরা test করতে চাই signal পাঠানো হয়েছে কি না।

একটা receiver:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):
    ...
```

Test-এ signal mocking করা যায়।

Advanced testing-এ:

```python
from unittest.mock import patch
```

ব্যবহার করা যায়।

উদাহরণ:

```python
@patch("orders.services.order_paid.send")
def test_order_paid_event(mock_send):

    mark_order_paid(order)

    mock_send.assert_called_once()
```

এতে আমরা verify করছি:

```text
Service
  ↓
order_paid.send()
```

call হয়েছে।

---

# 21. `on_commit()` Testing-এর সমস্যা

এখন একটা subtle বিষয়।

Production code:

```python
transaction.on_commit(
    lambda: order_paid.send(...)
)
```

Test-এ callback কখন execute হবে সেটা test transaction behavior-এর ওপর নির্ভর করতে পারে।

Django `TestCase` transaction handling করে।

তাই callback test করার সময়:

```python
self.captureOnCommitCallbacks(
    execute=True
)
```

ব্যবহার করা যায়।

Example:

```python
with self.captureOnCommitCallbacks(
    execute=True
):

    mark_order_paid(order)
```

এরপর callback execute হয়েছে কিনা assert করতে পারো।

---

# 22. Celery Signal Testing

ধরো:

```python
@receiver(order_paid)
def handle_order_paid(
    sender,
    order,
    **kwargs
):

    send_order_email.delay(
        order.id
    )
```

Test:

```python
from unittest.mock import patch


@patch(
    "orders.signals.send_order_email.delay"
)
def test_order_email_task(
    mock_delay
):

    order_paid.send(
        sender=Order,
        order=order
    )

    mock_delay.assert_called_once_with(
        order.id
    )
```

এতে actual Celery worker চালাতে হচ্ছে না।

আমরা শুধু test করছি:

```text
Signal
 ↓
.delay(order.id)
```

ঠিকভাবে call হয়েছে কি না।

---

# 23. Signal-এর আরেকটা danger — Hidden behavior

ধরো developer লিখল:

```python
Product.objects.create(...)
```

সে শুধু Product create করার কথা ভাবছে।

কিন্তু background-এ:

```text
post_save
 ↓
Inventory
 ↓
Audit
 ↓
Notification
 ↓
Celery
```

চলতে পারে।

এটা Signal-এর power, আবার danger-ও।

কারণ developer code দেখে সব side effect বুঝতে নাও পারে।

তাই Signals-এর naming clear হওয়া উচিত:

```python
create_product_inventory
create_product_audit_log
notify_product_created
```

এমন descriptive নাম ব্যবহার করো।

---

# 24. Signal-এ heavy business logic লিখবে না

❌ খারাপ:

```python
@receiver(post_save, sender=Order)
def process_everything(...):

    check_inventory()
    calculate_tax()
    reserve_stock()
    charge_payment()
    create_invoice()
    send_sms()
    send_email()
```

এতে debugging nightmare হয়ে যাবে।

---

# 25. ভালো architecture

```text
OrderService
    ↓
Business Logic
    ↓
Database
    ↓
COMMIT
    ↓
Domain Event
    ↓
Signal
    ↓
Celery
```

Signal:

```python
@receiver(order_paid)
def handle_order_paid(...):

    send_email.delay(order.id)
```

শুধু event handling করছে।

---

# 26. কখন Signal ব্যবহার না করাই ভালো?

এটা খুব গুরুত্বপূর্ণ।

যদি operation-এর success/failure-এর ওপর মূল business decision নির্ভর করে:

```text
Payment
Inventory
Refund
Order cancellation
Stock reservation
Money transfer
```

তাহলে Signal-এর ওপর পুরো workflow depend করো না।

বরং:

```text
PaymentService
InventoryService
OrderService
RefundService
```

ব্যবহার করো।

---

# 27. Signal কোথায় সবচেয়ে ভালো?

Signal-এর জন্য ভালো use case:

```text
User created
    ↓
Create profile

Product created
    ↓
Create basic inventory

Order created
    ↓
Create history

Payment completed
    ↓
Emit event

User registered
    ↓
Trigger welcome notification
```

তবে notification/email-এর মতো external side effect হলে:

```text
Signal
 ↓
Celery
```

ভালো pattern।

---

# 28. `dispatch_uid` + `ready()` + `on_commit()`

এই তিনটার সম্পর্ক মনে রাখো:

### `ready()`

```text
Django startup
   ↓
Register receiver
```

### `dispatch_uid`

```text
Receiver identity
   ↓
Avoid duplicate registration
```

### `on_commit()`

```text
Transaction success
   ↓
Run callback
```

তিনটার কাজ সম্পূর্ণ আলাদা।

---

# 29. Production Signal Checklist

কোনো নতুন Signal লিখলে নিজেকে জিজ্ঞেস করবে:

```text
☑ Receiver কি apps.py → ready() দিয়ে load হচ্ছে?

☑ Signal কি duplicate register হতে পারে?

☑ দরকার হলে dispatch_uid আছে?

☑ Circular import হচ্ছে না?

☑ created/update distinction ঠিক আছে?

☑ QuerySet.update() signal bypass করবে কিনা জানি?

☑ Transaction-এর মধ্যে external side effect করছি কি?

☑ দরকার হলে on_commit() ব্যবহার করেছি?

☑ Heavy কাজ Celery-তে পাঠিয়েছি?

☑ Duplicate event হলে idempotent থাকবে?

☑ Signal-এর unit test আছে?
```

---

# 30. পুরো Production Architecture

এখন Part 1 থেকে Part 10 পর্যন্ত শেখা জিনিসগুলো একসাথে:

```text
                         DRF API
                            │
                            ▼
                       Serializer
                            │
                            ▼
                       View / Service
                            │
                            ▼
                    Business Operation
                            │
                     atomic transaction
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
           Order         Payment        Inventory
             │              │              │
             └──────────────┼──────────────┘
                            │
                         COMMIT
                            │
                      on_commit()
                            │
                            ▼
                       Domain Event
                            │
                            ▼
                         Signal
                            │
                 ┌──────────┼──────────┐
                 ▼          ▼          ▼
              Audit       Celery     Analytics
                            │
                            ▼
                          Redis
                            │
                            ▼
                      Celery Worker
                            │
                    ┌───────┼────────┐
                    ▼       ▼        ▼
                  Email     SMS    Webhook
```

---

# PART 10 — Final Mental Model

তুমি এখন Signals-কে শুধু:

```python
@receiver(post_save)
```

হিসেবে দেখবে না।

বরং:

```text
Django Model Event
       ↓
Signal
       ↓
Event Handling
       ↓
on_commit (যদি প্রয়োজন)
       ↓
Celery (যদি কাজ heavy/external হয়)
```

আর core business:

```text
Order
Payment
Inventory
Refund
Cancellation
Exchange
```

এসব:

```text
Service Layer
```

এর মধ্যে থাকবে।

### সবচেয়ে গুরুত্বপূর্ণ rule:

> **Signal যেন তোমার business logic-এর কেন্দ্র না হয়; Signal হবে business event-এর listener.**

---

### PART 1 → PART 10 পর্যন্ত আমরা যা শিখলাম

```text
Part 1  → Signal Basic
Part 2  → pre_save / post_save
Part 3  → pre_delete / post_delete
Part 4  → m2m_changed
Part 5  → Custom Signal
Part 6  → Serializer + Signal
Part 7  → Service + Signal
Part 8  → atomic + on_commit
Part 9  → Signal + Celery + Redis
Part 10 → Production Signal Problems + Testing
```

এর পরের logical step হবে **PART 11 — Advanced Signal Patterns**, যেখানে আমরা **Order Status Change detect করা, old value বনাম new value, `pre_save` দিয়ে previous state বের করা, state transition event (`PENDING → PAID`, `PAID → REFUNDED`) এবং কীভাবে ভুলভাবে status-change Signal লিখলে duplicate event হয়**—এগুলো বাস্তব e-commerce code দিয়ে করব।

---
# PART 11 — Advanced Django Signals: Old Value → New Value → State Transition

এখন আমরা Signals-এর সবচেয়ে গুরুত্বপূর্ণ **production-level pattern** শিখব:

> **কোনো model-এর field change হলে কীভাবে বুঝব old value কী ছিল, new value কী হয়েছে, এবং নির্দিষ্ট state transition হলে কীভাবে event trigger করব।**

বিশেষ করে E-commerce-এ:

```text
PENDING → PAID
PAID → SHIPPED
SHIPPED → DELIVERED
PAID → REFUNDED
PENDING → CANCELLED
```

এই ধরনের state transition খুব common।

---

# 1. Problemটা কোথায়?

ধরি আমাদের `Order` model:

```python
class Order(models.Model):

    STATUS_CHOICES = (
        ("PENDING", "Pending"),
        ("PAID", "Paid"),
        ("SHIPPED", "Shipped"),
        ("DELIVERED", "Delivered"),
        ("CANCELLED", "Cancelled"),
        ("REFUNDED", "Refunded"),
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    total = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="PENDING"
    )
```

এখন:

```python
order.status = "PAID"
order.save()
```

`post_save`-এ আমরা কী পাই?

```python
@receiver(post_save, sender=Order)
def order_saved(sender, instance, created, **kwargs):

    print(instance.status)
```

Output:

```text
PAID
```

কিন্তু প্রশ্ন:

> আগে status কী ছিল?

Signal শুধু `instance.status` দিয়ে old value জানে না।

আমাদের দরকার:

```text
OLD STATUS = PENDING
NEW STATUS = PAID
```

---

# 2. কেন এটা গুরুত্বপূর্ণ?

ধরি আমরা চাই:

```text
PENDING → PAID
       ↓
send payment confirmation
```

আবার:

```text
PAID → REFUNDED
       ↓
send refund notification
```

কিন্তু যদি আমরা শুধু এটা করি:

```python
@receiver(post_save, sender=Order)
def order_saved(sender, instance, **kwargs):

    if instance.status == "PAID":
        send_payment_email(instance)
```

তাহলে সমস্যা হবে।

কারণ:

```python
order.status = "PAID"
order.save()
```

তারপর আবার:

```python
order.total = 6000
order.save()
```

এখনও:

```python
instance.status == "PAID"
```

তাই আবার email চলে যেতে পারে।

অর্থাৎ আমরা চাই:

```text
PENDING → PAID
```

শুধু তখন event trigger হবে।

---

# 3. State Transition কী?

সহজভাবে:

```text
old state → new state
```

Example:

```text
PENDING → PAID
```

এটাই একটা **state transition**।

আর:

```text
PAID → SHIPPED
```

আরেকটা transition।

---

# 4. প্রথম approach — `pre_save` দিয়ে old value বের করা

আমরা database থেকে পুরোনো object fetch করতে পারি।

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

@receiver(pre_save, sender=Order)
def order_pre_save(sender, instance, **kwargs):

    if not instance.pk:
        return

    old_order = Order.objects.get(pk=instance.pk)

    print("Old:", old_order.status)
    print("New:", instance.status)
```

ধরি database-এ:

```text
Order 1
status = PENDING
```

আমরা করি:

```python
order.status = "PAID"
order.save()
```

তখন:

```text
Old: PENDING
New: PAID
```

---

# 5. কেন `if not instance.pk`?

খুব গুরুত্বপূর্ণ।

নতুন object:

```python
order = Order(
    user=user,
    total=5000
)

order.save()
```

`save()` হওয়ার আগে:

```python
instance.pk
```

নাও থাকতে পারে।

তাই:

```python
if not instance.pk:
    return
```

মানে:

> এটা নতুন object হলে old database record খুঁজতে যেও না।

---

# 6. কিন্তু একটা বড় সমস্যা আছে

এই code:

```python
old_order = Order.objects.get(pk=instance.pk)
```

প্রতিবার database query করবে।

যদি 1000টা Order update হয়:

```text
1000 updates
+
1000 extra SELECT queries
```

এটা performance-এর জন্য ভালো না।

আরেকটা সমস্যা আছে।

ধরি:

```python
order.status = "PAID"
order.save()
```

`pre_save` old value বের করতে পারবে।

কিন্তু যদি আমরা state transition-এর ওপর business event তৈরি করতে চাই, তখন architecture আরও carefully design করা দরকার।

---

# 7. Old vs New আলাদা করে রাখা

আমরা একটা clean pattern করতে পারি।

```python
@receiver(pre_save, sender=Order)
def order_pre_save(sender, instance, **kwargs):

    if not instance.pk:
        instance._old_status = None
        return

    old_order = sender.objects.get(pk=instance.pk)

    instance._old_status = old_order.status
```

এখন object-এর মধ্যে temporarily:

```python
instance._old_status
```

থাকবে।

ধরি:

```text
Database:
status = PENDING
```

তারপর:

```python
order.status = "PAID"
order.save()
```

`pre_save`-এ:

```python
instance._old_status = "PENDING"
```

এবং:

```python
instance.status = "PAID"
```

তাহলে আমরা পাই:

```text
old = instance._old_status
new = instance.status
```

---

# 8. তারপর `post_save`

```python
@receiver(post_save, sender=Order)
def order_post_save(sender, instance, created, **kwargs):

    if created:
        return

    old_status = getattr(instance, "_old_status", None)
    new_status = instance.status

    print(
        f"{old_status} → {new_status}"
    )
```

Output:

```text
PENDING → PAID
```

---

# 9. নির্দিষ্ট transition detect করা

এখন আসল কাজ।

```python
@receiver(post_save, sender=Order)
def order_post_save(sender, instance, created, **kwargs):

    if created:
        return

    old_status = getattr(instance, "_old_status", None)
    new_status = instance.status

    if old_status == "PENDING" and new_status == "PAID":
        print("Order has been paid")
```

এখন:

```text
PENDING → PAID
```

হলে trigger হবে।

কিন্তু:

```text
PAID → PAID
```

হলে trigger হবে না।

এটাই আমরা চাই।

---

# 10. Multiple state transition

ধরি:

```python
@receiver(post_save, sender=Order)
def order_post_save(sender, instance, created, **kwargs):

    if created:
        return

    old_status = getattr(instance, "_old_status", None)
    new_status = instance.status

    if old_status == "PENDING" and new_status == "PAID":
        print("Payment successful")

    elif old_status == "PAID" and new_status == "SHIPPED":
        print("Order shipped")

    elif old_status == "SHIPPED" and new_status == "DELIVERED":
        print("Order delivered")

    elif old_status == "PAID" and new_status == "REFUNDED":
        print("Order refunded")

    elif old_status == "PENDING" and new_status == "CANCELLED":
        print("Order cancelled")
```

এখন আমরা state machine-এর মতো behavior পাচ্ছি।

---

# 11. কিন্তু Production-এ এইভাবে অনেক `if` রাখা ভালো না

যেমন:

```python
if old == "PENDING" and new == "PAID":
    ...

elif old == "PAID" and new == "SHIPPED":
    ...

elif old == "SHIPPED" and new == "DELIVERED":
    ...
```

১০টা status হলে code বড় হয়ে যাবে।

তাই transition আলাদা করে define করা যায়।

```python
TRANSITIONS = {
    ("PENDING", "PAID"): "order_paid",
    ("PAID", "SHIPPED"): "order_shipped",
    ("SHIPPED", "DELIVERED"): "order_delivered",
    ("PAID", "REFUNDED"): "order_refunded",
    ("PENDING", "CANCELLED"): "order_cancelled",
}
```

তারপর:

```python
transition = (old_status, new_status)

event = TRANSITIONS.get(transition)

if event:
    print(event)
```

Example:

```text
old = PENDING
new = PAID
```

তাহলে:

```python
transition = ("PENDING", "PAID")
```

এবং:

```python
event = "order_paid"
```

---

# 12. আরও ভালো — Custom Domain Signals

এখন আগের Part 5-এর concept ব্যবহার করি।

```python
order_paid = Signal()
order_shipped = Signal()
order_refunded = Signal()
order_cancelled = Signal()
```

তারপর state transition detect করে event fire করা যায়।

```python
@receiver(post_save, sender=Order)
def order_post_save(sender, instance, created, **kwargs):

    if created:
        return

    old_status = getattr(instance, "_old_status", None)
    new_status = instance.status

    if old_status == "PENDING" and new_status == "PAID":

        order_paid.send(
            sender=Order,
            order=instance
        )
```

এখন:

```text
Order status change
       ↓
PENDING → PAID
       ↓
order_paid
       ↓
Receivers
```

---

# 13. এখানে একটা খুব গুরুত্বপূর্ণ Architecture

আমরা এখন পুরো architecture-টা দেখতে পারি:

```text
Order Service
      ↓
change status
      ↓
atomic transaction
      ↓
Order saved
      ↓
COMMIT
      ↓
on_commit()
      ↓
order_paid event
      ↓
Signal
      ↓
Celery
      ↓
Email / Notification
```

এটা production architecture-এর দিকে যাচ্ছে।

---

# 14. কিন্তু আরও বড় প্রশ্ন

ধরি:

```python
order.status = "PAID"
order.save()
```

`post_save` হলো।

তারপর transaction rollback হলো।

তাহলে `post_save`-এ সরাসরি:

```python
order_paid.send(...)
```

করলে problem হতে পারে।

কারণ:

```text
post_save
   ↓
event fired
   ↓
transaction rollback
```

Database-এ Order আর PAID নেই।

কিন্তু email হয়তো চলে গেছে:

> "Your payment was successful."

এটা ভুল।

তাই আমরা আগের Part 8-এর rule ব্যবহার করব:

```python
transaction.on_commit()
```

---

# 15. Production Pattern

ধরি service:

```python
from django.db import transaction

@transaction.atomic
def mark_order_paid(order):

    order.status = "PAID"
    order.save()

    transaction.on_commit(
        lambda: order_paid.send(
            sender=Order,
            order=order
        )
    )

    return order
```

Flow:

```text
mark_order_paid()
        ↓
atomic()
        ↓
Order = PAID
        ↓
DB save
        ↓
COMMIT
        ↓
order_paid.send()
```

এখন event শুধু successful commit-এর পরে fire হবে।

---

# 16. একটা গুরুত্বপূর্ণ Warning — `QuerySet.update()`

এইটা:

```python
Order.objects.filter(
    id=order.id
).update(
    status="PAID"
)
```

সাধারণভাবে:

```text
pre_save ❌
post_save ❌
```

trigger করবে না।

কারণ এখানে model-এর:

```python
save()
```

call হচ্ছে না।

তাই state transition signal-এর ওপর depend করলে:

```python
order.status = "PAID"
order.save()
```

এবং:

```python
Order.objects.filter(...).update(status="PAID")
```

একই behavior দেবে না।

Production-এ এটা খুব গুরুত্বপূর্ণ।

---

# 17. আরও ভালো Production Pattern: Service-এ Transition

আমাদের E-commerce architecture যেহেতু production-grade হচ্ছে, সবচেয়ে গুরুত্বপূর্ণ rule হবে:

> **Critical state transition Signal-এর ওপর depend না করে Service Layer-এ explicitly control করা।**

Example:

```python
@transaction.atomic
def mark_order_paid(order):

    if order.status != "PENDING":
        raise ValueError(
            "Only pending order can be paid."
        )

    order.status = "PAID"
    order.save(update_fields=["status"])

    transaction.on_commit(
        lambda: order_paid.send(
            sender=Order,
            order=order
        )
    )

    return order
```

এখানে আমরা আগে check করছি:

```python
if order.status != "PENDING":
```

অর্থাৎ:

```text
PENDING → PAID ✅
PAID → PAID ❌
SHIPPED → PAID ❌
CANCELLED → PAID ❌
```

এটা অনেক বেশি reliable।

---

# 18. কেন Service + Signal দুইটা একসাথে?

এখানে responsibility ভাগ করা হয়েছে।

### Service

বলবে:

> Order PAID করা যাবে কি না?

```python
if order.status != "PENDING":
    raise ValueError(...)
```

এবং:

```python
order.status = "PAID"
```

### Signal

বলবে:

> Order PAID হওয়ার পরে আর কী কী side effect হবে?

যেমন:

```text
order_paid
   ├── send email
   ├── send notification
   ├── analytics
   └── audit log
```

---

# 19. এটা খুব গুরুত্বপূর্ণ mental model

### ভুল architecture

```text
post_save
   ↓
if status == PAID:
   ↓
payment logic
   ↓
inventory logic
   ↓
refund logic
   ↓
email
   ↓
notification
```

Signal বিশাল হয়ে যাবে।

---

### ভালো architecture

```text
PaymentService
      ↓
Validate transition
      ↓
Atomic transaction
      ↓
Order = PAID
      ↓
Commit
      ↓
order_paid event
      ↓
Signals
      ├── Audit
      ├── Notification
      ├── Analytics
      └── Celery Email
```

---

# 20. Complete Example

### `models.py`

```python
class Order(models.Model):

    STATUS_CHOICES = (
        ("PENDING", "Pending"),
        ("PAID", "Paid"),
        ("SHIPPED", "Shipped"),
        ("DELIVERED", "Delivered"),
        ("CANCELLED", "Cancelled"),
        ("REFUNDED", "Refunded"),
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    total = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="PENDING"
    )
```

### `signals.py`

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

from .models import Order


@receiver(pre_save, sender=Order)
def order_pre_save(sender, instance, **kwargs):

    if not instance.pk:
        instance._old_status = None
        return

    old_order = sender.objects.get(
        pk=instance.pk
    )

    instance._old_status = old_order.status
```

তারপর:

```python
@receiver(post_save, sender=Order)
def order_post_save(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        return

    old_status = getattr(
        instance,
        "_old_status",
        None
    )

    new_status = instance.status

    if (
        old_status == "PENDING"
        and new_status == "PAID"
    ):
        print("Order Paid")

    elif (
        old_status == "PAID"
        and new_status == "REFUNDED"
    ):
        print("Order Refunded")
```

এটা শেখার জন্য useful pattern।

কিন্তু **production-critical order state machine-এর final implementation হিসেবে আমি Service Layer-কে বেশি prefer করব।**

---

# 21. আরেকটা গুরুত্বপূর্ণ বিষয়: `update_fields`

ধরি:

```python
order.status = "PAID"

order.save(
    update_fields=["status"]
)
```

তবুও:

```text
pre_save
post_save
```

trigger হবে।

কিন্তু শুধু:

```text
status
```

field database-এ update হবে।

Signal-এর মধ্যে চাইলে:

```python
kwargs.get("update_fields")
```

দেখতে পারি।

Example:

```python
@receiver(post_save, sender=Order)
def order_post_save(
    sender,
    instance,
    created,
    update_fields,
    **kwargs
):

    print(update_fields)
```

যদি:

```python
order.save(update_fields=["status"])
```

হয়:

```text
{'status'}
```

পেতে পারি।

---

# 22. আজকের সবচেয়ে গুরুত্বপূর্ণ ৫টা জিনিস

### ① Old value

```python
old_order = Order.objects.get(
    pk=instance.pk
)

old_status = old_order.status
```

### ② New value

```python
new_status = instance.status
```

### ③ Transition

```python
(old_status, new_status)
```

Example:

```python
("PENDING", "PAID")
```

### ④ Critical workflow

Service Layer:

```python
mark_order_paid()
```

### ⑤ Side effects

Signal:

```text
order_paid
    ↓
email
notification
audit
analytics
```

---

# 🧠 Final Mental Model

```text
                 ORDER STATE MACHINE

                    PENDING
                       │
                       │ payment
                       ▼
                     PAID
                    /    \
                   /      \
              shipping    refund
                 ↓          ↓
              SHIPPED    REFUNDED
                 │
                 │ delivery
                 ▼
             DELIVERED


Service Layer
      │
      ├── Validate transition
      ├── transaction.atomic()
      ├── Update Order
      └── on_commit()
                │
                ▼
          Domain Event
                │
                ▼
             Signal
          ┌─────┼─────┐
          ↓     ↓     ↓
        Email Audit Notification
          │
          ▼
        Celery
          │
          ▼
        Redis
```

**Part 11-এর মূল কথা:**

> `Signal` দিয়ে old value → new value detect করা যায়, কিন্তু **Order/Payment/Inventory-এর critical state transition Service Layer-এ explicitভাবে control করা উচিত; Signal ব্যবহার করা উচিত সেই transition-এর পরের side effects-এর জন্য।**

পরের **PART 12**-এ আমরা আরও production-level বিষয় ধরতে পারি: **Signal recursion/infinite loop, `save()` থেকে আবার `save()`, `post_save` recursion কীভাবে হয় এবং কীভাবে safely prevent করা যায়।**

----
# PART 12 — Django Signal Recursion, Infinite Loop & Safe Patterns

এখন আমরা Signals-এর এমন একটা বিষয় শিখব যেটা production project-এ **খুব dangerous** হতে পারে:

> একটা Signal-এর ভিতরে আবার `save()` করলে সেই একই Signal আবার trigger হতে পারে।

এতে **infinite loop / recursion** হতে পারে।

---

# 1. প্রথমে Problemটা বুঝি

ধরি আমাদের `Product` model:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
    slug = models.SlugField(
        unique=True,
        blank=True
    )
```

আমরা চাই:

> Product save হলে automatically slug তৈরি হবে।

একজন beginner হয়তো এমন লিখবে:

```python
@receiver(post_save, sender=Product)
def create_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = slugify(instance.name)
        instance.save()
```

দেখতে ঠিক মনে হচ্ছে।

কিন্তু এখানে dangerous অংশ:

```python
instance.save()
```

কারণ আমরা আছি:

```text
post_save
```

এর ভিতরে।

---

# 2. কী হচ্ছে step-by-step?

ধরি:

```python
product = Product.objects.create(
    name="Gaming Laptop"
)
```

Flow:

```text
Product.objects.create()
        ↓
Product.save()
        ↓
post_save
        ↓
create_slug()
        ↓
instance.save()
        ↓
post_save
        ↓
create_slug()
        ↓
instance.save()
        ↓
post_save
        ↓
...
```

এটা চলতেই থাকবে।

```text
♾️
```

শেষ পর্যন্ত:

```text
RecursionError
```

হতে পারে।

---

# 3. `if not instance.slug` কি আমাদের বাঁচাবে?

অনেক সময় প্রথমবার মনে হবে:

```python
@receiver(post_save, sender=Product)
def create_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = slugify(instance.name)
        instance.save()
```

প্রথম save:

```text
slug = ""
```

তাই:

```text
slug তৈরি
↓
save()
```

দ্বিতীয়বার:

```text
slug = gaming-laptop
```

তাই:

```python
if not instance.slug:
```

False।

তখন আর save হবে না।

### তাহলে recursion হলো না?

এই particular example-এ **infinite recursion নাও হতে পারে**।

কিন্তু patternটা এখনও risky।

কারণ Signal-এর ভিতরে আবার model save করলে:

```text
post_save
   ↓
save()
   ↓
post_save
```

অর্থাৎ একই signal আবার execute হচ্ছে।

Production code-এ এ ধরনের hidden behavior avoid করা ভালো।

---

# 4. আরও dangerous example

ধরি:

```python
class Order(models.Model):

    status = models.CharField(max_length=20)

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

Signal:

```python
@receiver(post_save, sender=Order)
def update_order(sender, instance, **kwargs):

    instance.updated_at = timezone.now()
    instance.save()
```

এখন:

```text
post_save
   ↓
save()
   ↓
post_save
   ↓
save()
   ↓
post_save
   ↓
save()
   ↓
∞
```

এখানে কোনো stopping condition নেই।

এটা সরাসরি infinite recursion।

---

# 5. Signal-এর ভিতরে `save()` কেন avoid করা উচিত?

কারণ:

```python
instance.save()
```

মানে আবার:

```text
pre_save
↓
DB save
↓
post_save
```

তাই Signal-এর ভিতরে save করলে Signal lifecycle আবার শুরু হয়।

Production rule:

> **একটি Signal-এর ভিতরে একই model-এর `save()` করার আগে খুব সতর্ক হতে হবে।**

---

# 6. Solution 1 — `update_fields`

ধরি আমাদের সত্যিই database-এ একটা field update করতে হবে।

```python
@receiver(post_save, sender=Product)
def update_product(sender, instance, **kwargs):

    Product.objects.filter(
        pk=instance.pk
    ).update(
        slug=slugify(instance.name)
    )
```

এখানে:

```python
QuerySet.update()
```

ব্যবহার হচ্ছে।

এটা:

```text
model.save()
```

call করে না।

তাই:

```text
post_save
   ↓
QuerySet.update()
   ↓
DB UPDATE
```

আবার `post_save` trigger হবে না।

---

# 7. কিন্তু এখানে একটা গুরুত্বপূর্ণ পার্থক্য

`update()` ব্যবহার করলে:

```text
pre_save ❌
post_save ❌
```

চলবে না।

এটা কখন useful?

যখন আমরা intentionally signal recursion avoid করতে চাই এবং direct database update চাই।

---

# 8. Solution 2 — `save(update_fields=...)`

ধরি:

```python
@receiver(pre_save, sender=Product)
def normalize_product(sender, instance, **kwargs):

    instance.name = instance.name.strip()
```

এখানে আমাদের আবার `save()` দরকার নেই।

কারণ `pre_save` already save-এর আগে চলছে।

```text
Product.save()
      ↓
pre_save
      ↓
name modify
      ↓
DB save
```

এটাই সবচেয়ে clean approach।

### Rule:

> `pre_save`-এ object modify করতে পারলে আবার `save()` করো না।

---

# 9. খুব ভালো Example — Slug

আগের slug example-টা `pre_save` দিয়ে করি।

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver
from django.utils.text import slugify


@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = slugify(instance.name)
```

এখন:

```python
product = Product.objects.create(
    name="Gaming Laptop"
)
```

Flow:

```text
save()
 ↓
pre_save
 ↓
slug তৈরি
 ↓
DB INSERT
 ↓
post_save
```

কোনো দ্বিতীয় `save()` নেই।

এটা much cleaner।

---

# 10. Solution 3 — Signal disconnect করা

Django signal manually disconnect/connect করা যায়।

যেমন:

```python
post_save.disconnect(
    product_signal,
    sender=Product
)

instance.save()

post_save.connect(
    product_signal,
    sender=Product
)
```

কিন্তু production application-এ সাধারণ business logic-এর জন্য এটা ব্যবহার করা উচিত না।

কারণ code খুব difficult to reason about হয়ে যায়।

```text
disconnect
   ↓
save
   ↓
connect
```

কোথায় disconnect হয়েছে, কোথায় reconnect হয়েছে—debug করা কঠিন।

---

# 11. Solution 4 — Guard flag

আরেকটা pattern আছে:

```python
@receiver(post_save, sender=Product)
def product_signal(sender, instance, **kwargs):

    if getattr(instance, "_signal_processed", False):
        return

    instance._signal_processed = True

    instance.some_field = "something"
    instance.save()
```

এখানে:

```python
instance._signal_processed
```

temporary Python attribute।

প্রথমবার:

```text
False
```

তারপর:

```text
True
```

দ্বিতীয় signal:

```python
if True:
    return
```

তাই recursion বন্ধ।

---

# 12. কিন্তু এটা কি best solution?

সবসময় না।

এটা কাজ করতে পারে, কিন্তু প্রশ্ন হচ্ছে:

> আমাদের কি আসলেই Signal-এর ভিতরে আবার `save()` করা দরকার?

বেশিরভাগ ক্ষেত্রে উত্তর:

**না।**

তাই আগে চেষ্টা করব:

```text
pre_save
```

অথবা:

```text
QuerySet.update()
```

অথবা:

```text
Service Layer
```

ব্যবহার করতে।

---

# 13. সবচেয়ে ভালো Pattern — `pre_save`

ধরি:

```python
class Product(models.Model):

    name = models.CharField(
        max_length=200
    )

    slug = models.SlugField(
        unique=True,
        blank=True
    )
```

আমাদের requirement:

> Name change হলে slug update হবে।

তাহলে:

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):

    instance.slug = slugify(
        instance.name
    )
```

কিন্তু এখানে একটা নতুন problem:

ধরি:

```text
name = "Gaming Laptop"
slug = "gaming-laptop"
```

পরে name:

```text
Gaming Laptop Pro
```

তখন slug:

```text
gaming-laptop-pro
```

ঠিক।

কিন্তু যদি slug manually customize করা হয়:

```text
special-gaming-laptop
```

তাহলে automatic overwrite করা উচিত না।

তাই:

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = slugify(instance.name)
```

এটা safer।

---

# 14. আরেকটা বড় সমস্যা — Signal A → Signal B → Signal A

শুধু নিজের signal নিজেকে trigger করে না।

দুইটা model-এর signal থেকেও loop হতে পারে।

ধরি:

```text
Order
Payment
```

### Order signal

```python
@receiver(post_save, sender=Order)
def order_signal(sender, instance, **kwargs):

    payment = instance.payment

    payment.status = "SUCCESS"
    payment.save()
```

### Payment signal

```python
@receiver(post_save, sender=Payment)
def payment_signal(sender, instance, **kwargs):

    order = instance.order

    order.status = "PAID"
    order.save()
```

এখন:

```text
Order save
   ↓
Order Signal
   ↓
Payment save
   ↓
Payment Signal
   ↓
Order save
   ↓
Order Signal
   ↓
Payment save
   ↓
...
```

এটাও:

```text
♾️
```

---

# 15. এটা কেন Production-এ dangerous?

E-commerce-এ:

```text
Order
Payment
Inventory
Shipment
Refund
```

সব একে অপরের সাথে related।

যদি প্রত্যেক model-এর `post_save` অন্য model update করতে থাকে:

```text
Order
 ↓
Payment
 ↓
Inventory
 ↓
Shipment
 ↓
Order
 ↓
Payment
 ↓
...
```

তাহলে application-এর behavior খুব unpredictable হয়ে যাবে।

---

# 16. এজন্য Service Layer

আমরা আগে যে architecture শিখেছি সেটা এখানে কাজে লাগবে।

ধরি payment complete করার কাজ:

```python
@transaction.atomic
def mark_order_paid(order, payment):

    payment.status = "SUCCESS"

    payment.save(
        update_fields=["status"]
    )

    order.status = "PAID"

    order.save(
        update_fields=["status"]
    )
```

এখানে কে কী update করবে সেটা explicit:

```text
PaymentService
      ↓
Payment = SUCCESS
      ↓
Order = PAID
```

তারপর:

```text
on_commit
      ↓
order_paid
      ↓
Signal
      ↓
notification / email / audit
```

এখানে Signal আর core workflow control করছে না।

---

# 17. `post_save` দিয়ে Business Workflow তৈরি করা কেন খারাপ?

ধরি:

```python
@receiver(post_save, sender=Order)
def order_signal(...):

    if instance.status == "PAID":

        payment.status = "SUCCESS"
        payment.save()

        inventory.reduce()
        shipment.create()
        send_email()
```

এখানে একটা Order save করলেই অনেক hidden action হচ্ছে।

Developer পরে:

```python
order.save()
```

করল।

কিন্তু সে জানে না যে:

```text
Payment update
Inventory decrease
Shipment create
Email
```

সব trigger হয়ে যাবে।

এটা **hidden side effect**।

---

# 18. Better Architecture

```text
                Service Layer
                     │
                     ▼
              Validate operation
                     │
                     ▼
             transaction.atomic()
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        Order      Payment    Inventory
          │
          ▼
       COMMIT
          │
          ▼
      on_commit()
          │
          ▼
     Domain Event
          │
          ▼
       Signal
      ┌───┼────┐
      ▼   ▼    ▼
    Email Audit Analytics
      │
      ▼
    Celery
```

---

# 19. আরেকটা common recursion problem

ধরি:

```python
@receiver(post_save, sender=Order)
def order_signal(sender, instance, **kwargs):

    instance.total = calculate_total(instance)

    instance.save()
```

এখানে:

```text
post_save
 ↓
calculate
 ↓
save
 ↓
post_save
 ↓
calculate
 ↓
save
 ↓
...
```

এটা avoid করতে:

```python
@receiver(pre_save, sender=Order)
def order_pre_save(sender, instance, **kwargs):

    instance.total = calculate_total(instance)
```

এটাই proper জায়গা।

---

# 20. কখন `pre_save` ব্যবহার করব?

যখন database save হওয়ার **আগে object-এর value modify** করতে হবে।

Examples:

```text
slug তৈরি
name normalize
data clean
derived field calculate
```

Example:

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):

    instance.name = instance.name.strip()

    if not instance.slug:
        instance.slug = slugify(instance.name)
```

---

# 21. কখন `post_save` ব্যবহার করব?

যখন database save হওয়ার পরে কোনো **side effect** দরকার।

Examples:

```text
Audit log
Analytics
Create profile
Simple related record
Domain event
```

Example:

```python
@receiver(post_save, sender=Product)
def product_created(sender, instance, created, **kwargs):

    if created:
        ProductAuditLog.objects.create(
            product=instance,
            action="CREATED"
        )
```

---

# 22. `post_save` → Celery হলে recursion নেই

ধরি:

```python
@receiver(post_save, sender=Order)
def order_saved(sender, instance, created, **kwargs):

    if created:
        send_order_email.delay(
            instance.id
        )
```

এখানে:

```text
post_save
 ↓
Celery task
```

Task যদি শুধু email পাঠায়:

```text
Celery
 ↓
Email
```

তাহলে Order আবার save হচ্ছে না।

তাই recursion নেই।

---

# 23. কিন্তু Celery task যদি আবার Order save করে?

ধরি:

```python
@shared_task
def process_order(order_id):

    order = Order.objects.get(
        id=order_id
    )

    order.processed = True
    order.save()
```

তাহলে:

```text
Order save
 ↓
post_save
 ↓
Celery
 ↓
Order save
 ↓
post_save
 ↓
Celery
 ↓
...
```

এখন recursion হতে পারে।

তাই task-ও signal interaction-এর অংশ।

---

# 24. একটা Safe Pattern

Signal:

```python
@receiver(post_save, sender=Order)
def order_saved(sender, instance, created, **kwargs):

    if created:
        process_order.delay(
            instance.id
        )
```

Task:

```python
@shared_task
def process_order(order_id):

    order = Order.objects.get(
        id=order_id
    )

    Order.objects.filter(
        id=order_id
    ).update(
        processed=True
    )
```

এখানে task:

```python
.update()
```

ব্যবহার করছে।

তাই:

```text
post_save ❌
```

আবার trigger হবে না।

---

# 25. কিন্তু `.update()`-এর limitation মনে রাখবে

যেহেতু:

```python
QuerySet.update()
```

signal trigger করে না:

```text
pre_save ❌
post_save ❌
```

তাই model-level logic থাকলে সেটা bypass হবে।

অর্থাৎ:

```text
update()
```

কে "recursion prevent করার magic solution" ভাববে না।

প্রথমে বুঝতে হবে:

> এই update কি সত্যিই signal bypass করা উচিত?

---

# 26. Signal Recursion Debug করার উপায়

যদি মনে হয়:

```text
signal বারবার execute হচ্ছে
```

তাহলে temporary logging:

```python
@receiver(post_save, sender=Order)
def order_signal(sender, instance, **kwargs):

    print(
        "ORDER SIGNAL:",
        instance.id,
        instance.status
    )
```

যদি terminal-এ:

```text
ORDER SIGNAL: 1 PAID
ORDER SIGNAL: 1 PAID
ORDER SIGNAL: 1 PAID
ORDER SIGNAL: 1 PAID
...
```

দেখতে পাও:

তাহলে কোথাও আবার:

```python
order.save()
```

হচ্ছে।

---

# 27. `save()` Call Graph চিনতে শিখো

এই patternটা মাথায় রাখবে:

```text
model.save()
   │
   ├── pre_save
   │
   ├── database operation
   │
   └── post_save
```

তাই:

```python
post_save
    ↓
instance.save()
```

মানে:

```text
post_save
   ↓
save()
   ↓
pre_save
   ↓
DB
   ↓
post_save
```

এটাই recursion-এর মূল কারণ।

---

# 28. আজকের Production Rules

### Rule 1

`pre_save`-এর ভিতরে সাধারণত আবার `save()` করবে না।

```python
@receiver(pre_save, sender=Product)
def product_pre_save(...):
    instance.slug = ...
```

---

### Rule 2

`post_save`-এর ভিতরে একই model-এর `save()` খুব সতর্ক হয়ে ব্যবহার করবে।

---

### Rule 3

Core business workflow Signal দিয়ে orchestrate করবে না।

খারাপ:

```text
Order Signal
 → Payment
 → Inventory
 → Shipment
```

ভালো:

```text
OrderService
 → Payment
 → Inventory
 → Shipment
```

---

### Rule 4

Signal = side effects

```text
Audit
Notification
Analytics
Email
```

---

### Rule 5

Critical state transition = Service

```text
PENDING → PAID
PAID → REFUNDED
PAID → CANCELLED
```

---

# 🧠 PART 12 Mental Model

সবচেয়ে গুরুত্বপূর্ণ diagram:

```text
                MODEL SAVE
                    │
                    ▼
                pre_save
                    │
                    │
             modify instance
                    │
                    ▼
                DATABASE
                    │
                    ▼
                post_save
                    │
                    ▼
             Side Effects
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
        Audit    Celery    Analytics
                    │
                    ▼
                  Redis


⚠️ Avoid:

post_save
   ↓
instance.save()
   ↓
post_save
   ↓
instance.save()
   ↓
∞
```

### এক লাইনে:

> **Signal-এর ভিতরে আবার `save()` করলে সেই Signal আবার fire হতে পারে; তাই object পরিবর্তনের জন্য `pre_save`, direct DB update-এর জন্য সচেতনভাবে `update()`, আর complex workflow-এর জন্য Service Layer ব্যবহার করাই safer production pattern।**

পরের ধাপে **PART 13**-এ আমরা Django Signals-এর আরেকটি খুব গুরুত্বপূর্ণ বিষয় শিখতে পারি: **`bulk_create()`, `bulk_update()`, `QuerySet.update()` কেন Signals trigger করে না এবং বড় E-commerce application-এ এর performance/consistency impact কী।**

---
# PART 13 — `bulk_create()`, `bulk_update()`, `update()` এবং Signals

আজকে Django Signals course-এর **শেষ Part**। এই Part-টা খুব গুরুত্বপূর্ণ, কারণ বড় E-commerce project-এ performance-এর জন্য আমরা প্রায়ই bulk operation ব্যবহার করি।

কিন্তু সমস্যা হলো:

> **Bulk operation সাধারণত `save()` lifecycle এবং `pre_save`/`post_save` Signals trigger করে না।**

---

## 1. Normal `save()` কী করে?

ধরি:

```python
product = Product(
    name="Laptop",
    price=50000
)

product.save()
```

Flow:

```text
product.save()
      ↓
pre_save
      ↓
Database INSERT
      ↓
post_save
```

অর্থাৎ:

```text
pre_save  ✅
post_save ✅
```

---

# 2. `QuerySet.update()`

এখন:

```python
Product.objects.filter(
    category_id=1
).update(
    price=60000
)
```

এখানে সরাসরি SQL `UPDATE` হচ্ছে।

তাই:

```text
pre_save  ❌
post_save ❌
```

Flow:

```text
QuerySet.update()
      ↓
SQL UPDATE
      ↓
Database
```

Model-এর:

```python
save()
```

call হচ্ছে না।

---

# 3. কেন Django এমন করে?

কারণ `update()` মূলত performance-এর জন্য।

ধরি:

```text
100,000 Products
```

প্রতিটা product-এর:

```python
product.price = ...
product.save()
```

করলে:

```text
100,000 model operations
```

হতে পারে।

কিন্তু:

```python
Product.objects.update(...)
```

বা filtered update করলে database একবারে অনেক row update করতে পারে।

---

# 4. `bulk_create()`

ধরি 1000টা Product তৈরি করব।

Normal approach:

```python
for i in range(1000):

    Product.objects.create(
        name=f"Product {i}",
        price=100
    )
```

প্রতিটা create-এর lifecycle চলবে:

```text
Product.save()
   ↓
pre_save
   ↓
INSERT
   ↓
post_save
```

---

## Bulk approach

```python
products = []

for i in range(1000):

    products.append(
        Product(
            name=f"Product {i}",
            price=100
        )
    )

Product.objects.bulk_create(products)
```

এটা অনেক faster হতে পারে।

কিন্তু:

```text
pre_save  ❌
post_save ❌
```

---

# 5. খুব গুরুত্বপূর্ণ Example

ধরি আমাদের Signal আছে:

```python
@receiver(post_save, sender=Product)
def create_inventory(
    sender,
    instance,
    created,
    **kwargs
):

    if created:
        Inventory.objects.create(
            product=instance
        )
```

Normal:

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

তাহলে:

```text
Product created
      ↓
post_save
      ↓
Inventory created
```

সব ঠিক।

---

কিন্তু:

```python
Product.objects.bulk_create([
    Product(name="Laptop", price=50000),
    Product(name="Phone", price=30000),
])
```

তখন:

```text
bulk_create()
      ↓
Products inserted
      ↓
post_save ❌
      ↓
Inventory ❌
```

অর্থাৎ Product আছে কিন্তু Signal-এর মাধ্যমে Inventory তৈরি হয়নি।

---

# 6. এটাই Production-এর বড় lesson

ধরি architecture:

```text
Product created
      ↓
Signal
      ↓
Inventory automatically created
```

তাহলে developer যদি পরে:

```python
bulk_create()
```

ব্যবহার করে, সে unknowingly business rule bypass করতে পারে।

তাই Signals ব্যবহার করার সময় জানতে হবে:

> **কোন operation signal trigger করে এবং কোনটা করে না।**

---

# 7. `bulk_update()`

ধরি 1000টা Product-এর price change করতে হবে।

```python
products = Product.objects.filter(
    category_id=1
)

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

এখানেও সাধারণ model save lifecycle trigger হবে না।

```text
pre_save  ❌
post_save ❌
```

---

# 8. চারটা operation একসাথে মনে রাখো

| Operation                  | `pre_save` | `post_save` |
| -------------------------- | ---------: | ----------: |
| `product.save()`           |          ✅ |           ✅ |
| `Product.objects.create()` |          ✅ |           ✅ |
| `QuerySet.update()`        |          ❌ |           ❌ |
| `bulk_create()`            |          ❌ |           ❌ |
| `bulk_update()`            |          ❌ |           ❌ |

এটা খুব ভালোভাবে মনে রাখবে।

---

# 9. `bulk_delete` নিয়ে একটা important point

এখানে একটু nuance আছে।

যেমন:

```python
Product.objects.filter(
    category_id=1
).delete()
```

Django-এর deletion framework সাধারণভাবে `pre_delete` এবং `post_delete` signals dispatch করতে পারে।

অর্থাৎ:

```text
QuerySet.delete()
      ↓
pre_delete
      ↓
DELETE
      ↓
post_delete
```

তাই `delete()`-কে `update()` বা `bulk_create()`-এর মতো signal-free ভাববে না।

তবে বড় deletion-এর ক্ষেত্রে performance এবং cascading behavior অবশ্যই বুঝে ব্যবহার করতে হবে।

---

# 10. তাহলে Bulk operation-এর সাথে Signal-এর কাজ কীভাবে করব?

ধরি আমাদের requirement:

```text
1000 Product create
+
1000 Inventory create
```

একটা option:

```python
products = Product.objects.bulk_create(
    products
)
```

তারপর manually:

```python
inventories = [
    Inventory(product=product)
    for product in products
]

Inventory.objects.bulk_create(
    inventories
)
```

এটা অনেক বেশি efficient হতে পারে।

```text
bulk_create Products
        ↓
bulk_create Inventories
```

এখানে Signal-এর ওপর depend করছি না।

---

# 11. Service Layer এখানে খুব useful

ধরি:

```python
def bulk_create_products(product_data):

    products = [
        Product(
            name=data["name"],
            price=data["price"]
        )
        for data in product_data
    ]

    products = Product.objects.bulk_create(
        products
    )

    inventories = [
        Inventory(product=product)
        for product in products
    ]

    Inventory.objects.bulk_create(
        inventories
    )

    return products
```

এখন workflow explicit:

```text
Bulk Product Creation Service
          ↓
bulk_create Product
          ↓
bulk_create Inventory
```

কোনো hidden Signal dependency নেই।

---

# 12. Transaction-এর সাথে ব্যবহার

Production-এ আরও ভালো:

```python
from django.db import transaction


@transaction.atomic
def bulk_create_products(product_data):

    products = [
        Product(
            name=data["name"],
            price=data["price"]
        )
        for data in product_data
    ]

    products = Product.objects.bulk_create(
        products
    )

    inventories = [
        Inventory(product=product)
        for product in products
    ]

    Inventory.objects.bulk_create(
        inventories
    )

    return products
```

এখন:

```text
transaction.atomic()
       │
       ├── Product bulk_create
       │
       └── Inventory bulk_create
       
       ↓
     COMMIT
```

কোনো একটা অংশ fail করলে transaction rollback হতে পারে।

---

# 13. Bulk operation + `on_commit()`

যদি bulk operation শেষ হওয়ার পরে notification/event দরকার হয়:

```python
@transaction.atomic
def bulk_create_products(product_data):

    products = Product.objects.bulk_create(
        [
            Product(
                name=data["name"],
                price=data["price"]
            )
            for data in product_data
        ]
    )

    transaction.on_commit(
        lambda: products_created.send(
            sender=Product,
            products=products
        )
    )

    return products
```

Flow:

```text
bulk_create
    ↓
transaction
    ↓
COMMIT
    ↓
on_commit
    ↓
custom signal
```

এটা আগের Part 8-এর concept-এর সাথে যুক্ত।

---

# 14. `bulk_update()`-এর ক্ষেত্রেও একই বিষয়

ধরি:

```python
products = list(
    Product.objects.filter(
        category_id=1
    )
)

for product in products:
    product.price += 100

Product.objects.bulk_update(
    products,
    ["price"]
)
```

এখানে:

```text
1000 products
      ↓
bulk_update
      ↓
DB
```

কিন্তু:

```text
post_save ❌
```

তাই যদি price change-এর পরে কোনো business action দরকার হয়, সেটা আলাদাভাবে handle করতে হবে।

---

# 15. একটি common mistake

অনেকে ভাবেন:

```python
Product.objects.bulk_update(...)
```

করার পরে:

```python
@receiver(post_save, sender=Product)
```

automatically কাজ করবে।

**করবে না।**

এটাই আজকের সবচেয়ে গুরুত্বপূর্ণ বিষয়গুলোর একটি।

---

# 16. E-commerce Example

ধরি Black Friday।

আমাদের:

```text
50,000 Products
```

এর price 20% discount করতে হবে।

Normal:

```python
for product in Product.objects.all():

    product.price *= Decimal("0.80")

    product.save()
```

সমস্যা:

```text
50,000 save()
50,000 signal lifecycle
অনেক database operation
```

---

Better approach:

```python
from django.db.models import F, DecimalField, ExpressionWrapper
```

তারপর database-side update করা যায়।

ধারণাটা:

```python
Product.objects.update(
    price=ExpressionWrapper(
        F("price") * Decimal("0.80"),
        output_field=DecimalField(
            max_digits=10,
            decimal_places=2
        )
    )
)
```

এখানে model save না হওয়ায়:

```text
post_save ❌
```

কিন্তু performance অনেক ভালো হতে পারে।

তাই আগে সিদ্ধান্ত নিতে হবে:

> এই price change-এর জন্য কি কোনো Signal-based side effect mandatory?

যদি হয়, তাহলে bulk update architecture আলাদা করে design করতে হবে।

---

# 17. Signal dependency থাকলে কী সমস্যা?

ধরি:

```python
@receiver(post_save, sender=Product)
def update_search_index(...):
    ...
```

Normal:

```python
product.save()
```

Search index update হবে।

কিন্তু:

```python
Product.objects.update(...)
```

করলে:

```text
Product price changed
       ↓
post_save ❌
       ↓
Search index update ❌
```

Database-এর price এবং search index-এর data mismatch হতে পারে।

এটা production-এর serious issue হতে পারে।

---

# 18. তাহলে Production Architecture কী?

Critical data synchronization-এর জন্য:

```text
Service Layer
     ↓
Database operation
     ↓
Explicit domain event
     ↓
on_commit()
     ↓
Celery / Signal
```

অর্থাৎ:

```text
Bulk Update
    ↓
Update database
    ↓
Create "products_price_updated" event
    ↓
COMMIT
    ↓
Celery
    ↓
Search index update
```

এটা hidden Signal dependency-এর চেয়ে predictable।

---

# 19. Signals কখন ব্যবহার করব?

Signals খুব useful:

### Simple automatic side effects

```text
User created
    ↓
Profile create
```

```text
Product created
    ↓
Audit log
```

```text
Order paid
    ↓
Notification
```

```text
Payment completed
    ↓
Analytics event
```

---

# 20. Signals কখন ব্যবহার করব না?

বিশেষ করে এগুলো Signal-এর ভিতরে hide করা উচিত না:

```text
Order cancellation
Payment processing
Refund
Inventory reservation
Inventory release
Shipping workflow
Return
Exchange
Payment reconciliation
Complex state machine
```

এসব:

```text
Service Layer
```

এ explicit হওয়া ভালো।

---

# 21. পুরো Signal Course-এর Final Architecture

এখন Part 1 → Part 13 সব একসাথে দেখি।

```text
                     Django / DRF
                          │
                          ▼
                    API / Admin
                          │
                          ▼
                     Serializer
                          │
                          ▼
                    View / Service
                          │
                          ▼
              ┌─────────────────────┐
              │   Business Logic    │
              │                     │
              │ Order               │
              │ Payment             │
              │ Inventory           │
              │ Refund              │
              │ Return              │
              └─────────────────────┘
                          │
                          ▼
                  transaction.atomic()
                          │
                          ▼
                      Database
                          │
              ┌───────────┴───────────┐
              │                       │
          pre_save                post_save
              │                       │
        Modify data              Side effects
                                      │
                                      ▼
                               on_commit()
                                      │
                                      ▼
                              Domain Signal
                                      │
                       ┌──────────────┼──────────────┐
                       ▼              ▼              ▼
                     Audit        Notification    Analytics
                                      │
                                      ▼
                                    Celery
                                      │
                                      ▼
                                    Redis
                                      │
                                      ▼
                                   Worker
```

---

# 22. Signal Course-এর 13 Parts এক নজরে

| Part   | Topic                                    |
| ------ | ---------------------------------------- |
| 1      | Signal Fundamentals                      |
| 2      | `pre_save` vs `post_save`                |
| 3      | `pre_delete` vs `post_delete`            |
| 4      | `m2m_changed`                            |
| 5      | Custom Signals                           |
| 6      | DRF Serializer + Signals                 |
| 7      | Signal + Service Layer                   |
| 8      | `transaction.atomic()` + `on_commit()`   |
| 9      | Signal + Celery + Redis                  |
| 10     | Registration, `dispatch_uid`, Testing    |
| 11     | Old Value → New Value / State Transition |
| 12     | Recursion / Infinite Loop                |
| **13** | **Bulk Operations + Signals**            |

---

# 🧠 Final Mental Model

সবচেয়ে গুরুত্বপূর্ণভাবে এটা মনে রাখবে:

```text
Signal ≠ Business Logic
```

বরং:

```text
Service
   ↓
Make something happen
```

আর:

```text
Signal
   ↓
Something happened
```

### উদাহরণ:

```text
PaymentService
      ↓
PENDING → PAID
      ↓
COMMIT
      ↓
order_paid
      ↓
Signal
      ├── Audit
      ├── Notification
      ├── Analytics
      └── Celery Email
```

আর bulk operation:

```text
bulk_create()
bulk_update()
QuerySet.update()
        ↓
Normal save signals ❌
```

তাই production system-এ **Signal-এর ওপর critical business workflow-এর dependency তৈরি করবে না।**

---

## 🎯 পুরো Django Signals Course শেষ

তোমার এখন Django Signals-এর beginner থেকে production-level core concepts জানা উচিত:

**Lifecycle → Custom Signal → DRF → Service → Transaction → `on_commit` → Celery → State Transition → Recursion → Bulk Operations।**

তোমার E-commerce project-এর ক্ষেত্রে সবচেয়ে ভালো rule হবে:

> **Order/Payment/Inventory state transition → Service Layer**
> **Committed event → Domain Signal**
> **Heavy side effect → Celery**
> **Database consistency → `transaction.atomic()`**
> **Post-commit action → `transaction.on_commit()`**
> **Large-scale data operation → Bulk QuerySet operations, but never assume Signals will run.**


---
