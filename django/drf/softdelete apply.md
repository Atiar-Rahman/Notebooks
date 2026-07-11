Soft delete মানে database থেকে row **physically delete না করে**, একটা flag দিয়ে mark করা:

```text
delete ≠ remove row
delete = mark as deleted
```

Example:

Before:

| id | name       | is_deleted |
| -- | ---------- | ---------- |
| 1  | Python Job | False      |

Delete করার পরে:

| id | name       | is_deleted |
| -- | ---------- | ---------- |
| 1  | Python Job | True       |

Row DB-তে আছে, কিন্তু user দেখতে পাবে না।

---

# কেন Soft Delete?

Hard delete:

```python
job.delete()
```

Problem:

* data permanently gone
* restore করা কঠিন
* audit নেই
* accidental delete dangerous

Soft delete:

✅ restore করা যায়
✅ history থাকে
✅ admin দেখতে পারে
✅ analytics possible

Job portal-এর জন্য খুব useful।

---

# Step 1 — BaseModel এ field add

```python
from django.db import models

class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_deleted = models.BooleanField(default=False)

    class Meta:
        abstract = True
```

সব model inherit করলে auto field পাবে।

Example:

```python
class Job(BaseModel):
    title = models.CharField(max_length=100)
```

---

# Step 2 — Soft delete method

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_deleted = models.BooleanField(default=False)

    class Meta:
        abstract = True

    def soft_delete(self):
        self.is_deleted = True
        self.save()
```

Use:

```python
job.soft_delete()
```

---

# Step 3 — Problem: queryset still deleted rows ফেরত দেয়

ধরো:

```python
Job.objects.all()
```

Deleted rows-ও আসবে।

Example:

| id | title  | is_deleted |
| -- | ------ | ---------- |
| 1  | Python | False      |
| 2  | Java   | True       |

Query:

```python
Job.objects.all()
```

Output:

```python
[Python, Java]
```

Bad.

---

# Step 4 — Custom Manager

```python
class ActiveManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_deleted=False)
```

---

Model:

```python
class Job(BaseModel):
    title = models.CharField(max_length=100)

    objects = ActiveManager()
    all_objects = models.Manager()
```

Now:

### Default

```python
Job.objects.all()
```

Returns:

```python
only non deleted
```

### All rows

```python
Job.all_objects.all()
```

Returns:

```python
deleted + non deleted
```

---

# Step 5 — Override delete()

এটা powerful।

Default:

```python
instance.delete()
```

Normally hard delete করে।

Override:

```python
class BaseModel(models.Model):
    is_deleted = models.BooleanField(default=False)

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):
        self.is_deleted = True
        self.save()
```

Now:

```python
job.delete()
```

Actually soft delete করবে।

---

# Step 6 — Restore

```python
def restore(self):
    self.is_deleted = False
    self.save()
```

Use:

```python
job.restore()
```

---

# DRF Integration

## Serializer

Usually expose না করি:

```python
class JobSerializer(ModelSerializer):
    class Meta:
        model = Job
        exclude = ['is_deleted']
```

---

## ViewSet

```python
from rest_framework.viewsets import ModelViewSet

class JobViewSet(ModelViewSet):
    queryset = Job.objects.all()
    serializer_class = JobSerializer
```

Since manager already filters:

```python
Job.objects.all()
```

Deleted rows আসবে না।

---

# Custom soft delete endpoint

```python
from rest_framework.decorators import action
from rest_framework.response import Response
```

```python
class JobViewSet(ModelViewSet):
    queryset = Job.objects.all()
    serializer_class = JobSerializer

    @action(detail=True, methods=['post'])
    def soft_delete(self, request, pk=None):
        job = self.get_object()
        job.soft_delete()
        return Response({"message": "deleted"})
```

API:

```text
POST /jobs/5/soft_delete/
```

---

# Restore endpoint

```python
@action(detail=True, methods=['post'])
def restore(self, request, pk=None):
    job = Job.all_objects.get(pk=pk)
    job.restore()
    return Response({"message": "restored"})
```

---

# Full Flow Example

Create:

```python
job = Job.objects.create(title="Backend Dev")
```

DB:

| id | title       | is_deleted |
| -- | ----------- | ---------- |
| 1  | Backend Dev | False      |

Delete:

```python
job.delete()
```

DB:

| id | title       | is_deleted |
| -- | ----------- | ---------- |
| 1  | Backend Dev | True       |

Normal query:

```python
Job.objects.all()
```

Result:

```python
[]
```

Admin query:

```python
Job.all_objects.all()
```

Result:

```python
[Backend Dev]
```

Restore:

```python
job.restore()
```

Visible again.

---

# Production-level Better Design

অনেকে শুধু `is_deleted` না, `deleted_at` রাখে:

```python
deleted_at = models.DateTimeField(null=True, blank=True)
```

Delete করলে:

```python
from django.utils import timezone
self.deleted_at = timezone.now()
```

Benefit:

* কখন delete হয়েছে জানা যায়
* audit log better

---

## Job Portal এ কোথায় Soft Delete use করবে?

Recommended:

✅ User
✅ Company
✅ Job
✅ Application
✅ Post
✅ Message (optional)

Not necessary:

❌ Skill
❌ Category tables

---

Architecture:

```text
BaseModel
   ├── is_deleted
   ├── soft_delete()
   ├── restore()
   └── custom manager
```

এটাই clean reusable soft delete pattern।
E-commerce site-এ **সব model-এ soft delete লাগবে না**। Rule of thumb:

> যে data future audit / history / analytics / recovery-এর জন্য দরকার → Soft Delete
> যে data static/reference → Soft Delete usually unnecessary

---

# Soft Delete করা উচিত ✅

## 1. User / Customer

```python id="8jg0gr"
User
CustomerProfile
```

Why:

* account deactivate
* later restore
* order history রাখতে হবে

Example:
Amazon account delete করলেও পুরানো order history business side-এ থাকতে পারে।

---

## 2. Product (Usually yes)

```python id="9c4r67"
Product
```

Why:

* product discontinued হতে পারে
* old orders-এ product reference থাকবে

Bad hard delete case:

Order:

```text id="s2ozr8"
Order #101 → Product ID 5
```

Product hard delete → order broken ❌

Soft delete better.

---

## 3. Categories / Brands (Depends)

Example:

```python id="4l4h9j"
Category
Brand
```

Soft delete if:

* historical reporting দরকার

Example:
“2025 এ Nike category sales”

---

## 4. Orders (Almost NEVER hard delete)

```python id="xj8p5z"
Order
OrderItem
```

Very important.

Reason:

* accounting
* tax
* refund
* legal compliance

Orders usually:

* cancelled
* refunded
* archived

delete না।

Better:

```python id="5km9sa"
status = cancelled
```

---

## 5. Coupons / Promotions

```python id="ynzhf4"
Coupon
```

Coupon expired হলে hide করো।

Soft delete useful.

---

## 6. Reviews

```python id="vbjlwm"
Review
```

Useful if:

* moderation
* abuse recovery
* admin restore

---

## 7. Wishlist / Cart (Optional)

Depends business logic.

---

# Soft Delete না করলেও চলে ❌

## 1. Cart Items

```python id="mu6fzg"
CartItem
```

Temporary data.

User remove করলে hard delete fine.

---

## 2. Session / OTP

```python id="i4f4i5"
OTP
EmailVerificationToken
```

Temporary.

Delete.

---

## 3. Search History Cache

```python id="09wvv6"
SearchCache
RecommendationCache
```

No need.

---

## 4. Inventory Logs (Use logs instead)

Stock movement tables usually immutable logs.

---

## 5. Junction Tables (Mostly)

Example:

```python id="0r8nhv"
ProductTag
ProductColor
```

Usually hard delete okay.

---

# Special Case — Never delete, use status instead

Some models-এর জন্য soft delete-ও না।

Use status:

## Payment

```python id="s6b8pc"
Payment
Transaction
Invoice
```

Never delete.

Use:

```python id="x9rrfk"
PENDING
FAILED
SUCCESS
REFUNDED
```

Because finance data.

---

# My Recommended E-commerce Structure

## Soft Delete YES

* User
* Product
* ProductImage
* Category
* Brand
* Coupon
* Review
* Address

## Soft Delete NO

* Cart
* CartItem
* OTP
* Session
* Cache

## Never Delete (status only)

* Order
* OrderItem
* Payment
* Transaction
* Invoice

---

## Production tip

সব model-এ blindly `BaseModel(is_deleted)` দিও না।

আমি usually 3 base class রাখি:

```python id="q8x8dl"
BaseModel
SoftDeleteModel
TimestampModel
```

Example:

```python id="7a8c5t"
class Product(SoftDeleteModel):
    pass

class Payment(TimestampModel):
    pass
```

এটা cleaner architecture।
তিনটা base class আলাদা responsibility handle করবে:

1. **BaseModel** → common fields (`id`, timestamps)
2. **TimestampModel** → শুধু timestamps (যদি custom id না লাগে)
3. **SoftDeleteModel** → soft delete logic + manager

এভাবে inheritance flexible হয়।

---

# 1. BaseModel

সবচেয়ে generic base model।

```python
from django.db import models
import uuid


class BaseModel(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

Use when:

* UUID primary key চাই
* timestamps চাই

Example:

```python
class Category(BaseModel):
    name = models.CharField(max_length=100)
```

---

# 2. TimestampModel

শুধু timestamps, Django default id use করবে।

```python
from django.db import models


class TimestampModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

Use when:

* default auto increment id enough
* শুধু timestamps দরকার

Example:

```python
class Payment(TimestampModel):
    amount = models.DecimalField(max_digits=10, decimal_places=2)
```

Generated table:

```text
id (auto)
created_at
updated_at
amount
```

---

# 3. SoftDeleteModel

Soft delete logic + manager।

---

## Custom QuerySet

```python
from django.db import models


class SoftDeleteQuerySet(models.QuerySet):
    def delete(self):
        return super().update(is_deleted=True)

    def hard_delete(self):
        return super().delete()

    def alive(self):
        return self.filter(is_deleted=False)

    def deleted(self):
        return self.filter(is_deleted=True)
```

---

## Manager

```python
class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(
            self.model,
            using=self._db
        ).filter(is_deleted=False)
```

---

## SoftDeleteModel

```python
class SoftDeleteModel(TimestampModel):
    is_deleted = models.BooleanField(default=False)
    deleted_at = models.DateTimeField(null=True, blank=True)

    objects = SoftDeleteManager()
    all_objects = models.Manager()

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):
        from django.utils import timezone

        self.is_deleted = True
        self.deleted_at = timezone.now()
        self.save(update_fields=['is_deleted', 'deleted_at'])

    def restore(self):
        self.is_deleted = False
        self.deleted_at = None
        self.save(update_fields=['is_deleted', 'deleted_at'])

    def hard_delete(self):
        super().delete()
```

---

# Usage Examples

## Product → soft delete দরকার

```python
class Product(SoftDeleteModel):
    name = models.CharField(max_length=255)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

Delete:

```python
product.delete()
```

Actually:

```text
is_deleted = True
```

---

## Category → no soft delete

```python
class Category(BaseModel):
    name = models.CharField(max_length=100)
```

---

## Payment → never delete

```python
class Payment(TimestampModel):
    amount = models.DecimalField(max_digits=10, decimal_places=2)
    status = models.CharField(max_length=20)
```

---

# Query Example

Default manager:

```python
Product.objects.all()
```

Returns:

```text
only active products
```

All rows:

```python
Product.all_objects.all()
```

Returns:

```text
active + deleted
```

Deleted only:

```python
Product.all_objects.filter(is_deleted=True)
```

---

# Recommended Inheritance Pattern

```text
models/
 ├── base.py
 │    ├── BaseModel
 │    ├── TimestampModel
 │    └── SoftDeleteModel
```

---

## Which one use where?

| Model Type | Base Class      |
| ---------- | --------------- |
| Product    | SoftDeleteModel |
| User       | SoftDeleteModel |
| Coupon     | SoftDeleteModel |
| Payment    | TimestampModel  |
| Order      | TimestampModel  |
| Category   | BaseModel       |

আমি সাধারণত **large Django project**-এ এটাই use করি কারণ সব model-এ `is_deleted` force করতে হয় না।
`SoftDeleteQuerySet` এর methods আসলে **queryset level operations customize** করে।
মানে:

```python
Product.objects.filter(...)
```

এখানে যে object return হয় সেটা `QuerySet` — ওই QuerySet-এর behavior override করছি।

তোমার code:

```python
class SoftDeleteQuerySet(models.QuerySet):
    def delete(self):
        return super().update(is_deleted=True)

    def hard_delete(self):
        return super().delete()

    def alive(self):
        return self.filter(is_deleted=False)

    def deleted(self):
        return self.filter(is_deleted=True)
```

Line by line দেখি।

---

# 1. `delete()`

Default Django:

```python
Product.objects.filter(category=1).delete()
```

Normally SQL:

```sql
DELETE FROM product WHERE category_id=1;
```

সব row permanently delete।

---

আমাদের override:

```python
def delete(self):
    return super().update(is_deleted=True)
```

এখন:

```python
Product.objects.filter(category=1).delete()
```

Actually internally হবে:

```python
Product.objects.filter(category=1).update(is_deleted=True)
```

Example DB:

Before:

| id | name     | is_deleted |
| -- | -------- | ---------- |
| 1  | Mouse    | False      |
| 2  | Keyboard | False      |

Run:

```python
Product.objects.filter(id=1).delete()
```

After:

| id | name     | is_deleted |
| -- | -------- | ---------- |
| 1  | Mouse    | True       |
| 2  | Keyboard | False      |

Physical delete হয়নি।

---

# Why `super().update()`?

কারণ current queryset already filtered।

ধরো:

```python
qs = Product.objects.filter(price__gt=100)
```

এখন `qs.delete()` call করলে:

```python
super().update(is_deleted=True)
```

Only সেই queryset rows update হবে।

---

# 2. `hard_delete()`

```python
def hard_delete(self):
    return super().delete()
```

এটা original Django delete call করছে।

Example:

```python
Product.objects.filter(id=1).hard_delete()
```

SQL:

```sql
DELETE FROM product WHERE id=1;
```

Actually row remove।

Before:

| id | name  |
| -- | ----- |
| 1  | Mouse |

After:

Empty.

---

# 3. `alive()`

```python
def alive(self):
    return self.filter(is_deleted=False)
```

Shortcut method।

Instead of:

```python
Product.objects.filter(is_deleted=False)
```

Write:

```python
Product.objects.alive()
```

Returns only active rows.

Example:

DB:

| id | is_deleted |
| -- | ---------- |
| 1  | False      |
| 2  | True       |

Query:

```python
Product.all_objects.alive()
```

Result:

```python
[id=1]
```

---

# 4. `deleted()`

```python
def deleted(self):
    return self.filter(is_deleted=True)
```

Only deleted rows।

Example:

```python
Product.all_objects.deleted()
```

Result:

```python
[id=2]
```

Useful for admin panel / trash bin.

---

# Full flow with Manager

Custom manager:

```python
class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(
            self.model,
            using=self._db
        ).filter(is_deleted=False)
```

---

Model:

```python
class Product(SoftDeleteModel):
    name = models.CharField(max_length=100)
```

Suppose:

```python
objects = SoftDeleteManager()
all_objects = SoftDeleteQuerySet.as_manager()
```

---

## Query flow

### Normal query

```python
Product.objects.all()
```

Step:

1. calls manager
2. manager returns queryset
3. queryset auto adds:

```python
filter(is_deleted=False)
```

Result:

Only active rows.

---

### Access deleted rows

```python
Product.all_objects.deleted()
```

Flow:

* `all_objects`
* returns full queryset
* `.deleted()`

Result:

Only deleted rows.

---

# Important: QuerySet delete vs Instance delete

Many people confuse this.

## QuerySet delete

```python
Product.objects.filter(id=1).delete()
```

Uses:

```python
SoftDeleteQuerySet.delete()
```

---

## Instance delete

```python
product = Product.objects.get(id=1)
product.delete()
```

Uses:

```python
Model.delete()
```

NOT queryset delete.

So if তুমি শুধু QuerySet override করো:

```python
Product.objects.filter(id=1).delete()
```

Soft delete হবে ✅

কিন্তু:

```python
product.delete()
```

Hard delete হয়ে যেতে পারে ❌

তাই model-এও override করো:

```python
def delete(self, *args, **kwargs):
    self.is_deleted = True
    self.save()
```

---

# Final mental model

```text
Manager      -> controls Product.objects
QuerySet     -> controls filter(), delete(), chain methods
Model        -> controls single instance methods
```

Example:

| Code                      | Uses     |
| ------------------------- | -------- |
| Product.objects.all()     | Manager  |
| Product.objects.deleted() | QuerySet |
| product.delete()          | Model    |

এজন্য production-এ soft delete properly করতে **Manager + QuerySet + Model** — তিনটাতেই integration করা হয়।
`QuerySet` class-এ Django অনেক built-in method define করে। সব override করতে হয় না—**যেটা business logic change করতে চাও শুধু সেটা**।

Soft delete context-এ আগে বুঝি QuerySet-এ common methods কী কী।

---

# Common QuerySet Methods

## Retrieval

```python
all()
filter()
exclude()
get()
first()
last()
exists()
count()
```

Example:

```python id="wwcw7r"
Product.objects.filter(price__gt=100)
```

---

## Update

```python
update()
bulk_update()
```

Example:

```python id="wnln33"
Product.objects.filter(category=1).update(stock=0)
```

---

## Delete

```python
delete()
```

Default:

```python id="sfr73o"
DELETE FROM table
```

Soft delete-এ এটাকেই বেশি override করা হয়।

---

## Aggregation

```python
aggregate()
annotate()
```

Example:

```python id="k0p6s7"
Product.objects.aggregate(Avg('price'))
```

---

## Ordering / Limiting

```python
order_by()
distinct()
reverse()
```

---

## Related optimization

```python
select_related()
prefetch_related()
```

---

# Soft Delete-এ কোনগুলো override লাগে?

সাধারণত **৩টা জায়গা** important:

---

## 1. `delete()` — MUST override

কারণ default hard delete।

```python id="vd1jse"
class SoftDeleteQuerySet(models.QuerySet):
    def delete(self):
        return self.update(is_deleted=True)
```

Example:

```python id="cyh5hb"
Product.objects.filter(id=1).delete()
```

Hard delete → Soft delete

---

## 2. `get_queryset()` in Manager — MUST

Deleted rows hide করতে।

```python id="g63eyh"
class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(
            self.model,
            using=self._db
        ).filter(is_deleted=False)
```

Without this:

```python id="7u5whi"
Product.objects.all()
```

deleted rows-ও আসবে।

---

## 3. Model `delete()` — MUST

Single instance delete ধরার জন্য।

```python id="3cc22z"
def delete(self, *args, **kwargs):
    self.is_deleted = True
    self.save()
```

Because:

```python id="yv9wtm"
product.delete()
```

QuerySet delete না, Model delete call করে।

---

# Optional custom QuerySet methods

এগুলো override না, custom helper method।

## alive()

```python id="9w9c9m"
def alive(self):
    return self.filter(is_deleted=False)
```

---

## deleted()

```python id="hjv95s"
def deleted(self):
    return self.filter(is_deleted=True)
```

---

## hard_delete()

```python id="gqg0c8"
def hard_delete(self):
    return super().delete()
```

Admin cleanup-এর জন্য।

---

## restore()

```python id="ub8s08"
def restore(self):
    return self.update(is_deleted=False)
```

Deleted rows restore।

---

# `update()` override লাগবে?

Usually **না**।

কারণ:

```python id="u8v24n"
Product.objects.filter(id=1).update(is_deleted=True)
```

Developer explicit call করছে—override দরকার নেই।

Only override if strict business rule দরকার।

---

# `get()` override?

না।

কারণ:

```python id="kjm0h8"
Product.objects.get(id=1)
```

Manager already filtered queryset return করে।

---

# Production recommendation

Override / Define:

| Method               | Required? | Why                  |
| -------------------- | --------- | -------------------- |
| QuerySet.delete      | ✅         | bulk soft delete     |
| Manager.get_queryset | ✅         | hide deleted rows    |
| Model.delete         | ✅         | instance soft delete |
| QuerySet.deleted     | Optional  | helper               |
| QuerySet.alive       | Optional  | helper               |
| QuerySet.restore     | Optional  | helper               |
| QuerySet.hard_delete | Optional  | admin cleanup        |

---

### Mental model

```text
Manager   -> default queries control
QuerySet  -> bulk operations control
Model     -> single instance control
```

Soft delete-এ **minimum override**:

```text
QuerySet.delete
Manager.get_queryset
Model.delete
```

এই তিনটা থাকলেই বেশিরভাগ case cover হবে।


----------
আপনার `BaseModel`-এ `soft_delete()` method যোগ করার সিদ্ধান্ত ঠিক আছে। এখন প্রশ্ন হলো **কোথায় `soft_delete()` call করবেন?**

Senior Django developer হিসেবে উত্তর হলো: **Business logic যেখানে delete request handle করে, সেখানে `soft_delete()` call করবেন।** সাধারণত View, Service Layer, বা ViewSet-এর `destroy()` method-এ।

### Option 1 (সবচেয়ে common) - DRF ViewSet এ

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.active.all()
    serializer_class = ProductSerializer

    def destroy(self, request, *args, **kwargs):
        instance = self.get_object()
        instance.soft_delete()
        return Response(status=204)
```

এখন

```
DELETE /products/1/
```

database থেকে row delete হবে না।

বরং

```text
id=1
name="Laptop"
is_active=False
```

হয়ে যাবে।

---

## Option 2 - Service Layer

যদি Service Layer ব্যবহার করেন

```python
class ProductService:

    @staticmethod
    def delete_product(product):
        product.soft_delete()
```

View

```python
class ProductViewSet(ModelViewSet):

    def destroy(self, request, *args, **kwargs):
        product = self.get_object()
        ProductService.delete_product(product)
        return Response(status=204)
```

এটা বড় project-এর জন্য cleaner।

---

## Option 3 - Model এর delete() override করা (অনেক project এ ব্যবহৃত)

অনেকে `soft_delete()` আলাদা method না রেখে `delete()`-ই override করেন।

```python
class BaseModel(models.Model):
    ...

    def delete(self, *args, **kwargs):
        self.is_active = False
        self.save(update_fields=["is_active"])
```

এখন

```python
product.delete()
```

call করলেই soft delete হবে।

Hard delete করতে

```python
Product.objects.filter(id=1).delete()
```

এটা কিন্তু `QuerySet.delete()` হওয়ায় model-এর `delete()` bypass করতে পারে। তাই hard delete-এর জন্য আলাদা method রাখা ভালো:

```python
def hard_delete(self):
    super().delete()
```

---

## আপনার বর্তমান design

```python
class BaseModel(models.Model):

    objects = models.Manager()
    active = ActiveManager()

    ...

    def soft_delete(self):
        self.is_active = False
        self.save(update_fields=["is_active"])

    def restore(self):
        self.is_active = True
        self.save(update_fields=["is_active"])

    def hard_delete(self):
        super().delete()
```

এটা ভালো design।

ব্যবহার:

```python
product = Product.active.get(id=1)

product.soft_delete()
```

Restore:

```python
product = Product.objects.get(id=1)
product.restore()
```

Hard delete:

```python
product.hard_delete()
```

---

### Senior Tip

`instance.soft_delete()` ব্যবহার করা ভালো, কারণ এতে code পড়েই বোঝা যায় যে এটি **soft delete**। `delete()` override করলে অনেক সময় অন্য developer বুঝতে পারে না যে data আসলে database থেকে delete হচ্ছে না। তাই explicit `soft_delete()` method রাখা অনেক production project-এ বেশি readable এবং maintainable হয়।
হ্যাঁ, **অবশ্যই**। DRF-এ `perform_destroy()` (না যে `perform_delete()`) override করাই সবচেয়ে clean এবং recommended উপায়।

`ModelViewSet`-এর `destroy()` method ভেতরে `perform_destroy(instance)` call করে। তাই শুধু এই method override করলেই হবে।

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.active.all()
    serializer_class = ProductSerializer

    def perform_destroy(self, instance):
        instance.soft_delete()
```

Flow হবে:

```text
DELETE /products/1/
        │
        ▼
destroy()
        │
        ▼
perform_destroy(instance)
        │
        ▼
instance.soft_delete()
```

### কেন `perform_destroy()` ভালো?

* `destroy()`-এর default behavior (permission check, object lookup, response handling) ঠিক থাকে।
* শুধু delete করার logic পরিবর্তন করতে হয়।
* Code ছোট, clean এবং DRF-এর convention অনুযায়ী।

### `perform_delete()` আছে কি?

❌ না। DRF-এ `perform_delete()` নামে কোনো hook নেই।

সঠিক method হলো:

```python
def perform_destroy(self, instance):
    instance.soft_delete()
```

### Senior Recommendation

যদি আপনার project-এ সব model-ই `BaseModel` inherit করে এবং soft delete ব্যবহার করে, তাহলে প্রতিটি ViewSet-এ `perform_destroy()` লেখার পরিবর্তে একটি `SoftDeleteMixin` তৈরি করতে পারেন।

```python
class SoftDeleteMixin:
    def perform_destroy(self, instance):
        instance.soft_delete()
```

তারপর:

```python
class ProductViewSet(SoftDeleteMixin, ModelViewSet):
    queryset = Product.active.all()
    serializer_class = ProductSerializer
```

এভাবে এক জায়গায় logic লিখে সব ViewSet-এ reuse করা যায়।
হ্যাঁ, **`destroy()` এবং `perform_destroy()` আলাদা method**, এবং তাদের কাজও আলাদা। এটা DRF-এর design pattern-এর একটি গুরুত্বপূর্ণ অংশ।

---

# `destroy()` কী?

`destroy()` হলো পুরো DELETE request handle করার method।

এটি:

* Permission check করে
* Object খুঁজে বের করে (`get_object()`)
* `perform_destroy()` call করে
* শেষে HTTP response return করে

সরলভাবে:

```python
def destroy(self, request, *args, **kwargs):
    instance = self.get_object()
    self.perform_destroy(instance)
    return Response(status=204)
```

---

# `perform_destroy()` কী?

এটা শুধু **object কীভাবে delete হবে** সেই logic-এর জন্য।

Default implementation:

```python
def perform_destroy(self, instance):
    instance.delete()
```

আপনি soft delete করতে চাইলে শুধু এটুকু change করবেন।

```python
def perform_destroy(self, instance):
    instance.soft_delete()
```

---

# Flow

```
DELETE Request
       │
       ▼
destroy()
       │
       ├── get_object()
       │
       ├── permission check
       │
       ├── perform_destroy(instance)
       │          │
       │          └── instance.delete()
       │              (বা soft_delete())
       │
       ▼
HTTP 204 Response
```

---

# কখন `destroy()` override করবেন?

যখন পুরো request handling পরিবর্তন করতে হবে।

উদাহরণ:

```python
def destroy(self, request, *args, **kwargs):
    instance = self.get_object()

    if instance.status == "locked":
        return Response(
            {"error": "Cannot delete"},
            status=400
        )

    self.perform_destroy(instance)
    return Response(
        {"message": "Deleted successfully"}
    )
```

এখানে response-ও customize করা হয়েছে।

---

# কখন `perform_destroy()` override করবেন?

যখন শুধু delete করার behavior পরিবর্তন করবেন।

উদাহরণ:

```python
def perform_destroy(self, instance):
    instance.soft_delete()
```

এটাই soft delete-এর জন্য recommended।

---

# Senior DRF Rule

| যদি পরিবর্তন করতে চান    | Override করবেন        |
| ------------------------ | --------------------- |
| শুধু delete করার logic   | ✅ `perform_destroy()` |
| পুরো DELETE request flow | ✅ `destroy()`         |

**Rule of thumb:** যদি শুধু database operation বদলাতে চান (যেমন soft delete), তাহলে `perform_destroy()` ব্যবহার করুন। `destroy()` override করুন তখনই, যখন request handling বা response-ও পরিবর্তন করার প্রয়োজন আছে।


আপনার `BaseModel`-এ `hard_delete()` method যোগ করার উপায় মোটামুটি ঠিকই আছে। তবে এটাকে একটু improve করা যায়।

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)

    objects = models.Manager()
    active = ActiveManager()

    class Meta:
        abstract = True

    def soft_delete(self):
        self.is_active = False
        self.save(update_fields=["is_active"])

    def restore(self):
        self.is_active = True
        self.save(update_fields=["is_active"])

    def hard_delete(self):
        super().delete()
```

### ব্যবহার

Soft delete:

```python
product = Product.objects.get(id=1)
product.soft_delete()
```

Hard delete:

```python
product = Product.objects.get(id=1)
product.hard_delete()
```

এবার row database থেকে স্থায়ীভাবে delete হয়ে যাবে।

---

## DRF-এ Hard Delete Endpoint

যদি আলাদা API দিয়ে hard delete করতে চান, তাহলে custom action ব্যবহার করতে পারেন।

```python
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import status

class ProductViewSet(ModelViewSet):

    @action(detail=True, methods=["delete"])
    def hard_delete(self, request, pk=None):
        product = self.get_object()
        product.hard_delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

তখন endpoint হবে:

```text
DELETE /products/1/hard_delete/
```

---

## Senior Project-এ কী করা হয়?

সাধারণত:

* `DELETE /products/1/` → `soft_delete()`
* `DELETE /products/1/hard_delete/` → `hard_delete()`

এভাবে user ভুল করলেও data recover করা যায়, আর শুধুমাত্র admin বা superuser-কে hard delete permission দেওয়া হয়।

এটি production application-এ বহুল ব্যবহৃত একটি pattern।
`restore()`-ও `hard_delete()`-এর মতোই একটি action হিসেবে করা যায়। সাধারণত soft-deleted object restore করার জন্য custom endpoint তৈরি করা হয়।

প্রথমে `BaseModel`:

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)

    objects = models.Manager()
    active = ActiveManager()

    class Meta:
        abstract = True

    def soft_delete(self):
        self.is_active = False
        self.save(update_fields=["is_active"])

    def restore(self):
        self.is_active = True
        self.save(update_fields=["is_active"])

    def hard_delete(self):
        super().delete()
```

তারপর ViewSet-এ:

```python
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import status

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()   # restore করতে objects ব্যবহার করুন
    serializer_class = ProductSerializer

    @action(detail=True, methods=["post"])
    def restore(self, request, pk=None):
        product = self.get_object()
        product.restore()
        return Response(
            {"message": "Product restored successfully"},
            status=status.HTTP_200_OK
        )
```

### Endpoint

```text
POST /products/1/restore/
```

এতে:

```text
Before:
id=1
name="Laptop"
is_active=False
```

↓

```text
After:
id=1
name="Laptop"
is_active=True
```

---

## গুরুত্বপূর্ণ বিষয়

যদি আপনার `queryset` হয়:

```python
queryset = Product.active.all()
```

তাহলে soft-deleted object (`is_active=False`) `get_object()` দিয়ে পাওয়া যাবে না। ফলে restore কাজ করবে না।

Restore endpoint-এর জন্য হয়:

```python
queryset = Product.objects.all()
```

অথবা `get_queryset()` override করে action অনুযায়ী queryset পরিবর্তন করুন:

```python
def get_queryset(self):
    if self.action == "restore":
        return Product.objects.all()
    return Product.active.all()
```

এটি production-এ বেশি ব্যবহার করা হয়, কারণ সাধারণ API-তে শুধু active data দেখা যায়, কিন্তু restore action inactive data-ও access করতে পারে।





তোমার উদ্দেশ্য যদি একাধিক `ViewSet`-এ একই `perform_destroy()`, `restore()`, `hard_delete()` ব্যবহার করা হয়, তাহলে **Mixin (`DeleteAndRestore`) রাখাই ভালো**। তবে কিছু পরিবর্তন দরকার।

### ১. Inheritance-এর order

Mixin আগে, `ModelViewSet` পরে:

```python
class BannerViewSet(DeleteAndRestore, ModelViewSet):
    queryset = Banner.active.all()
    serializer_class = BannerSerializer
```

### ২. `hard_delete()`-কে action বানাও

এখন `hard_delete()`-তে `@action` নেই, তাই এটা route হিসেবে কাজ করবে না।

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class DeleteAndRestore:
    def perform_destroy(self, instance):
        instance.soft_delete()

    @action(detail=True, methods=["post"])
    def restore(self, request, pk=None):
        instance = self.get_object()
        instance.restore()
        return Response({"message": "Restored successfully"})

    @action(detail=True, methods=["delete"])
    def hard_delete(self, request, pk=None):
        instance = self.get_object()
        instance.hard_delete()
        return Response({"message": "Hard deleted successfully"})
```

### ৩. `BannerViewSet`

```python
class BannerViewSet(DeleteAndRestore, ModelViewSet):
    queryset = Banner.active.all()
    serializer_class = BannerSerializer
```

এখানে আর `perform_destroy()`, `restore()`, `hard_delete()` লিখতে হবে না।

---

### কোনটা রাখবে?

* যদি শুধু `BannerViewSet`-এ ব্যবহার করো → ViewSet-এর ভিতরে লিখলেও চলে।
* যদি `KnowledgeViewSet`, `ProjectViewSet`, `TopicViewSet`-এও একই functionality লাগবে → **Mixin (`DeleteAndRestore`) ব্যবহার করো**। এটিই DRF-এ reusable code লেখার প্রচলিত উপায়।

------
হ্যাঁ, একদম। এটাই **reusability** এবং **inheritance**-এর মূল উদ্দেশ্য।

যদি একই code অনেক `ViewSet`-এ লাগে, তাহলে একটি **Mixin** বা base class বানিয়ে inheritance করলে সেই class-এর সব method ব্যবহার করতে পারবে।

উদাহরণ:

```python
class DeleteAndRestore:
    def perform_destroy(self, instance):
        instance.soft_delete()

    @action(detail=True, methods=["post"])
    def restore(self, request, pk=None):
        instance = self.get_object()
        instance.restore()
        return Response({"message": "Restored successfully"})
```

তারপর:

```python
class BannerViewSet(DeleteAndRestore, ModelViewSet):
    queryset = Banner.active.all()
    serializer_class = BannerSerializer
```

এবং:

```python
class ProjectViewSet(DeleteAndRestore, ModelViewSet):
    queryset = Project.active.all()
    serializer_class = ProjectSerializer
```

এখন `BannerViewSet` এবং `ProjectViewSet`—দুটোতেই থাকবে:

* ✅ `perform_destroy()`
* ✅ `restore()`
* ✅ `hard_delete()` (যদি mixin-এ থাকে)

আবার যদি mixin-এ নতুন method যোগ করো:

```python
class DeleteAndRestore:
    ...

    def log_action(self):
        print("Action logged")
```

তাহলে inheritance করা সব `ViewSet`-এ `log_action()`-ও পাওয়া যাবে।

### তবে একটা বিষয় মনে রাখবে

যদি child class-এ একই নামের method আবার লেখো, তাহলে child class-এর method-ই চলবে।

উদাহরণ:

```python
class DeleteAndRestore:
    def perform_destroy(self, instance):
        print("Mixin")
```

```python
class BannerViewSet(DeleteAndRestore, ModelViewSet):
    def perform_destroy(self, instance):
        print("Banner")
```

এক্ষেত্রে `BannerViewSet`-এর `perform_destroy()` চলবে, mixin-এরটা override হয়ে যাবে।

**সংক্ষেপে:** হ্যাঁ, একই code বারবার লাগলে reusable class (সাধারণত Mixin বা Base Class) বানিয়ে inheritance করা Python এবং Django-তে সবচেয়ে ভালো practice। এতে code কমে, maintain করা সহজ হয় এবং সব জায়গায় একই behavior রাখা যায়।
