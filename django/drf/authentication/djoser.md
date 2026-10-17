হ্যাঁ, Djoser ব্যবহার করে Django REST Framework-এ অনেক সহজে Complete Authentication System তৈরি করা যায়। Registration, login, logout, password reset, password change, user profile এবং JWT authentication-এর মতো অনেক কাজের জন্য আগে থেকে তৈরি API পাওয়া যায়।

তবে একটা গুরুত্বপূর্ণ বিষয়: Djoser নিজে সব authentication feature করে না। এটি Django authentication system, DRF এবং JWT-এর মতো প্যাকেজের সঙ্গে কাজ করে। কোন endpoint কাজ করবে, তা তোমার configuration-এর ওপর নির্ভর করবে।

তুমি যেহেতু Beginner থেকে Production-level DRF শিখতে চাও, আমরা একটি বাস্তব authentication project বানাব, যেখানে থাকবে:

- User registration এবং login
    
- JWT access ও refresh token
    
- Email verification
    
- Password change ও reset
    
- User profile
    
- Admin, Staff ও সাধারণ User-এর role
    
- Permissions ও protected APIs
    
- Email configuration
    
- Automated tests
    
- Docker ও production deployment
    

চলো, পুরো সিস্টেমের architecture এবং implementation sequence সাজাই।

## ১. পুরো Authentication System-এর architecture

React / Next.js Frontend

Registration · Login · Profile · Password reset

Django REST Framework

API routing · Validation · Permissions · Throttling

Djoser

User management

Simple JWT

Access ও refresh tokens

Django User Model + PostgreSQL

Users · Roles · Authentication records

Djoser-এর official documentation: [Djoser documentation](https://djoser.readthedocs.io/en/latest/?utm_source=chatgpt.com)। JWT configuration-এর জন্য [Simple JWT documentation](https://django-rest-framework-simplejwt.readthedocs.io/en/stable/?utm_source=chatgpt.com) দেখবে।

![](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io&sz=32)

djoser 2.3.4 documentation

+2

## ২. কোন কোন feature তৈরি হবে?

|Feature|Implementation|
|---|---|
|Registration|Djoser|
|Login|Simple JWT|
|Access token refresh|Simple JWT|
|Email activation|Djoser + email backend|
|Resend activation|Djoser|
|Forgot password|Djoser|
|Reset password|Djoser|
|Change password|Djoser|
|Current user profile|Djoser `/users/me/`|
|User role|Custom User model|
|Staff/Admin permissions|DRF permission classes|
|JWT logout|Simple JWT blacklist endpoint|
|Rate limiting|DRF throttling|
|API documentation|drf-spectacular|
|Automated tests|pytest + DRF APIClient|
|Deployment|Docker + PostgreSQL + Gunicorn + Nginx|

মনে রাখবে: Djoser-এর built-in endpoints থাকলেও email settings, activation flow, role permissions এবং production security তোমাকে configure ও test করতে হবে।

## ৩. Project তৈরি ও package install

যদি নতুন project হয়, তাহলে:

```
mkdir djoser_auth_project
cd djoser_auth_project

python -m venv venv
source venv/bin/activate

pip install django djangorestframework
pip install djoser djangorestframework-simplejwt
pip install psycopg[binary] django-filter drf-spectacular
```

Django project ও app তৈরি করো:

```
django-admin startproject config .
python manage.py startapp accounts
```

প্রস্তাবিত structure:

```
djoser_auth_project/
├── manage.py
├── config/
│   ├── settings.py
│   └── urls.py
└── accounts/
    ├── models.py
    ├── serializers.py
    ├── permissions.py
    ├── views.py
    ├── urls.py
    └── tests.py
```

## ৪. `settings.py` configuration

`config/settings.py`-এ প্রয়োজনীয় apps যোগ করো:

```
INSTALLED_APPS = [    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "rest_framework",    "rest_framework.authtoken",    "rest_framework_simplejwt",    "rest_framework_simplejwt.token_blacklist",    "djoser",    "django_filters",    "drf_spectacular",    "accounts",]
```

DRF ও JWT settings:

```
from datetime import timedeltaREST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],    "DEFAULT_FILTER_BACKENDS": [        "django_filters.rest_framework.DjangoFilterBackend",    ],    "DEFAULT_SCHEMA_CLASS": "drf_spectacular.openapi.AutoSchema",    "DEFAULT_THROTTLE_CLASSES": [        "rest_framework.throttling.AnonRateThrottle",        "rest_framework.throttling.UserRateThrottle",    ],    "DEFAULT_THROTTLE_RATES": {        "anon": "100/hour",        "user": "1000/hour",    },}SIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}
```

Refresh-token rotation-এর জন্য blacklist app install করা এবং migrations চালানো প্রয়োজন।

![](https://www.google.com/s2/favicons?domain=https://github.com&sz=32)

GitHub

+1

## ৫. Djoser configuration

প্রথমে standard Django user model দিয়েই শুরু করতে পারো। `settings.py`-এ যোগ করো:

```
DJOSER = {    "LOGIN_FIELD": "username",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": True,    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),    "SERIALIZERS": {},}
```

এখানে `ACTIVATION_URL` ও `PASSWORD_RESET_CONFIRM_URL` হলো frontend-এর URL pattern। Frontend page-গুলোকে token ও UID নিয়ে backend-এর confirmation endpoint-এ request পাঠাতে হবে।

![](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io&sz=32)

djoser 2.3.1 documentation

+1

Email configuration: development-এ email console-এ দেখতে পারো:

```
EMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "noreply@example.com"
```

এটি শুধু development-এর জন্য। Production-এ verified email provider, environment-based credentials এবং HTTPS ব্যবহার করবে।

## ৬. User role তৈরি করা

`accounts/models.py`:

```
from django.contrib.auth.models import AbstractUserfrom django.db import modelsclass User(AbstractUser):    class Role(models.TextChoices):        USER = "USER", "User"        STAFF = "STAFF", "Staff"        ADMIN = "ADMIN", "Admin"    role = models.CharField(        max_length=10,        choices=Role.choices,        default=Role.USER,        db_index=True,    )
```

`settings.py`-এ যোগ করো:

```
AUTH_USER_MODEL = "accounts.User"
```

খুব গুরুত্বপূর্ণ: এই custom user model-টি database-এর প্রথম migration-এর আগেই configure করা সবচেয়ে সহজ। ইতিমধ্যে অন্য user model দিয়ে migrations করে থাকলে সরাসরি এই পরিবর্তন প্রয়োগ কোরো না; migration plan প্রয়োজন হতে পারে।

Public registration-এর সময় client-কে `role` নির্বাচন করতে দেবে না। সাধারণ user-এর role server-side-এ `USER` হবে। Admin role পরিবর্তনের জন্য আলাদা protected endpoint এবং permission লাগবে। Django-র `is_staff`, `is_superuser` এবং business `role` আলাদা উদ্দেশ্যে ব্যবহৃত হয়।

## ৭. API URLs configure করা

`config/urls.py`:

```
from django.contrib import adminfrom django.urls import include, pathfrom rest_framework_simplejwt.views import (    TokenBlacklistView,    TokenRefreshView,    TokenVerifyView,)urlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),    path(        "api/auth/jwt/refresh/",        TokenRefreshView.as_view(),        name="jwt-refresh",    ),    path(        "api/auth/jwt/verify/",        TokenVerifyView.as_view(),        name="jwt-verify",    ),    path(        "api/auth/jwt/logout/",        TokenBlacklistView.as_view(),        name="jwt-logout",    ),]
```

এখানে refresh ও verify route-গুলো `djoser.urls.jwt`-এর সঙ্গে duplicate হতে পারে। তাই বাস্তবে Djoser JWT URLs-ই ব্যবহার করলে আলাদা refresh/verify route আবার যোগ করবে না। সহজ configuration হিসেবে Djoser-এর JWT routes এবং custom logout route রাখাই যথেষ্ট।

## ৮. কোন endpoint কীভাবে ব্যবহার করবে?

উপরের URL configuration-এর ভিত্তিতে সাধারণত এই endpoints পাওয়া যাবে:

|কাজ|Method ও endpoint|
|---|---|
|Register|`POST /api/auth/users/`|
|Current user|`GET /api/auth/users/me/`|
|Update profile|`PATCH /api/auth/users/me/`|
|Activate account|`POST /api/auth/users/activation/`|
|Resend activation|`POST /api/auth/users/resend_activation/`|
|Login|`POST /api/auth/jwt/create/`|
|Refresh token|`POST /api/auth/jwt/refresh/`|
|Verify token|`POST /api/auth/jwt/verify/`|
|Forgot password|`POST /api/auth/users/reset_password/`|
|Confirm reset|`POST /api/auth/users/reset_password_confirm/`|
|Change password|`POST /api/auth/users/set_password/`|
|JWT logout|`POST /api/auth/jwt/logout/`|

Endpoint-এর সঠিক request fields ও response version/configuration অনুযায়ী official documentation থেকে যাচাই করবে।

![](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io&sz=32)

djoser 2.3.4 documentation

+2

## ৯. Migrations ও server চালানো

```
python manage.py makemigrations accounts
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

তারপর Postman বা DRF Browsable API দিয়ে registration, activation, login, profile, password reset এবং logout পরীক্ষা করবে।

## ১০. Production-ready করার আগে checklist

Production checklist

0/10

Registration-এ role privilege বাড়ানো যায় না

Inactive/unverified user-এর login policy পরীক্ষা করা হয়েছে

Password validation ও reset flow পরীক্ষা করা হয়েছে

JWT refresh rotation ও blacklist কাজ করে

User শুধু নিজের profile পরিবর্তন করতে পারে

Admin-only operations সঠিকভাবে protected

Rate limiting ও generic password-reset response আছে

Automated authentication ও permission tests পাস করে

Secrets environment variables-এ আছে

HTTPS, PostgreSQL backup ও deployment health checks configured

## আমার পরামর্শ

তুমি একবারে সব feature তৈরি করার চেষ্টা না করে এই ক্রমে এগোও:

1. Phase 1: Djoser + JWT দিয়ে registration, login, refresh ও profile।
    
2. Phase 2: Email activation ও password reset।
    
3. Phase 3: Custom user fields, role ও permissions।
    
4. Phase 4: Automated tests, throttling ও security audit।
    
5. Phase 5: PostgreSQL, Docker, CI/CD ও production deployment।
    

এভাবে করলে Djoser তোমার development-এর সময় বাঁচাবে, আবার authentication-এর ভেতরের কাজও বুঝতে পারবে।

পরবর্তী ধাপ: প্রথমে Phase 1 সম্পূর্ণভাবে implement করা উচিত—প্রতিটি file-এর code, Postman request, expected response এবং common errors-সহ। তারপর ধাপে ধাপে বাকি feature যোগ করবে।



---
# Phase 1: Djoser + JWT Authentication System

এই Phase-এ আমরা Django REST Framework, Djoser ও Simple JWT ব্যবহার করে একটি কার্যকর Authentication API তৈরি করব। একদম ধাপে ধাপে এগোব, যাতে প্রতিটি endpoint কীভাবে কাজ করে সেটাও বুঝতে পারো।

Phase 1 শেষে তোমার API-তে থাকবে:

- User Registration
- JWT Login
- Access Token ও Refresh Token
- Current User Profile দেখা
- নিজের Profile Update
- Protected API access
- Postman দিয়ে testing

সময়: আনুমানিক ২–৪ দিন, প্রতিদিন ১–২ ঘণ্টা। আগে থেকেই Django ভালো জানা থাকলে আরও কম লাগতে পারে।

## Step 1: Project তৈরি করো

যদি আগে থেকে project তৈরি করা থাকে, তাহলে নতুন project তৈরি না করে সেই project-এই কাজ করবে।

```
mkdir djoser_auth_project
cd djoser_auth_project

python -m venv venv
source venv/bin/activate

pip install django djangorestframework djoser djangorestframework-simplejwt
```

Django project ও app তৈরি করো:

```
django-admin startproject config .
python manage.py startapp accounts
```

তোমার project structure হবে:

```
djoser_auth_project/
├── manage.py
├── config/
│   ├── settings.py
│   └── urls.py
└── accounts/
    ├── models.py
    ├── admin.py
    └── ...
```

## Step 2: `settings.py` configure করো

`config/settings.py` ফাইলের `INSTALLED_APPS`-এ প্রয়োজনীয় app যোগ করো।

```
INSTALLED_APPS = [    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "rest_framework",    "rest_framework.authtoken",    "rest_framework_simplejwt",    "rest_framework_simplejwt.token_blacklist",    "djoser",    "accounts",]
```

এখানে:

- `rest_framework` — API তৈরি ও পরিচালনা করে।
- `djoser` — registration, user management ও password-related endpoints দেয়।
- `rest_framework_simplejwt` — JWT authentication দেয়।
- `token_blacklist` — সমর্থিত refresh token blacklist করার সুবিধা দেয়।

এখন একই ফাইলে JWT ও DRF configuration যোগ করো:

```
from datetime import timedeltaREST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],}SIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}DJOSER = {    "LOGIN_FIELD": "username",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,}
```

`IsAuthenticated` দেওয়ায় default হিসেবে API-তে login করা user প্রয়োজন হবে। Registration ও login-এর মতো public endpoints Djoser নিজস্বভাবে handle করে; পরে custom endpoints তৈরি করলে তাদের permission আলাদাভাবে যাচাই করতে হবে।

## Step 3: URLs configure করো

`config/urls.py` ফাইলের সম্পূর্ণ code:

```
from django.contrib import adminfrom django.urls import include, pathurlpatterns = [    path("admin/", admin.site.urls),    # Djoser user endpoints    path("api/auth/", include("djoser.urls")),    # JWT create, refresh and verify endpoints    path("api/auth/", include("djoser.urls.jwt")),]
```

এই configuration-এ আলাদা করে registration, login বা profile view লিখতে হচ্ছে না। Djoser সেগুলো সরবরাহ করছে।

## Step 4: Database migration করো

Terminal-এ চালাও:

```
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

`createsuperuser` command-এ username, email ও password চাইবে। এটি admin account তৈরি করবে; সাধারণ registration testing-এর জন্য আলাদা user তৈরি করবে।

Server চালু হলে:

`http://127.0.0.1:8000/`

## Step 5: Registration API তৈরি ও পরীক্ষা

POST

`/api/auth/users/`

Request body — JSON

```
{
  "username": "atiar",
  "email": "atiar@example.com",
  "password": "YourStrongPassword123!",
  "re_password": "YourStrongPassword123!"
}
```

Postman-এ Body → raw → JSON নির্বাচন করবে। নিজের পরীক্ষার email ও শক্তিশালী password ব্যবহার করবে।

এই request পাঠাও:

`POST http://127.0.0.1:8000/api/auth/users/`

সফল হলে সাধারণত `201 Created` response পাবে। Response-এ user information থাকবে; password ফেরত দেওয়া হবে না।

কেন `re_password` লাগছে?

আমরা `USER_CREATE_PASSWORD_RETYPE = True` দিয়েছি। এতে registration-এর সময় দুইবার password মিলিয়ে দেখা হয়। Password দুটি না মিললে validation error হবে।

## Step 6: JWT Login

POST

`/api/auth/jwt/create/`

Request body:

```
{
  "username": "atiar",
  "password": "YourStrongPassword123!"
}
```

Endpoint: `http://127.0.0.1:8000/api/auth/jwt/create/`

সফল login হলে response-এ এই ধরনের দুটি field পাবে:

```
{
  "refresh": "<refresh-token>",
  "access": "<access-token>"
}
```

এগুলো placeholder; তোমার server আসল token তৈরি করবে।

- Access token: protected API access করার জন্য।
- Refresh token: access token মেয়াদ শেষ হলে নতুন access token পাওয়ার জন্য।

Access token-এর মেয়াদ আমরা ১০ মিনিট রেখেছি। Refresh token-এর মেয়াদ ১ দিন।

## Step 7: Current User Profile দেখা

Login থেকে পাওয়া `access` token ব্যবহার করে request পাঠাও।

GET

`/api/auth/users/me/`

Header:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Endpoint: `http://127.0.0.1:8000/api/auth/users/me/`

সফল হলে বর্তমান login করা user-এর তথ্য পাবে। এখানে `me` মানে হলো token-এর মাধ্যমে শনাক্ত করা বর্তমান user, অন্য কোনো user নয়।

Token না পাঠালে সাধারণত `401 Unauthorized` response পাবে।

## Step 8: নিজের Profile Update

PATCH

`/api/auth/users/me/`

Header:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

Body:

```
{
  "first_name": "Atiar",
  "last_name": "Rahman"
}
```

এই request দিয়ে নিজের profile-এর অনুমোদিত field পরিবর্তন করতে পারবে। Default Djoser serializer-এ কোন কোন field writable, তা তোমার configuration অনুযায়ী যাচাই করবে। Password বা role এই endpoint দিয়ে পরিবর্তন করার ব্যবস্থা করা উচিত নয়; সেগুলোর জন্য আলাদা endpoint ও validation ব্যবহার করবে।

## Step 9: Refresh Token

Access token মেয়াদ শেষ হলে নতুন access token চাইবে।

POST

`/api/auth/jwt/refresh/`

Request body:

```
{
  "refresh": "YOUR_REFRESH_TOKEN"
}
```

সফল হলে নতুন access token পাবে। যেহেতু আমরা refresh rotation চালু করেছি, configuration অনুযায়ী নতুন refresh token-ও ফেরত আসতে পারে। তাই response-এ `refresh` field থাকলে পুরোনো token-এর বদলে সেটি সংরক্ষণ করবে। Blacklist app-এর migrations চালানোও জরুরি।

## Step 10: সম্পূর্ণ API flow পরীক্ষা করো

Phase 1 Testing Checklist

0/9

Project ও app তৈরি হয়েছে

Settings-এ DRF, Djoser ও Simple JWT যোগ করা হয়েছে

Database migrations সফল হয়েছে

POST registration দিয়ে user তৈরি হয়েছে

POST login দিয়ে access ও refresh token পাওয়া গেছে

GET profile দিয়ে নিজের তথ্য দেখা যাচ্ছে

PATCH profile দিয়ে অনুমোদিত তথ্য পরিবর্তন হচ্ছে

Refresh endpoint নতুন access token দিচ্ছে

Token ছাড়া protected endpoint-এ 401 পাওয়া যাচ্ছে

## Common errors ও সমাধান

| Error                  | কী পরীক্ষা করবে                                            |
| ---------------------- | ---------------------------------------------------------- |
| `404 Not Found`        | `config/urls.py`-এ Djoser URLs include হয়েছে কি না         |
| `401 Unauthorized`     | Access token ঠিক আছে কি না এবং `Bearer` prefix দিয়েছ কি না |
| `400 Bad Request`      | JSON field name, password confirmation ও validation errors |
| `Invalid token`        | Access ও refresh token গুলিয়ে ফেলেছ কি না                  |
| `ModuleNotFoundError`  | সঠিক virtual environment সক্রিয় আছে কি না                  |
| Refresh rotation error | Blacklist app ও migrations ঠিকমতো চালানো হয়েছে কি না       |

Phase 1-এর গুরুত্বপূর্ণ সীমাবদ্ধতা: এই পর্যায়ে আমরা Django-র default `User` model ব্যবহার করেছি। যদি তোমার final system-এ email দিয়ে login, custom role, staff/admin controls বা email verification প্রয়োজন হয়, তাহলে সেগুলো পরবর্তী Phase-এ যোগ করব। Custom user model দরকার হলে প্রথম migration-এর আগেই সিদ্ধান্ত নেওয়া সবচেয়ে ভালো।

পরবর্তী ধাপে আমরা Phase 2: Email Activation + Forgot Password + Password Reset তৈরি করব—Djoser-এর built-in endpoints, email backend এবং Postman testing-সহ।

---
# Phase 2: Email Activation + Forgot Password + Password Reset

এই ধাপে আমরা আগের Djoser + JWT Authentication System-এর ওপর Email Verification এবং Password Reset যোগ করব। বেশিরভাগ endpoint Djoser থেকেই পাব—তাই প্রতিটি কাজের জন্য আলাদা Django view লেখার প্রয়োজন হবে না।

এই Phase শেষে তুমি করতে পারবে:

1. Registration-এর পর user-এর email-এ activation link পাঠানো।
2. Link থেকে account activate করা।
3. Activation email আবার পাঠানো।
4. Password ভুলে গেলে reset email পাঠানো।
5. UID ও token ব্যবহার করে নতুন password সেট করা।
6. Email backend এবং Postman দিয়ে পুরো flow পরীক্ষা করা।

## Step 1: Djoser-এর activation configuration

আগের Phase-এর একই project-এ কাজ করবে। `config/settings.py`-এর `DJOSER` configuration আপডেট করো:

```
DJOSER = {    "LOGIN_FIELD": "username",    # Password confirmation    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    # Email activation    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    # Frontend URL patterns    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),}
```

এখানে:

- `SEND_ACTIVATION_EMAIL=True`: registration-এর পর activation email পাঠানো হবে।
- `SEND_CONFIRMATION_EMAIL=False`: এই পর্যায়ে email পরিবর্তনের পর confirmation email পাঠানোর flow চালু করছি না।
- `ACTIVATION_URL`: frontend-এর activation page-এর URL pattern।
- `PASSWORD_RESET_CONFIRM_URL`: frontend-এর password reset page-এর URL pattern।

`ACTIVATION_URL` ও `PASSWORD_RESET_CONFIRM_URL` নিজের frontend route-এর সঙ্গে মিলিয়ে দেবে। এগুলো Django backend endpoint নয়; email-এর link তৈরির জন্য ব্যবহৃত frontend URL pattern।

## Step 2: Development email backend configure করো

প্রথমে real email provider ব্যবহার না করে Django-এর Console Email Backend ব্যবহার করব। এতে email পাঠানো হবে না; terminal-এ email-এর content এবং activation link দেখা যাবে।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://docs.djangoproject.com\&sz=32)

Django

+1



`config/settings.py`-এ যোগ করো:

```
EMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "noreply@example.com"DJOSER = {    "LOGIN_FIELD": "username",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),}
```

আগের `DJOSER` dictionary-টি প্রতিস্থাপন করবে—একই setting দুবার লিখবে না।

এখন server চালাও:

```
python manage.py runserver
```

## Step 3: Registration ও activation email পরীক্ষা

Postman-এ request তৈরি করো:

POST

Register user

`http://127.0.0.1:8000/api/auth/users/`

Body → raw → JSON:

```
{
  "username": "testuser",
  "email": "testuser@example.com",
  "password": "StrongTestPass123!",
  "re_password": "StrongTestPass123!"
}
```

সফল registration-এর পর server-এর terminal দেখো। সেখানে activation email-এর content থাকবে। Email-এর link দেখতে এই ধরনের হতে পারে:

```
http://frontend-domain/activate/UID/TOKEN
```

এটি উদাহরণ, তোমার আসল link নয়।

এখানে `UID` ও `TOKEN` আলাদা করে নেবে। এই দুইটি value ব্যবহার করে backend-এর activation endpoint-এ request পাঠাতে হবে।

### Account activate করো

POST

Activate user

`http://127.0.0.1:8000/api/auth/users/activation/`

Body:

```
{
  "uid": "UID_FROM_EMAIL",
  "token": "TOKEN_FROM_EMAIL"
}
```

সফল activation-এ সাধারণত `204 No Content` response আসবে। Djoser-এর activation endpoint `uid` ও `token` গ্রহণ করে।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io\&sz=32)

djoser 2.3.4 documentation

+1



এবার login পরীক্ষা করো:

```
POST /api/auth/jwt/create/
```

```
{
  "username": "testuser",
  "password": "StrongTestPass123!"
}
```

Activation সফল হওয়ার পর user-এর login করা সম্ভব হওয়া উচিত।

### Activation email আবার পাঠানো

Email না পেলে এই endpoint পরীক্ষা করো:

```
POST /api/auth/users/resend_activation/
```

```
{
  "email": "testuser@example.com"
}
```

সাধারণত request সফল হলে `204 No Content` পাওয়া যায়। User ইতিমধ্যে active হলে বা activation email পাঠানো disabled থাকলে নতুন email পাঠানো হবে না।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io\&sz=32)

djoser 2.3.4 documentation



## Step 4: Forgot Password API

এখন password ভুলে গেলে email-এর মাধ্যমে reset করার ব্যবস্থা তৈরি করব।

প্রথমে `DJOSER`-এ `PASSWORD_RESET_CONFIRM_URL` আছে কি না যাচাই করো। এরপর Postman request:

POST

Request password reset

`http://127.0.0.1:8000/api/auth/users/reset_password/`

Body:

```
{
  "email": "testuser@example.com"
```

JSON body-তে শেষের closing brace-টিও দিতে হবে। সম্পূর্ণ valid JSON হলো:

```
{
  "email": "testuser@example.com"
}
```

সফল request-এর পর terminal-এ password reset email দেখো। সেই email-এ reset confirmation page-এর link থাকবে, যেখানে UID ও token থাকবে।

Password reset-এর সময় account-এর অস্তিত্ব সম্পর্কে অপ্রয়োজনীয় তথ্য প্রকাশ না করাই নিরাপদ। Djoser-এর default configuration-এ email না পাওয়া গেলে generic success response দেওয়া যায়।&#x20;

[image](https://www.google.com/s2/favicons?domain=https://djoser.readthedocs.io\&sz=32)

djoser 2.3.4 documentation

+1



## Step 5: Password Reset Confirm

Email থেকে পাওয়া `uid` এবং `token` নিয়ে নতুন password সেট করো।

POST

Confirm password reset

`http://127.0.0.1:8000/api/auth/users/reset_password_confirm/`

Body:

```
{
  "uid": "UID_FROM_EMAIL",
  "token": "TOKEN_FROM_EMAIL",
  "new_password": "NewStrongPass456!",
  "re_new_password": "NewStrongPass456!"
}
```

এখানে `PASSWORD_RESET_CONFIRM_RETYPE=True` থাকায় `re_new_password`-ও দিতে হবে।

সফল হলে সাধারণত `204 No Content` পাওয়া যায়। এরপর নতুন password দিয়ে login পরীক্ষা করো। পুরোনো password দিয়ে login আর সফল হওয়া উচিত নয়।

Security note: Reset token একবারের জন্য তৈরি হয় এবং password পরিবর্তন বা token invalid হয়ে গেলে আবার ব্যবহার করা যায় না। Email-এর token বা password terminal-এর বাইরে public জায়গায় শেয়ার করবে না।

## Step 6: Email provider-এর মাধ্যমে real email পাঠানো

Development-এ console backend যথেষ্ট। Production-এ SMTP বা email service provider ব্যবহার করবে।

Environment variables-এর উদাহরণ:

```
EMAIL_HOST=smtp.example.com
EMAIL_PORT=587
EMAIL_HOST_USER=your-smtp-user
EMAIL_HOST_PASSWORD=your-smtp-password
EMAIL_USE_TLS=True
DEFAULT_FROM_EMAIL=noreply@yourdomain.com
```

`settings.py`:

```
import osEMAIL_BACKEND = (    "django.core.mail.backends.smtp.EmailBackend")EMAIL_HOST = os.environ["EMAIL_HOST"]EMAIL_PORT = int(os.environ.get("EMAIL_PORT", "587"))EMAIL_HOST_USER = os.environ["EMAIL_HOST_USER"]EMAIL_HOST_PASSWORD = os.environ["EMAIL_HOST_PASSWORD"]EMAIL_USE_TLS = (    os.environ.get("EMAIL_USE_TLS", "True").lower() == "true")DEFAULT_FROM_EMAIL = os.environ["DEFAULT_FROM_EMAIL"]
```

এগুলো শুধু উদাহরণ—বাস্তবে email provider-এর দেওয়া host ও credentials ব্যবহার করবে। `.env` ফাইল GitHub-এ commit করবে না। Production-এ verified sending domain এবং HTTPS-সহ frontend URL ব্যবহার করবে।

## Step 7: পুরো flow-এর testing checklist

Phase 2 Checklist

0/10

Registration করলে activation email terminal-এ দেখা যায়

Activation-এর আগে login করা যায় না

সঠিক UID ও token দিয়ে account activate হয়

Activation-এর পর login সফল হয়

Resend activation endpoint কাজ করে

Forgot password request email তৈরি করে

Reset confirmation-এ সঠিক UID ও token লাগে

দুটি নতুন password না মিললে validation error আসে

Reset-এর পর নতুন password দিয়ে login হয়

Invalid বা পুরোনো reset token প্রত্যাখ্যান করা হয়

## Common errors

| সমস্যা                       | কী পরীক্ষা করবে                                                             |
| ---------------------------- | --------------------------------------------------------------------------- |
| Registration-এ email আসছে না | `SEND_ACTIVATION_EMAIL=True` এবং email backend                              |
| `400 Bad Request`            | Request JSON, field names, token validity                                   |
| `403 Forbidden`              | Account ইতিমধ্যে active হয়েছে কি না                                         |
| Invalid activation token     | Terminal থেকে UID ও token ঠিকমতো নিয়েছ কি না                                |
| SMTP authentication error    | Provider credentials, TLS ও port                                            |
| Password reset email আসছে না | User-এর email, email backend ও terminal logs                                |
| Password reset token invalid | সঠিক UID, token এবং password পরিবর্তনের পর পুরোনো token ব্যবহার হচ্ছে কি না |

## Phase 2 শেষ হলে কী শিখলে?

তুমি Djoser দিয়ে আলাদা custom views না লিখেই account activation, activation email resend, forgot password এবং password reset-এর মূল flow তৈরি করতে পারবে।

একটি কথা মনে রেখো: Email link-এ token থাকা মানেই account স্বয়ংক্রিয়ভাবে activate হয়ে গেছে—এমন নয়। Frontend link থেকে UID ও token নিয়ে backend confirmation endpoint-এ request পাঠাতে হয়।

Official reference:

- [Djoser Base Endpoints](https://djoser.readthedocs.io/en/latest/base_endpoints.html?utm_source=chatgpt.com)
- [Djoser Settings](https://djoser.readthedocs.io/en/latest/settings.html?utm_source=chatgpt.com)
- [Django Email Configuration](https://docs.djangoproject.com/en/5.2/topics/email/?utm_source=chatgpt.com)

পরের ধাপ হবে Phase 3: Custom User Model + Email Login + User Profile + Role-Based Permissions—যেখানে সাধারণ User, Staff ও Admin-এর access আলাদা করব এবং registration-এর মাধ্যমে কেউ যেন নিজের role বাড়াতে না পারে, সেটিও implement করব।

---
# Phase 3: Custom User Model + Email Login + Profile + Role-Based Permissions

এই ধাপে আমরা আগের Djoser + JWT Authentication System-কে আরও বাস্তবসম্মত করব। একটি গুরুত্বপূর্ণ বিষয় আগে বুঝে নাও: Custom User Model প্রথম migration-এর আগেই তৈরি করা সবচেয়ে সহজ। Phase 1 ও Phase 2-তে যদি default Django User দিয়ে migration করে থাকো, তাহলে সরাসরি Custom User Model-এ পরিবর্তন করলে database migration জটিল হতে পারে।

আমরা চারটি প্রধান feature implement করব:

- Custom User Model: `username`-এর বদলে email দিয়ে login।
- User Profile: প্রত্যেক user-এর নিজের profile থাকবে।
- Role-Based Access Control (RBAC): `USER`, `STAFF`, `ADMIN`-এর আলাদা permission।
- Secure Registration: public registration-এর মাধ্যমে কেউ নিজের role বা admin privilege বাড়াতে পারবে না।

## ১. Authentication architecture

Registration / Email Login

Djoser + Simple JWT

Custom User Model

Email · Password · Role · Account status

USER

নিজের profile

STAFF

অনুমোদিত কাজ

ADMIN

Admin operations

একটি গুরুত্বপূর্ণ security principle: Frontend-এ button লুকানো permission system নয়। Backend-এ প্রতিটি protected endpoint-এর permission যাচাই করতে হবে।

## Step 1: Custom User Model তৈরি

### 1.1 `accounts/managers.py`

প্রথমে custom manager তৈরি করো। এটি email normalize করে এবং password নিরাপদভাবে hash করে সংরক্ষণ করবে।

```
from django.contrib.auth.base_user import BaseUserManagerclass UserManager(BaseUserManager):    use_in_migrations = True    def create_user(self, email, password=None, **extra_fields):        if not email:            raise ValueError("Email is required.")        email = self.normalize_email(email).strip().lower()        user = self.model(            email=email,            **extra_fields,        )        user.set_password(password)        user.save(using=self._db)        return user    def create_superuser(self, email, password=None, **extra_fields):        extra_fields.setdefault("is_staff", True)        extra_fields.setdefault("is_superuser", True)        extra_fields.setdefault("is_active", True)        extra_fields.setdefault("role", "ADMIN")        if extra_fields.get("is_staff") is not True:            raise ValueError("Superuser must have is_staff=True.")        if extra_fields.get("is_superuser") is not True:            raise ValueError("Superuser must have is_superuser=True.")        return self.create_user(            email=email,
```

`set_password()` কেন ব্যবহার করছি? কারণ password সরাসরি database-এ plain text হিসেবে রাখা যাবে না। Django-এর password hashing system ব্যবহার করা হচ্ছে।

### 1.2 `accounts/models.py`

```
from django.contrib.auth.models import AbstractUserfrom django.db import modelsfrom .managers import UserManagerclass User(AbstractUser):    username = None    email = models.EmailField(        unique=True,        db_index=True,    )    class Role(models.TextChoices):        USER = "USER", "User"        STAFF = "STAFF", "Staff"        ADMIN = "ADMIN", "Admin"    role = models.CharField(        max_length=10,        choices=Role.choices,        default=Role.USER,        db_index=True,    )    USERNAME_FIELD = "email"    REQUIRED_FIELDS = []    objects = UserManager()    def __str__(self):        return self.emailclass Profile(models.Model):
```

এখানে দুটি model আছে:

- `User`: Login credentials, account status ও role।
- `Profile`: অতিরিক্ত ব্যক্তিগত তথ্য।

`OneToOneField` নিশ্চিত করে যে প্রতিটি user-এর সঙ্গে সর্বোচ্চ একটি profile থাকবে।

### 1.3 `settings.py`

```
AUTH_USER_MODEL = "accounts.User"
```

Migration সম্পর্কে সতর্কতা: আগে default `auth.User` দিয়ে migrations করে থাকলে এই পরিবর্তন সরাসরি প্রয়োগ কোরো না। Development project হলে backup নিয়ে নতুন database বা fresh project-এ custom model দিয়ে শুরু করা সহজ। Existing data থাকলে migration plan করে user, foreign key ও migration dependencies স্থানান্তর করতে হবে।

Fresh database-এর ক্ষেত্রে:

```
python manage.py makemigrations accounts
python manage.py migrate
python manage.py createsuperuser
```

Superuser তৈরির সময় email ও password দেবে।

## Step 2: Djoser-কে email login-এর জন্য configure করা

`config/settings.py`:

```
DJOSER = {    "LOGIN_FIELD": "email",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),}
```

এখন registration-এ username-এর পরিবর্তে email ব্যবহার করবে।

### Registration request

`POST /api/auth/users/`

```
{
    "email": "user@example.com",
    "password": "StrongPassword123!",
    "re_password": "StrongPassword123!"
}
```

### Login request

`POST /api/auth/jwt/create/`

```
{
    "email": "user@example.com",
    "password": "StrongPassword123!"
}
```

এগুলো কাজ করার জন্য Custom User Model এবং Djoser serializer-এর field configuration সঠিক হতে হবে। নিচের serializer configuration-টি সেটি স্পষ্ট করে দেবে।

## Step 3: Registration-এ role injection বন্ধ করা

এটি এই Phase-এর সবচেয়ে গুরুত্বপূর্ণ security অংশ।

ধরা যাক, কেউ malicious request পাঠাল:

```
{
    "email": "attacker@example.com",
    "password": "StrongPassword123!",
    "re_password": "StrongPassword123!",
    "role": "ADMIN",
    "is_staff": true,
    "is_superuser": true
}
```

আমাদের registration serializer-এ `role`, `is_staff` ও `is_superuser` writable field হিসেবে থাকবে না।

### `accounts/serializers.py`

```
from djoser.serializers import UserCreateSerializerfrom rest_framework import serializersfrom .models import Profile, Userclass RegistrationSerializer(UserCreateSerializer):    class Meta(UserCreateSerializer.Meta):        model = User        fields = (            "id",            "email",            "password",            "re_password",        )class CurrentUserSerializer(serializers.ModelSerializer):    class Meta:        model = User        fields = (            "id",            "email",            "first_name",            "last_name",            "role",            "email_verified",        )        read_only_fields = fieldsclass ProfileSerializer(serializers.ModelSerializer):    email = serializers.EmailField(        source="user.email",        read_only=True,    )    class Meta:        model = Profile        fields = (            "email",            "phone",            "bio",            "created_at",            "updated_at",        )        read_only_fields = (            "email",            "created_at",            "updated_at",        )
```

নোট: উপরের `CurrentUserSerializer`-এ `email_verified` field ব্যবহার করা হয়েছে শুধু তখনই, যখন তোমার `User` model-এ এই field আছে। Custom model-এ field না থাকলে সেটি বাদ দেবে। Django-র default `is_active` এবং Djoser activation flow-ও account activation পরিচালনায় ব্যবহৃত হয়।

এখন `settings.py`-এর `DJOSER` dictionary-তে serializer mapping যোগ করো:

```
DJOSER = {    "LOGIN_FIELD": "email",    "USER_CREATE_PASSWORD_RETYPE": True,    "SET_PASSWORD_RETYPE": True,    "PASSWORD_RESET_CONFIRM_RETYPE": True,    "SEND_ACTIVATION_EMAIL": True,    "SEND_CONFIRMATION_EMAIL": False,    "ACTIVATION_URL": "activate/{uid}/{token}",    "PASSWORD_RESET_CONFIRM_URL": (        "password/reset/confirm/{uid}/{token}"    ),    "SERIALIZERS": {        "user_create": "accounts.serializers.RegistrationSerializer",        "current_user": "accounts.serializers.CurrentUserSerializer",    },}
```

এখানে registration-এর সময় `role` পাঠালেও serializer সেটি গ্রহণ করবে না। `User` model-এর default role হবে `USER`।

## Step 4: Profile API তৈরি

এখন login করা user নিজের profile দেখতে এবং update করতে পারবে।

### `accounts/views.py`

```
from rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom .models import Profilefrom .serializers import ProfileSerializerclass MyProfileView(APIView):    permission_classes = [IsAuthenticated]    def get(self, request):        profile, _ = Profile.objects.get_or_create(            user=request.user        )        serializer = ProfileSerializer(profile)        return Response(serializer.data)    def patch(self, request):        profile, _ = Profile.objects.get_or_create(            user=request.user        )        serializer = ProfileSerializer(            profile,            data=request.data,            partial=True,        )        serializer.is_valid(raise_exception=True)        serializer.save()        return Response(serializer.data)
```

এখানে `request.user` হলো JWT token দিয়ে authenticated user। Client request body-তে অন্য user-এর ID পাঠিয়ে নিজের profile endpoint দিয়ে অন্য কারও profile update করতে পারবে না, কারণ view profile-কে `request.user`-এর সঙ্গে যুক্ত করে নেয়।

### `accounts/urls.py`

```
from django.urls import pathfrom .views import MyProfileViewurlpatterns = [    path("profile/", MyProfileView.as_view(), name="my-profile"),]
```

`config/urls.py`-তে app URL include করো:

```
from django.contrib import adminfrom django.urls import include, pathurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),    path("api/", include("accounts.urls")),]
```

এখন:

- `GET /api/profile/` — নিজের profile দেখা।
- `PATCH /api/profile/` — নিজের profile update।

Migration ও server চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
python manage.py runserver
```

যদি আগেই `Profile` model-এর migration তৈরি করে থাকো, আবার একই migration বানানোর দরকার হবে না।

## Step 5: Role-Based Permissions তৈরি

আমাদের তিনটি business role থাকবে:

| Role    | কী করতে পারবে                               |
| ------- | ------------------------------------------- |
| `USER`  | নিজের profile দেখা ও update                 |
| `STAFF` | নিজের profile এবং অনুমোদিত staff operations |
| `ADMIN` | অনুমোদিত admin operations                   |

Django-তে `is_staff` হলো Django Admin site-এ প্রবেশের একটি control; business `role` আলাদা। তাই custom role check নিজে implement করব।

### `accounts/permissions.py`

```
from rest_framework.permissions import BasePermissionclass IsStaffRole(BasePermission):    message = "Staff role is required."    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role == "STAFF"        )class IsAdminRole(BasePermission):    message = "Admin role is required."    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role == "ADMIN"        )class IsStaffOrAdminRole(BasePermission):    message = "Staff or Admin role is required."    def has_permission(self, request, view):        return (            request.user.is_authenticated            and request.user.role in {"STAFF", "ADMIN"}        )
```

### উদাহরণ: Staff-only API

`accounts/views.py`-এ যোগ করো:

```
from rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom .permissions import IsStaffRoleclass StaffDashboardView(APIView):    permission_classes = [        IsAuthenticated,        IsStaffRole,    ]    def get(self, request):        return Response({            "message": "Welcome to the staff dashboard."        })
```

`accounts/urls.py`-এ route যোগ করো:

```
path(    "staff/dashboard/",    StaffDashboardView.as_view(),    name="staff-dashboard",),
```

এখন `GET /api/staff/dashboard/`:

- `USER` হলে `403 Forbidden`
- `STAFF` হলে `200 OK`
- `ADMIN`-এরও অনুমতি দিতে চাইলে `IsStaffOrAdminRole` ব্যবহার করবে।

## Step 6: Admin-only API

শুধু অনুমোদিত `ADMIN` role-কে user list দেখানোর উদাহরণ:

`accounts/views.py`:

```
from rest_framework import genericsfrom rest_framework.permissions import IsAuthenticatedfrom .models import Userfrom .permissions import IsAdminRolefrom .serializers import CurrentUserSerializerclass AdminUserListView(generics.ListAPIView):    serializer_class = CurrentUserSerializer    permission_classes = [        IsAuthenticated,        IsAdminRole,    ]    def get_queryset(self):        return User.objects.all().order_by("id")
```

`accounts/urls.py`:

```
path(    "admin/users/",    AdminUserListView.as_view(),    name="admin-user-list",),
```

এখন `GET /api/admin/users/` কেবল `ADMIN` business role-এর জন্য অনুমোদিত।

Production note: Admin user list-এ pagination, sensitive-field review এবং audit logging যোগ করবে। আর এই endpoint-এর permission `role` যাচাই করে—এটি Django-র `is_superuser`-এর সমতুল্য নয়।

### Admin role কীভাবে দেওয়া হবে?

Public registration endpoint থেকে কখনোই নয়। Development-এ Django Admin বা trusted management command দিয়ে role assign করতে পারো। Production-এ dedicated admin-only role-management endpoint তৈরি করলে সেটিতে আবার authentication, permission, validation ও audit logging লাগবে।

## Step 7: Postman দিয়ে Role ও Profile পরীক্ষা

প্রথমে user login করো এবং access token নাও।

### Test A — User profile

`GET /api/profile/`

Header:

```
Authorization: Bearer YOUR_ACCESS_TOKEN
```

প্রত্যাশিত response-এর উদাহরণ:

```
{
    "email": "user@example.com",
    "phone": "",
    "bio": "",
    "created_at": "2026-10-17T00:00:00Z",
    "updated_at": "2026-10-17T00:00:00Z"
}
```

### Test B — Profile update

`PATCH /api/profile/`

```
{
    "phone": "+8801700000000",
    "bio": "Python and Django developer"
}
```

প্রত্যাশিত ফল: profile-এর অনুমোদিত field update হবে।

### Test C — Role injection

Registration request-এ চেষ্টা করো:

```
{
    "email": "attacker@example.com",
    "password": "StrongPassword123!",
    "re_password": "StrongPassword123!",
    "role": "ADMIN",
    "is_staff": true,
    "is_superuser": true
}
```

তোমার registration serializer-এর allowlist-এ এসব privilege field নেই। তাই এগুলো দিয়ে admin privilege পাওয়া যাবে না। Strict validation চাইলে unknown field এলে request-টি প্রত্যাখ্যান করার custom validation-ও যোগ করা যায়।

### Test D — Staff dashboard

`GET /api/staff/dashboard/`

- সাধারণ `USER` token দিয়ে: `403 Forbidden`
- `STAFF` token দিয়ে: `200 OK`
- Admin-এরও অনুমতি থাকলে permission class পরিবর্তন করে `IsStaffOrAdminRole` ব্যবহার করবে।

### Test E — Admin user list

`GET /api/admin/users/`

- `USER`: `403 Forbidden`
- `STAFF`: `403 Forbidden`
- `ADMIN`: `200 OK`

এগুলো পরীক্ষা করতে Django Admin বা নিরাপদ development-only setup দিয়ে আলাদা role-সহ test user তৈরি করো।

## Step 8: গুরুত্বপূর্ণ code correction

আগের `CurrentUserSerializer`-এ `email_verified` field উল্লেখ করা হয়েছিল। কিন্তু এই Phase-এর `User` model-এ field-টি নেই। তুমি আলাদা করে field যোগ না করলে serializer থেকে এটি বাদ দাও:

```
class CurrentUserSerializer(serializers.ModelSerializer):    class Meta:        model = User        fields = (            "id",            "email",            "first_name",            "last_name",            "role",        )        read_only_fields = fields
```

Djoser-এর activation workflow-এ Django-র `is_active` field ব্যবহৃত হয়। অতিরিক্ত `email_verified` field বাধ্যতামূলক নয়।

আরও দুটি বিষয় মনে রাখবে:

1. `role` default `USER` হলেও `is_staff` বা `is_superuser` স্বয়ংক্রিয়ভাবে সেটির সমান নয়।
2. যদি তুমি আগে default User model দিয়ে database migrate করে থাকো, Custom User Model-এর migration সমস্যা সমাধান না করে সরাসরি `migrate` চালিয়ে এগোবে না।

## Phase 3 completion checklist

Phase 3 Checklist

0/9

Custom User Model email দিয়ে authenticate করে

Djoser registration-এ role privilege assign করা যায় না

JWT login email দিয়ে কাজ করে

Profile API শুধু authenticated user-এর profile পরিবর্তন করে

USER staff dashboard access করতে পারে না

STAFF admin-only endpoint access করতে পারে না

ADMIN-only endpoint role যাচাই করে

Password ও sensitive fields API response-এ প্রকাশ পায় না

Registration, profile ও permissions automated tests আছে

পরবর্তী ধাপে সবচেয়ে যৌক্তিক কাজ হবে Phase 4: Automated Authentication Tests + Security Audit। সেখানে registration, email activation, JWT refresh, password reset, role escalation এবং object-level permissions-এর জন্য automated tests তৈরি করব।

-------
# Phase 4: Automated Authentication Tests + Security Audit

এবার আমরা তোমার Djoser + JWT Authentication System-এর জন্য automated testing তৈরি করব। লক্ষ্য হলো—কেউ registration-এর মাধ্যমে Admin হতে না পারে, অন্য user-এর profile পরিবর্তন করতে না পারে এবং token বা password reset-এর flow নিরাপদভাবে কাজ করে।

এই Phase-এ ব্যবহার করব:

- pytest + pytest-django — test runner ও Django integration।
- DRF APIClient — API request পাঠিয়ে পরীক্ষা করা।
- Django test database — production database-এর বাইরে isolated test চালানো।
- Security tests — authentication, role escalation, token refresh ও object-level permissions যাচাই করা।

একটি গুরুত্বপূর্ণ বিষয়: আগের Phase-গুলোতে `User`, `Profile`, `RegistrationSerializer`, `MyProfileView` এবং role permission classes তৈরি করেছি। নিচের test code সেই structure ধরে লেখা। তোমার বর্তমান model বা endpoint-এ নাম আলাদা হলে test-এ মিলিয়ে নেবে।

## ১. Testing architecture

pytest

Test discovery ও assertions

DRF APIClient

Registration · Login · Profile · Reset

Security Tests

RBAC · IDOR · Token

Test Database

Isolated test records

## Step 1: Testing packages install করো

Project-এর virtual environment activate করে চালাও:

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

প্রস্তাবিত test structure:

```
djoser_auth_project/
├── pytest.ini
├── config/
│   └── settings.py
└── accounts/
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── permissions.py
    └── tests/
        ├── __init__.py
        ├── conftest.py
        ├── test_registration.py
        ├── test_jwt.py
        ├── test_password_reset.py
        ├── test_profile_permissions.py
        └── test_rbac.py
```

`accounts` folder-এর ভেতরে `tests` directory না থাকলে তৈরি করো।

## Step 2: Shared fixtures তৈরি করো

`accounts/tests/conftest.py`

```
import pytestfrom django.contrib.auth import get_user_modelfrom rest_framework.test import APIClientfrom accounts.models import ProfileUser = get_user_model()@pytest.fixturedef api_client():    return APIClient()@pytest.fixturedef user(db):    user = User.objects.create_user(        email="user@example.com",        password="TestPassword123!",        role="USER",    )    Profile.objects.get_or_create(user=user)    return user@pytest.fixturedef staff_user(db):    staff = User.objects.create_user(        email="staff@example.com",        password="TestPassword123!",        role="STAFF",    )    Profile.objects.get_or_create(user=staff)    return staff@pytest.fixturedef admin_user(db):    admin = User.objects.create_user(        email="admin@example.com",        password="TestPassword123!",        role="ADMIN",        is_staff=True,    )    Profile.objects.get_or_create(user=admin)    return admin
```

কেন fixtures ব্যবহার করছি?

প্রতিটি test-এর জন্য বারবার user তৈরি করতে হচ্ছে না। `user`, `staff_user`, `admin_user` fixtures প্রয়োজন অনুযায়ী test-এ ব্যবহার করা যাবে।

এখানে `admin_user`-এর business role `ADMIN`, কিন্তু সেটি Django superuser নয়। বাস্তব ব্যবস্থায় business role ও Django superuser permission আলাদা রাখবে।

## Step 3: Registration ও role escalation tests

`accounts/tests/test_registration.py`

```
import pytestfrom django.contrib.auth import get_user_modelfrom django.core import mailfrom rest_framework import statusUser = get_user_model()REGISTER_URL = "/api/auth/users/"@pytest.mark.django_dbdef test_registration_sends_activation_email(api_client):    response = api_client.post(        REGISTER_URL,        {            "email": "newuser@example.com",            "password": "TestPassword123!",            "re_password": "TestPassword123!",        },        format="json",    )    assert response.status_code == status.HTTP_201_CREATED    assert User.objects.filter(        email="newuser@example.com"    ).exists()    # SEND_ACTIVATION_EMAIL=True হলে email তৈরি হওয়ার কথা।    assert len(mail.outbox) == 1@pytest.mark.django_dbdef test_registration_cannot_assign_admin_role(api_client):    response = api_client.post(        REGISTER_URL,        {            "email": "attacker@example.com",            "password": "TestPassword123!",            "re_password": "TestPassword123!",            "role": "ADMIN",            "is_staff": True,            "is_superuser": True,        },        format="json",    )    assert response.status_code == status.HTTP_201_CREATED    created_user = User.objects.get(        email="attacker@example.com"    )    assert created_user.role == "USER"    assert created_user.is_staff is False    assert created_user.is_superuser is False@pytest.mark.django_dbdef test_registration_rejects_password_mismatch(api_client):    response = api_client.post(        REGISTER_URL,        {            "email": "mismatch@example.com",            "password": "TestPassword123!",            "re_password": "DifferentPassword456!",        },        format="json",    )    assert response.status_code == status.HTTP_400_BAD_REQUEST    assert not User.objects.filter(        email="mismatch@example.com"    ).exists()
```

### এই tests কী যাচাই করে?

- Registration করলে user তৈরি হচ্ছে।
- Activation email তৈরি হচ্ছে।
- Request-এ `role=ADMIN` পাঠালেও privilege পাওয়া যাচ্ছে না।
- Password confirmation না মিললে registration ব্যর্থ হচ্ছে।

গুরুত্বপূর্ণ: Djoser/DRF-এর version ও serializer implementation অনুযায়ী unknown fields উপেক্ষা হতে পারে অথবা validation error হতে পারে। এই test-এর মূল security assertion হলো database-এ তৈরি user যেন `USER` role-এই থাকে এবং `is_staff`/`is_superuser` privilege না পায়।

## Step 4: Email activation test

`accounts/tests/test_registration.py`-এর শেষে যোগ করো:

```
from django.contrib.auth.tokens import default_token_generatorfrom django.utils.encoding import force_bytesfrom django.utils.http import urlsafe_base64_encode@pytest.mark.django_dbdef test_user_can_activate_account(api_client, user):    user.is_active = False    user.save(update_fields=["is_active"])    uid = urlsafe_base64_encode(force_bytes(user.pk))    token = default_token_generator.make_token(user)    response = api_client.post(        "/api/auth/users/activation/",        {            "uid": uid,            "token": token,        },        format="json",    )    assert response.status_code == status.HTTP_204_NO_CONTENT    user.refresh_from_db()    assert user.is_active is True
```

এই test একটি valid activation token তৈরি করে, activation endpoint-এ পাঠায় এবং account active হয়েছে কি না পরীক্ষা করে।

এটি valid activation flow-এর test। Email সত্যিই তৈরি হচ্ছে কি না, সেটি আগের registration test-এ আলাদাভাবে যাচাই করা হয়েছে।

## Step 5: JWT login, refresh ও token tests

`accounts/tests/test_jwt.py`

```
import pytestfrom rest_framework import statusfrom rest_framework_simplejwt.tokens import RefreshTokenLOGIN_URL = "/api/auth/jwt/create/"REFRESH_URL = "/api/auth/jwt/refresh/"PROFILE_URL = "/api/profile/"@pytest.mark.django_dbdef test_login_returns_access_and_refresh(api_client, user):    response = api_client.post(        LOGIN_URL,        {            "email": user.email,            "password": "TestPassword123!",        },        format="json",    )    assert response.status_code == status.HTTP_200_OK    assert "access" in response.data    assert "refresh" in response.data@pytest.mark.django_dbdef test_refresh_returns_new_access_token(api_client, user):    refresh = RefreshToken.for_user(user)    response = api_client.post(        REFRESH_URL,        {"refresh": str(refresh)},        format="json",    )    assert response.status_code == status.HTTP_200_OK    assert "access" in response.data@pytest.mark.django_dbdef test_profile_requires_authentication(api_client):    response = api_client.get(PROFILE_URL)    assert response.status_code in {        status.HTTP_401_UNAUTHORIZED,        status.HTTP_403_FORBIDDEN,    }@pytest.mark.django_dbdef test_authenticated_user_can_access_profile(    api_client,    user,):    api_client.force_authenticate(user=user)    response = api_client.get(PROFILE_URL)    assert response.status_code == status.HTTP_200_OK    assert response.data["email"] == user.email
```

এখানে `force_authenticate()` ব্যবহার করে profile permission পরীক্ষা করা হচ্ছে। এটি JWT token parsing পরীক্ষা করে না; সেটি `test_login_returns_access_and_refresh` ও `test_refresh_returns_new_access_token` দিয়ে আলাদাভাবে পরীক্ষা করছি।

JWT rotation সম্পর্কে: refresh endpoint নতুন `refresh` token ফেরত দেয় কি না, এবং পুরোনো token blacklist হয় কি না, সেটিও আলাদা test-এ যাচাই করা উচিত। এটি নির্ভর করে তোমার Simple JWT configuration ও blacklist setup-এর ওপর।

## Step 6: Forgot password ও reset password tests

`accounts/tests/test_password_reset.py`

```
import pytestfrom django.contrib.auth import get_user_modelfrom django.contrib.auth.tokens import default_token_generatorfrom django.utils.encoding import force_bytesfrom django.utils.http import urlsafe_base64_encodefrom rest_framework import statusUser = get_user_model()@pytest.mark.django_dbdef test_forgot_password_sends_email(api_client, user):    response = api_client.post(        "/api/auth/users/reset_password/",        {"email": user.email},        format="json",    )    assert response.status_code in {        status.HTTP_200_OK,        status.HTTP_204_NO_CONTENT,    }@pytest.mark.django_dbdef test_password_reset_changes_password(api_client, user):    uid = urlsafe_base64_encode(force_bytes(user.pk))    token = default_token_generator.make_token(user)    response = api_client.post(        "/api/auth/users/reset_password_confirm/",        {            "uid": uid,            "token": token,            "new_password": "NewPassword456!",            "re_new_password": "NewPassword456!",        },        format="json",    )    assert response.status_code == status.HTTP_204_NO_CONTENT    user.refresh_from_db()    assert user.check_password("NewPassword456!")    assert not user.check_password("TestPassword123!")
```

এই tests password reset request গ্রহণ হচ্ছে কি না এবং valid token দিয়ে password পরিবর্তন করা যাচ্ছে কি না যাচাই করে।

Production-grade test suite-এ আরও পরীক্ষা করবে:

- দুই password না মিললে reset ব্যর্থ হয়।
- Invalid token প্রত্যাখ্যাত হয়।
- একই reset token দ্বিতীয়বার ব্যবহার করা যায় না।
- Email না পাওয়া গেলে response দিয়ে user-এর অস্তিত্ব প্রকাশ করা হয় না।
- Password পরিবর্তনের পর পুরোনো refresh token বাতিল করার policy কাজ করে।

শেষের security policy-টি Djoser-এর default behaviour ধরে নেওয়া যাবে না; প্রয়োজনে token revocation mechanism implement করতে হবে।

## Step 7: Object-level permissions (IDOR) পরীক্ষা

এখন একটি গুরুত্বপূর্ণ security case দেখি। User A যেন User B-এর profile পরিবর্তন করতে না পারে।

আমাদের আগের `/api/profile/` endpoint `request.user` থেকে profile নেয়, তাই সেখানে অন্য user ID দিয়ে target বদলানোর সুযোগ নেই। কিন্তু যদি API-তে `/api/profiles/<id>/`-এর মতো endpoint থাকে, তাহলে সেটিও নিরাপদ করতে হবে।

### `accounts/views.py`-এ owner-scoped view যোগ করো

```
from rest_framework import genericsfrom rest_framework.permissions import IsAuthenticatedfrom .models import Profilefrom .serializers import ProfileSerializerclass OwnedProfileDetailView(generics.RetrieveUpdateAPIView):    serializer_class = ProfileSerializer    permission_classes = [IsAuthenticated]    def get_queryset(self):        return Profile.objects.filter(            user=self.request.user        )
```

`accounts/urls.py`-এ:

```
path(    "profiles/<int:pk>/",    OwnedProfileDetailView.as_view(),    name="owned-profile-detail",),
```

এই endpoint-এ queryset শুধু বর্তমান user-এর profile-এ সীমাবদ্ধ। ফলে অন্য user-এর profile ID দিলে সাধারণত `404 Not Found` আসবে।

### `accounts/tests/test_profile_permissions.py`

```
import pytestfrom rest_framework import statusfrom accounts.models import Profile@pytest.mark.django_dbdef test_user_cannot_update_another_users_profile(    api_client,    user,):    other_user = type(user).objects.create_user(        email="other@example.com",        password="OtherPassword123!",        role="USER",    )    other_profile = Profile.objects.create(        user=other_user,        bio="Original bio",    )    api_client.force_authenticate(user=user)    response = api_client.patch(        f"/api/profiles/{other_profile.pk}/",        {"bio": "Changed by someone else"},        format="json",    )    assert response.status_code == status.HTTP_404_NOT_FOUND    other_profile.refresh_from_db()    assert other_profile.bio == "Original bio"
```

এই test শুধু response code পরীক্ষা করছে না; database-এ অন্য user-এর profile অপরিবর্তিত আছে কি না, সেটিও যাচাই করছে। এটাই object-level access control-এর মূল লক্ষ্য।

## Step 8: RBAC tests — User, Staff ও Admin

`accounts/tests/test_rbac.py`

```
import pytestfrom rest_framework import statusSTAFF_URL = "/api/staff/dashboard/"ADMIN_USERS_URL = "/api/admin/users/"@pytest.mark.django_dbdef test_regular_user_cannot_access_staff_dashboard(    api_client,    user,):    api_client.force_authenticate(user=user)    response = api_client.get(STAFF_URL)    assert response.status_code == status.HTTP_403_FORBIDDEN@pytest.mark.django_dbdef test_staff_can_access_staff_dashboard(    api_client,    staff_user,):    api_client.force_authenticate(user=staff_user)    response = api_client.get(STAFF_URL)    assert response.status_code == status.HTTP_200_OK@pytest.mark.django_dbdef test_regular_user_cannot_list_all_users(    api_client,    user,):    api_client.force_authenticate(user=user)    response = api_client.get(ADMIN_USERS_URL)    assert response.status_code == status.HTTP_403_FORBIDDEN@pytest.mark.django_dbdef test_staff_cannot_access_admin_user_list(    api_client,    staff_user,):    api_client.force_authenticate(user=staff_user)    response = api_client.get(ADMIN_USERS_URL)    assert response.status_code == status.HTTP_403_FORBIDDEN@pytest.mark.django_dbdef test_admin_role_can_access_admin_user_list(    api_client,    admin_user,):    api_client.force_authenticate(user=admin_user)    response = api_client.get(ADMIN_USERS_URL)    assert response.status_code == status.HTTP_200_OK
```

এই tests আগের Phase-এর `StaffDashboardView`, `AdminUserListView` ও permission classes-এর ওপর নির্ভরশীল। URL বা view না থাকলে আগে সেগুলো implement করতে হবে।

এখানে `force_authenticate()` permission logic পরীক্ষা করে। বাস্তব JWT authentication-এর সম্পূর্ণ integration নিশ্চিত করতে অন্তত একটি test-এ actual login থেকে পাওয়া token ব্যবহার করাও ভালো।

## Step 9: সব test চালাও

Project root থেকে:

```
pytest
```

শুধু registration tests:

```
pytest accounts/tests/test_registration.py -v
```

শুধু JWT tests:

```
pytest accounts/tests/test_jwt.py -v
```

শুধু security tests:

```
pytest accounts/tests/test_profile_permissions.py accounts/tests/test_rbac.py -v
```

Coverage report:

```
pytest --cov=accounts --cov-report=term-missing
```

কোনো test fail হলে প্রথমে failure message দেখবে। বিশেষ করে Djoser version, custom serializer mapping, activation settings এবং URL configuration-এর পার্থক্যের কারণে কিছু response বা validation behaviour adjust করতে হতে পারে।

আমি তোমার actual repository-তে এই code চালাইনি; তাই সব tests প্রথমবারেই pass করবে বলে দাবি করছি না।

## Step 10: Security audit checklist

### Authentication Security Audit

0/14

Registration-এ role, is_staff বা is_superuser দিয়ে privilege escalation করা যায় না

Inactive account-এর login policy পরীক্ষা করা হয়েছে

Access token ছাড়া protected endpoint access করা যায় না

Refresh token rotation ও blacklist behaviour পরীক্ষা করা হয়েছে

এক user অন্য user-এর profile পড়তে বা পরিবর্তন করতে পারে না

Staff সাধারণ user-এর জন্য সংরক্ষিত admin endpoint access করতে পারে না

Admin operations-এর জন্য server-side permission checks আছে

Password reset token invalid বা পুনর্ব্যবহৃত হলে প্রত্যাখ্যাত হয়

Forgot password response দিয়ে account existence প্রকাশ পায় না

API responses-এ password, token বা অন্য sensitive data নেই

Registration, login, activation ও password reset-এ throttling আছে

Production secrets source code বা logs-এ নেই

HTTPS ও secure production settings configured

Dependencies vulnerability scanning-এর মধ্য দিয়ে যায়

## Step 11: GitHub Actions-এ tests চালানো

`.github/workflows/tests.yml`-এর একটি সাধারণ উদাহরণ:

```
name: Authentication Tests

on:
  push:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
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

      - name: Run Django checks
        run: python manage.py check

      - name: Run tests
        run: pytest --cov=accounts --cov-report=term-missing
```

এখানে `requirements.txt`-এ project-এর সব runtime dependency থাকতে হবে। PostgreSQL-specific tests বা external services থাকলে workflow-তে সেগুলোর test configuration যোগ করতে হবে। CI-তে real production secrets ব্যবহার করবে না।

## Phase 4 শেষে কী অর্জন করবে?

তোমার authentication system এখন শুধু endpoint-এর সমষ্টি থাকবে না; এর registration, activation, JWT, password reset, role এবং profile ownership behaviour-এর জন্য automated checks থাকবে।

পরবর্তী ধাপে যেতে চাইলে নিচের বিষয়গুলোও গুরুত্বপূর্ণ:

1. Test coverage বাড়ানো এবং edge cases যোগ করা।
2. JWT refresh rotation, logout এবং token revocation-এর integration tests।
3. CI-তে PostgreSQL ও Redis services চালানো।
4. `pip-audit` দিয়ে dependency security checks।
5. Staging environment-এ smoke tests এবং deployment gate।

মনে রাখবে: Automated tests security-এর নিশ্চয়তা নয়, কিন্তু regression ও access-control ভুল দ্রুত ধরার একটি গুরুত্বপূর্ণ উপায়। Production-এ যাওয়ার আগে সব tests বাস্তবে চালিয়ে ফলাফল যাচাই করবে।

-------
# Djoser-এর সব Authentication Endpoint — Beginner থেকে Advanced

Djoser হলো Django REST Framework-এর একটি authentication package। এটি ব্যবহার করে নিজে থেকে প্রতিটি authentication API তৈরি না করেই Registration, Login, Logout, Email Activation, Password Reset, Password Change এবং User Profile-এর মতো কাজ করা যায়।

তুমি যেহেতু Django REST Framework-এর সঙ্গে JWT এবং custom User model ব্যবহার করছ, তাই প্রতিটি endpoint-এর কাজ, request body, response, authentication এবং বাস্তব ব্যবহারের উদাহরণ দেখব।

## ১. প্রথমে Djoser endpoint-এর কাঠামো বুঝি

`config/urls.py`-তে সাধারণত এভাবে যুক্ত করা হয়:

```
from django.contrib import adminfrom django.urls import path, includeurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("djoser.urls")),    path("api/auth/", include("djoser.urls.jwt")),]
```

এখানে:

- `djoser.urls` — User registration, activation, password reset, user information ইত্যাদি।
- `djoser.urls.jwt` — JWT login, token refresh, token verification এবং package/version অনুযায়ী অন্যান্য JWT endpoint।

ধরি, তোমার backend চলছে `http://127.0.0.1:8000`-এ।

Registration ও Account

`/users/`, `/users/me/`, `/users/activation/`

JWT Authentication

`/jwt/create/`, `/jwt/refresh/`, `/jwt/verify/`

Password Management

`/users/set_password/`, `/users/reset_password/`, `/users/reset_password_confirm/`

নোট: endpoint-এর সুনির্দিষ্ট availability ও behavior তোমার ইনস্টল করা Djoser version এবং settings-এর ওপর নির্ভর করতে পারে।

## ২. Registration — নতুন User তৈরি

### Endpoint

POST

`/api/auth/users/`

কাজ: নতুন account তৈরি করা। এটি JWT login endpoint নয়; প্রথমে user register করবে, এরপর activation লাগলে account activate করবে, তারপর login করবে।

Request body:

```
{
  "email": "atiar@example.com",
  "password": "StrongPassword123!",
  "re_password": "StrongPassword123!"
}
```

`re_password` পাঠাতে হবে কি না, তা `USER_CREATE_PASSWORD_RETYPE` এবং ব্যবহৃত serializer-এর ওপর নির্ভর করে।

সম্ভাব্য response: `201 Created`

```
{
  "id": 1,
  "email": "atiar@example.com"
}
```

ভেতরে কী ঘটে?

1. Serializer input validation করে।
2. Email আগে থেকে আছে কি না যাচাই হয়।
3. Password-এর validation হয়।
4. Django password hash করে database-এ রাখে; plain-text password রাখা হয় না।
5. Activation email চালু থাকলে account activation-এর জন্য email পাঠানো হয়।

Frontend-এ registration form-এর submit button এই endpoint-এ request পাঠাবে।

## ৩. Login — JWT তৈরি

### Endpoint

POST

`/api/auth/jwt/create/`

কাজ: সঠিক credentials যাচাই করে access token ও refresh token তৈরি করা।

তোমার custom User model-এ `USERNAME_FIELD = "email"` এবং Djoser-এর `LOGIN_FIELD = "email"` সেট করা থাকলে request হবে:

```
{
  "email": "atiar@example.com",
  "password": "StrongPassword123!"
}
```

সম্ভাব্য response:

```
{
  "refresh": "<refresh-token>",
  "access": "<access-token>"
}
```

দুটি token-এর কাজ আলাদা:

| Token         | কাজ                                      |
| ------------- | ---------------------------------------- |
| Access token  | Protected API ব্যবহার করতে পাঠানো হয়     |
| Refresh token | নতুন access token পাওয়ার জন্য ব্যবহার হয় |

Protected endpoint-এ সাধারণত header পাঠাবে:

```
Authorization: Bearer <access-token>
```

গুরুত্বপূর্ণ: user inactive থাকলে login-এর আচরণ authentication configuration অনুযায়ী নিয়ন্ত্রিত হয়। Email activation বাধ্যতামূলক হলে activation সম্পন্ন না করা account দিয়ে login করা যাচ্ছে কি না, তা পরীক্ষা করতে হবে।

## ৪. Current User — নিজের তথ্য দেখা

### Endpoint

GET

`/api/auth/users/me/`

কাজ: বর্তমানে login করা user-এর তথ্য দেখা।

Request header:

```
Authorization: Bearer <access-token>
```

সম্ভাব্য response:

```
{
  "id": 1,
  "email": "atiar@example.com",
  "first_name": "Atiar",
  "last_name": "Rahman"
}
```

কোন কোন field response-এ আসবে, তা `current_user` serializer নির্ধারণ করে।

এখানে `id` পাঠিয়ে অন্য user-এর তথ্য চাওয়া হয় না। Token থেকে বর্তমান user শনাক্ত করা হয়।

### নিজের তথ্য Update

PATCH

`/api/auth/users/me/`

উদাহরণ:

```
{
  "first_name": "Md. Atiar",
  "last_name": "Rahman"
}
```

`PATCH` দিয়ে শুধু পরিবর্তন করতে চাওয়া field পাঠানো যায়।

`PUT` সাধারণত পূর্ণ update-এর জন্য ব্যবহৃত হয়, যদিও কোন field বাধ্যতামূলক হবে তা serializer-এর ওপর নির্ভর করে।

Security rule: `role`, `is_staff` বা `is_superuser`-এর মতো privilege field সাধারণ user-এর update করার সুযোগ দেওয়া উচিত নয়।

## ৫. JWT Refresh — নতুন Access Token

### Endpoint

POST

`/api/auth/jwt/refresh/`

কাজ: Access token-এর মেয়াদ শেষ হলে বৈধ refresh token দিয়ে নতুন access token পাওয়া।

Request:

```
{
  "refresh": "<refresh-token>"
}
```

সম্ভাব্য response:

```
{
  "access": "<new-access-token>",
  "refresh": "<rotated-refresh-token>"
}
```

দ্বিতীয় response-এ নতুন `refresh` আসবে কি না, তা `ROTATE_REFRESH_TOKENS`-এর মতো Simple JWT configuration-এর ওপর নির্ভর করে।

উদাহরণ:

```
SIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}
```

এই সেটিংসে refresh token rotation ও blacklist ব্যবহার করা যায়, যদি সংশ্লিষ্ট blacklist app এবং migration ঠিকমতো সেটআপ করা থাকে।

## ৬. JWT Verify — Token বৈধ কি না পরীক্ষা

### Endpoint

POST

`/api/auth/jwt/verify/`

Request:

```
{
  "token": "<access-or-refresh-token>"
}
```

সাধারণত token বৈধ হলে সফল response পাওয়া যায়; অবৈধ বা মেয়াদোত্তীর্ণ হলে error পাওয়া যায়।

মনে রাখবে: token verify হওয়া মানেই user-এর সব permission আছে, এমন নয়। Protected API-তে authentication এবং permission check আলাদাভাবে হয়।

## ৭. Account Activation — Email দিয়ে Account সক্রিয় করা

Djoser-এ activation-এর জন্য দুটি গুরুত্বপূর্ণ endpoint রয়েছে।

### ৭.১ Activation email পাঠানো

POST

`/api/auth/users/resend_activation/`

Request:

```
{
  "email": "atiar@example.com"
}
```

কাজ: আগে registration করা account-এর activation email আবার পাঠানোর চেষ্টা করা।

এর জন্য সাধারণত `SEND_ACTIVATION_EMAIL = True` এবং email backend/provider কনফিগার করা প্রয়োজন।

### ৭.২ Account Activate করা

POST

`/api/auth/users/activation/`

ইমেইল থেকে পাওয়া `uid` ও `token` দিয়ে request পাঠাতে হয়।

```
{
  "uid": "<uid-from-email>",
  "token": "<activation-token>"
}
```

সফল activation-এর পর user-এর `is_active` সাধারণত `True` হয়।

সাধারণ flow:

Registration

Email-এ activation link

Frontend থেকে `uid` + `token` পাঠানো

Account activated → Login

Activation token কোনো সাধারণ OTP নয়। এটি নির্দিষ্ট account-এর জন্য তৈরি token, এবং সাধারণত frontend link-এর মাধ্যমে বহন করা হয়।

## ৮. Password Reset — পাসওয়ার্ড ভুলে গেলে

এখানে দুটি আলাদা endpoint আছে।

### ৮.১ Reset Email Request

POST

`/api/auth/users/reset_password/`

Request:

```
{
  "email": "atiar@example.com"
}
```

কাজ: password reset email পাঠানোর প্রক্রিয়া শুরু করা।

Djoser-এর default flow-তে email-এর মাধ্যমে reset link এবং token দেওয়া হয়। এটি স্বয়ংক্রিয়ভাবে ৬ সংখ্যার OTP পাঠায় না।

### ৮.২ নতুন Password সেট করা

POST

`/api/auth/users/reset_password_confirm/`

Request:

```
{
  "uid": "<uid-from-email>",
  "token": "<reset-token>",
  "new_password": "NewStrongPassword123!",
  "re_new_password": "NewStrongPassword123!"
}
```

এখানে `re_new_password` প্রয়োজন হবে কি না, তা `PASSWORD_RESET_CONFIRM_RETYPE` এবং serializer configuration-এর ওপর নির্ভর করে।

সফল হলে password পরিবর্তিত হবে।

Security: ভুল, মেয়াদোত্তীর্ণ বা invalid token গ্রহণ করা যাবে না। Reset request-এর response এমনভাবে কনফিগার করা উচিত যাতে কেউ শুধু response দেখে অন্য ব্যক্তির account আছে কি না সহজে বুঝতে না পারে।

## ৯. Logged-in User-এর Password Change

### Endpoint

POST

`/api/auth/users/set_password/`

কাজ: user login অবস্থায় নিজের বর্তমান password দিয়ে নতুন password সেট করবে।

Request:

```
{
  "current_password": "OldPassword123!",
  "new_password": "NewPassword456!",
  "re_new_password": "NewPassword456!"
}
```

এখানে access token-ও পাঠাতে হবে:

```
Authorization: Bearer <access-token>
```

Password reset এবং password change এক নয়:

| বিষয়              | Password reset      | Password change |
| ----------------- | ------------------- | --------------- |
| Endpoint          | `reset_password/`   | `set_password/` |
| Login প্রয়োজন     | সাধারণত না          | হ্যাঁ           |
| Current password  | সাধারণত প্রয়োজন নেই | প্রয়োজন         |
| Email reset token | প্রয়োজন             | প্রয়োজন নেই     |

Password পরিবর্তনের পর আগে ইস্যু করা JWT token স্বয়ংক্রিয়ভাবে বাতিল হয়েছে—এমন ধরে নেওয়া যাবে না। JWT revocation আলাদাভাবে design করতে হতে পারে।

## ১০. Username-সম্পর্কিত Endpoint

Djoser-এর username-related endpoint-গুলো সাধারণত তখন কাজে লাগে, যখন তোমার User model-এ username field আছে।

| Method | Endpoint                                  | কাজ                                   |
| ------ | ----------------------------------------- | ------------------------------------- |
| `POST` | `/api/auth/users/set_username/`           | Login করা user-এর username পরিবর্তন   |
| `POST` | `/api/auth/users/reset_username/`         | Username reset/confirmation flow শুরু |
| `POST` | `/api/auth/users/reset_username_confirm/` | Username reset confirmation           |

এগুলো ব্যবহার করতে হলে তোমার Djoser configuration এবং User model-এ username field থাকতে হবে। তোমার আগের custom User model-এ `username = None` থাকলে এই endpoint-গুলো সাধারণত প্রযোজ্য নয়।

## ১১. Email পরিবর্তন Confirmation

### Endpoint

POST

`/api/auth/users/confirm/`

Djoser-এর সাধারণ URL configuration-এ এটি email/username পরিবর্তনের confirmation flow-এর অংশ হতে পারে। এর সঠিক ব্যবহার তোমার serializer, email confirmation settings এবং ইনস্টল করা Djoser version-এর ওপর নির্ভর করে।

এটিকে account activation endpoint-এর সঙ্গে গুলিয়ে ফেলবে না:

- `users/activation/` — নতুন account সক্রিয় করা।
- `users/confirm/` — confirmation-সম্পর্কিত অন্য flow, যেমন email পরিবর্তন নিশ্চিত করা।

## ১২. User Account Delete এবং User List

### ১২.১ নিজের Account Delete

DELETE

`/api/auth/users/me/`

বর্তমান user-এর account delete করার endpoint। Request-এ authenticated access token প্রয়োজন।

```
Authorization: Bearer <access-token>
```

এটি destructive operation। Production application-এ account deletion-এর আগে confirmation, related-data handling এবং audit requirements ঠিক করা উচিত। সফল deletion-এর response ও behavior package version/configuration অনুযায়ী যাচাই করবে।

### ১২.২ User List

GET

`/api/auth/users/`

এটি user list endpoint। সাধারণ user-কে সব user-এর তথ্য দেখানোর অনুমতি দেওয়া উচিত নয়। Djoser-এর permission settings অনুযায়ী list access সীমাবদ্ধ হতে পারে।

Admin dashboard-এর জন্য তোমার নিজের permission-protected endpoint ব্যবহার করাও একটি ভালো পদ্ধতি:

```
class AdminUserListView(ListAPIView):    serializer_class = CurrentUserSerializer    permission_classes = [IsAuthenticated, IsAdminRole]    def get_queryset(self):        return User.objects.all().order_by("id")
```

এখানে `IsAdminRole` তোমার business-level admin role যাচাই করে।

### ১২.৩ নির্দিষ্ট User দেখা বা Update করা

Djoser configuration ও permissions অনুমতি দিলে:

| Method   | Endpoint                | কাজ                                 |
| -------- | ----------------------- | ----------------------------------- |
| `GET`    | `/api/auth/users/<id>/` | নির্দিষ্ট user দেখা                 |
| `PUT`    | `/api/auth/users/<id>/` | নির্দিষ্ট user update               |
| `PATCH`  | `/api/auth/users/<id>/` | নির্দিষ্ট user-এর কিছু field update |
| `DELETE` | `/api/auth/users/<id>/` | নির্দিষ্ট user delete               |

এগুলোতে access আছে ধরে নেওয়া যাবে না। Default permission configuration পরীক্ষা করবে। সাধারণত user নিজের তথ্য দেখতে/পরিবর্তন করতে পারবে, কিন্তু অন্য user-এর account পরিবর্তনের অনুমতি পাবে না।

## ১৩. Token Login ও Logout — JWT-এর সঙ্গে পার্থক্য

Djoser-এর URL configuration-এ token authentication-এর endpoint-ও থাকতে পারে।

| Method | Endpoint                  | কাজ             |
| ------ | ------------------------- | --------------- |
| `POST` | `/api/auth/token/login/`  | DRF token তৈরি  |
| `POST` | `/api/auth/token/logout/` | DRF token বাতিল |

এগুলো DRF TokenAuthentication-এর জন্য; JWT-এর জন্য নয়। ব্যবহার করতে `rest_framework.authtoken` ও সংশ্লিষ্ট authentication configuration প্রয়োজন।

তুমি যেহেতু JWT ব্যবহার করছ, তাই:

- JWT login: `/api/auth/jwt/create/`
- JWT refresh: `/api/auth/jwt/refresh/`
- JWT verify: `/api/auth/jwt/verify/`
- JWT logout: Djoser-এ আলাদা logout endpoint আছে ধরে নেওয়া যাবে না। Logout-এর জন্য client-side token clearing এবং প্রয়োজনে refresh-token blacklist/revocation strategy দরকার।

## ১৪. সব গুরুত্বপূর্ণ Endpoint একসঙ্গে

নিচের তালিকাটি তোমার authentication API-এর দ্রুত reference হিসেবে রাখতে পারো।

| Method   | Endpoint                                  | Authentication সাধারণত লাগে?   |
| -------- | ----------------------------------------- | ------------------------------ |
| `POST`   | `/api/auth/users/`                        | না                             |
| `GET`    | `/api/auth/users/me/`                     | হ্যাঁ                          |
| `PATCH`  | `/api/auth/users/me/`                     | হ্যাঁ                          |
| `DELETE` | `/api/auth/users/me/`                     | হ্যাঁ                          |
| `POST`   | `/api/auth/jwt/create/`                   | না                             |
| `POST`   | `/api/auth/jwt/refresh/`                  | বৈধ refresh token              |
| `POST`   | `/api/auth/jwt/verify/`                   | Request-এ token                |
| `POST`   | `/api/auth/users/activation/`             | Activation token               |
| `POST`   | `/api/auth/users/resend_activation/`      | সাধারণত না                     |
| `POST`   | `/api/auth/users/reset_password/`         | সাধারণত না                     |
| `POST`   | `/api/auth/users/reset_password_confirm/` | Reset token                    |
| `POST`   | `/api/auth/users/set_password/`           | হ্যাঁ                          |
| `POST`   | `/api/auth/users/confirm/`                | সংশ্লিষ্ট confirmation flow    |
| `POST`   | `/api/auth/users/set_username/`           | Username configuration অনুযায়ী |
| `POST`   | `/api/auth/users/reset_username/`         | Username configuration অনুযায়ী |
| `POST`   | `/api/auth/users/reset_username_confirm/` | Username reset token           |

Token-based login/logout, user detail এবং list endpoint-এর availability ও permissions তোমার installed version এবং settings দিয়ে যাচাই করবে।

## ১৫. Postman দিয়ে কীভাবে পরীক্ষা করবে?

### প্রস্তাবিত Testing Sequence

নিজের অগ্রগতি চিহ্নিত করো

0/10

Registration — POST /api/auth/users/

Activation email terminal-এ এসেছে কি না পরীক্ষা

Activation — POST /api/auth/users/activation/

Login — POST /api/auth/jwt/create/

GET /api/auth/users/me/ — Bearer token দিয়ে

PATCH /api/auth/users/me/ — নিজের তথ্য update

Refresh — POST /api/auth/jwt/refresh/

Set password — POST /api/auth/users/set_password/

Reset password request — POST /api/auth/users/reset_password/

Reset confirmation — POST /api/auth/users/reset_password_confirm/

সব endpoint ঠিকমতো কাজ করছে কি না যাচাই করতে তোমার installed Djoser version-এর URL patterns ও settings-ও পরীক্ষা করতে হবে। কারণ শুধু URL অন্তর্ভুক্ত করলেই SMTP, activation, JWT rotation বা permissions স্বয়ংক্রিয়ভাবে সঠিকভাবে কনফিগার হয়ে যায় না।

পরবর্তী শেখার জন্য সবচেয়ে গুরুত্বপূর্ণ বিষয়: Djoser-এর প্রতিটি endpoint কীভাবে `Serializer → ViewSet/View → Permission → Model → Email/Token` flow অনুসরণ করে, তা বোঝা। এটি বুঝলে তুমি শুধু Djoser ব্যবহারই করবে না, প্রয়োজনে নিজের custom authentication API-ও তৈরি করতে পারবে।