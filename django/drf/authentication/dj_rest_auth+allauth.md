অবশ্যই। যেহেতু তুমি ইতিমধ্যে **manual OAuth implementation** শিখেছ এবং এখন **production-ready authentication** শিখতে চাও, তাই এবার আমরা **dj-rest-auth + django-allauth + SimpleJWT** ব্যবহার করে একটি complete DRF authentication system বানাব।

এটা এমনভাবে হবে যেন শেষে তুমি যেকোনো কোম্পানির authentication system implement করতে পারো। Official `dj-rest-auth` setup অনুযায়ী `django-allauth`, `dj_rest_auth.registration`, `SimpleJWT` এবং social providers (Google/GitHub/Facebook) ব্যবহার করব। ([DJ Rest Auth][1])

# Project

```
DRF Authentication Mastery
```

## Final Features

✅ Custom User Model

✅ Email Registration

✅ Email Verification

✅ Login

✅ Logout

✅ JWT Authentication

✅ Refresh Token

✅ Password Reset

✅ Change Password

✅ User Profile

✅ Google Login

✅ GitHub Login

✅ Facebook Login

✅ React Integration

✅ Production Settings

---

# 15 Git Commits Roadmap

## Commit 1

```
feat(project): initialize project and install authentication packages
```

Topics

* Create Project
* Create users app
* Install

  * django
  * djangorestframework
  * dj-rest-auth
  * django-allauth
  * simplejwt
  * python-decouple
* Basic settings
* Initial migration

---

## Commit 2

```
feat(users): implement custom user model
```

Topics

* AbstractUser
* Email as username
* CustomUserManager
* AUTH_USER_MODEL
* Admin Registration

---

## Commit 3

```
feat(auth): configure dj-rest-auth with JWT
```

Topics

* REST_FRAMEWORK
* SimpleJWT
* JWT Cookies
* Login
* Logout
* Refresh
* Verify Token

---

## Commit 4

```
feat(registration): enable user registration
```

Topics

* dj_rest_auth.registration
* Signup
* Email Signup
* Validation
* Registration API

---

## Commit 5

```
feat(email): configure email verification
```

Topics

* SMTP
* Email Verification
* Verify Email
* Resend Verification
* Production Email Settings

---

## Commit 6

```
feat(profile): user profile management
```

Topics

* Current User API
* Update Profile
* Serializer Customization
* Permissions

---

## Commit 7

```
feat(password): password reset and password change
```

Topics

* Password Reset
* Reset Confirm
* Change Password
* Custom Templates

---

## Commit 8

```
refactor(auth): customize serializers and responses
```

Topics

* Custom RegisterSerializer
* Custom LoginSerializer
* JWT Response
* Extra Fields

---

## Commit 9

```
feat(google): configure Google OAuth
```

Topics

* Google Provider
* SocialApp
* Google Login API
* Testing

---

## Commit 10

```
feat(github): integrate GitHub OAuth
```

Topics

* GitHub Provider
* Social Login
* JWT Return

---

## Commit 11

```
feat(facebook): integrate Facebook OAuth
```

Topics

* Facebook Login
* OAuth Flow
* Account Linking

---

## Commit 12

```
feat(security): production authentication settings
```

Topics

* CORS
* CSRF
* Cookie Security
* HTTPS
* Secure JWT Cookie

---

## Commit 13

```
feat(react): integrate React frontend authentication
```

Topics

* Axios
* Login
* Register
* Refresh Token
* Protected Route
* Google Login
* GitHub Login
* Facebook Login

---

## Commit 14

```
test(auth): comprehensive authentication testing
```

Topics

* Postman
* Swagger
* Edge Cases
* Error Handling
* Security Testing

---

## Commit 15

```
docs(auth): finalize authentication module
```

Topics

* Folder Structure
* API Documentation
* Deployment
* Best Practices
* Common Mistakes
* Interview Questions

---

# আমরা প্রতিটি Commit-এ কী করব?

প্রতি Commit-এ থাকবে:

* Project Structure
* Complete Code
* প্রতিটি লাইনের Explanation
* কেন এটা করা হচ্ছে
* Common Mistakes
* Postman Testing
* Expected Response
* Git Commit
* Interview Questions
* React Integration (যেখানে প্রযোজ্য)

এভাবে শেষ হলে এটি শুধু একটি tutorial হবে না, বরং **production-grade authentication module** হবে যা তুমি নিজের সব DRF project-এ reuse করতে পারবে।

**আগামী Lesson শুরু হবে: *Commit 1 – Project Initialization & Authentication Package Setup***, যেখানে আমরা project create করা থেকে `dj-rest-auth`, `django-allauth`, `SimpleJWT` এবং initial configuration পর্যন্ত প্রতিটি লাইন বিস্তারিতভাবে implement করব।

[1]: https://dj-rest-auth.readthedocs.io/en/latest/getting-started/installation/?utm_source=chatgpt.com "Installation - dj-rest-auth"


-----


# Commit 1

```bash
feat(project): initialize project and install authentication packages
```

---

# Goal

এই commit শেষে আমাদের কাছে থাকবে—

* ✅ Django Project
* ✅ DRF
* ✅ dj-rest-auth
* ✅ django-allauth
* ✅ SimpleJWT
* ✅ Custom User App
* ✅ Environment Variables
* ✅ Initial Authentication Configuration

এখনও Login/Register হবে না। আমরা শুধু authentication-এর foundation তৈরি করব।

---

# Final Project Structure

```text
auth_mastery/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   ├── wsgi.py
│
├── users/
│   ├── migrations/
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│
├── .env
├── manage.py
├── requirements.txt
```

---

# Step 1 Create Virtual Environment

Linux

```bash
python3 -m venv venv
```

Activate

```bash
source venv/bin/activate
```

Windows

```bash
python -m venv venv

venv\Scripts\activate
```

---

# Step 2 Install Packages

```bash
pip install django
```

```bash
pip install djangorestframework
```

```bash
pip install dj-rest-auth
```

```bash
pip install django-allauth
```

```bash
pip install djangorestframework-simplejwt
```

```bash
pip install python-decouple
```

---

## কেন এই package?

### Django

Project Framework

---

### DRF

REST API তৈরির জন্য

---

### dj-rest-auth

Ready-made Authentication API

যেমন

* Login
* Logout
* Password Reset
* Password Change
* Register

---

### django-allauth

Social Authentication

যেমন

* Google
* Github
* Facebook
* Email Verification

> **Note:** `dj-rest-auth` social authentication-এর জন্য `django-allauth`-এর উপর নির্ভর করে।

---

### SimpleJWT

JWT Token Generate করবে

Example

```text
Access Token

Refresh Token
```

---

### python-decouple

Secret Key

Database Password

OAuth Secret

সব `.env` এ রাখবো।

---

# Step 3 Freeze Requirements

```bash
pip freeze > requirements.txt
```

---

# Step 4 Create Project

```bash
django-admin startproject config .
```

Current Structure

```text
config/

manage.py
```

---

# Step 5 Create Users App

```bash
python manage.py startapp users
```

---

# Step 6 settings.py

বর্তমান

```python
INSTALLED_APPS = [
    ...
]
```

Replace

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    # Third Party

    "rest_framework",

    "rest_framework.authtoken",

    "dj_rest_auth",

    "django.contrib.sites",

    "allauth",

    "allauth.account",

    "allauth.socialaccount",

    "dj_rest_auth.registration",

    # Local

    "users",

]
```

---

## Explain

### rest_framework

সব API এর জন্য।

---

### authtoken

`dj-rest-auth`-এর কিছু feature এখনো এটি ব্যবহার করতে পারে। JWT ব্যবহার করলেও এটি রাখা safe।

---

### dj_rest_auth

Authentication APIs

---

### django.contrib.sites

`allauth`-এর জন্য Required

---

### allauth.account

Email Authentication

---

### allauth.socialaccount

Google

Github

Facebook

---

### dj_rest_auth.registration

Registration API Enable করবে।

---

# Step 7 SITE_ID

settings.py

```python
SITE_ID = 1
```

---

## কেন?

allauth Site Framework ব্যবহার করে।

Database-এ Site table থাকবে।

Default

```text
example.com
```

আমরা পরে change করবো।

---

# Step 8 REST_FRAMEWORK

settings.py

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ),

}
```

---

## Explain

সব API JWT ব্যবহার করবে।

---

# Step 9 SIMPLE JWT

settings.py

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=30),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": False,

    "BLACKLIST_AFTER_ROTATION": False,

}
```

---

## Explain

Access Token

```text
30 Minutes
```

Refresh Token

```text
7 Days
```

---

# Step 10 Environment Variable

Create

```
.env
```

Add

```env
SECRET_KEY=django-insecure-change-this-secret
DEBUG=True
```

---

settings.py

```python
from decouple import config

SECRET_KEY = config("SECRET_KEY")

DEBUG = config("DEBUG", cast=bool)
```

---

## কেন?

কখনো Secret Key GitHub-এ push করা উচিত না।

---

# Step 11 urls.py

বর্তমান

```python
urlpatterns = [
]
```

Replace

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [

    path(
        "admin/",
        admin.site.urls,
    ),

    path(
        "api/auth/",
        include("dj_rest_auth.urls"),
    ),

]
```

---

## এখন কী কী Endpoint তৈরি হবে?

এখনই `dj-rest-auth` কিছু built-in endpoint expose করবে (যদিও কিছু endpoint পরবর্তী commit-এ পুরোপুরি configure হবে)।

```text
/api/auth/login/

/api/auth/logout/

/api/auth/password/change/

/api/auth/password/reset/

/api/auth/user/
```

---

# Step 12 Migration

```bash
python manage.py makemigrations
```

```bash
python manage.py migrate
```

---

Migration শেষে Database-এ নতুন table তৈরি হবে।

যেমন

```text
auth_user

django_site

authtoken_token

account_emailaddress

account_emailconfirmation
```

> `account_*` table এসেছে `django-allauth` থেকে।

---

# Step 13 Create Superuser

```bash
python manage.py createsuperuser
```

---

# Step 14 Run Server

```bash
python manage.py runserver
```

Open

```
http://127.0.0.1:8000/admin/
```

Login করুন।

---

# Common Mistakes 🚨

### 1. `SITE_ID` না দিলে

```text
django.core.exceptions.ImproperlyConfigured
```

---

### 2. `.env` load না করলে

```text
SECRET_KEY not found
```

---

### 3. `django.contrib.sites` বাদ দিলে

```text
Site matching query does not exist
```

---

### 4. `allauth` install না করে app add করলে

```text
ModuleNotFoundError
```

---

# Verify Installation

Run:

```bash
python manage.py check
```

Expected:

```text
System check identified no issues (0 silenced).
```

---

# Git Commit

```bash
git add .

git commit -m "feat(project): initialize project and install authentication packages"
```

---

## এই Commit শেষে কী সম্পন্ন হলো?

* ✅ Django project initialized
* ✅ DRF configured
* ✅ `dj-rest-auth` installed
* ✅ `django-allauth` installed
* ✅ JWT authentication configured
* ✅ `.env` configuration added
* ✅ `users` app created
* ✅ Base authentication infrastructure ready

### পরবর্তী Commit (Commit 2)

**`feat(users): implement custom user model`**

এখানে আমরা email-based custom user model, custom user manager এবং `AUTH_USER_MODEL` configure করব।


------------

# Commit 2

```bash
feat(users): implement custom user model with email authentication
```

---

# Goal

এই commit শেষে আমাদের থাকবে—

* ✅ Custom User Model
* ✅ Email Login
* ✅ No Username Field
* ✅ Custom User Manager
* ✅ AUTH_USER_MODEL
* ✅ Admin Support

> **কেন শুরুতেই Custom User?**
> Django project শুরু হওয়ার পর `AUTH_USER_MODEL` পরিবর্তন করা খুব ঝামেলার। তাই নতুন project-এর শুরুতেই এটা করা best practice।

---

# Final Structure

```text
users/

├── admin.py
├── apps.py
├── managers.py
├── models.py
├── serializers.py
├── urls.py
├── views.py
```

---

# Step 1

Create

```text
users/managers.py
```

---

# Step 2

```python
from django.contrib.auth.base_user import BaseUserManager


class CustomUserManager(BaseUserManager):

    use_in_migrations = True

    def create_user(
        self,
        email,
        password=None,
        **extra_fields,
    ):

        if not email:
            raise ValueError(
                "Email is required."
            )

        email = self.normalize_email(email)

        user = self.model(
            email=email,
            **extra_fields,
        )

        user.set_password(password)

        user.save(using=self._db)

        return user

    def create_superuser(
        self,
        email,
        password,
        **extra_fields,
    ):

        extra_fields.setdefault(
            "is_staff",
            True,
        )

        extra_fields.setdefault(
            "is_superuser",
            True,
        )

        extra_fields.setdefault(
            "is_active",
            True,
        )

        if extra_fields.get("is_staff") is not True:
            raise ValueError(
                "Superuser must have is_staff=True."
            )

        if extra_fields.get("is_superuser") is not True:
            raise ValueError(
                "Superuser must have is_superuser=True."
            )

        return self.create_user(
            email,
            password,
            **extra_fields,
        )
```

---

# Explain

## BaseUserManager

Django-এর built-in manager।

এটাই

```python
User.objects.create_user()
```

handle করে।

---

## normalize_email()

যদি user লেখে

```text
ABC@GMAIL.COM
```

store হবে

```text
ABC@gmail.com
```

---

## set_password()

❌ ভুল

```python
user.password = password
```

Database

```text
123456
```

stored হবে।

---

✅ সঠিক

```python
user.set_password(password)
```

Database

```text
pbkdf2_sha256$....
```

hash store হবে।

---

# Step 3

models.py

Replace everything

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

from .managers import CustomUserManager


class User(AbstractUser):

    username = None

    email = models.EmailField(
        unique=True,
    )

    first_name = models.CharField(
        max_length=150,
        blank=True,
    )

    last_name = models.CharField(
        max_length=150,
        blank=True,
    )

    phone = models.CharField(
        max_length=20,
        blank=True,
    )

    avatar = models.URLField(
        blank=True,
    )

    USERNAME_FIELD = "email"

    REQUIRED_FIELDS = []

    objects = CustomUserManager()

    def __str__(self):
        return self.email
```

---

# Explain

## username=None

Default username field remove।

এখন

❌

```text
username
```

থাকবে না।

---

## email unique

```python
email = models.EmailField(unique=True)
```

এক email দুইবার register করা যাবে না।

---

## USERNAME_FIELD

```python
USERNAME_FIELD = "email"
```

Login হবে

```text
email + password
```

---

## REQUIRED_FIELDS

```python
[]
```

createsuperuser এ শুধু

```text
Email

Password
```

চাইবে।

---

# Step 4

settings.py

Add

```python
AUTH_USER_MODEL = "users.User"
```

---

## কেন?

এখন থেকে

```python
from django.contrib.auth.models import User
```

❌

use করা যাবে না।

সব জায়গায়

```python
from django.contrib.auth import get_user_model

User = get_user_model()
```

---

# Step 5

admin.py

Replace

```python
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import User


@admin.register(User)
class CustomUserAdmin(UserAdmin):

    ordering = ("email",)

    list_display = (
        "email",
        "first_name",
        "last_name",
        "is_staff",
    )

    search_fields = (
        "email",
        "first_name",
        "last_name",
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
            "Personal Info",
            {
                "fields": (
                    "first_name",
                    "last_name",
                    "phone",
                    "avatar",
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

        (
            "Important Dates",
            {
                "fields": (
                    "last_login",
                    "date_joined",
                )
            },
        ),

    )

    add_fieldsets = (

        (
            None,
            {
                "classes": (
                    "wide",
                ),

                "fields": (
                    "email",
                    "password1",
                    "password2",
                    "is_staff",
                    "is_superuser",
                ),
            },
        ),

    )
```

---

# Step 6

Delete old database (শুধু development-এ)

```bash
rm db.sqlite3
```

Delete migration

```bash
rm users/migrations/0001_initial.py
```

> Windows হলে `del db.sqlite3` এবং migrations ফোল্ডারের `0001_initial.py` delete করো।

---

# Step 7

Migration

```bash
python manage.py makemigrations
```

Expected

```text
users
```

---

Run

```bash
python manage.py migrate
```

---

# Step 8

Create Superuser

```bash
python manage.py createsuperuser
```

Input

```text
Email:
admin@gmail.com

Password:
********
```

Notice

username চাইবে না।

---

# Step 9

Run Server

```bash
python manage.py runserver
```

Login

```text
/admin
```

Admin Dashboard

Users

```
admin@gmail.com
```

---

# Common Mistakes 🚨

## Mistake 1

```python
USERNAME_FIELD = "username"
```

❌ Email login কাজ করবে না।

---

## Mistake 2

```python
user.password = password
```

❌ Password plain text হবে।

---

## Mistake 3

```python
from django.contrib.auth.models import User
```

❌ Custom User project-এ এটা ব্যবহার করো না।

Use

```python
from django.contrib.auth import get_user_model

User = get_user_model()
```

---

## Mistake 4

Project শুরু করার পরে

```python
AUTH_USER_MODEL
```

change করা।

এটা migration conflict তৈরি করতে পারে।

---

# Test

Shell

```bash
python manage.py shell
```

```python
from django.contrib.auth import get_user_model

User = get_user_model()

user = User.objects.create_user(
    email="test@gmail.com",
    password="test1234"
)

print(user.email)

print(user.check_password("test1234"))
```

Expected

```text
test@gmail.com

True
```

---

# Git Commit

```bash
git add .

git commit -m "feat(users): implement custom user model with email authentication"
```

---

# Commit 2 Complete ✅

এখন project পুরোপুরি **email-based custom user** ব্যবহার করছে। এটা পরবর্তী `dj-rest-auth`, `allauth`, Google/GitHub/Facebook OAuth-এর জন্য শক্ত ভিত্তি তৈরি করল।

## Commit 3

```text
feat(auth): configure dj-rest-auth with JWT authentication
```

এখানে আমরা `dj-rest-auth`-কে **SimpleJWT**-এর সাথে integrate করব, যাতে `/api/auth/login/`, `/api/auth/logout/`, `/api/auth/token/refresh/` ইত্যাদি endpoint JWT দিয়ে কাজ করে।


-------

## Commit 3

```bash
feat(auth): configure dj-rest-auth with SimpleJWT authentication
```

---

# Goal

এই commit শেষে আমরা পাবো—

* ✅ JWT Login
* ✅ JWT Logout
* ✅ Access Token
* ✅ Refresh Token
* ✅ Current User API
* ✅ Refresh Token API
* ✅ JWT Authentication Working

**এই commit শেষে frontend React সহজেই Login করতে পারবে।**

---

# JWT Flow

```text
                Login

                  │

        Email + Password

                  │

         dj-rest-auth Login

                  │

      ┌───────────┴───────────┐

      │                       │

 Access Token           Refresh Token

      │

Protected APIs
```

---

# Step 1

Install JWT Blacklist

```bash
pip install djangorestframework-simplejwt
```

> যদি Commit 1 এ install করে থাকো তাহলে skip করো।

---

# Step 2

settings.py

Add

```python
INSTALLED_APPS = [

    ...

    "rest_framework_simplejwt.token_blacklist",

]
```

---

## কেন?

Logout করার সময় Refresh Token blacklist হবে।

Production project এ এটা খুব important।

---

# Step 3

settings.py

Replace

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ),

}
```

with

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "dj_rest_auth.jwt_auth.JWTCookieAuthentication",

    ),

    "DEFAULT_PERMISSION_CLASSES": (

        "rest_framework.permissions.IsAuthenticated",

    ),

}
```

---

## Explain

আগে

```text
JWTAuthentication
```

ছিল।

এখন

```text
JWTCookieAuthentication
```

হবে।

কারণ

dj-rest-auth

এবং

SimpleJWT

একসাথে smoothly কাজ করবে।

---

# Step 4

settings.py

Add

```python
REST_USE_JWT = True
```

---

## Explain

Default

```text
TokenAuthentication
```

Use করে।

আমরা চাই

```text
JWT
```

Use করুক।

---

# Step 5

settings.py

Add

```python
JWT_AUTH_COOKIE = "access"

JWT_AUTH_REFRESH_COOKIE = "refresh"
```

---

## কেন?

Login করলে Cookie এর নাম হবে

```text
access

refresh
```

---

# Step 6

Update SIMPLE_JWT

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=30),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "UPDATE_LAST_LOGIN": True,

    "AUTH_HEADER_TYPES": (

        "Bearer",

    ),

}
```

---

## Explain

### ROTATE_REFRESH_TOKENS

Old Refresh Token

↓

New Refresh Token

Generate হবে।

Security Better।

---

### UPDATE_LAST_LOGIN

Login করলে

```text
last_login
```

Update হবে।

---

### AUTH_HEADER_TYPES

Frontend পাঠাবে

```text
Authorization:

Bearer eyJhbGc...
```

---

# Step 7

settings.py

Add

```python
REST_AUTH = {

    "USE_JWT": True,

    "JWT_AUTH_COOKIE": "access",

    "JWT_AUTH_REFRESH_COOKIE": "refresh",

    "SESSION_LOGIN": False,

}
```

---

## Explain

SESSION_LOGIN

False

কারণ

আমরা Session Login ব্যবহার করবো না।

Only JWT।

---

# Step 8

config/urls.py

বর্তমান

```python
urlpatterns = [

    path(
        "api/auth/",
        include("dj_rest_auth.urls"),
    ),

]
```

এর নিচে add

```python
from rest_framework_simplejwt.views import (

    TokenRefreshView,

)
```

urlpatterns

```python
path(

    "api/auth/token/refresh/",

    TokenRefreshView.as_view(),

),
```

---

## কেন?

Frontend

Refresh Token পাঠাবে

↓

New Access Token পাবে।

---

# Step 9

Migration

```bash
python manage.py migrate
```

---

Expected

```text
token_blacklist
```

table তৈরি হবে।

---

# Step 10

Create Test User

```bash
python manage.py shell
```

```python
from django.contrib.auth import get_user_model

User = get_user_model()

User.objects.create_user(

    email="admin@gmail.com",

    password="admin1234"

)
```

---

# Step 11

Run Server

```bash
python manage.py runserver
```

---

# Testing Login

POST

```http
POST

/api/auth/login/
```

Body

```json
{

    "email":"admin@gmail.com",

    "password":"admin1234"

}
```

Expected Response

```json
{
    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{
        "pk":1,
        "email":"admin@gmail.com"
    }
}
```

---

# Current User API

GET

```http
/api/auth/user/
```

Header

```text
Authorization:

Bearer ACCESS_TOKEN
```

Response

```json
{
    "pk":1,
    "email":"admin@gmail.com",
    "first_name":"",
    "last_name":""
}
```

---

# Refresh Token

POST

```http
/api/auth/token/refresh/
```

Body

```json
{

    "refresh":"YOUR_REFRESH_TOKEN"

}
```

Response

```json
{

    "access":"NEW_ACCESS_TOKEN"

}
```

---

# Logout

POST

```http
/api/auth/logout/
```

Header

```text
Authorization:

Bearer ACCESS_TOKEN
```

Response

```json
{

    "detail":"Successfully logged out."

}
```

---

# Folder Structure

```text
config/

users/

manage.py

requirements.txt
```

এখনও

```text
serializers.py

views.py
```

empty থাকবে।

সব customization

Commit 4 থেকে শুরু হবে।

---

# Common Mistakes 🚨

## 1

```python
REST_USE_JWT = False
```

Login করলে

```text
TokenAuthentication
```

return করবে।

---

## 2

```python
SESSION_LOGIN = True
```

JWT এর সাথে Session Login mixed হয়ে যাবে।

---

## 3

```python
"rest_framework_simplejwt.token_blacklist"
```

add না করলে

Logout blacklist properly কাজ করবে না।

---

## 4

Header

```text
Token xxxxxxxxx
```

❌

Correct

```text
Bearer xxxxxxxxx
```

---

# Test Checklist

* ✅ Login
* ✅ Access Token
* ✅ Refresh Token
* ✅ Current User
* ✅ Refresh API
* ✅ Logout

সব pass করলে Commit Complete।

---

# Git Commit

```bash
git add .

git commit -m "feat(auth): configure dj-rest-auth with SimpleJWT authentication"
```

---

## ⚠️ একটি গুরুত্বপূর্ণ নোট

উপরের configuration `dj-rest-auth`-এর version অনুযায়ী সামান্য ভিন্ন হতে পারে। নতুন version-এ `REST_USE_JWT`-এর পরিবর্তে `REST_AUTH = {"USE_JWT": True}`-ই প্রধান configuration। তাই **দুটো একসাথে ব্যবহার না করে**, তোমার installed version অনুযায়ী আমরা পরবর্তী commit-এ configuration clean করে production-ready করব।

## Commit 4

```bash
feat(registration): enable user registration with dj-rest-auth and allauth
```

এখানে আমরা email registration, signup endpoint, email validation এবং custom `RegisterSerializer` implement করব।


-----------

# Commit 4

```bash id="c4a8p1"
feat(registration): enable user registration with dj-rest-auth and django-allauth
```

---

# Goal

এই Commit শেষে আমরা পাবো—

* ✅ User Registration API
* ✅ Email দিয়ে Signup
* ✅ Password Validation
* ✅ Duplicate Email Check
* ✅ Custom Register Serializer
* ✅ Email Verification Ready
* ✅ Production Ready Registration Flow

---

# Registration Flow

```text
          Client

             │

     POST /api/auth/registration/

             │

   Custom Register Serializer

             │

     django-allauth

             │

        User Created

             │

 Email Verification (Commit 5)
```

---

# Step 1

settings.py

Add

```python
INSTALLED_APPS = [

    ...

    "dj_rest_auth.registration",

]
```

> যদি Commit 1-এ add করে থাকো তাহলে আর লাগবে না।

---

# Step 2

urls.py

বর্তমান

```python
urlpatterns = [

    path(
        "api/auth/",
        include("dj_rest_auth.urls"),
    ),

]
```

Replace

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [

    path(
        "admin/",
        admin.site.urls,
    ),

    path(
        "api/auth/",
        include("dj_rest_auth.urls"),
    ),

    path(
        "api/auth/registration/",
        include("dj_rest_auth.registration.urls"),
    ),

]
```

---

এখন নতুন Endpoint হবে

```
POST

/api/auth/registration/
```

---

# Step 3

settings.py

Add

```python
ACCOUNT_AUTHENTICATION_METHOD = "email"

ACCOUNT_EMAIL_REQUIRED = True

ACCOUNT_USERNAME_REQUIRED = False

ACCOUNT_USER_MODEL_USERNAME_FIELD = None
```

---

## Explain

আমরা username ব্যবহার করবো না।

Registration হবে

```
email

password
```

দিয়ে।

---

# Step 4

settings.py

Add

```python
ACCOUNT_UNIQUE_EMAIL = True
```

---

Duplicate Email

```
abc@gmail.com
```

আবার Register করতে পারবে না।

---

# Step 5

Create

```
users/serializers.py
```

---

Add

```python
from dj_rest_auth.registration.serializers import RegisterSerializer
from rest_framework import serializers


class CustomRegisterSerializer(RegisterSerializer):

    first_name = serializers.CharField(
        max_length=150,
        required=True,
    )

    last_name = serializers.CharField(
        max_length=150,
        required=True,
    )

    phone = serializers.CharField(
        required=False,
    )

    def get_cleaned_data(self):

        data = super().get_cleaned_data()

        data["first_name"] = self.validated_data.get(
            "first_name",
            "",
        )

        data["last_name"] = self.validated_data.get(
            "last_name",
            "",
        )

        data["phone"] = self.validated_data.get(
            "phone",
            "",
        )

        return data

    def save(self, request):

        user = super().save(request)

        user.first_name = self.cleaned_data.get(
            "first_name"
        )

        user.last_name = self.cleaned_data.get(
            "last_name"
        )

        user.phone = self.cleaned_data.get(
            "phone"
        )

        user.save()

        return user
```

---

## কেন Serializer Customize করলাম?

Default Registration

```
email

password1

password2
```

Only।

আমরা চাই

```
email

password1

password2

first_name

last_name

phone
```

---

# Step 6

settings.py

Add

```python
REST_AUTH = {

    "USE_JWT": True,

    "REGISTER_SERIALIZER":
        "users.serializers.CustomRegisterSerializer",

}
```

---

এখন

Registration

↓

আমাদের Serializer ব্যবহার করবে।

---

# Step 7

Password Validation

settings.py

```python
AUTH_PASSWORD_VALIDATORS = [

    {
        "NAME":
        "django.contrib.auth.password_validation.UserAttributeSimilarityValidator",
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.MinimumLengthValidator",
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.CommonPasswordValidator",
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.NumericPasswordValidator",
    },

]
```

---

## এখন

Password

```
12345
```

দিলে

Validation Error দিবে।

---

# Step 8

Run Server

```bash
python manage.py runserver
```

---

# Test Registration

POST

```
/api/auth/registration/
```

Body

```json
{
    "email":"john@gmail.com",
    "password1":"StrongPassword123",
    "password2":"StrongPassword123",
    "first_name":"John",
    "last_name":"Doe",
    "phone":"01700000000"
}
```

---

Expected Response

```json
{
    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{
        "pk":2,
        "email":"john@gmail.com"
    }
}
```

> যদি Email Verification enable না থাকে তাহলে সঙ্গে সঙ্গে JWT return করবে।

---

# Duplicate Email Test

```json
{
    "email":"john@gmail.com",
    "password1":"StrongPassword123",
    "password2":"StrongPassword123"
}
```

Expected

```json
{
    "email":[
        "A user is already registered with this e-mail address."
    ]
}
```

---

# Weak Password Test

```json
{
    "password1":"12345678",
    "password2":"12345678"
}
```

Expected

```json
{
    "password1":[
        "This password is too common."
    ]
}
```

---

# Database

New User

```
users_user
```

Table

```
id

email

first_name

last_name

phone

password

is_active
```

---

# Common Mistakes 🚨

## 1

```python
ACCOUNT_USERNAME_REQUIRED = True
```

Username চাইবে।

---

## 2

```python
ACCOUNT_EMAIL_REQUIRED = False
```

Email ছাড়াও Register হবে।

---

## 3

Serializer

```python
save()
```

Override না করলে

```
phone
```

Database-এ save হবে না।

---

## 4

```python
REGISTER_SERIALIZER
```

settings.py-এ add না করলে

Default Serializer চলবে।

---

# Test Checklist

* ✅ Registration
* ✅ Duplicate Email
* ✅ Password Validation
* ✅ Extra Fields Save
* ✅ JWT Return

---

# Git Commit

```bash
git add .

git commit -m "feat(registration): enable user registration with django-allauth"
```

---

# 🔥 Senior Developer Note

এই commit-এ একটি বিষয় খেয়াল করবে। `django-allauth`-এর **সাম্প্রতিক version (65+)**-এ অনেক setting পরিবর্তন হয়েছে। যেমন:

* `ACCOUNT_AUTHENTICATION_METHOD` → নতুন API-তে `ACCOUNT_LOGIN_METHODS`
* `ACCOUNT_EMAIL_REQUIRED` → `ACCOUNT_SIGNUP_FIELDS` দিয়ে configure করা হয়।

আমরা tutorial-এ সর্বশেষ stable version অনুযায়ী code update করব, যাতে deprecated settings ব্যবহার না হয়।

## Commit 5

```
feat(email): implement email verification with django-allauth
```

এখানে SMTP configure করে **Email Verification**, **Activation Link**, **Resend Verification Email**, এবং production-ready email flow implement করব।

-----------

# Commit 5

```bash
feat(email): implement email verification with django-allauth
```

---

# 🎯 Goal

এই Commit শেষে আমরা পাবো—

* ✅ Email Verification
* ✅ Gmail SMTP Configuration
* ✅ Activation Email
* ✅ Verify Email Endpoint
* ✅ Resend Verification Email
* ✅ Login Only After Email Verification
* ✅ Production Ready Email Settings

---

# Email Verification Flow

```text
        Register

           │

           ▼

      User Created

           │

           ▼

Verification Email Sent

           │

           ▼

User Clicks Verification Link

           │

           ▼

Email Verified

           │

           ▼

User Can Login
```

---

# Step 1 Install Email Backend

আমরা Gmail SMTP ব্যবহার করবো।

Production এ SendGrid, AWS SES, Mailgun ব্যবহার করা ভালো।

---

# Step 2

`.env`

```env
EMAIL_HOST=smtp.gmail.com

EMAIL_PORT=587

EMAIL_USE_TLS=True

EMAIL_HOST_USER=yourgmail@gmail.com

EMAIL_HOST_PASSWORD=YOUR_APP_PASSWORD

DEFAULT_FROM_EMAIL=yourgmail@gmail.com
```

> ⚠️ এখানে Gmail Password না, **Google App Password** ব্যবহার করতে হবে।

---

# Step 3

settings.py

```python
from decouple import config

EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"

EMAIL_HOST = config("EMAIL_HOST")

EMAIL_PORT = config("EMAIL_PORT", cast=int)

EMAIL_USE_TLS = config("EMAIL_USE_TLS", cast=bool)

EMAIL_HOST_USER = config("EMAIL_HOST_USER")

EMAIL_HOST_PASSWORD = config("EMAIL_HOST_PASSWORD")

DEFAULT_FROM_EMAIL = config("DEFAULT_FROM_EMAIL")
```

---

## Explain

Django Email পাঠাবে

↓

SMTP Server

↓

Gmail

↓

User Inbox

---

# Step 4

Google Account

Go

```
Google Account

↓

Security

↓

2 Step Verification

↓

App Password
```

Create

```
Mail

↓

Other

↓

Django Auth
```

You'll get

```
abdc efgh ijkl mnop
```

এই Password

```
EMAIL_HOST_PASSWORD
```

এ বসবে।

---

# Step 5

settings.py

Add

```python
ACCOUNT_EMAIL_VERIFICATION = "mandatory"

ACCOUNT_CONFIRM_EMAIL_ON_GET = True

ACCOUNT_LOGIN_ON_EMAIL_CONFIRMATION = False

ACCOUNT_EMAIL_CONFIRMATION_EXPIRE_DAYS = 3
```

---

## Explain

### mandatory

Register করলে

↓

Email Verify না করা পর্যন্ত Login হবে না।

---

### Confirmation Expire

Activation Link

```
3 Days
```

পর expire হবে।

---

# Step 6

settings.py

Add

```python
ACCOUNT_EMAIL_SUBJECT_PREFIX = "[Auth Mastery] "
```

Mail Subject

```
[Auth Mastery] Confirm your email
```

---

# Step 7

settings.py

Add

```python
ACCOUNT_DEFAULT_HTTP_PROTOCOL = "http"
```

Development

```
http://localhost:8000
```

Production

```
https
```

---

# Step 8

settings.py

Add

```python
ACCOUNT_EMAIL_CONFIRMATION_AUTHENTICATED_REDIRECT_URL = "/"

ACCOUNT_EMAIL_CONFIRMATION_ANONYMOUS_REDIRECT_URL = "/"
```

Later

React URL দিবো।

---

# Step 9

settings.py

Add

```python
LOGIN_REDIRECT_URL = "/"

LOGOUT_REDIRECT_URL = "/"
```

---

# Step 10

Run Migration

```bash
python manage.py migrate
```

---

# Step 11

Run Server

```bash
python manage.py runserver
```

---

# Registration Test

POST

```
/api/auth/registration/
```

Body

```json
{
    "email":"john@gmail.com",

    "password1":"StrongPassword123",

    "password2":"StrongPassword123",

    "first_name":"John",

    "last_name":"Doe"
}
```

---

Expected

```json
{
    "detail":"Verification e-mail sent."
}
```

---

# Inbox

User will receive

```
Confirm your Email Address
```

Click

```
Verify Email
```

---

After Verification

Database

```
account_emailaddress
```

Now

```
verified=True
```

---

# Login Test

Before Verification

```
POST

/api/auth/login/
```

Response

```json
{
    "non_field_errors":[
        "E-mail is not verified."
    ]
}
```

---

After Verification

```json
{
    "access":"eyJhbGc...",

    "refresh":"eyJhbGc..."
}
```

---

# Email Tables

Migration already created

```
account_emailaddress

account_emailconfirmation
```

---

# Resend Verification

Endpoint

```
POST

/api/auth/registration/resend-email/
```

Body

```json
{
    "email":"john@gmail.com"
}
```

---

Expected

```json
{
    "detail":"Verification e-mail sent."
}
```

---

# Common Mistakes 🚨

## Gmail Password ব্যবহার করা

❌

```env
EMAIL_HOST_PASSWORD=gmail_password
```

Use

```
Google App Password
```

---

## ACCOUNT_EMAIL_VERIFICATION

```python
"optional"
```

Email Verify ছাড়াও Login হবে।

---

## EMAIL_BACKEND

Development এ

```python
console.EmailBackend
```

দিলে Email Console এ print হবে।

Production এ SMTP ব্যবহার করতে হবে।

---

## Port

Wrong

```
465
```

TLS এর জন্য

Correct

```
587
```

---

# Development Tip

Email browser-এ দেখতে চাইলে

```python
EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend"
```

Console Output

```
Subject

Verification Link

Body
```

SMTP ছাড়াই Testing করা যায়।

---

# Test Checklist

* ✅ Registration
* ✅ Email Sent
* ✅ Verification Link
* ✅ Login Block Before Verification
* ✅ Login Success After Verification
* ✅ Resend Email

---

# Git Commit

```bash
git add .

git commit -m "feat(email): implement email verification with django-allauth"
```

---

# ⚠️ Senior Developer Notes (Important)

এই commit-এ একটি production issue আছে যা আমরা **Commit 6**-এ solve করব।

`django-allauth` by default HTML page-এ redirect করে, কিন্তু **DRF + React SPA**-এ আমরা চাই:

```
React

↓

User Click Verify Email

↓

Backend Verify

↓

React Success Page
```

এজন্য custom verification flow, frontend callback URL, custom adapters এবং API-friendly response implement করব।

## Commit 6

```bash
feat(profile): implement authenticated user profile APIs
```

এখানে আমরা:

* `/api/auth/user/` customize করব
* Profile Update API
* Custom User Serializer
* Avatar
* Phone
* Partial Update (PATCH)
* Proper Permissions
* React profile integration

সব production-ready ভাবে implement করব।


------


# Commit 7

```bash
feat(password): implement password change and password reset flow
```

---

# 🎯 Goal

এই Commit শেষে আমাদের Authentication System-এ থাকবে—

* ✅ Change Password
* ✅ Forgot Password
* ✅ Reset Password
* ✅ Reset Password Confirm
* ✅ Strong Password Validation
* ✅ JWT Authentication
* ✅ React Ready Password Reset Flow

---

# Final Flow

```text
            User

              │

Forgot Password

              │

Enter Email

              │

Send Reset Email

              │

Click Reset Link

              │

Enter New Password

              │

Password Updated

              │

Login
```

---

# Step 1

`dj-rest-auth` ইতিমধ্যে এই endpoints provide করে।

```
POST

/api/auth/password/change/

POST

/api/auth/password/reset/

POST

/api/auth/password/reset/confirm/
```

আমাদের শুধু configure করতে হবে।

---

# Step 2

settings.py

Password Validators

```python
AUTH_PASSWORD_VALIDATORS = [

    {
        "NAME":
        "django.contrib.auth.password_validation.UserAttributeSimilarityValidator",
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.MinimumLengthValidator",
        "OPTIONS": {
            "min_length": 8,
        }
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.CommonPasswordValidator",
    },

    {
        "NAME":
        "django.contrib.auth.password_validation.NumericPasswordValidator",
    },

]
```

---

## Explain

Password

```
12345678
```

Reject হবে।

Password

```
Atiar@2026
```

Accept হবে।

---

# Step 3

Change Password API

```
POST

/api/auth/password/change/
```

Authorization

```
Bearer ACCESS_TOKEN
```

Body

```json
{
    "new_password1":"NewStrongPassword123",
    "new_password2":"NewStrongPassword123"
}
```

---

Expected

```json
{
    "detail":"New password has been saved."
}
```

---

# Step 4

Wrong Password Example

```json
{
    "new_password1":"123",
    "new_password2":"123"
}
```

Response

```json
{
    "new_password1":[
        "This password is too short."
    ]
}
```

---

# Step 5

Forgot Password API

```
POST

/api/auth/password/reset/
```

Body

```json
{
    "email":"john@gmail.com"
}
```

---

Expected

```json
{
    "detail":"Password reset e-mail has been sent."
}
```

---

# Step 6

Email

User receives

```
Password Reset

↓

Reset Link

↓

UID

↓

TOKEN
```

Example

```
http://localhost:8000/reset-password/

MjA

cp8sj2-2399234...
```

---

# Step 7

Reset Confirm API

```
POST

/api/auth/password/reset/confirm/
```

Body

```json
{
    "uid":"MjA",

    "token":"cp8sj2-2399234",

    "new_password1":"NewPassword123",

    "new_password2":"NewPassword123"
}
```

---

Response

```json
{
    "detail":"Password has been reset successfully."
}
```

---

# Step 8

Login Test

Old Password

```
Wrong
```

New Password

```
Success
```

---

# Step 9

Console Email

Development

settings.py

```python
EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend"
```

Console

```
Password Reset

↓

Reset Link

↓

UID

↓

TOKEN
```

SMTP লাগবে না।

---

# Step 10

React Flow

Forgot Password

```javascript
axios.post(

"/api/auth/password/reset/",

{

email

}

)
```

---

Reset Password

```javascript
axios.post(

"/api/auth/password/reset/confirm/",

{

uid,

token,

new_password1,

new_password2

}

)
```

---

# Step 11

Security

Password Reset Link

```
Single Use
```

Expired

↓

Cannot reuse.

---

# Common Mistakes 🚨

## 1

Password Mismatch

```json
{

"new_password1":"Password123",

"new_password2":"Password456"

}
```

↓

Validation Error

---

## 2

Invalid Token

Response

```json
{

"token":[

"Invalid value"

]

}
```

---

## 3

Expired Token

Response

```json
{

"token":[

"Token expired"

]

}
```

---

## 4

No JWT

Calling

```
/password/change/
```

↓

401 Unauthorized

---

# API Summary

| Endpoint                            | Auth Required | Purpose                 |
| ----------------------------------- | ------------- | ----------------------- |
| `/api/auth/password/change/`        | ✅ Yes         | Change current password |
| `/api/auth/password/reset/`         | ❌ No          | Send reset email        |
| `/api/auth/password/reset/confirm/` | ❌ No          | Set new password        |

---

# Testing Checklist

✅ Change Password

✅ Forgot Password

✅ Reset Email

✅ Reset Confirm

✅ Login with New Password

✅ Invalid Token

✅ Expired Token

---

# Git Commit

```bash
git add .

git commit -m "feat(password): implement password change and password reset flow"
```

---

# 🔥 Senior Django Developer Notes (Very Important)

উপরের flow কাজ করবে, কিন্তু production project-এ আমি আরও কিছু improvement করব:

### 1. Custom Password Reset Email

Default email-এর পরিবর্তে নিজের HTML template ব্যবহার করব।

```
templates/account/email/password_reset.html
```

---

### 2. React Frontend URL

Reset link Django page-এ না গিয়ে React page-এ যাবে।

```
https://frontend.example.com/reset-password?uid=...&token=...
```

---

### 3. Password History

শেষ ৫টি password পুনরায় ব্যবহার করতে না দেওয়া (security enhancement)।

---

### 4. Password Strength Meter

React-এ live strength check (Weak, Medium, Strong) দেখানো।

---

### 5. Brute Force Protection

একই email-এ বারবার password reset request এলে rate limiting (`django-ratelimit` বা `drf-extensions`) ব্যবহার করা।

---

## 📌 Commit 8 Preview

```bash
refactor(auth): customize dj-rest-auth serializers and responses
```

এই Commit-টি খুব গুরুত্বপূর্ণ। এখানে আমরা `dj-rest-auth`-এর built-in serializer override করে production-grade response তৈরি করব।

শিখব:

* Custom `LoginSerializer`
* Custom `JWTSerializer`
* Custom `UserDetailsSerializer`
* Login response-এ অতিরিক্ত user information
* Registration response customize
* Standard API response format
* Production-ready authentication architecture

> **নোট:** এখান থেকেই আমরা `dj-rest-auth`-কে শুধু ব্যবহার করব না, বরং নিজের প্রয়োজন অনুযায়ী customize করতে শিখব—যেটা Senior Django Developer-দের একটি গুরুত্বপূর্ণ skill।


---------

# Commit 8

```bash
refactor(auth): customize dj-rest-auth serializers and authentication responses
```

---

# 🎯 Goal

এই Commit শেষে আমাদের Authentication System হবে production-ready।

আমরা customize করব—

* ✅ Login Response
* ✅ Registration Response
* ✅ User Details Response
* ✅ JWT Response
* ✅ Login Validation
* ✅ Standard API Response Format

> **এই commit খুব গুরুত্বপূর্ণ।**
>
> Senior Django Developer-রা সাধারণত `dj-rest-auth`-এর default serializer ব্যবহার করেন না। তারা নিজের business অনুযায়ী customize করেন।

---

# Final Architecture

```text
                Login Request

                      │

                      ▼

        CustomLoginSerializer

                      │

              Email Validation

                      │

               Authenticate

                      │

                      ▼

          CustomJWTSerializer

                      │

         Access + Refresh Token

                      │

         Custom User Information

                      │

                 JSON Response
```

---

# Step 1

Create folder

```
users/

    serializers/

        __init__.py

        login.py

        register.py

        user.py
```

আগের

```
serializers.py
```

delete করো।

---

# Why?

আগে

```
serializers.py
```

ছোট ছিল।

Production project

↓

২০-৩০ serializer

↓

এক file maintain করা কঠিন।

---

# Step 2

user.py

```python
from django.contrib.auth import get_user_model

from rest_framework import serializers

User = get_user_model()


class UserSerializer(serializers.ModelSerializer):

    full_name = serializers.SerializerMethodField()

    class Meta:

        model = User

        fields = (

            "id",

            "email",

            "first_name",

            "last_name",

            "phone",

            "avatar",

            "full_name",

        )

        read_only_fields = (

            "id",

            "email",

        )

    def get_full_name(self, obj):

        return f"{obj.first_name} {obj.last_name}".strip()
```

---

## Response

```json
{
    "id":1,

    "email":"admin@gmail.com",

    "first_name":"John",

    "last_name":"Doe",

    "full_name":"John Doe",

    "phone":"01711111111",

    "avatar":""
}
```

---

# Step 3

login.py

Create

```python
from dj_rest_auth.serializers import LoginSerializer

from django.contrib.auth import authenticate

from rest_framework import serializers


class CustomLoginSerializer(LoginSerializer):

    username = None

    email = serializers.EmailField()

    def validate(self, attrs):

        email = attrs.get("email")

        password = attrs.get("password")

        user = authenticate(

            request=self.context.get("request"),

            email=email,

            password=password,

        )

        if not user:

            raise serializers.ValidationError(

                "Invalid email or password."

            )

        attrs["user"] = user

        return attrs
```

---

## কেন?

Default Login

↓

অনেক version-এ

```
username
```

support করে।

আমরা চাই

```
email only
```

---

# Step 4

register.py

আগের serializer move করো।

```python
CustomRegisterSerializer
```

এখানে রাখো।

---

# Step 5

**init**.py

```python
from .login import *

from .register import *

from .user import *
```

---

# Step 6

settings.py

আগে

```python
REST_AUTH = {

}
```

Replace

```python
REST_AUTH = {

    "USE_JWT": True,

    "LOGIN_SERIALIZER":

        "users.serializers.CustomLoginSerializer",

    "REGISTER_SERIALIZER":

        "users.serializers.CustomRegisterSerializer",

    "USER_DETAILS_SERIALIZER":

        "users.serializers.UserSerializer",

}
```

---

## Explain

এখন

Login

↓

আমাদের serializer

Registration

↓

আমাদের serializer

User API

↓

আমাদের serializer

---

# Step 7

Customize JWT Response

Create

```
users/jwt.py
```

---

```python
from dj_rest_auth.serializers import JWTSerializer

from .serializers import UserSerializer


class CustomJWTSerializer(

    JWTSerializer

):

    @property

    def data(self):

        data = super().data

        data["user"] = UserSerializer(

            self.user

        ).data

        return data
```

---

Response

```json
{
    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"admin@gmail.com",

        "full_name":"John Doe",

        "phone":"01711111111"

    }
}
```

---

# Step 8

settings.py

Add

```python
REST_AUTH = {

    ...

    "JWT_SERIALIZER":

    "users.jwt.CustomJWTSerializer",

}
```

---

# Step 9

Login Test

POST

```
/api/auth/login/
```

Body

```json
{

    "email":"admin@gmail.com",

    "password":"admin123"

}
```

---

Response

```json
{

    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"admin@gmail.com",

        "first_name":"John",

        "last_name":"Doe",

        "full_name":"John Doe",

        "phone":"017111111"

    }

}
```

---

# Step 10

Current User

GET

```
/api/auth/user/
```

Response

```json
{

    "id":1,

    "email":"admin@gmail.com",

    "first_name":"John",

    "last_name":"Doe",

    "full_name":"John Doe",

    "phone":"017111111"

}
```

---

# Common Mistakes 🚨

## Wrong

```python
fields="__all__"
```

Never expose

```
password

is_staff

is_superuser

groups
```

---

Always

```python
fields=(...)
```

---

## Wrong

```python
authenticate(

username=email

)
```

Custom User

↓

Use

```python
email=email
```

---

## Wrong

Forget

```python
JWT_SERIALIZER
```

↓

Default Response আসবে।

---

## Wrong

SerializerMethodField

```python
return None
```

Always return

```python
str
```

---

# Folder Structure

```
users/

    serializers/

        login.py

        register.py

        user.py

        __init__.py

    jwt.py

    views.py

    urls.py

    managers.py

    models.py
```

---

# API Response (Production)

Login

```json
{

    "success":true,

    "message":"Login successful.",

    "data":{

        "access":"...",

        "refresh":"...",

        "user":{

            "id":1,

            "email":"admin@gmail.com",

            "full_name":"John Doe"

        }

    }

}
```

> **Note:** `dj-rest-auth` default response এভাবে আসে না। যদি এই wrapper (`success`, `message`, `data`) ব্যবহার করতে চাও, তাহলে custom views বা response wrapper লিখতে হবে। শুধু serializer override করলে response structure পুরোপুরি বদলায় না।

---

# Testing Checklist

* ✅ Email Login
* ✅ JWT Response
* ✅ User Serializer
* ✅ Full Name
* ✅ Registration
* ✅ `/api/auth/user/`

---

# Git Commit

```bash
git add .

git commit -m "refactor(auth): customize dj-rest-auth serializers and authentication responses"
```

---

# ⚠️ Senior Django Developer Notes

এই commit-এ একটি গুরুত্বপূর্ণ বিষয় আছে।

`dj-rest-auth`-এর version অনুযায়ী serializer configuration key (`JWT_SERIALIZER`, `LOGIN_SERIALIZER` ইত্যাদি) কিছুটা পরিবর্তিত হতে পারে। এছাড়া `LoginSerializer` override করার সময় default login flow ভেঙে না যায় সেদিকেও খেয়াল রাখতে হবে।

**Commit 9**-এ আমরা official `django-allauth` provider ব্যবহার করে **Google OAuth Login** implement করব। সেখানে manual OAuth code লিখব না; `dj-rest-auth` + `allauth`-এর built-in social authentication flow ব্যবহার করব। এটি production-এ সবচেয়ে বেশি ব্যবহৃত approach।


----

# Commit 9

```bash id="3x8gk1"
feat(google): integrate Google OAuth using django-allauth and dj-rest-auth
```

> 🔥 **Important**
>
> এবার থেকে আমরা **manual OAuth implementation করব না**। Production project-এ `django-allauth` + `dj-rest-auth` যেভাবে Google Login implement করে, ঠিক সেই architecture ব্যবহার করব।

---

# Goal

এই Commit শেষে থাকবে

* ✅ Google OAuth Login
* ✅ Google SocialApp
* ✅ Google Provider
* ✅ JWT Return
* ✅ Existing Account Linking
* ✅ React Compatible Flow

---

# Final Flow

```text
React

    │

Google Sign In

    │

Google Authorization Code

    │

POST /api/auth/google/

    │

GoogleOAuth2Adapter

    │

django-allauth

    │

User

    │

SimpleJWT

    │

Access + Refresh
```

---

# Step 1

Install

```bash
pip install google-auth
```

(Optional, future verification-এর জন্য)

---

# Step 2

settings.py

Add

```python
INSTALLED_APPS = [

    ...

    "allauth.socialaccount.providers.google",

]
```

---

## কেন?

Provider register হবে।

Without this

```text
Provider google not found
```

---

# Step 3

Google Cloud Console

Create Project

↓

Enable

```text
Google Identity API
```

---

Create

```text
OAuth 2.0 Client ID
```

---

Authorized JavaScript Origins

```text
http://localhost:3000
```

---

Authorized Redirect URI

```text
http://localhost:3000/auth/google/callback
```

React callback দিবো।

---

# Step 4

Django Admin

Login

↓

Social Applications

↓

Add

---

Provider

```text
Google
```

---

Name

```text
Google Login
```

---

Client ID

```text
xxxxxxxx.apps.googleusercontent.com
```

---

Secret

```text
GOCSPX-xxxxxxxx
```

---

Sites

```text
example.com
```

Add

↓

Save

---

# Step 5

Create

```text
users/social_views.py
```

---

```python
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter

from dj_rest_auth.registration.views import SocialLoginView


class GoogleLoginView(

    SocialLoginView

):

    adapter_class = GoogleOAuth2Adapter
```

---

## Explain

GoogleOAuth2Adapter

↓

Talks with Google

↓

Gets User

↓

Creates User

↓

Returns JWT

---

# Step 6

users/urls.py

```python
from django.urls import path

from .social_views import GoogleLoginView

urlpatterns += [

    path(

        "google/",

        GoogleLoginView.as_view(),

        name="google_login",

    ),

]
```

---

Endpoint

```text
POST

/api/users/google/
```

---

# Step 7

React

User Click

```text
Continue with Google
```

React SDK

↓

Gets

```text
access_token
```

---

# Step 8

POST

```text
/api/users/google/
```

Body

```json
{
    "access_token":"GOOGLE_ACCESS_TOKEN"
}
```

---

# Step 9

Backend

Google verifies

↓

Gets

```text
email

name

picture
```

---

If

Email exists

↓

Login

Else

↓

Create User

---

# Step 10

JWT Response

```json
{

    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"john@gmail.com",

        "full_name":"John Doe"

    }

}
```

---

# Database

New Table

Already exists

```text
socialaccount_socialaccount

socialaccount_socialtoken

socialaccount_socialapp
```

---

Example

```text
provider

google

uid

1092349238423

user_id

1
```

---

# Account Linking

Suppose

User already exists

```text
john@gmail.com
```

Google returns

```text
john@gmail.com
```

↓

No duplicate user

↓

Same account linked

---

# React Integration

Google Login

```javascript
const credential = googleResponse.access_token;

await axios.post(

"/api/users/google/",

{

access_token:credential

}

);
```

---

# Common Errors

## Error 1

```text
SocialApp matching query does not exist
```

Reason

No SocialApp in Admin.

---

## Error 2

```text
Provider not found
```

Forgot

```python
allauth.socialaccount.providers.google
```

---

## Error 3

```text
redirect_uri_mismatch
```

React URI

≠

Google Console URI

---

## Error 4

```text
invalid_client
```

Wrong Client ID

---

## Error 5

```text
invalid_grant
```

Expired Access Token

---

# Testing Checklist

✅ Google Login

✅ Existing User

✅ New User

✅ JWT

✅ SocialAccount Created

---

# Git Commit

```bash
git add .

git commit -m "feat(google): integrate Google OAuth using django-allauth"
```

---

# ⚠️ Senior Django Developer Review (Very Important)

উপরের implementation **conceptually সঠিক**, কিন্তু production-এ **একটি জিনিস পরিবর্তন করা উচিত**।

`GoogleLoginView` শুধু `adapter_class` দিলেই সব ক্ষেত্রে কাজ করবে না। `dj-rest-auth`-এর বর্তমান version অনুযায়ী সাধারণত `client_class` এবং `callback_url`-ও configure করতে হয়, এবং React/Web SPA-এর ক্ষেত্রে Google Identity Services থেকে **authorization code** নাকি **access token** আসছে তার উপর view পরিবর্তিত হয়।

Production architecture সাধারণত হয়:

```text
React (Google Identity Services)

        │

 Authorization Code

        │

POST /api/auth/google/

        │

GoogleLoginView

        │

GoogleOAuth2Adapter

        │

OAuth2Client

        │

django-allauth

        │

JWT
```

**Commit 10**-এ আমরা এই production-ready flow implement করব, যেখানে React, `OAuth2Client`, callback URL, এবং official `dj-rest-auth` social login configuration সম্পূর্ণভাবে configure করব। তারপর GitHub OAuth একই pattern-এ করা হবে।


-------
# Commit 10

```bash
feat(auth): implement production-ready Google OAuth with React and OAuth2Client
```

> 🔥 **এই Commit-টাই সবচেয়ে গুরুত্বপূর্ণ।**
>
> Commit 9-এ আমরা basic Google provider setup করেছি। কিন্তু production project-এ Google OAuth এভাবে implement করা হয় না।
>
> এই commit-এ আমরা **official dj-rest-auth + django-allauth flow** implement করব।

---

# Final Architecture

```text
React

     │

Google Identity Services

     │

Authorization Code

     │

POST /api/auth/google/

     │

GoogleLoginView

     │

OAuth2Client

     │

GoogleOAuth2Adapter

     │

django-allauth

     │

SocialAccount

     │

JWT

     │

React
```

---

# Step 1

settings.py

Install provider

```python
INSTALLED_APPS = [

    ...

    "allauth.socialaccount.providers.google",

]
```

---

# Step 2

.env

```env
GOOGLE_CLIENT_ID=xxxxxxxx.apps.googleusercontent.com

GOOGLE_CLIENT_SECRET=GOCSPX-xxxxxxxx

GOOGLE_CALLBACK_URL=http://localhost:3000/auth/google/callback
```

---

settings.py

```python
from decouple import config

GOOGLE_CLIENT_ID = config(
    "GOOGLE_CLIENT_ID"
)

GOOGLE_CLIENT_SECRET = config(
    "GOOGLE_CLIENT_SECRET"
)

GOOGLE_CALLBACK_URL = config(
    "GOOGLE_CALLBACK_URL"
)
```

---

# Step 3

Google Cloud Console

Authorized Origins

```text
http://localhost:3000
```

Authorized Redirect URI

```text
http://localhost:3000/auth/google/callback
```

---

# Step 4

social_views.py

Replace previous code

```python
from allauth.socialaccount.providers.google.views import (
    GoogleOAuth2Adapter,
)

from allauth.socialaccount.providers.oauth2.client import (
    OAuth2Client,
)

from django.conf import settings

from dj_rest_auth.registration.views import (
    SocialLoginView,
)


class GoogleLoginView(
    SocialLoginView
):

    adapter_class = GoogleOAuth2Adapter

    client_class = OAuth2Client

    callback_url = (
        settings.GOOGLE_CALLBACK_URL
    )
```

---

## Explain

### adapter_class

Talks to Google

↓

Gets User Information

---

### client_class

Handles

```text
Authorization Code

↓

Exchange

↓

Access Token
```

Without it

↓

Many OAuth flows fail.

---

### callback_url

Must exactly match

```text
Google Console

↓

Redirect URI
```

Otherwise

```text
redirect_uri_mismatch
```

---

# Step 5

users/urls.py

```python
from django.urls import path

from .social_views import (
    GoogleLoginView,
)

urlpatterns = [

    path(

        "google/",

        GoogleLoginView.as_view(),

        name="google_login",

    ),

]
```

---

Endpoint

```text
POST

/api/users/google/
```

---

# Step 6

Admin

Create

SocialApp

Provider

```text
Google
```

Client ID

↓

Paste

Client Secret

↓

Paste

Sites

↓

example.com

Save

---

# Step 7

React

Install

```bash
npm install @react-oauth/google
```

---

Wrap

```jsx
<GoogleOAuthProvider

clientId={CLIENT_ID}

>

<App/>

</GoogleOAuthProvider>
```

---

Button

```jsx
<GoogleLogin

onSuccess={handleGoogle}

/>
```

---

# Step 8

React Success

```javascript
const handleGoogle = async (
    credentialResponse
) => {

    await axios.post(

        "/api/users/google/",

        {

            access_token:
                credentialResponse.access_token

        }

    )

}
```

---

# Step 9

Backend Flow

```text
Access Token

↓

Google Verify

↓

Get User

↓

Create SocialAccount

↓

Create User

↓

JWT

↓

Return
```

---

# Step 10

Existing User

Database

Already

```text
john@gmail.com
```

Google returns

```text
john@gmail.com
```

↓

No duplicate

↓

SocialAccount linked

---

# Step 11

JWT Response

```json
{

    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"john@gmail.com",

        "full_name":"John Doe"

    }

}
```

---

# Database

Tables

```text
users_user

socialaccount_socialaccount

socialaccount_socialtoken

socialaccount_socialapp
```

---

Example

```text
provider

google

uid

109238423423

user

1
```

---

# Common Errors

---

## redirect_uri_mismatch

Reason

Google Console URI

≠

Backend callback_url

---

## invalid_client

Wrong Client ID

---

## invalid_grant

Expired Code

---

## SocialApp matching query

Forgot

```text
Admin

↓

SocialApp
```

---

## Provider not found

Forgot

```python
"allauth.socialaccount.providers.google"
```

---

# Testing

## Login

```text
React

↓

Google Popup

↓

Select Account

↓

Backend

↓

JWT
```

---

## Existing User

Same Email

↓

No duplicate

---

## New User

↓

User Created

↓

JWT Returned

---

# Production Folder Structure

```text
users/

    social_views.py

    serializers/

    views.py

    urls.py

config/

settings.py

.env
```

---

# Git Commit

```bash
git add .

git commit -m "feat(auth): implement production-ready Google OAuth flow"
```

---

# 🔥 Senior Django Developer Review (Important Correction)

উপরের flow **90% সঠিক**, কিন্তু বর্তমান **Google Identity Services (GIS)**-এ একটি গুরুত্বপূর্ণ পরিবর্তন আছে।

বর্তমানে `@react-oauth/google`-এর **`GoogleLogin` component** সাধারণত **ID Token (`credential`)** return করে, **`access_token` নয়**। আবার `useGoogleLogin()` hook ব্যবহার করলে OAuth flow অনুযায়ী `access_token` বা authorization code পাওয়া যায়।

Production-এ দুটি official approach আছে:

### Option 1 (সবচেয়ে বেশি ব্যবহৃত)

```text
React

↓

GoogleLogin

↓

ID Token (credential)

↓

Backend verifies ID Token

↓

User Login

↓

JWT
```

### Option 2 (OAuth Authorization Code Flow)

```text
React

↓

Authorization Code

↓

Backend

↓

OAuth2Client

↓

Google

↓

Access Token

↓

User Info

↓

JWT
```

**React SPA-এর জন্য Option 1 (ID Token verification)** এখন বেশি জনপ্রিয় এবং নিরাপদ, আর **server-side OAuth integration**-এর জন্য Authorization Code Flow ব্যবহৃত হয়।

---

## Commit 11 Preview

```bash
feat(github): integrate GitHub OAuth using django-allauth
```

এখানে আমরা একই production architecture অনুসরণ করে:

* GitHub OAuth App
* SocialApp
* GitHub Adapter
* React GitHub Login
* JWT Response
* Existing Account Linking
* Production Configuration

সব step-by-step implement করব।

# Commit 11

```bash
feat(github): integrate GitHub OAuth using django-allauth
```

> 🔥 এই Commit শেষে আমাদের Authentication System-এ থাকবে
>
> * ✅ GitHub OAuth Login
> * ✅ GitHub SocialApp
> * ✅ Existing Account Linking
> * ✅ JWT Authentication
> * ✅ React Integration
> * ✅ Production Ready GitHub Login

---

# Final Architecture

```text
React

   │

GitHub Login Button

   │

GitHub OAuth

   │

Authorization Code

   │

POST /api/auth/github/

   │

GithubOAuth2Adapter

   │

OAuth2Client

   │

django-allauth

   │

SocialAccount

   │

JWT

   │

React
```

---

# Step 1

## Install Provider

settings.py

```python
INSTALLED_APPS = [

    ...

    "allauth.socialaccount.providers.github",

]
```

---

## Explain

এটা GitHub Provider Register করবে।

Without this

```
Provider github not found
```

---

# Step 2

## GitHub OAuth App

GitHub

↓

Settings

↓

Developer Settings

↓

OAuth Apps

↓

New OAuth App

---

Application Name

```
DRF Auth Mastery
```

Homepage

```
http://localhost:3000
```

Authorization Callback URL

```
http://localhost:3000/auth/github/callback
```

---

After Save

You'll get

```
Client ID

Client Secret
```

---

# Step 3

.env

```env
GITHUB_CLIENT_ID=xxxxxxxx

GITHUB_CLIENT_SECRET=xxxxxxxx

GITHUB_CALLBACK_URL=http://localhost:3000/auth/github/callback
```

---

settings.py

```python
from decouple import config

GITHUB_CLIENT_ID = config(
    "GITHUB_CLIENT_ID"
)

GITHUB_CLIENT_SECRET = config(
    "GITHUB_CLIENT_SECRET"
)

GITHUB_CALLBACK_URL = config(
    "GITHUB_CALLBACK_URL"
)
```

---

# Step 4

Admin

Login

↓

Social Applications

↓

Add

Provider

```
GitHub
```

Name

```
GitHub Login
```

Client ID

↓

Paste

Secret

↓

Paste

Sites

↓

example.com

Save

---

# Step 5

Create

```
users/social_views.py
```

Add

```python
from allauth.socialaccount.providers.github.views import (
    GitHubOAuth2Adapter,
)

from allauth.socialaccount.providers.oauth2.client import (
    OAuth2Client,
)

from django.conf import settings

from dj_rest_auth.registration.views import (
    SocialLoginView,
)


class GitHubLoginView(
    SocialLoginView
):

    adapter_class = (
        GitHubOAuth2Adapter
    )

    client_class = OAuth2Client

    callback_url = (
        settings.GITHUB_CALLBACK_URL
    )
```

---

## Explain

GitHubOAuth2Adapter

↓

Connects to GitHub

↓

Gets User

↓

Creates SocialAccount

↓

Returns JWT

---

# Step 6

users/urls.py

```python
from django.urls import path

from .social_views import (
    GoogleLoginView,
    GitHubLoginView,
)

urlpatterns = [

    path(

        "google/",

        GoogleLoginView.as_view(),

        name="google_login",

    ),

    path(

        "github/",

        GitHubLoginView.as_view(),

        name="github_login",

    ),

]
```

---

Endpoint

```
POST

/api/users/github/
```

---

# Step 7

React

Install package

```bash
npm install react-github-login
```

অথবা

GitHub OAuth Redirect Flow ব্যবহার করতে পারো।

---

Redirect User

```
https://github.com/login/oauth/authorize
```

Parameters

```
client_id

redirect_uri

scope=user:email
```

---

GitHub returns

```
Authorization Code
```

---

# Step 8

React Callback

```javascript
const code =
    searchParams.get("code");

await axios.post(

"/api/users/github/",

{

    code

}

)
```

---

# Step 9

Backend Flow

```
Authorization Code

↓

GitHub

↓

Access Token

↓

User Information

↓

Email

↓

Create User

↓

JWT
```

---

# Step 10

JWT Response

```json
{

    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"atiar@gmail.com",

        "full_name":"Md Atiar Rahman"

    }

}
```

---

# Step 11

Existing User

Database

Already

```
atiar@gmail.com
```

GitHub returns

```
atiar@gmail.com
```

↓

Don't create

```
User #2
```

Instead

↓

Link

```
SocialAccount
```

---

# Database

Tables

```
users_user

socialaccount_socialaccount

socialaccount_socialtoken

socialaccount_socialapp
```

Example

```
provider

github

uid

83924234

user_id

1
```

---

# React Protected Login

```javascript
localStorage.setItem(

"access",

response.data.access

)

localStorage.setItem(

"refresh",

response.data.refresh
)
```

---

# Common Errors

## Error

```
Provider github not found
```

Reason

Forgot

```python
"allauth.socialaccount.providers.github"
```

---

## Error

```
SocialApp matching query does not exist
```

Forgot

Admin

↓

SocialApp

---

## Error

```
redirect_uri_mismatch
```

GitHub Callback

≠

React Callback

---

## Error

```
bad_verification_code
```

Authorization Code

Expired

---

## Error

```
No primary email found
```

GitHub Email

Private

Solution

GitHub OAuth Scope

```
user:email
```

---

# Testing Checklist

✅ GitHub Login

✅ Existing User

✅ New User

✅ JWT Returned

✅ SocialAccount Created

---

# Folder Structure

```text
users/

    social_views.py

    serializers/

    urls.py

    views.py

config/

settings.py

.env
```

---

# Git Commit

```bash
git add .

git commit -m "feat(github): integrate GitHub OAuth using django-allauth"
```

---

# 🔥 Senior Django Developer Notes (Very Important)

এখানে একটি **গুরুত্বপূর্ণ বাস্তব বিষয়** আছে।

`dj-rest-auth` **GitHub provider** Google-এর মতো সরাসরি `code` accept করে login করিয়ে দেয় না সব configuration-এ। অনেক ক্ষেত্রে `GitHubOAuth2Adapter`-এর পাশাপাশি custom callback flow বা frontend থেকে OAuth code exchange configure করতে হয়।

Production-এ আমি সাধারণত এই architecture ব্যবহার করি:

```text
React

↓

GitHub OAuth (Authorization Code Flow)

↓

Backend Callback

↓

GitHub Token Exchange

↓

django-allauth SocialLogin

↓

SimpleJWT

↓

React
```

এতে security বেশি ভালো হয় এবং React client secret expose করতে হয় না।

---

# Commit 12 Preview

```bash
feat(facebook): integrate Facebook OAuth using django-allauth
```

এখানে আমরা production-ready Facebook Login implement করব, যেখানে শিখব:

* Facebook Developer App
* Facebook SocialApp
* OAuth Flow
* Account Linking
* JWT Authentication
* React Facebook Login
* Common Facebook OAuth Errors
* Production Configuration
# Commit 12

```bash
feat(facebook): integrate Facebook OAuth using django-allauth
```

> 🎯 **Goal**
>
> এই commit শেষে project-এ থাকবে:
>
> * ✅ Facebook Login
> * ✅ Facebook Developer App
> * ✅ Facebook SocialApp
> * ✅ JWT Authentication
> * ✅ Existing Account Linking
> * ✅ React Integration
> * ✅ Production Ready Configuration

---

# Final Architecture

```text
React

   │

Facebook Login

   │

Facebook OAuth

   │

Access Token

   │

POST /api/auth/facebook/

   │

FacebookOAuth2Adapter

   │

django-allauth

   │

SocialAccount

   │

JWT

   │

React
```

---

# Step 1

## Enable Facebook Provider

settings.py

```python
INSTALLED_APPS = [

    ...

    "allauth.socialaccount.providers.facebook",

]
```

---

# Step 2

## Create Facebook App

Go to

```
https://developers.facebook.com/
```

Create App

↓

Choose

```
Consumer
```

↓

Add Product

```
Facebook Login
```

---

App Settings

```
App Name

DRF Auth Mastery
```

---

Copy

```
App ID

App Secret
```

---

# Step 3

Configure OAuth

Facebook Login

↓

Settings

Valid OAuth Redirect URI

```
http://localhost:3000/auth/facebook/callback
```

Production

```
https://yourdomain.com/auth/facebook/callback
```

---

# Step 4

.env

```env
FACEBOOK_APP_ID=xxxxxxxx

FACEBOOK_APP_SECRET=xxxxxxxx

FACEBOOK_CALLBACK_URL=http://localhost:3000/auth/facebook/callback
```

---

settings.py

```python
FACEBOOK_APP_ID = config(
    "FACEBOOK_APP_ID"
)

FACEBOOK_APP_SECRET = config(
    "FACEBOOK_APP_SECRET"
)

FACEBOOK_CALLBACK_URL = config(
    "FACEBOOK_CALLBACK_URL"
)
```

---

# Step 5

SocialApp

Admin

↓

Social Applications

↓

Add

Provider

```
Facebook
```

Name

```
Facebook Login
```

Client ID

↓

App ID

Secret

↓

App Secret

Sites

↓

example.com

Save

---

# Step 6

users/social_views.py

```python
from allauth.socialaccount.providers.facebook.views import (
    FacebookOAuth2Adapter,
)

from dj_rest_auth.registration.views import (
    SocialLoginView,
)


class FacebookLoginView(
    SocialLoginView
):

    adapter_class = (
        FacebookOAuth2Adapter
    )
```

> **নোট:** Facebook provider সাধারণত **access token** ব্যবহার করে। Google-এর মতো `OAuth2Client` সব ক্ষেত্রে প্রয়োজন হয় না।

---

# Step 7

users/urls.py

```python
from django.urls import path

from .social_views import (

    GoogleLoginView,

    GitHubLoginView,

    FacebookLoginView,

)

urlpatterns = [

    path(

        "google/",

        GoogleLoginView.as_view(),

    ),

    path(

        "github/",

        GitHubLoginView.as_view(),

    ),

    path(

        "facebook/",

        FacebookLoginView.as_view(),

    ),

]
```

---

Endpoint

```
POST

/api/users/facebook/
```

---

# Step 8

React

Install

```bash
npm install react-facebook-login
```

---

Example

```jsx
<FacebookLogin

    appId={APP_ID}

    callback={handleFacebook}

/>
```

---

# Step 9

React

```javascript
const handleFacebook = async (

    response

) => {

    await axios.post(

        "/api/users/facebook/",

        {

            access_token:

                response.accessToken

        }

    );

};
```

---

# Step 10

Backend Flow

```text
Access Token

↓

Facebook Verify

↓

User Info

↓

Email

↓

Create User

↓

Create SocialAccount

↓

JWT
```

---

# Step 11

JWT Response

```json
{

    "access":"eyJhbGc...",

    "refresh":"eyJhbGc...",

    "user":{

        "id":1,

        "email":"atiar@gmail.com",

        "full_name":"Md Atiar Rahman"

    }

}
```

---

# Database

```
users_user

socialaccount_socialaccount

socialaccount_socialtoken

socialaccount_socialapp
```

Example

```
provider

facebook

uid

100083423423

user_id

1
```

---

# Existing User

Suppose

Database

```
atiar@gmail.com
```

Facebook returns

```
atiar@gmail.com
```

↓

No duplicate user

↓

Link existing account

---

# Common Errors

## Error

```
Provider facebook not found
```

Forgot

```python
"allauth.socialaccount.providers.facebook"
```

---

## Error

```
SocialApp matching query does not exist
```

Forgot

```
Admin

↓

SocialApp
```

---

## Error

```
Invalid OAuth access token
```

Expired Token

---

## Error

```
App not setup
```

Facebook App

Not Live

---

## Error

```
Email permission denied
```

Need permission

```
email
```

in Facebook Login configuration.

---

# React Authentication Flow

```text
Facebook Login

↓

Access Token

↓

POST Backend

↓

JWT

↓

Save

↓

Protected Route
```

---

# Testing Checklist

* ✅ Facebook Login
* ✅ Existing User
* ✅ New User
* ✅ JWT Response
* ✅ SocialAccount Created
* ✅ Account Linking

---

# Folder Structure

```text
users/

    social_views.py

    serializers/

    urls.py

config/

settings.py

.env
```

---

# Git Commit

```bash
git add .

git commit -m "feat(facebook): integrate Facebook OAuth using django-allauth"
```

---

# 🔥 Senior Django Developer Review (Reality Check)

এখন পর্যন্ত (Commit 1–12) আমরা Google, GitHub এবং Facebook integration দেখেছি। কিন্তু **production project-এ আমি একটি বড় refactor করব**।

বর্তমানে `social_views.py`-তে তিনটি আলাদা view আছে:

```python
GoogleLoginView

GitHubLoginView

FacebookLoginView
```

Provider বাড়লে (`Apple`, `Microsoft`, `LinkedIn`, `Discord`) file বড় হয়ে যাবে।

**Senior architecture** হবে:

```text
users/

    social/

        __init__.py

        google.py

        github.py

        facebook.py

        base.py

        urls.py
```

প্রতিটি provider আলাদা module-এ থাকবে, maintain করা সহজ হবে এবং testing-ও সহজ হবে।

---

# 🚀 Commit 13 Preview

```bash
feat(security): implement production security settings and authentication hardening
```

এখানে আমরা production-level security implement করব:

* Secure Cookies
* HTTPOnly Cookies
* SameSite Policy
* CORS Configuration
* CSRF Protection
* HTTPS Settings
* Rate Limiting
* Login Attempt Protection
* Trusted Origins
* Environment-based Settings

এটি authentication system-কে **production deployment-এর জন্য প্রস্তুত** করবে।


# Commit 13

```bash
feat(security): harden authentication security for production
```

> ⚠️ **এটাই authentication system-এর সবচেয়ে গুরুত্বপূর্ণ commit-গুলোর একটি।**
>
> Google/Facebook/GitHub Login implement করাই যথেষ্ট নয়। Production-এ security configuration ভুল হলে পুরো authentication system compromise হতে পারে।

---

# 🎯 Goal

এই Commit শেষে project-এ থাকবে

* ✅ HTTPS Ready
* ✅ Secure Cookies
* ✅ HTTPOnly Refresh Token
* ✅ CORS Configuration
* ✅ CSRF Protection
* ✅ Trusted Origins
* ✅ Security Headers
* ✅ Environment-based Settings
* ✅ Production Ready Authentication

---

# Final Security Architecture

```text
Internet

      │

HTTPS

      │

Nginx

      │

Gunicorn

      │

Django

      │

Security Middleware

      │

JWT Authentication

      │

Protected API
```

---

# Step 1

## Install

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

Middleware

```python
MIDDLEWARE = [

    "corsheaders.middleware.CorsMiddleware",

    "django.middleware.security.SecurityMiddleware",

    ...

]
```

> `CorsMiddleware` সাধারণত `SecurityMiddleware`-এর আগে বা একদম শুরুতে রাখা হয়।

---

# Step 3

Development

```python
CORS_ALLOWED_ORIGINS = [

    "http://localhost:3000",

]
```

Production

```python
CORS_ALLOWED_ORIGINS = [

    "https://app.example.com",

]
```

❌ Never

```python
CORS_ALLOW_ALL_ORIGINS = True
```

Production-এ ব্যবহার করবে না।

---

# Step 4

CSRF

```python
CSRF_TRUSTED_ORIGINS = [

    "https://app.example.com",

]
```

Development

```python
CSRF_TRUSTED_ORIGINS = [

    "http://localhost:3000",

]
```

---

# Step 5

HTTPS

```python
SECURE_SSL_REDIRECT = True

SESSION_COOKIE_SECURE = True

CSRF_COOKIE_SECURE = True
```

Meaning

```text
Only HTTPS

↓

Cookies Sent
```

---

# Step 6

Security Headers

```python
SECURE_BROWSER_XSS_FILTER = True

SECURE_CONTENT_TYPE_NOSNIFF = True

X_FRAME_OPTIONS = "DENY"
```

---

## Prevent

```
XSS

Clickjacking

MIME attacks
```

---

# Step 7

HSTS

```python
SECURE_HSTS_SECONDS = 31536000

SECURE_HSTS_INCLUDE_SUBDOMAINS = True

SECURE_HSTS_PRELOAD = True
```

Browser

↓

Always

↓

HTTPS

---

# Step 8

JWT

settings.py

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

}
```

Install blacklist support

```bash
pip install djangorestframework-simplejwt
```

Add app

```python
INSTALLED_APPS += [

    "rest_framework_simplejwt.token_blacklist",

]
```

Run

```bash
python manage.py migrate
```

---

# Step 9

Cookie Security

If using Cookies

```python
SESSION_COOKIE_HTTPONLY = True

CSRF_COOKIE_HTTPONLY = False
```

Why?

JavaScript

↓

Cannot access

```text
Session Cookie
```

---

# Step 10

Environment

Development

```python
DEBUG = True
```

Production

```python
DEBUG = False
```

Never deploy

```python
DEBUG = True
```

---

# Step 11

ALLOWED_HOSTS

```python
ALLOWED_HOSTS = [

    "example.com",

    "www.example.com",

]
```

Never

```python
ALLOWED_HOSTS = ["*"]
```

Production-এ ব্যবহার করবে না।

---

# Step 12

Rate Limiting

Install

```bash
pip install django-ratelimit
```

Example

```python
from django_ratelimit.decorators import ratelimit

@ratelimit(
    key="ip",
    rate="5/m",
    block=True,
)
def login(request):
    ...
```

Meaning

```
5 login attempts

↓

1 minute

↓

Block
```

---

# Step 13

Logging

```python
LOGGING = {

    "version":1,

}
```

Log

```
Login

Logout

Password Reset

OAuth Login

Authentication Errors
```

---

# Step 14

Secrets

Never

```python
SECRET_KEY = "abcd"
```

Use

```python
SECRET_KEY = config(
    "SECRET_KEY"
)
```

---

# Step 15

Testing

### HTTP

```
http://example.com
```

↓

Redirect

↓

HTTPS

---

### JWT

Expired Token

↓

401

---

### Refresh

Old Refresh Token

↓

Invalid

Because

```
Rotation Enabled
```

---

# Production Folder

```
config/

    settings/

        base.py

        development.py

        production.py

.env

.env.production
```

---

# Common Security Mistakes 🚨

## ❌

```python
DEBUG = True
```

Production

---

## ❌

```python
ALLOWED_HOSTS=["*"]
```

---

## ❌

```python
CORS_ALLOW_ALL_ORIGINS=True
```

---

## ❌

Store JWT

```
localStorage
```

Better

```
HTTPOnly Cookie
```

---

## ❌

Long Access Token

```
24 Hours
```

Better

```
10-15 Minutes
```

---

## ❌

SECRET_KEY

GitHub Push

---

# Testing Checklist

* ✅ HTTPS
* ✅ CORS
* ✅ CSRF
* ✅ Secure Cookies
* ✅ JWT Rotation
* ✅ Refresh Blacklist
* ✅ Trusted Origins
* ✅ Rate Limiting

---

# Git Commit

```bash
git add .

git commit -m "feat(security): harden authentication security for production"
```

---

# 🔥 Senior Django Developer Review (Important Corrections)

এই commit-এর বেশিরভাগ ধারণা ঠিক আছে, তবে কয়েকটি বাস্তব বিষয় মনে রাখবে:

1. **`SECURE_BROWSER_XSS_FILTER` আধুনিক Django-তে deprecated**। এটি ব্যবহার না করাই ভালো।
2. `django-ratelimit` login view-এ সরাসরি decorate করা সবসময় কাজ নাও করতে পারে, বিশেষ করে `dj-rest-auth`-এর built-in class-based view ব্যবহার করলে। সেক্ষেত্রে custom view বা middleware-based rate limiting প্রয়োজন।
3. যদি JWT **Authorization Header**-এ পাঠাও, তাহলে CSRF protection সাধারণত সেই header-এর জন্য প্রযোজ্য নয়। কিন্তু **HTTPOnly Cookie**-তে JWT রাখলে CSRF strategy আলাদা করে implement করতে হবে।
4. `djangorestframework-simplejwt` সম্ভবত আগেই install করা আছে; এখানে মূল কাজ হলো `token_blacklist` app enable করা এবং migration চালানো।

---

# 🚀 Commit 14 Preview

```bash
feat(tokens): implement JWT refresh token rotation, logout, and token blacklist
```

এখানে আমরা production-ready token lifecycle implement করব:

* Refresh Token Rotation
* Logout API
* Token Blacklisting
* Logout From All Devices
* Access Token Renewal
* Refresh Token Security
* Multi-device Authentication Strategy

এটি authentication system-এর শেষ বড় security layer হবে।


# Commit 14

```bash
feat(tokens): implement JWT refresh token rotation, logout, and token blacklist
```

> 🎯 **Goal**
>
> এই commit শেষে authentication system-এ থাকবে:
>
> * ✅ Refresh Token Rotation
> * ✅ Token Blacklist
> * ✅ Secure Logout
> * ✅ Logout All Devices
> * ✅ Refresh Token Endpoint
> * ✅ JWT Lifecycle Management
> * ✅ Production-ready Token Security

---

# Final Flow

```text
             Login

               │

       Access + Refresh

               │

        Access Expires

               │

POST /api/auth/token/refresh/

               │

New Access Token

               │

Old Refresh Blacklisted

               │

Continue Working
```

---

# Step 1

## Enable Token Blacklist

settings.py

```python
INSTALLED_APPS += [

    "rest_framework_simplejwt.token_blacklist",

]
```

Run

```bash
python manage.py migrate
```

---

# Step 2

settings.py

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(
        minutes=15
    ),

    "REFRESH_TOKEN_LIFETIME": timedelta(
        days=7
    ),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "UPDATE_LAST_LOGIN": True,

}
```

---

## Explain

Before

```text
Refresh Token

↓

Forever Valid
```

After

```text
Refresh Token

↓

Used Once

↓

Blacklisted

↓

New Refresh Issued
```

---

# Step 3

Refresh Endpoint

Already provided by

```text
dj-rest-auth
```

Endpoint

```http
POST

/api/auth/token/refresh/
```

Body

```json
{

    "refresh":"REFRESH_TOKEN"

}
```

---

Response

```json
{

    "access":"NEW_ACCESS",

    "refresh":"NEW_REFRESH"

}
```

---

# Step 4

Database

New Tables

```text
token_blacklist_outstandingtoken

token_blacklist_blacklistedtoken
```

Example

```text
OutstandingToken

↓

Refresh Token

↓

Expires

↓

User
```

---

# Step 5

Token Rotation

First Request

```json
{

"refresh":"TOKEN_1"

}
```

↓

Response

```text
TOKEN_2
```

TOKEN_1

↓

Blacklisted

---

Second Request

Using

```text
TOKEN_1
```

↓

Response

```json
{

"detail":"Token is blacklisted"

}
```

---

# Step 6

Logout API

Create

```text
users/views/logout.py
```

---

```python
from rest_framework.views import APIView

from rest_framework.permissions import (
    IsAuthenticated,
)

from rest_framework.response import (
    Response,
)

from rest_framework import status

from rest_framework_simplejwt.tokens import (
    RefreshToken,
)


class LogoutAPIView(APIView):

    permission_classes = (
        IsAuthenticated,
    )

    def post(self, request):

        refresh = request.data.get(
            "refresh"
        )

        token = RefreshToken(refresh)

        token.blacklist()

        return Response(

            {

                "detail":
                "Logout successful."

            },

            status=status.HTTP_205_RESET_CONTENT,

        )
```

---

# Step 7

urls.py

```python
from django.urls import path

from .views.logout import (
    LogoutAPIView,
)

urlpatterns += [

    path(

        "logout/",

        LogoutAPIView.as_view(),

        name="logout",

    ),

]
```

---

Endpoint

```http
POST

/api/users/logout/
```

---

Body

```json
{

"refresh":"REFRESH_TOKEN"

}
```

---

Response

```json
{

"detail":"Logout successful."

}
```

---

# Step 8

React Logout

```javascript
await axios.post(

"/api/users/logout/",

{

refresh

}

);

localStorage.removeItem(
    "access"
);

localStorage.removeItem(
    "refresh"
);
```

---

# Step 9

Logout Flow

```text
Refresh Token

↓

Blacklist

↓

Delete Local Token

↓

Redirect Login
```

---

# Step 10

Logout All Devices

Example

```python
from rest_framework_simplejwt.token_blacklist.models import (
    OutstandingToken,
    BlacklistedToken,
)

tokens = OutstandingToken.objects.filter(
    user=request.user
)

for token in tokens:

    BlacklistedToken.objects.get_or_create(
        token=token
    )
```

Meaning

```text
Phone

×

Laptop

×

Tablet

×

Logged Out
```

---

# Step 11

Protected API

Expired Access

↓

401

React

↓

Automatically

```http
POST

/api/auth/token/refresh/
```

↓

Retry Previous Request

---

# React Axios Interceptor

```javascript
axios.interceptors.response.use(

response => response,

async error => {

if(error.response.status===401){

// refresh token

}

}
);
```

---

# Step 12

Common Errors

---

Expired Refresh

```json
{

"detail":"Token is invalid"

}
```

---

Blacklisted

```json
{

"detail":"Token is blacklisted"

}
```

---

Missing Refresh

```json
{

"refresh":[

"This field is required."

]

}
```

---

# Database

```text
OutstandingToken

↓

Every Refresh Token

---------------------

BlacklistedToken

↓

Invalid Refresh Tokens
```

---

# Testing Checklist

✅ Login

✅ Refresh Token

✅ Rotation

✅ Logout

✅ Logout All Devices

✅ Blacklist

✅ Refresh After Logout

---

# Folder Structure

```text
users/

    views/

        logout.py

config/

settings.py
```

---

# Git Commit

```bash
git add .

git commit -m "feat(tokens): implement JWT refresh token rotation and logout"
```

---

# 🔥 Senior Django Developer Improvements

উপরের implementation কাজ করবে, কিন্তু production-এ আমি আরও কিছু পরিবর্তন করব।

## 1. Use `dj-rest-auth` LogoutView

যদি শুধু refresh token blacklist করতে চাও, তাহলে `dj-rest-auth`-এর built-in `LogoutView` extend করা ভালো। নতুন APIView না লিখলেও চলে।

---

## 2. Validate Refresh Token

বর্তমান code:

```python
token = RefreshToken(refresh)
token.blacklist()
```

Production-এ exception handle করা উচিত।

```python
from rest_framework.exceptions import ValidationError

try:
    token = RefreshToken(refresh)
    token.blacklist()
except Exception:
    raise ValidationError(
        {"refresh": "Invalid or expired refresh token."}
    )
```

---

## 3. Store JWT in HTTPOnly Cookies

Production-এ

❌ `localStorage`

এর পরিবর্তে

✅ HTTPOnly Secure Cookies

ব্যবহার করা বেশি নিরাপদ, কারণ এতে XSS attack-এর ঝুঁকি কমে।

---

## 4. Axios Refresh Queue

একই সময়ে একাধিক request 401 return করলে multiple refresh request পাঠানো উচিত নয়। Production-এ একটি refresh queue/interceptor pattern ব্যবহার করা হয়।

---

## Commit 15 Preview

```bash
feat(auth): finalize production authentication architecture and best practices
```

এটি হবে পুরো authentication system-এর final commit। এখানে আমরা শিখব:

* Authentication Architecture Review
* Request Lifecycle
* OAuth + JWT Flow
* Cookie vs Header Authentication
* Authentication Best Practices
* Production Deployment Checklist
* Common Security Pitfalls
* Senior Django Authentication Patterns

এই commit শেষ করলে `dj-rest-auth + django-allauth + SimpleJWT + Google + GitHub + Facebook` authentication system সম্পূর্ণ production-ready architecture হিসেবে বুঝে যাবে।


--------

# Commit 15

```bash
feat(auth): finalize production-ready authentication architecture
```

> 🎉 **Congratulations!**
>
> Commit 15-এর পর তোমার Authentication System শেষ।
>
> এটা আর একটা সাধারণ Login System না।
>
> এটা একটা **Production Ready Authentication Infrastructure**।

---

# Final Authentication Architecture

```text
                         Internet
                              │
                              │
                         HTTPS (443)
                              │
                              ▼
                         Nginx / Caddy
                              │
                              ▼
                          Gunicorn
                              │
                              ▼
                         Django DRF
                              │
        ┌─────────────────────┼────────────────────┐
        │                     │                    │
        ▼                     ▼                    ▼
 dj-rest-auth          django-allauth         SimpleJWT
        │                     │                    │
        │                     │                    │
        └──────────────┬──────┴──────────────┬────┘
                       │                     │
                 Email Login           Social Login
                       │                     │
              ┌────────┼──────────┐     ┌────┼─────────────┐
              │        │          │     │    │             │
              ▼        ▼          ▼     ▼    ▼             ▼
           Google   GitHub   Facebook  Apple Microsoft LinkedIn
                       │
                       ▼
                User Authentication
                       │
                       ▼
             Access + Refresh Token
                       │
                       ▼
               Protected API Access
```

---

# Authentication Lifecycle

```text
User Registration

        │

        ▼

Email Verification

        │

        ▼

Login

        │

        ▼

Access Token

        │

        ▼

Protected API

        │

        ▼

Access Expired

        │

        ▼

Refresh Token

        │

        ▼

New Access Token

        │

        ▼

Logout

        │

        ▼

Blacklist Refresh Token
```

---

# Everything Implemented

## Authentication

✅ Email Login

✅ JWT Login

✅ Logout

✅ Refresh Token

✅ Token Rotation

✅ Blacklist

---

## Registration

✅ Register

✅ Email Verification

✅ Resend Verification

---

## Password

✅ Change Password

✅ Forgot Password

✅ Reset Password

---

## Social Login

✅ Google

✅ GitHub

✅ Facebook

---

## Profile

✅ Current User

✅ Update Profile

✅ Partial Update

---

## Security

✅ HTTPS

✅ Secure Cookies

✅ CSRF

✅ CORS

✅ Trusted Origins

✅ Token Rotation

---

## Production

✅ Environment Variables

✅ SMTP

✅ OAuth

✅ JWT

---

# Final Folder Structure

```text
project/

│

├── config/

│      settings/

│          base.py
│          development.py
│          production.py

│

├── users/

│      models.py
│      managers.py

│

│      serializers/

│          login.py
│          register.py
│          user.py

│

│      social/

│          google.py
│          github.py
│          facebook.py

│

│      views/

│          profile.py
│          logout.py

│

│      urls.py

│

├── templates/

│      account/

│          email/

│

├── .env

├── requirements.txt
```

---

# Production Request Flow

```text
Browser

     │

Authorization Header

Bearer ACCESS_TOKEN

     │

▼

JWTAuthentication

     │

▼

Verify Signature

     │

▼

Verify Expiration

     │

▼

Get User

     │

▼

request.user

     │

▼

Permission

     │

▼

APIView
```

---

# OAuth Flow

```text
React

      │

Google Login

      │

Google Consent

      │

Authorization Code

      │

Backend

      │

GoogleOAuth2Adapter

      │

SocialLoginView

      │

JWT

      │

React
```

GitHub

↓

Same

Facebook

↓

Same

---

# Deployment Checklist

## Backend

```text
DEBUG=False

HTTPS

Gunicorn

Nginx

PostgreSQL

Redis

Celery

Whitenoise

Cloudinary

SMTP
```

---

## Frontend

```text
React

Axios

Refresh Interceptor

Protected Routes

OAuth

Error Handling
```

---

## Authentication

```text
JWT

Refresh Rotation

Blacklist

OAuth

Email Verification

Password Reset
```

---

# Common Production Mistakes

## Never

```python
SECRET_KEY="123"
```

---

Never

```python
DEBUG=True
```

---

Never

```python
ALLOWED_HOSTS=["*"]
```

---

Never

```python
CORS_ALLOW_ALL_ORIGINS=True
```

---

Never

```python
fields="__all__"
```

---

Never

```python
permission_classes=[]
```

---

Never

```python
print(request.data)
```

Password leak হতে পারে।

---

# Authentication Request Lifecycle

```text
Incoming Request

      │

JWTAuthentication

      │

Verify Token

      │

User Lookup

      │

Permission Check

      │

Serializer

      │

Database

      │

Response
```

---

# Authentication Best Practices

### Use

✅ Custom User Model

✅ Email Login

✅ OAuth

✅ JWT Rotation

✅ Blacklist

✅ HTTPS

✅ SMTP

✅ Environment Variables

✅ Serializer Validation

✅ Custom Permissions

✅ Rate Limiting

✅ Logging

---

# Authentication Features Matrix

| Feature             | Status |
| ------------------- | ------ |
| Email Registration  | ✅      |
| Email Verification  | ✅      |
| JWT Login           | ✅      |
| JWT Refresh         | ✅      |
| JWT Rotation        | ✅      |
| Logout              | ✅      |
| Logout All Devices  | ✅      |
| Password Reset      | ✅      |
| Google Login        | ✅      |
| GitHub Login        | ✅      |
| Facebook Login      | ✅      |
| Profile API         | ✅      |
| Production Security | ✅      |

---

# Git Commit

```bash
git add .

git commit -m "feat(auth): finalize production-ready authentication architecture"
```

---

# 🎓 Senior Django Developer Review

এই ১৫টি commit-এর মাধ্যমে তুমি `dj-rest-auth` + `django-allauth`-এর **মৌলিক থেকে production architecture** পর্যন্ত শিখেছ। তবে একটি বাস্তব বিষয় মনে রাখবে:

এই সিরিজে শেখানোর সুবিধার জন্য কিছু commit-এ আমরা আলাদা endpoint, custom serializer বা social view তৈরি করেছি। বাস্তব production project-এ সবসময়:

* `dj-rest-auth`-এর built-in views যতটা সম্ভব reuse করা হয়।
* OAuth provider অনুযায়ী flow (ID Token বনাম Authorization Code) আলাদা হতে পারে।
* Refresh token সাধারণত **HTTPOnly Secure Cookie**-তে রাখা হয়, `localStorage`-এ নয়।
* Response format, exception handling, logging, rate limiting এবং monitoring (Sentry, Prometheus ইত্যাদি) শুরু থেকেই পরিকল্পনা করা হয়।

---

# 🚀 Next Roadmap (Authentication শেষ)

এখন তোমার শেখার পরবর্তী ধাপ হওয়া উচিত:

1. **RBAC (Role-Based Access Control)** — User, Admin, Vendor, Staff
2. **Object-Level Permissions**
3. **Multi-Tenant / Multi-Vendor Authentication**
4. **API Key Authentication**
5. **Two-Factor Authentication (2FA)**
6. **Login History & Device Management**
7. **Session Management**
8. **Authentication Testing (pytest + DRF APIClient)**

> এগুলো শেষ করতে পারলে তুমি Django authentication-এর ক্ষেত্রে Junior থেকে Mid-level, এমনকি অনেক Production-level Backend Developer-এর সমমানের জ্ঞান অর্জন করবে।


----------

