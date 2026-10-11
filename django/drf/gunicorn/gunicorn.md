# Gunicorn কী এবং Django-তে কীভাবে কাজ করে?

তুমি যেহেতু Django ও Django REST Framework দিয়ে production-level backend তৈরি করতে চাও, তাই Gunicorn বোঝা খুবই গুরুত্বপূর্ণ। চলো, একদম beginner থেকে বাস্তব উদাহরণ দিয়ে শিখি।

## ১. Gunicorn কী?

Gunicorn (Green Unicorn) হলো Python-এর একটি WSGI HTTP server। এটি Django application-কে production environment-এ HTTP request handle করতে সাহায্য করে।

সহজভাবে বললে, তুমি Django দিয়ে API তৈরি করলে Gunicorn সেই application-কে production server থেকে request গ্রহণ করে process করতে সাহায্য করে।

Client / Browser / React Frontend

GET /api/products/

Nginx — Reverse Proxy

Request গ্রহণ ও forward করে

Gunicorn — WSGI Server

Django application-এ request পাঠায়

Django / DRF

URL → View → Model/Database → Response

JSON Response → Client

এখানে Nginx সামনে থেকে request নেয়, Gunicorn Django application চালায় এবং Django প্রয়োজনীয় data process করে response তৈরি করে।

## ২. Gunicorn কেন প্রয়োজন?

Django-তে development করার সময় আমরা সাধারণত এই command চালাই:

Bash

```
python manage.py runserver
```

এটি Django-র development server। এটি local development ও testing-এর জন্য, production deployment-এর জন্য নয়।

Production-এ সাধারণত ব্যবহার করা হয়:

* Gunicorn: Django application-এর request handle করার জন্য।

* Nginx: Reverse proxy, static/media file serving এবং অন্যান্য web-server কাজের জন্য।

* PostgreSQL: Database হিসেবে।

* Docker: Application ও dependencies container-এ চালানোর জন্য।

মনে রাখবে, Gunicorn database নয়, আবার এটি Nginx-এর বিকল্পও নয়।

## ৩. Django project-এ Gunicorn install করবে কীভাবে?

ধরি, তোমার Django project-এর structure এমন:

```
ecommerce/
├── manage.py
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── products/
    ├── models.py
    └── views.py
```

এখানে `config` হলো Django project package।

Step 1: Gunicorn install করো

Bash

```
pip install gunicorn
```

তোমার virtual environment active থাকা উচিত।

Step 2: Gunicorn চালাও

Project-এর root directory-তে, যেখানে `manage.py` আছে, চালাও:

Bash

```
gunicorn config.wsgi:application
```

এই command-এর অর্থ:

| অংশ           | অর্থ                                |
| ------------- | ----------------------------------- |
| `gunicorn`    | Gunicorn server চালাও               |
| `config.wsgi` | `config/wsgi.py` module import করো  |
| `application` | WSGI application object ব্যবহার করো |

Django-র `wsgi.py` ফাইলে সাধারণত এমন code থাকে:

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

এই `application` object-ই Gunicorn-কে Django application-এর সঙ্গে যুক্ত করে।

Step 3: নির্দিষ্ট port-এ চালাও

Bash

```
gunicorn config.wsgi:application --bind 127.0.0.1:8000
```

এখন Gunicorn local machine-এর `8000` port-এ listen করবে।

Browser বা API client দিয়ে পরীক্ষা করতে পারো:

```
http://127.0.0.1:8000/
```

তোমার URL configuration অনুযায়ী response পাবে।

## ৪. Gunicorn Workers কী?

এটি Gunicorn-এর সবচেয়ে গুরুত্বপূর্ণ concept-গুলোর একটি।

ধরো, তোমার e-commerce API-তে একই সময়ে ১০০ জন user request পাঠাচ্ছে। Gunicorn একাধিক worker process চালাতে পারে, যাতে request-গুলো একাধিক process-এর মধ্যে handle হয়।

Gunicorn Master Process

Worker process পরিচালনা করে

Worker 1

Request handle

Worker 2

Request handle

Worker 3

Request handle

Worker 4

Request handle

চারটি worker দিয়ে চালানোর উদাহরণ:

Bash

```
gunicorn config.wsgi:application \
    --workers 4 \
    --bind 127.0.0.1:8000
```

এখানে `--workers 4` মানে চারটি worker process চালানোর নির্দেশ দেওয়া হয়েছে।

তবে ৪টি worker মানেই ঠিক ৪টি request একসঙ্গে handle করা যাবে—এমন নয়। Request-এর ধরন, worker class, database latency এবং server resources-এর ওপর concurrency নির্ভর করে। সাধারণ synchronous worker-এ প্রতিটি worker এক সময়ে একটি request handle করে।

## ৫. Gunicorn-এর গুরুত্বপূর্ণ options

| Option               | কাজ                                                |
| -------------------- | -------------------------------------------------- |
| `--bind`             | কোন IP ও port-এ listen করবে                        |
| `--workers`          | কতটি worker process চালাবে                         |
| `--timeout`          | worker কতক্ষণ response না দিলে timeout হবে         |
| `--access-logfile -` | Access log terminal-এ দেখাবে                       |
| `--error-logfile -`  | Error log terminal-এ দেখাবে                        |
| `--reload`           | Code পরিবর্তন হলে development-এ server reload করবে |

Production-এর একটি সাধারণ উদাহরণ:

Bash

```
gunicorn config.wsgi:application \
    --bind 127.0.0.1:8000 \
    --workers 3 \
    --timeout 60 \
    --access-logfile - \
    --error-logfile -
```

Worker সংখ্যা বেছে নেওয়ার সময় CPU, RAM এবং workload বিবেচনা করবে। ছোট server-এ বেশি worker দিলে উল্টো memory pressure তৈরি হতে পারে।

## ৬. Docker ও Nginx-এর সঙ্গে Gunicorn

তোমার Django + React project production-এ deploy করলে architecture এমন হতে পারে:

Internet

Nginx Container

Port 80/443 · Reverse proxy

Django Container

Gunicorn → Django REST Framework

PostgreSQL Container / Database Server

Docker Compose-এ Django service-এর command হতে পারে:

YAML

```
services:
  backend:
    build: ./backend
    command: gunicorn config.wsgi:application --bind 0.0.0.0:8000 --workers 3
    expose:
      - "8000"
```

এটি একটি আংশিক উদাহরণ। বাস্তবে `Dockerfile`, environment variables, database connection এবং Nginx configuration-ও লাগবে। Docker network-এ Nginx সাধারণত `backend:8000` ঠিকানায় Django service-এ request পাঠাবে।

আরেকটি বিষয়: Gunicorn হলো WSGI server। Django-তে WebSocket বা ASGI-ভিত্তিক real-time feature, যেমন Django Channels, চালাতে সাধারণত উপযুক্ত ASGI server ব্যবহার করতে হয়।

## ৭. এবার নিজে practice করো

এই তিনটি command-এর কাজ বোঝার চেষ্টা করো:

Bash

```
python manage.py runserver
```

Bash

```
gunicorn config.wsgi:application --bind 127.0.0.1:8000
```

Bash

```
gunicorn config.wsgi:application --workers 4 --bind 127.0.0.1:8000
```

প্রথমটি Django development server চালায়। দ্বিতীয়টি Gunicorn দিয়ে Django চালায়। তৃতীয়টি চারটি worker process ব্যবহার করে Gunicorn চালায়।

পরবর্তী ধাপে তোমার জন্য সবচেয়ে কাজে লাগবে: Django + Gunicorn + Nginx + Docker দিয়ে একটি বাস্তব production deployment তৈরি করা—`Dockerfile`, `docker-compose.yml`, Nginx configuration এবং worker tuning-সহ।

---
# Django + Gunicorn + Nginx + Docker: Production Deployment

চলো, একটি বাস্তব Django REST Framework backend production-এ deploy করার মতো করে তৈরি করি। আমরা ধাপে ধাপে শিখব—কোন ফাইল কেন দরকার, কীভাবে request flow করে এবং Docker-এর মাধ্যমে সব service একসঙ্গে কীভাবে চালাতে হয়।

আমরা ধরে নিচ্ছি তোমার project-এ Django/DRF API আছে এবং PostgreSQL database ব্যবহার করবে।

## ১. পুরো architecture বুঝে নাও

React / Next.js frontend

API request পাঠায়

Nginx container

HTTP/HTTPS · Reverse proxy

Gunicorn container

WSGI server · Worker processes

Django REST Framework

PostgreSQL

Persistent database storage

প্রতিটি অংশের কাজ আলাদা:

* Docker: প্রতিটি service-কে container-এ চালায়।

* Gunicorn: Django application-এর WSGI request handle করে।

* Nginx: বাইরের request গ্রহণ করে Gunicorn-এ পাঠায়।

* PostgreSQL: application data সংরক্ষণ করে।

এখানে Docker নিজে web server নয়, আর Gunicorn নিজে database-ও নয়।

## ২. Project structure তৈরি করো

প্রথমে তোমার project-কে এভাবে সাজানো যেতে পারে:

```
myproject/
├── backend/
│   ├── manage.py
│   ├── requirements.txt
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── config/
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   └── products/
│       ├── models.py
│       ├── views.py
│       └── ...
├── nginx/
│   └── default.conf
├── docker-compose.yml
└── .env
```

`config`-এর জায়গায় তোমার Django project package-এর প্রকৃত নাম বসাতে হবে। যেমন, তোমার package-এর নাম `core` হলে `config.wsgi:application`-এর বদলে `core.wsgi:application` ব্যবহার করবে।

## ৩. Django-এর requirements তৈরি করো

`backend/requirements.txt`

```
Django
djangorestframework
gunicorn
psycopg[binary]
```

এগুলো minimum example dependencies। তোমার project-এ ব্যবহৃত package-গুলোও এখানে রাখতে হবে। Production-এ tested version pin করে রাখা উচিত।

## ৪. Dockerfile তৈরি করো

`backend/Dockerfile`

dockerfile

```
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       libpq5 \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN addgroup --system django \
    && adduser --system --ingroup django django \
    && mkdir -p /app/staticfiles /app/media \
    && chown -R django:django /app

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

এখানে কী হচ্ছে?

1. `FROM` Python runtime image নির্বাচন করে।

2. `WORKDIR` container-এর working directory নির্ধারণ করে।

3. `COPY` dependency ও project code container-এ রাখে।

4. `pip install` প্রয়োজনীয় package install করে।

5. `USER django` application-কে non-root user হিসেবে চালায়।

6. `CMD` Gunicorn চালু করে।

খেয়াল করো, এখানে `config.wsgi:application` তোমার প্রকৃত Django package name দিয়ে পরিবর্তন করতে হবে।

## ৫. `.dockerignore` তৈরি করো

`backend/.dockerignore`

```
.git/
.venv/
venv/
__pycache__/
*.py[cod]
.env
.pytest_cache/
.coverage
media/
staticfiles/
```

এটি অপ্রয়োজনীয় ফাইল Docker build context-এ যাওয়া কমায়। বিশেষ করে `.env` এবং secret-গুলো image-এ copy হওয়া ঠেকানো জরুরি।

## ৬. Environment variables তৈরি করো

Project root-এর `.env` ফাইলে রাখো:

dotenv

```
DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1

POSTGRES_DB=ecommerce
POSTGRES_USER=ecommerce_user
POSTGRES_PASSWORD=replace-with-a-strong-password
POSTGRES_HOST=db
POSTGRES_PORT=5432
```

এগুলো example value। Production-এ শক্তিশালী secret ও password ব্যবহার করবে। `.env` Git-এ commit করবে না।

### Django `settings.py`-তে environment variables পড়া

প্রয়োজন হলে `django-environ` ব্যবহার করতে পারো। এখানে built-in Python দিয়ে সাধারণ উদাহরণ:

Python

Run

```
import os

SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]

DEBUG = os.environ.get("DJANGO_DEBUG", "False").lower() == "true"

ALLOWED_HOSTS = [
    host.strip()
    for host in os.environ.get(
        "DJANGO_ALLOWED_HOSTS", ""
    ).split(",")
    if host.strip()
]

DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": os.environ["POSTGRES_DB"],
        "USER": os.environ["POSTGRES_USER"],
        "PASSWORD": os.environ["POSTGRES_PASSWORD"],
        "HOST": os.environ.get("POSTGRES_HOST", "db"),
        "PORT": os.environ.get("POSTGRES_PORT", "5432"),
    }
}

STATIC_URL = "static/"
STATIC_ROOT = "/app/staticfiles"

MEDIA_URL = "media/"
MEDIA_ROOT = "/app/media"
```

এই settings তোমার বিদ্যমান `settings.py`-এর সঙ্গে merge করবে; পুরো ফাইল অন্ধভাবে replace করবে না। আগে থেকে database বা static settings থাকলে duplicate configuration সরিয়ে নেবে।

Production-এ HTTPS চালু হলে secure cookie, CSRF trusted origins এবং HTTPS redirect-ও সঠিকভাবে configure করতে হবে।

## ৭. Docker Compose তৈরি করো

Project root-এ `docker-compose.yml` ফাইল তৈরি করো।

YAML

```
services:
  backend:
    build:
      context: ./backend
    env_file:
      - .env
    expose:
      - "8000"
    volumes:
      - static_volume:/app/staticfiles
      - media_volume:/app/media
    depends_on:
      db:
        condition: service_healthy
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - static_volume:/app/staticfiles:ro
      - media_volume:/app/media:ro
    depends_on:
      - backend
    restart: unless-stopped

  db:
    image: postgres:16
    env_file:
      - .env
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped

volumes:
  postgres_data:
  static_volume:
  media_volume:
```

### Compose ফাইলের গুরুত্বপূর্ণ বিষয়

* `backend`-এ Gunicorn চলবে।

* `nginx` বাইরের HTTP request গ্রহণ করবে।

* `db`-তে PostgreSQL চলবে।

* `postgres_data` container পুনরায় তৈরি হলেও database data ধরে রাখবে।

* `static_volume` ও `media_volume` static এবং uploaded media file সংরক্ষণের জন্য।

* `expose: 8000` শুধু Docker network-এ backend port-টি প্রকাশ করে; এটি host machine-এ port publish করে না।

গুরুত্বপূর্ণ: PostgreSQL volume persistent হলেও আলাদা backup নিতে হবে। আর `depends_on` database ready হওয়া নিশ্চিত করে, কিন্তু Django migration স্বয়ংক্রিয়ভাবে চালায় না।

## ৮. Nginx configuration তৈরি করো

`nginx/default.conf`

Nginx

```
upstream django_backend {
    server backend:8000;
}

server {
    listen 80;
    server_name localhost;

    client_max_body_size 20M;

    location /static/ {
        alias /app/staticfiles/;
    }

    location /media/ {
        alias /app/media/;
    }

    location / {
        proxy_pass http://django_backend;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

এখানে:

* `upstream django_backend` backend service-এর ঠিকানা নির্ধারণ করে।

* `proxy_pass` request Gunicorn-এ পাঠায়।

* `/static/` Django-র collected static file পরিবেশন করে।

* `/media/` uploaded media file পরিবেশন করে।

* `client_max_body_size 20M` সর্বোচ্চ request body size নির্ধারণ করে।

`server_name localhost` এই local example-এর জন্য। Public server-এ তোমার domain name বসাতে হবে।

## ৯. Application চালু করো

Project root-এ terminal খুলে নিচের ধাপগুলো অনুসরণ করো।

ধাপ ১ — Configuration পরীক্ষা

Bash

```
docker compose config
```

এতে Compose configuration ও variable substitution-এর সমস্যা খুঁজে পাওয়া সহজ হবে। এটি secret-সহ configuration output করতে পারে, তাই output প্রকাশ করার সময় সতর্ক থাকবে।

ধাপ ২ — Image build ও service চালু

Bash

```
docker compose up -d --build
```

ধাপ ৩ — Database migration চালাও

Bash

```
docker compose exec backend python manage.py migrate
```

প্রথমবার backend container চালু হওয়ার পর এটি চালাবে। নতুন deployment-এ migration চালানোর আগে backup ও migration compatibility যাচাই করবে।

ধাপ ৪ — Static files collect করো

Bash

```
docker compose exec backend python manage.py collectstatic --noinput
```

ধাপ ৫ — Service ও log পরীক্ষা

Bash

```
docker compose ps
```

Bash

```
docker compose logs -f backend nginx db
```

তারপর browser বা API client-এ পরীক্ষা করো:

```
http://localhost/
```

তোমার root URL configure করা না থাকলে `404 Not Found` আসতে পারে; সেটি একাই server failure প্রমাণ করে না। নিজের API endpoint দিয়ে পরীক্ষা করো, যেমন `/api/v1/products/`।

## ১০. Gunicorn worker tuning কীভাবে করবে?

শুরুতে তিনটি worker দিয়ে পরীক্ষা করতে পারো:

Bash

```
gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers 3 \
    --timeout 60
```

Worker সংখ্যা নির্বাচন করার জন্য কোনো একটিমাত্র formula সব application-এর ক্ষেত্রে সঠিক নয়। CPU, RAM, database latency, request-এর সময়কাল এবং concurrency বিবেচনা করতে হবে।

তোমার কম্পিউটারে ১৬ GB RAM থাকলেও production server-এর resource আলাদা হতে পারে। তাই server-এর RAM না জেনে বেশি worker configure করবে না।

একটি practical পদ্ধতি:

1. প্রথমে ২–৩টি worker দিয়ে শুরু করো।

2. API load test চালাও।

3. CPU, memory, response time এবং database connection পর্যবেক্ষণ করো।

4. Worker সংখ্যা পরিবর্তন করে ফলাফল তুলনা করো।

5. দীর্ঘ request বা timeout হলে কারণ অনুসন্ধান করো; শুধু timeout বাড়িয়ে সমস্যাটি ঢেকে রেখো না।

## ১১. Production-এ যাওয়ার আগে checklist

## Deployment checklist

0/10 সম্পন্ন

DEBUG=False এবং শক্তিশালী SECRET_KEY

ALLOWED_HOSTS ও CSRF settings সঠিক

HTTPS ও TLS certificate configure করা

Database backup ও restore পরীক্ষা

Migration strategy নির্ধারণ

Static ও media storage যাচাই

Authentication, permissions ও file upload security পরীক্ষা

Logs, health checks ও monitoring

Dependency version pin এবং vulnerability পরীক্ষা

Gunicorn worker ও resource load test

এটি একটি শেখার উপযোগী production-style starting point; public production deployment-এর জন্য এখনো HTTPS, secret management, backup, monitoring এবং security review প্রয়োজন। Nginx-এর এই configuration-এ WebSocket proxy-ও configure করা হয়নি।

## এরপর কোন ধাপে যাবে?

পর্ব ২ — Docker networking ও volumes

Container-to-container communication, persistent storage এবং build optimization।

এই পর্ব শেখাও

পর্ব ৩ — VPS-এ বাস্তব deployment

Ubuntu server, domain, HTTPS, firewall, Nginx ও deployment updates।

VPS deployment শেখাও


----
# Django Production Deployment Course — Part 2

## Docker Networking, Volumes, Bind Mounts ও Named Volumes

এই পর্বে আমরা আগের Django + Gunicorn + Nginx + PostgreSQL project-টিকে আরও ভালোভাবে বুঝব। শুধু configuration মুখস্থ নয়—প্রতিটি জিনিস কেন ব্যবহার করি, কীভাবে কাজ করে এবং সমস্যা হলে কীভাবে debug করতে হয়, তা হাতে-কলমে শিখব।

এই পর্ব শেষে তুমি বুঝতে পারবে:

* Docker container কীভাবে অন্য container-এর সঙ্গে যোগাযোগ করে।

* Django container থেকে PostgreSQL-এ কীভাবে connect করতে হয়।

* Named volume ও bind mount-এর পার্থক্য।

* Container delete করলেও database data কীভাবে রাখা যায়।

* Nginx কীভাবে Gunicorn-এর সঙ্গে যোগাযোগ করে।

* Docker networking ও storage-এর সাধারণ ভুলগুলো কীভাবে ঠিক করতে হয়।

# Part 1: Docker Networking

## ১. Docker Network কী?

ধরো, তোমার application-এ তিনটি container আছে:

* `backend` — Django + Gunicorn

* `db` — PostgreSQL

* `nginx` — Reverse proxy

প্রতিটি container আলাদা environment-এ চলে। তাদের মধ্যে যোগাযোগের জন্য Docker network ব্যবহার করা হয়।

Docker Network: `app_network`

একই network-এ যুক্ত container-গুলো

Nginx

:80

Django

:8000

PostgreSQL

:5432

একই network-এ service name দিয়ে একে অন্যকে খুঁজে পাওয়া যায়।

এখানে port-গুলোর অর্থ:

| Port   | Service       |
| ------ | ------------- |
| `80`   | Nginx-এর HTTP |
| `8000` | Gunicorn      |
| `5432` | PostgreSQL    |

Port number-গুলো default/example। Configuration-এ এগুলো পরিবর্তন করা যায়।

## ২. Container-এর IP ব্যবহার না করে service name কেন ব্যবহার করব?

ধরো, Django container থেকে PostgreSQL-এ connect করবে।

ভুল বা অনির্ভরযোগ্য পদ্ধতি:

Python

Run

```
"HOST": "172.20.0.5"
```

এই IP পরিবর্তিত হতে পারে, যেমন container পুনরায় তৈরি হলে।

Docker Compose-এর network-এ সঠিক পদ্ধতি:

Python

Run

```
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "ecommerce",
        "USER": "ecommerce_user",
        "PASSWORD": "your-password",
        "HOST": "db",
        "PORT": "5432",
    }
}
```

এখানে `db` হলো Compose service name।

মনে রাখবে: Django container-এর ভেতরে `localhost` মানে Django container নিজেই। PostgreSQL অন্য container-এ থাকলে database host হিসেবে `localhost` ব্যবহার করলে সাধারণত connection fail হবে।

## ৩. Hands-on: Docker Compose network তৈরি করা

আগের project structure ব্যবহার করো:

```
myproject/
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   └── config/
├── nginx/
│   └── default.conf
├── docker-compose.yml
└── .env
```

Compose file-এ আমরা একটি custom network স্পষ্টভাবে তৈরি করব।

`docker-compose.yml`

YAML

```
services:
  backend:
    build:
      context: ./backend
    env_file:
      - .env
    networks:
      - app_network
    expose:
      - "8000"
    depends_on:
      db:
        condition: service_healthy
    restart: unless-stopped

  db:
    image: postgres:16
    env_file:
      - .env
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app_network
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    networks:
      - app_network
    depends_on:
      - backend
    restart: unless-stopped

networks:
  app_network:
    driver: bridge

volumes:
  postgres_data:
```

এটি আগের configuration-এর একটি network-focused version। এখানে static ও media volume বাদ রাখা হয়েছে যাতে networking-এর বিষয়টি পরিষ্কার থাকে।

### Service-গুলো কীভাবে যোগাযোগ করে?

Nginx configuration:

Nginx

```
upstream django_backend {
    server backend:8000;
}

server {
    listen 80;

    location / {
        proxy_pass http://django_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Nginx `backend:8000` ব্যবহার করছে, কারণ `backend` হলো Django service-এর নাম।

Django একইভাবে database-এর host হিসেবে `db` ব্যবহার করবে।

## ৪. Network-সংক্রান্ত commands

প্রথমে service চালু করো:

Bash

```
docker compose up -d --build
```

Network-এর তালিকা দেখো:

Bash

```
docker network ls
```

Compose project-এর network-এর বিস্তারিত দেখো:

Bash

```
docker network inspect <project-name>_app_network
```

কোন container চলছে:

Bash

```
docker compose ps
```

Django container-এর shell-এ ঢোকো:

Bash

```
docker compose exec backend sh
```

তারপর shell থেকে বের হতে:

Bash

```
exit
```

Debugging tip: Django থেকে `db:5432`-এ connection fail করলে প্রথমে যাচাই করবে—database healthy কি না, উভয় service একই network-এ আছে কি না, environment variables সঠিক কি না এবং PostgreSQL initialization সম্পন্ন হয়েছে কি না।

# Part 2: Docker Volumes

## ৫. Volume কেন প্রয়োজন?

ধরো, তোমার e-commerce application-এ ১০,০০০টি product আছে। PostgreSQL container-এ data রাখা হচ্ছে।

যদি container সরিয়ে নতুন container তৈরি করো, container-এর writable layer-এর data স্থায়ীভাবে রাখার নিশ্চয়তা নেই। তাই database-এর data container-এর বাইরে persistent storage-এ রাখতে হয়।

Docker volume এই কাজের একটি standard উপায়।

PostgreSQL Container

PostgreSQL process + database files

Persistent storage mount

Named Volume: `postgres_data`

Container-এর lifecycle থেকে আলাদা storage

এখানে volume container-এর বাইরে managed storage হিসেবে থাকে। Container recreate হলেও volume মুছে না ফেললে data টিকে থাকতে পারে।

তবে volume মানেই backup নয়। Disk failure, accidental deletion বা data corruption থেকে সুরক্ষার জন্য আলাদা backup দরকার।

## ৬. Named Volume কী?

Named volume হলো Docker-কে দিয়ে তৈরি ও পরিচালিত persistent storage, যেটিকে একটি নাম দিয়ে ব্যবহার করা হয়।

উদাহরণ:

YAML

```
services:
  db:
    image: postgres:16
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

এখানে:

* `postgres_data` হলো volume-এর নাম।

* `/var/lib/postgresql/data` হলো PostgreSQL container-এর ভেতরের directory।

* PostgreSQL-এর data ওই mount-এ লেখা হয়।

### Named volume তৈরি ও পরীক্ষা

Compose চালাও:

Bash

```
docker compose up -d
```

Volume তালিকা:

Bash

```
docker volume ls
```

নির্দিষ্ট volume-এর তথ্য:

Bash

```
docker volume inspect <project-name>_postgres_data
```

Compose project-এর নাম অনুযায়ী volume-এর আসল নাম আলাদা হতে পারে। `docker volume ls` থেকে সঠিক নাম দেখবে।

### Container recreate করলে কী হয়?

Bash

```
docker compose up -d --force-recreate db
```

এতে database container recreate হতে পারে, কিন্তু named volume মুছে ফেলা হয় না। PostgreSQL একই volume ব্যবহার করলে আগের data পাওয়া যায়।

সতর্কতা: production database-এ এ ধরনের operation-এর আগে backup এবং service impact যাচাই করবে।

## ৭. Bind Mount কী?

Bind mount হলো host machine-এর একটি নির্দিষ্ট file বা directory-কে container-এর ভেতরে mount করা।

ধরো, তোমার কম্পিউটারে Django project আছে:

```
/home/atiar/myproject/backend/
```

তুমি এই directory-কে container-এর `/app` directory হিসেবে ব্যবহার করতে পারো।

YAML

```
services:
  backend:
    build:
      context: ./backend
    volumes:
      - ./backend:/app
```

এখন host machine-এ `views.py` পরিবর্তন করলে সেই পরিবর্তন container-এর `/app` directory-তেও দেখা যাবে।

এটি local development-এ খুবই সুবিধাজনক।

### Bind mount-এর ব্যবহার

Host machine

backend/products/views.py

Code edit করো।

Django container

/app/products/views.py

একই file content দেখা যায়।

এখানে একটি গুরুত্বপূর্ণ বিষয়: file পরিবর্তন container-এ দেখা গেলেও Gunicorn নিজে থেকে reload করবে এমন নয়। Development-এ `--reload` ব্যবহার করা যায়; production-এ সাধারণত image rebuild করে controlled deployment করা হয়।

## ৮. Named Volume বনাম Bind Mount

| বিষয়                       | Named Volume                            | Bind Mount                                 |
| -------------------------- | --------------------------------------- | ------------------------------------------ |
| Storage location           | Docker পরিচালনা করে                     | Host-এর নির্দিষ্ট path                     |
| প্রধান ব্যবহার             | Database, persistent application data   | Development source code, নির্দিষ্ট config  |
| Host path নিজে নির্বাচন    | সাধারণত না                              | হ্যাঁ                                      |
| Source code edit-এর সুবিধা | সাধারণত কম                              | খুব ভালো                                   |
| Container delete করলে      | সাধারণত থাকে                            | Host-এর মূল file থাকে                      |
| `docker compose down -v`   | সংশ্লিষ্ট Compose volume মুছে দিতে পারে | Host-এর original directory সাধারণত মুছে না |

Production-এ সাধারণত PostgreSQL-এর জন্য named volume এবং development-এর জন্য source-code bind mount ব্যবহার করা হয়।

# Part 3: Hands-on — Django + PostgreSQL persistence

## ৯. একটি বাস্তব পরীক্ষা করো

প্রথমে database container চালু করো:

Bash

```
docker compose up -d db
```

তারপর PostgreSQL-এ একটি table ও row তৈরি করো। এখানে ধরে নেওয়া হচ্ছে `.env`-এ `POSTGRES_DB`, `POSTGRES_USER` এবং `POSTGRES_PASSWORD` আছে।

Bash

```
docker compose exec db sh -c \
  'psql -U "$POSTGRES_USER" -d "$POSTGRES_DB"'
```

PostgreSQL prompt-এ চালাও:

SQL

```
CREATE TABLE deployment_test (
    id SERIAL PRIMARY KEY,
    message TEXT NOT NULL
);

INSERT INTO deployment_test (message)
VALUES ('My data survives container recreation');
```

Data পরীক্ষা করো:

SQL

```
SELECT * FROM deployment_test;
```

তারপর PostgreSQL shell থেকে বের হও:

SQL

```
\q
```

এবার container recreate করো:

Bash

```
docker compose up -d --force-recreate db
```

আবার database-এ connect করে query চালাও:

SQL

```
SELECT * FROM deployment_test;
```

আগের data পাওয়া উচিত, কারণ `postgres_data` volume ব্যবহার করা হচ্ছে।

কেন এই পরীক্ষা গুরুত্বপূর্ণ? এতে তুমি বুঝতে পারবে container আর database data একই জিনিস নয়। Container হলো service চালানোর environment, আর volume হলো persistent storage।

পরীক্ষা শেষ হলে table মুছতে চাইলে:

SQL

```
DROP TABLE deployment_test;
```

এটি শুধু এই test table মুছবে; volume মুছবে না।

# Part 4: Django Static Files ও Media Files

## ১০. Static ও media file কি একই?

না, দুটির উদ্দেশ্য আলাদা।

* Static files: CSS, JavaScript, logo, icon—application-এর frontend asset।

* Media files: User upload করা ছবি, product image, profile photo বা অন্যান্য uploaded file।

Django-তে সাধারণত:

Python

Run

```
STATIC_URL = "static/"
STATIC_ROOT = "/app/staticfiles"

MEDIA_URL = "media/"
MEDIA_ROOT = "/app/media"
```

এখন Compose-এ দুইটি named volume যোগ করতে পারো:

YAML

```
services:
  backend:
    volumes:
      - static_volume:/app/staticfiles
      - media_volume:/app/media

  nginx:
    volumes:
      - static_volume:/app/staticfiles:ro
      - media_volume:/app/media:ro

volumes:
  static_volume:
  media_volume:
```

এখানে `:ro` মানে read-only। Nginx file পড়তে পারবে, কিন্তু এই mount দিয়ে file পরিবর্তন করতে পারবে না।

Django-র static files collect করতে:

Bash

```
docker compose exec backend \
  python manage.py collectstatic --noinput
```

Nginx configuration:

Nginx

```
location /static/ {
    alias /app/staticfiles/;
}

location /media/ {
    alias /app/media/;
}
```

এই configuration-এ Nginx volume থেকে static ও media file serve করতে পারে।

Production security-এর জন্য মনে রাখবে: user-uploaded media file সবসময় public হওয়া উচিত নয়। Private document বা sensitive evidence থাকলে authenticated access-এর ব্যবস্থা করতে হবে। বড় production system-এ media storage হিসেবে S3-compatible object storage-ও ব্যবহার করা হয়।

# Part 5: Docker Network ও Storage Debugging

## ১১. সাধারণ সমস্যাগুলো কীভাবে সমাধান করবে?

Problem 1: Django database-এ connect করতে পারছে না

```
could not translate host name "db"
```

সম্ভাব্য কারণ: ভুল service name, container ভিন্ন network-এ আছে অথবা database service configuration ভুল।

পরীক্ষা:

Bash

```
docker compose ps
docker compose logs db
docker compose exec backend sh
```

Container-এর shell থেকে DNS ও connection পরীক্ষা করার জন্য প্রয়োজন হলে `getent hosts db` এবং PostgreSQL client-এর `pg_isready -h db -p 5432` ব্যবহার করতে পারো—তবে সংশ্লিষ্ট command container-এ install থাকতে হবে।

Problem 2: Nginx থেকে `502 Bad Gateway`

সম্ভাব্য কারণ: Gunicorn চালু হয়নি, ভুল upstream service name/port অথবা backend crash করেছে।

Bash

```
docker compose logs backend
docker compose logs nginx
```

যাচাই করবে Gunicorn `0.0.0.0:8000`-এ listen করছে কি না।

Problem 3: Container recreate করার পরে data নেই

সম্ভাব্য কারণ: volume mount ঠিকমতো করা হয়নি, ভিন্ন volume ব্যবহার হচ্ছে অথবা volume মুছে গেছে।

Bash

```
docker volume ls
docker compose config
```

PostgreSQL-এর data directory-তে সঠিক named volume mount করা আছে কি না পরীক্ষা করবে।

Problem 4: Static file `404 Not Found`

সম্ভাব্য কারণ: `collectstatic` চালানো হয়নি, `STATIC_ROOT` এবং Nginx alias মেলেনি অথবা volume সঠিকভাবে share করা হয়নি।

Bash

```
docker compose exec backend \
  python manage.py collectstatic --noinput
```

তারপর Nginx logs পরীক্ষা করবে।

## ১২. Container, image ও volume মুছলে কী হয়?

| Command                   | প্রভাব                                                         |
| ------------------------- | -------------------------------------------------------------- |
| `docker compose stop`     | Container বন্ধ করে, delete করে না                              |
| `docker compose down`     | Compose-এর container ও network সরায়; named volume সাধারণত রাখে |
| `docker compose down -v`  | Compose-সংশ্লিষ্ট named volume-ও মুছে দিতে পারে                |
| `docker image rm IMAGE`   | নির্দিষ্ট image মুছে দেয়, যদি সেটি ব্যবহারাধীন না থাকে         |
| `docker volume rm VOLUME` | নির্দিষ্ট volume মুছে দেয়, যদি সেটি ব্যবহারাধীন না থাকে        |

Production সতর্কতা: `docker compose down -v` চালানোর আগে নিশ্চিত হও যে কোনো প্রয়োজনীয় database data ওই volume-এ নেই, অথবা যাচাইকৃত backup আছে। Volume মুছে ফেললে data ফেরত পাওয়া কঠিন বা অসম্ভব হতে পারে।

# Part 6: তোমার Practical Assignment

এবার নিজে হাতে কাজ করো। শুধু code copy করলে হবে না—প্রতিটি পরীক্ষা কেন সফল বা ব্যর্থ হচ্ছে তা বুঝতে হবে।

## Assignment tracker

0 / 5

Exercise 1 — Network

একটি custom app_network তৈরি করো এবং backend ও db-কে যুক্ত করো। Django settings-এ database host হিসেবে db ব্যবহার করো।

Exercise 2 — Named Volume

PostgreSQL-এ একটি test row insert করো। Database container recreate করে row আবার query করো।

Exercise 3 — Bind Mount

একটি development Compose configuration তৈরি করো, যেখানে ./backend:/app bind mount হবে। Host-এ একটি Python file পরিবর্তন করে container থেকে পরিবর্তনটি যাচাই করো।

Exercise 4 — Static Files

static_volume ও media_volume তৈরি করো। collectstatic চালিয়ে Nginx থেকে একটি static file পরিবেশন হচ্ছে কি না পরীক্ষা করো।

Exercise 5 — Debugging

ভুল database hostname দিলে কী error হয় তা পর্যবেক্ষণ করো। তারপর hostname ঠিক করে service connection পুনরুদ্ধার করো।

Assignment solution review করো

## এই পর্বের মূল বিষয়

* Networking: Container-গুলোর মধ্যে communication।

* Named volume: Container recreate হলেও data ধরে রাখার ব্যবস্থা।

* Bind mount: Host-এর file container-এ ব্যবহার করা।

* Nginx: Gunicorn-এ request পাঠানো ও static/media পরিবেশন।

* Debugging: Service logs, network, mount এবং database connection পরীক্ষা।

পরবর্তী পর্বে আমরা শিখব Part 3 — Production Dockerfile, Multi-stage build, `.dockerignore`, environment secrets, health checks এবং non-root container hardening। এগুলো তোমার Django/DRF application-কে আরও নিরাপদ ও maintainable করে তুলবে।

----
# Django Production Deployment Course — Part 3

## Production Dockerfile, Multi-stage Build, Secrets, Health Checks ও Security Hardening

এই পর্বে আমরা আগের Django + Gunicorn + Nginx + PostgreSQL project-কে আরও production-ready করব।

আগের পর্বে তুমি Docker networking, named volumes এবং bind mounts শিখেছ। এবার focus থাকবে—কীভাবে ছোট, নিরাপদ, maintainable Docker image তৈরি করবে এবং application ঠিকভাবে চলছে কি না যাচাই করবে।

এই পর্বে আমরা শিখব:

1. Production Dockerfile-এর structure

2. Multi-stage Docker build

3. `.dockerignore` এবং image size optimization

4. Environment variables ও secrets management

5. Non-root user দিয়ে container চালানো

6. Docker health checks

7. Gunicorn ও Django production configuration

8. Build, run এবং debugging practice

## ১. Production Dockerfile কেন আলাদা?

Development-এ তুমি হয়তো এভাবে চালাও:

Bash

```
python manage.py runserver
```

কিন্তু production-এ আমরা চাই:

* Gunicorn দিয়ে Django চালাতে।

* অপ্রয়োজনীয় package image-এ না রাখতে।

* Root user হিসেবে application না চালাতে।

* Secret code repository বা image-এ না রাখতে।

* Application চালু হয়েছে কি না যাচাই করতে।

* একই image বিভিন্ন environment-এ ব্যবহার করতে।

আমাদের project structure হবে:

```
myproject/
├── backend/
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── requirements.txt
│   ├── manage.py
│   └── config/
│       ├── settings.py
│       ├── urls.py
│       └── wsgi.py
├── nginx/
│   └── default.conf
├── docker-compose.yml
└── .env
```

এখানে `config`-এর জায়গায় তোমার Django project package-এর নাম বসাবে।

## ২. প্রথমে একটি ভালো Production Dockerfile

`backend/Dockerfile` তৈরি করো:

dockerfile

```
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PIP_NO_CACHE_DIR=1

WORKDIR /app

RUN groupadd --system django \
    && useradd --system \
       --gid django \
       --home-dir /app \
       django

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=django:django . .

RUN mkdir -p /app/staticfiles /app/media \
    && chown -R django:django /app/staticfiles /app/media

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### প্রতিটি গুরুত্বপূর্ণ instruction-এর কাজ

| Instruction             | কাজ                                     |
| ----------------------- | --------------------------------------- |
| `FROM`                  | Python base image নির্বাচন              |
| `ENV`                   | Python ও pip-এর আচরণ নিয়ন্ত্রণ          |
| `WORKDIR`               | Application-এর working directory        |
| `COPY requirements.txt` | Dependency file আগে copy করা            |
| `RUN pip install`       | Python package install করা              |
| `COPY --chown`          | সঠিক file ownership-সহ source copy করা  |
| `USER django`           | Non-root user হিসেবে application চালানো |
| `EXPOSE 8000`           | Container-এর intended port ঘোষণা        |
| `CMD`                   | Container চালুর সময় Gunicorn শুরু করা   |

গুরুত্বপূর্ণ: `EXPOSE 8000` নিজে থেকে port-টি Internet-এ প্রকাশ করে না। Host port publish করতে Compose-এর `ports` প্রয়োজন; internal communication-এর জন্য `expose` বা একই network-এ থাকা যথেষ্ট।

এই Dockerfile একটি ভালো starting point, তবে এটি এখনো multi-stage নয়।

## ৩. Multi-stage Docker Build কী?

Multi-stage build মানে একই Dockerfile-এ একাধিক `FROM` stage ব্যবহার করা।

ধরো, Python dependency install করার সময় কিছু compiler ও build tools লাগে। কিন্তু application চালানোর সময় সেগুলোর সবকিছু দরকার হয় না।

Multi-stage build-এর ধারণা:

### Stage 1 — Builder

Python + pip + build dependencies

Dependency install করে virtual environment তৈরি করে।

শুধু প্রয়োজনীয় runtime environment কপি

### Stage 2 — Runtime

Python + installed dependencies + application code

Gunicorn দিয়ে Django চালায়।

ফলাফল: build tools-সহ পুরো builder stage runtime image-এ রাখতে হয় না। এতে image ছোট ও attack surface কম হতে পারে।

### Hands-on: Multi-stage Dockerfile

`backend/Dockerfile`-এর আগের code-এর বদলে এই version ব্যবহার করো:

dockerfile

```
# ---------- Stage 1: Builder ----------
FROM python:3.12-slim AS builder

ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       build-essential \
       libpq-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /build

RUN python -m venv /opt/venv

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt


# ---------- Stage 2: Runtime ----------
FROM python:3.12-slim AS runtime

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       libpq5 \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --system django \
    && useradd --system --gid django django

COPY --from=builder /opt/venv /opt/venv

COPY --chown=django:django . .

RUN mkdir -p /app/staticfiles /app/media \
    && chown -R django:django /app/staticfiles /app/media

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### এখানে `COPY --from=builder` কেন?

dockerfile

```
COPY --from=builder /opt/venv /opt/venv
```

এটি builder stage-এ install করা Python dependencies runtime stage-এ কপি করে।

তবে সতর্কতা: কিছু Python package-এর native library বা compiled extension থাকলে runtime stage-এ সঠিক shared library থাকতে হবে। এখানে `libpq5` রাখা হয়েছে PostgreSQL client library-নির্ভর package-এর জন্য।

`requirements.txt`-এ dependency version pin করো এবং যে Python ও operating-system base image ব্যবহার করছ, সেটির সঙ্গে compatible কি না পরীক্ষা করো।

## ৪. `.dockerignore` দিয়ে অপ্রয়োজনীয় ফাইল বাদ দাও

`backend/.dockerignore`:

```
.git/
.venv/
venv/
__pycache__/
*.py[cod]
.pytest_cache/
.coverage
.env
.env.*
!.env.example
media/
staticfiles/
dist/
build/
```

এর ফলে local virtual environment, Git history, environment secrets এবং generated files সাধারণত Docker build context-এ যাবে না।

মনে রাখবে: `.dockerignore` runtime container-এর file access control নয়। এটি মূলত build context থেকে file বাদ দেয়। আর `COPY . .` করার আগে `.dockerignore` ঠিকভাবে configure করা গুরুত্বপূর্ণ।

# Part 2: Secrets Management

## ৫. Django Secret Key নিরাপদ রাখবে কীভাবে?

কখনোই এমন করো না:

dockerfile

```
ENV DJANGO_SECRET_KEY="my-secret-key"
```

অথবা source code-এ:

Python

Run

```
SECRET_KEY = "my-production-secret"
```

এগুলো Git history, image metadata বা অন্য মাধ্যমে প্রকাশ পেতে পারে।

Development-এ `.env` ব্যবহার করা যায়, তবে `.env`-কে `.gitignore`-এ রাখবে। Production-এ secret manager অথবা উপযুক্ত secret file mechanism ব্যবহার করো।

### Option A — Environment variable

`settings.py`:

Python

Run

```
import os

SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]
```

এটি সহজ পদ্ধতি, তবে environment variables process inspection বা diagnostic output-এর মাধ্যমে প্রকাশ পাওয়ার ঝুঁকি থাকতে পারে।

### Option B — Docker Compose secrets

Project root-এ এই structure তৈরি করো:

```
myproject/
├── secrets/
│   ├── django_secret_key.txt
│   └── postgres_password.txt
├── backend/
├── nginx/
└── docker-compose.yml
```

এই secret file-গুলো Git-এ commit করবে না। `.gitignore`-এ যোগ করো:

gitignore

```
.env
secrets/
```

`django_secret_key.txt`-এ একটি শক্তিশালী random secret রাখো। `postgres_password.txt`-এ PostgreSQL-এর শক্তিশালী password রাখো।

Django settings-এ secret file পড়ার জন্য:

Python

Run

```
from pathlib import Path

SECRET_KEY = Path(
    "/run/secrets/django_secret_key"
).read_text().strip()
```

Compose-এ Django service-এর অংশ:

YAML

```
services:
  backend:
    secrets:
      - django_secret_key

secrets:
  django_secret_key:
    file: ./secrets/django_secret_key.txt
```

এখানে `secrets:` declaration-টি Compose file-এর top level-এ থাকবে; উপরের snippet-এ সেটি দেখানোর জন্য service section-এর পর রাখা হয়েছে।

PostgreSQL-এর official image-এ `_FILE` environment variable support ব্যবহার করা যায়:

YAML

```
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
    secrets:
      - postgres_password

secrets:
  postgres_password:
    file: ./secrets/postgres_password.txt
```

Django-কে একই database password পড়তে হলে settings-এ `POSTGRES_PASSWORD_FILE`-এর path ব্যবহার করে file-এর content পড়ার ব্যবস্থা করতে হবে, অথবা application-এ password secret mount করে সেই file পড়তে হবে।

গুরুত্বপূর্ণ সীমাবদ্ধতা: সাধারণ local Docker Compose secrets file-কে encrypted secret manager বানিয়ে দেয় না। Host-এর secret file নিরাপদ রাখতে হবে, access সীমিত করতে হবে এবং production infrastructure অনুযায়ী secret management বেছে নিতে হবে।

# Part 3: Health Checks

## ৬. Health check কী এবং কেন দরকার?

কোনো container running থাকলেই application সঠিকভাবে কাজ করছে, এমন নয়।

উদাহরণ:

* Gunicorn process চলছে, কিন্তু Django startup-এ error হচ্ছে।

* PostgreSQL container চলছে, কিন্তু database connection গ্রহণ করার জন্য প্রস্তুত নয়।

* Nginx চলছে, কিন্তু upstream backend unreachable।

Health check দিয়ে Docker নির্দিষ্ট সময় পরপর service-এর অবস্থা পরীক্ষা করতে পারে।

### Step 1 — Django health endpoint তৈরি করো

`backend/config/views.py`:

Python

Run

```
from django.http import JsonResponse
from django.views.decorators.http import require_GET


@require_GET
def health_check(request):
    return JsonResponse({"status": "ok"})
```

`backend/config/urls.py`:

Python

Run

```
from django.contrib import admin
from django.urls import path
from .views import health_check

urlpatterns = [
    path("admin/", admin.site.urls),
    path("health/", health_check),
]
```

এখন endpoint-টি চালু Django application থেকে `{"status": "ok"}` response দেবে।

এই endpoint শুধু HTTP application response পরীক্ষা করে; database বা অন্য dependency ঠিক আছে কি না তা নিজে থেকে নিশ্চিত করে না।

### Step 2 — Dockerfile-এ health check যোগ করো

Runtime stage-এ `USER django`-এর আগে বা পরে এই instruction যোগ করতে পারো:

dockerfile

```
HEALTHCHECK --interval=30s \
    --timeout=5s \
    --start-period=20s \
    --retries=3 \
    CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/', timeout=3)"
```

এর অর্থ:

| Option               | অর্থ                                                 |
| -------------------- | ---------------------------------------------------- |
| `--interval=30s`     | প্রতি ৩০ সেকেন্ডে পরীক্ষা                            |
| `--timeout=5s`       | Health check-এর সর্বোচ্চ সময়                         |
| `--start-period=20s` | Startup-এর জন্য grace period                         |
| `--retries=3`        | ধারাবাহিক failure-এর পর unhealthy হিসেবে চিহ্নিত করা |

Docker health status দেখার command:

Bash

```
docker compose ps
```

অথবা:

Bash

```
docker inspect \
  --format='{{json .State.Health}}' \
  <container-name>
```

সতর্কতা: Docker-এর `HEALTHCHECK` কোনো application-কে স্বয়ংক্রিয়ভাবে restart করার universal guarantee নয়। এটি health status রিপোর্ট করে; restart ও recovery policy আলাদাভাবে বুঝে configure করতে হবে।

## ৭. PostgreSQL health check

Compose-এ database-এর জন্য:

YAML

```
services:
  db:
    image: postgres:16
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s
```

`pg_isready` PostgreSQL connection গ্রহণ করতে প্রস্তুত কি না যাচাই করে।

তবে এটি application-এর database credentials দিয়ে সব ধরনের query সফল হবে কি না তার পূর্ণ পরীক্ষা নয়। Django-এর actual database connection পরীক্ষা করতে চাইলে আলাদা readiness check তৈরি করতে হবে।

# Part 4: Production Security Settings

## ৮. Django settings hardening

Production environment-এ সাধারণত এই ধরনের settings দরকার:

Python

Run

```
DEBUG = False

ALLOWED_HOSTS = [
    "api.example.com",
]

CSRF_TRUSTED_ORIGINS = [
    "https://api.example.com",
]

SECURE_SSL_REDIRECT = True

SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True

SECURE_CONTENT_TYPE_NOSNIFF = True

X_FRAME_OPTIONS = "DENY"
```

`api.example.com` তোমার প্রকৃত domain দিয়ে পরিবর্তন করবে।

HTTPS যদি Nginx বা load balancer-এ terminate করা হয়, তাহলে `SECURE_SSL_REDIRECT` এবং proxy SSL configuration সঠিকভাবে configure করতে হবে; ভুল proxy configuration redirect loop তৈরি করতে পারে।

যদি React frontend আলাদা domain-এ থাকে, তাহলে CORS configuration-ও সঠিকভাবে করতে হবে। CORS এবং CSRF এক বিষয় নয়।

আরেকটি গুরুত্বপূর্ণ বিষয়: public health endpoint-এ database credentials, stack trace বা internal configuration কখনো প্রকাশ করবে না।

# Part 5: সবকিছু একসঙ্গে চালানো

## ৯. Production-style Compose configuration

এবার আগের networking, persistent volumes, health checks ও secrets একত্রে সাজানো যাক।

`docker-compose.yml`-এর একটি reference configuration:

YAML

```
services:
  backend:
    build:
      context: ./backend
    environment:
      DJANGO_SETTINGS_MODULE: config.settings
      DJANGO_SECRET_KEY_FILE: /run/secrets/django_secret_key
      DJANGO_ALLOWED_HOSTS: api.example.com
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
      POSTGRES_HOST: db
      POSTGRES_PORT: "5432"
    secrets:
      - django_secret_key
      - postgres_password
    expose:
      - "8000"
    volumes:
      - static_volume:/app/staticfiles
      - media_volume:/app/media
    networks:
      - app_network
    depends_on:
      db:
        condition: service_healthy
    restart: unless-stopped

  db:
    image: postgres:16
    environment:
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
    secrets:
      - postgres_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app_network
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - static_volume:/app/staticfiles:ro
      - media_volume:/app/media:ro
    networks:
      - app_network
    depends_on:
      - backend
    restart: unless-stopped

networks:
  app_network:
    driver: bridge

volumes:
  postgres_data:
  static_volume:
  media_volume:

secrets:
  django_secret_key:
    file: ./secrets/django_secret_key.txt
  postgres_password:
    file: ./secrets/postgres_password.txt
```

এই Compose configuration-এ Django settings-কে `DJANGO_SECRET_KEY_FILE` ও `POSTGRES_PASSWORD_FILE` থেকে file পড়ে secret ব্যবহার করার code যোগ করতে হবে। আগের সাধারণ environment-variable ভিত্তিক settings সরাসরি এই file path-গুলোকে secret value হিসেবে ব্যবহার করতে পারবে না।

Production-এ deploy করার আগে নিশ্চিত করবে:

* `config.wsgi:application` সঠিক module-কে নির্দেশ করছে।

* Django database password file থেকে পড়ছে।

* `.env` ও `secrets/` Git-এ নেই।

* Database volume-এর backup আছে।

* Nginx-এ বাস্তব domain ও HTTPS configuration আছে।

* Migration controlled deployment step হিসেবে চলছে।

আর মনে রাখবে, `depends_on: condition: service_healthy` database healthy হওয়া পর্যন্ত backend startup অপেক্ষা করায়; database পরে disconnect হলে Django নিজে থেকেই সব connection সমস্যা সমাধান করবে, এমন নিশ্চয়তা নেই।

# Part 6: Build, Run ও Verify

## ১০. নিজের machine-এ পরীক্ষা করো

Project root থেকে একে একে command চালাবে।

Step 1 — Dockerfile build

Bash

```
docker compose build --no-cache backend
```

Step 2 — Configuration validation

Bash

```
docker compose config -q
```

Step 3 — Container চালু

Bash

```
docker compose up -d
```

Step 4 — Database migration

Bash

```
docker compose exec backend python manage.py migrate
```

Step 5 — Static files collect

Bash

```
docker compose exec backend python manage.py collectstatic --noinput
```

Step 6 — Health check ও logs

Bash

```
docker compose ps
docker compose logs --tail=100 backend
docker compose logs --tail=100 nginx
docker compose logs --tail=100 db
```

Step 7 — Health endpoint পরীক্ষা

Bash

```
curl -i http://localhost/health/
```

Expected response:

JSON

```
{
  "status": "ok"
}
```

JSON response-এ whitespace বা formatting আলাদা হতে পারে। আর `curl` সফল হতে হলে Nginx configuration, Django URL এবং container startup—সব সঠিক থাকতে হবে।

## ১১. Non-root user সত্যিই ব্যবহার হচ্ছে কি না দেখো

Bash

```
docker compose exec backend id
```

Output-এ `root` user দেখা উচিত নয়। আমাদের Dockerfile-এ `USER django` ব্যবহার করা হয়েছে।

Image-এর size দেখো:

Bash

```
docker image ls
```

এবং running container-এর resource usage:

Bash

```
docker stats
```

এগুলো দেখে তুমি image optimization ও worker resource consumption সম্পর্কে ধারণা পাবে।

# Part 7: Gunicorn Worker Tuning

## ১২. Worker সংখ্যা কীভাবে নির্ধারণ করবে?

শুরুতে:

Bash

```
gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers 3 \
    --timeout 60
```

এটি একটি starting point, universal recommendation নয়।

Worker সংখ্যা বাড়ানোর আগে এই বিষয়গুলো পরীক্ষা করবে:

1. প্রতিটি worker-এর memory consumption।

2. CPU utilization।

3. Database connection-এর সংখ্যা।

4. API-এর response time।

5. Request-গুলো CPU-bound, database-bound নাকি network-bound।

ধরো, তোমার application-এ ৩টি worker আছে এবং প্রতিটি worker-এর memory ব্যবহার অনেক বেশি। Worker সংখ্যা ৬ করলে throughput বাড়তেও পারে, আবার memory exhaustion-এর কারণে container crash-ও করতে পারে।

তাই load test চালিয়ে ধাপে ধাপে পরিবর্তন করো। Django application-এ background task-এর জন্য Celery ব্যবহার করলে সেটির worker-গুলো Gunicorn worker থেকে আলাদা process/service হিসেবে চালাবে।

## ১৩. Final assignment

## Part 3 checklist

0/ সম্পন্ন

আমার solution review করো

পরবর্তী পর্বে আমরা শিখব Part 4 — Ubuntu VPS-এ বাস্তব deployment: SSH, firewall, domain, HTTPS/Let's Encrypt, Nginx reverse proxy এবং নিরাপদ deployment workflow। সেখানে local Docker project-কে Internet-এ accessible production application হিসেবে চালানোর সম্পূর্ণ প্রক্রিয়া দেখব।
# Django Production Deployment Course — Part 3

## Production Dockerfile, Multi-stage Build, Secrets, Health Checks ও Security Hardening

এই পর্বে আমরা আগের Django + Gunicorn + Nginx + PostgreSQL project-কে আরও production-ready করব।

আগের পর্বে তুমি Docker networking, named volumes এবং bind mounts শিখেছ। এবার focus থাকবে—কীভাবে ছোট, নিরাপদ, maintainable Docker image তৈরি করবে এবং application ঠিকভাবে চলছে কি না যাচাই করবে।

এই পর্বে আমরা শিখব:

1. Production Dockerfile-এর structure

2. Multi-stage Docker build

3. `.dockerignore` এবং image size optimization

4. Environment variables ও secrets management

5. Non-root user দিয়ে container চালানো

6. Docker health checks

7. Gunicorn ও Django production configuration

8. Build, run এবং debugging practice

## ১. Production Dockerfile কেন আলাদা?

Development-এ তুমি হয়তো এভাবে চালাও:

Bash

```
python manage.py runserver
```

কিন্তু production-এ আমরা চাই:

* Gunicorn দিয়ে Django চালাতে।

* অপ্রয়োজনীয় package image-এ না রাখতে।

* Root user হিসেবে application না চালাতে।

* Secret code repository বা image-এ না রাখতে।

* Application চালু হয়েছে কি না যাচাই করতে।

* একই image বিভিন্ন environment-এ ব্যবহার করতে।

আমাদের project structure হবে:

```
myproject/
├── backend/
│   ├── Dockerfile
│   ├── .dockerignore
│   ├── requirements.txt
│   ├── manage.py
│   └── config/
│       ├── settings.py
│       ├── urls.py
│       └── wsgi.py
├── nginx/
│   └── default.conf
├── docker-compose.yml
└── .env
```

এখানে `config`-এর জায়গায় তোমার Django project package-এর নাম বসাবে।

## ২. প্রথমে একটি ভালো Production Dockerfile

`backend/Dockerfile` তৈরি করো:

dockerfile

```
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PIP_NO_CACHE_DIR=1

WORKDIR /app

RUN groupadd --system django \
    && useradd --system \
       --gid django \
       --home-dir /app \
       django

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY --chown=django:django . .

RUN mkdir -p /app/staticfiles /app/media \
    && chown -R django:django /app/staticfiles /app/media

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### প্রতিটি গুরুত্বপূর্ণ instruction-এর কাজ

| Instruction             | কাজ                                     |
| ----------------------- | --------------------------------------- |
| `FROM`                  | Python base image নির্বাচন              |
| `ENV`                   | Python ও pip-এর আচরণ নিয়ন্ত্রণ          |
| `WORKDIR`               | Application-এর working directory        |
| `COPY requirements.txt` | Dependency file আগে copy করা            |
| `RUN pip install`       | Python package install করা              |
| `COPY --chown`          | সঠিক file ownership-সহ source copy করা  |
| `USER django`           | Non-root user হিসেবে application চালানো |
| `EXPOSE 8000`           | Container-এর intended port ঘোষণা        |
| `CMD`                   | Container চালুর সময় Gunicorn শুরু করা   |

গুরুত্বপূর্ণ: `EXPOSE 8000` নিজে থেকে port-টি Internet-এ প্রকাশ করে না। Host port publish করতে Compose-এর `ports` প্রয়োজন; internal communication-এর জন্য `expose` বা একই network-এ থাকা যথেষ্ট।

এই Dockerfile একটি ভালো starting point, তবে এটি এখনো multi-stage নয়।

## ৩. Multi-stage Docker Build কী?

Multi-stage build মানে একই Dockerfile-এ একাধিক `FROM` stage ব্যবহার করা।

ধরো, Python dependency install করার সময় কিছু compiler ও build tools লাগে। কিন্তু application চালানোর সময় সেগুলোর সবকিছু দরকার হয় না।

Multi-stage build-এর ধারণা:

### Stage 1 — Builder

Python + pip + build dependencies

Dependency install করে virtual environment তৈরি করে।

শুধু প্রয়োজনীয় runtime environment কপি

### Stage 2 — Runtime

Python + installed dependencies + application code

Gunicorn দিয়ে Django চালায়।

ফলাফল: build tools-সহ পুরো builder stage runtime image-এ রাখতে হয় না। এতে image ছোট ও attack surface কম হতে পারে।

### Hands-on: Multi-stage Dockerfile

`backend/Dockerfile`-এর আগের code-এর বদলে এই version ব্যবহার করো:

dockerfile

```
# ---------- Stage 1: Builder ----------
FROM python:3.12-slim AS builder

ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       build-essential \
       libpq-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /build

RUN python -m venv /opt/venv

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt


# ---------- Stage 2: Runtime ----------
FROM python:3.12-slim AS runtime

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

WORKDIR /app

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       libpq5 \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --system django \
    && useradd --system --gid django django

COPY --from=builder /opt/venv /opt/venv

COPY --chown=django:django . .

RUN mkdir -p /app/staticfiles /app/media \
    && chown -R django:django /app/staticfiles /app/media

USER django

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "3", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### এখানে `COPY --from=builder` কেন?

dockerfile

```
COPY --from=builder /opt/venv /opt/venv
```

এটি builder stage-এ install করা Python dependencies runtime stage-এ কপি করে।

তবে সতর্কতা: কিছু Python package-এর native library বা compiled extension থাকলে runtime stage-এ সঠিক shared library থাকতে হবে। এখানে `libpq5` রাখা হয়েছে PostgreSQL client library-নির্ভর package-এর জন্য।

`requirements.txt`-এ dependency version pin করো এবং যে Python ও operating-system base image ব্যবহার করছ, সেটির সঙ্গে compatible কি না পরীক্ষা করো।

## ৪. `.dockerignore` দিয়ে অপ্রয়োজনীয় ফাইল বাদ দাও

`backend/.dockerignore`:

```
.git/
.venv/
venv/
__pycache__/
*.py[cod]
.pytest_cache/
.coverage
.env
.env.*
!.env.example
media/
staticfiles/
dist/
build/
```

এর ফলে local virtual environment, Git history, environment secrets এবং generated files সাধারণত Docker build context-এ যাবে না।

মনে রাখবে: `.dockerignore` runtime container-এর file access control নয়। এটি মূলত build context থেকে file বাদ দেয়। আর `COPY . .` করার আগে `.dockerignore` ঠিকভাবে configure করা গুরুত্বপূর্ণ।

# Part 2: Secrets Management

## ৫. Django Secret Key নিরাপদ রাখবে কীভাবে?

কখনোই এমন করো না:

dockerfile

```
ENV DJANGO_SECRET_KEY="my-secret-key"
```

অথবা source code-এ:

Python

Run

```
SECRET_KEY = "my-production-secret"
```

এগুলো Git history, image metadata বা অন্য মাধ্যমে প্রকাশ পেতে পারে।

Development-এ `.env` ব্যবহার করা যায়, তবে `.env`-কে `.gitignore`-এ রাখবে। Production-এ secret manager অথবা উপযুক্ত secret file mechanism ব্যবহার করো।

### Option A — Environment variable

`settings.py`:

Python

Run

```
import os

SECRET_KEY = os.environ["DJANGO_SECRET_KEY"]
```

এটি সহজ পদ্ধতি, তবে environment variables process inspection বা diagnostic output-এর মাধ্যমে প্রকাশ পাওয়ার ঝুঁকি থাকতে পারে।

### Option B — Docker Compose secrets

Project root-এ এই structure তৈরি করো:

```
myproject/
├── secrets/
│   ├── django_secret_key.txt
│   └── postgres_password.txt
├── backend/
├── nginx/
└── docker-compose.yml
```

এই secret file-গুলো Git-এ commit করবে না। `.gitignore`-এ যোগ করো:

gitignore

```
.env
secrets/
```

`django_secret_key.txt`-এ একটি শক্তিশালী random secret রাখো। `postgres_password.txt`-এ PostgreSQL-এর শক্তিশালী password রাখো।

Django settings-এ secret file পড়ার জন্য:

Python

Run

```
from pathlib import Path

SECRET_KEY = Path(
    "/run/secrets/django_secret_key"
).read_text().strip()
```

Compose-এ Django service-এর অংশ:

YAML

```
services:
  backend:
    secrets:
      - django_secret_key

secrets:
  django_secret_key:
    file: ./secrets/django_secret_key.txt
```

এখানে `secrets:` declaration-টি Compose file-এর top level-এ থাকবে; উপরের snippet-এ সেটি দেখানোর জন্য service section-এর পর রাখা হয়েছে।

PostgreSQL-এর official image-এ `_FILE` environment variable support ব্যবহার করা যায়:

YAML

```
services:
  db:
    image: postgres:16
    environment:
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
    secrets:
      - postgres_password

secrets:
  postgres_password:
    file: ./secrets/postgres_password.txt
```

Django-কে একই database password পড়তে হলে settings-এ `POSTGRES_PASSWORD_FILE`-এর path ব্যবহার করে file-এর content পড়ার ব্যবস্থা করতে হবে, অথবা application-এ password secret mount করে সেই file পড়তে হবে।

গুরুত্বপূর্ণ সীমাবদ্ধতা: সাধারণ local Docker Compose secrets file-কে encrypted secret manager বানিয়ে দেয় না। Host-এর secret file নিরাপদ রাখতে হবে, access সীমিত করতে হবে এবং production infrastructure অনুযায়ী secret management বেছে নিতে হবে।

# Part 3: Health Checks

## ৬. Health check কী এবং কেন দরকার?

কোনো container running থাকলেই application সঠিকভাবে কাজ করছে, এমন নয়।

উদাহরণ:

* Gunicorn process চলছে, কিন্তু Django startup-এ error হচ্ছে।

* PostgreSQL container চলছে, কিন্তু database connection গ্রহণ করার জন্য প্রস্তুত নয়।

* Nginx চলছে, কিন্তু upstream backend unreachable।

Health check দিয়ে Docker নির্দিষ্ট সময় পরপর service-এর অবস্থা পরীক্ষা করতে পারে।

### Step 1 — Django health endpoint তৈরি করো

`backend/config/views.py`:

Python

Run

```
from django.http import JsonResponse
from django.views.decorators.http import require_GET


@require_GET
def health_check(request):
    return JsonResponse({"status": "ok"})
```

`backend/config/urls.py`:

Python

Run

```
from django.contrib import admin
from django.urls import path
from .views import health_check

urlpatterns = [
    path("admin/", admin.site.urls),
    path("health/", health_check),
]
```

এখন endpoint-টি চালু Django application থেকে `{"status": "ok"}` response দেবে।

এই endpoint শুধু HTTP application response পরীক্ষা করে; database বা অন্য dependency ঠিক আছে কি না তা নিজে থেকে নিশ্চিত করে না।

### Step 2 — Dockerfile-এ health check যোগ করো

Runtime stage-এ `USER django`-এর আগে বা পরে এই instruction যোগ করতে পারো:

dockerfile

```
HEALTHCHECK --interval=30s \
    --timeout=5s \
    --start-period=20s \
    --retries=3 \
    CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health/', timeout=3)"
```

এর অর্থ:

| Option               | অর্থ                                                 |
| -------------------- | ---------------------------------------------------- |
| `--interval=30s`     | প্রতি ৩০ সেকেন্ডে পরীক্ষা                            |
| `--timeout=5s`       | Health check-এর সর্বোচ্চ সময়                         |
| `--start-period=20s` | Startup-এর জন্য grace period                         |
| `--retries=3`        | ধারাবাহিক failure-এর পর unhealthy হিসেবে চিহ্নিত করা |

Docker health status দেখার command:

Bash

```
docker compose ps
```

অথবা:

Bash

```
docker inspect \
  --format='{{json .State.Health}}' \
  <container-name>
```

সতর্কতা: Docker-এর `HEALTHCHECK` কোনো application-কে স্বয়ংক্রিয়ভাবে restart করার universal guarantee নয়। এটি health status রিপোর্ট করে; restart ও recovery policy আলাদাভাবে বুঝে configure করতে হবে।

## ৭. PostgreSQL health check

Compose-এ database-এর জন্য:

YAML

```
services:
  db:
    image: postgres:16
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 10s
```

`pg_isready` PostgreSQL connection গ্রহণ করতে প্রস্তুত কি না যাচাই করে।

তবে এটি application-এর database credentials দিয়ে সব ধরনের query সফল হবে কি না তার পূর্ণ পরীক্ষা নয়। Django-এর actual database connection পরীক্ষা করতে চাইলে আলাদা readiness check তৈরি করতে হবে।

# Part 4: Production Security Settings

## ৮. Django settings hardening

Production environment-এ সাধারণত এই ধরনের settings দরকার:

Python

Run

```
DEBUG = False

ALLOWED_HOSTS = [
    "api.example.com",
]

CSRF_TRUSTED_ORIGINS = [
    "https://api.example.com",
]

SECURE_SSL_REDIRECT = True

SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True

SECURE_CONTENT_TYPE_NOSNIFF = True

X_FRAME_OPTIONS = "DENY"
```

`api.example.com` তোমার প্রকৃত domain দিয়ে পরিবর্তন করবে।

HTTPS যদি Nginx বা load balancer-এ terminate করা হয়, তাহলে `SECURE_SSL_REDIRECT` এবং proxy SSL configuration সঠিকভাবে configure করতে হবে; ভুল proxy configuration redirect loop তৈরি করতে পারে।

যদি React frontend আলাদা domain-এ থাকে, তাহলে CORS configuration-ও সঠিকভাবে করতে হবে। CORS এবং CSRF এক বিষয় নয়।

আরেকটি গুরুত্বপূর্ণ বিষয়: public health endpoint-এ database credentials, stack trace বা internal configuration কখনো প্রকাশ করবে না।

# Part 5: সবকিছু একসঙ্গে চালানো

## ৯. Production-style Compose configuration

এবার আগের networking, persistent volumes, health checks ও secrets একত্রে সাজানো যাক।

`docker-compose.yml`-এর একটি reference configuration:

YAML

```
services:
  backend:
    build:
      context: ./backend
    environment:
      DJANGO_SETTINGS_MODULE: config.settings
      DJANGO_SECRET_KEY_FILE: /run/secrets/django_secret_key
      DJANGO_ALLOWED_HOSTS: api.example.com
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
      POSTGRES_HOST: db
      POSTGRES_PORT: "5432"
    secrets:
      - django_secret_key
      - postgres_password
    expose:
      - "8000"
    volumes:
      - static_volume:/app/staticfiles
      - media_volume:/app/media
    networks:
      - app_network
    depends_on:
      db:
        condition: service_healthy
    restart: unless-stopped

  db:
    image: postgres:16
    environment:
      POSTGRES_DB: ecommerce
      POSTGRES_USER: ecommerce_user
      POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password
    secrets:
      - postgres_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - app_network
    healthcheck:
      test:
        - CMD-SHELL
        - pg_isready -U "$$POSTGRES_USER" -d "$$POSTGRES_DB"
      interval: 10s
      timeout: 5s
      retries: 5
    restart: unless-stopped

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - static_volume:/app/staticfiles:ro
      - media_volume:/app/media:ro
    networks:
      - app_network
    depends_on:
      - backend
    restart: unless-stopped

networks:
  app_network:
    driver: bridge

volumes:
  postgres_data:
  static_volume:
  media_volume:

secrets:
  django_secret_key:
    file: ./secrets/django_secret_key.txt
  postgres_password:
    file: ./secrets/postgres_password.txt
```

এই Compose configuration-এ Django settings-কে `DJANGO_SECRET_KEY_FILE` ও `POSTGRES_PASSWORD_FILE` থেকে file পড়ে secret ব্যবহার করার code যোগ করতে হবে। আগের সাধারণ environment-variable ভিত্তিক settings সরাসরি এই file path-গুলোকে secret value হিসেবে ব্যবহার করতে পারবে না।

Production-এ deploy করার আগে নিশ্চিত করবে:

* `config.wsgi:application` সঠিক module-কে নির্দেশ করছে।

* Django database password file থেকে পড়ছে।

* `.env` ও `secrets/` Git-এ নেই।

* Database volume-এর backup আছে।

* Nginx-এ বাস্তব domain ও HTTPS configuration আছে।

* Migration controlled deployment step হিসেবে চলছে।

আর মনে রাখবে, `depends_on: condition: service_healthy` database healthy হওয়া পর্যন্ত backend startup অপেক্ষা করায়; database পরে disconnect হলে Django নিজে থেকেই সব connection সমস্যা সমাধান করবে, এমন নিশ্চয়তা নেই।

# Part 6: Build, Run ও Verify

## ১০. নিজের machine-এ পরীক্ষা করো

Project root থেকে একে একে command চালাবে।

Step 1 — Dockerfile build

Bash

```
docker compose build --no-cache backend
```

Step 2 — Configuration validation

Bash

```
docker compose config -q
```

Step 3 — Container চালু

Bash

```
docker compose up -d
```

Step 4 — Database migration

Bash

```
docker compose exec backend python manage.py migrate
```

Step 5 — Static files collect

Bash

```
docker compose exec backend python manage.py collectstatic --noinput
```

Step 6 — Health check ও logs

Bash

```
docker compose ps
docker compose logs --tail=100 backend
docker compose logs --tail=100 nginx
docker compose logs --tail=100 db
```

Step 7 — Health endpoint পরীক্ষা

Bash

```
curl -i http://localhost/health/
```

Expected response:

JSON

```
{
  "status": "ok"
}
```

JSON response-এ whitespace বা formatting আলাদা হতে পারে। আর `curl` সফল হতে হলে Nginx configuration, Django URL এবং container startup—সব সঠিক থাকতে হবে।

## ১১. Non-root user সত্যিই ব্যবহার হচ্ছে কি না দেখো

Bash

```
docker compose exec backend id
```

Output-এ `root` user দেখা উচিত নয়। আমাদের Dockerfile-এ `USER django` ব্যবহার করা হয়েছে।

Image-এর size দেখো:

Bash

```
docker image ls
```

এবং running container-এর resource usage:

Bash

```
docker stats
```

এগুলো দেখে তুমি image optimization ও worker resource consumption সম্পর্কে ধারণা পাবে।

# Part 7: Gunicorn Worker Tuning

## ১২. Worker সংখ্যা কীভাবে নির্ধারণ করবে?

শুরুতে:

Bash

```
gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers 3 \
    --timeout 60
```

এটি একটি starting point, universal recommendation নয়।

Worker সংখ্যা বাড়ানোর আগে এই বিষয়গুলো পরীক্ষা করবে:

1. প্রতিটি worker-এর memory consumption।

2. CPU utilization।

3. Database connection-এর সংখ্যা।

4. API-এর response time।

5. Request-গুলো CPU-bound, database-bound নাকি network-bound।

ধরো, তোমার application-এ ৩টি worker আছে এবং প্রতিটি worker-এর memory ব্যবহার অনেক বেশি। Worker সংখ্যা ৬ করলে throughput বাড়তেও পারে, আবার memory exhaustion-এর কারণে container crash-ও করতে পারে।

তাই load test চালিয়ে ধাপে ধাপে পরিবর্তন করো। Django application-এ background task-এর জন্য Celery ব্যবহার করলে সেটির worker-গুলো Gunicorn worker থেকে আলাদা process/service হিসেবে চালাবে।

## ১৩. Final assignment

## Part 3 checklist

0/ সম্পন্ন

আমার solution review করো

পরবর্তী পর্বে আমরা শিখব Part 4 — Ubuntu VPS-এ বাস্তব deployment: SSH, firewall, domain, HTTPS/Let's Encrypt, Nginx reverse proxy এবং নিরাপদ deployment workflow। সেখানে local Docker project-কে Internet-এ accessible production application হিসেবে চালানোর সম্পূর্ণ প্রক্রিয়া দেখব।

----
# Django Production Deployment Course — Part 4

## Ubuntu VPS, SSH, Firewall, Domain, HTTPS ও Live Deployment

এই পর্বে আমরা তোমার Django REST Framework application-কে local computer থেকে Internet-এ deploy করার প্রক্রিয়া শিখব।

আগের পর্বগুলোতে আমরা শিখেছি:

* Part 1: Gunicorn + Nginx + Docker architecture

* Part 2: Docker networking, volumes ও persistent storage

* Part 3: Multi-stage Dockerfile, secrets, health checks ও security

এবার সেগুলো ব্যবহার করে একটি VPS-এ Django application চালাব।

এই পর্বের লক্ষ্য: কেউ যেন তোমার domain-এ প্রবেশ করে Django API ব্যবহার করতে পারে, আর application-এর সামনে HTTPS ও Nginx থাকে।

## ১. Production architecture

React / Next.js / API Client

HTTPS request

Domain + DNS

api.example.com → VPS public IP

Ubuntu VPS

Firewall + HTTPS certificate

Nginx :443

Docker network

Gunicorn :8000 → Django REST Framework

PostgreSQL

Persistent volume + backups

এখানে একটি security rule মনে রাখবে: Internet থেকে সাধারণত শুধু SSH (নির্দিষ্ট admin access), HTTP এবং HTTPS access থাকবে। PostgreSQL-এর 5432 ও Gunicorn-এর 8000 port public Internet-এ খুলব না।

## ২. VPS কী এবং কী কিনতে হবে?

VPS (Virtual Private Server) হলো cloud provider-এর একটি virtual server, যেখানে তুমি Ubuntu, Docker, Nginx এবং Django চালাতে পারবে।

শেখার জন্য একটি সাধারণ Linux VPS যথেষ্ট হতে পারে। নির্বাচন করার সময় বিবেচনা করবে:

* Ubuntu-এর supported LTS release

* RAM ও CPU

* SSD storage

* Public IPv4 address বা উপযুক্ত IPv6 configuration

* Firewall ও backup সুবিধা

* তোমার বাজেট ও server-এর location

শুধু শেখার জন্য প্রথমে নিজের Ubuntu computer-এ Docker Compose দিয়ে এই workflow পরীক্ষা করতে পারো। VPS না কিনেও domain ও HTTPS-এর deployment ধারণাগুলো শিখতে পারবে, যদিও public server-এর বাস্তব পরীক্ষা তখন করা যাবে না।

এই tutorial-এ আমরা ধরে নিচ্ছি:

```
VPS public IP: 203.0.113.10
Domain: example.com
API domain: api.example.com
Linux user: deploy
Project path: /opt/myproject
```

এগুলো শুধু example value। `203.0.113.10` documentation-এর reserved example IP; নিজের VPS-এর আসল public IP দিয়ে পরিবর্তন করবে।

## ৩. SSH দিয়ে VPS-এ connect করো

VPS provider-এর dashboard থেকে server তৈরি করার পর সাধারণত public IP এবং SSH key বা initial login credentials পাওয়া যায়।

নিজের Ubuntu computer-এর terminal থেকে:

Bash

```
ssh deploy@YOUR_SERVER_IP
```

এখানে `deploy` হলো server-এর username। Provider যদি `ubuntu` বা অন্য user দেয়, সেটি ব্যবহার করবে।

SSH key ব্যবহার করলে:

Bash

```
ssh -i ~/.ssh/my-vps-key deploy@YOUR_SERVER_IP
```

প্রথমবার connect করার সময় server host fingerprint যাচাই করবে। Provider-এর দেওয়া fingerprint-এর সঙ্গে মিলিয়ে নিয়ে তারপর trust করবে।

### Server update করো

VPS-এ login করার পর:

Bash

```
sudo apt update
sudo apt upgrade
```

প্রয়োজনে server restart করবে, বিশেষত kernel update হলে।

### Deploy user ও permissions

Provider যদি আগে থেকেই non-root user দেয়, সেটি ব্যবহার করাই ভালো। নিজের user তৈরি করতে হলে administrator হিসেবে:

Bash

```
sudo adduser deploy
sudo usermod -aG sudo deploy
```

এরপর SSH key authentication ও sudo access ঠিকভাবে পরীক্ষা করবে।

সতর্কতা: SSH key login কাজ করছে নিশ্চিত না হয়ে password authentication বন্ধ করবে না। ভুল SSH/firewall configuration করলে server-এ প্রবেশাধিকার হারাতে পারো।

## ৪. Firewall configure করো

Ubuntu-তে `ufw` ব্যবহার করে firewall configure করা যায়।

প্রথমে SSH access অনুমোদন করো:

Bash

```
sudo ufw allow OpenSSH
```

তারপর HTTP ও HTTPS:

Bash

```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Firewall চালু করো:

Bash

```
sudo ufw enable
```

Status পরীক্ষা:

Bash

```
sudo ufw status verbose
```

যদি SSH-এর default port `22` না হয়, তাহলে তোমার প্রকৃত SSH port-টিও আগে allow করতে হবে। VPS provider-এর cloud firewall বা security group-এও একই প্রয়োজনীয় port-গুলো অনুমোদন করো।

### কোন port public হবে?

| Port | ব্যবহার                       | Public access               |
| ---- | ----------------------------- | --------------------------- |
| 22   | SSH, যদি default port হয়      | শুধু প্রয়োজনীয় admin access |
| 80   | HTTP ও certificate validation | হ্যাঁ                       |
| 443  | HTTPS                         | হ্যাঁ                       |
| 8000 | Gunicorn                      | না                          |
| 5432 | PostgreSQL                    | না                          |

Docker-এর published port কিছু ক্ষেত্রে UFW-এর সাধারণ rules প্রত্যাশিতভাবে bypass করতে পারে। তাই শুধু UFW-এর ওপর নির্ভর করবে না—Docker port publishing সীমিত রাখবে এবং provider firewall-ও configure করবে।

## ৫. Domain-কে VPS-এর সঙ্গে যুক্ত করো

ধরি, তোমার domain `example.com` এবং API হবে `api.example.com`।

Domain registrar বা DNS provider-এর dashboard-এ এই record তৈরি করো:

| Type  | Name  | Value                                          |
| ----- | ----- | ---------------------------------------------- |
| A     | `api` | তোমার VPS-এর public IPv4                       |
| A     | `@`   | তোমার VPS-এর IPv4, যদি root domain ব্যবহার করো |
| CNAME | `www` | `example.com`, যদি `www` প্রয়োজন হয়            |

IPv6 ব্যবহার করলে কেবল সঠিক IPv6 configuration থাকলেই AAAA record যোগ করবে।

DNS resolve হচ্ছে কি না পরীক্ষা:

Bash

```
dig +short api.example.com
```

অথবা:

Bash

```
nslookup api.example.com
```

এখানে `api.example.com`-এর পরিবর্তে তোমার প্রকৃত domain বসাবে।

HTTPS certificate নেওয়ার আগে নিশ্চিত হও:

* DNS সঠিক public IP-তে নির্দেশ করছে।

* Port 80 Internet থেকে accessible।

* Port 443-ও খোলা।

* অন্য কোনো service একই port ব্যবহার করছে না।

## ৬. VPS-এ Docker install করো

Ubuntu-তে production-এর জন্য Docker-এর official installation instructions অনুসরণ করা ভালো। Docker Engine, CLI এবং Compose plugin install করার পর পরীক্ষা করো:

Bash

```
docker --version
docker compose version
```

Installation ঠিক আছে কি না যাচাই করতে:

Bash

```
sudo docker run --rm hello-world
```

Docker-এর official installation guide: [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/).

### একটি security বিষয়

`docker` group-এর সদস্যরা কার্যত host machine-এর root-level ক্ষমতা পেতে পারে। তাই deployment-এর সুবিধার জন্য নির্বিচারে user-কে এই group-এ যোগ করবে না। শুরুতে প্রয়োজন হলে `sudo docker ...` ব্যবহার করতে পারো।

## ৭. Project-টি VPS-এ নিয়ে আসো

তোমার Django project GitHub-এ থাকলে VPS-এ clone করতে পারো:

Bash

```
sudo mkdir -p /opt/myproject
sudo chown deploy:deploy /opt/myproject

cd /opt/myproject
git clone YOUR_REPOSITORY_URL .
```

`YOUR_REPOSITORY_URL`-এর জায়গায় তোমার repository URL বসাবে। Private repository হলে SSH deploy key বা অন্য secure authentication পদ্ধতি ব্যবহার করবে; Git URL-এর মধ্যে password বা access token লিখবে না।

Project structure যাচাই করো:

Bash

```
ls -la
```

এবার production `.env` বা secret files তৈরি করো। Local development-এর secret সরাসরি production-এ ব্যবহার না করে নতুন production secret তৈরি করাই ভালো।

Django settings-এ অবশ্যই যাচাই করবে:

Python

Run

```
DEBUG = False
```

`ALLOWED_HOSTS`, database credentials, HTTPS-related settings এবং CORS/CSRF configuration-ও তোমার বাস্তব domain অনুযায়ী ঠিক করতে হবে।

## ৮. Docker Compose-এ public port সীমিত করো

VPS-এ তোমার Compose configuration-এর মূল অংশ এমন হবে:

YAML

```
services:
  backend:
    build:
      context: ./backend
    expose:
      - "8000"
    restart: unless-stopped
    networks:
      - app_network

  db:
    image: postgres:16
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped
    networks:
      - app_network

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    restart: unless-stopped
    networks:
      - app_network

networks:
  app_network:

volumes:
  postgres_data:
```

এটি একটি সংক্ষিপ্ত illustration। তোমার আগের working Compose configuration থেকে environment variables, PostgreSQL initialization, health checks, static/media volumes ও secrets বজায় রাখবে।

এখানে গুরুত্বপূর্ণ পার্থক্য:

YAML

```
expose:
  - "8000"
```

এটি Docker network-এ backend port-টি ব্যবহারযোগ্য করে; host-এর public port হিসেবে publish করে না।

অন্যদিকে:

YAML

```
ports:
  - "8000:8000"
```

সাধারণত host-এর সব interface-এ port publish করে দিতে পারে। এই deployment-এ Gunicorn-এর জন্য সেটি প্রয়োজন নেই।

Application প্রথমবার চালাও:

Bash

```
docker compose up -d --build
```

এরপর:

Bash

```
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic --noinput
docker compose ps
```

Migration ও static collection সফল হয়েছে কি না নিশ্চিত করো। এরপর HTTP-তে Nginx এবং Django API পরীক্ষা করব।

# Part 2: HTTPS ও Let's Encrypt

## ৯. HTTPS কেন প্রয়োজন?

HTTP-তে browser ও server-এর মধ্যে data encrypted থাকে না। HTTPS TLS encryption ব্যবহার করে communication-কে সুরক্ষিত করে এবং server-এর identity যাচাই করতে সাহায্য করে।

Let's Encrypt একটি certificate authority, যা domain validation-এর পর TLS certificate দেয়।

Certificate নিতে আমরা Certbot ব্যবহার করব।

এই অংশে ধরে নিচ্ছি তোমার Nginx Docker container-এর ভেতরে চলছে। তাই certificate এবং ACME challenge files Nginx ও Certbot-এর মধ্যে shared volume দিয়ে ব্যবহার করব।

## ১০. প্রথমে HTTP challenge configure করো

`nginx/default.conf`-এ প্রথমবার certificate নেওয়ার জন্য এই configuration ব্যবহার করো:

Nginx

```
server {
    listen 80;
    server_name api.example.com;

    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }

    location / {
        proxy_pass http://backend:8000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

`api.example.com`-এর জায়গায় তোমার domain বসাবে।

Compose-এর `nginx` service-এ ACME webroot ও certificate volumes mount করো:

YAML

```
services:
  nginx:
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - certbot_webroot:/var/www/certbot
      - letsencrypt_certs:/etc/letsencrypt:ro

  certbot:
    image: certbot/certbot
    volumes:
      - certbot_webroot:/var/www/certbot
      - letsencrypt_certs:/etc/letsencrypt

volumes:
  certbot_webroot:
  letsencrypt_certs:
```

এগুলো আগের Compose file-এর সংশ্লিষ্ট service ও top-level volume definition-এর সঙ্গে merge করবে; duplicate `services:` বা `volumes:` section তৈরি করবে না।

Configuration reload করার আগে syntax পরীক্ষা করো:

Bash

```
docker compose config -q
```

তারপর:

Bash

```
docker compose up -d nginx
```

## ১১. Let's Encrypt certificate নাও

ধরি তোমার domain `api.example.com` এবং email `admin@example.com`।

Bash

```
docker compose run --rm certbot certonly \
  --webroot \
  -w /var/www/certbot \
  -d api.example.com \
  --email admin@example.com \
  --agree-tos \
  --no-eff-email
```

এখানে নিজের email ও domain ব্যবহার করবে।

Certificate issuance সফল হলে সাধারণত certificate ও private key থাকবে:

```
/etc/letsencrypt/live/api.example.com/fullchain.pem
/etc/letsencrypt/live/api.example.com/privkey.pem
```

Private key কখনো public repository-তে commit করবে না বা কাউকে পাঠাবে না।

যদি certificate না পাওয়া যায়, DNS record, port 80, Nginx logs এবং ACME challenge path পরীক্ষা করবে।

## ১২. Nginx-এ HTTPS চালু করো

Certificate সফলভাবে পাওয়ার পরে `nginx/default.conf`-কে এই configuration দিয়ে update করো:

Nginx

```
server {
    listen 80;
    server_name api.example.com;

    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }

    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name api.example.com;

    ssl_certificate
        /etc/letsencrypt/live/api.example.com/fullchain.pem;

    ssl_certificate_key
        /etc/letsencrypt/live/api.example.com/privkey.pem;

    location / {
        proxy_pass http://backend:8000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

এটি একটি basic HTTPS configuration। Production-এ Nginx version ও security requirements অনুযায়ী TLS protocol এবং অন্যান্য security options review করা উচিত।

Compose-এর Nginx service-এ 443 port যোগ করো:

YAML

```
ports:
  - "80:80"
  - "443:443"
```

তারপর configuration পরীক্ষা ও reload করো:

Bash

```
docker compose exec nginx nginx -t
```

Bash

```
docker compose exec nginx nginx -s reload
```

এখন পরীক্ষা করো:

Bash

```
curl -I https://api.example.com/
```

Domain, DNS, certificate এবং API routing ঠিক থাকলে HTTPS response পাবে। Root URL configure না থাকলে `404` আসতে পারে—নিজের বাস্তব API endpoint দিয়েও পরীক্ষা করবে।

## ১৩. Certificate renewal স্বয়ংক্রিয় করো

Let's Encrypt certificate-এর মেয়াদ সীমিত। তাই renewal process configure করা জরুরি।

প্রথমে renewal test করো:

Bash

```
docker compose run --rm certbot renew --dry-run
```

এটি সফল হলে renewal scheduling configure করতে পারো। উদাহরণ হিসেবে host-এর cron থেকে প্রতিদিন renewal check চালানো যায়:

cron

```
17 3 * * * cd /opt/myproject && docker compose run --rm certbot renew --quiet && docker compose exec -T nginx nginx -s reload
```

এটি host-এর crontab-এ যোগ করার উদাহরণ। বাস্তবে cron-এর PATH, Compose project directory, service availability এবং exit status সঠিকভাবে handle করতে হবে। Reload প্রতিদিন চেষ্টা করবে, এমনকি নতুন certificate না হলেও; চাইলে renewal hook ব্যবহার করে শুধু certificate পরিবর্তিত হলে reload করতে পারো।

Renewal test ও actual scheduling নিশ্চিত না করে certificate-এর স্বয়ংক্রিয় renewal হয়েছে বলে ধরে নেবে না।

# Part 3: Production Deployment যাচাই

## ১৪. Final verification checklist

## Deployment verification

0/8

SSH ও firewall

SSH login কাজ করছে এবং কেবল প্রয়োজনীয় public port খোলা।

DNS

api.example.com সঠিক VPS IP-তে resolve হচ্ছে।

Docker

backend, nginx ও db container running/healthy।

Database

Django migration সফল এবং PostgreSQL volume persistent।

Gunicorn

Backend logs-এ startup error নেই; port 8000 public নয়।

HTTPS

Certificate valid এবং HTTP থেকে HTTPS redirect কাজ করছে।

Django security

DEBUG=False, ALLOWED_HOSTS সঠিক, secret নিরাপদ।

Backup ও renewal

Database backup এবং certificate renewal test করা হয়েছে।

## ১৫. Deployment-এর পরে code update করবে কীভাবে?

ধরো, তুমি Django API-তে নতুন feature যোগ করেছ এবং GitHub-এ push করেছ।

VPS-এ:

Bash

```
cd /opt/myproject

git pull
docker compose build backend
docker compose up -d backend
```

এরপর migration প্রয়োজন হলে:

Bash

```
docker compose exec backend python manage.py migrate
```

Static files পরিবর্তিত হলে:

Bash

```
docker compose exec backend python manage.py collectstatic --noinput
```

তারপর logs ও API পরীক্ষা করবে:

Bash

```
docker compose logs --tail=100 backend
curl -I https://api.example.com/health/
```

এটি একটি basic deployment workflow। বড় production system-এ zero-downtime deployment, backward-compatible database migration, rollback strategy এবং automated CI/CD দরকার হতে পারে। Migration চালানোর আগে backup ও application compatibility যাচাই করবে।

## ১৬. তোমার শেখার পরবর্তী ধাপ

Part 5 — CI/CD with GitHub Actions

GitHub-এ code push হলে automated tests, Docker image build এবং VPS deployment workflow তৈরি করা।

Part 5 শেখাও

Production monitoring ও backup

Application logs, server resource usage, database backup/restore, uptime monitoring এবং failure recovery।

Monitoring শেখাও

বাস্তব পরামর্শ: প্রথমে নিজের Ubuntu machine-এ পুরো deployment flow পরীক্ষা করো। এরপর VPS-এ deploy করো। এভাবে Docker networking, Nginx, TLS এবং production debugging—সবকিছু অনেক ভালোভাবে বুঝতে পারবে।

----
# Django Production Deployment Course — Part 5

## GitHub Actions, CI/CD, Automated Testing, Docker Build, Secure VPS Deployment ও Rollback

এই পর্বে আমরা এমন একটি workflow তৈরি করব, যেখানে তুমি GitHub-এ code push করলে স্বয়ংক্রিয়ভাবে:

1. Django application-এর automated tests চলবে।

2. Code ও configuration-এর প্রাথমিক validation হবে।

3. Docker image build হবে।

4. Test সফল হলেই Ubuntu VPS-এ deployment হবে।

5. Deployment ব্যর্থ হলে আগের version-এ ফিরে যাওয়ার ব্যবস্থা থাকবে।

আমরা তোমার Django + Django REST Framework + PostgreSQL + Gunicorn + Nginx + Docker architecture ব্যবহার করব।

## ১. CI/CD কী?

Developer

Code লেখে, tests যোগ করে, GitHub-এ push করে

GitHub Actions — CI

Install dependencies → Run tests → Validate

Build & Publish Docker Image

Unique version tag দিয়ে image তৈরি ও registry-তে push

CD — Ubuntu VPS

নতুন image pull → deploy → health check

Deployment verified

Failure হলে rollback procedure

CI (Continuous Integration): code change-এর সঙ্গে automated checks ও tests চালানো।

CD (Continuous Delivery/Deployment): validated code-কে release বা production environment-এ পৌঁছে দেওয়া। Continuous Delivery-তে release manual approval-এর অপেক্ষায় থাকতে পারে; Continuous Deployment-এ সফল checks-এর পর স্বয়ংক্রিয়ভাবে production-এ release হয়।

## ২. Project structure তৈরি করো

আমরা ধরে নিচ্ছি তোমার GitHub repository-তে এই structure আছে:

```
myproject/
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   ├── config/
│   └── products/
├── nginx/
│   └── default.conf
├── docker-compose.yml
└── .github/
    └── workflows/
        └── deploy.yml
```

এখানে `config` এবং `products` তোমার প্রকৃত Django package ও app name দিয়ে পরিবর্তন করবে।

CI/CD-তে আমাদের তিনটি প্রধান অংশ থাকবে:

* CI: GitHub-hosted runner-এ test চালানো।

* Image registry: Docker image সংরক্ষণ করা।

* CD: SSH-এর মাধ্যমে VPS-এ deployment trigger করা।

আমরা উদাহরণে GitHub Container Registry (GHCR) ব্যবহার করব। GitHub Actions-এর workflow file হবে `.github/workflows/deploy.yml`।

# Part 1 — Automated Testing (CI)

## ৩. Django application-এর tests তৈরি করো

ধরি, তোমার `products` app-এ একটি API আছে। প্রথমে নিশ্চিত করো যে automated test ছাড়া production deployment হচ্ছে না।

`backend/products/tests.py`:

Python

Run

```
from django.test import TestCase
from django.urls import reverse


class HealthCheckTests(TestCase):
    def test_health_endpoint_returns_ok(self):
        response = self.client.get("/health/")

        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.json()["status"], "ok")
```

এখানে `/health/` endpoint আগের deployment course-এ তৈরি করা হয়েছে বলে ধরে নেওয়া হয়েছে।

Test চালাও:

Bash

```
cd backend

python manage.py test
```

Expected result-এর উদাহরণ:

```
Ran 1 test
OK
```

এটি শুধু একটি test। বাস্তব e-commerce বা DRF project-এ authentication, permissions, serializers, product APIs, order creation এবং database constraints-এর test-ও থাকবে।

## ৪. GitHub Actions-এর CI workflow তৈরি করো

ফাইল তৈরি করো:

`.github/workflows/ci.yml`

YAML

```
name: Django CI

on:
  pull_request:
    branches: [main]
  push:
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
          POSTGRES_DB: test_db
          POSTGRES_USER: test_user
          POSTGRES_PASSWORD: test_password
        ports:
          - 5432:5432
        options: >-
          --health-cmd "pg_isready -U test_user -d test_db"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    defaults:
      run:
        working-directory: backend

    env:
      DJANGO_SECRET_KEY: ci-test-secret-key-not-for-production
      DJANGO_DEBUG: "False"
      DJANGO_ALLOWED_HOSTS: localhost,127.0.0.1
      POSTGRES_DB: test_db
      POSTGRES_USER: test_user
      POSTGRES_PASSWORD: test_password
      POSTGRES_HOST: 127.0.0.1
      POSTGRES_PORT: "5432"

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.12"
          cache: pip
          cache-dependency-path: backend/requirements.txt

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Django system check
        run: python manage.py check

      - name: Run tests
        run: python manage.py test
```

### এই workflow কীভাবে কাজ করে?

1. `push` বা `pull_request` হলে workflow শুরু হয়।

2. GitHub একটি temporary Ubuntu runner চালু করে।

3. Python ও PostgreSQL environment তৈরি হয়।

4. Dependency install হয়।

5. Django configuration check হয়।

6. সব test চালানো হয়।

Test ব্যর্থ হলে job fail করবে।

গুরুত্বপূর্ণ: উপরের PostgreSQL credentials কেবল disposable CI database-এর জন্য। এগুলো production credentials নয়। তোমার `settings.py`-তে `DJANGO_SECRET_KEY`, database settings এবং environment variable names একইভাবে configured থাকতে হবে।

## ৫. CI সফল হওয়ার পর কী হবে?

ধরো, তুমি একটি bug fix করে GitHub-এ push করলে।

Tests pass

পরবর্তী ধাপে যাওয়া যাবে।

Tests fail

Deployment বন্ধ থাকবে; আগে bug fix করতে হবে।

আমাদের লক্ষ্য হলো যে code test pass করেনি, সেটি যেন production-এ deploy না হয়।

# Part 2 — Docker Image Build ও Registry

## ৬. Docker image tag কেন দরকার?

প্রতিবার `latest` tag ব্যবহার করলে কোন version production-এ চলছে, তা বোঝা কঠিন হতে পারে।

তার বদলে Git commit SHA দিয়ে version তৈরি করব:

```
ghcr.io/your-username/your-repository/backend:abc123...
```

প্রতিটি commit-এর আলাদা image tag থাকবে। এতে rollback-এর জন্য আগের image চিহ্নিত করা সহজ হবে।

GitHub Container Registry (GHCR) ব্যবহার করলে image-গুলো GitHub-এর সঙ্গে সম্পর্কিত registry-তে রাখা যায়।

## ৭. Docker build ও push job তৈরি করো

এবার আগের CI workflow-এর পরে image build job যুক্ত করব। সহজ রাখার জন্য আলাদা workflow file ব্যবহার করব, যা শুধু `main` branch-এ push হলে এবং CI সফল হলে image build করবে।

`.github/workflows/build.yml`:

YAML

```
name: Build and Publish Docker Image

on:
  workflow_run:
    workflows: ["Django CI"]
    types: [completed]
    branches: [main]

permissions:
  contents: read
  packages: write

jobs:
  build:
    if: >-
      github.event.workflow_run.conclusion == 'success'
      && github.event.workflow_run.event == 'push'

    runs-on: ubuntu-latest

    steps:
      - name: Checkout tested commit
        uses: actions/checkout@v4
        with:
          ref: ${{ github.event.workflow_run.head_sha }}

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Log in to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build and push image
        uses: docker/build-push-action@v6
        with:
          context: ./backend
          push: true
          tags: ghcr.io/${{ github.repository }}/backend:${{ github.event.workflow_run.head_sha }}
```

### এখানে কী হচ্ছে?

* `workflow_run` আগের `Django CI` workflow শেষ হওয়ার পরে build workflow চালায়।

* `conclusion == 'success'` নিশ্চিত করে যে CI সফল হয়েছে।

* `head_sha` দিয়ে ঠিক যে commit test হয়েছে, সেই commit checkout করা হয়।

* `GITHUB_TOKEN` ব্যবহার করে GHCR-এ login করা হয়।

* Docker image build ও push করা হয়।

Security note: `workflow_run`-ভিত্তিক workflow-এ untrusted pull request code checkout করে privileged secrets ব্যবহার করা বিপজ্জনক হতে পারে। এই উদাহরণে শুধু সফল `push` event-এর জন্য build করা হচ্ছে। তবু production-এ workflow permissions সীমিত রাখবে এবং repository settings ও branch protection সঠিকভাবে configure করবে।

আরেকটি বিষয়: `github.repository`-এর owner/repository নাম সাধারণত lowercase হওয়া প্রয়োজন। Repository নাম lowercase না হলে image name lowercase করে নিতে হবে।

# Part 3 — Secure Deployment to Ubuntu VPS

## ৮. VPS-এর Docker Compose-কে image registry-এর সঙ্গে যুক্ত করো

Production VPS-এ code rebuild করার পরিবর্তে registry থেকে tested image pull করব।

`docker-compose.yml`-এর backend service:

YAML

```
services:
  backend:
    image: ${BACKEND_IMAGE:?Set BACKEND_IMAGE}:${IMAGE_TAG:?Set IMAGE_TAG}
    env_file:
      - .env
    expose:
      - "8000"
    restart: unless-stopped
    networks:
      - app_network
```

VPS-এর `/opt/myproject/.env`-এ রাখবে:

dotenv

```
BACKEND_IMAGE=ghcr.io/your-username/your-repository/backend
IMAGE_TAG=your-tested-commit-sha

DJANGO_SECRET_KEY=your-production-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=api.example.com

POSTGRES_DB=ecommerce
POSTGRES_USER=ecommerce_user
POSTGRES_PASSWORD=your-production-database-password
POSTGRES_HOST=db
POSTGRES_PORT=5432
```

এখানে image path ও tag example; তোমার repository-এর সঠিক image name এবং tested commit SHA ব্যবহার করবে।

`.env` file-এর permission সীমিত করো:

Bash

```
chmod 600 /opt/myproject/.env
```

এবং নিশ্চিত করো `.env` Git-এ commit হয়নি।

## ৯. Private GHCR image pull করার ব্যবস্থা

যদি GHCR package private হয়, তাহলে VPS-এ image pull করার জন্য registry authentication লাগবে।

GitHub-এ সীমিত permission-সহ একটি token তৈরি করো, যার অন্তত প্রয়োজনীয় `read:packages` permission আছে। সেটি server-এর নিরাপদ credential storage-এ রাখবে; Git repository, shell script বা workflow log-এ লিখবে না।

প্রথমবার deploy user হিসেবে:

Bash

```
docker login ghcr.io -u YOUR_GITHUB_USERNAME
```

Prompt এলে token-টি password হিসেবে দাও। এটি token command line-এ লিখে দেওয়ার চেয়ে নিরাপদ, যদিও Docker-এর credential storage-ও ঠিকভাবে configure করা প্রয়োজন।

Private registry-এর জন্য সম্ভব হলে credential helper ব্যবহার করো। Public package হলে এই authentication step প্রয়োজন হয় না।

Security note: Docker socket access-সহ `docker` group-এর সদস্যকে প্রায় root-level ক্ষমতাসম্পন্ন user হিসেবে বিবেচনা করবে। VPS-এ deployment user-এর access সীমিত রাখবে।

## ১০. SSH secrets GitHub-এ configure করো

GitHub repository খুলে:

Settings → Secrets and variables → Actions → New repository secret

এই secrets যোগ করো:

| Secret                | কী থাকবে                           |
| --------------------- | ---------------------------------- |
| `VPS_HOST`            | VPS-এর public IP বা hostname       |
| `VPS_USER`            | SSH deployment username            |
| `VPS_SSH_PRIVATE_KEY` | Deployment-এর জন্য private SSH key |
| `VPS_SSH_KNOWN_HOSTS` | VPS-এর যাচাইকৃত SSH host-key entry |

Private key এবং host key এক জিনিস নয়।

* Private key দিয়ে client নিজের পরিচয় প্রমাণ করে।

* Host key দিয়ে client নিশ্চিত হয় যে সে সঠিক SSH server-এ connect করছে।

`VPS_SSH_KNOWN_HOSTS`-এর value server-এর host key আগে থেকেই নির্ভরযোগ্য উপায়ে যাচাই করে সংগ্রহ করবে। Workflow চলার সময় blind `ssh-keyscan` করে পাওয়া key-কে যাচাই ছাড়া trust করবে না।

সম্ভব হলে dedicated deploy user, সীমিত SSH access এবং আলাদা deployment key ব্যবহার করো।

## ১১. VPS-এ deployment script তৈরি করো

Server-এ `/opt/myproject/deploy.sh` ফাইল তৈরি করো:

Bash

```
#!/usr/bin/env bash
set -Eeuo pipefail

cd /opt/myproject

NEW_TAG="${1:?Usage: deploy.sh IMAGE_TAG}"

# Accept only a full Git commit SHA.
if [[ ! "$NEW_TAG" =~ ^[a-f0-9]{40}$ ]]; then
    echo "Invalid image tag"
    exit 1
fi

OLD_TAG="$(grep '^IMAGE_TAG=' .env | cut -d= -f2- || true)"

if [[ -z "$OLD_TAG" ]]; then
    echo "IMAGE_TAG is missing from .env"
    exit 1
fi

echo "Previous image: $OLD_TAG"
echo "New image:      $NEW_TAG"

# Update the version used by Docker Compose.
sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=$NEW_TAG/" .env

rollback() {
    echo "Deployment failed. Attempting rollback..."

    sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=$OLD_TAG/" .env

    if docker compose pull backend &&
       docker compose up -d --no-deps backend; then
        echo "Previous application image restored."
    else
        echo "Rollback failed; manual intervention is required."
    fi
}

# Pull the exact image that passed CI.
if ! docker compose pull backend; then
    sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=$OLD_TAG/" .env
    echo "Image pull failed."
    exit 1
fi

# Run migrations using the new image.
if ! docker compose run --rm backend python manage.py migrate --noinput; then
    sed -i "s/^IMAGE_TAG=.*/IMAGE_TAG=$OLD_TAG/" .env
    echo "Migration failed; application version was not switched."
    exit 1
fi

# Start the new backend image.
if ! docker compose up -d --no-deps backend; then
    rollback
    exit 1
fi

# Verify the deployed API through Nginx and HTTPS.
for attempt in $(seq 1 12); do
    if curl --fail --silent --show-error \
        https://api.example.com/health/; then
        echo
        echo "Deployment successful: $NEW_TAG"
        exit 0
    fi

    sleep 5
done

rollback
exit 1
```

নিজের domain দিয়ে `https://api.example.com/health/` পরিবর্তন করবে।

এরপর executable permission দাও:

Bash

```
chmod 750 /opt/myproject/deploy.sh
```

### Script-এর গুরুত্বপূর্ণ সীমাবদ্ধতা

এটি একটি শিক্ষামূলক rollback script, পূর্ণাঙ্গ zero-downtime release system নয়।

* Migration database schema পরিবর্তন করে ফেললে আগের application image-এ ফিরে গেলেও schema আগের অবস্থায় ফিরে আসে না।

* `migrate` সফল হলেও API health check ব্যর্থ হতে পারে।

* Rollback-এর পর আগের image pull বা start ব্যর্থ হলে manual recovery দরকার হতে পারে।

* `curl` check domain-এর DNS ও HTTPS routing-সহ পুরো request path পরীক্ষা করে; তাই DNS সমস্যা থাকলেও deployment verification fail করতে পারে।

Production database migration backward-compatible রাখবে, backup নেবে এবং rollback procedure আগে staging-এ পরীক্ষা করবে।

# Part 4 — Automatic Deployment Workflow

## ১২. GitHub Actions দিয়ে VPS-এ deploy করো

ফাইল তৈরি করো:

`.github/workflows/deploy.yml`

YAML

```
name: Deploy to Production

on:
  workflow_run:
    workflows: ["Build and Publish Docker Image"]
    types: [completed]
    branches: [main]

permissions:
  contents: read

concurrency:
  group: production-deployment
  cancel-in-progress: false

jobs:
  deploy:
    if: >-
      github.event.workflow_run.conclusion == 'success'
      && github.event.workflow_run.event == 'push'

    runs-on: ubuntu-latest

    steps:
      - name: Configure SSH
        env:
          SSH_PRIVATE_KEY: ${{ secrets.VPS_SSH_PRIVATE_KEY }}
          SSH_KNOWN_HOSTS: ${{ secrets.VPS_SSH_KNOWN_HOSTS }}
        run: |
          install -m 700 -d ~/.ssh
          printf '%s\n' "$SSH_PRIVATE_KEY" > ~/.ssh/id_ed25519
          chmod 600 ~/.ssh/id_ed25519
          printf '%s\n' "$SSH_KNOWN_HOSTS" > ~/.ssh/known_hosts
          chmod 600 ~/.ssh/known_hosts

      - name: Deploy tested image to VPS
        env:
          VPS_HOST: ${{ secrets.VPS_HOST }}
          VPS_USER: ${{ secrets.VPS_USER }}
          IMAGE_TAG: ${{ github.event.workflow_run.head_sha }}
        run: |
          ssh \
            -i ~/.ssh/id_ed25519 \
            -o StrictHostKeyChecking=yes \
            -o IdentitiesOnly=yes \
            "$VPS_USER@$VPS_HOST" \
            "cd /opt/myproject && ./deploy.sh '$IMAGE_TAG'"
```

### Workflow-এর flow

1. Developer pushes to `main`

2. Django CI passes

3. Docker image is published

Commit SHA tag

4. SSH deployment starts

Pull → Migrate → Restart → Health check

Success

New release active

Failure

Rollback attempt

একটি গুরুত্বপূর্ণ design detail: এই workflow-গুলো `workflow_run` ব্যবহার করছে। GitHub-এর security model অনুযায়ী এ ধরনের downstream workflow-এ privileged secrets ব্যবহার করার আগে upstream workflow-এর code ও event origin সম্পর্কে সতর্ক থাকতে হবে। এখানে pull-request event-এ deployment বন্ধ রাখা হয়েছে। আরও শক্ত production setup-এ protected environment, required reviewers এবং trusted branch/tag restrictions ব্যবহার করো।

# Part 5 — Manual Rollback ও Debugging

## ১৩. আগের image-এ ফিরে যাবে কীভাবে?

ধরো, production-এ নতুন version deploy করার পরে API-তে bug দেখা দিল।

প্রথমে বর্তমান image tag দেখো:

Bash

```
cd /opt/myproject
grep '^IMAGE_TAG=' .env
```

তারপর GitHub Actions-এর successful build history থেকে আগের known-good commit SHA খুঁজে বের করো।

সেই SHA দিয়ে deploy script চালাও:

Bash

```
./deploy.sh PREVIOUS_COMMIT_SHA
```

এখানে `PREVIOUS_COMMIT_SHA`-এর জায়গায় প্রকৃত ৪০-character commit SHA বসাবে।

এতে ওই image pull করে deployment ও health check চালানোর চেষ্টা করবে।

সতর্কতা: আগের image-এ ফিরে যাওয়া মানেই database rollback নয়। Schema migration, data transformation বা destructive changes হয়ে থাকলে আলাদা database recovery plan দরকার। Production migration-এ backward-compatible expand-and-contract strategy অনুসরণ করা ভালো।

## ১৪. Deployment ব্যর্থ হলে কী পরীক্ষা করবে?

| সমস্যা                  | কী পরীক্ষা করবে                                                           |
| ----------------------- | ------------------------------------------------------------------------- |
| CI test fail            | GitHub Actions-এর test logs                                               |
| Docker build fail       | Dockerfile, dependencies ও build logs                                     |
| GHCR image pull fail    | Image path, tag এবং registry authentication                               |
| SSH connection fail     | VPS host, user, private key, firewall ও host key                          |
| Gunicorn start fail     | `docker compose logs backend`                                             |
| Database migration fail | Migration files, database connection ও schema compatibility               |
| HTTPS health check fail | DNS, certificate, Nginx routing এবং Django logs                           |
| Rollback fail           | পুরোনো image availability, Compose configuration ও database compatibility |

VPS-এ useful commands:

Bash

```
docker compose ps
docker compose logs --tail=100 backend
docker compose logs --tail=100 nginx
docker compose logs --tail=100 db
```

Image tags পরীক্ষা:

Bash

```
docker image ls
```

এবং API health endpoint:

Bash

```
curl -i https://api.example.com/health/
```

## ১৫. Production-ready হওয়ার আগে checklist

## Part 5 deployment checklist

0/9

Django tests স্থানীয়ভাবে সফল

GitHub CI workflow সফল

Docker image GHCR-এ publish হয়েছে

VPS SSH secrets ও verified host key configure করা

Production environment variables ও secrets নিরাপদ

Database backup এবং migration strategy প্রস্তুত

Deployment-এর পর HTTPS health check সফল

Staging-এ rollback পরীক্ষা করা

GitHub main branch protection ও approval rules configure করা

আমার CI/CD configuration review করো

## এই পর্বে তুমি কী শিখলে?

তোমার deployment workflow এখন ধারণাগতভাবে এমন:

Code push → Automated tests → Docker image build → GHCR publish → SSH deployment → Health check → Rollback attempt if needed

বাস্তবে production-এ ব্যবহার করার আগে একটি গুরুত্বপূর্ণ উন্নতি করো: GitHub Actions-এ protected production environment ও manual approval যোগ করো এবং database migration ও rollback staging server-এ পরীক্ষা করো।

পরবর্তী ধাপ হিসেবে Part 6 — Production Monitoring, Centralized Logging, PostgreSQL Backup/Restore, Alerting এবং Disaster Recovery শিখলে deployment-এর পাশাপাশি application পরিচালনা করাও শিখবে।
