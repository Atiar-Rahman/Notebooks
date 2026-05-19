## 📦 Package: `drf-nested-routers`

🔗 drf-nested-routers

### 👉 What it is

`drf-nested-routers` is a **third-party extension for Django REST Framework (DRF)** that helps you create **nested API URLs (parent → child relationships)** easily.

➡️ Example:

```
/users/
/users/1/posts/
/users/1/posts/10/
```

👉 Without this package → manually handle URL + filtering
👉 With this package → automatic nested routing

---

## 🧠 Why you need it (Core Idea)

In real-world apps (like your **ecommerce project**), resources are related:

* Seller → Products
* Product → Reviews
* Order → OrderItems

👉 These are **nested resources**

💡 DRF default router cannot handle this cleanly
👉 That’s why this package exists ([django-rest-framework.org][1])

---

## 🔥 Example (Simple)

### Models

```
Domain
 └── Nameserver
```

### URL Structure

```
/domains/
/domains/1/
/domains/1/nameservers/
/domains/1/nameservers/5/
```

---

## ⚙️ How to Use

### 1. Install

```bash
pip install drf-nested-routers
```

(No need to add in `INSTALLED_APPS`) ([Socket][2])

---

### 2. urls.py

```python
from rest_framework_nested import routers
from .views import DomainViewSet, NameserverViewSet

router = routers.SimpleRouter()
router.register(r'domains', DomainViewSet)

domains_router = routers.NestedSimpleRouter(
    router,
    r'domains',
    lookup='domain'
)

domains_router.register(
    r'nameservers',
    NameserverViewSet,
    basename='domain-nameservers'
)

urlpatterns = router.urls + domains_router.urls
```

---

### 3. ViewSet (IMPORTANT ⚠️)

You must filter by parent ID:

```python
class NameserverViewSet(viewsets.ModelViewSet):
    serializer_class = NameserverSerializer

    def get_queryset(self):
        return Nameserver.objects.filter(
            domain_id=self.kwargs['domain_pk']
        )
```

👉 Because nested router only gives you URL
👉 Filtering is your responsibility ([Stack Overflow][3])

---

## 🧩 How it works internally

* Parent router → `/domains/`
* Nested router → `/domains/{domain_pk}/nameservers/`
* `domain_pk` automatically passed to ViewSet via `kwargs`

---

## 💡 Real Use Case (Your Ecommerce)

For your project:

```
/sellers/
/sellers/5/products/
/sellers/5/products/10/

/products/10/reviews/
```

👉 Perfect for:

* Multi-vendor system
* Cart → CartItems
* Order → OrderItems

---

## ✅ Advantages

* Clean REST structure
* Auto URL generation
* Easy parent-child relationship
* Scalable for complex APIs

---

## ⚠️ Limitations / Things to know

* You MUST override `get_queryset()`
* Deep nesting (3+ levels) can get messy
* Sometimes `@action` is enough (no need for nested router)

---

## 🚀 When to Use vs NOT

### ✅ Use when:

* Strong parent-child relation
* Example: Seller → Products

### ❌ Avoid when:

* Independent resources
* Example: `/products/` (no need `/seller/5/products/` always)

---

## 🧠 Pro Tip (Very Important for you)

For your Django + DRF ecommerce:

👉 Use nested routers for:

* Seller → Products
* Order → OrderItems

👉 Use normal router for:

* Products (global listing)
* Categories

👉 Combine both 🔥

---

If you want, I can **integrate this into your full ecommerce system (models + routers + viewsets)** step-by-step.

[1]: https://www.django-rest-framework.org/api-guide/routers/?utm_source=chatgpt.com "Routers - Django REST framework"
[2]: https://socket.dev/pypi/package/drf-nested-routers?utm_source=chatgpt.com "drf-nested-routers - PyPI Package Security Analysis - Socket"
[3]: https://stackoverflow.com/questions/22194499/django-rest-framework-nested-urls-with-drf-nested-routers?utm_source=chatgpt.com "Django-rest-framework nested urls with drf-nested-routers - Stack Overflow"






--------------
# **age router create, tarpor register** korte hoy. Eta DRF er standard flow.

---

# 🧠 Basic Rule

```text
1. Router create
2. Router e register
3. urlpatterns e add
```

---

# 🔥 Step-by-step Example

## ✅ 1️⃣ Router create

```python
from rest_framework import routers

router = routers.DefaultRouter()
```

---

## ✅ 2️⃣ Register ViewSet

```python
router.register(r'sellers', SellerViewSet)
router.register(r'products', ProductViewSet)
```

---

## ✅ 3️⃣ URL add

```python
urlpatterns = router.urls
```

---

# ⚡ Nested Router er khetreo same rule

## 🔥 Full Example

```python
from rest_framework_nested import routers

# 1️⃣ parent router
router = routers.DefaultRouter()
router.register(r'sellers', SellerViewSet)

# 2️⃣ nested router create
seller_router = routers.NestedSimpleRouter(
    router,
    r'sellers',
    lookup='seller'
)

# 3️⃣ nested register
seller_router.register(
    r'products',
    SellerProductViewSet,
    basename='seller-products'
)

# 4️⃣ urlpatterns
urlpatterns = router.urls + seller_router.urls
```

---

# 🧩 Flow ta bujho

```text
router create
   ↓
register (parent)
   ↓
nested router create
   ↓
register (child)
   ↓
urlpatterns add
```

---

# ❌ Common mistake

❌ router create na kore register kora:

```python
router.register(...)  ❌
```

✔️ correct:

```python
router = DefaultRouter()
router.register(...) ✅
```

---

# 🚀 Short Summary

👉 Always:

```text
Router → Register → URL add
```

👉 Nested hole:

```text
Parent Router → Parent Register
→ Nested Router → Child Register
→ urlpatterns
```

---



👉 **Parent → Child relation ke URL diye represent kora**

---

# 🧠 Nested Routing ki?

ধরো:

* 1 ta **Seller**
* tar onek **Product**

👉 relation:

```
Seller → Products
```

👉 Normal URL:

```
/products/
```

👉 Nested URL:

```
/sellers/5/products/
```

✔️ mane: **seller 5 er sob product**

---

# 🔥 Real Example (Step-by-step)

## 1️⃣ Models

```python
class Seller(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):
    name = models.CharField(max_length=100)
    seller = models.ForeignKey(Seller, on_delete=models.CASCADE)
```

👉 ekhane clearly:
**1 Seller → Many Product**

---

## 2️⃣ Nested URL Structure

```
/sellers/          → all sellers
/sellers/1/        → single seller
/sellers/1/products/ → seller 1 er sob product
/sellers/1/products/5/ → specific product
```

👉 ei tai holo nested routing 🔥

---

## 3️⃣ Install package

```bash
pip install drf-nested-routers
```

---

## 4️⃣ urls.py (Main part ⚡)

```python
from rest_framework_nested import routers
from .views import SellerViewSet, ProductViewSet

router = routers.SimpleRouter()
router.register(r'sellers', SellerViewSet)

# nested router
seller_router = routers.NestedSimpleRouter(
    router,
    r'sellers',
    lookup='seller'
)

seller_router.register(
    r'products',
    ProductViewSet,
    basename='seller-products'
)

urlpatterns = router.urls + seller_router.urls
```

---

## 5️⃣ ViewSet (Most Important ⚠️)

```python
class ProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(
            seller_id=self.kwargs['seller_pk']
        )
```

👉 🔥 KEY POINT:

* `seller_pk` automatically URL theke ashbe
* tumi manually filter korba

---

## 6️⃣ API Call Example

### 👉 GET

```
GET /sellers/1/products/
```

✔️ Output:

```
seller 1 er sob product
```

---

### 👉 POST

```
POST /sellers/1/products/
```

```json
{
  "name": "Laptop"
}
```

👉 create korar time e:

```python
def perform_create(self, serializer):
    serializer.save(seller_id=self.kwargs['seller_pk'])
```

---

# ⚡ Flow ta bujho

```
URL: /sellers/1/products/

→ router detect korlo
→ seller_pk = 1
→ ViewSet e gelo
→ get_queryset() filter korlo
→ sudhu seller 1 er data ashlo
```

---

# 🧩 Real-life Ecommerce Mapping (Important for you)

Use nested routing for:

### ✅ Good Use Cases

```
/sellers/5/products/
/products/10/reviews/
/orders/2/items/
```

### ❌ Avoid

```
/categories/ (no parent needed)
/products/ (global list)
```

---

# ⚠️ Common Mistake

❌ filter na kora:

```python
Product.objects.all()
```

✔️ correct:

```python
Product.objects.filter(seller_id=self.kwargs['seller_pk'])
```

---

# 🚀 Short Summary

👉 Nested Routing =
**Parent resource er under e child resource show kora**

👉 Formula:

```
/parent/{id}/child/
```

---

# 💡 Pro Insight (Senior Level)

* Small project → use `@action`
* Large scalable system (like your ecommerce) → use nested routers

---

👉 chaile ami tomar jonno
**full ecommerce nested routing structure (Seller, Product, Cart, Order)** ready kore dite pari 🔥


--------
Nice 🔥—tomar ecommerce system er jonno ekta **production-ready nested routing structure** diye dichhi (Seller, Product, Cart, Order)।

আমি এমনভাবে বানাচ্ছি যাতে তুমি **direct Django project e use korte paro** ✅

---

# 🧠 🏗️ Full Structure Overview

```text
User (Buyer / Seller)
│
├── Seller
│   └── Products
│       └── Reviews
│
├── Cart (Buyer)
│   └── CartItems
│
└── Order
    └── OrderItems
```

---

# 🔥 Final API Structure (IMPORTANT)

```http
# Seller + Product
/sellers/
/sellers/{seller_id}/products/
/sellers/{seller_id}/products/{product_id}/

# Global product
/products/
/products/{id}/

# Cart
/cart/
/cart/{cart_id}/items/

# Order
/orders/
/orders/{order_id}/items/
```

👉 🔥 Mix of **nested + flat routing (best practice)**

---

# ⚙️ 1️⃣ Models (Simplified but scalable)

```python
from django.db import models
from django.contrib.auth import get_user_model

User = get_user_model()


class Seller(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)


class Product(models.Model):
    seller = models.ForeignKey(Seller, on_delete=models.CASCADE)
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)


class Cart(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)


class CartItem(models.Model):
    cart = models.ForeignKey(Cart, on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField()


class Order(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)


class OrderItem(models.Model):
    order = models.ForeignKey(Order, on_delete=models.CASCADE)
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField()
```

---

# ⚙️ 2️⃣ urls.py (CORE PART ⚡)

```python
from rest_framework_nested import routers
from .views import *

router = routers.DefaultRouter()

# Seller
router.register(r'sellers', SellerViewSet)

# Product (global)
router.register(r'products', ProductViewSet)

# Cart
router.register(r'cart', CartViewSet)

# Order
router.register(r'orders', OrderViewSet)


# 🔥 Seller → Products
seller_router = routers.NestedSimpleRouter(
    router,
    r'sellers',
    lookup='seller'
)
seller_router.register(
    r'products',
    SellerProductViewSet,
    basename='seller-products'
)


# 🔥 Cart → Items
cart_router = routers.NestedSimpleRouter(
    router,
    r'cart',
    lookup='cart'
)
cart_router.register(
    r'items',
    CartItemViewSet,
    basename='cart-items'
)


# 🔥 Order → Items
order_router = routers.NestedSimpleRouter(
    router,
    r'orders',
    lookup='order'
)
order_router.register(
    r'items',
    OrderItemViewSet,
    basename='order-items'
)


urlpatterns = (
    router.urls +
    seller_router.urls +
    cart_router.urls +
    order_router.urls
)
```

---

# ⚙️ 3️⃣ ViewSets (KEY LOGIC ⚠️)

## 🟢 Seller Product ViewSet (Nested)

```python
class SellerProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(
            seller_id=self.kwargs['seller_pk']
        )

    def perform_create(self, serializer):
        serializer.save(
            seller_id=self.kwargs['seller_pk']
        )
```

---

## 🟢 Cart Items

```python
class CartItemViewSet(viewsets.ModelViewSet):
    serializer_class = CartItemSerializer

    def get_queryset(self):
        return CartItem.objects.filter(
            cart_id=self.kwargs['cart_pk']
        )

    def perform_create(self, serializer):
        serializer.save(
            cart_id=self.kwargs['cart_pk']
        )
```

---

## 🟢 Order Items

```python
class OrderItemViewSet(viewsets.ModelViewSet):
    serializer_class = OrderItemSerializer

    def get_queryset(self):
        return OrderItem.objects.filter(
            order_id=self.kwargs['order_pk']
        )

    def perform_create(self, serializer):
        serializer.save(
            order_id=self.kwargs['order_pk']
        )
```

---

## 🟢 Global Product ViewSet

```python
class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

# ⚡ 🔥 Important Design Decisions

## ✅ কেন mix routing ব্যবহার করছি?

### Nested:

✔ seller → products
✔ cart → items
✔ order → items

### Flat:

✔ products (global browsing)

👉 Daraz / Amazon same concept use kore

---

# 🧠 Advanced Logic (VERY IMPORTANT)

## 🟡 Buyer multiple seller product কিনলে?

👉 Cart example:

```http
/cart/1/items/
```

```json
[
  { "product": 1, "seller": 2 },
  { "product": 5, "seller": 9 }
]
```

👉 Order create time:

* same order
* multiple seller
* backend ভাগ করবে payment 🔥

---

# 🚀 Senior Level Improvement

👉 Add later:

* Payment model
* Transaction per seller
* Commission system
* Order status tracking

---

# 🧩 Summary

👉 Nested routing use korba:

* Seller → Product
* Cart → CartItem
* Order → OrderItem

👉 Flat routing:

* Product browsing

👉 Always remember:

```python
self.kwargs['seller_pk']
self.kwargs['cart_pk']
self.kwargs['order_pk']
```

---

## 🔥 Next Step (I recommend)

Chaile ami next e tomake dibo:

✅ Full **Serializer + Validation**
✅ JWT Auth (Buyer/Seller role)
✅ Payment flow design
✅ Admin control system

Just bolo 👍
Nice 🔥—eta bujhle nested router fully clear hoye jabe. Cholo step-by-step dekhi **nested router er moddhe ViewSet kivabe kaj kore** 👇

---

# 🧠 Core Idea

👉 Nested router **URL banay**
👉 ViewSet **oi URL er request handle kore**

---

# 🔥 Example Setup

```python
# urls.py
router.register(r'sellers', SellerViewSet)

seller_router = NestedSimpleRouter(
    router,
    r'sellers',
    lookup='seller'
)

seller_router.register(
    r'products',
    SellerProductViewSet,
    basename='seller-products'
)
```

---

# ⚡ URL jokhon hit kore

```http
GET /sellers/5/products/
```

👉 ekhon dekho internally ki hoy 👇

---

# 🧩 Step-by-step Flow

```text
1. URL hit: /sellers/5/products/

2. Nested router match kore:
   → sellers/{seller_pk}/products/

3. lookup='seller' thakar jonno:
   → seller_pk = 5

4. DRF call kore:
   → SellerProductViewSet

5. kwargs e data pathay:
   → self.kwargs = { "seller_pk": 5 }

6. ViewSet run hoy:
   → get_queryset()

7. filtered data return hoy
```

---

# 🔥 ViewSet er vitore actual kaj

```python
class SellerProductViewSet(ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(
            seller_id=self.kwargs['seller_pk']   # 🔥 main magic
        )
```

👉 ekhanei main logic:

* URL theke `seller_pk` nilo
* oi seller er product filter korlo

---

# ⚡ POST request e ki hoy?

```http
POST /sellers/5/products/
```

```json
{
  "name": "Laptop",
  "price": 1000
}
```

👉 ViewSet e:

```python
def perform_create(self, serializer):
    serializer.save(
        seller_id=self.kwargs['seller_pk']
    )
```

👉 result:

* automatically seller = 5 assign holo 🔥

---

# 🧠 Important Concept

👉 Nested router **automatic filter kore na ❌**

👉 ViewSet e manually korte hoy ✅

---

# ❌ Common mistake

```python
def get_queryset(self):
    return Product.objects.all()   ❌
```

👉 eta dile:

* sob seller er product chole ashbe 😵

---

# 🧩 Full Mapping

```text
URL                      → ViewSet
-----------------------------------------
/sellers/                → SellerViewSet
/sellers/5/              → SellerViewSet
/sellers/5/products/     → SellerProductViewSet
```

---

# 🔥 Real Ecommerce Flow

```text
/sellers/2/products/
→ seller 2 er product

/cart/1/items/
→ cart 1 er item

/orders/10/items/
→ order 10 er item
```

👉 sob jaygay same logic 🔁

---

# 🚀 Short Formula

```text
Nested URL
→ lookup_pk generate
→ kwargs e pass
→ ViewSet filter kore
```

---

# 🎯 Final Summary

👉 Nested router:

✔ URL create kore
✔ parent id pass kore (`seller_pk`)

👉 ViewSet:

✔ kwargs theke id ney
✔ queryset filter kore
✔ create/update handle kore

---

👉 jodi chao next e ami tomake
**diagram diye pura request lifecycle (client → router → viewset → database)** visual kore bujhai 🔥
Haan 👍—**`seller_id` actually model er sathei related**. Cholo clear kori step-by-step 👇

---

# 🧠 `seller_id` ki?

👉 Short answer:
✔️ **Haan — eta model er field theke automatically ashe**
❗ but directly tumi define koro na

---

# 🔥 Model dekho

```python id="yox35l"
class Product(models.Model):
    seller = models.ForeignKey(Seller, on_delete=models.CASCADE)
```

👉 ekhane tumi likhso:

```python id="mjbqmn"
seller = ForeignKey(...)
```

---

# ⚡ Django internally create kore:

```python id="eibaf0"
seller_id
```

👉 mane:

* `seller` = object reference
* `seller_id` = actual database column (integer)

---

# 🧩 Example

```python id="dv2m8i"
product = Product.objects.get(id=1)

product.seller     # 👉 Seller object
product.seller_id  # 👉 Seller er ID (int)
```

---

# 🔥 Database level e

```text id="e6m9pj"
Product Table:

id | name | seller_id
---------------------
1  | pen  | 5
```

👉 ekhane:

* `seller_id` = real column

---

# ⚡ Nested router e use

```python id="a4b3yl"
Product.objects.filter(
    seller_id=self.kwargs['seller_pk']
)
```

👉 ekhane:

* `seller_pk` → URL theke asche
* `seller_id` → DB column

👉 match korche 🔥

---

# ❌ Alternative way

```python id="4wlt3d"
Product.objects.filter(
    seller__id=self.kwargs['seller_pk']
)
```

✔️ eta o correct
👉 but `seller_id` faster (direct column access)

---

# 🧠 Important difference

| Field       | Meaning           |
| ----------- | ----------------- |
| `seller`    | relation (object) |
| `seller_id` | actual integer ID |

---

# 🔥 Create er time e

```python id="4k92v5"
serializer.save(
    seller_id=self.kwargs['seller_pk']
)
```

👉 OR:

```python id="i4a2gr"
serializer.save(
    seller=Seller.objects.get(id=self.kwargs['seller_pk'])
)
```

✔️ duita same kaj kore
👉 but first one faster 🔥

---

# 🚀 Short Summary

👉 `seller_id`:

✔ model theke auto create hoy
✔ DB column
✔ integer value

👉 `seller`:

✔ relation object

---

# 🎯 Final Understanding

```text id="5okn30"
ForeignKey field → Django auto creates → <field_name>_id
```

---

# 🧠 ForeignKey Relation Basics

Django model e:

```python
class Product(models.Model):
    seller = models.ForeignKey(Seller, on_delete=models.CASCADE)
```

* `seller` = **ForeignKey field**
* ForeignKey mane: ei model **onno model er ekta record er sathe link** ache
* Database level e, link **always primary key (id) diye** hoy

---

# 🔥 Database Representation

```text
Seller Table:
id | name
-----------
1  | John
2  | Alice

Product Table:
id | name     | seller_id
------------------------
1  | Laptop   | 1
2  | Mouse    | 2
```

* `seller_id` = actual integer value (Seller table er `id`)
* `product.seller` = Django ORM er object reference
* `product.seller_id` = database column (integer)

---

# ⚡ How ORM uses it

```python
product = Product.objects.get(id=1)

product.seller     # 👉 <Seller: John>
product.seller_id  # 👉 1
```

* `product.seller` → object
* `product.seller_id` → primary key value

---

# 🧩 Query example

```python
# all products by seller 1
Product.objects.filter(seller_id=1)
```

✔️ efficient, direct column query

```python
# same using object
seller = Seller.objects.get(id=1)
Product.objects.filter(seller=seller)
```

* Both give same result
* First one slightly faster

---

# 🔥 Nested Router / ViewSet Context

```python
class SellerProductViewSet(ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(
            seller_id=self.kwargs['seller_pk']  # 🔥 URL theke pk match
        )

    def perform_create(self, serializer):
        serializer.save(
            seller_id=self.kwargs['seller_pk']  # 🔥 link to parent
        )
```

* Nested URL → `/sellers/5/products/`
* `seller_pk = 5` → automatically linked with `seller_id`

---

# ✅ Key Points

1. ForeignKey always connect **parent model primary key (usually id)** diye
2. Django automatically create kore `<field_name>_id` database column
3. ORM e tumi object or id duita use korte paro
4. Nested routing + ForeignKey → perfect combo for parent-child resource

---

# 🧠 Short Formula

```text
Child model ForeignKey → Parent model PK
URL (nested) → kwargs['parent_pk']
ViewSet → filter on child using parent_pk
```

---
# Complete Example


Cholo ami tomake **nested router + ForeignKey er complete example** diye dekhi, e-commerce chara, ekta simple **Blog and Comment** system diye. Eta fully working pattern bujhabe 🔥

---

# 🧩 Models (Blog → Comment)

```python
# models.py
from django.db import models

class Blog(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()

    def __str__(self):
        return self.title

class Comment(models.Model):
    blog = models.ForeignKey(Blog, on_delete=models.CASCADE, related_name='comments')
    text = models.TextField()

    def __str__(self):
        return f"Comment on {self.blog.title}"
```

* `Comment.blog` → **ForeignKey to Blog**
* DB e automatically column `blog_id` create hoy
* `Comment.blog_id` = Blog er primary key (id)

---

# 🧩 Serializers

```python
# serializers.py
from rest_framework import serializers
from .models import Blog, Comment

class BlogSerializer(serializers.ModelSerializer):
    class Meta:
        model = Blog
        fields = '__all__'

class CommentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Comment
        fields = '__all__'
```

---

# 🧩 ViewSets

```python
# views.py
from rest_framework import viewsets
from .models import Blog, Comment
from .serializers import BlogSerializer, CommentSerializer

class BlogViewSet(viewsets.ModelViewSet):
    queryset = Blog.objects.all()
    serializer_class = BlogSerializer

class BlogCommentViewSet(viewsets.ModelViewSet):
    serializer_class = CommentSerializer

    def get_queryset(self):
        return Comment.objects.filter(blog_id=self.kwargs['blog_pk'])

    def perform_create(self, serializer):
        serializer.save(blog_id=self.kwargs['blog_pk'])
```

✅ Key point:

* Nested URL theke `blog_pk` peye child query filter kore
* `perform_create` e save korar somoy **foreign key set kore**

---

# 🧩 URLs (Nested Router)

```python
# urls.py
from django.urls import path, include
from rest_framework_nested import routers
from .views import BlogViewSet, BlogCommentViewSet

# parent router
router = routers.DefaultRouter()
router.register(r'blogs', BlogViewSet)

# nested router
blog_router = routers.NestedSimpleRouter(router, r'blogs', lookup='blog')
blog_router.register(r'comments', BlogCommentViewSet, basename='blog-comments')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(blog_router.urls)),
]
```

---

# 🧩 Resulting URLs

| URL                  | Method               | Description                        |
| -------------------- | -------------------- | ---------------------------------- |
| /blogs/              | GET/POST             | List or create blogs               |
| /blogs/1/            | GET/PUT/PATCH/DELETE | Single blog                        |
| /blogs/1/comments/   | GET/POST             | List or create comments for blog 1 |
| /blogs/1/comments/5/ | GET/PUT/PATCH/DELETE | Single comment under blog 1        |

---

# 🧩 How It Works

1. Client hits: `/blogs/2/comments/`
2. Nested router captures `blog_pk=2`
3. `BlogCommentViewSet.get_queryset()` filter kore **blog_id=2**
4. Data return kore

For POST:

```json
POST /blogs/2/comments/
{
    "text": "Great blog!"
}
```

* `perform_create` automatically sets `blog_id=2`

---

# ✅ Summary

* Nested router = URL structure + kwargs
* ForeignKey = parent-child relation
* ViewSet = kwargs use kore queryset filter + foreign key set

---

💡 Eta **e-commerce chara complete nested router example**

* Blog = parent model
* Comment = child model

---

Jodi chao ami ekta **diagram diye full flow (client → nested router → viewset → DB → response)** o show kore dite pari, jevabe full process hoy, next step clear hobe.

Tumi chao ami eta ready kori?
Perfect! 😄 Cholo ami tomake **Category → Product** nested routing example diye dekhi, **ei khetre ForeignKey thakbe**, jate fully natural nested API hoy.

---

# 🧩 Scenario

* **Parent:** Category
* **Child:** Product
* Product model er **ForeignKey → Category**
* Nested URL: `/categories/5/products/` → automatically filter kore oi category er products

---

# 🧩 Models

```python id="catprod1"
# models.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

    def __str__(self):
        return self.name

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.name
```

* `Product.category` → ForeignKey → automatically DB column `category_id` create kore
* `related_name='products'` → optional, ORM e `category.products.all()` use korte paro

---

# 🧩 Serializers

```python id="catprod2"
# serializers.py
from rest_framework import serializers
from .models import Category, Product

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'
```

---

# 🧩 ViewSets

```python id="catprod3"
# views.py
from rest_framework import viewsets
from .models import Category, Product
from .serializers import CategorySerializer, ProductSerializer

class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

class CategoryProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        # Nested router theke category_pk pawa jabe
        return Product.objects.filter(category_id=self.kwargs['category_pk'])

    def perform_create(self, serializer):
        # automatically parent category assign
        serializer.save(category_id=self.kwargs['category_pk'])
```

✅ Key point:

* Nested URL theke `category_pk` automatically `kwargs` e asche
* Filter + create er time ForeignKey automatically assign hocche

---

# 🧩 URLs (Nested Router)

```python id="catprod4"
# urls.py
from django.urls import path, include
from rest_framework_nested import routers
from .views import CategoryViewSet, CategoryProductViewSet

# parent router
router = routers.DefaultRouter()
router.register(r'categories', CategoryViewSet)

# nested router
category_router = routers.NestedSimpleRouter(router, r'categories', lookup='category')
category_router.register(r'products', CategoryProductViewSet, basename='category-products')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(category_router.urls)),
]
```

---

# 🧩 Resulting URLs

| URL                       | Method               | Description                              |
| ------------------------- | -------------------- | ---------------------------------------- |
| /categories/              | GET/POST             | List or create categories                |
| /categories/1/            | GET/PUT/PATCH/DELETE | Single category                          |
| /categories/1/products/   | GET/POST             | List or create products under category 1 |
| /categories/1/products/5/ | GET/PUT/PATCH/DELETE | Single product under category 1          |

---

# 🧩 How It Works

1. Client hits `/categories/3/products/`
2. Nested router captures `category_pk = 3`
3. `CategoryProductViewSet.get_queryset()` → filter by `category_id=3`
4. GET request → only products in category 3
5. POST request → product automatically assigned to category 3

---

# 🔥 Notes

* ForeignKey thakle nested router **fully automatic + natural**
* `category_pk` URL theke ViewSet e pass hoye filtering + creation smooth
* Performance better because direct DB column (`category_id`) use hocche

---

Jodi chao ami eta next step e **diagram + request flow** diye visual kore dekhai, jevabe request → nested router → ViewSet → DB → response hoy 🔥

Chao ami eta ready kori?
Haan! 😄 totally possible — **nested router er ViewSet e sob operation (GET, POST, PUT, DELETE) kora jabe**, sudhu **`get_queryset`** + **`perform_create`** + optional **`perform_update`/`perform_destroy`** properly handle korle. `lookup_id` (nested URL theke) use kore sob kaj hoy 🔥

Cholo step-by-step clean example dei using **Category → Product** scenario.

---

# 🧩 Models

```python
# models.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

---

# 🧩 Serializers

```python
# serializers.py
from rest_framework import serializers
from .models import Category, Product

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'
```

---

# 🧩 ViewSets (Nested ViewSet e sob operation)

```python
# views.py
from rest_framework import viewsets
from .models import Category, Product
from .serializers import CategorySerializer, ProductSerializer
from rest_framework.response import Response
from rest_framework import status

class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

class CategoryProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        # nested URL theke category_pk use kore filter
        return Product.objects.filter(category_id=self.kwargs['category_pk'])

    def perform_create(self, serializer):
        serializer.save(category_id=self.kwargs['category_pk'])

    # Optional: perform_update / perform_destroy if custom logic needed
    def perform_update(self, serializer):
        # ensure product stays in same category
        serializer.save(category_id=self.kwargs['category_pk'])

    def perform_destroy(self, instance):
        instance.delete()
```

✅ Key Points:

* `get_queryset()` → GET, list, retrieve, etc. sob operation e automatic filter
* `perform_create()` → POST e nested parent assign
* `perform_update()` → PUT/PATCH e parent maintain
* `perform_destroy()` → DELETE

---

# 🧩 URLs (Nested Router)

```python
from rest_framework_nested import routers
from django.urls import path, include
from .views import CategoryViewSet, CategoryProductViewSet

router = routers.DefaultRouter()
router.register(r'categories', CategoryViewSet)

category_router = routers.NestedSimpleRouter(router, r'categories', lookup='category')
category_router.register(r'products', CategoryProductViewSet, basename='category-products')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(category_router.urls)),
]
```

---

# 🧩 URLs & Operations

| URL                       | Method               | Description                           |
| ------------------------- | -------------------- | ------------------------------------- |
| /categories/              | GET/POST             | List/create categories                |
| /categories/1/            | GET/PUT/PATCH/DELETE | Single category                       |
| /categories/1/products/   | GET/POST             | List/create products under category 1 |
| /categories/1/products/5/ | GET/PUT/PATCH/DELETE | Single product under category 1       |

---

# 🔥 Notes

* **All CRUD operation** possible in nested ViewSet
* `kwargs['category_pk']` → automatically URL theke asche, sob filter er jonno use hobe
* DB ForeignKey thakle fully natural, nested URL → parent ID automatically pass

---

Ami chai tahole ami **ekta fully working diagram** banai jevabe **nested router → ViewSet → get_queryset / perform_create → DB → response** flow hoy, sob operation clearly visual dekhabe 🔥

Chao ami eta ready kori?
Haan, exactly 😄—`category_router` er khetre **parent router boshe**, ei parent router theke start hobe nested router. Cholo step-by-step bujhi 🔥

---

# 🧩 Concept

```python id="nestedconcept"
router = DefaultRouter()
router.register(r'categories', CategoryViewSet)   # ← parent router

category_router = NestedSimpleRouter(
    router,              # ← parent router ekhanei pass hoy
    r'categories',       # ← parent route name
    lookup='category'    # ← URL e parameter name
)
category_router.register(
    r'products', 
    CategoryProductViewSet,
    basename='category-products'
)
```

* `router` → parent router, jekhane main resource (`categories`) register kora hoy
* `category_router` → nested router, je **parent router er URL** (`/categories/`) diye start hobe
* `lookup='category'` → nested URL e parent ID pawa jabe (`category_pk`)

---

# 🧩 URL Mapping

| Router          | URL Start    | Child Resource                        |
| --------------- | ------------ | ------------------------------------- |
| router          | /categories/ | CategoryViewSet                       |
| category_router | /categories/ | `/categories/<category_pk>/products/` |

---

# 🧩 Key Points

1. **Parent router must exist first**
2. Nested router always **starts from parent router URL**
3. `lookup` → parent ID parameter name (`kwargs['category_pk']`)
4. Nested router **automatically appends child route**

---

# 🔥 Example URL Flow

```text
/categories/           → CategoryViewSet (parent router)
/categories/3/         → CategoryViewSet retrieve category 3
/categories/3/products/ → CategoryProductViewSet (nested router)
/categories/3/products/5/ → CategoryProductViewSet retrieve product 5 in category 3
```

---

💡 **Summary**:

* Nested router **always need parent router**
* Parent router er URL name (`r'categories'`) diye start hoy
* ViewSet er `get_queryset` e `kwargs['category_pk']` automatically available

---

Jodi chao ami **diagram diye full parent → nested router → ViewSet → DB flow** dekhiye dekhai jekhane sob CRUD operation handle hoy.
Tumi chai ami eta ready kori?
