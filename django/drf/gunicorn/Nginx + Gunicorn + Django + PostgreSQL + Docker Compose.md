# Class 4: Django REST Framework Production Deployment

Nginx + Gunicorn + Django + PostgreSQL + Docker Compose + Ubuntu VPS + HTTPS

এই ক্লাসে আমাদের আগের Product API-কে internet-এ deploy করার সম্পূর্ণ workflow শিখব। লক্ষ্য হলো, কেউ তোমার domain-এ request পাঠালে Nginx সেটি Gunicorn-এর মাধ্যমে Django-তে পাঠাবে, আর Django PostgreSQL থেকে data নিয়ে response দেবে।

আমরা আগের project-এর `config/`, `products/`, `Dockerfile`, `requirements.txt` এবং PostgreSQL model ব্যবহার করব। নতুন করে Django project তৈরি করতে হবে না।

## ১. Production architecture

Client / React / Next.js

HTTPS request → api.example.com

Domain DNS + VPS Firewall

TCP 443 / HTTPS · TCP 80 / certificate issuance & redirect

Nginx Container

TLS certificate · Reverse proxy · Static files

Gunicorn → Django REST Framework

Application logic · Authentication · ORM

PostgreSQL

Database · Persistent volume · Backups

মূল ধারণা: Internet থেকে শুধু Nginx-এর public port-এ request আসবে। Gunicorn ও PostgreSQL-এর port সরাসরি public internet-এ expose করব না।

## ২. Deploy করার আগে কী লাগবে?

তোমার প্রয়োজন হবে:

* Ubuntu VPS, যেখানে Docker Engine ও Docker Compose plugin থাকবে।

* একটি domain অথবা subdomain, যেমন `api.example.com`।

* VPS-এর public IPv4 address; IPv6 ব্যবহার করলে সেটির DNS ও firewall-ও ঠিকভাবে configure করতে হবে।

* VPS-এ SSH access ও `sudo` permission।

* Project-এর Docker image build করার ব্যবস্থা অথবা VPS-এ source code থেকে image build করার ব্যবস্থা।

নিচের উদাহরণে `api.example.com` এবং `203.0.113.10` placeholder হিসেবে ব্যবহার করছি। এগুলো তোমার আসল domain ও VPS IP দিয়ে পরিবর্তন করবে। `203.0.113.10` documentation-এর example IP, বাস্তব VPS address নয়।

## ৩. Domain DNS configure করো

তোমার domain provider-এর DNS management page-এ গিয়ে একটি `A` record তৈরি করো।

| Type | Name  | Value                            |
| ---- | ----- | -------------------------------- |
| A    | `api` | তোমার VPS-এর public IPv4 address |

তাহলে `api.example.com` তোমার VPS-এ point করবে। DNS propagation-এর সময় provider অনুযায়ী পরিবর্তিত হতে পারে।

VPS-এ SSH করে DNS পরীক্ষা করো:

Bash

```
getent ahostsv4 api.example.com
```

Returned address তোমার VPS-এর public IP-এর সঙ্গে মিলছে কি না নিশ্চিত করো।

## ৪. Ubuntu VPS firewall configure করো

VPS provider-এর cloud firewall/security group এবং Ubuntu-এর firewall—দুটিই যাচাই করো। প্রথমে provider panel-এ SSH, HTTP ও HTTPS access অনুমোদিত আছে কি না দেখো।

Ubuntu-তে UFW ব্যবহার করলে:

Bash

```
sudo ufw status
```

SSH-এর জন্য সঠিক port অনুমোদন না করে firewall enable করবে না। SSH port যদি default `22` হয়:

Bash

```
sudo ufw allow OpenSSH
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status
```

তোমার SSH port আলাদা হলে `OpenSSH` profile-এর পরিবর্তে সেই port-এর নিয়ম ব্যবহার করবে।

Security rule: PostgreSQL `5432` এবং Gunicorn `8000`-এর জন্য public inbound firewall rule তৈরি করবে না।

Docker-এর published ports কিছু setup-এ UFW-এর প্রত্যাশিত filtering এড়িয়ে যেতে পারে। তাই cloud firewall-এও শুধু প্রয়োজনীয় inbound ports খোলা রাখো এবং নিচের Compose configuration-এ backend/database-এর public port publish করব না।

## ৫. VPS-এ project directory তৈরি করো

SSH দিয়ে VPS-এ প্রবেশ করো:

Bash

```
ssh YOUR_USER@YOUR_VPS_IP
```

তারপর:

Bash

```
sudo mkdir -p /opt/django-api/nginx
sudo chown -R "$USER":"$USER" /opt/django-api
cd /opt/django-api
```

তোমার Django project files এখানে রাখো—Git repository থেকে clone করতে পারো অথবা নিরাপদভাবে deploy করতে পারো।

এই উদাহরণে folder structure হবে:

```
/opt/django-api/
├── config/
├── products/
├── nginx/
│   └── default.conf
├── .env
├── .dockerignore
├── Dockerfile
├── entrypoint.sh
├── compose.yaml
├── manage.py
└── requirements.txt
```

আগের ক্লাসের `Dockerfile`, `entrypoint.sh`, Django settings ও Product API এখানে ব্যবহার করবে। পরের ধাপের configuration-গুলো এই structure অনুযায়ী।

## ৬. Production `.env` তৈরি করো

`/opt/django-api/.env`:

dotenv

```
POSTGRES_DB=shopdb
POSTGRES_USER=shopuser
POSTGRES_PASSWORD=REPLACE_WITH_STRONG_RANDOM_PASSWORD

DJANGO_SECRET_KEY=REPLACE_WITH_GENERATED_SECRET
DJANGO_DEBUG=False
DJANGO_ALLOWED_HOSTS=api.example.com
DJANGO_CSRF_TRUSTED_ORIGINS=https://api.example.com

GUNICORN_WORKERS=2
GUNICORN_TIMEOUT=60
```

Secret generate করার জন্য নিজের trusted machine বা VPS-এ:

Bash

```
python3 -c 'import secrets; print(secrets.token_urlsafe(50))'
```

Output-টি `DJANGO_SECRET_KEY`-এর জায়গায় বসাও। Database password ও Django secret আলাদা হবে।

Permissions সীমিত করো:

Bash

```
chmod 600 .env
```

এবং নিশ্চিত করো `.env` Git-এ commit হয়নি।

## ৭. Django production settings যাচাই করো

`config/settings.py`-তে production-এর জন্য নিচের settings যোগ করো। একই setting আগে থাকলে duplicate না করে update করবে।

Python

Run

```
DEBUG = os.getenv("DJANGO_DEBUG", "False").lower() == "true"

ALLOWED_HOSTS = [
    host.strip()
    for host in os.getenv("DJANGO_ALLOWED_HOSTS", "").split(",")
    if host.strip()
]

CSRF_TRUSTED_ORIGINS = [
    origin.strip()
    for origin in os.getenv("DJANGO_CSRF_TRUSTED_ORIGINS", "").split(",")
    if origin.strip()
]

SECURE_PROXY_SSL_HEADER = ("HTTP_X_FORWARDED_PROTO", "https")
```

HTTPS চালু হওয়ার পরে এবং Nginx-এ proxy headers ঠিকভাবে configure করার পর যোগ করতে পারো:

Python

Run

```
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

`SECURE_PROXY_SSL_HEADER` শুধু তখনই নিরাপদ যখন application-এর কাছে request পাঠানো trusted proxy-ই `X-Forwarded-Proto` header সেট করে। Nginx-এর configuration-এ আমরা সেই header নিজেরাই সেট করব।

এখন static files-এর জন্য WhiteNoise ব্যবহার করা থাকলে `STATIC_ROOT`, `STATIC_URL` ও WhiteNoise middleware আগের ক্লাসের মতোই রাখবে। Django admin ও browsable API-এর static files-এর জন্য `collectstatic` প্রয়োজন।

## ৮. Production Docker Compose তৈরি করো

`compose.yaml`:

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
    networks:
      - backend_net

  backend:
    build: .
    restart: unless-stopped
    env_file:
      - .env
    environment:
      DB_ENGINE: postgresql
      DB_HOST: db
      DB_PORT: "5432"
    expose:
      - "8000"
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
    networks:
      - backend_net
      - proxy_net

  nginx:
    image: nginx:1.28-alpine
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - letsencrypt_data:/etc/letsencrypt:ro
      - certbot_webroot:/var/www/certbot:ro
    depends_on:
      backend:
        condition: service_healthy
    networks:
      - proxy_net

volumes:
  postgres_data:
  letsencrypt_data:
  certbot_webroot:

networks:
  backend_net:
    internal: true
  proxy_net:
```

এই configuration-এ:

* PostgreSQL-এর port host-এ publish করা হয়নি।

* Gunicorn-এর port host-এ publish করা হয়নি।

* Nginx শুধু public port `80` ও `443` publish করছে।

* `postgres_data` database data persist করে।

* `letsencrypt_data` TLS certificate সংরক্ষণ করে।

* `certbot_webroot` HTTP certificate challenge file-এর জন্য ব্যবহৃত হবে।

`nginx` image version-টি উদাহরণ হিসেবে pin করা হয়েছে। Production-এ deploy করার আগে official image-এর বর্তমান supported version ও security updates যাচাই করবে।

## ৯. Nginx-এর প্রথম configuration: certificate পাওয়ার আগে

প্রথমে শুধু HTTP চালাব, যাতে Let's Encrypt certificate validation করতে পারে।

`nginx/default.conf`:

Nginx

```
server {
    listen 80;
    server_name api.example.com;

    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }

    location / {
        return 200 "HTTP bootstrap is working\n";
        add_header Content-Type text/plain;
    }
}
```

`api.example.com`-এর জায়গায় তোমার domain বসাবে।

এই প্রথম configuration ইচ্ছাকৃতভাবে API-কে proxy করছে না। প্রথমে certificate সংগ্রহ করব, তারপর HTTPS configuration বসাব।

## ১০. Compose দিয়ে database ও Nginx চালাও

VPS-এ project directory থেকে:

Bash

```
docker compose config
```

এটি Compose configuration যাচাই করবে। `.env`-এ placeholder value রয়ে গেছে কি না নিজে পরীক্ষা করবে—এই command সব ভুল ধরতে পারবে না।

Image build করো:

Bash

```
docker compose build
```

Database চালু করো:

Bash

```
docker compose up -d db
docker compose ps
```

PostgreSQL healthy না হওয়া পর্যন্ত অপেক্ষা করো। তারপর certificate bootstrap-এর জন্য Nginx চালু করো:

Bash

```
docker compose up -d nginx
```

Browser-এ খোলো:

`http://api.example.com`

যদি `HTTP bootstrap is working` দেখো, তাহলে DNS, port `80` এবং Nginx-এর প্রাথমিক configuration কাজ করছে।

যদি কাজ না করে, DNS address, VPS provider firewall, UFW, এবং Nginx logs পরীক্ষা করো:

Bash

```
docker compose logs nginx
```

## ১১. Let's Encrypt certificate সংগ্রহ করো

Let's Encrypt free TLS certificate দেয়। আমরা Certbot ব্যবহার করব।

`compose.yaml`-এর `services:` section-এ নিচের service যোগ করো:

YAML

```
  certbot:
    image: certbot/certbot
    profiles:
      - tools
    volumes:
      - letsencrypt_data:/etc/letsencrypt
      - certbot_webroot:/var/www/certbot
```

এটি সাধারণ application service নয়; আমরা যখন certificate issue বা renew করতে চাই, তখন চালাব।

এবার certificate সংগ্রহ করো:

Bash

```
docker compose run --rm certbot certonly \
  --webroot \
  -w /var/www/certbot \
  -d api.example.com \
  --email YOUR_EMAIL \
  --agree-tos \
  --no-eff-email
```

`api.example.com` ও `YOUR_EMAIL` তোমার তথ্য দিয়ে পরিবর্তন করবে।

এই command সফল হওয়ার জন্য:

* Domain-এর DNS সঠিক VPS-এ point করতে হবে।

* Public port `80`-এ Nginx পৌঁছানো সম্ভব হতে হবে।

* Nginx-এর ACME challenge directory ঠিকভাবে serve করতে হবে।

Certificate তৈরি হলে সাধারণত নিচের file পাওয়া যাবে:

```
/etc/letsencrypt/live/api.example.com/fullchain.pem
/etc/letsencrypt/live/api.example.com/privkey.pem
```

এগুলো Docker volume-এর মধ্যে থাকবে। Private key কখনো public repository-তে commit করবে না।

## ১২. Nginx-এর HTTPS reverse proxy configuration

এখন `nginx/default.conf`-এর আগের bootstrap configuration সরিয়ে নিচের configuration বসাও:

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

    ssl_protocols TLSv1.2 TLSv1.3;

    client_max_body_size 20m;

    location / {
        proxy_pass http://backend:8000;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        proxy_connect_timeout 5s;
        proxy_read_timeout 60s;
    }
}
```

এখানে `proxy_pass http://backend:8000`-এ `backend` হলো Docker Compose service name। Nginx ও backend একই `proxy_net`-এ থাকায় service name দিয়ে একে অপরকে খুঁজে পাবে।

এখন Nginx configuration reload করার আগে test করো:

Bash

```
docker compose exec nginx nginx -t
```

যদি test সফল হয়:

Bash

```
docker compose up -d nginx
```

Nginx certificate file read করতে না পারলে service চালু হবে না। সে ক্ষেত্রে certificate issuance সফল হয়েছে কি না এবং path ঠিক আছে কি না যাচাই করো।

## ১৩. Deployment-এর সময় database migrations

এটি production deployment-এর সবচেয়ে গুরুত্বপূর্ণ ধাপগুলোর একটি।

আগের `entrypoint.sh`-এ নিশ্চিত করো, সেটি custom command গ্রহণ করতে পারে। ফাইলটি এভাবে রাখো:

Bash

```
#!/bin/sh
set -eu

if [ "${RUN_COLLECTSTATIC:-true}" = "true" ]; then
    python manage.py collectstatic --noinput
fi

exec "$@"
```

এবং Dockerfile-এ নিশ্চিত করো:

dockerfile

```
ENTRYPOINT ["/app/entrypoint.sh"]

CMD ["gunicorn", "config.wsgi:application", \
     "--bind", "0.0.0.0:8000", \
     "--workers", "2", \
     "--timeout", "60", \
     "--access-logfile", "-", \
     "--error-logfile", "-"]
```

এতে normal startup-এ static files collect করে Gunicorn চালু হবে। আর migration command দিলে Gunicorn-এর পরিবর্তে migration চলবে।

### প্রথম deployment

প্রথমে image build করো:

Bash

```
docker compose build
```

Database চালু করো:

Bash

```
docker compose up -d db
```

তারপর migration চালাও:

Bash

```
docker compose run --rm \
  -e RUN_COLLECTSTATIC=false \
  backend python manage.py migrate --noinput
```

এবার application চালু করো:

Bash

```
docker compose up -d
```

যেহেতু Nginx-এর `depends_on` backend health check-এর ওপর নির্ভর করে, backend healthy না হওয়া পর্যন্ত Nginx চালু হওয়ার জন্য অপেক্ষা করবে।

### পরবর্তী deployment-এ কী করবে?

যখন code পরিবর্তন করে নতুন image build করবে, তখন deployment sequence হবে:

1. নতুন image build বা pull করা।

2. Database backup নেওয়া, বিশেষত schema পরিবর্তন হলে।

3. নতুন image দিয়ে migration চালানো।

4. Application service update করা।

5. Health check ও API test করা।

উদাহরণ:

Bash

```
docker compose build backend

docker compose run --rm \
  -e RUN_COLLECTSTATIC=false \
  backend python manage.py migrate --noinput

docker compose up -d --no-deps backend
```

এখানে গুরুত্বপূর্ণ সীমাবদ্ধতা আছে: `docker compose up -d --no-deps backend` পুরোনো container-কে নতুন container দিয়ে replace করতে পারে, তাই সামান্য downtime হতে পারে। Migration ব্যর্থ হলে নতুন application চালু করা উচিত নয়। Database migration নিজে থেকে rollback হবে—এমন ধরে নেওয়াও ঠিক নয়।

Production migration-এর নিয়ম: আগে backup, তারপর backward-compatible migration, তারপর application deployment। পুরোনো ও নতুন application version-এর মধ্যে schema compatibility না থাকলে deployment strategy আলাদা করে পরিকল্পনা করতে হবে।

## ১৪. HTTPS ও API পরীক্ষা করো

VPS-এ:

Bash

```
docker compose ps
docker compose logs --tail=100 backend
docker compose logs --tail=100 nginx
```

Django health check:

Bash

```
curl -i https://api.example.com/api/health/
```

Product API:

Bash

```
curl -i https://api.example.com/api/products/
```

TLS certificate যাচাই:

Bash

```
curl -Iv https://api.example.com/
```

Django deployment checks চালাও:

Bash

```
docker compose exec backend \
  python manage.py check --deploy
```

এই command production configuration-এর সম্ভাব্য security issue দেখাতে পারে। Warning-গুলো বুঝে সমাধান করবে; সব warning উপেক্ষা করে deployment শেষ করবে না।

## ১৫. Certificate auto-renewal configure করো

Let's Encrypt certificate-এর মেয়াদ শেষ হওয়ার আগে renew করতে হবে। Certbot-এর `renew` command দিয়ে এটি করা যায়।

পরীক্ষা করো:

Bash

```
docker compose run --rm certbot renew --dry-run
```

এটি সফল হলে VPS-এ root cron job বা systemd timer দিয়ে নিয়মিত renewal schedule করো। উদাহরণ হিসেবে `/etc/cron.d/django-api-cert-renew`:

cron

```
0 3,15 * * * root cd /opt/django-api && docker compose run --rm certbot renew --webroot -w /var/www/certbot --quiet && docker compose exec -T nginx nginx -s reload
```

এটি প্রতিদিন দুইবার renewal পরীক্ষা করবে এবং command সফল হলে Nginx reload করবে। নিশ্চিত করো cron-এর `docker compose` command সঠিকভাবে কাজ করে, project-এর `.env` পাওয়া যায় এবং Nginx চলমান আছে।

## ১৬. PostgreSQL backup রাখো

Production database-এর backup নিয়মিত নেওয়া উচিত। উদাহরণস্বরূপ, manual logical backup:

Bash

```
cd /opt/django-api

docker compose exec -T db sh -c \
  'pg_dump -U "$POSTGRES_USER" "$POSTGRES_DB"' \
  > backup.sql
```

এই command-এর জন্য PostgreSQL container-এর environment-এ `POSTGRES_USER` ও `POSTGRES_DB` থাকতে হবে, যা আমাদের Compose configuration-এ আছে।

Backup-এ sensitive data থাকতে পারে। এটি নিরাপদ, সীমিত-permission-এর storage-এ রাখবে এবং VPS-এর বাইরে encrypted backup রাখার ব্যবস্থাও করবে। শুধু backup তৈরি করাই যথেষ্ট নয়—restore করে নিয়মিত পরীক্ষা করতে হবে।

## ১৭. Deployment troubleshooting

502 Bad Gateway

Bash

```
docker compose logs nginx backend
docker compose ps
```

Backend healthy কি না, Nginx `backend:8000`-এ পৌঁছাতে পারছে কি না এবং application চালু আছে কি না দেখো।

Database connection error

Bash

```
docker compose logs db
docker compose exec backend python manage.py migrate --check
```

Database health, `DB_HOST=db`, database credentials ও migrations যাচাই করো।

HTTPS certificate error

Bash

```
docker compose run --rm certbot certificates
docker compose exec nginx nginx -t
```

Domain name, certificate path, certificate expiry এবং port `80/443` পরীক্ষা করো।

Static files load হচ্ছে না

Bash

```
docker compose exec backend python manage.py collectstatic --noinput
```

WhiteNoise middleware, `STATIC_ROOT`, `STATIC_URL` ও browser-এর Network tab পরীক্ষা করো।

## ১৮. Final production checklist

Deployment readiness

0/10

DNS সঠিক VPS IP-তে point করছে

Firewall-এ প্রয়োজনীয় SSH, HTTP ও HTTPS port খোলা

PostgreSQL ও Gunicorn public port হিসেবে প্রকাশ করা হয়নি

Production secrets .env-এ এবং file permission সীমিত

DEBUG=False ও ALLOWED_HOSTS ঠিক

Nginx reverse proxy ও HTTPS কাজ করছে

Certificate renewal পরীক্ষা করা হয়েছে

Database migrations সফল

Health check ও API request সফল

Database backup এবং restore পরীক্ষা করা হয়েছে

### এই ক্লাসের মূল শিক্ষা

তোমার production request flow এখন:

`Domain → HTTPS → Nginx → Gunicorn → Django REST Framework → PostgreSQL`

* Nginx public traffic ও TLS পরিচালনা করে।

* Gunicorn Django application চালায়।

* Docker Compose service ও network পরিচালনা করে।

* PostgreSQL persistent data রাখে।

* Deployment-এর সময় migration database schema update করে।

* Health checks, logs ও backup production troubleshooting-এ সাহায্য করে।

এর পরের যৌক্তিক ধাপ: GitHub Actions দিয়ে automated tests, Docker image build ও VPS deployment তৈরি করা; deployment ব্যর্থ হলে health check, rollback strategy এবং database migration compatibility যাচাই করা।


---
