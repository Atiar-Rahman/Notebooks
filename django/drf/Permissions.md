DRF (Django REST Framework) এ **permission system** খুবই important — এটা control করে কে API access করতে পারবে, কে modify করতে পারবে, কে শুধু read করতে পারবে।

---

# 🔐 1. DRF Permission কী?

👉 Permission = **User কি করতে পারবে (Allow / Deny)**

Example:

* শুধু logged-in user access পাবে
* শুধু admin create/update/delete করতে পারবে
* user নিজের data ছাড়া অন্য কারও data দেখতে পারবে না

---

# 🧱 2. Permission Types (2 Layer)

DRF-এ permission দুইভাবে কাজ করে:

### ✅ 1. Global Permission (View Level)

* পুরো view-এর জন্য apply হয়

### ✅ 2. Object Level Permission

* নির্দিষ্ট object (instance) এর জন্য check হয়

---

# 📦 3. Built-in Permissions (Most Important)

### 🔹 1. AllowAny

```python
permission_classes = [AllowAny]
```

👉 সবাই access করতে পারবে (default)

---

### 🔹 2. IsAuthenticated

```python
permission_classes = [IsAuthenticated]
```

👉 শুধু logged-in user

---

### 🔹 3. IsAdminUser

```python
permission_classes = [IsAdminUser]
```

👉 শুধু admin (is_staff=True)

---

### 🔹 4. IsAuthenticatedOrReadOnly

```python
permission_classes = [IsAuthenticatedOrReadOnly]
```

👉

* GET → সবাই পারবে
* POST/PUT/DELETE → শুধু authenticated user

---

# ⚙️ 4. Permission কিভাবে use করবো?

## ✅ ViewSet Example

```python
from rest_framework.permissions import IsAuthenticated

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [IsAuthenticated]
```

---

## ✅ Function-based View

```python
from rest_framework.decorators import api_view, permission_classes
from rest_framework.permissions import IsAuthenticated

@api_view(['GET'])
@permission_classes([IsAuthenticated])
def my_view(request):
    return Response({"msg": "Hello"})
```

---

# 🧠 5. Custom Permission (VERY IMPORTANT 🔥)

## Example: Owner ছাড়া কেউ edit করতে পারবে না

```python
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

👉 use করো:

```python
permission_classes = [IsAuthenticated, IsOwner]
```

---

# 🔍 6. Object Level Permission কিভাবে কাজ করে?

DRF automatically call করে:

```python
def has_object_permission(self, request, view, obj):
```

👉 এটা trigger হয়:

* retrieve
* update
* delete

❗ কিন্তু list view-এ automatically call হয় না

---

# ⚡ 7. Advanced: Different Permission per Action

## 🔥 ViewSet এ action অনুযায়ী permission

```python
class ProductViewSet(ModelViewSet):

    def get_permissions(self):
        if self.action == 'list':
            return [AllowAny()]
        elif self.action == 'create':
            return [IsAuthenticated()]
        elif self.action in ['update', 'destroy']:
            return [IsAdminUser()]
        return [IsAuthenticated()]
```

---

# 🧩 8. Custom Logic Example (Real-world)

### 👉 Seller ছাড়া কেউ product edit করতে পারবে না

```python
class IsSeller(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.company.user == request.user
```

---

# 🛡️ 9. Best Practice (IMPORTANT)

✅ Always use:

```python
DEFAULT_PERMISSION_CLASSES = [
    'rest_framework.permissions.IsAuthenticated'
]
```

👉 settings.py

---

# ⚠️ 10. Common Mistakes

❌ শুধু `IsAuthenticated` use করলে:

* user অন্যের data edit করতে পারবে

✔️ fix:
👉 Custom object permission use করো

---

# 🔥 11. Real API Design (Recommended)

| Action   | Permission    |     |
| -------- | ------------- | --- |
| List     | AllowAny      |     |
| Retrieve | AllowAny      |     |
| Create   | Authenticated |     |
| Update   | Owner only    |     |
| Delete   | Admin         |     |

---

# 🎯 Summary

👉 DRF Permission = Security layer
👉 2 types: View level + Object level
👉 Built-in + Custom permission use করতে হয়
👉 Production-এ always object-level check দরকার

---

# Custom permission 

# 🧱 1. Custom Permission কীভাবে create করবো?

DRF-এ সব custom permission তৈরি হয় এই class inherit করে:

```python
from rest_framework.permissions import BasePermission
```

---

# ⚙️ 2. Basic Structure

```python
class MyPermission(BasePermission):

    def has_permission(self, request, view):
        # view level check
        return True

    def has_object_permission(self, request, view, obj):
        # object level check
        return True
```

---

# 🧠 3. Difference (IMPORTANT)

| Method                  | কাজ                     |     |
| ----------------------- | ----------------------- | --- |
| `has_permission`        | View access control     |     |
| `has_object_permission` | Specific object control |     |

---

# ✅ 4. Example 1: Only Authenticated User

```python
class IsLoggedIn(BasePermission):

    def has_permission(self, request, view):
        return request.user and request.user.is_authenticated
```

👉 (Already built-in আছে: `IsAuthenticated`)

---

# 🔥 5. Example 2: Owner Permission (MOST COMMON)

👉 User শুধু নিজের data edit করতে পারবে

```python
class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

---

# 🛒 6. Example 3: Seller Permission (Your Project 🔥)

ধরি তোমার `Product` model এ:

```python
product.company.user
```

👉 Seller ছাড়া কেউ modify করতে পারবে না

```python
class IsSeller(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.company.user == request.user
```

---

# 🧪 7. Example 4: Read Only for Everyone, Write for Owner

```python
class IsOwnerOrReadOnly(BasePermission):

    def has_object_permission(self, request, view, obj):

        # সবাই read করতে পারবে
        if request.method in ['GET', 'HEAD', 'OPTIONS']:
            return True

        # write only owner
        return obj.user == request.user
```

---

# ⚡ 8. Example 5: Role-based Permission

ধরি user model এ role আছে:

```python
user.role = 'admin' / 'seller' / 'customer'
```

```python
class IsAdminOrSeller(BasePermission):

    def has_permission(self, request, view):
        return request.user.role in ['admin', 'seller']
```

---

# 🚀 9. ViewSet এ use করা

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [IsAuthenticated, IsSeller]
```

---

# 🧩 10. Action-wise Permission (PRO LEVEL 🔥)

```python
def get_permissions(self):

    if self.action == 'list':
        return [AllowAny()]

    elif self.action == 'create':
        return [IsAuthenticated()]

    elif self.action in ['update', 'partial_update']:
        return [IsAuthenticated(), IsSeller()]

    elif self.action == 'destroy':
        return [IsAdminUser()]

    return [IsAuthenticated()]
```

---

# ⚠️ 11. Important Notes

### ❗ Object permission কাজ করবে না যদি:

👉 `get_object()` call না হয়

✔️ DRF automatically handle করে in:

* retrieve
* update
* delete

---

# 🧠 12. Best Practice Structure

📁 project structure:

```
apps/
 ├── products/
 │    ├── models.py
 │    ├── views.py
 │    ├── permissions.py   ✅ (important)
```

---

# 🔐 13. Advanced Example (Real-world combo)

```python
class IsSellerOrAdmin(BasePermission):

    def has_object_permission(self, request, view, obj):

        if request.user.is_staff:
            return True

        return obj.company.user == request.user
```

---

# 🎯 Final Summary

✅ `BasePermission` inherit করতে হবে
✅ `has_permission` → view level
✅ `has_object_permission` → object level
✅ Real project = Always object-level check
✅ Use cases:

* Owner check
* Seller check
* Role-based access
* Read-only logic

---
একদম solid question 🔥 — DRF-এ `get_object()` কিভাবে permission trigger করে এটা বুঝলে **custom permission mastery complete** 😎

---

# 🧠 Core Concept (Important)

👉 `has_object_permission()` **শুধু তখনই call হয় যখন `get_object()` call হয়**

✔️ DRF automatically `get_object()` call করে:

* retrieve (GET /id/)
* update (PUT/PATCH)
* destroy (DELETE)

❌ কিন্তু:

* list (GET /) → `get_object()` call হয় না
  ➡️ তাই object permission apply হয় না

---

# ⚙️ 1. Full Example (Custom Permission + ViewSet)

## 🔐 Custom Permission

```python
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

---

# 🧱 2. Model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

---

# 🚀 3. Full ViewSet Example

```python
from rest_framework.viewsets import ModelViewSet
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer
from .permissions import IsOwner

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [IsAuthenticated, IsOwner]

    # 🔥 Custom retrieve (get_object() call হচ্ছে)
    def retrieve(self, request, *args, **kwargs):
        product = self.get_object()   # 👈 IMPORTANT

        serializer = self.get_serializer(product)
        return Response(serializer.data)

    # 🔥 Custom update
    def update(self, request, *args, **kwargs):
        product = self.get_object()   # 👈 permission trigger হবে

        serializer = self.get_serializer(product, data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()

        return Response(serializer.data)

    # 🔥 Custom delete
    def destroy(self, request, *args, **kwargs):
        product = self.get_object()   # 👈 permission trigger হবে

        product.delete()
        return Response({"msg": "Deleted"})
```

---

# 🔍 4. Flow Explanation

### যখন request আসে:

```
GET /products/5/
```

👉 DRF internally করে:

1. `get_object()` call
2. `check_object_permissions(request, obj)` call
3. → `has_object_permission()` run

---

# ⚠️ 5. WRONG Example (Common Mistake ❌)

```python
def retrieve(self, request, *args, **kwargs):
    product = Product.objects.get(id=kwargs['pk'])  # ❌ WRONG

    serializer = ProductSerializer(product)
    return Response(serializer.data)
```

🚨 Problem:

* `get_object()` use করা হয়নি
* ❌ permission check skip হয়ে যাবে

---

# ✅ 6. Correct Way (Manual Permission Call)

যদি `get_object()` use না করো:

```python
def retrieve(self, request, *args, **kwargs):
    product = Product.objects.get(id=kwargs['pk'])

    self.check_object_permissions(request, product)  # ✅ manually call

    serializer = ProductSerializer(product)
    return Response(serializer.data)
```

---

# 🔥 7. List View-এ Object Permission apply করতে চাইলে

👉 manually handle করতে হবে

```python
def list(self, request, *args, **kwargs):
    queryset = self.get_queryset()

    filtered = [
        obj for obj in queryset
        if obj.user == request.user
    ]

    serializer = self.get_serializer(filtered, many=True)
    return Response(serializer.data)
```

---

# 🧠 Pro Tip (BEST PRACTICE)

👉 Always use:

```python
product = self.get_object()
```

👉 কারণ:

* permission auto handle করে
* 404 handle করে
* clean code

---

# 🎯 Final Summary

✔ `get_object()` = object permission trigger
✔ না করলে → security hole 😨
✔ custom logic করলে → `check_object_permissions()` manually call করতে হবে
✔ list view → আলাদা handle করতে হয়

---

এটা আসলেই **real-world DRF design question 🔥** — কোন জায়গায় কোন permission use করবে সেটাই production-quality API বানানোর মূল skill।

আমি তোমাকে **practical mapping + real use-case** দিয়ে বুঝাচ্ছি 👇

---

# 🎯 1. Quick Decision Rule (Shortcut 🧠)

👉 প্রথমে এই 3টা প্রশ্ন করো:

1. **User login করা লাগবে?**
2. **সবাই data দেখতে পারবে নাকি restricted?**
3. **User কি নিজের data ছাড়া অন্যটা edit করতে পারবে?**

---

# 🧱 2. Permission Selection Table (Most Important)

| Situation                          | Use Permission              |
| ---------------------------------- | --------------------------- |
| Public API (no login)              | `AllowAny`                  |
| Login required                     | `IsAuthenticated`           |
| Admin only                         | `IsAdminUser`               |
| Read for all, write for login user | `IsAuthenticatedOrReadOnly` |
| Only owner access                  | Custom (`IsOwner`)          |
| Seller only access                 | Custom (`IsSeller`)         |
| Role-based system                  | Custom (RBAC)               |

---

# 🛒 3. Real Project Mapping (eCommerce style 🔥)

## 🟢 Category

| Action               | Permission    |
| -------------------- | ------------- |
| list / retrieve      | `AllowAny`    |
| create/update/delete | `IsAdminUser` |

👉 Reason: Category সাধারণত admin manage করে

---

## 🟡 Product

| Action          | Permission                 |
| --------------- | -------------------------- |
| list / retrieve | `AllowAny`                 |
| create          | `IsAuthenticated` (seller) |
| update/delete   | `IsSeller` (owner only)    |

👉 Example:

```python
permission_classes = [IsAuthenticated, IsSeller]
```

---

## 🔵 Review

| Action        | Permission        |
| ------------- | ----------------- |
| list          | `AllowAny`        |
| create        | `IsAuthenticated` |
| update/delete | `IsOwner`         |

👉 User নিজের review ছাড়া অন্যটা edit করতে পারবে না

---

## 🛍️ Cart

| Action      | Permission        |
| ----------- | ----------------- |
| all actions | `IsAuthenticated` |

👉 Cart personal → login required

---

## 📦 Order

| Action   | Permission                           |
| -------- | ------------------------------------ |
| create   | `IsAuthenticated`                    |
| list     | `IsAuthenticated` (নিজের order only) |
| update   | `IsAdminUser`                        |
| retrieve | `IsOwner`                            |

---

# ⚙️ 4. Real ViewSet Design (Production 🔥)

```python
def get_permissions(self):

    if self.action in ['list', 'retrieve']:
        return [AllowAny()]

    elif self.action == 'create':
        return [IsAuthenticated()]

    elif self.action in ['update', 'partial_update']:
        return [IsAuthenticated(), IsOwner()]

    elif self.action == 'destroy':
        return [IsAdminUser()]

    return [IsAuthenticated()]
```

---

# 🧠 5. When to Use Custom Permission

👉 Custom লাগবে যখন:

* Owner check দরকার
* Seller / Company check দরকার
* Role-based access (admin, seller, buyer)
* Business logic (e.g. only paid user access)

---

# ⚠️ 6. Common Mistakes (VERY IMPORTANT)

❌ শুধু `IsAuthenticated` use করা
➡️ User অন্যের data modify করতে পারবে 😨

✔️ Fix:
👉 Always combine with object permission

```python
[IsAuthenticated, IsOwner]
```

---

# 🔥 7. Golden Rules (Must Follow)

✅ Public data → `AllowAny`
✅ Private data → `IsAuthenticated`
✅ Sensitive update → `IsOwner` / `IsSeller`
✅ System control → `IsAdminUser`
✅ Complex logic → Custom Permission

---

# 🎯 Final Architecture (Best Practice)

👉 Ideal combo:

```python
permission_classes = [IsAuthenticated, CustomPermission]
```

---

# 🚀 Summary

👉 Built-in = basic control
👉 Custom = real security
👉 View-level + Object-level combine করতে হবে
👉 Always think: **"Who can SEE vs Who can CHANGE?"**

---

খুব ভালো question 👌 — অনেকেই এখানে confused হয়।

---

# 🎯 Main Answer (Short)

👉 `permission_classes = [A, B, C]`

➡️ **Order technically matter করে না (logic-wise)**
➡️ DRF **সবগুলো permission check করে**

👉 যদি কোনো একটা fail করে → ❌ access denied

---

# 🧠 How DRF Actually Works

DRF internally এইভাবে run করে:

```python
for permission in permission_classes:
    if not permission.has_permission(request, view):
        raise PermissionDenied
```

👉 তারপর object level এ:

```python
for permission in permission_classes:
    if not permission.has_object_permission(request, view, obj):
        raise PermissionDenied
```

---

# ⚙️ Example

```python
permission_classes = [IsAuthenticated, IsOwner]
```

👉 Flow:

1. `IsAuthenticated` check
2. `IsOwner` check

✔️ দুইটাই True → access allowed
❌ যেকোনো একটা False → denied

---

# 🔥 Important Insight

👉 এটা **AND condition (সবগুলো True হতে হবে)**

```text
IsAuthenticated AND IsOwner
```

---

# ⚠️ Order কি একদমই matter করে না?

👉 **Mostly না**, BUT practical কিছু case আছে 👇

---

# 🚨 1. Performance Optimization (Minor ⚡)

```python
permission_classes = [IsAuthenticated, IsOwner]
```

✔️ ভালো order:

* আগে cheap check (IsAuthenticated)
* পরে heavy check (DB-based IsOwner)

👉 এতে unnecessary DB hit কমে

---

# 🚨 2. Error Message Priority

👉 DRF প্রথম fail করা permission এর error দেখায়

```python
permission_classes = [IsOwner, IsAuthenticated]
```

❌ user login না থাকলে:

* আগে `IsOwner` check হবে → confusing error আসতে পারে

✔️ better:

```python
[IsAuthenticated, IsOwner]
```

---

# 🚀 3. Best Practice Order

👉 Always follow this:

```python
permission_classes = [
    IsAuthenticated,   # basic check
    CustomPermission   # business logic
]
```

---

# 🧩 4. OR Logic লাগলে কী করবো?

👉 Default = AND
👉 OR চাইলে custom লিখতে হবে

```python
class IsAdminOrOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return request.user.is_staff or obj.user == request.user
```

---

# 🛑 Common Mistake

❌ এটা ভাবা:

```python
[IsAdminUser, IsAuthenticated]
```

👉 এটা OR না
👉 এটা actually:

```
IsAdminUser AND IsAuthenticated
```

---

# 🎯 Final Summary

✔ permission list = AND logic
✔ order mostly matter করে না
✔ but:

* performance এর জন্য আগে simple check
* error clarity এর জন্য আগে auth check

---

	দারুণ question 🔥 — এখানে **`or` vs `and`** বুঝা মানেই permission logic clear 😎

---

# 🎯 Codeটা আবার দেখি

```python
return request.user.is_staff or obj.user == request.user
```

👉 মানে:

* admin হলে ✅ allowed
* অথবা owner হলে ✅ allowed

---

# 🔀 1. যদি `or` use করি (Current)

```python
return request.user.is_staff or obj.user == request.user
```

### 👉 Logic:

```text
Admin  OR  Owner
```

### ✅ Allowed cases:

| User Type  | Result |
| ---------- | ------ |
| Admin      | ✅      |
| Owner      | ✅      |
| Other user | ❌      |

👉 এটা **most common real-world case**

---

# 🔒 2. যদি `and` use করি

```python
return request.user.is_staff and obj.user == request.user
```

### 👉 Logic:

```text
Admin AND Owner
```

### ⚠️ Allowed cases:

| User Type           | Result |
| ------------------- | ------ |
| Admin + Owner same  | ✅      |
| Admin but not owner | ❌      |
| Owner but not admin | ❌      |

👉 practically almost **সবাই blocked হয়ে যাবে** 😨

---

# 🧠 3. Real-world Interpretation

### 🔹 `or` = flexible access

👉 "এই দুইটার যেকোনো একটা হলেই হবে"

✔️ Use when:

* Admin OR Owner
* Seller OR Admin
* Paid user OR Trial user

---

### 🔹 `and` = strict access

👉 "দুইটাই একসাথে true হতে হবে"

✔️ Use when:

* verified AND subscribed user
* active AND email verified

---

# 🔥 4. Visual বুঝো

### OR case:

```text
Admin ❌ Owner ❌ → ❌
Admin ✅ Owner ❌ → ✅
Admin ❌ Owner ✅ → ✅
```

---

### AND case:

```text
Admin ❌ Owner ❌ → ❌
Admin ✅ Owner ❌ → ❌
Admin ❌ Owner ✅ → ❌
Admin ✅ Owner ✅ → ✅
```

---

# ⚡ 5. Best Practice (IMPORTANT)

👉 permission-এ usually use হয়:

✔️ `or` → access control
❌ `and` → rarely used

---

# 🧩 6. Real Example

### Correct:

```python
# eCommerce product edit
return request.user.is_staff or obj.seller == request.user
```

### Wrong (too strict):

```python
return request.user.is_staff and obj.seller == request.user
```

---

# 🎯 Final Summary

✔ `or` = any one condition → flexible (use most cases)
✔ `and` = all conditions → strict (rare)
✔ permission system-এ mostly `or` লাগে

---
