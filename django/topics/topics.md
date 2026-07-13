# permission
---------------
1. view level permission
**View-level permission** হলো Django REST Framework (DRF)-এর এমন একটি ব্যবস্থা, যেখানে নির্ধারণ করা হয় **কে একটি View বা ViewSet-এর endpoint access করতে পারবে**।

এটি request View-তে পৌঁছানোর পর, কিন্তু View-এর business logic (`list()`, `create()`, `retrieve()` ইত্যাদি) চালানোর আগে কাজ করে।

## কীভাবে ব্যবহার করা হয়

View বা ViewSet-এ `permission_classes` ব্যবহার করা হয়।

```python
from rest_framework.viewsets import ModelViewSet
from rest_framework.permissions import IsAuthenticated

class CategoryViewSet(ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer
    permission_classes = [IsAuthenticated]
```

এখন শুধু login করা user-ই এই View ব্যবহার করতে পারবে।

---

## DRF-এর কিছু Built-in Permission

### 1. `AllowAny`

সবার জন্য উন্মুক্ত।

```python
from rest_framework.permissions import AllowAny

permission_classes = [AllowAny]
```

---

### 2. `IsAuthenticated`

শুধু authenticated user।

```python
from rest_framework.permissions import IsAuthenticated

permission_classes = [IsAuthenticated]
```

---

### 3. `IsAdminUser`

শুধু `is_staff=True` user।

```python
from rest_framework.permissions import IsAdminUser

permission_classes = [IsAdminUser]
```

---

### 4. `IsAuthenticatedOrReadOnly`

* সবাই `GET` করতে পারবে।
* `POST`, `PUT`, `DELETE` শুধু authenticated user করতে পারবে।

```python
from rest_framework.permissions import IsAuthenticatedOrReadOnly

permission_classes = [IsAuthenticatedOrReadOnly]
```

---

## Custom View Permission

নিজের নিয়মও তৈরি করতে পারেন।

```python
from rest_framework.permissions import BasePermission

class IsSuperUser(BasePermission):
    def has_permission(self, request, view):
        return request.user.is_superuser
```

View-এ ব্যবহার:

```python
permission_classes = [IsSuperUser]
```

---

## `has_permission()` বনাম `has_object_permission()`

### `has_permission()`

View-level permission।

এটি **object database থেকে আনার আগেই** check হয়।

```python
class MyPermission(BasePermission):
    def has_permission(self, request, view):
        return request.user.is_authenticated
```

---

### `has_object_permission()`

Object-level permission।

এটি নির্দিষ্ট object পাওয়ার পরে check হয়।

```python
class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):
        return obj.user == request.user
```

ধরুন `Blog` model-এর owner আছে।

```python
class Blog(models.Model):
    title = models.CharField(max_length=100)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

এখন শুধু owner edit করতে পারবে।

---

## Request Flow

```
Client Request
       │
       ▼
Authentication
       │
       ▼
View Permission (has_permission)
       │
       ▼
Object Retrieve
       │
       ▼
Object Permission (has_object_permission)
       │
       ▼
View Method (list/create/update/delete)
```

অর্থাৎ:

* **View-level permission** → "এই View-তে ঢোকার অনুমতি আছে কি?"
* **Object-level permission** → "এই নির্দিষ্ট object-এর উপর কাজ করার অনুমতি আছে কি?"

এটাই দুটির মূল পার্থক্য।
`get_permissions()` হলো DRF-এর `APIView`/`ViewSet`-এর একটি method, যার মাধ্যমে **runtime-এ** নির্ধারণ করা যায় কোন request-এর জন্য কোন permission ব্যবহার হবে।

অর্থাৎ, একই ViewSet-এ বিভিন্ন action-এর জন্য ভিন্ন permission দিতে পারবেন।

## কেন `get_permissions()` ব্যবহার করা হয়?

ধরুন:

* `list` → সবাই দেখতে পারবে।
* `create` → শুধু authenticated user।
* `destroy` → শুধু admin।

এটা `permission_classes` দিয়ে একসাথে করা যায় না। তখন `get_permissions()` ব্যবহার করা হয়।

### উদাহরণ

```python
from rest_framework.permissions import (
    AllowAny,
    IsAuthenticated,
    IsAdminUser
)
from rest_framework.viewsets import ModelViewSet

class CategoryViewSet(ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

    def get_permissions(self):
        if self.action == "list":
            permission_classes = [AllowAny]
        elif self.action == "create":
            permission_classes = [IsAuthenticated]
        elif self.action == "destroy":
            permission_classes = [IsAdminUser]
        else:
            permission_classes = [IsAuthenticated]

        return [permission() for permission in permission_classes]
```

> লক্ষ্য করুন, শেষে `permission()` লিখে **instance** তৈরি করা হচ্ছে, শুধু class return করা হচ্ছে না।

---

## `self.action` কী?

`ViewSet`-এ DRF নিজেই `self.action` সেট করে।

উদাহরণ:

| Request                       | `self.action`             |
| ----------------------------- | ------------------------- |
| `GET /categories/`            | `list`                    |
| `GET /categories/5/`          | `retrieve`                |
| `POST /categories/`           | `create`                  |
| `PUT /categories/5/`          | `update`                  |
| `PATCH /categories/5/`        | `partial_update`          |
| `DELETE /categories/5/`       | `destroy`                 |
| `POST /categories/5/restore/` | `restore` (custom action) |

তাই custom action-এর জন্যও permission আলাদা দিতে পারেন।

```python
from rest_framework.permissions import IsAdminUser

class CategoryViewSet(ModelViewSet):

    @action(detail=True, methods=["post"])
    def restore(self, request, pk=None):
        ...

    def get_permissions(self):
        if self.action == "restore":
            return [IsAdminUser()]
        return super().get_permissions()
```

এখানে `restore` endpoint শুধুমাত্র admin ব্যবহার করতে পারবে, আর অন্য action-গুলোর জন্য `permission_classes` (বা parent implementation) অনুযায়ী permission প্রয়োগ হবে।

### `permission_classes` বনাম `get_permissions()`

* `permission_classes` → সব action-এর জন্য একই permission।
* `get_permissions()` → action বা request অনুযায়ী permission পরিবর্তন করা যায়।

তাই যখন বিভিন্ন endpoint-এর জন্য বিভিন্ন access rule দরকার হয়, তখন `get_permissions()` সবচেয়ে উপযোগী।


--------

DRF ViewSet-এ **action name** বলতে `self.action`-এর value বোঝায়। এটি বলে দেয় বর্তমানে কোন ViewSet method call হয়েছে।

### Built-in action names

| HTTP Method | URL              | Action name (`self.action`) |
| ----------- | ---------------- | --------------------------- |
| GET         | `/categories/`   | `list`                      |
| POST        | `/categories/`   | `create`                    |
| GET         | `/categories/1/` | `retrieve`                  |
| PUT         | `/categories/1/` | `update`                    |
| PATCH       | `/categories/1/` | `partial_update`            |
| DELETE      | `/categories/1/` | `destroy`                   |

---

### Custom action-এর ক্ষেত্রে

আপনি যদি লেখেন:

```python
from rest_framework.decorators import action

class CategoryViewSet(ModelViewSet):

    @action(detail=True, methods=["post"])
    def restore(self, request, pk=None):
        ...
```

তাহলে:

```python
self.action == "restore"
```

হবে।

আরেকটি উদাহরণ:

```python
@action(detail=True, methods=["delete"])
def hard_delete(self, request, pk=None):
    ...
```

এখানে:

```python
self.action == "hard_delete"
```

---

### `get_permissions()`-এ ব্যবহার

```python
def get_permissions(self):
    if self.action == "restore":
        return [IsAdminUser()]

    if self.action == "destroy":
        return [IsAdminUser()]

    return [IsAuthenticated()]
```

এখন:

* `restore` → admin দরকার
* `destroy` → admin দরকার
* অন্য action → authenticated user দরকার

---

### নিজের action name দেখতে চাইলে

Temporary test:

```python
def get_permissions(self):
    print(self.action)
    return super().get_permissions()
```

Request পাঠালে terminal-এ action name দেখাবে।

--------
যদি `list` action-এ কোনো permission না দিতে চান (মানে সবাই access করতে পারবে), তাহলে `list`-এর জন্য `AllowAny` ব্যবহার করতে পারেন।

উদাহরণ:

```python id="qj5x5b"
from rest_framework.permissions import IsAdminUser, IsAuthenticated, AllowAny

def get_permissions(self):
    if self.action == 'list':
        return [AllowAny()]

    if self.action in ['create', 'update', 'destroy', 'restore', 'hard_delete']:
        return [IsAdminUser()]

    return [IsAuthenticated()]
```

এখন:

* `GET /categories/` → সবাই পারবে (`list`)
* `POST /categories/` → শুধু admin
* `PUT /categories/1/` → শুধু admin
* `DELETE /categories/1/` → শুধু admin
* `restore` → শুধু admin
* `hard_delete` → শুধু admin
* অন্য action → authenticated user

আর যদি আপনি একদম কোনো permission check-ই না চান, তাহলে `AllowAny()`-ই DRF-এর সঠিক উপায়। `[]` return করলে permission system অস্বাভাবিক আচরণ করতে পারে।


-------
DRF-এ **user role wise permission** দিতে হলে সাধারণত নিজের role system তৈরি করে custom permission class ব্যবহার করা হয়।

ধরুন আপনার user role হবে:

* `admin`
* `author`
* `user`

---

## 1. User model-এ role field যোগ করুন

যদি custom user model থাকে:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):

    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('author', 'Author'),
        ('user', 'User'),
    )

    role = models.CharField(
        max_length=20,
        choices=ROLE_CHOICES,
        default='user'
    )
```

Migration:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 2. Custom Permission তৈরি করুন

`permissions.py`

```python
from rest_framework.permissions import BasePermission


class IsAdmin(BasePermission):
    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == 'admin'


class IsAuthor(BasePermission):
    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == 'author'


class IsAdminOrAuthor(BasePermission):
    def has_permission(self, request, view):
        return (
            request.user.is_authenticated
            and request.user.role in ['admin', 'author']
        )
```

---

## 3. ViewSet-এ role অনুযায়ী permission দিন

Example:

```python
from .permissions import IsAdmin, IsAdminOrAuthor


class BlogViewSet(ModelViewSet):

    serializer_class = BlogSerializer

    def get_permissions(self):

        if self.action in [
            'create'
        ]:
            return [IsAdminOrAuthor()]

        if self.action in [
            'update',
            'partial_update',
            'destroy'
        ]:
            return [IsAdmin()]

        return []
```

এখন:

| Action      | Permission     |
| ----------- | -------------- |
| create blog | Admin + Author |
| update blog | Admin          |
| delete blog | Admin          |
| list blog   | সবাই           |

---

## 4. Object owner অনুযায়ী permission

যদি author শুধু নিজের blog edit করতে পারে:

```python
class IsOwnerOrAdmin(BasePermission):

    def has_object_permission(self, request, view, obj):

        if request.user.role == 'admin':
            return True

        return obj.author == request.user
```

ViewSet:

```python
permission_classes = [IsOwnerOrAdmin]
```

---

## 5. আপনার Category example অনুযায়ী

```python
def get_permissions(self):

    if self.action in [
        'create',
        'update',
        'partial_update',
        'destroy',
        'restore',
        'hard_delete'
    ]:
        return [IsAdmin()]

    return [AllowAny()]
```

Result:

* Admin → CRUD + restore + hard delete
* Author/User → শুধু view করতে পারবে

---
হ্যাঁ, **role-wise permission দিতে চাইলে custom permission class তৈরি করা ভালো practice**। তবে ছোট project হলে `get_permissions()`-এর ভিতরেও role check করতে পারেন।

দুইটা approach আছে।

---

## Approach 1: `get_permissions()` এর ভিতরে role check (ছোট project)

ধরুন আপনার User model-এ আছে:

```python
role = models.CharField(max_length=20)
```

তাহলে:

```python
def get_permissions(self):
    if self.action in ['create', 'update', 'destroy']:
        if self.request.user.role == 'admin':
            return [AllowAny()]
        return [IsAuthenticated()]

    return [AllowAny()]
```

এটা কাজ করবে, কিন্তু বড় project-এ code বেশি জটিল হয়ে যায়।

---

## Approach 2: Custom Permission Class (Recommended)

`permissions.py`

```python
from rest_framework.permissions import BasePermission


class IsAdminRole(BasePermission):
    def has_permission(self, request, view):
        return (
            request.user.is_authenticated
            and request.user.role == 'admin'
        )


class IsAuthorRole(BasePermission):
    def has_permission(self, request, view):
        return (
            request.user.is_authenticated
            and request.user.role == 'author'
        )
```

তারপর ViewSet-এ:

```python
from .permissions import IsAdminRole


class CategoryViewSet(ModelViewSet):

    def get_permissions(self):
        if self.action in [
            'create',
            'update',
            'partial_update',
            'destroy',
            'restore',
            'hard_delete'
        ]:
            return [IsAdminRole()]

        return [AllowAny()]
```

---

## Multiple role allow করতে চাইলে

যেমন admin এবং author দুজনই create করতে পারবে:

```python
class IsAdminOrAuthor(BasePermission):

    def has_permission(self, request, view):
        return (
            request.user.is_authenticated
            and request.user.role in ['admin', 'author']
        )
```

---

## কখন কোনটা ব্যবহার করবেন?

| Situation                | Use                         |
| ------------------------ | --------------------------- |
| 2-3টা role, ছোট API      | `get_permissions()`         |
| অনেক role, অনেক ViewSet  | Custom Permission           |
| Object owner check দরকার | `has_object_permission()`   |
| Enterprise project       | Django Groups + Permissions |

আপনার blog project-এর জন্য (admin, author, user role থাকলে) **custom permission class + `get_permissions()` combination** সবচেয়ে clean হবে।


-----


আরেকটি Django standard approach হলো **Groups + Django Model Permission** ব্যবহার করা, যেখানে admin/author/editor group বানিয়ে permission assign করা হয়। বড় project-এ সাধারণত সেটাই বেশি ব্যবহার করা হয়।

---------

হ্যাঁ, আপনি যদি এভাবে বলেন:

```python
if self.request.user.role == 'admin':
```

তাহলে **কাজ করবে**, তবে শর্ত হলো আপনার `User` model-এ `role` নামে একটি field থাকতে হবে।

উদাহরণ:

```python
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('author', 'Author'),
        ('user', 'User'),
    )

    role = models.CharField(
        max_length=20,
        choices=ROLE_CHOICES,
        default='user'
    )
```

তাহলে database-এ:

| username | role   |
| -------- | ------ |
| rahim    | user   |
| karim    | author |
| admin    | admin  |

এখন ViewSet-এ:

```python
def get_queryset(self):
    if self.request.user.role == 'admin':
        return Category.all_objects.all()

    return Category.objects.all()
```

এটা কাজ করবে।

---

কিন্তু যদি আপনার User model-এ `role` field না থাকে, তাহলে:

```python
self.request.user.role
```

করলে error হবে:

```
AttributeError: 'User' object has no attribute 'role'
```

---

আরেকটা বিষয়: unauthenticated user হলে `AnonymousUser` আসতে পারে। তাই safe ভাবে লিখা ভালো:

```python
def get_queryset(self):
    if self.request.user.is_authenticated and self.request.user.role == 'admin':
        return Category.all_objects.all()

    return Category.objects.all()
```

তাহলে login না করা user-এর ক্ষেত্রেও error হবে না।

আপনার যদি `role` field ব্যবহার করে admin/author/user manage করার plan থাকে, তাহলে এই approach ঠিক আছে।



2. queryset and get_queryset
Django REST Framework (DRF)-এ `queryset` এবং `get_queryset()` দুটোই database থেকে data আনার জন্য ব্যবহার হয়, কিন্তু তাদের ব্যবহারের ক্ষেত্রে পার্থক্য আছে।

## 1. `queryset`

`queryset` হলো View/ViewSet-এর একটি class attribute। এটি সাধারণত fixed queryset দেওয়ার জন্য ব্যবহার করা হয়।

উদাহরণ:

```python
from rest_framework.viewsets import ModelViewSet

class CategoryViewSet(ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer
```

এখানে সব request-এর জন্য একই queryset ব্যবহার হবে।

যেমন:

```python
GET /categories/
```

→ `Category.objects.all()`

```python
GET /categories/1/
```

→ একই queryset থেকে id=1 খুঁজবে।

---

## 2. `get_queryset()`

`get_queryset()` হলো একটি method। এটি ব্যবহার করলে runtime অনুযায়ী queryset পরিবর্তন করা যায়।

উদাহরণ:

```python
class CategoryViewSet(ModelViewSet):
    serializer_class = CategorySerializer

    def get_queryset(self):
        return Category.objects.all()
```

এটিও `queryset`-এর মতো কাজ করে।

---

## কেন `get_queryset()` বেশি ব্যবহার করা হয়?

কারণ এখানে condition দিতে পারেন।

### User অনুযায়ী data filter:

```python
class BlogViewSet(ModelViewSet):
    serializer_class = BlogSerializer

    def get_queryset(self):
        return Blog.objects.filter(
            author=self.request.user
        )
```

এখন প্রত্যেক user শুধু নিজের blog দেখতে পারবে।

---

### Action অনুযায়ী আলাদা queryset:

আপনার soft delete-এর ক্ষেত্রে:

```python
class CategoryViewSet(ModelViewSet):
    serializer_class = CategorySerializer

    def get_queryset(self):
        if self.action == "restore":
            return Category.all_objects.all()

        return Category.objects.all()
```

এখানে:

* সাধারণ list/retrieve → deleted data আসবে না
* restore action → deleted data-ও পাওয়া যাবে

---

## `queryset` বনাম `get_queryset()`

| বিষয়                     | queryset  | get_queryset()   |
| ------------------------ | --------- | ---------------- |
| Type                     | attribute | method           |
| Dynamic filtering        | ❌         | ✅                |
| User-based data          | ❌         | ✅                |
| Action অনুযায়ী পরিবর্তন | ❌         | ✅                |
| Simple CRUD              | ✅         | ✅                |
| Complex API              | সীমিত     | বেশি ব্যবহার হয় |

---

## গুরুত্বপূর্ণ বিষয়

যদি `get_queryset()` লিখেন, তাহলে সাধারণত `queryset` দেওয়ার দরকার নেই।

এভাবে:

```python
class CategoryViewSet(ModelViewSet):
    serializer_class = CategorySerializer

    def get_queryset(self):
        return Category.objects.all()
```

এটাই যথেষ্ট।

আপনার soft delete project-এর ক্ষেত্রে `get_queryset()` ব্যবহার করা বেশি উপযুক্ত, কারণ `restore` এবং `hard_delete` action-এর জন্য আলাদা manager (`all_objects`) দরকার হচ্ছে।


----------


Django REST Framework (DRF)-এ **`serializer_context`** এবং **`get_serializer_context()`** ব্যবহার করা হয় Serializer-এর ভিতরে অতিরিক্ত data পাঠানোর জন্য।

মূলত Serializer শুধু `instance` বা `data` পায়, কিন্তু অনেক সময় Serializer-এর ভিতরে request, user, view ইত্যাদি দরকার হয়। তখন context ব্যবহার করা হয়।

---

## 1. `serializer_context` কী?

`serializer_context` হলো একটি dictionary যেটা Serializer-এ পাঠানো হয়।

Example:

```python
serializer = BlogSerializer(
    blog,
    context={
        'request': request
    }
)
```

এখন Serializer-এর ভিতরে:

```python
self.context
```

দিয়ে এটি পাওয়া যাবে।

---

## 2. DRF default serializer context

DRF নিজে থেকেই কিছু context পাঠায়:

```python
{
    'request': request,
    'format': format,
    'view': self
}
```

অর্থাৎ সাধারণভাবে:

```python
class BlogSerializer(serializers.ModelSerializer):

    def validate(self, attrs):
        print(self.context)
        return attrs
```

Output:

```python
{
 'request': <Request>,
 'format': None,
 'view': <BlogViewSet>
}
```

---

# 3. `get_serializer_context()`

ViewSet-এর একটি method।

Default implementation:

```python
def get_serializer_context(self):
    return {
        'request': self.request,
        'format': self.format_kwarg,
        'view': self
    }
```

আপনি এটাকে override করে নিজের data যোগ করতে পারেন।

---

## Example 1: User Serializer-এ পাঠানো

ViewSet:

```python
class BlogViewSet(ModelViewSet):

    serializer_class = BlogSerializer
    queryset = Blog.objects.all()

    def get_serializer_context(self):
        context = super().get_serializer_context()

        context['user_role'] = self.request.user.role

        return context
```

এখন Serializer-এ:

```python
class BlogSerializer(serializers.ModelSerializer):

    def validate(self, attrs):
        role = self.context.get('user_role')

        if role != 'admin':
            raise serializers.ValidationError(
                "Only admin can create blog"
            )

        return attrs
```

---

# 4. Request user access করা

সবচেয়ে বেশি ব্যবহার:

View:

```python
def get_serializer_context(self):
    return {
        'request': self.request
    }
```

Serializer:

```python
class BlogSerializer(serializers.ModelSerializer):

    def create(self, validated_data):

        user = self.context['request'].user

        return Blog.objects.create(
            author=user,
            **validated_data
        )
```

এখন frontend থেকে author পাঠানোর দরকার নেই।

POST:

```json
{
    "title": "My Blog",
    "description": "Hello"
}
```

Backend নিজে:

```
author = logged in user
```

set করবে।

---

# 5. Serializer-এ request ব্যবহার

Example:

Model:

```python
class Blog(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
```

Serializer:

```python
class BlogSerializer(serializers.ModelSerializer):

    is_owner = serializers.SerializerMethodField()

    class Meta:
        model = Blog
        fields = [
            'id',
            'title',
            'is_owner'
        ]

    def get_is_owner(self, obj):
        user = self.context['request'].user

        return obj.author == user
```

Response:

```json
{
    "id": 1,
    "title": "Django Tutorial",
    "is_owner": true
}
```

---

# 6. Custom context পাঠানো

View:

```python
def get_serializer_context(self):

    context = super().get_serializer_context()

    context['company_name'] = "ABC Ltd"

    return context
```

Serializer:

```python
company = self.context['company_name']
```

---

# 7. `serializer_context` বনাম `get_serializer_context()`

| বিষয়              | serializer_context        | get_serializer_context |
| ----------------- | ------------------------- | ---------------------- |
| কোথায় ব্যবহার    | Serializer call করার সময় | View/ViewSet-এ         |
| Custom data       | ✅                         | ✅                      |
| Automatically আসে | ❌                         | ✅                      |
| ViewSet-এর জন্য   | কম ব্যবহার                | বেশি ব্যবহার           |

---

## আপনার Blog project-এর ক্ষেত্রে useful example

ধরুন:

* Admin সব category দেখতে পারবে
* Reporter শুধু নিজের blog edit করতে পারবে

তাহলে:

```python
def get_serializer_context(self):
    context = super().get_serializer_context()

    context['role'] = self.request.user.role

    return context
```

Serializer:

```python
role = self.context.get('role')

if role == 'reporter':
    ...
```

---

সংক্ষেপে:

* **`serializer_context` = Serializer-এ extra information পাঠানোর container**
* **`get_serializer_context()` = ViewSet থেকে সেই container customize করার method**
* সবচেয়ে common ব্যবহার: `request.user`, logged-in user, role, permissions, URL info Serializer-এর ভিতরে ব্যবহার করা।

------------


হ্যাঁ, **process ঠিক আছে**। তবে আরও একটি সহজ উপায় আছে।

আপনার code:

```python
def get_serializer_context(self):
    context = super().get_serializer_context()
    context['user'] = self.request.user
    return context
```

এখন serializer-এ:

```python
user = self.context['user']
```

এভাবে user পাবেন।

---

### তবে DRF-এ আরও standard উপায়

`super().get_serializer_context()` নিজেই `request` context-এ পাঠায়।

অর্থাৎ আপনি সরাসরি serializer-এ লিখতে পারেন:

```python
user = self.context['request'].user
```

এক্ষেত্রে `get_serializer_context()` override করারই দরকার নেই।

```python
def create(self, validated_data):
    user = self.context['request'].user
    tags = validated_data.pop('tags', [])

    blog = Blog.objects.create(
        user=user,
        **validated_data
    )

    blog.tags.set(tags)
    return blog
```

### কোনটা ভালো?

* যদি শুধু logged-in user দরকার হয়, তাহলে **`self.context['request'].user`** ব্যবহার করাই বেশি প্রচলিত।
* যদি `request.user` ছাড়াও extra data (যেমন `role`, `company`, `ip_address`) পাঠাতে চান, তখন `get_serializer_context()` override করা ভালো।

অর্থাৎ আপনার `get_serializer_context()` ভুল নয়, কিন্তু **শুধু user পাঠানোর জন্য এটি প্রয়োজনীয়ও নয়**, কারণ `request.user` আগেই context-এ থাকে।

----------


যদি Serializer-এ লিখেন:

```python
user = self.context['request'].user
```

তাহলে **View-এ কিছুই extra লিখতে হবে না**।

কারণ `ModelViewSet`-এর default `get_serializer_context()` নিজেই `request` পাঠিয়ে দেয়।

অর্থাৎ ViewSet এমন থাকলেই হবে:

```python
class BlogViewSet(ModelViewSet):
    queryset = Blog.objects.all()
    serializer_class = BlogSerializer
```

Serializer:

```python
class BlogSerializer(ModelSerializer):

    def create(self, validated_data):
        user = self.context['request'].user
        tags = validated_data.pop('tags', [])

        blog = Blog.objects.create(
            user=user,
            **validated_data
        )

        blog.tags.set(tags)
        return blog
```

এটাই যথেষ্ট।

---

### কখন `get_serializer_context()` override করবেন?

যখন `request` ছাড়াও নিজের data পাঠাতে চান।

উদাহরণ:

```python
def get_serializer_context(self):
    context = super().get_serializer_context()
    context['role'] = self.request.user.role
    context['company'] = self.request.user.company
    return context
```

Serializer:

```python
role = self.context['role']
company = self.context['company']
```

---

### সংক্ষেপে

* `self.context['request'].user` ব্যবহার করলে → **View-এ কিছু লিখতে হবে না।**
* Custom data (যেমন `role`, `company`, `department`) পাঠাতে চাইলে → `get_serializer_context()` override করবেন।

এটাই DRF-এর standard practice।


------------

`@action` হলো DRF-এর একটি decorator, যা **ViewSet-এর মধ্যে custom endpoint** তৈরি করতে ব্যবহৃত হয়। যখন CRUD (`list`, `create`, `retrieve`, `update`, `destroy`) এর বাইরে কোনো extra operation দরকার হয়, তখন `@action` ব্যবহার করা হয়।

---

# 1. কোথায় লিখবেন?

`ViewSet`-এর ভিতরে method হিসেবে লিখবেন।

```python
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.viewsets import ModelViewSet

class BlogViewSet(ModelViewSet):

    queryset = Blog.objects.all()
    serializer_class = BlogSerializer

    @action(detail=True, methods=['post'])
    def publish(self, request, pk=None):
        ...
```

---

# 2. Syntax

```python
@action(
    detail=True/False,
    methods=['get', 'post', 'put', 'delete']
)
def action_name(self, request, pk=None):
    ...
```

---

# 3. `detail=True`

একটি নির্দিষ্ট object-এর উপর action চালাতে।

```python
@action(detail=True, methods=['post'])
def restore(self, request, pk=None):

    blog = self.get_object()

    blog.restore()

    return Response({
        "message": "Restored"
    })
```

URL হবে

```
POST /blogs/5/restore/
```

এখানে `5` হলো blog id।

---

# 4. `detail=False`

Collection-এর উপর action চালাতে।

```python
@action(detail=False, methods=['get'])
def featured(self, request):

    blogs = Blog.objects.filter(is_featured=True)

    serializer = self.get_serializer(blogs, many=True)

    return Response(serializer.data)
```

URL

```
GET /blogs/featured/
```

এখানে কোনো id নেই।

---

# 5. কখন Action ব্যবহার করবেন?

যখন CRUD-এর বাইরে কোনো কাজ করবেন।

যেমন

```
restore
hard_delete
publish
unpublish
like
dislike
bookmark
approve
reject
add_tags
remove_tags
```

---

# 6. Example: Restore

```python
@action(detail=True, methods=['post'])
def restore(self, request, pk=None):

    blog = self.get_object()

    blog.restore()

    return Response({
        "message": "Blog restored"
    })
```

URL

```
POST /blogs/3/restore/
```

---

# 7. Example: Hard Delete

```python
@action(detail=True, methods=['delete'])
def hard_delete(self, request, pk=None):

    blog = self.get_object()

    blog.hard_delete()

    return Response({
        "message": "Deleted"
    })
```

URL

```
DELETE /blogs/3/hard_delete/
```

---

# 8. Example: Publish Blog

```python
@action(detail=True, methods=['post'])
def publish(self, request, pk=None):

    blog = self.get_object()

    blog.status = "published"

    blog.save()

    return Response({
        "message": "Published"
    })
```

---

# 9. Example: Like Blog

```python
@action(detail=True, methods=['post'])
def like(self, request, pk=None):

    blog = self.get_object()

    blog.likes_count += 1

    blog.save()

    return Response({
        "likes": blog.likes_count
    })
```

URL

```
POST /blogs/1/like/
```

---

# 10. Example: Add Tags

```python
@action(detail=True, methods=['post'])
def add_tags(self, request, pk=None):

    blog = self.get_object()

    tag_ids = request.data.get("tags", [])

    blog.tags.add(*tag_ids)

    return Response({
        "message": "Tags added"
    })
```

Request

```json
{
    "tags": [1,2,5]
}
```

---

# 11. Example: Remove Tags

```python
@action(detail=True, methods=['post'])
def remove_tags(self, request, pk=None):

    blog = self.get_object()

    tag_ids = request.data.get("tags", [])

    blog.tags.remove(*tag_ids)

    return Response({
        "message": "Tags removed"
    })
```

---

# 12. Action-এ Serializer ব্যবহার

```python
@action(detail=True, methods=['post'])
def add_comment(self, request, pk=None):

    blog = self.get_object()

    serializer = CommentSerializer(
        data=request.data,
        context={
            "request": request
        }
    )

    serializer.is_valid(raise_exception=True)

    serializer.save(blog=blog)

    return Response(serializer.data)
```

---

# 13. Permission

`get_permissions()`-এ action name ব্যবহার করতে পারেন।

```python
def get_permissions(self):

    if self.action in [
        "restore",
        "hard_delete"
    ]:
        return [IsAdminUser()]

    return [AllowAny()]
```

---

# 14. URL

ধরুন router:

```python
router.register(
    "blogs",
    BlogViewSet
)
```

তাহলে

| Action      | Method | URL                     |
| ----------- | ------ | ----------------------- |
| list        | GET    | `/blogs/`               |
| retrieve    | GET    | `/blogs/1/`             |
| create      | POST   | `/blogs/`               |
| update      | PUT    | `/blogs/1/`             |
| destroy     | DELETE | `/blogs/1/`             |
| restore     | POST   | `/blogs/1/restore/`     |
| hard_delete | DELETE | `/blogs/1/hard_delete/` |
| like        | POST   | `/blogs/1/like/`        |
| publish     | POST   | `/blogs/1/publish/`     |
| featured    | GET    | `/blogs/featured/`      |

---

## `@action`-এ সাধারণত কী লিখবেন?

প্রায় সব action-এর structure একই রকম হয়:

```python
@action(detail=True, methods=["post"])
def action_name(self, request, pk=None):
    instance = self.get_object()      # নির্দিষ্ট object নিন

    # Custom business logic লিখুন

    serializer = self.get_serializer(instance)  # দরকার হলে
    return Response(serializer.data)            # অথবা custom response
```

অর্থাৎ, `@action` ব্যবহার করবেন তখনই যখন ViewSet-এর standard CRUD operation-এর বাইরে কোনো অতিরিক্ত কাজ করতে হবে। এটি custom endpoint তৈরি করার DRF-এর standard উপায়।


-------

হ্যাঁ। `ModelViewSet` অনেকগুলো **built-in action** দেয়। এগুলোর নাম জানা খুব গুরুত্বপূর্ণ, কারণ `self.action` এবং `get_permissions()`-এ এগুলোই ব্যবহার করেন।

## ModelViewSet-এর Built-in Actions

| Action           | HTTP Method | URL         | Description            |
| ---------------- | ----------- | ----------- | ---------------------- |
| `list`           | GET         | `/blogs/`   | সব object দেখায়       |
| `retrieve`       | GET         | `/blogs/1/` | একটি object দেখায়     |
| `create`         | POST        | `/blogs/`   | নতুন object তৈরি করে   |
| `update`         | PUT         | `/blogs/1/` | পুরো object update করে |
| `partial_update` | PATCH       | `/blogs/1/` | আংশিক update করে       |
| `destroy`        | DELETE      | `/blogs/1/` | object delete করে      |

---

## কোন action কোন method call করে?

### 1. list

```
GET /blogs/
```

DRF call করে

```python
def list(self, request, *args, **kwargs):
```

---

### 2. retrieve

```
GET /blogs/1/
```

Call করে

```python
def retrieve(self, request, *args, **kwargs):
```

---

### 3. create

```
POST /blogs/
```

Call করে

```python
def create(self, request, *args, **kwargs):
```

এবং ভিতরে

```python
perform_create(serializer)
```

call হয়।

---

### 4. update

```
PUT /blogs/1/
```

Call করে

```python
def update(self, request, *args, **kwargs):
```

এবং

```python
perform_update(serializer)
```

call হয়।

---

### 5. partial_update

```
PATCH /blogs/1/
```

Call করে

```python
def partial_update(self, request, *args, **kwargs):
```

এবং

```python
perform_update(serializer)
```

call হয়।

---

### 6. destroy

```
DELETE /blogs/1/
```

Call করে

```python
def destroy(self, request, *args, **kwargs):
```

এবং

```python
perform_destroy(instance)
```

call হয়।

---

# Override করতে চাইলে

### list

```python
def list(self, request, *args, **kwargs):
    queryset = self.get_queryset()

    serializer = self.get_serializer(queryset, many=True)

    return Response(serializer.data)
```

---

### retrieve

```python
def retrieve(self, request, *args, **kwargs):

    instance = self.get_object()

    serializer = self.get_serializer(instance)

    return Response(serializer.data)
```

---

### create

```python
def create(self, request, *args, **kwargs):

    serializer = self.get_serializer(data=request.data)

    serializer.is_valid(raise_exception=True)

    self.perform_create(serializer)

    return Response(serializer.data)
```

---

### perform_create

```python
def perform_create(self, serializer):
    serializer.save(user=self.request.user)
```

---

### update

```python
def update(self, request, *args, **kwargs):
    ...
```

---

### perform_update

```python
def perform_update(self, serializer):
    serializer.save()
```

---

### destroy

```python
def destroy(self, request, *args, **kwargs):
    ...
```

---

### perform_destroy

```python
def perform_destroy(self, instance):
    instance.soft_delete()
```

---

# Built-in helper methods

`ModelViewSet`-এ আরও কিছু গুরুত্বপূর্ণ method আছে, যেগুলো প্রায়ই override করা হয়:

```python
get_queryset()
```

```python
get_serializer()
```

```python
get_serializer_class()
```

```python
get_serializer_context()
```

```python
get_permissions()
```

```python
get_object()
```

```python
filter_queryset()
```

```python
paginate_queryset()
```

---

# self.action-এ কী কী value আসে?

```python
self.action
```

এর value হতে পারে:

```python
list
retrieve
create
update
partial_update
destroy
```

এবং আপনার custom action:

```python
restore
hard_delete
publish
like
bookmark
```

---

## Interview/প্র্যাকটিক্যালের জন্য সবচেয়ে গুরুত্বপূর্ণ methods

```text
list()
retrieve()
create()
update()
partial_update()
destroy()

perform_create()
perform_update()
perform_destroy()

get_queryset()
get_object()

get_serializer()
get_serializer_class()
get_serializer_context()

get_permissions()

filter_queryset()

paginate_queryset()
```

এগুলোই `ModelViewSet`-এ সবচেয়ে বেশি ব্যবহৃত built-in methods এবং actions।

----
এটা খুব গুরুত্বপূর্ণ প্রশ্ন। DRF-এ **সব action override করার দরকার নেই**। কোন পরিস্থিতিতে কোন method override করবেন, সেটা জানা বেশি জরুরি।

নিচে একে একে দেখানো হলো।

---

# 1. `get_queryset()`

**কখন override করবেন?**

যখন user অনুযায়ী different queryset দেখাতে চান।

Example:

```python
def get_queryset(self):
    if self.request.user.role == "admin":
        return Blog.all_objects.all()

    return Blog.objects.filter(status="published")
```

ব্যবহার:

* Role-based queryset
* Soft delete
* Logged-in user-এর own data

---

# 2. `perform_create()`

**কখন override করবেন?**

শুধু save করার আগে extra data add করতে।

Example:

```python
def perform_create(self, serializer):
    serializer.save(user=self.request.user)
```

ব্যবহার:

* Logged-in user assign
* Company assign
* Organization assign

এটা `create()` override করার চেয়ে cleaner।

---

# 3. `create()`

**কখন override করবেন?**

যখন পুরো create process পরিবর্তন করতে হবে।

Example:

```python
def create(self, request, *args, **kwargs):

    if Blog.objects.filter(title=request.data["title"]).exists():
        return Response(
            {"error": "Already exists"},
            status=400
        )

    return super().create(request, *args, **kwargs)
```

ব্যবহার:

* Custom response
* Extra validation
* Different status code

---

# 4. `perform_update()`

**কখন override করবেন?**

Update-এর সময় extra field save করতে।

```python
def perform_update(self, serializer):
    serializer.save(updated_by=self.request.user)
```

---

# 5. `update()`

**কখন override করবেন?**

PUT request-এর পুরো flow change করতে।

Example

```python
def update(self, request, *args, **kwargs):

    print("Updating")

    return super().update(request, *args, **kwargs)
```

---

# 6. `partial_update()`

PATCH request customize করতে।

```python
def partial_update(self, request, *args, **kwargs):
    return super().partial_update(request, *args, **kwargs)
```

---

# 7. `perform_destroy()`

Soft delete-এর জন্য সবচেয়ে common।

```python
def perform_destroy(self, instance):
    instance.soft_delete()
```

---

# 8. `destroy()`

যদি delete-এর আগে check করতে চান।

```python
def destroy(self, request, *args, **kwargs):

    instance = self.get_object()

    if instance.status == "published":
        return Response(
            {"error": "Can't delete"}
        )

    return super().destroy(request, *args, **kwargs)
```

---

# 9. `retrieve()`

একটি object দেখানোর সময় extra কাজ।

Example:

```python
def retrieve(self, request, *args, **kwargs):

    blog = self.get_object()

    blog.views += 1
    blog.save()

    serializer = self.get_serializer(blog)

    return Response(serializer.data)
```

ব্যবহার:

* View count
* Recent history
* BlogView create

---

# 10. `list()`

List API customize করতে।

```python
def list(self, request, *args, **kwargs):

    queryset = self.filter_queryset(
        self.get_queryset()
    )

    serializer = self.get_serializer(
        queryset,
        many=True
    )

    return Response({
        "count": queryset.count(),
        "data": serializer.data
    })
```

---

# 11. `get_permissions()`

Role-wise permission

```python
def get_permissions(self):

    if self.action in ["list", "retrieve"]:
        return [AllowAny()]

    return [IsAdminUser()]
```

---

# 12. `get_serializer_class()`

Different action-এ different serializer

```python
def get_serializer_class(self):

    if self.action == "list":
        return BlogListSerializer

    if self.action == "retrieve":
        return BlogDetailSerializer

    return BlogSerializer
```

---

# 13. `get_serializer_context()`

Extra data পাঠাতে।

```python
def get_serializer_context(self):

    context = super().get_serializer_context()

    context["role"] = self.request.user.role

    return context
```

Serializer

```python
role = self.context["role"]
```

---

# 14. `get_object()`

Object fetch customize করতে।

```python
def get_object(self):

    obj = super().get_object()

    print(obj)

    return obj
```

---

# 15. `@action`

CRUD-এর বাইরে custom endpoint

```python
@action(detail=True, methods=["post"])
def publish(self, request, pk=None):

    blog = self.get_object()

    blog.status = "published"

    blog.save()

    return Response({
        "message": "Published"
    })
```

---

# Practical Rule (মনে রাখার সহজ উপায়)

| Requirement                     | Override                   |
| ------------------------------- | -------------------------- |
| User অনুযায়ী data দেখাব        | `get_queryset()`           |
| Save করার সময় extra field add  | `perform_create()`         |
| Update-এর সময় extra field      | `perform_update()`         |
| Soft delete                     | `perform_destroy()`        |
| Create process পরিবর্তন         | `create()`                 |
| Retrieve-এর সময় view count/log | `retrieve()`               |
| List response customize         | `list()`                   |
| Role-wise permission            | `get_permissions()`        |
| Different serializer            | `get_serializer_class()`   |
| Serializer-এ extra data         | `get_serializer_context()` |
| CRUD-এর বাইরে endpoint          | `@action`                  |

### একটি সহজ guideline

* **শুধু save-এর সময় কিছু যোগ করতে হলে** → `perform_create()`, `perform_update()`, `perform_destroy()`
* **Request/Response-এর পুরো flow বদলাতে হলে** → `create()`, `update()`, `retrieve()`, `list()`, `destroy()`
* **Configuration পরিবর্তন করতে হলে** → `get_queryset()`, `get_permissions()`, `get_serializer_class()`, `get_serializer_context()`
* **নতুন endpoint দরকার হলে** → `@action`


--------

হ্যাঁ, Django-তে অনেক **shortcut methods/functions** আছে, যেগুলো খুব বেশি ব্যবহৃত হয়। নিচে গুরুত্বপূর্ণগুলো উদাহরণসহ দিলাম।

---

# 1. `get_object_or_404()`

Object না পেলে `Http404` raise করে।

```python
from django.shortcuts import get_object_or_404

blog = get_object_or_404(Blog, id=1)
```

এটা equivalent:

```python
try:
    blog = Blog.objects.get(id=1)
except Blog.DoesNotExist:
    raise Http404
```

---

# 2. `get_list_or_404()`

Queryset empty হলে `Http404` raise করে।

```python
from django.shortcuts import get_list_or_404

blogs = get_list_or_404(Blog, status="published")
```

---

# 3. `get_or_create()`

Object থাকলে সেটাই দেয়, না থাকলে create করে।

```python
tag, created = Tag.objects.get_or_create(
    name="Django"
)
```

`created` হবে:

* `True` → নতুন object তৈরি হয়েছে।
* `False` → আগে থেকেই ছিল।

---

# 4. `update_or_create()`

থাকলে update করবে, না থাকলে create করবে।

```python
tag, created = Tag.objects.update_or_create(
    name="Python",
    defaults={
        "slug": "python"
    }
)
```

---

# 5. `bulk_create()`

একসাথে অনেক object create করতে।

```python
Tag.objects.bulk_create([
    Tag(name="Django"),
    Tag(name="Python"),
    Tag(name="DRF"),
])
```

---

# 6. `bulk_update()`

একসাথে অনেক object update করতে।

```python
blogs = Blog.objects.all()

for blog in blogs:
    blog.status = "published"

Blog.objects.bulk_update(
    blogs,
    ["status"]
)
```

---

# 7. `exists()`

Object আছে কিনা।

```python
if Blog.objects.filter(id=1).exists():
    print("Found")
```

---

# 8. `first()`

প্রথম object।

```python
blog = Blog.objects.first()
```

---

# 9. `last()`

শেষ object।

```python
blog = Blog.objects.last()
```

---

# 10. `latest()`

সর্বশেষ object।

```python
blog = Blog.objects.latest("created_at")
```

---

# 11. `earliest()`

সবচেয়ে পুরনো object।

```python
blog = Blog.objects.earliest("created_at")
```

---

# 12. `count()`

```python
Blog.objects.count()
```

---

# 13. `create()`

```python
Blog.objects.create(
    title="Django"
)
```

---

# 14. `filter()`

```python
Blog.objects.filter(status="published")
```

---

# 15. `exclude()`

```python
Blog.objects.exclude(status="draft")
```

---

# 16. `values()`

Dictionary return করে।

```python
Blog.objects.values("title", "status")
```

Output:

```python
[
    {"title": "Django", "status": "published"}
]
```

---

# 17. `values_list()`

```python
Blog.objects.values_list("title", flat=True)
```

Output:

```python
[
    "Django",
    "Python"
]
```

---

# 18. `only()`

কিছু field load করবে।

```python
Blog.objects.only("title", "slug")
```

---

# 19. `defer()`

কিছু field বাদ দেবে।

```python
Blog.objects.defer("description")
```

---

# 20. `select_related()`

ForeignKey optimize।

```python
Blog.objects.select_related("category")
```

---

# 21. `prefetch_related()`

ManyToMany optimize।

```python
Blog.objects.prefetch_related("tags")
```

---

# 22. `order_by()`

```python
Blog.objects.order_by("-created_at")
```

---

# 23. `aggregate()`

```python
from django.db.models import Count

Blog.objects.aggregate(
    total=Count("id")
)
```

---

# 24. `annotate()`

```python
from django.db.models import Count

Category.objects.annotate(
    total_blog=Count("blogs")
)
```

---

# 25. `delete()`

```python
Blog.objects.filter(id=1).delete()
```

---

# 26. `update()`

```python
Blog.objects.filter(id=1).update(
    status="published"
)
```

---

## DRF-এ সবচেয়ে বেশি ব্যবহৃত methods

আপনি যেহেতু DRF শিখছেন, এগুলো সবচেয়ে বেশি কাজে লাগবে:

* `get_object_or_404()`
* `get_or_create()`
* `update_or_create()`
* `filter()`
* `get()`
* `create()`
* `update()`
* `exists()`
* `first()`
* `last()`
* `select_related()`
* `prefetch_related()`
* `bulk_create()`
* `bulk_update()`
* `values()`
* `values_list()`
* `count()`
* `annotate()`
* `aggregate()`

এগুলো Django ও DRF project-এ সবচেয়ে বেশি ব্যবহৃত ORM helper/shortcut methods।
এগুলো Django ORM-এর সবচেয়ে গুরুত্বপূর্ণ methods। DRF project-এ প্রায়ই ব্যবহার হয়। এক এক করে সহজ উদাহরণসহ দেখি।

ধরি আপনার Model:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)


class Tag(models.Model):
    name = models.CharField(max_length=100)


class Blog(models.Model):
    title = models.CharField(max_length=200)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    tags = models.ManyToManyField(Tag)
    views = models.PositiveIntegerField(default=0)
```

---

# 1. `select_related()`

**ForeignKey বা OneToOne field-এর জন্য ব্যবহার হয়।**

## Problem (N+1 Query)

```python
blogs = Blog.objects.all()

for blog in blogs:
    print(blog.category.name)
```

ধরুন 10টা blog আছে।

Query হবে:

```
1 query -> Blog
10 query -> Category

Total = 11 queries
```

---

## Solution

```python
blogs = Blog.objects.select_related("category")

for blog in blogs:
    print(blog.category.name)
```

এখন মাত্র

```
1 query
```

SQL JOIN ব্যবহার করে category নিয়ে আসবে।

### কখন ব্যবহার করবেন?

* ForeignKey
* OneToOneField

---

# 2. `prefetch_related()`

**ManyToMany এবং Reverse ForeignKey-এর জন্য।**

ধরি

```python
for blog in Blog.objects.all():
    print(blog.tags.all())
```

১০টা blog হলে

```
1 query -> Blog
10 query -> Tags

Total = 11
```

---

### Solution

```python
blogs = Blog.objects.prefetch_related("tags")

for blog in blogs:
    print(blog.tags.all())
```

এখন

```
1 query -> Blog
1 query -> Tags

Total = 2 queries
```

---

## Difference

| select_related | prefetch_related |
| -------------- | ---------------- |
| ForeignKey     | ManyToMany       |
| SQL JOIN       | Separate Query   |

---

# 3. `bulk_create()`

একসাথে অনেক object create।

### Without

```python
Tag.objects.create(name="Python")
Tag.objects.create(name="Django")
Tag.objects.create(name="DRF")
```

৩টা query।

---

### With

```python
Tag.objects.bulk_create([
    Tag(name="Python"),
    Tag(name="Django"),
    Tag(name="DRF"),
])
```

একটা query।

---

## Use Case

CSV Import

Excel Import

1000 records insert

---

# 4. `bulk_update()`

একসাথে update।

```python
blogs = Blog.objects.all()

for blog in blogs:
    blog.views += 100

Blog.objects.bulk_update(
    blogs,
    ["views"]
)
```

সব blog একসাথে update হবে।

---

# 5. `values()`

Object না দিয়ে Dictionary দেয়।

```python
blogs = Blog.objects.values("id", "title")
```

Output

```python
[
    {
        "id":1,
        "title":"Django"
    },
    {
        "id":2,
        "title":"Python"
    }
]
```

---

### Without values()

```python
blogs = Blog.objects.all()

for blog in blogs:
    print(blog.title)
```

Object return করে।

---

### With values()

```python
blogs = Blog.objects.values("title")
```

Dictionary return করে।

---

# 6. `values_list()`

Tuple বা List return করে।

```python
Blog.objects.values_list("title")
```

Output

```python
[
    ("Django",),
    ("Python",)
]
```

---

### flat=True

```python
Blog.objects.values_list(
    "title",
    flat=True
)
```

Output

```python
[
    "Django",
    "Python"
]
```

---

## Use Case

Dropdown

Choice

IDs List

---

# 7. `count()`

Object সংখ্যা।

```python
Blog.objects.count()
```

Output

```
25
```

---

### Filter সহ

```python
Blog.objects.filter(
    status="published"
).count()
```

Output

```
10
```

---

# 8. `annotate()`

প্রতিটি object-এর সাথে extra calculated field যোগ করে।

ধরি

Category

```
Python

Django
```

Blog

```
Python
Python
Python
Django
```

---

```python
from django.db.models import Count

Category.objects.annotate(
    total_blog=Count("blog")
)
```

Output

```
Python
total_blog = 3

Django
total_blog =1
```

Access

```python
for category in categories:
    print(category.name)
    print(category.total_blog)
```

---

আরেকটি উদাহরণ:

```python
from django.db.models import Avg

Category.objects.annotate(
    avg_views=Avg("blog__views")
)
```

---

# 9. `aggregate()`

সব object-এর উপর summary বের করে।

```python
from django.db.models import Count

Blog.objects.aggregate(
    total_blog=Count("id")
)
```

Output

```python
{
    "total_blog":25
}
```

---

আরও উদাহরণ

```python
from django.db.models import Sum

Blog.objects.aggregate(
    total_views=Sum("views")
)
```

Output

```python
{
    "total_views":3500
}
```

---

Average

```python
from django.db.models import Avg

Blog.objects.aggregate(
    avg_views=Avg("views")
)
```

Output

```python
{
    "avg_views":150
}
```

---

Maximum

```python
from django.db.models import Max

Blog.objects.aggregate(
    max_views=Max("views")
)
```

---

Minimum

```python
from django.db.models import Min

Blog.objects.aggregate(
    min_views=Min("views")
)
```

---

# `annotate()` vs `aggregate()`

ধরি:

Category

```
Python
Django
Java
```

Blog

```
Python -> 5 blogs
Django -> 3 blogs
Java -> 2 blogs
```

### `annotate()`

```python
Category.objects.annotate(
    total_blog=Count("blog")
)
```

Output

```
Python -> 5

Django -> 3

Java -> 2
```

প্রতিটি Category-এর জন্য আলাদা count।

---

### `aggregate()`

```python
Blog.objects.aggregate(
    total=Count("id")
)
```

Output

```
10
```

শুধু একটি summary result।

---

## Interview Shortcut

| Method               | কাজ                                                  |
| -------------------- | ---------------------------------------------------- |
| `select_related()`   | ForeignKey/OneToOne optimize (JOIN)                  |
| `prefetch_related()` | ManyToMany/Reverse FK optimize                       |
| `bulk_create()`      | এক query-তে অনেক object create                       |
| `bulk_update()`      | এক query-তে অনেক object update                       |
| `values()`           | Dictionary return করে                                |
| `values_list()`      | Tuple/List return করে                                |
| `count()`            | Record সংখ্যা                                        |
| `annotate()`         | প্রতিটি object-এর সাথে calculated field যোগ করে      |
| `aggregate()`        | পুরো queryset-এর summary (Count, Sum, Avg, Max, Min) |

এগুলো Django ORM-এর সবচেয়ে বেশি ব্যবহৃত advanced query methods এবং DRF project-এ performance ও reporting API তৈরির সময় খুব কাজে লাগে।
হ্যাঁ, এগুলো সাধারণত **extra business logic**। DRF-এ এ ধরনের কাজ প্রায়ই করতে হয়। নিচে কিছু common example দিলাম এবং কোন method-এ করা ভালো তাও দেখালাম।

| Requirement                      | কোথায় লিখবেন       |
| -------------------------------- | ------------------- |
| Blog view হয়েছে কিনা check      | `retrieve()`        |
| View count বাড়ানো               | `retrieve()`        |
| Blog Like                        | `@action`           |
| Bookmark                         | `@action`           |
| Publish/Unpublish                | `@action`           |
| Approve Comment                  | `@action`           |
| Soft Delete                      | `perform_destroy()` |
| Logged-in user assign            | `perform_create()`  |
| Update-এর সময় `updated_by` save | `perform_update()`  |

---

## Example 1: User আগে view করেছে কি না

```python
def retrieve(self, request, *args, **kwargs):
    blog = self.get_object()

    viewed = False

    if request.user.is_authenticated:
        viewed = BlogView.objects.filter(
            user=request.user,
            blog=blog
        ).exists()

    serializer = self.get_serializer(blog)

    data = serializer.data
    data["viewed"] = viewed

    return Response(data)
```

Response:

```json
{
    "id": 1,
    "title": "DRF Tutorial",
    "viewed": true
}
```

---

## Example 2: View Count

```python
def retrieve(self, request, *args, **kwargs):
    blog = self.get_object()

    blog.views += 1
    blog.save(update_fields=["views"])

    serializer = self.get_serializer(blog)
    return Response(serializer.data)
```

---

## Example 3: Unique View

একজন user একবারই view count বাড়াবে।

```python
def retrieve(self, request, *args, **kwargs):
    blog = self.get_object()

    if request.user.is_authenticated:
        _, created = BlogView.objects.get_or_create(
            user=request.user,
            blog=blog
        )

        if created:
            blog.views += 1
            blog.save(update_fields=["views"])

    serializer = self.get_serializer(blog)
    return Response(serializer.data)
```

---

## Example 4: Like

```python
@action(detail=True, methods=["post"])
def like(self, request, pk=None):

    blog = self.get_object()

    blog.likes_count += 1
    blog.save(update_fields=["likes_count"])

    return Response({
        "likes": blog.likes_count
    })
```

---

## Example 5: Bookmark

```python
@action(detail=True, methods=["post"])
def bookmark(self, request, pk=None):

    blog = self.get_object()

    Bookmark.objects.get_or_create(
        user=request.user,
        blog=blog
    )

    return Response({
        "message": "Bookmarked"
    })
```

---

## Example 6: Comment Count

Comment create হলে:

```python
def perform_create(self, serializer):

    comment = serializer.save(
        user=self.request.user
    )

    comment.blog.comments_count += 1
    comment.blog.save(
        update_fields=["comments_count"]
    )
```

---

## Example 7: Reply Count

Reply create হলে:

```python
if comment.parent:
    comment.parent.replies_count += 1
    comment.parent.save(
        update_fields=["replies_count"]
    )
```

---

## Example 8: Blog Published

```python
@action(detail=True, methods=["post"])
def publish(self, request, pk=None):

    blog = self.get_object()

    blog.status = "published"
    blog.save()

    return Response({
        "message": "Published"
    })
```

---

### একটি সহজ নিয়ম

* **Object দেখানোর সময় কিছু extra করতে হলে** → `retrieve()`
* **Create/Update/Delete-এর সময় extra logic** → `perform_create()`, `perform_update()`, `perform_destroy()`
* **CRUD-এর বাইরে নতুন operation (like, bookmark, publish, approve, restore)** → `@action`

আপনার Blog API-তে **view, like, bookmark, comment, reply, publish**—এসবই এই category-তে পড়ে এবং এগুলো DRF project-এ খুবই common business logic।
এটা বুঝার জন্য একটা সহজ rule আছে:

**Serializer নির্ধারণ করবেন আপনি কোন model-এর data নিয়ে কাজ করছেন এবং কোন কাজ করছেন তার উপর।**

Serializer হলো **একটা model-এর input/output controller**।

---

## 1. User create করলে → UserSerializer

Request:

```
POST /users/
```

Data:

```json
{
    "username": "rahim",
    "email": "a@gmail.com",
    "password": "123456"
}
```

তখন:

```python
UserSerializer
```

কারণ আপনি User object তৈরি করছেন।

```python
class UserSerializer(ModelSerializer):

    def create(self, validated_data):
        return User.objects.create_user(
            **validated_data
        )
```

---

## 2. Blog create করলে → BlogSerializer

Request:

```
POST /blogs/
```

Data:

```json
{
    "title": "Django DRF",
    "category": 1,
    "tags": [1,2]
}
```

তখন:

```python
BlogSerializer
```

কারণ আপনি Blog object তৈরি করছেন।

```python
class BlogSerializer(ModelSerializer):

    def create(self, validated_data):
        ...
```

---

## 3. Comment create করলে → CommentSerializer

Request:

```
POST /comments/
```

Data:

```json
{
    "blog":1,
    "comment":"Nice"
}
```

তখন:

```python
CommentSerializer
```

কারণ আপনি Comment table-এ data insert করছেন।

---

## 4. Bookmark create করলে → BookmarkSerializer

Request:

```
POST /bookmark/
```

Data:

```json
{
    "blog":5
}
```

তখন:

```python
BookmarkSerializer
```

কারণ আপনি Bookmark model-এর object তৈরি করছেন।

---

# কিন্তু ViewSet-এ কোন serializer কখন call হবে?

সাধারণত:

```python
class BlogViewSet(ModelViewSet):

    serializer_class = BlogSerializer
```

এখানে সব action-এ BlogSerializer ব্যবহার হবে।

যেমন:

### List

```
GET /blogs/
```

হবে:

```python
BlogSerializer(
    blogs,
    many=True
)
```

### Retrieve

```
GET /blogs/1/
```

হবে:

```python
BlogSerializer(blog)
```

### Create

```
POST /blogs/
```

হবে:

```python
BlogSerializer(data=request.data)
```

### Update

```
PUT /blogs/1/
```

হবে:

```python
BlogSerializer(
    instance=blog,
    data=request.data
)
```

---

# কখন আলাদা serializer লাগবে?

ধরুন Blog list-এ আপনি শুধু ছোট data দেখাবেন।

List response:

```json
{
    "id":1,
    "title":"DRF"
}
```

কিন্তু detail page:

```json
{
    "id":1,
    "title":"DRF",
    "description":"....",
    "comments":[]
}
```

তখন:

```python
BlogListSerializer
```

এবং

```python
BlogDetailSerializer
```

করবেন।

View:

```python
def get_serializer_class(self):

    if self.action == "list":
        return BlogListSerializer

    if self.action == "retrieve":
        return BlogDetailSerializer

    return BlogSerializer
```

---

# Nested data হলে?

ধরুন Blog response:

```json
{
 "title":"DRF",
 "category":{
    "id":1,
    "name":"Programming"
 }
}
```

এখানে CategorySerializer লাগবে:

```python
class BlogSerializer(ModelSerializer):

    category = CategorySerializer()

    class Meta:
        model = Blog
```

কারণ Blog-এর ভিতরে Category data দেখাচ্ছেন।

---

# সবচেয়ে সহজ চিন্তার নিয়ম

নিজেকে প্রশ্ন করুন:

### ১. আমি কোন table-এ save করছি?

| Table    | Serializer         |
| -------- | ------------------ |
| User     | UserSerializer     |
| Blog     | BlogSerializer     |
| Comment  | CommentSerializer  |
| Bookmark | BookmarkSerializer |

### ২. আমি কি শুধু দেখাচ্ছি নাকি create/update করছি?

শুধু দেখানো:

```python
Read Serializer
```

Create/update:

```python
Write Serializer
```

---

### ৩. আমার response কি বড়/ছোট হবে?

ছোট response:

```
BlogListSerializer
```

বিস্তারিত:

```
BlogDetailSerializer
```

---

আপনার Blog project-এর জন্য সাধারণত structure এমন হবে:

```
users/
    serializers.py
        UserSerializer

blogs/
    serializers.py
        BlogSerializer
        BlogListSerializer
        BlogDetailSerializer
        CategorySerializer
        TagSerializer

comments/
    serializers.py
        CommentSerializer

bookmark/
    serializers.py
        BookmarkSerializer
```

একটা model = সাধারণত একটা main serializer।
আর বিভিন্ন view requirement অনুযায়ী extra serializer তৈরি হয়।


-----
Custom action-এ **কোন serializer হবে সেটা action-এর কাজের উপর নির্ভর করে**। সব custom action-এ একই serializer ব্যবহার করতে হবে এমন না।

মূল rule:

> **Action-এ কোন model-এর data input/output হচ্ছে, সেই অনুযায়ী serializer নির্বাচন করবেন।**

---

## Case 1: শুধু status change (serializer লাগবে না)

যেমন Blog publish করা:

```python
@action(detail=True, methods=['post'])
def publish(self, request, pk=None):

    blog = self.get_object()

    blog.status = "published"
    blog.save()

    return Response({
        "message": "Blog published"
    })
```

এখানে:

* কোনো নতুন data নিচ্ছেন না
* কোনো object return করছেন না

তাই serializer দরকার নেই।

---

## Case 2: Object return করলে → ViewSet-এর default serializer

Example:

```python
@action(detail=True, methods=['post'])
def restore(self, request, pk=None):

    blog = self.get_object()

    blog.restore()

    serializer = self.get_serializer(blog)

    return Response(serializer.data)
```

এখানে:

```python
self.get_serializer()
```

মানে আপনার ViewSet-এর:

```python
serializer_class = BlogSerializer
```

ব্যবহার হবে।

---

## Case 3: Custom input নিলে → আলাদা serializer

ধরুন Blog-এ rating দিতে চান:

Request:

```json
{
    "rating": 5,
    "comment": "Good blog"
}
```

এটা Blog model-এর field না।

তাই:

```python
class RatingSerializer(serializers.Serializer):

    rating = serializers.IntegerField()
    comment = serializers.CharField()
```

Action:

```python
@action(detail=True, methods=['post'])
def rating(self, request, pk=None):

    serializer = RatingSerializer(
        data=request.data
    )

    serializer.is_valid(raise_exception=True)

    blog = self.get_object()

    # save rating logic

    return Response(serializer.data)
```

---

## Case 4: Bookmark action

ধরি:

```python
class Bookmark(models.Model):
    user = models.ForeignKey(User)
    blog = models.ForeignKey(Blog)
```

Action:

```python
@action(detail=True, methods=['post'])
def bookmark(self, request, pk=None):

    blog = self.get_object()

    Bookmark.objects.get_or_create(
        user=request.user,
        blog=blog
    )

    return Response({
        "message":"Bookmarked"
    })
```

এখানে serializer লাগছে না।

কারণ আপনি শুধু create করছেন এবং message দিচ্ছেন।

---

কিন্তু যদি bookmark object return করেন:

```python
@action(detail=True, methods=['post'])
def bookmark(self, request, pk=None):

    bookmark = Bookmark.objects.create(
        user=request.user,
        blog=self.get_object()
    )

    serializer = BookmarkSerializer(bookmark)

    return Response(serializer.data)
```

তখন:

```python
BookmarkSerializer
```

ব্যবহার হবে।

---

## Case 5: Action-এ আলাদা serializer নির্ধারণ

অনেক বড় project-এ এটা করা হয়:

```python
class BlogViewSet(ModelViewSet):

    serializer_class = BlogSerializer


    def get_serializer_class(self):

        if self.action == "like":
            return LikeSerializer

        if self.action == "bookmark":
            return BookmarkSerializer

        return BlogSerializer
```

---

## মনে রাখার shortcut

### Action শুধু কাজ করে:

```
publish
restore
delete
like count increase
bookmark toggle
approve
```

➡️ সাধারণত serializer লাগে না।

---

### Action data নেয়:

```
rating
change_password
add_tags
filter_custom
```

➡️ আলাদা serializer লাগে।

---

### Action object return করে:

```
create bookmark
create history
create reaction
```

➡️ ওই model-এর serializer লাগে।

---

আপনার Blog project-এ:

| Action      | Serializer                         |
| ----------- | ---------------------------------- |
| restore     | লাগবে না                           |
| hard_delete | লাগবে না                           |
| publish     | লাগবে না                           |
| like        | লাগবে না / LikeSerializer          |
| bookmark    | লাগবে না / BookmarkSerializer      |
| add_tags    | TagSerializer বা custom serializer |
| add_comment | CommentSerializer                  |
| rating      | RatingSerializer                   |

অর্থাৎ **custom action দেখেই serializer ঠিক করবেন না; action-এর ভিতরে কী data flow হচ্ছে সেটা দেখে ঠিক করবেন।**


------
