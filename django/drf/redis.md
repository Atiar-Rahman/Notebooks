
# 1️⃣ Redis কি?

**Redis** = **Re**mote **Di**ctionary **S**erver

* এটা **in-memory key-value store**
* Data **RAM এ save হয়**, তাই extremely fast
* Open-source এবং single-threaded design, কিন্তু extremely high-performance
* Key-value pairs, lists, sets, sorted sets, hashes, bitmaps, streams ইত্যাদি support করে

---

# 2️⃣ Redis কেন use করি?

Redis use করার মূল কারণ হলো **speed এবং efficiency**।

| Use case                     | Explanation                                                                            |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| **Cache**                    | Heavy queries or frequently used data RAM এ store করলে DB query কম হয়, site faster হয়। |
| **Message Broker / Queue**   | Celery এর মতো background task system কে message pass করার জন্য।                        |
| **Session store**            | Django sessions কে database এর চেয়ে দ্রুত manage করতে।                                 |
| **Rate Limiting / Counters** | API calls, login attempts ইত্যাদি track করা।                                           |
| **Pub/Sub**                  | Real-time chat or notifications।                                                       |

✅ মূলত: **যেখানে speed critical এবং frequent read/write হয়, সেখানে Redis best choice।**

---

# 3️⃣ Django context এ Redis এর use

1. **Celery broker** (Most common)

   * Celery task queue messages store করার জন্য
   * Example: background email sending, image processing, notifications

```python
# settings.py
CELERY_BROKER_URL = 'redis://localhost:6379/0'
CELERY_RESULT_BACKEND = 'redis://localhost:6379/0'
```

2. **Cache**

   * Django cache backend হিসেবে use করা যায়

```python
# settings.py
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://localhost:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
```

3. **Session storage**

   * DB session এর চেয়ে দ্রুত

```python
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "default"
```

---

# 4️⃣ Redis structure basics

* **Key-value store**: `SET key value`, `GET key`
* **Data types**:

  * Strings – normal key-value
  * Hashes – like dicts
  * Lists – ordered lists
  * Sets – unordered unique items
  * Sorted sets – like leaderboard
  * Streams – logs/events

```bash
# Redis CLI example
redis-cli
SET name "Atiar"
GET name
LPUSH tasks "task1"
LRANGE tasks 0 -1
```

---

# 5️⃣ Docker + Django + Redis

```yaml
services:
  redis:
    image: redis:7
    ports:
      - "6379:6379"

  celery:
    build: ./backend
    command: celery -A config worker --loglevel=info
    env_file:
      - ./.env
    depends_on:
      - redis
      - backend
```

* Redis container expose করে 6379 port
* Celery container Redis এর সাথে connect করে

---

# 6️⃣ Practical example

Suppose তুমি background email sending করতে চাও:

1. Install Celery + Redis Python library:

```bash
pip install celery redis
```

2. Django Celery config (`backend/celery.py`):

```python
import os
from celery import Celery

os.environ.setdefault("DJANGO_SETTINGS_MODULE", "config.settings")
app = Celery("backend")
app.config_from_object("django.conf:settings", namespace="CELERY")
app.autodiscover_tasks()
```

3. Create a task (`tasks.py`):

```python
from celery import shared_task
import time

@shared_task
def send_email_task(email):
    time.sleep(5)
    print(f"Email sent to {email}")
```

4. Run Redis + Celery + Django:

```bash
docker compose up -d redis backend celery
```

5. Call task from Django view:

```python
from .tasks import send_email_task

send_email_task.delay("user@example.com")
```

✅ Output: Celery worker Redis queue থেকে task read করে 5s পরে print করবে।

---

# 7️⃣ Summary

* **Redis = fast in-memory DB / broker / cache**
* **Where to use**:

  1. Celery broker / async tasks
  2. Cache frequent DB queries
  3. Session storage (fast)
  4. Pub/Sub / real-time notifications
* **Why use**: speed, scalability, distributed systems

---

💡 Tip: Redis use করা **অত্যন্ত common in production fullstack projects**—Celery ছাড়া almost কোনো large Django project production-ready হয় না।

---
