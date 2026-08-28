ঠিক আছে। তাহলে আমি তোমাকে **DRF Serializer Complete Course (Beginner → Advanced)** হিসেবে সাজিয়ে দিচ্ছি। এখানে শুধু Serializer syntax না, বরং **real-world API design mindset** শেখানো হবে।

# DRF Serializer Complete Course Roadmap

## Phase 1: Serializer Foundation (Beginner)

### Module 1: Serializer কেন দরকার?

শিখবে:

* API কীভাবে JSON exchange করে
* Serializer এর কাজ
* Serialization vs Deserialization
* JSON → Python
* Python → JSON

Example:

```
Database
    |
    ↓
Python Object
    |
    ↓
Serializer
    |
    ↓
JSON Response
```

---

### Module 2: Basic Serializer

শিখবে:

* serializers.Serializer
* Field types

Fields:

```python
CharField()
IntegerField()
BooleanField()
EmailField()
DateField()
DateTimeField()
DecimalField()
```

Practice:

Student API:

```json
{
"name":"Atiar",
"age":25,
"department":"CSE"
}
```

---

### Module 3: Serializer Validation

শিখবে:

* is_valid()
* validated_data
* errors
* required
* allow_null
* allow_blank

Example:

```python
name = serializers.CharField(
    min_length=3
)
```

---

### Module 4: Custom Validation

শিখবে:

Field validation:

```python
def validate_age(self,value):

    if value < 18:
        raise serializers.ValidationError(
            "Age must be 18+"
        )

    return value
```

Object validation:

```python
def validate(self,data):

    return data
```

---

# Phase 2: Model Serializer (Intermediate)

## Module 5: ModelSerializer

শিখবে:

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Product
        fields="__all__"
```

Topics:

* Meta class
* fields
* exclude
* read_only_fields

---

## Module 6: Serializer Create & Update

শিখবে:

POST request:

```json
{
"name":"Laptop",
"price":80000
}
```

কিভাবে database এ save হয়।

Methods:

```python
create()

update()
```

---

## Module 7: Serializer Field Options

শিখবে:

```python
read_only=True

write_only=True

required=False

default=

allow_null=True
```

Real example:

Password:

```python
password = serializers.CharField(
    write_only=True
)
```

---

# Phase 3: Relationship Serializer

## Module 8: ForeignKey Serializer

Example:

```
Category
    |
    |
 Product
```

Models:

```python
class Product(models.Model):

    category=models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

---

Learn:

* Primary Key Related Field
* String Related Field
* Nested Serializer

---

## Module 9: Nested Serializer

Example:

Response:

```json
{
"name":"Atiar",

"products":[

{
"name":"Laptop"
}

]

}
```

Learn:

* many=True
* depth
* custom nested serializer

---

## Module 10: OneToOne Relationship

Example:

```
User

 |

Profile
```

Learn:

* User profile API
* Nested update

---

## Module 11: ManyToMany Relationship

Example:

```
Student

 |

Courses
```

Learn:

* ManyToManyField
* Multiple objects handling

---

# Phase 4: Professional Serializer Design

## Module 12: Request Serializer vs Response Serializer

Professional API তে:

Input:

```json
{
"category_id":1
}
```

Output:

```json
{
"category":{
"id":1,
"name":"Laptop"
}
}
```

Learn:

* write_only
* read_only

---

## Module 13: SerializerMethodField

Example:

```python
total_price =
serializers.SerializerMethodField()
```

Output:

```json
{
"name":"Laptop",
"discount_price":70000
}
```

---

## Module 14: Dynamic Serializer

Different user:

Admin:

```json
{
"id":1,
"email":"a@gmail.com",
"role":"admin"
}
```

Normal:

```json
{
"id":1,
"name":"Atiar"
}
```

---

## Module 15: Custom Serializer Mixins

Learn:

* reusable serializer logic
* common fields

---

# Phase 5: Advanced API Serializer

## Module 16: User Serializer Design

Complete:

* Register serializer
* Login serializer
* Profile serializer
* Password change

---

## Module 17: Authentication Serializer

Learn:

* JWT token serializer
* Refresh token
* Custom claims

---

## Module 18: File Upload Serializer

Example:

```json
{
"profile_image":"image.png"
}
```

Learn:

* ImageField
* FileField
* Validation

---

## Module 19: Bulk Serializer

Example:

একসাথে:

```json
[
{
"name":"A"
},
{
"name":"B"
}
]
```

Learn:

* many=True
* bulk create

---

## Module 20: Serializer Performance

Professional topics:

* select_related()
* prefetch_related()
* N+1 query problem
* Serializer optimization

---

# Phase 6: Real Project Implementation

## Project 1: Blog API

Models:

```
User

Post

Category

Comment

Like
```

Serializer:

```
UserSerializer

PostSerializer

CommentSerializer

CategorySerializer
```

---

## Project 2: E-commerce API

Models:

```
User

Product

Category

Cart

Order

Payment
```

Advanced serializer:

* Nested data
* Order creation
* Cart calculation
* Product stock validation

---

# Phase 7: Interview Level Topics

শেষে শিখবে:

* Serializer vs ModelSerializer
* Serializer validation flow
* Nested serializer performance
* How to design API response
* Best practices
* Common mistakes

---

## Learning Order (তোমার জন্য)

তুমি যেহেতু Django + DRF already জানো, এই order follow করো:

```
Module 1-4
      ↓
Module 5-7
      ↓
Module 8-11
      ↓
Module 12-15
      ↓
Module 16-20
      ↓
Real Project
```

প্রতিটি module এ আমি দেব:

1. Concept explanation
2. Real API example
3. Code
4. Practice task
5. Interview questions

পরের থেকে শুরু করবো:

# Module 1: Serializer কেন দরকার + Serialization/Deserialization Deep Explanation + Real API Flow

(তারপর ধাপে ধাপে Module 20 পর্যন্ত যাবো)

---
# Module 1: Serializer কেন দরকার + Serialization / Deserialization Deep Explanation + Real API Flow

আজকে আমরা DRF Serializer-এর foundation শিখবো। Serializer ভালোভাবে না বুঝলে পরের সব advanced বিষয় (Nested Serializer, ModelSerializer, Validation) কঠিন লাগবে।

---

# 1. API আসলে কী করে?

ধরো তোমার Backend হলো Django এবং Frontend হলো React।

Architecture:

```
React Frontend
       |
       | JSON Request
       ↓
Django REST API
       |
       | Database Query
       ↓
PostgreSQL/MySQL
```

Frontend আর Backend একই language ব্যবহার করে না।

Example:

React:

```javascript
const user = {
    name:"Atiar",
    age:25
}
```

Python:

```python
user = {
    "name":"Atiar",
    "age":25
}
```

দুই জায়গায় data structure আলাদা।

তাই তাদের মধ্যে communication এর জন্য দরকার:

```
JSON Format
```

---

# 2. Serializer কেন দরকার?

ধরো Database থেকে User object পেলাম:

```python
user = User.objects.get(id=1)
```

এটা Django Model Object:

```python
User(
    id=1,
    name="Atiar",
    email="atiar@gmail.com"
)
```

কিন্তু React এটা বুঝবে না।

React চায়:

```json
{
    "id":1,
    "name":"Atiar",
    "email":"atiar@gmail.com"
}
```

এখন Model Object → JSON করতে হবে।

এই কাজ করে:

```
Serializer
```

Flow:

```
Django Model Object

        |
        |
        ↓

    Serializer

        |
        |
        ↓

       JSON
```

---

# 3. Serialization কী?

Serialization মানে:

> Python Object কে JSON এ convert করা।

Example:

Python Object:

```python
user = {
    "id":1,
    "name":"Atiar",
    "email":"atiar@gmail.com"
}
```

Serializer:

```
Python
   |
   ↓
Serializer
   |
   ↓
JSON
```

Output:

```json
{
    "id":1,
    "name":"Atiar",
    "email":"atiar@gmail.com"
}
```

এটাই Serialization।

---

# 4. Deserialization কী?

Reverse process:

> JSON কে Python Object এ convert করা।

Example:

Frontend থেকে request:

```json
{
    "name":"Rahim",
    "email":"rahim@gmail.com"
}
```

Django এটাকে সরাসরি ব্যবহার করতে পারে না।

Serializer convert করবে:

```
JSON

 ↓

Python Dictionary

 ↓

Database Object
```

Example:

```python
{
"name":"Rahim",
"email":"rahim@gmail.com"
}
```

তারপর:

```python
User.objects.create(
    name="Rahim",
    email="rahim@gmail.com"
)
```

---

# 5. Real API Flow বুঝি

ধরো User Profile API:

## GET Request

Frontend:

```
GET /api/profile/
```

---

Database:

```
User Table

id | name  | email
-------------------
1  | Atiar | a@gmail.com
```

Django:

```python
user = User.objects.get(id=1)
```

Result:

```
User Object
```

Serializer:

```python
UserSerializer(user)
```

Response:

```json
{
    "id":1,
    "name":"Atiar",
    "email":"a@gmail.com"
}
```

---

# 6. POST Request Flow

Frontend:

```
POST /api/users/
```

JSON:

```json
{
    "name":"Karim",
    "email":"karim@gmail.com",
    "password":"12345"
}
```

Django receive:

```python
request.data
```

Data:

```python
{
"name":"Karim",
"email":"karim@gmail.com",
"password":"12345"
}
```

Serializer:

```python
serializer = UserSerializer(
    data=request.data
)
```

Validation:

```python
serializer.is_valid()
```

Save:

```python
serializer.save()
```

Database:

```
User Table

id | name
---------
1  | Karim
```

---

# 7. Serializer না থাকলে কী সমস্যা?

ধরো Serializer নেই।

তাহলে তোমাকে নিজে করতে হবে:

```python
user = User.objects.get(id=1)

data = {
    "id":user.id,
    "name":user.name,
    "email":user.email
}
```

প্রতিটি Model এর জন্য একই code লিখতে হবে।

100টা Model হলে?

অনেক duplicate code।

Serializer এই কাজ automate করে।

---

# 8. Django REST Framework Serializer দুই ধরনের

## 1. Serializer

Manual control:

```python
class UserSerializer(
    serializers.Serializer
):
    
    name = serializers.CharField()
    email = serializers.EmailField()
```

তুমি সব নিজে define করবে।

---

## 2. ModelSerializer

Database Model থেকে automatic:

```python
class UserSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = User
        fields = "__all__"
```

DRF নিজে field তৈরি করবে।

---

# 9. Serializer এর মূল 4টি কাজ

একজন ভালো DRF developer হিসেবে Serializer দিয়ে:

## 1. Convert

```
Model → JSON
JSON → Model
```

---

## 2. Validate

Example:

Email ঠিক আছে কিনা:

```python
email="abc"
```

Reject করবে।

---

## 3. Transform

Database:

```python
first_name
last_name
```

Response:

```json
{
"name":"Atiar Rahman"
}
```

---

## 4. Control API Output

Database:

```
password
```

কিন্তু API:

```json
{
"name":"Atiar"
}
```

password hide করবে।

---

# 10. Real World Example

ধরো তোমার StayBangla Hotel Management System:

Models:

```
User

Hotel

Room

Booking
```

Frontend Room list চায়:

```json
[
{
"id":1,
"name":"Deluxe Room",
"price":5000
}
]
```

Database:

```
Room Object
```

Serializer:

```
RoomSerializer
```

Output:

```
JSON
```

এটাই পুরো API flow।

---

# Module 1 Summary

মনে রাখবে:

```
Database
   |
   ↓
Django Model
   |
   ↓
Serializer
   |
   ↓
JSON Response
   |
   ↓
Frontend
```

আর Create করার সময়:

```
Frontend
   |
   ↓
JSON
   |
   ↓
Serializer
   |
   ↓
Validation
   |
   ↓
Database
```

---

# Practice Task

1. একটি User JSON design করো:

```json
{
"name":"",
"email":"",
"age":""
}
```

2. চিন্তা করো:

* কোন field কোন type হবে?
* কোন field required হবে?
* কোন field hide করতে হবে?

পরের Module:

**Module 2: Basic Serializer + All Serializer Fields + First DRF API বানানো**

---

# Module 2: Basic Serializer + All Serializer Fields + First DRF API বানানো

Module 1 এ আমরা শিখেছি:

* Serializer কেন দরকার
* Serialization
* Deserialization
* API flow

এখন আমরা হাতে-কলমে **Basic Serializer** তৈরি করবো।

---

# 1. `serializers.Serializer` কী?

DRF-এ দুই ধরনের Serializer আছে:

```
1. serializers.Serializer
2. serializers.ModelSerializer
```

আজকে আমরা প্রথমটি শিখবো:

```python
serializers.Serializer
```

এখানে সব field আমাদের নিজে define করতে হয়।

---

# 2. Project Setup

ধরি আমাদের একটি Student API লাগবে।

JSON Structure:

```json
{
    "name": "Atiar",
    "email": "atiar@gmail.com",
    "age": 25,
    "is_active": true
}
```

আমাদের field:

| Field     | Type    |
| --------- | ------- |
| name      | String  |
| email     | Email   |
| age       | Integer |
| is_active | Boolean |

---

# 3. Serializer তৈরি করা

`serializers.py`

```python
from rest_framework import serializers


class StudentSerializer(serializers.Serializer):

    name = serializers.CharField()

    email = serializers.EmailField()

    age = serializers.IntegerField()

    is_active = serializers.BooleanField()
```

এখন Serializer JSON structure বুঝতে পারবে।

---

# 4. Field কীভাবে কাজ করে?

## CharField()

String data এর জন্য:

```python
name = serializers.CharField()
```

Valid:

```json
{
"name":"Atiar"
}
```

Invalid:

```json
{
"name":123
}
```

---

## IntegerField()

Number এর জন্য:

```python
age = serializers.IntegerField()
```

Valid:

```json
{
"age":25
}
```

Invalid:

```json
{
"age":"twenty"
}
```

---

## EmailField()

Email validation করে:

```python
email = serializers.EmailField()
```

Valid:

```json
{
"email":"test@gmail.com"
}
```

Invalid:

```json
{
"email":"hello"
}
```

---

## BooleanField()

True/False:

```python
is_active = serializers.BooleanField()
```

Valid:

```json
{
"is_active":true
}
```

---

# 5. আরো Important Serializer Fields

## DateField()

Date:

```python
birth_date = serializers.DateField()
```

JSON:

```json
{
"birth_date":"2000-01-20"
}
```

---

## DateTimeField()

Date + Time:

```python
created_at = serializers.DateTimeField()
```

JSON:

```json
{
"created_at":"2026-07-29T10:30:00"
}
```

---

## DecimalField()

Money / Price:

```python
price = serializers.DecimalField(
    max_digits=10,
    decimal_places=2
)
```

Example:

```json
{
"price":5000.50
}
```

---

## ChoiceField()

Fixed option:

```python
role = serializers.ChoiceField(
    choices=[
        "student",
        "teacher"
    ]
)
```

Valid:

```json
{
"role":"student"
}
```

Invalid:

```json
{
"role":"admin"
}
```

---

## ListField()

Array:

```python
skills = serializers.ListField()
```

JSON:

```json
{
"skills":[
    "Python",
    "Django",
    "React"
]
}
```

---

# 6. Optional Field তৈরি করা

Default ভাবে field required।

Example:

```python
name = serializers.CharField()
```

এটা চাইবে:

```json
{
"name":"Atiar"
}
```

---

কিন্তু optional করতে:

```python
name = serializers.CharField(
    required=False
)
```

এখন:

```json
{}
```

Allowed হবে।

---

# 7. allow_null

Null value allow:

```python
phone = serializers.CharField(
    allow_null=True
)
```

Allowed:

```json
{
"phone":null
}
```

---

# 8. allow_blank

Empty string allow:

```python
address = serializers.CharField(
    allow_blank=True
)
```

Allowed:

```json
{
"address":""
}
```

---

# 9. Read Only Field

কিছু field user পাঠাবে না।

Example:

id backend তৈরি করবে।

```python
id = serializers.IntegerField(
    read_only=True
)
```

Frontend:

```json
{
"name":"Atiar"
}
```

Response:

```json
{
"id":1,
"name":"Atiar"
}
```

---

# 10. Write Only Field

Password এর ক্ষেত্রে:

```python
password = serializers.CharField(
    write_only=True
)
```

Request:

```json
{
"password":"12345"
}
```

Response:

```json
{
"name":"Atiar"
}
```

Password দেখাবে না।

---

# 11. JSON থেকে Data Validate করা

ধরি:

```python
data = {
    "name":"Atiar",
    "email":"atiar@gmail.com",
    "age":25,
    "is_active":True
}
```

Serializer:

```python
serializer = StudentSerializer(
    data=data
)
```

Validation:

```python
serializer.is_valid()
```

Output:

```
True
```

---

Valid data:

```python
serializer.validated_data
```

Output:

```python
{
'name':'Atiar',
'email':'atiar@gmail.com',
'age':25,
'is_active':True
}
```

---

# 12. Invalid Data Example

```python
data = {

"name":"Atiar",

"email":"wrong",

"age":"abc"

}
```

Run:

```python
serializer.is_valid()
```

Output:

```
False
```

Errors:

```python
{
"email":[
"Enter a valid email address."
],

"age":[
"A valid integer is required."
]
}
```

---

# 13. First DRF API তৈরি

ধরি:

`views.py`

```python
from rest_framework.views import APIView
from rest_framework.response import Response

from .serializers import StudentSerializer


class StudentAPI(APIView):

    def post(self, request):

        serializer = StudentSerializer(
            data=request.data
        )


        if serializer.is_valid():

            return Response(
                serializer.validated_data
            )


        return Response(
            serializer.errors
        )
```

---

URL:

```python
urlpatterns = [

path(
"students/",
StudentAPI.as_view()
)

]
```

---

# 14. API Test

POST:

```
http://localhost:8000/students/
```

Body:

```json
{
"name":"Atiar",
"email":"atiar@gmail.com",
"age":25,
"is_active":true
}
```

Response:

```json
{
"name":"Atiar",
"email":"atiar@gmail.com",
"age":25,
"is_active":true
}
```

---

# 15. Real Project Example

তোমার StayBangla Hotel Project এ:

Room JSON:

```json
{
"name":"Deluxe Room",
"price":5000,
"available":true
}
```

Serializer:

```python
class RoomSerializer(serializers.Serializer):

    name = serializers.CharField()

    price = serializers.IntegerField()

    available = serializers.BooleanField()
```

এভাবেই JSON দেখে Serializer design করতে হয়।

---

# Module 2 Summary

আজকে শিখলে:

✅ `serializers.Serializer`

✅ Basic Fields

✅ Required/Optional Field

✅ read_only

✅ write_only

✅ Validation

✅ First API

পরের Module:

# Module 3: Serializer Validation Deep Dive

* Field Validation
* validate_<field>()
* validate()
* Custom Error Message
* Real Project Validation Pattern

----

# Module 3: Serializer Validation Deep Dive (DRF)

Module 2 এ আমরা শিখেছি:

* `serializers.Serializer`
* Field types
* `is_valid()`
* `validated_data`
* `errors`

এখন শিখবো **Serializer Validation**। Real project এ data save করার আগে validation সবচেয়ে গুরুত্বপূর্ণ অংশ।

---

# 1. Validation কেন দরকার?

Frontend থেকে data আসলে আমরা কখনো trust করি না।

ধরো User registration API:

Request:

```json
{
    "username":"atiar",
    "email":"wrong-email",
    "age":12,
    "password":"123"
}
```

সমস্যা:

* Email invalid
* Age কম
* Password ছোট

Database এ save করার আগে এগুলো আটকাতে হবে।

এই কাজ করে:

```
Request Data
      |
      ↓
Serializer Validation
      |
      ↓
Database Save
```

---

# 2. Validation Flow

DRF validation flow:

```
request.data

     ↓

Serializer(data=request.data)

     ↓

is_valid()

     ↓

Field Validation

     ↓

Custom Validation

     ↓

validate()

     ↓

validated_data

     ↓

save()
```

---

# 3. Built-in Field Validation

DRF অনেক validation আগে থেকেই দেয়।

Example:

```python
class UserSerializer(serializers.Serializer):

    username = serializers.CharField(
        min_length=3,
        max_length=20
    )

    email = serializers.EmailField()

    age = serializers.IntegerField(
        min_value=18
    )
```

---

Input:

```json
{
    "username":"a",
    "email":"hello",
    "age":15
}
```

Output:

```json
{
    "username":[
        "Ensure this field has at least 3 characters."
    ],

    "email":[
        "Enter a valid email address."
    ],

    "age":[
        "Ensure this value is greater than or equal to 18."
    ]
}
```

---

# 4. Common Field Validation Options

## required

Field অবশ্যই লাগবে:

```python
name = serializers.CharField(
    required=True
)
```

Request:

```json
{}
```

Error:

```json
{
"name":[
"This field is required."
]
}
```

---

## allow_null

None/null allow:

```python
phone = serializers.CharField(
    allow_null=True
)
```

Allowed:

```json
{
"phone":null
}
```

---

## allow_blank

Empty string allow:

```python
address = serializers.CharField(
    allow_blank=True
)
```

Allowed:

```json
{
"address":""
}
```

---

## max_length

```python
username = serializers.CharField(
    max_length=10
)
```

---

## min_length

```python
password = serializers.CharField(
    min_length=8
)
```

---

# 5. Field Level Custom Validation

অনেক সময় built-in validation যথেষ্ট না।

Example:

Requirement:

> Age অবশ্যই 18 এর বেশি হতে হবে।

Serializer:

```python
class UserSerializer(serializers.Serializer):

    name = serializers.CharField()

    age = serializers.IntegerField()


    def validate_age(self, value):

        if value < 18:

            raise serializers.ValidationError(
                "Age must be 18 or above"
            )

        return value
```

---

এখানে:

```
validate_
    +
field name
```

Pattern:

```python
validate_<field_name>()
```

---

Example:

Email validation:

```python
def validate_email(self,value):

    if value.endswith("@test.com"):

        raise serializers.ValidationError(
            "Test email is not allowed"
        )

    return value
```

---

# 6. Object Level Validation

কখনো একাধিক field একসাথে check করতে হয়।

Example:

Password এবং Confirm Password একই হতে হবে।

JSON:

```json
{
"password":"12345678",
"confirm_password":"123456"
}
```

এখানে শুধু password field check করলে হবে না।

---

Serializer:

```python
class RegisterSerializer(serializers.Serializer):

    password = serializers.CharField()

    confirm_password = serializers.CharField()


    def validate(self,data):

        if data["password"] != data["confirm_password"]:

            raise serializers.ValidationError(
                "Passwords do not match"
            )

        return data
```

---

Flow:

```
password
      |
confirm_password
      |
      ↓
validate()
```

---

# 7. Field Validation এবং Object Validation Difference

## Field Validation

একটা field:

Example:

```python
validate_age()
```

Check:

```
age only
```

---

## Object Validation

একাধিক field:

Example:

```python
validate()
```

Check:

```
password
confirm_password
```

---

# 8. Custom Error Message

Default:

```json
{
"email":[
"Enter a valid email address."
]
}
```

নিজের message:

```python
email = serializers.EmailField(
    error_messages={
        "invalid":
        "Please enter correct email"
    }
)
```

Output:

```json
{
"email":[
"Please enter correct email"
]
}
```

---

# 9. Multiple Validation Example

Real Registration Serializer:

```python
from rest_framework import serializers


class RegisterSerializer(serializers.Serializer):

    username = serializers.CharField(
        min_length=3
    )

    email = serializers.EmailField()

    age = serializers.IntegerField()

    password = serializers.CharField(
        min_length=8
    )


    def validate_age(self,value):

        if value < 18:

            raise serializers.ValidationError(
                "You must be adult"
            )

        return value


    def validate_username(self,value):

        if " " in value:

            raise serializers.ValidationError(
                "Username cannot contain space"
            )

        return value
```

---

# 10. Database Related Validation

ধরো email already exist:

Database:

```
User Table

id | email
---------
1  | a@gmail.com
```

Request:

```json
{
"email":"a@gmail.com"
}
```

Check:

```python
def validate_email(self,value):

    if User.objects.filter(
        email=value
    ).exists():

        raise serializers.ValidationError(
            "Email already exists"
        )

    return value
```

---

# 11. Validation কখন কাজ করে?

Important:

এটা কাজ করে:

```python
serializer.is_valid()
```

এটা না করলে:

```python
serializer.validated_data
```

পাওয়া যাবে না।

Example:

Wrong:

```python
serializer = UserSerializer(
    data=request.data
)

serializer.save()
```

Correct:

```python
serializer = UserSerializer(
    data=request.data
)


if serializer.is_valid():

    serializer.save()
```

---

# 12. Real Project Example (Hotel Booking)

Requirement:

একজন user future date এ booking করতে পারবে।

JSON:

```json
{
"check_in":"2026-07-20",
"check_out":"2026-07-15"
}
```

সমস্যা:

checkout আগে হয়ে গেছে।

Serializer:

```python
class BookingSerializer(serializers.Serializer):

    check_in = serializers.DateField()

    check_out = serializers.DateField()


    def validate(self,data):

        if data["check_out"] <= data["check_in"]:

            raise serializers.ValidationError(
                "Invalid booking date"
            )

        return data
```

---

# 13. Professional Validation Structure

Real project এ:

```
serializers.py

UserSerializer

    |
    |-- Field Validation
    |
    |-- Object Validation
    |
    |-- Database Check
    |
    |-- Custom Error
```

---

# Module 3 Summary

আজকে শিখলে:

✅ Built-in Validation
✅ Field Validation
✅ `validate_<field>()`
✅ Object Validation
✅ `validate()`
✅ Custom Error Message
✅ Database Validation
✅ Real Project Pattern

Practice Task:

একটি **ProductSerializer** বানাও:

JSON:

```json
{
"name":"Laptop",
"price":80000,
"discount":90000,
"stock":10
}
```

Validation:

1. price 0 এর কম হতে পারবে না
2. discount price এর চেয়ে বেশি হতে পারবে না
3. stock negative হতে পারবে না

পরের Module:

# Module 4: Serializer `create()` এবং `update()` Deep Dive

* কীভাবে Database এ save হয়
* Custom create method
* Custom update method
* User registration example
* Password hashing pattern

---
# Module 4: Serializer `create()` এবং `update()` Deep Dive

Module 3 এ আমরা শিখেছি:

* Field validation
* `validate_<field>()`
* `validate()`
* Custom validation

এখন শিখবো:

* Serializer দিয়ে Database এ data কীভাবে save হয়
* `create()`
* `update()`
* Custom save logic
* User registration example

---

# 1. Serializer এ Data Save Flow

যখন POST request আসে:

Frontend:

```json
{
    "name":"Atiar",
    "email":"atiar@gmail.com",
    "age":25
}
```

View:

```python
serializer = UserSerializer(
    data=request.data
)
```

Validation:

```python
serializer.is_valid()
```

তারপর:

```python
serializer.save()
```

এখন প্রশ্ন:

`save()` কী করে?

Answer:

Serializer এর ভিতরে:

```
save()
   |
   |
   ├── create()
   |
   └── update()
```

চলে।

---

# 2. create() কী?

`create()` ব্যবহার হয় যখন **নতুন object তৈরি করা হয়**।

Example:

POST request:

```json
{
    "name":"Atiar",
    "email":"atiar@gmail.com"
}
```

Database:

```
User Table

id | name   | email
--------------------
1  | Atiar  | atiar@gmail.com
```

---

# 3. Default create()

ধরো Model:

```python
class Student(models.Model):

    name = models.CharField(
        max_length=100
    )

    email = models.EmailField()

    age = models.IntegerField()
```

Serializer:

```python
from rest_framework import serializers


class StudentSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Student

        fields = "__all__"
```

এখানে DRF নিজে:

```python
Student.objects.create()
```

call করে।

---

# 4. Custom create() কেন দরকার?

Real project এ অনেক সময় extra কাজ করতে হয়।

Example:

User registration:

Request:

```json
{
    "username":"atiar",
    "password":"12345678"
}
```

কিন্তু password plain text এ database এ রাখা যাবে না।

তাই custom create দরকার।

---

# 5. Custom create() Example

Model:

```python
class User(models.Model):

    username = models.CharField(
        max_length=100
    )

    password = models.CharField(
        max_length=255
    )
```

Serializer:

```python
class UserSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = User

        fields = [
            "username",
            "password"
        ]


    def create(self, validated_data):

        user = User.objects.create(
            username=validated_data["username"],
            password=validated_data["password"]
        )

        return user
```

---

এখানে:

```python
validated_data
```

এর ভিতরে থাকে:

```python
{
"username":"atiar",
"password":"12345678"
}
```

---

# 6. Password Hashing Example

Django User হলে password কখনো direct save করা যাবে না।

Wrong:

```python
user.password = "123456"
```

Correct:

```python
user.set_password(
    validated_data["password"]
)
```

Example:

```python
def create(self, validated_data):

    user = User(
        username=validated_data["username"]
    )


    user.set_password(
        validated_data["password"]
    )


    user.save()


    return user
```

---

# 7. `update()` কী?

`update()` ব্যবহার হয় existing object modify করার জন্য।

Example:

Database:

```
User

id | name
---------
1  | Atiar
```

Request:

PUT:

```json
{
"name":"Atiar Rahman"
}
```

---

Serializer:

```python
def update(
    self,
    instance,
    validated_data
):

    instance.name = validated_data["name"]

    instance.save()

    return instance
```

---

# 8. update() এর ভিতরে কী থাকে?

দুইটা জিনিস:

## instance

আগের database object:

```python
instance = User(
    id=1,
    name="Atiar"
)
```

---

## validated_data

নতুন data:

```python
{
"name":"Atiar Rahman"
}
```

---

Flow:

```
Old Object
     +
New Data
     |
     ↓
update()
     |
     ↓
Database Updated
```

---

# 9. Partial Update (PATCH)

PUT:

সব field দিতে হয়।

Example:

```json
{
"name":"Atiar",
"email":"a@gmail.com",
"age":25
}
```

---

PATCH:

শুধু পরিবর্তিত field:

```json
{
"name":"Atiar Rahman"
}
```

---

View:

```python
serializer = UserSerializer(
    user,
    data=request.data,
    partial=True
)
```

---

# 10. create() এবং update() Difference

| Method   | কাজ                    |
| -------- | ---------------------- |
| create() | নতুন object তৈরি       |
| update() | পুরানো object পরিবর্তন |

---

Example:

```
POST
 |
 ↓
create()


PUT/PATCH
 |
 ↓
update()
```

---

# 11. Real Project Example: Hotel Booking

Model:

```python
class Booking(models.Model):

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    room = models.ForeignKey(
        Room,
        on_delete=models.CASCADE
    )

    total_price = models.IntegerField()
```

Frontend পাঠাবে:

```json
{
"room":5,
"days":3
}
```

কিন্তু database এ save হবে:

```json
{
"user":1,
"room":5,
"total_price":15000
}
```

এখানে custom create লাগবে।

---

Serializer:

```python
class BookingSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Booking

        fields = [
            "room",
            "days"
        ]


    def create(self, validated_data):

        user = self.context["request"].user


        booking = Booking.objects.create(
            user=user,
            room=validated_data["room"],
            total_price=5000 * validated_data["days"]
        )


        return booking
```

---

# 12. `context` কেন লাগে?

Serializer অনেক সময় request information চায়।

Example:

Current user:

```python
self.context["request"].user
```

View থেকে:

```python
serializer = BookingSerializer(
    data=request.data,
    context={
        "request":request
    }
)
```

---

# 13. create() এ Extra Validation

Example:

Stock check:

```python
def create(self, validated_data):

    product = validated_data["product"]


    if product.stock <= 0:

        raise serializers.ValidationError(
            "Product unavailable"
        )


    return Order.objects.create(
        **validated_data
    )
```

---

# 14. `**validated_data` কী?

ধরো:

```python
validated_data = {

"name":"Laptop",

"price":80000

}
```

এটা:

```python
Product.objects.create(
    **validated_data
)
```

মানে:

```python
Product.objects.create(
    name="Laptop",
    price=80000
)
```

---

# 15. Professional Pattern

Real project serializer:

```python
class ProductSerializer(
    serializers.ModelSerializer
):


    class Meta:

        model = Product

        fields="__all__"



    def create(self, validated_data):

        # extra logic

        return Product.objects.create(
            **validated_data
        )



    def update(
        self,
        instance,
        validated_data
    ):

        for key,value in validated_data.items():

            setattr(
                instance,
                key,
                value
            )


        instance.save()

        return instance
```

---

# Module 4 Summary

আজকে শিখলে:

✅ `serializer.save()` flow
✅ `create()` method
✅ `update()` method
✅ Custom object creation
✅ Password hashing
✅ PATCH update
✅ Serializer context
✅ Real project create logic

## Practice Task

একটি **User Registration Serializer** বানাও:

Input:

```json
{
"username":"atiar",
"email":"a@gmail.com",
"password":"12345678"
}
```

Requirement:

1. Custom `create()` ব্যবহার করতে হবে
2. Password hash করে save করতে হবে
3. Email duplicate হলে error দিতে হবে

পরের Module:

# Module 5: ModelSerializer Deep Dive

* ModelSerializer ভিতরে কীভাবে কাজ করে
* Meta class
* fields
* exclude
* read_only_fields
* Real Django Model API Design

---
# Module 5: ModelSerializer Deep Dive (DRF)

Module 4 এ আমরা শিখেছি:

* `create()`
* `update()`
* `serializer.save()`
* Custom save logic

এখন আমরা শিখবো **ModelSerializer**, যেটা real Django REST API project-এ সবচেয়ে বেশি ব্যবহার হয়।

---

# 1. ModelSerializer কী?

`ModelSerializer` হলো `Serializer` এর advanced version।

এটা Django Model দেখে automatic:

* Field তৈরি করে
* Validation তৈরি করে
* Create/Update logic তৈরি করে

অর্থাৎ:

Normal Serializer:

```python
Field নিজে লিখতে হয়
```

ModelSerializer:

```python
Model থেকে automatic তৈরি হয়
```

---

# 2. Serializer vs ModelSerializer

## Normal Serializer

```python
class ProductSerializer(serializers.Serializer):

    name = serializers.CharField()

    price = serializers.IntegerField()

```

সব field manually লিখতে হয়।

---

## ModelSerializer

Model:

```python
class Product(models.Model):

    name = models.CharField(
        max_length=100
    )

    price = models.IntegerField()

```

Serializer:

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Product

        fields = "__all__"
```

DRF নিজে তৈরি করবে:

```python
name = serializers.CharField()

price = serializers.IntegerField()
```

---

# 3. ModelSerializer Structure

Standard format:

```python
from rest_framework import serializers


class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Product

        fields = "__all__"
```

এখানে তিনটি অংশ:

```
ProductSerializer

        |
        |
        ↓

ModelSerializer

        |
        |
        ↓

Meta Class
```

---

# 4. Meta Class কী?

`Meta` class Serializer কে configuration দেয়।

Example:

```python
class Meta:

    model = Product

    fields = [
        "id",
        "name",
        "price"
    ]
```

এখানে বলছি:

আমার serializer কোন model ব্যবহার করবে এবং কোন field দেখাবে।

---

# 5. `model` Property

Example:

Model:

```python
class Student(models.Model):

    name=models.CharField(
        max_length=100
    )

    age=models.IntegerField()
```

Serializer:

```python
class StudentSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Student
```

এখন Serializer জানবে:

```
Student Model
       |
       ↓
StudentSerializer
```

---

# 6. `fields` কী?

`fields` দিয়ে API response control করা হয়।

---

## Option 1: সব field

```python
fields="__all__"
```

Model:

```python
class User(models.Model):

    username=models.CharField()

    email=models.EmailField()

    password=models.CharField()
```

Output:

```json
{
    "id":1,
    "username":"Atiar",
    "email":"a@gmail.com",
    "password":"12345"
}
```

সব চলে আসবে।

---

# 7. Specific Fields

Production এ সাধারণত এটা ব্যবহার করা হয়।

```python
class UserSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = User

        fields = [
            "id",
            "username",
            "email"
        ]
```

Output:

```json
{
"id":1,
"username":"Atiar",
"email":"a@gmail.com"
}
```

Password বাদ।

---

# 8. `exclude`

কিছু field বাদ দিতে চাইলে:

```python
class UserSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = User

        exclude = [
            "password"
        ]
```

Output:

```json
{
"id":1,
"username":"Atiar",
"email":"a@gmail.com"
}
```

---

# 9. fields বনাম exclude

| fields                       | exclude                  |
| ---------------------------- | ------------------------ |
| যা চাই শুধু তা দেখায়         | যা বাদ দিতে চাই          |
| বেশি control                 | কম control               |
| Production এ বেশি ব্যবহার হয় | ছোট project এ ব্যবহার হয় |

Best practice:

```python
fields ব্যবহার করো
```

---

# 10. Automatic Validation

Model:

```python
class Product(models.Model):

    name=models.CharField(
        max_length=100
    )

    price=models.IntegerField()
```

ModelSerializer:

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model=Product

        fields="__all__"
```

DRF automatically:

```python
name required=True

price required=True
```

করবে।

---

# 11. Model Validation থেকে Serializer Validation

Model:

```python
class Product(models.Model):

    name=models.CharField(
        max_length=100
    )
```

Serializer automatically:

```python
name = serializers.CharField(
    max_length=100
)
```

তৈরি করবে।

---

# 12. read_only_fields

অনেক সময় কিছু field user পরিবর্তন করতে পারবে না।

Example:

Product:

```python
id
name
price
created_at
```

তুমি চাও:

* id backend তৈরি করবে
* created_at backend তৈরি করবে

Serializer:

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Product

        fields = [
            "id",
            "name",
            "price",
            "created_at"
        ]

        read_only_fields = [
            "id",
            "created_at"
        ]
```

---

Request:

```json
{
"name":"Laptop",
"price":80000
}
```

Allowed।

কিন্তু:

```json
{
"id":50
}
```

ignore হবে।

---

# 13. Extra Field Add করা

ধরো Model:

```python
class User(models.Model):

    first_name=models.CharField()

    last_name=models.CharField()
```

তুমি response এ চাও:

```json
{
"name":"Atiar Rahman"
}
```

Serializer:

```python
class UserSerializer(
    serializers.ModelSerializer
):

    name = serializers.SerializerMethodField()


    class Meta:

        model = User

        fields=[
            "first_name",
            "last_name",
            "name"
        ]


    def get_name(self,obj):

        return (
            obj.first_name
            +" "
            +obj.last_name
        )
```

---

# 14. Extra Serializer Field Override করা

Model:

```python
email=models.EmailField()
```

Default:

```python
email required=True
```

কিন্তু চাই:

```python
email optional
```

Serializer:

```python
class UserSerializer(
    serializers.ModelSerializer
):

    email = serializers.EmailField(
        required=False
    )


    class Meta:

        model=User

        fields="__all__"
```

---

# 15. Real Project Example

তোমার Hotel Management System:

Model:

```python
class Room(models.Model):

    name=models.CharField(
        max_length=100
    )

    price=models.IntegerField()

    is_available=models.BooleanField()

    created_at=models.DateTimeField(
        auto_now_add=True
    )
```

Serializer:

```python
class RoomSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model=Room

        fields=[
            "id",
            "name",
            "price",
            "is_available",
            "created_at"
        ]

        read_only_fields=[
            "id",
            "created_at"
        ]
```

API Response:

```json
{
"id":1,
"name":"Deluxe Room",
"price":5000,
"is_available":true,
"created_at":"2026-07-29"
}
```

---

# 16. ModelSerializer কখন ব্যবহার করবে?

Real project:

```
95% API
      |
      ↓
ModelSerializer
```

Use cases:

✅ CRUD API
✅ User API
✅ Product API
✅ Blog API
✅ Booking API

---

# 17. কখন Normal Serializer ব্যবহার করবে?

যখন Database Model নেই।

Example:

Payment Gateway Request:

```json
{
"card_number":"1234",
"amount":500
}
```

এখানে Model নেই।

তখন:

```python
serializers.Serializer
```

ব্যবহার করবে।

---

# Module 5 Summary

আজকে শিখলে:

✅ ModelSerializer কী
✅ Serializer vs ModelSerializer
✅ Meta class
✅ model
✅ fields
✅ exclude
✅ read_only_fields
✅ Automatic validation
✅ Extra field add
✅ Real project pattern

## Practice Task

একটি `Product` Model ধরো:

```python
class Product(models.Model):

    name
    price
    stock
    created_at
```

Serializer তৈরি করো যেখানে:

1. API তে দেখাবে:

```
id
name
price
stock
```

2. User পরিবর্তন করতে পারবে না:

```
id
created_at
```

---

পরের Module:

# Module 6: ModelSerializer Create & Update Advanced

* Default create/update কীভাবে কাজ করে
* Custom create()
* Custom update()
* Nested object create
* Real E-commerce example

----
