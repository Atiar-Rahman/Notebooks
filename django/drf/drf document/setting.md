আচ্ছা 🤝 বুঝেছি — **project না**, একদম **DRF settings শেখা**।
চল এটা **Beginner → Intermediate → Pro** লেভেলে করি, **pure learning mode**, ছোট ছোট example সহ।

---

# 🧠 DJANGO REST FRAMEWORK SETTINGS

**Beginner → Pro (with examples)**

---

## 🟢 LEVEL 1: BEGINNER (DRF চালু করা)

### 1️⃣ DRF install + enable

```bash
pip install djangorestframework
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

👉 এখন DRF use করা যাবে

---

### 2️⃣ Minimum REST_FRAMEWORK setting

```python
REST_FRAMEWORK = {}
```

👉 না দিলেও চলে, কিন্তু learning এর জন্য রাখা ভালো

---

### 3️⃣ Simple APIView (no auth, no permission)

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class HelloAPI(APIView):
    def get(self, request):
        return Response({"msg": "Hello DRF"})
```

🧠 **Beginner goal:**
👉 DRF কী
👉 APIView কীভাবে কাজ করে

---

## 🟡 LEVEL 2: AUTHENTICATION & PERMISSION (Core concept)

### 4️⃣ Authentication class

Authentication = **তুমি কে?**

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
    ]
}
```

✔️ Django login user detect করবে

---

### 5️⃣ Permission class

Permission = **কি করতে পারবে?**

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.AllowAny',
    ]
}
```

Common permissions 👇

| Class                     | Meaning          |
| ------------------------- | ---------------- |
| AllowAny                  | সবাই             |
| IsAuthenticated           | শুধু logged user |
| IsAdminUser               | শুধু admin       |
| IsAuthenticatedOrReadOnly | read public      |

---

### 6️⃣ View-wise permission override

```python
from rest_framework.permissions import IsAuthenticated

class ProfileAPI(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response({"user": request.user.username})
```

🧠 **Beginner → Intermediate transition**

---

## 🟠 LEVEL 3: TOKEN AUTH (Industry standard)

### 7️⃣ Token authentication setup

```python
INSTALLED_APPS += ['rest_framework.authtoken']
```

```bash
python manage.py migrate
```

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

Request header 👇

```
Authorization: Token abc123...
```

🧠 **Concept:** Stateless auth

---

## 🟠 LEVEL 4: SERIALIZER & RENDERER

### 8️⃣ Renderer (Response format)

```python
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
    ]
}
```

👉 JSON only
👉 Browsable API off

---

### 9️⃣ Parser (Request format)

```python
REST_FRAMEWORK = {
    'DEFAULT_PARSER_CLASSES': [
        'rest_framework.parsers.JSONParser',
        'rest_framework.parsers.FormParser',
    ]
}
```

---

## 🔵 LEVEL 5: PAGINATION (Big APIs)

### 🔹 PageNumberPagination

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS':
        'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 5,
}
```

Response 👇

```json
{
  "count": 25,
  "next": "?page=2",
  "previous": null,
  "results": [...]
}
```

---

## 🔵 LEVEL 6: FILTERING & ORDERING

```python
REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend',
        'rest_framework.filters.SearchFilter',
        'rest_framework.filters.OrderingFilter',
    ]
}
```

Example 👇

```
/users/?search=atiar
/users/?ordering=-id
```

---

## 🔴 LEVEL 7: THROTTLING (Rate limit)

```python
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.AnonRateThrottle',
        'rest_framework.throttling.UserRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'anon': '5/min',
        'user': '50/min',
    }
}
```

👉 DDOS protection

---

## 🔴 LEVEL 8: VERSIONING (Pro API)

```python
REST_FRAMEWORK = {
    'DEFAULT_VERSIONING_CLASS':
        'rest_framework.versioning.URLPathVersioning',
}
```

URL 👇

```
/api/v1/users/
/api/v2/users/
```

---

## ⚫ LEVEL 9: CUSTOM GLOBAL EXCEPTION HANDLER (PRO)

```python
REST_FRAMEWORK = {
    'EXCEPTION_HANDLER':
        'core.exceptions.custom_exception_handler',
}
```

```python
def custom_exception_handler(exc, context):
    response = exception_handler(exc, context)
    if response:
        response.data['status'] = False
    return response
```

---

## ⚫ LEVEL 10: SETTINGS PRIORITY (Very important 🔥)

```
View-level >
APIView >
Global REST_FRAMEWORK
```

---

## 🧩 COMPLETE LEARNING SUMMARY

| Level    | What you master      |
| -------- | -------------------- |
| Beginner | APIView, Response    |
| Mid      | Auth, Permission     |
| Advanced | Token, Pagination    |
| Pro      | Throttle, Versioning |

---

## 🎯 DRF MASTER CHECKLIST

তুমি যদি এগুলো বুঝো → তুমি **DRF ready** ✔️

* Authentication vs Permission
* Global vs View settings
* Stateless auth
* Pagination response
* Throttling logic

---

চাও তো next আমি দিতে পারি 👇
🔥 **DRF settings MCQ (interview style)**
🔥 **Common mistakes + debugging**
🔥 **DRF flow diagram (request → response)**

বল 👉 কোনটা চাই 😄
Yess 🔥 এখন আমরা **DRF-এর সবচেয়ে dangerous জিনিস** শিখবো
👉 **Common mistakes + debugging mindset**
এইগুলো জানলে তুমি 80% DRF bug নিজেই ধরতে পারবে।

---

# 🚨 DRF Common Mistakes + Debugging (Beginner → Pro)

---

## 🟥 1. “Why API open for everyone?” 😵

### ❌ Mistake

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.AllowAny',
    ]
}
```

### 😬 Problem

সব API public হয়ে গেছে

### ✅ Fix

```python
'DEFAULT_PERMISSION_CLASSES': [
    'rest_framework.permissions.IsAuthenticated',
]
```

### 🧠 Debug tip

Check করো:

```python
print(self.permission_classes)
```

---

## 🟥 2. TokenAuthentication but still 401 ❌

### ❌ Mistake

Header ভুল

```text
Authorization: Bearer token123
```

### ✅ Correct

```text
Authorization: Token token123
```

### 🧠 Debug

```python
print(request.user)
print(request.auth)
```

---

## 🟥 3. Authentication class defined but not working

### ❌ Mistake

```python
authentication_classes = TokenAuthentication   # ❌
```

### ✅ Fix

```python
authentication_classes = [TokenAuthentication]
```

🧠 DRF always expects **list**

---

## 🟥 4. Permission denied even after login

### ❌ Reason

SessionAuthentication + CSRF

### ❌ Code

```python
SessionAuthentication
```

### ✅ Fix (API only)

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

---

## 🟥 5. POST works in Postman but not browser 🤯

### ❌ Cause

CSRF token missing

### ✅ Fix

Use:

* TokenAuthentication
* or add CSRF token
* or test via Postman

---

## 🟥 6. Browsable API suddenly gone 😱

### ❌ Mistake

```python
'DEFAULT_RENDERER_CLASSES': [
    'rest_framework.renderers.JSONRenderer',
]
```

### ✅ Fix (dev only)

```python
'DEFAULT_RENDERER_CLASSES': [
    'rest_framework.renderers.JSONRenderer',
    'rest_framework.renderers.BrowsableAPIRenderer',
]
```

---

## 🟥 7. Pagination not working

### ❌ Mistake

```python
PAGE_SIZE = 10
```

### 😬 Nothing happens

### ✅ Fix

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS':
        'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10,
}
```

---

## 🟥 8. Throttling never triggers

### ❌ Mistake

Only rate defined

```python
'DEFAULT_THROTTLE_RATES': {
    'anon': '5/min'
}
```

### ✅ Fix

```python
'DEFAULT_THROTTLE_CLASSES': [
    'rest_framework.throttling.AnonRateThrottle',
]
```

🧠 Class + Rate → both required

---

## 🟥 9. Custom permission not applied

### ❌ Mistake

```python
class MyPermission:
    pass
```

### ✅ Fix

```python
from rest_framework.permissions import BasePermission

class MyPermission(BasePermission):
    def has_permission(self, request, view):
        return True
```

---

## 🟥 10. View-level settings not working

### ❌ Mistake

```python
class MyAPI(APIView):
    permission_classes = IsAuthenticated   # ❌
```

### ✅ Fix

```python
permission_classes = [IsAuthenticated]
```

🧠 Again: **list required**

---

## 🟥 11. “Why request.data empty?” 🤔

### ❌ Cause

Wrong parser

### ✅ Fix

```python
'DEFAULT_PARSER_CLASSES': [
    'rest_framework.parsers.JSONParser',
]
```

Or send correct `Content-Type: application/json`

---

## 🟥 12. Global setting not applying 😵‍💫

### ❌ Cause

View overrides global

### 🧠 Rule (Very Important)

```
View-level >
APIView >
Global REST_FRAMEWORK
```

---

## 🟥 13. 403 Forbidden vs 401 Unauthorized confusion

| Code | Meaning                     |
| ---- | --------------------------- |
| 401  | Not logged in               |
| 403  | Logged in but no permission |

🧠 Debug:

```python
print(request.user.is_authenticated)
```

---

## 🟥 14. API slow / hanging

### ❌ Common cause

* Large queryset
* No pagination
* Serializer N+1 issue

### ✅ Debug

```python
print(queryset.query)
```

Use:

```python
select_related()
prefetch_related()
```

---

## 🧰 DRF DEBUGGING CHECKLIST (SAVE THIS 🔥)

When API fails → check in this order:

1️⃣ URL mapped correctly?
2️⃣ View reached? (`print("here")`)
3️⃣ Authentication ok? (`request.user`)
4️⃣ Permission blocking?
5️⃣ Serializer valid? (`serializer.errors`)
6️⃣ Headers correct?
7️⃣ Settings overridden?

---

## 🧠 PRO DEBUGGING HABITS

✔️ Always check `request.user`
✔️ Print `request.auth`
✔️ Test with Postman
✔️ Keep Browsable API in dev
✔️ Read error message fully (DRF error is helpful!)

---

## 🎯 If you understand all this…

তুমি **DRF Intermediate+** already 💪

চাও তো next আমি দিতে পারি 👇
🔥 **DRF request–response lifecycle diagram**
🔥 **Interview Q&A (real company level)**
🔥 **Mini practice problems (spot the bug)**

বল 👉 কোনটা চাই 😄


---------
Nice question 👍
**Browsable API** বুঝলে DRF অনেক easy লাগে।

---

## 🌐 Browsable API কী?

**Browsable API** হলো
👉 DRF-এর একটা **web-based UI**
👉 Browser এ গিয়ে API **দেখা, test করা, POST/PUT করা** যায়
👉 Postman ছাড়াই API interact করা যায়

Basically:

> **API + HTML UI = Browsable API**

---

## 🧠 Without Browsable API (Normal API)

Browser এ গেলে দেখবে 👇

```json
{
  "id": 1,
  "name": "Test"
}
```

Only JSON
❌ Click করা যায় না
❌ Form নেই

---

## 🧠 With Browsable API

Browser এ গেলে দেখবে 👇

* GET / POST button
* HTML form
* Login / Logout
* Field validation error
* Serializer structure

📌 একদম **Django admin এর মতো**, কিন্তু API এর জন্য

---

## 🔧 Browsable API enable কিভাবে?

### 1️⃣ Default (DRF default ON)

```python
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
        'rest_framework.renderers.BrowsableAPIRenderer',
    ]
}
```

👉 এটা থাকলে Browsable API কাজ করবে

---

## ❌ Browsable API disable করলে কী হয়?

```python
'DEFAULT_RENDERER_CLASSES': [
    'rest_framework.renderers.JSONRenderer',
]
```

✔️ Faster
✔️ Secure (production)
❌ No UI

---

## 🔐 Authentication + Browsable API

Browsable API তে:

* Login form আসে
* SessionAuthentication use করে
* CSRF required

👉 TokenAuthentication দিলে login form নাই
👉 Header manually দিতে হয়

---

## 🧪 Example

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class TestAPI(APIView):
    def post(self, request):
        return Response(request.data)
```

Browsable API তে:

* Form auto generate হবে
* Field name auto show করবে

---

## 🧠 Real use case

### ✅ Use Browsable API when:

✔️ Learning DRF
✔️ Debugging
✔️ Backend dev testing
✔️ Serializer structure বুঝতে

### ❌ Avoid in:

❌ Production
❌ Public API

---

## ⚠️ Common confusion

❓ “Browsable API থাকলে কি frontend দরকার নাই?”

❌ না
Browsable API = **Dev tool**
Frontend = **User UI**

---

## 🧠 Pro tip 🔥

Development:

```python
DEBUG = True
BrowsableAPIRenderer ON
```

Production:

```python
DEBUG = False
JSONRenderer only
```

---

## 🧩 One line summary

> **Browsable API = DRF-এর built-in Postman + UI**

---


## ❓ `JSONRenderer` কি mandatory?

### ❌ Mandatory না

Browsable API **একাই** কাজ করতে পারে

```python
DEFAULT_RENDERER_CLASSES = [
    'rest_framework.renderers.BrowsableAPIRenderer',
]
```

✔️ Browser এ UI দেখাবে
✔️ GET / POST কাজ করবে
✔️ Response HTML হবে (browser-friendly)

---

## 🤔 তাহলে `JSONRenderer` কেন ব্যবহার করি?

### 1️⃣ API client (Postman, frontend) এর জন্য

Frontend / mobile app **JSON expect করে**

### 2️⃣ Content negotiation এর জন্য

Browser → HTML
Postman → JSON

```python
DEFAULT_RENDERER_CLASSES = [
    'rest_framework.renderers.JSONRenderer',
    'rest_framework.renderers.BrowsableAPIRenderer',
]
```

👉 Best of both worlds

---

## 🧪 Comparison

| Setup                     | Browser | Postman |
| ------------------------- | ------- | ------- |
| Only BrowsableAPIRenderer | UI      | ❌ HTML  |
| Only JSONRenderer         | ❌ UI    | ✅ JSON  |
| Both                      | ✅ UI    | ✅ JSON  |

---

## ⚠️ Real-world rule (important 🔥)

### 🔹 Development

```python
JSONRenderer + BrowsableAPIRenderer
```

### 🔹 Production

```python
JSONRenderer only
```

👉 Browsable API dev tool
👉 JSONRenderer = actual API

---

## 🧠 Pro tip (interview answer)

❓ *“Is JSONRenderer required for Browsable API?”*

✔️ **No**
✔️ Browsable API works independently
✔️ JSONRenderer is for API consumers

---

## 🧩 One-line summary

> **Browsable API চালাতে JSONRenderer লাগেই না**
> **API use করতে JSONRenderer দরকার**


-----
Cool 👍
চল **আরেকটা important DRF setting** শিখি — যেগুলো beginner রা কম জানে কিন্তু **real-world + interview** এ কাজে লাগে।

---

# 🔧 Another DRF Settings (Very Useful)

## 1️⃣ `DEFAULT_SCHEMA_CLASS` (API documentation)

👉 DRF কীভাবে **API structure describe** করবে

```python
REST_FRAMEWORK = {
    'DEFAULT_SCHEMA_CLASS': 
        'rest_framework.schemas.openapi.AutoSchema',
}
```

### কেন দরকার?

* Swagger / OpenAPI
* API contract বুঝতে
* Frontend team এর জন্য

🧠 Without this → docs incomplete হতে পারে

---

## 2️⃣ `DATETIME_FORMAT` (response format control)

### ❌ Default

```json
"created_at": "2026-01-28T12:45:22.123456Z"
```

### ✅ Custom

```python
REST_FRAMEWORK = {
    'DATETIME_FORMAT': "%Y-%m-%d %H:%M:%S"
}
```

Response 👇

```json
"created_at": "2026-01-28 12:45:22"
```

🔥 খুব common frontend request

---

## 3️⃣ `DEFAULT_CONTENT_NEGOTIATION_CLASS`

DRF কীভাবে decide করবে
👉 JSON নাকি HTML?

```python
REST_FRAMEWORK = {
    'DEFAULT_CONTENT_NEGOTIATION_CLASS':
        'rest_framework.negotiation.DefaultContentNegotiation',
}
```

🧠 Browser → HTML
🧠 API client → JSON

👉 Normally change করা লাগে না
(interview knowledge)

---

## 4️⃣ `UNAUTHENTICATED_USER`

Anonymous user কে কীভাবে represent করবে

```python
REST_FRAMEWORK = {
    'UNAUTHENTICATED_USER': None
}
```

### Effect

```python
request.user  # None
```

❌ Instead of `AnonymousUser`

🔥 Performance sensitive API তে use হয়

---

## 5️⃣ `UNAUTHENTICATED_TOKEN`

```python
REST_FRAMEWORK = {
    'UNAUTHENTICATED_TOKEN': None
}
```

👉 `request.auth` empty থাকবে
👉 Clean logic

---

## 6️⃣ `DEFAULT_METADATA_CLASS`

Browsable API তে
👉 Form field info show করে

```python
REST_FRAMEWORK = {
    'DEFAULT_METADATA_CLASS':
        'rest_framework.metadata.SimpleMetadata',
}
```

Disable করলে 👇

```python
'DEFAULT_METADATA_CLASS': None
```

✔️ Faster
✔️ Less info leak

---

## 7️⃣ `TEST_REQUEST_DEFAULT_FORMAT` (Testing time 🔥)

```python
REST_FRAMEWORK = {
    'TEST_REQUEST_DEFAULT_FORMAT': 'json'
}
```

👉 `APITestCase` এ auto JSON
👉 `.format='json'` লিখতে হয় না

---

## 🧠 Common confusion (important)

❓ “সব setting কি ব্যবহার করতেই হবে?”

❌ না
DRF settings = **toolbox**
👉 প্রয়োজন হলে use
👉 না হলে ignore

---

## 🎯 Pro mindset

তুমি যদি জানো:

* setting কী করে
* কখন use করবো
* কখন avoid করবো

👉 তুমি **DRF Pro direction** এ যাচ্ছো 🔥

---

Perfect 👍
এইটা আসলে **DRF Pro mindset**।
চল clean ভাবে দেই — **setting কী করে / কখন use / কখন avoid** এক জায়গায়।

---

# 🧠 DRF SETTINGS — WHAT / WHEN / WHEN NOT

আমি সবচেয়ে **important settings** গুলো নিলাম (learning + real-world)

---

## 1️⃣ `DEFAULT_AUTHENTICATION_CLASSES`

### 🔹 কী করে

User **কে** সেটা identify করে

### ✅ কখন use করবো

* Login required API
* User-based data

```python
TokenAuthentication
SessionAuthentication
```

### ❌ কখন avoid

* Public API
* Read-only API

---

## 2️⃣ `DEFAULT_PERMISSION_CLASSES`

### 🔹 কী করে

User **কি করতে পারবে** control করে

### ✅ Use when

* Security দরকার
* Role based access

```python
IsAuthenticated
IsAdminUser
```

### ❌ Avoid when

* Open/public API

---

## 3️⃣ `DEFAULT_RENDERER_CLASSES`

### 🔹 কী করে

Response **কোন format এ যাবে** (JSON / HTML)

### ✅ Use

* JSONRenderer → API
* BrowsableAPIRenderer → Learning/debug

```python
JSONRenderer
BrowsableAPIRenderer
```

### ❌ Avoid

* Production এ Browsable API

---

## 4️⃣ `DEFAULT_PARSER_CLASSES`

### 🔹 কী করে

Request **কোন format এ আসবে**

### ✅ Use

* JSON data
* File upload

```python
JSONParser
MultiPartParser
```

### ❌ Avoid

* Unnecessary parser (security risk)

---

## 5️⃣ `DEFAULT_PAGINATION_CLASS`

### 🔹 কী করে

Large data **page by page** পাঠায়

### ✅ Use

* List API
* Big dataset

### ❌ Avoid

* Small static data

---

## 6️⃣ `DEFAULT_FILTER_BACKENDS`

### 🔹 কী করে

Search / filter / ordering enable করে

### ✅ Use

* Search API
* Admin panel API

### ❌ Avoid

* Simple fixed response

---

## 7️⃣ `DEFAULT_THROTTLE_CLASSES`

### 🔹 কী করে

Request rate limit (DDOS protection)

### ✅ Use

* Public API
* Auth API

### ❌ Avoid

* Internal / trusted system

---

## 8️⃣ `DEFAULT_VERSIONING_CLASS`

### 🔹 কী করে

API version manage করে

### ✅ Use

* Long-term API
* Mobile app backend

### ❌ Avoid

* Small project
* One-time API

---

## 9️⃣ `EXCEPTION_HANDLER`

### 🔹 কী করে

Error response customize করে

### ✅ Use

* Unified error format
* Frontend friendly API

### ❌ Avoid

* Beginner phase (confusing)

---

## 🔟 `DEFAULT_SCHEMA_CLASS`

### 🔹 কী করে

API documentation generate করে

### ✅ Use

* Swagger / OpenAPI
* Team project

### ❌ Avoid

* Private internal API

---

## 1️⃣1️⃣ `UNAUTHENTICATED_USER`

### 🔹 কী করে

Anonymous user handle করে

### ✅ Use

* Performance optimize
* Simple logic

### ❌ Avoid

* Permission heavy logic

---

## 1️⃣2️⃣ `TEST_REQUEST_DEFAULT_FORMAT`

### 🔹 কী করে

DRF test easy করে

### ✅ Use

* Automated testing

### ❌ Avoid

* If no tests

---

# 🧠 PRO RULE (সবচেয়ে important)

> ❌ সব setting একসাথে use করবো না
> ✅ Need অনুযায়ী enable করবো

---

## 🧩 SIMPLE DECISION GUIDE

| Situation      | Use           |
| -------------- | ------------- |
| Learning DRF   | Browsable API |
| Production API | JSON only     |
| Public API     | Throttle      |
| Big data       | Pagination    |
| Team project   | Schema        |
| Testing        | Test format   |

---

## 🎯 Interview-ready one-liner

> “DRF settings are optional tools.
> I enable them based on **security, scale, and consumers**.”

---

তুমি চাইলে next step করতে পারি 👇
🔥 **Security-focused DRF settings**
🔥 **Real-life DRF settings templates**
🔥 **Settings MCQ (interview)**

বল 👉 কোনটা 🔥

---------
🔥 Perfect choice.  
এখন আমরা **DRF Security-focused settings** শিখবো — যেগুলো **real production API** তে লাগে।

আমি এটা **what / why / when / example** format এ দেবো, যাতে মাথায় বসে যায়।

---

# 🔐 SECURITY-FOCUSED DRF SETTINGS (BEGINNER → PRO)

---

## 1️⃣ `DEFAULT_PERMISSION_CLASSES` (FIRST LINE OF DEFENSE)

### 🔹 কী করে

API কে **defaultভাবে secure** করে

### ❌ Insecure (common mistake)

```python
AllowAny
```

### ✅ Secure default

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}
```

### 🧠 Rule

> **Public না হলে → Always IsAuthenticated**

---

## 2️⃣ `DEFAULT_AUTHENTICATION_CLASSES` (WHO ARE YOU?)

### 🔹 Secure choices

```python
TokenAuthentication
JWTAuthentication
```

### ❌ Avoid in pure API

```python
SessionAuthentication
```

👉 CSRF issue  
👉 Browser dependent

### ✅ Recommended

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

---

## 3️⃣ Disable Browsable API in Production

### ❌ Risk

- API structure leak
    
- Field names exposed
    

### ✅ Secure setting

```python
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
    ]
}
```

---

## 4️⃣ Throttling (DDOS + Bruteforce protection)

### 🔹 What it stops

- Login bruteforce
    
- API abuse
    

```python
REST_FRAMEWORK = {
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.AnonRateThrottle',
        'rest_framework.throttling.UserRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'anon': '5/min',
        'user': '60/min',
    }
}
```

🔥 **Must for public APIs**

---

## 5️⃣ Custom Throttle for Login API (PRO)

```python
class LoginAPI(APIView):
    throttle_scope = 'login'
```

```python
'DEFAULT_THROTTLE_RATES': {
    'login': '3/min'
}
```

🧠 Bruteforce protection

---

## 6️⃣ Parser restriction (Attack surface reduce)

### ❌ Bad

```python
DEFAULT_PARSER_CLASSES = ALL
```

### ✅ Good

```python
'DEFAULT_PARSER_CLASSES': [
    'rest_framework.parsers.JSONParser',
]
```

👉 Unknown content-type reject হবে

---

## 7️⃣ File upload security

```python
'DEFAULT_PARSER_CLASSES': [
    'rest_framework.parsers.MultiPartParser',
]
```

✔️ Only when needed  
❌ Never globally if not required

---

## 8️⃣ Custom Exception Handler (Info leak prevent)

### ❌ Default

Too much internal info

### ✅ Secure

```python
REST_FRAMEWORK = {
    'EXCEPTION_HANDLER':
        'core.exceptions.custom_exception_handler',
}
```

```python
def custom_exception_handler(exc, context):
    response = exception_handler(exc, context)
    if response:
        response.data = {
            "success": False,
            "message": "Invalid request"
        }
    return response
```

---

## 9️⃣ Hide metadata (Browsable API hardening)

```python
'DEFAULT_METADATA_CLASS': None
```

👉 Form field info hide  
👉 Less info leak

---

## 🔟 `UNAUTHENTICATED_USER = None`

```python
REST_FRAMEWORK = {
    'UNAUTHENTICATED_USER': None
}
```

### Benefit

- Faster
    
- Simpler logic
    
- Less anonymous probing
    

---

## 1️⃣1️⃣ Versioning (Breaking change safety)

```python
'DEFAULT_VERSIONING_CLASS':
    'rest_framework.versioning.URLPathVersioning'
```

👉 Old client break হবে না

---

## 1️⃣2️⃣ CORS (DRF + frontend security)

```bash
pip install django-cors-headers
```

```python
CORS_ALLOWED_ORIGINS = [
    "https://frontend.com",
]
```

❌ Never:

```python
CORS_ALLOW_ALL_ORIGINS = True
```

---

# 🛑 SECURITY ANTI-PATTERNS (Avoid These)

❌ AllowAny globally  
❌ Browsable API in prod  
❌ No throttling  
❌ Open CORS  
❌ Exposing detailed errors  
❌ No auth on POST/DELETE

---

# 🔐 MINIMUM PRODUCTION-SAFE DRF TEMPLATE

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_RENDERER_CLASSES': [
        'rest_framework.renderers.JSONRenderer',
    ],
    'DEFAULT_THROTTLE_CLASSES': [
        'rest_framework.throttling.AnonRateThrottle',
        'rest_framework.throttling.UserRateThrottle',
    ],
    'DEFAULT_THROTTLE_RATES': {
        'anon': '5/min',
        'user': '60/min',
    },
}
```

---

## 🎯 Pro interview line

> “Security in DRF starts from **permissions**, reinforced by  
> **authentication, throttling, renderer restriction, and error control**.”

---

চাও তো next আমরা করতে পারি 👇  
🔥 **DRF security checklist (before deploy)**  
🔥 **JWT vs Token security comparison**  
🔥 **Common security bugs in DRF apps**

বল 👉 কোনটা 🔥

------
🔥 এইটা **very important topic** — real projects + interviews দুটোতেই আসে।
চল **DRF Common Security Bugs** একদম practical ভাবে দেখি: **bug → risk → fix**।

---

# 🚨 Common Security Bugs in DRF Apps

---

## 🟥 1. `AllowAny` globally (MOST DANGEROUS)

### ❌ Bug

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.AllowAny',
    ]
}
```

### ☠️ Risk

* Anyone can POST / DELETE
* Data leak

### ✅ Fix

```python
IsAuthenticated
```

🧠 Rule: **Public না হলে AllowAny না**

---

## 🟥 2. Browsable API enabled in production

### ❌ Bug

```python
BrowsableAPIRenderer enabled
```

### ☠️ Risk

* Field names leak
* Validation rules visible

### ✅ Fix

```python
DEFAULT_RENDERER_CLASSES = [JSONRenderer]
```

---

## 🟥 3. No throttling on auth APIs

### ❌ Bug

Login / OTP / Password reset unlimited

### ☠️ Risk

* Bruteforce
* Credential stuffing

### ✅ Fix

```python
Login scope: 3/min
```

---

## 🟥 4. Open CORS (`*`)

### ❌ Bug

```python
CORS_ALLOW_ALL_ORIGINS = True
```

### ☠️ Risk

* Token hijack
* CSRF-like attacks

### ✅ Fix

Whitelist domains only

---

## 🟥 5. Using `SessionAuthentication` for API

### ❌ Bug

```python
SessionAuthentication
```

### ☠️ Risk

* CSRF issues
* Cookie abuse

### ✅ Fix

```python
Token / JWT Authentication
```

---

## 🟥 6. Detailed error messages exposed

### ❌ Bug

```json
{
  "detail": "User with email test@test.com does not exist"
}
```

### ☠️ Risk

* User enumeration

### ✅ Fix

Generic message

```json
"Invalid credentials"
```

---

## 🟥 7. No object-level permission check

### ❌ Bug

```python
def get(self, request, pk):
    return Model.objects.get(pk=pk)
```

### ☠️ Risk

User A accesses User B data

### ✅ Fix

```python
obj.user == request.user
```

---

## 🟥 8. Missing `IsAuthenticated` on write methods

### ❌ Bug

```python
def post(self, request):
    ...
```

(No permission)

### ☠️ Risk

Anonymous data injection

### ✅ Fix

```python
permission_classes = [IsAuthenticated]
```

---

## 🟥 9. File upload without validation

### ❌ Bug

* No size check
* No extension check

### ☠️ Risk

* Malware upload
* Disk fill attack

### ✅ Fix

* File size limit
* MIME type check

---

## 🟥 10. Using `eval()` / raw SQL with request data

### ❌ Bug

```python
eval(request.data['filter'])
```

### ☠️ Risk

Remote Code Execution

### ✅ Fix

Never trust input

---

## 🟥 11. Token stored in localStorage (frontend)

### ❌ Bug

```js
localStorage.setItem("token", token)
```

### ☠️ Risk

XSS → token steal

### ✅ Fix

* HttpOnly cookies (JWT)
* Short-lived tokens

---

## 🟥 12. No HTTPS in production

### ❌ Bug

HTTP API

### ☠️ Risk

Man-in-the-middle

### ✅ Fix

HTTPS only

---

## 🟥 13. Exposing debug info

### ❌ Bug

```python
DEBUG = True
```

### ☠️ Risk

Stacktrace leak

### ✅ Fix

```python
DEBUG = False
```

---

## 🟥 14. Over-permissive serializer

### ❌ Bug

```python
fields = '__all__'
```

### ☠️ Risk

User edits sensitive fields

### ✅ Fix

Explicit fields

---

## 🟥 15. No API versioning

### ❌ Bug

Breaking changes

### ☠️ Risk

Old client break → security bypass

### ✅ Fix

Use versioning

---

# 🛡️ SECURITY REVIEW CHECKLIST (Before Deploy)

✔️ IsAuthenticated default
✔️ No Browsable API
✔️ Throttling enabled
✔️ CORS restricted
✔️ HTTPS
✔️ Debug False
✔️ Serializer fields limited
✔️ Object-level permission

---

## 🎯 Interview killer line 🔥

> “Most DRF security bugs come from **misconfiguration**, not framework flaws.”

---

চাও তো next level যেতে পারি 👇
🔥 **Secure DRF project template**
🔥 **JWT security deep dive**
🔥 **Security audit checklist PDF-style**

বল 👉 কোনটা 🚀

------------
