DRF API-এর জন্য সবচেয়ে ভালো choice সাধারণত:

### ✅ Recommended stack

```text
django-allauth
        +
dj-rest-auth
        +
djangorestframework-simplejwt
```

কারণ:

- ✅ Google/Facebook/GitHub OAuth ready support
    
- ✅ DRF endpoint ready পাওয়া যায়
    
- ✅ JWT access + refresh token ব্যবহার করা যায়
    
- ✅ React / Vue / Flutter / Mobile app-এর সাথে সহজে কাজ করে
    
- ✅ User model, email, password reset ইত্যাদি built-in flow পাওয়া যায়
    

Architecture:

```
Frontend (React/Flutter)
        |
        | Google OAuth token
        ↓
DRF API
        |
        ↓
django-allauth
        |
        ↓
User create/login
        |
        ↓
SimpleJWT
        |
        ↓
access + refresh token
```

---

### যদি শুধু Google login লাগে

তাহলে আরও lightweight:

```text
django-allauth
+
custom DRF view
+
simplejwt
```

অনেক production API এ এটা ব্যবহার করে।

---

### `python-social-auth`?

DRF নতুন project-এর জন্য আমি কম recommend করবো, কারণ:

- API-first flow এ একটু বেশি custom code লাগে
    
- JWT integration নিজে handle করতে হয়
    

---

### Production DRF API এর জন্য আমার ranking:

1. 🥇 `django-allauth + dj-rest-auth + simplejwt`
    
2. 🥈 `django-allauth + custom OAuth views + simplejwt`
    
3. 🥉 `python-social-auth`
    

React/Flutter client থাকলে ১ নম্বরটাই সবচেয়ে practical।

----------

নিচে **Django REST Framework + django-allauth + dj-rest-auth + SimpleJWT দিয়ে Social Login (Google example)** এর complete setup দিলাম।

## 1. Install packages

```bash
pip install django
pip install djangorestframework
pip install django-allauth
pip install dj-rest-auth
pip install djangorestframework-simplejwt
```

---

## 2. Django project create

```bash
django-admin startproject config
cd config

python manage.py startapp accounts
```

---

## 3. `settings.py` configure

### Apps

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "django.contrib.sites",

    # DRF
    "rest_framework",
    "rest_framework.authtoken",

    # allauth
    "allauth",
    "allauth.account",
    "allauth.socialaccount",

    # providers
    "allauth.socialaccount.providers.google",

    # dj-rest-auth
    "dj_rest_auth",
    "dj_rest_auth.registration",

    "accounts",
]
```

---

### Site ID

```python
SITE_ID = 1
```

---

## 4. Authentication config

`settings.py`

```python
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    )
}
```

---

## 5. SimpleJWT config

```python
from datetime import timedelta


SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=30),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),

}
```

---

## 6. Allauth settings

```python
ACCOUNT_EMAIL_REQUIRED = True

ACCOUNT_USERNAME_REQUIRED = False

ACCOUNT_AUTHENTICATION_METHOD = "email"

ACCOUNT_EMAIL_VERIFICATION = "none"


SOCIALACCOUNT_QUERY_EMAIL = True
```

---

## 7. Google provider config

`settings.py`

```python
SOCIALACCOUNT_PROVIDERS = {

    "google": {

        "SCOPE": [
            "profile",
            "email",
        ],

        "AUTH_PARAMS": {
            "access_type": "online"
        }

    }
}
```

---

# 8. Database migrate

```bash
python manage.py migrate
```

Create admin:

```bash
python manage.py createsuperuser
```

---

# 9. Add Google OAuth credentials

Go to:

[Google Cloud Console](https://console.cloud.google.com?utm_source=chatgpt.com)

Create:

```
APIs & Services
      ↓
Credentials
      ↓
Create OAuth Client ID
```

Choose:

```
Application type:
Web Application
```

Add redirect:

```
http://localhost:8000/accounts/google/login/callback/
```

Get:

```
CLIENT_ID
CLIENT_SECRET
```

---

# 10. Admin panel এ Social Application add

Run:

```bash
python manage.py runserver
```

Open:

```
localhost:8000/admin
```

Go:

```
Social Accounts
   |
Social applications
   |
Add
```

Fill:

```
Provider:
Google

Name:
Google

Client id:
xxxxx

Secret:
xxxxx

Sites:
example.com
```

Save.

---

# 11. URLs

`config/urls.py`

```python
from django.urls import path, include


urlpatterns = [

    path(
        "api/auth/",
        include("dj_rest_auth.urls")
    ),


    path(
        "api/auth/registration/",
        include(
            "dj_rest_auth.registration.urls"
        )
    ),


    path(
        "accounts/",
        include("allauth.urls")
    ),

]
```

---

# 12. JWT Token endpoints

`urls.py`

```python
from rest_framework_simplejwt.views import (
    TokenRefreshView,
)


urlpatterns += [

    path(
        "api/token/refresh/",
        TokenRefreshView.as_view()
    ),

]
```

---

# 13. Normal Registration

Request:

```
POST

/api/auth/registration/
```

Body:

```json
{
 "email":"test@gmail.com",
 "password1":"12345678",
 "password2":"12345678"
}
```

Response:

```json
{
 "access":"xxxxx",
 "refresh":"xxxxx"
}
```

---

# 14. Login

```
POST

/api/auth/login/
```

Body:

```json
{
"email":"test@gmail.com",
"password":"12345678"
}
```

Response:

```json
{
"access":"jwt-access-token",
"refresh":"jwt-refresh-token"
}
```

---

# 15. Google Login API

Install provider already done.

Frontend থেকে Google OAuth token নাও।

Then:

```
POST

/api/auth/google/
```

Body:

```json
{
"access_token":"google-token"
}
```

Response:

```json
{
"access":"jwt-token",
"refresh":"jwt-refresh-token"
}
```

---

# 16. Protected API example

views.py

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated


class ProfileView(APIView):

    permission_classes=[
        IsAuthenticated
    ]


    def get(self,request):

        return Response({
            "email":request.user.email
        })
```

URL:

```python
path(
 "api/profile/",
 ProfileView.as_view()
)
```

Call:

```
GET /api/profile/
```

Header:

```
Authorization:

Bearer your_access_token
```

---

# Final Flow

```text
React / Flutter
        |
        |
 Google Login
        |
        |
 Google Access Token
        |
        |
POST /api/auth/google/
        |
        |
django-allauth verify
        |
        |
Create User
        |
        |
SimpleJWT
        |
        |
access + refresh token
        |
        |
DRF Protected API
```

এই setup production-level DRF API এর জন্য একটি common pattern।

-----------
তুমি যে documentation link দিয়েছো সেটা [django-allauth Quickstart documentation](https://docs.allauth.org/en/latest/installation/quickstart.html?utm_source=chatgpt.com) — এখানে মূলত **django-allauth install + basic configuration** দেখানো হয়েছে। DRF-এর জন্য কীভাবে বুঝবে সেটা নিচে সহজ করে দিলাম।

## 1. django-allauth কী করে?

`django-allauth` মূলত handle করে:

- User registration
    
- Login/logout
    
- Email verification
    
- Password reset
    
- Social login (Google, GitHub, Facebook)
    

মানে:

```
User
 |
 | login/register
 ↓
django-allauth
 |
 ↓
Django User Model
```

---

## 2. Install

প্রথমে install:

```bash
pip install django-allauth
```

---

## 3. settings.py এ app add

Documentation অনুযায়ী:

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "django.contrib.sites",

    "allauth",
    "allauth.account",
    "allauth.socialaccount",

]
```

এখানে:

### `django.contrib.sites`

একই project-এর multiple domain manage করতে লাগে।

Example:

```
localhost:8000
mywebsite.com
api.mywebsite.com
```

সবকে site হিসেবে রাখে।

---

## 4. SITE_ID

```python
SITE_ID = 1
```

মানে Django কোন site ব্যবহার করবে সেটা বলে।

---

## 5. Authentication backend add

```python
AUTHENTICATION_BACKENDS = [

    "django.contrib.auth.backends.ModelBackend",

    "allauth.account.auth_backends.AuthenticationBackend",

]
```

এটা দরকার কারণ Django default authentication + allauth authentication দুইটাই চালাবে।

---

## 6. URL include

urls.py:

```python
urlpatterns = [

    path(
        "accounts/",
        include("allauth.urls")
    ),

]
```

এখন allauth routes পাওয়া যাবে:

```
/accounts/login/
/accounts/logout/
/accounts/signup/
/accounts/password/reset/
```

---

## 7. Migration

কারণ allauth নিজের database table বানায়:

```bash
python manage.py migrate
```

এগুলো তৈরি হবে:

```
account_emailaddress
socialaccount_socialaccount
socialaccount_socialapp
```

---

# এখন DRF এর সাথে relation

Documentation-এর quickstart মূলত Django website-এর জন্য।

DRF API হলে তুমি সাধারণত add করবে:

```
django-allauth
        +
dj-rest-auth
        +
simplejwt
```

Flow:

```
Mobile / React App

        |
        |
        v

POST /api/auth/google/

        |
        |
        v

dj-rest-auth

        |
        |
        v

django-allauth

        |
        |
        v

User create/login

        |
        |
        v

JWT Token
```

---

## Social provider add

Example Google:

```python
INSTALLED_APPS = [

    "allauth.socialaccount.providers.google",

]
```

তারপর:

```python
SOCIALACCOUNT_PROVIDERS = {

    "google": {

        "SCOPE": [
            "profile",
            "email"
        ]

    }

}
```

---

## সহজ ভাষায়

Documentation যেটা বলছে:

1. allauth install করো
    
2. apps add করো
    
3. authentication backend add করো
    
4. urls connect করো
    
5. migrate চালাও
    

তারপর DRF project-এ `dj-rest-auth` বসিয়ে API বানাও।

DRF API হলে শুধু quickstart follow করলে হবে না, তার উপর `dj-rest-auth + JWT` layer লাগবে।