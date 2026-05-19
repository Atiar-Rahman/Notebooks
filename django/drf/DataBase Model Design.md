Django-এ `CharField`-এর জন্য `null=True` এবং `blank=True` ব্যবহার নিয়ে কিছু best practice আছে।

---

## 🔹 Key point

* **`blank=True`** → form বা validation level-এ field খালি থাকতে পারবে
* **`null=True`** → database level-এ `NULL` save হবে

### ⚠️ Important for CharField / TextField

* Django convention: **`CharField` বা `TextField`-এ `null=True` দেওয়া ঠিক নয়**
* কারণ:

  * database-এ `NULL` এবং empty string `""` আলাদা
  * অনেক logic/queries confuse হতে পারে `" "` vs `NULL`
* সাধারণভাবে:

  ```python
  name = models.CharField(max_length=100, blank=True)  # ✔ Recommended
  ```

  → database-এ empty string `""` save হবে, null হবে না

---

### 🔹 কখন `null=True` দেওয়া হয়?

* Mostly non-string fields-এ:

  * `IntegerField`, `FloatField`, `DateField`, `ForeignKey` ইত্যাদি
* CharField-এ খুব rare cases-এ দিলে হবে, কিন্তু avoid করা better

---

### 🔹 সংক্ষেপে

| Field type              | blank=True    | null=True    | Recommendation             |
| ----------------------- | ------------- | ------------ | -------------------------- |
| CharField/TextField     | ✅ allow empty | ❌ avoid      | use blank=True, null=False |
| Integer/Date/ForeignKey | ✅ allow empty | ✅ allow null | use both if optional       |

---

✔ Conclusion:
**CharField-এর জন্য:** `blank=True` দাও, **`null=True` না দেওয়াই ভালো**

---



Soft delete beginnerদের জন্য প্রথমে confusing লাগে — but once বুঝে ফেললে তুমি **production-level backend** এ huge upgrade পেয়ে যাবে 🔥

চলো একদম সহজভাবে step-by-step বুঝাই 👇

---

# 🧠 Soft Delete কী?

👉 Normally:

```python
obj.delete()
```

➡️ database থেকে permanently delete ❌

👉 Soft delete:

```python
obj.is_active = False
obj.save()
```

➡️ database এ থাকে, কিন্তু hidden থাকে ✅

---

# ❗ কেন use করি?

✔ Accidentally delete হলে recover করা যাবে
✔ Audit/logging possible
✔ Important data lose হবে না
✔ Industry standard practice

---

# 🏗️ Step-by-Step Implementation

## ✅ Step 1: BaseModel এ field add করো

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)  # 🔥 main field

    class Meta:
        abstract = True
```

---

## ✅ Step 2: Custom Manager বানাও

👉 Default query যেন শুধু active data আনে

```python
class ActiveManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_active=True)
```

---

## ✅ Step 3: Model এ apply করো

```python
class Camera(BaseModel):
    name = models.CharField(max_length=100)

    objects = models.Manager()          # সব data (including deleted)
    active_objects = ActiveManager()    # only active data
```

---

## 🔍 এখন কী হবে?

### 👉 Normal query:

```python
Camera.active_objects.all()
```

➡️ only active data

### 👉 All data:

```python
Camera.objects.all()
```

➡️ including deleted

---

# 🗑️ Step 4: Delete override (IMPORTANT 🔥)

👉 যেন `.delete()` call করলে soft delete হয়

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):
        self.is_active = False
        self.save()
```

---

## 🎯 Usage

```python
camera = Camera.objects.get(id=1)
camera.delete()
```

👉 database থেকে delete হবে না
👉 শুধু `is_active = False`

---

# ♻️ Restore (undo delete)

```python
camera.is_active = True
camera.save()
```

---

# ⚠️ Beginner Mistakes

❌ শুধু `is_active` add করে, filtering না করা
❌ `.objects.all()` everywhere use করা
❌ delete override না করা

---

# 🚀 Pro Level Upgrade (Optional)

👉 QuerySet level delete override

```python
class SoftDeleteQuerySet(models.QuerySet):
    def delete(self):
        return super().update(is_active=False)
```

```python
class ActiveManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(self.model, using=self._db).filter(is_active=True)
```

---

# 🧩 Real Example (Your CCTV Project)

```python
class Detection(BaseModel):
    camera = models.ForeignKey(Camera, on_delete=models.CASCADE)
    label = models.CharField(max_length=100)
```

👉 detection delete করলে:

* record থাকবে
* future analysis possible

---

# 🧭 Simple Analogy

Hard delete = 🗑️ file permanently delete
Soft delete = 📁 recycle bin এ রাখা

---

# 🎯 Final কথা

Soft delete মানে:

> “data delete না করে invisible করা”

---


Short answer: **Yes — production-level design এ almost সব important model এ soft delete field রাখা হয়**, but blindly সব model এ না 👇

---

# ✅ কখন `is_deleted` / `is_active` রাখবে?

### ✔️ MUST use (important data)

এইগুলায় অবশ্যই রাখবে:

* User-related data
* Orders / Transactions
* Camera / Detection (তোমার project 🔥)
* Logs / Alerts
* Any business-critical data

👉 কারণ: এগুলো delete করলে future এ দরকার হতে পারে

---

# ❌ কখন দরকার নাই?

এইগুলায় usually লাগে না:

* Temporary data (OTP, cache)
* Session/token table
* Auto-generated logs (massive data হলে)
* Pure junction table (many-to-many only)

👉 কারণ: এগুলো delete হলেও problem নাই

---

# 🧠 Best Practice (Industry Way)

👉 Directly সব model এ field না দিয়ে **BaseModel use করো**

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_deleted = models.BooleanField(default=False)

    class Meta:
        abstract = True
```

👉 তারপর:

```python
class Camera(BaseModel):
    name = models.CharField(max_length=100)
```

✔️ clean
✔️ reusable
✔️ scalable

---

# ⚠️ Important Decision: `is_deleted` vs `is_active`

### 🔹 Option 1: `is_deleted`

* True = deleted
* False = active

### 🔹 Option 2: `is_active`

* True = active
* False = deleted

👉 Industry te **duita-i use hoy**, but:

✔️ Simple project → `is_active`
✔️ Complex system → `is_deleted` (clear meaning)

---

# 🚨 Pro-Level Tip (VERY IMPORTANT)

👉 শুধু field রাখলেই হবে না

তোমাকে ensure করতে হবে:

```python
Model.objects.filter(is_deleted=False)
```

👉 না হলে deleted data show হবে 😑

---

# 🔥 Best Setup (Recommended)

```python
class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_deleted=False)
```

```python
class BaseModel(models.Model):
    is_deleted = models.BooleanField(default=False)

    objects = models.Manager()          # all data
    active_objects = SoftDeleteManager()  # only active

    class Meta:
        abstract = True
```

---

# 🎯 তোমার CCTV Project এর জন্য

✔ Camera → YES
✔ Detection → YES
✔ Alert → YES

❌ Frame cache / temp data → NO

---

# 🧭 Final Rule (Interview Level Answer)

👉 বলবে:

> “I use soft delete for all business-critical models via a BaseModel abstraction, but avoid it for temporary or non-critical tables to reduce unnecessary overhead.”

🔥 এই answer দিলে interviewer impress হয়ে যাবে

---

চাও তাহলে আমি তোমার project এর জন্য **full production-ready BaseModel + Manager + DRF integration (auto filter deleted data)** complete code দিয়ে দেই?
চলো তোমার **Hotel Management Project** এর জন্য একদম **production-ready Soft Delete System (BaseModel + Manager + DRF integration)** complete setup বানাই 🔥

আমি এমনভাবে দিচ্ছি যাতে:
✔ `.delete()` = soft delete
✔ API automatically deleted data hide করে
✔ চাইলে restore করা যায়
✔ clean, scalable, industry-level

---

# 🏗️ 1. BaseModel (Core 🔥)

```python
# core/models.py

from django.db import models

class SoftDeleteQuerySet(models.QuerySet):
    def delete(self):
        return super().update(is_deleted=True)

    def hard_delete(self):
        return super().delete()

    def alive(self):
        return self.filter(is_deleted=False)

    def deleted(self):
        return self.filter(is_deleted=True)


class SoftDeleteManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(self.model, using=self._db).filter(is_deleted=False)


class AllObjectsManager(models.Manager):
    def get_queryset(self):
        return SoftDeleteQuerySet(self.model, using=self._db)


class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_deleted = models.BooleanField(default=False)

    objects = SoftDeleteManager()      # 🔥 only active
    all_objects = AllObjectsManager()  # 🔥 all data

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):
        self.is_deleted = True
        self.save()

    def hard_delete(self, *args, **kwargs):
        super().delete(*args, **kwargs)

    def restore(self):
        self.is_deleted = False
        self.save()
```

---

# 🏨 2. Hotel Project Models

```python
# hotel/models.py

from django.db import models
from core.models import BaseModel

class Hotel(BaseModel):
    name = models.CharField(max_length=200)
    location = models.CharField(max_length=255)

    def __str__(self):
        return self.name


class Room(BaseModel):
    ROOM_TYPE = [
        ('single', 'Single'),
        ('double', 'Double'),
    ]

    hotel = models.ForeignKey(Hotel, on_delete=models.CASCADE, related_name='rooms')
    number = models.CharField(max_length=10)
    room_type = models.CharField(max_length=10, choices=ROOM_TYPE)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    class Meta:
        unique_together = ['hotel', 'number']


class Booking(BaseModel):
    room = models.ForeignKey(Room, on_delete=models.CASCADE, related_name='bookings')
    guest_name = models.CharField(max_length=200)
    check_in = models.DateField()
    check_out = models.DateField()
```

---

# 🔌 3. DRF Serializer

```python
# hotel/serializers.py

from rest_framework import serializers
from .models import Hotel, Room, Booking

class HotelSerializer(serializers.ModelSerializer):
    class Meta:
        model = Hotel
        fields = '__all__'


class RoomSerializer(serializers.ModelSerializer):
    class Meta:
        model = Room
        fields = '__all__'


class BookingSerializer(serializers.ModelSerializer):
    class Meta:
        model = Booking
        fields = '__all__'
```

---

# 🚀 4. DRF ViewSet (Auto Filter 🔥)

👉 এখানে magic হচ্ছে:
`objects` already filtered → deleted data আসবেই না

```python
# hotel/views.py

from rest_framework.viewsets import ModelViewSet
from .models import Hotel, Room, Booking
from .serializers import HotelSerializer, RoomSerializer, BookingSerializer


class HotelViewSet(ModelViewSet):
    queryset = Hotel.objects.all()  # 🔥 only active
    serializer_class = HotelSerializer


class RoomViewSet(ModelViewSet):
    queryset = Room.objects.all()
    serializer_class = RoomSerializer


class BookingViewSet(ModelViewSet):
    queryset = Booking.objects.all()
    serializer_class = BookingSerializer
```

---

# 🔄 5. Restore + Hard Delete API (Advanced 🔥)

```python
# hotel/views.py (extend)

from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import status


class HotelViewSet(ModelViewSet):
    queryset = Hotel.objects.all()
    serializer_class = HotelSerializer

    @action(detail=True, methods=['post'])
    def restore(self, request, pk=None):
        obj = Hotel.all_objects.get(pk=pk)
        obj.restore()
        return Response({'status': 'restored'})

    @action(detail=True, methods=['delete'])
    def hard_delete(self, request, pk=None):
        obj = Hotel.all_objects.get(pk=pk)
        obj.hard_delete()
        return Response({'status': 'permanently deleted'})
```

---

# 🔗 6. URLs

```python
# hotel/urls.py

from rest_framework.routers import DefaultRouter
from .views import HotelViewSet, RoomViewSet, BookingViewSet

router = DefaultRouter()
router.register('hotels', HotelViewSet)
router.register('rooms', RoomViewSet)
router.register('bookings', BookingViewSet)

urlpatterns = router.urls
```

---

# 🧪 7. কীভাবে কাজ করবে (IMPORTANT)

### 👉 Delete

```http
DELETE /hotels/1/
```

➡️ DB থেকে delete না
➡️ `is_deleted = True`

---

### 👉 Normal GET

```http
GET /hotels/
```

➡️ deleted data আসবে না 🔥

---

### 👉 Restore

```http
POST /hotels/1/restore/
```

---

### 👉 Permanent Delete

```http
DELETE /hotels/1/hard_delete/
```

---

# ⚠️ Final Pro Tips

✔ সব query তে `.objects` use করো (auto filter)
✔ admin panel এ `all_objects` use করতে পারো
✔ index add করো:

```python
is_deleted = models.BooleanField(default=False, db_index=True)
```

✔ large system হলে archive table consider করো

---

# 🎯 Final Summary

👉 তুমি এখন যে system বানাইছো:

* ✅ Soft delete implemented
* ✅ Auto filtering
* ✅ Restore support
* ✅ Hard delete option
* ✅ DRF integrated
* ✅ Production-ready 🔥

---

চাও তাহলে next step এ আমি তোমার জন্য
👉 **Admin panel customization (deleted data show/hide toggle)**
👉 **Query optimization (select_related, prefetch_related)**
👉 **Full scalable DB design (10M users ready)**

এইগুলোও setup করে দিতে পারি 🚀
চলো এখন তোমার **Hotel Management Project** কে একদম next level এ নিয়ে যাই 🔥
(এটাই real **production engineering mindset**)

---

# 🧩 1. Django Admin Customization (Soft Delete Toggle 🔥)

👉 Goal:

* Admin এ deleted + active data দুটোই দেখা যাবে
* filter দিয়ে toggle করা যাবে
* restore button থাকবে

---

## ✅ Admin Setup

```python
# hotel/admin.py

from django.contrib import admin
from .models import Hotel, Room, Booking


class SoftDeleteAdmin(admin.ModelAdmin):
    list_display = ('id', 'created_at', 'is_deleted')
    list_filter = ('is_deleted',)
    actions = ['restore_selected']

    def get_queryset(self, request):
        # 🔥 show ALL objects (including deleted)
        return self.model.all_objects.all()

    def restore_selected(self, request, queryset):
        queryset.update(is_deleted=False)

    restore_selected.short_description = "Restore selected items"


@admin.register(Hotel)
class HotelAdmin(SoftDeleteAdmin):
    list_display = ('id', 'name', 'location', 'is_deleted')


@admin.register(Room)
class RoomAdmin(SoftDeleteAdmin):
    list_display = ('id', 'hotel', 'number', 'is_deleted')


@admin.register(Booking)
class BookingAdmin(SoftDeleteAdmin):
    list_display = ('id', 'room', 'guest_name', 'is_deleted')
```

---

## 🎯 Result

✔ Admin panel এ filter:

* is_deleted = True / False
  ✔ bulk restore button
  ✔ full control 🔥

---

# ⚡ 2. Query Optimization (VERY IMPORTANT 🚀)

👉 তুমি backend build করছো = performance matters

---

## ❌ Problem: N+1 Query

```python
bookings = Booking.objects.all()

for b in bookings:
    print(b.room.hotel.name)
```

👉 100 booking = 201 queries 😑

---

## ✅ Solution: `select_related`

👉 ForeignKey / OneToOne এর জন্য

```python
bookings = Booking.objects.select_related('room__hotel')
```

✔ single query
✔ super fast

---

## ✅ ManyToMany / Reverse → `prefetch_related`

```python
hotels = Hotel.objects.prefetch_related('rooms')
```

---

## 🔥 DRF ViewSet Optimization

```python
class BookingViewSet(ModelViewSet):
    queryset = Booking.objects.select_related('room__hotel')
    serializer_class = BookingSerializer
```

---

## 🧠 Pro Tip

| Relation Type | Use              |
| ------------- | ---------------- |
| FK / O2O      | select_related   |
| M2M / reverse | prefetch_related |

---

# 🏗️ 3. Scalable DB Design (10M Users Ready 🔥)

👉 এখন real engineering শুরু

---

## ✅ 1. Indexing (MUST)

```python
class Booking(BaseModel):
    check_in = models.DateField(db_index=True)
    check_out = models.DateField(db_index=True)
```

👉 filter/search fast হবে

---

## ✅ 2. Composite Index

```python
class Meta:
    indexes = [
        models.Index(fields=['room', 'check_in']),
    ]
```

---

## ✅ 3. UUID instead of ID (Advanced)

```python
import uuid

id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
```

👉 security + distributed system friendly

---

## ✅ 4. Read/Write Separation (Concept)

👉 Heavy system হলে:

* Read DB (replica)
* Write DB (primary)

---

## ✅ 5. Caching (Redis 🔥)

👉 Example:

* hotel list cache
* room availability cache

---

## ✅ 6. Denormalization (Smart Use)

```python
class Booking(BaseModel):
    hotel_name = models.CharField(max_length=200)  # snapshot
```

👉 report fast হবে

---

## ✅ 7. Pagination (DRF)

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 20
}
```

---

## ✅ 8. Rate Limiting

```python
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.UserRateThrottle'
    ],
    'DEFAULT_THROTTLE_RATES': {
        'user': '100/day'
    }
}
```

---

## ✅ 9. Logging & Monitoring

```python
class AuditLog(BaseModel):
    action = models.CharField(max_length=100)
    user_id = models.IntegerField()
```

---

## 🚀 4. Ultimate Production Architecture (Simple View)

👉 Your system now:

* Django (API)
* PostgreSQL (DB)
* Redis (cache)
* Celery (background jobs)
* Nginx (reverse proxy)

---

# 🎯 Final Checklist (Production Ready ✅)

✔ Soft delete system
✔ Admin control panel
✔ Optimized queries
✔ Indexed DB
✔ Pagination
✔ Caching ready
✔ Scalable design

---

# 🧠 Interview Killer Answer

👉 যদি interviewer জিজ্ঞেস করে:

> “How do you design scalable models?”

তুমি বলবে:

> “I design models with soft delete support, proper indexing, optimized queries using select_related/prefetch_related, and ensure scalability using caching, pagination, and denormalization where needed.”

🔥 Boom — strong impression

---

চাও তাহলে next step এ আমি তোমার জন্য
👉 **Full API design (auth + permission + role-based system)**
👉 **Room booking availability algorithm (real-world logic)**
👉 **End-to-end deployment (Docker + VPS)**

এইগুলোও step-by-step বানিয়ে দিতে পারি 🚀
চলো তোমার **Hotel Management Project** এর জন্য একদম **production-level API design (Auth + Permission + Role-Based System)** বানাই 🔥
এটা করলে তোমার backend পুরো industry-ready হয়ে যাবে

---

# 🧩 1. System Design Overview

👉 আমরা 3 ধরনের user ধরছি:

* **Admin** → full control
* **Manager** → hotel manage
* **Customer** → booking only

---

# 🏗️ 2. Custom User Model (MUST 🔥)

👉 শুরুতেই custom user use করো (later change করা hard)

```python id="u8h2ka"
# users/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('manager', 'Manager'),
        ('customer', 'Customer'),
    )

    role = models.CharField(max_length=20, choices=ROLE_CHOICES, default='customer')

    def __str__(self):
        return self.username
```

---

## ⚙️ settings.py

```python id="u2d3kd"
AUTH_USER_MODEL = 'users.User'
```

---

# 🔐 3. Authentication (JWT 🔥)

👉 আমরা JWT use করবো (industry standard)

📦 install:

```bash id="zjfj8x"
pip install djangorestframework-simplejwt
```

---

## settings.py

```python id="p1h5mq"
from datetime import timedelta

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}

SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
    'AUTH_HEADER_TYPES': ('Bearer',),
}
```

---

## URLs

```python id="8wmtc9"
# users/urls.py

from django.urls import path
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [
    path('login/', TokenObtainPairView.as_view()),
    path('refresh/', TokenRefreshView.as_view()),
]
```

---

# 🔑 4. Role-Based Permission System

## ✅ Custom Permission

```python id="g8lwhb"
# users/permissions.py

from rest_framework.permissions import BasePermission

class IsAdmin(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'admin'


class IsManager(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'manager'


class IsCustomer(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'customer'
```

---

## 🔥 Advanced (Combined Permission)

```python id="o45xbo"
class IsAdminOrManager(BasePermission):
    def has_permission(self, request, view):
        return request.user.role in ['admin', 'manager']
```

---

# 🏨 5. Model-Level Ownership (IMPORTANT)

```python id="35yajz"
# hotel/models.py

class Hotel(BaseModel):
    name = models.CharField(max_length=200)
    location = models.CharField(max_length=255)
    owner = models.ForeignKey('users.User', on_delete=models.CASCADE)
```

👉 Manager only his hotel manage করতে পারবে

---

# 🚀 6. DRF ViewSet with Permissions

## 🔹 Hotel API

```python id="sv2n0c"
# hotel/views.py

from rest_framework.viewsets import ModelViewSet
from rest_framework.permissions import IsAuthenticated
from users.permissions import IsAdminOrManager
from .models import Hotel
from .serializers import HotelSerializer


class HotelViewSet(ModelViewSet):
    serializer_class = HotelSerializer
    permission_classes = [IsAuthenticated, IsAdminOrManager]

    def get_queryset(self):
        user = self.request.user

        if user.role == 'admin':
            return Hotel.objects.all()
        elif user.role == 'manager':
            return Hotel.objects.filter(owner=user)
        return Hotel.objects.none()

    def perform_create(self, serializer):
        serializer.save(owner=self.request.user)
```

---

## 🔹 Booking API (Customer)

```python id="mgs2kf"
class BookingViewSet(ModelViewSet):
    serializer_class = BookingSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        user = self.request.user

        if user.role == 'customer':
            return Booking.objects.filter(user=user)
        elif user.role in ['admin', 'manager']:
            return Booking.objects.all()

    def perform_create(self, serializer):
        serializer.save(user=self.request.user)
```

---

# 🔐 7. Object-Level Permission (Advanced 🔥)

👉 user নিজের data ছাড়া access করতে পারবে না

```python id="e7zv4c"
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.owner == request.user
```

---

# 🧪 8. API Flow (Real Example)

### 🔑 Login

```http id="h83e9p"
POST /api/auth/login/
{
  "username": "manager1",
  "password": "1234"
}
```

➡️ token return

---

### 🔐 Use Token

```http id="5w9c4y"
Authorization: Bearer <access_token>
```

---

### 🏨 Create Hotel (Manager)

```http id="0h6qha"
POST /api/hotels/
```

✔ auto owner set

---

### 📅 Booking (Customer)

```http id="44y1i4"
POST /api/bookings/
```

✔ only own booking

---

# ⚠️ Security Best Practices

✔ Password hash (default Django)
✔ JWT expiry short রাখো
✔ HTTPS use করো
✔ Role check always backend এ

---

# 🚀 9. Bonus (Pro Level)

👉 Future upgrade:

* Permission per action (`get_permissions()`)
* RBAC table (dynamic roles)
* API rate limit
* Audit logging

---

# 🎯 Final Architecture

✔ Custom User Model
✔ JWT Auth
✔ Role-Based Permission
✔ Object-Level Security
✔ Owner Filtering
✔ Clean DRF ViewSet

---

# 🧠 Interview Answer

> “I implement JWT-based authentication with a custom user model and role-based permissions, ensuring both view-level and object-level access control for secure and scalable APIs.”

---

🔥 এখন তুমি চাইলে next step এ আমি তোমার জন্য:

👉 **Room availability algorithm (real-world booking logic)**
👉 **Payment integration structure**
👉 **Docker + Deployment (live project)**

এইগুলোও production-level করে দিতে পারি 🚀
চলো এখন তোমার **Hotel Management System** এর সবচেয়ে important partটা করি —
👉 **Real-world Room Availability Algorithm (Production-Level 🔥)**

এটা interview + real project দুটাতেই game changer।

---

# 🧠 1. Problem বুঝি (Core Logic)

👉 Question:

> “এই room কি given date range এ available?”

### 📅 Input:

* room_id
* check_in
* check_out

### ❗ Rule:

Room **available হবে না** যদি existing booking এর সাথে overlap করে

---

# ⚠️ Overlap Logic (VERY IMPORTANT)

👉 Two date range overlap করে যদি:

\text{Overlap যদি } (check_in < existing_out) ; \text{AND} ; (check_out > existing_in)

---

# 🏗️ 2. Model Update (Booking)

```python
class Booking(BaseModel):
    room = models.ForeignKey(Room, on_delete=models.CASCADE, related_name='bookings')
    user = models.ForeignKey('users.User', on_delete=models.CASCADE)

    check_in = models.DateField()
    check_out = models.DateField()

    status = models.CharField(
        max_length=20,
        choices=[
            ('pending', 'Pending'),
            ('confirmed', 'Confirmed'),
            ('cancelled', 'Cancelled'),
        ],
        default='pending'
    )

    class Meta:
        indexes = [
            models.Index(fields=['room', 'check_in', 'check_out']),
        ]
```

---

# ⚡ 3. Core Availability Function

```python
from django.db.models import Q

def is_room_available(room, check_in, check_out):
    return not Booking.objects.filter(
        room=room,
        status__in=['pending', 'confirmed']
    ).filter(
        Q(check_in__lt=check_out) &
        Q(check_out__gt=check_in)
    ).exists()
```

---

## 🎯 কী হচ্ছে এখানে?

👉 Query meaning:

* same room
* booking overlap
* not cancelled

👉 যদি এমন booking থাকে → NOT available ❌
👉 না থাকলে → available ✅

---

# 🚀 4. Booking Create Logic (Production 🔥)

```python
from rest_framework.exceptions import ValidationError

def create_booking(room, user, check_in, check_out):
    if check_in >= check_out:
        raise ValidationError("Invalid date range")

    if not is_room_available(room, check_in, check_out):
        raise ValidationError("Room is not available")

    return Booking.objects.create(
        room=room,
        user=user,
        check_in=check_in,
        check_out=check_out,
        status='confirmed'
    )
```

---

# 🔌 5. DRF Serializer Validation

```python
class BookingSerializer(serializers.ModelSerializer):

    class Meta:
        model = Booking
        fields = '__all__'

    def validate(self, data):
        room = data['room']
        check_in = data['check_in']
        check_out = data['check_out']

        if check_in >= check_out:
            raise serializers.ValidationError("Invalid date range")

        if not is_room_available(room, check_in, check_out):
            raise serializers.ValidationError("Room not available")

        return data
```

---

# ⚡ 6. High Performance Version (Scaling 🔥)

👉 Multiple rooms check

```python
available_rooms = Room.objects.exclude(
    bookings__status__in=['pending', 'confirmed'],
    bookings__check_in__lt=check_out,
    bookings__check_out__gt=check_in
)
```

👉 এক query তেই available rooms 🔥

---

# 🧠 7. Edge Cases (Real World)

### ✔ Same day checkout → allowed

* User A: 1-5
* User B: 5-10 ✅

👉 No overlap

---

### ❌ Full overlap

* 1-10
* 3-6 ❌

---

### ❌ Partial overlap

* 1-5
* 4-8 ❌

---

### ✔ Cancelled booking ignore

```python
status='cancelled'
```

---

# 🔥 8. Race Condition (ADVANCED ⚠️)

👉 Problem:
2 user same time booking করলে double booking হতে পারে 😑

---

## ✅ Solution (Transaction Lock)

```python
from django.db import transaction

@transaction.atomic
def safe_booking(room, user, check_in, check_out):
    if not is_room_available(room, check_in, check_out):
        raise Exception("Already booked")

    return Booking.objects.create(
        room=room,
        user=user,
        check_in=check_in,
        check_out=check_out
    )
```

---

## 🔥 Pro Level (DB Lock)

```python
Room.objects.select_for_update().get(id=room.id)
```

👉 concurrent booking prevent

---

# ⚡ 9. Extra Features (Industry)

✔ buffer time (cleaning gap)
✔ pricing per day
✔ seasonal pricing
✔ overbooking logic (airlines style 😄)

---

# 🎯 Final Flow (Real System)

1. User selects date
2. Backend checks availability
3. Lock room (optional)
4. Create booking
5. Payment
6. Confirm

---

# 🧠 Interview Killer Answer

> “I implement room availability using an overlap detection query with indexed date fields, ensure consistency using transactions, and optimize performance using exclusion queries for bulk availability checks.”

---

🔥 এখন তুমি চাইলে next step:

👉 **Payment system design (Stripe / SSLCommerz)**
👉 **Real-time availability (Redis + WebSocket)**
👉 **Full system architecture diagram**

এইগুলোও production-level করে দিতে পারি 🚀
