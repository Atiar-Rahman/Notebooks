
দারুণ। আমি **Official `dj-rest-auth` Quickstart**-কে এমনভাবে ব্যাখ্যা করব যেন আপনি শুধু Package ব্যবহার করবেন না, বরং **Internally কী হচ্ছে** সেটাও বুঝতে পারেন। আমরা এটাকে **Backend Developer Level**-এ শিখব।

# Complete Learning Roadmap

আমরা মোট **১০টি Part**-এ শিখব।

## Part 1: Installation & Project Setup

- Django Project Create
    
- Virtual Environment
    
- Package Installation
    
- প্রতিটি Package-এর কাজ
    
- Dependency Relationship
    

---

## Part 2: settings.py (Line by Line)

আমরা `settings.py`-এর প্রতিটি Configuration বুঝব।

```python
INSTALLED_APPS = [
    "rest_framework",
    "rest_framework.authtoken",
    "dj_rest_auth",
]
```

প্রতিটি App-এর কাজ।

তারপর

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        ...
    )
}
```

Authentication Pipeline কীভাবে কাজ করে।

---

## Part 3: URLs

```python
urlpatterns = [
    path("auth/", include("dj_rest_auth.urls")),
]
```

এই **এক লাইনের** পিছনে কী হয়?

কোন View Call হয়?

কোন Serializer Call হয়?

কোন URL Generate হয়?

Internally Routing কীভাবে কাজ করে?

---

## Part 4: Login Flow (Very Important)

আমরা Login-এর পুরো Internal Flow দেখব।

```text
Client

↓

POST /auth/login/

↓

urls.py

↓

LoginView

↓

LoginSerializer

↓

authenticate()

↓

User Model

↓

Token Create

↓

Response
```

তারপর Source Code-এর Logic বুঝব।

---

## Part 5: Logout Flow

Logout-এর সময়

```text
Request

↓

Token Delete

↓

Response
```

JWT হলে

```text
Blacklist

↓

Refresh Token

↓

Logout
```

---

## Part 6: User Endpoint

```http
GET

/auth/user/
```

Internally

```text
JWTAuthentication

↓

request.user

↓

UserSerializer

↓

Response
```

---

## Part 7: Registration

এখানে

```text
dj-rest-auth

↓

django-allauth

↓

RegisterSerializer

↓

Create User

↓

Email Verify
```

সব Internal Flow দেখব।

---

## Part 8: JWT Integration

সবচেয়ে গুরুত্বপূর্ণ Part

```text
Login

↓

Access Token

↓

Refresh Token

↓

Cookie/Header

↓

Protected API

↓

Refresh

↓

Logout
```

---

## Part 9: Source Code Analysis

আমরা Source Code পড়ব।

যেমন

```python
LoginView
```

Internally

```python
post()

↓

serializer.is_valid()

↓

login()

↓

create token()

↓

Response()
```

সব Explain করব।

---

## Part 10: Production Setup

React-এর সাথে

```text
React

↓

Axios

↓

JWT

↓

Refresh Token

↓

Interceptor

↓

Logout

↓

Protected Route
```

---

# প্রতিটি Part-এ আমরা কী শিখব?

প্রতিটি Class

```python
LoginView
```

↓

Method

```python
post()
```

↓

Serializer

↓

Authentication

↓

Permission

↓

Token

↓

Response

সব Diagram সহ বুঝব।

---

# শেখানোর Style

আমি শুধু

```python
INSTALLED_APPS = [
    "dj_rest_auth"
]
```

এভাবে লিখে এগোব না।

আমি Explain করব

**এই Package Install করলে Django-এর ভিতরে কী Register হয়?**

তারপর

**Request এলে কোন Class Call হয়?**

তারপর

**Response কোথা থেকে আসে?**

অর্থাৎ আমরা **Internal Workflow** শিখব।

---

# Example

আপনি শুধু শিখবেন না

```python
path(
    "auth/",
    include("dj_rest_auth.urls")
)
```

আপনি বুঝবেন

```text
include()

↓

dj_rest_auth.urls

↓

LoginView

↓

APIView

↓

Serializer

↓

Authentication

↓

Token

↓

JSON Response
```

---

# শেষে আপনি কী পারবেন?

এই Course শেষ হলে আপনি নিজেই তৈরি করতে পারবেন—

- ✅ Custom Login API
    
- ✅ Custom Register API
    
- ✅ JWT Authentication
    
- ✅ Role-based Authentication (Admin, Teacher, Student)
    
- ✅ Email Verification
    
- ✅ Password Reset
    
- ✅ Google Login
    
- ✅ React + Django Authentication
    
- ✅ Production-level Authentication System
    

---

## আমি কীভাবে এগোব?

আমরা **Official Documentation-এর ক্রম** অনুসরণ করব, কিন্তু প্রতিটি ধাপের **Source Code** এবং **Internal Working**-ও ব্যাখ্যা করব।

### **Lesson 1 (পরবর্তী ধাপ):**

**Installation & Project Setup (Line by Line)**

এখানে আমরা শিখব:

- Virtual Environment কেন দরকার?
    
- `pip install dj-rest-auth` করলে কী কী Install হয়?
    
- `rest_framework`, `dj_rest_auth`, `rest_framework.authtoken`—প্রতিটির কাজ কী?
    
- Dependency Diagram
    
- Request Lifecycle Overview
    

এটাই হবে আমাদের Foundation। এরপর ধাপে ধাপে পুরো `dj-rest-auth` গভীরভাবে শিখব।

-------
# Lesson 1: Installation & Project Setup (Deep Explanation)

আজকের লক্ষ্য শুধু Project Run করা নয়, **প্রতিটি Package কেন Install করছি এবং Internally কী হচ্ছে** সেটা বোঝা।

---

# Lesson Overview

আজ আমরা শিখব:

* Virtual Environment
* Django Installation
* DRF Installation
* dj-rest-auth Installation
* Package Relationship
* Authentication Architecture
* Project Structure
* Request Flow Overview

---

# Step 1: Create Virtual Environment

```bash
python -m venv venv
```

Linux/macOS

```bash
source venv/bin/activate
```

Windows

```bash
venv\Scripts\activate
```

---

## Virtual Environment কেন?

ধরুন আপনার PC-তে

Project A

```
Django 4.2
```

Project B

```
Django 5.2
```

Global Installation হলে Conflict হবে।

Virtual Environment করলে

```
PC

│

├── Project A

│     ├── Django 4.2

│     └── DRF 3.15

│

└── Project B

      ├── Django 5.2

      └── DRF 3.16
```

প্রত্যেক Project নিজের Package ব্যবহার করবে।

---

# Step 2: Install Django

```bash
pip install django
```

Check Version

```bash
django-admin --version
```

---

## Django কী?

Django হলো Full Stack Web Framework।

এতে Built-in আছে

```
ORM

Authentication

Admin Panel

Template Engine

Middleware

Security

Sessions

Caching
```

---

# Step 3: Install Django REST Framework

```bash
pip install djangorestframework
```

---

## DRF কী?

Django HTML Page Return করে।

DRF JSON Return করে।

Example

Django

```python
return render(request,"index.html")
```

↓

HTML

DRF

```python
return Response({
    "username":"atiar"
})
```

↓

JSON

---

# DRF Architecture

```
Browser / React

        │

        ▼

APIView

        │

Serializer

        │

Model

        │

Database
```

---

# Step 4: Install dj-rest-auth

```bash
pip install dj-rest-auth
```

---

## প্রশ্ন

**এটা Install করলে কী হয়?**

অনেকে মনে করে

```
Authentication তৈরি হয়ে গেছে।
```

আসলে না।

এটা শুধু

```
Ready-made Views

Ready-made Serializers

Ready-made URLs
```

দেয়।

---

# Example

নিজে Login লিখতে হলে

```python
class LoginView(APIView):

    def post(self,request):

        serializer=LoginSerializer(...)

        authenticate(...)

        login(...)

        return Response(...)
```

অনেক Code লাগবে।

dj-rest-auth

এগুলো Ready করে দেয়।

---

# Step 5: Dependency Diagram

```
            Django

               │

               ▼

Django REST Framework

               │

               ▼

dj-rest-auth

               │

               ▼

Simple JWT

(optional)
```

Meaning

```
Django

↓

DRF

↓

dj-rest-auth

↓

JWT
```

---

# Step 6: Create Project

```bash
django-admin startproject config .
```

Project

```
config/

manage.py

config/

    settings.py

    urls.py

    asgi.py

    wsgi.py
```

---

# File Explanation

## manage.py

সব Django Command এখানে।

Example

```bash
python manage.py runserver

python manage.py migrate

python manage.py createsuperuser
```

---

## settings.py

Project Configuration

```
Database

Installed Apps

Middleware

Authentication

Timezone

Static Files
```

সব এখানে থাকে।

---

## urls.py

সব URL এখানে Register হয়।

Example

```python
urlpatterns=[
]
```

---

## wsgi.py

Production Server-এর জন্য।

Gunicorn

uWSGI

Apache

এগুলো WSGI ব্যবহার করে।

---

## asgi.py

Async Server

WebSocket

Django Channels

Real-time Chat

এগুলো ASGI ব্যবহার করে।

---

# Step 7: Create App

```bash
python manage.py startapp accounts
```

কেন?

Authentication সম্পর্কিত সব Code এখানে থাকবে।

Structure

```
accounts/

models.py

views.py

serializers.py

urls.py

permissions.py

authentication.py
```

---

# Step 8: Install Apps

settings.py

```python
INSTALLED_APPS = [

    "django.contrib.admin",

    "django.contrib.auth",

    "django.contrib.contenttypes",

    "django.contrib.sessions",

    "django.contrib.messages",

    "django.contrib.staticfiles",

    "rest_framework",

    "rest_framework.authtoken",

    "dj_rest_auth",

    "accounts",
]
```

---

## প্রতিটি App-এর কাজ

### django.contrib.auth

Built-in User System

```
Login

Logout

Permissions

Groups

Password Hashing
```

---

### rest_framework

DRF Enable করে।

APIView

Serializer

ViewSet

Router

সব এখান থেকে আসে।

---

### rest_framework.authtoken

Database Token Authentication।

Example

```
Token

↓

abcf34fkj893...
```

এই Token Database-এ Save হয়।

> **নোট:** পরে JWT ব্যবহার করলে এটি সব ক্ষেত্রে দরকার নাও হতে পারে। কিন্তু অফিসিয়াল Quickstart প্রথমে Token Authentication দেখায়, তাই সেখানে এটি যোগ করা হয়।

---

### dj_rest_auth

এটা যোগ করার পরে

Ready-made Views পাওয়া যায়।

যেমন

```
LoginView

LogoutView

UserDetailsView

PasswordResetView

PasswordChangeView
```

---

# Internally কী Install হয়?

```
dj_rest_auth

│

├── views.py

├── serializers.py

├── urls.py

├── app

├── forms.py

└── utils.py
```

আপনি

```python
include("dj_rest_auth.urls")
```

করলেই

এই URL গুলো Register হয়।

---

# Step 9: Authentication Architecture

```
React

│

▼

Login Request

│

▼

dj-rest-auth LoginView

│

▼

Django authenticate()

│

▼

User Model

│

▼

Generate Token

│

▼

JSON Response
```

---

# Step 10: Installation পর্যন্ত কী শিখলাম?

আপনি এখন জানেন

✅ Django Framework কী

✅ DRF কী

✅ dj-rest-auth কী

✅ Package Dependency

✅ Authentication Architecture

✅ কেন Virtual Environment দরকার

✅ Project Structure

✅ কোন App কী কাজ করে

---

# Interview Questions

### 1. `dj-rest-auth` কী?

**Answer:**
`dj-rest-auth` হলো Django REST Framework-এর জন্য একটি Package যা Login, Logout, Registration, Password Reset, Password Change, User Details ইত্যাদির জন্য Ready-made Authentication API প্রদান করে।

---

### 2. `dj-rest-auth` কি Authentication করে?

**Answer:**
না। এটি Django-এর Authentication System ব্যবহার করে এবং তার উপর Ready-made API প্রদান করে।

---

### 3. `rest_framework.authtoken` কেন Install করা হয়?

**Answer:**
DRF-এর Built-in Token Authentication ব্যবহার করার জন্য। অফিসিয়াল Quickstart প্রথমে এই Token Authentication দেখায়। JWT ব্যবহার করলে সাধারণত `djangorestframework-simplejwt` এবং তার Configuration ব্যবহার করা হয়।

---

### 4. `dj-rest-auth` এবং `Simple JWT`-এর সম্পর্ক কী?

**Answer:**

* `dj-rest-auth` → Authentication API (Login, Logout, Register)
* `Simple JWT` → Access Token ও Refresh Token তৈরি এবং Verify করে।

---

## Homework

পরবর্তী Lesson শুরু করার আগে নিচের কাজগুলো করুন:

```bash
python -m venv venv

pip install django

pip install djangorestframework

pip install dj-rest-auth

django-admin startproject config .

python manage.py startapp accounts
```

তারপর `settings.py`-এ যোগ করুন:

```python
INSTALLED_APPS = [
    ...
    "rest_framework",
    "rest_framework.authtoken",
    "dj_rest_auth",
    "accounts",
]
```

---

### পরবর্তী Lesson (Lesson 2)

**`settings.py` Deep Dive (Line by Line)**

এখানে আমরা বিস্তারিত শিখব:

* `INSTALLED_APPS` কীভাবে কাজ করে
* `REST_FRAMEWORK` Configuration
* `DEFAULT_AUTHENTICATION_CLASSES`
* `DEFAULT_PERMISSION_CLASSES`
* `MIDDLEWARE`
* Request Lifecycle
* কেন `settings.py`-এর প্রতিটি Configuration প্রয়োজন এবং Django Startup-এর সময় এগুলো কীভাবে Load হয়।


---------------------

# Lesson 2: `settings.py` Deep Dive (Line by Line)

আজকের Lesson-এর শেষে আপনি বুঝতে পারবেন—

* Django Startup-এর সময় `settings.py` কীভাবে Load হয়
* `INSTALLED_APPS` কী করে
* `REST_FRAMEWORK` Configuration কীভাবে কাজ করে
* `DEFAULT_AUTHENTICATION_CLASSES`
* `DEFAULT_PERMISSION_CLASSES`
* `MIDDLEWARE`
* `dj-rest-auth` কেন এই Configuration-গুলো দরকার

---

# Django Startup Flow

যখন আপনি লিখেন

```bash
python manage.py runserver
```

Internally Django এই Flow Follow করে।

```text
manage.py

      │

      ▼

settings.py Load

      │

      ▼

INSTALLED_APPS Load

      │

      ▼

Middleware Load

      │

      ▼

URL Configuration

      │

      ▼

Start Server
```

**Interview Question**

**Q:** `settings.py` কখন Load হয়?

**Answer:**
Django Project Start হওয়ার সময় প্রথমেই `settings.py` Load হয় এবং পুরো Project-এর Configuration Initialize হয়।

---

# settings.py Structure

একটি সাধারণ `settings.py`

```python
INSTALLED_APPS = []

MIDDLEWARE = []

DATABASES = {}

REST_FRAMEWORK = {}

AUTH_PASSWORD_VALIDATORS = []

LANGUAGE_CODE = "en-us"

TIME_ZONE = "UTC"

STATIC_URL = "static/"
```

প্রতিটি Section-এর আলাদা কাজ আছে।

---

# INSTALLED_APPS

সবচেয়ে গুরুত্বপূর্ণ অংশ।

```python
INSTALLED_APPS = [

    "django.contrib.admin",

    "django.contrib.auth",

    "django.contrib.contenttypes",

    "django.contrib.sessions",

    "django.contrib.messages",

    "django.contrib.staticfiles",

    "rest_framework",

    "rest_framework.authtoken",

    "dj_rest_auth",

    "accounts",

]
```

---

## Django Startup-এর সময় কী হয়?

Django একে একে সব App Load করে।

```text
admin

↓

auth

↓

contenttypes

↓

sessions

↓

rest_framework

↓

dj_rest_auth

↓

accounts
```

প্রতিটি App

* models.py
* admin.py
* signals.py
* migrations

সব Register করে।

---

## django.contrib.auth

Authentication System

দেয়

```text
User

Permission

Group

Authentication

Password Hashing
```

---

## django.contrib.sessions

Session Authentication-এর জন্য।

Session Data Database-এ Store করে।

Table

```text
django_session
```

---

## django.contrib.contenttypes

Django-এর Generic Relationship-এর জন্য।

Example

```text
Permission

↓

Any Model
```

Internally এটি ContentType Table Maintain করে।

---

## rest_framework

DRF Enable করে।

এখান থেকে পাই

```text
APIView

GenericAPIView

Serializer

ViewSet

Router

Permissions

Authentication
```

---

## rest_framework.authtoken

Token Authentication Enable করে।

Database Table

```text
authtoken_token
```

Example

| User  | Token   |
| ----- | ------- |
| admin | abcd123 |

---

## dj_rest_auth

Ready-made Authentication Views দেয়।

Internally

```text
LoginView

LogoutView

UserDetailsView

PasswordResetView

PasswordChangeView
```

---

## accounts

এটি আপনার নিজের App।

এখানে থাকবে

```text
Custom User

Serializer

Permission

Authentication

Signals
```

---

# REST_FRAMEWORK

এটি DRF-এর Global Configuration।

Example

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES":[

        "rest_framework.authentication.TokenAuthentication",

    ],

}
```

---

## এটা কী করে?

ধরুন Request আসলো।

```http
GET /products/
```

Header

```http
Authorization:
Token abc123
```

DRF

প্রথমে

```python
TokenAuthentication
```

Call করবে।

---

Flow

```text
Request

↓

Authentication Class

↓

Authenticated User

↓

APIView
```

---

# DEFAULT_AUTHENTICATION_CLASSES

Example

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES":[

        "rest_framework.authentication.TokenAuthentication",

    ]

}
```

মানে

সব API Defaultভাবে

```text
TokenAuthentication
```

Use করবে।

---

JWT হলে

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES":[

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ]

}
```

এখন সব Request

JWT দিয়ে Authenticate হবে।

---

## Multiple Authentication Classes

```python
REST_FRAMEWORK = {

"DEFAULT_AUTHENTICATION_CLASSES":[

"rest_framework.authentication.SessionAuthentication",

"rest_framework.authentication.TokenAuthentication",

]
}
```

Flow

```text
Request

↓

SessionAuthentication

↓

Failed?

↓

TokenAuthentication

↓

Success

↓

request.user
```

---

# request.user কোথায় Set হয়?

Authentication Class-এর ভিতরে।

Example

```python
class JWTAuthentication:
    def authenticate(self, request):
```

Internally

```text
Read Header

↓

Decode Token

↓

Find User

↓

request.user = user
```

এরপর View-তে

```python
request.user
```

Available হয়।

---

# DEFAULT_PERMISSION_CLASSES

Example

```python
REST_FRAMEWORK = {

"DEFAULT_PERMISSION_CLASSES":[

"rest_framework.permissions.IsAuthenticated",

]

}
```

মানে

Defaultভাবে

সব API Login Required।

---

Flow

```text
Request

↓

Authentication

↓

Permission

↓

APIView
```

---

Example

```python
permission_classes = [
    IsAuthenticated
]
```

Token না থাকলে

```http
401 Unauthorized
```

---

Public API চাইলে

```python
from rest_framework.permissions import AllowAny

class ProductList(APIView):

    permission_classes = [
        AllowAny
    ]
```

---

# MIDDLEWARE

এটা Django-এর Request Pipeline।

```python
MIDDLEWARE = [

"django.middleware.security.SecurityMiddleware",

"django.contrib.sessions.middleware.SessionMiddleware",

"django.middleware.common.CommonMiddleware",

"django.middleware.csrf.CsrfViewMiddleware",

"django.contrib.auth.middleware.AuthenticationMiddleware",

"django.contrib.messages.middleware.MessageMiddleware",

]
```

---

Flow

```text
Request

↓

Middleware

↓

URL

↓

View

↓

Response

↓

Middleware

↓

Browser
```

---

## AuthenticationMiddleware

Session Authentication-এর জন্য।

Internally

```text
Session

↓

User

↓

request.user
```

Set করে।

**Note:** JWTAuthentication DRF-এর Authentication Layer-এ কাজ করে, Middleware-এ নয়।

---

## CSRF Middleware

Protect করে

```text
Cross Site Request Forgery
```

Attack থেকে।

---

## Security Middleware

Headers Add করে।

Example

```text
HSTS

HTTPS

Secure Cookies
```

---

# DATABASES

```python
DATABASES = {

"default":{

"ENGINE":"django.db.backends.sqlite3",

"NAME":BASE_DIR/"db.sqlite3"

}

}
```

Project-এর Database Configuration।

---

# Authentication Request Lifecycle

সব মিলিয়ে Flow

```text
Client

│

▼

Middleware

│

▼

URL

│

▼

APIView

│

▼

Authentication Class

│

▼

Permission

│

▼

Serializer

│

▼

Model

│

▼

Database

│

▼

Response
```

---

# dj-rest-auth এখানে কোথায়?

```text
React

↓

Login Request

↓

URL

↓

LoginView (dj-rest-auth)

↓

Authentication

↓

Serializer

↓

User

↓

Token

↓

Response
```

---

# Production JWT Configuration

Later আমরা লিখব

```python
REST_FRAMEWORK = {

"DEFAULT_AUTHENTICATION_CLASSES":[

"rest_framework_simplejwt.authentication.JWTAuthentication",

]

}

REST_AUTH = {

"USE_JWT":True

}
```

মানে

```text
Login

↓

JWT

↓

Access Token

↓

Refresh Token
```

---

# Interview Questions

## 1. `INSTALLED_APPS` কী?

**Answer:**
এটি Django-কে জানায় কোন Apps Project-এ Load করতে হবে। Startup-এর সময় Django এই Apps-এর Models, Migrations, Admin Configuration ইত্যাদি Register করে।

---

## 2. `REST_FRAMEWORK` কেন ব্যবহার করা হয়?

**Answer:**
DRF-এর Global Configuration করার জন্য। যেমন Authentication, Permission, Pagination, Renderer, Parser ইত্যাদি।

---

## 3. `DEFAULT_AUTHENTICATION_CLASSES` কী?

**Answer:**
এটি নির্ধারণ করে DRF কোন Authentication Backend ব্যবহার করবে, যেমন `SessionAuthentication`, `TokenAuthentication` বা `JWTAuthentication`।

---

## 4. Authentication এবং Permission-এর পার্থক্য কী?

**Authentication:** User কে তা শনাক্ত করে (`request.user` সেট করে)।

**Permission:** সেই User-এর Access আছে কি না তা যাচাই করে।

Flow:

```text
Authentication
        ↓
Who are you?
        ↓
Permission
        ↓
What can you do?
```

---

## 5. Middleware এবং Authentication Class-এর মধ্যে পার্থক্য কী?

| Middleware                   | Authentication Class             |
| ---------------------------- | -------------------------------- |
| Django Level                 | DRF Level                        |
| Request/Response Process করে | User Authenticate করে            |
| সব Request-এর জন্য চলে       | শুধু DRF API Request-এর জন্য চলে |

---

# Homework

পরবর্তী Lesson-এর আগে নিচের Configuration নিজের Project-এ যোগ করুন:

```python
INSTALLED_APPS = [
    ...
    "rest_framework",
    "rest_framework.authtoken",
    "dj_rest_auth",
]
```

এবং

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.TokenAuthentication",
    ],
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.AllowAny",
    ],
}
```

তারপর

```bash
python manage.py migrate
```

Run করুন এবং `authtoken_token` table তৈরি হয়েছে কিনা Database-এ দেখুন।

---

## পরবর্তী Lesson (Lesson 3)

**Official `dj-rest-auth` URLs & Login API (Source Code Analysis)**

এখানে আমরা শিখব:

* `include("dj_rest_auth.urls")` আসলে কী করে?
* `LoginView` কোথা থেকে আসে?
* `LoginSerializer` কীভাবে কাজ করে?
* `authenticate()` Function কীভাবে User Verify করে?
* Login Request থেকে Response পর্যন্ত সম্পূর্ণ Internal Call Stack।


---------

# Lesson 3: `dj-rest-auth` URLs & Login API (Internal Workflow)

আজকের Lesson-এর শেষে আপনি বুঝতে পারবেন:

* `include("dj_rest_auth.urls")` আসলে কী করে?
* `LoginView` কোথা থেকে আসে?
* `LoginSerializer` কীভাবে কাজ করে?
* Django-এর `authenticate()` কী করে?
* Login Request-এর সম্পূর্ণ Call Stack

---

# আজ আমরা কী শিখব?

ধরুন React থেকে Request আসলো।

```http
POST /auth/login/
```

Body

```json
{
    "username": "atiar",
    "password": "123456"
}
```

Internally কী কী হয়?

---

# Step 1: URL Configuration

আপনি লিখলেন

```python
# config/urls.py

from django.urls import path, include

urlpatterns = [
    path("auth/", include("dj_rest_auth.urls")),
]
```

অনেকে মনে করে

```python
include("dj_rest_auth.urls")
```

শুধু URL Include করে।

আসলে এর ভিতরে অনেক URL Register হয়।

---

# Internally

`dj_rest_auth/urls.py`

Simplified Version

```python
urlpatterns = [

    path("login/", LoginView.as_view()),

    path("logout/", LogoutView.as_view()),

    path("user/", UserDetailsView.as_view()),

    path("password/change/", PasswordChangeView.as_view()),

    path("password/reset/", PasswordResetView.as_view()),

]
```

অর্থাৎ

আপনি

```python
path("auth/", include("dj_rest_auth.urls"))
```

লিখলে Automatically

```text
/auth/login/

/auth/logout/

/auth/user/

/auth/password/change/

/auth/password/reset/
```

সব তৈরি হয়ে যায়।

---

# URL Resolution

Request

```http
POST /auth/login/
```

↓

Django

```text
config.urls

↓

include()

↓

dj_rest_auth.urls

↓

LoginView
```

Diagram

```text
Browser

     │

     ▼

config.urls

     │

     ▼

include()

     │

     ▼

dj_rest_auth.urls

     │

     ▼

LoginView
```

---

# Step 2: LoginView

Internally

```python
class LoginView(APIView):
```

মানে

```text
APIView

↓

LoginView
```

Inheritance

```text
APIView

     ▲

     │

LoginView
```

তাই

LoginView

DRF-এর

```text
Request

Response

Serializer

Authentication

Permission
```

সব Feature ব্যবহার করতে পারে।

---

# Step 3: Client Request

React

↓

POST

```http
POST /auth/login/
```

Body

```json
{
    "username":"atiar",

    "password":"123456"
}
```

Header

```http
Content-Type:
application/json
```

---

# Step 4: APIView Dispatch

APIView-এর ভিতরে

Internally

```python
dispatch()
```

Call হয়।

Flow

```text
Request

↓

dispatch()

↓

Authentication

↓

Permission

↓

post()
```

---

# Step 5: LoginView.post()

Simplified

```python
class LoginView(APIView):

    def post(self, request):

        serializer = LoginSerializer(
            data=request.data
        )

        serializer.is_valid()

        login()

        return Response(...)
```

সবচেয়ে গুরুত্বপূর্ণ

```python
serializer.is_valid()
```

---

# Step 6: LoginSerializer

Internally

```python
class LoginSerializer(serializers.Serializer):

    username = serializers.CharField()

    password = serializers.CharField()
```

User Input

```json
{
"username":"atiar",

"password":"123456"
}
```

Serializer

Validate করে।

---

# Validation

```python
serializer.is_valid()
```

মানে

Check করবে

```text
Username আছে?

Password আছে?

Empty?

Correct Format?
```

---

যদি ভুল হয়

```json
{
"password":[

"This field is required."

]
}
```

Return করবে।

---

# Step 7: authenticate()

Validation Pass হলে

Internally

```python
authenticate(
username=username,
password=password
)
```

Call হয়।

---

# authenticate() কোথা থেকে আসে?

```python
from django.contrib.auth import authenticate
```

এটা Django-এর Built-in Function।

---

# authenticate() Internally

Flow

```text
Username

↓

Find User

↓

Check Password Hash

↓

Correct?

↓

Return User
```

---

Diagram

```text
Request

↓

authenticate()

↓

User Model

↓

Password Hash

↓

Success

↓

User Object
```

---

# Password কখনো Compare হয়?

Database-এ

Password

এভাবে থাকে না

```text
123456
```

থাকে

```text
pbkdf2_sha256$600000$.....
```

authenticate()

Internally

```python
check_password()
```

Call করে।

---

# যদি Password ভুল হয়?

```python
authenticate()
```

Return করবে

```python
None
```

তখন

```json
{
"non_field_errors":[

"Unable to log in."

]
}
```

---

# যদি Password ঠিক হয়?

Return

```python
<User: atiar>
```

---

# Step 8: Login

User পাওয়া গেলে

Internally

```python
login(request,user)
```

Call হয়।

Session Authentication হলে

Session তৈরি হবে।

JWT হলে

Token তৈরি হবে।

---

# Step 9: Token Creation

Token Authentication হলে

Internally

```python
Token.objects.get_or_create(
user=user
)
```

Database

| User  | Token  |
| ----- | ------ |
| atiar | abc123 |

---

JWT হলে

```text
Access Token

Refresh Token
```

Generate হবে।

---

# Step 10: Response

Token হলে

```json
{
"key":"abc123"
}
```

JWT হলে

```json
{
"access":"eyJ...",

"refresh":"eyJ..."
}
```

---

# Complete Login Flow

```text
React

│

▼

POST /auth/login/

│

▼

config.urls

│

▼

include()

│

▼

dj_rest_auth.urls

│

▼

LoginView

│

▼

dispatch()

│

▼

LoginSerializer

│

▼

is_valid()

│

▼

authenticate()

│

▼

User

│

▼

Generate Token

│

▼

JSON Response
```

---

# Important Classes

## APIView

Responsible For

```text
HTTP Request

Authentication

Permission

Dispatch

Response
```

---

## LoginSerializer

Responsible For

```text
Validate Username

Validate Password
```

---

## authenticate()

Responsible For

```text
Find User

Check Password

Return User
```

---

## Token

Responsible For

```text
Authentication

Future Requests
```

---

# Login Call Stack

```text
Browser

↓

POST

↓

URL

↓

APIView.dispatch()

↓

LoginView.post()

↓

LoginSerializer

↓

authenticate()

↓

login()

↓

create token

↓

Response()
```

---

# Interview Questions

## 1. `include("dj_rest_auth.urls")` কী করে?

**Answer:**
এটি `dj_rest_auth`-এর সমস্ত Built-in Authentication URL (Login, Logout, User Details, Password Change, Password Reset ইত্যাদি) Project-এ Register করে।

---

## 2. `LoginView` কী Inherit করে?

**Answer:**

```text
APIView
```

---

## 3. `serializer.is_valid()` কী করে?

**Answer:**
Incoming Request Data Validate করে। Required Field, Data Type এবং Credentials যাচাইয়ের জন্য Serializer-এর Validation Logic চালায়।

---

## 4. `authenticate()` কী করে?

**Answer:**
Django Authentication Backends ব্যবহার করে User খুঁজে বের করে, Password Hash Verify করে এবং Credentials সঠিক হলে User Object Return করে।

---

## 5. Password কীভাবে Verify হয়?

**Answer:**
Plain Password Database-এর Hashed Password-এর সাথে `check_password()` এর মাধ্যমে Compare করা হয়। Plain Password কখনো Database-এ Store করা হয় না।

---

# Homework

1. `config/urls.py`-এ লিখুন:

```python
urlpatterns = [
    path("auth/", include("dj_rest_auth.urls")),
]
```

2. Server চালিয়ে নিচের Endpoints Browser বা Postman-এ দেখুন:

```text
/auth/login/
/auth/logout/
/auth/user/
/auth/password/change/
/auth/password/reset/
```

3. একটি Superuser তৈরি করুন এবং `/auth/login/` Endpoint-এ Login Test করুন।

---

# Lesson 4 (Next)

**LoginSerializer & Django Authentication Backend (Deep Dive)**

এখানে আমরা শিখব:

* `serializer.is_valid()` এর ভিতরে কী ঘটে?
* `validate()` Method কীভাবে কাজ করে?
* Django Authentication Backends কী?
* `ModelBackend.authenticate()` কীভাবে User খুঁজে বের করে?
* `check_password()` Internally কীভাবে Password Verify করে?
* `request.user` ঠিক কোন মুহূর্তে Set হয়?


---------
# Lesson 4: LoginSerializer & Django Authentication Backend (Deep Dive)

আজ আমরা `dj-rest-auth`-এর **সবচেয়ে গুরুত্বপূর্ণ অংশ** শিখব।

অনেক Developer জানে

```python
serializer.is_valid()
```

কিন্তু **এর ভিতরে কী হয়** সেটা জানে না।

Interview-এ এখান থেকেই প্রশ্ন আসে।

---

# আজ কী শিখবো?

```
Request

↓

LoginSerializer

↓

serializer.is_valid()

↓

validate()

↓

authenticate()

↓

Authentication Backend

↓

User Object

↓

request.user
```

---

# Login Request

React

```http
POST /auth/login/
```

Body

```json
{
    "username": "atiar",
    "password": "123456"
}
```

---

# Step 1

LoginView

```python
serializer = LoginSerializer(
    data=request.data
)
```

এখন

```
serializer

↓

LoginSerializer Instance
```

এখনও Validation হয়নি।

---

# Step 2

```python
serializer.is_valid()
```

এটাই সবচেয়ে গুরুত্বপূর্ণ Method।

Internally

```
is_valid()

↓

run_validation()

↓

to_internal_value()

↓

validate()

↓

validated_data
```

---

## Flow

```
Incoming JSON

↓

Serializer

↓

Field Validation

↓

Object Validation

↓

validated_data
```

---

# Step 3

Field Validation

Example

```python
class LoginSerializer(serializers.Serializer):

    username = serializers.CharField()

    password = serializers.CharField()
```

Request

```json
{
    "username":"atiar",

    "password":"123456"
}
```

Serializer Check করবে

```
username আছে?

↓

password আছে?

↓

Empty?

↓

Correct datatype?
```

---

যদি

```json
{
    "username":""
}
```

হয়

Error

```json
{
    "password":[
        "This field is required."
    ]
}
```

---

# Step 4

সব Field ঠিক থাকলে

```python
validate()
```

Call হয়।

এটাই

সবচেয়ে Powerful Method।

Example

```python
def validate(self, attrs):

    return attrs
```

---

কিন্তু

LoginSerializer

এখানে

Internally

```python
authenticate(...)
```

Call করে।

---

Flow

```
Field Validation

↓

validate()

↓

authenticate()
```

---

# Step 5

authenticate()

Import

```python
from django.contrib.auth import authenticate
```

এটা

Django-এর Built-in Function।

---

Example

```python
user = authenticate(

    username="atiar",

    password="123456"

)
```

---

# প্রশ্ন

authenticate()

User কোথায় খুঁজে?

Database-এ?

না।

প্রথমে

Authentication Backend

খুঁজে।

---

# Authentication Backend

settings.py

```python
AUTHENTICATION_BACKENDS = [

    "django.contrib.auth.backends.ModelBackend",

]
```

Default

```text
ModelBackend
```

ব্যবহার হয়।

---

Flow

```
authenticate()

↓

ModelBackend

↓

Database

↓

User
```

---

# ModelBackend

Internally

Simplified

```python
class ModelBackend:

    def authenticate(

        self,

        username,

        password

    ):

        user = User.objects.get(
            username=username
        )

        if user.check_password(password):

            return user
```

এটাই Main Logic।

---

# Step 6

Database Query

```python
User.objects.get(

username=username
)
```

Database

| id | username |
| -- | -------- |
| 1  | atiar    |

Return

```python
<User: atiar>
```

---

# Step 7

Password Verification

এখানে

সবচেয়ে Important অংশ।

User Table

```
Password

↓

pbkdf2_sha256$600000....
```

Password

Plain Text

হিসেবে থাকে না।

---

Internally

```python
user.check_password(
    password
)
```

Call হয়।

---

Flow

```
Input Password

↓

Hash Input Password

↓

Compare Hash

↓

Match?

↓

True
```

---

Diagram

```
123456

↓

Hash

↓

PBKDF2

↓

Compare

↓

Database Hash

↓

Success
```

---

# যদি Match না করে

```python
authenticate()
```

Return

```python
None
```

---

LoginSerializer

Raise করবে

```python
ValidationError(

"Unable to log in."

)
```

Response

```json
{
    "non_field_errors":[

        "Unable to log in."
    ]
}
```

---

# Step 8

যদি Match করে

Return

```python
<User: atiar>
```

---

validate()

Internally

```python
attrs["user"] = user
```

এখন

validated_data

```
username

password

user
```

সব থাকবে।

---

# Step 9

serializer.is_valid()

শেষে

```python
serializer.validated_data
```

হয়ে যায়

```python
{

    "username":"atiar",

    "password":"123456",

    "user":<User:atiar>

}
```

---

# Step 10

LoginView

এখন

```python
user = serializer.validated_data["user"]
```

পেয়ে যায়।

---

তারপর

```python
login()

create token()

Response()
```

---

# Complete Flow

```
Client

↓

POST

↓

LoginView

↓

LoginSerializer

↓

is_valid()

↓

Field Validation

↓

validate()

↓

authenticate()

↓

ModelBackend

↓

User Query

↓

check_password()

↓

Return User

↓

validated_data

↓

LoginView

↓

Create Token

↓

Response
```

---

# কোথায় `request.user` Set হয়?

এটা অনেক Interview-এ আসে।

**Login-এর সময় `authenticate()` `request.user` Set করে না।**

`authenticate()` শুধু

```python
return user
```

করে।

এরপর:

* **Session Authentication** হলে `login(request, user)` Session তৈরি করে এবং পরবর্তী Request-এ `AuthenticationMiddleware` `request.user` Set করে।
* **JWT Authentication** হলে Login Response-এ Token দেওয়া হয়। পরবর্তী Request-এ `JWTAuthentication.authenticate()` Token Decode করে `request.user` Set করে।

অর্থাৎ **Login Request-এ নয়, পরবর্তী Authenticated Request-এ `request.user` পাওয়া যায়।**

---

# Authentication Backend পরিবর্তন করা যায়?

হ্যাঁ।

Example

```python
AUTHENTICATION_BACKENDS = [

    "accounts.backends.EmailBackend",

    "django.contrib.auth.backends.ModelBackend",

]
```

তখন

```
authenticate()

↓

EmailBackend

↓

Fail?

↓

ModelBackend
```

---

# Email দিয়ে Login

Custom Backend

```python
class EmailBackend(ModelBackend):

    def authenticate(

        self,

        request,

        username=None,

        password=None

    ):

        user = User.objects.get(
            email=username
        )

        if user.check_password(password):

            return user
```

এখন

```
Email

↓

User

↓

Password

↓

Login
```

---

# Interview Questions

## 1. `serializer.is_valid()` কী করে?

**Answer:**
এটি Field Validation এবং Object Validation চালায়। সফল হলে `validated_data` তৈরি করে, ব্যর্থ হলে `ValidationError` Raise করে।

---

## 2. `validate()` Method কী?

**Answer:**
Serializer-এর Object-level Validation Method। LoginSerializer-এ এটি `authenticate()` Call করে User Verify করে।

---

## 3. `authenticate()` কী Return করে?

**Answer:**

* Credentials সঠিক হলে `User` Object।
* ভুল হলে `None`।

---

## 4. Password কীভাবে Verify হয়?

**Answer:**
`user.check_password()` Plain Password-কে Hash করে Database-এর Hashed Password-এর সাথে Compare করে।

---

## 5. Authentication Backend কী?

**Answer:**
Authentication Backend হলো Django-এর Component যা User Verify করার Logic Implement করে। Default Backend হলো `ModelBackend`।

---

# Homework

এই ৪টি Function-এর Source Code GitHub-এ পড়ার চেষ্টা করুন:

```python
authenticate()

check_password()

ModelBackend.authenticate()

Serializer.is_valid()
```

শুধু Copy করবেন না। প্রতিটি Function-এর Input, Output এবং Responsibility লিখে রাখুন।

---

# Lesson 5 (সবচেয়ে গুরুত্বপূর্ণ)

পরবর্তী Lesson-এ আমরা **JWT Login-এর Internal Flow** শিখব।

সেখানে দেখব:

* `dj-rest-auth` কীভাবে `Simple JWT`-কে Call করে
* Access Token কোথায় তৈরি হয়
* Refresh Token কোথায় তৈরি হয়
* Token Payload কীভাবে তৈরি হয়
* Signature কীভাবে Generate হয়
* `JWTAuthentication` কীভাবে Token Decode করে `request.user` Set করে

এটি পুরো JWT Authentication System-এর Core, এবং DRF Interview-এর অন্যতম গুরুত্বপূর্ণ বিষয়।

---------
# Lesson 5: JWT Login Internal Flow (Deep Dive)

এটি **DRF + Simple JWT + dj-rest-auth**-এর সবচেয়ে গুরুত্বপূর্ণ Lesson।

আজকের Lesson শেষে আপনি বুঝবেন:

* JWT Login-এর পরে কী হয়?
* Access Token কোথায় তৈরি হয়?
* Refresh Token কোথায় তৈরি হয়?
* Payload কীভাবে তৈরি হয়?
* Signature কীভাবে তৈরি হয়?
* পরবর্তী Request-এ `request.user` কীভাবে সেট হয়?

---

# Complete JWT Authentication Flow

```text
                Login Request
                     │
                     ▼
          dj-rest-auth LoginView
                     │
                     ▼
          LoginSerializer.is_valid()
                     │
                     ▼
              authenticate()
                     │
                     ▼
                 User Object
                     │
                     ▼
       Simple JWT Token Generator
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
   Access Token          Refresh Token
          │                     │
          └──────────┬──────────┘
                     ▼
              JSON Response
                     │
                     ▼
      Client Stores Tokens
                     │
                     ▼
 Next Request (Authorization Header)
                     │
                     ▼
           JWTAuthentication
                     │
                     ▼
            Decode Token
                     │
                     ▼
          request.user = user
```

---

# Step 1 : Login Request

```http
POST /auth/login/
```

Body

```json
{
    "username":"atiar",
    "password":"123456"
}
```

---

# Step 2 : LoginView

Internally

```python
serializer = LoginSerializer(data=request.data)

serializer.is_valid()
```

আমরা Lesson 4-এ দেখেছি

```
authenticate()

↓

User Object
```

ধরুন

```python
<User: atiar>
```

পাওয়া গেল।

---

# Step 3 : Token Generation

এখন dj-rest-auth Simple JWT-কে Call করে।

Internally

```python
RefreshToken.for_user(user)
```

এটাই সবচেয়ে গুরুত্বপূর্ণ Method।

---

# প্রশ্ন

`for_user()` কী করে?

Internally

```
User

↓

Generate Refresh Token

↓

Generate Access Token

↓

Return Both
```

---

Simplified

```python
refresh = RefreshToken.for_user(user)

access = refresh.access_token
```

এখন

```python
refresh
```

এবং

```python
access
```

দুটো Token পাওয়া গেল।

---

# Step 4 : Refresh Token

Example

```
eyJhbGc...

.....

.....
```

Refresh Token-এর Lifetime

```
7 Days
```

---

# Step 5 : Access Token

Access Token

```
eyJhbGc....

.....

.....
```

Lifetime

```
15 Minutes
```

---

# Step 6 : JWT Structure

প্রত্যেক JWT

```
xxxxx.yyyyy.zzzzz
```

এই তিন ভাগে বিভক্ত।

```
Header

Payload

Signature
```

---

# Header

```json
{
    "alg":"HS256",

    "typ":"JWT"
}
```

Meaning

```
Algorithm

Token Type
```

---

# Payload

Example

```json
{
    "token_type":"access",

    "exp":1750000,

    "iat":1740000,

    "jti":"abc123",

    "user_id":5
}
```

---

Explanation

| Field      | Meaning          |
| ---------- | ---------------- |
| token_type | access/refresh   |
| exp        | Expire Time      |
| iat        | Issued At        |
| jti        | Unique Token ID  |
| user_id    | User Primary Key |

---

# Signature

সবচেয়ে গুরুত্বপূর্ণ অংশ।

Internally

```
Header

+

Payload

+

SECRET_KEY

↓

HS256

↓

Signature
```

Example

```
abc.xyz.signature
```

---

# প্রশ্ন

Signature কেন লাগে?

ধরুন Hacker

Payload

```
user_id

5
```

↓

পরিবর্তন করল

```
1
```

তখন

Signature আর Match করবে না।

Server সাথে সাথে Reject করবে।

---

# Token Response

```json
{
    "access":"eyJhbGc....",

    "refresh":"eyJhbGc...."
}
```

---

# Client কী করবে?

React

```
Store Access Token

↓

Store Refresh Token
```

তারপর

API Call

```http
Authorization:
Bearer eyJ....
```

---

# Step 7 : Protected API

Example

```http
GET /api/orders/
```

Header

```http
Authorization:
Bearer eyJ....
```

---

এখন

DRF

Call করবে

```python
JWTAuthentication.authenticate()
```

---

# Step 8 : JWTAuthentication

Internally

```
Read Header

↓

Extract Token

↓

Verify Signature

↓

Decode Payload

↓

Find User

↓

request.user

↓

APIView
```

---

Simplified

```python
class JWTAuthentication:

    def authenticate(self, request):

        token = self.get_raw_token(...)

        payload = self.get_validated_token(token)

        user = self.get_user(payload)

        return (user, token)
```

---

# Step 9 : Decode Payload

Payload

```json
{
"user_id":5
}
```

Internally

```python
User.objects.get(id=5)
```

Return

```python
<User: atiar>
```

---

# Step 10 : request.user

DRF

Internally

```python
request.user = user
```

এখন View-এর ভিতরে

```python
request.user.username
```

লিখলে

```
atiar
```

পাওয়া যাবে।

---

# Access Token Expire

ধরুন

```
15 Minutes
```

শেষ।

API Call

↓

401 Unauthorized

---

এখন

Client

```http
POST

/api/token/refresh/
```

Body

```json
{
"refresh":"eyJ..."
}
```

---

Server

```
Verify Refresh

↓

Generate New Access

↓

Return Access
```

Response

```json
{
"access":"new token"
}
```

---

# Complete Refresh Flow

```
Access Expired

↓

Refresh Token

↓

Verify

↓

New Access Token

↓

Continue API Calls
```

---

# Logout

Logout

↓

Blacklist Refresh Token

↓

Delete Client Token

↓

Finished

---

# Complete JWT Lifecycle

```
Login

↓

Authenticate User

↓

Generate Refresh

↓

Generate Access

↓

Client Store

↓

API Call

↓

JWTAuthentication

↓

request.user

↓

Access Expired

↓

Refresh

↓

New Access

↓

Logout

↓

Blacklist
```

---

# Source Code Relationship

```
LoginView

↓

LoginSerializer

↓

authenticate()

↓

User

↓

RefreshToken.for_user()

↓

AccessToken

↓

JSON Response
```

---

# JWTAuthentication Relationship

```
Incoming Request

↓

Authorization Header

↓

JWTAuthentication

↓

Decode

↓

Verify

↓

Find User

↓

request.user
```

---

# Interview Questions

## 1. Access Token কে Generate করে?

**Answer:**

```python
RefreshToken.for_user(user)
```

এর মাধ্যমে Refresh Token তৈরি হয় এবং সেখান থেকে

```python
refresh.access_token
```

ব্যবহার করে Access Token তৈরি হয়।

---

## 2. JWT Token-এ Password থাকে?

**Answer:**

না।

Payload-এ সাধারণত থাকে

```
user_id

exp

jti

token_type
```

Password কখনো রাখা হয় না।

---

## 3. `request.user` কখন Set হয়?

**Answer:**

Login-এর সময় নয়।

Protected API Request-এর সময়

```python
JWTAuthentication.authenticate()
```

Token Decode করে `request.user` Set করে।

---

## 4. Access Token Expire হলে কী হয়?

**Answer:**

Client Refresh Token পাঠায়। Server Refresh Token Verify করে নতুন Access Token দেয়।

---

## 5. Signature কেন দরকার?

**Answer:**

Token পরিবর্তন (Tampering) হয়েছে কিনা তা যাচাই করার জন্য। Payload পরিবর্তন করলে Signature আর মিলবে না, ফলে Token Invalid হয়ে যাবে।

---

# Homework

আজকের Lesson-এর পরে নিচের তিনটি Class-এর Source Code GitHub-এ পড়ুন:

* `RefreshToken`
* `AccessToken`
* `JWTAuthentication`

এগুলো Simple JWT-এর Core Class। Source Code পড়লে JWT Internally কীভাবে কাজ করে তা আরও পরিষ্কার হবে।

---

# 📖 Lesson 6 (সবচেয়ে গুরুত্বপূর্ণ)

পরবর্তী Lesson-এ আমরা **Simple JWT-এর Source Code Analysis** করব।

আমরা লাইন বাই লাইন বুঝব:

* `RefreshToken.for_user()` Internally কী করে?
* `AccessToken` কীভাবে Payload তৈরি করে?
* `TokenBackend.encode()` কীভাবে JWT Encode করে?
* `TokenBackend.decode()` কীভাবে Verify করে?
* `SECRET_KEY` কীভাবে Signature Generate করতে ব্যবহৃত হয়?
* HS256 Algorithm কীভাবে কাজ করে?

এটি বুঝে গেলে আপনি শুধু JWT ব্যবহারই করবেন না, **নিজে JWT Authentication System লিখতেও পারবেন**।


---------


# Lesson 6: Simple JWT Source Code Analysis (Deep Dive)

আজকের Lesson-এ আমরা **Simple JWT-এর Source Code** Conceptually বিশ্লেষণ করব।

**লক্ষ্য:**

* `RefreshToken.for_user()` কীভাবে কাজ করে?
* `AccessToken` কীভাবে তৈরি হয়?
* `TokenBackend.encode()` কীভাবে JWT বানায়?
* `TokenBackend.decode()` কীভাবে Verify করে?
* HS256 Signature কীভাবে তৈরি হয়?

---

# JWT-এর Architecture

```text
                User
                  │
                  ▼
      RefreshToken.for_user()
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
 RefreshToken          AccessToken
        │                   │
        └─────────┬─────────┘
                  ▼
         TokenBackend.encode()
                  │
                  ▼
             JWT String
```

---

# Step 1: Login Success

ধরুন User Login করেছে।

```python
user = <User: atiar>
```

এখন

```python
refresh = RefreshToken.for_user(user)
```

Call হয়।

---

# RefreshToken.for_user()

Simplified Logic

```python
class RefreshToken(Token):

    @classmethod
    def for_user(cls, user):

        token = cls()

        token["user_id"] = user.id

        return token
```

**আসল Source Code** আরও বড়, কিন্তু Concept একই।

---

## কী হলো?

User

```text
id = 5
```

↓

Token Payload

```json
{
    "user_id":5
}
```

---

# Step 2: Token Class

RefreshToken Inherit করে

```text
Token

   ▲

   │

RefreshToken
```

এবং

AccessToken-ও

```text
Token

   ▲

   │

AccessToken
```

Inherit করে।

অর্থাৎ Common Logic

```text
encode()

decode()

set_exp()

verify()
```

সব Parent Class-এ থাকে।

---

# Step 3: Token Initialization

Internally

```python
token = RefreshToken()
```

এটা নতুন Token Object তৈরি করে।

তারপর

```python
token["user_id"] = 5
```

---

এখন Payload

```json
{
    "user_id":5
}
```

---

# Step 4: Automatic Claims

Simple JWT নিজে থেকেই কিছু Claim Add করে।

Final Payload

```json
{
    "token_type":"refresh",

    "exp":1750000,

    "iat":1740000,

    "jti":"8f8db12...",


    "user_id":5
}
```

---

## Claim Meaning

| Claim      | কাজ              |
| ---------- | ---------------- |
| token_type | access / refresh |
| exp        | Expire Time      |
| iat        | Issued At        |
| jti        | Unique Token ID  |
| user_id    | User ID          |

---

# Step 5: Access Token

Internally

```python
access = refresh.access_token
```

Conceptually

```python
access = AccessToken()

access["user_id"] = refresh["user_id"]
```

এখন

Access Token

```json
{
    "token_type":"access",

    "user_id":5,

    "exp":1745000
}
```

---

# পার্থক্য

Refresh

```text
7 Days
```

Access

```text
15 Minutes
```

---

# Step 6: TokenBackend

এখনও পর্যন্ত

Token Object আছে।

JWT String হয়নি।

এখন

```python
TokenBackend.encode()
```

Call হবে।

---

# TokenBackend.encode()

Simplified

```python
payload = {

    "user_id":5,

    "exp":1745000

}

jwt.encode(
    payload,

    SECRET_KEY,

    algorithm="HS256"
)
```

---

# এখানে কী হচ্ছে?

Payload

↓

JSON

↓

Encode

↓

JWT

---

# JWT Structure

```text
Header

.

Payload

.

Signature
```

Example

```text
xxxxx.yyyyy.zzzzz
```

---

# Header

```json
{
    "alg":"HS256",

    "typ":"JWT"
}
```

---

# Payload

```json
{
    "user_id":5,

    "exp":1745000
}
```

---

# Signature

এটাই Security।

Internally

```text
Header

+

Payload

+

SECRET_KEY

↓

HMAC SHA256

↓

Signature
```

---

# SECRET_KEY কোথা থেকে আসে?

settings.py

```python
SECRET_KEY = "django-insecure-abc123..."
```

এটা Django Project-এর Secret।

**কখনো GitHub-এ Upload করবেন না।**

---

# HS256 কী?

HS256 মানে

```text
HMAC

+

SHA256
```

এটি Symmetric Algorithm।

মানে

```text
Encode

↓

SECRET_KEY

↓

Decode

↓

Same SECRET_KEY
```

---

# Step 7: Final JWT

```text
Header

↓

Base64

↓

eyJ...

.

Payload

↓

Base64

↓

eyJ...

.

Signature

↓

Base64

↓

kJ8h...
```

সব মিলিয়ে

```text
eyJ....eyJ....kJ8h...
```

---

# Step 8: Client Request

```http
GET /orders/
```

Header

```http
Authorization:
Bearer eyJ...
```

---

# Step 9: JWTAuthentication

Internally

```python
authenticate(request)
```

---

Flow

```text
Read Header

↓

Extract Token

↓

Decode

↓

Verify Signature

↓

Verify Expiration

↓

Find User

↓

request.user
```

---

# Step 10: Decode

Internally

```python
payload = jwt.decode(

token,

SECRET_KEY,

algorithms=["HS256"]

)
```

Return

```json
{
"user_id":5
}
```

---

# Step 11: User Lookup

```python
User.objects.get(id=5)
```

Return

```python
<User: atiar>
```

---

# Step 12: request.user

Internally

```python
request.user = user
```

এখন View

```python
print(request.user.username)
```

Output

```text
atiar
```

---

# যদি Hacker Payload পরিবর্তন করে?

Original

```json
{
"user_id":5
}
```

↓

পরিবর্তন

```json
{
"user_id":1
}
```

Signature আর Match করবে না।

Server

```text
Invalid Signature
```

Return করবে।

---

# যদি Token Expire হয়?

Payload

```json
{
"exp":1745000
}
```

Current Time

```text
1746000
```

↓

Token Expired

↓

401 Unauthorized

---

# Complete Encode Flow

```text
User

↓

RefreshToken.for_user()

↓

Payload

↓

TokenBackend.encode()

↓

Header

+

Payload

+

SECRET_KEY

↓

HS256

↓

JWT
```

---

# Complete Decode Flow

```text
JWT

↓

Split

↓

Header

↓

Payload

↓

Signature

↓

Verify SECRET_KEY

↓

Check Expiration

↓

User Lookup

↓

request.user
```

---

# Class Relationship

```text
Token
│
├── AccessToken
│
└── RefreshToken

        │

        ▼

TokenBackend

        │

        ▼

JWT String
```

---

# Interview Questions

## 1. `RefreshToken.for_user()` কী করে?

**Answer:**
নির্দিষ্ট User-এর জন্য একটি Refresh Token তৈরি করে, যেখানে `user_id` সহ প্রয়োজনীয় Claims (`exp`, `iat`, `jti`, `token_type`) যোগ করা হয়।

---

## 2. Access Token কীভাবে তৈরি হয়?

**Answer:**
`RefreshToken` থেকে `access_token` Property ব্যবহার করে একটি নতুন `AccessToken` তৈরি হয়।

---

## 3. `TokenBackend.encode()` কী করে?

**Answer:**
Token Payload-কে `SECRET_KEY` এবং নির্ধারিত Algorithm (যেমন HS256) ব্যবহার করে JWT String-এ Encode করে।

---

## 4. `TokenBackend.decode()` কী করে?

**Answer:**
JWT-এর Signature Verify করে, Expiration Check করে এবং Payload Return করে।

---

## 5. HS256 কী?

**Answer:**
HS256 হলো HMAC-SHA256 ভিত্তিক একটি Symmetric Signing Algorithm, যেখানে একই `SECRET_KEY` দিয়ে Token Sign এবং Verify করা হয়।

---

## 6. `SECRET_KEY` কেন গুরুত্বপূর্ণ?

**Answer:**
এটি JWT Signature তৈরির এবং Verify করার জন্য ব্যবহৃত হয়। `SECRET_KEY` ফাঁস হয়ে গেলে কেউ বৈধ Token তৈরি করতে পারে, তাই এটি সর্বদা গোপন রাখতে হবে।

---

# Homework

Simple JWT-এর অফিসিয়াল Source Code থেকে এই Class-গুলো পড়ুন (লাইন বাই লাইন না বুঝলেও Structure বোঝার চেষ্টা করুন):

* `Token`
* `AccessToken`
* `RefreshToken`
* `TokenBackend`
* `JWTAuthentication`

এগুলো বোঝা গেলে JWT সম্পর্কে আপনার ধারণা অনেক শক্ত হবে।

---

# 🎯 Lesson 7 (Production-Level JWT)

পরবর্তী Lesson-এ আমরা **Production-এ JWT কীভাবে Configure করা হয়** তা শিখব।

বিষয়গুলো হবে:

* `SIMPLE_JWT` Settings-এর প্রতিটি Option
* `ACCESS_TOKEN_LIFETIME`
* `REFRESH_TOKEN_LIFETIME`
* `ROTATE_REFRESH_TOKENS`
* `BLACKLIST_AFTER_ROTATION`
* `UPDATE_LAST_LOGIN`
* `ALGORITHM`
* `SIGNING_KEY`
* `AUTH_HEADER_TYPES`
* `AUTH_HEADER_NAME`
* Production Security Best Practices

এটি DRF Interview এবং Real Project—দুই ক্ষেত্রেই অত্যন্ত গুরুত্বপূর্ণ।

------
# Lesson 7: Production-Level JWT Configuration (Simple JWT Deep Dive)

আজকের Lesson-এ আমরা **Production-এ JWT কীভাবে Configure করা হয়** তা শিখব।

এটি DRF Interview এবং Real Project—দুই ক্ষেত্রেই অত্যন্ত গুরুত্বপূর্ণ।

---

# Lesson Goals

আজ আমরা শিখব:

* `SIMPLE_JWT` কী?
* প্রতিটি Configuration-এর কাজ
* Access Token Lifetime
* Refresh Token Lifetime
* Refresh Rotation
* Blacklist
* Signing Key
* Algorithm
* Auth Header
* Production Best Practices

---

# Step 1: Install Simple JWT

```bash
pip install djangorestframework-simplejwt
```

---

# Step 2: Add Authentication Class

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    )
}
```

## Internally

Request

```http
Authorization: Bearer eyJhbGc...
```

↓

```text
JWTAuthentication

↓

Decode Token

↓

Verify

↓

request.user
```

---

# Step 3: SIMPLE_JWT Settings

Example

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": False,

    "BLACKLIST_AFTER_ROTATION": False,

    "UPDATE_LAST_LOGIN": False,

    "ALGORITHM": "HS256",

    "SIGNING_KEY": SECRET_KEY,

    "AUTH_HEADER_TYPES": ("Bearer",),

    "AUTH_HEADER_NAME": "HTTP_AUTHORIZATION",

}
```

এখন প্রতিটি Option বুঝি।

---

# 1. ACCESS_TOKEN_LIFETIME

```python
"ACCESS_TOKEN_LIFETIME": timedelta(minutes=15)
```

মানে

Access Token

```text
15 মিনিট
```

Valid থাকবে।

Flow

```text
Login

↓

Access Token

↓

15 Minutes

↓

Expired
```

---

## কেন ছোট Lifetime?

যদি Hacker Access Token পেয়ে যায়

তাহলে

```text
15 Minutes
```

পর Token নিজেই Expire হবে।

Production-এ সাধারণত

```text
5-30 Minutes
```

ব্যবহার করা হয়।

---

# 2. REFRESH_TOKEN_LIFETIME

```python
"REFRESH_TOKEN_LIFETIME": timedelta(days=7)
```

মানে

Refresh Token

```text
7 Days
```

Valid।

Flow

```text
Login

↓

Refresh Token

↓

7 Days

↓

Expired
```

---

## কেন বড় Lifetime?

কারণ

User যেন

বারবার Login না করে।

---

# 3. ROTATE_REFRESH_TOKENS

```python
"ROTATE_REFRESH_TOKENS": True
```

এটি অনেক Interview-এ আসে।

---

## False হলে

```text
Login

↓

Refresh Token

↓

Same Refresh Token

↓

Reuse
```

একই Refresh Token বারবার ব্যবহার হবে।

---

## True হলে

```text
Old Refresh

↓

Request Refresh

↓

New Refresh

↓

Old Invalid
```

প্রতিবার Refresh করলে

নতুন Refresh Token তৈরি হবে।

---

# Example

Login

```text
Refresh A
```

↓

Refresh API

↓

Server

```text
Refresh B
```

↓

Old

```text
Refresh A
```

Invalid।

---

# সুবিধা

যদি কেউ পুরোনো Refresh Token চুরি করে

সে আর ব্যবহার করতে পারবে না।

---

# 4. BLACKLIST_AFTER_ROTATION

```python
"BLACKLIST_AFTER_ROTATION": True
```

এটি কাজ করবে যখন

```python
ROTATE_REFRESH_TOKENS=True
```

---

Flow

```text
Refresh A

↓

Refresh API

↓

Refresh B

↓

Refresh A

↓

Blacklist
```

Old Refresh Token

Database Blacklist-এ যাবে।

---

## Blacklist কেন?

যদি Hacker

পুরোনো Refresh Token ব্যবহার করে

↓

Server বলবে

```text
Token Blacklisted
```

---

# Blacklist App

Install করতে হবে

```python
INSTALLED_APPS = [

    ...

    "rest_framework_simplejwt.token_blacklist",

]
```

Migration

```bash
python manage.py migrate
```

---

Database Table

```text
OutstandingToken

BlacklistedToken
```

---

# 5. UPDATE_LAST_LOGIN

```python
"UPDATE_LAST_LOGIN": True
```

User Login করলে

Database

```text
last_login
```

Field Update হবে।

Example

Before

```text
last_login

NULL
```

After

```text
2026-06-28
10:30
```

---

Production-এ

অনেক কোম্পানি

```python
False
```

রাখে

কারণ

প্রতি Login-এ Database Write হয়।

---

# 6. ALGORITHM

```python
"ALGORITHM":"HS256"
```

মানে

```text
HMAC SHA256
```

Signature Generate হবে।

---

আরও Algorithm আছে

```text
HS256

HS384

HS512

RS256
```

---

## HS256

Same Key

```text
Sign

↓

Verify
```

---

## RS256

Different Keys

```text
Private Key

↓

Sign

↓

Public Key

↓

Verify
```

Microservice Architecture-এ

RS256 বেশি ব্যবহৃত হয়।

---

# 7. SIGNING_KEY

```python
"SIGNING_KEY":SECRET_KEY
```

মানে

JWT Signature

```text
SECRET_KEY
```

দিয়ে তৈরি হবে।

---

Production-এ

অনেকে

```python
SIGNING_KEY = env("JWT_SECRET")
```

ব্যবহার করে।

Django-এর `SECRET_KEY` এবং JWT-এর Signing Key আলাদা রাখলে Security আরও ভালো হয়।

---

# 8. AUTH_HEADER_TYPES

```python
"AUTH_HEADER_TYPES":("Bearer",)
```

মানে

Client

Header

```http
Authorization:
Bearer eyJ...
```

---

আপনি চাইলে

```python
("JWT",)
```

করতে পারেন।

তখন

```http
Authorization:
JWT eyJ...
```

---

# 9. AUTH_HEADER_NAME

```python
"AUTH_HEADER_NAME":

"HTTP_AUTHORIZATION"
```

মানে

Django

এই Header পড়বে।

```http
Authorization:
Bearer ....
```

---

# Complete JWT Refresh Flow

```text
Login

↓

Access Token

↓

Refresh Token

↓

Access Expired

↓

Refresh API

↓

Verify Refresh

↓

Generate New Access

↓

(Optional)

Generate New Refresh

↓

Blacklist Old Refresh

↓

Return Response
```

---

# Production Recommended Configuration

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "UPDATE_LAST_LOGIN": False,

    "ALGORITHM": "HS256",

    "SIGNING_KEY": SECRET_KEY,

    "AUTH_HEADER_TYPES": ("Bearer",),

}
```

---

# Security Best Practices

## ✅ Short Access Token

```text
5–15 Minutes
```

---

## ✅ Rotate Refresh Tokens

```python
ROTATE_REFRESH_TOKENS=True
```

---

## ✅ Blacklist Old Tokens

```python
BLACKLIST_AFTER_ROTATION=True
```

---

## ✅ Use HTTPS

Never send JWT over plain HTTP in production.

---

## ✅ Never Store Password in JWT

JWT Payload-এ শুধুমাত্র প্রয়োজনীয় Claim রাখুন।

ভালো Example

```json
{
    "user_id": 5,
    "role": "teacher"
}
```

খারাপ Example

```json
{
    "password": "123456"
}
```

---

## ✅ Keep Signing Key Secret

Never commit

```python
SECRET_KEY
```

to GitHub।

---

# Interview Questions

## 1. Access Token-এর Lifetime ছোট কেন?

**Answer:**
যদি Token চুরি হয়, তাহলে খুব অল্প সময়ের মধ্যেই Expire হবে। এতে Risk কমে।

---

## 2. Refresh Token-এর Lifetime বড় কেন?

**Answer:**
যাতে User বারবার Login না করেও নতুন Access Token নিতে পারে।

---

## 3. `ROTATE_REFRESH_TOKENS` কী?

**Answer:**
প্রতিবার Refresh Request-এর সময় নতুন Refresh Token Generate করে এবং (Blacklist Enable থাকলে) পুরোনো Token অকার্যকর করে দেয়।

---

## 4. `BLACKLIST_AFTER_ROTATION` কী?

**Answer:**
Rotate হওয়ার পর পুরোনো Refresh Token Blacklist-এ যোগ করে, যাতে সেটি পুনরায় ব্যবহার করা না যায়।

---

## 5. `AUTH_HEADER_TYPES` কী করে?

**Answer:**
Authorization Header-এর Prefix নির্ধারণ করে, যেমন `Bearer` বা `JWT`।

---

## 6. `SIGNING_KEY` কী?

**Answer:**
JWT-এর Signature তৈরি এবং Verify করার জন্য ব্যবহৃত Secret Key।

---

# Homework

নিজের Project-এ নিচের Configuration যোগ করুন:

```python
from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),
    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),
    "ROTATE_REFRESH_TOKENS": True,
    "BLACKLIST_AFTER_ROTATION": True,
    "UPDATE_LAST_LOGIN": False,
}
```

এবং Blacklist Support-এর জন্য:

```python
INSTALLED_APPS = [
    ...
    "rest_framework_simplejwt.token_blacklist",
]
```

তারপর Run করুন:

```bash
python manage.py migrate
```

Database-এ `token_blacklist` সম্পর্কিত Table তৈরি হয়েছে কিনা দেখুন।

---

# 🎯 Lesson 8 (Next)

এখন আমরা **dj-rest-auth + Simple JWT Integration** শিখব।

এই Lesson-এ দেখব:

* `REST_AUTH` Settings কী?
* `USE_JWT = True` Internally কী করে?
* `JWT_AUTH_COOKIE` বনাম Authorization Header
* `LoginView` কীভাবে Simple JWT-কে Call করে
* `dj-rest-auth`-এর Source Code Analysis
* React-এর সাথে Production Authentication Flow

এই Lesson শেষ হলে আপনি বুঝতে পারবেন **`dj-rest-auth` এবং `Simple JWT` একসাথে কীভাবে কাজ করে**।

---------
# Lesson 8: `dj-rest-auth` + Simple JWT Integration (Production Level)

আজকের Lesson-এ আমরা শিখব **`dj-rest-auth` এবং `Simple JWT` একসাথে কীভাবে কাজ করে।**

এটা Interview-এর জন্য যেমন গুরুত্বপূর্ণ, তেমনি Real Project-এর জন্যও।

---

# Lesson Goals

আজ আমরা শিখব

* `REST_AUTH` Settings
* `USE_JWT = True`
* `JWT_AUTH_COOKIE`
* `JWT_AUTH_REFRESH_COOKIE`
* LoginView Internals
* Cookie Authentication vs Authorization Header
* React Authentication Flow

---

# Architecture

```text
                    React

                      │

                      ▼

          POST /auth/login/

                      │

                      ▼

            dj-rest-auth LoginView

                      │

                      ▼

          LoginSerializer

                      │

                      ▼

              authenticate()

                      │

                      ▼

                  User Object

                      │

                      ▼

              Simple JWT

                      │

         ┌────────────┴────────────┐

         ▼                         ▼

    Access Token             Refresh Token

         │                         │

         └────────────┬────────────┘

                      ▼

              JSON / Cookies
```

---

# Step 1

Install

```bash
pip install dj-rest-auth

pip install djangorestframework-simplejwt
```

---

# Step 2

settings.py

```python
INSTALLED_APPS = [

    ...

    "rest_framework",

    "dj_rest_auth",

]
```

---

# Step 3

REST Framework

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES":[

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ]

}
```

এখন সব API

JWT Authentication ব্যবহার করবে।

---

# Step 4

REST_AUTH Configuration

```python
REST_AUTH = {

    "USE_JWT": True,

}
```

---

## প্রশ্ন

`USE_JWT=True`

আসলে কী করে?

অনেকে মনে করে

```text
JWT Generate করে।
```

না।

এটা শুধু

```text
dj-rest-auth

↓

TokenAuthentication

↓

Simple JWT
```

Switch করে দেয়।

---

## False হলে

Login Response

```json
{
    "key":"abc123"
}
```

Database Token

---

## True হলে

```json
{
    "access":"eyJ...",

    "refresh":"eyJ..."
}
```

Simple JWT

---

# Internally

```text
LoginView

↓

if USE_JWT:

↓

JWT Serializer

↓

RefreshToken.for_user()

↓

Response
```

---

# Step 5

URL

```python
urlpatterns=[

path(

"auth/",

include("dj_rest_auth.urls")

)

]
```

---

এখন

Login API

```http
POST

/auth/login/
```

---

# Step 6

Client Login

```json
{

"username":"atiar",

"password":"123456"

}
```

↓

LoginSerializer

↓

authenticate()

↓

User

↓

JWT Serializer

↓

Simple JWT

↓

Access + Refresh

↓

Response

---

# Login Response

```json
{
    "access":"eyJhbGc...",

    "refresh":"eyJhbGc..."
}
```

---

# Step 7

Protected API

React

```http
Authorization:

Bearer eyJ....
```

↓

DRF

↓

JWTAuthentication

↓

request.user

↓

APIView

---

# JWT_AUTH_COOKIE

এখন আসি

Cookie Authentication-এ।

Example

```python
REST_AUTH={

"USE_JWT":True,

"JWT_AUTH_COOKIE":"access"

}
```

---

## প্রশ্ন

এটা কী?

Login হলে

Server

Header

```http
Set-Cookie:

access=eyJ....
```

Browser

Automatically

Cookie Store করবে।

---

Diagram

```text
Login

↓

Response

↓

Set-Cookie

↓

Browser

↓

Cookie Saved
```

---

# এরপর

React

API Call

Browser

Automatically

```http
Cookie

access=eyJ...
```

পাঠাবে।

---

# JWT_AUTH_REFRESH_COOKIE

```python
REST_AUTH={

"JWT_AUTH_REFRESH_COOKIE":"refresh"

}
```

মানে

Refresh Token

Cookie-তে Save হবে।

---

# Example

Browser

Cookies

```text
access

refresh
```

---

# Cookie বনাম LocalStorage

## Option 1

LocalStorage

```text
Access Token

↓

localStorage
```

Header

```http
Authorization:

Bearer token
```

---

## Option 2

Cookie

```text
Cookie

↓

Automatically Sent
```

---

# Comparison

| LocalStorage                | HttpOnly Cookie                |
| --------------------------- | ------------------------------ |
| JavaScript Access করতে পারে | JavaScript Access করতে পারে না |
| XSS Attack-এর Risk বেশি     | XSS থেকে তুলনামূলক নিরাপদ      |
| Header নিজে Add করতে হয়    | Browser Automatically পাঠায়   |

---

# Production Recommendation

অনেক কোম্পানি

```text
Access Token

↓

Memory

Refresh Token

↓

HttpOnly Cookie
```

ব্যবহার করে।

কারণ

Refresh Token

JavaScript Access করতে পারে না।

---

# JWT_AUTH_SECURE

```python
REST_AUTH={

"JWT_AUTH_SECURE":True

}
```

মানে

HTTPS

ছাড়া Cookie যাবে না।

Production-এ

Always

```python
True
```

---

# JWT_AUTH_HTTPONLY

```python
REST_AUTH={

"JWT_AUTH_HTTPONLY":True

}
```

মানে

JavaScript

```javascript
document.cookie
```

দিয়ে Access Token পড়তে পারবে না।

Security বাড়ে।

---

# JWT_AUTH_SAMESITE

```python
REST_AUTH={

"JWT_AUTH_SAMESITE":"Lax"

}
```

Possible Values

```text
Lax

Strict

None
```

CSRF Protection-এর জন্য ব্যবহৃত হয়।

---

# Production Cookie Config

```python
REST_AUTH = {

    "USE_JWT":True,

    "JWT_AUTH_COOKIE":"access",

    "JWT_AUTH_REFRESH_COOKIE":"refresh",

    "JWT_AUTH_HTTPONLY":True,

    "JWT_AUTH_SECURE":True,

    "JWT_AUTH_SAMESITE":"Lax",

}
```

---

# Complete Login Flow

```text
React

↓

POST Login

↓

LoginView

↓

LoginSerializer

↓

authenticate()

↓

RefreshToken.for_user()

↓

Access Token

↓

Refresh Token

↓

Set Cookie

↓

Browser
```

---

# Complete Protected Request

```text
Browser

↓

Cookie/Header

↓

JWTAuthentication

↓

Decode

↓

Verify

↓

request.user

↓

APIView
```

---

# Logout

Logout

↓

Delete Cookie

↓

Blacklist Refresh

↓

Response

---

# React Flow

```text
Login

↓

Store Access

↓

API Calls

↓

Access Expired

↓

Refresh API

↓

New Access

↓

Continue

↓

Logout

↓

Delete Tokens
```

---

# Interview Questions

## 1. `USE_JWT=True` কী করে?

**Answer:**

`dj-rest-auth`-কে Token Authentication-এর পরিবর্তে **Simple JWT** ব্যবহার করতে বলে। ফলে Login Response-এ Access এবং Refresh Token Return হয়।

---

## 2. `JWT_AUTH_COOKIE` কী?

**Answer:**

Access Token Browser Cookie-তে Store করার জন্য ব্যবহৃত হয়।

---

## 3. `JWT_AUTH_HTTPONLY` কেন ব্যবহার করা হয়?

**Answer:**

JavaScript যাতে Cookie পড়তে না পারে। এতে XSS Attack-এর Risk কমে।

---

## 4. `JWT_AUTH_SECURE` কী?

**Answer:**

HTTPS Connection ছাড়া Cookie পাঠানো হবে না।

---

## 5. LocalStorage না Cookie—কোনটি ভালো?

**Answer:**

Production-এ সাধারণত HttpOnly Cookie বেশি নিরাপদ, কারণ JavaScript Cookie পড়তে পারে না। তবে Cookie ব্যবহার করলে CSRF Protection-এর বিষয়টি সঠিকভাবে Configure করতে হয়।

---

# Real-World Architecture (Recommended)

```text
Frontend (React)

↓

Login

↓

Access Token (Memory)

↓

Refresh Token (HttpOnly Cookie)

↓

API Call

↓

401?

↓

Refresh Endpoint

↓

New Access Token

↓

Retry Request
```

এটি বর্তমানে অনেক Professional Web Application ব্যবহার করে।

---

# Homework

নিজের Project-এ নিচের Configuration যোগ করে দেখুন:

```python
REST_AUTH = {
    "USE_JWT": True,
    "JWT_AUTH_COOKIE": "access",
    "JWT_AUTH_REFRESH_COOKIE": "refresh",
}
```

তারপর Login API Call করে দেখুন:

* Response-এ Access/Refresh Token আসছে কি?
* Cookie Set হচ্ছে কি? (Browser DevTools → Application → Cookies)

---

# 🎯 Lesson 9 (Professional Level)

এখন আমরা **Custom User Model + Custom JWT Claims + Role-based Authentication** শিখব।

এই Lesson-এ দেখব:

* কেন শুরুতেই Custom User Model বানানো উচিত
* Email দিয়ে Login
* Role (`Admin`, `Teacher`, `Student`)
* JWT Payload-এ Custom Claims (যেমন `role`, `email`, `full_name`)
* Custom Permission Classes
* Production-ready Authentication Architecture

এটি আপনার **Exam SaaS Project**-এর Authentication System তৈরির ভিত্তি হবে।

----------
# Lesson 9: Custom User Model + Role-Based Authentication + Custom JWT Claims

> **এই Lesson আপনার Exam SaaS Project-এর জন্য সবচেয়ে গুরুত্বপূর্ণ।**
>
> Teacher, Student, Admin—সবকিছু এই Architecture-এর উপর নির্ভর করবে।

---

# আজ আমরা কী শিখব?

* কেন শুরুতেই Custom User Model ব্যবহার করা উচিত
* Custom User Model তৈরি করা
* Role Field যোগ করা
* Email দিয়ে Login
* JWT Payload-এ Custom Claims যোগ করা
* Role-based Authentication
* Role-based Permission
* আপনার Exam SaaS Project-এর Authentication Design

---

# আমাদের Project Architecture

ধরুন আপনার Project

```text
Teacher

↓

Create Course

↓

Course Code

↓

Student Join

↓

Exam

↓

Result
```

এখানে তিন ধরনের User আছে

```text
Admin

Teacher

Student
```

---

# Problem

Default Django User

```python
from django.contrib.auth.models import User
```

এতে আছে

```text
username

email

first_name

last_name

password
```

কিন্তু নেই

```text
role

phone

profile_picture

department

university
```

---

# Solution

Custom User Model

---

# Project Structure

```text
accounts/

    models.py

    manager.py

    serializers.py

    views.py

    permissions.py
```

---

# Step 1

Create App

```bash
python manage.py startapp accounts
```

---

# Step 2

settings.py

```python
INSTALLED_APPS = [

    ...

    "accounts",

]
```

---

# Step 3

AUTH_USER_MODEL

```python
AUTH_USER_MODEL = "accounts.User"
```

> ⚠️ **সবচেয়ে গুরুত্বপূর্ণ Rule**
>
> **Project শুরু করার আগেই এটি সেট করবেন।**
>
> Project-এ Migration হওয়ার পরে User Model পরিবর্তন করা খুব কঠিন।

---

# Step 4

models.py

```python
from django.contrib.auth.models import AbstractUser

from django.db import models


class User(AbstractUser):

    pass
```

এখনও পর্যন্ত

```text
AbstractUser

↓

User
```

---

# কেন AbstractUser?

কারণ এতে Django-এর Built-in Features সব থাকে

```text
username

password

groups

permissions

is_staff

is_superuser

last_login
```

---

# Step 5

Role Field

```python
class User(AbstractUser):

    class Role(models.TextChoices):

        ADMIN = "admin", "Admin"

        TEACHER = "teacher", "Teacher"

        STUDENT = "student", "Student"

    role = models.CharField(

        max_length=20,

        choices=Role.choices,

        default=Role.STUDENT

    )
```

---

Database

| username | role    |
| -------- | ------- |
| atiar    | teacher |
| fahim    | student |
| admin    | admin   |

---

# আরও Field যোগ করা

```python
phone = models.CharField(max_length=20)

profile_picture = models.ImageField(
    upload_to="profiles/",
    null=True,
    blank=True
)

bio = models.TextField(blank=True)
```

---

# এখন User Model

```text
username

email

password

role

phone

profile_picture

bio
```

---

# কেন Custom User?

কারণ ভবিষ্যতে

```text
Teacher

↓

Department

↓

Experience

↓

Qualification
```

সব যোগ করা যাবে।

---

# Step 6

Migration

```bash
python manage.py makemigrations

python manage.py migrate
```

---

# Email Login

Default

```text
username
```

দিয়ে Login হয়।

কিন্তু Professional Project-এ

```text
email
```

দিয়ে Login করা হয়।

---

# Example

Instead of

```json
{
    "username":"atiar",

    "password":"123456"
}
```

Use

```json
{
    "email":"atiar@gmail.com",

    "password":"123456"
}
```

---

# Custom Authentication Backend

```python
from django.contrib.auth.backends import ModelBackend

from django.contrib.auth import get_user_model

User = get_user_model()


class EmailBackend(ModelBackend):

    def authenticate(

        self,

        request,

        username=None,

        password=None,

        **kwargs

    ):

        email = kwargs.get("email") or username

        try:

            user = User.objects.get(email=email)

        except User.DoesNotExist:

            return None

        if user.check_password(password):

            return user

        return None
```

---

settings.py

```python
AUTHENTICATION_BACKENDS = [

    "accounts.backends.EmailBackend",

]
```

---

Flow

```text
Email

↓

Find User

↓

Check Password

↓

Return User
```

---

# JWT Payload

Default Payload

```json
{
    "user_id":5,

    "token_type":"access",

    "exp":1740000
}
```

---

কিন্তু

আমরা চাই

```json
{
    "user_id":5,

    "role":"teacher",

    "email":"atiar@gmail.com",

    "full_name":"Md Atiar Rahman"
}
```

---

# Custom JWT Claims

Simple JWT

```python
from rest_framework_simplejwt.serializers import TokenObtainPairSerializer


class MyTokenSerializer(TokenObtainPairSerializer):

    @classmethod

    def get_token(cls, user):

        token = super().get_token(user)

        token["role"] = user.role

        token["email"] = user.email

        token["username"] = user.username

        return token
```

---

Generated Payload

```json
{
    "user_id":5,

    "role":"teacher",

    "email":"atiar@gmail.com",

    "username":"atiar"
}
```

---

# কেন Role Token-এ রাখব?

কারণ

Frontend

Immediate জানতে পারবে

```text
Teacher

না

Student
```

---

React

```text
Login

↓

Decode Token

↓

role

↓

Teacher Dashboard
```

---

# Role-based Permission

Example

```text
Teacher

↓

Can Create Exam

Student

↓

Cannot Create Exam
```

---

Custom Permission

```python
from rest_framework.permissions import BasePermission


class IsTeacher(BasePermission):

    def has_permission(self, request, view):

        return (

            request.user.is_authenticated

            and

            request.user.role == "teacher"

        )
```

---

Use

```python
permission_classes = [IsTeacher]
```

---

Flow

```text
Request

↓

JWTAuthentication

↓

request.user

↓

IsTeacher

↓

Allow

or

Deny
```

---

# Student Permission

```python
class IsStudent(BasePermission):

    def has_permission(self, request, view):

        return (

            request.user.role == "student"

        )
```

---

# Admin Permission

```python
class IsAdmin(BasePermission):

    def has_permission(self, request, view):

        return request.user.role == "admin"
```

---

# Complete Flow

```text
Login

↓

JWT Token

↓

Payload

↓

role

↓

API Request

↓

JWTAuthentication

↓

request.user

↓

Permission Class

↓

APIView
```

---

# Exam SaaS Authentication

Teacher

```text
Login

↓

Teacher Dashboard

↓

Create Course

↓

Create Exam

↓

Publish Result
```

---

Student

```text
Login

↓

Student Dashboard

↓

Join Course

↓

Attend Exam

↓

View Result
```

---

Admin

```text
Login

↓

Manage Users

↓

Manage Teachers

↓

Analytics
```

---

# Recommended Project Structure

```text
accounts/

    models.py

    managers.py

    serializers.py

    permissions.py

    authentication.py

    urls.py

    views.py
```

---

# Interview Questions

## 1. কেন Custom User Model ব্যবহার করবেন?

**Answer:**

ভবিষ্যতে `role`, `phone`, `profile_picture`, `bio` ইত্যাদি Field সহজে যোগ করার জন্য এবং Authentication System নিজের প্রয়োজন অনুযায়ী Customize করার জন্য।

---

## 2. `AUTH_USER_MODEL` কখন Set করা উচিত?

**Answer:**

Project-এর একদম শুরুতে, প্রথম Migration করার আগে।

---

## 3. `AbstractUser` এবং `AbstractBaseUser`-এর মধ্যে পার্থক্য কী?

| AbstractUser                                | AbstractBaseUser                          |
| ------------------------------------------- | ----------------------------------------- |
| Django-এর Built-in User Features Ready থাকে | একদম শুরু থেকে নিজে সব Implement করতে হয় |
| সহজ                                         | Advanced                                  |
| অধিকাংশ Project-এর জন্য Recommended         | বিশেষ Requirement থাকলে ব্যবহার করা হয়   |

---

## 4. JWT-তে Custom Claims কী?

**Answer:**

Default Claims-এর বাইরে অতিরিক্ত তথ্য (যেমন `role`, `email`, `username`) Token Payload-এ যোগ করাকে Custom Claims বলে।

---

## 5. Permission Class কেন ব্যবহার করবেন?

**Answer:**

নির্দিষ্ট User Role বা Condition অনুযায়ী API Access নিয়ন্ত্রণ করার জন্য।

---

# Homework

একটি `accounts` App তৈরি করে:

1. Custom User Model বানান।
2. `role` Field যোগ করুন।
3. `AUTH_USER_MODEL` Configure করুন।
4. `IsTeacher` Permission লিখুন।
5. JWT Payload-এ `role` যোগ করুন।

---

# 🎯 Lesson 10 (Professional DRF Authentication)

পরবর্তী Lesson-এ আমরা **Production-Level Authentication System** তৈরি করব, যেখানে থাকবে:

* ✅ Registration API
* ✅ Email Verification
* ✅ Login API
* ✅ Logout API
* ✅ Password Change
* ✅ Forgot Password
* ✅ Reset Password
* ✅ Refresh Token API
* ✅ User Profile API
* ✅ React Authentication Flow (Axios + Auto Refresh)
* ✅ Complete Authentication Folder Structure

এটি হবে একটি **Production-ready Authentication Module**, যা আপনি ভবিষ্যতের যেকোনো Django REST Framework Project-এ পুনরায় ব্যবহার করতে পারবেন।

---
# Lesson 10: Production-Ready Authentication System (DRF + dj-rest-auth + Simple JWT + React)

এটি আমাদের Authentication Series-এর **সবচেয়ে গুরুত্বপূর্ণ Lesson**।

এখানে আমরা একটি **Production-Level Authentication System** ডিজাইন করব, যা আপনি আপনার **Exam SaaS Project**, **E-commerce**, **Job Portal**, বা যেকোনো বড় Project-এ ব্যবহার করতে পারবেন।

---

# আজ আমরা কী শিখব?

আমরা নিচের Authentication Flow তৈরি করব:

```text
Register
    │
    ▼
Email Verification
    │
    ▼
Login
    │
    ▼
Access + Refresh Token
    │
    ▼
Protected APIs
    │
    ▼
Auto Refresh
    │
    ▼
Logout
```

---

# Complete Authentication Architecture

```text
                 React

                   │

                   ▼

            Register API

                   │

                   ▼

         Email Verification

                   │

                   ▼

              Login API

                   │

                   ▼

      Access + Refresh Token

                   │

                   ▼

      Protected API Requests

                   │

                   ▼

       Access Token Expired

                   │

                   ▼

         Refresh Token API

                   │

                   ▼

         New Access Token

                   │

                   ▼

              Logout API
```

---

# Project Structure

```text
accounts/

    models.py

    serializers.py

    permissions.py

    authentication.py

    views.py

    urls.py

    managers.py

    tokens.py

    signals.py

config/

    settings.py

    urls.py
```

---

# Authentication APIs

| Method | Endpoint                        | Description          |
| ------ | ------------------------------- | -------------------- |
| POST   | `/auth/register/`               | Register User        |
| POST   | `/auth/login/`                  | Login                |
| POST   | `/auth/logout/`                 | Logout               |
| POST   | `/auth/token/refresh/`          | Refresh Access Token |
| GET    | `/auth/user/`                   | Current User         |
| PATCH  | `/auth/user/`                   | Update Profile       |
| POST   | `/auth/password/change/`        | Change Password      |
| POST   | `/auth/password/reset/`         | Forgot Password      |
| POST   | `/auth/password/reset/confirm/` | Reset Password       |
| POST   | `/auth/email/verify/`           | Verify Email         |

---

# Step 1: Registration

Client

```http
POST /auth/register/
```

Body

```json
{
    "username":"atiar",

    "email":"atiar@gmail.com",

    "password1":"12345678",

    "password2":"12345678"
}
```

---

## Server Flow

```text
Validate Data

↓

Create User

↓

Hash Password

↓

Save User

↓

Send Verification Email

↓

Response
```

---

Database

```text
User

↓

is_active=False
```

Production-এ সাধারণত Email Verify না করা পর্যন্ত Account Active করা হয় না।

---

# Step 2: Email Verification

User Email পাবে

```text
Click Verification Link
```

↓

Frontend

↓

API

```http
POST /auth/email/verify/
```

↓

Server

```text
Verify Token

↓

is_active=True
```

---

# Step 3: Login

```http
POST /auth/login/
```

↓

```text
LoginSerializer

↓

authenticate()

↓

User
```

↓

Simple JWT

↓

```text
Access Token

Refresh Token
```

---

Response

```json
{
    "access":"xxxxx",

    "refresh":"yyyyy"
}
```

---

# Step 4: Protected APIs

Header

```http
Authorization: Bearer eyJ....
```

↓

JWTAuthentication

↓

```text
Decode

↓

Verify

↓

request.user
```

---

Example

```python
class CourseListAPIView(ListAPIView):

    permission_classes = [

        IsAuthenticated

    ]
```

---

# Step 5: User Profile API

```http
GET /auth/user/
```

Response

```json
{
    "id":1,

    "username":"atiar",

    "email":"atiar@gmail.com",

    "role":"teacher"
}
```

---

Update Profile

```http
PATCH /auth/user/
```

Body

```json
{
    "phone":"017xxxxxxxx"
}
```

---

# Step 6: Change Password

```http
POST /auth/password/change/
```

Body

```json
{
    "old_password":"123456",

    "new_password1":"abcdef12",

    "new_password2":"abcdef12"
}
```

Flow

```text
Verify Old Password

↓

Validate New Password

↓

Hash

↓

Save
```

---

# Step 7: Forgot Password

```http
POST /auth/password/reset/
```

Body

```json
{
    "email":"atiar@gmail.com"
}
```

↓

Email পাঠানো হবে

↓

User Link-এ Click করবে

↓

```http
POST /auth/password/reset/confirm/
```

↓

Password Update

---

# Step 8: Refresh Token

Access Token Expired

↓

```http
POST /auth/token/refresh/
```

Body

```json
{
"refresh":"xxxxx"
}
```

↓

Response

```json
{
"access":"new token"
}
```

---

# Step 9: Logout

```http
POST /auth/logout/
```

Flow

```text
Receive Refresh Token

↓

Blacklist Token

↓

Delete Cookie (if used)

↓

Success
```

---

# React Authentication Flow

```text
User Login

↓

Store Access Token (Memory)

↓

Store Refresh Token (HttpOnly Cookie)

↓

Axios Request

↓

401?

↓

Refresh Token API

↓

Retry Request

↓

Success
```

---

# Axios Interceptor Flow

```text
API Request

↓

Access Token

↓

401 Unauthorized

↓

Refresh Token

↓

New Access Token

↓

Retry Original Request
```

এটাই Professional React Application-এ সবচেয়ে বেশি ব্যবহৃত Pattern।

---

# Role-Based Authentication

Teacher

```text
Create Exam

Create Question

Publish Result
```

Student

```text
Join Course

Attend Exam

View Result
```

Admin

```text
Manage Users

Analytics

Reports
```

---

# Recommended Permission Structure

```text
permissions.py

    IsTeacher

    IsStudent

    IsAdmin

    IsCourseOwner

    IsExamOwner
```

---

# Security Best Practices

## ✅ Password

সবসময়

```python
set_password()
```

ব্যবহার করুন।

কখনো

```python
user.password="123456"
```

করবেন না।

---

## ✅ JWT

Access Token

```text
5-15 Minutes
```

Refresh Token

```text
7 Days
```

---

## ✅ Refresh Rotation

```python
ROTATE_REFRESH_TOKENS=True
```

---

## ✅ Blacklist

```python
BLACKLIST_AFTER_ROTATION=True
```

---

## ✅ HTTPS

Production-এ শুধুমাত্র HTTPS ব্যবহার করুন।

---

## ✅ Environment Variables

```text
SECRET_KEY

EMAIL_PASSWORD

DATABASE_URL

JWT_SECRET
```

`.env` File-এ রাখুন।

---

# Complete Authentication Sequence

```text
Register

↓

Verify Email

↓

Login

↓

JWT Token

↓

Protected APIs

↓

Refresh Token

↓

New Access

↓

Logout
```

---

# Authentication Lifecycle

```text
Register

↓

Activate

↓

Login

↓

Access Token

↓

API Calls

↓

Refresh

↓

Continue

↓

Logout
```

---

# Authentication Checklist

| Feature           | Status |
| ----------------- | ------ |
| Custom User Model | ✅      |
| JWT Login         | ✅      |
| Refresh Token     | ✅      |
| Email Login       | ✅      |
| Role Field        | ✅      |
| Custom Claims     | ✅      |
| Protected APIs    | ✅      |
| Password Reset    | ✅      |
| Password Change   | ✅      |
| User Profile      | ✅      |
| Logout            | ✅      |
| Refresh Rotation  | ✅      |
| Blacklist         | ✅      |

---

# Exam SaaS Authentication Design

```text
Teacher

↓

Create Course

↓

Generate Course Code

↓

Student Join

↓

Attend Exam

↓

Auto Submit

↓

Result

↓

Leaderboard
```

এই পুরো Flow Authentication-এর উপর নির্ভর করবে।

---

# Interview Questions

### 1. Production Authentication Flow কী?

**Answer:**

```text
Register

↓

Verify Email

↓

Login

↓

JWT

↓

Protected APIs

↓

Refresh

↓

Logout
```

---

### 2. কেন Email Verification ব্যবহার করবেন?

**Answer:**

* Fake Account কমাতে
* Email Ownership নিশ্চিত করতে
* Security বাড়াতে

---

### 3. কেন Refresh Token Blacklist করবেন?

**Answer:**

Logout বা Refresh Rotation-এর পরে পুরোনো Refresh Token পুনরায় ব্যবহার ঠেকাতে।

---

### 4. React-এ Access Token কোথায় রাখবেন?

**Answer:**

Production-এ সাধারণত Access Token Memory-তে রাখা হয়। Refresh Token HttpOnly Cookie-তে রাখা হয়।

---

### 5. Registration-এর সময় Password কীভাবে Save করবেন?

**Answer:**

`set_password()` বা `create_user()` ব্যবহার করবেন। এগুলো Password Hash করে Save করে।

---

# 🎯 আমাদের Authentication Series এখানে শেষ।

আপনি এখন ধারণাগতভাবে শিখেছেন:

* DRF Authentication
* JWT
* Simple JWT
* dj-rest-auth
* Custom User Model
* Custom Claims
* Role-based Authentication
* Production Authentication Architecture

## এরপর কী শিখবেন?

আপনার **Exam SaaS Project**-এর জন্য আমি এই ক্রমে এগোনোর পরামর্শ দেব:

1. **Lesson 11:** Custom Permission Classes (Advanced)
2. **Lesson 12:** Django Groups & Permissions (RBAC)
3. **Lesson 13:** Object-Level Permissions
4. **Lesson 14:** DRF Throttling (Rate Limiting)
5. **Lesson 15:** API Security (CORS, CSRF, XSS, SQL Injection, HTTPS)
6. **Lesson 16:** React + Django Authentication (Axios Interceptors, Auto Refresh, Protected Routes)
7. **Lesson 17:** Complete Authentication Module (Production Code)

এই সিরিজ শেষ হলে আপনি একটি **Professional Production-Level Authentication System** নিজে তৈরি করতে পারবেন এবং এটি আপনার SaaS Exam Platform-এ সরাসরি ব্যবহার করতে পারবেন।

----------
# Lesson 11: Custom Permission Classes (Advanced DRF)

> **এই Lesson DRF Interview এবং বড় Project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।**

Authentication-এর কাজ হলো **"User কে?"**

Permission-এর কাজ হলো **"User কী করতে পারবে?"**

এটাই Authentication এবং Authorization-এর মূল পার্থক্য।

---

# আজ আমরা কী শিখব?

* Authentication vs Permission
* Permission Flow
* Built-in Permission Classes
* Custom Permission Class
* Object-Level Permission
* Combining Multiple Permissions
* Permission in ViewSet
* Permission in Your Exam SaaS Project
* Interview Questions

---

# Big Picture

```text
Request
    │
    ▼
Authentication
    │
(request.user)
    │
    ▼
Permission
    │
Allow / Deny
    │
    ▼
APIView
```

---

# Authentication vs Permission

| Authentication         | Permission            |
| ---------------------- | --------------------- |
| User কে?               | User কী করতে পারবে?   |
| Login Verify করে       | Access Control করে    |
| `request.user` Set করে | True/False Return করে |

Example

```text
Login Success

↓

request.user = Teacher

↓

Permission Check

↓

Teacher?

↓

Allow
```

---

# DRF Request Lifecycle

```text
Incoming Request

↓

Authentication

↓

Throttle

↓

Permission

↓

APIView Method

↓

Serializer

↓

Response
```

Interview-এ অনেক সময় জিজ্ঞেস করে:

> Authentication আগে হয় নাকি Permission?

**Answer: Authentication → Permission**

---

# Example

Teacher API

```python
class CreateExamAPIView(APIView):

    permission_classes = [IsAuthenticated]
```

Flow

```text
Request

↓

JWTAuthentication

↓

request.user

↓

IsAuthenticated

↓

True

↓

post()
```

---

# Built-in Permission Classes

DRF-এ অনেক Built-in Permission আছে।

## 1. AllowAny

```python
permission_classes = [AllowAny]
```

মানে

```text
Everyone Can Access
```

Example

```text
Register

Login

Public Courses
```

---

## 2. IsAuthenticated

```python
permission_classes = [IsAuthenticated]
```

মানে

```text
Login Required
```

Example

```text
Profile

Orders

Dashboard
```

---

## 3. IsAdminUser

```python
permission_classes = [IsAdminUser]
```

Check করে

```python
request.user.is_staff
```

---

## 4. IsAuthenticatedOrReadOnly

```python
permission_classes = [
    IsAuthenticatedOrReadOnly
]
```

Meaning

| Method | Permission     |
| ------ | -------------- |
| GET    | Everyone       |
| POST   | Login Required |
| PUT    | Login Required |
| DELETE | Login Required |

Example

Blog

```text
GET Articles

↓

Everyone

POST Article

↓

Authenticated User
```

---

# Custom Permission

এখন ধরুন

শুধু Teacher Exam Create করতে পারবে।

---

## Step 1

permissions.py

```python
from rest_framework.permissions import BasePermission

class IsTeacher(BasePermission):

    def has_permission(self, request, view):

        return (
            request.user.is_authenticated
            and
            request.user.role == "teacher"
        )
```

---

## Flow

```text
Request

↓

JWTAuthentication

↓

request.user

↓

IsTeacher

↓

Teacher?

↓

True

↓

APIView
```

---

# View

```python
class CreateExamAPIView(APIView):

    permission_classes = [
        IsTeacher
    ]
```

---

Teacher

```text
Teacher

↓

Create Exam

↓

Allowed
```

Student

```text
Student

↓

Create Exam

↓

403 Forbidden
```

---

# Response

```json
{
    "detail": "You do not have permission to perform this action."
}
```

---

# Student Permission

```python
class IsStudent(BasePermission):

    def has_permission(self, request, view):

        return (
            request.user.is_authenticated
            and
            request.user.role == "student"
        )
```

---

# Admin Permission

```python
class IsAdmin(BasePermission):

    def has_permission(self, request, view):

        return (
            request.user.is_authenticated
            and
            request.user.role == "admin"
        )
```

---

# Multiple Permissions

একাধিক Permission ব্যবহার করা যায়।

```python
permission_classes = [
    IsAuthenticated,
    IsTeacher
]
```

Flow

```text
Login?

↓

Yes

↓

Teacher?

↓

Yes

↓

Allow
```

যেকোনো একটি False হলে

```text
403 Forbidden
```

---

# How DRF Executes Permissions

Internally

```python
for permission in self.get_permissions():

    if not permission.has_permission(request, self):

        deny()
```

মানে

সব Permission Check হবে।

---

# Object-Level Permission

এটি Interview-এর Favorite Question।

Question

Teacher কি **সব Exam Edit** করতে পারবে?

না।

শুধু **নিজের তৈরি Exam** Edit করতে পারবে।

---

Exam Table

| Exam   | Owner     |
| ------ | --------- |
| Python | Teacher A |
| Django | Teacher B |

Teacher A

```text
Edit Python

↓

Allowed
```

Teacher A

```text
Edit Django

↓

Forbidden
```

---

## has_object_permission()

```python
class IsExamOwner(BasePermission):

    def has_object_permission(
        self,
        request,
        view,
        obj
    ):

        return obj.teacher == request.user
```

---

Flow

```text
Request

↓

Get Exam

↓

Exam.teacher

↓

request.user

↓

Equal?

↓

Allow
```

---

# GenericAPIView

DRF

```python
self.check_object_permissions(
    request,
    obj
)
```

Call করে।

---

# Example

```python
class ExamUpdateAPIView(
    RetrieveUpdateAPIView
):

    permission_classes = [
        IsTeacher,
        IsExamOwner
    ]
```

---

# ViewSet Permission

```python
class ExamViewSet(ModelViewSet):

    permission_classes = [
        IsAuthenticated,
        IsTeacher
    ]
```

---

# Dynamic Permission

Interview Question

Login ছাড়া

List দেখতে পারবে।

Create করতে হলে Teacher লাগবে।

---

Solution

```python
class ExamViewSet(ModelViewSet):

    def get_permissions(self):

        if self.action == "list":

            return [AllowAny()]

        elif self.action == "create":

            return [IsTeacher()]

        return [IsAuthenticated()]
```

---

Flow

```text
GET /exams/

↓

AllowAny

-------------------

POST /exams/

↓

IsTeacher

-------------------

PUT

↓

IsAuthenticated
```

---

# Real Exam SaaS Permissions

## Teacher

```text
Create Course

Create Exam

Upload Questions

Publish Result
```

---

## Student

```text
Join Course

Attend Exam

View Result
```

---

## Admin

```text
Manage Users

Delete Courses

Analytics

Reports
```

---

# Permission Architecture

```text
permissions.py

IsTeacher

IsStudent

IsAdmin

IsCourseOwner

IsExamOwner

IsEnrollmentOwner

IsResultOwner
```

---

# Folder Structure

```text
accounts/

permissions.py

courses/

permissions.py

exams/

permissions.py

results/

permissions.py
```

এভাবে Feature অনুযায়ী Permission আলাদা রাখলে Project Maintain করা সহজ হয়।

---

# Common Mistakes

## ❌ Mistake 1

```python
if request.user.role == "teacher":
```

Authentication Check নেই।

সঠিক

```python
request.user.is_authenticated
```

Check করুন।

---

## ❌ Mistake 2

Business Logic View-এর ভিতরে লেখা।

```python
if request.user.role != "teacher":

    return Response(...)
```

এটি View-তে না লিখে Permission Class-এ লিখুন।

---

## ❌ Mistake 3

সব Permission এক File-এ 1000 Line।

Feature অনুযায়ী ভাগ করুন।

---

# Complete Permission Flow

```text
Client

↓

JWT Token

↓

Authentication

↓

request.user

↓

Permission

↓

Object Permission

↓

APIView

↓

Serializer

↓

Database
```

---

# Interview Questions

## 1. Authentication এবং Permission-এর মধ্যে পার্থক্য কী?

**Answer:**

* Authentication User-এর পরিচয় যাচাই করে।
* Permission User নির্দিষ্ট Action করতে পারবে কিনা তা নির্ধারণ করে।

---

## 2. `has_permission()` এবং `has_object_permission()`-এর মধ্যে পার্থক্য কী?

| Method                    | Purpose                          |
| ------------------------- | -------------------------------- |
| `has_permission()`        | View-Level Access Check          |
| `has_object_permission()` | নির্দিষ্ট Object-এর Access Check |

---

## 3. Object-Level Permission কখন ব্যবহার করবেন?

**Answer:**

যখন User শুধুমাত্র নিজের Resource Access করতে পারবে।

যেমন:

* নিজের Course
* নিজের Exam
* নিজের Result
* নিজের Profile

---

## 4. `permission_classes`-এ একাধিক Permission দিলে কী হয়?

**Answer:**

সব Permission Sequentially Check হয়। যেকোনো একটি False হলে Request Reject হয়।

---

## 5. `get_permissions()` কেন Override করবেন?

**Answer:**

একই ViewSet-এর বিভিন্ন Action-এর জন্য ভিন্ন Permission প্রয়োগ করার জন্য।

---

# Homework

আপনার **Exam SaaS Project**-এর জন্য নিচের Permission Class-গুলো Implement করার চেষ্টা করুন:

```text
IsTeacher

IsStudent

IsAdmin

IsCourseOwner

IsExamOwner

IsEnrolledStudent

IsResultOwner
```

এবং প্রতিটির জন্য লিখুন:

* `has_permission()` লাগবে?
* `has_object_permission()` লাগবে?
* কোন API-তে ব্যবহার করবেন?

---

# 🎯 Lesson 12 (Advanced RBAC)

পরবর্তী Lesson-এ আমরা **Role-Based Access Control (RBAC)** শিখব।

সেখানে আলোচনা করব:

* Django Groups
* Django Permissions
* Custom Permissions
* Groups vs Role Field
* Permission Decorators
* Model Permissions
* Object Permissions
* Enterprise RBAC Design

এই Lesson শেষ হলে আপনি **Admin, Teacher, Student, Moderator, Manager**—যেকোনো Role-based System Professionalভাবে ডিজাইন করতে পারবেন।

------------
# Lesson 12: Django Groups & Permissions (Enterprise RBAC)

> **RBAC = Role-Based Access Control**
>
> এটি Enterprise Application-এর সবচেয়ে গুরুত্বপূর্ণ Security Model।

আগের Lesson-এ আমরা `role` Field ব্যবহার করেছি (`teacher`, `student`, `admin`)।

আজ শিখব Django-এর Built-in **Groups** এবং **Permissions** System, যা Enterprise Company-গুলো ব্যবহার করে।

---

# আজ আমরা কী শিখব?

* RBAC কী?
* Django Group কী?
* Django Permission কী?
* Default Model Permissions
* Custom Permissions
* Group vs Role Field
* User → Group → Permission Flow
* Exam SaaS RBAC Design
* Best Practices
* Interview Questions

---

# What is RBAC?

RBAC-এর মূল ধারণা:

```text
User

↓

Group (Role)

↓

Permissions

↓

Action
```

Example

```text
Atiar

↓

Teacher Group

↓

add_exam
change_exam
delete_exam

↓

Create Exam
```

---

# Authentication vs Authorization vs RBAC

| Authentication | Authorization  | RBAC                     |
| -------------- | -------------- | ------------------------ |
| User কে?       | কী করতে পারবে? | Role অনুযায়ী Permission |

---

# Django Security Architecture

```text
User

↓

Authentication

↓

Groups

↓

Permissions

↓

APIView
```

---

# Django Group

Group হলো

> **একটি Collection of Permissions**

Example

```text
Teacher Group

↓

add_exam

change_exam

view_exam
```

Student Group

```text
Student

↓

view_exam

take_exam
```

Admin

```text
Admin

↓

All Permissions
```

---

# Database Relationship

```text
User

↓

Many-to-Many

↓

Groups

↓

Many-to-Many

↓

Permissions
```

---

Diagram

```text
User
 │
 ├──────────────┐
 │              │
 ▼              ▼

Teacher      Moderator

 │              │

 ▼              ▼

Permissions  Permissions
```

---

# Django Automatically Creates Permissions

ধরুন Model

```python
class Exam(models.Model):

    title = models.CharField(max_length=100)
```

Migration-এর পরে Django Automatically তৈরি করবে

```text
add_exam

change_exam

delete_exam

view_exam
```

এগুলোকে বলে

**Model Permissions**

---

# Database

Permission Table

| Permission  |
| ----------- |
| add_exam    |
| change_exam |
| delete_exam |
| view_exam   |

---

# Group Creation

Admin Panel

```text
Admin

↓

Authentication

↓

Groups

↓

Add Group
```

Create

```text
Teacher
```

তারপর Permission Select করুন

```text
✓ add_exam

✓ change_exam

✓ view_exam
```

Save

---

# User Assign to Group

Admin Panel

```text
Users

↓

Atiar

↓

Groups

↓

Teacher
```

এখন Atiar-এর Role

```text
Teacher
```

---

# Permission Check

Python

```python
request.user.has_perm(
    "exam.add_exam"
)
```

Return

```python
True
```

অথবা

```python
False
```

---

# Flow

```text
User

↓

Teacher Group

↓

Has add_exam?

↓

Yes

↓

Allow
```

---

# Multiple Groups

একজন User

একাধিক Group-এ থাকতে পারে।

Example

```text
Atiar

↓

Teacher

Moderator
```

Permissions

```text
Teacher

+

Moderator

=

Combined Permissions
```

---

# Custom Permission

Model

```python
class Exam(models.Model):

    class Meta:

        permissions = [

            ("publish_exam",
             "Can Publish Exam"),

            ("archive_exam",
             "Can Archive Exam"),

        ]
```

Migration

↓

Permission Table

```text
publish_exam

archive_exam
```

---

# Permission Check

```python
request.user.has_perm(
    "exam.publish_exam"
)
```

---

# Custom Permission Class

```python
from rest_framework.permissions import BasePermission


class CanPublishExam(BasePermission):

    def has_permission(
        self,
        request,
        view
    ):

        return request.user.has_perm(
            "exam.publish_exam"
        )
```

View

```python
permission_classes = [
    CanPublishExam
]
```

---

# Group vs Role Field

আগের Lesson-এ

```python
role="teacher"
```

ব্যবহার করেছি।

এখন প্রশ্ন

**Role Field নাকি Group?**

---

## Option 1

Role Field

```python
role

↓

teacher
```

সহজ

Fast

---

## Option 2

Groups

```text
Teacher

↓

Permissions
```

Flexible

Enterprise

---

# Comparison

| Role Field       | Django Groups                       |
| ---------------- | ----------------------------------- |
| Simple           | Advanced                            |
| Fixed Roles      | Flexible Roles                      |
| Code Change লাগে | Admin Panel থেকেই পরিবর্তন করা যায় |
| Small Project    | Large Enterprise                    |

---

# Best Practice

Small Project

```text
Role Field
```

Medium Project

```text
Role

+

Groups
```

Enterprise

```text
Groups

+

Permissions
```

---

# Your Exam SaaS

আমি কী Recommend করবো?

```text
User

↓

Role Field

Teacher

Student

Admin

↓

+

Groups

↓

Permissions
```

---

Example

Teacher

Role

```text
teacher
```

Group

```text
Teacher
```

Permissions

```text
add_exam

change_exam

publish_exam
```

---

# Object-Level Permission

Teacher

```text
Can Edit

↓

Own Exam
```

Permission

↓

Group

↓

Object Check

---

Flow

```text
request.user

↓

Group

↓

Permission

↓

Object Owner

↓

Allow
```

---

# Complete Enterprise Flow

```text
Login

↓

JWT

↓

request.user

↓

Group

↓

Permission

↓

Object Permission

↓

APIView
```

---

# Exam SaaS RBAC

## Student Group

```text
view_course

join_course

take_exam

view_result
```

---

## Teacher Group

```text
create_course

add_exam

publish_exam

view_students
```

---

## Moderator Group

```text
approve_exam

archive_exam

manage_questions
```

---

## Admin Group

```text
All Permissions
```

---

# Folder Structure

```text
accounts/

    permissions.py

courses/

    permissions.py

exams/

    permissions.py

results/

    permissions.py

groups.py
```

---

# Real Company Example

```text
Employee

↓

Department

↓

Role

↓

Group

↓

Permissions

↓

Object Permission
```

---

# Common Mistakes

## ❌ শুধুমাত্র Role Field ব্যবহার

বড় Project-এ Permission Manage করা কঠিন হয়ে যায়।

---

## ❌ View-এর ভিতরে Permission Logic

```python
if request.user.role == "teacher":
```

এটি Permission Class-এ রাখুন।

---

## ❌ Hardcoded Permission

```python
if user.username == "admin":
```

কখনো করবেন না।

---

# Interview Questions

## 1. Django Group কী?

**Answer:**

Group হলো একাধিক Permission-এর Collection, যা এক বা একাধিক User-কে Assign করা যায়।

---

## 2. Django Automatically কোন Permission তৈরি করে?

**Answer:**

প্রত্যেক Model-এর জন্য সাধারণত:

```text
add

change

delete

view
```

Permission তৈরি হয়।

---

## 3. `has_perm()` কী করে?

**Answer:**

User-এর কাছে নির্দিষ্ট Permission আছে কিনা Check করে।

Example

```python
request.user.has_perm(
    "exam.change_exam"
)
```

---

## 4. Role Field নাকি Group—কোনটি ভালো?

**Answer:**

* ছোট Project → Role Field যথেষ্ট।
* বড় Enterprise Project → Django Groups + Permissions।
* Medium Project (যেমন আপনার Exam SaaS) → **Role Field + Groups + Custom Permissions** সবচেয়ে ভালো Design।

---

## 5. Custom Permission কখন ব্যবহার করবেন?

**Answer:**

যখন Default `add`, `change`, `delete`, `view` Permission যথেষ্ট নয়।

যেমন:

* `publish_exam`
* `approve_result`
* `archive_course`

---

# 🏗️ Recommended Architecture for Your Exam SaaS

```text
Authentication
      │
      ▼
JWTAuthentication
      │
      ▼
request.user
      │
      ▼
Role (Teacher/Student/Admin)
      │
      ▼
Group
      │
      ▼
Permission
      │
      ▼
Object Permission
      │
      ▼
APIView
```

---

# Homework

আপনার Project-এর জন্য নিচের Group Design করুন:

### Teacher

```text
add_course
change_course
add_exam
change_exam
publish_exam
```

### Student

```text
view_course
join_course
take_exam
view_result
```

### Admin

```text
All Permissions
```

তারপর লিখুন:

1. কোনগুলো Django-এর Default Permission?
2. কোনগুলো Custom Permission?
3. কোনগুলো `has_permission()` দিয়ে Check করবেন?
4. কোনগুলো `has_object_permission()` দিয়ে Check করবেন?

---

# 🎯 Lesson 13 (Next)

পরবর্তী Lesson হবে **Object-Level Permissions (Professional Level)**।

সেখানে আমরা শিখব:

* `has_object_permission()` Deep Dive
* Owner-based Security
* Multi-Tenant Security
* Teacher শুধুমাত্র নিজের Course/Edit করতে পারবে
* Student শুধুমাত্র নিজের Result দেখতে পারবে
* `check_object_permissions()` Internals
* ViewSet Object Permissions
* Real SaaS Security Design

এটি DRF-এর সবচেয়ে গুরুত্বপূর্ণ Security Topics-এর একটি এবং বড় SaaS Application-এ প্রায় সব জায়গায় ব্যবহৃত হয়।

--------
# Lesson 13: Object-Level Permissions (Professional DRF Security)

> **এই Lesson DRF-এর সবচেয়ে গুরুত্বপূর্ণ Security Topic-এর একটি।**
>
> Authentication বলে **"কে?"**
>
> Permission বলে **"কি করতে পারবে?"**
>
> **Object Permission বলে "কোন Object-এর উপর করতে পারবে?"**

---

# আজ আমরা কী শিখব?

* Object-Level Permission কী?
* `has_permission()` vs `has_object_permission()`
* Owner-Based Access Control
* Multi-Tenant Security
* `check_object_permissions()` Internals
* GenericAPIView Internals
* ViewSet Object Permissions
* Exam SaaS বাস্তব উদাহরণ
* Interview Questions

---

# Authentication → Permission → Object Permission

```text
Request
    │
    ▼
Authentication
    │
request.user
    │
    ▼
View Permission
    │
    ▼
Get Object
    │
    ▼
Object Permission
    │
    ▼
APIView
```

---

# Problem

ধরুন Database-এ দুইজন Teacher আছে।

## Exam Table

| ID | Exam   | Owner     |
| -- | ------ | --------- |
| 1  | Python | Teacher A |
| 2  | Django | Teacher B |

---

Teacher A Request

```http
PUT /api/exams/1/
```

Allowed

কারণ

```text
Owner
```

---

Teacher A

```http
PUT /api/exams/2/
```

Should be

```text
403 Forbidden
```

কারণ

Exam-এর Owner

```text
Teacher B
```

---

# View-Level Permission যথেষ্ট নয়

```python
permission_classes = [
    IsTeacher
]
```

এটি শুধু Check করবে

```text
Teacher?
```

কিন্তু

```text
Owner?
```

Check করবে না।

---

# Solution

Object Permission

---

# has_permission()

এটি View Level

```python
class IsTeacher(BasePermission):

    def has_permission(
        self,
        request,
        view
    ):
        return (
            request.user.is_authenticated
            and
            request.user.role=="teacher"
        )
```

Check করে

```text
Teacher?
```

---

# has_object_permission()

```python
class IsExamOwner(BasePermission):

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.teacher == request.user
```

---

Flow

```text
Request

↓

Get Exam Object

↓

Exam.teacher

↓

request.user

↓

Same?

↓

Allow
```

---

# Visual Example

Teacher A

```text
request.user

↓

Teacher A
```

Exam

```text
obj.teacher

↓

Teacher A
```

↓

True

↓

Allow

---

Teacher A

↓

Exam

↓

Teacher B

↓

False

↓

403 Forbidden

---

# Full Permission

```python
from rest_framework.permissions import BasePermission


class IsExamOwner(BasePermission):

    def has_permission(
        self,
        request,
        view
    ):
        return request.user.is_authenticated

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.teacher == request.user
```

---

# GenericAPIView Internals

Interview Question

Object Permission

Automatically

কীভাবে Call হয়?

---

DRF Internal Flow

```python
obj = self.get_object()

self.check_object_permissions(
    request,
    obj
)
```

---

Internally

```python
for permission in self.get_permissions():

    permission.has_object_permission(
        request,
        self,
        obj
    )
```

---

# get_object()

```python
obj = self.get_object()
```

Returns

```text
Exam Object
```

---

# check_object_permissions()

```python
self.check_object_permissions(
    request,
    obj
)
```

Calls

```python
has_object_permission()
```

---

# RetrieveUpdateAPIView

```python
class ExamUpdateAPIView(

    RetrieveUpdateAPIView

):

    queryset = Exam.objects.all()

    serializer_class = ExamSerializer

    permission_classes = [

        IsTeacher,

        IsExamOwner

    ]
```

---

Flow

```text
Request

↓

JWT

↓

Teacher?

↓

Get Object

↓

Owner?

↓

Update
```

---

# ViewSet

```python
class ExamViewSet(

    ModelViewSet

):

    permission_classes = [

        IsTeacher,

        IsExamOwner

    ]
```

DRF Automatically

```python
get_object()

↓

check_object_permissions()
```

---

# Custom APIView

APIView

Automatically করবে না।

নিজে Call করতে হবে।

```python
exam = Exam.objects.get(pk=pk)

self.check_object_permissions(

    request,

    exam
)
```

---

তারপর

```python
serializer.save()
```

---

# Multi-Tenant Security

এটি SaaS Interview-এ খুব Popular।

---

Company A

```text
Teacher A

Course A
```

Company B

```text
Teacher B

Course B
```

Teacher A

কখনো

```text
Course B
```

দেখতে পারবে না।

---

Permission

```python
return obj.organization == request.user.organization
```

---

# Exam SaaS

Teacher

```text
Own Course

↓

Own Exam

↓

Own Questions

↓

Own Students
```

---

Student

```text
Own Enrollments

↓

Own Results

↓

Own Certificates
```

---

# Result Permission

```python
class IsResultOwner(

    BasePermission

):

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.student == request.user
```

---

# Course Owner

```python
class IsCourseOwner(

    BasePermission

):

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.teacher == request.user
```

---

# Enrollment Permission

```python
class IsEnrollmentOwner(

    BasePermission

):

    def has_object_permission(

        self,

        request,

        view,

        obj

    ):

        return obj.student == request.user
```

---

# Multiple Object Permissions

```python
permission_classes = [

    IsTeacher,

    IsCourseOwner
]
```

Flow

```text
Teacher?

↓

Yes

↓

Course Owner?

↓

Yes

↓

Allow
```

---

# Complete Security Flow

```text
Login

↓

JWTAuthentication

↓

request.user

↓

View Permission

↓

Get Object

↓

Object Permission

↓

Serializer

↓

Database
```

---

# Object Permission Best Practice

সবসময়

```python
has_permission()
```

*

```python
has_object_permission()
```

একসাথে ব্যবহার করুন।

---

# Common Mistakes

## ❌ Mistake 1

```python
permission_classes = [

    IsTeacher
]
```

Owner Check নেই।

---

## ❌ Mistake 2

View-এর ভিতরে

```python
if exam.teacher != request.user:
```

Permission Class-এ লিখুন।

---

## ❌ Mistake 3

Queryset Filter না করা।

Bad

```python
Exam.objects.all()
```

Better

```python
Exam.objects.filter(
    teacher=request.user
)
```

> **Production Tip:** শুধু Object Permission-এর উপর নির্ভর না করে Queryset-ও Filter করুন। এতে অপ্রয়োজনীয় Object Database থেকে আসবে না এবং Security আরও শক্তিশালী হবে।

---

# Production Pattern

```python
class ExamViewSet(ModelViewSet):

    serializer_class = ExamSerializer
    permission_classes = [
        IsTeacher,
        IsExamOwner
    ]

    def get_queryset(self):
        return Exam.objects.filter(
            teacher=self.request.user
        )
```

এতে:

* অন্য Teacher-এর Exam Queryset-এ আসবেই না।
* Object Permission অতিরিক্ত Security Layer হিসেবে কাজ করবে।

---

# Real Exam SaaS Security

Teacher

```text
Create Course

↓

Own Courses

↓

Own Exams

↓

Own Questions
```

Student

```text
Enroll

↓

Own Exams

↓

Own Results

↓

Own Certificates
```

Admin

```text
Everything
```

---

# DRF Interview Questions

## 1. `has_permission()` এবং `has_object_permission()`-এর পার্থক্য কী?

| has_permission()       | has_object_permission() |
| ---------------------- | ----------------------- |
| View-Level             | Object-Level            |
| Object পাওয়ার আগে চলে | Object পাওয়ার পরে চলে  |

---

## 2. `check_object_permissions()` কী করে?

**Answer:**

এটি বর্তমান Object-এর জন্য সব Permission Class-এর `has_object_permission()` Method Call করে। কোনোটি `False` Return করলে `403 Forbidden` দেয়।

---

## 3. GenericAPIView কি Object Permission Automatically Check করে?

**Answer:**

হ্যাঁ। `get_object()` ব্যবহার করলে DRF নিজেই `check_object_permissions()` Call করে।

---

## 4. APIView-এ কি Object Permission Automatically Check হয়?

**Answer:**

না। APIView ব্যবহার করলে Developer-কে নিজে `self.check_object_permissions(request, obj)` Call করতে হয়।

---

## 5. Production-এ শুধু Object Permission যথেষ্ট?

**Answer:**

না। **দুটি Layer** ব্যবহার করা উচিত:

1. `get_queryset()` দিয়ে User-এর জন্য অনুমোদিত Object-গুলোই Query করুন।
2. `has_object_permission()` দিয়ে Object-Level Access Verify করুন।

---

# Homework

আপনার **Exam SaaS Project**-এর জন্য নিচের Permission Class-গুলো তৈরি করার চেষ্টা করুন:

```text
IsCourseOwner
IsExamOwner
IsQuestionOwner
IsEnrollmentOwner
IsResultOwner
```

তারপর প্রতিটির জন্য:

* `has_permission()`-এ কী Check করবেন?
* `has_object_permission()`-এ কোন Field Compare করবেন?
* `get_queryset()` কীভাবে Restrict করবেন?

---

# 🎯 Lesson 14 (Next)

পরবর্তী Lesson হবে **DRF Throttling (Rate Limiting)**।

আমরা শিখব:

* Request Throttling কী?
* `AnonRateThrottle`
* `UserRateThrottle`
* `ScopedRateThrottle`
* Custom Throttle Classes
* Login API Brute Force Protection
* OTP Rate Limiting
* Production API Security Strategy

এই Lesson-এর পর আপনি আপনার API-কে **Spam, Abuse এবং Brute Force Attack** থেকে সুরক্ষিত রাখতে পারবেন।

---------
# Lesson 14: DRF Throttling (Rate Limiting) - Production API Security

> **Throttling** হলো API-কে **Spam, Brute Force Attack, DDoS-এর ছোট আকারের Abuse, এবং Excessive Requests** থেকে রক্ষা করার একটি উপায়।

অনেক DRF Interview-এ প্রশ্ন আসে:

> **Authentication, Permission এবং Throttling-এর মধ্যে পার্থক্য কী?**

এই Lesson শেষে আপনি Production-Level API Rate Limiting Implement করতে পারবেন।

---

# আজ আমরা কী শিখব?

* Throttling কী?
* Authentication vs Permission vs Throttle
* Built-in Throttle Classes
* `AnonRateThrottle`
* `UserRateThrottle`
* `ScopedRateThrottle`
* Custom Throttle
* Login Rate Limiting
* OTP Rate Limiting
* Redis Cache vs Local Cache
* Production Best Practices
* Interview Questions

---

# DRF Request Lifecycle

```text
Incoming Request
      │
      ▼
Authentication
      │
      ▼
Permission
      │
      ▼
Throttle
      │
      ▼
APIView
      │
      ▼
Serializer
      │
      ▼
Database
      │
      ▼
Response
```

---

# Authentication vs Permission vs Throttle

| Authentication | Permission          | Throttle                  |
| -------------- | ------------------- | ------------------------- |
| User কে?       | User কী করতে পারবে? | কতবার Request করতে পারবে? |

Example

```text
Login

↓

Teacher

↓

Can Create Exam

↓

Only 100 Requests/hour
```

---

# What is Throttling?

ধরুন

একজন Hacker

```text
POST /login
```

এক সেকেন্ডে

```text
10,000 Requests
```

পাঠাচ্ছে।

Server

```text
CPU ↑

Database ↑

Memory ↑

Server Crash
```

---

Throttling

```text
Only

10 Requests/minute

Allowed
```

---

# Built-in Throttle Classes

DRF-এ তিনটি প্রধান Built-in Throttle আছে।

| Class                | Purpose                |
| -------------------- | ---------------------- |
| `AnonRateThrottle`   | Anonymous User         |
| `UserRateThrottle`   | Logged-in User         |
| `ScopedRateThrottle` | Different Rate per API |

---

# 1. AnonRateThrottle

Anonymous User-এর জন্য।

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_THROTTLE_CLASSES": [

        "rest_framework.throttling.AnonRateThrottle",

    ],

    "DEFAULT_THROTTLE_RATES": {

        "anon": "100/day",

    },

}
```

---

Meaning

```text
Anonymous User

↓

100 Requests

↓

Per Day
```

101st Request

↓

```http
429 Too Many Requests
```

---

# 2. UserRateThrottle

Authenticated User-এর জন্য।

```python
REST_FRAMEWORK = {

    "DEFAULT_THROTTLE_CLASSES":[

        "rest_framework.throttling.UserRateThrottle",

    ],

    "DEFAULT_THROTTLE_RATES":{

        "user":"1000/day"

    }

}
```

---

Flow

```text
Login

↓

JWT

↓

User

↓

1000 Requests/day
```

---

# Multiple Throttles

```python
REST_FRAMEWORK = {

    "DEFAULT_THROTTLE_CLASSES":[

        "rest_framework.throttling.AnonRateThrottle",

        "rest_framework.throttling.UserRateThrottle",

    ],

    "DEFAULT_THROTTLE_RATES":{

        "anon":"100/day",

        "user":"1000/day",

    }

}
```

---

# 3. ScopedRateThrottle

সব API-এর Rate এক রকম হবে না।

Example

| API         | Rate      |
| ----------- | --------- |
| Login       | 5/min     |
| Register    | 3/hour    |
| Search      | 200/min   |
| Course List | 1000/hour |

---

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_THROTTLE_CLASSES":[

        "rest_framework.throttling.ScopedRateThrottle",

    ],

    "DEFAULT_THROTTLE_RATES":{

        "login":"5/min",

        "register":"3/hour",

        "search":"100/min",

    }

}
```

---

View

```python
from rest_framework.views import APIView

class LoginAPIView(APIView):

    throttle_scope = "login"
```

---

Flow

```text
Request

↓

Login API

↓

Throttle Scope

↓

login

↓

5/min
```

---

# Per View Throttle

```python
from rest_framework.throttling import UserRateThrottle

class CourseAPIView(APIView):

    throttle_classes = [

        UserRateThrottle

    ]
```

---

# Custom Throttle

ধরুন

Teacher

```text
1000/day
```

Student

```text
500/day
```

---

```python
from rest_framework.throttling import UserRateThrottle

class TeacherThrottle(UserRateThrottle):

    scope = "teacher"
```

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_THROTTLE_RATES":{

        "teacher":"1000/day"

    }

}
```

---

# Login Protection

Production Login API

```text
5 Attempts

↓

1 Minute

↓

Blocked
```

Example

```python
class LoginAPIView(APIView):

    throttle_scope = "login"
```

settings.py

```python
DEFAULT_THROTTLE_RATES = {

    "login":"5/min"

}
```

---

# OTP API

OTP পাঠানো খুব Sensitive।

```text
POST

/send-otp/
```

Rate

```text
3/min
```

তারপর

```text
429 Too Many Requests
```

---

# Password Reset API

```text
2/hour
```

---

# Search API

```text
500/min
```

---

# AI Chat API

Expensive API

```text
20/hour
```

---

# Response

Limit Cross করলে

```http
HTTP 429 Too Many Requests
```

Body

```json
{
    "detail":"Request was throttled. Expected available in 58 seconds."
}
```

---

# Internally

DRF

```python
allow_request()

↓

History

↓

Count

↓

Limit?

↓

Allow

or

Reject
```

---

# Cache

Throttle Database-এ Store হয় না।

এটি Cache-এ Store হয়।

Default

```text
Local Memory Cache
```

Production

```text
Redis
```

---

# Redis Example

```python
CACHES = {

    "default": {

        "BACKEND":"django_redis.cache.RedisCache",

        "LOCATION":"redis://127.0.0.1:6379/1",

    }

}
```

Redis Fast হওয়ায় Throttling Production-এ কার্যকরভাবে কাজ করে।

---

# Your Exam SaaS Throttle Design

| API             | Rate    |
| --------------- | ------- |
| Login           | 5/min   |
| Register        | 3/hour  |
| Forgot Password | 2/hour  |
| OTP             | 3/min   |
| Join Course     | 20/min  |
| Submit Exam     | 5/min   |
| Search          | 100/min |
| AI Assistant    | 20/hour |

---

# Security Strategy

```text
Authentication

↓

Permission

↓

Throttle

↓

Business Logic
```

---

# Common Mistakes

## ❌ Login-এ Throttle না দেওয়া

Brute Force Attack সহজ হয়ে যায়।

---

## ❌ OTP Unlimited

একজন User

```text
1000 OTP
```

পাঠাতে পারে।

---

## ❌ Password Reset Unlimited

Email Spam শুরু হবে।

---

## ❌ Production-এ Local Cache

Multiple Server থাকলে Counter Sync হবে না।

Use

```text
Redis
```

---

# Production Best Practices

✅ Login → `5/min`

✅ Register → `3/hour`

✅ Password Reset → `2/hour`

✅ OTP → `3/min`

✅ AI API → `20/hour`

✅ Redis Cache ব্যবহার করুন

---

# Interview Questions

## 1. Throttling কী?

**Answer:**

একটি নির্দিষ্ট সময়ে একজন User বা IP কতগুলো Request করতে পারবে তা নিয়ন্ত্রণ করার ব্যবস্থা।

---

## 2. `AnonRateThrottle` এবং `UserRateThrottle`-এর পার্থক্য কী?

| AnonRateThrottle               | UserRateThrottle                       |
| ------------------------------ | -------------------------------------- |
| Anonymous User-এর জন্য         | Logged-in User-এর জন্য                 |
| IP Address-এর ভিত্তিতে কাজ করে | Authenticated User-এর ভিত্তিতে কাজ করে |

---

## 3. `ScopedRateThrottle` কখন ব্যবহার করবেন?

**Answer:**

যখন বিভিন্ন API-এর জন্য ভিন্ন Rate Limit দরকার।

যেমন:

* Login → `5/min`
* Search → `100/min`
* AI Chat → `20/hour`

---

## 4. Throttle Data কোথায় Store হয়?

**Answer:**

Cache Backend-এ। Development-এ Local Memory Cache, Production-এ সাধারণত Redis।

---

## 5. HTTP Status Code কী Return করে?

**Answer:**

```http
429 Too Many Requests
```

---

# Homework

আপনার **Exam SaaS Project**-এর জন্য একটি Throttling Plan তৈরি করুন:

| API             | Suggested Rate |
| --------------- | -------------- |
| Login           | ?              |
| Register        | ?              |
| Send OTP        | ?              |
| Forgot Password | ?              |
| Create Course   | ?              |
| Submit Exam     | ?              |
| Search Courses  | ?              |
| AI Assistant    | ?              |

তারপর:

1. কোন API-তে `ScopedRateThrottle` ব্যবহার করবেন?
2. কোন API-তে `UserRateThrottle` যথেষ্ট?
3. Production-এ কোন Cache Backend ব্যবহার করবেন এবং কেন?

---

# 🎯 Lesson 15 (Next)

পরবর্তী Lesson হবে **Production API Security**।

আমরা শিখব:

* CORS
* CSRF
* XSS
* SQL Injection
* Clickjacking
* HTTPS
* Secure Cookies
* Security Headers
* Django Security Middleware
* API Security Checklist
* OWASP Top 10-এর সাথে Django Security

এই Lesson শেষ হলে আপনি একটি **Production-Ready Secure Django REST API** তৈরি করতে পারবেন।

--------
# Lesson 15: Production API Security (DRF + Django Security)

> **এই Lesson DRF-এর সবচেয়ে গুরুত্বপূর্ণ Security Lesson।**

Production-এ শুধু Authentication করলেই Security শেষ হয় না।

আপনাকে API-কে **CORS, CSRF, XSS, SQL Injection, Clickjacking, HTTPS, Security Headers, Cookie Security, Secret Management** থেকেও সুরক্ষিত রাখতে হবে।

---

# আজ আমরা কী শিখব?

* OWASP Top 10 পরিচিতি
* CORS
* CSRF
* XSS
* SQL Injection
* Clickjacking
* HTTPS
* Secure Cookies
* Security Headers
* Django Security Middleware
* Environment Variables
* API Security Checklist
* Interview Questions

---

# Security Layers

```text
Internet
     │
     ▼
HTTPS
     │
     ▼
Nginx
     │
     ▼
Gunicorn
     │
     ▼
Django
     │
     ▼
Authentication
     │
     ▼
Permission
     │
     ▼
Throttle
     │
     ▼
Business Logic
     │
     ▼
Database
```

---

# OWASP Top 10

সব Web Developer-এর জানা উচিত।

সবগুলো মুখস্থ করার দরকার নেই, কিন্তু এগুলো কী সেটা জানতে হবে।

| Threat                    | Description                 |
| ------------------------- | --------------------------- |
| Broken Access Control     | Unauthorized Access         |
| Cryptographic Failures    | Weak Encryption             |
| Injection                 | SQL Injection               |
| Security Misconfiguration | Wrong Settings              |
| Vulnerable Components     | Old Packages                |
| Authentication Failure    | Weak Login                  |
| Software Integrity        | Unsafe Updates              |
| Logging Failure           | No Audit                    |
| SSRF                      | Server-side Request Forgery |

---

# 1. CORS (Cross-Origin Resource Sharing)

ধরুন

Frontend

```text
http://localhost:5173
```

Backend

```text
http://127.0.0.1:8000
```

Browser বলবে

```text
Different Origin
```

Request Block হবে।

---

## Solution

Install

```bash
pip install django-cors-headers
```

---

settings.py

```python
INSTALLED_APPS = [

    ...

    "corsheaders",

]
```

---

Middleware

```python
MIDDLEWARE = [

    "corsheaders.middleware.CorsMiddleware",

    ...

]
```

---

Allow React

```python
CORS_ALLOWED_ORIGINS = [

    "http://localhost:5173",

]
```

---

Production

```python
CORS_ALLOWED_ORIGINS = [

    "https://exam.example.com",

]
```

❌ কখনো করবেন না

```python
CORS_ALLOW_ALL_ORIGINS = True
```

Production-এ।

---

# Flow

```text
React

↓

Browser

↓

Origin Check

↓

Allowed?

↓

API
```

---

# 2. CSRF

CSRF

মানে

অন্য Website

আপনার Website-এর নামে Request পাঠাচ্ছে।

---

Example

User

```text
Logged In
```

↓

Fake Website

↓

```html
<form action="/delete-account/">
```

↓

Browser Automatically Cookie পাঠিয়ে দেয়।

---

## Solution

Django

Automatically

```text
CSRF Token
```

ব্যবহার করে।

---

API

JWT Header ব্যবহার করলে

CSRF Risk অনেক কমে।

কিন্তু

Cookie Authentication হলে

CSRF Protection লাগবে।

---

# CSRF Settings

```python
CSRF_TRUSTED_ORIGINS = [

    "https://exam.example.com",

]
```

---

# 3. XSS (Cross Site Scripting)

Bad User

Comment

```html
<script>

alert("Hacked")

</script>
```

যদি Render হয়

↓

JavaScript Execute হবে।

---

## Django Protection

Django Template

Automatically

Escape করে।

Example

```django
{{ comment }}
```

Output

```html
&lt;script&gt;
```

---

Bad

```django
{{ comment|safe }}
```

❌ User Input-এর উপর `safe` ব্যবহার করবেন না।

---

# React

React-ও Defaultভাবে Escape করে।

Dangerous

```jsx
dangerouslySetInnerHTML
```

এটি খুব সতর্কতার সাথে ব্যবহার করতে হবে।

---

# 4. SQL Injection

Bad Code

```python
cursor.execute(

f"SELECT * FROM users WHERE id={id}"

)
```

Attacker

```sql
1 OR 1=1
```

↓

সব Data Return।

---

Good

Django ORM

```python
User.objects.get(id=id)
```

ORM Parameterized Query ব্যবহার করে।

---

Raw SQL লাগলে

```python
cursor.execute(

"SELECT * FROM users WHERE id=%s",

[user_id]

)
```

---

# 5. Clickjacking

Attacker

আপনার Website

Invisible Frame-এ Load করে।

User

না জেনেই

Button Click করে।

---

Django

Default

```python
X_FRAME_OPTIONS = "DENY"
```

---

# 6. HTTPS

Development

```text
http://
```

Production

```text
https://
```

Always HTTPS।

---

Settings

```python
SECURE_SSL_REDIRECT = True
```

---

# 7. Secure Cookies

Cookie

```python
SESSION_COOKIE_SECURE = True

CSRF_COOKIE_SECURE = True
```

মানে

HTTPS ছাড়া Cookie যাবে না।

---

HttpOnly

```python
SESSION_COOKIE_HTTPONLY = True
```

JavaScript

Cookie পড়তে পারবে না।

---

SameSite

```python
SESSION_COOKIE_SAMESITE = "Lax"
```

Options

```text
Lax

Strict

None
```

---

# 8. Security Headers

Settings

```python
SECURE_CONTENT_TYPE_NOSNIFF = True

SECURE_BROWSER_XSS_FILTER = True

X_FRAME_OPTIONS = "DENY"
```

> **Note:** `SECURE_BROWSER_XSS_FILTER` আধুনিক Browser-এ Deprecated। আজকাল ভালো Practice হলো **Content Security Policy (CSP)** ব্যবহার করা।

---

# Content Security Policy (CSP)

Install

```bash
pip install django-csp
```

Example

```python
INSTALLED_APPS = [
    ...
    "csp",
]

MIDDLEWARE = [
    "csp.middleware.CSPMiddleware",
    ...
]

CSP_DEFAULT_SRC = ("'self'",)
CSP_SCRIPT_SRC = ("'self'",)
```

CSP Browser-কে বলে দেয় কোন Source থেকে Script, Style, Image Load করা যাবে।

---

# 9. Secret Key

❌ Wrong

```python
SECRET_KEY = "abc123"
```

GitHub-এ Upload।

---

Correct

`.env`

```text
SECRET_KEY=xxxxx
```

settings.py

```python
from decouple import config

SECRET_KEY = config("SECRET_KEY")
```

---

# 10. DEBUG

Development

```python
DEBUG = True
```

Production

```python
DEBUG = False
```

না হলে Error Page-এ Sensitive Information দেখা যেতে পারে।

---

# ALLOWED_HOSTS

Development

```python
ALLOWED_HOSTS = []
```

Production

```python
ALLOWED_HOSTS = [

    "api.exam.com"

]
```

---

# Password Validation

```python
AUTH_PASSWORD_VALIDATORS = [

    ...

]
```

Never Remove।

---

# Logging

Production

সব Login

সব Error

সব Security Event

Log করুন।

---

# File Upload Security

Bad

সব File Accept।

Good

```python
ALLOWED_IMAGE_TYPES

MAX_UPLOAD_SIZE
```

Check করুন।

---

# JWT Security

Access Token

```text
5-15 Minutes
```

Refresh

```text
7 Days
```

Rotate

```python
ROTATE_REFRESH_TOKENS=True
```

Blacklist

```python
BLACKLIST_AFTER_ROTATION=True
```

---

# Production Security Flow

```text
HTTPS

↓

CORS

↓

CSRF

↓

JWT

↓

Permission

↓

Throttle

↓

Validation

↓

ORM

↓

Database
```

---

# Production Security Checklist

## Authentication

* ✅ JWT
* ✅ Refresh Rotation
* ✅ Blacklist

---

## API

* ✅ CORS
* ✅ Throttle
* ✅ Permission

---

## Cookies

* ✅ Secure
* ✅ HttpOnly
* ✅ SameSite

---

## Django

* ✅ DEBUG=False
* ✅ ALLOWED_HOSTS
* ✅ HTTPS

---

## Database

* ✅ ORM
* ✅ No Raw SQL

---

## Secrets

* ✅ .env
* ✅ Never Push Keys

---

## Logging

* ✅ Errors
* ✅ Login
* ✅ Security Events

---

# Your Exam SaaS Security Design

```text
React

↓

HTTPS

↓

JWT

↓

Access Token

↓

Refresh Cookie

↓

Django

↓

Permission

↓

Object Permission

↓

Throttle

↓

ORM

↓

PostgreSQL
```

---

# Common Mistakes

## ❌ DEBUG=True in Production

Security Risk।

---

## ❌ CORS_ALLOW_ALL_ORIGINS=True

সব Website API Call করতে পারবে।

---

## ❌ Raw SQL

SQL Injection Risk।

---

## ❌ Store JWT in LocalStorage without considering XSS

Production-এ Refresh Token সাধারণত **HttpOnly Cookie**-তে রাখা হয়।

---

## ❌ Commit `.env`

GitHub-এ Secret Upload হয়ে যাবে।

---

# Interview Questions

## 1. CORS কী?

**Answer:**

Browser-এর Same-Origin Policy অনুযায়ী Cross-Origin Request নিয়ন্ত্রণ করার Mechanism।

---

## 2. CSRF এবং XSS-এর পার্থক্য কী?

| CSRF                                            | XSS                                    |
| ----------------------------------------------- | -------------------------------------- |
| User-এর Browser দিয়ে Unauthorized Request      | Website-এ Malicious Script Execute     |
| Cookie-based Authentication-এ বেশি গুরুত্বপূর্ণ | User Input Properly Escape না করলে হয় |

---

## 3. SQL Injection কীভাবে Prevent করবেন?

**Answer:**

* Django ORM ব্যবহার করে।
* Raw SQL হলে Parameterized Query ব্যবহার করে।

---

## 4. Production-এ `DEBUG` কেন `False`?

**Answer:**

কারণ `DEBUG=True` হলে Error Page-এ Sensitive Information (Settings, Paths, Environment) প্রকাশ হতে পারে।

---

## 5. JWT-এর সাথে CSRF লাগে?

**Answer:**

* **Authorization Header (`Bearer Token`)** ব্যবহার করলে সাধারণত CSRF Protection প্রয়োজন হয় না।
* **Cookie-based JWT Authentication** ব্যবহার করলে CSRF Protection অবশ্যই Configure করতে হবে।

---

# 🎯 Lesson 16 (Next)

এখন Authentication-এর Backend অংশ প্রায় শেষ।

পরবর্তী Lesson হবে:

# **React + Django Authentication (Production)**

আমরা শিখব:

* React Login Flow
* Axios Configuration
* Axios Interceptors
* Auto Refresh Token
* Protected Routes
* Private Routes
* Logout Flow
* Token Expiration Handling
* Refresh Queue
* React Authentication Architecture

এটি Full Stack Developer Interview এবং Production Project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
# Lesson 15: Production API Security (DRF + Django Security)

> **এই Lesson DRF-এর সবচেয়ে গুরুত্বপূর্ণ Security Lesson।**

Production-এ শুধু Authentication করলেই Security শেষ হয় না।

আপনাকে API-কে **CORS, CSRF, XSS, SQL Injection, Clickjacking, HTTPS, Security Headers, Cookie Security, Secret Management** থেকেও সুরক্ষিত রাখতে হবে।

---

# আজ আমরা কী শিখব?

* OWASP Top 10 পরিচিতি
* CORS
* CSRF
* XSS
* SQL Injection
* Clickjacking
* HTTPS
* Secure Cookies
* Security Headers
* Django Security Middleware
* Environment Variables
* API Security Checklist
* Interview Questions

---

# Security Layers

```text
Internet
     │
     ▼
HTTPS
     │
     ▼
Nginx
     │
     ▼
Gunicorn
     │
     ▼
Django
     │
     ▼
Authentication
     │
     ▼
Permission
     │
     ▼
Throttle
     │
     ▼
Business Logic
     │
     ▼
Database
```

---

# OWASP Top 10

সব Web Developer-এর জানা উচিত।

সবগুলো মুখস্থ করার দরকার নেই, কিন্তু এগুলো কী সেটা জানতে হবে।

| Threat                    | Description                 |
| ------------------------- | --------------------------- |
| Broken Access Control     | Unauthorized Access         |
| Cryptographic Failures    | Weak Encryption             |
| Injection                 | SQL Injection               |
| Security Misconfiguration | Wrong Settings              |
| Vulnerable Components     | Old Packages                |
| Authentication Failure    | Weak Login                  |
| Software Integrity        | Unsafe Updates              |
| Logging Failure           | No Audit                    |
| SSRF                      | Server-side Request Forgery |

---

# 1. CORS (Cross-Origin Resource Sharing)

ধরুন

Frontend

```text
http://localhost:5173
```

Backend

```text
http://127.0.0.1:8000
```

Browser বলবে

```text
Different Origin
```

Request Block হবে।

---

## Solution

Install

```bash
pip install django-cors-headers
```

---

settings.py

```python
INSTALLED_APPS = [

    ...

    "corsheaders",

]
```

---

Middleware

```python
MIDDLEWARE = [

    "corsheaders.middleware.CorsMiddleware",

    ...

]
```

---

Allow React

```python
CORS_ALLOWED_ORIGINS = [

    "http://localhost:5173",

]
```

---

Production

```python
CORS_ALLOWED_ORIGINS = [

    "https://exam.example.com",

]
```

❌ কখনো করবেন না

```python
CORS_ALLOW_ALL_ORIGINS = True
```

Production-এ।

---

# Flow

```text
React

↓

Browser

↓

Origin Check

↓

Allowed?

↓

API
```

---

# 2. CSRF

CSRF

মানে

অন্য Website

আপনার Website-এর নামে Request পাঠাচ্ছে।

---

Example

User

```text
Logged In
```

↓

Fake Website

↓

```html
<form action="/delete-account/">
```

↓

Browser Automatically Cookie পাঠিয়ে দেয়।

---

## Solution

Django

Automatically

```text
CSRF Token
```

ব্যবহার করে।

---

API

JWT Header ব্যবহার করলে

CSRF Risk অনেক কমে।

কিন্তু

Cookie Authentication হলে

CSRF Protection লাগবে।

---

# CSRF Settings

```python
CSRF_TRUSTED_ORIGINS = [

    "https://exam.example.com",

]
```

---

# 3. XSS (Cross Site Scripting)

Bad User

Comment

```html
<script>

alert("Hacked")

</script>
```

যদি Render হয়

↓

JavaScript Execute হবে।

---

## Django Protection

Django Template

Automatically

Escape করে।

Example

```django
{{ comment }}
```

Output

```html
&lt;script&gt;
```

---

Bad

```django
{{ comment|safe }}
```

❌ User Input-এর উপর `safe` ব্যবহার করবেন না।

---

# React

React-ও Defaultভাবে Escape করে।

Dangerous

```jsx
dangerouslySetInnerHTML
```

এটি খুব সতর্কতার সাথে ব্যবহার করতে হবে।

---

# 4. SQL Injection

Bad Code

```python
cursor.execute(

f"SELECT * FROM users WHERE id={id}"

)
```

Attacker

```sql
1 OR 1=1
```

↓

সব Data Return।

---

Good

Django ORM

```python
User.objects.get(id=id)
```

ORM Parameterized Query ব্যবহার করে।

---

Raw SQL লাগলে

```python
cursor.execute(

"SELECT * FROM users WHERE id=%s",

[user_id]

)
```

---

# 5. Clickjacking

Attacker

আপনার Website

Invisible Frame-এ Load করে।

User

না জেনেই

Button Click করে।

---

Django

Default

```python
X_FRAME_OPTIONS = "DENY"
```

---

# 6. HTTPS

Development

```text
http://
```

Production

```text
https://
```

Always HTTPS।

---

Settings

```python
SECURE_SSL_REDIRECT = True
```

---

# 7. Secure Cookies

Cookie

```python
SESSION_COOKIE_SECURE = True

CSRF_COOKIE_SECURE = True
```

মানে

HTTPS ছাড়া Cookie যাবে না।

---

HttpOnly

```python
SESSION_COOKIE_HTTPONLY = True
```

JavaScript

Cookie পড়তে পারবে না।

---

SameSite

```python
SESSION_COOKIE_SAMESITE = "Lax"
```

Options

```text
Lax

Strict

None
```

---

# 8. Security Headers

Settings

```python
SECURE_CONTENT_TYPE_NOSNIFF = True

SECURE_BROWSER_XSS_FILTER = True

X_FRAME_OPTIONS = "DENY"
```

> **Note:** `SECURE_BROWSER_XSS_FILTER` আধুনিক Browser-এ Deprecated। আজকাল ভালো Practice হলো **Content Security Policy (CSP)** ব্যবহার করা।

---

# Content Security Policy (CSP)

Install

```bash
pip install django-csp
```

Example

```python
INSTALLED_APPS = [
    ...
    "csp",
]

MIDDLEWARE = [
    "csp.middleware.CSPMiddleware",
    ...
]

CSP_DEFAULT_SRC = ("'self'",)
CSP_SCRIPT_SRC = ("'self'",)
```

CSP Browser-কে বলে দেয় কোন Source থেকে Script, Style, Image Load করা যাবে।

---

# 9. Secret Key

❌ Wrong

```python
SECRET_KEY = "abc123"
```

GitHub-এ Upload।

---

Correct

`.env`

```text
SECRET_KEY=xxxxx
```

settings.py

```python
from decouple import config

SECRET_KEY = config("SECRET_KEY")
```

---

# 10. DEBUG

Development

```python
DEBUG = True
```

Production

```python
DEBUG = False
```

না হলে Error Page-এ Sensitive Information দেখা যেতে পারে।

---

# ALLOWED_HOSTS

Development

```python
ALLOWED_HOSTS = []
```

Production

```python
ALLOWED_HOSTS = [

    "api.exam.com"

]
```

---

# Password Validation

```python
AUTH_PASSWORD_VALIDATORS = [

    ...

]
```

Never Remove।

---

# Logging

Production

সব Login

সব Error

সব Security Event

Log করুন।

---

# File Upload Security

Bad

সব File Accept।

Good

```python
ALLOWED_IMAGE_TYPES

MAX_UPLOAD_SIZE
```

Check করুন।

---

# JWT Security

Access Token

```text
5-15 Minutes
```

Refresh

```text
7 Days
```

Rotate

```python
ROTATE_REFRESH_TOKENS=True
```

Blacklist

```python
BLACKLIST_AFTER_ROTATION=True
```

---

# Production Security Flow

```text
HTTPS

↓

CORS

↓

CSRF

↓

JWT

↓

Permission

↓

Throttle

↓

Validation

↓

ORM

↓

Database
```

---

# Production Security Checklist

## Authentication

* ✅ JWT
* ✅ Refresh Rotation
* ✅ Blacklist

---

## API

* ✅ CORS
* ✅ Throttle
* ✅ Permission

---

## Cookies

* ✅ Secure
* ✅ HttpOnly
* ✅ SameSite

---

## Django

* ✅ DEBUG=False
* ✅ ALLOWED_HOSTS
* ✅ HTTPS

---

## Database

* ✅ ORM
* ✅ No Raw SQL

---

## Secrets

* ✅ .env
* ✅ Never Push Keys

---

## Logging

* ✅ Errors
* ✅ Login
* ✅ Security Events

---

# Your Exam SaaS Security Design

```text
React

↓

HTTPS

↓

JWT

↓

Access Token

↓

Refresh Cookie

↓

Django

↓

Permission

↓

Object Permission

↓

Throttle

↓

ORM

↓

PostgreSQL
```

---

# Common Mistakes

## ❌ DEBUG=True in Production

Security Risk।

---

## ❌ CORS_ALLOW_ALL_ORIGINS=True

সব Website API Call করতে পারবে।

---

## ❌ Raw SQL

SQL Injection Risk।

---

## ❌ Store JWT in LocalStorage without considering XSS

Production-এ Refresh Token সাধারণত **HttpOnly Cookie**-তে রাখা হয়।

---

## ❌ Commit `.env`

GitHub-এ Secret Upload হয়ে যাবে।

---

# Interview Questions

## 1. CORS কী?

**Answer:**

Browser-এর Same-Origin Policy অনুযায়ী Cross-Origin Request নিয়ন্ত্রণ করার Mechanism।

---

## 2. CSRF এবং XSS-এর পার্থক্য কী?

| CSRF                                            | XSS                                    |
| ----------------------------------------------- | -------------------------------------- |
| User-এর Browser দিয়ে Unauthorized Request      | Website-এ Malicious Script Execute     |
| Cookie-based Authentication-এ বেশি গুরুত্বপূর্ণ | User Input Properly Escape না করলে হয় |

---

## 3. SQL Injection কীভাবে Prevent করবেন?

**Answer:**

* Django ORM ব্যবহার করে।
* Raw SQL হলে Parameterized Query ব্যবহার করে।

---

## 4. Production-এ `DEBUG` কেন `False`?

**Answer:**

কারণ `DEBUG=True` হলে Error Page-এ Sensitive Information (Settings, Paths, Environment) প্রকাশ হতে পারে।

---

## 5. JWT-এর সাথে CSRF লাগে?

**Answer:**

* **Authorization Header (`Bearer Token`)** ব্যবহার করলে সাধারণত CSRF Protection প্রয়োজন হয় না।
* **Cookie-based JWT Authentication** ব্যবহার করলে CSRF Protection অবশ্যই Configure করতে হবে।

---

# 🎯 Lesson 16 (Next)

এখন Authentication-এর Backend অংশ প্রায় শেষ।

পরবর্তী Lesson হবে:

# **React + Django Authentication (Production)**

আমরা শিখব:

* React Login Flow
* Axios Configuration
* Axios Interceptors
* Auto Refresh Token
* Protected Routes
* Private Routes
* Logout Flow
* Token Expiration Handling
* Refresh Queue
* React Authentication Architecture

এটি Full Stack Developer Interview এবং Production Project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।


------------
# Lesson 16: React + Django Authentication (Production-Level)

> এটি **React + Django Full Stack Development-এর সবচেয়ে গুরুত্বপূর্ণ Lesson**।

আপনি যেহেতু **Django REST Framework Backend + React Frontend** দিয়ে **Exam SaaS** তৈরি করতে চান, এই Authentication Flow-টি আপনাকে অবশ্যই ভালোভাবে বুঝতে হবে।

---

# আজ আমরা কী শিখব?

* Complete Authentication Architecture
* React Login Flow
* Token Storage Strategy
* Axios Configuration
* Axios Interceptors
* Auto Refresh Token
* Protected Routes
* Logout Flow
* Token Expiration Handling
* Refresh Queue
* Best Practices
* Interview Questions

---

# Complete Authentication Flow

```text
                User

                 │

                 ▼

          Login Form (React)

                 │

                 ▼

          POST /auth/login/

                 │

                 ▼

      Django (dj-rest-auth)

                 │

                 ▼

 Access Token + Refresh Token

                 │

        ┌────────┴─────────┐
        ▼                  ▼

Access Token        Refresh Token
(Memory)            (HttpOnly Cookie)

        │
        ▼

API Requests

        │
        ▼

401 Unauthorized

        │
        ▼

Refresh Token API

        │
        ▼

New Access Token

        │
        ▼

Retry Original Request

        │
        ▼

Success
```

---

# Authentication Architecture

```text
React

↓

Login Page

↓

Axios

↓

Django REST API

↓

JWT

↓

Protected APIs

↓

Auto Refresh

↓

Logout
```

---

# Step 1: User Login

User

```text
Email

Password
```

↓

React

```http
POST /auth/login/
```

Body

```json
{
    "email":"teacher@gmail.com",

    "password":"12345678"
}
```

---

# Django Response

```json
{
    "access":"eyJ....",

    "refresh":"eyJ....",

    "user":{

        "id":1,

        "name":"Atiar",

        "role":"teacher"

    }
}
```

---

# Step 2: Store Tokens

## Development

অনেক Tutorial

```text
LocalStorage
```

ব্যবহার করে।

Example

```javascript
localStorage.setItem(
    "access",
    token
)
```

---

## Production

Recommended

```text
Access Token

↓

Memory

-----------------

Refresh Token

↓

HttpOnly Cookie
```

### কেন?

| Storage         | সুবিধা                         | অসুবিধা                            |
| --------------- | ------------------------------ | ---------------------------------- |
| LocalStorage    | সহজ                            | XSS Attack হলে Token চুরি হতে পারে |
| Memory          | Browser Refresh-এ Clear হয়    | বেশি নিরাপদ                        |
| HttpOnly Cookie | JavaScript Access করতে পারে না | CSRF Config ঠিক রাখতে হবে          |

---

# Step 3: Axios Instance

সব API Call-এর জন্য একটি Common Axios Instance তৈরি করুন।

```text
api.js

↓

Axios Instance

↓

Base URL

↓

Headers

↓

Interceptors
```

---

Example

```javascript
const api = axios.create({

    baseURL:"http://localhost:8000/api"

})
```

---

# Step 4: Request Interceptor

প্রতিটি Request-এর আগে

```text
Access Token
```

Header-এ যোগ হবে।

```text
Request

↓

Access Token

↓

Authorization Header

↓

API
```

Header

```http
Authorization: Bearer eyJ...
```

---

# Step 5: Protected API

Example

```http
GET /api/profile/
```

↓

Header

```http
Authorization: Bearer eyJ...
```

↓

Django

↓

JWTAuthentication

↓

request.user

↓

Profile

---

# Step 6: Access Token Expired

ধরুন

```text
Access Token

↓

Expired
```

↓

API

```http
401 Unauthorized
```

---

# Solution

```text
Axios Response Interceptor

↓

401?

↓

Refresh Token

↓

New Access Token

↓

Retry Request
```

---

# Auto Refresh Flow

```text
API Request

↓

401

↓

Refresh API

↓

New Access Token

↓

Retry Previous Request

↓

Success
```

---

# Refresh API

```http
POST /auth/token/refresh/
```

Body

```json
{
    "refresh":"xxxxx"
}
```

Response

```json
{
    "access":"new_token"
}
```

> যদি Refresh Token HttpOnly Cookie-তে থাকে, তাহলে Body-তে Refresh Token পাঠাতে হয় না। Browser Cookie নিজে পাঠাবে (যদি `withCredentials` এবং Backend Configuration ঠিক থাকে)।

---

# Axios Response Interceptor

Internally

```text
API Request

↓

401

↓

Refresh Token

↓

Save New Access

↓

Retry Original Request
```

---

# Step 7: Retry Request

Example

```text
GET

↓

401

↓

Refresh

↓

Retry

↓

200 OK
```

User

কিছুই বুঝবে না।

---

# Step 8: Refresh Failed

Refresh Token

↓

Expired

↓

Refresh API

↓

401

↓

Logout

↓

Login Page

---

# Logout Flow

```text
Logout Button

↓

POST /logout/

↓

Blacklist Refresh Token

↓

Clear Memory

↓

Clear Cookie

↓

Navigate Login
```

---

# Protected Route

Public

```text
/login

/register
```

Private

```text
/dashboard

/profile

/exams

/results
```

---

Flow

```text
Route

↓

Authenticated?

↓

Yes

↓

Render

---------------

No

↓

Login
```

---

# Teacher Route

```text
/admin

↓

Role?

↓

Teacher?

↓

Render
```

Student

↓

403 Page

---

# Auth Context

React

```text
AuthContext

↓

User

↓

Access Token

↓

Login()

↓

Logout()
```

সব Component

```text
useAuth()
```

দিয়ে Authentication State পাবে।

---

# Token Lifecycle

```text
Login

↓

Access

↓

API

↓

Expired

↓

Refresh

↓

New Access

↓

Continue
```

---

# Refresh Queue Problem

ধরুন

একসাথে

```text
10 Requests
```

গেল।

সবগুলো

```text
401
```

Return করল।

যদি প্রতিটি Request আলাদা Refresh Call করে, তাহলে

```text
10 Refresh Requests
```

হয়ে যাবে।

Production Solution

```text
First Refresh

↓

Other Requests Wait

↓

New Token

↓

Retry All
```

এটাকে **Refresh Queue** বা **Single Refresh Strategy** বলা হয়।

---

# React Folder Structure

```text
src/

    api/

        api.js

    context/

        AuthContext.jsx

    hooks/

        useAuth.js

    pages/

        Login.jsx

        Register.jsx

    routes/

        ProtectedRoute.jsx

    services/

        authService.js
```

---

# Your Exam SaaS Flow

Teacher

```text
Login

↓

Dashboard

↓

Create Course

↓

Create Exam

↓

Publish Result
```

Student

```text
Login

↓

Join Course

↓

Attend Exam

↓

View Result
```

---

# Authentication Architecture

```text
React

↓

Axios

↓

Request Interceptor

↓

Access Token

↓

Django

↓

JWT

↓

401

↓

Response Interceptor

↓

Refresh

↓

Retry
```

---

# Production Best Practices

### ✅ Access Token

5–15 Minutes

---

### ✅ Refresh Token

7–30 Days (Project Requirement অনুযায়ী)

---

### ✅ Access Token

Memory-তে রাখুন

---

### ✅ Refresh Token

HttpOnly Cookie-তে রাখুন

---

### ✅ Axios Interceptor

Use করুন

---

### ✅ Logout

Server + Client উভয় জায়গায় Session/Token পরিষ্কার করুন।

---

### ✅ HTTPS

Production-এ Always

---

# Common Mistakes

## ❌ Store Everything in LocalStorage

XSS Risk।

---

## ❌ No Refresh Flow

বারবার Login করতে হবে।

---

## ❌ Multiple Refresh Requests

Performance Problem।

---

## ❌ Token Never Expires

Security Risk।

---

## ❌ Public Route Protection নেই

সবাই Dashboard দেখতে পারবে।

---

# Interview Questions

## 1. React-এ Access Token কোথায় রাখবেন?

**Answer:**

Production-এ সাধারণত Memory-তে।

---

## 2. Refresh Token কোথায় রাখবেন?

**Answer:**

HttpOnly Secure Cookie-তে।

---

## 3. Axios Interceptor কেন ব্যবহার করবেন?

**Answer:**

প্রতিটি Request-এ Token Automatically Add করা এবং 401 পেলে Automatically Refresh করার জন্য।

---

## 4. Access Token Expire হলে কী হবে?

**Answer:**

Response Interceptor Refresh API Call করবে, নতুন Access Token নেবে, তারপর Original Request Retry করবে।

---

## 5. Refresh Token-ও Expire হলে?

**Answer:**

User-কে Logout করে Login Page-এ Redirect করা হবে।

---

# React Authentication Flow Summary

```text
Login
   │
   ▼
Access + Refresh
   │
   ▼
Access in Memory
Refresh in HttpOnly Cookie
   │
   ▼
Protected API
   │
   ▼
401?
   │
   ▼
Refresh Access Token
   │
   ▼
Retry Request
   │
   ▼
Success
```

---

# 🎯 Homework

আপনার **Exam SaaS Project**-এর Authentication Architecture ডিজাইন করুন:

```text
Login Page
      │
      ▼
AuthContext
      │
      ▼
Axios Instance
      │
      ▼
Request Interceptor
      │
      ▼
Django REST API
      │
      ▼
JWT
      │
      ▼
Protected Routes
      │
      ▼
Response Interceptor
      │
      ▼
Auto Refresh
      │
      ▼
Logout
```

ভাবুন:

1. Teacher Login-এর পরে কোন Route-এ যাবে?
2. Student Login-এর পরে কোন Route-এ যাবে?
3. কোন Page Public হবে?
4. কোন Page শুধুমাত্র Teacher দেখতে পারবে?
5. Refresh Token Expire হলে User Experience কী হবে?

---

## 🎓 এরপর কী?

Authentication ও Security সিরিজ প্রায় সম্পূর্ণ। আপনার লক্ষ্য যেহেতু **Production-Level Django REST Framework + React SaaS Development**, তাই পরবর্তী ধাপে আমি এই ক্রমে এগোনোর পরামর্শ দেব:

1. **Advanced ViewSets & Routers**
2. **Advanced Serializers**
3. **Filtering, Searching & Ordering**
4. **Pagination**
5. **File Uploads**
6. **Signals & Background Tasks**
7. **Caching**
8. **Testing (API Tests)**
9. **Deployment (Docker + Nginx + Gunicorn + PostgreSQL + Redis)**

এই বিষয়গুলো শেষ করলে আপনি একটি সম্পূর্ণ Production-Ready DRF Backend তৈরি করার জন্য প্রস্তুত হবেন।
এটি খুব ভালো সিদ্ধান্ত। **নতুন Topic শেখা এখন বন্ধ করুন।** এখন সবচেয়ে গুরুত্বপূর্ণ হলো **Revision + Hands-on Coding**।

আপনি গত কয়েকদিনে অনেক গুরুত্বপূর্ণ Topic শিখেছেন। যদি এখন নতুন Topic শিখতে থাকেন, তাহলে আগেরগুলো ভুলে যাওয়ার সম্ভাবনা থাকবে।

## Phase 1: Revision (2-3 Days)

নিচের ক্রমে Revision করুন:

### Day 1: Authentication

* ✅ JWT Basics
* ✅ Access Token
* ✅ Refresh Token
* ✅ Simple JWT
* ✅ dj-rest-auth
* ✅ Login
* ✅ Logout
* ✅ Registration
* ✅ Password Reset
* ✅ Email Verification

**Coding করুন:**

* Login API
* Register API
* Profile API
* Change Password API
* Logout API

---

### Day 2: Authorization

* ✅ Authentication vs Permission
* ✅ Permission Classes
* ✅ Custom Permission
* ✅ Object Permission
* ✅ Django Groups
* ✅ RBAC
* ✅ Owner Permission

**Coding করুন:**

* Teacher Create Course
* Student Cannot Create Course
* Teacher Edit Own Course
* Teacher Cannot Edit Others Course

---

### Day 3: Security

* ✅ Throttling
* ✅ JWT Security
* ✅ CORS
* ✅ CSRF
* ✅ XSS
* ✅ SQL Injection
* ✅ Production Security

**Coding করুন:**

* Login Throttle
* OTP Throttle
* Custom Permission
* Secure Settings

---

# Phase 2: Build Everything Yourself

শুধু পড়বেন না।

নিজে Build করুন।

Example

```text
accounts/

POST /register/

POST /login/

POST /logout/

GET /profile/

PATCH /change-password/
```

সব নিজে লিখুন।

---

তারপর

```text
courses/

Course CRUD

Owner Permission

Teacher Permission
```

---

তারপর

```text
exams/

Exam CRUD

Object Permission

Custom Permission
```

---

# Phase 3: React Integration

যখন Backend Ready হবে

তখন

```text
React

↓

Login

↓

JWT

↓

Protected Route

↓

Axios

↓

Refresh Token
```

Implement করবেন।

---

# Coding Rule

প্রতিটি Feature-এর জন্য এই ১০টি Step Follow করুন:

```text
1. Model

2. Serializer

3. Validation

4. View/ViewSet

5. URL

6. Permission

7. Authentication

8. Testing (Postman)

9. Error Handling

10. Refactor
```

---

# Interview Revision Checklist

নিজেকে এই প্রশ্নগুলো করুন:

* JWT Stateless কেন?
* Access Token ও Refresh Token-এর পার্থক্য কী?
* Authentication vs Permission?
* `request.user` কীভাবে Set হয়?
* `has_permission()` vs `has_object_permission()`?
* Django Group কী?
* RBAC কী?
* Throttling কেন ব্যবহার করি?
* CORS কী?
* CSRF কী?
* JWT Flow কী?
* React Authentication Flow কী?

যদি **বই বা নোট না দেখে** এগুলোর উত্তর দিতে পারেন, তাহলে আপনার ধারণা ভালো হয়েছে।

---

# আমার পরামর্শ

এখন **নতুন Lesson শুরু করবেন না।**

আগে:

* ✅ Revision
* ✅ Coding Implementation
* ✅ বারবার Practice
* ✅ ছোট Project-এ Apply

এগুলো শেষ করুন।

আপনি যেহেতু **Production-Level Django REST Framework + React Exam SaaS** বানাতে চান, তাই **Theory + Coding**—দুটোই সমান গুরুত্বপূর্ণ। শুধু পড়লে হবে না, আর শুধু Code Copy করলেও হবে না। প্রতিটি Feature নিজে লিখে, Debug করে, এবং কেন কাজ করছে তা বুঝে এগোলে আপনার শেখা অনেক বেশি শক্ত হবে।

যখন Revision এবং Coding শেষ হবে, তখন আমরা **Production-Level Exam SaaS Backend** (Course, Enrollment, Exam, Question, Result, Payment, Notifications ইত্যাদি) Step-by-Step তৈরি শুরু করতে পারব।
