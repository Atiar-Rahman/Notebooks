হ্যাঁ। Celery মূলত Django/DRF project-এ **background task** চালানোর জন্য ব্যবহার করা হয়।

সহজভাবে:

```text
Normal Django request
        ↓
     Task তৈরি
        ↓
      Redis
        ↓
 Celery Worker
        ↓
 Background কাজ
```

যেমন user order করল → API response দিয়ে দিল → এরপর email background-এ পাঠানো হলো।

## 1. Celery কখন ব্যবহার করবে?

যেসব কাজ করতে সময় লাগে বা request-এর response-এর জন্য অপেক্ষা করানোর দরকার নেই:

* Email পাঠানো
* Notification
* Report তৈরি
* Image/file processing
* Background data processing
* Scheduled/periodic jobs
* External API call

---

# 2. Install

আগের project-এ:

```bash
pip install celery redis
```

Redis Docker-এ থাকলে:

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:7
```

Test:

```bash
docker exec -it redis redis-cli ping
```

Expected:

```text
PONG
```

---

# 3. Django project

ধরি project:

```text
myproject/
├── manage.py
├── config/
│   ├── settings.py
│   ├── celery.py
│   └── __init__.py
│
└── orders/
    ├── models.py
    ├── views.py
    └── tasks.py
```

---

# 4. Celery configuration

`config/celery.py`

```python
import os

from celery import Celery


os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "config.settings"
)

app = Celery("config")

app.config_from_object(
    "django.conf:settings",
    namespace="CELERY"
)

app.autodiscover_tasks()
```

---

# 5. `__init__.py`

`config/__init__.py`

```python
from .celery import app as celery_app

__all__ = ("celery_app",)
```

এতে Django project load হওয়ার সময় Celery app-টাও available থাকবে।

---

# 6. Redis broker configure

`settings.py`

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

এখানে:

```text
Redis
 └── DB 0
      ↓
Celery Broker
```

তোমার আগের cache:

```text
Redis DB 1 → Django Cache
```

এভাবে আলাদা রাখা যায়।

---

# 7. প্রথম Celery task

`orders/tasks.py`

```python
from celery import shared_task


@shared_task
def send_order_email(order_id):

    print(f"Sending email for order {order_id}")

    return True
```

এটাই Celery task।

`@shared_task` বলছে:

> এই function-টা Celery background task হিসেবে ব্যবহার করা যাবে।

---

# 8. Task call করা

Django view:

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .tasks import send_order_email


class OrderCreateView(APIView):

    def post(self, request):

        # এখানে বাস্তবে Order create করবে
        order_id = 101

        send_order_email.delay(order_id)

        return Response({
            "message": "Order created",
            "order_id": order_id
        })
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

```python
send_order_email.delay(order_id)
```

`.delay()` task-টাকে background queue-তে পাঠায়।

---

# 9. Worker চালানো

Django server:

```bash
python manage.py runserver
```

আরেকটা terminal:

```bash
celery -A config worker --loglevel=info
```

এখন architecture:

```text
POST /orders/
       ↓
    Django
       ↓
Order created
       ↓
.delay()
       ↓
    Redis
       ↓
Celery Worker
       ↓
send_order_email()
```

---

# 10. কেন `.delay()`?

ধরো তুমি সরাসরি লিখলে:

```python
send_order_email(order_id)
```

তাহলে functionটা Django process-এর মধ্যেই execute হবে।

কিন্তু:

```python
send_order_email.delay(order_id)
```

মানে:

```text
Task queue-তে পাঠাও
```

তারপর worker execute করবে।

---

# 11. Real Email Example

ধরো Django-র email configuration আছে।

`tasks.py`:

```python
from celery import shared_task
from django.core.mail import send_mail


@shared_task
def send_order_email(email, order_id):

    send_mail(
        subject="Order Confirmation",
        message=f"Your order #{order_id} has been created.",
        from_email="noreply@example.com",
        recipient_list=[email],
    )
```

View:

```python
class OrderCreateView(APIView):

    def post(self, request):

        email = request.data["email"]

        # Normally database থেকে order তৈরি করবে
        order_id = 101

        send_order_email.delay(
            email,
            order_id
        )

        return Response({
            "message": "Order created successfully"
        })
```

তখন:

```text
User
 ↓
POST /orders/
 ↓
Django
 ↓
Create Order
 ↓
Queue Email Task
 ↓
Response immediately
```

আর background:

```text
Redis
 ↓
Celery Worker
 ↓
Send Email
```

---

# 12. Celery Worker না চালালে?

এটা খুব গুরুত্বপূর্ণ।

যদি:

```bash
celery -A config worker --loglevel=info
```

worker চালু না থাকে, তাহলে task queue-তে থাকতে পারে কিন্তু execute হবে না।

তাই development-এ সাধারণত তিনটা process লাগে:

```text
Terminal 1
──────────
Redis


Terminal 2
──────────
Django


Terminal 3
──────────
Celery Worker
```

---

# 13. `delay()` বনাম `apply_async()`

Simple:

```python
send_order_email.delay(
    email,
    order_id
)
```

More control চাইলে:

```python
send_order_email.apply_async(
    args=[email, order_id],
    countdown=10
)
```

মানে task প্রায় 10 seconds পরে execute করার জন্য queue করা।

আর:

```python
send_order_email.apply_async(
    args=[email, order_id],
    countdown=60
)
```

প্রায় 60 seconds delay।

---

# 14. Retry

ধরো email server temporary unavailable।

Celery retry করতে পারে:

```python
from celery import shared_task


@shared_task(
    autoretry_for=(Exception,),
    retry_backoff=True,
    max_retries=3,
)
def send_order_email(email, order_id):

    # email sending
    ...
```

Concept:

```text
Task
 ↓
Failed
 ↓
Retry
 ↓
Failed
 ↓
Retry
 ↓
Success
```

Production-এ কোন error retry করা উচিত সেটা carefully define করা ভালো।

---

# 15. Multiple workers

Traffic বেশি হলে:

```text
                Redis
                  │
          ┌───────┼───────┐
          ▼       ▼       ▼
       Worker1 Worker2 Worker3
```

তিনটা worker task process করতে পারে।

তখন background workload parallelভাবে handle করা সম্ভব।

---

# 16. Celery + DRF বাস্তব project

ধরো E-commerce API:

```text
POST /orders/
```

Django করবে:

```text
1. Validate request
2. Create Order
3. Update database
4. Queue background tasks
5. Return response
```

তারপর Celery:

```text
Celery
 ├── Send confirmation email
 ├── Send notification
 ├── Generate invoice
 └── Other background processing
```

Architecture:

```text
                    DRF
                     │
                     ▼
                 PostgreSQL
                     │
                     │
                     ▼
                  Celery
                     │
                     ▼
                   Redis
                     │
                     ▼
                Celery Worker
                /     |      \
               ▼      ▼       ▼
            Email  Invoice Notification
```

একটা correction: বাস্তবে সাধারণত **Django task message Redis broker-এ publish করে, worker Redis থেকে task নেয়**—তাই Redis হলো queue/broker-এর মধ্যবর্তী অংশ।

---

# 17. Celery + Redis + Cache একসাথে

তুমি যেহেতু Redis-এর ৫টা lesson শেষ করেছ, পুরো picture এখন এমন:

```text
                    Django / DRF
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
       Cache          Throttle        Celery
          │              │              │
          └──────┬───────┘              │
                 ▼                      ▼
               Redis ◄────────────── Celery Worker
                                         │
                                         ▼
                                  Background Tasks
```

এখানে Redis-এর তিনটা role:

```text
Redis
├── Cache
├── Throttle state
└── Celery broker
```

---

## এখন তোমার শেখার ideal order

তুমি যদি Celery ভালোভাবে শিখতে চাও, আমি এই sequence recommend করব:

```text
Part 1 → Celery basic + Redis
Part 2 → DRF + Celery
Part 3 → Email + Notification
Part 4 → Retry + Task failure + Celery Beat
Part 5 → Production + Docker + Multiple Workers
```

এরপর একটা **real DRF E-commerce project**-এ সবগুলো একসাথে implement করলে Celery practically অনেক পরিষ্কার হয়ে যাবে।


---
অবশ্যই। আমরা একদম **zero → working project** হিসেবে দেখব, যাতে শুধু Celery-এর theory না, পুরো flow বুঝতে পারো।

আমি একটা **DRF Order API** বানাব যেখানে:

```text
User
  ↓
POST /orders/
  ↓
Django creates Order
  ↓
Celery task queue
  ↓
Redis
  ↓
Celery Worker
  ↓
Send confirmation email
```

এখানে আমরা **Django + DRF + PostgreSQL/SQLite + Redis + Celery** ব্যবহার করব।

## Project structure

শেষে projectটা হবে:

```text
order_project/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── celery.py
│
└── orders/
    ├── __init__.py
    ├── models.py
    ├── serializers.py
    ├── tasks.py
    ├── views.py
    └── urls.py
```

### আমরা ধাপে ধাপে করব

**Part 1:** Project setup + Redis
**Part 2:** Order model + DRF API
**Part 3:** Celery setup
**Part 4:** Order create → Celery task
**Part 5:** Email task
**Part 6:** Retry + failure handling
**Part 7:** Celery Beat
**Part 8:** পুরো project Docker দিয়ে run করা

প্রথমে **Part 1** থেকে শুরু করি।

### 1. Project তৈরি

```bash
mkdir order_project
cd order_project

python -m venv venv
```

Linux/macOS:

```bash
source venv/bin/activate
```

Windows:

```bash
venv\Scripts\activate
```

তারপর:

```bash
pip install django djangorestframework celery redis
```

Project:

```bash
django-admin startproject config .
python manage.py startapp orders
```

### 2. `settings.py`

`config/settings.py`

```python
INSTALLED_APPS = [
    # Django apps

    "rest_framework",
    "orders",
]
```

### 3. Redis চালাও

Docker থাকলে:

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:7
```

Check:

```bash
docker exec -it redis redis-cli ping
```

Result:

```text
PONG
```

### 4. Celery configuration

`config/celery.py`

```python
import os

from celery import Celery


os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "config.settings"
)

app = Celery("config")

app.config_from_object(
    "django.conf:settings",
    namespace="CELERY"
)

app.autodiscover_tasks()
```

### 5. `config/__init__.py`

```python
from .celery import app as celery_app

__all__ = ("celery_app",)
```

### 6. Redis broker

`settings.py`-এর শেষে:

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

এখন flow:

```text
Django
   │
   │ .delay()
   ▼
 Redis
   │
   │ task
   ▼
Celery Worker
```

### 7. প্রথম task

`orders/tasks.py`

```python
from celery import shared_task


@shared_task
def test_task():
    print("Celery task is working!")

    return "Success"
```

### 8. Worker চালাও

একটা নতুন terminal:

```bash
celery -A config worker --loglevel=info
```

Worker চালু হলে Celery `orders.tasks.test_task` discover করার কথা।

### 9. Django shell থেকে test

আরেক terminal:

```bash
python manage.py shell
```

তারপর:

```python
from orders.tasks import test_task

result = test_task.delay()
```

তুমি Celery terminal-এ task execute হওয়ার log দেখতে পাবে।

এটাই Celery-এর basic lifecycle:

```text
test_task.delay()
       ↓
    Redis
       ↓
Celery Worker
       ↓
test_task()
       ↓
"Celery task is working!"
```

**পরের ধাপে আমরা এটাকে real বানাব:** `POST /orders/` করলে database-এ Order তৈরি হবে, তারপর automatically Celery দিয়ে confirmation email task queue হবে।
