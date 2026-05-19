

[https://www.youtube.com/watch?v=PWKyhmqV2ls](https://www.youtube.com/watch?v=PWKyhmqV2ls)
চলো এখন **Fly.io-তে free-তে Django app deploy করা step-by-step দেখি 🔥
এটা Render-এর চেয়ে একটু technical, কিন্তু once setup করলে খুব smooth 😎

---

# 🎯 Goal

👉 Django app live করা (free tier)
👉 production-ready setup (Gunicorn + Postgres optional)

---

# 🧱 Step 1: Fly CLI install

👉 install করো:

```bash id="jym61q"
curl -L https://fly.io/install.sh | sh
```

👉 login:

```bash id="k0o9mw"
fly auth login
```

---

# 📁 Step 2: Project prepare

👉 তোমার Django project ready থাকতে হবে:

```bash id="2jzjzj"
requirements.txt
manage.py
myproject/
```

👉 ensure:

```bash id="9j2l1g"
pip install gunicorn whitenoise psycopg2-binary
```

---

# ⚙️ Step 3: settings.py (production config)

```python id="w3u7np"
import os

DEBUG = False

ALLOWED_HOSTS = ["*"]

SECRET_KEY = os.environ.get("SECRET_KEY")

STATIC_ROOT = os.path.join(BASE_DIR, "staticfiles")
```

👉 whitenoise:

```python id="gzt2go"
MIDDLEWARE = [
    "whitenoise.middleware.WhiteNoiseMiddleware",
    ...
]
```

---

# 🚀 Step 4: Fly init

```bash id="7c34mg"
fly launch
```

👉 prompt এ:

* App name → choose করো
* Region → nearest (e.g. sin, bom)
* PostgreSQL → no (optional)

👉 এটা auto generate করবে:

```bash id="mgm7fa"
fly.toml
Dockerfile
```

---

# 🐳 Step 5: Dockerfile check/fix

👉 ensure আছে:

```dockerfile id="xv9c3g"
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

---

# 🌐 Step 6: Static collect

👉 deploy এর আগে:

```bash id="5ov9j7"
python manage.py collectstatic
```

---

# 🔐 Step 7: Environment variables

```bash id="2x4j8l"
fly secrets set SECRET_KEY=your_secret
```

👉 DB থাকলে:

```bash id="4g8n5w"
fly secrets set DATABASE_URL=postgres://...
```

---

# 🚀 Step 8: Deploy

```bash id="x6ztxg"
fly deploy
```

👉 success হলে:

```bash id="9x3d2f"
https://your-app.fly.dev
```

---

# 🧪 Step 9: Run migration (important ⚠️)

```bash id="mx4kz0"
fly ssh console
python manage.py migrate
```

---

# ⚡ Celery use করতে চাইলে?

👉 Fly.io-তে worker run করা যায়:

```bash id="7qg9jd"
fly scale count 1
```

👉 বা separate process:

```toml id="iyf1n7"
[processes]
web = "gunicorn myproject.wsgi:application"
worker = "celery -A myproject worker --loglevel=info"
```

---

# 🔥 Redis use

👉 external use করো:

* Upstash Redis (free tier)

```bash id="y9q7ke"
fly secrets set REDIS_URL=redis://...
```

---

# ❗ Common সমস্যা

## ❌ static load না

```python id="4t3e2x"
STATIC_URL = "/static/"
```

---

## ❌ app crash

```bash id="0j7q9p"
fly logs
```

---

## ❌ migration হয়নি

```bash id="1w8q2r"
fly ssh console
python manage.py migrate
```

---

# 🎯 Final Architecture

```text id="fsk9k2"
User →
    Fly.io →
        Gunicorn →
            Django API →
                Celery →
                    Redis →
                        Worker
```

---

# 💬 Final Summary

* Fly.io = full control + free tier ✅
* Docker-based deploy
* Gunicorn use
* Redis external

---

চাও তো আমি তোমার project অনুযায়ী
👉 **ready-to-use fly.toml + Dockerfile + settings config** বানিয়ে দিতে পারি (copy-paste ready) 👍
Django app কে Fly.io তে deploy করার সহজ ধাপগুলো:

1. `flyctl` install করুন
   [Fly.io CLI Install Guide](https://fly.io/docs/flyctl/install/?utm_source=chatgpt.com)

2. Fly.io login করুন

```bash
fly auth login
```

3. Django project folder এ যান

```bash
cd your_project
```

4. App initialize করুন

```bash
fly launch
```

এটা `fly.toml` এবং Docker setup তৈরি করবে।

5. `Dockerfile` না থাকলে তৈরি করুন
   উদাহরণ:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["gunicorn", "project_name.wsgi:application", "--bind", "0.0.0.0:8000"]
```

6. `requirements.txt` এ নিশ্চিত করুন:

```txt
gunicorn
whitenoise
psycopg2-binary
```

7. Django settings update করুন

```python
ALLOWED_HOSTS = ["your-app.fly.dev"]

STATIC_ROOT = BASE_DIR / "staticfiles"

MIDDLEWARE = [
    "whitenoise.middleware.WhiteNoiseMiddleware",
]
```

8. Static collect করুন

```bash
python manage.py collectstatic
```

9. Deploy করুন

```bash
fly deploy
```

10. Database migrate করুন

```bash
fly ssh console
python manage.py migrate
```

Official docs:
[Fly.io Django Deployment Docs](https://fly.io/docs/django/?utm_source=chatgpt.com)

চাইলে আমি তোমার জন্য:

* ready-to-use `Dockerfile`
* production `settings.py`
* PostgreSQL setup
* custom domain setup
* GitHub Actions auto deploy

সব তৈরি করে দিতে পারি।
নিচে একটি production-ready Django + PostgreSQL + Fly.io setup দিলাম।

---

# Project Structure

```text id="m2sk5n"
project/
│
├── app/
├── project/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── requirements.txt
├── Dockerfile
├── fly.toml
├── .dockerignore
└── .github/workflows/deploy.yml
```

---

# 1. requirements.txt

```txt id="d4h4v5"
Django>=5.0
gunicorn
whitenoise
psycopg2-binary
dj-database-url
python-dotenv
```

---

# 2. Production Dockerfile

```dockerfile id="g4bg2h"
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

RUN apt-get update && apt-get install -y gcc libpq-dev

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

EXPOSE 8000

CMD ["gunicorn", "project.wsgi:application", "--bind", "0.0.0.0:8000"]
```

`project` এর জায়গায় তোমার Django project name দাও।

---

# 3. .dockerignore

```txt id="z5pq90"
venv
__pycache__
*.pyc
db.sqlite3
.env
.git
```

---

# 4. Production settings.py

```python id="j3r5gs"
from pathlib import Path
import os
import dj_database_url

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.environ.get("SECRET_KEY")

DEBUG = False

ALLOWED_HOSTS = [
    ".fly.dev",
    "yourdomain.com",
    "www.yourdomain.com"
]

CSRF_TRUSTED_ORIGINS = [
    "https://*.fly.dev",
    "https://yourdomain.com",
    "https://www.yourdomain.com"
]

INSTALLED_APPS = [
    ...
]

MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",
    ...
]

STATIC_URL = "/static/"
STATIC_ROOT = BASE_DIR / "staticfiles"

STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"

DATABASES = {
    "default": dj_database_url.config(
        default=os.environ.get("DATABASE_URL")
    )
}

SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')

SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_SSL_REDIRECT = True
```

---

# 5. Fly.io PostgreSQL Setup

Database create করো:

```bash id="o9e8dz"
fly postgres create
```

Database attach করো:

```bash id="l3stjj"
fly postgres attach --app your-app-name
```

এটা automatic `DATABASE_URL` secret add করবে।

---

# 6. SECRET_KEY add করা

```bash id="pj1k5k"
fly secrets set SECRET_KEY="your-secret-key"
```

Generate secret key:

```bash id="el8lyv"
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

---

# 7. fly.toml Example

```toml id="mr8kec"
app = "your-app-name"

[build]

[env]
  PORT = "8000"

[http_service]
  internal_port = 8000
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 1
```

---

# 8. Deploy Command

```bash id="h01m92"
fly deploy
```

---

# 9. Run Migrations

```bash id="f9lf1u"
fly ssh console
```

তারপর:

```bash id="x12kz9"
python manage.py migrate
```

---

# 10. Custom Domain Setup

Domain add:

```bash id="2qj3vh"
fly certs add yourdomain.com
```

Check certificates:

```bash id="8lt9xv"
fly certs show yourdomain.com
```

DNS এ যোগ করো:

| Type | Name | Value     |
| ---- | ---- | --------- |
| A    | @    | Fly.io IP |
| AAAA | @    | Fly IPv6  |

Fly.io docs:
[Fly.io Custom Domains Docs](https://fly.io/docs/networking/custom-domain/?utm_source=chatgpt.com)

---

# 11. GitHub Actions Auto Deploy

`.github/workflows/deploy.yml`

```yaml id="i0c41m"
name: Deploy Django to Fly.io

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy App
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: superfly/flyctl-actions/setup-flyctl@master

      - run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```

---

# 12. GitHub Secret Add

GitHub repo → Settings → Secrets → Actions

Add:

```text id="3mjlwm"
FLY_API_TOKEN
```

Token generate:

```bash id="bzmyyv"
fly tokens create deploy
```

---

# 13. Useful Fly.io Commands

Logs:

```bash id="6l6z0u"
fly logs
```

Open app:

```bash id="mdu5sm"
fly open
```

SSH:

```bash id="gw4nzy"
fly ssh console
```

Scale memory:

```bash id="5jvbce"
fly scale memory 512
```

---

Official Resources:

* [Fly.io Official Website](https://fly.io?utm_source=chatgpt.com)
* [Fly.io Django Docs](https://fly.io/docs/django/?utm_source=chatgpt.com)
* [Django Official Website](https://www.djangoproject.com/?utm_source=chatgpt.com)

চাইলে এখন আমি তোমাকে:

* Celery + Redis setup
* Nginx reverse proxy
* Docker Compose local dev
* CI/CD with staging + production
* Free SSL + Cloudflare
* Media file storage (S3/Cloudinary)

এগুলোর complete production setup-ও দিতে পারি।
যদি database ছাড়া simple Django app Fly.io তে deploy করতে চাও, তাহলে setup আরও সহজ হবে।

---

# requirements.txt

```txt id="nmb6xj"
Django>=5.0
gunicorn
whitenoise
```

---

# Dockerfile

```dockerfile id="2f0yq6"
FROM python:3.12-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

EXPOSE 8000

CMD ["gunicorn", "project.wsgi:application", "--bind", "0.0.0.0:8000"]
```

`project` এর জায়গায় তোমার Django project name দাও।

---

# settings.py (Production)

```python id="d3mg8r"
from pathlib import Path
import os

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.environ.get("SECRET_KEY")

DEBUG = False

ALLOWED_HOSTS = [
    ".fly.dev",
]

INSTALLED_APPS = [
    ...
]

MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",
    ...
]

STATIC_URL = "/static/"
STATIC_ROOT = BASE_DIR / "staticfiles"

STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"

# SQLite disable করতে চাইলে:
DATABASES = {}
```

---

# SECRET_KEY add

```bash id="0i1pt9"
fly secrets set SECRET_KEY="your-secret-key"
```

Generate key:

```bash id="x0o85m"
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

---

# fly.toml

```toml id="j7wo0r"
app = "your-app-name"

[build]

[env]
  PORT = "8000"

[http_service]
  internal_port = 8000
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 1
```

---

# Deploy

```bash id="ck6px6"
fly launch
```

তারপর:

```bash id="d45k7r"
fly deploy
```

---

# GitHub Actions Auto Deploy

`.github/workflows/deploy.yml`

```yaml id="7d3vbd"
name: Deploy Django to Fly.io

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: superfly/flyctl-actions/setup-flyctl@master

      - run: flyctl deploy --remote-only
        env:
          FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}
```

---

# GitHub Secret

Generate token:

```bash id="dyv93e"
fly tokens create deploy
```

তারপর GitHub → Settings → Secrets → Actions এ:

```text id="vq5ifx"
FLY_API_TOKEN
```

add করো।

---

Useful Docs:

* [Fly.io Official Website](https://fly.io?utm_source=chatgpt.com)
* [Fly.io Django Docs](https://fly.io/docs/django/?utm_source=chatgpt.com)
* [Gunicorn Docs](https://gunicorn.org/?utm_source=chatgpt.com)
