Since you're learning **Django REST Framework for senior-level backend development**, understanding **Router**, **Nested Router**, and **API endpoint design** is extremely important. Many beginners know how to create endpoints, but senior developers know **when to use nested routes and when not to**.

---

# 1. What is a Router?

Without a router, you manually write every URL.

```python
urlpatterns = [
    path("products/", ProductListAPIView.as_view()),
    path("products/<int:pk>/", ProductDetailAPIView.as_view()),
]
```

With a **DRF Router**, you only register the ViewSet.

```python
router = DefaultRouter()
router.register("products", ProductViewSet)

urlpatterns = router.urls
```

The router automatically creates all CRUD endpoints.

```
GET      /products/
POST     /products/

GET      /products/1/
PUT      /products/1/
PATCH    /products/1/
DELETE   /products/1/
```

Instead of writing six URLs manually, DRF generates them automatically.

---

# 2. How Router Works Internally

Suppose you have

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

When you register

```python
router.register("products", ProductViewSet)
```

DRF internally maps HTTP methods.

| HTTP Method | URL          | ViewSet Method   |
| ----------- | ------------ | ---------------- |
| GET         | /products/   | list()           |
| POST        | /products/   | create()         |
| GET         | /products/5/ | retrieve()       |
| PUT         | /products/5/ | update()         |
| PATCH       | /products/5/ | partial_update() |
| DELETE      | /products/5/ | destroy()        |

The router simply converts URLs into ViewSet actions.

---

# 3. Example Project

Imagine an E-Commerce project.

```
Category
   │
   ├── Product
            │
            ├── Review
```

Models

```
Category

    Electronics

Product

    iPhone

Review

    ⭐⭐⭐⭐⭐
```

Relationship

```
Category

    has many Products

Product

    belongs to Category

Product

    has many Reviews
```

---

# 4. Flat API Design

The simplest design is independent resources.

```
/categories/
/products/
/reviews/
```

Example

```
GET /categories/

GET /products/

GET /reviews/
```

To find reviews of product 5,

```
GET /reviews/?product=5
```

This is called **Flat Resource Design**.

Advantages

* Simple
* Scalable
* Easy caching
* Common in large APIs

---

# 5. Nested Router

Sometimes a child resource only makes sense inside its parent.

Instead of

```
GET /reviews/?product=5
```

you write

```
GET /products/5/reviews/
```

The URL itself explains

> Reviews belonging to Product 5.

That's why Nested Router exists.

---

# 6. Nested Router Example

Register parent router.

```python
router = DefaultRouter()

router.register(
    "products",
    ProductViewSet
)
```

Create nested router.

```python
product_router = NestedDefaultRouter(
    router,
    "products",
    lookup="product"
)

product_router.register(
    "reviews",
    ReviewViewSet,
    basename="product-reviews"
)
```

Generated endpoints

```
GET /products/

GET /products/1/

GET /products/1/reviews/

POST /products/1/reviews/

GET /products/1/reviews/8/

DELETE /products/1/reviews/8/
```

Notice how the product id becomes part of the URL.

---

# 7. How Nested Router Passes IDs

Suppose

```
GET

/products/5/reviews/
```

The router extracts

```
product_pk = 5
```

Inside the ViewSet

```python
class ReviewViewSet(ModelViewSet):

    def get_queryset(self):
        return Review.objects.filter(
            product_id=self.kwargs["product_pk"]
        )
```

`self.kwargs`

```
{
    "product_pk": 5
}
```

The nested router automatically injects the parent object's ID.

---

# 8. Multi-Level Nested Router

```
Category
      ↓
Product
      ↓
Review
```

Endpoints become

```
/categories/

/categories/2/

/categories/2/products/

/categories/2/products/8/

/categories/2/products/8/reviews/

/categories/2/products/8/reviews/12/
```

URL hierarchy

```
Category
   ↓
Product
   ↓
Review
```

---

# 9. What Happens During a Request?

User requests

```
GET

/categories/3/products/10/reviews/
```

The router extracts

```
category_pk = 3

product_pk = 10
```

Your ViewSet can filter

```python
Review.objects.filter(
    product_id=10,
    product__category_id=3
)
```

This guarantees the review belongs to that product in that category.

---

# 10. Nested Serializer vs Nested Router

Many developers confuse these concepts.

## Nested Serializer

Controls **response data**.

```json
{
    "id":1,
    "name":"Electronics",
    "products":[
        {
            "id":5,
            "name":"Laptop"
        }
    ]
}
```

This changes **JSON structure**.

---

## Nested Router

Controls **URL structure**.

```
/categories/1/products/
```

This changes **API endpoints**.

They solve different problems and can be used together.

---

# 11. API Endpoint Design

Suppose you're building an e-commerce backend.

## Categories

```
GET     /categories/

POST    /categories/

GET     /categories/3/

PATCH   /categories/3/

DELETE  /categories/3/
```

---

## Products

```
GET     /products/

POST    /products/

GET     /products/7/

PATCH   /products/7/

DELETE  /products/7/
```

---

## Reviews

```
GET     /reviews/

POST    /reviews/

GET     /reviews/12/
```

---

## Reviews Inside Product

```
GET

/products/7/reviews/

POST

/products/7/reviews/
```

---

# 12. Which Design Should You Choose?

### Good

```
GET /products/5/reviews/
```

Reason:

The review belongs to a product.

---

### Better

```
GET /orders/50/items/
```

An order contains items.

---

### Good

```
GET /courses/4/lessons/
```

A lesson belongs to a course.

---

### Avoid

```
/users/5/orders/8/items/3/payments/2/
```

Very deep nesting is difficult to maintain.

A good rule is **maximum 2–3 levels** of nesting.

---

# 13. Real-World Endpoint Examples

### E-commerce

```
/products/
/products/5/reviews/
/orders/
/orders/9/items/
/cart/
/wishlist/
```

---

### Learning Management System (LMS)

```
/courses/
/courses/5/modules/
/modules/10/lessons/
/lessons/25/comments/
```

---

### Blog

```
/posts/
/posts/5/comments/
/authors/
/tags/
```

---

### Exam Management System

```
/courses/

/courses/1/students/

/courses/1/exams/

/courses/1/exams/8/questions/

/courses/1/exams/8/submissions/
```

---

# 14. Senior Backend Design Principles

A senior backend developer usually follows these guidelines:

* **Use flat resources** (`/products/`) for top-level entities.
* **Use nested routes** only when the child resource has a strong parent-child relationship (e.g., `/products/{id}/reviews/`).
* **Keep nesting shallow**, ideally no more than 2–3 levels.
* **Use plural nouns** for resource names (`/products`, `/orders`, `/reviews`).
* **Rely on HTTP methods** (`GET`, `POST`, `PATCH`, `DELETE`) instead of putting actions in URLs.
* **Separate URL design from response design**: nested routers define endpoint hierarchy, while nested serializers define JSON structure. 

---

## Next Topic (Highly Recommended)

The next advanced DRF topic to learn is:

1. **DefaultRouter vs SimpleRouter**
2. **basename**
3. **lookup_field**
4. **Custom `@action` endpoints**
5. **How `reverse()` works with routers**
6. **Building RESTful APIs for large projects (Amazon-style endpoint architecture)**

These topics will help you understand how experienced DRF developers design clean, scalable APIs.
Excellent roadmap. These topics are exactly what you should master if your goal is to become a **Senior Django REST Framework Backend Developer**. Here's the order I recommend because each topic builds on the previous one.

---

# DRF Advanced Routing Roadmap

```
Module 1
├── SimpleRouter
├── DefaultRouter
├── Router Internals

Module 2
├── basename
├── lookup_field
├── lookup_url_kwarg

Module 3
├── Custom @action
├── detail=True
├── detail=False
├── URL generation

Module 4
├── reverse()
├── Hyperlinked serializers
├── URL names
├── Router naming

Module 5
├── Large API architecture
├── Versioning
├── Nested resources
├── API consistency

Module 6
├── Production endpoint design
├── Authentication endpoints
├── Search
├── Pagination
├── Filtering
```

---

# Lesson 1 — SimpleRouter vs DefaultRouter

Most beginners don't know why DRF has two routers.

---

## What is a Router?

A router automatically creates URLs for a ViewSet.

Instead of writing

```python
urlpatterns = [
    path("products/", ...),
    path("products/<int:pk>/", ...),
]
```

you simply write

```python
router = DefaultRouter()
router.register("products", ProductViewSet)
```

---

# SimpleRouter

```python
from rest_framework.routers import SimpleRouter

router = SimpleRouter()

router.register(
    "products",
    ProductViewSet
)
```

Generated URLs

```
GET     /products/

POST    /products/

GET     /products/1/

PUT     /products/1/

PATCH   /products/1/

DELETE  /products/1/
```

Nothing else.

---

# DefaultRouter

```python
from rest_framework.routers import DefaultRouter

router = DefaultRouter()

router.register(
    "products",
    ProductViewSet
)
```

Generated URLs

```
GET     /products/

POST    /products/

GET     /products/1/

PUT     /products/1/

PATCH   /products/1/

DELETE  /products/1/

GET     /
```

Notice the extra endpoint.

```
GET /
```

This is called the **API Root**.

Example response

```json
{
    "products": "http://localhost:8000/products/",
    "categories": "http://localhost:8000/categories/",
    "orders": "http://localhost:8000/orders/"
}
```

---

# API Root

Suppose your project has

```python
router.register("products", ProductViewSet)
router.register("categories", CategoryViewSet)
router.register("orders", OrderViewSet)
```

Going to

```
GET /
```

returns

```json
{
    "products": ".../products/",
    "categories": ".../categories/",
    "orders": ".../orders/"
}
```

DRF automatically builds this page.

---

# Another Difference

DefaultRouter also supports optional format suffixes.

```
/products.json

/products.api

/products.xml
```

SimpleRouter does not add these automatically.

---

# Which One Should You Use?

### During development

```
DefaultRouter
```

Reason

* Browsable API
* API root
* Easier testing

---

### Production APIs

Many companies use

```
SimpleRouter
```

because

* Cleaner URLs
* No unnecessary API root
* Better control

Some companies still keep `DefaultRouter` internally for developer convenience.

---

# How Router Builds URLs

When you register

```python
router.register(
    "products",
    ProductViewSet
)
```

DRF internally creates something similar to

```
products-list

products-detail
```

These are URL names.

They are important because many DRF features rely on them, such as `reverse()`, hyperlinks, and serializers.

---

# Router Internals

Imagine this ViewSet:

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
```

Router mapping:

| URL               | HTTP   | ViewSet Method     |
| ----------------- | ------ | ------------------ |
| `/products/`      | GET    | `list()`           |
| `/products/`      | POST   | `create()`         |
| `/products/{pk}/` | GET    | `retrieve()`       |
| `/products/{pk}/` | PUT    | `update()`         |
| `/products/{pk}/` | PATCH  | `partial_update()` |
| `/products/{pk}/` | DELETE | `destroy()`        |

The router simply connects URL patterns to ViewSet actions.

---

# Example Project Structure

```
api/
│
├── routers.py
├── urls.py
├── views.py
├── serializers.py
└── models.py
```

`routers.py`

```python
from rest_framework.routers import DefaultRouter
from .views import ProductViewSet, CategoryViewSet

router = DefaultRouter()

router.register("products", ProductViewSet)
router.register("categories", CategoryViewSet)
```

`urls.py`

```python
from django.urls import path, include
from .routers import router

urlpatterns = [
    path("", include(router.urls)),
]
```

This keeps routing organized as your project grows.

---

# Interview Questions

### Q1. Difference between SimpleRouter and DefaultRouter?

**Answer:**

* `SimpleRouter` generates CRUD endpoints only.
* `DefaultRouter` generates CRUD endpoints plus an API root and optional format suffix support.

---

### Q2. Which router should you use?

**Answer:**

* Development: `DefaultRouter`
* Production: depends on project needs; many teams prefer `SimpleRouter` for cleaner APIs, while others keep `DefaultRouter` if the API root is useful.

---

### Q3. Does the router execute database queries?

**Answer:**

No. The router only maps URLs to ViewSet actions. Database queries are executed inside methods like `list()`, `retrieve()`, or `get_queryset()`.

---

# Practice Exercise

Create three `ModelViewSet`s:

* `CategoryViewSet`
* `ProductViewSet`
* `OrderViewSet`

Then:

1. Register them using `SimpleRouter` and inspect the generated URLs.
2. Replace it with `DefaultRouter` and compare the output.
3. Visit the API root (`/`) when using `DefaultRouter`.
4. Use Django's `show_urls` command (if installed) or inspect `router.urls` in the Django shell to see the generated URL patterns.

---

## Next Lesson

The next lesson will cover **`basename`** in depth:

* Why `basename` exists
* When it is required
* Why omitting it sometimes raises an error
* How DRF generates URL names from `basename`
* How `reverse()` depends on it
* Common interview questions and production examples

Understanding `basename` is essential because it underpins URL naming, reversing, and custom actions in DRF.

--------
# Module 2 — `basename`, `lookup_field`, `lookup_url_kwarg`

This module is one of the most misunderstood parts of DRF. A senior Django developer must understand **how routers identify ViewSets**, **how URLs are generated**, and **how objects are looked up**.

---

# Module Overview

```
Module 2

├── Lesson 1: basename
├── Lesson 2: lookup_field
├── Lesson 3: lookup_url_kwarg
├── Lesson 4: basename + reverse()
├── Lesson 5: basename with @action
├── Lesson 6: Production Examples
```

---

# Lesson 1 — basename

## What is basename?

**basename is the base name used by the router to generate URL names.**

Suppose you register

```python
router.register(
    "products",
    ProductViewSet
)
```

DRF automatically creates URL names.

```
products-list

products-detail
```

Where did **products** come from?

It came from **basename**.

---

## How DRF Finds basename Automatically

Suppose

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
```

Router

```python
router.register(
    "products",
    ProductViewSet
)
```

Since the ViewSet has

```python
queryset = Product.objects.all()
```

DRF knows

```
Model = Product
```

So it automatically creates

```
basename = product
```

Generated URL names become

```
product-list
product-detail
```

Notice

```
URL prefix

products

≠

basename

product
```

They are **different concepts**.

| Concept    | Example  |
| ---------- | -------- |
| URL Prefix | products |
| basename   | product  |

---

# URL Prefix vs basename

People often think these are identical.

They are not.

```python
router.register(
    "inventory",
    ProductViewSet
)
```

Generated URL

```
/inventory/
```

Generated URL names

```
product-list

product-detail
```

because basename still comes from the model.

---

# When basename Is Required

Suppose

```python
class ProductViewSet(ModelViewSet):

    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(is_active=True)
```

Notice

```
No queryset attribute.
```

Router cannot determine

* Which model?
* Which basename?

So you'll get an error similar to:

```
'basename' argument not specified, and could not automatically determine the name...
```

---

# Solution

Specify basename manually.

```python
router.register(
    "products",
    ProductViewSet,
    basename="product"
)
```

Now DRF knows

```
product-list

product-detail
```

---

# Another Example

```python
class SaleProductViewSet(ModelViewSet):

    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(on_sale=True)
```

Register

```python
router.register(
    "sale-products",
    SaleProductViewSet,
    basename="sale-product"
)
```

Generated URL names

```
sale-product-list

sale-product-detail
```

---

# How basename Affects reverse()

Suppose

```python
basename="product"
```

Generated names

```
product-list

product-detail
```

Then

```python
from rest_framework.reverse import reverse

reverse(
    "product-list",
    request=request
)
```

returns

```
http://localhost:8000/products/
```

And

```python
reverse(
    "product-detail",
    kwargs={"pk": 5},
    request=request
)
```

returns

```
http://localhost:8000/products/5/
```

Without basename,

reverse cannot find these names.

---

# basename with Multiple ViewSets

Suppose

```
Product
```

needs two APIs.

Normal API

```
/products/
```

Featured API

```
/featured-products/
```

You create

```python
class ProductViewSet(...)
```

and

```python
class FeaturedProductViewSet(...)
```

Register

```python
router.register(
    "products",
    ProductViewSet
)

router.register(
    "featured-products",
    FeaturedProductViewSet,
    basename="featured-product"
)
```

Generated URL names

```
product-list

featured-product-list
```

No conflict.

---

# Common Mistake

Two ViewSets using the same basename.

```python
router.register(
    "products",
    ProductViewSet,
    basename="product"
)

router.register(
    "featured-products",
    FeaturedProductViewSet,
    basename="product"
)
```

Generated names

```
product-list

product-list
```

Conflict.

Always use unique basenames.

---

# When Do You Need basename?

### Not Needed

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
```

DRF can infer it.

---

### Required

```python
class ProductViewSet(ModelViewSet):

    def get_queryset(self):
        ...
```

No `queryset` attribute means you must provide `basename`.

---

### Required

If you're using a `GenericViewSet` or a custom `ViewSet` without a `queryset`.

---

# Interview Questions

### Q1. What is basename?

**Answer:**
It is the base name DRF uses to generate URL names such as `product-list` and `product-detail`.

---

### Q2. When is basename required?

**Answer:**
When DRF cannot automatically determine the model, typically because the ViewSet does not define a `queryset` attribute.

---

### Q3. Does basename affect the URL path?

**Answer:**
No. The URL path comes from the **prefix** passed to `router.register()`. `basename` affects only the generated URL names.

Example:

```python
router.register(
    "inventory",
    ProductViewSet,
    basename="product"
)
```

* URL: `/inventory/`
* URL names: `product-list`, `product-detail`

---

# Lesson 2 — `lookup_field`

By default, DRF retrieves an object using its primary key.

```python
GET /products/5/
```

Internally, DRF performs something equivalent to:

```python
Product.objects.get(pk=5)
```

because the default is:

```python
lookup_field = "pk"
```

You can change this.

Suppose your model has a unique slug:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)
```

Then:

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    lookup_field = "slug"
```

Now your endpoint becomes:

```
GET /products/macbook-pro/
```

DRF internally performs:

```python
Product.objects.get(slug="macbook-pro")
```

This is common in blogs, e-commerce, and CMS applications because slugs are more readable than numeric IDs.

---

# Lesson 3 — `lookup_url_kwarg`

Sometimes the URL parameter name should differ from the model field name.

Example URL:

```
GET /products/macbook-pro/
```

You want the URL keyword to be `product_slug` instead of `slug`.

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    lookup_field = "slug"
    lookup_url_kwarg = "product_slug"
```

Then your URL pattern effectively becomes:

```
/products/<product_slug>/
```

Inside DRF:

```python
self.kwargs["product_slug"]
```

is used to search:

```python
Product.objects.get(slug=...)
```

This is especially useful when working with nested routers where parameter names like `category_pk`, `product_slug`, or `user_uuid` make the code clearer.

---

# Summary

| Concept            | Purpose                                | Example                          |
| ------------------ | -------------------------------------- | -------------------------------- |
| `basename`         | Generates URL names                    | `product-list`, `product-detail` |
| `lookup_field`     | Model field used to retrieve an object | `slug`, `uuid`, `pk`             |
| `lookup_url_kwarg` | URL parameter name used in the route   | `product_slug`, `user_uuid`      |

---

## Practice Exercise

Create a `Product` model with these fields:

```python
id
name
slug
uuid
price
```

Then implement three ViewSets:

1. Default lookup using `pk`.
2. Lookup using `slug`.
3. Lookup using `uuid` while exposing the URL parameter as `product_uuid` via `lookup_url_kwarg`.

This exercise will make the differences between these three concepts very clear.

---

### Next Module (Module 3)

We'll cover **Custom `@action` Endpoints**, including:

* `@action(detail=True)` vs `@action(detail=False)`
* Custom URLs like `/products/{id}/publish/`
* Bulk actions (e.g., `/products/export/`)
* How routers generate action endpoints
* Best practices and interview questions for production APIs

----
# Module 3 — Custom `@action` Endpoints

This is one of the most powerful features of **Django REST Framework ViewSets**. It allows you to create **custom REST endpoints** without creating separate APIViews.

---

# Module Roadmap

```text
Module 3

├── Lesson 1: Why @action exists
├── Lesson 2: detail=True
├── Lesson 3: detail=False
├── Lesson 4: methods=[]
├── Lesson 5: url_path
├── Lesson 6: url_name
├── Lesson 7: permission_classes
├── Lesson 8: serializer_class
├── Lesson 9: Production Examples
├── Lesson 10: Best Practices
├── Lesson 11: Interview Questions
```

---

# Lesson 1 — Why `@action` Exists

A `ModelViewSet` already provides:

```text
GET      /products/
POST     /products/

GET      /products/1/
PUT      /products/1/
PATCH    /products/1/
DELETE   /products/1/
```

But what if you want:

```text
Publish Product

POST /products/1/publish/
```

or

```text
Feature Product

POST /products/1/feature/
```

or

```text
Export Products

GET /products/export/
```

These are **not CRUD operations**.

Instead of creating a new APIView, DRF provides `@action`.

---

# Lesson 2 — detail=True

Imagine a product.

```text
Product

id = 10
```

You want

```text
POST

/products/10/publish/
```

This action works on **one object**.

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    @action(
        detail=True,
        methods=["post"]
    )
    def publish(self, request, pk=None):

        product = self.get_object()

        product.is_published = True

        product.save()

        return Response(
            {
                "message": "Published"
            }
        )
```

Generated endpoint

```text
POST

/products/10/publish/
```

Router automatically creates it.

---

# What Happens Internally?

Request

```text
POST

/products/10/publish/
```

Router extracts

```text
pk = 10
```

Then

```python
product = self.get_object()
```

becomes

```python
Product.objects.get(pk=10)
```

---

# detail=True Means

The endpoint belongs to **one object**.

Examples

```text
/products/8/publish/

/products/8/archive/

/products/8/activate/

/products/8/deactivate/

/products/8/reset-stock/
```

All require

```text
pk
```

---

# Lesson 3 — detail=False

Suppose you want

```text
GET

/products/export/
```

No product id.

This endpoint works on the **entire collection**.

```python
@action(
    detail=False,
    methods=["get"]
)
def export(self, request):

    return Response(
        {
            "message": "Export started"
        }
    )
```

Generated endpoint

```text
GET

/products/export/
```

Notice

No

```text
pk
```

---

# detail=False Examples

```text
/products/export/

/products/statistics/

/products/popular/

/products/latest/

/products/search/
```

These work on many objects.

---

# Comparison

| detail=True            | detail=False          |
| ---------------------- | --------------------- |
| One object             | Collection            |
| `/products/5/publish/` | `/products/export/`   |
| Uses `get_object()`    | Uses `get_queryset()` |

---

# Lesson 4 — methods

You can choose HTTP methods.

```python
@action(
    detail=True,
    methods=["post"]
)
```

Only POST allowed.

---

Multiple methods

```python
@action(
    detail=True,
    methods=["get", "post"]
)
```

Supports

```text
GET

POST
```

---

Delete action

```python
@action(
    detail=True,
    methods=["delete"]
)
```

---

# Lesson 5 — url_path

Default

```python
@action(detail=True)
def publish(self):
```

Endpoint

```text
/products/5/publish/
```

Want

```text
/products/5/make-public/
```

```python
@action(
    detail=True,
    url_path="make-public"
)
def publish(self, request, pk=None):
```

Function name

```text
publish
```

URL

```text
make-public
```

---

# Lesson 6 — url_name

Default URL name

```text
product-publish
```

Customize

```python
@action(
    detail=True,
    url_name="make-public"
)
```

Now

```text
reverse(
    "product-make-public"
)
```

works.

---

# Lesson 7 — Custom Permissions

Normal ViewSet

```python
permission_classes = [
    IsAuthenticated
]
```

But

Export

should be Admin only.

```python
from rest_framework.permissions import IsAdminUser

@action(
    detail=False,
    permission_classes=[IsAdminUser]
)
def export(self, request):
```

Now only admins can export.

---

# Lesson 8 — Different Serializer

Publish endpoint

doesn't need ProductSerializer.

```python
class PublishSerializer(serializers.Serializer):

    message = serializers.CharField()
```

```python
@action(
    detail=True,
    serializer_class=PublishSerializer
)
```

Very common in production.

---

# Lesson 9 — Production Examples

## Amazon

```text
GET

/products/

GET

/products/10/

POST

/products/10/add-to-cart/

POST

/products/10/add-to-wishlist/

POST

/products/10/report/

POST

/products/10/review/
```

---

## LMS

```text
POST

/courses/5/enroll/

POST

/courses/5/complete/

POST

/courses/5/unenroll/

GET

/courses/popular/
```

---

## Banking

```text
POST

/accounts/9/freeze/

POST

/accounts/9/unfreeze/

POST

/accounts/9/close/

GET

/accounts/report/
```

---

## Blog

```text
POST

/posts/15/like/

POST

/posts/15/share/

POST

/posts/15/bookmark/

GET

/posts/trending/
```

---

# Lesson 10 — Best Practices

✅ Use `@action` only for **business operations**, not CRUD.

Good

```text
/products/5/publish/

/products/5/archive/

/orders/10/cancel/

/courses/2/enroll/
```

Bad

```text
/products/create/

/products/update/

/products/delete/
```

CRUD already exists in `ModelViewSet`.

---

# Lesson 11 — Complete Example

```python
from rest_framework import status
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.viewsets import ModelViewSet

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    @action(detail=True, methods=["post"])
    def publish(self, request, pk=None):
        product = self.get_object()
        product.is_published = True
        product.save()
        return Response({"message": "Published"})

    @action(detail=True, methods=["post"])
    def archive(self, request, pk=None):
        product = self.get_object()
        product.is_archived = True
        product.save()
        return Response({"message": "Archived"})

    @action(detail=False, methods=["get"])
    def statistics(self, request):
        return Response({
            "total_products": self.get_queryset().count()
        })

    @action(detail=False, methods=["get"], url_path="latest")
    def latest_products(self, request):
        products = self.get_queryset().order_by("-id")[:5]
        serializer = self.get_serializer(products, many=True)
        return Response(serializer.data)
```

Generated endpoints:

```text
GET     /products/
GET     /products/5/

POST    /products/5/publish/
POST    /products/5/archive/

GET     /products/statistics/
GET     /products/latest/
```

---

# Interview Questions

### 1. What is `@action`?

It is a DRF decorator that adds **custom endpoints** to a ViewSet beyond the standard CRUD operations.

---

### 2. Difference between `detail=True` and `detail=False`?

| `detail=True`            | `detail=False`                       |
| ------------------------ | ------------------------------------ |
| Works on a single object | Works on the collection              |
| Has `pk` in the URL      | No `pk` in the URL                   |
| Uses `self.get_object()` | Typically uses `self.get_queryset()` |

---

### 3. When should you use `@action`?

When implementing **business-specific operations** such as:

* Publish a product
* Cancel an order
* Enroll in a course
* Freeze a bank account
* Export data

Avoid using it for standard CRUD operations, since `ModelViewSet` already provides those.

---

## Next Module (Module 4)

We'll cover **`reverse()` and Router URL Resolution**, including:

* How `reverse()` generates URLs
* How `basename` affects `reverse()`
* URL names (`product-list`, `product-detail`, custom action names)
* Hyperlinked serializers
* How DRF avoids hardcoding URLs
* Production patterns used in large REST APIs

------------
# Module 4 — `reverse()` and Router URL Resolution

This module separates **intermediate** DRF developers from **senior** DRF developers. If you hardcode URLs in your code, your API becomes difficult to maintain. `reverse()` solves this problem.

---

# Module Roadmap

```text
Module 4

├── Lesson 1: What is reverse()
├── Lesson 2: Why reverse() is needed
├── Lesson 3: URL Names
├── Lesson 4: basename + reverse()
├── Lesson 5: reverse() with Custom @action
├── Lesson 6: reverse() in Serializers
├── Lesson 7: HyperlinkedModelSerializer
├── Lesson 8: reverse() in Production
├── Lesson 9: Best Practices
├── Lesson 10: Interview Questions
```

---

# Lesson 1 — What is `reverse()`?

`reverse()` generates a URL **from its name**, instead of you writing the URL manually.

Instead of:

```python
return Response({
    "product_url": "/products/5/"
})
```

You write:

```python
from rest_framework.reverse import reverse

url = reverse(
    "product-detail",
    kwargs={"pk": 5},
    request=request
)
```

Result:

```text
http://localhost:8000/products/5/
```

The URL is generated automatically.

---

# Lesson 2 — Why is `reverse()` Needed?

Imagine your API starts like this:

```text
/products/
```

Later, the company changes the API version:

```text
/api/v2/products/
```

If you hardcoded:

```python
"/products/5/"
```

you now need to update your code everywhere.

If you used:

```python
reverse("product-detail")
```

nothing changes in your application code. The router resolves the new path automatically.

---

# Lesson 3 — URL Names

Suppose:

```python
router.register(
    "products",
    ProductViewSet
)
```

DRF creates these URL names:

```text
product-list

product-detail
```

These names are what `reverse()` uses.

---

## List Endpoint

```python
reverse(
    "product-list",
    request=request
)
```

Output:

```text
http://localhost:8000/products/
```

---

## Detail Endpoint

```python
reverse(
    "product-detail",
    kwargs={"pk": 10},
    request=request
)
```

Output:

```text
http://localhost:8000/products/10/
```

Notice:

`detail` endpoints always require the lookup value (`pk` by default).

---

# Lesson 4 — How `basename` Affects `reverse()`

Suppose:

```python
router.register(
    "products",
    ProductViewSet,
    basename="product"
)
```

Generated names:

```text
product-list

product-detail
```

Now:

```python
reverse("product-list")
```

works.

But:

```python
reverse("products-list")
```

raises:

```text
NoReverseMatch
```

Because the router created:

```text
product-list
```

not

```text
products-list
```

---

# Lesson 5 — reverse() with Custom `@action`

Suppose:

```python
@action(
    detail=True,
    methods=["post"]
)
def publish(self, request, pk=None):
    ...
```

Router creates:

```text
product-publish
```

Now:

```python
reverse(
    "product-publish",
    kwargs={"pk": 8},
    request=request
)
```

returns:

```text
http://localhost:8000/products/8/publish/
```

---

Another example:

```python
@action(
    detail=False
)
def statistics(self, request):
    ...
```

Generated URL name:

```text
product-statistics
```

Reverse:

```python
reverse(
    "product-statistics",
    request=request
)
```

returns:

```text
/ products/statistics/
```

---

# Lesson 6 — reverse() Inside Serializers

Suppose you want every product to include its own URL.

```json
{
    "id":1,
    "name":"Laptop",
    "url":"http://localhost:8000/products/1/"
}
```

Serializer:

```python
from rest_framework import serializers
from rest_framework.reverse import reverse

class ProductSerializer(serializers.ModelSerializer):

    url = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "url"
        ]

    def get_url(self, obj):

        request = self.context["request"]

        return reverse(
            "product-detail",
            kwargs={
                "pk": obj.pk
            },
            request=request
        )
```

Result:

```json
{
    "id":5,
    "name":"MacBook",
    "url":"http://localhost:8000/products/5/"
}
```

---

# Lesson 7 — HyperlinkedModelSerializer

Instead of manually writing `SerializerMethodField`, DRF provides:

```python
from rest_framework.serializers import HyperlinkedModelSerializer

class ProductSerializer(
    HyperlinkedModelSerializer
):

    class Meta:

        model = Product

        fields = [
            "url",
            "id",
            "name",
            "price"
        ]
```

Response:

```json
{
    "url":"http://localhost:8000/products/5/",
    "id":5,
    "name":"Laptop"
}
```

DRF internally uses `reverse()`.

---

# Lesson 8 — reverse() in Production

Imagine an Amazon-like API.

```text
/orders/10/

/orders/10/cancel/

/orders/10/refund/

/orders/10/invoice/
```

Instead of writing:

```python
"/orders/10/cancel/"
```

generate it:

```python
reverse(
    "order-cancel",
    kwargs={"pk": order.pk},
    request=request
)
```

If tomorrow:

```text
/api/v3/orders/
```

is introduced,

your code **still works** because `reverse()` uses the router.

---

# Lesson 9 — How Router Resolves URLs

When you register:

```python
router.register(
    "products",
    ProductViewSet,
    basename="product"
)
```

The router builds something conceptually like this:

| URL                       | Name                 |
| ------------------------- | -------------------- |
| `/products/`              | `product-list`       |
| `/products/{pk}/`         | `product-detail`     |
| `/products/{pk}/publish/` | `product-publish`    |
| `/products/statistics/`   | `product-statistics` |

`reverse()` looks up the name and generates the corresponding URL.

---

# Lesson 10 — Nested Router + reverse()

Suppose:

```text
/categories/2/products/8/
```

Route name:

```text
category-products-detail
```

Reverse:

```python
reverse(
    "category-products-detail",
    kwargs={
        "category_pk":2,
        "pk":8
    },
    request=request
)
```

Result:

```text
/ categories/2/products/8/
```

Notice that **every lookup parameter required by the route must be supplied**.

---

# Lesson 11 — Common Mistakes

## ❌ Hardcoding URLs

```python
url = "/products/5/"
```

Avoid this.

---

## ✅ Use reverse()

```python
reverse(
    "product-detail",
    kwargs={"pk":5},
    request=request
)
```

---

## ❌ Wrong URL name

```python
reverse(
    "products-detail"
)
```

Error:

```text
NoReverseMatch
```

because the router created:

```text
product-detail
```

---

## ❌ Missing kwargs

```python
reverse(
    "product-detail"
)
```

Error:

```text
NoReverseMatch
```

because the route requires `pk`.

---

# Visual Flow

```text
Router Register
        │
        ▼
Creates URL Patterns
        │
        ▼
Assigns URL Names
        │
        ▼
reverse()
        │
        ▼
Generates URL
        │
        ▼
Serializer / View / Response
```

---

# Best Practices

✅ Never hardcode API URLs.

✅ Always use `reverse()` when generating links.

✅ Use `basename` carefully because it determines URL names.

✅ Keep URL names stable even if URL paths change.

✅ Use `HyperlinkedModelSerializer` when your API is designed around navigable links (HATEOAS-style APIs).

---

# Interview Questions

### 1. What does `reverse()` do?

It generates a URL from a **named route**, avoiding hardcoded URL strings.

---

### 2. Why is `reverse()` better than writing URLs manually?

Because URL paths can change, but route names usually remain stable. This makes the code easier to maintain.

---

### 3. What does `product-detail` mean?

It is the **URL name** generated by the router for the detail endpoint of the `ProductViewSet`.

---

### 4. Why do detail routes require `kwargs={"pk": ...}`?

Because the router's detail URL pattern includes a lookup parameter (by default `pk`), and `reverse()` needs its value to build the URL.

---

### 5. Does `HyperlinkedModelSerializer` use `reverse()` internally?

Yes. It automatically generates hyperlink fields by resolving named routes with `reverse()`.

---

# Senior Developer Insight

Large companies (Amazon, Shopify, Stripe, GitHub, etc.) generally avoid hardcoded URLs in backend code. Instead, they rely on **named routes** and URL resolution. This allows API paths to evolve (for example, introducing `/api/v2/`) while minimizing changes throughout the codebase.

---

## Next Module (Module 5)

**Building RESTful APIs for Large Projects (Amazon-Style Architecture)**

We'll cover:

* API versioning (`/api/v1/`, `/api/v2/`)
* App-based URL organization
* Large project folder structure
* Resource naming conventions
* Authentication endpoints
* Nested vs flat resources
* Filtering, searching, ordering, and pagination design
* Consistent response formats
* Error handling strategy
* Real-world endpoint design for e-commerce, LMS, SaaS, and banking systems

This module focuses on how experienced backend teams organize APIs that remain maintainable as projects grow from dozens to hundreds of endpoints.

--------------
# Module 5 — Building RESTful APIs for Large Projects (Amazon-Style Architecture)

This is one of the most important modules if your goal is to become a **Senior Django REST Framework Backend Developer**.

At this level, you're no longer just writing endpoints—you are **designing APIs that can scale to millions of users and hundreds of developers**.

---

# Module Overview

```text
Module 5

├── Lesson 1: What is API Architecture?
├── Lesson 2: Project Folder Structure
├── Lesson 3: API Versioning
├── Lesson 4: Resource Naming
├── Lesson 5: Endpoint Design
├── Lesson 6: Nested vs Flat Resources
├── Lesson 7: Filtering, Search & Pagination
├── Lesson 8: Authentication Architecture
├── Lesson 9: Consistent Response Format
├── Lesson 10: Error Handling
├── Lesson 11: Permissions
├── Lesson 12: API Documentation
├── Lesson 13: Amazon-style E-commerce API
├── Lesson 14: Interview Questions
```

---

# Lesson 1 — What is API Architecture?

Small project:

```text
Product
```

Large company:

```text
Products

Orders

Payments

Shipping

Coupons

Inventory

Returns

Wishlist

Cart

Reviews

Notifications

Users

Analytics

Reports
```

There may be **500+ endpoints**.

Without architecture:

```text
views.py

urls.py

models.py
```

Everything becomes huge.

A good architecture keeps each feature isolated.

---

# Lesson 2 — Recommended Project Structure

```text
project/

    config/

    apps/

        accounts/

        products/

        categories/

        carts/

        orders/

        payments/

        inventory/

        shipping/

        reviews/

        coupons/

        notifications/

        analytics/

    common/

    core/

    api/
```

Each app contains:

```text
products/

    models.py

    serializers.py

    views.py

    permissions.py

    filters.py

    services.py

    selectors.py

    urls.py

    tests/
```

Senior developers **avoid one giant app**.

---

# Lesson 3 — API Versioning

Never expose APIs like:

```text
/api/products/
```

Instead:

```text
/api/v1/products/

/api/v2/products/
```

Example

```text
/api/v1/orders/

/api/v1/products/

/api/v1/users/
```

Later

```text
/api/v2/products/
```

can introduce breaking changes without affecting existing clients.

---

Example

```
config/
    urls.py
```

```python
urlpatterns = [
    path(
        "api/v1/",
        include("api.v1.urls")
    )
]
```

---

# Lesson 4 — Resource Naming

Always use **plural nouns**.

Good

```text
/products/

/orders/

/reviews/

/categories/

/users/
```

Avoid

```text
/getProducts

/createProduct

/deleteOrder

/updateUser
```

HTTP methods already indicate the action.

| Method | Action |
| ------ | ------ |
| GET    | Read   |
| POST   | Create |
| PATCH  | Update |
| DELETE | Delete |

---

# Lesson 5 — Endpoint Design

Bad

```text
POST

/create-product
```

Good

```text
POST

/products/
```

Bad

```text
GET

/get-all-products
```

Good

```text
GET

/products/
```

Bad

```text
DELETE

/delete-order/5
```

Good

```text
DELETE

/orders/5/
```

---

# Lesson 6 — Nested vs Flat Resources

Example

```text
Products

Reviews
```

Good

```text
/products/

/reviews/
```

Need reviews for one product?

```text
/products/5/reviews/
```

Need all reviews?

```text
/ reviews/
```

Don't over-nest.

Avoid

```text
/users/5/orders/10/items/8/reviews/2/
```

Prefer

```text
/orders/10/

/order-items/8/

/reviews/2/
```

---

# Lesson 7 — Filtering, Search, Ordering & Pagination

Instead of creating many endpoints:

Bad

```text
/products/cheap/

/products/expensive/

/products/popular/

/products/latest/
```

Use query parameters:

```text
/products/?price__lt=100

/products/?ordering=-price

/products/?search=laptop

/products/?page=2
```

One endpoint.

Many possibilities.

---

# Lesson 8 — Authentication Architecture

Large projects separate authentication.

```text
/api/v1/auth/

    login/

    logout/

    register/

    refresh/

    verify-email/

    forgot-password/

    reset-password/
```

Business APIs

```text
/products/

/orders/

/payments/
```

remain clean.

---

# Lesson 9 — Consistent Response Format

Avoid random responses.

Bad

```json
{
    "ok": true
}
```

Another endpoint

```json
{
    "message":"Done"
}
```

Another endpoint

```json
{
    "status":"success"
}
```

Use consistency.

Success

```json
{
    "success": true,
    "message": "Product created",
    "data": {
        "id": 1
    }
}
```

Error

```json
{
    "success": false,
    "message": "Validation failed",
    "errors": {
        "price": [
            "Must be positive."
        ]
    }
}
```

---

# Lesson 10 — Error Handling

Never return

```text
500
```

without explanation.

Good

```json
{
    "message":"Product not found"
}
```

Validation

```json
{
    "errors": {
        "name": [
            "Required"
        ]
    }
}
```

---

# Lesson 11 — Permissions

Don't write

```python
if request.user.is_staff:
```

inside every view.

Create permissions.

```python
class IsSeller(...)

class IsCustomer(...)

class IsOwner(...)
```

Reuse them.

---

# Lesson 12 — Documentation

Professional APIs always provide documentation.

Popular choices:

* **drf-spectacular** (recommended)
* drf-yasg (older)
* OpenAPI / Swagger UI
* ReDoc

Every endpoint should describe:

* Request body
* Response
* Authentication
* Error codes

---

# Lesson 13 — Amazon-style API Design

Imagine Amazon.

## Authentication

```text
POST

/auth/login/

POST

/auth/register/

POST

/auth/refresh/
```

---

## Products

```text
GET

/products/

GET

/products/15/

POST

/products/

PATCH

/products/15/

DELETE

/products/15/
```

---

## Reviews

```text
GET

/products/15/reviews/

POST

/products/15/reviews/
```

---

## Categories

```text
GET

/categories/

GET

/categories/8/products/
```

---

## Cart

```text
GET

/cart/

POST

/cart/items/

PATCH

/cart/items/10/

DELETE

/cart/items/10/
```

---

## Orders

```text
GET

/orders/

POST

/orders/

GET

/orders/10/
```

Custom actions

```text
POST

/orders/10/cancel/

POST

/orders/10/pay/

POST

/orders/10/refund/
```

---

## Payments

```text
POST

/payments/

GET

/payments/8/
```

---

## Coupons

```text
POST

/coupons/apply/
```

---

## Wishlist

```text
GET

/wishlist/

POST

/wishlist/
```

---

# Example URL Tree

```text
/api/v1/

    auth/

    users/

    products/

    categories/

    reviews/

    orders/

    payments/

    cart/

    coupons/

    wishlist/

    shipping/

    inventory/

    notifications/
```

This is much easier to maintain than placing everything under a single `urls.py`.

---

# Lesson 14 — Service Layer (Very Important)

Many beginners put business logic directly in views:

```python
def create(...):
    ...
    ...
    ...
```

A better approach is:

```text
View
      ↓
Service
      ↓
Model
```

Example:

```python
# views.py

OrderService.create_order(...)
```

```python
# services.py

class OrderService:

    @staticmethod
    def create_order(...):
        ...
```

Benefits:

* Reusable logic
* Easier testing
* Cleaner ViewSets

---

# Lesson 15 — Selectors (Advanced)

Instead of:

```python
Product.objects.filter(...)
```

inside many views:

Create:

```text
selectors.py
```

```python
class ProductSelector:

    @staticmethod
    def active_products():
        ...
```

Benefits:

* Centralized query logic
* Easier optimization (`select_related`, `prefetch_related`)
* Less duplicated code

---

# Lesson 16 — Senior Project Architecture

```text
Product Request

        │

        ▼

Router

        │

        ▼

ViewSet

        │

        ▼

Permission

        │

        ▼

Serializer

        │

        ▼

Service

        │

        ▼

Selector

        │

        ▼

Database
```

Every layer has a single responsibility.

---

# Interview Questions

### 1. Why use API versioning?

To introduce breaking changes without affecting existing clients.

---

### 2. Why use plural resource names?

They represent collections and follow REST conventions (`/products/`, `/orders/`).

---

### 3. When should you use nested resources?

When the child resource naturally belongs to the parent, such as `/products/{id}/reviews/`.

---

### 4. Why use a service layer?

To separate business logic from ViewSets, making the code more reusable and testable.

---

### 5. Why use selectors?

To centralize database query logic and avoid duplicating complex queries across views.

---

# Production Checklist

Before starting a real project, ask yourself:

* ✅ API versioning (`/api/v1/`)
* ✅ One app per business domain
* ✅ ViewSets + Routers
* ✅ Business logic in services
* ✅ Query logic in selectors
* ✅ Custom permissions
* ✅ Filtering, search, ordering, pagination
* ✅ Authentication separated under `/auth/`
* ✅ OpenAPI/Swagger documentation
* ✅ Comprehensive automated tests

---

# My Recommendation for Your Learning Path

Based on your goal of becoming a **backend developer specializing in Django REST Framework**, I recommend this sequence:

1. **Master DRF fundamentals** (ViewSets, Routers, Serializers, Authentication).
2. **Build a production-quality E-commerce API** implementing the architecture above.
3. **Learn asynchronous processing** (e.g., background jobs for emails, payments, notifications).
4. **Study caching, performance optimization, deployment, and monitoring**.
5. **Write automated tests** (unit tests and API tests) for every endpoint.

Following this progression will prepare you not only to build APIs but also to design and maintain large-scale backend systems in a professional environment.
Excellent question. This is exactly how **large companies** build APIs.

The short answer is:

> **Yes, sometimes the same ViewSet is used for multiple API versions, and sometimes different ViewSets are used.** It depends on whether the API behavior has changed.

Let's understand with examples.

---

# Case 1: Same ViewSet (No Breaking Changes)

Suppose v1 and v2 behave exactly the same.

```text
/api/v1/products/
/api/v2/products/
```

Project structure

```text
api/
    v1/
        urls.py

    v2/
        urls.py

products/
    views.py
```

`products/views.py`

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

`api/v1/urls.py`

```python
router = DefaultRouter()
router.register("products", ProductViewSet)

urlpatterns = router.urls
```

`api/v2/urls.py`

```python
router = DefaultRouter()
router.register("products", ProductViewSet)

urlpatterns = router.urls
```

`config/urls.py`

```python
urlpatterns = [
    path("api/v1/", include("api.v1.urls")),
    path("api/v2/", include("api.v2.urls")),
]
```

Now both URLs use the **same ViewSet**.

```text
/api/v1/products/

/api/v2/products/
```

↓

```text
ProductViewSet
```

---

# Request Flow

```text
GET /api/v1/products/

        │
        ▼

v1 Router

        │
        ▼

ProductViewSet.list()
```

---

```text
GET /api/v2/products/

        │
        ▼

v2 Router

        │
        ▼

ProductViewSet.list()
```

Different routers, **same ViewSet**.

---

# Case 2: Different ViewSet (Breaking Changes)

Suppose v2 introduces discounts and new fields.

v1 response

```json
{
    "id":1,
    "name":"Laptop"
}
```

v2 response

```json
{
    "id":1,
    "name":"Laptop",
    "discount":20,
    "stock":15
}
```

Now you shouldn't reuse the same serializer/ViewSet.

Structure:

```text
products/

    v1/
        serializers.py
        views.py

    v2/
        serializers.py
        views.py
```

---

v1

```python
class ProductViewSet(ModelViewSet):
    serializer_class = ProductV1Serializer
```

---

v2

```python
class ProductViewSet(ModelViewSet):
    serializer_class = ProductV2Serializer
```

Router

```text
/api/v1/products/
        │
        ▼
ProductV1ViewSet
```

```text
/api/v2/products/
        │
        ▼
ProductV2ViewSet
```

---

# Case 3: Same ViewSet, Different Serializer (Very Common)

Sometimes only the response changes.

```python
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    def get_serializer_class(self):

        version = self.request.version

        if version == "v2":
            return ProductV2Serializer

        return ProductV1Serializer
```

Now

```text
/api/v1/products/
```

↓

uses

```text
ProductV1Serializer
```

---

```text
/api/v2/products/
```

↓

uses

```text
ProductV2Serializer
```

Same ViewSet.

Different Serializer.

This is a common production pattern when the business logic is unchanged.

---

# Case 4: Same ViewSet, Different Logic

You can also inspect the version inside the ViewSet.

```python
def list(self, request):

    if request.version == "v1":
        ...

    if request.version == "v2":
        ...
```

But this approach should be used sparingly. If version-specific logic grows, separate ViewSets become easier to maintain.

---

# How Does `request.version` Work?

If you enable DRF versioning in `settings.py`:

```python
REST_FRAMEWORK = {
    "DEFAULT_VERSIONING_CLASS":
        "rest_framework.versioning.URLPathVersioning"
}
```

and your URL is:

```text
/api/v1/products/
```

then inside the ViewSet:

```python
print(request.version)
```

Output:

```text
v1
```

For:

```text
/api/v2/products/
```

Output:

```text
v2
```

---

# Which Approach Do Big Companies Use?

| Situation                            | Recommended Approach                    |
| ------------------------------------ | --------------------------------------- |
| No API changes                       | Same ViewSet + Same Serializer          |
| Response format changes              | Same ViewSet + Different Serializer     |
| Business logic changes significantly | Different ViewSet                       |
| Major API redesign                   | Separate `v1` and `v2` apps or packages |

---

## Example Project Structure

```text
apps/
    products/
        models.py
        services.py

api/
    v1/
        products/
            views.py
            serializers.py
            urls.py

    v2/
        products/
            views.py
            serializers.py
            urls.py
```

Notice that **both versions share the same `Product` model and often the same service layer**. Usually, only the API layer (serializers, views, URLs) differs between versions. This minimizes code duplication while allowing each API version to evolve independently.

This is the architecture you'll commonly see in mature DRF projects.
