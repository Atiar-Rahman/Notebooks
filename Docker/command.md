
## 1️⃣ Running container দেখার জন্য

```bash
docker ps
```

সব running container দেখাবে।

---

## 2️⃣ সব container দেখার জন্য

```bash
docker ps -a
```

Running + stopped container দেখাবে।

---

## 3️⃣ Docker image list

```bash
docker images
```

লোকাল machine এ থাকা সব image দেখাবে।

---

## 4️⃣ Container logs দেখার জন্য

```bash
docker logs CONTAINER_NAME
```

Example:

```bash
docker logs my_app
```

Live logs দেখতে:

```bash
docker logs -f my_app
```

---

## 5️⃣ Container এর ভিতরে ঢোকার জন্য

```bash
docker exec -it CONTAINER_NAME bash
```

Example:

```bash
docker exec -it my_app bash
```

---

## 6️⃣ Container stop করা

```bash
docker stop CONTAINER_NAME
```

---

## 7️⃣ Container remove করা

```bash
docker rm CONTAINER_NAME
```

---

## 8️⃣ Image delete করা

```bash
docker rmi IMAGE_ID
```

---

## 9️⃣ Container resource usage check

```bash
docker stats
```

CPU / RAM usage দেখাবে।

---

## 🔟 Docker clean (unused container + image)

```bash
docker system prune
```

সব unused resource clean করবে।

---

💡 **Bonus (very useful)**  
Disk space কত Docker নিচ্ছে:

```bash
docker system df
```

---
নিচে **Docker এর 15টা real production command** দিলাম যেগুলো DevOps / backend engineerরা প্রায়ই ব্যবহার করে। প্রতিটা সাথে ছোট exampleও আছে।

---

# 🐳 Docker এর 15টা Real Production Command

## 1️⃣ Running container list

```bash
docker ps
```

➡️ সব running container দেখাবে।

Example:

```
CONTAINER ID   IMAGE     STATUS
3f21abcde      nginx     Up 2 hours
```

---

## 2️⃣ All container (running + stopped)

```bash
docker ps -a
```

---

## 3️⃣ Image list

```bash
docker images
```

Output:

```
REPOSITORY   TAG       IMAGE ID
nginx        latest    605c77e
redis        7         a1b2c3d
```

---

## 4️⃣ Container run করা

```bash
docker run -d -p 80:80 nginx
```

Explanation

- `-d` = background
    
- `-p` = port mapping
    

---

## 5️⃣ Container logs দেখা

```bash
docker logs my_container
```

Live logs:

```bash
docker logs -f my_container
```

---

## 6️⃣ Container এর ভিতরে ঢোকা

```bash
docker exec -it my_container bash
```

---

## 7️⃣ Container stop করা

```bash
docker stop my_container
```

---

## 8️⃣ Container start করা

```bash
docker start my_container
```

---

## 9️⃣ Container restart করা

```bash
docker restart my_container
```

Production server এ খুব common।

---

## 🔟 Container delete করা

```bash
docker rm my_container
```

Force delete:

```bash
docker rm -f my_container
```

---

## 1️⃣1️⃣ Image delete করা

```bash
docker rmi IMAGE_ID
```

---

## 1️⃣2️⃣ Docker resource usage

```bash
docker stats
```

Output example:

```
CONTAINER   CPU %   MEM USAGE
nginx       0.10%   20MB
redis       0.05%   10MB
```

---

## 1️⃣3️⃣ Container inspect

```bash
docker inspect my_container
```

Container এর full configuration দেখাবে (IP, volume, network)।

---

## 1️⃣4️⃣ Docker disk usage

```bash
docker system df
```

Example:

```
TYPE            TOTAL
Images          5
Containers      3
Local Volumes   2
```

---

## 1️⃣5️⃣ Docker cleanup

```bash
docker system prune
```

সব unused resource remove করবে।

Force:

```bash
docker system prune -a
```

---

# ⚡ Real Production Example

ধরো **nginx deploy করতে চাও**

```bash
docker pull nginx
docker run -d -p 80:80 --name web nginx
docker ps
docker logs web
```

Server restart হলে auto start করতে:

```bash
docker run -d -p 80:80 --restart=always nginx
```

---

✅ চাইলে আমি আরও দেখাতে পারি:

- **20টা Docker troubleshooting command**
    
- **Docker interview top 30 question**
    
- **Docker networking simple explanation**
    
- **Docker compose production example**
    

তুমি চারটা জিনিস জানতে চেয়েছো। আমি সহজভাবে একসাথে সাজিয়ে দিলাম যাতে **DevOps / Backend interview + real production** এ কাজে লাগে। 🚀

---

# 🛠️ 1️⃣ 20টা Docker Troubleshooting Command

### Container সমস্যা চেক

```bash
docker ps
docker ps -a
docker logs CONTAINER_NAME
docker logs -f CONTAINER_NAME
docker inspect CONTAINER_NAME
```

### Container ভিতরে debug

```bash
docker exec -it CONTAINER_NAME bash
docker exec -it CONTAINER_NAME sh
```

### Resource সমস্যা

```bash
docker stats
docker top CONTAINER_NAME
```

### Network debug

```bash
docker network ls
docker network inspect NETWORK_NAME
```

### Disk space সমস্যা

```bash
docker system df
docker system prune
docker system prune -a
```

### Image সমস্যা

```bash
docker images
docker pull IMAGE_NAME
docker rmi IMAGE_ID
```

### Container lifecycle

```bash
docker stop CONTAINER
docker start CONTAINER
docker restart CONTAINER
docker rm CONTAINER
```

---

# 🎯 2️⃣ Docker Interview Top 30 Questions

### Basic

1. Docker কি?
    
2. Container vs VM পার্থক্য?
    
3. Docker image কি?
    
4. Docker container কি?
    
5. Dockerfile কি?
    

### Intermediate

6. Docker volume কি?
    
7. Docker network কি?
    
8. Docker compose কি?
    
9. Port mapping কি?
    
10. Bind mount vs volume difference?
    

### Image related

11. `docker build` কি করে?
    
12. `docker pull` কি?
    
13. `docker push` কি?
    
14. Layered filesystem কি?
    
15. Multi-stage build কি?
    

### Container related

16. Container lifecycle কি?
    
17. `docker run` vs `docker start`
    
18. Detached mode কি?
    
19. Restart policy কি?
    
20. Environment variable container এ কিভাবে pass করো?
    

### Production

21. Docker security best practice?
    
22. Container logging কিভাবে manage করো?
    
23. Docker networking types?
    
24. Container scaling কিভাবে করো?
    
25. Healthcheck কি?
    

### Advanced

26. Docker swarm কি?
    
27. Kubernetes vs Docker?
    
28. Docker registry কি?
    
29. Overlay network কি?
    
30. Docker compose production এ কিভাবে use করো?
    

---

# 🌐 3️⃣ Docker Networking Simple Explanation

Docker এ **3টা main network type** আছে।

### 1️⃣ Bridge Network (default)

Container ↔ Container communication

```
Container A ----\
                  -> Bridge Network
Container B ----/
```

Command:

```bash
docker network ls
```

Custom network:

```bash
docker network create mynetwork
```

Run container in network:

```bash
docker run -d --network=mynetwork nginx
```

---

### 2️⃣ Host Network

Container সরাসরি host network ব্যবহার করে।

```
Container -> Host Network
```

```bash
docker run --network host nginx
```

---

### 3️⃣ None Network

Network disable।

```bash
docker run --network none nginx
```

---

# ⚙️ 4️⃣ Docker Compose Production Example

ধরো **Nginx + NodeJS + MySQL**

### docker-compose.yml

```yaml
version: "3.8"

services:

  app:
    image: node:18
    container_name: node_app
    restart: always
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: npm start
    depends_on:
      - db

  db:
    image: mysql:8
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: appdb
    volumes:
      - dbdata:/var/lib/mysql

  nginx:
    image: nginx:latest
    container_name: nginx_web
    restart: always
    ports:
      - "80:80"
    depends_on:
      - app

volumes:
  dbdata:
```

---

### Run compose

```bash
docker compose up -d
```

Stop

```bash
docker compose down
```

---

# 🧠 Production Tip (Important)

Always use:

```
restart: always
volumes
environment variables
custom network
```

---
তুমি সম্ভবত জানতে চাও **Docker Compose কোথায় শিখতে পারি / কোথায় পড়তে পারি**। নিচে কয়েকটা ভালো source দিলাম। 📚

---

# 📖 Docker Compose কোথায় শিখবে

## 1️⃣ Official Documentation (সবচেয়ে ভালো)

👉 Docker Compose এর official docs

- খুব clear explanation
    
- production example আছে
    
- best practice শেখানো হয়
    

Link:  
[https://docs.docker.com/compose/](https://docs.docker.com/compose/)

---

## 2️⃣ YouTube (Beginner friendly)

Search করো:

- **Docker Compose tutorial**
    
- **Docker Compose for beginners**
    
- **Docker Compose production setup**
    

ভালো channels:

- TechWorld with Nana
    
- NetworkChuck
    

---

## 3️⃣ Interactive learning website

### Play with Docker

Browser এর ভিতরেই Docker practice করা যায়।

---

## 4️⃣ GitHub production example

GitHub এ search করো:

```
docker-compose.yml example
```

অনেক real project পাওয়া যায়।

GitHub:  
[https://github.com](https://github.com)

---

# 🧠 Docker Compose শিখতে যে 5টা topic পড়বে

1️⃣ docker-compose.yml structure  
2️⃣ services  
3️⃣ volumes  
4️⃣ networks  
5️⃣ environment variables

Example:

```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "80:80"
```

Run:

```bash
docker compose up -d
```

---

✅ চাইলে আমি তোমাকে দেখাতে পারি:

- **Docker Compose complete tutorial (beginner → advanced)**
    
- **Real production compose file (NodeJS + Redis + MySQL + Nginx)**
    
- **Docker Compose interview questions**
    

এগুলো শিখলে **Docker Compose খুব সহজ হয়ে যাবে।** 🚀