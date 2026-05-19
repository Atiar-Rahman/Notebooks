Haan! 😄 Cholo ami **`ModelViewSet` er sob built-in methods + override points** ekta complete example diye dekhi. Ei example e **Category → Product** nested structure use korbo, jate sob CRUD clearly bujha jai.

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

# 🧩 ModelViewSet with all methods

```python
# views.py
from rest_framework import viewsets
from rest_framework.response import Response
from rest_framework import status
from .models import Category, Product
from .serializers import CategorySerializer, ProductSerializer

# Parent ViewSet
class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

# Nested Product ViewSet
class CategoryProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    # -------- GET: list & retrieve --------
    def get_queryset(self):
        # List & retrieve e parent category filter
        return Product.objects.filter(category_id=self.kwargs['category_pk'])

    # -------- POST: create --------
    def perform_create(self, serializer):
        # automatically assign parent category
        serializer.save(category_id=self.kwargs['category_pk'])

    # -------- PUT/PATCH: update --------
    def perform_update(self, serializer):
        # maintain parent category
        serializer.save(category_id=self.kwargs['category_pk'])

    # -------- DELETE: destroy --------
    def perform_destroy(self, instance):
        instance.delete()

    # -------- Optional: override retrieve --------
    def retrieve(self, request, *args, **kwargs):
        instance = self.get_object()
        serializer = self.get_serializer(instance)
        return Response(serializer.data)

    # -------- Optional: override list --------
    def list(self, request, *args, **kwargs):
        queryset = self.get_queryset()
        serializer = self.get_serializer(queryset, many=True)
        return Response(serializer.data)

    # -------- Optional: override create --------
    def create(self, request, *args, **kwargs):
        serializer = self.get_serializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        self.perform_create(serializer)
        return Response(serializer.data, status=status.HTTP_201_CREATED)

    # -------- Optional: override update --------
    def update(self, request, *args, **kwargs):
        partial = kwargs.pop('partial', False)
        instance = self.get_object()
        serializer = self.get_serializer(instance, data=request.data, partial=partial)
        serializer.is_valid(raise_exception=True)
        self.perform_update(serializer)
        return Response(serializer.data)

    # -------- Optional: override destroy --------
    def destroy(self, request, *args, **kwargs):
        instance = self.get_object()
        self.perform_destroy(instance)
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🧩 Nested Router URLs

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

# 🧩 Summary of ModelViewSet Methods

| HTTP Method                         | DRF Method   | Purpose                               |
| ----------------------------------- | ------------ | ------------------------------------- |
| GET /categories/                    | `list()`     | List all categories                   |
| GET /categories/1/                  | `retrieve()` | Retrieve single category              |
| POST /categories/                   | `create()`   | Create category                       |
| PUT/PATCH /categories/1/            | `update()`   | Update category                       |
| DELETE /categories/1/               | `destroy()`  | Delete category                       |
| GET /categories/1/products/         | `list()`     | List products under category 1        |
| GET /categories/1/products/5/       | `retrieve()` | Retrieve single product in category 1 |
| POST /categories/1/products/        | `create()`   | Create product under category 1       |
| PUT/PATCH /categories/1/products/5/ | `update()`   | Update product under category 1       |
| DELETE /categories/1/products/5/    | `destroy()`  | Delete product under category 1       |

> 🔥 Key Insight:
>
> * `get_queryset()` → read operations (list/retrieve) e apply
> * `perform_create/update/destroy()` → write operations e apply
> * Optional overrides of `list/retrieve/create/update/destroy` → **only if custom behavior lage**

---

Jodi chao ami eta ekta **diagram + flowchart** diye visualize kore dekhai, jekhane **request → nested router → get_queryset/perform_create → DB → response** clearly dekhte parbe.

Chao ami eta ready kori?
Exactly! 😄 Tumi ja copy korecho oi methods **sob optional override**, **DRF er `ModelViewSet` already built-in e implement kore rakhe**, tai **override na korleo sob kaj korbe**. Cholo step-by-step bujhi logic keno automatic kaj kore:

---

# 1️⃣ Retrieve / list

```python
def retrieve(self, request, *args, **kwargs):
    instance = self.get_object()
    serializer = self.get_serializer(instance)
    return Response(serializer.data)
```

- **Logic already DRF e ache**
    
- `get_object()` → instance fetch kore queryset theke, jekhane `get_queryset()` use hoy
    
- `get_serializer()` → serialize kore response return kore
    
- Override kora lage **custom behavior lagle** (extra fields, logging, permission, etc.)
    
- ✅ Default e sob kaj korbe
    

---

# 2️⃣ List

```python
def list(self, request, *args, **kwargs):
    queryset = self.get_queryset()
    serializer = self.get_serializer(queryset, many=True)
    return Response(serializer.data)
```

- `get_queryset()` already filtered by nested router (`category_pk`)
    
- Serializer automatically many=True → list response
    
- DRF default e already implement
    
- Override lagbe **custom filtering / extra metadata / pagination changes** lagle
    

---

# 3️⃣ Create

```python
def create(self, request, *args, **kwargs):
    serializer = self.get_serializer(data=request.data)
    serializer.is_valid(raise_exception=True)
    self.perform_create(serializer)
    return Response(serializer.data, status=status.HTTP_201_CREATED)
```

- DRF default behavior e **serializer validate & save** hoy
    
- `perform_create()` call kore → default save e data DB te store hoy
    
- Override lagbe → **nested router parent assign** er jonno
    
    - e.g., `serializer.save(category_id=self.kwargs['category_pk'])`
        

---

# 4️⃣ Update

```python
def update(self, request, *args, **kwargs):
    partial = kwargs.pop('partial', False)
    instance = self.get_object()
    serializer = self.get_serializer(instance, data=request.data, partial=partial)
    serializer.is_valid(raise_exception=True)
    self.perform_update(serializer)
    return Response(serializer.data)
```

- DRF default behavior e PUT/PATCH update automatically kaj kore
    
- `partial=True` → PATCH, `partial=False` → PUT
    
- Override lagbe → **nested parent ID maintain** korte, otherwise optional
    

---

# 5️⃣ Destroy

```python
def destroy(self, request, *args, **kwargs):
    instance = self.get_object()
    self.perform_destroy(instance)
    return Response(status=status.HTTP_204_NO_CONTENT)
```

- DRF default e `destroy()` instance delete kore response return kore
    
- Override lagbe → extra logic lagle (audit, cascade, custom checks)
    

---

# ✅ Key Insight

- **Default DRF methods = list, retrieve, create, update, destroy**
    
- Override lagbe **only jodi custom logic lage**
    
- Nested router + `get_queryset()` use korle:
    
    - **List & Retrieve** → automatic filtered by parent
        
    - **Create / Update / Destroy** → optionally override for parent assignment / extra logic
        

---

💡 **So short answer:**

> Override na korleo sob kaj korbe, kintu **nested parent assign, custom validation, logging, extra response data** lagle override korte hoy.

---

Jodi chao ami ekta **minimal nested ViewSet example** ready kore diye dekhai, jekhane **override na korleo sob GET, POST, PUT, DELETE smooth kaj kore**, sudhu `perform_create` diye parent assign kora hobe 🔥

Chao ami eta ready kori?


Ok! 😄 Ami clearly ekta **nested router + ModelViewSet** scenario te **konti override “must” lagbe** and konti optional, step-by-step bujhi. Ami **Category → Product** example niye explain korchi.

---

# 1️⃣ GET / List & Retrieve

* **Must override?** ❌ No
* DRF default e `list()` & `retrieve()` already **`get_queryset()`** use kore kaj kore.
* **Must implement** only jodi **filter by parent** lagbe → `get_queryset()`

```python
def get_queryset(self):
    return Product.objects.filter(category_id=self.kwargs['category_pk'])
```

✅ Ei `get_queryset()` override **must** hobe **nested filtering** er jonno.
`list()` / `retrieve()` override optional, normally lagbe na.

---

# 2️⃣ POST / Create

* **Must override?** ✅ Yes, for nested parent assignment
* Default `create()` save kore, kintu **parent category assign korar jonno** `perform_create()` override lagbe

```python
def perform_create(self, serializer):
    serializer.save(category_id=self.kwargs['category_pk'])
```

* `create()` method override → optional, sudhu extra response / logging lagle

---

# 3️⃣ PUT / PATCH / Update

* **Must override?** ❌ Optional
* Default `update()` instance fetch kore update kore
* Override lagbe **only if parent maintain korte hobe**

```python
def perform_update(self, serializer):
    serializer.save(category_id=self.kwargs['category_pk'])
```

* Otherwise, default `update()` enough

---

# 4️⃣ DELETE / Destroy

* **Must override?** ❌ Optional
* Default `destroy()` instance delete kore
* Override lagbe **only extra logic / audit / parent check** lagle

---

# 🔥 Summary Table

| Operation | Must override?                               | Notes                            |
| --------- | -------------------------------------------- | -------------------------------- |
| List      | ❌ Optional if `get_queryset()` handle korcho | Default logic automatic          |
| Retrieve  | ❌ Optional if `get_queryset()` handle korcho | Default logic automatic          |
| Create    | ✅ perform_create                             | Must assign nested parent        |
| Update    | ❌ Optional                                   | Override only to maintain parent |
| Delete    | ❌ Optional                                   | Override only for extra logic    |

---

💡 **Key Insight:**

* **Mandatory:**

  * `get_queryset()` → list/retrieve filter by parent
  * `perform_create()` → POST e parent assign

* **Optional:**

  * `perform_update()` → parent maintain
  * `perform_destroy()` → extra checks / logging
  * Override `list()`, `retrieve()`, `create()`, `update()`, `destroy()` → only custom behavior lagle

---

Tumi chaile ami ekta **minimal nested router + ModelViewSet example** ready kore dekhai jekhane **only `get_queryset()` + `perform_create()` must**, baki sob default DRF logic diye smooth kaj korbe 🔥

Chao ami eta ready kori?
