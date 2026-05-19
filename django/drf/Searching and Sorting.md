
👉 **DRF এ Searching (search) + Sorting (ordering) কিভাবে use করতে হয় + কোন view এ কিভাবে কাজ করে**

---

# 🧠 1. Searching & Sorting কি?

### 🔍 Searching

👉 keyword দিয়ে data খোঁজা

```
/products/?search=phone
```

### 🔃 Sorting (Ordering)

👉 data order করা

```
/products/?ordering=price
/products/?ordering=-price   # descending
```

---

# 🚀 2. ModelViewSet / GenericViewSet এ (BEST 🔥)

👉 এখানে automatic support আছে 😎

## ✅ Example

```python
from rest_framework.viewsets import ModelViewSet
from rest_framework.filters import SearchFilter, OrderingFilter
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,   # filtering
        SearchFilter,          # searching
        OrderingFilter         # sorting
    ]

    search_fields = ['name', 'description']   # search fields
    ordering_fields = ['price', 'created_at']  # allowed sorting
    ordering = ['price']  # default sorting
```

---

## 🌐 Use in URL

### 🔍 Search:

```
/products/?search=iphone
```

### 🔃 Sort:

```
/products/?ordering=price
/products/?ordering=-price
```

### 🔥 Combine:

```
/products/?search=phone&ordering=-price
```

---

# ⚡ 3. GenericViewSet + Mixins

👉 exactly same কাজ করবে

```python
from rest_framework.viewsets import GenericViewSet
from rest_framework.mixins import ListModelMixin

class ProductViewSet(ListModelMixin, GenericViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [SearchFilter, OrderingFilter]
    search_fields = ['name']
    ordering_fields = ['price']
```

👉 ✔ automatic

---

# 🧩 4. APIView / GenericAPIView এ

👉 এখানে manual apply করতে হয় ❗

---

## 🔍 Search (manual)

```python
class ProductAPIView(APIView):
    def get(self, request):
        queryset = Product.objects.all()

        search = request.GET.get('search')
        if search:
            queryset = queryset.filter(name__icontains=search)

        serializer = ProductSerializer(queryset, many=True)
        return Response(serializer.data)
```

---

## 🔃 Sorting (manual)

```python
ordering = request.GET.get('ordering')
if ordering:
    queryset = queryset.order_by(ordering)
```

---

## 🔥 Full Example

```python
class ProductAPIView(APIView):
    def get(self, request):
        queryset = Product.objects.all()

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

# 🚀 5. GenericAPIView (semi-auto)

👉 একটু clean way

```python
from rest_framework.generics import GenericAPIView

class ProductAPIView(GenericAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    def get(self, request):
        queryset = self.get_queryset()

        search = request.GET.get('search')
        if search:
            queryset = queryset.filter(name__icontains=search)

        ordering = request.GET.get('ordering')
        if ordering:
            queryset = queryset.order_by(ordering)

        serializer = self.get_serializer(queryset, many=True)
        return Response(serializer.data)
```

---

# ⚠️ 6. Important Notes

### ❗ search_fields rules:

```python
search_fields = ['name']          # normal
search_fields = ['^name']        # startswith
search_fields = ['=name']        # exact
search_fields = ['@name']        # full-text (PostgreSQL)
```

---

### ❗ ordering_fields:

👉 define না করলে সব field expose হয়ে যাবে ❌

```python
ordering_fields = ['price', 'created_at']
```

---

# 🎯 7. Real Project Setup (BEST 🔥)

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,
        SearchFilter,
        OrderingFilter
    ]

    filterset_fields = ['category']
    search_fields = ['name']
    ordering_fields = ['price']
```

👉 ✔ filter + search + sort all together 😎

---

# ⚔️ 8. Final Comparison

| View Type      | Search         | Sorting        |
| -------------- | -------------- | -------------- |
| ModelViewSet   | ✅ auto         | ✅ auto         |
| GenericViewSet | ✅ auto         | ✅ auto         |
| GenericAPIView | ⚠️ manual      | ⚠️ manual      |
| APIView        | ❌ fully manual | ❌ fully manual |

---

# 🧠 Final Insight

👉 ViewSet use করলে:

* কম code
* clean API
* built-in powerful features

👉 APIView use করলে:

* full control
* but বেশি code

---

# 🔥 Interview Answer

👉
“Search and ordering in DRF are implemented using SearchFilter and OrderingFilter in ViewSets, while in APIView we must manually filter and order the queryset.”

---

