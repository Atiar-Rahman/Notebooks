
# 🚀 DAY 1 PLAN (Django + DRF Setup + Register API)

## 🎯 Goal:

👉 Django project + DRF setup + **User Registration API**

---

# 🧱 Step 1: Project Setup

```bash
mkdir drf_project
cd drf_project

python -m venv env
source env/bin/activate   # (Windows: env\Scripts\activate)

pip install django djangorestframework
```

---

## 👉 Django project create

```bash
django-admin startproject config .
python manage.py startapp accounts
```

---

## 👉 settings.py edit

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
    'accounts',
]
```

---

# 🧩 Step 2: Custom User Model (IMPORTANT 🔥)

👉 accounts/models.py

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    email = models.EmailField(unique=True)

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['username']
```

---

## 👉 settings.py add

```python
AUTH_USER_MODEL = 'accounts.User'
```

---

## 👉 migrate

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# 🔌 Step 3: Serializer

👉 accounts/serializers.py

```python
from rest_framework import serializers
from .models import User

class RegisterSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = ['id', 'email', 'username', 'password']

    def create(self, validated_data):
        user = User.objects.create_user(**validated_data)
        return user
```

---

# 🌐 Step 4: API View

👉 accounts/views.py

```python
from rest_framework import generics
from .models import User
from .serializers import RegisterSerializer

class RegisterView(generics.CreateAPIView):
    queryset = User.objects.all()
    serializer_class = RegisterSerializer
```

---

# 🔗 Step 5: URL Setup

👉 accounts/urls.py

```python
from django.urls import path
from .views import RegisterView

urlpatterns = [
    path('register/', RegisterView.as_view(), name='register'),
]
```

👉 config/urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('accounts.urls')),
]
```

---

# ▶️ Step 6: Run Server

```bash
python manage.py runserver
```

---

# 🧪 Test API

👉 POST request:

```
http://127.0.0.1:8000/api/register/
```

👉 JSON:

```json
{
  "email": "test@gmail.com",
  "username": "testuser",
  "password": "12345678"
}
```

---

# ✅ Expected Result

```json
{
  "id": 1,
  "email": "test@gmail.com",
  "username": "testuser"
}
```

---

# 💥 Bonus (If time thake)

👉 Password validation add করো:

```python
def validate_password(self, value):
    if len(value) < 6:
        raise serializers.ValidationError("Password too short")
    return value
```

---

# 🎯 DAY 1 DONE CHECKLIST

✔ Project setup
✔ DRF install
✔ Custom User model
✔ Register API

---

# **custom user model fully control** করতে পারবা 🔥

---

# 🧩 Custom User Model এ নতুন field add করা

👉 তুমি এখন এই model use করছো:

```python
class User(AbstractUser):
    email = models.EmailField(unique=True)

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['username']
```

---

# ✅ এখন নতুন field add করতে চাইলে

👉 তুমি direct নতুন field add করতে পারো:

## 🔹 Example:

```python
class User(AbstractUser):
    email = models.EmailField(unique=True)

    # 🔥 new fields
    phone = models.CharField(max_length=15, blank=True, null=True)
    profile_image = models.ImageField(upload_to='profiles/', blank=True, null=True)
    is_verified = models.BooleanField(default=False)

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['username']
```

---

# ⚙️ এরপর কি করতে হবে?

## 1️⃣ Migration

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 2️⃣ Serializer update (VERY IMPORTANT ❗)

👉 না করলে API তে field আসবে না

```python
class RegisterSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'email', 'username', 'password', 'phone']
```

---

## 3️⃣ Admin panel এ দেখাতে চাইলে

👉 accounts/admin.py

```python
from django.contrib import admin
from .models import User

admin.site.register(User)
```

---

# 🔥 Advanced (Expert Tip)

👉 যদি field **required করতে চাও**:

```python
phone = models.CharField(max_length=15)
```

👉 যদি optional:

```python
blank=True, null=True
```

---

# ⚠️ VERY IMPORTANT RULE

👉 Custom User Model change করলে:

❌ project start হওয়ার পরে বড় change কোরো না
👉 না হলে migration problem হবে 💀

---

# 💡 Real-world useful fields

তুমি SaaS project করতেছো, so এগুলো add করতে পারো:

```python
role = models.CharField(max_length=10, choices=[
    ('admin', 'Admin'),
    ('user', 'User')
], default='user')

created_at = models.DateTimeField(auto_now_add=True)
```

---

# 🎯 Summary

👉 Field add =

1. Model এ add
2. migrate
3. serializer update

---

চল 🔥 — **Day 2 = Login + JWT Authentication (REAL SECURITY)**
আজ থেকে তোমার API “secure system” হয়ে যাবে 💀

---

# 🚀 DAY 2 GOAL

👉 তুমি আজ শিখবা:

* Login API
* JWT (access + refresh token)
* Protected API

---

# 🔐 JWT কী?

👉 JSON Web Token = login করলে server তোমাকে একটা token দেয়
👉 এরপর সব request এ token দিয়ে authentication হয়

---

# 🧱 Step 1: Install JWT

```bash
pip install djangorestframework-simplejwt
```

---

# ⚙️ Step 2: settings.py

```python
from datetime import timedelta

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}
```

---

## 🔑 JWT Config

```python
SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=60),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
    'AUTH_HEADER_TYPES': ('Bearer',),
}
```

---

# 🔌 Step 3: Login Serializer

👉 accounts/serializers.py

```python
from django.contrib.auth import authenticate
from rest_framework import serializers

class LoginSerializer(serializers.Serializer):
    email = serializers.EmailField()
    password = serializers.CharField()

    def validate(self, data):
        user = authenticate(
            username=data['email'],
            password=data['password']
        )

        if not user:
            raise serializers.ValidationError("Invalid credentials")

        data['user'] = user
        return data
```

---

# 🌐 Step 4: Login View (JWT Token Generate)

👉 accounts/views.py

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from .serializers import LoginSerializer
from rest_framework_simplejwt.tokens import RefreshToken

class LoginView(APIView):
    def post(self, request):
        serializer = LoginSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        user = serializer.validated_data['user']

        refresh = RefreshToken.for_user(user)

        return Response({
            "message": "Login successful",
            "access": str(refresh.access_token),
            "refresh": str(refresh),
            "user": {
                "id": user.id,
                "email": user.email,
                "role": user.role
            }
        }, status=status.HTTP_200_OK)
```

---

# 🔗 Step 5: URL

👉 accounts/urls.py

```python
from .views import LoginView

urlpatterns = [
    path('login/', LoginView.as_view(), name='login'),
]
```

---

# ▶️ Step 6: Test Login

👉 POST `/api/login/`

```json
{
  "email": "test@gmail.com",
  "password": "12345678"
}
```

---

# ✅ Response

```json
{
  "message": "Login successful",
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIs...",
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": 1,
    "email": "test@gmail.com",
    "role": "user"
  }
}
```

---

# 🔒 Step 7: Protected API

👉 accounts/views.py

```python
from rest_framework.permissions import IsAuthenticated

class ProfileView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response({
            "email": request.user.email,
            "role": request.user.role
        })
```

---

# 🔗 URL add

```python
path('profile/', ProfileView.as_view()),
```

---

# 🧪 Test Protected API

👉 Header add করো:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

---

# 💥 Result

```json
{
  "email": "test@gmail.com",
  "role": "user"
}
```

---

# 🎯 DAY 2 CHECKLIST

✔ Login API
✔ JWT token generate
✔ Access + Refresh
✔ Protected route

---

# ⚠️ Common Mistake

❌ Token না দিয়ে API call করা
❌ Bearer miss করা
❌ wrong header

---

# 🔥 Expert Tip

👉 Frontend এ:

* access token → API call
* refresh token → renew

---

# 🚀 Tomorrow (Day 3)

👉 Custom permissions (admin only API)
👉 Role-based access control
👉 Real-world security

---

# ⚡ Now YOUR TASK

👉 Login API implement করো
👉 Profile API test করো

-----------
চল 🔥 — **Day 3 = Role-Based Permission (REAL BACKEND POWER 💀)**

আজ থেকে তুমি শুধু API বানাচ্ছো না…
👉 তুমি **control করবা কে কি করতে পারবে** — এটাকেই বলে real backend engineering

---

# 🚀 DAY 3 GOAL

👉 তুমি আজ শিখবা:

* Custom Permission
* Admin vs User access
* Secure API design

---

# 🧠 Problem বুঝো

👉 এখন তোমার system এ:

* User login করতে পারে ✔
* Token আছে ✔

❌ কিন্তু:

* কে admin?
* কে user?
* কে কি করতে পারবে?

👉 আজ এটা solve করবো

---

# 🔥 Step 1: Custom Permission তৈরি

👉 accounts/permissions.py

```python id="pn8k3v"
from rest_framework.permissions import BasePermission

class IsAdminUserRole(BasePermission):
    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == 'admin'
```

---

# 🔒 Step 2: Admin-only API

👉 accounts/views.py

```python id="3m2o4h"
from rest_framework.views import APIView
from rest_framework.response import Response
from .permissions import IsAdminUserRole

class AdminOnlyView(APIView):
    permission_classes = [IsAdminUserRole]

    def get(self, request):
        return Response({
            "message": "Welcome Admin 🔥"
        })
```

---

# 🔗 URL add

```python id="9vxk47"
path('admin-only/', AdminOnlyView.as_view()),
```

---

# 🧪 Test Case

## ❌ Normal User

👉 Access denied:

```json id="3blm27"
{
  "detail": "You do not have permission to perform this action."
}
```

---

## ✅ Admin User

👉 Access granted:

```json id="p6azjq"
{
  "message": "Welcome Admin 🔥"
}
```

---

# 🔥 Step 3: Mixed Permission (Advanced)

👉 accounts/permissions.py

```python id="g3gkux"
class IsAdminOrReadOnly(BasePermission):
    def has_permission(self, request, view):
        if request.method == 'GET':
            return True
        return request.user.role == 'admin'
```

---

# 💡 Use Case

👉 GET → সবাই দেখতে পারবে
👉 POST/PUT/DELETE → শুধু admin

---

# 🧱 Example

```python id="xqpf91"
class CourseView(APIView):
    permission_classes = [IsAdminOrReadOnly]
```

---

# 🔥 Step 4: Real-world Role Use

👉 Example:

```python id="2frs4h"
if request.user.role == 'admin':
    # full access
elif request.user.role == 'user':
    # limited access
```

---

# ⚠️ SECURITY RULE

👉 NEVER trust frontend ❌
👉 Always check role in backend ✔

---

# 🎯 DAY 3 CHECKLIST

✔ Custom permission
✔ Admin-only API
✔ Role-based logic
✔ Secure backend

---

# 💥 Expert Mindset

👉 এখন তুমি:

* শুধু developer না ❌
* তুমি backend architect level এ ঢুকতেছো 🔥

---

# 🚀 Tomorrow (Day 4)

👉 Serializer deep dive
👉 Custom validation (advanced)
👉 Clean API structure

---

# ⚡ Now YOUR TASK

👉 Admin user manually DB তে set করো:

```python id="8hrgzi"
user.role = 'admin'
user.save()
```

👉 Admin API test করো


------
#  **Day 4 = Serializer Deep Dive (Expert Level Core 💀)**

আজকের দিনটা খুব important —  
👉 **DRF-এ 70% power = Serializer**  
এটা master করলে তুমি clean, secure, scalable API বানাতে পারবা

---

# 🚀 DAY 4 GOAL

👉 তুমি আজ শিখবা:

- Advanced validation
    
- Custom fields
    
- Read vs Write control
    
- Clean API response design
    

---

# 🧠 Serializer আসলে কী?

👉 Serializer =  
✔ Data validate করে  
✔ DB save করে  
✔ JSON → Python & Python → JSON convert করে

---

# 🔥 Step 1: Advanced Validation

👉 accounts/serializers.py

```python
class RegisterSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = ['id', 'email', 'username', 'password']

    def validate_email(self, value):
        if not value.endswith('@gmail.com'):
            raise serializers.ValidationError("Only Gmail allowed")
        return value

    def validate(self, data):
        if data['username'] == data['email']:
            raise serializers.ValidationError("Username and email can't be same")
        return data
```

---

# 🔥 Step 2: Read vs Write Control

👉 Sensitive field hide করতে:

```python
password = serializers.CharField(write_only=True)
```

👉 Only show (input না নেওয়া):

```python
created_at = serializers.DateTimeField(read_only=True)
```

---

# 🔥 Step 3: Custom Response Field

👉 extra field add করা (DB-তে নেই কিন্তু response এ আছে)

```python
class UserSerializer(serializers.ModelSerializer):
    is_admin = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['id', 'email', 'role', 'is_admin']

    def get_is_admin(self, obj):
        return obj.role == 'admin'
```

---

# 💥 Output:

```json
{
  "id": 1,
  "email": "test@gmail.com",
  "role": "admin",
  "is_admin": true
}
```

---

# 🔥 Step 4: Nested Serializer (🔥 IMPORTANT)

👉 Example: User + Courses

```python
class CourseSerializer(serializers.ModelSerializer):
    class Meta:
        model = Course
        fields = '__all__'


class UserSerializer(serializers.ModelSerializer):
    courses = CourseSerializer(many=True, read_only=True)

    class Meta:
        model = User
        fields = ['id', 'email', 'courses']
```

---

# 🔥 Step 5: Override create/update (Expert move)

```python
def create(self, validated_data):
    validated_data['role'] = 'user'
    return User.objects.create_user(**validated_data)
```

---

# ⚠️ Common Mistakes

❌ সব logic view-এ লেখা  
👉 ✔ logic serializer-এ রাখো

❌ password plain save করা  
👉 ✔ create_user use করো

---

# 🎯 DAY 4 CHECKLIST

✔ Field validation  
✔ Object validation  
✔ Read/Write control  
✔ Custom field  
✔ Nested serializer

---

# 💥 Real-world Impact

👉 তুমি এখন পারবা:

- Clean API design
    
- Frontend-friendly response
    
- Secure data handling
    
---

# 🧠 কেন পারবে না?

তুমি লিখেছো:

```python
is_admin = serializers.SerializerMethodField()
```

👉 এর মানে:

* এটা **read-only field**
* এটা **database এ save হয় না**
* এটা শুধু **response এ দেখানোর জন্য**

---

# 🔍 ভিতরের logic

```python
def get_is_admin(self, obj):
    return obj.role == 'admin'
```

👉 এখানে:

* `is_admin` depend করছে `role` এর উপর
* user direct `is_admin` change করতে পারবে না
* **role change করলেই only change হবে**

---

# ⚠️ REAL SECURITY ISSUE (IMPORTANT 🚨)

👉 আসল সমস্যা এখানে 👇

```json
{
  "role": "admin"
}
```

👉 যদি user API তে এইটা পাঠাতে পারে →
💀 সে নিজেকে admin বানিয়ে ফেলতে পারে

---

# 🔥 Proper Fix (MUST DO)

## ✅ Register / Create এ force করো

```python
def create(self, validated_data):
    validated_data['role'] = 'user'  # force user
    return User.objects.create_user(**validated_data)
```

---

## ✅ Update এ block করো

```python
def update(self, instance, validated_data):
    validated_data.pop('role', None)  # role change block
    return super().update(instance, validated_data)
```

---

# 🔒 Extra Secure (Best Practice)

👉 Serializer এ role read-only করে দাও:

```python
class UserSerializer(serializers.ModelSerializer):
    is_admin = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['id', 'email', 'role', 'is_admin']
        read_only_fields = ['role']
```

---

# 💥 Final Understanding

| Field                     | User Change করতে পারবে? |
| ------------------------- | ----------------------- |
| is_admin                  | ❌ না                    |
| role (without protection) | ⚠️ হ্যাঁ (danger)       |
| role (after fix)          | ❌ না                    |

---

# 🔥 Pro Tip

👉 Admin role change করবে:

* Django admin panel থেকে
* বা admin-only API দিয়ে

---

# 🎯 Summary

👉 `is_admin` safe ✔
👉 `role` unsafe (if not protected) ❌
👉 Fix করলে = production-ready ✔

---

# ⚡ Next Step

তুমি যদি এটা বুঝে ফেলো → তুমি already **security-aware backend dev** 🔥

👉 বলো:
**“Day 5”**

আজ থেকে আমরা DRF-এর real power (ViewSet + Router) শুরু করবো 🚀


-----
একদম clean question 🔥 — এটা বুঝলে তুমি serializer fully বুঝে ফেলবা

---

# 🎯 Short Answer

👉 **`SerializerMethodField`**

- ✅ Response এ যাবে
    
- ❌ Request এ আসবে না (input হিসেবে নেওয়া যাবে না)
    

---

# 🧠 কেন?

```python
is_admin = serializers.SerializerMethodField()
```

👉 এর মানে:

- এটা **read-only field**
    
- এটা শুধু backend থেকে calculate হয়
    
- client (frontend/user) এটা send করতে পারে না
    

---

# 🔍 Example

## 👉 Serializer

```python
class UserSerializer(serializers.ModelSerializer):
    is_admin = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['id', 'email', 'role', 'is_admin']

    def get_is_admin(self, obj):
        return obj.role == 'admin'
```

---

## 📤 Response (server → client)

```json
{
  "id": 1,
  "email": "test@gmail.com",
  "role": "user",
  "is_admin": false
}
```

✔ এখানে `is_admin` আছে

---

## 📥 Request (client → server)

```json
{
  "email": "test@gmail.com",
  "is_admin": true
}
```

👉 DRF কী করবে?

❌ **ignore করবে**  
👉 কারণ এটা writeable field না

---

# ⚠️ Important Rule

👉 DRF-এ field দুই ধরনের:

|Type|Example|Request এ আসবে?|Response এ যাবে?|
|---|---|---|---|
|Read-only|`SerializerMethodField`|❌ না|✅ হ্যাঁ|
|Write-only|password|✅ হ্যাঁ|❌ না|
|Normal|email|✅ হ্যাঁ|✅ হ্যাঁ|

---

# 🔥 যদি request এ নিতে চাও?

👉 তাহলে `SerializerMethodField` use করা যাবে না ❌

👉 Instead:

```python
is_admin = serializers.BooleanField()
```

কিন্তু ❗  
👉 এটা dangerous (user control পাবে)

---

# 💥 Best Practice

👉 `SerializerMethodField` use করো যখন:

- calculated field
    
- derived data
    
- safe info
    

---

# 🧠 Real-world Examples

👉 এগুলো সব `SerializerMethodField` দিয়ে করা হয়:

- is_admin
    
- full_name
    
- total_orders
    
- profile_completion %
    

---

# 🎯 Final Summary

👉 `SerializerMethodField` =

- server calculate করে ✔
    
- response এ যায় ✔
    
- request এ আসে না ❌
    

---

# ⚡ Next Step

তুমি এখন serializer deep বুঝে গেছো 🔥

👉 বলো:  
**“Day 5”**

আজ আমরা DRF-এর **ViewSet + Router (pro structure)** শুরু করবো 🚀

-----
ভালো 🔥 — এখন তুমি আসল জায়গায় ঢুকছো:
👉 **“serializer থেকে extra field কিভাবে নেওয়া যায়?”**

এটার ২টা meaning হয়, আমি দুটোই clear করে দিচ্ছি 👇

---

# 🎯 Case 1: Response এ extra field add করতে চাই (Most Common)

👉 এটা তুমি already দেখছো — `SerializerMethodField`

## ✅ Example:

```python
class UserSerializer(serializers.ModelSerializer):
    full_name = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['id', 'email', 'full_name']

    def get_full_name(self, obj):
        return f"{obj.first_name} {obj.last_name}"
```

👉 Output:

```json
{
  "email": "test@gmail.com",
  "full_name": "John Doe"
}
```

✔ DB-তে নেই
✔ কিন্তু response এ আছে

---

# 🎯 Case 2: Request থেকেও extra field নিতে চাই (IMPORTANT)

👉 ধরো frontend পাঠাবে:

```json
{
  "email": "test@gmail.com",
  "password": "123456",
  "confirm_password": "123456"
}
```

👉 কিন্তু `confirm_password` model এ নাই

---

## ✅ Solution:

```python
class RegisterSerializer(serializers.ModelSerializer):
    confirm_password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = ['email', 'password', 'confirm_password']

    def validate(self, data):
        if data['password'] != data['confirm_password']:
            raise serializers.ValidationError("Password mismatch")
        return data

    def create(self, validated_data):
        validated_data.pop('confirm_password')  # remove extra field
        return User.objects.create_user(**validated_data)
```

---

# 🎯 Case 3: Model এ নাই, but manually add (Advanced)

👉 Example:

```python
extra_info = serializers.CharField(write_only=True)
```

👉 তারপর use করো:

```python
def create(self, validated_data):
    extra = validated_data.pop('extra_info')
    print(extra)  # use it
    return super().create(validated_data)
```

---

# ⚠️ Important Concept

👉 Serializer field 3 type:

| Type              | Use                 |
| ----------------- | ------------------- |
| Model field       | DB save হয়          |
| Extra write field | শুধু request এ আসে  |
| Method field      | শুধু response এ যায় |

---

# 🔥 Real-world Examples

👉 তুমি future এ এগুলো ব্যবহার করবা:

* confirm_password
* OTP
* referral_code
* discount_code

---

# 💥 Pro Tip

👉 Rule মনে রাখো:

* Response extra → `SerializerMethodField`
* Request extra → `CharField(write_only=True)`
* Save করার আগে → `pop()`

---

# 🎯 Summary

👉 extra field নিতে পারো 2 way:

1. Response → MethodField
2. Request → write_only field

---

# ⚡ Next Step

তুমি এখন serializer fully বুঝে ফেলছো 🔥

👉 বলো:
**“Day 5”**

আমি তোমাকে **ViewSet + Router (real DRF structure)** শেখাবো 🚀
এইটা খুবই important question 🔥 — **serializer design = clean API + security**

আমি একদম simple করে rule set দিচ্ছি 👇

---

# 🎯 1. `read_only=True` কখনো দিবা?

👉 যখন field:

* user input দিতে পারবে না ❌
* backend auto generate করবে ✔
* শুধু response এ দেখাতে চাও ✔

---

## ✅ Example

```python
created_at = serializers.DateTimeField(read_only=True)
```

👉 কেন?

* user date set করবে না
* server auto set করবে

---

## 🔥 আরো example

```python
id = serializers.IntegerField(read_only=True)
role = serializers.CharField(read_only=True)
```

👉 `role` কেন read_only?
👉 user যেন নিজে admin না হতে পারে 💀

---

# 🎯 2. `write_only=True` কখনো দিবা?

👉 যখন field:

* user input দিবে ✔
* response এ দেখাতে চাও না ❌

---

## ✅ Example

```python
password = serializers.CharField(write_only=True)
```

👉 কেন?

* user password দিবে ✔
* response এ password দেখানো dangerous ❌

---

## 🔥 আরো example

```python
confirm_password = serializers.CharField(write_only=True)
otp = serializers.CharField(write_only=True)
```

---

# 🎯 3. কিছুই দিবা না (default case)

👉 যখন field:

* request এ আসবে ✔
* response এও যাবে ✔

---

## ✅ Example

```python
email = serializers.EmailField()
username = serializers.CharField()
```

---

# ⚖️ Full Comparison

| Field Type | Request | Response | Use Case             |
| ---------- | ------- | -------- | -------------------- |
| read_only  | ❌       | ✅        | id, role, created_at |
| write_only | ✅       | ❌        | password, otp        |
| default    | ✅       | ✅        | email, username      |

---

# 🔥 Real Example (Perfect Serializer)

```python
class UserSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)
    role = serializers.CharField(read_only=True)
    is_admin = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['id', 'email', 'password', 'role', 'is_admin']

    def get_is_admin(self, obj):
        return obj.role == 'admin'
```

---

# ⚠️ Common Mistake

❌ role default রাখলে
👉 user request এ role পাঠিয়ে admin হয়ে যাবে 💀

✔ তাই read_only করো

---

# 🧠 Easy Rule (মনে রাখার shortcut)

👉 **User control করবে? → YES → write/default**
👉 **User control করবে না? → read_only**

---

# 💥 Expert Mindset

👉 API design মানে শুধু data না
👉 **security + control + clean response**

---

# 🎯 Final Summary

👉 read_only → backend control
👉 write_only → sensitive input
👉 default → normal data

---

# ⚡ Next

তুমি এখন serializer master হয়ে যাচ্ছো 🔥

👉 বলো:
**“Day 5”**

আজ আমরা DRF-এর **ViewSet + Router (code 50% কম 😎)** শুরু করবো 🚀


-------
ভালো 🔥 — “**serializer এ extra keyword**” বলতে সাধারণত DRF-এ ২টা জিনিস বোঝায়। আমি দুটোই clear করে দিচ্ছি 👇

---

# 🎯 1. `extra_kwargs` (MOST IMPORTANT)

👉 এটা use হয় **existing field-এর behavior change করতে**

---

## ✅ Example

```python
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'email', 'password', 'role']

        extra_kwargs = {
            'password': {'write_only': True},
            'role': {'read_only': True}
        }
```

---

## 🔥 কেন use করবো?

👉 আলাদা করে field define না করে shortcut নেওয়ার জন্য

❌ Without extra_kwargs:

```python
password = serializers.CharField(write_only=True)
```

✔ With extra_kwargs:

```python
extra_kwargs = {
    'password': {'write_only': True}
}
```

---

# 🎯 2. Extra field (model এ নাই কিন্তু serializer এ আছে)

👉 এটাও অনেক সময় “extra field” বলা হয়

---

## ✅ Example

```python
confirm_password = serializers.CharField(write_only=True)
```

👉 এটা model এ নাই
👉 কিন্তু request handle করার জন্য use হচ্ছে

---

# 🎯 3. SerializerMethodField (extra response field)

👉 এটাও extra field category

```python
is_admin = serializers.SerializerMethodField()
```

👉 এটা শুধু response এ যায়

---

# ⚖️ Difference (সব clear)

| Type         | Example             | কাজ                   |
| ------------ | ------------------- | --------------------- |
| extra_kwargs | password write_only | existing field modify |
| extra field  | confirm_password    | request extra         |
| method field | is_admin            | response extra        |

---

# 🔥 Real-world Combined Example

```python
class RegisterSerializer(serializers.ModelSerializer):
    confirm_password = serializers.CharField(write_only=True)
    is_admin = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ['email', 'password', 'confirm_password', 'role', 'is_admin']

        extra_kwargs = {
            'password': {'write_only': True},
            'role': {'read_only': True}
        }

    def get_is_admin(self, obj):
        return obj.role == 'admin'
```

---

# 🧠 Easy Rule

👉 existing field modify → `extra_kwargs`
👉 new field add → direct define
👉 calculated field → `SerializerMethodField`

---

# 🎯 Summary

👉 “extra keyword” বলতে mostly বোঝায়:

* `extra_kwargs` ✔
* extra fields ✔
* method fields ✔

---

# ⚡ Next Step

তুমি এখন serializer full clear 🔥

👉 বলো:
**“Day 5”**

আজ আমরা DRF-এর **ViewSet + Router (real project structure)** শুরু করবো 🚀

---------
চল 🔥 — **Day 5 = ViewSet + Router (DRF Magic 💀)**

আজকের পর তুমি বুঝবা কেন DRF এত powerful 😎
👉 **Code 50% কম + structure clean + scalable**

---

# 🚀 DAY 5 GOAL

👉 তুমি আজ শিখবা:

* ViewSet কি
* Router কি
* CRUD auto generate
* Clean API structure

---

# 🧠 Problem (আগে কী করতেছিলে)

👉 আগে:

```python
RegisterView
LoginView
ProfileView
```

❌ আলাদা আলাদা view
❌ code বেশি
❌ messy structure

---

# 🔥 Solution = ViewSet

👉 ViewSet =
💥 **একটাই class → সব CRUD handle করবে**

---

# 🧱 Step 1: Example Model (Course)

👉 models.py

```python
class Course(models.Model):
    title = models.CharField(max_length=100)
    description = models.TextField()
```

---

# 🔌 Step 2: Serializer

```python
class CourseSerializer(serializers.ModelSerializer):
    class Meta:
        model = Course
        fields = '__all__'
```

---

# ⚡ Step 3: ViewSet (🔥 MAIN PART)

👉 views.py

```python
from rest_framework.viewsets import ModelViewSet
from .models import Course
from .serializers import CourseSerializer

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
```

---

# 🤯 কি হলো এখন?

👉 Automatically পেয়ে গেলে:

| Method | URL          | কাজ      |
| ------ | ------------ | -------- |
| GET    | /courses/    | list     |
| POST   | /courses/    | create   |
| GET    | /courses/id/ | retrieve |
| PUT    | /courses/id/ | update   |
| DELETE | /courses/id/ | delete   |

---

# 🔗 Step 4: Router (🔥 MAGIC)

👉 urls.py

```python
from rest_framework.routers import DefaultRouter
from .views import CourseViewSet

router = DefaultRouter()
router.register('courses', CourseViewSet)

urlpatterns = router.urls
```

---

# 💥 Final API

👉 `/courses/`
👉 `/courses/1/`

✔ সব auto generate 🎉

---

# 🔒 Step 5: Permission add

```python
from rest_framework.permissions import IsAuthenticated

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    permission_classes = [IsAuthenticated]
```

---

# 🔥 Step 6: Role-based control

👉 শুধু admin create করতে পারবে:

```python
from .permissions import IsAdminUserRole

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer

    def get_permissions(self):
        if self.action == 'create':
            return [IsAdminUserRole()]
        return [IsAuthenticated()]
```

---

# 🎯 DAY 5 CHECKLIST

✔ ViewSet use
✔ Router setup
✔ CRUD auto
✔ Permission control

---

# 💥 Real Impact

👉 আগে:
❌ 5টা view
👉 এখন:
✔ 1টা ViewSet

---

# 🔥 Advanced (Expert Move)

👉 Custom action add করতে পারো:

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class CourseViewSet(ModelViewSet):

    @action(detail=False, methods=['get'])
    def my_courses(self, request):
        return Response({"msg": "Custom API"})
```

👉 URL:

```
/courses/my_courses/
```

---

# ⚠️ Common Mistake

❌ permission ভুল দেওয়া
❌ queryset optimize না করা

---

# 🧠 Mindset

👉 DRF expert =
✔ ViewSet
✔ Router
✔ Clean architecture

---

# 🚀 Tomorrow (Day 6)

👉 Filtering + Search + Pagination
👉 Real production API features

---

# ⚡ Now YOUR TASK

👉 Course model + ViewSet বানাও
👉 CRUD test করো

---

তারপর বলো:
**“Day 6”**

আমি তোমাকে production-level API features শেখাবো 🚀🔥

-----------
চল 🔥 — **Day 6 = Filtering + Search + Pagination (Production API 💀)**

আজ থেকে তোমার API **real-world usable** হয়ে যাবে 😎
👉 User হাজার data থেকেও easily খুঁজে পাবে

---

# 🚀 DAY 6 GOAL

👉 তুমি আজ শিখবা:

* Filtering
* Search
* Pagination
* Clean list API

---

# 🧠 Problem

👉 এখন `/courses/` call করলে:

* সব data একসাথে আসে ❌
* slow হয়ে যায় ❌
* user কিছু খুঁজতে পারে না ❌

---

# 🔥 Step 1: Install Filter

```bash
pip install django-filter
```

---

# ⚙️ settings.py

```python
REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend'
    ]
}
```

---

# 🔍 Step 2: Filtering

👉 views.py

```python
from django_filters.rest_framework import DjangoFilterBackend

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer

    filter_backends = [DjangoFilterBackend]
    filterset_fields = ['title']
```

---

## 🧪 Test

👉 `/courses/?title=python`

✔ শুধু python course আসবে

---

# 🔎 Step 3: Search

👉 add করো:

```python
from rest_framework.filters import SearchFilter

class CourseViewSet(ModelViewSet):
    ...
    filter_backends = [DjangoFilterBackend, SearchFilter]
    search_fields = ['title', 'description']
```

---

## 🧪 Test

👉 `/courses/?search=django`

✔ title বা description এ django থাকলে আসবে

---

# 📄 Step 4: Pagination

👉 settings.py

```python
REST_FRAMEWORK = {
    ...
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 5
}
```

---

## 🧪 Response

```json
{
  "count": 20,
  "next": "http://127.0.0.1:8000/courses/?page=2",
  "previous": null,
  "results": [
    { "id": 1, "title": "Python" }
  ]
}
```

---

# 🔥 Step 5: Custom Pagination (Pro)

👉 pagination.py

```python
from rest_framework.pagination import PageNumberPagination

class CustomPagination(PageNumberPagination):
    page_size = 3
    page_size_query_param = 'page_size'
```

---

👉 views.py

```python
from .pagination import CustomPagination

class CourseViewSet(ModelViewSet):
    ...
    pagination_class = CustomPagination
```

---

## 🧪 Test

👉 `/courses/?page_size=2`

✔ user control করতে পারবে কত data নিবে

---

# 💥 Step 6: Ordering (Bonus)

```python
from rest_framework.filters import OrderingFilter

filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
ordering_fields = ['id', 'title']
```

👉 `/courses/?ordering=-id`

✔ latest first

---

# 🎯 DAY 6 CHECKLIST

✔ Filtering
✔ Search
✔ Pagination
✔ Ordering

---

# 💥 Real Impact

👉 তোমার API এখন:
✔ fast
✔ scalable
✔ user-friendly

---

# ⚠️ Common Mistake

❌ pagination না দেওয়া
❌ সব data একবারে পাঠানো

---

# 🧠 Expert Tip

👉 বড় project এ:

* filtering must
* pagination must
* search must

---

# 🚀 Tomorrow (Day 7)

👉 File Upload (Image/Video)
👉 Media handling
👉 Real SaaS feature

---

# ⚡ Now YOUR TASK

👉 Course API তে add করো:

* search
* pagination
* filter

---

তারপর বলো:
**“Day 7”**

আমি তোমাকে file upload + media system বানাতে দিবো 🔥🚀

--------
চল 🔥 — **Day 7 = File Upload (Image/Video) + Media System (Real SaaS Feature 💀)**

আজ তুমি এমন feature বানাবে যেটা প্রায় সব real project-এ লাগে 😎
👉 Profile image, course thumbnail, CCTV video upload — সব এখান থেকে

---

# 🚀 DAY 7 GOAL

👉 তুমি আজ শিখবা:

* Image upload
* File upload (video/pdf)
* Media handling
* API দিয়ে file serve করা

---

# 🧱 Step 1: Model এ File Field add

👉 Example: Course model

```python
class Course(models.Model):
    title = models.CharField(max_length=100)
    description = models.TextField()

    # 🔥 new fields
    thumbnail = models.ImageField(upload_to='courses/', blank=True, null=True)
    video = models.FileField(upload_to='videos/', blank=True, null=True)
```

---

# ⚙️ Step 2: settings.py (MEDIA config)

```python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

👉 import os লাগবে:

```python
import os
```

---

# 🔗 Step 3: URL config (VERY IMPORTANT)

👉 config/urls.py

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    ...
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

# 🔌 Step 4: Serializer

👉 DRF automatically handle করবে

```python
class CourseSerializer(serializers.ModelSerializer):
    class Meta:
        model = Course
        fields = '__all__'
```

✔ আলাদা কিছু লাগবে না

---

# 🧪 Step 5: Postman / Frontend Test

👉 Request type: **POST**
👉 Body type: **form-data**

| Key         | Type | Value         |
| ----------- | ---- | ------------- |
| title       | text | Python Course |
| description | text | Learn Django  |
| thumbnail   | file | image.jpg     |
| video       | file | video.mp4     |

---

# 💥 Response Example

```json
{
  "id": 1,
  "title": "Python Course",
  "thumbnail": "/media/courses/image.jpg",
  "video": "/media/videos/video.mp4"
}
```

---

# 🖼️ কীভাবে কাজ করে (Flow)

![Image](https://images.openai.com/static-rsc-4/a7BEg5LmMoM8OthiXt7xwpfQce8HCzzwYW7SvobiIR7LeDbLpURx7MbfGecDBCePx1N7K5dZJexsz29aXIpT0KB-s2W3YMiFh42sun6NWpvWUH09KbsQo6VjiCBinlDNKHhdNWwhPCOAVmU1Bh3T3A26QcCJ1CcTTdvo1zy5H4MOFmQlByOobO297kypWJPj?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/nLoSGmS9hH3NXDFPqkSlfbhJ74nml6Oyxs306B6Gl7PWiRiN6JivQp_GFprYQgBPsJqDb-Au7aUcCiDvGtbbmLy9DDAUE1jN_6TjfGzUNQ7s55eg70t_nKDj1tqzrp6HjJbfAg63kmu17A2lRwplUUebaxlT6_GcMT16N8CNG725SobqIimQAqy6zpytjgq-?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NqLRJy8U2BJeK17baMjJbxxlIM0gTnBA6VBKIpRa3MvJMQEsUKu515312q76mzW8dygctMDZavANQsh7pCkC6oMVMGIwA7KupmtJpU8-QqczpnEg9HG86seSjnOuVne74IlyTWVOmRcV21nAlYk4LfQyQxNBT5Ra1IGeBJ6BZ__QAknyLe06_dhI0NnYZev1?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/lwdwzhsykElM8V8Bn4R2AgRpb-UDcxEpzSBWjcM4HofdyVRQJmGQcVIp18JoAEGhd2U2-0H-6ida4qe_OTwYY0gSXi-q9q4MYhrZloftjTD6ifWn0Hi52eI40a3u-0W54AOAfR5L2y9xJ4F50uE0G6iikD40pB5b0xVHVXq3DilP8NnJqA3KCoYfVX3CES9g?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/kJJe8iTg4MamOj8KmCFCowur3Vxg-HAn8iTqde_tC6Bm74HBWL4R0saT3ilb3o5JTpwZvDgiZPgIETrEaM6PxS9Bq2rLUBg-fJDFFxFG8O8CznX3RxJhax4Hh-5a0TkbDh6AKG9yRsDwRnVWmfQG-Da8dB4Jd1owIkMHJlVhUHL9seJ8RddRTF9LK5DfHNQy?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/OTdyLPLI3YTs5QCvqhPmGwjn01A0NZVW1Gf085SG4VGfxAKZi7uds0nXGwqs0lPI3iaetlhMdflc9u7WW6beaD2SPm2Tb6pvTTGUdVi8eE9a43JW660vZVO9oI0kNyxMLmaB3cjg9EjlXTi_OlNOQaOaP_l5VUzXv4XVsZQm4OnDpHRFnhPw1gN4yT_74zSr?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/8vl_NTCjDjZw0NMf34jafMLNCvYl0w2N5-Bc10oWPHOMB2vGgEeb5IYAmJNxcZOSCbgTdgaOiyxO3cq1gqnSO0_V3jDUWkGRSdUrprPNntrWQkkNF9s7kGnT122FMUzIub88kuLjw5iKIsPh2V3FCX_jiSLoizQu5PZqyZ-EqTQ_e4bDq5h5QxOY0d_bXPAB?purpose=fullsize)

👉 Flow:

1. User file upload করে
2. Django save করে `media/` folder-এ
3. URL generate হয়
4. Frontend access করে

---

# 🔥 Step 6: Access File

👉 Browser এ:

```
http://127.0.0.1:8000/media/courses/image.jpg
```

✔ image show হবে

---

# ⚠️ Common Problems

❌ image upload হচ্ছে না
👉 কারণ: `MEDIA_URL` / `urls.py` miss

❌ file null আসছে
👉 কারণ: JSON না, form-data use করতে হবে

---

# 🔥 Step 7: Profile Image (Real Use Case)

👉 User model এ add করতে পারো:

```python
profile_image = models.ImageField(upload_to='profiles/', blank=True, null=True)
```

---

# 💥 Bonus (Expert)

👉 file size validation:

```python
def validate_thumbnail(self, value):
    if value.size > 2 * 1024 * 1024:
        raise serializers.ValidationError("Max 2MB allowed")
    return value
```

---

# 🎯 DAY 7 CHECKLIST

✔ Image upload
✔ Video upload
✔ Media config
✔ API test

---

# 💥 Real Impact

👉 এখন তুমি পারো:

* profile image system
* video course upload
* AI CCTV footage upload

---

# 🚀 Tomorrow (Day 8)

👉 Authentication advanced (Refresh token, logout)
👉 Secure system
👉 Production-level auth

---

# ⚡ Now YOUR TASK

👉 Course model এ thumbnail add করো
👉 API দিয়ে image upload করো

---

তারপর বলো:
**“Day 8”**

আমি তোমাকে authentication pro level এ নিয়ে যাবো 🔥🚀

--------
চল 🔥 — **Day 8 = Authentication Advanced (JWT Pro Level 💀)**

আজ তুমি **secure login system** বানাবে যেটা real SaaS-এ use হয় 😎

---

# 🚀 DAY 8 GOAL

👉 তুমি আজ শিখবা:

* JWT login
* Access + Refresh token
* Token refresh
* Logout system
* Secure API

---

# 🧠 JWT Flow (Important)

![Image](https://images.openai.com/static-rsc-4/rBzQvTNMPmHqfmomsx1Cp5HNHtYOqwGfLq2VERF7rSYhKXIPfcfnTir9cTlfSCjVaqd3bJ2p8tsGM3L4oFXf4Hp2KK3dPrMBM2nFPp7IEQoxcuDvyFmCEpodWamQwFnUlZ-0nck8J5fLNv78OrIYmH5jn2ht2A4J4WbKiCNNVFgKkveqnlA-qxY6v1vfDG2H?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/DZnBgOa5DgQzFFHu0caa3pcm7oVizOIabNaAlBYDNNfch1WD4l9egMFVrMlnqLYGejXMucYMpphqDSZS8CzFplz-xmk5HONSfQt22wZCNkidQxJXaG0jrgP6ysHBshcb-x1ZyIwK-yQ6-rkF3X97srS7CjSYTS_zJ7U-uC7qSuyZCOXJ_2ozVOySpR-ZwMdR?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/FEeki1wUEdJwdZarzSZtG0xzzS5fSheoUINmh2mTs7Rr4L8g-9BjGjth2wkXRMDDzk8c5tfUpXCgcysiJ4xQmmBa7W7DRH1o7b5xDw7w_MRjYDkbf3CNBXqAK4dlyxniLXYsiIamsk-AIsvtuVGqD6dU-NzDnCqMoJNTPxWi9ZIYp43yna6VUoYo10-L8Fn6?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/hCuVxJOVwl9s6cWL3NCf1feufbiWtbFr0zF00KaC2b6bV6jSEOM1qL4JAJf_0Jr1ifHvKJE5B7bSYeFXsTdpbjFgH2iE5sZYTRbVfl5P-FGwjKSdKRtaMzM7yGkhGq8QkkfVDIWwLfatCTbNPlzve7qdNkStWXXxKJ0aHCV0idb3qNAjCpLty3IGSGXcvSVc?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/cdzapyOvlYO0mp7OM45jPWMvas_V8mAV_dNO89sIuBiWlOs-9WSek43aAvNJLjCf_XdC2GXykUvQEKL4vf5i83EtZ8XxC0XIKNj_pPFybSK1yLbEvE7jdMszc7NaXOIobyeOHm5h3pjFpC70tM9dp4bv42kJw9E7Z4jEy_-W4hUynHkxo90r7NXNi-21g8XR?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/isAygogz3hqT4s79R8KjLRSXkYXt2ZBZxuQw0TjHBTW712196O50Y7Tz7V8nBH-chAv01gTss5-pYMg3zTcevIGWZ2Ar0BPPZ2p5TDJg0cXy8Zw1MXwfGMMJJjfC4u2X8vUKIryXqD_qKPZCdHQZsIH69kZVF89Gh-wXvJ6JUPdT_zzxtCSZEZ-RdsPT5UOB?purpose=fullsize)

👉 Flow:

1. User login → Access + Refresh token পায়
2. Access token দিয়ে API call
3. Expire হলে → refresh token দিয়ে নতুন access নেয়

---

# 🔥 Step 1: Install JWT

```bash
pip install djangorestframework-simplejwt
```

---

# ⚙️ settings.py

```python
from datetime import timedelta

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    ),
}
```

---

## 🔑 JWT Config

```python
SIMPLE_JWT = {
    'ACCESS_TOKEN_LIFETIME': timedelta(minutes=15),
    'REFRESH_TOKEN_LIFETIME': timedelta(days=1),
}
```

---

# 🔌 Step 2: URLs

👉 urls.py

```python
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

# 🧪 Step 3: Login Test

👉 POST `/login/`

```json
{
  "email": "admin@gmail.com",
  "password": "123456"
}
```

---

## 💥 Response

```json
{
  "access": "eyJhbGciOiJIUzI1NiIs...",
  "refresh": "eyJhbGciOiJIUzI1NiIs..."
}
```

---

# 🔐 Step 4: Protected API

👉 views.py

```python
from rest_framework.permissions import IsAuthenticated

class CourseViewSet(ModelViewSet):
    ...
    permission_classes = [IsAuthenticated]
```

---

## 🧪 Test

👉 Header:

```
Authorization: Bearer <access_token>
```

✔ না দিলে → 401 Unauthorized

---

# 🔁 Step 5: Refresh Token

👉 POST `/refresh/`

```json
{
  "refresh": "your_refresh_token"
}
```

✔ নতুন access token পাবে

---

# 🔥 Step 6: Logout (Important)

👉 JWT default এ logout নাই ❌
👉 manually handle করতে হয় ✔

---

## 🧠 Solution: Blacklist Token

👉 install:

```bash
pip install djangorestframework-simplejwt[blacklist]
```

---

👉 settings.py

```python
INSTALLED_APPS = [
    ...
    'rest_framework_simplejwt.token_blacklist',
]
```

👉 migrate:

```bash
python manage.py migrate
```

---

## 🔌 Logout API

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from rest_framework_simplejwt.tokens import RefreshToken

class LogoutView(APIView):
    def post(self, request):
        try:
            refresh_token = request.data["refresh"]
            token = RefreshToken(refresh_token)
            token.blacklist()

            return Response({"message": "Logged out"}, status=200)
        except Exception:
            return Response({"error": "Invalid token"}, status=400)
```

---

# 🎯 DAY 8 CHECKLIST

✔ JWT login
✔ Access token use
✔ Refresh token
✔ Logout system

---

# ⚠️ Common Mistake

❌ access token DB তে save করা
❌ refresh token ignore করা

---

# 🧠 Expert Tips

👉 Production এ:

* Access = short time
* Refresh = long time

👉 Always use:

```
Authorization: Bearer <token>
```

---

# 💥 Real Impact

👉 এখন তুমি বানাতে পারো:

* Secure SaaS backend
* Multi-user system
* Role-based system

---

# 🚀 Tomorrow (Day 9)

👉 Permissions (Admin / User control 🔥)
👉 Custom permission
👉 Role-based API

---

# ⚡ YOUR TASK

👉 Login API test করো
👉 Protected API call করো
👉 Logout implement করো

---

তারপর বলো:
**“Day 9”**

🔥 Next level শুরু হবে (Role system 💀) 🚀

-----
চল 🔥 — **Day 9 = Permissions + Role-Based Access (Admin / User Control 💀)**

আজ তুমি এমন system বানাবে যেটা **real SaaS-এর core** 😎
👉 কে কি করতে পারবে — পুরো control তোমার হাতে

---

# 🚀 DAY 9 GOAL

👉 তুমি আজ শিখবা:

* Permission system (DRF built-in)
* Custom permission
* Role-based access (admin / user)
* Secure API control

---

# 🧠 Problem

👉 এখন:

* সবাই সব API access করতে পারছে ❌
* user course delete করতে পারছে ❌

👉 এটা dangerous ⚠️

---

# 🔥 Step 1: Built-in Permissions

👉 DRF already দেয়:

```python id="d0sx1m"
from rest_framework.permissions import IsAuthenticated, IsAdminUser
```

---

## 🧪 Example

```python id="qv0r5m"
class CourseViewSet(ModelViewSet):
    ...
    permission_classes = [IsAuthenticated]
```

✔ শুধু login user access করতে পারবে

---

## 🔐 Admin Only

```python id="r1m9z2"
permission_classes = [IsAdminUser]
```

✔ শুধু admin (is_staff=True)

---

# ⚠️ Problem

👉 তুমি already `role` field use করতেছো
👉 `IsAdminUser` = Django admin (is_staff)
👉 তোমার custom role = আলাদা ❗

---

# 🔥 Step 2: Custom Permission (🔥 IMPORTANT)

👉 permissions.py

```python id="a3y7kl"
from rest_framework.permissions import BasePermission

class IsAdminRole(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'admin'
```

---

## 🧪 Use it

```python id="xj9m8t"
from .permissions import IsAdminRole

class CourseViewSet(ModelViewSet):
    ...
    permission_classes = [IsAdminRole]
```

✔ শুধু role=admin access পাবে

---

# 🔥 Step 3: Mixed Permission (Real Use Case)

👉 Read = সবাই
👉 Write = admin

```python id="8c4nvs"
class IsAdminOrReadOnly(BasePermission):
    def has_permission(self, request, view):
        if request.method in ['GET']:
            return True
        return request.user.role == 'admin'
```

---

## 🧪 Use

```python id="clxq2w"
permission_classes = [IsAdminOrReadOnly]
```

✔ GET → everyone
✔ POST/PUT/DELETE → admin only

---

# 🔥 Step 4: Object Level Permission

👉 Example: user only own data edit করতে পারবে

```python id="h2m7qp"
class IsOwner(BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

---

## 🧪 Use

```python id="v1p9te"
permission_classes = [IsAuthenticated, IsOwner]
```

---

# 💥 Step 5: Role Field Best Practice

👉 তোমার User model:

```python id="y8l0dz"
ROLE_CHOICES = (
    ('admin', 'Admin'),
    ('user', 'User'),
)

role = models.CharField(max_length=10, choices=ROLE_CHOICES, default='user')
```

✔ typo avoid হবে
✔ secure হবে

---

# ⚠️ VERY IMPORTANT (🔥)

👉 user যেন নিজে admin না হতে পারে ❗

## ❌ Wrong

```json id="9dbb8t"
{
  "email": "user@gmail.com",
  "role": "admin"
}
```

---

## ✅ Fix (Serializer)

```python id="0lyz0w"
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'email', 'role']
        extra_kwargs = {
            'role': {'read_only': True}
        }
```

✔ user role change করতে পারবে না

---

# 🎯 DAY 9 CHECKLIST

✔ Custom permission
✔ Role-based access
✔ Admin vs user control
✔ Secure API

---

# 💥 Real Impact

👉 এখন তুমি বানাতে পারো:

* Admin dashboard
* Instructor system
* Multi-role SaaS

---

# 🧠 Expert Tip

👉 Production এ:

* Role + Permission combine করো
* Never trust frontend ❗

---

# 🚀 Tomorrow (Day 10)

👉 Signals (Auto action 🔥)
👉 Auto profile create
👉 Email trigger

---

# ⚡ YOUR TASK

👉 Course API তে apply করো:

* GET → public
* POST → admin only

👉 User role secure করো

---

তারপর বলো:
**“Day 10”**

🔥 তুমি এখন mid → advanced level এ চলে গেছো 🚀

----
চল 🔥 — **Day 10 = Django Signals (Auto কাজ 🔁 Real Automation 💀)**

আজ তুমি এমন system বানাবে যেটা automatically কাজ করে 😎
👉 user create হলে profile auto তৈরি
👉 email auto send
👉 log system

---

# 🚀 DAY 10 GOAL

👉 তুমি আজ শিখবা:

* Django signals কী
* post_save ব্যবহার
* auto profile create
* clean architecture

---

# 🧠 Signal কী?

👉 Signal = **event trigger system**

✔ যখন কিছু ঘটে → auto function run হয়

---

# 🔄 Example Flow

![Image](https://images.openai.com/static-rsc-4/QXUAAbiohaYlimYRGxy2AfODmMjMPoMbnHkeD9duYu0FEmXUkfjI0PiK27rhGLCQxeJmO9HfPoARt0fM-ARgPuhxqpmYwNBMKHLxkHtEAibRqRnxwXGeuhKW49OqKsV_Y_tCmJdP4a5zx3xDQD_tExMHO4Ib3kO1FFToIEpIT3uL8Y4a4SwodedYgzKcFQtO?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/9saK9wQ3_Rw_RtZHB52zFqnE55p9jDCgCZ-31lQxwulACGdfxDAeu81F4vYvBYj3AEHMPo4h0u3eVZZOFs0mCUn8jx3q6_rQv0s1MFect5QOi74cVqkA9oU4txToSgILKViC2OxzPdCeL6cvmLUIW_DH08RalRtrt02jJcgeK32DvkgOZ83Ql-UhxNz_0mxb?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/udSBqG0_fkYdlKUV3kd0t8pJmIadufBQ_Md-2LhKEEbTCUMRfepVhpKWvI5E8a9p00lEvP6BZZLBfcfnTr1r_naGC3jwaufRfWrdNXuvmWAuZCaXe2094SiORO0DXxJDbCH2ixvNkGIQ1vDkpKAomRU6mvr8r2Ksg6sms-4Q2LX6YOsu4rrgIL3greY7mdnW?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/X7LrN2oY59zNdpTvNjhBdOJ98BtrSon4O9UOeuh8w2lQJn8hVutIHdM9OPunYGQ8pW8u1GU301h-43fv_6l5ER7xmOe9Ke_s722VFR3EQjv2zoDrrpwBveSdunlMEAKVkh2NcQTSwNCeBy3KcTraG_uAkZpE6q34373ZNFTYPB2x2_xCMiwWLnmriSyf0bZs?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/A2HaVL7yNf0opsxL4YQlDmP5GbahxTys-Q_AaE5cAPRY1boXWsaugAW8MlZIyFcWDEPY0Bl5Fm74zjh6ePsyN6P6vQsUbgpbhDxxxyZK_mCZhwFx84yEvFJ2-nZaP959UudfdO5ebaPkELHKHoZG9JNk5F_OZflH3Xl7Wiu4PWB-mWLd_bE9HXKmoZNk10t4?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/PYXYJx6_MqEua6QnQtXP5j_Os78M5Bl5E3f_wx5HcoAfyybsOzAon2784uhQMQPTR4mQqFQXapdEHI-yTgzHsq0mhnuExYqXlcHu1gQ0Q-PMnVs3Ac1nB9GUrQXQxzB8DZXeJEbqe2EJ1gr70CLvVlS_Y9-g6Ef2f3poDlyk1I4ckL83ozyijIGtYWugHny-?purpose=fullsize)

👉 Flow:

1. User create
2. Signal detect করে
3. Profile auto create

---

# 🔥 Step 1: Profile Model

```python id="h7x2az"
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.TextField(blank=True)
```

---

# 🔥 Step 2: Signal create

👉 signals.py

```python id="y2lm5v"
from django.db.models.signals import post_save
from django.dispatch import receiver
from .models import User, Profile

@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)
```

---

# ⚠️ Step 3: Connect Signal (IMPORTANT)

👉 apps.py

```python id="l8m2xe"
class YourAppConfig(AppConfig):
    name = 'yourapp'

    def ready(self):
        import yourapp.signals
```

✔ না করলে signal কাজ করবে না ❌

---

# 🧪 Test

👉 নতুন user create করো

✔ automatically profile create হবে

---

# 🔥 Step 4: Update Signal (Advanced)

👉 user save হলে profile update:

```python id="a3fdv7"
@receiver(post_save, sender=User)
def save_profile(sender, instance, **kwargs):
    instance.profile.save()
```

---

# 💥 Step 5: Real Use Cases

👉 তুমি use করতে পারো:

✔ User signup → welcome email
✔ Order create → notification
✔ AI CCTV → suspicious alert trigger

---

# ⚠️ Common Mistakes

❌ signal connect না করা
❌ heavy logic signal এ লেখা

---

# 🧠 Best Practice

👉 Signal = **light task only**

❌ ML model run ❌
❌ heavy processing ❌

👉 heavy হলে:
👉 Celery use করো (Day 11 😉)

---

# 🎯 DAY 10 CHECKLIST

✔ Signal create
✔ Auto profile create
✔ apps.py connect
✔ test

---

# 💥 Real Impact

👉 এখন তুমি পারো:

* automation system
* background trigger
* scalable architecture

---

# 🚀 Tomorrow (Day 11)

👉 Celery + Redis 🔥
👉 Background task
👉 Async system (real SaaS 💀)

---

# ⚡ YOUR TASK

👉 User create করলে auto profile create করো
👉 Test করো

---

তারপর বলো:
**“Day 11”**

🔥 তুমি এখন advanced backend engineer হওয়ার পথে 🚀

--------
চল 🔥 — **Day 11 = Celery + Redis (Background Task 💀 Async Power)**

আজ তুমি এমন জিনিস শিখবা যেটা **real SaaS backend-এর backbone** 😎
👉 heavy কাজ background-এ যাবে (API fast থাকবে ⚡)

---

# 🚀 DAY 11 GOAL

👉 তুমি আজ শিখবা:

* Celery কী
* Redis setup
* Background task run
* Django + Celery integration

---

# 🧠 Problem

👉 এখন যদি:

* email send
* video process
* AI detection

👉 সব API এর ভিতরে করো → ❌ slow / hang

---

# 🔄 Solution = Celery

![Image](https://images.openai.com/static-rsc-4/6LQYP3P0ZY6pvXwLOTpxbaAGKNtDTU0pXr5dthHxY9fT-1Pdian4sXHanvrabfx7yOLv1bV_7AwP2AyqYS3OqbGIzjFSPL5AF9qYIjOQkB3QJErwK5oXkftiS_dDTHttn11z4GS51GtV8MuRN6Kczqfnw2ReCyIuEMEpi1aqO9LqeCFIWBhL4CU6AAgA4oGj?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/szb-7pFFmVtRlB2mwlOZSK_EvJflJEc9R3BKTuqT-sS2VriZK-fYgVpGdhmInGtoT4AIM11XDn2bxVZXYCVfuAedAqIgIDx55m_r9_WgyZU-GgtB7C_HogSPk42NH7wBuYYO3v8TVp9x3SbcCsHb8jjcl877dFElBwhBcvfyH-_M-yaoKUn56MsOKv3LdtM_?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/BasAQmRiory4ZlJEKMSKiKh4pyKX75anYlv_ICPUNMKZjvPvl2qh5WbBTvwPLb801KowLa9TiVRA0z3vENbVrLC2ZGg8idVVwm5nmcICTZowA0rzsCiI88ZVXrpqdR8a0AkkkLFD5HhC2cJP1d1gkSwMGCJGGlz9GdaDx3CsC-xaOWLuxcQi6kKXoKGEstlq?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/BRRrdkwkDfbgPXRv4KY5G6Dy_v-t_rTFwwr7mToeCE2jho3VX_GRa1hpLnifEhw2qP-ISQq1pvdiJWrzVvPDASClceVejVrPSkqRpFNwVOOBQ8OSmhGE0PdsF_F2P8Fefz6pEO9QJcqUHhF4dXW1nbuc3HRxP8YsnnzXhxI9xX0rqqTEvnP7my1NhPX8160N?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/SEfaLdAvrjh64eYKn6bNWUTzhZaA2f0esrbOQKLUHLPfkY3puR2N0xZeN12xhIL99D_WmUrX3TUSOo6RNBwRUzpb4l0lwIwAsemTd6T0S1NMChQA3XDsKlMYmDJtqlZdelI9aclJtpmPGw-3Wg2L9SiOy3WigkmUjQd8Hj1RgKN60-oacL9I3coRfCILjvNB?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/OBp4XpFRAU6jfrWH6kj2nrrmE5i5NiRZESxz-yWwIpr8xPEhiy1E9IowKkcIHCwfTEBIb520OqJzqf_mdtcEtEeG-TBI001zz8KY5s3YUKMXLX5Gk-9tuXtsCWawPobEANcqG_jdcY0p1LJ37HjEyxn4__kiXwOidZPviKVJgddtGbX8WKaByW0Av4K4kxmN?purpose=fullsize)

👉 Flow:

1. User request করে
2. Django → task queue (Redis)
3. Worker → background এ run করে

---

# 🔥 Step 1: Install

```bash id="zrmq6g"
pip install celery redis
```

---

# ⚙️ Step 2: celery.py create

👉 project root (same level as settings.py)

```python id="g9pj4d"
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')

app = Celery('config')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

---

# 🔌 Step 3: **init**.py

```python id="ijb6nv"
from .celery import app as celery_app

__all__ = ('celery_app',)
```

---

# ⚙️ Step 4: settings.py

```python id="6m1t0f"
CELERY_BROKER_URL = 'redis://127.0.0.1:6379/0'
CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
```

---

# 🔥 Step 5: Task create

👉 app/tasks.py

```python id="p3rq1c"
from celery import shared_task

@shared_task
def send_email_task(email):
    print(f"Sending email to {email}")
```

---

# 🔥 Step 6: Use Task

👉 views.py

```python id="cf6s0v"
from .tasks import send_email_task

class RegisterView(APIView):
    def post(self, request):
        email = request.data.get('email')

        # 🔥 async call
        send_email_task.delay(email)

        return Response({"message": "User created"})
```

✔ API fast থাকবে
✔ task background এ যাবে

---

# 🧪 Step 7: Run System

👉 Redis start করো:

```bash id="9y4o2o"
redis-server
```

---

👉 Celery worker run:

```bash id="v9r9kq"
celery -A config worker -l info
```

---

👉 Django run:

```bash id="7k2zff"
python manage.py runserver
```

---

# 💥 Output

👉 terminal এ দেখবা:

```id="b6b0fa"
Sending email to test@gmail.com
```

---

# 🔥 Step 8: Real Use Case (🔥)

👉 তুমি use করতে পারো:

✔ Email sending
✔ AI CCTV detection processing
✔ Video processing
✔ Notification system

---

# ⚠️ Common Mistakes

❌ Redis run না করা
❌ `.delay()` না দিয়ে direct call

---

# 🧠 Expert Tips

👉 Production এ:

* Celery + Redis MUST
* heavy task always async

👉 Signal + Celery combo 🔥
👉 (Signal trigger → Celery task run)

---

# 🎯 DAY 11 CHECKLIST

✔ Celery setup
✔ Redis connect
✔ Task create
✔ Async call

---

# 💥 Real Impact

👉 এখন তুমি বানাতে পারো:

* scalable SaaS
* async system
* high-performance backend

---

# 🚀 Tomorrow (Day 12)

👉 Caching (Redis caching 🔥 speed boost)
👉 API fast ×10
👉 performance tuning

---

# ⚡ YOUR TASK

👉 simple task বানাও
👉 API call করলে background এ run হচ্ছে কিনা check করো

---

তারপর বলো:
**“Day 12”**

🔥 তুমি এখন backend beast হওয়ার পথে 🚀

---
চল 🔥 — **Day 12 = Caching (Redis Cache ⚡ API Speed x10)**

আজ তুমি এমন technique শিখবা যেটা দিয়ে **slow API → lightning fast ⚡** করে ফেলতে পারবা 😎

---

# 🚀 DAY 12 GOAL

👉 তুমি আজ শিখবা:

* Caching কী
* Django cache setup
* Redis cache use
* DRF API cache করা

---

# 🧠 Problem

👉 ধরো:

* `/courses/` এ 1000 data
* প্রতি request এ DB query হচ্ছে ❌

👉 Result:

* slow API ❌
* server load ❌

---

# 🔄 Solution = Cache

![Image](https://images.openai.com/static-rsc-4/ykzH0a8dHFqH2YzMtUhNn5SVq6mwqfsQhIhl-ObU1cr2okDtScRlRHpZVBIdEJigqIwcYEV83ntvdp9XEwky_Clg6QBSo6sISV53Bi1TLrtujKZnf3mtB2h5laQoU1OggHmsPY3XtN8zUUtDtWdsX5tQmMNAaMlZDKDWQZQf96MyYPIqxa1-fw7ilwaolIS6?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/ikc_w0p2Ac9yDua4gpj_7sg0e3a80aovFd7HviAUFgSbJexyPgmHj-bQYsJ99rODuwqVca34uHBuiVjc6BEhkv3ZQQEYW8YO61zuSy5SRIxcblMVhGFMpUbAGE6tVEHz6oZBEHHYecv7uusJdVp87qzcKWYd-6mxVBWkCzd_C2PtcJOMBQfWtfUZw1jpKGcq?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/WQR15mQyQzLO7H-MkUw4DJJFA8VW2iECEGqAcqxfuaJmCP9XJ1v3YtXaP2GQS1Uv75c140EfduJwfYZtQqgLw2M8WUdfh5fmYAoCo9RDxPnVS6vKVfxLrzZBBkWVzXRgBzoMdblDxc0G6keGZCyDDJW0XBpa9LxK-zITjQKoh1iLSRDxceBTNmvF-tDN7c7Q?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/hyFOtZvmZggs-fUArZxwog9368wi2KVZ_n3fvbDlajXkrN5eR1i3nDmZJtaAYX-pa3-7KASaN-1PKALslYthO6AP36bkmmWV7VFww0Gfsjxnf8vdnBAxbUVG4YlUSP5iznCRNoxPIvmo81c5np3He48qsHjY3xJQYT7Jy7DlSfyiWWElQKjqWd13e6UguUh2?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/OsTyYmFtcLCwXw1cJQfUeZhfHvP3zL55IchNhEKUAlVZuYVF6aliMFjv-Nidp5ZTyLSAEpmlDuhWTw0m0r9NqQIAjWjgE2id8eL1b-e28bZ9DGSeSpT_4ww-kW_bJnTd_wKUMthGhH81PIt8DQx_AxBXIM0DhtblilTC8ixaBhwRLOc57-08EfW6YlCUznLN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tiUsieNS7nqlM-uAfxbWRUZpYZ94v_SXc9YIvis_2POp5ZE2IxsusO40xVDQ_Bm_G1tvpExQc7LAZJqaskWFNzBCjnmVp-MFJocasUXycxAwck5J4j8cORw9YcaXJdBE6cKIDHuPPfQ7TpqlATTLDx4b1b299rnM0j0S1oMUG1t8_aDWVhKBiq9GhgwxzIgv?purpose=fullsize)

👉 Flow:

1. First request → DB hit
2. Data cache এ save
3. Next request → cache থেকে fast response ⚡

---

# 🔥 Step 1: Install Redis Cache

```bash id="o1d4cd"
pip install django-redis
```

---

# ⚙️ Step 2: settings.py

```python id="v9eqje"
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```

---

# 🔥 Step 3: Simple Cache Use

👉 views.py

```python id="m0tqyk"
from django.core.cache import cache
from rest_framework.response import Response

class CourseList(APIView):
    def get(self, request):
        data = cache.get('course_list')

        if not data:
            courses = Course.objects.all()
            data = CourseSerializer(courses, many=True).data

            cache.set('course_list', data, timeout=60)  # 60 sec

        return Response(data)
```

---

# 🧪 Test

👉 First request → slow
👉 Second request → ⚡ fast

---

# 🔥 Step 4: Decorator Cache (Easy Way)

```python id="3m6lqk"
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator

class CourseViewSet(ModelViewSet):

    @method_decorator(cache_page(60))
    def list(self, request, *args, **kwargs):
        return super().list(request, *args, **kwargs)
```

---

✔ 60 sec cache

---

# 🔥 Step 5: Cache Clear (Important)

👉 new course add করলে cache clear করতে হবে ❗

```python id="rs0d7k"
cache.delete('course_list')
```

---

# 💥 Step 6: Where to Use

👉 use করো:

✔ list API
✔ dashboard data
✔ heavy query

---

❌ use করো না:

❌ login
❌ sensitive data

---

# ⚠️ Common Mistakes

❌ cache clear না করা
❌ user-specific data cache করা

---

# 🧠 Expert Tips

👉 Production এ:

* Redis cache MUST
* API response cache করো

👉 Cache + Pagination = 🔥🔥

---

# 🎯 DAY 12 CHECKLIST

✔ Redis cache setup
✔ API cache
✔ decorator use
✔ cache clear

---

# 💥 Real Impact

👉 এখন:

* API fast ⚡
* DB load কম
* scalable system

---

# 🚀 Tomorrow (Day 13)

👉 Throttling (Rate limit 🔥 security)
👉 API abuse protection
👉 Hacker control 😈

---

# ⚡ YOUR TASK

👉 `/courses/` API cache করো
👉 response time compare করো

---

তারপর বলো:
**“Day 13”**

🔥 তুমি এখন performance engineer level এ যাচ্ছো 🚀

--------
চল 🔥 — **Day 13 = Throttling (Rate Limit + API Protection 💀)**

আজ তুমি তোমার API কে **abuse / spam / hacker attack থেকে protect** করতে শিখবা 😎

---

# 🚀 DAY 13 GOAL

👉 তুমি আজ শিখবা:

* Throttling কী
* DRF built-in throttle
* Custom rate limit
* User vs Anonymous control

---

# 🧠 Problem

👉 যদি throttle না দাও:

* কেউ 1 sec এ 1000 request দিবে ❌
* server crash 😵
* brute-force login attack ❌

---

# 🔄 Solution = Throttling

![Image](https://images.openai.com/static-rsc-4/TbFWWaz9YeZ68cUlyc5NNnvUc7eXoxoFdE_UavwOi216w665eDpdBNg2vop1E_Oq7XF0W74XUm25Av0W3UZ6MwMSPtAsT4kNTN7bnqV_Ad5ziHLvJQ9WR-zaBbw4G9PHJ1BUNDBr9KvkhOLoGahxlLxqg39q7zujUMlq6aDLscAhVyloIPcz95XEqv1wrkUQ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/e_PYFcF45ZOyzPB2XwRVuIUuIhIyuVZg0di80whvbF9N8H8mDQDDvY582Koe946JgB-k3AWSi1S7PajLcM7ItCyYP8sc_Sy3JYt26XrNYJd1l-ClJatfIUA2MPg1QF7LUD3_4JQkWvwU5F2Nm7yeO5CAwGfbpVf0B03-rjDPSobx89pQaW94eQ6b9Lgqwlro?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/k7VXu2WjYV5q16yFB1erOrieo4xV4nPs5NuUTdQHCjUzNyZompBGFjtW7zZh7T2ndeBE-Y-DsPzJHML_Pu9DlyC_6zE700zqA8VSR_dNHaMoehC-P-AhURdNfEpzt0r4HFRVRT2rG4mft5cYVYSSoH7rG6NIdpsW3NGJZZOyVZq_LRcIh-PPOrmkQYboEHMU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/vv4eZ4Zh7zf3ga2umVYXgUNenJVX5I5raEntxsn_t7-8PvGzuRSalOErBy4SnVZujEfrJE45S5cU9miYs10N5CXs9pllP6CQAjTrVY7ZjbnM5L49nAwUfa-4cJBhbEeILkJFkSDqBBg0HMJZM6Ylkj5YPFpEYooB07g47JGfotT2zl3SeWIrgmd42w3NTyTH?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/xu1Y_csrW4eaw4XpbLIakiJhunpxotagReLROpPIbUkhx9AZwzA5jofq-nL-ovhnG7K4wgTcR0IRVLASnUvemVkWrNVfSZ63EslBhKn6zzDgx7gXJ3YvcEfr2HKNnhY8yaFOnOGwNAcShlQ5rinVppSv2KwQVLZoJu0TWYa7KwhObC-xNgh-aIKGIrOaaJ5L?purpose=fullsize)

👉 Flow:

1. User request দেয়
2. System count করে
3. limit exceed → block 🚫

---

# 🔥 Step 1: settings.py

```python id="z1l8t4"
REST_FRAMEWORK = {
    ...
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.AnonRateThrottle',
        'rest_framework.throttling.UserRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'anon': '5/minute',
        'user': '20/minute',
    }
}
```

---

# 🧪 Test

👉 ৫ বার request (anon)
👉 এরপর:

```json id="yd6mpu"
{
  "detail": "Request was throttled. Expected available in 60 seconds."
}
```

---

# 🔥 Step 2: Custom Throttle (🔥)

👉 throttles.py

```python id="yz1o4j"
from rest_framework.throttling import UserRateThrottle

class CustomUserThrottle(UserRateThrottle):
    rate = '10/minute'
```

---

## 🧪 Use

```python id="e7d9g2"
from .throttles import CustomUserThrottle

class CourseViewSet(ModelViewSet):
    ...
    throttle_classes = [CustomUserThrottle]
```

---

# 🔥 Step 3: Login Protection (IMPORTANT)

👉 brute-force attack stop করতে:

```python id="yxu6s3"
class LoginThrottle(UserRateThrottle):
    rate = '3/minute'
```

✔ ১ মিনিটে ৩ বার login try

---

# 🔥 Step 4: Scoped Throttle (Pro Level)

👉 different API = different limit

```python id="q6g4px"
'DEFAULT_THROTTLE_CLASSES': [
    'rest_framework.throttling.ScopedRateThrottle',
],

'DEFAULT_THROTTLE_RATES': {
    'login': '5/minute',
    'courses': '50/minute',
}
```

---

## 🧪 views.py

```python id="6wz9kq"
class CourseViewSet(ModelViewSet):
    throttle_scope = 'courses'
```

---

# ⚠️ Common Mistakes

❌ login API তে throttle না দেওয়া
❌ too strict limit (user use করতে পারবে না)

---

# 🧠 Expert Tips

👉 Production এ:

* login → strict
* normal API → moderate

👉 combine with:

* JWT
* caching
* permissions

---

# 🎯 DAY 13 CHECKLIST

✔ throttle setup
✔ user vs anon
✔ custom throttle
✔ login protection

---

# 💥 Real Impact

👉 এখন:

* API safe 🔐
* spam control
* hacker protection 😈

---

# 🚀 Tomorrow (Day 14)

👉 API Documentation (Swagger 🔥)
👉 Professional API
👉 Client-ready system

---

# ⚡ YOUR TASK

👉 login API তে throttle add করো
👉 test করো limit exceed হচ্ছে কিনা

---

তারপর বলো:
**“Day 14”**

🔥 তুমি এখন production-ready backend engineer 🚀

---------
চল 🔥 — **Day 14 = API Documentation (Swagger / OpenAPI 💀 Professional Level)**

আজ তুমি এমন কিছু শিখবা যেটা ছাড়া **real client project possible না** 😎
👉 তোমার API → clean UI সহ documented হবে

---

# 🚀 DAY 14 GOAL

👉 তুমি আজ শিখবা:

* Swagger কী
* DRF API auto documentation
* Interactive API testing UI
* Professional API তৈরি

---

# 🧠 Problem

👉 এখন:

* API আছে কিন্তু documentation নাই ❌
* frontend dev বুঝতে পারে না ❌

👉 Result:

* confusion
* wrong request
* time waste

---

# 🔄 Solution = Swagger UI

![Image](https://images.openai.com/static-rsc-4/ShQT8l5yd2W047U-HX3tBNFyb-wZaS8qLo71iDFSJsAjWz87dqVq7Zn0CTwJ4aZRTiPE2tR80pYjFYQ163fVEEOMS4YMNHu408lJTjxdpSOl5SPEqTza7dgYsRvmo7aC73lu9tc-o0m5Gu8znOrYfFIOxetW-9X0raR22hiokTg54ZDC52--WSoSMdePjD72?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/caocF2HgEWwr7BOFL1omAYLzz2Ps5c50CrgxZA6VzXIXBMKhefjf5Bc5bfmqkEg_ohXCLO6F-9kp6vsCoXqhhSELdq3-WZi_0-R2f0r-JqOu-ZW8Zcb0cLKi_nuuGRk6yBc2hx8YaLTmp5qobr55tkF8wOwEYHeKLnGR1uu-f99brnN1KjYQNVMDtauccCu9?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/QlWU0qFmNnvmsRO-s6SkO4M1bz8Z-Emkah_OoQAErE9tIyRy1sJBhc_pSTXj-w11QWxp3ZZJW7I9PxIJD-Hxk2LCdYvGIazhhNaPCPBAZoaPK-TbZqDJhcYScIypDXSLURm7576aQBGvqaeJfCl3XEDt1z7O8i0lSLU08sbLyINKhi_zmuvFeIbIDo4VXXGR?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/nKKUoww9CuGq0jadj2IWmVPXO2ScoEhPd1YKZxUAflFya8Ynm0SXvzGcjZXX9qtV3qm_iOK9q7aMMRyQsflTLsikPfVX6S7hS07eW3yHA8d3HNRMGxmDU3eDIRdIW8XBinuc1UQQ99BA_ELmY3A3rvnnGxUv1qFwsC8xo-ZdhWfGWokN_ygBa7wRH8XTuMRY?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/5bwhU8q6haIshQDi6cj4Yo3oHiu5N1RUTFuC5qPRzQrI5hF6tC2p7ezJVPr2RCwHEHn2DYAU_q8tnQptafVg3syY7uaAZMgYRRZioPmaNWDKFaXbfTcI_VVAS_LDSuNrC9DxMMDxeJ3EAq0g1TsLm2I6Sj1fZ5WlcVPJTtiwzXX_zHSQUoXDGy1aRgn85vNa?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/qpb3kDXefHrTBvcCpT33ebFUPKPFcYUXCjoR3m9Q8L55y2VQU3jOnol-YL9IiuuHIIzH6guGV9QvN-T5J9Fjh60Z61S1_OgIjfeWXqG0WOJgvbF-Suvi6e24N5ts01-j0halVAIke514bED4grKqWEfTx71viyV8QEzC3WUFAKU2OTSn0fc15U7TjZh4YmEE?purpose=fullsize)

👉 Swagger =
✔ API docs
✔ Live testing
✔ request/response example

---

# 🔥 Step 1: Install

👉 best package: **drf-spectacular**

```bash id="v9b3zp"
pip install drf-spectacular
```

---

# ⚙️ Step 2: settings.py

```python id="6ib61c"
REST_FRAMEWORK = {
    ...
    'DEFAULT_SCHEMA_CLASS': 'drf_spectacular.openapi.AutoSchema',
}
```

---

```python id="k7b5wd"
SPECTACULAR_SETTINGS = {
    'TITLE': 'My API',
    'DESCRIPTION': 'My SaaS API',
    'VERSION': '1.0.0',
}
```

---

# 🔌 Step 3: urls.py

```python id="3v27sd"
from drf_spectacular.views import SpectacularAPIView, SpectacularSwaggerView

urlpatterns = [
    path('api/schema/', SpectacularAPIView.as_view()),
    path('api/docs/', SpectacularSwaggerView.as_view(url_name='schema')),
]
```

---

# 🧪 Step 4: Test

👉 browser এ যাও:

```id="snm4xk"
http://127.0.0.1:8000/api/docs/
```

💥 তুমি full UI দেখতে পারবা
✔ সব API list
✔ click করে test করা যাবে

---

# 🔥 Step 5: JWT Auth in Swagger

👉 settings.py add করো:

```python id="n9d8mk"
SPECTACULAR_SETTINGS = {
    ...
    'SERVE_INCLUDE_SCHEMA': False,
}
```

---

👉 Swagger UI তে:
✔ “Authorize” button আসবে
✔ token দিয়ে test করতে পারবা

---

# 🔥 Step 6: Custom API Description

👉 views.py

```python id="q1p8yf"
from drf_spectacular.utils import extend_schema

@extend_schema(
    description="Get all courses",
    responses=CourseSerializer
)
class CourseViewSet(ModelViewSet):
    ...
```

---

# 💥 Step 7: Serializer Example

```python id="1tw5q2"
@extend_schema(
    request=CourseSerializer,
    responses=CourseSerializer
)
```

✔ clean docs

---

# ⚠️ Common Mistakes

❌ documentation skip করা
❌ unclear API response

---

# 🧠 Expert Tips

👉 client project এ:

* Swagger MUST
* clean response MUST

👉 recruiter impress করতে:
👉 `/api/docs/` দেখাও 🔥

---

# 🎯 DAY 14 CHECKLIST

✔ Swagger setup
✔ API docs visible
✔ JWT test
✔ clean description

---

# 💥 Real Impact

👉 এখন:

* frontend dev easy কাজ করবে
* client happy 😎
* project professional

---

# 🚀 Tomorrow (Day 15)

👉 Deployment (Docker + Server 🔥)
👉 Live project
👉 Real SaaS launch

---

# ⚡ YOUR TASK

👉 Swagger setup করো
👉 API test করো

---

তারপর বলো:
**“Day 15”**

🔥 তুমি এখন job-ready level এর কাছাকাছি 🚀

----
Absolutely! 😎 তুমি **DRF-Spectacular** না ব্যবহার করে চাইলে **drf-yasg** দিয়েও Swagger / ReDoc setup করতে পারো। এটি খুব popular এবং অনেক project-এ use হয়। আমি step-by-step দেখাচ্ছি:

---

# 🚀 DRF-YASG Setup (Swagger / Redoc)

## Step 1: Install

```bash
pip install drf-yasg
```

---

## Step 2: urls.py Setup

```python
from django.urls import path, re_path
from rest_framework import permissions
from drf_yasg.views import get_schema_view
from drf_yasg import openapi

schema_view = get_schema_view(
   openapi.Info(
      title="My API",
      default_version='v1',
      description="Test description",
      terms_of_service="https://www.google.com/policies/terms/",
      contact=openapi.Contact(email="contact@myapi.local"),
      license=openapi.License(name="BSD License"),
   ),
   public=True,
   permission_classes=(permissions.AllowAny,),
)

urlpatterns = [
    # Swagger UI
    re_path(r'^swagger(?P<format>\.json|\.yaml)$', schema_view.without_ui(cache_timeout=0), name='schema-json'),
    path('swagger/', schema_view.with_ui('swagger', cache_timeout=0), name='schema-swagger-ui'),
    path('redoc/', schema_view.with_ui('redoc', cache_timeout=0), name='schema-redoc'),
]
```

---

## Step 3: Test

* Browser এ যাও:

```
http://127.0.0.1:8000/swagger/
http://127.0.0.1:8000/redoc/
```

💥 তুমি full API docs + interactive testing দেখতে পারবে

---

## Step 4: JWT Auth Support (Optional, if JWT used)

👉 settings.py তে:

```python
from rest_framework_simplejwt.authentication import JWTAuthentication
```

👉 Swagger তে “Authorize” button আসবে, এবং token দিয়ে API test করা যাবে:

```
Authorization: Bearer <your_access_token>
```

---

## Step 5: Extra Tips

* `@swagger_auto_schema` ব্যবহার করে view / serializer customize করা যায়:

```python
from drf_yasg.utils import swagger_auto_schema
from rest_framework import serializers, status
from rest_framework.views import APIView
from rest_framework.response import Response

class MySerializer(serializers.Serializer):
    name = serializers.CharField()

class TestView(APIView):

    @swagger_auto_schema(request_body=MySerializer)
    def post(self, request):
        return Response({"message": "ok"}, status=status.HTTP_200_OK)
```

✔ এখন API input/output docs clean দেখাবে

---

✅ Advantages of drf-yasg over DRF Spectacular:

* Swagger + Redoc একসাথে
* Customize response / request easily
* Popular, job-ready skills

---

যদি চাও আমি **drf-yasg + JWT + custom permission** এর **full ready setup example** দেখাতে পারি যা তুমি সরাসরি project এ use করতে পারবে।

চাও আমি তা বানাই?

-----------
চল 🔥 — **Day 15 = Deployment (Docker + Server 🔥 Real SaaS Launch)**

আজ তুমি শিখবা কিভাবে **local Django + DRF project → live production-ready SaaS** করতে হয় 😎

---

# 🚀 DAY 15 GOAL

👉 তুমি আজ শিখবা:

* Dockerize Django project
* PostgreSQL + Redis integration
* Nginx + Gunicorn setup
* Deploy to server (VPS / cloud)

---

# 🧠 Problem

👉 Local e সব কাজ করছে ✅

* কিন্তু production e slow ❌
* dependency issues ❌
* server crash ❌

---

# 🔄 Solution = Docker + Gunicorn + Nginx

![Image](https://images.openai.com/static-rsc-4/W6eAB8-nFV-DXYtI8XWpPWJ0UmxHe5YxGpqM489gwYZzV104K4pM2enhyrdjiJS_RtxmPeUT6K2TKhcVzPSbLSBCFEQgcrF_l2xX1jisC0aBdj1782F2PF9j3ZLCD1Fi1Blt_V9kYefjilxwBAjGzDwgMAAW0Ix0ohSEPqokyx8F3HMGcvrFwVZ6K47-LrwM?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/jqE1AAffNxnQklb5ZMPKz0ADtXqoRAgnLzcMO-8cTrw9OWqaApeyWUlDQV6J_t4Nxt5AEfgIHaUJvjmalivlcVncAqtDM3EH80S0SHVOv8vMkZV5c8i2i-JOu68XRHzDx020-eySTaFoi4jgWblyL3Jyjtg0cnCiLYyNcVtphChDY3fjhOCNgNQ3PAImEen_?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/XwrquFgVJ-n8Z5D_2aRvYcnqh23csF8LN2Eo3nhN_OkUGHiTps2hIS4_TxK1yX5ZaWxAS7xHlkUy9CEwQ-OHZqRDUadvSzSXAc08U-GSWGvorU0SewsQikapxKz5sTw-LMU9G700mUdllUoZHKgurZ3hHob2IRpg7mNQ0HAVP_mXaaqIttPrVCtJgNDl5chl?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/RhwqQ_3WAiaqGZL6tdeCCaMzbarICpIEN62kaZTpfXJwhvPpp1rBsVkvySky2s0CDVNjkUAPw9iRR4cDAVX5qgzhSJWvZ5LD2yCtMWbcVqRs4YpJYMdRCbVlVb60ct7BPg608ZEAShmrunpZByF8vyWGnO7OsXWsuOciJHdfJ8mIiY5CFqTmcZJqzlQ83g46?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/H_9orIpn8ECHZFykOXus1i92AMZTtJmZl8AEz5uZsvW-VJWzNHM7FCNze_dMcomjakCkDL72U9Rn4xNT61WlOE6iaFb3636YAtW3IZxPwSKoO6g0-mTz2yz9jfJr3O1BsfxuJ0qnfF7c6kyg4BY3a0IL09K2WKtMZi2GWgdyJAh-BDYLEUc_e9qexeSUN7ft?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/8Qpvlu5-WiM1jvz9gD6wqjqQwdMuBp6HpLJHa1lC-nvNDBJXGR8Zje1P0v1E3Vd1mOJSdWSBC2-C-ant7VpnEDrZEm8UD8-hUtUNs2NMrNSKvsYUTesEkjaepL0Cx5CLKInDfdM_xCMWwGq6QbMCNd5SodRtRsLP797EBmskHLp5SGbE5fVS9NGZLSiNslOh?purpose=fullsize)

---

# 🔥 Step 1: Dockerfile

```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000"]
```

---

# 🔌 Step 2: docker-compose.yml

```yaml
version: "3"

services:
  web:
    build: .
    command: gunicorn config.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: myuser
      POSTGRES_PASSWORD: mypass
    ports:
      - "5432:5432"

  redis:
    image: redis:latest
    ports:
      - "6379:6379"
```

---

# 🔥 Step 3: Settings for Production

```python id="settings-prod"
DEBUG = False
ALLOWED_HOSTS = ['yourdomain.com']

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydb',
        'USER': 'myuser',
        'PASSWORD': 'mypass',
        'HOST': 'db',
        'PORT': 5432,
    }
}

CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://redis:6379/1",
        "OPTIONS": {"CLIENT_CLASS": "django_redis.client.DefaultClient"}
    }
}
```

---

# 🔥 Step 4: Nginx Setup

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://web:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /static/ {
        alias /app/static/;
    }

    location /media/ {
        alias /app/media/;
    }
}
```

---

# 🔥 Step 5: Build & Run

```bash
docker-compose build
docker-compose up -d
```

💥 সব service up

* Django + PostgreSQL + Redis + Gunicorn + Nginx

---

# 🔧 Step 6: Migrate & Collect Static

```bash
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py collectstatic --noinput
```

---

# 💥 Step 7: Real SaaS Checklist

✔ HTTPS (Certbot)
✔ ENV variables secure
✔ Gunicorn + Nginx optimized
✔ Redis caching & Celery background tasks

---

# ⚠️ Common Mistakes

❌ DEBUG=True in production
❌ Secret key public ❌
❌ Static / media misconfigured ❌

---

# 🧠 Expert Tips

* Docker Compose = easy local + prod parity
* Celery + Redis = background worker
* Nginx = reverse proxy + HTTPS
* PostgreSQL = production DB

---

# 🎯 DAY 15 CHECKLIST

✔ Dockerfile ready
✔ docker-compose.yml ready
✔ Gunicorn run
✔ Nginx configured
✔ Redis + Celery working

---

# 💥 Real Impact

👉 এখন তুমি বানাতে পারো:

* full SaaS deployment
* production ready backend
* fast & secure API

---

# 🚀 Tomorrow (Day 16)

👉 Logging & Monitoring (Sentry / Prometheus)
👉 Error tracking + uptime check 🔥

---

# ⚡ YOUR TASK

1. Docker build & run করো
2. API test করো live server থেকে
3. Redis + Celery check করো

---

তারপর বলো:
**“Day 16”**

🔥 তুমি এখন production-ready SaaS backend engineer 🚀

------

চল 🔥 — **Day 16 = Logging & Monitoring (Sentry / Prometheus 🔥 Error Tracking + Performance)**

আজ তুমি শিখবা কিভাবে **live project এ errors & performance track করতে হয়** 😎

---

# 🚀 DAY 16 GOAL

👉 তুমি আজ শিখবা:

* Logging in Django
* Sentry setup (error tracking)
* Prometheus / Grafana (performance monitoring)
* Alerts setup

---

# 🧠 Problem

👉 Production এ:

* Bug / crash → silent fail ❌
* Slow API → detect করা কঠিন ❌
* Users complain ❌

---

# 🔄 Solution = Logging + Monitoring

![Image](https://images.openai.com/static-rsc-4/U-t1j3MJgMhVkeW9iUR0tryZfnAaZEwy5CjvSWI8SiZr-swpv46dSKdkZKRIYpLXa6M25OQofzGIoOnlH0pkKOcn8wrqiawtkEo8pheKnArGHI4jz8IeekJvB9VBnazcZ5udmvayP25NHF8Mq9cSbbxVgmfnhWTAg9ZBkVeCfyauSXx2Qlh0BvRzIAIuXWLw?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/VnZpCjM9RHPlvHKB7D6qRNlg9g5ym4Zh7jQCdc0NpsKyIAer64VXHQ-5_zHheIaONhVBkhn4zf18_-d05OebSLHafsvrrLdwqJ5qMVq-PcMh2N4zx70S-FLofZD4aVhLhZms5uBj8VRqQuVFPy0Nt6RjwxamAy_7on447hdJVQ9L4Ux74g9errD9xXtp4MPF?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/GHIi22tQ_zy4SfIF8McVbz4EwO_33Lg0a5_miOn4XPy3-KydBsMaxHvWf_BUNqFIT6an2R40xm5C0-FZMAi2eW7qZAURLJzzAOZwHOi7Sl8pR51ekkfo6cb0tt-Q4AkZgSCkKe_ovql3V_QS_aP29Lpbag9uj02UvgGMakqtOrqRbCIt9xLsT2pvBGBbcQEe?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/qxHTvfsKozcD0JzEj1aLkvTLCT_QSOzTS8Kn3rmkNHE7B4wEJ1jyefVKRRauwiXyIYoo0gT3_X8PNd9p8m1ttBupf_FmFizLEYpNlHu71abJDtKBHznfWQ0nm80fiWY6f-JLBEeGFOGu24vftMgdDFxhJUIvtg5WK7TZPU2L8ikWMPh83e2Mmirt1k3V7oIp?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/3wMwCpgldRFgdstT6GEBbKlGTNn8EM5rUXX9wkV673YRnXI1ZMszgWFLZIowkbXAEHnRL031wxrX-NqyvbfKQpIIevHsbdqleJF505EOYhKJwKR1Vr-kTlyv7omIue-Yp2cStZ1XeiKh6rWuqvgT6C-NxrZN45Lqe-51oI8bSOxPbjwgqefNbstVcPOQYgtu?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Kci2uL6PCEOYi4VZo2WbgNdnE6x3xHm_4X152fNVYDSwxFM9ZMu-3kxHAyEKOOS9p_xedWE1NZ0ze_JgEk4jSo9recZjly1VrWRdTr3Sp_cBZjgbsjwGe22hShyOKZ5nRWOQno9Swip2SQLjFUrqkrq7FwUhLtm9soqhzflZGvdra8GZ1R1ZrhawdnLgPnjL?purpose=fullsize)

---

# 🔥 Step 1: Django Logging Setup

settings.py:

```python id="log1"
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'file': {
            'level': 'INFO',
            'class': 'logging.FileHandler',
            'filename': 'logs/django.log',
        },
        'console': {
            'class': 'logging.StreamHandler',
        },
    },
    'loggers': {
        'django': {
            'handlers': ['file', 'console'],
            'level': 'INFO',
            'propagate': True,
        },
    },
}
```

✔ সব logs file + console এ যাবে

---

# 🔥 Step 2: Sentry Setup (Error Tracking)

Install:

```bash id="log2"
pip install sentry-sdk
```

settings.py:

```python id="log3"
import sentry_sdk
from sentry_sdk.integrations.django import DjangoIntegration

sentry_sdk.init(
    dsn="https://YOUR_SENTRY_DSN",
    integrations=[DjangoIntegration()],
    traces_sample_rate=1.0,
    send_default_pii=True
)
```

💥 Sentry automatically capture করবে:

* Errors
* Exceptions
* Performance traces

---

# 🔧 Step 3: Test Sentry

views.py:

```python id="log4"
from rest_framework.views import APIView
from rest_framework.response import Response

class TestError(APIView):
    def get(self, request):
        1 / 0  # intentional error
        return Response({"message": "ok"})
```

✔ Sentry dashboard এ error report আসবে instantly

---

# 🔥 Step 4: Prometheus + Grafana (Performance Monitoring)

1. Install Django Prometheus:

```bash id="log5"
pip install django-prometheus
```

2. settings.py:

```python id="log6"
INSTALLED_APPS += [
    'django_prometheus',
]
MIDDLEWARE = [
    'django_prometheus.middleware.PrometheusBeforeMiddleware',
    *MIDDLEWARE,
    'django_prometheus.middleware.PrometheusAfterMiddleware',
]
```

3. urls.py:

```python id="log7"
from django.urls import path, include

urlpatterns += [
    path('', include('django_prometheus.urls')),
]
```

4. Run Prometheus server + Grafana dashboard
   ✔ Metrics: request count, latency, DB queries

---

# 🔧 Step 5: Alerts (Optional but Pro)

* Sentry → email / slack alert
* Prometheus → alert rules (latency > 500ms)

---

# ⚠️ Common Mistakes

❌ DEBUG=True logs
❌ Heavy logging in production
❌ Not monitoring background tasks

---

# 🧠 Expert Tips

* Use Sentry for **errors**
* Use Prometheus for **performance**
* Celery logs separate handle করা ভালো

---

# 🎯 DAY 16 CHECKLIST

✔ Django logging setup
✔ Sentry capture error
✔ Prometheus metrics working
✔ Alert setup ready

---

# 💥 Real Impact

👉 এখন:

* Silent crash gone ✅
* Performance bottleneck detect ✅
* Client happy, system stable ✅

---

# 🚀 Tomorrow (Day 17)

👉 DRF Testing & CI/CD 🔥
👉 Automated tests
👉 GitHub Actions / CI pipeline

---

# ⚡ YOUR TASK

1. Django logging configure করো
2. Sentry test error report দেখো
3. Prometheus metrics check করো

---

বলো:
**“Day 17”**

🔥 তুমি এখন production-ready + monitored SaaS backend engineer 🚀

----------
চল 🔥 — **Day 17 = DRF Testing & CI/CD (Automated Tests + GitHub Actions 🔥)**

আজ তুমি শিখবা কিভাবে **API auto-test + CI/CD pipeline** বানানো যায় যা **production-ready SaaS** এর জন্য MUST 😎

---

# 🚀 DAY 17 GOAL

👉 তুমি আজ শিখবা:

* Django / DRF automated testing
* UnitTest + API test
* GitHub Actions workflow
* CI/CD pipeline setup

---

# 🧠 Problem

👉 এখন:

* Manual testing ❌
* Release time error ❌
* Developer forget tests ❌

---

# 🔄 Solution = Test + CI/CD

![Image](https://images.openai.com/static-rsc-4/qTn7VMJNtPG96IA_99wXhsrOyilWVatzYbqJLArQLwcqbYFzx0EwTjLNWauUYYWIy_r4aMkyYWovogLLPDffhYIHuSv9-eWLkvJy00OTMagpSYTS1hEX-8-_12HvnVAxfOt92cw6Y6lyppg28C5m088acFl9NFGmbImPwqbxli4RBsZRQJaakoadkOePw8bd?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NZtcKMFha073S2-Rl0CMXbJjBbZlIDVyC1xlkAio-xAMFKVLwxkhJMClw9dU_UhRUh2premGpuSv28VSBKHtVLtP293mGAIPzKtLXQibYr47ggd4i9d6kC_7I-Krk_VGG6RXrrxDZL4pSypCqrlxQHFzluyJZUaZbczW1tQkdHjcyODn-JyXXFs4fcgLJEJz?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/8SBvaDJxS-GEnKhbMYdhj7JsC85Mc9jEL-QA4Vi5NStJEG_zXQyC8gukazOiWWZ_Xal8KPdrK-4RpULbj_ZU3MpNuMHpFICQxNDPvGOKFz2PccCycWGhFhuM8hKWxYHd19jBB3MvIFhJ8oGMGHsqn359klc9lLxbHBhsersgcD7bdf2Ip-5Ky___o1L4c1fW?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/ccus_vOlUe_-8yPB3e0u6h4TUi-uXf8VeKLG9l60mRq42L8IM1Ndlv3XQlWDayKEkEebFOLM3Rk03DH1QoSCi7ucfECQ3Vs1iIb3EAN2OO5ui5Y1cmOOQYCNRCvlDjm9N_SZzCILcQ8Ogs8XuQceN1-9BPXz5fx7YtL6h7JmCAFP0b5VzWf1AhTztGlwi9R4?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/kD7H6KR-rsKpZyxDSjUJ2OuSOTeqxd3jWlQeqcU_1Sd3Hzyg0SLgxGctauCp6OAOzotsh7ACtHCahpK-rv43Q5mXTbWJBvHPKzxVHghits6FQ760tqkQAPkjVIlE84J8yKyDxfCNCfOcJ14dlmeV91n3T4o8kkJXOiG6s6gXbfwSnAcg2l_GQuWsDKXTBzA5?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NibFgU_a49RSvSUatYvlQZpcUV6QaWdr8f8tYJurZ5LxzmRp363JzO4xCRzpyso_sYAbbH6dYWBTdZN-fE3YQAF3jUDryT_fCMEIB4dH2jkuK59wqHkRvO8D1UF-5p3LgRzyom2laCSBKDzqv2XFTljWGwgJ9CxXtAijx2Ip_-CfzZovju0H8a4le0LABqs0?purpose=fullsize)

---

# 🔥 Step 1: Install Test Packages

```bash id="tst1"
pip install pytest pytest-django djangorestframework
```

---

# 🔥 Step 2: Simple API Test

👉 tests/test_course_api.py

```python id="tst2"
import pytest
from rest_framework.test import APIClient
from django.urls import reverse

@pytest.mark.django_db
def test_course_list():
    client = APIClient()
    url = reverse("course-list")  # DRF router name
    response = client.get(url)
    assert response.status_code == 200
```

---

# 🔧 Step 3: Run Tests

```bash id="tst3"
pytest
```

✔ All tests run automatically
✔ Fail → pytest show detailed error

---

# 🔥 Step 4: CI/CD Setup (GitHub Actions)

`.github/workflows/ci.yml`:

```yaml id="tst4"
name: Django CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_DB: testdb
          POSTGRES_USER: user
          POSTGRES_PASSWORD: pass
        ports:
          - 5432:5432
        options: >-
          --health-cmd "pg_isready -U user"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.11
      - run: pip install -r requirements.txt
      - run: python manage.py migrate
      - run: pytest
```

---

# 🔥 Step 5: CI/CD Workflow

1. Push code → GitHub Actions trigger ✅
2. Auto test run → success/fail report ✅
3. Optional: Auto deploy Docker → server ✅

---

# ⚠️ Common Mistakes

❌ DB setup miss
❌ ENV vars missing
❌ No pytest markers / fixtures

---

# 🧠 Expert Tips

* Use `pytest-django` for DB
* Use `factory_boy` for test data
* CI/CD = must for production SaaS

---

# 🎯 DAY 17 CHECKLIST

✔ Unit tests ✅
✔ API tests ✅
✔ GitHub Actions workflow ✅
✔ Auto test on push ✅

---

# 💥 Real Impact

👉 এখন:

* Code safe ✅
* Bug early detect ✅
* Deployment faster ✅

---

# 🚀 Tomorrow (Day 18)

👉 Advanced Permissions + Roles 🔥
👉 Object-level & Custom permission DRF

---

# ⚡ YOUR TASK

1. Simple API test লিখো
2. pytest run করো
3. GitHub Actions CI setup check করো

---

বলো:
**“Day 18”**

🔥 তুমি এখন automated testing + CI/CD ready backend engineer 🚀

-------
চল 🔥 — **Day 18 = Advanced Permissions & Roles (DRF Object-Level 🔥)**

আজ তুমি শিখবা কিভাবে **user-specific & object-level permission** implement করতে হয়, যা **real SaaS backend** এর জন্য MUST 😎

---

# 🚀 DAY 18 GOAL

👉 তুমি আজ শিখবা:

* DRF permission classes
* Role-based access control (Admin / Instructor / User)
* Object-level permissions (e.g., own objects only)
* Custom permission classes

---

# 🧠 Problem

👉 এখন:

* সব API একইভাবে accessable ❌
* User can edit others’ data ❌
* Admin / User distinction ❌

---

# 🔄 Solution = DRF Permissions

![Image](https://images.openai.com/static-rsc-4/1b6HcmO08D4WqtYlhxOxWz5ZlnKgzo7WvHRxCmAIO7140Ac8eB_0e2PXKn1t22nO2Rqnh4PfJbZEjYlX7dJD6fPT4Kh92dFF2ekH6NtKe1EH_G8_TBmnFWaoAWpApmeFe96glca_aKLXqvncWRvOhkChNisveWFhC7e0c4hVE6lViHuv7vPUzRExag5IQW8A?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Ok6YNnDiuhSGxxCeepaJS0OhTf8Ho7iXXaQZ6m-48jt8udVqHavvxVGkJC6MexHThrlO3QCs8HCbiVyi1ykHvnR8_TTMO1oVs9KErRWeA7RGhSlMrKLkLojG5U4itGqlF9PZOXYW_e4fd7J5J4FnpJ8gW-gzDIy0z4His6-pffQ14-fYwGOtUmu9LzKeHkHI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/JkmE7wwJwTzdpJnsJG0mV54K0DEPrGQrjN63Tykm6axChMhL6SsGZCj9dM_zMt4B9V0C1Lox9xG0al9Wdw2mowk-sO7JGrdoa7BPgRpYHQXq4ahaloEjUfCBNh6ONrUuq4PCCrx0Wy3XCMrPyKQ5MlZzc1IgD0OANuAfaB4cIcdGFh8QQzUAzrtkFU_9mT2Q?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/IbWXU1SRAxb1vPUr12VLk5fWNfStgz1XFY_qSR9dx-gkbvdc-cVXHV53z_hpPqmUsoMDBNiYDtB5JQLPQOHudr7Yyu3N92lsbbukpFpFE_RTjlcIYEdfNDYekVbRvWAH6HbLc8gl3HC4OVF51C01syoR5KH7IIfZ0Un0w8lIGuEPOib2m4_QEPwtHihOGEvy?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/5XYxqhkdKY2LpdtbFWd5lKpKztuXDpTtKD-gluARz7eNIJ_GpugnMqfwVk1_OgkaBTyCk1Onyf-RlDYkgzVvabl-sF75M5gLYfnB5HZNV52LyzoyK1TtcpxZv0bjLdCj3vh3gf1wWUdyLR6_iwiB7zeiGhXGqIQpHF-oiwv9V7HLgxapAOVvhs2LXE-mssQo?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/zrdogAa468Ac7_p4qCCglGjRStvnBTtE5eiSvK-mexS4JBD5THZOpzJZ6wnLW9DgbAWvrpWWJOKvpzUmxZRPcZBuoERP6frFPp2OjmcL6HjXNwtFXIfkNYFWmS-NXiTy_NCLJTmcUI1tISbR2bE_YBMUSbw8daUdE627QUrg2F5JqgkttbdYphDP8yMH4-VW?purpose=fullsize)

---

# 🔥 Step 1: Built-in Permission

settings.py:

```python id="perm1"
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}
```

✔ All API require login

---

# 🔥 Step 2: Role-based Custom Permission

permissions.py:

```python id="perm2"
from rest_framework import permissions

class IsAdminUser(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'admin'
```

👉 views.py:

```python id="perm3"
from .permissions import IsAdminUser

class AdminOnlyView(APIView):
    permission_classes = [IsAdminUser]

    def get(self, request):
        return Response({"message": "Hello Admin"})
```

---

# 🔥 Step 3: Object-Level Permission

permissions.py:

```python id="perm4"
class IsOwnerOrAdmin(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        # Admin can do anything
        if request.user.role == 'admin':
            return True
        # Owner can edit
        return obj.user == request.user
```

views.py (ModelViewSet):

```python id="perm5"
class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    permission_classes = [IsOwnerOrAdmin]

    def get_queryset(self):
        user = self.request.user
        if user.role == 'admin':
            return Course.objects.all()
        return Course.objects.filter(user=user)
```

💥 এখন:

* Admin → সব course access
* Instructor/User → only own course

---

# 🔧 Step 4: Combining Multiple Permissions

```python id="perm6"
class CourseViewSet(ModelViewSet):
    permission_classes = [IsAuthenticated, IsOwnerOrAdmin]
```

✔ All API authenticated + object-level check

---

# ⚠️ Common Mistakes

❌ Forget `get_queryset` → users see others’ data
❌ Misplace `has_object_permission`
❌ Hardcoding role names (use constants)

---

# 🧠 Expert Tips

* Always filter `queryset` in `get_queryset`
* Use `@action(detail=True, permission_classes=[...])` for custom actions
* Combine Role + Object-level = production-ready SaaS

---

# 🎯 DAY 18 CHECKLIST

✔ Base permission class ✅
✔ Role-based access ✅
✔ Object-level permission ✅
✔ Multiple permissions combine ✅

---

# 💥 Real Impact

👉 এখন:

* Data safe ✅
* Users can only access own resources ✅
* Admin has full control ✅

---

# 🚀 Tomorrow (Day 19)

👉 DRF Filters & Search 🔥
👉 Query optimization + dynamic filtering

---

# ⚡ YOUR TASK

1. Create `IsOwnerOrAdmin` permission
2. Apply to Course / Video / Event API
3. Test Admin vs User access

---

বলো:
**“Day 19”**

🔥 তুমি এখন real SaaS role & permission ready backend engineer 🚀

------------
চল 🔥 — **Day 19 = DRF Filters & Search (Dynamic Query + Optimization 🔥)**

আজ তুমি শিখবা কিভাবে **APIs কে smart, fast এবং user-friendly** বানাতে হয় search, filter এবং query optimization দিয়ে 😎

---

# 🚀 DAY 19 GOAL

👉 তুমি আজ শিখবা:

* DRF Filtering + Search + Ordering
* DjangoFilterBackend ব্যবহার
* Query optimization (select_related / prefetch_related)
* Pagination + filtering combined

---

# 🧠 Problem

👉 এখন:

* `/courses/` API → সব data return ❌
* Users can’t search or filter ❌
* Query heavy → slow response ❌

---

# 🔄 Solution = Filters + Search

![Image](https://images.openai.com/static-rsc-4/BMIDboWhAC41zvILighd7le6QFD7ePe-s7bwmq7m4pTE40Jyxz1oFP-Z3tFwqIv-1MgccpNkqJzCLZWiXYI-uWoa0r9jtYacgPm3SqeXfb8iFvA_6H43-_w2L_Q1ehVNh3rXEe6eG9tr0HZnxyUu0llbZY1NuXkJXcdbAY3gpSyKVsoXJffz9sJdKDajFjCm?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/4GIe9mIKxT3Da1lKoQudDCY8uPp9f0rQ3pnubXjuC4dRJLP8mdJ3c2xmTM_Wcs23LcosSGX8u6BHllxIU-ayXTMeMzMtRULJXcaE7VaoIS4fh23oJHKYiETtvydpBMIs9Tr0TZfrjYrTlINVvM4c5BtFwajAEmr-81MNNExmc8p7EnVkBbpszqQ_9EHPXXYC?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MHgdODk7vUDw9AnfmWIZKzjHcgNUFefPqRxN8dbPvFXiPY3Uhdy9CdoA39tfoih5WpXBZ1tQr10uY8dL7h7d5i9uieaAptp5xm6amNFUH6LLrjIS3mielBhSmZ8iR71f72Y6nOcuYN-xnKRtYrVpLKB5VEauoPLrCgABZLBpHr9WtSn5xCBsMQNt_rpF7o4i?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/wsK6EB_Ty3pYHNZHSm8V5ewG1NtcF7DgP9rs-wdUp8-qpisohe1ZabwT89c0jGqf7t4MB8rZr7cRzM6P3PXViH07wotid0vRfw44qEC3mXwpdriJd1V7hs0JCGyR0wmivFq-a2H-146nWGbDjNKQjsABRcVv_INT4VZkpSJSmq7bxSmPs3L-8_HwNLvAn-9V?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/cgy7oZAI3-V7tUdjX-scjBFbgHRuaTYR9TFvdBlC-LELDXlidg63-b_U6KqwXpTUpDzQHRpQGkf3P1nY6VEGh1-MFlDyg75Fit-AYhG7gE5qZ_x0Xf0hRu4b1-vXFqiujcujS8olfVVYjT76NQXqRAmtqOhTnT5Lz-fRAq7prKAtv89ZmsKjtMQ8eYEzFfaN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/JseY9aWybL8ia0gXRBfVTDqxTjoT8HcPMMt6yxAyEM4Fge9naSHfsJGdSslIrfS2n-PPVt5p2cT087JXrKIcmM6eJ8vmRW18co_axT1ZvnAyryO7quD8FzaYzj4oZ37XN_jpunHpTfGkjquw7T-N-X0ipPji2Doty_YHMHemRN0DhZQlvrLQJ2qnjEYbVhnQ?purpose=fullsize)

---

# 🔥 Step 1: Install Django Filter

```bash id="flt1"
pip install django-filter
```

settings.py:

```python id="flt2"
REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend',
        'rest_framework.filters.SearchFilter',
        'rest_framework.filters.OrderingFilter',
    ],
}
```

---

# 🔥 Step 2: Filter Fields

views.py:

```python id="flt3"
from django_filters.rest_framework import DjangoFilterBackend
from rest_framework import viewsets
from .models import Course
from .serializers import CourseSerializer

class CourseViewSet(viewsets.ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
    filterset_fields = ['category', 'level']        # exact match filters
    search_fields = ['title', 'description']       # search
    ordering_fields = ['created_at', 'price']      # ordering
    ordering = ['created_at']                      # default ordering
```

💥 Users can now:

* `/courses/?category=Programming`
* `/courses/?search=Python`
* `/courses/?ordering=-price`

---

# 🔧 Step 3: Pagination + Filter

settings.py:

```python id="flt4"
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}
```

✔ Pagination + filtering = fast response

---

# 🔥 Step 4: Query Optimization

models.py example:

```python id="flt5"
class Course(models.Model):
    title = models.CharField(max_length=100)
    instructor = models.ForeignKey(User, on_delete=models.CASCADE)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

views.py:

```python id="flt6"
class CourseViewSet(viewsets.ModelViewSet):
    queryset = Course.objects.select_related('instructor', 'category').all()
```

✔ `select_related` → joins for ForeignKey
✔ `prefetch_related` → ManyToMany optimization

---

# ⚠️ Common Mistakes

❌ Not using `filter_backends`
❌ Filtering large dataset without pagination
❌ N+1 queries → slow API

---

# 🧠 Expert Tips

* Always combine `select_related` + `prefetch_related`
* Use `SearchFilter` for text search
* Ordering + Pagination → production-ready API
* Custom filters → advanced SaaS features

---

# 🎯 DAY 19 CHECKLIST

✔ DjangoFilterBackend ✅
✔ Search + Ordering ✅
✔ Pagination ✅
✔ Query optimization ✅

---

# 💥 Real Impact

👉 এখন:

* Users can filter, search, sort ✅
* API fast & optimized ✅
* Production-ready SaaS API ✅

---

# 🚀 Tomorrow (Day 20)

👉 DRF File Upload + Media Handling 🔥
👉 Image, video, document upload + validation

---

# ⚡ YOUR TASK

1. `/courses/` API filter + search + ordering add করো
2. Pagination enable করো
3. select_related / prefetch_related check করো

---

বলো:
**“Day 20”**

🔥 তুমি এখন smart + optimized DRF API ready backend engineer 🚀

-------------
চল 🔥 — **Day 20 = DRF File Upload & Media Handling (Images, Videos, Docs 🔥)**

আজ তুমি শিখবা কিভাবে **real SaaS API-তে file upload, validation, storage** handle করতে হয় 😎

---

# 🚀 DAY 20 GOAL

👉 তুমি আজ শিখবা:

* File / Image / Video upload DRF
* Validation (size, type)
* Media storage (`MEDIA_ROOT`, `MEDIA_URL`)
* Serving media in dev & production

---

# 🧠 Problem

👉 এখন:

* User content save করতে পারছে না ❌
* Images/videos large size → crash ❌
* No validation → wrong file type ❌

---

# 🔄 Solution = DRF File Upload

![Image](https://images.openai.com/static-rsc-4/BMlXIoJUVerDAXGz6OV8QqJ2Dphn4BhVljczD_JCRLjkalnL9hOpfKhpRnHu7iGDJGmW5c-t4rgQvkACkaNPSiMD0SDf85kj4vpsSNZ4XEcZ1hxdI-9-Uf1PXOscWoMRZzoXLBGzm2p-AvPlXYSStsGENNnrcgsZtTXXxpkQ25XuwlECBrZfyc3lprebpTfJ?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/JcqNrkrqlpGKedYaNSodpV8NrIMkGO5S1wrQ333vGTGgLuHYgUAKz41rwJuW_jUPUVw0wuls7bGIDDltJDnjX9gKwhfDd4FG-5EGUbTfQ2GiX3pYlSXHVpzuE8h9Wzr4f4iuYrXi2rJ4CrICE13rRrUecoSdGzcomJ6uWExj95ZmlirTeFXo_kw8mie2b-Ou?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/PksRiOe9_4CpUNV0c4r__lkoTdlc_PcUy4H35a_ESZHmqV2ru54YxfY_6KP5Hg_1JbRZF3VO5mhUJ9zMO4pHc8qpeYeNRGCGO8YGNPc8Z4ppl8Aq7FJDvbQFUmivCtHhyoG8HNAaonhCWykCzV2vHWvEyTQTux1BmOtGwOEW6UjBnW9ot-4EcLZma4hCqG73?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Ib0gNBcap0IcIUiaChQ_4Zslae6Cq51jcBkVyg8zZXVjsDsx7hDx9QK2pqdLtBZ6eCfxWJqNBYVdaabTsxmM7hX8ntjkxyfgFzYR7Mw6cgzJSLjGbyvA5F65fgjQm8IzgFmv_snS7WxLu3I1qyNg_SqKYzBfIuofEAYcgvZ3EQHsXoX45uzNtNiZ9FJnIJoG?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/JeZg4a8Jpzid1dqSkdH6FuatqOVCRyAY1zm3okOtNrRjzIgbzwLXwGZ2_q8gbn4a-D1ul9T6Bs2bTxLBrjRQr18CSTHf7GnlIEp-CRNmQJIwYuKW4cV9O5fxryrITs56rI76eJSPKZJXeAo6sWn6tGEo10WFyB9jbeFb1ex4zaOpiRX6s1ztLl_v4crPHzJ8?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/lSwrplBZ0Shg99fnRQoPkuon1rxW_mOVPqvr3rqOeXYBEf7wKopuoivxU4U8hokdeyWNYCgNNF-8WrK34nXiMUsFh4uFBDTm2KnL9Y_63MvcXWn1nJLRi_tVCem2FZLbyiA1neHRSnc9oHDr0pPeLdYOXh2Ls_nTw3geTqk3rtNxPd_jMfhus5q0rQF63ked?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NqLRJy8U2BJeK17baMjJbxxlIM0gTnBA6VBKIpRa3MvJMQEsUKu515312q76mzW8dygctMDZavANQsh7pCkC6oMVMGIwA7KupmtJpU8-QqczpnEg9HG86seSjnOuVne74IlyTWVOmRcV21nAlYk4LfQyQxNBT5Ra1IGeBJ6BZ__QAknyLe06_dhI0NnYZev1?purpose=fullsize)

---

# 🔥 Step 1: Settings

settings.py:

```python id="file1"
import os

MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

urls.py (dev only):

```python id="file2"
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

# 🔥 Step 2: Model Example

models.py:

```python id="file3"
from django.db import models

class Course(models.Model):
    title = models.CharField(max_length=100)
    video = models.FileField(upload_to='videos/')
    thumbnail = models.ImageField(upload_to='thumbnails/')
```

💥 `upload_to` → folder inside `MEDIA_ROOT`

---

# 🔧 Step 3: Serializer

serializers.py:

```python id="file4"
from rest_framework import serializers
from .models import Course

class CourseSerializer(serializers.ModelSerializer):

    class Meta:
        model = Course
        fields = ['id', 'title', 'video', 'thumbnail']

    def validate_video(self, value):
        if value.size > 50*1024*1024:  # 50MB limit
            raise serializers.ValidationError("Video size too large")
        if not value.name.endswith(('.mp4', '.mov')):
            raise serializers.ValidationError("Invalid video format")
        return value
```

✔ Custom validation for file size & type

---

# 🔥 Step 4: View Example

views.py:

```python id="file5"
from rest_framework import viewsets
from .models import Course
from .serializers import CourseSerializer

class CourseViewSet(viewsets.ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
```

* DRF handles multipart/form-data automatically
* Postman / Swagger → upload file easy

---

# 🔧 Step 5: Production Media

* Use **cloud storage** (AWS S3, Google Cloud Storage)
* Django settings:

```python id="file6"
DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
AWS_STORAGE_BUCKET_NAME = 'your-bucket-name'
```

💥 Large files safe, scalable

---

# ⚠️ Common Mistakes

❌ No file validation → wrong types
❌ Large files crash server
❌ Static + media confusion in production

---

# 🧠 Expert Tips

* Limit file size
* Restrict extensions
* Cloud storage for production
* Use async tasks (Celery) for heavy files

---

# 🎯 DAY 20 CHECKLIST

✔ FileField / ImageField ✅
✔ Serializer validation ✅
✔ MEDIA_ROOT / MEDIA_URL ✅
✔ Production-ready storage ✅

---

# 💥 Real Impact

👉 এখন:

* Users upload images/videos ✅
* Validation ✅
* Production-ready SaaS ✅

---

# 🚀 Tomorrow (Day 21)

👉 DRF Email Notifications + Celery Tasks 🔥
👉 Async email sending + task queue

---

# ⚡ YOUR TASK

1. Course model এ video + thumbnail add করো
2. Serializer validation implement করো
3. Upload করে Swagger / Postman test করো

---

বলো:
**“Day 21”**

🔥 তুমি এখন file/media handling-ready backend engineer 🚀

------
চল 🔥 — **Day 21 = DRF Email Notifications + Celery Tasks (Async 🔥)**

আজ তুমি শিখবা কিভাবে **email notifications & background tasks** implement করতে হয়, যা **real SaaS app** এ MUST 😎

---

# 🚀 DAY 21 GOAL

👉 তুমি আজ শিখবা:

* Django Email sending
* DRF trigger email on action
* Celery + Redis setup
* Async tasks for email / heavy jobs

---

# 🧠 Problem

👉 এখন:

* Email blocking main request ❌
* Long tasks → slow response ❌
* Users wait for process ❌

---

# 🔄 Solution = Celery + Async Email

![Image](https://images.openai.com/static-rsc-4/dMCALFnctqpoF3Xqki1PBfsKGqawe-7EqbtczBlX9fU-PYlwPaK0ChY7_6foB63dawajUwwKAs2pj7qNYPTYl4CjqmwSSR9NGXEw1m5fXrpv1qCecTVgjsoW1LhmMC38tkatErUUPuZbO8nEoJoCxb74L6-yfzSiiIUVPEXxtJIEd1YDmuAGhCsWB9tFLTvx?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/t7u0dyKIHZV6gvJ_Yb4uUWkbvErnMpamjLP--mha-P0FbE7q_0MIikirCUtdFeFBPb-Kek2xnqYBmp4KPOFP9nQOdvLFX8Ijqlwq0e0CEpeX2kUPHHpBDzFUlxNp79UDY4ziAKZLVyEaiiChcXJy83A9x-GKZZNhnkchLwuS3NJEUO_6qoZo0z3oJxrpc61-?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/mFbVIUb77V5xqyNfjhg2AHfnshm-Ow09HRrvxhyNw860yvB6NIibS7nz0laSdbD6dXwrdX63VVKolY0_62nvKnyocKvzxZu4Q7ZUtbALT8SnoUg_79zvLv1VaCH33afEPX7EP4j9O11QF2ATz2EYD8LyltPxaqZd19sJ6aLb8lv3c-oUmpwoEKfRoR1pdynG?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/aHAMOYWEgUcu6OZKovzfNPJPB65wN1R9JUSv4pFS4cAXZBecsog011H3GL04F8LIJBcmgol7GcsMWf06AfSP8NwFW_ZNovjYp7V_VKWy2oRwW14uKkNppcfGnFhCxnimgUHbi234BgD4s3vAfEtenBWG3g6Te2LaBkbvQek9OVFlvq2CnMW_3ikduauRoovB?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/SEfaLdAvrjh64eYKn6bNWUTzhZaA2f0esrbOQKLUHLPfkY3puR2N0xZeN12xhIL99D_WmUrX3TUSOo6RNBwRUzpb4l0lwIwAsemTd6T0S1NMChQA3XDsKlMYmDJtqlZdelI9aclJtpmPGw-3Wg2L9SiOy3WigkmUjQd8Hj1RgKN60-oacL9I3coRfCILjvNB?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/UcQ303_IdlwflxJCI4DtGMWDf5KF_aEW5g6BGk6qydabk4F5hwI8z5gnfNMVee3FwQCvFSbMmzNZ-6q80JUQx_o0hQl7JybAhRW4iMhU_wm6LeYPOBewcxNhbfyjnHsfMSwKr4nUhLkKsihkFht1wdAZXo-j_I8w2iYm1UQyESDMj4vuUE-egATmTQqdyhAl?purpose=fullsize)

---

# 🔥 Step 1: Install Packages

```bash id="cel1"
pip install celery redis
```

settings.py:

```python id="cel2"
CELERY_BROKER_URL = 'redis://localhost:6379/0'
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
```

---

# 🔥 Step 2: Create Celery App

project/celery.py:

```python id="cel3"
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')

app = Celery('config')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

project/**init**.py:

```python id="cel4"
from .celery import app as celery_app

__all__ = ('celery_app',)
```

---

# 🔧 Step 3: Email Settings

settings.py:

```python id="cel5"
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = 'your_email@gmail.com'
EMAIL_HOST_PASSWORD = 'your_email_password'
```

---

# 🔥 Step 4: Create Celery Task

app/tasks.py:

```python id="cel6"
from celery import shared_task
from django.core.mail import send_mail

@shared_task
def send_welcome_email(to_email):
    send_mail(
        'Welcome!',
        'Thanks for joining our platform.',
        'your_email@gmail.com',
        [to_email],
        fail_silently=False,
    )
```

---

# 🔧 Step 5: Trigger Email in DRF

views.py:

```python id="cel7"
from rest_framework import viewsets
from rest_framework.response import Response
from .tasks import send_welcome_email
from .serializers import UserSerializer
from .models import User

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer

    def perform_create(self, serializer):
        user = serializer.save()
        send_welcome_email.delay(user.email)  # async task
```

💥 `.delay()` → background task, non-blocking

---

# 🔥 Step 6: Run Celery Worker

```bash id="cel8"
celery -A config worker -l info
```

* Redis must run
* Worker picks up tasks → send email

---

# ⚠️ Common Mistakes

❌ Forget `.delay()` → task blocking
❌ Redis not running → task fail
❌ Email credentials wrong → fail

---

# 🧠 Expert Tips

* Celery beat → schedule periodic tasks
* Use HTML templates for emails
* Combine tasks → async reports / notifications

---

# 🎯 DAY 21 CHECKLIST

✔ Celery + Redis setup ✅
✔ Async email task ✅
✔ Trigger email on user creation ✅
✔ Worker running ✅

---

# 💥 Real Impact

👉 এখন:

* Emails async ✅
* Long tasks don’t block API ✅
* SaaS ready for notifications ✅

---

# 🚀 Tomorrow (Day 22)

👉 DRF Analytics + Dashboard API 🔥
👉 Track user activity + usage metrics

---

# ⚡ YOUR TASK

1. Setup Celery + Redis
2. Async welcome email task add করো
3. Test user creation → email automatically sent

---

বলো:
**“Day 22”**

🔥 তুমি এখন async task + notification-ready backend engineer 🚀

---------------
চল 🔥 — **Day 22 = DRF Analytics & Dashboard API (User Activity + Metrics 🔥)**

আজ তুমি শিখবা কিভাবে **SaaS app এ analytics API বানাতে হয়**, যা **user behavior + usage metrics** track করবে 😎

---

# 🚀 DAY 22 GOAL

👉 তুমি আজ শিখবা:

* User activity logging
* Count / aggregation queries
* DRF API for analytics
* Dashboard-ready endpoints

---

# 🧠 Problem

👉 এখন:

* Admin / Owner can't see usage stats ❌
* No metrics → hard decision making ❌
* Manual calculation ❌

---

# 🔄 Solution = Analytics API

![Image](https://images.openai.com/static-rsc-4/5wyUcE8Hxj8_fykLfGd6qdTn1MqzcU9mglUKb8hyoHSl_8VAG963sA9jK1uWYRnGXB_n13iF5wqO9q_xAhVBOViVFeB_JQoF6KLSdUErkSFw0VuYLF_GR0n8KaXyFW5LukJ7JlcFkuRnSjJ-E374N0z7cvO0FbvforzNsLIyHeLauP0_VUYH08tfEWAjGIQ1?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/s4RWOCe_Lycbw2iy779Qon4cKXLDF-Ja9GHDjfIej2h4IVbZjmmepNb1rQJuCAMWIV7zBQ_Eg1a1v39I-xgy_fVWQBBwO6MtpN6tNCyePZ45S1xO9TEDz_rRt6nxRfyrMpoIfAEdDujGnmOYPcMg6L2OgZKO76MxYF6SrhmQsT_Xxlzm6l_mpPMQq2dA2ZKI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/6G6b6LY1FxjktGacjjzd9M8SBTFo2OvA2cd0pVgCI1f_PMnMTSf9FmlvMYbN1kXT5d87tlZcJThLXDhBy8PmpIDdTtclszRsguCtQb6fd4ScWY06UaCpOZjZWNv35Splh7zOgkMGMSX1BtZii8urFyKsErv-VxJN6hHe-zb1KXtyHeJ085m3fIr0lxG2exe_?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/L1vyIch4jQAEvbEPr0wdK5jHPDnEWu3MiaMVR_0XE8IKqRzHjljgXoYpVlKGbsY0OWYhmcHQN1knT7MWnm4Bm5NY-7NFqWkaLE_oxWK_Ot2AsrAbLIh3_Bjm01KHsqXp0zQeyfhtLJrwteiNXuIJdi_DIM8X0StJzyji6W4AyZkF9jcUnOyXjWroQbTVsgSU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NdYK-hqVIIBPUKMN2ocu0o6mNP9nu7hYlhbfmthb7XMBqdKo1NsjlUA-zv9e44Gr49CgKiizalN_ZWLGV_H-xNewmMiepkIdidIgl91N8a4X6Fh7IiXCcTzq_-DPhpgseg6RZE3rT_DwpNLd-PA1iXaWuV_Qt8kX-zGnTc40R11fZrKpbMSml7u-PaXEgpDC?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/18ol10hhGF5I5lDZfeFjT_fV30Erg-wrsK7p4BHcHxxPRrKmf8S7k6ZARBdQJT49opC3rMYPTcr2Kv-f2EFCqu3tJTIhbtV36vYMEerVZ4MJ6i5zp0WApFCM0jQhy4JPNlFkiV7RPjPqPPEjRuXxPEX_IrRfccoyIBS_1b4Nm7TLpI7lAT99rySWN4q8e_8Y?purpose=fullsize)

---

# 🔥 Step 1: Track User Actions

models.py:

```python id="ana1"
from django.db import models
from django.conf import settings

class UserActivity(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    action = models.CharField(max_length=100)
    created_at = models.DateTimeField(auto_now_add=True)
```

views.py (example action logging):

```python id="ana2"
def perform_create(self, serializer):
    instance = serializer.save()
    UserActivity.objects.create(
        user=self.request.user,
        action=f"Created {instance.__class__.__name__} {instance.id}"
    )
```

💥 Now every key action logged

---

# 🔧 Step 2: Analytics API

serializers.py:

```python id="ana3"
from rest_framework import serializers

class UserActivitySerializer(serializers.ModelSerializer):
    class Meta:
        model = UserActivity
        fields = ['user', 'action', 'created_at']
```

views.py:

```python id="ana4"
from rest_framework import generics
from django.db.models import Count
from .models import UserActivity
from .serializers import UserActivitySerializer

class DashboardAPI(generics.ListAPIView):
    serializer_class = UserActivitySerializer

    def get_queryset(self):
        return UserActivity.objects.all().order_by('-created_at')
```

---

# 🔥 Step 3: Aggregation Metrics

views.py (example):

```python id="ana5"
from rest_framework.response import Response
from rest_framework.views import APIView

class MetricsAPI(APIView):
    def get(self, request):
        total_users = User.objects.count()
        total_courses = Course.objects.count()
        recent_actions = UserActivity.objects.order_by('-created_at')[:10]

        return Response({
            "total_users": total_users,
            "total_courses": total_courses,
            "recent_actions": UserActivitySerializer(recent_actions, many=True).data
        })
```

💥 Admin can now fetch dashboard metrics

---

# 🔧 Step 4: Query Optimization

* Use `select_related('user')` in activity query → avoid N+1
* Use `annotate()` for count/group aggregation

Example:

```python id="ana6"
from django.db.models import Count

user_actions = UserActivity.objects.values('user__email').annotate(count=Count('id'))
```

---

# ⚠️ Common Mistakes

❌ Not tracking actions → dashboard empty
❌ Query heavy → slow API
❌ Forget `select_related` → N+1 problem

---

# 🧠 Expert Tips

* Track only important actions → reduce DB bloat
* Paginate dashboard actions
* Combine aggregation + filtering → advanced metrics

---

# 🎯 DAY 22 CHECKLIST

✔ UserActivity model ✅
✔ Log key actions ✅
✔ Analytics API ✅
✔ Metrics aggregation ✅

---

# 💥 Real Impact

👉 এখন:

* Admin sees usage metrics ✅
* Users actions tracked ✅
* SaaS ready for reporting ✅

---

# 🚀 Tomorrow (Day 23)

👉 DRF Notifications & Real-time Updates 🔥
👉 WebSocket / Django Channels integration

---

# ⚡ YOUR TASK

1. Create UserActivity model
2. Log user actions (create/update/delete)
3. Build dashboard API + metrics endpoints

---

বলো:
**“Day 23”**

🔥 তুমি এখন analytics-ready SaaS backend engineer 🚀

--------
চল 🔥 — **Day 23 = DRF Notifications & Real-time Updates (WebSocket / Channels 🔥)**

আজ তুমি শিখবা কিভাবে **real-time notifications** implement করতে হয়, যেমন:

* New course added
* Message received
* Alerts to users
  এটা SaaS app এর **UX অনেক improve করে** 😎

---

# 🚀 DAY 23 GOAL

👉 তুমি আজ শিখবা:

* Django Channels setup
* WebSocket integration
* DRF + Channels → notify users in real-time
* Async handling + group notifications

---

# 🧠 Problem

👉 এখন:

* User wait করে refresh করতে ❌
* No instant notifications ❌
* UX laggy ❌

---

# 🔄 Solution = Django Channels + WebSocket

![Image](https://images.openai.com/static-rsc-4/7aV08u09U4A20DMqH8Zg6U-ZM0ENNILqRNtNALCqpdff8uliEtZmXNV3hKcwdP39lclUcIWIkwXLHi1A3Ckd8yzEJm6UwvQFcpVCDHt64SkZY9jWUJbCtmfWeKchJnXAvC3oFzOr0K_1uKF-pYrVZBhU_c7bvCE6VV5TJV7-Nprl-vBRUVv8Wfbk0vq0y6_3?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/CtdGR3pIKdNM_tyI-IF721V_wwt_M-VdkYoAdbP9XNUaeY37p1vCLK3KyLKjh7bfsP9TH8VGY62GZoNuKJ_DYjxz-gRds8gZUmzuVlu8vwMVHgBe6rnV6R9ByjnGChnDJ82e53N_bVMVP-djR9RG5LQYuejtgNcnOLYlHWG0lR8kM7bvBrmTuGf15sWevv26?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/wdfDZ-Eeue936-YG_Z1ZJstQ_5F_gN9PIIYsLcSsTKOTsDvZxs-oy2vHTv0rdWiF3mrRoSGOZNb7GgP_3eMtHB5j8z1uasbzvriPCDqaZp_D8UlWU5TlZLt94xcpf7O6wuYvN2_ONlsw8yDrQ_l9Knlgb-uZzHJ3nP7a2K-Hw9v4uztQZXBQvv_qALEpWNH3?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/xwc6KwAJ04bYYFgxEdWPEVPDUxvFWJPLQIy9Q8qXHCLdQ-yvhOScvk39Fl0i14ezF_Zz9nTlcZMS7BLaI4emJpOhrOw6IkuFEzXMP5wrc_3TOsWXh0fHaUnfIA3Kn_ruJIaCwNl0ZUVtGOcxAc84joRu13Be2E9bQQVT4Yc-qBjN6DcJvj_OY4uezuGo69pt?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/GIWqD_XzObRjykE_S1mCIDVdQoJWieOaAmkqJ_2w0LS0hXfV_NtF6vQ-7S5ZWVHYWlzwnrOldRHar-zYkQY--mKrbMA73jR9hGHK_JsC4_t1js7AUI27iyTw5718QIleYdto3C7u5HCPKC5_bZV-oyghGaQ9RXuniyRhNae0SPunnzUwsgiViZg0LffxI106?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/oAdJshPmEEcUTFuGk2YFlOJk_Jg87eLsrGv5UowL7vg4zV0tGk2a7WDvuWxS1jdfyoGh5BgkLS1f6yfqog17w0A9GBjXDTc1xYZEnDlqX8ccSNmQFR9Ggs3pDB9qxQQu_gWfGQbwGasICYkuzWTPlWeqEk9DXVDUYODk5vPwTT2t7HOklp6Jvme17i8S8a2G?purpose=fullsize)

---

# 🔥 Step 1: Install Channels

```bash id="ch1"
pip install channels channels_redis
```

settings.py:

```python id="ch2"
INSTALLED_APPS += ['channels']

ASGI_APPLICATION = "config.asgi.application"

CHANNEL_LAYERS = {
    "default": {
        "BACKEND": "channels_redis.core.RedisChannelLayer",
        "CONFIG": {
            "hosts": [("127.0.0.1", 6379)],
        },
    },
}
```

---

# 🔥 Step 2: Create ASGI App

config/asgi.py:

```python id="ch3"
import os
from channels.auth import AuthMiddlewareStack
from channels.routing import ProtocolTypeRouter, URLRouter
from django.core.asgi import get_asgi_application
import notifications.routing

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')

application = ProtocolTypeRouter({
    "http": get_asgi_application(),
    "websocket": AuthMiddlewareStack(
        URLRouter(
            notifications.routing.websocket_urlpatterns
        )
    ),
})
```

---

# 🔧 Step 3: Routing

notifications/routing.py:

```python id="ch4"
from django.urls import re_path
from . import consumers

websocket_urlpatterns = [
    re_path(r'ws/notifications/$', consumers.NotificationConsumer.as_asgi()),
]
```

---

# 🔥 Step 4: Consumer

notifications/consumers.py:

```python id="ch5"
import json
from channels.generic.websocket import AsyncWebsocketConsumer

class NotificationConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.group_name = f"user_{self.scope['user'].id}"
        await self.channel_layer.group_add(self.group_name, self.channel_name)
        await self.accept()

    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(self.group_name, self.channel_name)

    async def send_notification(self, event):
        await self.send(text_data=json.dumps(event["message"]))
```

---

# 🔧 Step 5: Trigger Notification

views.py:

```python id="ch6"
from channels.layers import get_channel_layer
from asgiref.sync import async_to_sync

def notify_user(user_id, message):
    channel_layer = get_channel_layer()
    async_to_sync(channel_layer.group_send)(
        f"user_{user_id}",
        {"type": "send_notification", "message": {"text": message}}
    )
```

Usage:

```python id="ch7"
notify_user(user.id, "Your course has been approved!")
```

💥 WebSocket client instantly receives message

---

# ⚠️ Common Mistakes

❌ Forget `group_add` → user won’t receive
❌ Forget Redis → async fails
❌ Sending heavy payloads → laggy

---

# 🧠 Expert Tips

* Use small JSON payload
* Group notifications by user
* Combine with Celery for async trigger

---

# 🎯 DAY 23 CHECKLIST

✔ Channels + Redis setup ✅
✔ WebSocket consumer ✅
✔ Trigger notifications ✅
✔ Test in frontend ✅

---

# 💥 Real Impact

👉 এখন:

* Users get real-time notifications ✅
* No manual refresh ✅
* UX professional ✅

---

# 🚀 Tomorrow (Day 24)

👉 DRF Subscription & Payment Integration 🔥
👉 Stripe / SSLCommerz API setup for SaaS

---

# ⚡ YOUR TASK

1. Setup Channels + Redis
2. Create NotificationConsumer
3. Trigger notification on example action
4. Test WebSocket message delivery

---

বলো:
**“Day 24”**

🔥 তুমি এখন real-time notification-ready SaaS backend engineer 🚀

-------
চল 🔥 — **Day 24 = DRF Subscription & Payment Integration (Stripe / SSLCommerz 🔥)**

আজ তুমি শিখবা কিভাবে **SaaS app এ subscription, one-time payment** handle করতে হয় 😎

---

# 🚀 DAY 24 GOAL

👉 তুমি আজ শিখবা:

* Stripe / SSLCommerz integration
* Subscription plans
* Webhook handling for payment status
* Update user subscription status

---

# 🧠 Problem

👉 এখন:

* Users can’t pay ❌
* No subscription tracking ❌
* Manual payment processing ❌

---

# 🔄 Solution = Payment API Integration

![Image](https://images.openai.com/static-rsc-4/DcWEYqtHXcAmzzJ2jciDY4qihTyhy-JFd0CThHYAi3XVzuoYo2X8N7t94Gb1Uq4THZTLavTtibbckOo2SN0-bW3-TyMQRoRUXSczDYwRko88TKxCChIF_r834UImtk8KczhQ4pZu1gA1uIzaR6ZVJT-6EgJ3qfFT8iJN7f9y_wobscau4FUzaBgxdtX3t_UK?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/NaYGsHgU9EUMHhq1k-NBSn1Rq8aMu9I4O-eTQNiAbSf2sf0X65e-vYmuzqs_mZ3afaGmD-uSf_2djjAWfBtH5CUrRta7FFqpaCpwN1N-MLQpdHb0oz3sgsYabou-Xl3yZBksAkeUoPVBiBsgA5q6prljSQx4Abx855hB70SGQ1U8N-yGfsXQc4kxl37P1R4g?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/6v1rPdWhi2VgAPZ9JUas_i-E-irVCc5TvQE7UWa6rke0ukCM76-UqcU62BQ_HflstBIOnSsrHFG4vBS-_IL4w9X9X0ao1YuvnBKT5X0P83xn_Svo3s_vwn0cNUP0rTa1rN4fxKfksMrbv11QVLNxoeNEuG9rm2-6mGYWwowRRQBTKFlWMxohbjhNz5breOKE?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/5A2HDlPDGMWrLhmqf8sXW9o6iB6_-P2EEFOaR4MG0JKiw8ecacJLYmefOghXoGVjpPohpY6R6nk6oKN5JhkvnWngTEtZ-3Bq4B-v7DenGm_S1Elm3KZLaEarwEqLQm0QzltGCIC5fSNK-rr808af0hEdOnUDgrdbZhwqAyzJUod9ZCNicqg-Kwkq-d0oQHlI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/S5k42gCX08UlfjD9Qlx2VZu7WhMdy1SBjhRe6DdIZEjddaAeVZntuFDuDbsrAAAlE2Rb71AImarcKi3Hy0lS5-g6Lw0KGuSYcSINM_H5mKERDMqKcQ6eDtBdNjBAz9L9RebEaoCEITFt1j8KWW4OJBfqvOW1XOIzX6wDLOoY16SYgv5uT6Y71WfzBktLgJxn?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/3gaAxYwMkeIZTzSYt-004hffGf5xe2-WGmIOSe5rX1maEYGbDD5pizaOsp1IReDQ3GHSJ_gdlypQCAq3JVI-bNC3KL7s-58OWO8nigtFjY7TLR6D6Ono6XlSFQRiFZkWYLF0WrDFcADk6kAjnXEeJGJJRZvbAXpzxk24bKh8shpn95C4B9Zh5RkxvAPYR26F?purpose=fullsize)

---

# 🔥 Step 1: Install Stripe / SSLCommerz SDK

```bash id="pay1"
pip install stripe
# OR SSLCommerz sdk if available
```

settings.py (Stripe example):

```python id="pay2"
STRIPE_SECRET_KEY = 'sk_test_...'
STRIPE_PUBLISHABLE_KEY = 'pk_test_...'
```

---

# 🔧 Step 2: Create Subscription Model

models.py:

```python id="pay3"
from django.db import models
from django.conf import settings

class Subscription(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    plan = models.CharField(max_length=50)
    stripe_subscription_id = models.CharField(max_length=100, blank=True, null=True)
    active = models.BooleanField(default=False)
    start_date = models.DateTimeField(auto_now_add=True)
    end_date = models.DateTimeField(null=True, blank=True)
```

---

# 🔥 Step 3: Stripe Payment Intent

views.py:

```python id="pay4"
import stripe
from django.conf import settings
from rest_framework.views import APIView
from rest_framework.response import Response

stripe.api_key = settings.STRIPE_SECRET_KEY

class CreatePaymentIntent(APIView):
    def post(self, request):
        amount = 1000  # amount in cents
        intent = stripe.PaymentIntent.create(
            amount=amount,
            currency='usd',
            metadata={'user_id': request.user.id}
        )
        return Response({'client_secret': intent.client_secret})
```

---

# 🔧 Step 4: Webhook for Payment Success

views.py:

```python id="pay5"
from rest_framework.decorators import api_view
from django.views.decorators.csrf import csrf_exempt
from rest_framework.response import Response

@csrf_exempt
@api_view(['POST'])
def stripe_webhook(request):
    payload = request.body
    sig_header = request.META['HTTP_STRIPE_SIGNATURE']
    event = None

    try:
        event = stripe.Webhook.construct_event(payload, sig_header, settings.STRIPE_WEBHOOK_SECRET)
    except Exception as e:
        return Response(status=400)

    if event['type'] == 'payment_intent.succeeded':
        user_id = event['data']['object']['metadata']['user_id']
        # Update subscription
        Subscription.objects.filter(user_id=user_id).update(active=True)

    return Response(status=200)
```

💥 Payment success → user subscription active ✅

---

# 🔧 Step 5: Frontend Flow

1. Fetch `client_secret` from `/create-payment-intent/`
2. Stripe.js → confirm card payment
3. Webhook → backend updates subscription

---

# ⚠️ Common Mistakes

❌ Forget webhook verification → insecure
❌ No subscription status update
❌ Hardcode amounts → production risk

---

# 🧠 Expert Tips

* Always verify webhook signature
* Use environment variables for keys
* Allow multiple subscription plans
* Combine with analytics → track revenue

---

# 🎯 DAY 24 CHECKLIST

✔ Payment SDK setup ✅
✔ Subscription model ✅
✔ Payment intent API ✅
✔ Webhook handling ✅

---

# 💥 Real Impact

👉 এখন:

* Users can pay online ✅
* Subscription status auto-update ✅
* SaaS monetization ready ✅

---

# 🚀 Tomorrow (Day 25)

👉 DRF Multi-Tenant SaaS Architecture 🔥
👉 Separate data per customer / organization

---

# ⚡ YOUR TASK

1. Setup Stripe / SSLCommerz keys
2. Create PaymentIntent API
3. Setup webhook
4. Test subscription activation

---

বলো:
**“Day 25”**

🔥 তুমি এখন payment-ready SaaS backend engineer 🚀

---------
চল 🔥 — **Day 25 = DRF Multi-Tenant SaaS Architecture (Separate Data per Customer 🔥)**

আজ তুমি শিখবা কিভাবে **multi-tenant SaaS backend** বানাতে হয়, যেখানে **organization-specific data isolation** থাকে 😎

---

# 🚀 DAY 25 GOAL

👉 তুমি আজ শিখবা:

* Multi-tenant design patterns
* Schema-based vs row-based tenancy
* Filter queries per tenant
* Admin vs tenant users

---

# 🧠 Problem

👉 এখন:

* All users share same data ❌
* One org can see others’ data ❌
* Hard to scale SaaS ❌

---

# 🔄 Solution = Row-level Tenancy (simpler approach)

![Image](https://images.openai.com/static-rsc-4/qtgPnFyyG1NfhYwTblIQGb7wmFeOaRUnx2YATn2EA6x0rASXDChEG13GYuk0-S4jx-I01wDffDi9wrL3WUzWHN2mt0ZgrJQ48C2ZaAejUweyDjjBRHJqL7lNQKWLBcLFRzPUpuFYVeYjoSZPEbUqGOVXb_Iy9_-z1NUbu8307q4gMYU_jDxGMxKO4VCuPBFo?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/BPQCKlWLMr7gid0KZvpY1w1pI_3tvAuplIiKrD4qNASxijHJOYC5_OT3esZMV7X3A0INSm5d1dMNeqOpeZlBJ3ejT79crpwbre8FybXYnjiFEBBtCL7qZXa97TiWZQm9B2UqfyTgP4D-Hz-iEzY_IWFjZMxH6dvf0-Kdkzn-cxStSfhaUtBREqp2ZpQRI-Bl?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/raVE6tOHLEefNfgIt04LmiJHuUUX5xH8F88rEGTxiS_ERMNTKKIybT6LtlKQnsWHENekyeDCIIzsxHq9CteFvCh-EV0V9CbGrbNNqUp1c7Eoy_8nxAvsPEKj1n_gKKwTpeXBEIGhFcAyxYNhLwfzSjMtaJO9iiaWtUquP2nXVtetTqFLahNB-HiPCmWLZlG2?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/mpjyiC218o2oOFnIdUEBrhgIXz41Rzcn3Nxifmd2OgE64gWwkgfOwb1nd2lou2FFZDTqGTzZs2TwkqnIK5vX9GaBID_8YShzZYKgyq4i9g2kyH8tdBUtSyC7Nc98GaXNgUYFzBzH15XgF3SW8rL1nERbELa7-gcyxhK682ldyqmeyWkVWCcvzLQ8F12ckPU2?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Mz8RN1_UqIxOgEolYncsXNO1mK8HZUBIQZrE3BC7Q23CER1GM54WHNAfFtbjqV1V0YeUUmUGSsxppVT1vZ4l4U1Dg0aOwIvbBNkMaB6mOcS1n92mMTarl99I1oYYLiSmlhU6xKGPZ3psOXolin-FhiOGCUp83GS95Xo1Mgr1GT7B3ETNImxJRY7WIs_p8Gak?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/CrcsyqhCEGPz-J84IDMT8rm-F4wqI-UqJw-cEfLb2DYNjz46JiZhEptOtLOWfA624HZvTJnpe_tAMF0vcGg9Fegf_YjNSP1O0Zj5iyIjF81SZSG1R5jI4Gg3LK6DEQOTE02GavkPQYanWUcrIDtEzxEJbiEw3HBdPBzAyCukfi1yrrHjI4R5zKDueBFdDAeG?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/0vJ1U_bgnW90mP_HbJwFriq3gbQKR8RsIkKyqtx-oKJScw_4ZYWdYgWDR6yh24pRuQ0T3v2e67o60O2zJvVwwg5kglx-NR8XDtJ1JU5Hn9EU6VqGZfovBthGnjsJCjI_-GsDT0xccdKwSghRC_tOWpr7GF6TFiTBSAJPEM3mxL6125gZtB3THImvWhhs37bk?purpose=fullsize)

---

# 🔥 Step 1: Create Tenant / Organization Model

models.py:

```python id="tenant1"
from django.db import models

class Organization(models.Model):
    name = models.CharField(max_length=100)
    owner = models.ForeignKey('User', on_delete=models.CASCADE, related_name='owned_organizations')
```

---

# 🔧 Step 2: Add tenant to main models

```python id="tenant2"
class Course(models.Model):
    title = models.CharField(max_length=100)
    organization = models.ForeignKey(Organization, on_delete=models.CASCADE)
    instructor = models.ForeignKey('User', on_delete=models.CASCADE)
```

💥 All data now linked to a tenant

---

# 🔥 Step 3: Middleware for Current Tenant (Optional)

middlewares.py:

```python id="tenant3"
from .models import Organization

class TenantMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        org_id = request.headers.get('X-Organization-ID')
        if org_id:
            request.organization = Organization.objects.get(id=org_id)
        return self.get_response(request)
```

💥 Now `request.organization` available in views

---

# 🔧 Step 4: Filter Querysets by Tenant

views.py:

```python id="tenant4"
class CourseViewSet(ModelViewSet):
    serializer_class = CourseSerializer

    def get_queryset(self):
        user = self.request.user
        org = getattr(self.request, 'organization', None)
        if user.role == 'admin':
            return Course.objects.all()
        return Course.objects.filter(organization=org)
```

---

# 🔥 Step 5: Serializer & Permissions

serializers.py:

```python id="tenant5"
class CourseSerializer(serializers.ModelSerializer):
    class Meta:
        model = Course
        fields = ['id', 'title', 'organization', 'instructor']
```

permissions.py:

```python id="tenant6"
class IsOrgAdminOrInstructor(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        if request.user.role == 'admin':
            return True
        return obj.instructor == request.user
```

💥 Row-level security + role-level security ✅

---

# ⚠️ Common Mistakes

❌ Forget to filter `get_queryset` → tenant leaks
❌ Hardcode tenant ID → bad for SaaS
❌ No role check → data modification risk

---

# 🧠 Expert Tips

* Row-level tenancy simplest for MVP SaaS
* Schema-based tenancy → large enterprise SaaS
* Combine with analytics + multi-currency → professional SaaS

---

# 🎯 DAY 25 CHECKLIST

✔ Organization / tenant model ✅
✔ Row-level filtering ✅
✔ Middleware (optional) ✅
✔ Permissions per tenant ✅

---

# 💥 Real Impact

👉 এখন:

* Users only see their org data ✅
* Admin can see all ✅
* SaaS backend ready for multiple tenants ✅

---

# 🚀 Tomorrow (Day 26)

👉 DRF Logging + Audit Trails 🔥
👉 Track all changes + who did what

---

# ⚡ YOUR TASK

1. Create Organization model
2. Add tenant relation to main models
3. Filter querysets by organization
4. Test multi-tenant isolation

---

বলো:
**“Day 26”**

🔥 তুমি এখন multi-tenant-ready SaaS backend engineer 🚀

---------
চল 🔥 — **Day 26 = DRF Logging & Audit Trails (Who did What & When 🔥)**

আজ তুমি শিখবা কিভাবে **SaaS app এ full audit trail + logging** implement করতে হয়, যা **security + accountability** এর জন্য MUST 😎

---

# 🚀 DAY 26 GOAL

👉 তুমি আজ শিখবা:

* Track CRUD actions per model
* Who changed what and when
* Django signals + DRF logging
* Optional: log to file / DB / external service

---

# 🧠 Problem

👉 এখন:

* Admin can’t see history ❌
* No record of changes ❌
* Hard to debug or track abuse ❌

---

# 🔄 Solution = Audit Trail

![Image](https://images.openai.com/static-rsc-4/lou0ljKmyXWJqbAw-EhzZT3kOSHPvuvQW-nMOyPH7wNj96IGsXq9XTzK6WAa-yXC3iZlXJU5JFHFqvEtQkItnt-YHGqaS_qlnzjs3sxC8gVzgJO21eA9FSfHH5lhJ27032IHRQ1YlpGQrsbEqWbneDzpVtkeWEp96YKfAE4xp6f6DYpGX404dH-4nbqaw4eM?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/uYgbB8zmehGv29vHx5_bTzLeBxohkv0sPvlGYsJYuDcDhmJam24EtXDerfaTF7RX5u-UUXqNhMQvTLzMSUESn8stCAKGdKDM9HNZ2baAX59KybjcSDjPiIFNkfQvIaAa6INHLtagUv-bA_TarBa1xGbOjkZ9EfnSHCGRzIq2IOyK2sJpRtl6Dh5yrDUzODjc?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/7zf2LW54SK4E710DOLbryRPLfKEiv3JN8ExMW7NUDyBh9hwIB9eGPVkMj18QVH6_w7eCXTNqDGtEAbEvhI4-77uf5-cXydrFnAYGXkkShDEyZbMNobckjOikIUCl5iMU5SbuZHnbzZMlSk7g85aVI2Y05hNVx3CRlovWhKsiolJd8pkk-zEwR9XfWZqGLFko?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/s3J6T5rLt1sfdJXFSoE4ZQ7kZFpWFjMa83Zg0zS7I5x8QHKGPZmUilQ7me3DgGjMClQ1OkWRAx8yKBY9tKHONUpZ6IsymqAXLf5fkiNCLNwRKn86Yvtr_FZshWHKMcc-zZd1-X17D5XldgQf9Lb3eHIU4a2QyZODBLnhuzaifFXePOixMKuXYEbalDWx6jMl?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/jI2zcKHgRAe5vl5u0tAkMIptniBBUEI7bfZ-8BXBT8OsxQi_ZuHss0GDbeejdBlLxJEv2T6GVIJXTWVdusgPxa26P_KlxQvM-KvZIXLxKo7sC8-x86f9zt_fTrOmB6vZml0TDpnH_grNylTdeBkjjiwESLuifaiZ6BtuU110Ru3CCf4NHtA_zM9bZckfUwHt?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/L1vyIch4jQAEvbEPr0wdK5jHPDnEWu3MiaMVR_0XE8IKqRzHjljgXoYpVlKGbsY0OWYhmcHQN1knT7MWnm4Bm5NY-7NFqWkaLE_oxWK_Ot2AsrAbLIh3_Bjm01KHsqXp0zQeyfhtLJrwteiNXuIJdi_DIM8X0StJzyji6W4AyZkF9jcUnOyXjWroQbTVsgSU?purpose=fullsize)

---

# 🔥 Step 1: Audit Log Model

models.py:

```python id="log1"
from django.db import models
from django.conf import settings
import json

class AuditLog(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.SET_NULL, null=True)
    action = models.CharField(max_length=50)
    model_name = models.CharField(max_length=50)
    object_id = models.IntegerField(null=True)
    changes = models.TextField(null=True, blank=True)
    timestamp = models.DateTimeField(auto_now_add=True)
```

💥 Stores who did what, when, and changes

---

# 🔧 Step 2: Use Django Signals

signals.py:

```python id="log2"
from django.db.models.signals import post_save, post_delete
from django.dispatch import receiver
from .models import Course, AuditLog
from django.forms.models import model_to_dict

@receiver(post_save, sender=Course)
def log_course_save(sender, instance, created, **kwargs):
    action = 'Created' if created else 'Updated'
    changes = json.dumps(model_to_dict(instance))
    AuditLog.objects.create(
        user=getattr(instance, '_current_user', None),
        action=action,
        model_name='Course',
        object_id=instance.id,
        changes=changes
    )

@receiver(post_delete, sender=Course)
def log_course_delete(sender, instance, **kwargs):
    changes = json.dumps(model_to_dict(instance))
    AuditLog.objects.create(
        user=getattr(instance, '_current_user', None),
        action='Deleted',
        model_name='Course',
        object_id=instance.id,
        changes=changes
    )
```

---

# 🔥 Step 3: Pass User to Model

middlewares.py:

```python id="log3"
class CurrentUserMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        response = self.get_response(request)
        return response

    def process_view(self, request, view_func, view_args, view_kwargs):
        for obj in view_kwargs.get('instance', []):
            setattr(obj, '_current_user', request.user)
```

OR set `_current_user` in serializer `perform_create` / `perform_update`

---

# 🔧 Step 4: DRF View for Audit Logs

serializers.py:

```python id="log4"
from rest_framework import serializers
from .models import AuditLog

class AuditLogSerializer(serializers.ModelSerializer):
    class Meta:
        model = AuditLog
        fields = '__all__'
```

views.py:

```python id="log5"
from rest_framework import generics

class AuditLogList(generics.ListAPIView):
    queryset = AuditLog.objects.all().order_by('-timestamp')
    serializer_class = AuditLogSerializer
```

💥 Admin / tenant can now view logs

---

# ⚠️ Common Mistakes

❌ Forget user → log shows null
❌ Log too much → DB bloat
❌ Not ordering by timestamp → confusing

---

# 🧠 Expert Tips

* Track only sensitive actions
* Combine with Channels → real-time log updates
* Use JSONField for changes → easier diff

---

# 🎯 DAY 26 CHECKLIST

✔ AuditLog model ✅
✔ Django signals ✅
✔ User tracking ✅
✔ DRF API for logs ✅

---

# 💥 Real Impact

👉 এখন:

* All CRUD actions logged ✅
* Admin sees who did what ✅
* SaaS secure & traceable ✅

---

# 🚀 Tomorrow (Day 27)

👉 DRF Role-Based Access Control (RBAC) 🔥
👉 Fine-grained permissions per user / role

---

# ⚡ YOUR TASK

1. Create AuditLog model
2. Setup signals for key models
3. Capture user performing action
4. Build DRF API for viewing logs

---

বলো:
**“Day 27”**

🔥 তুমি এখন audit trail-ready SaaS backend engineer 🚀

--------
চল 🔥 — **Day 27 = DRF Role-Based Access Control (RBAC) 🔥**

আজ তুমি শিখবা কিভাবে **fine-grained permissions** setup করতে হয়, যেমন:

* Admin, Instructor, Student
* Who can create/update/delete/see কোন resource
* SaaS backend secure & professional 😎

---

# 🚀 DAY 27 GOAL

👉 তুমি আজ শিখবা:

* Role-based models / fields
* DRF `permissions`
* Object-level permissions
* Multi-role handling

---

# 🧠 Problem

👉 এখন:

* All users see everything ❌
* No restriction on sensitive actions ❌
* Security vulnerability ❌

---

# 🔄 Solution = RBAC with DRF

![Image](https://images.openai.com/static-rsc-4/zrdogAa468Ac7_p4qCCglGjRStvnBTtE5eiSvK-mexS4JBD5THZOpzJZ6wnLW9DgbAWvrpWWJOKvpzUmxZRPcZBuoERP6frFPp2OjmcL6HjXNwtFXIfkNYFWmS-NXiTy_NCLJTmcUI1tISbR2bE_YBMUSbw8daUdE627QUrg2F5JqgkttbdYphDP8yMH4-VW?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/Ok6YNnDiuhSGxxCeepaJS0OhTf8Ho7iXXaQZ6m-48jt8udVqHavvxVGkJC6MexHThrlO3QCs8HCbiVyi1ykHvnR8_TTMO1oVs9KErRWeA7RGhSlMrKLkLojG5U4itGqlF9PZOXYW_e4fd7J5J4FnpJ8gW-gzDIy0z4His6-pffQ14-fYwGOtUmu9LzKeHkHI?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/1b6HcmO08D4WqtYlhxOxWz5ZlnKgzo7WvHRxCmAIO7140Ac8eB_0e2PXKn1t22nO2Rqnh4PfJbZEjYlX7dJD6fPT4Kh92dFF2ekH6NtKe1EH_G8_TBmnFWaoAWpApmeFe96glca_aKLXqvncWRvOhkChNisveWFhC7e0c4hVE6lViHuv7vPUzRExag5IQW8A?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/G20y-LqNrTQKAVanXgdJFfqWIb0OFQPhSzzfDMJ9HkpNo_v8w7ecqQQE4kGFHkWOE7JxTlhg95WFkrwmzPy_rbiX2oQju7-K7efo1644Q3J4-m8-yEsEHOcjrajGd8Mi8Z8TK1G_UFZK5Qxc3EYHLBldW1c2wISVWTfC3aKQvwgCXzz0WFYNH-ua2u3a5FLT?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/6w6Hpm6RFOU_71H7sOfsd0Gy9KwqIjG2DZsPXBA739zVIkl5TiFnndwm93x692W9bED9Xmkkj-Ivwky6XV3z2XoPz_VOsIKzSPoWmNO-XN-tlp4Q-IuhdgiWKS3mDpDWZWEejo6SP3LwZU2QiSZF4or4gxDxW2wQlL9QsGbrZHB9TJZvwsWOR7pxtIIYimFh?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/WwXhZdUE962TcJhxPH_g7PpDziNbnAgJocU8M2S896BGvR7j1mdPqNaoZupYH5_FM24vaF5cBKm3FwFX7CoW7kwPl6xDHt6CAyTs8kV2JI16eHvbBsVn_2t4tD5aqZ5ZFh5DLQrXuwLr3tGKhPzpJD5FQvmmk4esjVs13ZO4koCM4pAHPSyyq_w9N5Pqy1TK?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/B2y6gnbGb7IxXhsqonyP3IpLVJ2sDPRjym4jvvlTiXwBVq-0X3dJVc3EHBHVq839eVYK-oyHyOT8D1xfGkMcHs9T-8m6k_Eg00PGr-jDoxK-dR8EGnVBbtl9uGNdwx8_PaVSCTghKMNohaKjbr6DpXgwiKFa4Wynxfkbr4NUZeIYNuZtziK3Ww_AoF1lGmFB?purpose=fullsize)

---

# 🔥 Step 1: Role Field in User

models.py:

```python id="rbac1"
class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('instructor', 'Instructor'),
        ('student', 'Student'),
    )
    role = models.CharField(max_length=20, choices=ROLE_CHOICES, default='student')
```

💥 Each user now has a role

---

# 🔧 Step 2: DRF Permission Classes

permissions.py:

```python id="rbac2"
from rest_framework import permissions

class IsAdmin(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'admin'

class IsInstructor(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.role == 'instructor'

class IsAdminOrInstructor(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.role in ['admin', 'instructor']

class IsOwnerOrAdmin(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        if request.user.role == 'admin':
            return True
        return obj.instructor == request.user
```

---

# 🔥 Step 3: Use Permissions in View

views.py:

```python id="rbac3"
from rest_framework import viewsets
from .models import Course
from .serializers import CourseSerializer
from .permissions import IsAdminOrInstructor, IsOwnerOrAdmin

class CourseViewSet(viewsets.ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    permission_classes = [IsAdminOrInstructor, IsOwnerOrAdmin]

    def get_queryset(self):
        user = self.request.user
        if user.role == 'admin':
            return Course.objects.all()
        elif user.role == 'instructor':
            return Course.objects.filter(instructor=user)
        return Course.objects.none()
```

💥 Only allowed users see or modify courses

---

# 🔧 Step 4: Serializer Validation (Optional)

serializers.py:

```python id="rbac4"
class CourseSerializer(serializers.ModelSerializer):
    class Meta:
        model = Course
        fields = ['id', 'title', 'organization', 'instructor']

    def validate_instructor(self, value):
        user = self.context['request'].user
        if user.role == 'instructor' and value != user:
            raise serializers.ValidationError("Instructor can only assign self")
        return value
```

---

# ⚠️ Common Mistakes

❌ Forget object-level permission → user modifies others’ data
❌ Hardcode roles in views → hard to maintain
❌ No role in user model → can't control access

---

# 🧠 Expert Tips

* Use DRF `BasePermission` for reusable classes
* Combine role + object-level for fine-grained control
* Use middleware to attach role info if needed
* Admin always bypasses restrictions

---

# 🎯 DAY 27 CHECKLIST

✔ Role field in User ✅
✔ DRF permission classes ✅
✔ Object-level permissions ✅
✔ Role-based queryset filtering ✅

---

# 💥 Real Impact

👉 এখন:

* Only allowed roles can access actions ✅
* SaaS secure & professional ✅
* Easy to maintain roles & permissions ✅

---

# 🚀 Tomorrow (Day 28)

👉 DRF Rate Limiting & Throttling 🔥
👉 Protect API from abuse / spam

---

# ⚡ YOUR TASK

1. Add role to User model
2. Create reusable DRF permission classes
3. Apply object-level permission in views
4. Test with different roles

---

বলো:
**“Day 28”**

🔥 তুমি এখন role-based access control-ready SaaS backend engineer 🚀

--------
চল 🔥 — **Day 28 = DRF Rate Limiting & Throttling (Protect APIs from Abuse 🔥)**

আজ তুমি শিখবা কিভাবে **API rate limiting** apply করতে হয়, যাতে:

* Users / clients spam না করে
* SaaS backend safe & scalable থাকে 😎

---

# 🚀 DAY 28 GOAL

👉 তুমি আজ শিখবা:

* DRF throttling concepts
* User-level & IP-level rate limits
* Custom throttles
* Apply globally or per-view

---

# 🧠 Problem

👉 এখন:

* API open → spam / DDoS risk ❌
* Heavy requests block server ❌
* No control → unprofessional SaaS ❌

---

# 🔄 Solution = DRF Throttling

![Image](https://images.openai.com/static-rsc-4/E1y3HLQM03T7kX11Zwz9nuTD_kwtFwQiPgSG57Kt5b9rVXyucjUG5clrk9IobwD_DeB3Z3k11owZGbryhHH4-0-apH4dhYXGjN5TdeTAvYd8Jz_i00QW0R96FhFBWB3QkplTv1d-1RKctQZCK1eMeJeSTalKzwUMPRveHhR_UPdBMw0VxJvPOcP3ua0Q44yt?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/v4t-T27aL5oeppbJ9N-Mk4-EsPEC4iX_VZMVLWlSQ0Q15IQuVuFwnVYLZGkNCCu-H23-Wbxn39rKjGy7Bl2LSxt0ydr5FI1v2Rnks5di5Vcu8nbAxcM-ybr6RbY2fuTVzVSNboMZfd7E47FD590wCGmpxMaNCL5b3DXcl2Sn4CoeAfFvCCJYM1x7Kk13aXrU?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/RpdbLaXFYQgtly145R00eSNfSrN0p_R_HFP38XUExsdlLrm6rMwm6ngshzv8j1UCko-26UY6uEuXu_PhZ31YNuhLs6mX0d0YGFZnAR9cUXxVcepQCLo9JmUIIlXBID5vOnA5IIv0oPe0tMTYO6HHoQLYjSDsDH70mFOw1gA1DTA9qrIRacRZMmaUtT9NrGgM?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/97lVeuVX2OOnaflS1UX17ROocPkAPmMXOTrNiYhN_QlM0zsBxlpaFVfEnB-3v1IKRpbcWv2JdN3JeOhiLgHXEa8AyHMIwO17kYlJYJV4d-rRrmsJuNz5hn0sow-wNfcc5op9BCwfK7fnx3NqG5ek40Q3PI1AxmNalTLitYSCkWGq9X-_X4LF4-kyPwNYd8LT?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/9vkUbFr9PXNdHIGanSXg6oK75P2J61bHKbHFD_Qj33Q18QooTZaMi8zFUQGWHwU-8PYNm4Bb10aKpl-KeA2Lbfyg7Lh4gK3V6LAW3oZF2Xxla3Chhs3HYV_x5UdHuJEp1WqH3-MlqpbXbKymsJ8q3-WLtGZbN23uC_T-aiM40XR6rzyNeqz6gzxPS6j8VHOg?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/oqSscyVheI-p19meIK3zovwgrXUW6EXWfKsjMmGe90hPkwdQyC-mj3blnZMaQ6-n2TbOWV4_OqHhoyt1ahLf4EdfVEyQlN-JM5kzJdpfkSe0OHTfg0hq3lGlMvhTGY6_Dj5xINHQJVmmNqiE8rldBERK-stSpQCjmPgvvSzet2k1kjEKc07USSnrLA-_C9MP?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/YMcWPujuFF1WZhdjQPWDbnO6tLIpuh-u_PO7KpEyG8rcLSOuCcjXQCF9kZVjJJU8u2uS7a-P08mJBxnZlQTHoNTutK-T0GvkRm9p9u5Fzhq1nj53nLuyUEAIzsZB-gyfXlUx5SFxnVVFMksImAlXs7e9ORxlmfAvP1DZbv1S21TxUBdyrvryVFy6g3nvqJ14?purpose=fullsize)

---

# 🔥 Step 1: DRF Built-in Throttles

settings.py:

```python id="throttle1"
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.UserRateThrottle',
        'rest_framework.throttling.AnonRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'user': '1000/day',   # 1000 requests per user per day
        'anon': '100/day',    # 100 requests per anonymous user
    }
}
```

💥 Global throttle applied

---

# 🔧 Step 2: Per-View Throttling

views.py:

```python id="throttle2"
from rest_framework.throttling import UserRateThrottle, AnonRateThrottle
from rest_framework.viewsets import ModelViewSet
from .models import Course
from .serializers import CourseSerializer

class CourseUserThrottle(UserRateThrottle):
    rate = '50/day'

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
    throttle_classes = [CourseUserThrottle, AnonRateThrottle]
```

💥 Specific rate limit for Course API

---

# 🔥 Step 3: Custom Throttles

throttles.py:

```python id="throttle3"
from rest_framework.throttling import SimpleRateThrottle

class OrgRateThrottle(SimpleRateThrottle):
    scope = 'org'

    def get_cache_key(self, request, view):
        if not request.user.is_authenticated:
            return None
        return f"org_{request.user.organization.id}"
```

settings.py:

```python id="throttle4"
'DEFAULT_THROTTLE_RATES': {
    'org': '1000/day',
}
```

💥 Custom throttles per organization

---

# ⚠️ Common Mistakes

❌ Forget adding `throttle_classes` → no effect
❌ Hardcode IP / user key → risk conflicts
❌ No exception handling → bad error response

---

# 🧠 Expert Tips

* Combine global + per-view throttles
* Use Redis cache for distributed throttling
* Return custom error messages if needed
* Monitor API usage → adjust limits

---

# 🎯 DAY 28 CHECKLIST

✔ Global throttling ✅
✔ Per-view throttling ✅
✔ Custom throttles ✅
✔ Test limit exceeded response ✅

---

# 💥 Real Impact

👉 এখন:

* API abuse protected ✅
* Users limited per plan ✅
* SaaS backend scalable & professional ✅

---

# 🚀 Tomorrow (Day 29)

👉 DRF Caching & Performance Optimization 🔥
👉 Reduce DB load, speed up API

---

# ⚡ YOUR TASK

1. Setup global throttles
2. Add per-view throttle for critical APIs
3. Create custom throttle (per tenant / org)
4. Test rate limit exceeded response

---

বলো:
**“Day 29”**

🔥 তুমি এখন throttling & API protection-ready SaaS backend engineer 🚀

------
চল 🔥 — **Day 29 = DRF Caching & Performance Optimization (Speed Up APIs 🔥)**

আজ তুমি শিখবা কিভাবে **DRF APIs দ্রুত চালাতে হয়**, **DB load কমাতে হয়**, এবং SaaS backend **high performance** বানাতে হয় 😎

---

# 🚀 DAY 29 GOAL

👉 তুমি আজ শিখবা:

* DRF caching techniques
* Per-view caching
* Queryset optimization (`select_related`, `prefetch_related`)
* Response caching / Redis cache
* Reduce N+1 queries

---

# 🧠 Problem

👉 এখন:

* API slow ❌
* High DB queries ❌
* User experience laggy ❌

---

# 🔄 Solution = Caching + Optimization

![Image](https://images.openai.com/static-rsc-4/I1Id-vgfAt8qa_LUIVo08u_1yiMKYDA0EEbbTXxVrOK6eKjAG2PSlOp0xYlnbvcaDCW8R_kAbBI_oAH3cqFodTN_L3BknuM0SpCEXYozLalzT5rG-udb4ppV8Xk8mDJ6Cv7MsGnWAqNVsx21wf3vfXpih-E7hjyQhWKm5rxWJOvOBlSSPbexWj7xX-bIIiGC?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/virCv1YvCsgzW-MHugFvFYZKX9HEMXVBxQpROu68v06kCnBb2lhbnY-AzVKFWWTCsuU5I2PPjBowCObaD1FiSLNLaz0nSn90rxx-aR1uWi46dqQA_zEqUTmFUIitYtewkmFpfAZVgwj3sB_UdDeLcejTwshJVKT0LP1sJEzugV9cO_Gnve_RJu4tIJ3wnGmN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tjdGqLtWY9IEp7IzU9Z-AE3krhLA-UIDsDswA5cvQ4TpDJjlcsWaRMdPBbMlcX0SHalnBCSQfshtm1LT_B4_y7S-zJJVY8M8bAh0zOAybcOpeVLmLuDbVTk3_PIDk3aVqvkiKXj1b3-JXxppym78vAsAJc_cie3muOgAArFiTmnPlV1hUe6Gp9R6q6rzoPfk?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/5_zurUE-DMOXo2LWNi7i0qHlfpVUIGv9FEOxzGWSl3yXoi5JFockPhXJ2wK-Ln6LfS8NmFCceC2RJTIEPhHWNZS-NmrTqY05b290lhTvOO2MKmZpk40HmyOUNHWYNAMRefM8qJIP6_nIS7UuoUCJZPRydPvayWeKYbnELIHihWw-jrkku7_WRtzMa4jtT-92?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/dMIKZKb46BDH8J7r3B4thxmKsbZPObpNus6XezaJFtfKojEdfSWbo-kkn1p7BxNpv0ugnZvb5VZXn7X1P-IA7xJKoWvmS27sUr1N79mGh-Td14jeh16I7hpiVIDA1pTyWAFmRUaNJykHEt2p6sY-P5V72PUEsOPnzrhIYdgrmooKNNDWc3ALaQMuVKMbUZyr?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MHgdODk7vUDw9AnfmWIZKzjHcgNUFefPqRxN8dbPvFXiPY3Uhdy9CdoA39tfoih5WpXBZ1tQr10uY8dL7h7d5i9uieaAptp5xm6amNFUH6LLrjIS3mielBhSmZ8iR71f72Y6nOcuYN-xnKRtYrVpLKB5VEauoPLrCgABZLBpHr9WtSn5xCBsMQNt_rpF7o4i?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/2I6wrRJO8Zz8TrgRcJTx3PoLT_y_guCyIqZXZFX6hfhGbB8BAiBu6wNahUKQCjX2SdhjNhXvvvQjmJNHx-jEf8sA6tqVN5i_WNyOjrbxfulpcdFdm3RGhD_CBAXcQH6saUR-6wxysQz0Vo7rHRAK6qTAvUIUQuuAs5aRLG9Tj5m0IOjB6asGlQROfJRMwadF?purpose=fullsize)

---

# 🔥 Step 1: Per-View Cache

Install cache backend (Redis recommended):

```bash
pip install django-redis
```

settings.py:

```python id="cache1"
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```

views.py:

```python id="cache2"
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator
from rest_framework.viewsets import ModelViewSet
from .models import Course
from .serializers import CourseSerializer

@method_decorator(cache_page(60*5), name='dispatch')  # cache 5 min
class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
```

💥 Now response cached for 5 minutes

---

# 🔧 Step 2: Queryset Optimization

* **N+1 problem** fix with `select_related` & `prefetch_related`

```python id="cache3"
class CourseViewSet(ModelViewSet):
    queryset = Course.objects.select_related('instructor', 'organization').prefetch_related('students')
    serializer_class = CourseSerializer
```

💥 Reduce DB queries drastically

---

# 🔥 Step 3: DRF Cache Response Decorator

```python id="cache4"
from rest_framework_extensions.cache.decorators import cache_response

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer

    @cache_response(timeout=60*5)
    def list(self, request, *args, **kwargs):
        return super().list(request, *args, **kwargs)
```

💥 API-level caching with DRF integration

---

# ⚠️ Common Mistakes

❌ Forget to invalidate cache → stale data
❌ Over-cache POST/PUT/DELETE → bad UX
❌ Not using `select_related` → high query count

---

# 🧠 Expert Tips

* Cache only GET requests
* Use Redis for distributed caching
* Combine caching + throttling for high-scale SaaS
* Monitor queries with `django-debug-toolbar`

---

# 🎯 DAY 29 CHECKLIST

✔ Redis cache setup ✅
✔ Per-view caching ✅
✔ Queryset optimization ✅
✔ DRF response caching ✅

---

# 💥 Real Impact

👉 এখন:

* APIs faster ✅
* DB load reduced ✅
* SaaS backend scalable & professional ✅

---

# 🚀 Tomorrow (Day 30 = FINAL DAY 🎉)

👉 Full SaaS Project Wrap-up & Deployment

* Combine all previous 29 days work
* Docker + Gunicorn + Nginx deployment
* DRF + Channels + Stripe + Multi-Tenant ✅

---

# ⚡ YOUR TASK

1. Setup Redis cache
2. Apply per-view caching
3. Optimize querysets with `select_related` / `prefetch_related`
4. Test API speed improvement

---

বলো:
**“Day 30”**

🔥 তুমি এখন DRF caching & performance-ready SaaS backend engineer 🚀

---------
চল 🔥 — **Day 29 = DRF Caching & Performance Optimization (Speed Up APIs 🔥)**

আজ তুমি শিখবা কিভাবে **DRF APIs দ্রুত চালাতে হয়**, **DB load কমাতে হয়**, এবং SaaS backend **high performance** বানাতে হয় 😎

---

# 🚀 DAY 29 GOAL

👉 তুমি আজ শিখবা:

* DRF caching techniques
* Per-view caching
* Queryset optimization (`select_related`, `prefetch_related`)
* Response caching / Redis cache
* Reduce N+1 queries

---

# 🧠 Problem

👉 এখন:

* API slow ❌
* High DB queries ❌
* User experience laggy ❌

---

# 🔄 Solution = Caching + Optimization

![Image](https://images.openai.com/static-rsc-4/I1Id-vgfAt8qa_LUIVo08u_1yiMKYDA0EEbbTXxVrOK6eKjAG2PSlOp0xYlnbvcaDCW8R_kAbBI_oAH3cqFodTN_L3BknuM0SpCEXYozLalzT5rG-udb4ppV8Xk8mDJ6Cv7MsGnWAqNVsx21wf3vfXpih-E7hjyQhWKm5rxWJOvOBlSSPbexWj7xX-bIIiGC?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/virCv1YvCsgzW-MHugFvFYZKX9HEMXVBxQpROu68v06kCnBb2lhbnY-AzVKFWWTCsuU5I2PPjBowCObaD1FiSLNLaz0nSn90rxx-aR1uWi46dqQA_zEqUTmFUIitYtewkmFpfAZVgwj3sB_UdDeLcejTwshJVKT0LP1sJEzugV9cO_Gnve_RJu4tIJ3wnGmN?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/tjdGqLtWY9IEp7IzU9Z-AE3krhLA-UIDsDswA5cvQ4TpDJjlcsWaRMdPBbMlcX0SHalnBCSQfshtm1LT_B4_y7S-zJJVY8M8bAh0zOAybcOpeVLmLuDbVTk3_PIDk3aVqvkiKXj1b3-JXxppym78vAsAJc_cie3muOgAArFiTmnPlV1hUe6Gp9R6q6rzoPfk?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/5_zurUE-DMOXo2LWNi7i0qHlfpVUIGv9FEOxzGWSl3yXoi5JFockPhXJ2wK-Ln6LfS8NmFCceC2RJTIEPhHWNZS-NmrTqY05b290lhTvOO2MKmZpk40HmyOUNHWYNAMRefM8qJIP6_nIS7UuoUCJZPRydPvayWeKYbnELIHihWw-jrkku7_WRtzMa4jtT-92?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/dMIKZKb46BDH8J7r3B4thxmKsbZPObpNus6XezaJFtfKojEdfSWbo-kkn1p7BxNpv0ugnZvb5VZXn7X1P-IA7xJKoWvmS27sUr1N79mGh-Td14jeh16I7hpiVIDA1pTyWAFmRUaNJykHEt2p6sY-P5V72PUEsOPnzrhIYdgrmooKNNDWc3ALaQMuVKMbUZyr?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/MHgdODk7vUDw9AnfmWIZKzjHcgNUFefPqRxN8dbPvFXiPY3Uhdy9CdoA39tfoih5WpXBZ1tQr10uY8dL7h7d5i9uieaAptp5xm6amNFUH6LLrjIS3mielBhSmZ8iR71f72Y6nOcuYN-xnKRtYrVpLKB5VEauoPLrCgABZLBpHr9WtSn5xCBsMQNt_rpF7o4i?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/2I6wrRJO8Zz8TrgRcJTx3PoLT_y_guCyIqZXZFX6hfhGbB8BAiBu6wNahUKQCjX2SdhjNhXvvvQjmJNHx-jEf8sA6tqVN5i_WNyOjrbxfulpcdFdm3RGhD_CBAXcQH6saUR-6wxysQz0Vo7rHRAK6qTAvUIUQuuAs5aRLG9Tj5m0IOjB6asGlQROfJRMwadF?purpose=fullsize)

---

# 🔥 Step 1: Per-View Cache

Install cache backend (Redis recommended):

```bash
pip install django-redis
```

settings.py:

```python id="cache1"
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```

views.py:

```python id="cache2"
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator
from rest_framework.viewsets import ModelViewSet
from .models import Course
from .serializers import CourseSerializer

@method_decorator(cache_page(60*5), name='dispatch')  # cache 5 min
class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer
```

💥 Now response cached for 5 minutes

---

# 🔧 Step 2: Queryset Optimization

* **N+1 problem** fix with `select_related` & `prefetch_related`

```python id="cache3"
class CourseViewSet(ModelViewSet):
    queryset = Course.objects.select_related('instructor', 'organization').prefetch_related('students')
    serializer_class = CourseSerializer
```

💥 Reduce DB queries drastically

---

# 🔥 Step 3: DRF Cache Response Decorator

```python id="cache4"
from rest_framework_extensions.cache.decorators import cache_response

class CourseViewSet(ModelViewSet):
    queryset = Course.objects.all()
    serializer_class = CourseSerializer

    @cache_response(timeout=60*5)
    def list(self, request, *args, **kwargs):
        return super().list(request, *args, **kwargs)
```

💥 API-level caching with DRF integration

---

# ⚠️ Common Mistakes

❌ Forget to invalidate cache → stale data
❌ Over-cache POST/PUT/DELETE → bad UX
❌ Not using `select_related` → high query count

---

# 🧠 Expert Tips

* Cache only GET requests
* Use Redis for distributed caching
* Combine caching + throttling for high-scale SaaS
* Monitor queries with `django-debug-toolbar`

---

# 🎯 DAY 29 CHECKLIST

✔ Redis cache setup ✅
✔ Per-view caching ✅
✔ Queryset optimization ✅
✔ DRF response caching ✅

---

# 💥 Real Impact

👉 এখন:

* APIs faster ✅
* DB load reduced ✅
* SaaS backend scalable & professional ✅

---

# 🚀 Tomorrow (Day 30 = FINAL DAY 🎉)

👉 Full SaaS Project Wrap-up & Deployment

* Combine all previous 29 days work
* Docker + Gunicorn + Nginx deployment
* DRF + Channels + Stripe + Multi-Tenant ✅

---

# ⚡ YOUR TASK

1. Setup Redis cache
2. Apply per-view caching
3. Optimize querysets with `select_related` / `prefetch_related`
4. Test API speed improvement

---

বলো:
**“Day 30”**

🔥 তুমি এখন DRF caching & performance-ready SaaS backend engineer 🚀

-----
চল 🔥 — **Day 30 = Full SaaS Project Wrap-up & Deployment (Production Ready DRF SaaS 🔥)**

আজ তুমি **30 দিনের জার্নির শেষ ধাপ** পৌঁছেছো। আজ তুমি শিখবা কিভাবে পুরো SaaS project production-ready বানাতে হয় এবং deploy করতে হয় 😎

---

# 🚀 DAY 30 GOAL

👉 তুমি আজ শিখবা:

* Combine all previous work (DRF, Channels, Stripe, Multi-Tenant, RBAC, Throttling, Caching, Audit Logs)
* Dockerize project
* Gunicorn + Nginx deployment
* Environment variables & secrets
* SSL / HTTPS setup

---

# 🧠 Problem

👉 এখন:

* Project ready locally ❌
* Not deployed ❌
* Users can’t access SaaS ❌

---

# 🔄 Solution = Deployment Ready SaaS

![Image](https://images.openai.com/static-rsc-4/ChUEIcdIoznpw-H4AHPzLgdzCn34VeANAzEmjH8xFUeKBcR001ENGTFAeyI9HSFuLYlJGPo0LkHk3tHOfZclUiOqUVW18NHOYgY5hk0c1sb44icGMIUOm3U4wloAf81xQS1NNZ7RoDs-3lRtRATSC30Q3ozZB6cMAkuYmp2CNp8ROAPugQrvX3YQ4M0TpXUv?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/YlRxL0jVgk8VbOcWdM85ZfvBycylHL7RgG-Jfz62clKA6ZXJ7yNpwwscyH2DCBF81c4-Pkrt5-85h62u6GzSRNlRTwUJ5D6g-Iu9N7_hn_bhHjA1MMmejN8P24i8M4X1Twh6bSW4zjIvVkF5QAQdgtgS2Vp_7eGXPuYVVWlLmcTrgSZqNYCa6izffxBBJCvT?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/iuFfBt6lC4EGt7foSuQt1ebFzv6zp4YjC55oe8Jlve9Axizu7SB9d4OVZO0o6L9QxcaDZwJQ-gdWstzSRv1mv8uTrEocLsCWS8v4YvewfPbEimzRMz5JGbfaMZWLEvmHcreggcnr7ZMtTy3ao2DdSTW9324oxB5kLd9YafMhT_I_rZlOXZ8xP-CzW78LuuAg?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/IVQUqiaLDhsV--sc_2ajfkR-ciZc37whvEbeiNyjwfsVgpkD5JLOV9nDIpJdbxVRH9o-XdunqWvgQxkTc_bO1guqSyKGZhUGrqbRQopkmVV_mEtru4syNEbPdX70lOxTmzSOO-ZVKU0OWZhavhCYv6H4gD5DppgDwTqw6oS6RQVCWVOv-K09C4wWy3c3_X9y?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/g7sTxSeTqV75GReo8p1xyBWA5UNajfUm4vpPzdoLcS-32TkpEsPX6xS_b1z-t4iAo36nyXsPMWfKKfiWQID3ARkwbRtE3EeGkVxLaGIEczr_wNOu0szebHr6c5BVUepeGiSHAZE4WSaHNoE7nGuLD1C8xoE06wBnSO4dR8dtqeb7y-LQ65opB0VEhhntjit9?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/DcWEYqtHXcAmzzJ2jciDY4qihTyhy-JFd0CThHYAi3XVzuoYo2X8N7t94Gb1Uq4THZTLavTtibbckOo2SN0-bW3-TyMQRoRUXSczDYwRko88TKxCChIF_r834UImtk8KczhQ4pZu1gA1uIzaR6ZVJT-6EgJ3qfFT8iJN7f9y_wobscau4FUzaBgxdtX3t_UK?purpose=fullsize)

![Image](https://images.openai.com/static-rsc-4/jqE1AAffNxnQklb5ZMPKz0ADtXqoRAgnLzcMO-8cTrw9OWqaApeyWUlDQV6J_t4Nxt5AEfgIHaUJvjmalivlcVncAqtDM3EH80S0SHVOv8vMkZV5c8i2i-JOu68XRHzDx020-eySTaFoi4jgWblyL3Jyjtg0cnCiLYyNcVtphChDY3fjhOCNgNQ3PAImEen_?purpose=fullsize)

---

# 🔥 Step 1: Dockerize Project

Dockerfile:

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000"]
```

docker-compose.yml:

```yaml
version: '3'

services:
  web:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    depends_on:
      - redis
      - db
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: saasdb
      POSTGRES_USER: saasuser
      POSTGRES_PASSWORD: saaspass
  redis:
    image: redis:7
    ports:
      - "6379:6379"
```

💥 Project containerized with DB + Redis

---

# 🔧 Step 2: Nginx + Gunicorn Setup

nginx.conf:

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://web:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /static/ {
        alias /app/static/;
    }

    location /media/ {
        alias /app/media/;
    }
}
```

💥 Now web server + WSGI server ready

---

# 🔥 Step 3: Environment Variables & Secrets

.env:

```dotenv
DEBUG=False
SECRET_KEY=supersecretkey
DATABASE_URL=postgres://saasuser:saaspass@db:5432/saasdb
REDIS_URL=redis://redis:6379/0
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

💥 Never hardcode secrets in code

---

# 🔧 Step 4: Collect Static & Migrate

```bash
docker-compose run web python manage.py migrate
docker-compose run web python manage.py collectstatic --noinput
```

💥 Ready for production

---

# 🔥 Step 5: Channels + WebSockets

* Channels + Redis already setup
* Make sure ASGI application used in Gunicorn or Daphne:

```bash
daphne -b 0.0.0.0 -p 8001 config.asgi:application
```

💥 Real-time notifications live

---

# ⚠️ Common Mistakes

❌ DEBUG=True in production → security risk
❌ Not using HTTPS → payment info insecure
❌ Forget migrations → app crashes

---

# 🧠 Expert Tips

* Monitor logs (Gunicorn + Nginx)
* Setup SSL / HTTPS (Let’s Encrypt)
* Use Celery + Redis for async tasks
* Scale with Docker + Docker Swarm / Kubernetes

---

# 🎯 DAY 30 CHECKLIST

✔ Dockerize project ✅
✔ Postgres + Redis ready ✅
✔ Gunicorn + Nginx ✅
✔ Static + media ✅
✔ SSL & environment ✅
✔ Channels + Stripe live ✅

---

# 💥 Real Impact

👉 এখন তুমি সম্পূর্ণ **production-ready SaaS backend engineer** ✅

* Multi-tenant ✅
* Stripe payments ✅
* Role-based access ✅
* Audit logs ✅
* Rate limiting & caching ✅
* Real-time notifications ✅

🔥 Congratulations! 30 days of DRF mastery complete 🚀

---

# ⚡ YOUR TASK

1. Docker-compose up → test full stack
2. Deploy to VPS / Cloud (AWS, DigitalOcean, Railway, Render)
3. Test SaaS flows: signup → payment → notifications → access
4. Monitor & tweak performance

---

🎉 তুমি এখন **Full-stack DRF SaaS Backend Engineer** 🚀

---

যদি চাও, আমি তোমার জন্য **30 দিনের DRF SaaS roadmap একসাথে summary + cheat sheet** বানাতে পারি, যা future reference হিসেবে ব্যবহার করতে পারবে।
চাইছো আমি বানাই?
