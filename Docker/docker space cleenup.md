
ঠিক আছে 👍 নিচের **একটা safe cleanup script** দিলে তুমি Linux + Docker + pip + apt cache অনেকটা clean করতে পারবে। এতে সাধারণত **30-100GB পর্যন্ত space free হয়** (যদি cache বেশি থাকে) 🚀

## 🧹 Full Cleanup Commands

একটার পর একটা run করো:

```bash
# 1. Docker unused images, containers, networks remove
docker system prune -a -f

# 2. Docker build cache clean
docker builder prune -a -f

# 3. Docker unused volumes
docker volume prune -f

# 4. apt cache clean
sudo apt clean
sudo apt autoremove -y

# 5. pip cache clean
pip cache purge

# 6. user cache clean
rm -rf ~/.cache/*
```

---

## 📊 এরপর check করো কত space free হলো

```bash
df -h
```

---

## 🔎 যদি এখনও drive full থাকে

এই command run করো (সবচেয়ে বড় folder খুঁজে বের করবে):

```bash
sudo du -h / | sort -rh | head -20
```

---

💡 তোমার লগ দেখে মনে হচ্ছে তুমি **Docker দিয়ে Django + Celery + Postgres project run করছো**।  
এই ধরনের project এ **Docker build cache খুব দ্রুত 20-50GB হয়ে যায়** — এটা normal।

---

যদি চাও, আমি তোমাকে দেখাতে পারি:

- **Docker cache permanently limit করার উপায়**
    
- **Docker build 10x faster করার trick**
    
- **AI/ML project এর জন্য disk safe setup**
    

এগুলো জানলে ভবিষ্যতে **drive আর full হবে না** 😄