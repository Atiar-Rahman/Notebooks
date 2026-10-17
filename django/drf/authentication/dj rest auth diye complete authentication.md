অবশ্যই! আমরা Django REST Framework দিয়ে ২০টি Lesson-এ একটি complete, production-oriented Forgot Password with Email OTP System তৈরি করব। প্রতিটি Lesson-এ থাকবে Theory + Code + Example + Implementation + Testing + Practice Task। শুরু থেকে শেষ পর্যন্ত নিজের হাতে implement করতে পারবে।

আমাদের project-এ `dj-rest-auth`, `django-allauth`, DRF এবং পরবর্তীতে SimpleJWT ব্যবহার করে authentication system তৈরি করব। Email OTP ও HTML email design-এর জন্য প্রয়োজনীয় custom code-ও লিখব।

# Complete Course: DRF Email OTP Password Reset

![Django plain logo - free Icon PNG, SVG](https://images.openai.com/static-rsc-4/aSYmFommayt5nEBCbd1Mf6TAqUecLA6SNdcRv1U0fjWoZsG537ZuNL2cY5c6XKJAIrkRCBGd0kkaUafFv6cN6lq-zq_v9iF2gC1yDB4HIg4JwRr6jC4dhw64cBZP5UNLhChb9N6_JahJsw-IkYK1z241dTEf8Qo-nhCDszvCysg?purpose=inline)

## Django REST Framework

Beginner → Advanced → Production

20 Lessons

Code-first

Project-based

Final project-এ যা থাকবে

- Forgot Password API
    
- Email-এ ৬ digit OTP
    
- Professional HTML email template
    
- OTP expiry ও secure verification
    
- New Password ও Confirm Password
    
- OTP resend ও rate limiting
    
- Automated tests এবং production email configuration
    

## ২০টি Lesson-এর সম্পূর্ণ Roadmap

## Course progress

0 / 20 completed

Lesson 1: Authentication System-এর Foundation

Authentication বনাম Authorization, password reset flow, API design এবং project requirements।

Lesson 2: Project Setup & Package Installation

Virtual environment, Django, DRF, dj-rest-auth, django-allauth এবং SimpleJWT installation।

Lesson 3: Custom User Model

Email-based user model, USERNAME_FIELD, manager, migrations এবং কেন শুরুতেই custom user model দরকার।

Lesson 4: DRF & dj-rest-auth Configuration

INSTALLED_APPS, middleware, REST_AUTH settings, URL routing এবং built-in endpoints।

Lesson 5: Email Backend & SMTP

Console backend, SMTP settings, environment variables, Gmail/provider credentials ও email testing।

Lesson 6: Professional HTML Email Design

HTML template, inline CSS, OTP card, branding, plain-text fallback এবং responsive email layout।

Lesson 7: OTP Generation

Secure random OTP, Python secrets module, six-digit code এবং OTP generation service।

Lesson 8: OTP Model & Database Design

User/email relation, OTP hash, expiry, used status, attempts এবং database constraints।

Lesson 9: Forgot Password Serializer

Email input validation, normalized email, generic response এবং serializer-level validation।

Lesson 10: Send OTP API

APIView, service layer, OTP save, email send, transaction handling এবং error management।

Lesson 11: OTP Email Integration

Dynamic template context, EmailMultiAlternatives, branded subject ও inbox preview testing।

Lesson 12: Verify OTP API

OTP matching, expiry, attempt limits, single-use verification এবং race-condition prevention।

Lesson 13: Reset Password Serializer

New password, confirm password, password validators এবং safe password update।

Lesson 14: Reset Password API

Verified OTP দিয়ে password change, atomic transaction এবং OTP invalidation।

Lesson 15: Resend OTP API

OTP resend, cooldown, previous code invalidation এবং abuse prevention।

Lesson 16: Security & Rate Limiting

Brute-force protection, generic errors, OTP hashing, secrets management ও audit events।

Lesson 17: React/Next.js Frontend Integration

Forgot password form, OTP input, countdown, resend button ও reset password page।

Lesson 18: Automated Testing

APIClient, mail.outbox, valid/invalid OTP, expiry, password validation এবং regression tests।

Lesson 19: Production Deployment

Production SMTP, environment configuration, HTTPS, logging, Redis-backed throttling ও background email delivery।

Lesson 20: Final Project & Code Review

সব API integrate, complete testing checklist, API documentation, common mistakes এবং deployment checklist।

## প্রতিটি Lesson কীভাবে পড়ব?

প্রতিটি ক্লাসে এই কাঠামো অনুসরণ করব:

1. Theory: বিষয়টি কী এবং কেন ব্যবহার হয়।
    
2. Code explanation: প্রতিটি গুরুত্বপূর্ণ line ব্যাখ্যা।
    
3. Real example: বাস্তব e-commerce বা job portal project-এর উদাহরণ।
    
4. Implementation: কোন file তৈরি করতে হবে, কোথায় code লিখতে হবে।
    
5. API testing: Postman দিয়ে request ও response যাচাই।
    
6. Common mistakes: beginner-দের ভুল ও সমাধান।
    
7. Practice task: পরবর্তী Lesson-এ যাওয়ার আগে নিজে implement করার কাজ।
    

## আমাদের final API flow

1. Forgot Password

`POST /api/auth/password/forgot/`

2. Email OTP

৬ digit code · ৫ মিনিট expiry

3. Verify OTP

`POST /api/auth/password/verify-otp/`

4. Set New Password

`POST /api/auth/password/reset/`

Password Reset Successful

একটি গুরুত্বপূর্ণ design decision: OTP শুধু verify করে `verified=True` করে রাখলে হবে না। অন্য কেউ যেন OTP verification ছাড়াই password reset করতে না পারে, সেজন্য verified reset session/token অথবা একবার ব্যবহারযোগ্য server-side verification state implement করব।

# Lesson 1 শুরু করি

## Authentication System-এর Foundation

### ১. Authentication কী?

Authentication হলো ব্যবহারকারী আসলেই কে, তা যাচাই করা।

উদাহরণ:

- Email + Password দিয়ে login
    
- Email-এ OTP পাঠিয়ে পরিচয় যাচাই
    
- Google login
    

### ২. Password Reset কী?

ধরো, তোমার e-commerce website-এ একজন user password ভুলে গেছে।

তখন তাকে নতুন password তৈরি করার সুযোগ দিতে হবে। কিন্তু যে কেউ যেন অন্যের account-এর password পরিবর্তন করতে না পারে, তার জন্য email OTP দিয়ে verification করব।

### ৩. আমাদের project-এ কোন package কী করবে?

|Package|দায়িত্ব|
|---|---|
|Django|User model, database ও email infrastructure|
|DRF|API endpoints, serializers ও validation|
|`dj-rest-auth`|প্রচলিত authentication ও password-management features|
|`django-allauth`|Account management ও email-related authentication features|
|SimpleJWT|প্রয়োজন হলে login-এর JWT access/refresh tokens|
|Custom OTP service|OTP তৈরি, সংরক্ষণ, যাচাই ও expiry|

`dj-rest-auth` নিজে থেকেই আমাদের চাহিদামতো সম্পূর্ণ email-OTP password-reset workflow তৈরি করে দেবে না। Built-in reset flow সাধারণত email reset link/token ব্যবহার করে; OTP flow-এর জন্য আমরা custom endpoint ও service তৈরি করব।

### ৪. আজকের Practice Task

নিজের project-এর জন্য নিচের বিষয়গুলো ঠিক করো:

- User email দিয়ে account তৈরি করবে।
    
- Password ভুলে গেলে email OTP চাইবে।
    
- OTP পাঁচ মিনিটের মধ্যে verify করতে হবে।
    
- নতুন password ও confirm password মিলতে হবে।
    
- সফল reset-এর পর পুরোনো OTP পুনরায় ব্যবহার করা যাবে না।
    

এগুলোই হবে আমাদের project-এর initial requirements।

পরবর্তী ক্লাস: Lesson 2 — Django Project Setup, Virtual Environment, Package Installation এবং সম্পূর্ণ folder structure। আমরা একদম শুরু থেকে command চালিয়ে project তৈরি করব।


---
# Lesson 2: Django REST Framework Project Setup — Beginner to Professional

এই Lesson-এর লক্ষ্য শুধু command copy করা নয়। এমনভাবে শিখবে, যাতে পরবর্তীতে নতুন computer বা নতুন project-এ নিজেই Django REST Framework authentication project setup করতে পারো।

আজ আমরা Forgot Password + Email OTP project-এর foundation তৈরি করব। প্রতিটি step-এ জানবে কী করছ, কেন করছ, কীভাবে verify করবে এবং error হলে কীভাবে troubleshoot করবে।

## আজকের learning outcomes

Python virtual environment তৈরি ও activate করতে পারব

Django ও DRF project initialize করতে পারব

dj-rest-auth, django-allauth ও SimpleJWT install করতে পারব

Django apps এবং project configuration বুঝতে পারব

Development server চালিয়ে setup নিজে verify করতে পারব

নিজে কাজ শেষ করার পর প্রতিটি checkbox mark করবে।

## Part 1 — Project setup-এর আগে কী বুঝতে হবে?

আমাদের project-এর নাম হবে `otp_auth_project`, আর Django app-এর নাম হবে `accounts`।

otp_auth_project/

পুরো Django project

config/

Settings, root URLs, WSGI/ASGI

accounts/

User, OTP, serializers, views

এটি লক্ষ্য architecture-এর একটি সরল ধারণা। Django-এর default folder structure আমরা পরের ধাপে তৈরি করব।

### Project ও app-এর পার্থক্য

- Project: পুরো application-এর configuration ও apps-এর সমষ্টি।
- App: একটি নির্দিষ্ট feature বা domain-এর code; যেমন `accounts`, `products`, `orders`।
- Virtual environment: এই project-এর Python packages আলাদা রাখে, যাতে অন্য project-এর dependency-র সঙ্গে conflict না হয়।

উদাহরণ: একটি e-commerce project-এ `accounts`, `products`, `orders`, `payments` আলাদা app হতে পারে।

## Part 2 — Terminal দিয়ে project তৈরি করো

আমরা Ubuntu/Linux ধরে এগোব।

### Step 1: Python version যাচাই

Terminal খুলে চালাও:

```
python3 --version
pip3 --version
```

কেন? Django install করার আগে Python ও pip আছে কি না নিশ্চিত হতে হবে।

Expected output-এর উদাহরণ:

```
Python 3.12.x
pip 24.x
```

তোমার version আলাদা হতে পারে। `pip3` না থাকলে Ubuntu-তে সাধারণত `python3-pip` package লাগতে পারে।

### Step 2: Project directory তৈরি

```
mkdir otp_auth_project
cd otp_auth_project
```

এখন যাচাই করো:

```
pwd
```

তোমার terminal-এ `otp_auth_project`-এ শেষ হওয়া path দেখা উচিত।

### Step 3: Virtual environment তৈরি

```
python3 -m venv .venv
```

এখানে:

- `python3`: Python interpreter।
- `-m venv`: Python-এর built-in virtual environment module চালায়।
- `.venv`: environment-এর directory name।

যদি `ensurepip` বা `venv`-সংক্রান্ত error আসে, Ubuntu-তে প্রয়োজন অনুযায়ী `python3-venv` install করতে হতে পারে।

### Step 4: Virtual environment activate

```
source .venv/bin/activate
```

এখন terminal prompt-এর শুরুতে সাধারণত `(.venv)` দেখতে পাবে।

তারপর:

```
which python
python --version
python -m pip --version
```

`which python`-এর output তোমার project-এর `.venv/bin/python` নির্দেশ করবে।

কেন `python -m pip` ব্যবহার করছি? এতে যে Python interpreter ব্যবহার করছ, তার সঙ্গে সংশ্লিষ্ট pip-ই packages install করবে।

### Step 5: pip upgrade ও dependency file তৈরি

```
python -m pip install --upgrade pip
```

তারপর project-এর root directory-তে `requirements.txt` নামে file তৈরি করো। আমরা package versions পরীক্ষা করে পরে pin করব; আপাতত install করা versions record করার জন্য setup শেষে `pip freeze` ব্যবহার করব।

## Part 3 — প্রয়োজনীয় packages install করো

### Step 6: কোন package কেন লাগবে?

| Package                         | ব্যবহার                                     |
| ------------------------------- | ------------------------------------------- |
| `Django`                        | Backend framework                           |
| `djangorestframework`           | REST API তৈরি                               |
| `dj-rest-auth`                  | Authentication endpoints                    |
| `django-allauth`                | Account management ও email-related features |
| `djangorestframework-simplejwt` | JWT access ও refresh tokens                 |

এখন virtual environment active থাকা অবস্থায় চালাও:

```
python -m pip install Django
python -m pip install djangorestframework
python -m pip install dj-rest-auth
python -m pip install django-allauth
python -m pip install djangorestframework-simplejwt
```

একটি command-এও install করতে পারো:

```
python -m pip install \
    Django \
    djangorestframework \
    dj-rest-auth \
    django-allauth \
    djangorestframework-simplejwt
```

Theory: package install করলেই feature সম্পূর্ণ configure হয়ে যায় না। যেমন, SimpleJWT install করার পরও DRF authentication class configure করতে হবে। একইভাবে `dj-rest-auth` install করার পর URL ও settings configure করতে হবে।

### Step 7: Installation verify করো

```
python -m pip show Django
python -m pip show djangorestframework
python -m pip show dj-rest-auth
python -m pip show django-allauth
python -m pip show djangorestframework-simplejwt
```

সবগুলো package-এর metadata দেখা গেলে installation হয়েছে।

আরও একটি useful command:

```
python -m pip check
```

এটি installed packages-এর dependency conflict আছে কি না পরীক্ষা করে।

### Step 8: `requirements.txt` তৈরি

```
python -m pip freeze > requirements.txt
```

এখন `requirements.txt`-এ installed package ও version-এর তালিকা থাকবে।

উদাহরণ:

```
Django==<installed-version>
djangorestframework==<installed-version>
dj-rest-auth==<installed-version>
```

এগুলো শুধু format বোঝানোর উদাহরণ। আসল version file-এ স্বয়ংক্রিয়ভাবে লেখা হবে।

কেন প্রয়োজন? অন্য computer বা server-এ project setup করতে এই file থেকে dependencies install করা যাবে:

```
python -m pip install -r requirements.txt
```

Production-এ যাওয়ার আগে package versions যাচাই, test এবং pin করে রাখবে। শুধু latest package install করলেই সব package পরস্পরের সঙ্গে compatible হবে, এমন নিশ্চয়তা নেই।

## Part 4 — Django project তৈরি

### Step 9: Project initialize করো

Project root-এ থেকেই চালাও:

```
django-admin startproject config .
```

এখানে:

- `startproject`: নতুন Django project তৈরি করে।
- `config`: configuration package-এর নাম।
- `.`: বর্তমান directory-তে project তৈরি করে।

শেষের dot (`.`) গুরুত্বপূর্ণ। এটি বাদ দিলে আরেকটি nested directory তৈরি হতে পারে।

### Step 10: প্রথমবার server চালাও

```
python manage.py check
python manage.py migrate
python manage.py runserver
```

প্রতিটি command-এর কাজ:

- `check`: Django configuration-এর সাধারণ সমস্যা খুঁজবে।
- `migrate`: প্রয়োজনীয় database tables তৈরি করবে।
- `runserver`: development server চালাবে।

Browser-এ খোলো:

`http://127.0.0.1:8000/`

Django-এর welcome page দেখা গেলে project initialize হয়েছে।

মনে রেখো: `runserver` development-এর জন্য। এটি production server নয়। Production deployment আমরা পরের পর্যায়ে শিখব।

Server বন্ধ করতে terminal-এ `Ctrl + C` চাপো।

## Part 5 — `accounts` app তৈরি

### Step 11: App তৈরি করো

```
python manage.py startapp accounts
```

এখন Django project-এর মধ্যে `accounts` নামে একটি app তৈরি হবে।

কেন আলাদা app? আমাদের authentication-এর code এক জায়গায় রাখতে পারব। পরবর্তীতে OTP model, password reset serializers, API views, email service ও tests এই app-এর মধ্যে সংগঠিত করব।

### Step 12: `settings.py` খুঁজে বের করো

ফাইলটি এখানে:

```
config/settings.py
```

এখনই সব package settings যোগ করার দরকার নেই। সেগুলো Lesson 3 ও Lesson 4-এ ব্যাখ্যাসহ configure করব। তবে Django-কে আমাদের `accounts` app সম্পর্কে জানাতে হবে।

`config/settings.py`-এর `INSTALLED_APPS` তালিকায় যোগ করো:

```
INSTALLED_APPS = [    # Django built-in apps    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    # Third-party apps    "rest_framework",    # Local apps    "accounts",]
```

Django project তৈরি করার সময় default `INSTALLED_APPS`-এ থাকা entries মুছে ফেলবে না। উপরের তালিকাটি default entries-সহ দেখানো হয়েছে; তোমার ফাইলে বিদ্যমান configuration বজায় রাখবে।

এখন চালাও:

```
python manage.py check
```

Error না থাকলে ভালো।

## Part 6 — Professional folder structure তৈরি

এখন থেকে project-টি এমনভাবে সাজাব, যাতে বড় হলেও code খুঁজে পাওয়া সহজ হয়।

### Step 13: প্রয়োজনীয় directories তৈরি

Terminal-এ চালাও:

```
mkdir -p accounts/services
mkdir -p accounts/templates/emails
mkdir -p accounts/tests
```

এখন `accounts/` directory-র মধ্যে নিচের structure তৈরি হবে:

```
accounts/
├── migrations/
├── services/
├── templates/
│   └── emails/
├── tests/
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
└── views.py
```

`serializers.py`, `urls.py` এবং `tests/`-এর ভেতরের test files প্রয়োজন অনুযায়ী পরে তৈরি করবে।

কোন directory-তে কী থাকবে?

| File / Folder       | দায়িত্ব                                    |
| ------------------- | ------------------------------------------ |
| `models.py`         | User ও OTP database models                 |
| `serializers.py`    | Request validation                         |
| `views.py`          | API request ও response                     |
| `urls.py`           | API routing                                |
| `services/`         | OTP generation, email sending, reset logic |
| `templates/emails/` | HTML email design                          |
| `tests/`            | Automated tests                            |

`services/` ও `templates/emails/` Django নিজে তৈরি করে না; আমরা নিজেদের architecture অনুযায়ী তৈরি করছি।

`services/`-কে Python package হিসেবে ব্যবহার করতে চাইলে তৈরি করো:

```
touch accounts/services/__init__.py
touch accounts/serializers.py
touch accounts/urls.py
```

### Step 14: `.gitignore` তৈরি করো

Project root-এ `.gitignore` file তৈরি করো:

```
.venv/
__pycache__/
*.py[cod]
.env
db.sqlite3
media/
staticfiles/
```

কেন?

- `.venv/`: environment-এর সব installed package Git-এ রাখার প্রয়োজন নেই।
- `.env`: secret credentials যেন GitHub-এ প্রকাশ না হয়।
- `db.sqlite3`: development database file সাধারণত commit করার প্রয়োজন নেই।
- `__pycache__/`: Python-এর generated cache files।

Production project-এ database backup, migrations, static/media files ও deployment configuration-এর handling আলাদাভাবে পরিকল্পনা করতে হবে। `.gitignore` কোনো file আগে থেকেই tracked থাকলে সেটিকে স্বয়ংক্রিয়ভাবে Git থেকে সরায় না।

## Part 7 — Final setup verify করো

### Step 15: Final commands

```
python manage.py check
python manage.py migrate
python -m pip check
python manage.py runserver
```

সব ঠিক থাকলে server চালু হবে। Terminal-এ `Ctrl + C` দিয়ে বন্ধ করবে।

### Expected project structure

otp_auth_project/

config/

settings.py, urls.py

accounts/

Authentication app

.venv/

manage.py

requirements.txt

.gitignore

## Part 8 — Common errors ও troubleshooting

| Error                               | সম্ভাব্য কারণ                                 | সমাধান                                                |
| ----------------------------------- | --------------------------------------------- | ----------------------------------------------------- |
| `No module named django`            | ভুল Python environment                        | `.venv` activate করে install করো                      |
| `No module named venv`              | Ubuntu-তে venv support নেই                    | `python3-venv` install করো                            |
| `manage.py not found`               | ভুল directory                                 | `cd otp_auth_project` করো                             |
| `Port is already in use`            | Port 8000 অন্য process ব্যবহার করছে           | `python manage.py runserver 8001`                     |
| `pip check` dependency error        | Package version conflict                      | Error message দেখে compatible versions ঠিক করো        |
| `ModuleNotFoundError` for a package | Package install হয়নি বা অন্য interpreter চলছে | `which python` ও `python -m pip show ...` পরীক্ষা করো |

## Part 9 — তোমার Practice Assignment

এখন নিচের কাজগুলো নিজে করার চেষ্টা করো। প্রথমবার code দেখে করলেও সমস্যা নেই, কিন্তু দ্বিতীয়বার না দেখে করতে পারাই লক্ষ্য।

## Lesson 2 assignment

0/5

Environment setup

Virtual environment তৈরি, activate ও Python path verify করো।

Package installation

সব পাঁচটি package install করে requirements.txt তৈরি করো।

Project creation

config project ও accounts app তৈরি করো।

Folder organization

services, templates/emails এবং tests directories তৈরি করো।

Verification

manage.py check, migrate ও runserver চালিয়ে পরীক্ষা করো।

Assignment review

## Self-test: তুমি বুঝেছ কি না?

১. Virtual environment কেন ব্যবহার করি?

Django-এর UI বানাতে

Project-এর Python dependencies আলাদা রাখতে

Database তৈরি করতে

২. \`django-admin startproject config .\`-এ dot-এর কাজ কী?

নতুন virtual environment বানায়

বর্তমান directory-তে project তৈরি করে

Database migrate করে

৩. OTP email-এর HTML design কোথায় রাখব?

accounts/templates/emails/

accounts/migrations/

.venv/

## পরবর্তী Lesson

Lesson 3 — Custom User Model: Email-based Login, User Manager, `USERNAME_FIELD`, Password Hashing এবং Database Migration।

এই Lesson-টি খুব গুরুত্বপূর্ণ। কারণ User Model ভুলভাবে শুরু করলে পরে authentication system-এ বড় পরিবর্তন করতে হতে পারে। আমরা প্রথমে বুঝব, তারপর model লিখব, তারপর database-এ migrate করে নিজের implementation verify করব।

---
# Lesson 3 — Custom User Model in Django REST Framework

আজকের লক্ষ্য: তুমি যেন নিজের হাতে এমন একটি Custom User Model তৈরি করতে পারো, যেখানে user email ও password দিয়ে account তৈরি করবে, Django নিরাপদভাবে password সংরক্ষণ করবে এবং পরবর্তীতে Forgot Password + Email OTP feature যুক্ত করা যাবে।

আজ শুধু code copy করব না। প্রতিটি অংশ কেন লিখছি, কীভাবে কাজ করে, কীভাবে test করবে এবং অন্য project-এ কীভাবে ব্যবহার করবে—সব শিখব।

## আজকের syllabus

Default User Model ও Custom User Model-এর পার্থক্য বুঝব

AbstractUser ও AbstractBaseUser-এর পার্থক্য শিখব

Email দিয়ে login করার জন্য User Model তৈরি করব

Custom User Manager লিখব

Password hashing ও superuser creation পরীক্ষা করব

AUTH_USER_MODEL ও migrations সঠিকভাবে configure করব

0 / 6টি learning goal সম্পন্ন

## Part 1 — Custom User Model কেন প্রয়োজন?

Django-তে default User Model আছে। কিন্তু আমাদের project-এ email হবে login identifier। ভবিষ্যতে একই authentication system e-commerce, job portal বা hotel management project-এ ব্যবহার করতে চাই।

Default User Model-এর সাধারণ field:

| Field        | কাজ                                      |
| ------------ | ---------------------------------------- |
| `username`   | Username                                 |
| `email`      | Email address                            |
| `password`   | Hashed password                          |
| `first_name` | First name                               |
| `last_name`  | Last name                                |
| `is_staff`   | Django admin access-এর জন্য staff status |
| `is_active`  | Account active কি না                     |

আমরা চাই:

- Email হবে unique login identifier।
- Username বাধ্যতামূলক হবে না।
- Password Django-র built-in secure hashing দিয়ে সংরক্ষিত হবে।
- Admin ও superuser তৈরির সুবিধা থাকবে।
- ভবিষ্যতে Profile ও OTP model সহজে যুক্ত করা যাবে।

এজন্য আমরা `AbstractUser` extend করব।

## Part 2 — `AbstractUser` বনাম `AbstractBaseUser`

AbstractUser

Django-র built-in user fields, permissions এবং group support পাওয়া যায়। কিছু field পরিবর্তন করে email-based login তৈরি করা সহজ।

এই course-এ ব্যবহার করব

AbstractBaseUser

Password hashing ও basic authentication support পাওয়া যায়, কিন্তু fields, manager এবং permissions-related configuration আরও বেশি নিজে তৈরি করতে হয়।

Advanced customization

Rule of thumb: `AbstractUser` দিয়েই শুরু করো, যদি না তোমার requirements সত্যিই অনেক বেশি custom হয়।

## Part 3 — প্রথমে project structure যাচাই করো

Lesson 2-এ তৈরি করা project-এ আমরা এই file-এ কাজ করব:

```
otp_auth_project/
├── manage.py
├── config/
│   └── settings.py
└── accounts/
    ├── models.py
    └── managers.py
```

Terminal-এ project root-এ যাও এবং virtual environment activate করো:

```
cd otp_auth_project
source .venv/bin/activate
```

নিজের project-এর path আলাদা হলে সেই path ব্যবহার করবে।

গুরুত্বপূর্ণ: Custom User Model প্রথম migration-এর আগেই configure করা সবচেয়ে সহজ। যদি ইতিমধ্যে default User Model ব্যবহার করে migrations ও data তৈরি করে থাকো, তাহলে সরাসরি model পরিবর্তন কোরো না; migration plan আগে পর্যালোচনা করতে হবে।

## Part 4 — Custom User Manager তৈরি

প্রথমে বুঝি, Manager কী?

Django Manager হলো database-এ model-এর records নিয়ে কাজ করার interface। যেমন:

```
User.objects.all()User.objects.create_user(...)User.objects.create_superuser(...)
```

আমরা `create_user()` এবং `create_superuser()`-এর মাধ্যমে নিশ্চিত করব যে user তৈরি করার সময় password plain text হিসেবে save না হয়।

### Step 1: `accounts/managers.py` তৈরি করো

```
from django.contrib.auth.base_user import BaseUserManagerclass UserManager(BaseUserManager):    def create_user(self, email, password=None, **extra_fields):        if not email:            raise ValueError("Email is required")        email = self.normalize_email(email)        user = self.model(            email=email,            **extra_fields,        )        user.set_password(password)        user.save(using=self._db)        return user    def create_superuser(self, email, password=None, **extra_fields):        extra_fields.setdefault("is_staff", True)        extra_fields.setdefault("is_superuser", True)        extra_fields.setdefault("is_active", True)        if extra_fields.get("is_staff") is not True:            raise ValueError("Superuser must have is_staff=True")        if extra_fields.get("is_superuser") is not True:            raise ValueError("Superuser must have is_superuser=True")        return self.create_user(            email=email,            password=password,            **extra_fields,        )
```

### Step 2: প্রতিটি গুরুত্বপূর্ণ অংশ বুঝে নাও

`self.normalize_email(email)`

Email address-এর domain অংশ normalize করে। তবে এটি সব ধরনের email equivalence নিশ্চিত করে না; তাই email uniqueness-এর জন্য database constraint-ও প্রয়োজন।

`self.model(...)`

Manager-এর সঙ্গে যুক্ত User Model-এর একটি object তৈরি করে।

`user.set_password(password)`

Password-কে Django-র password hasher দিয়ে hash করে। সরাসরি `user.password = password` লিখলে নিরাপদ password handling হবে না।

`user.save(using=self._db)`

সঠিক database alias ব্যবহার করে user-কে database-এ save করে।

`create_superuser()`

Superuser-এর জন্য `is_staff=True` এবং `is_superuser=True` নিশ্চিত করে। এতে Django admin ও permission system সঠিকভাবে কাজ করতে পারে।

একটি গুরুত্বপূর্ণ security detail: উপরের manager-এ `password=None` অনুমোদিত signature হলেও password ছাড়া সাধারণ user তৈরি করতে চাই না। তাই `create_user()`-এ password বাধ্যতামূলক করার validation যোগ করা ভালো। আমাদের final version-এ সেটিই করব।

## Part 5 — Custom User Model তৈরি

### Step 3: `accounts/models.py`

এখন `accounts/models.py`-তে লিখো:

```
from django.contrib.auth.models import AbstractUserfrom django.db import modelsfrom .managers import UserManagerclass User(AbstractUser):    username = None    email = models.EmailField(        unique=True,        db_index=True,    )    USERNAME_FIELD = "email"    REQUIRED_FIELDS = []    objects = UserManager()    def __str__(self):        return self.email
```

### Step 4: Code-এর logic বুঝে নাও

| Code                                     | ব্যাখ্যা                                                        |
| ---------------------------------------- | --------------------------------------------------------------- |
| `AbstractUser`                           | Django-র built-in user fields ও permissions ব্যবহার             |
| `username = None`                        | Username field বাদ দেওয়া                                        |
| `email = models.EmailField(unique=True)` | Email-কে unique database field করা                              |
| `USERNAME_FIELD = "email"`               | Django authentication-এ email-কে identifier হিসেবে ব্যবহার      |
| `REQUIRED_FIELDS = []`                   | `createsuperuser` command-এ email ছাড়া অন্য required prompt নেই |
| `objects = UserManager()`                | আমাদের custom manager ব্যবহার                                   |
| `__str__()`                              | Admin ও debugging-এ email দেখানো                                |

একটি বিষয় পরিষ্কার: `USERNAME_FIELD = "email"` দিলেই তোমার সব login endpoint স্বয়ংক্রিয়ভাবে email-based হয়ে যাবে না। Authentication backend ও API serializer-এর configuration-ও সঠিক হতে হবে। সেগুলো Lesson 4-এ করব।

## Part 6 — `settings.py` configure করো

### Step 5: `AUTH_USER_MODEL` যোগ করো

`config/settings.py`-এর নিচের দিকে যোগ করো:

```
AUTH_USER_MODEL = "accounts.User"
```

এখানে:

- `accounts` হলো app label।
- `User` হলো model name।

Django-কে জানানো হচ্ছে, এখন থেকে এই project-এর user model হবে `accounts.User`।

কেন এটি এত গুরুত্বপূর্ণ?

Django-এর built-in authentication, admin, foreign keys এবং অন্যান্য app-এর user relations এই setting-এর ওপর নির্ভর করে। এটি ভুল হলে migration ও authentication-এ সমস্যা হতে পারে।

## Part 7 — Migration করার আগে গুরুত্বপূর্ণ সতর্কতা

Lesson 2-এ তুমি `python manage.py migrate` চালিয়ে থাকলে `db.sqlite3`-এ Django-র default user-related tables তৈরি হয়ে থাকতে পারে।

Custom User Model-কে `accounts` app-এর প্রথম migration-এ রাখতে হবে। তাই নতুন learning project-এ database reset করা সহজ হতে পারে।

শুধু disposable development database হলে নিচের reset পদ্ধতি ব্যবহার করো। গুরুত্বপূর্ণ data থাকলে database delete করবে না।

```
# Stop the development server first.

# Only for a fresh, disposable SQLite learning database:
rm db.sqlite3

# If accounts already has generated migration files,
# remove only its numbered migration files.
# Preserve accounts/migrations/__init__.py.
```

উপরের শেষ command-টি comment, সরাসরি executable command নয়। Numbered migration files থাকলে আগে দেখে নিয়ে সেগুলো সরাবে। Third-party বা Django-এর migration files কখনো delete করবে না।

তারপর চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
```

Expected result: `accounts` app-এর জন্য initial migration তৈরি হবে এবং database-এ custom user table তৈরি হবে।

যদি আগে থেকেই গুরুত্বপূর্ণ database data থাকে, migration reset না করে আলাদা migration plan তৈরি করতে হবে।

## Part 8 — Password ছাড়া user creation বন্ধ করো

আগের Manager-এ আমরা `password=None` রেখেছিলাম method signature-এ। Django-তে password ছাড়া user তৈরি করার বৈধ use case আছে, কিন্তু এই project-এ আমরা password-based registration চাই। তাই এখন manager-টি একটু শক্তিশালী করি।

`accounts/managers.py`-এর সম্পূর্ণ code এই version দিয়ে replace করো:

```
from django.contrib.auth.base_user import BaseUserManagerclass UserManager(BaseUserManager):    def create_user(self, email, password=None, **extra_fields):        if not email:            raise ValueError("Email is required")        if not password:            raise ValueError("Password is required")        email = self.normalize_email(email)        user = self.model(            email=email,            **extra_fields,        )        user.set_password(password)        user.save(using=self._db)        return user    def create_superuser(self, email, password=None, **extra_fields):        if not password:            raise ValueError("Superuser password is required")        extra_fields.setdefault("is_staff", True)        extra_fields.setdefault("is_superuser", True)        extra_fields.setdefault("is_active", True)        if extra_fields.get("is_staff") is not True:            raise ValueError("Superuser must have is_staff=True")        if extra_fields.get("is_superuser") is not True:            raise ValueError("Superuser must have is_superuser=True")        return self.create_user(            email=email,            password=password,            **extra_fields,        )
```

এখন `create_user()`-এ password না দিলে error হবে।

তবে মনে রেখো, এই manager শুধু user creation-এর নিয়ম নিয়ন্ত্রণ করে। Password-এর minimum length, common password, similarity ইত্যাদি validation registration/reset serializer বা Django password validators-এও configure করতে হবে।

## Part 9 — Django Admin-এ Custom User দেখাও

### Step 6: `accounts/admin.py`

```
from django.contrib import adminfrom django.contrib.auth.admin import UserAdminfrom .models import User@admin.register(User)class CustomUserAdmin(UserAdmin):    ordering = ("email",)    list_display = (        "id",        "email",        "is_staff",        "is_active",    )    search_fields = ("email",)    fieldsets = (        (None, {"fields": ("email", "password")}),        (            "Permissions",            {                "fields": (                    "is_active",                    "is_staff",                    "is_superuser",                    "groups",                    "user_permissions",                )            },        ),        ("Important dates", {"fields": ("last_login", "date_joined")}),    )    add_fieldsets = (        (            None,            {                "classes": ("wide",),                "fields": (                    "email",                    "password1",                    "password2",                    "is_staff",                    "is_superuser",                ),            },        ),    )
```

এটি কেন করছি?

Django-এর default `UserAdmin` username field আশা করে। আমরা username বাদ দিয়েছি, তাই admin-এর list, search, edit ও add form-কে email-based configuration দিতে হচ্ছে।

Admin-এর মাধ্যমে password set করলে Django-র password handling ব্যবহার হবে; raw password database-এ লেখা উচিত নয়।

## Part 10 — User Model নিজে test করো

### Step 7: Django shell খোলো

```
python manage.py shell
```

Shell-এর ভেতরে এক এক করে চালাও:

```
from django.contrib.auth import get_user_modelUser = get_user_model()user = User.objects.create_user(    email="student@example.com",    password="A-Strong-Password-2026!",)print(user.email)print(user.check_password("A-Strong-Password-2026!"))print(user.check_password("wrong-password"))
```

Expected result:

```
student@example.com
True
False
```

প্রথম password check `True` হবে, কারণ password সঠিক। ভুল password দিলে `False` হবে।

Shell থেকে বের হতে:

```
exit()
```

### Step 8: Database-এ password কীভাবে থাকে?

Database-এ সাধারণত password-এর বদলে Django password hasher-এর encoded hash থাকে।

```
user.password
```

এটি চালালে hash-জাতীয় string দেখবে। এর format configured password hasher-এর ওপর নির্ভর করে।

কখনো `user.password`-কে plain password ধরে নিও না। Password যাচাই করতে `check_password()` ব্যবহার করবে।

## Part 11 — Superuser তৈরি করো

Terminal-এ:

```
python manage.py createsuperuser
```

Email ও password দাও।

যদি migration ও admin configuration ঠিক থাকে, superuser তৈরি হবে।

তারপর server চালাও:

```
python manage.py runserver
```

Browser-এ খোলো:

`http://127.0.0.1:8000/admin/`

তৈরি করা superuser দিয়ে login করে `Users` section পরীক্ষা করো।

যদি login না হয়, error message, `AUTH_USER_MODEL`, migrations এবং `accounts/admin.py` পরীক্ষা করো।

## Part 12 — Automated checks ও common mistakes

### Step 9: Model configuration যাচাই

Shell থেকে বের হয়ে terminal-এ চালাও:

```
python manage.py check
python manage.py makemigrations --check --dry-run
python manage.py showmigrations accounts
```

এগুলোর কাজ:

- `check`: Django configuration-এর সমস্যা খুঁজবে।
- `makemigrations --check --dry-run`: model ও migration-এর মধ্যে নতুন migration দরকার কি না যাচাই করবে।
- `showmigrations accounts`: `accounts` app-এর migration status দেখাবে।

যদি `No changes detected` দেখায়, তাহলে model-এর বর্তমান অবস্থার জন্য নতুন migration দরকার নেই।

### Step 10: Duplicate email পরীক্ষা

Email field-এ `unique=True` দিয়েছি। তাই একই email দিয়ে দ্বিতীয় user তৈরি করলে database uniqueness constraint-এর কারণে operation ব্যর্থ হবে।

পরীক্ষা করতে:

```
User.objects.create_user(    email="student@example.com",    password="Another-Strong-Password-2026!",)
```

এই email আগে তৈরি করা থাকলে database error হবে। Django shell-এ এ ধরনের error পরীক্ষা করতে `try/except` ব্যবহার করা ভালো, কারণ database transaction-এর অবস্থা অনুযায়ী recovery প্রয়োজন হতে পারে।

### Common mistakes checklist

| ভুল                                                             | সঠিক পদ্ধতি                                                                           |
| --------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Custom User Model তৈরি করার পর `AUTH_USER_MODEL` ভুলে যাওয়া     | `accounts.User` configure করা                                                         |
| `user.password = raw_password` ব্যবহার করা                      | `user.set_password()` ব্যবহার করা                                                     |
| Model পরিবর্তনের পর migration না করা                            | `makemigrations` ও `migrate` চালানো                                                   |
| Default admin configuration 그대로 রাখা                            | Custom `UserAdmin` configure করা                                                      |
| Existing database data না বুঝে delete করা                       | আগে backup ও migration plan তৈরি করা                                                  |
| Email unique হলেই case-insensitive uniqueness নিশ্চিত ধরে নেওয়া | প্রয়োজন অনুযায়ী database-level case-insensitive constraint ও normalization design করা |

আরও একটি গুরুত্বপূর্ণ বিষয়: Custom User Model-এ `unique=True` ব্যবহার করলে database duplicate email আটকাবে। কিন্তু কিছু database configuration-এ `User@Example.com` ও `user@example.com` আলাদা value হিসেবে বিবেচিত হতে পারে। Email case policy-টি আমরা registration serializer ও database design-এর সময় ঠিক করব।

## Part 13 — Lesson 3 assignment

এবার নিজে implement করার চেষ্টা করো। নিচের checklist ব্যবহার করো।

## Practice tracker

0/6

Custom User Model

AbstractUser extend করে username বাদ দাও এবং email unique করো।

User Manager

create_user ও create_superuser implement করো।

Settings

AUTH_USER_MODEL = 'accounts.User' configure করো।

Migration

Fresh development database-এ initial custom user migration তৈরি করো।

Password test

create_user দিয়ে user তৈরি করে check_password() যাচাই করো।

Admin test

Superuser তৈরি করে /admin/ থেকে email দিয়ে login করো।

আমার assignment review করো

## Self-test

১. Email দিয়ে login-এর জন্য কোন setting প্রয়োজন?

AUTH_USER_MODEL = 'accounts.User'

EMAIL_BACKEND = 'accounts.User'

LOGIN_URL = 'accounts.User'

২. Password database-এ নিরাপদভাবে সংরক্ষণের জন্য কী ব্যবহার করবে?

user.password = password

user.set_password(password)

print(password)

৩. কেন AbstractUser ব্যবহার করছি?

কারণ এতে built-in user fields ও permissions পাওয়া যায়

কারণ এটি email পাঠায়

কারণ এটি JWT নিজে থেকেই তৈরি করে

## Next: Lesson 4

Django REST Framework + `dj-rest-auth` Configuration

পরের Lesson-এ আমরা শিখব:

1. `INSTALLED_APPS`-এ `dj-rest-auth` ও `django-allauth` কীভাবে configure করতে হয়।
2. Authentication middleware ও account settings-এর ভূমিকা।
3. `urls.py`-তে registration, login ও password-reset routes যুক্ত করা।
4. SimpleJWT-এর access/refresh token settings।
5. API endpoint চালিয়ে configuration যাচাই করা।

তারপর Lesson 5-এ email backend ও SMTP, Lesson 6-এ professional HTML email design এবং পরের Lesson-গুলোতে OTP generation, expiry, verification ও password reset implement করব।

মনে রাখবে: Lesson 3-এর সবচেয়ে গুরুত্বপূর্ণ কাজ হলো Custom User Model সঠিকভাবে configure করা। এটি ঠিক থাকলে পরের authentication features তৈরি করা অনেক সহজ হবে।

----
# Lesson 4 — Django REST Framework + `dj-rest-auth` Configuration

আজ আমরা তোমার Custom User Model-এর ওপর authentication infrastructure তৈরি করব, যাতে পরবর্তী Lesson-গুলোতে Email OTP, Forgot Password, HTML Email এবং JWT Authentication যোগ করতে পারি।

এই Lesson-এর লক্ষ্য হলো, নিজে নতুন DRF project-এ authentication packages configure করে API চালাতে পারা এবং প্রতিটি setting কেন প্রয়োজন তা ব্যাখ্যা করতে পারা।

## আজকের learning outcomes

Django ও DRF authentication settings বুঝব

dj-rest-auth ও django-allauth configure করব

Custom User Model-এর সঙ্গে package integration করব

URL routing ও JWT settings তৈরি করব

Authentication API-গুলো নিজে test করব

Common configuration errors debug করব

0 / 6 objectives completed

## Part 1 — Authentication architecture বুঝে নাও

আমাদের project-এ প্রতিটি package-এর আলাদা দায়িত্ব আছে।

React / Next.js / Postman

API request পাঠায়

Django REST Framework

Request, serializer, authentication ও permission

dj-rest-auth

Authentication API

SimpleJWT

JWT tokens

Custom User Model + Database

User information ও authentication state

`django-allauth` account management ও email/social authentication-এর বিভিন্ন feature দেয়। তবে `dj-rest-auth`-এর সব endpoint, allauth-এর সব feature এবং JWT—কোনোটিই package install করলেই সম্পূর্ণ configure হয়ে যায় না।

## Part 2 — Version compatibility যাচাই

Lesson 2-এ আমরা Django, DRF, `dj-rest-auth`, `django-allauth` এবং SimpleJWT install করেছি।

প্রথমে project directory-তে যাও:

```
cd otp_auth_project
source .venv/bin/activate
```

তারপর:

```
python --version
python -m pip show Django
python -m pip show djangorestframework
python -m pip show dj-rest-auth
python -m pip show django-allauth
python -m pip show djangorestframework-simplejwt
python -m pip check
```

কেন এই step গুরুত্বপূর্ণ?

Package-এর version অনুযায়ী `settings.py`, registration configuration এবং URL setup-এ কিছু পার্থক্য থাকতে পারে। তাই error হলে অন্ধভাবে পুরোনো tutorial-এর settings copy করবে না।

## Part 3 — `INSTALLED_APPS` configure করো

খোলো:

```
config/settings.py
```

`INSTALLED_APPS`-এ প্রয়োজনীয় apps যোগ করো। আগের Django built-in apps এবং `accounts` app রেখে নিচের entries নিশ্চিত করো:

```
INSTALLED_APPS = [    # Django built-in apps    "django.contrib.admin",    "django.contrib.auth",    "django.contrib.contenttypes",    "django.contrib.sessions",    "django.contrib.messages",    "django.contrib.staticfiles",    "django.contrib.sites",    # Django REST Framework    "rest_framework",    # django-allauth    "allauth",    "allauth.account",    # dj-rest-auth    "dj_rest_auth",    "dj_rest_auth.registration",    # Local apps    "accounts",]
```

`django.contrib.sites` কেন লাগছে? Registration ও account management-এর কিছু feature site configuration ব্যবহার করে।

এখানে `dj_rest_auth.registration` যোগ করেছি, কারণ ভবিষ্যতে registration API ব্যবহার করব। Social login এখনই configure করছি না।

## Part 4 — Middleware configure করো

`settings.py`-তে `MIDDLEWARE` খুঁজে বের করো। Django-এর default middleware রেখে `allauth.account.middleware.AccountMiddleware` যোগ করো।

```
MIDDLEWARE = [    "django.middleware.security.SecurityMiddleware",    "django.contrib.sessions.middleware.SessionMiddleware",    "django.middleware.common.CommonMiddleware",    "django.middleware.csrf.CsrfViewMiddleware",    "django.contrib.auth.middleware.AuthenticationMiddleware",    "django.contrib.messages.middleware.MessageMiddleware",    "django.middleware.clickjacking.XFrameOptionsMiddleware",    "allauth.account.middleware.AccountMiddleware",]
```

Theory: Middleware হলো request ও response processing-এর একটি layer। `allauth`-এর account functionality সঠিকভাবে চালানোর জন্য তার middleware প্রয়োজন।

Django-এর default middleware-এর order অকারণে পরিবর্তন করবে না।

## Part 5 — Custom User Model ও Site settings

`settings.py`-তে নিশ্চিত করো:

```
AUTH_USER_MODEL = "accounts.User"SITE_ID = 1
```

এগুলো কেন?

- `AUTH_USER_MODEL`: আমাদের custom User Model ব্যবহার করবে।
- `SITE_ID`: Django Sites framework-এর default site record নির্দেশ করে।

যদি database-এ Site record না থাকে, migrations শেষ হওয়ার পর Django shell দিয়ে তৈরি বা update করতে পারবে। তবে সাধারণত `migrate` চালালে default site record তৈরি হয় না; `SITE_ID = 1` ধরে নেওয়ার আগে record যাচাই করবে।

## Part 6 — DRF authentication ও permission settings

এখন `settings.py`-তে যোগ করো:

```
REST_FRAMEWORK = {    "DEFAULT_AUTHENTICATION_CLASSES": [        "rest_framework_simplejwt.authentication.JWTAuthentication",        "rest_framework.authentication.SessionAuthentication",    ],    "DEFAULT_PERMISSION_CLASSES": [        "rest_framework.permissions.IsAuthenticated",    ],}
```

### প্রতিটি setting-এর কাজ

`JWTAuthentication`

Request-এর `Authorization` header থেকে Bearer token নিয়ে user authenticate করে।

```
Authorization: Bearer <access_token>
```

`SessionAuthentication`

Django session ব্যবহার করে browser-ভিত্তিক authenticated request সমর্থন করে।

`IsAuthenticated`

Default permission হিসেবে দিলে API endpoint-গুলো সাধারণত authenticated user ছাড়া access করা যাবে না।

এটি একটি গুরুত্বপূর্ণ security decision। Registration, login ও Forgot Password-এর মতো public endpoint-এ আলাদাভাবে `AllowAny` permission দিতে হবে, নইলে unauthenticated user সেগুলো ব্যবহার করতে পারবে না। Package-এর built-in views তাদের নিজস্ব permission settings ব্যবহার করতে পারে; custom views-এ আমরা সচেতনভাবে permission সেট করব।

## Part 7 — `dj-rest-auth` ও JWT settings

`settings.py`-তে যোগ করো:

```
REST_AUTH = {    "USE_JWT": True,}
```

এটি `dj-rest-auth`-কে JWT authentication ব্যবহার করতে বলে।

এখন SimpleJWT-এর token lifetime configure করতে পারো:

```
from datetime import timedeltaSIMPLE_JWT = {    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=10),    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),    "ROTATE_REFRESH_TOKENS": True,    "BLACKLIST_AFTER_ROTATION": True,}
```

এখানে:

- Access token: ১০ মিনিট।
- Refresh token: ১ দিন।
- Refresh rotation: refresh করলে নতুন refresh token তৈরি হবে।
- Blacklist: পুরোনো refresh token invalid করার ব্যবস্থা।

গুরুত্বপূর্ণ: `BLACKLIST_AFTER_ROTATION=True` ব্যবহার করলে `rest_framework_simplejwt.token_blacklist`-কেও `INSTALLED_APPS`-এ যোগ করতে হবে, তারপর migration চালাতে হবে।

```
INSTALLED_APPS += [    "rest_framework_simplejwt.token_blacklist",]
```

তারপর:

```
python manage.py migrate
```

Production-এ token storage, refresh-cookie settings, CSRF এবং HTTPS configuration-ও ঠিক করতে হবে। শুধু `USE_JWT=True` দিলেই secure cookie-based architecture তৈরি হয়ে যায় না।

## Part 8 — `django-allauth` account settings

আমাদের Custom User Model-এ `username` নেই। তাই account settings-এ email login ও signup fields স্পষ্ট করে দেব।

`settings.py`-তে যোগ করো:

```
ACCOUNT_LOGIN_METHODS = {"email"}ACCOUNT_SIGNUP_FIELDS = [    "email*",    "password1*",    "password2*",]ACCOUNT_EMAIL_VERIFICATION = "none"
```

এখানে:

- `ACCOUNT_LOGIN_METHODS`: login-এর identifier হিসেবে email ব্যবহার করবে।
- `ACCOUNT_SIGNUP_FIELDS`: registration-এ email, password ও confirmation চাইবে।
- `ACCOUNT_EMAIL_VERIFICATION = "none"`: এই প্রাথমিক setup-এ registration-এর সময় allauth email verification বাধ্যতামূলক নয়।

আমরা এখন registration-এর email verification তৈরি করছি না; পরবর্তী ধাপে password-reset OTP তৈরি করব। Production-এ registration-এর জন্য email verification বাধ্যতামূলক করতে চাইলে আলাদা configuration ও email flow implement করতে হবে।

নতুন version-এর `django-allauth`-এ এই settings ব্যবহার করা হয়। যদি installed version পুরোনো হয়, setting names ভিন্ন হতে পারে—তাই version check করে সেই version-এর documentation অনুসরণ করবে।

## Part 9 — API URL configure করো

### Step 1: `config/urls.py` খোলো

এখন নিচের code ব্যবহার করো:

```
from django.contrib import adminfrom django.urls import include, pathurlpatterns = [    path("admin/", admin.site.urls),    path("api/auth/", include("dj_rest_auth.urls")),    path(        "api/auth/registration/",        include("dj_rest_auth.registration.urls"),    ),]
```

### Step 2: কোন URL কী করবে?

| Endpoint                                 | কাজ                                      |
| ---------------------------------------- | ---------------------------------------- |
| `POST /api/auth/login/`                  | Login                                    |
| `POST /api/auth/logout/`                 | Logout                                   |
| `POST /api/auth/password/change/`        | Authenticated user-এর password change    |
| `POST /api/auth/password/reset/`         | Built-in password reset email request    |
| `POST /api/auth/password/reset/confirm/` | Built-in reset token দিয়ে password reset |
| `POST /api/auth/registration/`           | Registration                             |

এই endpoints `dj-rest-auth` package থেকে আসে। তোমার installed version ও configuration অনুযায়ী কিছু behavior আলাদা হতে পারে।

খুব গুরুত্বপূর্ণ: Built-in `/api/auth/password/reset/` সাধারণত reset link/token-ভিত্তিক email পাঠায়, আমাদের custom OTP flow নয়। ভবিষ্যতে custom OTP endpoints-এর জন্য আমরা আলাদা routes ব্যবহার করব, যেমন:

- `/api/auth/otp/forgot/`
- `/api/auth/otp/verify/`
- `/api/auth/otp/reset/`

এতে built-in password-reset routes-এর সঙ্গে সংঘর্ষ হবে না।

## Part 10 — Migration ও configuration verify করো

এখন terminal-এ এক এক করে চালাও:

```
python manage.py check
python manage.py makemigrations
python manage.py migrate
```

যদি `No changes detected` দেখায়, সেটি স্বাভাবিক হতে পারে—যদি model-এর জন্য নতুন migration না লাগে।

এরপর:

```
python manage.py createsuperuser
```

একটি email ও strong password দিয়ে superuser তৈরি করো।

তারপর:

```
python manage.py runserver
```

Server চালু হলে অন্য terminal থেকে API test করতে পারবে।

## Part 11 — API নিজে test করো

আমরা Postman বা `curl` ব্যবহার করতে পারি। এখানে `curl` দিয়ে দেখাচ্ছি।

### Test A: Registration

নতুন email দিয়ে request পাঠাও:

```
curl -X POST http://127.0.0.1:8000/api/auth/registration/ \
  -H "Content-Type: application/json" \
  -d '{
    "email": "learner@example.com",
    "password1": "Strong-Password-2026!",
    "password2": "Strong-Password-2026!"
  }'
```

Registration সফল হলে response-এ user বা authentication-related তথ্য আসতে পারে। Exact response package version ও settings-এর ওপর নির্ভর করে।

### Test B: Login

আগে তৈরি করা user-এর email ও password ব্যবহার করো:

```
curl -X POST http://127.0.0.1:8000/api/auth/login/ \
  -H "Content-Type: application/json" \
  -d '{
    "email": "learner@example.com",
    "password": "Strong-Password-2026!"
  }'
```

JWT configuration ঠিক থাকলে response-এ access token এবং refresh token-সংক্রান্ত তথ্য পাওয়া উচিত।

Security note: বাস্তব password বা token terminal history, screenshots কিংবা public GitHub repository-তে প্রকাশ করবে না। এগুলো শুধু local testing-এর dummy credentials।

### Test C: Authenticated endpoint

আমাদের custom User Model যাচাই করার জন্য Django admin ব্যবহার করতে পারো। পরের ধাপে একটি protected DRF endpoint তৈরি করে `Authorization: Bearer <access_token>` দিয়ে authenticated request test করব।

## Part 12 — Common errors

| Error                          | কী পরীক্ষা করবে                                             |
| ------------------------------ | ----------------------------------------------------------- |
| `ModuleNotFoundError: allauth` | Package install হয়েছে কি না এবং `.venv` active কি না        |
| `AccountMiddleware` error      | `MIDDLEWARE`-তে allauth middleware যোগ করা হয়েছে কি না      |
| `AUTH_USER_MODEL` error        | `accounts.User` model ও migrations সঠিক কি না               |
| Registration-এ username error  | Installed allauth/dj-rest-auth versions এবং signup settings |
| JWT token response নেই         | `REST_AUTH["USE_JWT"]` ও SimpleJWT configuration            |
| `NoReverseMatch`               | `config/urls.py`-তে URL include সঠিক কি না                  |
| Token blacklist table missing  | `token_blacklist` app ও migrations পরীক্ষা করো              |

যদি package version-এর কারণে error হয়, error message-এর পুরো অংশ সংরক্ষণ করবে। আন্দাজ করে settings পরিবর্তন করার বদলে নির্দিষ্ট error ধরে debug করবে।

## Part 13 — Lesson 4 assignment

## Assignment tracker

0/6

Packages ও versions

সব authentication package-এর installed version যাচাই করো।

Settings configuration

INSTALLED_APPS, middleware, AUTH_USER_MODEL, REST_FRAMEWORK ও REST_AUTH configure করো।

URL routing

dj-rest-auth এবং registration URLs যুক্ত করো।

Migrations

manage.py check ও migrate চালাও।

API testing

Registration ও login endpoint test করো এবং response বুঝে নাও।

Debugging notes

নিজে পাওয়া অন্তত একটি error অথবা successful response-এর ব্যাখ্যা লিখো।

Assignment review করো

## Self-test

১. \`REST_AUTH = {'USE_JWT': True}\` কী করে?

HTML email পাঠায়

dj-rest-auth-এ JWT authentication enable করে

OTP তৈরি করে

২. Built-in password reset সাধারণত কী ব্যবহার করে?

Email reset link/token

অবশ্যই ৬ digit OTP

শুধু database password

৩. Protected endpoint-এর default permission \`IsAuthenticated\` হলে কী হয়?

সবাই access করতে পারে

Authenticated user ছাড়া access সীমাবদ্ধ হয়

Email verification নিজে থেকে হয়

## Next Lesson — Lesson 5: Email Backend & SMTP

পরবর্তী ক্লাসে আমরা শিখব:

1. Django email backend কীভাবে কাজ করে।
2. Console backend দিয়ে email test করা।
3. SMTP configuration ও environment variables।
4. Gmail বা অন্য provider দিয়ে বাস্তব inbox-এ email পাঠানো।
5. Email delivery failure ও troubleshooting।
6. Email service-কে এমনভাবে তৈরি করা, যাতে পরের Lesson-এ professional HTML OTP email যুক্ত করতে পারি।

নিজে implement করার নিয়ম: Lesson 4-এর code না দেখে আবার একটি নতুন practice project-এ configuration করার চেষ্টা করবে। কোথায় আটকে যাও, সেই error-সহ জানালে আমরা code review করে ঠিক করব।

----
# Lesson 5: Django Email Backend & SMTP — Beginner to Production

এই লেসনে আমরা Django থেকে email পাঠানো শিখব, যাতে পরের লেসনগুলোতে Forgot Password → OTP Generate → Email-এ OTP Send → OTP Verify → New Password Set পুরো workflow তৈরি করতে পারো।

এখানে শুধু code copy করাই লক্ষ্য নয়। প্রতিটি ধাপে বুঝবে কেন code লিখছি, কীভাবে কাজ করছে, কীভাবে test করব এবং নিজে আবার implement করব।

## আজকের learning goals

Django Email Backend কী এবং কেন দরকার

Console backend দিয়ে email testing

SMTP ও Gmail App Password configuration

.env ফাইলে email credentials নিরাপদে রাখা

Reusable email service তৈরি করা

Email সফলভাবে পাঠানো হয়েছে কি না পরীক্ষা করা

## 1. Email Backend কী?

Django-তে email পাঠানোর জন্য `django.core.mail` ব্যবহার করা হয়। কিন্তু Django-কে জানতে হয়, email কোথা দিয়ে পাঠাবে। এই ব্যবস্থাটিই Email Backend।

Django application

Forgot password view / Email service

Django Email Backend

Console অথবা SMTP

Console

Terminal-এ email দেখায়

SMTP

বাস্তবে email পাঠায়

উদাহরণ: user password ভুলে গেলে Django OTP তৈরি করবে। তারপর email service সেই OTP-সহ message তৈরি করবে। Backend সেটি terminal-এ দেখাতে পারে অথবা SMTP server-এর মাধ্যমে user-এর inbox-এ পাঠাতে পারে।

## 2. Project structure

আগের লেসনের `otp_auth_project` project-এই কাজ করব।

```
otp_auth_project/
├── .env
├── .gitignore
├── manage.py
├── requirements.txt
├── config/
│   ├── settings.py
│   └── urls.py
└── accounts/
    ├── services/
    │   ├── __init__.py
    │   └── email_service.py
    └── ...
```

প্রথমে Ubuntu terminal-এ project directory-তে যাও:

```
cd otp_auth_project
source .venv/bin/activate
```

নিশ্চিত হও virtual environment active আছে:

```
python --version
python -m pip show Django
```

এখন আমরা প্রথমে Console Backend দিয়ে শুরু করব। সরাসরি real SMTP দিয়ে শুরু না করার কারণ হলো, এতে email configuration-এর ভুল আর email delivery-এর ভুল আলাদাভাবে বোঝা সহজ হয়।

## 3. প্রথম ধাপ — Console Email Backend

ফাইল: `config/settings.py`

ফাইলের নিচের দিকে এই configuration যোগ করো:

```
# Email configuration for local developmentEMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "OTP Auth <noreply@example.com>"
```

### প্রতিটি setting-এর কাজ

- `EMAIL_BACKEND`: Django-কে বলে কোন backend দিয়ে email handle করবে।
- `console.EmailBackend`: email পাঠানোর পরিবর্তে terminal-এ message দেখায়।
- `DEFAULT_FROM_EMAIL`: email-এর sender হিসেবে কোন address দেখাবে।

মনে রাখবে: Console backend ব্যবহার করলে বাস্তবে কোনো email inbox-এ যাবে না। এটি development ও debugging-এর জন্য।

### এখন email পাঠিয়ে পরীক্ষা করো

Terminal-এ চালাও:

```
python manage.py shell
```

Shell-এর মধ্যে নিচের code লিখো:

```
from django.core.mail import send_mailresult = send_mail(    subject="Test Email from Django",    message="Hello! Django email is working.",    from_email=None,    recipient_list=["your-test-email@example.com"],    fail_silently=False,)print("Result:", result)
```

`your-test-email@example.com`-এর জায়গায় নিজের test email address লিখতে পারো।

Console backend-এ email-এর subject, body ও recipient terminal-এ দেখা যাবে। সাধারণত `Result: 1` মানে একটি message backend-এর কাছে সফলভাবে handle হয়েছে—এটি বাস্তব inbox-এ পৌঁছানোর প্রমাণ নয়।

Shell থেকে বের হতে:

```
exit()
```

## 4. দ্বিতীয় ধাপ — SMTP কীভাবে কাজ করে?

SMTP-এর পূর্ণরূপ Simple Mail Transfer Protocol। এটি email server-এর মাধ্যমে message পাঠানোর একটি standard protocol।

Django application

SMTP server

Authentication + secure connection

Recipient's email service

Inbox অথবা spam folder

SMTP ব্যবহার করলে Django email server-এ message পাঠায়। Server সেটি গ্রহণ করলেও recipient-এর inbox-এ পৌঁছাবে—এমন নিশ্চয়তা নেই; delivery, spam filtering ও provider policies-ও গুরুত্বপূর্ণ।

## 5. Third step — SMTP credentials নিরাপদে রাখা

আমরা Gmail SMTP-এর উদাহরণ ব্যবহার করব। Gmail-এর জন্য সাধারণত Google Account-এ 2-Step Verification চালু করে একটি App Password তৈরি করতে হয়। নিজের সাধারণ Gmail password Django configuration-এ ব্যবহার করবে না।

Gmail-এর বর্তমান নির্দেশনা: [Google App Passwords documentation](https://support.google.com/accounts/answer/185833?utm_source=chatgpt.com)।

প্রথমে package install করো:

```
python -m pip install python-dotenv
python -m pip freeze > requirements.txt
```

`python-dotenv` `.env` ফাইল থেকে environment variables পড়তে সাহায্য করবে।

### Step A: `.env` ফাইল তৈরি

Project root-এ—যেখানে `manage.py` আছে—`.env` ফাইল তৈরি করো:

```
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
DEFAULT_FROM_EMAIL=OTP Auth <your-email@gmail.com>
```

এখানে placeholder-এর জায়গায় নিজের credentials বসাবে। আসল password বা App Password কোনো chat, screenshot, public repository বা source code-এ প্রকাশ করবে না।

### Step B: `.gitignore` পরীক্ষা করো

Project root-এর `.gitignore` ফাইলে নিচের entry আছে কি না দেখো:

```
.env
.venv/
__pycache__/
*.py[cod]
db.sqlite3
```

এতে `.env` ও local database Git-এ track হওয়া থেকে সাধারণত বাদ থাকবে। আগে থেকেই কোনো secret commit হয়ে গেলে শুধু `.gitignore` যোগ করাই যথেষ্ট নয়—secret rotate করতে হবে এবং Git history-ও বিবেচনা করতে হবে।

### Step C: `config/settings.py` update করো

ফাইলের শুরুতে প্রয়োজনীয় import যোগ করো। `BASE_DIR` আগে থেকেই থাকলে সেটি আবার তৈরি করার প্রয়োজন নেই।

```
import osfrom dotenv import load_dotenv
```

`BASE_DIR` definition-এর পরে যোগ করো:

```
load_dotenv(BASE_DIR / ".env")
```

এবার আগের Console Backend configuration-টি replace করো:

```
# Email configurationEMAIL_BACKEND = (    "django.core.mail.backends.smtp.EmailBackend")EMAIL_HOST = os.getenv(    "EMAIL_HOST",    "smtp.gmail.com",)EMAIL_PORT = int(    os.getenv("EMAIL_PORT", "587"))EMAIL_USE_TLS = (    os.getenv("EMAIL_USE_TLS", "True").lower()    == "true")EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER", "")EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD", "")DEFAULT_FROM_EMAIL = os.getenv(    "DEFAULT_FROM_EMAIL",    EMAIL_HOST_USER,)EMAIL_TIMEOUT = 10
```

### কেন এভাবে লিখলাম?

| Setting               | কাজ                               |
| --------------------- | --------------------------------- |
| `EMAIL_HOST`          | SMTP server-এর address            |
| `EMAIL_PORT`          | SMTP connection port              |
| `EMAIL_USE_TLS`       | Connection-এ TLS security ব্যবহার |
| `EMAIL_HOST_USER`     | SMTP account                      |
| `EMAIL_HOST_PASSWORD` | SMTP authentication secret        |
| `DEFAULT_FROM_EMAIL`  | Message-এর sender address         |
| `EMAIL_TIMEOUT`       | Connection-এর জন্য অপেক্ষার সীমা  |

Port `587` সাধারণত STARTTLS ব্যবহার করে। `EMAIL_USE_TLS=True` হলে `EMAIL_USE_SSL=True` একসঙ্গে enable করবে না; SSL-এর জন্য আলাদা configuration লাগে।

এখন Django configuration যাচাই করো:

```
python manage.py check
```

গুরুত্বপূর্ণ: production-এ `.env` ফাইলের বদলে hosting platform বা deployment environment-এর secret manager থেকেও variables দেওয়া যায়। `.env` থাকলেই secrets স্বয়ংক্রিয়ভাবে নিরাপদ হয়ে যায় না—ফাইলের permissions-ও ঠিক রাখতে হবে।

## 6. চতুর্থ ধাপ — Reusable Email Service তৈরি

এবার email পাঠানোর logic আলাদা service file-এ রাখব। এতে ভবিষ্যতে Forgot Password view, OTP resend view কিংবা অন্য কোনো feature থেকে একই service ব্যবহার করা যাবে।

ফাইল তৈরি করো: `accounts/services/email_service.py`

```
from django.conf import settingsfrom django.core.mail import send_maildef send_plain_email(    subject: str,    message: str,    recipient_email: str,) -> bool:    """    Send a plain-text email to one recipient.    """    sent_count = send_mail(        subject=subject,        message=message,        from_email=settings.DEFAULT_FROM_EMAIL,        recipient_list=[recipient_email],        fail_silently=False,    )    return sent_count == 1
```

### Code বুঝে নাও

1. `settings` থেকে sender email নেওয়া হয়েছে; credentials সরাসরি service-এ hardcode করা হয়নি।
2. `send_mail()` message পাঠানোর দায়িত্ব পালন করে।
3. `recipient_list` একটি list, তাই এখানে একজন recipient থাকলেও list ব্যবহার করেছি।
4. `fail_silently=False` রাখায় email পাঠানোর সময় Django error পেলে সেটি গোপন করবে না।
5. `sent_count == 1` হলে function `True` return করে।

এই function email backend-এর result যাচাই করে; recipient-এর inbox-এ email পৌঁছেছে কি না তা নিশ্চিত করে না।

## 7. পঞ্চম ধাপ — SMTP দিয়ে বাস্তব email test

প্রথমে `.env`-এ নিজের valid credentials বসিয়েছ কি না নিশ্চিত হও। তারপর:

```
python manage.py shell
```

Shell-এ চালাও:

```
from accounts.services.email_service import send_plain_emailresult = send_plain_email(    subject="Django SMTP Test",    message="This is a test email from my Django project.",    recipient_email="your-test-email@example.com",)print(result)
```

নিজের test recipient address ব্যবহার করবে। SMTP server message গ্রহণ করলে সাধারণত `True` পাওয়া যাবে। এরপর inbox ও spam folder—দুটিই পরীক্ষা করো।

পরীক্ষা শেষে:

```
exit()
```

### SMTP error হলে কী করবে?

| Error                                    | সম্ভাব্য কারণ                                                   | কী পরীক্ষা করবে                                   |
| ---------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------- |
| `SMTPAuthenticationError`                | Credentials ভুল অথবা provider authentication প্রত্যাখ্যান করেছে | Username, App Password, account security settings |
| `SMTPConnectError`                       | Server connection ব্যর্থ                                        | Host, port, network, firewall                     |
| `TimeoutError`                           | SMTP server-এ পৌঁছাতে পারছে না                                  | Network, hosting-এর outbound SMTP restrictions    |
| `SMTPRecipientsRefused`                  | Recipient address প্রত্যাখ্যাত                                  | Recipient address ও server response               |
| `ModuleNotFoundError: dotenv`            | Package install হয়নি বা অন্য environment active                 | Virtualenv active করে package install             |
| `ImproperlyConfigured` বা settings error | Configuration ভুল                                               | Import, `.env` path, settings value               |

SMTP server-এর response ও provider অনুযায়ী error আলাদা হতে পারে। Production server-এ outbound SMTP port বন্ধ থাকলে configuration ঠিক থাকলেও connection হবে না।

## 8. Console ও SMTP — কোনটি কখন ব্যবহার করবে?

| বিষয়                | Console Backend | SMTP Backend                |
| ------------------- | --------------- | --------------------------- |
| Local development   | খুব ভালো        | সম্ভব                       |
| Inbox-এ email       | না              | সম্ভব                       |
| Credentials দরকার   | না              | সাধারণত হ্যাঁ               |
| Email design debug  | হ্যাঁ           | হ্যাঁ                       |
| Production delivery | না              | সম্ভব, তবে monitoring দরকার |

আমাদের project-এ development-এর সময় Console Backend সুবিধাজনক। SMTP credentials ও delivery flow যাচাই করার পর local SMTP configuration অথবা production email provider ব্যবহার করতে পারবে।

## 9. আজকের Assignment

## Lesson 5 checklist

0 / 7

Virtual environment activate করে requirements install/check করেছি

Console Backend দিয়ে একটি test email পাঠিয়েছি

SMTP settings \`.env\` থেকে load করেছি

\`.gitignore\`-এ \`.env\` রেখেছি

\`accounts/services/email_service.py\` তৈরি করেছি

SMTP দিয়ে test email পাঠিয়ে ফলাফল যাচাই করেছি

ভুল credentials দিয়ে পাওয়া error বুঝে দেখেছি

## 10. নিজের জ্ঞান যাচাই করো

1\. Console Backend কী করে?

Email inbox-এ পাঠায়

Terminal-এ email output দেখায়

OTP database-এ save করে

2\. SMTP password কোথায় রাখা উচিত?

GitHub-এ

Python source code-এ

Environment variable বা secret manager-এ

3\. \`fail_silently=False\` কেন ব্যবহার করি?

Error গোপন না রাখতে

Email HTML করতে

OTP expire করতে

4\. \`send_mail()\`-এর success result কী নিশ্চিত করে?

Email inbox-এ পৌঁছেছে

Backend একটি message handle করেছে

User password পরিবর্তন করেছে

Quiz আবার শুরু করো

## পরের লেসন — Lesson 6

Professional HTML Email Template Design

সেখানে আমরা তৈরি করব:

- Brand header ও সুন্দর OTP card
- HTML email-এর পাশাপাশি plain-text fallback
- OTP, expiry time ও security notice
- Django template দিয়ে dynamic email rendering
- `EmailMultiAlternatives` দিয়ে HTML email পাঠানো

তারপর Lesson 7-এ OTP generation শুরু করব। Production-এ OTP যেন email বা application log-এ অপ্রয়োজনে প্রকাশ না পায়, সেই নিরাপত্তাও অনুসরণ করব।

---
# Lesson 6: Professional HTML Email Template Design with Django

এই লেসনে আমরা আগের Lesson 5-এর email service-কে আরও professional করব। এবার সাধারণ text email নয়, বরং এমন একটি branded HTML email তৈরি করব, যেখানে থাকবে logo/brand name, OTP card, expiry time, security notice এবং plain-text fallback।

আমাদের final goal হলো—Forgot Password request এলে Django একটি সুন্দর, responsive email template render করবে এবং SMTP-এর মাধ্যমে সেটি user-এর email address-এ পাঠাবে।

## 1. আজকের email design

# OTP Auth

Secure account recovery

## Reset your password

Hello there,

Someone requested a password reset for your account. Use the verification code below to continue.

YOUR VERIFICATION CODE

# 482 731

This code expires in 5 minutes.

If you did not request a password reset, you can ignore this email. Never share your verification code with anyone.

OTP Auth · Automated security notification

এটি design preview। দেখানো OTP কেবল উদাহরণ—এটি বাস্তব বা ব্যবহারযোগ্য verification code নয়।

আজ আমরা এই design-কে Django template এবং reusable email service দিয়ে implement করব।

## 2. Email template-এর folder structure

আগের project-এ এই structure তৈরি করো:

```
otp_auth_project/
├── config/
│   └── settings.py
├── accounts/
│   ├── services/
│   │   ├── __init__.py
│   │   └── email_service.py
│   └── templates/
│       └── emails/
│           ├── password_reset_otp.html
│           └── password_reset_otp.txt
└── manage.py
```

Project root থেকে folder তৈরি করার command:

```
mkdir -p accounts/templates/emails
```

এখানে দুটি template রাখছি:

- `password_reset_otp.html` — সুন্দর HTML email-এর জন্য।
- `password_reset_otp.txt` — HTML render না হলে বা plain-text email client-এর জন্য বিকল্প message।

Django-তে template ব্যবহার করলে HTML-এর layout আর Python-এর email logic আলাদা রাখা যায়। ফলে design পরিবর্তন করতে service code বদলানোর প্রয়োজন হয় না।

## 3. HTML email template তৈরি করো

ফাইল: `accounts/templates/emails/password_reset_otp.html`

Email clients—বিশেষ করে Gmail ও Outlook—সব CSS feature একইভাবে support করে না। তাই email layout-এর জন্য table-based HTML, inline CSS এবং simple design ব্যবহার করব।

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Password Reset</title>
</head>

<body style="
    margin: 0;
    padding: 0;
    background-color: #f3f5f9;
    font-family: Arial, Helvetica, sans-serif;
    color: #243047;
">
    <table
        role="presentation"
        width="100%"
        cellpadding="0"
        cellspacing="0"
        border="0"
        style="background-color: #f3f5f9; padding: 24px 10px;"
    >
        <tr>
            <td align="center">

                <table
                    role="presentation"
                    width="100%"
                    cellpadding="0"
                    cellspacing="0"
                    border="0"
                    style="
                        max-width: 560px;
                        background-color: #ffffff;
                        border-radius: 12px;
                        overflow: hidden;
                    "
                >
                    <!-- Brand header -->
                    <tr>
                        <td
                            align="center"
                            style="
                                background-color: #152b4a;
                                padding: 28px 20px;
                                color: #ffffff;
                            "
                        >
                            <h1 style="margin: 0; font-size: 25px;">
                                OTP Auth
                            </h1>

                            <p style="
                                margin: 8px 0 0;
                                font-size: 13px;
                                color: #dce8f8;
                            ">
                                Secure account recovery
                            </p>
                        </td>
                    </tr>

                    <!-- Main content -->
                    <tr>
                        <td style="padding: 30px 24px;">

                            <h2 style="
                                margin: 0 0 16px;
                                font-size: 22px;
                                color: #152b4a;
                            ">
                                Reset your password
                            </h2>

                            <p style="
                                margin: 0 0 16px;
                                font-size: 15px;
                                line-height: 1.7;
                            ">
                                Hello,
                            </p>

                            <p style="
                                margin: 0 0 24px;
                                font-size: 15px;
                                line-height: 1.7;
                            ">
                                We received a request to reset your password.
                                Use the verification code below to continue.
                            </p>

                            <!-- OTP card -->
                            <table
                                role="presentation"
                                width="100%"
                                cellpadding="0"
                                cellspacing="0"
                                border="0"
                                style="
                                    background-color: #f1f5ff;
                                    border: 1px solid #dbe5ff;
                                    border-radius: 10px;
                                "
                            >
                                <tr>
                                    <td align="center" style="padding: 24px 12px;">

                                        <p style="
                                            margin: 0 0 12px;
                                            font-size: 12px;
                                            font-weight: bold;
                                            letter-spacing: 1px;
                                            color: #52627a;
                                        ">
                                            YOUR VERIFICATION CODE
                                        </p>

                                        <p style="
                                            margin: 0;
                                            font-size: 32px;
                                            font-weight: bold;
                                            letter-spacing: 7px;
                                            color: #2858bb;
                                        ">
                                            {{ otp }}
                                        </p>

                                        <p style="
                                            margin: 16px 0 0;
                                            font-size: 13px;
                                            color: #52627a;
                                        ">
                                            Expires in {{ expiry_minutes }} minutes.
                                        </p>

                                    </td>
                                </tr>
                            </table>

                            <!-- Security notice -->
                            <p style="
                                margin: 24px 0 0;
                                font-size: 14px;
                                line-height: 1.7;
                            ">
                                <strong>Security notice:</strong>
                                Never share this code with anyone.
                                Our team will never ask you to disclose it.
                            </p>

                            <p style="
                                margin: 16px 0 0;
                                font-size: 14px;
                                line-height: 1.7;
                            ">
                                If you did not request a password reset,
                                you can ignore this email.
                            </p>

                        </td>
                    </tr>

                    <!-- Footer -->
                    <tr>
                        <td
                            align="center"
                            style="
                                padding: 20px;
                                background-color: #f8fafc;
                                border-top: 1px solid #e7ebf2;
                            "
                        >
                            <p style="
                                margin: 0;
                                font-size: 12px;
                                line-height: 1.7;
                                color: #667085;
                            ">
                                OTP Auth · Automated security notification
                            </p>
                        </td>
                    </tr>

                </table>

            </td>
        </tr>
    </table>
</body>
</html>
```

### গুরুত্বপূর্ণ বিষয়গুলো

- `{{ otp }}` এবং `{{ expiry_minutes }}` হলো Django template variables। Email পাঠানোর সময় Python থেকে এগুলোর value দেওয়া হবে।
- `role="presentation"` email layout-এর table-কে screen reader-এর কাছে decorative layout হিসেবে চিহ্নিত করতে সাহায্য করে।
- Inline CSS ব্যবহার করায় email client-এ styling ঠিক থাকার সম্ভাবনা বাড়ে।
- কোনো external JavaScript বা CSS file ব্যবহার করিনি, কারণ email clients এগুলো সীমিত বা block করতে পারে।

এখনও OTP generate করা হয়নি। পরবর্তী লেসনে আমরা নিরাপদভাবে OTP তৈরি করব; আপাতত testing-এর জন্য sample value ব্যবহার করব।

## 4. Plain-text email template

ফাইল: `accounts/templates/emails/password_reset_otp.txt`

```
OTP Auth — Secure account recovery

Hello,

We received a request to reset your password.

Your verification code is: {{ otp }}

This code expires in {{ expiry_minutes }} minutes.

Never share this code with anyone.

If you did not request a password reset, you can ignore this email.

OTP Auth
Automated security notification
```

কেন দুটি template? `EmailMultiAlternatives` একই email-এর HTML এবং plain-text—দুই version পাঠাতে পারে। Email client HTML না দেখালে plain-text version কাজে লাগে।

## 5. Django template settings যাচাই

ফাইল: `config/settings.py`

`TEMPLATES` configuration-এ `APP_DIRS=True` আছে কি না দেখো। `startproject` দিয়ে তৈরি Django project-এ সাধারণত এটি আগে থেকেই থাকে।

```
TEMPLATES = [    {        "BACKEND": "django.template.backends.django.DjangoTemplates",        "DIRS": [],        "APP_DIRS": True,        "OPTIONS": {            "context_processors": [                "django.template.context_processors.request",                "django.contrib.auth.context_processors.auth",                "django.contrib.messages.context_processors.messages",            ],        },    },]
```

`APP_DIRS=True` থাকার ফলে Django installed apps-এর `templates/` directory-তে template খুঁজতে পারে। আগের Lesson 4 অনুযায়ী `accounts` অবশ্যই `INSTALLED_APPS`-এ থাকতে হবে।

যদি তোমার project-এ এই configuration ইতিমধ্যে থাকে, আবার যোগ করবে না।

## 6. HTML email পাঠানোর reusable service

এখন Lesson 5-এর `email_service.py`-তে HTML email পাঠানোর function যোগ করব।

ফাইল: `accounts/services/email_service.py`

```
from django.conf import settingsfrom django.core.mail import EmailMultiAlternativesfrom django.template.loader import render_to_stringdef send_password_reset_otp_email(    recipient_email: str,    otp: str,    expiry_minutes: int = 5,) -> bool:    """    Send a password-reset OTP email with HTML and plain-text versions.    """    context = {        "otp": otp,        "expiry_minutes": expiry_minutes,    }    subject = "Your password reset verification code"    # Render both email templates using the same context.    text_content = render_to_string(        "emails/password_reset_otp.txt",        context,    )    html_content = render_to_string(        "emails/password_reset_otp.html",        context,    )    # Create the email with its plain-text version.    email = EmailMultiAlternatives(        subject=subject,        body=text_content,        from_email=settings.DEFAULT_FROM_EMAIL,        to=[recipient_email],    )    # Attach the HTML alternative.    email.attach_alternative(        html_content,        "text/html",    )    # Send through the configured Django email backend.    sent_count = email.send(fail_silently=False)    return sent_count == 1
```

### Function-এর execution flow

1\. Function call

Recipient email + OTP + expiry

2\. Template rendering

HTML এবং plain-text তৈরি

3\. EmailMultiAlternatives

একই email-এ দুটি format সংযুক্ত

4\. Configured email backend

Console অথবা SMTP

### এখানে `EmailMultiAlternatives` কেন ব্যবহার করলাম?

`send_mail()` সাধারণ text email পাঠানোর জন্য যথেষ্ট। কিন্তু HTML ও plain-text version একসঙ্গে পাঠাতে `EmailMultiAlternatives` সুবিধাজনক।

আরেকটি গুরুত্বপূর্ণ বিষয়: Django template-এর autoescaping সাধারণত চালু থাকে। তাই template-এ variable render করার সময় সাধারণ HTML escaping পাওয়া যায়। তবুও OTP-কে string হিসেবে validate করা এবং user-supplied content সরাসরি HTML হিসেবে render না করা জরুরি।

## 7. প্রথম test — SMTP ছাড়াই HTML email পরীক্ষা

আগে console backend ব্যবহার করে HTML template ও service পরীক্ষা করো। এতে Gmail credentials ছাড়াই template rendering-এর ভুল ধরতে পারবে।

```
python manage.py shell
```

Shell-এর মধ্যে:

```
from django.test.utils import override_settingsfrom accounts.services.email_service import (    send_password_reset_otp_email,)with override_settings(    EMAIL_BACKEND="django.core.mail.backends.console.EmailBackend"):    result = send_password_reset_otp_email(        recipient_email="learner@example.com",        otp="482731",        expiry_minutes=5,    )print("Email handled:", result)
```

এখানে `482731` কেবল testing-এর sample OTP।

সফল হলে terminal-এ email-এর subject, plain-text body এবং HTML alternative দেখতে পাবে। `Email handled: True` মানে configured backend একটি message handle করেছে—বাস্তব email delivery নিশ্চিত হয়েছে, এমন নয়।

Shell থেকে বের হও:

```
exit()
```

## 8. দ্বিতীয় test — বাস্তব SMTP দিয়ে পাঠানো

Lesson 5-এর SMTP settings `.env`-এ সঠিকভাবে configured থাকলে console override ছাড়াই একই function ব্যবহার করতে পারবে।

```
python manage.py shell
```

```
from accounts.services.email_service import (    send_password_reset_otp_email,)result = send_password_reset_otp_email(    recipient_email="your-test-email@example.com",    otp="482731",    expiry_minutes=5,)print("Email accepted by backend:", result)
```

নিজের test email address ব্যবহার করবে। Inbox ও spam folder পরীক্ষা করো।

Security note: Production-এ real OTP application log, terminal output, error-tracking event বা analytics-এ প্রকাশ করবে না। Console backend কেবল development-এর জন্য রাখবে। OTP-এর validity ও single-use enforcement এই লেসনের email function-এর কাজ নয়—সেগুলো OTP model এবং verification service-এ implement করতে হবে।

## 9. Common mistakes ও debugging

| সমস্যা                          | সম্ভাব্য কারণ                                            | সমাধান                                          |
| ------------------------------- | -------------------------------------------------------- | ----------------------------------------------- |
| `TemplateDoesNotExist`          | Template path ভুল                                        | `accounts/templates/emails/` path যাচাই করো     |
| `ModuleNotFoundError`           | ভুল virtualenv বা missing package                        | `.venv` activate করে check করো                  |
| `SMTPAuthenticationError`       | Credentials বা authentication সমস্যা                     | Gmail App Password ও account settings যাচাই করো |
| Email-এ `{{ otp }}` দেখা যাচ্ছে | Template render না করে raw HTML পাঠানো হয়েছে             | `render_to_string()` ব্যবহার করো                |
| Email plain text-এ দেখাচ্ছে     | HTML alternative সংযুক্ত হয়নি বা client HTML বন্ধ রেখেছে | `attach_alternative()` যাচাই করো                |
| Email পাঠাতে দেরি হচ্ছে         | SMTP connection বা network timeout                       | Host, port, network ও timeout পরীক্ষা করো       |

## 10. Lesson 6 assignment

নিজে implement করে প্রতিটি item যাচাই করো।

Assignment progress

0/7

HTML template তৈরি করেছি

Plain-text template তৈরি করেছি

Django template settings যাচাই করেছি

EmailMultiAlternatives দিয়ে service লিখেছি

Console backend দিয়ে template পরীক্ষা করেছি

SMTP দিয়ে test email পাঠিয়েছি

Production-এ OTP log না করার বিষয়টি বুঝেছি

## পরবর্তী লেসন — Lesson 7: Secure OTP Generation

পরের লেসনে আমরা শিখব:

1. Python-এর `secrets` module দিয়ে cryptographically secure OTP তৈরি।
2. OTP-এর length ও expiry policy নির্ধারণ।
3. OTP database-এ plain text না রেখে নিরাপদভাবে সংরক্ষণ করার পদ্ধতি।
4. OTP expiry, single-use validation এবং resend-এর নিয়ম।
5. Django service-এর সঙ্গে OTP generation যুক্ত করা।

এভাবে আমরা সুন্দর email design থেকে এগিয়ে একটি বাস্তব, নিরাপদ Forgot Password OTP system তৈরি করব।

----
# Lesson 7: Secure OTP Generation with Django

এই লেসনে আমরা Python ও Django দিয়ে secure, time-limited, six-digit OTP তৈরি করব। এটি আমাদের Forgot Password system-এর প্রথম security-critical অংশ।

আগের লেসনগুলোতে আমরা email backend, SMTP এবং HTML email template তৈরি করেছি। এবার সেই email-এ পাঠানোর জন্য OTP তৈরি করব।

আজকের লক্ষ্য শুধু ছয়টি সংখ্যা তৈরি করা নয়। আমরা বুঝব:

- Secure OTP ও সাধারণ random number-এর পার্থক্য
- Python-এর `secrets` module ব্যবহার
- OTP-এর মেয়াদ (expiry) নির্ধারণ
- OTP-কে string হিসেবে রাখার কারণ
- OTP-কে plain text হিসেবে database-এ না রাখার security design
- OTP generation service তৈরি ও test করা

## 1. OTP কীভাবে কাজ করবে?

User requests password reset

Email address দিয়ে request

Generate secure OTP

# 6 digits

উদাহরণ: 084271

Store OTP verifier securely

Plain OTP নয়, তার hash

Send OTP by email

আগের Lesson 6-এর email service

Verify → Set new password

পরবর্তী লেসনগুলোতে implement করব

একটি গুরুত্বপূর্ণ বিষয়: ছয় সংখ্যার OTP-এর সম্ভাব্য combination মাত্র ১০ লাখ। তাই শুধু secure generation যথেষ্ট নয়। OTP expiry, attempt limit, resend throttling এবং single-use validation-ও লাগবে।

## 2. কেন `random` নয়, `secrets`?

Python-এ random number তৈরি করার একাধিক উপায় আছে।

```
import randomotp = random.randint(100000, 999999)
```

এটি সাধারণ simulation বা casual randomization-এর জন্য কাজে লাগতে পারে। কিন্তু authentication-এর মতো security-sensitive কাজে `random` ব্যবহার করা উচিত নয়।

এর পরিবর্তে:

```
import secretsotp = f"{secrets.randbelow(1_000_000):06d}"
```

এখানে:

- `secrets.randbelow(1_000_000)` শূন্য থেকে `999999`-এর মধ্যে একটি secure random integer তৈরি করে।
- `:06d` integer-টিকে ছয় digit-এর decimal string হিসেবে format করে।
- শুরুতে শূন্য থাকলেও সেটি বজায় থাকে।

উদাহরণ: `84271`-এর পরিবর্তে `"084271"` পাওয়া যেতে পারে।

কেন `:06d` গুরুত্বপূর্ণ? OTP হলো একটি verification code, গণনার সংখ্যা নয়। তাই `"084271"`-কে integer `84271` বানিয়ে ফেললে প্রথম শূন্যটি হারিয়ে যাবে।

## 3. নিজে OTP generator implement করো

আমাদের project structure:

```
accounts/
└── services/
    ├── __init__.py
    ├── email_service.py
    └── otp_service.py
```

`accounts/services/otp_service.py` ফাইল তৈরি করো।

```
import secretsOTP_LENGTH = 6def generate_otp() -> str:    """    Generate a cryptographically secure six-digit OTP.    Leading zeroes are preserved.    """    return f"{secrets.randbelow(10 ** OTP_LENGTH):0{OTP_LENGTH}d}"
```

### লাইন ধরে বুঝি

`import secrets`

Python-এর standard library থেকে secure random generation-এর functionality নিচ্ছি। আলাদা package install করার প্রয়োজন নেই।

`OTP_LENGTH = 6`

এক জায়গায় OTP length রাখছি। পরে length পরিবর্তন করতে হলে function-এর ভেতরে একাধিক জায়গা edit করতে হবে না।

`10 ** OTP_LENGTH`

যেহেতু `OTP_LENGTH` ছয়, তাই `10 ** 6 = 1,000,000`। `randbelow(1_000_000)`-এর upper bound বাদ পড়ে, অর্থাৎ ফলাফল `0` থেকে `999999` পর্যন্ত হতে পারে।

`-> str`

এটি return type hint। Function যে string ফেরত দেওয়ার জন্য design করা হয়েছে, তা বোঝায়।

### Generator test করো

Terminal-এ:

```
python manage.py shell
```

তারপর:

```
from accounts.services.otp_service import generate_otpotp = generate_otp()print(otp)print(type(otp))print(len(otp))print(otp.isdigit())
```

Expected checks:

- Output ছয়টি digit-এর হবে।
- Type হবে `str`।
- Length হবে `6`।
- `isdigit()` হবে `True`।

প্রতিবার function call করলে সাধারণত আলাদা OTP পাবে। তবে random generation-এ একই OTP আবার আসা গাণিতিকভাবে সম্ভব; তাই uniqueness বা single-use database logic-ও প্রয়োজন।

## 4. OTP-এর expiry time নির্ধারণ

OTP তৈরি হলেই সেটি অনির্দিষ্ট সময় ব্যবহার করা যাবে—এমন হওয়া উচিত নয়।

আমরা প্রাথমিক policy হিসেবে ৫ মিনিটের expiry নেব। বাস্তব ব্যবহারে তোমার threat model ও user experience অনুযায়ী সময় নির্ধারণ করবে।

```
from datetime import timedeltafrom django.utils import timezoneOTP_EXPIRY_MINUTES = 5def get_otp_expiry():    return timezone.now() + timedelta(        minutes=OTP_EXPIRY_MINUTES    )
```

এই function-টি একই `otp_service.py` ফাইলে যোগ করতে পারো।

### কেন `timezone.now()` ব্যবহার করলাম?

Django project-এ timezone-aware datetime ব্যবহার করা উচিত। এতে OTP তৈরির সময়ের সঙ্গে বর্তমান সময় তুলনা করে expiry যাচাই করা সহজ হয়।

ধরো OTP তৈরি হয়েছে দুপুর ১২:০০-তে। Expiry হবে ১২:০৫-এ। Verification-এর সময়:

```
from django.utils import timezoneis_expired = timezone.now() >= expires_at
```

এখানে `expires_at` হবে database থেকে পাওয়া OTP-এর expiry datetime।

সতর্কতা: শুধু frontend-এ countdown দেখানো নিরাপত্তা নয়। Backend-কে প্রতিবার OTP verify করার সময় expiry পরীক্ষা করতে হবে।

## 5. Database-এ OTP plain text রাখা উচিত?

ধরো database-এ এমন record আছে:

| email                | otp      | expires_at |
| -------------------- | -------- | ---------- |
| learner\@example.com | `084271` | 12:05 PM   |

এভাবে OTP সরাসরি সংরক্ষণ করলে database access পেয়ে যাওয়া কেউ active code দেখতে পারে। তাই আমরা OTP-এর বদলে একটি keyed verifier সংরক্ষণ করব।

একটি গুরুত্বপূর্ণ technical detail: OTP মাত্র ছয় digit হওয়ায় শুধু SHA-256 hash করলেই database leak-এর বিরুদ্ধে যথেষ্ট সুরক্ষা পাওয়া যায় না। সম্ভাব্য সব code সহজে পরীক্ষা করা সম্ভব। তাই আমরা server-side secret key দিয়ে HMAC-SHA-256 ব্যবহার করব।

### Step A — OTP pepper configuration

Project root-এর `.env` ফাইলে একটি আলাদা secret যোগ করো:

```
OTP_PEPPER=replace-with-a-long-random-secret
```

এটি একটি placeholder। বাস্তবে cryptographically secure random secret তৈরি করে ব্যবহার করবে। এই secret Git-এ commit করবে না এবং Django `SECRET_KEY`-এর সঙ্গে একই value রাখবে না।

Python shell থেকে secret তৈরি করতে পারো:

```
python -c "import secrets; print(secrets.token_urlsafe(48))"
```

Generated value `.env`-এ রাখো। যদি এটি আগে থেকেই অন্য কোথাও প্রকাশিত হয়ে থাকে, নতুন secret তৈরি করো।

`config/settings.py`-এ:

```
OTP_PEPPER = os.environ["OTP_PEPPER"]
```

এটি তোমার আগের `.env` loading configuration-এর পরে রাখবে। Secret অনুপস্থিত থাকলে application startup-এ error হওয়া ইচ্ছাকৃত—নীরবে insecure fallback ব্যবহার করার চেয়ে এটি নিরাপদ।

### Step B — OTP verifier তৈরি

`accounts/services/otp_service.py` ফাইলটি এখন এভাবে সাজাও:

```
import hashlibimport hmacimport secretsfrom datetime import timedeltafrom django.conf import settingsfrom django.utils import timezoneOTP_LENGTH = 6OTP_EXPIRY_MINUTES = 5def generate_otp() -> str:    """Generate a secure six-digit OTP."""    return f"{secrets.randbelow(10 ** OTP_LENGTH):0{OTP_LENGTH}d}"def get_otp_expiry():    """Return the OTP expiry datetime."""    return timezone.now() + timedelta(        minutes=OTP_EXPIRY_MINUTES    )def get_otp_verifier(otp: str) -> str:    """Create a keyed verifier for a six-digit OTP."""    if (        len(otp) != OTP_LENGTH        or not otp.isascii()        or not otp.isdigit()    ):        raise ValueError("OTP must contain exactly six ASCII digits.")    return hmac.new(        key=settings.OTP_PEPPER.encode("utf-8"),        msg=otp.encode("utf-8"),        digestmod=hashlib.sha256,    ).hexdigest()def verify_otp_value(    submitted_otp: str,    stored_verifier: str,) -> bool:    """Compare a submitted OTP against its stored verifier."""    try:        submitted_verifier = get_otp_verifier(submitted_otp)    except (ValueError, AttributeError):        return False    return hmac.compare_digest(        submitted_verifier,        stored_verifier,    )
```

### কীভাবে কাজ করছে?

1. `get_otp_verifier()` OTP থেকে HMAC তৈরি করে; database-এ এই verifier রাখব, original OTP নয়।
2. `verify_otp_value()` user-এর দেওয়া OTP থেকে আবার verifier তৈরি করে।
3. `hmac.compare_digest()` দুইটি verifier নিরাপদভাবে তুলনা করে।
4. OTP ভুল format-এ হলে function `False` return করে।

এই keyed verifier-ও security-এর সব সমস্যার সমাধান নয়। `OTP_PEPPER` নিরাপদে রাখতে হবে, OTP endpoint-এ rate limit দিতে হবে এবং verification সফল হলে code-কে আর ব্যবহারযোগ্য রাখা যাবে না।

## 6. Generator ও verifier নিজে test করো

Django shell-এ:

```
python manage.py shell
```

তারপর:

```
from accounts.services.otp_service import (    generate_otp,    get_otp_verifier,    verify_otp_value,)otp = generate_otp()verifier = get_otp_verifier(otp)print("OTP:", otp)print("Length:", len(otp))print("Verifier length:", len(verifier))print(    "Correct OTP:",    verify_otp_value(otp, verifier),)print(    "Wrong OTP:",    verify_otp_value("000000", verifier),)
```

`Correct OTP`-এর ফলাফল `True` হওয়া উচিত। `Wrong OTP`-এর ফলাফল সাধারণত `False` হবে—তবে test-এর ভুল code-টি দৈবক্রমে generated OTP-এর সমান হয়ে গেলে সেটি `True` হতে পারে। নির্ভরযোগ্য unit test-এ তাই ভুল OTP নিশ্চিতভাবে আলাদা রাখবে।

একটি নির্দিষ্ট leading-zero test:

```
verifier = get_otp_verifier("084271")print(verify_otp_value("084271", verifier))  # Trueprint(verify_otp_value("84271", verifier))   # False
```

এখানে OTP-কে string হিসেবে রাখার গুরুত্ব আবার বোঝা যাচ্ছে।

## 7. OTP তৈরি করে email service-এ পাঠানো

এখন Lesson 6-এর email service-এর সঙ্গে generator connect করব। এটি শুধু integration test; database-এ OTP record, attempt limit ও single-use verification এখনো implement হয়নি।

Django shell-এ:

```
from accounts.services.otp_service import generate_otpfrom accounts.services.email_service import (    send_password_reset_otp_email,)otp = generate_otp()sent = send_password_reset_otp_email(    recipient_email="your-test-email@example.com",    otp=otp,    expiry_minutes=5,)print("Email handled:", sent)
```

নিজের test email address ব্যবহার করবে। Console backend চালু থাকলে email terminal-এ দেখাবে; SMTP backend চালু থাকলে email provider-এর মাধ্যমে পাঠানোর চেষ্টা করবে।

Production rule: OTP তৈরি, database record তৈরি এবং email পাঠানোর workflow এমনভাবে design করতে হবে যেন resend, simultaneous requests, expired OTP এবং failed email delivery সঠিকভাবে handle হয়। শুধু generator ও email function একসঙ্গে call করলেই সম্পূর্ণ নিরাপদ password-reset workflow তৈরি হয় না।

## 8. Common mistakes

| ভুল                                 | সঠিক পদ্ধতি                                              |
| ----------------------------------- | -------------------------------------------------------- |
| `random.randint()` দিয়ে OTP তৈরি    | `secrets` ব্যবহার                                        |
| OTP-কে integer হিসেবে রাখা          | String হিসেবে রাখা                                       |
| Expiry শুধু frontend-এ check        | Backend-এ প্রতিবার যাচাই                                 |
| OTP database-এ plain text রাখা      | Keyed verifier সংরক্ষণ                                   |
| শুধু hash ব্যবহার করে নিরাপদ ভাবা   | Low-entropy OTP-এর জন্য HMAC ও secret protection বিবেচনা |
| OTP বারবার verify করতে দেওয়া        | সফল verification-এর পর একবারই ব্যবহারযোগ্য করা           |
| অনেকবার ভুল OTP দেওয়া সম্ভব         | Server-side attempt limit ও rate limiting                |
| Resend করলে আগের OTP-ও কার্যকর থাকা | নতুন code তৈরি করলে আগের code invalidate করা             |

## 9. Lesson 7 assignment

Assignment checklist

0/7

secrets module দিয়ে ছয় digit OTP তৈরি করেছি

Leading zero-সহ OTP string হিসেবে পরীক্ষা করেছি

OTP expiry datetime তৈরি করেছি

OTP_PEPPER environment variable-এ রেখেছি

HMAC verifier তৈরি করেছি

সঠিক ও ভুল OTP যাচাই করেছি

Email service-এর সঙ্গে generator integrate করেছি

## পরবর্তী লেসন — Lesson 8: OTP Model & Database Design

পরবর্তী লেসনে আমরা Django model তৈরি করব, যেখানে থাকবে:

- কোন user-এর জন্য OTP তৈরি হয়েছে
- OTP verifier ও expiry time
- Verification attempts-এর হিসাব
- Used/verified state
- Resend এবং নতুন OTP-এর lifecycle
- Database constraint, indexing এবং concurrent request-এর ঝুঁকি

তারপর Lesson 9–14-এ এই model-এর ওপর Forgot Password, OTP verification ও password reset API তৈরি করব।

---
# Lesson 8: OTP Model & Database Design — Django REST Framework

এই লেসনে আমরা আগের Lesson 7-এর secure OTP generator ও HMAC verifier-এর ওপর ভিত্তি করে Django database model তৈরি করব।

এখন পর্যন্ত আমরা OTP তৈরি করতে এবং তার verifier তৈরি করতে শিখেছি। কিন্তু OTP কোথায় থাকবে, কখন expire হবে, কতবার ভুল দেওয়া হয়েছে, resend করলে আগের OTP-এর কী হবে—এসব database ও application logic দিয়ে নিয়ন্ত্রণ করতে হবে।

আজকের লক্ষ্য: এমন একটি OTP model design করা, যা Forgot Password workflow-এ নিরাপদভাবে ব্যবহার করা যায় এবং ভবিষ্যতে production-এ নেওয়ার উপযোগী হয়।

## 1. Database design: কী কী তথ্য রাখতে হবে?

আমাদের OTP record-এ থাকবে:

- কোন user-এর password reset হচ্ছে
- OTP-এর keyed verifier — আসল OTP নয়
- কখন OTP তৈরি হয়েছে ও expire হবে
- কতবার ভুল OTP দেওয়া হয়েছে
- OTP ব্যবহার হয়ে গেছে কি না
- Record তৈরি ও পরিবর্তনের সময়

User

accounts.User

One user → multiple OTP records over time

## PasswordResetOTP

otp_verifier

HMAC digest; original OTP নয়

expires_at

OTP-এর মেয়াদ শেষ হওয়ার সময়

attempts / is_used

ভুল চেষ্টা ও single-use tracking

created_at / updated_at

Record lifecycle tracking

## 2. কেন আলাদা OTP model?

আমাদের আগের `accounts.User` model user-এর account information রাখে। Password reset OTP হলো সাময়িক security state—এটি User model-এর মধ্যে রাখা উচিত নয়।

আলাদা model রাখলে:

1. একই user-এর OTP lifecycle আলাদাভাবে নিয়ন্ত্রণ করা যায়।
2. OTP expire হলে record পরিষ্কার করা যায়।
3. ভুল attempt-এর হিসাব রাখা যায়।
4. Resend করলে পুরোনো OTP invalidate করা যায়।
5. OTP feature-এর test ও maintenance সহজ হয়।

একটি design decision: আমরা `email` সরাসরি OTP model-এ duplicate করব না; `User` foreign key ব্যবহার করব। এতে OTP record নির্দিষ্ট account-এর সঙ্গে যুক্ত থাকবে।

## 3. Model তৈরি করো

ফাইল: `accounts/models.py`

আগের `User` model মুছে ফেলবে না। সেটির নিচে নতুন model যোগ করো।

```
from django.conf import settingsfrom django.db import modelsclass PasswordResetOTP(models.Model):    user = models.ForeignKey(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="password_reset_otps",    )    otp_verifier = models.CharField(        max_length=64,    )    expires_at = models.DateTimeField()    attempts = models.PositiveSmallIntegerField(        default=0,    )    is_used = models.BooleanField(        default=False,    )    used_at = models.DateTimeField(        null=True,        blank=True,    )    invalidated_at = models.DateTimeField(        null=True,        blank=True,    )    created_at = models.DateTimeField(        auto_now_add=True,    )    updated_at = models.DateTimeField(        auto_now=True,    )    class Meta:        indexes = [            models.Index(                fields=["user", "-created_at"],                name="pwdotp_user_created_idx",            ),            models.Index(                fields=["expires_at"],                name="pwdotp_expires_idx",            ),        ]    def __str__(self):        return (            f"PasswordResetOTP("            f"user_id={self.user_id}, "            f"id={self.pk})"        )
```

### প্রতিটি field-এর কাজ

| Field            | কেন দরকার                                  |
| ---------------- | ------------------------------------------ |
| `user`           | OTP কোন account-এর জন্য তা নির্ধারণ করে    |
| `otp_verifier`   | HMAC-SHA-256 verifier সংরক্ষণ করে          |
| `expires_at`     | OTP-এর expiry time                         |
| `attempts`       | ভুল verification attempt গণনা              |
| `is_used`        | OTP সফলভাবে ব্যবহার হয়েছে কি না            |
| `used_at`        | কখন OTP ব্যবহার হয়েছে                      |
| `invalidated_at` | OTP মেয়াদ শেষ হওয়ার আগেই বাতিল হয়েছে কি না |
| `created_at`     | Record তৈরির সময়                           |
| `updated_at`     | সর্বশেষ পরিবর্তনের সময়                     |

### কেন `settings.AUTH_USER_MODEL` ব্যবহার করলাম?

তোমার custom user model হলো `accounts.User`। সরাসরি `User` class import না করে `settings.AUTH_USER_MODEL` ব্যবহার করলে Django-এর custom user configuration-এর সঙ্গে model relationship সামঞ্জস্যপূর্ণ থাকে।

### কেন `otp_verifier`-এর length 64?

Lesson 7-এ HMAC-SHA-256 digest-কে hexadecimal string হিসেবে return করেছি। তার length 64 character। তাই `max_length=64` যথেষ্ট।

এখানে OTP নিজে রাখা হয়নি। OTP-এর verifier রাখা হয়েছে।

### `on_delete=models.CASCADE` কেন?

যদি একটি user account delete করা হয়, সেই user-এর সঙ্গে যুক্ত OTP records-ও delete হবে। তোমার application-এর account deletion policy যদি audit records ধরে রাখার দাবি করে, তাহলে আলাদা retention design প্রয়োজন হতে পারে।

### `__str__()`-এ OTP দেখাচ্ছি না কেন?

Django admin, logs বা debugging output-এ model-এর string representation দেখা যেতে পারে। তাই `otp_verifier` বা original OTP কখনো `__str__()`-এ প্রকাশ করছি না।

## 4. Database migration চালাও

Project root-এ:

```
python manage.py check
python manage.py makemigrations accounts
python manage.py migrate
```

এবার Django model থেকে database schema তৈরি করবে।

Migration-এর আগে যাচাই করো:

- আগের custom `User` model অক্ষত আছে।
- `AUTH_USER_MODEL = "accounts.User"` আগেই configure করা আছে।
- `accounts` `INSTALLED_APPS`-এ আছে।
- Lesson 7-এর OTP generator ও verifier function আছে।

সতর্কতা: Custom user model-এর migrations আগে থেকেই হয়ে থাকলে database reset করার প্রয়োজন নেই। শুধু নতুন model-এর migration তৈরি করো। গুরুত্বপূর্ণ database কখনো মুছে ফেলবে না।

## 5. Django shell দিয়ে record তৈরি করো

প্রথমে OTP তৈরি করে verifier বানাব। Database-এ শুধু verifier save করব।

```
python manage.py shell
```

তারপর:

```
from django.contrib.auth import get_user_modelfrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import (    generate_otp,    get_otp_verifier,    get_otp_expiry,)User = get_user_model()user = User.objects.get(    email="your-test-email@example.com")otp = generate_otp()verifier = get_otp_verifier(otp)record = PasswordResetOTP.objects.create(    user=user,    otp_verifier=verifier,    expires_at=get_otp_expiry(),)print("Record ID:", record.pk)print("User ID:", record.user_id)print("Expiry:", record.expires_at)print("Attempts:", record.attempts)print("Used:", record.is_used)
```

এখানে `your-test-email@example.com`-এর জায়গায় database-এ থাকা test user-এর email দেবে।

Development-এ email পাঠানোর জন্য তৈরি OTP-টি service থেকে email function-এ pass করবে। Production-এ OTP console-এ print করা বা log-এ রাখা উচিত নয়।

পরীক্ষা শেষে shell থেকে বের হও:

```
exit()
```

## 6. Active, expired, used ও invalidated OTP

একটি OTP record আছে মানেই সেটি valid নয়। Verification-এর সময় অন্তত চারটি condition পরীক্ষা করতে হবে।

| অবস্থা      | Condition                                | ব্যবহার করা যাবে?  |
| ----------- | ---------------------------------------- | ------------------ |
| Active      | মেয়াদ আছে, ব্যবহার হয়নি, বাতিল হয়নি      | শর্তসাপেক্ষে হ্যাঁ |
| Expired     | বর্তমান সময় `expires_at`-এর সমান বা বেশি | না                 |
| Used        | `is_used=True`                           | না                 |
| Invalidated | `invalidated_at`-এ timestamp আছে         | না                 |

আমরা এই logic-টি পরবর্তী verification service-এ ব্যবহার করব। আপাতত Django shell-এ record পরীক্ষা করতে পারো:

```
from django.utils import timezonefrom accounts.models import PasswordResetOTPrecord = PasswordResetOTP.objects.latest("created_at")expired = timezone.now() >= record.expires_atvalid_state = (    not expired    and not record.is_used    and record.invalidated_at is None)print("Expired:", expired)print("Valid state:", valid_state)
```

`valid_state=True` শুধু record-এর lifecycle condition বোঝায়। User যে OTP দিয়েছে সেটি সঠিক কি না, attempts limit অতিক্রম করেছে কি না, কিংবা OTP request-টি বর্তমান কি না—এসবও যাচাই করতে হবে।

## 7. Resend করলে কী হবে?

ধরো user প্রথম OTP চাইল, তারপর নতুন OTP-এর জন্য resend করল। নিরাপদ design-এ নতুন code তৈরি করার সময় আগের active OTP invalidate করতে হবে।

নিচের code-টি পরবর্তী service layer-এর একটি শিক্ষামূলক উদাহরণ:

```
from django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import (    generate_otp,    get_otp_verifier,    get_otp_expiry,)def create_password_reset_otp(user):    with transaction.atomic():        # Lock the user row to serialize OTP creation        # for this account.        locked_user = type(user).objects.select_for_update().get(            pk=user.pk        )        now = timezone.now()        # Invalidate any previously active OTP records.        PasswordResetOTP.objects.filter(            user=locked_user,            is_used=False,            invalidated_at__isnull=True,        ).update(invalidated_at=now)        # Generate the new OTP and store only its verifier.        otp = generate_otp()        record = PasswordResetOTP.objects.create(            user=locked_user,            otp_verifier=get_otp_verifier(otp),            expires_at=get_otp_expiry(),        )    # Return the raw OTP only to the caller so it can be    # sent by email; never save it in the database.    return record, otp
```

এখানে `select_for_update()` user row lock করে একই user-এর জন্য একাধিক concurrent OTP creation serialize করতে সাহায্য করে। এটি কার্যকর হতে transaction এবং database-এর lock support প্রয়োজন; SQLite-এ production PostgreSQL-এর মতো locking behavior ধরে নেওয়া যাবে না।

আরেকটি গুরুত্বপূর্ণ বিষয়: শুধু `transaction.atomic()` ব্যবহার করলেই প্রতিটি race condition সমাধান হয় না। OTP verification ও password update-ও transaction-এর মধ্যে সঠিকভাবে design করতে হবে। পরবর্তী লেসনগুলোতে আমরা এটি ধাপে ধাপে করব।

এই উদাহরণটি resend rate limit, user enumeration protection, email delivery failure এবং request throttling এখনো implement করে না। Production API বানানোর আগে সেগুলো যোগ করতে হবে।

## 8. Database indexing কেন করেছি?

আমরা দুটি index যোগ করেছি:

```
models.Index(    fields=["user", "-created_at"],    name="pwdotp_user_created_idx",)
```

এটি একটি user-এর সাম্প্রতিক OTP record খুঁজতে সাহায্য করে।

```
models.Index(    fields=["expires_at"],    name="pwdotp_expires_idx",)
```

এটি expiry time অনুযায়ী record খোঁজা বা cleanup query-তে সহায়ক হতে পারে।

তবে index-এরও খরচ আছে: database storage লাগে এবং insert/update-এর সময় অতিরিক্ত কাজ হয়। Query pattern অনুযায়ী index বেছে নিতে হবে; প্রতিটি field-এ index দেওয়া ভালো practice নয়।

## 9. Production-এর আগে আরও যেসব বিষয় implement করতে হবে

এই model হলো একটি ভিত্তি, সম্পূর্ণ security solution নয়।

- Attempt limit: উদাহরণ হিসেবে পাঁচটি ভুল verification attempt-এর পর OTP বাতিল করা।
- Resend throttling: একই user বা IP থেকে বারবার OTP পাঠানো সীমিত করা।
- Single-use verification: সফল verification-এর পর একই OTP দ্বিতীয়বার গ্রহণ না করা।
- Password reset authorization: OTP verify হওয়ার পর password reset করার জন্য স্বল্পমেয়াদি reset grant/token দেওয়া, অথবা একটি নিরাপদ atomic workflow ব্যবহার করা।
- Cleanup: পুরোনো expired records নিয়মিত delete বা archive করা।
- Email delivery failure: email পাঠাতে ব্যর্থ হলে record কীভাবে invalidate বা retry হবে, তা নির্ধারণ করা।
- Account enumeration protection: email address registered কি না, তা API response দিয়ে প্রকাশ না করা।

## 10. Lesson 8 assignment

Assignment progress

0/8

PasswordResetOTP model তৈরি করেছি

OTP verifier ও expiry time save করেছি

User-এর সঙ্গে ForeignKey relationship তৈরি করেছি

Attempts, used এবং invalidated state যোগ করেছি

Migration চালিয়ে database schema তৈরি করেছি

Shell দিয়ে test OTP record তৈরি করেছি

Expiry ও lifecycle conditions পরীক্ষা করেছি

Resend-এর সময় আগের OTP invalidate করার flow বুঝেছি

## পরবর্তী লেসন — Lesson 9: Forgot Password Serializer

পরের লেসনে আমরা DRF serializer তৈরি করব, যা:

1. User-এর email input validate করবে।
2. Email-এর format পরীক্ষা করবে।
3. Password reset request-এর input গ্রহণ করবে।
4. Sensitive account information প্রকাশ না করে request handle করার ভিত্তি তৈরি করবে।
5. পরবর্তী Lesson 10-এর Forgot Password API-এর সঙ্গে যুক্ত হবে।

এখন পর্যন্ত আমরা OTP তৈরি, email পাঠানো এবং database-এ নিরাপদ verifier রাখার ভিত্তি তৈরি করেছি। পরের ধাপে এগুলোকে বাস্তব API workflow-তে যুক্ত করব।

---
# Lesson 9: Forgot Password Serializer — Django REST Framework

আজ আমরা আমাদের OTP-based password reset system-এর প্রথম API layer তৈরি করব: Forgot Password Serializer।

আগের লেসনগুলোতে আমরা secure OTP generate করা, HTML email তৈরি করা এবং `PasswordResetOTP` database model তৈরি করা শিখেছি। এবার user যখন Forgot Password form-এ email দিয়ে Submit করবে, তখন DRF কীভাবে সেই input validate করবে তা implement করব।

আজকের মূল লক্ষ্য হলো শুধু serializer-এর code লেখা নয়—কোন validation serializer-এ হবে, কোন কাজ service layer-এ হবে এবং কেন হবে, তা বোঝা।

## 1. সম্পূর্ণ workflow-তে Serializer-এর জায়গা

Frontend Forgot Password Form

User email address দেয়

ForgotPasswordSerializer

Input ও email format validate করে

Forgot Password API View

Request গ্রহণ করে service call করবে

OTP Service → Email Service

OTP তৈরি, record সংরক্ষণ ও email পাঠানো

একটি গুরুত্বপূর্ণ distinction:

- Serializer: input-এর structure ও validity পরীক্ষা করে।
- View: HTTP request ও response পরিচালনা করে।
- Service: OTP তৈরি, database operation এবং email delivery-এর business logic পরিচালনা করে।

Serializer-এর মধ্যে সরাসরি SMTP call বা OTP database management রাখব না। এতে code test করা ও maintain করা সহজ হয়।

## 2. Project structure

আগের project-এ এই ফাইল ব্যবহার করব:

```
accounts/
├── models.py
├── serializers.py
├── services/
│   ├── email_service.py
│   └── otp_service.py
└── views.py
```

যদি `accounts/serializers.py` আগে তৈরি করে থাকো, সেটি replace করবে না। নতুন serializer-টি বিদ্যমান ফাইলের মধ্যে যোগ করবে।

## 3. প্রথম Serializer তৈরি করো

ফাইল: `accounts/serializers.py`

```
from rest_framework import serializersclass ForgotPasswordSerializer(serializers.Serializer):    email = serializers.EmailField(        required=True,        max_length=254,        trim_whitespace=True,        write_only=True,    )
```

এই code ছোট, কিন্তু প্রতিটি option-এর কাজ বোঝা জরুরি।

### Line-by-line explanation

`serializers.Serializer`

আমরা `ModelSerializer` ব্যবহার করছি না, কারণ এই request সরাসরি কোনো model record তৈরি বা update করে না। এটি একটি input-validation operation।

`serializers.EmailField`

DRF-এর `EmailField` email-এর format validate করে। যেমন `user@example.com` গ্রহণযোগ্য format, কিন্তু `hello` valid email format নয়।

মনে রাখবে, email format সঠিক হলেই mailbox বাস্তবে আছে—এমন নিশ্চয়তা নেই।

`required=True`

Request-এ `email` field অবশ্যই দিতে হবে।

`max_length=254`

Email address-এর সর্বোচ্চ দৈর্ঘ্য সীমাবদ্ধ রাখছি।

`trim_whitespace=True`

Email-এর শুরু বা শেষে accidental whitespace থাকলে তা trim করতে সাহায্য করে।

`write_only=True`

এটি input field। Response-এ email field স্বয়ংক্রিয়ভাবে প্রকাশ করার জন্য নয়। যদিও আমাদের response আলাদাভাবে view-তে তৈরি হবে।

## 4. Email registered কি না, Serializer-এ পরীক্ষা করব?

ধরো, কেউ এই request পাঠাল:

```
{
  "email": "someone@example.com"
}
```

এখন দুটি সম্ভাবনা:

1. Email address দিয়ে account registered আছে।
2. Email address দিয়ে কোনো account নেই।

Serializer-এর কাজ email format validate করা। এই ধাপে database-এ user খোঁজার প্রয়োজন নেই।

কেন?

যদি API এমন response দেয়—

- “এই email registered”
- “এই email registered নয়”

তাহলে কেউ API-তে বিভিন্ন email দিয়ে পরীক্ষা করে account-এর অস্তিত্ব জানতে পারে। একে account enumeration বলা হয়।

তাই আমাদের API সাধারণত দুই ক্ষেত্রেই একই ধরনের generic response দেবে:

> If an account exists with this email, password reset instructions will be sent.

এই response দেওয়ার জন্য view ও service layer পরবর্তী লেসনে implement করব।

গুরুত্বপূর্ণ: শুধু generic response দিলেই সব ধরনের enumeration risk দূর হয় না। Response timing, rate limiting এবং email sending-এর behavior-ও বিবেচনা করতে হবে।

## 5. Serializer নিজে test করো

প্রথমে Django shell চালাও:

```
python manage.py shell
```

### Test A: Valid email

```
from accounts.serializers import ForgotPasswordSerializerserializer = ForgotPasswordSerializer(    data={        "email": "learner@example.com"    })print(serializer.is_valid())print(serializer.errors)print(serializer.validated_data)
```

Expected result:

```
True{}{"email": "learner@example.com"}
```

`validated_data`-তে কেবল validation সফল হওয়া data পাওয়া যায়।

### Test B: Invalid email

```
serializer = ForgotPasswordSerializer(    data={        "email": "not-an-email"    })print(serializer.is_valid())print(serializer.errors)
```

এখানে `is_valid()` হবে `False` এবং `email` field-এর জন্য validation error পাওয়া যাবে।

### Test C: Email missing

```
serializer = ForgotPasswordSerializer(    data={})print(serializer.is_valid())print(serializer.errors)
```

এখানেও validation fail করবে, কারণ `email` required।

### Test D: Whitespace

```
serializer = ForgotPasswordSerializer(    data={        "email": "  learner@example.com  "    })print(serializer.is_valid())if serializer.is_valid():    print(serializer.validated_data)
```

`trim_whitespace=True` থাকার কারণে email-এর বাইরের whitespace trim হবে।

## 6. API-তে পাঠানোর request format

আমাদের পরবর্তী লেসনে endpoint হবে:

`POST /api/auth/otp/forgot/`

Request body:

```
{
  "email": "learner@example.com"
}
```

এই endpoint-এর জন্য আমরা পরে `ForgotPasswordSerializer` ব্যবহার করব।

এখনও endpoint তৈরি হয়নি, তাই এই মুহূর্তে request পাঠালে 404 পাওয়া স্বাভাবিক। Lesson 10-এ view, URL এবং OTP service সংযুক্ত করে endpoint তৈরি করব।

## 7. Serializer-এ যেসব কাজ করবে না

| কাজ                         | কোথায় করা উচিত                                |
| --------------------------- | --------------------------------------------- |
| Email format validate       | Serializer                                    |
| OTP generate                | OTP service                                   |
| OTP verifier তৈরি           | OTP service                                   |
| OTP record save/invalidate  | Service বা উপযুক্ত business logic layer       |
| Email পাঠানো                | Email service                                 |
| HTTP status ও response তৈরি | View                                          |
| Request throttling          | DRF throttling বা উপযুক্ত rate-limiting layer |
| Password পরিবর্তন           | Password reset service/view                   |

এই separation বজায় রাখলে একই OTP service ভবিষ্যতে অন্য view বা workflow থেকেও ব্যবহার করতে পারবে।

## 8. ঐচ্ছিক উন্নতি: Custom error message

তুমি চাইলে email field-এর error message নিজে নির্ধারণ করতে পারো:

```
from rest_framework import serializersclass ForgotPasswordSerializer(serializers.Serializer):    email = serializers.EmailField(        required=True,        max_length=254,        trim_whitespace=True,        write_only=True,        error_messages={            "required": "Email address is required.",            "blank": "Email address cannot be empty.",            "invalid": "Enter a valid email address.",            "max_length": "Email address is too long.",        },    )
```

এটি বাধ্যতামূলক নয়। তবে API-এর validation response ধারাবাহিক রাখতে custom message উপকারী।

## 9. Lesson 9 assignment

নিজে implement করে checklist পূরণ করো।

Assignment progress

0/7

ForgotPasswordSerializer তৈরি করেছি

Valid email দিয়ে test করেছি

Invalid email দিয়ে test করেছি

Email missing থাকলে validation fail হচ্ছে

Whitespace trim হচ্ছে কি না পরীক্ষা করেছি

Serializer-এ OTP generation বা email sending রাখিনি

Account enumeration কেন এড়াতে হয় বুঝেছি

## পরবর্তী লেসন — Lesson 10: Forgot Password API View

এবার আমরা তৈরি করব:

1. `ForgotPasswordSerializer`-কে API view-তে ব্যবহার।
2. `POST /api/auth/otp/forgot/` endpoint।
3. User account খোঁজা ও generic response দেওয়া।
4. OTP generation, database record এবং email service যুক্ত করা।
5. Error handling, throttling এবং email failure-এর আচরণ নির্ধারণ।

তখন প্রথমবারের মতো আমাদের OTP-based password reset project-এর একটি বাস্তব API end-to-end কাজ করবে।

----
# Lesson 10: Forgot Password API View — Django REST Framework

এই লেসনে আমরা Lesson 9-এর `ForgotPasswordSerializer` ব্যবহার করে একটি বাস্তব API তৈরি করব। API-টি ব্যবহারকারীকে ইমেইলের মাধ্যমে password reset OTP পাঠানোর প্রক্রিয়া শুরু করবে।

আজকের লক্ষ্য হলো শুধু কোড লেখা নয়—Serializer → API View → User lookup → OTP তৈরি → Database save → Email send → API response পুরো flow বুঝে নিজের হাতে implement করতে শেখা।

## ১. আজকের API কীভাবে কাজ করবে?

Frontend

ব্যবহারকারী ইমেইল দিয়ে Forgot Password submit করবে

`POST /api/auth/otp/forgot/`

`ForgotPasswordSerializer` ইমেইল validate করবে

User lookup

ইমেইল দিয়ে account খোঁজা হবে; account না থাকলেও response একই থাকবে

OTP service

পুরোনো সক্রিয় OTP invalid করে নতুন OTP তৈরি ও database-এ save

Email service

OTP ইমেইল করা হবে

গুরুত্বপূর্ণ: এই API শুধু OTP পাঠানোর অনুরোধ করবে। OTP verify করা এবং password পরিবর্তন করা হবে পরবর্তী lessons-এ।

## ২. Lesson 9-এর Serializer যাচাই করো

ফাইল: `accounts/serializers.py`

```
from rest_framework import serializersclass ForgotPasswordSerializer(serializers.Serializer):    email = serializers.EmailField(        required=True,        max_length=254,        trim_whitespace=True,        write_only=True,    )
```

এখানে `Serializer` ব্যবহার করেছি, কারণ আমরা request data validate করছি; সরাসরি কোনো model তৈরি করছি না।

## ৩. OTP তৈরি ও save করার service

Lesson 8-এ OTP model ও generation নিয়ে কাজ করেছি। এবার সেই logic-কে reusable service-এ রাখব।

ফাইল: `accounts/services/password_reset_service.py`

```
from django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import (    generate_otp,    get_otp_expiry,    get_otp_verifier,)def create_password_reset_otp(user):    """    Create a new OTP and invalidate previous unused OTP records.    Return the saved record and plaintext OTP for immediate email delivery.    """    with transaction.atomic():        user_model = type(user)        # Lock the user row where the database supports row locking.        locked_user = (            user_model.objects            .select_for_update()            .get(pk=user.pk)        )        now = timezone.now()        PasswordResetOTP.objects.filter(            user=locked_user,            is_used=False,            invalidated_at__isnull=True,        ).update(invalidated_at=now)        otp = generate_otp()        record = PasswordResetOTP.objects.create(            user=locked_user,            otp_verifier=get_otp_verifier(otp),            expires_at=get_otp_expiry(),        )    return record, otp
```

### কোডটি কেন এমনভাবে লিখলাম?

- `transaction.atomic()` — OTP record তৈরির database operation-গুলো একসঙ্গে সম্পন্ন করতে সাহায্য করে।
- `select_for_update()` — সমর্থিত database-এ একই user-এর concurrent request নিয়ন্ত্রণে সহায়তা করে। SQLite-এ row-level locking-এর আচরণ আলাদা।
- `invalidated_at` — আগের unused OTP-গুলোকে আর ব্যবহারযোগ্য না রাখার জন্য।
- `get_otp_verifier(otp)` — database-এ plaintext OTP না রেখে HMAC verifier রাখার জন্য।
- `return record, otp` — database-এ verifier save হবে; আসল OTP শুধু ইমেইল পাঠানোর কাজে ব্যবহার করা হবে।

এই service নিজে rate limiting করে না। Resend limit, request throttling এবং email failure handling-ও আলাদাভাবে যুক্ত করতে হবে।

## ৪. Forgot Password API View তৈরি করো

এবার মূল API তৈরি করব।

ফাইল: `accounts/views.py`

```
import loggingfrom django.contrib.auth import get_user_modelfrom django.utils import timezonefrom rest_framework import statusfrom rest_framework.permissions import AllowAnyfrom rest_framework.response import Responsefrom rest_framework.throttling import ScopedRateThrottlefrom rest_framework.views import APIViewfrom accounts.serializers import ForgotPasswordSerializerfrom accounts.models import PasswordResetOTPfrom accounts.services.email_service import (    send_password_reset_otp_email,)from accounts.services.password_reset_service import (    create_password_reset_otp,)logger = logging.getLogger(__name__)User = get_user_model()class ForgotPasswordAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "forgot_password"    def post(self, request):        # Step 1: Validate incoming request data.        serializer = ForgotPasswordSerializer(data=request.data)        serializer.is_valid(raise_exception=True)        email = serializer.validated_data["email"]        # Step 2: Always use a generic response.        response_data = {            "detail": (                "If an account exists with this email, "                "password reset instructions will be sent."            )        }        # Step 3: Find an active account.        user = User.objects.filter(            email__iexact=email,            is_active=True,        ).first()        # Step 4: Do not reveal whether the account exists.        if user is None:            return Response(                response_data,                status=status.HTTP_200_OK,            )        # Step 5: Create and save a new OTP.        record, otp = create_password_reset_otp(user)        # Step 6: Send the OTP email.        try:            sent = send_password_reset_otp_email(                recipient_email=user.email,                otp=otp,                expiry_minutes=5,            )            if not sent:                raise RuntimeError(                    "Email backend did not report a successful send."                )        except Exception:            # Invalidate an OTP that was not successfully handed            # to the configured email backend.            PasswordResetOTP.objects.filter(                pk=record.pk,                is_used=False,                invalidated_at__isnull=True,            ).update(invalidated_at=timezone.now())            logger.exception(                "Password reset OTP email delivery failed."            )        # Step 7: Return the same generic response.        return Response(            response_data,            status=status.HTTP_200_OK,        )
```

### View-এর গুরুত্বপূর্ণ অংশগুলো বুঝে নাও

| কোড                              | কাজ                                                                         |
| -------------------------------- | --------------------------------------------------------------------------- |
| `AllowAny`                       | Login না করেও endpoint ব্যবহার করা যাবে                                     |
| `ScopedRateThrottle`             | নির্ধারিত scope অনুযায়ী request সীমিত করবে                                  |
| `is_valid(raise_exception=True)` | Invalid input হলে DRF স্বয়ংক্রিয়ভাবে `400 Bad Request` দেবে                 |
| `email__iexact`                  | Case-insensitive email lookup                                               |
| `is_active=True`                 | নিষ্ক্রিয় account-এর জন্য OTP তৈরি করবে না                                  |
| Generic response                 | ইমেইল দিয়ে account আছে কি না, তা প্রকাশ করবে না                             |
| `try/except`                     | Email backend-এর failure সামলাবে                                            |
| `logger.exception()`             | Server log-এ failure-এর তথ্য রাখবে; OTP বা email address সরাসরি log করবে না |

নিরাপত্তার বিষয়: account না থাকলে এবং account থাকলে—দুই ক্ষেত্রেই একই response ও status code দেওয়া হচ্ছে। এতে account enumeration-এর ঝুঁকি কমে। তবে response time-এর পার্থক্য, throttling এবং অন্যান্য আচরণও বিবেচনা করতে হবে।

আরেকটি বিষয়: Django email backend-এর `send()` সফল হওয়া মানেই ইমেইলটি ব্যবহারকারীর inbox-এ পৌঁছেছে, এমন নিশ্চয়তা নেই।

## ৫. URL তৈরি করো

ফাইল: `accounts/urls.py`

```
from django.urls import pathfrom accounts.views import ForgotPasswordAPIViewurlpatterns = [    path(        "otp/forgot/",        ForgotPasswordAPIView.as_view(),        name="forgot-password-otp",    ),]
```

এবার `config/urls.py`-এ accounts-এর URL যুক্ত করো:

```
from django.contrib import adminfrom django.urls import include, pathurlpatterns = [    path("admin/", admin.site.urls),    path(        "api/auth/",        include("dj_rest_auth.urls"),    ),    path(        "api/auth/registration/",        include("dj_rest_auth.registration.urls"),    ),    path(        "api/auth/",        include("accounts.urls"),    ),]
```

এখন custom endpoint হবে:

`POST /api/auth/otp/forgot/`

`dj-rest-auth`-এর built-in password-reset endpoint এবং আমাদের custom OTP endpoint আলাদা। দুটোকে এক করে ফেলবে না।

## ৬. API rate limiting configure করো

ফাইল: `config/settings.py`

তোমার `REST_FRAMEWORK` dictionary-তে নিচের rate যোগ করো। আগে থেকেই `REST_FRAMEWORK` থাকলে সেটি replace না করে এই key-টি তার মধ্যে যুক্ত করবে।

```
REST_FRAMEWORK = {    # তোমার আগের authentication ও permission settings রাখবে।    "DEFAULT_THROTTLE_RATES": {        "forgot_password": "5/hour",    },}
```

এটি `ScopedRateThrottle`-এর জন্য প্রতি IP-ভিত্তিক সাধারণ সীমা নির্ধারণ করবে। তোমার আগের `REST_FRAMEWORK`-এ থাকা `DEFAULT_AUTHENTICATION_CLASSES` ও `DEFAULT_PERMISSION_CLASSES`-ও রাখতে হবে।

এটি একটি প্রাথমিক সীমা, সম্পূর্ণ production security নয়। Production-এ shared cache (যেমন Redis), email address-ভিত্তিক সীমা, resend cooldown এবং monitoring বিবেচনা করবে। DRF throttling নিজে সব ধরনের abuse প্রতিরোধের নিশ্চয়তা দেয় না।

## ৭. API পরীক্ষা করো

প্রথমে project root-এ এই command চালাও:

```
python manage.py check
python manage.py runserver
```

যদি check-এ error আসে, আগে সেটি ঠিক করো।

### Test A: Valid email

Terminal-এর অন্য একটি tab-এ চালাও:

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/forgot/ \
  -H "Content-Type: application/json" \
  -d '{"email":"your-test-email@example.com"}'
```

এখানে `your-test-email@example.com`-এর জায়গায় তোমার test account-এর email দেবে।

Response:

```
{
  "detail": "If an account exists with this email, password reset instructions will be sent."
}
```

HTTP status: `200 OK`

- Console email backend ব্যবহার করলে terminal-এ email content দেখা যাবে।
- SMTP ব্যবহার করলে email backend পাঠানোর চেষ্টা করবে।
- Response একই হলেও, account থাকলে OTP record তৈরি হবে এবং email backend-এ পাঠানোর চেষ্টা করা হবে।

### Test B: Account নেই এমন email

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/forgot/ \
  -H "Content-Type: application/json" \
  -d '{"email":"unknown-user@example.com"}'
```

এক্ষেত্রেও একই response পাওয়ার কথা। এতে কেউ শুধু API call করে সহজে বুঝতে পারবে না কোন email নিবন্ধিত।

### Test C: Invalid email

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/forgot/ \
  -H "Content-Type: application/json" \
  -d '{"email":"invalid-email"}'
```

এবার `400 Bad Request` আসবে, কারণ email validation ব্যর্থ হয়েছে।

### Test D: OTP database-এ save হয়েছে কি না

```
python manage.py shell
```

তারপর:

```
from accounts.models import PasswordResetOTPPasswordResetOTP.objects.order_by("-created_at").values(    "id",    "user_id",    "otp_verifier",    "expires_at",    "is_used",    "invalidated_at",).first()
```

এখানে `otp_verifier` দেখতে পাবে; আসল ছয় অঙ্কের OTP database-এ রাখা হচ্ছে না।

যদি কোনো record না আসে, তাহলে যাচাই করো:

1. Email-টি কোনো active user-এর কি না।
2. `PasswordResetOTP` model migrate হয়েছে কি না।
3. Request-টি সঠিক endpoint-এ যাচ্ছে কি না।
4. Email পাঠানোর আগে OTP service-এ error হচ্ছে কি না।

## ৮. Common mistakes

- `404 Not Found`: `accounts/urls.py` তৈরি হয়েছে কি না এবং `config/urls.py`-এ include করা হয়েছে কি না দেখো।
- `401 Unauthorized`: View-এ `permission_classes = [AllowAny]` আছে কি না দেখো।
- `429 Too Many Requests`: Throttle limit অতিক্রম করলে এমন হতে পারে; testing-এর জন্য বারবার request পাঠিয়ো না।
- Email যাচ্ছে না: Development-এ console backend ব্যবহার করো; SMTP হলে `.env`, Gmail App Password, TLS ও server log যাচাই করো।
- `ModuleNotFoundError`: Lesson 8-এর `PasswordResetOTP` model এবং Lesson 7-এর `otp_service.py` ফাইলের নাম ও import path মিলিয়ে দেখো।
- Duplicate বা invalid OTP: পরের ধাপে verify endpoint-এ expiry, attempt limit, invalidation এবং single-use enforcement নিশ্চিত করতে হবে।

## ৯. আজকের lesson checklist

Lesson 10 progress

0 / 7

ForgotPasswordSerializer দিয়ে request validate করেছি

ForgotPasswordAPIView তৈরি করেছি

User lookup এবং generic response বুঝেছি

OTP database-এ save ও email service call করেছি

URL configure করেছি

Valid, invalid এবং unknown email দিয়ে API test করেছি

Database-এ plaintext OTP রাখা হচ্ছে না—এটি যাচাই করেছি

## ১০. তোমার practical assignment

নিজে implement করে নিচের তিনটি প্রশ্নের উত্তর বের করার চেষ্টা করো:

1. `AllowAny` কেন ব্যবহার করেছি, কিন্তু `IsAuthenticated` নয়?
2. Email backend fail করলে OTP-কে invalid করা কেন গুরুত্বপূর্ণ?
3. Account না থাকলেও কেন `404` না দিয়ে `200` response দিচ্ছি?

পরবর্তী লেসন — Lesson 11: OTP Email Integration ও Failure Handling। সেখানে email service-কে আরও ভালোভাবে পরীক্ষা করব, email delivery failure-এর পর কী হবে তা নির্ধারণ করব, এবং OTP resend-এর সঙ্গে এর সম্পর্ক বুঝব। এরপর Lesson 12-এ OTP verification endpoint তৈরি করব।

-----
# Lesson 11: OTP Email Integration ও Failure Handling

এই লেসনে আমরা আগের Lesson 6-এর HTML email service এবং Lesson 10-এর Forgot Password API-কে আরও নির্ভরযোগ্যভাবে যুক্ত করব। বিশেষ করে, OTP তৈরি হয়েছে কিন্তু email পাঠানো ব্যর্থ হয়েছে—এমন পরিস্থিতিতে কী হবে, সেটি সঠিকভাবে handle করব।

আজকের মূল লক্ষ্য:

- OTP email service-কে testable ও reusable করা।
- HTML এবং plain-text email পাঠানো।
- Email backend-এর failure শনাক্ত করা।
- Email ব্যর্থ হলে OTP-কে invalid করা।
- Email-এ OTP বা sensitive data log না করা।
- Automated test দিয়ে success এবং failure—দুই পরিস্থিতিই যাচাই করা।

## ১. Email flow বুঝে নাও

1\. OTP generate

ছয় অঙ্কের OTP তৈরি

2\. OTP verifier database-এ save

Plaintext OTP নয়, HMAC verifier রাখা হবে

3\. Email service call

HTML + plain-text message তৈরি করে backend-এ পাঠানো

Email backend success

OTP ব্যবহারকারীর কাছে পৌঁছানোর চেষ্টা সম্পন্ন

Email backend failure

OTP invalid করে failure log করা

মনে রাখবে: email backend success মানেই email inbox-এ পৌঁছেছে—এমন নয়। SMTP server message গ্রহণ করলেও পরবর্তী delivery ব্যর্থ হতে পারে।

## ২. Email service-এর দায়িত্ব আলাদা রাখো

আমাদের project structure হবে:

```
accounts/
├── services/
│   ├── __init__.py
│   ├── email_service.py
│   ├── otp_service.py
│   └── password_reset_service.py
└── templates/
    └── emails/
        ├── password_reset_otp.html
        └── password_reset_otp.txt
```

এখানে:

- `otp_service.py` — OTP generate ও verify করার logic।
- `password_reset_service.py` — OTP record তৈরি ও invalidation।
- `email_service.py` — email message তৈরি ও পাঠানো।

এই separation-এর সুবিধা হলো, ভবিষ্যতে Gmail SMTP থেকে অন্য email provider-এ পরিবর্তন করলেও API view-এর অধিকাংশ logic পরিবর্তন করতে হবে না।

## ৩. Professional Email Service তৈরি করো

ফাইল: `accounts/services/email_service.py`

আগের code-এর সঙ্গে মিলিয়ে নিচের version ব্যবহার করো:

```
from django.conf import settingsfrom django.core.mail import EmailMultiAlternativesfrom django.template.loader import render_to_stringdef send_password_reset_otp_email(    recipient_email: str,    otp: str,    expiry_minutes: int = 5,) -> bool:    """    Send password-reset OTP as both HTML and plain-text email.    Raises an exception if the configured email backend fails.    Returns True when the backend reports that one message was sent.    """    context = {        "otp": otp,        "expiry_minutes": expiry_minutes,    }    subject = "Your password reset verification code"    text_content = render_to_string(        "emails/password_reset_otp.txt",        context,    )    html_content = render_to_string(        "emails/password_reset_otp.html",        context,    )    email = EmailMultiAlternatives(        subject=subject,        body=text_content,        from_email=settings.DEFAULT_FROM_EMAIL,        to=[recipient_email],    )    email.attach_alternative(        html_content,        "text/html",    )    sent_count = email.send(fail_silently=False)    return sent_count == 1
```

### কোন লাইন কেন প্রয়োজন?

`render_to_string()`

Template-এর মধ্যে থাকা `{{ otp }}` এবং `{{ expiry_minutes }}`-এর জায়গায় নির্দিষ্ট মান বসায়।

`EmailMultiAlternatives`

একই email-এ দুটি format পাঠায়:

- Plain text — HTML render করতে পারে না এমন email client-এর জন্য।
- HTML — সুন্দর layout ও OTP highlight করার জন্য।

`fail_silently=False`

Email backend exception দিলে সেটি চেপে না রেখে caller-এর কাছে পাঠায়। ফলে API view failure handling করতে পারে।

`return sent_count == 1`

Backend একটি message গ্রহণ করেছে কি না, সেটি বোঝায়। Inbox delivery নিশ্চিত করে না।

## ৪. HTML ও plain-text template যাচাই করো

ফাইল: `accounts/templates/emails/password_reset_otp.txt`

```
Password Reset Verification Code

Your password reset code is: {{ otp }}

This code expires in {{ expiry_minutes }} minutes.

If you did not request a password reset, you can ignore this email.
Do not share this code with anyone.
```

ফাইল: `accounts/templates/emails/password_reset_otp.html`

তোমার Lesson 6-এর professional HTML template আগে থেকেই থাকলে সেটিই রাখবে। নিশ্চিত করবে সেখানে এই variables আছে:

```
<h2>Password Reset Verification</h2>

<p>Your verification code is:</p>

<h1>{{ otp }}</h1>

<p>
  This code expires in {{ expiry_minutes }} minutes.
</p>

<p>
  If you did not request this, you can ignore this email.
  Do not share this code with anyone.
</p>
```

এটি template-এর মূল অংশের উদাহরণ, সম্পূর্ণ design নয়। HTML email-এর জন্য inline CSS ব্যবহার করা ভালো, কারণ অনেক email client external stylesheet উপেক্ষা করে।

## ৫. Email configuration যাচাই করো

Development-এ email কোথায় যাচ্ছে তা দেখার জন্য console backend ব্যবহার করতে পারো।

`config/settings.py`:

```
EMAIL_BACKEND = (    "django.core.mail.backends.console.EmailBackend")DEFAULT_FROM_EMAIL = "OTP Auth <noreply@example.com>"
```

Console backend email terminal-এ print করবে। এটি inbox-এ email পাঠায় না।

SMTP ব্যবহার করতে চাইলে `.env`-এ configuration রাখবে:

```
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
DEFAULT_FROM_EMAIL=OTP Auth <your-email@gmail.com>
```

Settings-এ `.env` থেকে মান load করার পর:

```
import osEMAIL_BACKEND = (    "django.core.mail.backends.smtp.EmailBackend")EMAIL_HOST = os.getenv("EMAIL_HOST", "smtp.gmail.com")EMAIL_PORT = int(os.getenv("EMAIL_PORT", "587"))EMAIL_USE_TLS = (    os.getenv("EMAIL_USE_TLS", "True").lower() == "true")EMAIL_HOST_USER = os.getenv("EMAIL_HOST_USER", "")EMAIL_HOST_PASSWORD = os.getenv("EMAIL_HOST_PASSWORD", "")DEFAULT_FROM_EMAIL = os.getenv(    "DEFAULT_FROM_EMAIL",    EMAIL_HOST_USER,)EMAIL_TIMEOUT = 10
```

`EMAIL_TIMEOUT = 10` connection attempt-এর সময়সীমা নির্ধারণ করে। `.env` কখনো Git-এ commit করবে না; Gmail-এর ক্ষেত্রে সাধারণ account password-এর বদলে App Password ব্যবহার করতে হবে।

## ৬. Email ব্যর্থ হলে OTP invalid করো

Lesson 10-এর `ForgotPasswordAPIView`-এ আমরা ইতিমধ্যে email failure ধরার code লিখেছি। এখন সেই অংশটি ভালোভাবে বুঝি।

```
try:    sent = send_password_reset_otp_email(        recipient_email=user.email,        otp=otp,        expiry_minutes=5,    )    if not sent:        raise RuntimeError(            "Email backend did not report a successful send."        )except Exception:    PasswordResetOTP.objects.filter(        pk=record.pk,        is_used=False,        invalidated_at__isnull=True,    ).update(        invalidated_at=timezone.now()    )    logger.exception(        "Password reset OTP email delivery failed."    )
```

### কেন OTP invalid করছি?

ধরো:

1. OTP তৈরি হলো: `482731`।
2. Database-এ OTP-এর verifier save হলো।
3. Email server connection ব্যর্থ হলো।
4. ব্যবহারকারী OTP পেল না, কিন্তু database-এ সেটি ব্যবহারযোগ্য রয়ে গেল।

এক্ষেত্রে OTP-টি invalid করা উচিত, যাতে email পাঠানো ব্যর্থ হওয়ার পরেও সেটি দিয়ে password reset করার সুযোগ না থাকে।

`invalidated_at` ব্যবহার করে আমরা record-এর invalidation time রাখছি। Verification endpoint-এ অবশ্যই এই condition-ও পরীক্ষা করতে হবে:

```
otp_record.invalidated_at is None
```

এছাড়া `is_used` এবং `expires_at`-ও যাচাই করতে হবে।

গুরুত্বপূর্ণ: Email পাঠানো ও database transaction-কে একটি atomic operation বানানো যায় না—SMTP এবং database আলাদা system। তাই এই pattern-টি failure সামলাতে সাহায্য করে, কিন্তু email provider message গ্রহণ করার পরেও delivery ব্যর্থ হলে তা শনাক্ত করতে পারে না।

আরেকটি বাস্তব trade-off আছে: একই ব্যবহারকারীর একাধিক request একসঙ্গে এলে নতুন OTP আগের OTP-কে invalid করতে পারে। তাই rate limiting, resend cooldown এবং request concurrency-ও নিয়ন্ত্রণ করতে হবে।

## ৭. Automated test: Email সফলভাবে তৈরি হচ্ছে কি না

Django-তে `locmem` email backend ব্যবহার করে প্রকৃত email না পাঠিয়েই পরীক্ষা করা যায়।

ফাইল: `accounts/tests/test_email_service.py`

প্রথমে `accounts/tests/`-এর মধ্যে `__init__.py` আছে কি না নিশ্চিত করো। তারপর:

```
from django.core import mailfrom django.test import TestCase, override_settingsfrom accounts.services.email_service import (    send_password_reset_otp_email,)@override_settings(    EMAIL_BACKEND="django.core.mail.backends.locmem.EmailBackend",    DEFAULT_FROM_EMAIL="test@example.com",)class PasswordResetEmailServiceTests(TestCase):    def test_sends_html_and_plain_text_email(self):        result = send_password_reset_otp_email(            recipient_email="learner@example.com",            otp="482731",            expiry_minutes=5,        )        self.assertTrue(result)        self.assertEqual(len(mail.outbox), 1)        email = mail.outbox[0]        self.assertEqual(            email.subject,            "Your password reset verification code",        )        self.assertEqual(            email.to,            ["learner@example.com"],        )        self.assertIn("482731", email.body)        self.assertTrue(            any(                content_type == "text/html"                and "482731" in content                for content, content_type                in email.alternatives            )        )
```

Test চালাও:

```
python manage.py test accounts.tests.test_email_service
```

এখানে `mail.outbox` হলো test চলাকালীন Django যে email তৈরি করেছে তার তালিকা। এটি বাস্তবে ইমেইল পাঠায় না।

## ৮. Automated test: Email failure হলে exception আসে কি না

একই test file-এ এই test যোগ করো:

```
from unittest.mock import patchfrom django.test import TestCase, override_settingsfrom accounts.services.email_service import (    send_password_reset_otp_email,)@override_settings(    EMAIL_BACKEND="django.core.mail.backends.locmem.EmailBackend",    DEFAULT_FROM_EMAIL="test@example.com",)class PasswordResetEmailFailureTests(TestCase):    @patch(        "accounts.services.email_service.EmailMultiAlternatives.send"    )    def test_email_backend_exception_is_propagated(        self,        mocked_send,    ):        mocked_send.side_effect = OSError(            "Simulated email backend failure"        )        with self.assertRaises(OSError):            send_password_reset_otp_email(                recipient_email="learner@example.com",                otp="482731",                expiry_minutes=5,            )
```

এই test-এর উদ্দেশ্য হলো নিশ্চিত করা যে email backend failure চেপে রাখা হচ্ছে না। API view-ই সেই exception ধরে OTP invalid করবে এবং failure log করবে।

Test চালাও:

```
python manage.py test accounts.tests.test_email_service
```

## ৯. API-level failure test কেন প্রয়োজন?

Service test প্রমাণ করে email service exception দেয়। কিন্তু পুরো API সঠিকভাবে OTP invalid করছে কি না, তা আলাদাভাবে পরীক্ষা করা উচিত।

API-level test-এ আমরা এই scenario তৈরি করব:

1. Database-এ active user তৈরি হবে।
2. Email service-কে exception দিতে বাধ্য করব।
3. Forgot Password API call করব।
4. Response-এ generic message আছে কি না দেখব।
5. সর্বশেষ OTP record-এ `invalidated_at` সেট হয়েছে কি না যাচাই করব।

এখানে API-এর URL হবে:

```
POST /api/auth/otp/forgot/
```

আর test-এর মূল assertion হবে:

```
self.assertEqual(response.status_code, 200)record.refresh_from_db()self.assertIsNotNone(record.invalidated_at)
```

সম্পূর্ণ API test লেখার সময় custom user model-এর required field এবং project-এর বিদ্যমান URL configuration অনুযায়ী user তৈরি করবে।

## ১০. সম্পূর্ণ API failure test

এবার যাচাই করি—email ব্যর্থ হলে API কি OTP invalid করছে?

ফাইল: `accounts/tests/test_forgot_password_api.py`

```
from unittest.mock import patchfrom django.contrib.auth import get_user_modelfrom django.test import TestCasefrom django.urls import reversefrom rest_framework.test import APIClientfrom accounts.models import PasswordResetOTPUser = get_user_model()class ForgotPasswordAPITests(TestCase):    def setUp(self):        self.client = APIClient()        self.user = User.objects.create_user(            email="learner@example.com",            password="StrongPass123!",        )        self.url = reverse("forgot-password-otp")    @patch("accounts.views.send_password_reset_otp_email")    def test_email_failure_invalidates_otp(        self,        mocked_send_email,    ):        mocked_send_email.side_effect = OSError(            "Simulated SMTP failure"        )        response = self.client.post(            self.url,            {"email": self.user.email},            format="json",        )        self.assertEqual(response.status_code, 200)        record = PasswordResetOTP.objects.filter(            user=self.user,        ).latest("created_at")        self.assertIsNotNone(record.invalidated_at)        mocked_send_email.assert_called_once()
```

চালাও:

```
python manage.py test accounts.tests
```

Test pass করলে কী বুঝবে?

- API request গ্রহণ করছে।
- OTP record তৈরি হচ্ছে।
- Email service failure হলেও API generic response দিচ্ছে।
- তৈরি হওয়া OTP record invalid করা হচ্ছে।

এই test-এ development-এর console বা বাস্তব SMTP server-এ email পাঠানো হবে না। Mock দিয়ে email failure তৈরি করা হচ্ছে।

## ১১. Production-এ যাওয়ার আগে আরও যা বিবেচনা করবে

| বিষয়               | কী করতে হবে                                                  |
| ------------------ | ------------------------------------------------------------ |
| Request abuse      | IP ও account-ভিত্তিক rate limit এবং resend cooldown          |
| OTP verification   | Expiry, invalidation, attempt limit ও single-use enforcement |
| Email delivery     | Provider logs এবং bounce/delivery status, প্রয়োজন হলে        |
| Logging            | OTP, password, email credentials বা secret log না করা        |
| Database cleanup   | মেয়াদোত্তীর্ণ OTP record পর্যায়ক্রমে পরিষ্কার করা            |
| Concurrency        | একই user-এর একাধিক OTP request-এর race condition নিয়ন্ত্রণ   |
| Long-running email | উচ্চ traffic-এ background task queue বিবেচনা করা             |

Email পাঠানো যদি request-এর মধ্যে দীর্ঘ সময় নেয়, ভবিষ্যতে Celery ও Redis দিয়ে background email delivery করা যায়। তবে তখন task queue ব্যর্থ হওয়া, retry এবং OTP expiry-এর সঙ্গে task timing-এর সম্পর্কও design করতে হবে।

## ১২. Lesson 11 checklist

তোমার progress

0/6

Email service-এ HTML ও plain-text template যুক্ত করেছি

Email backend failure হলে exception propagate হচ্ছে

Forgot Password API-তে failed OTP invalid হচ্ছে

Locmem backend দিয়ে email service test করেছি

Email failure mock করে automated test চালিয়েছি

OTP বা secret log না করার বিষয়টি যাচাই করেছি

## ১৩. নিজের বোঝাপড়া যাচাই করো

1\. `fail_silently=False` কেন ব্যবহার করি?

Email ব্যর্থ হলেও exception লুকিয়ে রাখার জন্য

Email backend-এর exception ধরতে পারার জন্য

OTP-এর মেয়াদ বাড়ানোর জন্য

2\. `EmailMultiAlternatives` ব্যবহারের সুবিধা কী?

একই email-এ HTML ও plain-text version পাঠানো যায়

Database migration প্রয়োজন হয় না

OTP স্বয়ংক্রিয়ভাবে verify হয়

3\. Email backend failure হলে কী করা উচিত?

OTP-কে সব অবস্থায় ব্যবহারযোগ্য রাখা

Plaintext OTP database-এ save করা

ব্যর্থতা log করা এবং ওই OTP invalid করা

উত্তর যাচাই করো

পরবর্তী লেসন: Lesson 12 — Verify OTP API। সেখানে ব্যবহারকারীর OTP input validate করব, stored HMAC verifier-এর সঙ্গে নিরাপদে তুলনা করব, expiry ও attempt limit পরীক্ষা করব এবং সফল verification-এর পর পরবর্তী password reset ধাপের জন্য কীভাবে state পরিচালনা করা যায় তা শিখব।

---
# Lesson 12 — Verify OTP API

এই লেসনে আমরা Django REST Framework দিয়ে এমন একটি API তৈরি করব, যেখানে ব্যবহারকারী ইমেইলে পাওয়া ৬ অঙ্কের OTP submit করলে server সেটি যাচাই করবে। OTP সঠিক, মেয়াদোত্তীর্ণ নয় এবং আগে ব্যবহার করা হয়নি—এগুলো নিশ্চিত করার পরই verification সফল হবে।

আজকের implementation-এ আমরা আগের lessons-এর `PasswordResetOTP` model, HMAC verifier এবং `ForgotPasswordAPIView` ব্যবহার করব।

## ১. আজকের API flow

Frontend

Email + 6-digit OTP submit করে

`POST /api/auth/otp/verify/`

Serializer দিয়ে input validation

Database lookup

সর্বশেষ active OTP record খোঁজা

Security checks

Expiry, invalidation, attempt limit এবং HMAC comparison

সঠিক OTP

পরবর্তী password-reset ধাপের জন্য verification grant তৈরি হবে।

ভুল OTP

Attempt count বাড়বে; সীমা ছাড়ালে OTP invalid হবে।

একটি গুরুত্বপূর্ণ design decision: শুধু OTP সঠিক হলেই `is_used=True` করে দিলে সমস্যা হতে পারে—তাহলে পরবর্তী Lesson 13–14-এ password reset API কীভাবে একই verification ব্যবহার করবে? আবার OTP-কে বারবার ব্যবহারযোগ্য রাখাও নিরাপদ নয়।

তাই আমরা OTP যাচাই সফল হলে একটি স্বল্পমেয়াদি, একবার ব্যবহারযোগ্য reset grant তৈরি করব। এই লেসনে OTP record-টিকে consumed হিসেবে চিহ্নিত করব; পরের ধাপে grant ব্যবহার করে password reset হবে। এটি OTP ও password-reset authorization-কে আলাদা রাখে।

## ২. Verify OTP Serializer তৈরি করো

ফাইল: `accounts/serializers.py`

আগের `ForgotPasswordSerializer` মুছবে না। তার নিচে নতুন serializer যোগ করো:

```
from rest_framework import serializersclass VerifyOTPSerializer(serializers.Serializer):    email = serializers.EmailField(        required=True,        max_length=254,        trim_whitespace=True,        write_only=True,    )    otp = serializers.CharField(        required=True,        min_length=6,        max_length=6,        trim_whitespace=True,        write_only=True,    )    def validate_otp(self, value):        if not value.isascii() or not value.isdigit():            raise serializers.ValidationError(                "Enter a valid 6-digit OTP."            )        return value
```

### কেন `CharField`, `IntegerField` নয়?

OTP হলো identifier-এর মতো একটি code, গণনার সংখ্যা নয়। যেমন OTP `004281` হলে integer হিসেবে এটি `4281` হয়ে যাবে। `CharField` দিয়ে leading zero অক্ষুণ্ণ থাকে।

`validate_otp()` নিশ্চিত করে যে OTP-তে ঠিক ছয়টি ASCII digit আছে। তবে এখানে OTP সঠিক কি না যাচাই হচ্ছে না—সেটি service layer-এর কাজ।

## ৩. Reset grant-এর database model তৈরি করো

OTP সফলভাবে verify হওয়ার পর password reset করার অনুমতি দিতে একটি random token দরকার। আমরা এটিকে `PasswordResetGrant` বলব।

ফাইল: `accounts/models.py`

আগের `User` এবং `PasswordResetOTP` model রেখে নিচের model যোগ করো:

```
class PasswordResetGrant(models.Model):    user = models.ForeignKey(        settings.AUTH_USER_MODEL,        on_delete=models.CASCADE,        related_name="password_reset_grants",    )    token_hash = models.CharField(max_length=64, unique=True)    expires_at = models.DateTimeField()    is_used = models.BooleanField(default=False)    created_at = models.DateTimeField(auto_now_add=True)    class Meta:        indexes = [            models.Index(                fields=["user", "is_used"],                name="pwdgrant_user_used_idx",            ),            models.Index(                fields=["expires_at"],                name="pwdgrant_expires_idx",            ),        ]    def __str__(self):        return f"PasswordResetGrant(user_id={self.user_id}, id={self.pk})"
```

`accounts/models.py`-এর শুরুতে `settings` import না থাকলে যোগ করো:

```
from django.conf import settings
```

এখন migration চালাও:

```
python manage.py makemigrations accounts
python manage.py migrate
python manage.py check
```

### `PasswordResetGrant` কেন প্রয়োজন?

- `token_hash` — reset token-এর hash রাখে, plaintext token নয়।
- `expires_at` — grant-এর মেয়াদ শেষ হওয়ার সময়।
- `is_used` — সফল password reset-এর পর grant আবার ব্যবহার করা আটকাতে কাজে লাগবে।

Grant token-এর জন্য আমরা cryptographically secure random token ব্যবহার করব। এটি ছয় অঙ্কের OTP থেকে আলাদা এবং যথেষ্ট দীর্ঘ হবে।

## ৪. OTP verification service তৈরি করো

ফাইল: `accounts/services/verification_service.py`

```
import hashlibimport secretsfrom datetime import timedeltafrom django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetGrant, PasswordResetOTPfrom accounts.services.otp_service import verify_otp_valueMAX_OTP_ATTEMPTS = 5GRANT_EXPIRY_MINUTES = 10def verify_otp_and_create_grant(user, submitted_otp):    """    Verify the newest eligible OTP.    On success, consume the OTP and return a one-time reset token.    On failure, return None.    """    with transaction.atomic():        now = timezone.now()        otp_record = (            PasswordResetOTP.objects            .select_for_update()            .filter(                user=user,                is_used=False,                invalidated_at__isnull=True,            )            .order_by("-created_at")            .first()        )        if otp_record is None:            return None        if otp_record.expires_at <= now:            otp_record.invalidated_at = now            otp_record.save(                update_fields=["invalidated_at", "updated_at"]            )            return None        if otp_record.attempts >= MAX_OTP_ATTEMPTS:            otp_record.invalidated_at = now            otp_record.save(                update_fields=["invalidated_at", "updated_at"]            )            return None        if not verify_otp_value(            submitted_otp,            otp_record.otp_verifier,        ):            otp_record.attempts += 1            if otp_record.attempts >= MAX_OTP_ATTEMPTS:                otp_record.invalidated_at = now            otp_record.save(                update_fields=[                    "attempts",                    "invalidated_at",                    "updated_at",                ]            )            return None        # Consume the OTP so it cannot be verified again.        otp_record.is_used = True        otp_record.used_at = now        otp_record.save(            update_fields=["is_used", "used_at", "updated_at"]        )        # Invalidate older outstanding grants for this user.        PasswordResetGrant.objects.filter(            user=user,            is_used=False,        ).update(is_used=True)        # Create a strong, short-lived reset token.        raw_token = secrets.token_urlsafe(32)        token_hash = hashlib.sha256(            raw_token.encode("utf-8")        ).hexdigest()        PasswordResetGrant.objects.create(            user=user,            token_hash=token_hash,            expires_at=now + timedelta(                minutes=GRANT_EXPIRY_MINUTES            ),        )        return raw_token
```

### এই service কীভাবে কাজ করে?

1. `transaction.atomic()` OTP যাচাই ও grant তৈরিকে একটি database transaction-এর মধ্যে রাখে।
2. `select_for_update()` সমর্থিত database-এ একই OTP-তে concurrent verification নিয়ন্ত্রণে সাহায্য করে।
3. Expired বা invalidated OTP গ্রহণ করা হয় না।
4. ভুল OTP-তে `attempts` বাড়ে; পাঁচটি ভুল চেষ্টার পর OTP invalid হয়।
5. সঠিক OTP-কে `is_used=True` করা হয়।
6. ১০ মিনিটের জন্য একটি random reset token তৈরি হয়; database-এ শুধু তার SHA-256 hash রাখা হয়।

এখানে OTP-এর জন্য HMAC ব্যবহার করছি, কারণ OTP-তে মাত্র দশ লক্ষ সম্ভাব্য ছয় অঙ্কের মান থাকে। Grant token অনেক বেশি entropy-র random value, তাই তার hash-কে সরাসরি database-এ রেখে plaintext token সংরক্ষণ না করাই যথেষ্ট।

Database note: `select_for_update()` PostgreSQL-এর মতো database-এ কার্যকর row locking দেয়। SQLite-এ একই concurrency guarantee ধরে নেওয়া যাবে না।

## ৫. Verify OTP API View তৈরি করো

ফাইল: `accounts/views.py`

আগের `ForgotPasswordAPIView` মুছবে না। প্রয়োজনীয় import যোগ করো:

```
from rest_framework.exceptions import ValidationErrorfrom accounts.serializers import VerifyOTPSerializerfrom accounts.services.verification_service import (    verify_otp_and_create_grant,)
```

তারপর একই ফাইলে নিচের view যোগ করো:

```
class VerifyOTPAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "verify_otp"    def post(self, request):        serializer = VerifyOTPSerializer(data=request.data)        serializer.is_valid(raise_exception=True)        email = serializer.validated_data["email"]        otp = serializer.validated_data["otp"]        user = User.objects.filter(            email__iexact=email,            is_active=True,        ).first()        if user is None:            raise ValidationError({                "detail": "Invalid or expired verification code."            })        reset_token = verify_otp_and_create_grant(            user=user,            submitted_otp=otp,        )        if reset_token is None:            raise ValidationError({                "detail": "Invalid or expired verification code."            })        return Response(            {                "detail": "OTP verified successfully.",                "reset_token": reset_token,                "expires_in": 600,            },            status=status.HTTP_200_OK,        )
```

`ValidationError` ব্যবহার করলে DRF সাধারণত `400 Bad Request` response দেবে।

### সফল response কেমন হবে?

```
{
  "detail": "OTP verified successfully.",
  "reset_token": "একটি-দীর্ঘ-random-token",
  "expires_in": 600
}
```

এখানে `reset_token`-এর জায়গায় বাস্তবে random token থাকবে। এটি শুধু উদাহরণ।

ব্যর্থ OTP, expired OTP এবং account না পাওয়া—এসব ক্ষেত্রে একই error message দেওয়া হচ্ছে, যাতে error response থেকে অপ্রয়োজনীয় account তথ্য প্রকাশ না পায়।

## ৬. URL যুক্ত করো

ফাইল: `accounts/urls.py`

```
from django.urls import pathfrom accounts.views import (    ForgotPasswordAPIView,    VerifyOTPAPIView,)urlpatterns = [    path(        "otp/forgot/",        ForgotPasswordAPIView.as_view(),        name="forgot-password-otp",    ),    path(        "otp/verify/",        VerifyOTPAPIView.as_view(),        name="verify-password-reset-otp",    ),]
```

এখন endpoint:

`POST /api/auth/otp/verify/`

Request body:

```
{
  "email": "learner@example.com",
  "otp": "004281"
}
```

OTP string হিসেবে পাঠাবে—integer হিসেবে নয়।

## ৭. Verify API-এর throttle configure করো

`config/settings.py`-এ আগের `DEFAULT_THROTTLE_RATES`-এর মধ্যে নতুন scope যোগ করো:

```
REST_FRAMEWORK = {    # তোমার আগের authentication ও permission settings রাখবে।    "DEFAULT_THROTTLE_RATES": {        "forgot_password": "5/hour",        "verify_otp": "10/hour",    },}
```

যদি আগে থেকেই এই dictionary-তে অন্য settings থাকে, সেগুলো রেখে শুধু নতুন rate যোগ করবে।

এই throttle একটি প্রাথমিক IP-ভিত্তিক সীমা। OTP attempt limit আলাদা করে database-এ রাখা হচ্ছে। Production-এ shared cache, account-ভিত্তিক rate limit এবং distributed abuse protection-ও দরকার হতে পারে।

## ৮. API পরীক্ষা করো

প্রথমে server চালাও:

```
python manage.py check
python manage.py runserver
```

### Test A: সঠিক OTP

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/verify/ \
  -H "Content-Type: application/json" \
  -d '{"email":"learner@example.com","otp":"004281"}'
```

এখানে `004281`-এর জায়গায় email-এ পাওয়া প্রকৃত OTP ব্যবহার করবে।

সফল হলে `200 OK` এবং `reset_token` পাবে।

### Test B: ভুল OTP

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/verify/ \
  -H "Content-Type: application/json" \
  -d '{"email":"learner@example.com","otp":"111111"}'
```

সঠিক OTP আগে ব্যবহার না করে থাকলে, ভুল OTP-তে `400 Bad Request` পাওয়ার কথা।

### Test C: Attempt count পরীক্ষা

```
python manage.py shell
```

তারপর:

```
from accounts.models import PasswordResetOTPPasswordResetOTP.objects.order_by(    "-created_at").values(    "attempts",    "is_used",    "expires_at",    "invalidated_at",).first()
```

একই OTP-তে ভুল verification করলে `attempts` বাড়বে। পাঁচটি ভুল চেষ্টার পর record invalid হওয়ার কথা।

মনে রাখবে: `004281` কেবল উদাহরণ। নিজের email-এ পাওয়া OTP ব্যবহার করবে। Console backend থাকলে OTP development terminal-এ দেখা যাবে।

## ৯. Automated test যোগ করো

ফাইল: `accounts/tests/test_verification_service.py`

```
import hashlibfrom datetime import timedeltafrom django.contrib.auth import get_user_modelfrom django.test import TestCasefrom django.utils import timezonefrom accounts.models import PasswordResetGrant, PasswordResetOTPfrom accounts.services.otp_service import get_otp_verifierfrom accounts.services.verification_service import (    verify_otp_and_create_grant,)User = get_user_model()class VerifyOTPServiceTests(TestCase):    def setUp(self):        self.user = User.objects.create_user(            email="learner@example.com",            password="StrongPass123!",        )        self.otp = "004281"        self.record = PasswordResetOTP.objects.create(            user=self.user,            otp_verifier=get_otp_verifier(self.otp),            expires_at=timezone.now() + timedelta(minutes=5),        )    def test_correct_otp_creates_reset_grant(self):        token = verify_otp_and_create_grant(            self.user,            self.otp,        )        self.assertIsNotNone(token)        self.record.refresh_from_db()        self.assertTrue(self.record.is_used)        token_hash = hashlib.sha256(            token.encode("utf-8")        ).hexdigest()        grant = PasswordResetGrant.objects.get(            token_hash=token_hash,            user=self.user,        )        self.assertFalse(grant.is_used)        self.assertGreater(grant.expires_at, timezone.now())    def test_wrong_otp_increments_attempts(self):        token = verify_otp_and_create_grant(            self.user,            "111111",        )        self.assertIsNone(token)        self.record.refresh_from_db()        self.assertEqual(self.record.attempts, 1)        self.assertFalse(self.record.is_used)    def test_expired_otp_is_invalidated(self):        self.record.expires_at = timezone.now() - timedelta(seconds=1)        self.record.save(update_fields=["expires_at"])        token = verify_otp_and_create_grant(            self.user,            self.otp,        )        self.assertIsNone(token)        self.record.refresh_from_db()        self.assertIsNotNone(self.record.invalidated_at)
```

Test চালাও:

```
python manage.py test accounts.tests.test_verification_service
```

এই test-গুলো যথাক্রমে সঠিক OTP, ভুল OTP এবং expired OTP যাচাই করে।

## ১০. Security review — production-এর আগে

এই lesson-এর code শেখার উপযোগী ভিত্তি, তবে production-ready করতে আরও কিছু বিষয় নিশ্চিত করতে হবে:

- Grant verification: পরবর্তী reset API-তে token-এর SHA-256 hash দিয়ে grant খুঁজতে হবে, মেয়াদ ও `is_used` যাচাই করতে হবে এবং সফল password reset-এর সময় grant-কে atomic transaction-এর মধ্যে consume করতে হবে।
- Single use: একটি OTP দ্বিতীয়বার verify করা যাবে না; grant-ও একবারের বেশি ব্যবহার করা যাবে না।
- Concurrent requests: একই OTP দিয়ে দুটি request একসঙ্গে এলে একটিমাত্র request যেন grant তৈরি করতে পারে, সেটি বাস্তব database-এ integration test করতে হবে।
- Rate limiting: IP ও user/account-ভিত্তিক সীমা, resend cooldown এবং monitoring যুক্ত করতে হবে।
- Token handling: Reset token কেবল HTTPS-এ ফেরত দেবে; frontend-এ অপ্রয়োজনীয়ভাবে URL, analytics, logs বা persistent browser storage-এ রাখবে না।
- Database constraints: একই সময়ে একাধিক active OTP বা grant তৈরির policy নির্ধারণ করে database ও service layer—দুই জায়গায়ই enforce করতে হবে।

বিশেষ করে, `select_for_update()` ব্যবহার করলেই সব database-এ একই concurrency guarantee পাওয়া যায় না। Production-এর PostgreSQL-এ transaction ও locking behaviour পরীক্ষা করবে।

## ১১. Lesson 12 checklist

Lesson progress

0/7

VerifyOTPSerializer তৈরি করেছি

PasswordResetGrant model migrate করেছি

OTP expiry এবং attempt limit যাচাই করেছি

সঠিক OTP-তে reset token তৈরি হচ্ছে

ভুল OTP-তে attempt count বাড়ছে

Expired OTP invalid হচ্ছে

Automated test চালিয়ে ফল যাচাই করেছি

পরবর্তী লেসন — Lesson 13: Reset Password Serializer। সেখানে নতুন password ও confirm password validate করব, password policy প্রয়োগ করব এবং reset token গ্রহণের জন্য request structure তৈরি করব। তারপর Lesson 14-এ `PasswordResetGrant` ব্যবহার করে নিরাপদে password পরিবর্তন সম্পন্ন করব।

---
# Lesson 13 — Reset Password Serializer

এই লেসনে আমরা Django REST Framework-এ এমন একটি Serializer তৈরি করব, যেটি OTP verify করার পর পাওয়া `reset_token`, নতুন password এবং confirm password validate করবে।

আমাদের লক্ষ্য হলো, শুধু valid reset token থাকলে এবং দুইটি password মিলে গেলেই পরবর্তী API password পরিবর্তনের অনুমতি দিতে পারবে।

## ১. সম্পূর্ণ Password Reset Flow

Lesson 10 — Forgot Password

ইমেইলে OTP পাঠানো

Lesson 12 — Verify OTP

সঠিক OTP দিলে স্বল্পমেয়াদি reset token পাওয়া

Lesson 13 — Reset Password Serializer

Token ও password validation

Lesson 14 — Reset Password API

Token যাচাই করে নতুন password save করা

আজকের গুরুত্বপূর্ণ পার্থক্য:

- Serializer: Request data সঠিক কি না যাচাই করবে।
- Service/API View: Reset token সত্যিই valid কি না যাচাই করে password পরিবর্তনের কাজ করবে।

Password পরিবর্তনের মতো গুরুত্বপূর্ণ কাজ শুধু Serializer-এর validation-এর ওপর ছেড়ে দেব না।

## ২. Request body কেমন হবে?

Lesson 14-এ আমাদের API-তে এমন request পাঠানো হবে:

```
{
  "reset_token": "your-long-reset-token",
  "new_password": "A-Strong-Password-123!",
  "confirm_password": "A-Strong-Password-123!"
}
```

এখানে `your-long-reset-token` একটি উদাহরণ। বাস্তবে Lesson 12-এর Verify OTP API থেকে পাওয়া token ব্যবহার করতে হবে।

প্রতিটি field-এর উদ্দেশ্য:

| Field              | উদ্দেশ্য                                              |
| ------------------ | ----------------------------------------------------- |
| `reset_token`      | OTP verification সফল হওয়ার পর পাওয়া অনুমতিপত্র        |
| `new_password`     | ব্যবহারকারীর নতুন password                            |
| `confirm_password` | নতুন password-টি ঠিকভাবে লেখা হয়েছে কি না নিশ্চিত করা |

Password এবং reset token কখনো URL query parameter-এ পাঠাবে না। HTTPS ব্যবহার করবে এবং request body-তে পাঠাবে।

## ৩. Password Reset Serializer তৈরি করো

ফাইল: `accounts/serializers.py`

আগের `ForgotPasswordSerializer` এবং `VerifyOTPSerializer` মুছবে না। ফাইলের import-এ নিচের দুটি import যোগ করো:

```
from django.contrib.auth.password_validation import validate_passwordfrom django.core.exceptions import ValidationError as DjangoValidationErrorfrom rest_framework import serializers
```

তারপর নতুন Serializer যোগ করো:

```
class ResetPasswordSerializer(serializers.Serializer):    reset_token = serializers.CharField(        required=True,        max_length=256,        trim_whitespace=False,        write_only=True,    )    new_password = serializers.CharField(        required=True,        write_only=True,        trim_whitespace=False,        style={"input_type": "password"},    )    confirm_password = serializers.CharField(        required=True,        write_only=True,        trim_whitespace=False,        style={"input_type": "password"},    )    def validate_reset_token(self, value):        if not value or value.strip() != value:            raise serializers.ValidationError(                "Enter a valid reset token."            )        return value    def validate_new_password(self, value):        try:            validate_password(value)        except DjangoValidationError as exc:            raise serializers.ValidationError(                list(exc.messages)            )        return value    def validate(self, attrs):        if attrs["new_password"] != attrs["confirm_password"]:            raise serializers.ValidationError({                "confirm_password": "Passwords do not match."            })        return attrs
```

### প্রতিটি অংশ বুঝে নাও

`write_only=True`

API response-এ password বা reset token ফেরত না দেওয়ার জন্য। এই field-গুলো request input হিসেবে ব্যবহৃত হবে।

`trim_whitespace=False`

Password-এর শুরু বা শেষে থাকা space স্বয়ংক্রিয়ভাবে বাদ দেওয়া হবে না। Password-এর ক্ষেত্রে নীরবে input বদলে দেওয়া ঠিক নয়।

`validate_password(value)`

Django-এর configured password validators চালায়। যেমন, `settings.py`-তে `AUTH_PASSWORD_VALIDATORS`-এর মাধ্যমে minimum length এবং common password checks configure করা থাকতে পারে।

`validate_new_password()`

শুধু নতুন password-এর নিয়ম যাচাই করে। Password policy ব্যর্থ হলে error ফেরত দেয়।

`validate()`

এখানে একাধিক field একসঙ্গে যাচাই করা হয়। `new_password` ও `confirm_password` এক কি না, সেটি নিশ্চিত করে।

`validate_reset_token()`

Token-এর input format-এ অস্বাভাবিক whitespace আছে কি না পরীক্ষা করে। কিন্তু token database-এ আছে কি না, মেয়াদ শেষ হয়েছে কি না, অথবা ব্যবহার করা হয়েছে কি না—এই Serializer তা নিশ্চিত করে না। সেগুলো Lesson 14-এর API/service-এর দায়িত্ব।

## ৪. Django password validators configure করো

ফাইল: `config/settings.py`

`AUTH_PASSWORD_VALIDATORS`-এ সাধারণত Django-এর default validators থাকে। নিশ্চিত করো অন্তত এই ধরনের validation configured আছে:

```
AUTH_PASSWORD_VALIDATORS = [    {        "NAME": (            "django.contrib.auth.password_validation."            "UserAttributeSimilarityValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "MinimumLengthValidator"        ),        "OPTIONS": {            "min_length": 12,        },    },    {        "NAME": (            "django.contrib.auth.password_validation."            "CommonPasswordValidator"        ),    },    {        "NAME": (            "django.contrib.auth.password_validation."            "NumericPasswordValidator"        ),    },]
```

যদি তোমার settings-এ আগে থেকেই এই list থাকে, অন্ধভাবে replace না করে বর্তমান configuration যাচাই করবে। `MinimumLengthValidator`-এ `min_length: 12` দিলে password কমপক্ষে ১২ অক্ষরের হতে হবে।

একটি বিষয় খেয়াল করো: Serializer-এ `validate_password(value)` ব্যবহার করার সময় user object দেওয়া হচ্ছে না। তাই `UserAttributeSimilarityValidator`-এর মতো user-specific validator সম্পূর্ণভাবে কাজ নাও করতে পারে। Lesson 14-এ token থেকে user শনাক্ত করার পর password-কে সেই user-এর context দিয়েও validate করব।

## ৫. Serializer নিজে পরীক্ষা করো

Django shell চালাও:

```
python manage.py shell
```

### Test A — দুইটি password মিলে গেলে

```
from accounts.serializers import ResetPasswordSerializerdata = {    "reset_token": "example-long-reset-token",    "new_password": "River!Cloud2026Secure",    "confirm_password": "River!Cloud2026Secure",}serializer = ResetPasswordSerializer(data=data)print(serializer.is_valid())print(serializer.errors)
```

Password তোমার configured validators-এর শর্ত পূরণ করলে `True` পাওয়ার কথা। তবে Django-এর common-password ও similarity validators-এর কারণে ফল ভিন্ন হতে পারে।

### Test B — Password না মিললে

```
data = {    "reset_token": "example-long-reset-token",    "new_password": "River!Cloud2026Secure",    "confirm_password": "Different!Password2026",}serializer = ResetPasswordSerializer(data=data)print(serializer.is_valid())print(serializer.errors)
```

এখানে validation ব্যর্থ হবে এবং `confirm_password`-এর জন্য error দেখাবে।

### Test C — দুর্বল password

```
data = {    "reset_token": "example-long-reset-token",    "new_password": "123",    "confirm_password": "123",}serializer = ResetPasswordSerializer(data=data)print(serializer.is_valid())print(serializer.errors)
```

Configured password policy অনুযায়ী এটি ব্যর্থ হওয়ার কথা।

### Test D — Required field অনুপস্থিত

```
serializer = ResetPasswordSerializer(    data={        "reset_token": "example-long-reset-token",        "new_password": "River!Cloud2026Secure",    })print(serializer.is_valid())print(serializer.errors)
```

`confirm_password` না থাকায় validation ব্যর্থ হবে।

## ৬. Automated tests তৈরি করো

ফাইল: `accounts/tests/test_reset_password_serializer.py`

```
from django.test import TestCasefrom accounts.serializers import ResetPasswordSerializerclass ResetPasswordSerializerTests(TestCase):    def setUp(self):        self.data = {            "reset_token": "example-long-reset-token",            "new_password": "River!Cloud2026Secure",            "confirm_password": "River!Cloud2026Secure",        }    def test_matching_passwords_are_valid(self):        serializer = ResetPasswordSerializer(data=self.data)        self.assertTrue(            serializer.is_valid(),            serializer.errors,        )    def test_mismatched_passwords_are_invalid(self):        data = {            **self.data,            "confirm_password": "Another!Password2026",        }        serializer = ResetPasswordSerializer(data=data)        self.assertFalse(serializer.is_valid())        self.assertIn(            "confirm_password",            serializer.errors,        )    def test_missing_token_is_invalid(self):        data = {            "new_password": "River!Cloud2026Secure",            "confirm_password": "River!Cloud2026Secure",        }        serializer = ResetPasswordSerializer(data=data)        self.assertFalse(serializer.is_valid())        self.assertIn("reset_token", serializer.errors)
```

Test চালাও:

```
python manage.py test accounts.tests.test_reset_password_serializer
```

যদি matching password-এর test ব্যর্থ হয়, তাহলে তোমার `AUTH_PASSWORD_VALIDATORS` configuration পরীক্ষা করো। Validation error message-ই বলে দেবে কোন নিয়ম পূরণ হয়নি।

## ৭. Lesson 13-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়

এই Serializer শুধু request data validate করে। এখনো এটি:

- Reset token-এর hash database-এ খুঁজছে না।
- Token expired বা consumed কি না পরীক্ষা করছে না।
- User-এর password পরিবর্তন করছে না।
- Reset token একবারের বেশি ব্যবহার করা আটকাচ্ছে না।

এগুলো ইচ্ছাকৃতভাবেই পরবর্তী lesson-এর জন্য রাখা হয়েছে।

আরেকটি গুরুত্বপূর্ণ security rule: password পরিবর্তনের সময় `user.password = raw_password` করে সরাসরি save করবে না। Django-এর `user.set_password(raw_password)` ব্যবহার করতে হবে, যাতে password সঠিকভাবে hash হয়।

## ৮. আজকের checklist

Lesson 13 progress

0/6

ResetPasswordSerializer তৈরি করেছি

Reset token, new password ও confirm password field যুক্ত করেছি

Password mismatch validation পরীক্ষা করেছি

Django password validators পরীক্ষা করেছি

Missing field ও weak password test করেছি

Automated tests চালিয়েছি

পরবর্তী লেসন — Lesson 14: Reset Password API View। সেখানে আমরা `PasswordResetGrant` থেকে reset token যাচাই করব, token expiry ও single-use enforcement করব, নতুন password save করব এবং database transaction-এর মধ্যে grant consume করব। ফলে Forgot Password থেকে শুরু করে password পরিবর্তন পর্যন্ত পুরো flow যুক্ত হবে।

---
# Lesson 14 — Reset Password API View

এই লেসনে আমরা Forgot Password workflow-এর সবচেয়ে গুরুত্বপূর্ণ অংশ তৈরি করব: OTP verify করার পর পাওয়া reset token ব্যবহার করে নিরাপদে নতুন password সেট করা।

এখন পর্যন্ত আমাদের তৈরি হয়েছে:

- Lesson 10: Forgot Password API
- Lesson 11: OTP Email Integration ও Failure Handling
- Lesson 12: Verify OTP API এবং `PasswordResetGrant`
- Lesson 13: `ResetPasswordSerializer`

আজ এগুলো একসঙ্গে যুক্ত করব।

## ১. API কীভাবে কাজ করবে?

Frontend request

Reset token + নতুন password + confirm password

ResetPasswordSerializer

Input ও password policy validate করবে

Reset token verification

Token hash, expiry এবং single-use status যাচাই

Database transaction

Password hash save এবং reset grant consume

Password reset successful

আমাদের security rules:

1. Reset token plaintext database-এ রাখা যাবে না।
2. Expired বা আগেই ব্যবহার করা token গ্রহণ করা যাবে না।
3. Password পরিবর্তনের জন্য Django-এর `set_password()` ব্যবহার করতে হবে।
4. Password save এবং grant consume একই database transaction-এ করতে হবে।
5. Reset token দ্বিতীয়বার ব্যবহার করতে দেওয়া যাবে না।

## ২. Reset token দিয়ে grant খুঁজে বের করো

Lesson 12-এ `PasswordResetGrant`-এ আমরা token-এর SHA-256 hash রেখেছি। তাই request-এর plaintext token hash করে database-এর সঙ্গে তুলনা করব।

নতুন ফাইল: `accounts/services/reset_password_service.py`

```
import hashlibfrom django.contrib.auth import get_user_modelfrom django.contrib.auth.password_validation import validate_passwordfrom django.core.exceptions import ValidationError as DjangoValidationErrorfrom django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetGrantUser = get_user_model()class InvalidResetToken(Exception):    """Raised when a reset token is invalid, expired, or already used."""class InvalidNewPassword(Exception):    """Raised when the new password fails validation."""def get_reset_token_hash(raw_token: str) -> str:    return hashlib.sha256(        raw_token.encode("utf-8")    ).hexdigest()
```

এই helper-টি Lesson 12-এর grant তৈরির সময় ব্যবহৃত hash algorithm-এর সঙ্গে মিলতে হবে। একই token-এর hash তৈরির নিয়ম দুই জায়গায় এক হতে হবে।

এখন একই ফাইলে মূল service যোগ করব। তার আগে নিচের গুরুত্বপূর্ণ বিষয়টি বুঝে নাও: Password validation-এ user object ব্যবহার করতে হবে, যাতে Django-এর user-attribute similarity validator-ও কাজ করতে পারে।

## ৩. Password reset service সম্পূর্ণ করো

`accounts/services/reset_password_service.py`-এ নিচের function যোগ করো:

```
def reset_password(*, raw_token: str, new_password: str) -> None:    token_hash = get_reset_token_hash(raw_token)    with transaction.atomic():        # Lock the grant so concurrent requests cannot both use it.        grant = (            PasswordResetGrant.objects            .select_for_update()            .filter(token_hash=token_hash)            .first()        )        now = timezone.now()        if (            grant is None            or grant.is_used            or grant.expires_at <= now        ):            raise InvalidResetToken        # Lock the user row as well.        user = User.objects.select_for_update().get(            pk=grant.user_id        )        if not user.is_active:            raise InvalidResetToken        # Validate against the actual user account.        try:            validate_password(new_password, user=user)        except DjangoValidationError as exc:            raise InvalidNewPassword(                "; ".join(exc.messages)            ) from exc        # Always hash the password through Django.        user.set_password(new_password)        user.save(update_fields=["password"])        # Consume every outstanding grant for this user.        PasswordResetGrant.objects.filter(            user=user,            is_used=False,        ).update(is_used=True)
```

### কীভাবে কাজ করছে?

- `get_reset_token_hash()` request-এর token hash করে।
- `select_for_update()` সমর্থিত database-এ grant row lock করে।
- Grant পাওয়া না গেলে, মেয়াদ শেষ হলে বা আগে ব্যবহার করা হলে reset প্রত্যাখ্যান করে।
- `validate_password(new_password, user=user)` user-specific password validation-ও চালায়।
- `set_password()` password hash করে save করে।
- সব outstanding grant consume করে, যাতে অন্য পুরোনো reset token দিয়েও password পরিবর্তন করা না যায়।

`transaction.atomic()`-এর কারণে password update বা grant consumption-এর মধ্যে database error হলে transaction rollback হবে।

গুরুত্বপূর্ণ: এই locking strategy PostgreSQL-এর মতো row-locking database-এ পরীক্ষা করবে। SQLite-এ একই concurrency guarantee ধরে নেওয়া যাবে না।

## ৪. Reset Password API View তৈরি করো

ফাইল: `accounts/views.py`

আগের import-গুলোর সঙ্গে এগুলো যোগ করো:

```
from rest_framework.exceptions import ValidationErrorfrom accounts.serializers import ResetPasswordSerializerfrom accounts.services.reset_password_service import (    InvalidNewPassword,    InvalidResetToken,    reset_password,)
```

তারপর view যোগ করো:

```
class ResetPasswordAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "reset_password"    def post(self, request):        serializer = ResetPasswordSerializer(            data=request.data        )        serializer.is_valid(raise_exception=True)        reset_token = serializer.validated_data["reset_token"]        new_password = serializer.validated_data["new_password"]        try:            reset_password(                raw_token=reset_token,                new_password=new_password,            )        except InvalidResetToken:            raise ValidationError({                "reset_token": "Invalid or expired reset token."            })        except InvalidNewPassword as exc:            raise ValidationError({                "new_password": str(exc)            })        return Response(            {                "detail": (                    "Password has been reset successfully."                )            },            status=status.HTTP_200_OK,        )
```

এই endpoint-এ `AllowAny` ব্যবহার করছি, কারণ ব্যবহারকারী সাধারণত password ভুলে যাওয়ার পর login করতে পারেন না। তবে এর মানে এই নয় যে যে কেউ password বদলাতে পারবে—একটি valid, unexpired, unused reset token অবশ্যই লাগবে।

## ৫. URL configure করো

ফাইল: `accounts/urls.py`

```
from django.urls import pathfrom accounts.views import (    ForgotPasswordAPIView,    VerifyOTPAPIView,    ResetPasswordAPIView,)urlpatterns = [    path(        "otp/forgot/",        ForgotPasswordAPIView.as_view(),        name="forgot-password-otp",    ),    path(        "otp/verify/",        VerifyOTPAPIView.as_view(),        name="verify-password-reset-otp",    ),    path(        "otp/reset/",        ResetPasswordAPIView.as_view(),        name="reset-password-otp",    ),]
```

Endpoint:

`POST /api/auth/otp/reset/`

এবার `config/settings.py`-এর `DEFAULT_THROTTLE_RATES`-এ এই scope-টিও যোগ করো:

```
"reset_password": "5/hour",
```

আগের `forgot_password` এবং `verify_otp` rates-গুলোও রেখে দেবে।

## ৬. API পরীক্ষা করো

প্রথমে:

```
python manage.py check
python manage.py runserver
```

### Test A — Request format

```
curl -X POST http://127.0.0.1:8000/api/auth/otp/reset/ \
  -H "Content-Type: application/json" \
  -d '{
    "reset_token": "PASTE_YOUR_RESET_TOKEN_HERE",
    "new_password": "River!Cloud2026Secure",
    "confirm_password": "River!Cloud2026Secure"
  }'
```

`PASTE_YOUR_RESET_TOKEN_HERE`-এর জায়গায় Lesson 12-এর Verify OTP API থেকে পাওয়া আসল `reset_token` বসাবে।

সফল হলে:

```
{
  "detail": "Password has been reset successfully."
}
```

Status: `200 OK`

### Test B — Token ভুল হলে

ইচ্ছাকৃতভাবে ভুল token পাঠাও:

```
{
  "reset_token": "invalid-token",
  "new_password": "River!Cloud2026Secure",
  "confirm_password": "River!Cloud2026Secure"
}
```

প্রত্যাশিত ফল: `400 Bad Request` এবং `Invalid or expired reset token.`

### Test C — Password mismatch

```
{
  "reset_token": "your-valid-reset-token",
  "new_password": "River!Cloud2026Secure",
  "confirm_password": "Another!Password2026"
}
```

Serializer `confirm_password`-এর validation error দেবে। এই request-এ password পরিবর্তন হওয়ার কথা নয়।

### Test D — একই token দ্বিতীয়বার ব্যবহার

সফল reset-এর পরে একই token আবার submit করো। এবার token ইতিমধ্যে consumed হওয়ায় request প্রত্যাখ্যাত হবে।

## ৭. Automated test যোগ করো

ফাইল: `accounts/tests/test_reset_password_service.py`

```
import hashlibfrom datetime import timedeltafrom django.contrib.auth import get_user_modelfrom django.test import TestCasefrom django.utils import timezonefrom accounts.models import PasswordResetGrantfrom accounts.services.reset_password_service import (    InvalidResetToken,    reset_password,)User = get_user_model()class ResetPasswordServiceTests(TestCase):    def setUp(self):        self.user = User.objects.create_user(            email="learner@example.com",            password="OldPassword!2026Secure",        )        self.raw_token = "example-reset-token-123456789"        token_hash = hashlib.sha256(            self.raw_token.encode("utf-8")        ).hexdigest()        self.grant = PasswordResetGrant.objects.create(            user=self.user,            token_hash=token_hash,            expires_at=timezone.now() + timedelta(minutes=10),        )    def test_password_is_changed(self):        reset_password(            raw_token=self.raw_token,            new_password="New!Password2026Secure",        )        self.user.refresh_from_db()        self.grant.refresh_from_db()        self.assertTrue(            self.user.check_password("New!Password2026Secure")        )        self.assertFalse(            self.user.check_password("OldPassword!2026Secure")        )        self.assertTrue(self.grant.is_used)    def test_token_cannot_be_reused(self):        reset_password(            raw_token=self.raw_token,            new_password="New!Password2026Secure",        )        with self.assertRaises(InvalidResetToken):            reset_password(                raw_token=self.raw_token,                new_password="Another!Password2026Secure",            )    def test_expired_token_is_rejected(self):        self.grant.expires_at = (            timezone.now() - timedelta(seconds=1)        )        self.grant.save(update_fields=["expires_at"])        with self.assertRaises(InvalidResetToken):            reset_password(                raw_token=self.raw_token,                new_password="New!Password2026Secure",            )
```

চালাও:

```
python manage.py test accounts.tests.test_reset_password_service
```

যদি password validator কোনো test password-কে দুর্বল বলে প্রত্যাখ্যান করে, configured policy অনুযায়ী test password পরিবর্তন করো; validation বন্ধ করে দেবে না।

## ৮. Password reset-এর পর আর কী বিবেচনা করতে হবে?

১. Existing sessions: Django-এর password hash বদলালে পুরোনো Django session সাধারণত পরবর্তী request-এ invalid হয়ে যায়, তবে session handling configuration অনুযায়ী যাচাই করতে হবে।

২. JWT tokens: Password পরিবর্তন করলেই আগে ইস্যু করা সব JWT স্বয়ংক্রিয়ভাবে বাতিল হয় না। তোমার project-এ SimpleJWT ব্যবহার করা হচ্ছে বলে refresh-token revocation, token versioning বা অন্য session-revocation strategy আলাদাভাবে design করতে হবে।

৩. Notification: Password পরিবর্তন সফল হলে ব্যবহারকারীকে security notification email পাঠানো যেতে পারে। তবে notification email ব্যর্থ হওয়ার কারণে ইতিমধ্যে সফল password reset rollback করার চেষ্টা করবে না।

৪. Rate limiting: Forgot, verify এবং reset endpoint—তিনটিতেই throttling রাখবে। Production-এ shared cache এবং account-ভিত্তিক abuse protection পরীক্ষা করবে।

৫. Logging: Password, reset token, OTP বা `.env`-এর secret log করবে না।

## ৯. পুরো flow-এর final checklist

Password reset project progress

0/9

Forgot Password API email-এ OTP পাঠায়

Verify OTP API reset token তৈরি করে

ResetPasswordSerializer input ও password validate করে

Reset Password API token hash যাচাই করে

Expired ও reused token প্রত্যাখ্যাত হয়

set_password() দিয়ে password hash করে save হয়

Database transaction-এ grant consume হয়

Automated tests pass করেছে

JWT revocation strategy নির্ধারণ করেছি

পরবর্তী লেসন — Lesson 15: Resend OTP API। সেখানে নতুন OTP পাঠানো, cooldown, আগের OTP invalid করা এবং বারবার email পাঠিয়ে abuse করার ঝুঁকি নিয়ন্ত্রণ করা শিখব। তার আগে তোমার project-এ Lesson 12 থেকে 14 পর্যন্ত migration, imports এবং automated tests একসঙ্গে ঠিকমতো কাজ করছে কি না যাচাই করে নাও। মনে রেখো, এখানে দেখানো code একটি শিক্ষামূলক ভিত্তি; production deployment-এর আগে concurrency, token revocation এবং abuse protection বাস্তবে পরীক্ষা করা জরুরি।

---
# Lesson 15: Resend OTP API — Django REST Framework

এই লেসনে আমরা আগের Password Reset Flow-এর সঙ্গে Resend OTP API যুক্ত করব। ব্যবহারকারী প্রথম OTP না পেলে বা OTP-এর মেয়াদ শেষ হওয়ার আগে নতুন কোড চাইলে এই API ব্যবহার করতে পারবে।

আমাদের আগের lessons-এর architecture বজায় থাকবে:

- `Serializer` — email input validate করবে।
- `APIView` — HTTP request handle করবে।
- `Service` — OTP তৈরি, cooldown ও পুরোনো OTP invalidate করবে।
- `Email Service` — নতুন OTP ইমেইল করবে।
- `Tests` — cooldown, invalid OTP এবং email failure পরীক্ষা করবে।

## ১. Resend OTP কীভাবে কাজ করবে?

POST `/api/auth/otp/forgot/`

প্রথমবার password reset request

OTP তৈরি ও ইমেইল পাঠানো

OTP-এর মেয়াদ ৫ মিনিট

POST `/api/auth/otp/resend/`

আগের OTP এখনো pending থাকলে নতুন OTP চাইবে

নতুন OTP পাঠানো

পুরোনো OTP invalidate হবে; ৬০ সেকেন্ড cooldown থাকবে

গুরুত্বপূর্ণ নিয়ম: একই OTP বারবার পাঠাব না। নতুন OTP তৈরি হলে আগেরটি আর ব্যবহার করা যাবে না। আর OTP resend করার জন্য আগের password-reset request থাকা প্রয়োজন; না থাকলে ব্যবহারকারীকে প্রথমে `forgot` endpoint ব্যবহার করতে হবে।

## ২. নতুন ফাইল তৈরি করো

আমাদের project structure-এ একটি service file যোগ হবে:

```
accounts/
├── serializers.py
├── views.py
├── urls.py
├── services/
│   ├── otp_service.py
│   ├── password_reset_service.py
│   ├── email_service.py
│   └── resend_otp_service.py   # নতুন
└── tests/
```

এখানে `PasswordResetOTP` model এবং আগের `generate_otp()`, `get_otp_expiry()`, `get_otp_verifier()` functions পুনরায় ব্যবহার করব।

## ৩. Resend OTP Serializer

`accounts/serializers.py`-এ নিচের serializer যোগ করো। আগের `ForgotPasswordSerializer` থাকলে সেটি পরিবর্তন করার প্রয়োজন নেই।

```
# accounts/serializers.pyfrom rest_framework import serializersclass ResendOTPSerializer(serializers.Serializer):    email = serializers.EmailField(        required=True,        max_length=254,        trim_whitespace=True,        write_only=True,    )
```

কেন শুধু email নিচ্ছি? কারণ সার্ভার নিজেই সর্বশেষ OTP request, তার expiry এবং resend cooldown যাচাই করবে। Client থেকে `user_id`, `otp`, বা `expires_at` গ্রহণ করার দরকার নেই।

## ৪. Resend OTP Service তৈরি করো

নতুন ফাইল `accounts/services/resend_otp_service.py` তৈরি করো।

```
# accounts/services/resend_otp_service.pyfrom datetime import timedeltafrom django.db import transactionfrom django.utils import timezonefrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import (    generate_otp,    get_otp_expiry,    get_otp_verifier,)RESEND_COOLDOWN_SECONDS = 60def create_resend_otp(user):    """    Create a new OTP only when a valid, unused OTP    already exists and the resend cooldown has passed.    Returns:        (record, raw_otp, status)    """    with transaction.atomic():        # Concurrent resend requests যেন একই user-এর জন্য        # একসঙ্গে cooldown পার হতে না পারে।        user_model = type(user)        locked_user = user_model.objects.select_for_update().get(            pk=user.pk        )        now = timezone.now()        latest_otp = (            PasswordResetOTP.objects            .filter(user=locked_user)            .order_by("-created_at", "-pk")            .first()        )        # প্রথমে forgot-password request করতে হবে।        if latest_otp is None:            return None, None, "no_pending_otp"        # ব্যবহৃত, invalidated অথবা expired OTP resend-এর        # জন্য বৈধ pending request নয়।        if (            latest_otp.is_used            or latest_otp.invalidated_at is not None            or latest_otp.expires_at <= now        ):            return None, None, "no_pending_otp"        cooldown_ends_at = (            latest_otp.created_at            + timedelta(seconds=RESEND_COOLDOWN_SECONDS)        )        if now < cooldown_ends_at:            return None, None, "cooldown"        # আগের সব unused OTP invalidate করো।        PasswordResetOTP.objects.filter(            user=locked_user,            is_used=False,            invalidated_at__isnull=True,        ).update(invalidated_at=now)        # নতুন OTP তৈরি করো।        raw_otp = generate_otp()        record = PasswordResetOTP.objects.create(            user=locked_user,            otp_verifier=get_otp_verifier(raw_otp),            expires_at=get_otp_expiry(),        )    # Database transaction শেষ হওয়ার পর raw OTP return হবে।    # Email পাঠানোর কাজ view থেকে transaction-এর বাইরে হবে।    return record, raw_otp, "created"
```

### Service-এর গুরুত্বপূর্ণ অংশগুলো বুঝে নাও

`select_for_update()` একই user-এর resend request-গুলোর মধ্যে race condition কমাতে সাহায্য করে। PostgreSQL-এর মতো database-এ এটি কার্যকর row lock দেয়; SQLite-এ একই locking guarantee নেই।

Cooldown এখানে ৬০ সেকেন্ড। অর্থাৎ নতুন OTP তৈরির পর পরবর্তী ৬০ সেকেন্ডে আরেকটি resend request নতুন OTP তৈরি করতে পারবে না।

OTP expiry পাঁচ মিনিটই থাকবে। Cooldown শেষ হলেই OTP অবশ্যই resend হবে এমন নয়—আগের OTP তখনো pending ও unexpired থাকতে হবে।

Raw OTP database-এ রাখা হচ্ছে না। আগের lesson-এর মতো শুধু HMAC verifier সংরক্ষণ করছি।

## ৫. Resend OTP API View তৈরি করো

`accounts/views.py`-এ আগের imports ও views রেখে নিচের প্রয়োজনীয় imports এবং class যোগ করো।

```
# accounts/views.pyimport loggingfrom django.contrib.auth import get_user_modelfrom django.utils import timezonefrom rest_framework import statusfrom rest_framework.permissions import AllowAnyfrom rest_framework.response import Responsefrom rest_framework.throttling import ScopedRateThrottlefrom rest_framework.views import APIViewfrom accounts.models import PasswordResetOTPfrom accounts.serializers import ResendOTPSerializerfrom accounts.services.email_service import (    send_password_reset_otp_email,)from accounts.services.resend_otp_service import (    create_resend_otp,)User = get_user_model()logger = logging.getLogger(__name__)class ResendOTPAPIView(APIView):    permission_classes = [AllowAny]    throttle_classes = [ScopedRateThrottle]    throttle_scope = "resend_otp"    def post(self, request):        serializer = ResendOTPSerializer(data=request.data)        serializer.is_valid(raise_exception=True)        email = serializer.validated_data["email"]        # Email account আছে কি না, response দিয়ে প্রকাশ করা হবে না।        user = User.objects.filter(            email__iexact=email,            is_active=True,        ).first()        if user is not None:            record, otp, result = create_resend_otp(user)            if result == "created":                try:                    sent = send_password_reset_otp_email(                        recipient_email=user.email,                        otp=otp,                        expiry_minutes=5,                    )                    if not sent:                        raise RuntimeError(                            "Email backend did not accept the message."                        )                except Exception:                    # Email ব্যর্থ হলে তৈরি করা OTP-টিও                    # আর ব্যবহারযোগ্য রাখা হবে না।                    PasswordResetOTP.objects.filter(                        pk=record.pk,                        is_used=False,                        invalidated_at__isnull=True,                    ).update(invalidated_at=timezone.now())                    logger.exception(                        "Failed to send password-reset OTP."                    )        return Response(            {                "detail": (                    "If an eligible password reset request exists, "                    "a new verification code will be sent."                )            },            status=status.HTTP_200_OK,        )
```

### এখানে generic response কেন?

ধরো, কেউ অন্য ব্যক্তির email দিয়ে request করল। API যদি বলে, “এই email-এর কোনো account নেই,” তাহলে সে বুঝতে পারবে ওই email দিয়ে account তৈরি করা হয়েছে কি না।

তাই তিনটি অবস্থাতেই—account নেই, pending OTP নেই, অথবা cooldown চলছে—একই success response দেব।

> মনে রাখবে: `200 OK` মানে email পাঠানো নিশ্চিত নয়। এটি শুধু বোঝায় API একটি generic response দিয়েছে। Email delivery-এর প্রকৃত অবস্থা আলাদা বিষয়।

## ৬. URL যোগ করো

`accounts/urls.py`-এ নতুন view import করে URL যোগ করো। আগের URL-গুলো মুছবে না।

```
from django.urls import pathfrom accounts.views import (    ForgotPasswordAPIView,    VerifyOTPAPIView,    ResetPasswordAPIView,    ResendOTPAPIView,)urlpatterns = [    path(        "otp/forgot/",        ForgotPasswordAPIView.as_view(),        name="forgot-password-otp",    ),    path(        "otp/verify/",        VerifyOTPAPIView.as_view(),        name="verify-password-reset-otp",    ),    path(        "otp/reset/",        ResetPasswordAPIView.as_view(),        name="reset-password-otp",    ),    path(        "otp/resend/",        ResendOTPAPIView.as_view(),        name="resend-password-reset-otp",    ),]
```

যেহেতু `config/urls.py`-এ আগে থেকেই `accounts.urls`-কে `api/auth/` prefix-এর অধীনে include করা আছে, নতুন endpoint হবে:

`POST /api/auth/otp/resend/`

## ৭. DRF rate limit যোগ করো

`config/settings.py`-এর বিদ্যমান `REST_FRAMEWORK` dictionary-তে `DEFAULT_THROTTLE_RATES` থাকলে তার মধ্যে এই entry যোগ করো:

```
REST_FRAMEWORK = {    # তোমার বিদ্যমান authentication, permission    # এবং অন্যান্য settings এখানেই রাখতে হবে।    "DEFAULT_THROTTLE_RATES": {        # বিদ্যমান rate-গুলোও এখানে রাখতে হবে।        "forgot_password": "5/hour",        "verify_otp": "10/hour",        "reset_password": "5/hour",        "resend_otp": "5/hour",    },}
```

এটি তোমার পুরো `REST_FRAMEWORK` configuration-এর বিকল্প নয়—বিদ্যমান dictionary-এর সঙ্গে merge করবে। একই key একাধিকবার রাখবে না।

DRF throttle সাধারণত request rate কমানোর একটি প্রাথমিক স্তর। Production-এ shared Redis cache, account/email-ভিত্তিক সীমা এবং abuse monitoring-ও দরকার। বিশেষ করে unknown email-এর request-গুলোর জন্যও সীমা প্রয়োগ করা জরুরি; শুধু user-ভিত্তিক cooldown তা করতে পারে না।

## ৮. API কীভাবে পরীক্ষা করবে?

প্রথমে Django server চালাও:

```
python manage.py runserver
```

### Step 1 — প্রথম OTP request

```
POST /api/auth/otp/forgot/
Content-Type: application/json
```

```
{
  "email": "your-email@example.com"
}
```

Email account থাকলে এবং email backend সফল হলে প্রথম OTP পাঠানো হবে। Development-এ console email backend ব্যবহার করলে OTP terminal-এ দেখতে পারবে।

### Step 2 — Cooldown চলাকালে resend

```
POST /api/auth/otp/resend/
Content-Type: application/json
```

```
{
  "email": "your-email@example.com"
}
```

৬০ সেকেন্ডের আগে resend করলে নতুন OTP তৈরি হবে না। তবুও API generic `200 OK` response দেবে।

### Step 3 — Cooldown শেষ হলে resend

প্রথম OTP তৈরির ৬০ সেকেন্ড পর আবার resend request পাঠাও। আগের OTP এখনো pending এবং unexpired থাকলে নতুন OTP তৈরি হবে ও ইমেইল পাঠানোর চেষ্টা হবে।

এবার আগের OTP দিয়ে verify করার চেষ্টা করলে সেটি ব্যর্থ হওয়ার কথা। নতুন OTP দিয়ে verify করতে হবে।

## ৯. Automated tests

`accounts/tests/test_resend_otp.py` নামে একটি test file তৈরি করতে পারো। নিচের test-গুলো API-র মূল আচরণ যাচাই করে।

```
# accounts/tests/test_resend_otp.pyfrom datetime import timedeltafrom unittest.mock import patchfrom django.contrib.auth import get_user_modelfrom django.utils import timezonefrom rest_framework import statusfrom rest_framework.test import APITestCasefrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import (    generate_otp,    get_otp_expiry,    get_otp_verifier,)User = get_user_model()class ResendOTPTests(APITestCase):    def setUp(self):        self.user = User.objects.create_user(            email="student@example.com",            password="Strong-Test-Password-928!",        )        self.url = "/api/auth/otp/resend/"
```

Test চালাও:

```
python manage.py test accounts.tests.test_resend_otp
```

নোট: তোমার existing test setup-এ custom user manager, required fields বা settings আলাদা হলে `setUp()` সেই অনুযায়ী adjust করবে। SQLite-এ test পাস করলেই PostgreSQL-এর concurrent locking আচরণ পুরোপুরি যাচাই হয়েছে—এমন নয়।

## ১০. Production checklist

Implementation checklist

0/8 complete

Serializer ও URL ঠিকমতো যুক্ত হয়েছে

Cooldown-এর আগে নতুন OTP তৈরি হচ্ছে না

নতুন OTP পুরোনো pending OTP invalidate করছে

Expired, used বা invalidated OTP resend করা যাচ্ছে না

Email failure হলে নতুন OTP invalidate হচ্ছে

Unknown email-এর জন্য একই generic response আসছে

IP-based throttle এবং shared-cache rate limiting পরিকল্পনা করা হয়েছে

PostgreSQL-এ concurrent resend behavior পরীক্ষা করা হয়েছে

## এই লেসনের মূল শিক্ষা

- `ResendOTPSerializer` request validate করে।
- `create_resend_otp()` cooldown, expiry এবং OTP invalidation নিয়ন্ত্রণ করে।
- `ResendOTPAPIView` generic response দিয়ে email enumeration কমায়।
- Email পাঠানো database transaction-এর বাইরে করা হয়।
- Rate limiting এবং database locking এক জিনিস নয়—দুটিই প্রয়োজন হতে পারে।

পরবর্তী লেসন — Lesson 16: Security & Rate Limiting। সেখানে আমরা OTP brute-force protection, per-IP ও per-email limits, Redis cache, cooldown abuse, logging এবং password reset flow-এর security tests আরও শক্ত করব।

----
# Lesson 16: Security & Rate Limiting — Django REST Framework

এই লেসনে আমাদের Password Reset OTP system-কে আরও নিরাপদ করব। আগের lessons-এ আমরা OTP তৈরি, email পাঠানো, verify করা, password reset এবং resend API তৈরি করেছি। এখন লক্ষ্য হলো কেউ যেন অসংখ্য request পাঠিয়ে OTP অনুমান করতে, email spam করতে বা password reset endpoint অপব্যবহার করতে না পারে।

আজকের lesson-এ আমরা ৬টি বিষয় শিখব:

1. OTP brute-force protection — বারবার ভুল OTP দিলে কী হবে।
2. IP-based rate limiting — একই IP থেকে অতিরিক্ত request বন্ধ করা।
3. Email/account-based rate limiting — একই email-এ বারবার OTP পাঠানো কমানো।
4. Redis cache — একাধিক Django worker-এ rate limit ভাগ করে ব্যবহার করা।
5. Security logging — নিরাপদভাবে সন্দেহজনক activity record করা।
6. Automated security tests — limit কাজ করছে কি না যাচাই করা।

## ১. Threat model: আমরা কী থেকে সুরক্ষা দিচ্ছি?

OTP brute force

কেউ বারবার OTP guess করছে।

প্রতিরোধ: সর্বোচ্চ ৫টি ভুল চেষ্টা, এরপর OTP invalidation।

Email bombing

একই email-এ বারবার OTP পাঠানোর চেষ্টা।

প্রতিরোধ: cooldown এবং account/email-based limit।

Request flooding

একটি IP থেকে অতিরিক্ত API call।

প্রতিরোধ: DRF throttle, Redis cache এবং প্রয়োজনে reverse-proxy limit।

Email enumeration

কোন email-এ account আছে তা খুঁজে বের করা।

প্রতিরোধ: একই ধরনের generic response এবং সতর্ক timing design।

একটি গুরুত্বপূর্ণ পার্থক্য: DRF throttling abuse কমাতে সাহায্য করে, কিন্তু এটি পূর্ণাঙ্গ security boundary নয়। DRF-এর সাধারণ cache-based throttle atomic distributed rate limiter নয়। গুরুত্বপূর্ণ production system-এ আরও শক্তিশালী, shared rate-limiting ব্যবস্থা লাগতে পারে।

## ২. OTP brute-force protection যাচাই

আমাদের আগের `verification_service.py`-তে ইতিমধ্যে এই নিয়ম ছিল:

```
MAX_OTP_ATTEMPTS = 5GRANT_EXPIRY_MINUTES = 10
```

এর অর্থ:

- OTP ভুল হলে `attempts` বাড়বে।
- সর্বোচ্চ পাঁচটি ভুল চেষ্টার পর OTP invalid হবে।
- সঠিক OTP দিলে একবার ব্যবহারযোগ্য reset grant তৈরি হবে।
- Grant-এর মেয়াদ ১০ মিনিট।
- OTP verifier HMAC দিয়ে যাচাই হবে; সরাসরি OTP database-এ রাখা হবে না।

এই অংশটি নিশ্চিত করো:

```
# accounts/services/verification_service.pyMAX_OTP_ATTEMPTS = 5GRANT_EXPIRY_MINUTES = 10
```

এবং ভুল OTP-এর ক্ষেত্রে transaction-এর ভেতরে attempt count বাড়াতে হবে:

```
otp_record.attempts += 1if otp_record.attempts >= MAX_OTP_ATTEMPTS:    otp_record.invalidated_at = nowotp_record.save(    update_fields=["attempts", "invalidated_at", "updated_at"])
```

এই snippet-টি তোমার বিদ্যমান verification service-এর ভুল-OTP branch-এ বসাবে; পুরো function-এর বিকল্প হিসেবে নয়। Model-এর field এবং বর্তমান implementation-এর সঙ্গে মিলিয়ে নেবে।

কেন transaction ও row lock গুরুত্বপূর্ণ? একসঙ্গে একাধিক ভুল request এলে attempt count হারিয়ে যাওয়া বা limit অতিক্রম করার ঝুঁকি থাকে। তাই OTP record lock করে যাচাই ও update একই transaction-এ করতে হবে। PostgreSQL-এ concurrency test করাও জরুরি।

## ৩. DRF-এর IP-based rate limiting

প্রথমে আমরা বিদ্যমান DRF throttle ব্যবহার করব।

`config/settings.py`-এ বিদ্যমান `REST_FRAMEWORK` dictionary-এর ভেতরে প্রয়োজনীয় settings merge করো:

```
REST_FRAMEWORK = {    # তোমার বিদ্যমান authentication ও permission settings রাখবে।    "DEFAULT_THROTTLE_CLASSES": [        "rest_framework.throttling.AnonRateThrottle",        "rest_framework.throttling.UserRateThrottle",    ],    "DEFAULT_THROTTLE_RATES": {        "anon": "100/hour",        "user": "1000/hour",        "forgot_password": "5/hour",        "verify_otp": "10/hour",        "reset_password": "5/hour",        "resend_otp": "5/hour",    },}
```

সতর্কতা: তোমার settings-এ আগে থেকেই `DEFAULT_THROTTLE_CLASSES` বা অন্য rate থাকলে সেগুলো অন্ধভাবে replace করবে না। বিশেষ করে `ScopedRateThrottle` ব্যবহার করা view-গুলোর জন্য সংশ্লিষ্ট scope-এর rate থাকতে হবে।

আমাদের OTP views-এ আগে থেকেই আছে:

```
permission_classes = [AllowAny]throttle_classes = [ScopedRateThrottle]throttle_scope = "verify_otp"
```

এখানে `verify_otp`-এর মতো scope অনুযায়ী limit প্রযোজ্য হবে।

### IP limit কীভাবে কাজ করে?

- একজন anonymous client নির্দিষ্ট সময়ের মধ্যে সীমিত request করতে পারবে।
- সীমা ছাড়ালে DRF সাধারণত `429 Too Many Requests` ফেরত দেবে।
- authenticated user-এর জন্য `UserRateThrottle` user identity অনুযায়ী সীমা নির্ধারণ করে।

তবে anonymous request-এর IP নির্ভরতা proxy configuration-এর ওপরও নির্ভর করতে পারে। `X-Forwarded-For` header-কে সরাসরি বিশ্বাস করবে না; trusted reverse proxy ও Django-এর proxy settings সঠিকভাবে configure করতে হবে।

## ৪. Email-based rate limiting

IP limit একা যথেষ্ট নয়। কেউ একাধিক IP থেকে একই email-এ OTP request পাঠাতে পারে। তাই email-ভিত্তিক limit-ও লাগবে।

এখানে আমরা Redis-backed Django cache ব্যবহার করে একটি সহজ fixed-window limiter তৈরি করব। Email-কে সরাসরি cache key-তে না রেখে HMAC দিয়ে key তৈরি করব, যাতে cache key-তে email প্রকাশ না পায়।

### ৪.১ Dedicated secret যোগ করো

`.env`:

```
RATE_LIMIT_PEPPER=replace-with-a-long-random-secret
```

`config/settings.py`:

```
import osRATE_LIMIT_PEPPER = os.environ["RATE_LIMIT_PEPPER"]
```

Secret-টি version control-এ commit করবে না এবং production-এ শক্তিশালী random value ব্যবহার করবে।

### ৪.২ Rate-limit service তৈরি করো

নতুন ফাইল `accounts/services/rate_limit_service.py`:

```
import hashlibimport hmacfrom django.conf import settingsfrom django.core.cache import cachedef _email_cache_key(email: str) -> str:    normalized_email = email.strip().casefold()    digest = hmac.new(        settings.RATE_LIMIT_PEPPER.encode("utf-8"),        normalized_email.encode("utf-8"),        hashlib.sha256,    ).hexdigest()    return f"security:password-reset:email:{digest}"def allow_email_request(    email: str,    *,    limit: int = 5,    window_seconds: int = 3600,) -> bool:    """    Fixed-window limiter.    Returns True if the request is allowed.    Returns False if the limit has been reached.    """    key = _email_cache_key(email)    # প্রথম request এ window তৈরি করার চেষ্টা।    added = cache.add(        key,        1,        timeout=window_seconds,    )    if added:        return True    try:        count = cache.incr(key)    except ValueError:        # Key expiry-র কারণে হারিয়ে গেলে নতুন window তৈরি করো।        added = cache.add(            key,            1,            timeout=window_seconds,        )        if added:            return True        # Concurrent request-এ key তৈরি হয়ে গেলে আবার increment।        try:            count = cache.incr(key)        except ValueError:            return False    return count <= limit
```

এই implementation-এ প্রথম request-সহ সর্বোচ্চ পাঁচটি request অনুমোদিত হবে, প্রতি এক ঘণ্টার window-এ।

Implementation note: এই service shared Redis cache-এ চালাবে। Cache backend যদি atomic increment নিশ্চিত না করে, concurrent request-এর ক্ষেত্রে এই code যথেষ্ট নির্ভরযোগ্য নয়। আরও শক্তিশালী production limiter-এর জন্য Redis atomic script বা dedicated rate-limiting service ব্যবহার করা যায়। Fixed-window পদ্ধতিতে window boundary-র আশপাশে request rate অল্প সময়ের জন্য বেশি হতে পারে।

## ৫. Forgot Password API-তে limit প্রয়োগ

`accounts/views.py`-এর `ForgotPasswordAPIView`-এ serializer validation-এর পরে, user lookup করার আগে email-based limiter প্রয়োগ করো।

```
from accounts.services.rate_limit_service import allow_email_request
```

তারপর `post()` method-এ:

```
serializer = ForgotPasswordSerializer(data=request.data)serializer.is_valid(raise_exception=True)email = serializer.validated_data["email"]allowed = allow_email_request(    email,    limit=5,    window_seconds=3600,)if not allowed:    # Email account আছে কি না প্রকাশ করবে না।    return Response(        {            "detail": (                "If an account exists with this email, "                "password reset instructions will be sent."            )        },        status=status.HTTP_200_OK,    )# এরপর আগের user lookup ও OTP creation logic চলবে।
```

এই check-টি user lookup-এর আগে করা গুরুত্বপূর্ণ। এতে account না থাকলেও একই email-এর request সীমিত হবে।

একই helper `ResendOTPAPIView`-তেও ব্যবহার করতে পারো, তবে দুই endpoint-এর জন্য আলাদা limit দরকার হলে cache key-তে action-ও যোগ করতে হবে। মনে রাখবে, একই email-কে দুই endpoint দিয়ে ঘুরিয়ে request পাঠানো ঠেকাতে shared email limit উপকারী।

Verify endpoint-এও অতিরিক্ত limit যোগ করতে পারো, তবে ভুল OTP-এর পাঁচ-চেষ্টার সীমা অবশ্যই বজায় থাকবে। API-level limit ও OTP-level attempt count আলাদা স্তর।

## ৬. Redis-কে Django cache হিসেবে configure করা

Local memory cache ব্যবহার করলে একাধিক Django worker-এর মধ্যে counter share হয় না। Production-এ shared Redis cache ব্যবহার করা ভালো।

Redis package ইনস্টল করো:

```
pip install django-redis
```

`config/settings.py`-এ:

```
CACHES = {    "default": {        "BACKEND": "django_redis.cache.RedisCache",        "LOCATION": os.environ.get(            "REDIS_CACHE_URL",            "redis://127.0.0.1:6379/1",        ),        "OPTIONS": {            "CLIENT_CLASS": "django_redis.client.DefaultClient",        },        "TIMEOUT": 3600,    },}
```

`.env`:

```
REDIS_CACHE_URL=redis://127.0.0.1:6379/1
```

Redis চালু আছে কি না যাচাই করো:

```
redis-cli ping
```

প্রত্যাশিত output:

```
PONG
```

এখানে `/1` Redis-এর database index। তোমার deployment-এ Redis authentication, network isolation এবং TLS-এর প্রয়োজনীয়তা বিবেচনা করবে। Redis-কে public internet-এ উন্মুক্ত রাখবে না।

আরেকটি production বিষয়: Redis down হলে rate limiter কী করবে, সেটি আগে থেকেই নির্ধারণ করতে হবে। Sensitive password-reset endpoint-এর ক্ষেত্রে fail-open করলে abuse-এর সুযোগ হতে পারে; fail-closed করলে legitimate user-ও সাময়িকভাবে request করতে নাও পারবে। সিদ্ধান্তটি monitoring ও availability requirement অনুযায়ী নেবে।

## ৭. Security logging

সন্দেহজনক activity log করা দরকার, কিন্তু OTP, raw reset token, password বা email-সহ sensitive তথ্য log করা উচিত নয়।

উদাহরণ হিসেবে একটি ছোট logging helper:

```
# accounts/services/security_logging.pyimport logginglogger = logging.getLogger("accounts.security")def log_security_event(event: str, *, reason: str) -> None:    logger.warning(        "security_event=%s reason=%s",        event,        reason,    )
```

ব্যবহার:

```
log_security_event(    "password_reset_rate_limited",    reason="email_limit_exceeded",)
```

এখানে email বা OTP log করা হচ্ছে না।

Production-এ Django logging configuration-এ `accounts.security` logger-এর handler ও level নির্ধারণ করবে। Log retention, access control এবং monitoring-ও গুরুত্বপূর্ণ। IP address লগ করলে সেটিকে personal data হিসেবে যথাযথভাবে সংরক্ষণ ও সীমিত access-এর আওতায় রাখবে।

## ৮. Automated security tests

এখন rate-limit service-এর আচরণ পরীক্ষা করি।

`accounts/tests/test_rate_limit_service.py`:

```
from unittest.mock import patchfrom django.test import SimpleTestCase, override_settingsfrom accounts.services.rate_limit_service import (    allow_email_request,)@override_settings(    RATE_LIMIT_PEPPER="test-only-secret",)class EmailRateLimitTests(SimpleTestCase):    def setUp(self):        from django.core.cache import cache        cache.clear()    @patch(        "accounts.services.rate_limit_service.cache.add",        return_value=True,    )    def test_first_request_is_allowed(self, mock_add):        allowed = allow_email_request(            "student@example.com",            limit=5,            window_seconds=3600,        )        self.assertTrue(allowed)        mock_add.assert_called_once()    @patch(        "accounts.services.rate_limit_service.cache.add",        return_value=False,    )    @patch(        "accounts.services.rate_limit_service.cache.incr",        return_value=6,    )    def test_request_over_limit_is_denied(        self,        mock_incr,        mock_add,    ):        allowed = allow_email_request(            "student@example.com",            limit=5,            window_seconds=3600,        )        self.assertFalse(allowed)
```

Test চালাও:

```
python manage.py test accounts.tests.test_rate_limit_service
```

এই tests limiter-এর basic decision logic যাচাই করে। Mock করা cache দিয়ে বাস্তব Redis-এর atomicity, expiration বা concurrent request যাচাই করা যায় না। সেগুলোর জন্য Redis-সহ integration tests লিখবে।

## ৯. পুরো security flow একবার দেখে নাও

Client request

Forgot / Verify / Resend / Reset

IP / API throttle

অতিরিক্ত request সীমিত করা

Email-based limiter

একই email-এ বারবার request নিয়ন্ত্রণ

OTP verification

Expiry, attempt count, HMAC verification, row locking

Single-use reset grant

Token expiry ও password validation

একটি গুরুত্বপূর্ণ অতিরিক্ত সুরক্ষা: password reset সফল হলে আগের JWT access/refresh token-গুলো স্বয়ংক্রিয়ভাবে বাতিল হয়েছে—এমন ধরে নেওয়া যাবে না। তোমার JWT configuration অনুযায়ী refresh-token blacklist, token versioning বা session revocation strategy আলাদাভাবে ডিজাইন করতে হবে।

## ১০. Lesson 16 checklist

Security checklist

0/9

ভুল OTP-এর সর্বোচ্চ চেষ্টা ৫টি

OTP expiry ও একবার ব্যবহারযোগ্য grant যাচাই

DRF API throttling configured

Forgot ও Resend-এ email-based rate limit

Shared Redis cache configured

Sensitive তথ্য ছাড়া security logging

Rate limit ও OTP failure-এর automated tests

PostgreSQL-এ concurrency tests

Password reset-এর পর JWT/session revocation strategy নির্ধারণ

### Lesson 16-এর সারসংক্ষেপ

আমরা শিখলাম যে নিরাপদ OTP system শুধু শক্তিশালী OTP তৈরির ওপর নির্ভর করে না। IP limit, email limit, OTP attempt count, expiry, shared cache, transaction locking এবং monitoring—সবগুলো স্তর একসঙ্গে কাজ করে।

পরবর্তী লেসন — Lesson 17: React/Next.js Integration। সেখানে আমরা frontend থেকে Forgot Password → OTP Verify → Reset Password flow তৈরি করব, API validation error দেখাব এবং loading state ও resend countdown যোগ করব।

----
# Lesson 17: React/Next.js Integration — Django REST Framework OTP Password Reset

এই লেসনে আমরা আগের Django REST Framework backend-এর সঙ্গে React বা Next.js frontend যুক্ত করব। ব্যবহারকারী যেন ওয়েবসাইট থেকেই Forgot Password, OTP Verify, Resend OTP এবং Reset Password সম্পন্ন করতে পারে।

আমরা আগের backend endpoint-গুলো ব্যবহার করব—নতুন authentication system তৈরি করব না।

## ১. Frontend থেকে পুরো flow

Step 1 — Forgot Password

Email input → `/api/auth/otp/forgot/`

Step 2 — Verify OTP

৬-ডিজিট OTP → `/api/auth/otp/verify/`

Step 3 — Reset Password

Reset token + নতুন password → `/api/auth/otp/reset/`

Success

Confirmation দেখাবে এবং Login page-এ যেতে দেবে

আমরা এমনভাবে frontend বানাব, যাতে:

- প্রতিটি ধাপে validation error দেখায়।
- API request চলার সময় button disable থাকে।
- Resend OTP-এর আগে countdown থাকে।
- Reset token URL বা browser storage-এ না রেখে React state-এ রাখা হয়।
- Backend-এর generic response ব্যবহার করে account enumeration কমানো হয়।

## ২. React project তৈরি

যদি তোমার আগে থেকেই React/Vite project থাকে, নতুন project তৈরি না করে সেই project-এ নিচের files যোগ করো।

নতুন project হলে:

```
npm create vite@latest otp-frontend -- --template react
cd otp-frontend
npm install
npm run dev
```

Project structure:

```
src/
├── api/
│   └── passwordResetApi.js
├── components/
│   └── PasswordReset.jsx
├── App.jsx
└── main.jsx
```

Backend-এর base URL environment variable-এ রাখব।

Vite project-এর `.env`:

```
VITE_API_BASE_URL=http://127.0.0.1:8000/api/auth
```

`.env`-এ secret বা password রাখবে না। `VITE_` দিয়ে শুরু হওয়া variable browser bundle-এ প্রকাশিত হতে পারে।

## ৩. API helper তৈরি করো

`src/api/passwordResetApi.js` তৈরি করো। API call-গুলো একটি file-এ রাখলে component পরিষ্কার থাকবে।

```
// src/api/passwordResetApi.js

const API_BASE_URL = import.meta.env.VITE_API_BASE_URL;

async function postJSON(endpoint, payload) {
  const response = await fetch(`${API_BASE_URL}${endpoint}`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
    body: JSON.stringify(payload),
  });

  const data = await response.json().catch(() => ({}));

  if (!response.ok) {
    const error = new Error(
      data.detail || "Request failed. Please try again."
    );

    error.status = response.status;
    error.data = data;

    throw error;
  }

  return data;
}

export function requestPasswordReset(email) {
  return postJSON("/otp/forgot/", { email });
}

export function verifyPasswordResetOTP(email, otp) {
  return postJSON("/otp/verify/", { email, otp });
}

export function resendPasswordResetOTP(email) {
  return postJSON("/otp/resend/", { email });
}

export function resetPassword(resetToken, newPassword, confirmPassword) {
  return postJSON("/otp/reset/", {
    reset_token: resetToken,
    new_password: newPassword,
    confirm_password: confirmPassword,
  });
}
```

### কী শিখলে?

- `fetch()` backend-এ HTTP request পাঠায়।
- `JSON.stringify()` JavaScript object-কে JSON body-তে রূপান্তর করে।
- `response.ok` দিয়ে HTTP success যাচাই করা হয়।
- `error.data`-তে DRF-এর field-level validation errors রাখা হয়।

নোট: এই helper ধরে নিচ্ছে backend JSON response দেয়। Network failure বা server unavailable হলে `fetch()` নিজেই error throw করবে, যা component-এ catch করব।

## ৪. সম্পূর্ণ Password Reset component

এবার `src/components/PasswordReset.jsx` তৈরি করো। নিচের component-এ তিনটি form, resend countdown, loading state, validation errors এবং success message থাকবে।

```
// src/components/PasswordReset.jsx

import { useEffect, useState } from "react";

import {
  requestPasswordReset,
  verifyPasswordResetOTP,
  resendPasswordResetOTP,
  resetPassword,
} from "../api/passwordResetApi";

const RESEND_COOLDOWN = 60;

function getErrorMessage(error) {
  const data = error?.data;

  if (data && typeof data === "object") {
    if (typeof data.detail === "string") {
      return data.detail;
    }

    // DRF field-level errors, যেমন:
    // { "otp": ["Invalid or expired verification code."] }
    const firstFieldError = Object.values(data).flat().find(
      (item) => typeof item === "string"
    );

    if (firstFieldError) {
      return firstFieldError;
    }
  }

  if (error?.status === 429) {
    return "Too many requests. Please wait before trying again.";
  }

  return error?.message || "Something went wrong. Please try again.";
}

export default function PasswordReset() {
  const [step, setStep] = useState("email");

  const [email, setEmail] = useState("");
  const [otp, setOtp] = useState("");

  const [resetToken, setResetToken] = useState("");
  const [newPassword, setNewPassword] = useState("");
  const [confirmPassword, setConfirmPassword] = useState("");

  const [loading, setLoading] = useState(false);
  const [resendSeconds, setResendSeconds] = useState(0);

  const [message, setMessage] = useState("");
  const [error, setError] = useState("");

  // Resend countdown
  useEffect(() => {
    if (resendSeconds <= 0) return;

    const timerId = setTimeout(() => {
      setResendSeconds((seconds) => seconds - 1);
    }, 1000);

    return () => clearTimeout(timerId);
  }, [resendSeconds]);

  function clearFeedback() {
    setMessage("");
    setError("");
  }

  async function handleForgotPassword(event) {
    event.preventDefault();
    clearFeedback();
    setLoading(true);

    try {
      const data = await requestPasswordReset(email.trim());

      setMessage(
        data.detail ||
          "If an account exists with this email, instructions will be sent."
      );

      setStep("otp");
      setResendSeconds(RESEND_COOLDOWN);
    } catch (err) {
      setError(getErrorMessage(err));
    } finally {
      setLoading(false);
    }
  }

  async function handleVerifyOTP(event) {
    event.preventDefault();
    clearFeedback();
    setLoading(true);

    try {
      const data = await verifyPasswordResetOTP(email.trim(), otp);

      if (!data.reset_token) {
        throw new Error("The server did not return a reset token.");
      }

      // Token শুধু component state-এ থাকবে।
      setResetToken(data.reset_token);
      setMessage("OTP verified. You can now reset your password.");
      setStep("password");
    } catch (err) {
      setError(getErrorMessage(err));
    } finally {
      setLoading(false);
    }
  }

  async function handleResendOTP() {
    clearFeedback();
    setLoading(true);

    try {
      const data = await resendPasswordResetOTP(email.trim());

      setMessage(
        data.detail ||
          "If an eligible request exists, a new code will be sent."
      );

      setOtp("");
      setResendSeconds(RESEND_COOLDOWN);
    } catch (err) {
      setError(getErrorMessage(err));
    } finally {
      setLoading(false);
    }
  }

  async function handleResetPassword(event) {
    event.preventDefault();
    clearFeedback();

    if (newPassword !== confirmPassword) {
      setError("Passwords do not match.");
      return;
    }

    setLoading(true);

    try {
      const data = await resetPassword(
        resetToken,
        newPassword,
        confirmPassword
      );

      setMessage(
        data.detail || "Password has been reset successfully."
      );

      setStep("success");

      // কাজ শেষ হলে sensitive values পরিষ্কার করো।
      setResetToken("");
      setOtp("");
      setNewPassword("");
      setConfirmPassword("");
    } catch (err) {
      setError(getErrorMessage(err));
    } finally {
      setLoading(false);
    }
  }

  function startOver() {
    setStep("email");
    setEmail("");
    setOtp("");
    setResetToken("");
    setNewPassword("");
    setConfirmPassword("");
    setResendSeconds(0);
    clearFeedback();
  }

  return (
    <main className="password-reset-page">
      <section className="password-reset-card">
        <h1>Password Reset</h1>

        <p className="step-label">
          {step === "email" && "Step 1 of 3 — Enter your email"}
          {step === "otp" && "Step 2 of 3 — Verify your OTP"}
          {step === "password" && "Step 3 of 3 — Set a new password"}
          {step === "success" && "Password reset complete"}
        </p>

        {message && (
          <div className="message success-message" role="status">
            {message}
          </div>
        )}

        {error && (
          <div className="message error-message" role="alert">
            {error}
          </div>
        )}

        {step === "email" && (
          <form onSubmit={handleForgotPassword}>
            <label htmlFor="email">Email address</label>

            <input
              id="email"
              type="email"
              autoComplete="email"
              value={email}
              onChange={(event) => setEmail(event.target.value)}
              placeholder="you@example.com"
              maxLength={254}
              required
            />

            <button type="submit" disabled={loading}>
              {loading ? "Sending..." : "Send verification code"}
            </button>
          </form>
        )}

        {step === "otp" && (
          <form onSubmit={handleVerifyOTP}>
            <p>
              If your email is eligible, a verification code will be sent.
            </p>

            <label htmlFor="otp">6-digit OTP</label>

            <input
              id="otp"
              type="text"
              inputMode="numeric"
              autoComplete="one-time-code"
              pattern="[0-9]{6}"
              minLength={6}
              maxLength={6}
              value={otp}
              onChange={(event) => {
                const value = event.target.value;

                if (/^[0-9]*$/.test(value)) {
                  setOtp(value);
                }
              }}
              placeholder="Enter 6-digit code"
              required
            />

            <button
              type="submit"
              disabled={loading || otp.length !== 6}
            >
              {loading ? "Verifying..." : "Verify OTP"}
            </button>

            <button
              type="button"
              className="secondary-button"
              onClick={handleResendOTP}
              disabled={loading || resendSeconds > 0}
            >
              {resendSeconds > 0
                ? `Resend available in ${resendSeconds}s`
                : "Resend OTP"}
            </button>

            <button
              type="button"
              className="text-button"
              onClick={startOver}
              disabled={loading}
            >
              Use another email
            </button>
          </form>
        )}

        {step === "password" && (
          <form onSubmit={handleResetPassword}>
            <label htmlFor="new-password">New password</label>

            <input
              id="new-password"
              type="password"
              autoComplete="new-password"
              value={newPassword}
              onChange={(event) => setNewPassword(event.target.value)}
              required
            />

            <label htmlFor="confirm-password">
              Confirm new password
            </label>

            <input
              id="confirm-password"
              type="password"
              autoComplete="new-password"
              value={confirmPassword}
              onChange={(event) =>
                setConfirmPassword(event.target.value)
              }
              required
            />

            <button type="submit" disabled={loading}>
              {loading ? "Resetting..." : "Reset password"}
            </button>
          </form>
        )}

        {step === "success" && (
          <button type="button" onClick={startOver}>
            Back to password reset
          </button>
        )}
      </section>
    </main>
  );
}
```

## ৫. App-এ component ব্যবহার করো

`src/App.jsx`:

```
import PasswordReset from "./components/PasswordReset";
import "./style.css";

export default function App() {
  return <PasswordReset />;
}
```

`src/style.css`:

```
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: system-ui, sans-serif;
  background: #f3f4f6;
  color: #111827;
}

.password-reset-page {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 24px;
}

.password-reset-card {
  width: 100%;
  max-width: 440px;
  padding: 28px;
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgb(0 0 0 / 6%);
}

.password-reset-card h1 {
  margin-top: 0;
}

.step-label {
  color: #6b7280;
  font-size: 14px;
  margin-bottom: 24px;
}

.password-reset-card form {
  display: grid;
  gap: 12px;
}

.password-reset-card label {
  font-size: 14px;
  font-weight: 600;
}

.password-reset-card input {
  width: 100%;
  padding: 12px;
  border: 1px solid #d1d5db;
  border-radius: 8px;
  font: inherit;
}

.password-reset-card input:focus {
  outline: 2px solid #2563eb;
  outline-offset: 1px;
}

.password-reset-card button {
  padding: 12px;
  border: 0;
  border-radius: 8px;
  background: #2563eb;
  color: white;
  font: inherit;
  cursor: pointer;
}

.password-reset-card button:disabled {
  opacity: 0.55;
  cursor: not-allowed;
}

.password-reset-card .secondary-button {
  background: #374151;
}

.password-reset-card .text-button {
  background: transparent;
  color: #2563eb;
}

.message {
  padding: 12px;
  margin-bottom: 16px;
  border-radius: 8px;
  overflow-wrap: anywhere;
}

.success-message {
  background: #ecfdf5;
  color: #065f46;
}

.error-message {
  background: #fef2f2;
  color: #991b1b;
}
```

চালাও:

```
npm run dev
```

এখন browser-এ Vite যে local URL দেখাবে, সেখানে component দেখতে পাবে।

## ৬. Django backend-এ CORS configure করো

React development server সাধারণত Django-এর থেকে আলাদা origin-এ চলে। তাই browser request block করলে backend-এ CORS configure করতে হবে।

Install:

```
pip install django-cors-headers
```

`config/settings.py`:

```
INSTALLED_APPS = [    # Existing apps...    "corsheaders",]MIDDLEWARE = [    "corsheaders.middleware.CorsMiddleware",    # Existing middleware...]
```

Development-এর জন্য:

```
CORS_ALLOWED_ORIGINS = [    "http://localhost:5173",    "http://127.0.0.1:5173",]
```

Production-এ তোমার প্রকৃত frontend origin যোগ করবে। `CORS_ALLOW_ALL_ORIGINS = True` দিয়ে production চালানো উচিত নয়।

## ৭. Next.js ব্যবহার করলে কী পরিবর্তন হবে?

একই API helper ও component Next.js App Router-এ ব্যবহার করা যাবে, তবে কয়েকটি পরিবর্তন দরকার।

Environment variable — `.env.local`:

```
NEXT_PUBLIC_API_BASE_URL=http://127.0.0.1:8000/api/auth
```

`passwordResetApi.js`-এ:

```
const API_BASE_URL = process.env.NEXT_PUBLIC_API_BASE_URL;
```

`PasswordReset.jsx`-এর একেবারে শুরুতে যোগ করবে:

```
"use client";
```

কারণ component-এ `useState`, `useEffect` এবং browser interaction রয়েছে। এরপর App Router-এ `app/forgot-password/page.jsx` তৈরি করে:

```
"use client";

import PasswordReset from "@/components/PasswordReset";

export default function ForgotPasswordPage() {
  return <PasswordReset />;
}
```

তোমার project-এ component alias আলাদা হলে import path ঠিক করে নেবে। মনে রেখো, `NEXT_PUBLIC_` variable-ও browser-এ প্রকাশিত হয়—এতে কোনো secret রাখা যাবে না।

## ৮. Manual testing checklist

Frontend test checklist

0/10

Forgot Password-এ valid email format দিয়ে request পাঠানো

Email backend থেকে OTP পাওয়া

সঠিক OTP দিয়ে reset token পাওয়া

ভুল বা expired OTP-তে error দেখা

নতুন password ও confirmation দিয়ে password reset করা

ভুল confirmation দিলে frontend validation দেখা

Cooldown শেষ হওয়ার আগে Resend button disabled থাকা

Cooldown শেষে resend request পাঠানো

Backend 429 দিলে user-friendly message দেখা

Browser DevTools-এ reset token URL বা localStorage-এ না থাকা

### কয়েকটি production বিষয় মনে রাখবে

- Frontend-এর countdown শুধু user experience উন্নত করে; আসল cooldown backend-এ enforce করতে হবে।
- Reset token React state-এ রাখা হয়েছে, কিন্তু XSS হলে JavaScript state-ও ঝুঁকিতে পড়তে পারে। তাই frontend-এর XSS protection গুরুত্বপূর্ণ।
- Password reset সফল হওয়ার পর ব্যবহারকারীকে Login page-এ পাঠাতে পারো। আগের JWT token বাতিল করার ব্যবস্থা backend-এ আলাদাভাবে থাকতে হবে।
- Backend error-এর সম্পূর্ণ response ব্যবহারকারীর সামনে দেখানোর পরিবর্তে প্রয়োজনীয় field error দেখাবে; internal exception বা stack trace প্রকাশ করবে না।

## Lesson 17 সম্পন্ন

এখন তোমার কাছে Django REST Framework-এর OTP password reset API-এর সঙ্গে যুক্ত একটি React/Next.js-compatible frontend flow আছে।

পরবর্তী লেসন — Lesson 18: Automated Testing। সেখানে আমরা model, serializer, service, API response, OTP expiry, brute-force limit, email failure এবং password reset-এর success/failure cases নিয়ে test suite তৈরি করব—যাতে code পরিবর্তন করলেও security ভেঙে না যায়।

----
# Lesson 18: Automated Testing — Django REST Framework OTP Authentication

এই লেসনে আমরা আমাদের Password Reset System-এর জন্য একটি বাস্তবসম্মত automated test suite তৈরি করব। এখন পর্যন্ত আমরা Custom User, OTP Model, OTP Email, Verify OTP, Reset Password, Resend OTP, Rate Limiting এবং React/Next.js integration শিখেছি। এবার যাচাই করব—সঠিক অবস্থায় system কাজ করে কি না এবং ভুল বা আক্রমণাত্মক request এলে নিরাপদ থাকে কি না।

আজকের লক্ষ্য: শুধু test লিখে pass করানো নয়; কোন security rule ভেঙে গেলে test সেটি ধরতে পারবে, সেটি শেখা।

## ১. কোন কোন layer test করব?

Model tests

User, OTP, reset grant এবং database constraints।

Serializer tests

Invalid email, ভুল OTP format, mismatch password এবং invalid input।

Service tests

OTP generation, expiry, attempts, grant creation এবং password change।

API integration tests

HTTP status, JSON response, email failure এবং endpoint behavior।

Security tests

OTP brute force, single-use token, throttling এবং email enumeration।

Django-তে সাধারণত `TestCase` ব্যবহার করে database-সহ tests চালানো যায়। DRF-এর `APITestCase` API request পাঠানোর সুবিধা দেয়। আমাদের এই course-এ দুটোই ব্যবহার করব।

## ২. Test folder তৈরি করো

আমাদের project structure হবে:

```
accounts/
└── tests/
    ├── __init__.py
    ├── test_otp_service.py
    ├── test_serializers.py
    ├── test_password_reset_service.py
    ├── test_auth_api.py
    └── test_security.py
```

আগের `test_resend_otp.py` ও `test_rate_limit_service.py` থাকলে সেগুলোও রাখতে পারো।

Test চালানোর জন্য আলাদা database নিজে হাতে তৈরি করতে হবে না। Django test runner সাধারণত test database তৈরি করে, test চালায় এবং শেষে তা পরিষ্কার করে।

## ৩. OTP service tests

প্রথমে আমাদের OTP helper functions যাচাই করি। এখানে পরীক্ষা করব:

- OTP ছয়টি ASCII digit কি না।
- OTP-এর শুরুতে `0` থাকলে সেটি ঠিকমতো সংরক্ষিত হচ্ছে কি না।
- সঠিক OTP verifier match করছে কি না।
- ভুল OTP প্রত্যাখ্যাত হচ্ছে কি না।

`accounts/tests/test_otp_service.py`:

```
# accounts/tests/test_otp_service.pyfrom django.test import SimpleTestCase, override_settingsfrom accounts.services.otp_service import (    generate_otp,    get_otp_verifier,    verify_otp_value,)@override_settings(OTP_PEPPER="test-only-pepper-secret")class OTPServiceTests(SimpleTestCase):    def test_generated_otp_contains_six_ascii_digits(self):        otp = generate_otp()        self.assertEqual(len(otp), 6)        self.assertTrue(otp.isascii())        self.assertTrue(otp.isdigit())    def test_otp_preserves_leading_zero(self):        # Randomness বাদ দিয়ে নির্দিষ্ট return value পরীক্ষা।        from unittest.mock import patch        with patch(            "accounts.services.otp_service.secrets.randbelow",            return_value=42,        ):            otp = generate_otp()        self.assertEqual(otp, "000042")    def test_same_otp_produces_matching_verifier(self):        otp = "042781"        verifier = get_otp_verifier(otp)        self.assertTrue(verify_otp_value(otp, verifier))    def test_wrong_otp_is_rejected(self):        verifier = get_otp_verifier("042781")        self.assertFalse(verify_otp_value("042782", verifier))    def test_invalid_otp_format_is_rejected(self):        verifier = get_otp_verifier("042781")        self.assertFalse(verify_otp_value("１２３４５６", verifier))        self.assertFalse(verify_otp_value("12ab56", verifier))        self.assertFalse(verify_otp_value("12345", verifier))
```

### কী শিখলে?

`SimpleTestCase` ব্যবহার করেছি, কারণ এই tests-এ database প্রয়োজন নেই।

`patch()` ব্যবহার করে random generator-এর output নিয়ন্ত্রণ করেছি। এতে leading-zero test নির্ভরযোগ্য হয়; বাস্তবে random OTP বারবার generate করে শূন্য দিয়ে শুরু হওয়া OTP পাওয়ার অপেক্ষা করতে হয় না।

## ৪. Serializer tests

এবার নিশ্চিত করব যে API-তে invalid input এলে তা service-এ পৌঁছানোর আগেই প্রত্যাখ্যাত হয়।

`accounts/tests/test_serializers.py`:

```
from django.test import SimpleTestCase, override_settingsfrom accounts.serializers import (    ForgotPasswordSerializer,    VerifyOTPSerializer,    ResetPasswordSerializer,)@override_settings(    AUTH_PASSWORD_VALIDATORS=[        {            "NAME": (                "django.contrib.auth.password_validation."                "MinimumLengthValidator"            ),            "OPTIONS": {"min_length": 8},        },    ])class PasswordResetSerializerTests(SimpleTestCase):    def test_forgot_password_rejects_invalid_email(self):        serializer = ForgotPasswordSerializer(            data={"email": "not-an-email"}        )        self.assertFalse(serializer.is_valid())        self.assertIn("email", serializer.errors)    def test_verify_otp_rejects_non_digit_code(self):        serializer = VerifyOTPSerializer(            data={                "email": "student@example.com",                "otp": "12AB56",            }        )        self.assertFalse(serializer.is_valid())        self.assertIn("otp", serializer.errors)    def test_verify_otp_rejects_short_code(self):        serializer = VerifyOTPSerializer(            data={                "email": "student@example.com",                "otp": "123",            }        )        self.assertFalse(serializer.is_valid())    def test_reset_password_rejects_mismatch(self):        serializer = ResetPasswordSerializer(            data={                "reset_token": "example-reset-token",                "new_password": "Example-Password-123!",                "confirm_password": "Different-Password-123!",            }        )        self.assertFalse(serializer.is_valid())        self.assertIn("confirm_password", serializer.errors)    def test_reset_password_rejects_blank_token(self):        serializer = ResetPasswordSerializer(            data={                "reset_token": " ",                "new_password": "Example-Password-123!",                "confirm_password": "Example-Password-123!",            }        )        self.assertFalse(serializer.is_valid())        self.assertIn("reset_token", serializer.errors)
```

গুরুত্বপূর্ণ: তোমার `ResetPasswordSerializer` যদি project-এর বর্তমান password validators অনুযায়ী আরও শক্তিশালী password চায়, তাহলে test-এর password-গুলো সেই নিয়ম অনুযায়ী ঠিক করবে। Serializer-এ `validate_password()` চালু থাকলে কেবল mismatch পরীক্ষা করতে হলেও অন্য password validation-গুলো পাস করতে হবে।

## ৫. Password reset service tests

এটি সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি। আমরা যাচাই করব:

1. Valid grant দিয়ে password পরিবর্তন হয়।
2. Reset token দ্বিতীয়বার ব্যবহার করা যায় না।
3. Expired token প্রত্যাখ্যাত হয়।
4. Invalid token-এ password পরিবর্তন হয় না।

`accounts/tests/test_password_reset_service.py`:

```
import hashlibimport secretsfrom datetime import timedeltafrom django.contrib.auth import get_user_modelfrom django.test import TestCase, override_settingsfrom django.utils import timezonefrom accounts.models import PasswordResetGrantfrom accounts.services.reset_password_service import (    InvalidResetToken,    reset_password,)User = get_user_model()@override_settings(    AUTH_PASSWORD_VALIDATORS=[],)class PasswordResetServiceTests(TestCase):    def setUp(self):        self.user = User.objects.create_user(            email="student@example.com",            password="Old-Password-123!",        )        self.raw_token = secrets.token_urlsafe(32)        self.grant = PasswordResetGrant.objects.create(            user=self.user,            token_hash=hashlib.sha256(                self.raw_token.encode("utf-8")            ).hexdigest(),            expires_at=timezone.now() + timedelta(minutes=10),        )    def test_valid_token_changes_password(self):        reset_password(            raw_token=self.raw_token,            new_password="New-Password-456!",        )        self.user.refresh_from_db()        self.assertTrue(            self.user.check_password("New-Password-456!")        )        self.assertFalse(            self.user.check_password("Old-Password-123!")        )        self.grant.refresh_from_db()        self.assertTrue(self.grant.is_used)    def test_used_token_cannot_be_reused(self):        reset_password(            raw_token=self.raw_token,            new_password="New-Password-456!",        )        with self.assertRaises(InvalidResetToken):            reset_password(                raw_token=self.raw_token,                new_password="Another-Password-789!",            )    def test_expired_token_is_rejected(self):        self.grant.expires_at = timezone.now() - timedelta(seconds=1)        self.grant.save(update_fields=["expires_at"])        with self.assertRaises(InvalidResetToken):            reset_password(                raw_token=self.raw_token,                new_password="New-Password-456!",            )        self.user.refresh_from_db()        self.assertTrue(            self.user.check_password("Old-Password-123!")        )    def test_unknown_token_is_rejected(self):        with self.assertRaises(InvalidResetToken):            reset_password(                raw_token="not-a-valid-reset-token",                new_password="New-Password-456!",            )        self.user.refresh_from_db()        self.assertTrue(            self.user.check_password("Old-Password-123!")        )
```

### কেন raw token নয়, hash database-এ রাখছি?

আমাদের service-এ `PasswordResetGrant.token_hash`-এর সঙ্গে incoming token-এর SHA-256 hash তুলনা করা হয়। তাই test-এও token-এর hash তৈরি করে database-এ সংরক্ষণ করেছি।

Reset token দীর্ঘ ও cryptographically random হওয়ায় এর জন্য SHA-256 ব্যবহার উপযুক্ত। ছয়-ডিজিট OTP-এর ক্ষেত্রে একই পদ্ধতি যথেষ্ট নয়, কারণ OTP-এর সম্ভাব্য মান খুব কম; তাই OTP-এর জন্য HMAC pepper ব্যবহার করা হয়েছে।

## ৬. API integration tests

এখন শুধু service নয়, HTTP endpoint-ও পরীক্ষা করব। এখানে `APITestCase` ব্যবহার করব।

`accounts/tests/test_auth_api.py`:

```
from unittest.mock import patchfrom django.contrib.auth import get_user_modelfrom django.test import TestCase, override_settingsfrom rest_framework import statusfrom rest_framework.test import APITestCasefrom accounts.models import PasswordResetOTPUser = get_user_model()@override_settings(    REST_FRAMEWORK={        "DEFAULT_AUTHENTICATION_CLASSES": [],        "DEFAULT_PERMISSION_CLASSES": [            "rest_framework.permissions.AllowAny",        ],        "DEFAULT_THROTTLE_CLASSES": [],        "DEFAULT_THROTTLE_RATES": {},    },    AUTH_PASSWORD_VALIDATORS=[],)class PasswordResetAPITests(APITestCase):    def setUp(self):        self.user = User.objects.create_user(            email="student@example.com",            password="Old-Password-123!",        )    @patch(        "accounts.views.send_password_reset_otp_email",        return_value=True,    )    def test_forgot_password_returns_generic_response(        self,        mock_email,    ):        response = self.client.post(            "/api/auth/otp/forgot/",            {"email": self.user.email},            format="json",        )        self.assertEqual(response.status_code, status.HTTP_200_OK)        self.assertIn("detail", response.data)        mock_email.assert_called_once()    @patch(        "accounts.views.send_password_reset_otp_email",        return_value=True,    )    def test_unknown_email_gets_generic_response(        self,        mock_email,    ):        response = self.client.post(            "/api/auth/otp/forgot/",            {"email": "unknown@example.com"},            format="json",        )        self.assertEqual(response.status_code, status.HTTP_200_OK)        self.assertIn("detail", response.data)        mock_email.assert_not_called()    def test_invalid_email_is_rejected(self):        response = self.client.post(            "/api/auth/otp/forgot/",            {"email": "not-an-email"},            format="json",        )        self.assertEqual(            response.status_code,            status.HTTP_400_BAD_REQUEST,        )    @patch(        "accounts.views.send_password_reset_otp_email",        side_effect=RuntimeError("Email backend failed"),    )    def test_email_failure_does_not_expose_internal_error(        self,        mock_email,    ):        response = self.client.post(            "/api/auth/otp/forgot/",            {"email": self.user.email},            format="json",        )        self.assertEqual(response.status_code, status.HTTP_200_OK)        self.assertNotIn("Email backend failed", str(response.data))        record = PasswordResetOTP.objects.filter(            user=self.user        ).latest("created_at")        self.assertIsNotNone(record.invalidated_at)
```

### একটি বিষয় খেয়াল করো

এই test class-এ throttle সাময়িকভাবে disable করা হয়েছে, যাতে প্রতিটি test অন্য test-এর request count-এর ওপর নির্ভর না করে। এটি production settings পরিবর্তন নয়। Rate limiting-এর জন্য আলাদা tests থাকবে।

আরও বাস্তবসম্মত integration tests-এ তুমি প্রকৃত project settings রেখেও throttle test করতে পারো; তবে shared cache ও rate limit state আলাদা করে নিয়ন্ত্রণ করতে হবে।

## ৭. Verify OTP এবং attempt-limit tests

আমাদের security rule হলো: পাঁচটি ভুল OTP attempt-এর পর সেই OTP আর ব্যবহার করা যাবে না। এই rule-এর জন্য শুধু response status পরীক্ষা না করে database state-ও পরীক্ষা করতে হবে।

`accounts/tests/test_security.py`-এ উদাহরণ:

```
from datetime import timedeltafrom unittest.mock import patchfrom django.contrib.auth import get_user_modelfrom django.test import TestCase, override_settingsfrom django.utils import timezonefrom rest_framework.exceptions import ValidationErrorfrom accounts.models import PasswordResetOTPfrom accounts.services.otp_service import get_otp_verifierfrom accounts.services.verification_service import (    verify_otp_and_create_grant,)User = get_user_model()@override_settings(OTP_PEPPER="test-only-pepper")class OTPAttemptSecurityTests(TestCase):    def setUp(self):        self.user = User.objects.create_user(            email="student@example.com",            password="Old-Password-123!",        )        self.record = PasswordResetOTP.objects.create(            user=self.user,            otp_verifier=get_otp_verifier("123456"),            expires_at=timezone.now() + timedelta(minutes=5),        )    def test_wrong_otp_increments_attempt_count(self):        with self.assertRaises(ValidationError):            verify_otp_and_create_grant(                self.user,                submitted_otp="999999",            )        self.record.refresh_from_db()        self.assertEqual(self.record.attempts, 1)    def test_otp_is_invalidated_after_maximum_attempts(self):        # পাঁচটি ভুল attempt simulate করা হচ্ছে।        for _ in range(5):            with self.assertRaises(ValidationError):                verify_otp_and_create_grant(                    self.user,                    submitted_otp="999999",                )        self.record.refresh_from_db()        self.assertGreaterEqual(self.record.attempts, 5)        self.assertIsNotNone(self.record.invalidated_at)    def test_expired_otp_is_rejected(self):        self.record.expires_at = timezone.now() - timedelta(seconds=1)        self.record.save(update_fields=["expires_at"])        with self.assertRaises(ValidationError):            verify_otp_and_create_grant(                self.user,                submitted_otp="123456",            )
```

তোমার service-এ exception type আলাদা হলে test-এ সেই exception ব্যবহার করবে। উপরের উদাহরণ ধরে নিচ্ছে `verify_otp_and_create_grant()` invalid OTP-এর জন্য DRF `ValidationError` raise করে, যেমন আমাদের আগের API integration-এ দেখানো হয়েছিল।

এই test-গুলো চালানোর আগে নিশ্চিত করো `verify_otp_and_create_grant()` সত্যিই `MAX_OTP_ATTEMPTS` enforce করে এবং expired OTP-কে invalidate করে। Test ব্যর্থ হলে test-কে অন্ধভাবে পরিবর্তন না করে service-এর intended security behavior যাচাই করো।

## ৮. Rate limiting tests

আমাদের `allow_email_request()` service-এর জন্য আগে একটি basic test লিখেছিলাম। এখন আরও কয়েকটি বিষয় যাচাই করব:

- Limit-এর মধ্যে request অনুমোদিত হচ্ছে।
- Limit অতিক্রম করলে request block হচ্ছে।
- Email normalization-এর কারণে একই email-এর uppercase/lowercase ভিন্ন quota পাচ্ছে না।

```
# accounts/tests/test_rate_limit_service.pyfrom django.core.cache import cachefrom django.test import SimpleTestCase, override_settingsfrom accounts.services.rate_limit_service import allow_email_request@override_settings(RATE_LIMIT_PEPPER="test-only-pepper")class EmailRateLimitTests(SimpleTestCase):    def setUp(self):        cache.clear()    def tearDown(self):        cache.clear()    def test_allows_requests_within_limit(self):        for _ in range(3):            self.assertTrue(                allow_email_request(                    "student@example.com",                    limit=3,                    window_seconds=3600,                )            )    def test_blocks_request_after_limit(self):        for _ in range(3):            allow_email_request(                "student@example.com",                limit=3,                window_seconds=3600,            )        self.assertFalse(            allow_email_request(                "student@example.com",                limit=3,                window_seconds=3600,            )        )    def test_email_case_does_not_create_new_quota(self):        self.assertTrue(            allow_email_request(                "Student@example.com",                limit=1,                window_seconds=3600,            )        )        self.assertFalse(            allow_email_request(                "student@example.com",                limit=1,                window_seconds=3600,            )        )
```

এই tests তোমার configured test cache-এ চালাবে। `cache.clear()` shared production Redis-এ কখনো চালাবে না—এটি test setup-এর জন্য।

## ৯. সব test চালাও

একটি একটি করে:

```
python manage.py test accounts.tests.test_otp_service
python manage.py test accounts.tests.test_serializers
python manage.py test accounts.tests.test_password_reset_service
python manage.py test accounts.tests.test_auth_api
python manage.py test accounts.tests.test_security
python manage.py test accounts.tests.test_rate_limit_service
```

অথবা পুরো app-এর সব tests:

```
python manage.py test accounts
```

Test fail করলে প্রথমে error-এর গুরুত্বপূর্ণ অংশগুলো দেখো:

- `AssertionError` — expected ও actual ফল আলাদা।
- `ValidationError` — validation failure বা প্রত্যাশিত exception-এর ধরন মিলছে না।
- `DoesNotExist` — test-এর আগে প্রয়োজনীয় record তৈরি হয়নি, অথবা service record invalidate/delete করেছে।
- `ImproperlyConfigured` — settings, email backend বা environment variable অনুপস্থিত।
- `OperationalError` — database schema, migration বা database connection-সংক্রান্ত সমস্যা।

Test database-এর schema-তে নতুন model বা field যোগ করার পর migrations তৈরি ও প্রয়োগ করা আছে কি না যাচাই করবে:

```
python manage.py makemigrations
python manage.py migrate
```

## ১০. Test coverage দেখো

Coverage দিয়ে কোন code execute হয়েছে তা দেখা যায়। তবে coverage 100% মানেই application নিরাপদ—এমন নয়।

Install:

```
pip install coverage
```

চালাও:

```
coverage run manage.py test accounts
coverage report -m
```

HTML report তৈরি করতে:

```
coverage html
```

এরপর generated `htmlcov/index.html` browser-এ খুলে দেখতে পারো কোন line-গুলো test হয়নি।

## ১১. Production-grade testing-এ পরের ধাপ

Unit tests

OTP helper, serializers, password-reset service এবং rate-limit logic।

API integration tests

HTTP response, email failure, invalid input ও reset flow।

Concurrency tests

PostgreSQL-এ একই OTP বা reset grant নিয়ে একসঙ্গে একাধিক request পাঠানো। SQLite-এর test একা যথেষ্ট নয়।

CI automation

প্রতিটি Git commit বা pull request-এ স্বয়ংক্রিয়ভাবে tests চালানো।

### Lesson 18-এর assignment

Assignment checklist

0/7

সব OTP service tests pass করানো

সঠিক OTP দিয়ে reset grant তৈরি হওয়ার test যোগ করা

একই reset token দ্বিতীয়বার ব্যবহার করলে password অপরিবর্তিত থাকে—যাচাই করা

Email backend failure হলে OTP invalidate হয়—যাচাই করা

Email enumeration ঠেকানোর generic response test করা

Rate limit অতিক্রম করলে request block হয়—যাচাই করা

পুরো accounts test suite চালিয়ে failures সমাধান করা

এই লেসনের মূল শিক্ষা: Automated tests শুধু code কাজ করছে কি না তা যাচাই করে না; security rule-গুলো ভবিষ্যতে code পরিবর্তনের পরও বজায় থাকছে কি না, সেটিও যাচাই করে।

পরবর্তী লেসন — Lesson 19: Production Deployment। সেখানে Django OTP authentication system-কে production environment-এ deploy করার জন্য environment secrets, PostgreSQL, Redis, Gunicorn, Nginx, HTTPS, email configuration, logging এবং deployment-time checks নিয়ে কাজ করব।

----
# Lesson 19: Production Deployment — Django REST Framework OTP Authentication

এবার আমরা আমাদের Password Reset OTP project-কে development environment থেকে production server-এ deploy করার প্রস্তুতি নেব। শুধু `runserver` চালালেই production deployment সম্পূর্ণ হয় না—database, email, Redis, HTTPS, secrets, reverse proxy, logging এবং security settings ঠিকভাবে configure করতে হয়।

তুমি আগে Gunicorn, Docker, PostgreSQL, Nginx ও HTTPS নিয়ে কাজ করেছ। তাই এই লেসনে আমরা সেগুলোকে একসঙ্গে যুক্ত করে একটি বাস্তবসম্মত deployment architecture তৈরি করব।

## ১. Production architecture

React / Next.js Frontend

HTTPS • Forgot Password • OTP • Reset Password

Nginx Reverse Proxy

HTTPS termination • Proxy • Request limits

Gunicorn + Django REST Framework

Authentication • OTP services • Password reset API

PostgreSQL

Users, OTP verifiers, reset grants

Redis

Shared cache, rate limits

SMTP Email Provider

OTP email delivery

### কোন component কী কাজ করবে?

| Component     | দায়িত্ব                              |
| ------------- | ------------------------------------ |
| Nginx         | HTTPS, reverse proxy, request limits |
| Gunicorn      | Django application চালানো            |
| Django/DRF    | API ও authentication logic           |
| PostgreSQL    | স্থায়ী application data              |
| Redis         | Shared cache ও rate limiting         |
| SMTP provider | Password-reset OTP ইমেইল পাঠানো      |

Security rule: PostgreSQL ও Redis public internet-এ expose করবে না। Internet থেকে শুধু প্রয়োজনীয় web ports—সাধারণত 80 ও 443—উন্মুক্ত থাকবে। SSH-ও সীমিত access-এ রাখতে হবে।

## ২. Production project structure

আমাদের project-এ Docker configuration যোগ করলে structure এমন হতে পারে:

```
otp_auth_project/
├── accounts/
├── config/
├── manage.py
├── requirements.txt
├── Dockerfile
├── compose.yaml
├── .dockerignore
├── .env                  # Git-এ commit নয়
├── .env.example          # Secret ছাড়া template
└── deploy/
    └── nginx/
        └── default.conf
```

এখানে `.env`-এ production secrets থাকবে, আর `.env.example`-এ শুধু variable-এর নাম ও placeholder থাকবে।

## ৩. Production dependencies

`requirements.txt`-এ প্রয়োজনীয় package আছে কি না যাচাই করো:

```
Django
djangorestframework
gunicorn
psycopg[binary]
django-redis
django-cors-headers
python-dotenv
```

তোমার project-এ `dj-rest-auth`, `django-allauth`, SimpleJWT বা অন্য package ব্যবহার করলে সেগুলোও requirements-এ রাখতে হবে। Production-এ dependency version pin করে এবং lockfile/version control বজায় রেখে deploy করা ভালো।

Docker deployment-এ environment variable ব্যবহার করলে `python-dotenv` বাধ্যতামূলক নয়; Django সরাসরি environment থেকে settings পড়তে পারে।

## ৪. Dockerfile তৈরি করো

Project root-এ `Dockerfile`:

```
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN addgroup --system django \
    && adduser --system --ingroup django django

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=django:django . .

RUN mkdir -p /app/staticfiles \
    && chown -R django:django /app

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--timeout", "30", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### কেন এই configuration?

- `python:3.12-slim` — ছোট Python base image।
- `PYTHONUNBUFFERED=1` — log দ্রুত stdout-এ পাঠাতে সাহায্য করে।
- `USER django` — application root user হিসেবে চলে না।
- `config.wsgi:application` — Gunicorn-কে Django WSGI application-এর ঠিকানা জানায়।
- `--workers 3` — প্রাথমিক উদাহরণ; CPU, RAM এবং workload অনুযায়ী ঠিক করতে হবে।

তোমার Django version ও dependencies Python 3.12 সমর্থন করে কি না যাচাই করবে। Production-এ tested base image version pin করাও ভালো।

`.dockerignore`:

```
.env
.git
.venv
venv
__pycache__
*.py[cod]
.pytest_cache
htmlcov
node_modules
```

এতে secrets ও অপ্রয়োজনীয় development files image build context-এ যাওয়ার ঝুঁকি কমে।

## ৫. Production environment variables

`.env.example` তৈরি করো:

```
DJANGO_SETTINGS_MODULE=config.settings
DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=api.example.com,localhost

DB_NAME=otp_auth
DB_USER=otp_user
DB_PASSWORD=replace-with-a-strong-database-password
DB_HOST=db
DB_PORT=5432

REDIS_CACHE_URL=redis://redis:6379/1

EMAIL_HOST=smtp.example.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-smtp-user
EMAIL_HOST_PASSWORD=replace-with-smtp-secret
DEFAULT_FROM_EMAIL=no-reply@example.com

FRONTEND_ORIGIN=https://example.com
```

`api.example.com` ও `example.com` placeholder—নিজের domain দিয়ে পরিবর্তন করবে।

Production `.env`:

- Git-এ commit করবে না।
- Public repository বা frontend bundle-এ রাখবে না।
- Server-এ সীমিত file permissions-সহ সংরক্ষণ করবে।
- SMTP password, Django secret key এবং database password আলাদা ও শক্তিশালী রাখবে।

## ৬. Django production settings

`config/settings.py`-এ environment-based settings ব্যবহার করো। নিচের অংশগুলো existing settings-এর সঙ্গে merge করবে; পুরো settings file-কে অন্ধভাবে replace করবে না।

```
import osDEBUG = os.environ.get("DJANGO_DEBUG", "False").lower() == "true"SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]ALLOWED_HOSTS = [    host.strip()    for host in os.environ["DJANGO_ALLOWED_HOSTS"].split(",")    if host.strip()]DATABASES = {    "default": {        "ENGINE": "django.db.backends.postgresql",        "NAME": os.environ["DB_NAME"],        "USER": os.environ["DB_USER"],        "PASSWORD": os.environ["DB_PASSWORD"],        "HOST": os.environ.get("DB_HOST", "db"),        "PORT": os.environ.get("DB_PORT", "5432"),        "CONN_MAX_AGE": 60,    }}CACHES = {    "default": {        "BACKEND": "django_redis.cache.RedisCache",        "LOCATION": os.environ["REDIS_CACHE_URL"],        "OPTIONS": {            "CLIENT_CLASS": "django_redis.client.DefaultClient",        },    }}EMAIL_HOST = os.environ["EMAIL_HOST"]EMAIL_PORT = int(os.environ.get("EMAIL_PORT", "587"))EMAIL_USE_TLS = (    os.environ.get("EMAIL_USE_TLS", "True").lower() == "true")EMAIL_HOST_USER = os.environ["EMAIL_HOST_USER"]EMAIL_HOST_PASSWORD = os.environ["EMAIL_HOST_PASSWORD"]DEFAULT_FROM_EMAIL = os.environ["DEFAULT_FROM_EMAIL"]STATIC_URL = "/static/"STATIC_ROOT = "/app/staticfiles"
```

তোমার project-এ `MEDIA_ROOT`, custom user, `AUTH_PASSWORD_VALIDATORS`, `REST_FRAMEWORK`, SimpleJWT এবং OTP security settings আগের মতোই রাখতে হবে।

Production HTTPS-এর জন্য proxy header ও secure-cookie settings নিচের Nginx configuration-এর সঙ্গে সামঞ্জস্য রেখে configure করতে হবে। Nginx থেকে আসা forwarded header কেবল trusted proxy path থেকেই গ্রহণ করবে।

## ৭. Docker Compose তৈরি করো

Project root-এ `compose.yaml`:

```
services:
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
      test: ["CMD-SHELL", "pg_isready -U $${POSTGRES_USER} -d $${POSTGRES_DB}"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - backend

  redis:
    image: redis:7-alpine
    restart: unless-stopped
    command: ["redis-server", "--appendonly", "yes"]
    volumes:
      - redis_data:/data
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - backend

  app:
    build: .
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DB_HOST: db
      REDIS_CACHE_URL: redis://redis:6379/1
    expose:
      - "8000"
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    volumes:
      - staticfiles:/app/staticfiles
    networks:
      - backend

  nginx:
    image: nginx:alpine
    restart: unless-stopped
    ports:
      - "80:80"
    depends_on:
      - app
    volumes:
      - ./deploy/nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - staticfiles:/staticfiles:ro
    networks:
      - backend

volumes:
  postgres_data:
  redis_data:
  staticfiles:

networks:
  backend:
```

কীভাবে কাজ করবে?

- PostgreSQL ও Redis শুধু internal Docker network-এ থাকবে।
- Django container Gunicorn-এর মাধ্যমে API চালাবে।
- Nginx বাইরের HTTP request গ্রহণ করে Django-তে পাঠাবে।
- Database ও Redis-এর health check সফল হওয়ার পর Django service শুরু হবে।

`depends_on` দিয়ে database ও cache ready হওয়া নিশ্চিত করার চেষ্টা করা হয়েছে। তবে Django application-এ transient connection failure হলে graceful retry বা recovery strategy-ও প্রয়োজন।

Production-এ database ও Redis image-গুলো tested patch version বা digest-এ pin করো, backup strategy রাখো এবং Redis-এ প্রয়োজন অনুযায়ী authentication/network isolation যোগ করো।

## ৮. Nginx reverse proxy

`deploy/nginx/default.conf` তৈরি করো:

```
upstream django_app {
    server app:8000;
    keepalive 16;
}

server {
    listen 80;
    server_name api.example.com;

    client_max_body_size 10m;

    location /static/ {
        alias /staticfiles/;
        access_log off;
        expires 7d;
    }

    location / {
        proxy_pass http://django_app;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_connect_timeout 5s;
        proxy_read_timeout 30s;
    }
}
```

`api.example.com`-কে তোমার প্রকৃত API domain দিয়ে পরিবর্তন করবে।

এটি প্রাথমিক HTTP reverse-proxy configuration। এটি একা HTTPS deployment নয়। Public production deployment-এর আগে TLS certificate, HTTP-to-HTTPS redirect এবং certificate renewal configure করতে হবে। `X-Forwarded-For` header-কে trusted proxy configuration ছাড়া security decision-এর জন্য ব্যবহার করবে না।

## ৯. Deployment চালানোর ধাপ

Server-এ project code ও `.env` প্রস্তুত করার পর, project root থেকে:

### Step 1 — Image build ও service startup

```
docker compose build
docker compose up -d
docker compose ps
```

### Step 2 — Database migrations

```
docker compose run --rm app python manage.py migrate
```

Production deployment-এ migration চালানোর আগে database backup এবং migration compatibility যাচাই করবে। বড় application-এ migration-কে application startup-এর সঙ্গে অটোমেটিক চালিয়ে দেওয়া সবসময় ভালো কৌশল নয়।

### Step 3 — Static files

```
docker compose run --rm app python manage.py collectstatic --noinput
```

### Step 4 — Django deployment checks

```
docker compose run --rm app python manage.py check --deploy
```

এই command production configuration-এর কিছু পরিচিত security issue শনাক্ত করতে সাহায্য করে। Warning থাকলে বুঝে সমাধান করবে; কেবল warning লুকিয়ে deploy করবে না।

### Step 5 — Logs দেখো

```
docker compose logs --tail=100 app
docker compose logs --tail=100 nginx
docker compose logs --tail=100 db
docker compose logs --tail=100 redis
```

Gunicorn startup error, database authentication failure, SMTP configuration error অথবা Nginx `502 Bad Gateway` হলে logs দিয়ে কারণ খুঁজবে।

## ১০. HTTPS ও secure cookies

Production-এ HTTPS অপরিহার্য, কারণ password reset flow-তে email, OTP এবং reset token আদান-প্রদান হয়।

প্রথমে:

1. Domain-এর DNS record VPS-এর public IP-তে point করো।
2. Firewall-এ প্রয়োজনীয় HTTP/HTTPS ports খোলা রাখো।
3. Nginx-এর জন্য trusted TLS certificate তৈরি করো—যেমন Let's Encrypt।
4. Nginx-এ port 80 থেকে HTTPS redirect configure করো।
5. Certificate renewal স্বয়ংক্রিয়ভাবে হচ্ছে কি না পরীক্ষা করো।

HTTPS ও trusted reverse proxy নিশ্চিত হওয়ার পর Django settings-এ:

```
CSRF_COOKIE_SECURE = TrueSESSION_COOKIE_SECURE = TrueSECURE_SSL_REDIRECT = TrueSECURE_PROXY_SSL_HEADER = ("HTTP_X_FORWARDED_PROTO", "https")
```

`SECURE_PROXY_SSL_HEADER` শুধু তখনই ব্যবহার করবে যখন trusted Nginx proxy forwarded protocol header সঠিকভাবে সেট করছে এবং Django-তে বাইরের client সরাসরি পৌঁছাতে পারে না।

তোমার React frontend ও Django API আলাদা origin-এ থাকলে CORS allowlist-এ প্রকৃত frontend origin রাখতে হবে। Session authentication ব্যবহার করলে CSRF protection ও trusted origins-ও ঠিকমতো configure করতে হবে। JWT ব্যবহার করলেও token storage, refresh-token revocation এবং XSS protection উপেক্ষা করা যাবে না।

## ১১. Production OTP security checklist

Production readiness

0/12

DEBUG=False এবং শক্তিশালী DJANGO_SECRET_KEY

ALLOWED_HOSTS-এ শুধু প্রয়োজনীয় host

PostgreSQL ও Redis public internet থেকে বিচ্ছিন্ন

Production SMTP credentials environment secret-এ রাখা

OTP brute-force limit ও shared Redis rate limiting সচল

Email failure হলে OTP invalidation যাচাই করা

HTTPS certificate এবং automatic renewal

Gunicorn non-root user হিসেবে চলছে

Database backup ও restore পদ্ধতি যাচাই করা

Migration ও collectstatic deployment workflow পরীক্ষা

Health check, error logging ও monitoring

Password reset-এর পর JWT/session revocation policy নির্ধারণ

## ১২. Common production errors

| Error                     | সম্ভাব্য কারণ                                                  |
| ------------------------- | -------------------------------------------------------------- |
| `502 Bad Gateway`         | Gunicorn বন্ধ, ভুল upstream বা Django startup failure          |
| `DisallowedHost`          | `ALLOWED_HOSTS`-এ domain নেই                                   |
| Database connection error | ভুল credentials, host বা PostgreSQL readiness                  |
| Redis connection refused  | ভুল Redis URL বা Redis service বন্ধ                            |
| OTP email আসছে না         | SMTP credentials, provider restriction বা email delivery issue |
| Static files missing      | `collectstatic`, volume বা Nginx alias ভুল                     |
| HTTPS redirect loop       | Proxy protocol header বা SSL redirect configuration ভুল        |

কোনো error হলে production-এর secret বা password প্রকাশ না করে সংশ্লিষ্ট logs ও settings যাচাই করবে।

## Lesson 19 assignment

- Docker Compose দিয়ে PostgreSQL, Redis, Django/Gunicorn ও Nginx চালাও।
- Migrations ও `collectstatic` সফল করো।
- `check --deploy`-এর warnings পর্যালোচনা করো।
- Forgot → Verify → Reset flow বাস্তব email দিয়ে পরীক্ষা করো।
- HTTPS ও domain configuration সম্পন্ন করো।
- Database backup থেকে restore পরীক্ষা করো।
- Container restart-এর পরেও database data থাকে কি না যাচাই করো।

পরবর্তী লেসন — Lesson 20: Final Review & Complete Project। সেখানে পুরো architecture, authentication flow, security review, API documentation, deployment verification এবং ভবিষ্যৎ maintenance checklist একত্র করব।

---
# Lesson 20: Final Review & Complete Project

Django REST Framework + Custom User + Email OTP + Password Reset + React/Next.js + Docker

অভিনন্দন! আমরা যে ২০-লেসনের course অনুসরণ করেছি, তার শেষ লেসনে এখন সবগুলো অংশ একসঙ্গে review করব। লক্ষ্য হলো শুধু code লেখা নয়—একটি authentication feature কীভাবে design, implement, test, deploy এবং maintain করতে হয়, তা বোঝা।

এই project-এ ব্যবহারকারী email দিয়ে password reset request করবে, OTP verify করবে এবং একটি একবার ব্যবহারযোগ্য reset token দিয়ে password পরিবর্তন করবে।

## ১. Final architecture

React / Next.js

Forgot password, OTP verification, reset password

Django REST Framework

Serializers, APIViews, throttling, permissions

OTP Services

Generate, verify, expire

Email Service

HTML + text email

PostgreSQL

Users, OTP verifiers, grants

Redis

Cache, shared rate limits

Gunicorn + Nginx + HTTPS

Production application serving

## ২. Complete password-reset flow

1. Forgot Password: `POST /api/auth/otp/forgot/` — email validate করে, account eligible হলে OTP তৈরি ও email পাঠানোর চেষ্টা করে।
2. Verify OTP: `POST /api/auth/otp/verify/` — OTP, expiry এবং attempt limit যাচাই করে।
3. Create reset grant: OTP সঠিক হলে random reset token তৈরি হয়; database-এ token-এর hash রাখা হয়।
4. Reset Password: `POST /api/auth/otp/reset/` — token ও password যাচাই করে password পরিবর্তন করে এবং grant-কে used করে।
5. Resend OTP: `POST /api/auth/otp/resend/` — pending OTP request, cooldown এবং rate limit যাচাই করে নতুন OTP তৈরি করে।

এই flow-এর মূল security rule হলো: OTP ও reset token আলাদা জিনিস। OTP email-এ যায়; OTP সফলভাবে verify হলে reset token পাওয়া যায়। Reset token ছাড়া password পরিবর্তন করা যাবে না।

## ৩. Final project structure

```
otp_auth_project/
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── accounts/
│   ├── models.py
│   ├── managers.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── services/
│   │   ├── otp_service.py
│   │   ├── email_service.py
│   │   ├── password_reset_service.py
│   │   ├── verification_service.py
│   │   ├── reset_password_service.py
│   │   ├── resend_otp_service.py
│   │   ├── rate_limit_service.py
│   │   └── security_logging.py
│   ├── templates/
│   │   └── emails/
│   │       ├── password_reset_otp.html
│   │       └── password_reset_otp.txt
│   └── tests/
│       ├── test_otp_service.py
│       ├── test_serializers.py
│       ├── test_password_reset_service.py
│       ├── test_auth_api.py
│       ├── test_security.py
│       └── test_rate_limit_service.py
├── frontend/
│   └── src/
│       ├── api/passwordResetApi.js
│       └── components/PasswordReset.jsx
├── Dockerfile
├── compose.yaml
├── .dockerignore
├── .env.example
└── requirements.txt
```

এটি একটি reference structure। তোমার frontend যদি আলাদা repository-তে থাকে, তাহলে `frontend/` আলাদা project হিসেবেও রাখতে পারো।

## ৪. Database models review

আমাদের authentication system-এর তিনটি গুরুত্বপূর্ণ data model আছে।

`User`

Custom user identity, unique email, password hash, active status।

`PasswordResetOTP`

User FK, HMAC verifier, expiry, attempts, used status এবং invalidation timestamp।

`PasswordResetGrant`

User FK, unique token hash, expiry এবং single-use status।

### গুরুত্বপূর্ণ database rules

- `User.email` unique হতে হবে।
- `PasswordResetOTP.otp_verifier`-এ plaintext OTP রাখা যাবে না।
- `PasswordResetGrant.token_hash` unique থাকতে হবে।
- Expired বা used OTP/grant আর ব্যবহার করা যাবে না।
- OTP ও grant-এর পুরোনো records নিয়মিত cleanup করার পরিকল্পনা থাকতে হবে।
- Database constraint, index এবং locking behavior PostgreSQL-এ পরীক্ষা করতে হবে।

একটি গুরুত্বপূর্ণ বিষয়: database-এ পুরোনো OTP record রেখে দিলে সেটি নিজে থেকে expired বা deleted হয় না। Service-এর প্রতিটি verification-এ expiry যাচাই করতে হবে; প্রয়োজন হলে scheduled cleanup job যোগ করবে।

## ৫. Production security review

নিচের checklist-টি শুধু code review-এর জন্য নয়, deployment-এর আগে security acceptance checklist হিসেবেও ব্যবহার করো।

Security acceptance checklist

0/13

Custom user model ও unique email constraint ঠিক আছে

OTP cryptographically secure generator দিয়ে তৈরি হয়

OTP HMAC verifier হিসেবে সংরক্ষিত হয়

OTP expiry এবং maximum attempts enforce করা হয়

Reset token random, hashed, expiring এবং single-use

Password validation Django validators দিয়ে করা হয়

Unknown email-এ generic response দেওয়া হয়

Forgot ও resend endpoint-এ email-based এবং IP-based limits আছে

Shared Redis rate limit concurrent request-এর জন্য যাচাই করা হয়েছে

Email failure হলে নতুন OTP invalidated হয়

Sensitive values logs, URLs ও frontend storage-এ প্রকাশ করা হয় না

Password reset-এর পর session/JWT revocation policy আছে

HTTPS, secret management, backup এবং monitoring প্রস্তুত

## ৬. Final commands: local থেকে deployment

প্রথমে project root-এ:

```
python manage.py check
python manage.py makemigrations
python manage.py migrate
python manage.py test accounts
```

Production configuration ও environment variables সঠিকভাবে set করা থাকলে:

```
python manage.py check --deploy
```

Docker deployment-এর ক্ষেত্রে:

```
docker compose build
docker compose up -d
docker compose ps
docker compose run --rm app python manage.py migrate
docker compose run --rm app python manage.py collectstatic --noinput
docker compose run --rm app python manage.py check --deploy
docker compose logs --tail=100 app
```

Production-এ migration চালানোর আগে backup ও migration compatibility যাচাই করবে। একইভাবে `check --deploy` সফল হলেই পুরো system নিরাপদ প্রমাণিত হয় না; live email delivery, HTTPS, rate limiting এবং recovery procedure-ও পরীক্ষা করতে হবে।

## ৭. পাঁচটি বিষয় অবশ্যই ঠিক করে নেবে

আগের lessons-এর snippets একত্র করার সময় এই বিষয়গুলো যাচাই করা জরুরি।

1. Settings merge: `REST_FRAMEWORK`-এর নতুন configuration যোগ করার সময় আগের authentication classes, permissions এবং throttle rates হারিয়ে ফেলবে না।
2. Rate limiter: আগের Redis-backed fixed-window limiter একটি শিক্ষামূলক implementation। Production-এ concurrency, key expiry, Redis failure এবং বহু endpoint দিয়ে একই email-এ request পাঠানোর বিষয়গুলো integration test করতে হবে।
3. Email delivery: SMTP call সফল হওয়া মানে email নিশ্চিতভাবে inbox-এ পৌঁছেছে, এমন নয়। Production-এ delivery monitoring ও retry strategy দরকার। আরও নির্ভরযোগ্য ব্যবস্থায় email provider-এর সঙ্গে transactional outbox pattern ব্যবহার করা যায়।
4. OTP resend: `created_at`-কে cooldown-এর ভিত্তি হিসেবে ব্যবহার করা হয়েছে। এটি তখনই যথেষ্ট, যখন OTP record তৈরি হওয়ার সময় ও প্রকৃত email-send attempt-এর মধ্যে পার্থক্যটি design-এ গ্রহণযোগ্য। আরও নির্ভুল tracking চাইলে `last_sent_at` এবং send status-এর মতো field যোগ করা যায়।
5. Tests: সব snippets একই project-এ সরাসরি run করলেই pass করবে—এমন নিশ্চয়তা নেই। তোমার প্রকৃত serializer imports, exception types, URL names, password validators, settings এবং service implementations-এর সঙ্গে tests মিলিয়ে নিতে হবে। বিশেষ করে PostgreSQL locking ও Redis concurrency-এর integration tests আলাদাভাবে চালাতে হবে।

## ৮. Course completion map

01–05

Authentication foundation, setup, custom user, JWT, email backend

06–10

Email templates, OTP generation, OTP model, serializer, API view

11–15

Email failure handling, OTP verification, password reset, resend

16–18

Security, React/Next.js integration, automated testing

19–20

Production deployment, final review

## ৯. Final project assignment

এখন একটি বাস্তব end-to-end demonstration তৈরি করো:

- একটি নতুন test user তৈরি করো।
- React/Next.js থেকে Forgot Password request পাঠাও।
- Email-এ OTP পাওয়া যাচ্ছে কি না যাচাই করো।
- সঠিক OTP দিয়ে reset token তৈরি করো।
- নতুন password দিয়ে reset সম্পন্ন করো।
- পুরোনো password দিয়ে login ব্যর্থ এবং নতুন password দিয়ে login সফল হচ্ছে কি না পরীক্ষা করো।
- একই reset token দ্বিতীয়বার ব্যবহার করে ব্যর্থতা যাচাই করো।
- Rate limit, email failure এবং expiry tests চালাও।
- Docker container restart ও database backup/restore পরীক্ষা করো।
- HTTPS-এর মাধ্যমে deployed API-তে সম্পূর্ণ flow যাচাই করো।

Course-এর চূড়ান্ত শিক্ষা: Production-ready authentication মানে শুধু login ও password reset কাজ করা নয়। এর সঙ্গে data integrity, security, error handling, automated testing, deployment এবং maintenance—সবকিছুই জড়িত।

তোমার পরবর্তী ভালো পদক্ষেপ হবে এই course-এর code-গুলোকে একত্র করে একটি বাস্তব repository তৈরি করা, সব tests pass করানো এবং তারপর GitHub Actions দিয়ে automated testing ও deployment pipeline যোগ করা।


---
হ্যাঁ, অবশ্যই! তুমি আমাদের ২০টি Lesson ভালোভাবে follow করে code implement ও test করলে Django REST Framework project-এ Email OTP Password Reset system তৈরি করে integrate করতে পারবে। তবে একটা বিষয় মনে রাখবে: এই ২০টি Lesson মূলত authentication-এর একটি গুরুত্বপূর্ণ অংশ—সম্পূর্ণ authentication ecosystem নয়।

## কোন কোন Authentication feature তৈরি করতে পারবে?

| Feature                                        | Course-এ অবস্থা                                        |
| ---------------------------------------------- | ------------------------------------------------------ |
| Custom User Model (Email login)                | ✅ অন্তর্ভুক্ত                                          |
| Email OTP Password Reset                       | ✅ অন্তর্ভুক্ত                                          |
| OTP Verify ও Resend                            | ✅ অন্তর্ভুক্ত                                          |
| Password validation                            | ✅ অন্তর্ভুক্ত                                          |
| Rate limiting ও security                       | ✅ অন্তর্ভুক্ত                                          |
| Automated tests                                | ✅ অন্তর্ভুক্ত                                          |
| Docker ও production deployment                 | ✅ অন্তর্ভুক্ত                                          |
| User Registration API                          | 🔎 আলাদা করে সম্পূর্ণ করতে হবে                         |
| Login / Logout API                             | 🔎 Authentication configuration অনুযায়ী যাচাই করতে হবে |
| JWT Access ও Refresh Token                     | 🔎 সম্পূর্ণ flow implement ও test করতে হবে             |
| Refresh token rotation ও blacklist             | 🔎 যোগ করতে হবে                                        |
| Email verification                             | 🔎 আলাদা feature                                       |
| Change Password (logged-in user)               | 🔎 আলাদা feature                                       |
| Role-based permissions (Admin/Customer/Seller) | 🔎 আলাদা feature                                       |
| Social Login (Google/GitHub)                   | 🔎 ঐচ্ছিক feature                                      |

## Complete Authentication-এর জন্য আমার recommended roadmap

Phase 1

User foundation

Custom User Model, UserManager, email uniqueness, registration, password hashing

Phase 2

Login & JWT

Login, access/refresh tokens, refresh rotation, logout ও blacklist

Phase 3

Email security

Email verification, OTP password reset, resend cooldown, rate limiting

Phase 4

Account management

Change password, profile, deactivate account, session/token revocation

Phase 5

Authorization

IsAuthenticated, custom permissions, roles, object-level access

Phase 6

Production readiness

Automated tests, PostgreSQL, Redis, Docker, HTTPS, monitoring

## বাস্তবে কীভাবে ব্যবহার করবে?

ধরো, তুমি একটি E-commerce project তৈরি করছ। এই authentication system-কে সেখানে integrate করে:

- Customer registration ও login করতে পারবে।
- Seller এবং Admin-এর জন্য আলাদা permission দিতে পারবে।
- ভুলে যাওয়া password নিরাপদভাবে reset করতে পারবে।
- JWT দিয়ে protected API access করতে পারবে।
- অন্য user-এর order বা private data-তে অননুমোদিত access বন্ধ করতে পারবে।

আমার পরামর্শ: আগে এই ২০টি Lesson-এর project সম্পূর্ণ run করো। এরপর `Complete Authentication System with Django REST Framework` নামে পরের course-এ Registration → Email Verification → Login → JWT Refresh → Logout → Change Password → Forgot Password → Roles & Permissions পর্যন্ত সবকিছু একসঙ্গে তৈরি করো। তাহলে তোমার কাছে reusable authentication module থাকবে, যেটি Hotel Management, E-commerce বা অন্য Django project-এ ব্যবহার করতে পারবে।

----
