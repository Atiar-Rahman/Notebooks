Deploying a **Django REST Framework (DRF)** project on cPanel is a bit different from deploying on VPS/cloud because cPanel is mainly built for PHP—but you _can_ do it using **Python App (Passenger)** support if your hosting allows it.

Here’s a clear, practical step-by-step guide 👇

---

# ✅ 1. Check Requirements

Make sure your cPanel hosting supports:

- **Python (Setup Python App / Passenger)**
    
- SSH access (recommended)
    

If you don’t see “Setup Python App” in cPanel, your host likely doesn’t support Django deployment.

---

# ✅ 2. Prepare Your Django Project

Before uploading:

### ✔️ Update `settings.py`

```python
ALLOWED_HOSTS = ['yourdomain.com']

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```

### ✔️ Collect static files

Run locally or on server:

```bash
python manage.py collectstatic
```

### ✔️ Freeze dependencies

```bash
pip freeze > requirements.txt
```

---

# ✅ 3. Upload Project to cPanel

- Go to **File Manager**
    
- Upload your project folder (zip → extract)
    
- Place it inside something like:
    

```
/home/username/myproject
```

---

# ✅ 4. Create Python App in cPanel

Go to:  
👉 **cPanel → Setup Python App**

Then:

- Python version: 3.x
    
- App root: `myproject`
    
- App URL: `/` or subdomain
    
- Startup file: `passenger_wsgi.py`
    
- Application entry point: `application`
    

Click **Create**

---

# ✅ 5. Configure WSGI File

Inside your app root, edit/create:

### `passenger_wsgi.py`

```python
import sys
import os

sys.path.insert(0, os.path.dirname(__file__))

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'myproject.settings')

from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
```

---

# ✅ 6. Install Dependencies

In cPanel Python App interface:

- Activate virtual environment
    
- Run:
    

```bash
pip install -r requirements.txt
```

---

# ✅ 7. Configure Database

If using MySQL in cPanel:

- Create DB via **MySQL Databases**
    
- Update `settings.py`:
    

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'cpanel_dbname',
        'USER': 'cpanel_user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

Install MySQL client:

```bash
pip install mysqlclient
```

---

# ✅ 8. Run Migrations

```bash
python manage.py migrate
```

---

# ✅ 9. Restart App

In Python App panel:  
👉 Click **Restart**

---

# ✅ 10. Configure Static Files (IMPORTANT)

cPanel does NOT serve static files automatically.

### Option 1: Add `.htaccess`

```apache
Alias /static /home/username/myproject/staticfiles
```

### Option 2 (better):

Use WhiteNoise:

```bash
pip install whitenoise
```

Then in `settings.py`:

```python
MIDDLEWARE.insert(1, 'whitenoise.middleware.WhiteNoiseMiddleware')

STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'
```

---

# ✅ 11. Test Your API

Visit:

```
https://yourdomain.com/api/
```

---

# ⚠️ Common Issues

- ❌ Module not found → wrong path in WSGI
    
- ❌ Static not loading → WhiteNoise not configured
    
- ❌ 500 error → check error logs in cPanel
    
- ❌ MySQL errors → missing `mysqlclient`
    

---

# 💡 Important Notes

- cPanel is **not ideal for Django** (good for small projects only)
    
- For production-grade DRF apps, consider:
    
    - VPS (DigitalOcean, AWS, etc.)
        
    - Docker deployment
        
    - Platforms like Railway / Render
        

---

Short answer: **`.env` file use korai best practice** 👍 — direct values `settings.py` te likha uchit na.

Let me explain simply 👇

---

# ✅ কেন `.env` use করা ভালো

### 1. 🔒 Security

Sensitive data hide থাকে:

* `SECRET_KEY`
* DB password
* API keys

GitHub এ push করলেও leak হবে না (if `.env` ignored).

---

# ✅ Recommended Way (Best Practice)

### 1. `.env` file create করো

Project root এ:

```env
DEBUG=False
SECRET_KEY=your-secret-key
DB_NAME=your_db
DB_USER=your_user
DB_PASSWORD=your_password
```

---

### 2. `python-decouple` install করো

```bash
pip install python-decouple
```

---

### 3. `settings.py` modify করো

```python
from decouple import config

DEBUG = config('DEBUG', default=False, cast=bool)
SECRET_KEY = config('SECRET_KEY')

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

# ⚠️ cPanel এ `.env` কাজ করবে?

👉 **হ্যাঁ, করবে** — but:

### Condition:

* `.env` file অবশ্যই project root এ থাকতে হবে
* permission ঠিক থাকতে হবে

---

# 🚫 Direct apply করলে সমস্যা

If you directly write:

```python
SECRET_KEY = "123456"
```

Problems:

* ❌ Security risk
* ❌ Code reuse করা কঠিন
* ❌ Production/Development mix হয়ে যায়

---

# 🔥 Alternative (Advanced - cPanel)

cPanel Python App এ environment variable set করা যায়:

👉 **Setup Python App → Environment Variables**

Example:

```
SECRET_KEY=xxxxx
DEBUG=False
```

Then use:

```python
import os
SECRET_KEY = os.environ.get('SECRET_KEY')
```

👉 This is actually **best for production**

---

# 💡 My Recommendation

* Development → `.env`
* Production (cPanel) → **Environment Variables (better than .env)**

---

# ✅ Final Verdict

✔ Use `.env` (easy & safe)
✔ OR use cPanel Environment Variables (more secure in production)
❌ Don’t hardcode secrets in `settings.py`

---

ভাল প্রশ্ন — এটা অনেকেই প্রথমে confused হয় 👍

## ✅ Short Answer

👉 **cPanel hosting হলে `localhost database` (MySQL) use করলেই যথেষ্ট**
👉 **cloud database use করা বাধ্যতামূলক না**

---

# 🧠 বিস্তারিত বুঝে নাও

## ✅ Option 1: cPanel Local Database (Recommended for you)

cPanel এ তুমি **MySQL Database** create করতে পারো:

👉 cPanel → MySQL Databases

তারপর `settings.py` এ:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'cpanel_dbname',
        'USER': 'cpanel_user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

### 👍 সুবিধা:

* সহজ setup
* extra cost নাই
* cPanel এর সাথে fully compatible
* beginners এর জন্য best

---

## ☁️ Option 2: Cloud Database (Optional)

Examples:

* Amazon RDS
* PlanetScale
* Supabase

### 👍 সুবিধা:

* better scalability
* backup & reliability বেশি
* multiple server থেকে access করা যায়

### 👎 অসুবিধা:

* setup complex
* latency issue হতে পারে
* paid হতে পারে

---

# ⚖️ কোনটা use করবে?

### 👉 তোমার case (DRF + cPanel):

✔ **Local MySQL (localhost) use করো**

---

### 👉 Cloud use করো যদি:

* high traffic app
* multiple server
* microservices architecture
* production scaling দরকার

---

# 🔥 Important Tip

cPanel এ database name সাধারণত এমন হয়:

```
username_dbname
```

---

# ✅ Final Recommendation

👉 এখন:
✔ localhost database use করো
👉 পরে scale হলে:
✔ cloud database এ migrate করো

---

এই তথ্যগুলো তুমি **cPanel থেকেই নিজে create করলে পাবে** — Django নিজে এগুলো দেয় না।

আমি step-by-step সহজভাবে দেখাচ্ছি 👇

---

# 🟢 1. `NAME` (Database Name) কোথা থেকে পাবে?

👉 cPanel → **MySQL Databases**

### Steps:

1. “Create New Database” এ যাও
2. নাম দাও (example: `mydb`)

👉 cPanel auto করে full name বানাবে:

```text
username_mydb
```

✔ এটিই তোমার `NAME`

---

# 🟢 2. `USER` (Database User)

👉 একই page এ:

### Steps:

1. “MySQL Users” section এ যাও
2. “Add New User” করো
3. username + password set করো

👉 cPanel বানাবে:

```text
username_dbuser
```

✔ এটিই তোমার `USER`

---

# 🟢 3. `PASSWORD`

👉 তুমি যখন user create করো তখনই password set করো

✔ সেই password-ই Django তে দিতে হবে

⚠️ এটা পরে আর দেখানো যায় না
(যদি ভুলে যাও → reset করতে হবে)

---

# 🟢 4. User কে Database এর সাথে connect করা (IMPORTANT)

👉 cPanel → “Add User To Database”

### Steps:

1. user select করো
2. database select করো
3. ALL PRIVILEGES tick করো ✔

---

# 🔥 Final Example

ধরো তুমি create করলে:

* Database: `username_blogdb`
* User: `username_bloguser`
* Password: `mypassword123`

তাহলে Django settings:

```python id="dbcfg1"
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'username_blogdb',
        'USER': 'username_bloguser',
        'PASSWORD': 'mypassword123',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

# ⚠️ Common Mistakes

❌ শুধু “db name” লিখে দেওয়া (username ছাড়া)
❌ user কে database permission না দেওয়া
❌ wrong password copy করা
❌ HOST = 127.0.0.1 instead of localhost (cPanel এ usually localhost)

---

# 👍 Summary

তুমি manually create করবে:

* Database → NAME
* User → USER
* Password → PASSWORD
* Then link them together

---

ভালো প্রশ্ন 👍 — Django REST Framework deploy করার সময় এটা খুব গুরুত্বপূর্ণ সিদ্ধান্ত।

---

# 🟢 Short Answer

👉 **cPanel hosting এ সাধারণভাবে direct media upload (local storage) কাজ করবে**
👉 কিন্তু **production + scalable app হলে Cloudinary use করাই better**

---

# 📁 Option 1: Direct (cPanel Local Storage)

Django default ভাবে server এ ফাইল save করে:

```python id="media1"
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

---

## ✔️ এটা কিভাবে কাজ করে?

* Upload করলে file যাবে:

```text id="media2"
/home/username/project/media/
```

* তারপর URL:

```text
https://yourdomain.com/media/image.jpg
```

---

## 👍 সুবিধা

* সহজ setup
* extra service লাগে না
* cPanel hosting এ fully supported

---

## 👎 সমস্যা

* server storage fill হয়ে যাবে
* backup কঠিন
* scaling difficult
* shared hosting এ performance issue হতে পারে

---

# ☁️ Option 2: Cloudinary (Recommended for DRF APIs)

👉 Cloudinary

---

## ✔️ কিভাবে কাজ করে?

* Image/video upload করলে cloud এ যায়
* Django শুধু URL store করে

Example:

```text id="cdn1"
https://res.cloudinary.com/xyz/image/upload/v123/sample.jpg
```

---

## 👍 সুবিধা

* Unlimited storage (plan-based)
* Fast CDN delivery
* Auto image optimization
* Secure & scalable
* Mobile app / API এর জন্য best

---

## 👎 অসুবিধা

* extra setup লাগে
* free tier limited

---

# ⚖️ কোনটা use করবে?

## 👉 তোমার case (DRF + cPanel)

### 🟡 Start stage:

✔ Direct media upload (local) use করতে পারো

### 🔵 Production / real app:

✔ Cloudinary use করাই best

---

# 🔥 Best Practice (Recommended Hybrid)

👉 Images = Cloudinary
👉 Files (PDF, docs) = local OR cloud storage

---

# ⚙️ Cloudinary setup (basic idea)

```bash id="cl1"
pip install cloudinary
```

```python id="cl2"
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

---

# 🚀 Final Recommendation

✔ ছোট project / learning → local media
✔ real app / API / mobile app → **Cloudinary (best choice)**

---

# 💡 Simple Rule

👉 “If you care about scaling → use Cloudinary”
👉 “If you just testing on cPanel → local is fine”

---

If you want, I can:

* full Cloudinary setup for Django REST Framework
* or cPanel media upload fix (static + media serving properly)

just tell 👍

-------------




https://www.youtube.com/watch?v=yuM8thlrEs8




---------------
![[Pasted image 20260430095630.png]]
![[Pasted image 20260430100021.png]]
