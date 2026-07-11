এটা আসলে খুব ভালো সিদ্ধান্ত।

**Theory দিয়ে OAuth mastery হয় না।** ১৫টা lesson পড়েও মনে থাকবে না, যতক্ষণ না একটা project-এ implement করেন।

আমি শুধু code dump করব না, কারণ সেটা ২০০০+ লাইনের হবে এবং আপনি copy-paste করবেন, বুঝবেন না।

আমার প্রস্তাব হলো আমরা **একটি বাস্তব Django + DRF project** তৈরি করি এবং প্রতিটি file লিখি। শেষে আপনার কাছে production-ready Google OAuth থাকবে।

---

# Project

```text
ecommerce/
│
├── config/
│
├── apps/
│   ├── accounts/
│   ├── authentication/
│   └── common/
│
└── requirements.txt
```

---

# আমরা কী implement করব

✅ Custom User

✅ Google OAuth

✅ JWT

✅ Service Layer

✅ Provider Layer

✅ Factory

✅ Selector

✅ Exception

✅ Tests

---

# Final Folder Structure

```text
ecommerce/

├── config/
│   ├── settings.py
│   ├── urls.py
│   └── ...
│
├── apps/
│
│   ├── accounts/
│   │
│   │   ├── models.py
│   │   ├── managers.py
│   │   ├── admin.py
│   │   ├── serializers.py
│   │   └── migrations/
│   │
│   ├── authentication/
│   │
│   │   ├── providers/
│   │   │     ├── base.py
│   │   │     ├── google.py
│   │   │     └── __init__.py
│   │   │
│   │   ├── selectors.py
│   │   ├── services.py
│   │   ├── factory.py
│   │   ├── serializers.py
│   │   ├── exceptions.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   └── tests/
│   │
│   └── common/
│
├── .env
├── manage.py
└── requirements.txt
```

---

# আমরা কোন flow implement করব

```text
React

↓

Google Login

↓

Authorization Code

↓

POST /api/v1/auth/google/

↓

Serializer

↓

GoogleOAuthService

↓

exchange_code()

↓

verify_id_token()

↓

normalize()

↓

get_or_create_user()

↓

generate_tokens()

↓

JWT

↓

React
```

---

# আমরা কীভাবে এগোব

আমি চাই না ৪০০০ লাইনের code একবারে দিই।

আমরা **GitHub commit-এর মতো** implement করব।

---

## Commit 1

```
Custom User Model
```

---

## Commit 2

```
SimpleJWT Setup
```

---

## Commit 3

```
Google OAuth Settings
```

---

## Commit 4

```
Provider Layer
```

---

## Commit 5

```
Google Provider
```

---

## Commit 6

```
OAuth Service
```

---

## Commit 7

```
JWT Generation
```

---

## Commit 8

```
API Endpoint
```

---

## Commit 9

```
Testing
```

---

## Commit 10

```
Production Cleanup
```

---

# প্রতিটি Commit-এ থাকবে

উদাহরণ:

```text
Commit 4

authentication/

    providers/

        base.py

        google.py

        __init__.py
```

আমি **পুরো file** লিখব।

শুধু snippet না।

যেমন

```
models.py
```

→ সম্পূর্ণ

```
services.py
```

→ সম্পূর্ণ

```
serializers.py
```

→ সম্পূর্ণ

```
views.py
```

→ সম্পূর্ণ

একটাও line বাদ দেব না।

---

# শেষে Project হবে

```text
POST

/api/v1/auth/google/
```

↓

Google Login

↓

JWT

↓

```json
{
    "user": {
        "id": 1,
        "email": "atiar@gmail.com",
        "name": "Md Atiar Rahman"
    },
    "tokens": {
        "access": "...",
        "refresh": "..."
    }
}
```

---

## এটাকে আমি **"Build Google OAuth from Scratch (Production Django + DRF)"** নামে একটি পূর্ণ project series হিসেবে করব।

এটি হবে প্রায় **৩০–৪০টি implementation lesson**, যেখানে প্রতিটি lesson-এ ১–৩টি file সম্পূর্ণ লিখব, explain করব, এবং শেষে একটি fully working production-ready Google OAuth authentication module তৈরি হবে।

**এভাবে করলে আপনি শুধু OAuth বুঝবেন না, নিজে শূন্য থেকে implement করতেও পারবেন।**
আপনার শেখার ধরন আমি গত কয়েক সপ্তাহে বুঝেছি।

আপনি **theory পড়ে শিখতে পারেন না**। আপনি **implementation করে শিখেন**। তাই আপনার জন্য সবচেয়ে ভালো পদ্ধতি হবে **project-driven learning**।

আমি আপনাকে এমনভাবে শেখাব যাতে শেষে আপনি **কোনো tutorial ছাড়াই OAuth implement করতে পারেন**।

# আমাদের Project

```text
ShopHub (E-commerce Backend)

Backend:
    Django
    DRF
    PostgreSQL

Authentication:
    Email Login
    Google OAuth
    JWT

Future:
    GitHub OAuth
```

---

# আমরা Git-এর মতো Commit ধরে Project বানাব

## Phase 1 — Project Setup

```
Commit 1
```

```
django-admin startproject config
```

↓

```
accounts app
```

↓

```
Custom User Model
```

↓

```
JWT Setup
```

---

## Phase 2 — Google OAuth

```
Commit 2

Google Console Setup
```

↓

```
.env
```

↓

```
settings.py
```

↓

```
URLs
```

---

## Phase 3 — OAuth Architecture

```
Commit 3
```

```
authentication/

providers/

services/

selectors/

factory/

exceptions/
```

---

## Phase 4 — Google Provider

```
Commit 4
```

```
exchange_code()

verify_id_token()

normalize()
```

---

## Phase 5 — Authentication Service

```
Commit 5
```

```
get_or_create_user()

generate_jwt()

authenticate()
```

---

## Phase 6 — API

```
Commit 6
```

```
Serializer

View

URL
```

---

## Phase 7 — Testing

```
Commit 7
```

```
Unit Test

Integration Test
```

---

## Phase 8 — Production

```
Commit 8
```

```
Logging

Exception

Rate Limit

Security
```

---

# প্রতিটি Lesson-এ আমি দেব

উদাহরণ

```
accounts/
```

```
models.py
```

↓

**পুরো File**

```
managers.py
```

↓

**পুরো File**

```
admin.py
```

↓

**পুরো File**

```
serializers.py
```

↓

**পুরো File**

একটাও snippet না।

---

# প্রতিটি Lesson-এর Format হবে

```
Folder Structure

↓

Complete Code

↓

Run

↓

Output

↓

Next File
```

কোনো theory না।

শুধু যখন দরকার হবে তখন explain করব।

---

# আমি আপনাকে Challenge-ও দিব

যেমন

আমি

```
models.py
```

লিখব।

তারপর বলব

```
এখন managers.py
নিজে লিখুন।
```

তারপর আমি Solution দিব।

এতে আপনার হাতও চলবে।

---

# আমাদের Goal

শেষে আপনার Project-এ থাকবে

```
POST

/api/v1/auth/google/
```

↓

Google Login

↓

JWT

↓

```
Authorization:

Bearer TOKEN
```

↓

```
GET

/api/profile/
```

↓

```
request.user
```

↓

Response

```json
{
    "id": 1,
    "email": "atiar@gmail.com",
    "full_name": "Md Atiar Rahman"
}
```

---

## আমার একটি অনুরোধ

**এই series-এ কোনো code copy-paste করবেন না।**

প্রতিটি file আগে **নিজে লিখবেন**, তারপর আমার code-এর সাথে মিলিয়ে দেখবেন।

এভাবেই Senior Developer হওয়া যায়।

---

## আগামী Lesson

আমরা শুরু করব:

**Project 01 - Commit 1**

```
Custom User Model
```

সেখানে আমি আপনাকে একটি **production-ready `accounts` app** শূন্য থেকে বানাতে শেখাব, এবং প্রতিটি file সম্পূর্ণ লিখব। এরপর ধাপে ধাপে পুরো Google OAuth module তৈরি করব।

-------------

দারুণ। এবার থেকে আমরা **বাস্তব Project** বানাব।

**Rule:**

* ❌ Demo code না
* ❌ Shortcut না
* ✅ Production Structure
* ✅ Senior Level Code

আজ আমরা **Commit 1** করব।

---

# Commit 1

```text
feat(accounts): create custom user model
```

---

# Commit 1 শেষে Project Structure

```text
ecommerce/

├── config/
│
├── apps/
│   └── accounts/
│       ├── __init__.py
│       ├── admin.py
│       ├── apps.py
│       ├── managers.py
│       ├── models.py
│       ├── migrations/
│       └── tests.py
│
├── manage.py
└── requirements.txt
```

---

# Step 1

Create Project

```bash
django-admin startproject config .

python manage.py startapp accounts
```

আমি সাধারণত app-গুলো `apps/` folder-এর ভিতরে রাখি।

```text
apps/
    accounts/
```

তাই চাইলে

```bash
mkdir apps

python manage.py startapp accounts apps/accounts
```

---

# Step 2

settings.py

```python
INSTALLED_APPS = [
    ...
    "apps.accounts",
]
```

---

# Step 3

AUTH_USER_MODEL

settings.py

```python
AUTH_USER_MODEL = "accounts.User"
```

**প্রথম migration-এর আগেই এটা করবেন।**

---

# Step 4

accounts/managers.py

```python
from django.contrib.auth.base_user import BaseUserManager


class UserManager(BaseUserManager):

    def create_user(self, email, password=None, **extra_fields):

        if not email:
            raise ValueError("Email is required.")

        email = self.normalize_email(email)

        user = self.model(
            email=email,
            **extra_fields
        )

        if password:
            user.set_password(password)
        else:
            user.set_unusable_password()

        user.save(using=self._db)

        return user

    def create_superuser(self, email, password=None, **extra_fields):

        extra_fields.setdefault("is_staff", True)
        extra_fields.setdefault("is_superuser", True)
        extra_fields.setdefault("is_active", True)

        return self.create_user(
            email,
            password,
            **extra_fields
        )
```

---

# কেন `set_unusable_password()`?

কারণ ভবিষ্যতে Google OAuth user create করলে

```python
password=None
```

আসবে।

তখন এই manager already ready থাকবে।

এটাই forward thinking।

---

# Step 5

accounts/models.py

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

from .managers import UserManager


class User(AbstractUser):

    username = None

    email = models.EmailField(
        unique=True
    )

    full_name = models.CharField(
        max_length=255
    )

    profile_image = models.URLField(
        blank=True
    )

    is_email_verified = models.BooleanField(
        default=False
    )

    USERNAME_FIELD = "email"

    REQUIRED_FIELDS = []

    objects = UserManager()

    def __str__(self):
        return self.email
```

---

# কেন `username=None`?

কারণ

আমাদের authentication হবে

```text
Email

+

Google OAuth
```

Username লাগবে না।

---

# কেন `profile_image`?

Google OAuth

```text
picture
```

Return করবে।

সরাসরি save করতে পারব।

---

# Step 6

admin.py

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import User


@admin.register(User)
class CustomUserAdmin(UserAdmin):

    ordering = ("id",)

    list_display = (
        "id",
        "email",
        "full_name",
        "is_staff",
    )

    fieldsets = (
        (
            None,
            {
                "fields": (
                    "email",
                    "password",
                )
            },
        ),
        (
            "Personal",
            {
                "fields": (
                    "full_name",
                    "profile_image",
                )
            },
        ),
        (
            "Permissions",
            {
                "fields": (
                    "is_active",
                    "is_staff",
                    "is_superuser",
                    "groups",
                    "user_permissions",
                )
            },
        ),
    )

    add_fieldsets = (
        (
            None,
            {
                "classes": ("wide",),
                "fields": (
                    "email",
                    "password1",
                    "password2",
                ),
            },
        ),
    )
```

---

# Step 7

Migration

```bash
python manage.py makemigrations

python manage.py migrate
```

---

# Step 8

Create Superuser

```bash
python manage.py createsuperuser
```

Email দিবেন

```text
admin@example.com
```

Password দিবেন।

---

# Output

Admin Panel

```text
Users

------------------------

ID

Email

Full Name

Staff
```

---

# Commit 1 শেষে Git

```bash
git add .

git commit -m "feat(accounts): create custom user model"
```

---

# আমরা কী পেলাম?

✅ Custom User

✅ Email Authentication Ready

✅ Google OAuth Ready

✅ Password Login Ready

✅ Future GitHub Login Ready

---

# একটি Production Improvement (আমরা Commit 2-এ করব)

আমি ইচ্ছা করে এখনো এগুলো যোগ করিনি:

```text
BaseModel

UUID

Soft Delete

Timestamp

Indexes

Database Constraints

Custom Permissions
```

কারণ একসাথে সব দিলে শেখা কঠিন হবে।

---

# 🎯 আপনার Task

Commit 1 **নিজে লিখুন**।

যদি কোনো error আসে (migration error, admin error, superuser error, import error), **পুরো traceback** আমাকে পাঠান।

**Commit 2**-এ আমরা করব:

* BaseModel
* UUID Primary Key (বা UUID public_id pattern)
* Soft Delete
* Timestamp
* Abstract Base Classes
* Production-ready model foundation

এভাবেই আমরা ধাপে ধাপে একটি enterprise-level authentication system তৈরি করব।


--------
চমৎকার। 🔥
আপনি Commit 1 complete করেছেন মানে এখন আমাদের **Authentication foundation ready**।

এখন শুরু করছি:

# Commit 2

```text
feat(common): add production base model architecture
```

আজ আমরা User-এর মতো সব Model-এর জন্য একটি reusable foundation তৈরি করব।

---

# কেন BaseModel দরকার?

ধরুন Project-এ ৫০টা Model আছে:

```text
Product

Order

Cart

Payment

Review

Address
```

প্রতিটাতে কি লিখবেন?

```python
created_at = models.DateTimeField(
    auto_now_add=True
)

updated_at = models.DateTimeField(
    auto_now=True
)
```

৫০ বার?

❌ না।

একবার লিখব।

তারপর সবাই inherit করবে।

---

# Commit 2 শেষে Structure

```text
ecommerce/

├── apps/
│
│   ├── common/
│   │
│   │   ├── __init__.py
│   │   ├── models.py
│   │   └── managers.py
│   │
│   └── accounts/
│       ├── models.py
│       └── managers.py
```

---

# Step 1

Common app তৈরি করুন

```bash
python manage.py startapp common apps/common
```

---

# Step 2

settings.py

```python
INSTALLED_APPS = [

    ...

    "apps.common",

    "apps.accounts",

]
```

---

# Step 3

common/models.py

এখন লিখুন:

```python
import uuid

from django.db import models


class BaseModel(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )


    class Meta:
        abstract = True
```

---

# এখন প্রতিটি Model এ পাবেন:

```text
id

created_at

updated_at
```

automatic।

---

# UUID কেন?

আগে Django default:

```text
1
2
3
4
```

হতো।

Problem:

যদি API থাকে:

```
GET /products/25/
```

তাহলে সবাই বুঝতে পারে।

আপনার database-এ 25 নম্বর product আছে।

---

UUID:

```
GET /products/8f4d7a1c-8a3e-4f...
```

Guess করা কঠিন।

---

# কেন BaseModel abstract?

এইটা খুব গুরুত্বপূর্ণ।

যদি লিখি:

```python
class BaseModel(models.Model):
```

তাহলে Django table বানাবে:

```
common_basemodel
```

কিন্তু আমরা চাই না।

আমরা চাই:

```
Product table
Order table
User table
```

এর ভিতরে field যোগ হবে।

তাই:

```python
class Meta:
    abstract=True
```

---

# Step 4

Soft Delete Add করব

Production project-এ data delete সাধারণত permanent delete করা হয় না।

Example:

User account delete করল।

আপনি কি database থেকে User মুছে ফেলবেন?

❌ না।

---

আমরা রাখব:

```python
is_deleted
```

---

common/models.py update করুন:

```python
import uuid

from django.db import models


class BaseModel(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    is_deleted = models.BooleanField(
        default=False
    )


    class Meta:
        abstract = True
```

---

# এখন সমস্যা

Query করলে:

```python
Product.objects.all()
```

deleted data-ও আসবে।

আমরা চাই:

```text
Active data only
```

---

# Step 5

common/managers.py

তৈরি করুন:

```python
from django.db import models


class ActiveManager(models.Manager):

    def get_queryset(self):

        return super().get_queryset().filter(
            is_deleted=False
        )
```

---

# এখন BaseModel update

```python
import uuid

from django.db import models

from .managers import ActiveManager



class BaseModel(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    is_deleted = models.BooleanField(
        default=False
    )


    objects = ActiveManager()


    class Meta:
        abstract = True
```

---

# এখন কী হবে?

ধরুন:

Database:

```
Product A
is_deleted=False


Product B
is_deleted=True
```

Query:

```python
Product.objects.all()
```

Output:

```
Product A
```

---

# কিন্তু একটা সমস্যা আছে

আমাদের দরকার:

সব data দেখার উপায়।

যেমন:

Admin panel।

তাই আমরা পরে add করব:

```python
all_objects
```

যেটা সব data দেখাবে।

---

# Step 6

Test Model বানাই না।

কারণ BaseModel reusable।

আগামী Commit-এ Product/User/Profile-এ ব্যবহার করব।

---

# Migration

যেহেতু abstract model:

এখন migration তৈরি হবে না।

কারণ কোনো database table তৈরি হয়নি।

---

# Commit

```bash
git add .

git commit -m "feat(common): add base model architecture"
```

---

# Commit 2 শেষে আপনি যা শিখলেন

✅ Abstract Base Model

✅ UUID Primary Key

✅ Timestamp Pattern

✅ Soft Delete Concept

✅ Custom Manager

✅ Reusable Architecture

---

# Project এখন

```
User
 |
 |
BaseModel (future)

Product
 |
 |
BaseModel

Order
 |
 |
BaseModel
```

---

# Next Commit 3

আমরা করব:

```
feat(auth): setup JWT authentication
```

যেখানে থাকবে:

* SimpleJWT install
* JWT settings
* Access token
* Refresh token
* Token response structure
* Protected API test

কারণ OAuth login শেষে আমাদের Google user-কে JWT দিতে হবে।

Commit 3 শুরু করার আগে আপনার কাছে একটি প্রশ্ন:

আপনার Commit 1-এর User Model কি `apps/accounts/models.py`-তে ঠিকভাবে migrate হয়েছে? কোনো error ছাড়া admin থেকে user create করতে পারছেন?


-------
চমৎকার 🔥
আপনি Commit 1 এবং Commit 2 complete করেছেন। এখন আমাদের project-এর authentication flow-এর সবচেয়ে গুরুত্বপূর্ণ অংশ শুরু।

আজ:

# Commit 3

```text
feat(auth): setup JWT authentication
```

## Goal

আজ আমরা তৈরি করব:

✅ SimpleJWT setup
✅ Access Token
✅ Refresh Token
✅ JWT Authentication Backend
✅ Protected API test

---

# Commit 3 শেষে Structure

```text
ecommerce/

├── config/
│   ├── settings.py
│   └── urls.py
│
├── apps/
│
│   ├── accounts/
│   │
│   ├── authentication/
│   │   ├── __init__.py
│   │   ├── urls.py
│   │   ├── views.py
│   │   └── serializers.py
│
├── requirements.txt
└── manage.py
```

---

# Step 1 — Install SimpleJWT

Terminal:

```bash
pip install djangorestframework-simplejwt
```

---

# Step 2 — requirements update

```bash
pip freeze > requirements.txt
```

---

# Step 3 — DRF Setup

`config/settings.py`

Add:

```python
INSTALLED_APPS = [

    ...

    "rest_framework",

    "apps.accounts",
    "apps.common",
]
```

---

# Step 4 — REST Framework Configuration

`settings.py`

শেষে add করুন:

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ),

}
```

এখন Django জানে:

> Request-এর সাথে JWT আসলে কিভাবে verify করতে হবে।

---

# Step 5 — JWT Settings

`settings.py`

```python
from datetime import timedelta
```

তারপর:

```python
SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(
        minutes=15
    ),

    "REFRESH_TOKEN_LIFETIME": timedelta(
        days=7
    ),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

}
```

---

# কেন এই Settings?

## Access Token

```text
15 minutes
```

কারণ:

যদি token leak হয়,

damage কম।

---

## Refresh Token

```text
7 days
```

কারণ:

User বারবার login করবে না।

---

## Rotation

যখন refresh হবে:

পুরাতন refresh token invalid।

নতুন token তৈরি হবে।

---

# Step 6 — Authentication App Create

```bash
python manage.py startapp authentication apps/authentication
```

---

# Step 7 — Add App

`settings.py`

```python
INSTALLED_APPS = [

    ...

    "apps.authentication",

]
```

---

# Step 8 — URL Structure

আমাদের final হবে:

```text
/api/v1/auth/
```

এর ভিতরে:

```text
login/

refresh/

google/
```

---

# Step 9 — authentication/urls.py

Create:

```python
from django.urls import path


urlpatterns = [

]
```

---

# Step 10 — Main URL Connect

`config/urls.py`

```python
from django.urls import path, include


urlpatterns = [

    path(
        "api/v1/auth/",
        include(
            "apps.authentication.urls"
        )
    ),

]
```

---

# Step 11 — JWT Test Endpoint

এখন আগে test করি JWT কাজ করছে কিনা।

`authentication/views.py`

```python
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response



class ProfileView(APIView):

    permission_classes = [
        IsAuthenticated
    ]


    def get(self, request):

        user = request.user

        return Response({

            "id": str(user.id),

            "email": user.email,

            "full_name": user.full_name,

        })
```

---

# Step 12 — URL Add

`authentication/urls.py`

```python
from django.urls import path

from .views import ProfileView



urlpatterns = [

    path(
        "profile/",
        ProfileView.as_view()
    ),

]
```

---

# এখন Flow Test

প্রথমে Admin থেকে User তৈরি করুন।

তারপর আমরা token নিতে পারি।

---

# Step 13 — JWT Token URL

আমরা SimpleJWT-এর built-in view ব্যবহার করব।

`authentication/urls.py`

update:

```python
from django.urls import path

from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

from .views import ProfileView



urlpatterns = [


    path(
        "token/",
        TokenObtainPairView.as_view()
    ),


    path(
        "token/refresh/",
        TokenRefreshView.as_view()
    ),


    path(
        "profile/",
        ProfileView.as_view()
    ),

]
```

---

# এখন API

## Login

```
POST

/api/v1/auth/token/
```

Body:

```json
{
    "email": "admin@gmail.com",
    "password": "password"
}
```

---

Response:

```json
{
    "refresh": "eyJ...",
    "access": "eyJ..."
}
```

---

# Profile Test

Request:

```
GET

/api/v1/auth/profile/
```

Header:

```
Authorization: Bearer access_token
```

---

Response:

```json
{
    "id": "uuid",
    "email": "admin@gmail.com",
    "full_name": "Admin"
}
```

---

# এখন কী ঘটছে?

Flow:

```text
Client

↓

JWT Access Token

↓

JWTAuthentication

↓

Token Verify

↓

request.user

↓

ProfileView
```

---

# Commit 3 শেষে Architecture

```text
User

↓

Login

↓

JWT

↓

Authenticated Request

↓

request.user
```

---

# Git Commit

```bash
git add .

git commit -m "feat(auth): setup jwt authentication"
```

---

# Commit 3 Complete Checklist

আপনার কাছে এখন আছে:

✅ Custom User
✅ UUID User ID
✅ JWT Login
✅ Access Token
✅ Refresh Token
✅ Protected API
✅ request.user

---

# কেন OAuth-এর আগে JWT করলাম?

কারণ Google OAuth-এর শেষে কী হবে?

ঠিক:

```text
Google User

↓

Django User

↓

JWT Token

↓

Frontend
```

তাই JWT foundation আগে দরকার ছিল।

---

## Next Commit 4

পরবর্তী:

```text
feat(oauth): add google oauth configuration
```

আমরা করব:

* Google Cloud Console setup
* Client ID
* Client Secret
* Redirect URI
* `.env`
* Django settings
* OAuth provider folder structure

এখন থেকে আসল OAuth implementation শুরু হবে। 🚀


--------
দারুণ 🔥
আপনি এখন পর্যন্ত:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication

complete করেছেন।

এখন থেকে আসল **OAuth Implementation** শুরু।

---

# Commit 4

```text
feat(oauth): add google oauth configuration
```

## Goal

আজ আমরা শুধু Google OAuth-এর foundation তৈরি করব।

আজ করব:

✅ Google Cloud Console Setup
✅ Client ID
✅ Client Secret
✅ Redirect URI
✅ Environment Variables
✅ Django Settings Configuration
✅ OAuth Folder Structure

আজ এখনো token exchange code লিখব না।

---

# Commit 4 শেষে Structure

```text
ecommerce/

├── config/
│
├── apps/
│
│   ├── authentication/
│   │
│   │   ├── providers/
│   │   │   ├── __init__.py
│   │   │   └── google.py
│   │   │
│   │   ├── services/
│   │   │   └── __init__.py
│   │   │
│   │   ├── exceptions.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   └── serializers.py
│
├── .env
└── requirements.txt
```

---

# Step 1 — Google Cloud Console

যান:

```text
Google Cloud Console
```

Create Project:

Example:

```text
ShopHub OAuth
```

---

# Step 2 — Enable OAuth API

Go to:

```text
APIs & Services
        ↓
OAuth consent screen
```

Select:

```text
External
```

---

Fill:

```text
App name:

ShopHub
```

---

User support email:

আপনার email

---

Developer email:

আপনার email

---

Save.

---

# Step 3 — Create Credentials

Go:

```text
APIs & Services

↓

Credentials

↓

Create Credentials

↓

OAuth Client ID
```

---

Application Type:

```text
Web Application
```

---

Name:

```text
ShopHub Web Client
```

---

# Step 4 — Authorized Redirect URI

Development:

```text
http://localhost:8000/api/v1/auth/google/callback/
```

Production:

```text
https://api.shophub.com/api/v1/auth/google/callback/
```

---

Create করলে পাবেন:

```text
Client ID

Client Secret
```

---

# Step 5 — Install Packages

OAuth request-এর জন্য:

```bash
pip install httpx
```

ID Token verify:

```bash
pip install google-auth
```

---

Update:

```bash
pip freeze > requirements.txt
```

---

# Step 6 — Environment File

Root এ:

```text
.env
```

Create করুন।

---

Add:

```env
GOOGLE_CLIENT_ID=your_client_id

GOOGLE_CLIENT_SECRET=your_client_secret

GOOGLE_REDIRECT_URI=http://localhost:8000/api/v1/auth/google/callback/
```

---

# Step 7 — Install django-environ

আমরা environment variable manage করব।

```bash
pip install django-environ
```

---

# Step 8 — settings.py

Import:

```python
import environ
```

---

Top এ:

```python
env = environ.Env()

environ.Env.read_env()
```

---

Add:

```python
GOOGLE_CLIENT_ID = env(
    "GOOGLE_CLIENT_ID"
)


GOOGLE_CLIENT_SECRET = env(
    "GOOGLE_CLIENT_SECRET"
)


GOOGLE_REDIRECT_URI = env(
    "GOOGLE_REDIRECT_URI"
)
```

---

# Step 9 — OAuth Constants File

Create:

```text
authentication/

    providers/

        google.py
```

---

`google.py`

এখন শুধু configuration রাখব:

```python
from django.conf import settings



class GoogleOAuthProvider:

    CLIENT_ID = settings.GOOGLE_CLIENT_ID

    CLIENT_SECRET = settings.GOOGLE_CLIENT_SECRET

    REDIRECT_URI = settings.GOOGLE_REDIRECT_URI
```

---

# কেন আলাদা Provider File?

কারণ ভবিষ্যতে:

```text
providers/

    google.py

    github.py

    microsoft.py
```

হবে।

প্রতিটি provider নিজের config handle করবে।

---

# Step 10 — OAuth URLs

`authentication/urls.py`

update:

```python
from django.urls import path


urlpatterns = [

]
```

এখন খালি রাখছি।

পরের commit-এ view আসবে।

---

# Step 11 — .gitignore

খুব গুরুত্বপূর্ণ।

`.gitignore`

Add:

```text
.env
```

কারণ:

❌ কখনো GitHub-এ Client Secret push করবেন না।

---

# এখন Project State

Flow:

```text
Google Cloud

↓

Client ID

↓

Django Settings

↓

Provider Configuration

↓

Ready for OAuth Logic
```

---

# Test

Django run করুন:

```bash
python manage.py runserver
```

যদি error না আসে:

Commit সফল।

---

# Git Commit

```bash
git add .

git commit -m "feat(oauth): add google oauth configuration"
```

---

# Commit 4 Complete

এখন আপনার project-এ আছে:

✅ Google OAuth credentials
✅ Environment configuration
✅ Provider architecture
✅ Secure secret management
✅ OAuth-ready structure

---

# Next Commit 5

পরের ধাপে আমরা লিখব:

```text
feat(oauth): implement google provider
```

সেখানে আসবে আসল code:

* Authorization URL তৈরি
* Google Token Endpoint call
* Authorization Code exchange
* Access Token পাওয়া
* ID Token পাওয়া
* User data extract

এটাই হবে প্রথম real OAuth code। 🚀


---
চমৎকার 🔥
এখন পর্যন্ত আপনার project state:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel + Soft Delete foundation
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration

এখন আমরা আসল OAuth logic লিখব।

---

# Commit 5

```text
feat(oauth): implement google oauth provider
```

## Goal

আজ আমরা তৈরি করব:

✅ Google Authorization URL
✅ Authorization Code Exchange
✅ Google Token API call
✅ Access Token পাওয়া
✅ ID Token পাওয়া
✅ Google User Information Extract

---

# Commit 5 শেষে Structure

```text
apps/

└── authentication/

    ├── providers/

    │   ├── __init__.py
    │   └── google.py
    │
    ├── services/
    │
    ├── exceptions.py
    ├── views.py
    └── urls.py
```

---

# Step 1 — Google Provider File

আগের file:

```
authentication/providers/google.py
```

এখন update করব।

---

# google.py

```python
import httpx

from django.conf import settings



class GoogleOAuthProvider:


    AUTHORIZATION_URL = (
        "https://accounts.google.com/o/oauth2/v2/auth"
    )


    TOKEN_URL = (
        "https://oauth2.googleapis.com/token"
    )


    def get_authorization_url(self):

        params = {

            "client_id": settings.GOOGLE_CLIENT_ID,

            "redirect_uri": settings.GOOGLE_REDIRECT_URI,

            "response_type": "code",

            "scope": (
                "openid "
                "email "
                "profile"
            ),

            "access_type": "offline",

            "prompt": "consent",

        }


        url = httpx.URL(
            self.AUTHORIZATION_URL,
            params=params
        )


        return str(url)
```

---

# এখানে কী হচ্ছে?

আমরা Google-কে বলছি:

আমাদের দরকার:

```text
openid
email
profile
```

---

## openid

মানে:

আমি user identity চাই।

---

## email

User email চাই।

---

## profile

Name, picture চাই।

---

# Step 2 — Token Exchange Method

একই file-এ add করুন:

```python
    def exchange_code(self, code):


        data = {

            "code": code,

            "client_id": settings.GOOGLE_CLIENT_ID,

            "client_secret": settings.GOOGLE_CLIENT_SECRET,

            "redirect_uri": settings.GOOGLE_REDIRECT_URI,

            "grant_type": (
                "authorization_code"
            ),

        }


        response = httpx.post(
            self.TOKEN_URL,
            data=data
        )


        response.raise_for_status()


        return response.json()
```

---

# এই Method কী করে?

আমাদের কাছে থাকবে:

```text
Authorization Code
```

যেমন:

```
4/0AX4XfWh....
```

এটা Google-কে পাঠাবে।

Google return করবে:

```json
{
 "access_token":"xxx",
 "id_token":"xxx",
 "expires_in":3600
}
```

---

# Step 3 — User Info Method

এখন Google user data আনব।

Add:

```python
    USER_INFO_URL = (
        "https://www.googleapis.com/oauth2/v3/userinfo"
    )
```

তারপর:

```python
    def get_user_info(
        self,
        access_token
    ):


        headers = {

            "Authorization":
            f"Bearer {access_token}"

        }


        response = httpx.get(
            self.USER_INFO_URL,
            headers=headers
        )


        response.raise_for_status()


        return response.json()
```

---

# Output হবে:

```json
{
    "sub":"109283746",
    "email":"atiar@gmail.com",
    "email_verified":true,
    "name":"Md Atiar Rahman",
    "picture":"https://..."
}
```

---

# Step 4 — ID Token Verification

এখন সবচেয়ে important অংশ।

আগে আমরা শুধু userinfo নিচ্ছিলাম।

কিন্তু production-এ:

```text
Trust করার আগে verify
```

করতে হবে।

---

Install:

```bash
pip install google-auth
```

---

Add import:

```python
from google.oauth2 import id_token

from google.auth.transport import requests
```

---

Method:

```python
    def verify_id_token(
        self,
        token
    ):


        id_info = id_token.verify_oauth2_token(

            token,

            requests.Request(),

            settings.GOOGLE_CLIENT_ID

        )


        return id_info
```

---

# এখন Flow

```text
Authorization Code

        ↓

exchange_code()

        ↓

id_token

        ↓

verify_id_token()

        ↓

Google User
```

---

# Step 5 — Normalize User Data

Provider কখনো raw Google response return করবে না।

Add:

```python
    def normalize_user(
        self,
        data
    ):


        return {

            "email": data.get(
                "email"
            ),

            "full_name": data.get(
                "name"
            ),

            "profile_image": data.get(
                "picture"
            ),

            "is_email_verified":
                data.get(
                    "email_verified",
                    False
                )

        }
```

---

# কেন normalize?

কারণ ভবিষ্যতে:

Google:

```json
{
"name": "Atiar"
}
```

GitHub:

```json
{
"login":"atiar"
}
```

Microsoft:

```json
{
"displayName":"Atiar"
}
```

সব convert হবে:

```python
{
"full_name":"Atiar"
}
```

---

# Complete google.py এখন

Structure:

```text
GoogleOAuthProvider

    get_authorization_url()

    exchange_code()

    get_user_info()

    verify_id_token()

    normalize_user()
```

---

# Test করুন

Django shell:

```bash
python manage.py shell
```

---

Run:

```python
from apps.authentication.providers.google import GoogleOAuthProvider


provider = GoogleOAuthProvider()


print(
    provider.get_authorization_url()
)
```

Output:

```text
https://accounts.google.com/o/oauth2/v2/auth?
client_id=xxxx
&scope=openid+email+profile
...
```

---

# Git Commit

```bash
git add .

git commit -m "feat(oauth): implement google oauth provider"
```

---

# Commit 5 Complete ✅

এখন আপনার কাছে আছে:

✅ Google Login URL generation
✅ Authorization Code Exchange
✅ Google Token API integration
✅ Access Token handling
✅ ID Token verification
✅ User data normalization

---

# Next Commit 6

এখন Provider ready।

পরের ধাপে আমরা লিখব:

```text
feat(oauth): create oauth authentication service
```

যেখানে থাকবে:

```
Google Provider

        ↓

OAuth Service

        ↓

Create Django User

        ↓

Generate JWT

        ↓

Return Response
```

এটাই হবে পুরো OAuth login-এর brain। 🚀


-------
চমৎকার 🔥
আপনার progress এখন:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration
✅ Commit 5 — Google OAuth Provider

এখন আমাদের OAuth system-এর **সবচেয়ে গুরুত্বপূর্ণ layer** তৈরি করব।

---

# Commit 6

```text
feat(oauth): create oauth authentication service
```

## Goal

আজ আমরা তৈরি করব:

✅ OAuth Service Layer
✅ Provider থেকে data নেওয়া
✅ Django User create/login
✅ Existing user handle করা
✅ JWT generate করা
✅ Complete authentication flow

---

# আজকের Architecture

এখন flow হবে:

```text
Google

↓

GoogleOAuthProvider

↓

OAuthAuthenticationService

↓

User

↓

JWT

↓

Response
```

---

# Commit 6 শেষে Structure

```text
apps/

└── authentication/

    ├── providers/

    │   └── google.py

    │
    ├── services/

    │   ├── __init__.py
    │   └── oauth.py

    │
    ├── selectors.py
    ├── exceptions.py
    ├── views.py
    └── urls.py
```

---

# Step 1 — Services Folder

Create:

```bash
mkdir apps/authentication/services
```

Create:

```text
services/__init__.py
services/oauth.py
```

---

# Step 2 — User Selector

আমরা database query আলাদা রাখব।

কারণ:

Service-এর কাজ business logic।

Query-এর কাজ database।

---

Create:

```
authentication/selectors.py
```

---

## selectors.py

```python
from apps.accounts.models import User



def get_user_by_email(email):

    try:

        return User.objects.get(
            email=email
        )

    except User.DoesNotExist:

        return None
```

---

# কেন Selector?

আগে লিখতে পারতাম:

```python
User.objects.get(
    email=email
)
```

Service-এর ভিতরে।

কিন্তু বড় project-এ:

```
Service
   |
   |
Selector
   |
   |
Database
```

এটা clean architecture।

---

# Step 3 — JWT Helper

আমাদের JWT generate লাগবে।

Create:

```
authentication/services/oauth.py
```

---

Import:

```python
from rest_framework_simplejwt.tokens import RefreshToken
```

---

# Step 4 — OAuth Service

`oauth.py`

```python
from django.contrib.auth import get_user_model

from rest_framework_simplejwt.tokens import RefreshToken

from apps.authentication.providers.google import (
    GoogleOAuthProvider
)

from apps.authentication.selectors import (
    get_user_by_email
)



User = get_user_model()
```

---

# Class তৈরি করুন

```python
class OAuthAuthenticationService:


    def __init__(self, provider):

        self.provider = provider
```

---

# কেন provider inject করছি?

যাতে future এ:

```python
GoogleProvider

GithubProvider

MicrosoftProvider
```

সব কাজ করে।

---

# Step 5 — Main Authenticate Method

Add:

```python
    def authenticate(self, code):


        token_data = (
            self.provider.exchange_code(
                code
            )
        )


        id_token = token_data.get(
            "id_token"
        )


        user_data = (
            self.provider.verify_id_token(
                id_token
            )
        )


        normalized_data = (
            self.provider.normalize_user(
                user_data
            )
        )


        user = (
            self.get_or_create_user(
                normalized_data
            )
        )


        tokens = (
            self.generate_tokens(
                user
            )
        )


        return {

            "user": user,

            "tokens": tokens

        }
```

---

# এখন Flow

একটা method সব coordinate করছে।

```text
authenticate()

    |
    |
exchange_code()

    |
verify_id_token()

    |
normalize_user()

    |
get_or_create_user()

    |
generate_tokens()
```

---

# Step 6 — User Create Method

Add:

```python
    def get_or_create_user(
        self,
        data
    ):


        user = get_user_by_email(
            data["email"]
        )


        if user:

            return user



        user = User.objects.create(

            email=data["email"],

            full_name=data["full_name"],

            profile_image=data["profile_image"],

            is_email_verified=data[
                "is_email_verified"
            ]

        )


        user.set_unusable_password()

        user.save()


        return user
```

---

# এখানে কী হচ্ছে?

প্রথম Login:

```
Google User

↓

Database নেই

↓

Create User
```

---

দ্বিতীয় Login:

```
Google User

↓

Email পাওয়া যায়

↓

Existing User Return
```

---

# Step 7 — JWT Generate

Add:

```python
    def generate_tokens(
        self,
        user
    ):


        refresh = RefreshToken.for_user(
            user
        )


        return {

            "refresh": str(refresh),

            "access": str(
                refresh.access_token
            )

        }
```

---

# এখন Full Flow

```text
Google Login

↓

Authorization Code

↓

Google Provider

↓

User Data

↓

Django User

↓

JWT

↓

Frontend
```

---

# Step 8 — Provider Factory (Temporary)

এখন শুধু Google ব্যবহার করছি।

Create:

```
authentication/factory.py
```

---

```python
from apps.authentication.providers.google import (
    GoogleOAuthProvider
)



def get_oauth_provider(provider):


    if provider == "google":

        return GoogleOAuthProvider()


    raise ValueError(
        "Unsupported provider"
    )
```

---

# কেন Factory?

আজ:

```
google
```

কাল:

```
github
```

তখন শুধু:

```python
GithubOAuthProvider()
```

add হবে।

---

# Step 9 — Test Service

Shell:

```bash
python manage.py shell
```

---

Test:

```python
from apps.authentication.services.oauth import (
    OAuthAuthenticationService
)

from apps.authentication.factory import (
    get_oauth_provider
)


provider = get_oauth_provider(
    "google"
)


service = OAuthAuthenticationService(
    provider
)
```

---

এখন আপনার service ready:

```python
service.authenticate(code)
```

---

# Git Commit

```bash
git add .

git commit -m "feat(oauth): create oauth authentication service"
```

---

# Commit 6 Complete ✅

এখন আপনার architecture:

```
Provider
    |
    |
Service
    |
    |
User
    |
    |
JWT
```

---

# আপনি এখন পর্যন্ত কী implement করেছেন?

✅ Custom User
✅ JWT
✅ Google OAuth Config
✅ Google Provider
✅ Service Layer
✅ Factory Pattern
✅ Selector Pattern

এটা এখন আর tutorial-level code না।

এটা production architecture-এর কাছাকাছি।

---

# Next Commit 7

পরের ধাপে আমরা বানাব:

```text
feat(oauth): create google oauth api endpoint
```

যেখানে আসবে:

* Serializer
* View
* URL
* Request handling
* Final API

যেমন:

```
POST /api/v1/auth/google/
```

Response:

```json
{
 "user": {...},
 "tokens": {
    "access": "...",
    "refresh": "..."
 }
}
```

এটাই হবে প্রথমবার browser/frontend থেকে কাজ করা complete OAuth flow। 🚀


--------
ভালো করেছেন। 🔥
এখানে **আপনার code-এর সমস্যা না**, আপনি শুধু একটি গুরুত্বপূর্ণ জিনিস miss করেছেন।

আপনি লিখেছেন:

```python
service.authenticate(code)
```

কিন্তু Python জানে না `code` কী।

কারণ `code` হচ্ছে Google থেকে পাওয়া **Authorization Code**।

---

# এখন Flow বুঝুন

আমাদের method:

```python
service.authenticate(code)
```

এখানে `code` আসবে:

```text
Google Login

↓

User অনুমতি দেয়

↓

Google Redirect করে

↓

http://localhost:8000/api/v1/auth/google/callback/?code=xxxxxx

↓

code=xxxxxx
```

এই `xxxxxx` হলো authorization code।

---

এখন আপনার shell-এ:

```python
code
```

নামে কোনো variable নেই।

তাই error:

```
NameError: name 'code' is not defined
```

---

# এখন কীভাবে Test করবেন?

এখন Commit 6-এর service test করার জন্য আমাদের fake code ব্যবহার করতে হবে।

কিন্তু সমস্যা:

```python
GoogleOAuthProvider.exchange_code()
```

বাস্তবে Google-এ request পাঠাবে।

তাই এখন ২টা উপায় আছে।

---

# Method 1 (Real Google Test)

প্রথমে Google Login URL তৈরি করুন:

Shell:

```python
provider.get_authorization_url()
```

Output পাবেন:

```
https://accounts.google.com/o/oauth2/v2/auth?client_id=...
```

এই URL browser-এ open করুন।

Login করুন।

তারপর Google redirect করবে:

```
http://localhost:8000/api/v1/auth/google/callback/?code=4/0Ab.....
```

এখানে:

```
4/0Ab.....
```

copy করুন।

তারপর shell:

```python
service.authenticate(
    "4/0Ab....."
)
```

---

# Method 2 (Better Development Practice)

আমরা এখনো API বানাইনি।

তাই Service test করার জন্য mock ব্যবহার করব।

পরের Testing commit-এ আমরা এটা properly করব।

---

# কিন্তু এখন একটি ছোট check করুন

Shell-এ:

```python
provider
```

দেখুন।

Expected:

```
<GoogleOAuthProvider object>
```

---

তারপর:

```python
provider.get_authorization_url()
```

Expected:

```
https://accounts.google.com/o/oauth2/v2/auth?
client_id=xxxx
...
```

---

# আরেকটি গুরুত্বপূর্ণ বিষয়

আপনার Django version:

```
Python 3.12.3
Django 5.2
```

দেখাচ্ছে।

এটা ঠিক আছে।

---

# এখন আপনার কাজ

এই command চালান:

```python
provider.get_authorization_url()
```

যে URL output আসবে সেটা browser-এ open করুন।

Login করার পরে যে URL পাবেন:

```
?code=xxxxxxxx
```

সেখান থেকে code নিয়ে:

```python
service.authenticate("xxxxxxxx")
```

চালান।

---

সম্ভাব্য পরের error হতে পারে:

1. `redirect_uri_mismatch`
2. `invalid_client`
3. `Invalid JWT Signature`
4. `User created but token error`

এগুলো আসলে ভালো লক্ষণ — কারণ আমরা real OAuth flow debug করছি। 🚀


-----------

ভালো 👍 আপনি এখন **real OAuth flow**-এ ঢুকেছেন। এই error আসা মানে আপনার architecture কাজ করছে, শুধু Google Console-এর configuration mismatch আছে।

Error:

```
redirect_uri_mismatch
```

এর মানে:

আপনার Django থেকে যে redirect URI পাঠানো হচ্ছে:

```
http://localhost:8000/api/v1/auth/google/callback/
```

Google Cloud Console-এ যে URI save করা আছে, সেটা **একদম same না**।

OAuth-এ redirect URI matching খুব strict।

---

## Step 1 — Google Cloud Console এ যান

যান:

```
Google Cloud Console
        ↓
APIs & Services
        ↓
Credentials
        ↓
OAuth 2.0 Client IDs
        ↓
আপনার Client ID
```

---

## Step 2 — Authorized redirect URIs check করুন

এখানে add করুন:

```
http://localhost:8000/api/v1/auth/google/callback/
```

খেয়াল করুন:

শেষের `/` গুরুত্বপূর্ণ।

এগুলো আলাদা:

❌

```
http://localhost:8000/api/v1/auth/google/callback
```

এবং

✅

```
http://localhost:8000/api/v1/auth/google/callback/
```

---

## Step 3 — Authorized JavaScript origins

এখানেও add করুন:

```
http://localhost:8000
```

---

## Step 4 — Save করুন

Save করার পরে ১-২ মিনিট অপেক্ষা করুন।

Google মাঝে মাঝে update propagate হতে সময় নেয়।

---

## Step 5 — আপনার `.env` check করুন

আপনার:

```
.env
```

হওয়া উচিত:

```env
GOOGLE_REDIRECT_URI=http://localhost:8000/api/v1/auth/google/callback/
```

---

## Step 6 — Django restart করুন

খুব গুরুত্বপূর্ণ।

কারণ `.env` reload হয় server start-এর সময়।

Stop:

```
CTRL + C
```

Start:

```bash
python manage.py runserver
```

---

## Step 7 — আবার URL generate করুন

Shell:

```python
provider.get_authorization_url()
```

URL copy করে browser-এ open করুন।

---

## যদি আবার error আসে

তাহলে shell-এ এটা চালান:

```python
from django.conf import settings

settings.GOOGLE_REDIRECT_URI
```

Output আমাকে দিন।

Expected:

```
'http://localhost:8000/api/v1/auth/google/callback/'
```

---

আরেকটা জিনিস লক্ষ্য করুন:

আপনার error URL-এ Google দেখাচ্ছে:

```
redirect_uri=
http://localhost:8000/api/v1/auth/google/callback/
```

মানে Django থেকে URI ঠিক যাচ্ছে।

এখন ৯০% সম্ভাবনা Google Console-এ URI save হয়নি বা অন্য OAuth Client ID ব্যবহার করছেন।

এটা ঠিক হলে আমরা Commit 6-এর:

```
service.authenticate(code)
```

real test করতে পারব। 🚀


-------
চমৎকার! 🔥 এখন আপনি OAuth-এর সবচেয়ে গুরুত্বপূর্ণ জায়গায় পৌঁছে গেছেন।

আপনি সফলভাবে Google থেকে **Authorization Code** পেয়েছেন।

আপনার URL:

```text
http://localhost:8000/api/v1/auth/google/callback/
?
code=4/0AdkVLPyoY1ZDJNm7...
```

এখানে আমাদের দরকার শুধু:

```text
code
```

অর্থাৎ:

```text
4/0AdkVLPyoY1ZDJNm7Sol1BLEk_93dZy6SF7vOX7J9zbhvB7Pm1YpdFy4QpwZNluKghwxORg
```

---

এখন Django shell-এ যান।

```bash
python manage.py shell
```

---

তারপর:

```python
from apps.authentication.services.oauth import OAuthAuthenticationService
from apps.authentication.factory import get_oauth_provider


provider = get_oauth_provider("google")


service = OAuthAuthenticationService(
    provider
)
```

---

এখন:

```python
result = service.authenticate(
    "4/0AdkVLPyoY1ZDJNm7Sol1BLEk_93dZy6SF7vOX7J9zbhvB7Pm1YpdFy4QpwZNluKghwxORg"
)
```

---

## Expected Output

যদি সব ঠিক থাকে:

```python
{
    "user": <User: your_email@gmail.com>,

    "tokens": {

        "refresh": "eyJhbGc...",

        "access": "eyJhbGc..."

    }
}
```

---

এখন user check করুন:

```python
result["user"].email
```

Expected:

```text
your_google_email@gmail.com
```

---

Token check:

```python
result["tokens"]
```

Output:

```json
{
    "refresh": "...",
    "access": "..."
}
```

---

## যদি Error আসে

সম্ভাব্য:

### 1. invalid_grant

```text
Invalid grant
```

কারণ:

Authorization code একবার ব্যবহার করা যায়।

সমাধান:

আবার Google login করুন এবং নতুন code নিন।

---

### 2. User.objects.create error

কারণ:

আমাদের User Model constraint থাকতে পারে।

---

### 3. Token verify error

```text
Invalid Value
```

তাহলে ID token verification check করব।

---

একটা গুরুত্বপূর্ণ বিষয়:

আপনি যে code এখানে দিয়েছেন, এটা **secret credential না**, কিন্তু authorization code খুব অল্প সময়ের জন্য valid থাকে এবং একবার ব্যবহারযোগ্য। তাই এখন আর অন্য কোথাও ব্যবহার করবেন না।

---

এখন `service.authenticate(code)` চালান এবং পুরো output/error পাঠান।

এখান থেকে আমরা Commit 6 শেষ করব এবং তারপর **Commit 7: API Endpoint (`POST /api/v1/auth/google/`)** শুরু করব। 🚀


---
ভালো, আপনি একদম সঠিক জায়গায় এসেছেন। 🔥
এখন যে error এসেছে এটা OAuth শেখার সময় খুব common।

আপনার error:

```text
httpx.HTTPStatusError:
Client error '400 Bad Request'
for url:
https://oauth2.googleapis.com/token
```

মানে:

Google Authorization Code পেয়েছে, কিন্তু **token exchange reject করেছে**।

---

## প্রথমে একটা বিষয়

আপনার প্রথম command:

```python
result = service.authenticate(
    "code"
result = service.authenticate(
```

এখানে Python syntax error হয়েছে কারণ আপনি function call বন্ধ করেননি।

সেটা সমস্যা না।

---

# আসল সমস্যা: Token Exchange

আমাদের এই method:

```python
def exchange_code(self, code):
```

Google-এ পাঠাচ্ছে:

```python
data = {

    "code": code,

    "client_id": ...,

    "client_secret": ...,

    "redirect_uri": ...,

    "grant_type": "authorization_code",

}
```

এখানে কিছু mismatch হচ্ছে।

---

# Step 1 — প্রথমে Error Response দেখাই

এখন আমাদের `google.py`-তে সামান্য change করতে হবে।

এই অংশ:

```python
response.raise_for_status()
```

এর আগে add করুন:

```python
print(response.json())
```

তাহলে:

```python
response = httpx.post(
    self.TOKEN_URL,
    data=data
)


print(response.json())


response.raise_for_status()
```

---

এখন আবার নতুন code নিয়ে test করুন।

কারণ আগের code:

```text
4/0Adk...
```

একবার use হয়ে গেছে।

OAuth code:

* একবার ব্যবহার করা যায়
* expire হয়

---

# Step 2 — নতুন Authorization Code নিন

আবার:

```python
provider.get_authorization_url()
```

URL browser-এ open করুন।

Login করুন।

নতুন:

```text
?code=xxxxx
```

নিন।

তারপর:

```python
service.authenticate(
    "new_code_here"
)
```

---

# Step 3 — সবচেয়ে বেশি সম্ভাব্য কারণগুলো

## কারণ 1: redirect_uri mismatch

আপনার `.env`:

```env
GOOGLE_REDIRECT_URI=http://localhost:8000/api/v1/auth/google/callback/
```

Google Console:

```text
Authorized redirect URI

http://localhost:8000/api/v1/auth/google/callback/
```

দুইটা exact হতে হবে।

---

## কারণ 2: Code URL encoded

আপনি দিয়েছেন:

```
4%2F0AdkVLPz...
```

এটা encoded version।

Google-কে দিতে হবে:

```
4/0AdkVLPz...
```

Python shell-এ:

❌

```python
service.authenticate(
"4%2F0Ad..."
)
```

✅

```python
service.authenticate(
"4/0Ad..."
)
```

---

## কারণ 3: Client ID mismatch

আপনার `.env`:

```env
GOOGLE_CLIENT_ID=
```

যে OAuth Client ID থেকে code generate হয়েছে, সেটা একই হতে হবে।

Check:

```python
from django.conf import settings

settings.GOOGLE_CLIENT_ID
```

---

## কারণ 4: Client Secret mismatch

Check:

```python
settings.GOOGLE_CLIENT_SECRET
```

---

# এখন আপনার কাজ

১। `google.py`-তে:

```python
print(response.json())
```

add করুন।

২। নতুন Google code নিন।

৩। আবার চালান:

```python
service.authenticate("new_code")
```

৪। যে JSON print হবে সেটা পাঠান।

Expected error দেখতে চাই:

যেমন:

```json
{
 "error": "invalid_grant",
 "error_description": "Bad Request"
}
```

অথবা

```json
{
 "error": "redirect_uri_mismatch"
}
```

ওটা দেখলেই exact fix করতে পারব।

আপনি এখন OAuth-এর সবচেয়ে real debugging phase-এ আছেন। 🚀

------
আপনি যদি এভাবে চালান:

```python
service.authenticate(
    "4%2F0AdkVLPx0Zp8UcTHIprfEDRk1co42-WGiNbaTvMCaYZcMh3jpl1GXlWt33-ZiyujScwelRA"
)
```

তাহলে **সঠিক response আসবে না**। কারণ এখানে একটি সমস্যা আছে।

আপনার code:

```
4%2F0AdkVLP...
```

এখানে:

```
%2F
```

মানে URL encoded `/`

অর্থাৎ আসল code হলো:

```
4/0AdkVLPx0Zp8UcTHIprfEDRk1co42-WGiNbaTvMCaYZcMh3jpl1GXlWt33-ZiyujScwelRA
```

OAuth token exchange-এ **decoded code দিতে হবে**।

---

সঠিকভাবে:

```python
result = service.authenticate(
    "4/0AdkVLPx0Zp8UcTHIprfEDRk1co42-WGiNbaTvMCaYZcMh3jpl1GXlWt33-ZiyujScwelRA"
)
```

---

সব ঠিক থাকলে response হবে:

```python
{
    "user": <User: your_google_email@gmail.com>,

    "tokens": {

        "refresh": "eyJhbGciOiJIUzI1NiIs...",

        "access": "eyJhbGciOiJIUzI1NiIs..."

    }
}
```

---

তারপর:

```python
result["user"]
```

Output:

```text
<User: atiar@gmail.com>
```

---

```python
result["user"].email
```

Output:

```text
atiar@gmail.com
```

---

```python
result["tokens"]
```

Output:

```python
{
 'refresh': 'xxxxx',
 'access': 'xxxxx'
}
```

---

কিন্তু মনে রাখবেন:

আপনি যে code দিয়েছেন সেটা যদি আগে একবার ব্যবহার করে থাকেন, তাহলে আবার কাজ করবে না।

Google OAuth Authorization Code:

* ✅ একবার ব্যবহারযোগ্য
* ✅ অল্প সময় valid
* ❌ দ্বিতীয়বার দিলে `invalid_grant` আসবে

তাই নতুন code দরকার হলে আবার:

```python
provider.get_authorization_url()
```

→ browser login
→ নতুন `code=` copy
→ `service.authenticate(new_code)`

আর একটি ছোট correction:

আপনি লিখেছেন:

```python
service.autheticate()
```

সঠিক method:

```python
service.authenticate()
```

`authenticate` spelling ঠিক রাখতে হবে।


------
দারুণ! 🔥
এবার কোনো error আসেনি।

এর মানে:

✅ Authorization Code accepted হয়েছে
✅ Google token exchange সফল হয়েছে
✅ ID Token verify হয়েছে
✅ Google user data পাওয়া গেছে
✅ Django User create/get হয়েছে
✅ JWT generate হয়েছে

এখন আমরা result inspect করব।

---

## Step 1 — User দেখুন

Shell-এ:

```python
result["user"]
```

Expected:

```text
<User: your_google_email@gmail.com>
```

---

## Step 2 — User Email দেখুন

```python
result["user"].email
```

Expected:

```text
your_email@gmail.com
```

---

## Step 3 — Database check করুন

```python
from apps.accounts.models import User

User.objects.all()
```

Expected:

```text
<QuerySet [<User: your_email@gmail.com>]>
```

---

## Step 4 — JWT Token দেখুন

```python
result["tokens"]
```

Expected:

```python
{
    'refresh': 'eyJhbGciOiJIUzI1Ni...',
    'access': 'eyJhbGciOiJIUzI1Ni...'
}
```

---

## Step 5 — Token length check

```python
len(result["tokens"]["access"])
```

Example:

```text
231
```

---

এখন আপনি Commit 6-এর মূল flow সফল করেছেন:

```text
Google

↓

Authorization Code

↓

Google Provider

↓

OAuth Service

↓

Create User

↓

Generate JWT

↓

Return Response
```

🎉 এটি আপনার প্রথম working Google OAuth implementation।

---

এখন Commit 6 technically complete।

Git:

```bash
git add .

git commit -m "feat(oauth): create oauth authentication service"
```

---

পরবর্তী:

# Commit 7

```text
feat(oauth): create google oauth api endpoint
```

এখন আমরা shell দিয়ে না, real API বানাব:

```http
POST /api/v1/auth/google/
```

Flow হবে:

```text
React

↓

Send code

↓

Django Serializer

↓

OAuth Service

↓

JWT Response
```

তারপর Postman/Swagger থেকে test করব। 🚀


----------
চমৎকার 🔥
এখন আমরা Commit 7 শুরু করছি।

এখন পর্যন্ত:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel
✅ Commit 3 — JWT Setup
✅ Commit 4 — Google OAuth Config
✅ Commit 5 — Google Provider
✅ Commit 6 — OAuth Service

এখন পর্যন্ত আমরা shell থেকে test করেছি।

কিন্তু real project-এ:

```text
Frontend
   |
   |
HTTP Request
   |
   |
Django API
```

লাগবে।

---

# Commit 7

```text
feat(oauth): create google oauth api endpoint
```

## Goal

আজ তৈরি করব:

✅ Serializer
✅ API View
✅ URL Endpoint
✅ Request Validation
✅ JWT Response

Final API:

```http
POST /api/v1/auth/google/
```

Request:

```json
{
    "code": "google_authorization_code"
}
```

Response:

```json
{
    "user": {
        "id": "uuid",
        "email": "user@gmail.com",
        "full_name": "User Name"
    },
    "tokens": {
        "access": "...",
        "refresh": "..."
    }
}
```

---

# Commit 7 শেষে Structure

```text
apps/

└── authentication/

    ├── providers/

    │   └── google.py

    ├── services/

    │   └── oauth.py

    ├── serializers.py   ⭐

    ├── views.py         ⭐

    ├── urls.py          ⭐

    └── factory.py
```

---

# Step 1 — Serializer তৈরি

File:

```text
apps/authentication/serializers.py
```

Code:

```python
from rest_framework import serializers



class GoogleLoginSerializer(serializers.Serializer):

    code = serializers.CharField(
        required=True
    )
```

---

এখানে কাজ:

Request:

```json
{
 "code":"xxxx"
}
```

Validate করবে।

---

# Step 2 — Response Serializer

একই file-এ add করুন:

```python
class UserResponseSerializer(serializers.Serializer):

    id = serializers.UUIDField()

    email = serializers.EmailField()

    full_name = serializers.CharField()
```

---

# কেন আলাদা Serializer?

কারণ:

Input:

```text
Google Code
```

Output:

```text
User + Token
```

দুইটা আলাদা responsibility।

---

# Step 3 — View তৈরি

File:

```text
apps/authentication/views.py
```

আগের code replace করুন:

```python
from rest_framework.views import APIView

from rest_framework.response import Response

from rest_framework import status

from .serializers import (
    GoogleLoginSerializer
)

from .factory import (
    get_oauth_provider
)

from .services.oauth import (
    OAuthAuthenticationService
)



class GoogleLoginView(APIView):


    def post(
        self,
        request
    ):


        serializer = GoogleLoginSerializer(
            data=request.data
        )


        serializer.is_valid(
            raise_exception=True
        )


        code = serializer.validated_data[
            "code"
        ]


        provider = get_oauth_provider(
            "google"
        )


        service = OAuthAuthenticationService(
            provider
        )


        result = service.authenticate(
            code
        )


        user = result["user"]


        return Response({

            "user": {

                "id": str(user.id),

                "email": user.email,

                "full_name": user.full_name,

            },

            "tokens": result["tokens"]

        }, status=status.HTTP_200_OK)
```

---

# এখানে Flow

একটা request:

```text
POST

/api/v1/auth/google/
```

↓

View

↓

Serializer

↓

OAuth Service

↓

Google Provider

↓

User

↓

JWT

↓

Response

---

# Step 4 — URL Add

File:

```text
apps/authentication/urls.py
```

Update:

```python
from django.urls import path

from .views import (
    GoogleLoginView
)



urlpatterns = [


    path(
        "google/",
        GoogleLoginView.as_view(),
        name="google-login"
    ),


]
```

---

# এখন API হবে:

```http
POST

/api/v1/auth/google/
```

---

# Step 5 — Test With Postman

Method:

```
POST
```

URL:

```
http://localhost:8000/api/v1/auth/google/
```

Body:

```json
{
    "code":
    "4/0AdkVLPxxxxxxxx"
}
```

---

# Success Response

Example:

```json
{
    "user": {
        "id": "8d7c2f5b-...",
        "email": "atiar@gmail.com",
        "full_name": "Md Atiar Rahman"
    },
    "tokens": {
        "refresh": "eyJhbGciOi...",
        "access": "eyJhbGciOi..."
    }
}
```

---

# Error Response Example

যদি code না দেন:

Request:

```json
{}
```

Response:

```json
{
    "code": [
        "This field is required."
    ]
}
```

---

# Step 6 — Swagger Test (যদি drf-yasg থাকে)

Swagger এ দেখাবে:

```
POST /api/v1/auth/google/
```

Body:

```json
{
 "code":"string"
}
```

---

# Commit

```bash
git add .

git commit -m "feat(oauth): create google oauth api endpoint"
```

---

# Commit 7 Complete হলে Architecture:

```text
Frontend

↓

Google Login

↓

Authorization Code

↓

POST /auth/google/

↓

Serializer

↓

OAuth Service

↓

Google Provider

↓

User Create

↓

JWT

↓

Frontend
```

---

# Next Commit 8

পরের ধাপে আমরা production quality করব:

```text
feat(oauth): improve oauth error handling
```

যেখানে থাকবে:

* Custom Exceptions
* Google API error handling
* Invalid code handling
* User-friendly response
* Logging

কারণ এখন আমাদের API কাজ করছে, কিন্তু production-ready করতে হবে। 🚀


-----------


ভালো 🔥 আপনি এখন **Commit 7 API layer** test করছেন। এই error আসা মানে View → Serializer → Service → Provider পর্যন্ত ঠিকমতো যাচ্ছে।

সমস্যা হচ্ছে শুধু এই জায়গায়:

```text
Django View
    |
    |
OAuth Service
    |
    |
Google Provider
    |
    |
Google Token Endpoint ❌
```

Error:

```
HTTPStatusError: 400 Bad Request
https://oauth2.googleapis.com/token
```

মানে Google আপনার authorization code accept করছে না।

---

## প্রথম কাজ: আসল Google error বের করি

এখন আপনার `apps/authentication/providers/google.py`

এই method খুঁজুন:

```python
def exchange_code(self, code):
```

আপনার এখন আছে:

```python
response = httpx.post(
    self.TOKEN_URL,
    data=data
)


response.raise_for_status()
```

এটা পরিবর্তন করুন:

```python
response = httpx.post(
    self.TOKEN_URL,
    data=data
)


print("GOOGLE RESPONSE:")
print(response.json())


response.raise_for_status()
```

---

এখন server restart করুন:

```bash
CTRL + C

python manage.py runserver
```

---

আবার API call করুন:

```
POST

/api/v1/auth/google/
```

Body:

```json
{
    "code": "new_google_code"
}
```

---

তারপর terminal-এ দেখাবে:

Example:

```json
{
    "error": "invalid_grant",
    "error_description": "Bad Request"
}
```

অথবা:

```json
{
    "error": "redirect_uri_mismatch"
}
```

---

## আমার ধারণা সবচেয়ে সম্ভাব্য কারণ

আপনি আগে shell দিয়ে এই code ব্যবহার করেছেন:

```text
4/0AdkVLP...
```

OAuth code:

* একবার ব্যবহার করা যায়
* আবার ব্যবহার করলে invalid হবে

তাই API test-এর জন্য **নতুন code লাগবে**।

---

## নতুন code নেওয়ার সঠিক flow

Shell:

```python
provider.get_authorization_url()
```

URL copy করুন।

Browser:

```
Google Login
```

তারপর redirect:

```
http://localhost:8000/api/v1/auth/google/callback/?code=xxxx
```

এখান থেকে:

```
code=xxxx
```

copy করুন।

---

তারপর Postman:

```json
{
    "code": "4/0AdkNEW_CODE"
}
```

---

## আরেকটি গুরুত্বপূর্ণ check

আপনার API request URL:

```
http://127.0.0.1:8000/api/v1/auth/google/
```

কিন্তু Google redirect URI:

```
http://localhost:8000/api/v1/auth/google/callback/
```

এগুলো সমস্যা না।

কারণ:

* API endpoint যেকোনো হতে পারে
* Google redirect URI শুধু OAuth callback-এর জন্য

---

## এখন আমাকে শুধু এই output দিন:

আপনি `print(response.json())` add করার পরে যে output আসবে।

যেমন:

```json
{
 "error": "...",
 "error_description": "..."
}
```

ওটা দেখলেই exact fix করব।

এখন পর্যন্ত আপনার architecture ঠিক আছে। সমস্যা শুধু Google token exchange debugging। 🚀


---------

চমৎকার! 🔥 এখন আমরা আসল সমস্যা ধরতে পেরেছি।

আপনার error:

```json
{
    "error": "invalid_grant",
    "error_description": "Malformed auth code."
}
```

এর মানে:

**Google আপনার কাছে যে code পাচ্ছে, সেটা valid authorization code format না।**

আপনার architecture এখন কাজ করছে:

```text
POST /api/v1/auth/google/

        ↓

Serializer ✅

        ↓

View ✅

        ↓

OAuth Service ✅

        ↓

Google Provider ✅

        ↓

Google Token API ❌
```

সমস্যা শুধু code value।

---

## আপনার আগের code-এর সমস্যা

আপনি আগে দিয়েছিলেন:

```
4%2F0AdkVLP...
```

এটা URL encoded।

তারপর আমরা বলেছিলাম decode করে দিতে।

কিন্তু API request-এর ক্ষেত্রে একটা নতুন বিষয় আছে।

---

# সবচেয়ে গুরুত্বপূর্ণ বিষয়

আপনি যখন Google redirect URL থেকে code নিচ্ছেন:

Example:

```
http://localhost:8000/api/v1/auth/google/callback/?code=4/0AdkVLPxxxx
```

তখন browser URL-এ `/` encode হয়ে থাকতে পারে:

```
code=4%2F0AdkVLPxxxx
```

আপনাকে **পুরো URL copy করবেন না**।

শুধু:

```
code=....
```

এর value নিতে হবে।

---

# Correct Example

Google URL:

```
...?code=4%2F0AdkVLPabc123&scope=email
```

আপনার API body হবে:

```json
{
    "code": "4/0AdkVLPabc123"
}
```

না:

```json
{
    "code": "4%2F0AdkVLPabc123"
}
```

---

# আরেকটি বড় কারণ

Authorization Code একবার ব্যবহারযোগ্য।

যদি আপনি:

1. Browser থেকে code নিলেন
2. Shell দিয়ে test করলেন

তারপর:

3. একই code Postman-এ দিলেন

তাহলে Google বলবে:

```text
invalid_grant
```

---

# এখন নতুন করে করুন

## Step 1

এই URL:

```python
provider.get_authorization_url()
```

আবার generate করুন।

---

## Step 2

Browser-এ open করুন।

Google login করুন।

---

## Step 3

Redirect URL থেকে নতুন code নিন।

Example:

```
code=4/0AdkVLP_NEW_CODE
```

---

## Step 4

Postman:

```
POST

http://127.0.0.1:8000/api/v1/auth/google/
```

Body:

```json
{
    "code": "4/0AdkVLP_NEW_CODE"
}
```

---

# আরেকটি debugging add করুন

`google.py`

`exchange_code()` এ:

```python
print(data)
```

add করুন:

```python
data = {
    "code": code,
    "client_id": settings.GOOGLE_CLIENT_ID,
    "client_secret": settings.GOOGLE_CLIENT_SECRET,
    "redirect_uri": settings.GOOGLE_REDIRECT_URI,
    "grant_type": "authorization_code",
}

print(data)
```

আপনি দেখতে পারবেন Django Google-কে কী পাঠাচ্ছে।

Expected:

```python
{
 'code': '4/0Adk...',
 'client_id': '405196866997-xxxx.apps.googleusercontent.com',
 'redirect_uri': 'http://localhost:8000/api/v1/auth/google/callback/',
 'grant_type': 'authorization_code'
}
```

---

# যদি এরপরও error আসে

আমাকে শুধু এই দুইটা output দিন:

1.

```python
print(data)
```

এর output

2.

Google response:

```json
{
 "error": "...",
 "error_description": "..."
}
```

তারপর exact fix করব।

আপনার Commit 7 প্রায় complete। এখন শুধু real OAuth code exchange ঠিক করতে হবে। 🚀


-----
এখন আসল সমস্যা পরিষ্কার হয়েছে। 🔥
আপনার OAuth flow-এর দুইটা আলাদা issue আছে।

Log:

```text
Not Found: /api/v1/auth/google/callback/
```

মানে Google সফলভাবে redirect করছে, কিন্তু Django-তে এই URL-এর কোনো endpoint নেই।

আপনার Google Console এ আছে:

```text
http://localhost:8000/api/v1/auth/google/callback/
```

কিন্তু Django URL তৈরি করেননি।

---

## এখন বুঝুন বর্তমান Flow

এখন:

```text
Google Login

↓

Google Redirect

↓

/api/v1/auth/google/callback/   ❌ 404

↓

POST /api/v1/auth/google/
```

কিন্তু আমরা Commit 7-এ শুধু:

```text
POST /api/v1/auth/google/
```

বানিয়েছি।

Callback endpoint বানাইনি।

---

# Fix: Callback API তৈরি করুন

## Step 1 — views.py

Add করুন:

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .factory import get_oauth_provider
from .services.oauth import OAuthAuthenticationService



class GoogleCallbackView(APIView):


    def get(self, request):

        code = request.query_params.get(
            "code"
        )


        if not code:
            return Response(
                {
                    "error": "Code missing"
                },
                status=400
            )


        provider = get_oauth_provider(
            "google"
        )


        service = OAuthAuthenticationService(
            provider
        )


        result = service.authenticate(
            code
        )


        user = result["user"]


        return Response({

            "user": {

                "id": str(user.id),

                "email": user.email,

                "full_name": user.full_name

            },

            "tokens": result["tokens"]

        })
```

---

# Step 2 — urls.py

`authentication/urls.py`

Update:

```python
from django.urls import path

from .views import (
    GoogleLoginView,
    GoogleCallbackView
)



urlpatterns = [

    path(
        "google/",
        GoogleLoginView.as_view(),
        name="google-login"
    ),


    path(
        "google/callback/",
        GoogleCallbackView.as_view(),
        name="google-callback"
    ),

]
```

---

# এখন URL দুইটা থাকবে

## Frontend login endpoint:

```http
POST

/api/v1/auth/google/
```

---

## Google redirect endpoint:

```http
GET

/api/v1/auth/google/callback/
```

---

# Important: Code decode সমস্যা

আপনার log:

```
code=4%2F0AdkVLP...
```

এটা ঠিক আছে।

Django:

```python
request.query_params.get("code")
```

নিজে decode করে দিবে।

আপনার manually decode করার দরকার নেই।

---

# এখন Test

Server restart:

```bash
CTRL + C

python manage.py runserver
```

তারপর:

```python
provider.get_authorization_url()
```

Browser open করুন।

Login করুন।

এবার redirect হবে:

```
/api/v1/auth/google/callback/?code=xxxx
```

এবং আর 404 হবে না।

---

# Expected Response

```json
{
    "user": {
        "id": "uuid",
        "email": "your@gmail.com",
        "full_name": "Your Name"
    },
    "tokens": {
        "access": "eyJ...",
        "refresh": "eyJ..."
    }
}
```

---

একটা architectural note:

Production project-এ সাধারণত আমরা:

```
GET /auth/google/start/
        |
        |
Google
        |
        |
GET /auth/google/callback/
        |
        |
JWT Response
```

এই pattern ব্যবহার করি।

পরের Commit-এ আমরা এটাকে clean করব:

**Commit 8 → OAuth Error Handling + Callback Cleanup** 🚀


----------
চমৎকার 🔥
আপনার OAuth project এখন পর্যন্ত:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration
✅ Commit 5 — Google OAuth Provider
✅ Commit 6 — OAuth Authentication Service
✅ Commit 7 — Google OAuth API Endpoint + Callback

এখন আমাদের code কাজ করছে, কিন্তু production-ready না।

বর্তমানে সমস্যা:

* Google error সরাসরি expose হচ্ছে
* Service exception handle করছে না
* View-তে try/except নেই
* Debug information user-কে দেখানো হতে পারে

এখন এগুলো ঠিক করব।

---

# Commit 8

```text
feat(oauth): improve oauth error handling
```

## Goal

আজ আমরা তৈরি করব:

✅ Custom OAuth Exception
✅ Google API Error Handling
✅ Service Layer Exception Handling
✅ Clean API Error Response
✅ Logging Foundation

---

# Commit 8 শেষে Structure

```text
apps/

└── authentication/

    ├── providers/

    │   └── google.py

    ├── services/

    │   └── oauth.py

    ├── exceptions.py        ⭐

    ├── views.py             ⭐

    ├── serializers.py

    └── urls.py
```

---

# Step 1 — Custom Exception তৈরি

File:

```text
apps/authentication/exceptions.py
```

Code:

```python
class OAuthException(Exception):

    def __init__(
        self,
        message,
        status_code=400,
        extra=None
    ):

        self.message = message

        self.status_code = status_code

        self.extra = extra or {}

        super().__init__(message)
```

---

এখন আমরা নিজের error তৈরি করতে পারব।

Example:

```python
raise OAuthException(
    "Google login failed"
)
```

---

# Step 2 — Google Provider Update

File:

```text
providers/google.py
```

Import:

```python
from apps.authentication.exceptions import (
    OAuthException
)
```

---

আগে:

```python
response.raise_for_status()
```

ছিল।

Replace করুন:

```python
if response.status_code != 200:

    raise OAuthException(

        message=
        "Google rejected the authorization code exchange.",

        status_code=response.status_code,

        extra=response.json()

    )
```

---

এখন Google error:

```json
{
 "error":"invalid_grant"
}
```

clean ভাবে handle হবে।

---

# Step 3 — Service Update

File:

```text
services/oauth.py
```

Import:

```python
from apps.authentication.exceptions import (
    OAuthException
)
```

---

`authenticate()` method:

আগে:

```python
token_data = self.provider.exchange_code(code)
```

এখন:

```python
try:

    token_data = (
        self.provider.exchange_code(code)
    )


except OAuthException:

    raise
```

---

কেন?

কারণ Service error hide করবে না।

Provider যেটা বলবে সেটা pass করবে।

---

# Step 4 — View Error Handling

File:

```text
views.py
```

Import:

```python
from rest_framework import status

from .exceptions import (
    OAuthException
)
```

---

`GoogleLoginView`

এবং

`GoogleCallbackView`

দুই জায়গায়:

```python
try:

    result = service.authenticate(
        code
    )


except OAuthException as e:


    return Response(

        {

            "error": {

                "message": e.message,

                "details": e.extra

            }

        },

        status=e.status_code

    )
```

---

# এখন Error Response হবে

আগে:

```json
{
 "error":
 "invalid_grant"
}
```

এখন:

```json
{
    "error": {

        "message":
        "Google rejected the authorization code exchange.",


        "details": {

            "error":
            "invalid_grant",

            "error_description":
            "Malformed auth code."

        }

    }
}
```

---

# Step 5 — Logging Add

`settings.py`

Add:

```python
LOGGING = {

    "version": 1,

    "handlers": {

        "console": {

            "class":
            "logging.StreamHandler"

        }

    },

    "loggers": {

        "oauth": {

            "handlers":
            ["console"],

            "level":
            "INFO"

        }

    }

}
```

---

Provider:

```python
import logging


logger = logging.getLogger(
    "oauth"
)
```

---

Error হলে:

```python
logger.error(
    response.json()
)
```

---

# এখন Architecture

আগে:

```text
Google Error

↓

Crash

↓

500 Error
```

এখন:

```text
Google Error

↓

OAuthException

↓

View Handler

↓

Clean JSON Response
```

---

# Test

Invalid code দিয়ে:

```json
{
 "code":"wrong-code"
}
```

Response:

```json
{
    "error":{
        "message":
        "Google rejected the authorization code exchange.",

        "details":{
            "error":"invalid_grant"
        }
    }
}
```

---

# Commit

```bash
git add .

git commit -m "feat(oauth): improve oauth error handling"
```

---

# Commit 8 Complete হলে আপনি শিখলেন:

✅ Production exception pattern
✅ Provider error isolation
✅ Clean API response
✅ Service error propagation
✅ Logging foundation

---

# Next Commit 9

পরের ধাপে:

```text
feat(oauth): add oauth account linking
```

করব।

মানে:

একজন user:

```
Email signup
      |
      |
Google login
```

দুইটা account merge হবে।

এটাই real-world SaaS/E-commerce project-এ লাগে। 🚀


--------
চমৎকার 🔥
আপনার OAuth implementation এখন production architecture-এর দিকে যাচ্ছে।

বর্তমান অবস্থা:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration
✅ Commit 5 — Google OAuth Provider
✅ Commit 6 — OAuth Authentication Service
✅ Commit 7 — Google OAuth API Endpoint + Callback
✅ Commit 8 — OAuth Error Handling

এখন আমরা খুব গুরুত্বপূর্ণ feature যোগ করব।

---

# Commit 9

```text id="7k931"
feat(oauth): add oauth account linking
```

## Goal

একই user যেন:

```
Email + Password Login
        |
        |
        +------ Google Login
```

দুইভাবে login করতে পারে।

---

## Real World Problem

ধরুন:

প্রথমে user signup করলো:

```text
email:
atiar@gmail.com

password:
123456
```

Database:

```
User
-----
id: 1
email: atiar@gmail.com
password: hashed
```

---

এরপর user Google দিয়ে login করলো:

Google দেয়:

```json
{
 "email":"atiar@gmail.com"
}
```

আমরা নতুন User create করলে:

```
User
-----
id:1
email:atiar@gmail.com


User
-----
id:2
email:atiar@gmail.com
```

❌ Duplicate account

---

আমাদের solution:

```
Google Account
        |
        |
        ↓

Existing User খুঁজবে

        |
        |
        ↓

Link করবে
```

---

# Commit 9 শেষে Structure

```text
apps/

└── authentication/

    ├── models.py              ⭐

    ├── selectors.py

    ├── services/

    │   └── oauth.py           ⭐

    ├── providers/

    │   └── google.py

    ├── exceptions.py

    └── views.py
```

---

# Step 1 — OAuth Account Model

আমরা আলাদা table রাখব।

কারণ:

একজন user এর multiple provider থাকতে পারে।

Example:

```
User

 |
 |
 +--- Google
 |
 +--- Github
 |
 +--- Microsoft
```

---

Create:

```text id="3v9wq"
authentication/models.py
```

---

Code:

```python
from django.db import models

from django.conf import settings



class OAuthAccount(models.Model):


    PROVIDER_CHOICES = (

        ("google", "Google"),

        ("github", "Github"),

    )


    user = models.ForeignKey(

        settings.AUTH_USER_MODEL,

        on_delete=models.CASCADE,

        related_name="oauth_accounts"

    )


    provider = models.CharField(

        max_length=50,

        choices=PROVIDER_CHOICES

    )


    provider_user_id = models.CharField(

        max_length=255

    )


    email = models.EmailField()


    created_at = models.DateTimeField(

        auto_now_add=True

    )


    class Meta:

        unique_together = (

            "provider",

            "provider_user_id"

        )
```

---

# কেন provider_user_id?

Email দিয়ে সবসময় identity ধরা যায় না।

Google দেয়:

```json
{
"sub":"1092837464893"
}
```

এই:

```
sub
```

হলো Google-এর unique ID।

---

# Database হবে:

```
oauth_account

id
user_id
provider
provider_user_id
email
```

---

# Step 2 — Migration

Run:

```bash
python manage.py makemigrations
```

তারপর:

```bash
python manage.py migrate
```

---

# Step 3 — Selector Add

File:

```text
authentication/selectors.py
```

Add:

```python
from .models import OAuthAccount



def get_oauth_account(
    provider,
    provider_user_id
):

    try:

        return OAuthAccount.objects.get(

            provider=provider,

            provider_user_id=provider_user_id

        )


    except OAuthAccount.DoesNotExist:

        return None
```

---

# Step 4 — Service Update

File:

```text
services/oauth.py
```

Import:

```python
from apps.authentication.models import OAuthAccount

from apps.authentication.selectors import (
    get_oauth_account
)
```

---

# authenticate() update

আগে:

```python
normalized_data = (
    self.provider.normalize_user(
        user_data
    )
)
```

এখন:

```python
normalized_data = (
    self.provider.normalize_user(
        user_data
    )
)


provider_user_id = user_data.get(
    "sub"
)
```

---

তারপর:

```python
oauth_account = get_oauth_account(

    "google",

    provider_user_id

)
```

---

যদি account থাকে:

```python
if oauth_account:

    user = oauth_account.user
```

---

না থাকলে:

```python
else:

    user = self.get_or_create_user(
        normalized_data
    )


    OAuthAccount.objects.create(

        user=user,

        provider="google",

        provider_user_id=
        provider_user_id,

        email=
        normalized_data["email"]

    )
```

---

# এখন Flow

## First Google Login

```
Google
 |
 |
No OAuthAccount
 |
 |
Create User
 |
 |
Create OAuthAccount
```

---

## Second Google Login

```
Google
 |
 |
Find OAuthAccount
 |
 |
Return Existing User
```

---

# Step 5 — Test

Shell:

```bash
python manage.py shell
```

---

Check:

```python
from apps.authentication.models import OAuthAccount


OAuthAccount.objects.all()
```

Output:

```
<QuerySet [

<OAuthAccount:
google - atiar@gmail.com>

]>
```

---

# Database Relation

এখন:

```
User
 |
 |
 +----------------+
                  |
                  |
          OAuthAccount

          provider:
          google

          provider_user_id:
          109283746
```

---

# Commit

```bash
git add .

git commit -m "feat(oauth): add oauth account linking"
```

---

# Commit 9 Complete হলে আপনি শিখলেন:

✅ Social account table design
✅ Multiple OAuth provider architecture
✅ Account linking
✅ Duplicate user prevention
✅ Provider identity management

---

# Next Commit 10

পরের ধাপে:

```text
feat(oauth): add github oauth provider
```

করব।

এখানে দেখবেন:

Google Provider একই interface follow করে Github Provider add করা কত সহজ হয়।

এটাই Provider Pattern-এর আসল শক্তি। 🚀



-------------


খুব ভালো প্রশ্ন 🔥
এটা Commit 9-এর সবচেয়ে গুরুত্বপূর্ণ design decision।

আপনার প্রশ্ন:

```python
user = (
    self.get_or_create_user(
        normalized_data
    )
)
```

এটা কি লাগবে?

**উত্তর: সবসময় না।**
আপনার OAuth Account Linking design-এর উপর depend করবে।

---

## বর্তমান Commit 9 flow অনুযায়ী

আমরা এখন করছি:

```text
Google Login

        |
        |
Check OAuthAccount
        |
        |
Found?
  |
  |
 Yes ---------------- No
  |                   |
  |                   |
Existing User     Create User
                      |
                      |
              Create OAuthAccount
```

তাহলে code:

```python
oauth_account = get_oauth_account(
    "google",
    provider_user_id
)


if oauth_account:

    user = oauth_account.user


else:

    user = self.get_or_create_user(
        normalized_data
    )


    OAuthAccount.objects.create(
        user=user,
        provider="google",
        provider_user_id=provider_user_id,
        email=normalized_data["email"]
    )
```

এখানে:

```python
self.get_or_create_user()
```

**No case-এর জন্য লাগবে।**

---

## কিন্তু আরও ভালো production approach

আসলে আগে check করা উচিত:

1. OAuthAccount আছে কিনা
2. না থাকলে email দিয়ে existing User আছে কিনা
3. থাকলে link করা
4. না থাকলে নতুন User create করা

Flow:

```text
Google User

       |
       |
OAuthAccount আছে?
       |
       |
  +----+----+
  |         |
 Yes        No
  |         |
Login    Email দিয়ে User খোঁজ
              |
              |
        +-----+-----+
        |           |
       আছে        নেই
        |           |
     Link       Create User
```

---

তখন method হবে:

```python
def authenticate_google_user(data):

    oauth_account = get_oauth_account(
        "google",
        data["provider_user_id"]
    )


    if oauth_account:

        return oauth_account.user


    user = get_user_by_email(
        data["email"]
    )


    if user:

        create_oauth_account(
            user,
            data
        )

        return user


    user = create_user(data)


    create_oauth_account(
        user,
        data
    )


    return user
```

---

## তাহলে আপনার প্রশ্নের short answer:

### এই code:

```python
user = self.get_or_create_user(
    normalized_data
)
```

✅ লাগবে যদি:

* নতুন Google user হলে User create করতে চান।

❌ লাগবে না যদি:

* শুধু OAuthAccount থেকে user return করেন।

---

Production SaaS/E-commerce project-এর জন্য আমি দ্বিতীয় pattern recommend করব:

```text
OAuthAccount
        ↓
Existing User
        ↓
Link
        ↓
New User Create
```

কারণ এতে duplicate account হয় না।

আপনি যেহেতু mastery করতে চান, Commit 9-এ এই improved linking flow implement করাই ভালো হবে।

-------------
চমৎকার 🔥
এটার মানে আপনার **Commit 9-এর মূল feature কাজ করছে**।

আপনার output:

```python
>>> OAuthAccount.objects.all()
<QuerySet [<OAuthAccount: OAuthAccount object (1)>]>
```

মানে database-এ একটি OAuthAccount তৈরি হয়েছে।

অর্থাৎ flow:

```text id="oauthflow"
Google Login

        ↓

Google Provider

        ↓

OAuth Service

        ↓

Create User

        ↓

Create OAuthAccount ✅
```

---

কিন্তু এখন আপনার model-এর `__str__()` method নেই, তাই Django দেখাচ্ছে:

```text
<OAuthAccount: OAuthAccount object (1)>
```

এটা normal।

---

## Improve করুন

`authentication/models.py`

`OAuthAccount` model-এর ভিতরে add করুন:

```python
def __str__(self):
    return f"{self.provider} - {self.email}"
```

---

এখন shell:

```python
OAuthAccount.objects.all()
```

output হবে:

```text
<QuerySet [
    <OAuthAccount: google - atiar@gmail.com>
]>
```

---

আরো verify করুন:

### 1. Provider check

```python
account = OAuthAccount.objects.first()

account.provider
```

Output:

```text
'google'
```

---

### 2. Google ID check

```python
account.provider_user_id
```

Output:

```text
'109283746xxxx'
```

এটা Google-এর:

```json
{
 "sub":"109283746xxxx"
}
```

---

### 3. Related User check

```python
account.user
```

Output:

```text
<User: atiar@gmail.com>
```

---

### 4. Reverse relation test

কারণ আমরা দিয়েছি:

```python
related_name="oauth_accounts"
```

তাই:

```python
account.user.oauth_accounts.all()
```

Output:

```text
<QuerySet [
    <OAuthAccount: google - atiar@gmail.com>
]>
```

---

এখন আপনার database structure:

```
User
 |
 |
 +----------------+
                  |
                  |
           OAuthAccount

           provider = google

           provider_user_id = Google sub

           email = user email
```

---

Commit 9 verification complete ✅

এখন next logical step:

# Commit 10

```text
feat(oauth): add github oauth provider
```

এখানে আমরা দেখব:

একই Service:

```text
OAuthAuthenticationService
          |
          |
   +------+------+
   |             |
Google       Github
Provider     Provider
```

কোনো service code change না করে নতুন provider add করা যায়।

এটাই Provider Pattern mastery। 🚀


--------

চমৎকার 🔥
আপনি এখন OAuth-এর সবচেয়ে মজার জায়গায় আসছেন — **Multiple OAuth Provider Architecture**।

এখন পর্যন্ত:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration
✅ Commit 5 — Google OAuth Provider
✅ Commit 6 — OAuth Authentication Service
✅ Commit 7 — Google OAuth API Endpoint + Callback
✅ Commit 8 — OAuth Error Handling
✅ Commit 9 — OAuth Account Linking

এখন আমরা দেখব কেন আমরা শুরু থেকেই:

```python
provider
```

আলাদা করেছি।

---

# Commit 10

```text
feat(oauth): add github oauth provider
```

## Goal

আজ আমরা add করব:

✅ GitHub OAuth App
✅ GitHub Provider Class
✅ Same Provider Interface
✅ Factory Update
✅ GitHub Login Support

সবচেয়ে গুরুত্বপূর্ণ:

**OAuth Service এক লাইনও change হবে না।**

---

# Current Architecture

এখন:

```text
OAuthAuthenticationService

            |
            |
    GoogleOAuthProvider
```

Commit 10 পরে:

```text
              OAuthAuthenticationService

                         |

              +----------+----------+

              |                     |

       GoogleProvider        GithubProvider
```

---

# Commit 10 শেষে Structure

```text
apps/

└── authentication/

    ├── providers/

    │   ├── google.py

    │   ├── github.py        ⭐

    │
    ├── factory.py           ⭐

    ├── services/

    │   └── oauth.py

    ├── models.py

    └── views.py
```

---

# Step 1 — GitHub OAuth App Create

যান:

```text
GitHub

↓

Settings

↓

Developer settings

↓

OAuth Apps

↓

New OAuth App
```

---

Fill:

Application name:

```text
ShopHub
```

Homepage URL:

Development:

```text
http://localhost:8000
```

---

Authorization callback URL:

```text
http://localhost:8000/api/v1/auth/github/callback/
```

---

Create করলে পাবেন:

```text
Client ID

Client Secret
```

---

# Step 2 — .env Update

Add করুন:

```env
GITHUB_CLIENT_ID=your_client_id

GITHUB_CLIENT_SECRET=your_client_secret

GITHUB_REDIRECT_URI=http://localhost:8000/api/v1/auth/github/callback/
```

---

# Step 3 — settings.py Update

Add:

```python
GITHUB_CLIENT_ID = env(
    "GITHUB_CLIENT_ID"
)


GITHUB_CLIENT_SECRET = env(
    "GITHUB_CLIENT_SECRET"
)


GITHUB_REDIRECT_URI = env(
    "GITHUB_REDIRECT_URI"
)
```

---

# Step 4 — Github Provider Create

Create:

```text
apps/authentication/providers/github.py
```

---

Code:

```python
import httpx

from django.conf import settings



class GithubOAuthProvider:


    AUTHORIZATION_URL = (
        "https://github.com/login/oauth/authorize"
    )


    TOKEN_URL = (
        "https://github.com/login/oauth/access_token"
    )


    USER_URL = (
        "https://api.github.com/user"
    )


    EMAIL_URL = (
        "https://api.github.com/user/emails"
    )
```

---

# Step 5 — Authorization URL

Add:

```python
def get_authorization_url(self):

    params = {

        "client_id":
        settings.GITHUB_CLIENT_ID,

        "redirect_uri":
        settings.GITHUB_REDIRECT_URI,

        "scope":
        "user:email",

    }


    return str(
        httpx.URL(
            self.AUTHORIZATION_URL,
            params=params
        )
    )
```

---

# Step 6 — Exchange Code

Add:

```python
def exchange_code(
    self,
    code
):


    data = {

        "client_id":
        settings.GITHUB_CLIENT_ID,


        "client_secret":
        settings.GITHUB_CLIENT_SECRET,


        "code":
        code,


        "redirect_uri":
        settings.GITHUB_REDIRECT_URI

    }


    headers = {

        "Accept":
        "application/json"

    }


    response = httpx.post(

        self.TOKEN_URL,

        data=data,

        headers=headers

    )


    response.raise_for_status()


    return response.json()
```

---

GitHub response:

```json
{
 "access_token":"gho_xxxxx",
 "token_type":"bearer"
}
```

---

# Step 7 — User Info

Add:

```python
def get_user_info(
    self,
    access_token
):


    headers = {

        "Authorization":
        f"Bearer {access_token}"

    }


    response = httpx.get(

        self.USER_URL,

        headers=headers

    )


    response.raise_for_status()


    return response.json()
```

---

GitHub data:

```json
{
"id":12345,
"login":"atiar",
"name":"Md Atiar",
"avatar_url":"..."
}
```

---

# Step 8 — Email Fetch

GitHub email private হতে পারে।

তাই:

```python
def get_email(
    self,
    access_token
):

    headers = {

        "Authorization":
        f"Bearer {access_token}"

    }


    response = httpx.get(

        self.EMAIL_URL,

        headers=headers

    )


    response.raise_for_status()


    emails = response.json()


    for email in emails:

        if email["primary"]:

            return email["email"]


    return None
```

---

# Step 9 — Normalize

Google দিয়েছিল:

```python
{
email,
full_name,
profile_image
}
```

GitHub-ও একই format দিতে হবে।

Add:

```python
def normalize_user(
    self,
    user_data,
    email
):


    return {

        "email": email,

        "full_name":
        user_data.get(
            "name"
        )
        or user_data.get(
            "login"
        ),


        "profile_image":
        user_data.get(
            "avatar_url"
        ),

        "provider_user_id":
        str(
            user_data.get(
                "id"
            )
        )

    }
```

---

# Step 10 — Factory Update

File:

```text
authentication/factory.py
```

Update:

```python
from apps.authentication.providers.github import (
    GithubOAuthProvider
)



def get_oauth_provider(provider):


    if provider == "google":

        return GoogleOAuthProvider()


    if provider == "github":

        return GithubOAuthProvider()


    raise ValueError(
        "Unsupported provider"
    )
```

---

# Important

এখন:

```python
service.authenticate()
```

এর ভিতরে কোনো change লাগবে না।

কারণ:

Google:

```python
exchange_code()
normalize_user()
```

Github:

```python
exchange_code()
normalize_user()
```

একই interface।

---

# Test

Shell:

```bash
python manage.py shell
```

---

Test:

```python
from apps.authentication.factory import get_oauth_provider


provider = get_oauth_provider(
    "github"
)


provider.get_authorization_url()
```

Output:

```text
https://github.com/login/oauth/authorize?client_id=xxx
```

---

# Commit

```bash
git add .

git commit -m "feat(oauth): add github oauth provider"
```

---

# Commit 10 Complete হলে আপনি শিখলেন:

✅ Multiple OAuth Provider
✅ Provider Pattern
✅ Open/Closed Principle
✅ GitHub OAuth Flow
✅ Same Service Reuse

---

Next Commit 11:

```text
feat(oauth): create generic oauth callback system
```

এখানে Google/GitHub আলাদা callback না রেখে:

```text
/auth/{provider}/callback/
```

একটা dynamic system বানাব।

এটা বড় SaaS project-এ ব্যবহার হয়। 🚀


----------------


চমৎকার 🔥
Commit 10 শুরু করছি।

আপনার বর্তমান progress:

✅ Commit 1 — Custom User Model
✅ Commit 2 — BaseModel Architecture
✅ Commit 3 — JWT Authentication
✅ Commit 4 — Google OAuth Configuration
✅ Commit 5 — Google OAuth Provider
✅ Commit 6 — OAuth Authentication Service
✅ Commit 7 — Google OAuth API Endpoint + Callback
✅ Commit 8 — OAuth Error Handling
✅ Commit 9 — OAuth Account Linking

এখন:

# Commit 10

```bash
feat(oauth): add github oauth provider
```

---

## Goal

আমরা এখন Google-এর মতো GitHub login add করব।

Final flow:

```text
User

 ↓

Github Login

 ↓

Github Authorization Code

 ↓

Github Provider

 ↓

OAuth Service

 ↓

User

 ↓

JWT Token
```

---

## Step 1 — GitHub OAuth App

GitHub এ যান:

```
Settings
    ↓
Developer settings
    ↓
OAuth Apps
    ↓
New OAuth App
```

Create করুন।

---

Application:

```
ShopHub
```

Homepage:

```
http://localhost:8000
```

Callback:

```
http://localhost:8000/api/v1/auth/github/callback/
```

---

আপনি পাবেন:

```
Client ID

Client Secret
```

---

# Step 2 — .env

Add:

```env
GITHUB_CLIENT_ID=xxxxxxxx

GITHUB_CLIENT_SECRET=xxxxxxxx

GITHUB_REDIRECT_URI=http://localhost:8000/api/v1/auth/github/callback/
```

---

# Step 3 — settings.py

Add:

```python
GITHUB_CLIENT_ID = env(
    "GITHUB_CLIENT_ID"
)


GITHUB_CLIENT_SECRET = env(
    "GITHUB_CLIENT_SECRET"
)


GITHUB_REDIRECT_URI = env(
    "GITHUB_REDIRECT_URI"
)
```

---

# Step 4 — Github Provider

Create:

```
authentication/providers/github.py
```

---

Code:

```python
import httpx

from django.conf import settings



class GithubOAuthProvider:


    AUTHORIZATION_URL = (
        "https://github.com/login/oauth/authorize"
    )


    TOKEN_URL = (
        "https://github.com/login/oauth/access_token"
    )


    USER_URL = (
        "https://api.github.com/user"
    )


    EMAIL_URL = (
        "https://api.github.com/user/emails"
    )
```

---

# Step 5 — Authorization URL

Add:

```python
def get_authorization_url(self):

    params = {

        "client_id":
        settings.GITHUB_CLIENT_ID,


        "redirect_uri":
        settings.GITHUB_REDIRECT_URI,


        "scope":
        "user:email",

    }


    url = httpx.URL(
        self.AUTHORIZATION_URL,
        params=params
    )


    return str(url)
```

---

# Step 6 — Exchange Code

Add:

```python
def exchange_code(
    self,
    code
):

    data = {

        "client_id":
        settings.GITHUB_CLIENT_ID,


        "client_secret":
        settings.GITHUB_CLIENT_SECRET,


        "code":
        code,


        "redirect_uri":
        settings.GITHUB_REDIRECT_URI

    }


    headers = {

        "Accept":
        "application/json"

    }


    response = httpx.post(

        self.TOKEN_URL,

        data=data,

        headers=headers

    )


    response.raise_for_status()


    return response.json()
```

---

# Step 7 — Get User

Add:

```python
def get_user_info(
    self,
    access_token
):


    headers = {

        "Authorization":
        f"Bearer {access_token}"

    }


    response = httpx.get(

        self.USER_URL,

        headers=headers

    )


    response.raise_for_status()


    return response.json()
```

---

# Step 8 — Get Email

GitHub email private হতে পারে।

তাই:

```python
def get_email(
    self,
    access_token
):


    headers = {

        "Authorization":
        f"Bearer {access_token}"

    }


    response = httpx.get(

        self.EMAIL_URL,

        headers=headers

    )


    response.raise_for_status()


    emails = response.json()


    for email in emails:

        if email["primary"]:

            return email["email"]


    return None
```

---

# Step 9 — Normalize Data

Google এবং Github একই format return করবে।

Add:

```python
def normalize_user(
    self,
    user_data,
    email
):


    return {

        "email": email,


        "full_name":

            user_data.get("name")

            or

            user_data.get("login"),


        "profile_image":

            user_data.get(
                "avatar_url"
            ),


        "provider_user_id":

            str(
                user_data.get(
                    "id"
                )
            )

    }
```

---

# Step 10 — Factory Update

`factory.py`

আগে:

```python
if provider == "google":

    return GoogleOAuthProvider()
```

Add:

```python
from apps.authentication.providers.github import (
    GithubOAuthProvider
)
```

তারপর:

```python
if provider == "github":

    return GithubOAuthProvider()
```

---

এখন:

```python
get_oauth_provider("google")
```

দিলে:

```
GoogleOAuthProvider
```

---

আর:

```python
get_oauth_provider("github")
```

দিলে:

```
GithubOAuthProvider
```

---

# Test

Shell:

```bash
python manage.py shell
```

Run:

```python
from apps.authentication.factory import get_oauth_provider


provider = get_oauth_provider(
    "github"
)


provider.get_authorization_url()
```

Expected:

```
https://github.com/login/oauth/authorize?client_id=xxxx
```

---

# Commit

সব ঠিক থাকলে:

```bash
git add .

git commit -m "feat(oauth): add github oauth provider"
```

---

Commit 10 complete হলে আপনার architecture:

```
                OAuth Service

                     |

          +----------+----------+

          |                     |

     Google Provider       Github Provider
```

একই service দিয়ে দুই provider handle হচ্ছে। 🔥

পরের Commit 11-এ আমরা এটাকে আরও clean করব:

```
/auth/{provider}/callback/
```

একটা dynamic callback system বানাব।


-----------









হ্যাঁ, **লাগবে**। তবে **Commit 10-এ provider class বানালেই GitHub login কাজ করবে না**। Frontend বা GitHub redirect করার জন্য endpoint দরকার।

আপনার এখন Google-এর মতো GitHub-এর জন্যও endpoint থাকবে।

## Minimum endpoints

### 1. Login endpoint (optional, যদি frontend authorization URL generate না করে)

```http
GET /api/v1/auth/github/login/
```

Response:

```json
{
    "authorization_url": "https://github.com/login/oauth/authorize?..."
}
```

---

### 2. Callback endpoint (required)

```http
GET /api/v1/auth/github/callback/?code=xxxx
```

Flow:

```text
GitHub
   │
   ▼
/github/callback/
   │
   ▼
GithubOAuthProvider
   │
   ▼
OAuthAuthenticationService
   │
   ▼
JWT Response
```

---

## Commit 10-এ কি Google-এর মতো View লাগবে?

হ্যাঁ, আপাতত লাগবে।

উদাহরণ:

```python
class GithubCallbackView(APIView):

    def get(self, request):
        code = request.query_params.get("code")

        provider = get_oauth_provider("github")
        service = OAuthAuthenticationService(provider)

        result = service.authenticate(code)

        return Response(result)
```

URL:

```python
urlpatterns = [
    path(
        "github/callback/",
        GithubCallbackView.as_view(),
        name="github-callback",
    ),
]
```

---

## কিন্তু একজন Senior Developer কী করবে?

আমি **Commit 11**-এ Google ও GitHub-এর জন্য আলাদা view রাখব না।

এভাবে করব:

```http
GET /api/v1/auth/<provider>/callback/
```

Examples:

```text
/api/v1/auth/google/callback/

/api/v1/auth/github/callback/

/api/v1/auth/microsoft/callback/
```

একটাই View:

```python
class OAuthCallbackView(APIView):

    def get(self, request, provider):
        provider_instance = get_oauth_provider(provider)

        service = OAuthAuthenticationService(provider_instance)

        return Response(
            service.authenticate(
                request.query_params["code"]
            )
        )
```

এতে নতুন provider (GitHub, Microsoft, Facebook) যোগ করতে শুধু:

* Provider class
* Factory registration

করলেই হবে। View বা Service আর পরিবর্তন করতে হবে না।

### তাই আমার পরামর্শ

* **Commit 10:** GitHub-এর জন্য আলাদা callback endpoint বানান (Google-এর মতো) যাতে flow পরিষ্কার বোঝেন।
* **Commit 11:** Refactor করে **একটি Generic OAuth Callback View** বানান। এটাই production-quality architecture।


ঠিক আছে 🔥
Commit 10-এ আমরা GitHub-এর জন্য **Google-এর মতো আলাদা endpoint** বানাব।

এখন architecture হবে:

```text
Google

GET /api/v1/auth/google/callback/

        ↓

GoogleOAuthProvider

        ↓

OAuthAuthenticationService


--------------------------------


Github

GET /api/v1/auth/github/callback/

        ↓

GithubOAuthProvider

        ↓

OAuthAuthenticationService
```

---

# Commit 10 (Part 2)

## Goal

Add:

✅ Github Login Endpoint
✅ Github Callback Endpoint
✅ Github URL Routing

---

## Step 1 — views.py

File:

```text
apps/authentication/views.py
```

Add:

```python
from .exceptions import OAuthException
from .factory import get_oauth_provider
from .services.oauth import OAuthAuthenticationService

from rest_framework.views import APIView
from rest_framework.response import Response



class GithubCallbackView(APIView):


    def get(self, request):

        code = request.query_params.get(
            "code"
        )


        if not code:

            return Response(
                {
                    "error": "Code missing"
                },
                status=400
            )


        try:

            provider = get_oauth_provider(
                "github"
            )


            service = OAuthAuthenticationService(
                provider
            )


            result = service.authenticate(
                code
            )


            user = result["user"]


            return Response({

                "user": {

                    "id": str(user.id),

                    "email": user.email,

                    "full_name": user.full_name

                },


                "tokens": result["tokens"]

            })


        except OAuthException as e:


            return Response(

                {

                    "error": {

                        "message": e.message,

                        "details": e.extra

                    }

                },

                status=e.status_code

            )
```

---

# Step 2 — urls.py

File:

```text
apps/authentication/urls.py
```

Update:

```python
from django.urls import path

from .views import (
    GoogleCallbackView,
    GithubCallbackView
)



urlpatterns = [


    path(

        "google/callback/",

        GoogleCallbackView.as_view(),

        name="google-callback"

    ),



    path(

        "github/callback/",

        GithubCallbackView.as_view(),

        name="github-callback"

    ),

]
```

---

এখন URL:

Google:

```http
GET

/api/v1/auth/google/callback/
```

Github:

```http
GET

/api/v1/auth/github/callback/
```

---

# Step 3 — Test Github Authorization URL

Shell:

```bash
python manage.py shell
```

Run:

```python
from apps.authentication.factory import get_oauth_provider


provider = get_oauth_provider(
    "github"
)


url = provider.get_authorization_url()


print(url)
```

Output:

```text
https://github.com/login/oauth/authorize?
client_id=xxxxx
&redirect_uri=http://localhost:8000/api/v1/auth/github/callback/
&scope=user:email
```

---

Browser-এ URL open করুন।

GitHub login করুন।

Redirect:

```text
http://localhost:8000/api/v1/auth/github/callback/?code=xxxx
```

---

Expected response:

```json
{
    "user": {
        "id": "uuid",
        "email": "user@gmail.com",
        "full_name": "Ati ar"
    },
    "tokens": {
        "access": "xxxxx",
        "refresh": "xxxxx"
    }
}
```

---

# Database check

```python
from apps.authentication.models import OAuthAccount


OAuthAccount.objects.all()
```

Expected:

```text
google - your@gmail.com

github - your@gmail.com
```

---

# Commit

সব ঠিক থাকলে:

```bash
git add .

git commit -m "feat(oauth): add github oauth callback endpoint"
```

---

Commit 10 শেষে আপনার structure:

```text
authentication/

├── providers/
│   ├── google.py
│   └── github.py
│
├── services/
│   └── oauth.py
│
├── views.py
│
├── urls.py
│
└── models.py
```

---

পরবর্তী **Commit 11** এ আমরা এই duplicate code remove করব:

```python
GoogleCallbackView
GithubCallbackView
```

দুটো বাদ দিয়ে বানাব:

```python
OAuthCallbackView
```

যেটা handle করবে:

```
/auth/google/callback/
/auth/github/callback/
/auth/microsoft/callback/
```

এটাই production SaaS pattern। 🚀


-----


চমৎকার 🔥
আপনার GitHub OAuth authorization URL তৈরি হয়েছে। এর মানে:

✅ GitHub Provider কাজ করছে
✅ Factory থেকে `github` provider পাওয়া যাচ্ছে
✅ Authorization URL generate হচ্ছে

এখন পরের step হলো **browser দিয়ে flow complete করা**।

---

## Step 1 — URL Browser-এ open করুন

এই URL:

```
https://github.com/login/oauth/authorize?client_id=Iv23li55Xshr5pBLIXjp&redirect_uri=http%3A%2F%2Flocalhost%3A8000%2Fapi%2Fv1%2Fauth%2Fgithub%2Fcallback%2F&scope=user%3Aemail
```

Browser-এ paste করুন।

---

## Step 2 — GitHub Login করুন

Login করার পরে GitHub permission চাইবে:

```
Authorize OAuth App
```

Allow করুন।

---

## Step 3 — Redirect হবে

আপনার callback URL:

```
http://localhost:8000/api/v1/auth/github/callback/
```

এভাবে:

```
http://localhost:8000/api/v1/auth/github/callback/?code=xxxxxxxx
```

আপনি terminal-এ Django log দেখবেন:

```
GET /api/v1/auth/github/callback/?code=xxxx
```

---

## Step 4 — Expected Response

সব ঠিক থাকলে:

```json
{
    "user": {
        "id": "uuid",
        "email": "your_github_email@gmail.com",
        "full_name": "Your Name"
    },
    "tokens": {
        "access": "eyJ...",
        "refresh": "eyJ..."
    }
}
```

---

## যদি Error আসে

সম্ভাব্য:

### 1. Email None

GitHub অনেক সময় email private রাখে।

Error:

```
email is required
```

তাহলে check করব:

```python
get_email()
```

---

### 2. Redirect mismatch

GitHub বলবে:

```
The redirect_uri is not associated with this application
```

তাহলে GitHub OAuth App settings এ check:

```
Authorization callback URL

=
http://localhost:8000/api/v1/auth/github/callback/
```

---

### 3. Token exchange error

যদি:

```
Bad credentials
```

আসে:

check:

```
GITHUB_CLIENT_ID
GITHUB_CLIENT_SECRET
```

---

এখন browser-এ authorize করে callback response দিন।
তারপর আমরা Commit 10 complete verify করব। 🚀


----------


হ্যাঁ, **লাগবে**। প্রকৃতপক্ষে Google-এর মতো GitHub-এরও **Login URL endpoint** থাকা উচিত।

আপনার Google-এর জন্য ideally দুইটা endpoint থাকা উচিত:

```text
GET  /api/v1/auth/google/login/
GET  /api/v1/auth/google/callback/
```

GitHub-এর জন্যও একই pattern:

```text
GET  /api/v1/auth/github/login/
GET  /api/v1/auth/github/callback/
```

---

## 1. views.py

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .factory import get_oauth_provider


class GithubLoginView(APIView):

    def get(self, request):

        provider = get_oauth_provider("github")

        return Response({
            "authorization_url": provider.get_authorization_url()
        })
```

---

## 2. urls.py

```python
from .views import (
    GithubLoginView,
    GithubCallbackView,
)

urlpatterns = [

    path(
        "github/login/",
        GithubLoginView.as_view(),
        name="github-login",
    ),

    path(
        "github/callback/",
        GithubCallbackView.as_view(),
        name="github-callback",
    ),
]
```

---

## 3. Test

Browser-এ যান:

```text
GET http://localhost:8000/api/v1/auth/github/login/
```

Response:

```json
{
    "authorization_url": "https://github.com/login/oauth/authorize?client_id=..."
}
```

তারপর ওই URL browser-এ open করুন।

---

## Professional Architecture

শেষে (Commit 11-এ) আমরা Google এবং GitHub দুটোর জন্য একই pattern রাখব:

```text
GET /api/v1/auth/google/login/
GET /api/v1/auth/google/callback/

GET /api/v1/auth/github/login/
GET /api/v1/auth/github/callback/
```

এবং পরে এগুলো refactor করে বানাব:

```text
GET /api/v1/auth/<provider>/login/
GET /api/v1/auth/<provider>/callback/
```

এটাই scalable architecture, যেখানে নতুন provider (Microsoft, Facebook, Apple) যোগ করতে শুধু নতুন Provider class যোগ করলেই হবে।


----------
খুব ভালো প্রশ্ন। **এটাই Google OAuth আর GitHub OAuth-এর flow বোঝার মূল জায়গা।**

উত্তর: **না, browser-based OAuth flow-তে GitHub login-এর সময় প্রথমে কিছু POST করতে হয় না।**

Flowটা দেখুন:

## Google (আপনার বর্তমান implementation)

```text
Frontend
    │
    ▼
GET /auth/google/login/
    │
    ▼
authorization_url
    │
    ▼
Browser → Google Login
    │
    ▼
Google redirects
    │
    ▼
GET /auth/google/callback/?code=xxxx
    │
    ▼
Backend internally POST করে
https://oauth2.googleapis.com/token
```

খেয়াল করুন, **frontend কখনও Google token endpoint-এ POST করে না**। Backend করে।

---

## GitHub

একই flow:

```text
Frontend
    │
    ▼
GET /auth/github/login/
    │
    ▼
authorization_url
    │
    ▼
Browser → GitHub Login
    │
    ▼
GitHub redirects
    │
    ▼
GET /auth/github/callback/?code=xxxx
    │
    ▼
Backend internally POST করে
https://github.com/login/oauth/access_token
```

অর্থাৎ **GitHub-ও callback-এ `code` পাঠায়**, আর আপনার `GithubOAuthProvider.exchange_code()` সেই `code` দিয়ে GitHub token endpoint-এ POST করে।

---

## তাহলে Google-এর POST `/auth/google/` কেন বানিয়েছিলাম?

সেটা ছিল **SPA (React/Next.js)** pattern।

Flow:

```text
React

↓

Google JS SDK

↓

code পায়

↓

POST /api/v1/auth/google/

{
    "code": "xxxx"
}
```

এখানে callback URL frontend handle করে, তারপর backend-এ code পাঠায়।

---

## GitHub-এর জন্য কোনটা ব্যবহার করবেন?

দুইটা valid pattern আছে:

### Pattern 1 (Server-side OAuth) ✅

```text
GET /auth/github/login/
        ↓
GitHub
        ↓
GET /auth/github/callback/?code=xxxx
```

**এটাই আপনি এখন implement করছেন।**

---

### Pattern 2 (SPA / React)

```text
React
      ↓
GitHub Login
      ↓
React code পায়
      ↓
POST /auth/github/
{
   "code":"xxxx"
}
```

এটা Google-এর POST endpoint-এর মতো।

---

## আমি কোনটা recommend করি?

আপনি যেহেতু **Django Backend mastery** শিখছেন, আমি recommend করব:

* Google: **Login + Callback**
* GitHub: **Login + Callback**

অর্থাৎ:

```text
GET /api/v1/auth/google/login/
GET /api/v1/auth/google/callback/

GET /api/v1/auth/github/login/
GET /api/v1/auth/github/callback/
```

এরপর **Commit 11**-এ এগুলো refactor করে বানাব:

```text
GET /api/v1/auth/<provider>/login/
GET /api/v1/auth/<provider>/callback/
```

এটাই production-grade এবং সবচেয়ে scalable architecture।


----------

এটা খুব ভালো error। 👍 এটা দেখাচ্ছে যে **GoogleProvider** এবং **GithubProvider**-এর interface এক রকম নেই।

Error:

```text
GithubOAuthProvider.exchange_code() got an unexpected keyword argument 'redirect_uri'
```

এর মানে `OAuthAuthenticationService` এইভাবে call করছে:

```python
token_data = self.provider.exchange_code(
    code=code,
    redirect_uri=...
)
```

কিন্তু `GithubOAuthProvider`-এ method সম্ভবত এভাবে লেখা:

```python
def exchange_code(self, code):
    ...
```

অথবা

```python
def exchange_code(self, code, state=None):
    ...
```

তাই Python বলছে `redirect_uri` নামে parameter নেই।

---

## Solution 1 (আমি এটাই recommend করি) ✅

**সব Provider-এর interface একই রাখুন।**

Google:

```python
def exchange_code(
    self,
    code,
    redirect_uri,
):
    ...
```

GitHub:

```python
def exchange_code(
    self,
    code,
    redirect_uri,
):
    data = {
        "client_id": settings.GITHUB_CLIENT_ID,
        "client_secret": settings.GITHUB_CLIENT_SECRET,
        "code": code,
        "redirect_uri": redirect_uri,
    }

    ...
```

এতে `OAuthAuthenticationService` কোনো provider-specific logic জানবে না।

---

## Solution 2

Service-কে provider অনুযায়ী আলাদা call করানো:

```python
if provider == "google":
    ...
elif provider == "github":
    ...
```

❌ এটা করবেন না।

এতে Provider Pattern নষ্ট হয়ে যাবে।

---

## এখন আমি আপনার `OAuthAuthenticationService.authenticate()`-এর এই অংশটা দেখতে চাই:

বিশেষ করে যেখানে আছে:

```python
self.provider.exchange_code(...)
```

এবং

`GithubOAuthProvider.exchange_code()` method-টাও দেখান।

**এই দুইটা method paste করুন**, আমি exact কোন line change করতে হবে বলে দেব।

আমার ৯৯% ধারণা শুধু **method signature mismatch** হয়েছে।


--------------



হ্যাঁ, সমস্যাটা এখানেই। ✅

আপনার `OAuthAuthenticationService` সম্ভবত এভাবে call করছে:

```python
self.provider.exchange_code(
    code=code,
    redirect_uri=redirect_uri,
)
```

কিন্তু `GithubOAuthProvider`-এ method:

```python
def exchange_code(self, code):
```

শুধু `code` নিচ্ছে। তাই Python বলছে:

```text
unexpected keyword argument 'redirect_uri'
```

---

## Fix (Recommended)

Method signature Google Provider-এর মতো করুন।

```python
def exchange_code(
    self,
    code,
    redirect_uri,
):
    data = {
        "client_id": settings.GITHUB_CLIENT_ID,
        "client_secret": settings.GITHUB_CLIENT_SECRET,
        "code": code,
        "redirect_uri": redirect_uri,
    }

    headers = {
        "Accept": "application/json",
    }

    response = httpx.post(
        self.TOKEN_URL,
        data=data,
        headers=headers,
    )

    response.raise_for_status()

    return response.json()
```

এখানে `settings.GITHUB_REDIRECT_URI`-এর বদলে **parameter হিসেবে পাওয়া** `redirect_uri` ব্যবহার করছি। এতে সব provider-এর interface এক হবে।

---

## আরেকটা জিনিস check করুন

আপনার `OAuthAuthenticationService.authenticate()`-এ সম্ভবত আছে:

```python
self.provider.exchange_code(
    code=code,
    redirect_uri=settings.GITHUB_REDIRECT_URI,   # বা Google redirect URI
)
```

এখানে provider অনুযায়ী redirect URI পাঠাতে হবে।

Production-quality design হবে:

প্রতিটি provider-এর একটা property থাকবে:

```python
GoogleOAuthProvider.redirect_uri
GithubOAuthProvider.redirect_uri
```

আর Service করবে:

```python
token_data = self.provider.exchange_code(
    code=code,
    redirect_uri=self.provider.redirect_uri,
)
```

এতে Service কখনও জানবে না এটা Google নাকি GitHub।

---

### এখন আমাকে `OAuthAuthenticationService.authenticate()`-এর `exchange_code(...)` call-টা দেখান।

বিশেষ করে এই অংশ:

```python
token_data = self.provider.exchange_code(...)
```

এটা দেখলে পরের bug (যেটা GitHub-এ আসতে পারে) আগেই ঠিক করে দেব।


------------


অবশ্যই পারবেন। তবে আমি **Facebook Login** `dj-rest-auth` বা `allauth` দিয়ে না, **আপনার বর্তমান Provider Pattern Architecture**-এর উপর implement করব।

আপনার architecture এখন:

```text
authentication/

├── providers/
│   ├── google.py
│   ├── github.py
│   └── base.py
│
├── services/
│   └── oauth.py
│
├── factory.py
├── views.py
├── urls.py
├── models.py
└── exceptions.py
```

Facebook-ও এই architecture follow করবে। এতে Google, GitHub, Facebook, Microsoft—সব একই pattern-এ add করা যাবে।

---

# Facebook OAuth Mastery Roadmap

আমরা ১০টি commit-এ implement করব।

### Commit 1

```
feat(facebook): create facebook developer app
```

* Facebook Developer Account
* Create App
* Facebook Login product
* Callback URL
* App ID
* App Secret

---

### Commit 2

```
feat(facebook): add facebook configuration
```

* `.env`
* `settings.py`
* Facebook URLs
* Redirect URI

---

### Commit 3

```
feat(facebook): implement FacebookOAuthProvider
```

Methods:

```python
get_authorization_url()

exchange_code()

get_user_info()

normalize_user()
```

---

### Commit 4

```
feat(facebook): register provider in factory
```

```python
get_oauth_provider("facebook")
```

---

### Commit 5

```
feat(facebook): add facebook login endpoint
```

```
GET /api/v1/auth/facebook/login/
```

---

### Commit 6

```
feat(facebook): add facebook callback endpoint
```

```
GET /api/v1/auth/facebook/callback/
```

---

### Commit 7

```
feat(facebook): integrate oauth service
```

Existing

```python
OAuthAuthenticationService
```

reuse হবে।

---

### Commit 8

```
feat(facebook): add account linking
```

OAuthAccount table reuse হবে।

---

### Commit 9

```
feat(facebook): add error handling
```

* invalid code
* invalid token
* revoked app
* expired code

---

### Commit 10

```
refactor(oauth): generic provider endpoints
```

শেষে structure হবে

```
GET /auth/google/login/
GET /auth/google/callback/

GET /auth/github/login/
GET /auth/github/callback/

GET /auth/facebook/login/
GET /auth/facebook/callback/
```

এরপর refactor:

```
GET /auth/<provider>/login/

GET /auth/<provider>/callback/
```

---

## Facebook OAuth শেষে আপনি implement করতে পারবেন

* ✅ Google Login
* ✅ GitHub Login
* ✅ Facebook Login

একই architecture ব্যবহার করে।

---

এর পরে খুব সহজে add করা যাবে:

* Microsoft Login
* Apple Login
* LinkedIn Login
* Discord Login
* GitLab Login

কারণ আপনার **Provider Pattern** তখন সম্পূর্ণ reusable হবে।

**আমার পরামর্শ:** Google এবং GitHub শেষ করার পরই Facebook শুরু করুন। এতে একই pattern তিনবার implement করার ফলে OAuth architecture পুরোপুরি মাথায় বসে যাবে।
