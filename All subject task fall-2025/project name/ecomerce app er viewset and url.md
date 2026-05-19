ঠিক আছে! তুমি চাইছো **ViewSet ব্যবহার না করে, manual/custom API views তৈরি করা**। অর্থাৎ, আমরা **DRF এর APIView / GenericAPIView / mixins** ব্যবহার করে সব endpoint নিজ হাতে লিখব।

আমি তোমার জন্য **Category + CategoryBanner + Product + ProductImage** সবগুলোর **custom API views** বানিয়ে দেখাচ্ছি।

---

# 🔹 1️⃣ Imports

```python id="manual_api_imports"
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from products.models import Category, CategoryBanner, Product, ProductImage
from products.serializers import (
    CategorySerializer,
    CategoryBannerSerializer,
    ProductSerializer,
    ProductImageSerializer
)
from django.shortcuts import get_object_or_404
```

---

# 🔹 2️⃣ Category APIs

```python id="category_api"
class CategoryListCreateAPIView(APIView):
    def get(self, request):
        categories = Category.objects.all()
        serializer = CategorySerializer(categories, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = CategorySerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


class CategoryDetailAPIView(APIView):
    def get(self, request, pk):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category)
        return Response(serializer.data)

    def put(self, request, pk):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def delete(self, request, pk):
        category = get_object_or_404(Category, id=pk)
        category.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 3️⃣ Product APIs

```python id="product_api"
class ProductListCreateAPIView(APIView):
    def get(self, request):
        products = Product.objects.all()
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


class ProductDetailAPIView(APIView):
    def get(self, request, pk):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product)
        return Response(serializer.data)

    def put(self, request, pk):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def delete(self, request, pk):
        product = get_object_or_404(Product, id=pk)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 4️⃣ CategoryBanner APIs

```python id="banner_api"
class CategoryBannerListCreateAPIView(APIView):
    def get(self, request):
        banners = CategoryBanner.objects.all()
        serializer = CategoryBannerSerializer(banners, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = CategoryBannerSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


class CategoryBannerDetailAPIView(APIView):
    def get(self, request, pk):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner)
        return Response(serializer.data)

    def put(self, request, pk):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def delete(self, request, pk):
        banner = get_object_or_404(CategoryBanner, id=pk)
        banner.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 5️⃣ ProductImage APIs

```python id="productimage_api"
class ProductImageListCreateAPIView(APIView):
    def get(self, request):
        images = ProductImage.objects.all()
        serializer = ProductImageSerializer(images, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ProductImageSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)


class ProductImageDetailAPIView(APIView):
    def get(self, request, pk):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image)
        return Response(serializer.data)

    def put(self, request, pk):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def delete(self, request, pk):
        image = get_object_or_404(ProductImage, id=pk)
        image.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 6️⃣ URLs

```python id="custom_api_urls"
from django.urls import path
from products.views import (
    CategoryListCreateAPIView,
    CategoryDetailAPIView,
    ProductListCreateAPIView,
    ProductDetailAPIView,
    CategoryBannerListCreateAPIView,
    CategoryBannerDetailAPIView,
    ProductImageListCreateAPIView,
    ProductImageDetailAPIView
)

urlpatterns = [
    # Categories
    path('categories/', CategoryListCreateAPIView.as_view(), name='category-list-create'),
    path('categories/<uuid:pk>/', CategoryDetailAPIView.as_view(), name='category-detail'),

    # Products
    path('products/', ProductListCreateAPIView.as_view(), name='product-list-create'),
    path('products/<uuid:pk>/', ProductDetailAPIView.as_view(), name='product-detail'),

    # Category Banners
    path('banners/', CategoryBannerListCreateAPIView.as_view(), name='banner-list-create'),
    path('banners/<uuid:pk>/', CategoryBannerDetailAPIView.as_view(), name='banner-detail'),

    # Product Images
    path('product-images/', ProductImageListCreateAPIView.as_view(), name='productimage-list-create'),
    path('product-images/<uuid:pk>/', ProductImageDetailAPIView.as_view(), name='productimage-detail'),
]
```

---

✅ **Features of this manual approach**

1. Full CRUD for all models
2. UUID lookup (`<uuid:pk>`)
3. Separate endpoints → easy to customize logic
4. Nested serializers already handle related objects in response

---

💡 পরবর্তী ধাপ:

আমি চাইলে **extra custom filters / search** add করতে পারি, যেমন:

* `/products/?category=<uuid>` → category অনুযায়ী products
* `/categories/?featured=true` → only categories with featured banners

চাও আমি সেটা দেখাই?


----------
আচ্ছা! তুমি চাইছো **ViewSet ব্যবহার করতে, কিন্তু ModelViewSet বা APIView ব্যবহার করবে না**।
মানে আমরা **`ViewSet` base class** ব্যবহার করব এবং সব CRUD method manually define করব।

এটা করার জন্য DRF এ সাধারণ pattern হলো `ViewSet` class + `@action` decorators + manual methods (list, retrieve, create, update, destroy) লিখা।

আমি তোমার জন্য উদাহরণ দিচ্ছি **Category, Product, CategoryBanner, ProductImage** models এর জন্য।

---

# 🔹 1️⃣ Imports

```python
from rest_framework import viewsets, status
from rest_framework.response import Response
from rest_framework.decorators import action
from django.shortcuts import get_object_or_404
from products.models import Category, Product, CategoryBanner, ProductImage
from products.serializers import (
    CategorySerializer,
    ProductSerializer,
    CategoryBannerSerializer,
    ProductImageSerializer
)
```

---

# 🔹 2️⃣ Category ViewSet (manual methods)

```python
class CategoryViewSet(viewsets.ViewSet):
    """
    Manual CRUD for Category using ViewSet (not ModelViewSet)
    """

    def list(self, request):
        categories = Category.objects.all()
        serializer = CategorySerializer(categories, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category)
        return Response(serializer.data)

    def create(self, request):
        serializer = CategorySerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        category.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 3️⃣ Product ViewSet (manual)

```python
class ProductViewSet(viewsets.ViewSet):

    def list(self, request):
        products = Product.objects.all()
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product)
        return Response(serializer.data)

    def create(self, request):
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 4️⃣ CategoryBanner ViewSet

```python
class CategoryBannerViewSet(viewsets.ViewSet):

    def list(self, request):
        banners = CategoryBanner.objects.all()
        serializer = CategoryBannerSerializer(banners, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner)
        return Response(serializer.data)

    def create(self, request):
        serializer = CategoryBannerSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        banner.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 5️⃣ ProductImage ViewSet

```python
class ProductImageViewSet(viewsets.ViewSet):

    def list(self, request):
        images = ProductImage.objects.all()
        serializer = ProductImageSerializer(images, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image)
        return Response(serializer.data)

    def create(self, request):
        serializer = ProductImageSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        image.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 6️⃣ URLs (with `as_view` mapping)

```python
from django.urls import path
from products.views import (
    CategoryViewSet,
    ProductViewSet,
    CategoryBannerViewSet,
    ProductImageViewSet
)

category_list = CategoryViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
category_detail = CategoryViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

product_list = ProductViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
product_detail = ProductViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

banner_list = CategoryBannerViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
banner_detail = CategoryBannerViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

image_list = ProductImageViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
image_detail = ProductImageViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

urlpatterns = [
    path('categories/', category_list, name='category-list'),
    path('categories/<uuid:pk>/', category_detail, name='category-detail'),

    path('products/', product_list, name='product-list'),
    path('products/<uuid:pk>/', product_detail, name='product-detail'),

    path('banners/', banner_list, name='banner-list'),
    path('banners/<uuid:pk>/', banner_detail, name='banner-detail'),

    path('product-images/', image_list, name='image-list'),
    path('product-images/<uuid:pk>/', image_detail, name='image-detail'),
]
```

---

✅ **Features of this manual ViewSet approach**

1. Full CRUD for all models
2. UUID PK support (`<uuid:pk>`)
3. ViewSet base class, but **manual methods** → no ModelViewSet used
4. Flexible → later `@action` decorator use করে custom endpoints add করা যাবে

---

💡 পরবর্তী স্টেপ:

আমি চাইলে আমি দেখাতে পারি কিভাবে **nested / filtered response** তৈরি করা যায়, যেমন:

* `/categories/<uuid>/` → nested banners + products + product images
* `/products/?category=<uuid>` → filtered products

চাও আমি সেটা বানাই?
আচ্ছা! তুমি চাইছো **ViewSet ব্যবহার করতে, কিন্তু ModelViewSet বা APIView ব্যবহার করবে না**।
মানে আমরা **`ViewSet` base class** ব্যবহার করব এবং সব CRUD method manually define করব।

এটা করার জন্য DRF এ সাধারণ pattern হলো `ViewSet` class + `@action` decorators + manual methods (list, retrieve, create, update, destroy) লিখা।

আমি তোমার জন্য উদাহরণ দিচ্ছি **Category, Product, CategoryBanner, ProductImage** models এর জন্য।

---

# 🔹 1️⃣ Imports

```python
from rest_framework import viewsets, status
from rest_framework.response import Response
from rest_framework.decorators import action
from django.shortcuts import get_object_or_404
from products.models import Category, Product, CategoryBanner, ProductImage
from products.serializers import (
    CategorySerializer,
    ProductSerializer,
    CategoryBannerSerializer,
    ProductImageSerializer
)
```

---

# 🔹 2️⃣ Category ViewSet (manual methods)

```python
class CategoryViewSet(viewsets.ViewSet):
    """
    Manual CRUD for Category using ViewSet (not ModelViewSet)
    """

    def list(self, request):
        categories = Category.objects.all()
        serializer = CategorySerializer(categories, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category)
        return Response(serializer.data)

    def create(self, request):
        serializer = CategorySerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        serializer = CategorySerializer(category, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        category = get_object_or_404(Category, id=pk)
        category.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 3️⃣ Product ViewSet (manual)

```python
class ProductViewSet(viewsets.ViewSet):

    def list(self, request):
        products = Product.objects.all()
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product)
        return Response(serializer.data)

    def create(self, request):
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        serializer = ProductSerializer(product, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        product = get_object_or_404(Product, id=pk)
        product.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 4️⃣ CategoryBanner ViewSet

```python
class CategoryBannerViewSet(viewsets.ViewSet):

    def list(self, request):
        banners = CategoryBanner.objects.all()
        serializer = CategoryBannerSerializer(banners, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner)
        return Response(serializer.data)

    def create(self, request):
        serializer = CategoryBannerSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        serializer = CategoryBannerSerializer(banner, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        banner = get_object_or_404(CategoryBanner, id=pk)
        banner.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 5️⃣ ProductImage ViewSet

```python
class ProductImageViewSet(viewsets.ViewSet):

    def list(self, request):
        images = ProductImage.objects.all()
        serializer = ProductImageSerializer(images, many=True)
        return Response(serializer.data)

    def retrieve(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image)
        return Response(serializer.data)

    def create(self, request):
        serializer = ProductImageSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def update(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        serializer = ProductImageSerializer(image, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    def destroy(self, request, pk=None):
        image = get_object_or_404(ProductImage, id=pk)
        image.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

---

# 🔹 6️⃣ URLs (with `as_view` mapping)

```python
from django.urls import path
from products.views import (
    CategoryViewSet,
    ProductViewSet,
    CategoryBannerViewSet,
    ProductImageViewSet
)

category_list = CategoryViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
category_detail = CategoryViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

product_list = ProductViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
product_detail = ProductViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

banner_list = CategoryBannerViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
banner_detail = CategoryBannerViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

image_list = ProductImageViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
image_detail = ProductImageViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'delete': 'destroy'
})

urlpatterns = [
    path('categories/', category_list, name='category-list'),
    path('categories/<uuid:pk>/', category_detail, name='category-detail'),

    path('products/', product_list, name='product-list'),
    path('products/<uuid:pk>/', product_detail, name='product-detail'),

    path('banners/', banner_list, name='banner-list'),
    path('banners/<uuid:pk>/', banner_detail, name='banner-detail'),

    path('product-images/', image_list, name='image-list'),
    path('product-images/<uuid:pk>/', image_detail, name='image-detail'),
]
```

---

✅ **Features of this manual ViewSet approach**

1. Full CRUD for all models
2. UUID PK support (`<uuid:pk>`)
3. ViewSet base class, but **manual methods** → no ModelViewSet used
4. Flexible → later `@action` decorator use করে custom endpoints add করা যাবে

---

💡 পরবর্তী স্টেপ:

আমি চাইলে আমি দেখাতে পারি কিভাবে **nested / filtered response** তৈরি করা যায়, যেমন:

* `/categories/<uuid>/` → nested banners + products + product images
* `/products/?category=<uuid>` → filtered products

চাও আমি সেটা বানাই?


ঠিক আছে! তুমি চাইছো **`SimpleRouter` ব্যবহার করে ViewSet** বানাতে, যেখানে আমরা **manual methods লিখব** (কোনো ModelViewSet নয়)। আমি তোমার জন্য **SimpleRouter + manual ViewSet** example বানাচ্ছি।

---

# 🔹 1️⃣ Imports

```python
from rest_framework.routers import SimpleRouter
from products.views import (
    CategoryViewSet,
    ProductViewSet,
    CategoryBannerViewSet,
    ProductImageViewSet
)
```

---

# 🔹 2️⃣ ViewSets (manual methods)

আমরা আগের মতো **ViewSet base class** ব্যবহার করব:

```python
# CategoryViewSet, ProductViewSet, CategoryBannerViewSet, ProductImageViewSet
# আগের manual ViewSet code 그대로 ব্যবহার হবে
# list, retrieve, create, update, destroy method সব define থাকবে
```

> লক্ষ্য: এখানে আমরা **ModelViewSet ব্যবহার করছি না**, শুধুমাত্র ViewSet এবং manual CRUD methods।

---

# 🔹 3️⃣ Router setup

```python
router = SimpleRouter()
router.register(r'categories', CategoryViewSet, basename='category')
router.register(r'products', ProductViewSet, basename='product')
router.register(r'banners', CategoryBannerViewSet, basename='banner')
router.register(r'product-images', ProductImageViewSet, basename='productimage')

urlpatterns = router.urls
```

---

# 🔹 4️⃣ URLs behavior

`SimpleRouter` automatically generate করবে:

| HTTP Method | Endpoint            | Action (ViewSet method) |
| ----------- | ------------------- | ----------------------- |
| GET         | /categories/        | list                    |
| POST        | /categories/        | create                  |
| GET         | /categories/<uuid>/ | retrieve                |
| PUT/PATCH   | /categories/<uuid>/ | update                  |
| DELETE      | /categories/<uuid>/ | destroy                 |

`products`, `banners`, `product-images` সবকিছুর জন্য একই pattern।

---

# 🔹 5️⃣ Key Notes

1. **Manual CRUD:** SimpleRouter + ViewSet gives you **automatic URL mapping**, কিন্তু actual logic (`list`, `retrieve`, etc.) তুমি ViewSet এ manually লিখবে।
2. **UUID support:** URLs: `/categories/<uuid:id>/` → ViewSet এর `pk` automatically UUID হবে।
3. **Nested / related objects:** Serializer এ nested field handle করতে পারবে, router কাজ করবে শুধু routing এর জন্য।
4. **basename:** প্রয়োজন হলে custom নাম দিতে পারো, যেমন `basename='category'`।

---

💡 পরবর্তী স্টেপ:

আমি চাইলে দেখাতে পারি **Category nested banners + products + product images** এর জন্য manual ViewSet + SimpleRouter combination API বানানো।

চাও আমি সেটা বানাই?
