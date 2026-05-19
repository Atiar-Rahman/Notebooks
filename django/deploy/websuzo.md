
# mysql db connect 

1. dbcreate



```
Database: username_dbname  ; conference
User: username_user  ; admin
Password: your_password ;6fdeyWECqY
Host: localhost ; domain name
Port: 3306
```

হ্যাঁ 👍 তুমি যেটা লিখেছো — **`username_dbname`** — এটা একদম ঠিক format।

Webuzo / cPanel টাইপ হোস্টিং-এ database name সাধারণত হয়:

```text
cpanel_username + "_" + database_name
```

---

# ✅ Example বুঝার জন্য

ধরো:

* তোমার Webuzo username = `john`
* তুমি database বানাও = `myapp`

👉 তাহলে final database name হবে:

```text
john_myapp
```

---

# 🧩 Django-তে কিভাবে বসাবে

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'john_myapp',        # 👈 full database name
        'USER': 'john_user',         # 👈 full username
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

# ⚠️ খুব গুরুত্বপূর্ণ

❌ ভুল:

```text
myapp
```

✅ সঠিক:

```text
john_myapp
```

---

# 🔍 Check করার জায়গা

Webuzo → **Current Databases**

সেখানে exact name দেখাবে 👇
👉 সেটাই copy করে ব্যবহার করো

---

# ❗ Common mistake

* database name ভুল (prefix বাদ দেওয়া)
* user name ভুল
* user database-এ add করা হয়নি

👉 নিশ্চিত হও:
**Add User To Database** করা আছে ✔

---


ভালো 👍 তুমি এখন **database user create step-এ আছো**, কিন্তু এখনও user-টা database-এর সাথে connect করো নাই — তাই ডান পাশে দেখাচ্ছে:

👉 **“Please add Database/User to assign privileges”**

এখন কী করতে হবে step-by-step 👇

---

# ✅ Next Step: User কে Database-এ Add করা

## 👉 Step 1:

উপরে click করো:

```
Add User To Database
```

---

## 👉 Step 2:

তুমি dropdown-এ দেখবে:

* **User:** `myheest_admin` (তুমি যেটা বানিয়েছো)
* **Database:** `myheest_dbname` (তোমার database)

👉 এই দুটা select করো

---

## 👉 Step 3:

Click:

```
Add
```

---

## 👉 Step 4:

Privileges page আসবে

👉 সব checkbox tick দাও:

```
ALL PRIVILEGES ✅
```

তারপর:

```
Make Changes
```

---

# 🎯 এখন তোমার final info হবে:

```text
Database: myheest_dbname
User: myheest_admin
Password: (তুমি যেটা দিয়েছো)
Host: localhost
Port: 3306
```

---

# ⚙️ Django-তে বসাও

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'myheest_dbname',
        'USER': 'myheest_admin',
        'PASSWORD': 'your_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

# 🧪 Test করো

```bash
python manage.py migrate
```

👉 যদি error না আসে → ✅ Done

---

# ❗ Important

তুমি এখনো **user কে database-এ attach করোনি**, তাই Django connect করলে error দিবে ❌

---

# 👍 চাইলে

তুমি পরের screenshot দাও (Add User To Database step),
আমি দেখে confirm করে দিবো সব ঠিক আছে কিনা 🔍
