হ্যাঁ—তাহলে specific **Order project** ধরে না গিয়ে এমন একটা **reusable Celery pattern** দেখাই, যেটা তুমি প্রায় যেকোনো Django/DRF project-এ বসাতে পারবে।

মূল idea হলো:

```text
Any Django/DRF Project
        │
        ├── Normal API logic
        │
        └── Background কাজ
                ↓
             .delay()
                ↓
              Redis
                ↓
         Celery Worker
                ↓
          Celery Task
```

# 1. Celery-এর জন্য minimum setup

প্রথমে install:

```bash
pip install celery redis
```

Redis চালাও:

```bash
docker run -d \
  --name redis \
  -p 6379:6379 \
  redis:7
```

---

# 2. Project structure

ধরো যেকোনো Django project:

```text
myproject/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── celery.py
│
└── app/
    ├── models.py
    ├── views.py
    ├── serializers.py
    └── tasks.py
```

এখানে `app` হতে পারে:

```text
products
orders
users
payments
notifications
blog
school
booking
```

Celery setup একই থাকবে।

---

# 3. `celery.py`

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

এটা **প্রায় সব Django project-এ একই**।

শুধু `config` তোমার project-এর নাম অনুযায়ী হবে।

যেমন project যদি:

```text
ecommerce/
```

হয়, তাহলে:

```python
app = Celery("ecommerce")
```

এবং:

```python
os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "ecommerce.settings"
)
```

---

# 4. `__init__.py`

`config/__init__.py`

```python
from .celery import app as celery_app

__all__ = ("celery_app",)
```

এটাও সাধারণত একই থাকবে।

---

# 5. Redis configure

`settings.py`

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

এখন Celery জানে:

> আমার task queue কোথায়?

উত্তর:

```text
Redis
```

---

# 6. যেকোনো app-এ `tasks.py`

ধরো:

```text
products/
    tasks.py
```

লিখবে:

```python
from celery import shared_task


@shared_task
def my_task():
    print("Background task running")

    return "Done"
```

এখানে একটা গুরুত্বপূর্ণ pattern মনে রাখো:

```python
@shared_task
def task_name():
    ...
```

---

# 7. API থেকে task call

ধরো DRF view:

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .tasks import my_task


class MyAPIView(APIView):

    def post(self, request):

        # Normal API logic
        print("API request received")

        # Background task
        my_task.delay()

        return Response({
            "message": "Request accepted"
        })
```

এখানে:

```python
my_task.delay()
```

হলো সবচেয়ে important অংশ।

---

# 8. Worker চালানো

Django server:

```bash
python manage.py runserver
```

আরেক terminal:

```bash
celery -A config worker --loglevel=info
```

এখন:

```text
             POST /api/
                 │
                 ▼
              Django
                 │
                 │ .delay()
                 ▼
               Redis
                 │
                 ▼
          Celery Worker
                 │
                 ▼
             my_task()
```

---

# 9. এখন real use case দেখো

ধরো **E-commerce project**।

User order করল।

```python
create_order()
```

তারপর:

```python
send_email.delay(order_id)
```

Celery:

```python
@shared_task
def send_email(order_id):
    # send email
    pass
```

---

## একই pattern Blog project-এ

User article publish করল:

```python
publish_article()
```

তারপর:

```python
notify_followers.delay(article_id)
```

Task:

```python
@shared_task
def notify_followers(article_id):
    # notify followers
    pass
```

---

## একই pattern LMS project-এ

Student course কিনল:

```python
create_enrollment()
```

তারপর:

```python
send_course_email.delay(student_id)
```

Task:

```python
@shared_task
def send_course_email(student_id):
    # send email
    pass
```

---

## Booking project

Booking তৈরি হলো:

```python
create_booking()
```

তারপর:

```python
send_booking_confirmation.delay(booking_id)
```

---

# 10. তাহলে Celery-এর universal pattern

তুমি যেকোনো project-এ এই pattern চিনবে:

```python
# tasks.py

from celery import shared_task


@shared_task
def background_task(data_id):

    # expensive / background work

    pass
```

তারপর যেখানে দরকার:

```python
from .tasks import background_task

background_task.delay(data_id)
```

ব্যস।

---

# 11. কখন Celery ব্যবহার করবে?

এই ruleটা মনে রাখো:

### Normal কাজ

যেটা API response দেওয়ার আগে করতেই হবে:

```text
Validate
↓
Database operation
↓
Response
```

Celery লাগবে না।

### Background কাজ

যেটা পরে করলেও চলে:

```text
Email
Notification
Report
Image processing
Long calculation
External API
Periodic task
```

Celery ব্যবহার করতে পারো।

---

# 12. সবচেয়ে গুরুত্বপূর্ণ distinction

ধরো:

```python
product = Product.objects.create(
    name="Laptop"
)
```

এটা সাধারণত সরাসরি Django-তেই করবে।

তারপর:

```python
send_product_email.delay(product.id)
```

এটা background-এ পাঠাবে।

অর্থাৎ:

```text
Django
 │
 ├── Important DB work
 │        ↓
 │     PostgreSQL
 │
 └── Background work
          ↓
        Redis
          ↓
       Celery
```

**Database-এর critical operation অযথা Celery-তে পাঠাবে না।**

---

# 13. আরেকটা খুব useful pattern

Celery task-এ পুরো object পাঠানোর বদলে সাধারণত **ID পাঠানো ভালো**:

❌ এভাবে না:

```python
send_email.delay(order)
```

বরং:

```python
send_email.delay(order.id)
```

তারপর task:

```python
@shared_task
def send_email(order_id):

    order = Order.objects.get(id=order_id)

    # work
```

কারণ Celery queue-তে ছোট, serializable data পাঠানো সহজ এবং নির্ভরযোগ্য।

---

# 14. Celery-এর পুরো mental model

তুমি শুধু এই ৫টা জিনিস বুঝে রাখো:

```text
1. Task
      ↓
2. .delay()
      ↓
3. Redis Broker
      ↓
4. Celery Worker
      ↓
5. Task Execute
```

Example:

```python
@shared_task
def send_email(user_id):
    ...
```

↓

```python
send_email.delay(user_id)
```

↓

```text
Redis
```

↓

```text
Celery Worker
```

↓

```python
send_email(user_id)
```

এই pattern বুঝে গেলে **E-commerce, Blog, LMS, Booking, Social Media, SaaS—সব Django/DRF project-এ একই architecture apply করতে পারবে।**

---
অবশ্যই। এবার একটা **generic Django + DRF project-এ Celery + Redis পুরোপুরি implement করার জন্য কোন file কোথায় থাকবে এবং প্রতিটা file-এ কী লিখবে**—একদম copy-paste করার মতো করে দেখাচ্ছি।

আমরা এমন একটা example নেব যেটা পরে যেকোনো project-এ adapt করতে পারবে।

## Final architecture

```text
Client
  │
  │ POST /api/tasks/
  ▼
Django / DRF
  │
  │ task.delay()
  ▼
Redis
  │
  ▼
Celery Worker
  │
  ▼
Background Task
```

Project:

```text
myproject/
│
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── celery.py
│
└── core/
    ├── __init__.py
    ├── tasks.py
    ├── views.py
    └── urls.py
```

---

# 1. Project তৈরি

```bash
mkdir myproject
cd myproject

python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

Install:

```bash
pip install django djangorestframework celery redis
```

Project:

```bash
django-admin startproject config .
python manage.py startapp core
```

---

# 2. `settings.py`

`config/settings.py`

`INSTALLED_APPS`-এ:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "rest_framework",
    "core",
]
```

তারপর file-এর নিচে:

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

এটাই Celery-এর Redis broker।

---

# 3. `config/celery.py`

এই fileটা manually তৈরি করবে।

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

এখানে:

```python
app.autodiscover_tasks()
```

বলছে Django-এর installed apps-এর `tasks.py` খুঁজে বের করতে।

---

# 4. `config/__init__.py`

```python
from .celery import app as celery_app


__all__ = ("celery_app",)
```

এখন Django project-এর সাথে Celery properly connected।

---

# 5. `core/tasks.py`

এখানে background task থাকবে।

```python
from celery import shared_task


@shared_task
def send_notification(user_id):

    print(
        f"Sending notification to user {user_id}"
    )

    return "Notification sent successfully"
```

আরেকটা task:

```python
@shared_task
def generate_report(report_id):

    print(
        f"Generating report {report_id}"
    )

    return "Report generated successfully"
```

তাহলে পুরো `tasks.py`:

```python
from celery import shared_task


@shared_task
def send_notification(user_id):

    print(
        f"Sending notification to user {user_id}"
    )

    return "Notification sent successfully"


@shared_task
def generate_report(report_id):

    print(
        f"Generating report {report_id}"
    )

    return "Report generated successfully"
```

---

# 6. `core/views.py`

এখন DRF API থেকে Celery task call করব।

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .tasks import send_notification


class NotificationView(APIView):

    def post(self, request):

        user_id = request.data.get("user_id")

        if not user_id:
            return Response(
                {
                    "error": "user_id is required"
                },
                status=status.HTTP_400_BAD_REQUEST
            )

        send_notification.delay(user_id)

        return Response(
            {
                "message": "Notification task added to queue",
                "user_id": user_id
            },
            status=status.HTTP_202_ACCEPTED
        )
```

সবচেয়ে important line:

```python
send_notification.delay(user_id)
```

এটাই Django থেকে Celery-তে task পাঠাচ্ছে।

---

# 7. `core/urls.py`

```python
from django.urls import path

from .views import NotificationView


urlpatterns = [
    path(
        "notification/",
        NotificationView.as_view()
    ),
]
```

---

# 8. `config/urls.py`

```python
from django.contrib import admin
from django.urls import path, include


urlpatterns = [
    path("admin/", admin.site.urls),

    path(
        "api/",
        include("core.urls")
    ),
]
```

এখন endpoint:

```text
POST /api/notification/
```

---

# 9. Redis চালাও

Docker ব্যবহার করলে:

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

---

# 10. Django server চালাও

Terminal 1:

```bash
python manage.py runserver
```

---

# 11. Celery worker চালাও

Terminal 2:

```bash
celery -A config worker --loglevel=info
```

Worker চালু হলে `send_notification` task discover হওয়ার কথা।

---

# 12. API call করো

Postman দিয়ে:

```text
POST http://127.0.0.1:8000/api/notification/
```

Body:

```json
{
    "user_id": 10
}
```

Django response:

```json
{
    "message": "Notification task added to queue",
    "user_id": 10
}
```

কিন্তু আসল কাজটা Celery worker করবে।

Worker terminal-এ দেখতে পাবে task execute হয়েছে।

```text
Sending notification to user 10
```

---

# পুরো flow

এখন সবচেয়ে গুরুত্বপূর্ণ অংশটা দেখো:

```text
POST /api/notification/
          │
          ▼
     Django View
          │
          │
          ▼
send_notification.delay(10)
          │
          ▼
        Redis
          │
          ▼
    Celery Worker
          │
          ▼
send_notification(10)
```

---

# 13. Real project-এ কেমন হবে?

এখন `send_notification()` শুধু `print()` করছে।

বাস্তব project-এ এখানে actual কাজ করবে।

যেমন Email:

```python
from celery import shared_task
from django.core.mail import send_mail


@shared_task
def send_email(email, subject, message):

    send_mail(
        subject=subject,
        message=message,
        from_email="noreply@example.com",
        recipient_list=[email],
    )

    return "Email sent"
```

তারপর view:

```python
send_email.delay(
    "user@example.com",
    "Welcome",
    "Welcome to our platform!"
)
```

---

# 14. Database-এর সাথে Celery

ধরো তোমার `Order` model আছে।

```python
class Order(models.Model):
    user = models.ForeignKey(
        "auth.User",
        on_delete=models.CASCADE
    )

    total = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )
```

Task:

```python
from celery import shared_task

from .models import Order


@shared_task
def process_order(order_id):

    order = Order.objects.get(
        id=order_id
    )

    print(
        f"Processing order {order.id}"
    )

    return True
```

View:

```python
order = Order.objects.create(
    user=request.user,
    total=500
)

process_order.delay(order.id)
```

এখানে **পুরো object পাঠাবে না**:

```python
process_order.delay(order)
```

বরং:

```python
process_order.delay(order.id)
```

এটা সাধারণত cleaner pattern।

---

# 15. Task failure হলে retry

Production project-এ task fail করতে পারে।

যেমন external API unavailable।

তখন:

```python
from celery import shared_task


@shared_task(
    autoretry_for=(Exception,),
    retry_backoff=True,
    max_retries=3,
)
def process_order(order_id):

    # background work

    return True
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

---

# 16. Celery Beat — scheduled task

ধরো প্রতিদিন রাত ১২টায় একটা task চালাতে চাও।

`settings.py`:

```python
from celery.schedules import crontab


CELERY_BEAT_SCHEDULE = {
    "daily-report": {
        "task": "core.tasks.generate_report",
        "schedule": crontab(
            hour=0,
            minute=0
        ),
        "args": (1,),
    },
}
```

তারপর Beat চালাবে:

```bash
celery -A config beat --loglevel=info
```

Production-এ worker এবং beat সাধারণত আলাদা process হিসেবে চালানো হয়।

---

# 17. তাহলে complete project-এ কোন file-এর কী কাজ?

| File                 | কাজ                            |
| -------------------- | ------------------------------ |
| `config/celery.py`   | Celery initialize              |
| `config/__init__.py` | Django-র সাথে Celery load      |
| `settings.py`        | Redis broker configuration     |
| `tasks.py`           | Background tasks               |
| `views.py`           | `.delay()` দিয়ে task queue করা |
| `urls.py`            | API endpoint                   |
| Redis                | Task broker                    |
| Celery Worker        | Task execute                   |
| Celery Beat          | Scheduled task                 |

---

# 18. Generic template মনে রাখো

যেকোনো Django/DRF project-এ:

### `config/celery.py`

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

### `settings.py`

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"
```

### `tasks.py`

```python
from celery import shared_task


@shared_task
def my_background_task(object_id):

    # background work

    pass
```

### `views.py`

```python
from .tasks import my_background_task


my_background_task.delay(object_id)
```

### Worker

```bash
celery -A config worker --loglevel=info
```

এটাই তোমার **universal Celery pattern**।

```text
             ANY DRF PROJECT
                    │
                    ▼
              API / View
                    │
                    │ .delay(id)
                    ▼
                  Redis
                    │
                    ▼
             Celery Worker
                    │
                    ▼
               tasks.py
                    │
          ┌─────────┼──────────┐
          ▼         ▼          ▼
        Email   Notification  Report
```

**এই structure একবার বুঝে ফেললে project বদলালেও Celery-এর মূল setup বদলাবে না; মূলত `tasks.py`-এর business logic-টাই বদলাবে।**



---------
হ্যাঁ, **সাধারণত `views.py` থেকে Celery task call করা হয়**, যখন কোনো API request-এর কারণে background কাজ শুরু করতে হবে।

তবে একটা গুরুত্বপূর্ণ পার্থক্য আছে:

### `tasks.py`-এর function সরাসরি call করবে না

❌ এভাবে না:

```python
send_email(user_id)
```

বরং Celery দিয়ে:

```python
send_email.delay(user_id)
```

---

## পুরো flow

```text
Client
  ↓
DRF View
  ↓
task.delay()
  ↓
Redis
  ↓
Celery Worker
  ↓
tasks.py-এর function
```

### `tasks.py`

```python
from celery import shared_task


@shared_task
def send_email(user_id):
    print(f"Sending email to user {user_id}")
```

### `views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .tasks import send_email


class UserView(APIView):

    def post(self, request):

        user_id = request.user.id

        send_email.delay(user_id)

        return Response({
            "message": "User created successfully"
        })
```

এখানে:

```python
send_email.delay(user_id)
```

মানে **"এই task-টা এখনই আমার API process-এ চালিও না; Redis queue-তে পাঠাও, Celery worker পরে execute করবে।"**

---

## কিন্তু সবসময় View থেকে call করতে হবে না

যেখানে event ঘটছে, সেখান থেকেই task trigger করতে পারো।

যেমন **Django signal**:

```python
@receiver(post_save, sender=Order)
def order_created(sender, instance, created, **kwargs):

    if created:
        send_email.delay(instance.id)
```

তখন flow:

```text
Order created
     ↓
Signal
     ↓
send_email.delay()
     ↓
Redis
     ↓
Celery Worker
```

অথবা অন্য কোনো service/business logic থেকেও:

```python
send_email.delay(user.id)
```

### সহজ rule

```text
API request-এর কারণে task?
→ View থেকে .delay()

Database event-এর কারণে task?
→ Signal থেকে .delay()

অন্য business logic-এর কারণে task?
→ সেই service/function থেকে .delay()

Scheduled কাজ?
→ Celery Beat
```

আর **`tasks.py` মূলত task-এর কাজের definition রাখবে**; `.delay()` দিয়ে queue করা হবে যেখান থেকে কাজটি trigger হচ্ছে।


---
হ্যাঁ, এটা বুঝে ফেললে Celery অনেক সহজ হয়ে যাবে। `tasks.py`-এর task **কোথা থেকে call করলে কাজ করবে**—মূল বিষয় হলো task-কে `.delay()` দিয়ে queue করতে হবে।

## ১. View থেকে — সবচেয়ে common

যখন API request-এর কারণে background কাজ করতে হবে:

```python
# views.py

from .tasks import send_email

send_email.delay(user_id)
```

Flow:

```text
POST API
   ↓
View
   ↓
send_email.delay()
   ↓
Redis
   ↓
Celery Worker
   ↓
send_email()
```

---

## ২. অন্য Python service/function থেকে

ধরো তোমার project-এ `services.py` আছে:

```text
orders/
├── views.py
├── services.py
└── tasks.py
```

`services.py`:

```python
from .tasks import send_order_email


def create_order(user_id):

    # order create logic

    order_id = 10

    send_order_email.delay(order_id)

    return order_id
```

এটাও perfectly কাজ করবে।

---

## ৩. Django Signal থেকে

Database-এ নতুন object তৈরি হলে task চালাতে চাইলে:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

from .models import Order
from .tasks import send_order_email


@receiver(post_save, sender=Order)
def order_created(sender, instance, created, **kwargs):

    if created:
        send_order_email.delay(instance.id)
```

Flow:

```text
Order created
     ↓
Signal
     ↓
.delay()
     ↓
Redis
     ↓
Worker
```

---

## ৪. Celery Beat থেকে

যে task নির্দিষ্ট সময় পরপর চলবে:

```text
প্রতি ১ ঘণ্টা
প্রতি দিন
প্রতি সপ্তাহ
```

তখন View থেকে call করার দরকার নেই।

উদাহরণ:

```python
@shared_task
def generate_daily_report():
    print("Report generated")
```

Celery Beat এই task schedule করবে।

```text
Celery Beat
    ↓
Redis
    ↓
Celery Worker
    ↓
generate_daily_report()
```

---

## ৫. অন্য task থেকেও task call করা যায়

ধরো:

```python
@shared_task
def create_report():

    # report তৈরি

    send_email.delay()
```

অর্থাৎ একটা Celery task শেষ হওয়ার পরে আরেকটা task queue করতে পারে।

---

# তাহলে `tasks.py` থেকে task কোথা থেকে ব্যবহার করা যায়?

সহজভাবে:

```text
                  tasks.py
                     ▲
                     │
        ┌────────────┼────────────┐
        │            │            │
        │            │            │
      View        Service       Signal
        │            │            │
        └────────────┼────────────┘
                     │
                  .delay()
                     │
                     ▼
                   Redis
                     │
                     ▼
              Celery Worker
                     │
                     ▼
                Task runs
```

আর scheduled task হলে:

```text
Celery Beat
    ↓
 Redis
    ↓
Worker
    ↓
tasks.py
```

## সবচেয়ে important rule

`tasks.py`-এর function **সরাসরি call করলে**:

```python
send_email(user_id)
```

এটা সাধারণ Python function-এর মতো **সাথেসাথে execute হবে**।

Celery দিয়ে background-এ পাঠাতে:

```python
send_email.delay(user_id)
```

এটাই ব্যবহার করবে।

আর `.delay()` কাজ করার জন্য অবশ্যই:

```text
Redis চলছে
+
Celery Worker চলছে
```

থাকতে হবে।

**এক লাইনে মনে রাখো:**
`tasks.py` = *কাজটা কী হবে*
`.delay()` = *কাজটা queue-তে পাঠানো*
`Redis` = *queue/broker*
`Celery Worker` = *কাজটা execute করা*
