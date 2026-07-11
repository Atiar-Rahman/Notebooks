নিচে **React + Django + django-allauth + dj-rest-auth + SimpleJWT + Google/GitHub Login**-এর একটি complete step-by-step setup দিলাম।

## 1. Django package install

```bash
pip install django-allauth
pip install dj-rest-auth
pip install djangorestframework
pip install djangorestframework-simplejwt
pip install django-cors-headers
```

---

# Backend (Django)

## 2. `settings.py`

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "django.contrib.sites",

    "rest_framework",
    "corsheaders",

    "allauth",
    "allauth.account",
    "allauth.socialaccount",

    "allauth.socialaccount.providers.google",
    "allauth.socialaccount.providers.github",

    "dj_rest_auth",
    "dj_rest_auth.registration",
]


SITE_ID = 1


MIDDLEWARE = [
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",

    "allauth.account.middleware.AccountMiddleware",

    "django.contrib.messages.middleware.MessageMiddleware",
]


CORS_ALLOWED_ORIGINS = [
    "http://localhost:5173",
]


REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    )

}
```

---

## 3. Database migrate

```bash
python manage.py migrate
```

---

## 4. Admin user তৈরি

```bash
python manage.py createsuperuser
```

---

# Social Provider Setup

## 5. Google OAuth

Google Cloud Console থেকে:

- OAuth Client তৈরি করুন
    
- Redirect URL দিন:
    

```
http://localhost:8000/accounts/google/login/callback/
```

তারপর Django Admin:

```
/admin/
```

যান।

Social Applications:

```
Provider:
Google

Client ID:
xxxxx

Secret:
xxxxx

Sites:
example.com
```

একইভাবে GitHub:

```
http://localhost:8000/accounts/github/login/callback/
```

---

# URL Setup

## 6. `urls.py`

```python
from django.urls import path, include


urlpatterns = [

    path(
        "accounts/",
        include("allauth.urls")
    ),


]
```

এখন URL তৈরি হবে:

```
/accounts/google/login/

/accounts/github/login/
```

---

# JWT Callback

Allauth login করার পরে React-এ JWT পাঠানোর জন্য custom view লাগবে।

## 7. `views.py`

```python
from django.shortcuts import redirect
from rest_framework_simplejwt.tokens import RefreshToken


def oauth_success(request):

    user = request.user


    refresh = RefreshToken.for_user(user)

    access_token = str(refresh.access_token)

    refresh_token = str(refresh)


    return redirect(
        f"http://localhost:5173/auth/callback?"
        f"access={access_token}"
        f"&refresh={refresh_token}"
    )
```

---

## 8. URL add করুন

```python
from .views import oauth_success


urlpatterns = [

    path(
        "oauth/success/",
        oauth_success
    ),

]
```

তারপর settings:

```python
LOGIN_REDIRECT_URL = "/oauth/success/"
```

---

# React Part

## 9. Login Button

Install কিছু লাগবে না।

### Google Button

```jsx
function GoogleLogin(){

    const login = ()=>{

        window.location.href =
        "http://localhost:8000/accounts/google/login/";

    }


    return(
        <button onClick={login}>
            Login Google
        </button>
    )

}


export default GoogleLogin;
```

---

### GitHub Button

```jsx
function GithubLogin(){

    const login = ()=>{

        window.location.href =
        "http://localhost:8000/accounts/github/login/";

    }


    return(
        <button onClick={login}>
            Login Github
        </button>
    )

}


export default GithubLogin;
```

---

# React Callback Page

## 10. `/auth/callback`

```jsx
import {useEffect} from "react";


function AuthCallback(){

useEffect(()=>{


const params =
new URLSearchParams(
window.location.search
);


const access =
params.get("access");


const refresh =
params.get("refresh");


localStorage.setItem(
"access",
access
);


localStorage.setItem(
"refresh",
refresh
);


window.location.href="/dashboard";


},[])



return <h1>
Login Success
</h1>


}


export default AuthCallback;
```

---

# Protected API Call

React থেকে:

```javascript
fetch(
"http://localhost:8000/api/profile/",
{
headers:{
Authorization:
`Bearer ${localStorage.getItem("access")}`
}
}
)
```

---

## Final Flow

```
React Button
      |
      |
/accounts/google/login/
      |
      |
Google
      |
      |
callback ?code=
      |
      |
Allauth
      |
      |
Django User
      |
      |
SimpleJWT
      |
      |
React access + refresh token
```

এটাই হলো **React + Django Allauth + dj-rest-auth + JWT social login architecture**।



----------------

হ্যাঁ, **Django Allauth-এর Social Application model-এ OAuth credential setup করতে হয়**, তবে সব field পূরণ করতে হয় না।

আপনার screenshot-এর field গুলো:

### 1. Provider

এখানে নির্বাচন করবেন:

```
Google
```

অথবা

```
GitHub
```

---

### 2. Provider ID

সাধারণত খালি রাখুন।

---

### 3. Name

যেকোনো নাম দিতে পারেন:

```
Google Login
```

অথবা

```
GitHub Login
```

---

### 4. Client ID ✅ (অবশ্যই লাগবে)

এখানে Google/GitHub Developer Console থেকে পাওয়া:

```
Client ID
```

দিতে হবে।

Example:

```
1234567890-xxxx.apps.googleusercontent.com
```

---

### 5. Secret key / Client Secret ✅ (অবশ্যই লাগবে)

এখানে দিতে হবে:

```
Client Secret
```

Example:

```
GOCSPX-xxxxxxxx
```

---

### 6. Key

বেশিরভাগ provider-এর জন্য দরকার হয় না।

খালি রাখতে পারেন।

---

### 7. Settings

সাধারণত:

```json
{}
```

এভাবেই রাখুন।

---

### 8. Sites ✅ (খুব গুরুত্বপূর্ণ)

নিচে:

```
Available sites
```

থেকে আপনার site select করে ডান পাশে নিতে হবে।

যেমন:

```
example.com
```

বা localhost হলে:

```
localhost:8000
```

তারপর Save করবেন।

---

## Google OAuth Console-এ Redirect URL অবশ্যই দিতে হবে:

Development:

```
http://localhost:8000/accounts/google/login/callback/
```

Production:

```
https://yourdomain.com/accounts/google/login/callback/
```

---

## আপনার screenshot অনুযায়ী minimum যা লাগবে:

|Field|লাগবে?|
|---|---|
|Provider|✅|
|Name|✅|
|Client ID|✅|
|Secret Key|✅|
|Key|❌|
|Settings|❌|
|Sites|✅|

তারপর React থেকে:

```javascript
window.location.href =
"http://localhost:8000/accounts/google/login/";
```

দিলে Allauth কাজ করবে।


--------


নিচে **React + dj-rest-auth + django-allauth + SimpleJWT + Google Login** এর backend full setup দিলাম।

ধরি আপনার Django app নাম: `accounts`

---

## 1. Install packages

```bash
pip install django-allauth
pip install dj-rest-auth
pip install djangorestframework
pip install djangorestframework-simplejwt
```

---

# settings.py

```python
INSTALLED_APPS = [

    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    # required
    "django.contrib.sites",

    # DRF
    "rest_framework",

    # allauth
    "allauth",
    "allauth.account",
    "allauth.socialaccount",

    # google provider
    "allauth.socialaccount.providers.google",

    # dj-rest-auth
    "dj_rest_auth",
    "dj_rest_auth.registration",

    # your app
    "accounts",
]


SITE_ID = 1


AUTHENTICATION_BACKENDS = [

    "django.contrib.auth.backends.ModelBackend",

    "allauth.account.auth_backends.AuthenticationBackend",

]


MIDDLEWARE = [

    "django.middleware.security.SecurityMiddleware",

    "django.contrib.sessions.middleware.SessionMiddleware",

    "django.middleware.common.CommonMiddleware",

    "django.middleware.csrf.CsrfViewMiddleware",

    "django.contrib.auth.middleware.AuthenticationMiddleware",

    "django.contrib.messages.middleware.MessageMiddleware",

    "django.middleware.clickjacking.XFrameOptionsMiddleware",

    # IMPORTANT
    "allauth.account.middleware.AccountMiddleware",

]


REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (

        "rest_framework_simplejwt.authentication.JWTAuthentication",

    ),

}


REST_AUTH = {

    "USE_JWT": True,

}
```

---

# settings.py এ Google redirect

```python
GOOGLE_CALLBACK_URL = (
    "http://localhost:5173/auth/google/callback"
)
```

---

# accounts/views.py

```python
from allauth.socialaccount.providers.google.views import (
    GoogleOAuth2Adapter
)

from allauth.socialaccount.providers.oauth2.client import (
    OAuth2Client
)

from dj_rest_auth.registration.views import (
    SocialLoginView
)


class GoogleLogin(SocialLoginView):

    adapter_class = GoogleOAuth2Adapter

    callback_url = (
        "http://localhost:5173/auth/google/callback"
    )

    client_class = OAuth2Client
```

---

# accounts/urls.py

```python
from django.urls import path

from .views import GoogleLogin


urlpatterns = [

    path(
        "google/",
        GoogleLogin.as_view(),
        name="google_login"
    ),

]
```

---

# Main project urls.py

যেখানে `admin/` আছে:

```python
from django.contrib import admin
from django.urls import path, include


urlpatterns = [

    path(
        "admin/",
        admin.site.urls
    ),


    path(
        "api/auth/",
        include("accounts.urls")
    ),


]
```

---

এখন আপনার API হবে:

```
POST

http://localhost:8000/api/auth/google/
```

---

## Django Admin এ Google setup

Run:

```bash
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

তারপর:

```
http://localhost:8000/admin/
```

যান।

খুঁজুন:

```
Social Accounts
    ↓
Social applications
    ↓
Add
```

দিবেন:

```
Provider:
Google

Name:
Google Login

Client id:
Google Cloud Console এর Client ID

Secret key:
Google Client Secret

Sites:
example.com
```

---

## React থেকে request গেলে:

Body:

```json
{
    "code": "google_returned_code"
}
```

Response:

```json
{
    "access": "eyJhbGciOiJIUzI1Ni...",
    "refresh": "eyJhbGciOiJIUzI1Ni..."
}
```

---

## Google Cloud Console

Authorized redirect URI:

```
http://localhost:5173/auth/google/callback
```

---

এই backend দিয়ে flow হবে:

```
React
 |
 | Google OAuth
 |
Google
 |
 | code
 |
React callback
 |
POST /api/auth/google/
 |
dj-rest-auth
 |
allauth
 |
JWT
 |
React
```

এটাই production style setup।
