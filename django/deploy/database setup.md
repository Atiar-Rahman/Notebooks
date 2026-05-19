ঠিক জায়গায় এসেছো 👍 — এখানে তোমাকে **production database setup করতে হবে**। আমি step-by-step বলছি কী কী করতে হবে 👇

---

# 🟢 Step 1: Database create করো

👉 Click করো: **Add Database**

তারপর:

- **Database Name:**  
    👉 example: `zsbuilder_db`
    

✔ Create করো

---

# 🟢 Step 2: Database User create করো

👉 যাও: **Database User(s)** tab

- **Username:**  
    👉 example: `zsbuilder_user`
    
- **Password:**  
    👉 strong password দাও
    

✔ Create User

---

# 🟢 Step 3: User কে database-এ add করো

👉 যাও: **Add User To Database**

Select করো:

- Database: `zsbuilder_db`
    
- User: `zsbuilder_user`
    

👉 তারপর:  
✔ **ALL PRIVILEGES** enable করো

✔ Save

---

## 🔥 Important (naming rule)

cPanel-এ usually full name হয়:

```
myheettst_zsbuilder_db
myheettst_zsbuilder_user
```

👉 prefix (`myheettst_`) automatically যোগ হয়

---

# ⚙️ Step 4: Django settings.py update

SSH-এ গিয়ে `settings.py` edit করো:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myheettst_zsbuilder_db',
        'USER': 'myheettst_zsbuilder_user',
        'PASSWORD': 'your_password_here',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

# 📦 Step 5: MySQL driver install

SSH-এ run করো:

```bash
pip install mysqlclient
```

👉 error হলে:

```bash
pip install PyMySQL
```

তারপর `settings.py`-এর top এ add করো:

```python
import pymysql
pymysql.install_as_MySQLdb()
```

---

# 🔁 Step 6: migrate করো

```bash
python manage.py migrate
```

---

# ✅ Done!

এখন তোমার Django database fully ready 🎉

---

## ❗ Quick checklist

✔ Database created  
✔ User created  
✔ User added to DB (ALL PRIVILEGES)  
✔ settings.py updated  
✔ migrate done

---

## 👉 চাইলে আমি verify করে দিতে পারি

তুমি শুধু বলো:

- তুমি কী name দিয়েছো (db + user)
    
- password ছাড়া settings.py paste করো
    

আমি check করে ঠিক করে দিবো 💯




Perfect 👍 তুমি এখন একদম final setup stage-এ আছো। এখন কী কী fill করতে হবে সেটা clear করে দিচ্ছি 👇

---

# ✅ তোমার form কীভাবে fill করবে

## 🔹 Application Name

👉 যেকোনো নাম দাও:

```
zsbuilder
```

---

## 🔹 Deployment Domain

👉 Already ঠিক আছে:

```
zsbuilder.myheetstarea.com
```

---

## 🔹 Base Application URL

👉 এটা রাখো:

```
/
```

(বা default থাকলে change করার দরকার নাই)

---

## 🔹 Application Path

👉 ঠিক আছে:

```
/home/myheetst/
```

---

## 🔹 Application Type

👉 Already correct:

```
Python 3 ✅
```

---

## 🔹 ⚠️ Application Startup File (VERY IMPORTANT)

👉 এখানে লিখো:

```
passenger_wsgi.py
```

---

## 🔹 Deployment Environment

👉 Select করো:

```
Production ✅
```

---

## 🔹 Start Command

👉 ফাঁকা রাখো (Passenger auto handle করবে)

---

## 🔹 Stop Command

👉 ফাঁকা রাখো

---

## 🔹 Environment Variables

👉 এখন দরকার নাই (পরে লাগলে add করবো)

---

# 🔥 Final filled version (summary)

```id="b4w7kx"
Application Name: zsbuilder
Domain: zsbuilder.myheetstarea.com
Base URL: /
Path: /home/myheetst/
Type: Python 3
Startup File: passenger_wsgi.py
Environment: Production
Start/Stop: (empty)
```

---

# 🚀 এরপর কী করবে

👉 **Create button চাপো**

---

# ⚠️ Create করার পর IMPORTANT

Immediately এইগুলো করো:

## 1️⃣ Project upload করো

```bash
/home/myheetst/
```

---

## 2️⃣ passenger_wsgi.py বানাও

---

## 3️⃣ SSH-এ গিয়ে install + migrate

---

## 4️⃣ Restart app

---

# ❗ Common error avoid করো

❌ startup file empty রাখলে app run করবে না
❌ Python 2 select করলে Django crash করবে

---

## 👉 Next step

তুমি এখন:
👉 **Create করে ফেলো**

তারপর বলো:

* create হয়েছে ✅
* বা error আসছে ❌

আমি next step (live site চালানো) full guide করবো 🔥









