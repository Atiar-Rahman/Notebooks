নিচের structure-টা **JWT + Django REST Framework + Django Admin Group/Role + Model Permission + ViewSet** ভিত্তিক production-ready RBAC-এর জন্য ভালো starting point। এখানে Role management পুরোপুরি Django Admin থেকে হবে।

## 1. Folder structure

```
myproject/
├── manage.py
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── accounts/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   ├── views.py
│   └── permissions.py
│
├── products/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   ├── views.py
│   └── permissions.py
│
├── requirements.txt
└── .env
```

---

# 2. Install packages

```
pip install django
pip install djangorestframework
pip install djangorestframework-simplejwt
```

`requirements.txt`:

```
Django
djangorestframework
djangorestframework-simplejwt
```

Production-এ অবশ্যই versions pin করে রাখবেন, যেমন:

```
Django==5.x.x
djangorestframework==3.x.x
djangorestframework-simplejwt==5.x.x
```

---

# 3. `settings.py`

```
# config/settings.py

from pathlib import Path
from datetime import timedelta
import os

BASE_DIR = Path(__file__).resolve().parent.parent


SECRET_KEY = os.environ.get(
    "DJANGO_SECRET_KEY",
    "change-this-in-production"
)

DEBUG = os.environ.get("DJANGO_DEBUG", "False") == "True"

ALLOWED_HOSTS = [
    "localhost",
    "127.0.0.1",
]


INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "rest_framework",

    "accounts",
    "products",
]


MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "django.contrib.sessions.middleware.SessionMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
]


ROOT_URLCONF = "config.urls"


TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "DIRS": [],
        "APP_DIRS": True,
        "OPTIONS": {
            "context_processors": [
                "django.template.context_processors.request",
                "django.contrib.auth.context_processors.auth",
                "django.contrib.messages.context_processors.messages",
            ],
        },
    },
]


WSGI_APPLICATION = "config.wsgi.application"


DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.sqlite3",
        "NAME": BASE_DIR / "db.sqlite3",
    }
}


AUTH_PASSWORD_VALIDATORS = [
    {
        "NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator",
    },
    {
        "NAME": "django.contrib.auth.password_validation.MinimumLengthValidator",
    },
    {
        "NAME": "django.contrib.auth.password_validation.CommonPasswordValidator",
    },
    {
        "NAME": "django.contrib.auth.password_validation.NumericPasswordValidator",
    },
]


LANGUAGE_CODE = "en-us"
TIME_ZONE = "Asia/Dhaka"

USE_I18N = True
USE_TZ = True


STATIC_URL = "static/"


DEFAULT_AUTO_FIELD = "django.db.models.BigAutoField"


# ============================================================
# DRF
# ============================================================

REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),

    "DEFAULT_PERMISSION_CLASSES": (
        "rest_framework.permissions.IsAuthenticated",
    ),

    "DEFAULT_PAGINATION_CLASS":
        "rest_framework.pagination.PageNumberPagination",

    "PAGE_SIZE": 20,
}


# ============================================================
# JWT
# ============================================================

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(
        minutes=15
    ),

    "REFRESH_TOKEN_LIFETIME": timedelta(
        days=7
    ),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "UPDATE_LAST_LOGIN": True,

    "AUTH_HEADER_TYPES": (
        "Bearer",
    ),
}
```

Production-এ `SECRET_KEY`, `DEBUG`, database credentials ইত্যাদি `.env`/environment variable থেকে নেওয়া উচিত।

---

# 4. User model

শুরু থেকেই custom user ব্যবহার করতে চাইলে সেটা ভালো practice।

`accounts/models.py`:

```
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):
    pass
```

তারপর `settings.py`:

```
AUTH_USER_MODEL = "accounts.User"
```

**খুব গুরুত্বপূর্ণ:** project-এর শুরুতেই custom user model configure করুন। Production project-এ পরে `AUTH_USER_MODEL` পরিবর্তন করা বেশ জটিল হতে পারে।

---

# 5. Product model

```
# products/models.py

from django.conf import settings
from django.db import models


class Product(models.Model):

    name = models.CharField(
        max_length=255
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    created_by = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="products"
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    def __str__(self):
        return self.name
```

---

# 6. Custom permissions

`products/permissions.py`:

```
from rest_framework.permissions import DjangoModelPermissions


class RBACModelPermissions(DjangoModelPermissions):

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

এটা করলে Django Admin-এর permissions সরাসরি API methods-এর সঙ্গে map হবে।

---

# 7. Serializer

```
# products/serializers.py

from rest_framework import serializers

from .models import Product


class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product

        fields = [
            "id",
            "name",
            "price",
            "created_by",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_by",
            "created_at",
            "updated_at",
        ]
```

---

# 8. Product ViewSet

```
# products/views.py

from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer
from .permissions import RBACModelPermissions


class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]

    def perform_create(self, serializer):

        serializer.save(
            created_by=self.request.user
        )
```

এখন:

```
GET       → view_product
POST      → add_product
PUT       → change_product
PATCH     → change_product
DELETE    → delete_product
```

---

# 9. Object-level ownership

ধরুন requirement:

> User নিজের Product edit/delete করতে পারবে, অন্যের Product পারবে না।

তাহলে শুধু model permission যথেষ্ট নয়।

একটি permission class:

```
# products/permissions.py

from rest_framework.permissions import DjangoModelPermissions


class RBACModelPermissions(DjangoModelPermissions):

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

আর ViewSet queryset দিয়ে ownership enforce করা যায়:

```
class ProductViewSet(ModelViewSet):

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]

    def get_queryset(self):

        user = self.request.user

        if user.is_superuser:
            return Product.objects.all()

        return Product.objects.filter(
            created_by=user
        )

    def perform_create(self, serializer):

        serializer.save(
            created_by=self.request.user
        )
```

এখানে একটা গুরুত্বপূর্ণ design decision আছে: **Manager যদি অন্য user's product দেখতে/edit করতে পারে**, তাহলে ownership filtering শুধু `created_by=user` দিয়ে করা যাবে না। সে ক্ষেত্রে role অনুযায়ী queryset policy করতে হবে।

---

# 10. JWT Login

`accounts/urls.py`:

```
from django.urls import path

from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)


urlpatterns = [

    path(
        "login/",
        TokenObtainPairView.as_view(),
        name="token_obtain_pair",
    ),

    path(
        "refresh/",
        TokenRefreshView.as_view(),
        name="token_refresh",
    ),
]
```

`config/urls.py`:

```
from django.contrib import admin
from django.urls import include, path


urlpatterns = [

    path(
        "admin/",
        admin.site.urls
    ),

    path(
        "api/auth/",
        include("accounts.urls")
    ),

    path(
        "api/products/",
        include("products.urls")
    ),
]
```

---

# 11. Product URLs

`products/urls.py`:

```
from django.urls import include, path
from rest_framework.routers import DefaultRouter

from .views import ProductViewSet


router = DefaultRouter()

router.register(
    "products",
    ProductViewSet,
    basename="product"
)


urlpatterns = [
    path("", include(router.urls)),
]
```

তাহলে endpoint হবে:

```
POST   /api/auth/login/
POST   /api/auth/refresh/

GET    /api/products/products/
POST   /api/products/products/

GET    /api/products/products/1/
PUT    /api/products/products/1/
PATCH  /api/products/products/1/
DELETE /api/products/products/1/
```

---

# 12. Admin setup

`products/admin.py`:

```
from django.contrib import admin

from .models import Product


@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):

    list_display = (
        "id",
        "name",
        "price",
        "created_by",
        "created_at",
    )

    search_fields = (
        "name",
        "created_by__username",
    )

    list_filter = (
        "created_at",
    )

    readonly_fields = (
        "created_by",
        "created_at",
        "updated_at",
    )
```

`accounts/admin.py`:

```
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import User


@admin.register(User)
class CustomUserAdmin(UserAdmin):

    list_display = (
        "username",
        "email",
        "is_staff",
        "is_active",
    )

    list_filter = (
        "is_staff",
        "is_active",
        "groups",
    )
```

---

# 13. Database migration

```
python manage.py makemigrations
python manage.py migrate
```

তারপর superuser:

```
python manage.py createsuperuser
```

Admin:

```
/admin/
```

---

# 14. Admin থেকে Role বানানো

এখানে **Group = Role** হিসেবে ব্যবহার করবেন।

ধরুন তিনটি role:

```
Admin
Manager
Viewer
```

### Viewer

```
✓ Can view product
✗ Can add product
✗ Can change product
✗ Can delete product
```

### Manager

```
✓ Can view product
✓ Can add product
✓ Can change product
✗ Can delete product
```

### Admin

সব permission।

তারপর:

```
Users
 └── Rahim
      └── Groups
           └── Manager
```

এখন Rahim Manager role-এর permissions পাবে।

---

# 15. API request

Login:

```
POST /api/auth/login/
Content-Type: application/json
```

```
{
    "username": "rahim",
    "password": "your-password"
}
```

Response:

```
{
    "refresh": "eyJ...",
    "access": "eyJ..."
}
```

তারপর API:

```
GET /api/products/products/
Authorization: Bearer eyJ...
```

DRF:

```
JWT
 ↓
Authentication
 ↓
request.user = Rahim
 ↓
Rahim's Groups
 ↓
Group permissions
 ↓
RBACModelPermissions
 ↓
GET → view_product
 ↓
200 / 403
```

---

# 16. Custom business permission

Django model permission সব authorization-এর জন্য যথেষ্ট নয়।

যেমন:

> Manager product approve করতে পারবে।

Model:

```
class Product(models.Model):

    name = models.CharField(max_length=255)

    class Meta:
        permissions = [
            (
                "approve_product",
                "Can approve product"
            ),
        ]
```

Migration:

```
python manage.py makemigrations
python manage.py migrate
```

Admin থেকে:

```
Manager
 ├── Can view product
 ├── Can add product
 ├── Can change product
 └── Can approve product
```

Custom DRF permission:

```
from rest_framework.permissions import BasePermission


class CanApproveProduct(BasePermission):

    def has_permission(self, request, view):

        return request.user.has_perm(
            "products.approve_product"
        )
```

ViewSet-এ action-specific permission দিতে পারেন:

```
from rest_framework.decorators import action
from rest_framework.response import Response


class ProductViewSet(ModelViewSet):

    # ...

    @action(
        detail=True,
        methods=["post"],
        permission_classes=[CanApproveProduct],
    )
    def approve(self, request, pk=None):

        product = self.get_object()

        # approval logic

        return Response({
            "message": "Product approved"
        })
```

Endpoint:

```
POST /api/products/products/1/approve/
```

এটার জন্য Django Admin-এ শুধু:

```
products → Can approve product
```

permission দিলেই হবে।

---

# 17. Production RBAC-এর সবচেয়ে গুরুত্বপূর্ণ rule

আমি authorization-টা তিন layer-এ রাখার পরামর্শ দেব:

```
Layer 1
Authentication
        ↓
"এই request কে করেছে?"

Layer 2
Model / Role Permission
        ↓
"এই user এই ধরনের operation করতে পারে?"

Layer 3
Object / Business Permission
        ↓
"এই নির্দিষ্ট object-এর ওপর operation করতে পারে?"
```

উদাহরণ:

```
Rahim
  │
  ├── JWT valid?                 ✓
  │
  ├── Manager group?             ✓
  │
  ├── change_product permission? ✓
  │
  └── এই product-এর owner?       ✓
                         ↓
                       ALLOW
```

---

## 18. একটি গুরুত্বপূর্ণ security point

শুধু frontend-এ button hide করবেন না:

```
❌ Frontend:
"Delete button দেখাব না"

```

Backend-এ অবশ্যই permission enforce করবেন:

```
✓ Backend:
DELETE request
   ↓
delete_product permission?
   ↓
YES → continue
NO  → 403
```

কারণ attacker সরাসরি API call করতে পারে।

---

## 19. Final architecture

আপনার project শেষ পর্যন্ত এমন হতে পারে:

```
                    Django Admin
                         │
             ┌───────────┴───────────┐
             │                       │
          Groups                  Users
             │                       │
        Role/Permissions        Direct Permissions
             │                       │
             └───────────┬───────────┘
                         ↓
                  Django Auth System
                         ↓
                       JWT
                         ↓
                  DRF Authentication
                         ↓
              RBACModelPermissions
                         ↓
                     ViewSet
                         ↓
              Object-level permission
                         ↓
                  Business rules
                         ↓
                     Database
```

**এই setup-এ সবচেয়ে বড় সুবিধা হলো:** developer-কে প্রতিবার role hard-code করতে হচ্ছে না। নতুন `Viewer`, `Editor`, `Manager`, `Accountant` ইত্যাদি role তৈরি করে তাদের permission **Django Admin থেকেই** পরিবর্তন করা যাবে; API-এর authorization layer একই থাকবে।

------
হ্যাঁ — **যদি `permissions.py`-এর `RBACModelPermissions`-এর কথা বলেন, তাহলে একই permission class সব Model/ViewSet-এর জন্য ব্যবহার করতে পারবেন।** আলাদা আলাদা model-এর জন্য আলাদা `permissions.py` লাগবে না।

 ### Recommended structure

 একটা common permission file রাখুন:

```
project/
├── config/
├── common/
│   ├── __init__.py
│   └── permissions.py
│
├── accounts/
├── products/
├── orders/
└── customers/
```

 `common/permissions.py`:

```
from rest_framework.permissions import DjangoModelPermissions

class RBACModelPermissions(DjangoModelPermissions):

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

 তারপর **যেকোনো ViewSet-এ একই class** ব্যবহার করবেন।

 ### Product

```
from common.permissions import RBACModelPermissions

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    permission_classes = [RBACModelPermissions]
```

 ### Order

```
from common.permissions import RBACModelPermissions

class OrderViewSet(ModelViewSet):
    queryset = Order.objects.all()
    serializer_class = OrderSerializer
    permission_classes = [RBACModelPermissions]
```

 ### Customer

```
from common.permissions import RBACModelPermissions

class CustomerViewSet(ModelViewSet):
    queryset = Customer.objects.all()
    serializer_class = CustomerSerializer
    permission_classes = [RBACModelPermissions]
```

 এখানে magic অংশটা হলো:

```
"%(app_label)s.view_%(model_name)s"
```

 Django নিজে ViewSet-এর model অনুযায়ী permission বের করবে।

 যেমন `ProductViewSet` হলে:

```
products.view_product
products.add_product
products.change_product
products.delete_product
```

 `OrderViewSet` হলে:

```
orders.view_order
orders.add_order
orders.change_order
orders.delete_order
```

 `CustomerViewSet` হলে:

```
customers.view_customer
customers.add_customer
customers.change_customer
customers.delete_customer
```

 তাই **একটা common `RBACModelPermissions` পুরো project-এর সব standard CRUD ViewSet-এ reuse করা যায়।**

 ### তবে কখন আলাদা permission লাগবে?

 যদি কোনো বিশেষ business rule থাকে:

```
Product → standard CRUD permission
Order → standard CRUD permission
Invoice → standard CRUD permission
```

 তাহলে একই class যথেষ্ট।

 কিন্তু:

```
POST /orders/1/cancel/
POST /products/1/approve/
POST /users/1/activate/
```

 এগুলো custom action। এগুলোর জন্য custom permission লাগতে পারে:

```
class CanApproveProduct(BasePermission):
    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.approve_product"
        )
```

 **সুতরাং architecture হিসেবে আমি বলব:**

```
common/
└── permissions.py
      ├── RBACModelPermissions      ← সব CRUD ViewSet
      ├── CanApproveProduct          ← special action
      ├── CanCancelOrder             ← special action
      └── ...
```

 এতে project বড় হলেও permission logic centralized এবং maintain করা সহজ হবে।

----
হ্যাঁ, **এই ধরনের custom permission আপনি যত ইচ্ছা তৈরি করতে পারবেন**। এগুলো Django-এর built-in `view/add/change/delete` permission-এর বাইরে **business-specific action control** করার জন্য ব্যবহার করা হয়।

 ## 1\. কেন `approve_product` permission লাগবে?

 Django automatically দেয়:

```
products.view_product
products.add_product
products.change_product
products.delete_product
```

 কিন্তু আপনার business-এ যদি থাকে:

```
Product approve
Product reject
Product publish
Product archive
```

 এগুলো CRUD operation না। তাই custom permission তৈরি করবেন।

 যেমন:

```
class Product(models.Model):
    name = models.CharField(max_length=255)

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
            ("publish_product", "Can publish product"),
        ]
```

 তারপর:

```
python manage.py makemigrations
python manage.py migrate
```

 এখন Django Admin-এ এই permissions দেখতে পাবেন।

---

 ## 2\. Admin থেকে Role-এ permission দেবেন

 ধরুন:

```
Manager
 ├── Can view product
 ├── Can add product
 ├── Can change product
 └── Can approve product
```

 আর:

```
Editor
 ├── Can view product
 ├── Can add product
 ├── Can change product
 └── Can publish product
```

 এখন Manager `approve` করতে পারবে, কিন্তু Editor পারবে না।

---

 ## 3\. API-তে permission check

```
from rest_framework.permissions import BasePermission

class CanApproveProduct(BasePermission):

    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.approve_product"
        )
```

 তারপর ViewSet:

```
from rest_framework.decorators import action
from rest_framework.response import Response

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    @action(
        detail=True,
        methods=["post"],
        permission_classes=[CanApproveProduct],
    )
    def approve(self, request, pk=None):

        product = self.get_object()

        # approval logic
        product.is_approved = True
        product.save()

        return Response({
            "message": "Product approved"
        })
```

 এখন:

```
POST /api/products/10/approve/
```

 করলে প্রথমে:

```
request.user.has_perm(
    "products.approve_product"
)
```

 check হবে।

 Permission থাকলে → API চলবে।

 Permission না থাকলে → `403 Forbidden`।

---

 ## 4\. কত ধরনের custom permission করতে পারবেন?

 প্রায় যতগুলো business action আপনার application-এ আছে।

 উদাহরণ:

```
class Product(models.Model):

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
            ("publish_product", "Can publish product"),
            ("archive_product", "Can archive product"),
        ]
```

 Order-এর জন্য:

```
class Order(models.Model):

    class Meta:
        permissions = [
            ("confirm_order", "Can confirm order"),
            ("cancel_order", "Can cancel order"),
            ("refund_order", "Can refund order"),
            ("ship_order", "Can ship order"),
        ]
```

 Invoice:

```
class Invoice(models.Model):

    class Meta:
        permissions = [
            ("approve_invoice", "Can approve invoice"),
            ("void_invoice", "Can void invoice"),
            ("send_invoice", "Can send invoice"),
        ]
```

---

 ## 5\. একটা গুরুত্বপূর্ণ পার্থক্য

 ### CRUD permission

 Django automatically:

```
view
add
change
delete
```

 এগুলো সাধারণ database CRUD operation-এর জন্য।

 ### Custom permission

 আপনার business action:

```
approve
reject
publish
cancel
refund
confirm
archive
restore
```

 এগুলোর জন্য।

 অর্থাৎ:

```
                    Permissions
                         │
             ┌───────────┴───────────┐
             │                       │
         CRUD permissions       Custom permissions
             │                       │
       view/add/change/delete   approve/reject/publish
                                 cancel/refund/etc.
```

---

 ## 6\. সবচেয়ে ভালো ব্যাপার

 আপনাকে permission hard-code করে রাখতে হবে না।

 Django Admin থেকেই:

```
Manager
 ├── view_product
 ├── change_product
 ├── approve_product
 └── publish_product
```

 অথবা:

```
Sales
 ├── view_product
 └── publish_product
```

 এভাবে role তৈরি করতে পারবেন।

 তারপর API শুধু check করবে:

```
request.user.has_perm("products.approve_product")
```

 এতে **Role definition Admin-এর হাতে**, আর **authorization enforcement API-এর হাতে** থাকে।

 আপনার মতো project-এ আমি সাধারণত **CRUD-এর জন্য একটি common `RBACModelPermissions` \+ special business actions-এর জন্য custom permissions** এই দুইটা একসাথে ব্যবহার করব।

----
হ্যাঁ। `Model.Meta`-এ custom permission লেখার পর কয়েকটা step আছে। পুরো flow-টা দেখুন।

 ## 1\. Model-এ permission তৈরি করুন

```
# products/models.py

from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=255)
    is_approved = models.BooleanField(default=False)

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
        ]
```

---

 ## 2\. Migration তৈরি করুন

```
python manage.py makemigrations
```

 তারপর:

```
python manage.py migrate
```

 এতেই Django database-এ এই permissions তৈরি করবে:

```
products.approve_product
products.reject_product
```

---

 ## 3\. Django Admin-এ Group-এ permission দিন

 Admin → **Groups** → আপনার Role/Group:

```
Manager

Products:
☑ Can view product
☑ Can add product
☑ Can change product
☑ Can approve product
☑ Can reject product
```

 Save করুন।

 তারপর User-কে সেই Group-এ রাখুন:

```
User: Rahim

Groups:
☑ Manager
```

 এখন Rahim-এর কাছে `approve_product` permission আছে।

---

 ## 4\. Permission class তৈরি করুন

 `permissions.py`:

```
from rest_framework.permissions import BasePermission

class CanApproveProduct(BasePermission):

    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.approve_product"
        )
```

 এখানে:

```
"products.approve_product"
```

 এর `products` হলো **app label**, আর `approve_product` হলো আপনার `Meta.permissions`-এ দেওয়া codename।

---

 ## 5\. ViewSet-এর custom action-এ ব্যবহার করুন

```
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer
from .permissions import CanApproveProduct

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    @action(
        detail=True,
        methods=["post"],
        permission_classes=[CanApproveProduct],
    )
    def approve(self, request, pk=None):

        product = self.get_object()

        product.is_approved = True
        product.save(update_fields=["is_approved"])

        return Response({
            "message": "Product approved successfully"
        })
```

 এখন endpoint হবে:

```
POST /api/products/10/approve/
```

 Request আসলে:

```
JWT
 ↓
request.user
 ↓
CanApproveProduct
 ↓
has_perm("products.approve_product")
 ↓
Permission আছে?
 ├── YES → approve()
 └── NO  → 403 Forbidden
```

---

 ## 6\. Test করুন

 ধরুন `Manager` Group-এ:

```
✓ Can approve product
```

 আছে।

 Rahim Manager-এর member।

 তাহলে:

```
POST /api/products/10/approve/
Authorization: Bearer <access_token>
```

 → **200 OK**

 কিন্তু Karim-এর Group-এ `approve_product` নেই:

```
POST /api/products/10/approve/
Authorization: Bearer <karim_token>
```

 → **403 Forbidden**

---

 ## 7\. একাধিক custom permission হলে

 ধরুন:

```
class Product(models.Model):

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
            ("publish_product", "Can publish product"),
        ]
```

 তাহলে আলাদা permission class করতে পারেন:

```
class CanApproveProduct(BasePermission):
    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.approve_product"
        )

class CanRejectProduct(BasePermission):
    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.reject_product"
        )

class CanPublishProduct(BasePermission):
    def has_permission(self, request, view):
        return request.user.has_perm(
            "products.publish_product"
        )
```

 তারপর:

```
@action(
    detail=True,
    methods=["post"],
    permission_classes=[CanApproveProduct],
)
def approve(self, request, pk=None):
    ...

@action(
    detail=True,
    methods=["post"],
    permission_classes=[CanRejectProduct],
)
def reject(self, request, pk=None):
    ...

@action(
    detail=True,
    methods=["post"],
    permission_classes=[CanPublishProduct],
)
def publish(self, request, pk=None):
    ...
```

 ### সংক্ষেপে আপনার কাজ

```
1. Model.Meta → permissions লিখবেন
             ↓
2. makemigrations
             ↓
3. migrate
             ↓
4. Django Admin → Group → permission assign
             ↓
5. User → Group assign
             ↓
6. DRF permission class → has_perm()
             ↓
7. ViewSet @action → permission_classes
```

 **একটা জিনিস মনে রাখবেন:** `Meta.permissions` লিখলেই API protected হয় না। সেটা শুধু Django permission তৈরি করে। **ViewSet-এর custom action-এ `permission_classes` দিয়ে সেই permission enforce করতে হবে।**


----
হ্যাঁ। একজন user-কে অনেকগুলো permission দেওয়ার **দুইটা clean উপায়** আছে।

 ## 1\. Group/Role দিয়ে — Recommended

 ধরুন একজন user-এর এই permissionগুলো দরকার:

```
Product:
✓ view_product
✓ add_product
✓ change_product
✓ approve_product

Order:
✓ view_order
✓ change_order
✓ confirm_order

Invoice:
✓ view_invoice
✓ send_invoice
```

 একজন একজন করে user-কে এতগুলো permission দেওয়ার দরকার নেই।

 Django Admin → **Groups** → `Manager`

 সেখানে সব permission select করুন:

```
Manager
├── Product
│   ├── ✓ view
│   ├── ✓ add
│   ├── ✓ change
│   └── ✓ approve
│
├── Order
│   ├── ✓ view
│   ├── ✓ change
│   └── ✓ confirm
│
└── Invoice
    ├── ✓ view
    └── ✓ send
```

 তারপর:

 **Users → Rahim → Groups → Manager**

 দিলেই Rahim সব permission পেয়ে যাবে।

 এটাই সবচেয়ে ভালো যখন একই permission set অনেক user-এর থাকবে।

---

 ## 2\. সরাসরি User-কে permission দেওয়া

 যদি শুধু একজন specific user-এর জন্য permissions দিতে চান:

 **Admin → Users → Rahim → User permissions**

 তারপর multiple permission select করতে পারবেন:

```
User permissions

✓ products | Can view product
✓ products | Can add product
✓ products | Can change product
✓ products | Can approve product
✓ orders | Can view order
✓ orders | Can confirm order
✓ invoices | Can view invoice
```

 Save করলেই সবগুলো ওই user-এর direct permissions হয়ে যাবে।

---

 ## 3\. Group + Direct permission একসাথেও ব্যবহার করা যায়

 ধরুন:

```
Rahim
├── Group: Manager
│     ├── view_product
│     ├── add_product
│     └── change_product
│
└── Direct permissions
      └── approve_product
```

 তাহলে Rahim-এর effective permissions হবে:

```
view_product
add_product
change_product
approve_product
```

 অর্থাৎ Group-এর permission এবং user-এর direct permission **দুটোই কাজ করবে**।

---

 ## 4\. আপনার project-এর জন্য কোনটা ব্যবহার করবেন?

 আমি এই pattern রাখতাম:

```
                    Django Admin
                         │
              ┌──────────┴──────────┐
              │                     │
            Group                 User
           (Role)             Direct Permission
              │                     │
              └──────────┬──────────┘
                         ↓
                  Effective Permission
                         ↓
                    DRF Permission
                         ↓
                       ViewSet
```

 **একই ধরনের access অনেক user-এর হলে → Group/Role**

 **একজন user-এর exceptional access হলে → Direct permission**

 যেমন:

```
Manager role
  → 20টা permission

100 জন Manager user
  → শুধু Manager group assign

Rahim-এর extra permission
  → Direct permission হিসেবে add
```

 এভাবে করলে পরে permission পরিবর্তন করাও অনেক সহজ হবে।


----
অবশ্যই। নিচে **Django + DRF + JWT \+ Django Admin Group/Role + Model Permission \+ Custom Permission**-এর পুরো বিষয়টা একসাথে summary দিলাম।

 # Django REST API — Complete RBAC Summary

 আপনার architecture হবে:

```
JWT Login
   ↓
Authentication
   ↓
request.user
   ↓
User + Groups
   ↓
Django Permissions
   ↓
DRF Permission Class
   ↓
ViewSet
   ↓
API
```

 ## 1\. Group = Role

 Django-তে আলাদা `Role` model বানানোর দরকার নেই, যদি আপনার requirement সাধারণ RBAC হয়।

 Django-এর:

```
Group
```

 কেই:

```
Role
```

 হিসেবে ব্যবহার করবেন।

 উদাহরণ:

```
Viewer
Editor
Manager
Accountant
Admin
```

---

 ## 2\. Model তৈরি করলে Django automatic CRUD permissions দেয়

 ধরুন:

```
class Product(models.Model):
    name = models.CharField(max_length=255)
```

 Django automatically তৈরি করবে:

```
products.view_product
products.add_product
products.change_product
products.delete_product
```

 Migration:

```
python manage.py makemigrations
python manage.py migrate
```

---

 # 3\. Custom business permission

 CRUD-এর বাইরে কোনো action থাকলে `Meta.permissions` ব্যবহার করবেন।

```
class Product(models.Model):
    name = models.CharField(max_length=255)

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
            ("publish_product", "Can publish product"),
        ]
```

 তারপর:

```
python manage.py makemigrations
python manage.py migrate
```

 এখন Django Admin-এ পাবেন:

```
Can approve product
Can reject product
Can publish product
```

 Custom permission সাধারণত এগুলোর জন্য:

```
approve
reject
publish
archive
restore
cancel
confirm
refund
verify
```

---

 # 4\. Group-এ permission assign করবেন

 Admin:

```
/admin/
   ↓
Groups
   ↓
Manager
```

 Manager-এর permissions:

```
Product
├── ✓ view_product
├── ✓ add_product
├── ✓ change_product
├── ✓ approve_product
└── ✗ delete_product

Order
├── ✓ view_order
├── ✓ change_order
└── ✓ confirm_order
```

 এখানে `Manager` আপনার Role।

---

 # 5\. User-কে Group assign করবেন

 Admin:

```
Users
   ↓
Rahim
   ↓
Groups
   ↓
✓ Manager
```

 এখন Rahim Manager-এর সব permission পাবে।

 অর্থাৎ:

```
Rahim
   ↓
Manager Group
   ↓
Manager Permissions
```

---

 # 6\. একজন user-কে অনেক permission দেওয়ার সবচেয়ে ভালো উপায়

 যদি একই permission অনেক user-এর লাগে:

```
Group/Role ব্যবহার করুন
```

 যেমন:

```
Manager
  ├── view_product
  ├── add_product
  ├── change_product
  ├── approve_product
  ├── view_order
  ├── change_order
  └── confirm_order
```

 তারপর 100 জন Manager user-কে শুধু:

```
Manager
```

 group assign করবেন।

 **একজন একজন করে permission দেওয়ার দরকার নেই।**

---

 # 7\. Direct User Permission-ও দেওয়া যায়

 কোনো specific user-এর extra permission দরকার হলে:

```
User
  ↓
User permissions
```

 থেকে সরাসরি দিতে পারবেন।

 যেমন:

```
Rahim
 ├── Group: Manager
 │
 └── Direct permission:
       └── delete_product
```

 তাহলে Rahim Manager-এর permission + direct `delete_product`—দুটোই পাবে।

---

 # 8\. Common permission.py

 সব CRUD ViewSet-এর জন্য একই permission class ব্যবহার করতে পারবেন।

```
from rest_framework.permissions import DjangoModelPermissions

class RBACModelPermissions(DjangoModelPermissions):

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

 একটা common জায়গায় রাখুন:

```
common/
└── permissions.py
```

---

 # 9\. ViewSet-এ permission বসাবেন

```
from rest_framework.viewsets import ModelViewSet

from common.permissions import RBACModelPermissions

from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]
```

 একই permission class:

```
ProductViewSet
OrderViewSet
CustomerViewSet
InvoiceViewSet
PaymentViewSet
```

 সব জায়গায় ব্যবহার করা যাবে।

---

 # 10\. HTTP method → permission mapping

 আপনার common permission class অনুযায়ী:

```
GET
 ↓
view_product
```

```
POST
 ↓
add_product
```

```
PUT
 ↓
change_product
```

```
PATCH
 ↓
change_product
```

```
DELETE
 ↓
delete_product
```

 Order হলে Django automatically `order` permission খুঁজবে:

```
GET     → orders.view_order
POST    → orders.add_order
PUT     → orders.change_order
PATCH   → orders.change_order
DELETE  → orders.delete_order
```

---

 # 11\. Custom action-এর জন্য custom permission

 ধরুন:

```
POST /products/1/approve/
```

 এটা normal CRUD না।

 তাই:

```
from rest_framework.permissions import BasePermission

class CanApproveProduct(BasePermission):

    def has_permission(self, request, view):

        return request.user.has_perm(
            "products.approve_product"
        )
```

 তারপর:

```
from rest_framework.decorators import action
from rest_framework.response import Response

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]

    @action(
        detail=True,
        methods=["post"],
        permission_classes=[CanApproveProduct],
    )
    def approve(self, request, pk=None):

        product = self.get_object()

        product.is_approved = True
        product.save(
            update_fields=["is_approved"]
        )

        return Response({
            "message": "Product approved"
        })
```

 এখন:

```
POST /api/products/1/approve/
```

 করলে:

```
request.user.has_perm(
    "products.approve_product"
)
```

 check হবে।

---

 # 12\. JWT Authentication

 `settings.py`:

```
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),

    "DEFAULT_PERMISSION_CLASSES": (
        "rest_framework.permissions.IsAuthenticated",
    ),
}
```

 JWT:

```
from datetime import timedelta

SIMPLE_JWT = {

    "ACCESS_TOKEN_LIFETIME": timedelta(
        minutes=15
    ),

    "REFRESH_TOKEN_LIFETIME": timedelta(
        days=7
    ),

    "ROTATE_REFRESH_TOKENS": True,

    "BLACKLIST_AFTER_ROTATION": True,

    "AUTH_HEADER_TYPES": (
        "Bearer",
    ),
}
```

---

 # 13\. Login

 URL:

```
POST /api/auth/login/
```

 Body:

```
{
    "username": "rahim",
    "password": "your-password"
}
```

 Response:

```
{
    "refresh": "xxxxx",
    "access": "xxxxx"
}
```

 তারপর API request:

```
Authorization: Bearer <access_token>
```

 DRF JWT থেকে user বের করবে:

```
JWT
 ↓
Rahim
 ↓
Rahim's Groups
 ↓
Manager
 ↓
Manager's Permissions
 ↓
Permission Check
```

---

 # 14\. `settings.py`-এর core setup

 শেষ পর্যন্ত মূল configuration হবে:

```
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "rest_framework",

    "accounts",
    "products",
]
```

 তারপর:

```
AUTH_USER_MODEL = "accounts.User"
```

 এবং:

```
REST_FRAMEWORK = {

    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),

    "DEFAULT_PERMISSION_CLASSES": (
        "rest_framework.permissions.IsAuthenticated",
    ),
}
```

---

 # 15\. Folder structure

 আমি project-এ এভাবে রাখতাম:

```
myproject/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── common/
│   ├── __init__.py
│   └── permissions.py
│
├── accounts/
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   └── views.py
│
├── products/
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   ├── views.py
│   └── permissions.py
│
├── orders/
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   ├── urls.py
│   └── views.py
│
└── requirements.txt
```

 `common/permissions.py`:

```
RBACModelPermissions
```

 আর app-specific special permission হলে সেই app-এর `permissions.py`:

```
products/permissions.py
orders/permissions.py
```

---

 # 16\. Authentication vs Authorization

 দুটোকে আলাদা করে মনে রাখবেন।

 ### Authentication

 > **কে?**

 JWT:

```
JWT → Rahim
```

 ### Authorization

 > **Rahim কী করতে পারবে?**

 Django permissions:

```
Rahim
 ↓
Manager
 ↓
change_product
 ↓
ALLOW
```

---

 # 17\. Object-level permission

 Model permission বলছে:

```
Rahim → change_product ✓
```

 এর মানে সাধারণভাবে Product model-এর change operation করতে পারে।

 কিন্তু business rule হতে পারে:

 > Rahim শুধু নিজের product edit করতে পারবে।

 তখন আলাদা object-level logic লাগবে।

 যেমন:

```
def get_queryset(self):

    if self.request.user.is_superuser:
        return Product.objects.all()

    return Product.objects.filter(
        created_by=self.request.user
    )
```

 অর্থাৎ:

```
Model permission
+
Object ownership
```

 দুটো আলাদা concept।

---

 # 18\. Production-এর জন্য সবচেয়ে গুরুত্বপূর্ণ structure

 শেষ পর্যন্ত আপনার authorization এমন:

```
                       REQUEST
                          │
                          ▼
                    JWT Authentication
                          │
                          ▼
                     request.user
                          │
              ┌───────────┴───────────┐
              │                       │
          User Groups             Direct User
              │                   Permissions
              │                       │
              └───────────┬───────────┘
                          ▼
                  Django Permissions
                          │
              ┌───────────┴───────────┐
              │                       │
          CRUD Permission        Custom Permission
              │                       │
      view/add/change/delete    approve/reject/etc.
              │                       │
              └───────────┬───────────┘
                          ▼
                   DRF Permission
                          │
                          ▼
                       ViewSet
                          │
                          ▼
                Object-level checks
                          │
                          ▼
                       Database
```

 ## Bottom line

 আপনার জন্য সবচেয়ে clean approach:

```
Django Group
    =
Role
```

```
Django Model Permissions
    =
CRUD authorization
```

```
Meta.permissions
    =
Business-specific authorization
```

```
DjangoModelPermissions
    =
CRUD permission enforcement in DRF
```

```
Custom BasePermission
    =
approve/reject/publish/refund/etc.
```

```
JWT
    =
Authentication
```

```
User
    =
Group permissions + Direct permissions
```

 আর সবচেয়ে গুরুত্বপূর্ণ হলো: **Role/permission management Django Admin-এ করবেন, কিন্তু permission enforcement সবসময় backend/API-তে করবেন।** Frontend-এ শুধু button hide/show করা security নয়।


----
হ্যাঁ, **মোটামুটি ঠিক বুঝেছেন**—তবে একটা ছোট correction আছে।

 `role` field দিয়েও API-level access control করা যায়, কিন্তু সেটা **নিজে থেকে কোনো permission system নয়**। আপনাকে manually code করে check করতে হবে।

 অন্যদিকে Django `Group` \+ `Permission` ব্যবহার করলে Django/DRF-এর built-in permission system ব্যবহার করে **API endpoint পর্যন্ত authorization** করা যায়।

 ### `role` field

```
if request.user.role == "manager":
    # allow
```

 এখানে আপনাকে manually define করতে হবে:

```
manager → কোন API?
editor  → কোন API?
viewer  → কোন API?
```

 এটা বড় project-এ maintain করা কঠিন হতে পারে।

 ### Group \+ Permission

```
User
 ↓
Manager Group
 ↓
Permissions
 ├── view_product
 ├── add_product
 ├── change_product
 └── approve_product
 ↓
DRF ViewSet
 ↓
API access
```

 ViewSet:

```
permission_classes = [RBACModelPermissions]
```

 তখন:

```
GET /products/
    ↓
view_product?

POST /products/
    ↓
add_product?

PATCH /products/1/
    ↓
change_product?

POST /products/1/approve/
    ↓
approve_product?
```

 অর্থাৎ **Group → Permission → API endpoint/action** পর্যন্ত খুব cleanভাবে নিয়ে যেতে পারবেন।

 ### সবচেয়ে ভালো design

```
User
 │
 ├── Groups = Role
 │      │
 │      └── Permissions
 │             │
 │             └── API authorization
 │
 └── Other business fields
```

 তাই আপনার বর্তমান **JWT + DRF RBAC** architecture-এ:

 > **Role হিসেবে Django Group ব্যবহার করুন, এবং API access-এর জন্য Django Permissions ব্যবহার করুন।**

 আলাদা `role` field শুধু তখন রাখবেন যখন role-এর **business meaning** আছে, যেমন `customer/seller/employee`—শুধু API permission-এর জন্য নয়।



---

হ্যাঁ। আপনি যদি **Django default Admin Panel ব্যবহার না করে নিজের frontend/dashboard থেকে Group-এর permission manage করতে চান**, সেটাও করা যায়। Django-এর built-in `Group` এবং `Permission` model-ই backend হিসেবে ব্যবহার করবেন; শুধু নিজের API/UI বানাবেন।

 ## Architecture

```
Your Dashboard
      ↓
Role Management API
      ↓
Django Group
      ↓
Django Permission
      ↓
User
      ↓
Normal API authorization
```

 উদাহরণ:

```
Dashboard → Roles

Manager
├── Products
│   ├── ☑ View
│   ├── ☑ Add
│   ├── ☑ Change
│   ├── ☐ Delete
│   └── ☑ Approve
│
└── Orders
    ├── ☑ View
    ├── ☑ Change
    └── ☑ Confirm
```

 Frontend শুধু checkbox দেখাবে। Backend-এ Django-এর `Group`/`Permission` update হবে।

---

 # 1\. Django-এর built-in Group/Permission ব্যবহার করুন

 আলাদা `Role` বা `GroupPermission` model বানানোর দরকার নেই।

```
from django.contrib.auth.models import Group, Permission
```

 Django database-এ already থাকে:

```
auth_group
auth_permission
```

 এবং relationship:

```
Group
  ↓
Permissions
```

---

 # 2\. Role list API

 ধরুন dashboard-এ সব role দেখাবেন।

```
from django.contrib.auth.models import Group
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAdminUser

class RoleListView(APIView):

    permission_classes = [IsAdminUser]

    def get(self, request):

        groups = Group.objects.all()

        data = [
            {
                "id": group.id,
                "name": group.name,
            }
            for group in groups
        ]

        return Response(data)
```

 Response:

```
[
    {
        "id": 1,
        "name": "Manager"
    },
    {
        "id": 2,
        "name": "Editor"
    },
    {
        "id": 3,
        "name": "Viewer"
    }
]
```

---

 # 3\. Permission list API

 Dashboard-এ checkbox বানানোর জন্য permissions দরকার।

```
from django.contrib.auth.models import Permission
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAdminUser

class PermissionListView(APIView):

    permission_classes = [IsAdminUser]

    def get(self, request):

        permissions = Permission.objects.select_related(
            "content_type"
        ).all()

        data = [
            {
                "id": permission.id,
                "name": permission.name,
                "codename": permission.codename,
                "app_label": permission.content_type.app_label,
                "model": permission.content_type.model,
            }
            for permission in permissions
        ]

        return Response(data)
```

 তখন frontend এমন data পাবে:

```
[
    {
        "id": 1,
        "name": "Can add product",
        "codename": "add_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 2,
        "name": "Can change product",
        "codename": "change_product",
        "app_label": "products",
        "model": "product"
    }
]
```

---

 # 4\. Dashboard থেকে Group create

 Frontend:

```
Create Role

Role Name:
[ Manager ]

[ Save ]
```

 Backend:

```
from django.contrib.auth.models import Group

group = Group.objects.create(
    name="Manager"
)
```

 API:

```
POST /api/admin/roles/
```

 Body:

```
{
    "name": "Manager"
}
```

---

 # 5\. Group-এর permission update

 এটাই সবচেয়ে গুরুত্বপূর্ণ অংশ।

 Frontend থেকে পাঠাবেন:

```
{
    "permission_ids": [
        1,
        2,
        5,
        8,
        10
    ]
}
```

 Backend:

```
from django.contrib.auth.models import Group, Permission
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAdminUser

class RolePermissionUpdateView(APIView):

    permission_classes = [IsAdminUser]

    def put(self, request, pk):

        group = Group.objects.get(pk=pk)

        permission_ids = request.data.get(
            "permission_ids",
            []
        )

        permissions = Permission.objects.filter(
            id__in=permission_ids
        )

        group.permissions.set(permissions)

        return Response({
            "message": "Permissions updated successfully"
        })
```

 এখানে:

```
group.permissions.set(permissions)
```

 এর ফলে Group-এর পুরনো permissions replace হয়ে নতুন permissions set হবে।

---

 # 6\. Existing permissions দেখানো

 Dashboard খুললে আপনি চাইবেন:

```
Manager

Product
☑ View
☑ Add
☑ Change
☐ Delete
☑ Approve
```

 এর জন্য:

```
group.permissions.all()
```

 ব্যবহার করবেন।

```
permissions = group.permissions.all()
```

 Frontend-এর জন্য permission ID পাঠাতে পারেন:

```
permission_ids = list(
    group.permissions.values_list(
        "id",
        flat=True
    )
)
```

 Response:

```
{
    "id": 1,
    "name": "Manager",
    "permission_ids": [
        1,
        2,
        5,
        8
    ]
}
```

 Frontend এই ID অনুযায়ী checkbox checked করবে।

---

 # 7\. User → Role assign

 এখন dashboard-এ:

```
Users

Rahim
Role:
[ Manager ▼ ]

[ Save ]
```

 Backend:

```
from django.contrib.auth.models import Group

user.groups.set([
    Group.objects.get(name="Manager")
])
```

 অথবা existing group add করতে:

```
user.groups.add(group)
```

 একাধিক role/group রাখতে চাইলে:

```
user.groups.add(
    manager_group,
    report_group
)
```

---

 # 8\. তারপর API permission আগের মতোই থাকবে

 এখানে খুব সুন্দর বিষয় হলো:

 **Dashboard custom হলেও আপনার API permission system পরিবর্তন করতে হবে না।**

 আগের:

```
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]
```

 এটাই থাকবে।

 Dashboard শুধু Django-এর:

```
Group
   ↓
Permission
```

 update করবে।

 তারপর ViewSet:

```
request.user.has_perm(
    "products.change_product"
)
```

 check করবে।

---

 # 9\. Custom permission-ও dashboard-এ দেখাতে পারবেন

 Model:

```
class Product(models.Model):

    class Meta:
        permissions = [
            (
                "approve_product",
                "Can approve product"
            ),
            (
                "reject_product",
                "Can reject product"
            ),
        ]
```

 Migration:

```
python manage.py makemigrations
python manage.py migrate
```

 তারপর Django `Permission` table-এ এগুলো থাকবে।

 আপনার permission API automatically এগুলোও return করবে:

```
{
    "name": "Can approve product",
    "codename": "approve_product",
    "app_label": "products"
}
```

 তাই dashboard-এ:

```
Product

☑ View
☑ Add
☑ Change
☐ Delete
☑ Approve
☐ Reject
```

 দেখাতে পারবেন।

---

 # 10\. আমি permission API একটু group করে রাখার পরামর্শ দেব

 Frontend-এর জন্য raw permission list-এর চেয়ে এই ধরনের response বেশি useful:

```
{
    "products": {
        "product": {
            "view": 1,
            "add": 2,
            "change": 3,
            "delete": 4,
            "approve": 5,
            "reject": 6
        }
    },
    "orders": {
        "order": {
            "view": 10,
            "add": 11,
            "change": 12,
            "delete": 13,
            "confirm": 14
        }
    }
}
```

 তাহলে React/Vue/Next.js dashboard সহজে render করতে পারবে:

```
Products
 └── Product
      ☑ View
      ☑ Add
      ☑ Change
      ☐ Delete
      ☑ Approve
      ☐ Reject

Orders
 └── Order
      ☑ View
      ☑ Change
      ☑ Confirm
```

---

 # 11\. Security — সবচেয়ে গুরুত্বপূর্ণ

 আপনার **Role/Permission management API নিজেই protected** হতে হবে।

 যেমন:

```
permission_classes = [
    IsAdminUser
]
```

 কিন্তু production RBAC-এ আমি শুধু `is_staff`-এর ওপর নির্ভর না করে আলাদা management permission রাখার পরামর্শ দেব।

 যেমন:

```
manage_roles
manage_permissions
assign_roles
```

 তারপর:

```
class CanManageRoles(BasePermission):

    def has_permission(self, request, view):

        return request.user.has_perm(
            "accounts.manage_roles"
        )
```

 তাহলে শুধু authorized administrator-ই dashboard থেকে Role/Permission পরিবর্তন করতে পারবে।

---

 # Final structure

 আপনার system এখন এমন হবে:

```
                    ADMIN DASHBOARD
                           │
             ┌─────────────┴─────────────┐
             │                           │
        Role Management            User Management
             │                           │
             ↓                           ↓
       Django Group                User.groups
             │
             ↓
       Django Permission
             │
      ┌──────┴───────┐
      │              │
    CRUD          Custom
 view/add/      approve/reject/
 change/delete  publish/etc.
      │              │
      └──────┬───────┘
             ↓
        DRF Permission
             ↓
          ViewSet
             ↓
           API
```

 অর্থাৎ **Django Admin UI বাদ দিলেও Django-এর `Group` এবং `Permission` বাদ দিতে হবে না।** আপনার নিজের Dashboard হবে management interface, আর Django-এর built-in authorization system থাকবে backend-এর মূল RBAC engine হিসেবে।

 এই approach-টাই আপনার বর্তমান **`role` = user type + `group` = API authorization** design-এর সাথে সবচেয়ে cleanভাবে মিলে যায়।

হ্যাঁ। Django model-এর `view/add/change/delete` permission **automatic generate হবে**। আপনি শুধু `Permission` table থেকে list এনে API দিয়ে frontend dashboard-এ দেখাতে পারেন।

 ## 1\. Permission API

```
# accounts/views.py

from django.contrib.auth.models import Permission
from rest_framework.viewsets import ReadOnlyModelViewSet
from rest_framework.permissions import IsAdminUser

from .serializers import PermissionSerializer

class PermissionViewSet(ReadOnlyModelViewSet):

    queryset = Permission.objects.select_related(
        "content_type"
    ).order_by(
        "content_type__app_label",
        "content_type__model",
        "codename",
    )

    serializer_class = PermissionSerializer

    permission_classes = [IsAdminUser]
```

 এটা শুধু **read/list** করবে।

---

 ## 2\. Serializer

```
# accounts/serializers.py

from django.contrib.auth.models import Permission
from rest_framework import serializers

class PermissionSerializer(serializers.ModelSerializer):

    app_label = serializers.CharField(
        source="content_type.app_label",
        read_only=True
    )

    model = serializers.CharField(
        source="content_type.model",
        read_only=True
    )

    class Meta:
        model = Permission
        fields = [
            "id",
            "name",
            "codename",
            "app_label",
            "model",
        ]
```

---

 ## 3\. URL

```
# accounts/urls.py

from rest_framework.routers import DefaultRouter

from .views import PermissionViewSet

router = DefaultRouter()

router.register(
    "permissions",
    PermissionViewSet,
    basename="permissions"
)

urlpatterns = router.urls
```

 তাহলে API:

```
GET /api/admin/permissions/
```

---

 ## 4\. Response

 ধরুন আপনার project-এ `Product` এবং `Order` model আছে।

 API থেকে এমন data আসবে:

```
[
    {
        "id": 1,
        "name": "Can add product",
        "codename": "add_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 2,
        "name": "Can change product",
        "codename": "change_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 3,
        "name": "Can delete product",
        "codename": "delete_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 4,
        "name": "Can view product",
        "codename": "view_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 5,
        "name": "Can add order",
        "codename": "add_order",
        "app_label": "orders",
        "model": "order"
    }
]
```

 আপনার custom permission থাকলে সেটাও automatically আসবে:

```
class Product(models.Model):

    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
            ("reject_product", "Can reject product"),
        ]
```

 তাহলে list-এ:

```
approve_product
reject_product
```

 এগুলোও পাবেন।

---

 ## 5\. Frontend-এ সুন্দরভাবে দেখাবেন

 API থেকে flat list আসলেও frontend-এ group করে দেখাতে পারেন:

```
Products
├── ☑ View
├── ☑ Add
├── ☐ Change
├── ☐ Delete
├── ☑ Approve
└── ☐ Reject

Orders
├── ☑ View
├── ☐ Add
├── ☐ Change
└── ☐ Delete
```

 অর্থাৎ Django Admin ব্যবহার করার দরকার নেই।

```
Django Model
     ↓
Django automatically creates Permission
     ↓
Permission table
     ↓
GET /api/admin/permissions/
     ↓
Your Admin Dashboard
     ↓
Checkbox
```

 **একটা জিনিস খেয়াল রাখবেন:** `Permission` list endpoint-এ `POST/PUT/DELETE` দেওয়ার দরকার নেই। Permission definition Django নিজেই manage করবে; আপনার dashboard শুধু **দেখবে**, আর `Group` API দিয়ে কোন permission কোন role-এ থাকবে সেটা manage করবে।হ্যাঁ, **API দিয়ে Group-এর permission change করা যাবে**।
 
  তবে **`Permission` নিজে edit করবেন না**; কোন `Group/Role` কোন permission পাবে, সেটাই API দিয়ে change করবেন।

 উদাহরণ:

```
PUT /api/admin/roles/1/permissions/
```

 Body:

```
{
  "permission_ids": [1, 2, 5, 8]
}
```

 Backend:

```
group.permissions.set(
    Permission.objects.filter(
        id__in=permission_ids
    )
)
```

 এর ফলে:

```
Manager
├── view_product      ✓
├── add_product       ✓
├── change_product    ✗
├── delete_product    ✗
└── approve_product   ✓
```

 API দিয়ে পরিবর্তন হয়ে যাবে।

 ### কিন্তু Permission definition আলাদা বিষয়

 Django automatically তৈরি করে:

```
view_product
add_product
change_product
delete_product
```

 এগুলোকে dashboard API দিয়ে:

```
❌ delete permission
❌ rename permission
❌ create arbitrary permission
```

 করার দরকার নেই।

 Custom permission হলে Model-এ define করবেন:

```
class Product(models.Model):
    class Meta:
        permissions = [
            ("approve_product", "Can approve product"),
        ]
```

 তারপর migration:

```
python manage.py makemigrations
python manage.py migrate
```

 এরপর আপনার API শুধু permission list দেখাবে এবং **Group-এর সাথে assign/unassign করবে**।

 ### সবচেয়ে clean flow

```
Model
 ↓
Django creates Permission
 ↓
GET /permissions/
 ↓
Admin Dashboard
 ↓
Select permissions
 ↓
PUT /roles/{id}/permissions/
 ↓
Django Group.permissions
 ↓
DRF ViewSet
 ↓
API access
```

 তাই **হ্যাঁ, API দিয়েই পুরো Role/Group permission management করা যাবে**, Django Admin Panel ছাড়াই।