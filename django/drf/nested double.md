Ah, double nested routing! 😄 Cholo step-by-step bujhi, jevabe **parent → child → grandchild** nested routing kora hoy. Ami ekta clean example dibo jekhane:

* `Category` → `Product` → `Review`

---

# 1️⃣ Models

```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

class Review(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='reviews')
    rating = models.IntegerField()
    comment = models.TextField()
```

---

# 2️⃣ Serializers

```python
from rest_framework import serializers
from .models import Category, Product, Review

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'

class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = '__all__'
```

---

# 3️⃣ ViewSets

```python
from rest_framework import viewsets
from .models import Category, Product, Review
from .serializers import CategorySerializer, ProductSerializer, ReviewSerializer

class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

class ProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(category_id=self.kwargs['category_pk'])

    def perform_create(self, serializer):
        serializer.save(category_id=self.kwargs['category_pk'])

class ReviewViewSet(viewsets.ModelViewSet):
    serializer_class = ReviewSerializer

    def get_queryset(self):
        return Review.objects.filter(product_id=self.kwargs['product_pk'])

    def perform_create(self, serializer):
        serializer.save(product_id=self.kwargs['product_pk'])
```

---

# 4️⃣ Nested Routers

```python
from rest_framework_nested import routers
from django.urls import path, include
from .views import CategoryViewSet, ProductViewSet, ReviewViewSet

router = routers.DefaultRouter()
router.register(r'categories', CategoryViewSet)

# First-level nested: Category → Product
product_router = routers.NestedSimpleRouter(router, r'categories', lookup='category')
product_router.register(r'products', ProductViewSet, basename='category-products')

# Second-level nested: Product → Review
review_router = routers.NestedSimpleRouter(product_router, r'products', lookup='product')
review_router.register(r'reviews', ReviewViewSet, basename='product-reviews')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(product_router.urls)),
    path('', include(review_router.urls)),
]
```

---

# 5️⃣ Example URLs

| URL                                 | Description                                       |
| ----------------------------------- | ------------------------------------------------- |
| /categories/                        | List/create categories                            |
| /categories/1/                      | Retrieve/update/delete category 1                 |
| /categories/1/products/             | List/create products under category 1             |
| /categories/1/products/5/           | Retrieve/update/delete product 5 under category 1 |
| /categories/1/products/5/reviews/   | List/create reviews for product 5                 |
| /categories/1/products/5/reviews/2/ | Retrieve/update/delete review 2 for product 5     |

---

# 🔥 Key Points

1. **Double nested router** = parent router → first nested → second nested
2. **lookup** er naming important:

   * First level: `lookup='category'` → `category_pk`
   * Second level: `lookup='product'` → `product_pk`
3. **ViewSets** e `get_queryset()` + `perform_create()` use kore nested parent automatically assign hoy
4. **All CRUD** automatically smooth, just ensure parent IDs use kore filter & save

---

💡 Summary:

* Single nested → parent → child
* Double nested → parent → child → grandchild
* Triple nested o kora jai same pattern follow kore

---

Jodi chao ami ekta **visual diagram** banai, jekhane **double nested router → ViewSets → DB flow → all CRUD** clearly dekhte parbe.

Chao ami eta ready kori?


Perfect! 😄 Cholo ami ekta **complete double nested example** ready kori jekhane **Category → Product → Review** properly handle kora hobe. Ei example e:

* `Review` CRUD properly double nested router er upor base kore
* `get_queryset()` + `perform_create()` use kore parent (category + product) validate kora hobe

---

# 1️⃣ Models

```python
# models.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

class Review(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='reviews')
    rating = models.IntegerField()
    comment = models.TextField()
```

---

# 2️⃣ Serializers

```python
# serializers.py
from rest_framework import serializers
from .models import Category, Product, Review

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'

class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = '__all__'
```

---

# 3️⃣ ViewSets

```python
# views.py
from rest_framework import viewsets
from .models import Category, Product, Review
from .serializers import CategorySerializer, ProductSerializer, ReviewSerializer

class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

class ProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(category_id=self.kwargs['category_pk'])

    def perform_create(self, serializer):
        serializer.save(category_id=self.kwargs['category_pk'])

class ReviewViewSet(viewsets.ModelViewSet):
    serializer_class = ReviewSerializer

    # ✅ Double nested get_queryset
    def get_queryset(self):
        return Review.objects.filter(
            product_id=self.kwargs['product_pk'],
            product__category_id=self.kwargs['category_pk']
        )

    # ✅ Assign product automatically on create
    def perform_create(self, serializer):
        serializer.save(product_id=self.kwargs['product_pk'])
```

---

# 4️⃣ Routers (Double Nested)

```python
# urls.py
from rest_framework_nested import routers
from django.urls import path, include
from .views import CategoryViewSet, ProductViewSet, ReviewViewSet

router = routers.DefaultRouter()
router.register(r'categories', CategoryViewSet)

# Single nested: Category → Product
product_router = routers.NestedSimpleRouter(router, r'categories', lookup='category')
product_router.register(r'products', ProductViewSet, basename='category-products')

# Double nested: Product → Review (under Category context)
review_router = routers.NestedSimpleRouter(product_router, r'products', lookup='product')
review_router.register(r'reviews', ReviewViewSet, basename='product-reviews')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(product_router.urls)),
    path('', include(review_router.urls)),
]
```

---

# 5️⃣ Example URLs & Purpose

| URL                                 | Description                                                    |
| ----------------------------------- | -------------------------------------------------------------- |
| /categories/1/products/5/reviews/   | List/create reviews for Product 5 under Category 1             |
| /categories/1/products/5/reviews/2/ | Retrieve/update/delete Review 2 for Product 5 under Category 1 |

---

# 6️⃣ ✅ Key Notes

1. **Double nested required** → Review needs both `product_pk` + `category_pk`
2. **get_queryset()** → ensures **parent validation**, cannot access review under wrong product/category
3. **perform_create()** → automatically assign `product_id`
4. Update & delete automatically respect `get_queryset()` filter → double nested safe

---

💡 **Flow:**

* User requests: `/categories/1/products/5/reviews/`
* DRF Nested Router passes `category_pk=1`, `product_pk=5` to `ReviewViewSet`
* `get_queryset()` → filters reviews for that product under that category
* `perform_create()` → assigns product automatically when creating new review

---

Tumi chaile ami eta **extra optional override + permission check + full CRUD working** version ready kore **production-ready double nested ViewSet** diye dekhai, jekhane sob GET/POST/PUT/DELETE smooth kaj korbe.

Chao ami eta ready kori?
Exactly 😄! Tumi create korer time **shudhu oi parent ID diye save korlei hobe**, ar DRF automatically oi parent-child relationship maintain korbe, **extra override lagbe na**, sudhu `perform_create()` e parent ID assign korte hobe.

Cholo step-by-step bujhi:

---

# 1️⃣ Single nested example (Product under Category)

```python id="singlecreate"
def perform_create(self, serializer):
    serializer.save(category_id=self.kwargs['category_pk'])
```

* `category_pk` = URL theke pass kora parent ID
* `serializer.save()` → automatically `category` field e assign hoye DB te insert hobe
* DRF er default create logic baki sob handle kore: validation, response, status code ✅

---

# 2️⃣ Double nested example (Review under Product under Category)

```python id="doublecreate"
def perform_create(self, serializer):
    serializer.save(product_id=self.kwargs['product_pk'])
```

* `product_pk` = URL theke pass kora parent ID
* `serializer.save()` → Review create hoy product er sathe attach kore automatically
* `get_queryset()` → ensure kore review **shudhu oi product + category er under e thake**

---

# 3️⃣ Important Notes

1. **Parent ID must match model FK field**

   * `Product.category_id` → category_pk
   * `Review.product_id` → product_pk

2. **No need to manually pass parent in request body**

   * User only POST `rating` + `comment`
   * Parent ID automatically assigned from URL

3. **Optional override** only lage:

   * Extra validation (product belongs to category)
   * Logging / audit

---

# ✅ Example POST body for Review

**URL:** `/categories/1/products/5/reviews/`

**Request body:**

```json
{
    "rating": 5,
    "comment": "Excellent product!"
}
```

* **No need to pass `product` or `category` in body**
* `perform_create()` automatically assigns `product_id=5`
* DB entry will look like:

```python
Review.objects.create(product_id=5, rating=5, comment="Excellent product!")
```

---

💡 **Conclusion:**

> Create korer time **shudhu ekta parent ID URL theke assign kore `serializer.save()`** dile sob kaj smoothly hobe. Extra override optional, only custom behavior lagle lage.

---

Jodi chao ami ekta **minimal working double nested create example** ready kore **full request → DB → response** flow diagram diye dekhai, jekhane sob clearly visible hobe 🔥

Chao ami eta ready kori?

Perfect! 😄 Cholo ami ekta **full double nested example** ready kori jekhane **Category → Product → Review** properly handle kora hobe. Ei example e:

* **List, Create, Update, Delete** sob smooth
* `get_queryset()` + `perform_create()` use kore parent-child validation
* DRF default `update()` & `destroy()` automatically handle kore

---

# 1️⃣ Models

```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=50)

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

class Review(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='reviews')
    rating = models.IntegerField()
    comment = models.TextField()
```

---

# 2️⃣ Serializers

```python
from rest_framework import serializers
from .models import Category, Product, Review

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'

class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = '__all__'
```

---

# 3️⃣ ViewSets (double nested)

```python
from rest_framework import viewsets
from .models import Category, Product, Review
from .serializers import CategorySerializer, ProductSerializer, ReviewSerializer

# ----------------- Category -----------------
class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

# ----------------- Product -----------------
class ProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        category_id = self.kwargs['category_pk']
        return Product.objects.filter(category_id=category_id)

    def perform_create(self, serializer):
        serializer.save(category_id=self.kwargs['category_pk'])

# ----------------- Review -----------------
class ReviewViewSet(viewsets.ModelViewSet):
    serializer_class = ReviewSerializer

    # Double nested queryset (Category + Product)
    def get_queryset(self):
        return Review.objects.filter(
            product_id=self.kwargs['product_pk'],
            product__category_id=self.kwargs['category_pk']
        )

    def perform_create(self, serializer):
        serializer.save(product_id=self.kwargs['product_pk'])
```

---

# 4️⃣ Routers (double nested)

```python
from rest_framework_nested import routers
from django.urls import path, include
from .views import CategoryViewSet, ProductViewSet, ReviewViewSet

router = routers.DefaultRouter()
router.register(r'categories', CategoryViewSet)

# Category → Product
product_router = routers.NestedSimpleRouter(router, r'categories', lookup='category')
product_router.register(r'products', ProductViewSet, basename='category-products')

# Product → Review (under Category context)
review_router = routers.NestedSimpleRouter(product_router, r'products', lookup='product')
review_router.register(r'reviews', ReviewViewSet, basename='product-reviews')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(product_router.urls)),
    path('', include(review_router.urls)),
]
```

---

# 5️⃣ Example URLs

| URL                                   | Description                                                    |
| ------------------------------------- | -------------------------------------------------------------- |
| `/categories/`                        | List/Create categories                                         |
| `/categories/1/`                      | Retrieve/Update/Delete category 1                              |
| `/categories/1/products/`             | List/Create products under category 1                          |
| `/categories/1/products/5/`           | Retrieve/Update/Delete product 5 under category 1              |
| `/categories/1/products/5/reviews/`   | List/Create reviews for product 5 under category 1             |
| `/categories/1/products/5/reviews/2/` | Retrieve/Update/Delete review 2 for product 5 under category 1 |

---

# 6️⃣ ✅ Key Notes

1. **List & Retrieve** → override lagbe na (`get_queryset()` already handle)
2. **Create** → `perform_create()` must to assign parent
3. **Update & Delete** → auto follow `get_queryset()`, safe under double nested
4. **Double nested safety** → Review always tied to **correct Product + Category**

---

💡 **Extra tip:**

* POST request body e **parent IDs lagbe na**, URL theke assign hoy
* Filter & validation automatically enforced by `get_queryset()`

---

If you want, ami eta niye **example POST, PUT, DELETE request + actual DB entries diagram** o ready kore dekhate pari, jate full CRUD flow clearly bujha jai 🔥

Chao ami eta ready kori?
