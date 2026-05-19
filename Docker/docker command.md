
## 1️⃣ `docker pull IMAGE_NAME`

👉 Docker Hub থেকে কোনো **image download** করার জন্য।

**Example**

```bash
docker pull ubuntu
```

📌 মানে: Docker Hub থেকে **Ubuntu image** নামিয়ে আনবে।

---

## 2️⃣ `docker images`

👉 তোমার কম্পিউটারে **কোন কোন Docker image আছে** তা দেখায়।

**Example**

```bash
docker images
```

Output example:

```
REPOSITORY   TAG       IMAGE ID
ubuntu       latest    3f2e3
node         20        9a8f1
```

---

## 3️⃣ `docker run IMAGE_NAME`

👉 একটি **container run/start** করে সেই image থেকে।

**Example**

```bash
docker run ubuntu
```

📌 Ubuntu image দিয়ে একটি container চালু হবে।

---

## 4️⃣ `docker run -it IMAGE_NAME`

👉 Interactive mode এ container চালায়।

**Example**

```bash
docker run -it ubuntu
```

📌 এতে তুমি container এর ভিতরে **terminal ব্যবহার করতে পারবে**।

Example output:

```
root@container:/#
```

---

## 5️⃣ `docker stop CONT_NAME or CONT_ID`

👉 চলমান container **stop** করার জন্য।

**Example**

```bash
docker stop my_container
```

অথবা

```bash
docker stop a34f56
```

---

## 6️⃣ `docker start CONT_NAME or CONT_ID`

👉 Stop করা container **আবার start** করার জন্য।

**Example**

```bash
docker start my_container
```

---

# 🧠 Easy Flow (Docker কাজ করার ধাপ)

```
docker pull ubuntu
       ↓
docker run -it ubuntu
       ↓
docker stop container_id
       ↓
docker start container_id
```

---

এই ছবিটাতে আরও কিছু **important Docker commands** আছে। আমি সহজভাবে explain করছি। 🐳

---

## 1️⃣ `docker ps`

👉 বর্তমানে **running container** গুলো দেখায়।

**Example**

```bash
docker ps
```

**Output example**

```
CONTAINER ID   IMAGE     STATUS       PORTS
a12bc34        ubuntu    Up 2 minutes
```

📌 মানে এখন কোন container **চালু আছে** তা দেখাবে।

---

## 2️⃣ `docker ps -a`

👉 সব container দেখায় (Running + Stopped)।

**Example**

```bash
docker ps -a
```

**Output example**

```
CONTAINER ID   IMAGE     STATUS
a12bc34        ubuntu    Up 2 minutes
b45cd67        node      Exited
```

📌 এখানে **বন্ধ container গুলোও দেখা যাবে**।

---

## 3️⃣ `docker rmi IMAGE_NAME`

👉 Docker **image delete** করার জন্য।

**Example**

```bash
docker rmi ubuntu
```

📌 এতে **Ubuntu image remove হয়ে যাবে**।

⚠️ যদি সেই image দিয়ে container run থাকে তাহলে আগে container stop/remove করতে হবে।

---

## 4️⃣ `docker rm CONT_NAME`

👉 **Container delete** করার জন্য।

**Example**

```bash
docker rm my_container
```

অথবা

```bash
docker rm 8a7f3
```

📌 এতে container permanently delete হয়ে যাবে।

---

# 🧠 Easy Docker Lifecycle

```
docker pull ubuntu
      ↓
docker run -it ubuntu
      ↓
docker ps
      ↓
docker stop container_id
      ↓
docker rm container_id
      ↓
docker rmi ubuntu
```

---
![[Pasted image 20260310173804.png]]





![[Pasted image 20260310174415.png]]

---
![[Pasted image 20260310192300.png]]

---

![[Pasted image 20260310192821.png]]


---

![[Pasted image 20260310193124.png]]



---
![[Pasted image 20260310194307.png]]
![[Pasted image 20260310194444.png]]





---

# 1. Docker System & Info Commands

|Command|Description|
|---|---|
|`docker version`|Show Docker version|
|`docker info`|Display system-wide information|
|`docker help`|Show help for Docker|
|`docker --help`|List all commands|

---

# 2. Docker Image Commands

|Command|Description|
|---|---|
|`docker images`|List images|
|`docker pull <image>`|Download image from registry|
|`docker push <image>`|Upload image to registry|
|`docker build -t <name> .`|Build image from Dockerfile|
|`docker rmi <image>`|Remove image|
|`docker tag <image> <new-tag>`|Tag an image|
|`docker history <image>`|Show image history|
|`docker inspect <image>`|Detailed image info|
|`docker save <image>`|Save image to tar|
|`docker load`|Load image from tar|

Example:

```bash
docker pull nginx
docker images
docker rmi nginx
```

---

# 3. Docker Container Commands

|Command|Description|
|---|---|
|`docker run <image>`|Create & start container|
|`docker start <container>`|Start container|
|`docker stop <container>`|Stop container|
|`docker restart <container>`|Restart container|
|`docker kill <container>`|Force stop|
|`docker pause <container>`|Pause container|
|`docker unpause <container>`|Resume container|
|`docker rm <container>`|Remove container|
|`docker ps`|Running containers|
|`docker ps -a`|All containers|
|`docker rename <container>`|Rename container|

Example:

```bash
docker run -d nginx
docker ps
docker stop container_id
```

---

# 4. Docker Container Interaction

|Command|Description|
|---|---|
|`docker exec -it <container> bash`|Run command inside container|
|`docker attach <container>`|Attach to running container|
|`docker logs <container>`|View logs|
|`docker top <container>`|Show processes|
|`docker stats`|Container resource usage|

Example:

```bash
docker exec -it mycontainer bash
docker logs mycontainer
```

---

# 5. Docker Networking

|Command|Description|
|---|---|
|`docker network ls`|List networks|
|`docker network create <name>`|Create network|
|`docker network inspect <name>`|Network details|
|`docker network connect`|Connect container|
|`docker network disconnect`|Disconnect container|
|`docker network rm`|Remove network|

---

# 6. Docker Volume Commands

|Command|Description|
|---|---|
|`docker volume ls`|List volumes|
|`docker volume create`|Create volume|
|`docker volume inspect`|Volume details|
|`docker volume rm`|Remove volume|
|`docker volume prune`|Remove unused volumes|

Example:

```bash
docker volume create myvolume
docker volume ls
```

---

# 7. Docker System Cleanup

|Command|Description|
|---|---|
|`docker system df`|Disk usage|
|`docker system prune`|Remove unused data|
|`docker container prune`|Remove stopped containers|
|`docker image prune`|Remove unused images|
|`docker volume prune`|Remove unused volumes|
|`docker network prune`|Remove unused networks|

---

# 8. Docker Login & Registry

|Command|Description|
|---|---|
|`docker login`|Login to Docker Hub|
|`docker logout`|Logout|
|`docker search <image>`|Search images|

---

# 9. Docker Compose (multi-container)

If you use **Docker Compose**:

|Command|Description|
|---|---|
|`docker compose up`|Start services|
|`docker compose up -d`|Start in background|
|`docker compose down`|Stop services|
|`docker compose ps`|List containers|
|`docker compose logs`|View logs|
|`docker compose build`|Build services|

---

# 10. Advanced Docker Commands

|Command|Description|
|---|---|
|`docker cp`|Copy files between host/container|
|`docker diff`|Show file changes|
|`docker export`|Export container|
|`docker import`|Import filesystem|
|`docker commit`|Create image from container|

Example:

```bash
docker cp file.txt container:/app/
```

---

# 11. Most Used Docker Commands (Daily Use) ⭐

These are the **10 commands developers use most**:

```bash
docker pull
docker build
docker run
docker ps
docker stop
docker rm
docker images
docker exec
docker logs
docker compose up
```

---

