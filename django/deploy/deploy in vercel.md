1. env make
2. debug=False
```python
ALLOWED_HOSTS = ['.vercel.app'127.0.0.1']
```


4. Root e file create
```
vercel.json
```

```
{
  "builds": [
    {
      "src": "staybangla/wsgi.py",
      "use": "@vercel/python",
      "config": { "maxLambdaSize": "15mb", "runtime": "python3.11" }
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "dest": "staybangla/wsgi.py"
    }
  ]
}
```

5. wsgi.py 
```
application = get_wsgi_application()
```
here, `applicaiton` change `app`

6. go to `ettings.py`
```
WSGI_APPLICATION = 'config.wsgi.application'
```

here `application ` change to `app`
why `vercel does not support applicaion`


7. `requirements.txt` file `genereated`
```
pip freeze > requirements.txt
```




------------

# Djanngo cors header added

আপনি সম্ভবত **`django-cors-headers`** প্যাকেজের কথা বলছেন। এটি Django API-তে অন্য ডোমেইন (যেমন Vercel frontend) থেকে request আসতে দিলে CORS কনফিগার করার জন্য ব্যবহৃত হয়।

## ১. প্যাকেজ ইনস্টল করুন

```bash
pip install django-cors-headers
```

তারপর `requirements.txt` আপডেট করুন:

```bash
pip freeze > requirements.txt
```

---

## ২. `INSTALLED_APPS`-এ যোগ করুন

```python
INSTALLED_APPS = [
    ...
    "corsheaders",
    ...
]
```

---

## ৩. `MIDDLEWARE`-এ যোগ করুন

`CorsMiddleware` যতটা সম্ভব উপরে রাখুন:

```python
MIDDLEWARE = [
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    ...
]
```

---

## ৪. CORS কনফিগার করুন

যদি আপনার frontend Vercel-এ থাকে:

```python
CORS_ALLOWED_ORIGINS = [
    "https://your-frontend.vercel.app",
]
```

একাধিক ডোমেইন হলে:

```python
CORS_ALLOWED_ORIGINS = [
    "https://newsora.vercel.app",
    "http://localhost:3000",
]
```

---

## ৫. Development-এর জন্য (শুধু টেস্টিং)

```python
CORS_ALLOW_ALL_ORIGINS = True
```

> **Production-এ এটি ব্যবহার করবেন না**, কারণ এতে যেকোনো ডোমেইন আপনার API-তে request পাঠাতে পারবে।

---

## ৬. যদি Cookie বা Session Authentication ব্যবহার করেন

```python
CORS_ALLOW_CREDENTIALS = True
```

এবং:

```python
CSRF_TRUSTED_ORIGINS = [
    "https://your-frontend.vercel.app",
]
```

---

### গুরুত্বপূর্ণ

`django-cors-headers` **400 Bad Request (DisallowedHost)** ঠিক করবে না। এটি শুধুমাত্র **CORS** সমস্যা (যেমন browser-এ "Access-Control-Allow-Origin" error) সমাধান করে।

যদি আপনার Vercel-এ সরাসরি URL খুললেই **400 Bad Request** আসে, তাহলে সেটি সাধারণত `ALLOWED_HOSTS` বা `CSRF`-সংক্রান্ত সমস্যা, CORS নয়।

আপনি যদি `settings.py`-এর `DEBUG`, `ALLOWED_HOSTS`, `CSRF_TRUSTED_ORIGINS`, `CORS_ALLOWED_ORIGINS`, এবং `MIDDLEWARE` অংশ শেয়ার করেন, তাহলে আমি দেখে বলতে পারব ঠিক কোথায় সমস্যা আছে।


