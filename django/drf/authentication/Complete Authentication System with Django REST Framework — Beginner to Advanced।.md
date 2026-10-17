# Complete Authentication System with Django REST Framework — Beginner to Advanced

চলো, নতুন course শুরু করি। আমরা একটি reusable, production-oriented authentication system তৈরি করব, যেটি পরে তোমার E-commerce, Hotel Management বা অন্য Django REST Framework project-এ ব্যবহার করতে পারবে।

আগের ২০টি Lesson-এর OTP Password Reset system-টি আমাদের এই নতুন project-এর অংশ হবে। এবার আমরা Registration থেকে শুরু করে Login, JWT, Email Verification, Permissions এবং Production Deployment পর্যন্ত সম্পূর্ণ flow তৈরি করব।

## Course roadmap

Module 1

Foundation & Custom User

Django project setup, app structure, custom User model, UserManager, migrations

Module 2

Registration System

Register serializer, password hashing, validation, duplicate email handling

Module 3

Email Verification

Verification token, email delivery, expiry, resend and verification API

Module 4

Login & JWT

Login, access token, refresh token, rotation, blacklist and logout

Module 5

Password Management

Forgot password, OTP verification, reset token, change password

Module 6

Profile & Account

User profile, update, deactivate/reactivate policy, account security

Module 7

Roles & Permissions

Admin, Customer, Seller, custom permissions and object ownership

Module 8

Testing & Security

API tests, rate limiting, enumeration prevention, token/session policy

Module 9

Frontend Integration

React/Next.js API client, auth state, protected pages, token handling

Module 10

Production Deployment

PostgreSQL, Redis, Docker, Gunicorn, Nginx, HTTPS and CI/CD

# Lesson 1: Project Setup & Custom User Model

Level: Beginner · Practical implementation · Django REST Framework

আজকের lesson শেষে তুমি একটি Django project তৈরি করতে পারবে, `accounts` app বানাতে পারবে এবং email-ভিত্তিক custom User model configure করতে পারবে।

## Step 1 — Project তৈরি করো

Ubuntu terminal খুলে নিচের commands চালাও:

```
mkdir complete_auth_project
cd complete_auth_project

python3 -m venv venv
source venv/bin/activate

pip install django djangorestframework djangorestframework-simplejwt django-cors-headers python-dotenv

django-admin startproject config .
python manage.py startapp accounts
```

এখানে কোন command কী কাজ করে?

| Command                 | কাজ                                            |
| ----------------------- | ---------------------------------------------- |
| `python3 -m venv venv`  | আলাদা Python environment তৈরি করে              |
| `pip install ...`       | Django ও প্রয়োজনীয় packages ইনস্টল করে         |
| `startproject config .` | Django project configuration তৈরি করে          |
| `startapp accounts`     | User ও authentication logic রাখার app তৈরি করে |

## Step 2 — Project structure বোঝো

এখন তোমার project দেখতে এমন হবে:

```
complete_auth_project/
├── venv/
├── manage.py
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
└── accounts/
    ├── migrations/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    └── views.py
```

মনে রাখবে:

- `config/settings.py` — project configuration।
- `config/urls.py` — মূল URL routing।
- `accounts/models.py` — User model ও database structure।
- `accounts/views.py` — API request handle করবে।
- `accounts/serializers.py` — আমরা পরের Lesson-এ তৈরি করব।
- `accounts/services/` — ভবিষ্যতে reusable business logic রাখব।

## Step 3 — Installed apps configure করো

`config/settings.py` খুলে `INSTALLED_APPS`-এ নিচের apps যোগ করো:

```
INSTALLED_APPS = [    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "rest_framework",    "corsheaders",    "accounts",]
```

`MIDDLEWARE`-এর মধ্যে `CorsMiddleware` যোগ করো। এটি `CommonMiddleware`-এর আগে রাখবে।

```
MIDDLEWARE = [    "django.middleware.security.SecurityMiddleware",    "django.contrib.sessions.middleware.SessionMiddleware",    "corsheaders.middleware.CorsMiddleware",    "django.middleware.common.CommonMiddleware",    "django.middleware.csrf.CsrfViewMiddleware",    "django.contrib.auth.middleware.AuthenticationMiddleware",    "django.contrib.messages.middleware.MessageMiddleware",    "django.middleware.clickjacking.XFrameOptionsMiddleware",]
```

CORS configuration পরে frontend-এর নির্দিষ্ট origin অনুযায়ী করব। এখন production-এর জন্য `CORS_ALLOW_ALL_ORIGINS = True` ব্যবহার করবে না।

## Step 4 — Custom User Model কেন প্রয়োজন?

Django-তে default User model-এ `username` এবং `password` থাকে। আমাদের system-এ email দিয়ে login করতে হবে, তাই আমরা custom User model তৈরি করব।

আমাদের User model-এর লক্ষ্য:

- Username-এর পরিবর্তে email দিয়ে authentication।
- Unique email address।
- Django-এর built-in password hashing।
- Admin ও superuser support।
- ভবিষ্যতে role এবং account status যোগ করার সুযোগ।

### 4.1 — `accounts/managers.py` তৈরি করো

`accounts/` directory-তে নতুন `managers.py` file তৈরি করো।

```
from django.contrib.auth.base_user import BaseUserManagerclass UserManager(BaseUserManager):    use_in_migrations = True    def create_user(self, email, password=None, **extra_fields):        if not email:            raise ValueError("Email is required.")        email = self.normalize_email(email)        user = self.model(            email=email,            **extra_fields,        )        user.set_password(password)        user.save(using=self._db)        return user    def create_superuser(self, email, password=None, **extra_fields):        extra_fields.setdefault("is_staff", True)        extra_fields.setdefault("is_superuser", True)        extra_fields.setdefault("is_active", True)        if extra_fields.get("is_staff") is not True:            raise ValueError("Superuser must have is_staff=True.")        if extra_fields.get("is_superuser") is not True:            raise ValueError("Superuser must have is_superuser=True.")        return self.create_user(            email=email,            password=password,            **extra_fields,        )
```

এখানে গুরুত্বপূর্ণ বিষয়: `set_password()` password-কে hash করে সংরক্ষণ করে। Password সরাসরি `user.password = password` দিয়ে assign করা নিরাপদ নয়।

### 4.2 — `accounts/models.py` তৈরি করো

আগের file-এর content সরিয়ে নিচের code রাখো:

```
from django.contrib.auth.models import AbstractUserfrom django.db import modelsfrom .managers import UserManagerclass User(AbstractUser):    username = None    email = models.EmailField(        unique=True,        db_index=True,    )    USERNAME_FIELD = "email"    REQUIRED_FIELDS = []    objects = UserManager()    def __str__(self):        return self.email
```

এখন আমাদের User model email-কে login identifier হিসেবে ব্যবহার করবে।

### 4.3 — `settings.py`-তে custom model নির্ধারণ করো

`config/settings.py`-এর শেষে যোগ করো:

```
AUTH_USER_MODEL = "accounts.User"
```

অত্যন্ত গুরুত্বপূর্ণ: প্রথম database migration-এর আগেই custom User model configure করা সবচেয়ে সহজ ও নিরাপদ। পুরোনো project-এ migration হয়ে গেলে মাঝপথে User model পরিবর্তন অনেক জটিল হতে পারে। তাই এই course-এর জন্য নতুন project ব্যবহার করছি।

## Step 5 — Database migration

Terminal-এ চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
```

এখন Django custom User model-এর জন্য database table তৈরি করবে।

## Step 6 — Superuser তৈরি করো

```
python manage.py createsuperuser
```

Email ও password দাও। এরপর:

```
python manage.py runserver
```

Browser-এ খোলো:

`http://127.0.0.1:8000/admin/`

Admin panel-এ User model দেখানোর জন্য পরের ধাপে `accounts/admin.py` configure করব। এখন superuser তৈরির command সফল হয়েছে কি না সেটি আগে যাচাই করো।

## Step 7 — Custom User model পরীক্ষা করো

Django shell চালাও:

```
python manage.py shell
```

তারপর:

```
from django.contrib.auth import get_user_modelUser = get_user_model()print(User)print(User.USERNAME_FIELD)
```

প্রত্যাশিত output:

```
<class 'accounts.models.User'>
email
```

আরও একটি গুরুত্বপূর্ণ test:

```
user = User.objects.create_user(    email="student@example.com",    password="StrongPassword123!",)print(user.email)print(user.check_password("StrongPassword123!"))
```

শেষ লাইনে `True` পাওয়া উচিত। এটি প্রমাণ করে password সঠিকভাবে hash হয়েছে এবং password verification কাজ করছে।

পরীক্ষা শেষে shell থেকে বের হতে পারো:

```
exit()
```

## আজকের practical assignment

Lesson 1 checklist

0/6

Virtual environment ও Django project তৈরি করেছি

accounts app এবং required packages configure করেছি

Custom UserManager তৈরি করেছি

Email-based custom User model তৈরি করেছি

AUTH_USER_MODEL সেট করে migrations চালিয়েছি

Superuser তৈরি ও password hashing পরীক্ষা করেছি

পরবর্তী Lesson 2: Registration API — `RegisterSerializer`, password validation, duplicate email handling, `CreateAPIView`, API endpoint এবং Postman দিয়ে registration test।

তোমার project-এ যদি কোনো error আসে, error message ও সংশ্লিষ্ট code পাঠাও। আমরা পরের Lesson-এ যাওয়ার আগে সেটি ঠিক করে নেব।


----
# Lesson 2: Registration API — Beginner to Advanced

আজ আমরা আমাদের Django REST Framework Authentication Project-এ User Registration API তৈরি করব। Lesson 1-এ তৈরি করা Custom User Model ব্যবহার করেই registration করব; নতুন User model তৈরি করতে হবে না।

আজকের lesson শেষে একজন নতুন user email ও password দিয়ে register করতে পারবে, duplicate email দিলে validation error পাবে এবং password database-এ plain text হিসেবে নয়, hash আকারে সংরক্ষিত হবে।

## আজকের learning objectives

- `RegisterSerializer` তৈরি করা
- `validate_email()` দিয়ে duplicate email আটকানো
- Django password validators ব্যবহার করা
- `CreateAPIView` দিয়ে registration endpoint তৈরি করা
- API URL configure করা
- Postman দিয়ে successful ও failed registration পরীক্ষা করা

## Step 1 — প্রয়োজনীয় file structure

Lesson 1-এর project-এ নিচের files তৈরি বা update করো:

```
complete_auth_project/
├── config/
│   ├── settings.py
│   └── urls.py
└── accounts/
    ├── models.py
    ├── managers.py
    ├── serializers.py     # নতুন
    ├── views.py            # update
    └── urls.py             # নতুন
```

## Step 2 — Password validation configure করো

`config/settings.py`-এ `AUTH_PASSWORD_VALIDATORS` আছে কি না দেখো। Django-এর default validators ব্যবহার করতে পারো:

```
AUTH_PASSWORD_VALIDATORS = [    {        "NAME": (            "django.contrib.auth.password_validation."            "UserAttributeSimilarityValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "MinimumLengthValidator"        ),        "OPTIONS": {            "min_length": 8,        },    },    {        "NAME": (            "django.contrib.auth.password_validation."            "CommonPasswordValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "NumericPasswordValidator"        ),    },]
```

এই validators কী করে?

| Validator                          | কাজ                                                                       |
| ---------------------------------- | ------------------------------------------------------------------------- |
| `UserAttributeSimilarityValidator` | Email বা user information-এর সঙ্গে অতিরিক্ত মিল থাকা password আটকাতে পারে |
| `MinimumLengthValidator`           | ন্যূনতম দৈর্ঘ্য যাচাই করে                                                 |
| `CommonPasswordValidator`          | বহুল ব্যবহৃত দুর্বল password আটকায়                                        |
| `NumericPasswordValidator`         | শুধু সংখ্যা দিয়ে তৈরি password আটকায়                                      |

মনে রাখবে: `AUTH_PASSWORD_VALIDATORS` configure করলেই `set_password()` নিজে থেকে সব validator চালায় না। Registration serializer-এ আমরা `validate_password()` ব্যবহার করব।

## Step 3 — `RegisterSerializer` তৈরি করো

`accounts/serializers.py` file তৈরি করো।

```
from django.contrib.auth import get_user_modelfrom django.contrib.auth.password_validation import validate_passwordfrom django.core.exceptions import ValidationError as DjangoValidationErrorfrom rest_framework import serializersUser = get_user_model()class RegisterSerializer(serializers.ModelSerializer):    password = serializers.CharField(        write_only=True,        trim_whitespace=False,        style={"input_type": "password"},    )    password2 = serializers.CharField(        write_only=True,        trim_whitespace=False,        style={"input_type": "password"},    )    class Meta:        model = User        fields = [            "id",            "email",            "password",            "password2",        ]        read_only_fields = ["id"]    def validate_email(self, value):        email = value.strip()        if User.objects.filter(email__iexact=email).exists():            raise serializers.ValidationError(                "An account with this email already exists."            )        return email    def validate(self, attrs):        password = attrs.get("password")        password2 = attrs.get("password2")        if password != password2:            raise serializers.ValidationError({                "password2": "Passwords do not match."            })        try:            validate_password(password)        except DjangoValidationError as exc:            raise serializers.ValidationError({                "password": list(exc.messages)            })        return attrs    def create(self, validated_data):        validated_data.pop("password2")        password = validated_data.pop("password")        user = User.objects.create_user(            password=password,            **validated_data,        )        return user
```

### Code explanation

১. `ModelSerializer` কেন?

`ModelSerializer` আমাদের User model-এর fields ব্যবহার করে serialization ও validation সহজ করে।

২. `write_only=True` কেন?

Password request body-তে পাঠানো যাবে, কিন্তু response-এ ফেরত পাঠানো হবে না।

৩. `validate_email()` কী করে?

একই email আগে থেকেই থাকলে registration reject করে। `__iexact` ব্যবহার করায় case-insensitive duplicate-ও খুঁজতে পারে। তবে এই check একা যথেষ্ট নয়—database-এর unique constraint-ও প্রয়োজন।

৪. `validate()` কী করে?

দুটি password মিলে কি না এবং Django-এর password policy পূরণ করছে কি না যাচাই করে।

৫. `create()` কেন override করেছি?

`User.objects.create_user()` ব্যবহার করে password hash করানোর জন্য। এটি আমাদের Lesson 1-এর `UserManager` ব্যবহার করবে।

## Step 4 — Registration API View তৈরি করো

`accounts/views.py` খুলে নিচের code যোগ করো:

```
from rest_framework import genericsfrom rest_framework.permissions import AllowAnyfrom rest_framework.throttling import ScopedRateThrottlefrom .serializers import RegisterSerializerclass RegisterAPIView(generics.CreateAPIView):    serializer_class = RegisterSerializer    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "register"
```

এখানে `CreateAPIView` POST request গ্রহণ করে serializer validation চালায় এবং সফল হলে database-এ object তৈরি করে।

- `AllowAny`: login ছাড়াই registration করা যাবে।
- `ScopedRateThrottle`: request rate সীমিত করার ব্যবস্থা।
- `serializer_class`: কোন serializer registration-এর জন্য ব্যবহৃত হবে তা নির্ধারণ করে।

## Step 5 — API URL configure করো

`accounts/urls.py` নামে নতুন file তৈরি করো:

```
from django.urls import pathfrom .views import RegisterAPIViewurlpatterns = [    path(        "register/",        RegisterAPIView.as_view(),        name="register",    ),]
```

এবার `config/urls.py` update করো:

```
from django.contrib import adminfrom django.urls import include, pathurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("accounts.urls")),]
```

আমাদের registration endpoint:

POST

`/api/auth/register/`

Local URL: `http://127.0.0.1:8000/api/auth/register/`

&#x20;Copy endpoint

## Step 6 — Registration throttling configure করো

`config/settings.py`-এ তোমার existing `REST_FRAMEWORK` dictionary থাকলে সেটি replace না করে নিচের key-গুলো merge করো:

```
REST_FRAMEWORK = {    # Keep your existing authentication and permission settings.    "DEFAULT_THROTTLE_RATES": {        "register": "5/hour",    },}
```

এটি সম্পূর্ণ `REST_FRAMEWORK` configuration নয়—আগের settings থাকলে সেগুলোও একই dictionary-তে রাখতে হবে। DRF-এর throttling সাধারণ abuse কমাতে সাহায্য করে, কিন্তু একে একমাত্র security control হিসেবে ব্যবহার করা যাবে না।

## Step 7 — Postman দিয়ে Registration API test করো

প্রথমে server চালাও:

```
python manage.py check
python manage.py runserver
```

Postman খুলে নতুন request তৈরি করো।

Request configuration

POST

`http://127.0.0.1:8000/api/auth/register/`

Copy

Headers

```
Content-Type: application/json
```

Body → raw → JSON

```
{
  "email": "student@example.com",
  "password": "MyStrongPass!829",
  "password2": "MyStrongPass!829"
}
```

এটি একটি উদাহরণ। নিজের testing email ব্যবহার করতে পারো।

### Test A — Successful registration

Request-এর response সাধারণত এমন হবে:

```
{
  "id": 1,
  "email": "student@example.com"
}
```

Status code:

`201 Created`

Password response-এ নেই—এটাই প্রত্যাশিত।

### Test B — Duplicate email

একই request আবার পাঠাও।

Expected response:

```
{
  "email": [
    "An account with this email already exists."
  ]
}
```

সাধারণত status হবে `400 Bad Request`।

### Test C — Password mismatch

```
{
  "email": "another@example.com",
  "password": "MyStrongPass!829",
  "password2": "DifferentPass!829"
}
```

Expected: `400 Bad Request`, সঙ্গে `password2`-এর validation error।

### Test D — Weak password

```
{
  "email": "weak@example.com",
  "password": "12345678",
  "password2": "12345678"
}
```

Django-এর configured validators অনুযায়ী request reject হওয়ার কথা।

## Step 8 — Database-এ password hash হয়েছে কি না যাচাই করো

Terminal-এ:

```
python manage.py shell
```

তারপর:

```
from django.contrib.auth import get_user_modelUser = get_user_model()user = User.objects.get(email="student@example.com")print(user.password)print(user.check_password("MyStrongPass!829"))
```

প্রথম output-এ Django-এর encoded password hash দেখতে পাবে; আসল password নয়। দ্বিতীয় output হবে:

```
True
```

এভাবে database-এ password hashing কাজ করছে কি না যাচাই করতে পারবে।

## Step 9 — একটি গুরুত্বপূর্ণ production improvement

Duplicate email check করার সময় একটি subtle issue আছে: দুটি registration request একই সময়ে এলে, শুধু serializer-এর `.exists()` check যথেষ্ট নয়। Database-এর unique constraint-ই চূড়ান্ত সুরক্ষা।

আমাদের project-এ email consistently normalize করব।

`accounts/serializers.py`-এর `validate_email()` method-এ:

```
def validate_email(self, value):    email = value.strip().lower()    if User.objects.filter(email__iexact=email).exists():        raise serializers.ValidationError(            "An account with this email already exists."        )    return email
```

আর `accounts/managers.py`-এর `create_user()` method-এ:

```
email = self.normalize_email(email).strip().lower()
```

এতে এই registration flow-তে email lowercase হয়ে সংরক্ষিত হবে। তবে অন্য code path থেকেও user তৈরি করলে একই normalization policy প্রয়োগ করবে। আরও শক্তিশালী database-level case-insensitive uniqueness চাইলে PostgreSQL-এ functional unique constraint ব্যবহার করা যায়।

## Lesson 2 — Final assignment

Progress

0/6

RegisterSerializer তৈরি করেছি

Password confirmation ও Django password validation পরীক্ষা করেছি

CreateAPIView এবং registration URL configure করেছি

Postman দিয়ে successful registration পরীক্ষা করেছি

Duplicate email, mismatch ও weak password পরীক্ষা করেছি

Database-এ password hash যাচাই করেছি

আজকের lesson-এর মূল শিক্ষা: Registration API তৈরি করার অর্থ শুধু database-এ User তৈরি করা নয়। Input validation, password hashing, duplicate handling এবং API response—সবগুলো একসঙ্গে সঠিকভাবে কাজ করতে হবে।

পরবর্তী Lesson 3-এ আমরা Email Verification System তৈরি করব: verification token তৈরি, email পাঠানো, token expiry, verification endpoint এবং resend verification email। এতে registration-এর পর email verified না হওয়া পর্যন্ত account ব্যবহারের policy-ও implement করব।

---
# Lesson 3: Email Verification System — Beginner to Advanced

আজ আমরা Registration API-এর সঙ্গে Email Verification System integrate করব। এর ফলে user registration করতে পারবে, কিন্তু email verify না করা পর্যন্ত protected application features ব্যবহার করতে পারবে না।

আমরা Django REST Framework, custom User model, secure verification token এবং email service ব্যবহার করব।

## আজকের lesson-এর flow

1\. User Registration

Email + Password

2\. Account Pending

is_email_verified = False

3\. Verification Email

Secure random token + expiry

4\. Verify Email API

Token যাচাই, expiry ও single-use check

5\. Email Verified

is_email_verified = True

আজকের implementation-এ আমরা token-এর raw value database-এ রাখব না; তার hash সংরক্ষণ করব। Verification token expire হবে এবং সফলভাবে ব্যবহার হলে আবার ব্যবহার করা যাবে না।

## Step 1 — User model update করো

`accounts/models.py`-এ `User` model-এর মধ্যে নতুন field যোগ করো:

```
email_verified = models.BooleanField(default=False)
```

সম্পূর্ণ model-এর প্রাসঙ্গিক অংশ হবে:

```
from django.contrib.auth.models import AbstractUserfrom django.db import modelsfrom .managers import UserManagerclass User(AbstractUser):    username = None    email = models.EmailField(        unique=True,        db_index=True,    )    email_verified = models.BooleanField(default=False)    USERNAME_FIELD = "email"    REQUIRED_FIELDS = []    objects = UserManager()    def __str__(self):        return self.email
```

এখন migration তৈরি করো:

```
python manage.py makemigrations accounts
python manage.py migrate
```

কেন `default=False`? নতুন account তৈরি হলে email verification সম্পন্ন হয়েছে—এমন ধরে নেওয়া যাবে না।

> আগের Lesson 2-এ তৈরি registration API-কে আমরা পরবর্তীতে update করব, যাতে registration সফল হওয়ার সঙ্গে verification email পাঠানো হয়।

## Step 2 — Verification token-এর database model

নতুন file তৈরি করো: `accounts/models.py`-এর নিচে `EmailVerificationToken` model যোগ করো।

```
import hashlibfrom django.conf import settingsfrom django.db import modelsfrom django.utils import timezoneclass EmailVerificationToken(models.Model):    user = models.ForeignKey(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="email_verification_tokens",    )    token_hash = models.CharField(        max_length=64,        unique=True,    )    expires_at = models.DateTimeField()    used_at = models.DateTimeField(        null=True,        blank=True,    )    created_at = models.DateTimeField(auto_now_add=True)    class Meta:        indexes = [            models.Index(                fields=["user", "expires_at"],                name="email_verify_user_exp_idx",            ),        ]    @property    def is_expired(self):        return timezone.now() >= self.expires_at    def __str__(self):        return f"Email verification for user {self.user_id}"
```

এখন `hashlib` import-টি যদি শুধু token hashing-এর জন্য model file-এ যোগ করে থাকো, সেটি প্রয়োজন নেই—আমরা hashing service-এ করব। তাই `import hashlib` সরিয়ে দাও। Model-এর প্রয়োজনীয় imports হবে:

```
from django.conf import settingsfrom django.db import modelsfrom django.utils import timezone
```

তারপর:

```
python manage.py makemigrations accounts
python manage.py migrate
```

### Model-এর field-গুলো কেন?

- `user`: কোন account-এর verification token।
- `token_hash`: raw token-এর SHA-256 hash।
- `expires_at`: token কখন expire হবে।
- `used_at`: token ব্যবহার হয়েছে কি না; `NULL` মানে এখনো ব্যবহার হয়নি।
- `created_at`: token তৈরির সময়।

এখানে `used_at` এবং `expires_at` দিয়ে service-level verification logic enforce করতে হবে। Database-এ record থাকলেই token valid নয়।

## Step 3 — Token generation service তৈরি করো

নতুন folder ও file তৈরি করো:

```
mkdir -p accounts/services
touch accounts/services/__init__.py
touch accounts/services/email_verification_service.py
```

`accounts/services/email_verification_service.py`:

```
import hashlibimport secretsfrom datetime import timedeltafrom django.db import transactionfrom django.utils import timezonefrom accounts.models import EmailVerificationTokenTOKEN_EXPIRY_HOURS = 24def hash_verification_token(raw_token: str) -> str:    return hashlib.sha256(        raw_token.encode("utf-8")    ).hexdigest()@transaction.atomicdef create_verification_token(user):    # Invalidate any previously issued unused tokens.    EmailVerificationToken.objects.filter(        user=user,        used_at__isnull=True,    ).update(used_at=timezone.now())    raw_token = secrets.token_urlsafe(32)    record = EmailVerificationToken.objects.create(        user=user,        token_hash=hash_verification_token(raw_token),        expires_at=timezone.now()        + timedelta(hours=TOKEN_EXPIRY_HOURS),    )
```

এখানে কী হচ্ছে?

1. `secrets.token_urlsafe(32)` একটি unpredictable token তৈরি করে।
2. SHA-256 hash database-এ সংরক্ষণ করা হয়।
3. আগের unused token invalidated হয়।
4. Token ২৪ ঘণ্টা পর expire হবে।
5. Raw token শুধু email link তৈরির জন্য service থেকে ফেরত আসে।

Raw token database-এ রাখবে না। Email link-এ token থাকবেই, তাই HTTPS ব্যবহার করতে হবে এবং frontend/server logs-এ full verification URL record করা এড়িয়ে চলতে হবে।

## Step 4 — Email service তৈরি করো

নতুন file: `accounts/services/email_service.py`

```
from django.conf import settingsfrom django.core.mail import send_maildef send_verification_email(user, raw_token):    verification_url = (        f"{settings.FRONTEND_ORIGIN.rstrip('/')}"        f"/verify-email?token={raw_token}"    )    subject = "Verify your email address"    message = (        f"Hello,\n\n"        f"Verify your email using this link:\n"        f"{verification_url}\n\n"        f"This link expires in 24 hours.\n"        f"If you did not create this account, ignore this email."    )    return send_mail(        subject=subject,        message=message,        from_email=settings.DEFAULT_FROM_EMAIL,        recipient_list=[user.email],        fail_silently=False,    )
```

এটি আপাতত plain-text email। পরে HTML template ও email provider-এর delivery monitoring যোগ করা যাবে।

`config/settings.py`-এ development configuration যোগ করো:

```
# Development only: emails appear in the terminal.EMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "noreply@example.com"FRONTEND_ORIGIN = "http://localhost:5173"
```

Console backend শুধু development/testing-এর জন্য। Production-এ SMTP বা email delivery provider configure করতে হবে এবং secrets environment variables থেকে নিতে হবে।

## Step 5 — Registration-এর সঙ্গে email verification যুক্ত করো

এখন আমাদের আগের `RegisterSerializer` update করতে হবে, যেন registration-এর সময় account unverified থাকে।

`accounts/serializers.py`-এর `create()` method-টি এভাবে update করো:

```
def create(self, validated_data):    validated_data.pop("password2")    password = validated_data.pop("password")    user = User.objects.create_user(        password=password,        is_active=False,        email_verified=False,        **validated_data,    )    return user
```

এখন নতুন user তৈরি হলে:

```
user.is_active          # Falseuser.email_verified     # False
```

কেন `is_active=False`? Django-এর standard authentication backend এবং SimpleJWT-এর standard token serializer inactive user-কে authenticate করতে দেয় না। ফলে আমরা login policy-তেও verification enforce করতে পারব।

> গুরুত্বপূর্ণ: `is_active=False` দিয়ে account disable করলে admin বা অন্য কোনো trusted workflow থেকে সক্রিয় করার নিয়মও পরিষ্কার রাখতে হবে। Email verification সফল হলেই আমরা এই registration flow-তে account সক্রিয় করব।

### Registration view update

`accounts/views.py`-এ আগের `RegisterAPIView` update করো:

```
import loggingfrom rest_framework import genericsfrom rest_framework.permissions import AllowAnyfrom rest_framework.throttling import ScopedRateThrottlefrom .serializers import RegisterSerializerfrom accounts.services.email_verification_service import (    create_verification_token,)from accounts.services.email_service import send_verification_emaillogger = logging.getLogger(__name__)class RegisterAPIView(generics.CreateAPIView):    serializer_class = RegisterSerializer    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "register"    def perform_create(self, serializer):        user = serializer.save()        try:            _, raw_token = create_verification_token(user)            send_verification_email(user, raw_token)        except Exception:            # Never log the raw verification token.            logger.exception(                "Verification email could not be sent."            )
```

এই version-এ email sending ব্যর্থ হলেও user record থাকবে, তবে account inactive থাকবে। ব্যবহারকারী পরে resend endpoint দিয়ে নতুন verification email চাইতে পারবে।

Production-এ email delivery failure monitoring ও retry-এর জন্য background task বা transactional outbox ব্যবহার করা আরও নির্ভরযোগ্য।

## Step 6 — Verify Email API তৈরি করো

এখন email link থেকে পাওয়া token যাচাই করব।

### 6.1 Serializer

`accounts/serializers.py`-এ যোগ করো:

```
class VerifyEmailSerializer(serializers.Serializer):    token = serializers.CharField(        write_only=True,        trim_whitespace=False,    )
```

### 6.2 Verification service

`accounts/services/email_verification_service.py`-এর নিচে যোগ করো:

```
from django.db import transactionclass InvalidVerificationToken(Exception):    pass@transaction.atomicdef verify_email_token(raw_token: str):    token_hash = hash_verification_token(raw_token)    record = (        EmailVerificationToken.objects        .select_for_update()        .select_related("user")        .filter(token_hash=token_hash)        .first()    )    if record is None:        raise InvalidVerificationToken    if record.used_at is not None or record.is_expired:        raise InvalidVerificationToken    user = record.user    record.used_at = timezone.now()    record.save(update_fields=["used_at"])    user.email_verified = True    user.is_active = True    user.save(update_fields=["email_verified", "is_active"])    # Invalidate any other outstanding verification tokens.    EmailVerificationToken.objects.filter(        user=user,        used_at__isnull=True,    ).exclude(pk=record.pk).update(used_at=timezone.now())    return user
```

এই service-এ `transaction` ও `timezone` imports আগে থেকেই file-এ আছে। একই file-এ `EmailVerificationToken` model import-টিও থাকতে হবে।

Security behavior:

- Unknown token → reject।
- Expired token → reject।
- Previously used token → reject।
- Valid token → email verified এবং account active।
- একবার সফল হলে token আবার ব্যবহার করা যাবে না।

PostgreSQL-এর row locking concurrent verification request নিয়ন্ত্রণে সহায়তা করে। SQLite দিয়ে production concurrency behavior যাচাই করা যাবে না।

### 6.3 API view

`accounts/views.py`-এ যোগ করো:

```
from rest_framework import statusfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom rest_framework.exceptions import ValidationErrorfrom .serializers import VerifyEmailSerializerfrom accounts.services.email_verification_service import (    verify_email_token,    InvalidVerificationToken,)class VerifyEmailAPIView(APIView):    permission_classes = [AllowAny]    def post(self, request):        serializer = VerifyEmailSerializer(data=request.data)        serializer.is_valid(raise_exception=True)        try:            verify_email_token(serializer.validated_data["token"])        except InvalidVerificationToken:            raise ValidationError({                "token": "Invalid or expired verification token."            })        return Response(            {"detail": "Email verified successfully."},            status=status.HTTP_200_OK,        )
```

এখন frontend verification link থেকে token পড়বে এবং POST request পাঠাবে। Token-টি URL query string-এ থাকে বলে frontend-এ সেটি ব্যবহার করার পর address bar থেকে সরিয়ে দেওয়া, referrer leakage প্রতিরোধ করা এবং analytics/logging-এ token না পাঠানো গুরুত্বপূর্ণ।

## Step 7 — Resend Verification Email API

ব্যবহারকারী email না পেলে নতুন verification email চাইতে পারবে। এই endpoint-এ unknown email এবং known email-এর জন্য একই response দেব, যাতে account enumeration কমানো যায়।

### 7.1 Serializer

`accounts/serializers.py`-এ যোগ করো:

```
class ResendVerificationEmailSerializer(serializers.Serializer):    email = serializers.EmailField()
```

### 7.2 View

`accounts/views.py`-এ যোগ করো:

```
from django.contrib.auth import get_user_modelfrom .serializers import ResendVerificationEmailSerializerfrom accounts.services.email_verification_service import (    create_verification_token,)from accounts.services.email_service import send_verification_emailUser = get_user_model()class ResendVerificationEmailAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "resend_verification"    def post(self, request):        serializer = ResendVerificationEmailSerializer(            data=request.data        )        serializer.is_valid(raise_exception=True)        email = serializer.validated_data["email"].strip()        user = User.objects.filter(            email__iexact=email,            email_verified=False,            is_active=False,        ).first()        if user:            try:                _, raw_token = create_verification_token(user)                send_verification_email(user, raw_token)            except Exception:                logger.exception(                    "Verification resend failed."                )        return Response({            "detail": (                "If an unverified account exists for this email, "                "verification instructions will be sent."            )        }, status=status.HTTP_200_OK)
```

এখানে একটি গুরুত্বপূর্ণ সীমাবদ্ধতা আছে: generic response account enumeration কমালেও, email-based cooldown এবং distributed rate limiting-এর বিকল্প নয়। Production-এ একই email-এ বারবার email পাঠানো আটকাতে cooldown এবং IP/email-based shared rate limits যোগ করতে হবে।

## Step 8 — URL configuration

`accounts/urls.py` update করো:

```
from django.urls import pathfrom .views import (    RegisterAPIView,    VerifyEmailAPIView,    ResendVerificationEmailAPIView,)urlpatterns = [    path(        "register/",        RegisterAPIView.as_view(),        name="register",    ),    path(        "email/verify/",        VerifyEmailAPIView.as_view(),        name="verify-email",    ),    path(        "email/resend-verification/",        ResendVerificationEmailAPIView.as_view(),        name="resend-verification-email",    ),]
```

এখন আমাদের endpoint-গুলো:

| Method | Endpoint                               | কাজ                                                   |
| ------ | -------------------------------------- | ----------------------------------------------------- |
| POST   | `/api/auth/register/`                  | নতুন account তৈরি ও verification email পাঠানোর চেষ্টা |
| POST   | `/api/auth/email/verify/`              | Token যাচাই করে account activate                      |
| POST   | `/api/auth/email/resend-verification/` | নতুন verification email পাঠানোর চেষ্টা                |

`config/urls.py`-এ আগের `include("accounts.urls")` থাকলে পরিবর্তন করতে হবে না।

## Step 9 — Postman দিয়ে সম্পূর্ণ flow test করো

### Test A: Registration

POST

`http://127.0.0.1:8000/api/auth/register/`

Body → raw → JSON

```
{
  "email": "student@example.com",
  "password": "MyStrongPass!829",
  "password2": "MyStrongPass!829"
}
```

Development console email backend ব্যবহার করলে verification email-এর link terminal-এ দেখা যাবে। এই link-এ থাকা raw token শুধু development testing-এর জন্য ব্যবহার করো।

### Test B: Verify email

Terminal-এর email থেকে token কপি করো। তারপর:

POST

`http://127.0.0.1:8000/api/auth/email/verify/`

Body → raw → JSON

```
{
  "token": "PASTE_REAL_TOKEN_HERE"
}
```

সফল হলে:

```
{
  "detail": "Email verified successfully."
}
```

Status: `200 OK`

### Test C: Token দ্বিতীয়বার ব্যবহার

একই token আবার পাঠাও। Expected: `400 Bad Request`।

### Test D: Resend verification email

POST

`http://127.0.0.1:8000/api/auth/email/resend-verification/`

Body → raw → JSON

```
{
  "email": "student@example.com"
}
```

Expected: generic `200 OK` response। Account unverified থাকলে নতুন email পাঠানোর চেষ্টা হবে। Account verified হলে বা account না থাকলেও response একই থাকবে।

## Step 10 — Registration throttling configure করো

`config/settings.py`-এর existing `REST_FRAMEWORK` dictionary-তে এই rate-গুলো merge করো:

```
"DEFAULT_THROTTLE_RATES": {    "register": "5/hour",    "resend_verification": "5/hour",},
```

এটি `ScopedRateThrottle`-এর জন্য baseline protection। Production-এ Redis-backed email/IP limits, cooldown এবং email sending retry policy-ও implement করতে হবে।

## Step 11 — Unverified user-কে protected features থেকে আটকানো

আমাদের registration flow-তে `is_active=False` রাখা হয়েছে। Django-এর standard authentication ও SimpleJWT token obtain flow inactive user-কে login করতে দেবে না।

তবুও protected API-তে email verification-এর জন্য আলাদা permission রাখা ভালো—বিশেষ করে project-এ আগে থেকে authenticated sessions বা custom token logic থাকলে।

`accounts/permissions.py` তৈরি করো:

```
from rest_framework.permissions import BasePermissionclass IsEmailVerified(BasePermission):    message = "Please verify your email first."    def has_permission(self, request, view):        user = request.user        return bool(            user            and user.is_authenticated            and user.is_active            and user.email_verified        )
```

যে protected API-তে verified email বাধ্যতামূলক, সেখানে:

```
from rest_framework.permissions import IsAuthenticatedfrom accounts.permissions import IsEmailVerifiedclass ExampleProtectedAPIView(APIView):    permission_classes = [        IsAuthenticated,        IsEmailVerified,    ]
```

এই permission সব endpoint-এ অন্ধভাবে প্রয়োগ করবে না। Registration, login, email verification, resend এবং password reset-এর মতো public authentication endpoints-এ `AllowAny` policy লাগবে।

### Superuser-এর জন্য ছোট adjustment

যেহেতু `UserManager`-এ `email_verified` field এখন যোগ হয়েছে, `create_superuser()`-এ এটিও default হিসেবে সেট করতে পারো:

```
extra_fields.setdefault("email_verified", True)
```

এটি `is_staff`, `is_superuser` এবং `is_active`-এর defaults-এর পাশে রাখবে। এতে management command দিয়ে তৈরি superuser-কে email verification flow দিয়ে যেতে হবে না।

## Step 12 — Final verification checklist

Lesson 3 completion

0/10

Registration-এর পর email_verified=False

Registration-এর পর is_active=False

Email-এ verification token পাঠানোর চেষ্টা হয়

Valid token দিয়ে email_verified=True ও is_active=True হয়

Expired token reject হয়

Used token আবার ব্যবহার করা যায় না

Unknown email-এ resend response একই থাকে

Protected API unverified account reject করে

Raw token database-এ রাখা হয় না

Production-এ HTTPS ও rate limiting configure করা আছে

একটি বাস্তব production note: Verification token তৈরি করা ও email পাঠানো এখন দুটি আলাদা operation। Email provider ব্যর্থ হলে token record তৈরি হয়ে থাকতে পারে, তাই resend logic, token invalidation, monitoring ও retry strategy সঠিকভাবে পরীক্ষা করবে। Production-এ email link-এর token যেন logs, analytics বা third-party referrer-এ leak না হয় সেটিও নিশ্চিত করতে হবে।

পরবর্তী Lesson 4 হবে Login API + JWT Access Token & Refresh Token। সেখানে `TokenObtainPairView`, custom login validation, unverified account rejection, access/refresh token এবং Postman দিয়ে login testing তৈরি করব।

----
# Lesson 4: Login API + JWT Access Token & Refresh Token

আজ আমরা Django REST Framework authentication system-এ Login API তৈরি করব এবং JWT access ও refresh token implement করব।

আমাদের আগের Lesson-গুলোতে Custom User Model, Registration এবং Email Verification তৈরি করেছি। এবার verified user email ও password দিয়ে login করতে পারবে। Email verify না করা account login করতে পারবে না।

## আজকের lesson শেষে যা তৈরি হবে

- `TokenObtainPairView` দিয়ে JWT login
- Email ও password দিয়ে authentication
- Unverified user-এর login reject করা
- Access token দিয়ে protected API access
- Refresh token দিয়ে নতুন access token নেওয়া
- Postman দিয়ে success ও failure test

## ১. JWT authentication কীভাবে কাজ করে?

1\. Login request

Email + Password

2\. Django validates user

Password, is_active, email_verified

Access Token

Protected APIs

Refresh Token

New access token

Access token অল্প সময়ের জন্য API access দেয়। Refresh token ব্যবহার করে নতুন access token নেওয়া যায়। Refresh token নিজেও sensitive credential—এটি access token-এর মতো প্রতিটি API request-এ পাঠাবে না।

## Step 1 — Simple JWT configure করো

Lesson 1-এ আমরা `djangorestframework-simplejwt` install করেছি। না থাকলে:

```
pip install djangorestframework-simplejwt
```

`config/settings.py`-এর `REST_FRAMEWORK` dictionary-তে নিচের configuration merge করো। আগে থেকে `DEFAULT_THROTTLE_RATES` বা অন্য settings থাকলে সেগুলো মুছে ফেলবে না।

```
REST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],    "DEFAULT_THROTTLE_RATES": {        "register": "5/hour",        "resend_verification": "5/hour",    },}
```

এখানে `IsAuthenticated` default করায় protected API-তে login করা লাগবে। Registration, login, email verification এবং password reset-এর মতো public endpoint-এ `AllowAny` স্পষ্টভাবে সেট করতে হবে।

এবার `settings.py`-তে যোগ করো:

```
from datetime import timedelta
```

```
SIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,    "UPDATE_LAST_LOGIN": True,}
```

এগুলো এই course-এর learning configuration। Production-এ token lifetime, refresh token storage এবং revocation policy তোমার threat model অনুযায়ী ঠিক করতে হবে।

## Step 2 — Refresh token blacklist enable করো

যেহেতু আমরা refresh token rotation ও blacklist ব্যবহার করতে চাই, `config/settings.py`-এর `INSTALLED_APPS`-এ যোগ করো:

```
INSTALLED_APPS = [    # Django apps ...    "rest_framework",    "corsheaders",    "rest_framework_simplejwt.token_blacklist",    "accounts",]
```

এরপর migration চালাও:

```
python manage.py migrate
```

কেন দরকার? Refresh token rotate হলে আগের refresh token blacklist করা যায়। এই app ছাড়া `BLACKLIST_AFTER_ROTATION=True`-এর প্রত্যাশিত revocation behavior পাওয়া যাবে না।

## Step 3 — Custom Login Serializer তৈরি করো

আমাদের custom User model-এ `USERNAME_FIELD = "email"` আছে, তাই SimpleJWT email field দিয়ে user খুঁজতে পারবে। কিন্তু verified email ছাড়া token দেওয়া যাবে না—এই rule-টি আমরা যোগ করব।

`accounts/serializers.py`-এর শেষে যোগ করো:

```
from rest_framework.exceptions import AuthenticationFailedfrom rest_framework_simplejwt.serializers import (    TokenObtainPairSerializer,)class CustomTokenObtainPairSerializer(    TokenObtainPairSerializer):    def validate(self, attrs):        data = super().validate(attrs)        if not self.user.email_verified:            raise AuthenticationFailed(                "Please verify your email before logging in."            )        return data
```

### Code explanation

- `TokenObtainPairSerializer` email/password validate করে।
- Django authentication backend inactive user-কে reject করবে।
- `email_verified=False` হলে custom error হবে।
- Verified user হলে response-এ access ও refresh token থাকবে।

এখানে `super().validate(attrs)` token pair তৈরি করে, তারপর verification check হয়। Unverified user-এর token response-এ ফেরত যায় না, তবে আরও পরিষ্কার design-এর জন্য token তৈরির আগেই verification check করতে চাইলে custom authentication serializer-এর flow আলাদাভাবে implement করা যায়।

## Step 4 — Login API View তৈরি করো

`accounts/views.py`-এর শেষে যোগ করো:

```
from rest_framework_simplejwt.views import TokenObtainPairViewclass LoginAPIView(TokenObtainPairView):    serializer_class = CustomTokenObtainPairSerializer    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "login"
```

ফাইলের import-এ `CustomTokenObtainPairSerializer` যোগ করতে হবে:

```
from .serializers import (    RegisterSerializer,    CustomTokenObtainPairSerializer,)
```

তোমার existing `serializers.py`-এ অন্য serializer থাকলে সেগুলোও রাখবে; শুধু import list-এ যোগ করবে।

`AllowAny` প্রয়োজন, কারণ login করার আগে user authenticated নয়।

## Step 5 — Login ও Refresh URL তৈরি করো

`accounts/urls.py` update করো:

```
from django.urls import pathfrom rest_framework_simplejwt.views import TokenRefreshViewfrom .views import (    RegisterAPIView,    VerifyEmailAPIView,    ResendVerificationEmailAPIView,    LoginAPIView,)urlpatterns = [    path(        "register/",        RegisterAPIView.as_view(),        name="register",    ),    path(        "email/verify/",        VerifyEmailAPIView.as_view(),        name="verify-email",    ),    path(        "email/resend-verification/",        ResendVerificationEmailAPIView.as_view(),        name="resend-verification-email",    ),    path(        "login/",        LoginAPIView.as_view(),        name="login",    ),    path(        "token/refresh/",        TokenRefreshView.as_view(),        name="token-refresh",
```

এখন API endpoints:

| Method | Endpoint                   | কাজ                                  |
| ------ | -------------------------- | ------------------------------------ |
| POST   | `/api/auth/login/`         | Email/password দিয়ে login            |
| POST   | `/api/auth/token/refresh/` | Refresh token দিয়ে নতুন access token |

## Step 6 — Login rate limit configure করো

`config/settings.py`-এর `REST_FRAMEWORK["DEFAULT_THROTTLE_RATES"]`-এ যোগ করো:

```
"login": "10/minute",
```

এটি আগের rates-এর পাশাপাশি থাকবে। উদাহরণ:

```
"DEFAULT_THROTTLE_RATES": {    "register": "5/hour",    "resend_verification": "5/hour",    "login": "10/minute",},
```

DRF throttle abuse কমাতে সাহায্য করে, তবে এটি distributed brute-force protection-এর বিকল্প নয়। Production-এ shared Redis-backed rate limits, IP/email limits এবং monitoring ব্যবহার করবে।

## Step 7 — Postman দিয়ে Login test করো

Server চালাও:

```
python manage.py check
python manage.py runserver
```

### Test A: Verified user login

Postman-এ নতুন request তৈরি করো।

POST

Login endpoint

`http://127.0.0.1:8000/api/auth/login/`

Body → raw → JSON

```
{
  "email": "student@example.com",
  "password": "MyStrongPass!829"
}
```

&#x20;Copy login URL

Verified ও active user হলে response-এ এই ধরনের JSON পাবে:

```
{
  "refresh": "<refresh-token>",
  "access": "<access-token>"
}
```

Token-এর আসল value এখানে দেখানো হয়নি; Postman response থেকে তোমার token ব্যবহার করবে।

### Test B: Unverified user login

Registration-এর পরে email verification সম্পন্ন না করা user-এর email/password দিয়ে login করো।

Expected: `401 Unauthorized` এবং verification-সংক্রান্ত error message।

যদি user-এর `is_active=False` থাকে, তাহলে Django authentication আগেই reject করতে পারে। তাই response-এ ঠিক কোন error দেখাবে তা request যে validation stage-এ ব্যর্থ হচ্ছে তার ওপর নির্ভর করবে।

### Test C: ভুল password

```
{
  "email": "student@example.com",
  "password": "WrongPassword123!"
}
```

Expected: `401 Unauthorized`। Error response-এ password ভুল নাকি account আছে—এমন sensitive distinction প্রকাশ না করাই ভালো।

## Step 8 — Access token দিয়ে protected API test

প্রথমে `accounts/views.py`-এ একটি temporary test endpoint যোগ করো:

```
from rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewclass MeAPIView(APIView):    permission_classes = [IsAuthenticated]    def get(self, request):        return Response({            "id": request.user.id,            "email": request.user.email,            "email_verified": request.user.email_verified,        })
```

`accounts/urls.py`-এ import করে URL যোগ করো:

```
path("me/", MeAPIView.as_view(), name="me"),
```

Postman-এ:

- Method: `GET`
- URL: `http://127.0.0.1:8000/api/auth/me/`
- Authorization → Type: `Bearer Token`
- Token: login response থেকে পাওয়া `access` token

Expected response:

```
{
  "id": 1,
  "email": "student@example.com",
  "email_verified": true
}
```

Token ছাড়া request পাঠালে সাধারণত `401 Unauthorized` পাবে।

## Step 9 — Refresh token দিয়ে নতুন access token

Login response থেকে পাওয়া refresh token ব্যবহার করো।

POST

Refresh endpoint

`http://127.0.0.1:8000/api/auth/token/refresh/`

Body → raw → JSON

```
{
  "refresh": "<your-refresh-token>"
}
```

Rotation enabled থাকলে response-এ নতুন `access` এবং নতুন `refresh` token পাবে। পরবর্তী refresh-এর জন্য নতুন refresh token ব্যবহার করবে; পুরোনো token blacklist হয়ে যেতে পারে।

Security rule: Refresh token browser local storage-এ রাখার বদলে web application-এর জন্য secure, HttpOnly cookie-based strategy বিবেচনা করো। Cookie ব্যবহার করলে CSRF protection-ও সঠিকভাবে configure করতে হবে। Frontend storage strategy ও logout flow আমরা পরবর্তী lessons-এ আরও বিস্তারিত করব।

## Step 10 — Login serializer-এর production improvement

আগের Step 3-এর serializer-এ token তৈরি হওয়ার পরে `email_verified` পরীক্ষা করা হয়েছিল। আরও ভালো design হলো token তৈরি করার আগেই verification check করা।

`accounts/serializers.py`-এর login serializer-টি নিচের version দিয়ে replace করো:

```
from rest_framework.exceptions import AuthenticationFailedfrom rest_framework_simplejwt.serializers import (    TokenObtainPairSerializer,    TokenObtainSerializer,)class CustomTokenObtainPairSerializer(    TokenObtainPairSerializer):    def validate(self, attrs):        # Authenticate credentials first.        data = TokenObtainSerializer.validate(self, attrs)        # Reject unverified users before creating JWTs.        if not self.user.email_verified:            raise AuthenticationFailed(                "Please verify your email before logging in."            )        # Generate tokens only for verified users.        refresh = self.get_token(self.user)        data["refresh"] = str(refresh)        data["access"] = str(refresh.access_token)        return data
```

এখানে `TokenObtainSerializer.validate()` প্রথমে credentials authenticate করে, তারপর আমরা email verification check করি। সফল হলে তবেই access ও refresh token তৈরি হয়।

## Step 11 — Final checklist

Lesson 4 completion

0/8

Verified user email ও password দিয়ে login করতে পারে

Unverified বা inactive user JWT পায় না

ভুল password দিলে login reject হয়

Access token দিয়ে protected endpoint ব্যবহার করা যায়

Access token ছাড়া protected endpoint reject করে

Refresh token দিয়ে নতুন access token পাওয়া যায়

Refresh rotation ও blacklist behavior পরীক্ষা করেছি

Login endpoint-এ throttling configure করেছি

### আজকের lesson-এর মূল শিক্ষা

- Registration user তৈরি করে।
- Email verification account ব্যবহারের অনুমতি নির্ধারণ করে।
- Login credentials যাচাই করে JWT দেয়।
- Access token protected API access দেয়।
- Refresh token নতুন access token পেতে সাহায্য করে।
- Refresh token blacklist করলেও আগে থেকে issue করা access token স্বয়ংক্রিয়ভাবে সঙ্গে সঙ্গে বাতিল হয় না।

পরবর্তী Lesson 5: Logout API + Refresh Token Blacklisting + Token Revocation Policy। সেখানে logout endpoint, refresh token blacklist, token rotation test এবং password reset-এর পরে পুরোনো authentication tokens কীভাবে handle করতে হবে তা implement করব।

----
# Lesson 5: Logout API + Refresh Token Blacklisting + Token Revocation Policy

আজ আমরা Authentication System-এর একটি গুরুত্বপূর্ণ অংশ তৈরি করব: Logout, Refresh Token Revocation এবং Password Reset-এর পরে পুরোনো token কীভাবে নিয়ন্ত্রণ করতে হয়।

একটি বিষয় আগে বুঝে রাখো: JWT authentication-এ logout করা মানেই সব token তাৎক্ষণিকভাবে বাতিল হয়ে যাওয়া নয়। বিশেষ করে access token সাধারণত expiry পর্যন্ত valid থাকে, যদি না application অতিরিক্ত revocation ব্যবস্থা implement করে।

## আজকের lesson-এ কী তৈরি করব?

- `POST /api/auth/logout/` — refresh token blacklist করা
- Refresh token rotation ও পুরোনো refresh token বাতিল পরীক্ষা
- Invalid বা expired refresh token handle করা
- Password reset-এর পরে পুরোনো refresh token বাতিল করা
- Access token revocation-এর সীমাবদ্ধতা বোঝা
- Postman দিয়ে logout ও token reuse test করা

## ১. JWT token lifecycle

Login

Access token + Refresh token

Access token

API requests

Refresh token

Issue new access token

Logout

Refresh token blacklist করা হয়

আমাদের current configuration-এ refresh token blacklist করা যায়, কিন্তু logout-এর আগেই issue করা access token-এর জন্য আলাদা revocation strategy লাগতে পারে।

## Step 1 — Blacklist app যাচাই করো

Lesson 4-এ আমরা এই app যোগ করেছিলাম:

```
# config/settings.pyINSTALLED_APPS = [    # Existing Django apps...    "rest_framework",    "rest_framework_simplejwt.token_blacklist",    "accounts",]
```

JWT configuration-এ rotation চালু রাখো:

```
from datetime import timedeltaSIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}
```

তারপর:

```
python manage.py migrate
```

Simple JWT-এর blacklist app refresh token ও outstanding token-এর records database-এ রাখে। এই records ব্যবহার করে revoked refresh token আবার ব্যবহার করা আটকানো যায়।

## Step 2 — Logout serializer তৈরি করো

`accounts/serializers.py`-এর শেষে যোগ করো:

```
from rest_framework import serializersfrom rest_framework_simplejwt.tokens import RefreshTokenfrom rest_framework_simplejwt.exceptions import TokenErrorclass LogoutSerializer(serializers.Serializer):    refresh = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    def validate(self, attrs):        try:            self.token = RefreshToken(attrs["refresh"])        except TokenError:            raise serializers.ValidationError({                "refresh": "Invalid or expired refresh token."            })        return attrs    def save(self, **kwargs):        self.token.blacklist()
```

### Code explanation

- `refresh` field-এ client-এর refresh token আসবে।
- `RefreshToken(...)` token-এর validity যাচাই করে।
- `blacklist()` refresh token-টিকে revoke করে।
- Token invalid বা expired হলে validation error ফেরত আসে।

গুরুত্বপূর্ণ: Serializer token-টিকে blacklist করে, কিন্তু tokenটি যে user-এর—সেটি access token দিয়ে authenticate করা user-এর সঙ্গে মেলে কি না, তা এই code যাচাই করে না। পরের ধাপে আমরা এই বিষয়টি ঠিক করব।

## Step 3 — নিরাপদ Logout API তৈরি করো

`accounts/views.py`-এ যোগ করো:

```
from rest_framework import statusfrom rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom .serializers import LogoutSerializerclass LogoutAPIView(APIView):    permission_classes = [IsAuthenticated]    def post(self, request):        serializer = LogoutSerializer(data=request.data)        serializer.is_valid(raise_exception=True)        # Ensure the refresh token belongs to the logged-in user.        refresh_token = serializer.validated_data["refresh"]        token = serializer.token        if str(token["user_id"]) != str(request.user.pk):            return Response(                {"detail": "Invalid refresh token."},                status=status.HTTP_400_BAD_REQUEST,            )        serializer.save()        return Response(            {"detail": "Logout successful."},            status=status.HTTP_200_OK,        )
```

এই version-এ `serializer.token`-এ validated refresh token পাওয়া যাচ্ছে। `user_id` comparison refresh token-এর identity-কে current authenticated user-এর সঙ্গে মিলিয়ে দেখে।

তবে JWT-এর `user_id` claim নির্ভর করে তোমার `SIMPLE_JWT["USER_ID_CLAIM"]` configuration-এর ওপর। Default হলো `"user_id"`। Custom claim ব্যবহার করলে view-এ সেটিও মিলিয়ে নিতে হবে।

## Step 4 — Logout URL যোগ করো

`accounts/urls.py`-এর import list-এ `LogoutAPIView` যোগ করো এবং urlpatterns-এ এই route রাখো:

```
path("logout/", LogoutAPIView.as_view(), name="logout"),
```

এখন logout endpoint:

`POST http://127.0.0.1:8000/api/auth/logout/`

## Step 5 — Postman দিয়ে Logout test করো

প্রথমে verified user দিয়ে login করো:

`POST /api/auth/login/`

Response থেকে `access` এবং `refresh` token নাও।

তারপর logout request পাঠাও:

POST

Logout

`http://127.0.0.1:8000/api/auth/logout/`

Authorization → Bearer Token

Login response-এর `access` token ব্যবহার করো।

Body → raw → JSON

```
{
  "refresh": "<your-refresh-token>"
}
```

সফল হলে:

```
{
  "detail": "Logout successful."
}
```

তারপর একই refresh token দিয়ে request পাঠাও:

`POST /api/auth/token/refresh/`

```
{
  "refresh": "<same-refresh-token>"
}
```

এবার refresh request reject হওয়ার কথা, কারণ token blacklist হয়েছে।

মনে রাখবে: Logout endpoint-এর response সফল হলেও পুরোনো access token সঙ্গে সঙ্গে invalid হয় না। সেটি expiry পর্যন্ত চলতে পারে, যদি আলাদা access-token revocation ব্যবস্থা না থাকে।

## Step 6 — Refresh token rotation test করো

এই test-টি logout-এর আগে, নতুন login session দিয়ে করবে।

1. Login করে `refresh_A` এবং `access_A` সংগ্রহ করো।
2. `refresh_A` দিয়ে `/api/auth/token/refresh/` call করো।
3. Response থেকে `refresh_B` এবং `access_B` সংগ্রহ করো।
4. আবার `refresh_A` ব্যবহার করার চেষ্টা করো।
5. এরপর `refresh_B` দিয়ে refresh করে দেখো।

Expected behavior:

| Action               | Expected result                      |
| -------------------- | ------------------------------------ |
| প্রথমবার `refresh_A` | নতুন token pair                      |
| আবার `refresh_A`     | Reject                               |
| `refresh_B`          | নতুন token pair, যদি এখনো valid থাকে |

Rotation-এর সময় পুরোনো refresh token blacklist হয়। তবে একই refresh token দিয়ে একাধিক concurrent request করলে race condition হতে পারে। Production frontend-এ refresh request serialize করা বা single-flight mechanism ব্যবহার করা ভালো।

## Step 7 — Password reset-এর পরে সব refresh token revoke করো

আমাদের policy হবে: Password reset হলে user-এর সব existing refresh token বাতিল হবে। এতে পুরোনো refresh token দিয়ে নতুন access token নেওয়া যাবে না।

নতুন file তৈরি করো:

`accounts/services/token_service.py`

```
from django.db import transactionfrom rest_framework_simplejwt.token_blacklist.models import (    OutstandingToken,    BlacklistedToken,)@transaction.atomicdef revoke_user_refresh_tokens(user):    outstanding_tokens = OutstandingToken.objects.filter(        user=user,    )    for outstanding in outstanding_tokens:        BlacklistedToken.objects.get_or_create(            token=outstanding,        )
```

এই service-টি user-এর জন্য সংরক্ষিত সব outstanding refresh token blacklist করে। আগে থেকেই blacklist করা token থাকলেও `get_or_create()` duplicate record তৈরি করবে না।

### Password reset service-এর সঙ্গে integrate করো

আমাদের আগের password reset service-এ password save করার পরে এই function call করো:

```
from accounts.services.token_service import (    revoke_user_refresh_tokens,)
```

তারপর password পরিবর্তনের transaction-এর ভেতরে:

```
user.set_password(new_password)user.save(update_fields=["password"])revoke_user_refresh_tokens(user)
```

এটি `transaction.atomic()`-এর মধ্যে থাকলে password update এবং refresh-token revocation একই database transaction-এ সম্পন্ন হতে পারে। তোমার আগের service-এ grant validation, password validation ও grant-used status-এর logic অক্ষুণ্ণ রাখবে।

একটি গুরুত্বপূর্ণ সীমাবদ্ধতা: এই service refresh token revoke করে, কিন্তু ইতোমধ্যে issue করা access token-কে সঙ্গে সঙ্গে বাতিল করে না।

## Step 8 — Access token-ও revoke করার policy

এখানে দুইটি design আছে।

- Basic policy: Access token-এর lifetime ১০ মিনিট রাখবে। Password reset-এর পরে সব refresh token blacklist করবে। পুরোনো access token সর্বোচ্চ তার expiry পর্যন্ত valid থাকতে পারে।
- Strict policy: User-এর `token_version` ব্যবহার করে প্রতিটি authenticated request-এ token-এর version যাচাই করবে। Password reset হলে version বাড়িয়ে পুরোনো access token-ও reject করা যাবে।

যেসব application-এ password reset-এর পর পুরোনো session সঙ্গে সঙ্গে বন্ধ করা জরুরি, সেখানে দ্বিতীয় পদ্ধতি বিবেচনা করো।

### 8.1 — User model-এ token version যোগ করো

`accounts/models.py`-এর `User` model-এ যোগ করো:

```
token_version = models.PositiveIntegerField(default=0)
```

তারপর:

```
python manage.py makemigrations accounts
python manage.py migrate
```

### 8.2 — Login token-এ version যোগ করো

`CustomTokenObtainPairSerializer`-এ এই method যোগ করো:

```
@classmethoddef get_token(cls, user):    token = super().get_token(user)    token["token_version"] = user.token_version    return token
```

এতে login-এর সময় তৈরি refresh token-এ `token_version` থাকবে এবং তার থেকে তৈরি access token-এও claim-টি থাকবে।

### 8.3 — Custom JWT authentication তৈরি করো

নতুন file: `accounts/authentication.py`

```
from rest_framework.exceptions import AuthenticationFailedfrom rest_framework_simplejwt.authentication import JWTAuthenticationclass VersionedJWTAuthentication(JWTAuthentication):    def get_user(self, validated_token):        user = super().get_user(validated_token)        token_version = validated_token.get("token_version")        if token_version != user.token_version:            raise AuthenticationFailed(                "Token is no longer valid. Please log in again."            )        return user
```

`config/settings.py`-এর `REST_FRAMEWORK`-এ default JWT authentication class পরিবর্তন করো:

```
"DEFAULT_AUTHENTICATION_CLASSES": [    "accounts.authentication.VersionedJWTAuthentication",],
```

এখন `token_version` claim না থাকা পুরোনো JWT-ও reject হবে। Development-এ নতুন করে login করে token নিতে হবে।

### 8.4 — Password reset-এর পরে version বাড়াও

Password reset service-এ password save করার সময়:

```
user.set_password(new_password)user.token_version += 1user.save(    update_fields=["password", "token_version"])revoke_user_refresh_tokens(user)
```

এই code তোমার আগের `transaction.atomic()`-এর মধ্যে রাখবে।

এখন password reset হলে:

1. Password পরিবর্তিত হবে।
2. `token_version` বাড়বে।
3. সব outstanding refresh token blacklist হবে।
4. আগের version-সহ access token পরবর্তী authenticated request-এ reject হবে।

সীমাবদ্ধতা: Version check প্রতিটি authenticated request-এ user record পড়বে; caching ব্যবহার করলে revocation দ্রুত করতে cache invalidation policy লাগবে। এটি logout-এর জন্য সব device revoke করে দেয় না—এই উদাহরণে version বাড়ানো হবে password reset-এর সময়। একক device logout-এর জন্য refresh token blacklist করা হবে; সেই device-এর access token expiry পর্যন্ত চলতে পারে।

## Step 9 — Final test checklist

Lesson 5 completion

0/8

Logout API authenticated user ছাড়া ব্যবহার করা যায় না

অন্য user-এর refresh token দিয়ে logout করা যায় না

Logout-এর পর refresh token reject হয়

Rotation-এর পর পুরোনো refresh token reject হয়

Password reset-এর পর সব refresh token blacklist হয়

Token version চালু থাকলে পুরোনো access token reject হয়

নতুন password দিয়ে login করলে নতুন token pair পাওয়া যায়

Refresh token ও access token application logs-এ প্রকাশ পায় না

আজকের মূল শিক্ষা: JWT logout, refresh token revocation এবং access token revocation এক জিনিস নয়। কোন token কীভাবে বাতিল হবে, সেটি application-এর security policy-তে স্পষ্টভাবে নির্ধারণ করতে হয়।

পরবর্তী Lesson 6-এ আমরা Change Password API + Current Password Validation + Password Policy + Token Revocation Integration তৈরি করব—যেখানে logged-in user নিজের password পরিবর্তন করতে পারবে এবং password পরিবর্তনের পর পুরোনো tokens কীভাবে handle করতে হবে, তা পরীক্ষা করব।

----
# Lesson 6: Change Password API — DRF Authentication System

এই lesson-এ আমরা logged-in user-এর জন্য একটি production-oriented Change Password API তৈরি করব। User-কে নিজের বর্তমান password দিতে হবে, নতুন password policy pass করতে হবে, এবং password পরিবর্তনের পর পুরোনো authentication tokens revoke করতে হবে।

আমাদের আগের project structure-ই ব্যবহার করব:

```
complete_auth_project/
├── config/
│   └── settings.py
└── accounts/
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── urls.py
    ├── authentication.py
    └── services/
        └── token_service.py
```

## ১. API design

POST

` /api/auth/change-password/`

Request body

```
{
  "current_password": "OldStrongPass!123",
  "new_password": "NewStrongPass!456",
  "confirm_password": "NewStrongPass!456"
}
```

Security requirements

- User অবশ্যই authenticated হতে হবে।
- Current password সঠিক হতে হবে।
- নতুন password ও confirmation মিলতে হবে।
- Django-এর password validators pass করতে হবে।
- Password পরিবর্তনের পরে refresh token revoke করতে হবে।
- `token_version` ব্যবহার করলে পুরোনো access token-ও reject হবে।

## ২. Password policy configure করো

`config/settings.py`-এ `AUTH_PASSWORD_VALIDATORS` যাচাই করো। Default validators থাকলে সেগুলো replace না করে প্রয়োজন অনুযায়ী configure করো।

```
AUTH_PASSWORD_VALIDATORS = [    {        "NAME": (            "django.contrib.auth.password_validation."            "UserAttributeSimilarityValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "MinimumLengthValidator"        ),        "OPTIONS": {            "min_length": 12,        },    },    {        "NAME": (            "django.contrib.auth.password_validation."            "CommonPasswordValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "NumericPasswordValidator"        ),    },]
```

এখানে minimum length ১২ করা হয়েছে। বাস্তব application-এ password policy এমন হওয়া উচিত, যাতে password যথেষ্ট দীর্ঘ ও অনুমান করা কঠিন হয়। বাধ্যতামূলক uppercase, lowercase, digit ও special character-এর নিয়ম সব ক্ষেত্রে প্রয়োজন হয় না; common বা compromised password ঠেকানো এবং rate limiting-ও গুরুত্বপূর্ণ।

Django-এর `validate_password()` এই configured validators চালাবে।

## ৩. Change Password serializer তৈরি করো

`accounts/serializers.py`-এর শেষে নিচের class যোগ করো। File-এ আগে থেকেই `serializers`, `get_user_model` বা `validate_password` import করা থাকলে duplicate import করার প্রয়োজন নেই।

```
from django.contrib.auth import get_user_modelfrom django.contrib.auth.password_validation import validate_passwordfrom django.core.exceptions import ValidationError as DjangoValidationErrorfrom django.db import transactionfrom rest_framework import serializersfrom accounts.services.token_service import (    revoke_user_refresh_tokens,)User = get_user_model()class ChangePasswordSerializer(serializers.Serializer):    current_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    new_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    confirm_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    def validate_current_password(self, value):        user = self.context["request"].user        if not user.check_password(value):            raise serializers.ValidationError(                "Current password is incorrect."            )        return value    def validate(self, attrs):        user = self.context["request"].user        if attrs["new_password"] != attrs["confirm_password"]:            raise serializers.ValidationError({                "confirm_password": "Passwords do not match."            })        if attrs["current_password"] == attrs["new_password"]:            raise serializers.ValidationError({                "new_password": (                    "New password must be different from "                    "the current password."                )            })        try:            validate_password(                attrs["new_password"],                user=user,            )        except DjangoValidationError as exc:            raise serializers.ValidationError({                "new_password": list(exc.messages)            })        return attrs    @transaction.atomic    def save(self, **kwargs):        user = self.context["request"].user        new_password = self.validated_data["new_password"]        # Update the password hash, never store plaintext.        user.set_password(new_password)        # Invalidate JWTs issued with the previous version.        user.token_version += 1        user.save(            update_fields=["password", "token_version"]        )        # Revoke every outstanding refresh token for this user.        revoke_user_refresh_tokens(user)        return user
```

### Code কীভাবে কাজ করছে?

1. `check_password()` — database-এ থাকা password hash-এর সঙ্গে বর্তমান password মিলিয়ে দেখে। Plaintext password database-এ রাখা হয় না।
2. `validate_password()` — Django-এর configured password validators চালায় এবং user-এর তথ্যের সঙ্গে password-এর similarity-ও পরীক্ষা করতে পারে।
3. `set_password()` — নতুন password নিরাপদভাবে hash করে user object-এ সেট করে।
4. `token_version += 1` — আগের version-সহ access token পরের authenticated request-এ reject করায়, যদি Lesson 5-এর `VersionedJWTAuthentication` সক্রিয় থাকে।
5. `revoke_user_refresh_tokens()` — user-এর outstanding refresh tokens blacklist করে।

`@transaction.atomic` নিশ্চিত করে যে password update এবং refresh token revocation একই database transaction-এ সম্পন্ন হবে। কোনো database error হলে transaction rollback হতে পারে।

## ৪. Change Password API view তৈরি করো

`accounts/views.py`-এ যোগ করো:

```
from rest_framework import statusfrom rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom .serializers import ChangePasswordSerializerclass ChangePasswordAPIView(APIView):    permission_classes = [IsAuthenticated]    def post(self, request):        serializer = ChangePasswordSerializer(            data=request.data,            context={"request": request},        )        serializer.is_valid(raise_exception=True)        serializer.save()        return Response(            {                "detail": (                    "Password changed successfully. "                    "Please log in again."                )            },            status=status.HTTP_200_OK,        )
```

এখানে `context={"request": request}` গুরুত্বপূর্ণ। Serializer এই request থেকে authenticated user পায়; client body-তে user ID পাঠিয়ে অন্য কারও password পরিবর্তন করতে পারে না।

## ৫. URL যোগ করো

`accounts/urls.py`-এ view import করে route যোগ করো:

```
from .views import ChangePasswordAPIViewurlpatterns = [    # Existing routes...    path(        "change-password/",        ChangePasswordAPIView.as_view(),        name="change-password",    ),]
```

এখন endpoint:

`POST /api/auth/change-password/`

## ৬. Postman দিয়ে test করো

প্রথমে login করে নতুন access token নাও।

POST

Change Password

`http://127.0.0.1:8000/api/auth/change-password/`

Authorization: Bearer Token → login-এর access token

Body → raw → JSON

```
{
  "current_password": "OldStrongPass!123",
  "new_password": "NewStrongPass!456",
  "confirm_password": "NewStrongPass!456"
}
```

সফল হলে:

```
{
  "detail": "Password changed successfully. Please log in again."
}
```

### Error cases পরীক্ষা করো

| Test                       | Expected result    |
| -------------------------- | ------------------ |
| Access token ছাড়া request  | `401 Unauthorized` |
| ভুল current password       | `400 Bad Request`  |
| দুইটি নতুন password আলাদা  | `400 Bad Request`  |
| দুর্বল password            | `400 Bad Request`  |
| একই current ও new password | `400 Bad Request`  |
| সব validation ঠিক          | `200 OK`           |

Django/DRF validation error-এর response-এ field অনুযায়ী error message আসবে। নির্দিষ্ট HTTP response format তোমার exception handler-এর ওপরও নির্ভর করতে পারে।

## ৭. Password change-এর পরে token revocation test

এটি Lesson 6-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

Test A — পুরোনো access token

Password change করার আগের `access_A` দিয়ে `/api/auth/me/` call করো।

Expected: `401 Unauthorized`, যদি `VersionedJWTAuthentication` এবং `token_version` সঠিকভাবে configure করা থাকে।

Test B — পুরোনো refresh token

আগের `refresh_A` দিয়ে `/api/auth/token/refresh/` call করো।

Expected: token blacklist হওয়ার কারণে reject হবে।

Test C — নতুন password

নতুন password দিয়ে login করো।

Expected: নতুন access ও refresh token পাওয়া যাবে।

একটি বিষয় মনে রেখো: token version ব্যবহার করলে password change-এর যে request সফল হলো, সেই request-এর access token-টিও এরপর invalid হয়ে যায়। তাই frontend-কে user-কে পুনরায় login করাতে হবে।

## ৮. Password reset-এর ক্ষেত্রেও একই policy ব্যবহার করো

Lesson 5-এ তৈরি `revoke_user_refresh_tokens(user)` service-টি password reset-এর পরেও ব্যবহার করবে। এতে Change Password ও Forgot Password—দুই ক্ষেত্রেই refresh-token revocation-এর নিয়ম একই থাকবে।

Password reset flow-এ সাধারণত:

1. Reset token যাচাই করবে।
2. নতুন password validate করবে।
3. Password update করবে।
4. `token_version` বাড়াবে।
5. Outstanding refresh token blacklist করবে।
6. Reset token-কে ব্যবহৃত হিসেবে চিহ্নিত করবে।

এসব database পরিবর্তন একই transaction-এ রাখা ভালো। Email বা অন্য external service call দীর্ঘ database transaction-এর মধ্যে রেখো না।

## ৯. Production checklist

Production readiness

0/8

User model-এ token_version field আছে এবং migration চালানো হয়েছে

Custom JWT authentication প্রতিটি protected request-এ version যাচাই করে

Login ও refresh flow-এ token_version claim বজায় থাকে

Password change এবং reset—দুই flow-তেই refresh tokens revoke হয়

Frontend password change-এর পরে login screen-এ পাঠায়

Login ও password-change endpoint-এ rate limiting এবং security logging আছে

Access token, refresh token ও password logs-এ লেখা হয় না

Automated tests-এ invalid password, token revocation ও rollback যাচাই করা হয়েছে

শেষ কথা: এই implementation-এ password change হলে সব refresh token blacklist হবে এবং token version-এর কারণে আগের access token-ও reject হবে। তবে মনে রেখো, এটি তখনই কাজ করবে যখন Lesson 5-এর `token_version` field, token claim এবং custom authentication class সত্যিই project-এ configure করা আছে।

পরবর্তী Lesson 7-এ আমরা Forgot Password + Secure Password Reset API তৈরি করতে পারি—reset token generate, hash করে database-এ রাখা, expiry, one-time use, email delivery এবং abuse prevention-সহ।

----
# Lesson 7: Forgot Password + Secure Password Reset API

এই lesson-এ আমরা Django REST Framework দিয়ে এমন একটি password reset system তৈরি করব, যেখানে user password ভুলে গেলে email-এর মাধ্যমে নতুন password সেট করতে পারবে—আগের password না জেনেও।

আমাদের system-এ থাকবে random reset token, database-এ token hash, expiry, one-time use, email delivery, rate limiting এবং token revocation।

## ১. Password reset flow

1\. Forgot Password

User email submit করে

2\. Reset token generate

Random token তৈরি, hash database-এ save

3\. Email delivery

Frontend-এ reset link পাঠানো

4\. Reset Password

Token + নতুন password submit

5\. Security actions

Token consume, password update, পুরোনো session revoke

আমাদের endpoints হবে:

| Method | Endpoint                     | কাজ                   |
| ------ | ---------------------------- | --------------------- |
| `POST` | `/api/auth/password/forgot/` | Reset email request   |
| `POST` | `/api/auth/password/reset/`  | নতুন password সেট করা |

Forgot Password endpoint-এ email account আছে কি নেই—দুই ক্ষেত্রেই একই generic response দেব। এতে attacker সহজে জানতে পারবে না কোন email নিবন্ধিত আছে।

## ২. Reset token-এর database model

`accounts/models.py`-এ নতুন model যোগ করো। তোমার existing `User` এবং `EmailVerificationToken` model মুছবে না।

```
import uuidfrom django.conf import settingsfrom django.db import modelsfrom django.utils import timezoneclass PasswordResetToken(models.Model):    id = models.UUIDField(        primary_key=True,        default=uuid.uuid4,        editable=False,    )    user = models.ForeignKey(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="password_reset_tokens",    )    token_hash = models.CharField(        max_length=64,        unique=True,    )    expires_at = models.DateTimeField()    used_at = models.DateTimeField(        null=True,        blank=True,    )    created_at = models.DateTimeField(        auto_now_add=True,    )    class Meta:        indexes = [            models.Index(                fields=["user", "expires_at"],                name="pwd_reset_user_exp_idx",            ),        ]    @property    def is_expired(self):        return timezone.now() >= self.expires_at    def __str__(self):        return f"Password reset for user {self.user_id}"
```

### কেন raw token database-এ রাখছি না?

ধরো, email-এ পাঠানো raw token হলো:

```
Kj8...random-secret-token...Pq2
```

Database-এ raw token না রেখে শুধু তার SHA-256 hash রাখব। Email-এর token দিয়ে request এলে তার hash তৈরি করে database-এর hash-এর সঙ্গে মিলিয়ে দেখব।

এতে database-এর token records ফাঁস হলেও attacker সরাসরি সেই hash-কে reset link হিসেবে ব্যবহার করতে পারবে না।

Migration চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
```

## ৩. Token service তৈরি করো

নতুন file তৈরি করো:

`accounts/services/password_reset_service.py`

```
import hashlibimport secretsfrom datetime import timedeltafrom django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetTokenRESET_TOKEN_EXPIRY_MINUTES = 15def hash_reset_token(raw_token: str) -> str:    return hashlib.sha256(        raw_token.encode("utf-8")    ).hexdigest()@transaction.atomicdef create_password_reset_token(user):    now = timezone.now()    # Invalidate older unused reset tokens.    PasswordResetToken.objects.filter(        user=user,        used_at__isnull=True,    ).update(used_at=now)    raw_token = secrets.token_urlsafe(32)    PasswordResetToken.objects.create(        user=user,        token_hash=hash_reset_token(raw_token),        expires_at=now + timedelta(            minutes=RESET_TOKEN_EXPIRY_MINUTES        ),    )    # Return raw token only to send it through email.    return raw_token
```

এখানে:

- `secrets.token_urlsafe(32)` cryptographically secure random token তৈরি করে।
- Token-এর মেয়াদ ১৫ মিনিট।
- নতুন token তৈরি হলে আগের unused reset token-গুলো invalid হয়।
- Raw token শুধু email delivery-এর জন্য service থেকে return হয়; database-এ save হয় না।

## ৪. Password reset email পাঠাও

`accounts/services/email_service.py`-এ আগের email-verification function অক্ষুণ্ণ রেখে নতুন function যোগ করো:

```
from django.conf import settingsfrom django.core.mail import send_maildef send_password_reset_email(user, raw_token):    reset_url = (        f"{settings.FRONTEND_ORIGIN.rstrip('/')}"        f"/reset-password?token={raw_token}"    )    subject = "Reset your password"    message = (        "Hello,\n\n"        "We received a request to reset your password.\n\n"        f"Reset your password using this link:\n{reset_url}\n\n"        "This link expires in 15 minutes and can only be used once.\n"        "If you did not request a password reset, ignore this email."    )    return send_mail(        subject,        message,        settings.DEFAULT_FROM_EMAIL,        [user.email],        fail_silently=False,    )
```

`config/settings.py`-এ development environment-এর জন্য আগে থেকে থাকা `FRONTEND_ORIGIN` এবং `DEFAULT_FROM_EMAIL` ব্যবহার করো। Console email backend থাকলে email terminal-এ দেখা যাবে।

Production-এ HTTPS ব্যবহার করবে। Reset token-সহ URL analytics, application logs বা third-party tracking-এ leak হওয়া আটকাবে; frontend token পড়ার পর address bar থেকে সরিয়ে ফেলবে।

## ৫. Forgot Password serializer

`accounts/serializers.py`-এ যোগ করো:

```
from django.contrib.auth import get_user_modelfrom rest_framework import serializersUser = get_user_model()class ForgotPasswordSerializer(serializers.Serializer):    email = serializers.EmailField()    def validate_email(self, value):        return value.strip().lower()
```

এখানে email format যাচাই হচ্ছে। User আছে কি নেই—সেটি serializer-এর error response দিয়ে প্রকাশ করা হবে না।

## ৬. Forgot Password API view

`accounts/views.py`-এ যোগ করো:

```
import loggingfrom django.contrib.auth import get_user_modelfrom rest_framework import statusfrom rest_framework.permissions import AllowAnyfrom rest_framework.response import Responsefrom rest_framework.throttling import ScopedRateThrottlefrom rest_framework.views import APIViewfrom accounts.serializers import ForgotPasswordSerializerfrom accounts.services.password_reset_service import (    create_password_reset_token,)from accounts.services.email_service import (    send_password_reset_email,)logger = logging.getLogger(__name__)User = get_user_model()class ForgotPasswordAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "forgot_password"    def post(self, request):        serializer = ForgotPasswordSerializer(            data=request.data        )        serializer.is_valid(raise_exception=True)        email = serializer.validated_data["email"]        user = User.objects.filter(            email__iexact=email,            is_active=True,            email_verified=True,        ).first()        if user is not None:            raw_token = create_password_reset_token(user)            try:                send_password_reset_email(                    user,                    raw_token,                )            except Exception:                # Never log the raw reset token.                logger.exception(                    "Password reset email delivery failed."                )        return Response(            {                "detail": (                    "If an eligible account exists for this email, "                    "password reset instructions will be sent."                )            },            status=status.HTTP_200_OK,        )
```

Security note: Generic response account enumeration কমায়, কিন্তু একই response time এবং email sending behavior-ও গুরুত্বপূর্ণ। Production-এ email delivery queue, per-email cooldown এবং IP-based throttling ব্যবহার করো। Django REST Framework-এর built-in throttling abuse কমাতে সাহায্য করে, তবে এটি একা শক্তিশালী DDoS বা brute-force protection নয়।

## ৭. Secure Password Reset service

এখন reset token যাচাই, one-time use, expiry, password update এবং token revocation একসঙ্গে implement করব।

`accounts/services/password_reset_service.py`-এর import list ও শেষে নিচের code যোগ করো। আগের `hash_reset_token()` ও `create_password_reset_token()` function রেখে দেবে।

```
from django.contrib.auth.password_validation import validate_passwordfrom django.core.exceptions import ValidationError as DjangoValidationErrorfrom django.db import transactionfrom accounts.services.token_service import (    revoke_user_refresh_tokens,)class InvalidPasswordResetToken(Exception):    pass@transaction.atomicdef reset_password(raw_token: str, new_password: str):    token_hash = hash_reset_token(raw_token)    record = (        PasswordResetToken.objects        .select_for_update()        .select_related("user")        .filter(token_hash=token_hash)        .first()    )    if (        record is None        or record.used_at is not None        or record.is_expired    ):        raise InvalidPasswordResetToken    user = record.user    if not user.is_active or not user.email_verified:        raise InvalidPasswordResetToken    try:        validate_password(new_password, user=user)    except DjangoValidationError:        raise    user.set_password(new_password)    # Requires the token_version field from Lesson 5.    user.token_version += 1    user.save(        update_fields=["password", "token_version"]    )    revoke_user_refresh_tokens(user)    # Consume this token and invalidate any other outstanding reset links.    now = timezone.now()    record.used_at = now    record.save(update_fields=["used_at"])    PasswordResetToken.objects.filter(        user=user,        used_at__isnull=True,    ).exclude(pk=record.pk).update(used_at=now)    return user
```

এই code-এর `select_for_update()` token record-কে transaction চলাকালে lock করে। ফলে একই token দিয়ে concurrent reset request এলে দ্বিতীয় request-এর token-used status পুনরায় যাচাই হবে।

`validate_password()`-এর validation error-কে view-এ user-friendly response-এ রূপান্তর করব।

## ৮. Reset Password serializer

`accounts/serializers.py`-এ যোগ করো:

```
class ResetPasswordSerializer(serializers.Serializer):    token = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    new_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    confirm_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    def validate(self, attrs):        if attrs["new_password"] != attrs["confirm_password"]:            raise serializers.ValidationError({                "confirm_password": "Passwords do not match."            })        return attrs
```

Serializer এখানে token-এর উপস্থিতি ও password confirmation যাচাই করে। Token সত্যিই valid, expired নয়, এবং ব্যবহার করা হয়নি কি না—এসব যাচাই service-এর transaction-এর ভেতরে হবে।

## ৯. Reset Password API view

`accounts/views.py`-এ যোগ করো:

```
from django.core.exceptions import ValidationError as DjangoValidationErrorfrom accounts.serializers import ResetPasswordSerializerfrom accounts.services.password_reset_service import (    reset_password,    InvalidPasswordResetToken,)class ResetPasswordAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "password_reset"    def post(self, request):        serializer = ResetPasswordSerializer(            data=request.data        )        serializer.is_valid(raise_exception=True)        data = serializer.validated_data        try:            reset_password(                raw_token=data["token"],                new_password=data["new_password"],            )        except InvalidPasswordResetToken:            return Response(                {                    "detail": (                        "This password reset link is invalid "                        "or has expired."                    )                },                status=status.HTTP_400_BAD_REQUEST,            )        except DjangoValidationError as exc:            return Response(                {"new_password": list(exc.messages)},                status=status.HTTP_400_BAD_REQUEST,            )        return Response(            {                "detail": (                    "Password reset successful. "                    "Please log in with your new password."                )            },            status=status.HTTP_200_OK,        )
```

## ১০. URL configuration

`accounts/urls.py`-এ imports ও `urlpatterns`-এ নিচের routes যোগ করো:

```
from .views import (    ForgotPasswordAPIView,    ResetPasswordAPIView,)urlpatterns = [    # Existing authentication routes...    path(        "password/forgot/",        ForgotPasswordAPIView.as_view(),        name="forgot-password",    ),    path(        "password/reset/",        ResetPasswordAPIView.as_view(),        name="reset-password",    ),]
```

## ১১. Rate limiting configure করো

`config/settings.py`-এর existing `REST_FRAMEWORK["DEFAULT_THROTTLE_RATES"]`-এ এই scope-গুলো যোগ করো; আগের rates মুছে ফেলবে না।

```
REST_FRAMEWORK = {    # Keep your existing authentication and permission settings.    "DEFAULT_THROTTLE_RATES": {        # Keep your existing rates...        "forgot_password": "5/hour",        "password_reset": "10/hour",    },}
```

এই উদাহরণের rate-গুলো development starting point। Production-এ shared cache/Redis, IP ও account-based cooldown, এবং email provider-এর sending limits-ও বিবেচনা করবে।

## ১২. Postman testing

### Test A — Forgot Password request

POST

Forgot Password

`http://127.0.0.1:8000/api/auth/password/forgot/`

Body → raw → JSON

```
{
  "email": "student@example.com"
}
```

Expected response: `200 OK`

```
{
  "detail": "If an eligible account exists for this email, password reset instructions will be sent."
}
```

Development-এ console email backend ব্যবহার করলে terminal-এ reset link দেখতে পাবে। Link থেকে raw token copy করো। Database-এ অবশ্য raw token নয়, তার hash সংরক্ষিত থাকবে।

### Test B — Reset Password

POST

Reset Password

`http://127.0.0.1:8000/api/auth/password/reset/`

Body → raw → JSON

```
{
  "token": "<token-from-email>",
  "new_password": "AnotherStrongPass!829",
  "confirm_password": "AnotherStrongPass!829"
}
```

সফল হলে `200 OK` এবং password reset successful message পাবে।

### Test C — One-time use

একই reset token দিয়ে আবার request পাঠাও।

Expected: `400 Bad Request` — token ইতোমধ্যে ব্যবহৃত।

### Test D — Expiry

Database-এ test token-এর `expires_at` অতীতের সময় করে দাও, তারপর request পাঠাও।

Expected: `400 Bad Request` — invalid বা expired reset link।

### Test E — Token revocation

Password reset-এর আগে পুরোনো `access_A` ও `refresh_A` সংগ্রহ করো।

- Reset-এর পরে `refresh_A` দিয়ে `/api/auth/token/refresh/` call করো: reject হওয়া উচিত।
- `access_A` দিয়ে `/api/auth/me/` call করো: `token_version` authentication চালু থাকলে reject হওয়া উচিত।
- নতুন password দিয়ে login করো: সফল হওয়া উচিত।

## ১৩. Production security checklist

Security checklist

0/9

Raw reset token database-এ সংরক্ষণ করা হয় না

Reset token-এর মেয়াদ ১৫ মিনিট এবং one-time use

Forgot Password response registered email প্রকাশ করে না

Email sending failure-এর জন্য retry/queue ব্যবস্থা আছে

Reset endpoint-এ rate limiting ও abuse monitoring আছে

Password reset-এর পর refresh tokens revoke হয়

token_version authentication সক্রিয় থাকলে পুরোনো access tokens reject হয়

Reset link HTTPS-এ পাঠানো হয় এবং logs/analytics-এ token leak হয় না

Automated tests-এ expired, reused, invalid token ও concurrent requests যাচাই করা হয়েছে

Production-এর আগে আরও একটি বিষয়: এই implementation-এ password update, reset-token consumption এবং refresh-token revocation একই database transaction-এ আছে। কিন্তু email একটি external service—তাই email পাঠানো ব্যর্থ হলে retryable background queue বা transactional outbox ব্যবহার করা ভালো। এতে user-এর reset link হারিয়ে যাওয়ার ঝুঁকি কমবে।

পরবর্তী Lesson 8-এ আমরা Account Profile API + Change Email + Email Re-verification তৈরি করতে পারি; সেখানে নিজের profile update, email পরিবর্তনের verification, permission এবং sensitive account changes-এর security policy implement করব।


-----
# Lesson 8: Account Profile API + Change Email + Email Re-verification

এই lesson-এ আমরা আমাদের Django REST Framework Authentication System-এ user profile management এবং secure email change system তৈরি করব।

মূল security rule হবে: একজন user শুধু নিজের profile update করতে পারবে, আর email পরিবর্তন করলে নতুন email verify না হওয়া পর্যন্ত সেটিকে verified email হিসেবে ব্যবহার করা যাবে না।

## ১. আজকের API design

| Method  | Endpoint                                      | কাজ                                     |
| ------- | --------------------------------------------- | --------------------------------------- |
| `GET`   | `/api/auth/profile/`                          | নিজের profile দেখা                      |
| `PATCH` | `/api/auth/profile/`                          | নিজের profile-এর অনুমোদিত তথ্য পরিবর্তন |
| `POST`  | `/api/auth/email/change/`                     | নতুন email-এর জন্য change request       |
| `POST`  | `/api/auth/email/confirm-change/`             | নতুন email verify করা                   |
| `POST`  | `/api/auth/email/resend-change-verification/` | Verification email পুনরায় পাঠানো        |

সব profile ও email-change endpoint authenticated user-এর জন্য হবে। Email verification endpoint-এও token-এর মালিকানা যাচাই করতে হবে।

## ২. Profile model তৈরি করো

আমাদের `User` model-এ email, `email_verified`, `is_active` এবং `token_version` আগে থেকেই আছে। অতিরিক্ত profile information আলাদা model-এ রাখব।

`accounts/models.py`-এ যোগ করো:

```
from django.conf import settingsfrom django.db import modelsclass Profile(models.Model):    user = models.OneToOneField(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="profile",    )    full_name = models.CharField(        max_length=150,        blank=True,    )    phone_number = models.CharField(        max_length=20,        blank=True,    )    bio = models.TextField(        max_length=500,        blank=True,    )    avatar = models.ImageField(        upload_to="profiles/avatars/",        null=True,        blank=True,    )    updated_at = models.DateTimeField(        auto_now=True,    )    def __str__(self):        return f"Profile: {self.user.email}"
```

Avatar upload ব্যবহার করতে চাইলে Pillow install করো:

```
pip install Pillow
```

তারপর migration:

```
python manage.py makemigrations accounts
python manage.py migrate
```

`Profile.user` হলো `OneToOneField`, তাই একজন user-এর একটি profile থাকবে। এখানে user ID client-এর কাছ থেকে নেওয়া হবে না—authenticated request থেকেই user নির্ধারিত হবে।

## ৩. Email change verification model

Email পরিবর্তন একটি sensitive account operation। তাই নতুন email-এ verification link পাঠাব, আর verification সফল হলে তবেই `User.email` update করব।

`accounts/models.py`-এ যোগ করো:

```
import uuidfrom django.conf import settingsfrom django.db import modelsfrom django.utils import timezoneclass EmailChangeRequest(models.Model):    id = models.UUIDField(        primary_key=True,        default=uuid.uuid4,        editable=False,    )    user = models.ForeignKey(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="email_change_requests",    )    new_email = models.EmailField()    token_hash = models.CharField(        max_length=64,        unique=True,    )    expires_at = models.DateTimeField()    used_at = models.DateTimeField(        null=True,        blank=True,    )    created_at = models.DateTimeField(        auto_now_add=True,    )    @property    def is_expired(self):        return timezone.now() >= self.expires_at    def __str__(self):        return f"Email change request for user {self.user_id}"
```

এখন migration চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
```

এই model-এ আমরা `new_email` এবং token hash রাখছি। Verification সফল হওয়ার আগে user-এর মূল email পরিবর্তন হবে না।

## ৪. Profile serializer তৈরি করো

`accounts/serializers.py`-এ যোগ করো:

```
from rest_framework import serializersfrom accounts.models import Profileclass ProfileSerializer(serializers.ModelSerializer):    email = serializers.EmailField(        source="user.email",        read_only=True,    )    email_verified = serializers.BooleanField(        source="user.email_verified",        read_only=True,    )    class Meta:        model = Profile        fields = [            "full_name",            "phone_number",            "bio",            "avatar",            "email",            "email_verified",            "updated_at",        ]        read_only_fields = [            "email",            "email_verified",            "updated_at",        ]
```

### কেন `email` read-only?

Email পরিবর্তনের জন্য আমাদের আলাদা verification workflow আছে। Profile PATCH request-এর মাধ্যমে সরাসরি email পরিবর্তনের অনুমতি দিলে verification bypass করা সম্ভব হতে পারে।

একইভাবে `user`, `is_staff`, `is_superuser`, `is_active` বা `token_version` profile serializer-এর writable field হিসেবে রাখবে না।

## ৫. Profile API view তৈরি করো

`accounts/views.py`-এ যোগ করো:

```
from django.db import transactionfrom rest_framework import statusfrom rest_framework.parsers import (    JSONParser,    FormParser,    MultiPartParser,)from rest_framework.permissions import IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.views import APIViewfrom accounts.models import Profilefrom accounts.serializers import ProfileSerializerclass AccountProfileAPIView(APIView):    permission_classes = [IsAuthenticated]    parser_classes = [        JSONParser,        FormParser,        MultiPartParser,    ]    def get(self, request):        profile, _ = Profile.objects.get_or_create(            user=request.user,        )        serializer = ProfileSerializer(            profile,            context={"request": request},        )        return Response(serializer.data)    @transaction.atomic    def patch(self, request):        profile, _ = Profile.objects.get_or_create(            user=request.user,        )        serializer = ProfileSerializer(            profile,            data=request.data,            partial=True,            context={"request": request},        )        serializer.is_valid(raise_exception=True)        serializer.save()        return Response(            serializer.data,            status=status.HTTP_200_OK,        )
```

`get_or_create()` ব্যবহার করায় registration-এর সময় profile তৈরি না হলেও প্রথম profile request-এ তৈরি হয়ে যাবে। Production-এ চাইলে registration service-এর transaction-এর মধ্যে profile তৈরি করতে পারো, যাতে user ও profile creation একই workflow-এ থাকে।

### URL যোগ করো

`accounts/urls.py`-এ:

```
path(    "profile/",    AccountProfileAPIView.as_view(),    name="account-profile",),
```

এখন:

- `GET /api/auth/profile/`
- `PATCH /api/auth/profile/`

দুইটি endpoint-ই শুধু authenticated user-এর নিজের profile নিয়ে কাজ করবে।

## ৬. Email change token service

নতুন file তৈরি করো:

`accounts/services/email_change_service.py`

```
import hashlibimport secretsfrom datetime import timedeltafrom django.contrib.auth import get_user_modelfrom django.db import transactionfrom django.utils import timezonefrom accounts.models import EmailChangeRequestfrom accounts.services.token_service import (    revoke_user_refresh_tokens,)User = get_user_model()EMAIL_CHANGE_EXPIRY_MINUTES = 30def hash_email_change_token(raw_token: str) -> str:    return hashlib.sha256(        raw_token.encode("utf-8")    ).hexdigest()@transaction.atomicdef create_email_change_request(user, new_email):    new_email = new_email.strip().lower()    # Do not allow an email already assigned to another account.    if User.objects.filter(email__iexact=new_email).exists():        raise ValueError("This email cannot be used.")    now = timezone.now()    # Invalidate older pending requests for this user.    EmailChangeRequest.objects.filter(        user=user,        used_at__isnull=True,    ).update(used_at=now)    raw_token = secrets.token_urlsafe(32)    EmailChangeRequest.objects.create(        user=user,        new_email=new_email,        token_hash=hash_email_change_token(raw_token),        expires_at=now + timedelta(            minutes=EMAIL_CHANGE_EXPIRY_MINUTES        ),    )    return raw_token@transaction.atomicdef confirm_email_change(raw_token: str):    token_hash = hash_email_change_token(raw_token)    request_record = (        EmailChangeRequest.objects        .select_for_update()        .select_related("user")        .filter(token_hash=token_hash)        .first()    )    if (        request_record is None        or request_record.used_at is not None        or request_record.is_expired    ):        raise ValueError("Invalid or expired verification link.")    user = User.objects.select_for_update().get(        pk=request_record.user_id,    )    if User.objects.filter(        email__iexact=request_record.new_email,    ).exclude(pk=user.pk).exists():        raise ValueError("This email cannot be used.")    now = timezone.now()    user.email = request_record.new_email    user.email_verified = True    user.is_active = True    # Revoke sessions because the account identifier changed.    user.token_version += 1    user.save(        update_fields=[            "email",            "email_verified",            "is_active",            "token_version",        ]    )    revoke_user_refresh_tokens(user)    request_record.used_at = now    request_record.save(update_fields=["used_at"])    EmailChangeRequest.objects.filter(        user=user,        used_at__isnull=True,    ).exclude(pk=request_record.pk).update(used_at=now)    return user
```

### এই service-এর security rules

- Token random ও unpredictable।
- Database-এ শুধু token hash থাকে।
- Verification link ৩০ মিনিটের মধ্যে ব্যবহার করতে হবে।
- একই token দ্বিতীয়বার ব্যবহার করা যাবে না।
- নতুন email অন্য account-এর সঙ্গে যুক্ত থাকলে পরিবর্তন হবে না।
- Email পরিবর্তনের পর refresh tokens revoke এবং token version increment হবে।

`ValueError` এখানে service-এর উদাহরণ হিসেবে ব্যবহার করা হয়েছে। Production code-এ `EmailAlreadyInUse` ও `InvalidEmailChangeToken`-এর মতো আলাদা custom exceptions ব্যবহার করা ভালো, যাতে API নির্ভরযোগ্যভাবে error classify করতে পারে।

আরও একটি গুরুত্বপূর্ণ policy: Email change request তৈরির আগে current password পুনরায় যাচাই করানো উচিত। নিচের serializer-এ সেটি যোগ করব।

## ৭. Email change serializers

`accounts/serializers.py`-এ যোগ করো:

```
from django.contrib.auth import get_user_modelfrom rest_framework import serializersUser = get_user_model()class ChangeEmailSerializer(serializers.Serializer):    current_password = serializers.CharField(        write_only=True,        trim_whitespace=False,    )    new_email = serializers.EmailField()    def validate_current_password(self, value):        user = self.context["request"].user        if not user.check_password(value):            raise serializers.ValidationError(                "Current password is incorrect."            )        return value    def validate_new_email(self, value):        email = value.strip().lower()        user = self.context["request"].user        if email == user.email.lower():            raise serializers.ValidationError(                "New email must be different."            )        if User.objects.filter(email__iexact=email).exists():            raise serializers.ValidationError(                "This email cannot be used."            )        return emailclass ConfirmEmailChangeSerializer(serializers.Serializer):    token = serializers.CharField(        write_only=True,        trim_whitespace=False,    )
```

এখানে email validation-এর পাশাপাশি current password যাচাই করা হচ্ছে। তবে serializer validation এবং database write-এর মাঝখানে concurrent request হতে পারে, তাই service-এও email uniqueness যাচাই রাখা হয়েছে। Database-এর unique constraint-ই শেষ প্রতিরক্ষা।

## ৮. Email verification email পাঠানো

`accounts/services/email_service.py`-এ function যোগ করো:

```
from django.conf import settingsfrom django.core.mail import send_maildef send_email_change_verification(user, new_email, raw_token):    verification_url = (        f"{settings.FRONTEND_ORIGIN.rstrip('/')}"        f"/confirm-email-change?token={raw_token}"    )    subject = "Confirm your new email address"    message = (        f"Hello,\n\n"        f"A request was made to change the email for your account "        f"to {new_email}.\n\n"        f"Confirm the change using this link:\n"        f"{verification_url}\n\n"        f"This link expires in 30 minutes.\n"        f"If you did not request this change, do not use the link "        f"and contact support if you suspect account compromise."    )    return send_mail(        subject,        message,        settings.DEFAULT_FROM_EMAIL,        [new_email],        fail_silently=False,    )
```

Email change verification নতুন email-এ পাঠানো হচ্ছে, কারণ সেটির মালিকানা যাচাই করতে হবে। Production-এ email পরিবর্তনের বিষয়ে পুরোনো email address-এও একটি notification পাঠানো ভালো, যাতে অননুমোদিত পরিবর্তন হলে account owner জানতে পারে।

## ৯. Email change API views

`accounts/views.py`-এ যোগ করো:

```
import loggingfrom rest_framework import statusfrom rest_framework.permissions import AllowAny, IsAuthenticatedfrom rest_framework.response import Responsefrom rest_framework.throttling import ScopedRateThrottlefrom rest_framework.views import APIViewfrom accounts.serializers import (    ChangeEmailSerializer,    ConfirmEmailChangeSerializer,)from accounts.services.email_change_service import (    create_email_change_request,    confirm_email_change,)from accounts.services.email_service import (    send_email_change_verification,)logger = logging.getLogger(__name__)class ChangeEmailAPIView(APIView):    permission_classes = [IsAuthenticated]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "change_email"    def post(self, request):        serializer = ChangeEmailSerializer(            data=request.data,            context={"request": request},        )        serializer.is_valid(raise_exception=True)        new_email = serializer.validated_data["new_email"]        try:            raw_token = create_email_change_request(                request.user,                new_email,            )        except ValueError:            return Response(                {"detail": "This email cannot be used."},                status=status.HTTP_400_BAD_REQUEST,            )        try:            send_email_change_verification(                request.user,                new_email,                raw_token,            )        except Exception:            # Do not log the raw token or verification URL.            logger.exception(                "Email-change verification delivery failed."            )            return Response(                {                    "detail": (                        "The verification email could not be sent. "                        "Please try again later."                    )                },                status=status.HTTP_503_SERVICE_UNAVAILABLE,            )        return Response(            {                "detail": (                    "If the email can be used, a verification "                    "link has been sent."                )            },            status=status.HTTP_200_OK,        )class ConfirmEmailChangeAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "confirm_email_change"    def post(self, request):        serializer = ConfirmEmailChangeSerializer(            data=request.data,        )        serializer.is_valid(raise_exception=True)        try:            confirm_email_change(                serializer.validated_data["token"]            )        except ValueError:            return Response(                {                    "detail": (                        "The verification link is invalid, "                        "expired, or cannot be used."                    )                },                status=status.HTTP_400_BAD_REQUEST,            )        return Response(            {                "detail": (                    "Email address verified and changed. "                    "Please log in again."                )            },            status=status.HTTP_200_OK,        )
```

এই confirmation endpoint-টি `AllowAny`, কারণ email link থেকে token দিয়ে confirmation হতে পারে, এমনকি user-এর আগের access token expire হয়ে গেলেও। তাই token-টি একটি secret capability হিসেবে বিবেচনা করতে হবে: URL logging, analytics, third-party referrer leakage এবং browser history-তে এর exposure কমাতে হবে।

Production improvement: Email delivery ব্যর্থ হলে আগের pending request রেখে দেওয়া হয়েছে। Retry endpoint-এ token আবার email করতে চাইলে raw token database-এ রাখা যাবে না; নতুন token তৈরি করে পুরোনো request invalidate করো, অথবা encrypted/outbox design ব্যবহার করো। Token হারিয়ে গেলে hash থেকে raw token পুনরুদ্ধার করা যায় না।

## ১০. URLs ও throttling configure করো

`accounts/urls.py`-এ imports ও `urlpatterns`-এ যোগ করো:

```
from .views import (    ChangeEmailAPIView,    ConfirmEmailChangeAPIView,)urlpatterns = [    # Existing routes...    path(        "email/change/",        ChangeEmailAPIView.as_view(),        name="change-email",    ),    path(        "email/confirm-change/",        ConfirmEmailChangeAPIView.as_view(),        name="confirm-email-change",    ),]
```

`config/settings.py`-এর existing throttle rates-এর সঙ্গে এই entries যোগ করো:

```
REST_FRAMEWORK = {    # Preserve your existing settings and rates.    "DEFAULT_THROTTLE_RATES": {        # Existing scopes...        "change_email": "5/hour",        "confirm_email_change": "10/hour",    },}
```

এখন API routes:

- `POST /api/auth/email/change/`
- `POST /api/auth/email/confirm-change/`

## ১১. Postman দিয়ে পরীক্ষা করো

### Test A — Profile দেখা

`GET /api/auth/profile/`

Authorization: Bearer Token → login-এর access token।

সম্ভাব্য response:

```
{
  "full_name": "",
  "phone_number": "",
  "bio": "",
  "avatar": null,
  "email": "student@example.com",
  "email_verified": true,
  "updated_at": "2026-10-17T10:00:00Z"
}
```

### Test B — Profile update

`PATCH /api/auth/profile/`

```
{
  "full_name": "Student Name",
  "bio": "Learning Django REST Framework"
}
```

Expected: `200 OK` এবং updated profile।

এরপর `email` পরিবর্তন করে PATCH request পাঠিয়ে দেখো—`email` read-only হওয়ায় এটি update হবে না।

### Test C — Email change request

`POST /api/auth/email/change/`

```
{
  "current_password": "YourCurrentStrongPass!123",
  "new_email": "new-address@example.com"
}
```

Expected: `200 OK` এবং verification email পাঠানোর confirmation message। Development-এ terminal-এ email link দেখতে পাবে।

### Test D — Confirm email change

Email থেকে raw token নিয়ে:

`POST /api/auth/email/confirm-change/`

```
{
  "token": "<token-from-email>"
}
```

Expected: `200 OK`।

এরপর নতুন email দিয়ে login করে দেখো। পুরোনো email দিয়ে login করা উচিত নয়।

### Test E — Security checks

| Test                                    | Expected                                      |
| --------------------------------------- | --------------------------------------------- |
| Access token ছাড়া profile GET/PATCH     | `401 Unauthorized`                            |
| ভুল current password দিয়ে email change  | `400 Bad Request`                             |
| অন্য account-এর ব্যবহৃত email           | `400 Bad Request`                             |
| Expired verification token              | `400 Bad Request`                             |
| একই token দ্বিতীয়বার                    | `400 Bad Request`                             |
| Email change-এর পর পুরোনো access token  | `401`, যদি token version checking সক্রিয় থাকে |
| Email change-এর পর পুরোনো refresh token | Blacklisted হওয়ায় reject                      |

## ১২. Production security-এর জন্য আরও চারটি বিষয়

### A. Email change যেন account-কে নিজে থেকে reactivate না করে

আগের `confirm_email_change()` service-এ এই line-টি ছিল:

```
user.is_active = True
```

এটি বাদ দাও। কোনো administrator যদি account deactivate করে থাকেন, email পরিবর্তনের মাধ্যমে account আবার সক্রিয় হয়ে যাওয়া উচিত নয়।

`user.save()`-এর `update_fields` থেকেও `"is_active"` বাদ দাও। Email change-এর সময় শুধু email ও verification state update করবে, account activation policy আলাদা রাখবে।

### B. Email change-এর পরে পুরোনো email-এ notification পাঠাও

পুরোনো email address-এ notification পাঠালে account owner অননুমোদিত email-change request সম্পর্কে জানতে পারবেন। এই notification-এ reset token বা verification token পাঠাবে না।

### C. Email uniqueness database-এ enforce করো

Serializer ও service-এর existence check প্রয়োজনীয়, কিন্তু concurrent request-এর কারণে দুটো request একই সময়ে একই email বেছে নিতে পারে। তাই `User.email`-এর database unique constraint বজায় রাখবে। Database integrity error হলে সেটিকে নিরাপদ API error-এ রূপান্তর করতে হবে।

### D. Email পরিবর্তন ও session revocation-এর সম্পর্ক বুঝে রাখো

Email change সফল হলে আমরা:

- নতুন email verified করি।
- `token_version` বাড়াই।
- সব refresh token blacklist করি।
- আগের access token-কে version mismatch-এর কারণে reject করি।

এটি কাজ করার জন্য Lesson 5-এর `VersionedJWTAuthentication` সক্রিয় থাকা জরুরি। Token version claim ছাড়া পুরোনো JWT-গুলো শুধু blacklist দিয়ে তাৎক্ষণিকভাবে revoke হবে না।

## ১৩. Lesson 8 completion checklist

Lesson 8 progress

0/9

Profile GET ও PATCH শুধু authenticated user-এর নিজের data নিয়ে কাজ করে

Profile serializer দিয়ে email বা privileged account fields পরিবর্তন করা যায় না

Email change-এর আগে current password যাচাই করা হয়

নতুন email-এ expiry-সহ hashed-token verification link পাঠানো হয়

Email verify না হওয়া পর্যন্ত মূল email পরিবর্তিত হয় না

Verification token একবারই ব্যবহার করা যায়

Email change-এর পর পুরোনো refresh ও access token revoke হয়

Admin-deactivated account email change-এর মাধ্যমে reactivate হয় না

Rate limiting, notification ও email delivery failure handling আছে

পরবর্তী Lesson 9: Role-Based Access Control (RBAC) + Custom Permissions + Admin/User Permissions + Object-Level Authorization। সেখানে সাধারণ user, staff ও admin-এর permission আলাদা করব এবং নিশ্চিত করব যে user অন্য user-এর private data পরিবর্তন বা দেখতে না পারে।

---
# Lesson 9: Role-Based Access Control (RBAC) + Custom Permissions + Object-Level Authorization

আজ আমরা Authentication System-কে আরও নিরাপদ করব। শুধু user login করেছে কি না, সেটি যাচাই করলেই যথেষ্ট নয়—user কী করতে পারবে, কোন data দেখতে পারবে এবং কোন resource পরিবর্তন করতে পারবে, সেটিও server-side-এ নির্ধারণ করতে হবে।

আমাদের Django REST Framework project-এ তিনটি access level নিয়ে কাজ করব:

- User: নিজের profile ও অনুমোদিত account information পরিচালনা করবে।
- Staff: নির্দিষ্ট administrative কাজ করতে পারবে।
- Admin: সম্পূর্ণ প্রশাসনিক access পাবে, তবে সেটিও explicit policy ও audit-এর অধীনে থাকবে।

## ১. Authentication বনাম Authorization

Authentication

“তুমি কে?”

উদাহরণ: JWT access token বৈধ কি না যাচাই করা।

Authorization

“তুমি কী করতে পারবে?”

উদাহরণ: একজন user শুধু নিজের profile edit করতে পারবে।

আমাদের আগে তৈরি করা `IsAuthenticated` শুধু login করা আছে কি না, তা নিশ্চিত করে। এটি নিজে থেকে অন্য user-এর data access বন্ধ করে না। সে জন্য queryset filtering, custom permissions এবং object-level authorization একসঙ্গে ব্যবহার করব।

## ২. Role design: Django-তে কোন field ব্যবহার করব?

Django-এর `User` model-এ আগে থেকেই আছে:

- `is_active` — account সক্রিয় কি না।
- `is_staff` — Django admin site-এ প্রবেশাধিকার দেওয়ার জন্য ব্যবহৃত flag।
- `is_superuser` — Django permission system-এ সব permission পাওয়ার বিশেষ flag।
- `groups` ও `user_permissions` — granular permission management-এর জন্য।

শুধু `is_staff=True` হলেই একজন staff user-কে তোমার application-এর প্রতিটি API access দেওয়া উচিত নয়। একইভাবে, custom role থাকলেও `is_superuser`-এর প্রভাব আলাদাভাবে বিবেচনা করতে হবে।

এই lesson-এ আমরা Django-এর built-in flags বজায় রেখে custom role field যোগ করব।

## ৩. User model-এ role যোগ করো

`accounts/models.py`-এর existing `User` model-এ নিচের field যোগ করো। তোমার পুরোনো fields মুছবে না।

```
class User(AbstractUser):    # Keep your existing custom user fields.    class Role(models.TextChoices):        USER = "USER", "User"        STAFF = "STAFF", "Staff"        ADMIN = "ADMIN", "Admin"    role = models.CharField(        max_length=10,        choices=Role.choices,        default=Role.USER,        db_index=True,    )    # Keep the existing fields:    # email, email_verified, token_version, etc.
```

তোমার project-এ `User` model ইতোমধ্যে আছে, তাই শুধু `Role` class এবং `role` field-টি existing class-এর মধ্যে merge করবে; দ্বিতীয় `User` class তৈরি করবে না।

তারপর migration চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
```

### Role policy

| Role    | নিজের profile | User list                | অন্য user-এর private profile | Admin actions |
| ------- | ------------- | ------------------------ | ---------------------------- | ------------- |
| `USER`  | Read/update   | নিষিদ্ধ                  | নিষিদ্ধ                      | নিষিদ্ধ       |
| `STAFF` | Read/update   | নির্ধারিত policy অনুযায়ী | শুধু অনুমোদিত কাজে           | সীমিত         |
| `ADMIN` | Read/update   | অনুমোদিত                 | প্রশাসনিক policy অনুযায়ী     | অনুমোদিত      |

এটি আমাদের application policy। Django admin access-এর জন্য `is_staff` এবং `is_superuser` আলাদা করে কাজ করে। Custom API role field নিজে থেকে Django-এর built-in permissions পরিবর্তন করে না।

গুরুত্বপূর্ণ: সাধারণ user যেন request body-তে `"role": "ADMIN"` পাঠিয়ে নিজের role বাড়াতে না পারে। তাই public serializers-এ `role`, `is_staff` বা `is_superuser` writable field হিসেবে রাখবে না।

## ৪. Custom permission classes তৈরি করো

নতুন file তৈরি করো:

`accounts/permissions.py`

```
from rest_framework.permissions import BasePermission, SAFE_METHODSclass IsAdminRole(BasePermission):    """    Only application admins can access this endpoint.    """    def has_permission(self, request, view):        user = request.user        return bool(            user            and user.is_authenticated            and (                user.is_superuser                or user.role == user.Role.ADMIN            )        )class IsStaffOrAdminRole(BasePermission):    """    Staff and admin users can access this endpoint.    """    def has_permission(self, request, view):        user = request.user        return bool(            user            and user.is_authenticated            and (                user.is_superuser                or user.role in [                    user.Role.STAFF,                    user.Role.ADMIN,                ]            )        )class IsOwnerOrReadOnly(BasePermission):    """    Owners can edit their own objects.    Other users may only use safe methods, if the queryset    allows them to see the object in the first place.    """    def has_object_permission(self, request, view, obj):        if request.method in SAFE_METHODS:            return True        owner_id = getattr(obj, "user_id", None)        if owner_id is None:            owner = getattr(obj, "user", None)            owner_id = getattr(owner, "pk", None)        return owner_id == request.user.pk
```

### এই permissions কীভাবে কাজ করে?

- `IsAdminRole` — admin role বা superuser-এর জন্য।
- `IsStaffOrAdminRole` — staff, admin অথবা superuser-এর জন্য।
- `IsOwnerOrReadOnly` — object-এর owner পরিবর্তন করতে পারবে; অন্য user safe methods ব্যবহার করতে পারবে, যদি view-এর queryset সেই object দেখার অনুমতি দেয়।

শেষের permission-টি একা অন্য user-এর data লুকায় না। Read permission-এ অন্যের object দেখানো বন্ধ করতে queryset filtering-ও লাগবে।

## ৫. Admin-only user management serializer

Admin API-তে user-এর সীমিত fields দেখাব। Password hash বা sensitive authentication fields কখনো response-এ পাঠাব না।

`accounts/serializers.py`-এ যোগ করো:

```
from django.contrib.auth import get_user_modelfrom rest_framework import serializersUser = get_user_model()class AdminUserSerializer(serializers.ModelSerializer):    class Meta:        model = User        fields = [            "id",            "email",            "email_verified",            "is_active",            "is_staff",            "role",        ]        read_only_fields = fieldsclass AdminRoleUpdateSerializer(serializers.ModelSerializer):    class Meta:        model = User        fields = ["role"]    def validate_role(self, value):        allowed_roles = {            User.Role.USER,            User.Role.STAFF,            User.Role.ADMIN,        }        if value not in allowed_roles:            raise serializers.ValidationError(                "Invalid role."            )        return value
```

এখানে `AdminUserSerializer` সম্পূর্ণ read-only। Role পরিবর্তনের জন্য আলাদা serializer ব্যবহার করছি, যাতে সেই operation-টি শুধু admin-protected endpoint দিয়ে করা যায়।

## ৬. Staff/Admin-only user list API

`accounts/views.py`-এ যোগ করো:

```
from rest_framework.generics import ListAPIViewfrom rest_framework.permissions import IsAuthenticatedfrom accounts.models import Userfrom accounts.permissions import IsStaffOrAdminRolefrom accounts.serializers import AdminUserSerializerclass AdminUserListAPIView(ListAPIView):    permission_classes = [        IsAuthenticated,        IsStaffOrAdminRole,    ]    serializer_class = AdminUserSerializer    def get_queryset(self):        # Only staff/admin reach this method through the permission.        return User.objects.order_by("id")
```

এটি শুধু staff ও admin-কে user list দেখায়। কিন্তু আমাদের policy অনুযায়ী staff-কে সব user-এর email ও account security fields দেখানোর অনুমতি দেওয়া নাও হতে পারে।

তাই production-এ আরও ভালো design হলো staff ও admin-এর জন্য আলাদা serializer এবং queryset রাখা। উদাহরণস্বরূপ, staff-কে শুধু প্রয়োজনীয় directory fields দেখানো হবে, আর admin-কে account management-এর প্রয়োজনীয় fields দেওয়া হবে।

এই lesson-এ endpoint-টিকে administrative API হিসেবে ধরছি। যদি তোমার staff-এর access সীমিত রাখতে হয়, তবে `AdminUserListAPIView`-এর permission-কে `IsAdminRole` করো, অথবা আলাদা staff serializer তৈরি করো।

## ৭. Admin-only role update API

এখন একজন admin অন্য user-এর role পরিবর্তন করতে পারবে। সাধারণ user বা staff এই endpoint ব্যবহার করতে পারবে না।

`accounts/views.py`-এ যোগ করো:

```
from django.shortcuts import get_object_or_404from rest_framework.views import APIViewfrom rest_framework.response import Responsefrom rest_framework import statusfrom rest_framework.permissions import IsAuthenticatedfrom accounts.models import Userfrom accounts.permissions import IsAdminRolefrom accounts.serializers import AdminRoleUpdateSerializerclass AdminUserRoleUpdateAPIView(APIView):    permission_classes = [        IsAuthenticated,        IsAdminRole,    ]    def patch(self, request, user_id):        target_user = get_object_or_404(            User,            pk=user_id,        )        serializer = AdminRoleUpdateSerializer(            target_user,            data=request.data,            partial=True,        )        serializer.is_valid(raise_exception=True)        serializer.save()        return Response(            {                "id": target_user.pk,                "role": target_user.role,            },            status=status.HTTP_200_OK,        )
```

এখানে request user-এর role নয়, URL-এর `user_id` অনুযায়ী target user পাওয়া হচ্ছে। কিন্তু view-এ `IsAdminRole` থাকার কারণে শুধু authorized admin এই operation করতে পারবে।

Production warning: Admin role update-এর জন্য audit log রাখা, নিজের role কমিয়ে ফেলার মতো ভুল operation প্রতিরোধ করা এবং sensitive role change-এর আগে re-authentication বা MFA বিবেচনা করা উচিত।

## ৮. URLs যোগ করো

`accounts/urls.py`-এ যোগ করো:

```
from .views import (    AdminUserListAPIView,    AdminUserRoleUpdateAPIView,)urlpatterns = [    # Existing routes...    path(        "admin/users/",        AdminUserListAPIView.as_view(),        name="admin-user-list",    ),    path(        "admin/users/<int:user_id>/role/",        AdminUserRoleUpdateAPIView.as_view(),        name="admin-user-role-update",    ),]
```

Endpoints:

- `GET /api/auth/admin/users/`
- `PATCH /api/auth/admin/users/12/role/`

`12` হলো উদাহরণস্বরূপ user ID; বাস্তবে database-এ থাকা user ID ব্যবহার করবে।

## ৯. Object-Level Authorization: অন্য user-এর profile রক্ষা করা

এখন ধরো API আছে:

`GET /api/auth/profiles/25/`

একজন user যদি URL-এ অন্য user-এর ID বসিয়ে দেয়, তাহলে server-কে নিশ্চিত করতে হবে যে সেই object দেখার অনুমতি তার নেই। শুধু frontend-এ edit button লুকিয়ে রাখা security নয়।

### ৯.১ — Owner/Admin permission যোগ করো

`accounts/permissions.py`-এ যোগ করো:

```
class IsOwnerOrAdmin(BasePermission):    """    Only the owner or an application admin can access an object.    """    def has_object_permission(self, request, view, obj):        user = request.user        if (            user.is_superuser            or user.role == user.Role.ADMIN        ):            return True        owner_id = getattr(obj, "user_id", None)        if owner_id is None:            owner = getattr(obj, "user", None)            owner_id = getattr(owner, "pk", None)        return owner_id == user.pk
```

এই permission-টি object-এর owner এবং admin role-কে access দেয়। Staff-কে স্বয়ংক্রিয়ভাবে সব profile access দেওয়া হচ্ছে না।

### ৯.২ — Profile detail view তৈরি করো

`accounts/views.py`-এ যোগ করো:

```
from rest_framework.generics import RetrieveUpdateAPIViewfrom accounts.models import Profilefrom accounts.permissions import IsOwnerOrAdminfrom accounts.serializers import ProfileSerializerclass ProfileDetailAPIView(RetrieveUpdateAPIView):    serializer_class = ProfileSerializer    permission_classes = [        IsAuthenticated,        IsOwnerOrAdmin,    ]    def get_queryset(self):        user = self.request.user        if (            user.is_superuser            or user.role == user.Role.ADMIN        ):            return Profile.objects.select_related("user")        # Normal users can only resolve their own profile.        return Profile.objects.filter(            user=user,        ).select_related("user")
```

এই view-তে দুটি security layer আছে:

1. Queryset filtering: সাধারণ user-এর queryset-এ অন্য user-এর profile থাকে না।
2. Object permission: object পাওয়া গেলেও তার owner বা admin authorization যাচাই করা হয়।

সাধারণ user অন্য user-এর ID দিয়ে request করলে সাধারণত `404 Not Found` পাবে, কারণ object তার queryset-এ নেই। এটি private object-এর অস্তিত্ব প্রকাশ কমাতে সাহায্য করে।

Admin অন্য user-এর profile access করতে পারবে। তবে `ProfileSerializer`-এর field restrictions বজায় থাকবে—admin endpoint ব্যবহার করলেও `email` বা `email_verified` সরাসরি edit করা যাবে না।

URL যোগ করো:

```
path(    "profiles/<int:pk>/",    ProfileDetailAPIView.as_view(),    name="profile-detail",),
```

> বাস্তব project-এর জন্য: নিজের profile-এর ক্ষেত্রে আগের `/profile/` endpoint-ই সবচেয়ে সহজ এবং নিরাপদ। `/profiles/<pk>/` endpoint মূলত object-level authorization বোঝানোর জন্য; প্রয়োজন না থাকলে public API-তে এমন ID-based endpoint যোগ না করলেও চলবে।

## ১০. Role পরিবর্তন ও object-level access test

Postman দিয়ে নিচের tests চালাও। তিনটি আলাদা account তৈরি করে পরীক্ষা করো: `USER`, `STAFF` এবং `ADMIN`।

| Request                                | USER  | STAFF   | ADMIN |
| -------------------------------------- | ----- | ------- | ----- |
| `GET /api/auth/profile/`               | `200` | `200`   | `200` |
| `GET /api/auth/admin/users/`           | `403` | `200`\* | `200` |
| `PATCH /api/auth/admin/users/12/role/` | `403` | `403`   | `200` |
| অন্য user-এর `/profiles/25/`           | `404` | `404`   | `200` |

\*এই উদাহরণে staff list endpoint-এ প্রবেশ করতে পারে। যদি staff-এর user list access প্রয়োজন না হয়, permission-এ শুধু `IsAdminRole` ব্যবহার করো।

### Test A — User নিজে role পরিবর্তন করতে পারে না

সাধারণ user-এর token দিয়ে profile update request পাঠাও:

```
PATCH /api/auth/profile/
Authorization: Bearer <user-access-token>
Content-Type: application/json
```

```
{
  "full_name": "Updated Name",
  "role": "ADMIN",
  "is_staff": true
}
```

Expected: `full_name` update হতে পারে, কিন্তু `role` ও `is_staff` পরিবর্তন হবে না। কারণ `ProfileSerializer`-এ এই fields নেই।

### Test B — Staff admin action করতে পারে না

Staff token দিয়ে পাঠাও:

```
PATCH /api/auth/admin/users/12/role/
Authorization: Bearer <staff-access-token>
Content-Type: application/json
```

```
{
  "role": "ADMIN"
}
```

Expected: `403 Forbidden`।

### Test C — Admin role পরিবর্তন করতে পারে

Admin token দিয়ে একই request পাঠাও।

Expected: `200 OK` এবং response-এ target user-এর updated role থাকবে।

### Test D — ID পরিবর্তন করে অন্য user-এর profile access

User A-এর token দিয়ে User B-এর profile ID ব্যবহার করো:

```
GET /api/auth/profiles/25/
Authorization: Bearer <user-a-access-token>
```

Expected: `404 Not Found`, যদি ID 25 User A-এর profile না হয় এবং User A admin না হয়।

## ১১. Production-এ role ও permissions কীভাবে manage করবে?

### Django Admin এবং application role আলাদা রাখো

`role="ADMIN"` এবং `is_staff=True` একই জিনিস নয়। Django admin site-এ ঢোকার জন্য সাধারণত `is_staff=True` প্রয়োজন, আর Django-এর model permissions-ও প্রযোজ্য হয়। তোমার application API-তে `role` দিয়ে access control করা হচ্ছে।

যদি business policy অনুযায়ী application admin-দের Django admin site-এও access দিতে চাও, তাহলে trusted management workflow-এ দুটো flag-ই নিয়ন্ত্রিতভাবে update করবে। Public registration বা profile update API থেকে কখনোই তা করবে না।

### Custom role-এর বদলে Django Groups-ও ব্যবহার করা যায়

Application ছোট হলে `role` field সহজ ও কার্যকর। কিন্তু application বড় হলে `Groups` এবং granular permissions ব্যবহার করলে যেমন `accounts.view_user`, `accounts.change_user`, `orders.refund_order`—প্রতিটি operation-এর access আলাদাভাবে নিয়ন্ত্রণ করা যায়।

আরও গুরুত্বপূর্ণ: শুধু permission class-এ check করলেই সব শেষ নয়। List endpoints-এর queryset filter করতে হবে, update endpoints-এ writable fields সীমিত করতে হবে এবং sensitive actions-এর audit trail রাখতে হবে।

## ১২. Lesson 9 completion checklist

RBAC progress

0/9

User model-এ role field এবং migration সম্পন্ন

User, staff, admin-এর permission policy নির্ধারণ

Custom permission classes তৈরি

Public serializer থেকে role ও privileged fields বাদ

Admin-only role update endpoint তৈরি

Object-level permission এবং queryset filtering একসঙ্গে ব্যবহার

অন্য user-এর private profile access test করা

Role escalation ও unauthorized API access test করা

Production-এর জন্য audit logging ও staff data restrictions নির্ধারণ

Lesson 9-এর মূল শিক্ষা: Authentication বলে user কে, RBAC বলে কোন কাজ করতে পারবে, আর object-level authorization নিশ্চিত করে সেই নির্দিষ্ট resource-এ তার access আছে কি না। নিরাপদ DRF application-এ এই তিনটি layer একসঙ্গে ব্যবহার করতে হবে।

পরবর্তী Lesson 10-এ আমরা Authentication System-এর Automated Testing + Security Hardening করতে পারি—Django `APITestCase`/`APIClient`, permission tests, token revocation tests, password reset tests, throttling, এবং production-ready test coverage-সহ।

---
# Lesson 10: Django REST Framework Authentication System — Automated Testing + Security Hardening

এই Lesson-এ আমরা আগের ৯টি Lesson-এ তৈরি Authentication System-কে automated test দিয়ে যাচাই করব। শুধু API `200 OK` দিচ্ছে কি না, সেটি দেখব না—বরং unauthorized access, অন্য user-এর profile পরিবর্তন, JWT revocation, password reset token reuse, role escalation এবং request throttling-ও পরীক্ষা করব।

Lesson শেষে আমাদের লক্ষ্য হবে:

- `APITestCase` ও `APIClient` ব্যবহার করে API test লেখা।
- Registration, login, profile ও RBAC permission tests তৈরি করা।
- Password change-এর পরে পুরোনো access/refresh token প্রত্যাখ্যাত হচ্ছে কি না যাচাই করা।
- Password reset token একবারই ব্যবহার করা যাচ্ছে কি না পরীক্ষা করা।
- Rate limiting ও security configuration পরীক্ষা করা।
- Production deployment-এর আগে একটি reusable test suite চালানো।

## 1. Testing architecture

আগের project structure-এর সঙ্গে মিল রেখে `accounts/tests/` folder তৈরি করব।

```
complete_auth_project/
├── manage.py
├── config/
│   └── settings.py
└── accounts/
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── permissions.py
    ├── authentication.py
    ├── services/
    │   └── password_reset_service.py
    └── tests/
        ├── __init__.py
        ├── helpers.py
        ├── test_authentication.py
        ├── test_permissions.py
        ├── test_password_reset.py
        └── test_security.py
```

Django-তে automated test চালালে সাধারণত আলাদা test database তৈরি হয়। তাই test data আপনার development database-এর data-এর সঙ্গে মিশে যায় না।

## 2. `APITestCase` ও `APIClient` কী?

| Tool                   | কাজ                                                                     |
| ---------------------- | ----------------------------------------------------------------------- |
| `APITestCase`          | Django REST Framework API test লেখার class                              |
| `APIClient`            | API endpoint-এ GET, POST, PATCH, DELETE request পাঠায়                   |
| `force_authenticate()` | নির্দিষ্ট user হিসেবে authenticate করে permission test করতে সাহায্য করে |
| `assertEqual()`        | প্রত্যাশিত ও বাস্তব ফলাফল তুলনা করে                                     |
| `override_settings()`  | একটি test-এর জন্য সাময়িকভাবে setting পরিবর্তন করে                       |

উদাহরণ: কোনো user login ছাড়া private endpoint-এ request করলে `401 Unauthorized` বা authentication configuration অনুযায়ী অন্য উপযুক্ত denial status পাওয়া উচিত।

## 3. প্রথমে test environment প্রস্তুত করি

Project root-এ যান:

```
cd complete_auth_project
```

Django ও DRF-এর test tools আগে থেকেই আমাদের installed packages-এর অংশ। এখন test folder তৈরি করুন:

```
mkdir -p accounts/tests
touch accounts/tests/__init__.py
touch accounts/tests/helpers.py
touch accounts/tests/test_authentication.py
touch accounts/tests/test_permissions.py
touch accounts/tests/test_password_reset.py
touch accounts/tests/test_security.py
```

প্রথমে existing migrations ঠিক আছে কি না যাচাই করুন:

```
python manage.py check
python manage.py makemigrations --check
python manage.py migrate
```

`makemigrations --check` নতুন migration প্রয়োজন হলে তা জানাবে; migration প্রয়োজন হলে আগে সেটি তৈরি ও review করুন।

গুরুত্বপূর্ণ: test-এ database-এ আগে থেকে থাকা user ব্যবহার করব না। প্রতিটি test নিজস্ব test data তৈরি করবে, যাতে test পুনরায় চালালেও ফলাফল নির্ভরযোগ্য থাকে।

## 4. Reusable test helper তৈরি

ফাইল: `accounts/tests/helpers.py`

একই ধরনের user ও authentication setup বারবার না লিখে reusable helper তৈরি করব।

```
from rest_framework.test import APIClientfrom accounts.models import Userdef create_user(    email="user@example.com",    password="StrongTestPass!2026",    role=User.Role.USER,    is_active=True,    email_verified=True,):    return User.objects.create_user(        email=email,        password=password,        role=role,        is_active=is_active,        email_verified=email_verified,    )def authenticated_client(user):    client = APIClient()    client.force_authenticate(user=user)    return client
```

এখানে `force_authenticate()` কেবল test-এ ব্যবহারের সুবিধা। এটি login API বা JWT token validation পরীক্ষা করে না; সেই কাজের জন্য আমরা আসল access token-ও ব্যবহার করব।

## 5. Authentication ও login tests

ফাইল: `accounts/tests/test_authentication.py`

প্রথমে যাচাই করব:

1. Login ছাড়া private API access করা যায় না।
2. সঠিক credentials দিয়ে login করলে access ও refresh token পাওয়া যায়।
3. Email verify না করা user login করতে পারে না।
4. ভুল password দিলে login ব্যর্থ হয়।
5. বৈধ JWT দিয়ে protected endpoint access করা যায়।

```
from django.urls import reversefrom rest_framework import statusfrom rest_framework.test import APITestCasefrom accounts.models import Userfrom accounts.tests.helpers import create_userclass AuthenticationTests(APITestCase):    def setUp(self):        self.user = create_user()        # URL name আপনার accounts/urls.py অনুযায়ী রাখুন।        self.login_url = "/api/auth/login/"        self.me_url = "/api/auth/me/"    def test_private_endpoint_requires_authentication(self):        response = self.client.get(self.me_url)        self.assertIn(            response.status_code,            [                status.HTTP_401_UNAUTHORIZED,                status.HTTP_403_FORBIDDEN,            ],        )    def test_login_returns_access_and_refresh_tokens(self):        response = self.client.post(            self.login_url,            {                "email": self.user.email,                "password": "StrongTestPass!2026",            },            format="json",        )        self.assertEqual(response.status_code, status.HTTP_200_OK)        self.assertIn("access", response.data)        self.assertIn("refresh", response.data)    def test_wrong_password_is_rejected(self):        response = self.client.post(            self.login_url,            {                "email": self.user.email,                "password": "WrongPassword!123",            },            format="json",        )        self.assertEqual(            response.status_code,            status.HTTP_401_UNAUTHORIZED,        )    def test_unverified_user_cannot_login(self):        unverified_user = create_user(            email="unverified@example.com",            email_verified=False,            is_active=False,        )        response = self.client.post(            self.login_url,            {                "email": unverified_user.email,                "password": "StrongTestPass!2026",            },            format="json",        )        self.assertEqual(            response.status_code,            status.HTTP_401_UNAUTHORIZED,        )    def test_access_token_can_access_me_endpoint(self):        login_response = self.client.post(            self.login_url,            {                "email": self.user.email,                "password": "StrongTestPass!2026",            },            format="json",        )        self.assertEqual(login_response.status_code, status.HTTP_200_OK)        access_token = login_response.data["access"]        self.client.credentials(            HTTP_AUTHORIZATION=f"Bearer {access_token}"        )        response = self.client.get(self.me_url)        self.assertEqual(response.status_code, status.HTTP_200_OK)        self.assertEqual(response.data["email"], self.user.email)
```

### URL name বনাম সরাসরি path

উপরের উদাহরণে endpoint path সরাসরি দেওয়া হয়েছে, যাতে আগের project-এর URL structure-এর সঙ্গে মেলে। আপনার `accounts/urls.py`-তে login path আলাদা হলে সেটি ব্যবহার করুন। `reverse("login")` ব্যবহার করতে চাইলে আগে URL-এর সঠিক `name` নিশ্চিত করুন।

Expected result: পাঁচটি test-ই pass করবে, যদি আগের login, email verification এবং versioned JWT implementation ঠিকভাবে কাজ করে।

## 6. RBAC ও object-level permission tests

এখন নিশ্চিত করব সাধারণ user admin action করতে পারে না এবং একজন user অন্য user-এর profile পড়তে বা পরিবর্তন করতে পারে না।

ফাইল: `accounts/tests/test_permissions.py`

```
from rest_framework import statusfrom rest_framework.test import APITestCasefrom accounts.models import User, Profilefrom accounts.tests.helpers import create_userclass PermissionTests(APITestCase):    def setUp(self):        self.user_a = create_user(            email="a@example.com",            role=User.Role.USER,        )        self.user_b = create_user(            email="b@example.com",            role=User.Role.USER,        )        self.admin = create_user(            email="admin@example.com",            role=User.Role.ADMIN,        )        self.profile_a, _ = Profile.objects.get_or_create(            user=self.user_a        )        self.profile_b, _ = Profile.objects.get_or_create(            user=self.user_b        )        self.admin_users_url = "/api/auth/admin/users/"        self.profile_detail_url = (            f"/api/auth/profiles/{self.profile_b.pk}/"        )    def test_regular_user_cannot_list_users(self):        self.client.force_authenticate(user=self.user_a)        response = self.client.get(self.admin_users_url)        self.assertEqual(            response.status_code,            status.HTTP_403_FORBIDDEN,        )    def test_admin_can_list_users(self):        self.client.force_authenticate(user=self.admin)        response = self.client.get(self.admin_users_url)        self.assertEqual(response.status_code, status.HTTP_200_OK)    def test_user_cannot_access_another_users_profile(self):        self.client.force_authenticate(user=self.user_a)        response = self.client.get(self.profile_detail_url)        # Lesson 9-এর queryset filtering অনুযায়ী প্রত্যাশিত ফল।        self.assertEqual(response.status_code, status.HTTP_404_NOT_FOUND)    def test_user_cannot_modify_another_users_profile(self):        self.client.force_authenticate(user=self.user_a)        response = self.client.patch(            self.profile_detail_url,            {"full_name": "Unauthorized Change"},            format="json",        )        self.assertIn(            response.status_code,            [                status.HTTP_403_FORBIDDEN,                status.HTTP_404_NOT_FOUND,            ],        )        self.profile_b.refresh_from_db()        self.assertNotEqual(            self.profile_b.full_name,            "Unauthorized Change",        )    def test_admin_can_access_another_users_profile(self):        self.client.force_authenticate(user=self.admin)        response = self.client.get(self.profile_detail_url)        self.assertEqual(response.status_code, status.HTTP_200_OK)
```

### কেন 404 এবং 403—দুই রকম ফল দেখা যেতে পারে?

- 404 Not Found: user-এর queryset থেকেই অন্য user-এর profile বাদ দেওয়া হয়েছে।
- 403 Forbidden: object পাওয়া গেছে, কিন্তু permission class access নিষিদ্ধ করেছে।

দুটিই সঠিক হতে পারে। এই project-এ অন্য user-এর profile-এর জন্য queryset filtering থাকায় `404` প্রত্যাশা করছি।

> Production note: Lesson 9-এর উদাহরণে `STAFF` role user list দেখতে পারে। সেখানে email-সহ account data প্রকাশের আগে staff-এর প্রয়োজনীয় access সীমিত করুন। সাধারণ user-এর public serializer-এ `role`, `is_staff`, `is_superuser` বা `token_version` প্রকাশ করবেন না।

## 7. Password reset tests

Password reset-এর ক্ষেত্রে সবচেয়ে গুরুত্বপূর্ণ security rules:

- ভুল token গ্রহণ করা যাবে না।
- Expired token গ্রহণ করা যাবে না।
- একই token দ্বিতীয়বার ব্যবহার করা যাবে না।
- Password reset-এর পরে পুরোনো refresh token কাজ করা যাবে না।
- Password reset request-এ email account-এ নেই কি না, তা response দিয়ে প্রকাশ করা যাবে না।

### 7.1 Password reset service-এর unit tests

আমাদের আগের service-এর নাম `reset_password()` এবং token database-এ SHA-256 hash হিসেবে সংরক্ষিত হয়। তাই test-এ raw token-এর বদলে hash database-এ রাখব।

ফাইল: `accounts/tests/test_password_reset.py`

```
import hashlibfrom datetime import timedeltafrom django.core.exceptions import ValidationErrorfrom django.utils import timezonefrom rest_framework.test import APITestCasefrom accounts.models import PasswordResetTokenfrom accounts.tests.helpers import create_userfrom accounts.services.password_reset_service import reset_passwordclass PasswordResetServiceTests(APITestCase):    def setUp(self):        self.user = create_user(            email="reset@example.com",            password="OldStrongPass!2026",        )        self.raw_token = "test-reset-token-123"        self.token_hash = hashlib.sha256(            self.raw_token.encode("utf-8")        ).hexdigest()    def create_reset_token(self, expires_at=None):        return PasswordResetToken.objects.create(            user=self.user,            token_hash=self.token_hash,            expires_at=expires_at or (                timezone.now() + timedelta(minutes=15)            ),        )    def test_valid_token_resets_password(self):        self.create_reset_token()        reset_password(            raw_token=self.raw_token,            new_password="NewStrongPass!2026",        )        self.user.refresh_from_db()        self.assertTrue(            self.user.check_password("NewStrongPass!2026")        )        self.assertFalse(            self.user.check_password("OldStrongPass!2026")        )    def test_expired_token_is_rejected(self):        self.create_reset_token(            expires_at=timezone.now() - timedelta(minutes=1)        )        with self.assertRaises(ValidationError):            reset_password(                raw_token=self.raw_token,                new_password="NewStrongPass!2026",            )    def test_invalid_token_is_rejected(self):        with self.assertRaises(ValidationError):            reset_password(                raw_token="invalid-token",                new_password="NewStrongPass!2026",            )    def test_used_token_cannot_be_reused(self):        self.create_reset_token()        reset_password(            raw_token=self.raw_token,            new_password="NewStrongPass!2026",        )        with self.assertRaises(ValidationError):            reset_password(                raw_token=self.raw_token,                new_password="AnotherStrongPass!2026",            )
```

গুরুত্বপূর্ণ compatibility check: এই code আগের service-এর interface ধরে লেখা। আপনার `reset_password()` function-এ argument-এর নাম আলাদা হলে সেটি মিলিয়ে নিন। Service যদি invalid token-এর জন্য `InvalidPasswordResetToken` exception তোলে, তাহলে `assertRaises(ValidationError)`-এর জায়গায় সেই exception ব্যবহার করুন। Password validation-এর জন্য `DjangoValidationError` এবং invalid token-এর জন্য custom exception আলাদা হলে উভয়টিই test করতে হবে।

### 7.2 Password reset API-তে generic response test

Unknown email এবং existing email—দুই ক্ষেত্রেই response একই হওয়া উচিত। এতে attacker সহজে জানতে পারে না কোন email registered আছে।

একই test file-এ যোগ করুন:

```
from django.test import override_settingsclass PasswordResetAPITests(APITestCase):    def setUp(self):        self.forgot_url = "/api/auth/password/forgot/"    @override_settings(        EMAIL_BACKEND="django.core.mail.backends.locmem.EmailBackend"    )    def test_forgot_password_response_does_not_reveal_account(self):        create_user(email="known@example.com")        known_response = self.client.post(            self.forgot_url,            {"email": "known@example.com"},            format="json",        )        unknown_response = self.client.post(            self.forgot_url,            {"email": "unknown@example.com"},            format="json",        )        self.assertEqual(            known_response.status_code,            unknown_response.status_code,        )        self.assertEqual(            known_response.data,            unknown_response.data,        )
```

এখানে response একই থাকলেও বাস্তবে email sending-এর সময়ের পার্থক্য থেকে account-এর অস্তিত্ব অনুমান করার ঝুঁকি থাকতে পারে। Production system-এ asynchronous email queue ব্যবহার করা ভালো।

## 8. Password change ও JWT revocation tests

আমাদের authentication system-এ `token_version` claim ব্যবহার করা হয়। Password পরিবর্তনের পরে user-এর `token_version` বাড়ে। পুরোনো access token-এ আগের version থাকায় সেটি প্রত্যাখ্যাত হওয়ার কথা।

ফাইল: `accounts/tests/test_security.py`

```
from rest_framework import statusfrom rest_framework.test import APITestCasefrom accounts.tests.helpers import create_userclass TokenRevocationTests(APITestCase):    def setUp(self):        self.user = create_user()        self.login_url = "/api/auth/login/"        self.change_password_url = "/api/auth/change-password/"        self.me_url = "/api/auth/me/"    def test_old_access_token_is_rejected_after_password_change(self):        login_response = self.client.post(            self.login_url,            {                "email": self.user.email,                "password": "StrongTestPass!2026",            },            format="json",        )        self.assertEqual(login_response.status_code, status.HTTP_200_OK)        old_access = login_response.data["access"]        self.client.credentials(            HTTP_AUTHORIZATION=f"Bearer {old_access}"        )        change_response = self.client.post(            self.change_password_url,            {                "current_password": "StrongTestPass!2026",                "new_password": "BrandNewStrongPass!2026",                "confirm_password": "BrandNewStrongPass!2026",            },            format="json",        )        self.assertEqual(            change_response.status_code,            status.HTTP_200_OK,        )        self.client.credentials(            HTTP_AUTHORIZATION=f"Bearer {old_access}"        )        me_response = self.client.get(self.me_url)        self.assertEqual(            me_response.status_code,            status.HTTP_401_UNAUTHORIZED,        )
```

এই test-এর password-change payload ও successful status আপনার Lesson 6-এর serializer/view-এর সঙ্গে মিলিয়ে নেবেন। আপনার endpoint যদি `new_password2` নেয়, তাহলে `confirm_password`-এর জায়গায় সেটি ব্যবহার করুন।

### Refresh token revocation-ও পরীক্ষা করুন

Password change-এর পরে আগের refresh token দিয়ে নতুন access token তৈরি করা যাবে না। এই test-এ refresh endpoint ব্যবহার করছি:

```
def test_old_refresh_token_is_rejected_after_password_change(self):    login_response = self.client.post(        "/api/auth/login/",        {            "email": self.user.email,            "password": "StrongTestPass!2026",        },        format="json",    )    self.assertEqual(login_response.status_code, 200)    old_refresh = login_response.data["refresh"]    self.client.credentials(        HTTP_AUTHORIZATION=f"Bearer {login_response.data['access']}"    )    change_response = self.client.post(        "/api/auth/change-password/",        {            "current_password": "StrongTestPass!2026",            "new_password": "BrandNewStrongPass!2026",            "confirm_password": "BrandNewStrongPass!2026",        },        format="json",    )    self.assertEqual(change_response.status_code, 200)    refresh_response = self.client.post(        "/api/auth/token/refresh/",        {"refresh": old_refresh},        format="json",    )    self.assertEqual(        refresh_response.status_code,        status.HTTP_401_UNAUTHORIZED,    )
```

এই method-টি `TokenRevocationTests` class-এর মধ্যে রাখুন। Refresh-token rotation, blacklist app ও `revoke_user_refresh_tokens()` ঠিকমতো সংযুক্ত থাকলে এটি pass করার কথা।

কেন দুটো test দরকার? Refresh token blacklist করা এবং access token-এর version যাচাই করা দুটি আলাদা নিরাপত্তা ব্যবস্থা। একটির test pass করলেই অন্যটি কাজ করছে—এমন নিশ্চয়তা নেই।

## 9. Throttling test — অতিরিক্ত request সীমিত করা

আগের settings-এ `login` scope-এর rate ছিল `10/minute`। এখন যাচাই করব সীমা অতিক্রম করলে API `429 Too Many Requests` দেয় কি না।

`accounts/tests/test_security.py`-এ যোগ করুন:

```
from django.core.cache import cachefrom django.test import override_settingsclass ThrottlingTests(APITestCase):    def setUp(self):        cache.clear()        self.login_url = "/api/auth/login/"    @override_settings(        REST_FRAMEWORK={            "DEFAULT_AUTHENTICATION_CLASSES": [                "accounts.authentication.VersionedJWTAuthentication",            ],            "DEFAULT_PERMISSION_CLASSES": [                "rest_framework.permissions.IsAuthenticated",            ],            "DEFAULT_THROTTLE_CLASSES": [                "rest_framework.throttling.ScopedRateThrottle",            ],            "DEFAULT_THROTTLE_RATES": {                "login": "2/minute",            },        }    )    def test_login_is_throttled(self):        # Test-এর জন্য প্রথম দুই request অনুমোদিত,        # তৃতীয় request rate limit অতিক্রম করবে।        for _ in range(2):            self.client.post(                self.login_url,                {                    "email": "unknown@example.com",                    "password": "WrongPassword!123",                },                format="json",            )        response = self.client.post(            self.login_url,            {                "email": "unknown@example.com",                "password": "WrongPassword!123",            },            format="json",        )        self.assertEqual(            response.status_code,            status.HTTP_429_TOO_MANY_REQUESTS,        )
```

### Throttling test-এর গুরুত্বপূর্ণ বিষয়

এই test কাজ করার জন্য login view-এ `ScopedRateThrottle` এবং `throttle_scope = "login"` থাকতে হবে। আগে থেকে cache-এ rate-limit record থাকলে test-এর ফল প্রভাবিত হতে পারে, তাই test-এর শুরুতে `cache.clear()` ব্যবহার করেছি।

এই উদাহরণে `REST_FRAMEWORK` override করা হয়েছে বলে সেটির প্রয়োজনীয় authentication, permission ও throttle settings একসঙ্গে রাখা হয়েছে। আপনার project-এ যদি custom exception handler বা অন্য গুরুত্বপূর্ণ DRF settings থাকে, সেগুলোও override-এর মধ্যে রাখতে হবে—অথবা মূল settings বজায় রেখে আলাদা test settings ব্যবহার করতে পারেন।

মনে রাখবেন: DRF throttling সাধারণ abuse কমাতে সাহায্য করে; এটি পূর্ণাঙ্গ brute-force protection নয়। Production-এ reverse proxy বা API gateway-এ rate limiting, monitoring এবং প্রয়োজন অনুযায়ী temporary lockout যোগ করা যেতে পারে।

## 10. Security hardening — production-এর আগে যা যাচাই করবেন

Automated tests-এর পাশাপাশি নিচের configuration ও implementation-ও যাচাই করতে হবে।

### 10.1 Django production settings

`config/settings.py`-এ production environment অনুযায়ী নিশ্চিত করুন:

```
DEBUG = False# Environment variable থেকে নিতে হবে।SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]ALLOWED_HOSTS = os.environ["DJANGO_ALLOWED_HOSTS"].split(",")# HTTPS deployment-এর ক্ষেত্রে:SESSION_COOKIE_SECURE = TrueCSRF_COOKIE_SECURE = TrueSECURE_SSL_REDIRECT = True
```

এই snippet-এ `os` import করতে হবে। Environment variable অনুপস্থিত থাকলে application শুরু না হওয়া ভালো, বরং development-এর secret production-এ ব্যবহার করা বিপজ্জনক।

HTTPS-এর পেছনে reverse proxy ব্যবহার করলে `SECURE_SSL_REDIRECT` ও proxy-related settings deployment architecture অনুযায়ী যাচাই করুন। ভুল proxy configuration redirect loop তৈরি করতে পারে।

### 10.2 Password ও token security

- `AUTH_PASSWORD_VALIDATORS` সক্রিয় আছে।
- Password কখনো plaintext হিসেবে database-এ রাখা হয় না।
- Password reset ও email verification token database-এ hash করে রাখা হয়।
- Reset token-এর মেয়াদ আছে এবং একবার ব্যবহারের পর invalid হয়।
- Login, password reset ও email verification endpoint-এ throttling আছে।
- Password change/reset-এর পরে refresh token revoke হয়।
- Versioned JWT authentication পুরোনো access token প্রত্যাখ্যান করে।
- Access token-এর lifetime সংক্ষিপ্ত রাখা হয়েছে।
- Token, password বা reset link application log-এ লেখা হয় না।

### 10.3 Authorization security

- Default permission `IsAuthenticated`।
- Public endpoint-এ `AllowAny` শুধু প্রয়োজন অনুযায়ী।
- Admin endpoint-এ `IsAdminRole` বা উপযুক্ত permission আছে।
- User queryset-এ নিজের data-তেই সীমাবদ্ধ।
- Public serializer-এ `role`, `is_staff`, `is_superuser`, `token_version` writeable নয়।
- Admin role পরিবর্তনের endpoint-এ সাধারণ user access করতে পারে না।
- Admin promotion/demotion audit log করা হয়।
- কোনো user নিজের privilege বাড়াতে পারে না।

### 10.4 Email change ও account recovery

- Email change-এর আগে বর্তমান password যাচাই করা হয়।
- নতুন email-এর মালিকানা verify করা হয়।
- Email পরিবর্তনের পরে পুরোনো refresh token revoke হয়।
- Email change-এর সময় administrator দ্বারা নিষ্ক্রিয় করা account পুনরায় সক্রিয় হয় না।
- Forgot-password response registered email প্রকাশ করে না।
- Email service ব্যর্থ হলে token-সহ sensitive তথ্য log করা হয় না।

### 10.5 Deployment safety check

Project root থেকে চালান:

```
python manage.py check --deploy
```

এই command production configuration-এর কিছু সাধারণ সমস্যা জানাবে। এটি সব security vulnerability খুঁজে পায় না এবং সব warning ঠিক করলেই application নিরাপদ হয়ে যায়—এমন নয়।

## 11. পুরো test suite চালানো

Project root-এ চালান:

```
python manage.py test accounts.tests -v 2
```

শুধু authentication tests চালাতে:

```
python manage.py test accounts.tests.test_authentication -v 2
```

শুধু permission tests চালাতে:

```
python manage.py test accounts.tests.test_permissions -v 2
```

Password reset tests:

```
python manage.py test accounts.tests.test_password_reset -v 2
```

Security ও throttling tests:

```
python manage.py test accounts.tests.test_security -v 2
```

Expected output-এর ধরন:

```
Creating test database...
System check identified no issues.
...
Ran 10 tests in 2.4s

OK
Destroying test database...
```

এটি একটি উদাহরণমাত্র—আপনার test-এর সংখ্যা ও সময় ভিন্ন হবে।

### কোনো test fail করলে কী করবেন?

| Error                         | কী যাচাই করবেন                                    |
| ----------------------------- | ------------------------------------------------- |
| `404 Not Found`               | URL path ও `accounts/urls.py`                     |
| `401 Unauthorized`            | JWT authentication class, token ও credentials     |
| `403 Forbidden`               | Permission class এবং user role                    |
| `AttributeError`              | Model/serializer/service-এর প্রকৃত field ও method |
| `ValidationError`             | Password validator ও service-এর exception         |
| `429 Too Many Requests`       | Throttle scope, rate ও cache                      |
| Test database migration error | `makemigrations`, `migrate` ও custom user model   |

বিশেষভাবে, password change endpoint যদি `204 No Content` দেয়, তাহলে সেই test-এ `200 OK`-এর পরিবর্তে `204` প্রত্যাশা করতে হবে। Test-কে প্রকৃত API contract অনুযায়ী লিখবেন; শুধু test pass করানোর জন্য ভুল security behavior পরিবর্তন করবেন না।

## 12. Code coverage — কোন অংশ পরীক্ষা হয়েছে?

Coverage রিপোর্টের জন্য:

```
pip install coverage
```

এরপর চালান:

```
coverage run manage.py test accounts.tests
coverage report -m
coverage html
```

HTML report দেখতে Ubuntu-তে:

```
xdg-open htmlcov/index.html
```

Coverage হলো কতটা code test-এর মধ্য দিয়ে চালানো হয়েছে তার একটি পরিমাপ। ৯০% coverage থাকলেও authorization bug থাকতে পারে, যদি গুরুত্বপূর্ণ negative cases পরীক্ষা না করা হয়। তাই coverage-এর পাশাপাশি test-এর মান গুরুত্বপূর্ণ।

## 13. Final security test checklist

### Security verification

0/12 complete

Unauthenticated request private API-তে প্রত্যাখ্যাত হয়

Login সঠিক credentials-এ token দেয় এবং ভুল password প্রত্যাখ্যান করে

Unverified user login করতে পারে না

USER admin endpoint access করতে পারে না

একজন user অন্য user-এর profile পরিবর্তন করতে পারে না

Admin role update permission সঠিকভাবে কাজ করে

Password reset token expired হলে প্রত্যাখ্যাত হয়

Password reset token দ্বিতীয়বার ব্যবহার করা যায় না

Password change-এর পরে পুরোনো access token প্রত্যাখ্যাত হয়

Password change-এর পরে পুরোনো refresh token প্রত্যাখ্যাত হয়

Login rate limit অতিক্রম করলে 429 পাওয়া যায়

Public API response-এ sensitive account fields প্রকাশ পায় না

## Lesson 10-এর সারাংশ

এই Lesson-এ আমরা authentication system-এর প্রধান security boundary-গুলো test করার কাঠামো তৈরি করেছি। এখন system-কে শুধু স্বাভাবিক request-এর ক্ষেত্রে নয়, ভুল credentials, unauthorized access, expired token, token reuse, role escalation এবং excessive requests-এর ক্ষেত্রেও যাচাই করতে পারব।

একটি বাস্তব production project-এ পরবর্তী উন্নতির মধ্যে থাকবে:

1. GitHub Actions দিয়ে প্রতিটি push ও pull request-এ tests চালানো।
2. PostgreSQL-ভিত্তিক integration tests চালানো।
3. Concurrent password reset ও email change-এর race condition পরীক্ষা করা।
4. Admin role পরিবর্তনের audit log ও last-admin protection যোগ করা।
5. Dependency vulnerability scan এবং deployment security checks চালানো।

পরবর্তী Lesson 11: চাইলে আমরা এই Authentication System-এর জন্য GitHub Actions CI pipeline তৈরি করতে পারি—যেখানে automated tests, migration checks, code coverage এবং test failure হলে deployment বন্ধ করার ব্যবস্থা থাকবে।

----
# Lesson 11: Django REST Framework Authentication System — GitHub Actions CI Pipeline

এই Lesson-এ আমরা আগের Authentication System-এর জন্য Continuous Integration (CI) তৈরি করব। ফলে GitHub-এ code push বা Pull Request তৈরি করলে স্বয়ংক্রিয়ভাবে automated tests, migration checks, Django configuration checks এবং code coverage চলবে।

সবচেয়ে গুরুত্বপূর্ণ বিষয়: কোনো test বা check ব্যর্থ হলে CI workflow fail করবে, আর CI সফল না হলে সেটিকে deployment-এর অনুমতি দেওয়া হবে না।

## 1. CI/CD কী এবং আমাদের pipeline কীভাবে কাজ করবে?

- CI (Continuous Integration): নতুন code যোগ হওয়ার পর স্বয়ংক্রিয়ভাবে code ও tests যাচাই করা।
- CD (Continuous Delivery/Deployment): যাচাই সফল হলে release বা deployment-এর জন্য প্রস্তুত করা, অথবা deployment করা।

Developer pushes code

git push অথবা Pull Request

GitHub Actions runner

Python environment + dependencies

Quality checks

Django check, migration check

Automated tests

Authentication, RBAC, token security

Coverage report

পরীক্ষিত code-এর পরিমাণ

PASS

পরবর্তী ধাপের অনুমতি

FAIL

Merge/deploy আটকে যাবে, যদি branch protection সেট থাকে

## 2. Project structure

আমাদের আগের project structure-এ নতুন করে শুধু `.github/workflows/ci.yml` যোগ করব।

```
complete_auth_project/
├── .github/
│   └── workflows/
│       └── ci.yml
├── config/
│   ├── settings.py
│   └── urls.py
├── accounts/
│   ├── tests/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   └── services/
├── manage.py
├── requirements.txt
└── .gitignore
```

যদি আপনার project-এ `requirements.txt` না থাকে, প্রথমে virtual environment সক্রিয় করে সেটি তৈরি করুন:

```
pip freeze > requirements.txt
```

এটি বর্তমান environment-এর সব installed package লিখবে। Production project-এ পরে অপ্রয়োজনীয় package বাদ দিয়ে এবং version pin করে dependency file পরিষ্কার করা ভালো।

## 3. Coverage dependency যোগ করুন

Project-এর virtual environment সক্রিয় করে চালান:

```
pip install coverage
pip freeze > requirements.txt
```

`coverage` আমাদের জানাবে `accounts` app-এর কত শতাংশ code automated tests দিয়ে execute হয়েছে।

একটি গুরুত্বপূর্ণ পার্থক্য:

- Tests pass: লেখা test-গুলো সফল হয়েছে।
- Coverage pass: নির্ধারিত পরিমাণ code test-এর মধ্য দিয়ে গেছে।
- Security pass: প্রয়োজনীয় security properties সঠিকভাবে যাচাই হয়েছে।

এই তিনটি এক বিষয় নয়।

## 4. GitHub Actions workflow তৈরি করুন

প্রথমে folder ও file তৈরি করুন:

```
mkdir -p .github/workflows
touch .github/workflows/ci.yml
```

ফাইল: `.github/workflows/ci.yml`

```

name: Django Authentication CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]
  workflow_dispatch:

permissions:
  contents: read

jobs:
  test:
    name: Tests and Quality Checks
    runs-on: ubuntu-latest
    timeout-minutes: 15

    env:
      DJANGO_SETTINGS_MODULE: config.settings
      DJANGO_SECRET_KEY: ci-only-not-for-production
      DEBUG: "False"
      EMAIL_BACKEND: django.core.mail.backends.locmem.EmailBackend
      FRONTEND_ORIGIN: http://localhost:3000

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
          cache: pip
          cache-dependency-path: requirements.txt

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install coverage

      - name: Django system check
        run: python manage.py check

      - name: Check for missing migrations
        run: python manage.py makemigrations --check --dry-run

      - name: Apply migrations to test database
        run: python manage.py migrate --noinput

      - name: Run tests with coverage
        run: |
          coverage run --branch --source=accounts manage.py test accounts.tests -v 2
          coverage report -m --fail-under=70

      - name: Save coverage report
        if: always()
        run: coverage report -m || true

```

### এই workflow-এর প্রতিটি ধাপ কী করে?

| Step                 | কাজ                                                  |
| -------------------- | ---------------------------------------------------- |
| Checkout             | GitHub repository-এর code runner-এ আনে               |
| Set up Python        | নির্দিষ্ট Python version প্রস্তুত করে                |
| Install dependencies | `requirements.txt` থেকে packages install করে         |
| Django system check  | Django configuration-এর সাধারণ সমস্যা শনাক্ত করে     |
| Migration check      | Model পরিবর্তনের জন্য migration অনুপস্থিত কি না দেখে |
| Apply migrations     | CI database-এ migrations প্রয়োগ করে                  |
| Run tests            | `accounts.tests`-এর automated tests চালায়            |
| Coverage threshold   | Coverage 70%-এর কম হলে job fail করে                  |

এখানে `70` একটি শুরুর threshold, Django-এর বাধ্যতামূলক নিয়ম নয়। পরে project-এর critical code ও test quality অনুযায়ী এটি বাড়াতে পারেন।

`coverage report ... || true` শেষ ধাপে report দেখানোর চেষ্টা করে, কিন্তু এটিকে quality gate হিসেবে ব্যবহার করা হচ্ছে না। প্রকৃত gate হলো আগের `coverage report -m --fail-under=70` command।

গুরুত্বপূর্ণ: এই workflow ধরে নেয় আপনার CI environment-এ Django settings একটি test database ব্যবহার করতে পারে—সাধারণত SQLite। আপনার `config/settings.py` যদি PostgreSQL-এর environment variables বাধ্যতামূলক করে, তাহলে পরের PostgreSQL CI setup-টি অনুসরণ করুন।

## 5. যদি project PostgreSQL ব্যবহার করে

Production database PostgreSQL হলে SQLite দিয়ে test করা যথেষ্ট নয়। Database-specific behavior—যেমন constraints, indexes, transactions ও locking—পরীক্ষা করার জন্য CI-তেও PostgreSQL ব্যবহার করা ভালো।

GitHub Actions-এ PostgreSQL service যোগ করার উদাহরণ:

```
jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_DB: auth_test
          POSTGRES_USER: auth_user
          POSTGRES_PASSWORD: ci_test_password
        ports:
          - 5432:5432
        options: >-
          --health-cmd "pg_isready -U auth_user -d auth_test"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    env:
      DJANGO_SETTINGS_MODULE: config.settings
      DJANGO_SECRET_KEY: ci-only-not-for-production
      DB_NAME: auth_test
      DB_USER: auth_user
      DB_PASSWORD: ci_test_password
      DB_HOST: 127.0.0.1
      DB_PORT: "5432"
```

এটি আগের workflow-এর বিকল্প configuration অংশ—দুটো `jobs.test` আলাদাভাবে একই ফাইলে কপি করবেন না। আপনার `settings.py`-তে `DB_NAME`, `DB_USER`, `DB_PASSWORD`, `DB_HOST` ও `DB_PORT` environment variables থেকে database configuration পড়তে হবে এবং PostgreSQL driver, যেমন `psycopg`, dependencies-এ থাকতে হবে।

CI-এর database credentials শুধু disposable test database-এর জন্য। Production database credentials workflow-এ hardcode করবেন না।

## 6. GitHub-এ code push করুন

Repository আগে তৈরি করা থাকলে project root থেকে:

```
git status
git add .github/workflows/ci.yml requirements.txt
git commit -m "Add authentication CI pipeline"
git push origin main
```

আপনার বর্তমান branch যদি `develop` হয়, তাহলে:

```
git push origin develop
```

প্রথমবার repository তৈরি করতে হলে GitHub-এ repository তৈরি করে সেটিকে local project-এর সঙ্গে connect করতে হবে। `.env`, database dump, private key বা production secret GitHub-এ commit করবেন না।

একটি `.gitignore`-এ অন্তত এগুলো রাখুন:

```
.env
.venv/
venv/
__pycache__/
*.py[cod]
db.sqlite3
htmlcov/
.coverage
```

আপনার প্রয়োজন অনুযায়ী media uploads ও local configuration-ও ignore করুন। তবে source migrations-কে ignore করবেন না।

## 7. GitHub Actions-এ ফলাফল দেখুন

[Introduction to Continuous Integration with Github Actions - Automated testing with Github Actions](https://images.openai.com/static-rsc-4/U0wNkx9DuHC9og6OoHyx374m1Vguj2crCf4-YVZKpY5kZvBfqxott6Ud_vdaIzHBtEmudvuJRP-NTtgM6_13VipPb66q6Hl7DUKLo-usxJt12sP0DP3yeULIYgFZ399Kpckt724_j1-qcNqrCfyozKet2EuXM0qI9enlMRAK454?purpose=inline)

Success — সব check pass

Workflow-এর সব required step সফল হলে run-এ সবুজ check দেখা যাবে।

[Introduction to GitHub Actions – RSE Tools](https://images.openai.com/static-rsc-4/Xh_wdpGb2HJTkfOSOun3UzP17OtaCBINzMcTKlPyyE5TW-gY3REaFdpD3oOR1FXMvoXrpINZ2qqtn87Or2Acw5V4QiwlCR5ZFeeQHgSrdLLHiDzcL6sD3zKUMvOMw5DHZ6q5cJoEWSUzKp5u76v_LdpJfqsOwkBh7jxLoPFC8BM?purpose=inline)

Failure — অন্তত একটি check fail

Failed step খুলে error log পড়ুন, local-এ সমস্যা reproduce করুন, fix করে আবার push করুন।

GitHub repository খুলে Actions tab-এ গেলে workflow run দেখতে পাবেন। `workflow_dispatch` থাকার কারণে UI থেকেও manually workflow চালানো যাবে।

## 8. CI fail হলে merge আটকানোর ব্যবস্থা

শুধু workflow তৈরি করলেই সব merge আটকে যায় না। Repository-তে branch protection বা ruleset configure করতে হবে।

1. GitHub repository খুলুন।
2. Settings → Rules → Rulesets অথবা Settings → Branches-এ যান। UI অনুযায়ী branch protection বা ruleset তৈরি করুন।
3. `main` branch-এর জন্য rule প্রযোজ্য করুন।
4. Require a pull request before merging চালু করুন।
5. Require status checks to pass before merging চালু করে `Tests and Quality Checks` job-টি required check হিসেবে নির্বাচন করুন।
6. Rule save করে একটি test Pull Request খুলে যাচাই করুন যে CI fail হলে merge আটকে থাকে।

এতে developer-এর code review ও required CI check pass না করা পর্যন্ত সাধারণ Pull Request merge করা যাবে না। Administrator bypass বা repository-specific exceptions থাকলে সেগুলোও পরীক্ষা করতে হবে।

## 9. Test failure হলে deployment বন্ধ করা

বর্তমান workflow শুধু CI চালায়—এখনো কোনো VPS-এ deployment করে না। পরবর্তী deployment job যোগ করলে সেটিকে `needs: test` দিয়ে CI job-এর ওপর নির্ভরশীল করতে হবে।

উদাহরণ:

```
  deploy:
    name: Deploy to production
    needs: test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest

    steps:
      - name: Deployment gate passed
        run: echo "CI passed; deployment may proceed."
```

এটি শুধু dependency gate-এর demonstration; বাস্তবে এটি server-এ deploy করে না। `needs: test` থাকার কারণে `test` job fail বা skip হলে deployment job চলবে না। প্রকৃত deployment-এর জন্য SSH, image registry বা VPS-এর উপযোগী deployment steps এবং GitHub Secrets/Environment protection প্রয়োজন হবে।

Production deployment-এ secrets সীমিত রাখুন এবং deployment-কে `main` branch ও successful CI-এর সঙ্গে যুক্ত করুন।

## 10. Troubleshooting: সাধারণ CI errors

| Error                              | সমাধান                                                                            |
| ---------------------------------- | --------------------------------------------------------------------------------- |
| `ModuleNotFoundError`              | package `requirements.txt`-এ আছে কি না যাচাই করুন                                 |
| `ImproperlyConfigured: SECRET_KEY` | CI environment-এ test-only secret দিন                                             |
| `makemigrations --check` fail      | Model পরিবর্তনের migration তৈরি, review ও commit করুন                             |
| `OperationalError`                 | Database settings ও PostgreSQL service যাচাই করুন                                 |
| `DisallowedHost`                   | CI environment-এর host configuration পরীক্ষা করুন                                 |
| Coverage 70%-এর কম                 | গুরুত্বপূর্ণ behavior-এর test লিখুন; শুধু threshold কমিয়ে দেবেন না                |
| Throttling test fail               | Cache isolation, throttle scope ও rate যাচাই করুন                                 |
| Test local-এ pass, CI-তে fail      | Python/package version, environment variables ও timezone differences পরীক্ষা করুন |

## 11. Lesson 11 practical assignment

এই checklist শেষ করলে আপনার CI pipeline-এর মূল কাজ সম্পন্ন হবে।

### Assignment tracker

0/9

\`.github/workflows/ci.yml\` তৈরি করেছি

\`requirements.txt\`-এ প্রয়োজনীয় dependencies আছে

GitHub Actions-এ Django system check pass করে

Missing migrations check pass করে

Authentication ও permission tests pass করে

Password reset ও token revocation tests pass করে

Coverage threshold pass করে

\`main\` branch-এর required status check configure করেছি

Failed CI হলে deployment বন্ধ হওয়ার gate তৈরি করেছি

&#x20;Copy checklist

Lesson 11-এর মূল শিক্ষা: CI pipeline code push-এর পর automated quality gate তৈরি করে। তবে production-ready deployment-এর জন্য আরও প্রয়োজন সঠিক database testing, dependency/security scanning, protected branches, deployment secrets এবং rollback strategy।

পরবর্তী যৌক্তিক Lesson 12 হবে GitHub Actions + Docker image build + GitHub Container Registry + Ubuntu VPS deployment—যেখানে CI pass হলে তবেই নতুন image build ও deploy হবে, আর health check ব্যর্থ হলে deployment সফল বলে গণ্য হবে না।

---
# Lesson 12: GitHub Actions + Docker + GHCR + Ubuntu VPS Deployment

এই Lesson-এ আমরা আগের Django REST Framework Authentication System-কে production deployment workflow-এর সঙ্গে যুক্ত করব। GitHub-এ code push হলে প্রথমে automated tests ও migration checks চলবে। সব check pass করলে Docker image build হবে, GitHub Container Registry (GHCR)-এ publish হবে এবং Ubuntu VPS-এ deploy হবে।

সবচেয়ে গুরুত্বপূর্ণ নিয়ম: CI fail করলে deployment হবে না; deployment-এর পরে health check fail করলেও deployment সফল বলে গণ্য হবে না। আমরা আগের working version-এ ফিরে যাওয়ার জন্য একটি basic rollback strategy-ও তৈরি করব।

## 1. সম্পূর্ণ deployment architecture

GitHub repository

Code push / Pull Request

CI — Test & Quality Gate

Django checks · migrations · tests · coverage

Build & Publish Docker Image

GitHub Actions → GHCR

Ubuntu VPS

Docker Compose · Django · Gunicorn · PostgreSQL · Nginx

Health check PASS

Deployment accepted

Health check FAIL

Rollback attempted · job fails

## 2. আগে কিছু assumption ঠিক করে নিই

এই lesson-এর উদাহরণে ধরে নিচ্ছি:

- Django project: `complete_auth_project`
- Django settings module: `config.settings`
- WSGI application: `config.wsgi:application`
- Production domain: `api.example.com` — এটি placeholder, নিজের domain দিয়ে বদলাবেন।
- Ubuntu VPS-এ Docker Engine ও Docker Compose plugin ইনস্টল করা থাকবে।
- GitHub repository-তে `main` branch production branch।
- Application Gunicorn দিয়ে চলবে; Nginx public HTTPS traffic handle করবে।
- PostgreSQL-এর data container-এর বাইরে persistent volume-এ থাকবে।

আপনার আগের authentication project-এর settings যদি environment variables থেকে PostgreSQL configuration নেয়, সেই pattern-ই বজায় রাখব। Production secret GitHub repository বা Docker image-এর মধ্যে রাখব না।

## 3. Django-এর health-check endpoint তৈরি

Deployment-এর পরে শুধু container `running` আছে কি না দেখলেই হবে না। Django process request নিতে পারছে কি না এবং database connection কাজ করছে কি না, সেটিও যাচাই করতে হবে।

আমরা দুটি ধারণা আলাদা রাখব:

- Liveness: application process সচল আছে কি না।
- Readiness: application প্রয়োজনীয় dependency-সহ request serve করতে প্রস্তুত কি না।

এই lesson-এ `/health/` endpoint database connection পরীক্ষা করবে, তাই এটি readiness check হিসেবে ব্যবহার করব।

ফাইল: `config/health.py`

```
from django.db import connectionfrom django.http import JsonResponsefrom django.views.decorators.http import require_GET@require_GETdef health_check(request):    try:        with connection.cursor() as cursor:            cursor.execute("SELECT 1")            cursor.fetchone()    except Exception:        return JsonResponse(            {"status": "unhealthy"},            status=503,        )    return JsonResponse(        {"status": "ok"},        status=200,    )
```

ফাইল: `config/urls.py`-এ যোগ করুন। আগের URL patterns মুছে ফেলবেন না।

```
from django.urls import path, includefrom config.health import health_checkurlpatterns = [    # আগের URL patterns রাখুন।    path("health/", health_check, name="health-check"),]
```

এখন স্থানীয়ভাবে পরীক্ষা করুন:

```
python manage.py runserver
```

অন্য terminal থেকে:

```
curl -i http://127.0.0.1:8000/health/
```

সুস্থ database connection থাকলে response:

```
{"status": "ok"}
```

HTTP status হবে `200`। Database connection ব্যর্থ হলে endpoint `503 Service Unavailable` দেবে।

Security note: health endpoint-এ database password, hostname, exception text বা traceback প্রকাশ করবেন না। এই endpoint-এ কোনো sensitive তথ্য নেই, তবে public internet-এ expose করা উচিত কি না তা deployment architecture অনুযায়ী সিদ্ধান্ত নিন।

## 4. Production Dockerfile তৈরি

Project root-এ `Dockerfile` তৈরি করুন।

ফাইল: `Dockerfile`

```

FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1

WORKDIR /app

RUN addgroup --system django \
    && adduser --system --ingroup django django

COPY requirements.txt .
RUN python -m pip install --upgrade pip \
    && pip install -r requirements.txt

COPY --chown=django:django . .

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]

```

### কেন এই Dockerfile?

- `python:3.12-slim` তুলনামূলক ছোট base image দেয়।
- `PYTHONUNBUFFERED=1` container log দ্রুত দেখতে সাহায্য করে।
- `django` non-root user হিসেবে process চালায়।
- Gunicorn Django WSGI application serve করে।
- Log standard output/error-এ যায়, তাই `docker logs` দিয়ে দেখা যায়।

`3` worker কেবল একটি starting point; VPS-এর CPU ও memory অনুযায়ী worker সংখ্যা ঠিক করবেন। আপনার project-এ PostgreSQL driver বা Pillow-এর মতো package build dependencies চাইলে সেগুলোর system dependencies-ও Dockerfile-এ যোগ করতে হতে পারে।

### Docker build context ছোট রাখুন

ফাইল: `.dockerignore`

```
.git/
.github/
.venv/
venv/
__pycache__/
*.py[cod]
.env
.coverage
htmlcov/
media/
staticfiles/
*.sqlite3
```

যদি production media বা static files Docker image-এর মাধ্যমে পরিচালিত হয়, তাহলে ignore rules ও file collection strategy সেই অনুযায়ী পরিবর্তন করবেন। User-uploaded media-কে image-এর মধ্যে রাখবেন না; persistent storage ব্যবহার করুন।

স্থানীয়ভাবে build করুন:

```
docker build -t auth-api:local .
```

Container run করতে হলে environment variables ও database access configure করতে হবে। Production-এর মতো configuration ছাড়া কেবল build সফল হলেই application ঠিকভাবে run করবে—এমন নয়।

## 5. Docker Compose দিয়ে production application চালানো

ধরি, VPS-এ Nginx আগে থেকেই configure করা আছে এবং সেটি `127.0.0.1:8000`-এ Django application-এ proxy করবে।

Production-এর Compose file তৈরি করুন:

ফাইল: `compose.prod.yaml`

```

services:
  web:
    image: ${GHCR_IMAGE}:${IMAGE_TAG}
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DJANGO_SETTINGS_MODULE: config.settings
      PORT: "8000"
    ports:
      - "127.0.0.1:8000:8000"
    depends_on:
      db:
        condition: service_healthy
    healthcheck:
      test:
        - CMD
        - python
        - -c
        - "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/', timeout=3)"
      interval: 15s
      timeout: 5s
      retries: 5
      start_period: 30s

  db:
    image: postgres:16
    restart: unless-stopped
    env_file:
      - .env
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:

```

এই Compose configuration-এ:

- `web` GHCR থেকে নির্দিষ্ট image tag ব্যবহার করে।
- `db` PostgreSQL চালায় এবং `postgres_data` volume-এ data রাখে।
- Application port শুধু `127.0.0.1`-এ bind হয়; তাই এটি সরাসরি public interface-এ expose হয় না।
- Container health check Django endpoint পরীক্ষা করে।

সতর্কতা: আপনার VPS-এ আগে থেকেই PostgreSQL service বা অন্য Compose stack থাকলে দ্বিতীয় PostgreSQL container তৈরি করার আগে বর্তমান database architecture যাচাই করুন। Existing database ব্যবহার করলে `db` service ও তার volume অন্ধভাবে যোগ করবেন না। Production data volume কখনো delete করবেন না।

`depends_on` startup ordering-এ সাহায্য করে, কিন্তু database পরে অচল হলে application নিজে থেকে সব সমস্যা সমাধান করবে না। Django database connection retry, logs এবং monitoring-ও প্রয়োজন।

### Production `.env` উদাহরণ

VPS-এ `.env` ফাইল থাকবে, repository-তে নয়।

```
GHCR_IMAGE=ghcr.io/YOUR_GITHUB_OWNER/YOUR_REPOSITORY
IMAGE_TAG=initial
DJANGO_SECRET_KEY=REPLACE_WITH_A_LONG_RANDOM_SECRET
DEBUG=False
DJANGO_ALLOWED_HOSTS=api.example.com
FRONTEND_ORIGIN=https://example.com

DB_NAME=auth_db
DB_USER=auth_user
DB_PASSWORD=REPLACE_WITH_A_STRONG_DATABASE_PASSWORD
DB_HOST=db
DB_PORT=5432
```

আপনার `settings.py`-কে এই variables পড়তে হবে। যেমন `DEBUG`-কে string হিসেবে সরাসরি assign করবেন না; environment value-কে boolean হিসেবে parse করুন। `DJANGO_ALLOWED_HOSTS`-এর comma-separated value-কে list-এ রূপান্তর করতে হবে।

VPS-এ permissions সীমিত করুন:

```
chmod 600 .env
```

`.env` ফাইলের owner যেন deployment user হয় এবং অন্য user-রা সেটি পড়তে না পারে, তা নিশ্চিত করুন।

## 6. GitHub Container Registry (GHCR)-এ image publish

GHCR-এর image নাম সাধারণত এ রকম হয়:

```
ghcr.io/GITHUB_OWNER/REPOSITORY:TAG
```

আমরা প্রতিটি commit-এর জন্য immutable tag হিসেবে Git commit SHA ব্যবহার করব। `latest`-এর ওপর নির্ভর না করায় কোন version deploy হয়েছে তা শনাক্ত করা সহজ হবে।

উদাহরণ:

```
ghcr.io/example-org/complete-auth-project:a1b2c3d4...
```

এখানে `example-org` ও repository name শুধু উদাহরণ। নিজের GitHub owner ও repository অনুযায়ী image name ব্যবহার করবেন।

GitHub Actions workflow-এ GHCR push-এর জন্য প্রয়োজন হবে:

- `contents: read`
- `packages: write`
- GitHub Actions-এর `GITHUB_TOKEN`

Public registry image VPS থেকে সহজে pull করা যায়। Private image হলে VPS-এ registry authentication প্রয়োজন হবে। Production-এর জন্য যতটা সম্ভব সীমিত permission-সহ registry access ব্যবহার করুন।

## 7. VPS-এ deploy করার script তৈরি

আমরা deployment script-টি repository-তে রাখব, যাতে release process version control-এর মধ্যে থাকে।

ফাইল: `deploy/deploy.sh`

```

#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete-auth-project"
COMPOSE_FILE="compose.prod.yaml"
HEALTH_URL="http://127.0.0.1:8000/health/"

NEW_TAG="${1:?Usage: deploy.sh IMAGE_TAG}"

cd "$APP_DIR"

# .env-এর আগের image tag সংরক্ষণ
OLD_TAG="$(sed -n 's/^IMAGE_TAG=//p' .env | head -n 1)"

if [[ -z "$OLD_TAG" ]]; then
  echo "ERROR: IMAGE_TAG is missing from .env"
  exit 1
fi

# IMAGE_TAG আপডেট
sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=${NEW_TAG}/" .env

rollback() {
  echo "Deployment failed; attempting application rollback."

  sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=${OLD_TAG}/" .env

  if docker compose -f "$COMPOSE_FILE" up -d web; then
    echo "Previous application image restored."
  else
    echo "ERROR: Automatic rollback failed."
  fi
}

# Image pull ব্যর্থ হলে deployment থামবে
if ! docker compose -f "$COMPOSE_FILE" pull web; then
  sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=${OLD_TAG}/" .env
  echo "ERROR: Image pull failed."
  exit 1
fi

# Migration আগে চালানো হবে
if ! docker compose -f "$COMPOSE_FILE" run --rm --no-deps web \
  python manage.py migrate --noinput; then
  sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=${OLD_TAG}/" .env
  echo "ERROR: Database migration failed."
  exit 1
fi

# নতুন application চালু
docker compose -f "$COMPOSE_FILE" up -d web

# Health check retry
for attempt in $(seq 1 12); do
  if curl --fail --silent --show-error "$HEALTH_URL"; then
    echo
    echo "Deployment successful: ${NEW_TAG}"
    exit 0
  fi

  echo "Health check attempt ${attempt}/12 failed."
  sleep 5
done

rollback

# পুরোনো app পুনরুদ্ধারের পর সেটিও health check করব
for attempt in $(seq 1 6); do
  if curl --fail --silent "$HEALTH_URL"; then
    echo "Previous application is responding."
    exit 1
  fi
  sleep 5
done

echo "CRITICAL: New deployment failed and previous app health is not confirmed."
exit 1

```

এই script-এর উদ্দেশ্য:

1. নতুন image pull করা।
2. Database migration চালানো।
3. নতুন application container চালু করা।
4. সর্বোচ্চ ৬০ সেকেন্ড পর্যন্ত health check করা।
5. Health check fail করলে আগের application image-এ ফিরে যাওয়ার চেষ্টা করা।
6. Deployment ব্যর্থ হলে non-zero exit status ফেরত দেওয়া, যাতে GitHub Actions job fail হয়।

### Rollback-এর গুরুত্বপূর্ণ সীমাবদ্ধতা

এটি application-image rollback, পূর্ণ database rollback নয়। Migration সফল হওয়ার পর নতুন schema তৈরি হয়ে গেলে পুরোনো application সেই schema-তে চলবে—এমন নিশ্চয়তা নেই। এজন্য production migration-এ backward-compatible expand/contract পদ্ধতি ব্যবহার করুন এবং deployment-এর আগে database backup ও restore procedure পরীক্ষা করুন।

আরেকটি বিষয়: এই script Compose-এর `web` service update করে। Nginx, database, Redis বা অন্য service-এর health আলাদাভাবে যাচাই করতে হবে, যদি সেগুলো deployment-এর critical dependency হয়।

VPS-এ script-টি executable করুন:

```
chmod +x deploy/deploy.sh
```

প্রথমে staging environment-এ এটি পরীক্ষা করুন। সরাসরি production-এ failure injection করে rollback পরীক্ষা করবেন না।

## 8. GitHub Actions: CI pass হলে image build ও deploy

এখন আগের Lesson 11-এর workflow-এ দ্বিতীয় job যোগ করব। নিচের উদাহরণটি একটি সম্পূর্ণ workflow skeleton—এর `test` job-এ আপনার আগের CI steps রাখবেন এবং `build-and-deploy` job-টি যোগ করবেন।

ফাইল: `.github/workflows/ci.yml`

```

name: Authentication CI and Deployment

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]
  workflow_dispatch:

permissions:
  contents: read

jobs:
  test:
    name: Tests and Quality Checks
    runs-on: ubuntu-latest
    timeout-minutes: 15

    env:
      DJANGO_SETTINGS_MODULE: config.settings
      DJANGO_SECRET_KEY: ci-only-not-for-production
      DEBUG: "False"
      EMAIL_BACKEND: django.core.mail.backends.locmem.EmailBackend
      FRONTEND_ORIGIN: http://localhost:3000

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
          cache: pip
          cache-dependency-path: requirements.txt

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
          pip install coverage

      - name: Django system check
        run: python manage.py check

      - name: Migration check
        run: python manage.py makemigrations --check --dry-run

      - name: Apply migrations
        run: python manage.py migrate --noinput

      - name: Automated tests and coverage
        run: |
          coverage run --branch --source=accounts manage.py test accounts.tests -v 2
          coverage report -m --fail-under=70

  build-and-deploy:
    name: Build, Publish and Deploy
    needs: test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    timeout-minutes: 20

    permissions:
      contents: read
      packages: write

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to GitHub Container Registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build and push image
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          tags: |
            ghcr.io/${{ github.repository }}:${{ github.sha }}

      - name: Configure SSH
        uses: webfactory/ssh-agent@v0.9.0
        with:
          ssh-private-key: ${{ secrets.VPS_SSH_PRIVATE_KEY }}

      - name: Add verified VPS host key
        env:
          VPS_KNOWN_HOSTS: ${{ secrets.VPS_KNOWN_HOSTS }}
        run: |
          mkdir -p ~/.ssh
          chmod 700 ~/.ssh
          printf '%s\n' "$VPS_KNOWN_HOSTS" >> ~/.ssh/known_hosts
          chmod 600 ~/.ssh/known_hosts

      - name: Deploy image to VPS
        env:
          VPS_HOST: ${{ secrets.VPS_HOST }}
          VPS_USER: ${{ secrets.VPS_USER }}
          IMAGE_TAG: ${{ github.sha }}
        run: |
          ssh "$VPS_USER@$VPS_HOST" \
            "cd /opt/complete-auth-project && ./deploy/deploy.sh '$IMAGE_TAG'"

```

### Workflow কীভাবে failure আটকায়?

`needs: test` হলো মূল gate। `test` job fail হলে `build-and-deploy` job চলবে না। Pull Request-এ test চলবে, কিন্তু deployment job শুধু `main` branch-এ push event হলে চলবে।

তবে workflow-তে একটি গুরুত্বপূর্ণ বিষয় আছে: GitHub-এর `GITHUB_TOKEN` দিয়ে GHCR-এ image publish করা যায়, কিন্তু VPS-কে সেই image pull করার অনুমতি আলাদাভাবে দিতে হবে। একইভাবে, `ghcr.io/${{ github.repository }}`-এর path lowercase হতে হবে। Repository বা owner-এর নাম uppercase থাকলে tag-টি lowercase করে build ও deployment—দুই জায়গায় একই image name ব্যবহার করুন।

Production workflow-এ external Actions-এর version pinning ও supply-chain security review-ও গুরুত্বপূর্ণ। উপরের version tags উদাহরণ হিসেবে দেওয়া; production-এ আপনার প্রতিষ্ঠানের নীতি অনুযায়ী নির্দিষ্ট reviewed commit SHA-তে pin করুন।

## 9. GitHub Secrets configure করুন

GitHub repository-তে যান:

Settings → Secrets and variables → Actions → New repository secret

এই secrets তৈরি করুন:

| Secret                | কী রাখবেন                               |
| --------------------- | --------------------------------------- |
| `VPS_HOST`            | VPS-এর IP address বা SSH hostname       |
| `VPS_USER`            | Deployment-এর জন্য নির্ধারিত Linux user |
| `VPS_SSH_PRIVATE_KEY` | সেই user-এর SSH private key             |
| `VPS_KNOWN_HOSTS`     | VPS-এর যাচাই করা SSH host-key entry     |

কোনো secret-কে workflow file-এ সরাসরি লিখবেন না।

### SSH key setup

নিজের trusted computer-এ deployment-এর জন্য আলাদা SSH key তৈরি করতে পারেন:

```
ssh-keygen -t ed25519 -C "github-actions-deploy"
```

- Public key (`.pub`) VPS-এর deployment user-এর `~/.ssh/authorized_keys`-এ যোগ করুন।
- Private key `VPS_SSH_PRIVATE_KEY` secret-এ রাখুন।
- Private key repository-তে commit করবেন না।
- `VPS_KNOWN_HOSTS`-এ VPS-এর host key নির্ভরযোগ্য উপায়ে যাচাই করে রাখুন।

`ssh-keyscan` দিয়ে host key সংগ্রহ করা যায়, কিন্তু সেটি একা যাচাইয়ের বিকল্প নয়। সংগ্রহ করা fingerprint-টি VPS provider console বা অন্য trusted channel থেকে পাওয়া fingerprint-এর সঙ্গে মিলিয়ে নিন।

## 10. Ubuntu VPS প্রস্তুত করুন

প্রথমে VPS-এ deployment user ও application directory প্রস্তুত করুন। নিচের উদাহরণে `deploy` নামে user ব্যবহার করা হয়েছে; নিজের server policy অনুযায়ী সেটি তৈরি ও configure করুন।

```
sudo mkdir -p /opt/complete-auth-project/deploy
sudo chown -R deploy:deploy /opt/complete-auth-project
```

Deployment user-এর Docker access, SSH permissions ও sudo privileges সীমিত রাখুন। Docker group membership কার্যত খুব উচ্চ privilege দেয়; তাই untrusted user-কে এই group-এ যুক্ত করবেন না।

GitHub Actions-এ SSH connection সফল হওয়ার জন্য deployment user-এর authorized public key থাকতে হবে এবং VPS firewall-এ SSH access অনুমোদিত হতে হবে।

### Private GHCR image pull

আপনার GHCR package private হলে VPS-এর deployment user দিয়ে একবার registry login করুন:

```
echo "YOUR_READ_PACKAGES_TOKEN" | \
  docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
```

এখানে `YOUR_READ_PACKAGES_TOKEN` হলো GHCR package পড়ার অনুমতি-সহ token। Command-এ placeholder-এর জায়গায় নিজের credential দিন, কিন্তু token-টি shell history-তে রেখে দেবেন না। নিরাপদ secret manager বা interactive input ব্যবহার করা উত্তম। Login সফল হলে Docker credentials file-টি সীমিত permissions-এ রাখুন।

Private registry-এর ক্ষেত্রে শুধু `docker login` সফল হলেই হবে না; token-এর package access permission ও package visibility-ও ঠিক থাকতে হবে।

## 11. Workflow-তে deployment files VPS-এ পাঠানো

একটি গুরুত্বপূর্ণ সংশোধন: আগের workflow শুধু VPS-এ `deploy.sh` চালাতে বলেছে। কিন্তু VPS-এ script ও Compose file আগে থেকে না থাকলে বা নতুন version না পৌঁছালে deployment ব্যর্থ হবে। তাই deployment step-এর আগে files copy করতে হবে।

`.github/workflows/ci.yml`-এর `Deploy image to VPS` step-টি নিচের version দিয়ে প্রতিস্থাপন করুন:

```

      - name: Deploy image to VPS
        env:
          VPS_HOST: ${{ secrets.VPS_HOST }}
          VPS_USER: ${{ secrets.VPS_USER }}
          IMAGE_TAG: ${{ github.sha }}
        run: |
          set -euo pipefail

          scp compose.prod.yaml \
            "$VPS_USER@$VPS_HOST:/tmp/compose.prod.yaml"

          scp deploy/deploy.sh \
            "$VPS_USER@$VPS_HOST:/tmp/deploy.sh"

          ssh "$VPS_USER@$VPS_HOST" \
            "install -m 644 /tmp/compose.prod.yaml /opt/complete-auth-project/compose.prod.yaml && \
             install -m 755 /tmp/deploy.sh /opt/complete-auth-project/deploy/deploy.sh && \
             rm -f /tmp/compose.prod.yaml /tmp/deploy.sh && \
             cd /opt/complete-auth-project && \
             ./deploy/deploy.sh '$IMAGE_TAG'"

```

এই ধাপটি ধরে নেয় deployment user `/opt/complete-auth-project`-এ লিখতে পারে। Production-এ SSH user-কে পুরো server-এর administrator না বানিয়ে নির্দিষ্ট deployment directory-তে প্রয়োজনীয় access দিন।

## 12. Image name ও environment মিলিয়ে নিন

GitHub repository owner বা repository name-এ uppercase অক্ষর থাকলে Docker image reference lowercase করুন। Workflow-এর build step-এ নিচের step যোগ করুন:

```
      - name: Set lowercase image name
        id: image
        env:
          REPOSITORY: ${{ github.repository }}
        run: |
          IMAGE_NAME="ghcr.io/$(echo "$REPOSITORY" | tr '[:upper:]' '[:lower:]')"
          echo "name=$IMAGE_NAME" >> "$GITHUB_OUTPUT"
```

তারপর `Build and push image` step-এর `tags` অংশটি এভাবে করুন:

```
          tags: |
            ${{ steps.image.outputs.name }}:${{ github.sha }}
```

VPS-এর `.env` ফাইলে একই image name ব্যবহার করুন:

```
GHCR_IMAGE=ghcr.io/your-owner/complete-auth-project
IMAGE_TAG=initial
```

`your-owner` ও repository name lowercase করে নিজের প্রকৃত নাম বসাবেন। `IMAGE_TAG`-এর প্রাথমিক value হিসেবে এমন একটি tag দিতে হবে যা GHCR-এ বাস্তবে আছে—যেমন আগে build ও publish করা image tag।

Health check-এ Django `ALLOWED_HOSTS`-এর বিষয়টিও যাচাই করুন। Container-এর ভিতরে health check `127.0.0.1` ব্যবহার করলে `127.0.0.1`-কে `ALLOWED_HOSTS`-এ যুক্ত করুন, অথবা health request-এ অনুমোদিত `Host` header পাঠান। অন্যথায় application সচল থাকলেও health check `400 Bad Request` দিতে পারে।

## 13. Nginx ও HTTPS-এর সঙ্গে যুক্ত করা

যদি আপনার আগের Lesson-এ Nginx ও HTTPS ইতোমধ্যে configure করা থাকে, নিশ্চিত করুন Nginx upstream এই port-এ proxy করছে:

```
location / {
    proxy_pass http://127.0.0.1:8000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

এটি server block-এর `location /` অংশের উদাহরণ, পুরো HTTPS configuration নয়। আপনার TLS certificate, redirect, security headers এবং WebSocket প্রয়োজন হলে সেগুলোর configuration বজায় রাখুন।

Nginx config যাচাই করুন:

```
sudo nginx -t
sudo systemctl reload nginx
```

Deployment-এর পরে বাইরের URL থেকেও health check করুন:

```
curl -i https://api.example.com/health/
```

এটি `200` দিলে public HTTPS route-ও application পর্যন্ত পৌঁছাচ্ছে। Local container check ও public HTTPS check দুটোই গুরুত্বপূর্ণ, কারণ Nginx, TLS বা firewall-এর সমস্যা container health check-এ ধরা নাও পড়তে পারে।

## 14. Deployment-এর আগে final verification

Production-এ deploy করার আগে এই checklist অনুসরণ করুন।

### Production deployment checklist

0/12

Local-এ Django tests ও migration checks pass করেছে

Docker image local-এ build হয়েছে

GHCR-এ commit SHA tag-সহ image publish হয়েছে

VPS-এর .env-এ সঠিক GHCR_IMAGE ও IMAGE_TAG আছে

VPS SSH key ও verified known_hosts configure করা হয়েছে

VPS থেকে GHCR image pull করা যায়

PostgreSQL persistent volume ও backup যাচাই করা হয়েছে

/health/ endpoint container-এর ভিতরে 200 দেয়

Nginx HTTPS URL থেকেও /health/ endpoint 200 দেয়

Test failure হলে build/deploy job চলবে না

Health check failure হলে rollback attempt হয় এবং CI job fail করে

Database migration-এর backward compatibility ও restore plan review করা হয়েছে

### Deployment সফল হয়েছে কীভাবে বুঝবেন?

VPS-এ চালান:

```
cd /opt/complete-auth-project

docker compose -f compose.prod.yaml ps
docker compose -f compose.prod.yaml logs --tail=100 web
docker compose -f compose.prod.yaml logs --tail=100 db

curl -i http://127.0.0.1:8000/health/
curl -i https://api.example.com/health/
```

সবচেয়ে গুরুত্বপূর্ণ: শুধু `docker compose ps`-এ `Up` দেখা মানেই deployment সফল নয়। Application health check এবং public route—দুটোই যাচাই করুন।

## 15. Failure scenario-গুলো কীভাবে যাচাই করবেন?

Production data ব্যবহার না করে staging environment-এ পরীক্ষা করুন।

| Scenario                         | প্রত্যাশিত আচরণ                                                    |
| -------------------------------- | ------------------------------------------------------------------ |
| Automated test fail              | `test` job fail; image build/deploy হবে না                         |
| Docker build fail                | GHCR publish/deploy হবে না                                         |
| Image pull fail                  | পুরোনো application চালু থাকবে; deployment fail                     |
| Migration fail                   | নতুন application switch হবে না; deployment fail                    |
| নতুন container health check fail | আগের image-এ rollback attempt; workflow fail                       |
| পুরোনো image-ও healthy নয়        | Critical error; manual investigation প্রয়োজন                       |
| Public HTTPS route fail          | Public endpoint test fail; Nginx/TLS/network troubleshooting দরকার |

Rollback সম্পর্কে শেষ সতর্কতা: migration চালানোর পরে application image-এ ফিরে যাওয়া সবসময় নিরাপদ নয়। Database migration-কে backward-compatible রাখুন, production backup তৈরি করুন এবং backup থেকে restore সত্যিই কাজ করে কি না পরীক্ষা করুন। শুধু container rollback-কে database recovery হিসেবে বিবেচনা করবেন না।

## Lesson 12-এর সারাংশ

এখন আপনার deployment pipeline-এর মূল ধাপগুলো হলো:

1. GitHub Actions-এ tests ও migration checks।
2. সফল CI-এর পরে Docker image build।
3. GHCR-এ commit SHA-সহ image publish।
4. SSH দিয়ে Ubuntu VPS-এ deployment।
5. Database migration ও container restart।
6. Local এবং public health check।
7. Failure হলে rollback attempt এবং deployment job fail।

এই কাঠামো একটি ভালো production foundation, তবে production readiness নিশ্চিত করতে PostgreSQL backup/restore, logs ও monitoring, least-privilege credentials, dependency scanning এবং migration strategy-ও প্রয়োজন।

পরবর্তী Lesson 13: Docker Compose-ভিত্তিক deployment-কে আরও নির্ভরযোগ্য করা—zero-downtime deployment strategy, blue-green deployment, database migration compatibility, automatic rollback verification, health monitoring এবং deployment notifications।

---
# Lesson 13: Production-Grade Deployment — Blue-Green, Zero-Downtime, Rollback ও Monitoring

আগের Lesson 12-এ আমরা GitHub Actions → Docker image → GHCR → Ubuntu VPS deployment তৈরি করেছি। এবার সেটিকে আরও নির্ভরযোগ্য করব, যাতে নতুন release deploy করার সময় ব্যবহারকারীরা যতটা সম্ভব uninterrupted service পান এবং release ব্যর্থ হলে দ্রুত আগের working version-এ ফিরে যাওয়া যায়।

এই Lesson-এ আমরা ছয়টি বিষয় শিখব:

1. Zero-downtime deployment-এর ধারণা ও সীমাবদ্ধতা।
2. Docker Compose দিয়ে Blue-Green deployment।
3. Backward-compatible database migration।
4. Automatic rollback এবং rollback verification।
5. Health monitoring ও deployment notification।
6. GitHub Actions থেকে deployment workflow পরিচালনা।

একটি গুরুত্বপূর্ণ বিষয়: কোনো deployment design-ই শূন্য downtime নিশ্চিত করে না। Application, database, reverse proxy, network এবং migration—সবকিছুর আচরণ সঠিকভাবে পরিচালনা করতে হবে। আমরা এমন architecture তৈরি করব যা downtime-এর ঝুঁকি কমায় এবং failure দ্রুত শনাক্ত করে।

## 1. Single-container deployment বনাম Blue-Green deployment

আগের architecture-এ Nginx সরাসরি একটি Django container-এ request পাঠাত:

Users

Nginx

Django container — current version

সমস্যা: একই service replace করার সময় restart বা startup-এর কারণে request ব্যর্থ হতে পারে।

Blue-Green deployment-এ আমরা দুটি application environment রাখব:

- Blue: বর্তমানে traffic serve করছে এমন version।
- Green: নতুন version, যা production traffic নেওয়ার আগে পরীক্ষা করা হবে।

Users

Nginx — traffic switch

Blue

বর্তমান release

Serving traffic

Green

নতুন release

Pre-deployment check

Green healthy হলে Nginx upstream switch করা হবে। Switch-এর পরে সমস্যা হলে Blue-তে ফিরিয়ে নেওয়া যাবে।

এই architecture-এর বড় সুবিধা হলো নতুন version পরীক্ষা করার সময় পুরোনো version request serve করতে পারে। তবে database schema ও shared resources compatible না হলে traffic switch করেও সম্পূর্ণ নিরাপত্তা নিশ্চিত করা যায় না।

## 2. নতুন deployment architecture

এই lesson-এ Nginx host machine-এ থাকবে, আর Docker Compose দুটি Django application container চালাবে। PostgreSQL থাকবে shared persistent database হিসেবে।

Nginx + HTTPS

Public entry point

Blue container

127.0.0.1:8001

Release A

Green container

127.0.0.1:8002

Release B

Shared PostgreSQL

Persistent volume · backup · compatible migrations

এখানে Blue ও Green আলাদা container হলেও একই database ব্যবহার করবে। তাই নতুন code-কে পুরোনো schema-তে চলতে পারার মতো করে তৈরি করতে হবে, এবং traffic switch-এর পর rollback দরকার হলেও database যেন পুরোনো version-এর সঙ্গে compatible থাকে।

## 3. Docker Compose Blue-Green configuration

আগের `compose.prod.yaml`-এর application service-কে দুটি service-এ ভাগ করব। নিচের উদাহরণে database-ও একই Compose project-এর মধ্যে আছে। যদি আপনার VPS-এ PostgreSQL ইতিমধ্যে আলাদা service হিসেবে চলে, তাহলে database service duplicate না করে সেই বিদ্যমান network ও database configuration ব্যবহার করবেন।

ফাইল: `compose.prod.yaml`

```

services:
  app-blue:
    image: ${GHCR_IMAGE}:${IMAGE_TAG_BLUE}
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DJANGO_SETTINGS_MODULE: config.settings
    ports:
      - "127.0.0.1:8001:8000"
    depends_on:
      db:
        condition: service_healthy
    healthcheck:
      test:
        - CMD
        - python
        - -c
        - "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/', timeout=3)"
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

  app-green:
    image: ${GHCR_IMAGE}:${IMAGE_TAG_GREEN}
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DJANGO_SETTINGS_MODULE: config.settings
    ports:
      - "127.0.0.1:8002:8000"
    depends_on:
      db:
        condition: service_healthy
    healthcheck:
      test:
        - CMD
        - python
        - -c
        - "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/', timeout=3)"
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

  db:
    image: postgres:16
    restart: unless-stopped
    env_file:
      - .env
    environment:
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:

```

### এই configuration-এর গুরুত্বপূর্ণ বিষয়

- Blue port `8001`; Green port `8002`।
- দুটো container-ই একই PostgreSQL database ব্যবহার করে।
- `.env`-এ দুই image tag আলাদাভাবে রাখা হয়।
- Container health check application-এর `/health/` endpoint পরীক্ষা করে।
- Nginx একবারে একটি application port-এ traffic পাঠাবে।

`.env`-এ এই variables যোগ করুন:

```
GHCR_IMAGE=ghcr.io/your-owner/complete-auth-project
IMAGE_TAG_BLUE=your-current-known-good-tag
IMAGE_TAG_GREEN=your-current-known-good-tag

DJANGO_SECRET_KEY=YOUR_SECRET
DEBUG=False
DJANGO_ALLOWED_HOSTS=api.example.com
FRONTEND_ORIGIN=https://example.com

DB_NAME=auth_db
DB_USER=auth_user
DB_PASSWORD=YOUR_DATABASE_PASSWORD
DB_HOST=db
DB_PORT=5432
```

`your-current-known-good-tag`-এর জায়গায় GHCR-এ থাকা সত্যিকারের image tag দিন। Production `.env`-এ secret-গুলো শুধু VPS-এ থাকবে; repository-তে নয়।

Migration বিষয়ে সতর্কতা: Compose-এ `depends_on` database startup order নিয়ন্ত্রণ করে। এটি migration-কে স্বয়ংক্রিয়ভাবে চালায় না। আমরা deployment script-এ migration আলাদাভাবে চালাব।

## 4. Nginx upstream দিয়ে traffic switch করা

Nginx-কে সরাসরি কোনো নির্দিষ্ট container name-এর ওপর নির্ভর না করিয়ে একটি upstream name ব্যবহার করব। এরপর active upstream-এর port পরিবর্তন করে traffic switch করব।

Nginx configuration-এ এই upstream reference ব্যবহার করুন:

ফাইল: আপনার domain-এর Nginx server configuration, যেমন `/etc/nginx/sites-available/api.example.com`

```
location / {
    proxy_pass http://app_backend;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

`app_backend` upstream-টি `http` context-এ define করতে হবে। Ubuntu-তে সাধারণত `/etc/nginx/conf.d/*.conf` ফাইলগুলো `http` context থেকে include হয়।

প্রাথমিকভাবে Blue active ধরে নিচের ফাইল তৈরি করুন:

ফাইল: `/etc/nginx/conf.d/active-upstream.conf`

```
upstream app_backend {
    server 127.0.0.1:8001;
    keepalive 32;
}
```

পরীক্ষা করুন:

```
sudo nginx -t
sudo systemctl reload nginx
```

Nginx এখন Blue application-এ request পাঠাবে। Green healthy হলে একই ফাইলে port `8002` বসিয়ে reload করলে নতুন request Green-এ যাবে।

গুরুত্বপূর্ণ: Nginx reload সাধারণত graceful হয়, কিন্তু বিদ্যমান request ও দীর্ঘস্থায়ী connections-এর আচরণ application configuration অনুযায়ী ভিন্ন হতে পারে। WebSocket, streaming request এবং long-running API-এর জন্য আলাদা drain strategy প্রয়োজন হতে পারে।

## 5. Database migration compatibility: Expand → Migrate → Contract

Blue-Green deployment-এ database সবচেয়ে গুরুত্বপূর্ণ অংশ। ধরুন, আপনার `User` model-এ `full_name` যোগ করতে হবে। সরাসরি পুরোনো column rename বা delete করে দিলে Blue version ভেঙে যেতে পারে।

নিরাপদ পদ্ধতি তিন ধাপে:

Phase 1 — Expand

নতুন nullable column বা backward-compatible schema change যোগ করুন। পুরোনো ও নতুন application version যেন উভয়েই কাজ করতে পারে।

Phase 2 — Migrate

নতুন application deploy করুন। প্রয়োজন হলে background data migration বা dual-write/read compatibility সাময়িকভাবে বজায় রাখুন।

Phase 3 — Contract

পুরোনো application version আর deploy বা rollback করার প্রয়োজন না থাকলে পরে পুরোনো column, field বা compatibility code সরান।

### Django migration-এর উদাহরণ

ধরি, `Profile` model-এ নতুন field যোগ করতে হবে।

```
# accounts/models.pyclass Profile(models.Model):    # আগের fields থাকবে।    display_name = models.CharField(        max_length=150,        null=True,        blank=True,    )
```

Migration তৈরি করুন:

```
python manage.py makemigrations accounts
python manage.py sqlmigrate accounts <migration_number>
```

`<migration_number>`-এর জায়গায় তৈরি হওয়া migration-এর প্রকৃত নম্বর দিন। Migration review করে তারপর commit করুন।

এখানে nullable field যোগ করা সাধারণত backward-compatible হওয়ার সম্ভাবনা বেশি, তবে table size, database backend, index, constraints এবং query behavior বিবেচনা করতে হবে। বড় production table-এ migration lock বা দীর্ঘসময় নিতে পারে।

কোনো migration fail করলে শুধু পুরোনো container চালু করাই যথেষ্ট নয়। Database schema আংশিক বদলেছে কি না, migration transaction-এর আচরণ কী, এবং recovery কীভাবে হবে—সেটি যাচাই করতে হবে। Production database-এর migration rollback করার আগে backup ও restore plan থাকা আবশ্যক।

## 6. Blue-Green deployment script

এখন একটি script তৈরি করব, যা:

1. বর্তমান active color শনাক্ত করবে।
2. অন্য color-এ নতুন image pull করবে।
3. migration চালাবে।
4. নতুন container start করে health check করবে।
5. Nginx upstream switch করবে।
6. Public HTTPS health check করবে।
7. ব্যর্থ হলে আগের upstream-এ ফিরে গিয়ে rollback verification করবে।

ফাইল: `deploy/deploy-blue-green.sh`

```

#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete-auth-project"
COMPOSE_FILE="compose.prod.yaml"
ACTIVE_FILE="$APP_DIR/active-color"
UPSTREAM_FILE="/etc/nginx/conf.d/active-upstream.conf"
PUBLIC_HEALTH_URL="https://api.example.com/health/"

NEW_TAG="${1:?Usage: deploy-blue-green.sh IMAGE_TAG}"

cd "$APP_DIR"

if [[ ! -f "$ACTIVE_FILE" ]]; then
  echo "ERROR: active-color file is missing."
  exit 1
fi

OLD_COLOR="$(cat "$ACTIVE_FILE")"

case "$OLD_COLOR" in
  blue)
    NEW_COLOR="green"
    OLD_PORT="8001"
    NEW_PORT="8002"
    ;;
  green)
    NEW_COLOR="blue"
    OLD_PORT="8002"
    NEW_PORT="8001"
    ;;
  *)
    echo "ERROR: invalid active color: $OLD_COLOR"
    exit 1
    ;;
esac

echo "Current color: $OLD_COLOR"
echo "Deploying to: $NEW_COLOR"
echo "Image tag: $NEW_TAG"

# Record the current tag for rollback.
OLD_TAG_VAR="IMAGE_TAG_${OLD_COLOR^^}"
OLD_TAG="$(sed -n "s/^${OLD_TAG_VAR}=//p" .env | head -n 1)"

if [[ -z "$OLD_TAG" ]]; then
  echo "ERROR: current image tag is missing."
  exit 1
fi

NEW_TAG_VAR="IMAGE_TAG_${NEW_COLOR^^}"

set_image_tag() {
  local variable="$1"
  local value="$2"

  if grep -q "^${variable}=" .env; then
    sed -i "s|^${variable}=.*|${variable}=${value}|" .env
  else
    printf '%s=%s\n' "$variable" "$value" >> .env
  fi
}

service_for_color() {
  case "$1" in
    blue) echo "app-blue" ;;
    green) echo "app-green" ;;
    *) return 1 ;;
  esac
}

health_check() {
  local url="$1"
  local attempts="${2:-12}"

  for attempt in $(seq 1 "$attempts"); do
    if curl --fail --silent --show-error \
      --max-time 5 "$url"; then
      echo
      return 0
    fi

    echo "Health check ${attempt}/${attempts} failed."
    sleep 5
  done

  return 1
}

switch_upstream() {
  local port="$1"
  local temp_file

  temp_file="$(mktemp)"

  cat > "$temp_file" <<EOF
upstream app_backend {
    server 127.0.0.1:${port};
    keepalive 32;
}
EOF

  sudo install -m 644 "$temp_file" "${UPSTREAM_FILE}.new"
  rm -f "$temp_file"

  sudo nginx -t

  sudo mv "${UPSTREAM_FILE}.new" "$UPSTREAM_FILE"

  if ! sudo nginx -t || ! sudo systemctl reload nginx; then
    echo "ERROR: Nginx switch failed."
    return 1
  fi
}

rollback() {
  echo "Attempting rollback to ${OLD_COLOR}..."

  set_image_tag "$NEW_TAG_VAR" "$OLD_TAG"

  # Restore previous traffic route.
  if switch_upstream "$OLD_PORT"; then
    printf '%s\n' "$OLD_COLOR" > "$ACTIVE_FILE"

    if health_check "$PUBLIC_HEALTH_URL" 6; then
      echo "Rollback verified: previous release is healthy."
    else
      echo "CRITICAL: rollback route restored but health is failing."
    fi
  else
    echo "CRITICAL: unable to restore previous Nginx route."
  fi
}

# Update the inactive color's image tag.
set_image_tag "$NEW_TAG_VAR" "$NEW_TAG"

# Pull the new image before changing live traffic.
if ! docker compose -f "$COMPOSE_FILE" pull \
  "$(service_for_color "$NEW_COLOR")"; then
  set_image_tag "$NEW_TAG_VAR" "$OLD_TAG"
  echo "ERROR: image pull failed."
  exit 1
fi

# Run migrations from the new application image.
if ! docker compose -f "$COMPOSE_FILE" run --rm --no-deps \
  "$(service_for_color "$NEW_COLOR")" \
  python manage.py migrate --noinput; then
  set_image_tag "$NEW_TAG_VAR" "$OLD_TAG"
  echo "ERROR: migration failed; live traffic was not switched."
  exit 1
fi

# Start the inactive environment.
if ! docker compose -f "$COMPOSE_FILE" up -d \
  "$(service_for_color "$NEW_COLOR")"; then
  set_image_tag "$NEW_TAG_VAR" "$OLD_TAG"
  echo "ERROR: new environment could not start."
  exit 1
fi

# Test the new application directly before switching traffic.
if ! health_check "http://127.0.0.1:${NEW_PORT}/health/" 12; then
  set_image_tag "$NEW_TAG_VAR" "$OLD_TAG"
  echo "ERROR: new environment is unhealthy; old traffic remains active."
  exit 1
fi

# Switch traffic to the new environment.
if ! switch_upstream "$NEW_PORT"; then
  rollback
  exit 1
fi

# Verify the actual public route.
if ! health_check "$PUBLIC_HEALTH_URL" 12; then
  rollback
  exit 1
fi

printf '%s\n' "$NEW_COLOR" > "$ACTIVE_FILE"

echo "Deployment successful: ${NEW_COLOR} (${NEW_TAG})"
echo "Public health check passed."

```

### Script ব্যবহারের আগে যে পরিবর্তনগুলো করবেন

- `api.example.com` নিজের domain দিয়ে বদলান।
- `active-color` ফাইলে বর্তমানে traffic যে color-এ যাচ্ছে সেটি লিখুন—`blue` বা `green`।
- `.env`-এ উভয় image tag সঠিক আছে কি না দেখুন।
- `deploy` user-কে Nginx configuration install, `nginx -t` ও reload করার জন্য সীমিত sudo permission দিন।
- Script-টি staging-এ পরীক্ষা করুন; প্রথমে public traffic switch না করে নতুন color-এর health check আলাদাভাবে যাচাই করুন।

শুরুতে `active-color` ফাইল তৈরি করার উদাহরণ:

```
printf 'blue\n' | sudo tee /opt/complete-auth-project/active-color
sudo chown deploy:deploy /opt/complete-auth-project/active-color
```

এটি কেবল তখনই করুন যখন Nginx সত্যিই Blue port `8001`-এ traffic পাঠাচ্ছে।

### এই script-এর সীমাবদ্ধতা

এটি শিক্ষামূলক baseline, সম্পূর্ণ race-safe production deployment controller নয়। একসঙ্গে দুটি deployment চললে `.env`, Nginx config ও `active-color`-এর ওপর conflict হতে পারে। Production-এ deployment lock (যেমন `flock`), structured logging, migration compatibility checks এবং failure recovery-কে আরও শক্ত করতে হবে।

এছাড়া `docker compose run --rm --no-deps` migration চালানোর সময় service-এর environment ও database network সঠিকভাবে উপলব্ধ থাকতে হবে। Production-এ migration-এর জন্য আলাদা one-shot service বা deployment command ব্যবহার করা আরও পরিষ্কার হতে পারে।

## 7. Rollback verification — শুধু switch করলেই শেষ নয়

Rollback-এর পরে তিনটি বিষয় নিশ্চিত করতে হবে:

1. Nginx পুরোনো application port-এ request পাঠাচ্ছে।
2. Public health endpoint আবার সফল response দিচ্ছে।
3. পুরোনো release-এর version সত্যিই চালু আছে।

এখনকার `/health/` endpoint শুধু database connection পরীক্ষা করে। তাই আরও একটি version endpoint যোগ করা উপকারী।

ফাইল: `config/health.py`-এ যোগ করুন:

```
import osfrom django.http import JsonResponsefrom django.views.decorators.http import require_GET@require_GETdef version_check(request):    return JsonResponse({        "status": "ok",        "version": os.environ.get("RELEASE_VERSION", "unknown"),    })
```

`config/urls.py`-এ যোগ করুন:

```
path("health/version/", version_check, name="version-check"),
```

Compose-এ দুই application service-এর জন্য environment variable যোগ করুন:

```
environment:
  DJANGO_SETTINGS_MODULE: config.settings
  RELEASE_VERSION: ${IMAGE_TAG_BLUE}
```

Blue service-এ `RELEASE_VERSION` হবে `${IMAGE_TAG_BLUE}` এবং Green service-এ `${IMAGE_TAG_GREEN}`। আলাদা service-এ আলাদা value দিতে হবে।

এখন direct endpoint দিয়ে version যাচাই করা যাবে:

```
curl -s http://127.0.0.1:8001/health/version/
curl -s http://127.0.0.1:8002/health/version/
```

Rollback script-এ public health check-এর পাশাপাশি `/health/version/`-ও যাচাই করুন। এতে আগের image-এর tag প্রত্যাশিত কি না বোঝা যাবে।

আরেকটি গুরুত্বপূর্ণ পার্থক্য: version endpoint-এ image tag দেখানো operational debugging-এর জন্য উপকারী, কিন্তু sensitive commit metadata বা deployment secrets প্রকাশ করবেন না। Public endpoint-এ version প্রকাশ করা আপনার threat model অনুযায়ী সীমিত করা যেতে পারে।

## 8. Health monitoring: deployment-এর বাইরেও নজরদারি

Deployment-এর সময় health check করা যথেষ্ট নয়। Application কয়েক ঘণ্টা বা কয়েক দিন পরে database connection হারাতে পারে, disk পূর্ণ হতে পারে, অথবা Nginx error দিতে পারে।

Production monitoring-এর ন্যূনতম স্তর:

- Application: `/health/` ও error logs।
- Database: connection availability, disk usage, backup status।
- Container: restart count, CPU ও memory।
- Nginx: `5xx` response, upstream errors, TLS expiry।
- External monitoring: VPS-এর বাইরে থেকে public HTTPS endpoint পরীক্ষা।

### সহজ health monitor script

ফাইল: `/usr/local/bin/auth-api-health-check.sh`

```
#!/usr/bin/env bash
set -u

URL="https://api.example.com/health/"
LOG="/var/log/auth-api-health.log"

if curl --fail --silent --show-error \
  --max-time 10 "$URL" >/dev/null; then
  echo "$(date -Is) OK" >> "$LOG"
  exit 0
fi

echo "$(date -Is) FAIL" >> "$LOG"
exit 1
```

এই script log-এ শুধু ফলাফল রাখে; এটি নিজে থেকে restart বা rollback করে না। Permission সীমিত রাখুন এবং log rotation configure করুন।

Production-এ এটি `systemd timer` বা monitoring platform দিয়ে নিয়মিত চালানো যায়। উদাহরণস্বরূপ, প্রতি মিনিটে check করার systemd timer:

ফাইল: `/etc/systemd/system/auth-api-health-check.service`

```
[Unit]
Description=Check Authentication API health

[Service]
Type=oneshot
ExecStart=/usr/local/bin/auth-api-health-check.sh
```

ফাইল: `/etc/systemd/system/auth-api-health-check.timer`

```
[Unit]
Description=Run Authentication API health check periodically

[Timer]
OnBootSec=30s
OnUnitActiveSec=60s
Unit=auth-api-health-check.service

[Install]
WantedBy=timers.target
```

Enable করুন:

```
sudo systemctl daemon-reload
sudo systemctl enable --now auth-api-health-check.timer
systemctl list-timers auth-api-health-check.timer
```

এই basic monitor failure log করবে, কিন্তু alert পাঠাবে না। Production-এ repeated failures, latency, resource usage ও backup failures-এর জন্য alerting threshold নির্ধারণ করুন। Public health endpoint-এ database error-এর বিস্তারিত প্রকাশ না করে শুধু status ফেরত দিন।

## 9. Deployment notifications — Slack-এ success/failure alert

GitHub Actions থেকে deployment status notification পাঠাতে পারেন। নিচে Slack Incoming Webhook-এর উদাহরণ দেওয়া হলো।

প্রথমে GitHub repository-তে `SLACK_WEBHOOK_URL` নামে একটি Actions secret যোগ করুন। Webhook URL-টি secret হিসেবেই রাখবেন।

Workflow-এ job-গুলোর শেষে এই notification job যোগ করুন:

ফাইল: `.github/workflows/ci.yml`

```

  notify:
    name: Deployment notification
    needs: [test, build-and-deploy]
    if: always()
    runs-on: ubuntu-latest
    permissions:
      contents: read

    steps:
      - name: Send Slack notification
        env:
          SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
          TEST_RESULT: ${{ needs.test.result }}
          DEPLOY_RESULT: ${{ needs.build-and-deploy.result }}
          BRANCH: ${{ github.ref_name }}
          COMMIT_SHA: ${{ github.sha }}
        run: |
          if [ -z "$SLACK_WEBHOOK_URL" ]; then
            echo "Slack webhook not configured; skipping notification."
            exit 0
          fi

          MESSAGE="Authentication CI: test=${TEST_RESULT}, deploy=${DEPLOY_RESULT}, branch=${BRANCH}, commit=${COMMIT_SHA}"

          python -c 'import json, os; print(json.dumps({"text": os.environ["MESSAGE"]}))' \
            > /tmp/slack-payload.json

          curl --fail --silent --show-error \
            --request POST \
            --header "Content-Type: application/json" \
            --data @/tmp/slack-payload.json \
            "$SLACK_WEBHOOK_URL"
        env:
          SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
          TEST_RESULT: ${{ needs.test.result }}
          DEPLOY_RESULT: ${{ needs.build-and-deploy.result }}
          BRANCH: ${{ github.ref_name }}
          COMMIT_SHA: ${{ github.sha }}
          MESSAGE: Authentication CI: test=${{ needs.test.result }}, deploy=${{ needs.build-and-deploy.result }}, branch=${{ github.ref_name }}, commit=${{ github.sha }}

```

YAML correction: একই step-এ `env:` দুবার দেওয়া যাবে না। উপরের উদাহরণে একটি মাত্র `env:` block রাখবেন। সঠিক সম্পূর্ণ step-টি হলো:

```

      - name: Send Slack notification
        env:
          SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
          TEST_RESULT: ${{ needs.test.result }}
          DEPLOY_RESULT: ${{ needs.build-and-deploy.result }}
          BRANCH: ${{ github.ref_name }}
          COMMIT_SHA: ${{ github.sha }}
        run: |
          if [ -z "$SLACK_WEBHOOK_URL" ]; then
            echo "Slack webhook not configured; skipping notification."
            exit 0
          fi

          export MESSAGE="Authentication CI: test=${TEST_RESULT}, deploy=${DEPLOY_RESULT}, branch=${BRANCH}, commit=${COMMIT_SHA}"

          python -c 'import json, os; print(json.dumps({"text": os.environ["MESSAGE"]}))' \
            > /tmp/slack-payload.json

          curl --fail --silent --show-error \
            --request POST \
            --header "Content-Type: application/json" \
            --data @/tmp/slack-payload.json \
            "$SLACK_WEBHOOK_URL"

```

এই notification job `always()`-এর কারণে আগের job fail বা skip হলেও চলবে। তবে notification-টি GitHub Actions job-এর ফলাফল জানায়; VPS-এ deploy script rollback করেছে কি না, সেটি আলাদা deployment result হিসেবে report করতে চাইলে script-এর exit code ও logs-এর সঙ্গে সেই তথ্য যুক্ত করতে হবে।

## 10. একসঙ্গে একাধিক deployment ঠেকানো

দুটি workflow একই সময়ে চালু হলে দুটোই `.env`, active color এবং Nginx upstream বদলানোর চেষ্টা করতে পারে। তাই GitHub Actions-এ concurrency group ব্যবহার করুন:

```
concurrency:
  group: authentication-production
  cancel-in-progress: false
```

এটি workflow-level configuration হিসেবে `on:`-এর পরে top-level-এ রাখুন। একই group-এর overlapping runs-কে serialise করতে এটি সাহায্য করে। Server-side-এও deployment lock রাখুন, কারণ SSH দিয়ে manual deployment বা অন্য workflow একই সময় চলতে পারে।

VPS script-এর শুরুতে `flock`-এর মতো lock ব্যবহার করা যায়:

```
exec 9>/var/lock/auth-api-deploy.lock
flock -n 9 || {
  echo "Another deployment is already running."
  exit 1
}
```

Lock file তৈরি ও ব্যবহার করার অনুমতি deployment user-এর থাকতে হবে। `/var/lock`-এ permission সমস্যা হলে একটি নির্দিষ্ট writable deployment directory-তে lock রাখুন।

## 11. Deployment workflow-এর শেষ verification

Production traffic switch করার আগে নতুন environment-এর জন্য নিচের checks চালানো উচিত:

```
# Blue ও Green container status
docker compose -f compose.prod.yaml ps

# Application logs
docker compose -f compose.prod.yaml logs --tail=100 app-blue
docker compose -f compose.prod.yaml logs --tail=100 app-green

# Direct health checks
curl -i http://127.0.0.1:8001/health/
curl -i http://127.0.0.1:8002/health/

# Public health check
curl -i https://api.example.com/health/

# Nginx configuration
sudo nginx -t
```

Deployment script-এ image tag, active color, public health check এবং rollback status log করতে হবে। কোনো failure হলে deploy job non-zero exit status ফেরত দেবে, যাতে GitHub Actions-এ release-টি failed হিসেবে দেখা যায়।

## 12. Zero-downtime deployment-এর সীমাবদ্ধতা

Blue-Green পদ্ধতি downtime-এর ঝুঁকি কমায়, কিন্তু কিছু বিষয় আলাদা করে বিবেচনা করতে হবে:

- Database migration: destructive migration করলে পুরোনো release আর কাজ নাও করতে পারে।
- Long-running requests: Nginx reload-এর পরও পুরোনো worker-এর request চলতে পারে।
- Session ও cache: Redis বা shared cache-এর schema/data format দুই version-এর সঙ্গে compatible হতে হবে।
- Background workers: Celery worker বা scheduled jobs-এর duplicate execution ঠেকাতে হবে।
- Static files ও media: release switch-এর সঙ্গে assets ও uploaded files সামঞ্জস্যপূর্ণ রাখতে হবে।
- Deployment failure: rollback শুধু পুরোনো image চালু করলেই সম্পূর্ণ হয় না; database ও external dependencies-ও সুস্থ থাকতে হবে।

সুতরাং production-এ প্রথমে staging environment-এ deploy, rollback, migration failure এবং health-check failure অনুশীলন করুন।

## 13. Lesson 13 practical checklist

### Production readiness

0/10

Blue ও Green-এর জন্য আলাদা container এবং port configure করেছি

Nginx upstream দিয়ে traffic switch কাজ করে

নতুন environment live traffic নেওয়ার আগে health check pass করে

Migration backward-compatible কি না review করেছি

Health check fail হলে rollback attempt হয়

Rollback-এর পরে পুরোনো release-এর health ও version যাচাই হয়

একসঙ্গে একাধিক deployment আটকানোর ব্যবস্থা আছে

External health monitoring চালু করেছি

Deployment success/failure notification কাজ করে

Staging-এ failure scenarios পরীক্ষা করেছি

&#x20;Copy checklist

## Lesson 13-এর সারাংশ

আজ আমরা Docker Compose-এর ওপর Blue-Green deployment architecture, Nginx traffic switching, database migration compatibility, rollback verification, health monitoring এবং Slack notification-এর ভিত্তি তৈরি করেছি।

Production deployment-এ সবচেয়ে গুরুত্বপূর্ণ নিয়মটি হলো: নতুন release healthy এবং compatible প্রমাণিত না হওয়া পর্যন্ত পুরোনো release ও database recovery path সংরক্ষণ করতে হবে।

পরবর্তী Lesson 14-এ আমরা চাইলে আরও গভীরে যেতে পারি: Production Observability — structured logging, Sentry error tracking, Prometheus/Grafana metrics, PostgreSQL backup automation এবং disaster recovery drill।

----
# Lesson 14: Production Observability — Django REST Framework

এই Lesson-এ আমাদের `complete_auth_project` authentication API-কে production monitoring ও recovery-এর জন্য প্রস্তুত করব। শুধু API চালু থাকলেই production-ready হয় না—API কেন ব্যর্থ হচ্ছে, কত সময় নিচ্ছে, database সুস্থ কি না, এবং server নষ্ট হলে data কীভাবে ফিরিয়ে আনব, সেগুলোও জানতে হবে।

## এই Lesson শেষে যা তৈরি হবে

1\. Structured logging

Application error, request, status code ও latency-র লগ—যাতে সমস্যা দ্রুত খুঁজে পাওয়া যায়।

2\. Sentry error tracking

Production-এ unexpected exception হলে stack trace ও error context সংগ্রহ করা।

3\. Prometheus + Grafana

Request rate, error rate, latency ও database-related health metrics পর্যবেক্ষণ।

4\. PostgreSQL backup automation

নিয়মিত backup, retention policy এবং backup থেকে বাস্তবে restore পরীক্ষা।

## 1. Production architecture

Client / Frontend

HTTPS request

Nginx → Gunicorn → Django REST Framework

Authentication API + application logs

Sentry

Exceptions ও stack traces

PostgreSQL

Application data + backups

Prometheus → Grafana

Metrics সংগ্রহ → Dashboard ও alert

গুরুত্বপূর্ণ পার্থক্য: Logging বলে কী ঘটেছে; Sentry exception-এর কারণ খুঁজতে সাহায্য করে; Prometheus সময়ের সঙ্গে system metrics সংগ্রহ করে; Grafana সেই metrics দৃশ্যমান করে। Backup ও restore হলো data recovery-এর আলাদা ব্যবস্থা।

## 2. Project structure

আমাদের আগের Django project-এর মধ্যে নতুন observability files যোগ হবে।

```
complete_auth_project/
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── observability.py
├── accounts/
├── deploy/
│   ├── backup-postgres.sh
│   └── restore-drill.sh
├── docker-compose.yml
├── requirements.txt
└── .env
```

এখানে `observability.py` logging configuration-এর জন্য; backup scripts server-side deployment directory-তে চলবে। তোমার existing project-এ আলাদা নাম বা folder থাকলে সেই অনুযায়ী path সমন্বয় করবে।

## 3. Structured logging তৈরি করা

### ধাপ 1 — Django logging configuration

Django-এর built-in `logging` ব্যবহার করব। লগ JSON format-এ থাকবে, ফলে পরে log collector দিয়ে filter করা সহজ হবে।

`config/observability.py`

```
import jsonimport loggingfrom datetime import datetime, timezoneclass JSONFormatter(logging.Formatter):    def format(self, record):        payload = {            "timestamp": datetime.now(timezone.utc).isoformat(),            "level": record.levelname,            "logger": record.name,            "message": record.getMessage(),        }        if record.exc_info:            payload["exception"] = self.formatException(                record.exc_info            )        if hasattr(record, "status_code"):            payload["status_code"] = record.status_code        if hasattr(record, "duration_ms"):            payload["duration_ms"] = record.duration_ms        return json.dumps(payload, ensure_ascii=False)
```

এই formatter সাধারণ message এবং exception-কে JSON-এ রূপান্তর করে। `duration_ms` বা `status_code`-এর মতো custom fields থাকলে সেগুলোও যোগ হবে।

### ধাপ 2 — `settings.py`-তে configuration

`config/settings.py`-এর শেষে যোগ করো:

```
LOGGING = {    "version": 1,    "disable_existing_loggers": False,    "formatters": {        "json": {            "()": "config.observability.JSONFormatter",        },    },    "handlers": {        "console": {            "class": "logging.StreamHandler",            "formatter": "json",        },    },    "root": {        "handlers": ["console"],        "level": "INFO",    },    "loggers": {        "django": {            "handlers": ["console"],            "level": "INFO",            "propagate": False,        },        "accounts": {            "handlers": ["console"],            "level": "INFO",            "propagate": False,        },    },}
```

Docker-এর মধ্যে console logging সুবিধাজনক, কারণ লগ `docker compose logs` দিয়ে দেখা যায়। Host-এর disk-এ আলাদা log file লিখলে rotation এবং disk-space management-ও করতে হবে।

### ধাপ 3 — নিজের application log লেখা

যে কোনো service বা view-তে:

```
import logginglogger = logging.getLogger("accounts")def example_auth_event(user_id):    logger.info(        "Authentication event processed",        extra={            "user_id": user_id,            "event": "authentication_processed",        },    )
```

`extra`-এর fields এই মুহূর্তের formatter-এ স্বয়ংক্রিয়ভাবে output হবে না, কারণ formatter শুধু নির্দিষ্ট fields সংগ্রহ করছে। সেগুলোও JSON-এ রাখতে চাইলে formatter-কে allowlisted fields যোগ করে আপডেট করতে হবে।

Security rule: Password, JWT access/refresh token, OTP, password-reset token, authorization header বা email verification token কখনো log করবে না। Production log-এ ব্যক্তিগত তথ্যও অপ্রয়োজনীয়ভাবে রাখবে না।

## 4. Request latency ও status code log করা

প্রতিটি request কত সময় নিচ্ছে এবং কী status code দিচ্ছে তা দেখতে middleware ব্যবহার করা যায়।

`config/middleware.py`

```
import loggingimport timefrom django.utils.deprecation import MiddlewareMixinlogger = logging.getLogger("accounts")class RequestObservabilityMiddleware(MiddlewareMixin):    def process_request(self, request):        request.observability_started_at = time.perf_counter()    def process_response(self, request, response):        started_at = getattr(            request,            "observability_started_at",            None,        )        if started_at is not None:            duration_ms = round(                (time.perf_counter() - started_at) * 1000,                2,            )            logger.info(                "HTTP request completed",                extra={                    "status_code": response.status_code,                    "duration_ms": duration_ms,                    "method": request.method,                    "path": request.path,                },            )        return response
```

এবার `config/settings.py`-এর `MIDDLEWARE` list-এ যোগ করো:

```
MIDDLEWARE = [    # Existing middleware...    "config.middleware.RequestObservabilityMiddleware",]
```

এটিকে সাধারণত middleware list-এর নিচের দিকে রাখলে view processing-এর সময়সহ request latency মাপা যায়। তবে middleware order-এর কারণে response-এ অন্য middleware-এর পরিবর্তন বা processing এই পরিমাপে সব সময় অন্তর্ভুক্ত হবে না।

`/api/auth/login/`-এর মতো endpoint-এর request body log করবে না। Path-এ user ID, email বা reset token থাকার সম্ভাবনা থাকলে raw path-এর বদলে route name বা sanitized path log করা ভালো।

## 5. Sentry দিয়ে production exception tracking

Sentry application exception সংগ্রহ করতে পারে, যাতে server-এ SSH করে শুধু log পড়ার ওপর নির্ভর করতে না হয়।

### ধাপ 1 — Package install

```
pip install "sentry-sdk[django]"
```

`requirements.txt`-এ package dependency সংরক্ষণ করো।

### ধাপ 2 — Environment variable

Production `.env`-এ:

```
SENTRY_DSN=https://your-project-key@example.ingest.sentry.io/your-project-id
SENTRY_TRACES_SAMPLE_RATE=0.05
```

এটি একটি উদাহরণ। Sentry project তৈরি করে তার আসল DSN ব্যবহার করতে হবে। DSN সাধারণত ingest-এর জন্য ব্যবহৃত হয়, কিন্তু এটিকে private credential ধরে অনিরাপদভাবে প্রকাশ না করাই ভালো।

### ধাপ 3 — `settings.py`-তে initialization

```
import osimport sentry_sdkfrom sentry_sdk.integrations.django import DjangoIntegrationSENTRY_DSN = os.getenv("SENTRY_DSN", "")if SENTRY_DSN:    sentry_sdk.init(        dsn=SENTRY_DSN,        integrations=[DjangoIntegration()],        traces_sample_rate=float(            os.getenv("SENTRY_TRACES_SAMPLE_RATE", "0.05")        ),        send_default_pii=False,    )
```

এখানে `0.05` মানে performance tracing-এর জন্য প্রায় ৫% transaction sample করার configuration। এটি error capture-এর ৫% limit নয়। Traffic, cost ও privacy অনুযায়ী sampling rate ঠিক করবে।

### ধাপ 4 — Production checklist

- Sentry dashboard-এ project তৈরি করো।
- Development ও production-এর environment আলাদা রাখো।
- Error event-এ password, token বা sensitive request data যাচ্ছে কি না পরীক্ষা করো।
- শুধু error capture-এর জন্য ইচ্ছাকৃতভাবে production endpoint-এ exception তৈরি করবে না; staging-এ controlled test করো।
- Django-এর expected validation errors সাধারণত 400 response হিসেবে ফেরে; প্রতিটি 400-কে server failure মনে করা যাবে না।

## 6. Prometheus + Grafana metrics

এখন application-এর request metrics সংগ্রহ করব।

### ধাপ 1 — Django Prometheus package

```
pip install django-prometheus
```

`requirements.txt`-এ যোগ করো:

```
django-prometheus
```

### ধাপ 2 — `INSTALLED_APPS` ও middleware

`config/settings.py`-তে:

```
INSTALLED_APPS = [    "django_prometheus",    # Existing apps...]
```

`MIDDLEWARE` list-এ metrics middleware যুক্ত করো:

```
MIDDLEWARE = [    "django_prometheus.middleware.PrometheusBeforeMiddleware",    # Existing middleware...    "django_prometheus.middleware.PrometheusAfterMiddleware",]
```

`PrometheusBeforeMiddleware` প্রথমে এবং `PrometheusAfterMiddleware` শেষে রাখবে। আগের custom request logging middleware-ও রাখতে পারো।

### ধাপ 3 — Metrics URL

`config/urls.py`:

```
from django.urls import include, pathurlpatterns = [    # Existing API routes...    path("", include("django_prometheus.urls")),]
```

সাধারণ configuration-এ metrics endpoint হবে `/metrics`; exact path package configuration অনুযায়ী যাচাই করবে।

অত্যন্ত গুরুত্বপূর্ণ: `/metrics` public Internet-এ উন্মুক্ত রেখো না। এতে infrastructure ও traffic pattern সম্পর্কে তথ্য প্রকাশ হতে পারে। Nginx বা firewall দিয়ে internal network/IP allowlist-এ সীমাবদ্ধ রাখবে।

### ধাপ 4 — Prometheus configuration

Project-এর `deploy/prometheus.yml` তৈরি করো:

```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "auth-api"
    metrics_path: "/metrics"
    static_configs:
      - targets: ["web:8000"]
```

এখানে `web:8000` তখনই কাজ করবে যখন Prometheus এবং Django container একই Docker network-এ থাকবে এবং `web` সঠিক Compose service name হবে। Blue-green setup-এ service name আলাদা হলে সেই অনুযায়ী targets বদলাতে হবে।

### ধাপ 5 — Docker Compose-এ Prometheus

```
services:
  prometheus:
    image: prom/prometheus
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"
    volumes:
      - ./deploy/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    networks:
      - monitoring
      - app_internal
    restart: unless-stopped

volumes:
  prometheus_data:

networks:
  monitoring:
  app_internal:
```

এটি বিদ্যমান `docker-compose.yml`-এর service/volume/network configuration-এর সঙ্গে merge করার উদাহরণ—পুরো Compose file হিসেবে সরাসরি replace করবে না। `app_internal` network-টি তোমার Django service-এও থাকতে হবে। Production-এ image version pin করো এবং metrics endpoint internal-only রাখো।

### ধাপ 6 — Grafana

Grafana-কে একই monitoring network-এ চালাও। Grafana UI-তে Prometheus data source যোগ করার সময় URL হিসেবে সাধারণত `http://prometheus:9090` ব্যবহার করা যায়, যদি দুটো একই Docker network-এ থাকে।

প্রাথমিক dashboard-এ এই metrics রাখো:

- HTTP request rate
- 5xx error rate
- p95/p99 request latency
- Django process/resource usage—প্রযোজ্য exporter থাকলে
- Database availability ও connection saturation—প্রযোজ্য PostgreSQL exporter থাকলে

শুধু `django-prometheus` যোগ করলেই PostgreSQL-এর সব operational metric পাওয়া যাবে না। PostgreSQL-এর connections, locks, replication lag, disk usage ইত্যাদির জন্য PostgreSQL exporter বা database monitoring আলাদাভাবে configure করতে হবে।

## 7. PostgreSQL backup automation

Monitoring থাকলেও database data হারিয়ে গেলে সমস্যা হতে পারে। তাই backup তৈরি, নিরাপদে সংরক্ষণ এবং restore পরীক্ষা—তিনটিই দরকার।

### ধাপ 1 — Backup script

Production server-এর deployment directory-তে `deploy/backup-postgres.sh` তৈরি করো:

```
#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete_auth_project"
BACKUP_DIR="/var/backups/auth-api/postgres"
TIMESTAMP="$(date -u +'%Y-%m-%dT%H-%M-%SZ')"
BACKUP_FILE="${BACKUP_DIR}/auth_${TIMESTAMP}.dump"

cd "$APP_DIR"

install -d -m 700 "$BACKUP_DIR"
umask 077

echo "Starting PostgreSQL backup: $TIMESTAMP"

docker compose exec -T db sh -c \
  'pg_dump -U "$POSTGRES_USER" -d "$POSTGRES_DB" -Fc' \
  > "$BACKUP_FILE"

if [[ ! -s "$BACKUP_FILE" ]]; then
    echo "ERROR: Backup file is empty."
    rm -f "$BACKUP_FILE"
    exit 1
fi

# Validate that the archive can be read.
docker compose exec -T db sh -c \
  'pg_restore --list' < "$BACKUP_FILE" > /dev/null

echo "Backup created: $BACKUP_FILE"

# Keep local backups for 14 days.
find "$BACKUP_DIR" \
  -type f \
  -name 'auth_*.dump' \
  -mtime +14 \
  -delete

echo "Backup job completed."
```

এখানে `db`, `POSTGRES_USER` ও `POSTGRES_DB` তোমার Compose configuration-এর সঙ্গে মিলতে হবে। `pg_dump -Fc` PostgreSQL-এর custom archive format তৈরি করে; `pg_restore` দিয়ে সেটি restore করা যায়।

Script executable করো:

```
chmod 700 deploy/backup-postgres.sh
```

তারপর staging বা test server-এ চালিয়ে যাচাই করো:

```
sudo ./deploy/backup-postgres.sh
```

সতর্কতা: `-mtime +14` দিয়ে ১৪ দিনের বেশি পুরোনো local backup মুছে ফেলা হবে। এই local retention-এর পাশাপাশি আলাদা off-site backup না থাকলে server বা disk নষ্ট হওয়ার পর সব backup হারাতে পারো।

### ধাপ 2 — Backup security

Production backup-এ user account, email এবং অন্যান্য ব্যক্তিগত তথ্য থাকতে পারে। তাই:

- Backup directory-র permission সীমিত রাখবে।
- Backup encrypted storage-এ পাঠাবে; যেমন encrypted object storage বা appropriately configured encrypted backup remote।
- Encryption key এবং storage credentials database server-এর একই disk-এ শুধু একটি copy হিসেবে রাখবে না।
- সফল backup-এর পাশাপাশি off-site upload-এর সফলতাও যাচাই করবে।
- Retention policy অনুযায়ী local ও remote copy আলাদাভাবে পরিচালনা করবে।

### ধাপ 3 — প্রতিদিন স্বয়ংক্রিয় backup

Ubuntu server-এ systemd timer ব্যবহার করতে পারো।

`/etc/systemd/system/auth-api-backup.service`

```
[Unit]
Description=Authentication API PostgreSQL backup

[Service]
Type=oneshot
ExecStart=/opt/complete_auth_project/deploy/backup-postgres.sh
```

`/etc/systemd/system/auth-api-backup.timer`

```
[Unit]
Description=Daily authentication database backup

[Timer]
OnCalendar=*-*-* 02:00:00 UTC
Persistent=true

[Install]
WantedBy=timers.target
```

সক্রিয় করো:

```
sudo systemctl daemon-reload
sudo systemctl enable --now auth-api-backup.timer

systemctl list-timers auth-api-backup.timer
```

Log দেখার জন্য:

```
sudo journalctl -u auth-api-backup.service
```

Production-এ backup script কোন Unix user হিসেবে চলবে, সে user-এর Docker access ও backup-directory permission আগে ঠিক করতে হবে। Docker group access-কে root-সদৃশ privilege হিসেবে বিবেচনা করো; সম্ভব হলে dedicated backup account ও সীমিত permissions ব্যবহার করো।

## 8. Disaster recovery drill — backup সত্যিই restore হয় কি না?

Backup file তৈরি হওয়া মানেই recovery সম্ভব—এটি নিশ্চিত নয়। Archive corrupt হতে পারে, credentials ভুল হতে পারে অথবা schema/data অসম্পূর্ণ থাকতে পারে। তাই আলাদা test database-এ restore করতে হবে।

Production database-এ পরীক্ষা করবে না

Restore drill-এর জন্য disposable database ব্যবহার করো। নিচের উদাহরণে `auth_restore_drill` নামে একটি পৃথক database তৈরি করা হবে। এটি আগে থেকে থাকলে নাম পরিবর্তন করো বা আগের test database মুছে ফেলার আগে তার data সত্যিই disposable কি না যাচাই করো।

### ধাপ 1 — Restore drill script

`deploy/restore-drill.sh`:

```
#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete_auth_project"
BACKUP_FILE="${1:?Usage: restore-drill.sh /path/to/backup.dump}"
TEST_DB="auth_restore_drill"

cd "$APP_DIR"

if [[ ! -r "$BACKUP_FILE" ]]; then
    echo "ERROR: Cannot read backup file."
    exit 1
fi

echo "Creating isolated test database: $TEST_DB"

docker compose exec -T db sh -c \
  'createdb -U "$POSTGRES_USER" auth_restore_drill'

echo "Restoring backup into test database..."

docker compose exec -T db sh -c \
  'pg_restore -U "$POSTGRES_USER" \
    -d auth_restore_drill \
    --no-owner --no-privileges' \
  < "$BACKUP_FILE"

echo "Checking restored database..."

docker compose exec -T db sh -c \
  'psql -v ON_ERROR_STOP=1 \
    -U "$POSTGRES_USER" \
    -d auth_restore_drill \
    -c "SELECT COUNT(*) FROM django_migrations;"'

echo "Restore completed. Verify tables and critical application data."
echo "Do not delete the test database until verification is complete."
```

এরপর:

```
chmod 700 deploy/restore-drill.sh

sudo ./deploy/restore-drill.sh \
  /var/backups/auth-api/postgres/auth_YYYY-MM-DDTHH-MM-SSZ.dump
```

`YYYY-MM-DDTHH-MM-SSZ`-এর জায়গায় বাস্তব backup filename বসাবে।

এই script-এর শেষের query একটি প্রাথমিক smoke test মাত্র। তোমার database-এ `django_migrations` table থাকা দরকার; পুরোনো বা অসম্পূর্ণ backup হলে query ব্যর্থ হতে পারে। Restore সফল হলে আরও যাচাই করবে:

1. প্রত্যাশিত tables ও migrations আছে কি না।
2. User record এবং গুরুত্বপূর্ণ application data-এর যুক্তিসংগত সংখ্যা আছে কি না।
3. Foreign key ও গুরুত্বপূর্ণ constraints ঠিক আছে কি না।
4. Staging configuration দিয়ে application ওই restored database পড়তে পারছে কি না।
5. Restore করতে কত সময় লাগল, সেটি লিখে রাখবে।

সতর্কতা: `--no-owner --no-privileges` ব্যবহার করলে archive-এর owner ও privilege restoration বাদ যায়। Recovery environment-এ প্রয়োজনীয় database roles ও permissions আলাদাভাবে প্রস্তুত করতে হবে।

### ধাপ 2 — Recovery objective ঠিক করা

দুটি গুরুত্বপূর্ণ production ধারণা:

- RPO (Recovery Point Objective): সর্বোচ্চ কত সময়ের data হারানো গ্রহণযোগ্য?
- RTO (Recovery Time Objective): কত সময়ের মধ্যে service পুনরুদ্ধার করতে হবে?

উদাহরণস্বরূপ, যদি RPO এক ঘণ্টা হয়, তাহলে প্রতিদিন একবার backup যথেষ্ট নয়। সে ক্ষেত্রে আরও ঘন backup, WAL archiving এবং point-in-time recovery (PITR) পরিকল্পনা বিবেচনা করতে হবে।

## 9. Monitoring alert: কখন ব্যবস্থা নিতে হবে?

Dashboard শুধু দেখার জন্য নয়; কোনো সমস্যা হলে notification-ও দরকার। শুরুতে এই alert conditions পরিকল্পনা করতে পারো:

| Alert                | উদাহরণ condition                 | কী পরীক্ষা করবে                    |
| -------------------- | -------------------------------- | ---------------------------------- |
| API errors           | 5xx rate স্বাভাবিকের চেয়ে বেশি  | Django logs, Sentry                |
| High latency         | p95 latency 1 সেকেন্ডের বেশি     | Slow queries, workers, network     |
| API unavailable      | Health endpoint বারবার ব্যর্থ    | Gunicorn, container, Nginx         |
| Database unavailable | PostgreSQL health check ব্যর্থ   | DB logs, disk, connections         |
| Backup failure       | Backup বা off-site upload ব্যর্থ | systemd logs, credentials, storage |
| Disk nearly full     | Disk usage 85% ছাড়িয়েছে        | Logs, backups, database storage    |

এই সংখ্যাগুলো উদাহরণমাত্র; প্রকৃত threshold তোমার API traffic ও service requirements অনুযায়ী ঠিক করবে।

Prometheus alerting-এর জন্য Alertmanager যুক্ত করা যায়। Grafana-তেও alert rules ও notification contact points configure করা যায়। যেকোনো একটি ব্যবস্থা বেছে নিলেও backup failure এবং service outage-এর alert যেন dashboard-এর বাইরে পৌঁছায়, তা নিশ্চিত করবে।

## 10. Lesson 14 implementation checklist

## Production readiness

0 / 9

Structured JSON logging

Application logs-এ timestamp, severity, logger ও exception তথ্য দেখা যাচ্ছে।

Request latency logging

HTTP status ও duration log হচ্ছে; sensitive data প্রকাশ পাচ্ছে না।

Sentry

Staging-এ controlled exception capture হচ্ছে এবং event-এ secret নেই।

Prometheus metrics

Metrics scrape হচ্ছে; public Internet থেকে endpoint access বন্ধ।

Grafana dashboard

Request rate, error rate ও latency দেখা যাচ্ছে।

Automated PostgreSQL backup

Scheduled backup সফল হচ্ছে এবং retention কাজ করছে।

Off-site backup

Backup server-এর বাইরের encrypted storage-এ সংরক্ষিত হচ্ছে।

Restore drill

আলাদা database-এ restore করে application data যাচাই করা হয়েছে।

Alerting

API outage, backup failure ও disk-space alert পরীক্ষা করা হয়েছে।

## 11. Final verification commands

Ubuntu VPS-এ এগুলো ব্যবহার করে প্রাথমিক অবস্থা যাচাই করতে পারো:

```
# Running services
docker compose ps

# Application logs
docker compose logs --tail=100 web

# Database logs
docker compose logs --tail=100 db

# Backup timer
systemctl list-timers auth-api-backup.timer

# Latest backup files
sudo ls -lh /var/backups/auth-api/postgres/

# Backup service logs
sudo journalctl -u auth-api-backup.service -n 100

# Nginx configuration
sudo nginx -t

# Disk capacity
df -h
```

এখানে `web` ও `db` তোমার actual Compose service names-এর সঙ্গে মিলিয়ে নেবে। Blue-green deployment-এ `web`-এর বদলে `app-blue` বা `app-green`-এর মতো service name হতে পারে।

## Lesson 14-এর মূল শিক্ষা

Production observability মানে শুধু Grafana dashboard তৈরি করা নয়। একটি সম্পূর্ণ ব্যবস্থা হবে:

- Detect: Logs, Sentry এবং metrics দিয়ে সমস্যা শনাক্ত করা।
- Diagnose: Stack trace, latency ও database health দেখে কারণ বের করা।
- Recover: Tested backup থেকে database restore করা এবং recovery time মাপা।
- Prevent recurrence: Alert, deployment checks এবং incident review দিয়ে একই সমস্যা পুনরায় হওয়ার ঝুঁকি কমানো।

পরের ধাপে আমরা Lesson 15 — Production Security Audit করতে পারি: Django security settings, HTTPS/HSTS, CORS/CSRF, JWT attack scenarios, rate limiting, dependency scanning, container hardening এবং automated security tests—সবকিছু checklist ও বাস্তব code দিয়ে।\

-----
# Lesson 14: Production Observability — Django REST Framework

এই Lesson-এ আমাদের `complete_auth_project` authentication API-কে production monitoring ও recovery-এর জন্য প্রস্তুত করব। শুধু API চালু থাকলেই production-ready হয় না—API কেন ব্যর্থ হচ্ছে, কত সময় নিচ্ছে, database সুস্থ কি না, এবং server নষ্ট হলে data কীভাবে ফিরিয়ে আনব, সেগুলোও জানতে হবে।

## এই Lesson শেষে যা তৈরি হবে

1\. Structured logging

Application error, request, status code ও latency-র লগ—যাতে সমস্যা দ্রুত খুঁজে পাওয়া যায়।

2\. Sentry error tracking

Production-এ unexpected exception হলে stack trace ও error context সংগ্রহ করা।

3\. Prometheus + Grafana

Request rate, error rate, latency ও database-related health metrics পর্যবেক্ষণ।

4\. PostgreSQL backup automation

নিয়মিত backup, retention policy এবং backup থেকে বাস্তবে restore পরীক্ষা।

## 1. Production architecture

Client / Frontend

HTTPS request

Nginx → Gunicorn → Django REST Framework

Authentication API + application logs

Sentry

Exceptions ও stack traces

PostgreSQL

Application data + backups

Prometheus → Grafana

Metrics সংগ্রহ → Dashboard ও alert

গুরুত্বপূর্ণ পার্থক্য: Logging বলে কী ঘটেছে; Sentry exception-এর কারণ খুঁজতে সাহায্য করে; Prometheus সময়ের সঙ্গে system metrics সংগ্রহ করে; Grafana সেই metrics দৃশ্যমান করে। Backup ও restore হলো data recovery-এর আলাদা ব্যবস্থা।

## 2. Project structure

আমাদের আগের Django project-এর মধ্যে নতুন observability files যোগ হবে।

```
complete_auth_project/
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── observability.py
├── accounts/
├── deploy/
│   ├── backup-postgres.sh
│   └── restore-drill.sh
├── docker-compose.yml
├── requirements.txt
└── .env
```

এখানে `observability.py` logging configuration-এর জন্য; backup scripts server-side deployment directory-তে চলবে। তোমার existing project-এ আলাদা নাম বা folder থাকলে সেই অনুযায়ী path সমন্বয় করবে।

## 3. Structured logging তৈরি করা

### ধাপ 1 — Django logging configuration

Django-এর built-in `logging` ব্যবহার করব। লগ JSON format-এ থাকবে, ফলে পরে log collector দিয়ে filter করা সহজ হবে।

`config/observability.py`

```
import jsonimport loggingfrom datetime import datetime, timezoneclass JSONFormatter(logging.Formatter):    def format(self, record):        payload = {            "timestamp": datetime.now(timezone.utc).isoformat(),            "level": record.levelname,            "logger": record.name,            "message": record.getMessage(),        }        if record.exc_info:            payload["exception"] = self.formatException(                record.exc_info            )        if hasattr(record, "status_code"):            payload["status_code"] = record.status_code        if hasattr(record, "duration_ms"):            payload["duration_ms"] = record.duration_ms        return json.dumps(payload, ensure_ascii=False)
```

এই formatter সাধারণ message এবং exception-কে JSON-এ রূপান্তর করে। `duration_ms` বা `status_code`-এর মতো custom fields থাকলে সেগুলোও যোগ হবে।

### ধাপ 2 — `settings.py`-তে configuration

`config/settings.py`-এর শেষে যোগ করো:

```
LOGGING = {    "version": 1,    "disable_existing_loggers": False,    "formatters": {        "json": {            "()": "config.observability.JSONFormatter",        },    },    "handlers": {        "console": {            "class": "logging.StreamHandler",            "formatter": "json",        },    },    "root": {        "handlers": ["console"],        "level": "INFO",    },    "loggers": {        "django": {            "handlers": ["console"],            "level": "INFO",            "propagate": False,        },        "accounts": {            "handlers": ["console"],            "level": "INFO",            "propagate": False,        },    },}
```

Docker-এর মধ্যে console logging সুবিধাজনক, কারণ লগ `docker compose logs` দিয়ে দেখা যায়। Host-এর disk-এ আলাদা log file লিখলে rotation এবং disk-space management-ও করতে হবে।

### ধাপ 3 — নিজের application log লেখা

যে কোনো service বা view-তে:

```
import logginglogger = logging.getLogger("accounts")def example_auth_event(user_id):    logger.info(        "Authentication event processed",        extra={            "user_id": user_id,            "event": "authentication_processed",        },    )
```

`extra`-এর fields এই মুহূর্তের formatter-এ স্বয়ংক্রিয়ভাবে output হবে না, কারণ formatter শুধু নির্দিষ্ট fields সংগ্রহ করছে। সেগুলোও JSON-এ রাখতে চাইলে formatter-কে allowlisted fields যোগ করে আপডেট করতে হবে।

Security rule: Password, JWT access/refresh token, OTP, password-reset token, authorization header বা email verification token কখনো log করবে না। Production log-এ ব্যক্তিগত তথ্যও অপ্রয়োজনীয়ভাবে রাখবে না।

## 4. Request latency ও status code log করা

প্রতিটি request কত সময় নিচ্ছে এবং কী status code দিচ্ছে তা দেখতে middleware ব্যবহার করা যায়।

`config/middleware.py`

```
import loggingimport timefrom django.utils.deprecation import MiddlewareMixinlogger = logging.getLogger("accounts")class RequestObservabilityMiddleware(MiddlewareMixin):    def process_request(self, request):        request.observability_started_at = time.perf_counter()    def process_response(self, request, response):        started_at = getattr(            request,            "observability_started_at",            None,        )        if started_at is not None:            duration_ms = round(                (time.perf_counter() - started_at) * 1000,                2,            )            logger.info(                "HTTP request completed",                extra={                    "status_code": response.status_code,                    "duration_ms": duration_ms,                    "method": request.method,                    "path": request.path,                },            )        return response
```

এবার `config/settings.py`-এর `MIDDLEWARE` list-এ যোগ করো:

```
MIDDLEWARE = [    # Existing middleware...    "config.middleware.RequestObservabilityMiddleware",]
```

এটিকে সাধারণত middleware list-এর নিচের দিকে রাখলে view processing-এর সময়সহ request latency মাপা যায়। তবে middleware order-এর কারণে response-এ অন্য middleware-এর পরিবর্তন বা processing এই পরিমাপে সব সময় অন্তর্ভুক্ত হবে না।

`/api/auth/login/`-এর মতো endpoint-এর request body log করবে না। Path-এ user ID, email বা reset token থাকার সম্ভাবনা থাকলে raw path-এর বদলে route name বা sanitized path log করা ভালো।

## 5. Sentry দিয়ে production exception tracking

Sentry application exception সংগ্রহ করতে পারে, যাতে server-এ SSH করে শুধু log পড়ার ওপর নির্ভর করতে না হয়।

### ধাপ 1 — Package install

```
pip install "sentry-sdk[django]"
```

`requirements.txt`-এ package dependency সংরক্ষণ করো।

### ধাপ 2 — Environment variable

Production `.env`-এ:

```
SENTRY_DSN=https://your-project-key@example.ingest.sentry.io/your-project-id
SENTRY_TRACES_SAMPLE_RATE=0.05
```

এটি একটি উদাহরণ। Sentry project তৈরি করে তার আসল DSN ব্যবহার করতে হবে। DSN সাধারণত ingest-এর জন্য ব্যবহৃত হয়, কিন্তু এটিকে private credential ধরে অনিরাপদভাবে প্রকাশ না করাই ভালো।

### ধাপ 3 — `settings.py`-তে initialization

```
import osimport sentry_sdkfrom sentry_sdk.integrations.django import DjangoIntegrationSENTRY_DSN = os.getenv("SENTRY_DSN", "")if SENTRY_DSN:    sentry_sdk.init(        dsn=SENTRY_DSN,        integrations=[DjangoIntegration()],        traces_sample_rate=float(            os.getenv("SENTRY_TRACES_SAMPLE_RATE", "0.05")        ),        send_default_pii=False,    )
```

এখানে `0.05` মানে performance tracing-এর জন্য প্রায় ৫% transaction sample করার configuration। এটি error capture-এর ৫% limit নয়। Traffic, cost ও privacy অনুযায়ী sampling rate ঠিক করবে।

### ধাপ 4 — Production checklist

- Sentry dashboard-এ project তৈরি করো।
- Development ও production-এর environment আলাদা রাখো।
- Error event-এ password, token বা sensitive request data যাচ্ছে কি না পরীক্ষা করো।
- শুধু error capture-এর জন্য ইচ্ছাকৃতভাবে production endpoint-এ exception তৈরি করবে না; staging-এ controlled test করো।
- Django-এর expected validation errors সাধারণত 400 response হিসেবে ফেরে; প্রতিটি 400-কে server failure মনে করা যাবে না।

## 6. Prometheus + Grafana metrics

এখন application-এর request metrics সংগ্রহ করব।

### ধাপ 1 — Django Prometheus package

```
pip install django-prometheus
```

`requirements.txt`-এ যোগ করো:

```
django-prometheus
```

### ধাপ 2 — `INSTALLED_APPS` ও middleware

`config/settings.py`-তে:

```
INSTALLED_APPS = [    "django_prometheus",    # Existing apps...]
```

`MIDDLEWARE` list-এ metrics middleware যুক্ত করো:

```
MIDDLEWARE = [    "django_prometheus.middleware.PrometheusBeforeMiddleware",    # Existing middleware...    "django_prometheus.middleware.PrometheusAfterMiddleware",]
```

`PrometheusBeforeMiddleware` প্রথমে এবং `PrometheusAfterMiddleware` শেষে রাখবে। আগের custom request logging middleware-ও রাখতে পারো।

### ধাপ 3 — Metrics URL

`config/urls.py`:

```
from django.urls import include, pathurlpatterns = [    # Existing API routes...    path("", include("django_prometheus.urls")),]
```

সাধারণ configuration-এ metrics endpoint হবে `/metrics`; exact path package configuration অনুযায়ী যাচাই করবে।

অত্যন্ত গুরুত্বপূর্ণ: `/metrics` public Internet-এ উন্মুক্ত রেখো না। এতে infrastructure ও traffic pattern সম্পর্কে তথ্য প্রকাশ হতে পারে। Nginx বা firewall দিয়ে internal network/IP allowlist-এ সীমাবদ্ধ রাখবে।

### ধাপ 4 — Prometheus configuration

Project-এর `deploy/prometheus.yml` তৈরি করো:

```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "auth-api"
    metrics_path: "/metrics"
    static_configs:
      - targets: ["web:8000"]
```

এখানে `web:8000` তখনই কাজ করবে যখন Prometheus এবং Django container একই Docker network-এ থাকবে এবং `web` সঠিক Compose service name হবে। Blue-green setup-এ service name আলাদা হলে সেই অনুযায়ী targets বদলাতে হবে।

### ধাপ 5 — Docker Compose-এ Prometheus

```
services:
  prometheus:
    image: prom/prometheus
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"
    volumes:
      - ./deploy/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    networks:
      - monitoring
      - app_internal
    restart: unless-stopped

volumes:
  prometheus_data:

networks:
  monitoring:
  app_internal:
```

এটি বিদ্যমান `docker-compose.yml`-এর service/volume/network configuration-এর সঙ্গে merge করার উদাহরণ—পুরো Compose file হিসেবে সরাসরি replace করবে না। `app_internal` network-টি তোমার Django service-এও থাকতে হবে। Production-এ image version pin করো এবং metrics endpoint internal-only রাখো।

### ধাপ 6 — Grafana

Grafana-কে একই monitoring network-এ চালাও। Grafana UI-তে Prometheus data source যোগ করার সময় URL হিসেবে সাধারণত `http://prometheus:9090` ব্যবহার করা যায়, যদি দুটো একই Docker network-এ থাকে।

প্রাথমিক dashboard-এ এই metrics রাখো:

- HTTP request rate
- 5xx error rate
- p95/p99 request latency
- Django process/resource usage—প্রযোজ্য exporter থাকলে
- Database availability ও connection saturation—প্রযোজ্য PostgreSQL exporter থাকলে

শুধু `django-prometheus` যোগ করলেই PostgreSQL-এর সব operational metric পাওয়া যাবে না। PostgreSQL-এর connections, locks, replication lag, disk usage ইত্যাদির জন্য PostgreSQL exporter বা database monitoring আলাদাভাবে configure করতে হবে।

## 7. PostgreSQL backup automation

Monitoring থাকলেও database data হারিয়ে গেলে সমস্যা হতে পারে। তাই backup তৈরি, নিরাপদে সংরক্ষণ এবং restore পরীক্ষা—তিনটিই দরকার।

### ধাপ 1 — Backup script

Production server-এর deployment directory-তে `deploy/backup-postgres.sh` তৈরি করো:

```
#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete_auth_project"
BACKUP_DIR="/var/backups/auth-api/postgres"
TIMESTAMP="$(date -u +'%Y-%m-%dT%H-%M-%SZ')"
BACKUP_FILE="${BACKUP_DIR}/auth_${TIMESTAMP}.dump"

cd "$APP_DIR"

install -d -m 700 "$BACKUP_DIR"
umask 077

echo "Starting PostgreSQL backup: $TIMESTAMP"

docker compose exec -T db sh -c \
  'pg_dump -U "$POSTGRES_USER" -d "$POSTGRES_DB" -Fc' \
  > "$BACKUP_FILE"

if [[ ! -s "$BACKUP_FILE" ]]; then
    echo "ERROR: Backup file is empty."
    rm -f "$BACKUP_FILE"
    exit 1
fi

# Validate that the archive can be read.
docker compose exec -T db sh -c \
  'pg_restore --list' < "$BACKUP_FILE" > /dev/null

echo "Backup created: $BACKUP_FILE"

# Keep local backups for 14 days.
find "$BACKUP_DIR" \
  -type f \
  -name 'auth_*.dump' \
  -mtime +14 \
  -delete

echo "Backup job completed."
```

এখানে `db`, `POSTGRES_USER` ও `POSTGRES_DB` তোমার Compose configuration-এর সঙ্গে মিলতে হবে। `pg_dump -Fc` PostgreSQL-এর custom archive format তৈরি করে; `pg_restore` দিয়ে সেটি restore করা যায়।

Script executable করো:

```
chmod 700 deploy/backup-postgres.sh
```

তারপর staging বা test server-এ চালিয়ে যাচাই করো:

```
sudo ./deploy/backup-postgres.sh
```

সতর্কতা: `-mtime +14` দিয়ে ১৪ দিনের বেশি পুরোনো local backup মুছে ফেলা হবে। এই local retention-এর পাশাপাশি আলাদা off-site backup না থাকলে server বা disk নষ্ট হওয়ার পর সব backup হারাতে পারো।

### ধাপ 2 — Backup security

Production backup-এ user account, email এবং অন্যান্য ব্যক্তিগত তথ্য থাকতে পারে। তাই:

- Backup directory-র permission সীমিত রাখবে।
- Backup encrypted storage-এ পাঠাবে; যেমন encrypted object storage বা appropriately configured encrypted backup remote।
- Encryption key এবং storage credentials database server-এর একই disk-এ শুধু একটি copy হিসেবে রাখবে না।
- সফল backup-এর পাশাপাশি off-site upload-এর সফলতাও যাচাই করবে।
- Retention policy অনুযায়ী local ও remote copy আলাদাভাবে পরিচালনা করবে।

### ধাপ 3 — প্রতিদিন স্বয়ংক্রিয় backup

Ubuntu server-এ systemd timer ব্যবহার করতে পারো।

`/etc/systemd/system/auth-api-backup.service`

```
[Unit]
Description=Authentication API PostgreSQL backup

[Service]
Type=oneshot
ExecStart=/opt/complete_auth_project/deploy/backup-postgres.sh
```

`/etc/systemd/system/auth-api-backup.timer`

```
[Unit]
Description=Daily authentication database backup

[Timer]
OnCalendar=*-*-* 02:00:00 UTC
Persistent=true

[Install]
WantedBy=timers.target
```

সক্রিয় করো:

```
sudo systemctl daemon-reload
sudo systemctl enable --now auth-api-backup.timer

systemctl list-timers auth-api-backup.timer
```

Log দেখার জন্য:

```
sudo journalctl -u auth-api-backup.service
```

Production-এ backup script কোন Unix user হিসেবে চলবে, সে user-এর Docker access ও backup-directory permission আগে ঠিক করতে হবে। Docker group access-কে root-সদৃশ privilege হিসেবে বিবেচনা করো; সম্ভব হলে dedicated backup account ও সীমিত permissions ব্যবহার করো।

## 8. Disaster recovery drill — backup সত্যিই restore হয় কি না?

Backup file তৈরি হওয়া মানেই recovery সম্ভব—এটি নিশ্চিত নয়। Archive corrupt হতে পারে, credentials ভুল হতে পারে অথবা schema/data অসম্পূর্ণ থাকতে পারে। তাই আলাদা test database-এ restore করতে হবে।

Production database-এ পরীক্ষা করবে না

Restore drill-এর জন্য disposable database ব্যবহার করো। নিচের উদাহরণে `auth_restore_drill` নামে একটি পৃথক database তৈরি করা হবে। এটি আগে থেকে থাকলে নাম পরিবর্তন করো বা আগের test database মুছে ফেলার আগে তার data সত্যিই disposable কি না যাচাই করো।

### ধাপ 1 — Restore drill script

`deploy/restore-drill.sh`:

```
#!/usr/bin/env bash
set -Eeuo pipefail

APP_DIR="/opt/complete_auth_project"
BACKUP_FILE="${1:?Usage: restore-drill.sh /path/to/backup.dump}"
TEST_DB="auth_restore_drill"

cd "$APP_DIR"

if [[ ! -r "$BACKUP_FILE" ]]; then
    echo "ERROR: Cannot read backup file."
    exit 1
fi

echo "Creating isolated test database: $TEST_DB"

docker compose exec -T db sh -c \
  'createdb -U "$POSTGRES_USER" auth_restore_drill'

echo "Restoring backup into test database..."

docker compose exec -T db sh -c \
  'pg_restore -U "$POSTGRES_USER" \
    -d auth_restore_drill \
    --no-owner --no-privileges' \
  < "$BACKUP_FILE"

echo "Checking restored database..."

docker compose exec -T db sh -c \
  'psql -v ON_ERROR_STOP=1 \
    -U "$POSTGRES_USER" \
    -d auth_restore_drill \
    -c "SELECT COUNT(*) FROM django_migrations;"'

echo "Restore completed. Verify tables and critical application data."
echo "Do not delete the test database until verification is complete."
```

এরপর:

```
chmod 700 deploy/restore-drill.sh

sudo ./deploy/restore-drill.sh \
  /var/backups/auth-api/postgres/auth_YYYY-MM-DDTHH-MM-SSZ.dump
```

`YYYY-MM-DDTHH-MM-SSZ`-এর জায়গায় বাস্তব backup filename বসাবে।

এই script-এর শেষের query একটি প্রাথমিক smoke test মাত্র। তোমার database-এ `django_migrations` table থাকা দরকার; পুরোনো বা অসম্পূর্ণ backup হলে query ব্যর্থ হতে পারে। Restore সফল হলে আরও যাচাই করবে:

1. প্রত্যাশিত tables ও migrations আছে কি না।
2. User record এবং গুরুত্বপূর্ণ application data-এর যুক্তিসংগত সংখ্যা আছে কি না।
3. Foreign key ও গুরুত্বপূর্ণ constraints ঠিক আছে কি না।
4. Staging configuration দিয়ে application ওই restored database পড়তে পারছে কি না।
5. Restore করতে কত সময় লাগল, সেটি লিখে রাখবে।

সতর্কতা: `--no-owner --no-privileges` ব্যবহার করলে archive-এর owner ও privilege restoration বাদ যায়। Recovery environment-এ প্রয়োজনীয় database roles ও permissions আলাদাভাবে প্রস্তুত করতে হবে।

### ধাপ 2 — Recovery objective ঠিক করা

দুটি গুরুত্বপূর্ণ production ধারণা:

- RPO (Recovery Point Objective): সর্বোচ্চ কত সময়ের data হারানো গ্রহণযোগ্য?
- RTO (Recovery Time Objective): কত সময়ের মধ্যে service পুনরুদ্ধার করতে হবে?

উদাহরণস্বরূপ, যদি RPO এক ঘণ্টা হয়, তাহলে প্রতিদিন একবার backup যথেষ্ট নয়। সে ক্ষেত্রে আরও ঘন backup, WAL archiving এবং point-in-time recovery (PITR) পরিকল্পনা বিবেচনা করতে হবে।

## 9. Monitoring alert: কখন ব্যবস্থা নিতে হবে?

Dashboard শুধু দেখার জন্য নয়; কোনো সমস্যা হলে notification-ও দরকার। শুরুতে এই alert conditions পরিকল্পনা করতে পারো:

| Alert                | উদাহরণ condition                 | কী পরীক্ষা করবে                    |
| -------------------- | -------------------------------- | ---------------------------------- |
| API errors           | 5xx rate স্বাভাবিকের চেয়ে বেশি  | Django logs, Sentry                |
| High latency         | p95 latency 1 সেকেন্ডের বেশি     | Slow queries, workers, network     |
| API unavailable      | Health endpoint বারবার ব্যর্থ    | Gunicorn, container, Nginx         |
| Database unavailable | PostgreSQL health check ব্যর্থ   | DB logs, disk, connections         |
| Backup failure       | Backup বা off-site upload ব্যর্থ | systemd logs, credentials, storage |
| Disk nearly full     | Disk usage 85% ছাড়িয়েছে        | Logs, backups, database storage    |

এই সংখ্যাগুলো উদাহরণমাত্র; প্রকৃত threshold তোমার API traffic ও service requirements অনুযায়ী ঠিক করবে।

Prometheus alerting-এর জন্য Alertmanager যুক্ত করা যায়। Grafana-তেও alert rules ও notification contact points configure করা যায়। যেকোনো একটি ব্যবস্থা বেছে নিলেও backup failure এবং service outage-এর alert যেন dashboard-এর বাইরে পৌঁছায়, তা নিশ্চিত করবে।

## 10. Lesson 14 implementation checklist

## Production readiness

0 / 9

Structured JSON logging

Application logs-এ timestamp, severity, logger ও exception তথ্য দেখা যাচ্ছে।

Request latency logging

HTTP status ও duration log হচ্ছে; sensitive data প্রকাশ পাচ্ছে না।

Sentry

Staging-এ controlled exception capture হচ্ছে এবং event-এ secret নেই।

Prometheus metrics

Metrics scrape হচ্ছে; public Internet থেকে endpoint access বন্ধ।

Grafana dashboard

Request rate, error rate ও latency দেখা যাচ্ছে।

Automated PostgreSQL backup

Scheduled backup সফল হচ্ছে এবং retention কাজ করছে।

Off-site backup

Backup server-এর বাইরের encrypted storage-এ সংরক্ষিত হচ্ছে।

Restore drill

আলাদা database-এ restore করে application data যাচাই করা হয়েছে।

Alerting

API outage, backup failure ও disk-space alert পরীক্ষা করা হয়েছে।

## 11. Final verification commands

Ubuntu VPS-এ এগুলো ব্যবহার করে প্রাথমিক অবস্থা যাচাই করতে পারো:

```
# Running services
docker compose ps

# Application logs
docker compose logs --tail=100 web

# Database logs
docker compose logs --tail=100 db

# Backup timer
systemctl list-timers auth-api-backup.timer

# Latest backup files
sudo ls -lh /var/backups/auth-api/postgres/

# Backup service logs
sudo journalctl -u auth-api-backup.service -n 100

# Nginx configuration
sudo nginx -t

# Disk capacity
df -h
```

এখানে `web` ও `db` তোমার actual Compose service names-এর সঙ্গে মিলিয়ে নেবে। Blue-green deployment-এ `web`-এর বদলে `app-blue` বা `app-green`-এর মতো service name হতে পারে।

## Lesson 14-এর মূল শিক্ষা

Production observability মানে শুধু Grafana dashboard তৈরি করা নয়। একটি সম্পূর্ণ ব্যবস্থা হবে:

- Detect: Logs, Sentry এবং metrics দিয়ে সমস্যা শনাক্ত করা।
- Diagnose: Stack trace, latency ও database health দেখে কারণ বের করা।
- Recover: Tested backup থেকে database restore করা এবং recovery time মাপা।
- Prevent recurrence: Alert, deployment checks এবং incident review দিয়ে একই সমস্যা পুনরায় হওয়ার ঝুঁকি কমানো।

পরের ধাপে আমরা Lesson 15 — Production Security Audit করতে পারি: Django security settings, HTTPS/HSTS, CORS/CSRF, JWT attack scenarios, rate limiting, dependency scanning, container hardening এবং automated security tests—সবকিছু checklist ও বাস্তব code দিয়ে।


---
# Lesson 15: Production Security Audit — Django REST Framework

এই Lesson-এ আমাদের `complete_auth_project`-এর authentication API-কে production security audit করব। শুধু security settings চালু করলেই API নিরাপদ হয় না; configuration, authentication flow, permissions, dependencies এবং deployment—সবকিছু একসঙ্গে যাচাই করতে হবে।

আমরা আগের Lesson-এর custom User, JWT, email verification, password reset, role-based permissions, Docker, Nginx ও Gunicorn architecture ধরে এগোব।

## Lesson roadmap

1\. Django production settings

DEBUG, SECRET_KEY, ALLOWED_HOSTS, secure cookies এবং security headers।

2\. HTTPS, HSTS, CORS ও CSRF

Browser-based frontend এবং API-এর নিরাপদ communication configuration।

3\. JWT attack scenarios

Token theft, refresh-token rotation, logout, revocation এবং privilege escalation প্রতিরোধ।

4\. Rate limiting ও abuse prevention

Login brute-force, OTP abuse, password-reset abuse এবং distributed requests।

5\. Dependency scanning ও automated audit

Known vulnerabilities, dependency pinning, security tests এবং release checklist।

## 1. Django production security settings

প্রথমে বুঝে নাও: Django-এর `DEBUG=False` production-এর জন্য জরুরি, কিন্তু এটুকু করলেই security audit সম্পূর্ণ হয় না।

### ধাপ 1 — Environment variables ব্যবহার

Production `.env` ফাইলে:

```
DEBUG=False
DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_ALLOWED_HOSTS=api.example.com
DJANGO_CSRF_TRUSTED_ORIGINS=https://app.example.com
```

এগুলো উদাহরণ। নিজের domain ব্যবহার করবে। `.env` Git repository-তে commit করবে না; VPS-এ file permissions সীমিত রাখবে।

### ধাপ 2 — `config/settings.py`

```
import osDEBUG = os.getenv("DEBUG", "False").lower() == "true"SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]ALLOWED_HOSTS = [    host.strip()    for host in os.environ["DJANGO_ALLOWED_HOSTS"].split(",")    if host.strip()]CSRF_TRUSTED_ORIGINS = [    origin.strip()    for origin in os.getenv(        "DJANGO_CSRF_TRUSTED_ORIGINS", ""    ).split(",")    if origin.strip()]
```

`DJANGO_SECRET_KEY` না থাকলে application startup ব্যর্থ হবে—এটাই নিরাপদ আচরণ। Production-এ default development key ব্যবহার করা উচিত নয়।

### ধাপ 3 — HTTPS security settings

`config/settings.py`-তে:

```
SECURE_SSL_REDIRECT = TrueSESSION_COOKIE_SECURE = TrueCSRF_COOKIE_SECURE = TrueSECURE_CONTENT_TYPE_NOSNIFF = TrueSECURE_REFERRER_POLICY = "strict-origin-when-cross-origin"SECURE_HSTS_SECONDS = 31536000SECURE_HSTS_INCLUDE_SUBDOMAINS = FalseSECURE_HSTS_PRELOAD = False
```

এগুলো চালু করার আগে নিশ্চিত হও যে domain-এর HTTPS সঠিকভাবে কাজ করছে। বিশেষত HSTS browser-কে দীর্ঘ সময় HTTPS ব্যবহার করতে বাধ্য করতে পারে। `includeSubDomains` বা `preload` চালু করার আগে সব সংশ্লিষ্ট subdomain-এ HTTPS নিশ্চিত করতে হবে।

Reverse proxy সতর্কতা: Nginx TLS terminate করে Gunicorn-এর কাছে HTTP দিয়ে request পাঠালে Django যেন সঠিকভাবে original HTTPS scheme বুঝতে পারে। সাধারণ configuration:

```
SECURE_PROXY_SSL_HEADER = (    "HTTP_X_FORWARDED_PROTO",    "https",)
```

এটি কেবল তখনই ব্যবহার করবে যখন তোমার trusted Nginx proxy `X-Forwarded-Proto` header-টি নিজে সেট করে এবং untrusted clients-এর দেওয়া header সরাসরি বিশ্বাস করে না। অন্যথায় redirect loop বা scheme spoofing-এর ঝুঁকি তৈরি হতে পারে।

## 2. CORS ও CSRF — দুটির কাজ আলাদা

- CORS: কোন browser origin থেকে frontend API response পড়তে পারবে, তা নিয়ন্ত্রণ করে।
- CSRF protection: Browser স্বয়ংক্রিয়ভাবে পাঠানো credentials—বিশেষ করে cookies—ব্যবহার করে অনিচ্ছাকৃত request পাঠানো ঠেকাতে সাহায্য করে।

CORS নিজে authentication বা authorization-এর বিকল্প নয়।

### ধাপ 1 — CORS allowlist

`django-cors-headers` ইনস্টল করা না থাকলে:

```
pip install django-cors-headers
```

`settings.py`:

```
INSTALLED_APPS = [    "corsheaders",    # Existing apps...]MIDDLEWARE = [    "corsheaders.middleware.CorsMiddleware",    "django.middleware.common.CommonMiddleware",    # Remaining middleware...]CORS_ALLOWED_ORIGINS = [    "https://app.example.com",]
```

Production-এ সাধারণত `CORS_ALLOW_ALL_ORIGINS = True` ব্যবহার করবে না। শুধু বাস্তবে ব্যবহৃত frontend origins রাখবে।

### ধাপ 2 — JWT header বনাম cookie authentication

আমাদের আগের project-এ JWT `Authorization: Bearer ...` header দিয়ে পাঠানো হয়। এই পদ্ধতিতে browser স্বয়ংক্রিয়ভাবে token attach করে না, তাই cookie-based authentication-এর তুলনায় CSRF exposure আলাদা। তবে XSS-এর মাধ্যমে token চুরি হওয়ার ঝুঁকি থেকে যায়।

যদি JWT access বা refresh token `HttpOnly` cookie-তে রাখো, তাহলে cookie settings, `SameSite`, `Secure`, CSRF token এবং cross-origin credentials policy একসঙ্গে পরিকল্পনা করতে হবে। শুধু CORS allowlist দিলেই cookie-based request CSRF থেকে নিরাপদ হয় না।

আরেকটি গুরুত্বপূর্ণ বিষয়: browser-এ `localStorage`-এ long-lived refresh token রাখলে XSS হলে token চুরির ঝুঁকি বেশি। তোমার frontend architecture অনুযায়ী token storage বেছে নিতে হবে।

## 3. JWT attack scenarios এবং প্রতিরোধ

আমাদের authentication project-এ access token-এর lifetime ১০ মিনিট, refresh token-এর lifetime ১ দিন এবং custom `token_version` আছে। এগুলো ভালো ভিত্তি, কিন্তু কয়েকটি বিষয় যাচাই করা দরকার।

Scenario A — Access token চুরি

আক্রমণকারী কোনো ব্যবহারকারীর valid access token পেলে সেটির expiry পর্যন্ত API ব্যবহার করার চেষ্টা করতে পারে।

প্রতিরোধ: HTTPS, token exposure কমানো, short-lived access token, এবং password reset বা security event-এর সময় token-version increment।

Scenario B — Refresh token replay

পুরোনো refresh token আবার ব্যবহার করে নতুন access token পাওয়ার চেষ্টা হতে পারে।

প্রতিরোধ: Refresh rotation ও blacklist configuration যাচাই, concurrent refresh requests পরীক্ষা এবং refresh-token reuse-এর monitoring।

Scenario C — Privilege escalation

সাধারণ user request-এ role, is_staff বা is_superuser পরিবর্তন করে elevated access পাওয়ার চেষ্টা করতে পারে।

প্রতিরোধ: Public serializers থেকে privileged fields বাদ রাখা; role changes-এ explicit permission ও server-side validation।

Scenario D — Logout-এর পরও access token সচল

Refresh token blacklist করা হলেও বিদ্যমান access token expiry পর্যন্ত কার্যকর থাকতে পারে।

প্রতিরোধ: Custom token-version validation এবং logout-এর সময় token-version increment-এর policy বিবেচনা করা।

### ধাপ 1 — JWT settings যাচাই

```
from datetime import timedeltaSIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,    "UPDATE_LAST_LOGIN": False,}
```

এখানে `UPDATE_LAST_LOGIN=False` উদাহরণ হিসেবে রাখা হয়েছে, কারণ প্রতিটি login-এ database write এবং user-activity tracking-এর privacy considerations আছে। Login tracking দরকার হলে আলাদা, সীমিত logging policy তৈরি করতে পারো।

এছাড়া নিশ্চিত করো:

- `rest_framework_simplejwt.token_blacklist` `INSTALLED_APPS`-এ আছে।
- Migration চালানো হয়েছে।
- `VersionedJWTAuthentication` protected endpoints-এ ব্যবহৃত হচ্ছে।
- Refresh endpoint-এ refresh-token rotation ও blacklist প্রত্যাশামতো কাজ করছে।
- Access token এবং refresh token কোনো application log-এ লেখা হচ্ছে না।

### ধাপ 2 — Logout ও revocation-এর আচরণ নির্ধারণ

আমাদের আগের custom `VersionedJWTAuthentication` token-এর `token_version` এবং user-এর বর্তমান `token_version` তুলনা করে।

তাই যদি সব device থেকে access token বাতিল করতে চাও, user-এর `token_version` increment করলে পুরোনো version-এর access token আর গ্রহণ করা হবে না।

কিন্তু একটি policy সিদ্ধান্ত দরকার:

- শুধু refresh token blacklist করবে?
- নাকি logout-এ token-version increment করে সব device-এর access token-ও বাতিল করবে?

দ্বিতীয় পদ্ধতিতে সব device-এর session বাতিল হতে পারে। Multi-device application-এ per-device session tracking বেশি উপযোগী হতে পারে।

গুরুত্বপূর্ণ: Token version increment-এর পর পুরোনো access token invalid হলেও cache বা custom authentication flow থাকলে সেটিও পরীক্ষা করতে হবে। `token_version` claim না থাকা পুরোনো tokens-কে strict validation প্রত্যাখ্যান করবে—deployment-এর সময় পুরোনো session পুনরায় login করতে হতে পারে।

## 4. Rate limiting ও authentication abuse prevention

DRF-এর throttling সাধারণ abuse কমাতে সাহায্য করে, তবে এটি পূর্ণাঙ্গ brute-force defense বা DDoS protection নয়। বিশেষত distributed traffic-এর বিরুদ্ধে reverse proxy, WAF বা infrastructure-level controls প্রয়োজন হতে পারে।

### ধাপ 1 — DRF throttle configuration

`settings.py`:

```
REST_FRAMEWORK = {    # Keep your existing authentication and permission settings.    "DEFAULT_THROTTLE_CLASSES": [        "rest_framework.throttling.AnonRateThrottle",        "rest_framework.throttling.UserRateThrottle",        "rest_framework.throttling.ScopedRateThrottle",    ],    "DEFAULT_THROTTLE_RATES": {        "anon": "100/hour",        "user": "1000/hour",        "register": "5/hour",        "login": "10/minute",        "resend_verification": "3/hour",        "forgot_password": "5/hour",        "password_reset": "5/hour",        "change_email": "3/hour",        "confirm_email_change": "5/hour",    },}
```

এটি বিদ্যমান `REST_FRAMEWORK` dictionary-কে merge করে আপডেট করবে; আগের `DEFAULT_AUTHENTICATION_CLASSES`, `DEFAULT_PERMISSION_CLASSES` বা অন্যান্য settings মুছে ফেলবে না।

এই rate-গুলো প্রাথমিক উদাহরণ, চূড়ান্ত security limits নয়। বৈধ user traffic, shared IP, NAT এবং account recovery-এর ব্যবহার বিবেচনা করে tune করতে হবে।

### ধাপ 2 — View-এ scope ব্যবহার

```
from rest_framework.throttling import ScopedRateThrottlefrom rest_framework.views import APIViewclass LoginAPIView(APIView):    throttle_classes = [ScopedRateThrottle]    throttle_scope = "login"    # Existing login implementation remains here.
```

একইভাবে register, resend verification এবং password reset views-এ সংশ্লিষ্ট `throttle_scope` দিতে হবে।

### ধাপ 3 — Distributed production deployment-এ Redis

DRF-এর built-in throttling cache ব্যবহার করে। একাধিক Gunicorn worker বা blue-green instances-এ consistent limits পেতে shared Redis cache ব্যবহার করা ভালো। প্রতিটি container-এর local-memory cache ব্যবহার করলে প্রতিটি instance আলাদাভাবে request count করতে পারে।

তবে DRF-এর built-in throttling best-effort: এটি atomic, exact security counter হিসেবে নকশা করা হয়নি। উচ্চ-ঝুঁকির login protection-এর জন্য দরকার হলে atomic Redis counters, account-based cooldown, proxy-level limits এবং monitoring যোগ করো।

আরও কয়েকটি নিয়ম:

- Login-এ email আছে কি নেই—এমন তথ্য প্রকাশ না করে generic error response দাও।
- Password-reset endpoint-এ user account থাকুক বা না থাকুক, একই ধরনের response দাও।
- Email verification ও OTP resend-এ cooldown রাখো।
- Client-supplied `X-Forwarded-For` header সরাসরি বিশ্বাস করে IP limit নির্ধারণ করবে না; trusted proxy configuration সঠিক হতে হবে।

## 5. Dependency scanning — vulnerable package খুঁজে বের করা

Django, DRF, SimpleJWT এবং অন্য Python packages-এ security vulnerability থাকতে পারে। শুধু package install করলেই হবে না; dependency versions ও known vulnerabilities নিয়মিত যাচাই করতে হবে।

### ধাপ 1 — Dependency versions pin করা

`requirements.txt`-এ tested versions নির্দিষ্ট করে রাখো, যেমন:

```
Django==<tested-version>
djangorestframework==<tested-version>
djangorestframework-simplejwt==<tested-version>
django-cors-headers==<tested-version>
sentry-sdk[django]==<tested-version>
django-prometheus==<tested-version>
```

`<tested-version>` এখানে placeholder; literal হিসেবে file-এ রাখবে না। তোমার project-এ ব্যবহৃত compatible versions দিয়ে পূরণ করবে। Random version অনুমান না করে virtual environment-এ tests চালিয়ে dependency update করবে।

Installed versions দেখতে:

```
python -m pip list
python -m pip check
```

### ধাপ 2 — `pip-audit` দিয়ে vulnerability scan

```
python -m pip install pip-audit

pip-audit -r requirements.txt
```

এটি dependency-তে পরিচিত vulnerability খুঁজতে সাহায্য করে। Scan clean হলেই package সম্পূর্ণ নিরাপদ—এমন নিশ্চয়তা নেই।

Vulnerability পাওয়া গেলে:

1. Package ও affected version শনাক্ত করো।
2. Advisory অনুযায়ী fixed version নির্ধারণ করো।
3. Virtual environment-এ update করো।
4. `python manage.py check` ও automated tests চালাও।
5. Staging-এ smoke tests করে তারপর production deploy করো।

### ধাপ 3 — GitHub Actions CI-তে যোগ করা

তোমার আগের Lesson 11-এর CI workflow-তে tests-এর আগে বা আলাদা security job-এ যোগ করতে পারো:

```
- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    pip install pip-audit

- name: Check dependency vulnerabilities
  run: pip-audit -r requirements.txt

- name: Django deployment checks
  env:
    DEBUG: "False"
    DJANGO_SECRET_KEY: ${{ secrets.CI_DJANGO_SECRET_KEY }}
    DJANGO_ALLOWED_HOSTS: "localhost,127.0.0.1"
  run: python manage.py check --deploy
```

`CI_DJANGO_SECRET_KEY` একটি GitHub Actions secret হিসেবে configure করতে হবে। `manage.py check --deploy`-এর warnings ও errors পর্যালোচনা করবে; শুধু command exit code দেখেই audit শেষ করবে না।

CI-তে production secret ব্যবহার না করে আলাদা test-only secret ব্যবহার করবে। Vulnerability scan-এ exception বা allowlist রাখলে তার কারণ, owner এবং expiry date নথিভুক্ত করবে।

## 6. Automated security tests

Security configuration কার্যকর হচ্ছে কি না—test দিয়ে যাচাই করো। নিচের test examples `accounts/tests/test_security.py` ফাইলে রাখা যেতে পারে। এগুলো Django/DRF test runner-এর জন্য; তোমার project-এর model factory বা registration serializer অনুযায়ী setup পরিবর্তন করতে হতে পারে।

### Test A — Anonymous user protected endpoint access করতে পারবে না

```
from rest_framework.test import APITestCaseclass AuthenticationSecurityTests(APITestCase):    def test_profile_requires_authentication(self):        response = self.client.get("/api/auth/profile/")        self.assertIn(response.status_code, (401, 403))
```

এটি ধরে নিচ্ছে profile endpoint anonymous access অনুমোদন করে না। তোমার authentication configuration অনুযায়ী 401 বা 403 হতে পারে।

### Test B — Public serializer privileged fields expose করছে না

```
from django.test import TestCasefrom accounts.models import Userfrom accounts.serializers import UserSerializerclass PublicUserSerializerSecurityTests(TestCase):    def test_privileged_fields_are_not_exposed(self):        user = User(            email="audit-example@example.com",            role=User.Role.USER,        )        data = UserSerializer(user).data        forbidden_fields = {            "password",            "is_superuser",            "is_staff",            "token_version",        }        self.assertTrue(            forbidden_fields.isdisjoint(data.keys())        )
```

এখানে `UserSerializer` তোমার actual public serializer-এর নামের সঙ্গে মিলিয়ে নেবে। Test instance-টি database-এ save করা জরুরি নয়, যদি serializer-এর অন্য কোনো field database access না করে।

### Test C — Role change endpoint unauthorized access ঠেকায়

এখানে শুধু একটি example test pattern:

```
def test_regular_user_cannot_change_roles(self):    # Create a regular user and authenticate as that user.    # Call the role-change endpoint for another account.    # Assert that the response is 403 or otherwise denied.    pass
```

`pass`-টি ইচ্ছাকৃত placeholder—এটি নিজে security test নয়। বাস্তব test-এ তোমার user factory, URL name এবং role-change request ব্যবহার করে endpoint hit করতে হবে। শুধু permission class unit test না করে API-level behavior যাচাই করো।

### Test D — Password reset token single-use

পরীক্ষা করো:

- প্রথম valid reset request সফল হয়।
- একই token দ্বিতীয়বার ব্যবহার করা যায় না।
- Expired token প্রত্যাখ্যাত হয়।
- Token database-এ raw অবস্থায় সংরক্ষিত নেই।
- Password reset-এর পরে পুরোনো access token invalid হয়, যদি সেটি তোমার revocation policy হয়।

এগুলো তোমার আগের authentication features-এর জন্য অত্যন্ত গুরুত্বপূর্ণ regression tests।

## 7. Django-এর built-in deployment security audit

VPS-এ production settings যাচাই করতে চালাও:

```
python manage.py check --deploy
```

এটি Django-এর deployment-oriented checks চালায়। বিশেষ করে নিচের বিষয়গুলো পরীক্ষা করবে:

- `DEBUG=False`
- `SECRET_KEY` নিরাপদ ও গোপন
- `ALLOWED_HOSTS` সীমিত
- HTTPS ও secure cookie configuration
- HSTS policy
- CSRF protection
- Production database ও deployment configuration

এটি পূর্ণাঙ্গ penetration test নয় এবং সব সমস্যা শনাক্ত করতে পারে না। Output-এ warning থাকলে প্রতিটি warning-এর কারণ বুঝে সমাধান করতে হবে।

## 8. Final production security checklist

## Security audit progress

0/10

Django configuration

DEBUG=False, secret environment variable-এ, ALLOWED_HOSTS সীমিত।

HTTPS ও proxy

TLS কার্যকর, redirect loop নেই, trusted proxy header সঠিক।

HSTS

HTTPS স্থিতিশীলভাবে চালু হওয়ার পর policy যাচাই করে enable করা হয়েছে।

CORS ও CSRF

Allowed origins সীমিত; cookie authentication থাকলে CSRF test করা হয়েছে।

JWT lifecycle

Refresh rotation, blacklist, token-version validation ও logout policy test করা হয়েছে।

Permissions

Anonymous access, role escalation ও object-level access test করা হয়েছে।

Rate limiting

Login, registration, verification ও password reset endpoints সীমিত করা হয়েছে।

Dependency audit

pip-audit চালানো, vulnerabilities review এবং update tests সম্পন্ন।

Automated security tests

Authentication, password reset, serializers ও permission regression tests পাস।

CI deployment gate

Tests ও security checks সফল না হলে production deployment বন্ধ থাকে।

## 9. এখন বাস্তবে কীভাবে শুরু করবে?

একবারে সব production setting পরিবর্তন না করে এই sequence অনুসরণ করো:

1. বর্তমান `settings.py` ও `.env`-এর backup নাও।
2. Staging environment-এ `check --deploy` চালিয়ে warnings দেখো।
3. HTTPS, proxy ও CORS/CSRF configuration যাচাই করো।
4. JWT revocation ও permission tests লেখো।
5. Login এবং password-reset throttling পরীক্ষা করো।
6. `pip-audit` CI-তে যোগ করো।
7. Staging smoke test পাস করার পর controlled deployment করো।

মনে রেখো, security audit-এর উদ্দেশ্য শুধু warning দূর করা নয়; কোনো user বা attacker অননুমোদিত access পাবে না—এটি tests ও configuration দিয়ে প্রমাণ করার চেষ্টা করা।

পরবর্তী যৌক্তিক Lesson 16 হবে End-to-End Authentication Security Testing—pytest/DRF test client দিয়ে registration, email verification, login, JWT refresh, logout, password reset, token revocation, RBAC এবং rate limiting-এর automated test suite তৈরি করা; এরপর সেটিকে GitHub Actions CI-তে সংযুক্ত করা।

---
# Lesson 16: End-to-End Authentication Security Testing

আজ আমরা `complete_auth_project`-এর জন্য বাস্তবসম্মত automated authentication test suite তৈরি করব। লক্ষ্য হলো—কেউ registration, login, token refresh, password reset বা role-based permissions-এর কোনো অংশ ভেঙে ফেললে CI pipeline সেটি deployment-এর আগেই ধরতে পারবে।

এই Lesson-এ ব্যবহার করব:

- pytest + pytest-django — test runner ও Django integration
- DRF APIClient — HTTP API endpoint test
- Django test database — production database থেকে বিচ্ছিন্ন test data
- JWT token tests — refresh, logout এবং revocation
- GitHub Actions — automated test ও deployment gate

আমরা আগের project-এর custom `accounts.User`, `token_version`, SimpleJWT blacklist, email verification এবং role-based access control ধরে এগোব। কিছু endpoint-এর সঠিক নাম ও response format তোমার project-এ ভিন্ন হতে পারে, তাই নিচের test-গুলোকে একটি পূর্ণাঙ্গ implementation template হিসেবে ধরবে—নিজের URL ও serializer-এর সঙ্গে মিলিয়ে নিতে হবে।

## 1. Testing architecture

pytest test suite

Fixtures · APIClient · Assertions

Django REST API

Views · Serializers · Permissions · Services

Test DB

Isolated data

In-memory email

No real emails sent

GitHub Actions CI

Tests pass → build/deploy may proceed

## 2. Install testing dependencies

Project root-এ virtual environment সক্রিয় করে চালাও:

```
pip install pytest pytest-django pytest-cov
```

`requirements-dev.txt` তৈরি করতে পারো:

```
-r requirements.txt
pytest
pytest-django
pytest-cov
```

`pytest.ini`:

```
[pytest]
DJANGO_SETTINGS_MODULE = config.settings
python_files = tests.py test_*.py *_tests.py
addopts = -ra
```

এখন pytest-কে project-এর Django settings জানা থাকবে। Test database তৈরির জন্য তোমার production settings-এ PostgreSQL থাকলেও CI-তে আলাদা PostgreSQL service ব্যবহার করা ভালো, বিশেষ করে production-এ PostgreSQL-নির্ভর আচরণ থাকলে।

## 3. Test folder structure

```
complete_auth_project/
├── accounts/
│   ├── models.py
│   ├── views.py
│   ├── urls.py
│   └── tests/
│       ├── __init__.py
│       ├── conftest.py
│       ├── test_registration.py
│       ├── test_email_verification.py
│       ├── test_login.py
│       ├── test_jwt_lifecycle.py
│       ├── test_password_reset.py
│       ├── test_permissions.py
│       └── test_throttling.py
├── pytest.ini
├── requirements.txt
└── requirements-dev.txt
```

`conftest.py`-তে shared fixtures থাকবে। ফলে প্রতিটি test file-এ বারবার user তৈরির code লিখতে হবে না।

## 4. Shared fixtures তৈরি করা

`accounts/tests/conftest.py`:

```
import pytestfrom rest_framework.test import APIClientfrom accounts.models import User@pytest.fixturedef api_client():    return APIClient()@pytest.fixturedef user(db):    return User.objects.create_user(        email="user@example.com",        password="Strong-Test-Password-938!",    )@pytest.fixturedef second_user(db):    return User.objects.create_user(        email="second@example.com",        password="Strong-Test-Password-827!",    )@pytest.fixturedef authenticated_client(api_client, user):    api_client.force_authenticate(user=user)    return api_client
```

এখানে `db` fixture test database ব্যবহারের অনুমতি দেয়। `create_user()` অবশ্যই password hash করবে—সরাসরি `User.objects.create(password=...)` দিয়ে user তৈরি করবে না।

`force_authenticate()` permission tests-এর জন্য সুবিধাজনক, কিন্তু এটি JWT parsing বা signature যাচাই পরীক্ষা করে না। JWT-এর জন্য পরে বাস্তব login/refresh flow ব্যবহার করব।

## 5. Registration tests

ধরি registration endpoint:

`POST /api/auth/register/`

`accounts/tests/test_registration.py`:

```
import pytestfrom django.contrib.auth import get_user_modelfrom rest_framework import statusfrom rest_framework.test import APIClientUser = get_user_model()REGISTER_URL = "/api/auth/register/"@pytest.mark.django_dbdef test_registration_creates_user():    client = APIClient()    payload = {        "email": "newuser@example.com",        "password": "Strong-Test-Password-938!",    }    response = client.post(        REGISTER_URL,        payload,        format="json",    )    assert response.status_code in (        status.HTTP_200_OK,        status.HTTP_201_CREATED,    )    user = User.objects.get(email="newuser@example.com")    assert user.check_password(payload["password"])    assert user.email_verified is False
```

তোমার serializer-এ `password_confirm` বা অন্য required field থাকলে payload-এ সেটিও যোগ করবে। Response status-এর গ্রহণযোগ্যতা তোমার API contract অনুযায়ী একটি নির্দিষ্ট status code-এ সীমাবদ্ধ করাই ভালো।

এবার duplicate email test:

```
@pytest.mark.django_dbdef test_registration_rejects_duplicate_email(user):    client = APIClient()    response = client.post(        REGISTER_URL,        {            "email": user.email,            "password": "Another-Strong-Password-123!",        },        format="json",    )    assert response.status_code == status.HTTP_400_BAD_REQUEST    assert User.objects.filter(email=user.email).count() == 1
```

আরও test করা উচিত:

- Invalid email প্রত্যাখ্যান হচ্ছে।
- দুর্বল password প্রত্যাখ্যান হচ্ছে।
- Password database-এ plaintext হিসেবে রাখা হচ্ছে না।
- Client `role`, `is_staff`, `is_superuser` পাঠিয়ে privileged account তৈরি করতে পারছে না।
- Registration response-এ password বা internal security fields প্রকাশ পাচ্ছে না।

উদাহরণ:

```
@pytest.mark.django_dbdef test_registration_cannot_assign_admin_role():    client = APIClient()    response = client.post(        REGISTER_URL,        {            "email": "attacker@example.com",            "password": "Strong-Test-Password-938!",            "role": "ADMIN",            "is_staff": True,            "is_superuser": True,        },        format="json",    )    if response.status_code in (        status.HTTP_200_OK,        status.HTTP_201_CREATED,    ):        created_user = User.objects.get(            email="attacker@example.com"        )        assert created_user.role == User.Role.USER        assert created_user.is_staff is False        assert created_user.is_superuser is False
```

এই test ধরে নিচ্ছে registration সফল হলে সাধারণ user তৈরি হবে। তোমার API অতিরিক্ত fields-এর উপস্থিতিতেই 400 দিলে সেটিও নিরাপদ আচরণ হতে পারে; সেক্ষেত্রে test-টি response contract অনুযায়ী সামঞ্জস্য করবে।

## 6. Email verification tests

এই অংশে দুটি বিষয় আলাদা করে পরীক্ষা করব:

1. Verification-এর আগে user-এর `email_verified` false থাকে।
2. বৈধ verification token ব্যবহারের পর সেটি true হয় এবং token পুনরায় ব্যবহার করা যায় না।

প্রথম test:

```
import pytestfrom rest_framework.test import APIClientVERIFY_URL = "/api/auth/email/verify/"@pytest.mark.django_dbdef test_unverified_user_cannot_become_verified_without_token(user):    assert user.email_verified is False
```

এটি শুধু initial state যাচাই করে। প্রকৃত verification test-এ তোমার verification service যে token তৈরি করে, সেই token-টি ব্যবহার করতে হবে। Token কীভাবে তৈরি হয় তা না জেনে test-এর মধ্যে নিজের মতো করে token বানালে production implementation-এর সঙ্গে test-এর সম্পর্ক থাকবে না।

উদাহরণস্বরূপ, যদি verification API JSON-এ `token` গ্রহণ করে:

```
@pytest.mark.django_dbdef test_email_verification_requires_valid_token(api_client):    response = api_client.post(        VERIFY_URL,        {"token": "invalid-test-token"},        format="json",    )    assert response.status_code in (400, 404, 422)
```

এখানে গ্রহণযোগ্য status code তোমার API contract অনুযায়ী নির্দিষ্ট করবে। Invalid token যেন account verify না করে, সেটি নিশ্চিত করো।

পরবর্তী implementation step: তোমার `email_verification_service.py`-এর token-generation function এবং email template থেকে test token সংগ্রহের helper যোগ করবে। এরপর valid-token, expired-token, already-used-token এবং wrong-user tests লিখবে। Raw token-কে test database-এ রেখে দেওয়ার বদলে বাস্তব production design-এ hashed token storage থাকলে সেটিও যাচাই করবে।

## 7. Login tests

`POST /api/auth/login/` endpoint-এর জন্য:

```
import pytestfrom rest_framework import statusfrom rest_framework.test import APIClientLOGIN_URL = "/api/auth/login/"@pytest.mark.django_dbdef test_login_returns_tokens_for_valid_credentials(user):    client = APIClient()    response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Strong-Test-Password-938!",        },        format="json",    )    assert response.status_code == status.HTTP_200_OK    assert "access" in response.data    assert "refresh" in response.data
```

এটি ধরে নিচ্ছে তোমার login view access ও refresh token response body-তে ফেরায়। যদি response shape ভিন্ন হয়, test-টি তোমার API contract অনুযায়ী লিখবে।

ভুল password test:

```
@pytest.mark.django_dbdef test_login_rejects_wrong_password(user):    client = APIClient()    response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Definitely-Wrong-Password!",        },        format="json",    )    assert response.status_code == status.HTTP_401_UNAUTHORIZED
```

আরও গুরুত্বপূর্ণ test: verified নয় এমন user login করতে পারবে কি না? তোমার policy যদি verification বাধ্যতামূলক করে, তাহলে user `email_verified=False` অবস্থায় login প্রত্যাখ্যাত হচ্ছে কি না পরীক্ষা করো।

Login response-এ `password`, `is_superuser`, internal `token_version` বা অন্যান্য অপ্রয়োজনীয় sensitive field প্রকাশ পাওয়া উচিত নয়।

## 8. JWT refresh, logout এবং token revocation tests

এটাই authentication security-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

### Test A — Login-এর পরে refresh token দিয়ে নতুন access token

`accounts/tests/test_jwt_lifecycle.py`:

```
import pytestfrom rest_framework import statusfrom rest_framework.test import APIClientLOGIN_URL = "/api/auth/login/"REFRESH_URL = "/api/auth/token/refresh/"@pytest.mark.django_dbdef test_refresh_returns_new_access_token(user):    client = APIClient()    login_response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Strong-Test-Password-938!",        },        format="json",    )    assert login_response.status_code == status.HTTP_200_OK    refresh_token = login_response.data["refresh"]    refresh_response = client.post(        REFRESH_URL,        {"refresh": refresh_token},        format="json",    )    assert refresh_response.status_code == status.HTTP_200_OK    assert "access" in refresh_response.data
```

তোমার `ROTATE_REFRESH_TOKENS=True` হলে response-এ নতুন refresh token-ও আসতে পারে। সেটি এলে নতুন refresh token ব্যবহার করার policy পরীক্ষা করবে; পুরোনো token blacklist হওয়া প্রত্যাশিত।

### Test B — Logout-এর পরে refresh token আর ব্যবহার করা যাবে না

ধরি logout endpoint `POST /api/auth/logout/`-এ refresh token গ্রহণ করে:

```
import pytestfrom rest_framework import statusfrom rest_framework.test import APIClientLOGOUT_URL = "/api/auth/logout/"@pytest.mark.django_dbdef test_logout_revokes_refresh_token(user):    client = APIClient()    login_response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Strong-Test-Password-938!",        },        format="json",    )    refresh_token = login_response.data["refresh"]    logout_response = client.post(        LOGOUT_URL,        {"refresh": refresh_token},        format="json",    )    assert logout_response.status_code in (        status.HTTP_200_OK,        status.HTTP_204_NO_CONTENT,    )    refresh_response = client.post(        REFRESH_URL,        {"refresh": refresh_token},        format="json",    )    assert refresh_response.status_code in (        status.HTTP_400_BAD_REQUEST,        status.HTTP_401_UNAUTHORIZED,    )
```

এই test-এর জন্য `token_blacklist` app install ও migrate করা থাকতে হবে। তোমার logout endpoint যদি access token, refresh token বা authentication header-এর ভিন্ন combination চায়, সেই implementation অনুযায়ী test বদলাবে।

### Test C — Password reset-এর পরে পুরোনো access token invalid

তোমার custom `VersionedJWTAuthentication`-এর আচরণ পরীক্ষা করতে:

```
import pytestfrom rest_framework.test import APIClientPROFILE_URL = "/api/auth/profile/"@pytest.mark.django_dbdef test_old_access_token_is_rejected_after_version_change(user):    client = APIClient()    login_response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Strong-Test-Password-938!",        },        format="json",    )    assert login_response.status_code == 200    old_access = login_response.data["access"]    client.credentials(        HTTP_AUTHORIZATION=f"Bearer {old_access}"    )    # Simulate a security event that revokes old token versions.    user.token_version += 1    user.save(update_fields=["token_version"])    response = client.get(PROFILE_URL)    assert response.status_code == 401
```

এটি বাস্তব JWT signature ও custom authentication class পরীক্ষা করে—`force_authenticate()` ব্যবহার করে না। Test-টি সফল হতে protected endpoint-এ `VersionedJWTAuthentication` সক্রিয় থাকতে হবে এবং token-এর মধ্যে `token_version` claim থাকতে হবে।

## 9. Password reset tests

Password reset-এর ক্ষেত্রে সবচেয়ে গুরুত্বপূর্ণ হলো token-এর validity, single-use behavior এবং password change-এর পরে session revocation।

তোমার reset endpoint যদি `POST /api/auth/password/forgot/` এবং `POST /api/auth/password/reset/` হয়, তাহলে test suite-এ নিচের scenario-গুলো থাকবে:

| Test                                      | প্রত্যাশিত আচরণ                            |
| ----------------------------------------- | ------------------------------------------ |
| Existing email দিয়ে forgot request       | Generic success response                   |
| Unknown email দিয়ে forgot request        | একই ধরনের generic response                 |
| Invalid reset token                       | Request প্রত্যাখ্যান                       |
| Expired reset token                       | Request প্রত্যাখ্যান                       |
| Valid token                               | Password update                            |
| একই token দ্বিতীয়বার                     | Request প্রত্যাখ্যান                       |
| Password reset-এর পরে পুরোনো password     | Login ব্যর্থ                               |
| Password reset-এর পরে পুরোনো access token | Token-version policy অনুযায়ী প্রত্যাখ্যাত |

Forgot-password response-এর জন্য উদাহরণ:

```
import pytestfrom rest_framework.test import APIClientFORGOT_URL = "/api/auth/password/forgot/"@pytest.mark.django_dbdef test_forgot_password_does_not_reveal_account_existence(user):    client = APIClient()    existing_response = client.post(        FORGOT_URL,        {"email": user.email},        format="json",    )    unknown_response = client.post(        FORGOT_URL,        {"email": "unknown-account@example.com"},        format="json",    )    assert existing_response.status_code == unknown_response.status_code    assert existing_response.data == unknown_response.data
```

এটি response body ও status-এর সমতা পরীক্ষা করে; production-এ response timing-ও যথাসম্ভব কাছাকাছি রাখা দরকার। Throttling, asynchronous email sending বা অন্য side effect থাকলে test isolation ঠিক রাখতে হবে।

Valid password-reset test লেখার জন্য তোমার `password_reset_service.py`-এর token-creation ও validation interface ব্যবহার করো। Reset token-এর internal format অনুমান করে test লেখা উচিত নয়।

## 10. RBAC এবং object-level permission tests

এখন যাচাই করব, সাধারণ user অন্য user-এর profile বা admin endpoints-এ অনুমতি ছাড়া প্রবেশ করতে পারে কি না।

### Test A — নিজের profile পড়তে পারবে

```
import pytestfrom rest_framework.test import APIClientPROFILE_URL = "/api/auth/profile/"@pytest.mark.django_dbdef test_authenticated_user_can_read_own_profile(user):    client = APIClient()    client.force_authenticate(user=user)    response = client.get(PROFILE_URL)    assert response.status_code == 200
```

### Test B — সাধারণ user admin endpoint access করতে পারবে না

```
import pytestfrom rest_framework.test import APIClientADMIN_USERS_URL = "/api/auth/admin/users/"@pytest.mark.django_dbdef test_regular_user_cannot_list_admin_users(user):    client = APIClient()    client.force_authenticate(user=user)    response = client.get(ADMIN_USERS_URL)    assert response.status_code == 403
```

এই test ধরে নিচ্ছে `USER` role-এর user-এর জন্য endpoint-এ access নিষিদ্ধ। তোমার project যদি authentication failure-এর জন্য 401 দেয়, তবে unauthenticated access-এর আলাদা test লিখবে।

### Test C — User অন্য user-এর profile edit করতে পারবে না

```
import pytestfrom rest_framework.test import APIClientPROFILE_DETAIL_URL = "/api/auth/profiles/{}/"@pytest.mark.django_dbdef test_user_cannot_edit_another_users_profile(user, second_user):    client = APIClient()    client.force_authenticate(user=user)    response = client.patch(        PROFILE_DETAIL_URL.format(second_user.pk),        {"display_name": "Unauthorized change"},        format="json",    )    assert response.status_code in (403, 404)
```

তোমার profile model/serializer-এ `display_name` না থাকলে একটি বাস্তব editable field ব্যবহার করবে। এখানে 403 বা 404 দুটোই গ্রহণযোগ্য হতে পারে, কারণ কিছু API resource existence প্রকাশ না করার জন্য 404 ফেরায়।

RBAC-এর জন্য আরও test করো:

- STAFF-এর অনুমতি আছে এমন কাজ করতে পারে, কিন্তু ADMIN-only কাজ নয়।
- ADMIN role change করতে পারে; সাধারণ user পারে না।
- User নিজের role PATCH করে ADMIN হতে পারে না।
- Disabled/inactive user protected endpoints-এ প্রবেশ করতে পারে না।
- Object-level permission queryset filtering-এর মাধ্যমে অন্য user-এর data expose করে না।

## 11. Rate limiting tests

DRF throttling test-এ request সংখ্যা ও status code যাচাই করব। Test isolation-এর জন্য Django cache reset করা এবং test-এ নির্দিষ্ট throttle rate ব্যবহার করা সুবিধাজনক।

`accounts/tests/test_throttling.py`:

```
import pytestfrom django.core.cache import cachefrom rest_framework import statusfrom rest_framework.test import APIClient, override_settingsLOGIN_URL = "/api/auth/login/"@pytest.mark.django_db@override_settings(    REST_FRAMEWORK={        "DEFAULT_THROTTLE_CLASSES": [            "rest_framework.throttling.ScopedRateThrottle",        ],        "DEFAULT_THROTTLE_RATES": {            "login": "2/minute",        },    })def test_login_endpoint_is_throttled(user):    cache.clear()    client = APIClient()    for _ in range(2):        client.post(            LOGIN_URL,            {                "email": user.email,                "password": "Wrong-Password-For-Test!",            },            format="json",        )    response = client.post(        LOGIN_URL,        {            "email": user.email,            "password": "Wrong-Password-For-Test!",        },        format="json",    )    assert response.status_code == status.HTTP_429_TOO_MANY_REQUESTS
```

এই test-এর শর্ত: Login view-এ `ScopedRateThrottle` এবং `throttle_scope = "login"` থাকতে হবে। অন্য throttle class বা caching backend ব্যবহার করলে test সেই configuration অনুযায়ী পরিবর্তন করবে।

আরও নির্ভরযোগ্য production throttling-এর জন্য Redis-ভিত্তিক shared cache ব্যবহার করো। Django-এর সাধারণ cache throttling একাধিক instance জুড়ে strict atomic security limit নিশ্চিত করে না।

## 12. সব test চালানো ও coverage দেখা

Project root থেকে:

```
pytest
```

Coverage report:

```
pytest --cov=accounts --cov-report=term-missing
```

HTML report:

```
pytest --cov=accounts --cov-report=html
```

Coverage-এর একটি প্রাথমিক threshold নির্ধারণ করতে পারো:

```
pytest --cov=accounts --cov-report=term-missing --cov-fail-under=80
```

`80%` শুধু উদাহরণ। বেশি coverage থাকলেই security নিশ্চিত হয় না—গুরুত্বপূর্ণ failure scenarios-এ assertions আছে কি না সেটিও যাচাই করতে হবে।

প্রথমে test suite-টি ছোট ছোট অংশে চালাও:

```
pytest accounts/tests/test_registration.py -q
pytest accounts/tests/test_login.py -q
pytest accounts/tests/test_jwt_lifecycle.py -q
pytest accounts/tests/test_permissions.py -q
pytest accounts/tests/test_throttling.py -q
```

যদি failure হয়, endpoint URL, response structure, custom User manager, email verification service এবং SimpleJWT configuration-এর সঙ্গে test মিলিয়ে দেখো। Test পাস করানোর জন্য security assertion সরিয়ে ফেলবে না।

## 13. GitHub Actions CI-তে যুক্ত করা

এবার আগের Lesson 11-এর CI pipeline-এ pytest যোগ করব।

`.github/workflows/ci.yml`:

```
name: Authentication Security CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

permissions:
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:16
        env:
          POSTGRES_DB: auth_test
          POSTGRES_USER: auth_test_user
          POSTGRES_PASSWORD: test-only-password
        ports:
          - 5432:5432
        options: >-
          --health-cmd "pg_isready -U auth_test_user -d auth_test"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    env:
      DEBUG: "False"
      DJANGO_SECRET_KEY: "ci-only-not-a-production-secret"
      DJANGO_ALLOWED_HOSTS: "localhost,127.0.0.1"
      DATABASE_URL: "postgres://auth_test_user:test-only-password@localhost:5432/auth_test"
      EMAIL_BACKEND: "django.core.mail.backends.locmem.EmailBackend"

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
          cache: "pip"
          cache-dependency-path: requirements-dev.txt

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements-dev.txt

      - name: Check dependency vulnerabilities
        run: pip-audit -r requirements.txt

      - name: Django deployment checks
        run: python manage.py check --deploy

      - name: Check migrations
        run: python manage.py makemigrations --check --dry-run

      - name: Run database migrations
        run: python manage.py migrate --noinput

      - name: Run authentication tests
        run: |
          pytest \
            --cov=accounts \
            --cov-report=term-missing \
            --cov-fail-under=80

      - name: Upload coverage report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: authentication-coverage
          path: coverage.xml
          if-no-files-found: ignore
```

`coverage.xml` তৈরি করতে pytest command-এ `--cov-report=xml:coverage.xml` যোগ করো:

```
      - name: Run authentication tests
        run: |
          pytest \
            --cov=accounts \
            --cov-report=term-missing \
            --cov-report=xml:coverage.xml \
            --cov-fail-under=80
```

### CI configuration-এর গুরুত্বপূর্ণ বিষয়

এই workflow-এর জন্য কয়েকটি বিষয় তোমার project অনুযায়ী ঠিক করতে হবে:

1. `DATABASE_URL` যদি Django settings সরাসরি ব্যবহার না করে, তাহলে `settings.py`-তে তোমার ব্যবহৃত database environment variables অনুযায়ী configuration দিতে হবে।
2. `requirements-dev.txt`-এ `requirements.txt`, pytest, pytest-django এবং pytest-cov থাকতে হবে।
3. `check --deploy`-এর warnings পর্যালোচনা করবে। CI-তে warning থাকলেই অন্ধভাবে ignore করবে না।
4. উদাহরণে GitHub Actions-এর major-version tags ব্যবহার করা হয়েছে; production workflow-এ action versions review করে commit SHA-তে pin করা আরও নিরাপদ।
5. CI test database-এর password শুধু test environment-এর জন্য। কখনো production database credentials এখানে ব্যবহার করবে না।

## 14. CI সফল না হলে deployment বন্ধ রাখো

আগের Lesson-এ তোমার build/deploy job ছিল। সেটিকে test job-এর ওপর নির্ভরশীল করো:

```
  build-and-deploy:
    needs: test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest

    steps:
      - name: Build and deploy
        run: echo "Connect your existing GHCR and VPS deployment steps here"
```

এটি শুধু dependency-এর উদাহরণ; তোমার আগের GHCR build ও VPS deployment steps-এর জায়গায় বাস্তব steps থাকবে। `needs: test` নিশ্চিত করে test job সফল না হলে deployment job শুরু হবে না। এখানে `echo`-কে বাস্তব deployment হিসেবে ধরে নেবে না।

Production branch-এ GitHub branch protection বা ruleset চালু করে required status check হিসেবে `test` নির্বাচন করো। তাহলে pull request-এ security tests ব্যর্থ হলে merge-ও আটকে রাখা যাবে।

## 15. End-to-end authentication test matrix

শেষে এই matrix ধরে নিশ্চিত করো যে গুরুত্বপূর্ণ flow-গুলোর success ও failure—দুটিই পরীক্ষা করা হয়েছে।

| Feature            | Success test            | Security/failure test                  |
| ------------------ | ----------------------- | -------------------------------------- |
| Registration       | User তৈরি               | Duplicate email, privilege injection   |
| Email verification | Valid token             | Invalid, expired, reused token         |
| Login              | Valid credentials       | Wrong password, unverified user        |
| JWT refresh        | নতুন access token       | Expired, revoked, reused refresh token |
| Logout             | Refresh token revoke    | Logout-এর পরে refresh প্রত্যাখ্যাত     |
| Password reset     | Password পরিবর্তন       | Invalid/expired/reused token           |
| Token revocation   | পুরোনো token বাতিল      | পুরোনো access token প্রত্যাখ্যাত       |
| RBAC               | Authorized role allowed | Unauthorized role denied               |
| Object permissions | নিজের resource access   | অন্য user-এর resource blocked          |
| Rate limiting      | Limit-এর মধ্যে request  | Limit অতিক্রমে HTTP 429                |
| CI                 | Tests pass              | Test failure-এ deployment blocked      |

## 16. Final checklist

## Lesson 16 completion

0/11

pytest configuration ও shared fixtures তৈরি

Registration এবং login tests পাস

Email verification-এর valid/invalid/expired token tests সম্পন্ন

JWT refresh, logout এবং token-version revocation যাচাই

Password reset-এর single-use ও expiration tests পাস

RBAC এবং object-level permissions পরীক্ষা

Rate limiting test ও cache isolation যাচাই

pip-audit CI pipeline-এ যুক্ত

GitHub Actions-এ pytest ও coverage report চালু

Production deployment job test job-এর ওপর নির্ভরশীল

Staging-এ সম্পূর্ণ authentication flow smoke test

### এই Lesson-এর সবচেয়ে গুরুত্বপূর্ণ শিক্ষা

একটি authentication system নিরাপদ কি না তা শুধু login সফল হওয়া দিয়ে বোঝা যায় না। Password reset-এর পরে পুরোনো token কাজ করছে কি না, সাধারণ user admin role নিতে পারছে কি না, একই verification token আবার ব্যবহার করা যাচ্ছে কি না—এসব failure case-ও পরীক্ষা করতে হবে।

আরেকটি কথা: এখানে দেওয়া test suite একটি শক্তিশালী starting point, কিন্তু তোমার project-এর সব test বাস্তবে run না করা পর্যন্ত একে সম্পূর্ণ বা verified বলা যাবে না। বিশেষ করে email token service, password reset service এবং logout implementation-এর সঙ্গে test-গুলো মিলিয়ে নিতে হবে।

পরবর্তী Lesson 17: Authentication API-এর Load Testing & Performance Engineering — Locust দিয়ে concurrent login/refresh traffic, PostgreSQL connection pressure, Redis throttling, p95/p99 latency এবং Gunicorn worker tuning; তারপর performance regression-কে CI/CD-তে কীভাবে ধরতে হয়।

----
# Lesson 17: Authentication API Load Testing & Performance Engineering

এই Lesson-এ আমরা `complete_auth_project`-এর Django REST Framework authentication API-তে concurrent traffic তৈরি করব, bottleneck খুঁজব এবং performance regression হলে CI/CD-তে deployment আটকে দেওয়ার ব্যবস্থা করব।

আমাদের আগের project-এর architecture ধরে এগোব: Django REST Framework + Gunicorn + PostgreSQL + Redis + Nginx + JWT।

## Lesson শেষে যা তৈরি হবে

1\. Locust load tests

Concurrent login, JWT refresh, protected profile requests ও mixed authentication traffic।

2\. PostgreSQL ও Redis bottleneck analysis

Database connection saturation, slow query, cache/throttling behavior ও resource pressure।

3\. Latency ও Gunicorn tuning

p50/p95/p99 latency, throughput, worker count এবং timeout configuration।

4\. CI/CD performance regression gate

নির্ধারিত latency ও error-rate threshold অতিক্রম করলে build-কে fail করানো।

## 1. Load testing-এর আগে কয়েকটি ধারণা

| Metric           | অর্থ                                          |
| ---------------- | --------------------------------------------- |
| Concurrent users | একই সময়ে কতজন virtual user কাজ করছে          |
| RPS              | প্রতি সেকেন্ডে কতটি request সম্পন্ন হচ্ছে     |
| p50 latency      | ৫০% request এই সময়ের মধ্যে সম্পন্ন হয়       |
| p95 latency      | ৯৫% request এই সময়ের মধ্যে সম্পন্ন হয়       |
| p99 latency      | ৯৯% request এই সময়ের মধ্যে সম্পন্ন হয়       |
| Error rate       | মোট request-এর মধ্যে ব্যর্থ request-এর অনুপাত |
| Throughput       | নির্দিষ্ট সময়ে সফলভাবে সম্পন্ন কাজের পরিমাণ  |

p95 ও p99 কেন গুরুত্বপূর্ণ? Average latency ভালো হলেও অল্প কিছু request অনেক ধীর হতে পারে। Tail latency ধরতে p95/p99 দেখা জরুরি।

উদাহরণ: p95 যদি 300 ms হয়, তার মানে ৯৫% request প্রায় 300 ms বা তার কম সময়ে শেষ হয়েছে; বাকি ৫% এর বেশি সময় নিয়েছে।

## 2. Test environment প্রস্তুত করা

Production server-এ সরাসরি heavy load test চালাবে না। প্রথমে staging environment ব্যবহার করো, যেখানে:

- Production-এর কাছাকাছি Gunicorn worker configuration থাকবে।
- PostgreSQL ও Redis ব্যবহৃত হবে।
- Nginx এবং TLS path পরীক্ষা করা যাবে।
- Test-only accounts থাকবে।
- Email verification ও password reset test-এর জন্য real email delivery বন্ধ থাকবে।
- Load generator এবং application server-এর CPU/RAM আলাদা করে পর্যবেক্ষণ করা যাবে।

Load testing-এর সময় বাস্তব ব্যবহারকারীর account, production password বা real refresh token ব্যবহার করবে না।

## 3. Locust install ও project structure

Project root-এ আলাদা load-testing folder তৈরি করো:

```
complete_auth_project/
├── accounts/
├── config/
├── loadtests/
│   ├── locustfile.py
│   └── README.md
├── requirements.txt
└── requirements-dev.txt
```

Locust আলাদা development dependency হিসেবে install করো:

```
pip install locust
```

`requirements-dev.txt`-এ যোগ করো:

```
locust
```

Load generator-কে application container-এর মধ্যে চালানো বাধ্যতামূলক নয়। আলাদা machine/container থেকে চালালে application-এর CPU ও Locust-এর CPU usage আলাদা করে বোঝা সহজ হয়।

## 4. Locust দিয়ে login, refresh ও profile load test

আমাদের API endpoints:

- `POST /api/auth/login/`
- `POST /api/auth/token/refresh/`
- `GET /api/auth/profile/`

প্রথমে staging-এ test accounts তৈরি করো। প্রতিটি virtual user-এর জন্য আলাদা account ব্যবহার করা ভালো, কারণ refresh-token rotation-এ একই account-এর token একাধিক virtual user একসঙ্গে ব্যবহার করলে token-reuse conflict হতে পারে।

### `loadtests/locustfile.py`

```
import itertoolsimport osfrom locust import HttpUser, between, task# Accounts must already exist in the staging database.# Example:# LOADTEST_EMAIL_PREFIX=loadtest# LOADTEST_EMAIL_DOMAIN=example.test# LOADTEST_PASSWORD=<test-only-password>## User 0: loadtest0@example.test# User 1: loadtest1@example.test# User 2: loadtest2@example.testUSER_COUNTER = itertools.count()EMAIL_PREFIX = os.getenv("LOADTEST_EMAIL_PREFIX", "loadtest")EMAIL_DOMAIN = os.getenv("LOADTEST_EMAIL_DOMAIN", "example.test")PASSWORD = os.environ["LOADTEST_PASSWORD"]class AuthenticationUser(HttpUser):    wait_time = between(1, 3)    def on_start(self):        self.access_token = None        self.refresh_token = None
```

### এই script কী করছে?

- প্রতিটি virtual user শুরুতে login করে।
- Profile endpoint-এ বেশি request পাঠায়।
- Refresh endpoint-এ কম request পাঠায়।
- Refresh response-এ নতুন refresh token এলে সেটি সংরক্ষণ করে।
- Login/refresh failure-কে Locust statistics-এ failure হিসেবে দেখায়।

দুটি গুরুত্বপূর্ণ সতর্কতা:

1. `USER_COUNTER` একটি সাধারণ process-local counter। Single Locust process-এ এটি সুবিধাজনক; distributed Locust workers চালালে আলাদা worker একই email তৈরি করতে পারে। Distributed testing-এর জন্য account allocation-কে worker ID বা আলাদা CSV partition অনুযায়ী unique করতে হবে।
2. Login rate limit যদি খুব কম হয়, `login_again` task-এর কারণে HTTP 429 আসতে পারে। এটি ইচ্ছাকৃত authentication-abuse test হলে ঠিক; সাধারণ throughput test হলে login rate ও throttling policy আলাদাভাবে configure করো।

`on_start()`-এ login ব্যর্থ হলেও Locust user চলতে থাকবে, কিন্তু তার protected requests বাদ যাবে। তাই benchmark শুরু করার আগে test accounts ও credentials সঠিক কি না নিশ্চিত করো।

## 5. Test account প্রস্তুত করা

Staging database-এ Locust-এর virtual users-এর সমান বা তার চেয়ে বেশি account তৈরি করো। উদাহরণ হিসেবে Django management shell ব্যবহার করতে পারো:

```
python manage.py shell
```

```
from accounts.models import Userpassword = "Replace-With-Your-Load-Test-Only-Password!"for i in range(200):    email = f"loadtest{i}@example.test"    if not User.objects.filter(email=email).exists():        User.objects.create_user(            email=email,            password=password,            email_verified=True,        )
```

এই snippet ধরে নিচ্ছে তোমার `User` model-এ `email_verified` field আছে এবং manager-এর `create_user()` এই arguments গ্রহণ করে। Test environment-এর বাইরে এটি চালাবে না। বাস্তব load test-এ account তৈরির জন্য আলাদা management command ব্যবহার করলে পুনরায় চালানো, cleanup ও account count যাচাই সহজ হবে।

এখানে email verification আগে থেকেই true করা হয়েছে, যাতে test traffic login/refresh-এর performance মাপে; email delivery-এর latency নয়।

## 6. প্রথম load test চালানো

Staging server-এ test accounts প্রস্তুত হওয়ার পরে Locust command:

```
export LOADTEST_PASSWORD='Replace-With-Your-Load-Test-Only-Password!'
export LOADTEST_EMAIL_PREFIX='loadtest'
export LOADTEST_EMAIL_DOMAIN='example.test'

locust -f loadtests/locustfile.py \
  --host https://staging-api.example.test
```

Browser-এ Locust-এর web UI খুলে users ও spawn rate নির্ধারণ করতে পারো। অথবা headless mode:

```
locust -f loadtests/locustfile.py \
  --host https://staging-api.example.test \
  --headless \
  --users 20 \
  --spawn-rate 2 \
  --run-time 3m \
  --csv loadtests/results/baseline
```

প্রথম run-এ ২০ virtual users ও ৩ মিনিট একটি উদাহরণমাত্র—তোমার staging capacity অনুযায়ী আরও কম থেকে শুরু করো। Output directory আগে তৈরি করতে হবে:

```
mkdir -p loadtests/results
```

এরপর ধাপে ধাপে traffic বাড়াও: যেমন 5 → 10 → 20 → 40 virtual users। প্রতিটি ধাপে error rate, p95/p99 latency, CPU, memory এবং database connections পর্যবেক্ষণ করো। কোনো ধাপে error rate দ্রুত বাড়লে আরও load বাড়ানোর পরিবর্তে থেমে bottleneck খুঁজে বের করো।

## 7. p95/p99 latency ও throughput বিশ্লেষণ

Locust-এর Statistics tab বা CSV output-এ request-এর response time percentile দেখা যায়। আমরা সাধারণত তিনটি স্তরে performance মাপব:

- Baseline: খুব কম traffic-এ latency কত?
- Expected load: বাস্তবসম্মত concurrent traffic-এ latency কত?
- Stress test: কোন পর্যায়ে latency বা error rate অগ্রহণযোগ্য হয়ে ওঠে?

উদাহরণস্বরূপ, একটি staging run-এর hypothetical ফল:

| Metric          | Baseline | Higher load |
| --------------- | -------- | ----------- |
| p50             | 70 ms    | 110 ms      |
| p95             | 160 ms   | 420 ms      |
| p99             | 260 ms   | 950 ms      |
| HTTP error rate | 0.1%     | 1.8%        |

এগুলো শুধু উদাহরণ, বাস্তব test result নয়। Higher load-এ p99 অনেক বেড়ে গেলে request queueing, database contention, CPU saturation অথবা rate limiting পরীক্ষা করতে হবে।

শুধু average response time দেখে সিদ্ধান্ত নেবে না। Authentication endpoint-এ password hashing-এর খরচ, database writes, token blacklist queries এবং throttling cache access latency-কে প্রভাবিত করতে পারে।

## 8. PostgreSQL connection pressure পরীক্ষা

Concurrent requests বাড়লে Gunicorn workers থেকে PostgreSQL-এ connection বাড়তে পারে। PostgreSQL-এর `max_connections` অসীম নয়, আর প্রতিটি connection-এরও resource cost আছে।

### ধাপ 1 — Active connections দেখো

Staging database-এ চালাও:

```
SELECT
    state,
    COUNT(*) AS connection_count
FROM pg_stat_activity
WHERE datname = current_database()
GROUP BY state
ORDER BY connection_count DESC;
```

এতে current database-এর connections state অনুযায়ী দেখা যাবে।

Connection limit ও usage দেখো:

```
SHOW max_connections;
```

```
SELECT
    COUNT(*) AS current_connections,
    current_setting('max_connections')::int AS max_connections
FROM pg_stat_activity;
```

এই query-তে `pg_stat_activity`-এর সব database connection গণনা হয়; নির্দিষ্ট database-এর connection দেখতে চাইলে `WHERE datname = current_database()` যোগ করো।

### ধাপ 2 — Slow queries খুঁজে বের করা

`pg_stat_statements` extension আগে থেকে configure করা থাকলে query statistics দেখতে পারো:

```
SELECT
    calls,
    ROUND(mean_exec_time::numeric, 2) AS mean_ms,
    ROUND(max_exec_time::numeric, 2) AS max_ms,
    LEFT(query, 120) AS query_sample
FROM pg_stat_statements
ORDER BY mean_exec_time DESC
LIMIT 10;
```

এটি চালাতে extension install/enable থাকতে হবে এবং database configuration-এ `pg_stat_statements` preload করা লাগতে পারে। Production-এ query text-এ sensitive data থাকার সম্ভাবনা মাথায় রেখে output access সীমিত রাখবে।

### ধাপ 3 — Database connection budget

উদাহরণস্বরূপ, তোমার API-তে ৩টি application instances এবং প্রতিটিতে ৪টি Gunicorn workers থাকলে, প্রতিটি worker-এর জন্য একটি connection ধরে নিলেই সম্ভাব্য connection demand প্রায় ১২ হতে পারে। কিন্তু বাস্তবে Django connection lifecycle, threads, async handling, background workers, admin access এবং monitoring tools-ও connections ব্যবহার করতে পারে।

তাই connection budget হিসাব করবে:

- Gunicorn workers ও threads
- Celery/background workers
- Blue-green deployment-এর দুই environment একসঙ্গে চালু থাকার সময়
- Monitoring ও migration processes
- Database admin connections
- PostgreSQL-এর নিজস্ব reserved capacity

`max_connections` বাড়ানোই সবসময় সমাধান নয়। প্রথমে connection leak, long-running transaction এবং slow query আছে কি না যাচাই করো। বড় application-এ PgBouncer-এর মতো connection pooler বিবেচনা করা যেতে পারে।

## 9. Redis throttling ও cache performance

আমাদের আগের authentication project-এ login, registration, verification ও password-reset endpoints-এ throttling আছে। Load testing-এ দুটি আলাদা পরিস্থিতি পরীক্ষা করো।

### Scenario A — স্বাভাবিক request traffic

- বৈধ login ও refresh requests চালাও।
- Redis CPU, memory এবং latency দেখো।
- Application-এর p95/p99 latency-এর সঙ্গে Redis latency তুলনা করো।
- Redis connection errors বা timeouts হচ্ছে কি না দেখো।

### Scenario B — Rate limit অতিক্রম করা

- একটি staging account বা controlled test client দিয়ে নির্দিষ্ট rate অতিক্রম করো।
- প্রত্যাশিত HTTP 429 response আসে কি না যাচাই করো।
- Rate limiting চালু থাকার কারণে বৈধ traffic অপ্রত্যাশিতভাবে block হচ্ছে কি না দেখো।

Redis-এ সাধারণ health check:

```
docker compose exec redis redis-cli PING
```

প্রত্যাশিত response:

```
PONG
```

Redis service-এর নাম `redis` না হলে actual Compose service name ব্যবহার করবে। Authentication-enabled Redis হলে credentials/configuration অনুযায়ী command চালাতে হবে; credentials shell history-তে প্রকাশ করবে না।

গুরুত্বপূর্ণ: Load testing-এ শুধু Redis দ্রুত কি না দেখা যথেষ্ট নয়। Django throttle cache key-এর behavior, expiry, cache eviction এবং multiple application instances একই Redis ব্যবহার করছে কি না—এসবও যাচাই করতে হবে।

## 10. Gunicorn worker tuning

Gunicorn worker count বাড়ালে concurrency বাড়তে পারে, কিন্তু বেশি worker মানেই বেশি performance নয়। অতিরিক্ত worker RAM ও database connections খরচ বাড়াতে পারে।

### ধাপ 1 — বর্তমান worker configuration

তোমার আগের Dockerfile-এ ছিল:

```
CMD ["gunicorn", "config.wsgi:application",
     "--bind", "0.0.0.0:8000",
     "--workers", "3",
     "--access-logfile", "-",
     "--error-logfile", "-"]
```

শুরুতে ৩টি synchronous worker একটি baseline হতে পারে; তবে উপযুক্ত worker count CPU, RAM, request duration এবং database capacity-এর ওপর নির্ভর করে।

### ধাপ 2 — Environment variable থেকে workers নির্ধারণ

Production Dockerfile-এর command-কে environment-configurable করতে shell expansion বা entrypoint script ব্যবহার করতে পারো। একটি সহজ `docker-entrypoint.sh`:

```
#!/bin/sh
set -eu

: "${GUNICORN_WORKERS:=3}"

exec gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers "$GUNICORN_WORKERS" \
    --access-logfile - \
    --error-logfile - \
    --timeout 30
```

Dockerfile:

```
COPY --chown=django:django docker-entrypoint.sh /app/
RUN chmod 755 /app/docker-entrypoint.sh

ENTRYPOINT ["/app/docker-entrypoint.sh"]
```

Compose environment:

```
services:
  web:
    environment:
      GUNICORN_WORKERS: "3"
```

এখানে `timeout 30` একটি উদাহরণ; request workload অনুযায়ী ঠিক করবে। Timeout বাড়িয়ে দিলেই slow request সমাধান হয় না—দীর্ঘস্থায়ী database queries বা blocked requests আলাদাভাবে তদন্ত করতে হবে।

### ধাপ 3 — একবারে একটি variable পরিবর্তন

নিচের test sequence অনুসরণ করো:

1. Workers = 2 দিয়ে baseline run।
2. Workers = 3 দিয়ে একই load run।
3. Workers = 4 দিয়ে একই load run।
4. প্রতিটি run-এ CPU, RSS memory, database connections, throughput এবং p95/p99 তুলনা করো।

একই সময়ে worker count, database pool, cache এবং query code সব পরিবর্তন করলে কোন পরিবর্তনে performance উন্নত হয়েছে বোঝা কঠিন হবে।

## 11. Performance regression gate তৈরি করা

এখন এমন ব্যবস্থা তৈরি করব যাতে নতুন code আগের তুলনায় ধীর হয়ে গেলে CI warning বা failure দিতে পারে।

প্রথমে baseline নির্ধারণ করো। উদাহরণস্বরূপ:

- p95 latency ≤ 300 ms
- HTTP failure rate ≤ 1%
- Minimum throughput নির্ধারিত workload-এর সঙ্গে সামঞ্জস্যপূর্ণ

এগুলো উদাহরণমাত্র; staging-এর বাস্তব measurements ও business requirements অনুযায়ী threshold ঠিক করবে। Load test চলাকালে 429 response ইচ্ছাকৃত হলে সেটিকে সাধারণ server failure-এর সঙ্গে আলাদাভাবে বিশ্লেষণ করতে হবে।

### ধাপ 1 — Locust CSV output তৈরি

```
mkdir -p loadtests/results

locust -f loadtests/locustfile.py \
  --host https://staging-api.example.test \
  --headless \
  --users 20 \
  --spawn-rate 2 \
  --run-time 3m \
  --csv loadtests/results/auth-baseline \
  --csv-full-history
```

এই command-এ সাধারণত `auth-baseline_stats.csv` এবং history CSV-সহ output তৈরি হবে। Locust version অনুযায়ী CSV fields যাচাই করে script লিখবে।

### ধাপ 2 — Threshold checker

`loadtests/check_performance.py`:

```
import csvimport osimport sysfrom pathlib import Pathstats_file = Path(    sys.argv[1] if len(sys.argv) > 1    else "loadtests/results/auth-baseline_stats.csv")max_p95_ms = float(os.getenv("MAX_P95_MS", "300"))max_failure_rate_pct = float(    os.getenv("MAX_FAILURE_RATE_PCT", "1.0"))if not stats_file.exists():    raise SystemExit(f"Missing Locust stats file: {stats_file}")with stats_file.open(newline="", encoding="utf-8") as file:    rows = list(csv.DictReader(file))if not rows:    raise SystemExit("Locust stats CSV is empty.")# Prefer the Locust aggregate row when available.aggregate = next(    (row for row in rows if row.get("Name") == "Aggregated"),    None,)if aggregate is None:    raise SystemExit(        "No Aggregated row found; inspect CSV schema for your Locust version."    )requests = int(aggregate.get("# requests") or 0)failures = int(aggregate.get("# failures") or 0)if requests == 0:    raise SystemExit("No requests were recorded.")p95 = float(aggregate.get("95%") or 0)failure_rate_pct = failures / requests * 100print(f"Requests: {requests}")print(f"Failures: {failures}")print(f"p95 latency: {p95:.2f} ms")print(f"Failure rate: {failure_rate_pct:.2f}%")problems = []if p95 > max_p95_ms:    problems.append(        f"p95 {p95:.2f} ms exceeds {max_p95_ms:.2f} ms"    )if failure_rate_pct > max_failure_rate_pct:    problems.append(        f"Failure rate {failure_rate_pct:.2f}% exceeds "        f"{max_failure_rate_pct:.2f}%"    )if problems:    print("PERFORMANCE GATE FAILED")    for problem in problems:        print(f"- {problem}")    raise SystemExit(1)print("PERFORMANCE GATE PASSED")
```

CSV schema আগে যাচাই করবে: তোমার Locust version-এর aggregate row এবং percentile column নাম ঠিক এই রকম কি না নিশ্চিত হও। কিছু version-এ header format আলাদা হতে পারে। Script threshold-এর বেশি latency বা failure rate পেলে non-zero exit code দেয়।

চালাও:

```
MAX_P95_MS=300 \
MAX_FAILURE_RATE_PCT=1.0 \
python loadtests/check_performance.py \
  loadtests/results/auth-baseline_stats.csv
```

## 12. GitHub Actions-এ performance test যুক্ত করা

Full load test প্রতিটি pull request-এ চালানো সবসময় ভালো নয়—এটি resource-intensive এবং shared staging environment-এ noise তৈরি করতে পারে। তাই দুই ধরনের test রাখব:

- PR CI: Unit tests, security tests এবং lightweight regression checks।
- Staging performance workflow: Scheduled বা manual load test, যেখানে নির্দিষ্ট workload ও threshold ব্যবহার করা হবে।

`.github/workflows/performance.yml`:

```
name: Staging Authentication Performance

on:
  workflow_dispatch:
  schedule:
    - cron: "30 20 * * 1-5"

permissions:
  contents: read

concurrency:
  group: staging-auth-performance
  cancel-in-progress: false

jobs:
  load-test:
    runs-on: ubuntu-latest
    environment: staging
    timeout-minutes: 15

    env:
      LOADTEST_PASSWORD: ${{ secrets.LOADTEST_PASSWORD }}
      LOADTEST_EMAIL_PREFIX: "loadtest"
      LOADTEST_EMAIL_DOMAIN: "example.test"
      MAX_P95_MS: "300"
      MAX_FAILURE_RATE_PCT: "1.0"

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
          cache: "pip"
          cache-dependency-path: requirements-dev.txt

      - name: Install test dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements-dev.txt

      - name: Prepare result directory
        run: mkdir -p loadtests/results

      - name: Run staging load test
        env:
          STAGING_API_URL: ${{ secrets.STAGING_API_URL }}
        run: |
          test -n "$STAGING_API_URL"
          test -n "$LOADTEST_PASSWORD"

          locust -f loadtests/locustfile.py \
            --host "$STAGING_API_URL" \
            --headless \
            --users 20 \
            --spawn-rate 2 \
            --run-time 3m \
            --csv loadtests/results/auth \
            --csv-full-history

      - name: Enforce performance thresholds
        run: |
          python loadtests/check_performance.py \
            loadtests/results/auth_stats.csv

      - name: Upload Locust results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: authentication-performance-results
          path: loadtests/results/
          if-no-files-found: warn
          retention-days: 14
```

### Workflow চালানোর আগে

1. GitHub repository-তে `LOADTEST_PASSWORD` ও `STAGING_API_URL` secrets যোগ করো।
2. Staging database-এ অন্তত ২০টি matching load-test account তৈরি করো।
3. Locust generator থেকে staging endpoint-এ network access আছে কি না নিশ্চিত করো।
4. Staging-এর জন্য আলাদা test accounts ও data ব্যবহার করো।
5. Scheduled run-এর সময় একই staging environment-এ অন্য load test চলতে দিও না।

Cron schedule UTC-তে নির্ধারিত। GitHub Actions scheduled runs ঠিক নির্দিষ্ট মুহূর্তে চলার নিশ্চয়তা দেয় না। আর performance workflow-টি production-এ নয়, staging-এ চালাবে।

## 13. Load test-এর ফল থেকে bottleneck নির্ণয়

CPU বেশি, throughput আর বাড়ছে না

Password hashing, serialization বা Python worker saturation পরীক্ষা করো। CPU ও worker count একসঙ্গে দেখো।

Database connections বেশি, latency বাড়ছে

Connection lifecycle, slow queries, long transactions ও connection pooling যাচাই করো।

Redis latency বা HTTP 429 বাড়ছে

Shared cache, throttle configuration, cache contention এবং load-test traffic pattern যাচাই করো।

p99 অনেক বেশি, কিন্তু p50 ভালো

Occasional slow query, worker queueing, garbage collection, network delays এবং resource contention খুঁজে দেখো।

একটি performance regression দেখলে সরাসরি worker সংখ্যা বাড়াবে না। প্রথমে একই workload-এ আগের baseline-এর সঙ্গে নতুন ফল তুলনা করো; তারপর একটি করে configuration পরিবর্তন করে পুনরায় test করো।

## 14. Lesson 17 completion checklist

## Performance readiness

0/10

Staging environment-এ Locust install ও test accounts প্রস্তুত

Login, refresh ও protected profile traffic পরীক্ষা

p50, p95, p99 latency ও failure rate baseline সংরক্ষণ

PostgreSQL connection count ও slow queries পর্যবেক্ষণ

Redis throttling এবং HTTP 429 behavior যাচাই

Gunicorn workers 2, 3 ও 4-এর ফল তুলনা

Performance threshold checker CSV-তে কাজ করছে

GitHub Actions staging workflow চালু

Performance test failure হলে workflow fail হচ্ছে

Performance results artifact হিসেবে সংরক্ষিত

## এই Lesson-এর মূল শিক্ষা

Production performance engineering মানে শুধু বেশি request পাঠানো নয়। নির্দিষ্ট workload তৈরি করতে হবে, বাস্তব metrics সংগ্রহ করতে হবে, bottleneck খুঁজে বের করতে হবে এবং একই test বারবার চালিয়ে পরিবর্তনের প্রভাব যাচাই করতে হবে।

পরবর্তী Lesson 18: Authentication API-কে Production Architecture Review—Nginx reverse proxy, Gunicorn, Django, PostgreSQL, Redis, Celery, connection pooling, secrets management এবং deployment topology-কে একত্রে পর্যালোচনা করে production capacity ও failure scenarios অনুযায়ী final architecture design।

---
# Lesson 18: Authentication API — Production Architecture Review

এই Lesson-এ আমরা আগের Authentication API lessons-এর সবকিছু একসঙ্গে পর্যালোচনা করে একটি বাস্তবসম্মত production architecture তৈরি করব। লক্ষ্য শুধু Django API চালানো নয়—বরং এমন একটি সিস্টেম তৈরি করা, যা একাধিক application instance, database connection pressure, Redis failure, Celery worker failure, deployment এবং traffic বৃদ্ধির সময়ও নির্ভরযোগ্যভাবে কাজ করতে পারে।

আমাদের project: `complete_auth_project`

আগের architecture-এ আমরা Django REST Framework, custom User model, JWT authentication, email verification, password reset, role-based permissions, Docker deployment, CI/CD এবং Locust load testing নিয়ে কাজ করেছি। এবার এগুলোকে একটি production system-এর মধ্যে সাজাব।

## 1. Final architecture: পুরো system কীভাবে কাজ করবে?

Client applications

React / Next.js / Mobile App

HTTPS · TLS

Nginx reverse proxy

TLS · request limits · proxy headers · routing

Internal Docker network

Django API tier

API 1

Gunicorn + Django

API 2

Gunicorn + Django

একই version-এর application instances; প্রয়োজনে load balancer

Queries

PostgreSQL

Users · tokens · business data

Cache / broker

Redis

Cache · throttling · Celery broker

Asynchronous jobs

Celery worker

Verification email · password-reset email · retries

প্রয়োজনে আলাদা monitoring, error tracking, backup এবং secret-management services যুক্ত হবে। Diagram-টি logical architecture; production-এ Redis-এর workload ও failure domain অনুযায়ী আলাদা instance ব্যবহার করা যেতে পারে।

### প্রতিটি component-এর দায়িত্ব

| Component         | মূল দায়িত্ব                                                                      |
| ----------------- | -------------------------------------------------------------------------------- |
| Nginx             | HTTPS termination, reverse proxy, request-size limits                            |
| Gunicorn          | Django application-এর worker process পরিচালনা                                    |
| Django + DRF      | Authentication, authorization, validation, API business logic                    |
| PostgreSQL        | স্থায়ী ও authoritative data storage                                              |
| Redis             | Cache, shared throttling state এবং Celery broker—যদি একই instance ব্যবহার করা হয় |
| Celery            | Email ও অন্যান্য দীর্ঘ সময়ের কাজ background-এ করা                                |
| Connection pooler | PostgreSQL connection সংখ্যা নিয়ন্ত্রণ, প্রয়োজনে PgBouncer                       |
| Monitoring        | Latency, error rate, resource pressure এবং alerts                                |
| Backup            | Database recovery ও disaster recovery                                            |

গুরুত্বপূর্ণ: Redis cache-এর data হারানো সহনীয় হতে পারে, কিন্তু Celery queue-এর data হারানো সবসময় সহনীয় নয়। একই Redis instance-এ দুটো workload রাখলে capacity, persistence, eviction policy এবং failure impact ভালোভাবে বিবেচনা করতে হবে।

## 2. Docker Compose deployment topology

শুরুতে একটি Ubuntu VPS-এ এই topology দিয়ে শেখা ও deploy করা সম্ভব:

- `nginx`: public HTTP/HTTPS entry point
- `api`: Gunicorn ও Django
- `celery_worker`: asynchronous jobs
- `db`: PostgreSQL
- `redis`: cache, throttling ও broker
- `pgbouncer`: database connection pooling, প্রয়োজন হলে

Production-এ managed PostgreSQL/Redis বা আলাদা server ব্যবহার করলে database ও cache-এর failure domain application server থেকে আলাদা রাখা যায়। Docker Compose একাই high availability নিশ্চিত করে না; একই VPS-এর host failure হলে একই host-এ থাকা সব container একসঙ্গে unavailable হতে পারে।

## 3. Nginx reverse proxy: নিরাপদ entry point

Nginx-এর সামনে দিয়ে সব public request যাবে। Django/Gunicorn port সরাসরি internet-এ expose করা উচিত নয়।

উদাহরণ: `deploy/nginx/conf.d/api.conf`

```
upstream django_api {
    server api:8000;
    keepalive 32;
}

server {
    listen 80;
    server_name api.example.com;

    # HTTPS configuration চালু থাকলে HTTP থেকে redirect
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    http2 on;

    server_name api.example.com;

    ssl_certificate     /etc/letsencrypt/live/api.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/api.example.com/privkey.pem;

    client_max_body_size 2m;

    location / {
        proxy_pass http://django_api;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_connect_timeout 5s;
        proxy_read_timeout 35s;
        proxy_send_timeout 35s;

        proxy_set_header Connection "";
    }
}
```

এখানে `example.com`-কে নিজের domain দিয়ে প্রতিস্থাপন করবে। Certificate file-গুলো আগে তৈরি থাকতে হবে; নইলে Nginx শুরু হবে না।

### Nginx-এ rate limiting

Authentication endpoints-এ অতিরিক্ত request নিয়ন্ত্রণে Nginx-level limit একটি অতিরিক্ত সুরক্ষা স্তর হতে পারে।

`http {}` context-এ:

```
limit_req_zone $binary_remote_addr
    zone=auth_limit:10m rate=5r/s;
```

তারপর HTTPS server-এর মধ্যে:

```
location ~ ^/api/auth/(login|password/forgot)/$ {
    limit_req zone=auth_limit burst=10 nodelay;

    proxy_pass http://django_api;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Real-IP $remote_addr;
}
```

এই snippet-টি মূল proxy configuration-এর বিকল্প নয়; এখানে শুধু authentication route-এর অতিরিক্ত rule দেখানো হয়েছে। Nginx-এ client IP ঠিকভাবে নির্ণয় না করে `real_ip` configuration যোগ করবে না, এবং trusted proxy ছাড়া client-supplied forwarded IP-কে বিশ্বাস করবে না।

মনে রাখবে: IP-based limit shared office, mobile carrier NAT বা school network-এর বৈধ ব্যবহারকারীদেরও প্রভাবিত করতে পারে। Django/DRF account-aware throttling, password-hashing cost এবং monitoring-এর সঙ্গে এটি tune করতে হবে।

## 4. Gunicorn + Django: API process design

Gunicorn HTTP request-কে Django application পর্যন্ত পৌঁছায়। Worker বেশি হলেই সবসময় performance ভালো হয় না—প্রতিটি worker RAM ব্যবহার করে এবং database connection-এর চাহিদা বাড়াতে পারে।

উদাহরণ `docker-entrypoint.sh`:

```
#!/bin/sh
set -eu

: "${GUNICORN_WORKERS:=3}"
: "${GUNICORN_THREADS:=1}"
: "${GUNICORN_TIMEOUT:=30}"

exec gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers "$GUNICORN_WORKERS" \
    --threads "$GUNICORN_THREADS" \
    --timeout "$GUNICORN_TIMEOUT" \
    --access-logfile - \
    --error-logfile -
```

Dockerfile-এ entrypoint copy ও executable করার উদাহরণ:

```
COPY --chown=django:django docker-entrypoint.sh /app/docker-entrypoint.sh
RUN chmod 755 /app/docker-entrypoint.sh

ENTRYPOINT ["/app/docker-entrypoint.sh"]
```

Compose-এর API service-এ:

```
services:
  api:
    build: .
    environment:
      GUNICORN_WORKERS: "3"
      GUNICORN_THREADS: "1"
      GUNICORN_TIMEOUT: "30"
    expose:
      - "8000"
```

`expose` internal network-এ port দেখায়; এটি host-এ public port publish করে না। Nginx ও API-কে একই Docker network-এ থাকতে হবে।

### Worker সংখ্যা কীভাবে নির্ধারণ করবে?

শুরুতে 2 বা 3 worker দিয়ে benchmark করো। তারপর 2, 3, 4 worker configuration-এ একই load চালিয়ে তুলনা করো।

- CPU saturation হলে আরও worker যোগ করলে contention বাড়তে পারে।
- RAM কম হলে worker বাড়ালে out-of-memory (OOM) হতে পারে।
- Login request-এ password hashing CPU-intensive হতে পারে।
- বেশি concurrent request মানে database connection-এর চাহিদাও বাড়তে পারে।
- Sync worker দীর্ঘ network I/O-তে আটকে থাকলে latency বাড়তে পারে।

পুরোনো `2 × CPU cores + 1` formula-কে production-এর চূড়ান্ত উত্তর হিসেবে ব্যবহার করবে না। CPU, RAM, request profile, database connection budget এবং measured p95/p99 latency একসঙ্গে বিবেচনা করবে।

## 5. PostgreSQL connection pooling

প্রতিটি Django process-এর নিজস্ব database connection থাকতে পারে। ফলে Gunicorn worker ও Celery worker বাড়ালে database connection-এর সংখ্যা দ্রুত বাড়তে পারে।

ধরা যাক:

- 2টি API instance
- প্রতি instance-এ 3 Gunicorn worker
- 2টি Celery worker process

সাধারণভাবে আনুমানিক application-side connection demand:

\\[ (2 \times 3) + 2 = 8 \\]

এটি শুধু একটি সরল baseline estimate। Threads, connection reuse, background jobs, management commands, health checks এবং pooling configuration-এর কারণে বাস্তব সংখ্যা ভিন্ন হতে পারে।

### PgBouncer কোথায় বসবে?

Django API + Celery

PgBouncer

Client connections pool করে

PostgreSQL

সীমিত সংখ্যক backend connections

PgBouncer-এর `transaction` pooling mode অনেক web API-র জন্য কার্যকর হতে পারে, তবে transaction-এর বাইরে session state ধরে রাখে এমন feature-এর সঙ্গে compatibility যাচাই করতে হবে। Django-এর persistent connections, server-side cursors, prepared statements এবং session-level configuration ব্যবহারের ধরন অনুযায়ী উপযুক্ত pooling mode নির্বাচন করা জরুরি।

### Django database configuration

`config/settings.py`-এর একটি সরল উদাহরণ:

```
import osDATABASES = {    "default": {        "ENGINE": "django.db.backends.postgresql",        "NAME": os.environ["POSTGRES_DB"],        "USER": os.environ["POSTGRES_USER"],        "PASSWORD": os.environ["POSTGRES_PASSWORD"],        "HOST": os.environ.get("POSTGRES_HOST", "db"),        "PORT": os.environ.get("POSTGRES_PORT", "5432"),        "CONN_MAX_AGE": 60,        "CONN_HEALTH_CHECKS": True,    }}
```

এটি সরাসরি PostgreSQL-এ সংযোগ করার configuration। PgBouncer ব্যবহার করলে `POSTGRES_HOST` ও `POSTGRES_PORT`-এ PgBouncer-এর internal hostname ও port দেবে। Transaction pooling চালুর আগে ব্যবহৃত Django/PostgreSQL features পরীক্ষা করবে।

দুটি বিষয় আলাদা:

- `CONN_MAX_AGE`: Django-এর persistent connection কতক্ষণ পুনর্ব্যবহার করা যেতে পারে।
- PgBouncer: application client connections-কে সীমিত backend connection pool-এর সঙ্গে multiplex করে।

`CONN_MAX_AGE=60` সেট করলেই connection pool তৈরি হয় না। Connection budget গণনা করে এবং load test করে configuration ঠিক করতে হবে।

### Database connection budget

একটি বাস্তব হিসাবের জন্য নিচের সূত্র ব্যবহার করতে পারো:

\\[ C\_{\text{total}} = C\_{\text{API}} + C\_{\text{Celery}} + C\_{\text{operations}} + C\_{\text{other}} \\]

`C_total` যেন database-এর নিরাপদ connection budget অতিক্রম না করে। Blue-green deployment চলাকালে পুরোনো ও নতুন version একই সময়ে চালু থাকলে দুই version-এর connection demand-ও হিসাব করতে হবে।

## 6. Redis architecture: cache, throttling ও Celery broker

আমাদের authentication system-এ Redis তিন ধরনের কাজে ব্যবহৃত হতে পারে:

1. Cache: বারবার ব্যবহৃত data অল্প সময়ের জন্য রাখা।
2. DRF throttling: একাধিক Django instance-এ shared request counter ব্যবহার করা।
3. Celery broker: email বা অন্য background task-এর message queue করা।

সবগুলো একই Redis-এ রাখা ছোট project-এর জন্য সহজ; কিন্তু workload ও failure isolation গুরুত্বপূর্ণ হলে আলাদা Redis instance বা managed service ভালো।

### Django cache ও throttling

`config/settings.py`:

```
CACHES = {    "default": {        "BACKEND": "django.core.cache.backends.redis.RedisCache",        "LOCATION": os.environ["REDIS_CACHE_URL"],    }}
```

DRF throttle classes ব্যবহার করলে cache backend-টি shared Redis হতে হবে, যদি একাধিক API instance-এর মধ্যে rate limit সমন্বয় করতে চাও।

Security note: DRF throttling একটি সম্পূর্ণ brute-force protection system নয়। Login-এ account-aware throttling, generic error messages, monitoring এবং প্রয়োজনে edge-level controls যুক্ত করো।

### Redis failure হলে কী হবে?

Redis-কে একসঙ্গে cache ও broker হিসেবে ব্যবহার করলে একটি outage দুই ধরনের feature-এ প্রভাব ফেলতে পারে:

- Cache unavailable: cache-dependent endpoint ধীর হতে পারে বা fail করতে পারে।
- Throttling state unavailable: rate limiting কীভাবে আচরণ করবে, তা নির্দিষ্টভাবে design করতে হবে।
- Broker unavailable: নতুন Celery tasks queue করা যাবে না।
- Queue data হারালে: কিছু email বা job পুনরায় তৈরি করতে হতে পারে।

Security-sensitive endpoint-এর throttling Redis unavailable হলে silently unlimited করে দেবে—এমন সিদ্ধান্ত না নিয়ে intentional fallback policy নির্ধারণ করতে হবে। Celery broker-এর জন্যও persistence, monitoring এবং recovery plan প্রয়োজন।

## 7. Celery: email ও background tasks

Authentication API-তে email পাঠানোর জন্য request-এর মধ্যে সরাসরি SMTP call করলে mail provider ধীর হলে API response-ও ধীর হবে। Celery ব্যবহার করলে API task enqueue করে দ্রুত response দিতে পারে; worker পরে email পাঠায়।

### উদাহরণ project structure

```
config/
├── __init__.py
├── celery.py
├── settings.py
└── urls.py

accounts/
├── tasks.py
└── services/
    └── email_service.py
```

`config/celery.py`:

```
import osfrom celery import Celeryos.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")app = Celery("config")app.config_from_object("django.conf:settings", namespace="CELERY")app.autodiscover_tasks()
```

`config/__init__.py`:

```
from .celery import app as celery_app__all__ = ("celery_app",)
```

`config/settings.py`:

```
import osCELERY_BROKER_URL = os.environ["CELERY_BROKER_URL"]CELERY_TASK_IGNORE_RESULT = TrueCELERY_TASK_ACKS_LATE = TrueCELERY_WORKER_PREFETCH_MULTIPLIER = 1CELERY_BROKER_CONNECTION_RETRY_ON_STARTUP = True
```

`accounts/tasks.py`:

```
from celery import shared_taskfrom django.core.mail import send_mailfrom django.conf import settings@shared_task(    bind=True,    autoretry_for=(OSError,),    retry_backoff=True,    retry_kwargs={"max_retries": 5},)def send_authentication_email(self, subject, message, recipient):    send_mail(        subject=subject,        message=message,        from_email=settings.DEFAULT_FROM_EMAIL,        recipient_list=[recipient],        fail_silently=False,    )
```

এটি একটি illustrative task। তোমার আগের email service HTML email, token URL বা provider API ব্যবহার করলে সেই service-টিকেই task থেকে call করো। এখানে raw verification token বা password-reset token log করবে না।

### গুরুত্বপূর্ণ production বিষয়

- Retry সব ধরনের exception-এর জন্য অন্ধভাবে চালাবে না; transient error এবং permanent error আলাদা করো।
- `acks_late=True`-তে worker কাজ শেষ হওয়ার আগে মারা গেলে task আবার চালানো হতে পারে। তাই task idempotent হতে হবে।
- Duplicate email বা duplicate business action ঠেকাতে idempotency strategy রাখো।
- Queue depth, task failure, retry count এবং oldest queued task-এর বয়স monitor করো।
- Password-reset ও verification email-এর ক্ষেত্রে token expiry এবং single-use validation অবশ্যই database/service layer-এ enforce করো।
- Broker restart বা worker downtime-এর সময় email delivery বিলম্বিত হতে পারে; API যেন মিথ্যা করে “email delivered” না বলে।

### `transaction.on_commit()` কেন দরকার?

যদি user registration-এর database transaction commit হওয়ার আগেই Celery task enqueue করা হয়, worker user record তৈরি হওয়ার আগেই কাজ শুরু করতে পারে। তাই commit হওয়ার পর task enqueue করো:

```
from django.db import transactiontransaction.on_commit(    lambda: send_authentication_email.delay(        "Verify your email",        "Please open the verification link sent separately.",        user.email,    ))
```

এখানে উদাহরণটি শুধু task scheduling দেখায়। বাস্তব verification email-এ তোমার email service দিয়ে তৈরি নিরাপদ verification link যুক্ত করতে হবে। Lambda-তে এমন mutable variable ব্যবহার করবে না, যার value callback চলার আগে বদলে যেতে পারে।

`transaction.on_commit()` database commit এবং task enqueue-এর মাঝখানে process crash হলে task হারানোর সম্ভাবনা পুরোপুরি দূর করে না। অত্যন্ত গুরুত্বপূর্ণ workflow-তে transactional outbox pattern বিবেচনা করা যায়।

## 8. Docker Compose: services একত্র করা

নিচের configuration-টি architecture বোঝার ও staging environment তৈরির একটি ভিত্তি। এটি সরাসরি সম্পূর্ণ production-ready নয়: image build, persistent volumes, TLS certificates, database initialization, backup, Redis persistence, health checks, non-root users, secret delivery এবং network hardening তোমার deployment অনুযায়ী যোগ করতে হবে।

`compose.production.yaml`-এর সরল skeleton:

```
services:
  nginx:
    image: nginx:stable
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./deploy/nginx/conf.d:/etc/nginx/conf.d:ro
      - ./deploy/certbot/conf:/etc/letsencrypt:ro
    depends_on:
      - api
    networks:
      - edge
      - internal
    restart: unless-stopped

  api:
    build: .
    env_file:
      - .env.production
    expose:
      - "8000"
    environment:
      POSTGRES_HOST: db
      POSTGRES_PORT: "5432"
      REDIS_CACHE_URL: redis://redis:6379/1
      CELERY_BROKER_URL: redis://redis:6379/2
      GUNICORN_WORKERS: "3"
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    networks:
      - internal
    restart: unless-stopped

  celery_worker:
    build: .
    command: celery -A config worker --loglevel=INFO
    env_file:
      - .env.production
    environment:
      POSTGRES_HOST: db
      POSTGRES_PORT: "5432"
      CELERY_BROKER_URL: redis://redis:6379/2
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    networks:
      - internal
    restart: unless-stopped

  db:
    image: postgres:16
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U \"$${POSTGRES_USER}\" -d \"$${POSTGRES_DB}\""]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - internal
    restart: unless-stopped

  redis:
    image: redis:7
    command: ["redis-server", "--appendonly", "yes"]
    volumes:
      - redis_data:/data
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 3s
      retries: 5
    networks:
      - internal
    restart: unless-stopped

volumes:
  postgres_data:
  redis_data:

networks:
  edge:
  internal:
    internal: true
```

### এই skeleton-এ কী কী ঠিক করতে হবে?

1. Nginx-এর জন্য certificate renewal process এবং বাস্তব certificate files নিশ্চিত করতে হবে।
2. `.env.production`-এ sensitive values থাকলে file permission কঠোর রাখতে হবে; version control-এ commit করবে না।
3. `api` ও `celery_worker` একই application image ব্যবহার করতে পারে, তবে image-এ Celery dependencies থাকতে হবে।
4. PostgreSQL health check database ready হওয়া যাচাই করে, কিন্তু application-level schema বা migration readiness নিশ্চিত করে না।
5. Redis-এর জন্য `redis-cli ping` শুধু process availability দেখায়; persistence, memory pressure, queue health ও eviction policy আলাদাভাবে monitor করতে হবে।
6. Nginx public-facing; PostgreSQL, Redis এবং application port host-এ publish করা হয়নি।
7. Production-এ image tag immutable হওয়া উচিত—যেমন Git commit SHA বা release version; `latest`-এর ওপর নির্ভর করবে না।
8. একই host-এ সব service থাকলে host failure-এ সব service একসঙ্গে unavailable হতে পারে। প্রয়োজন অনুযায়ী managed database, managed Redis ও পৃথক application hosts ব্যবহার করো।

আরেকটি গুরুত্বপূর্ণ বিষয়: `depends_on` startup ordering ও health condition-এ সাহায্য করে, কিন্তু চলমান অবস্থায় dependency crash হলে automatic failover বা data recovery নিশ্চিত করে না।

## 9. Secrets management: password ও signing key কোথায় রাখবে?

Production secrets-এর মধ্যে থাকবে:

- `DJANGO_SECRET_KEY`
- `POSTGRES_PASSWORD`
- SMTP credentials বা email provider API key
- JWT signing key, যদি আলাদা key ব্যবহৃত হয়
- Sentry DSN ও অন্যান্য service credentials
- TLS private key

### Django production settings

```
import osDEBUG = FalseSECRET_KEY = os.environ["DJANGO_SECRET_KEY"]ALLOWED_HOSTS = [    host.strip()    for host in os.environ["DJANGO_ALLOWED_HOSTS"].split(",")    if host.strip()]SECURE_SSL_REDIRECT = TrueSESSION_COOKIE_SECURE = TrueCSRF_COOKIE_SECURE = TrueSECURE_PROXY_SSL_HEADER = ("HTTP_X_FORWARDED_PROTO", "https")SECURE_HSTS_SECONDS = 31536000SECURE_HSTS_INCLUDE_SUBDOMAINS = TrueSECURE_HSTS_PRELOAD = False
```

এগুলো `config/settings.py`-এর সংশ্লিষ্ট configuration-এর সঙ্গে merge করবে; existing settings অন্ধভাবে duplicate করবে না।

`SECURE_PROXY_SSL_HEADER` তখনই ব্যবহার করবে, যখন Nginx বা trusted proxy incoming forwarded protocol header-কে সঠিকভাবে overwrite করে। অন্যথায় client forged header দিয়ে ভুল security signal দিতে পারে।

HSTS চালুর আগে HTTPS সম্পূর্ণভাবে কাজ করছে নিশ্চিত করো। `includeSubDomains` এবং `preload` কেবল সব সংশ্লিষ্ট subdomain দীর্ঘমেয়াদে HTTPS-এ চালানোর প্রস্তুতি থাকলে বিবেচনা করবে।

### `.env.production` উদাহরণ

```
DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_ALLOWED_HOSTS=api.example.com

POSTGRES_DB=authdb
POSTGRES_USER=authapp
POSTGRES_PASSWORD=replace-with-a-strong-unique-password
POSTGRES_HOST=db
POSTGRES_PORT=5432

REDIS_CACHE_URL=redis://redis:6379/1
CELERY_BROKER_URL=redis://redis:6379/2
```

এটি শুধু configuration-এর উদাহরণ। বাস্তবে এখানে sample value-এর জায়গায় নিরাপদ secret দেবে।

### Secret management checklist

- `.env.production` Git-এ commit করবে না; `.gitignore`-এ রাখবে।
- Production-এ সম্ভব হলে cloud secret manager, deployment platform secret store বা Docker secrets ব্যবহার করবে।
- Container environment variable-ও process inspection বা debugging output-এর মাধ্যমে exposed হতে পারে; সেগুলোকে সম্পূর্ণ risk-free ভাববে না।
- Secret rotation-এর সময় পুরোনো ও নতুন key-এর compatibility এবং rollout plan তৈরি করবে।
- Database-এর জন্য application-এর সীমিত privilege-সহ আলাদা user ব্যবহার করবে; superuser নয়।
- JWT signing key পরিবর্তনের ফলে token invalidation হতে পারে—rotation পরিকল্পিতভাবে করবে।
- Logs, error reports এবং CI output-এ password, bearer token, verification token বা reset token থাকবে না।

## 10. Production capacity planning

Production architecture নির্বাচন করার আগে “কত user support করবে?” প্রশ্নটিকে measurable workload-এ পরিণত করতে হবে।

ধরা যাক, তোমার staging benchmark-এ 20 concurrent users দিয়ে login, refresh ও profile traffic পরীক্ষা করা হয়েছে। সেটি থেকে সরাসরি “production-এ 20,000 users চলবে” সিদ্ধান্ত নেওয়া যাবে না। প্রয়োজন হবে endpoint mix, request rate, latency distribution, CPU, RAM, database connections এবং error rate-এর বাস্তব measurement।

### গুরুত্বপূর্ণ performance metrics

| Metric         | কী বোঝায়                               | কেন গুরুত্বপূর্ণ        |
| -------------- | -------------------------------------- | ----------------------- |
| RPS            | প্রতি সেকেন্ডে request                 | System-এর load          |
| p50 latency    | মাঝের request-এর latency               | Typical experience      |
| p95 latency    | 95% request এর চেয়ে দ্রুত শেষ হওয়া সময় | Slow-request experience |
| p99 latency    | 99% request এর চেয়ে দ্রুত শেষ হওয়া সময় | Tail latency            |
| Error rate     | Failed request-এর অনুপাত               | Reliability             |
| CPU/RAM        | Application ও worker resource          | Saturation / OOM        |
| DB connections | Database connection demand             | Connection exhaustion   |
| Queue depth    | Pending Celery tasks                   | Background backlog      |

### একটি আনুমানিক capacity calculation

ধরা যাক:

- Peak load: 100 requests/second
- Benchmark-এ এক API instance স্থিতিশীলভাবে 40 RPS সামলেছে, নির্ধারিত latency ও error target বজায় রেখে
- Capacity headroom রাখতে সর্বোচ্চ measured capacity-এর 60% ব্যবহার করতে চাই

প্রতি instance-এর planning capacity:

\\[ 40 \times 0.60 = 24\ \text{RPS} \\]

প্রয়োজনীয় API instance-এর আনুমানিক সংখ্যা:

\\[ N = \left\lceil \frac{100}{24} \right\rceil = 5 \\]

এখানে 5টি instance একটি hypothetical planning estimate, বাস্তব benchmark নয়। প্রকৃত capacity request mix, worker settings, database, Redis, network এবং instance failure-এর ওপর নির্ভর করবে। একটি instance নষ্ট হলেও peak load সামলাতে চাইলে N+1 capacity-ও বিবেচনা করতে হবে।

### Database-কে ভুলে যেও না

যদি 5টি API instance-এর প্রতিটিতে 3টি Gunicorn worker থাকে, তাহলে worker সংখ্যা হবে 15। কিন্তু এর অর্থ এই নয় যে PostgreSQL-এ সর্বোচ্চ 15টি connection-ই লাগবে—Celery, management commands, monitoring এবং অন্যান্য service-ও connection নিতে পারে।

Database যদি bottleneck হয়, API instance বাড়ালে throughput না বেড়ে connection pressure ও query contention বাড়তে পারে। Capacity planning-এ তাই API, PostgreSQL, Redis এবং Celery-কে আলাদা component হিসেবে benchmark করতে হবে।

## 11. Failure scenarios: কিছু নষ্ট হলে system কী করবে?

Production architecture-এর আসল পরীক্ষা শুধু সবকিছু ঠিক থাকা অবস্থায় নয়—কোনো dependency fail করলেও system কীভাবে আচরণ করে, সেটি।

| Failure scenario                 | সম্ভাব্য প্রভাব                                 | প্রয়োজনীয় ব্যবস্থা                                      |
| -------------------------------- | ----------------------------------------------- | ------------------------------------------------------- |
| একটি Gunicorn worker crash       | কিছু request ব্যর্থ বা retry হতে পারে           | Worker restart, error monitoring                        |
| পুরো API container crash         | ঐ instance unavailable                          | Multiple instances, health checks, load balancer        |
| PostgreSQL unavailable           | Login, registration ও data operations ব্যর্থ    | Managed HA/replication, backup, recovery plan           |
| PostgreSQL connection exhaustion | Query অপেক্ষা করবে বা ব্যর্থ হবে                | PgBouncer, connection budget, slow-query analysis       |
| Redis unavailable                | Cache, throttling বা broker ক্ষতিগ্রস্ত         | Workload অনুযায়ী isolation, fallback policy, alerts     |
| Celery worker বন্ধ               | Email ও background jobs queue-তে জমবে           | Worker restart, queue monitoring, retry                 |
| Email provider failure           | Verification/reset email দেরি হবে               | Bounded retries, provider monitoring, safe user message |
| Nginx misconfiguration           | সব API traffic ব্যর্থ হতে পারে                  | Config test, staged rollout, rollback                   |
| Secret ভুল বা expired            | App startup বা external service call ব্যর্থ     | Secret validation, rotation runbook                     |
| Disk পূর্ণ                       | Database, logs বা containers সমস্যায় পড়তে পারে  | Disk alerts, log rotation, capacity monitoring          |
| নতুন DB migration incompatible   | নতুন ও পুরোনো app version একসঙ্গে চলতে পারবে না | Expand/contract migration, staged deployment            |
| Backup corrupt বা restore ব্যর্থ | Disaster recovery সম্ভব নাও হতে পারে            | Automated restore verification, recovery drill          |

### Health check-এর স্তর আলাদা করো

- Liveness: Process চলছে কি? না চললে restart দরকার হতে পারে।
- Readiness: Instance নতুন traffic নেওয়ার জন্য প্রস্তুত কি?
- Dependency monitoring: PostgreSQL, Redis, email provider এবং Celery queue ঠিক আছে কি?

সব dependency-এর health endpoint একটিতে জুড়ে দিলে database সাময়িক unavailable হলেই orchestration পুরো application বারবার restart করতে পারে। তাই liveness ও readiness-এর উদ্দেশ্য আলাদা রাখবে; dependency failure-এর জন্য monitoring/alerting এবং নির্ধারিত fallback ব্যবহার করবে।

### Authentication-specific failure rules

1. Database unavailable হলে login সফল বলে response দেবে না।
2. JWT signature, expiry ও `token_version` validation bypass করবে না।
3. Redis unavailable হলে throttling অজান্তে disable করবে না।
4. Password-reset email queue করা গেলেই email পৌঁছেছে—এমন দাবি করবে না।
5. Email retry করলে token-এর expiry ও single-use rule অক্ষুণ্ণ থাকতে হবে।
6. কোনো instance-এ login হলে অন্য instance-এও JWT validation কাজ করতে হবে; shared signing configuration ও database state নিশ্চিত করতে হবে।
7. Password reset বা password change-এর পর access-token revocation strategy—যেমন তোমার project-এর `token_version` validation—সব API instance-এ কার্যকর হতে হবে।

## 12. Deployment topology: কখন কোন architecture বেছে নেবে?

[Beget VPS для OpenClaw: какой тариф выбрать в 2026 году](https://images.openai.com/static-rsc-4/MuwpS5XdC72J6G1mX60SfMHlbYrHvuhJpp94YKOzEh3Q4MAWAIo2-JLm3dysurRg68qjKsLcqwQ2VMgivHvus4-kB7Gjt0E661mVKvf3bhV2MA9VwuDDoagfem4l77sei6a2sTPExlNGYh_QFBkb4zJHvr2hAP2G9ShyClNMwyk?purpose=inline)

Stage A — Learning / Small deployment

Single VPS

একটি VPS-এ Nginx, Django/Gunicorn, PostgreSQL, Redis ও Celery। শেখা, staging এবং কম traffic-এর application-এর জন্য সহজ ও কম খরচের architecture।

সীমাবদ্ধতা: VPS বা host নষ্ট হলে পুরো system unavailable হতে পারে।

[Autoscaling architecture - Architecting Cloud Computing Solutions \[Book\]](https://images.openai.com/static-rsc-4/wBl5mclMK2eg-QOKdXaztAIKxUBzNnq1sOX99EDc_apSt_sR7iShNWVT4fhZi72x2jE0xpxIQ1TskmqG4asq6x47aDM6G19dUS9ye65EQeA2z1hKFrJKIxOoIpukr8pfCnVoPZRFIrQ9cw7RcDPDyHBEwuKSlq0z23OBazaKoLQ?purpose=inline)

Stage B — Growing production

Separated services

Nginx বা load balancer-এর পেছনে একাধিক API instance; managed PostgreSQL ও Redis; আলাদা Celery worker। Database ও cache-এর resource এবং failure domain আলাদা করা সহজ হয়।

প্রয়োজন: shared configuration, centralized logs, secrets management, monitoring ও tested backups।

[Scaling and Stabilizing a Growing Web Application on AWS | by Yamini Mandadi | Medium](https://images.openai.com/static-rsc-4/WBavG5iwttF0k7rUXDLg_K4wHnPvlVTG7UmxKEM0GNZmzA3rPtgBAuj6GDWJbQpN3bm1uW1mS1-UgsJ3IEZEOfQvpIfGSfnWRL22HStqbOLyv6rBSN59GGAvperb-Pf-j8TUBJ8oTR9O9AGxB30YoMbn4SXBjZH7Id1bcbmUNZw?purpose=inline)

Stage C — High availability

Redundant infrastructure

একাধিক failure domain-এ API instances, redundant ingress/load balancing, managed database HA, Redis-এর উপযুক্ত HA configuration এবং আলাদা worker capacity।

প্রয়োজন: failover testing, backup restore drill, capacity headroom এবং documented recovery objectives। শুধু বেশি container চালালেই HA হয় না।

## 13. Production verification: হাতে-কলমে পরীক্ষা

প্রথমে staging-এ deploy করবে। এরপর নিচের checklist ধরে পরীক্ষা করবে।

## Production readiness checklist

0/10 complete

Network isolation

Internet থেকে PostgreSQL, Redis ও Gunicorn port সরাসরি accessible নয়।

HTTPS and Django security

Certificate valid; DEBUG=False; trusted proxy headers ও allowed hosts সঠিক।

Authentication

Registration, verification, login, refresh, logout এবং token revocation কাজ করে।

Redis and throttling

একাধিক API instance-এ throttling state shared; Redis failure policy পরীক্ষা করা হয়েছে।

Celery

Email enqueue, worker restart, retry ও duplicate task handling পরীক্ষা করা হয়েছে।

PostgreSQL capacity

Connection budget, slow queries, backups ও restore যাচাই করা হয়েছে।

Load testing

Locust দিয়ে baseline, p95/p99, error rate, CPU/RAM ও database pressure মাপা হয়েছে।

Deployment

Health checks, immutable image tag, migration compatibility ও rollback runbook প্রস্তুত।

Monitoring

API errors, latency, queue depth, database connections, disk space ও alerts চালু।

Secrets

Production credentials Git-এ নেই; access সীমিত এবং rotation procedure আছে।

&#x20; Checklist copy করো&#x20;

### Useful deployment commands

```
# Compose configuration validate
docker compose -f compose.production.yaml config

# Services ও health status
docker compose -f compose.production.yaml ps

# API logs
docker compose -f compose.production.yaml logs --tail=200 api

# Celery worker logs
docker compose -f compose.production.yaml logs --tail=200 celery_worker

# Django production deployment checks
docker compose -f compose.production.yaml exec api \
    python manage.py check --deploy

# Database migrations
docker compose -f compose.production.yaml exec api \
    python manage.py migrate --check
```

`migrate --check` pending migration আছে কি না পরীক্ষা করে; এটি migration apply করে না। Deployment-এ migration apply করার আগে backup, compatibility এবং rollout order যাচাই করবে।

## 14. Final architecture decision

তোমার `complete_auth_project`-এর জন্য আমার সুপারিশ:

- Application: Django REST Framework + Gunicorn, environment-based configuration।
- Edge: Nginx + HTTPS; প্রয়োজন অনুযায়ী edge rate limiting।
- Database: PostgreSQL; connection pressure প্রমাণিত হলে PgBouncer।
- Cache/throttling: Shared Redis; production scale ও reliability অনুযায়ী cache এবং Celery broker আলাদা করা।
- Background jobs: Celery worker, bounded retries, idempotency এবং queue monitoring।
- Authentication security: JWT validation, refresh-token rotation/blacklisting, `token_version`-ভিত্তিক revocation এবং password-reset token-এর single-use/expiry checks।
- Deployment: Immutable Docker images, automated tests, health checks, compatible migrations ও rollback plan।
- Operations: Structured logs, error tracking, latency metrics, database backups, restore drills এবং alerting।

সবচেয়ে গুরুত্বপূর্ণ architectural principle হলো: API server-কে যত ইচ্ছা বাড়ানো যায়—এমনভাবে design করার আগে database, Redis ও background worker-এর capacity এবং failure behavior নিশ্চিত করতে হবে। API instance বাড়িয়ে bottleneck দূর করার চেষ্টা করলে অনেক সময় bottleneck শুধু PostgreSQL বা Redis-এ স্থানান্তরিত হয়।

পরবর্তী যৌক্তিক ধাপ হতে পারে Lesson 19: Production Implementation Lab—এই architecture-কে তোমার বর্তমান repository-তে বাস্তবে প্রয়োগ করা, Compose services যাচাই করা, health endpoints, secrets validation, PostgreSQL pooling এবং staging load test একসঙ্গে সম্পন্ন করা।


--------

# Lesson 19: Production Implementation Lab

Project: `complete_auth_project` — Django REST Framework Authentication API

এই Lesson-এ শুধু architecture আলোচনা করব না; বরং তোমার repository-তে ধাপে ধাপে implementation, configuration validation, health checks, secret validation, PostgreSQL connection management এবং staging load test সম্পন্ন করার মতো code তৈরি করব।

আগের Lesson 18-এ আমরা Nginx, Gunicorn, Django, PostgreSQL, Redis, Celery, PgBouncer ও deployment topology পর্যালোচনা করেছি। এবার সেগুলোকে একটি কার্যকর implementation workflow-তে নিয়ে যাব।

## আজকের Lab roadmap

Lab 1 — Repository audit

বর্তমান project structure, dependencies, Compose configuration এবং settings যাচাই।

Lab 2 — Health endpoints

Liveness, readiness, database connectivity এবং container health checks।

Lab 3 — Secrets validation

Production secrets, DEBUG, allowed hosts এবং insecure defaults প্রতিরোধ।

Lab 4 — PostgreSQL connection management

Django persistent connections, connection budget এবং ঐচ্ছিক PgBouncer।

Lab 5 — Compose validation ও staging load test

Service health, dependency failure এবং Locust দিয়ে performance baseline।

একটি গুরুত্বপূর্ণ সীমাবদ্ধতা: এই কথোপকথনে তোমার repository-র actual files সরাসরি দৃশ্যমান নয়। তাই নিচের code তোমার পরিচিত `config.settings`, `config.urls`, `accounts` structure ধরে লেখা। যেখানে existing implementation-এর সঙ্গে merge করতে হবে, তা উল্লেখ করছি—পুরো `settings.py` বা Compose file অন্ধভাবে replace করবে না।

## Lab 1 — Repository audit

প্রথমে project root-এ যাও:

```
cd complete_auth_project

pwd
find . -maxdepth 3 -type f \
  -not -path './.git/*' \
  -not -path './.venv/*' \
  | sort
```

Virtual environment সক্রিয় করে dependencies যাচাই করো:

```
python -m pip show Django djangorestframework \
  djangorestframework-simplejwt psycopg locust celery
```

যে package install করা নেই, তার জন্য output না পাওয়া স্বাভাবিক। Project-এর বিদ্যমান `requirements.txt` বা `pyproject.toml`-ই dependency-এর source of truth হিসেবে রাখবে।

বর্তমান Git changes পরীক্ষা করো:

```
git status --short
```

এরপর নিচের files আছে কি না দেখো:

```
config/settings.py
config/urls.py
config/wsgi.py
accounts/models.py
requirements.txt
Dockerfile
compose.yaml
```

তোমার project-এ `docker-compose.yml` বা অন্য নাম থাকলেও সমস্যা নেই। পরবর্তী command-এ সঠিক filename ব্যবহার করবে।

## Lab 2 — Django health endpoints

Production monitoring-এর জন্য দুটি endpoint তৈরি করব:

- `/health/live/` — Django process response দিতে পারছে কি না।
- `/health/ready/` — Django নতুন request নেওয়ার জন্য প্রস্তুত কি না; এই উদাহরণে database connection-ও পরীক্ষা হবে।

Readiness endpoint-এ dependency check থাকলেও liveness endpoint-এ থাকবে না। Database সাময়িকভাবে unavailable হলে প্রতিটি Django process restart করাতে চাই না।

### Step 2.1 — Health views তৈরি করো

`config/health.py` নামে file তৈরি করো:

```
from django.db import DatabaseError, connectionfrom django.http import JsonResponsefrom django.views.decorators.http import require_GET@require_GETdef live(request):    return JsonResponse({"status": "ok"})@require_GETdef ready(request):    try:        with connection.cursor() as cursor:            cursor.execute("SELECT 1")            cursor.fetchone()    except DatabaseError:        # Internal database details response-এ প্রকাশ করবে না।        return JsonResponse(            {"status": "unavailable"},            status=503,        )    return JsonResponse({"status": "ready"})
```

কেন `SELECT 1`? এটি ছোট query, যা যাচাই করে Django database connection দিয়ে query execute করতে পারছে। এটি database-এর সব table, migration, write permission, Redis বা Celery-র health প্রমাণ করে না।

### Step 2.2 — URLs যুক্ত করো

তোমার existing `config/urls.py`-এ এই routes যুক্ত করো:

```
from django.contrib import adminfrom django.urls import pathfrom config.health import live, readyurlpatterns = [    path("admin/", admin.site.urls),    path("health/live/", live, name="health-live"),    path("health/ready/", ready, name="health-ready"),    # তোমার existing API routes অক্ষুণ্ণ রাখবে।]
```

এখানে দেখানো `urlpatterns` একটি উদাহরণ। Existing authentication routes যেমন `/api/auth/`-এর include statements মুছে ফেলবে না।

### Step 2.3 — Local test

```
python manage.py runserver
```

অন্য terminal থেকে:

```
curl -i http://127.0.0.1:8000/health/live/
curl -i http://127.0.0.1:8000/health/ready/
```

স্বাভাবিক অবস্থায় প্রত্যাশিত ফল:

```
{"status": "ok"}
```

এবং

```
{"status": "ready"}
```

Database connection ব্যর্থ হলে readiness endpoint `503 Service Unavailable` দেবে। Production monitoring-এ status code এবং response time দেখবে; raw database exception বা credential log করবে না।

### Step 2.4 — Health endpoint tests

`accounts/tests/test_health.py` তৈরি করো:

```
from unittest.mock import patchfrom django.test import TestCasefrom django.db import DatabaseErrorclass HealthEndpointTests(TestCase):    def test_liveness_returns_ok(self):        response = self.client.get("/health/live/")        self.assertEqual(response.status_code, 200)        self.assertEqual(response.json()["status"], "ok")    def test_readiness_returns_ready(self):        response = self.client.get("/health/ready/")        self.assertEqual(response.status_code, 200)        self.assertEqual(response.json()["status"], "ready")    @patch("config.health.connection.cursor")    def test_readiness_returns_503_when_database_fails(self, mock_cursor):        mock_cursor.side_effect = DatabaseError("database unavailable")        response = self.client.get("/health/ready/")        self.assertEqual(response.status_code, 503)        self.assertEqual(            response.json()["status"],            "unavailable",        )
```

পরীক্ষাগুলো চালাও:

```
python manage.py test accounts.tests.test_health
```

এখানে `config.health.connection.cursor` mock করা হয়েছে, যাতে failure test-এ সত্যিকারের database বন্ধ করার প্রয়োজন না হয়।

## Lab 3 — Production secrets validation

Django-তে environment variable থেকে secret পড়া গুরুত্বপূর্ণ, কিন্তু শুধু environment variable ব্যবহার করলেই application secure হয়ে যায় না। Production-এ secret অনুপস্থিত বা unsafe default থাকলে deployment ব্যর্থ হওয়াই ভালো।

### Step 3.1 — Settings-এ configuration যাচাই

`config/settings.py`-এ বিদ্যমান `SECRET_KEY`, `DEBUG` এবং `ALLOWED_HOSTS` configuration-কে নিচের pattern অনুযায়ী সাজাও:

```
import osfrom django.core.exceptions import ImproperlyConfiguredDEBUG = os.environ.get("DJANGO_DEBUG", "false").lower() == "true"SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY", "")ALLOWED_HOSTS = [    host.strip()    for host in os.environ.get("DJANGO_ALLOWED_HOSTS", "").split(",")    if host.strip()]if not DEBUG:    if len(SECRET_KEY) < 50:        raise ImproperlyConfigured(            "Production requires a strong DJANGO_SECRET_KEY."        )    if not ALLOWED_HOSTS:        raise ImproperlyConfigured(            "Production requires DJANGO_ALLOWED_HOSTS."        )
```

এটি production configuration-এর একটি ন্যূনতম guardrail। ৫০ character-এর দৈর্ঘ্য একাই secret-এর randomness বা security নিশ্চিত করে না। Secret cryptographically secure random generator দিয়ে তৈরি করবে এবং production credential কখনও source code-এ রাখবে না।

যদি তোমার settings-এ আগে থেকেই `SECRET_KEY = ...`, `DEBUG = ...` বা `ALLOWED_HOSTS = ...` থাকে, সেগুলো duplicate না করে existing configuration-কে এই logic-এর সঙ্গে merge করবে।

### Step 3.2 — Production environment file

উদাহরণ `.env.production`:

```
DJANGO_DEBUG=false
DJANGO_SECRET_KEY=replace-with-a-strong-random-secret
DJANGO_ALLOWED_HOSTS=api.example.com

POSTGRES_DB=authdb
POSTGRES_USER=authapp
POSTGRES_PASSWORD=replace-with-a-unique-password
POSTGRES_HOST=db
POSTGRES_PORT=5432
```

এগুলো placeholder। বাস্তব secret তৈরি করে বসাতে হবে। File-টি Git-এ commit করবে না:

```
.env
.env.*
!.env.example
```

যদি তোমার repository-তে অন্য environment naming convention থাকে, সেটি বজায় রেখে production secret file ignore করো। আগে থেকেই tracked secret থাকলে `.gitignore` যোগ করাই যথেষ্ট নয়—secret rotate করতে হবে এবং Git history-ও বিবেচনা করতে হবে।

### Step 3.3 — Django deployment checks

```
python manage.py check --deploy
```

এই command deployment security configuration-এর বিভিন্ন সমস্যা শনাক্ত করতে সাহায্য করে। তবে এটি secret manager, database permissions, TLS certificate, Redis security বা server firewall-এর সম্পূর্ণ audit নয়।

Production configuration ভুল হলে application শুরু হওয়ার সময় fail হওয়া উচিত; অথচ secret-এর value exception message বা logs-এ প্রকাশ করা যাবে না।

## Lab 4 — PostgreSQL connection management

এখন database connection-এর configuration-কে production workload-এর উপযোগী করব।

### Step 4.1 — Django database settings

`config/settings.py`-এ PostgreSQL configuration:

```
import osDATABASES = {    "default": {        "ENGINE": "django.db.backends.postgresql",        "NAME": os.environ["POSTGRES_DB"],        "USER": os.environ["POSTGRES_USER"],        "PASSWORD": os.environ["POSTGRES_PASSWORD"],        "HOST": os.environ.get("POSTGRES_HOST", "db"),        "PORT": os.environ.get("POSTGRES_PORT", "5432"),        "CONN_MAX_AGE": int(            os.environ.get("DB_CONN_MAX_AGE", "60")        ),        "CONN_HEALTH_CHECKS": True,    }}
```

যদি তোমার বর্তমান project `DATABASE_URL` ব্যবহার করে, তাহলে এই block দিয়ে আগের database configuration replace করবে না। `DATABASE_URL` parsing-এর existing implementation বজায় রেখে connection options যোগ করবে।

`CONN_MAX_AGE=60` মানে persistent connection ব্যবহারের ক্ষেত্রে Django connection-কে সর্বোচ্চ প্রায় ৬০ সেকেন্ড পর্যন্ত reuse করার সুযোগ পাবে। এটি সব connection ঠিক ৬০ সেকেন্ড পর বন্ধ হবে—এমন নিশ্চয়তা নয়।

### Step 4.2 — PostgreSQL connection budget

ধরা যাক, staging-এ:

- API instance: 2
- প্রতি API instance-এ Gunicorn worker: 3
- Celery worker process: 2
- Operations ও monitoring-এর জন্য reserve: 5 connections

একটি প্রাথমিক estimate:

\\[ C = (2 \times 3) + 2 + 5 = 13 \\]

এটি planning estimate, measured maximum নয়। বাস্তব connection demand নির্ভর করে process model, threads, connection reuse, background tasks এবং pooling-এর ওপর।

PostgreSQL-এ বর্তমান অবস্থা দেখো:

```
SELECT
    state,
    COUNT(*) AS connection_count
FROM pg_stat_activity
WHERE datname = current_database()
GROUP BY state
ORDER BY connection_count DESC;
```

বর্তমান connection count ও configured maximum:

```
SELECT
    COUNT(*) AS current_connections,
    current_setting('max_connections')::int AS max_connections
FROM pg_stat_activity;
```

এই query-গুলো database monitoring-এর প্রাথমিক উপায়। Connection সংখ্যা বেশি হলেই সবসময় সমস্যা হচ্ছে এমন নয়; connection saturation, wait time, slow queries এবং resource pressure-ও দেখতে হবে।

### Step 4.3 — কখন PgBouncer লাগবে?

প্রথমে Django connection management

কম instance ও কম traffic থাকলে সরল PostgreSQL connection setup দিয়ে benchmark শুরু করো।

Connection pressure প্রমাণিত হলে pooling

Connection count বা connection establishment cost সমস্যা হলে PgBouncer বিবেচনা করো।

Transaction pooling-এর compatibility

Session state, server-side cursors ও prepared statements-এর ব্যবহার পরীক্ষা না করে transaction pooling চালু করবে না।

PgBouncer যোগ করলে Django-এর database host ও port PgBouncer-এর internal address-এ পরিবর্তন করতে হবে। একই সঙ্গে PgBouncer-এর client pool limit, backend pool size এবং PostgreSQL connection budget মিলিয়ে configure করতে হবে।

## Lab 5 — Compose services validate করা

তোমার বর্তমান Compose file-এ `api`, `db`, `redis`, `celery_worker` এবং `nginx` services থাকলে নিচের checks ব্যবহার করো।

### Step 5.1 — Configuration ও health

```
# Compose file syntax ও resolved configuration
docker compose config

# Container status
docker compose ps

# API logs
docker compose logs --tail=200 api

# Database logs
docker compose logs --tail=100 db

# Redis connectivity
docker compose exec redis redis-cli ping

# Celery worker logs
docker compose logs --tail=100 celery_worker
```

Redis স্বাভাবিকভাবে `PONG` দেবে। Compose service name ভিন্ন হলে সংশ্লিষ্ট service name ব্যবহার করবে।

### Step 5.2 — Container health check

তোমার Django image-এ Python আছে বলে API health check-এর একটি উপায় হলো Python-এর standard library ব্যবহার করা। `api` service-এর মধ্যে এই block যোগ করা যায়:

```
healthcheck:
  test:
    - CMD
    - python
    - -c
    - "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/live/', timeout=3)"
  interval: 15s
  timeout: 5s
  retries: 3
  start_period: 20s
```

এটি `services.api`-এর অধীনে বসবে; সম্পূর্ণ Compose file-এর root-এ নয়।

এই check liveness endpoint পরীক্ষা করে। Readiness endpoint-এর database check আলাদাভাবে monitoring করতে পারো। Liveness এবং readiness-কে এক করে ফেললে database outage-এর সময় অপ্রয়োজনীয় restart loop হতে পারে।

### Step 5.3 — Migration ও API test

```
docker compose exec api python manage.py check
docker compose exec api python manage.py check --deploy
docker compose exec api python manage.py migrate --check
docker compose exec api python manage.py test accounts.tests
```

শেষ command-এ তোমার existing test suite-এর নাম অনুযায়ী পরিবর্তন লাগতে পারে। Production database-এর পরিবর্তে staging বা test database-এ migration ও integration tests চালাবে।

## Lab 6 — Staging load test

এখন আগের Lesson 17-এর Locust setup ব্যবহার করে বাস্তবসম্মত performance baseline তৈরি করব।

Production-এ সরাসরি load test চালাবে না। Staging-এ আলাদা test accounts, test email configuration এবং পর্যাপ্ত database capacity ব্যবহার করো।

### Step 6.1 — Load test-এর আগে

1. অন্তত 20টি dedicated staging account তৈরি করো।
2. প্রতিটি virtual user-এর জন্য সঠিক login credentials নিশ্চিত করো।
3. `locustfile.py`-তে login, token refresh এবং profile endpoints সঠিক আছে কি না যাচাই করো।
4. Login throttle limit-এর কারণে 429 আসছে কি না পর্যবেক্ষণ করো।
5. Test চলাকালে API CPU/RAM, PostgreSQL connections, Redis latency ও Celery queue depth monitor করো।

### Step 6.2 — Locust চালাও

```
python -m pip install locust

export LOADTEST_PASSWORD='your-staging-only-password'
export LOADTEST_EMAIL_PREFIX='loadtest'
export LOADTEST_EMAIL_DOMAIN='example.test'

mkdir -p loadtests/results

locust -f loadtests/locustfile.py \
  --host https://staging-api.example.test \
  --headless \
  --users 20 \
  --spawn-rate 2 \
  --run-time 3m \
  --csv loadtests/results/auth-baseline \
  --csv-full-history
```

`https://staging-api.example.test`-এর জায়গায় তোমার staging API URL দেবে। Password-টি শুধু dedicated test accounts-এর জন্য ব্যবহার করবে; production account বা production secret নয়।

Locust-এর CSV output-এ সাধারণত request statistics এবং history পাওয়া যায়। Installed Locust version অনুযায়ী generated filenames ও columns যাচাই করবে।

### Step 6.3 — ফলাফল কীভাবে বিচার করবে?

| Measurement       | কী দেখবে                                      |
| ----------------- | --------------------------------------------- |
| p95 / p99 latency | Tail latency বাড়ছে কি না                      |
| Failure rate      | 401/429/5xx ও connection errors               |
| RPS               | Load বাড়ালে throughput বাড়ছে কি না            |
| CPU/RAM           | Gunicorn worker saturation বা memory pressure |
| PostgreSQL        | Connection exhaustion ও slow queries          |
| Redis             | Latency, availability ও throttling behavior   |
| Celery            | Queue backlog ও task failures                 |

প্রথমে 5 users, তারপর 10, 20 এবং প্রয়োজনে 40 users পর্যন্ত ধাপে ধাপে বাড়াও। কোনো ধাপে error rate বা latency দ্রুত বাড়লে test থামিয়ে bottleneck খুঁজে বের করো।

মনে রাখবে: 20 concurrent users মানেই 20 RPS নয়। RPS নির্ভর করে task frequency, response time, wait time এবং request mix-এর ওপর।

## Lab 7 — Failure testing ও release gate

Production-ready হওয়ার আগে শুধু happy path নয়, failure path-ও পরীক্ষা করতে হবে।

## Failure drill tracker

প্রতিটি পরীক্ষা disposable staging environment-এ করো; production database বা production Redis বন্ধ করে পরীক্ষা করবে না।

Database readiness failure

Test environment-এ database connection ব্যর্থ করিয়ে readiness endpoint 503 দেয় কি না যাচাই করো।

Redis outage

Staging Redis বন্ধ করে throttling ও Celery enqueue-এর নির্ধারিত failure policy যাচাই করো।

Celery worker stopped

Worker বন্ধ থাকলে queue backlog বাড়ে কি না এবং worker চালু হলে task processing আবার শুরু হয় কি না দেখো।

Invalid production secret

Dedicated test environment-এ required secret বাদ দিয়ে application startup fail করে কি না যাচাই করো।

Migration compatibility

পুরোনো ও নতুন app version একসঙ্গে চলার সময় migration backward-compatible কি না পরীক্ষা করো।

Load regression

একই staging workload-এ baseline ও নতুন release-এর p95 latency এবং failure rate তুলনা করো।

0 / 6 drills completed

### CI/CD-তে কীভাবে যুক্ত করবে?

তোমার existing GitHub Actions workflow-তে প্রথমে এই checks রাখো:

```
python manage.py check
python manage.py makemigrations --check --dry-run
python manage.py migrate --check
python manage.py test accounts.tests
```

এগুলোর সঙ্গে staging performance workflow-তে Locust run ও CSV threshold checker যুক্ত করবে। Performance regression gate-এর জন্য উদাহরণ হিসেবে p95 latency 300 ms এবং failure rate 1%-এর নিচে রাখার লক্ষ্য নির্ধারণ করা যায়—কিন্তু এগুলো universal standard নয়। তোমার baseline, SLA এবং business requirements অনুযায়ী target নির্ধারণ করবে।

আরও দুটি নিয়ম:

- Performance test threshold অতিক্রম করলে workflow fail করবে এবং CSV artifact সংরক্ষণ করবে।
- CI-তে deployment secret, test password ও token log করবে না; staging credentials-কে সীমিত privilege-এ রাখবে।

## Lesson 19 — Final completion checklist

## Release readiness

### 0/9

Health endpoints ও automated tests সফল

Production settings-এ unsafe defaults বন্ধ

Secrets Git-এর বাইরে এবং startup validation কার্যকর

Compose configuration valid; services ও health checks যাচাই করা

PostgreSQL connection budget হিসাব করা

PgBouncer দরকার কি না benchmark দিয়ে সিদ্ধান্ত নেওয়া

Redis ও Celery failure behavior পরীক্ষা করা

Staging Locust baseline ও performance regression gate তৈরি

Database backup restore এবং deployment rollback যাচাই

&#x20;Release checklist copy করো

## এরপর কী?

এই Lesson-এর code ও commands তোমার repository-তে প্রয়োগ করে test result সংগ্রহ করাই সবচেয়ে ভালো পরবর্তী পদক্ষেপ। Actual `settings.py`, Compose file এবং Dockerfile না দেখে পুরো production configuration একবারে replace করা নিরাপদ নয়।

পরবর্তী Lesson 20-এর জন্য সবচেয়ে যৌক্তিক বিষয় হবে Production Deployment Rehearsal—staging থেকে release candidate তৈরি, automated migration check, smoke tests, rollback drill, backup restore verification এবং deployment-এর পর authentication flow end-to-end পরীক্ষা।

-------
# Lesson 20: Production Deployment Rehearsal

Project: `complete_auth_project` — Django REST Framework Authentication API

এই Lesson-এ আমরা production-এ deploy করার আগে একটি পূর্ণ rehearsal চালাব। অর্থাৎ staging environment-এ production-এর মতো release তৈরি করব, database migration যাচাই করব, smoke tests চালাব, rollback drill করব, backup restore পরীক্ষা করব এবং deployment-এর পর সম্পূর্ণ authentication flow যাচাই করব।

মূল নীতি: শুধু deployment সফল হলেই release সফল নয়। নতুন version-এ login, token refresh, logout, password reset এবং database compatibility ঠিক আছে—সেটিও প্রমাণ করতে হবে।

## 1. Deployment rehearsal architecture

Git commit / release candidate

Code review · tests · dependency checks

CI validation

Tests · migration checks · Docker image build

Staging deployment

Migration · health checks · smoke tests

সব পরীক্ষা পাস

Release approval

কোনো পরীক্ষা ব্যর্থ

Stop · diagnose · rollback

Production release

Post-deployment verification · monitoring

এই rehearsal-এ আমরা ধরে নিচ্ছি, তোমার project-এ Docker, Django/DRF, PostgreSQL, Redis এবং authentication tests আছে। তোমার repository-র প্রকৃত deployment file-গুলো এখানে দৃশ্যমান না থাকায় commands-গুলো পরিচিত project structure ধরে লেখা হয়েছে; existing scripts ও Compose file-এর নাম অনুযায়ী প্রয়োজনমতো সামঞ্জস্য করবে।

## 2. Release candidate তৈরি

প্রথমে working tree পরিষ্কার কি না দেখো:

```
git status
git branch --show-current
git log -1 --oneline
```

Code review ও tests শেষ হলে release candidate-এর জন্য নির্দিষ্ট commit নির্বাচন করো। উদাহরণ:

```
git switch main
git pull --ff-only origin main

git tag -a v1.0.0-rc.1 -m "Authentication API release candidate 1"
git show --stat v1.0.0-rc.1
```

এটি local tag তৈরি করে। Remote-এ পাঠাতে চাইলে:

```
git push origin v1.0.0-rc.1
```

Tag push করার আগে নিশ্চিত হবে যে সঠিক commit-এ আছ। একই release tag-কে পরে অন্য commit-এ সরিয়ে দেওয়া উচিত নয়; release identity স্থায়ী রাখবে।

### Release metadata

প্রতিটি release-এর জন্য অন্তত এগুলো record করবে:

| Field              | উদাহরণ                                   |
| ------------------ | ---------------------------------------- |
| Release            | `v1.0.0-rc.1`                            |
| Git commit         | নির্দিষ্ট commit SHA                     |
| Docker image       | `ghcr.io/your-org/auth-api:<commit-sha>` |
| Database migration | নতুন migration-গুলোর নাম                 |
| Test status        | CI run link / result                     |
| Backup             | staging backup ID                        |
| Rollback image     | আগের stable image tag                    |

Production image-এর জন্য `latest`-এর বদলে immutable commit SHA বা version tag ব্যবহার করবে।

## 3. Automated pre-deployment validation

এবার release candidate-এর code ও database migration যাচাই করব।

### Step 3.1 — Local CI checks

Project root-এ চালাও:

```
python manage.py check
python manage.py makemigrations --check --dry-run
python manage.py test accounts.tests
```

যদি pytest ব্যবহার করো:

```
pytest --cov=accounts --cov-report=term-missing
```

`makemigrations --check --dry-run` নিশ্চিত করে যে model changes থেকে নতুন migration প্রয়োজন কি না। এটি migration production database-এ নিরাপদে apply হবে—এমন নিশ্চয়তা দেয় না।

### Step 3.2 — Docker image তৈরি

```
docker build \
  -t auth-api:rc1 \
  .
```

Image তৈরি হওয়ার পর তার metadata পরীক্ষা করো:

```
docker image inspect auth-api:rc1
```

CI/CD-তে image তৈরি হলে একই image-কে staging এবং পরে production-এ promote করবে। Production-এ নতুন করে আলাদা image build করলে staging-এ পরীক্ষিত artifact-এর সঙ্গে deployed artifact-এর পার্থক্য তৈরি হতে পারে।

### Step 3.3 — Compose configuration validate

যদি production Compose file `compose.production.yaml` হয়:

```
docker compose \
  -f compose.production.yaml \
  config --quiet
```

Environment variables অনুপস্থিত থাকলে বা configuration invalid হলে এই পর্যায়েই deployment থামানো উচিত। Resolved Compose configuration-এ secret থাকতে পারে, তাই সেটি public CI log-এ print করবে না।

## 4. Database migration rehearsal

এটি পুরো deployment-এর সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

### Migration কেন deployment ভাঙতে পারে?

ধরা যাক, নতুন release-এ `User` model-এর একটি field rename করলে:

- নতুন code নতুন field name আশা করতে পারে।
- পুরোনো code এখনও পুরোনো field name ব্যবহার করতে পারে।
- পুরোনো ও নতুন application instance একই সময়ে চললে request ব্যর্থ হতে পারে।
- Database migration rollback করলেও ইতোমধ্যে পরিবর্তিত বা হারানো data স্বয়ংক্রিয়ভাবে ফিরে আসে না।

### Step 4.1 — Pending migrations দেখো

Staging environment-এ:

```
docker compose \
  -f compose.staging.yaml \
  exec api python manage.py showmigrations
```

তারপর:

```
docker compose \
  -f compose.staging.yaml \
  exec api python manage.py migrate --check
```

দ্বিতীয় command pending migration থাকলে non-zero exit status দিতে পারে। এটি migration status যাচাই করে, migration execute করে না।

### Step 4.2 — Migration SQL review

নির্দিষ্ট app-এর migration SQL দেখতে:

```
python manage.py sqlmigrate accounts 0005
```

`0005`-এর জায়গায় প্রকৃত migration name ব্যবহার করবে।

বিশেষভাবে খেয়াল করবে:

- বড় table-এ table rewrite বা দীর্ঘ lock লাগতে পারে কি না।
- Unique constraint যোগ করার আগে duplicate data আছে কি না।
- Nullable field থেকে non-nullable field-এ পরিবর্তনের সময় existing rows কীভাবে পূরণ হবে।
- Migration-এর মধ্যে data transformation আছে কি না।
- Migration application traffic চলাকালে দীর্ঘ সময় database lock করে রাখবে কি না।

### Step 4.3 — Expand/contract migration strategy

Phase A — Expand

নতুন column বা schema যোগ করো, কিন্তু পুরোনো code যেন এখনও কাজ করতে পারে তা নিশ্চিত করো।

Phase B — Migrate data and code

প্রয়োজনে পুরোনো ও নতুন field কিছু সময় একসঙ্গে রাখো। Data backfill ও compatibility পরীক্ষা করো।

Phase C — Contract

পুরোনো code আর ব্যবহার হচ্ছে না এবং rollback compatibility আর প্রয়োজন নেই—এটি নিশ্চিত হওয়ার পর পুরোনো field বা constraint সরাও।

Production rule: নতুন application image-এ rollback করা গেলেও database migration rollback করা নিরাপদ হবে—এমন ধরে নেবে না। অনেক ক্ষেত্রে পুরোনো application image-এ ফিরে যাওয়া নিরাপদ, কিন্তু database schema নতুন অবস্থায় রেখে দেওয়া প্রয়োজন। এজন্য schema backward-compatible রাখা অত্যন্ত গুরুত্বপূর্ণ।

## 5. Backup তৈরি ও restore verification

Backup file তৈরি হওয়া আর সেটি থেকে database restore করা সম্ভব হওয়া এক জিনিস নয়। এই lab-এ staging database-এর backup তৈরি করে একটি আলাদা disposable restore database-এ restore পরীক্ষা করব।

### Step 5.1 — PostgreSQL backup

যদি PostgreSQL service-এর নাম `db` হয়:

```
mkdir -p backups

docker compose \
  -f compose.staging.yaml \
  exec -T db \
  sh -c 'pg_dump -U "$POSTGRES_USER" -d "$POSTGRES_DB" -Fc' \
  > backups/auth-staging.dump
```

File পরীক্ষা করো:

```
test -s backups/auth-staging.dump
```

Backup file-এর সঙ্গে timestamp, Git release SHA, database version এবং backup status record রাখবে। Backup-এ user emails ও authentication-related data থাকতে পারে, তাই এটিকে sensitive data হিসেবে সুরক্ষিত রাখবে।

### Step 5.2 — Backup archive যাচাই

```
docker compose \
  -f compose.staging.yaml \
  exec -T db \
  pg_restore --list \
  < backups/auth-staging.dump
```

এটি archive-এর metadata ও object list পড়তে পারছে কি না পরীক্ষা করে। কিন্তু এটি একাই সম্পূর্ণ restore সফল হওয়ার প্রমাণ নয়।

### Step 5.3 — আলাদা restore database

একই PostgreSQL server-এ disposable database তৈরি করার উদাহরণ:

```
docker compose \
  -f compose.staging.yaml \
  exec db \
  sh -c 'createdb -U "$POSTGRES_USER" auth_restore_test'
```

তারপর restore করো:

```
docker compose \
  -f compose.staging.yaml \
  exec -T db \
  sh -c 'pg_restore -U "$POSTGRES_USER" \
    -d auth_restore_test \
    --no-owner --no-privileges' \
  < backups/auth-staging.dump
```

এখানে `auth_restore_test` অবশ্যই disposable database হতে হবে; কোনোভাবেই production database-এর নাম ব্যবহার করবে না। Restore-এর সময় extension, ownership বা role-related সমস্যা দেখা দিতে পারে; সেগুলো restore runbook-এ document করবে।

Restore সম্পন্ন হলে database-এ ঢুকে schema যাচাই করো:

```
docker compose \
  -f compose.staging.yaml \
  exec db \
  psql -U "$POSTGRES_USER" -d auth_restore_test
```

তারপর SQL prompt-এ:

```
SELECT COUNT(*) FROM django_migrations;
SELECT COUNT(*) FROM accounts_user;
```

`accounts_user` তোমার প্রকৃত custom user table-এর নাম অনুযায়ী বদলাবে। শুধু row count মিললেই backup সম্পূর্ণ ঠিক প্রমাণিত হয় না; গুরুত্বপূর্ণ tables, constraints, relationships এবং application-level reads-ও যাচাই করতে হবে।

### Step 5.4 — Recovery objectives

দুটি লক্ষ্য আগে থেকেই নির্ধারণ করবে:

- RPO (Recovery Point Objective): সর্বোচ্চ কতটা সাম্প্রতিক data হারানো গ্রহণযোগ্য?
- RTO (Recovery Time Objective): system পুনরুদ্ধারে সর্বোচ্চ কত সময় লাগতে পারে?

Backup frequency, transaction-log/WAL retention, storage location এবং restore procedure এই লক্ষ্য পূরণ করছে কি না নিয়মিত পরীক্ষা করবে।

সতর্কতা: এই উদাহরণে backup local directory-তে লেখা হচ্ছে। এটি production disaster recovery-এর জন্য যথেষ্ট নয়। Encrypted off-host/object-storage backup, access restrictions, retention policy এবং নিয়মিত restore drill দরকার।

## 6. Smoke tests: deployment-এর পর দ্রুত যাচাই

Smoke tests হলো অল্প কয়েকটি গুরুত্বপূর্ণ পরীক্ষা, যা দ্রুত বোঝায় যে deployed application মৌলিক কাজ করতে পারছে কি না।

### Step 6.1 — Health checks

```
curl --fail --show-error --silent \
  https://staging-api.example.test/health/live/
```

```
curl --fail --show-error --silent \
  https://staging-api.example.test/health/ready/
```

এখানে staging URL-টি নিজের URL দিয়ে বদলাবে।

### Step 6.2 — Authentication endpoints

আগে থেকে তৈরি dedicated staging account ব্যবহার করো:

```
export STAGING_API_URL='https://staging-api.example.test'
export STAGING_TEST_EMAIL='loadtest0@example.test'
```

Login request:

```
curl --fail-with-body --silent --show-error \
  -X POST "$STAGING_API_URL/api/auth/login/" \
  -H 'Content-Type: application/json' \
  -d "{\"email\":\"$STAGING_TEST_EMAIL\",\"password\":\"$STAGING_TEST_PASSWORD\"}"
```

`STAGING_TEST_PASSWORD` environment variable-টি আগে নিরাপদভাবে সেট করতে হবে। Command-line history-তে password লিখবে না। Response-এ access ও refresh token থাকতে পারে, তাই output shared terminal log বা CI log-এ প্রকাশ করবে না।

Smoke test-এ অন্তত নিচের বিষয়গুলো পরীক্ষা করো:

1. Health endpoints প্রত্যাশিত status দেয়।
2. Login বৈধ credentials-এ সফল হয়।
3. Invalid credentials প্রত্যাখ্যাত হয়।
4. Authenticated profile endpoint কাজ করে।
5. Token refresh সঠিকভাবে কাজ করে।
6. Logout-এর পর refresh-token policy কার্যকর হয়।
7. Password reset ও email verification flow কাজ করে।
8. Admin-only endpoint সাধারণ user-কে অনুমতি দেয় না।

### Step 6.3 — Automated smoke test script

`deploy/smoke_test.py` তৈরি করো:

```
import osimport sysimport requestsBASE_URL = os.environ["STAGING_API_URL"].rstrip("/")TIMEOUT = 10def check(condition, message):    if not condition:        raise RuntimeError(message)def main():    session = requests.Session()    # 1. Liveness    response = session.get(        f"{BASE_URL}/health/live/",        timeout=TIMEOUT,    )    check(response.status_code == 200, "Liveness failed")    # 2. Readiness    response = session.get(        f"{BASE_URL}/health/ready/",        timeout=TIMEOUT,    )    check(response.status_code == 200, "Readiness failed")    # 3. Login    email = os.environ["STAGING_TEST_EMAIL"]    password = os.environ["STAGING_TEST_PASSWORD"]    response = session.post(        f"{BASE_URL}/api/auth/login/",        json={"email": email, "password": password},        timeout=TIMEOUT,    )    check(response.status_code == 200, "Login failed")    data = response.json()    access = data.get("access")    refresh = data.get("refresh")    check(bool(access), "Login response missing access token")    check(bool(refresh), "Login response missing refresh token")    # 4. Profile    response = session.get(        f"{BASE_URL}/api/auth/profile/",        headers={"Authorization": f"Bearer {access}"},        timeout=TIMEOUT,    )    check(response.status_code == 200, "Profile request failed")    print("Smoke tests passed.")if __name__ == "__main__":    try:        main()    except Exception as exc:        # Exception text-এ response body/token না রেখে generic error।        print(f"Smoke test failed: {type(exc).__name__}", file=sys.stderr)        sys.exit(1)
```

Dependencies:

```
python -m pip install requests
```

Run:

```
python deploy/smoke_test.py
```

এটি একটি ন্যূনতম smoke test; তোমার login serializer যদি token response-এর key-গুলো ভিন্নভাবে দেয়, সেই অনুযায়ী বদলাবে। Script-টি refresh বা logout পরীক্ষা করে না—সেগুলো পরবর্তী end-to-end test-এ যোগ করব।

## 7. Rollback drill: deployment ব্যর্থ হলে কী করবে?

Rollback দুই ধরনের হতে পারে:

- Application rollback: আগের tested Docker image-এ ফিরে যাওয়া।
- Database recovery: backup restore বা forward-fix migration দিয়ে data/schema recovery।

এ দুটো এক নয়। Application rollback সাধারণত দ্রুত, কিন্তু database schema নতুন code-এর সঙ্গে বদলে গেলে পুরোনো application আর কাজ নাও করতে পারে।

### Step 7.1 — আগের image tag সংরক্ষণ

ধরা যাক:

```
export PREVIOUS_IMAGE='ghcr.io/your-org/auth-api:stable-commit-sha'
export CANDIDATE_IMAGE='ghcr.io/your-org/auth-api:new-commit-sha'
```

এগুলো illustrative image references; তোমার actual registry ও immutable tags ব্যবহার করবে।

### Step 7.2 — Failure condition নির্ধারণ

Staging rehearsal-এ নিচের যেকোনোটি ঘটলে release থামানোর নিয়ম নির্ধারণ করো:

- API readiness ব্যর্থ।
- Login বা profile smoke test ব্যর্থ।
- Error rate নির্ধারিত সীমা অতিক্রম।
- p95 latency baseline-এর তুলনায় অস্বাভাবিক বৃদ্ধি।
- Database migration দীর্ঘ lock তৈরি করে।
- Celery queue দ্রুত বাড়ে বা গুরুত্বপূর্ণ task fail হয়।

### Step 7.3 — Application rollback

যদি Compose configuration image environment variable থেকে নেয়:

```
services:
  api:
    image: ${AUTH_API_IMAGE}
```

তাহলে আগের image দিয়ে deploy করার একটি সরল উদাহরণ:

```
AUTH_API_IMAGE="$PREVIOUS_IMAGE" \
docker compose -f compose.staging.yaml up -d api
```

সতর্কতা: শুধু API service rollback করলে Nginx, Celery worker বা অন্য service নতুন image-এ থেকে যেতে পারে। তোমার release topology অনুযায়ী সব সংশ্লিষ্ট application service-এর version সামঞ্জস্যপূর্ণভাবে ফিরিয়ে আনবে। Configuration-এ image variable অন্যভাবে ব্যবহৃত হলে সেই অনুযায়ী command বদলাবে।

এরপর যাচাই করো:

```
docker compose -f compose.staging.yaml ps
docker compose -f compose.staging.yaml logs --tail=100 api
python deploy/smoke_test.py
```

Rollback-এর পর smoke tests সফল হলেও database state ও background jobs যাচাই করতে হবে।

### Step 7.4 — Database rollback policy

Production-এ migration-এর পর backup restore-কে প্রথম প্রতিক্রিয়া হিসেবে ব্যবহার করবে না। Restore করলে migration-এর পর তৈরি হওয়া বৈধ নতুন data হারিয়ে যেতে পারে।

অগ্রাধিকার সাধারণত:

1. Traffic বন্ধ বা সীমিত করে release-এর প্রভাব থামানো।
2. পুরোনো application-এর সঙ্গে compatible schema থাকলে application rollback।
3. Schema পরিবর্তন irreversible বা incompatible হলে tested forward-fix migration বিবেচনা।
4. Data corruption বা গুরুতর database failure হলে incident runbook অনুযায়ী recovery/restore।
5. Restore-এর আগে data-loss window, RPO এবং প্রয়োজনীয় approvals যাচাই।

Staging-এ ইচ্ছাকৃতভাবে একটি release failure ঘটিয়ে এই পুরো sequence অনুশীলন করবে। Production-এ প্রথমবার rollback procedure শিখতে যেও না।

## 8. Authentication flow end-to-end verification

এবার তোমার authentication system-এর সম্পূর্ণ journey যাচাই করব।

Registration

Step 1

User create, password hashing, verification token ও email enqueue।

Email verification

Step 2

Valid token গ্রহণ, expired/used token প্রত্যাখ্যান।

Login ও protected profile

Step 3

JWT issue, authenticated profile access, anonymous request প্রত্যাখ্যান।

Refresh ও logout

Step 4

Refresh rotation, blacklist এবং token revocation behavior।

Password reset / change

Step 5

Single-use token, password validation ও `token_version`-ভিত্তিক revocation।

RBAC ও email change

Step 6

USER/STAFF/ADMIN permissions, confirmation token ও account state যাচাই।

### গুরুত্বপূর্ণ integration test matrix

| Test case                         | প্রত্যাশিত ফল                                           |
| --------------------------------- | ------------------------------------------------------- |
| Registration with valid data      | Account তৈরি; verification policy অনুযায়ী email enqueue |
| Duplicate email                   | Duplicate account তৈরি নয়                               |
| Unverified user login             | Project policy অনুযায়ী প্রত্যাখ্যাত                     |
| Verified user login               | Access ও refresh token পাওয়া যায়                        |
| Missing/invalid JWT               | Protected endpoint থেকে 401                             |
| Refresh with valid token          | নতুন access token; rotation policy অনুসরণ               |
| Refresh old rotated token         | Blacklist policy অনুযায়ী প্রত্যাখ্যাত                   |
| Logout                            | Refresh-token revocation কার্যকর                        |
| Password reset                    | Token single-use; password পরিবর্তিত                    |
| Password change                   | `token_version` বাড়ে; পুরোনো access token অকার্যকর      |
| USER accesses admin endpoint      | 403 বা authentication policy অনুযায়ী প্রত্যাখ্যাত       |
| Email change without confirmation | Email পরিবর্তিত হয় না                                   |
| Deactivated user                  | Account reactivation ছাড়াই authentication বন্ধ          |

`401 Unauthorized` সাধারণত authentication অনুপস্থিত বা অবৈধ হলে, আর `403 Forbidden` authenticated user-এর permission না থাকলে প্রত্যাশিত। তবে তোমার authentication class ও endpoint policy অনুযায়ী নির্দিষ্ট behavior test-এ স্থির করবে।

## 9. CI/CD release gate: সব পরীক্ষা পাস না হলে production নয়

GitHub Actions-এ release workflow-এর ধারণাগত sequence হবে:

```
1. Checkout release commit
2. Install locked dependencies
3. Run Django checks and unit tests
4. Check migration files
5. Build immutable Docker image
6. Scan dependencies and image
7. Deploy the exact image to staging
8. Apply backward-compatible migrations
9. Wait for readiness
10. Run smoke and authentication E2E tests
11. Verify backup and rollback readiness
12. Approve production deployment
13. Deploy and verify again
```

Production approval-এর আগে নিশ্চিত করবে যে staging-এ পরীক্ষিত image-এর digest এবং production-এ deploy হওয়া image-এর digest একই। Staging pass করার পর code বা image বদলে গেলে release candidate আবার যাচাই করতে হবে।

### Release decision tracker

## Go / No-Go decision

Not ready

সবগুলো check বাস্তবে যাচাই করে তবেই complete হিসেবে চিহ্নিত করবে। এটি checklist tracker, automated verification নয়।

CI checks

Unit tests, security checks এবং migration checks সফল।

Artifact integrity

Release image tag/digest immutable ও record করা আছে।

Migration safety

Schema change reviewed এবং rollback compatibility বোঝা হয়েছে।

Backup recovery

Staging backup থেকে পৃথক database-এ restore সফল।

Smoke tests

Health, login ও profile endpoint সফল।

Authentication E2E

Refresh, logout, password reset ও RBAC test সফল।

Observability

Logs, latency, error rate, DB connections ও queue metrics দেখা যাচ্ছে।

Rollback rehearsal

আগের image-এ ফিরে গিয়ে smoke tests সফল হয়েছে।

&#x20;Release report checklist copy করো

## 10. Deployment-এর পর প্রথম 30 মিনিট

Production deployment শেষ হলেই কাজ শেষ নয়। প্রথম 30 মিনিটে পর্যবেক্ষণ করবে:

- API 5xx error rate ও p95/p99 latency।
- Login, refresh এবং profile endpoint-এর success rate।
- PostgreSQL connection saturation ও slow queries।
- Redis availability ও throttling behavior।
- Celery queue depth, retry count ও email delivery failures।
- CPU, memory, disk space এবং container restarts।
- নতুন release-এর পর কোনো migration বা permission regression হয়েছে কি না।

Alert threshold আগে থেকেই নির্ধারণ করবে। গুরুতর সমস্যা হলে incident procedure অনুসরণ করবে—প্রথমে প্রভাব সীমিত করবে, তারপর compatible rollback বা forward fix নির্বাচন করবে।

## Lesson 20 — Final outcome

এই rehearsal শেষ হলে তোমার কাছে থাকা উচিত:

1. একটি versioned release candidate ও immutable image reference।
2. Automated test এবং migration-validation results।
3. Staging deployment-এর health ও smoke-test report।
4. Restore-verified database backup।
5. Successful rollback drill-এর evidence।
6. End-to-end authentication test results।
7. Production go/no-go decision ও deployment runbook।

চূড়ান্ত শিক্ষা: Production deployment কোনো একক command নয়; এটি প্রমাণভিত্তিক release process। Code, database schema, secrets, background jobs এবং recovery procedure—সবগুলো একসঙ্গে কাজ করছে, সেটিই production readiness-এর প্রকৃত মানদণ্ড।

পরবর্তী যৌক্তিক Lesson 21 হবে Release Automation Engineering—GitHub Actions-এ staging deployment, approval-gated production release, image digest promotion, database migration safety gate, automated smoke tests এবং failure হলে deployment pipeline থামিয়ে দেওয়ার সম্পূর্ণ workflow।

-----
