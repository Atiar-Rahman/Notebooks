JWT (JSON Web Token) Authentication হলো **stateless authentication system**। Django REST Framework (DRF)-এ এটি API authentication-এর জন্য সবচেয়ে বেশি ব্যবহৃত হয়।

---

# JWT Authentication কী?

ধরুন আপনার একটি E-commerce API আছে।

1. User Login করবে
    
2. Server username/password verify করবে
    
3. Server একটি **JWT Token** দিবে
    
4. এরপর User প্রতিটি API request-এর সাথে Token পাঠাবে
    
5. Server Token verify করবে
    
6. Token valid হলে request allow করবে
    

**Password শুধুমাত্র Login-এর সময় পাঠানো হয়। এরপর শুধু Token ব্যবহার করা হয়।**

---

# JWT Flow

```text
             Login
                │
                ▼
      username + password
                │
                ▼
           Django Server
                │
     Verify username/password
                │
                ▼
      Generate JWT Token
                │
                ▼
          Send Token
                │
────────────────────────────────────

Next Request

Client
   │
Authorization: Bearer <Access Token>
   │
   ▼
Django Server
   │
Verify Token
   │
   ▼
Authenticated User
```

---

# JWT Structure

JWT তিনটি অংশ নিয়ে তৈরি।

```text
xxxxx.yyyyy.zzzzz
```

এগুলো হলো

```
Header
Payload
Signature
```

Example

```
eyJhbGc...
.
eyJ1c2VyX2lk...
.
QwErTyUiOp...
```

---

# 1. Header

Header বলে Token কোন Algorithm দিয়ে তৈরি হয়েছে।

Example

```json
{
   "alg": "HS256",
   "typ": "JWT"
}
```

HS256 = HMAC SHA256

---

# 2. Payload

Payload-এ User Information থাকে।

Example

```json
{
   "user_id": 5,
   "username": "Atiar",
   "exp": 1753200000
}
```

এখানে

```
user_id
username
expire time
```

থাকে।

⚠️ এখানে Password কখনো রাখা হয় না।

---

# 3. Signature

Signature verify করে Token পরিবর্তন হয়েছে কিনা।

```
HMACSHA256(
Header +
Payload,
SECRET_KEY
)
```

যদি কেউ Payload পরিবর্তন করে

```
user_id = 5

↓

user_id = 1
```

তাহলে Signature আর Match করবে না।

Server সাথে সাথে Token Reject করবে।

---

# JWT Types

DRF Simple JWT-এ দুই ধরনের Token থাকে।

## Access Token

Short Time

```
5 minutes
15 minutes
30 minutes
```

Example

```
eyJhbGc....
```

এটা API Call করার জন্য ব্যবহার হয়।

---

## Refresh Token

Long Time

```
1 day
7 days
30 days
```

এটা দিয়ে নতুন Access Token Generate করা হয়।

---

Flow

```text
Login

↓

Access Token (5 min)

Refresh Token (7 days)

↓

Access Expired

↓

Send Refresh Token

↓

New Access Token
```

---

# Why Two Tokens?

ধরুন Access Token ৫ মিনিটের।

৫ মিনিট পরে Expire।

User যদি আবার Login করতে বাধ্য হয় তাহলে বিরক্ত হবে।

তাই

Refresh Token

নতুন Access Token তৈরি করে দেয়।

---

# Installation

```bash
pip install djangorestframework-simplejwt
```

---

settings.py

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]

REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}
```

---

urls.py

```python
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns = [

    path(
        'api/token/',
        TokenObtainPairView.as_view()
    ),

    path(
        'api/token/refresh/',
        TokenRefreshView.as_view()
    ),
]
```

---

# Login Request

POST

```
/api/token/
```

Body

```json
{
   "username":"admin",
   "password":"1234"
}
```

---

Response

```json
{
   "access":"eyJhbGc....",
   "refresh":"eyJhbGc..."
}
```

---

# API Request

Headers

```
Authorization: Bearer eyJhbGc...
```

Example

```http
GET /products/

Authorization: Bearer eyJhbGc....
```

---

# JWT Authentication Class

যখন Request আসে

```http
Authorization:
Bearer eyJ...
```

JWTAuthentication

এই Header পড়ে।

```python
JWTAuthentication.authenticate()
```

এই Method

```
Read Header

↓

Extract Token

↓

Verify Signature

↓

Check Expiration

↓

Load User

↓

request.user
```

---

# request.user

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class Profile(APIView):

    def get(self, request):

        print(request.user)

        return Response({
            "username": request.user.username
        })
```

যদি Token Valid হয়

```
request.user

↓

<User: Atiar>
```

---

# Protect API

```python
from rest_framework.permissions import IsAuthenticated

class OrderView(APIView):

    permission_classes = [
        IsAuthenticated
    ]

    def get(self, request):

        return Response({
            "user": request.user.username
        })
```

Token না থাকলে

```
401 Unauthorized
```

---

# Custom Login Response

```python
from rest_framework_simplejwt.serializers import TokenObtainPairSerializer

class MyTokenSerializer(TokenObtainPairSerializer):

    @classmethod
    def get_token(cls, user):

        token = super().get_token(user)

        token["username"] = user.username
        token["email"] = user.email

        return token
```

View

```python
from rest_framework_simplejwt.views import TokenObtainPairView

class MyTokenView(TokenObtainPairView):
    serializer_class = MyTokenSerializer
```

Response Token-এর Payload-এ অতিরিক্ত তথ্য যুক্ত হবে।

---

# Token Lifetime

```python
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=15),

    "REFRESH_TOKEN_LIFETIME": timedelta(days=7),
}
```

---

# Logout

JWT Stateless হওয়ায় Server সাধারণত Token Store করে না। তাই শুধু Client থেকে Token Delete করলেই অনেক ক্ষেত্রে Logout সম্পন্ন হয়।

যদি Refresh Token-ও Invalid করতে চান, তাহলে Blacklist Feature ব্যবহার করতে পারেন।

```python
INSTALLED_APPS = [
    ...
    'rest_framework_simplejwt.token_blacklist',
]
```

```python
SIMPLE_JWT = {
    "BLACKLIST_AFTER_ROTATION": True,
}
```

Logout View

```python
from rest_framework_simplejwt.tokens import RefreshToken
from rest_framework.views import APIView
from rest_framework.response import Response

class Logout(APIView):

    def post(self, request):

        token = request.data["refresh"]

        RefreshToken(token).blacklist()

        return Response({
            "message":"Logout Successfully"
        })
```

---

# Complete Flow

```text
User
 │
 │ Login(username,password)
 ▼
Django
 │
 │ Verify User
 ▼
Access Token
Refresh Token
 │
 ▼
Store Token (Client)
 │
 ▼
Request
Authorization: Bearer AccessToken
 │
 ▼
JWTAuthentication
 │
Verify Signature
 │
Check Expiration
 │
Find User
 │
▼
request.user
 │
▼
Response
```

---

# JWT-এর সুবিধা

- **Stateless:** Server-এ Session Store করতে হয় না।
    
- **Scalable:** Multiple Server বা Microservices-এ সহজে কাজ করে।
    
- **Cross-platform:** Web, Android, iOS, React, Vue, Flutter—সব জায়গায় ব্যবহার করা যায়।
    
- **Performance:** Session Database Query-এর প্রয়োজন কমে যায়।
    

# JWT-এর সীমাবদ্ধতা

- Access Token চুরি হলে Expire হওয়া পর্যন্ত ব্যবহার করা যেতে পারে।
    
- Logout বা Token Revoke করার জন্য অতিরিক্ত ব্যবস্থা (যেমন Blacklist) দরকার।
    
- Payload Base64-encoded, **encrypted নয়**—তাই Sensitive Data (যেমন Password) Token-এ রাখা উচিত নয়।
    

---

## DRF Interview-এ সাধারণ প্রশ্ন

1. JWT এবং Session Authentication-এর মধ্যে পার্থক্য কী?
    
2. Access Token ও Refresh Token কেন আলাদা?
    
3. JWT Stateless কেন বলা হয়?
    
4. JWT-এর Header, Payload ও Signature কী কাজ করে?
    
5. `request.user` কীভাবে JWT Token থেকে সেট হয়?
    
6. Refresh Token Blacklist কী এবং কখন ব্যবহার করবেন?
    
7. JWT-তে Password বা Sensitive Data কেন রাখা উচিত নয়?
    

যেহেতু আপনি **Django REST Framework** শিখছেন এবং বড় E-commerce/SaaS Project তৈরি করছেন, এরপর আপনার শেখা উচিত:

1. Custom JWT Authentication
    
2. Role-based Authentication (Admin, Teacher, Student)
    
3. Custom Permission Classes
    
4. Refresh Token Rotation
    
5. JWT + React Authentication Flow (Login → Store Token → Auto Refresh → Logout) — যা Full Stack Project-এ সবচেয়ে বেশি ব্যবহৃত হয়।

----------

এগুলো Django REST Framework Interview-এর সবচেয়ে গুরুত্বপূর্ণ JWT Authentication প্রশ্ন। আমি প্রতিটি প্রশ্ন **Definition + Explanation + Example + Interview Answer** ফরম্যাটে দিচ্ছি।

---

# 1. JWT এবং Session Authentication-এর মধ্যে পার্থক্য কী?

## Session Authentication

User Login করার পরে

```text
Client
   │
Username + Password
   │
   ▼
Server
```

Server

```text
Create Session
```

Database অথবা Cache-এ

```text
Session ID
```

Store করে।

Server Client-কে

```text
sessionid=abc123
```

Cookie হিসেবে পাঠায়।

Next Request

```text
Cookie:
sessionid=abc123
```

Server Database-এ Session Check করে।

---

### Flow

```text
Login

↓

Server creates session

↓

Store Session in DB

↓

Browser stores Cookie

↓

Every Request

↓

Cookie Sent

↓

DB Lookup

↓

Authenticated
```

---

## JWT Authentication

Login

↓

Server

```text
Access Token

Refresh Token
```

Generate করে।

Client Token Store করে।

Next Request

```http
Authorization:
Bearer eyJ...
```

Server শুধুমাত্র Token Verify করে।

Database-এ Session Search করে না।

---

## Main Difference

|Session|JWT|
|---|---|
|Stateful|Stateless|
|Session DB লাগে|Session DB লাগে না|
|Cookie use করে|Authorization Header use করে|
|Server Session Store করে|Client Token Store করে|
|Web Apps-এর জন্য ভালো|REST API, Mobile Apps-এর জন্য ভালো|
|Horizontal Scaling কঠিন|Scaling সহজ|

---

## Interview Answer

> Session Authentication-এ Server Session Database-এ Store করে এবং Cookie-এর মাধ্যমে Authenticate করে। JWT Authentication Stateless; Server Session Store করে না। Client Token পাঠায়, Server Token Verify করে।

---

# 2. Access Token ও Refresh Token কেন আলাদা?

Access Token-এর Lifetime ছোট।

Example

```text
15 minutes
```

Refresh Token-এর Lifetime বড়।

Example

```text
7 days
```

---

## কেন?

ধরুন

Access Token

```text
15 minutes
```

Expire হয়ে গেল।

User আবার Login করবে?

না।

সে Refresh Token পাঠাবে।

Server

নতুন Access Token দিবে।

---

### Flow

```text
Login

↓

Access Token (15 min)

↓

Expired

↓

Refresh Token

↓

New Access Token

↓

Continue
```

---

## Security

যদি Access Token Hack হয়

শুধু

```text
15 minutes
```

Use করা যাবে।

Refresh Token আলাদা থাকে।

---

## Interview Answer

> Access Token API Access-এর জন্য এবং ছোট সময় Valid থাকে। Refresh Token নতুন Access Token Generate করার জন্য এবং বেশি সময় Valid থাকে।

---

# 3. JWT Stateless কেন বলা হয়?

Stateless মানে

Server

কোন Session রাখে না।

Example

Request 1

```http
Authorization:
Bearer eyJ...
```

Server

Verify

↓

Response

---

Request 2

```http
Authorization:
Bearer eyJ...
```

Server

আবার Verify।

আগের Request-এর কোনো Information Server Remember করে না।

---

Stateful

```text
Server

↓

Session

↓

Memory
```

Stateless

```text
Server

↓

Nothing Stored
```

---

## Interview Answer

> JWT Stateless কারণ Server কোনো Session Store করে না। প্রতিটি Request স্বাধীনভাবে Token Verify করে Authenticate করে।

---

# 4. JWT-এর Header, Payload ও Signature কী কাজ করে?

## Header

বলবে

```json
{
 "alg":"HS256",
 "typ":"JWT"
}
```

Meaning

```text
Algorithm

Token Type
```

---

## Payload

Contains

```json
{
"user_id":5,
"username":"Atiar",
"exp":17500000
}
```

এখানে

```text
Claims
```

থাকে।

---

## Signature

Generated

```text
Header

+

Payload

+

SECRET_KEY
```

Using

```text
HMAC SHA256
```

যদি Payload Change হয়

Signature Match করবে না।

Server Reject করবে।

---

## Diagram

```text
Header

↓

Payload

↓

SECRET_KEY

↓

Signature
```

---

## Interview Answer

> Header Token-এর Algorithm জানায়, Payload User Claims রাখে, Signature Token Verify করে এবং Tampering Detect করে।

---

# 5. request.user কীভাবে JWT Token থেকে সেট হয়?

Request আসে

```http
Authorization:
Bearer eyJ...
```

↓

JWTAuthentication

```python
authenticate()
```

Method Call হয়।

Step

```text
Read Header

↓

Extract Token

↓

Verify Signature

↓

Check Expiration

↓

Decode Payload

↓

Find User

↓

request.user=user
```

---

Internally

```python
user = User.objects.get(id=payload["user_id"])
```

তারপর

```python
request.user = user
```

---

## Interview Answer

> JWTAuthentication Authorization Header থেকে Token Extract করে, Signature Verify করে, Payload Decode করে User বের করে request.user সেট করে।

---

# 6. Refresh Token Blacklist কী?

Normally

Refresh Token

Expire না হওয়া পর্যন্ত Valid থাকে।

কিন্তু

User Logout করল।

তবুও

Refresh Token থাকলে

নতুন Access Token Generate করা যাবে।

এটা Problem।

---

Solution

Blacklist

Logout

↓

Refresh Token

↓

Blacklist Table

↓

Store

↓

Next Time

↓

Rejected

---

Example

```python
RefreshToken(token).blacklist()
```

---

Database

```text
OutstandingToken

BlacklistedToken
```

---

## কখন ব্যবহার করবেন?

✔ Logout

✔ Password Change

✔ Account Disable

✔ Token Compromised

---

## Interview Answer

> Blacklist Refresh Token-কে Invalid করে দেয় যাতে Logout-এর পরে অথবা Token Leak হলে আর নতুন Access Token Generate করা না যায়।

---

# 7. JWT-তে Password বা Sensitive Data কেন রাখা উচিত নয়?

JWT

Encrypted না।

Base64 Encoded।

Example

```text
Header.Payload.Signature
```

Payload Decode করা যায়।

Example

```json
{
"user_id":5,
"password":"123456"
}
```

Anyone

Decode করতে পারবে।

---

Safe

```json
{
"user_id":5,
"username":"Atiar"
}
```

---

Unsafe

```json
{
"password":"abcd",
"credit_card":"1234",
"otp":"5555"
}
```

---

## Interview Answer

> JWT Payload Base64 Encoded, Encrypted নয়। তাই Password, OTP, Credit Card Number বা Sensitive Information Token-এ রাখা উচিত নয়।

---

# 8. Custom JWT Authentication কী?

Default JWTAuthentication-এর পরিবর্তে নিজের Authentication Logic লেখা।

Example

```python
class CustomJWTAuthentication(JWTAuthentication):

    def authenticate(self, request):

        user_auth = super().authenticate(request)

        if user_auth is None:
            return None

        user, token = user_auth

        if not user.is_active:
            raise AuthenticationFailed("Inactive user")

        return user, token
```

Use cases:

- Active User Check
    
- Email Verified Check
    
- Subscription Check
    
- Device Validation
    
- IP Restriction
    

---

# 9. Role-based Authentication (Admin, Teacher, Student)

একই API-তে Role অনুযায়ী Access Control।

Model

```python
class User(AbstractUser):
    ROLE_CHOICES = [
        ("admin", "Admin"),
        ("teacher", "Teacher"),
        ("student", "Student"),
    ]
    role = models.CharField(max_length=20, choices=ROLE_CHOICES)
```

Permission

```python
from rest_framework.permissions import BasePermission

class IsTeacher(BasePermission):
    def has_permission(self, request, view):
        return request.user.role == "teacher"
```

View

```python
permission_classes = [IsTeacher]
```

Flow

```text
JWT Login
     ↓
request.user
     ↓
Role Check
     ↓
Allow / Deny
```

---

# 10. Custom Permission Classes

নিজের Permission Logic লেখার জন্য `BasePermission` ব্যবহার করা হয়।

Example

```python
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

এটি নিশ্চিত করে যে একজন User শুধু নিজের Object-ই Edit/Delete করতে পারবে।

---

# 11. Refresh Token Rotation

Rotation-এর অর্থ হলো প্রতিবার Refresh Token ব্যবহার করলে একটি **নতুন Refresh Token** দেওয়া হবে এবং পুরোনোটি আর ব্যবহারযোগ্য থাকবে না।

Settings:

```python
SIMPLE_JWT = {
    "ROTATE_REFRESH_TOKENS": True,
    "BLACKLIST_AFTER_ROTATION": True,
}
```

Flow:

```text
Login
   ↓
Refresh Token A
   ↓
Use A to refresh
   ↓
Access Token B
Refresh Token B
   ↓
Refresh Token A ব্ল্যাকলিস্ট
```

এটি Token Replay Attack-এর ঝুঁকি কমায়।

---

# 12. JWT + React Authentication Flow

সবচেয়ে প্রচলিত Full Stack Flow:

```text
React Login Form
        │
        ▼
POST /api/token/
        │
        ▼
Django
        │
        ▼
Access + Refresh Token
        │
        ▼
React Store Tokens
        │
        ├── Access Token → Memory (বা নিরাপদ Storage Strategy)
        └── Refresh Token → Secure Storage (প্রজেক্টের Security Design অনুযায়ী)
        │
        ▼
API Call

Authorization:
Bearer AccessToken
        │
        ▼
Access Expired?
        │
       Yes
        │
        ▼
POST /api/token/refresh/
        │
        ▼
New Access Token
        │
        ▼
Retry Previous API
```

Logout:

```text
User Click Logout
      ↓
(Optional) Refresh Token Blacklist
      ↓
Client Removes Stored Tokens
      ↓
User Logged Out
```

---

# Interview Tip (১-২ মিনিটে উত্তর দেওয়ার মতো সারসংক্ষেপ)

- **Session vs JWT:** Session Server-side stateful, JWT Client-side stateless।
    
- **Access vs Refresh:** Access API Access-এর জন্য, Refresh নতুন Access Token তৈরির জন্য।
    
- **Stateless:** Server Session Store করে না; প্রতিটি Request-এ Token Verify হয়।
    
- **Header/Payload/Signature:** Header Algorithm, Payload Claims, Signature Integrity নিশ্চিত করে।
    
- **`request.user`:** JWTAuthentication Token Decode করে User Object Load করে `request.user` সেট করে।
    
- **Blacklist:** Logout বা Token Compromise-এর পরে Refresh Token Invalid করতে ব্যবহৃত হয়।
    
- **Sensitive Data:** JWT Payload Encrypted নয়, তাই Password বা OTP রাখা যাবে না।
    
- **Custom Permission:** `BasePermission` ব্যবহার করে Role বা Ownership অনুযায়ী Access Control করা হয়।
    
- **Refresh Rotation:** প্রতিবার Refresh-এর সময় নতুন Refresh Token ইস্যু করে পুরোনোটি বাতিল করা হয়।
    
- **React + JWT:** Login → Token Store → Bearer Token দিয়ে API Call → Refresh → Logout।
    

এই ১২টি বিষয় ভালোভাবে বুঝে এবং কোডসহ অনুশীলন করলে DRF-এর অধিকাংশ JWT Authentication Interview প্রশ্ন আত্মবিশ্বাসের সঙ্গে উত্তর দিতে পারবেন।

------------

