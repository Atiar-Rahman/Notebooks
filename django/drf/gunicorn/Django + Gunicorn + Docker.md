
# Class 1: Django REST Framework + Gunicorn + Docker

আমরা একদম শুরু থেকে একটি ছোট কিন্তু বাস্তব Django REST Framework API তৈরি করব, তারপর Gunicorn দিয়ে চালিয়ে Docker container-এর মধ্যে deploy করব।

এই ক্লাসে প্রথমে PostgreSQL, Nginx বা VPS যোগ করব না। আগে মূল বিষয়গুলো বুঝব, যাতে পরের ধাপে এগুলো সহজে যোগ করতে পারো।

## ১. আমরা কী তৈরি করব?

একটি Product API, যেখানে product list দেখা যাবে এবং প্রতিটি product-এর তথ্য JSON format-এ পাওয়া যাবে।

তোমার Browser / API Client

GET /api/products/

Docker Container

Gunicorn → Django REST Framework

JSON Response

Product data

আজকের লক্ষ্য:

* Django ও DRF API তৈরি করা।

* Gunicorn দিয়ে API চালানো।

* Docker image তৈরি করা।

* Container থেকে API request পাঠিয়ে পরীক্ষা করা।

## ২. প্রয়োজনীয় software

তোমার Ubuntu-তে Python ও Docker লাগবে। আগে terminal-এ পরীক্ষা করো:

Bash

```
python3 --version
docker --version
docker compose version
```

Docker install করা না থাকলে Ubuntu-তে Docker Engine-এর official installation guide অনুসরণ করবে: [Docker Engine installation for Ubuntu](https://docs.docker.com/engine/install/ubuntu/)।

এখন project তৈরি করি।

## ৩. Project folder তৈরি করো

Terminal-এ নিচের command-গুলো একে একে চালাও:

Bash

```
mkdir django-gunicorn-docker
cd django-gunicorn-docker

python3 -m venv venv
source venv/bin/activate

pip install django djangorestframework gunicorn

pip freeze > requirements.txt
```

এখন Django project তৈরি করো:

Bash

```
django-admin startproject config .
python manage.py startapp products
```

এখানে:

* `config` — Django project configuration।

* `products` — আমাদের API application।

* `gunicorn` — production WSGI server।

* `requirements.txt` — project-এর Python dependencies।

## ৪. Project structure বুঝে নাও

এখন তোমার folder দেখতে এমন হবে:

```
django-gunicorn-docker/
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
├── products/
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── manage.py
├── requirements.txt
└── venv/
```

`venv/` হলো তোমার local Python virtual environment। Docker image-এ এটি copy করব না।

## ৫. Django-তে DRF configure করো

`config/settings.py` ফাইল খোলো। `INSTALLED_APPS`-এর মধ্যে নিচের app-গুলো যোগ করো:

Python

Run

```
INSTALLED_APPS = [
    # Django default apps
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    # Third-party apps
    "rest_framework",

    # Local apps
    "products",
]
```

এখন `products/views.py` ফাইলে API তৈরি করব।

## ৬. প্রথম API endpoint তৈরি করো

`products/views.py`:

Python

Run

```
from rest_framework.decorators import api_view
from rest_framework.response import Response


@api_view(["GET"])
def product_list(request):
    products = [
        {
            "id": 1,
            "name": "Keyboard",
            "price": 1200,
        },
        {
            "id": 2,
            "name": "Mouse",
            "price": 600,
        },
        {
            "id": 3,
            "name": "Monitor",
            "price": 15000,
        },
    ]

    return Response({
        "success": True,
        "count": len(products),
        "results": products,
    })
```

এই উদাহরণে database ব্যবহার করছি না। API-টি বোঝার সুবিধার জন্য Python list থেকে data পাঠাচ্ছে।

এবার `products/urls.py` নামে নতুন ফাইল তৈরি করো:

Python

Run

```
from django.urls import path
from .views import product_list

urlpatterns = [
    path("products/", product_list, name="product-list"),
]
```

তারপর `config/urls.py` পরিবর্তন করো:

Python

Run

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("api/", include("products.urls")),
]
```

এখন আমাদের endpoint:

```
GET /api/products/
```

## ৭. Docker ছাড়াই API পরীক্ষা করো

প্রথমে Django development server চালাও:

Bash

```
python manage.py runserver
```

Browser-এ খোলো:

[http://127.0.0.1:8000/api/products/](http://127.0.0.1:8000/api/products/)

অথবা terminal থেকে:

Bash

```
curl http://127.0.0.1:8000/api/products/
```

তুমি এমন JSON response পাবে:

JSON

```
{
  "success": true,
  "count": 3,
  "results": [
    {
      "id": 1,
      "name": "Keyboard",
      "price": 1200
    },
    {
      "id": 2,
      "name": "Mouse",
      "price": 600
    },
    {
      "id": 3,
      "name": "Monitor",
      "price": 15000
    }
  ]
}
```

এখানে API কাজ করছে কি না সেটি আগে নিশ্চিত করো। এরপর Docker যোগ করব।

## ৮. Dockerfile তৈরি করো

Project-এর root folder-এ `Dockerfile` নামে একটি ফাইল তৈরি করো। ফাইলের নামের শেষে কোনো extension থাকবে না।

Dockerfile

dockerfile

```
FROM python:3.12-slim

# Container-এর working directory
WORKDIR /app

# Python dependency file copy
COPY requirements.txt .

# Dependencies install
RUN pip install --no-cache-dir -r requirements.txt

# Project code copy
COPY . .

# Container-এর application port
EXPOSE 8000

# Gunicorn দিয়ে Django চালানো
CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "2"]
```

### Dockerfile-এর প্রতিটি অংশের কাজ

| Instruction | কাজ                                                |
| ----------- | -------------------------------------------------- |
| `FROM`      | Python-সহ base image নেয়                           |
| `WORKDIR`   | Container-এর working directory নির্ধারণ করে        |
| `COPY`      | Host থেকে file image-এ কপি করে                     |
| `RUN`       | Image build করার সময় command চালায়                 |
| `EXPOSE`    | Application কোন port-এ listen করবে তা document করে |
| `CMD`       | Container শুরু হলে Gunicorn চালায়                  |

সবচেয়ে গুরুত্বপূর্ণ লাইন:

dockerfile

```
CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "2"]
```

আগে তুমি চালিয়েছিলে:

Bash

```
python manage.py runserver
```

এখন container চালু হলে তার পরিবর্তে Gunicorn Django-কে serve করবে।

`0.0.0.0` দেওয়া হয়েছে, যাতে Docker-এর বাইরে থেকে mapped port-এর মাধ্যমে application-এ পৌঁছানো যায়।

## ৯. `.dockerignore` তৈরি করো

Root folder-এ `.dockerignore` ফাইল তৈরি করো:

```
venv/
__pycache__/
*.py[cod]
.git/
.gitignore
.env
*.sqlite3
.pytest_cache/
.coverage
```

এটি Docker build context থেকে অপ্রয়োজনীয় file বাদ দেয়। বিশেষ করে `.env`-এর মতো secret file image-এ copy হওয়া আটকাতে সাহায্য করে।

## ১০. Docker image তৈরি করো

প্রথমে project structure পরীক্ষা করো:

Bash

```
ls
```

এখানে `Dockerfile`, `requirements.txt`, `manage.py` দেখতে পাবে।

তারপর image build করো:

Bash

```
docker build -t django-gunicorn-api .
```

এখানে:

* `docker build` — image তৈরি করে।

* `-t django-gunicorn-api` — image-এর নাম দেয়।

* `.` — বর্তমান directory-কে build context হিসেবে ব্যবহার করে।

Image তৈরি হয়েছে কি না:

Bash

```
docker images
```

## ১১. Container চালাও

Bash

```
docker run --rm \
  --name django-api \
  -p 8000:8000 \
  django-gunicorn-api
```

এখানে `-p 8000:8000`-এর অর্থ:

* প্রথম `8000` — তোমার host computer-এর port।

* দ্বিতীয় `8000` — container-এর Gunicorn port।

এখন browser-এ আবার খোলো:

[Docker-এর ভেতরে চলা Product API](http://127.0.0.1:8000/api/products/)

এবার request-এর response Docker container-এর ভেতরে চলা Gunicorn ও Django থেকে আসছে।

## ১২. Container-এর log দেখো

আরেকটি terminal খোলো:

Bash

```
docker logs django-api
```

Container চালু আছে কি না:

Bash

```
docker ps
```

Container বন্ধ করতে প্রথম terminal-এ `Ctrl+C` চাপো। `--rm` দেওয়ায় container বন্ধ হলে সেটি মুছে যাবে; image থাকবে।

## ১৩. Common error ও সমাধান

Error: `ModuleNotFoundError: No module named 'gunicorn'`

`requirements.txt`-এ Gunicorn আছে কি না যাচাই করো। তারপর image পুনরায় build করো।

Bash

```
pip freeze > requirements.txt
docker build -t django-gunicorn-api .
```

Error: `ModuleNotFoundError: No module named 'config'`

`Dockerfile`-এ `WORKDIR /app` এবং `COPY . .` ঠিক আছে কি না দেখো। `manage.py` ও `config/` folder project root-এ থাকতে হবে।

Error: `port is already allocated`

Host-এর port `8000` অন্য application ব্যবহার করলে অন্য port ব্যবহার করো:

Bash

```
docker run --rm -p 8001:8000 django-gunicorn-api
```

এরপর `http://127.0.0.1:8001/api/products/` খোলো।

Error: `DisallowedHost`

`config/settings.py`-এর `ALLOWED_HOSTS`-এ প্রয়োজনীয় host যোগ করো:

Python

Run

```
ALLOWED_HOSTS = ["localhost", "127.0.0.1"]
```

পরিবর্তনের পর image rebuild করে container চালাও।

## ১৪. এখন পর্যন্ত কী শিখলে?

Learning checklist

0/5 complete

Django project ও DRF endpoint তৈরি করেছি

Gunicorn-এর WSGI command বুঝেছি

Dockerfile তৈরি করেছি

Docker image build করেছি

Container থেকে API test করেছি

### গুরুত্বপূর্ণ production note

এই উদাহরণটি শেখার জন্য। Public production deployment-এর আগে আরও কাজ করতে হবে:

* `DEBUG=False`, secure `SECRET_KEY` এবং environment-based configuration।

* PostgreSQL ও persistent volume।

* Database migrations।

* Static files ও health check।

* HTTPS, firewall এবং নিরাপদ reverse proxy configuration।

এছাড়া, project settings-এ development-এর জন্য তৈরি default secret-টি production-এ ব্যবহার করবে না।

পরবর্তী ক্লাস: এই project-এ PostgreSQL যুক্ত করে `Docker Compose` দিয়ে Django + Gunicorn + PostgreSQL একসঙ্গে চালানো। এতে API-র product data আর Python list-এ থাকবে না, database থেকে আসবে।


--------

# Class 2: Django + Gunicorn + PostgreSQL + Docker Compose

এই ক্লাসে আগের `django-gunicorn-docker` project-টিকেই upgrade করব। এবার Product API-র data Python list থেকে নয়, PostgreSQL database থেকে আসবে।

শেষে আমাদের architecture হবে:

Client / Browser

GET /api/products/

Django + Gunicorn Container

DRF Views, Serializers, ORM

PostgreSQL Container

Products table + persistent volume

আজ যা শিখবে:

* PostgreSQL-এ Django connect করা।

* `Product` model তৈরি করা।

* Serializer ও ModelViewSet ব্যবহার করে API বানানো।

* Docker Compose দিয়ে দুটি container চালানো।

* Migration, database data এবং API পরীক্ষা করা।

## ১. Project structure আপডেট করো

আগের project-এ নিচের ফাইলগুলো যোগ ও পরিবর্তন করব:

```
django-gunicorn-docker/
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── products/
│   ├── migrations/
│   ├── models.py
│   ├── serializers.py       # নতুন
│   ├── views.py
│   └── urls.py
├── .env                    # নতুন
├── .dockerignore
├── Dockerfile
├── compose.yaml             # নতুন
├── manage.py
└── requirements.txt
```

## ২. PostgreSQL driver install করো

Django-কে PostgreSQL-এর সঙ্গে connect করতে driver লাগবে। Project-এর virtual environment চালু রেখে:

Bash

```
source venv/bin/activate
pip install "psycopg[binary]>=3.2,<4"
pip freeze > requirements.txt
```

এখন `requirements.txt`-এ Django, DRF, Gunicorn এবং PostgreSQL driver থাকবে।

## ৩. Product database model তৈরি করো

আগের `products/models.py` ফাইলটি পরিবর্তন করো:

Python

Run

```
from django.db import models


class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2,
    )
    stock = models.PositiveIntegerField(default=0)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

### Model-এর field-গুলো বুঝে নাও

| Field         | কাজ                              |
| ------------- | -------------------------------- |
| `name`        | Product-এর নাম                   |
| `description` | বিস্তারিত বিবরণ; ফাঁকা রাখা যাবে |
| `price`       | দশমিকসহ মূল্য                    |
| `stock`       | কতটি পণ্য মজুত আছে               |
| `created_at`  | কখন product তৈরি হয়েছে           |

এই model থেকে Django PostgreSQL-এ `products_product` নামে একটি table তৈরি করতে পারবে।

## ৪. Serializer তৈরি করো

`products/serializers.py` নামে ফাইল তৈরি করো:

Python

Run

```
from rest_framework import serializers
from .models import Product


class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "description",
            "price",
            "stock",
            "created_at",
        ]
        read_only_fields = ["id", "created_at"]
```

Serializer কেন প্রয়োজন?

Database-এর `Product` object-কে JSON response-এ রূপান্তর করে। আবার client থেকে JSON data এলে সেটি validate করে model-এ save করতেও সাহায্য করে।

## ৫. Database থেকে data আনার API তৈরি করো

আগের `products/views.py`-এর Python list-ভিত্তিক code মুছে এটি লেখো:

Python

Run

```
from rest_framework.viewsets import ModelViewSet
from .models import Product
from .serializers import ProductSerializer


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all().order_by("-created_at")
    serializer_class = ProductSerializer
```

এখন `Product.objects.all()` database থেকে product সংগ্রহ করবে।

`ModelViewSet` ব্যবহার করায় আমরা স্বয়ংক্রিয়ভাবে এই operation-গুলো পাব:

* `GET` — সব product দেখা।

* `POST` — নতুন product তৈরি।

* `GET /<id>/` — একটি product দেখা।

* `PUT` — product সম্পূর্ণ update করা।

* `PATCH` — product-এর নির্দিষ্ট field update করা।

* `DELETE` — product মুছে ফেলা।

## ৬. API URL configure করো

`products/urls.py`:

Python

Run

```
from rest_framework.routers import DefaultRouter
from .views import ProductViewSet

router = DefaultRouter()
router.register("products", ProductViewSet, basename="product")

urlpatterns = router.urls
```

`config/urls.py`:

Python

Run

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path("admin/", admin.site.urls),
    path("api/", include("products.urls")),
]
```

এখন endpoint-গুলো হবে:

| Method | Endpoint           | কাজ             |
| ------ | ------------------ | --------------- |
| GET    | `/api/products/`   | সব product      |
| POST   | `/api/products/`   | নতুন product    |
| GET    | `/api/products/1/` | ID 1-এর product |
| PATCH  | `/api/products/1/` | product update  |
| DELETE | `/api/products/1/` | product delete  |

এখন পর্যন্ত আমরা API ও model তৈরি করেছি। পরের কাজ হচ্ছে Django-কে PostgreSQL-এর সঙ্গে connect করা।

## ৭. Django settings-এ PostgreSQL configuration যোগ করো

`config/settings.py`-এ `import os` যোগ করো:

Python

Run

```
import os
```

`settings.py`-তে আগের `DATABASES` configuration-এর জায়গায় এই code বসাও:

Python

Run

```
if os.getenv("DB_ENGINE") == "postgresql":
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.postgresql",
            "NAME": os.environ["POSTGRES_DB"],
            "USER": os.environ["POSTGRES_USER"],
            "PASSWORD": os.environ["POSTGRES_PASSWORD"],
            "HOST": os.getenv("DB_HOST", "db"),
            "PORT": os.getenv("DB_PORT", "5432"),
        }
    }
else:
    # Local development-এর জন্য SQLite
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.sqlite3",
            "NAME": BASE_DIR / "db.sqlite3",
        }
    }
```

এখানে দুটি mode আছে:

* Local machine-এ `DB_ENGINE` না দিলে SQLite ব্যবহার হবে।

* Docker Compose থেকে `DB_ENGINE=postgresql` দিলে PostgreSQL ব্যবহার হবে।

একই model ও migration ব্যবহার করেই দুই environment-এ কাজ করতে পারবে।

এছাড়া `INSTALLED_APPS`-এ নিশ্চিত করো:

Python

Run

```
INSTALLED_APPS = [
    # Django-এর default apps...
    "rest_framework",
    "products",
]
```

Host configuration-ও environment থেকে নেওয়া যায়:

Python

Run

```
DEBUG = os.getenv("DJANGO_DEBUG", "False").lower() == "true"

ALLOWED_HOSTS = [
    host.strip()
    for host in os.getenv(
        "DJANGO_ALLOWED_HOSTS",
        "127.0.0.1,localhost",
    ).split(",")
    if host.strip()
]
```

আগের `SECRET_KEY`-কে production-এ সরাসরি hardcode করে রেখো না। Environment variable থেকে নাও:

Python

Run

```
SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY", "")
```

এটি খালি থাকলে production startup-এর আগে secret configure করতে হবে।

## ৮. `.env` file তৈরি করো

Project-এর root-এ `.env` তৈরি করো:

dotenv

```
POSTGRES_DB=shopdb
POSTGRES_USER=shopuser
POSTGRES_PASSWORD=replace-with-a-long-random-password

DB_ENGINE=postgresql
DB_HOST=db
DB_PORT=5432

DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1
```

`replace-with-...`-এর জায়গায় নিজের random password ও secret বসাবে। এটি শেখার local environment; production-এর secret আলাদাভাবে generate ও manage করবে।

খুব গুরুত্বপূর্ণ: `.env` GitHub-এ commit করবে না।

`.gitignore`-এ যোগ করো:

```
.env
venv/
__pycache__/
*.py[cod]
db.sqlite3
```

আর `.dockerignore`-এ যোগ করো:

```
.env
.git/
venv/
__pycache__/
*.py[cod]
db.sqlite3
```

`.env` বাদ দেওয়ার ফলে secret Docker image-এর ভেতরে copy হবে না।

## ৯. Docker Compose configuration তৈরি করো

আগের project root-এ `compose.yaml` ফাইল তৈরি করো:

YAML

```
services:
  db:
    image: postgres:16
    restart: unless-stopped
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        [
          "CMD-SHELL",
          "pg_isready -U $${POSTGRES_USER} -d $${POSTGRES_DB}"
        ]
      interval: 5s
      timeout: 5s
      retries: 10

  backend:
    build: .
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DB_ENGINE: postgresql
      DB_HOST: db
      DB_PORT: "5432"
    ports:
      - "127.0.0.1:8000:8000"
    depends_on:
      db:
        condition: service_healthy
    command:
      [
        "gunicorn",
        "config.wsgi:application",
        "--bind",
        "0.0.0.0:8000",
        "--workers",
        "2"
      ]

volumes:
  postgres_data:
```

### এই configuration কী করছে?

* `db`: PostgreSQL database container চালায়।

* `backend`: তোমার Django ও Gunicorn application চালায়।

* `depends_on`: PostgreSQL healthy হওয়ার পর backend service শুরু করতে সাহায্য করে।

* `postgres_data`: container পুনরায় তৈরি হলেও database data ধরে রাখে।

* `ports`: শুধু host-এর `127.0.0.1:8000`-এ API প্রকাশ করে; অন্য কম্পিউটার থেকে সরাসরি access করা যাবে না।

`DB_HOST=db` খুব গুরুত্বপূর্ণ। Docker Compose-এর ভেতরে `db` হলো PostgreSQL service-এর নাম। তাই Django `localhost` নয়, `db` host ব্যবহার করে database-এ connect করবে।

## ১০. Database migration তৈরি করো

প্রথমে virtual environment activate করে model-এর migration file তৈরি করো:

Bash

```
source venv/bin/activate

python manage.py makemigrations products
```

এতে সাধারণত `products/migrations/0001_initial.py` তৈরি হবে।

Migration হলো Django-কে জানানোর উপায় যে database-এ কোন table বা field তৈরি করতে হবে।

এরপর image build করো:

Bash

```
docker compose build
```

## ১১. PostgreSQL ও Django migration চালাও

প্রথমে database container-এর সঙ্গে Django migration চালাও:

Bash

```
docker compose run --rm backend python manage.py migrate
```

এখানে Django PostgreSQL-এর সঙ্গে connect করে প্রয়োজনীয় table তৈরি করবে।

এরপর দুটি service চালু করো:

Bash

```
docker compose up -d
```

চলছে কি না পরীক্ষা করো:

Bash

```
docker compose ps
```

Expected result-এ `db` ও `backend` service running থাকবে। PostgreSQL-এর health status-ও পরীক্ষা করো।

Log দেখতে:

Bash

```
docker compose logs -f backend
```

অথবা শুধু PostgreSQL-এর log:

Bash

```
docker compose logs -f db
```

## ১২. API test করো

GET — সব product দেখা

Browser-এ খোলো:

[Product API খুলুন](http://127.0.0.1:8000/api/products/)

অথবা:

Bash

```
curl http://127.0.0.1:8000/api/products/
```

প্রথমবার database-এ product না থাকলে response হবে:

JSON

```
{
  "count": 0,
  "next": null,
  "previous": null,
  "results": []
}
```

DRF-এর default pagination configure করা না থাকলে response হবে `[]`। তাই এই উদাহরণের `count`-সহ response default pagination enabled থাকলে পাওয়া যাবে। Pagination না থাকলেও API ঠিকভাবে কাজ করবে।

### নতুন product তৈরি করো

Terminal থেকে POST request পাঠাও:

Bash

```
curl -X POST http://127.0.0.1:8000/api/products/ \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Mechanical Keyboard",
    "description": "USB keyboard",
    "price": "2500.00",
    "stock": 10
  }'
```

DRF-এর default permission settings অনুযায়ী request অনুমোদিত হলে নতুন product database-এ save হবে এবং response-এ product-এর `id` পাওয়া যাবে।

তারপর আবার GET request পাঠাও:

Bash

```
curl http://127.0.0.1:8000/api/products/
```

এবার product দেখতে পাবে। এখন data Python list থেকে নয়, PostgreSQL database থেকে আসছে।

## ১৩. Database-এর data সত্যিই persist হচ্ছে কি না পরীক্ষা করো

Container বন্ধ করে আবার চালাও:

Bash

```
docker compose down
docker compose up -d
```

আবার API request পাঠাও:

Bash

```
curl http://127.0.0.1:8000/api/products/
```

আগের product থেকে যাওয়ার কথা, কারণ আমরা `postgres_data` named volume ব্যবহার করেছি।

Database persistence

`docker compose down` volume মুছে দেয় না। কিন্তু `docker compose down -v` চালালে এই Compose project-এর `postgres_data` volume-ও মুছে যেতে পারে—তখন database-এর data হারাবে। Production-এ backup ছাড়া কখনো এটি চালাবে না।

## ১৪. Model পরিবর্তন করলে কী করবে?

ধরো, `Product` model-এ নতুন field যোগ করলে:

Python

Run

```
is_active = models.BooleanField(default=True)
```

তারপর:

Bash

```
python manage.py makemigrations products
docker compose build backend
docker compose run --rm backend python manage.py migrate
docker compose up -d
```

এভাবে model পরিবর্তন database schema-তে প্রয়োগ হবে। Production-এ migration করার আগে backup এবং migration compatibility যাচাই করবে।

## আজকের ক্লাসের final checklist

নিজে করে যাচাই করো

0 / 7

Product model তৈরি করেছি

ModelSerializer ও ModelViewSet ব্যবহার করেছি

PostgreSQL database container চালিয়েছি

Docker Compose দিয়ে backend ও database যুক্ত করেছি

Migration চালিয়ে database table তৈরি করেছি

POST ও GET request দিয়ে data পরীক্ষা করেছি

Container restart করে data persistence পরীক্ষা করেছি

পরবর্তী ক্লাসে এই project-কে আরও production-oriented করব: Docker Compose-এর health checks, non-root user, environment-based configuration, static files এবং Gunicorn worker configuration। এরপর Nginx ও Ubuntu VPS-এ deployment-এর দিকে এগোনো যাবে।

----
# Class 3: Django + Gunicorn + Docker — Production Hardening

এই ক্লাসে আগের project-টিকে আরও production-ready করব। আমরা Django + Gunicorn + PostgreSQL + Docker Compose-ই ব্যবহার করব; নতুন করে project তৈরি করতে হবে না।

আজকের লক্ষ্য:

1. Docker container-এর health check তৈরি করা।

2. Root user-এর পরিবর্তে non-root user দিয়ে Django চালানো।

3. Secret ও settings environment variables থেকে নেওয়া।

4. Django static files collect ও serve করার ব্যবস্থা করা।

5. Gunicorn workers, timeout ও logging configure করা।

6. সবকিছু Docker Compose দিয়ে test করা।

একটি বিষয় আগে পরিষ্কার করি: Docker health check শুধু service-এর অবস্থা জানায়; এটি নিজে থেকে সব application error ঠিক করে না। একইভাবে, non-root user ব্যবহার করলে container-এর security বাড়ে, কিন্তু এটি একাই সম্পূর্ণ security solution নয়।

## ১. Final architecture

API Client

HTTP request

Django + Gunicorn

Non-root user · Health endpoint · JSON API

PostgreSQL

Persistent named volume

Static files

Django collectstatic → shared volume → local static server for testing

আজকের ক্লাসে static files test করার জন্য একটি আলাদা lightweight static server ব্যবহার করব। Public production-এ এগুলো Nginx, CDN বা object storage দিয়ে serve করা ভালো।

## ২. Environment-based settings ঠিক করো

আমাদের `.env` file আগের মতোই থাকবে, তবে production configuration একটু পরিষ্কার করব।

Project root-এর `.env`:

dotenv

```
POSTGRES_DB=shopdb
POSTGRES_USER=shopuser
POSTGRES_PASSWORD=replace-with-a-strong-password

DB_ENGINE=postgresql
DB_HOST=db
DB_PORT=5432

DJANGO_SECRET_KEY=replace-with-a-long-random-secret
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=localhost,127.0.0.1
DJANGO_CSRF_TRUSTED_ORIGINS=
```

নিজের secret generate করতে পারো:

Bash

```
python -c "import secrets; print(secrets.token_urlsafe(50))"
```

Output-টি `DJANGO_SECRET_KEY`-এর value হিসেবে বসাও। Password-ও আলাদা strong random value হবে।

`.env`-কে Git-এ commit করবে না। `.gitignore`-এ এটি থাকা নিশ্চিত করো:

```
.env
venv/
__pycache__/
*.py[cod]
db.sqlite3
```

এবার `config/settings.py`-তে নিচের configuration নিশ্চিত করো। আগের একই setting থাকলে duplicate না করে update করবে।

Python

Run

```
import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.environ.get("DJANGO_SECRET_KEY", "")

DEBUG = os.getenv("DJANGO_DEBUG", "False").lower() == "true"

ALLOWED_HOSTS = [
    host.strip()
    for host in os.getenv(
        "DJANGO_ALLOWED_HOSTS",
        "localhost,127.0.0.1",
    ).split(",")
    if host.strip()
]

CSRF_TRUSTED_ORIGINS = [
    origin.strip()
    for origin in os.getenv(
        "DJANGO_CSRF_TRUSTED_ORIGINS", ""
    ).split(",")
    if origin.strip()
]
```

Production configuration ভুলে application যেন অনিচ্ছাকৃতভাবে চালু না হয়, তার জন্য `settings.py`-তে validation যোগ করো:

Python

Run

```
if not SECRET_KEY:
    raise RuntimeError("DJANGO_SECRET_KEY is required")

if not DEBUG and SECRET_KEY == "django-insecure-change-me":
    raise RuntimeError("Replace the insecure Django secret key")
```

এখানে দ্বিতীয় validation কেবল ওই নির্দিষ্ট insecure placeholder-টি আটকায়; এটি random secret-এর মান যাচাই করে না। আসল secret কখনো source code-এ রাখবে না।

Database configuration:

Python

Run

```
if os.getenv("DB_ENGINE") == "postgresql":
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.postgresql",
            "NAME": os.environ["POSTGRES_DB"],
            "USER": os.environ["POSTGRES_USER"],
            "PASSWORD": os.environ["POSTGRES_PASSWORD"],
            "HOST": os.getenv("DB_HOST", "db"),
            "PORT": os.getenv("DB_PORT", "5432"),
            "CONN_MAX_AGE": 60,
        }
    }
else:
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.sqlite3",
            "NAME": BASE_DIR / "db.sqlite3",
        }
    }
```

`CONN_MAX_AGE=60` database connection পুনর্ব্যবহার করতে সাহায্য করে। এটি সব workload-এর জন্য সর্বোত্তম মান নয়; production-এ connection সংখ্যা ও database limit-ও বিবেচনা করবে।

## ৩. Static files configure করো

Django-র admin ও browsable API-এর মতো page-এ CSS/JavaScript প্রয়োজন হতে পারে। Static file-এর জন্য WhiteNoise ব্যবহার করব, যাতে আপাতত Nginx ছাড়াও Django application static assets serve করতে পারে।

Install করো:

Bash

```
pip install whitenoise
pip freeze > requirements.txt
```

`config/settings.py`-তে `MIDDLEWARE`-এর শুরুতে WhiteNoise middleware বসাও—`SecurityMiddleware`-এর ঠিক পরে:

Python

Run

```
MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",

    # বাকি default middleware অপরিবর্তিত রাখবে
]
```

Static settings যোগ করো:

Python

Run

```
STATIC_URL = "static/"
STATIC_ROOT = BASE_DIR / "staticfiles"

STORAGES = {
    "default": {
        "BACKEND": "django.core.files.storage.FileSystemStorage",
    },
    "staticfiles": {
        "BACKEND": (
            "whitenoise.storage.CompressedManifestStaticFilesStorage"
        ),
    },
}
```

এখন `collectstatic` command Django-র static files-গুলো `staticfiles/` directory-তে সংগ্রহ করবে। WhiteNoise compressed static files serve করতে পারবে।

## ৪. Health-check endpoint তৈরি করো

Container running থাকা আর application ঠিকমতো কাজ করা এক বিষয় নয়। তাই এমন endpoint তৈরি করব যা Django ও database connection দুটোই পরীক্ষা করবে।

`products/views.py`-তে আগের `ProductViewSet` রেখে নিচের view যোগ করো:

Python

Run

```
from django.db import connection
from django.db.utils import DatabaseError
from django.http import JsonResponse


def health_check(request):
    try:
        with connection.cursor() as cursor:
            cursor.execute("SELECT 1")
            cursor.fetchone()

        return JsonResponse({
            "status": "ok",
            "database": "ok",
        })

    except DatabaseError:
        return JsonResponse(
            {
                "status": "error",
                "database": "unavailable",
            },
            status=503,
        )
```

`products/urls.py`-তে health endpoint যোগ করো। আগের router configuration-টিও রাখবে:

Python

Run

```
from django.urls import path
from rest_framework.routers import DefaultRouter

from .views import ProductViewSet, health_check

router = DefaultRouter()
router.register("products", ProductViewSet, basename="product")

urlpatterns = [
    path("health/", health_check, name="health-check"),
    *router.urls,
]
```

এখন endpoint:

```
GET /api/health/
```

Database ঠিক থাকলে response:

JSON

```
{
  "status": "ok",
  "database": "ok"
}
```

Database connection ব্যর্থ হলে `503 Service Unavailable` দেবে। এই endpoint-এ database-এর secret বা connection details প্রকাশ করা হচ্ছে না।

## ৫. Dockerfile-এ non-root user যোগ করো

আগের Dockerfile-এ application সাধারণত root user হিসেবে চলত। এখন `appuser` নামে আলাদা user তৈরি করব।

Root directory-র `Dockerfile` পুরোপুরি update করো:

dockerfile

```
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Dependencies install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Application-এর জন্য non-root user
RUN groupadd --system appgroup \
    && useradd --system --gid appgroup appuser \
    && mkdir -p /app/staticfiles \
    && chown -R appuser:appgroup /app

# Project files copy
COPY --chown=appuser:appgroup . .

# Root হিসেবে নয়, appuser হিসেবে application চালাবে
USER appuser

EXPOSE 8000

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "2", \
     "--timeout", "60", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

### নতুন কী হলো?

* `PYTHONDONTWRITEBYTECODE=1` — Python bytecode file তৈরি করা কমায়।

* `PYTHONUNBUFFERED=1` — log দ্রুত stdout/stderr-এ পাঠায়।

* `appuser` — application root privileges ছাড়া চালায়।

* `COPY --chown` — project files-এর ownership ঠিক রাখে।

* `--access-logfile -` ও `--error-logfile -` — Docker logs থেকে Gunicorn-এর log দেখা যায়।

`--workers 2` শেখার জন্য একটি প্রাথমিক মান। তোমার server-এর CPU, RAM ও workload অনুযায়ী পরে পরিবর্তন করবে।

## ৬. Static files startup-এ collect করো

Container startup-এর সময় `collectstatic` চালানোর জন্য root directory-তে `entrypoint.sh` তৈরি করো:

Bash

```
#!/bin/sh
set -eu

python manage.py collectstatic --noinput

exec gunicorn config.wsgi:application \
    --bind 0.0.0.0:8000 \
    --workers "${GUNICORN_WORKERS:-2}" \
    --timeout "${GUNICORN_TIMEOUT:-60}" \
    --access-logfile - \
    --error-logfile -
```

এই file executable করো:

Bash

```
chmod +x entrypoint.sh
```

এবার Dockerfile-এর শেষের `CMD` পরিবর্তন করে দাও:

dockerfile

```
COPY --chown=appuser:appgroup entrypoint.sh /app/entrypoint.sh

ENTRYPOINT ["/app/entrypoint.sh"]
```

Dockerfile-এ `ENTRYPOINT`-এর আগের `CMD` সরিয়ে দাও, যাতে Gunicorn দুবার চালু না হয়।

এখানে একটি গুরুত্বপূর্ণ বিষয়: `staticfiles/` directory-তে `appuser`-এর write permission আছে, তাই startup-এ `collectstatic` চালানো সম্ভব। Production-এ প্রতিবার startup-এ static files collect করার পরিবর্তে image build/release stage-এ collect করা আরও ভালো হতে পারে। আপাতত শেখার জন্য এই পদ্ধতি সহজ।

## ৭. Docker Compose-এ health checks যোগ করো

এবার `compose.yaml` update করো:

YAML

```
services:
  db:
    image: postgres:16
    restart: unless-stopped
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    healthcheck:
      test:
        [
          "CMD-SHELL",
          "pg_isready -U $${POSTGRES_USER} -d $${POSTGRES_DB}"
        ]
      interval: 5s
      timeout: 3s
      retries: 10
      start_period: 10s

  backend:
    build: .
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DB_ENGINE: postgresql
      DB_HOST: db
      DB_PORT: "5432"
      GUNICORN_WORKERS: ${GUNICORN_WORKERS:-2}
      GUNICORN_TIMEOUT: ${GUNICORN_TIMEOUT:-60}
    ports:
      - "127.0.0.1:8000:8000"
    depends_on:
      db:
        condition: service_healthy
    healthcheck:
      test:
        [
          "CMD",
          "python",
          "-c",
          "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/api/health/', timeout=3)"
        ]
      interval: 15s
      timeout: 5s
      retries: 3
      start_period: 20s

volumes:
  postgres_data:
```

`.env`-এ এই দুটি configuration-ও যোগ করতে পারো:

dotenv

```
GUNICORN_WORKERS=2
GUNICORN_TIMEOUT=60
```

### Health check কীভাবে কাজ করে?

| Configuration       | অর্থ                                     |
| ------------------- | ---------------------------------------- |
| `interval: 15s`     | প্রতি ১৫ সেকেন্ডে পরীক্ষা                |
| `timeout: 5s`       | পাঁচ সেকেন্ডে উত্তর না পেলে check ব্যর্থ |
| `retries: 3`        | পরপর তিনবার ব্যর্থ হলে unhealthy         |
| `start_period: 20s` | startup-এর জন্য grace period             |

PostgreSQL-এর health check `pg_isready` দিয়ে database readiness পরীক্ষা করে। Backend-এর health check HTTP endpoint-এ request পাঠায়, যেটি database connection-ও পরীক্ষা করে।

মনে রেখো, Docker-এর `unhealthy` status দেখালেই container স্বয়ংক্রিয়ভাবে restart হয় না। `restart: unless-stopped` মূলত process/container বন্ধ হয়ে যাওয়ার ক্ষেত্রে কাজ করে, health status-এর কারণে নয়।

## ৮. নতুন image build ও application চালাও

আগে থেকেই চালু container থাকলে:

Bash

```
docker compose down
```

তারপর নতুন image build করো:

Bash

```
docker compose build --no-cache
```

Database migration চালাও:

Bash

```
docker compose run --rm backend python manage.py migrate
```

এরপর services চালু করো:

Bash

```
docker compose up -d
```

Status দেখো:

Bash

```
docker compose ps
```

আরও বিস্তারিত health status:

Bash

```
docker inspect \
  --format='{{json .State.Health}}' \
  "$(docker compose ps -q backend)"
```

Log দেখো:

Bash

```
docker compose logs -f backend
```

সবকিছু ঠিক থাকলে backend `healthy` হবে এবং Gunicorn-এর log দেখতে পাবে।

## ৯. API ও static files পরীক্ষা করো

Health check

Bash

```
curl -i http://127.0.0.1:8000/api/health/
```

Expected: `HTTP 200` এবং database status `ok`।

Product API

Bash

```
curl http://127.0.0.1:8000/api/products/
```

Django admin static files

`collectstatic` সফল হয়েছে কি না দেখো:

Bash

```
docker compose exec backend \
  python manage.py collectstatic --noinput
```

এরপর admin page খোলো: [Django Admin](http://127.0.0.1:8000/admin/)।

Static file serve হচ্ছে কি না নিশ্চিত করতে browser developer tools-এর Network tab-এ CSS/JS request-এর status দেখো।

## ১০. Production-এর আগে security checklist

Production readiness

0/9

DEBUG=False এবং শক্তিশালী DJANGO_SECRET_KEY

SECRET ও password Git/Docker image-এ নেই

Application non-root appuser হিসেবে চলছে

PostgreSQL-এর port public host-এ expose করা হয়নি

Database volume ও backup strategy আছে

Health endpoint application ও database পরীক্ষা করে

Static files collect ও serve হচ্ছে

Gunicorn workers ও timeout server resource অনুযায়ী নির্ধারিত

Public deployment-এ HTTPS এবং reverse proxy পরিকল্পনা আছে

### আজকের সবচেয়ে গুরুত্বপূর্ণ শেখা

* Gunicorn Django application চালায়।

* Dockerfile application image তৈরি করে।

* Docker Compose backend ও PostgreSQL একসঙ্গে পরিচালনা করে।

* Health check service-এর readiness ও application health পর্যবেক্ষণ করে।

* Non-root user container-এর privilege কমায়।

* WhiteNoise এই উদাহরণে Nginx ছাড়াই Django static files serve করতে সাহায্য করে।

পরবর্তী ধাপ হবে Nginx + Gunicorn + Django + PostgreSQL + Docker Compose দিয়ে Ubuntu VPS-এ HTTPS-সহ production deployment। সেখানে domain, reverse proxy, TLS certificate, firewall এবং deployment-time migrations নিয়ে কাজ করব।

---
