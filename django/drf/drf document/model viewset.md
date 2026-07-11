`ViewSet` হলো Django REST Framework (DRF)-এর সবচেয়ে গুরুত্বপূর্ণ concepts-এর একটি। আপনি যেহেতু Django REST Framework ভালোভাবে শিখতে চান এবং বড় project (SaaS, E-commerce, Exam System) বানাতে চান, তাই এগুলো **গভীরভাবে** বোঝা খুবই গুরুত্বপূর্ণ।

---

# DRF ViewSet Family Overview

```
APIView
   │
   ├──────────────► ViewSet
   │                    │
   │                    ├────────► GenericViewSet
   │                    │               │
   │                    │               ├────────► ReadOnlyModelViewSet
   │                    │               │
   │                    │               └────────► ModelViewSet
   │                    │
   │                    └────────► ViewSetMixin
```

---

# 1. ViewSet

সবচেয়ে basic ViewSet।

এখানে Django automatic `GET`, `POST`, `PUT` map করে না।

আপনাকে নিজের method লিখতে হবে।

Example

```python
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response

class StudentViewSet(ViewSet):

    def list(self, request):
        return Response({"message": "All Students"})

    def retrieve(self, request, pk=None):
        return Response({"message": f"Student {pk}"})

    def create(self, request):
        return Response({"message": "Created"})

    def update(self, request, pk=None):
        return Response({"message": f"Updated {pk}"})

    def partial_update(self, request, pk=None):
        return Response({"message": "Patch"})

    def destroy(self, request, pk=None):
        return Response({"message": "Deleted"})
```

Router

```python
router.register("students", StudentViewSet)
```

Automatically

```
GET     /students/
GET     /students/1/

POST    /students/

PUT     /students/1/

PATCH   /students/1/

DELETE  /students/1/
```

---

## কখন ব্যবহার করবেন?

যখন পুরো logic নিজে লিখতে চান।

যেমন

* API Gateway
* Custom Authentication
* Payment API
* External API

---

# 2. GenericViewSet

এটি ViewSet + GenericAPIView

এখানে

* queryset
* serializer
* pagination
* filtering
* lookup_field

সব use করা যায়।

কিন্তু CRUD automatic আসে না।

নিজে mixin add করতে হয়।

Example

```python
from rest_framework import mixins
from rest_framework.viewsets import GenericViewSet

class StudentViewSet(
    mixins.ListModelMixin,
    mixins.CreateModelMixin,
    GenericViewSet
):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer
```

এখন

```
GET /students/
POST /students/
```

শুধু এই দুইটা থাকবে।

---

## যদি Retrieve চান

```python
class StudentViewSet(
    mixins.ListModelMixin,
    mixins.CreateModelMixin,
    mixins.RetrieveModelMixin,
    GenericViewSet
):
```

---

## যদি Update চান

```python
mixins.UpdateModelMixin
```

---

## যদি Delete চান

```python
mixins.DestroyModelMixin
```

---

## GenericViewSet = Lego Block

```
List
Create
Retrieve
Update
Delete

↓

যেটা দরকার
সেটা লাগাও
```

---

# 3. ModelViewSet

সবচেয়ে বেশি ব্যবহৃত।

CRUD সব ready।

Example

```python
from rest_framework.viewsets import ModelViewSet

class StudentViewSet(ModelViewSet):

    queryset = Student.objects.all()

    serializer_class = StudentSerializer
```

Automatically

```
GET

POST

PUT

PATCH

DELETE
```

সব ready.

---

## Internal Mixins

ModelViewSet আসলে

```python
class ModelViewSet(

    CreateModelMixin,

    RetrieveModelMixin,

    UpdateModelMixin,

    DestroyModelMixin,

    ListModelMixin,

    GenericViewSet
)
```

অর্থাৎ

```
GenericViewSet

+

5 Mixins
```

---

# কোন Method Call হয়?

GET /students/

↓

```
list()
```

GET /students/5/

↓

```
retrieve()
```

POST

↓

```
create()
```

PUT

↓

```
update()
```

PATCH

↓

```
partial_update()
```

DELETE

↓

```
destroy()
```

---

## সবচেয়ে Common Override

### get_queryset()

```python
def get_queryset(self):

    return Student.objects.filter(active=True)
```

---

### get_serializer_class()

```python
def get_serializer_class(self):

    if self.action == "list":
        return StudentListSerializer

    return StudentDetailSerializer
```

এটি বড় project-এ খুবই common। 

---

### perform_create()

```python
def perform_create(self, serializer):

    serializer.save(user=self.request.user)
```

---

### perform_update()

```python
def perform_update(self, serializer):

    serializer.save(updated_by=self.request.user)
```

---

### perform_destroy()

```python
def perform_destroy(self, instance):

    instance.delete()
```

---

# 4. ReadOnlyModelViewSet

শুধু Read API

মানে

```
GET

GET Detail
```

POST নেই

DELETE নেই

PUT নেই

PATCH নেই

Example

```python
from rest_framework.viewsets import ReadOnlyModelViewSet

class ProductViewSet(ReadOnlyModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer
```

Automatically

```
GET /products/

GET /products/1/
```

---

## কোথায় ব্যবহার হয়?

Product Catalog

Blog

News

Public APIs

Course List

Exam List

Student Result View

---

# 5. ViewSetMixin

এটি সাধারণত সরাসরি ব্যবহার করা হয় না।

এটি DRF-এর internal class।

এটি

```
action

basename

router

mapping
```

manage করে।

যেমন

```
GET

↓

list()

POST

↓

create()

DELETE

↓

destroy()
```

এই mapping `ViewSetMixin` করে।

---

# Comparison Table

| Feature        | ViewSet | GenericViewSet | ModelViewSet | ReadOnlyModelViewSet |
| -------------- | ------- | -------------- | ------------ | -------------------- |
| queryset       | ❌       | ✅              | ✅            | ✅                    |
| serializer     | ❌       | ✅              | ✅            | ✅                    |
| CRUD Auto      | ❌       | Mixins দিয়ে    | ✅            | Read Only            |
| Pagination     | ❌       | ✅              | ✅            | ✅                    |
| Filtering      | ❌       | ✅              | ✅            | ✅                    |
| Search         | ❌       | ✅              | ✅            | ✅                    |
| Permissions    | Manual  | ✅              | ✅            | ✅                    |
| Authentication | Manual  | ✅              | ✅            | ✅                    |

---

# কোন Project-এ কোনটি ব্যবহার করবেন?

### 1. Custom API

```
ViewSet
```

Example

```
Payment API

OTP API

Firebase Login

SMS API
```

---

### 2. কিছু CRUD দরকার

```
GenericViewSet
```

Example

```
Admin

Teacher Panel

Dashboard

Only List + Create
```

---

### 3. Full CRUD

```
ModelViewSet
```

Example

```
Product

Category

Course

Student

Teacher

Enrollment

Review

Order
```

---

### 4. Public API

```
ReadOnlyModelViewSet
```

Example

```
Courses

Products

Blogs

News

Public Exam
```

---

# বাস্তব E-commerce উদাহরণ

| Model               | Recommended ViewSet  |
| ------------------- | -------------------- |
| Category            | ModelViewSet         |
| Product             | ModelViewSet         |
| Order               | ModelViewSet         |
| Review              | ModelViewSet         |
| Cart                | ModelViewSet         |
| Public Product List | ReadOnlyModelViewSet |
| Payment             | ViewSet              |
| Stripe Webhook      | ViewSet              |
| Analytics Dashboard | GenericViewSet       |

---

# শেখার ক্রম (Recommended Learning Order)

1. ✅ `ViewSet` – method mapping (`list`, `create`, `retrieve`, `update`, `partial_update`, `destroy`)
2. ✅ `GenericViewSet` – Mixins (`ListModelMixin`, `CreateModelMixin`, `RetrieveModelMixin`, `UpdateModelMixin`, `DestroyModelMixin`)
3. ✅ `ModelViewSet` – `get_queryset()`, `get_serializer_class()`, `perform_create()`, `perform_update()`, `perform_destroy()`
4. ✅ `ReadOnlyModelViewSet` – Public read-only APIs
5. ✅ Advanced topics – `@action`, custom routes, dynamic serializers, custom permissions per action, filtering, pagination, throttling

এই roadmap অনুসরণ করলে আপনি বড় DRF project-এর প্রায় সব ধরনের ViewSet confidently ব্যবহার করতে পারবেন।
খুব ভালো প্রশ্ন। `ViewSet`-এর প্রতিটি method আসলে একটি HTTP request handle করে। তবে মনে রাখবেন:

> **ViewSet শুধুমাত্র method mapping দেয়। Database CRUD, serializer validation, queryset management—কোনোটাই নিজে করে না। সব আপনাকেই লিখতে হবে।**

---

# Example Model

ধরি আমাদের একটি Student model আছে।

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
    email = models.EmailField()

    def __str__(self):
        return self.name
```

Serializer

```python
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"
```

---

# 1. list()

## URL

```
GET /students/
```

Purpose

> সমস্ত Student দেখানোর জন্য।

---

## Flow

```
Client

↓

GET /students/

↓

list()

↓

Database

↓

Serializer

↓

JSON Response
```

---

## Example

```python
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response
from .models import Student
from .serializers import StudentSerializer

class StudentViewSet(ViewSet):

    def list(self, request):

        students = Student.objects.all()

        serializer = StudentSerializer(students, many=True)

        return Response(serializer.data)
```

---

## Response

```json
[
    {
        "id":1,
        "name":"Rahim",
        "age":20
    },
    {
        "id":2,
        "name":"Karim",
        "age":22
    }
]
```

---

## এখানে কী কী করতে পারবেন?

✅ Database query

```python
Student.objects.all()
```

✅ Filter

```python
Student.objects.filter(age=20)
```

✅ Search

```python
Student.objects.filter(name__icontains="rah")
```

✅ Ordering

```python
Student.objects.order_by("-id")
```

✅ Pagination (নিজে implement করতে হবে)

✅ Permission check

```python
if not request.user.is_staff:
```

✅ Custom Response

```python
return Response({

    "count":10,

    "students":serializer.data
})
```

---

## কী পারবেন না?

❌ Automatic Pagination

❌ Automatic Filtering

❌ Automatic Search

❌ Automatic Ordering

❌ Automatic Serializer Selection

সব নিজে লিখতে হবে।

---

# 2. retrieve()

## URL

```
GET /students/5/
```

Purpose

একজন Student দেখানো।

---

## Flow

```
GET /students/5/

↓

retrieve()

↓

pk=5

↓

Database

↓

Serializer

↓

Response
```

---

## Example

```python
from django.shortcuts import get_object_or_404

def retrieve(self, request, pk=None):

    student = get_object_or_404(Student, pk=pk)

    serializer = StudentSerializer(student)

    return Response(serializer.data)
```

---

## Response

```json
{
    "id":5,
    "name":"Rahim",
    "age":20
}
```

---

## এখানে কী করতে পারবেন?

✅ pk দিয়ে object বের করা

```python
Student.objects.get(pk=pk)
```

✅ Permission Check

```python
if student.user != request.user:
```

✅ Related data দেখানো

```python
StudentSerializer(student)
```

---

## পারবেন না

❌ Object automatic পাওয়া

❌ 404 automatic

সব নিজে লিখবেন।

---

# 3. create()

## URL

```
POST /students/
```

Purpose

নতুন Student তৈরি করা।

---

## Request

```json
{
    "name":"Rahim",
    "age":20,
    "email":"rahim@gmail.com"
}
```

---

## Flow

```
POST

↓

request.data

↓

Serializer

↓

Validation

↓

Save

↓

Response
```

---

## Example

```python
def create(self, request):

    serializer = StudentSerializer(data=request.data)

    if serializer.is_valid():

        serializer.save()

        return Response(serializer.data)

    return Response(serializer.errors)
```

---

## এখানে কী পারবেন?

✅ request.data পড়তে

```python
request.data
```

✅ Validation

```python
serializer.is_valid()
```

✅ Save

```python
serializer.save()
```

✅ Email Send

✅ OTP Generate

✅ Notification

✅ Log

---

## পারবেন না

❌ Automatic Validation

❌ Automatic Save

সব manually লিখবেন।

---

# 4. update()

## URL

```
PUT /students/3/
```

Purpose

পুরো Object Update করা।

---

## Request

```json
{
    "name":"Hasan",
    "age":25,
    "email":"hasan@gmail.com"
}
```

---

## Example

```python
def update(self, request, pk=None):

    student = get_object_or_404(Student, pk=pk)

    serializer = StudentSerializer(student, data=request.data)

    if serializer.is_valid():

        serializer.save()

        return Response(serializer.data)

    return Response(serializer.errors)
```

---

## এখানে পারবেন

✅ Full Update

✅ Validation

✅ Business Logic

```python
if student.is_active:
```

---

## পারবেন না

❌ Partial Update

PUT-এ সব field পাঠানো উচিত।

---

# 5. partial_update()

## URL

```
PATCH /students/3/
```

Purpose

শুধু কিছু field Update করা।

---

## Request

```json
{
    "age":30
}
```

---

## Example

```python
def partial_update(self, request, pk=None):

    student = get_object_or_404(Student, pk=pk)

    serializer = StudentSerializer(
        student,
        data=request.data,
        partial=True
    )

    if serializer.is_valid():

        serializer.save()

        return Response(serializer.data)

    return Response(serializer.errors)
```

---

## Difference

PUT

```json
{
"name":"",
"age":20,
"email":""
}
```

PATCH

```json
{
"age":22
}
```

---

## এখানে পারবেন

✅ Single Field Update

✅ Multiple Field Update

✅ Validation

---

## পারবেন না

❌ Full Replace

---

# 6. destroy()

## URL

```
DELETE /students/5/
```

Purpose

Object Delete করা।

---

## Example

```python
def destroy(self, request, pk=None):

    student = get_object_or_404(Student, pk=pk)

    student.delete()

    return Response({
        "message":"Deleted Successfully"
    })
```

---

## এখানে পারবেন

✅ Delete

✅ Soft Delete

```python
student.is_deleted=True
student.save()
```

✅ Permission Check

```python
if request.user != student.user:
```

✅ Delete Log

---

## পারবেন না

❌ Automatic Delete

---

# `request`-এ কী কী থাকে?

প্রতিটি method-এ `request` object থেকে অনেক তথ্য পাওয়া যায়:

```python
request.data          # POST/PUT/PATCH body
request.user          # Logged-in user
request.auth          # Authentication info
request.query_params  # URL query (?page=1&search=abc)
request.headers       # HTTP headers
request.method        # GET, POST, PUT...
request.FILES         # Uploaded files
```

উদাহরণ:

```python
def list(self, request):
    search = request.query_params.get("search")

    if search:
        students = Student.objects.filter(name__icontains=search)
    else:
        students = Student.objects.all()

    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

---

# Summary Table

| Method             | HTTP Method | URL            | Main Purpose           | সাধারণত কী করবেন                                |
| ------------------ | ----------- | -------------- | ---------------------- | ----------------------------------------------- |
| `list()`           | GET         | `/students/`   | সব object দেখানো       | Filter, Search, Pagination, Serialize           |
| `retrieve()`       | GET         | `/students/1/` | একটি object দেখানো     | `get_object_or_404()`, Permission, Serialize    |
| `create()`         | POST        | `/students/`   | নতুন object তৈরি       | `request.data`, Validation, `serializer.save()` |
| `update()`         | PUT         | `/students/1/` | সম্পূর্ণ object update | Full validation, Save                           |
| `partial_update()` | PATCH       | `/students/1/` | আংশিক update           | `partial=True`, Save                            |
| `destroy()`        | DELETE      | `/students/1/` | object delete          | Delete, Soft delete, Permission                 |

## বাস্তব প্রজেক্টে (E-commerce/Exam SaaS)

* `list()` → Product List, Course List, Exam List
* `retrieve()` → Product Details, Course Details
* `create()` → Register, Order Create, Review Add
* `update()` → Profile Update, Product Edit
* `partial_update()` → Status Change (`is_active`, `is_published`, `completed`)
* `destroy()` → Review Delete, Cart Item Remove, Category Delete

**পরবর্তী ধাপে** আমি `request`, `args`, `kwargs`, `self.action`, `pk`, `lookup_field`, `router`—এগুলো কীভাবে ViewSet-এর ভিতরে কাজ করে, request lifecycle সহ diagram দিয়ে ব্যাখ্যা করতে পারি। এটি ViewSet বোঝার সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।
এটি ViewSet-এর **সবচেয়ে গুরুত্বপূর্ণ অধ্যায়**। একবার এগুলো বুঝে গেলে `ModelViewSet`, `GenericViewSet`, `@action`, `Router`, Nested Router—সব অনেক সহজ লাগবে।

---

# DRF ViewSet Request Lifecycle

একটি request যখন আসে তখন DRF-এর ভিতরে কী ঘটে?

```text
Client (Browser/Postman)
        │
        │
        ▼
URL Request

GET /students/5/

        │
        ▼
urls.py

router.register("students", StudentViewSet)

        │
        ▼
Router

        │
        ▼
StudentViewSet.as_view()

        │
        ▼
ViewSetMixin

GET + Detail

↓

retrieve()

        │
        ▼
request object তৈরি

pk = 5

kwargs = {"pk":5}

action = "retrieve"

        │
        ▼
Your retrieve()

        │
        ▼
Response(JSON)
```

---

# Router কী?

ধরি

```python
from rest_framework.routers import DefaultRouter

router = DefaultRouter()

router.register("students", StudentViewSet)
```

আপনি একটাও URL লেখেননি।

কিন্তু DRF automatically তৈরি করে

```text
GET     /students/
POST    /students/

GET     /students/1/
PUT     /students/1/
PATCH   /students/1/
DELETE  /students/1/
```

---

## Router ভিতরে কী করে?

ধরুন

```text
GET /students/
```

Router দেখে

```text
GET

↓

list()
```

যদি

```text
GET /students/10/
```

তাহলে

```text
retrieve(pk=10)
```

যদি

```text
POST /students/
```

তাহলে

```text
create()
```

যদি

```text
DELETE /students/10/
```

তাহলে

```text
destroy(pk=10)
```

Router শুধু URL → Method Mapping করে।

---

# request Object

সব method-এর প্রথম parameter

```python
def list(self, request):
```

এই request-এর মধ্যে client-এর সব information থাকে।

Example

```python
def list(self, request):

    print(request.method)

    print(request.user)

    print(request.headers)

    print(request.query_params)

    print(request.data)
```

---

## request.method

```python
request.method
```

Output

```text
GET
```

অথবা

```text
POST
```

---

## request.user

Logged in user

```python
print(request.user)
```

Output

```text
Atiar
```

Anonymous হলে

```text
AnonymousUser
```

---

## request.data

POST Body

```json
{
    "name":"Rahim",
    "age":20
}
```

Python

```python
print(request.data)
```

Output

```python
{
'name':'Rahim',
'age':20
}
```

---

## request.query_params

ধরি

```text
GET

/students/?age=20
```

Python

```python
print(request.query_params)
```

Output

```python
<QueryDict: {'age':['20']}>
```

Value

```python
age = request.query_params.get("age")
```

Output

```python
20
```

---

## request.headers

```python
print(request.headers)
```

Output

```text
Authorization

Content-Type

Accept

Host
```

JWT Token

```python
token = request.headers.get("Authorization")
```

---

# pk কী?

ধরি

```text
GET

/students/8/
```

Router automatically

```python
retrieve(request, pk=8)
```

call করে।

Method

```python
def retrieve(self, request, pk=None):

    print(pk)
```

Output

```text
8
```

Database

```python
student = Student.objects.get(pk=pk)
```

---

## update()

```text
PUT

/students/12/
```

Method

```python
def update(self, request, pk=None):

    print(pk)
```

Output

```text
12
```

---

## destroy()

```text
DELETE

/students/25/
```

Output

```text
25
```

---

# kwargs

kwargs হচ্ছে URL-এর dynamic parameters-এর dictionary।

Example

```text
/students/10/
```

Inside View

```python
def retrieve(self, request, *args, **kwargs):

    print(kwargs)
```

Output

```python
{
'pk':'10'
}
```

অর্থাৎ

```python
kwargs["pk"]
```

Output

```text
10
```

এজন্য

```python
pk = kwargs.get("pk")
```

লিখলেও কাজ করবে।

---

## Multiple URL Parameters

ধরি

```text
/courses/5/students/20/
```

kwargs

```python
{
'course_id':5,

'student_id':20
}
```

---

# args

args সাধারণত খুব কম ব্যবহার হয়।

Example

```python
def retrieve(self, request, *args, **kwargs):

    print(args)

    print(kwargs)
```

Output

```python
()

{'pk':5}
```

সাধারণ ViewSet-এ `args` প্রায় সবসময় empty tuple (`()`) থাকে।

---

# self.action

এটি ViewSet-এর সবচেয়ে powerful feature।

Method

```python
def get_serializer_class(self):

    print(self.action)
```

---

যদি

```text
GET /students/
```

Output

```text
list
```

---

যদি

```text
GET /students/5/
```

Output

```text
retrieve
```

---

যদি

```text
POST /students/
```

Output

```text
create
```

---

যদি

```text
PUT /students/5/
```

Output

```text
update
```

---

যদি

```text
PATCH /students/5/
```

Output

```text
partial_update
```

---

যদি

```text
DELETE /students/5/
```

Output

```text
destroy
```

---

## self.action কোথায় সবচেয়ে বেশি ব্যবহার হয়?

### Different Serializer

```python
def get_serializer_class(self):

    if self.action == "list":

        return StudentListSerializer

    elif self.action == "retrieve":

        return StudentDetailSerializer

    return StudentSerializer
```

এটি production project-এ খুবই common pattern। 

---

## Different Permission

```python
def get_permissions(self):

    if self.action == "create":

        return [AllowAny()]

    return [IsAuthenticated()]
```

---

# lookup_field

Default

```python
pk
```

মানে

```text
/students/5/
```

Database

```python
Student.objects.get(pk=5)
```

---

কিন্তু আপনি চাইলে pk-এর বদলে slug বা uuid ব্যবহার করতে পারেন।

Model

```python
class Student(models.Model):

    uuid = models.UUIDField(unique=True)

    name = models.CharField(max_length=100)
```

ViewSet

```python
class StudentViewSet(ModelViewSet):

    queryset = Student.objects.all()

    serializer_class = StudentSerializer

    lookup_field = "uuid"
```

URL

```text
/students/4fd4d4-4454-55aa/
```

এখন DRF করবে

```python
Student.objects.get(uuid=value)
```

---

আরেকটি Example

```python
lookup_field = "email"
```

URL

```text
/students/rahim@gmail.com/
```

Database

```python
Student.objects.get(email="rahim@gmail.com")
```

---

# Complete Flow Example

```text
Client

↓

GET

/students/25/?age=20

↓

Router

↓

retrieve()

↓

request.method

↓

GET

↓

request.query_params

↓

{"age":20}

↓

kwargs

↓

{"pk":25}

↓

pk

↓

25

↓

self.action

↓

retrieve

↓

Database Query

↓

Serializer

↓

JSON Response
```

# Quick Reference Table

| Item                   | কী?                               | উদাহরণ                                                 |
| ---------------------- | --------------------------------- | ------------------------------------------------------ |
| `request`              | Client থেকে আসা পুরো HTTP request | `request.data`, `request.user`, `request.query_params` |
| `request.data`         | POST/PUT/PATCH body               | `{"name": "Rahim"}`                                    |
| `request.query_params` | URL query string                  | `/students/?age=20`                                    |
| `args`                 | Positional arguments              | সাধারণত `()`                                           |
| `kwargs`               | URL-এর named parameters           | `{"pk": 5}`                                            |
| `pk`                   | বর্তমান object's primary key      | `5`                                                    |
| `self.action`          | কোন ViewSet action চলছে           | `"list"`, `"create"`, `"retrieve"`                     |
| `lookup_field`         | কোন field দিয়ে object খুঁজবে     | `"pk"` (default), `"uuid"`, `"slug"`                   |
| `Router`               | URL → ViewSet method mapping      | `GET /students/` → `list()`                            |

## এরপর কী শিখবেন?

এখন আপনার জন্য সবচেয়ে যৌক্তিক পরবর্তী বিষয় হলো:

1. **`ModelViewSet` Internals** (`get_queryset()`, `get_serializer_class()`, `perform_create()`, `perform_update()`, `perform_destroy()`)
2. **Mixins** (`ListModelMixin`, `CreateModelMixin` ইত্যাদি)
3. **Custom Actions (`@action`)** — যেমন `/students/{id}/activate/`, `/students/{id}/reset-password/`
4. **Dynamic Serializer + Dynamic Permissions** (production-level pattern)

এই চারটি শিখে ফেললে আপনি বাস্তব DRF backend-এর প্রায় ৮০–৯০% ViewSet pattern বুঝে যাবেন।
এটাই **ModelViewSet-এর heart**। একজন Professional Django REST Framework Developer-এর সবচেয়ে বেশি ব্যবহার করা methods এগুলোই।

---

# ModelViewSet Internal Workflow

ধরুন আমাদের ModelViewSet:

```python
class StudentViewSet(ModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer
```

আপনি যখন API call করেন, DRF ভিতরে এই flow follow করে।

```text
Client
   │
   ▼
Router
   │
   ▼
ModelViewSet
   │
   ├── get_queryset()
   │
   ├── get_object()
   │
   ├── get_serializer_class()
   │
   ├── get_serializer()
   │
   ├── Validation
   │
   ├── perform_create()
   │
   ├── perform_update()
   │
   ├── perform_destroy()
   │
   ▼
Response(JSON)
```

---

# 1. get_queryset()

## কাজ কী?

Database থেকে কোন data আসবে সেটা নির্ধারণ করে।

Default

```python
queryset = Student.objects.all()
```

DRF internally

```python
def get_queryset(self):
    return self.queryset
```

---

## কখন Override করবেন?

### Example 1

শুধু Active Student

```python
class StudentViewSet(ModelViewSet):

    serializer_class = StudentSerializer

    def get_queryset(self):
        return Student.objects.filter(is_active=True)
```

---

### Example 2

Logged-in User-এর Student

```python
def get_queryset(self):

    return Student.objects.filter(user=self.request.user)
```

---

### Example 3

Search

```
GET

/students/?name=rahim
```

```python
def get_queryset(self):

    queryset = Student.objects.all()

    name = self.request.query_params.get("name")

    if name:
        queryset = queryset.filter(name__icontains=name)

    return queryset
```

---

### Example 4

Different Query for Different Action

```python
def get_queryset(self):

    if self.action == "list":

        return Student.objects.only("id", "name")

    return Student.objects.all()
```

Professional Project-এ খুব common।

---

# Flow

```text
GET /students/

↓

get_queryset()

↓

Student.objects.filter(...)

↓

Serializer

↓

JSON
```

---

# 2. get_serializer_class()

## কাজ কী?

কোন Serializer ব্যবহার হবে সেটা decide করে।

Default

```python
serializer_class = StudentSerializer
```

DRF internally

```python
def get_serializer_class(self):

    return self.serializer_class
```

---

## কেন Override করবো?

কারণ সব API-তে একই serializer দরকার হয় না।

---

### Example

List API

```json
{
"id":1,
"name":"Rahim"
}
```

Detail API

```json
{
"id":1,
"name":"Rahim",
"email":"abc@gmail.com",
"phone":"018888888",
"address":"Dhaka"
}
```

---

### Serializer

```python
class StudentListSerializer(...):
```

```python
class StudentDetailSerializer(...):
```

View

```python
def get_serializer_class(self):

    if self.action == "list":

        return StudentListSerializer

    return StudentDetailSerializer
```

---

### Create API

```python
class StudentCreateSerializer(...)
```

```python
def get_serializer_class(self):

    if self.action == "create":

        return StudentCreateSerializer

    return StudentSerializer
```

---

Professional project-এ এই method সবচেয়ে বেশি override করা হয়। 

---

# Flow

```text
POST

↓

get_serializer_class()

↓

StudentCreateSerializer

↓

Validation

↓

Save
```

---

# 3. perform_create()

## কখন Call হয়?

শুধু

```
POST
```

অর্থাৎ

```
create()
```

এর ভিতরে।

---

DRF internally

```python
serializer.is_valid()

↓

perform_create(serializer)

↓

serializer.save()
```

---

Default

```python
def perform_create(self, serializer):

    serializer.save()
```

---

## কেন Override করবো?

Database save-এর আগে extra data যোগ করতে।

---

### Example

Current User Save

Model

```python
class Student(models.Model):

    user=models.ForeignKey(User)
```

View

```python
def perform_create(self, serializer):

    serializer.save(user=self.request.user)
```

এখন client user পাঠাবে না।

Automatically save হবে।

---

### Example

Create Log

```python
def perform_create(self, serializer):

    student = serializer.save()

    print(student.name)
```

---

### Example

Email Send

```python
def perform_create(self, serializer):

    student = serializer.save()

    send_mail(...)
```

---

### Example

Notification

```python
def perform_create(self, serializer):

    student = serializer.save()

    Notification.objects.create(...)
```

---

# Flow

```text
POST

↓

Serializer Validation

↓

perform_create()

↓

serializer.save()

↓

Database
```

---

# 4. perform_update()

## কখন Call হয়?

```
PUT

PATCH
```

দুই ক্ষেত্রেই।

---

Default

```python
def perform_update(self, serializer):

    serializer.save()
```

---

## Example

Update User

```python
def perform_update(self, serializer):

    serializer.save(updated_by=self.request.user)
```

---

### Example

Last Modified

```python
def perform_update(self, serializer):

    serializer.save(last_modified=timezone.now())
```

---

### Example

Audit Log

```python
def perform_update(self, serializer):

    student = serializer.save()

    print("Updated", student.name)
```

---

### Example

Cache Clear

```python
def perform_update(self, serializer):

    student = serializer.save()

    cache.delete(f"student_{student.id}")
```

---

# Flow

```text
PUT/PATCH

↓

Validation

↓

perform_update()

↓

serializer.save()

↓

Database
```

---

# 5. perform_destroy()

## কখন Call হয়?

```
DELETE
```

---

Default

```python
def perform_destroy(self, instance):

    instance.delete()
```

---

## Example

Soft Delete

Model

```python
is_deleted=True
```

View

```python
def perform_destroy(self, instance):

    instance.is_deleted=True

    instance.save()
```

Database থেকে delete হবে না।

---

### Example

Delete Log

```python
def perform_destroy(self, instance):

    print(instance.name)

    instance.delete()
```

---

### Example

Delete Image

```python
def perform_destroy(self, instance):

    instance.image.delete()

    instance.delete()
```

---

### Example

Archive

```python
def perform_destroy(self, instance):

    ArchiveStudent.objects.create(
        name=instance.name
    )

    instance.delete()
```

---

# Complete CRUD Lifecycle

## LIST

```text
GET /students/

↓

get_queryset()

↓

get_serializer_class()

↓

Serializer

↓

Response
```

---

## DETAIL

```text
GET /students/5/

↓

get_queryset()

↓

get_object()

↓

get_serializer_class()

↓

Response
```

---

## CREATE

```text
POST

↓

get_serializer_class()

↓

Validation

↓

perform_create()

↓

serializer.save()

↓

Response
```

---

## UPDATE

```text
PUT

↓

get_queryset()

↓

get_object()

↓

get_serializer_class()

↓

Validation

↓

perform_update()

↓

serializer.save()

↓

Response
```

---

## DELETE

```text
DELETE

↓

get_queryset()

↓

get_object()

↓

perform_destroy()

↓

instance.delete()

↓

204 No Content
```

---

# Real E-commerce Example

```python
class ProductViewSet(ModelViewSet):

    def get_queryset(self):

        # শুধু Published Product
        return Product.objects.filter(is_published=True)


    def get_serializer_class(self):

        if self.action == "list":
            return ProductListSerializer

        if self.action == "create":
            return ProductCreateSerializer

        return ProductDetailSerializer


    def perform_create(self, serializer):

        serializer.save(created_by=self.request.user)


    def perform_update(self, serializer):

        serializer.save(updated_by=self.request.user)


    def perform_destroy(self, instance):

        # Soft Delete
        instance.is_deleted=True
        instance.save()
```

---

# Professional Interview Summary

| Method                   | কখন Call হয়                   | Purpose                        | সবচেয়ে Common Use                                                                |
| ------------------------ | ------------------------------ | ------------------------------ | --------------------------------------------------------------------------------- |
| `get_queryset()`         | List, Retrieve, Update, Delete | কোন data আনবে                  | User-based filtering, search, optimization (`select_related`, `prefetch_related`) |
| `get_serializer_class()` | সব Action-এর আগে               | কোন serializer ব্যবহার হবে     | List/Detail/Create-এর জন্য আলাদা serializer                                       |
| `perform_create()`       | POST                           | Save-এর আগে/সময় extra logic   | `created_by`, owner, notifications, emails                                        |
| `perform_update()`       | PUT/PATCH                      | Update-এর আগে/সময় extra logic | `updated_by`, audit log, cache invalidation                                       |
| `perform_destroy()`      | DELETE                         | Delete logic                   | Soft delete, file cleanup, archiving                                              |

## পরবর্তী গুরুত্বপূর্ণ বিষয়

এখন সবচেয়ে যৌক্তিক বিষয় হলো **`get_object()`**। এটি `retrieve()`, `update()`, `partial_update()`, `destroy()`-এর ভিতরে কীভাবে object খুঁজে বের করে, `lookup_field`, permissions এবং `404` handling কীভাবে কাজ করে—এগুলো বোঝা। `get_object()` বুঝলে `ModelViewSet`-এর অভ্যন্তরীণ flow সম্পূর্ণ পরিষ্কার হয়ে যাবে।
দারুণ। `get_object()` বুঝতে পারলে আপনি DRF-এর `ModelViewSet`-এর **retrieve(), update(), partial_update(), destroy()** সম্পূর্ণ বুঝে যাবেন।

---

# get_object() কী?

`get_object()`-এর কাজ হলো:

> **URL থেকে আসা `pk` (বা `lookup_field`) ব্যবহার করে Database থেকে একটি নির্দিষ্ট object বের করা, permission check করা, এবং object না থাকলে 404 return করা।**

---

# Complete Flow

ধরি API call হলো

```text
GET /students/5/
```

DRF-এর ভিতরে কী হয়?

```text
Client
   │
   ▼
GET /students/5/
   │
   ▼
Router
   │
   ▼
StudentViewSet.retrieve()
   │
   ▼
get_object()
   │
   ├── get_queryset()
   │
   ├── lookup_field
   │
   ├── filter()
   │
   ├── get_object_or_404()
   │
   ├── check_object_permissions()
   │
   ▼
Student Object
   │
   ▼
Serializer
   │
   ▼
JSON Response
```

---

# DRF Source Code (Simplified)

DRF-এর `GenericAPIView`-এ `get_object()` প্রায় এইভাবে implement করা আছে।

```python
def get_object(self):

    queryset = self.filter_queryset(self.get_queryset())

    lookup_url_kwarg = self.lookup_url_kwarg or self.lookup_field

    lookup_value = self.kwargs[lookup_url_kwarg]

    obj = get_object_or_404(
        queryset,
        **{self.lookup_field: lookup_value}
    )

    self.check_object_permissions(self.request, obj)

    return obj
```

এখন আমরা এক লাইনের অর্থও বুঝব।

---

# Step 1 : get_queryset()

```python
queryset = self.get_queryset()
```

ধরি

```python
class StudentViewSet(ModelViewSet):

    queryset = Student.objects.filter(is_active=True)
```

Result

```python
queryset

↓

Student.objects.filter(is_active=True)
```

অর্থাৎ inactive student কখনো পাওয়া যাবে না।

---

# Step 2 : lookup_field

Default

```python
lookup_field = "pk"
```

URL

```text
/students/5/
```

DRF বুঝে

```python
pk = 5
```

Database Query

```python
Student.objects.get(pk=5)
```

---

# যদি lookup_field পরিবর্তন করি?

```python
class StudentViewSet(ModelViewSet):

    lookup_field = "uuid"
```

URL

```text
/students/f4f-554-ff4/
```

Database

```python
Student.objects.get(uuid="f4f-554-ff4")
```

---

আরও Example

```python
lookup_field = "slug"
```

URL

```text
/products/iphone-16/
```

Database

```python
Product.objects.get(slug="iphone-16")
```

---

# Step 3 : kwargs

Router

```text
/students/5/
```

kwargs

```python
{
    "pk":5
}
```

যদি

```python
lookup_field="uuid"
```

তাহলে

```python
{
    "uuid":"abc123"
}
```

---

View-এর ভিতরে

```python
print(self.kwargs)
```

Output

```python
{
    "pk":5
}
```

---

একটা value নিতে

```python
pk = self.kwargs["pk"]
```

---

# Step 4 : Object Query

DRF internally

```python
obj = get_object_or_404(
    queryset,
    pk=5
)
```

Equivalent

```python
Student.objects.get(pk=5)
```

কিন্তু safer।

---

যদি Object থাকে

Database

```text
id=5
name=Rahim
```

Output

```python
student_object
```

---

যদি না থাকে

```text
GET /students/500/
```

Database

```text
No Student
```

Automatically

```text
404 Not Found
```

JSON

```json
{
    "detail":"Not found."
}
```

আপনাকে কিছু লিখতে হবে না।

---

# Step 5 : Permission Check

Object পাওয়ার পরে DRF

```python
self.check_object_permissions(
    request,
    obj
)
```

call করে।

---

ধরি Permission

```python
class IsOwner(BasePermission):

    def has_object_permission(
        self,
        request,
        view,
        obj
    ):

        return obj.user == request.user
```

View

```python
permission_classes = [IsOwner]
```

Flow

```text
Student Found

↓

Owner?

↓

Yes

↓

Response
```

---

Owner না হলে

```text
403 Forbidden
```

Response

```json
{
    "detail":"Permission denied."
}
```

---

# retrieve()

DRF internally

```python
def retrieve(self, request, *args, **kwargs):

    instance = self.get_object()

    serializer = self.get_serializer(instance)

    return Response(serializer.data)
```

---

Diagram

```text
GET /students/5/

↓

retrieve()

↓

get_object()

↓

Student

↓

Serializer

↓

JSON
```

---

# update()

DRF internally

```python
def update(self, request, *args, **kwargs):

    instance = self.get_object()

    serializer = self.get_serializer(
        instance,
        data=request.data
    )

    serializer.is_valid()

    serializer.save()

    return Response(serializer.data)
```

---

Flow

```text
PUT

↓

get_object()

↓

Validation

↓

Save

↓

Response
```

---

# partial_update()

Exactly একই।

শুধু

```python
partial=True
```

ব্যবহার করে।

```python
serializer = self.get_serializer(
    instance,
    data=request.data,
    partial=True
)
```

---

# destroy()

```python
def destroy(self, request, *args, **kwargs):

    instance = self.get_object()

    instance.delete()

    return Response(status=204)
```

---

Flow

```text
DELETE

↓

get_object()

↓

Delete

↓

204
```

---

# Override get_object()

Professional project-এ অনেক সময় Override করা হয়।

Example

```python
class StudentViewSet(ModelViewSet):

    def get_object(self):

        obj = super().get_object()

        print("Student Found")

        return obj
```

---

## Example 2

Object Access Log

```python
def get_object(self):

    obj = super().get_object()

    AccessLog.objects.create(

        user=self.request.user,

        student=obj
    )

    return obj
```

---

## Example 3

Extra Validation

```python
def get_object(self):

    obj = super().get_object()

    if obj.is_deleted:

        raise PermissionDenied(
            "Deleted Student"
        )

    return obj
```

---

# get_object() vs get_queryset()

অনেকেই এই দুইটা গুলিয়ে ফেলে।

| get_queryset()               | get_object()                   |
| ---------------------------- | ------------------------------ |
| অনেক object return করে       | একটি object return করে         |
| List API-তে বেশি ব্যবহার হয় | Detail API-তে ব্যবহার হয়      |
| Filter করে                   | নির্দিষ্ট object খুঁজে বের করে |
| QuerySet return করে          | Model Instance return করে      |

Example

```python
get_queryset()

↓

<QuerySet [
Rahim,
Karim,
Hasan
]>
```

আর

```python
get_object()

↓

Rahim
```

---

# Complete Lifecycle (Detail Request)

```text
GET /students/5/

        │
        ▼
Router

        │
        ▼
retrieve()

        │
        ▼
get_queryset()

        │
        ▼
Student.objects.filter(is_active=True)

        │
        ▼
lookup_field="pk"

        │
        ▼
kwargs={"pk":5}

        │
        ▼
get_object_or_404()

        │
        ▼
Student(id=5)

        │
        ▼
check_object_permissions()

        │
        ▼
Serializer

        │
        ▼
JSON Response
```

# Interview Tips

যদি Interview-তে প্রশ্ন করে:

> **"ModelViewSet-এ get_object() কী করে?"**

সংক্ষিপ্ত ও Professional উত্তর হবে:

> "`get_object()` হলো `GenericAPIView`-এর একটি method। এটি `get_queryset()` থেকে queryset নেয়, `lookup_field` এবং URL-এর `kwargs` ব্যবহার করে নির্দিষ্ট object খুঁজে বের করে, object না পেলে `404 Not Found` দেয়, object-level permission check করে, তারপর সেই model instance return করে। এটি `retrieve()`, `update()`, `partial_update()`, এবং `destroy()`-এর ভিতরে ব্যবহৃত হয়।"

---

## পরবর্তী অধ্যায় (সবচেয়ে গুরুত্বপূর্ণ)

এখন আপনার শেখা উচিত **`@action` Decorator (Custom Endpoints)**।

এটি শিখলে আপনি শুধু CRUD নয়, এরকম production-level API তৈরি করতে পারবেন:

```text
POST   /students/5/activate/
POST   /students/5/reset-password/
POST   /orders/25/cancel/
POST   /courses/10/enroll/
GET    /products/featured/
GET    /dashboard/statistics/
```

এগুলোই বাস্তব SaaS, E-commerce, LMS, Exam System-এ প্রতিদিন ব্যবহার হয়।
এটি DRF-এর **সবচেয়ে শক্তিশালী feature**। একজন Professional Backend Developer হিসেবে `@action` অবশ্যই জানতে হবে।

---

# @action কী?

`@action` হলো একটি **custom endpoint** তৈরির decorator।

`ModelViewSet`-এ default endpoint থাকে:

```text
GET      /students/
GET      /students/1/
POST     /students/
PUT      /students/1/
PATCH    /students/1/
DELETE   /students/1/
```

কিন্তু যদি নতুন endpoint দরকার হয়?

যেমন

```text
POST /students/1/activate/

POST /students/1/reset-password/

POST /orders/5/cancel/

POST /courses/10/enroll/

GET /products/featured/
```

এগুলো CRUD-এর মধ্যে নেই।

এখানেই `@action` ব্যবহার করা হয়।

---

# Without @action

ধরি Student Activate করতে হবে।

CRUD method গুলো

```python
list()

retrieve()

create()

update()

partial_update()

destroy()
```

এগুলোর কোনটাই

```text
activate()
```

support করে না।

---

# With @action

```python
from rest_framework.decorators import action
from rest_framework.response import Response

class StudentViewSet(ModelViewSet):

    @action(
        detail=True,
        methods=["post"]
    )
    def activate(self, request, pk=None):

        return Response({
            "message":"Student Activated"
        })
```

Automatically URL

```text
POST

/students/5/activate/
```

---

# detail=True vs detail=False

এটাই সবচেয়ে গুরুত্বপূর্ণ।

---

## detail=True

মানে

একটি নির্দিষ্ট object-এর উপর কাজ হবে।

URL

```text
/students/5/activate/
```

এখানে

```text
pk=5
```

থাকে।

---

Flow

```text
Student

↓

id=5

↓

activate()

↓

Response
```

---

Example

```python
@action(
    detail=True,
    methods=["post"]
)
def activate(self, request, pk=None):

    student = self.get_object()

    student.is_active=True

    student.save()

    return Response({
        "status":"Activated"
    })
```

---

URL

```text
POST

/students/5/activate/
```

---

# detail=False

এখানে

কোন pk থাকে না।

পুরো collection-এর জন্য endpoint।

Example

```python
@action(
    detail=False,
    methods=["get"]
)
def featured(self, request):

    return Response({
        "products":[]
    })
```

URL

```text
GET

/products/featured/
```

Notice

```text
/products/

↓

featured
```

No PK.

---

# Difference

## detail=True

```text
/products/10/

↓

activate
```

Object Level

---

## detail=False

```text
/products/

↓

featured
```

Collection Level

---

# Example 1

Student Activate

Model

```python
class Student(models.Model):

    name=models.CharField(max_length=100)

    is_active=models.BooleanField(default=False)
```

View

```python
from rest_framework.decorators import action

class StudentViewSet(ModelViewSet):

    queryset=Student.objects.all()

    serializer_class=StudentSerializer

    @action(
        detail=True,
        methods=["post"]
    )
    def activate(self,request,pk=None):

        student=self.get_object()

        student.is_active=True

        student.save()

        return Response({

            "message":"Activated"
        })
```

---

URL

```text
POST

/students/5/activate/
```

Response

```json
{
"message":"Activated"
}
```

---

# Example 2

Deactivate

```python
@action(
    detail=True,
    methods=["post"]
)
def deactivate(self,request,pk=None):

    student=self.get_object()

    student.is_active=False

    student.save()

    return Response({
        "message":"Deactivated"
    })
```

URL

```text
POST

/students/5/deactivate/
```

---

# Example 3

Reset Password

```python
@action(
    detail=True,
    methods=["post"]
)
def reset_password(self,request,pk=None):

    student=self.get_object()

    password=request.data.get("password")

    student.set_password(password)

    student.save()

    return Response({

        "message":"Password Reset"
    })
```

URL

```text
POST

/users/7/reset_password/
```

Request

```json
{
"password":"abc123"
}
```

---

# Example 4

Enroll Course

Course

```python
class CourseViewSet(ModelViewSet):
```

```python
@action(
    detail=True,
    methods=["post"]
)
def enroll(self,request,pk=None):

    course=self.get_object()

    Enrollment.objects.create(

        course=course,

        student=request.user
    )

    return Response({

        "message":"Enrollment Success"
    })
```

---

URL

```text
POST

/courses/10/enroll/
```

---

# Example 5

Order Cancel

```python
@action(
    detail=True,
    methods=["post"]
)
def cancel(self,request,pk=None):

    order=self.get_object()

    order.status="Cancelled"

    order.save()

    return Response({

        "message":"Cancelled"
    })
```

---

URL

```text
POST

/orders/25/cancel/
```

---

# detail=False Example

Featured Products

```python
@action(
    detail=False,
    methods=["get"]
)
def featured(self,request):

    queryset=Product.objects.filter(

        featured=True
    )

    serializer=self.get_serializer(

        queryset,

        many=True
    )

    return Response(serializer.data)
```

URL

```text
GET

/products/featured/
```

---

# Example 2

Statistics

```python
@action(
    detail=False,
    methods=["get"]
)
def statistics(self,request):

    return Response({

        "students":200,

        "courses":30,

        "orders":1000
    })
```

URL

```text
GET

/dashboard/statistics/
```

---

# Multiple HTTP Methods

```python
@action(

    detail=True,

    methods=["get","post"]
)
```

এখন

```text
GET

POST
```

দুইটাই support করবে।

---

# Custom URL Name

```python
@action(

    detail=True,

    methods=["post"],

    url_path="change-status"
)
```

Method

```python
def status(self,request,pk=None):
```

URL

```text
POST

/products/5/change-status/
```

---

# Custom URL Name + URL Route

```python
@action(

    detail=True,

    methods=["post"],

    url_path="publish",

    url_name="publish-product"
)
```

---

# Permission per Action

```python
from rest_framework.permissions import IsAdminUser

@action(

    detail=True,

    methods=["post"],

    permission_classes=[IsAdminUser]
)
def publish(self,request,pk=None):

    ...
```

শুধু Admin call করতে পারবে।

---

# Different Serializer

```python
class PasswordSerializer(serializers.Serializer):

    password=serializers.CharField()
```

```python
@action(

    detail=True,

    methods=["post"]
)
def reset_password(self,request,pk=None):

    serializer=PasswordSerializer(

        data=request.data
    )

    serializer.is_valid(

        raise_exception=True
    )

    return Response()
```

---

# Complete Flow

```text
POST

/students/5/activate/

        │
        ▼

Router

        │
        ▼

StudentViewSet.activate()

        │
        ▼

get_object()

        │
        ▼

Student(id=5)

        │
        ▼

Business Logic

is_active=True

        │
        ▼

Save()

        │
        ▼

JSON Response
```

---

# Real SaaS Examples

### Authentication

```text
POST

/users/5/verify-email/
```

```text
POST

/users/5/resend-otp/
```

```text
POST

/users/5/change-password/
```

---

### E-commerce

```text
POST

/orders/5/cancel/
```

```text
POST

/orders/5/refund/
```

```text
POST

/products/10/add-stock/
```

```text
POST

/products/10/remove-stock/
```

---

### LMS / Exam

```text
POST

/courses/5/enroll/
```

```text
POST

/exams/10/start/
```

```text
POST

/exams/10/submit/
```

```text
GET

/exams/upcoming/
```

---

### Admin Dashboard

```text
GET

/dashboard/statistics/
```

```text
GET

/dashboard/recent-users/
```

```text
GET

/dashboard/sales-report/
```

---

# Production Tips

### ✅ `detail=True` ব্যবহার করুন যখন:

* একটি নির্দিষ্ট object-এর উপর action হবে।
* `self.get_object()` ব্যবহার করতে হবে।
* URL-এ `pk` বা `lookup_field` লাগবে।

উদাহরণ:

* `activate`
* `cancel`
* `publish`
* `reset_password`
* `enroll`

### ✅ `detail=False` ব্যবহার করুন যখন:

* পুরো collection নিয়ে কাজ হবে।
* `pk` লাগবে না।
* Filtered list, reports, dashboard data ফেরত দেবেন।

উদাহরণ:

* `featured`
* `statistics`
* `recent_orders`
* `top_students`

---

# Interview Question

**প্রশ্ন:** `@action` কেন ব্যবহার করবেন, নতুন APIView লিখলেই তো হয়?

**উত্তর:**

* `@action` একই `ViewSet`-এর মধ্যে related business logic রাখে।
* একই `queryset`, `serializer`, `permission`, `authentication`, `throttling` পুনরায় ব্যবহার করা যায়।
* Router স্বয়ংক্রিয়ভাবে URL তৈরি করে।
* Code বেশি organized এবং maintainable হয়।

---

## পরবর্তী অধ্যায় (Advanced DRF)

এখন আপনি এমন একটি বিষয় শিখতে প্রস্তুত যেটা প্রায় সব বড় DRF project-এ ব্যবহৃত হয়:

> **Dynamic Serializer + Dynamic Permission + Dynamic Queryset Pattern**

এখানে আপনি শিখবেন কীভাবে **একটি মাত্র `ModelViewSet`** ব্যবহার করে:

* `list()` → `StudentListSerializer`
* `retrieve()` → `StudentDetailSerializer`
* `create()` → `StudentCreateSerializer`
* `update()` → `StudentUpdateSerializer`
* `reset_password()` → `PasswordResetSerializer`

এবং একই ViewSet-এ action অনুযায়ী ভিন্ন `permission_classes`, `queryset` optimization (`select_related`, `prefetch_related`) ও business logic ব্যবহার করবেন। এটি production-grade DRF development-এর সবচেয়ে জনপ্রিয় pattern।
চমৎকার। এখন আমরা **Production-Level DRF Pattern** শিখব। এটি বড় কোম্পানি (Netflix, Stripe, GitLab, Shopify-এর মতো backend architecture)-তেও একই ধরনের ধারণা ব্যবহার করা হয়।

---

# কেন Dynamic Pattern দরকার?

ধরুন আপনার `Student` Model আছে।

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    phone = models.CharField(max_length=20)
    address = models.TextField()
    is_active = models.BooleanField(default=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

একটি API-এর সব action-এ কি একই data লাগবে?

না।

| Action           | কী Data লাগবে?     |
| ---------------- | ------------------ |
| list()           | id, name           |
| retrieve()       | সব field           |
| create()         | name, email, phone |
| update()         | phone, address     |
| reset_password() | শুধু password      |

এখন যদি একটাই Serializer ব্যবহার করেন?

```python
class StudentSerializer(ModelSerializer):
    class Meta:
        model = Student
        fields = "__all__"
```

তাহলে সমস্যা হবে।

* List API-তে unnecessary data যাবে।
* Password field expose হতে পারে।
* Performance কমে যাবে।
* Validation complicated হবে।

তাই Dynamic Serializer ব্যবহার করা হয়।

---

# Step 1: Multiple Serializer তৈরি

## List Serializer

```python
class StudentListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = [
            "id",
            "name"
        ]
```

Response

```json
[
    {
        "id":1,
        "name":"Rahim"
    }
]
```

---

## Detail Serializer

```python
class StudentDetailSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"
```

Response

```json
{
    "id":1,
    "name":"Rahim",
    "email":"abc@gmail.com",
    "phone":"0188",
    "address":"Dhaka"
}
```

---

## Create Serializer

```python
class StudentCreateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = [
            "name",
            "email",
            "phone"
        ]
```

---

## Update Serializer

```python
class StudentUpdateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Student
        fields = [
            "phone",
            "address"
        ]
```

---

## Password Serializer

```python
class PasswordResetSerializer(serializers.Serializer):

    password = serializers.CharField(
        min_length=8
    )
```

---

# Step 2: Dynamic Serializer

এখন ViewSet

```python
from rest_framework.viewsets import ModelViewSet

class StudentViewSet(ModelViewSet):

    queryset = Student.objects.all()
```

---

## get_serializer_class()

```python
def get_serializer_class(self):

    if self.action == "list":
        return StudentListSerializer

    elif self.action == "retrieve":
        return StudentDetailSerializer

    elif self.action == "create":
        return StudentCreateSerializer

    elif self.action in ["update", "partial_update"]:
        return StudentUpdateSerializer

    elif self.action == "reset_password":
        return PasswordResetSerializer

    return StudentDetailSerializer
```

---

# Flow

## GET /students/

```
Router

↓

action = list

↓

get_serializer_class()

↓

StudentListSerializer
```

---

## GET /students/5/

```
action

↓

retrieve

↓

StudentDetailSerializer
```

---

## POST /students/

```
action

↓

create

↓

StudentCreateSerializer
```

---

## PATCH

```
action

↓

update

↓

StudentUpdateSerializer
```

---

## POST

```
/students/5/reset_password/
```

```
action

↓

reset_password

↓

PasswordResetSerializer
```

---

# Step 3: Dynamic Permission

সব API কি একই permission ব্যবহার করবে?

না।

| Action   | Permission |
| -------- | ---------- |
| list     | Everyone   |
| retrieve | Login User |
| create   | Admin      |
| delete   | Superuser  |

---

Example

```python
from rest_framework.permissions import (
    AllowAny,
    IsAuthenticated,
    IsAdminUser
)
```

```python
def get_permissions(self):

    if self.action == "list":

        permission_classes = [
            AllowAny
        ]

    elif self.action == "retrieve":

        permission_classes = [
            IsAuthenticated
        ]

    elif self.action == "create":

        permission_classes = [
            IsAdminUser
        ]

    else:

        permission_classes = [
            IsAuthenticated
        ]

    return [
        permission()
        for permission in permission_classes
    ]
```

---

Flow

```
GET /students/

↓

AllowAny
```

---

```
POST /students/

↓

IsAdminUser
```

---

```
DELETE

↓

IsAuthenticated
```

---

# Step 4: Dynamic Queryset

এটাই Professional Optimization।

---

## Problem

List API

```text
GET /students/
```

শুধু

```text
id

name
```

দরকার।

কিন্তু Database

```python
Student.objects.all()
```

সব data load করছে।

---

## Better

```python
def get_queryset(self):

    if self.action == "list":

        return Student.objects.only(
            "id",
            "name"
        )

    return Student.objects.all()
```

---

আরও Example

Suppose

```python
Student

↓

Course

↓

Teacher
```

List API

```python
def get_queryset(self):

    if self.action=="list":

        return Student.objects.select_related(

            "course"

        )

    return Student.objects.all()
```

---

Many-to-Many হলে

```python
def get_queryset(self):

    return Student.objects.prefetch_related(

        "subjects"
    )
```

---

# select_related()

One-to-One

ForeignKey

এর জন্য।

```python
Student

↓

Department
```

```python
Student.objects.select_related(

    "department"
)
```

Database Query

Without

```
100 Query
```

With

```
1 Query
```

---

# prefetch_related()

ManyToMany

Reverse FK

এর জন্য।

```python
Student

↓

Subjects
```

```python
Student.objects.prefetch_related(

    "subjects"
)
```

---

# Step 5: Dynamic Business Logic

```python
def perform_create(self, serializer):

    serializer.save(

        created_by=self.request.user
    )
```

---

Update

```python
def perform_update(self, serializer):

    serializer.save(

        updated_by=self.request.user
    )
```

---

Delete

```python
def perform_destroy(self, instance):

    instance.is_deleted=True

    instance.save()
```

---

# Production ViewSet

```python
class StudentViewSet(ModelViewSet):

    def get_queryset(self):

        if self.action=="list":

            return Student.objects.only(

                "id",
                "name"

            )

        return Student.objects.all()


    def get_serializer_class(self):

        if self.action=="list":

            return StudentListSerializer

        elif self.action=="create":

            return StudentCreateSerializer

        elif self.action in [

            "update",

            "partial_update"

        ]:

            return StudentUpdateSerializer

        return StudentDetailSerializer


    def get_permissions(self):

        if self.action=="list":

            permission_classes=[AllowAny]

        else:

            permission_classes=[IsAuthenticated]

        return [

            permission()

            for permission in permission_classes

        ]


    def perform_create(self,serializer):

        serializer.save(

            user=self.request.user
        )
```

---

# Request Lifecycle

```
GET /students/

        │
        ▼

Router

        │
        ▼

action = list

        │
        ▼

get_permissions()

        │
        ▼

AllowAny

        │
        ▼

get_queryset()

        │
        ▼

Student.objects.only(
id,name
)

        │
        ▼

get_serializer_class()

        │
        ▼

StudentListSerializer

        │
        ▼

Serializer

        │
        ▼

JSON
```

---

# Production Folder Structure

```
students/

    serializers/

        list.py

        detail.py

        create.py

        update.py

        password.py

    permissions.py

    views.py

    models.py
```

এভাবে serializer আলাদা file-এ রাখলে project clean থাকে।

---

# Senior Developer Pattern (Serializer Map)

বড় project-এ বারবার `if-elif` লেখা হয় না।

বরং একটি mapping dictionary ব্যবহার করা হয়।

```python
class StudentViewSet(ModelViewSet):

    serializer_action_classes = {
        "list": StudentListSerializer,
        "retrieve": StudentDetailSerializer,
        "create": StudentCreateSerializer,
        "update": StudentUpdateSerializer,
        "partial_update": StudentUpdateSerializer,
        "reset_password": PasswordResetSerializer,
    }

    def get_serializer_class(self):
        return self.serializer_action_classes.get(
            self.action,
            StudentDetailSerializer
        )
```

একইভাবে Permission-এর জন্যও mapping করা যায়।

```python
permission_action_classes = {
    "list": [AllowAny],
    "create": [IsAdminUser],
}
```

এটি **production-grade** pattern, code clean থাকে, নতুন action যোগ করাও সহজ হয়।

---

# আপনি এখন DRF-এর Advanced Level-এ

আপনি ইতিমধ্যে শিখেছেন:

* ✅ APIView
* ✅ ViewSet
* ✅ GenericViewSet
* ✅ ModelViewSet
* ✅ Request Lifecycle
* ✅ `get_queryset()`
* ✅ `get_object()`
* ✅ `get_serializer_class()`
* ✅ `perform_create()`
* ✅ `perform_update()`
* ✅ `perform_destroy()`
* ✅ `@action`
* ✅ Dynamic Serializer
* ✅ Dynamic Permission
* ✅ Dynamic Queryset

## পরবর্তী অধ্যায় (যেটা আমি Senior DRF Developer-এর জন্য শেখাই)

এখন শিখুন **Filtering + Search + Ordering + Pagination + django-filter**। এগুলো ছাড়া কোনো production API সম্পূর্ণ হয় না। প্রায় প্রতিটি E-commerce, LMS, SaaS, Job Portal, Exam System-এ এই features থাকে এবং Interview-তেও খুবই common।
এটি DRF-এর **Production API Development**-এর সবচেয়ে গুরুত্বপূর্ণ অধ্যায়গুলোর একটি।

বাস্তব কোনো API দেখুন (Amazon, Daraz, Coursera, LinkedIn, Job Portal)—প্রায় সব List API-তেই এই ৫টি feature থাকে।

* Filtering
* Search
* Ordering
* Pagination
* django-filter

---

# একটি Real Example

ধরি Product API

```text
GET /products/
```

Client চাইতে পারে—

```text
সব Product
```

অথবা

```text
GET /products/?category=electronics
```

অথবা

```text
GET /products/?search=iphone
```

অথবা

```text
GET /products/?ordering=-price
```

অথবা

```text
GET /products/?page=3
```

অথবা

```text
GET /products/?category=electronics&search=iphone&ordering=-price&page=2
```

একটি API-তেই সব একসাথে কাজ করবে।

---

# Complete Request Flow

```text
Client

      │

      ▼

GET /products/

      │

      ▼

ViewSet

      │

      ▼

get_queryset()

      │

      ▼

Filtering

      │

      ▼

Search

      │

      ▼

Ordering

      │

      ▼

Pagination

      │

      ▼

Serializer

      │

      ▼

JSON Response
```

---

# Example Model

```python
class Product(models.Model):

    name = models.CharField(max_length=200)

    category = models.CharField(max_length=100)

    price = models.DecimalField(max_digits=10, decimal_places=2)

    stock = models.IntegerField()

    created_at = models.DateTimeField(auto_now_add=True)

    description = models.TextField()
```

---

# ১. Filtering

## Filtering কী?

নির্দিষ্ট condition অনুযায়ী data বের করা।

ধরি

```text
GET

/products/?category=electronics
```

Output

```text
Electronics Products Only
```

---

## Manual Filtering

```python
def get_queryset(self):

    queryset = Product.objects.all()

    category = self.request.query_params.get("category")

    if category:

        queryset = queryset.filter(category=category)

    return queryset
```

---

Request

```text
GET

/products/?category=electronics
```

SQL

```sql
SELECT *

FROM product

WHERE category='electronics';
```

---

Multiple Filter

```python
def get_queryset(self):

    queryset = Product.objects.all()

    category = self.request.query_params.get("category")

    stock = self.request.query_params.get("stock")

    if category:

        queryset = queryset.filter(category=category)

    if stock:

        queryset = queryset.filter(stock=stock)

    return queryset
```

---

Request

```text
GET

/products/?category=electronics&stock=10
```

---

# ২. Search

Filtering exact match করে।

Search partial match করে।

---

Example

```text
GET

/products/?search=iphone
```

Database

```text
iPhone 16

iPhone 15

iPhone Cover
```

সব return করবে।

---

Manual

```python
from django.db.models import Q

def get_queryset(self):

    queryset = Product.objects.all()

    search = self.request.query_params.get("search")

    if search:

        queryset = queryset.filter(

            Q(name__icontains=search)

            |

            Q(description__icontains=search)

        )

    return queryset
```

---

Request

```text
GET

/products/?search=iphone
```

SQL

```sql
WHERE

name LIKE '%iphone%'

OR

description LIKE '%iphone%'
```

---

# ৩. Ordering

Price অনুযায়ী Sort।

Request

```text
GET

/products/?ordering=price
```

Ascending

```text
100

200

300
```

---

Descending

```text
GET

/products/?ordering=-price
```

Output

```text
300

200

100
```

---

Manual

```python
def get_queryset(self):

    queryset = Product.objects.all()

    ordering = self.request.query_params.get("ordering")

    if ordering:

        queryset = queryset.order_by(ordering)

    return queryset
```

---

More Example

```text
?ordering=name

?ordering=created_at

?ordering=-created_at

?ordering=stock
```

---

# ৪. Pagination

সব data একবারে পাঠানো উচিত?

না।

Suppose

```text
5 Million Products
```

সব এক request-এ পাঠালে

* Slow হবে
* Memory বেশি লাগবে
* Response বিশাল হবে

তাই Pagination।

---

Without Pagination

```text
GET

/products/
```

Response

```text
500000 Records
```

---

With Pagination

```text
GET

/products/?page=1
```

Response

```json
{
    "count":500000,

    "next":"page=2",

    "previous":null,

    "results":[]
}
```

---

Settings

```python
REST_FRAMEWORK={

    "DEFAULT_PAGINATION_CLASS":

    "rest_framework.pagination.PageNumberPagination",

    "PAGE_SIZE":10
}
```

---

Output

```text
Page 1

↓

10 Products
```

---

Next

```text
GET

?page=2
```

---

Custom Pagination

```python
from rest_framework.pagination import PageNumberPagination

class ProductPagination(PageNumberPagination):

    page_size = 20

    page_size_query_param = "page_size"

    max_page_size = 100
```

ViewSet

```python
pagination_class = ProductPagination
```

---

Request

```text
GET

?page=1&page_size=50
```

---

# ৫. django-filter

এটাই Professional Way।

আগে install

```bash
pip install django-filter
```

---

settings.py

```python
INSTALLED_APPS = [

    ...

    "django_filters",
]
```

---

REST_FRAMEWORK

```python
REST_FRAMEWORK = {

    "DEFAULT_FILTER_BACKENDS":[

        "django_filters.rest_framework.DjangoFilterBackend"
    ]
}
```

---

View

```python
from django_filters.rest_framework import DjangoFilterBackend

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [

        DjangoFilterBackend
    ]

    filterset_fields = [

        "category",

        "stock"
    ]
```

---

Request

```text
GET

/products/?category=electronics
```

Automatically

```python
Product.objects.filter(

    category="electronics"
)
```

---

Multiple

```text
GET

/products/?category=electronics&stock=10
```

Automatically work করবে।

---

# SearchFilter

```python
from rest_framework.filters import SearchFilter
```

```python
filter_backends = [

    SearchFilter
]
```

```python
search_fields = [

    "name",

    "description"
]
```

Request

```text
GET

/products/?search=iphone
```

Automatically

```python
icontains
```

search করবে।

---

# OrderingFilter

```python
from rest_framework.filters import OrderingFilter
```

```python
filter_backends = [

    OrderingFilter
]
```

```python
ordering_fields = [

    "price",

    "created_at"
]
```

Request

```text
GET

/products/?ordering=-price
```

Automatically Sort করবে।

---

# Production Version

```python
from django_filters.rest_framework import DjangoFilterBackend
from rest_framework.filters import SearchFilter, OrderingFilter

class ProductViewSet(ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

    filter_backends = [

        DjangoFilterBackend,

        SearchFilter,

        OrderingFilter
    ]

    filterset_fields = [

        "category",

        "stock"
    ]

    search_fields = [

        "name",

        "description"
    ]

    ordering_fields = [

        "price",

        "created_at"
    ]
```

---

# এখন Request

Filtering

```text
GET

/products/?category=electronics
```

Search

```text
GET

/products/?search=iphone
```

Ordering

```text
GET

/products/?ordering=-price
```

সব একসাথে

```text
GET

/products/

?category=electronics

&search=iphone

&ordering=-price
```

সব Automatically।

---

# django-filter বনাম Manual Filtering

| Manual Filtering      | django-filter                       |
| --------------------- | ----------------------------------- |
| নিজে `if` লিখতে হয়   | Backend স্বয়ংক্রিয়ভাবে filter করে |
| Code বড় হয়          | Code ছোট ও পরিষ্কার                 |
| Maintain করা কঠিন     | Maintain করা সহজ                    |
| Complex filter-এ জটিল | Custom `FilterSet` দিয়ে সহজ        |

---

# Professional Tip: Custom FilterSet

শুধু `filterset_fields` নয়, Production project-এ `FilterSet` class ব্যবহার করা হয়।

```python
import django_filters

class ProductFilter(django_filters.FilterSet):
    min_price = django_filters.NumberFilter(field_name="price", lookup_expr="gte")
    max_price = django_filters.NumberFilter(field_name="price", lookup_expr="lte")

    class Meta:
        model = Product
        fields = ["category", "stock"]
```

ViewSet:

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer

    filter_backends = [
        DjangoFilterBackend,
        SearchFilter,
        OrderingFilter,
    ]

    filterset_class = ProductFilter
```

এখন API:

```text
GET /products/?category=electronics&min_price=500&max_price=5000&ordering=-price
```

---

# Interview Questions

### ১. `filterset_fields` আর `FilterSet`-এর মধ্যে পার্থক্য কী?

* `filterset_fields` → Simple exact filtering।
* `FilterSet` → Range filter, custom methods, complex filtering।

### ২. `SearchFilter` কীভাবে search করে?

Defaultভাবে `icontains` lookup ব্যবহার করে।

### ৩. `OrderingFilter`-এ `ordering_fields` না দিলে কী সমস্যা?

User যেকোনো model field দিয়ে ordering করার চেষ্টা করতে পারে। তাই production-এ allowed fields সীমাবদ্ধ রাখা ভালো।

---

# DRF Learning Roadmap (আপনি এখন এখানে)

```
✓ Serializer
✓ APIView
✓ GenericAPIView
✓ Mixins
✓ ViewSet
✓ GenericViewSet
✓ ModelViewSet
✓ Routers
✓ Actions
✓ Dynamic Serializer
✓ Dynamic Permission
✓ Dynamic Queryset
✓ Filtering
✓ Search
✓ Ordering
✓ Pagination
✓ django-filter

⬇ Next

□ Authentication
□ JWT
□ Custom Permission
□ Throttling
□ Versioning
□ Caching
□ Signals
□ Celery
□ Testing
□ Performance Optimization
```

## আমার সুপারিশ

আপনার লক্ষ্য যেহেতু **Production Django REST Framework + Full Stack Backend Developer**, তাই পরবর্তী বিষয় হওয়া উচিত:

> **Custom Authentication + Custom Permission + Object-Level Permission**

কারণ এগুলো ছাড়া কোনো SaaS, E-commerce, Job Portal বা Exam System নিরাপদভাবে তৈরি করা যায় না। আপনার আগের প্রশ্নগুলো (Firebase Auth, JWT, `dj-rest-auth`) বিবেচনা করলে এই অধ্যায়টি আপনার বর্তমান শেখার ধারার সঙ্গে সবচেয়ে ভালোভাবে মিলবে।

------------
এটা Django Model-এর **সবচেয়ে গুরুত্বপূর্ণ concept**। একজন Backend Developer হিসেবে আপনাকে বুঝতে হবে **কোন field required (mandatory)** আর **কোন field optional**।

---

# Rule 1: Default Behavior

যদি কিছুই না দেন, তাহলে Django ধরে নেয় field **Required**।

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

এখন

```python
Student.objects.create(
    name="Rahim"
)
```

❌ Error হবে।

কারণ

```python
age
```

দেওয়া হয়নি।

ঠিকভাবে

```python
Student.objects.create(
    name="Rahim",
    age=20
)
```

✔ Create হবে।

---

# Rule 2: null=True

```python
age = models.IntegerField(null=True)
```

মানে

Database-এ

```text
NULL
```

store করা যাবে।

এখন

```python
Student.objects.create(
    name="Rahim"
)
```

✔ Create হবে।

Database

| id | name  | age  |
| -- | ----- | ---- |
| 1  | Rahim | NULL |

---

# Rule 3: blank=True

এটা **Database-এর জন্য না**।

এটা

* Form
* Admin Panel
* Serializer Validation

এর জন্য।

Example

```python
name = models.CharField(
    max_length=100,
    blank=True
)
```

মানে

Form-এ

```text
Name

[      ]
```

খালি রাখা যাবে।

---

# Rule 4: default

```python
status = models.CharField(
    max_length=20,
    default="Pending"
)
```

এখন

```python
Student.objects.create(
    name="Rahim"
)
```

Database

| name  | status  |
| ----- | ------- |
| Rahim | Pending |

আপনি status দেননি।

Django নিজেই দিয়েছে।

---

# Rule 5: auto_now_add

```python
created_at = models.DateTimeField(
    auto_now_add=True
)
```

Create করার সময়

```python
Student.objects.create(
    name="Rahim"
)
```

Database

```text
created_at

2026-07-04 10:30
```

Automatically।

আপনাকে দিতে হবে না।

---

# Rule 6: auto_now

```python
updated_at = models.DateTimeField(
    auto_now=True
)
```

Update হলেই

Automatically change হবে।

---

# Rule 7: ForeignKey

```python
class Student(models.Model):

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )
```

Create

```python
Student.objects.create(
    name="Rahim"
)
```

❌ Error

কারণ

```python
user
```

Required।

---

Optional করতে

```python
user = models.ForeignKey(

    User,

    on_delete=models.CASCADE,

    null=True,

    blank=True
)
```

---

# Rule 8: ManyToMany

```python
subjects = models.ManyToManyField(Subject)
```

Create

```python
student = Student.objects.create(
    name="Rahim"
)
```

✔ Create হবে।

ManyToMany পরে add করা হয়।

```python
student.subjects.add(math)
```

---

# Rule 9: BooleanField

```python
is_active = models.BooleanField(default=True)
```

Create

```python
Student.objects.create(
    name="Rahim"
)
```

Database

```text
is_active=True
```

Automatically।

---

# Rule 10: UUID

```python
id = models.UUIDField(
    primary_key=True,
    default=uuid.uuid4,
    editable=False
)
```

আপনাকে UUID দিতে হবে না।

Automatically generate হবে।

---

# Rule 11: EmailField

```python
email = models.EmailField()
```

Create

```python
Student.objects.create(
    name="Rahim"
)
```

❌ Error

কারণ email required।

Optional

```python
email = models.EmailField(

    blank=True,

    null=True
)
```

---

# Rule 12: ImageField

```python
image = models.ImageField(
    upload_to="students/"
)
```

Default

Required।

Optional

```python
image = models.ImageField(

    upload_to="students/",

    null=True,

    blank=True
)
```

---

# Shortcut Rule

এই Model দেখুন।

```python
class Student(models.Model):

    name = models.CharField(max_length=100)

    age = models.IntegerField()

    email = models.EmailField(
        null=True,
        blank=True
    )

    phone = models.CharField(
        max_length=20,
        default=""
    )

    is_active = models.BooleanField(
        default=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

এখন প্রশ্ন—

কোনগুলো অবশ্যই দিতে হবে?

চলুন বিশ্লেষণ করি।

---

## name

```python
name = models.CharField(max_length=100)
```

❌ Required

---

## age

```python
age = models.IntegerField()
```

❌ Required

---

## email

```python
null=True

blank=True
```

✔ Optional

---

## phone

```python
default=""
```

✔ Optional

---

## is_active

```python
default=True
```

✔ Optional

---

## created_at

```python
auto_now_add=True
```

✔ Optional

---

Create

```python
Student.objects.create(

    name="Rahim",

    age=20
)
```

✔ কাজ করবে।

Database

```text
name

Rahim

age

20

email

NULL

phone

""

is_active

True

created_at

Current Time
```

---

# Interview Trick

এই Model দেখুন।

```python
class Product(models.Model):

    name = models.CharField(max_length=100)

    price = models.DecimalField(max_digits=10, decimal_places=2)

    description = models.TextField(
        blank=True
    )

    stock = models.IntegerField(
        default=0
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

Create করার সময় **কোন field অবশ্যই দিতে হবে?**

উত্তর:

```python
name

price
```

শুধু এই দুইটি।

কারণ:

* `description` → `blank=True`
* `stock` → `default=0`
* `created_at` → `auto_now_add=True`

---

# Professional Rule (মনে রাখার জন্য)

নিচের টেবিলটি মুখস্থ রাখুন:

| Field Option                        | Required?                         | কেন                                     |
| ----------------------------------- | --------------------------------- | --------------------------------------- |
| কিছুই নেই                           | ✅ Required                        | Django value আশা করে                    |
| `null=True`                         | ❌ Optional (DB)                   | Database-এ `NULL` রাখতে পারে            |
| `blank=True`                        | ❌ Optional (Validation)           | Form/Serializer খালি মান গ্রহণ করে      |
| `default=...`                       | ❌ Optional                        | Django নিজে মান বসিয়ে দেয়             |
| `auto_now_add=True`                 | ❌ Optional                        | Create-এর সময় স্বয়ংক্রিয়ভাবে সেট হয় |
| `auto_now=True`                     | ❌ Optional                        | Update-এর সময় স্বয়ংক্রিয়ভাবে সেট হয় |
| `ManyToManyField`                   | ❌ সাধারণত Create-এর সময় Optional | পরে `.add()` করা যায়                   |
| `ForeignKey` (default)              | ✅ Required                        | সম্পর্কিত object দিতে হবে               |
| `ForeignKey(null=True, blank=True)` | ❌ Optional                        | সম্পর্ক না থাকলেও চলবে                  |

## Production Tip

**Model দেখে Required Field চেনার সহজ নিয়ম:**

নিজেকে এই প্রশ্ন করুন:

> **"যদি আমি এই field-এর value না দিই, Django কি নিজে কোনো value দিতে পারবে?"**

* **হ্যাঁ** → Optional (যেমন `default`, `auto_now_add`, `auto_now`, `null=True`)
* **না** → Required (যেমন সাধারণ `CharField`, `IntegerField`, `ForeignKey`)

এই একটি নিয়ম মনে রাখলে প্রায় সব Model-এর required/optional field আপনি সহজেই বুঝতে পারবেন।
এটি Django Model-এর **সবচেয়ে confusing topic**। অনেক beginner বুঝতে পারে না **ForeignKey, OneToOneField, ManyToManyField** required নাকি optional।

মনে রাখার জন্য একটি Golden Rule আছে:

> **Relationship field-ও সাধারণ field-এর মতোই required হয়, যদি না আপনি explicitly optional করেন।**

---

# Django Relationship Types

```text
Student
   │
   ├── ForeignKey
   │
   ├── OneToOneField
   │
   └── ManyToManyField
```

এখন একে একে দেখি।

---

# 1. ForeignKey

ধরি

```python
class Department(models.Model):
    name = models.CharField(max_length=100)


class Student(models.Model):
    name = models.CharField(max_length=100)

    department = models.ForeignKey(
        Department,
        on_delete=models.CASCADE
    )
```

## Required না Optional?

```python
department = models.ForeignKey(...)
```

✅ **Required**

কারণ

* `null=True` নেই
* `default` নেই

---

## Create

```python
Student.objects.create(
    name="Rahim"
)
```

❌ Error

```
NOT NULL constraint failed
```

কারণ department দিতে হবে।

---

## Correct

```python
department = Department.objects.get(id=1)

Student.objects.create(
    name="Rahim",
    department=department
)
```

অথবা

```python
Student.objects.create(
    name="Rahim",
    department_id=1
)
```

দুটোই একই কাজ।

---

# ForeignKey Optional

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE,
    null=True,
    blank=True
)
```

এখন

```python
Student.objects.create(
    name="Rahim"
)
```

✔ Create হবে।

Database

| name  | department |
| ----- | ---------- |
| Rahim | NULL       |

---

# ForeignKey with default

```python
department = models.ForeignKey(
    Department,
    on_delete=models.CASCADE,
    default=1
)
```

Create

```python
Student.objects.create(
    name="Rahim"
)
```

Automatically

```text
department_id=1
```

save হবে।

---

# 2. OneToOneField

```python
class UserProfile(models.Model):

    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE
    )

    phone = models.CharField(max_length=20)
```

## Required?

হ্যাঁ।

```python
UserProfile.objects.create(
    phone="01888"
)
```

❌ Error

কারণ user লাগবে।

---

Optional

```python
user = models.OneToOneField(
    User,
    on_delete=models.CASCADE,
    null=True,
    blank=True
)
```

এখন Optional।

---

# OneToOne কখন ব্যবহার হয়?

```text
User
   │
   ▼
Profile
```

একজন User-এর

মাত্র

একটি Profile।

---

# 3. ManyToManyField

এটাই সবচেয়ে আলাদা।

```python
class Subject(models.Model):

    name = models.CharField(max_length=100)


class Student(models.Model):

    name = models.CharField(max_length=100)

    subjects = models.ManyToManyField(
        Subject
    )
```

---

## Required?

**Create-এর সময় Required না।**

কারণ

ManyToMany relationship save হয়

**Student save হওয়ার পরে।**

---

Create

```python
student = Student.objects.create(
    name="Rahim"
)
```

✔ Create হবে।

এখনও কোন Subject নেই।

---

পরে

```python
math = Subject.objects.get(id=1)

physics = Subject.objects.get(id=2)

student.subjects.add(math)

student.subjects.add(physics)
```

---

Database

Student

| id | name  |
| -- | ----- |
| 1  | Rahim |

Subject

| id | name    |
| -- | ------- |
| 1  | Math    |
| 2  | Physics |

Intermediate Table

| student_id | subject_id |
| ---------- | ---------- |
| 1          | 1          |
| 1          | 2          |

---

# Why ManyToMany Required নয়?

কারণ

Create Flow

```text
Student

↓

Save

↓

ID Generated

↓

ManyToMany Table Update
```

Student-এর ID না থাকলে ManyToMany relation save করা যায় না।

---

# Serializer-এর ক্ষেত্রে

DRF Serializer-এ

```python
class StudentSerializer(ModelSerializer):

    class Meta:

        model = Student

        fields = "__all__"
```

Request

```json
{
    "name":"Rahim",
    "department":1
}
```

ForeignKey

✔ Works

---

ManyToMany

```json
{
    "name":"Rahim",
    "subjects":[
        1,
        2,
        3
    ]
}
```

Serializer

Automatically

```python
student.subjects.set([
    1,
    2,
    3
])
```

করবে।

---

# Required vs Optional Summary

| Relationship    | Default                   | Optional করার উপায়                                                                  |
| --------------- | ------------------------- | ------------------------------------------------------------------------------------ |
| ForeignKey      | ✅ Required                | `null=True, blank=True`                                                              |
| OneToOneField   | ✅ Required                | `null=True, blank=True`                                                              |
| ManyToManyField | ❌ Create-এর সময় Optional | আলাদা `null=True` লাগে না; প্রয়োজনে `blank=True` validation-এর জন্য ব্যবহার করা হয় |

---

# Interview Example

```python
class Book(models.Model):

    title = models.CharField(max_length=100)

    author = models.ForeignKey(
        Author,
        on_delete=models.CASCADE
    )

    tags = models.ManyToManyField(Tag)
```

এই Model-এ

```python
Book.objects.create(
    title="Python"
)
```

কি হবে?

**Answer:**

❌ Error

কারণ

```python
author
```

Required।

কিন্তু

```python
tags
```

দিতে হবে না।

---

# Real Project Example (E-commerce)

```python
class Product(models.Model):

    category = models.ForeignKey(Category)

    seller = models.ForeignKey(User)

    tags = models.ManyToManyField(Tag)

    brand = models.ForeignKey(
        Brand,
        null=True,
        blank=True
    )
```

Create করার সময়:

| Field      | Required? | Reason                                       |
| ---------- | --------- | -------------------------------------------- |
| `category` | ✅ Yes     | ForeignKey, `null=False`                     |
| `seller`   | ✅ Yes     | ForeignKey, `null=False`                     |
| `tags`     | ❌ No      | ManyToMany পরে `.set()` বা `.add()` করা যায় |
| `brand`    | ❌ No      | `null=True`, `blank=True`                    |

---

# Professional Tip (Production)

DRF-এ **Model-এর `null`/`blank`** এবং **Serializer-এর `required`** এক জিনিস নয়।

উদাহরণ:

```python
class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
```

কিন্তু Serializer-এ চাইলে আপনি এটিকে optional করতে পারেন:

```python
class ProductSerializer(serializers.ModelSerializer):
    category = serializers.PrimaryKeyRelatedField(
        queryset=Category.objects.all(),
        required=False
    )

    class Meta:
        model = Product
        fields = "__all__"
```

এখানে API validation category না চাইলেও, **database save করার সময়** যদি category-এর অন্য কোনো value (যেমন `perform_create()`-এ `serializer.save(category=...)`) না দেন, তাহলে আবার database error হবে।

**অর্থাৎ:**

* **Model** ঠিক করে Database কী accept করবে।
* **Serializer** ঠিক করে API Client কী পাঠাবে।
* **View (`perform_create`, `perform_update`)** চাইলে missing relationship নিজে assign করতে পারে।

এটাই Production DRF-এর সবচেয়ে গুরুত্বপূর্ণ pattern।

------------

	এটি Django-এর **design decision** এবং Interview-তে খুব common প্রশ্ন।

**সংক্ষিপ্ত উত্তর:**

> **ManyToManyField create-এর সময় optional কারণ relationship আলাদা একটি intermediate (join) table-এ save হয়। Parent object save হওয়ার আগে সেই relationship তৈরি করা সম্ভব নয়।**

এখন বিস্তারিত বুঝি।

---

# Database Structure

ধরি Model

```python
class Subject(models.Model):
    name = models.CharField(max_length=100)


class Student(models.Model):
    name = models.CharField(max_length=100)

    subjects = models.ManyToManyField(Subject)
```

Database-এ Django **৩টি Table** তৈরি করবে।

## Student Table

| id | name  |
| -- | ----- |
| 1  | Rahim |

---

## Subject Table

| id | name    |
| -- | ------- |
| 1  | Math    |
| 2  | Physics |

---

## Intermediate Table (Automatically Created)

```text
student_subjects
```

| student_id | subject_id |
| ---------- | ---------- |
| 1          | 1          |
| 1          | 2          |

এই তৃতীয় table-এই relationship save হয়।

---

# Create করার সময় কী হয়?

আপনি লিখলেন

```python
student = Student.objects.create(
    name="Rahim"
)
```

Django প্রথমে

```sql
INSERT INTO student(name)

VALUES ('Rahim');
```

করবে।

Database

| id | name  |
| -- | ----- |
| 1  | Rahim |

এখন Student-এর ID পাওয়া গেল।

---

এরপর আপনি লিখলেন

```python
student.subjects.add(math)
```

Django এখন

```sql
INSERT INTO student_subjects

(student_id, subject_id)

VALUES

(1,1);
```

করতে পারবে।

---

# যদি Student Save-ই না হয়?

ধরি

```python
student = Student(
    name="Rahim"
)
```

এখনও

```python
student.save()
```

করেননি।

এখন

```python
student.subjects.add(math)
```

করলে?

❌ Error

কারণ

```text
student.id

==

None
```

Intermediate Table-এ

```text
student_id
```

দেওয়ার মতো কোনো value নেই।

---

Flow

```text
Student Object

↓

ID নেই

↓

ManyToMany Save করা অসম্ভব
```

---

# তাই Django Design করেছে

প্রথমে

```text
Student Save
```

তারপর

```text
ManyToMany Save
```

---

Diagram

```text
Student()

      │

      ▼

save()

      │

      ▼

Student ID = 5

      │

      ▼

subjects.add()

      │

      ▼

Intermediate Table
```

---

# ForeignKey-এর ক্ষেত্রে কেন Required?

ForeignKey থাকে

```python
class Student(models.Model):

    department = models.ForeignKey(Department)
```

Database

Student Table

| id | name | department_id |
| -- | ---- | ------------- |

এখানে

```text
department_id
```

Student Table-এর column।

Student Save করার সময়ই

```text
department_id
```

লাগবে।

তাই Required।

---

Flow

```text
Student Save

↓

department_id লাগবে

↓

না দিলে Error
```

---

# ManyToMany-এর ক্ষেত্রে

Student Table

| id | name |
| -- | ---- |

এখানে

```text
subjects
```

column-ই নেই।

Relationship

অন্য Table-এ।

তাই

Student Save করার সময়

Subjects লাগে না।

---

# Real Example

ধরি

একজন Student

১০টা Subject পড়তে পারে।

আজ Student Create করলেন।

```python
student = Student.objects.create(
    name="Rahim"
)
```

আজ কোনো Subject assign করলেন না।

আগামী সপ্তাহে

```python
student.subjects.add(math)
```

আরও পরে

```python
student.subjects.add(physics)
```

আরও পরে

```python
student.subjects.remove(math)
```

সবই সম্ভব।

---

# যদি ManyToMany Required হতো?

তাহলে

Student Create করার আগেই

```text
Student ID
```

দরকার হতো।

কিন্তু

ID তখনও তৈরি হয়নি।

এটা logical contradiction।

---

# তাহলে `blank=False` কেন আছে?

অনেকে বলেন,

```python
subjects = models.ManyToManyField(
    Subject,
    blank=False
)
```

তাহলে কি Required?

উত্তর:

**Form/Admin validation-এর জন্য Required।**

Admin Panel-এ Subject না দিলে validation error হবে।

কিন্তু Database level-এ ManyToMany relation **Parent object save হওয়ার পরে**-ই তৈরি হয়।

---

# DRF Serializer-এ

```python
class StudentSerializer(ModelSerializer):

    class Meta:
        model = Student
        fields = "__all__"
```

Request

```json
{
    "name":"Rahim",
    "subjects":[1,2]
}
```

Serializer কী করে?

```text
is_valid()

↓

Student Save

↓

student.subjects.set([1,2])

↓

Done
```

খেয়াল করুন, Serializer-ও **প্রথমে Student save করে**, তারপর ManyToMany relation সেট করে।

---

# Interview Answer (Professional)

**প্রশ্ন:** *"ManyToManyField create-এর সময় optional কেন?"*

**উত্তর:**

> "কারণ ManyToMany relationship model-এর নিজস্ব table-এ নয়, একটি আলাদা join/intermediate table-এ সংরক্ষিত হয়। সেই join table-এ record তৈরি করতে parent object-এর primary key প্রয়োজন। তাই Django প্রথমে parent object save করে primary key তৈরি করে, এরপর ManyToMany relationship insert করে। এই কারণেই ManyToManyField create-এর সময় defaultভাবে optional আচরণ করে।"

---

## Professional Tip

একটি ছোট টেবিল মনে রাখুন:

| Relationship      | Data কোথায় Save হয়?                    | Create-এর সময় Required?     |
| ----------------- | ---------------------------------------- | ---------------------------- |
| `ForeignKey`      | Parent table-এর column (`department_id`) | ✅ Yes                        |
| `OneToOneField`   | Parent table-এর column (`user_id`)       | ✅ Yes                        |
| `ManyToManyField` | আলাদা join/intermediate table            | ❌ No (relation পরে save হয়) |

**এটাই মূল কারণ** কেন `ManyToManyField`-এর আচরণ অন্য relational field-এর থেকে আলাদা।

-------
