DRF project-এ **Django Signal** মূলত ব্যবহার করা হয়—একটা model/database event ঘটলে **automatically অন্য কোনো কাজ trigger করার জন্য**।

সবচেয়ে common example:

```text
User create
   ↓
Signal automatically run
   ↓
Profile create
```

DRF-এর নিজস্ব signal না; এটা **Django-এর signal system**। DRF API দিয়ে User create হলেও model save হওয়ার সময় Django signal কাজ করতে পারে।

## 1. Example: User তৈরি হলে Profile automatically তৈরি

ধরি:

```text
accounts/
├── models.py
├── signals.py
├── apps.py
└── views.py
```

### `models.py`

```python
from django.db import models
from django.contrib.auth.models import AbstractUser


class User(AbstractUser):
    email = models.EmailField(unique=True)


class Profile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="profile"
    )
    phone = models.CharField(max_length=20, blank=True)
    address = models.TextField(blank=True)
```

এখন চাই:

```text
POST /api/users/

User created
      ↓
Profile automatically created
```

---

## 2. `signals.py`

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import User, Profile


@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):

    if created:
        Profile.objects.create(user=instance)
```

এখানে:

```python
@receiver(post_save, sender=User)
```

মানে:

> User model-এর `save()` হওয়ার পরে এই function-টা চালাও।

আর:

```python
if created:
```

মানে:

> User নতুন করে তৈরি হলে শুধু Profile বানাও।

কারণ existing User update হলেও `post_save` trigger হয়।

---

# 3. Signal register করতে হবে

এখানে beginners-দের একটা common mistake হয়।

শুধু `signals.py` বানালেই সবসময় যথেষ্ট নয়। App load হওয়ার সময় signal module import/register করানো ভালো practice।

`apps.py`:

```python
from django.apps import AppConfig


class AccountsConfig(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "accounts"

    def ready(self):
        import accounts.signals
```

তারপর `settings.py`-এ app config ব্যবহার:

```python
INSTALLED_APPS = [
    # ...
    "accounts.apps.AccountsConfig",
]
```

---

# 4. এখন DRF API থেকে User create করলে

ধরো serializer:

```python
from rest_framework import serializers
from .models import User


class UserSerializer(serializers.ModelSerializer):

    class Meta:
        model = User
        fields = [
            "id",
            "username",
            "email",
            "password",
        ]

    def create(self, validated_data):
        password = validated_data.pop("password")

        user = User(**validated_data)
        user.set_password(password)
        user.save()

        return user
```

API:

```text
POST /api/users/
```

Body:

```json
{
    "username": "atiar",
    "email": "atiar@example.com",
    "password": "123456"
}
```

`user.save()` হওয়ার সময়:

```text
UserSerializer
      ↓
user.save()
      ↓
post_save signal
      ↓
create_user_profile()
      ↓
Profile.objects.create()
```

অর্থাৎ তোমার View/Serializer-এ আলাদাভাবে:

```python
Profile.objects.create(...)
```

লিখতে হচ্ছে না।

---

# 5. `pre_save` বনাম `post_save`

দুইটা খুব গুরুত্বপূর্ণ signal:

### `pre_save`

Save হওয়ার **আগে**:

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):
    ...
```

Flow:

```text
product.save()
    ↓
pre_save
    ↓
Database save
```

### `post_save`

Save হওয়ার **পরে**:

```python
@receiver(post_save, sender=Product)
def product_post_save(sender, instance, created, **kwargs):
    ...
```

Flow:

```text
product.save()
    ↓
Database save
    ↓
post_save
```

---

# 6. E-commerce project-এ Signal কোথায় useful?

তোমার e-commerce project ধরলে:

### User → Profile

```text
User created
    ↓
Profile created
```

### Product → slug

Product save হওয়ার আগে slug generate করা যেতে পারে।

### Order → notification

Order তৈরি হলে notification তৈরি করা যেতে পারে।

### Review → something

Review তৈরি হলে related aggregate/cache update করা যেতে পারে।

তবে এখানে একটা গুরুত্বপূর্ণ production rule আছে।

## Signal সব জায়গায় ব্যবহার করবে না

Signal-এর কারণে code-এর behavior **hidden** হয়ে যায়।

ধরো:

```python
order.save()
```

দেখে developer ভাবতে পারে শুধু Order save হচ্ছে।

কিন্তু পিছনে:

```text
order.save()
   ↓
signal
   ↓
inventory update
   ↓
notification
   ↓
email
```

হতে পারে।

তাই **simple automatic model-related behavior**-এর জন্য signal ভালো।

কিন্তু বড় business workflow হলে সাধারণত service layer বেশি পরিষ্কার:

```text
OrderService
    ↓
Create Order
    ↓
Update Inventory
    ↓
Create Payment
    ↓
Send Notification
```

---

## 7. একটা গুরুত্বপূর্ণ ভুল

Signal-এর মধ্যে একই model আবার save করলে recursion হতে পারে।

যেমন:

```python
@receiver(post_save, sender=Product)
def update_product(sender, instance, **kwargs):
    instance.save()
```

এটা dangerous:

```text
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
...
```

তাই signal লিখার সময় **signal-এর ভিতর আবার একই model-এর save** করলে বিশেষভাবে সাবধান হতে হবে।

---

### তোমার জন্য মনে রাখার formula

```text
Django Model Event
       ↓
pre_save
post_save
pre_delete
post_delete
       ↓
Signal Handler
       ↓
Automatic Side Effect
```

আর DRF-এ:

```text
React
 ↓
DRF API
 ↓
Serializer
 ↓
Model.save()
 ↓
Django Signal
 ↓
Automatic Action
```

**তুমি যেহেতু e-commerce/DRF production architecture শিখছো, পরের ধাপে `Order + OrderItem + Product stock` নিয়ে signal বনাম service layer—কখন কোনটা ব্যবহার করা উচিত—এই real-world example-টা শেখা সবচেয়ে useful হবে।**

---
অবশ্যই। Django Signal ভালোভাবে বুঝতে হলে আগে একটা জিনিস মাথায় রাখো:

> **Signal হলো Django-এর event system — কোনো নির্দিষ্ট event ঘটলে অন্য একটি function automatically চালানো।**

DRF project-এও এগুলো ব্যবহার করা যায়, কারণ DRF শেষ পর্যন্ত Django model/database-এর উপরই কাজ করে।

---

# 1. Django-তে কত ধরনের Signal আছে?

Django-র built-in signals অনেকগুলো। তবে তোমার **DRF/backend development**-এর জন্য আগে এইগুলো ভালোভাবে জানলেই যথেষ্ট:

|Signal|কখন চলে?|Common use|
|---|---|---|
|`pre_save`|Model save হওয়ার আগে|data modify/validate|
|`post_save`|Model save হওয়ার পরে|Profile/create related data|
|`pre_delete`|Delete হওয়ার আগে|cleanup/check|
|`post_delete`|Delete হওয়ার পরে|file/cache cleanup|
|`m2m_changed`|ManyToMany change হলে|relationship-related action|
|`pre_init`|Model instance তৈরি হওয়ার আগে|advanced use|
|`post_init`|Model instance তৈরি হওয়ার পরে|advanced use|

আর authentication-এর জন্য:

|Signal|কখন|
|---|---|
|`user_logged_in`|User login করলে|
|`user_logged_out`|User logout করলে|
|`user_login_failed`|Login fail করলে|

এখন একে একে দেখি।

---

# 2. `pre_save`

### কখন ব্যবহার করবে?

কোনো Model database-এ save হওয়ার **আগে** কিছু করতে চাইলে।

```text
product.save()
     ↓
pre_save
     ↓
database save
```

### Example: Product slug তৈরি

```python
from django.db.models.signals import pre_save
from django.dispatch import receiver

from .models import Product


@receiver(pre_save, sender=Product)
def create_product_slug(sender, instance, **kwargs):

    if not instance.slug:
        instance.slug = instance.name.lower().replace(" ", "-")
```

ধরো:

```python
product.name = "iPhone 17"
product.save()
```

Signal-এর কারণে:

```text
name
 ↓
iPhone 17

slug
 ↓
iphone-17
```

তারপর database-এ save হবে।

### কখন `pre_save`?

যখন **save হওয়ার আগে instance পরিবর্তন করতে হবে**।

উদাহরণ:

- slug generate
    
- কিছু field automatically set
    
- save-এর আগে normalization
    
- derived field calculate
    

---

# 3. `post_save`

এটা সবচেয়ে বেশি ব্যবহৃত signal-এর একটি।

### কখন?

Model save হওয়ার **পরে**।

```text
product.save()
     ↓
Database save
     ↓
post_save
```

### Example: User তৈরি হলে Profile তৈরি

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import User, Profile


@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):

    if created:
        Profile.objects.create(user=instance)
```

এখানে:

```python
created
```

খুব গুরুত্বপূর্ণ।

যদি নতুন User:

```text
created = True
```

আর existing User update:

```text
created = False
```

তাই:

```python
if created:
```

দিয়ে শুধু নতুন User-এর জন্য Profile বানাচ্ছি।

### Use cases

```text
User create
    ↓
Profile create

Order create
    ↓
Notification create

Product create
    ↓
Search index update
```

---

# 4. `pre_delete`

Model delete হওয়ার **আগে** চলে।

```text
product.delete()
      ↓
pre_delete
      ↓
database delete
```

### Example

ধরো Product-এর সাথে একটা image file আছে।

Delete করার আগে কিছু cleanup করতে চাই:

```python
from django.db.models.signals import pre_delete
from django.dispatch import receiver

from .models import Product


@receiver(pre_delete, sender=Product)
def product_before_delete(sender, instance, **kwargs):

    print(
        f"Deleting product: {instance.name}"
    )
```

### কখন useful?

যখন delete হওয়ার আগে information দরকার।

যেমন:

```text
Product delete
      ↓
check something
      ↓
cleanup
      ↓
delete
```

---

# 5. `post_delete`

এটা delete হওয়ার **পরে** চলে।

```text
product.delete()
      ↓
database delete
      ↓
post_delete
```

Example:

```python
from django.db.models.signals import post_delete
from django.dispatch import receiver

from .models import Product


@receiver(post_delete, sender=Product)
def product_deleted(sender, instance, **kwargs):

    print(
        f"Product deleted: {instance.id}"
    )
```

### Common use

```text
Database object deleted
        ↓
Delete associated file
        ↓
Delete cache
        ↓
Cleanup external resource
```

---

# 6. `m2m_changed`

এটা একটু interesting।

Many-to-Many relationship change হলে চলে।

ধরো:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    categories = models.ManyToManyField(Category)
```

এখন:

```python
product.categories.add(category)
```

বা:

```python
product.categories.remove(category)
```

বা:

```python
product.categories.clear()
```

হলে `m2m_changed` trigger হতে পারে।

### Example

```python
from django.db.models.signals import m2m_changed
from django.dispatch import receiver

from .models import Product


@receiver(
    m2m_changed,
    sender=Product.categories.through
)
def product_category_changed(
    sender,
    instance,
    action,
    **kwargs
):

    print(
        f"Product: {instance.name}"
    )

    print(
        f"Action: {action}"
    )
```

`action` বিভিন্ন value হতে পারে:

```text
pre_add
post_add

pre_remove
post_remove

pre_clear
post_clear
```

যেমন:

```python
product.categories.add(category)
```

flow:

```text
pre_add
   ↓
relationship add
   ↓
post_add
```

### কখন ব্যবহার করবে?

যখন ManyToMany relationship পরিবর্তনের উপর কিছু করতে হবে।

---

# 7. `pre_init`

এটা advanced signal।

Model instance তৈরি হওয়ার **আগে**।

```python
from django.db.models.signals import pre_init
```

যেমন:

```python
@receiver(pre_init, sender=Product)
def product_pre_init(
    sender,
    *args,
    **kwargs
):
    print("Product instance is about to initialize")
```

কিন্তু সাধারণ DRF project-এ এটা খুব কম লাগবে।

---

# 8. `post_init`

Model instance তৈরি হওয়ার পরে।

```python
from django.db.models.signals import post_init
```

Example:

```python
@receiver(post_init, sender=Product)
def product_initialized(
    sender,
    instance,
    **kwargs
):
    print(
        f"Product initialized: {instance.name}"
    )
```

এটাও advanced use।

---

# 9. Authentication Signals

DRF project-এ এগুলোও useful।

Django-এর:

```python
user_logged_in
user_logged_out
user_login_failed
```

---

## `user_logged_in`

User successfully login করলে।

```python
from django.contrib.auth.signals import user_logged_in
from django.dispatch import receiver


@receiver(user_logged_in)
def user_login_handler(
    sender,
    request,
    user,
    **kwargs
):
    print(
        f"{user.email} logged in"
    )
```

Useful for:

```text
Login
 ↓
audit log
 ↓
login history
```

---

# 10. `user_logged_out`

Logout করলে।

```python
from django.contrib.auth.signals import user_logged_out
from django.dispatch import receiver


@receiver(user_logged_out)
def user_logout_handler(
    sender,
    request,
    user,
    **kwargs
):
    if user:
        print(
            f"{user.email} logged out"
        )
```

---

# 11. `user_login_failed`

Login failed হলে।

```python
from django.contrib.auth.signals import user_login_failed
from django.dispatch import receiver


@receiver(user_login_failed)
def login_failed_handler(
    sender,
    credentials,
    request,
    **kwargs
):
    print(
        "Login attempt failed"
    )
```

এটা useful হতে পারে:

```text
Failed login
     ↓
Audit log
     ↓
Security monitoring
```

তবে sensitive credentials log করা যাবে না।

---

# 12. তোমার E-commerce project দিয়ে সবগুলো চিন্তা করো

ধরো:

```text
User
Category
Product
Order
OrderItem
Review
ProductImage
```

### User

```text
User.save()
    ↓
post_save
    ↓
Profile create
```

### Product

```text
Product.save()
    ↓
pre_save
    ↓
slug generate
```

### Product delete

```text
Product.delete()
    ↓
pre_delete
    ↓
cleanup/check
    ↓
delete
    ↓
post_delete
    ↓
cache/file cleanup
```

### Product + Category

```text
product.categories.add(category)
       ↓
m2m_changed
       ↓
update something
```

### Login

```text
login
 ↓
user_logged_in
 ↓
login history
```

---

# 13. Signal কোথায় রাখবে?

আমি সাধারণত এভাবে রাখব:

```text
products/
│
├── models.py
├── serializers.py
├── views.py
├── urls.py
├── signals.py
└── apps.py
```

`signals.py`:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Product


@receiver(post_save, sender=Product)
def product_created(sender, instance, created, **kwargs):

    if created:
        print(
            f"New product: {instance.name}"
        )
```

`apps.py`:

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):

    default_auto_field = (
        "django.db.models.BigAutoField"
    )

    name = "products"

    def ready(self):
        import products.signals
```

`settings.py`:

```python
INSTALLED_APPS = [
    # ...

    "products.apps.ProductsConfig",
]
```

এতে Django app load করার সময় `signals.py` import হবে এবং receivers register হবে।

---

# 14. Signal-এর সবচেয়ে গুরুত্বপূর্ণ limitation

এটা খুব ভালোভাবে বুঝবে।

ধরো:

```python
Product.objects.bulk_create(products)
```

অনেক ক্ষেত্রে তুমি আশা করতে পারো:

```text
bulk_create
 ↓
post_save
 ↓
signal
```

কিন্তু **`bulk_create()` `save()` call করে না, তাই `pre_save`/`post_save` signal সাধারণভাবে trigger করে না।**

একইভাবে:

```python
QuerySet.update()
```

এটাও individual model `save()` চালায় না, তাই `pre_save`/`post_save` পাবে না।

তাই:

```text
product.save()
      ↓
pre_save
post_save
```

কিন্তু:

```text
Product.objects.bulk_create(...)
      ↓
pre_save/post_save ❌
```

এটা production-এ খুব গুরুত্বপূর্ণ।

---

# 15. Signal কখন ব্যবহার করবে?

এই rule মনে রাখো:

### Signal ভালো:

```text
Model event
   ↓
Small automatic side effect
```

যেমন:

```text
User created
 ↓
Create Profile
```

### Signal এড়িয়ে যাও:

যদি বড় business workflow হয়:

```text
Order
 ↓
Payment
 ↓
Inventory
 ↓
Coupon
 ↓
Shipping
 ↓
Notification
 ↓
Email
```

এগুলো signal-এর মধ্যে লুকিয়ে দিলে debugging কঠিন হতে পারে।

এর বদলে:

```text
OrderService
     ↓
Create Order
     ↓
Update Inventory
     ↓
Create Payment
     ↓
Notification
```

এভাবে explicit service layer অনেক পরিষ্কার।

---

# 16. Beginner হিসেবে তোমার আগে কোনগুলো শিখবে?

আমি এই order-এ শেখার পরামর্শ দেব:

```text
Phase 1
├── pre_save
└── post_save

Phase 2
├── pre_delete
└── post_delete

Phase 3
└── m2m_changed

Phase 4
├── user_logged_in
├── user_logged_out
└── user_login_failed

Phase 5
└── Signal vs Service Layer
```

সবচেয়ে আগে **`post_save` + `pre_save`** ভালোভাবে আয়ত্ত করো। এগুলো দিয়েই তোমার DRF project-এর অনেক real-world কাজ বুঝে যাবে।