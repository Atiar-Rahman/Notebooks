হ্যাঁ। DRF-এ throttle basicভাবে জানলেই শুরু করা যায়, কিন্তু **production-level project** করতে গেলে কয়েকটা advanced concept জানা বেশ কাজে লাগে।

### যেগুলো ধাপে ধাপে শিখতে পারো

1. **Custom Throttle**
    
    - নিজের logic অনুযায়ী request limit করা
        
    - যেমন: নির্দিষ্ট API-র জন্য আলাদা limit
        
2. **Scoped Throttling**
    
    - `user`, `anon`, `login`, `search`, `upload`—প্রতিটির আলাদা rate
        
    - `scope = "login"` ব্যবহার করা
        
3. **Custom Throttle Rate**
    
    - `10/minute`
        
    - `100/hour`
        
    - `1000/day`
        
    - বিভিন্ন endpoint অনুযায়ী আলাদা rate
        
4. **Authentication + Throttling**
    
    - Session authentication
        
    - Token authentication
        
    - JWT
        
    - authenticated বনাম anonymous user-এর আলাদা limits
        
5. **Caching কীভাবে throttle-এর সাথে কাজ করে**
    
    - DRF throttle সাধারণত Django cache ব্যবহার করে
        
    - Redis ব্যবহার করলে production environment-এ কীভাবে setup করতে হয় সেটা জানা ভালো
        
6. **Rate Limiting Strategy**
    
    - Login → খুব strict
        
    - Search → মাঝারি
        
    - সাধারণ GET API → তুলনামূলক বেশি
        
    - Admin/expensive API → আলাদা limit
        
7. **Throttling-এর limitation**
    
    - DRF throttling মূলত application-level protection
        
    - এটা একাই DDoS protection-এর replacement না
        
    - বড় production system-এ Nginx/API gateway/cloud-level rate limiting-ও থাকতে পারে
        
8. **429 response handling**
    
    - client কীভাবে `429 Too Many Requests` handle করবে
        
    - `Retry-After` ইত্যাদি সম্পর্কে ধারণা
        

### DRF শেখার জন্য একটা ভালো progression

```text
DRF Basics
   ↓
Serializers
   ↓
APIView / GenericAPIView
   ↓
ViewSets + Routers
   ↓
Authentication
   ↓
Permissions
   ↓
Filtering / Searching / Ordering
   ↓
Pagination
   ↓
Throttling
   ↓
Caching + Redis
   ↓
Custom Permissions / Throttles
   ↓
Testing
   ↓
Production Deployment
```

**বিশেষ করে `Authentication + Permission + Throttling + Caching/Redis`—এই চারটা ভালোভাবে বুঝলে DRF-এর production-side অনেক শক্ত হয়ে যাবে।**

---
অবশ্যই। আমরা **DRF Throttling**-কে ৪টা lesson-এ ভাগ করে, প্রতিটাতে বাস্তব implementation করব।

### Course Structure

| Lesson | Topic                    | আমরা কী বানাব                                       |
| ------ | ------------------------ | --------------------------------------------------- |
| 1      | Basic Throttling         | Anonymous + Authenticated rate limit                |
| 2      | Scoped Throttling        | Login/Search/API অনুযায়ী আলাদা limit                |
| 3      | Custom Throttle          | নিজের business logic দিয়ে throttle                  |
| 4      | Redis + Production Setup | Redis-backed throttling + production considerations |

প্রতিটি lesson-এ **code → configuration → API test → কেন কাজ করছে সেটা** দেখব।

## Lesson 1 — Basic Throttling

ধরি আমাদের একটা simple API আছে:

```python
# views.py

from rest_framework.views import APIView
from rest_framework.response import Response


class ProductView(APIView):

    def get(self, request):
        return Response({
            "message": "Product list"
        })
```

এখন আমরা চাই:

* Anonymous user → `5 requests/minute`
* Logged-in user → `20 requests/minute`

### Step 1 — `settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "5/minute",
        "user": "20/minute",
    },
}
```

এখানে:

```text
AnonRateThrottle
       ↓
Anonymous user কে track করবে

UserRateThrottle
       ↓
Authenticated user কে track করবে
```

### Step 2 — কোনো view-তে আলাদাভাবে কিছু করার দরকার নেই

কারণ আমরা `DEFAULT_THROTTLE_CLASSES` দিয়েছি।

```python
class ProductView(APIView):

    def get(self, request):
        return Response({
            "message": "Product list"
        })
```

Request করলে:

```text
GET /api/products/
```

Anonymous অবস্থায় প্রথম ৫টা request allowed হবে।

৬ নম্বর request-এর ক্ষেত্রে DRF:

```text
HTTP 429 Too Many Requests
```

দেবে।

### Step 3 — Authentication থাকলে

ধরি user login করেছে:

```text
Authorization: Bearer <token>
```

তাহলে DRF তাকে anonymous হিসেবে নয়, authenticated user হিসেবে ধরবে।

তার limit হবে:

```text
20 requests / minute
```

অর্থাৎ:

```text
Anonymous
    ↓
5/minute

Authenticated
    ↓
20/minute
```

### Step 4 — Test করার জন্য

Postman/Thunder Client থেকে একই API বারবার call করো:

```text
GET http://127.0.0.1:8000/api/products/
```

প্রথম ৫টা:

```text
200 OK
```

তারপর:

```text
429 Too Many Requests
```

### একটা গুরুত্বপূর্ণ বিষয়

DRF-এর built-in throttling **security-এর একমাত্র layer না**। এটা API request rate control করার জন্য। Production application-এ Redis/cache এবং প্রয়োজনে reverse proxy/API gateway-level rate limiting-ও ব্যবহার করা হয়।

---

## Lesson 1-এর concept

আজকে মূলত এই ৩টা জিনিস বুঝলেই হবে:

```text
AnonRateThrottle
       ↓
anonymous clients

UserRateThrottle
       ↓
authenticated users

DEFAULT_THROTTLE_RATES
       ↓
কত request allowed
```

পরের lesson-এ আমরা **Scoped Throttling** করব—যেমন:

```text
/login/     → 5/minute
/search/    → 30/minute
/products/  → 100/minute
```

এটা real project-এ অনেক বেশি useful।

---
## Lesson 1 — DRF Basic Throttling

এই lesson-এ আমরা একদম শুরু থেকে একটা ছোট DRF project-এ **Anonymous + Authenticated user throttling** implement করব।

### আমরা যা বানাব

```text
Anonymous user       → 5 requests / minute
Authenticated user   → 20 requests / minute
Limit শেষ            → 429 Too Many Requests
```

### 1. DRF install

```bash
pip install djangorestframework
```

`settings.py`:

```python
INSTALLED_APPS = [
    # ...
    "rest_framework",
]
```

---

### 2. একটা API বানাও

`views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response


class ProductView(APIView):

    def get(self, request):
        return Response({
            "message": "Product list"
        })
```

`urls.py`

```python
from django.urls import path
from .views import ProductView

urlpatterns = [
    path("products/", ProductView.as_view()),
]
```

এখন:

```text
GET /products/
```

করলে:

```json
{
    "message": "Product list"
}
```

পাবে।

---

## 3. এখন Throttling enable করি

`settings.py`-তে:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "5/minute",
        "user": "20/minute",
    },
}
```

এখানে সবচেয়ে গুরুত্বপূর্ণ অংশ:

```python
"DEFAULT_THROTTLE_CLASSES": [
    "rest_framework.throttling.AnonRateThrottle",
    "rest_framework.throttling.UserRateThrottle",
]
```

এর অর্থ DRF globally এই দুই ধরনের throttle ব্যবহার করবে।

### `AnonRateThrottle`

যে user login করেনি:

```text
Anonymous
    ↓
5 requests / minute
```

### `UserRateThrottle`

যে user authenticated:

```text
Authenticated
    ↓
20 requests / minute
```

---

## 4. এখন test করি

Server চালাও:

```bash
python manage.py runserver
```

তারপর Postman/Thunder Client দিয়ে:

```http
GET http://127.0.0.1:8000/products/
```

Anonymous অবস্থায় request পাঠাও।

প্রথম request:

```text
200 OK
```

এভাবে ৫ বার:

```text
Request 1 → 200
Request 2 → 200
Request 3 → 200
Request 4 → 200
Request 5 → 200
```

এরপর আবার request:

```text
Request 6 → 429 Too Many Requests
```

Response সাধারণত এরকম হবে:

```json
{
    "detail": "Request was throttled. Expected available in 60 seconds."
}
```

---

## 5. এখানে একটা গুরুত্বপূর্ণ প্রশ্ন

**DRF কীভাবে বুঝল যে এই client ৫টা request করে ফেলেছে?**

এখানে আসে **cache**।

Simplifiedভাবে:

```text
Client
  ↓
GET /products/
  ↓
DRF Throttle
  ↓
Cache-এ request information check
  ↓
Allowed?
 ├── Yes → API execute
 └── No  → 429
```

অর্থাৎ throttle request-এর count/state রাখার জন্য Django cache mechanism ব্যবহার করে।

Development-এ Django-এর default cache দিয়ে শুরু করা যায়। Production-এ Redis-এর মতো shared cache ব্যবহার করা বেশি উপযোগী।

---

## 6. View-এর মধ্যে কিছু লিখতে হলো না কেন?

কারণ আমরা global configuration দিয়েছি:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],
}
```

তাই DRF-এর API views-গুলোতে defaultভাবেই throttle apply হবে।

তুমি চাইলে নির্দিষ্ট view-তে override-ও করতে পারো:

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.throttling import UserRateThrottle


class ProductView(APIView):

    throttle_classes = [UserRateThrottle]

    def get(self, request):
        return Response({
            "message": "Product list"
        })
```

এক্ষেত্রে ওই view-তে শুধু `UserRateThrottle` থাকবে।

---

## 7. পুরো flow একবার দেখো

```text
                    API Request
                         │
                         ▼
                 ┌──────────────┐
                 │ DRF Throttle │
                 └──────┬───────┘
                        │
              ┌─────────┴─────────┐
              ▼                   ▼
        Anonymous             Authenticated
              │                   │
              ▼                   ▼
          5/minute             20/minute
              │                   │
              └─────────┬─────────┘
                        ▼
                   Limit আছে?
                   /        \
                 Yes         No
                  │           │
                  ▼           ▼
              API runs      429
```

### আজকের মূল জিনিস

তোমার মাথায় এই ৪টা জিনিস পরিষ্কার থাকা উচিত:

```python
AnonRateThrottle
```

→ anonymous user-এর rate control

```python
UserRateThrottle
```

→ authenticated user-এর rate control

```python
DEFAULT_THROTTLE_RATES
```

→ কত request allowed হবে

```text
429 Too Many Requests
```

→ limit exceed করেছে

**Lesson 2-তে আমরা `Scoped Throttling` করব**, যেখানে একই project-এ আলাদা API-র আলাদা limit দিতে পারবে—যেমন login `5/minute`, search `30/minute`, আর products `100/minute`।


---
# Lesson 2 — Scoped Throttling

Lesson 1-এ আমরা দেখেছি:

```text
Anonymous → 5/minute
User      → 20/minute
```

কিন্তু real project-এ সব API-র জন্য একই limit রাখা ভালো না।

ধরো:

```text
/login/      → 5/minute
/search/     → 30/minute
/products/   → 100/minute
```

এখানেই **Scoped Throttling** কাজে আসে।

---

## 1. Scope কী?

Scope হচ্ছে একটা **নাম**, যেটা দিয়ে আমরা নির্দিষ্ট throttle rate identify করি।

যেমন:

```python
scope = "login"
```

তারপর `settings.py`-তে:

```python
"login": "5/minute"
```

অর্থাৎ:

```text
scope = login
       ↓
5 requests / minute
```

---

# 2. প্রথমে Custom Scoped Throttle তৈরি করি

`throttles.py` নামে file বানাও:

```python
from rest_framework.throttling import UserRateThrottle


class LoginThrottle(UserRateThrottle):
    scope = "login"


class SearchThrottle(UserRateThrottle):
    scope = "search"


class ProductThrottle(UserRateThrottle):
    scope = "product"
```

এখন আমাদের ৩টা throttle:

```text
LoginThrottle
     ↓
login scope

SearchThrottle
     ↓
search scope

ProductThrottle
     ↓
product scope
```

---

# 3. `settings.py` configure করি

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_RATES": {
        "login": "5/minute",
        "search": "30/minute",
        "product": "100/minute",
    },
}
```

এখানে খেয়াল করো:

```python
"login": "5/minute"
```

এটা `LoginThrottle`-এর:

```python
scope = "login"
```

এর সাথে match করছে।

একইভাবে:

```python
scope = "search"
```

এর জন্য:

```python
"search": "30/minute"
```

---

# 4. Login API-তে ব্যবহার করি

ধরি:

```python
# views.py

from rest_framework.views import APIView
from rest_framework.response import Response

from .throttles import LoginThrottle


class LoginView(APIView):

    throttle_classes = [LoginThrottle]

    def post(self, request):
        return Response({
            "message": "Login successful"
        })
```

এখন:

```text
POST /login/
```

করলে `LoginThrottle` কাজ করবে।

Limit:

```text
5 requests / minute
```

---

# 5. Search API

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .throttles import SearchThrottle


class SearchView(APIView):

    throttle_classes = [SearchThrottle]

    def get(self, request):
        return Response({
            "results": []
        })
```

এখন:

```text
GET /search/
```

এর limit:

```text
30 requests / minute
```

---

# 6. Product API

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .throttles import ProductThrottle


class ProductView(APIView):

    throttle_classes = [ProductThrottle]

    def get(self, request):
        return Response({
            "products": []
        })
```

Limit:

```text
100 requests / minute
```

---

# 7. পুরো structure

এখন project দেখতে এরকম হতে পারে:

```text
myproject/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   └── urls.py
│
└── api/
    ├── views.py
    ├── throttles.py
    └── urls.py
```

### `throttles.py`

```python
from rest_framework.throttling import UserRateThrottle


class LoginThrottle(UserRateThrottle):
    scope = "login"


class SearchThrottle(UserRateThrottle):
    scope = "search"


class ProductThrottle(UserRateThrottle):
    scope = "product"
```

### `settings.py`

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_RATES": {
        "login": "5/minute",
        "search": "30/minute",
        "product": "100/minute",
    },
}
```

---

# 8. একটা গুরুত্বপূর্ণ ব্যাপার

তুমি হয়তো ভাবছ:

> `UserRateThrottle` তো authenticated user-এর জন্য। তাহলে anonymous user কী করবে?

ঠিক ধরেছ।

`UserRateThrottle` মূলত authenticated users-এর জন্য ব্যবহৃত হয়। Login endpoint-এ anonymous users থাকলে বাস্তবে login throttling-এর জন্য `AnonRateThrottle`-ভিত্তিক custom throttle ব্যবহার করা বেশি উপযুক্ত হতে পারে।

যেমন:

```python
from rest_framework.throttling import AnonRateThrottle


class LoginThrottle(AnonRateThrottle):
    scope = "login"
```

তারপর:

```python
class LoginView(APIView):

    throttle_classes = [LoginThrottle]

    def post(self, request):
        return Response({
            "message": "Login successful"
        })
```

এখন anonymous client-এর জন্য:

```text
/login/
   ↓
LoginThrottle
   ↓
5/minute
```

---

# 9. কেন Login-এ strict throttle?

Login endpoint সাধারণত sensitive endpoint।

ধরো:

```text
POST /login/
```

একজন client যদি খুব দ্রুত অনেক request পাঠায়, তাহলে system-এর ওপর unnecessary load পড়তে পারে এবং credential-guessing attempts-এর মতো abuse হতে পারে।

তাই আমরা রাখতে পারি:

```text
Login     → 5/minute
Search    → 30/minute
Products  → 100/minute
```

এটা একটা **policy example**, universal rule না—তোমার application's traffic ও requirements অনুযায়ী rate ঠিক করতে হবে।

---

# 10. Function-based API হলে?

`@throttle_classes` ব্যবহার করতে পারো:

```python
from rest_framework.decorators import api_view
from rest_framework.decorators import throttle_classes
from rest_framework.response import Response

from .throttles import SearchThrottle


@api_view(["GET"])
@throttle_classes([SearchThrottle])
def search(request):
    return Response({
        "results": []
    })
```

---

# 11. সবচেয়ে important concept

Lesson 1:

```text
UserRateThrottle
        ↓
সব user-এর জন্য একই rate
```

Lesson 2:

```text
                    Scoped Throttling
                           │
             ┌─────────────┼─────────────┐
             ▼             ▼             ▼
           login         search        product
             │             │             │
             ▼             ▼             ▼
         5/minute      30/minute      100/minute
```

অর্থাৎ **একই project-এর বিভিন্ন endpoint-এর জন্য আলাদা rate define করতে পারছি।**

### Lesson 2 শেষে তোমার জানা উচিত

* `scope` কী
* custom throttle class কীভাবে বানাতে হয়
* `DEFAULT_THROTTLE_RATES` কীভাবে scope-এর সাথে কাজ করে
* API অনুযায়ী আলাদা rate কীভাবে দিতে হয়
* anonymous বনাম authenticated throttling-এর পার্থক্য

**Lesson 3-এ আমরা Custom Throttle বানাব**, যেখানে শুধু `5/minute` বা `30/minute` না—নিজের business logic দিয়ে **কে কত request করতে পারবে সেটা dynamically control** করব।


---
# Lesson 3 — Custom Throttle

Lesson 1-এ আমরা built-in throttle দেখেছি, Lesson 2-তে **scope-based throttle** দেখেছি। এবার আমরা নিজের **business logic** দিয়ে throttle তৈরি করব।

ধরো আমাদের requirement:

```text
Normal user → 20 requests/minute
Premium user → 100 requests/minute
Anonymous → 5 requests/minute
```

এখানে একই throttle class-এর behavior user অনুযায়ী বদলাবে। এটাই custom throttle-এর একটা গুরুত্বপূর্ণ use case।

---

## 1. Custom Throttle কীভাবে কাজ করে?

DRF-এর throttle মূলত একটা প্রশ্নের উত্তর দেয়:

```text
"এই request-টা এখন allow করব, নাকি block করব?"
```

Custom throttle-এ আমরা `allow_request()` override করতে পারি।

Basic structure:

```python
from rest_framework.throttling import BaseThrottle


class MyCustomThrottle(BaseThrottle):

    def allow_request(self, request, view):
        # নিজের logic
        return True
```

`True` → request allowed

`False` → request throttled

---

# 2. একটা সহজ Custom Throttle বানাই

ধরো আমরা চাই:

> একই IP থেকে প্রতি মিনিটে সর্বোচ্চ 5টি request।

`throttles.py`:

```python
from rest_framework.throttling import BaseThrottle


class FivePerMinuteThrottle(BaseThrottle):

    def allow_request(self, request, view):
        return True
```

এখন শুধু `True` দিলে সব request allowed হবে। তাই আমাদের request count কোথাও রাখতে হবে।

এখানেই **Django cache** ব্যবহার করব।

---

# 3. Cache ব্যবহার করি

```python
from django.core.cache import cache
from rest_framework.throttling import BaseThrottle


class FivePerMinuteThrottle(BaseThrottle):

    def allow_request(self, request, view):

        ip = self.get_ident(request)

        key = f"throttle:{ip}"

        requests = cache.get(key, 0)

        if requests >= 5:
            return False

        cache.set(key, requests + 1, timeout=60)

        return True
```

এখন flow:

```text
Request
   ↓
IP বের করি
   ↓
Cache থেকে count দেখি
   ↓
count >= 5 ?
   │
   ├── Yes → False → 429
   │
   └── No
        ↓
     count + 1
        ↓
      Allow
```

---

# 4. View-তে ব্যবহার

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .throttles import FivePerMinuteThrottle


class ProductView(APIView):

    throttle_classes = [FivePerMinuteThrottle]

    def get(self, request):
        return Response({
            "message": "Products"
        })
```

এখন:

```text
GET /products/
```

একই IP থেকে প্রথম ৫টা request allowed হবে।

৬ নম্বর:

```text
429 Too Many Requests
```

---

# 5. কিন্তু এখানে একটা সমস্যা আছে

উপরের implementation শেখার জন্য ভালো, কিন্তু production-ready না।

কারণ:

```python
requests = cache.get(key, 0)

if requests >= 5:
    return False

cache.set(key, requests + 1, timeout=60)
```

এখানে একাধিক request একই সময়ে এলে race condition হতে পারে।

আরেকটা বিষয় হলো আমরা এখনো `wait()` implement করিনি।

DRF-এর `BaseThrottle`-এ `wait()` method ব্যবহার করে client-কে বলতে পারি কতক্ষণ অপেক্ষা করতে হবে।

---

# 6. `wait()` implement করি

```python
from django.core.cache import cache
from rest_framework.throttling import BaseThrottle


class FivePerMinuteThrottle(BaseThrottle):

    def allow_request(self, request, view):

        ip = self.get_ident(request)

        self.key = f"throttle:{ip}"

        requests = cache.get(self.key, 0)

        if requests >= 5:
            return False

        cache.set(
            self.key,
            requests + 1,
            timeout=60
        )

        return True

    def wait(self):
        return 60
```

এখন DRF `429` response-এর সাথে throttling wait information দিতে পারে।

---

# 7. User অনুযায়ী Dynamic Limit

এবার আরও useful example।

ধরো:

```text
Anonymous → 5/minute
Normal user → 20/minute
Premium user → 100/minute
```

Custom throttle:

```python
from rest_framework.throttling import UserRateThrottle


class PlanBasedThrottle(UserRateThrottle):

    def get_rate(self):
        request = self.request

        if not request.user.is_authenticated:
            return "5/minute"

        if getattr(request.user, "is_premium", False):
            return "100/minute"

        return "20/minute"
```

এখানে:

```text
request.user
     │
     ├── Anonymous
     │      ↓
     │    5/min
     │
     ├── Normal
     │      ↓
     │    20/min
     │
     └── Premium
            ↓
          100/min
```

তারপর:

```python
class ProductView(APIView):

    throttle_classes = [PlanBasedThrottle]

    def get(self, request):
        return Response({
            "message": "Products"
        })
```

---

# 8. একটা গুরুত্বপূর্ণ ব্যাপার

Custom throttle মানেই সবসময় `BaseThrottle` থেকে শুরু করতে হবে—এমন না।

দুইটা common approach আছে:

### Approach A — `UserRateThrottle` extend করা

যখন শুধু rate/identity-এর behavior customize করতে চাও:

```python
class PlanBasedThrottle(UserRateThrottle):
    ...
```

### Approach B — `BaseThrottle` extend করা

যখন completely নিজের throttling logic দরকার:

```python
class MyThrottle(BaseThrottle):
    ...
```

---

# 9. কখন কোনটা ব্যবহার করবে?

```text
Simple rate limit
       ↓
UserRateThrottle
       ↓
ScopedThrottle
```

আর:

```text
Complex business logic
       ↓
Custom UserRateThrottle
       অথবা
Custom BaseThrottle
```

উদাহরণ:

```text
Premium user
    → বেশি limit

Normal user
    → কম limit

Specific endpoint
    → আলাদা limit

Special business rule
    → Custom BaseThrottle
```

---

# 10. Real-world example

ধরো তোমার e-commerce API:

```text
/products/
    → 100/minute

/search/
    → 30/minute

/login/
    → 5/minute

/checkout/
    → 10/minute

/premium-report/
    → Premium: 50/minute
       Normal: 5/minute
```

এখানে scoped throttling + custom throttling একসাথে ব্যবহার করা যায়।

---

## Lesson 3-এর মূল ধারণা

```text
                Custom Throttle
                      │
          ┌───────────┴───────────┐
          │                       │
          ▼                       ▼
 UserRateThrottle             BaseThrottle
          │                       │
          ▼                       ▼
 Dynamic rate              Completely custom
 Premium/Normal             business logic
```

সবচেয়ে গুরুত্বপূর্ণ হলো **throttle শুধু `if count > limit` না**—production implementation-এ cache consistency, concurrent requests, distributed servers এবং Redis-এর মতো shared backend-এর বিষয়ও আসে।

**Lesson 4-এ আমরা এই production side-টাই দেখব: Redis + DRF throttling**, এবং কেন production-এ সাধারণ local memory/cache-এর বদলে shared Redis দরকার হতে পারে।


---
# Lesson 4 — Redis + Production Throttling

এখন আমরা Lesson 1–3-এর সব concept একসাথে নিয়ে **production-style throttling** দেখব।

আজকের লক্ষ্য:

```text
Client
   ↓
Django REST Framework
   ↓
Throttle
   ↓
Redis
   ↓
Request allowed / 429
```

---

## 1. কেন Redis দরকার?

Development-এ Django-এর local cache দিয়ে throttle test করা যায়।

কিন্তু ধরো production-এ তোমার 2টা server আছে:

```text
              Load Balancer
               /          \
              ↓            ↓
          Server 1      Server 2
              \            /
               ↓          ↓
                  Redis
```

একজন user:

```text
Request 1 → Server 1
Request 2 → Server 2
Request 3 → Server 1
```

যদি দুই server-এর আলাদা local cache থাকে, তাহলে তারা request count properly share নাও করতে পারে।

Redis shared state রাখে:

```text
Server 1 ─┐
          ├──→ Redis
Server 2 ─┘
```

তাই distributed application-এ shared cache গুরুত্বপূর্ণ।

---

# 2. Redis install

Local machine-এ Redis চালু থাকতে হবে।

তারপর Python package:

```bash
pip install redis
```

এবং Django Redis cache backend-এর জন্য:

```bash
pip install django-redis
```

---

# 3. `settings.py`-তে Redis configure

```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        },
    },
}
```

এখানে:

```text
127.0.0.1 → Redis server
6379       → Redis default port
/1         → Redis database
```

---

# 4. এখন DRF throttle configure

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "10/minute",
        "user": "100/minute",
    },
}
```

এখন DRF-এর throttle state Django cache ব্যবহার করবে, আর Django cache Redis-এ থাকবে।

Flow:

```text
Request
   ↓
DRF Throttle
   ↓
Django Cache
   ↓
Redis
   ↓
request count
```

---

# 5. Scoped throttling + Redis

ধরো:

```python
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.AnonRateThrottle",
        "rest_framework.throttling.UserRateThrottle",
    ],

    "DEFAULT_THROTTLE_RATES": {
        "anon": "10/minute",
        "user": "100/minute",

        "login": "5/minute",
        "search": "30/minute",
    },
}
```

Custom throttle:

```python
from rest_framework.throttling import AnonRateThrottle
from rest_framework.throttling import UserRateThrottle


class LoginThrottle(AnonRateThrottle):
    scope = "login"


class SearchThrottle(UserRateThrottle):
    scope = "search"
```

এখন:

```text
/login/
   ↓
LoginThrottle
   ↓
Redis
   ↓
5/minute
```

এবং:

```text
/search/
   ↓
SearchThrottle
   ↓
Redis
   ↓
30/minute
```

---

# 6. Production architecture

একটা realistic architecture হতে পারে:

```text
                    Internet
                       │
                       ▼
                Reverse Proxy
                       │
                       ▼
                 Load Balancer
                 /           \
                ▼             ▼
          Django API 1    Django API 2
                │             │
                └──────┬──────┘
                       ▼
                     Redis
                       │
                       ▼
                    Database
```

এখানে Redis-এর কাজ শুধু throttle না। Cache, sessions, Celery ইত্যাদির জন্যও ব্যবহার করা যেতে পারে—তবে configuration অনুযায়ী আলাদা Redis DB/instance বা key namespace ব্যবহার করা ভালো।

---

# 7. একটি important production issue

অনেকে ভাবে:

> "DRF throttle আছে, তাহলে API completely secure."

এটা ঠিক না।

DRF throttling application-level rate control।

এটা **DDoS protection-এর replacement নয়**।

Production system-এ layer থাকতে পারে:

```text
Internet
   ↓
CDN / WAF
   ↓
Reverse Proxy
   ↓
Application
   ↓
DRF Throttle
   ↓
Redis
```

প্রতিটি layer-এর আলাদা উদ্দেশ্য।

---

# 8. Rate কীভাবে ঠিক করবে?

একটা universal number নেই।

ধরো API:

```text
/login/
```

এটা relatively sensitive, তাই comparatively strict limit লাগতে পারে।

অন্যদিকে:

```text
/products/
```

high-traffic read endpoint হতে পারে, তাই বেশি limit লাগতে পারে।

উদাহরণ:

```text
/login/       → 5/minute
/search/      → 30/minute
/products/    → 100/minute
/user/profile → 60/minute
```

এগুলো **example values**, production-এ তোমার traffic এবং requirements অনুযায়ী load testing/monitoring করে নির্ধারণ করবে।

---

# 9. `429` কীভাবে handle করবে?

Throttle limit শেষ হলে client পাবে:

```text
HTTP 429 Too Many Requests
```

Frontend/mobile application-এর উচিত এটাকে properly handle করা।

Conceptually:

```text
API
 ↓
429
 ↓
Client
 ↓
wait
 ↓
retry
```

Blindly খুব দ্রুত retry করা উচিত না, কারণ তাতে throttling আরও বাড়তে পারে।

---

# 10. Redis check করার ধারণা

Redis CLI দিয়ে Redis চলছে কিনা দেখতে পারো:

```bash
redis-cli ping
```

Expected:

```text
PONG
```

এরপর Django application থেকে request পাঠিয়ে Redis-এর activity monitor করা যায়।

Development/debugging-এর সময় এটা useful।

---

# 11. Production checklist

DRF throttling production-এ নেওয়ার আগে:

```text
☑ Redis/shared cache configured
☑ Anonymous rate defined
☑ Authenticated rate defined
☑ Sensitive endpoints have appropriate limits
☑ Scoped throttling where needed
☑ 429 response handled by clients
☑ Load tested
☑ Monitoring/logging configured
☑ Reverse proxy/WAF protection considered
```

---

# 12. পুরো ৪টা Lesson একসাথে

এখন তোমার DRF throttling-এর complete picture:

```text
Lesson 1
Basic Throttling
      ↓
AnonRateThrottle
UserRateThrottle
      ↓
5/minute
20/minute
```

```text
Lesson 2
Scoped Throttling
      ↓
login
search
product
      ↓
different rates
```

```text
Lesson 3
Custom Throttling
      ↓
Business logic
      ↓
Normal / Premium
different limits
```

```text
Lesson 4
Redis + Production
      ↓
Shared cache
      ↓
Multiple Django servers
      ↓
Consistent throttling
```

## এখন তোমার next step

একটা ছোট **DRF E-commerce API** বানিয়ে এই চারটা একসাথে practice করো:

```text
POST /login/
    → 5/minute

GET /products/
    → 100/minute

GET /search/
    → 30/minute

GET /premium-products/
    → Normal: 10/minute
       Premium: 100/minute

Redis
    → throttle state
```

এটা করলে শুধু syntax না, **কখন কোন ধরনের throttle ব্যবহার করতে হয়** সেটাও practically পরিষ্কার হয়ে যাবে।
