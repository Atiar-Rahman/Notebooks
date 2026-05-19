
# Function Based View → APIView → ViewSet → ModelViewSet
👉 **kivabe data access korba (request, user, params, etc.)**

---

# 🧠 0. Common Idea (IMPORTANT)

👉 Django REST e sob view e same jinis access kora jai:

| Data         | Access                 |
| ------------ | ---------------------- |
| Body data    | `request.data`         |
| Query params | `request.query_params` |
| User         | `request.user`         |
| URL param    | `pk / kwargs`          |
| Headers      | `request.headers`      |

---

# 🔰 1. Function Based View (FBV)

👉 Basic + manual

```python id="fbv1"
from rest_framework.decorators import api_view
from rest_framework.response import Response
from contact.models import Contact
from contact.serialisers import ContactSerializer

@api_view(['GET', 'POST'])
def contact_view(request):

    # 📥 GET data
    if request.method == 'GET':
        contacts = Contact.objects.all()
        serializer = ContactSerializer(contacts, many=True)
        return Response(serializer.data)

    # 📤 POST data
    if request.method == 'POST':
        print(request.data)  # 🔥 data access

        serializer = ContactSerializer(data=request.data)

        if serializer.is_valid():
            user = request.user if request.user.is_authenticated else None
            serializer.save(user=user)

            return Response(serializer.data)

        return Response(serializer.errors)
```

---

# 🔥 Data Access in FBV

```python id="fbv2"
request.data              # body
request.query_params      # ?id=1
request.user              # logged user
request.headers           # headers
```

---

# ⚙️ 2. APIView (Class Based)

👉 More control, cleaner

```python id="apiview1"
from rest_framework.views import APIView
from rest_framework.response import Response

class ContactAPIView(APIView):

    def get(self, request):
        email = request.query_params.get('email')  # 🔥 query param

        contacts = Contact.objects.all()
        serializer = ContactSerializer(contacts, many=True)

        return Response(serializer.data)

    def post(self, request):
        print(request.data)        # 🔥 body
        print(request.user)        # 🔥 user

        serializer = ContactSerializer(data=request.data)

        if serializer.is_valid():
            serializer.save(user=request.user if request.user.is_authenticated else None)
            return Response(serializer.data)

        return Response(serializer.errors)
```

---

# 🔥 Data Access in APIView

Same as FBV but inside class:

```python id="apiview2"
request.data
request.user
request.query_params
request.headers
```

---

# ⚡ 3. ViewSet

👉 group multiple actions (list, create, retrieve)

```python id="viewset1"
from rest_framework.viewsets import ViewSet

class ContactViewSet(ViewSet):

    def list(self, request):
        contacts = Contact.objects.all()
        serializer = ContactSerializer(contacts, many=True)
        return Response(serializer.data)

    def create(self, request):
        print(request.data)  # 🔥 data

        serializer = ContactSerializer(data=request.data)

        if serializer.is_valid():
            serializer.save(user=request.user)
            return Response(serializer.data)

        return Response(serializer.errors)
```

---

# 🔥 Data Access in ViewSet

```python id="viewset2"
request.data
request.user
request.query_params
self.kwargs   # URL param
```

---

# 🚀 4. ModelViewSet (MOST USED 🔥)

👉 automatic CRUD + override when needed

```python id="modelvs1"
from rest_framework.viewsets import ModelViewSet

class ContactModelViewSet(ModelViewSet):
    queryset = Contact.objects.all()
    serializer_class = ContactSerializer
```

👉 but data access korte hole override korte hobe 👇

---

## 🔥 Important Methods

### ✅ 1. get_queryset()

```python id="modelvs2"
def get_queryset(self):
    user = self.request.user

    if user.is_staff:
        return Contact.objects.all()

    return Contact.objects.filter(user=user)
```

---

### ✅ 2. perform_create()

```python id="modelvs3"
def perform_create(self, serializer):
    print(self.request.data)   # 🔥 body
    print(self.request.user)   # 🔥 user

    serializer.save(user=self.request.user)
```

---

### ✅ 3. create() (full control)

```python id="modelvs4"
def create(self, request, *args, **kwargs):
    print(request.data)

    return super().create(request, *args, **kwargs)
```

---

### ✅ 4. URL param

```python id="modelvs5"
def retrieve(self, request, *args, **kwargs):
    pk = self.kwargs.get('pk')
    print(pk)
    return super().retrieve(request, *args, **kwargs)
```

---

# 🎯 FULL COMPARISON

| Feature   | FBV     | APIView | ViewSet       | ModelViewSet    |
| --------- | ------- | ------- | ------------- | --------------- |
| Control   | 🔥 Full | 🔥 Full | Medium        | Medium          |
| Code      | More    | Medium  | Less          | Very less       |
| CRUD auto | ❌       | ❌       | ❌             | ✅               |
| Best for  | Simple  | Custom  | grouped logic | production CRUD |

---

# 🧠 FINAL UNDERSTANDING

👉 sob jaygay same data access:

```python id="final1"
request.data          # POST/PUT body
request.user          # JWT user
request.query_params  # URL query
request.headers       # headers
self.kwargs           # URL param (class based)
```

---


 
# **complete CRUD + data access** dekhai ekta example diye (Contact API)

Ami 4 ta style e dekhabo:

👉 FBV
👉 APIView
👉 ViewSet
👉 ModelViewSet

And sab gula te use korbo:
**GET, POST, PUT, PATCH, DELETE**

---

# 🧱 Example Model (same for all)

```python
class Contact(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    message = models.TextField()
```

---

# 🔰 1. Function Based View (FBV)

```python id="fbv_full"
from rest_framework.decorators import api_view
from rest_framework.response import Response
from contact.models import Contact
from contact.serialisers import ContactSerializer

@api_view(['GET', 'POST', 'PUT', 'PATCH', 'DELETE'])
def contact_view(request, pk=None):

    # 🔍 GET (list or single)
    if request.method == 'GET':
        if pk:
            contact = Contact.objects.get(id=pk)
            serializer = ContactSerializer(contact)
        else:
            contacts = Contact.objects.all()
            serializer = ContactSerializer(contacts, many=True)

        return Response(serializer.data)

    # ➕ POST
    if request.method == 'POST':
        print(request.data)  # 🔥 data access

        serializer = ContactSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # 🔄 PUT (full update)
    if request.method == 'PUT':
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # ⚡ PATCH (partial update)
    if request.method == 'PATCH':
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # ❌ DELETE
    if request.method == 'DELETE':
        contact = Contact.objects.get(id=pk)
        contact.delete()
        return Response({"message": "Deleted"})
```

---

# ⚙️ 2. APIView (Class Based)

```python id="apiview_full"
from rest_framework.views import APIView
from rest_framework.response import Response

class ContactAPIView(APIView):

    # 🔍 GET
    def get(self, request, pk=None):
        if pk:
            contact = Contact.objects.get(id=pk)
            serializer = ContactSerializer(contact)
        else:
            contacts = Contact.objects.all()
            serializer = ContactSerializer(contacts, many=True)

        return Response(serializer.data)

    # ➕ POST
    def post(self, request):
        print(request.data)  # 🔥

        serializer = ContactSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # 🔄 PUT
    def put(self, request, pk):
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # ⚡ PATCH
    def patch(self, request, pk):
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # ❌ DELETE
    def delete(self, request, pk):
        contact = Contact.objects.get(id=pk)
        contact.delete()
        return Response({"message": "Deleted"})
```

---

# ⚡ 3. ViewSet

```python id="viewset_full"
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response

class ContactViewSet(ViewSet):

    # GET list
    def list(self, request):
        contacts = Contact.objects.all()
        serializer = ContactSerializer(contacts, many=True)
        return Response(serializer.data)

    # GET single
    def retrieve(self, request, pk=None):
        contact = Contact.objects.get(id=pk)
        serializer = ContactSerializer(contact)
        return Response(serializer.data)

    # POST
    def create(self, request):
        print(request.data)

        serializer = ContactSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # PUT
    def update(self, request, pk=None):
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # PATCH
    def partial_update(self, request, pk=None):
        contact = Contact.objects.get(id=pk)

        serializer = ContactSerializer(contact, data=request.data, partial=True)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors)

    # DELETE
    def destroy(self, request, pk=None):
        contact = Contact.objects.get(id=pk)
        contact.delete()
        return Response({"message": "Deleted"})
```

---

# 🚀 4. ModelViewSet (BEST 🔥)

👉 automatic sob method already ache

```python id="modelvs_full"
from rest_framework.viewsets import ModelViewSet

class ContactModelViewSet(ModelViewSet):
    queryset = Contact.objects.all()
    serializer_class = ContactSerializer
```

---

## 🔥 Override for data access

```python id="modelvs_override"
# POST
def perform_create(self, serializer):
    print(self.request.data)
    serializer.save()

# GET filter
def get_queryset(self):
    email = self.request.query_params.get('email')

    if email:
        return Contact.objects.filter(email=email)

    return Contact.objects.all()

# PUT/PATCH
def update(self, request, *args, **kwargs):
    print(request.data)
    return super().update(request, *args, **kwargs)

# DELETE
def destroy(self, request, *args, **kwargs):
    print("Deleting...")
    return super().destroy(request, *args, **kwargs)
```

---

# 🎯 FINAL SUMMARY

| Method | FBV      | APIView  | ViewSet          | ModelViewSet |
| ------ | -------- | -------- | ---------------- | ------------ |
| GET    | if block | get()    | list/retrieve    | auto         |
| POST   | if block | post()   | create()         | auto         |
| PUT    | if block | put()    | update()         | auto         |
| PATCH  | if block | patch()  | partial_update() | auto         |
| DELETE | if block | delete() | destroy()        | auto         |

---

# 🧠 SUPER IMPORTANT

👉 sob jaygay same:

```python
request.data          # POST body
request.user          # JWT user
request.query_params  # ?id=1
self.kwargs           # pk
```

---

# 🚀 Final Advice

👉 Beginner → FBV
👉 Intermediate → APIView
👉 Production → ModelViewSet 🔥

---

# Complete Crud Example with Student Model 

---

# 🔹 1. Model (আগেরটাই use করবো)

```python
# models.py
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    phone = models.CharField(max_length=15)
    address = models.TextField()
    age = models.IntegerField()
    gender = models.CharField(max_length=10)
    dob = models.DateField()
    description = models.TextField()
    status = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

---

# 🔹 2. Serializer

```python
# serializers.py
from rest_framework import serializers
from .models import Student

class StudentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Student
        fields = '__all__'
```

---

# 🔹 3. ViewSet (🔥 Main Part)

```python
# views.py
from rest_framework import viewsets
from .models import Student
from .serializers import StudentSerializer

class StudentViewSet(viewsets.ModelViewSet):
    queryset = Student.objects.all().order_by('-created_at')
    serializer_class = StudentSerializer
```

👉 এই একটা class দিয়েই তুমি পাচ্ছো:

* Create ✅
* List ✅
* Retrieve ✅
* Update ✅
* Delete ✅

---

# 🔹 4. Router (Auto URL Generate করবে)

```python
# urls.py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import StudentViewSet

router = DefaultRouter()
router.register(r'students', StudentViewSet)

urlpatterns = [
    path('api/', include(router.urls)),
]
```

---

# 🔥 Final API Endpoints (Auto তৈরি হবে)

| Method | URL                 | কাজ         |
| ------ | ------------------- | ----------- |
| GET    | /api/students/      | List        |
| POST   | /api/students/      | Create      |
| GET    | /api/students/{id}/ | Single Data |
| PUT    | /api/students/{id}/ | Update      |
| DELETE | /api/students/{id}/ | Delete      |

---

# 🔹 5. Custom Behavior (Optional 🔥)

### 👉 Search + Filter add করতে চাইলে

```python
from rest_framework import filters

class StudentViewSet(viewsets.ModelViewSet):
    queryset = Student.objects.all()
    serializer_class = StudentSerializer

    filter_backends = [filters.SearchFilter]
    search_fields = ['name', 'email']
```

---

### 👉 Only Active Data দেখাতে চাইলে

```python
def get_queryset(self):
    return Student.objects.filter(status=True)
```

---

### 👉 Custom Create Logic

```python
def perform_create(self, serializer):
    serializer.save()
```

---

# 🧠 Important Concept

👉 `ModelViewSet` =
`List + Create + Retrieve + Update + Destroy` (all-in-one)

👉 Router = automatic URL generator (manual URL লিখতে হয় না)

---

# 🚀 Pro Tips (Interview + Real Project)

* `select_related()` / `prefetch_related()` use করো performance এর জন্য
* Pagination add করো
* Permission add করো (IsAuthenticated)

---


# 🔹 1. ViewSet (Manual CRUD Implementation)

```python
# views.py
from rest_framework import viewsets, status
from rest_framework.response import Response
from .models import Student
from .serializers import StudentSerializer


class StudentViewSet(viewsets.ViewSet):

    # ✅ GET /students/
    def list(self, request):
        queryset = Student.objects.all()
        serializer = StudentSerializer(queryset, many=True)
        return Response(serializer.data)

    # ✅ POST /students/
    def create(self, request):
        serializer = StudentSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    # ✅ GET /students/{id}/
    def retrieve(self, request, pk=None):
        try:
            student = Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return Response({"error": "Not found"}, status=404)

        serializer = StudentSerializer(student)
        return Response(serializer.data)

    # ✅ PUT /students/{id}/
    def update(self, request, pk=None):
        try:
            student = Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return Response({"error": "Not found"}, status=404)

        serializer = StudentSerializer(student, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=400)

    # ✅ DELETE /students/{id}/
    def destroy(self, request, pk=None):
        try:
            student = Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return Response({"error": "Not found"}, status=404)

        student.delete()
        return Response({"message": "Deleted successfully"}, status=204)
```

---

# 🔹 2. Router Setup

```python
# urls.py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from .views import StudentViewSet

router = DefaultRouter()
router.register(r'students', StudentViewSet, basename='student')

urlpatterns = [
    path('api/', include(router.urls)),
]
```

---

# 🔥 Final API Endpoints

| Method | URL                 | Method Name |
| ------ | ------------------- | ----------- |
| GET    | /api/students/      | list        |
| POST   | /api/students/      | create      |
| GET    | /api/students/{id}/ | retrieve    |
| PUT    | /api/students/{id}/ | update      |
| DELETE | /api/students/{id}/ | destroy     |

---

# 🔥 Key Difference (Important)

| Feature | ViewSet         | ModelViewSet |
| ------- | --------------- | ------------ |
| Logic   | Manual লিখতে হয় | Auto         |
| Control | বেশি 🔥         | কম           |
| Code    | বেশি            | কম           |

👉 **ViewSet = full control (interview favourite)**
👉 **ModelViewSet = fast development (real project)**

---

# 🔥 Bonus (Clean Code Version using helper function)

```python
def get_object(self, pk):
    try:
        return Student.objects.get(pk=pk)
    except Student.DoesNotExist:
        return None
```

Use it:

```python
student = self.get_object(pk)
if not student:
    return Response({"error": "Not found"}, status=404)
```

---

তুমি শুরু করছো:

```python
class StudentDetailsViewset(ViewSet):
    student =
```



# ✅ Complete `StudentDetailsViewset` (Best Practice)

```python
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response
from rest_framework import status
from .models import Student
from .serializers import StudentSerializer


class StudentDetailsViewset(ViewSet):

    # 🔹 helper function (BEST PRACTICE)
    def get_object(self, pk):
        try:
            return Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return None

    # ✅ GET single student
    def retrieve(self, request, pk=None):
        student = self.get_object(pk)
        if not student:
            return Response({"error": "Not found"}, status=404)

        serializer = StudentSerializer(student)
        return Response(serializer.data)

    # ✅ UPDATE student
    def update(self, request, pk=None):
        student = self.get_object(pk)
        if not student:
            return Response({"error": "Not found"}, status=404)

        serializer = StudentSerializer(student, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)

        return Response(serializer.errors, status=400)

    # ✅ DELETE student
    def destroy(self, request, pk=None):
        student = self.get_object(pk)
        if not student:
            return Response({"error": "Not found"}, status=404)

        student.delete()
        return Response({"message": "Deleted"}, status=204)
```

---

# 🔥 তুমি যে ভুলটা করতে যাচ্ছিলে

```python
student =
```

👉 এটা সাধারণত use করা হয় না ViewSet-এ
👉 Instead use:

* `queryset` (ModelViewSet হলে)
* `get_object()` (ViewSet হলে) ✅

---

# 🔹 URL Setup (Important)

```python
router.register(r'students', StudentDetailsViewset, basename='student')
```

---

# 🔥 Pro Tip

👉 যদি তুমি শুধু details (retrieve/update/delete) handle করতে চাও,
তাহলে `list()` / `create()` না দিলেও কাজ করবে।

---

# **custom endpoint** শিখতে চাচ্ছো — এটা real project + interview দুই জায়গাতেই খুব important।

আমরা বানাবো:
👉 `/students/{id}/activate/`

---

# 🔹 Concept

👉 DRF-এ custom endpoint বানাতে `@action` decorator use করা হয়

* `detail=True` → specific object (id লাগবে)
* `methods=['post']` → POST request

---

# ✅ Full Example (ViewSet with custom endpoint)

```python id="l9r1qg"
from rest_framework.viewsets import ViewSet
from rest_framework.response import Response
from rest_framework.decorators import action
from rest_framework import status
from .models import Student
from .serializers import StudentSerializer


class StudentViewSet(ViewSet):

    def get_object(self, pk):
        try:
            return Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return None

    # 🔹 Custom Endpoint: Activate Student
    @action(detail=True, methods=['post'])
    def activate(self, request, pk=None):
        student = self.get_object(pk)
        if not student:
            return Response({"error": "Not found"}, status=404)

        student.status = True
        student.save()

        return Response({
            "message": "Student activated successfully",
            "id": student.id,
            "status": student.status
        })
```

---

# 🔥 Auto Generated URL

```
POST /api/students/{id}/activate/
```

👉 Example:

```
POST /api/students/5/activate/
```

---

# 🔹 Deactivate Endpoint (Bonus 🔥)

```python id="sfdbz3"
@action(detail=True, methods=['post'])
def deactivate(self, request, pk=None):
    student = self.get_object(pk)
    if not student:
        return Response({"error": "Not found"}, status=404)

    student.status = False
    student.save()

    return Response({"message": "Student deactivated"})
```

---

# 🔥 Router (same থাকবে)

```python id="04pynv"
router.register(r'students', StudentViewSet, basename='student')
```

---

# 🔹 React / Postman থেকে Call

👉 POST request দাও:

```
/api/students/1/activate/
```

---

# 🧠 Important Notes

* `@action` না দিলে custom URL তৈরি হবে না ❌
* `detail=True` মানে object-level API
* `detail=False` দিলে list-level API হয়

---

# 🔥 Example (List Level Custom Endpoint)

```python id="6r6qgp"
@action(detail=False, methods=['get'])
def active_students(self, request):
    students = Student.objects.filter(status=True)
    serializer = StudentSerializer(students, many=True)
    return Response(serializer.data)
```

👉 URL:

```
GET /api/students/active_students/
```

---


#  **তুমি যত খুশি `@action` create করতে পারো** — DRF-এ এর কোনো fixed limit নেই।

কিন্তু… 😏 **real project-এ unlimited না, structured way-এ করতে হয়**। আমি explain করছি 👇

---

# ✅ Unlimited Actions — Example

```python
from rest_framework.viewsets import ViewSet
from rest_framework.decorators import action
from rest_framework.response import Response
from .models import Student


class StudentViewSet(ViewSet):

    def get_object(self, pk):
        try:
            return Student.objects.get(pk=pk)
        except Student.DoesNotExist:
            return None

    @action(detail=True, methods=['post'])
    def activate(self, request, pk=None):
        return Response({"msg": "activate"})

    @action(detail=True, methods=['post'])
    def deactivate(self, request, pk=None):
        return Response({"msg": "deactivate"})

    @action(detail=True, methods=['post'])
    def promote(self, request, pk=None):
        return Response({"msg": "promote"})

    @action(detail=True, methods=['post'])
    def suspend(self, request, pk=None):
        return Response({"msg": "suspend"})
```

👉 সবগুলো আলাদা endpoint হবে:

```
POST /students/{id}/activate/
POST /students/{id}/deactivate/
POST /students/{id}/promote/
POST /students/{id}/suspend/
```

---

# ⚠️ But Important Rules (Very Important)

## ❌ 1. Random action বানানো যাবে না

👉 Bad:

* `doSomething()`
* `randomAction()`

👉 Good:

* `activate`
* `approve`
* `cancel`
* `publish`

---

## ❌ 2. Too many actions = bad design

👉 যদি 10+ action লাগে, তাহলে:
👉 তুমি **ViewSet wrong design করছো** ❌

---

# 🔥 Best Practice (Senior Level)

## 👉 Rule:

* **CRUD → ViewSet**
* **Business Logic → Service Layer / Separate API**

---

## 🔹 Clean Example

```python
@action(detail=True, methods=['post'])
def activate(self, request, pk=None):
    ...
```

✔️ valid
✔️ clear
✔️ RESTful

---

## 🔥 Advanced Trick (Dynamic Action ⚡)

```python
@action(detail=True, methods=['post'], url_path='change-status')
def change_status(self, request, pk=None):
    student = self.get_object(pk)
    status_value = request.data.get("status")

    student.status = status_value
    student.save()

    return Response({"status": student.status})
```

👉 URL:

```
POST /students/{id}/change-status/
```

👉 Body:

```json
{
  "status": true
}
```

🔥 এটা 1টা endpoint দিয়ে multiple কাজ করে

---

# 🧠 Summary

| Question                   | Answer               |
| -------------------------- | -------------------- |
| Unlimited action possible? | ✅ Yes                |
| Best practice?             | ❌ Limit & meaningful |
| When too many?             | ❌ Bad design         |
| Smart way?                 | ✅ Dynamic endpoint   |

---

# 🚀 Pro Tip (Interview Killer Answer 😎)

👉 বলবা:

> “Yes, we can create multiple custom actions using @action, but in production we should keep them minimal and meaningful, otherwise it violates REST design principles.”

---


* ✅ `permission_classes` per action
* ✅ `serializer_class` per action

---

# 🔹 1. `permission_classes` per action

👉 Default permission set করো class level-এ
👉 তারপর specific action-এ override করো

---

## ✅ Example

```python
from rest_framework.viewsets import ViewSet
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated, AllowAny, IsAdminUser

class StudentViewSet(ViewSet):

    # 🔹 default (সব action এ apply হবে)
    permission_classes = [IsAuthenticated]

    def list(self, request):
        return Response({"msg": "only logged in users"})

    # 🔥 custom permission (override)
    @action(detail=True, methods=['post'], permission_classes=[IsAdminUser])
    def activate(self, request, pk=None):
        return Response({"msg": "only admin can activate"})

    # 🔥 public endpoint
    @action(detail=False, methods=['get'], permission_classes=[AllowAny])
    def public_students(self, request):
        return Response({"msg": "anyone can see"})
```

---

# 🧠 Rule

| Level        | Priority   |
| ------------ | ---------- |
| action-level | 🔥 highest |
| class-level  | default    |

👉 action এ দিলে class-এরটা override হয়ে যায় ✅

---

# 🔹 2. `serializer_class` per action

👉 ViewSet-এ default serializer define করো
👉 তারপর `get_serializer_class()` override করো

---

## ✅ Example

```python
from .serializers import StudentSerializer, StudentActivateSerializer

class StudentViewSet(ViewSet):

    def get_serializer_class(self):
        if self.action == 'activate':
            return StudentActivateSerializer
        return StudentSerializer
```

---

## 🔥 Custom Serializer Example

```python
# serializers.py

from rest_framework import serializers

class StudentActivateSerializer(serializers.Serializer):
    confirm = serializers.BooleanField()
```

---

## 🔹 Use in action

```python
@action(detail=True, methods=['post'])
def activate(self, request, pk=None):
    serializer = self.get_serializer(data=request.data)
    serializer.is_valid(raise_exception=True)

    return Response({"msg": "activated"})
```

---

# 🔥 Full Combined Example (Best Practice)

```python
class StudentViewSet(ViewSet):

    permission_classes = [IsAuthenticated]

    def get_serializer_class(self):
        if self.action == 'activate':
            return StudentActivateSerializer
        return StudentSerializer

    @action(
        detail=True,
        methods=['post'],
        permission_classes=[IsAdminUser]
    )
    def activate(self, request, pk=None):
        serializer = self.get_serializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        return Response({"msg": "activated by admin"})
```

---

# 🚀 Pro Tips (Interview 🔥)

👉 বলবা:

> “I use action-level permission_classes for fine-grained access control and override get_serializer_class() to dynamically switch serializers per action.”

---

# ⚠️ Common Mistake

❌ এটা কাজ করবে না:

```python
@action(detail=True)
serializer_class = MySerializer   # ❌ WRONG
```

👉 always use `get_serializer_class()` ✅

---


# **can apply all HTTP methods** to a single DRF `@action`. The `methods` argument is just a list of allowed verbs. If you want truly **all standard methods**, you can list them all:

```python id="z6u0ox"
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import viewsets

class MyViewSet(viewsets.ViewSet):

    @action(detail=False, methods=['get', 'post', 'put', 'patch', 'delete', 'head', 'options', 'trace'])
    def custom_action(self, request):
        if request.method == 'GET':
            return Response({"message": "GET request"})
        elif request.method == 'POST':
            return Response({"message": "POST request"})
        elif request.method == 'PUT':
            return Response({"message": "PUT request"})
        elif request.method == 'PATCH':
            return Response({"message": "PATCH request"})
        elif request.method == 'DELETE':
            return Response({"message": "DELETE request"})
        elif request.method == 'HEAD':
            return Response({"message": "HEAD request"})
        elif request.method == 'OPTIONS':
            return Response({"message": "OPTIONS request"})
        elif request.method == 'TRACE':
            return Response({"message": "TRACE request"})
```

✅ Notes:

1. DRF will **only allow the methods you specify** in the list.
2. Commonly, people just use `['get', 'post', 'put', 'patch', 'delete']`. `'head'`, `'options'`, `'trace'` are rarely needed manually because DRF handles `OPTIONS` automatically.
3. Always check `request.method` inside your action to handle each type differently.


# **`GET` requests that don’t return a response**—this usually happens because of a **misconfiguration in DRF `@action`** or the view. Let me clarify why it happens and how to fix it.

---

### Common Reasons `GET` Returns Nothing in `@action`

1. **`methods` list missing `'get'`**

```python
@action(detail=False, methods=['post'])  # GET not allowed here
def my_action(self, request):
    return Response({"msg": "hello"})
```

* Solution: Make sure `'get'` is in the list:

```python
@action(detail=False, methods=['get', 'post'])
```

---

2. **Forgot to return a Response**

* DRF actions **must return a `Response` object**, otherwise nothing is sent back.

```python
@action(detail=False, methods=['get'])
def my_action(self, request):
    data = {"msg": "hello"}
    # ❌ forgot return
```

* Fix:

```python
return Response(data)  # ✅
```

---

3. **URL not correct**

* `detail=False` → list-level → URL is `/myviewset/my_action/`
* `detail=True` → object-level → URL is `/myviewset/<pk>/my_action/`

If you call the wrong URL for your action, you’ll get 404 or no response.

---

4. **Permission / Authentication Issues**

* If your `permission_classes` or `authentication_classes` block the request, DRF may return **empty response or 403/401**.

---

5. **Serializer / Query Issues**

* If you try to serialize a queryset but it’s empty and you return `serializer.data` without `many=True`, DRF may throw an error or return empty.

---

### Minimal Working Example of GET Action

```python
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import viewsets

class MyViewSet(viewsets.ViewSet):

    @action(detail=False, methods=['get'])
    def hello(self, request):
        return Response({"message": "GET works!"})
```

* URL (if using default router): `/myviewset/hello/`
* Should return: `{"message": "GET works!"}`

---

💡 **Tip:** Always check `curl` or Postman to confirm the correct URL and method.

---

**DRF @action template that works for all methods (GET/POST/PUT/PATCH/DELETE) and never returns empty**, so you can just plug in your logic.

