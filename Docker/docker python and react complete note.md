আমি একটা **Simple Django + React project Docker দিয়ে run করার complete step-by-step guide** দেখাচ্ছি। এটা beginner friendly এবং production-style structure। 🚀

---

# 1️⃣ Project Structure

```
django-react-docker
│
├── backend
│   ├── Dockerfile
│   ├── requirements.txt
│   └── django_app
│       ├── manage.py
│       └── config
│
├── frontend
│   ├── Dockerfile
│   └── package.json
│
└── docker-compose.yml
```

---

# 2️⃣ Django Backend Setup

### Create Django Project

```bash
mkdir backend
cd backend

django-admin startproject config
cd config
django-admin startapp api
```

---

### requirements.txt

```
Django
djangorestframework
gunicorn
```

---

### Django settings

`config/settings.py`

```python
ALLOWED_HOSTS = ["*"]

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'rest_framework',
]
```

---

### Simple API

`views.py`

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET'])
def hello(request):
    return Response({"message": "Hello from Django"})
```

---

### urls.py

```python
from django.urls import path
from .views import hello

urlpatterns = [
    path("hello/", hello),
]
```

---

# 3️⃣ Django Dockerfile

`backend/Dockerfile`

```dockerfile
FROM python:3.11

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

---

# 4️⃣ React Frontend Setup

```bash
npx create-react-app frontend
cd frontend
```

---

### Simple API Call

`App.js`

```javascript
import { useEffect, useState } from "react";

function App() {
  const [msg, setMsg] = useState("");

  useEffect(() => {
    fetch("http://localhost:8000/hello/")
      .then(res => res.json())
      .then(data => setMsg(data.message));
  }, []);

  return (
    <div>
      <h1>{msg}</h1>
    </div>
  );
}

export default App;
```

---

# 5️⃣ React Dockerfile

`frontend/Dockerfile`

```dockerfile
FROM node:18

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

CMD ["npm", "run","dev"]
```

---

# 6️⃣ docker-compose.yml

root folder এ:

```yaml
version: "3"

services:

  backend:
    build: ./backend
    ports:
      - "8000:8000"
    volumes:
      - ./backend:/app

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
```

---

# 7️⃣ Run Project

project root এ:

```bash
docker compose up --build
```

---

# 8️⃣ Open Browser

Frontend

```
http://localhost:3000
```

Backend API

```
http://localhost:8000/hello
```

---

# Output

React page এ দেখাবে:

```
Hello from Django
```

---

💡 **Real production setup হলে normally এগুলো add করা হয়**

- PostgreSQL
    
- Nginx
    
- Gunicorn
    
- Redis
    
- Celery
    

---

ঠিক আছে 😎, তুমি চাইছো **real production-ready fullstack setup** যেখানে:

- Django backend (Gunicorn)
    
- React frontend (built & served via Nginx)
    
- PostgreSQL database
    
- Redis (cache / Celery broker)
    
- Celery (async tasks)
    
# **Docker + Docker Compose** দিয়ে complete production setup তৈরি করে দিচ্ছি।

---

# 1️⃣ Project structure (production-ready)

```
fulstack/
│
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   └── your apps...
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   └── src/
│
├── nginx/
│   └── default.conf
│
├── .env
└── docker-compose.yml
```

---

# 2️⃣ Backend Dockerfile (`backend/Dockerfile`)

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Gunicorn run
CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
```

> Dev জন্য `python manage.py runserver` use করতে পারো, production এ Gunicorn use হবে।

---

# 3️⃣ Frontend Dockerfile (`frontend/Dockerfile`)

```dockerfile
FROM node:22 AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build

# Nginx serve
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

# 4️⃣ Nginx config (`nginx/default.conf`)

```nginx
server {
    listen 80;

    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://backend:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

> `/api/` route backend Django app এ forward করবে।

---

# 5️⃣ `.env` file

```
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_HOST=db
POSTGRES_PORT=5432
REDIS_HOST=redis
REDIS_PORT=6379
SECRET_KEY=django-secret-key
DEBUG=False
```

---

# 6️⃣ Docker Compose (`docker-compose.yml`)

```yaml
version: "3.9"

services:
  backend:
    build: ./backend
    env_file:
      - ./.env
    depends_on:
      - db
      - redis
    ports:
      - "8000:8000"

  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

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

volumes:
  pgdata:
```

---

# 7️⃣ Django settings for Redis + Celery

`backend/settings.py`:

```python
import os
from decouple import config

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('POSTGRES_DB'),
        'USER': config('POSTGRES_USER'),
        'PASSWORD': config('POSTGRES_PASSWORD'),
        'HOST': config('POSTGRES_HOST'),
        'PORT': config('POSTGRES_PORT'),
    }
}

# Redis (for caching / Celery broker)
CELERY_BROKER_URL = f"redis://{config('REDIS_HOST')}:{config('REDIS_PORT')}/0"
CELERY_RESULT_BACKEND = f"redis://{config('REDIS_HOST')}:{config('REDIS_PORT')}/0"

# Debug & Secret
SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', cast=bool, default=False)
```

`backend/celery.py`:

```python
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')
app = Celery('backend')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

---

# 8️⃣ Workflow

```bash
# Build & start everything
docker compose up --build -d

# Django migrate
docker compose exec backend python manage.py migrate

# Celery worker logs
docker compose logs -f celery
```

- Frontend: `http://localhost/` (served by Nginx)
    
- Backend: `http://localhost/api/` (proxied by Nginx)
    
- Redis + Celery: background async tasks
    

---

💡 **Notes:**

1. Development এ live reload করতে:
    
    - Backend: volume mount + `runserver`
        
    - Frontend: volume mount + Vite dev server
        
2. Production: Gunicorn + Nginx + Celery + Redis
    

---
# যদি এরপরও error আসে

একটা command run করে দেখান:

tree -L 3 backend

আমি দেখব:

- Django project structure
    
- celery config
    
- Docker path



# Dockerfile প্রায় ঠিকই আছে 👍। আমি একটু explain করি এবং একটা **best practice version**ও দেখাই।

---

# তোমার Dockerfile

```dockerfile
FROM python:3.11

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
CMD [ "python3","manage.py","runserver","0.0.0.0:8000" ]
```

### প্রতিটি লাইনের কাজ

**1️⃣ Base Image**

```dockerfile
FROM python:3.11
```

Docker Hub থেকে Python 3.11 image নেয়।

---

**2️⃣ Working Directory**

```dockerfile
WORKDIR /app
```

container এর ভিতরে `/app` folder create করে।

সব command এখানেই run হবে।

---

**3️⃣ requirements.txt copy**

```dockerfile
COPY requirements.txt .
```

host machine থেকে container এ requirements.txt নেয়।

---

**4️⃣ Dependencies install**

```dockerfile
RUN pip install -r requirements.txt
```

Django / DRF / অন্যান্য library install করে।

---

**5️⃣ Project files copy**

```dockerfile
COPY . .
```

পুরো Django project container এ copy হয়।

---

**6️⃣ Run Django**

```dockerfile
CMD [ "python3","manage.py","runserver","0.0.0.0:8000" ]
```

container start হলে Django runserver start হয়।

`0.0.0.0` মানে **container বাইরে থেকেও access করা যাবে**।

---

# Better Dockerfile (Recommended)

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

### Improvements

**python:3.11-slim**

- image size ছোট
    
- faster build
    

---

**--no-cache-dir**

```dockerfile
pip install --no-cache-dir
```

image size কম হয়।

---

**EXPOSE**

```dockerfile
EXPOSE 8000
```

container port documentation।

---

# Run Docker

```bash
docker build -t django-app .
```

```bash
docker run -p 8000:8000 django-app
```

open

```
http://localhost:8000
```

---

# Django + Docker Common Mistake ⚠️

settings.py তে এটা দিতে হয়

```python
ALLOWED_HOSTS = ["*"]
```

নাহলে container এ error আসতে পারে।

---

# ১️⃣ প্রথমে আসল error দেখতে হবে

এই command চালাও:

```bash
docker compose build --no-cache
```

অথবা

```bash
docker build .
```

এরপর **উপরে একটু scroll করলে exact error দেখা যাবে** যেমন:

* package not found
* gcc missing
* psycopg2 build error
* numpy build error

---

# ২️⃣ Common Problem 1 — requirements.txt missing

চেক করো:

```bash
ls backend
```

দেখো `requirements.txt` আছে কিনা।

---

# ৩️⃣ Common Problem 2 — requirements.txt ভুল

উদাহরণ:

```txt
Django
djangorestframework
gunicorn
```

এটা safe।

কিন্তু অনেক সময় এমন থাকে:

```txt
tensorflow
torch
opencv-python
```

এগুলো build করতে extra dependency লাগে।

---

# ৪️⃣ Python Slim Image Problem

যদি তোমার Dockerfile এমন হয়:

```dockerfile
FROM python:3.11-slim
```

তাহলে build tools লাগবে।

Fix:

```dockerfile
FROM python:3.11

WORKDIR /app

COPY requirements.txt .

RUN pip install --upgrade pip
RUN pip install -r requirements.txt

COPY . .

CMD ["python","manage.py","runserver","0.0.0.0:8000"]
```

---

# ৫️⃣ Hard Reset Docker Build

অনেক সময় cache problem হয়।

```bash
docker compose down
docker system prune -a
docker compose up --build
```

---

# ৬️⃣ Most Common Real Error

যদি requirements.txt এ থাকে:

```txt
psycopg2
```

তাহলে install হবে না।

Replace করো:

```txt
psycopg2-binary
```

---

# ৭️⃣ Fast Debug Trick

container build করার আগে local এ test করো

```bash
pip install -r requirements.txt
```

যদি local এ fail করে তাহলে docker এও fail করবে।

---


# ৩️⃣ Docker rebuild করো

```bash
docker compose down
docker compose build --no-cache
docker compose up
```

---

# 🚀 সবচেয়ে সহজ সমাধান (Recommended)

project folder **home directory তে move করো**।

### Step 1

```bash
mv /media/atiar/DDDDD/docker_project/fulstack ~/fulstack
```

### Step 2

```bash
cd ~/fulstack
```

### Step 3

```bash
docker compose up --build
```

---

# ⚡ কেন এই সমস্যা হচ্ছে

তোমার project path:

```text
/media/atiar/DDDDD/docker_project/fulstack
```

Linux এ `/media` সাধারণত **external drive / mounted drive** হয়।

Docker অনেক সময় security কারণে এই path share করে না।

---

# 🔧 Alternative Fix (যদি move না করতে চাও)

`docker-compose.yml` এ যদি থাকে:

```yaml
volumes:
  - ./backend:/app
```

তাহলে temporarily remove করো:

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
```

এতে volume mount হবে না, errorও হবে না।

---

# ⚠️ ছোট warning টাও fix করা যায়

তোমার log এ ছিল:

```text
the attribute `version` is obsolete
```

`docker-compose.yml` থেকে এটা delete করো:

```yaml
version: "3"
```

modern docker compose এ এটা দরকার নেই।

---

# 📊 Final Expected Result

run করলে দেখতে পাবে:

```text
backend-1   | Starting Django development server
frontend-1  | Compiled successfully
```

open করো:

```
http://localhost:3000
```




# 1️⃣ docker-compose.yml থেকে volume remove করো

আগে হয়তো এমন ছিল:

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    volumes:
      - ./backend:/app

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
```

---

# 2️⃣ volumes remove করার পর

এভাবে লিখো:

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
```

---

# 3️⃣ তারপর run করো

```bash
docker compose down
docker compose up --build
```

---

# 4️⃣ Expected result

terminal এ দেখাবে:

```
backend-1   | Starting development server at http://0.0.0.0:8000/
frontend-1  | Compiled successfully
```

open করো:

```
http://localhost:3000
```

---

# ⚠️ volume কেন ব্যবহার করা হয়

Normally developerরা এটা ব্যবহার করে:

```yaml
volumes:
  - ./backend:/app
```

কারণ:

* code change করলে container restart লাগেনা
* live reload হয়

কিন্তু `/media` drive এ Docker অনেক সময় **permission / mount problem** দেয়।

---

✅ **Best practice (future)**

project রাখো:

```
~/projects/fulstack
```

তখন volumes use করলে কোনো সমস্যা হবে না।

---


# 1️⃣ Browser এ ঠিক URL যাচ্ছি কি না

ডিফল্ট Vite log দেখাচ্ছিল:

```
Local:   http://localhost:5173/
Network: use --host to expose
```

**Docker container থেকে host access করতে** normal browser এ `http://localhost:5173` খুলতে হবে।

> যদি host machine থেকে access না হয়, কারণ Vite container ভিতরে bind হচ্ছে শুধু container network এ।

---

# 2️⃣ `.vite.config.js` update করা দরকার

frontend root এ `.vite.config.js` খোলো এবং server host expose করো:

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    host: true,      // expose to all network interfaces
    port: 5173,
  }
})
```

> `host: true` না দিলে container এর frontend **external network থেকে accessible হয় না**, শুধু container ভিতরে চলে।

---

# 3️⃣ Docker rebuild

```bash
docker compose down
docker compose build --no-cache
docker compose up
```

---

# 4️⃣ Ports mapping check

`docker-compose.yml` এ:

```yaml
services:
  frontend:
    build: ./frontend
    ports:
      - "5173:5173"   # host:container
```

> এটা নিশ্চিত করবে host machine browser থেকে access করা যাবে।

---

# 5️⃣ Browser test

- URL: `http://localhost:5173`
    
- যদি port busy হয় বা কিছু দেখায় না, try different host port:
    

```yaml
ports:
  - "3000:5173"
```

Browser open:

```
http://localhost:3000
```

---

## সবসময় **পুরো build করতে হবে না**, কিন্তু কিছুটা context-ভিত্তিক। বিস্তারিত:

---

# 1️⃣ **Back End (Django)**

* যদি **Python code, templates, static files, Django apps** পরিবর্তন করো, **container rebuild দরকার নেই**।
* কারণ Django server **StateReloader** use করে, যা automatically file changes detect করে reload করে।
* শর্ত: তোমার `docker-compose.yml` volume mount করা আছে, যেমন:

```yaml
volumes:
  - ./backend:/app
```

এতে host machine এর code live container এ reflect হয়।

> যদি তুমি volume remove করো (যেমন আগে `/media/...` problem এর কারণে), তাহলে **container rebuild ছাড়া code change reflect হবে না**।

---

# 2️⃣ **Front end (React/`Vite`)**

* React/`Vite` normally **live reload** support করে।
* Container এ `npm run dev` run হলে `Vite` development server automatically changes detect করে reload দেয়।
* শর্ত: volume mount করা আছে:

```yaml
volumes:
  - ./frontend:/app
```

> Volume না থাকলে, `frontend` code change করলে rebuild ছাড়া browser update হবে না।

---

# 3️⃣ **When to rebuild**

1. **Dependencies change**

   * Python: `requirements.txt` পরিবর্তন হলে

     ```bash
     docker compose build backend
     ```
   * Node: `package.json` / `package-lock.json` পরিবর্তন হলে

     ```bash
     docker compose build frontend
     ```

2. **Dockerfile পরিবর্তন**

   * Base image, env variables, port, CMD ইত্যাদি পরিবর্তন করলে

---

# 4️⃣ **Quick workflow**

Volume enabled থাকলে:

```text
Backend code → save → Django reload automatically
Frontend code → save → Vite reload automatically
Dependencies change → docker build
Dockerfile change → docker build
```

Volume না থাকলে:

```text
সব কিছু পরিবর্তন হলে rebuild + restart
```

---

💡 **Recommendation**:

* Development এর জন্য **volume enable রাখো** (host folder → container), তাহলে rebuild প্রয়োজন হবে না।
* Production এ rebuild হয় সবসময় (image package + copy static files)।

---

# Summary 

 **full Django + React (`Vite`) development Docker setup** বানিয়ে দিচ্ছি যেখানে:

* **`Backend` (Django)** live reload করবে
* **Frontend (React/Vite)** live reload করবে
* Rebuild লাগবে **শুধু dependencies বা Dockerfile change এ**

---

# 1️⃣ Project structure

```
fulstack/
│
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   └── manage.py
│   └── your apps...
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   └── vite.config.js
│   └── src/
│
└── docker-compose.yml
```

---

# 2️⃣ Backend Dockerfile (`backend/Dockerfile`)

```dockerfile
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
```

> Dev workflow এর জন্য volume use করলে code change auto reflect হবে।

---

# 3️⃣ Frontend Dockerfile (`frontend/Dockerfile`)

```dockerfile
FROM node:22

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm install

COPY . .

EXPOSE 5173

CMD ["npm", "run", "dev"]
```

---

# 4️⃣ Vite config (`frontend/vite.config.js`)

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    host: true,   // expose to all network interfaces
    port: 5173
  }
})
```

---

# 5️⃣ Docker Compose (`docker-compose.yml`)

```yaml
services:
  backend:
    build: ./backend
    volumes:
      - ./backend:/app        # live reload
    ports:
      - "8000:8000"
    depends_on:
      - db

  frontend:
    build: ./frontend
    volumes:
      - ./frontend:/app       # live reload
    ports:
      - "5173:5173"

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: fulstack
    ports:
      - "5432:5432"
```

> Backend volume: Django code auto reload
> Frontend volume: Vite dev server auto reload

---

# 6️⃣ Workflow

1. Build & run containers:

```bash
docker compose up --build
```

2. Backend live reload: `http://localhost:8000/`
3. Frontend live reload: `http://localhost:5173/`

> কোড change করলে **auto reflect হবে**, rebuild দরকার হবে **শুধু `requirements.txt` বা `package.json` change হলে**।

---

# 7️⃣ Optional tips

* Static files sync করতে: Django `collectstatic` দরকার production এ
* Frontend production build: `npm run build` → serve via Nginx
* Database: change করে environment variable দিয়ে connect করা

---
## Docker dev setup এ **production/robust database** হিসেবে সাধারণত **PostgreSQL** ব্যবহার করা হয়।

তুমি চাইলে Django backend কে Docker PostgreSQL এর সাথে connect করতে পারবে।

---

# 1️⃣ Docker Compose এ Postgres সার্ভিস add করো

`docker-compose.yml` এ ইতিমধ্যে যেমন দেখেছিলাম:

```yaml
db:
  image: postgres:15
  environment:
    POSTGRES_USER: postgres
    POSTGRES_PASSWORD: password
    POSTGRES_DB: fulstack
  ports:
    - "5432:5432"
```

> এটা তৈরি করবে container-ভিত্তিক Postgres database

---

# 2️⃣ Django DATABASES সেটিংস update করো

`backend/settings.py` এ:

```python
import os

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('POSTGRES_DB', 'fulstack'),
        'USER': os.environ.get('POSTGRES_USER', 'postgres'),
        'PASSWORD': os.environ.get('POSTGRES_PASSWORD', 'password'),
        'HOST': os.environ.get('POSTGRES_HOST', 'db'),  # container name
        'PORT': os.environ.get('POSTGRES_PORT', '5432'),
    }
}
```

> এখানে `HOST=db` because Docker Compose সার্ভিসের নাম `db`

> Postgres credentials `.env` file থেকে নেওয়া হলে আরও clean হয়

---

# 3️⃣ Install PostgreSQL Python dependency

`backend/requirements.txt` এ add করো:

```
psycopg2-binary
```

---

# 4️⃣ Rebuild & run backend

```bash
docker compose build backend
docker compose up
```

---

# 5️⃣ Django migrate করো

একটি terminal এ run করো:

```bash
docker compose exec backend python manage.py migrate
```

✅ এখন Django backend **PostgreSQL** connect করবে, SQLite আর দরকার নেই।

---

💡 **Tip:** dev এ SQLite ঠিক আছে, কিন্তু **Docker + multi-container setup** এ PostgreSQL use করা উচিত।

---
### **development এবং production উভয়ের জন্য** সরাসরি code-এ actual database credentials রাখা নিরাপদ নয় ⚠️।

এর জন্য **environment variables (env file)** use করা best practice।

---

# 1️⃣ Create `.env` file

`backend/.env`:

```env
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_HOST=db
POSTGRES_PORT=5432
DEBUG=True
SECRET_KEY=django-insecure-xyz123
```

> এখানে credentials safe রাখা যায়, Git এ commit করা যাবে না।

---

# 2️⃣ Update `docker-compose.yml` to load env

```yaml
backend:
  build: ./backend
  volumes:
    - ./backend:/app
  ports:
    - "8000:8000"
  env_file:
    - ./backend/.env
  depends_on:
    - db
```

> Docker automatically inject করবে container এ env variables।

---

# 3️⃣ Update `settings.py` to use env

```python
import os

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('POSTGRES_DB', 'fulstack'),
        'USER': os.environ.get('POSTGRES_USER', 'postgres'),
        'PASSWORD': os.environ.get('POSTGRES_PASSWORD', 'password'),
        'HOST': os.environ.get('POSTGRES_HOST', 'db'),
        'PORT': os.environ.get('POSTGRES_PORT', '5432'),
    }
}

SECRET_KEY = os.environ.get('SECRET_KEY', 'fallback-secret')
DEBUG = os.environ.get('DEBUG', 'True') == 'True'
```

---

# 4️⃣ Advantages of `.env`

1. Code-এ sensitive info রাখা হয় না
2. সহজে **different environments** (dev / staging / production) handle করা যায়
3. Docker / Kubernetes / CI/CD এ easy deploy

---

💡 **Tip:** `.env` ফাইল কখনো Git এ commit করো না। `.gitignore` এ add করো:

```
# .gitignore
backend/.env
```

---
#### env` (environment variables)** এবং **Docker Compose variables** মাঝে subtle difference আছে। আমি step-by-step explain করি।

---

# 1️⃣ `.env` (Environment File)

* `.env` হলো **plain text file** যা **environment variables** define করে।
* সাধারণত project root বা backend folder এ থাকে।
* Python/Django বা Node/Vite এই variables access করে, যেমন:

```env
# backend/.env
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
DEBUG=True
SECRET_KEY=django-secret-key
```

Python code এ access:

```python
import os

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('POSTGRES_DB'),
        'USER': os.environ.get('POSTGRES_USER'),
        'PASSWORD': os.environ.get('POSTGRES_PASSWORD'),
        'HOST': os.environ.get('POSTGRES_HOST', 'db'),
        'PORT': os.environ.get('POSTGRES_PORT', '5432'),
    }
}
```

**Key points:**

* Sensitive info safe রাখতে ব্যবহার হয়
* Different environment (dev/staging/prod) অনুযায়ী আলাদা `.env` বানানো যায়
* Git ignore করে commit না করা উচিত

---

# 2️⃣ Docker Compose variables (`docker-compose.yml`)

Docker Compose এ variable inject করার দুই main way আছে:

### a) Directly `environment` section এ define করা

```yaml
services:
  backend:
    environment:
      POSTGRES_DB: fulstack
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
```

* Container start হলে Python/Django এই variables access করতে পারে
* কিন্তু sensitive info Dockerfile / compose এ plain text থাকবে

---

### b) Using `env_file`

```yaml
services:
  backend:
    env_file:
      - ./backend/.env
```

* Docker automatically `.env` file load করে
* Python/Django same way `os.environ.get()` use করে access করবে
* Secure, maintainable এবং Git ignore possible

---

# 3️⃣ Difference Summary

| Feature          | `.env`                                 | Docker Compose environment                            |
| ---------------- | -------------------------------------- | ----------------------------------------------------- |
| Location         | Project folder, local file             | docker-compose.yml                                    |
| Purpose          | App reads environment variables        | Docker container reads environment variables          |
| Security         | Can be gitignored                      | Plain text in docker-compose.yml unless env_file used |
| Flexibility      | Can have multiple env files (dev/prod) | Usually tied to compose file                          |
| Access in Python | `os.environ.get()`                     | `os.environ.get()` (same)                             |

✅ Best practice (dev setup):

* **.env file** for sensitive info & app config
* **docker-compose.yml** uses `env_file: ./backend/.env`

> এটা করলে Django live reload + Docker container + PostgreSQL সব smooth কাজ করবে।

---

####  Python/Django project এ **`python-decouple`** use করতে চাইছো। এটা খুব ভালো practice, কারণ এটা `.env` file থেকে configuration load করতে সহজ করে এবং code-এ sensitive info রাখার দরকার হয় না।

---

# 1️⃣ Install `python-decouple`

```bash
pip install python-decouple
```

---

# 2️⃣ Create `.env` file (in backend folder)

`backend/.env`:

```env
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_HOST=db
POSTGRES_PORT=5432
DEBUG=True
SECRET_KEY=django-secret-key
```

> Gitignore এ add করো যাতে commit না হয়:

```text
# backend/.gitignore
.env
```

---

# 3️⃣ Update `settings.py` to use `decouple`

```python
from decouple import config

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('POSTGRES_DB', default='fulstack'),
        'USER': config('POSTGRES_USER', default='postgres'),
        'PASSWORD': config('POSTGRES_PASSWORD', default='password'),
        'HOST': config('POSTGRES_HOST', default='db'),
        'PORT': config('POSTGRES_PORT', default='5432'),
    }
}

SECRET_KEY = config('SECRET_KEY', default='fallback-secret')
DEBUG = config('DEBUG', default=True, cast=bool)
```

✅ Advantages of `decouple`:

1. `.env` file থেকে easily load করে
2. Type casting support করে (`cast=bool`, `cast=int`)
3. Sensitive info code-এ রাখার প্রয়োজন নেই
4. Dev + Prod আলাদা `.env` file use করা সহজ

---

# 4️⃣ Docker Compose setup

`docker-compose.yml`:

```yaml
services:
  backend:
    build: ./backend
    volumes:
      - ./backend:/app
    ports:
      - "8000:8000"
    env_file:
      - ./backend/.env
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: password
      POSTGRES_DB: fulstack
    ports:
      - "5432:5432"
```

> Backend container automatically `.env` থেকে env variables load করবে এবং `decouple` তাদের use করবে।

---

# 5️⃣ Notes

* Frontend `.env` আলাদা রাখা উচিত (Vite/React)
* Backend `.env` শুধু Django/DB config এর জন্য
* Docker dev setup এ **volume enabled থাকলে** code change auto reflect হবে

---

ঠিক আছে 😎, তুমি চাইছো **real production-ready fullstack setup** যেখানে:

* Django backend (Gunicorn)
* React frontend (built & served via Nginx)
* PostgreSQL database
* Redis (cache / Celery broker)
* Celery (async tasks)

### Complete summary: **Docker + Docker Compose** দিয়ে complete production setup তৈরি করে দিচ্ছি।

---

# 1️⃣ Project structure (production-ready)

```
fulstack/
│
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   └── your apps...
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── package-lock.json
│   ├── vite.config.js
│   └── src/
│
├── nginx/
│   └── default.conf
│
├── .env
└── docker-compose.yml
```

---

# 2️⃣ Backend Dockerfile (`backend/Dockerfile`)

```dockerfile id="l0b7v1"
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Gunicorn run
CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
```

> Dev জন্য `python manage.py runserver` use করতে পারো, production এ Gunicorn use হবে।

---

# 3️⃣ Frontend Dockerfile (`frontend/Dockerfile`)

```dockerfile id="4uef9y"
FROM node:22 AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build

# Nginx serve
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

# 4️⃣ Nginx config (`nginx/default.conf`)

```nginx id="q1u6ch"
server {
    listen 80;

    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://backend:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

> `/api/` route backend Django app এ forward করবে।

---

# 5️⃣ `.env` file

```
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_HOST=db
POSTGRES_PORT=5432
REDIS_HOST=redis
REDIS_PORT=6379
SECRET_KEY=django-secret-key
DEBUG=False
```

---

# 6️⃣ Docker Compose (`docker-compose.yml`)

```yaml id="m3zj8h"
version: "3.9"

services:
  backend:
    build: ./backend
    env_file:
      - ./.env
    depends_on:
      - db
      - redis
    ports:
      - "8000:8000"

  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

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

volumes:
  pgdata:
```

---

# 7️⃣ Django settings for Redis + Celery

`backend/settings.py`:

```python id="zzk0f3"
import os
from decouple import config

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('POSTGRES_DB'),
        'USER': config('POSTGRES_USER'),
        'PASSWORD': config('POSTGRES_PASSWORD'),
        'HOST': config('POSTGRES_HOST'),
        'PORT': config('POSTGRES_PORT'),
    }
}

# Redis (for caching / Celery broker)
CELERY_BROKER_URL = f"redis://{config('REDIS_HOST')}:{config('REDIS_PORT')}/0"
CELERY_RESULT_BACKEND = f"redis://{config('REDIS_HOST')}:{config('REDIS_PORT')}/0"

# Debug & Secret
SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', cast=bool, default=False)
```

`backend/celery.py`:

```python id="iq2b3n"
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')
app = Celery('backend')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

---

# 8️⃣ Workflow

```bash id="kl9xv4"
# Build & start everything
docker compose up --build -d

# Django migrate
docker compose exec backend python manage.py migrate

# Celery worker logs
docker compose logs -f celery
```

* Frontend: `http://localhost/` (served by Nginx)
* Backend: `http://localhost/api/` (proxied by Nginx)
* Redis + Celery: background async tasks

---

💡 **Notes:**

1. Development এ live reload করতে:

   * Backend: volume mount + `runserver`
   * Frontend: volume mount + Vite dev server
2. Production: Gunicorn + Nginx + Celery + Redis

---

###  full **production stack**—Gunicorn + Nginx + PostgreSQL + Redis + Celery—একসাথে handle করতে চাও। আমি step-by-step guide দিচ্ছি, যেটা অনুসরণ করলে তুমি একে একে সব component চালাতে পারবে।

---

# 1️⃣ Step 0: প্রাথমিক ধাপ

প্রথমে project folder তৈরি করো:

```
fulstack/
├── backend/
├── frontend/
├── nginx/
├── .env
└── docker-compose.yml
```

* Backend = Django project
* Frontend = React project
* Nginx = React serve + reverse proxy for Django API

---

# 2️⃣ `.env` তৈরি করো (backend/.env)

```env
POSTGRES_DB=fulstack
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
POSTGRES_HOST=db
POSTGRES_PORT=5432

REDIS_HOST=redis
REDIS_PORT=6379

SECRET_KEY=django-secret-key
DEBUG=False
```

* Later তুমি `.gitignore` এ add করবে
* Backend ও Docker Compose এই file থেকে variables load করবে

---

# 3️⃣ Docker Compose তৈরি করা (docker-compose.yml)

```yaml
version: "3.9"
services:
  backend:
    build: ./backend
    env_file:
      - ./backend/.env
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis

  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data

  redis:
    image: redis:7
    ports:
      - "6379:6379"

  celery:
    build: ./backend
    command: celery -A config worker --loglevel=info
    env_file:
      - ./backend/.env
    depends_on:
      - redis
      - backend

volumes:
  pgdata:
```

✅ এটি প্রথম build/run করার জন্য core services সব ready।

---

# 4️⃣ Backend Dockerfile (backend/Dockerfile)

```dockerfile
FROM python:3.12-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

CMD ["gunicorn", "config.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
```

> Dev এর জন্য তুমি `python manage.py runserver 0.0.0.0:8000` use করতে পারো।

---

# 5️⃣ Frontend Dockerfile (frontend/Dockerfile)

```dockerfile
FROM node:22 AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

# 6️⃣ Nginx config (nginx/default.conf)

```nginx
server {
    listen 80;

    location / {
        root /usr/share/nginx/html;
        index index.html;
        try_files $uri /index.html;
    }

    location /api/ {
        proxy_pass http://backend:8000/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

> `/api/` route সব Django API কে forward করবে।

---

# 7️⃣ Django settings for PostgreSQL + Redis + Celery

`backend/settings.py`:

```python
from decouple import config

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('POSTGRES_DB'),
        'USER': config('POSTGRES_USER'),
        'PASSWORD': config('POSTGRES_PASSWORD'),
        'HOST': config('POSTGRES_HOST'),
        'PORT': config('POSTGRES_PORT'),
    }
}

# Celery
CELERY_BROKER_URL = f"redis://{config('REDIS_HOST')}:{config('REDIS_PORT')}/0"
CELERY_RESULT_BACKEND = CELERY_BROKER_URL

SECRET_KEY = config('SECRET_KEY')
DEBUG = config('DEBUG', cast=bool, default=False)
```

`backend/celery.py`:

```python
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')
app = Celery('backend')
app.config_from_object('django.conf:settings', namespace='CELERY')
app.autodiscover_tasks()
```

---

# 8️⃣ Start services step-by-step

1️⃣ Build everything:

```bash
docker compose up --build -d
```

2️⃣ Django migrate:

```bash
docker compose exec backend python manage.py migrate
```

3️⃣ Check backend:

```bash
docker compose logs -f backend
```

4️⃣ Check Celery:

```bash
docker compose logs -f celery
```

5️⃣ Frontend browser এ:

```
http://localhost/
```

* React app Nginx থেকে serve হবে
* `/api/` সব Django API কে Nginx proxy করবে

---

# 9️⃣ Dev workflow (optional)

* Dev mode এ frontend live reload: Vite dev server + volume mount
* Backend live reload: `python manage.py runserver` + volume mount
* Production: Gunicorn + Nginx + Celery + Redis + Postgres

---

💡 **Tip:**

* প্রথমে শুধু backend + db + redis চালিয়ে practice করো
* তারপর frontend + nginx যোগ করো
* এরপর Celery + async tasks add করো

---

