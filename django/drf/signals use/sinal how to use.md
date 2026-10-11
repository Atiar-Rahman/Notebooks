**Signal-এর structure** পরিষ্কারভাবে বুঝি। তারপর একে একে `pre_save`, `post_save`, `pre_delete`, `post_delete`, `m2m_changed`, custom signal—সব করব।

## 1. Signal আসলে কী?

Django Signal হলো এমন একটি mechanism যেখানে **কোনো নির্দিষ্ট event ঘটলে automatically অন্য একটা function চালানো যায়।**

উদাহরণ:

```text
Product তৈরি হলো
       ↓
post_save signal trigger
       ↓
আমাদের function automatically execute
```

DRF এখানে সরাসরি Signal চালায় না। DRF API → Django Model operation → Signal trigger হয়।

---

# 2. Signal তৈরি করার basic structure

সাধারণত app-এর ভিতরে `signals.py` তৈরি করি:

```text
products/
├── models.py
├── serializers.py
├── views.py
├── signals.py      ← এখানে
├── apps.py
└── urls.py
```

`signals.py`:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver
```

তারপর:

```python
@receiver(post_save, sender=Product)
def my_signal(sender, instance, created, **kwargs):
    pass
```

এখানে কয়েকটা গুরুত্বপূর্ণ জিনিস আছে।

---

# 3. `@receiver()` কী?

```python
@receiver(post_save, sender=Product)
```

এর অর্থ:

> `Product` model-এর `post_save` event ঘটলে নিচের function-টা চালাও।

এখানে:

```python
post_save
```

হলো **কোন event-এর জন্য অপেক্ষা করছি**।

আর:

```python
sender=Product
```

হলো **কোন model-এর event-এর জন্য অপেক্ষা করছি**।

---

# 4. Signal function-এর ভিতরে কী থাকে?

সাধারণ structure:

```python
@receiver(post_save, sender=Product)
def product_signal(sender, instance, created, **kwargs):

    if created:
        # নতুন Product তৈরি হলে এখানে code
        pass
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

### `sender`

```python
sender
```

কোন model signal পাঠিয়েছে।

আমাদের ক্ষেত্রে:

```python
Product
```

---

### `instance`

```python
instance
```

যে object-এর উপর event ঘটেছে।

যেমন:

```python
product = Product.objects.create(
    name="iPhone",
    price=100000
)
```

তখন signal-এর মধ্যে:

```python
instance
```

হবে সেই `Product` object।

অর্থাৎ:

```python
instance.name
instance.price
instance.id
```

ব্যবহার করতে পারবে।

---

### `created`

`post_save`-এর ক্ষেত্রে খুব গুরুত্বপূর্ণ।

```python
created
```

হবে:

```text
True  → নতুন object তৈরি হয়েছে
False → existing object update হয়েছে
```

তাই:

```python
if created:
    print("New product created")
else:
    print("Existing product updated")
```

---

### `**kwargs`

Django signal-এর অতিরিক্ত information এখানে আসে।

সাধারণত আমরা এটা রাখি:

```python
**kwargs
```

যাতে Django যে additional arguments পাঠায় সেগুলো receive করা যায়।

---

# 5. প্রথম real example

ধরো:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

এখন:

```python
@receiver(post_save, sender=Product)
def product_created(sender, instance, created, **kwargs):

    if created:
        print("Product created:", instance.name)
```

DRF থেকে:

```http
POST /api/products/
```

```json
{
    "name": "iPhone",
    "price": 100000
}
```

তখন:

```text
DRF
 ↓
Serializer
 ↓
Product.objects.create()
 ↓
Product saved
 ↓
post_save
 ↓
product_created()
```

---

# 6. Signal-এর প্রধান types

Django-তে কয়েকটি খুব গুরুত্বপূর্ণ built-in signal আছে।

### ① `pre_save`

Object database-এ save **হওয়ার আগে** চলে।

```python
@receiver(pre_save, sender=Product)
def product_pre_save(sender, instance, **kwargs):
    pass
```

Flow:

```text
Product.save()
    ↓
pre_save
    ↓
Database save
```

---

### ② `post_save`

Object database-এ save **হওয়ার পরে** চলে।

```python
@receiver(post_save, sender=Product)
def product_post_save(sender, instance, created, **kwargs):
    pass
```

Flow:

```text
Product.save()
    ↓
Database save
    ↓
post_save
```

E-commerce example:

```text
New Product
    ↓
post_save
    ↓
Inventory create
```

---

### ③ `pre_delete`

Object delete হওয়ার **আগে** চলে।

```python
@receiver(pre_delete, sender=Product)
def product_pre_delete(sender, instance, **kwargs):
    pass
```

Flow:

```text
Product.delete()
    ↓
pre_delete
    ↓
Database delete
```

---

### ④ `post_delete`

Object delete হওয়ার **পরে** চলে।

```python
@receiver(post_delete, sender=Product)
def product_post_delete(sender, instance, **kwargs):
    pass
```

Flow:

```text
Product.delete()
    ↓
Database delete
    ↓
post_delete
```

---

### ⑤ `m2m_changed`

Many-to-Many relationship change হলে চলে।

ধরো:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    categories = models.ManyToManyField(Category)
```

তারপর:

```python
product.categories.add(category)
```

বা:

```python
product.categories.remove(category)
```

তখন:

```python
m2m_changed
```

trigger হতে পারে।

---

# 7. Custom Signal

Django-এর built-in signal ছাড়াও তুমি নিজের signal তৈরি করতে পারো।

যেমন:

```text
Order paid
   ↓
Custom signal
   ↓
Send notification
```

`signals.py` বা আলাদা `events.py`:

```python
from django.dispatch import Signal

order_paid = Signal()
```

তারপর receiver:

```python
@receiver(order_paid)
def handle_order_paid(sender, order, **kwargs):
    print("Order paid:", order.id)
```

আর যেখানে payment successful:

```python
order_paid.send(
    sender=Order,
    order=order
)
```

এটা **custom event system** হিসেবে কাজ করতে পারে।

---

# 8. Signal কোথায় register করব?

এটা খুব গুরুত্বপূর্ণ।

`apps.py`:

```python
from django.apps import AppConfig


class ProductsConfig(AppConfig):

    default_auto_field = "django.db.models.BigAutoField"

    name = "products"

    def ready(self):
        import products.signals
```

এখানে:

```python
def ready(self):
    import products.signals
```

এর মাধ্যমে Django-কে বলা হচ্ছে:

> App load হওয়ার সময় আমার signals-গুলোও load করো।

---

# 9. তাহলে একটি Signal-এর basic anatomy

এটা মনে রাখো:

```python
@receiver(SIGNAL_TYPE, sender=MODEL)
def SIGNAL_FUNCTION(sender, instance, **kwargs):

    # তোমার কাজ
    pass
```

`post_save` হলে:

```python
@receiver(post_save, sender=Product)
def product_created(sender, instance, created, **kwargs):

    if created:
        # নতুন Product
        pass
```

---

# 10. আমাদের পুরো Signal course

আমরা এই order-এ শিখলে সবচেয়ে ভালো হবে:

```text
PART 1
Signal কী
    ↓
signals.py
    ↓
@receiver
    ↓
sender
    ↓
instance
    ↓
created

PART 2
pre_save
    ↓
post_save

PART 3
pre_delete
    ↓
post_delete

PART 4
m2m_changed

PART 5
Custom Signal

PART 6
Signal + DRF Serializer

PART 7
Signal + Service Layer

PART 8
Signal-এর সমস্যা
    ↓
Recursive signals
    ↓
Duplicate execution
    ↓
Transaction সমস্যা
    ↓
Performance সমস্যা

PART 9
কখন Signal ব্যবহার করব না

PART 10
Production E-commerce
    ↓
User → Profile
Product → Inventory
Order → OrderHistory
Payment → AuditLog
Order → Notification
```

সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো **শুধু syntax মুখস্থ না করে event flow বোঝা**:

```text
EVENT
  ↓
SIGNAL
  ↓
RECEIVER FUNCTION
  ↓
BUSINESS ACTION
```

এর পর আমরা **`pre_save` বনাম `post_save`** হাতে-কলমে `Product → Inventory` example দিয়ে শুরু করতে পারি।


----
অবশ্যই। তুমি যদি Profile-এর **কোনো field required** রাখতে চাও, তাহলে মূল বিষয় হলো `blank=True` এবং `null=True` কীভাবে ব্যবহার করছো সেটা।

### ১. Required field বানাতে

ধরো `phone` অবশ্যই দিতে হবে:

```python
class Profile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="profile"
    )

    phone = models.CharField(
        max_length=20
    )

    address = models.TextField(
        blank=True,
        null=True
    )

    date_of_birth = models.DateField(
        blank=True,
        null=True
    )

    avatar = models.ImageField(
        upload_to="profiles/",
        blank=True,
        null=True
    )
```

এখানে:

```python
phone = models.CharField(max_length=20)
```

মানে `phone` required।

---

### ২. `blank=True` কী করে?

Django form/serializer validation-এর ক্ষেত্রে `blank=True` মানে field খালি রাখা যাবে।

```python
phone = models.CharField(
    max_length=20,
    blank=True
)
```

→ phone optional.

আর:

```python
phone = models.CharField(
    max_length=20
)
```

→ phone required.

---

### ৩. `null=True` কী করে?

Database level-এ `NULL` রাখা যাবে কিনা সেটা নির্ধারণ করে।

```python
phone = models.CharField(
    max_length=20,
    null=True,
    blank=True
)
```

মানে:

```text
API validation → খালি দেওয়া যাবে
Database → NULL রাখা যাবে
```

---

## কিন্তু তোমার User + Profile registration-এ একটা গুরুত্বপূর্ণ বিষয় আছে

ধরো:

```python
class Profile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="profile"
    )

    phone = models.CharField(max_length=20)  # REQUIRED

    address = models.TextField(blank=True, null=True)
```

কিন্তু registration API-তে তুমি শুধু:

```json
{
    "username": "atiar",
    "email": "atiar@example.com",
    "password": "123456"
}
```

দিচ্ছো।

তখন signal:

```python
@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
```

`phone` required হওয়ায় সমস্যা হবে, কারণ Profile তৈরির সময় `phone` দেওয়া হয়নি।

---

# তাহলে ২টা approach আছে

### Approach 1 — Registration-এর সময় required Profile field নেবে

Serializer:

```python
class RegisterSerializer(serializers.ModelSerializer):
    phone = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = [
            "username",
            "email",
            "password",
            "phone",
        ]

    def create(self, validated_data):
        phone = validated_data.pop("phone")

        user = User.objects.create_user(
            **validated_data
        )

        user.profile.phone = phone
        user.profile.save()

        return user
```

Flow:

```text
username
email
password
phone
   ↓
User তৈরি
   ↓
Signal
   ↓
Profile তৈরি
   ↓
phone সেট
```

তবে এখানে signal দিয়ে Profile তৈরি করার পর আবার update হচ্ছে।

---

### Approach 2 — Service Layer দিয়ে User + Profile একসাথে তৈরি করা

Production application-এ registration-এর required profile information যদি একই workflow-এর অংশ হয়, এটা অনেক পরিষ্কার:

```python
@transaction.atomic
def register_user(
    username,
    email,
    password,
    phone
):
    user = User.objects.create_user(
        username=username,
        email=email,
        password=password
    )

    Profile.objects.create(
        user=user,
        phone=phone
    )

    return user
```

এখানে:

```text
Registration
     ↓
User create
     ↓
Profile create
     ↓
সব সফল হলে commit
```

---

## সবচেয়ে গুরুত্বপূর্ণ rule

ধরো Profile:

```python
class Profile(models.Model):

    phone = models.CharField(max_length=20)              # required
    address = models.TextField(blank=True, null=True)   # optional
    dob = models.DateField(blank=True, null=True)       # optional
    avatar = models.ImageField(
        upload_to="profiles/",
        blank=True,
        null=True
    )                                                     # optional
```

তাহলে:

```text
phone       → অবশ্যই দিতে হবে
address     → পরে দিলেও হবে
dob         → পরে দিলেও হবে
avatar      → পরে দিলেও হবে
```

**আর যদি registration-এর সময় Profile-এর required field দিতে না চাও, তাহলে সেই field required রাখা যাবে না**—অথবা User+Profile creation-এর পুরো workflow-টা Service Layer দিয়ে এমনভাবে design করতে হবে যাতে required value কোথা থেকে আসবে সেটা নির্ধারিত থাকে।


----
