Django REST Framework-এ **Secure Authentication System** বানাতে অনেক সময় **Djoser + Simple JWT** একসাথে ব্যবহার করা হয়।  
এটা production-ready authentication system তৈরি করতে সাহায্য করে। 🔐

আমি প্রতিটা **term + example** দিয়ে সহজভাবে explain করছি।

---

# 1️⃣ Djoser কী

**Djoser** হলো Django REST Framework এর জন্য **ready-made authentication API package**।

এটা automatically অনেক API তৈরি করে দেয়।

### Example APIs

```
POST /auth/users/          -> register
POST /auth/jwt/create/     -> login
POST /auth/jwt/refresh/    -> refresh token
POST /auth/jwt/verify/     -> verify token
GET  /auth/users/me/       -> current user
```

👉 মানে authentication system **নিজে লিখতে হয় না**।

---

# 2️⃣ JWT কী

**JSON Web Token**

JWT হলো **stateless authentication token**।

User login করলে server একটা **token** দেয়।

Example token

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJ1c2VyX2lkIjoxLCJleHAiOjE2NzE4NzA1MDB9
.
sdfksdjfksdjfksdjfksdjfk
```

এটা 3 অংশে থাকে

```
HEADER.PAYLOAD.SIGNATURE
```

---

# 3️⃣ Simple JWT কী

**Simple JWT**

এটা Django REST Framework এর **JWT authentication library**।

এটা handle করে:

- access token
    
- refresh token
    
- token verification
    
- token expiration
    

---

# 4️⃣ Access Token

Access token হলো **short-lived token**।

Example response

```json
{
  "access": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9",
  "refresh": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9"
}
```

Access token use করে API access করা হয়।

Example

```
Authorization: Bearer ACCESS_TOKEN
```

---

# 5️⃣ Refresh Token

Refresh token দিয়ে **নতুন access token তৈরি করা যায়**।

Example request

```
POST /auth/jwt/refresh/
```

Body

```json
{
  "refresh": "refresh_token_here"
}
```

Response

```json
{
  "access": "new_access_token"
}
```

---

# 6️⃣ Token Expiration

Token কিছু সময় পরে expire হয়ে যায়।

Example setting

```python
from datetime import timedelta

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=5),
    "REFRESH_TOKEN_LIFETIME": timedelta(days=1),
}
```

মানে

```
Access token -> 5 min
Refresh token -> 1 day
```

---

# 7️⃣ Authentication Header

Frontend যখন API call করবে তখন token পাঠাবে।

Example

```
GET /api/cameras/

Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
```

Backend automatically verify করবে।

---

# 8️⃣ Secure API Example

### DRF View

```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.views import APIView
from rest_framework.response import Response

class CameraList(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response({"message": "Secure Data"})
```

যদি token না থাকে

```
401 Unauthorized
```

---

# 9️⃣ Full Authentication Flow

```
User Register
     │
     ▼
POST /auth/users/
     │
     ▼
User Login
POST /auth/jwt/create/
     │
     ▼
Get Access + Refresh Token
     │
     ▼
Frontend send Access Token
Authorization: Bearer TOKEN
     │
     ▼
Backend Verify Token
     │
     ▼
Access API
```

---

# 🔟 Example Real API Request

### Login

```
POST /auth/jwt/create/
```

Body

```json
{
  "email": "user@gmail.com",
  "password": "123456"
}
```

Response

```json
{
  "refresh": "token123",
  "access": "token456"
}
```

---

# 1️⃣1️⃣ Production Security Tips

Use:

```
HTTPS
Short access token lifetime
Refresh token rotation
Blacklist token
```

Example

```python
SIMPLE_JWT = {
    "ROTATE_REFRESH_TOKENS": True,
    "BLACKLIST_AFTER_ROTATION": True,
}
```

---

# 1️⃣2️⃣ Industry Authentication Architecture

```
Frontend (React / Next.js)
        │
        │ JWT Token
        ▼
API Gateway
        │
        ▼
Django REST API
        │
        ▼
Djoser + SimpleJWT
        │
        ▼
Database (User)
```

---

✅ Since you are building **Django + AI CCTV backend**, this authentication system is **perfect for your project** because:

- mobile app login
    
- dashboard login
    
- API security
    
- token authentication
    

---

💡 চাইলে আমি তোমাকে দেখাতে পারি:

1️⃣ **Complete Django Djoser + Simple JWT production setup**  
2️⃣ **Custom User Model + Djoser integration**  
3️⃣ **Industry level authentication architecture (refresh rotation + blacklist + httpOnly cookie)**

এগুলো শিখলে তুমি **production-level backend developer** এর মতো authentication implement করতে পারবে। 🔥