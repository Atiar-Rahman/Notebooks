হ্যাঁ, `codename` আপনি নিজেই define করবেন। এটি সাধারণত **action + resource** pattern-এ লেখা হয়, যাতে code দেখে সহজে বোঝা যায় permission কী কাজ করে।

Format:

```
<action>_<resource>
```

### Common action:

```text
view
create
add
update
change
delete
remove
approve
reject
manage
publish
export
refund
```

---

### eCommerce project-এর example:

#### Product

```text
view_product
create_product
update_product
delete_product
publish_product
```

#### Category

```text
create_category
update_category
delete_category
```

#### Order

```text
view_order
create_order
update_order
cancel_order
approve_order
ship_order
```

#### User

```text
view_user
create_user
update_user
delete_user
block_user
```

#### Vendor

```text
create_vendor
approve_vendor
reject_vendor
suspend_vendor
```

#### Payment

```text
view_payment
verify_payment
refund_payment
```

---

আপনার Permission model:

```python
class Permission(models.Model):
    name = models.CharField(
        max_length=100
    )

    codename = models.CharField(
        max_length=100,
        unique=True
    )
```

Data:

|name|codename|
|---|---|
|Add Product|create_product|
|Delete Product|delete_product|
|Approve Vendor|approve_vendor|
|Refund Payment|refund_payment|

---

DRF-এ ব্যবহার:

```python
required_permission = "create_product"
```

তারপর check:

```python
request.user.role.permissions.filter(
    codename="create_product"
).exists()
```

---

Production project-এর জন্য consistent naming রাখুন। যেমন:

ভালো:

```
create_product
update_product
delete_product
view_product
```

এড়িয়ে চলুন:

```
product_create
makeProduct
createProductPermission
add-new-product
```

কারণ codebase বড় হলে প্রথম pattern maintain করা সহজ হয়।

--------
আপনার প্রশ্নটা হলো: যদি action `list` হয় তাহলে `view_product`, কিন্তু যদি একই pattern অন্য resource-এর জন্য হয় (যেমন `category`), তাহলে কী হবে?

এটার জন্য permission naming **resource অনুযায়ী dynamic** রাখতে হয়।

উদাহরণ:

### ProductViewSet

```python
class ProductViewSet(ModelViewSet):

    permission_map = {
        "list": "view_product",
        "retrieve": "view_product",
        "create": "create_product",
        "update": "update_product",
        "destroy": "delete_product",
    }
```

---

### CategoryViewSet

```python
class CategoryViewSet(ModelViewSet):

    permission_map = {
        "list": "view_category",
        "retrieve": "view_category",
        "create": "create_category",
        "update": "update_category",
        "destroy": "delete_category",
    }
```

এখানে:

```
GET /products/
→ view_product

GET /categories/
→ view_category
```

---

কিন্তু প্রতিটি ViewSet-এ বারবার `permission_map` লেখা কিছুটা repetitive। তাই production-এ একটি **generic permission naming system** করা যায়।

যেমন:

```python
class BasePermissionViewSet(ModelViewSet):

    permission_resource = None

    action_permission_map = {
        "list": "view",
        "retrieve": "view",
        "create": "create",
        "update": "update",
        "partial_update": "update",
        "destroy": "delete",
    }


    def get_required_permission(self):

        action = self.action
        permission_action = self.action_permission_map.get(action)

        if not permission_action:
            return None

        return f"{permission_action}_{self.permission_resource}"
```

---

তারপর Product:

```python
class ProductViewSet(BasePermissionViewSet):

    permission_resource = "product"
```

Category:

```python
class CategoryViewSet(BasePermissionViewSet):

    permission_resource = "category"
```

---

এখন automatically হবে:

Product:

```
list        → view_product
create      → create_product
update      → update_product
destroy     → delete_product
```

Category:

```
list        → view_category
create      → create_category
update      → update_category
destroy     → delete_category
```

---

তাহলে আপনার Permission table:

```
view_product
create_product
update_product
delete_product

view_category
create_category
update_category
delete_category
```

এভাবে হবে।

এটা বড় eCommerce project-এর জন্য বেশি maintainable, কারণ নতুন model যোগ করলে শুধু:

```python
permission_resource = "brand"
```

দিলেই হবে।
হ্যাঁ, production eCommerce-এ সাধারণত **প্রতিটি model/resource-এর আলাদা আলাদা permission থাকবে**।

যেমন:

```text
Product
    view_product
    create_product
    update_product
    delete_product
    publish_product


Category
    view_category
    create_category
    update_category
    delete_category


Order
    view_order
    update_order
    cancel_order
    approve_order
    ship_order


User
    view_user
    create_user
    update_user
    delete_user
```

কারণ সব resource-এর action একই না।

উদাহরণ:

### Product

```text
create_product
update_product
delete_product
publish_product
```

### Order

Order delete করা সাধারণত হয় না:

```text
view_order
update_order_status
cancel_order
refund_order
```

### Payment

```text
view_payment
verify_payment
refund_payment
```

---

## Model অনুযায়ী Permission structure

Database:

```
Permission
------------
id
name
codename
```

Data:

| name           | codename       |
| -------------- | -------------- |
| Create Product | create_product |
| Delete Product | delete_product |
| Approve Order  | approve_order  |
| Refund Payment | refund_payment |

---

## Role assignment

```
Admin Role

Permissions:
    create_product
    delete_product
    approve_order
    refund_payment
```

```
Vendor Role

Permissions:
    create_product
    update_product
    view_order
```

```
Customer Role

Permissions:
    view_product
    create_order
    cancel_order
```

---

## আপনার ViewSet-এ

Product:

```python
permission_resource = "product"
```

Category:

```python
permission_resource = "category"
```

Order:

```python
permission_resource = "order"
```

তারপর action অনুযায়ী permission generate হবে।

---

তবে সব model-এর permission একই pattern হবে না। যেমন:

```text
CRUD models:
    view
    create
    update
    delete


Business models:
    approve
    reject
    cancel
    refund
    publish
    assign
```

তাই production system-এ সাধারণত দুইটা approach মেশানো হয়:

1. **Common CRUD permission auto generate**
2. **Special business permission manually define**

যেমন:

```
Product:
    CRUD auto
    publish_product manual

Order:
    view/update auto
    cancel_order/refund_order manual
```

এটাই বড় eCommerce system-এ বেশি practical।
Backend থেকে check করার মূল idea হলো: **backend জানবে কোন API চালাতে কোন permission লাগবে**, তারপর `request.user` থেকে permission বের করে match করবে।

Flow:

```text id="2w6q5k"
Request আসে
    |
    ↓
DRF View/ViewSet
    |
    ↓
Required permission বের করে
    |
    ↓
User → Role → Permissions query
    |
    ↓
codename match
    |
    ↓
Allow / Deny
```

---

## 1. Permission Model

```python
class Permission(models.Model):

    name = models.CharField(
        max_length=100
    )

    codename = models.CharField(
        max_length=100,
        unique=True
    )
```

Example:

```
create_product
delete_product
view_order
```

---

## 2. Role Model

```python
class Role(models.Model):

    name = models.CharField(
        max_length=50
    )

    permissions = models.ManyToManyField(
        Permission,
        related_name="roles"
    )
```

---

## 3. User Model

```python
class User(AbstractUser):

    role = models.ForeignKey(
        Role,
        null=True,
        on_delete=models.SET_NULL
    )
```

---

## 4. DRF Permission Class

`permissions.py`

```python
from rest_framework.permissions import BasePermission


class HasPermission(BasePermission):

    def has_permission(self, request, view):

        required_permission = getattr(
            view,
            "required_permission",
            None
        )

        if not required_permission:
            return True


        if not request.user.is_authenticated:
            return False


        return request.user.role.permissions.filter(
            codename=required_permission
        ).exists()
```

---

## 5. View-এ permission define করবেন

Example:

```python
from rest_framework.views import APIView


class ProductCreateAPIView(APIView):

    permission_classes = [
        HasPermission
    ]

    required_permission = "create_product"


    def post(self, request):

        # product create logic

        return Response({
            "message": "Created"
        })
```

---

এখন request আসলে:

```
POST /api/products/
```

Backend দেখবে:

```python
required_permission = "create_product"
```

তারপর query হবে:

```python
request.user.role.permissions.filter(
    codename="create_product"
).exists()
```

Database:

```
User
 |
Role: Vendor
 |
Permissions:
    create_product
    update_product
```

Result:

```
True
```

Access দিবে।

---

## ViewSet হলে আরও ভালো

```python
class ProductViewSet(ModelViewSet):

    permission_classes = [
        HasPermission
    ]

    permission_map = {
        "list": "view_product",
        "create": "create_product",
        "update": "update_product",
        "destroy": "delete_product",
    }


    def get_permissions(self):

        self.required_permission = (
            self.permission_map.get(self.action)
        )

        return super().get_permissions()
```

এখন:

```
GET      /products/
→ view_product

POST     /products/
→ create_product

PUT      /products/1/
→ update_product

DELETE   /products/1/
→ delete_product
```

---

Production-এ এইটাই standard approach:

```
ViewSet
   |
   ↓
required_permission
   |
   ↓
User Role
   |
   ↓
Role Permissions
   |
   ↓
Permission.codename match
   |
   ↓
Allow / 403
```

এতে frontend dashboard-এর permission list আর backend security—দুটো একই permission system ব্যবহার করবে।
না, **প্রতিটি API view-তে আলাদা করে permission map রাখা বাধ্যতামূলক না**। Production project-এ সাধারণত দুইভাবে করা হয়।

---

## Approach 1: প্রতিটি ViewSet-এ `permission_map` রাখা (Simple)

ছোট/medium project-এর জন্য:

```python
class ProductViewSet(ModelViewSet):

    permission_map = {
        "list": "view_product",
        "create": "create_product",
        "update": "update_product",
        "destroy": "delete_product",
    }
```

Category:

```python
class CategoryViewSet(ModelViewSet):

    permission_map = {
        "list": "view_category",
        "create": "create_category",
        "update": "update_category",
        "destroy": "delete_category",
    }
```

এখানে control বেশি, কিন্তু code repeat হয়।

---

# Approach 2: Base ViewSet দিয়ে automatic generate (Production friendly)

একটা common base class বানাবেন:

```python
class BasePermissionViewSet(ModelViewSet):

    permission_resource = None

    action_permission = {
        "list": "view",
        "retrieve": "view",
        "create": "create",
        "update": "update",
        "partial_update": "update",
        "destroy": "delete",
    }


    def get_required_permission(self):

        action = self.action

        permission = self.action_permission.get(
            action
        )

        if not permission:
            return None

        return f"{permission}_{self.permission_resource}"
```

---

তারপর Product:

```python
class ProductViewSet(BasePermissionViewSet):

    permission_resource = "product"
```

Automatically:

```
list     → view_product
create   → create_product
update   → update_product
delete   → delete_product
```

---

Category:

```python
class CategoryViewSet(BasePermissionViewSet):

    permission_resource = "category"
```

Automatically:

```
list     → view_category
create   → create_category
update   → update_category
delete   → delete_category
```

---

## Special permission হলে?

যেমন:

Product publish:

```python
@action(
    detail=True,
    methods=["post"]
)
def publish(self, request, pk=None):
    ...
```

এখানে:

```python
required_permission = "publish_product"
```

অথবা:

```python
special_permissions = {
    "publish": "publish_product"
}
```

---

## Recommended structure আপনার eCommerce-এর জন্য:

```
core/
    permissions.py
    base_viewsets.py

catalog/
    views.py

orders/
    views.py
```

Flow:

```
ProductViewSet
        |
        ↓
permission_resource = "product"
        |
        ↓
BaseViewSet generate
        |
        ↓
create_product
        |
        ↓
Role Permission check
```

তাই প্রতিটি API-তে manually permission map না রেখে **common CRUD permission auto generate + special permission manually define** করা সবচেয়ে clean approach।
আপনার `action API` (DRF `@action`) এর ক্ষেত্রে CRUD-এর মতো automatic করা যায় না, কারণ action-এর নাম business অনুযায়ী আলাদা হতে পারে। তাই সেখানে permission map বা permission code আলাদাভাবে define করতে হয়।

Example:

ধরি Product-এর action:

* publish product
* approve product
* feature product

---

## Method 1: Action name থেকে automatic permission generate

Base ViewSet:

```python
from rest_framework.viewsets import ModelViewSet


class BasePermissionViewSet(ModelViewSet):

    permission_resource = None

    def get_required_permission(self):

        # normal CRUD
        if self.action in [
            "list",
            "retrieve",
            "create",
            "update",
            "partial_update",
            "destroy",
        ]:
            action_map = {
                "list": "view",
                "retrieve": "view",
                "create": "create",
                "update": "update",
                "partial_update": "update",
                "destroy": "delete",
            }

            return f"{action_map[self.action]}_{self.permission_resource}"


        # custom action
        return f"{self.action}_{self.permission_resource}"
```

---

এখন ProductViewSet:

```python
class ProductViewSet(BasePermissionViewSet):

    permission_resource = "product"


    @action(
        detail=True,
        methods=["post"]
    )
    def publish(self, request, pk=None):

        return Response({
            "message": "published"
        })
```

DRF action হবে:

```python
self.action = "publish"
```

তাই permission হবে:

```text
publish_product
```

---

## Database Permission:

```text
view_product
create_product
update_product
delete_product

publish_product
feature_product
approve_product
```

---

## Method 2: Explicit map (যখন নাম আলাদা)

ধরুন action:

```python
@action(
    detail=True,
    methods=["post"]
)
def make_live(self, request, pk=None):
    ...
```

কিন্তু permission নাম:

```text
publish_product
```

তাহলে map লাগবে:

```python
class ProductViewSet(BasePermissionViewSet):

    permission_resource = "product"


    action_permissions = {
        "make_live": "publish_product",
        "feature": "feature_product",
    }
```

Base class-এ:

```python
def get_required_permission(self):

    if self.action in self.action_permissions:
        return self.action_permissions[self.action]

    return super().get_required_permission()
```

---

তাহলে:

```python
@action
def make_live(...)
```

হবে:

```text
make_live
        |
        ↓
action_permissions
        |
        ↓
publish_product
```

---

Production eCommerce-এর জন্য আমি এই pattern ব্যবহার করতাম:

```text
CRUD:
    automatic

Custom action:
    action name থেকে generate

Exception:
    action_permissions map
```

তাহলে ৯০% permission লিখতে হবে না, আবার special business action-ও handle করা যাবে।
হ্যাঁ, **এটাই একটি সঠিক এবং widely used RBAC (Role-Based Access Control) flow**।

Flow হবে:

```text
User Login
    │
    ▼
JWT / Session
    │
    ▼
Backend → User Role
    │
    ▼
Role → Permissions
    │
    ▼
Frontend permissions পাবে
    │
    ▼
Frontend শুধু ওই permission-এর menu দেখাবে
    │
    ▼
User menu click করে API call করবে
    │
    ▼
Backend আবার User-এর permission verify করবে
    │
    ▼
Allow / 403 Forbidden
```

### Example

Vendor Role-এর permission:

```text
view_product
create_product
update_product
view_order
```

Login response:

```json
{
    "user": {
        "id": 1,
        "name": "Rahim",
        "role": "Vendor"
    },
    "permissions": [
        "view_product",
        "create_product",
        "update_product",
        "view_order"
    ]
}
```

Frontend:

* ✅ Products
* ✅ Add Product
* ✅ Orders

দেখাবে না:

* ❌ Users
* ❌ Roles
* ❌ Permissions

---

যখন user **Add Product**-এ click করবে:

```http
POST /api/products/
```

Backend আবার check করবে:

```python
request.user.role.permissions.filter(
    codename="create_product"
).exists()
```

যদি `True` হয়:

```
201 Created
```

যদি `False` হয়:

```
403 Forbidden
```

### একটি গুরুত্বপূর্ণ বিষয়

Frontend-এ menu hide/show করা **security নয়**, এটা শুধু user experience।

**আসল security সবসময় backend-এ হবে।**

কারণ একজন user Postman বা browser dev tools দিয়ে যেকোনো API call করতে পারে। তাই backend-এ প্রতিটি protected API-তে permission check অবশ্যই থাকতে হবে।

---

আপনার eCommerce project-এর জন্য:

* ✅ Permission database-এ থাকবে।
* ✅ Role-এর সাথে ManyToMany relation থাকবে।
* ✅ User-এর একটি Role থাকবে।
* ✅ Login-এর পর frontend user-এর permission list পাবে।
* ✅ সেই permission অনুযায়ী menu render হবে।
* ✅ প্রতিটি API call-এর সময় backend একই permission আবার verify করবে।

এটাই production-grade RBAC architecture।
হ্যাঁ, **frontend-এ route define করে user-এর role permission অনুযায়ী menu show/hide করা যাবে**। এটা খুব common approach। তবে শুধু menu hide/show করলেই security complete হবে না; backend-এও permission check রাখতে হবে।

আপনার flow এমন হতে পারে:

```text
User Login
    |
    ↓
Backend থেকে user + permissions আসবে
    |
    ↓
Frontend route config-এর সাথে permission match করবে
    |
    ↓
যে route-এর permission আছে শুধু সেই menu দেখাবে
    |
    ↓
User page open করবে
    |
    ↓
Backend API আবার permission check করবে
```

---

Example:

Frontend route config:

```javascript
const routes = [
  {
    path: "/products",
    name: "Products",
    permission: "view_product"
  },
  {
    path: "/products/create",
    name: "Add Product",
    permission: "create_product"
  },
  {
    path: "/orders",
    name: "Orders",
    permission: "view_order"
  },
  {
    path: "/users",
    name: "Users",
    permission: "view_user"
  }
];
```

User permissions:

```json
[
  "view_product",
  "create_product",
  "view_order"
]
```

Filter:

```javascript
const allowedRoutes = routes.filter(route =>
    userPermissions.includes(route.permission)
);
```

Output:

```text
/products
/products/create
/orders
```

`/users` show হবে না।

---

কিন্তু ধরুন user manually লিখলো:

```
/users
```

তখন frontend route guard:

```javascript
if (!permissions.includes("view_user")) {
    return <Navigate to="/403" />;
}
```

এটা prevent করবে।

---

তারপর backend:

```
GET /api/users/
```

এখানে backend:

```python
request.user.role.permissions.filter(
    codename="view_user"
).exists()
```

check করবে।

না থাকলে:

```
403 Forbidden
```

---

আপনার approach:

✅ Frontend route static থাকবে
✅ Route-এর সাথে permission থাকবে
✅ Login-এর পরে user permission আসবে
✅ Permission অনুযায়ী menu দেখাবে
✅ Backend API level-এ আবার check করবে

এটা বাস্তবে অনেক admin panel-এ ব্যবহার করা হয়।

শুধু মনে রাখবেন: **Frontend permission দিয়ে UI control হয়, Backend permission দিয়ে actual access control হয়।**
আপনার idea **ভুল না, বরং ভালো direction-এ আছে**। আপনার confusion হচ্ছে কোন জায়গায় permission control হবে—frontend নাকি backend। সহজভাবে বলি।

আপনার idea:

1. User login করবে ✅
2. User-এর role বের হবে ✅
3. Role অনুযায়ী permission বের হবে ✅
4. Permission অনুযায়ী frontend menu দেখাবে ✅
5. User menu click করে কাজ করবে ✅

এগুলো সব ঠিক।

একটা example:

ধরি আপনার system:

```
Role: Vendor

Permissions:
- view_product
- create_product
- update_product
```

Frontend route:

```javascript
[
  {
    path: "/products",
    permission: "view_product"
  },
  {
    path: "/products/create",
    permission: "create_product"
  },
  {
    path: "/products/edit",
    permission: "update_product"
  }
]
```

Login করার পরে backend দিল:

```json
{
  "permissions": [
    "view_product",
    "create_product"
  ]
}
```

Frontend দেখাবে:

```
Products        ✅
Create Product  ✅
Edit Product    ❌
```

এটা আপনার idea অনুযায়ীই হবে।

---

যেখানে একটু পরিবর্তন দরকার:

আপনি ভাবছেন:

```
Frontend
   |
   | permission পাঠাবে
   |
Backend
   |
   | permission match করে কাজ করবে
```

এটা avoid করা ভালো।

বরং:

```
Frontend
   |
   | API call করবে
   |
Backend
   |
   | নিজে জানবে required permission
   |
   | User permission check করবে
```

Example:

User click করলো:

```
Delete Product
```

Frontend call করলো:

```
DELETE /api/products/10/
```

Backend জানে:

```
এই API-এর permission লাগবে:
delete_product
```

তারপর check:

```
User role permission আছে?
        |
        ├── Yes → Delete
        └── No → 403
```

---

তাই final architecture:

```
                Permission Model
                       |
                       |
                    Role
                       |
                       |
                     User


Login
 |
 ↓
Get User Permissions
 |
 ↓
Frontend Menu Control


API Request
 |
 ↓
Backend Permission Check
 |
 ↓
Allow / Reject
```

আপনার মূল চিন্তা **ঠিক আছে**। শুধু মনে রাখবেন:

* Permission দিয়ে menu control → Frontend
* Permission দিয়ে actual security → Backend

এই দুইটা একসাথে রাখলেই production-ready system হবে।
হ্যাঁ, **dynamic permission class বানানো খুব ভালো idea**। Production system-এ সাধারণত একটা reusable permission system বানানো হয়, যাতে প্রতিটি ViewSet-এ বারবার permission check code লিখতে না হয়।

আপনার case-এ দুই ধরনের permission থাকবে:

1. **CRUD permission (automatic)**
2. **Custom business permission**

---

## Structure idea

```text
BasePermissionClass
        |
        |
        ├── CRUD permission generate
        |
        └── Custom permission check
```

---

### Example: Dynamic Permission Class

```python
from rest_framework.permissions import BasePermission


class DynamicPermission(BasePermission):

    def has_permission(self, request, view):

        if not request.user.is_authenticated:
            return False

        required_permission = self.get_required_permission(
            request,
            view
        )

        if not required_permission:
            return True

        return request.user.role.permissions.filter(
            codename=required_permission
        ).exists()


    def get_required_permission(self, request, view):

        # Custom permission first
        if hasattr(view, "required_permission"):
            return view.required_permission


        # CRUD permission
        action = getattr(view, "action", None)

        resource = getattr(
            view,
            "permission_resource",
            None
        )

        if not resource:
            return None


        action_map = {
            "list": "view",
            "retrieve": "view",
            "create": "create",
            "update": "update",
            "partial_update": "update",
            "destroy": "delete",
        }


        if action in action_map:
            return (
                f"{action_map[action]}_{resource}"
            )


        return None
```

---

## Product ViewSet

```python
class ProductViewSet(ModelViewSet):

    permission_resource = "product"
```

Automatic:

```
GET /products/
        |
        view_product


POST /products/
        |
        create_product


DELETE /products/1/
        |
        delete_product
```

---

## Custom Action

ধরি:

```python
@action(
    detail=True,
    methods=["post"]
)
def publish(self, request, pk=None):
    pass
```

এটার জন্য:

```python
class ProductViewSet(ModelViewSet):

    required_permission = "publish_product"
```

বা better:

```python
custom_permissions = {
    "publish": "publish_product",
    "feature": "feature_product",
}
```

---

## Production database:

Permission table:

```
view_product
create_product
update_product
delete_product

publish_product
feature_product
approve_order
refund_order
```

---

## সুবিধা

এভাবে করলে:

✅ নতুন Model add করলে শুধু:

```python
permission_resource = "category"
```

দিলেই CRUD permission কাজ করবে।

✅ Custom action-এর জন্য:

```python
publish_product
approve_order
```

add করা যাবে।

✅ সব API একই permission system follow করবে।

---

আপনার eCommerce project-এর জন্য এই approach ভালো হবে। শুধু permission generation-এর জন্য একটি management command রাখলে আরও ভালো হবে, যেটা নতুন ViewSet scan করে CRUD permission database-এ automatically create করবে।


Dynamic permission map বানানো **ভালো approach**। বিশেষ করে আপনার eCommerce project-এর মতো বড় system-এ এটা maintain করা সহজ হবে।

আপনার idea হবে:

```text
ViewSet
   |
   ↓
Dynamic Permission Map
   |
   ↓
Action অনুযায়ী required permission
   |
   ↓
User Role Permission Check
```

---

### Example: ProductViewSet

```python
class ProductViewSet(ModelViewSet):

    permission_map = {
        "list": "view_product",
        "retrieve": "view_product",
        "create": "create_product",
        "update": "update_product",
        "partial_update": "update_product",
        "destroy": "delete_product",

        "publish": "publish_product",
        "feature": "feature_product",
    }
```

এখন backend:

```python
def get_required_permission(view):
    action = view.action

    return view.permission_map.get(action)
```

যদি request:

```http
GET /products/
```

তাহলে:

```text
action = list

permission = view_product
```

---

যদি:

```http
POST /products/10/publish/
```

তাহলে:

```text
action = publish

permission = publish_product
```

---

তারপর user check:

```python
allowed = request.user.role.permissions.filter(
    codename=required_permission
).exists()
```

---

## আরও scalable করার জন্য Base Class

সব ViewSet-এ map না লিখে:

```python
class BasePermissionViewSet(ModelViewSet):

    permission_map = {}

    def get_required_permission(self):

        return self.permission_map.get(
            self.action
        )
```

Product:

```python
class ProductViewSet(BasePermissionViewSet):

    permission_map = {
        "list": "view_product",
        "create": "create_product",
        "destroy": "delete_product",
        "publish": "publish_product",
    }
```

---

## Dynamic generate + override করলে সবচেয়ে ভালো

CRUD auto:

```text
list       → view_product
create     → create_product
update     → update_product
destroy    → delete_product
```

আর custom:

```python
permission_map = {
    "publish": "publish_product",
    "approve": "approve_product",
}
```

মানে:

```text
Common CRUD → automatic
Business Action → manual map
```

---

আপনার idea ভালো কারণ:

* নতুন API add করলে permission কোথায় লাগবে স্পষ্ট থাকবে।
* Admin permission management সহজ হবে।
* Backend security centralized হবে।

শুধু একটা বিষয় রাখবেন: **permission map backend code-এ থাকবে, frontend থেকে আসবে না।** তাহলে user permission bypass করতে পারবে না।
