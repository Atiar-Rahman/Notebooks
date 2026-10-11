হ্যাঁ, করা যায়। এটাকে সাধারণভাবে **OTP-based login / two-step authentication flow** বলা যায়।

তোমার DRF project-এ flow-টা এমন হতে পারে:

```text
User
 │
 │ email + password
 ↓
DRF Login API
 │
 ├── credentials ভুল → Login failed
 │
 └── credentials ঠিক
        ↓
   Generate OTP
        ↓
   Send OTP
        ↓
   OTP verification page
        │
        ├── OTP ভুল → Login complete হবে না
        │
        └── OTP ঠিক
              ↓
        JWT access + refresh token
              ↓
             Login
```

### গুরুত্বপূর্ণ বিষয়

**Password সঠিক হলেই সরাসরি JWT token দেবে না।**

প্রথম ধাপে credentials verify করবে:

```text
email + password
       ↓
   valid?
       ↓
      YES
       ↓
Generate OTP
       ↓
Send OTP
       ↓
Wait for verification
```

তারপর OTP verify হলে:

```text
OTP correct
    ↓
Generate JWT
    ↓
Login successful
```

---

## DRF-এ API structure

আমি সাধারণত ২টা endpoint রাখতাম:

```text
POST /api/auth/login/
```

এটা:

```json
{
    "email": "user@example.com",
    "password": "password"
}
```

সঠিক হলে:

```json
{
    "message": "OTP sent successfully",
    "otp_required": true,
    "verification_id": "..."
}
```

তারপর:

```text
POST /api/auth/verify-otp/
```

```json
{
    "verification_id": "...",
    "otp": "123456"
}
```

সঠিক হলে:

```json
{
    "access": "...",
    "refresh": "..."
}
```

---

## OTP কোথায় রাখবে?

**Database বা Redis**-এ temporaryভাবে রাখতে পারো।

Production project-এ Redis ভালো option:

```text
Redis

otp:verification_id
        ↓
    123456
        ↓
    expires 5 min
```

OTP-এর সাথে অবশ্যই expiration রাখবে।

উদাহরণ:

```text
OTP = 123456
Valid for = 5 minutes
```

৫ মিনিট পরে:

```text
OTP expired → verification failed
```

আর OTP plain text হিসেবে দীর্ঘসময় database-এ রাখা উচিত নয়; verification state/hashed OTP বা short-lived Redis entry ব্যবহার করা ভালো।

---

## আরেকটা গুরুত্বপূর্ণ security বিষয়

OTP verify করার আগে **JWT token দেবে না**।

ভুল flow:

```text
Login
 ↓
JWT token
 ↓
OTP
```

ভালো flow:

```text
Login
 ↓
Password verified
 ↓
OTP
 ↓
OTP verified
 ↓
JWT token
 ↓
Authenticated
```

এটাই তুমি যেটা বলছো—**password ঠিক + OTP ঠিক হলেই login complete হবে।**

---
হ্যাঁ। তোমার **Django + DRF + SimpleJWT** project ধরে একদম শুরু থেকে দেখাই। এখানে OTP **email-এ পাঠানোর** example দিচ্ছি।

## 1. পুরো flow আগে বুঝো

```text
React Login Page
      │
      │ email + password
      ▼
POST /api/auth/login/
      │
      ▼
Password যাচাই
      │
      ├── ভুল → 401
      │
      └── ঠিক
           │
           ▼
        OTP তৈরি
           │
           ▼
       Redis-এ রাখে
           │
           ▼
      Email-এ পাঠায়
           │
           ▼
React OTP Page
           │
           │ OTP
           ▼
POST /api/auth/verify-otp/
           │
           ▼
       OTP যাচাই
           │
      ├── ভুল → error
      │
      └── ঠিক
           │
           ▼
     JWT Access/Refresh
           │
           ▼
        Login complete
```

---

# 2. Redis কেন ব্যবহার করব?

OTP temporary data:

```text
OTP = 583921
Valid = 5 minutes
```

এটা User model-এ রাখার দরকার নেই।

Redis:

```text
otp:abc123 → 583921
              ↓
           5 minutes
```

৫ মিনিট পরে automatically expire হবে।

---

# 3. OTP generate করা

একটা utility বানাও:

```python
# utils.py

import secrets


def generate_otp():
    return str(secrets.randbelow(900000) + 100000)
```

এতে 6-digit OTP হবে।

উদাহরণ:

```text
583921
```

`random` এর পরিবর্তে OTP-এর মতো security-sensitive value-এর জন্য `secrets` ব্যবহার করা ভালো।

---

# 4. Redis configuration

Redis package:

```bash
pip install redis
```

তারপর `settings.py`:

```python
REDIS_URL = "redis://localhost:6379/0"
```

Redis client:

```python
# redis_client.py

import redis
from django.conf import settings

redis_client = redis.from_url(
    settings.REDIS_URL,
    decode_responses=True,
)
```

---

# 5. Login API

এখানে প্রথমে email/password যাচাই করব।

```python
# serializers.py

from django.contrib.auth import authenticate
from rest_framework import serializers


class LoginSerializer(serializers.Serializer):

    email = serializers.EmailField()
    password = serializers.CharField(
        write_only=True
    )

    def validate(self, attrs):

        email = attrs["email"]
        password = attrs["password"]

        user = authenticate(
            email=email,
            password=password
        )

        if not user:
            raise serializers.ValidationError(
                "Invalid email or password."
            )

        if not user.is_active:
            raise serializers.ValidationError(
                "Account is inactive."
            )

        attrs["user"] = user

        return attrs
```

এখানে এখনো JWT দিচ্ছি না।

---

# 6. OTP generate + Redis-এ save

Login view:

```python
# views.py

import secrets

from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

from .serializers import LoginSerializer
from .redis_client import redis_client


class LoginView(APIView):

    def post(self, request):

        serializer = LoginSerializer(
            data=request.data
        )

        serializer.is_valid(raise_exception=True)

        user = serializer.validated_data["user"]

        otp = str(
            secrets.randbelow(900000) + 100000
        )

        verification_id = secrets.token_urlsafe(32)

        redis_client.setex(
            f"login_otp:{verification_id}",
            300,  # 5 minutes
            f"{user.id}:{otp}"
        )

        # এখানে email পাঠাবে

        return Response(
            {
                "message": "OTP sent successfully.",
                "verification_id": verification_id,
            },
            status=status.HTTP_200_OK
        )
```

এখানে:

```python
300
```

মানে:

```text
300 seconds
= 5 minutes
```

---

# 7. Email-এ OTP পাঠানো

Development-এর জন্য Django console email ব্যবহার করতে পারো।

`settings.py`:

```python
EMAIL_BACKEND = (
    "django.core.mail.backends.console.EmailBackend"
)
```

তারপর:

```python
from django.core.mail import send_mail
```

Login view-এ:

```python
send_mail(
    subject="Your Login OTP",
    message=f"Your OTP is: {otp}",
    from_email="noreply@example.com",
    recipient_list=[user.email],
)
```

Development-এ terminal-এ OTP দেখতে পাবে।

Production-এ transactional email provider ব্যবহার করবে।

---

# 8. OTP verification API

এখন দ্বিতীয় endpoint:

```python
# views.py

from rest_framework_simplejwt.tokens import RefreshToken


class VerifyOTPView(APIView):

    def post(self, request):

        verification_id = request.data.get(
            "verification_id"
        )

        otp = request.data.get("otp")

        if not verification_id or not otp:
            return Response(
                {
                    "detail": "verification_id and OTP are required."
                },
                status=status.HTTP_400_BAD_REQUEST
            )

        key = f"login_otp:{verification_id}"

        stored_value = redis_client.get(key)

        if not stored_value:
            return Response(
                {
                    "detail": "OTP expired or invalid."
                },
                status=status.HTTP_400_BAD_REQUEST
            )

        user_id, stored_otp = stored_value.split(":")

        if otp != stored_otp:
            return Response(
                {
                    "detail": "Invalid OTP."
                },
                status=status.HTTP_400_BAD_REQUEST
            )

        user = User.objects.get(id=user_id)

        refresh = RefreshToken.for_user(user)

        redis_client.delete(key)

        return Response(
            {
                "access": str(refresh.access_token),
                "refresh": str(refresh),
            }
        )
```

---

# 9. URL

```python
# urls.py

from django.urls import path

from .views import LoginView, VerifyOTPView


urlpatterns = [
    path(
        "auth/login/",
        LoginView.as_view()
    ),
    path(
        "auth/verify-otp/",
        VerifyOTPView.as_view()
    ),
]
```

এখন API:

```text
POST /api/auth/login/
```

তারপর:

```text
POST /api/auth/verify-otp/
```

---

# 10. React থেকে কীভাবে করবে?

প্রথম page:

```text
LoginPage
```

User দেয়:

```text
Email
Password
```

API:

```js
await apiClient.post("/auth/login/", {
  email,
  password,
});
```

Response:

```json
{
  "message": "OTP sent successfully.",
  "verification_id": "abc123..."
}
```

React এই `verification_id` রেখে OTP page-এ যাবে।

```text
LoginPage
     ↓
OTPPage
```

OTP page:

```text
Enter OTP
[  _ _ _ _ _ _ ]

     Verify
```

তারপর:

```js
await apiClient.post("/auth/verify-otp/", {
  verification_id,
  otp,
});
```

Response:

```json
{
  "access": "...",
  "refresh": "..."
}
```

তারপর তুমি access token ব্যবহার করে authenticated API call করবে।

---

# 11. কিন্তু production-এর জন্য আরও কয়েকটা জিনিস অবশ্যই যোগ করবে

উপরেরটা **learning implementation**। Production-এ সরাসরি এভাবেই রাখবে না।

বিশেষ করে:

```text
1. OTP attempt limit
2. OTP resend cooldown
3. Rate limiting
4. OTP brute-force protection
5. OTP hash করে রাখা
6. Generic login error যেখানে দরকার
7. Redis ব্যবহার
8. HTTPS
9. Refresh-token security
10. Account/session management
```

উদাহরণ:

```text
OTP:
583921

Attempts:
0 / 5

Resend:
wait 60 seconds

Expiry:
5 minutes
```

তাহলে কেউ বারবার:

```text
111111
111112
111113
...
```

দিয়ে চেষ্টা করতে পারবে না।

---

## তোমার project-এর জন্য আমি যে architecture রাখতাম

```text
authentication/
│
├── models.py
├── serializers.py
├── views.py
├── urls.py
├── services/
│   ├── otp_service.py
│   └── token_service.py
├── utils/
│   └── otp.py
└── redis_client.py
```

আর flow:

```text
LoginView
   ↓
LoginService
   ↓
verify email/password
   ↓
OTPService
   ├── generate OTP
   ├── store OTP
   ├── expiry
   ├── send OTP
   └── rate limit
   ↓
VerifyOTPView
   ↓
OTPService.verify()
   ↓
TokenService
   ↓
SimpleJWT
```

**তোমার বর্তমান DRF + SimpleJWT project-এর জন্য এই service-layer architecture-টাই শেখা বেশি useful**, কারণ পরে Google login, email verification, forgot password, phone OTP—সব একই pattern-এ organize করতে পারবে।


---
