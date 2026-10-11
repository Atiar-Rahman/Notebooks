হ্যাঁ। আপনি যদি Django Admin থেকে একজন user-কে `Can add product`, `Can change product` ইত্যাদি permission দিয়ে থাকেন, তাহলে DRF `ViewSet` থেকে সেটা ব্যবহার করার সবচেয়ে সহজ উপায় হলো `DjangoModelPermissions`।

### 1. ViewSet-এ permission দিন

```
from rest_framework.viewsets import ModelViewSet
from rest_framework.permissions import DjangoModelPermissions

from .models import Product
from .serializers import ProductSerializer


class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    permission_classes = [DjangoModelPermissions]
```

এখন DRF automatically Django-এর permission check করবে।

### 2. Admin থেকে permission দিন

ধরুন আপনার model:

```
class Product(models.Model):
    name = models.CharField(max_length=100)
```

Django Admin থেকে user-কে:

```
Products
 └── Product
      ✓ Can view product
      ✓ Can add product
      ✗ Can change product
      ✗ Can delete product
```

দিলেন।

তাহলে `DjangoModelPermissions` ব্যবহার করলে roughly:

```
GET     /api/products/       → view permission
POST    /api/products/       → add permission
PUT     /api/products/1/     → change permission
PATCH   /api/products/1/     → change permission
DELETE  /api/products/1/     → delete permission
```

অনুমতি না থাকলে DRF `403 Forbidden` দেবে।

### 3. যদি শুধু একটা custom permission check করতে চান

ধরুন আপনি specifically check করতে চান:

```
products.change_product
```

তাহলে ViewSet-এর মধ্যে:

```
if request.user.has_perm("products.change_product"):
    # allowed
```

অথবা custom DRF permission:

```
from rest_framework.permissions import BasePermission


class CanChangeProduct(BasePermission):

    def has_permission(self, request, view):
        return request.user.has_perm("products.change_product")
```

তারপর:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [CanChangeProduct]
```

**তবে আপনার requirement যদি হয় Admin Panel থেকে permission manage করবেন এবং ViewSet automatically সেই permission অনুযায়ী `GET/POST/PUT/DELETE` control করবে, তাহলে `DjangoModelPermissions`-ই সবচেয়ে straightforward approach।**

আপনি চাইলে আপনার বর্তমান `ViewSet` code দিলে আমি সেটার ওপরেই **Admin থেকে দেওয়া permission কীভাবে apply করবেন** দেখিয়ে দিতে পারি।



---
হ্যাঁ। পুরো flow-টা এমন হবে:

```
Django Admin
     │
     ├── User permission
     │      └── Can add/change/delete/view Product
     │
     └── Group permission
            └── Can add/change/delete/view Product
                     │
                     ▼
              Django Auth
                     │
                     ▼
             DRF ViewSet
                     │
              DjangoModelPermissions
                     │
                     ▼
                  API
```

 ## 1\. Model

 ধরি আপনার `Product` model:

```
# products/models.py

from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.name
```

 Django automatically এই permissions তৈরি করবে:

```
products.add_product
products.change_product
products.delete_product
products.view_product
```

 Migration করার পর এগুলো Django Admin-এ দেখতে পাবেন।

---

 ## 2\. Admin থেকে User-কে permission দেওয়া

 Django Admin:

```
Users
  ↓
Rahim
  ↓
Permissions
  ↓
User permissions
```

 তারপর দিন:

```
✓ products | product | Can view product
✓ products | product | Can add product
✗ products | product | Can change product
✗ products | product | Can delete product
```

 এখন Rahim-এর permission হলো:

```
view_product
add_product
```

---

 ## 3\. ViewSet-এ `DjangoModelPermissions`

 এটাই সবচেয়ে গুরুত্বপূর্ণ অংশ।

```
# products/views.py

from rest_framework.viewsets import ModelViewSet
from rest_framework.permissions import DjangoModelPermissions

from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    permission_classes = [DjangoModelPermissions]
```

 ব্যস। এখন DRF Django-এর permission system ব্যবহার করবে।

---

 ## 4\. কোন HTTP method কোন permission check করবে?

 সাধারণভাবে:

 | API | HTTP method | Django permission |
| --- | --- | --- |
| `/products/` | GET | `view_product` |
| `/products/` | POST | `add_product` |
| `/products/1/` | GET | `view_product` |
| `/products/1/` | PUT | `change_product` |
| `/products/1/` | PATCH | `change_product` |
| `/products/1/` | DELETE | `delete_product` |

তাই Rahim-এর যদি থাকে:

```
✓ view_product
✓ add_product
✗ change_product
✗ delete_product
```

 তাহলে:

```
GET       → allowed
POST      → allowed
PUT       → forbidden
PATCH     → forbidden
DELETE    → forbidden
```

 এটাই আপনার চাওয়া behavior।

---

 ## 5\. একটা গুরুত্বপূর্ণ বিষয়: `DjangoModelPermissions`

 DRF-এর `DjangoModelPermissions` সাধারণত unsafe methods-এর জন্য Django permission check করে।

 আপনি যদি চান **GET-এর জন্যও `view_model` permission অবশ্যই required হবে**, তাহলে custom permission class ব্যবহার করা ভালো।

```
from rest_framework.permissions import DjangoModelPermissions

class CustomDjangoModelPermissions(DjangoModelPermissions):

    perms_map = {
        "GET": ["%(app_label)s.view_%(model_name)s"],
        "OPTIONS": ["%(app_label)s.view_%(model_name)s"],
        "HEAD": ["%(app_label)s.view_%(model_name)s"],
        "POST": ["%(app_label)s.add_%(model_name)s"],
        "PUT": ["%(app_label)s.change_%(model_name)s"],
        "PATCH": ["%(app_label)s.change_%(model_name)s"],
        "DELETE": ["%(app_label)s.delete_%(model_name)s"],
    }
```

 তারপর:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [CustomDjangoModelPermissions]
```

 এখন GET করতেও অবশ্যই:

```
products.view_product
```

 থাকতে হবে।

---

 # 6\. User বনাম Group কীভাবে কাজ করবে?

 এখানে Django-এর built-in permission system বেশ সুন্দরভাবে কাজ করে।

 ধরি আপনার দুইটা Group:

```
Manager
Editor
```

 ### Manager

```
✓ view_product
✓ add_product
✓ change_product
✓ delete_product
```

 ### Editor

```
✓ view_product
✓ add_product
✓ change_product
✗ delete_product
```

 তারপর User:

```
Rahim
  └── Group: Manager

Karim
  └── Group: Editor
```

 Rahim automatically Manager-এর permissions পাবে।

 Karim automatically Editor-এর permissions পাবে।

 ViewSet-এর কোনো পরিবর্তন লাগবে না:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [CustomDjangoModelPermissions]
```

---

 # 7\. User-এর direct permission + Group permission

 ধরি:

```
Group: Editor

✓ view_product
✓ add_product
✓ change_product
✗ delete_product
```

 Karim Editor group-এর member।

 এখন Admin থেকে Karim-এর direct permission-এ:

```
✓ delete_product
```

 দিয়ে দিলেন।

 তাহলে Karim-এর effective permission হবে:

```
✓ view_product
✓ add_product
✓ change_product
✓ delete_product
```

 অর্থাৎ **Group permission + direct user permission** মিলিয়ে user-এর effective permissions তৈরি হয়।

---

 # 8\. `request.user.has_perm()` দিয়ে manually check

 কখনো আপনার custom business logic থাকতে পারে।

 তখন সরাসরি:

```
request.user.has_perm(
    "products.change_product"
)
```

 ব্যবহার করতে পারবেন।

 উদাহরণ:

```
from rest_framework.response import Response
from rest_framework import status

def update(self, request, *args, **kwargs):

    if not request.user.has_perm("products.change_product"):
        return Response(
            {"detail": "You don't have permission to change products."},
            status=status.HTTP_403_FORBIDDEN
        )

    return super().update(request, *args, **kwargs)
```

 কিন্তু সাধারণ CRUD API-এর জন্য এভাবে প্রতিটি method-এ manually check করার দরকার নেই। `DjangoModelPermissions` ব্যবহার করাই cleaner।

---

 # 9\. Custom permission class কখন দরকার?

 ধরি আপনার requirement:

 > Product delete করার জন্য Django permission থাকলেই হবে না, user-কে Manager group-এর member-ও হতে হবে।

 তখন custom permission করতে পারেন:

```
from rest_framework.permissions import BasePermission

class ProductPermission(BasePermission):

    def has_permission(self, request, view):

        if request.method == "GET":
            return request.user.has_perm(
                "products.view_product"
            )

        if request.method == "POST":
            return request.user.has_perm(
                "products.add_product"
            )

        if request.method in ["PUT", "PATCH"]:
            return request.user.has_perm(
                "products.change_product"
            )

        if request.method == "DELETE":
            return (
                request.user.has_perm(
                    "products.delete_product"
                )
                and request.user.groups.filter(
                    name="Manager"
                ).exists()
            )

        return False
```

 ViewSet:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [ProductPermission]
```

 তবে এখানে Group-এর নাম hard-code করার আগে আপনার actual authorization requirement অনুযায়ী design করা ভালো।

---

 # 10\. Authentication-ও লাগবে

 আরেকটা গুরুত্বপূর্ণ বিষয় হলো `permission` check করার আগে Django/DRF-কে জানতে হবে **কে request করছে**।

 যেমন JWT ব্যবহার করলে:

```
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ],
}
```

 তারপর:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [CustomDjangoModelPermissions]
```

 Flow হবে:

```
JWT
 ↓
Authentication
 ↓
request.user
 ↓
Django permissions
 ↓
DjangoModelPermissions
 ↓
API allowed / 403
```

---

 ## আমার recommendation

 আপনার requirement যদি হয়:

 > **Django Admin থেকেই User/Group-এর permission manage করব, আর API automatically সেই permission অনুযায়ী access দেবে।**

 তাহলে structure রাখুন:

```
class CustomDjangoModelPermissions(DjangoModelPermissions):

    perms_map = {
        "GET": ["%(app_label)s.view_%(model_name)s"],
        "OPTIONS": ["%(app_label)s.view_%(model_name)s"],
        "HEAD": ["%(app_label)s.view_%(model_name)s"],
        "POST": ["%(app_label)s.add_%(model_name)s"],
        "PUT": ["%(app_label)s.change_%(model_name)s"],
        "PATCH": ["%(app_label)s.change_%(model_name)s"],
        "DELETE": ["%(app_label)s.delete_%(model_name)s"],
    }
```

 এবং:

```
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [CustomDjangoModelPermissions]
```

 তারপর **পুরো role/permission management Django Admin থেকেই** করবেন। User-কে direct permission দিতে পারবেন, আবার Group বানিয়ে সেই Group-এর permission দিয়েও manage করতে পারবেন।


---
হ্যাঁ। আপনি যদি **Django Admin → Group → Permissions → User-কে Group assign** করে ফেলেন, তাহলে সাধারণ CRUD API-এর জন্য মূলত আর খুব বেশি কিছু লাগে না। তবে DRF-এ কয়েকটা জায়গা ঠিকভাবে configure করতে হবে।

 ## 1\. Model-এ Permission তৈরি হবে

 ধরুন:

```
class Product(models.Model):
    name = models.CharField(max_length=100)
```

 Migration করার পর Django automatically তৈরি করবে:

```
add_product
change_product
delete_product
view_product
```

 Custom permission দরকার হলে:

```
class Product(models.Model):
    name = models.CharField(max_length=100)

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
        ]
```

 তারপর:

```
python manage.py makemigrations
python manage.py migrate
```

---

 ## 2\. Admin থেকে Group বানাবেন

 Django Admin:

```
Groups
  └── Manager
       ├── Product → Can view
       ├── Product → Can add
       ├── Product → Can change
       └── Product → Can delete
```

 তারপর:

```
Users
  └── Rahim
       └── Groups
            └── Manager
```

 এটুকু করলেই Rahim Manager-এর permissions পেয়ে যাবে।

---

 ## 3\. DRF-এ Authentication configure করতে হবে

 এটা খুব গুরুত্বপূর্ণ।

 যেমন আপনি JWT ব্যবহার করলে:

```
# settings.py

REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ],
}
```

 তাহলে API বুঝতে পারবে request-টা কোন user-এর।

```
JWT
 ↓
request.user
 ↓
User's Groups
 ↓
Group Permissions
 ↓
API Permission Check
```

---

 ## 4\. ViewSet-এ Permission class দিতে হবে

 আপনার মূল CRUD ViewSet:

```
from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer
from .permissions import CustomDjangoModelPermissions

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    permission_classes = [CustomDjangoModelPermissions]
```

---

 ## 5\. `CustomDjangoModelPermissions` বানান

 আমি আপনার ক্ষেত্রে এটা recommend করব, কারণ এতে **GET-এর জন্যও `view` permission required** হবে।

```
# permissions.py

from rest_framework.permissions import DjangoModelPermissions

class CustomDjangoModelPermissions(DjangoModelPermissions):

    perms_map = {
        "GET": [
            "%(app_label)s.view_%(model_name)s"
        ],

        "OPTIONS": [
            "%(app_label)s.view_%(model_name)s"
        ],

        "HEAD": [
            "%(app_label)s.view_%(model_name)s"
        ],

        "POST": [
            "%(app_label)s.add_%(model_name)s"
        ],

        "PUT": [
            "%(app_label)s.change_%(model_name)s"
        ],

        "PATCH": [
            "%(app_label)s.change_%(model_name)s"
        ],

        "DELETE": [
            "%(app_label)s.delete_%(model_name)s"
        ],
    }
```

 এখন আপনার Admin-এর permission সরাসরি API-তে কাজ করবে।

---

 ## 6\. তাহলে API behavior হবে

 ধরি:

```
Group: Editor

✓ Can view product
✓ Can add product
✓ Can change product
✗ Can delete product
```

 Editor-এর user:

```
GET     /api/products/       → 200
GET     /api/products/1/     → 200

POST    /api/products/       → 201

PUT     /api/products/1/    → 200
PATCH   /api/products/1/    → 200

DELETE  /api/products/1/    → 403
```

 অর্থাৎ Admin থেকে permission পরিবর্তন করলেই API access পরিবর্তন হবে।

---

 ## 7\. Global default permission সেট করতে পারেন

 প্রতিটা ViewSet-এ:

```
permission_classes = [...]
```

 লেখার বদলে `settings.py`-তে default দিতে পারেন:

```
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ],

    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.IsAuthenticated",
    ],
}
```

 এতে API defaultভাবে authenticated user চাইবে।

 তারপর যেসব ViewSet-এ Django model permission দরকার সেখানে:

```
permission_classes = [
    CustomDjangoModelPermissions
]
```

 দেবেন।

---

 ## 8\. Public API থাকলে

 ধরুন login/register API public রাখতে চান:

```
from rest_framework.permissions import AllowAny

class LoginView(...):
    permission_classes = [AllowAny]
```

 অন্যদিকে Product API:

```
class ProductViewSet(ModelViewSet):
    permission_classes = [
        CustomDjangoModelPermissions
    ]
```

---

 ## 9\. Object-level permission আলাদা বিষয়

 এটা খুব গুরুত্বপূর্ণ।

 ধরুন Manager-এর:

```
change_product
```

 permission আছে।

 তার মানে Manager **সব Product change করতে পারবে**।

 কিন্তু আপনার requirement যদি হয়:

 > User শুধু নিজের তৈরি Product edit করতে পারবে।

 তাহলে শুধু Django Group permission যথেষ্ট নয়। তখন **object-level permission** লাগবে।

 যেমন:

```
def update(self, request, *args, **kwargs):
    product = self.get_object()

    if product.created_by != request.user:
        raise PermissionDenied(
            "You can only edit your own product."
        )

    return super().update(request, *args, **kwargs)
```

 এটা আলাদা authorization rule।

---

 # আপনার পুরো architecture

 আপনার project-এ আমি roughly এভাবে রাখতাম:

```
                    Django Admin
                         │
              ┌──────────┴──────────┐
              │                     │
            Groups              Direct User
              │                   Permission
              │                     │
              └──────────┬──────────┘
                         ↓
                  Django Permission
                         ↓
                 DRF Permission Class
                         ↓
                  ViewSet / API
                         ↓
                  Object-level rules
                         ↓
                     Database
```

 ### আপনার এখন যা যা লাগবে

 - ✅ Django Admin-এ Group তৈরি
- ✅ Group-এ model permissions দেওয়া
- ✅ User-কে Group assign করা
- ✅ JWT/Session authentication configure করা
- ✅ DRF `permission_classes` configure করা
- ✅ `DjangoModelPermissions` বা custom version ব্যবহার করা
- ✅ Object-specific restriction থাকলে আলাদা object-level check করা

 **শুধু Group তৈরি করে User-কে Group দিলেই API নিজে নিজে permission enforce করবে না**—ViewSet-এ DRF permission class-টা অবশ্যই থাকতে হবে।

 আপনি যদি **JWT + DRF + ViewSet \+ Django Admin Group/Role** দিয়ে production-ready RBAC বানাতে চান, তাহলে  আমি আপনার জন্য পুরো folder structure (permissions.py, views.py, settings.py, JWT login, Admin setup) একসাথে সাজিয়ে দিতে পারি ।