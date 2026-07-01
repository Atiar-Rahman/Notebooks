আপনি যদি **Django REST Framework** দিয়ে Professional Backend তৈরি করতে চান, তাহলে **dj-rest-auth** খুবই গুরুত্বপূর্ণ একটি package। বিশেষ করে React, Vue, Flutter, Next.js-এর সাথে Authentication করার সময় এটি অনেক সময় বাঁচায়।

---

# dj-rest-auth কী?

**dj-rest-auth** হলো একটি Authentication Package যা Django REST Framework-এর জন্য তৈরি।

এটি Ready-made API দেয়।

যেমন

* Login
* Logout
* Register
* Password Change
* Password Reset
* Email Verification
* JWT Authentication
* Token Authentication

অর্থাৎ এগুলো নিজে কোড না লিখেও ব্যবহার করা যায়।

---

# Without dj-rest-auth

নিজে লিখতে হবে

```text
Login API

Register API

Logout API

Password Reset API

Email Verification API

Change Password API

Confirm Password Reset API

JWT API
```

সবগুলো View, Serializer, URL নিজে লিখতে হবে।

---

# With dj-rest-auth

শুধু

```bash
pip install dj-rest-auth
```

তারপর URL Include করলেই অনেক API Ready হয়ে যায়।

---

# Architecture

```text
                React

                  │

                  ▼

          dj-rest-auth APIs

                  │

                  ▼

     Django Authentication System

                  │

                  ▼

             User Model
```

---

# How It Works

ধরুন User Login করবে।

```text
React

↓

POST /login/

↓

dj-rest-auth

↓

Authenticate User

↓

Return JWT

↓

React Store Token
```

---

# Main Features

## 1. Login

User

```json
{
   "email":"admin@gmail.com",
   "password":"123456"
}
```

↓

API

```text
POST

/login/
```

↓

Response

```json
{
   "access":"...",
   "refresh":"..."
}
```

---

## 2. Register

POST

```text
/register/
```

Body

```json
{
   "username":"Atiar",
   "email":"atiar@gmail.com",
   "password1":"12345678",
   "password2":"12345678"
}
```

↓

User Create হবে।

---

## 3. Logout

POST

```text
/logout/
```

↓

Token Invalid

↓

Logout

---

## 4. Password Change

```text
/password/change/
```

Body

```json
{
"old_password":"123",

"new_password1":"456",

"new_password2":"456"
}
```

---

## 5. Password Reset

Forgot Password

↓

User Email দিবে

↓

Reset Link যাবে

↓

Click করবে

↓

New Password দিবে

---

## 6. Email Verification

Register

↓

Email Sent

↓

Verification Link

↓

Verified

↓

Account Active

---

# Installation

```bash
pip install dj-rest-auth
```

JWT ব্যবহার করলে

```bash
pip install djangorestframework-simplejwt
```

---

# Required Packages

```bash
pip install dj-rest-auth

pip install django-allauth

pip install djangorestframework

pip install djangorestframework-simplejwt
```

---

# Why django-allauth?

**dj-rest-auth** Registration, Email Verification, Social Login-এর জন্য **django-allauth** ব্যবহার করে।

Relationship:

```text
dj-rest-auth

↓

django-allauth

↓

Django Authentication
```

---

# settings.py

```python
INSTALLED_APPS = [

    "django.contrib.sites",

    "rest_framework",

    "dj_rest_auth",

    "django.contrib.auth",

    "allauth",

    "allauth.account",

    "dj_rest_auth.registration",

]
```

---

Site ID

```python
SITE_ID = 1
```

---

REST Framework

```python
REST_FRAMEWORK = {

"DEFAULT_AUTHENTICATION_CLASSES":[

"rest_framework_simplejwt.authentication.JWTAuthentication"

]

}
```

---

JWT

```python
REST_USE_JWT = True
```

---

# urls.py

```python
urlpatterns=[

path("auth/",include("dj_rest_auth.urls")),

path("auth/registration/",include("dj_rest_auth.registration.urls"))

]
```

এখন Automatically API Ready।

---

# Available APIs

| Endpoint                      | Method | Purpose                    |
| ----------------------------- | ------ | -------------------------- |
| /auth/login/                  | POST   | Login                      |
| /auth/logout/                 | POST   | Logout                     |
| /auth/user/                   | GET    | Current User               |
| /auth/password/change/        | POST   | Change Password            |
| /auth/password/reset/         | POST   | Forgot Password            |
| /auth/password/reset/confirm/ | POST   | Confirm Reset              |
| /auth/token/verify/           | POST   | Verify JWT (if configured) |
| /auth/registration/           | POST   | Register                   |

---

# Login Flow

```text
React

↓

POST Login

↓

dj-rest-auth LoginView

↓

Authenticate()

↓

User Found

↓

Simple JWT

↓

Access

↓

Refresh

↓

Return JSON
```

---

# Registration Flow

```text
POST Register

↓

Serializer Validate

↓

Create User

↓

Email Verification

↓

Return Response
```

---

# Password Reset Flow

```text
Forgot Password

↓

Email

↓

Reset Link

↓

User Click

↓

New Password

↓

Success
```

---

# Logout Flow

```text
Logout

↓

Blacklist Refresh Token

↓

Delete Token

↓

Success
```

---

# Current User API

GET

```text
/auth/user/
```

Response

```json
{
"id":1,

"username":"Atiar",

"email":"atiar@gmail.com"
}
```

Internally

```python
request.user
```

Return করে।

---

# JWT Integration

Login

↓

Response

```json
{
"access":"...",

"refresh":"..."
}
```

React

↓

Store

↓

Header

```http
Authorization: Bearer access_token
```

↓

Protected API

---

# Custom Registration

Default Serializer পরিবর্তন করা যায়।

Example

```python
class CustomRegisterSerializer(RegisterSerializer):

    first_name = serializers.CharField()

    last_name = serializers.CharField()

    phone = serializers.CharField()
```

Settings

```python
REST_AUTH_REGISTER_SERIALIZERS = {
    "REGISTER_SERIALIZER":
    "accounts.serializers.CustomRegisterSerializer"
}
```

---

# Custom Login Serializer

Example

```python
class LoginSerializer(serializers.Serializer):

    email = serializers.EmailField()

    password = serializers.CharField()
```

Email দিয়ে Login করতে চাইলে Custom Serializer ব্যবহার করা যায়।

---

# Social Login Support

`dj-rest-auth` + `django-allauth` দিয়ে সহজেই Social Login যোগ করা যায়:

* Google Login
* GitHub Login
* Facebook Login
* Microsoft Login
* Apple Login

Flow:

```text
React

↓

Google OAuth

↓

Google

↓

Access Token

↓

dj-rest-auth

↓

Login

↓

JWT
```

---

# Advantages

* অনেক Authentication API Ready-made পাওয়া যায়।
* Django-এর Built-in Authentication System ব্যবহার করে।
* JWT এবং Token Authentication উভয়ই Support করে।
* Password Reset ও Email Verification সহজে যোগ করা যায়।
* Social Login সহজে Integrate করা যায়।
* Production-ready Authentication Flow দ্রুত তৈরি করা যায়।

---

# Limitations

* Package-এর Default Behavior বুঝতে কিছুটা সময় লাগে।
* Custom Business Logic থাকলে Serializer/View Override করতে হয়।
* বড় Project-এ Default Registration বা Login Flow প্রায়ই Customize করতে হয়।

---

# dj-rest-auth vs নিজে Authentication লেখা

| Feature            | dj-rest-auth         | Manual DRF              |
| ------------------ | -------------------- | ----------------------- |
| Login              | ✅ Built-in           | নিজে লিখতে হবে          |
| Register           | ✅ Built-in           | নিজে লিখতে হবে          |
| Logout             | ✅ Built-in           | নিজে লিখতে হবে          |
| Password Reset     | ✅ Built-in           | নিজে লিখতে হবে          |
| Email Verification | ✅ Built-in           | নিজে লিখতে হবে          |
| JWT Support        | ✅ Simple JWT-এর সাথে | নিজে Configure করতে হবে |
| Custom Logic       | Override করে         | সম্পূর্ণ Control        |

---

# Interview Questions

### 1. **dj-rest-auth কী?**

**Answer:** এটি Django REST Framework-এর জন্য একটি Authentication Package, যা Login, Logout, Registration, Password Reset, Email Verification এবং JWT Authentication-এর জন্য Ready-made API প্রদান করে।

### 2. **dj-rest-auth এবং Simple JWT-এর সম্পর্ক কী?**

**Answer:** `dj-rest-auth` Authentication Flow এবং API Endpoints দেয়, আর `Simple JWT` JWT Token তৈরি, Verify এবং Refresh করার কাজ করে।

### 3. **dj-rest-auth কেন `django-allauth` ব্যবহার করে?**

**Answer:** Registration, Email Verification, Password Reset এবং Social Authentication-এর সুবিধা দেওয়ার জন্য।

### 4. **কখন dj-rest-auth ব্যবহার করবেন?**

**Answer:** যখন দ্রুত একটি Secure Authentication System তৈরি করতে চান, বিশেষ করে React, Vue, Flutter বা Mobile App-এর Backend-এর জন্য।

---

## আপনার জন্য পরবর্তী শেখার সিকোয়েন্স

আপনি যেহেতু **Django + DRF + React SaaS Exam System** তৈরি করছেন, আমি এই ক্রমে শেখার পরামর্শ দেব:

1. ✅ Simple JWT (Complete)
2. ✅ dj-rest-auth
3. Custom User Model
4. Custom Register/Login Serializer
5. Email Verification
6. Role-based Authentication (Admin, Teacher, Student)
7. Custom Permission Classes
8. OAuth (Google Login)
9. React + JWT Authentication Flow (Axios Interceptors, Auto Refresh Token)
10. Production Security (HTTP-only Cookies, CSRF, Refresh Token Rotation)

এই ধারায় এগোলে আপনি একটি Production-level Authentication System তৈরি করতে পারবেন।

---------
আপনি যে Quickstart লিংকটি দিয়েছেন, সেটি **নতুন dj-rest-auth documentation**। আমি এটিকে এমনভাবে ব্যাখ্যা করছি যেন আপনি একদম Beginner থেকে Production পর্যন্ত বুঝতে পারেন। অফিসিয়াল Quickstart মূলত **Token Authentication** দিয়ে শুরু করে, এরপর **JWT** এবং **Registration** যোগ করতে বলে। ([dj-rest-auth.readthedocs.io][1])

---

# Step 1: Create Project

```bash
mkdir myproject
cd myproject

python -m venv venv

# Windows
venv\Scripts\activate

# Linux/macOS
source venv/bin/activate
```

### কেন Virtual Environment?

ধরুন আপনার কম্পিউটারে

```text
Django 5.2

Project A
```

আর অন্য Project

```text
Django 4.2
```

দুইটা Version Conflict করবে।

তাই

```text
Project

↓

Virtual Environment

↓

Own Packages
```

---

## Install Packages

```bash
pip install django djangorestframework dj-rest-auth
```

এখানে

| Package             | কাজ                 |
| ------------------- | ------------------- |
| django              | Main Framework      |
| djangorestframework | API তৈরির জন্য      |
| dj-rest-auth        | Authentication APIs |

---

## Create Project

```bash
django-admin startproject config .
```

Project Structure

```text
myproject/

    manage.py

    config/

        settings.py

        urls.py
```

---

# Step 2: Configure settings.py

Official Docs বলে

```python
INSTALLED_APPS = [

    ...

    "rest_framework",

    "rest_framework.authtoken",

    "dj_rest_auth",

]
```

## rest_framework

DRF Enable করে।

---

## rest_framework.authtoken

এটা DRF-এর Built-in Token Authentication।

Example

```text
Token

↓

5fd89ab....
```

এই Token Database-এ Store হয়।

---

## dj_rest_auth

Login

Logout

Password Change

User API

সব Enable করে।

---

## REST_FRAMEWORK

```python
REST_FRAMEWORK = {

"DEFAULT_AUTHENTICATION_CLASSES":[

"rest_framework.authentication.TokenAuthentication"

]

}
```

মানে

যখন Request আসবে

```http
Authorization:
Token abc123
```

DRF

```python
TokenAuthentication
```

Use করবে।

---

# Step 3: URLs

```python
urlpatterns=[

path(
"api/auth/",
include("dj_rest_auth.urls")
),

]
```

এখন Automatically API Ready।

---

## Available URLs

```text
/api/auth/login/

/api/auth/logout/

/api/auth/user/

/api/auth/password/change/

/api/auth/password/reset/
```

নিজে View লিখতে হবে না। ([dj-rest-auth.readthedocs.io][2])

---

# Step 4: Migration

```bash
python manage.py migrate
```

কি হয়?

Database Table তৈরি হবে।

Example

```text
auth_user

authtoken_token

django_session

...
```

---

# Step 5: Create User

```bash
python manage.py createsuperuser
```

Input

```text
Username

Email

Password
```

Database

```text
User Table
```

এ Save হবে।

---

# Step 6: Run Server

```bash
python manage.py runserver
```

Server

```text
http://127.0.0.1:8000
```

---

# Step 7: Login

POST

```text
/api/auth/login/
```

Body

```json
{
"username":"testuser",

"password":"123456"
}
```

---

Internally

```text
Request

↓

LoginView

↓

Authenticate()

↓

User Found

↓

Create Token

↓

Save Token

↓

Return Token
```

---

Response

```json
{
"key":"e9234908..."
}
```

এই Token

Database-এ থাকে।

---

# Step 8: Use Token

Next Request

```http
Authorization:
Token e9234908...
```

Example

```http
GET /api/auth/user/
```

↓

Server

```text
Read Header

↓

Find Token

↓

Find User

↓

request.user
```

---

Response

```json
{
"id":1,

"username":"Atiar",

"email":"abc@gmail.com"
}
```

---

# Step 9: Logout

```text
POST

/api/auth/logout/
```

↓

Delete Token

↓

Logout

---

# Complete Flow

```text
User

↓

POST Login

↓

dj-rest-auth LoginView

↓

Django Authenticate

↓

Generate Token

↓

Store DB

↓

Return Token

↓

Client Save Token

↓

Next Request

↓

Authorization: Token abc123

↓

Authenticated
```

---

# এরপর JWT যোগ করা

Official Docs বলছে

```bash
pip install djangorestframework-simplejwt
```

---

settings.py

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "dj_rest_auth.jwt_auth.JWTCookieAuthentication",
    ],
}
```

এখানে আর `TokenAuthentication` ব্যবহার হচ্ছে না।

এখন

```text
JWT Authentication
```

ব্যবহার হবে। ([dj-rest-auth.readthedocs.io][1])

---

## REST_AUTH Settings

```python
REST_AUTH = {

"USE_JWT":True,

"JWT_AUTH_COOKIE":"access",

"JWT_AUTH_REFRESH_COOKIE":"refresh",

"JWT_AUTH_HTTPONLY":True,

}
```

এগুলো কী?

### USE_JWT

```python
True
```

মানে

```text
Token Authentication

↓

OFF

JWT

↓

ON
```

---

### JWT_AUTH_COOKIE

```python
"access"
```

মানে

Browser Cookie

```text
access=eyJ...
```

---

### JWT_AUTH_REFRESH_COOKIE

```python
refresh
```

মানে

```text
refresh=eyJ...
```

---

### JWT_AUTH_HTTPONLY

```python
True
```

JavaScript

```javascript
document.cookie
```

দিয়ে Access করা যাবে না।

এটা XSS Attack থেকে Protection দেয়। ([dj-rest-auth.readthedocs.io][2])

---

# JWT Login

POST

```text
/api/auth/login/
```

Response

```json
{
"access":"eyJ...",

"refresh":"",

"user":{

"id":1,

"username":"Atiar"
}
}
```

Browser Automatically

```text
Cookie

↓

access

↓

refresh
```

Set করতে পারে যদি Cookie-based JWT Configuration ব্যবহার করেন। ([dj-rest-auth.readthedocs.io][1])

---

# Registration যোগ করা

Install

```bash
pip install "dj-rest-auth[with-social]"
```

এটা Install করবে

```text
django-allauth
```

---

settings.py

```python
INSTALLED_APPS = [

"django.contrib.sites",

"allauth",

"allauth.account",

"dj_rest_auth.registration"

]
```

---

Middleware

```python
MIDDLEWARE=[

...

"allauth.account.middleware.AccountMiddleware"

]
```

---

SITE_ID

```python
SITE_ID=1
```

এটা `django.contrib.sites` Framework-এর জন্য দরকার, যেটি `django-allauth` Email Verification এবং Social Login-এর মতো Feature-এ ব্যবহার করে। ([dj-rest-auth.readthedocs.io][2])

---

URL

```python
urlpatterns=[

path(
"api/auth/registration/",
include(
"dj_rest_auth.registration.urls"
)
),

]
```

---

Register API

```text
POST

/api/auth/registration/
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

↓

Flow

```text
Validate

↓

Create User

↓

Return Success
```

---

# Complete Production Authentication Flow

```text
React

↓

Register

↓

User Created

↓

Login

↓

Access Token

↓

Refresh Token

↓

Browser Cookie

↓

GET /user/

↓

request.user

↓

Protected APIs

↓

Logout

↓

Cookie Cleared / Token Invalid
```

---

## আমার পরামর্শ (Production Project)

আপনি যেহেতু **React + Django SaaS Exam System** বানাচ্ছেন, আমি অফিসিয়াল Quickstart-এর **Basic Token Authentication** ব্যবহার না করে সরাসরি **JWT + HTTP-only Cookies** Configuration শেখার পরামর্শ দেব। এটি আধুনিক SPA Application-এর জন্য বেশি নিরাপদ এবং অফিসিয়াল ডকুমেন্টেশনেও Recommended Configuration হিসেবে দেখানো হয়েছে। ([dj-rest-auth.readthedocs.io][3])

এরপরের ধাপে শিখুন:

1. Custom User Model
2. Custom Register Serializer
3. Email Verification
4. Role-based Authentication (Admin, Teacher, Student)
5. Google Login (OAuth)
6. React + Axios Interceptors + Auto Refresh Token
7. HTTP-only Cookie Authentication with CSRF Protection

[1]: https://dj-rest-auth.readthedocs.io/en/latest/getting-started/quickstart/?utm_source=chatgpt.com "Quickstart - dj-rest-auth"
[2]: https://dj-rest-auth.readthedocs.io/en/latest/getting-started/installation/?utm_source=chatgpt.com "Installation - dj-rest-auth"
[3]: https://dj-rest-auth.readthedocs.io/en/stable/?utm_source=chatgpt.com "dj-rest-auth"

-------

খুব ভালো প্রশ্ন। অনেকেই `SITE_ID = 1` লিখে দেন, কিন্তু **এটা আসলে কী এবং কোথায় ব্যবহার হয় তা বোঝেন না।**

---

# `SITE_ID = 1` কী?

Django-এর একটি built-in app আছে:

```python
django.contrib.sites
```

এই app-এর মাধ্যমে Django বুঝতে পারে **বর্তমানে কোন Website (Site) ব্যবহার হচ্ছে**।

যখন আপনি `settings.py`-এ লিখেন:

```python
SITE_ID = 1
```

তখন Django বলে:

> "আমি `django_site` table-এর ID = 1 রেকর্ডটি ব্যবহার করব।"

---

# Database-এ কী হয়?

Migration করার পরে একটি table তৈরি হয়:

```text
django_site
```

Table Structure:

| id | domain      | name        |
| -- | ----------- | ----------- |
| 1  | example.com | example.com |

Default ভাবে Django এটা তৈরি করে।

---

# Example

ধরুন আপনার দুইটি Website আছে।

```text
exam.com

shop.com
```

Database

| id | domain   |
| -- | -------- |
| 1  | exam.com |
| 2  | shop.com |

settings.py

```python
SITE_ID = 1
```

মানে

```text
Current Site

↓

exam.com
```

যদি

```python
SITE_ID = 2
```

হয়

তাহলে

```text
Current Site

↓

shop.com
```

---

# কোথায় ব্যবহার হয়?

## 1. Email Verification (সবচেয়ে Common)

ধরুন User Register করলো।

```text
User

↓

Register

↓

Verification Email
```

Email-এ Link পাঠানো হবে

```
https://example.com/verify/abc123
```

কিন্তু

```
example.com
```

কোথা থেকে আসলো?

এটা এসেছে

```python
django.contrib.sites
```

থেকে।

Flow

```text
SITE_ID

↓

django_site

↓

Domain

↓

Verification Link
```

---

## 2. Password Reset Email

Forgot Password

↓

Email যাবে

```
https://example.com/reset/abc/
```

এই

```
example.com
```

Site Framework থেকে আসে।

---

## 3. Google Login

Google OAuth

↓

Redirect URI

```
https://example.com/accounts/google/login/
```

এই Domain-ও Site Framework ব্যবহার করতে পারে।

---

## 4. Facebook Login

একইভাবে

Facebook Redirect URI

Site Framework থেকে আসে।

---

## 5. django-allauth

সবচেয়ে বেশি ব্যবহার হয়

```text
django-allauth
```

এ।

কারণ

```text
Email Verification

Password Reset

Social Login

Magic Link

Invitation
```

সবগুলোতে Domain লাগে।

---

# dj-rest-auth-এ কোথায় ব্যবহার হয়?

আপনি যদি

```python
INSTALLED_APPS = [

"django.contrib.sites",

"allauth",

"dj_rest_auth.registration",

]
```

ব্যবহার করেন

তাহলে

```python
SITE_ID = 1
```

অবশ্যই লাগবে।

কারণ

```
dj-rest-auth

↓

django-allauth

↓

Site Framework
```

---

# Example

settings.py

```python
SITE_ID = 1
```

Database

| id | domain         |
| -- | -------------- |
| 1  | localhost:8000 |

Register করলে

Email

```
http://localhost:8000/verify-email/...
```

Production-এ

Database

| id | domain   |
| -- | -------- |
| 1  | exam.com |

তখন Email

```
https://exam.com/verify-email/...
```

---

# Site Object কীভাবে পাওয়া যায়?

যেকোনো জায়গা থেকে

```python
from django.contrib.sites.models import Site

site = Site.objects.get_current()

print(site.domain)
print(site.name)
```

Output

```text
example.com
example.com
```

---

# Admin Panel থেকে পরিবর্তন

```
Admin

↓

Sites

↓

example.com
```

এখানে Domain Change করতে পারবেন।

উদাহরণ:

```
localhost:8000
```

↓

```
api.exam.com
```

---

# কখন `SITE_ID` দরকার?

| Feature                          | SITE_ID লাগবে?         |
| -------------------------------- | ---------------------- |
| Basic Django Login               | ❌ না                   |
| DRF Token Authentication         | ❌ না                   |
| Simple JWT                       | ❌ না                   |
| dj-rest-auth (শুধু Login/Logout) | ❌ না (সাধারণ ক্ষেত্রে) |
| dj-rest-auth Registration        | ✅ হ্যাঁ                |
| django-allauth                   | ✅ হ্যাঁ                |
| Email Verification               | ✅ হ্যাঁ                |
| Password Reset Email             | ✅ হ্যাঁ                |
| Google Login                     | ✅ হ্যাঁ                |
| Facebook Login                   | ✅ হ্যাঁ                |
| Social Authentication            | ✅ হ্যাঁ                |

---

# Interview Answer

**প্রশ্ন:** `SITE_ID = 1` কেন ব্যবহার করা হয়?

**উত্তর:**

> `SITE_ID` Django-এর `django.contrib.sites` framework-কে জানায় কোন Site Configuration ব্যবহার করতে হবে। এটি `django_site` table-এর একটি নির্দিষ্ট Site নির্বাচন করে। `django-allauth`, `dj-rest-auth`, Email Verification, Password Reset এবং Social Login-এর মতো Feature-এ বর্তমান Domain (`example.com`, `localhost:8000`, `api.myapp.com`) নির্ধারণ করার জন্য এটি ব্যবহৃত হয়।

### মনে রাখার সহজ নিয়ম

* **শুধু JWT বা DRF API বানাচ্ছেন?** → `SITE_ID` সাধারণত দরকার নেই।
* **`django-allauth` বা `dj-rest-auth.registration` ব্যবহার করছেন?** → `SITE_ID` এবং `django.contrib.sites` প্রয়োজন।



-----------
হ্যাঁ, **`SITE_ID = 1` শুধু `settings.py`-এ লিখলেই যথেষ্ট নয়।** আরও কিছু Configuration করতে হবে।

## Step 1: `settings.py`

```python
INSTALLED_APPS = [
    ...

    "django.contrib.sites",

    "allauth",
    "allauth.account",

    "dj_rest_auth",
    "dj_rest_auth.registration",
]

SITE_ID = 1
```

---

## Step 2: Migration

```bash
python manage.py migrate
```

এতে `django_site` table তৈরি হবে।

---

## Step 3: `django_site` Table Update

Superuser তৈরি করুন:

```bash
python manage.py createsuperuser
```

Admin Panel-এ যান:

```
http://127.0.0.1:8000/admin/
```

তারপর:

```
Sites
    ↓
example.com
```

এটি Edit করুন।

Development-এর জন্য:

| Field        | Value                                  |
| ------------ | -------------------------------------- |
| Domain name  | `127.0.0.1:8000` অথবা `localhost:8000` |
| Display name | `Local Development`                    |

Production-এর জন্য:

| Field        | Value              |
| ------------ | ------------------ |
| Domain name  | `exam.example.com` |
| Display name | `Exam System`      |

---

## Step 4: Middleware (যদি `django-allauth` ব্যবহার করেন)

```python
MIDDLEWARE = [
    ...
    "allauth.account.middleware.AccountMiddleware",
]
```

---

## কেন শুধু `SITE_ID = 1` লিখলেই হবে না?

ধরুন আপনি শুধু লিখলেন:

```python
SITE_ID = 1
```

কিন্তু `django_site` table-এ এখনও আছে:

| id | domain      |
| -- | ----------- |
| 1  | example.com |

তাহলে Email Verification Link হবে:

```
https://example.com/account-confirm-email/...
```

যা আপনার Local Server বা Production Domain হবে না।

তাই `django_site` table-এর Domain-ও Update করতে হবে।

---

## Summary

`SITE_ID = 1` ব্যবহার করতে হলে এই ৪টি জিনিস দরকার:

✅ `settings.py`

```python
INSTALLED_APPS = [
    "django.contrib.sites",
    ...
]

SITE_ID = 1
```

✅ Migration

```bash
python manage.py migrate
```

✅ Admin Panel → **Sites** → Domain Update

✅ `AccountMiddleware` যোগ করা (যদি `django-allauth` ব্যবহার করেন)

---

**Interview Tip:**

যদি Interview-তে জিজ্ঞেস করে, **"Is `SITE_ID = 1` enough?"**

উত্তর হবে:

> **না।** `SITE_ID = 1` শুধু Django-কে বলে কোন Site Record ব্যবহার করতে হবে। এছাড়া `django.contrib.sites` app install, migration, `django_site` table-এ সঠিক domain configure করা এবং `django-allauth` ব্যবহার করলে প্রয়োজনীয় middleware যোগ করতে হবে।


----------

**হ্যাঁ, হবে।** বরং আপনি যদি **DRF Authentication** শিখতে চান, তাহলে **অফিশিয়াল `dj-rest-auth` Quickstart Flow** অনুসরণ করাই সবচেয়ে ভালো শুরু।

তবে আমি একটি গুরুত্বপূর্ণ বিষয় বলব।

### Phase 1: Official Quickstart (অবশ্যই করুন)

এই Flow সম্পূর্ণ করুন:

1. ✅ Django Project
2. ✅ Install `djangorestframework`
3. ✅ Install `dj-rest-auth`
4. ✅ Configure `settings.py`
5. ✅ Login API
6. ✅ Logout API
7. ✅ User API
8. ✅ JWT Configure
9. ✅ Registration
10. ✅ Test সব API (Postman/Insomnia)

এটি করলে আপনি বুঝবেন `dj-rest-auth` কীভাবে কাজ করে।

---

### Phase 2: এরপর Customization শিখুন

বাস্তব Project-এ শুধু Quickstart যথেষ্ট নয়।

আপনার **SaaS Exam System**-এর জন্য এরপর শিখবেন:

* Custom User Model
* Custom Register Serializer
* Email দিয়ে Login
* Role (Admin, Teacher, Student)
* Email Verification
* Custom JWT Claims
* Custom Permission
* React Integration

---

## আপনার Project-এর Flow

```text
Official Quickstart
        ↓
JWT Setup
        ↓
Registration
        ↓
Custom User Model
        ↓
Role-based Authentication
        ↓
Custom Permissions
        ↓
React Login
        ↓
Production Deployment
```

---

## আমার Recommendation

আপনার লক্ষ্য যেহেতু **Professional Django Backend Developer** হওয়া, তাই আমি এই শেখার ক্রম সাজিয়ে দিচ্ছি:

```
Week 1
✅ Official dj-rest-auth Quickstart

Week 2
✅ Simple JWT Deep Dive

Week 3
✅ django-allauth

Week 4
✅ Custom Authentication

Week 5
✅ React + JWT Authentication

Week 6
✅ Production Security
```

### আমার পরামর্শ

**Quickstart-এর প্রতিটি Step Blindly Copy করবেন না।**

প্রতিটি লাইনের উত্তর জানুন:

* কেন `rest_framework.authtoken` যোগ করা হয়?
* কেন `SITE_ID = 1` লাগে?
* কেন `django.contrib.sites` লাগে?
* কেন `allauth.account.middleware.AccountMiddleware` যোগ করতে হয়?
* কেন `REST_AUTH["USE_JWT"] = True` দিই?
* কেন `JWT_AUTH_COOKIE` ব্যবহার করি?

এভাবে শিখলে Interview-তে যেকোনো প্রশ্নের উত্তর দিতে পারবেন, শুধু কোড রান করাতে পারবেন না।

**আমি চাইলে অফিসিয়াল `dj-rest-auth` Quickstart-এর প্রতিটি লাইন (`settings.py`, `urls.py`, `views`, `serializer`, `middleware`, `REST_AUTH`, `SIMPLE_JWT`) কী করে এবং কেন লাগে—লাইন বাই লাইন ব্যাখ্যা করতে পারি।** এটি প্রায় ৩–৪ ঘণ্টার একটি পূর্ণাঙ্গ টিউটোরিয়ালের সমান হবে।

-----------

