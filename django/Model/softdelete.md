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



না, **সব delete-এর জায়গায় `perform_destroy()` যোগ করতে হবে না।**

এটা নির্ভর করে আপনি **কোথা থেকে delete করছেন**।

### ১. DRF ViewSet-এর DELETE endpoint ✅

যদি API-এর মাধ্যমে delete করেন, তাহলে শুধু `perform_destroy()` override করলেই হবে।

```python
class ProductViewSet(ModelViewSet):
    ...

    def perform_destroy(self, instance):
        instance.soft_delete()
```

এখন API-এর `DELETE /products/1/` → soft delete করবে।

---

### ২. Model থেকে delete করলে ❌

যদি কোথাও লিখেন:

```python
product.delete()
```

এটা `perform_destroy()` দিয়ে যাবে না। কারণ এটা ViewSet-এর বাইরে।

এক্ষেত্রে আপনাকে লিখতে হবে:

```python
product.soft_delete()
```

---

### ৩. QuerySet delete করলে ❌

```python
Product.objects.filter(category=1).delete()
```

এটাও `perform_destroy()` call করবে না।

এটা সরাসরি database operation করবে।

Soft delete করতে হলে:

```python
Product.objects.filter(category=1).update(is_active=False)
```

অথবা custom QuerySet/Manager তৈরি করতে হবে।

---

## Summary

| কোথা থেকে delete হচ্ছে                 | `perform_destroy()` কাজ করবে? |
| -------------------------------------- | ----------------------------- |
| `DELETE` API (ViewSet)                 | ✅ হ্যাঁ                       |
| `product.delete()`                     | ❌ না                          |
| `Product.objects.filter(...).delete()` | ❌ না                          |
| Admin panel delete                     | ❌ না (ডিফল্টভাবে)             |
| Django shell                           | ❌ না                          |

### Production-এ কী করা হয়?

অনেক project-এ:

* API-এর জন্য `perform_destroy()` ব্যবহার করা হয়।
* Model-এ `soft_delete()` রাখা হয়।
* `QuerySet`-এর জন্য custom `SoftDeleteQuerySet` তৈরি করা হয়।
* Django Admin-এও custom delete action লেখা হয়।

এভাবে **সব জায়গায় consistent soft delete** নিশ্চিত করা হয়।

এটাই production-grade approach।


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


