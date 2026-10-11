# Django-তে Gunicorn কীভাবে ব্যবহার করবে?

Django project production server-এ deploy করার সময় Gunicorn ব্যবহার করা হয় Django application চালানোর জন্য। বিশেষ করে তুমি যখন Django REST Framework (DRF) API-কে Docker ও Ubuntu VPS-এ deploy করবে, তখন Gunicorn একটি গুরুত্বপূর্ণ অংশ।

## ১. Gunicorn কী এবং কেন ব্যবহার করব?

Django-তে development করার সময় সাধারণত চালাও:

Bash

```
python manage.py runserver
```

এটি development-এর জন্য। Production-এ সাধারণত `runserver` ব্যবহার না করে Gunicorn-এর মতো WSGI application server ব্যবহার করা হয়।

Client / React / Next.js

API request পাঠায়

Nginx

HTTP/HTTPS, reverse proxy, static files

Gunicorn

Django application চালায় এবং request handle করে

Django → PostgreSQL

Business logic ও database operations

মনে রাখবে:

* Django — তোমার application-এর logic।

* Gunicorn — Django-কে production WSGI server-এর মাধ্যমে চালায়।

* Nginx — সাধারণত বাইরের HTTP/HTTPS request গ্রহণ করে Gunicorn-এ পাঠায়।

## ২. Gunicorn install করো

তোমার Django project folder-এ virtual environment activate করে install করো।

Bash

```
pip install gunicorn
```

তারপর `requirements.txt` update করো:

Bash

```
pip freeze > requirements.txt
```

এখন installed package-গুলোর মধ্যে `gunicorn` থাকবে।

## ৩. Django project-এর WSGI file খুঁজে বের করো

ধরো, তোমার project structure এমন:

```
myproject/
├── manage.py
├── requirements.txt
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
└── products/
    ├── models.py
    ├── views.py
    └── urls.py
```

Django project তৈরি করার সময় `wsgi.py` সাধারণত স্বয়ংক্রিয়ভাবে তৈরি হয়।

`config/wsgi.py`:

Python

Run

```
import os

from django.core.wsgi import get_wsgi_application

os.environ.setdefault(
    "DJANGO_SETTINGS_MODULE",
    "config.settings"
)

application = get_wsgi_application()
```

এখানে `config.settings` হলো settings module-এর path। তোমার project package-এর নাম আলাদা হলে সেটি অনুযায়ী path দিতে হবে।

## ৪. Gunicorn দিয়ে Django চালাও

`manage.py` যে folder-এ আছে, সেই folder থেকে চালাও:

Bash

```
gunicorn config.wsgi:application
```

এই command-এর অর্থ:

* `gunicorn` — server চালু করবে।

* `config.wsgi` — Django-র WSGI module।

* `application` — `wsgi.py`-তে তৈরি WSGI application object।

এবার browser বা API client থেকে `http://127.0.0.1:8000/` দিয়ে পরীক্ষা করতে পারো।

### নির্দিষ্ট host ও port-এ চালানো

Bash

```
gunicorn config.wsgi:application \
    --bind 127.0.0.1:8000
```

অথবা, Docker container-এর ভেতরে অন্য container থেকে access করার প্রয়োজন হলে:

Bash

```
gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000
```

পার্থক্য: `127.0.0.1` শুধু নিজের network interface-এ listen করে; `0.0.0.0` container-এর network interface-গুলোতে listen করতে দেয়। Production-এ সাধারণত Gunicorn port সরাসরি public internet-এ expose না করে Nginx-এর মাধ্যমে access করানো হয়।

## ৫. Production-এর জন্য workers ব্যবহার

Gunicorn একাধিক worker process চালাতে পারে। যেমন:

Bash

```
gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers 3 \
    --timeout 60 \
    --access-logfile - \
    --error-logfile -
```

| Option               | কাজ                                     |
| -------------------- | --------------------------------------- |
| `--bind`             | কোন address ও port-এ listen করবে        |
| `--workers 3`        | তিনটি worker process চালাবে             |
| `--timeout 60`       | worker response না দিলে timeout-এর সীমা |
| `--access-logfile -` | access log stdout-এ দেখাবে              |
| `--error-logfile -`  | error log stderr-এ দেখাবে               |

Worker সংখ্যা server-এর CPU, RAM এবং application-এর workload অনুযায়ী ঠিক করবে। শুরুতেই অনেক worker ব্যবহার করার প্রয়োজন নেই।

## ৬. Docker-এর মধ্যে Gunicorn ব্যবহার

যদি তোমার Django application Docker দিয়ে deploy করো, তাহলে `backend/Dockerfile`-এ Gunicorn-এর command এভাবে দিতে পারো।

dockerfile

```
CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

এখানে ধরে নেওয়া হয়েছে:

* `gunicorn` `requirements.txt`-এ আছে।

* Docker image-এর working directory-তে `manage.py` আছে।

* `config/wsgi.py` সঠিক path-এ আছে।

Docker Compose-এ backend service-এর জন্য:

YAML

```
services:
  backend:
    build: ./backend
    expose:
      - "8000"
    restart: unless-stopped
```

`expose` দিয়ে container-এর internal port উল্লেখ করা হয়েছে। Nginx একই Docker network-এ থাকলে `http://backend:8000` ব্যবহার করে Gunicorn-এ request পাঠাতে পারবে।

## ৭. Production-এ চালানোর আগে Django settings যাচাই করো

`settings.py`-তে অন্তত নিচের বিষয়গুলো নিশ্চিত করবে:

Python

Run

```
DEBUG = False

ALLOWED_HOSTS = [
    "api.example.com",
]
```

`api.example.com`-এর জায়গায় তোমার প্রকৃত API domain বসাবে। `SECRET_KEY`-এর মতো secret source code-এ hardcode না করে environment variable বা secret management দিয়ে দেবে।

Static files-এর জন্য `STATIC_ROOT` configure করে deployment-এর সময় `collectstatic` চালানোর ব্যবস্থাও রাখবে।

## ৮. Gunicorn কাজ করছে কি না পরীক্ষা

প্রথমে server চালু করো:

Bash

```
gunicorn config.wsgi:application \
    --bind 127.0.0.1:8000
```

অন্য terminal-এ:

Bash

```
curl -I http://127.0.0.1:8000/
```

Django-র root URL configured থাকলে response পাবে। Root URL না থাকলে `404`-ও আসতে পারে—এটি নিজে থেকে Gunicorn ব্যর্থ হওয়ার প্রমাণ নয়।

## তোমার জন্য শেখার সঠিক ক্রম

1. Gunicorn: Django-কে WSGI server দিয়ে চালানো।

2. Nginx: reverse proxy ও HTTPS configuration।

3. Docker Compose: Django + Gunicorn + PostgreSQL + Nginx একসঙ্গে চালানো।

4. Production deployment: Ubuntu VPS, domain, SSL, logs, health checks ও restart policy।

একটি বিষয় মনে রাখবে: Django-র asynchronous features বা ASGI-নির্ভর কাজের জন্য ASGI server যেমন Uvicorn বা Daphne উপযুক্ত হতে পারে। সাধারণ synchronous DRF API-এর জন্য Gunicorn একটি প্রচলিত পছন্দ।

পরের ধাপে Gunicorn + Nginx + Django + PostgreSQL দিয়ে একটি পূর্ণ production-ready Docker Compose configuration তৈরি করতে পারো। এতে প্রতিটি ফাইল, প্রতিটি configuration এবং deployment command ব্যাখ্যা করা যাবে।

হ্যাঁ, Nginx ছাড়াই Django-তে Gunicorn ব্যবহার করা যাবে। ✅

Gunicorn নিজেই Django application চালাতে পারে এবং HTTP request গ্রহণ করতে পারে। Nginx বাধ্যতামূলক নয়।

## ১. Nginx ছাড়া Gunicorn চালানো

প্রথমে install করো:

Bash

```
pip install gunicorn
```

তারপর `manage.py`-এর folder থেকে চালাও:

Bash

```
gunicorn config.wsgi:application --bind 0.0.0.0:8000
```

এখানে `config`-এর জায়গায় তোমার Django project package-এর নাম দেবে।

এখন একই কম্পিউটারে browser দিয়ে `http://127.0.0.1:8000` খুলে পরীক্ষা করতে পারবে।

## ২. Nginx ছাড়া বনাম Nginx-সহ

| বিষয়                  | শুধু Gunicorn                | Gunicorn + Nginx                 |
| --------------------- | ---------------------------- | -------------------------------- |
| Django চালানো         | হ্যাঁ                        | হ্যাঁ                            |
| HTTP request গ্রহণ    | হ্যাঁ                        | Nginx গ্রহণ করে Gunicorn-এ পাঠায় |
| Reverse proxy         | নেই                          | আছে                              |
| HTTPS/SSL             | আলাদাভাবে configure করতে হবে | Nginx-এ configure করা যায়        |
| Static/media files    | আলাদা ব্যবস্থা প্রয়োজন       | Nginx দিয়ে serve করা যায়         |
| Production deployment | সম্ভব                        | সাধারণত বেশি সুবিধাজনক           |

## ৩. কখন Nginx ছাড়া ব্যবহার করবে?

* Local development ও testing: শুধু Gunicorn যথেষ্ট।

* ছোট API বা internal service: প্রয়োজন অনুযায়ী শুধু Gunicorn ব্যবহার করা যায়।

* Public production website/API: Nginx বা অন্য reverse proxy/load balancer ব্যবহার করা সাধারণত ভালো।

মনে রেখো, Gunicorn একা HTTPS, static files, request filtering এবং reverse proxy-এর সব কাজ স্বয়ংক্রিয়ভাবে করে না। Production-এ শুধু Gunicorn ব্যবহার করলে নিরাপত্তা, TLS এবং static/media file serving-এর ব্যবস্থা আলাদাভাবে করতে হবে।

আমার পরামর্শ: তোমার Django REST Framework API Docker দিয়ে deploy করার ক্ষেত্রে প্রথমে শুধু Gunicorn দিয়ে কাজ বোঝো, এরপর Gunicorn + Nginx architecture শেখো।



