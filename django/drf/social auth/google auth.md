যদি তুমি **শুধু DRF API** বানাতে চাও (frontend Google popup ছাড়া), তাহলে Google Sign-In flow একটু different।

তোমার API client (React / mobile / Postman) Google থেকে token নেবে, তারপর DRF backend-এ পাঠাবে।

Flow:

```text
Client
  ↓
Google OAuth login
  ↓
Google returns id_token
  ↓
POST /api/auth/google/
  ↓
Django verifies token
  ↓
User create/login
  ↓
JWT return
```

---

# Method 1 — `dj-rest-auth + allauth` (recommended)

তুমি already `dj-rest-auth` use করছ, তাই এটা easiest।

---

## 1. Install

```bash
pip install "dj-rest-auth[with-social]"
```

---

## 2. apps

```python
INSTALLED_APPS = [
    "django.contrib.sites",

    "rest_framework",
    "dj_rest_auth",
    "dj_rest_auth.registration",

    "allauth",
    "allauth.account",
    "allauth.socialaccount",
    "allauth.socialaccount.providers.google",
]
```

---

## 3. settings

```python
SITE_ID = 1

AUTHENTICATION_BACKENDS = (
    "django.contrib.auth.backends.ModelBackend",
    "allauth.account.auth_backends.AuthenticationBackend",
)
```

---

## 4. API View

```python
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter
from dj_rest_auth.registration.views import SocialLoginView
```

```python
class GoogleLogin(SocialLoginView):
    adapter_class = GoogleOAuth2Adapter
```

---

## 5. URL

```python
from django.urls import path
from .views import GoogleLogin

urlpatterns = [
    path("google/", GoogleLogin.as_view()),
]
```

---

## 6. Request

Client POST করবে:

```json
{
    "access_token": "google_access_token"
}
```

Response:

```json
{
    "access": "...",
    "refresh": "...",
    "user": {
        "email": "abc@gmail.com"
    }
}
```

---

# Method 2 — Pure DRF (allauth ছাড়া, more control)

Production-এ অনেক backend dev এটা prefer করে।

Idea:

1. frontend Google `id_token` পাঠাবে
    
2. backend token verify করবে
    
3. user create/login করবে
    
4. JWT issue করবে
    

---

## Install Google verifier

```bash
pip install google-auth
```

[google-auth docs](https://google-auth.readthedocs.io/en/latest/?utm_source=chatgpt.com)

---

## Serializer

```python
from rest_framework import serializers

class GoogleAuthSerializer(serializers.Serializer):
    token = serializers.CharField()
```

---

## View

```python
from google.oauth2 import id_token
from google.auth.transport import requests
from rest_framework.views import APIView
from rest_framework.response import Response
from django.contrib.auth import get_user_model
```

```python
User = get_user_model()

class GoogleLoginAPIView(APIView):
    def post(self, request):
        token = request.data.get("token")

        info = id_token.verify_oauth2_token(
            token,
            requests.Request()
        )

        email = info["email"]
        name = info.get("name", "")

        user, created = User.objects.get_or_create(
            email=email,
            defaults={"username": email}
        )

        return Response({
            "email": user.email,
            "created": created
        })
```

---

# কোনটা better?

### `dj-rest-auth`

Pros:

- Less code
    
- Existing auth system use করবে
    

Cons:

- Internal magic বেশি
    

---

### Pure DRF

Pros:

- Full control
    
- Easy debugging
    
- Cleaner architecture
    

Cons:

- More code
    

---

তুমি যেহেতু authentication internals শিখছ (JWT, serializer, custom user), আমার recommendation:

**Pure DRF Google API first শিখো**, তারপর `dj-rest-auth social login`।  
তাতে backend flow ভালো বুঝবে।

------

যেহেতু তুমি already **`dj-rest-auth`** add করেছ, এখন social login (Google) add করা সহজ — পুরো setup নতুন করে করতে হবে না।

Step-by-step:

---

# 1. Social dependencies install

```bash
pip install "dj-rest-auth[with-social]"
```

এটা install করবে `django-allauth` + social providers।

Already install করা থাকলে skip।

Check:

```bash
pip show django-allauth
```

---

# 2. `INSTALLED_APPS` update

Add করো:

```python
INSTALLED_APPS = [
    # existing apps...

    "django.contrib.sites",

    "allauth",
    "allauth.account",
    "allauth.socialaccount",
    "allauth.socialaccount.providers.google",

    "dj_rest_auth.registration",
]
```

> `dj_rest_auth` already আছে ধরে নিচ্ছি।

---

# 3. `SITE_ID`

```python
SITE_ID = 1
```

---

# 4. Authentication backend

```python
AUTHENTICATION_BACKENDS = (
    "django.contrib.auth.backends.ModelBackend",
    "allauth.account.auth_backends.AuthenticationBackend",
)
```

---

# 5. Migrate

```bash
python manage.py migrate
```

New tables হবে:

- socialaccount_socialapp
    
- socialaccount_socialtoken
    
- etc.
    

---

# 6. URLs

আগে যদি এটা থাকে:

```python
path("api/auth/", include("dj_rest_auth.urls"))
```

Add:

```python
path("api/auth/registration/", include("dj_rest_auth.registration.urls"))
```

---

# 7. Google Login View

`views.py`

```python
from allauth.socialaccount.providers.google.views import GoogleOAuth2Adapter
from dj_rest_auth.registration.views import SocialLoginView
```

```python
class GoogleLogin(SocialLoginView):
    adapter_class = GoogleOAuth2Adapter
```

---

# 8. Route

```python
from .views import GoogleLogin
```

```python
path("api/auth/google/", GoogleLogin.as_view(), name="google_login")
```

---

# 9. Google Cloud OAuth credentials

Open:  
[Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)

Create:

- Project
    
- OAuth Consent Screen
    
- OAuth Client ID
    

পাবে:

```text
CLIENT_ID
CLIENT_SECRET
```

---

# 10. Django Admin → SocialApp

```bash
python manage.py createsuperuser
```

Admin open:

```text
/admin/
```

Add Social App:

- Provider → Google
    
- Client ID
    
- Secret
    
- Sites → example.com
    

---

# Final Flow

Frontend / mobile / Postman:

Google token collect করবে → backend এ পাঠাবে

```json
POST /api/auth/google/

{
   "access_token": "google_token"
}
```

Backend:

1. Google token verify
    
2. user create / login
    
3. JWT return / cookie set
    

---

## তোমার জন্য checklist

Already আছে?

- ✅ `dj_rest_auth`
    
- ✅ JWT
    
- ❓ `dj_rest_auth.registration`
    
- ❓ `allauth`
    

শুধু এগুলো add করলেই social login ready হবে।

একটা জিনিস বলো — তুমি **Google OAuth popup frontend থেকে করবে**, নাকি **pure backend API testing (Postman/Swagger)**?  
কারণ token পাওয়ার part দুটাতে আলাদা।


------------
React থাকলে Google Sign-In অনেক easier — কারণ **frontend Google popup handle করবে**, backend শুধু token verify করবে।

Flow:

```text
React
 ↓
Google popup
 ↓
Google returns credential (id_token)
 ↓
POST Django API
 ↓
Backend verifies token
 ↓
JWT / Cookie
```

---

# Option 1 — React + dj-rest-auth + allauth

Recommended যদি already `dj-rest-auth` use করো।

---

## Step 1: React package install

[@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google?utm_source=chatgpt.com)

```bash
npm install @react-oauth/google
```

---

## Step 2: Provider wrap

```jsx
import { GoogleOAuthProvider } from '@react-oauth/google';
import App from './App';

export default function Root() {
  return (
    <GoogleOAuthProvider clientId="GOOGLE_CLIENT_ID">
      <App />
    </GoogleOAuthProvider>
  );
}
```

---

## Step 3: Login Button

```jsx
import { GoogleLogin } from '@react-oauth/google';

function Login() {
  return (
    <GoogleLogin
      onSuccess={credentialResponse => {
        console.log(credentialResponse);
      }}
      onError={() => console.log("Login Failed")}
    />
  );
}
```

Success response:

```json
{
  "credential": "eyJhbGciOiJSUzI1Ni..."
}
```

এই `credential` = **Google ID Token**

---

# Step 4: Django backend এ পাঠাও

React:

```jsx
const handleGoogleLogin = async (credential) => {
  const res = await fetch(
    "http://127.0.0.1:8000/api/auth/google/",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      credentials: "include",
      body: JSON.stringify({
        token: credential,
      }),
    }
  );

  const data = await res.json();
  console.log(data);
};
```

---

# Step 5: Backend verify

Pure DRF way (আমি এটা prefer করি debugging-এর জন্য)

Install:

```bash
pip install google-auth
```

[google-auth docs](https://google-auth.readthedocs.io/en/latest/?utm_source=chatgpt.com)

Serializer:

```python
from rest_framework import serializers

class GoogleAuthSerializer(serializers.Serializer):
    token = serializers.CharField()
```

---

## API View

```python
from google.oauth2 import id_token
from google.auth.transport import requests
from django.contrib.auth import get_user_model
from rest_framework.views import APIView
from rest_framework.response import Response

User = get_user_model()
```

```python
class GoogleLoginAPIView(APIView):
    def post(self, request):
        token = request.data.get("token")

        info = id_token.verify_oauth2_token(
            token,
            requests.Request()
        )

        email = info["email"]
        name = info.get("name", "")
        picture = info.get("picture", "")

        user, created = User.objects.get_or_create(
            email=email,
            defaults={"username": email}
        )

        return Response({
            "email": email,
            "picture": picture,
            "created": created
        })
```

---

# dj-rest-auth দিয়ে?

Possible, but একটু more magic আছে:

* allauth adapter
* SocialLoginView
* OAuth callback

React SPA-তে অনেকে **allauth বাদ দিয়ে pure DRF + google-auth** use করে।

---

## আমি কী recommend করি?

তুমি যেহেতু:

* DRF শিখছ
* JWT বুঝছ
* custom user করছ
* React use করছ

আমি recommend:

### Traditional Email/Password

→ `dj-rest-auth`

### Google Login

→ **Pure DRF custom endpoint**

কারণ:

✅ Easier debug
✅ Less hidden magic
✅ React-friendly

---

এক লাইনে:

**React app হলে Google Sign-In এর জন্য `dj-rest-auth social` mandatory না — pure DRF endpoint অনেক cleaner।**


-----
React + Django (DRF) এ **pure Google Login** (without `dj-rest-auth social`) করার complete roadmap দিচ্ছি।

Goal:

```text
User clicks Google Login
        ↓
Google popup opens
        ↓
Google returns ID token
        ↓
React sends token to Django
        ↓
Django verifies token
        ↓
Create / get user
        ↓
Issue JWT
        ↓
User logged in
```

---

# Phase 1 — Google OAuth Setup

## Step 1: Google Cloud Project

Open
[Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)

Create:

* New Project
* OAuth Consent Screen
* OAuth Client ID

Choose:

```text
Web Application
```

Add authorized origin:

```text
http://localhost:5173
```

(React Vite example)

Google দেবে:

```text
CLIENT_ID
CLIENT_SECRET
```

**Frontend-এর জন্য mainly `CLIENT_ID` লাগবে**।

---

# Phase 2 — React Frontend

## Step 2: Install package

[@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google?utm_source=chatgpt.com)

```bash
npm install @react-oauth/google
```

---

## Step 3: Provider Setup

```jsx
import { GoogleOAuthProvider } from "@react-oauth/google";
import App from "./App";

function Root() {
  return (
    <GoogleOAuthProvider clientId="YOUR_CLIENT_ID">
      <App />
    </GoogleOAuthProvider>
  );
}

export default Root;
```

---

## Step 4: Login Button

```jsx
import { GoogleLogin } from "@react-oauth/google";

function LoginPage() {
  return (
    <GoogleLogin
      onSuccess={(credentialResponse) => {
        console.log(credentialResponse);
      }}
      onError={() => console.log("Failed")}
    />
  );
}
```

Success হলে:

```json
{
  "credential": "eyJhbGciOiJSUzI1Ni..."
}
```

এটাই **Google ID Token**।

---

# Phase 3 — Django Backend Setup

## Step 5: Install dependencies

```bash
pip install google-auth djangorestframework simplejwt
```

[google-auth docs](https://google-auth.readthedocs.io/en/latest/?utm_source=chatgpt.com)

---

## Step 6: JWT setup

Install
[Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/?utm_source=chatgpt.com)

`settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ]
}
```

---

# Phase 4 — User Model

Minimal custom user recommended:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    email = models.EmailField(unique=True)
    profile_picture = models.URLField(blank=True)
    is_google_user = models.BooleanField(default=False)
```

settings:

```python
AUTH_USER_MODEL = "accounts.User"
```

---

# Phase 5 — Serializer

```python
from rest_framework import serializers

class GoogleAuthSerializer(serializers.Serializer):
    token = serializers.CharField()
```

---

# Phase 6 — Google Token Verification

## Step 7: Verify token

```python
from google.oauth2 import id_token
from google.auth.transport import requests
```

Google token থেকে পাওয়া যায়:

* email
* name
* picture
* email_verified

---

# Phase 7 — Login API

## Step 8: API View

```python
from google.oauth2 import id_token
from google.auth.transport import requests
from django.contrib.auth import get_user_model
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from rest_framework_simplejwt.tokens import RefreshToken

User = get_user_model()


class GoogleLoginAPIView(APIView):
    def post(self, request):
        token = request.data.get("token")

        if not token:
            return Response(
                {"error": "Token required"},
                status=400
            )

        try:
            info = id_token.verify_oauth2_token(
                token,
                requests.Request()
            )

            email = info["email"]
            name = info.get("name", "")
            picture = info.get("picture", "")

            user, created = User.objects.get_or_create(
                email=email,
                defaults={
                    "username": email,
                    "first_name": name,
                    "profile_picture": picture,
                    "is_google_user": True,
                },
            )

            refresh = RefreshToken.for_user(user)

            return Response({
                "access": str(refresh.access_token),
                "refresh": str(refresh),
                "user": {
                    "id": user.id,
                    "email": user.email,
                    "username": user.username
                }
            })

        except Exception as e:
            return Response(
                {"error": str(e)},
                status=status.HTTP_400_BAD_REQUEST
            )
```

---

# Phase 8 — URL

```python
from django.urls import path
from .views import GoogleLoginAPIView

urlpatterns = [
    path("auth/google/", GoogleLoginAPIView.as_view()),
]
```

---

# Phase 9 — React → Backend

## Step 9: Send token

```jsx
const handleGoogleSuccess = async (credentialResponse) => {
  const response = await fetch(
    "http://127.0.0.1:8000/api/auth/google/",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        token: credentialResponse.credential,
      }),
    }
  );

  const data = await response.json();
  console.log(data);
};
```

---

# Phase 10 — Store JWT

Option:

### localStorage

```javascript
localStorage.setItem("access", data.access);
```

OR

### secure cookie (better)

Backend cookie set:

```python
response.set_cookie(...)
```

---

# Phase 11 — Protected APIs

JWT header:

```http
Authorization: Bearer ACCESS_TOKEN
```

Example:

```javascript
fetch("/api/orders", {
  headers: {
    Authorization: `Bearer ${token}`
  }
})
```

---

# Phase 12 — Logout

Frontend:

```javascript
localStorage.removeItem("access");
localStorage.removeItem("refresh");
```

Google logout (optional):

```javascript
googleLogout();
```

---

# Advanced Production Topics

Later শিখবে:

### Refresh token rotation

### Token blacklist

### Silent re-login

### Account linking

(email/password + Google same account)

### Multi-provider login

* Google
* GitHub
* Facebook

---

# Recommended Learning Order

```text
1. React Google popup
2. ID token
3. Backend verify token
4. User create/get
5. JWT issue
6. Protected API
7. Refresh token
8. Logout
```

এটাই **pure Google Login roadmap**—industry-তে React SPA + DRF backend-এর common pattern।


------
Multi-provider social login (Google + GitHub + Facebook) production-ready roadmap দিচ্ছি — **React SPA + Django DRF + JWT** architecture ধরে।

High-level flow সব provider-এর জন্য same:

```text
User clicks provider button
        ↓
Provider OAuth popup
        ↓
Provider returns token / code
        ↓
React sends token/code to DRF
        ↓
Backend verifies with provider
        ↓
Get user profile
        ↓
Find existing account / create new
        ↓
Issue JWT
        ↓
Authenticated session
```

---

# Phase 0 — Architecture Design

Production-এ সাধারণত ৩টা model রাখি:

## User

```python
User
- id
- email
- username
- password (nullable for social)
- is_active
```

## SocialAccount

```python
SocialAccount
- user (FK)
- provider
- provider_user_id
- provider_email
- avatar
```

## Profile

```python
Profile
- phone
- address
- picture
```

Reason:

* এক user multiple provider use করতে পারবে
* account linking possible
* clean architecture

---

# Phase 1 — Frontend OAuth Layer

React packages:

### Google

[@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google?utm_source=chatgpt.com)

### GitHub

সাধারণ OAuth redirect flow

### Facebook

[react-facebook-login docs](https://developers.facebook.com/docs/facebook-login/?utm_source=chatgpt.com)

---

# UI

```text
Login with Google
Login with GitHub
Login with Facebook
```

---

# Phase 2 — OAuth Setup per Provider

---

## Google

Create app in
[Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)

Need:

* Client ID
* Client Secret

Scopes:

```text
openid
email
profile
```

Returns:

* id_token
* email
* name
* picture

---

## GitHub

Create OAuth app in
[GitHub Developer Settings](https://github.com/settings/developers?utm_source=chatgpt.com)

Need:

* Client ID
* Client Secret

Scopes:

```text
read:user
user:email
```

Returns:

* code
* access_token
* username
* emails

Important:

GitHub email sometimes private.

Need extra API call:

```text
GET /user/emails
```

---

## Facebook

Create app in
[Meta for Developers](https://developers.facebook.com/?utm_source=chatgpt.com)

Need:

* App ID
* App Secret

Scopes:

```text
public_profile
email
```

Returns:

* access_token
* id
* name
* picture

---

# Phase 3 — Backend Models

Custom user:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models
```

```python
class User(AbstractUser):
    email = models.EmailField(unique=True)
```

---

Social Account:

```python
class SocialAccount(models.Model):
    PROVIDERS = (
        ("google", "Google"),
        ("github", "GitHub"),
        ("facebook", "Facebook"),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE)
    provider = models.CharField(max_length=30, choices=PROVIDERS)
    provider_user_id = models.CharField(max_length=255)
    avatar = models.URLField(blank=True)

    class Meta:
        unique_together = ("provider", "provider_user_id")
```

Critical:

```text
same provider user cannot duplicate
```

---

# Phase 4 — DRF Endpoint Design

3টা endpoint করতে পারো:

```text
POST /api/auth/google/
POST /api/auth/github/
POST /api/auth/facebook/
```

অথবা single endpoint:

```text
POST /api/auth/social/
```

Request:

```json
{
  "provider": "google",
  "token": "..."
}
```

Single endpoint scalable.

আমি এটাকেই recommend করি.

---

# Phase 5 — Token Verification

Provider অনুযায়ী verification আলাদা।

---

## Google verify

Install:

```bash
pip install google-auth
```

Use:

```python
google.oauth2.id_token.verify_oauth2_token()
```

Verify:

* token signature
* issuer
* expiration

---

## GitHub verify

GitHub token verify direct হয় না।

Need API calls:

1.

```text
https://api.github.com/user
```

2.

```text
https://api.github.com/user/emails
```

Use:

[GitHub REST API](https://docs.github.com/en/rest?utm_source=chatgpt.com)

---

## Facebook verify

API call:

```text
https://graph.facebook.com/me
```

Use:

[Facebook Graph API](https://developers.facebook.com/docs/graph-api?utm_source=chatgpt.com)

---

# Phase 6 — Provider Services Layer

Production architecture:

```text
services/
    google.py
    github.py
    facebook.py
```

Example:

```python
class GoogleService:
    def verify(self, token):
        ...
```

```python
class GithubService:
    def verify(self, token):
        ...
```

Cleaner than huge views.

---

# Phase 7 — Normalize Provider Data

সব provider data এক format-এ convert করো:

```python
{
    "provider_user_id": "...",
    "email": "...",
    "name": "...",
    "avatar": "..."
}
```

Reason:

Google/GitHub/Facebook response আলাদা।

Normalize করলে rest of code same।

---

# Phase 8 — Account Linking Logic

Most important production topic.

Case:

User আগে email/password account বানিয়েছে:

```text
abc@gmail.com
```

পরে Google login করলো same email.

কি করবে?

---

Option A (Recommended)

Auto-link:

```text
same email → link social account
```

---

Option B

Reject:

```text
Email already exists
```

User-friendly না।

---

Pseudo:

```python
existing_user = User.objects.filter(email=email).first()
```

If exists:

```text
attach provider
```

Else:

```text
create user
```

---

# Phase 9 — Social Login Service

Pseudo:

```python
def social_login(provider, token):
    data = verify_provider(provider, token)

    user = get_user_by_email(data["email"])

    if not user:
        user = create_user()

    social = create_or_get_social_account()

    return jwt_for_user(user)
```

---

# Phase 10 — JWT

Use:

[Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/?utm_source=chatgpt.com)

Response:

```json
{
    "access": "...",
    "refresh": "...",
    "user": {}
}
```

---

# Phase 11 — Refresh Flow

Endpoint:

```text
POST /api/auth/token/refresh/
```

When access expires:

```text
refresh token -> new access token
```

Important for SPA.

---

# Phase 12 — Protected APIs

Use:

```http
Authorization: Bearer ACCESS_TOKEN
```

Example:

```text
GET /api/orders/
```

---

# Phase 13 — Logout

Two layers:

### App logout

Delete JWT:

```javascript
localStorage.clear()
```

### Provider logout

Optional.

Google:

```javascript
googleLogout()
```

GitHub/Facebook often শুধু app logout enough.

---

# Phase 14 — Security

Production checklist:

### State param

Prevent CSRF in OAuth

### Nonce

Prevent replay

### Token expiration check

### Rate limiting

### Email verification rules

### Secure cookies

Prefer cookies over localStorage

---

# Phase 15 — Edge Cases

Must handle:

---

## Provider email missing

GitHub common case.

Need fallback:

```text
ask user email
```

---

## Email changed at provider

Need sync policy.

---

## Same user multiple providers

Example:

* Google
* GitHub

Same account link.

---

## Account deletion

Delete:

* user
* linked socials

---

# Recommended Learning Order

```text
1. JWT auth
2. Google login
3. GitHub login
4. Facebook login
5. SocialAccount model
6. Account linking
7. Refresh tokens
8. Security hardening
```

---

# Recommended Project Structure

```text
accounts/
    models.py
    serializers.py
    views.py
    urls.py

services/
    google.py
    github.py
    facebook.py

auth/
    jwt.py
```

---

Production roadmap summary:

```text
OAuth Provider
      ↓
Frontend gets token
      ↓
Backend verifies token
      ↓
Normalize provider data
      ↓
Find/create user
      ↓
Link social account
      ↓
Issue JWT
      ↓
Authenticated user
```

এটাই scalable architecture—Google, GitHub, Facebook ছাড়াও পরে **Apple / Discord / LinkedIn** add করা যাবে without major rewrite।


---------
Multi-provider social login (Google + GitHub + Facebook) production-ready roadmap দিচ্ছি — **React SPA + Django DRF + JWT** architecture ধরে।

High-level flow সব provider-এর জন্য same:

```text
User clicks provider button
        ↓
Provider OAuth popup
        ↓
Provider returns token / code
        ↓
React sends token/code to DRF
        ↓
Backend verifies with provider
        ↓
Get user profile
        ↓
Find existing account / create new
        ↓
Issue JWT
        ↓
Authenticated session
```

---

# Phase 0 — Architecture Design

Production-এ সাধারণত ৩টা model রাখি:

## User

```python
User
- id
- email
- username
- password (nullable for social)
- is_active
```

## SocialAccount

```python
SocialAccount
- user (FK)
- provider
- provider_user_id
- provider_email
- avatar
```

## Profile

```python
Profile
- phone
- address
- picture
```

Reason:

* এক user multiple provider use করতে পারবে
* account linking possible
* clean architecture

---

# Phase 1 — Frontend OAuth Layer

React packages:

### Google

[@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google?utm_source=chatgpt.com)

### GitHub

সাধারণ OAuth redirect flow

### Facebook

[react-facebook-login docs](https://developers.facebook.com/docs/facebook-login/?utm_source=chatgpt.com)

---

# UI

```text
Login with Google
Login with GitHub
Login with Facebook
```

---

# Phase 2 — OAuth Setup per Provider

---

## Google

Create app in
[Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)

Need:

* Client ID
* Client Secret

Scopes:

```text
openid
email
profile
```

Returns:

* id_token
* email
* name
* picture

---

## GitHub

Create OAuth app in
[GitHub Developer Settings](https://github.com/settings/developers?utm_source=chatgpt.com)

Need:

* Client ID
* Client Secret

Scopes:

```text
read:user
user:email
```

Returns:

* code
* access_token
* username
* emails

Important:

GitHub email sometimes private.

Need extra API call:

```text
GET /user/emails
```

---

## Facebook

Create app in
[Meta for Developers](https://developers.facebook.com/?utm_source=chatgpt.com)

Need:

* App ID
* App Secret

Scopes:

```text
public_profile
email
```

Returns:

* access_token
* id
* name
* picture

---

# Phase 3 — Backend Models

Custom user:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models
```

```python
class User(AbstractUser):
    email = models.EmailField(unique=True)
```

---

Social Account:

```python
class SocialAccount(models.Model):
    PROVIDERS = (
        ("google", "Google"),
        ("github", "GitHub"),
        ("facebook", "Facebook"),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE)
    provider = models.CharField(max_length=30, choices=PROVIDERS)
    provider_user_id = models.CharField(max_length=255)
    avatar = models.URLField(blank=True)

    class Meta:
        unique_together = ("provider", "provider_user_id")
```

Critical:

```text
same provider user cannot duplicate
```

---

# Phase 4 — DRF Endpoint Design

3টা endpoint করতে পারো:

```text
POST /api/auth/google/
POST /api/auth/github/
POST /api/auth/facebook/
```

অথবা single endpoint:

```text
POST /api/auth/social/
```

Request:

```json
{
  "provider": "google",
  "token": "..."
}
```

Single endpoint scalable.

আমি এটাকেই recommend করি.

---

# Phase 5 — Token Verification

Provider অনুযায়ী verification আলাদা।

---

## Google verify

Install:

```bash
pip install google-auth
```

Use:

```python
google.oauth2.id_token.verify_oauth2_token()
```

Verify:

* token signature
* issuer
* expiration

---

## GitHub verify

GitHub token verify direct হয় না।

Need API calls:

1.

```text
https://api.github.com/user
```

2.

```text
https://api.github.com/user/emails
```

Use:

[GitHub REST API](https://docs.github.com/en/rest?utm_source=chatgpt.com)

---

## Facebook verify

API call:

```text
https://graph.facebook.com/me
```

Use:

[Facebook Graph API](https://developers.facebook.com/docs/graph-api?utm_source=chatgpt.com)

---

# Phase 6 — Provider Services Layer

Production architecture:

```text
services/
    google.py
    github.py
    facebook.py
```

Example:

```python
class GoogleService:
    def verify(self, token):
        ...
```

```python
class GithubService:
    def verify(self, token):
        ...
```

Cleaner than huge views.

---

# Phase 7 — Normalize Provider Data

সব provider data এক format-এ convert করো:

```python
{
    "provider_user_id": "...",
    "email": "...",
    "name": "...",
    "avatar": "..."
}
```

Reason:

Google/GitHub/Facebook response আলাদা।

Normalize করলে rest of code same।

---

# Phase 8 — Account Linking Logic

Most important production topic.

Case:

User আগে email/password account বানিয়েছে:

```text
abc@gmail.com
```

পরে Google login করলো same email.

কি করবে?

---

Option A (Recommended)

Auto-link:

```text
same email → link social account
```

---

Option B

Reject:

```text
Email already exists
```

User-friendly না।

---

Pseudo:

```python
existing_user = User.objects.filter(email=email).first()
```

If exists:

```text
attach provider
```

Else:

```text
create user
```

---

# Phase 9 — Social Login Service

Pseudo:

```python
def social_login(provider, token):
    data = verify_provider(provider, token)

    user = get_user_by_email(data["email"])

    if not user:
        user = create_user()

    social = create_or_get_social_account()

    return jwt_for_user(user)
```

---

# Phase 10 — JWT

Use:

[Simple JWT](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/?utm_source=chatgpt.com)

Response:

```json
{
    "access": "...",
    "refresh": "...",
    "user": {}
}
```

---

# Phase 11 — Refresh Flow

Endpoint:

```text
POST /api/auth/token/refresh/
```

When access expires:

```text
refresh token -> new access token
```

Important for SPA.

---

# Phase 12 — Protected APIs

Use:

```http
Authorization: Bearer ACCESS_TOKEN
```

Example:

```text
GET /api/orders/
```

---

# Phase 13 — Logout

Two layers:

### App logout

Delete JWT:

```javascript
localStorage.clear()
```

### Provider logout

Optional.

Google:

```javascript
googleLogout()
```

GitHub/Facebook often শুধু app logout enough.

---

# Phase 14 — Security

Production checklist:

### State param

Prevent CSRF in OAuth

### Nonce

Prevent replay

### Token expiration check

### Rate limiting

### Email verification rules

### Secure cookies

Prefer cookies over localStorage

---

# Phase 15 — Edge Cases

Must handle:

---

## Provider email missing

GitHub common case.

Need fallback:

```text
ask user email
```

---

## Email changed at provider

Need sync policy.

---

## Same user multiple providers

Example:

* Google
* GitHub

Same account link.

---

## Account deletion

Delete:

* user
* linked socials

---

# Recommended Learning Order

```text
1. JWT auth
2. Google login
3. GitHub login
4. Facebook login
5. SocialAccount model
6. Account linking
7. Refresh tokens
8. Security hardening
```

---

# Recommended Project Structure

```text
accounts/
    models.py
    serializers.py
    views.py
    urls.py

services/
    google.py
    github.py
    facebook.py

auth/
    jwt.py
```

---

Production roadmap summary:

```text
OAuth Provider
      ↓
Frontend gets token
      ↓
Backend verifies token
      ↓
Normalize provider data
      ↓
Find/create user
      ↓
Link social account
      ↓
Issue JWT
      ↓
Authenticated user
```

এটাই scalable architecture—Google, GitHub, Facebook ছাড়াও পরে **Apple / Discord / LinkedIn** add করা যাবে without major rewrite।

---------
ভালো question — social login-এর core concept এটাতেই।

**Frontend token provider (Google/GitHub/Facebook) থেকেই পায়**, তোমার backend থেকে না।

Flow:

```text
React App
   ↓
Provider SDK / OAuth page
   ↓
User login + consent
   ↓
Provider token দেয় frontend-কে
   ↓
Frontend token backend-এ পাঠায়
```

---

## Google

React package:

[@react-oauth/google](https://www.npmjs.com/package/@react-oauth/google?utm_source=chatgpt.com)

Example:

```jsx
<GoogleLogin
  onSuccess={(response) => {
    console.log(response);
  }}
/>
```

Google success response:

```json
{
  "credential": "eyJhbGciOiJSUzI1Ni..."
}
```

এই `credential`-টাই token (`id_token`)।

মানে token আসছে:

```text
Google popup → React callback
```

---

## GitHub

GitHub সাধারণত **token direct browser-এ দেয় না** (Authorization Code Flow বেশি common)।

Flow:

```text
React
 ↓
redirect to github.com/login/oauth/authorize
 ↓
User login
 ↓
GitHub redirect back with code
```

Callback URL:

```text
http://localhost:5173/auth/github/callback?code=abc123
```

React URL থেকে `code` extract করে:

```javascript
const code = searchParams.get("code")
```

এই code backend-এ পাঠাও।

Backend:

```text
code → GitHub access token exchange
```

---

## Facebook

Facebook JS SDK / OAuth popup use হয়।

[Meta Facebook Login Docs](https://developers.facebook.com/docs/facebook-login/?utm_source=chatgpt.com)

Success হলে:

```json
{
  "accessToken": "EAA..."
}
```

এই token frontend পায়।

---

# Two OAuth patterns

এখানে main difference:

---

## Pattern 1 — Implicit / Token Flow

Provider token frontend-এ দেয়।

Examples:

* Google
* Facebook (often)

Flow:

```text
Provider → Frontend gets token → Backend verify
```

---

## Pattern 2 — Authorization Code Flow

Provider frontend-এ token দেয় না, code দেয়।

Examples:

* GitHub
* অনেক enterprise providers

Flow:

```text
Provider → code
Backend → exchange code for token
```

---

# React এ token কোথায় store হয়?

Temporary variable:

```javascript
onSuccess={(res)=> {
   console.log(res.credential)
}}
```

তারপর:

```javascript
fetch("/api/auth/google/", {
   method: "POST",
   body: JSON.stringify({
      token: res.credential
   })
})
```

---

# Important distinction

Social login-এ usually **২ ধরনের token** থাকে:

### Provider token

Google/GitHub/Facebook দেয়

Example:

```text
google_id_token
```

এটা শুধু identity verify করতে।

---

### Your app token

তোমার Django JWT

Example:

```text
access_token
refresh_token
```

এটা protected API call করতে।

---

Summary:

| Provider | Frontend কী পায়    |
| -------- | ------------------ |
| Google   | id_token           |
| GitHub   | authorization code |
| Facebook | access_token       |

এক লাইনে:

> frontend token পায় provider-এর **OAuth SDK / popup / redirect callback** থেকে।

--------
```tsx
import { useEffect, useState } from "react";
import axios from "axios";
import { GoogleOAuthProvider, GoogleLogin } from "@react-oauth/google";
import { useLocation, useNavigate } from "react-router-dom";

type SocialProvider = "google" | "github" | "facebook";

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || "";
const GOOGLE_CLIENT_ID = import.meta.env.VITE_GOOGLE_CLIENT_ID || "";
const FACEBOOK_APP_ID = import.meta.env.VITE_FACEBOOK_APP_ID || "";
const GITHUB_CLIENT_ID = import.meta.env.VITE_GITHUB_CLIENT_ID || "";

function saveAuth(data: any) {
  if (data?.access) localStorage.setItem("access", data.access);
  if (data?.refresh) localStorage.setItem("refresh", data.refresh);
  if (data?.user) localStorage.setItem("user", JSON.stringify(data.user));
}

async function socialLogin(payload: Record<string, any>) {
  const res = await axios.post(`${API_BASE_URL}/api/auth/social/`, payload, {
    withCredentials: true,
  });
  saveAuth(res.data);
  return res.data;
}

export default function SocialLoginButtons() {
  const location = useLocation();
  const navigate = useNavigate();
  const [loading, setLoading] = useState<SocialProvider | null>(null);
  const [error, setError] = useState<string>("");

  useEffect(() => {
    const params = new URLSearchParams(location.search);
    const provider = params.get("provider");
    const code = params.get("code");
    const errorParam = params.get("error");

    if (errorParam) {
      setError(`GitHub login failed: ${errorParam}`);
      return;
    }

    if (provider === "github" && code) {
      (async () => {
        try {
          setLoading("github");
          setError("");
          await socialLogin({
            provider: "github",
            code,
            callback_url: `${window.location.origin}/login/social/callback`,
          });
          navigate("/dashboard");
        } catch (err: any) {
          setError(
            err?.response?.data?.detail ||
              err?.response?.data?.non_field_errors?.[0] ||
              "GitHub login failed"
          );
        } finally {
          setLoading(null);
        }
      })();
    }
  }, [location.search, navigate]);

  const handleFacebookLogin = async () => {
    setLoading("facebook");
    setError("");

    try {
      const fb = (window as any).FB;
      if (!fb) {
        throw new Error("Facebook SDK is not loaded");
      }

      fb.login(
        async (response: any) => {
          try {
            if (!response?.authResponse?.accessToken) {
              throw new Error("Facebook login cancelled");
            }

            await socialLogin({
              provider: "facebook",
              access_token: response.authResponse.accessToken,
            });

            navigate("/dashboard");
          } catch (err: any) {
            setError(
              err?.response?.data?.detail ||
                err?.response?.data?.non_field_errors?.[0] ||
                err?.message ||
                "Facebook login failed"
            );
          } finally {
            setLoading(null);
          }
        },
        { scope: "public_profile,email" }
      );
    } catch (err: any) {
      setError(err.message || "Facebook login failed");
      setLoading(null);
    }
  };

  const handleGithubLogin = () => {
    setError("");
    setLoading("github");

    const redirectUri = `${window.location.origin}/login/social/callback`;
    const scope = encodeURIComponent("read:user user:email");

    const githubUrl =
      `https://github.com/login/oauth/authorize` +
      `?client_id=${encodeURIComponent(GITHUB_CLIENT_ID)}` +
      `&redirect_uri=${encodeURIComponent(redirectUri)}` +
      `&scope=${scope}`;

    window.location.href = githubUrl;
  };

  return (
    <GoogleOAuthProvider clientId={GOOGLE_CLIENT_ID}>
      <div style={styles.wrapper}>
        <div style={styles.card}>
          <h2 style={styles.title}>Sign in</h2>
          <p style={styles.subtitle}>Use one of your social accounts to continue.</p>

          <div style={styles.stack}>
            <div style={styles.buttonWrap}>
              <GoogleLogin
                onSuccess={async (credentialResponse) => {
                  try {
                    setLoading("google");
                    setError("");

                    const credential =
                      credentialResponse.credential ||
                      credentialResponse.select_by ||
                      "";

                    if (!credential) {
                      throw new Error("Google credential not found");
                    }

                    await socialLogin({
                      provider: "google",
                      credential,
                    });

                    navigate("/dashboard");
                  } catch (err: any) {
                    setError(
                      err?.response?.data?.detail ||
                        err?.response?.data?.non_field_errors?.[0] ||
                        err?.message ||
                        "Google login failed"
                    );
                  } finally {
                    setLoading(null);
                  }
                }}
                onError={() => {
                  setError("Google login failed");
                }}
                useOneTap={false}
                theme="outline"
                shape="rectangular"
                size="large"
                text="signin_with"
                width="320"
              />
            </div>

            <button
              type="button"
              onClick={handleGithubLogin}
              disabled={loading !== null}
              style={{ ...styles.button, ...styles.githubButton }}
            >
              {loading === "github" ? "Connecting..." : "Continue with GitHub"}
            </button>

            <button
              type="button"
              onClick={handleFacebookLogin}
              disabled={loading !== null}
              style={{ ...styles.button, ...styles.facebookButton }}
            >
              {loading === "facebook" ? "Connecting..." : "Continue with Facebook"}
            </button>
          </div>

          {error ? <p style={styles.error}>{error}</p> : null}
        </div>
      </div>
    </GoogleOAuthProvider>
  );
}

const styles: Record<string, React.CSSProperties> = {
  wrapper: {
    minHeight: "100vh",
    display: "grid",
    placeItems: "center",
    padding: "24px",
    background:
      "radial-gradient(circle at top, #1b2a4a 0%, #0f172a 45%, #020617 100%)",
    color: "#e2e8f0",
  },
  card: {
    width: "100%",
    maxWidth: "420px",
    borderRadius: "24px",
    padding: "32px",
    background: "rgba(15, 23, 42, 0.72)",
    backdropFilter: "blur(16px)",
    border: "1px solid rgba(148, 163, 184, 0.18)",
    boxShadow: "0 24px 80px rgba(0, 0, 0, 0.35)",
  },
  title: {
    margin: 0,
    fontSize: "2rem",
    fontWeight: 700,
    letterSpacing: "-0.03em",
  },
  subtitle: {
    marginTop: "8px",
    marginBottom: "24px",
    color: "#94a3b8",
    lineHeight: 1.6,
  },
  stack: {
    display: "grid",
    gap: "14px",
  },
  buttonWrap: {
    display: "flex",
    justifyContent: "center",
  },
  button: {
    height: "48px",
    border: "none",
    borderRadius: "12px",
    fontSize: "15px",
    fontWeight: 600,
    cursor: "pointer",
    color: "#fff",
    transition: "transform 0.15s ease, opacity 0.15s ease",
  },
  githubButton: {
    background: "#111827",
    border: "1px solid rgba(255,255,255,0.08)",
  },
  facebookButton: {
    background: "#1877f2",
  },
  error: {
    marginTop: "18px",
    color: "#fca5a5",
    fontSize: "14px",
    lineHeight: 1.5,
  },
};
```

**React router setup**
- GitHub callback route লাগবে: `/login/social/callback`
- Example:
```tsx
<Route path="/login/social/callback" element={<SocialLoginButtons />} />
<Route path="/login" element={<SocialLoginButtons />} />
```

**Env vars**
```env
VITE_API_BASE_URL=http://127.0.0.1:8000
VITE_GOOGLE_CLIENT_ID=xxx
VITE_FACEBOOK_APP_ID=xxx
VITE_GITHUB_CLIENT_ID=xxx
```

**Important**
- Google frontend flow এখানে `credential` পাঠাচ্ছে backend-এ।
- GitHub redirect করে `code` নেয়, তারপর same component সেটা backend-এ পাঠায়।
- Facebook SDK load করতে হবে; না হলে আমি next step-এ সেটার script loader componentও দিয়ে দিতে পারি।

চাইলে আমি এখনই এই component-এর সাথে কাজ করার জন্য `Facebook SDK loader + GitHub callback helper`ও দিয়ে দিই।

--------
তোমার React component বেশ solid — backend-এর জন্য এখন একটা **single social endpoint** বানালেই তিন provider handle করতে পারবে।

তোমার frontend payload already clear:

### Google

```json
{
  "provider": "google",
  "credential": "GOOGLE_ID_TOKEN"
}
```

### GitHub

```json
{
  "provider": "github",
  "code": "GITHUB_AUTH_CODE",
  "callback_url": "http://localhost:5173/login/social/callback"
}
```

### Facebook

```json
{
  "provider": "facebook",
  "access_token": "FACEBOOK_ACCESS_TOKEN"
}
```

এখন backend roadmap + code structure:

---

# 1. Serializer

সব optional রাখবে, কিন্তু provider অনুযায়ী validate করবে।

```python
from rest_framework import serializers


class SocialLoginSerializer(serializers.Serializer):
    PROVIDERS = (
        ("google", "Google"),
        ("github", "GitHub"),
        ("facebook", "Facebook"),
    )

    provider = serializers.ChoiceField(choices=PROVIDERS)
    access_token = serializers.CharField(required=False)
    token = serializers.CharField(required=False)
    credential = serializers.CharField(required=False)
    id_token = serializers.CharField(required=False)
    code = serializers.CharField(required=False)
    callback_url = serializers.URLField(required=False)

    def validate(self, attrs):
        provider = attrs.get("provider")

        if provider == "google":
            if not (
                attrs.get("credential")
                or attrs.get("id_token")
                or attrs.get("token")
            ):
                raise serializers.ValidationError(
                    "Google requires credential or id_token"
                )

        elif provider == "github":
            if not attrs.get("code"):
                raise serializers.ValidationError(
                    "GitHub requires code"
                )

        elif provider == "facebook":
            if not attrs.get("access_token"):
                raise serializers.ValidationError(
                    "Facebook requires access_token"
                )

        return attrs
```

---

# 2. Service Layer

Project structure:

```text
accounts/
    services/
        google.py
        github.py
        facebook.py
```

---

## Google Service

Install:

```bash
pip install google-auth
```

```python
from google.oauth2 import id_token
from google.auth.transport import requests


def verify_google(token):
    info = id_token.verify_oauth2_token(
        token,
        requests.Request()
    )

    return {
        "provider_user_id": info["sub"],
        "email": info["email"],
        "name": info.get("name", ""),
        "avatar": info.get("picture", "")
    }
```

---

## GitHub Service

GitHub flow:

```text
code
↓
exchange code for access token
↓
call user api
```

Need:

* Client ID
* Client Secret

Use
[GitHub OAuth docs](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/authorizing-oauth-apps?utm_source=chatgpt.com)

Pseudo:

```python
def verify_github(code):
    # code -> access token
    # access token -> user info
    pass
```

---

## Facebook Service

Use Graph API
[Facebook Graph API docs](https://developers.facebook.com/docs/graph-api?utm_source=chatgpt.com)

```python
def verify_facebook(access_token):
    pass
```

---

# 3. SocialAccount Model

```python
from django.db import models
from django.conf import settings


class SocialAccount(models.Model):
    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE
    )

    provider = models.CharField(max_length=20)
    provider_user_id = models.CharField(max_length=255)
    avatar = models.URLField(blank=True)

    class Meta:
        unique_together = (
            "provider",
            "provider_user_id"
        )
```

---

# 4. User Resolver

সব provider normalized data return করবে:

```python
{
    "provider_user_id": "...",
    "email": "...",
    "name": "...",
    "avatar": "..."
}
```

তারপর common logic:

```python
from django.contrib.auth import get_user_model

User = get_user_model()


def get_or_create_social_user(provider, data):
    email = data["email"]

    user = User.objects.filter(email=email).first()

    if not user:
        user = User.objects.create_user(
            username=email,
            email=email
        )

    SocialAccount.objects.get_or_create(
        user=user,
        provider=provider,
        provider_user_id=data["provider_user_id"],
        defaults={"avatar": data.get("avatar", "")}
    )

    return user
```

---

# 5. JWT Issue

যেহেতু তুমি JWT জানো, use:

[Simple JWT docs](https://django-rest-framework-simplejwt.readthedocs.io/en/latest/?utm_source=chatgpt.com)

```python
from rest_framework_simplejwt.tokens import RefreshToken
```

```python
def jwt_for_user(user):
    refresh = RefreshToken.for_user(user)

    return {
        "access": str(refresh.access_token),
        "refresh": str(refresh),
    }
```

---

# 6. API View

```python
from rest_framework.views import APIView
from rest_framework.response import Response
```

```python
class SocialLoginAPIView(APIView):
    def post(self, request):
        serializer = SocialLoginSerializer(
            data=request.data
        )
        serializer.is_valid(raise_exception=True)

        provider = serializer.validated_data["provider"]

        if provider == "google":
            token = (
                serializer.validated_data.get("credential")
                or serializer.validated_data.get("id_token")
            )
            social_data = verify_google(token)

        elif provider == "github":
            social_data = verify_github(
                serializer.validated_data["code"]
            )

        else:
            social_data = verify_facebook(
                serializer.validated_data["access_token"]
            )

        user = get_or_create_social_user(
            provider,
            social_data
        )

        tokens = jwt_for_user(user)

        return Response({
            **tokens,
            "user": {
                "id": user.id,
                "email": user.email,
            }
        })
```

---

# 7. URL

```python
path(
    "api/auth/social/",
    SocialLoginAPIView.as_view()
)
```

---

# তোমার React code সম্পর্কে 3টা note

## 1. Google bug

এখানে:

```tsx
credentialResponse.select_by
```

এটা token না।

Bug:

```tsx
const credential =
    credentialResponse.credential ||
    credentialResponse.select_by
```

`select_by` remove করো।

Correct:

```tsx
const credential = credentialResponse.credential;
```

---

## 2. localStorage

তুমি:

```tsx
localStorage.setItem("access", ...)
```

Production-এ safer:

* httpOnly cookie
* secure cookie

---

## 3. GitHub security

GitHub login-এ `state` param add করো।

Current:

```tsx
https://github.com/login/oauth/authorize
```

Add:

```tsx
&state=random_secure_string
```

Reason:

CSRF protection.

---

# Final Architecture

```text
React
 ├── Google SDK
 ├── GitHub OAuth
 └── Facebook SDK
         ↓
POST /api/auth/social/
         ↓
Serializer Validation
         ↓
Provider Service
         ↓
Normalize Data
         ↓
Create / Get User
         ↓
Issue JWT
         ↓
Authenticated User
```

এখন যদি complete production code চাও, next step হবে:

1. `verify_github()` full implementation
2. `verify_facebook()` full implementation
3. cookie-based JWT integration
4. refresh token rotation

এগুলো করলে architecture production-ready হয়ে যাবে।

---------
তোমার `SocialLoginButtons` component render হলে UI roughly এমন দেখাবে:

```text
┌──────────────────────────────────────┐
│              Sign in                 │
│ Use one of your social accounts      │
│ to continue.                         │
│                                      │
│   [ Continue with Google ]           │
│                                      │
│   [ Continue with GitHub ]           │
│                                      │
│   [ Continue with Facebook ]         │
│                                      │
│   (error message if failed)          │
└──────────────────────────────────────┘
```

---

## Initial Render

Page load হলে:

* full screen center card
* dark gradient background
* 3 social buttons

React tree:

```jsx
<GoogleOAuthProvider>
   <div wrapper>
      <div card>
         <h2>Sign in</h2>
         <p>subtitle</p>
         <GoogleLogin />
         <Github button />
         <Facebook button />
      </div>
   </div>
</GoogleOAuthProvider>
```

---

## Google button output

`@react-oauth/google` নিজের button render করে:

```text
┌──────────────────────────────┐
│  G  Sign in with Google      │
└──────────────────────────────┘
```

Click করলে popup:

```text
Choose account
--------------
user1@gmail.com
user2@gmail.com
```

Success callback:

```js
{
  credential: "eyJhbGc..."
}
```

---

## GitHub button output

Normal HTML button:

```text
┌──────────────────────────────┐
│   Continue with GitHub       │
└──────────────────────────────┘
```

Click করলে:

```js
window.location.href = githubUrl
```

Browser redirect:

```text
github.com/login/oauth/authorize...
```

GitHub login page:

Success redirect back:

```text
http://localhost:5173/login/social/callback?code=abc123
```

তারপর `useEffect` auto detect করবে:

```ts
provider === "github"
code exists
```

Backend call:

```ts
socialLogin({
   provider:"github",
   code
})
```

---

## Facebook button output

```text
┌──────────────────────────────┐
│ Continue with Facebook       │
└──────────────────────────────┘
```

Click:

```js
FB.login(...)
```

Popup:

Success response:

```js
{
   authResponse: {
      accessToken: "EAA..."
   }
}
```

---

# Loading state output

Google click করলে:

GitHub/Facebook disabled:

```text
Google -> popup open
GitHub button disabled
Facebook button disabled
```

GitHub login চললে button text বদলাবে:

```text
Connecting...
```

Because:

```tsx
loading === "github"
```

---

# Error output

যদি backend fail করে:

```text
Google login failed
```

Card bottom এ red text:

```tsx
{error ? <p>{error}</p> : null}
```

Example UI:

```text
Continue with Facebook

❌ Invalid token
```

---

# Success output

Success হলে:

1. localStorage save

```js
access
refresh
user
```

2. redirect

```js
navigate("/dashboard")
```

Dashboard page:

```text
Welcome user@example.com
```

---

## Backend response expected

Component এই shape expect করছে:

```json
{
  "access": "jwt_access",
  "refresh": "jwt_refresh",
  "user": {
    "id": 1,
    "email": "abc@gmail.com"
  }
}
```

না হলে:

```ts
saveAuth()
```

properly কাজ করবে না।

---

তোমার component-এর final behavior এক লাইনে:

```text
Social button click → OAuth popup/redirect → backend auth → JWT save → dashboard redirect
```


----
