অবশ্যই। আমি **একদম শুরু থেকে production level পর্যন্ত হাতে-ধরে শেখাতে পারি**।

তোমার লক্ষ্য যদি হয় **Django REST Framework + Next.js দিয়ে WhatsApp/Messenger-এর মতো Real-time Chat Application** তৈরি করা, তাহলে আমরা শুধু কোড লিখব না—প্রতিটি লাইনের কারণ, আর্কিটেকচার, এবং best practice-ও বুঝব।

## আমরা কী কী তৈরি করব

শেষে তোমার অ্যাপে থাকবে:

- ✅ User Registration
    
- ✅ Login (JWT + HttpOnly Cookie)
    
- ✅ Refresh Token
    
- ✅ Logout
    
- ✅ User Profile
    
- ✅ User Search
    
- ✅ One-to-One Chat
    
- ✅ Group Chat
    
- ✅ Real-time Messaging (WebSocket)
    
- ✅ Online/Offline Status
    
- ✅ Typing Indicator
    
- ✅ Seen/Delivered Status
    
- ✅ Edit/Delete Message
    
- ✅ Image/File Sharing
    
- ✅ Notifications
    
- ✅ Docker Deployment
    
- ✅ Nginx
    
- ✅ Redis
    
- ✅ PostgreSQL
    
- ✅ Production Deployment
    

---

# Course Roadmap (30+ Phases)

## Module 1 — Project Setup

### Phase 1

- Project Architecture
    
- Folder Structure
    
- DRF Setup
    
- Next.js Setup
    
- PostgreSQL Setup
    
- Redis Setup
    

### Phase 2

- Custom User Model
    
- User Manager
    
- Profile Model
    

### Phase 3

- JWT Authentication
    
- Login
    
- Register
    
- Logout
    
- Refresh Token
    
- HttpOnly Cookie
    

---

## Module 2 — Chat Backend

### Phase 4

- Conversation Model
    

### Phase 5

- Conversation Member
    

### Phase 6

- Message Model
    

### Phase 7

- Serializer
    

### Phase 8

- Message API
    

### Phase 9

- Conversation API
    

### Phase 10

- Pagination
    

---

## Module 3 — Django Channels

### Phase 11

- What is ASGI?
    

### Phase 12

- Channels Installation
    

### Phase 13

- Redis
    

### Phase 14

- WebSocket Basics
    

### Phase 15

- Consumer
    

### Phase 16

- Routing
    

### Phase 17

- Authentication Middleware
    

### Phase 18

- Connect
    

### Phase 19

- Send Message
    

### Phase 20

- Receive Message
    

---

## Module 4 — Next.js Frontend

### Phase 21

- Login Page
    

### Phase 22

- Chat Sidebar
    

### Phase 23

- Chat Window
    

### Phase 24

- WebSocket Connection
    

### Phase 25

- Send Message
    

### Phase 26

- Receive Live Message
    

---

## Module 5 — Advanced Features

### Phase 27

- Typing Indicator
    

### Phase 28

- Online Status
    

### Phase 29

- Seen Status
    

### Phase 30

- Delivered Status
    

### Phase 31

- Edit Message
    

### Phase 32

- Delete Message
    

### Phase 33

- Image Upload
    

### Phase 34

- File Upload
    

### Phase 35

- Voice Message
    

---

## Module 6 — Production

### Phase 36

- Docker
    

### Phase 37

- Nginx
    

### Phase 38

- Gunicorn + Daphne
    

### Phase 39

- Redis Production
    

### Phase 40

- Deployment
    

---

# শেখানোর স্টাইল

প্রতিটি Phase-এ আমি:

1. আগে Concept বুঝাব।
    
2. তারপর Architecture দেখাব।
    
3. Database Design করব।
    
4. Model লিখব।
    
5. Serializer লিখব।
    
6. View লিখব।
    
7. URL লিখব।
    
8. Frontend বানাব।
    
9. API Test করব।
    
10. Error হলে Debug করব।
    
11. শেষে Best Practice ও Production Tips দেব।
    

অর্থাৎ, শুধু "কোড কপি-পেস্ট" নয়—কেন এইভাবে লেখা হচ্ছে, কী সমস্যা সমাধান করছে, আর production-এ কীভাবে ব্যবহার করা হয়, সব ব্যাখ্যা করব।

---

### আমার পরামর্শ

তুমি যেহেতু আগে **DRF** এবং **Next.js App Router** নিয়ে ধাপে ধাপে শিখেছ, এবার এই Chat Application-টাকেও একইভাবে **Phase 1 → Phase 40** পর্যন্ত এগোনোই সবচেয়ে ভালো হবে।

আমরা **Phase 1** থেকে শুরু করব এবং কোনো Phase বাদ দেব না। প্রতিটি ফাইল, প্রতিটি কোড, প্রতিটি command এবং প্রতিটি ধারণা বিস্তারিতভাবে আলোচনা করব। এতে কোর্স শেষে তুমি নিজেই production-ready real-time chat application তৈরি করতে পারবে।


-----------

চমৎকার। আমরা **Phase 1** থেকে শুরু করছি। এই Phase শেষে তোমার কাছে একটি production-ready backend ও frontend project structure থাকবে, যা পরবর্তী সব Phase-এর ভিত্তি হবে।

---

# Phase 1: Project Architecture & Initial Setup

## Goal

এই Phase শেষে আমরা পাবো:

- ✅ Django REST Framework Project
    
- ✅ Next.js Project
    
- ✅ PostgreSQL Configuration
    
- ✅ Redis Configuration
    
- ✅ Docker সম্পর্কে ধারণা (এখন ব্যবহার করব না)
    
- ✅ Production Folder Structure
    
- ✅ Environment Variables
    
- ✅ Git Setup
    

---

# Step 1: Final Architecture

```text
chat-app/

├── backend/
│   ├── config/
│   ├── apps/
│   │   ├── users/
│   │   ├── chat/
│   │   ├── notifications/
│   │   └── common/
│   ├── media/
│   ├── static/
│   ├── requirements/
│   ├── .env
│   ├── manage.py
│   └── requirements.txt
│
├── frontend/
│   ├── app/
│   ├── components/
│   ├── lib/
│   ├── hooks/
│   ├── services/
│   ├── types/
│   ├── middleware.ts
│   ├── .env.local
│   └── package.json
│
└── README.md
```

---

# Step 2: Required Software

Install:

- Python 3.12+
    
- PostgreSQL 16+
    
- Redis
    
- Node.js 22 LTS
    
- Git
    
- VS Code
    

Ubuntu হলে:

```bash
sudo apt update

sudo apt install git

sudo apt install redis-server

sudo apt install postgresql
```

Python Version

```bash
python3 --version
```

Node Version

```bash
node -v
```

Redis Version

```bash
redis-server --version
```

Postgres Version

```bash
psql --version
```

---

# Step 3: Create Project

```
mkdir chat-app

cd chat-app
```

---

# Backend

```
mkdir backend

cd backend
```

Create Virtual Environment

```bash
python3 -m venv .venv
```

Activate

Ubuntu

```bash
source .venv/bin/activate
```

Windows

```bash
.venv\Scripts\activate
```

---

# Install Packages

```bash
pip install django

pip install djangorestframework

pip install psycopg

pip install python-dotenv

pip install pillow
```

অথবা একসাথে:

```bash
pip install django djangorestframework psycopg python-dotenv pillow
```

---

# Save Requirements

```bash
pip freeze > requirements.txt
```

---

# Create Django Project

```bash
django-admin startproject config .
```

এখন `backend/` এর ভিতরে থাকবে:

```text
backend/

config/

manage.py

requirements.txt
```

---

# Create Apps Folder

```text
backend/

apps/

config/

manage.py
```

---

# Create First Apps

```bash
python manage.py startapp users apps/users

python manage.py startapp common apps/common

python manage.py startapp chat apps/chat

python manage.py startapp notifications apps/notifications
```

ফোল্ডার স্ট্রাকচার:

```text
backend/

apps/

    users/

    chat/

    common/

    notifications/
```

---

# Step 4: Next.js Project

Root Folder-এ ফিরে আসুন:

```bash
cd ..
```

তারপর:

```bash
npx create-next-app@latest frontend
```

প্রশ্নগুলোর জন্য প্রস্তাবিত উত্তর:

```
TypeScript?            Yes
ESLint?                Yes
Tailwind CSS?          Yes
src directory?         No
App Router?            Yes
Turbopack?             Yes
Import Alias?          Yes (@/*)
```

---

# Step 5: Backend Environment File

`backend/.env`

```env
SECRET_KEY=change-me

DEBUG=True

ALLOWED_HOSTS=127.0.0.1,localhost

DB_NAME=chat_db

DB_USER=postgres

DB_PASSWORD=your_password

DB_HOST=localhost

DB_PORT=5432

REDIS_HOST=localhost

REDIS_PORT=6379
```

> **Note:** `DB_PASSWORD`-এ আপনার PostgreSQL-এর আসল password দিন।

---

# Step 6: Frontend Environment

`frontend/.env.local`

```env
NEXT_PUBLIC_API_URL=http://127.0.0.1:8000/api

NEXT_PUBLIC_WS_URL=ws://127.0.0.1:8000/ws
```

---

# Step 7: Git

```bash
git init
```

`.gitignore`

```text
.venv/

__pycache__/

*.pyc

.env

.env.local

node_modules/

.next/

media/

staticfiles/

.vscode/
```

---

# Step 8: Production Apps Overview

|App|Purpose|
|---|---|
|users|Authentication, Profile, JWT|
|chat|Conversations, Messages|
|notifications|Real-time notifications|
|common|BaseModel, utilities, shared code|

---

# Phase 1 Checklist

- ✅ Project folders তৈরি
    
- ✅ Python virtual environment
    
- ✅ Django project তৈরি
    
- ✅ DRF install
    
- ✅ Next.js project তৈরি
    
- ✅ PostgreSQL install
    
- ✅ Redis install
    
- ✅ Environment files
    
- ✅ Git initialize
    

---

## এই Phase-এ এখনো যা করিনি

ইচ্ছাকৃতভাবে এগুলো Phase 2 থেকে শুরু করব:

- Custom User Model
    
- Django settings configuration
    
- PostgreSQL database connection
    
- DRF configuration
    
- JWT authentication
    
- First API endpoint
    

এভাবে প্রতিটি Phase ছোট, পরিষ্কার এবং production-oriented থাকবে। পরবর্তী **Phase 2**-তে আমরা **Custom User Model**, `settings.py` configuration, PostgreSQL connection, এবং DRF-এর প্রাথমিক configuration সম্পূর্ণ করব।

---

দারুণ। এখন আমরা **Phase 2** শুরু করব।

এই Phase খুবই গুরুত্বপূর্ণ, কারণ **User Model** একবার তৈরি করার পরে production project-এ সাধারণত আর পরিবর্তন করা হয় না।

---

# Phase 2 — Django Project Configuration + Custom User Model

## Goal

এই Phase শেষে আমরা পাবো:

- ✅ Production Folder Structure
    
- ✅ Django Settings Configuration
    
- ✅ Apps Registration
    
- ✅ PostgreSQL Connection
    
- ✅ Environment Variables Load
    
- ✅ Custom User Model
    
- ✅ BaseModel
    
- ✅ First Migration
    

---

# Step 1: Backend Structure

শেষে backend এর structure হবে:

```text
backend/
│
├── apps/
│   ├── users/
│   │   ├── migrations/
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── managers.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   └── permissions.py
│   │
│   ├── chat/
│   ├── notifications/
│   └── common/
│
├── config/
│
├── manage.py
│
└── .env
```

---

# Step 2: Install Required Packages

```bash
pip install djangorestframework
pip install psycopg[binary]
pip install python-decouple
pip install pillow
```

Save requirements:

```bash
pip freeze > requirements.txt
```

---

# Step 3: Configure `settings.py`

প্রথমে `.env` থেকে configuration পড়ব।

```python
from decouple import config
```

### Secret Key

```python
SECRET_KEY = config("SECRET_KEY")
```

### Debug

```python
DEBUG = config("DEBUG", cast=bool)
```

### Allowed Hosts

```python
ALLOWED_HOSTS = config("ALLOWED_HOSTS").split(",")
```

---

# Step 4: Installed Apps

```python
INSTALLED_APPS = [
    # Django

    # Third Party
    "rest_framework",

    # Local Apps
    "apps.users",
    "apps.chat",
    "apps.notifications",
    "apps.common",
]
```

---

# Step 5: PostgreSQL Database

```python
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": config("DB_NAME"),
        "USER": config("DB_USER"),
        "PASSWORD": config("DB_PASSWORD"),
        "HOST": config("DB_HOST"),
        "PORT": config("DB_PORT"),
    }
}
```

---

# Step 6: Create BaseModel

`apps/common/models.py`

```python
from django.db import models


class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

এখন থেকে আমাদের সব Model এই BaseModel inherit করবে।

---

# Step 7: Create User Manager

`apps/users/managers.py`

```python
from django.contrib.auth.base_user import BaseUserManager


class UserManager(BaseUserManager):

    def create_user(self, email, password=None, **extra_fields):

        if not email:
            raise ValueError("Email is required")

        email = self.normalize_email(email)

        user = self.model(email=email, **extra_fields)

        user.set_password(password)

        user.save(using=self._db)

        return user

    def create_superuser(self, email, password=None, **extra_fields):

        extra_fields.setdefault("is_staff", True)
        extra_fields.setdefault("is_superuser", True)
        extra_fields.setdefault("is_active", True)

        return self.create_user(email, password, **extra_fields)
```

---

# Step 8: Custom User Model

`apps/users/models.py`

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

from apps.common.models import BaseModel
from .managers import UserManager


class User(AbstractUser, BaseModel):

    username = None

    email = models.EmailField(unique=True)

    first_name = models.CharField(max_length=150)

    last_name = models.CharField(max_length=150, blank=True)

    USERNAME_FIELD = "email"

    REQUIRED_FIELDS = []

    objects = UserManager()

    def __str__(self):
        return self.email
```

---

# Step 9: Tell Django to Use Custom User

`settings.py`

```python
AUTH_USER_MODEL = "users.User"
```

এটি **প্রথম migration-এর আগেই** সেট করতে হবে।

---

# Step 10: Make Migrations

```bash
python manage.py makemigrations

python manage.py migrate
```

---

# Step 11: Create Superuser

```bash
python manage.py createsuperuser
```

উদাহরণ:

```text
Email: admin@example.com
Password: ********
```

---

# Phase 2 শেষে আমরা কী পেলাম?

- ✅ Production settings
    
- ✅ PostgreSQL configuration
    
- ✅ `.env` support
    
- ✅ BaseModel
    
- ✅ Custom User Manager
    
- ✅ Custom User Model (email-based login)
    
- ✅ Database migrations
    
- ✅ Admin user
    

---

## কেন আমরা `AbstractUser` ব্যবহার করলাম?

Django-তে দুইটি প্রধান উপায় আছে:

|Option|কখন ব্যবহার করবেন|
|---|---|
|`AbstractUser`|বেশিরভাগ production application-এর জন্য; Django-এর built-in authentication সুবিধা বজায় থাকে|
|`AbstractBaseUser`|যখন authentication system সম্পূর্ণ নিজের মতো করে বানাতে চান|

আমাদের chat application-এর জন্য `AbstractUser` সবচেয়ে ভারসাম্যপূর্ণ এবং production-friendly পছন্দ।

---

### Phase 3 Preview

পরবর্তী Phase-এ আমরা করব:

- Django REST Framework configuration
    
- SimpleJWT setup
    
- JWT Authentication
    
- Login API
    
- Register API
    
- Refresh Token
    
- Logout API
    
- HttpOnly Cookie authentication
    

এখান থেকেই আমাদের authentication system বাস্তবে কাজ করা শুরু করবে।

---------

চমৎকার। **Phase 3** আমাদের পুরো প্রজেক্টের সবচেয়ে গুরুত্বপূর্ণ Phaseগুলোর একটি। এখান থেকে Authentication System তৈরি হবে।

আমরা **SimpleJWT + HttpOnly Cookie** ব্যবহার করব। এটি production-এ বহুল ব্যবহৃত এবং Next.js-এর সাথে ভালোভাবে কাজ করে।

---

# Phase 3 – JWT Authentication (Production Ready)

## Goal

এই Phase শেষে থাকবে:

- ✅ Django REST Framework Configuration
    
- ✅ SimpleJWT Setup
    
- ✅ Register API
    
- ✅ Login API
    
- ✅ Refresh Token API
    
- ✅ Logout API
    
- ✅ HttpOnly Cookie Authentication
    
- ✅ Current User API (`/me`)
    

---

# Authentication Flow

```text
          Next.js

             │

        Login Request

             │

             ▼

      Django REST Framework

             │

      Verify Email/Password

             │

             ▼

 Generate Access + Refresh Token

             │

   Set HttpOnly Cookies

             │

             ▼

       Browser Stores Cookies

             │

             ▼

 Future Requests Automatically
 Send Cookies
```

---

# Step 1: Install Packages

```bash
pip install djangorestframework-simplejwt
```

Update requirements:

```bash
pip freeze > requirements.txt
```

---

# Step 2: Update `INSTALLED_APPS`

```python
INSTALLED_APPS = [
    ...

    "rest_framework",

    "rest_framework_simplejwt",
]
```

---

# Step 3: DRF Configuration

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),
    "DEFAULT_PERMISSION_CLASSES": (
        "rest_framework.permissions.IsAuthenticated",
    ),
}
```

> পরে Cookie-based authentication ব্যবহার করার জন্য আমরা একটি **Custom Authentication Class** তৈরি করব। আপাতত JWTAuthentication রাখছি।

---

# Step 4: SimpleJWT Configuration

```python
from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "UPDATE_LAST_LOGIN": True,
}
```

---

# Step 5: Install Blacklist App

```python
INSTALLED_APPS += [
    "rest_framework_simplejwt.token_blacklist",
]
```

Run migration:

```bash
python manage.py migrate
```

---

# Step 6: Serializer

`apps/users/serializers.py`

```python
from rest_framework import serializers
from .models import User


class RegisterSerializer(serializers.ModelSerializer):

    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = [
            "email",
            "first_name",
            "last_name",
            "password",
        ]

    def create(self, validated_data):

        password = validated_data.pop("password")

        user = User(**validated_data)

        user.set_password(password)

        user.save()

        return user
```

---

# Step 7: Register API

`apps/users/views.py`

```python
from rest_framework.generics import CreateAPIView
from rest_framework.permissions import AllowAny

from .serializers import RegisterSerializer


class RegisterAPIView(CreateAPIView):

    serializer_class = RegisterSerializer

    permission_classes = [AllowAny]
```

---

# Step 8: URL

`apps/users/urls.py`

```python
from django.urls import path

from .views import RegisterAPIView

urlpatterns = [
    path("register/", RegisterAPIView.as_view()),
]
```

`config/urls.py`

```python
from django.urls import include, path

urlpatterns = [
    path("api/auth/", include("apps.users.urls")),
]
```

---

# Step 9: Login View

এখানে আমরা Django-এর `authenticate()` ব্যবহার করব।

```python
from django.contrib.auth import authenticate

user = authenticate(
    email=email,
    password=password,
)
```

যদি credentials ঠিক থাকে:

```python
from rest_framework_simplejwt.tokens import RefreshToken

refresh = RefreshToken.for_user(user)

access = refresh.access_token
```

---

# Step 10: Cookie Set

Production-এ Token body-তে না পাঠিয়ে Cookie-তে রাখব।

```python
response.set_cookie(
    key="access_token",
    value=str(access),
    httponly=True,
    secure=False,     # Production=True
    samesite="Lax",
)
```

Refresh Token:

```python
response.set_cookie(
    key="refresh_token",
    value=str(refresh),
    httponly=True,
    secure=False,
    samesite="Lax",
)
```

---

# Step 11: Logout

Logout-এর সময়:

```python
response.delete_cookie("access_token")

response.delete_cookie("refresh_token")
```

---

# Step 12: Current User API

```text
GET

/api/auth/me/
```

Return:

```json
{
    "id": 1,
    "email": "admin@example.com",
    "first_name": "Admin",
    "last_name": "User"
}
```

---

# Final Endpoints

|Method|Endpoint|Description|
|---|---|---|
|POST|`/api/auth/register/`|Register|
|POST|`/api/auth/login/`|Login|
|POST|`/api/auth/logout/`|Logout|
|POST|`/api/auth/refresh/`|Refresh Token|
|GET|`/api/auth/me/`|Current User|

---

# Folder Structure

```text
users/

models.py

views.py

urls.py

serializers.py

managers.py

permissions.py

authentication.py

services.py
```

> `authentication.py` এবং `services.py` এখনই রাখছি, কারণ পরবর্তী Phase-এ এগুলো ব্যবহার করে codebase আরও পরিষ্কার ও production-ready করব।

---

# এই Phase শেষে

আমাদের Authentication System প্রস্তুত হবে, কিন্তু **Next.js-এর জন্য সবচেয়ে গুরুত্বপূর্ণ অংশ এখনো বাকি আছে**।

বর্তমানে `JWTAuthentication` শুধু `Authorization: Bearer <token>` header থেকে token পড়ে। অথচ আমরা token **HttpOnly Cookie**-তে রাখব।

## তাই Phase 4-এ আমরা করব

- Custom Cookie JWT Authentication Class
    
- Cookie থেকে JWT পড়া
    
- Refresh Token Rotation
    
- Secure Login/Logout Flow
    
- Next.js-এর সাথে পূর্ণ integration
    

এটাই production-level DRF + Next.js authentication-এর মূল ভিত্তি।

---
ভালো প্রশ্ন। **Phase 3-এর Step 9–12-এ আমি শুধুমাত্র concept দেখিয়েছিলাম**, পুরো implementation দিইনি। তাই এগুলো এখন করলে project চলবে না।

Production project-এ **Step 9–12 আমরা সম্পূর্ণ code লিখে করব**, শুধু snippet না।

এগুলো হলো:

## Step 9: Login API (সম্পূর্ণ)

ফাইল:

```text
apps/users/views.py
```

এখানে আমরা লিখব:

- `LoginAPIView`
    
- `authenticate()`
    
- `RefreshToken.for_user()`
    
- Response তৈরি
    
- Cookie set
    

---

## Step 10: Cookie Set

Login সফল হলে:

```text
access_token
refresh_token
```

এই দুইটা **HttpOnly Cookie** হিসেবে browser-এ save হবে।

এখানে helper function ব্যবহার করব, যেমন:

```python
def set_auth_cookies(response, access, refresh):
    ...
```

যাতে একই code বারবার লিখতে না হয়।

---

## Step 11: Logout API

ফাইল:

```text
apps/users/views.py
```

`LogoutAPIView`

এখানে:

- Refresh Token blacklist
    
- Cookie delete
    
- Success response
    

---

## Step 12: Current User API

ফাইল:

```text
apps/users/views.py
```

`MeAPIView`

```http
GET /api/auth/me/
```

Return করবে:

```json
{
    "id": 1,
    "email": "admin@example.com",
    "first_name": "Admin",
    "last_name": "User"
}
```

---

# তাহলে এখন কী করব?

আমি Phase 3-কে **ছোট ছোট sub-phase**-এ ভাগ করতে চাই, যাতে কিছু বাদ না যায়।

### Phase 3.1

- Login Serializer
    
- Register Serializer
    
- User Serializer
    

### Phase 3.2

- Login API (Complete)
    
- Register API (Complete)
    

### Phase 3.3

- Cookie Helper
    
- Cookie Utils
    

### Phase 3.4

- Logout API
    

### Phase 3.5

- Me API
    

### Phase 3.6

- Testing with Postman
    

### Phase 3.7

- Testing with Next.js
    

এভাবে করলে প্রতিটি ফাইল সম্পূর্ণ হবে এবং production-ready থাকবে। মাঝপথে কোনো code বা logic বাদ যাবে না।

**আমি এই পদ্ধতিটাই অনুসরণ করব**, কারণ শুধু snippet দিলে পরে অনেক জায়গায় confusion হয়।


------------

চমৎকার। আমরা এখন **Phase 3.1** শুরু করছি।

এই Phase-এ **কোন API লিখব না**। শুধুমাত্র **Serializers** তৈরি করব, কারণ DRF-এ API বানানোর আগে Serializer ঠিকভাবে ডিজাইন করা সবচেয়ে গুরুত্বপূর্ণ।

---

# Phase 3.1 – User Serializers

## Goal

এই Phase শেষে থাকবে:

- ✅ UserSerializer
    
- ✅ RegisterSerializer
    
- ✅ LoginSerializer
    
- ✅ Serializer Validation
    

---

# Project Structure

```text
apps/
└── users/
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── urls.py
    ├── managers.py
    └── permissions.py
```

---

# Step 1: কেন Serializer ব্যবহার করি?

Serializer-এর কাজ:

- Model → JSON
    
- JSON → Model
    
- Input Validation
    
- Password Validation
    
- Email Validation
    

উদাহরণ:

Frontend থেকে আসবে:

```json
{
    "email": "atiar@example.com",
    "password": "12345678"
}
```

Serializer এটি validate করবে।

---

# Step 2: Import

`apps/users/serializers.py`

```python
from django.contrib.auth import authenticate
from rest_framework import serializers

from .models import User
```

---

# Step 3: UserSerializer

এটি শুধুমাত্র User information return করবে।

```python
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = (
            "id",
            "email",
            "first_name",
            "last_name",
            "created_at",
            "updated_at",
        )
        read_only_fields = fields
```

### Example Response

```json
{
    "id": 1,
    "email": "admin@example.com",
    "first_name": "Md",
    "last_name": "Atiar",
    "created_at": "2026-07-26T10:30:00Z",
    "updated_at": "2026-07-26T10:30:00Z"
}
```

---

# Step 4: RegisterSerializer

```python
class RegisterSerializer(serializers.ModelSerializer):

    password = serializers.CharField(
        write_only=True,
        min_length=8,
    )

    class Meta:
        model = User
        fields = (
            "email",
            "first_name",
            "last_name",
            "password",
        )
```

---

## কেন `write_only=True`?

```python
password = serializers.CharField(
    write_only=True
)
```

এর মানে:

Client password পাঠাতে পারবে।

কিন্তু Response-এ password কখনো যাবে না।

উদাহরণ:

### Request

```json
{
    "email": "atiar@example.com",
    "password": "12345678"
}
```

### Response

```json
{
    "email": "atiar@example.com"
}
```

Password নেই।

---

# Step 5: Register Validation

```python
def validate_email(self, value):
    if User.objects.filter(email=value).exists():
        raise serializers.ValidationError(
            "Email already exists."
        )
    return value
```

---

# Step 6: Create User

```python
def create(self, validated_data):
    password = validated_data.pop("password")

    user = User(**validated_data)

    user.set_password(password)

    user.save()

    return user
```

> `set_password()` অবশ্যই ব্যবহার করতে হবে। কখনোই `user.password = password` লিখবে না, কারণ তাতে password hash হবে না।

---

# Step 7: LoginSerializer

```python
class LoginSerializer(serializers.Serializer):

    email = serializers.EmailField()

    password = serializers.CharField(
        write_only=True
    )
```

এটি ModelSerializer নয়, কারণ Login কোনো Model তৈরি করে না।

---

# Step 8: Login Validation

```python
def validate(self, attrs):

    email = attrs.get("email")
    password = attrs.get("password")

    user = authenticate(
        username=email,
        password=password,
    )

    if user is None:
        raise serializers.ValidationError(
            "Invalid email or password."
        )

    attrs["user"] = user

    return attrs
```

> আমাদের `USERNAME_FIELD = "email"` হওয়ায় `authenticate(username=email, ...)` ব্যবহার করলেও Django email দিয়েই authenticate করবে।

---

# Step 9: Final `serializers.py`

```text
serializers.py

├── UserSerializer
├── RegisterSerializer
└── LoginSerializer
```

---

# Serializer Flow

```text
Frontend
     │
     ▼
Serializer
     │
Validate Email
     │
Validate Password
     │
authenticate()
     │
Return User
```

---

# Best Practices

✅ `UserSerializer` শুধুমাত্র output-এর জন্য।

✅ `RegisterSerializer` শুধুমাত্র registration-এর জন্য।

✅ `LoginSerializer` শুধুমাত্র login validation-এর জন্য।

✅ Password সবসময় `write_only=True` হবে।

✅ Password সবসময় `set_password()` দিয়ে save করবে।

---

# Phase 3.1 Checklist

- ✅ UserSerializer
    
- ✅ RegisterSerializer
    
- ✅ LoginSerializer
    
- ✅ Email Validation
    
- ✅ Password Hashing
    
- ✅ Login Validation
    

---

## পরবর্তী Phase (3.2)

এখন আমরা এই Serializers ব্যবহার করে সম্পূর্ণ API লিখব:

- `RegisterAPIView`
    
- `LoginAPIView`
    
- Proper JSON Response
    
- Success & Error Handling
    
- DRF Generic Views বনাম APIView—কখন কোনটি ব্যবহার করতে হবে
    
- Production-ready code structure (services/helpers আলাদা করে)
    

এখান থেকে authentication flow বাস্তবে কাজ করা শুরু করবে।

-----

দারুণ। এখন **Phase 3.2**-তে আমরা **Register API** এবং **Login API** সম্পূর্ণভাবে তৈরি করব।

> **নোট:** Production project-এ আমি **APIView** ব্যবহার করব, কারণ Login/Logout-এর মতো API-তে Cookie set, Custom Response, Token Generate ইত্যাদি করতে হয়। `CreateAPIView` শুধু Register-এর জন্য সহজ, কিন্তু Login-এর জন্য যথেষ্ট নয়।

---

# Phase 3.2 - Register & Login API

## Goal

এই Phase শেষে থাকবে:

- ✅ Register API
    
- ✅ Login API
    
- ✅ JWT Token Generate
    
- ✅ JSON Response
    
- ❌ Cookie এখনও নয় (Phase 3.3-এ করব)
    

---

# Folder Structure

```text
apps/
└── users/
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── urls.py
    └── services.py
```

---

# Step 1: `views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from rest_framework.permissions import AllowAny

from rest_framework_simplejwt.tokens import RefreshToken

from .serializers import (
    RegisterSerializer,
    LoginSerializer,
    UserSerializer,
)
```

---

# Step 2: Register API

```python
class RegisterAPIView(APIView):

    permission_classes = [AllowAny]

    def post(self, request):

        serializer = RegisterSerializer(data=request.data)

        serializer.is_valid(raise_exception=True)

        user = serializer.save()

        return Response(
            {
                "message": "Registration successful.",
                "user": UserSerializer(user).data,
            },
            status=status.HTTP_201_CREATED,
        )
```

---

## Register Request

```http
POST /api/auth/register/
```

Body

```json
{
    "email": "atiar@example.com",
    "first_name": "Md",
    "last_name": "Atiar",
    "password": "12345678"
}
```

---

## Register Response

```json
{
    "message": "Registration successful.",
    "user": {
        "id": 1,
        "email": "atiar@example.com",
        "first_name": "Md",
        "last_name": "Atiar"
    }
}
```

---

# Step 3: Login API

```python
class LoginAPIView(APIView):

    permission_classes = [AllowAny]

    def post(self, request):

        serializer = LoginSerializer(data=request.data)

        serializer.is_valid(raise_exception=True)

        user = serializer.validated_data["user"]

        refresh = RefreshToken.for_user(user)

        access = refresh.access_token

        return Response(
            {
                "message": "Login successful.",
                "user": UserSerializer(user).data,
                "access": str(access),
                "refresh": str(refresh),
            },
            status=status.HTTP_200_OK,
        )
```

---

# Login Request

```http
POST /api/auth/login/
```

Body

```json
{
    "email": "atiar@example.com",
    "password": "12345678"
}
```

---

# Login Response

```json
{
    "message": "Login successful.",
    "user": {
        "id": 1,
        "email": "atiar@example.com",
        "first_name": "Md",
        "last_name": "Atiar"
    },
    "access": "eyJhbGc...",
    "refresh": "eyJhbGc..."
}
```

---

# Step 4: `urls.py`

```python
from django.urls import path

from .views import (
    RegisterAPIView,
    LoginAPIView,
)

urlpatterns = [
    path(
        "register/",
        RegisterAPIView.as_view(),
        name="register",
    ),

    path(
        "login/",
        LoginAPIView.as_view(),
        name="login",
    ),
]
```

---

# Step 5: Main URL

`config/urls.py`

```python
from django.urls import include, path

urlpatterns = [
    path(
        "api/auth/",
        include("apps.users.urls"),
    ),
]
```

---

# API Flow

## Register

```text
Frontend
     │
POST /register
     │
RegisterSerializer
     │
Validation
     │
Create User
     │
Response
```

---

## Login

```text
Frontend
      │
POST /login
      │
LoginSerializer
      │
authenticate()
      │
Generate JWT
      │
Return Token
```

---

# কেন এখন Response-এ Token দিচ্ছি?

এটি শুধুমাত্র JWT generation বোঝানোর জন্য।

Production-এ **এভাবে Token JSON body-তে ফেরত দেব না** যদি আমরা **HttpOnly Cookie** ব্যবহার করি।

Production flow হবে:

```text
Login

↓

Generate Token

↓

Set HttpOnly Cookie

↓

Return User Info

(No access token in JSON)
```

এটি আমরা **Phase 3.3**-এ implement করব।

---

# এই Phase শেষে Endpoints

|Method|Endpoint|Status|
|---|---|---|
|POST|`/api/auth/register/`|✅|
|POST|`/api/auth/login/`|✅|

---

# Phase 3.2 Checklist

- ✅ RegisterAPIView
    
- ✅ LoginAPIView
    
- ✅ JWT Token Generate
    
- ✅ URL Configuration
    
- ✅ Success Response
    
- ✅ Error Handling (`serializer.is_valid(raise_exception=True)`)
    

---

## একটি Production Improvement

এই code-এ `RefreshToken.for_user(user)` সরাসরি `views.py`-তে আছে। ছোট project-এ এটা ঠিক আছে, কিন্তু production project-এ business logic আলাদা রাখাই ভালো।

পরবর্তী Phase-এ আমরা:

- `services.py`-তে token generation নেব।
    
- `utils.py`-তে cookie helper তৈরি করব।
    
- Login API-তে **HttpOnly Cookie** set করব।
    
- Next.js থেকে `credentials: "include"` ব্যবহার করে authentication সম্পূর্ণ করব।
    

এতে `views.py` অনেক পরিষ্কার ও maintainable হবে।

------
দারুণ। এখন আমরা **Phase 3.3** করব।

এটি পুরো authentication system-এর **সবচেয়ে গুরুত্বপূর্ণ Phase**।

এখান থেকে আমরা **JSON-এ JWT token পাঠানো বন্ধ করব** এবং **HttpOnly Cookie** ব্যবহার করব। এটি production-level security-এর জন্য standard practice।

---

# Phase 3.3 - HttpOnly Cookie Authentication

## Goal

এই Phase শেষে থাকবে:

- ✅ Token Service
    
- ✅ Cookie Helper
    
- ✅ Login Cookie
    
- ✅ Refresh Cookie
    
- ✅ Secure Cookie Settings
    
- ✅ Clean Code Structure
    

---

# Folder Structure

```text
apps/
└── users/
    ├── services.py
    ├── utils.py
    ├── views.py
    ├── serializers.py
    ├── urls.py
    └── models.py
```

---

# Step 1: Token Service

**apps/users/services.py**

```python
from rest_framework_simplejwt.tokens import RefreshToken


def generate_tokens(user):
    refresh = RefreshToken.for_user(user)

    return {
        "access": str(refresh.access_token),
        "refresh": str(refresh),
    }
```

### কেন?

আগে Login View-এর মধ্যে ছিল:

```python
refresh = RefreshToken.for_user(user)
access = refresh.access_token
```

এখন business logic আলাদা হয়ে গেল।

---

# Step 2: Cookie Helper

**apps/users/utils.py**

```python
from django.conf import settings


def set_auth_cookies(response, access_token, refresh_token):
    response.set_cookie(
        key="access_token",
        value=access_token,
        httponly=True,
        secure=not settings.DEBUG,
        samesite="Lax",
        max_age=60 * 15,
    )

    response.set_cookie(
        key="refresh_token",
        value=refresh_token,
        httponly=True,
        secure=not settings.DEBUG,
        samesite="Lax",
        max_age=60 * 60 * 24 * 7,
    )
```

---

## Cookie Options

### httponly=True

```python
httponly=True
```

JavaScript Cookie পড়তে পারবে না।

✔ XSS Attack থেকে নিরাপদ।

---

### secure

```python
secure=not settings.DEBUG
```

Development

```text
False
```

Production

```text
True
```

HTTPS ছাড়া Cookie যাবে না।

---

### samesite

```python
samesite="Lax"
```

Development-এ ভালো।

Cross-domain হলে পরে `"None"` ব্যবহার করব (HTTPS সহ)।

---

### max_age

Access Token

```text
15 Minutes
```

Refresh Token

```text
7 Days
```

---

# Step 3: Update LoginAPIView

```python
from .services import generate_tokens
from .utils import set_auth_cookies
```

---

পুরনো code:

```python
refresh = RefreshToken.for_user(user)
access = refresh.access_token
```

Replace করুন:

```python
tokens = generate_tokens(user)
```

---

Response:

```python
response = Response(
    {
        "message": "Login successful.",
        "user": UserSerializer(user).data,
    }
)
```

Cookie Set:

```python
set_auth_cookies(
    response,
    tokens["access"],
    tokens["refresh"],
)
```

শেষে:

```python
return response
```

---

# Final LoginAPIView

```python
class LoginAPIView(APIView):

    permission_classes = [AllowAny]

    def post(self, request):

        serializer = LoginSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        user = serializer.validated_data["user"]

        tokens = generate_tokens(user)

        response = Response(
            {
                "message": "Login successful.",
                "user": UserSerializer(user).data,
            }
        )

        set_auth_cookies(
            response,
            tokens["access"],
            tokens["refresh"],
        )

        return response
```

---

# Browser Flow

```text
Login

↓

Email Password

↓

Authenticate

↓

Generate Token

↓

Set Cookie

↓

Browser Stores Cookie

↓

Future Request

↓

Cookie Automatically Sent
```

---

# Browser Cookies

Login করার পরে Browser-এ থাকবে

```text
access_token

refresh_token
```

JavaScript এগুলো পড়তে পারবে না।

---

# Next.js Login

```ts
await fetch("http://localhost:8000/api/auth/login/", {
  method: "POST",
  credentials: "include",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify(data),
});
```

## কেন `credentials: "include"`?

এটি না দিলে browser cookie receive করবে না এবং পরবর্তী request-এ cookie পাঠাবে না।

---

# Response

এখন Response হবে

```json
{
    "message": "Login successful.",
    "user": {
        "id": 1,
        "email": "atiar@example.com",
        "first_name": "Md",
        "last_name": "Atiar"
    }
}
```

কোন Token JSON-এ নেই।

---

# Authentication Flow

```text
Next.js

↓

POST Login

↓

DRF

↓

Generate JWT

↓

Set HttpOnly Cookie

↓

Browser Saves Cookie

↓

GET /me

↓

Cookie Automatically Sent

↓

User Authenticated
```

---

# Phase 3.3 Checklist

- ✅ `services.py`
    
- ✅ `generate_tokens()`
    
- ✅ `utils.py`
    
- ✅ `set_auth_cookies()`
    
- ✅ LoginAPIView update
    
- ✅ HttpOnly Cookie
    
- ✅ `credentials: "include"` বোঝা
    

---

# ⚠️ Production Note

এই Phase-এর শেষে একটি গুরুত্বপূর্ণ সমস্যা এখনও আছে।

আমরা Cookie-তে token **save** করছি, কিন্তু DRF-এর default `JWTAuthentication` শুধুমাত্র এই header খোঁজে:

```http
Authorization: Bearer <access_token>
```

কিন্তু আমাদের token থাকবে:

```http
Cookie: access_token=...
```

অর্থাৎ, Login সফল হলেও `GET /api/auth/me/` বা অন্য protected endpoint-এ DRF user-কে authenticate করতে পারবে না।

## তাই Phase 3.4-এ আমরা করব

- Custom `CookieJWTAuthentication` class
    
- Cookie থেকে access token পড়া
    
- DRF-কে Cookie-based authentication শেখানো
    
- `/me` endpoint তৈরি ও test
    
- Next.js-এর সাথে end-to-end authentication verification
    

এটি শেষ হলে আমাদের DRF + Next.js authentication production-ready হয়ে যাবে।

----
চমৎকার। **Phase 3.4** হলো আমাদের Authentication System-এর সবচেয়ে গুরুত্বপূর্ণ Phase।

এখন পর্যন্ত:

- ✅ Login হচ্ছে
    
- ✅ JWT Generate হচ্ছে
    
- ✅ Cookie-তে Save হচ্ছে
    

কিন্তু একটা সমস্যা আছে...

---

# সমস্যা কোথায়?

Browser Request পাঠাচ্ছে:

```http
GET /api/auth/me/

Cookie:
access_token=eyJhbGciOiJIUzI1NiIs...
refresh_token=eyJhbGciOiJIUzI1NiIs...
```

কিন্তু DRF-এর Default JWTAuthentication খুঁজে:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

অর্থাৎ,

```text
Browser
      │
      ▼
Cookie
      │
      ▼
DRF JWTAuthentication
      │
      ▼
Authorization Header খুঁজে
      │
      ▼
Not Found ❌
```

তাই আমাদের নিজের Authentication Class লিখতে হবে।

---

# Goal

এই Phase শেষে থাকবে

- ✅ CookieJWTAuthentication
    
- ✅ Cookie থেকে Token Read
    
- ✅ User Authenticate
    
- ✅ Me API
    
- ✅ Protected API
    

---

# Step 1

নতুন ফাইল তৈরি করো

```text
apps/users/authentication.py
```

---

# Step 2

Import

```python
from rest_framework_simplejwt.authentication import JWTAuthentication
from rest_framework_simplejwt.exceptions import InvalidToken
```

---

# Step 3

Class তৈরি

```python
class CookieJWTAuthentication(JWTAuthentication):

    def authenticate(self, request):

        pass
```

আমরা JWTAuthentication inherit করছি।

---

# Step 4

Cookie থেকে Access Token পড়ব

```python
access_token = request.COOKIES.get("access_token")
```

Browser যদি Cookie পাঠায়

```
access_token=eyJ...
```

তাহলে

```
access_token

↓

eyJ...
```

পাবো।

---

# Step 5

Cookie না থাকলে

```python
if access_token is None:
    return None
```

মানে

User Anonymous.

---

# Step 6

Token Validate

SimpleJWT already function দেয়।

```python
validated_token = self.get_validated_token(
    access_token
)
```

যদি Token Invalid হয়

```
401 Unauthorized
```

---

# Step 7

User বের করো

```python
user = self.get_user(validated_token)
```

এখন

```
validated_token

↓

User
```

---

# Step 8

Return

```python
return user, validated_token
```

DRF এখান থেকে

```
request.user
```

পাবে।

---

# পুরো Class

```python
from rest_framework_simplejwt.authentication import JWTAuthentication


class CookieJWTAuthentication(JWTAuthentication):

    def authenticate(self, request):

        access_token = request.COOKIES.get("access_token")

        if access_token is None:
            return None

        validated_token = self.get_validated_token(
            access_token
        )

        user = self.get_user(validated_token)

        return user, validated_token
```

---

# Step 9

settings.py

আগের

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),
}
```

Replace

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "apps.users.authentication.CookieJWTAuthentication",
    ),
}
```

এখন DRF Cookie দেখবে।

---

# Step 10

Current User API

views.py

```python
from rest_framework.permissions import IsAuthenticated
```

---

```python
class MeAPIView(APIView):

    permission_classes = [IsAuthenticated]

    def get(self, request):

        serializer = UserSerializer(request.user)

        return Response(serializer.data)
```

---

# Step 11

URL

```python
path(
    "me/",
    MeAPIView.as_view(),
    name="me",
)
```

---

# Step 12

Test

Login

```
POST

/api/auth/login/
```

↓

Browser Cookie Save করবে

↓

```http
GET /api/auth/me/
```

↓

Response

```json
{
    "id": 1,
    "email": "atiar@example.com",
    "first_name": "Md",
    "last_name": "Rahman"
}
```

---

# Flow

```text
Next.js

↓

Login

↓

Cookie Saved

↓

GET /me

↓

CookieJWTAuthentication

↓

Read Cookie

↓

Validate JWT

↓

Get User

↓

request.user

↓

Response
```

---

# Next.js

```typescript
const response = await fetch(
  "http://localhost:8000/api/auth/me/",
  {
    credentials: "include",
  }
);
```

`credentials: "include"` না দিলে Browser Cookie পাঠাবে না।

---

# Production Improvement (খুব গুরুত্বপূর্ণ)

উপরের `authenticate()` method কাজ করবে, কিন্তু production-এ আরও নিরাপদভাবে exception handle করা উচিত।

`authentication.py`

```python
from rest_framework_simplejwt.authentication import JWTAuthentication
from rest_framework_simplejwt.exceptions import InvalidToken


class CookieJWTAuthentication(JWTAuthentication):
    def authenticate(self, request):
        access_token = request.COOKIES.get("access_token")

        if not access_token:
            return None

        try:
            validated_token = self.get_validated_token(access_token)
            user = self.get_user(validated_token)
        except InvalidToken:
            return None

        return (user, validated_token)
```

এভাবে invalid বা expired token-এর কারণে server error হওয়ার ঝুঁকি কমে এবং DRF স্বাভাবিকভাবে request-টিকে unauthenticated হিসেবে বিবেচনা করতে পারে।

---

# Phase 3.4 Checklist

- ✅ `CookieJWTAuthentication`
    
- ✅ Cookie থেকে Access Token পড়া
    
- ✅ JWT Validation
    
- ✅ User Authentication
    
- ✅ `request.user`
    
- ✅ `MeAPIView`
    
- ✅ Protected Route
    

---

## Phase 3.5-এ আমরা করব

এখনও একটি গুরুত্বপূর্ণ feature বাকি আছে:

- Logout API
    
- Refresh Token Rotation
    
- Refresh Cookie Update
    
- Cookie Delete
    
- Token Blacklist
    
- Secure Session Management
    

এরপর authentication module সম্পূর্ণ production-ready হবে।

----

চমৎকার। এখন আমরা **Phase 3.5** শুরু করছি।

এটি Authentication Module-এর **শেষ গুরুত্বপূর্ণ অংশ**। এখানে আমরা **Logout**, **Refresh Token Rotation**, এবং **Secure Session Management** implement করব।

---

# Phase 3.5 - Logout & Refresh Token

## Goal

এই Phase শেষে থাকবে

- ✅ Logout API
    
- ✅ Refresh Token API
    
- ✅ Refresh Token Rotation
    
- ✅ Blacklist Old Refresh Token
    
- ✅ Delete Cookies
    
- ✅ Update Cookies
    
- ✅ Production Ready Session Management
    

---

# Authentication Flow

```text
            Login
               │
               ▼
      Access + Refresh Token
               │
               ▼
      HttpOnly Cookies
               │
               ▼
      Access Token Expired
               │
               ▼
       POST /refresh/
               │
               ▼
  New Access + New Refresh Token
               │
               ▼
     Update HttpOnly Cookies
```

---

# Step 1: Cookie Helper Update

`apps/users/utils.py`

আগের `set_auth_cookies()`-এর পাশাপাশি নতুন function যোগ করি।

```python
def delete_auth_cookies(response):
    response.delete_cookie("access_token")
    response.delete_cookie("refresh_token")
```

---

# Step 2: Logout API

`apps/users/views.py`

Import

```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from rest_framework_simplejwt.tokens import RefreshToken

from .utils import delete_auth_cookies
```

---

## LogoutAPIView

```python
class LogoutAPIView(APIView):

    permission_classes = [IsAuthenticated]

    def post(self, request):

        refresh_token = request.COOKIES.get("refresh_token")

        if refresh_token:
            try:
                token = RefreshToken(refresh_token)
                token.blacklist()
            except Exception:
                pass

        response = Response(
            {
                "message": "Logout successful."
            },
            status=status.HTTP_200_OK,
        )

        delete_auth_cookies(response)

        return response
```

---

# Step 3: Refresh API

Import

```python
from rest_framework_simplejwt.tokens import RefreshToken
from rest_framework_simplejwt.exceptions import TokenError
```

---

## RefreshAPIView

```python
from .services import generate_tokens
from .utils import set_auth_cookies


class RefreshAPIView(APIView):

    permission_classes = [AllowAny]

    def post(self, request):

        refresh_token = request.COOKIES.get("refresh_token")

        if not refresh_token:
            return Response(
                {
                    "detail": "Refresh token not found."
                },
                status=status.HTTP_401_UNAUTHORIZED,
            )

        try:

            refresh = RefreshToken(refresh_token)

            user = User.objects.get(id=refresh["user_id"])

            tokens = generate_tokens(user)

            response = Response(
                {
                    "message": "Token refreshed."
                }
            )

            set_auth_cookies(
                response,
                tokens["access"],
                tokens["refresh"],
            )

            return response

        except TokenError:

            return Response(
                {
                    "detail": "Invalid refresh token."
                },
                status=status.HTTP_401_UNAUTHORIZED,
            )
```

---

# Step 4: URL Update

`apps/users/urls.py`

```python
urlpatterns = [

    path(
        "register/",
        RegisterAPIView.as_view(),
    ),

    path(
        "login/",
        LoginAPIView.as_view(),
    ),

    path(
        "logout/",
        LogoutAPIView.as_view(),
    ),

    path(
        "refresh/",
        RefreshAPIView.as_view(),
    ),

    path(
        "me/",
        MeAPIView.as_view(),
    ),

]
```

---

# Step 5: Frontend Logout

```typescript
await fetch(
  "http://localhost:8000/api/auth/logout/",
  {
    method: "POST",
    credentials: "include",
  }
);
```

---

# Step 6: Frontend Refresh

```typescript
await fetch(
  "http://localhost:8000/api/auth/refresh/",
  {
    method: "POST",
    credentials: "include",
  }
);
```

---

# API Flow

## Logout

```text
Frontend

↓

POST /logout

↓

Read Refresh Cookie

↓

Blacklist Token

↓

Delete Cookies

↓

Success
```

---

## Refresh

```text
Frontend

↓

POST /refresh

↓

Read Refresh Cookie

↓

Validate Refresh Token

↓

Generate New Tokens

↓

Update Cookies

↓

Success
```

---

# Browser Cookies

### Before Logout

```text
access_token

refresh_token
```

### After Logout

```text
No Cookies
```

---

# Token Rotation

```text
Old Refresh Token

↓

Blacklist

↓

Generate New Refresh Token

↓

Save Cookie
```

এটি Replay Attack-এর ঝুঁকি কমায়।

---

# Authentication Lifecycle

```text
Register

↓

Login

↓

Cookie Saved

↓

Authenticated Requests

↓

Access Token Expired

↓

Refresh API

↓

New Cookies

↓

Continue

↓

Logout

↓

Blacklist Refresh Token

↓

Delete Cookies
```

---

# ⚠️ Production Improvements

উপরের `RefreshAPIView` কাজ করবে, কিন্তু production-এ আরও কিছু উন্নতি করা উচিত:

### 1. Refresh Serializer

`refresh_token` পড়া ও validation serializer-এর মাধ্যমে করা।

### 2. Service Layer

Token refresh logic `services.py`-তে রাখা।

### 3. Specific Exception Handling

`User.DoesNotExist` এবং `TokenError` আলাদাভাবে handle করা।

### 4. Cookie Settings

`path`, `domain`, `secure`, `samesite` সব cookie-তে consistent রাখা।

### 5. CORS

Next.js যদি আলাদা domain-এ থাকে, তাহলে:

```python
CORS_ALLOW_CREDENTIALS = True
```

এবং allowed origins সঠিকভাবে configure করতে হবে।

---

# Phase 3.5 Checklist

- ✅ Logout API
    
- ✅ Refresh API
    
- ✅ Refresh Token Rotation
    
- ✅ Refresh Token Blacklist
    
- ✅ Cookie Delete
    
- ✅ Cookie Update
    
- ✅ Secure Session Management
    

---

## 🎯 Authentication Module Review

এখন পর্যন্ত আমরা তৈরি করেছি:

- ✅ Custom User Model
    
- ✅ Register API
    
- ✅ Login API
    
- ✅ JWT Token Generation
    
- ✅ HttpOnly Cookies
    
- ✅ Cookie-based Authentication
    
- ✅ Current User API (`/me`)
    
- ✅ Logout API
    
- ✅ Refresh API
    

এখন আমাদের authentication system কার্যকর, তবে **Next.js-এর সাথে seamless integration**-এর জন্য আরও একটি Phase দরকার।

### Phase 3.6-এ আমরা করব

- `django-cors-headers` configuration
    
- CSRF configuration
    
- Next.js `credentials: "include"` setup
    
- Automatic refresh flow (401 → refresh → retry)
    
- Authentication testing (Postman + Next.js)
    
- Production security checklist
    

এটি শেষ হলে DRF + Next.js authentication সম্পূর্ণ production-ready হবে।

---

দারুণ। **Phase 3.6**-এ আমরা **Django REST Framework + Next.js Authentication Integration** করব।

> **গুরুত্বপূর্ণ:** Phase 3.5-এ আমি একটি সরল Refresh API দেখিয়েছিলাম। Production-এ Refresh Token Rotation, Blacklist এবং Cookie-based auth আরও সতর্কভাবে implement করতে হয়। এই Phase-এ আমরা সঠিক configuration করব, আর পরবর্তী Phase-এ frontend auto-refresh flow বানাব।

---

# Phase 3.6 - CORS, CSRF & Next.js Integration

## Goal

এই Phase শেষে থাকবে

- ✅ django-cors-headers
    
- ✅ CORS Configuration
    
- ✅ CSRF Configuration
    
- ✅ Next.js Cookie Integration
    
- ✅ credentials: "include"
    
- ✅ Local Development Setup
    
- ✅ Production Configuration
    

---

# Authentication Flow

```text
          Next.js

              │

credentials:"include"

              │

              ▼

     Browser Sends Cookie

              │

              ▼

          Django DRF

              │

 CookieJWTAuthentication

              │

              ▼

        request.user
```

---

# Step 1

Install package

```bash
pip install django-cors-headers
```

---

# Step 2

settings.py

```python
INSTALLED_APPS = [

    ...

    "corsheaders",

]
```

---

# Step 3

Middleware

**এটি খুব গুরুত্বপূর্ণ।**

```python
MIDDLEWARE = [

    "corsheaders.middleware.CorsMiddleware",

    "django.middleware.security.SecurityMiddleware",

    "django.contrib.sessions.middleware.SessionMiddleware",

    ...

]
```

`CorsMiddleware` অবশ্যই `CommonMiddleware`-এর আগে থাকবে।

---

# Step 4

Local Development

```python
CORS_ALLOWED_ORIGINS = [

    "http://localhost:3000",

]
```

যদি Next.js

```text
http://127.0.0.1:3000
```

এ চলে

তাহলে এটাও add করো

```python
CORS_ALLOWED_ORIGINS = [

    "http://localhost:3000",

    "http://127.0.0.1:3000",

]
```

---

# Step 5

Cookies পাঠাতে হলে

```python
CORS_ALLOW_CREDENTIALS = True
```

এটা না দিলে

```ts
credentials: "include"
```

কাজ করবে না।

---

# Step 6

CSRF Trusted Origin

```python
CSRF_TRUSTED_ORIGINS = [

    "http://localhost:3000",

    "http://127.0.0.1:3000",

]
```

---

# Step 7

Next.js Login

```ts
await fetch(
    "http://127.0.0.1:8000/api/auth/login/",
    {
        method: "POST",

        credentials: "include",

        headers: {
            "Content-Type": "application/json",
        },

        body: JSON.stringify({
            email,
            password,
        }),
    }
)
```

---

# কেন credentials include?

Without

```text
Request

↓

No Cookie

↓

Not Logged In
```

With

```text
Request

↓

Cookie Included

↓

Authenticated
```

---

# Step 8

Get Current User

```ts
await fetch(
    "http://127.0.0.1:8000/api/auth/me/",
    {
        credentials: "include",
    }
)
```

Browser automatically

```text
Cookie

↓

access_token

↓

refresh_token
```

send করবে।

---

# Step 9

Logout

```ts
await fetch(
    "http://127.0.0.1:8000/api/auth/logout/",
    {
        method: "POST",

        credentials: "include",
    }
)
```

---

# Step 10

Frontend API Helper

`frontend/lib/api.ts`

```ts
const API_URL = process.env.NEXT_PUBLIC_API_URL!;

export async function apiFetch(
  url: string,
  options: RequestInit = {}
) {
  return fetch(`${API_URL}${url}`, {
    ...options,
    credentials: "include",
    headers: {
      "Content-Type": "application/json",
      ...(options.headers || {}),
    },
  });
}
```

এখন সব request-এ `credentials: "include"` বারবার লিখতে হবে না।

---

# ব্যবহার

```ts
import { apiFetch } from "@/lib/api";

const response = await apiFetch("/auth/me/");
```

---

# Step 11

Environment

`.env.local`

```env
NEXT_PUBLIC_API_URL=http://127.0.0.1:8000/api
```

---

# Step 12

Production Cookie

Development

```python
response.set_cookie(

    secure=False,

    samesite="Lax",
)
```

Production

```python
response.set_cookie(

    secure=True,

    samesite="None",
)
```

HTTPS ছাড়া

```text
SameSite=None
```

কাজ করবে না।

---

# Request Flow

```text
Login

↓

Cookie Saved

↓

Browser

↓

GET /me

↓

Cookie Attached

↓

Authentication

↓

request.user
```

---

# Development vs Production

|Setting|Development|Production|
|---|---|---|
|DEBUG|True|False|
|Cookie Secure|False|True|
|SameSite|Lax|None (cross-origin) বা Lax (same-site)|
|HTTPS|No|Yes|
|credentials|include|include|
|CORS|localhost|Production Domain|

---

# ⚠️ গুরুত্বপূর্ণ Production Notes

এখানে দুটি বিষয় মনে রাখতে হবে:

### ১. CORS ≠ Authentication

অনেকে মনে করেন CORS configure করলেই authentication হয়ে যায়। আসলে:

- **CORS**: কোন origin request করতে পারবে।
    
- **Authentication**: User কে, সেটা যাচাই করে।
    

এগুলো আলাদা বিষয়।

---

### ২. CSRF

আমরা JWT Cookie ব্যবহার করছি। যদি authentication cookie-এর মাধ্যমে হয়, তাহলে **state-changing request (POST/PUT/PATCH/DELETE)**-এর জন্য CSRF protection বিবেচনা করা উচিত। অনেক production system আলাদা CSRF cookie + header ব্যবহার করে।

এই কোর্সে প্রথমে authentication flow সম্পূর্ণ করব, তারপর CSRF hardening আলাদা Phase-এ যোগ করব।

---

# Phase 3.6 Checklist

- ✅ django-cors-headers
    
- ✅ CORS Configuration
    
- ✅ CSRF Trusted Origins
    
- ✅ `credentials: "include"`
    
- ✅ API Helper
    
- ✅ Environment Variables
    
- ✅ Production Cookie Configuration
    

---

# 🎯 Authentication Module Status

এখন পর্যন্ত আমাদের আছে:

- ✅ Register
    
- ✅ Login
    
- ✅ Logout
    
- ✅ Refresh
    
- ✅ `/me`
    
- ✅ HttpOnly Cookie
    
- ✅ Cookie Authentication
    
- ✅ Next.js Integration
    
- ✅ CORS
    

---

## Phase 3.7-এ আমরা করব

এখন authentication ব্যবহার করা সহজ করতে frontend-এ একটি **Auth Layer** বানাব:

- `AuthContext`
    
- `useAuth()` Hook
    
- Route Protection
    
- Automatic 401 → Refresh → Retry
    
- Login Redirect
    
- Logout Redirect
    
- Next.js Middleware Integration
    

এটি শেষ হলে Next.js frontend থেকে authentication ব্যবহার করা অনেক সহজ হয়ে যাবে।

-------
চমৎকার। **Phase 3.7**-এ আমরা Next.js-এর Authentication Layer তৈরি করব।

> **গুরুত্বপূর্ণ:** Next.js App Router-এ **React Context দিয়ে Authentication State** এবং **Middleware দিয়ে Route Protection**—দুটোর আলাদা কাজ আছে। অনেক beginner এই দুটোকে গুলিয়ে ফেলে।

---

# Phase 3.7 – Next.js Authentication Layer

## Goal

এই Phase শেষে থাকবে

- ✅ API Client
    
- ✅ Auth Service
    
- ✅ Auth Context
    
- ✅ useAuth Hook
    
- ✅ Protected Routes
    
- ✅ Guest Routes
    
- ✅ Automatic Authentication Check
    

---

# Final Folder Structure

```text
frontend/

app/
│
├── (auth)/
│   ├── login/
│   └── register/
│
├── dashboard/
│
├── layout.tsx
│
providers/
│   └── auth-provider.tsx
│
hooks/
│   └── use-auth.ts
│
services/
│   └── auth.service.ts
│
lib/
│   └── api.ts
│
middleware.ts
```

---

# Authentication Flow

```text
Browser

↓

Login

↓

Cookie Saved

↓

Refresh Page

↓

AuthProvider

↓

GET /auth/me

↓

Authenticated

↓

Context Updated

↓

Entire App Knows User
```

---

# Step 1

আগের Phase-এ

```text
lib/api.ts
```

বানিয়েছি।

এখন

```text
services/auth.service.ts
```

তৈরি করি।

---

## auth.service.ts

```typescript
import { apiFetch } from "@/lib/api";

export async function getCurrentUser() {
  const response = await apiFetch("/auth/me/");

  if (!response.ok) {
    return null;
  }

  return response.json();
}
```

---

Login

```typescript
export async function login(data: {
  email: string;
  password: string;
}) {
  return apiFetch("/auth/login/", {
    method: "POST",
    body: JSON.stringify(data),
  });
}
```

---

Logout

```typescript
export async function logout() {
  return apiFetch("/auth/logout/", {
    method: "POST",
  });
}
```

---

# Step 2

Provider

```text
providers/

auth-provider.tsx
```

---

```tsx
"use client";
```

কারণ

React Context

↓

Client Component

---

Imports

```tsx
import {
    createContext,
    useEffect,
    useState,
} from "react";
```

---

# Step 3

State

```tsx
const [user, setUser] = useState(null);

const [loading, setLoading] = useState(true);
```

---

# Step 4

Startup

App Load হলে

```text
↓

GET /me

↓

Cookie

↓

User

↓

Context Update
```

---

```tsx
useEffect(() => {

    loadUser()

}, [])
```

---

loadUser

```tsx
async function loadUser() {

    const user = await getCurrentUser()

    setUser(user)

    setLoading(false)

}
```

---

# Step 5

Context

```tsx
<AuthContext.Provider

value={{

    user,

    loading,

    setUser,

}}

>

{children}

</AuthContext.Provider>
```

---

# Step 6

Root Layout

```tsx
app/layout.tsx
```

```tsx
<AuthProvider>

{children}

</AuthProvider>
```

এখন

পুরো App

↓

Authentication Access করতে পারবে।

---

# Step 7

Hook

```text
hooks/

use-auth.ts
```

---

```tsx
import { useContext } from "react";

import { AuthContext } from "@/providers/auth-provider";

export const useAuth = () => useContext(AuthContext);
```

---

Usage

```tsx
const {

    user,

    loading,

} = useAuth()
```

---

# Step 8

Dashboard

```tsx
"use client";

const {

    user,

    loading,

} = useAuth()

if(loading){

    return <>Loading...</>

}

return (

<h1>

{user.first_name}

</h1>

)
```

---

# Step 9

Login Page

```tsx
const response = await login(data)
```

Success

↓

```tsx
router.push("/dashboard")
```

---

# Step 10

Logout

```tsx
await logout()

router.replace("/login")
```

---

# Route Protection

```text
User

↓

Dashboard

↓

Authenticated ?

↓

Yes

↓

Show Dashboard

────────────

No

↓

Redirect Login
```

---

# Middleware

```text
middleware.ts
```

এখনও

Simple রাখবো।

Later

Refresh Token

Middleware

↓

Automatic Refresh

করবো।

---

# Auth Context Flow

```text
App Starts

↓

AuthProvider

↓

GET /me

↓

Cookie Authentication

↓

User

↓

Context

↓

All Components
```

---

# Why Context?

Without Context

```text
Navbar

↓

GET /me

Sidebar

↓

GET /me

Dashboard

↓

GET /me

Settings

↓

GET /me
```

৪টা Request।

---

With Context

```text
GET /me

↓

Context

↓

Navbar

↓

Sidebar

↓

Dashboard

↓

Settings
```

একটাই Request।

---

# Best Practice

❌ LocalStorage-এ User Token রাখবে না।

❌ Access Token React State-এ রাখবে না।

❌ Cookie JavaScript দিয়ে পড়ার চেষ্টা করবে না।

✅ শুধু `/me` API ব্যবহার করে user state maintain করবে।

---

# Phase 3.7 Checklist

- ✅ Auth Service
    
- ✅ Auth Provider
    
- ✅ React Context
    
- ✅ useAuth Hook
    
- ✅ Root Layout Integration
    
- ✅ Dashboard Authentication
    
- ✅ Login Flow
    
- ✅ Logout Flow
    

---

# ⚠️ Production Improvement

এখানে আমরা `loadUser()` শুধুমাত্র app start-এ call করছি। কিন্তু যদি:

- Access Token expire হয়ে যায়
    
- `/me` থেকে `401 Unauthorized` আসে
    

তাহলে user-কে সঙ্গে সঙ্গে logout করে দেওয়া উচিত নয়।

Production-এ flow হবে:

```text
GET /me
      │
      ▼
401 Unauthorized
      │
      ▼
POST /auth/refresh/
      │
      ▼
New Cookies
      │
      ▼
Retry GET /me
      │
      ▼
Success
```

এটি আমরা **Phase 3.8**-এ implement করব। সেটিই production-level automatic token refresh mechanism।


----

এটা স্বাভাবিক। কারণ **Phase 3.7-এর Step 2–10**-এ আমি অনেকগুলো React/Next.js concept একসাথে বলে ফেলেছি। তুমি যেহেতু **Next.js শিখছ**, তাই এগুলো ধীরে ধীরে বুঝানো উচিত।

**আমরা এখন Step 2–10 নতুন করে, একদম beginner থেকে বুঝব।**

---

# প্রথমে বড় ছবি বুঝো

Login হওয়ার পর কী হবে?

```text
User Login
      │
      ▼
Browser-এ Cookie Save
      │
      ▼
User Dashboard এ গেল
      │
      ▼
Dashboard কীভাবে জানবে User Login করেছে?
```

Dashboard-এর কাছে তো User-এর data নেই।

তাই Dashboard প্রথমে জিজ্ঞাসা করবে:

```text
GET /api/auth/me
```

DRF বলবে

```json
{
    "id":1,
    "email":"atiar@example.com",
    "first_name":"Atiar"
}
```

এখন Dashboard জানল User Login করেছে।

---

# কিন্তু সমস্যা

ধরো তোমার Application এ

```text
Navbar

Dashboard

Sidebar

Profile
```

চারটা Component আছে।

সবাই যদি

```text
GET /me
```

call করে?

তাহলে

```text
Navbar

↓

GET /me

Sidebar

↓

GET /me

Dashboard

↓

GET /me

Profile

↓

GET /me
```

একই API চারবার Call হবে।

এটা খারাপ Practice।

---

# Solution

একবার Call করো

তারপর সবাই Share করবে।

React এ এটাকে বলে

```text
Context
```

---

## Context কী?

ধরো তোমার বাসায়

একটা WiFi Router আছে।

```text
Router

↓

Internet
```

সব Mobile

Laptop

TV

একই Router ব্যবহার করছে।

Router নতুন Internet বানায় না।

শুধু Share করে।

React Context ঠিক একই।

```text
API

↓

User Data

↓

Context

↓

Navbar

↓

Dashboard

↓

Profile

↓

Sidebar
```

---

# Step 2

AuthProvider

এই Provider-এর কাজ

```text
User কে Save করা।
```

মানে

```tsx
const [user, setUser] = useState(null);
```

এর মানে

```text
user

↓

Initially

↓

null
```

কারণ

App Start হওয়ার সময়

আমরা জানি না

User Login করেছে কিনা।

---

## loading কেন?

```tsx
const [loading, setLoading] = useState(true);
```

মানে

```text
App

↓

Checking Login

↓

Loading
```

যখন

```text
GET /me
```

শেষ হবে

তখন

```tsx
loading = false
```

---

# Step 3

App Start

```text
App Open

↓

AuthProvider Start

↓

GET /me

↓

Cookie যায়

↓

Backend User পাঠায়

↓

setUser(user)

↓

loading=false
```

এটাই

```tsx
useEffect(...)
```

এর কাজ।

---

# useEffect কেন?

```tsx
useEffect(() => {

    loadUser()

}, [])
```

মানে

```text
App প্রথমবার Open

↓

একবার

↓

loadUser()
```

---

# loadUser()

```tsx
async function loadUser() {

    const user = await getCurrentUser()

    setUser(user)

}
```

মানে

```text
GET /me

↓

User পেলাম

↓

Save করলাম
```

---

# Step 4

Provider

```tsx
<AuthContext.Provider

value={

user

}

>

children

</AuthContext.Provider>
```

এটা বুঝতে হবে।

ধরো

```text
AuthProvider

↓

user
```

এখন

Navbar

Dashboard

Profile

সবাই

একই

```text
user
```

পাবে।

---

# Diagram

```text
           AuthProvider

                │

         user = Atiar

     ┌──────────┼───────────┐

 Navbar      Sidebar    Dashboard

     │           │            │

     ▼           ▼            ▼

     Atiar      Atiar       Atiar
```

---

# Step 5

Root Layout

```tsx
<AuthProvider>

{children}

</AuthProvider>
```

এটা মানে

পুরো Website-কে

Provider-এর ভিতরে রাখা।

যদি

```text
Navbar
Dashboard
Profile
```

সব Provider-এর ভিতরে থাকে

তাহলে

সবাই User Access করতে পারবে।

---

# Step 6

useAuth()

ধরো

তুমি Dashboard এ আছো।

এখন

User লাগবে।

তুমি লিখবে

```tsx
const { user } = useAuth();
```

এটার মানে

```text
Provider

↓

User

↓

Dashboard
```

---

# Step 7

Dashboard

```tsx
const { user } = useAuth();
```

তারপর

```tsx
<h1>

{user.first_name}

</h1>
```

Output

```text
Atiar
```

---

# Step 8

Login

```text
POST /login

↓

Cookie Save

↓

Dashboard
```

Dashboard Open হওয়ার পর

Provider

```text
GET /me
```

করবে।

তখন

```text
User

↓

Context

↓

Dashboard
```

---

# Step 9

Logout

```text
Logout

↓

Cookie Delete

↓

Context user=null

↓

Login Page
```

---

# Step 10 (সবচেয়ে গুরুত্বপূর্ণ)

পুরো Flow

```text
User Login
      │
      ▼
Cookie Saved
      │
      ▼
App Starts
      │
      ▼
AuthProvider
      │
      ▼
GET /me
      │
      ▼
Backend Returns User
      │
      ▼
setUser(user)
      │
      ▼
Context
      │
      ▼
Navbar
Sidebar
Dashboard
Profile
```

---

## আমার মনে হচ্ছে তুমি এখানেই আটকে গেছো

কারণ **React Context**, **Provider**, **useContext**, **Custom Hook (`useAuth`)**—এই চারটা জিনিস আগে আলাদা করে শেখানো হয়নি।

**আমার পরামর্শ হলো আমরা Chat App কিছুক্ষণের জন্য থামিয়ে আগে ১টি ছোট Next.js Demo Project-এ শুধু এই ৪টি বিষয় শিখি।**

সেখানে আমরা ৫০–৬০ লাইনের একটি উদাহরণ বানাব যেখানে:

- `AuthProvider` কী
    
- `createContext()` কী
    
- `useContext()` কী
    
- `useAuth()` কী
    
- কেন `layout.tsx`-এ Provider বসানো হয়
    

এগুলো পরিষ্কার হয়ে গেলে Chat Application-এর Authentication Flow অনেক সহজ মনে হবে।

----
হ্যাঁ। আমি **production-ready** `auth-provider.tsx` দিব, কিন্তু প্রতিটি লাইন ব্যাখ্যা করব।

---

# Folder Structure

```text
frontend/

providers/
    auth-provider.tsx

hooks/
    use-auth.ts

services/
    auth.service.ts
```

---

# Step 1: auth-provider.tsx

```tsx
"use client";

import {
  createContext,
  useContext,
  useEffect,
  useState,
  ReactNode,
} from "react";

import { getCurrentUser } from "@/services/auth.service";
```

## কেন `"use client"`?

React Context, `useState`, `useEffect` এগুলো **Client Component**-এ কাজ করে।

তাই এটি Client Component হতে হবে।

---

# Step 2: User Type

```tsx
type User = {
  id: number;
  email: string;
  first_name: string;
  last_name: string;
};
```

এটি User object-এর type।

যখন `/api/auth/me/` call করবে

তখন

```json
{
  "id": 1,
  "email": "atiar@example.com",
  "first_name": "Md",
  "last_name": "Atiar"
}
```

এই JSON-টাই User হবে।

---

# Step 3: Context Type

```tsx
type AuthContextType = {
  user: User | null;
  loading: boolean;
  setUser: React.Dispatch<React.SetStateAction<User | null>>;
};
```

মানে Context-এর ভিতরে কী থাকবে?

```
user

loading

setUser
```

---

# Step 4: Create Context

```tsx
export const AuthContext =
  createContext<AuthContextType | null>(null);
```

এখানে Context তৈরি হলো।

এখনো কোনো User নেই।

---

# Step 5: Props

```tsx
type AuthProviderProps = {
  children: ReactNode;
};
```

এখানে

```
children
```

মানে

```tsx
<AuthProvider>

    Navbar

    Dashboard

</AuthProvider>
```

Navbar এবং Dashboard হলো children।

---

# Step 6: Provider

```tsx
export default function AuthProvider({
  children,
}: AuthProviderProps) {
```

এখন Provider শুরু হলো।

---

# Step 7: State

```tsx
const [user, setUser] =
    useState<User | null>(null);

const [loading, setLoading] =
    useState(true);
```

প্রথমে

```
user = null

loading = true
```

---

# Step 8: Load User

```tsx
const loadUser = async () => {
  try {
    const data = await getCurrentUser();

    setUser(data);
  } catch {
    setUser(null);
  } finally {
    setLoading(false);
  }
};
```

এটা

```
GET /api/auth/me
```

call করবে।

---

# Step 9: useEffect

```tsx
useEffect(() => {
  loadUser();
}, []);
```

মানে

```
App প্রথমবার Open

↓

loadUser()
```

একবারই চলবে।

---

# Step 10: Return

```tsx
return (
  <AuthContext.Provider
    value={{
      user,
      loading,
      setUser,
    }}
  >
    {children}
  </AuthContext.Provider>
);
```

এটাই সবচেয়ে গুরুত্বপূর্ণ।

এখানে

```
user

loading

setUser
```

সব Component-এ Share হচ্ছে।

---

# Final auth-provider.tsx

```tsx
"use client";

import {
  createContext,
  useEffect,
  useState,
  ReactNode,
} from "react";

import { getCurrentUser } from "@/services/auth.service";

type User = {
  id: number;
  email: string;
  first_name: string;
  last_name: string;
};

type AuthContextType = {
  user: User | null;
  loading: boolean;
  setUser: React.Dispatch<React.SetStateAction<User | null>>;
};

export const AuthContext =
  createContext<AuthContextType | null>(null);

type AuthProviderProps = {
  children: ReactNode;
};

export default function AuthProvider({
  children,
}: AuthProviderProps) {
  const [user, setUser] =
    useState<User | null>(null);

  const [loading, setLoading] =
    useState(true);

  const loadUser = async () => {
    try {
      const data = await getCurrentUser();

      setUser(data);
    } catch {
      setUser(null);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    loadUser();
  }, []);

  return (
    <AuthContext.Provider
      value={{
        user,
        loading,
        setUser,
      }}
    >
      {children}
    </AuthContext.Provider>
  );
}
```

---

## এই কোডের Flow

```text
App Start
    │
    ▼
<AuthProvider>
    │
    ▼
useEffect()
    │
    ▼
loadUser()
    │
    ▼
GET /api/auth/me
    │
    ▼
User Data
    │
    ▼
setUser(user)
    │
    ▼
<AuthContext.Provider>
    │
    ├── Navbar
    ├── Sidebar
    ├── Dashboard
    └── Profile
```

### একটা গুরুত্বপূর্ণ পরামর্শ

এই `User` type-টা `auth-provider.tsx`-এর ভিতরে না রেখে আলাদা ফাইলে রাখা ভালো।

উদাহরণ:

```text
frontend/
├── types/
│   └── auth.ts
├── providers/
│   └── auth-provider.tsx
├── hooks/
└── services/
```

`types/auth.ts`

```ts
export interface User {
  id: number;
  email: string;
  first_name: string;
  last_name: string;
}
```

তাহলে `auth-provider.tsx`, `dashboard/page.tsx`, `profile/page.tsx`—সব জায়গায় একই `User` type reuse করা যাবে। এটি production project-এ বেশি maintainable।


--------

চমৎকার। এবার **Next.js অংশ** শুরু করি।

তুমি যেহেতু **DRF + Next.js** দিয়ে production-level project বানাতে চাও, তাই আমি Next.js-ও একইভাবে **Phase by Phase** শেখাব।

এখন পর্যন্ত আমরা Authentication Backend করেছি। এবার Frontend Authentication শুরু করব।

## Next.js Authentication Module Roadmap

### Phase 1

- ✅ Project Structure
    
- ✅ Folder Organization
    
- ✅ API Client (`lib/api.ts`)
    
- ✅ Environment Variables
    

### Phase 2

- ✅ Auth Service (`services/auth.service.ts`)
    
- Login
    
- Logout
    
- Register
    
- Get Current User
    

### Phase 3

- ✅ Auth Provider
    
- React Context
    
- useAuth Hook
    

### Phase 4

- Login Page
    
- Register Page
    
- React Hook Form
    
- Zod Validation
    

### Phase 5

- Protected Routes
    
- Guest Routes
    
- Middleware
    

### Phase 6

- Auto Refresh Token
    
- Retry Request
    
- Global Error Handling
    

### Phase 7

- Dashboard Layout
    
- Navbar
    
- User Menu
    

### Phase 8

- Production Authentication
    

---

## আমরা এখন কোথায়?

আমরা **Phase 3 (Auth Provider)** পর্যন্ত এসেছি।

এখন পরবর্তী ধাপ হবে:

### Next.js Phase 4 – Login Page

এখানে আমরা production-level Login Page বানাব।

শিখব:

- `react-hook-form`
    
- `zod`
    
- Login Form
    
- Error Message
    
- Loading Button
    
- API Call
    
- Redirect Dashboard
    
- Authentication Context Update
    

এখান থেকে Next.js-এর UI এবং DRF Backend একসাথে কাজ করা শুরু করবে।

এখন থেকে প্রতিটি ফাইল (যেমন `auth.service.ts`, `use-auth.ts`, `login/page.tsx`) সম্পূর্ণ কোড, ব্যাখ্যা এবং project structure সহ ধাপে ধাপে তৈরি করব।

----
