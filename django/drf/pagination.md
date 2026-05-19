
# 🧠 1. Pagination কি?

👉 বড় dataset কে ছোট ছোট page এ ভাগ করা

📌 Example:

```
/products/?page=1
/products/?page=2
```

👉 response:

```json
{
  "count": 100,
  "next": "...page=2",
  "previous": null,
  "results": [...]
}
```

---

# 🚀 2. Types of Pagination (DRF)

| Type                  | Use case            |
| --------------------- | ------------------- |
| PageNumberPagination  | 🔥 most common      |
| LimitOffsetPagination | API style           |
| CursorPagination      | large data + secure |

---

# ⚙️ 3. Global Pagination Setup (Best Practice)

👉 settings.py

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 5
}
```

👉 এখন সব ViewSet এ auto apply হবে 😎

---

# 🔥 4. ViewSet Example

```python
from rest_framework.viewsets import ModelViewSet

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

👉 ✔ automatic pagination

---

# 🌐 URL:

```
/products/?page=2
```

---

# 🎯 5. Custom Pagination Class (🔥 important)

👉 pagination customize করতে চাইলে

```python
from rest_framework.pagination import PageNumberPagination

class CustomPagination(PageNumberPagination):
    page_size = 5
    page_size_query_param = 'page_size'   # dynamic page size
    max_page_size = 50
```

---

## ViewSet এ use:

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = CustomPagination
```

---

## URL:

```
/products/?page=1&page_size=10
```

---

# ⚡ 6. LimitOffsetPagination

👉 frontend developer friendly 😎

```python
from rest_framework.pagination import LimitOffsetPagination

class CustomLimitPagination(LimitOffsetPagination):
    default_limit = 5
    max_limit = 50
```

---

## URL:

```
/products/?limit=5&offset=10
```

---

# 🔐 7. CursorPagination (Advanced 🔥)

👉 large data + secure pagination

```python
from rest_framework.pagination import CursorPagination

class CustomCursorPagination(CursorPagination):
    page_size = 5
    ordering = 'id'
```

---

## URL:

```
/products/?cursor=abc123
```

👉 ✔ no duplicate data
👉 ✔ best for real-time apps

---

# 🧩 8. GenericAPIView / APIView এ Pagination

👉 manually apply করতে হয়

```python
from rest_framework.generics import GenericAPIView
from rest_framework.pagination import PageNumberPagination

class ProductAPIView(GenericAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    pagination_class = PageNumberPagination

    def get(self, request):
        queryset = self.get_queryset()

        page = self.paginate_queryset(queryset)
        if page is not None:
            serializer = self.get_serializer(page, many=True)
            return self.get_paginated_response(serializer.data)

        serializer = self.get_serializer(queryset, many=True)
        return Response(serializer.data)
```

---

# ❌ APIView এ (manual full)

```python
paginator = PageNumberPagination()
page = paginator.paginate_queryset(queryset, request)
serializer = ProductSerializer(page, many=True)
return paginator.get_paginated_response(serializer.data)
```

---

# ⚠️ 9. Common Mistakes

❌ pagination_class na dile kaj korbe na
❌ APIView e paginate_queryset use na korle pagination ashbe na
❌ huge page_size dile performance down

---

# 🎯 10. Real Project Tips

👉 Ecommerce project:

* product list → pagination MUST ✅
* review list → pagination ✅
* category list → optional

---

# 🔥 11. Best Practice

👉 always use:

```python
PAGE_SIZE = 10–20
```

👉 combine with:

* filtering ✅
* search ✅
* ordering ✅

---

# 🧠 Final Insight

👉 ViewSet → auto pagination
👉 APIView → manual
👉 CursorPagination → best for large data

---

# 🚀 Interview Answer (🔥)

👉
“Pagination in DRF is implemented using pagination classes like PageNumberPagination, and it is automatically applied in ViewSets but must be manually handled in APIView using paginate_queryset.”

---


👉 `PageNumberPagination` এ অনেক useful attribute & method আছে — নিচে full breakdown দিলাম 👇

---

# 🧠 1. Basic Fields (most used)

```python
from rest_framework.pagination import PageNumberPagination

class CustomPagination(PageNumberPagination):
    page_size = 5                     # প্রতি page এ কয়টা item
    page_size_query_param = 'page_size'   # user change করতে পারবে
    max_page_size = 50               # max limit
    page_query_param = 'page'        # page param name
```

---

# ⚙️ 2. All Important Fields (🔥 full list)

## ✅ 1. page_size

👉 default items per page

```python
page_size = 10
```

---

## ✅ 2. page_query_param

👉 URL এ page এর নাম

```python
page_query_param = 'page'
```

📌 Example:

```
/products/?page=2
```

👉 change করলে:

```python
page_query_param = 'p'
```

```
/products/?p=2
```

---

## ✅ 3. page_size_query_param

👉 user dynamically size change করতে পারবে

```python
page_size_query_param = 'page_size'
```

📌 Example:

```
/products/?page=1&page_size=20
```

---

## ✅ 4. max_page_size

👉 user যাতে huge data না নিতে পারে

```python
max_page_size = 100
```

---

## ✅ 5. last_page_strings

👉 last page access keyword

```python
last_page_strings = ['last']
```

📌 Example:

```
/products/?page=last
```

---

## ✅ 6. template (Browsable API UI)

```python
template = 'rest_framework/pagination/numbers.html'
```

👉 mostly change লাগে না

---

# 🔥 3. Advanced Customization (Pro Level)

## 🧩 Custom Response Format

👉 default response:

```json
{
  "count": 100,
  "next": "...",
  "previous": "...",
  "results": [...]
}
```

👉 তুমি change করতে পারো:

```python
class CustomPagination(PageNumberPagination):
    page_size = 5

    def get_paginated_response(self, data):
        return Response({
            'total': self.page.paginator.count,
            'page': self.page.number,
            'total_pages': self.page.paginator.num_pages,
            'results': data
        })
```

---

## 🧠 Extra Info add করা

```python
def get_paginated_response(self, data):
    return Response({
        'count': self.page.paginator.count,
        'current_page': self.page.number,
        'next': self.get_next_link(),
        'previous': self.get_previous_link(),
        'total_pages': self.page.paginator.num_pages,
        'results': data
    })
```

---

# ⚡ 4. Performance Related Fields

👉 indirect effect 😎

```python
page_size = 10   # best (5–20 range)
max_page_size = 50
```

❌ bad:

```python
page_size = 1000  # slow response 😵
```

---

# 🚀 5. Full Example (Production Ready 🔥)

```python
from rest_framework.pagination import PageNumberPagination
from rest_framework.response import Response

class CustomPagination(PageNumberPagination):
    page_size = 10
    page_query_param = 'page'
    page_size_query_param = 'page_size'
    max_page_size = 50
    last_page_strings = ['last']

    def get_paginated_response(self, data):
        return Response({
            'total_items': self.page.paginator.count,
            'current_page': self.page.number,
            'total_pages': self.page.paginator.num_pages,
            'next': self.get_next_link(),
            'previous': self.get_previous_link(),
            'results': data
        })
```

---

# 🎯 6. Summary Table

| Field                  | কাজ                |
| ---------------------- | ------------------ |
| page_size              | প্রতি page item    |
| page_query_param       | page param name    |
| page_size_query_param  | dynamic size       |
| max_page_size          | limit control      |
| last_page_strings      | last page access   |
| get_paginated_response | response customize |

---

# 🧠 Final Insight

👉 Pagination customization mainly 2 level:

1. **Behavior control** → page_size, query_param
2. **Response control** → `get_paginated_response()`

---

💡 **Pro Tip 🔥**
👉 Real project এ সবসময় custom response use করো
👉 frontend dev der jonno easy হয়

---

চাওলে আমি তোমাকে next level দেখাতে পারি 😎
👉 **pagination + filter + search combine করে frontend-ready API design (like Amazon)** 🚀
চল এবার একদম **real-world / Amazon-style API design** বানাই 🔥
👉 **Pagination + Filter + Search + Sorting → frontend-ready API**

---

# 🧠 1. Goal (কি বানাবো?)

👉 একটাই endpoint:

```
/products/
```

👉 frontend থেকে সব control হবে:

```
/products/?search=phone&category=1&min_price=100&max_price=1000&ordering=-price&page=2&page_size=10
```

👉 এক API = full power 😎

---

# 🧱 2. Model (example)

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    price = models.FloatField()
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)
```

---

# 🔥 3. Filter (django-filter)

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

# 🚀 4. Custom Pagination (frontend-friendly)

```python
from rest_framework.pagination import PageNumberPagination
from rest_framework.response import Response

class ProductPagination(PageNumberPagination):
    page_size = 10
    page_size_query_param = 'page_size'
    max_page_size = 50

    def get_paginated_response(self, data):
        return Response({
            "success": True,
            "total_items": self.page.paginator.count,
            "total_pages": self.page.paginator.num_pages,
            "current_page": self.page.number,
            "next": self.get_next_link(),
            "previous": self.get_previous_link(),
            "results": data
        })
```

---

# ⚡ 5. ViewSet (🔥 main logic)

```python
from rest_framework.viewsets import ModelViewSet
from rest_framework.filters import SearchFilter, OrderingFilter
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all().select_related('category')
    serializer_class = ProductSerializer
    pagination_class = ProductPagination

    filter_backends = [
        DjangoFilterBackend,
        SearchFilter,
        OrderingFilter
    ]

    # filtering
    filterset_class = ProductFilter

    # search
    search_fields = ['name', 'description']

    # sorting
    ordering_fields = ['price', 'created_at']
    ordering = ['-created_at']  # default latest first
```

---

# 🌐 6. Frontend Usage (🔥 powerful)

## 🔍 Search

```
/products/?search=iphone
```

## 🎯 Filter

```
/products/?category=2&min_price=100&max_price=1000
```

## 🔃 Sorting

```
/products/?ordering=price
/products/?ordering=-price
```

## 📄 Pagination

```
/products/?page=2&page_size=10
```

---

## 🔥 Combine All (Amazon style)

```
/products/?search=phone&category=1&min_price=100&max_price=1000&ordering=-price&page=2&page_size=10
```

👉 frontend full control 😎

---

# 🧩 7. Response (Frontend Ready)

```json
{
  "success": true,
  "total_items": 120,
  "total_pages": 12,
  "current_page": 2,
  "next": "...",
  "previous": "...",
  "results": [
    {
      "id": 1,
      "name": "iPhone 13",
      "price": 900
    }
  ]
}
```

---

# ⚠️ 8. Performance Optimization (VERY IMPORTANT 🔥)

## ✅ 1. select_related

```python
queryset = Product.objects.select_related('category')
```

## ✅ 2. indexing (DB level)

```python
price = models.FloatField(db_index=True)
```

## ✅ 3. pagination limit

```python
max_page_size = 50
```

---

# 🎯 9. Real Project Flow

👉 Frontend (React / Next.js):

* search input → `?search=`
* filter sidebar → category, price
* sort dropdown → price / latest
* pagination → page change

👉 Backend:

* DRF automatically handle everything 😎

---

# 🧠 Final Insight

👉 **Best architecture:**

* `ModelViewSet`
* `django-filter`
* `SearchFilter`
* `OrderingFilter`
* `CustomPagination`

👉 = clean + scalable + production ready 🚀

---

# 🔥 Interview Answer

👉
“A production-ready DRF API combines django-filter for filtering, SearchFilter for search, OrderingFilter for sorting, and custom pagination to provide a flexible and frontend-friendly endpoint.”

---

💡 চাইলে আমি next step এ 🔥
👉 **Cart + Order + Payment API (complete ecommerce backend architecture)** design করে দিতে পারি 😎
