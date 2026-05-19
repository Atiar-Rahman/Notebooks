ঠিক আছে 😎  
তুমি এখন **APIView এর POST method ঠিকভাবে কাজ করতে চাও**, যাতে তুমি **image বা file upload** করতে পারো। আমি step by step দেখাচ্ছি।

---

## 1️⃣ Serializer (img/serialisers.py)

```python
from rest_framework import serializers
from .models import Image  # তোমার Image model

class ImageSerializer(serializers.ModelSerializer):
    class Meta:
        model = Image
        fields = '__all__'  # বা ['id', 'image', 'created_at']
```

---

## 2️⃣ Model (img/models.py)

```python
from django.db import models

class Image(models.Model):
    image = models.ImageField(upload_to='images/')  # media/images/ তে save হবে
    created_at = models.DateTimeField(auto_now_add=True)
```

---

## 3️⃣ APIView (img/views.py)

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from .serialisers import ImageSerializer

class ImageAPIView(APIView):
    def get(self, request):
        return Response('API is running')

    def post(self, request):
        serializer = ImageSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()  # DB তে save হবে
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

✅ এখানে `serializer.is_valid()` check করছে data ঠিক আছে কিনা।  
✅ `serializer.save()` দিয়ে database এ save হবে।

---

## 4️⃣ URL (urls.py)

```python
from django.urls import path
from .views import ImageAPIView

urlpatterns = [
    path('image/', ImageAPIView.as_view(), name='image-api'),
]
```

---

## 5️⃣ Settings (settings.py) – Media setup

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

`urls.py` (project level) এ add করো:

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('img.urls')),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

## 6️⃣ POST request (Postman / frontend)

- Method: `POST`
    
- URL: `http://127.0.0.1:8000/api/image/`
    
- Body → form-data:
    

```
Key       Type      Value
image     File      select an image
```

- Response:
    

```json
{
    "id": 1,
    "image": "/media/images/my_image.jpg",
    "created_at": "2026-01-22T09:30:00Z"
}
```

---

💡 **Tip:**  
যদি তুমি **video (.mp4) upload** করতে চাও, একই model / serializer ব্যবহার করতে পারো:

```python
video = models.FileField(upload_to='videos/')
```

---

যদি চাও, আমি এখনই দেখাতে পারি **POST method দিয়ে .mp4 video upload + streaming API** তৈরি করা।

চাও আমি এটা দেখাই?