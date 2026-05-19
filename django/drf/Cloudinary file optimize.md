ঠিক আছে—আমি তোমাকে **Django + DRF + Cloudinary**-এ `f_auto` + `q_auto` ব্যবহার করে **production-ready full flow** দেখাচ্ছি 👇
(Upload → Save → API → Optimized URL return)

---

# 🚀 Step 1: Install packages

```bash
pip install cloudinary django-cloudinary-storage
```

---

# ⚙️ Step 2: settings.py config

```python
import cloudinary

cloudinary.config(
    cloud_name = "your_cloud_name",
    api_key = "your_api_key",
    api_secret = "your_api_secret"
)

DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

---

# 🧱 Step 3: Model

```python
from django.db import models
from cloudinary.models import CloudinaryField

class Product(models.Model):
    name = models.CharField(max_length=100)
    image = CloudinaryField('image')

    def __str__(self):
        return self.name
```

---

# 🔥 Step 4: Serializer (MOST IMPORTANT)

👉 এখানে আমরা `f_auto + q_auto` apply করবো

```python
from rest_framework import serializers
from .models import Product
import cloudinary.utils

class ProductSerializer(serializers.ModelSerializer):
    image_url = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ['id', 'name', 'image_url']

    def get_image_url(self, obj):
        if not obj.image:
            return None

        url, _ = cloudinary.utils.cloudinary_url(
            obj.image.public_id,
            fetch_format="auto",   # f_auto
            quality="auto",        # q_auto
        )
        return url
```

---

# ⚡ Step 5: ViewSet

```python
from rest_framework.viewsets import ModelViewSet
from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

# 🔗 Step 6: URL

```python
from rest_framework.routers import DefaultRouter
from .views import ProductViewSet

router = DefaultRouter()
router.register('products', ProductViewSet)

urlpatterns = router.urls
```

---

# 🧪 Step 7: Postman Test

## ✅ POST (Upload image)

```
POST /products/
Content-Type: multipart/form-data
```

Body:

* name = "Test Product"
* image = (file upload)

---

## ✅ GET Response

```json
{
  "id": 1,
  "name": "Test Product",
  "image_url": "https://res.cloudinary.com/xxx/image/upload/f_auto,q_auto/sample.jpg"
}
```

👉 দেখো URL-এ already:

```
f_auto,q_auto
```

---

# 💎 Step 8: Advanced Optimization (Recommended)

```python
def get_image_url(self, obj):
    url, _ = cloudinary.utils.cloudinary_url(
        obj.image.public_id,
        fetch_format="auto",
        quality="auto",
        width=500,
        height=500,
        crop="fill"
    )
    return url
```

👉 Result:

```
.../w_500,h_500,c_fill,f_auto,q_auto/...
```

---

# 🧠 Real-world Best Practice

👉 Always:

* ❌ original image direct serve করো না
* ✅ optimized URL serve করো

---

# 🔥 Bonus: Separate Thumbnail + Full Image

```python
class ProductSerializer(serializers.ModelSerializer):
    thumbnail = serializers.SerializerMethodField()
    full_image = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ['id', 'name', 'thumbnail', 'full_image']

    def thumbnail(self, obj):
        url, _ = cloudinary.utils.cloudinary_url(
            obj.image.public_id,
            width=200,
            height=200,
            crop="fill",
            fetch_format="auto",
            quality="auto"
        )
        return url

    def full_image(self, obj):
        url, _ = cloudinary.utils.cloudinary_url(
            obj.image.public_id,
            fetch_format="auto",
            quality="auto"
        )
        return url
```

---

# 🎯 Final বুঝে নাও

👉 `f_auto + q_auto` use করার জায়গা:

| Layer        | Use   |
| ------------ | ----- |
| Upload time  | ❌ না  |
| Database     | ❌ না  |
| API response | ✅ YES |
| URL          | ✅ YES |

---

# 💡 Summary

* Cloudinary already handles optimization
* তুমি শুধু URL-এ:

  ```
  f_auto,q_auto
  ```

  add করলেই done

---
