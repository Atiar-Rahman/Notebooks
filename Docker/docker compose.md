নিচে **Docker Compose Complete Tutorial (Beginner → Advanced)** ধাপে ধাপে দিলাম। এটা শিখলে তুমি **multi-container application production-এ run করতে পারবে**। 🚀

---

# 🐳 Docker Compose Complete Tutorial

Docker Compose হলো এমন একটি tool যা **একাধিক Docker container একসাথে manage করার জন্য** ব্যবহার করা হয়।

Example:

- Web app
    
- Database
    
- Cache
    

সবগুলো এক ফাইলে define করা যায়।

---

# 1️⃣ Docker Compose install check

```bash
docker compose version
```

Output example:

```
Docker Compose version v2.20.0
```

---

# 2️⃣ Basic Project Structure

Example project:

```
project/
 ├── docker-compose.yml
 ├── app/
 │    └── index.js
 └── package.json
```

---

# 3️⃣ First Docker Compose Example

### docker-compose.yml

```yaml
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "80:80"
```

Run:

```bash
docker compose up
```

Background run:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

---

# 4️⃣ Multiple Container Example

Example: **NodeJS + MySQL**

```yaml
version: "3.8"

services:

  app:
    image: node:18
    container_name: node_app
    ports:
      - "3000:3000"
    volumes:
      - .:/app
    working_dir: /app
    command: npm start
    depends_on:
      - db

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
```

---

# 5️⃣ Volumes (Data persist)

Database data save করার জন্য।

```yaml
services:
  db:
    image: mysql:8
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

এতে container delete হলেও data থাকবে।

---

# 6️⃣ Environment Variables

```yaml
services:
  app:
    environment:
      DB_HOST: db
      DB_USER: root
      DB_PASS: root
```

---

# 7️⃣ Custom Network

Docker Compose automatically network create করে।

Example:

```yaml
networks:
  mynetwork:
```

Use:

```yaml
services:
  app:
    networks:
      - mynetwork
```

---

# 8️⃣ Build from Dockerfile

যদি নিজের image build করতে চাও।

```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
```

Dockerfile example:

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm","start"]
```

---

# 9️⃣ Restart Policy (Production)

Production এ always use করা হয়।

```yaml
restart: always
```

Example:

```yaml
services:
  nginx:
    image: nginx
    restart: always
```

---

# 🔟 Logs

সব service logs:

```bash
docker compose logs
```

Live logs:

```bash
docker compose logs -f
```

Specific service:

```bash
docker compose logs app
```

---

# 1️⃣1️⃣ Scale Containers

Example:

```bash
docker compose up --scale app=3
```

এতে 3টা container run করবে।

---

# 1️⃣2️⃣ Production Best Practice

Production compose file এ সাধারণত থাকে:

- restart policy
    
- volumes
    
- environment variables
    
- custom network
    
- nginx reverse proxy
    

Example structure:

```
docker-compose.yml
.env
nginx/
Dockerfile
```

---

# 🧠 Real Production Example

**NodeJS + MySQL + Nginx**

```yaml
version: "3.8"

services:

  app:
    build: .
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: mysql:8
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
    volumes:
      - dbdata:/var/lib/mysql

  nginx:
    image: nginx
    restart: always
    ports:
      - "80:80"
    depends_on:
      - app

volumes:
  dbdata:
```

Run:

```bash
docker compose up -d
```

---

# ⚡ Docker Compose Most Important Commands

```bash
docker compose up
docker compose up -d
docker compose down
docker compose ps
docker compose logs
docker compose restart
docker compose build
```

---

নিচে **১০টা real production Docker Compose example** দিলাম। এগুলো বাস্তবে অনেক project-এ ব্যবহার করা হয়। প্রতিটা example simplified করা হয়েছে যাতে সহজে বুঝতে পারো। 🚀

---

# 1️⃣ Nginx + Node.js + MySQL

```yaml
version: "3.8"

services:
  app:
    build: .
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: mysql:8
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
    volumes:
      - dbdata:/var/lib/mysql

  nginx:
    image: nginx
    restart: always
    ports:
      - "80:80"
    depends_on:
      - app

volumes:
  dbdata:
```

---

# 2️⃣ Node.js + Redis (cache)

```yaml
version: "3.8"

services:

  app:
    image: node:18
    restart: always
    ports:
      - "3000:3000"
    depends_on:
      - redis

  redis:
    image: redis:7
    restart: always
```

---

# 3️⃣ Python + PostgreSQL

```yaml
version: "3.8"

services:

  web:
    build: .
    restart: always
    ports:
      - "8000:8000"
    depends_on:
      - db

  db:
    image: postgres:15
    restart: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: appdb
```

---

# 4️⃣ Laravel + MySQL + Nginx

```yaml
version: "3.8"

services:

  app:
    image: php:8.2-fpm
    volumes:
      - .:/var/www

  webserver:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - .:/var/www
    depends_on:
      - app

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
```

---

# 5️⃣ WordPress + MySQL

```yaml
version: "3.8"

services:

  wordpress:
    image: wordpress
    ports:
      - "8080:80"
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
```

---

# 6️⃣ MongoDB + Express App

```yaml
version: "3.8"

services:

  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo
    volumes:
      - mongodata:/data/db

volumes:
  mongodata:
```

---

# 7️⃣ React + Nginx

```yaml
version: "3.8"

services:

  frontend:
    build: .
    ports:
      - "80:80"
    restart: always
```

React build হয়ে nginx serve করে।

---

# 8️⃣ ELK Stack (Logging)

Uses:

- Elasticsearch
    
- Logstash
    
- Kibana
    

```yaml
version: "3.8"

services:

  elasticsearch:
    image: elasticsearch:8.0.0
    environment:
      discovery.type: single-node
    ports:
      - "9200:9200"

  kibana:
    image: kibana:8.0.0
    ports:
      - "5601:5601"
    depends_on:
      - elasticsearch
```

---

# 9️⃣ Jenkins CI/CD

```yaml
version: "3.8"

services:

  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - "8080:8080"
    volumes:
      - jenkins_home:/var/jenkins_home

volumes:
  jenkins_home:
```

---

# 🔟 Monitoring Stack (Prometheus + Grafana)

```yaml
version: "3.8"

services:

  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
```

---

# ⚡ Production Best Practices

Production docker-compose এ সাধারণত থাকে:

✔ restart policy  
✔ volumes  
✔ environment variables  
✔ custom network  
✔ secrets / env file

Example:

```yaml
restart: always
env_file:
  - .env
```

---

নিচে একটি **Real Production Docker Project Structure** দেখাচ্ছি। এই ধরনের structure সাধারণত production backend / DevOps project-এ ব্যবহার করা হয়। 🚀

---

# 📁 Real Production Docker Project Structure

```id="ksx6rf"
project/

├── docker-compose.yml
├── docker-compose.prod.yml
├── .env

├── app/
│   ├── Dockerfile
│   ├── package.json
│   ├── src/
│   │   └── index.js

├── nginx/
│   ├── Dockerfile
│   └── nginx.conf

├── database/
│   └── init.sql

├── logs/

└── scripts/
    ├── backup.sh
    └── deploy.sh
```

---

# 📦 Folder Explanation

### 1️⃣ docker-compose.yml

Development environment run করার জন্য।

Example:

```yaml
version: "3.8"

services:

  app:
    build: ./app
    ports:
      - "3000:3000"
    env_file:
      - .env

  db:
    image: mysql:8
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

---

### 2️⃣ docker-compose.prod.yml

Production configuration।

```yaml
services:

  app:
    restart: always
    environment:
      NODE_ENV: production

  nginx:
    image: nginx
    ports:
      - "80:80"
    depends_on:
      - app
```

Run production:

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

---

### 3️⃣ `.env` file

Environment variables store করা হয়।

```id="1xx8qo"
DB_HOST=db
DB_USER=root
DB_PASS=root
PORT=3000
```

---

### 4️⃣ App Dockerfile

```dockerfile
FROM node:18

WORKDIR /app
COPY . .

RUN npm install

CMD ["npm","start"]
```

---

### 5️⃣ Nginx Reverse Proxy

nginx.conf

```id="d1itq3"
server {
    listen 80;

    location / {
        proxy_pass http://app:3000;
    }
}
```

---

### 6️⃣ Database Initialization

```sql
CREATE DATABASE appdb;
```

Container start হলে automatically run করা যায়।

---

### 7️⃣ Logs folder

Production logs store করার জন্য।

```id="dcs2hd"
logs/
```

---

### 8️⃣ Scripts folder

Automation scripts।

Example:

deploy.sh

```bash
#!/bin/bash
docker compose pull
docker compose up -d
```

---

# ⚡ Real Production Workflow

1️⃣ Code push → Git  
2️⃣ CI/CD build docker image  
3️⃣ Docker registry push  
4️⃣ Server deploy using docker compose

Example deploy:

```bash
docker compose pull
docker compose up -d
```

---

# 🧠 Production Best Practice

✔ `.env` file use  
✔ `restart: always`  
✔ volumes for database  
✔ nginx reverse proxy  
✔ separate dev & prod compose

---

✅ যদি চাও আমি আরও দেখাতে পারি:

- **Complete Docker production setup (step-by-step)**
    
- **Docker + Nginx + SSL HTTPS setup**
    
- **Docker CI/CD pipeline example**
    
- **Microservices Docker architecture**
    

এইগুলো DevOps job-এ খুব important। 🚀