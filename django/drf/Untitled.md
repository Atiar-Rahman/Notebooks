হ্যাঁ, Djoser + `django-allauth` — এই দুটি package দিয়েই Google Social Login-সহ অনেক authentication feature তৈরি করা যায়। তবে দুটিকে সরাসরি একসঙ্গে install করলেই সব endpoint তৈরি হয়ে যাবে না। Google OAuth flow-এর জন্য অতিরিক্ত integration code লিখতে হবে।

## কোন package কী করবে?

| Feature                          | Package                           |
| -------------------------------- | --------------------------------- |
| User Registration                | Djoser                            |
| Login ও User Management          | Djoser                            |
| Password Reset / Password Change | Djoser                            |
| Email Activation                 | Djoser                            |
| Google OAuth / Social Account    | `django-allauth`                  |
| Google login-এর পর JWT তৈরি      | অতিরিক্ত integration code প্রয়োজন |
| REST API ও permissions           | Django REST Framework             |

## Google Login কীভাবে কাজ করবে?

React / Next.js

Continue with Google

Google OAuth

Google থেকে authorization

django-allauth

Google identity যাচাই ও social account link

Django User Model

নতুন user তৈরি অথবা existing account-এর সঙ্গে link

JWT Authentication

Backend থেকে access ও refresh token

## একটি গুরুত্বপূর্ণ বিষয়

`django-allauth` মূলত social authentication পরিচালনা করে। এটি নিজে থেকে তোমার Djoser-এর JWT endpoint-এর বিকল্প নয়। Google OAuth সফল হওয়ার পরে JWT ফেরত দেওয়ার জন্য custom view/adapter বা উপযুক্ত integration প্রয়োজন হতে পারে।

আমার পরামর্শ: তোমার বর্তমান Djoser + custom email User model + SimpleJWT setup রেখেই Google login যুক্ত করো। এতে সাধারণ email/password login ও Google login একই user model ব্যবহার করতে পারবে।

Official documentation:

- [Djoser documentation](https://djoser.readthedocs.io/?utm_source=chatgpt.com)
- [django-allauth Google OAuth guide](https://docs.allauth.org/en/latest/socialaccount/providers/google.html?utm_source=chatgpt.com)

পরবর্তী ধাপে এই দুই package দিয়ে তোমার project-এর জন্য সম্পূর্ণ `settings.py`, URL configuration, Google OAuth setup এবং JWT response-সহ implementation করা যাবে।

----------
# Django Djoser + django-allauth দিয়ে Complete Authentication System

তুমি এই দুইটি package ব্যবহার করে একটি real-world authentication system তৈরি করতে পারবে, যেখানে থাকবে Email Registration, JWT Login, Google Login, Email Verification, Password Reset, Password Change, User Profile এবং Role-Based Access Control (RBAC)।

তোমার Django REST Framework backend-এর জন্য আমরা email-based custom User model ব্যবহার করব। মূল বিষয়টি হলো, Djoser এবং django-allauth আলাদা কাজ করবে, কিন্তু একই Django User model ব্যবহার করবে।

## ১. Authentication system-এর architecture

React / Next.js Frontend

Register · Login · Google Login · Forgot Password · Profile

Django REST Framework

API routing · Validation · Permissions · Business logic

Djoser

Registration, password management, user endpoints

django-allauth

Google OAuth, social accounts, identity verification

Simple JWT + Custom User Model

Access token · Refresh token · Email identity · User roles

PostgreSQL / Database

একটি গুরুত্বপূর্ণ বিষয়: `django-allauth` Google identity এবং social account পরিচালনা করবে। Google login-এর পরে JWT দিতে হলে একটি integration endpoint-ও তৈরি করতে হবে। Djoser নিজে থেকে Google login-এর JWT endpoint তৈরি করে না।

## ২. Project setup

আগে একটি গুরুত্বপূর্ণ সিদ্ধান্ত নিই:

- শুধু Djoser + django-allauth দিয়ে সাধারণ email/password authentication এবং Django-ভিত্তিক Google OAuth flow তৈরি করা যায়।
- React/Next.js frontend থেকে REST API দিয়ে Google login করে JWT পেতে হলে custom integration লিখতে হবে।
- এই integration কম code-এ করতে চাইলে তৃতীয় package `dj-rest-auth` ব্যবহার করা সুবিধাজনক। এর official documentation-এ Google social login এবং Simple JWT support আছে।&#x20;

  [image](https://www.google.com/s2/favicons?domain=https://dj-rest-auth.readthedocs.io\&sz=32)

  dj-rest-auth

  +1



তুমি যেহেতু দুইটি package দিয়েই করতে চেয়েছ, নিচে সেগুলো দিয়ে শুরু করার ভিত্তি দেখাচ্ছি।

### Step 1: Packages install

```
pip install django djangorestframework
pip install djoser djangorestframework-simplejwt
pip install "django-allauth[socialaccount]"
```

যদি আগে থেকেই Django project ও custom User model থাকে, তাহলে নতুন project তৈরি না করে বর্তমান project-এ এগোবে।

### Step 2: `settings.py` configure

```
INSTALLED_APPS = [    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "django.contrib.sites",    "rest_framework",    "rest_framework_simplejwt",    "rest_framework_simplejwt.token_blacklist",    "djoser",    "allauth",    "allauth.account",    "allauth.socialaccount",    "allauth.socialaccount.providers.google",    "accounts",]SITE_ID = 1
```

`MIDDLEWARE` তালিকায় allauth-এর middleware যুক্ত করবে:

```
MIDDLEWARE = [    # Django-র অন্যান্য middleware...    "allauth.account.middleware.AccountMiddleware",]
```

সতর্কতা: উপরের `MIDDLEWARE` snippet-টি তোমার সম্পূর্ণ middleware তালিকার বিকল্প নয়। বিদ্যমান middleware রেখেই প্রয়োজনীয় entry যোগ করবে।

### Step 3: Email login ও JWT

```
REST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],}SIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}AUTH_USER_MODEL = "accounts.User"
```

এখানে `timedelta` import করতে হবে:

```
from datetime import timedelta
```

`AUTH_USER_MODEL` তোমার প্রকৃত User model-এর নাম অনুযায়ী হবে। Database migration ইতিমধ্যে default Django User model দিয়ে হয়ে থাকলে এটি সরাসরি পরিবর্তন করবে না।

### Step 4: Djoser configuration

`settings.py`:

```
DJOSER = {    "LOGIN_FIELD": "email",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),}
```

এটি email registration, activation এবং password management-এর প্রাথমিক configuration। Custom User model ও serializer অনুযায়ী আরও configuration প্রয়োজন হতে পারে।

### Step 5: Google OAuth configure

প্রথমে Google Cloud Console-এ একটি project তৈরি করে OAuth Client ID ও Client Secret নিতে হবে। Google-এর official নির্দেশনা অনুযায়ী Web application client তৈরি করে redirect URI configure করতে হবে।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.allauth.org\&sz=32)

django-allauth



তারপর environment variables ব্যবহার করবে:

```
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
```

এগুলো GitHub-এ commit করবে না।

`settings.py`:

```
import osSOCIALACCOUNT_PROVIDERS = {    "google": {        "APPS": [            {                "client_id": os.environ["GOOGLE_CLIENT_ID"],                "secret": os.environ["GOOGLE_CLIENT_SECRET"],                "key": "",            }        ],        "SCOPE": ["profile", "email"],    }}
```

এটি Google provider-এর configuration। এটি একাই React frontend-এর জন্য JWT-সহ REST endpoint তৈরি করে না।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.allauth.org\&sz=32)

django-allauth

+1



### Step 6: URL configure

`config/urls.py`:

```
from django.contrib import adminfrom django.urls import path, includeurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),    # django-allauth-এর browser-based OAuth routes    path("accounts/", include("allauth.urls")),]
```

এখন Djoser-এর registration ও JWT endpoint থাকবে। `accounts/` route-গুলো allauth-এর browser-based authentication flow-এর জন্য।

React/Next.js থেকে Google login করে JWT ফেরত দেওয়ার জন্য পরের ধাপে custom API endpoint তৈরি করতে হবে। সেখানে Google-এর authorization code বা ID token সঠিকভাবে যাচাই করে user তৈরি/খুঁজে বের করে তোমার Simple JWT access ও refresh token দিতে হবে। Google-এর token-কে তোমার application-এর JWT হিসেবে সরাসরি ব্যবহার করা যাবে না।

## ৩. Complete system-এর development plan

Phase 1 — Core Authentication

Custom User model, email registration, JWT login, refresh, current user ও permissions।

Phase 2 — Email Security

Email activation, resend activation, forgot password, reset password ও password change।

Phase 3 — Google Login

OAuth configuration, Google identity validation, user creation/linking ও JWT integration।

Phase 4 — Production Security

Role-based permissions, rate limiting, token revocation, secure cookies/HTTPS ও automated tests।

আমার সুপারিশ: আমরা একবারে সব code না লিখে Phase 1 থেকে শুরু করব এবং প্রতিটি endpoint Postman দিয়ে test করব। এরপর Google OAuth যুক্ত করব।

একটি বিষয় নিশ্চিত করো: তোমার বর্তমান project-এ কি `AUTH_USER_MODEL = "accounts.User"`-সহ custom email-based User model এবং Djoser JWT login ইতিমধ্যে কাজ করছে, নাকি একেবারে নতুন project থেকে শুরু করতে চাও?

---------
# Phase 2: Djoser Authentication — Email Verification ও Password Security

এই Phase-এ আমরা Django REST Framework + Djoser দিয়ে authentication system-এর email security তৈরি করব। Phase 1-এ তোমার custom User model, email registration ও JWT login তৈরি করা আছে ধরে এগোচ্ছি।

এই Phase শেষ হলে user পারবে:

1. Registration করার পর email activation link দিয়ে account সক্রিয় করতে।
2. Activation email না পেলে আবার email পাঠাতে।
3. Password ভুলে গেলে reset email চাইতে।
4. Reset link ব্যবহার করে নতুন password সেট করতে।
5. Login অবস্থায় নিজের password পরিবর্তন করতে।

গুরুত্বপূর্ণ: Djoser-এর default password reset হলো email link/token-ভিত্তিক, ৬ সংখ্যার OTP-ভিত্তিক নয়।

## ১. Authentication flow

Registration

Email + Password

Email Activation

Email link → UID + Token

Active Account

তারপর JWT login

Forgot Password

Reset email → UID + Token → New Password

## ২. Email configuration

প্রথমে development environment-এ email testing চালু করব। এতে এখনই Gmail SMTP সেটআপ না করেও terminal-এ email content দেখতে পারবে।

`config/settings.py`

```
EMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "noreply@example.com"
```

Server চালাও:

```
python manage.py runserver
```

এখন Djoser email পাঠালে terminal-এ email-এর subject, body এবং activation/reset link দেখা যাবে। এই backend বাস্তবে email পাঠায় না। এটি শুধু development testing-এর জন্য।

Production-এ SMTP বা transactional email provider ব্যবহার করবে এবং credentials environment variables-এ রাখবে।

## ৩. Djoser configuration

`config/settings.py`-এর `DJOSER` configuration আপডেট করো:

```
DJOSER = {    "LOGIN_FIELD": "email",    # Registration    "USER_CREATE_PASSWORD_RETYPE": True,    # Password change and reset    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    # Email activation    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    # Frontend routes    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),}
```

এখানে গুরুত্বপূর্ণ বিষয়গুলো:

- `SEND_ACTIVATION_EMAIL=True`: registration-এর পর activation email পাঠানোর ব্যবস্থা চালু করে।
- `USER_CREATE_PASSWORD_RETYPE=True`: registration-এ password দুবার যাচাই করে।
- `SET_PASSWORD_RETYPE=True`: password change-এর সময় confirmation password যাচাই করে।
- `PASSWORD_RESET_CONFIRM_RETYPE=True`: reset-এর সময় দুইবার password মিলিয়ে দেখে।
- `ACTIVATION_URL`: frontend-এর activation page-এর path নির্ধারণ করে।
- `PASSWORD_RESET_CONFIRM_URL`: frontend-এর password reset page-এর path নির্ধারণ করে।

তোমার custom `UserCreateSerializer`-এ `re_password` field support থাকতে হবে। আগে তৈরি করা serializer-এ এটি থাকলে একই configuration ব্যবহার করতে পারবে।

## ৪. URL configuration

`config/urls.py`

```
from django.contrib import adminfrom django.urls import path, includeurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),]
```

Phase 1-এ এগুলো যোগ করা থাকলে আবার যোগ করবে না।

এখন backend-এর গুরুত্বপূর্ণ endpoint:

| Method | Endpoint                                  | কাজ                           |
| ------ | ----------------------------------------- | ----------------------------- |
| POST   | `/api/auth/users/`                        | Registration                  |
| POST   | `/api/auth/users/activation/`             | Account activate              |
| POST   | `/api/auth/users/resend_activation/`      | Activation email আবার পাঠানো  |
| POST   | `/api/auth/users/reset_password/`         | Reset email request           |
| POST   | `/api/auth/users/reset_password_confirm/` | নতুন password সেট             |
| POST   | `/api/auth/users/set_password/`           | Login অবস্থায় password change |

এখন প্রতিটি endpoint Postman দিয়ে পরীক্ষা করি।

## ৫. Registration এবং Email Activation

### Step A — Registration request

Postman-এ:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/`
- Body → raw → JSON

```
{
  "email": "atiar@example.com",
  "password": "StrongPassword123!",
  "re_password": "StrongPassword123!"
}
```

সঠিক হলে সাধারণত `201 Created` পাওয়া যাবে।

`SEND_ACTIVATION_EMAIL=True` থাকলে terminal-এ activation email-এর content দেখতে পাবে। Email-এ `uid` ও `token`-সহ frontend activation link থাকবে।

### Step B — Activation request

Email থেকে `uid` ও `token` নিয়ে Postman-এ পাঠাও:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/activation/`

```
{
  "uid": "MQ",
  "token": "activation-token-from-email"
}
```

এখানে `MQ` শুধু উদাহরণ। তোমার terminal-এ পাওয়া আসল `uid` এবং `token` ব্যবহার করবে।

সফল হলে Djoser সাধারণত `204 No Content` ফেরত দেয়। এরপর user-এর `is_active` সাধারণত `True` হয়।

### Step C — Activation email আবার পাঠানো

যদি user email না পায়:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/resend_activation/`

```
{
  "email": "atiar@example.com"
}
```

Djoser-এর configuration অনুযায়ী activation email আবার পাঠানোর চেষ্টা হবে। Security-এর জন্য response থেকে account-এর অস্তিত্ব অপ্রয়োজনে প্রকাশ করা উচিত নয়।

মনে রাখবে: activation URL frontend page-এ নিয়ে যাবে। সেই page-কে URL থেকে `uid` ও `token` সংগ্রহ করে backend-এর `/users/activation/` endpoint-এ POST করতে হবে।

## ৬. Forgot Password এবং Reset Password

এই অংশে user-এর login করা থাকা প্রয়োজন নেই।

### Step A — Reset email request

Postman:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/reset_password/`

```
{
  "email": "atiar@example.com"
}
```

Djoser password reset email পাঠানোর চেষ্টা করবে। Terminal-এ reset link দেখবে।

### Step B — Frontend reset page

ধরা যাক, email-এর link এমন:

```
http://localhost:3000/password/reset/confirm/UID/TOKEN
```

Frontend-এ user নতুন password লিখবে। Page-টি `UID` ও `TOKEN` ধরে রাখবে এবং সেগুলো backend-এ পাঠাবে।

### Step C — নতুন Password সেট করা

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/reset_password_confirm/`

```
{
  "uid": "MQ",
  "token": "reset-token-from-email",
  "new_password": "NewStrongPassword456!",
  "re_new_password": "NewStrongPassword456!"
}
```

সঠিক token ও password হলে সাধারণত `204 No Content` পাওয়া যাবে।

এরপর নতুন password দিয়ে JWT login পরীক্ষা করো:

`POST /api/auth/jwt/create/`

```
{
  "email": "atiar@example.com",
  "password": "NewStrongPassword456!"
}
```

Password reset link-টি valid, মেয়াদোত্তীর্ণ, invalid অথবা ইতিমধ্যে ব্যবহৃত কি না, সেসব অবস্থাও test করতে হবে।

## ৭. Login অবস্থায় Password Change

Forgot password এবং password change আলাদা feature।

এখানে user আগে থেকেই login করা থাকবে এবং পুরোনো password জানবে।

Postman request:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/users/set_password/`
- Authorization → Bearer Token → নিজের access token

```
{
  "current_password": "NewStrongPassword456!",
  "new_password": "MyUpdatedPassword789!",
  "re_new_password": "MyUpdatedPassword789!"
}
```

Djoser-এর password validation এবং serializer configuration অনুযায়ী সফল হলে password পরিবর্তিত হবে।

এরপর নতুন password দিয়ে login পরীক্ষা করবে। পুরোনো password দিয়ে login ব্যর্থ হওয়া উচিত।

## ৮. Production-এ Email পাঠানো

Development-এ console backend ব্যবহার করেছি। Production-এ SMTP বা email service configure করতে হবে।

উদাহরণস্বরূপ SMTP configuration:

```
import osEMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"EMAIL_HOST = os.environ["EMAIL_HOST"]EMAIL_PORT = int(os.environ.get("EMAIL_PORT", "587"))EMAIL_USE_TLS = TrueEMAIL_HOST_USER = os.environ["EMAIL_HOST_USER"]EMAIL_HOST_PASSWORD = os.environ["EMAIL_HOST_PASSWORD"]DEFAULT_FROM_EMAIL = os.environ["DEFAULT_FROM_EMAIL"]
```

Environment variables-এ provider-এর সঠিক host, port, username ও secret রাখবে। Gmail ব্যবহার করলে সাধারণত account password-এর বদলে উপযুক্ত App Password বা অনুমোদিত SMTP ব্যবস্থা প্রয়োজন হয়।

## ৯. Common errors এবং সমাধান

| Error                            | কী পরীক্ষা করবে                                                           |
| -------------------------------- | ------------------------------------------------------------------------- |
| `400 Bad Request`                | JSON field, password confirmation, serializer                             |
| `401 Unauthorized`               | Access token এবং authentication header                                    |
| Activation কাজ করে না            | `uid`, `token`, `is_active`, email configuration                          |
| Email আসছে না                    | Development console backend, SMTP credentials, provider logs              |
| Reset token invalid              | সঠিক UID/token, token-এর মেয়াদ, password পরিবর্তনের পর token invalidation |
| `re_password` field error        | Djoser version ও registration serializer                                  |
| User activation ছাড়াই login করছে | `is_active` validation এবং authentication configuration                   |

## ১০. Phase 2 শেষ করার Checklist

Phase 2 Progress

### 0/10

Registration করলে activation email তৈরি হয়

সঠিক activation token দিয়ে account active হয়

ভুল activation token প্রত্যাখ্যান হয়

Resend activation endpoint পরীক্ষা করা হয়েছে

Password reset email তৈরি হয়

সঠিক reset token দিয়ে নতুন password সেট হয়

ভুল ও পুনর্ব্যবহৃত reset token প্রত্যাখ্যান হয়

Password change-এ current password যাচাই হয়

নতুন password দিয়ে login সফল হয়

Production email credentials environment variables-এ রাখা হয়েছে

Phase 2-এর মূল শিক্ষা: Djoser email activation ও password management-এর endpoint দেয়; Django email backend বা provider email পাঠায়; frontend link থেকে token সংগ্রহ করে backend-এ পাঠায়।

এরপর Phase 3-এ আমরা Google OAuth integration করব, যাতে একই custom User model ব্যবহার করে Google login-এর পর application-এর JWT access ও refresh token পাওয়া যায়।

-------
# Phase 3: Google OAuth Login + Djoser + JWT

এই Phase-এ আমরা তোমার Django REST Framework authentication system-এ Google Login যুক্ত করব। আগে তৈরি করা email/password registration, Djoser এবং JWT login আগের মতোই কাজ করবে।

একটি গুরুত্বপূর্ণ বিষয়: `django-allauth` Google authentication পরিচালনা করবে, Djoser user management ও password endpoints দেবে, আর Google login সফল হওয়ার পরে JWT তৈরি করতে আমরা একটি custom API view লিখব।

## ১. Google Login-এর architecture

React / Next.js

Continue with Google

Google OAuth 2.0

User Google account দিয়ে অনুমতি দেয়

Django + django-allauth

Google identity যাচাই, account lookup ও linking

Custom Google Login API

Application User + JWT access/refresh token

আমরা frontend থেকে Google-এর ID token backend-এ পাঠানোর flow ব্যবহার করব। Backend token যাচাই করবে, তারপর application-এর JWT তৈরি করবে। Google ID token-কে application JWT হিসেবে ব্যবহার করা যাবে না।

## ২. Package install

Google OAuth REST API-তে যুক্ত করার জন্য আমরা একটি bridge package `dj-rest-auth`-ও ব্যবহার করব। কারণ শুধু Djoser ও django-allauth-এর installation দিয়ে frontend-এর জন্য JWT-সহ Google login endpoint স্বয়ংক্রিয়ভাবে তৈরি হয় না। `dj-rest-auth` এই integration সহজ করে।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+1



```
pip install "django-allauth[socialaccount]" "dj-rest-auth[with_social]"
```

যদি Djoser ও Simple JWT আগে থেকেই install করা থাকে, সেগুলো আবার install করার প্রয়োজন নেই।

## ৩. Django settings configure

`config/settings.py`-তে প্রয়োজনীয় apps নিশ্চিত করো:

```
INSTALLED_APPS = [    # Existing Django apps    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "django.contrib.sites",    # REST API    "rest_framework",    "rest_framework_simplejwt",    # Authentication    "djoser",    "dj_rest_auth",    "dj_rest_auth.registration",    # Google Social Login    "allauth",    "allauth.account",    "allauth.socialaccount",    "allauth.socialaccount.providers.google",    # Your app    "accounts",]SITE_ID = 1
```

`MIDDLEWARE`-এর মধ্যে এটি থাকতে হবে:

```
"allauth.account.middleware.AccountMiddleware",
```

তোমার আগে থেকে থাকা middleware সরিয়ে ফেলবে না; শুধু প্রয়োজনীয় entry যোগ করবে।

### JWT response configure

```
REST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],}REST_AUTH = {    "USE_JWT": True,}
```

তোমার Djoser-এর `DJOSER` configuration এবং `AUTH_USER_MODEL` আগের মতো থাকবে। JWT settings-এর বাকি অংশ—যেমন access token lifetime ও refresh rotation—Phase 1-এ যেভাবে configure করেছ, সেভাবেই রাখবে।

## ৪. Google Cloud Console configure

Google Login চালাতে Google OAuth Client তৈরি করতে হবে।

1. Google Cloud Console-এ একটি project তৈরি করো।
2. OAuth consent screen এবং প্রয়োজনীয় app information configure করো।
3. OAuth Client ID তৈরি করে application type হিসেবে Web application নির্বাচন করো।
4. তোমার frontend ও backend-এর উপযুক্ত authorized origins এবং redirect URI configure করো।

Official guide: [django-allauth Google provider documentation](https://docs.allauth.org/en/latest/socialaccount/providers/google.html?utm_source=chatgpt.com).

Client ID ও Client Secret গোপন রাখবে। Secret কখনো React/Next.js-এর frontend code-এ রাখবে না।

## ৫. Google credentials Django-তে configure

Google provider-এর credentials `django-allauth`-এ configure করতে হবে। একটি পদ্ধতি হলো Django Admin থেকে Social Applications তৈরি করা।

প্রথমে:

```
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

তারপর Django Admin-এ ঢুকে:

1. Social applications নির্বাচন করো।
2. Add social application-এ Provider হিসেবে Google নির্বাচন করো।
3. Name, Client ID এবং Secret Key দাও।
4. তোমার `example.com` default Site নয়, বরং সঠিক local development Site-টি নির্বাচন করো।
5. Save করো।

তোমার settings-এ `SITE_ID = 1` থাকলে admin-এ ওই ID-র Site-টি সঠিকভাবে configure করতে হবে।

## ৬. Google Login API তৈরি

আমাদের endpoint হবে:

`POST /api/auth/google/`

`accounts/views.py`:

```
from allauth.socialaccount.providers.google.views import (    GoogleOAuth2Adapter,)from allauth.socialaccount.providers.oauth2.client import OAuth2Clientfrom dj_rest_auth.registration.views import SocialLoginViewclass GoogleLoginView(SocialLoginView):    adapter_class = GoogleOAuth2Adapter    client_class = OAuth2Client    callback_url = "http://localhost:3000/auth/google/callback"
```

এখানে:

- `GoogleOAuth2Adapter` Google provider-এর সঙ্গে authentication পরিচালনা করে।
- `SocialLoginView` REST API-তে social login flow দেয়।
- `OAuth2Client` OAuth authorization-code flow-এ ব্যবহৃত হয়।
- `callback_url` frontend OAuth callback URL-এর সঙ্গে সামঞ্জস্যপূর্ণ হতে হবে।

`accounts/urls.py`:

```
from django.urls import pathfrom .views import GoogleLoginViewurlpatterns = [    path(        "auth/google/",        GoogleLoginView.as_view(),        name="google-login",    ),]
```

`config/urls.py`:

```
from django.contrib import adminfrom django.urls import path, includeurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),    path("api/auth/", include("dj_rest_auth.urls")),    path("api/auth/registration/", include(        "dj_rest_auth.registration.urls"    )),    path("api/", include("accounts.urls")),]
```

এখানে `accounts.urls`-এর route `auth/google/`, তাই endpoint হবে `/api/auth/google/`। Djoser ও `dj-rest-auth`-এর endpoint prefix আলাদা রাখলে route collision কমানো যায়; চাইলে `accounts/urls.py`-এর prefix-ও আলাদা করতে পারো।

নোট: এই view authorization-code flow-এর জন্য উপযুক্ত। Frontend যদি Google Identity Services থেকে `access_token` বা `id_token` সরাসরি পায়, request format ও token validation flow আলাদা হতে পারে। Frontend যেই OAuth flow ব্যবহার করছে, সেটির সঙ্গে backend flow মিলিয়ে নিতে হবে।

## ৭. Google Login কীভাবে test করবে?

এখানে frontend থেকে Google OAuth সম্পন্ন করার পর পাওয়া credential backend-এ পাঠানো হবে। Google credential-কে নিজে decode করে বিশ্বাস করবে না—backend-এ provider-এর মাধ্যমে validate করতে হবে।

Postman-এ:

- Method: `POST`
- URL: `http://127.0.0.1:8000/api/auth/google/`
- Body: `raw` → `JSON`

Request body-এর সঠিক field (`code` নাকি `access_token`) নির্ভর করবে frontend-এর OAuth flow এবং installed `dj-rest-auth` version-এর ওপর। উপরের `OAuth2Client`-ভিত্তিক flow-তে authorization code ব্যবহার করলে callback URL-ও মিলতে হবে।

সফল login-এর পর configured JWT response-এ application-এর access ও refresh token পাওয়া উচিত। Response shape version ও settings অনুযায়ী পরীক্ষা করবে।

## ৮. একই User model ব্যবহার করা

Google login-এর সময় নতুন User তৈরি হলেও সেটি তোমার `AUTH_USER_MODEL`-এর user-ই হবে। আলাদা Google User model তৈরি করার প্রয়োজন নেই।

তোমার custom User model-এ:

- `email` — unique
- `first_name`, `last_name` — ঐচ্ছিক profile data
- `role` — যেমন `USER`, `STAFF`, `ADMIN`
- `is_active` — account status

Security rule: Google login দিয়ে নতুন user তৈরি হলে তার role অবশ্যই default `USER` হবে। Google response বা frontend request থেকে `role=ADMIN`, `is_staff=True` কিংবা `is_superuser=True` গ্রহণ করবে না।

আর Google email কোনো existing local account-এর সঙ্গে মিলে গেলে স্বয়ংক্রিয়ভাবে account link করা উচিত নয়, যদি না verified identity এবং নিরাপদ account-linking policy দিয়ে তা নিশ্চিত করা হয়। `django-allauth`-এ email-based authentication/linking-এর আলাদা configuration আছে।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://django-allauth.readthedocs.io\&sz=32)

django-allauth 64.2.1 documentation

+1



## ৯. Google Login-এর পরে কী পরীক্ষা করবে?

Phase 3 Test Checklist

0/9

Google OAuth credentials সঠিকভাবে configure করা

Google login সফল হলে application user তৈরি/খুঁজে পাওয়া

JWT access ও refresh token পাওয়া

Access token দিয়ে /api/auth/users/me/ পরীক্ষা

Invalid Google credential প্রত্যাখ্যান করা

Inactive account দিয়ে login আটকানো

Existing email account নিরাপদে handle করা

নতুন Google user-এর role USER রাখা

Google Client Secret frontend-এ প্রকাশ না করা

## ১০. Phase 3 সম্পর্কে গুরুত্বপূর্ণ সিদ্ধান্ত

এই implementation-এ আমরা Djoser, django-allauth এবং JWT-এর সঙ্গে `dj-rest-auth` ব্যবহার করেছি, কারণ REST API-তে Google social login ও JWT response যুক্ত করা এতে সহজ হয়।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io\&sz=32)

djoser 2.3.5 documentation

+1



তবে এটি তোমার project-এ সরাসরি copy-paste করলেই নিশ্চিতভাবে কাজ করবে—এমন নয়। `dj-rest-auth` version, custom User model, allauth settings এবং frontend OAuth flow মিলিয়ে নিতে হবে।

এরপর Phase 4-এ আমরা authentication system-এর production security, RBAC, rate limiting, refresh-token revocation, secure frontend token storage এবং automated tests তৈরি করতে পারি।

------
# Phase 4: Production Security, RBAC ও Automated Testing

এই Phase-এ আমরা তোমার Djoser + django-allauth + Simple JWT authentication system-কে production-এর জন্য আরও নিরাপদ করব।

আগের তিনটি Phase-এ আমরা registration, email activation, password reset, JWT login এবং Google OAuth নিয়ে কাজ করেছি। এখন লক্ষ্য হলো শুধু login সফল করা নয়, বরং অননুমোদিত access, account takeover, privilege escalation এবং token misuse প্রতিরোধ করা।

এই Phase-এ থাকছে:

1. Role-Based Access Control (RBAC)
2. API rate limiting ও brute-force protection
3. JWT refresh-token revocation
4. Secure token storage ও HTTPS
5. Google login এবং account-linking security
6. Automated tests ও CI
7. Production deployment checklist

## ১. Authentication security architecture

React / Next.js

Secure login flow ও token handling

DRF Authentication

JWT validation · Google credential validation

Permissions

Role + object ownership

Throttling

Login ও reset limits

Database + Audit Logs

User state · Token blacklist · Security events

## ২. RBAC — User, Staff ও Admin permissions

প্রথমে role-based permission ঠিক করি। ধরি তোমার custom User model-এ `role` field আছে:

```
class Role(models.TextChoices):    USER = "USER", "User"    STAFF = "STAFF", "Staff"    ADMIN = "ADMIN", "Admin"role = models.CharField(    max_length=10,    choices=Role.choices,    default=Role.USER,)
```

একটি গুরুত্বপূর্ণ পার্থক্য:

- `role="ADMIN"` হলো তোমার application-এর business role।
- `is_staff=True` Django Admin site ব্যবহারের permission-এর সঙ্গে সম্পর্কিত।
- `is_superuser=True` Django-এর permission checks-এ বিশেষ অধিকার দেয়।

এই তিনটি একই জিনিস নয়।

### `accounts/permissions.py`

```
from rest_framework.permissions import BasePermissionclass IsStaffRole(BasePermission):    message = "Staff role is required."    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role == "STAFF"        )class IsAdminRole(BasePermission):    message = "Admin role is required."    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role == "ADMIN"        )class IsStaffOrAdminRole(BasePermission):    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role in {"STAFF", "ADMIN"}        )
```

### Protected API তৈরি

`accounts/views.py`:

```
from rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom .permissions import IsStaffRoleclass StaffDashboardView(APIView):    permission_classes = [        IsAuthenticated,        IsStaffRole,    ]    def get(self, request):        return Response({            "message": "Welcome to staff dashboard",            "email": request.user.email,        })
```

`accounts/urls.py`:

```
from django.urls import pathfrom .views import StaffDashboardViewurlpatterns = [    path(        "staff/dashboard/",        StaffDashboardView.as_view(),        name="staff-dashboard",    ),]
```

এখন `/api/staff/dashboard/` endpoint-এ:

| User      | Expected result                                                                      |
| --------- | ------------------------------------------------------------------------------------ |
| Anonymous | `401` বা authentication configuration অনুযায়ী `403`                                  |
| USER      | `403 Forbidden`                                                                      |
| STAFF     | `200 OK`                                                                             |
| ADMIN     | এই permission class অনুযায়ী `403`; admin-কে অনুমতি দিতে আলাদা permission ব্যবহার করো |

Security rule: Registration বা profile update serializer দিয়ে কখনো সাধারণ user-কে নিজের `role`, `is_staff` অথবা `is_superuser` পরিবর্তন করতে দেবে না।

## ৩. Object-level permission — অন্য User-এর data পরিবর্তন ঠেকানো

শুধু role যাচাই করলেই হবে না। একজন user যেন অন্য user-এর profile বা private data পরিবর্তন করতে না পারে, সেটাও নিশ্চিত করতে হবে।

`accounts/views.py`:

```
from rest_framework import genericsfrom rest_framework.permissions import IsAuthenticatedfrom .models import Profilefrom .serializers import ProfileSerializerclass MyProfileDetailView(generics.RetrieveUpdateAPIView):    serializer_class = ProfileSerializer    permission_classes = [IsAuthenticated]    def get_queryset(self):        return Profile.objects.filter(            user=self.request.user        )
```

`accounts/urls.py`:

```
path(    "profiles/<int:pk>/",    MyProfileDetailView.as_view(),    name="profile-detail",),
```

এখানে user অন্য profile-এর ID দিয়ে request করলেও queryset-এ সেই profile থাকবে না। ফলে সাধারণত `404 Not Found` পাওয়া যাবে।

এই পদ্ধতিটি `IDOR` (Insecure Direct Object Reference) ধরনের access-control সমস্যা কমাতে সাহায্য করে।

## ৪. Rate limiting — Brute-force protection

Login, registration এবং password reset endpoint-এ অতিরিক্ত request সীমিত করা জরুরি।

`config/settings.py`:

```
REST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],    "DEFAULT_THROTTLE_CLASSES": [        "rest_framework.throttling.AnonRateThrottle",        "rest_framework.throttling.UserRateThrottle",    ],    "DEFAULT_THROTTLE_RATES": {        "anon": "100/hour",        "user": "1000/hour",        "login": "10/min",        "password_reset": "5/hour",    },}
```

উপরের `login` ও `password_reset` rate নামগুলো কেবল সংজ্ঞায়িত করা হয়েছে। সংশ্লিষ্ট view-এ এগুলো প্রয়োগ করতে হবে।

### Custom throttle

`accounts/throttles.py`:

```
from rest_framework.throttling import AnonRateThrottleclass LoginRateThrottle(AnonRateThrottle):    scope = "login"class PasswordResetRateThrottle(AnonRateThrottle):    scope = "password_reset"
```

Djoser-এর login এবং reset view-এ এই throttle class যুক্ত করতে হলে Djoser-এর ব্যবহৃত view-গুলো subclass করে URL-এ override করতে হতে পারে। শুধু settings-এ scope লিখলেই সব authentication endpoint-এ আলাদা limit প্রয়োগ হবে না।

Production note: DRF-এর cache-based throttling মূলত সাধারণ rate limiting-এর জন্য; এটি একা শক্তিশালী brute-force protection নয়। Production-এ shared Redis cache, reverse-proxy rate limiting, monitoring এবং প্রয়োজনমতো IP ও account-based controls ব্যবহার করবে।

## ৫. JWT Refresh Token Revocation

তোমার project-এ `rest_framework_simplejwt.token_blacklist` ব্যবহার করলে refresh token rotation এবং blacklist চালু করা যায়।

### Step A — Settings

`config/settings.py`:

```
INSTALLED_APPS = [    # Existing apps...    "rest_framework",    "rest_framework_simplejwt",    "rest_framework_simplejwt.token_blacklist",]from datetime import timedeltaSIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}
```

`INSTALLED_APPS`-এ blacklist app আগেই থাকলে duplicate করবে না।

তারপর:

```
python manage.py migrate
```

### Step B — Refresh flow

`POST /api/auth/jwt/refresh/`

```
{
  "refresh": "<refresh-token>"
}
```

Rotation সক্রিয় থাকলে refresh-এর পরে নতুন refresh token পাওয়া যেতে পারে এবং পুরোনোটি blacklist হতে পারে।

### Step C — Logout endpoint

Djoser-এর JWT URL অন্তর্ভুক্ত করলেই একটি JWT logout endpoint নিশ্চিতভাবে পাওয়া যাবে—এমন নয়। Refresh token blacklist করতে Simple JWT-এর `TokenBlacklistView` ব্যবহার করে custom URL তৈরি করা যায়।

`config/urls.py`:

```
from django.urls import pathfrom rest_framework_simplejwt.views import TokenBlacklistViewurlpatterns = [    # Existing URL patterns...    path(        "api/auth/jwt/logout/",        TokenBlacklistView.as_view(),        name="jwt-logout",    ),]
```

Request:

`POST /api/auth/jwt/logout/`

```
{
  "refresh": "<refresh-token>"
}
```

এই endpoint ব্যবহারের আগে `token_blacklist` app install ও migrate থাকতে হবে।

গুরুত্বপূর্ণ সীমাবদ্ধতা: refresh token blacklist করলে সেই refresh token আর ব্যবহার করা যাবে না; কিন্তু ইতিমধ্যে তৈরি হওয়া access token সাধারণত মেয়াদ শেষ না হওয়া পর্যন্ত বৈধ থাকে। তাৎক্ষণিক access-token revocation দরকার হলে token versioning, denylist-ভিত্তিক authentication অথবা server-side session strategy বিবেচনা করতে হবে।

## ৬. Frontend-এ Token নিরাপদ রাখা

React/Next.js frontend-এ token কোথায় রাখবে, সেটি গুরুত্বপূর্ণ security decision।

- `localStorage`-এ long-lived refresh token রাখলে XSS হলে token চুরি হওয়ার ঝুঁকি থাকে।
- Browser-based application-এ `HttpOnly`, `Secure`, উপযুক্ত `SameSite` cookie অথবা server-side session/BFF architecture বিবেচনা করা যায়।
- Cookie-ভিত্তিক authentication ব্যবহার করলে CSRF protection, CORS এবং cookie settings সঠিক হতে হবে।
- শুধু frontend route hide করে private data সুরক্ষিত হয় না; backend-এ permission check অবশ্যই করতে হবে।

HTTPS ছাড়া production-এ authentication চালাবে না। Google Client Secret, Django `SECRET_KEY`, SMTP credentials এবং database password কখনো source code বা GitHub repository-তে commit করবে না।

## ৭. Google OAuth Security

Google Login-এ এই বিষয়গুলো যাচাই করবে:

1. Google credential backend-এ validate হচ্ছে।
2. OAuth `state` এবং authorization flow-এর নিরাপত্তা বজায় আছে।
3. Google-এর email verified কি না, এবং email ownership-এর ওপর ভিত্তি করে account link করা নিরাপদ কি না।
4. Frontend থেকে পাঠানো `role` বা privilege field উপেক্ষা করা হচ্ছে।
5. একই email-এর existing account থাকলে policy অনুযায়ী নিরাপদ linking বা re-authentication হচ্ছে।
6. Invalid বা expired credential প্রত্যাখ্যান হচ্ছে।

Google-এর ID token-এর signature, issuer, audience ও expiry যাচাই না করে তার decoded payload বিশ্বাস করবে না। `django-allauth`-এর provider flow ব্যবহার করলে সেই provider-এর validation process অনুসরণ করবে।

## ৮. Automated Security Testing

এখন authentication-এর security rules test করব। আগে install করো:

```
pip install pytest pytest-django pytest-cov
```

Project root-এ `pytest.ini` তৈরি করো:

```
[pytest]
DJANGO_SETTINGS_MODULE = config.settings
python_files = tests.py test_*.py *_tests.py
addopts = -ra
```

### Test 1 — সাধারণ User Staff Dashboard দেখতে পারবে না

`accounts/tests/test_rbac.py`:

```
import pytestfrom django.contrib.auth import get_user_modelfrom rest_framework.test import APIClientUser = get_user_model()@pytest.mark.django_dbdef test_regular_user_cannot_access_staff_dashboard():    user = User.objects.create_user(        email="user@example.com",        password="StrongPassword123!",        role="USER",    )    client = APIClient()    client.force_authenticate(user=user)    response = client.get("/api/staff/dashboard/")    assert response.status_code == 403
```

এই test ধরে নিচ্ছে যে custom User model-এ `email`, `password` এবং `role` আছে এবং staff dashboard URL তৈরি করা হয়েছে।

### Test 2 — Staff Dashboard ব্যবহার করতে পারবে

```
@pytest.mark.django_dbdef test_staff_can_access_staff_dashboard():    staff = User.objects.create_user(        email="staff@example.com",        password="StrongPassword123!",        role="STAFF",    )    client = APIClient()    client.force_authenticate(user=staff)    response = client.get("/api/staff/dashboard/")    assert response.status_code == 200
```

`force_authenticate()` permission test-এর জন্য উপকারী, কিন্তু এটি বাস্তব JWT parsing বা signature validation পরীক্ষা করে না। সে জন্য login ও protected endpoint-এ প্রকৃত JWT দিয়ে আলাদা integration test লিখবে।

### Test 3 — অন্যের Profile পরিবর্তন করা যাবে না

```
import pytestfrom django.contrib.auth import get_user_modelfrom rest_framework.test import APIClientfrom accounts.models import ProfileUser = get_user_model()@pytest.mark.django_dbdef test_user_cannot_update_another_users_profile():    user = User.objects.create_user(        email="one@example.com",        password="StrongPassword123!",        role="USER",    )    other_user = User.objects.create_user(        email="two@example.com",        password="StrongPassword123!",        role="USER",    )    other_profile = Profile.objects.create(        user=other_user,        bio="Original bio",    )    client = APIClient()    client.force_authenticate(user=user)    response = client.patch(        f"/api/profiles/{other_profile.pk}/",        {"bio": "Unauthorized change"},        format="json",    )    assert response.status_code == 404    other_profile.refresh_from_db()    assert other_profile.bio == "Original bio"
```

### আরও যেসব test লিখবে

- Registration request-এ `role="ADMIN"` পাঠালেও privilege বাড়বে না।
- ভুল password দিয়ে JWT login ব্যর্থ হবে।
- Inactive account login করতে পারবে না।
- Invalid Google credential প্রত্যাখ্যাত হবে।
- Password reset-এর invalid token গ্রহণ করা হবে না।
- Blacklist করা refresh token আবার ব্যবহার করা যাবে না।
- Anonymous user protected endpoint-এ access পাবে না।
- Staff user admin-only endpoint-এ access পাবে না।

## ৯. Test চালানো

```
# সব test
pytest

# শুধু RBAC test
pytest accounts/tests/test_rbac.py -v

# Coverage report
pytest --cov=accounts --cov-report=term-missing
```

এই commands চালিয়ে বাস্তব output দেখবে; code উদাহরণ দেওয়ার অর্থ এই নয় যে তোমার project-এ test ইতিমধ্যে pass করেছে।

## ১০. GitHub Actions দিয়ে Automated Testing

প্রতিবার GitHub-এ code push করলে বা pull request তৈরি হলে test চালানো যায়।

ফাইল তৈরি করো: `.github/workflows/tests.yml`

```
name: Authentication Security Tests

on:
  push:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install pytest pytest-django pytest-cov

      - name: Django system check
        run: python manage.py check

      - name: Run authentication tests
        run: pytest --cov=accounts --cov-report=term-missing
```

এই workflow চালাতে `requirements.txt`-এ project-এর প্রয়োজনীয় packages থাকতে হবে। PostgreSQL বা Redis-নির্ভর test থাকলে workflow-এ সংশ্লিষ্ট service-ও configure করতে হবে।

## ১১. Production Security Checklist

Production deployment-এর আগে এগুলো যাচাই করো।

### Production Readiness

0/12

Registration-এ privilege escalation আটকানো

RBAC এবং object-level permissions পরীক্ষা

Login ও password reset rate limiting

JWT refresh rotation ও blacklist পরীক্ষা

Google OAuth credential validation

Email activation ও password reset token validation

Production email provider configure

HTTPS এবং secure cookie/CORS/CSRF settings

Django SECRET_KEY ও API secrets environment-এ রাখা

Automated tests ও GitHub Actions চালানো

Production logs-এ password/token না রাখা

Database backup ও dependency security updates

## Phase 4 শেষ হলে কী অর্জন করবে?

তোমার authentication system-এ থাকবে:

- Email/password authentication এবং Google OAuth।
- JWT access ও refresh token management।
- Role-based এবং object-level access control।
- Login ও password reset-এর abuse protection।
- Automated security tests ও CI workflow।
- Production deployment-এর জন্য একটি security checklist।

একটি বাস্তব পরামর্শ: production security একবার configure করলেই শেষ নয়। Installed package-এর version, frontend token architecture, email provider, deployment server এবং database অনুযায়ী security test নিয়মিত চালাতে হবে।

পরবর্তী ধাপে তোমার authentication project-এর সব endpoint, serializer, permission, Google login এবং test-গুলো একসঙ্গে যাচাই করে একটি complete project structure ও integration audit তৈরি করা সবচেয়ে যৌক্তিক হবে।

--------
