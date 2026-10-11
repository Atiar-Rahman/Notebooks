হ্যাঁ। নিচে **Django + DRF দিয়ে Django Admin Panel ছাড়াই API-এর মাধ্যমে পুরো Role/Group + Permission Management**-এর একটা complete structure দিলাম।

এখানে design হবে:

```
User.role
    ↓
শুধু user type
(customer / seller / employee)

User.groups
    ↓
Role / API authorization group

Group.permissions
    ↓
API access

JWT
    ↓
Authentication
```

## 1. কী কী API থাকবে

```
ROLE / GROUP

GET    /api/admin/roles/
POST   /api/admin/roles/

GET    /api/admin/roles/{id}/
PATCH  /api/admin/roles/{id}/
DELETE /api/admin/roles/{id/


PERMISSIONS

GET    /api/admin/permissions/


ROLE ↔ PERMISSIONS

GET    /api/admin/roles/{id}/permissions/
PUT    /api/admin/roles/{id}/permissions/


USER ↔ ROLES

GET    /api/admin/users/{id}/roles/
PUT    /api/admin/users/{id}/roles/
```

Permission-এর নিজস্ব `POST/PUT/DELETE` রাখছি না, কারণ এগুলো Django model/migration থেকে তৈরি হবে।

---

# 2. Folder structure

```
project/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   └── urls.py
│
├── common/
│   ├── __init__.py
│   └── permissions.py
│
├── accounts/
│   ├── __init__.py
│   ├── admin.py
│   ├── models.py
│   ├── serializers.py
│   ├── permissions.py
│   ├── views.py
│   └── urls.py
│
└── products/
    ├── models.py
    ├── serializers.py
    └── views.py
```

---

# 3. User model

আপনি বলেছেন `role` শুধু user identify করার জন্য।

তাই:

```
# accounts/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):

    ROLE_CHOICES = [
        ("customer", "Customer"),
        ("seller", "Seller"),
        ("employee", "Employee"),
    ]

    role = models.CharField(
        max_length=20,
        choices=ROLE_CHOICES,
        default="customer",
    )
```

এখানে:

```
role = seller
```

শুধু বলছে user একজন seller।

**API permission-এর জন্য role ব্যবহার করব না।**

---

# 4. Product model

```
# products/models.py

from django.db import models


class Product(models.Model):

    name = models.CharField(
        max_length=255
    )

    is_approved = models.BooleanField(
        default=False
    )

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

Django automatically তৈরি করবে:

```
view_product
add_product
change_product
delete_product
approve_product
reject_product
```

Migration:

```
python manage.py makemigrations
python manage.py migrate
```

---

# 5. Permission list API

এখন database থেকে সব permission দেখাব।

```
# accounts/serializers.py

from django.contrib.auth.models import Group, Permission
from rest_framework import serializers


class PermissionSerializer(
    serializers.ModelSerializer
):

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

View:

```
# accounts/views.py

from django.contrib.auth.models import Permission
from rest_framework.viewsets import ReadOnlyModelViewSet
from rest_framework.permissions import IsAdminUser

from .serializers import PermissionSerializer


class PermissionViewSet(
    ReadOnlyModelViewSet
):

    queryset = Permission.objects.select_related(
        "content_type"
    ).order_by(
        "content_type__app_label",
        "content_type__model",
        "codename",
    )

    serializer_class = PermissionSerializer

    permission_classes = [
        IsAdminUser
    ]
```

API:

```
GET /api/admin/permissions/
```

Response:

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
        "name": "Can approve product",
        "codename": "approve_product",
        "app_label": "products",
        "model": "product"
    }
]
```

Frontend এই list দিয়ে checkbox বানাবে।

---

# 6. Role CRUD API

Django-এর `Group`-কেই Role হিসেবে ব্যবহার করব।

```
# accounts/serializers.py

class RoleSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Group
        fields = [
            "id",
            "name",
        ]
```

ViewSet:

```
# accounts/views.py

from django.contrib.auth.models import Group


class RoleViewSet(ModelViewSet):

    queryset = Group.objects.all().order_by(
        "name"
    )

    serializer_class = RoleSerializer

    permission_classes = [
        IsAdminUser
    ]
```

এতে automatically:

```
GET    /api/admin/roles/
POST   /api/admin/roles/

GET    /api/admin/roles/1/
PUT    /api/admin/roles/1/
PATCH  /api/admin/roles/1/
DELETE /api/admin/roles/1/
```

হয়ে যাবে।

---

# 7. Role create

Frontend:

```
POST /api/admin/roles/
```

```
{
    "name": "Manager"
}
```

Django তৈরি করবে:

```
Group
id = 1
name = Manager
```

---

# 8. Role-এর permission দেখানো

```
GET /api/admin/roles/1/permissions/
```

ViewSet:

```
from rest_framework.decorators import action
from rest_framework.response import Response


class RoleViewSet(ModelViewSet):

    queryset = Group.objects.all()
    serializer_class = RoleSerializer

    permission_classes = [
        IsAdminUser
    ]

    @action(
        detail=True,
        methods=["get"],
        url_path="permissions",
    )
    def get_permissions(
        self,
        request,
        pk=None
    ):

        group = self.get_object()

        permissions = (
            group.permissions
            .select_related("content_type")
        )

        serializer = PermissionSerializer(
            permissions,
            many=True
        )

        return Response(
            serializer.data
        )
```

Response:

```
[
    {
        "id": 1,
        "name": "Can view product",
        "codename": "view_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 5,
        "name": "Can approve product",
        "codename": "approve_product",
        "app_label": "products",
        "model": "product"
    }
]
```

---

# 9. Role-এর permission change

এখন আসল management API।

```
PUT /api/admin/roles/1/permissions/
```

Body:

```
{
    "permission_ids": [
        1,
        2,
        5,
        8
    ]
}
```

Backend:

```
@action(
    detail=True,
    methods=["put"],
    url_path="permissions",
)
def update_permissions(
    self,
    request,
    pk=None
):

    group = self.get_object()

    permission_ids = request.data.get(
        "permission_ids",
        []
    )

    permissions = Permission.objects.filter(
        id__in=permission_ids
    )

    if (
        len(permission_ids)
        != permissions.count()
    ):
        return Response(
            {
                "detail":
                "Invalid permission ID."
            },
            status=400
        )

    group.permissions.set(
        permissions
    )

    return Response({
        "message":
        "Permissions updated successfully"
    })
```

এখানে:

```
group.permissions.set(permissions)
```

মানে আগের permissions replace করে নতুন list set হবে।

---

# 10. Add/remove আলাদাভাবে না করেও পারবেন

ধরুন আগে:

```
Manager

✓ view_product
✓ add_product
✓ change_product
```

Dashboard-এ Delete tick করলেন:

```
Manager

✓ view_product
✓ add_product
✓ change_product
✓ delete_product
```

Frontend পুরো selected list পাঠাবে:

```
{
    "permission_ids": [
        1,
        2,
        3,
        4
    ]
}
```

Backend:

```
group.permissions.set(
    permissions
)
```

হয়ে যাবে।

এটাই সহজ approach।

---

# 11. User-এর Role/Group assign API

এখন user-কে Group দিতে হবে।

```
PUT /api/admin/users/10/roles/
```

Body:

```
{
    "group_ids": [
        1,
        3
    ]
}
```

Backend:

```
from django.contrib.auth import get_user_model
from django.contrib.auth.models import Group
from rest_framework.views import APIView

User = get_user_model()


class UserRoleUpdateView(APIView):

    permission_classes = [
        IsAdminUser
    ]

    def put(self, request, pk):

        user = User.objects.get(
            pk=pk
        )

        group_ids = request.data.get(
            "group_ids",
            []
        )

        groups = Group.objects.filter(
            id__in=group_ids
        )

        if (
            len(group_ids)
            != groups.count()
        ):
            return Response(
                {
                    "detail":
                    "Invalid group ID."
                },
                status=400
            )

        user.groups.set(groups)

        return Response({
            "message":
            "Roles updated successfully"
        })
```

এখন:

```
Rahim
│
├── Seller
└── ReportViewer
```

হতে পারে।

---

# 12. User-এর current roles দেখানো

```
GET /api/admin/users/10/roles/
```

Response:

```
{
    "user_id": 10,
    "roles": [
        {
            "id": 1,
            "name": "Seller"
        },
        {
            "id": 3,
            "name": "ReportViewer"
        }
    ]
}
```

---

# 13. Router

```
# accounts/urls.py

from rest_framework.routers import DefaultRouter

from .views import (
    RoleViewSet,
    PermissionViewSet,
)

router = DefaultRouter()

router.register(
    "roles",
    RoleViewSet,
    basename="roles"
)

router.register(
    "permissions",
    PermissionViewSet,
    basename="permissions"
)

urlpatterns = router.urls
```

Main URL:

```
# config/urls.py

from django.urls import path, include


urlpatterns = [
    path(
        "api/admin/",
        include("accounts.urls")
    ),
]
```

---

# 14. Frontend Dashboard

আপনার frontend:

```
Admin Dashboard
│
├── Users
│
├── Roles
│
└── Permissions
```

### Roles

```
Roles

Manager       [Edit] [Delete]
Seller        [Edit] [Delete]
Accountant    [Edit] [Delete]

             [+ Create Role]
```

### Edit Manager

```
Manager Permissions

Products
☑ View
☑ Add
☑ Change
☐ Delete
☑ Approve
☐ Reject

Orders
☑ View
☑ Add
☑ Change
☐ Delete
☑ Confirm

             [Save]
```

Frontend:

```
GET /permissions/
```

দিয়ে available permissions পাবে।

তারপর:

```
GET /roles/1/permissions/
```

দিয়ে কোনগুলো currently assigned সেটা জানবে।

Save করলে:

```
PUT /roles/1/permissions/
```

---

# 15. API authorization

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

Role management dashboard-এর সাথে আপনার normal API authorization-এর কোনো আলাদা system লাগবে না।

যেমন:

```
class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]
```

`RBACModelPermissions`:

```
from rest_framework.permissions import (
    DjangoModelPermissions
)


class RBACModelPermissions(
    DjangoModelPermissions
):

    perms_map = {
        "GET": [
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

---

# 16. Custom action

`approve` হলো custom permission:

```
class CanApproveProduct(
    BasePermission
):

    def has_permission(
        self,
        request,
        view
    ):

        return request.user.has_perm(
            "products.approve_product"
        )
```

ViewSet:

```
@action(
    detail=True,
    methods=["post"],
    permission_classes=[
        CanApproveProduct
    ],
)
def approve(
    self,
    request,
    pk=None
):

    product = self.get_object()

    product.is_approved = True

    product.save(
        update_fields=[
            "is_approved"
        ]
    )

    return Response({
        "message":
        "Product approved"
    })
```

---

# 17. JWT-এর সাথে পুরো flow

Login:

```
POST /api/auth/login/
```

JWT পাওয়া গেল:

```
access_token
```

তারপর:

```
Authorization: Bearer <access_token>
```

API request:

```
PATCH /api/products/10/
```

Flow:

```
JWT
 ↓
Authentication
 ↓
request.user
 ↓
User.groups
 ↓
Group.permissions
 ↓
change_product?
 ↓
YES → API allowed
NO  → 403
```

---

# 18. Role field এখানে কোথায়?

আপনার `role`:

```
Rahim

role = seller
```

শুধু identify করবে:

```
Rahim একজন Seller
```

এটা API permission check করবে না।

API permission:

```
Rahim
 ↓
groups
 ↓
permissions
```

---

# 19. Security খুব গুরুত্বপূর্ণ

এই APIগুলো:

```
/api/admin/roles/
/api/admin/permissions/
/api/admin/users/{id}/roles/
```

যে কেউ access করতে পারবে না।

Minimum:

```
permission_classes = [
    IsAdminUser
]
```

আর production RBAC-এ আরও granular করা ভালো:

```
manage_roles
manage_permissions
assign_roles
```

যেমন:

```
class CanManageRoles(
    BasePermission
):

    def has_permission(
        self,
        request,
        view
    ):

        return request.user.has_perm(
            "accounts.manage_roles"
        )
```

তাহলে একজন সাধারণ Manager আপনার Role Management API ব্যবহার করতে পারবে না, যদি তাকে `manage_roles` না দেওয়া হয়।

---

# 20. Final database relationship

শেষে database concept হবে:

```
User
 │
 ├── role
 │     └── seller
 │
 └── groups
       │
       ├── Seller
       │     │
       │     └── Permissions
       │           ├── view_product
       │           ├── add_product
       │           └── change_product
       │
       └── ReportViewer
             │
             └── Permissions
                   └── view_report
```

তারপর:

```
JWT
 ↓
User
 ↓
Groups
 ↓
Permissions
 ↓
DRF ViewSet
 ↓
API
```

## এক কথায়

আপনার **Django Admin Panel একদম ব্যবহার না করেও** পুরো system চালাতে পারবেন:

```
Custom Dashboard
     ↓
Role CRUD API
     ↓
Django Group

Custom Dashboard
     ↓
Permission List API
     ↓
Django Permission

Custom Dashboard
     ↓
Assign Permission API
     ↓
Group.permissions

Custom Dashboard
     ↓
Assign Role API
     ↓
User.groups

User Login
     ↓
JWT
     ↓
DRF
     ↓
Django Group Permission
     ↓
API access
```

**Permission definition Django নিজে তৈরি করবে; আপনার Dashboard permission তৈরি/মুছে ফেলবে না। Dashboard শুধু permission list দেখাবে এবং কোন Group কোন permission পাবে সেটা API দিয়ে manage করবে।**



----
হ্যাঁ, **checkbox দিয়েই সবচেয়ে সহজে Group-এর API permission access/remove manage করতে পারবেন।**

 Flow হবে:

```
Admin Dashboard
     ↓
Manager Role
     ↓
Permission List
     ↓
☑ View Product
☑ Add Product
☐ Change Product
☐ Delete Product
☑ Approve Product
     ↓
Save
     ↓
PUT /api/admin/roles/1/permissions/
```

 Frontend থেকে শুধু **যেগুলো checked সেগুলোর permission ID** পাঠাবেন:

```
{
  "permission_ids": [1, 2, 5]
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

 ### Access remove কীভাবে হবে?

 ধরুন আগে:

```
☑ View
☑ Add
☑ Change
☑ Delete
```

 Admin `Delete` uncheck করল:

```
☑ View
☑ Add
☑ Change
☐ Delete
```

 Frontend পাঠাবে:

```
{
  "permission_ids": [1, 2, 3]
}
```

 `group.permissions.set(...)` করার পর `delete_product` আর Group-এর মধ্যে থাকবে না।

 অর্থাৎ:

```
☑ = Access আছে
☐ = Access নেই
```

 এবং পরবর্তীতে User:

```
DELETE /api/products/10/
```

 করলে Group-এ `delete_product` না থাকায় DRF তাকে **403 Forbidden** দেবে।

 ### Dashboard UI

 আমি সাধারণত এমন রাখব:

```
┌─────────────────────────────────────┐
│ Manager Permissions                 │
├─────────────────────────────────────┤
│                                     │
│ Products                            │
│                                     │
│ ☑ View Product                      │
│ ☑ Add Product                       │
│ ☑ Change Product                    │
│ ☐ Delete Product                    │
│ ☑ Approve Product                   │
│ ☐ Reject Product                    │
│                                     │
│ Orders                              │
│                                     │
│ ☑ View Order                        │
│ ☑ Change Order                      │
│ ☐ Delete Order                      │
│                                     │
│             [ Save Permissions ]    │
└─────────────────────────────────────┘
```

 **একটা গুরুত্বপূর্ণ recommendation:** প্রতিবার checkbox change হলেই API call না করে, সব checkbox select/unselect করার পর **Save Permissions** চাপলে একবার `PUT` করুন। এতে permission state সহজে consistent থাকে।


হ্যাঁ। আপনি যদি জানতে চান **Django-এর সব generated + custom permission কীভাবে API থেকে পাবেন**, তাহলে `Permission.objects.all()` থেকে নিতে হবে।

 ## 1\. Permission Serializer

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

 ## 2\. Permission ViewSet

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

    permission_classes = [
        IsAdminUser
    ]
```

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

 এখন:

```
GET /api/admin/permissions/
```

 করলেই সব permission পাবেন।

 ### Response

 ধরুন `Product` model আছে:

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
  }
]
```

 আপনার custom permission থাকলেও:

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

 migration করার পরে:

```
python manage.py makemigrations
python manage.py migrate
```

 API-তে সেগুলোও পাবেন:

```
{
  "id": 5,
  "name": "Can approve product",
  "codename": "approve_product",
  "app_label": "products",
  "model": "product"
}
```

 ### তারপর Dashboard-এ

 আপনার frontend:

```
GET /api/admin/permissions/
```

 থেকে permissionগুলো নিয়ে:

```
Products
☑ View
☑ Add
☑ Change
☐ Delete
☑ Approve
☐ Reject
```

 checkbox বানাবে।

 আর Save করলে:

```
PUT /api/admin/roles/1/permissions/
```

```
{
  "permission_ids": [1, 2, 4, 5]
}
```

 এটাই Group-এর permission update করবে।

 **সুতরাং permission আলাদা করে database-এ manually বানাতে হবে না—Django model থেকে তৈরি করা permission এবং আপনার custom `Meta.permissions` দুটোই `Permission` table থেকে API-তে পাওয়া যাবে।**


হ্যাঁ। আপনার dashboard-এর জন্য **GET + PUT**-ই যথেষ্ট এবং clean approach।

 ### GET — বর্তমানে কোন permission আছে

```
GET /api/admin/roles/1/permissions/
```

 Response:

```
{
  "role": "Manager",
  "permission_ids": [1, 2, 5, 8]
}
```

 Frontend এই `permission_ids` দেখে checkbox checked করবে।

 ### PUT — checkbox অনুযায়ী permission update

```
PUT /api/admin/roles/1/permissions/
```

 Body:

```
{
  "permission_ids": [1, 2, 3, 5]
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

 এখানে **পুরো selected list** পাঠাবেন।

 যেমন আগে:

```
☑ view
☑ add
☑ change
☑ delete
```

 Admin `delete` uncheck করল:

```
☑ view
☑ add
☑ change
☐ delete
```

 PUT হবে:

```
{
  "permission_ids": [
    1,
    2,
    3
  ]
}
```

 `delete` automatically remove হয়ে যাবে।

 ### পুরো flow

```
GET /roles/1/permissions/
        ↓
Current permissions
        ↓
Frontend checkbox
        ↓
Admin check/uncheck
        ↓
PUT /roles/1/permissions/
        ↓
group.permissions.set(...)
        ↓
Permission updated
```

 আর **সব available permission** দেখানোর জন্য আলাদা:

```
GET /api/admin/permissions/
```

 তাই আপনার dashboard-এ মূলত এই ২টা GET + ১টা PUT গুরুত্বপূর্ণ:

```
GET  /permissions/              → সব available permission
GET  /roles/1/permissions/      → এই role-এর current permission
PUT  /roles/1/permissions/      → permission save/update
```

 এটাই checkbox-based RBAC-এর জন্য যথেষ্ট।

হ্যাঁ, **ঠিক এভাবেই করবেন**। Dashboard থেকে selected checkbox-এর **permission ID-এর list** পাঠাবেন।

 ধরুন available permissions:

```
1 → view_product
2 → add_product
3 → change_product
4 → delete_product
5 → approve_product
6 → reject_product
```

 Admin checkbox থেকে select করল:

```
☑ view_product
☑ add_product
☑ change_product
☐ delete_product
☑ approve_product
☐ reject_product
```

 Frontend পাঠাবে:

```
PUT /api/admin/roles/1/permissions/
```

```
{
  "permission_ids": [1, 2, 3, 5]
}
```

 Backend:

```
permission_ids = request.data.get(
    "permission_ids",
    []
)

permissions = Permission.objects.filter(
    id__in=permission_ids
)

group.permissions.set(permissions)
```

 এরপর `Manager` Group-এর permissions হবে:

```
view_product       ✓
add_product        ✓
change_product     ✓
delete_product     ✗
approve_product    ✓
reject_product     ✗
```

 ### Dashboard খুললে

 প্রথমে:

```
GET /api/admin/permissions/
```

 → সব permission ID পাবে।

 তারপর:

```
GET /api/admin/roles/1/permissions/
```

 → কোনগুলো বর্তমানে assigned সেটা পাবে।

 Admin checkbox change করে **Save** করলে:

```
PUT /api/admin/roles/1/permissions/
```

```
{
  "permission_ids": [1, 2, 3, 5]
}
```

 এটাই যথেষ্ট। **Permission-এর ID list-টাই frontend থেকে backend-এ পাঠাবেন; backend সেই list অনুযায়ী Group-এর permissions set করবে।**

----


অবশ্যই। নিচে আপনার পুরো **JWT + DRF + ViewSet + User Role + Django Group + Permission + Custom Admin Dashboard** flow একসাথে দিলাম। এটাকে আপনার final architecture হিসেবে ধরতে পারেন।

## 1. আপনার মূল concept

```
User.role
    ↓
শুধু user-এর type
customer / seller / employee

User.groups
    ↓
Authorization Role
Manager / Seller / Accountant

Group.permissions
    ↓
কোন API/action করতে পারবে

JWT
    ↓
User authentication

DRF ViewSet
    ↓
Permission check
```

অর্থাৎ:

> **Role = User কে?**  
> **Group = User কী করতে পারবে?**

---

# 2. Folder structure

```
project/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   └── urls.py
│
├── accounts/
│   ├── models.py
│   ├── serializers.py
│   ├── permissions.py
│   ├── views.py
│   └── urls.py
│
├── products/
│   ├── models.py
│   ├── serializers.py
│   ├── permissions.py
│   ├── views.py
│   └── urls.py
│
└── manage_roles/
    └── ...
```

---

# 3. User model

`role` শুধু user identify করবে।

```
# accounts/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):

    ROLE_CHOICES = [
        ("customer", "Customer"),
        ("seller", "Seller"),
        ("employee", "Employee"),
    ]

    role = models.CharField(
        max_length=20,
        choices=ROLE_CHOICES,
        default="customer",
    )
```

যেমন:

```
Rahim
role = seller
```

এর মানে শুধু:

```
Rahim একজন Seller
```

এখানে API permission check হবে না।

---

# 4. Product model

```
# products/models.py

from django.db import models


class Product(models.Model):

    name = models.CharField(
        max_length=255
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    is_approved = models.BooleanField(
        default=False
    )

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

Django automatically তৈরি করবে:

```
view_product
add_product
change_product
delete_product
```

আর custom:

```
approve_product
reject_product
```

Migration:

```
python manage.py makemigrations
python manage.py migrate
```

---

# 5. Available Permission API

এখানে Permission create/update/delete করব না।

শুধু list করব।

```
# accounts/serializers.py

from django.contrib.auth.models import (
    Group,
    Permission,
)
from rest_framework import serializers


class PermissionSerializer(
    serializers.ModelSerializer
):

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


class RoleSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Group

        fields = [
            "id",
            "name",
        ]
```

---

# 6. Permission ViewSet

```
# accounts/views.py

from django.contrib.auth.models import (
    Group,
    Permission,
)

from rest_framework.viewsets import (
    ReadOnlyModelViewSet,
    ModelViewSet,
)

from rest_framework.permissions import (
    IsAdminUser,
)

from .serializers import (
    PermissionSerializer,
    RoleSerializer,
)


class PermissionViewSet(
    ReadOnlyModelViewSet
):

    queryset = Permission.objects.select_related(
        "content_type"
    ).order_by(
        "content_type__app_label",
        "content_type__model",
        "codename",
    )

    serializer_class = PermissionSerializer

    permission_classes = [
        IsAdminUser
    ]
```

API:

```
GET /api/admin/permissions/
```

Response:

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
        "name": "Can approve product",
        "codename": "approve_product",
        "app_label": "products",
        "model": "product"
    }
]
```

---

# 7. Role/Group CRUD API

Django `Group`-কেই আমরা Role হিসেবে ব্যবহার করব।

```
# accounts/views.py

class RoleViewSet(ModelViewSet):

    queryset = Group.objects.all().order_by(
        "name"
    )

    serializer_class = RoleSerializer

    permission_classes = [
        IsAdminUser
    ]
```

এতে automatically:

```
GET    /api/admin/roles/
POST   /api/admin/roles/

GET    /api/admin/roles/1/
PUT    /api/admin/roles/1/
PATCH  /api/admin/roles/1/
DELETE /api/admin/roles/1/
```

হবে।

---

# 8. Role create

Dashboard থেকে:

```
POST /api/admin/roles/
```

```
{
    "name": "Manager"
}
```

Django:

```
Group
id = 1
name = Manager
```

---

# 9. Role-এর current permission GET

Dashboard যখন `Manager` edit করবে:

```
GET /api/admin/roles/1/permissions/
```

ViewSet:

```
from rest_framework.decorators import action
from rest_framework.response import Response


class RoleViewSet(ModelViewSet):

    queryset = Group.objects.all()

    serializer_class = RoleSerializer

    permission_classes = [
        IsAdminUser
    ]

    @action(
        detail=True,
        methods=["get"],
        url_path="permissions",
    )
    def get_permissions(
        self,
        request,
        pk=None
    ):

        group = self.get_object()

        permissions = (
            group.permissions
            .select_related("content_type")
        )

        serializer = PermissionSerializer(
            permissions,
            many=True
        )

        return Response(
            serializer.data
        )
```

Response:

```
[
    {
        "id": 1,
        "name": "Can view product",
        "codename": "view_product",
        "app_label": "products",
        "model": "product"
    },
    {
        "id": 5,
        "name": "Can approve product",
        "codename": "approve_product",
        "app_label": "products",
        "model": "product"
    }
]
```

---

# 10. Checkbox দিয়ে permission change

Dashboard:

```
Manager Permissions

Products

☑ View Product
☑ Add Product
☑ Change Product
☐ Delete Product
☑ Approve Product
☐ Reject Product

             [Save]
```

Frontend selected ID list পাঠাবে:

```
PUT /api/admin/roles/1/permissions/
```

```
{
    "permission_ids": [
        1,
        2,
        3,
        5
    ]
}
```

Backend:

```
@action(
    detail=True,
    methods=["put"],
    url_path="permissions",
)
def update_permissions(
    self,
    request,
    pk=None
):

    group = self.get_object()

    permission_ids = request.data.get(
        "permission_ids",
        []
    )

    permissions = Permission.objects.filter(
        id__in=permission_ids
    )

    if (
        len(permission_ids)
        != permissions.count()
    ):
        return Response(
            {
                "detail":
                "Invalid permission ID."
            },
            status=400
        )

    group.permissions.set(
        permissions
    )

    return Response({
        "message":
        "Permissions updated successfully"
    })
```

### `set()` কী করছে?

ধরুন আগে:

```
View       ✓
Add        ✓
Change     ✓
Delete     ✓
Approve    ✓
```

Admin Delete এবং Reject uncheck করল।

Frontend পাঠাবে:

```
{
    "permission_ids": [
        1,
        2,
        3,
        5
    ]
}
```

তারপর:

```
group.permissions.set(permissions)
```

ফলে:

```
View       ✓
Add        ✓
Change     ✓
Delete     ✗
Approve    ✓
Reject     ✗
```

হয়ে যাবে।

---

# 11. User → Group assign

এখন User Management।

```
Rahim

Role:
☑ Seller
☑ Report Viewer

[Save]
```

API:

```
PUT /api/admin/users/10/roles/
```

Body:

```
{
    "group_ids": [1, 3]
}
```

Backend:

```
from django.contrib.auth import get_user_model
from django.contrib.auth.models import Group

User = get_user_model()


class UserRoleUpdateView(APIView):

    permission_classes = [
        IsAdminUser
    ]

    def put(self, request, pk):

        user = User.objects.get(pk=pk)

        group_ids = request.data.get(
            "group_ids",
            []
        )

        groups = Group.objects.filter(
            id__in=group_ids
        )

        if (
            len(group_ids)
            != groups.count()
        ):
            return Response(
                {
                    "detail":
                    "Invalid group ID."
                },
                status=400
            )

        user.groups.set(groups)

        return Response({
            "message":
            "Roles updated successfully"
        })
```

---

# 12. User-এর Group permission-এর সাথে যুক্ত হবে

এখন ধরুন:

```
Rahim
│
├── role = seller
│
└── groups
      │
      └── Seller
            │
            ├── view_product
            ├── add_product
            ├── change_product
            └── approve_product
```

এখানে:

```
role = seller
```

শুধু user type।

আর:

```
Seller Group
```

দিয়ে API access হচ্ছে।

---

# 13. CRUD API-এর জন্য ViewSet permission

আপনার Product ViewSet:

```
# products/views.py

from rest_framework.viewsets import ModelViewSet

from .models import Product
from .serializers import ProductSerializer
from common.permissions import (
    RBACModelPermissions
)


class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]
```

`RBACModelPermissions`:

```
# common/permissions.py

from rest_framework.permissions import (
    DjangoModelPermissions
)


class RBACModelPermissions(
    DjangoModelPermissions
):

    perms_map = {

        "GET": [
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

---

# 14. তাহলে API নিজে permission check করবে

ধরুন Manager Group:

```
view_product      ✓
add_product       ✓
change_product    ✓
delete_product    ✗
```

তাহলে:

```
GET /api/products/
```

→ ✅

```
POST /api/products/
```

→ ✅

```
PATCH /api/products/1/
```

→ ✅

```
DELETE /api/products/1/
```

→ ❌ `403 Forbidden`

কারণ:

```
request.user.has_perm(
    "products.delete_product"
)
```

False।

---

# 15. Custom permission

`approve_product` CRUD permission না, এটা custom action।

```
# products/permissions.py

from rest_framework.permissions import (
    BasePermission
)


class CanApproveProduct(
    BasePermission
):

    def has_permission(
        self,
        request,
        view
    ):

        return request.user.has_perm(
            "products.approve_product"
        )
```

ViewSet:

```
from rest_framework.decorators import (
    action
)

from rest_framework.response import (
    Response
)

from .permissions import (
    CanApproveProduct
)


class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    permission_classes = [
        RBACModelPermissions
    ]

    @action(
        detail=True,
        methods=["post"],
        permission_classes=[
            CanApproveProduct
        ],
    )
    def approve(
        self,
        request,
        pk=None
    ):

        product = self.get_object()

        product.is_approved = True

        product.save(
            update_fields=[
                "is_approved"
            ]
        )

        return Response({
            "message":
            "Product approved"
        })
```

এখন:

```
POST /api/products/1/approve/
```

শুধু `approve_product` permission থাকা user করতে পারবে।

---

# 16. JWT কোথায় আসবে?

Login:

```
POST /api/auth/login/
```

JWT:

```
access token
refresh token
```

তারপর request:

```
Authorization: Bearer <access_token>
```

DRF প্রথমে user identify করবে:

```
JWT
 ↓
request.user
```

তারপর:

```
request.user
 ↓
groups
 ↓
permissions
 ↓
ViewSet permission
 ↓
Allow / 403
```

---

# 17. Router

```
# accounts/urls.py

from rest_framework.routers import (
    DefaultRouter
)

from .views import (
    RoleViewSet,
    PermissionViewSet,
)

router = DefaultRouter()

router.register(
    "roles",
    RoleViewSet,
    basename="roles"
)

router.register(
    "permissions",
    PermissionViewSet,
    basename="permissions"
)

urlpatterns = router.urls
```

Main URL:

```
# config/urls.py

from django.urls import (
    path,
    include
)


urlpatterns = [
    path(
        "api/admin/",
        include("accounts.urls")
    ),
]
```

---

# 18. Final API list

আপনার Admin Dashboard-এর জন্য:

```
ROLE

GET    /api/admin/roles/
POST   /api/admin/roles/

GET    /api/admin/roles/{id}/
PATCH  /api/admin/roles/{id}/
DELETE /api/admin/roles/{id}/


PERMISSION

GET    /api/admin/permissions/


ROLE PERMISSION

GET    /api/admin/roles/{id}/permissions/
PUT    /api/admin/roles/{id}/permissions/


USER ROLE

GET    /api/admin/users/{id}/roles/
PUT    /api/admin/users/{id}/roles/
```

---

# 19. Dashboard-এর complete flow

```
                    ADMIN DASHBOARD
                           │
             ┌─────────────┴─────────────┐
             │                           │
           Roles                       Users
             │                           │
       GET /roles/                GET /users/
             │                           │
        Manager                      Rahim
             │                           │
             ↓                           ↓
    GET /roles/1/permissions/    PUT /users/10/roles/
             │
             ↓
       Checkbox UI
             │
     ☑ View Product
     ☑ Add Product
     ☑ Change Product
     ☐ Delete Product
     ☑ Approve Product
             │
             ↓
    PUT /roles/1/permissions/
             │
             ↓
      Group.permissions
             │
             ↓
           User
             │
             ↓
            JWT
             │
             ↓
        DRF ViewSet
             │
             ↓
       Permission Check
             │
       ┌─────┴─────┐
       ↓           ↓
     ALLOW        403
```

## সবচেয়ে গুরুত্বপূর্ণ ৫টা rule

1. **`User.role` → শুধু customer/seller/employee identify করবে।**
    
2. **`Group` → আপনার authorization role হিসেবে কাজ করবে।**
    
3. **`Permission` → Group কী করতে পারবে সেটা define করবে।**
    
4. **Checkbox → selected permission ID list পাঠাবে।**
    
5. **ViewSet → `request.user`-এর Group/Permission দেখে API access দেবে বা `403` করবে।**
    

এই architecture-এ **Django Admin Panel ছাড়াই** আপনার নিজের React/Next/Vue Admin Dashboard থেকে পুরো Role/Group permission system পরিচালনা করা যাবে।

