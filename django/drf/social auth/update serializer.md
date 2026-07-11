আমি দুইটা version দিচ্ছি—কারণ তোমার `phone_number` **User model-এ** নাকি **Profile model-এ** সেটা এখনও clear না।

---

# Version 1 — `phone_number` User model-এ

Example model:

```python
class User(AbstractUser):
    phone_number = models.CharField(max_length=20, blank=True)
```

Serializer:

```python
from rest_framework import serializers
from dj_rest_auth.registration.serializers import RegisterSerializer


class CustomRegisterSerializer(RegisterSerializer):
    phone_number = serializers.CharField(max_length=20, required=False)

    def get_cleaned_data(self):
        data = super().get_cleaned_data()
        data["phone_number"] = self.validated_data.get("phone_number", "")
        return data

    def custom_signup(self, request, user):
        user.phone_number = self.validated_data.get("phone_number", "")
        user.save()
```

---

# Version 2 — `phone_number` Profile model-এ

Example:

```python
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    phone_number = models.CharField(max_length=20)
```

Serializer:

```python
from rest_framework import serializers
from dj_rest_auth.registration.serializers import RegisterSerializer


class CustomRegisterSerializer(RegisterSerializer):
    phone_number = serializers.CharField(max_length=20, required=False)

    def get_cleaned_data(self):
        data = super().get_cleaned_data()
        data["phone_number"] = self.validated_data.get("phone_number", "")
        return data

    def custom_signup(self, request, user):
        user.profile.phone_number = self.validated_data.get("phone_number", "")
        user.profile.save()
```

---

# settings.py

Register serializer use করাতে:

```python
REST_AUTH = {
    "REGISTER_SERIALIZER": "accounts.serializers.CustomRegisterSerializer"
}
```

যদি আগের config থাকে merge করো:

```python
REST_AUTH = {
    'USE_JWT': True,
    'JWT_AUTH_COOKIE': 'access',
    'JWT_AUTH_REFRESH_COOKIE': 'refresh',
    'JWT_AUTH_HTTPONLY': True,
    'REGISTER_SERIALIZER': 'accounts.serializers.CustomRegisterSerializer',
}
```

---

# Signup request

এখন `/registration/` এ:

```json
{
  "username": "admin2",
  "email": "admin2@gmail.com",
  "password1": "StrongPass123",
  "password2": "StrongPass123",
  "phone_number": "01712345678"
}
```

---

একটা note: `profile_picture` upload করতে চাইলে `ImageField` handle করার জন্য serializer-এ `serializers.ImageField()` add করতে হবে।

তোমার **User model code** দিলে আমি exact final serializer (phone + profile_picture সহ) লিখে দিতে পারি।

--------------
একটা **বড় ধরনের ecommerce-ready Custom User model** বানাই, তারপর `dj-rest-auth`-এর **Register Serializer + User Serializer** update করি।

ধরি তুমি চাইছ:

* username
* email
* first_name
* last_name
* phone_number
* profile_picture
* date_of_birth
* gender
* address
* city
* country
* is_verified

---

# 1. Custom User Model

```python id="80o4s6"
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):
    GENDER_CHOICES = (
        ("male", "Male"),
        ("female", "Female"),
        ("other", "Other"),
    )

    email = models.EmailField(unique=True)
    phone_number = models.CharField(max_length=20, blank=True)
    profile_picture = models.ImageField(
        upload_to="profile_pictures/",
        null=True,
        blank=True
    )
    date_of_birth = models.DateField(null=True, blank=True)
    gender = models.CharField(
        max_length=10,
        choices=GENDER_CHOICES,
        blank=True
    )
    address = models.TextField(blank=True)
    city = models.CharField(max_length=100, blank=True)
    country = models.CharField(max_length=100, blank=True)
    is_verified = models.BooleanField(default=False)

    def __str__(self):
        return self.username
```

settings:

```python id="g2l4m0"
AUTH_USER_MODEL = "accounts.User"
```

---

# 2. User Details Serializer (`/user/`)

```python id="kvmxqs"
from dj_rest_auth.serializers import UserDetailsSerializer


class CustomUserDetailsSerializer(UserDetailsSerializer):
    class Meta(UserDetailsSerializer.Meta):
        fields = (
            "pk",
            "username",
            "email",
            "first_name",
            "last_name",
            "phone_number",
            "profile_picture",
            "date_of_birth",
            "gender",
            "address",
            "city",
            "country",
            "is_verified",
        )
```

এটা `/api/auth/user/` response customize করবে।

---

# 3. Register Serializer

```python id="y0f0n0"
from rest_framework import serializers
from dj_rest_auth.registration.serializers import RegisterSerializer
```

```python id="qzt0h0"
class CustomRegisterSerializer(RegisterSerializer):
    phone_number = serializers.CharField(required=False)
    profile_picture = serializers.ImageField(required=False)
    date_of_birth = serializers.DateField(required=False)
    gender = serializers.CharField(required=False)
    address = serializers.CharField(required=False)
    city = serializers.CharField(required=False)
    country = serializers.CharField(required=False)

    def get_cleaned_data(self):
        data = super().get_cleaned_data()
        data["phone_number"] = self.validated_data.get("phone_number", "")
        data["profile_picture"] = self.validated_data.get("profile_picture", None)
        data["date_of_birth"] = self.validated_data.get("date_of_birth", None)
        data["gender"] = self.validated_data.get("gender", "")
        data["address"] = self.validated_data.get("address", "")
        data["city"] = self.validated_data.get("city", "")
        data["country"] = self.validated_data.get("country", "")
        return data

    def custom_signup(self, request, user):
        user.phone_number = self.validated_data.get("phone_number", "")
        user.profile_picture = self.validated_data.get("profile_picture", None)
        user.date_of_birth = self.validated_data.get("date_of_birth", None)
        user.gender = self.validated_data.get("gender", "")
        user.address = self.validated_data.get("address", "")
        user.city = self.validated_data.get("city", "")
        user.country = self.validated_data.get("country", "")
        user.save()
```

---

# 4. settings.py

```python id="02iz3p"
REST_AUTH = {
    'USE_JWT': True,
    'JWT_AUTH_COOKIE': 'access',
    'JWT_AUTH_REFRESH_COOKIE': 'refresh',
    'JWT_AUTH_HTTPONLY': True,

    'REGISTER_SERIALIZER':
        'accounts.serializers.CustomRegisterSerializer',

    'USER_DETAILS_SERIALIZER':
        'accounts.serializers.CustomUserDetailsSerializer',
}
```

---

# 5. Registration Request

JSON (image ছাড়া):

```json id="c2jlwm"
{
  "username": "admin",
  "email": "admin@gmail.com",
  "password1": "StrongPass123",
  "password2": "StrongPass123",
  "phone_number": "01712345678",
  "gender": "male",
  "city": "Dhaka",
  "country": "Bangladesh"
}
```

Image upload থাকলে `multipart/form-data` use করো।

---

## Practical advice (E-commerce)

সব field `User` model-এ না রেখে অনেক project এ split করা হয়:

* User → auth related
* Profile → personal info
* Address → shipping addresses

Large production app-এ এটা cleaner architecture।

--------------
হ্যাঁ — সাধারণত **different model (normalized design)** রাখলে `RegisterSerializer` অনেক ছোট হয় ✅

Example architecture:

### User model (auth only)

```python id="e0fy3n"
class User(AbstractUser):
    email = models.EmailField(unique=True)
```

### Profile model

```python id="5y6u24"
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    phone_number = models.CharField(max_length=20)
    profile_picture = models.ImageField(upload_to="profiles/")
    date_of_birth = models.DateField()
```

### Address model

```python id="1v2zcg"
class Address(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    city = models.CharField(max_length=100)
    country = models.CharField(max_length=100)
```

---

# Registration Serializer ছোট কেন?

কারণ signup-এর সময় usually সব info লাগে না।

সাধারণত শুধু লাগে:

* username / email
* password
* maybe phone

তাই serializer:

```python id="h93yo6"
from dj_rest_auth.registration.serializers import RegisterSerializer
from rest_framework import serializers

class CustomRegisterSerializer(RegisterSerializer):
    phone_number = serializers.CharField(required=False)

    def custom_signup(self, request, user):
        Profile.objects.create(
            user=user,
            phone_number=self.validated_data.get("phone_number", "")
        )
```

দেখো — অনেক ছোট।

---

## যদি সব User model-এ রাখো

```python id="wyo0p6"
User:
- phone
- picture
- gender
- city
- country
- dob
- bio
- ...
```

তখন Register serializer huge হয়ে যায়:

```text id="mvw8j8"
15-20 fields
get_cleaned_data()
custom_signup()
validation
```

Maintain করা harder।

---

# Real-world practice (Ecommerce)

আমি সাধারণত split করি এভাবে:

### User

* id
* email
* password
* is_staff
* is_active

### Profile

* name
* phone
* avatar

### Address

* shipping address
* billing address

### Customer

* loyalty points
* wallet balance

---

## Rule of thumb

### User model-এ রাখো

যেগুলো authentication-related:

✅ email
✅ password
✅ username
✅ is_active

---

### Separate model-এ রাখো

যেগুলো business/domain data:

✅ profile picture
✅ phone
✅ address
✅ order preferences

---

So answer:

> different model থাকলে Registration model small থাকবে?

**হ্যাঁ, বেশিরভাগ সময়** — কারণ register-এর সময় শুধু essential auth fields handle করলেই হয়।
বাকি profile/address পরে create/update করতে পারো।
যদি **login endpoint-এও `username` দেখায়**, তাহলে এর কারণ সাধারণত `dj-rest-auth`-এর **default `LoginSerializer`** এখনও `username` field ব্যবহার করছে।

তোমার setup অনুযায়ী:

* ✅ `User.username = None`
* ✅ `USERNAME_FIELD = "email"`
* ✅ `ACCOUNT_USERNAME_REQUIRED = False`

তাহলে login-এ `email` ব্যবহার হওয়ার কথা।

### প্রথমে এটা দেখো

`settings.py`-এ কি আছে?

```python
REST_AUTH = {
    "USE_JWT": True,
}
```

এছাড়া `LOGIN_SERIALIZER` সেট করেছো কি?

---

### আরেকটা গুরুত্বপূর্ণ বিষয়

Swagger (`drf-yasg`) অনেক সময় serializer cache করে। তাই code পরিবর্তনের পর:

```bash
python manage.py runserver
```

restart করো এবং browser hard refresh (Ctrl+Shift+R) দাও।

---

### যদি API documentation-এ এখনও `username` দেখায়

তাহলে custom `LoginSerializer` বানাতে হবে, যেমন:

```python
from dj_rest_auth.serializers import LoginSerializer
from rest_framework import serializers

class CustomLoginSerializer(LoginSerializer):
    username = None
    email = serializers.EmailField(required=True)
```

এবং:

```python
REST_AUTH = {
    "USE_JWT": True,
    "LOGIN_SERIALIZER": "users.serializers.CustomLoginSerializer",
}
```

---

### আমার ধারণা

তোমার `dj-rest-auth`-এর version অনুযায়ী default login serializer এখনও username expose করছে।

**একটা জিনিস দাও:**

```bash
pip show dj-rest-auth
```

বিশেষ করে **Version**-টা। তাহলে আমি তোমার version অনুযায়ী email-only login-এর exact configuration বলতে পারব।
