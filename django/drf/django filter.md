Django REST Framework (DRF) এ **filter** ব্যবহার করা হয় API response কে dynamic ভাবে control করার জন্য — যেমন:
👉 specific category এর product
👉 price range filter
👉 search / ordering

চলুন step-by-step বুঝি 👇

---

# 🔥 1. Django Filter ki?

**Django Filter** হলো একটি package (`django-filter`) যা দিয়ে সহজে query params দিয়ে data filter করা যায়।

📌 Example:

```
/products/?category=1
/products/?price__gte=100&price__lte=500
```

---

# ⚙️ 2. Install & Setup

```bash
pip install django-filter
```

### settings.py

```python
INSTALLED_APPS = [
    ...
    'django_filters',
]
```

---

# 🧠 3. Kon ViewSet e use kora jay?

✅ Mostly use hoy:

* `ModelViewSet` ✅ (most common)
* `ReadOnlyModelViewSet` ✅
* `GenericViewSet` + mixins ✅

❌ `APIView` e directly na (manual korte hoy)

---

# 🚀 4. Simple Filter Example (ModelViewSet)

ধরি Product model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.FloatField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

---

## ✅ Step 1: ViewSet e filter add

```python
from rest_framework import viewsets
from django_filters.rest_framework import DjangoFilterBackend
from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend]
    filterset_fields = ['category', 'price']
```

---

## ✅ Step 2: Use in URL

```
/products/?category=1
/products/?price=500
```

---

# 🎯 5. Advanced Filtering (Range, lookup)

```python
filterset_fields = {
    'price': ['gte', 'lte'],   # greater than, less than
    'name': ['icontains'],     # search
}
```

### Example:

```
/products/?price__gte=100&price__lte=500
/products/?name__icontains=phone
```

---

# 🧪 6. Custom FilterSet (Best Practice 🔥)

👉 Complex filtering er jonno use kora hoy

```python
import django_filters
from .models import Product

class ProductFilter(django_filters.FilterSet):
    min_price = django_filters.NumberFilter(field_name="price", lookup_expr='gte')
    max_price = django_filters.NumberFilter(field_name="price", lookup_expr='lte')

    class Meta:
        model = Product
        fields = ['category']
```

---

## ViewSet e use:

```python
class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend]
    filterset_class = ProductFilter
```

---

## URL:

```
/products/?min_price=100&max_price=500&category=2
```

---

# 🔍 7. Search + Ordering (Bonus 🔥)

```python
from rest_framework.filters import SearchFilter, OrderingFilter

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]

    filterset_fields = ['category']
    search_fields = ['name']
    ordering_fields = ['price']
```

### Example:

```
/products/?search=phone
/products/?ordering=price
/products/?ordering=-price
```

---

# ⚠️ 8. Important Notes

✅ `filterset_fields` → simple case
✅ `filterset_class` → complex case
✅ `filter_backends` na dile filter kaj korbe na ❌

---

# 🧩 9. Nested ViewSet e Filter

ধরি:

```
/categories/1/products/
```

```python
class CategoryProductViewSet(viewsets.ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        return Product.objects.filter(category_id=self.kwargs['category_pk'])
```

👉 ekhaneo filter add kora jabe:

```python
filter_backends = [DjangoFilterBackend]
filterset_fields = ['price']
```

---

# 🎯 Summary

| Feature            | Use                    |
| ------------------ | ---------------------- |
| `filterset_fields` | simple filter          |
| `filterset_class`  | advanced/custom filter |
| `SearchFilter`     | search                 |
| `OrderingFilter`   | sort                   |
| ViewSet            | ModelViewSet best      |

---

💡 **Real-life use case:**

* E-commerce → price range filter
* Blog → category filter
* Search → product name

---

চাওলে আমি তোমার project (Category → Product → Review system) এর জন্য
👉 full filter + search + ordering optimized setup করে দিতে পারি 😎

-----
হ্যাঁ ✅ **APIView** এবং **Function-Based View (FBV)** — দুইটাইতে filter use করা যায়, কিন্তু ⚠️ automatic না, তোমাকে **manually apply করতে হবে**।

চলুন পরিষ্কারভাবে বুঝি 👇

---

# 🔥 1. ViewSet vs APIView vs FBV (Filter difference)

| View Type           | Filter Support                |
| ------------------- | ----------------------------- |
| ModelViewSet        | ✅ automatic (filter_backends) |
| APIView             | ⚠️ manual                     |
| Function-Based View | ⚠️ manual                     |

👉 মানে:

* ViewSet → DRF নিজে filter handle করে
* APIView / FBV → তোমাকে নিজে queryset filter করতে হবে

---

# 🚀 2. APIView এ Filter ব্যবহার

## ✅ Example: Manual filtering

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer

class ProductAPIView(APIView):

    def get(self, request):
        queryset = Product.objects.all()

        category = request.query_params.get('category')
        min_price = request.query_params.get('min_price')

        if category:
            queryset = queryset.filter(category_id=category)

        if min_price:
            queryset = queryset.filter(price__gte=min_price)

        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
```

---

## 🌐 URL Example:

```
/products/?category=1&min_price=100
```

---

# 🧠 3. APIView এ django-filter use করা (advanced way)

👉 তুমি চাইলে `django-filter` use করতে পারো manually:

```python
from django_filters.rest_framework import DjangoFilterBackend
from .filters import ProductFilter

class ProductAPIView(APIView):

    def get(self, request):
        queryset = Product.objects.all()

        filterset = ProductFilter(request.GET, queryset=queryset)
        queryset = filterset.qs

        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
```

---

# ⚡ 4. Function-Based View (FBV) এ Filter

## ✅ Example:

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET'])
def product_list(request):
    queryset = Product.objects.all()

    category = request.GET.get('category')
    max_price = request.GET.get('max_price')

    if category:
        queryset = queryset.filter(category_id=category)

    if max_price:
        queryset = queryset.filter(price__lte=max_price)

    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)
```

---

# 🎯 5. FBV এ django-filter use

```python
@api_view(['GET'])
def product_list(request):
    queryset = Product.objects.all()

    filterset = ProductFilter(request.GET, queryset=queryset)
    queryset = filterset.qs

    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)
```

---

# ⚠️ 6. Important Difference

| Feature         | APIView / FBV   | ViewSet  |
| --------------- | --------------- | -------- |
| filter_backends | ❌ auto না       | ✅ auto   |
| django-filter   | ✅ manually      | ✅ direct |
| control         | 🔥 full control | medium   |

---

# 🧩 7. Kakhon konta use korbe?

👉 **APIView / FBV use করো যদি:**

* custom logic বেশি লাগে
* complex filtering (multiple condition, business logic)
* full control দরকার

👉 **ViewSet use করো যদি:**

* standard CRUD
* clean & short code
* automatic filtering

---

# 🧠 Final Insight

👉 Interview level answer 😎

* **APIView / FBV → manual filtering**
* **ViewSet → built-in filtering system**

---

চাওলে আমি তোমার জন্য 🔥
👉 **same project (Category → Product → Review)**

* ViewSet version
* APIView version
* FBV version

👉 3টা compare করে real-world structure দেখিয়ে দিতে পারি 🚀
চল তাহলে 🔥 তোমার **Category → Product → Review** project টা আমরা ৩টা style এ compare করি:

👉 ViewSet vs APIView vs FBV (filter সহ)

---

# 🧱 1. Models (same for all)

```python
class Category(models.Model):
    name = models.CharField(max_length=100)

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.FloatField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)

class Review(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    rating = models.IntegerField()
```

---

# 🚀 2. ✅ ViewSet Version (Best Practice)

👉 🔥 clean + powerful + automatic filter

```python
from rest_framework import viewsets
from django_filters.rest_framework import DjangoFilterBackend
from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend]
    filterset_fields = {
        'price': ['gte', 'lte'],
        'category': ['exact']
    }
```

### 🌐 URL:

```
/products/?price__gte=100&price__lte=500&category=1
```

👉 ✔ No extra code
👉 ✔ DRF automatically handle

---

# 🧠 3. ⚙️ APIView Version

👉 🔥 full control but manual

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class ProductAPIView(APIView):

    def get(self, request):
        queryset = Product.objects.all()

        category = request.query_params.get('category')
        min_price = request.query_params.get('min_price')
        max_price = request.query_params.get('max_price')

        if category:
            queryset = queryset.filter(category_id=category)

        if min_price:
            queryset = queryset.filter(price__gte=min_price)

        if max_price:
            queryset = queryset.filter(price__lte=max_price)

        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
```

👉 ✔ flexible
👉 ❌ বেশি code

---

# ⚡ 4. 🔧 FBV Version

👉 🔥 simplest but manual

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET'])
def product_list(request):
    queryset = Product.objects.all()

    category = request.GET.get('category')
    min_price = request.GET.get('min_price')

    if category:
        queryset = queryset.filter(category_id=category)

    if min_price:
        queryset = queryset.filter(price__gte=min_price)

    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)
```

👉 ✔ easy
👉 ❌ not scalable

---

# 🧩 5. 🔥 django-filter in APIView/FBV (pro level)

👉 same filter class use korte parba 3 jayga te 😎

```python
import django_filters

class ProductFilter(django_filters.FilterSet):
    min_price = django_filters.NumberFilter(field_name="price", lookup_expr='gte')
    max_price = django_filters.NumberFilter(field_name="price", lookup_expr='lte')

    class Meta:
        model = Product
        fields = ['category']
```

---

## APIView use:

```python
filterset = ProductFilter(request.GET, queryset=queryset)
queryset = filterset.qs
```

## FBV use:

```python
filterset = ProductFilter(request.GET, queryset=queryset)
queryset = filterset.qs
```

---

# ⚔️ 6. Final Comparison

| Feature     | ViewSet   | APIView   | FBV       |
| ----------- | --------- | --------- | --------- |
| Code size   | ✅ small   | ❌ medium  | ❌ medium  |
| Filter      | ✅ auto    | ⚠️ manual | ⚠️ manual |
| Control     | ⚠️ medium | 🔥 high   | 🔥 high   |
| Scalability | 🔥 best   | good      | low       |

---

# 🎯 Real Project Suggestion (IMPORTANT)

👉 তোমার project (ecommerce type):

✅ Use:

* `ModelViewSet` → Product, Category, Review
* `django-filter` → filtering
* `SearchFilter` → search
* `OrderingFilter` → sorting

❌ Avoid:

* FBV (large project e)
* APIView (unless custom logic needed)

---

# 🧠 Pro Tip (Interview 🔥)

👉 “DRF filtering works automatically in ViewSet using `filter_backends`,
but in APIView and FBV we must manually filter the queryset.”

---

চাওলে next step এ আমি তোমাকে দেখাতে পারি 👇
👉 **filter + search + pagination + nested সব একসাথে production ready setup** 😎
ভাল প্রশ্ন 🔥
👉 **`ViewSet` (not ModelViewSet)** এ django-filter use করা যায় — কিন্তু ⚠️ এখানে automatic queryset/CRUD নাই, তাই একটু manually handle করতে হয়।

চল step-by-step বুঝি 👇

---

# 🧠 1. ViewSet vs ModelViewSet (key difference)

| Feature  | ModelViewSet | ViewSet             |
| -------- | ------------ | ------------------- |
| queryset | ✅ built-in   | ❌ নাই               |
| list()   | ✅ auto       | ❌ manually লিখতে হয় |
| filter   | ✅ easy       | ⚠️ manually apply   |

👉 তাই `ViewSet` এ filter use করতে হলে
➡️ **queryset + filter নিজে apply করতে হবে**

---

# 🚀 2. Basic ViewSet + django-filter

## ✅ Step 1: Filter class

```python
import django_filters
from .models import Product

class ProductFilter(django_filters.FilterSet):
    min_price = django_filters.NumberFilter(field_name="price", lookup_expr='gte')
    max_price = django_filters.NumberFilter(field_name="price", lookup_expr='lte')

    class Meta:
        model = Product
        fields = ['category']
```

---

## ✅ Step 2: ViewSet

```python
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response
from .models import Product
from .serializers import ProductSerializer
from .filters import ProductFilter

class ProductViewSet(ViewSet):

    def list(self, request):
        queryset = Product.objects.all()

        # 🔥 apply filter manually
        filterset = ProductFilter(request.GET, queryset=queryset)

        if filterset.is_valid():
            queryset = filterset.qs

        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
```

---

## 🌐 URL:

```
/products/?min_price=100&max_price=500&category=1
```

---

# ⚡ 3. Detail View (retrieve)

```python
def retrieve(self, request, pk=None):
    product = Product.objects.get(pk=pk)
    serializer = ProductSerializer(product)
    return Response(serializer.data)
```

👉 এখানে filter লাগে না (single object)

---

# 🔥 4. Search + Ordering manually

👉 ViewSet এ automatic `SearchFilter` use করা যায় না (unless mixin use করো)

Manual way:

```python
def list(self, request):
    queryset = Product.objects.all()

    # filter
    filterset = ProductFilter(request.GET, queryset=queryset)
    queryset = filterset.qs

    # search
    search = request.GET.get('search')
    if search:
        queryset = queryset.filter(name__icontains=search)

    # ordering
    ordering = request.GET.get('ordering')
    if ordering:
        queryset = queryset.order_by(ordering)

    serializer = ProductSerializer(queryset, many=True)
    return Response(serializer.data)
```

---

# 🧩 5. Better Way (GenericViewSet 🔥)

👉 যদি তুমি `ViewSet` use করো, better হলো:

```python
from rest_framework.viewsets import GenericViewSet
from rest_framework.mixins import ListModelMixin

class ProductViewSet(ListModelMixin, GenericViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [DjangoFilterBackend]
    filterset_class = ProductFilter
```

👉 এখন ✔ automatic filter কাজ করবে 😎

---

# 🎯 Final Insight

👉 **Pure ViewSet:**

* সব manually (filter, search, ordering)

👉 **GenericViewSet:**

* ViewSet + automatic system (best combo)

👉 **ModelViewSet:**

* full automatic CRUD + filter (most used)

---

# 🔥 Recommendation

👉 তোমার project এর জন্য:

❌ Pure `ViewSet` avoid করো
✅ `GenericViewSet` OR `ModelViewSet` use করো

---

💡 Interview line 😎
👉 “django-filter works automatically with GenericViewSet/ModelViewSet,
but in pure ViewSet we must manually apply filterset.”

---

চাওলে আমি তোমাকে next level দেখাতে পারি 🔥
👉 `get_queryset()` + dynamic filtering + user-based filtering (real production logic) 🚀
সংক্ষেপে বলি 👉 **না, একই class-এর ভিতরে `ViewSet` এবং `ModelViewSet` একসাথে use করা যায় না।** ❌
কিন্তু 👉 **একই project-এ আলাদা আলাদা ViewSet class-এ দুটোই use করা যায়।** ✅

চল পরিষ্কারভাবে বুঝি 👇

---

# 🧠 1. কেন একসাথে use করা যায় না?

```python
class MyViewSet(ViewSet, ModelViewSet): ❌
    pass
```

👉 এটা ভুল ❌ কারণ:

* `ModelViewSet` নিজেই already `GenericViewSet` + mixins inherit করে
* `ViewSet` আলাদা base class
* Multiple inheritance conflict হবে (MRO issue)

👉 তাই same class এ দুইটা একসাথে possible না

---

# ✅ 2. Correct Way (same project এ use)

👉 তুমি আলাদা class এ use করতে পারো 😎

```python
# 🔥 Simple custom logic
from rest_framework.viewsets import ViewSet

class CustomAuthViewSet(ViewSet):
    def list(self, request):
        return Response({"msg": "custom logic"})
```

```python
# 🔥 CRUD + filter
from rest_framework.viewsets import ModelViewSet

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

👉 ✔ same project এ perfectly fine

---

# 🚀 3. Real Project Structure (Best Practice)

👉 e-commerce project example:

| Feature             | View Type      |
| ------------------- | -------------- |
| Product CRUD        | ✅ ModelViewSet |
| Category CRUD       | ✅ ModelViewSet |
| Review CRUD         | ✅ ModelViewSet |
| Custom login/logout | ✅ ViewSet      |
| Payment gateway     | ✅ ViewSet      |

---

# ⚡ 4. Hybrid Approach (🔥 pro level)

👉 তুমি চাইলে `GenericViewSet` use করতে পারো

```python
from rest_framework.viewsets import GenericViewSet
from rest_framework.mixins import ListModelMixin

class ProductViewSet(ListModelMixin, GenericViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

👉 ✔ partial CRUD
👉 ✔ filter support
👉 ✔ flexible

---

# 🎯 5. Final Summary

| Question                            | Answer                               |
| ----------------------------------- | ------------------------------------ |
| Same class এ ViewSet + ModelViewSet | ❌ possible না                        |
| Same project এ use                  | ✅ possible                           |
| Best practice                       | 🔥 ModelViewSet + custom ViewSet mix |

---

# 🧠 Pro Tip (Interview 🔥)

👉 “ModelViewSet is a high-level abstraction of ViewSet.
So we don’t combine them in one class, but we can use both in different parts of a project.”

---

👉 তুমি চাইলে আমি তোমার full project এর জন্য 🔥

* কোথায় ViewSet use করবে
* কোথায় ModelViewSet
* কোথায় GenericViewSet

👉 একটা clean architecture design করে দিতে পারি 🚀
