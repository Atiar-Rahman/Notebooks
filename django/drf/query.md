
`get_object_or_404()` Django এর একটি shortcut function, যেটা কোনো object খুঁজে বের করে। Object না পেলে automatically **404 Not Found** error দেয়।

এটা সাধারণত **views** এ ব্যবহার হয়।

Import:

```python
from django.shortcuts import get_object_or_404
```

---

## Basic usage

Model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
```

View:

```python
product = get_object_or_404(
    Product,
    id=1
)
```

এটা internally করে:

```python
Product.objects.get(id=1)
```

কিন্তু difference:

`get()`:

```python
try:
    product = Product.objects.get(id=1)
except Product.DoesNotExist:
    raise Http404
```

`get_object_or_404()`:

```python
product = get_object_or_404(Product, id=1)
```

---

# Filter query

## id দিয়ে

```python
product = get_object_or_404(
    Product,
    id=5
)
```

SQL:

```sql
WHERE id = 5
```

---

## primary key

Shortcut:

```python
product = get_object_or_404(
    Product,
    pk=5
)
```

`pk` মানে primary key.

Same:

```python
id=5
```

---

# Multiple condition

```python
product = get_object_or_404(
    Product,
    name="iPhone",
    price=999
)
```

SQL:

```sql
WHERE name='iPhone'
AND price=999
```

---

# Using QuerySet

এটা খুব useful:

```python
product = get_object_or_404(
    Product.objects.filter(
        is_active=True
    ),
    id=5
)
```

মানে:

আগে filter করবে:

```sql
WHERE is_active=true
```

তারপর:

```sql
AND id=5
```

---

# ForeignKey relation

Models:

```python
class Category(models.Model):
    name=models.CharField(max_length=100)


class Product(models.Model):
    category=models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

Query:

```python
product = get_object_or_404(
    Product,
    category__name="Electronics",
    id=1
)
```

SQL:

```sql
JOIN category
WHERE category.name='Electronics'
AND product.id=1
```

---

# URL parameter example

urls.py:

```python
path(
    "products/<int:id>/",
    product_detail
)
```

views.py:

```python
def product_detail(request,id):

    product = get_object_or_404(
        Product,
        id=id
    )

    return JsonResponse({
        "name":product.name
    })
```

Request:

```
GET /products/5/
```

---

# Delete example

```python
def delete_product(request,id):

    product = get_object_or_404(
        Product,
        id=id
    )

    product.delete()

    return JsonResponse({
        "message":"deleted"
    })
```

If id না থাকে:

Response:

```
404 Not Found
```

---

# Update example

```python
def update_product(request,id):

    product = get_object_or_404(
        Product,
        pk=id
    )

    product.name="New name"
    product.save()
```

---

# related_name query

Models:

```python
class Cart(models.Model):
    user=models.OneToOneField(
        User,
        related_name="cart"
    )
```

Query:

```python
cart = get_object_or_404(
    Cart,
    user__email="test@gmail.com"
)
```

---

# `get_list_or_404()` difference

আরেকটা shortcut আছে:

```python
from django.shortcuts import get_list_or_404
```

এটা multiple object দেয়।

Example:

```python
products = get_list_or_404(
    Product,
    category_id=1
)
```

Equivalent:

```python
Product.objects.filter(category_id=1)
```

Difference:

No data:

`filter()`:

```python
[]
```

`get_list_or_404()`:

```
404 error
```

---

# Common lookups with get_object_or_404

## contains

```python
get_object_or_404(
    Product,
    name__contains="phone"
)
```

SQL:

```sql
LIKE '%phone%'
```

---

## icontains

case insensitive:

```python
name__icontains="PHONE"
```

Matches:

```
Phone
phone
PHONE
```

---

## greater than

```python
price__gt=500
```

SQL:

```sql
price > 500
```

---

## less than

```python
price__lt=500
```

---

## range

```python
price__range=[100,1000]
```

---

## in

```python
id__in=[1,2,3]
```

---

## null

```python
deleted_at__isnull=True
```

---

## date

```python
created_at__year=2026
```

---

### DRF example

```python
from rest_framework.response import Response
from rest_framework.views import APIView


class ProductDetail(APIView):

    def get(self,request,id):

        product = get_object_or_404(
            Products,
            id=id
        )

        return Response({
            "name":product.name,
            "price":product.price
        })
```

এটা production API-তে খুব common pattern।

-------------

Django ORM এর অনেক **shortcut query functions** আছে যেগুলো database query সহজ করে। নিচে সবচেয়ে বেশি ব্যবহার করা গুলো example সহ দিলাম।

ধরি model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock = models.IntegerField()
    is_active = models.BooleanField(default=True)
```

---

## 1. `all()`

সব data আনতে:

```python
products = Product.objects.all()
```

SQL:

```sql
SELECT * FROM product;
```

Result:

```python
<QuerySet [
 Product1,
 Product2,
 Product3
]>
```

---

## 2. `filter()`

condition দিয়ে data আনে।

```python
products = Product.objects.filter(
    is_active=True
)
```

SQL:

```sql
WHERE is_active = true
```

Multiple:

```python
Product.objects.filter(
    price=100,
    stock=5
)
```

মানে:

```sql
price=100 AND stock=5
```

---

## 3. `exclude()`

যেটা match করে সেটা বাদ দেয়।

```python
Product.objects.exclude(
    stock=0
)
```

মানে:

```sql
WHERE stock != 0
```

Example:

```python
Product.objects.exclude(
    name="iPhone"
)
```

iPhone বাদে সব দিবে।

---

## 4. `get()`

একটা object দেয়।

```python
product = Product.objects.get(
    id=1
)
```

Output:

```
Product object
```

Problem:

যদি না থাকে:

```
DoesNotExist
```

যদি একের বেশি থাকে:

```
MultipleObjectsReturned
```

---

## 5. `first()`

প্রথম object:

```python
product = Product.objects.first()
```

SQL:

```sql
LIMIT 1
```

না থাকলে:

```python
None
```

---

## 6. `last()`

শেষ object:

```python
Product.objects.last()
```

---

## 7. `count()`

কয়টা row আছে:

```python
Product.objects.count()
```

Output:

```
50
```

SQL:

```sql
COUNT(*)
```

---

## 8. `exists()`

data আছে কিনা check:

```python
Product.objects.filter(
    name="Phone"
).exists()
```

Output:

```python
True
```

Use:

```python
if Product.objects.filter(email=email).exists():
    print("Already exists")
```

---

# Field lookup shortcuts

## 9. `contains`

case sensitive:

```python
Product.objects.filter(
    name__contains="phone"
)
```

Find:

```
iphone
phone case
```

SQL:

```sql
LIKE '%phone%'
```

---

## 10. `icontains`

case insensitive:

```python
Product.objects.filter(
    name__icontains="PHONE"
)
```

Matches:

```
Phone
phone
PHONE
```

---

## 11. `startswith`

```python
Product.objects.filter(
    name__startswith="Sam"
)
```

Find:

```
Samsung
SamPhone
```

---

## 12. `endswith`

```python
Product.objects.filter(
    name__endswith="Pro"
)
```

Find:

```
iPhone Pro
Macbook Pro
```

---

# Number query

## 13. `gt`

greater than

```python
Product.objects.filter(
    price__gt=500
)
```

SQL:

```sql
price > 500
```

---

## 14. `gte`

greater equal

```python
price__gte=500
```

---

## 15. `lt`

less than

```python
price__lt=500
```

---

## 16. `lte`

less equal

```python
price__lte=500
```

---

## 17. `range`

between:

```python
Product.objects.filter(
    price__range=[100,500]
)
```

SQL:

```sql
price BETWEEN 100 AND 500
```

---

## 18. `in`

multiple values:

```python
Product.objects.filter(
    id__in=[1,2,3]
)
```

SQL:

```sql
id IN (1,2,3)
```

---

# NULL query

## 19. `isnull`

```python
Product.objects.filter(
    description__isnull=True
)
```

SQL:

```sql
description IS NULL
```

---

# Date query

## 20. year

```python
Product.objects.filter(
    created_at__year=2026
)
```

---

## 21. month

```python
created_at__month=6
```

---

## 22. day

```python
created_at__day=27
```

---

# Ordering

## 23. `order_by()`

Ascending:

```python
Product.objects.order_by(
    "price"
)
```

Small → Large

Descending:

```python
Product.objects.order_by(
    "-price"
)
```

Large → Small

Multiple:

```python
Product.objects.order_by(
    "price",
    "-created_at"
)
```

---

# Values

## 24. `values()`

Dictionary return:

```python
Product.objects.values(
    "name",
    "price"
)
```

Output:

```json
[
 {
  "name":"Phone",
  "price":500
 }
]
```

---

## 25. `values_list()`

Tuple:

```python
Product.objects.values_list(
    "name",
    "price"
)
```

Output:

```python
[
 ("Phone",500)
]
```

Single field:

```python
Product.objects.values_list(
    "name",
    flat=True
)
```

Output:

```
["Phone","Laptop"]
```

---

# Limit

## 26. slicing

Top 5:

```python
Product.objects.all()[:5]
```

SQL:

```sql
LIMIT 5
```

---

# Update

## 27. update()

সব একসাথে update:

```python
Product.objects.filter(
    id=1
).update(
    price=1000
)
```

---

# Delete

## 28. delete()

```python
Product.objects.filter(
    id=1
).delete()
```

---

# Aggregate

## 29. Sum

```python
from django.db.models import Sum

Product.objects.aggregate(
    Sum("price")
)
```

Output:

```python
{
 'price__sum':5000
}
```

---

## 30. Avg

```python
from django.db.models import Avg

Product.objects.aggregate(
    Avg("price")
)
```

---

## 31. Max / Min

```python
from django.db.models import Max

Product.objects.aggregate(
    Max("price")
)
```

---

# Related query

Example:

```python
class Category(models.Model):
    name=models.CharField(max_length=50)


class Product(models.Model):
    category=models.ForeignKey(
        Category,
        related_name="products",
        on_delete=models.CASCADE
    )
```

Get products:

```python
category.products.all()
```

Filter relation:

```python
Product.objects.filter(
    category__name="Electronics"
)
```

---

## Most used in real API:

```python
Product.objects.filter()
Product.objects.get()
Product.objects.all()
Product.objects.exists()
Product.objects.count()
Product.objects.order_by()
Product.objects.values()
Product.objects.update()
Product.objects.select_related()
Product.objects.prefetch_related()
```

এইগুলো জানলে Django ORM-এর প্রায় 90% কাজ করা যায়।

-----------
`get_object_or_404()` এর সাথে Django-তে আরো কিছু **shortcut function** আছে যেগুলো একই ধরনের কাজ করে। এগুলো `django.shortcuts` থেকে আসে।

```python
from django.shortcuts import (
    get_object_or_404,
    get_list_or_404,
    redirect,
    render,
    resolve_url
)
```

---

## 1. `get_object_or_404()`

একটা object বের করে।

### Syntax:

```python
get_object_or_404(
    Model,
    condition
)
```

Example:

```python
from django.shortcuts import get_object_or_404

product = get_object_or_404(
    Products,
    id=10
)
```

Equivalent:

```python
Products.objects.get(id=10)
```

Difference:

`get()`:

```python
Products.DoesNotExist
```

throw করে।

`get_object_or_404()`:

```http
404 Not Found
```

return করে।

---

### Multiple condition

```python
product = get_object_or_404(
    Products,
    name="iPhone",
    stock__gt=0
)
```

SQL:

```sql
WHERE name='iPhone'
AND stock > 0
```

---

### QuerySet দিয়ে

```python
product = get_object_or_404(
    Products.objects.filter(
        is_active=True
    ),
    id=5
)
```

---

### Related lookup

Model:

```python
class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

Query:

```python
product = get_object_or_404(
    Product,
    category__name="Electronics",
    id=1
)
```

---

# 2. `get_list_or_404()`

একাধিক object এর জন্য।

```python
from django.shortcuts import get_list_or_404
```

Example:

```python
products = get_list_or_404(
    Products,
    category_id=1
)
```

Equivalent:

```python
Products.objects.filter(
    category_id=1
)
```

Difference:

No data:

`filter()`:

```python
[]
```

`get_list_or_404()`:

```http
404
```

---

# 3. `render()`

HTML template return করে।

Syntax:

```python
render(
    request,
    template_name,
    context
)
```

Example:

```python
def home(request):

    products = Products.objects.all()

    return render(
        request,
        "home.html",
        {
            "products":products
        }
    )
```

Template:

```html
{% for product in products %}
{{ product.name }}
{% endfor %}
```

---

# 4. `redirect()`

অন্য URL এ পাঠায়।

Import:

```python
from django.shortcuts import redirect
```

Example:

```python
def login_success(request):

    return redirect(
        "home"
    )
```

URL:

```python
path(
    "",
    home,
    name="home"
)
```

---

With arguments:

```python
return redirect(
    "product-detail",
    id=5
)
```

URL:

```python
/product/5/
```

---

# 5. `resolve_url()`

URL name থেকে URL বের করে।

Example:

```python
from django.shortcuts import resolve_url


url = resolve_url(
    "home"
)

print(url)
```

Output:

```
/
```

---

# 6. `HttpResponseRedirect`

Low-level redirect:

```python
from django.http import HttpResponseRedirect


return HttpResponseRedirect(
    "/products/"
)
```

`redirect()` এর ভিতরে এটা ব্যবহার হয়।

---

# 7. `get_object_or_404` + soft delete

তোমার BaseModel অনুযায়ী:

```python
product = get_object_or_404(
    Products,
    id=id,
    deleted_at__isnull=True
)
```

মানে:

- product আছে
    
- deleted না
    

দুইটাই লাগবে।

---

# DRF API তে common pattern

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from django.shortcuts import get_object_or_404


class ProductDetail(APIView):

    def get(self, request, id):

        product = get_object_or_404(
            Products,
            id=id
        )

        return Response({
            "name": product.name,
            "price": product.price
        })
```

---

## Short summary

|Function|কাজ|
|---|---|
|`get_object_or_404()`|১টা object অথবা 404|
|`get_list_or_404()`|অনেক object অথবা 404|
|`render()`|HTML page return|
|`redirect()`|অন্য URL এ পাঠায়|
|`resolve_url()`|URL name → URL|
|`HttpResponseRedirect`|direct redirect|

API project এ সবচেয়ে বেশি ব্যবহার হবে:

```python
get_object_or_404()
redirect()
render()
```
-----------
Django ORM-এ `create_or_update` নামে কোনো built-in function নেই। সাধারণত এর জন্য ৩টা common method ব্যবহার করা হয়:

1. `get_or_create()`
    
2. `update_or_create()`
    
3. নিজের custom create/update logic
    

---

## 1. `get_or_create()`

মানে:

> আগে খুঁজবে, থাকলে return করবে, না থাকলে create করবে।

Syntax:

```python
Model.objects.get_or_create(
    lookup_fields,
    defaults={}
)
```

Example:

Model:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
```

Use:

```python
category, created = Category.objects.get_or_create(
    name="Electronics"
)
```

### First time:

Database:

```
id | name
---------
1  | Electronics
```

Return:

```python
category = Category object
created = True
```

---

### Second time:

```python
category, created = Category.objects.get_or_create(
    name="Electronics"
)
```

Return:

```python
created = False
```

নতুন create করবে না।

---

### defaults ব্যবহার

```python
product, created = Products.objects.get_or_create(
    slug="iphone-15",
    defaults={
        "name":"iPhone 15",
        "price":999,
        "stock":20
    }
)
```

এখানে:

যদি slug না থাকে → create করবে।

যদি থাকে → শুধু সেই object return করবে।

---

# 2. `update_or_create()`

মানে:

> থাকলে update করবে, না থাকলে create করবে।

Syntax:

```python
Model.objects.update_or_create(
    lookup,
    defaults={}
)
```

Example:

```python
product, created = Products.objects.update_or_create(
    slug="iphone-15",
    defaults={
        "name":"iPhone 15 Pro",
        "price":1200,
        "stock":15
    }
)
```

---

### যদি আগে থাকে:

Before:

|slug|name|price|
|---|---|---|
|iphone-15|iPhone 15|999|

After:

|slug|name|price|
|---|---|---|
|iphone-15|iPhone 15 Pro|1200|

Return:

```python
created=False
```

---

### যদি না থাকে:

Create:

```python
created=True
```

---

# Difference

|Function|Exists|Not exists|
|---|---|---|
|`get_or_create()`|return object|create|
|`update_or_create()`|update + return|create|

---

# Cart example (real use)

তোমার e-commerce:

এক user এর একটাই cart:

```python
cart, created = Cart.objects.get_or_create(
    user=user
)
```

না থাকলে:

```
create cart
```

থাকলে:

```
existing cart
```

---

# Product update example

Admin থেকে product update:

```python
product, created = Products.objects.update_or_create(
    slug="laptop",
    defaults={
        "price":1500,
        "stock":10
    }
)
```

---

# Bulk এর জন্য

অনেক data create:

```python
Products.objects.bulk_create([
    Products(name="Phone"),
    Products(name="Laptop")
])
```

---

# DRF API example

POST `/products/`

```python
product, created = Products.objects.update_or_create(
    slug=request.data["slug"],
    defaults=request.data
)
```

একই API দিয়ে:

- নতুন product create
    
- existing product update
    

দুটো করা যায়।

---

Most used:

```python
get_or_create()
```

Cart, profile, settings এর জন্য

আর:

```python
update_or_create()
```

sync/update data এর জন্য।