
# Lesson 1: `Serializer` vs `ModelSerializer`

এটি DRF-এর **সবচেয়ে গুরুত্বপূর্ণ topic**। এটা না বুঝলে পরের সব topic (validation, create, update, nested serializer) ঠিকমতো বোঝা কঠিন হবে।

---

# Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন:

* Serializer কেন তৈরি হয়েছে?
* ModelSerializer কেন তৈরি হয়েছে?
* দুটির মধ্যে পার্থক্য
* Internal working
* কখন কোনটি ব্যবহার করবেন
* Real project example
* Common beginner mistakes
* Interview questions

---

# প্রথমে বুঝি Serializer কী?

DRF-এ **Serializer**-এর কাজ ২টি:

1. Python Object → JSON (Serialization)
2. JSON → Python Object + Validation (Deserialization)

Flow:

```text
Database Object
       │
       ▼
 Serializer
       │
       ▼
    JSON Response
```

এবং

```text
JSON Request
      │
      ▼
 Serializer
      │
      ▼
validated_data
```

---

# Serializer Example

ধরুন Model আছে

```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
```

এখন যদি `Serializer` ব্যবহার করেন

```python
from rest_framework import serializers

class StudentSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    name = serializers.CharField(max_length=100)
    age = serializers.IntegerField()
```

এখানে **সব field আপনাকে নিজে লিখতে হয়েছে।**

---

# Serialization

Database

```text
Student

id=1

name="Rahim"

age=22
```

Serializer

```python
serializer = StudentSerializer(student)
```

Output

```json
{
    "id":1,
    "name":"Rahim",
    "age":22
}
```

---

# Deserialization

Request

```json
{
    "name":"Karim",
    "age":25
}
```

Serializer

```python
serializer = StudentSerializer(data=request.data)

serializer.is_valid()

serializer.validated_data
```

Output

```python
{
    "name":"Karim",
    "age":25
}
```

---

# Problem

এখন প্রশ্ন:

Serializer data validate করল।

কিন্তু database-এ save করবে কে?

উত্তর:

আপনাকেই করতে হবে।

---

# create()

```python
class StudentSerializer(serializers.Serializer):

    name = serializers.CharField()

    age = serializers.IntegerField()

    def create(self, validated_data):

        return Student.objects.create(
            **validated_data
        )
```

---

# update()

```python
def update(self, instance, validated_data):

    instance.name = validated_data["name"]

    instance.age = validated_data["age"]

    instance.save()

    return instance
```

সবকিছু manually।

---

# তাহলে ModelSerializer কেন?

DRF Team ভাবলো

> "আমরা তো Model আগেই জানি।
>
> তাহলে field, create(), update() automatically generate করা যায়।"

এভাবেই `ModelSerializer` এসেছে।

---

# একই Serializer

```python
class StudentSerializer(serializers.ModelSerializer):

    class Meta:

        model = Student

        fields = "__all__"
```

এতেই শেষ।

---

# ভিতরে DRF কী করে?

আপনি লেখেন

```python
class StudentSerializer(serializers.ModelSerializer):

    class Meta:

        model = Student

        fields = "__all__"
```

DRF ভিতরে এমন কিছু তৈরি করে

```python
id = serializers.IntegerField(read_only=True)

name = serializers.CharField()

age = serializers.IntegerField()
```

---

তারপর

নিজেই

```python
create()
```

বানিয়ে দেয়

```python
def create(self, validated_data):

    return Student.objects.create(
        **validated_data
    )
```

---

তারপর

```python
update()
```

ও বানিয়ে দেয়

---

# ModelSerializer কী Automatically দেয়?

### Field

Model

```python
name=models.CharField()
```

↓

Serializer

```python
name=serializers.CharField()
```

---

Model

```python
price=models.IntegerField()
```

↓

Serializer

```python
price=serializers.IntegerField()
```

---

Model

```python
email=models.EmailField()
```

↓

Serializer

```python
email=serializers.EmailField()
```

---

Model

```python
is_active=models.BooleanField()
```

↓

Serializer

```python
is_active=serializers.BooleanField()
```

---

# শুধু Field না

Automatically

* validation
* create()
* update()

সব generate করে।

---

# Internal Flow

```text
Model
   │
   ▼
ModelSerializer
   │
   ├── Build Fields
   ├── Build Validators
   ├── Build create()
   ├── Build update()
   ▼
Ready Serializer
```

---

# তাহলে Serializer কবে ব্যবহার করবো?

যখন Model নেই।

Example

Login

```json
{
    "email":"abc@gmail.com",
    "password":"123456"
}
```

এখানে

Login request

Database Model না।

তাই

```python
class LoginSerializer(serializers.Serializer):

    email=serializers.EmailField()

    password=serializers.CharField()
```

---

আরও Example

OTP Verify

```json
{
    "phone":"017xxxx",

    "otp":"1234"
}
```

এখানে

OTP Model নাও থাকতে পারে।

---

Coupon Verify

```json
{
    "coupon":"SAVE10"
}
```

এখানেও

Serializer যথেষ্ট।

---

# ModelSerializer কবে?

যখন Model Save করবেন।

Example

```python
class Product(models.Model):

    name=...

    price=...
```

তখন

```python
class ProductSerializer(
    serializers.ModelSerializer
):
```

---

# Real Project

Registration

```python
User Model
```

↓

ModelSerializer

কারণ

User Save হবে।

---

Login

```python
email

password
```

↓

Serializer

কারণ

Database-এ কিছু Save হচ্ছে না।

---

OTP Verify

↓

Serializer

---

Password Reset

↓

Serializer

---

Product CRUD

↓

ModelSerializer

---

Blog CRUD

↓

ModelSerializer

---

Order CRUD

↓

ModelSerializer

---

# Beginner Mistakes

## Mistake 1

সব জায়গায়

```python
ModelSerializer
```

ব্যবহার করা।

Login-এর জন্যও।

ভুল।

---

## Mistake 2

সব জায়গায়

```python
Serializer
```

ব্যবহার করা।

তারপর

create()

update()

সব manually লেখা।

অপ্রয়োজনীয়।

---

## Mistake 3

ModelSerializer মানেই সবকিছু automatic।

না।

যদি

```python
coupon_code
```

এর মতো custom field যোগ করেন

তাহলে

নিজেকেই

create()

override করতে হবে।

---

# Interview Question

### প্রশ্ন

Serializer আর ModelSerializer-এর মধ্যে পার্থক্য কী?

উত্তর

| Serializer                        | ModelSerializer                |
| --------------------------------- | ------------------------------ |
| সব field manually define করতে হয় | Model থেকে field generate হয়  |
| create/update নিজে লিখতে হয়      | DRF default create/update দেয় |
| Non-model data-এর জন্য ভালো       | Model CRUD-এর জন্য ভালো        |
| বেশি flexibility                  | কম code, দ্রুত development     |

---

# Senior Best Practice

| Scenario          | কোনটি ব্যবহার করবেন? |
| ----------------- | -------------------- |
| Login             | ✅ Serializer         |
| OTP Verification  | ✅ Serializer         |
| Coupon Validation | ✅ Serializer         |
| Contact Form      | ✅ Serializer         |
| Product CRUD      | ✅ ModelSerializer    |
| Blog CRUD         | ✅ ModelSerializer    |
| User CRUD         | ✅ ModelSerializer    |
| Order CRUD        | ✅ ModelSerializer    |

---

# Assignment (অবশ্যই করবেন)

নিচের ৪টি API-এর জন্য বলুন কোন serializer ব্যবহার করবেন এবং **কেন**:

1. User Registration
2. User Login
3. Product Create
4. Forgot Password OTP Verification

আপনি উত্তর দিলে আমি review করব। এরপর **Lesson 2: Serializer Fields (Deep Dive)** শুরু করব।

-----------
দারুণ। এখন **Lesson 2: Serializer Fields (Deep Dive)** শুরু করি।

এই Lesson শেষে আপনি বুঝবেন:

* DRF-এর সব গুরুত্বপূর্ণ serializer field
* কোন field কখন ব্যবহার করবেন
* Model field থেকে serializer field কীভাবে তৈরি হয়
* Beginner mistakes
* Real project examples

---

# Serializer Field কী?

Serializer field-এর কাজ ৩টি:

1. Request data validate করা
2. Python type-এ convert করা
3. Response JSON তৈরি করা

উদাহরণ:

```python
price = serializers.IntegerField()
```

Request:

```json
{
    "price": "100"
}
```

Validation শেষে:

```python
validated_data
```

হবে

```python
{
    "price": 100
}
```

অর্থাৎ `"100"` (string) → `100` (integer)

---

# 1. CharField

সবচেয়ে বেশি ব্যবহৃত field।

```python
name = serializers.CharField(max_length=100)
```

Request

```json
{
    "name": "Laptop"
}
```

Validation

* max_length
* min_length
* required
* allow_blank

Example

```python
name = serializers.CharField(
    max_length=100,
    min_length=3,
    allow_blank=False
)
```

---

# 2. IntegerField

```python
age = serializers.IntegerField()
```

Request

```json
{
    "age": "25"
}
```

Output

```python
25
```

---

# 3. FloatField

```python
rating = serializers.FloatField()
```

Request

```json
{
    "rating": 4.5
}
```

---

# 4. DecimalField

Money-এর জন্য Float ব্যবহার করবেন না।

```python
price = serializers.DecimalField(
    max_digits=10,
    decimal_places=2
)
```

E-commerce-এ

```text
999.99
```

এর জন্য এটি ব্যবহার করবেন।

---

# 5. BooleanField

```python
is_active = serializers.BooleanField()
```

Request

```json
{
    "is_active": true
}
```

---

# 6. EmailField

```python
email = serializers.EmailField()
```

Request

```json
{
    "email": "abc@gmail.com"
}
```

Invalid হলে

```text
Enter a valid email address.
```

---

# 7. URLField

```python
website = serializers.URLField()
```

Valid

```text
https://example.com
```

---

# 8. DateField

```python
birth_date = serializers.DateField()
```

Request

```json
{
    "birth_date": "2000-10-20"
}
```

---

# 9. DateTimeField

```python
created_at = serializers.DateTimeField(read_only=True)
```

Response

```json
{
    "created_at":"2026-07-05T10:30:00Z"
}
```

---

# 10. ChoiceField

Model

```python
STATUS = [
    ("pending", "Pending"),
    ("paid", "Paid"),
]
```

Serializer

```python
status = serializers.ChoiceField(
    choices=STATUS
)
```

Request

```json
{
    "status":"paid"
}
```

Invalid

```json
{
    "status":"unknown"
}
```

Error

```text
"unknown" is not a valid choice.
```

---

# 11. ListField

```python
tags = serializers.ListField(
    child=serializers.CharField()
)
```

Request

```json
{
    "tags":[
        "django",
        "drf",
        "python"
    ]
}
```

---

# 12. JSONField

```python
metadata = serializers.JSONField()
```

Request

```json
{
    "metadata":{
        "color":"black",
        "size":"XL"
    }
}
```

---

# 13. FileField

```python
resume = serializers.FileField()
```

---

# 14. ImageField

```python
profile_picture = serializers.ImageField()
```

---

# 15. HiddenField

User request-এ পাঠাবে না।

আপনি value দেবেন।

```python
created_by = serializers.HiddenField(
    default=serializers.CurrentUserDefault()
)
```

User

```json
{
    "title":"Blog"
}
```

Database

```text
created_by=request.user
```

---

# Field Arguments (সবচেয়ে গুরুত্বপূর্ণ)

প্রায় সব field-এ এগুলো ব্যবহার করা হয়।

```python
name = serializers.CharField(
    required=True,
    read_only=False,
    write_only=False,
    allow_blank=False,
    allow_null=False,
    default="Unknown"
)
```

আপনি ইতিমধ্যে `required`, `read_only`, `write_only` বুঝেছেন।

---

# Model Field → Serializer Field Mapping

| Model Field   | Serializer Field |
| ------------- | ---------------- |
| CharField     | CharField        |
| TextField     | CharField        |
| IntegerField  | IntegerField     |
| FloatField    | FloatField       |
| DecimalField  | DecimalField     |
| BooleanField  | BooleanField     |
| EmailField    | EmailField       |
| URLField      | URLField         |
| DateField     | DateField        |
| DateTimeField | DateTimeField    |
| JSONField     | JSONField        |
| ImageField    | ImageField       |
| FileField     | FileField        |

এগুলো `ModelSerializer` নিজে তৈরি করে।

---

# Real Project Example

```python
class ProductSerializer(serializers.ModelSerializer):
    average_rating = serializers.FloatField(read_only=True)

    coupon_code = serializers.CharField(
        write_only=True, 
        required=False
    )

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
            "average_rating",
            "coupon_code"
        ]
```

এখানে

* `id` → Model থেকে
* `name` → Model থেকে
* `price` → Model থেকে
* `average_rating` → Custom response field
* `coupon_code` → Custom request field

---

# Beginner Mistakes

### 1.

Money-এর জন্য

```python
FloatField
```

ব্যবহার করা।

❌

ব্যবহার করুন

```python
DecimalField
```

---

### 2.

Email-এর জন্য

```python
CharField
```

ব্যবহার করা।

❌

ব্যবহার করুন

```python
EmailField
```

---

### 3.

সব জায়গায়

```python
CharField
```

ব্যবহার করা।

DRF-এর built-in validation নষ্ট হয়ে যায়।

---

### 4.

`required`, `allow_blank`, `allow_null`-এর পার্থক্য না বোঝা।

---

### 5.

Custom field যোগ করে

`create()`

override না করা।

---

# Senior Best Practice

**সবসময় field-এর semantics অনুযায়ী serializer field নির্বাচন করুন।**

❌

```python
email = serializers.CharField()
price = serializers.FloatField()
website = serializers.CharField()
```

✔️

```python
email = serializers.EmailField()
price = serializers.DecimalField(max_digits=10, decimal_places=2)
website = serializers.URLField()
```

এতে DRF আপনার জন্য অনেক validation নিজেই করে দেয়।

---

# Assignment

এই model-এর জন্য একটি `ModelSerializer` লিখুন এবং নিচের নিয়মগুলো অনুসরণ করুন।

```python
class Employee(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    salary = models.DecimalField(max_digits=10, decimal_places=2)
    is_active = models.BooleanField(default=True)
    joined_at = models.DateTimeField(auto_now_add=True)
```

শর্ত:

1. `joined_at` request-এ আসবে না।
2. `password` নামে একটি custom field থাকবে যা শুধু request-এ আসবে।
3. `referral_code` নামে একটি optional custom field থাকবে।
4. `id` response-এ থাকবে।

এই assignment করলে Lesson 3 (`required`, `read_only`, `write_only`, `allow_blank`, `allow_null`, `default`-এর deep dive) আপনার জন্য অনেক সহজ হয়ে যাবে।

-------------


চমৎকার। **Lesson 3** হলো DRF-এর সবচেয়ে বেশি confusing topicগুলোর একটি। কিন্তু এটা বুঝে গেলে serializer-এর ৭০% concept পরিষ্কার হয়ে যাবে।

# Lesson 3: `required`, `read_only`, `write_only`, `allow_blank`, `allow_null`, `default`

---

# প্রথমে একটি গুরুত্বপূর্ণ বিষয়

অনেক beginner মনে করে এগুলো একই জিনিস।

**আসলে এগুলো ৬টি আলাদা property।**

| Property      | প্রশ্নের উত্তর দেয়             |
| ------------- | ------------------------------- |
| `required`    | Request-এ field পাঠাতেই হবে?    |
| `read_only`   | শুধু Response-এ থাকবে?          |
| `write_only`  | শুধু Request-এ থাকবে?           |
| `allow_blank` | Empty string (`""`) গ্রহণ করবে? |
| `allow_null`  | `null` গ্রহণ করবে?              |
| `default`     | User না পাঠালে কোন value হবে?   |

---

# 1. required

## প্রশ্ন

> Client কি fieldটি অবশ্যই পাঠাবে?

```python
name = serializers.CharField(required=True)
```

Request

```json
{
    "age": 20
}
```

Error

```json
{
    "name": [
        "This field is required."
    ]
}
```

---

### required=False

```python
coupon_code = serializers.CharField(required=False)
```

Request

```json
{
    "name":"Laptop"
}
```

✔ Valid

---

## Real Project

Coupon optional

```python
coupon_code = serializers.CharField(
    required=False
)
```

Password

```python
password = serializers.CharField()
```

Default

```text
required=True
```

---

# 2. read_only

## প্রশ্ন

> এই field কি শুধু response-এ থাকবে?

```python
id = serializers.IntegerField(read_only=True)
```

Client

```json
{
    "id":100,
    "name":"Laptop"
}
```

DRF

```text
id ignore করবে।
```

Response

```json
{
    "id":1,
    "name":"Laptop"
}
```

---

## Real Project

```python
id

created_at

updated_at

average_rating

total_review
```

সবগুলো সাধারণত `read_only=True`।

---

# 3. write_only

## প্রশ্ন

> Field কি শুধু request-এ থাকবে?

```python
password = serializers.CharField(
    write_only=True
)
```

Request

```json
{
    "username":"rahim",
    "password":"123456"
}
```

Response

```json
{
    "username":"rahim"
}
```

Password আর response-এ নেই।

---

## Real Project

```text
password

otp

old_password

new_password

coupon_code
```

---

# 4. allow_blank

## প্রশ্ন

> Empty string (`""`) কি valid?

```python
nickname = serializers.CharField(
    allow_blank=True
)
```

Request

```json
{
    "nickname":""
}
```

✔ Valid

---

### allow_blank=False

```python
nickname=""
```

❌ Error

```text
This field may not be blank.
```

---

## Real Project

Middle Name

Nickname

Bio

এসব blank হতে পারে।

---

# 5. allow_null

## প্রশ্ন

> null কি গ্রহণ করবে?

```python
profile = serializers.CharField(
    allow_null=True
)
```

Request

```json
{
    "profile":null
}
```

✔ Valid

---

### allow_null=False

```json
{
    "profile":null
}
```

❌ Error

---

## Difference

Blank

```json
{
    "name":""
}
```

Null

```json
{
    "name":null
}
```

এগুলো এক নয়।

---

# 6. default

```python
status = serializers.CharField(
    default="pending"
)
```

User পাঠায়

```json
{
    "name":"Laptop"
}
```

validated_data

```python
{
    "name":"Laptop",

    "status":"pending"
}
```

---

# সবগুলো একসাথে

```python
coupon_code = serializers.CharField(

    required=False,

    write_only=True,

    allow_blank=False
)
```

মানে

```
Request-এ দিতে পারে

না দিলেও হবে

দিলে "" হবে না

Response-এ যাবে না
```

---

# আরেকটি Example

```python
bio = serializers.CharField(

    required=False,

    allow_blank=True,

    allow_null=True
)
```

Valid

```json
{}
```

Valid

```json
{
    "bio":""
}
```

Valid

```json
{
    "bio":null
}
```

Valid

```json
{
    "bio":"Hello"
}
```

---

# Validation Order

Request

```json
{
    "name":""
}
```

Serializer

```python
name=serializers.CharField(
    required=True,

    allow_blank=False
)
```

DRF internally

```
Field আছে?

↓

Yes

↓

Blank?

↓

Yes

↓

allow_blank?

↓

False

↓

Validation Error
```

---

# required vs allow_blank

```python
name=serializers.CharField(
    required=False,

    allow_blank=False
)
```

Case 1

```json
{}
```

✔ Valid

কারণ

required=False

---

Case 2

```json
{
    "name":""
}
```

❌ Invalid

কারণ

allow_blank=False

---

# required vs allow_null

```python
age=serializers.IntegerField(
    required=False,

    allow_null=True
)
```

Case 1

```json
{}
```

✔ Valid

---

Case 2

```json
{
    "age":null
}
```

✔ Valid

---

Case 3

```json
{
    "age":25
}
```

✔ Valid

---

# Interview Question

### Question

Difference between

```python
required=False
```

and

```python
allow_blank=True
```

Answer

required=False

মানে

Field না পাঠালেও হবে।

allow_blank=True

মানে

Field পাঠাতে হবে

কিন্তু

```text
""
```

হলেও হবে।

---

# Real Project Example

```python
class RegisterSerializer(serializers.Serializer):

    username=serializers.CharField()

    password=serializers.CharField(
        write_only=True
    )

    bio=serializers.CharField(
        required=False,
        allow_blank=True
    )

    referral_code=serializers.CharField(
        required=False,
        write_only=True
    )

    created_at=serializers.DateTimeField(
        read_only=True
    )
```

---

# Beginner Mistakes

### Mistake 1

ভাবা

```python
required=False
```

মানে

```text
allow_blank=True
```

❌

---

### Mistake 2

ভাবা

```python
allow_null=True
```

মানে

```text
allow_blank=True
```

❌

---

### Mistake 3

Password-এ

```python
write_only=False
```

রেখে দেওয়া।

---

### Mistake 4

Coupon optional

কিন্তু

```python
required=True
```

রেখে দেওয়া।

---

### Mistake 5

সব field-এ

```python
allow_null=True
```

দিয়ে দেওয়া।

এতে API contract দুর্বল হয়ে যায়।

---

# Senior Developer Decision Tree

Serializer field বানানোর সময় সবসময় নিজেকে এই ৬টি প্রশ্ন করুন:

1. **User কি এই field অবশ্যই পাঠাবে?** → `required`
2. **Response-এ দেখাতে হবে?** → `read_only`
3. **শুধু request-এর জন্য?** → `write_only`
4. **Empty string (`""`) গ্রহণযোগ্য?** → `allow_blank`
5. **`null` গ্রহণযোগ্য?** → `allow_null`
6. **User না পাঠালে default value দরকার?** → `default`

এই ৬টি প্রশ্নের উত্তর জানলে প্রায় সব serializer field সঠিকভাবে design করতে পারবেন।

---

## Lesson 4 (পরবর্তী)

পরবর্তী Lesson হবে **Validation Deep Dive**, যেখানে আমরা শিখব:

* `is_valid()` ভিতরে কী করে
* `validated_data` কীভাবে তৈরি হয়
* `errors` কীভাবে তৈরি হয়
* `validate_<field>()`
* `validate()`
* Validation execution order (DRF internally)
* Real-world examples (password confirmation, coupon validation, date validation)
* Interview questions এবং beginner mistakes

এটি DRF-এর সবচেয়ে গুরুত্বপূর্ণ lessonগুলোর একটি।


চমৎকার। **Lesson 4** হলো DRF-এর হৃদয় (Heart of Serializer)।

> **যদি Validation বুঝতে পারেন, তাহলে DRF-এর ৮০% serializer logic বুঝে ফেলবেন।**

---

# Lesson 4: Validation Deep Dive

## Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন:

- `serializer.is_valid()` ভিতরে কী করে
    
- `validated_data` কীভাবে তৈরি হয়
    
- `errors` কীভাবে তৈরি হয়
    
- `validate_<field>()`
    
- `validate()`
    
- Validation execution order
    
- `create()` কখন call হয়
    
- Real project examples
    
- Common mistakes
    

---

# পুরো Flow

একটি `POST` request এলে DRF-এর flow হয়:

```text
Client Request
      │
      ▼
Serializer(data=request.data)
      │
      ▼
serializer.is_valid()
      │
      ├── Field Validation
      ├── validate_<field>()
      ├── validate()
      │
      ▼
validated_data
      │
      ▼
serializer.save()
      │
      ▼
create()
      │
      ▼
Database
```

এটাই DRF-এর complete validation pipeline।

---

# Step 1: Request আসে

Request

```json
{
    "name": "Rahim",
    "age": 25
}
```

Serializer

```python
class StudentSerializer(serializers.Serializer):
    name = serializers.CharField()
    age = serializers.IntegerField()
```

View

```python
serializer = StudentSerializer(data=request.data)
```

এখনো validation হয়নি।

---

# Step 2: is_valid()

```python
serializer.is_valid()
```

এটাই DRF-এর validation engine চালু করে।

Internally DRF প্রায় এমন কাজ করে:

```python
for field in serializer.fields:
    value = request.data[field]

    # Field validation
    field.run_validation(value)

# তারপর
validate()

# তারপর
validated_data তৈরি
```

---

# Step 3: Field Validation

ধরুন

```python
age = serializers.IntegerField()
```

Request

```json
{
    "age": "abc"
}
```

Error

```json
{
    "age": [
        "A valid integer is required."
    ]
}
```

এখানে এখনও `validate_age()` call হয়নি।

প্রথমে built-in validation হয়।

---

# Step 4: validate_()

Serializer

```python
class StudentSerializer(serializers.Serializer):
    age = serializers.IntegerField()

    def validate_age(self, value):
        if value < 18:
            raise serializers.ValidationError(
                "Age must be at least 18."
            )

        return value
```

Request

```json
{
    "age": 15
}
```

Error

```json
{
    "age": [
        "Age must be at least 18."
    ]
}
```

---

## কেন return করতে হয়?

```python
return value
```

কারণ DRF এই return value-টাই `validated_data`-তে রাখে।

আপনি চাইলে modify-ও করতে পারেন।

```python
def validate_name(self, value):
    return value.strip().title()
```

Request

```json
{
    "name": "  rahim "
}
```

validated_data

```python
{
    "name": "Rahim"
}
```

---

# Step 5: validate()

এটি পুরো object validate করে।

Example

Password

Confirm Password

```python
class RegisterSerializer(serializers.Serializer):

    password = serializers.CharField()

    confirm_password = serializers.CharField()

    def validate(self, attrs):

        if attrs["password"] != attrs["confirm_password"]:
            raise serializers.ValidationError(
                "Passwords do not match."
            )

        return attrs
```

---

Request

```json
{
    "password": "123456",
    "confirm_password": "654321"
}
```

Error

```json
{
    "non_field_errors": [
        "Passwords do not match."
    ]
}
```

---

# validate_() vs validate()

|validate_()|validate()|
|---|---|
|একটি field|একাধিক field|
|`value` receive করে|`attrs` receive করে|

---

# attrs কী?

```python
attrs
```

হলো

```python
validated_data
```

before save.

Example

```python
{
    "username": "rahim",
    "password": "123456",
    "confirm_password": "123456"
}
```

---

# Step 6: validated_data

Validation pass করলে

```python
serializer.validated_data
```

Output

```python
{
    "name": "Rahim",
    "age": 25
}
```

এটাই পরে

```python
create(validated_data)
```

তে যায়।

---

# Step 7: save()

```python
serializer.save()
```

Internally

```python
if instance is None:
    create(validated_data)
else:
    update(instance, validated_data)
```

---

# Validation Order

এটি interview-তে খুব common।

DRF-এর execution order:

```text
1. Required Check

↓

2. Blank Check

↓

3. Null Check

↓

4. Field Type Validation

↓

5. validate_<field>()

↓

6. validate()

↓

7. validated_data

↓

8. save()

↓

9. create()/update()
```

---

# Real Project Example

Coupon

```python
class OrderSerializer(serializers.Serializer):

    product = serializers.IntegerField()

    coupon_code = serializers.CharField(
        required=False
    )

    def validate_coupon_code(self, value):

        if not Coupon.objects.filter(
            code=value,
            is_active=True
        ).exists():

            raise serializers.ValidationError(
                "Invalid Coupon"
            )

        return value
```

দেখুন,

Coupon validation

create()-এ না করে

validation stage-এ করছি।

এটাই clean approach।

---

# আরেকটি Example

Date Validation

```python
class BookingSerializer(serializers.Serializer):

    start = serializers.DateField()

    end = serializers.DateField()

    def validate(self, attrs):

        if attrs["end"] <= attrs["start"]:

            raise serializers.ValidationError(
                "End date must be after start date."
            )

        return attrs
```

---

# Beginner Mistakes

## Mistake 1

Validation

create()-এ করা।

❌

```python
def create():

    if age<18
```

✔

```python
validate_age()
```

---

## Mistake 2

Password Match

create()-এ করা।

✔

```python
validate()
```

---

## Mistake 3

`is_valid()` না ডেকে

```python
serializer.save()
```

করা।

এতে exception হবে।

---

## Mistake 4

`serializer.data`

ব্যবহার করা

validation-এর আগে।

---

## Mistake 5

`validated_data`

ব্যবহার করা

`is_valid()`-এর আগে।

---

# Interview Questions

### Question 1

Difference

```python
validate_name()
```

vs

```python
validate()
```

Answer

`validate_name()`

একটি field।

`validate()`

একাধিক field।

---

### Question 2

`validated_data`

কখন তৈরি হয়?

Answer

`serializer.is_valid()` successful হলে।

---

### Question 3

`serializer.save()`

কি করে?

Answer

Internally

```python
create()
```

অথবা

```python
update()
```

call করে।

---

# Senior Best Practice

Validation-এর জন্য এই নিয়ম অনুসরণ করুন:

- **Built-in validation** → Field (`EmailField`, `IntegerField`, `ChoiceField` ইত্যাদি) ব্যবহার করুন।
    
- **একটি field-এর custom rule** → `validate_<field>()`
    
- **একাধিক field-এর সম্পর্কিত rule** → `validate()`
    
- **Database-এ save করার logic** → `create()` / `update()`
    

এভাবে code পরিষ্কার, maintainable এবং test করা সহজ হয়।

---

# Assignment

একটি `RegisterSerializer` তৈরি করুন যেখানে:

- `username`
    
- `email`
    
- `password`
    
- `confirm_password`
    

থাকবে।

Requirements:

1. `email` অবশ্যই valid email হবে।
    
2. `password` কমপক্ষে ৮ অক্ষরের হবে।
    
3. `password` এবং `confirm_password` অবশ্যই match করবে।
    
4. `confirm_password` response-এ যাবে না (`write_only=True`)।
    
5. Validation `create()`-এ নয়, সঠিক validation method-এ করবেন।
    

---

## পরবর্তী Lesson (Lesson 5)

**`create()`, `update()`, `save()` Deep Dive**

এটি DRF-এর সবচেয়ে গুরুত্বপূর্ণ implementation lesson, যেখানে আমরা শিখব:

- `save()` ভিতরে কী করে
    
- `create()` কখন call হয়
    
- `update()` কখন call হয়
    
- `instance` কী
    
- `validated_data` কীভাবে `create()`-এ আসে
    
- `ModelSerializer`-এর default `create()`/`update()` internally কীভাবে কাজ করে
    
- Custom create/update-এর real project examples (User registration, Coupon, Nested create)।

---


# Lesson 5: `create()`, `update()`, `save()` Deep Dive

এটি DRF-এর **সবচেয়ে গুরুত্বপূর্ণ lesson**গুলোর একটি।

> একজন Senior Django Developer-এর জন্য `save()` → `create()` → `update()` flow পরিষ্কার থাকা খুবই জরুরি।

---

# Learning Objectives

এই Lesson শেষে আপনি জানতে পারবেন

* `serializer.save()` কী করে
* `create()` কখন call হয়
* `update()` কখন call হয়
* `instance` কী
* `validated_data` কীভাবে আসে
* `ModelSerializer` internally কী করে
* কখন `create()` override করবেন
* কখন `update()` override করবেন

---

# প্রথমে পুরো Flow দেখি

## Create API

```text
POST Request
      │
      ▼
Serializer(data=request.data)
      │
      ▼
is_valid()
      │
      ▼
validated_data
      │
      ▼
save()
      │
      ▼
create(validated_data)
      │
      ▼
Database Save
```

---

## Update API

```text
PUT/PATCH Request
        │
        ▼
Serializer(instance, data=request.data)
        │
        ▼
is_valid()
        │
        ▼
validated_data
        │
        ▼
save()
        │
        ▼
update(instance, validated_data)
        │
        ▼
Database Update
```

---

# save() কী?

অনেক Beginner মনে করে

```python
serializer.save()
```

সরাসরি Database-এ save করে।

❌ না।

`save()` নিজে কিছু save করে না।

এর কাজ হলো সিদ্ধান্ত নেওয়া

```text
Create করবো?

নাকি

Update করবো?
```

---

# DRF ভিতরে কী করে?

ধারণাগতভাবে

```python
def save(self):

    if self.instance is None:
        return self.create(self.validated_data)

    return self.update(
        self.instance,
        self.validated_data
    )
```

এটাই মূল logic।

---

# instance কী?

এটাই সবচেয়ে গুরুত্বপূর্ণ concept।

## Create

```python
serializer = ProductSerializer(
    data=request.data
)
```

এখানে

```python
instance=None
```

অর্থাৎ

```text
নতুন Object বানাতে হবে।
```

---

## Update

```python
product = Product.objects.get(id=1)

serializer = ProductSerializer(
    instance=product,
    data=request.data
)
```

এখন

```text
instance = product object
```

অর্থাৎ

```text
আগের Object Update করতে হবে।
```

---

# Create Example

Model

```python
class Product(models.Model):

    name=models.CharField(max_length=100)

    price=models.IntegerField()
```

Serializer

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model=Product

        fields="__all__"
```

View

```python
serializer=ProductSerializer(
    data=request.data
)

serializer.is_valid(
    raise_exception=True
)

serializer.save()
```

DRF internally

```python
create(validated_data)
```

call করবে।

---

# Default create()

`ModelSerializer` প্রায় এমন code generate করে

```python
def create(self, validated_data):

    return Product.objects.create(
        **validated_data
    )
```

এই কারণেই বেশিরভাগ CRUD API-তে `create()` override করার দরকার হয় না।

---

# Custom create()

ধরুন

Request

```json
{
    "name":"Laptop",

    "price":50000,

    "coupon_code":"SAVE10"
}
```

Serializer

```python
coupon_code = serializers.CharField(
    write_only=True
)
```

Model-এ

```text
coupon_code
```

নেই।

তাহলে

```python
def create(self, validated_data):

    coupon = validated_data.pop(
        "coupon_code"
    )

    # Business Logic

    return Product.objects.create(
        **validated_data
    )
```

---

# Update Example

ধরুন

Database

```text
Laptop

50000
```

Request

```json
{
    "price":55000
}
```

Serializer

```python
serializer = ProductSerializer(

    instance=product,

    data=request.data
)
```

---

save()

↓

```python
update(
    instance,
    validated_data
)
```

---

Default update()

প্রায়

```python
def update(
    self,
    instance,
    validated_data
):

    instance.name=validated_data.get(
        "name",
        instance.name
    )

    instance.price=validated_data.get(
        "price",
        instance.price
    )

    instance.save()

    return instance
```

---

# কেন get() ব্যবহার করছে?

কারণ

PATCH

এ

সব field আসে না।

যেমন

```json
{
    "price":55000
}
```

name আসেনি।

তাই

```python
validated_data.get(
    "name",
    instance.name
)
```

---

# কখন create() Override করবেন?

### ১

Password Hash

```python
user.set_password(password)
```

---

### ২

Coupon

```python
coupon_code
```

---

### ৩

OTP

---

### ৪

Extra Field

---

### ৫

Email Send

---

### ৬

Audit Log

---

### ৭

Notification

---

# কখন update() Override করবেন?

Password Change

```python
set_password()
```

---

Image Delete

---

Stock Update

---

Email Change

---

Activity Log

---

# validated_data কোথা থেকে আসে?

Flow

```text
Request

↓

is_valid()

↓

Field Validation

↓

validate()

↓

validated_data

↓

save()

↓

create()
```

create()

receive করে

```python
validated_data
```

---

# save() Return কী?

```python
product = serializer.save()
```

এখন

```python
product
```

হলো

Database Object

```python
print(product.id)
```

কাজ করবে।

---

# save(commit=False) কেন নেই?

Django Form

```python
form.save(commit=False)
```

আছে।

DRF Serializer

```python
serializer.save(commit=False)
```

নেই।

অনেক Beginner এই ভুল করে।

---

# Common Mistakes

---

## Mistake 1

```python
serializer.save()
```

এর আগে

```python
serializer.is_valid()
```

না ডাকা।

---

## Mistake 2

create()

এ

```python
return validated_data
```

ফিরিয়ে দেওয়া।

❌

Database Save হবে না।

---

## Mistake 3

Model-এ নেই

তবুও

```python
Product.objects.create(
    **validated_data
)
```

করা।

---

## Mistake 4

update()

এ

```python
instance.save()
```

ভুলে যাওয়া।

---

## Mistake 5

return

না করা।

---

# Interview Questions

### Question 1

save() কি করে?

Answer

create()

অথবা

update()

call করে।

---

### Question 2

create() কখন call হয়?

Answer

instance

None

হলে।

---

### Question 3

update()

কখন call হয়?

Answer

instance

থাকলে।

---

### Question 4

validated_data কোথা থেকে আসে?

Answer

is_valid()

successful হওয়ার পরে।

---

# Real Project Example

User Registration

```python
class RegisterSerializer(serializers.ModelSerializer):

    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = ["username", "password"]

    def create(self, validated_data):
        password = validated_data.pop("password")

        user = User(**validated_data)
        user.set_password(password)
        user.save()

        return user
```

কেন override করা হলো?

কারণ

```python
User.objects.create(**validated_data)
```

করলে password plain text হিসেবে save হবে।

`set_password()` ব্যবহার করে hash করতে হবে।

---

# Senior Best Practices

| Situation              | কী করবেন?                                                        |
| ---------------------- | ---------------------------------------------------------------- |
| Simple CRUD            | Default `ModelSerializer` `create()`/`update()` ব্যবহার করুন     |
| Password Hash          | `create()`/`update()` override করুন                              |
| Extra Serializer Field | `validated_data.pop()` করুন                                      |
| Business Logic         | `create()`/`update()`-এ বা বড় project হলে service layer-এ রাখুন |
| শুধু validation        | `create()`-এ নয়, `validate()` বা `validate_<field>()`-এ করুন    |

---

## Homework

একটি `UserRegistrationSerializer` লিখুন যেখানে:

* `username`
* `email`
* `password`
* `confirm_password`

থাকবে।

Requirements:

1. `confirm_password` model-এ নেই।
2. `password` ও `confirm_password` match করতে হবে (`validate()` ব্যবহার করুন)।
3. `create()`-এ `confirm_password` `pop()` করবেন।
4. `password` `set_password()` দিয়ে hash করবেন।
5. শেষে `user` object return করবেন।

---

## পরবর্তী Lesson (Lesson 6)

**`Serializer Context`, `source`, এবং `SerializerMethodField`**

এখানে আপনি শিখবেন:

* `self.context` কী
* `request.user` serializer-এ কীভাবে পাওয়া যায়
* `source` দিয়ে nested attribute mapping
* `SerializerMethodField` কীভাবে কাজ করে
* `annotate()` বনাম `SerializerMethodField`
* Performance (N+1 Query) এবং Best Practices

এটি বাস্তব DRF project-এ প্রতিদিন ব্যবহৃত হয়।
দারুণ। **Lesson 6** হলো এমন একটি topic যেটা Junior Developer-দের থেকে Senior Developer-দের আলাদা করে।

এই Lesson-এ আমরা শিখবো:

1. `context`
2. `source`
3. `SerializerMethodField`
4. কখন কোনটা ব্যবহার করবেন
5. Performance issue (N+1 Query)

---

# Part 1: Serializer Context

## Problem

ধরুন আপনি serializer-এর ভিতরে logged-in user ব্যবহার করতে চান।

যেমন

* created_by = request.user
* user নিজের profile update করছে কিনা
* request header access করতে হবে

কিন্তু serializer-এর ভিতরে `request` কোথায়?

---

## উত্তর

DRF `context` ব্যবহার করে।

View

```python
serializer = ProductSerializer(
    data=request.data,
    context={
        "request": request
    }
)
```

**কিন্তু একটা ভালো খবর আছে।**

যদি আপনি `APIView`, `GenericAPIView`, `ModelViewSet` ইত্যাদি ব্যবহার করেন এবং `self.get_serializer()` ব্যবহার করেন, তাহলে DRF **নিজেই** `request`, `view` এবং `format` context-এ পাঠিয়ে দেয়।

অর্থাৎ সাধারণ `ModelViewSet`-এ আপনাকে manually context পাঠাতে হয় না।

---

## Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = "__all__"

    def create(self, validated_data):

        user = self.context["request"].user

        return Product.objects.create(
            owner=user,
            **validated_data
        )
```

---

## Real Project

Blog তৈরি

Request

```json
{
    "title":"DRF"
}
```

User

```text
Rahim
```

Database

```text
title = DRF

owner = Rahim
```

User request-এ owner পাঠায়নি।

Serializer নিজেই

```python
request.user
```

নিয়েছে।

---

# কখন Context ব্যবহার করবেন?

✅ Logged-in User

✅ Request Header

✅ Language

✅ Custom Value

উদাহরণ

```python
serializer = ProductSerializer(
    data=request.data,
    context={
        "discount":20
    }
)
```

Serializer

```python
discount = self.context["discount"]
```

---

# Part 2: source

`source` অনেক Beginner জানেই না।

এটা খুব powerful feature।

---
# `source` তুমি তখন use করবে যখন তুমি চাইবে **serializer-এর field সরাসরি model-এর ভিতরের কোনো attribute/property থেকে value নিতে** — কোনো custom Python logic ছাড়াই।

---

## 🔥 কখন `source` ব্যবহার করবে

### 1️⃣ Model field rename করতে চাইলে

```python
class UserSerializer(serializers.ModelSerializer):
    full_name = serializers.CharField(source='first_name', read_only=True)
```

👉 এখানে `full_name` আসলে `first_name` দেখাবে (rename mapping)

---

### 2️⃣ Model property থাকলে

```python
class User(models.Model):
    first_name = models.CharField(max_length=100)
    last_name = models.CharField(max_length=100)

    @property
    def full_name(self):
        return f"{self.first_name} {self.last_name}"
```

Serializer:

```python
full_name = serializers.CharField(source='full_name', read_only=True)
```

👉 এটা model property থেকে value আনবে

---

### 3️⃣ Related model থেকে data আনতে

```python
class Order(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

Serializer:

```python
user_email = serializers.CharField(source='user.email', read_only=True)
```

👉 relationship traverse করে value নেয়

---

## ❌ কখন `source` ব্যবহার করবে না

### ❌ complex logic লাগলে

```python
return f"{first_name} {last_name}"
```

👉 তখন use করবে:

```python
SerializerMethodField()
```

---

### ❌ service layer call করলে

```python
self.context["service"].full_name(obj)
```

👉 এখানে `source` কাজ করবে না

---

## ⚡ simple rule

| Situation          | Use                       |
| ------------------ | ------------------------- |
| direct model field | `source` ✔                |
| model property     | `source` ✔                |
| related field      | `source` ✔                |
| custom logic       | `SerializerMethodField` ✔ |
| service layer      | `SerializerMethodField` ✔ |

---

## 🔥 এক লাইনে মনে রাখো

👉 `source = শুধু model-এর ভিতরের data fetch করার shortcut`

---
## Example 1

Model

```python
class User(models.Model):

    first_name=models.CharField()

    last_name=models.CharField()
```

Property

```python
@property
def full_name(self):

    return f"{self.first_name} {self.last_name}"
```

Serializer

```python
full_name = serializers.CharField(
    source="full_name",
    read_only=True
)
```

Response

```json
{
    "full_name":"Rahim Hasan"
}
```

---

## Example 2

Nested Object

Model

```python
class Product(models.Model):

    seller=models.ForeignKey(User)
```

Serializer

```python
seller_name = serializers.CharField(
    source="seller.username",
    read_only=True
)
```

Response

```json
{
    "seller_name":"rahim"
}
```

কোন

```python
get_seller_name()
```

লিখতে হলো না।

---

# source কখন ব্যবহার করবেন?

যদি শুধু

একটা attribute

বা

property

বা

related model-এর field

দেখাতে চান।

---

# ভুল Approach

```python
seller_name = serializers.SerializerMethodField()

def get_seller_name(self,obj):

    return obj.seller.username
```

এটা না লিখে

```python
seller_name = serializers.CharField(
    source="seller.username"
)
```

লিখুন।

Code ছোট হবে।

---

# Part 3: SerializerMethodField

এখন ধরুন

একটা field calculate করতে হবে।

তখন?

---

Example

Product

Review

Average Rating

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    average_rating = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = "__all__"

    def get_average_rating(self,obj):

        return 4.8
```

Response

```json
{
    "average_rating":4.8
}
```

---

আরও Example

```python
def get_is_owner(self,obj):

    return obj.owner==self.context["request"].user
```

Response

```json
{
    "is_owner":true
}
```

---

# SerializerMethodField-এর Rule

Field

```python
total = serializers.SerializerMethodField()
```

Method

```python
def get_total(self,obj):
```

Field Name

↓

Method Name

```
total

↓

get_total
```

---
হ্যাঁ—SerializerMethodField ব্যবহার করলে সবসময়ই obj receive করবে, কিন্তু সেটা কোন type হবে সেটা গুরুত্বপূর্ণ।

🔥 সোজা উত্তর

👉 SerializerMethodField এর method সবসময় model instance (object) receive করে।
# Real Project

Order

```python
class OrderSerializer(serializers.ModelSerializer):

    total_price=serializers.SerializerMethodField()

    def get_total_price(self,obj):

        return obj.quantity*obj.product.price
```

---

# কখন SerializerMethodField ব্যবহার করবেন?

যখন

* Calculation
* Dynamic Value
* Complex Logic
* User-specific Data

---

# কিন্তু একটা সমস্যা আছে

ধরুন

100 Product

Serializer

```python
def get_review_count(self,obj):

    return obj.reviews.count()
```

প্রতি Product-এর জন্য

```python
count()
```

চলবে।

তাহলে

```
1 Product Query

+

100 Count Query
```

মোট

```
101 Query
```

এটাই

**N+1 Query Problem**

---

# Solution

View-তে

```python
queryset = Product.objects.annotate(
    review_count=Count("reviews")
)
```

Serializer

```python
review_count = serializers.IntegerField(
    read_only=True
)
```

এখন

মাত্র

```
1 Query
```

---

# annotate vs SerializerMethodField

## SerializerMethodField

```python
def get_review_count()
```

✔ ছোট calculation

✔ user-specific logic

---

## annotate

✔ Count

✔ Avg

✔ Sum

✔ Exists

✔ Subquery

Database-এ calculation হবে।

Performance অনেক ভালো।

---

# কখন কোনটা?

| Situation                     | Best Choice                                                                 |
| ----------------------------- | --------------------------------------------------------------------------- |
| `obj.full_name`               | `source`                                                                    |
| `seller.username`             | `source`                                                                    |
| `quantity × price`            | `SerializerMethodField` (বা annotate যদি list API-তে performance দরকার হয়) |
| Review Count                  | `annotate()`                                                                |
| Average Rating                | `annotate()`                                                                |
| Sum                           | `annotate()`                                                                |
| Logged-in user অনুযায়ী value | `SerializerMethodField` + `context`                                         |

---

# Common Beginner Mistakes

## Mistake 1

সবকিছুর জন্য

```python
SerializerMethodField
```

ব্যবহার করা।

---

## Mistake 2

`source` ব্যবহার না জানা।

---

## Mistake 3

`SerializerMethodField`-এর ভিতরে

```python
Review.objects.filter(...)
```

চালানো।

List API-তে Performance নষ্ট হবে।

---

## Mistake 4

Context manually পাঠানোর দরকার নেই এমন জায়গায়ও

```python
context={"request":request}
```

লিখে ফেলা।

`ModelViewSet`-এ সাধারণত DRF নিজেই এটা করে।

---

# Senior Best Practices

1. **Simple attribute mapping** → `source`
2. **Calculated field (ছোট logic)** → `SerializerMethodField`
3. **Database aggregation (`Count`, `Sum`, `Avg`)** → `annotate()`
4. **Logged-in user দরকার** → `self.context["request"]`
5. **List API-তে performance সবসময় চিন্তা করুন।**

---

# Real E-commerce Example

```python
class ProductSerializer(serializers.ModelSerializer):

    seller_name = serializers.CharField(
        source="seller.username",
        read_only=True
    )

    average_rating = serializers.FloatField(
        read_only=True
    )  # annotate থেকে আসবে

    is_owner = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "seller_name",
            "average_rating",
            "is_owner"
        ]

    def get_is_owner(self, obj):
        request = self.context["request"]
        return request.user == obj.seller
```

এখানে তিনটি technique একসাথে ব্যবহার হয়েছে:

* `source` → `seller.username`
* `annotate()` → `average_rating`
* `SerializerMethodField` + `context` → `is_owner`

এটাই production-level pattern।

---

## Homework

একটি `BlogSerializer` তৈরি করুন যেখানে:

* `author_name` → `source="author.username"`
* `comment_count` → `annotate()` থেকে আসবে
* `is_author` → `SerializerMethodField` ব্যবহার করে `request.user`-এর সাথে compare করবে

এটি করতে পারলে আপনি `context`, `source`, `SerializerMethodField` এবং `annotate()`—এই চারটি গুরুত্বপূর্ণ concept একসাথে ব্যবহার করতে পারবেন।

---

### পরবর্তী Lesson (Lesson 7)

**Relationship Fields Deep Dive**

এখানে আমরা বিস্তারিত শিখব:

* `PrimaryKeyRelatedField`
* `StringRelatedField`
* `SlugRelatedField`
* `HyperlinkedRelatedField`
* Nested Serializer
* Writable Nested Serializer
* Many-to-Many এবং ForeignKey serialization
* Production-level relationship design

--------

# Lesson 7: Relationship Fields Deep Dive

এটি DRF-এর অন্যতম গুরুত্বপূর্ণ topic। প্রায় প্রতিটি real project-এ (E-commerce, Blog, LMS, Multi-vendor) relationship field ব্যবহার হয়।

---

# Learning Objectives

এই Lesson শেষে আপনি বুঝতে পারবেন:

* ForeignKey serializer-এ কীভাবে কাজ করে
* ManyToMany serializer-এ কীভাবে কাজ করে
* `PrimaryKeyRelatedField`
* `StringRelatedField`
* `SlugRelatedField`
* Nested Serializer
* Writable Nested Serializer
* কখন কোন approach ব্যবহার করবেন

---

# প্রথমে Database বুঝি

ধরুন

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
```

```python
class Product(models.Model):
    name = models.CharField(max_length=100)

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

Database

```
Category

id   name
--------------
1    Electronics
2    Books
```

```
Product

id   name        category_id
----------------------------
1    Laptop      1
```

Database-এ **category object save হয় না**, save হয় শুধু

```
category_id = 1
```

---

# DRF Default Behavior

যদি লিখেন

```python
class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = "__all__"
```

Response

```json
{
    "id":1,
    "name":"Laptop",
    "category":1
}
```

কারণ DRF default-এ

```
PrimaryKeyRelatedField
```

ব্যবহার করে।

---

# PrimaryKeyRelatedField

এটাই DRF-এর default relationship field।

Explicitly লিখতে চাইলে

```python
category = serializers.PrimaryKeyRelatedField(
    queryset=Category.objects.all()
)
```

Request

```json
{
    "name":"Laptop",
    "category":1
}
```

DRF internally

```
Category.objects.get(id=1)
```

করে।

তারপর

```
Product.category = Category Object
```

assign করে।

---

# যদি ID না থাকে?

Request

```json
{
    "category":100
}
```

Error

```json
{
    "category":[
        "Invalid pk \"100\" - object does not exist."
    ]
}
```

---

# StringRelatedField

Model

```python
class Category(models.Model):

    name=models.CharField(max_length=100)

    def __str__(self):

        return self.name
```

Serializer

```python
category = serializers.StringRelatedField()
```

Response

```json
{
    "category":"Electronics"
}
```

দেখুন

ID না।

String এসেছে।

---

# কিন্তু Problem

Request

```json
{
    "category":"Electronics"
}
```

❌ Save হবে না।

কারণ

`StringRelatedField`

**read_only**

---

# কখন ব্যবহার করবেন?

যদি শুধু

Response সুন্দর করতে চান।

---

# SlugRelatedField

ধরুন

Category

```
id=1

name="Electronics"
```

Serializer

```python
category = serializers.SlugRelatedField(

    queryset=Category.objects.all(),

    slug_field="name"
)
```

Request

```json
{
    "category":"Electronics"
}
```

DRF internally

```
Category.objects.get(
    name="Electronics"
)
```

---

Response

```json
{
    "category":"Electronics"
}
```

---

# Slug বলতে কী বোঝায়?

Slug মানে **একটি unique বা meaningful field** যা object identify করতে পারে।

যেমন

```
username

email

code

slug

sku
```

---

Example

```
Product

sku="ABC123"
```

```python
product = serializers.SlugRelatedField(

    slug_field="sku",

    queryset=Product.objects.all()
)
```

---

# কখন SlugRelatedField ব্যবহার করবেন?

যখন

ID expose করতে চান না।

---

# Nested Serializer

Category Serializer

```python
class CategorySerializer(
    serializers.ModelSerializer
):

    class Meta:

        model=Category

        fields=["id","name"]
```

Product Serializer

```python
class ProductSerializer(
    serializers.ModelSerializer
):

    category=CategorySerializer(
        read_only=True
    )

    class Meta:

        model=Product

        fields="__all__"
```

Response

```json
{
    "id":1,
    "name":"Laptop",

    "category":{

        "id":1,

        "name":"Electronics"
    }
}
```

এটাই Nested Serializer।

---

# কেন ব্যবহার করবেন?

Frontend-এর আলাদা API call কমে যায়।

---

# কিন্তু একটা Problem

Request

```json
{
    "name":"Laptop",

    "category":{

        "id":1,

        "name":"Electronics"
    }
}
```

❌

Default Nested Serializer

Save করতে পারে না।

---

# Writable Nested Serializer

এখানে

নিজেকেই

`create()`

override করতে হবে।

Example

```python
def create(self, validated_data):

    category_data = validated_data.pop(
        "category"
    )

    category = Category.objects.create(
        **category_data
    )

    return Product.objects.create(
        category=category,
        **validated_data
    )
```

---

# ManyToMany Example

```
Product

↓

ManyToMany

↓

Tag
```

Serializer

```python
tags = serializers.PrimaryKeyRelatedField(

    many=True,

    queryset=Tag.objects.all()
)
```

Request

```json
{
    "tags":[
        1,
        2,
        3
    ]
}
```

---

# Nested ManyToMany

```python
tags = TagSerializer(
    many=True,
    read_only=True
)
```

Response

```json
{
    "tags":[

        {
            "id":1,
            "name":"Python"
        },

        {
            "id":2,
            "name":"Django"
        }
    ]
}
```

---

# Relationship Summary

| Field                  | Request       | Response      | Save                 |
| ---------------------- | ------------- | ------------- | -------------------- |
| PrimaryKeyRelatedField | ID            | ID            | ✅                    |
| StringRelatedField     | ❌             | String        | ❌                    |
| SlugRelatedField       | Slug          | Slug          | ✅                    |
| Nested Serializer      | Nested Object | Nested Object | Read Only by default |

---

# Real E-commerce Example

Product

↓

Category

↓

Seller

↓

Tags

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    category = serializers.PrimaryKeyRelatedField(
        queryset=Category.objects.all()
    )

    seller = serializers.StringRelatedField()

    tags = TagSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = Product
        fields = "__all__"
```

---

# Common Beginner Mistakes

## Mistake 1

সব relationship-এ

Nested Serializer

ব্যবহার করা।

List API খুব slow হয়ে যায়।

---

## Mistake 2

Nested Serializer দিয়ে

Create

করতে চাওয়া।

Default-এ হবে না।

---

## Mistake 3

`StringRelatedField`

দিয়ে

Save করার চেষ্টা করা।

---

## Mistake 4

ForeignKey-এর জন্য

```python
category = serializers.IntegerField()
```

লেখা।

এটা করবেন না।

`PrimaryKeyRelatedField` ব্যবহার করুন।

---

# Senior Best Practices

| Scenario                   | Best Choice                                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------------------ |
| Create API                 | `PrimaryKeyRelatedField`                                                                         |
| Update API                 | `PrimaryKeyRelatedField`                                                                         |
| Simple Response            | `StringRelatedField`                                                                             |
| Public API (username/slug) | `SlugRelatedField`                                                                               |
| Detail API                 | Nested Serializer                                                                                |
| Large List API             | Nested Serializer এড়িয়ে চলুন, প্রয়োজনে `select_related()` / `prefetch_related()` ব্যবহার করুন |

---

# বাস্তব উদাহরণ (Amazon)

## Product List API

```
GET /products
```

Response

```json
[
  {
    "id": 1,
    "name": "Laptop",
    "category": 3
  }
]
```

কারণ List API-তে response ছোট রাখা ভালো।

---

## Product Detail API

```
GET /products/1
```

Response

```json
{
  "id": 1,
  "name": "Laptop",
  "category": {
    "id": 3,
    "name": "Electronics"
  }
}
```

এখানে Nested Serializer ব্যবহার করলে frontend-এর জন্য সুবিধা হয়।

এটাই production project-এ খুবই common pattern।

---

## Homework

নিচের Model-এর জন্য দুটি serializer লিখুন:

```python
class Author(models.Model):
    username = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

1. **BookListSerializer**

   * `author` → `PrimaryKeyRelatedField`

2. **BookDetailSerializer**

   * `author` → Nested `AuthorSerializer`

এতে আপনি একই Model-এর জন্য ভিন্ন serializer design করার অভ্যাস করবেন, যা বড় project-এ খুবই গুরুত্বপূর্ণ।

---

## পরবর্তী Lesson (Lesson 8)

আমরা শিখব **Nested Serializer & Writable Nested Serializer (Advanced)**:

* Nested create
* Nested update
* One-to-One, One-to-Many, Many-to-Many nested save
* Transaction ব্যবহার (`transaction.atomic`)
* Performance optimization
* Production-level patterns (Order + OrderItems, Blog + Comments, User + Profile)

# Lesson 8: Nested Serializer (Advanced) + Writable Nested + Real Production Patterns

এটা DRF-এর **most important + most tricky topic**।

> E-commerce, Blog, LMS, Order system—সব real project এখানে আটকে যায়।

এই lesson শেষে আপনি বুঝবেন:

* Nested serializer কেন complex হয়
* Read-only nested vs Writable nested
* Nested create/update কীভাবে কাজ করে
* `transaction.atomic()` কেন লাগে
* Real production pattern (Order system)

---

# Part 1: Nested Serializer Recap

আগের lesson:

```python
class AuthorSerializer(serializers.ModelSerializer):
    class Meta:
        model = Author
        fields = "__all__"
```

```python
class BookSerializer(serializers.ModelSerializer):

    author = AuthorSerializer(read_only=True)

    class Meta:
        model = Book
        fields = "__all__"
```

Response:

```json
{
    "id": 1,
    "title": "DRF Guide",
    "author": {
        "id": 1,
        "username": "rahim"
    }
}
```

✔ সুন্দর response
❌ কিন্তু create করতে পারি না

---

# Problem: Writable Nested

Request:

```json
{
    "title": "DRF Guide",
    "author": {
        "username": "rahim"
    }
}
```

DRF default এটা handle করতে পারে না।

---

# Part 2: Writable Nested Create

## Step 1: Serializer

```python
class AuthorSerializer(serializers.ModelSerializer):
    class Meta:
        model = Author
        fields = "__all__"
```

```python
class BookSerializer(serializers.ModelSerializer):

    author = AuthorSerializer()

    class Meta:
        model = Book
        fields = "__all__"
```

---

## Step 2: Custom create()

```python
def create(self, validated_data):

    author_data = validated_data.pop("author")

    author = Author.objects.create(**author_data)

    book = Book.objects.create(
        author=author,
        **validated_data
    )

    return book
```

---

## Flow বুঝুন

```text
Request JSON
   ↓
validated_data
   ↓
pop("author")
   ↓
Author তৈরি
   ↓
Book তৈরি
```

---

# Part 3: Writable Nested Update (Hard Part)

Request:

```json
{
    "title": "New Title",
    "author": {
        "username": "new_rahim"
    }
}
```

---

## update()

```python
def update(self, instance, validated_data):

    author_data = validated_data.pop("author")

    # update book
    instance.title = validated_data.get(
        "title",
        instance.title
    )
    instance.save()

    # update author
    author = instance.author
    author.username = author_data.get(
        "username",
        author.username
    )
    author.save()

    return instance
```

---

# Part 4: Real Production Example (VERY IMPORTANT)

## E-commerce Order System

### Models

```python
class Order(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    total = models.DecimalField(max_digits=10, decimal_places=2)


class OrderItem(models.Model):
    order = models.ForeignKey(Order, on_delete=models.CASCADE, related_name="items")
    product = models.CharField(max_length=100)
    quantity = models.IntegerField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

---

# Step 1: Serializer

```python
class OrderItemSerializer(serializers.ModelSerializer):

    class Meta:
        model = OrderItem
        fields = ["product", "quantity", "price"]
```

---

```python
class OrderSerializer(serializers.ModelSerializer):

    items = OrderItemSerializer(many=True)

    class Meta:
        model = Order
        fields = ["id", "user", "total", "items"]
```

---

# Step 2: Writable Nested Create

```python
from django.db import transaction
```

```python
def create(self, validated_data):

    items_data = validated_data.pop("items")

    with transaction.atomic():

        order = Order.objects.create(**validated_data)

        total = 0

        for item in items_data:

            OrderItem.objects.create(
                order=order,
                **item
            )

            total += item["price"] * item["quantity"]

        order.total = total
        order.save()

    return order
```

---

# Why transaction.atomic()?

If something fails:

```text
Order created ❌
OrderItems half created ❌
Total wrong ❌
```

With atomic:

```text
ALL OR NOTHING ✔
```

---

# Part 5: Writable Nested Update (Advanced)

Example:

```json
{
    "items": [
        {
            "product": "Laptop",
            "quantity": 2,
            "price": 50000
        }
    ]
}
```

---

```python
def update(self, instance, validated_data):

    items_data = validated_data.pop("items")

    with transaction.atomic():

        # update order
        instance.total = validated_data.get(
            "total",
            instance.total
        )
        instance.save()

        # delete old items
        instance.items.all().delete()

        # recreate items
        total = 0

        for item in items_data:

            OrderItem.objects.create(
                order=instance,
                **item
            )

            total += item["price"] * item["quantity"]

        instance.total = total
        instance.save()

    return instance
```

---

# Part 6: Best Practice (VERY IMPORTANT)

## ❌ Bad Approach

* Every nested serializer writable
* Deep nesting (3–4 level)
* No transaction
* Heavy logic in serializer only

---

## ✅ Good Approach

| Scenario              | Approach               |
| --------------------- | ---------------------- |
| Simple FK             | PrimaryKeyRelatedField |
| Read nested response  | Nested serializer      |
| Create complex nested | override create()      |
| Update complex nested | override update()      |
| Multi-step logic      | service layer          |
| Critical data         | transaction.atomic()   |

---

# Part 7: Common Mistakes

## Mistake 1

```python
author = AuthorSerializer()
```

without override create()

❌ will crash on POST

---

## Mistake 2

Nested update না জানা

→ only parent update করে

---

## Mistake 3

transaction.atomic() না ব্যবহার

→ partial data saved

---

## Mistake 4

Too deep nesting

```text
Order → Items → Product → Category → Seller
```

API slow + unreadable

---

# Part 8: Senior Architecture Pattern

Production systems usually follow:

## Option 1 (Best for APIs)

```text
Request
   ↓
Serializer (light validation only)
   ↓
Service Layer (business logic)
   ↓
Models
```

---

## Option 2 (Simple projects)

```text
Serializer handles everything
```

---

# Part 9: Real Interview Insight

### Q: Nested serializer কেন complex?

Answer:

Because:

* multiple object creation
* relationship handling
* transaction required
* validation across models

---

### Q: When NOT to use nested writable serializer?

* large scale system
* performance critical API
* deep relationship graph

---

# Homework (VERY IMPORTANT)

## Task:

Create Blog system

### Models:

* Author
* Blog
* Comment

### Requirements:

1. Blog create করবে সাথে comments থাকবে
2. Author nested থাকবে
3. Comment multiple থাকবে
4. `transaction.atomic()` ব্যবহার করতে হবে
5. total comment count annotate করা optional

---

# Next Lesson (Lesson 9)

👉 **Performance + Query Optimization in DRF**

আপনি শিখবেন:

* N+1 problem deep dive
* `select_related`
* `prefetch_related`
* annotate optimization
* Serializer vs DB query balance
* Production API optimization pattern

---

আপনি চাইলে আমি পরের lesson-এর আগে আপনার **Nested serializer project review** করে দিতে পারি (E-commerce বা Blog structure)।
# Lesson 9: Performance + Query Optimization in DRF (VERY IMPORTANT)

এটা এমন একটা topic যেটা **Junior → Senior Django Developer** পার্থক্য তৈরি করে।

> Real project-এ 80% performance problem আসে এখান থেকেই: **N+1 Query**

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* N+1 Query কী
* কেন DRF slow হয়
* `select_related()` কবে ব্যবহার করবেন
* `prefetch_related()` কবে ব্যবহার করবেন
* SerializerMethodField কেন dangerous হতে পারে
* Production-level optimization pattern

---

# Part 1: N+1 Query Problem (Core Concept)

ধরুন model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    category = models.ForeignKey("Category", on_delete=models.CASCADE)
```

---

## Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    category_name = serializers.SerializerMethodField()

    def get_category_name(self, obj):
        return obj.category.name
```

---

## View

```python
queryset = Product.objects.all()
```

---

## কী সমস্যা হবে?

ধরুন 100 products আছে:

### Query flow:

```
1 Query → Product list

+ 100 Queries → category.name
```

👉 Total: **101 Queries**

এটাই N+1 problem

---

# Part 2: select_related (ForeignKey optimization)

## ব্যবহার হবে যখন:

* ForeignKey
* OneToOneField

---

## Fix:

```python
queryset = Product.objects.select_related("category")
```

---

## এখন কী হবে?

```
1 Query only
JOIN ব্যবহার করে সব data চলে আসবে
```

---

## Optimized Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    category_name = serializers.CharField(
        source="category.name",
        read_only=True
    )
```

✔ Fast
✔ No extra query

---

# Rule:

> FK হলে সবসময় `select_related()`

---

# Part 3: prefetch_related (ManyToMany / Reverse FK)

ধরুন:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)

class Tag(models.Model):
    name = models.CharField(max_length=100)

class ProductTag(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    tag = models.ForeignKey(Tag, on_delete=models.CASCADE)
```

---

## Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    tags = serializers.SerializerMethodField()

    def get_tags(self, obj):
        return [t.tag.name for t in obj.producttag_set.all()]
```

---

## Problem

```
1 Query → Products
+ 100 Queries → producttag_set
```

---

## Fix:

```python
queryset = Product.objects.prefetch_related("producttag_set__tag")
```

---

## Result:

```
2 Queries only
```

---

# Rule:

> M2M / Reverse FK → `prefetch_related()`

---

# Part 4: SerializerMethodField Danger (BIG INTERVIEW TOPIC)

## Problem Example:

```python
def get_review_count(self, obj):
    return obj.reviews.count()
```

---

## If 100 products:

```
1 query → products
100 queries → reviews.count()
```

---

## Solution (Best Practice):

```python
queryset = Product.objects.annotate(
    review_count=Count("reviews")
)
```

Serializer:

```python
review_count = serializers.IntegerField(read_only=True)
```

---

✔ 1 query only
✔ fastest approach

---

# Part 5: annotate vs serializer

| Case             | Use                   |
| ---------------- | --------------------- |
| Count            | annotate              |
| Sum              | annotate              |
| Avg              | annotate              |
| Exists           | annotate              |
| Simple attribute | source                |
| Custom logic     | SerializerMethodField |

---

# Part 6: Real Production Example (E-commerce)

```python
queryset = Product.objects.select_related(
    "category",
    "seller"
).prefetch_related(
    "tags"
).annotate(
    review_count=Count("reviews"),
    avg_rating=Avg("reviews__rating")
)
```

---

## Serializer:

```python
class ProductSerializer(serializers.ModelSerializer):

    category_name = serializers.CharField(source="category.name", read_only=True)
    seller_name = serializers.CharField(source="seller.username", read_only=True)

    class Meta:
        model = Product
        fields = "__all__"
```

---

✔ 1 Query optimized API
✔ Production ready

---

# Part 7: Common Beginner Mistakes

## ❌ Mistake 1

SerializerMethodField everywhere

→ kills performance

---

## ❌ Mistake 2

select_related না জানা

---

## ❌ Mistake 3

prefetch_related না ব্যবহার করা

---

## ❌ Mistake 4

list API + nested serializer + no optimization

→ API slow 10x

---

## ❌ Mistake 5

Debug না করা

---

# Part 8: How to Debug Queries

## Django Debug

```python
from django.db import connection

print(len(connection.queries))
```

---

## Better Tool:

* Django Debug Toolbar (best)
* Silk profiler

---

# Part 9: Golden Rules (Senior Level)

## Rule 1:

```text
FK → select_related
```

## Rule 2:

```text
M2M / reverse FK → prefetch_related
```

## Rule 3:

```text
Aggregation → annotate
```

## Rule 4:

```text
SerializerMethodField → last option
```

## Rule 5:

```text
Never trust default queryset in production
```

---

# Part 10: Real Interview Questions

### Q1: N+1 problem কী?

Answer:

Multiple queries generated for related objects due to lazy loading.

---

### Q2: select_related vs prefetch_related difference?

| select_related | prefetch_related |
| -------------- | ---------------- |
| SQL JOIN       | separate query   |
| FK             | M2M / reverse    |

---

### Q3: SerializerMethodField কেন avoid করা উচিত?

Because:

* extra DB hits
* poor performance
* not scalable

---

# Homework (Important)

একটি Product API বানান:

### Requirements:

* category (FK)
* seller (FK)
* tags (M2M)
* review_count (annotate)
* avg_rating (annotate)

### Must:

* use select_related
* use prefetch_related
* avoid SerializerMethodField for DB queries

---

# Next Lesson (Lesson 10)

👉 **ViewSet + Router Deep Dive**

আপনি শিখবেন:

* ModelViewSet internal working
* Router auto URL generation
* Custom actions (@action)
* CRUD flow deep understanding
* real API architecture design

---

আপনি চাইলে আমি এখন আপনার জন্য **Mini Project (E-commerce API optimized version)** design করে দিতে পারি — যেখানে এই সব optimization একসাথে ব্যবহার হবে।
# Lesson 10: ViewSet + Router Deep Dive (DRF Architecture Core)

এটা DRF-এর **backend architecture backbone**।
এখান থেকে আপনি বুঝবেন:

> “কিভাবে Django REST Framework automatic CRUD API বানায়”

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* ViewSet কীভাবে কাজ করে
* `ModelViewSet` internally কী করে
* Router কীভাবে URL auto-generate করে
* `list`, `retrieve`, `create`, `update`, `destroy` flow
* `@action` custom endpoint
* Manual API vs ViewSet comparison
* Real production API structure

---

# Part 1: ViewSet কী?

## Traditional API (APIView)

```python id="zqk8b4"
class ProductListView(APIView):

    def get(self, request):
        pass

    def post(self, request):
        pass
```

---

## Problem:

* বেশি boilerplate code
* repeated logic
* scalability problem

---

# ViewSet Solution

```python id="n8f2jv"
class ProductViewSet(viewsets.ViewSet):
    pass
```

---

But real power আসে:

```python id="kq3p8x"
ModelViewSet
```

---

# Part 2: ModelViewSet (IMPORTANT)

```python id="7h2l0m"
class ProductViewSet(viewsets.ModelViewSet):

    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

## এতটুকুই লিখে আপনি পান:

```text id="q3v7xp"
GET     /products/        → list
POST    /products/        → create
GET     /products/1/      → retrieve
PUT     /products/1/      → update
PATCH   /products/1/      → partial_update
DELETE  /products/1/      → destroy
```

👉 Zero extra code

---

# Part 3: Internal Flow (VERY IMPORTANT)

## list()

```python id="p7v0kq"
def list(self, request):
    queryset = self.get_queryset()
    serializer = self.get_serializer(queryset, many=True)
    return Response(serializer.data)
```

---

## retrieve()

```python id="8m2vny"
def retrieve(self, request, pk=None):
    obj = self.get_object()
    serializer = self.get_serializer(obj)
    return Response(serializer.data)
```

---

## create()

```python id="t6w1rp"
def create(self, request):
    serializer = self.get_serializer(data=request.data)
    serializer.is_valid(raise_exception=True)
    serializer.save()
```

---

👉 সব DRF magic এখানেই ঘটে

---

# Part 4: Router (URL Auto Generator)

## Without Router

```python id="c9x2dw"
urlpatterns = [
    path("products/", ProductListView.as_view()),
    path("products/<int:pk>/", ProductDetailView.as_view()),
]
```

---

## With Router

```python id="v3k9pq"
router = DefaultRouter()
router.register("products", ProductViewSet)

urlpatterns = router.urls
```

---

## Auto Generated URLs

```text id="x2v8qm"
/products/          (list, create)
/products/{id}/     (retrieve, update, delete)
```

---

# Part 5: Router Types

## 1. DefaultRouter

* auto root API view দেখায়
* best for production

## 2. SimpleRouter

* no root API page
* clean API only

---

# Part 6: lookup_field (VERY IMPORTANT)

Default:

```text id="m8v2qp"
/products/1/
```

Custom:

```python id="b7q1lv"
class ProductViewSet(ModelViewSet):
    lookup_field = "slug"
```

Now URL:

```text id="s3k9qz"
/products/laptop-apple-m1/
```

---

# Part 7: Custom Action (@action)

## Example: Product Discount API

```python id="w2p9kt"
from rest_framework.decorators import action
from rest_framework.response import Response
```

---

```python id="d8x1qv"
class ProductViewSet(ModelViewSet):

    @action(detail=True, methods=["post"])
    def apply_discount(self, request, pk=None):

        product = self.get_object()

        discount = request.data.get("discount", 0)

        product.price -= discount
        product.save()

        return Response({
            "message": "Discount applied",
            "new_price": product.price
        })
```

---

## URL:

```text id="p9v7mx"
POST /products/1/apply_discount/
```

---

# Types of @action

| Type         | URL                 |
| ------------ | ------------------- |
| detail=True  | /products/1/action/ |
| detail=False | /products/action/   |

---

# Part 8: ViewSet vs APIView

| Feature          | APIView | ViewSet   |
| ---------------- | ------- | --------- |
| Boilerplate      | High    | Low       |
| CRUD             | Manual  | Automatic |
| Routing          | Manual  | Router    |
| Flexibility      | High    | Medium    |
| Production usage | Medium  | High      |

---

# Part 9: Real Project Architecture

## E-commerce structure

```text id="q8k1mv"
ProductViewSet
CategoryViewSet
OrderViewSet
UserViewSet
```

Router:

```python id="c1m8xp"
router.register("products", ProductViewSet)
router.register("categories", CategoryViewSet)
router.register("orders", OrderViewSet)
```

---

# Part 10: Best Practices (Senior Level)

## 1. Always use ModelViewSet for CRUD

```python id="k2v9xq"
class ProductViewSet(ModelViewSet):
```

---

## 2. Override only when needed

```python id="t9p2qm"
def perform_create(self, serializer):
    serializer.save(user=self.request.user)
```

---

## 3. Use select_related inside queryset

```python id="m3v8pq"
queryset = Product.objects.select_related("category")
```

---

## 4. Use @action only for business logic

❌ Bad:

* CRUD in @action

✔ Good:

* apply_discount
* checkout
* approve_order

---

# Part 11: Common Mistakes

## ❌ Mistake 1

ViewSet ব্যবহার করে manual logic লিখা

---

## ❌ Mistake 2

Router না বুঝে random URL expect করা

---

## ❌ Mistake 3

@action misuse

---

## ❌ Mistake 4

lookup_field ভুল ব্যবহার

---

# Part 12: Interview Questions

### Q1: ViewSet কী?

Answer:
A class that provides CRUD actions automatically mapped to HTTP methods.

---

### Q2: ModelViewSet কী দেয়?

Answer:

* list
* retrieve
* create
* update
* destroy

---

### Q3: Router কী করে?

Answer:

Automatically generates URLs for ViewSet.

---

### Q4: @action কেন ব্যবহার করা হয়?

Answer:

Custom business logic endpoint তৈরি করতে।

---

# Part 13: Real E-commerce Example

```python id="r4m9kp"
class OrderViewSet(ModelViewSet):

    queryset = Order.objects.all()
    serializer_class = OrderSerializer

    @action(detail=True, methods=["post"])
    def cancel_order(self, request, pk=None):

        order = self.get_object()
        order.status = "cancelled"
        order.save()

        return Response({"message": "Order cancelled"})
```

---

# Homework

একটি Product API বানান:

### Requirements:

* ModelViewSet ব্যবহার
* Router register করতে হবে
* Custom action:

  * `/products/{id}/activate/`
  * `/products/{id}/deactivate/`
* lookup_field = "slug"
* select_related use করতে হবে

---

# Next Lesson (Lesson 11)

👉 **Authentication + Permission System (DRF Security Core)**

আপনি শিখবেন:

* Authentication vs Permission
* Token Authentication
* JWT flow deep understanding
* IsAuthenticated vs IsAdminUser
* Custom permission class
* Real production security design

---

আপনি চাইলে আমি পরের lesson-এর আগে একটা **Mini E-commerce DRF architecture diagram** বানিয়ে দিতে পারি যাতে সব ViewSet + Router flow একসাথে clear হয়।
# Lesson 11: Authentication + Permission System (DRF Security Core)

এটা DRF-এর **সবচেয়ে গুরুত্বপূর্ণ security layer**।

> API বানানো সহজ, কিন্তু API secure করা হলো real skill।

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* Authentication vs Permission পার্থক্য
* DRF Authentication flow কীভাবে কাজ করে
* Token Authentication কী
* JWT কীভাবে কাজ করে (conceptually)
* `IsAuthenticated`, `IsAdminUser`
* Custom Permission class
* Real production security design

---

# Part 1: Authentication vs Permission (VERY IMPORTANT)

| Concept        | Meaning                               |
| -------------- | ------------------------------------- |
| Authentication | আপনি কে? (identity)                   |
| Permission     | আপনি কী করতে পারবেন? (access control) |

---

## Example:

* Login = Authentication
* Admin dashboard access = Permission

---

# Part 2: DRF Authentication Flow

```text id="a1k8m2"
Request
   ↓
Authentication class runs
   ↓
request.user set হয়
   ↓
Permission check হয়
   ↓
View execute হয়
```

---

## request.user কোথা থেকে আসে?

DRF middleware + authentication backend set করে:

```python id="m9x2pq"
request.user
request.auth
```

---

# Part 3: Token Authentication

## Step 1: install

```bash id="v3k8qz"
pip install djangorestframework
```

---

## settings.py

```python id="p2m8xq"
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.TokenAuthentication",
    ]
}
```

---

## Step 2: migrate

```bash id="c8v1mq"
python manage.py migrate
```

---

## Step 3: create token

```python id="k7p9xz"
from rest_framework.authtoken.models import Token

token = Token.objects.create(user=user)
```

---

## Response

```json id="t4m9qp"
{
    "token": "abc123xyz"
}
```

---

## Client request

```http id="r9x2mv"
Authorization: Token abc123xyz
```

---

# Part 4: JWT (Concept)

JWT = JSON Web Token

Structure:

```text id="j1k9pq"
Header.Payload.Signature
```

---

## Flow:

```text id="z8v2mq"
Login → JWT generate
      ↓
Frontend stores token
      ↓
Every request sends token
      ↓
Backend verifies token
```

---

## Why JWT used?

✔ Stateless
✔ Scalable
✔ Microservice friendly

---

# Part 5: Permission Classes

## 1. AllowAny (default)

```python id="b8k2pq"
permission_classes = [AllowAny]
```

👉 সবাই access করতে পারবে

---

## 2. IsAuthenticated

```python id="x7m9qp"
permission_classes = [IsAuthenticated]
```

👉 শুধু logged-in user

---

## 3. IsAdminUser

```python id="q2v8mz"
permission_classes = [IsAdminUser]
```

👉 শুধু admin

---

# Part 6: ViewSet Example

```python id="c9p2xq"
from rest_framework.permissions import IsAuthenticated

class ProductViewSet(ModelViewSet):

    permission_classes = [IsAuthenticated]

    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

# Part 7: Custom Permission (VERY IMPORTANT)

## Example: Only owner can edit

```python id="m8x1pq"
from rest_framework.permissions import BasePermission
```

---

```python id="v2k9mz"
class IsOwner(BasePermission):

    def has_object_permission(self, request, view, obj):

        return obj.owner == request.user
```

---

## Use:

```python id="p7m2xq"
permission_classes = [IsAuthenticated, IsOwner]
```

---

# Part 8: Object-level vs Global Permission

| Type         | Meaning              |
| ------------ | -------------------- |
| Global       | view-level access    |
| Object-level | single object access |

---

## Example:

```python id="k9v2mq"
GET /products/1/
```

👉 IsAuthenticated passes
👉 IsOwner checks specific product

---

# Part 9: Real Production Pattern

## Blog System

```python id="z3m8pq"
class BlogViewSet(ModelViewSet):

    permission_classes = [IsAuthenticated]

    def perform_create(self, serializer):
        serializer.save(author=self.request.user)
```

---

## Why perform_create?

✔ Cleaner than serializer
✔ Security controlled in backend
✔ No user spoofing possible

---

# Part 10: Common Mistakes

## ❌ Mistake 1

Frontend থেকে user পাঠানো

```json id="a9k2pq"
{
    "user": 5
}
```

❌ Dangerous

---

## ❌ Mistake 2

permission_classes ভুলভাবে না দেওয়া

---

## ❌ Mistake 3

authentication না setup করা

---

## ❌ Mistake 4

object-level permission ignore করা

---

# Part 11: Authentication Backends

| Type                  | Use         |
| --------------------- | ----------- |
| SessionAuthentication | browser     |
| TokenAuthentication   | simple APIs |
| JWTAuthentication     | modern apps |

---

# Part 12: JWT (Real Flow)

```text id="j9m2pq"
Login
 ↓
Access Token + Refresh Token
 ↓
Access token expires
 ↓
Refresh token used
 ↓
New access token
```

---

# Part 13: Senior Level Security Design

## Example architecture:

```text id="x2k9mq"
ViewSet
   ↓
Permission Layer
   ↓
Service Layer (optional)
   ↓
Model Layer
```

---

## Rule:

> Never trust frontend data for security decisions

---

# Part 14: Real E-commerce Example

```python id="c8m9pq"
class OrderViewSet(ModelViewSet):

    permission_classes = [IsAuthenticated]

    def perform_create(self, serializer):
        serializer.save(user=self.request.user)
```

---

# Part 15: Interview Questions

### Q1: Authentication vs Permission?

Authentication = user identity
Permission = user access level

---

### Q2: request.user কোথা থেকে আসে?

Authentication backend থেকে

---

### Q3: Why custom permission?

Business rules enforce করতে

---

### Q4: perform_create কেন ব্যবহার করি?

Security + clean architecture

---

# Part 16: Best Practices (Senior Level)

✔ Always use authentication in production
✔ Never trust request.user from frontend
✔ Use object-level permission for sensitive data
✔ Use perform_create for ownership
✔ Combine permissions (IsAuthenticated + Custom)

---

# Homework

একটি Blog API বানান:

### Requirements:

* Only logged-in user can create blog
* Only author can edit/delete blog
* Public can read blog
* Use custom permission `IsAuthor`
* auto assign author in perform_create

---

# Next Lesson (Lesson 12)

👉 **Advanced DRF Architecture (Service Layer + Clean Code Design)**

আপনি শিখবেন:

* Serializer vs Service layer separation
* Fat serializer problem
* Clean architecture design
* Large project structure (E-commerce level)
* Real-world folder structure

---

আপনি চাইলে আমি next lesson-এর আগে একটা **full DRF project architecture blueprint (Senior level folder structure)** বানিয়ে দিতে পারি।
# Lesson 12: Advanced DRF Architecture (Service Layer + Clean Code Design)

এটা হলো সেই lesson যেটা আপনাকে **“I can build projects” → “I can design systems”** লেভেলে নিয়ে যাবে।

> বড় project (E-commerce, SaaS, Multi-vendor) এ সমস্যা serializer বা view না—problem হয় **bad architecture**।

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* Fat Serializer problem
* Fat View problem
* Service Layer কী
* Clean architecture pattern
* Django project structure (production style)
* Business logic কোথায় রাখা উচিত
* Scalable DRF design

---

# Part 1: Common Beginner Architecture (BAD ❌)

```text id="a1k9pq"
View → Serializer → Model
```

সব logic এখানে ঢুকে যায়।

---

## Example (Bad)

```python id="m9x2pq"
class OrderSerializer(serializers.ModelSerializer):

    def create(self, validated_data):

        items = validated_data.pop("items")

        order = Order.objects.create(**validated_data)

        total = 0

        for item in items:
            total += item["price"] * item["quantity"]

            OrderItem.objects.create(order=order, **item)

        order.total = total
        order.save()

        return order
```

---

## Problem:

* Serializer overloaded
* Hard to test
* Hard to reuse
* Business logic scattered

---

# Part 2: Clean Architecture (GOOD ✅)

```text id="v2k8pq"
View → Serializer → Service Layer → Model
```

---

# Part 3: Service Layer কী?

👉 Service Layer = Business Logic Container

যেখানে রাখা হয়:

* Order calculation
* Payment logic
* Coupon validation
* Stock management
* Complex workflow

---

# Part 4: Refactor Example (Order System)

## Step 1: Serializer (Clean)

```python id="c8m2pq"
class OrderSerializer(serializers.ModelSerializer):

    class Meta:
        model = Order
        fields = "__all__"
```

👉 শুধু validation + data transfer

---

## Step 2: Service Layer

📁 services/order_service.py

```python id="k9v2mq"
from django.db import transaction

class OrderService:

    @staticmethod
    def create_order(user, items):

        with transaction.atomic():

            order = Order.objects.create(user=user, total=0)

            total = 0

            for item in items:

                OrderItem.objects.create(
                    order=order,
                    product=item["product"],
                    quantity=item["quantity"],
                    price=item["price"]
                )

                total += item["price"] * item["quantity"]

            order.total = total
            order.save()

            return order
```

---

## Step 3: View

```python id="x7m9qp"
class OrderViewSet(ModelViewSet):

    serializer_class = OrderSerializer
    queryset = Order.objects.all()

    def create(self, request, *args, **kwargs):

        items = request.data.pop("items")

        order = OrderService.create_order(
            user=request.user,
            items=items
        )

        serializer = self.get_serializer(order)

        return Response(serializer.data)
```

---

# Part 5: Benefits of Service Layer

✔ Reusable code
✔ Testable
✔ Clean View
✔ Clean Serializer
✔ Easy debugging
✔ Scalable architecture

---

# Part 6: Real Production Folder Structure

```text id="r8v2mq"
project/
│
├── apps/
│   ├── users/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── services/
│   │   │     └── user_service.py
│   │   ├── urls.py
│   │
│   ├── orders/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── services/
│   │   │     └── order_service.py
│   │
│   ├── products/
│       ├── models.py
│       ├── serializers.py
│       ├── views.py
│       ├── services/
│
├── core/
│   ├── permissions.py
│   ├── utils.py
│
└── config/
    ├── settings.py
    ├── urls.py
```

---

# Part 7: Fat Problems Explained

## ❌ Fat Serializer

* validation + business logic + DB logic

## ❌ Fat View

* API + business logic + calculations

---

## ✔ Clean System

| Layer      | Responsibility   |
| ---------- | ---------------- |
| Serializer | validation       |
| View       | request/response |
| Service    | business logic   |
| Model      | data             |

---

# Part 8: Real Example (Coupon System)

## BAD ❌

```python id="a9k2pq"
def validate_coupon(self, value):
    if not Coupon.objects.filter(code=value).exists():
        raise ValidationError("Invalid coupon")
```

---

## GOOD ✅ (Service Layer)

```python id="m2k9pq"
class CouponService:

    @staticmethod
    def validate_coupon(code, user):

        coupon = Coupon.objects.filter(code=code, is_active=True).first()

        if not coupon:
            raise Exception("Invalid coupon")

        if coupon.used_by.filter(id=user.id).exists():
            raise Exception("Already used")

        return coupon
```

---

# Part 9: Transaction Strategy

Always use:

```python id="t8v2mq"
with transaction.atomic():
```

When:

* Order creation
* Payment
* Inventory update
* Multi-table write

---

# Part 10: When to Use Service Layer?

✔ Complex logic
✔ Multiple models involved
✔ Reusable logic
✔ Payment system
✔ Order system
✔ Authentication workflows

---

# Part 11: When NOT to use Service Layer?

❌ Simple CRUD
❌ Single model save
❌ Basic API

---

# Part 12: Interview Questions

### Q1: Why service layer?

Answer:

To separate business logic from view/serializer for scalability and maintainability.

---

### Q2: Difference between view and service layer?

| View             | Service        |
| ---------------- | -------------- |
| HTTP logic       | Business logic |
| Request/Response | Processing     |

---

### Q3: Why not put logic in serializer?

Because:

* hard to test
* not reusable
* becomes messy

---

# Part 13: Senior-Level Architecture Rule

> “Serializer validates, View controls flow, Service handles logic.”

---

# Part 14: Real E-commerce Flow

```text id="k3v9mq"
Request
  ↓
ViewSet
  ↓
Serializer (validation only)
  ↓
Service Layer (business logic)
  ↓
Models
  ↓
Response
```

---

# Part 15: Common Mistakes

❌ Everything in serializer
❌ No separation of concerns
❌ No transaction usage
❌ Duplicate logic in multiple views
❌ No reusable service layer

---

# Homework (VERY IMPORTANT)

একটি E-commerce Order system design করুন:

### Requirements:

* OrderService বানাতে হবে
* CouponService বানাতে হবে
* Inventory update service
* ViewSet minimal রাখতে হবে
* transaction.atomic ব্যবহার করতে হবে

---

# Next Lesson (Lesson 13)

👉 **Advanced DRF Patterns (Real World Scaling)**

আপনি শিখবেন:

* Large scale API design
* Multi-app communication
* Async vs Sync API thinking
* Pagination strategy
* Rate limiting
* API versioning

---

আপনি চাইলে আমি next lesson-এর আগে আপনার জন্য একটা **Full Professional Django REST Framework Project Blueprint (like Amazon architecture)** বানিয়ে দিতে পারি।
# Lesson 13: Advanced DRF Patterns (Real-World Scaling Architecture)

এটা সেই lesson যেটা আপনাকে “project বানাতে পারি” থেকে **“production system design করতে পারি”** লেভেলে নিয়ে যাবে।

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* Large scale API design কীভাবে করা হয়
* API versioning কেন দরকার
* Pagination strategy (real production)
* Rate limiting (throttling)
* Caching basics in DRF
* Multi-app architecture thinking
* Scalable API design pattern

---

# Part 1: Real Problem in Large Projects

ছোট project:

```
1 app → 5 API → simple flow
```

Large project:

```
users
products
orders
payments
reviews
notifications
analytics
```

👉 Problem: everything becomes slow + messy

---

# Part 2: API Versioning (VERY IMPORTANT)

## Why needed?

Frontend change হলে backend break না হওয়া দরকার।

---

## Example:

```text id="v1"
api/v1/products/
```

```text id="v2"
api/v2/products/
```

---

## DRF Setup

```python id="k1v9mq"
REST_FRAMEWORK = {
    "DEFAULT_VERSIONING_CLASS": "rest_framework.versioning.URLPathVersioning",
    "DEFAULT_VERSION": "v1"
}
```

---

## ViewSet

```python id="m2v8pq"
class ProductViewSet(ModelViewSet):

    def get_queryset(self):

        if self.request.version == "v2":
            return Product.objects.filter(is_active=True)

        return Product.objects.all()
```

---

# Part 3: Pagination Strategy (VERY IMPORTANT)

## Problem:

```text id="p1"
100000 products → API crash / slow
```

---

## Solution:

### 1. PageNumberPagination

```python id="p2v8mq"
class StandardPagination(PageNumberPagination):
    page_size = 10
```

---

### 2. LimitOffsetPagination

```text id="p3"
?limit=10&offset=20
```

---

### 3. CursorPagination (BEST for large data)

```python id="p4v8mq"
class ProductPagination(CursorPagination):
    page_size = 10
    ordering = "-created_at"
```

---

## When to use?

| Type        | Use case                           |
| ----------- | ---------------------------------- |
| PageNumber  | small apps                         |
| LimitOffset | admin panels                       |
| Cursor      | large scale apps (Amazon, Netflix) |

---

# Part 4: Rate Limiting (Throttling)

## Why needed?

* API abuse prevent
* server protection
* fair usage

---

## DRF Setup:

```python id="t1v9mq"
REST_FRAMEWORK = {
    "DEFAULT_THROTTLE_CLASSES": [
        "rest_framework.throttling.UserRateThrottle",
        "rest_framework.throttling.AnonRateThrottle",
    ],
    "DEFAULT_THROTTLE_RATES": {
        "user": "100/day",
        "anon": "20/day"
    }
}
```

---

## Custom throttle:

```python id="t2v8mq"
class BurstThrottle(UserRateThrottle):
    rate = "10/min"
```

---

# Part 5: Caching in DRF

## Problem:

```text id="c1"
same API → same DB query → repeated load
```

---

## Solution:

```python id="c2v8mq"
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator
```

---

```python id="c3"
@method_decorator(cache_page(60 * 5), name="dispatch")
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

## Result:

* first request → DB hit
* next 5 min → cache hit

---

# Part 6: Multi-App Architecture (VERY IMPORTANT)

## Bad structure:

```
everything in one app
```

---

## Good structure:

```
users/
products/
orders/
payments/
core/
```

---

## Why?

✔ scalability
✔ team development
✔ easier debugging
✔ independent deployment thinking

---

# Part 7: Service Layer + API Flow (FINAL ARCHITECTURE)

Production flow:

```text id="f1"
Request
 ↓
ViewSet (thin)
 ↓
Serializer (validation only)
 ↓
Service Layer (business logic)
 ↓
Models
 ↓
Response
```

---

# Part 8: API Design Best Practices

## 1. Keep ViewSet thin

❌ Bad:
business logic in view

✔ Good:
call service layer

---

## 2. Keep serializer simple

❌ No heavy DB logic

---

## 3. Use annotate for performance

---

## 4. Avoid deep nesting in list APIs

---

## 5. Use caching for heavy reads

---

# Part 9: Real E-commerce Example

## Products API

```python id="e1"
queryset = Product.objects.select_related(
    "category",
    "seller"
).prefetch_related(
    "tags"
).annotate(
    review_count=Count("reviews")
)
```

---

## ViewSet

```python id="e2"
class ProductViewSet(ModelViewSet):

    serializer_class = ProductSerializer
    queryset = Product.objects.all()

    def get_queryset(self):

        return (
            Product.objects
            .select_related("category", "seller")
            .prefetch_related("tags")
            .annotate(review_count=Count("reviews"))
        )
```

---

# Part 10: Common Mistakes

## ❌ Mistake 1

No pagination → API crash

---

## ❌ Mistake 2

No caching → slow response

---

## ❌ Mistake 3

Everything in one app

---

## ❌ Mistake 4

No versioning → frontend break

---

## ❌ Mistake 5

Heavy SerializerMethodField usage

---

# Part 11: Interview Questions

### Q1: Why API versioning?

Answer:
To maintain backward compatibility.

---

### Q2: Best pagination for large data?

Answer:
CursorPagination.

---

### Q3: Why caching needed?

Answer:
Reduce DB load and improve response time.

---

### Q4: What is throttling?

Answer:
Rate limiting API usage to prevent abuse.

---

# Part 12: Senior-Level Rules

✔ Always paginate list APIs
✔ Always optimize queryset
✔ Use caching for heavy reads
✔ Use versioning in production
✔ Keep ViewSet thin
✔ Avoid logic duplication

---

# Homework

একটি scalable Product API design করুন:

### Requirements:

* API versioning (/v1/)
* Cursor pagination
* caching enabled
* optimized queryset
* rate limit (user + anon)
* service layer use করুন (optional)

---

# Next Lesson (Lesson 14)

👉 **Testing + Debugging + Production Deployment Thinking**

আপনি শিখবেন:

* DRF testing (APITestCase)
* API debugging techniques
* Postman vs automated test
* logging system
* production deployment basics (Gunicorn, Nginx concept)

---

আপনি চাইলে আমি next lesson-এর আগে আপনাকে একটি **“Complete Production DRF Architecture Blueprint (Amazon-style)”** diagram বানিয়ে দিতে পারি—যেটা সব lesson একসাথে connect করবে।
# Lesson 14: Testing + Debugging + Production Thinking (DRF Professional Level)

এটা সেই lesson যেটা আপনাকে **“I can build APIs” → “I can ship production APIs safely”** লেভেলে নিয়ে যাবে।

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* DRF Testing (APITestCase)
* API testing strategy
* Debugging techniques (real production)
* Logging system basics
* Common API failures detect করা
* Production deployment mindset (Gunicorn + Nginx concept)

---

# Part 1: Why Testing Matters?

Without testing:

```text id="t1"
API works in my machine ❌
breaks in production ❌
data corrupt ❌
bugs unknown ❌
```

With testing:

```text id="t2"
safe deploy ✔
stable API ✔
less bugs ✔
confident development ✔
```

---

# Part 2: DRF Testing Setup

## Import

```python id="a1"
from rest_framework.test import APITestCase
from rest_framework import status
from django.urls import reverse
```

---

## Basic Test Structure

```python id="a2"
class ProductAPITest(APITestCase):

    def setUp(self):
        self.url = "/api/products/"
```

---

# Part 3: Create API Test

```python id="a3"
def test_create_product(self):

    data = {
        "name": "Laptop",
        "price": 50000
    }

    response = self.client.post(self.url, data, format="json")

    self.assertEqual(response.status_code, status.HTTP_201_CREATED)
```

---

# Part 4: List API Test

```python id="a4"
def test_product_list(self):

    response = self.client.get(self.url)

    self.assertEqual(response.status_code, status.HTTP_200_OK)
```

---

# Part 5: Authentication Test

```python id="a5"
from django.contrib.auth.models import User
```

```python id="a6"
def test_auth_required(self):

    response = self.client.get(self.url)

    self.assertEqual(response.status_code, status.HTTP_401_UNAUTHORIZED)
```

---

## Login User

```python id="a7"
def setUp(self):

    self.user = User.objects.create_user(
        username="test",
        password="123456"
    )

    self.client.force_authenticate(user=self.user)
```

---

# Part 6: Object Detail Test

```python id="a8"
def test_product_detail(self):

    product = Product.objects.create(
        name="Laptop",
        price=50000
    )

    url = f"/api/products/{product.id}/"

    response = self.client.get(url)

    self.assertEqual(response.status_code, 200)
```

---

# Part 7: Debugging in DRF

## 1. Print Debugging (Basic)

```python id="d1"
print(serializer.errors)
```

---

## 2. Django Shell Debug

```bash id="d2"
python manage.py shell
```

---

## 3. Logging (PRO LEVEL)

```python id="d3"
import logging

logger = logging.getLogger(__name__)
```

```python id="d4"
logger.info("Product created successfully")
logger.error("Something went wrong")
```

---

## 4. Django Debug Toolbar (Best Tool)

* SQL queries
* API response time
* N+1 detection

---

# Part 8: Common API Failures

## ❌ 1. Serializer errors

```json id="e1"
{
  "name": ["This field is required."]
}
```

---

## ❌ 2. Permission errors

```json id="e2"
401 Unauthorized
```

---

## ❌ 3. Query error

```text id="e3"
DoesNotExist exception
```

---

## ❌ 4. N+1 query slow API

---

# Part 9: Production Debugging Strategy

## Step 1: Check logs

```text id="p1"
error.log
access.log
```

---

## Step 2: Check DB queries

```python id="p2"
len(connection.queries)
```

---

## Step 3: Check serializer

```python id="p3"
print(serializer.data)
```

---

## Step 4: Check request payload

```python id="p4"
print(request.data)
```

---

# Part 10: Production Deployment Thinking

## Django runs on dev server:

```text id="s1"
python manage.py runserver ❌ (NOT production)
```

---

## Production stack:

```text id="s2"
Client
  ↓
Nginx (Reverse Proxy)
  ↓
Gunicorn (WSGI Server)
  ↓
Django App
  ↓
Database
```

---

# Part 11: Gunicorn (Concept)

```text id="g1"
Gunicorn = Python production server
```

Run:

```bash id="g2"
gunicorn project.wsgi:application
```

---

# Part 12: Nginx (Concept)

Used for:

✔ load balancing
✔ static files
✔ reverse proxy
✔ security

---

# Part 13: Testing Strategy (Senior Level)

## Unit Test

* serializer logic
* service layer

---

## Integration Test

* API + DB

---

## End-to-End Test

* full flow (user → order → payment)

---

# Part 14: Real Project Test Example

```python id="r1"
def test_order_create(self):

    self.client.force_authenticate(user=self.user)

    data = {
        "items": [
            {"product": "Laptop", "quantity": 1, "price": 50000}
        ]
    }

    response = self.client.post("/api/orders/", data, format="json")

    self.assertEqual(response.status_code, 201)
```

---

# Part 15: Best Practices

✔ Always test CRUD APIs
✔ Test authentication
✔ Test permission
✔ Test edge cases
✔ Avoid logic in tests
✔ Keep tests independent

---

# Part 16: Common Mistakes

## ❌ Mistake 1

Only manual Postman testing

---

## ❌ Mistake 2

No authentication test

---

## ❌ Mistake 3

No edge case testing

---

## ❌ Mistake 4

Ignoring logging

---

## ❌ Mistake 5

Testing only happy path

---

# Part 17: Interview Questions

### Q1: Why testing important?

Answer:
To ensure API reliability and prevent production bugs.

---

### Q2: APITestCase vs TestCase?

APITestCase = API support
TestCase = Django model logic

---

### Q3: What is logging?

Tracking application events and errors.

---

### Q4: Why debug toolbar?

To analyze SQL queries and performance.

---

# Part 18: Senior Developer Rule

> “If it’s not tested, it’s not finished.”

---

# Homework

একটি Product API লিখুন এবং test করুন:

### Requirements:

* Create product test
* List product test
* Detail test
* Auth required test
* invalid data test

---

# Next Lesson (Lesson 15)

👉 **Final Advanced Architecture + Real Project Blueprint**

আপনি শিখবেন:

* Full E-commerce system design
* Folder structure (enterprise level)
* Service + View + Serializer integration
* scaling strategy
* production-ready API architecture

---

আপনি চাইলে আমি next lesson-এর আগে আপনার জন্য একটা **“Complete Django REST Framework Production Project Blueprint (Amazon-level architecture)”** একসাথে map করে দিতে পারি।
# Lesson 15: Final Advanced Architecture (Production-Level DRF Blueprint)

এটা আপনার পুরো সিরিজের **capstone lesson**।
এখানে আপনি শিখবেন কীভাবে একটা **real-world production backend system** design করা হয় (Amazon / Daraz / SaaS level thinking)।

---

# Learning Objectives

এই lesson শেষে আপনি বুঝবেন:

* Full DRF project architecture design
* App segmentation (enterprise structure)
* Request flow end-to-end
* Service + Serializer + View integration
* Scalable folder structure
* Real production patterns
* System thinking (Senior Developer mindset)

---

# Part 1: Real Production Problem

Beginner project:

```text id="p1"
1 app → everything inside
```

Problem:

* messy code
* no scalability
* hard to maintain
* team conflict

---

Enterprise project:

```text id="p2"
10+ apps
separated responsibilities
service layer
clean architecture
```

---

# Part 2: Final Architecture (SENIOR LEVEL)

## Folder Structure

```text id="a1"
project/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│
├── apps/
│   │
│   ├── users/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── services/
│   │   │     └── user_service.py
│   │   ├── permissions.py
│   │
│   ├── products/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── services/
│   │   │     └── product_service.py
│   │
│   ├── orders/
│   │   ├── models.py
│   │   ├── serializers.py
│   │   ├── views.py
│   │   ├── services/
│   │   │     └── order_service.py
│   │
│   ├── payments/
│   │
│   ├── reviews/
│   │
│
├── core/
│   ├── permissions.py
│   ├── utils.py
│   ├── exceptions.py
│   ├── pagination.py
│
└── requirements.txt
```

---

# Part 3: Request Flow (IMPORTANT)

```text id="f1"
Client Request
   ↓
URLs (router)
   ↓
ViewSet (thin layer)
   ↓
Serializer (validation only)
   ↓
Service Layer (business logic)
   ↓
Models (DB)
   ↓
Response
```

---

# Part 4: Full Example (Order System)

## 1. View (THIN)

```python id="v1"
class OrderViewSet(ModelViewSet):

    serializer_class = OrderSerializer
    queryset = Order.objects.all()

    def create(self, request, *args, **kwargs):

        order = OrderService.create_order(
            user=request.user,
            items=request.data.get("items", [])
        )

        serializer = self.get_serializer(order)

        return Response(serializer.data)
```

---

## 2. Service Layer (HEAVY LOGIC)

```python id="s1"
from django.db import transaction

class OrderService:

    @staticmethod
    def create_order(user, items):

        with transaction.atomic():

            order = Order.objects.create(
                user=user,
                total=0
            )

            total = 0

            for item in items:

                OrderItem.objects.create(
                    order=order,
                    product=item["product"],
                    quantity=item["quantity"],
                    price=item["price"]
                )

                total += item["price"] * item["quantity"]

            order.total = total
            order.save()

            return order
```

---

## 3. Serializer (CLEAN)

```python id="ser1"
class OrderSerializer(serializers.ModelSerializer):

    class Meta:
        model = Order
        fields = "__all__"
```

---

# Part 5: Core Design Principles

## Rule 1: Thin View

❌ Wrong:

* business logic in view

✔ Right:

* call service only

---

## Rule 2: Dumb Serializer

❌ Wrong:

* DB logic inside serializer

✔ Right:

* only validation

---

## Rule 3: Smart Service Layer

✔ business logic
✔ calculations
✔ workflows
✔ transactions

---

## Rule 4: Fat Models (optional)

✔ helper methods
✔ domain logic (light)

---

# Part 6: Real System Example (Amazon Style)

```text id="sys1"
User
 ↓
Product
 ↓
Cart
 ↓
Order
 ↓
Payment
 ↓
Delivery
 ↓
Review
```

---

# Part 7: API Design Strategy

## Product API

```text id="api1"
/api/v1/products/
```

## Order API

```text id="api2"
/api/v1/orders/
```

## Payment API

```text id="api3"
/api/v1/payments/
```

---

# Part 8: Scaling Strategy

## 1. Query Optimization

✔ select_related
✔ prefetch_related
✔ annotate

---

## 2. Caching

✔ product list
✔ homepage
✔ category list

---

## 3. Pagination

✔ CursorPagination for large data

---

## 4. Rate Limiting

✔ prevent abuse

---

# Part 9: Authentication + Security Layer

```text id="sec1"
Request
 ↓
Authentication
 ↓
Permission
 ↓
View
```

---

## Rule:

> Never trust frontend input

---

# Part 10: Common Senior Mistakes

## ❌ Mistake 1

Everything in one app

---

## ❌ Mistake 2

No service layer

---

## ❌ Mistake 3

Serializer overloaded

---

## ❌ Mistake 4

No pagination

---

## ❌ Mistake 5

No caching strategy

---

# Part 11: Interview-Level Questions

### Q1: Why service layer?

Answer:
To separate business logic from API layer for scalability and maintainability.

---

### Q2: Why thin view?

Answer:
To keep request handling simple and reusable.

---

### Q3: Why separate apps?

Answer:
To maintain modular, scalable architecture.

---

### Q4: What is production-ready API design?

Answer:

* clean architecture
* optimized queries
* authentication + permission
* caching + pagination
* service layer separation

---

# Part 12: Senior Developer Mindset

✔ Think in systems, not endpoints
✔ Think in scalability, not just functionality
✔ Think in maintainability, not just output

---

# Final Summary (Whole Series)

আপনি এখন শিখেছেন:

### Beginner → Advanced DRF Path:

* Serializer basics
* Relationship fields
* Writable nested
* Query optimization
* ViewSet + Router
* Authentication + Permission
* Service layer architecture
* Testing + debugging
* Production design

---

# Final Homework (Capstone Project)

## Build Full E-commerce Backend:

### Must include:

* User system
* Product system
* Order system
* Payment system (mock)
* Review system
* Service layer everywhere
* API versioning
* Pagination
* Authentication + permissions
* Optimized queries

---

# Next Step (If you continue)

আমি আপনাকে এখন guide করতে পারি:

👉 **Full Real E-commerce Project (Step-by-step coding)**
👉 **GitHub-ready professional backend structure**
👉 **Interview preparation (DRF + Python backend)**

Just বললেই আমি আপনার জন্য next level roadmap বানিয়ে দেব।
