
# 1️⃣ Celery কি?

**Celery** হলো একটি **asynchronous task queue / job queue system**।

* মানে, তুমি কিছু কাজ **background এ** পাঠাতে পারো, যা main application thread block না করে চলে।
* Python-এ Django বা Flask সহ ব্যবহৃত হয়।
* Task কে queue তে push করা হয়, worker process পরে execute করে।

**Example:**

* তুমি একজন user কে email পাঠাতে চাও।
* যদি synchronous করো, page loading delay হবে যতক্ষণ email send হচ্ছে।
* Celery use করলে:

  1. User click → task push to queue
  2. Worker background এ email send
  3. User instant response পায়, task later execute হয়

---

# 2️⃣ কেন use করি?

| Reason                 | Explanation                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------- |
| **Background jobs**    | Heavy operations (emails, file processing, PDF generation) app response block না করে। |
| **Scheduled tasks**    | Cron job এর মতো periodic tasks (daily report, cleanup jobs) run করতে।                 |
| **Scalability**        | Multiple workers ব্যবহার করে tasks parallel run করা যায়।                             |
| **Retry & monitoring** | Failed tasks retry করা যায়, status track করা যায়।                                   |

---

# 3️⃣ কোথায় use হয়?

**Common use cases in Django / fullstack apps:**

1. **Email sending**

   * Registration confirmation
   * Newsletter / marketing emails

2. **File processing / Image processing**

   * User upload → resize / compress → save

3. **Data scraping / API calls**

   * Background data fetch / sync tasks

4. **Periodic / scheduled tasks**

   * Daily cleanup / report generation

5. **Notifications / messaging**

   * Push notification / SMS / chat messages

6. **Machine Learning tasks**

   * Model inference / training jobs in background

---

# 4️⃣ Celery architecture (simple)

```
Django App
   │
   │ push task
   ▼
Task Queue (Redis / RabbitMQ)
   │
   ▼
Worker Process (Celery)
   │
   ▼
Execute task + save result (optional)
```

* **Broker** → task queue: Redis / RabbitMQ
* **Worker** → background process executing task
* **Result backend** → optional, task result save করার জন্য (Redis / DB / Cache)

---

# 5️⃣ Django + Celery + Redis Example

**Install packages:**

```bash
pip install celery redis
```

**backend/celery.py**

```python
import os
from celery import Celery

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")

app = Celery("backend")
app.config_from_object("django.conf:settings", namespace="CELERY")
app.autodiscover_tasks()
```

**backend/settings.py (Redis broker)**

```python
CELERY_BROKER_URL = "redis://redis:6379/0"
CELERY_RESULT_BACKEND = "redis://redis:6379/0"
```

**tasks.py**

```python
from celery import shared_task
import time

@shared_task
def send_email_task(email):
    time.sleep(5)
    print(f"Email sent to {email}")
```

**Call task from view:**

```python
send_email_task.delay("user@example.com")
```

* `delay()` → task push to queue
* Worker → Redis থেকে task read করে execute করবে

---

# 6️⃣ Docker Compose এর মধ্যে Celery

```yaml
celery:
  build: ./backend
  command: celery -A config worker --loglevel=info
  env_file:
    - ./.env
  depends_on:
    - redis
    - backend
```

* Redis broker হিসাবে use হবে
* Worker automatically backend code load করবে

---

# 7️⃣ Summary

* **Celery = background task runner**
* **Why**: prevent blocking, handle heavy tasks, run periodic tasks, scale easily
* **Where**: email, notifications, file/image processing, ML tasks, scheduled jobs
* **How**: task push → Redis/RabbitMQ queue → Celery worker executes → optional result storage

---

💡 Tip: **Production-ready Django project এর 90% ক্ষেত্রে Celery + Redis combination essential।**

---

ভালো—এটা real production skill 🔥
আমি তোমাকে এমনভাবে দেখাচ্ছি যাতে **যেকোনো Django/DRF project-এ Celery + Redis implement করতে পারো** 👇

---

# 🎯 Celery + Redis কেন use করবো?

👉 যখন task:

* slow (email sending, image processing)
* heavy (bulk কাজ)
* background এ চালাতে চাই

👉 Example:

* bulk email 📧
* PDF generate
* notification system
* scheduled job (cron)

---

# 🧱 Step-by-Step Setup

## ✅ 1. Install dependencies

```bash
pip install celery redis django-celery-results
```

---

## ✅ 2. Redis install/run

👉 local:

```bash
sudo apt install redis
redis-server
```

👉 test:

```bash
redis-cli ping
# PONG আসলে ঠিক আছে
```

---

## ✅ 3. Project structure

```bash
myproject/
│
├── myproject/
│   ├── __init__.py
│   ├── celery.py   👈 main config
│   └── settings.py
│
├── app/
│   ├── tasks.py    👈 background task
```

---

## ⚙️ 4. celery.py (main setup)

```python
# myproject/celery.py

import os
from celery import Celery

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "myproject.settings")

app = Celery("myproject")

app.config_from_object("django.conf:settings", namespace="CELERY")

app.autodiscover_tasks()
```

---

## 🔗 5. **init**.py

```python
# myproject/__init__.py

from .celery import app as celery_app

__all__ = ("celery_app",)
```

---

## ⚙️ 6. settings.py config

```python
CELERY_BROKER_URL = "redis://127.0.0.1:6379/0"

CELERY_ACCEPT_CONTENT = ["json"]
CELERY_TASK_SERIALIZER = "json"

CELERY_RESULT_BACKEND = "redis://127.0.0.1:6379/0"
```

---

## ⚡ 7. tasks.py (example task)

```python
# app/tasks.py

from celery import shared_task
from django.core.mail import send_mail


@shared_task
def send_bulk_email(subject, message, emails):
    send_mail(
        subject,
        message,
        "no-reply@example.com",
        emails,
        fail_silently=False,
    )
```

---

## 🚀 8. Task call করা (view থেকে)

```python
# views.py

from app.tasks import send_bulk_email

def send_email_view(request):
    emails = ["user1@gmail.com", "user2@gmail.com"]

    send_bulk_email.delay(
        "Hello",
        "This is a test email",
        emails
    )

    return Response({"status": "Email भेज दिया 😄"})
```

👉 `.delay()` = async call

---

# ▶️ 9. Run services

### Redis run

```bash
redis-server
```

### Celery worker run

```bash
celery -A myproject worker --loglevel=info
```

👉 এখন task background এ run হবে 🔥

---

# ⏰ 10. Scheduled task (optional)

```bash
pip install django-celery-beat
```

👉 use case:

* daily email
* reminder system

---

# 🎯 কোথায় use করবা project এ?

## ✅ Perfect use cases

* 📧 bulk email (তোমার case)
* 🔔 notifications
* 📊 report generation
* 🖼️ image/video processing
* ⏰ scheduled jobs

---

## ❌ use করো না যখন

* simple CRUD
* fast response দরকার
* small logic

---

# 🔥 Real Flow

```text
User request →
    View →
        Celery task trigger →
            Redis queue →
                Worker process →
                    Task complete ✅
```

---

# ⚠️ Common mistakes

❌ Redis run না করা
❌ celery worker start না করা
❌ `.delay()` না use করা

---

# 🚀 Pro Tips

* production এ:

  * Redis separate server
  * multiple workers use করো
* logging enable করো
* retry use করো

---

# 💬 Final Summary

👉 Celery = worker (কাজ করে)
👉 Redis = broker (queue manage করে)
👉 Django = trigger করে

---


ঠিক আছে, তাহলে তোমার use case অনুযায়ী একটা **real DRF + JWT + Celery + Redis bulk email system** বানাই—যেটা তুমি সরাসরি project-এ use করতে পারো 🔥

---

# 🎯 Scenario

👉 Admin/group select করবে
👉 API call করবে
👉 background-এ email যাবে (non-blocking)

---

# 🧱 1. Model (Group + User)

```python
# users/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    group = models.CharField(max_length=50, blank=True, null=True)
```

---

# ⚙️ 2. JWT setup (assume already done)

```python
# settings.py

REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    )
}
```

---

# ⚡ 3. Celery task (email sending)

```python
# users/tasks.py

from celery import shared_task
from django.core.mail import send_mass_mail


@shared_task(bind=True, max_retries=3)
def send_group_email(self, subject, message, email_list):
    try:
        messages = [
            (subject, message, "no-reply@yourapp.com", [email])
            for email in email_list
        ]
        send_mass_mail(messages, fail_silently=False)

    except Exception as e:
        raise self.retry(exc=e, countdown=10)
```

👉 `retry` থাকায় fail হলে আবার try করবে 🔁

---

# 🌐 4. DRF API View

```python
# users/views.py

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated

from django.contrib.auth import get_user_model
from .tasks import send_group_email

User = get_user_model()


class SendGroupEmailView(APIView):
    permission_classes = [IsAuthenticated]

    def post(self, request):
        group = request.data.get("group")
        subject = request.data.get("subject")
        message = request.data.get("message")

        users = User.objects.filter(group=group)
        emails = list(users.values_list("email", flat=True))

        send_group_email.delay(subject, message, emails)

        return Response({
            "status": "Email sending started 🚀",
            "total_users": len(emails)
        })
```

---

# 🔗 5. URL

```python
# users/urls.py

from django.urls import path
from .views import SendGroupEmailView

urlpatterns = [
    path("send-email/", SendGroupEmailView.as_view()),
]
```

---

# ▶️ 6. Run system

```bash
redis-server
celery -A myproject worker --loglevel=info
python manage.py runserver
```

---

# 🧪 7. API Test (Postman)

```json
POST /api/send-email/

{
  "group": "A",
  "subject": "Hello Users",
  "message": "This is a bulk email"
}
```

---

# 🔥 Result

👉 API instantly response দিবে
👉 background-এ email যাবে
👉 server block হবে না 😎

---

# ⚠️ Important Tips

* Gmail use করলে:

  * App password লাগবে
* production:

  * SMTP (SendGrid, Mailgun) use করো
* large email list:

  * batch করে পাঠাও

---

# 🚀 Advanced Upgrade (optional)

👉 queue split:

```python
send_group_email.apply_async(args=[...], queue="emails")
```

👉 rate limit:

```python
@shared_task(rate_limit="10/m")
```

---

# 🎯 Final Architecture

```text
Frontend →
    DRF API →
        Celery task →
            Redis queue →
                Worker →
                    Email sent 📧
```

---

# 💬 Summary

* signal না ❌
* Celery use করো ✅
* async = fast + scalable

---

চাও তো আমি এটাকে next level নিয়ে গিয়ে:
👉 email template (HTML)
👉 progress tracking
👉 admin dashboard

add করে দিতে পারি 👍
সংক্ষেপে বলি—**production-এ `python manage.py runserver` ব্যবহার করা ঠিক না** ❌
এটা শুধু development server। Render বা Vercel-এ proper production setup দরকার।

---

# 🧠 কেন `runserver` না?

* single-threaded, slow ❌
* security/robustness কম ❌
* production traffic handle করার জন্য বানানো না ❌

---

# ✅ Production-এ কী ব্যবহার করবে?

## 🔥 Django app (Render/VPS ইত্যাদি)

👉 use করো:

* Gunicorn (WSGI apps-এর জন্য)

### Command:

```bash
gunicorn myproject.wsgi:application
```

👉 Render-এ সাধারণত Start Command:

```bash
gunicorn myproject.wsgi:application --bind 0.0.0.0:$PORT
```

---

# ⚡ Celery production-এ কিভাবে run করবে?

👉 আলাদা process হিসেবে:

### Worker:

```bash
celery -A myproject worker --loglevel=info
```

👉 Render-এ এটাকে **separate service/worker** হিসেবে run করো

---

# 🔴 Redis production-এ

👉 use করো managed Redis:

* Render Redis service
* বা Redis Cloud

---

# ❗ Vercel case (important)

👉 Vercel:

* ❌ Django full backend support করে না
* mainly serverless (Node/Edge)

👉 তাই:

* Django + Celery → Vercel এ run করা practical না ❌
* use:

  * Render ✅
  * Railway ✅
  * VPS ✅

---

# 🚀 Production Architecture

```text
User →
    Gunicorn (Django) →
        API →
            Celery Task →
                Redis →
                    Worker →
                        Email sent 📧
```

---

# 🎯 Render-এ setup summary

### Web Service:

```bash
gunicorn myproject.wsgi:application
```

### Worker Service:

```bash
celery -A myproject worker --loglevel=info
```

### Redis:

👉 Add Redis instance

---

# 💬 Final Summary

* ❌ `runserver` production-এ না
* ✅ Gunicorn use করো
* ✅ Celery worker আলাদা run করো
* ❌ Vercel Django full backend-এর জন্য ideal না

---

চাও তো আমি তোমার project অনুযায়ী **Render-এ deploy step-by-step (settings + env + start command)** করে দেখাতে পারি 👍
