এটাই Django Developer-এর সবচেয়ে গুরুত্বপূর্ণ skill।

**অনেকেই Django শিখে View, Serializer, API বানাতে পারে। কিন্তু Senior Developer-দের আলাদা করে Model Design।**

আমার মতে Model design করার সময় এই thinking process follow করলে তুমি যেকোনো project-এর database design করতে পারবে।

---

# Django Model Design Thinking (Senior Mindset)

## Step 1: Business Requirement বুঝো (Database না)

❌ Beginner

> "একটা Product model বানাই।"

✅ Senior

> "Business কী চায়?"

Example

E-commerce

Business requirement

* Seller product add করবে
* Buyer order করবে
* Product multiple image থাকবে
* Product multiple category হতে পারবে
* Product review থাকবে
* Inventory track হবে

এখন model বের হবে।

---

## Step 2: Entity বের করো

নিজেকে প্রশ্ন করো

**Noun খুঁজো।**

Sentence

> Customer places Order using Address.

Entity

* Customer
* Order
* Address

আরেকটা

Seller uploads Product.

Entity

* Seller
* Product

Blog

* User
* Post
* Category
* Comment
* Tag

---

## Step 3: Relationship চিন্তা করো

প্রথমেই relation draw করো।

```
User
 |
 | 1
 |
 *
Product
```

মানে

One User → Many Products

অর্থাৎ

```
ForeignKey(User)
```

---

Many To Many?

```
Post

Python
Django
AI
```

একটা Post

অনেক Tag

একটা Tag

অনেক Post

```
ManyToManyField
```

---

One To One?

```
User

↓

Profile
```

```
OneToOneField
```

---

## Step 4: Data Ownership

নিজেকে জিজ্ঞেস করো

এই data কার?

Example

Address

```
User
```

নাকি

```
Order
```

অনেক Beginner

Address User এ রাখে।

Senior ভাবে

Order delivery address future change হতে পারবে।

তাই

```
Order
    delivery_name
    delivery_phone
    delivery_address
```

Snapshot রাখবে।

---

## Step 5: Normalization

এক data দুই জায়গায় রাখবে না।

Bad

```
Order

product_name
product_price
product_image
```

ভালো

```
OrderItem

product = FK(Product)
```

কিন্তু

Price?

Senior Thinking

Price change হতে পারে।

তাই

```
OrderItem

product
price
quantity
```

এখানে price copy করা হবে।

এটা intentional denormalization।

---

## Step 6: Future Change চিন্তা করো

আজকে দরকার নেই।

কাল লাগবে।

Example

Product

```
price
```

Future

Discount

Offer

Coupon

Tax

Currency

তাহলে

```
ProductPrice
```

আলাদা model হতে পারে।

---

## Step 7: Reusable Model

সব model এ

```
created_at
updated_at
```

থাকবে।

BaseModel

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

---

সব model

```
class Product(BaseModel):
```

---

## Step 8: Nullable না Required?

প্রশ্ন করো

Business এ এটা ছাড়া record create করা যাবে?

Example

```
title
```

Required

```
null=False
blank=False
```

Description?

Optional

```
blank=True
```

---

## Step 9: Choice নাকি আলাদা Model?

Status

```
Pending

Paid

Cancelled
```

Choice যথেষ্ট।

```python
STATUS = [
    ("pending", "Pending"),
    ("paid", "Paid"),
]
```

কিন্তু

Country

Department

Category

Dynamic

তাহলে

আলাদা model।

---

## Step 10: Delete হলে কী হবে?

সবচেয়ে important।

নিজেকে জিজ্ঞেস করো

User delete হলে

Order?

Product?

Comment?

কি হবে?

Example

```
Order

user = FK(
    User,
    on_delete=models.PROTECT
)
```

কারণ

Order history হারানো যাবে না।

---

Comment

```
CASCADE
```

হতে পারে।

---

Product

```
PROTECT
```

হতে পারে।

---

## Step 11: Query Pattern আগে ভাবো

খুব গুরুত্বপূর্ণ।

নিজেকে জিজ্ঞেস করো

Most frequent query কী?

Example

```
Latest Products
```

তাহলে

```
created_at
```

index।

---

Search

```
slug
```

unique।

---

Email login

```
email
```

unique index।

---

## Step 12: Model ছোট রাখো

Bad

```
Product

price

discount

tax

shipping

seller

inventory

review_count

rating

wishlist_count

sales

views

...
```

ভালো

```
Product

Inventory

ProductImage

Review

PriceHistory

StockMovement
```

---

# Model Design Checklist

প্রতিটি Model বানানোর আগে নিজেকে জিজ্ঞেস করো:

* Business requirement কী?
* এই Entity সত্যিই আলাদা Model হওয়া উচিত?
* Relationship কী? (One-to-One, One-to-Many, Many-to-Many)
* Data-এর মালিক কে?
* Duplicate data হচ্ছে কি?
* ভবিষ্যতে এই structure পরিবর্তন লাগতে পারে?
* কোন field required, কোনটি optional?
* `on_delete` কী হবে এবং কেন?
* সবচেয়ে বেশি কোন query চলবে?
* Index দরকার?
* Unique constraint দরকার?
* Model কি খুব বড় হয়ে যাচ্ছে? ভেঙে ছোট করা উচিত?

# Real Senior Thinking Example (E-commerce)

Business:

> একজন Seller Product বিক্রি করবে।

**অনেকে সরাসরি এভাবে শুরু করে:**

```python
class Product(models.Model):
    title = models.CharField(max_length=255)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

**Senior developer আগে প্রশ্ন করে:**

1. Product-এর মালিক কে? → `Seller`
2. Product-এর একাধিক ছবি থাকবে? → `ProductImage`
3. বিভিন্ন Variant থাকবে (Size/Color)? → `ProductVariant`
4. Stock কোথায় থাকবে? → `Inventory` বা Variant-এ
5. Review লাগবে? → `Review`
6. Category একাধিক হতে পারে? → `ManyToMany`
7. Soft delete দরকার? → `is_active` বা `deleted_at`
8. Slug দরকার? → SEO ও URL-এর জন্য
9. Price ভবিষ্যতে পরিবর্তন হবে? → Price history বা snapshot strategy
10. Query কী হবে? → Seller-এর product, category-wise product, latest product, search

তারপর Model design শুরু করে।

---

## তোমার জন্য Mastery Roadmap

তুমি যেহেতু Django REST Framework-এ দক্ষ হতে চাও, আমি এই ক্রমে Model Design শিখতে বলব:

1. Field types (`CharField`, `DecimalField`, `JSONField`, `UUIDField` ইত্যাদি)
2. Relationships (`ForeignKey`, `OneToOneField`, `ManyToManyField`)
3. `Meta` options (`ordering`, `indexes`, `constraints`, `db_table`)
4. Managers ও `QuerySet`
5. Model methods (`__str__`, `get_absolute_url`, custom methods)
6. Database normalization বনাম intentional denormalization
7. Performance (`select_related`, `prefetch_related`-বান্ধব design)
8. Real-world schema design (Blog → E-commerce → Multi-vendor → SaaS → ERP)

**আমার পরামর্শ:** API শেখার আগে যদি তুমি ৩০–৪০টি ভিন্ন business-এর database/model design নিজে করতে পারো, তাহলে Django Model-এ তোমার চিন্তাধারা অনেক শক্তিশালী হবে। তখন নতুন project পেলেও model design করা অনেক সহজ লাগবে।


---
অবশ্যই। আমরা **Zero → Senior Django Model Design Mastery** কোর্স শুরু করব।

**Rule:** প্রতিটি lesson শেষ না করে পরের lesson-এ যাব না। আমি শুধু theory বলব না, কেন ব্যবহার করা হয়, beginner mistake, senior thinking, interview question, এবং real project example সব দেখাব।

---

# Django Model Design Mastery

## Lesson 1: Model আসলে কী?

---

## আজকের Goal

আজকের lesson শেষে তুমি বুঝবে—

* Model কী?
* কেন Model দরকার?
* Model vs Database Table
* Model vs Object
* Model-এর life cycle
* Model নিয়ে Beginner কী ভুল করে
* Senior Developer কীভাবে চিন্তা করে

---

# ১. Model কী?

অনেক beginner ভাবে—

> Model মানে শুধু database table.

এটা **আংশিক সত্য**।

আসলে Django Model হলো **Python class যা database table-কে represent করে।**

যেমন—

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

এটা শুধু Python code।

Migration চালানোর পরে Django এটা database-এ table বানায়।

Database

```
Product Table

id
title
price
```

---

# ২. Model কেন দরকার?

ধরো Django model নেই।

তাহলে SQL লিখতে হতো।

```sql
CREATE TABLE product (
    id SERIAL,
    title VARCHAR(200),
    price DECIMAL
);
```

Insert

```sql
INSERT INTO product ...
```

Update

```sql
UPDATE ...
```

Delete

```sql
DELETE ...
```

সব SQL।

---

Model থাকলে

```python
Product.objects.create(
    title="Laptop",
    price=80000
)
```

Django SQL নিজে লিখে দেয়।

এটাকেই বলে

**ORM (Object Relational Mapping)**

---

# ৩. ORM কী?

ORM মানে

Python Object

↓

Database Row

↓

আবার Python Object

Example

Database

| id | title  | price |
| -- | ------ | ----- |
| 1  | Laptop | 80000 |

Python

```python
product = Product.objects.get(id=1)

print(product.title)
```

এখানে

```
Database Row

↓

Product Object
```

হয়ে গেছে।

---

# ৪. Model → Table

Model

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
```

Migration

↓

Database

```
category

id
name
```

---

# ৫. Object কী?

Model

```python
class Product(models.Model):
```

এটা Blueprint।

Object

```python
Product(
    title="Keyboard",
    price=1200
)
```

এটা Instance।

Real life

```
Blueprint

↓

House
```

House = Object

---

# ৬. একটা Row কী?

Database

| id | title | price |
| -- | ----- | ----- |
| 1  | Mouse | 500   |

Python

```python
product = Product.objects.first()
```

এই

```
product
```

হলো

একটা Python Object।

---

# ৭. একটা Table কী?

```
Product.objects.all()
```

ফিরিয়ে দেয়

অনেক Object।

```
<QuerySet>

↓

Product Object

Product Object

Product Object
```

---

# ৮. Model Life Cycle

এটা খুব গুরুত্বপূর্ণ।

```
Python Model লিখলে

↓

makemigrations

↓

Migration File

↓

migrate

↓

Database Table

↓

Insert Data

↓

Retrieve Data

↓

Update

↓

Delete
```

এটাই Model-এর Life Cycle।

---

# ৯. Beginner Mistake

## Mistake ১

Model = Database

❌

Model হলো Python Class।

Database Table পরে তৈরি হয়।

---

## Mistake ২

Object আর Model গুলিয়ে ফেলে।

```python
Product
```

এটা Model।

```python
Product(...)
```

এটা Object।

---

## Mistake ৩

Migration না দিয়ে Model edit করা।

```python
title = models.CharField(...)
```

লিখে ভাবে কাজ শেষ।

না।

Migration লাগবে।

---

# ১০. Senior Thinking

Senior কখনও Model লিখে শুরু করে না।

সে আগে ভাবে—

```
Business কী?

↓

Entity কী?

↓

Relationship কী?

↓

তারপর Model
```

Example

Business

```
Online Shop
```

Senior ভাবে—

```
Customer

Seller

Product

Cart

Order

Payment

Review
```

তারপর Model লিখে।

Beginner

```
Product Model বানাই।
```

Senior

```
Business বুঝি।
```

এটাই পার্থক্য।

---

# ১১. Real Project Example

ধরো তুমি একটি Hotel Booking System বানাচ্ছ।

অনেকেই শুরু করবে—

```python
class Hotel(models.Model):
    ...
```

কিন্তু আগে প্রশ্ন করবে:

* Hotel কী?
* Room আলাদা entity?
* Booking আলাদা entity?
* Guest কি User হবে?
* এক Room কি একাধিক Booking নিতে পারবে (ভিন্ন তারিখে)?
* Payment কোথায় থাকবে?

এই প্রশ্নগুলোর উত্তর থেকেই Model Design বের হবে।

---

# Lesson 1 Summary

আজ যা শিখলে:

* ✅ Model হলো Python Class।
* ✅ Migration-এর মাধ্যমে Database Table তৈরি হয়।
* ✅ ORM Python Object ↔ Database Row রূপান্তর করে।
* ✅ Model এবং Object এক জিনিস নয়।
* ✅ Model Design শুরু হয় Business Requirement বোঝা থেকে, কোড লেখা থেকে নয়।

---

## Homework (খুব গুরুত্বপূর্ণ)

Notebook-এ বা কাগজে নিচের প্রশ্নগুলোর উত্তর লেখো:

1. Model কী?
2. ORM কী?
3. Model আর Object-এর পার্থক্য কী?
4. `Product.objects.get(id=1)` কী return করে?
5. কেন migration দরকার?
6. **একটি Library Management System-এর জন্য অন্তত ৮টি Entity-এর নাম লিখো।** (কোড লিখবে না, শুধু Entity চিন্তা করবে।)

> **Lesson 2:** **Field Types Mastery** — `CharField`, `TextField`, `IntegerField`, `BooleanField`, `DecimalField`, `DateTimeField`, `JSONField`, `UUIDField` ইত্যাদি। শুধু কী করে তা নয়, **কখন কোন field ব্যবহার করতে হয় এবং beginner-রা কোথায় ভুল করে**—সব শিখব।


-----
# Django Model Design Mastery

# Lesson 2: Field Types Mastery (Senior Thinking)

আজকের lesson শেষে তুমি শিখবে—

* Field কী?
* Django-এর Common Field Types
* কখন কোন Field ব্যবহার করবে
* Beginner Mistakes
* Senior Thinking
* Real Project Examples

---

# ১. Field কী?

Model হলো Table।

Field হলো Table-এর Column।

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

Database

| id | title  | price |
| -- | ------ | ----- |
| 1  | Laptop | 80000 |

এখানে

* id → Field
* title → Field
* price → Field

---

# Senior Rule

Field choose করার আগে নিজেকে জিজ্ঞেস করো—

> **এই data-এর nature কী?**

উদাহরণ:

```
Age

Text?

Number?
```

অবশ্যই Number।

তাই

```
IntegerField
```

---

# ২. CharField

সবচেয়ে বেশি ব্যবহৃত।

```python
title = models.CharField(max_length=200)
```

Use for

* Name
* Title
* City
* Country
* Email
* Phone
* Slug

---

## কেন max_length লাগে?

Database-কে বলতে হয়

```
Maximum কত Character?
```

```python
name = models.CharField(max_length=100)
```

---

### Beginner Mistake

সব জায়গায়

```python
max_length=5000
```

দিয়ে দেয়।

এটা ভুল।

---

### Senior Thinking

বাস্তবে Name কত বড় হতে পারে?

```
50

100

150
```

যেটা যথেষ্ট সেটাই ব্যবহার করবে।

---

# ৩. TextField

বড় Text।

```python
description = models.TextField()
```

Use

* Blog Content
* Description
* Review
* Terms & Conditions

---

Difference

```
CharField

↓

Small Text
```

```
TextField

↓

Large Text
```

---

### Beginner Mistake

সবকিছু TextField করে দেয়।

ভুল।

---

# ৪. IntegerField

পূর্ণ সংখ্যা।

```python
stock = models.IntegerField()
```

Use

* Quantity
* Age
* Views
* Count

---

ভুল

```
price
```

IntegerField না।

কারণ

```
99.99
```

হতে পারে।

---

# ৫. DecimalField

Money-এর জন্য।

```python
price = models.DecimalField(
    max_digits=10,
    decimal_places=2
)
```

মানে

```
99999999.99
```

---

### কেন FloatField না?

Float

```
0.1 + 0.2

=

0.30000000000004
```

Financial calculation-এ সমস্যা।

---

Senior Rule

```
Money

=

DecimalField
```

সবসময়।

---

# ৬. FloatField

Scientific value

GPS

Measurement

Temperature

Machine Learning

---

Money না।

---

# ৭. BooleanField

```python
is_active = models.BooleanField(default=True)
```

Use

```
True

False
```

Example

```
is_verified

is_staff

is_paid

is_featured
```

---

# ৮. DateTimeField

```python
created_at = models.DateTimeField(auto_now_add=True)

updated_at = models.DateTimeField(auto_now=True)
```

Difference

auto_now_add

```
Create এর সময় একবার
```

auto_now

```
প্রতিবার Save হলে Update
```

---

### Beginner Mistake

দুইটাতেই

```
auto_now=True
```

দিয়ে দেয়।

---

# ৯. DateField

Only Date

```
Birthday

Holiday

Expiry Date
```

---

# ১০. TimeField

```
Office Start Time

Prayer Time
```

---

# ১১. EmailField

```python
email = models.EmailField(unique=True)
```

Validation built-in।

---

# ১২. URLField

```python
website = models.URLField()
```

Use

```
Website

Portfolio

Github Link
```

---

# ১৩. UUIDField

Normal id

```
1

2

3

4
```

UUID

```
0fa44f3b-9f...
```

Use

* Public API
* Security
* Hard to Guess

Example

```python
import uuid

id = models.UUIDField(
    primary_key=True,
    default=uuid.uuid4,
    editable=False
)
```

---

# ১৪. JSONField

একটা Field-এর ভিতরে JSON।

```python
metadata = models.JSONField(default=dict)
```

Example

```json
{
   "color":"red",
   "size":"XL"
}
```

---

কখন ব্যবহার করবে?

Flexible Data

যেখানে Structure বারবার পরিবর্তন হবে।

---

### Beginner Mistake

সবকিছু JSONField।

ভুল।

যদি Relation থাকে তাহলে Model বানাও।

---

Bad

```json
{
 "review1": "...",
 "review2":"..."
}
```

Good

```
Review Model
```

---

# ১৫. ImageField

```python
image = models.ImageField(upload_to="products/")
```

---

# ১৬. FileField

```python
file = models.FileField(upload_to="documents/")
```

---

# ১৭. SlugField

SEO URL

```
iphone-16-pro
```

```python
slug = models.SlugField(unique=True)
```

---

# ১৮. BinaryField

Rare।

Binary Data।

সাধারণত File Storage-এর জন্য recommend করা হয় না।

---

# Real Project Example

## Product

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField()

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.IntegerField()

    is_active = models.BooleanField(default=True)

    slug = models.SlugField(unique=True)

    created_at = models.DateTimeField(auto_now_add=True)

    updated_at = models.DateTimeField(auto_now=True)
```

---

# Beginner Version

```python
class Product(models.Model):
    title = models.TextField()

    price = models.FloatField()

    stock = models.CharField(max_length=200)

    active = models.CharField(max_length=10)
```

Problems

❌ price Float

❌ stock Text

❌ active Text

❌ title TextField

---

# Senior Version

```python
class Product(models.Model):
    title = models.CharField(max_length=200)

    description = models.TextField()

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.PositiveIntegerField()

    is_active = models.BooleanField(default=True)

    slug = models.SlugField(unique=True)

    created_at = models.DateTimeField(auto_now_add=True)

    updated_at = models.DateTimeField(auto_now=True)
```

---

# Field Selection Cheat Sheet

| Data          | Field                               |
| ------------- | ----------------------------------- |
| Name          | CharField                           |
| Description   | TextField                           |
| Price         | DecimalField                        |
| Quantity      | IntegerField / PositiveIntegerField |
| True/False    | BooleanField                        |
| Email         | EmailField                          |
| Website       | URLField                            |
| Birthday      | DateField                           |
| Created Time  | DateTimeField                       |
| Image         | ImageField                          |
| File          | FileField                           |
| SEO URL       | SlugField                           |
| Flexible JSON | JSONField                           |
| Public ID     | UUIDField                           |

---

# Senior Interview Thinking

ইন্টারভিউতে যদি জিজ্ঞেস করে:

> **Price-এর জন্য `FloatField` কেন ব্যবহার করবে না?**

উত্তর:

* `FloatField` binary floating-point ব্যবহার করে, তাই precision error হতে পারে।
* Financial data-তে 0.1 + 0.2 এর মতো মান সঠিক নাও আসতে পারে।
* `DecimalField` fixed precision দেয়, তাই টাকা বা হিসাবের জন্য এটি নিরাপদ।

---

## Homework

নিচের Model-এর জন্য কোন Field ব্যবহার করবে? শুধু Field-এর নাম লেখো, কোড নয়।

### Student

* Full Name
* Email
* Date of Birth
* Profile Photo
* CGPA
* Is Graduated
* Resume PDF
* Skills (Flexible JSON)
* Student ID (Public Unique ID)
* Bio

---

## আগামী Lesson 3

**Field Options Mastery** — `null`, `blank`, `default`, `unique`, `db_index`, `choices`, `editable`, `help_text`, `verbose_name` এবং এগুলোর সঠিক ব্যবহার। এটি এমন একটি topic যেখানে অনেক Django developer বছরের পর বছর ভুল করে।


----
# Django Model Design Mastery

# Lesson 3: Field Options Mastery (Senior Thinking)

এটি Django Model-এর সবচেয়ে বেশি ভুল হওয়া topicগুলোর একটি।

অনেক developer Field type জানে, কিন্তু `null`, `blank`, `default`, `unique`-এর পার্থক্য জানে না। এর ফলে production-এ bug, data inconsistency, এবং migration problem হয়।

---

# আজকের Goal

আজ তুমি শিখবে:

* `null`
* `blank`
* `default`
* `unique`
* `db_index`
* `choices`
* `editable`
* `help_text`
* `verbose_name`
* Senior Decision Making

---

# ১. `null`

## এটা Database-এর ব্যাপার।

```python
middle_name = models.CharField(
    max_length=100,
    null=True
)
```

এর মানে

Database-এ value হতে পারে

```
NULL
```

Database

| id | middle_name |
| -- | ----------- |
| 1  | NULL        |

---

## Beginner Mistake

সব Field-এ

```python
null=True
```

দিয়ে দেয়।

❌ এটা খুব common mistake।

---

## Senior Rule

`null=True` **শুধু তখন ব্যবহার করবে যখন Database-এ সত্যিই value না থাকাটা valid।**

Example

```
Date of Death
```

জীবিত মানুষের ক্ষেত্রে

```
NULL
```

হতে পারে।

---

# ২. `blank`

এটা Database-এর না।

এটা **Validation-এর জন্য।**

```python
bio = models.TextField(
    blank=True
)
```

মানে

Form

Serializer

Admin

এখানে Empty Accept করবে।

---

## Difference

```
null

↓

Database
```

```
blank

↓

Validation
```

---

### Interview Question

```
null=True

blank=False
```

Possible?

হ্যাঁ।

Database NULL accept করবে।

কিন্তু Form Empty accept করবে না।

---

```
blank=True

null=False
```

Possible?

হ্যাঁ।

বিশেষ করে CharField-এ খুব common।

Database-এ

```
""
```

(Empty String)

Save হবে।

---

# Senior Rule

### CharField

সাধারণত

```python
blank=True
```

ব্যবহার করো।

`null=True` ব্যবহার করো না।

কেন?

কারণ দুই ধরনের Empty হয়ে যায়।

```
NULL
```

এবং

```
""
```

এতে Query জটিল হয়।

তোমাকে দুইটাই handle করতে হবে।

```python
name__isnull=True
```

এবং

```python
name=""
```

---

# Django-এর Official Recommendation

**CharField এবং TextField-এ `null=True` সাধারণত avoid করা উচিত।**

---

# ৩. `default`

```python
is_active = models.BooleanField(
    default=True
)
```

যদি কিছু না পাঠাও

Automatically

```
True
```

হবে।

---

Example

```python
quantity = models.IntegerField(
    default=1
)
```

---

### Beginner Mistake

```python
created_at = models.DateTimeField(
    default=datetime.now()
)
```

❌

এতে Migration-এর সময় একবার execute হবে।

সব Record একই সময় পাবে।

---

Correct

```python
from django.utils import timezone

created_at = models.DateTimeField(
    default=timezone.now
)
```

**Function call (`()`) নয়, function reference ব্যবহার করবে।**

---

# ৪. `unique`

```python
email = models.EmailField(
    unique=True
)
```

Database বলবে

Duplicate Allow না।

---

Good Example

* Email
* Username
* Slug

---

Bad Example

```
First Name
```

Unique না।

---

# ৫. `db_index`

Frequently Search করলে

Index।

```python
email = models.EmailField(
    db_index=True
)
```

---

Query

```python
User.objects.filter(email=email)
```

Fast হবে।

---

### Senior Rule

Index দাও

যেখানে

```
WHERE
```

বেশি চলে।

যেমন

* slug
* email
* status
* created_at (অনেক ক্ষেত্রে)

---

### Beginner Mistake

সব Field-এ Index।

❌

Index বেশি হলে

Insert

Update

Slow হয়ে যায়।

কারণ Database-কে Index-ও Update করতে হয়।

---

# ৬. `choices`

Example

Order Status

```python
STATUS = [
    ("pending", "Pending"),
    ("paid", "Paid"),
    ("cancelled", "Cancelled"),
]
```

```python
status = models.CharField(
    max_length=20,
    choices=STATUS,
    default="pending"
)
```

---

Database-এ Save হবে

```
pending
```

Display হবে

```
Pending
```

---

## Django Best Practice

`TextChoices` ব্যবহার করো।

```python
class OrderStatus(models.TextChoices):
    PENDING = "pending", "Pending"
    PAID = "paid", "Paid"
    CANCELLED = "cancelled", "Cancelled"
```

```python
status = models.CharField(
    max_length=20,
    choices=OrderStatus.choices,
    default=OrderStatus.PENDING
)
```

এটা typo কমায় এবং maintainable।

---

# কখন `choices` ব্যবহার করবে?

যদি Value Fixed হয়।

Example

```
Gender

Status

Payment Method
```

---

কখন Model বানাবে?

যদি

Admin থেকে Change হবে।

Example

```
Category

Country

Department
```

---

# ৭. `editable`

```python
created_at = models.DateTimeField(
    auto_now_add=True,
    editable=False
)
```

Admin-এ Edit করা যাবে না।

---

# ৮. `help_text`

Admin-এ

Help দেখাবে।

```python
age = models.IntegerField(
    help_text="Age in years"
)
```

---

# ৯. `verbose_name`

Human Readable Name।

```python
phone = models.CharField(
    "Phone Number",
    max_length=20
)
```

Admin-এ

```
Phone Number
```

দেখাবে।

---

# ১০. `error_messages`

Custom Error।

```python
email = models.EmailField(
    unique=True,
    error_messages={
        "unique": "This email already exists."
    }
)
```

---

# Real Project Example

```python
class Product(models.Model):

    title = models.CharField(
        max_length=200,
        db_index=True
    )

    slug = models.SlugField(
        unique=True
    )

    description = models.TextField(
        blank=True
    )

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.PositiveIntegerField(
        default=0
    )

    is_active = models.BooleanField(
        default=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True,
        editable=False
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

---

# Beginner Version

```python
class Product(models.Model):

    title = models.TextField(
        null=True,
        blank=True
    )

    price = models.FloatField()

    stock = models.IntegerField(
        null=True
    )

    slug = models.CharField(
        max_length=500
    )
```

Problems

❌ title null=True

❌ price Float

❌ slug unique না

❌ title TextField

❌ stock null=True কেন?

---

# Senior Checklist

প্রতিটি Field লেখার সময় নিজেকে জিজ্ঞেস করো:

### ১

Business অনুযায়ী এটা Required?

```
Yes

↓

blank=False
```

---

### ২

Database-এ Value না থাকলে সমস্যা?

```
No

↓

null=True
```

(শুধু যেখানে যৌক্তিক)

---

### ৩

Default লাগবে?

```
default=
```

---

### ৪

Duplicate চলবে?

না হলে

```
unique=True
```

---

### ৫

Search বেশি হবে?

```
db_index=True
```

---

### ৬

Fixed Value?

```
choices
```

---

# Interview Questions

### Q1.

`null` আর `blank`-এর পার্থক্য?

**উত্তর:**

* `null` → Database level
* `blank` → Validation level

---

### Q2.

CharField-এ `null=True` কেন avoid করা হয়?

**উত্তর:**

কারণ Empty data দুইভাবে store হতে পারে:

* `NULL`
* `""`

এতে data inconsistency এবং query জটিল হয়।

---

### Q3.

সব Field-এ Index দিলে কী সমস্যা?

**উত্তর:**

Read কিছুটা fast হতে পারে, কিন্তু Insert, Update, Delete ধীর হয়ে যায় এবং অতিরিক্ত storage লাগে।

---

# Homework

একটি `UserProfile` model চিন্তা করো। নিচের প্রতিটি field-এর জন্য সিদ্ধান্ত নাও:

| Field         | Required? | `blank` | `null` | `default` | `unique` | Index? |
| ------------- | --------- | ------- | ------ | --------- | -------- | ------ |
| Full Name     | ?         | ?       | ?      | ?         | ?        | ?      |
| Email         | ?         | ?       | ?      | ?         | ?        | ?      |
| Bio           | ?         | ?       | ?      | ?         | ?        | ?      |
| Phone         | ?         | ?       | ?      | ?         | ?        | ?      |
| Profile Photo | ?         | ?       | ?      | ?         | ?        | ?      |

নিজে চিন্তা করে পূরণ করার চেষ্টা করো।

---

## পরের Lesson (Lesson 4)

**Relationship Mastery** — `ForeignKey`, `OneToOneField`, `ManyToManyField`, `related_name`, `on_delete`। এটি Django Model Design-এর সবচেয়ে গুরুত্বপূর্ণ অধ্যায়গুলোর একটি। এখান থেকেই তুমি বাস্তব Project Design করতে শুরু করবে।




# Django Model Design Mastery

# Lesson 4: Relationship Mastery (Most Important Lesson)

**যদি Django Model-এর একটা topic-এ mastery করতে চাও, সেটা হলো Relationship।**

বাস্তব project-এর **৮০% design** relationship-এর উপর দাঁড়িয়ে থাকে।

আজকের lesson শেষে তুমি বুঝবে—

* One-to-One
* One-to-Many
* Many-to-Many
* `related_name`
* Relationship কীভাবে চিন্তা করতে হয়
* Real Project Design
* Beginner Mistakes
* Senior Thinking

---

# Relationship Design করার আগে

**কখনও `ForeignKey` লিখে শুরু করবে না।**

Senior developer প্রথমে এই ৩টা প্রশ্ন করে।

```
Entity 1 কে?

Entity 2 কে?

তাদের relationship কী?
```

উদাহরণ

```
User

Product
```

প্রশ্ন

একজন User কতগুলো Product রাখতে পারে?

```
One User

↓

Many Products
```

তাহলে

```
One-To-Many
```

---

# Rule 1

**প্রথমে English-এ sentence লেখো।**

Example

```
One Seller has many Products.
```

এখন relationship বের করো।

---

# Relationship Type 1

# One-to-One

Example

```
User

↓

Profile
```

একজন User-এর

একটাই Profile।

একটা Profile

একজন User-এর।

```
1 ---------- 1
```

Django

```python
class Profile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE
    )
```

---

## Real Examples

```
User

↓

Profile
```

```
User

↓

Wallet
```

```
Car

↓

Engine
```

```
Student

↓

StudentIDCard
```

---

## Beginner Mistake

অনেকে লেখে

```python
user = models.ForeignKey(User)
```

এতে কী হবে?

এক User-এর

অনেক Profile হতে পারবে।

ভুল।

---

# Relationship Type 2

# One-To-Many

সবচেয়ে বেশি ব্যবহৃত।

Example

```
Category

↓

Product

↓

Product

↓

Product
```

একটা Category

অনেক Product।

কিন্তু

একটা Product

একটাই Category।

---

Django

```python
class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

---

আরও Example

```
User

↓

Order
```

এক User

অনেক Order।

---

```
Post

↓

Comment
```

---

```
Department

↓

Employee
```

---

# ForeignKey কোথায় থাকবে?

এটা সবচেয়ে Important।

Senior Rule

> **ForeignKey সবসময় "Many" side-এ থাকবে।**

Example

```
One Category

↓

Many Products
```

ForeignKey যাবে

```
Product
```

Model-এ।

```python
class Product(models.Model):
    category = models.ForeignKey(Category)
```

---

আরেকটা

```
One User

↓

Many Orders
```

FK যাবে

```
Order
```

Model-এ।

---

# Interview Question

কেন ForeignKey Product-এ?

কেন Category-তে না?

উত্তর

কারণ

Product হচ্ছে

Many side।

---

# Relationship Type 3

# Many-To-Many

Example

```
Post

Python

AI

Django
```

একটা Post

অনেক Tag।

---

একটা Tag

অনেক Post।

```
Many ←→ Many
```

---

Django

```python
class Post(models.Model):
    tags = models.ManyToManyField(Tag)
```

---

আরও Example

```
Student

↓

Course
```

এক Student

অনেক Course।

এক Course

অনেক Student।

---

```
Movie

↓

Actor
```

---

```
Product

↓

Category
```

(যদি Business Allow করে)

---

# Django ভিতরে কী করে?

অনেকে ভাবে

ManyToMany

Magic।

আসলে না।

Django Automatically

একটা Junction Table বানায়।

```
Post

id
```

```
Tag

id
```

Automatically

```
post_tags

post_id

tag_id
```

---

# Senior Thinking

নিজেকে প্রশ্ন করো।

```
Extra Information লাগবে?
```

Example

Student

Course

কিন্তু

Enrollment Date

Grade

Certificate

এগুলো কোথায় রাখবে?

Simple ManyToMany পারবে?

না।

---

তখন

Through Model।

```python
class Enrollment(models.Model):

    student = models.ForeignKey(Student)

    course = models.ForeignKey(Course)

    enrolled_at = models.DateField()

    grade = models.CharField(...)
```

এখন

```python
courses = models.ManyToManyField(
    Course,
    through="Enrollment"
)
```

---

# related_name

ধরো

```python
class Product(models.Model):
    seller = models.ForeignKey(User)
```

এখন

Product থেকে

```python
product.seller
```

পাওয়া যাবে।

কিন্তু

User থেকে?

Default

```python
user.product_set.all()
```

এটা সুন্দর না।

---

Better

```python
seller = models.ForeignKey(

    User,

    related_name="products",

    on_delete=models.CASCADE
)
```

এখন

```python
user.products.all()
```

---

Senior Rule

**সব ForeignKey-এ `related_name` দাও।**

কারণ code readable হয়।

---

# Real Project Example

## Blog

```
User

↓

Post

↓

Comment
```

Models

```python
class Post(models.Model):

    author = models.ForeignKey(
        User,
        related_name="posts",
        on_delete=models.CASCADE
    )
```

Comment

```python
class Comment(models.Model):

    post = models.ForeignKey(
        Post,
        related_name="comments",
        on_delete=models.CASCADE
    )
```

Query

```python
user.posts.all()
```

```python
post.comments.all()
```

কত সুন্দর।

---

# E-commerce Example

```
Seller

↓

Product

↓

Review
```

Product

↓

Images

↓

Variants

↓

Inventory

↓

OrderItems

সব One-To-Many।

---

# Beginner Mistakes

## Mistake 1

সব জায়গায় ForeignKey।

ভুল।

---

## Mistake 2

OneToOne লাগবে

ForeignKey ব্যবহার করে।

---

## Mistake 3

ManyToMany লাগবে

ForeignKey ব্যবহার করে।

---

## Mistake 4

related_name দেয় না।

তারপর

```
_set
```

use করে।

---

## Mistake 5

Business না বুঝে Relation।

---

# Senior Thinking Process

যখন নতুন Project পাবে।

প্রথমে

```
Entity লিখো।
```

Example

Library

```
Book

Author

Category

Publisher

Student

Borrow
```

এখন Relation।

```
Book

↓

Publisher

One
```

```
Book

↓

Category

Many?
```

```
Book

↓

Author

Many?
```

একটা বই

একাধিক Author?

হতে পারে।

তাহলে

ManyToMany।

---

Borrow

```
Student

↓

Borrow

↓

Book
```

Borrow হচ্ছে Transaction।

এটা ManyToMany না।

কারণ

Borrow Date

Return Date

Fine

Extra Data আছে।

তাই

Borrow Model।

---

# Senior Golden Rules

### Rule 1

Sentence লেখো।

```
One Seller has many Products.
```

---

### Rule 2

ForeignKey যাবে

Many Side-এ।

---

### Rule 3

Extra Information থাকলে

Through Model অথবা আলাদা Transaction Model।

---

### Rule 4

সব FK-এ

```
related_name
```

দাও।

---

### Rule 5

Database Relation

Business Rule থেকে আসে।

Code থেকে না।

---

# Interview Questions

### Q1.

ForeignKey কোথায় থাকবে?

**উত্তর:**

সবসময় **Many side**-এ।

---

### Q2.

ManyToMany-এর ভিতরে Django কী বানায়?

**উত্তর:**

একটি **Intermediate (Junction) Table**।

---

### Q3.

কখন Through Model ব্যবহার করবে?

**উত্তর:**

যখন দুই Model-এর relationship-এর সাথে অতিরিক্ত তথ্য (যেমন enrollment date, quantity, grade, role) সংরক্ষণ করতে হবে।

---

### Q4.

`related_name` কেন ব্যবহার করো?

**উত্তর:**

Reverse relationship-কে meaningful এবং readable করার জন্য। `user.products.all()` `user.product_set.all()`-এর চেয়ে অনেক পরিষ্কার।

---

# Homework (Design Thinking)

নিচের Business Requirement পড়ে শুধু Relationship বের করো (কোড লিখবে না)।

## Hospital Management System

Entities:

* Doctor
* Patient
* Appointment
* Prescription
* Medicine
* Department

প্রশ্ন:

1. Doctor ↔ Department
2. Patient ↔ Appointment
3. Appointment ↔ Prescription
4. Prescription ↔ Medicine
5. Doctor ↔ Appointment

প্রতিটির জন্য লিখো:

* One-to-One?
* One-to-Many?
* Many-to-Many?
* যদি Many-to-Many হয়, তাহলে কি Through Model দরকার?

---

## Lesson 5 Preview (সবচেয়ে Critical)

পরের Lesson হবে **`on_delete` Mastery**।

এটি এমন একটি topic যেখানে শুধু `CASCADE`, `PROTECT`, `SET_NULL` মুখস্থ করলেই হবে না। আমরা শিখব **Business Rule অনুযায়ী `on_delete` কীভাবে নির্বাচন করতে হয়**, কারণ ভুল `on_delete` production database-এর মূল্যবান data মুছে ফেলতে পারে।



# Django Model Design Mastery

# Lesson 5: `on_delete` Mastery (Business Thinking)

এটি এমন একটি topic যেখানে **অনেক Intermediate Django Developer-ও ভুল করে।**

অনেকে শুধু মুখস্থ করে:

* CASCADE
* PROTECT
* SET_NULL

কিন্তু **Senior Developer কখনো `on_delete` মুখস্থ করে না।**

সে আগে একটা প্রশ্ন করে:

> **"Parent object delete হলে Business কী চায়?"**

এই একটা প্রশ্নের উত্তরই সঠিক `on_delete` নির্ধারণ করে।

---

# আজকের Goal

আজ তুমি শিখবে:

* `on_delete` কেন লাগে?
* সব ধরনের `on_delete`
* Business Thinking
* Real Project Examples
* Common Mistakes
* Senior Decision Framework

---

# Step 1: `on_delete` কী?

ধরো,

```python
class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=?
    )
```

এখন যদি

```text
Category Delete
```

করা হয়,

তাহলে Product-এর কী হবে?

Database নিজেই প্রশ্ন করে।

কারণ Product-এর ভিতরে Category-এর ID আছে।

```
Product

id

title

category_id
```

যদি Category delete হয়ে যায়,

```
category_id = 5
```

কিন্তু

Category 5 আর নেই।

এখন Product broken হয়ে যাবে।

এই সমস্যা সমাধানের জন্যই `on_delete`।

---

# Business Thinking

কখনো কোড দিয়ে শুরু করবে না।

প্রথমে জিজ্ঞেস করো:

```
Parent Delete

↓

Child-এর কী হবে?
```

---

# ১. CASCADE

সবচেয়ে পরিচিত।

```python
category = models.ForeignKey(
    Category,
    on_delete=models.CASCADE
)
```

মানে

```
Category Delete

↓

সব Product Delete
```

---

Example

```
Post

↓

Comment
```

Post delete

↓

Comments delete

এটা perfectly logical।

---

আরেকটা

```
Playlist

↓

PlaylistSong
```

Playlist delete

↓

PlaylistSong delete

---

## কখন ব্যবহার করবে?

যখন Child-এর Parent ছাড়া কোনো অর্থ নেই।

Example

```
Blog Post

↓

Comment
```

Comment Post ছাড়া থাকবে না।

---

# ২. PROTECT

```python
user = models.ForeignKey(
    User,
    on_delete=models.PROTECT
)
```

মানে

```
Delete করতে চাই

↓

Error দিবে
```

যদি Child থাকে।

---

Example

```
Customer

↓

Order
```

Customer delete?

না।

কারণ Order History নষ্ট হবে।

---

আরেকটা

```
Country

↓

City
```

Country delete করা উচিত?

না।

---

Senior Rule

Historical Data থাকলে

অনেক সময় PROTECT।

---

# ৩. SET_NULL

```python
seller = models.ForeignKey(
    Seller,
    on_delete=models.SET_NULL,
    null=True
)
```

Seller delete

↓

Product থাকবে

↓

Seller হবে NULL

---

Database

Before

| Product | seller |
| ------- | ------ |
| Laptop  | 5      |

After

| Product | seller |
| ------- | ------ |
| Laptop  | NULL   |

---

কখন ব্যবহার করবে?

যখন Relationship Optional।

Example

```
Article

↓

Reviewed By Admin
```

Admin delete হলে

Article থাকবে।

Reviewer NULL হবে।

---

⚠️ মনে রাখবে

`SET_NULL` ব্যবহার করলে অবশ্যই

```python
null=True
```

দিতে হবে।

---

# ৪. SET_DEFAULT

```python
category = models.ForeignKey(
    Category,
    default=1,
    on_delete=models.SET_DEFAULT
)
```

Category delete

↓

Default Category হবে।

---

Example

```
Category

↓

General
```

Deleted category-এর সব Product

↓

General Category-তে চলে যাবে।

---

# ৫. SET()

Custom Function।

```python
def get_default_user():
    return User.objects.get(pk=1)

owner = models.ForeignKey(
    User,
    on_delete=models.SET(get_default_user)
)
```

Delete হলে

Function execute হবে।

---

কখন ব্যবহার করবে?

Advanced Case।

---

# ৬. DO_NOTHING

```python
on_delete=models.DO_NOTHING
```

মানে

Django কিছুই করবে না।

Database যদি Error দেয়

দেবে।

---

Senior Rule

Production-এ খুব কম ব্যবহার হয়।

---

# RESTRICT (Django 3.1+)

অনেকেই এটা জানে না।

```python
on_delete=models.RESTRICT
```

এটাও delete আটকায়।

কিন্তু

`PROTECT` থেকে একটু ভিন্ন behavior।

---

সহজ ভাষায়

```
PROTECT

↓

Always block
```

```
RESTRICT

↓

Database relation consider করে block
```

**৯০% project-এ `PROTECT` যথেষ্ট।**

---

# Real Project Examples

## Example 1

Blog

```
Post

↓

Comment
```

Post delete

↓

Comment?

Business

Comment useless।

Answer

```
CASCADE
```

---

## Example 2

E-commerce

```
Customer

↓

Order
```

Customer delete?

না।

কারণ

Invoice

Payment

History

সব নষ্ট হবে।

```
PROTECT
```

---

## Example 3

Product

↓

Category

Business বলে

Category delete হলে

Product থাকবে।

General Category-তে যাবে।

```
SET_DEFAULT
```

---

## Example 4

Article

↓

Reviewer

Reviewer delete

Article থাকবে।

```
SET_NULL
```

---

# Beginner Mistakes

## Mistake 1

সব জায়গায়

```python
CASCADE
```

❌

এটা সবচেয়ে Common ভুল।

---

## Mistake 2

Business না বুঝে

PROTECT।

---

## Mistake 3

SET_NULL

কিন্তু

```python
null=False
```

❌

Migration Error।

---

## Mistake 4

History Model-এ

CASCADE।

---

Example

```
Invoice

↓

Customer
```

Customer delete

↓

Invoice delete

Business শেষ।

---

# Senior Thinking

Senior কখনও জিজ্ঞেস করে না

```
CASCADE দিবো?
```

সে জিজ্ঞেস করে

```
Customer Delete

↓

Business কী চায়?
```

তারপর

Decision।

---

# Decision Tree

## Question 1

Child Parent ছাড়া বাঁচতে পারে?

Yes

↓

```
SET_NULL
```

অথবা

```
SET_DEFAULT
```

---

No

↓

Question 2

Delete করা উচিত?

Yes

↓

```
CASCADE
```

---

No

↓

```
PROTECT
```

---

# Real E-commerce Design

```
Seller

↓

Product
```

Business

Seller Account deactivate হতে পারে।

Product delete না।

তাই

```
SET_NULL
```

বা

Soft Delete।

---

```
Customer

↓

Order
```

```
PROTECT
```

---

```
Order

↓

OrderItem
```

```
CASCADE
```

কারণ OrderItem

Order ছাড়া meaningless।

---

```
Product

↓

Review
```

Business-এর উপর নির্ভর করে।

Option 1

Product delete

↓

Review delete

```
CASCADE
```

Option 2

Review historical data হিসেবে রাখতে চাই

↓

Soft Delete Product

---

# Soft Delete vs Hard Delete

Senior Project-এ অনেক সময় Parent delete-ই করা হয় না।

Instead

```python
is_active = False
```

অথবা

```python
deleted_at = models.DateTimeField(null=True, blank=True)
```

এটাকে বলে **Soft Delete**।

তখন `on_delete`-এর অনেক সমস্যা এড়ানো যায়।

---

# Interview Questions

### Q1. `CASCADE` কী?

**উত্তর:**

Parent delete হলে তার সাথে সম্পর্কিত Child row-গুলোও delete হয়ে যায়।

---

### Q2. `PROTECT` কখন ব্যবহার করবে?

**উত্তর:**

যখন Child data গুরুত্বপূর্ণ এবং Parent delete করলে history বা business data নষ্ট হবে।

---

### Q3. `SET_NULL` ব্যবহার করতে কী শর্ত?

**উত্তর:**

ForeignKey field-এ `null=True` থাকতে হবে।

---

### Q4. কেন সব জায়গায় `CASCADE` ব্যবহার করা উচিত নয়?

**উত্তর:**

কারণ Parent delete করলে অপ্রয়োজনীয়ভাবে গুরুত্বপূর্ণ Child data-ও delete হয়ে যেতে পারে, যেমন Order, Invoice, Payment History।

---

# Senior Checklist

প্রতিটি ForeignKey লেখার আগে নিজেকে জিজ্ঞেস করো:

* Parent delete হলে Child-এর কী হবে?
* Child কি Parent ছাড়া meaningful?
* Business কি history রাখতে চায়?
* Soft delete কি ভালো সমাধান?
* `SET_NULL` হলে `null=True` আছে তো?

---

# Homework (Design Challenge)

নিচের প্রতিটি Relationship-এর জন্য `on_delete` নির্বাচন করো এবং **কেন** সেটা লিখো।

| Parent   | Child           | `on_delete` কী হবে?                              |
| -------- | --------------- | ------------------------------------------------ |
| Post     | Comment         | ?                                                |
| Customer | Order           | ?                                                |
| Order    | OrderItem       | ?                                                |
| Teacher  | Course          | ?                                                |
| User     | Profile         | ?                                                |
| Category | Product         | ? (Business: Category delete হলেও Product থাকবে) |
| Admin    | ApprovedArticle | ?                                                |

**শুধু উত্তর নয়, Business Reason-ও লিখবে।**

---

# পরের Lesson (Lesson 6)

**Model Meta Mastery** — `ordering`, `db_table`, `verbose_name`, `indexes`, `constraints`, `UniqueConstraint`, `CheckConstraint`।

এই lesson-এর পর তুমি Django Model-কে শুধু "চলবে" এমনভাবে নয়, **production-ready**ভাবে design করতে শিখবে।









# Django Model Design Mastery

# Lesson 6: Meta Class Mastery (Senior Thinking)

আজকের lesson খুবই গুরুত্বপূর্ণ। কারণ `Meta` class-এর মাধ্যমে তুমি **database-এর behavior control** করতে পারো।

অনেক beginner শুধু Model লিখে শেষ করে। কিন্তু senior developer `Meta` ব্যবহার করে model-কে production-ready করে।

---

# আজকের Goal

আজ তুমি শিখবে:

* `Meta` কী?
* `ordering`
* `db_table`
* `verbose_name`
* `verbose_name_plural`
* `indexes`
* `constraints`
* `UniqueConstraint`
* `CheckConstraint`
* Senior Thinking

---

# ১. Meta কী?

প্রতিটি Model-এর জন্য Django কিছু extra configuration রাখার জায়গা দেয়।

```python
class Product(models.Model):
    title = models.CharField(max_length=200)

    class Meta:
        ...
```

এখানে

```python
class Meta:
```

Database-এর behavior configure করে।

---

# Beginner Thinking

```python
class Meta:
    pass
```

---

# Senior Thinking

প্রতিটি Model-এ ভাববে

* Table-এর নাম কী হবে?
* Default ordering কী হবে?
* কোন field index হবে?
* Duplicate কীভাবে আটকাবে?
* Invalid data কীভাবে আটকাবে?

---

# ২. ordering

ধরো

Database

| id | title    | created_at |
| -- | -------- | ---------- |
| 1  | Laptop   | 2025       |
| 2  | Mouse    | 2024       |
| 3  | Keyboard | 2026       |

তুমি লিখলে

```python
Product.objects.all()
```

Default কোন order-এ আসবে?

এটা Meta দিয়ে ঠিক করা যায়।

---

Example

```python
class Meta:
    ordering = ["title"]
```

Result

```text
Keyboard
Laptop
Mouse
```

Alphabetically।

---

Newest First

```python
class Meta:
    ordering = ["-created_at"]
```

Minus (`-`) মানে Descending।

Result

```text
2026

2025

2024
```

---

Multiple Ordering

```python
class Meta:
    ordering = [
        "-created_at",
        "title"
    ]
```

মানে

প্রথমে created_at

তারপর title

---

### Senior Rule

যে query সবচেয়ে বেশি হবে,

সেটাকে Default Ordering বানাও।

Example

Blog

```python
ordering = ["-published_at"]
```

News

```python
ordering = ["-created_at"]
```

Product

Business-এর উপর নির্ভর করবে।

---

# ৩. db_table

Normally

```python
class Product(models.Model):
```

Table হবে

```text
appname_product
```

Example

```text
shop_product
```

---

Change করতে চাইলে

```python
class Meta:
    db_table = "products"
```

Database

```text
products
```

---

### কখন ব্যবহার করবে?

* Legacy Database
* Existing Table
* Company Naming Standard

---

### Beginner Mistake

প্রতিটি Model-এ

```python
db_table
```

দিয়ে দেয়।

প্রয়োজন না থাকলে দরকার নেই।

---

# ৪. verbose_name

Admin-এ Human Friendly Name।

```python
class Meta:
    verbose_name = "Product"
```

---

Plural

```python
class Meta:
    verbose_name_plural = "Products"
```

Admin

```
Products
```

দেখাবে।

---

# ৫. indexes

এটা খুব গুরুত্বপূর্ণ।

ধরো

```python
Product.objects.filter(slug=slug)
```

প্রতিদিন হাজারবার হচ্ছে।

তাহলে?

Index।

---

Example

```python
class Meta:

    indexes = [
        models.Index(fields=["slug"]),
    ]
```

---

Multiple Index

```python
class Meta:

    indexes = [
        models.Index(fields=["status"]),
        models.Index(fields=["created_at"]),
    ]
```

---

Compound Index

```python
class Meta:

    indexes = [
        models.Index(
            fields=["status", "-created_at"]
        ),
    ]
```

এটা useful যখন query হয়

```python
Product.objects.filter(
    status="active"
).order_by("-created_at")
```

---

### Senior Rule

Index দাও

যেখানে

* filter()
* exclude()
* order_by()
* join()

বেশি হবে।

---

### Beginner Mistake

সব Field-এ Index।

❌

কারণ

Insert

Update

Slow হয়ে যায়।

---

# ৬. constraints

Constraint মানে

Database Rule।

Database নিজেই Data Protect করবে।

---

Example

Price

```text
-500
```

Allow করা উচিত?

না।

Constraint।

---

# ৭. UniqueConstraint

ধরো

Student

একই Email দুইবার না।

তাহলে

```python
email = models.EmailField(unique=True)
```

ঠিক আছে।

---

কিন্তু

একটা Seller

একই Product Name

দুইবার রাখতে পারবে?

না।

অন্য Seller?

পারবে।

তাহলে?

Composite Unique।

```python
class Meta:

    constraints = [

        models.UniqueConstraint(
            fields=["seller", "title"],
            name="unique_product_per_seller"
        )
    ]
```

---

Database বলবে

এক Seller

একই Title

দুইবার না।

---

### Real Example

Room Booking

```text
Room

Date
```

একই Room

একই Date

দুইবার Booking?

না।

Constraint।

---

# ৮. CheckConstraint

ধরো

Price

```text
-500
```

Save হওয়া উচিত?

না।

---

```python
from django.db.models import Q

class Meta:

    constraints = [

        models.CheckConstraint(
            condition=Q(price__gte=0),
            name="price_positive"
        )
    ]
```

---

আরও Example

Age

```python
models.CheckConstraint(
    condition=Q(age__gte=18),
    name="adult_only"
)
```

---

Stock

```python
condition=Q(stock__gte=0)
```

---

Rating

```python
condition=Q(rating__gte=1) &
          Q(rating__lte=5)
```

---

### Senior Rule

Business Rule

Database-এই Protect করো।

শুধু Serializer Validation-এর উপর নির্ভর করো না।

---

# Real Project Example

```python
from django.db import models
from django.db.models import Q


class Product(models.Model):

    seller = models.ForeignKey(
        "Seller",
        on_delete=models.CASCADE
    )

    title = models.CharField(
        max_length=200
    )

    slug = models.SlugField()

    price = models.DecimalField(
        max_digits=10,
        decimal_places=2
    )

    stock = models.PositiveIntegerField()

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    class Meta:

        ordering = ["-created_at"]

        indexes = [
            models.Index(fields=["slug"]),
            models.Index(fields=["seller"]),
        ]

        constraints = [

            models.UniqueConstraint(
                fields=["seller", "title"],
                name="unique_product_per_seller"
            ),

            models.CheckConstraint(
                condition=Q(price__gte=0),
                name="price_positive"
            )
        ]
```

---

# Beginner Version

```python
class Product(models.Model):

    title = models.CharField(max_length=200)

    price = models.DecimalField(...)
```

Problems

❌ No ordering

❌ No indexes

❌ No constraints

❌ Duplicate data possible

❌ Invalid data possible

---

# Senior Checklist

প্রতিটি Model-এর জন্য নিজেকে জিজ্ঞেস করো:

### ১

Default Order কী?

```python
ordering
```

---

### ২

Search বেশি কোথায়?

```python
indexes
```

---

### ৩

Duplicate আটকাতে হবে?

```python
UniqueConstraint
```

---

### ৪

Invalid Data আটকাতে হবে?

```python
CheckConstraint
```

---

### ৫

Table Name Change দরকার?

```python
db_table
```

---

# Interview Questions

### Q1.

`unique=True` আর `UniqueConstraint`-এর পার্থক্য?

**উত্তর:**

* `unique=True` একটি field-এর জন্য।
* `UniqueConstraint` একাধিক field মিলিয়ে uniqueness enforce করতে পারে।

উদাহরণ:

```python
UniqueConstraint(
    fields=["seller", "title"]
)
```

---

### Q2.

`ordering` কোথায় কাজ করে?

**উত্তর:**

Model-এর default queryset-এ। `Product.objects.all()` করলে এই ordering apply হবে, যদি আলাদা করে `order_by()` না দেওয়া হয়।

---

### Q3.

`CheckConstraint` কেন দরকার?

**উত্তর:**

Database level-এ invalid data (যেমন negative price, invalid rating) ঢোকা আটকাতে।

---

### Q4.

Index সব field-এ দিলে কী সমস্যা?

**উত্তর:**

Read query কিছুটা দ্রুত হতে পারে, কিন্তু Insert, Update, Delete ধীর হয় এবং অতিরিক্ত storage লাগে।

---

# Homework (Production Thinking)

একটি `Coupon` model design করো। Meta class নিয়ে চিন্তা করো।

Fields:

* code
* discount_percent
* start_date
* end_date
* is_active

ভাবো:

* Default ordering কী হবে?
* `code` কি unique হবে?
* `discount_percent`-এর জন্য কী constraint লাগবে? (Hint: 0–100)
* কোন field-এ index দরকার?

---

# 📌 এখান পর্যন্ত তুমি যা শিখেছ

* ✅ Lesson 1 — Model Fundamentals
* ✅ Lesson 2 — Field Types
* ✅ Lesson 3 — Field Options
* ✅ Lesson 4 — Relationships
* ✅ Lesson 5 — `on_delete`
* ✅ Lesson 6 — `Meta` Class

এগুলো Django Model Design-এর **foundation**।

---

## Lesson 7 (খুব গুরুত্বপূর্ণ)

**Model Inheritance Mastery**

আমরা শিখব:

* Abstract Base Model
* Multi-table Inheritance
* Proxy Model
* কোনটা কখন ব্যবহার করতে হয়
* কেন অনেক developer inheritance ভুলভাবে ব্যবহার করে
* Production-level patterns (`BaseModel`, `TimeStampedModel`, `SoftDeleteModel`)




# Django Model Design Mastery

# Lesson 7: Model Inheritance Mastery (Senior Thinking)

আজকের lesson Django-এর এমন একটি feature নিয়ে, যেটা অনেক developer জানে, কিন্তু **সঠিকভাবে ব্যবহার করতে পারে না**।

**Senior developer-এর প্রথম প্রশ্ন:**

> **"আমি কি code reuse করতে চাই, নাকি data reuse করতে চাই?"**

এই প্রশ্নের উত্তরই বলে দেবে কোন inheritance ব্যবহার করবে।

---

# আজকের Goal

আজ তুমি শিখবে:

* Model Inheritance কী?
* Abstract Base Model
* Multi-table Inheritance
* Proxy Model
* কখন কোনটা ব্যবহার করবে?
* Beginner Mistakes
* Senior Thinking

---

# Model Inheritance কী?

Python-এর মতো Django Model-ও inheritance support করে।

```python
class A:
    pass

class B(A):
    pass
```

Django-তেও একই concept।

---

# Django-তে Inheritance-এর ৩ ধরন

```
1. Abstract Base Model ⭐⭐⭐⭐⭐ (সবচেয়ে বেশি ব্যবহৃত)

2. Multi-table Inheritance ⭐⭐ (খুব কম ব্যবহৃত)

3. Proxy Model ⭐⭐⭐ (বিশেষ ক্ষেত্রে)
```

---

# ১. Abstract Base Model ⭐⭐⭐⭐⭐

এটাই সবচেয়ে গুরুত্বপূর্ণ।

ধরো,

তোমার ১০টা Model আছে।

```text
Product

Category

Order

Review

Cart

Invoice

Payment

Seller
```

সব Model-এ

```python
created_at

updated_at
```

আছে।

---

## Beginner Version

```python
class Product(models.Model):

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

```python
class Category(models.Model):

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

```python
class Order(models.Model):

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

একই code বারবার।

❌ DRY (Don't Repeat Yourself) ভেঙে যাচ্ছে।

---

## Senior Version

```python
class BaseModel(models.Model):

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        abstract = True
```

এখন

```python
class Product(BaseModel):

    title = models.CharField(max_length=200)
```

```python
class Category(BaseModel):

    name = models.CharField(max_length=100)
```

Database

```
Product Table

id
title
created_at
updated_at
```

Category

```
id
name
created_at
updated_at
```

---

## গুরুত্বপূর্ণ

**`BaseModel`-এর নিজের কোনো table তৈরি হবে না।**

কারণ

```python
abstract = True
```

---

# Database Visualization

```
BaseModel

↓

Product
```

Database

```
Product Table
```

BaseModel Table?

```
না
```

---

# Real Project Example

Production-এ প্রায়ই দেখা যায়:

```python
class TimeStampedModel(models.Model):

    created_at

    updated_at

    class Meta:
        abstract = True
```

---

তারপর

```python
Product(TimeStampedModel)

Order(TimeStampedModel)

Category(TimeStampedModel)

Review(TimeStampedModel)
```

---

# আরেকটা Example

Soft Delete

```python
class SoftDeleteModel(models.Model):

    is_deleted = models.BooleanField(
        default=False
    )

    deleted_at = models.DateTimeField(
        null=True,
        blank=True
    )

    class Meta:
        abstract = True
```

সব Model-এ reuse।

---

# কখন Abstract Model ব্যবহার করবে?

যখন

```
Code Share করতে হবে।
```

---

# Beginner Mistake

অনেকে

```python
abstract = True
```

দিতে ভুলে যায়।

তখন Django BaseModel-এরও table বানিয়ে ফেলে।

---

# ২. Multi-table Inheritance ⭐⭐

এটা খুব কম ব্যবহার হয়।

Example

```python
class Person(models.Model):

    name = models.CharField(max_length=100)
```

```python
class Employee(Person):

    salary = models.DecimalField(...)
```

Database

Person Table

```
id

name
```

Employee Table

```
person_ptr

salary
```

---

Employee Query

```
JOIN
```

করে।

---

Database

```
Person

↓

Employee
```

---

## কবে ব্যবহার করবে?

যখন

বাস্তবেই

```
Employee IS A Person
```

Relationship।

---

## কিন্তু...

Production-এ খুব কম।

কারণ

JOIN লাগে।

Performance কম।

---

# Senior Rule

৯৫% সময়

Abstract Model

ব্যবহার করো।

---

# Beginner Mistake

Multi-table দিয়ে Code Reuse করতে যায়।

❌

এটা Code Reuse-এর জন্য না।

---

# ৩. Proxy Model ⭐⭐⭐

এটা Table বানায় না।

Data Copy করে না।

শুধু Behavior Change করে।

Example

```python
class Product(models.Model):

    title = models.CharField(max_length=200)
```

Proxy

```python
class FeaturedProduct(Product):

    class Meta:
        proxy = True
```

Table

```
Product
```

একটাই।

---

এখন

Custom Manager

Different Ordering

Different Admin

ব্যবহার করতে পারবে।

---

Example

```python
class ActiveProduct(Product):

    objects = ActiveManager()

    class Meta:
        proxy = True
```

---

# কখন ব্যবহার করবে?

ধরো

একই Product Table।

কিন্তু

Admin-এ

Featured Product

আলাদা দেখতে চাই।

---

অথবা

Different Default Manager।

---

# Beginner Mistake

Proxy দিয়ে নতুন Field Add করতে চায়।

❌

পারবে না।

---

# Comparison

| Feature         | Abstract | Multi-table | Proxy |
| --------------- | -------- | ----------- | ----- |
| New Table       | ❌        | ✅           | ❌     |
| Reuse Fields    | ✅        | ✅           | ❌     |
| Add New Fields  | Child-এ  | Child-এ     | ❌     |
| Change Behavior | ❌        | ❌           | ✅     |
| Most Used       | ⭐⭐⭐⭐⭐    | ⭐           | ⭐⭐    |

---

# Senior Thinking

## Question 1

আমি কি শুধু Code Reuse চাই?

↓

```
Abstract
```

---

## Question 2

আমি কি সত্যিই Parent-Child Database Structure চাই?

↓

```
Multi-table
```

---

## Question 3

আমি কি শুধু Behavior Change চাই?

↓

```
Proxy
```

---

# Real E-commerce Example

```
BaseModel

↓

Product

Category

Order

Review
```

---

BaseModel

```python
created_at

updated_at
```

---

SoftDeleteModel

```python
is_deleted

deleted_at
```

---

AuditModel

```python
created_by

updated_by
```

---

তারপর

```python
class Product(

    TimeStampedModel,

    SoftDeleteModel
):
    ...
```

**Multiple inheritance**-ও Django support করে, যদি design পরিষ্কার থাকে।

---

# Production Pattern

অনেক বড় Project-এ

```python
TimeStampedModel
```

*

```python
UUIDModel
```

*

```python
SoftDeleteModel
```

একসাথে ব্যবহার হয়।

---

# Beginner Mistakes

## Mistake 1

সব Model Copy-Paste।

---

## Mistake 2

Abstract দিতে ভুলে যায়।

---

## Mistake 3

Proxy-তে Field Add করতে চায়।

---

## Mistake 4

Multi-table দিয়ে DRY করতে চায়।

---

# Interview Questions

### Q1.

Abstract Model-এর Table হয়?

উত্তর

```
না।
```

---

### Q2.

Proxy Model কি নতুন Table বানায়?

উত্তর

```
না।
```

---

### Q3.

Multi-table কেন Slow?

উত্তর

কারণ Parent এবং Child table-এর মধ্যে JOIN করতে হয়।

---

### Q4.

সবচেয়ে বেশি কোন Inheritance ব্যবহার হয়?

উত্তর

```
Abstract Base Model
```

---

# Senior Checklist

Model বানানোর আগে নিজেকে জিজ্ঞেস করো:

* একই field কি ৫–১০টি Model-এ আছে?
* শুধু code reuse দরকার, নাকি database relation-ও দরকার?
* নতুন table লাগবে?
* শুধু behavior change করতে চাই?
* এই inheritance query performance-এ কী প্রভাব ফেলবে?

---

# Homework

Design করো একটি production-ready inheritance structure।

Models:

* Product
* Category
* Order
* UserProfile

সব Model-এ দরকার:

* `created_at`
* `updated_at`
* `is_deleted`
* `deleted_at`

প্রশ্ন:

1. কয়টি Abstract Base Model বানাবে?
2. `BaseModel` আর `SoftDeleteModel` আলাদা রাখবে নাকি একসাথে? কেন?
3. কোন Model-গুলোর inheritance diagram কেমন হবে?

---

# 🎯 এখান পর্যন্ত যা শিখেছ

* ✅ Lesson 1 — Model Fundamentals
* ✅ Lesson 2 — Field Types
* ✅ Lesson 3 — Field Options
* ✅ Lesson 4 — Relationships
* ✅ Lesson 5 — `on_delete`
* ✅ Lesson 6 — Meta Class
* ✅ Lesson 7 — Model Inheritance

এখন তোমার Model Design-এর foundation বেশ শক্ত।

---

# Lesson 8 (Most Practical)

পরের lesson হবে **Custom Managers & QuerySets Mastery**।

এখানে আমরা শিখব:

* `objects = models.Manager()` আসলে কী?
* Custom Manager কেন দরকার?
* Custom `QuerySet` কী?
* Soft Delete-এর জন্য Manager কীভাবে বানানো হয়?
* Business Logic Model-এ না Manager-এ রাখবে?
* Senior Project Structure

এটি এমন একটি topic যা **Junior থেকে Mid-Level Django Developer**-এ যাওয়ার জন্য খুবই গুরুত্বপূর্ণ।
# Django Model Design Mastery

# Lesson 8: Custom Managers & QuerySets Mastery (Senior Thinking)

আজকের lesson-এর পর তুমি বুঝবে কেন বড় Django project-এ শুধু

```python
Product.objects.all()
```

দিয়ে কাজ শেষ হয় না।

Production project-এ **Manager** এবং **QuerySet** business query-কে clean, reusable এবং maintainable করে।

---

# আজকের Goal

আজ শিখবে

* Manager কী?
* QuerySet কী?
* দুটির পার্থক্য
* Custom Manager
* Custom QuerySet
* Soft Delete Manager
* Real Project Pattern
* Senior Thinking

---

# Step 1: Manager কী?

ধরো Model

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
```

এখন

```python
Product.objects
```

এটা কী?

অনেকে বলে

> "objects দিয়ে query করি"

কিন্তু এটা আসলে

```text
Manager
```

---

## Manager-এর কাজ

Database-এর সাথে যোগাযোগ করা।

```
Product

↓

objects (Manager)

↓

Database
```

যখন লিখো

```python
Product.objects.all()
```

Flow

```
Product

↓

Manager

↓

SQL

↓

Database
```

---

# Beginner Thinking

```
objects = query
```

না।

```
objects = Manager
```

---

# Step 2: QuerySet কী?

```python
Product.objects.all()
```

Return করে

```python
<QuerySet>
```

এটা List না।

এটা Lazy Object।

---

Example

```python
products = Product.objects.all()
```

এখনও SQL execute হয়নি।

যখন

```python
for p in products:
    print(p.title)
```

তখন SQL execute হবে।

---

# Senior Rule

Manager

↓

Query শুরু করে

QuerySet

↓

Data নিয়ে কাজ করে

---

# Difference

| Manager              | QuerySet                |
| -------------------- | ----------------------- |
| Entry Point          | Query Result            |
| `Product.objects`    | `Product.objects.all()` |
| Database Access শুরু | Query Chain             |

---

# Step 3: কেন Custom Manager?

ধরো

Product

```python
is_active = models.BooleanField(default=True)
```

Project-এ

সব জায়গায়

```python
Product.objects.filter(is_active=True)
```

লিখছ।

১০০ জায়গায়।

---

এটা DRY?

না।

---

Better

```python
class ActiveProductManager(models.Manager):

    def get_queryset(self):
        return super().get_queryset().filter(
            is_active=True
        )
```

Model

```python
class Product(models.Model):

    ...

    objects = ActiveProductManager()
```

এখন

```python
Product.objects.all()
```

Automatically

Active Product দিবে।

---

# কিন্তু Problem

Inactive Product কোথায়?

---

Senior Pattern

```python
class Product(models.Model):

    objects = models.Manager()

    active = ActiveProductManager()
```

এখন

সব

```python
Product.objects.all()
```

Active

```python
Product.active.all()
```

---

# Step 4: Soft Delete Example

ধরো

Delete না করে

```python
is_deleted=True
```

করো।

---

Problem

```python
Product.objects.all()
```

Deleted Product-ও দেখাবে।

---

Solution

```python
class ActiveManager(models.Manager):

    def get_queryset(self):
        return (
            super()
            .get_queryset()
            .filter(is_deleted=False)
        )
```

Model

```python
class Product(models.Model):

    objects = models.Manager()

    active = ActiveManager()
```

Now

```python
Product.active.all()
```

Deleted বাদ।

---

# Step 5: QuerySet কেন দরকার?

ধরো

```python
Product.objects.filter(
    is_active=True
).filter(
    stock__gt=0
).filter(
    price__lt=1000
)
```

অনেকবার লাগছে।

---

Custom QuerySet

```python
class ProductQuerySet(models.QuerySet):

    def active(self):
        return self.filter(
            is_active=True
        )

    def in_stock(self):
        return self.filter(
            stock__gt=0
        )

    def cheap(self):
        return self.filter(
            price__lt=1000
        )
```

---

Manager

```python
class ProductManager(models.Manager):

    def get_queryset(self):
        return ProductQuerySet(
            self.model,
            using=self._db
        )
```

---

Model

```python
class Product(models.Model):

    objects = ProductManager()
```

এখন

```python
Product.objects.active()
```

```python
Product.objects.in_stock()
```

```python
Product.objects.active().cheap()
```

এগুলো chain করা যায়।

---

# আরও সুন্দর Pattern

Django-এর built-in helper:

```python
class ProductQuerySet(models.QuerySet):

    def active(self):
        return self.filter(is_active=True)

    def in_stock(self):
        return self.filter(stock__gt=0)


class Product(models.Model):

    objects = ProductQuerySet.as_manager()
```

এটা production-এ খুব common।

---

# Manager vs QuerySet

Manager

```python
Product.objects.create()
```

Good

Manager

---

QuerySet

```python
Product.objects.filter(...)
```

Good

---

Business Filter

```python
active()

published()

featured()
```

ভালো

QuerySet

---

# Real Project

Blog

```python
class PostQuerySet(models.QuerySet):

    def published(self):
        return self.filter(
            status="published"
        )

    def featured(self):
        return self.filter(
            featured=True
        )

    def this_year(self):
        return self.filter(
            created_at__year=2026
        )
```

Model

```python
objects = PostQuerySet.as_manager()
```

Query

```python
Post.objects.published()
```

```python
Post.objects.featured()
```

```python
Post.objects.published().featured()
```

Beautiful.

---

# E-commerce Example

```python
Product.objects

.active()

.in_stock()

.featured()

.by_category()

.by_brand()

.price_between()
```

সব chain হবে।

---

# Beginner Mistakes

## Mistake 1

সব Business Logic View-এ।

```python
Product.objects.filter(...)
```

১০০ বার।

---

## Mistake 2

Manager-এ

সব Method।

যেগুলো chain করা উচিত ছিল।

---

## Mistake 3

Duplicate Query।

---

# Senior Thinking

নিজেকে জিজ্ঞেস করো।

এই Query

```
১০ জায়গায় লাগবে?
```

Yes

↓

QuerySet Method

---

এই Query

```
সব Query-এর Base?
```

Yes

↓

Manager

---

# Production Structure

```
Product

↓

Manager

↓

QuerySet

↓

Database
```

---

# Real Production Example

```python
Product.objects.active().in_stock().order_by("-created_at")
```

View

```python
queryset = Product.objects.active()
```

Serializer

No Filtering.

View Clean.

---

# Interview Questions

## Q1.

Manager কী?

উত্তর

Database query শুরু করার Entry Point।

---

## Q2.

QuerySet কী?

উত্তর

Lazy collection of database queries যা chain করা যায়।

---

## Q3.

কখন Custom Manager বানাবে?

উত্তর

যখন default queryset পরিবর্তন করতে হবে অথবা model-level database access customize করতে হবে।

---

## Q4.

কখন QuerySet Method বানাবে?

উত্তর

যখন reusable filtering logic chainable করতে চাই।

---

# Senior Checklist

প্রতিটি বড় Model-এর জন্য ভাবো:

* Active records কি আলাদা Manager দরকার?
* Soft Delete আছে?
* একই filter কি বারবার লিখছি?
* Query কি chain হওয়া উচিত?
* Business filtering View-এ আছে নাকি QuerySet-এ?

---

# 🔥 Senior Tip (খুব গুরুত্বপূর্ণ)

অনেক developer Manager আর QuerySet গুলিয়ে ফেলে।

সহজ নিয়ম মনে রাখো:

**Manager = "কোথা থেকে query শুরু হবে"**

```python
Product.objects
```

**QuerySet = "query নিয়ে কী কী operation করা যাবে"**

```python
Product.objects.active().in_stock().featured()
```

---

# Homework

একটি `Order` model-এর জন্য `OrderQuerySet` design করো।

Business requirements:

* Pending orders
* Paid orders
* Cancelled orders
* Today's orders
* This month's orders

ভাবো:

1. কোনগুলো QuerySet method হবে?
2. Manager আলাদা লাগবে কি?
3. Query কীভাবে chain করবে?

---

# পরের Lesson (Lesson 9)

**Model Methods & Clean Architecture**

এখানে আমরা শিখব:

* `__str__()`
* `save()`
* `clean()`
* `full_clean()`
* `get_absolute_url()`
* Model method বনাম Service layer
* `save()` override কখন করা উচিত, কখন করা উচিত নয়
* Production-ready model design

এটি Django-এর সবচেয়ে misunderstood topic-গুলোর একটি।
# Django Model Design Mastery

# Lesson 9: Model Methods & Clean Architecture (Senior Thinking)

আজকের lesson Django-এর সবচেয়ে misunderstood topicগুলোর একটি।

অনেক developer সব logic `save()`-এ লিখে দেয়।
আবার কেউ Model-এ কোনো logic-ই রাখে না।

**Senior Developer জানে কোন logic Model-এ থাকবে, কোনটা Service Layer-এ যাবে, আর কোনটা Serializer/View-এ যাবে।**

---

# আজকের Goal

আজ তুমি শিখবে:

* `__str__()`
* Model Properties
* Model Methods
* `save()`
* `clean()`
* `full_clean()`
* `get_absolute_url()`
* Business Logic কোথায় থাকবে?
* Senior Design Rules

---

# Step 1: `__str__()`

ধরো Model

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
```

Admin Panel

```
Product object (1)

Product object (2)

Product object (3)
```

Useful?

না।

---

Correct

```python
class Product(models.Model):
    title = models.CharField(max_length=200)

    def __str__(self):
        return self.title
```

Admin

```
Laptop

Keyboard

Mouse
```

---

## Senior Rule

`__str__()` সবসময় এমন কিছু return করবে যা **human-readable** এবং object-টিকে সহজে চিনতে সাহায্য করে।

---

### Bad Example

```python
def __str__(self):
    return str(self.id)
```

---

### Better

```python
def __str__(self):
    return self.email
```

অথবা

```python
return self.name
```

---

# Step 2: Model Method

Model-এর নিজের behavior Model-এর মধ্যেই থাকবে।

Example

```python
class Product(models.Model):

    price = models.DecimalField(...)
    discount = models.DecimalField(...)

    def final_price(self):
        return self.price - self.discount
```

Usage

```python
product.final_price()
```

---

আরেকটা

```python
class Order(models.Model):

    def is_paid(self):
        return self.status == "paid"
```

Usage

```python
if order.is_paid():
    ...
```

---

## Senior Rule

যে logic **একটি object-এর নিজের**, সেটা Model Method।

---

# Step 3: Property

সব method-এ `()` ব্যবহার করতে ভালো লাগে না।

Example

```python
@property
def final_price(self):
    return self.price - self.discount
```

এখন

```python
product.final_price
```

---

কখন Property?

যখন

* কোনো parameter লাগবে না
* শুধু value calculate করবে

---

# Step 4: `save()`

এটাই সবচেয়ে dangerous topic।

---

Normal Save

```python
product.save()
```

---

Override

```python
def save(self, *args, **kwargs):

    self.slug = slugify(self.title)

    super().save(*args, **kwargs)
```

---

এখন

```python
title = "Gaming Laptop"
```

Save করলে

```
gaming-laptop
```

Automatically।

---

# Beginner Mistake ১

```python
def save(self):

    ...
```

`*args, **kwargs` ভুলে যায়।

---

Correct

```python
def save(self, *args, **kwargs):

    ...

    super().save(*args, **kwargs)
```

---

# Beginner Mistake ২

```python
def save(...):

    self.save()
```

Infinite Recursion।

```
save()

↓

save()

↓

save()

↓

Crash
```

---

সবসময়

```python
super().save()
```

---

# Step 5: `clean()`

Model Validation।

Example

```python
class Product(models.Model):

    price = models.DecimalField(...)
    discount = models.DecimalField(...)

    def clean(self):

        if self.discount > self.price:
            raise ValidationError(
                "Discount cannot exceed price."
            )
```

---

এটা Business Rule।

Serializer Validation না।

Model Validation।

---

# Step 6: `full_clean()`

এখানে একটা গুরুত্বপূর্ণ বিষয় আছে।

অনেকে ভাবে

```python
product.save()
```

Automatically

```python
clean()
```

Call করবে।

❌ ভুল।

---

Reality

```
save()

↓

clean() হয় না।
```

তোমাকে

```python
product.full_clean()
```

Call করতে হবে।

---

Production Pattern

```python
product.full_clean()

product.save()
```

---

অনেক Project-এ

Serializer validation থাকে।

তাই সবসময় `full_clean()` call করা হয় না।

---

# Step 7: `get_absolute_url()`

Django-এর পুরোনো কিন্তু useful feature।

```python
from django.urls import reverse

class Product(models.Model):

    slug = models.SlugField()

    def get_absolute_url(self):

        return reverse(
            "product-detail",
            kwargs={
                "slug": self.slug
            }
        )
```

Usage

```python
product.get_absolute_url()
```

Output

```
/products/gaming-laptop/
```

---

# Step 8: Business Logic কোথায় থাকবে?

এটাই Senior Level Thinking।

ধরো

Order Total।

---

Wrong

Serializer

```python
total = ...
```

View

```python
total = ...
```

Admin

```python
total = ...
```

একই Logic তিন জায়গায়।

---

Better

```python
class Order(models.Model):

    @property
    def total(self):

        ...
```

সব জায়গায়

```python
order.total
```

---

# কিন্তু...

Payment Gateway Call?

Model-এ?

না।

Email Send?

Model-এ?

না।

SMS?

Model-এ?

না।

Inventory Update?

Depends।

---

# Senior Rule

## Model-এ থাকবে

✔ Object-এর নিজের behavior

Example

```python
order.total

product.final_price

user.full_name
```

---

## Model-এ থাকবে না

❌ Email

❌ Payment Gateway

❌ Stripe

❌ SSLCommerz

❌ Redis

❌ Celery

❌ External API

---

এসব Service Layer।

---

# Real Example

Bad

```python
class Order(models.Model):

    def save(...):

        send_email()

        update_stock()

        charge_card()

        create_invoice()

        ...
```

Monster Save Method।

---

Good

```python
class Order(models.Model):

    @property
    def total(self):

        ...
```

Service

```python
class OrderService:

    def checkout(...):

        ...

        payment

        inventory

        invoice

        email
```

Much Better।

---

# Step 9: Signals vs save()

অনেকে

সব

Signal-এ দেয়।

আবার

সব

save()-এ দেয়।

Senior Rule

Simple Model-specific work

↓

save()

---

Complex Workflow

↓

Service

---

Cross App Communication

↓

Signal (সীমিতভাবে)

---

# Production Example

```python
class Product(models.Model):

    title = models.CharField(max_length=200)

    slug = models.SlugField(unique=True)

    price = models.DecimalField(...)

    discount = models.DecimalField(...)

    def __str__(self):
        return self.title

    @property
    def final_price(self):
        return self.price - self.discount

    def clean(self):

        if self.discount > self.price:

            raise ValidationError(
                "Invalid discount."
            )

    def save(self, *args, **kwargs):

        self.slug = slugify(self.title)

        super().save(*args, **kwargs)
```

এটা Clean।

---

# Beginner Mistakes

## Mistake 1

সব logic View-এ।

---

## Mistake 2

সব logic Serializer-এ।

---

## Mistake 3

সব logic save()-এ।

---

## Mistake 4

`super().save()` ভুলে যায়।

---

## Mistake 5

`save()`-এর ভিতরে `self.save()`।

---

## Mistake 6

`clean()` আছে মনে করে Validation হয়ে যাবে।

হয় না।

---

# Senior Decision Tree

নিজেকে প্রশ্ন করো।

## এটা কি Object-এর behavior?

↓

Model Method

---

Value Calculate?

↓

@property

---

Database Save-এর আগে কিছু Update?

↓

save()

---

Business Validation?

↓

clean()

---

Email?

↓

Service

---

Payment?

↓

Service

---

Inventory?

↓

Service

---

# Interview Questions

### Q1.

`save()` override করার সময় সবচেয়ে গুরুত্বপূর্ণ কী?

**উত্তর:**

সবসময়

```python
super().save(*args, **kwargs)
```

call করতে হবে।

---

### Q2.

`clean()` কি `save()`-এর সময় automatically call হয়?

**উত্তর:**

না।

`full_clean()` call করলে `clean()` execute হয়।

---

### Q3.

কখন Model Method ব্যবহার করবে?

**উত্তর:**

যখন logic একটি নির্দিষ্ট object-এর behavior বা state-এর সাথে সম্পর্কিত।

---

### Q4.

Payment processing কোথায় থাকবে?

**উত্তর:**

Service Layer-এ।

---

### Q5.

`@property` কখন ব্যবহার করবে?

**উত্তর:**

যখন parameter ছাড়া calculated value expose করতে চাই।

---

# Senior Checklist

প্রতিটি Model-এর জন্য ভাবো:

* ভালো `__str__()` আছে?
* কোনো calculated field `@property` হতে পারে?
* `save()` কি খুব বড় হয়ে গেছে?
* Business validation `clean()`-এ থাকা উচিত?
* External API call কি ভুল করে Model-এ চলে এসেছে?

---

# Homework

একটি `Order` model কল্পনা করো।

Fields:

* subtotal
* tax
* shipping_cost
* discount
* status

Design করো:

1. `__str__()` কী return করবে?
2. `@property total` কীভাবে calculate করবে?
3. `clean()`-এ কোন validation লিখবে?
4. `save()`-এ কী কাজ করা যুক্তিযুক্ত?
5. কোন কাজ Service Layer-এ যাবে?

---

# 🎯 এখান পর্যন্ত তুমি Model Design-এর Core Foundation শেষ করেছ

এখন তুমি জানো:

* Model Design
* Field Selection
* Relationships
* `on_delete`
* Meta
* Inheritance
* Managers & QuerySets
* Model Methods

এগুলো মিলিয়ে তুমি production-ready model design করতে পারবে।

## পরের Lesson (Lesson 10)

**Database Normalization & Real-World Schema Design**

এটি সবচেয়ে গুরুত্বপূর্ণ architectural lessonগুলোর একটি। আমরা শিখব:

* 1NF, 2NF, 3NF (সহজ ভাষায়)
* কখন data আলাদা model-এ ভাঙবে?
* কখন duplicate data রাখা ঠিক?
* Snapshot data কী?
* E-commerce, Hospital, SaaS-এর real database design
* Senior architect কীভাবে schema design করে

এই lesson-এর পর তুমি শুধু Django Model নয়, **Database Designer-এর মতো চিন্তা করতে শুরু করবে।**
# Django Model Design Mastery

# Lesson 10: Database Normalization & Real-World Schema Design (Senior Thinking)

এটি পুরো course-এর **সবচেয়ে গুরুত্বপূর্ণ lesson**।

কারণ Django Model শেখা আর **Database Design শেখা এক জিনিস নয়**।

একজন Senior Django Developer আসলে একজন **Database Designer**-ও।

---

# আজকের Goal

আজ তুমি শিখবে:

* Normalization কী?
* 1NF, 2NF, 3NF (সহজ ভাষায়)
* Duplicate Data কখন খারাপ?
* Duplicate Data কখন ভালো?
* Snapshot Data
* Real-world Database Design
* Senior Thinking Framework

---

# Step 1: Normalization কী?

সহজ ভাষায়,

> **Data এমনভাবে organize করা যাতে unnecessary duplicate না হয় এবং update করতে সমস্যা না হয়।**

Example

খারাপ Design

| Product  | Category    |
| -------- | ----------- |
| Laptop   | Electronics |
| Mouse    | Electronics |
| Keyboard | Electronics |

এখন

```text
Electronics
```

এর নাম পরিবর্তন করে

```text
Electronic Devices
```

করতে হলে

৩টি Row update করতে হবে।

---

Better Design

Category Table

| id | name        |
| -- | ----------- |
| 1  | Electronics |

Product Table

| Product  | category_id |
| -------- | ----------- |
| Laptop   | 1           |
| Mouse    | 1           |
| Keyboard | 1           |

এখন

এক জায়গায় Update।

---

# Senior Rule

একটি তথ্যের **একটি Source of Truth** থাকবে।

---

# Step 2: First Normal Form (1NF)

Rule

> **একটি Cell-এ একটি Value।**

---

❌ Bad

| id | tags              |
| -- | ----------------- |
| 1  | Python,Django,DRF |

একটা Cell-এ তিনটা Value।

---

✅ Better

Tag Table

| id | name   |
| -- | ------ |
| 1  | Python |
| 2  | Django |
| 3  | DRF    |

PostTag Table

| post_id | tag_id |
| ------- | ------ |
| 1       | 1      |
| 1       | 2      |
| 1       | 3      |

---

### Django

```python
class Tag(models.Model):
    name = models.CharField(max_length=100)

class Post(models.Model):
    tags = models.ManyToManyField(Tag)
```

---

# Beginner Mistake

```python
tags = models.CharField(max_length=500)
```

তারপর

```text
Python,Django,DRF
```

Store করে।

❌

---

# Step 3: Second Normal Form (2NF)

Rule

> **একটি Table-এর Data শুধুমাত্র সেই Table-এর Entity সম্পর্কিত হবে।**

---

Bad

Student Table

| Student | Course | Teacher |
| ------- | ------ | ------- |

Teacher আসলে Course-এর।

Student-এর না।

---

Better

Student

Course

Teacher

আলাদা Model।

---

# Step 4: Third Normal Form (3NF)

Rule

> **একটি Non-key Field অন্য Non-key Field-এর উপর depend করবে না।**

সহজ Example

User

| Name | ZipCode | City |

City ZipCode থেকে বের করা যায়।

তাহলে

City duplicate।

Better

ZipCode Table

---

বাস্তবে

অনেক Project-এ

Performance-এর জন্য

City রাখেও।

Business-এর উপর নির্ভর করে।

---

# Step 5: Duplicate Data সবসময় খারাপ?

না।

এটাই Senior Thinking।

---

Example

Order

```text
Product Price = 100
```

Customer Order করল।

পরে Product Price হলো

```text
120
```

Order History?

100 থাকবে।

---

তাই

OrderItem

```python
price = models.DecimalField(...)
```

আলাদা রাখি।

এটা Duplicate?

হ্যাঁ।

কিন্তু Intentional।

---

এটাকে বলে

**Snapshot Data**।

---

# Step 6: Snapshot Data

Product

```text
Current Price

150
```

Order

```text
Purchased Price

120
```

Product Price Change

↓

Order Change হবে?

না।

---

Senior Rule

Historical Data কখনও Current Table-এর উপর নির্ভর করবে না।

---

# Step 7: E-commerce Schema

Business

Seller Product বিক্রি করে।

---

Entities

```text
Seller

Category

Product

ProductImage

ProductVariant

Inventory

Cart

CartItem

Order

OrderItem

Payment

Review
```

---

Relationship

```text
Seller

↓

Product

↓

Variant

↓

Inventory
```

---

Order

↓

OrderItem

↓

Snapshot Price

---

# কেন Snapshot?

আজ

Laptop

```text
1000
```

Customer কিনল।

কাল

```text
1500
```

Order History

1000 থাকবে।

---

# Step 8: Hospital Schema

Entities

```text
Doctor

Patient

Appointment

Prescription

Medicine
```

---

Bad

Prescription

```text
Medicine1

Medicine2

Medicine3
```

একটা Field-এ।

---

Better

Prescription

↓

PrescriptionItem

↓

Medicine

---

# Step 9: SaaS Schema

Entities

```text
Company

User

Subscription

Plan

Invoice

Payment
```

---

Invoice

Plan Price Copy করবে।

কারণ

Plan পরে Change হবে।

---

# Step 10: Denormalization

Normalization-এর উল্টো।

---

Example

Review

```text
Product Rating

4.6
```

প্রতিবার

Average Calculate?

Slow।

---

তাই

Product Table

```python
average_rating
```

Store।

Duplicate?

হ্যাঁ।

কিন্তু

Fast।

---

# Senior Rule

Read অনেক বেশি হলে

Denormalization acceptable।

---

# Step 11: Real Thinking

ধরো

Blog।

Beginner

```python
class Post(models.Model):

    comments = models.IntegerField()
```

---

Senior

```text
Comment Model
```

কিন্তু

Comment Count

Store করতে পারে।

Performance-এর জন্য।

---

# Step 12: Source of Truth

একটা Data-এর

একটাই Source থাকবে।

---

Bad

Product

```text
Stock = 10
```

Inventory

```text
Stock = 10
```

দুই জায়গায়।

কাল

একটা Update হলো।

আরেকটা হলো না।

Bug।

---

Better

Inventory

↓

Source of Truth

---

# Step 13: Real Production Example

Order

```python
Order
```

↓

```python
OrderItem
```

OrderItem

```python
product_name

price

quantity

tax

discount
```

কেন?

কারণ এগুলো

Purchase Time-এর Snapshot।

---

# Step 14: Beginner Mistakes

## Mistake 1

সব Data এক Model-এ।

---

## Mistake 2

Comma দিয়ে List Store।

---

## Mistake 3

Historical Data Copy না করা।

---

## Mistake 4

সব Normalize।

Performance খারাপ।

---

## Mistake 5

সব Denormalize।

Data Inconsistency।

---

# Senior Decision Tree

নিজেকে প্রশ্ন করো।

## এই Data কি একাধিক জায়গায় ব্যবহার হবে?

↓

Separate Model।

---

## এই Data কি ভবিষ্যতে Change হবে?

↓

Snapshot দরকার?

---

## এটা কি Calculation?

↓

Property?

Annotation?

Stored Field?

---

## Performance কি Problem?

↓

Denormalize।

---

# Real E-commerce Example

```text
Category

↓

Product

↓

Variant

↓

Inventory

↓

OrderItem
```

OrderItem

```text
price

tax

discount

product_name
```

সব Snapshot।

---

Product

```text
Current Price
```

---

# Interview Questions

### Q1.

Normalization কেন?

**উত্তর:**

Duplicate Data কমানো, consistency বজায় রাখা এবং update anomaly এড়ানোর জন্য।

---

### Q2.

Snapshot Data কী?

**উত্তর:**

যে Data Transaction-এর সময় Copy করে রাখা হয়, যাতে ভবিষ্যতে মূল Data পরিবর্তন হলেও History অপরিবর্তিত থাকে।

---

### Q3.

Duplicate Data সবসময় খারাপ?

**উত্তর:**

না। Historical record এবং performance optimization-এর জন্য Intentional duplicate (Denormalization) করা হয়।

---

### Q4.

OrderItem-এ Price কেন রাখা হয়?

**উত্তর:**

কারণ Product-এর বর্তমান Price ভবিষ্যতে পরিবর্তন হতে পারে, কিন্তু Order History অপরিবর্তিত থাকতে হবে।

---

# Senior Database Checklist

প্রতিটি নতুন Model Design-এর আগে নিজেকে জিজ্ঞেস করো:

### ১

এটা কি নতুন Entity?

↓

নতুন Model।

---

### ২

এটা কি Relationship?

↓

ForeignKey / ManyToMany।

---

### ৩

এটা কি History?

↓

Snapshot।

---

### ৪

এটা কি Calculation?

↓

Runtime না Stored?

---

### ৫

Performance কি Concern?

↓

Denormalization।

---

# 🧠 Senior Architect Thinking

যখন Business Requirement পাবে, **সরাসরি Model লিখবে না।**

এই ৮টি ধাপ অনুসরণ করো:

1. **Entity বের করো** (User, Product, Order...)
2. **Relationship আঁকো**
3. **Source of Truth নির্ধারণ করো**
4. **History কোথায় রাখতে হবে ভাবো**
5. **Snapshot দরকার কি না ঠিক করো**
6. **Performance bottleneck কোথায় হতে পারে ভাবো**
7. **Normalization বনাম Denormalization-এর balance করো**
8. **তারপর Django Model লেখা শুরু করো**

---

# Homework (Senior-Level Design)

একটি **Food Delivery System**-এর Database Design করো।

Business Requirements:

* Restaurant খাবার বিক্রি করবে।
* Customer Order করবে।
* প্রতিটি Order-এ একাধিক Food Item থাকবে।
* Food-এর দাম ভবিষ্যতে পরিবর্তন হতে পারে।
* Customer Review দিতে পারবে।
* Delivery Rider Order Deliver করবে।

ভাবো:

1. কী কী Entity লাগবে?
2. কোনগুলো `ForeignKey`?
3. কোনগুলো `ManyToMany`?
4. কোথায় Snapshot Data রাখবে?
5. কোন Table হবে Source of Truth?

---

## 🎯 এখান থেকে তুমি Junior Model Designer নও

Lesson 1–10 শেষ করার পর তুমি Django Model-এর syntax নয়, **Database Design-এর চিন্তাভাবনা** শিখেছ।

### পরের Lesson (Lesson 11)

**Database Performance & Query Optimization from Model Design**

এখানে আমরা শিখব:

* Model design কীভাবে query performance প্রভাবিত করে
* N+1 Problem-এর মূল কারণ
* `select_related()` বনাম `prefetch_related()`
* Index strategy
* Large table design
* Production database optimization

এই lesson-এর পর তুমি **Model শুধু সঠিক নয়, দ্রুত (fast)** বানাতেও শিখবে।
# Django Model Design Mastery

# Lesson 11: Database Performance & Query Optimization from Model Design (Senior Thinking)

এটি এমন একটি topic যেখানে **ভালো Django Developer** আর **Senior Django Developer**-এর পার্থক্য সবচেয়ে বেশি দেখা যায়।

একজন Junior ভাবে:

> "API কাজ করছে।"

একজন Senior ভাবে:

> "API কতটি Query করছে?"

---

# আজকের Goal

আজ শিখবে:

* Performance Thinking
* N+1 Problem
* `select_related()`
* `prefetch_related()`
* `only()`
* `defer()`
* `exists()`
* `count()`
* `annotate()`
* Model Design কীভাবে Performance-কে প্রভাবিত করে
* Senior Checklist

---

# Step 1: Performance শুরু হয় Model Design থেকেই

অনেকে মনে করে

```text
Performance = পরে optimize করবো
```

এটা ভুল।

Performance শুরু হয়

```text
Model Design

↓

Query Design

↓

Database Index

↓

API
```

---

# Example

Model

```python
class Product(models.Model):
    seller = models.ForeignKey(
        Seller,
        on_delete=models.CASCADE
    )

    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE
    )
```

এখন API

```python
products = Product.objects.all()

for product in products:
    print(product.seller.name)
```

Problem?

হ্যাঁ।

---

# Step 2: N+1 Query Problem

ধরো

১০০টা Product আছে।

প্রথম Query

```sql
SELECT * FROM product;
```

তারপর

প্রতি Product-এর জন্য

```sql
SELECT * FROM seller WHERE id=...
```

১০০ বার।

মোট

```text
1 + 100 = 101 Queries
```

এটাকে বলে

# N+1 Problem

---

## Visual

Without optimization

```text
Product

↓

Query 1

↓

Seller

↓

100 Queries
```

---

# Solution

```python
products = Product.objects.select_related(
    "seller"
)
```

এখন

```text
1 Query
```

JOIN করে Data নিয়ে আসে।

---

# Senior Rule

**ForeignKey** বা **OneToOneField** access করলে প্রথমে ভাবো:

> **select_related লাগবে কি?**

---

# Step 3: select_related()

Works With

✅ ForeignKey

✅ OneToOneField

---

Example

```python
Product.objects.select_related(
    "seller",
    "category"
)
```

SQL

```text
JOIN

Seller

Category
```

এক Query।

---

# Step 4: prefetch_related()

ManyToMany

Reverse ForeignKey

এর জন্য।

Example

```python
class Product:

    reviews
```

API

```python
products = Product.objects.prefetch_related(
    "reviews"
)
```

Without

```text
101 Queries
```

With

```text
2 Queries
```

---

# Difference

| select_related | prefetch_related |
| -------------- | ---------------- |
| JOIN           | Separate Query   |
| ForeignKey     | ManyToMany       |
| OneToOne       | Reverse FK       |

---

# Easy Trick

একটা Relationship

```text
Product

↓

Seller
```

এক Seller।

↓

select_related

---

একটা Relationship

```text
Product

↓

Reviews
```

অনেক Review।

↓

prefetch_related

---

# Step 5: only()

ধরো

Product Table

```text
title

description

image

price

slug

created_at

updated_at
```

API-তে দরকার

```text
title

price
```

তাহলে

```python
Product.objects.only(
    "title",
    "price"
)
```

সব Field Load করবে না।

---

# Step 6: defer()

উল্টো।

সব Field

Except

```python
Product.objects.defer(
    "description"
)
```

Large Text হলে Useful।

---

# Step 7: exists()

অনেকে লেখে

```python
if Product.objects.filter(
    slug=slug
):
```

অথবা

```python
len(Product.objects.filter(...))
```

❌

---

Correct

```python
Product.objects.filter(
    slug=slug
).exists()
```

Much Faster।

---

# Step 8: count()

অনেকে

```python
len(Product.objects.all())
```

❌

কারণ সব Data Load হবে।

---

Correct

```python
Product.objects.count()
```

Database

```sql
COUNT(*)
```

---

# Step 9: annotate()

ধরো

Product

↓

Review

Average Rating।

---

Wrong

Python Loop

```python
for product:

    avg(...)
```

---

Correct

```python
Product.objects.annotate(
    avg_rating=Avg("reviews__rating")
)
```

Database Calculate করবে।

---

# Step 10: values()

যদি Serializer না লাগে।

```python
Product.objects.values(
    "id",
    "title"
)
```

Model Object না।

Dictionary।

Fast।

---

# Step 11: values_list()

আরও Lightweight।

```python
Product.objects.values_list(
    "id",
    flat=True
)
```

Output

```text
1

2

3
```

---

# Step 12: Index Thinking

ধরো

```python
Product.objects.filter(
    slug=slug
)
```

প্রতিদিন

১ লাখ বার।

Index।

---

Search

```python
email
```

Index।

---

ForeignKey

Already Indexed।

---

# Beginner Mistake

সব Field-এ

Index।

না।

Index-এর Cost আছে।

---

# Step 13: QuerySet Evaluation

অনেকে জানে না।

```python
products = Product.objects.all()
```

SQL হয়নি।

---

কখন হবে?

```python
list(products)
```

```python
len(products)
```

```python
for p in products
```

```python
bool(products)
```

---

# Step 14: Caching QuerySet?

না।

QuerySet Lazy।

বারবার Evaluate হতে পারে।

প্রয়োজন হলে

```python
products = list(
    Product.objects.all()
)
```

---

# Step 15: Real E-commerce Example

Homepage

Needs

```text
Product

Seller

Category

Average Rating
```

Senior Query

```python
Product.objects.select_related(
    "seller",
    "category"
).annotate(
    avg_rating=Avg(...)
)
```

এক Query।

---

# Bad Example

```python
for product:

    seller

    category

    reviews
```

300 Queries।

---

# Model Design Mistakes That Hurt Performance

## Mistake 1

সব Relationship Lazy রেখে API-তে Loop করা।

---

## Mistake 2

Large JSON Field যেখানে Relation হওয়া উচিত ছিল।

---

## Mistake 3

Comma-separated Data।

---

## Mistake 4

Missing Index।

---

## Mistake 5

Huge Model।

৫০টা Field।

---

# Senior Performance Checklist

প্রতিটি API-এর জন্য নিজেকে জিজ্ঞেস করো।

### কয়টা Query হচ্ছে?

Django Debug Toolbar বা query log দিয়ে দেখো।

---

### ForeignKey Access?

↓

`select_related()`

---

### ManyToMany?

↓

`prefetch_related()`

---

### শুধু Count?

↓

`count()`

---

### শুধু Exists?

↓

`exists()`

---

### Aggregate?

↓

`annotate()`

---

### সব Field লাগবে?

↓

`only()` / `defer()`

---

# Real Interview Questions

## Q1.

N+1 কী?

উত্তর

একটি Query-এর পরে প্রতিটি Row-এর জন্য আলাদা Query হওয়া।

---

## Q2.

`select_related()` আর `prefetch_related()` পার্থক্য?

**উত্তর:**

* `select_related()` SQL JOIN ব্যবহার করে এবং `ForeignKey`/`OneToOneField`-এর জন্য।
* `prefetch_related()` আলাদা Query চালিয়ে Python-এ relation মিলিয়ে দেয় এবং `ManyToMany` ও reverse relation-এর জন্য।

---

## Q3.

`count()` কেন `len(queryset)` থেকে ভালো?

**উত্তর:**

`count()` Database-এ `COUNT(*)` চালায়। `len(queryset)` সব row memory-তে এনে তারপর count করে।

---

## Q4.

`exists()` কেন ব্যবহার করবে?

**উত্তর:**

শুধু record আছে কি না জানতে। এটি পুরো object load করে না।

---

# Senior Architect Mindset

একটি API লেখার আগে ৫টি প্রশ্ন করো:

1. **কোন relationship লাগবে?**
2. **কতগুলো query হবে?**
3. **Index আছে?**
4. **Database কি কাজটা করতে পারে? (aggregate/annotate)**
5. **Python loop এড়ানো যায় কি?**

---

# 🧠 Golden Rules (মুখস্থ করার মতো)

| Situation         | Best Choice          |
| ----------------- | -------------------- |
| ForeignKey access | `select_related()`   |
| ManyToMany access | `prefetch_related()` |
| Record আছে?       | `exists()`           |
| Total count       | `count()`            |
| Aggregate         | `annotate()`         |
| কিছু field দরকার  | `only()`             |
| কিছু field বাদ    | `defer()`            |
| Dictionary output | `values()`           |
| Single column     | `values_list()`      |

---

# Homework

একটি Blog API design করো।

Models:

* Post
* Author
* Category
* Comment

Homepage-এ দেখাতে হবে:

* Post Title
* Author Name
* Category Name
* Total Comment Count

ভাবো:

1. কোথায় `select_related()` ব্যবহার করবে?
2. কোথায় `annotate()` ব্যবহার করবে?
3. কতটি Query-তে API শেষ করা সম্ভব?
4. কোন field-এ index দরকার?

---

# 🎯 Model Mastery Status

এখন পর্যন্ত তুমি শিখেছ:

* ✅ Model Design
* ✅ Relationships
* ✅ `on_delete`
* ✅ Meta
* ✅ Inheritance
* ✅ Managers & QuerySets
* ✅ Model Methods
* ✅ Database Normalization
* ✅ Query Performance

এগুলো Django Model-এর **Core + Advanced Foundation**।

## পরের Lesson (Lesson 12)

**Database Transactions & Concurrency (Production-Level Data Integrity)**

এখানে আমরা শিখব:

* `transaction.atomic()`
* Savepoint
* Rollback
* Race Condition
* `select_for_update()`
* Double payment, overselling stock-এর মতো real production problem কীভাবে সমাধান করতে হয়।

এই lesson production backend development-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
# Django Model Design Mastery

# Lesson 12: Database Transactions & Concurrency (Production-Level Data Integrity)

এটি এমন একটি lesson যা **প্রতিটি Backend Developer-এর অবশ্যই জানা উচিত**।

অনেক API দেখতে ঠিকঠাক কাজ করে, কিন্তু **একই সময়ে (concurrent requests)** ১০০ জন user ব্যবহার করলে bug শুরু হয়।

Senior Developer-এর চিন্তা:

> **"একজন User নয়, ১০,০০০ User একসাথে Request পাঠালে কী হবে?"**

---

# আজকের Goal

আজ শিখবে

* Transaction কী?
* ACID কী?
* `transaction.atomic()`
* Rollback
* Savepoint
* Race Condition
* `select_for_update()`
* F() Expression
* Real Production Examples
* Senior Thinking

---

# Step 1: Transaction কী?

ধরো Checkout API।

Customer Order করলো।

তোমাকে ৪টা কাজ করতে হবে।

```text
1. Order Create

↓

2. OrderItem Create

↓

3. Stock কমাও

↓

4. Payment Save
```

এগুলো একসাথে সফল হওয়া উচিত।

---

Problem

```text
Order Create ✔

OrderItem ✔

Stock ✔

Payment ❌
```

এখন?

Database-এ অর্ধেক Data Save হয়েছে।

Business নষ্ট।

---

Solution

Transaction।

---

# Step 2: Transaction মানে কী?

Transaction মানে

```text
সব হবে

অথবা

কিছুই হবে না।
```

---

Visualization

Without Transaction

```text
Order ✔

Item ✔

Stock ✔

Payment ❌

↓

Broken Database
```

---

With Transaction

```text
Order

↓

Item

↓

Stock

↓

Payment ❌

↓

Rollback

↓

কিছুই Save হবে না
```

---

# Step 3: transaction.atomic()

Example

```python
from django.db import transaction

with transaction.atomic():

    order = Order.objects.create(...)

    OrderItem.objects.create(...)

    payment = Payment.objects.create(...)
```

যদি

Payment Error

↓

সব Rollback।

---

# Step 4: ACID (Interview Favorite)

Database Transaction-এর ৪টি Rule।

---

## A = Atomicity

সব হবে

অথবা

কিছুই হবে না।

---

## C = Consistency

Database সবসময় Valid State-এ থাকবে।

---

## I = Isolation

এক Transaction অন্য Transaction-এর মাঝখানে interfere করবে না।

---

## D = Durability

Commit হয়ে গেলে Data হারাবে না।

---

# Step 5: Rollback

Example

```python
with transaction.atomic():

    Order.objects.create(...)

    raise Exception()
```

কি হবে?

```text
Rollback
```

Order Save হবে না।

---

# Step 6: Nested Transaction

```python
with transaction.atomic():

    ...

    with transaction.atomic():

        ...
```

Django Savepoint তৈরি করে।

---

যদি ভিতরের অংশে Error হয়

সবসময় পুরো Transaction Rollback হবে না; Savepoint পর্যন্ত Rollback হতে পারে।

---

# Step 7: Race Condition

এটাই সবচেয়ে গুরুত্বপূর্ণ।

ধরো

Stock

```text
1
```

---

Customer A

এবং

Customer B

একসাথে Buy করলো।

---

Timeline

```text
A Read Stock = 1

B Read Stock = 1

A Buy

Stock = 0

B Buy

Stock = -1
```

Problem।

এটাকে বলে

# Race Condition

---

# Step 8: Wrong Code

```python
product = Product.objects.get(id=1)

if product.stock > 0:

    product.stock -= 1

    product.save()
```

একই সময়ে দুই Request এলে Problem।

---

# Step 9: select_for_update()

Solution

```python
from django.db import transaction

with transaction.atomic():

    product = Product.objects.select_for_update().get(id=1)

    if product.stock <= 0:

        raise Exception()

    product.stock -= 1

    product.save()
```

---

কি হলো?

Database Row Lock।

অন্য Transaction অপেক্ষা করবে।

---

Visualization

```text
Request A

↓

Lock Product

↓

Update

↓

Unlock
```

---

Request B

```text
Wait
```

---

# Senior Rule

Money

Stock

Wallet

Coupon

Balance

এসব Update?

↓

`select_for_update()`

---

# Step 10: F() Expression

আরও ভালো উপায়।

Wrong

```python
product.stock -= 1

product.save()
```

---

Better

```python
from django.db.models import F

Product.objects.filter(
    id=1
).update(

    stock=F("stock") - 1
)
```

Database-এই Calculation হবে।

---

আরও Safe

```python
updated = Product.objects.filter(
    id=1,
    stock__gt=0
).update(

    stock=F("stock") - 1
)

if updated == 0:
    raise Exception("Out of stock")
```

এখানে আলাদা করে Stock Read করার দরকার নেই।

---

# Step 11: Banking Example

Account

```text
Balance

100
```

Transfer

```text
-50

+50
```

Transaction ছাড়া?

Danger।

---

Correct

```python
with transaction.atomic():

    sender...

    receiver...
```

---

# Step 12: E-commerce Checkout

Transaction-এর ভিতরে

```text
Create Order

↓

Create Items

↓

Decrease Stock

↓

Save Payment

↓

Commit
```

---

কোনো Error

↓

Rollback।

---

# Step 13: Coupon Example

Coupon

```text
Limit

1
```

দুই User একসাথে ব্যবহার করলো।

Without Lock

দুজনই Coupon ব্যবহার করবে।

---

Solution

```python
select_for_update()
```

---

# Step 14: Inventory Example

Product

```text
Stock

5
```

১০ জন একসাথে কিনলো।

Without Lock

Negative Stock।

---

Production

```python
select_for_update()
```

অথবা

```python
F()
```

---

# Step 15: Common Mistakes

## Mistake 1

Checkout API-তে

Transaction নেই।

---

## Mistake 2

Balance Update

Normal Save।

---

## Mistake 3

Stock

Python Variable-এ কমানো।

---

## Mistake 4

১০টা Query

Atomic-এর বাইরে।

---

## Mistake 5

External API Call Transaction-এর ভিতরে।

Example

```python
with transaction.atomic():

    Stripe API

    SSLCommerz API

    Email
```

❌

কারণ Transaction অনেকক্ষণ Lock ধরে রাখবে।

---

# Senior Pattern

```text
Transaction

↓

Database Work

↓

Commit

↓

Email

↓

Notification

↓

Celery Task
```

Database Lock যত কম সময় থাকবে তত ভালো।

---

# Production Example

```python
from django.db import transaction
from django.db.models import F

with transaction.atomic():

    product = Product.objects.select_for_update().get(pk=1)

    if product.stock <= 0:
        raise ValidationError("Out of stock")

    Product.objects.filter(pk=product.pk).update(
        stock=F("stock") - 1
    )

    order = Order.objects.create(...)
```

---

# Interview Questions

### Q1.

`transaction.atomic()` কী?

**উত্তর:**

একটি block-এর সব database operation-কে একটি transaction হিসেবে execute করে। কোনো error হলে সব rollback হয়।

---

### Q2.

Race Condition কী?

**উত্তর:**

একই data-তে একাধিক request একসাথে কাজ করে ভুল ফলাফল তৈরি করলে তাকে Race Condition বলে।

---

### Q3.

`select_for_update()` কখন ব্যবহার করবে?

**উত্তর:**

যখন একই row update করার সম্ভাবনা থাকে, যেমন stock, wallet balance, bank account, coupon usage।

---

### Q4.

`F()` Expression-এর সুবিধা কী?

**উত্তর:**

Database-এই value update হয়। Python-এ read-modify-write করার কারণে যে race condition হতে পারে, তা কমায়।

---

### Q5.

Transaction-এর ভিতরে Email পাঠানো উচিত?

**উত্তর:**

না। Transaction commit হওয়ার পরে Email/Celery task চালানো উচিত।

---

# Senior Checklist

যখনই নিচের কোনো feature বানাবে, নিজেকে জিজ্ঞেস করো:

* Checkout?
* Payment?
* Wallet?
* Bank Transfer?
* Inventory?
* Coupon?
* Seat Booking?

যদি **হ্যাঁ** হয়, তাহলে ভাবো:

* `transaction.atomic()` লাগবে?
* `select_for_update()` লাগবে?
* `F()` ব্যবহার করা যায়?
* External API কি transaction-এর বাইরে নেওয়া উচিত?

---

# 🔥 Real Production Challenge

ধরো তোমার কাছে এই API আছে:

```python
def buy_product(request, product_id):
    product = Product.objects.get(id=product_id)

    if product.stock > 0:
        product.stock -= 1
        product.save()

        Order.objects.create(product=product)
```

**প্রশ্ন:**

১০০ জন user একই সময়ে এই API call করলে কী কী bug হতে পারে?

ভাবো:

1. কোথায় Race Condition হবে?
2. কোথায় `transaction.atomic()` ব্যবহার করবে?
3. `select_for_update()` লাগবে?
4. `F()` ব্যবহার করলে design আরও ভালো হবে কি?

---

# 🎯 এখান পর্যন্ত তুমি যা শিখেছ

* ✅ Model Design
* ✅ Relationships
* ✅ Meta
* ✅ Managers
* ✅ Query Optimization
* ✅ Database Normalization
* ✅ Transactions
* ✅ Concurrency Control

এগুলো Production Backend-এর মূল ভিত্তি।

---

# পরের Lesson (Lesson 13)

**Production-Ready Django Model Patterns**

এখানে আমরা শিখব:

* UUID Primary Key
* Soft Delete Pattern
* Audit Fields (`created_by`, `updated_by`)
* TimeStampedModel
* Slug Pattern
* Status Pattern
* Choice vs Enum
* Production Base Models
* Enterprise-level Model Architecture

এটি এমন pattern যেগুলো বড় Django codebase-এ প্রায় প্রতিদিন দেখা যায়।
# Django Model Design Mastery

# Lesson 13: Production-Ready Django Model Patterns (Enterprise Thinking)

এটি এমন একটি lesson যেখানে আমরা **syntax নয়, architecture** শিখব।

এখন পর্যন্ত তুমি Model লিখতে শিখেছ।

এখন শিখবে—

> **Senior Developer একই ধরনের Model বারবার কীভাবে clean, reusable এবং scalable করে?**

---

# আজকের Goal

আজ শিখবে:

* UUID Primary Key
* TimeStampedModel
* Soft Delete Pattern
* Audit Fields
* Slug Pattern
* Status Pattern
* Choices vs TextChoices
* BaseModel Architecture
* Real Enterprise Structure

---

# Pattern 1: UUID Primary Key

## Beginner

```python
class Product(models.Model):
    title = models.CharField(max_length=200)
```

Database

```text
id = 1
id = 2
id = 3
```

---

Problem

API

```text
/products/1/
/products/2/
/products/3/
```

যে কেউ Guess করতে পারে।

---

## Production

```python
import uuid

class Product(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )
```

Database

```text
4c7316ef...

91ac781d...

df6e9d2b...
```

Guess করা কঠিন।

---

### কখন UUID ব্যবহার করবে?

✅ SaaS

✅ Public API

✅ Microservice

✅ Multi Database

---

### কখন Integer ID যথেষ্ট?

* Internal Admin System
* ছোট Project
* High-performance internal database যেখানে sequential ID-ই যথেষ্ট

---

## Senior Rule

Public-facing API হলে UUID খুব ভালো choice।

---

# Pattern 2: TimeStampedModel

Production Project-এ

৯০% Model-এ

```python
created_at

updated_at
```

থাকে।

---

```python
class TimeStampedModel(models.Model):

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        abstract = True
```

---

Usage

```python
class Product(TimeStampedModel):
    ...
```

---

# Pattern 3: Soft Delete

Hard Delete

```python
product.delete()
```

Data চলে গেল।

---

Production

```python
is_deleted = True
```

---

Example

```python
class SoftDeleteModel(models.Model):

    is_deleted = models.BooleanField(
        default=False
    )

    deleted_at = models.DateTimeField(
        null=True,
        blank=True
    )

    class Meta:
        abstract = True
```

---

Delete

```python
product.is_deleted = True
```

---

### কেন?

Customer ভুল করে Delete করলো।

Recover করা যাবে।

---

## Real Example

E-commerce

Product Delete?

আসলে

Hide।

---

# Pattern 4: Audit Fields

Business জানতে চায়

কে Create করেছে?

কে Update করেছে?

---

```python
created_by

updated_by
```

---

Example

```python
class AuditModel(models.Model):

    created_by = models.ForeignKey(
        User,
        ...
    )

    updated_by = models.ForeignKey(
        User,
        ...
    )

    class Meta:
        abstract = True
```

---

Admin Panel

```text
Created By

Updated By
```

---

Enterprise Project-এ খুব common।

---

# Pattern 5: Slug Pattern

URL

```text
/products/1/
```

Better

```text
/products/gaming-laptop/
```

---

Model

```python
slug = models.SlugField(
    unique=True
)
```

---

Save

```python
slugify(title)
```

---

### Senior Tip

Duplicate title?

Handle করতে হবে।

Example

```text
gaming-laptop

gaming-laptop-2

gaming-laptop-3
```

---

শুধু

```python
slug = slugify(title)
```

Production-ready নয়।

---

# Pattern 6: Status Pattern

Beginner

```python
status = models.CharField(
    max_length=50
)
```

Problem

```text
paid

Paid

PAYED

payment
```

সব Save হতে পারে।

---

Production

```python
from django.db import models

class OrderStatus(models.TextChoices):

    PENDING = "pending", "Pending"

    PAID = "paid", "Paid"

    CANCELLED = "cancelled", "Cancelled"
```

---

Model

```python
status = models.CharField(
    max_length=20,
    choices=OrderStatus.choices,
    default=OrderStatus.PENDING
)
```

---

Usage

```python
order.status == OrderStatus.PAID
```

Magic String নেই।

---

# Choice vs TextChoices

Old Style

```python
STATUS = (

("paid","Paid"),

...
)
```

---

New Style

```python
TextChoices
```

Readable

IDE Support

Autocomplete

Production Preferred।

---

# Pattern 7: Boolean Explosion

Beginner

```python
is_active

is_verified

is_paid

is_blocked

is_completed

is_refunded
```

অনেক Boolean।

---

Senior

Status Field।

```text
pending

approved

rejected
```

একটাই Source of Truth।

---

# Pattern 8: BaseModel Architecture

Enterprise Structure

```text
TimeStampedModel

↓

SoftDeleteModel

↓

AuditModel
```

↓

```text
Product

Order

Category

Review
```

---

Example

```python
class Product(

    TimeStampedModel,

    SoftDeleteModel

):
    ...
```

---

# Pattern 9: Image/File Pattern

Beginner

```python
image = models.ImageField()
```

---

E-commerce

Multiple Image

↓

Separate Model

```python
class ProductImage(models.Model):

    product = models.ForeignKey(...)

    image = models.ImageField(...)
```

---

১ Product

↓

১০ Image

---

# Pattern 10: Money Pattern

Wrong

```python
FloatField
```

---

Correct

```python
DecimalField(
    max_digits=10,
    decimal_places=2
)
```

Money-র জন্য কখনো `FloatField` ব্যবহার করবে না।

---

# Pattern 11: JSONField

যখন Structure বারবার বদলাবে।

Example

```python
extra_data = models.JSONField(
    default=dict
)
```

---

কিন্তু

সব Data JSON-এ রাখবে?

না।

Search করা কঠিন।

Index করা কঠিন।

Relationship করা যায় না।

---

# Real Production Product Model

```python
class Product(
    TimeStampedModel,
    SoftDeleteModel,
):

    seller = models.ForeignKey(...)

    title = models.CharField(...)

    slug = models.SlugField(...)

    status = models.CharField(
        choices=ProductStatus.choices,
        ...
    )

    price = models.DecimalField(...)

    stock = models.PositiveIntegerField(...)
```

Clean।

Readable।

Scalable।

---

# Beginner Mistakes

## Mistake 1

Money

↓

FloatField

❌

---

## Mistake 2

Status

↓

Random String

---

## Mistake 3

Everything Hard Delete

---

## Mistake 4

Slug Unique না।

---

## Mistake 5

১০টা Boolean।

---

## Mistake 6

Image

↓

Comma Separated URL

---

# Senior Production Checklist

প্রতিটি নতুন Model-এর জন্য নিজেকে জিজ্ঞেস করো:

### Public API?

↓

UUID লাগবে?

---

### History দরকার?

↓

Soft Delete?

---

### কে Create করেছে?

↓

Audit Field?

---

### Human URL?

↓

Slug?

---

### State আছে?

↓

TextChoices?

---

### Money?

↓

DecimalField?

---

### Multiple Images?

↓

Separate Model?

---

# Real Interview Questions

### Q1.

UUID কেন ব্যবহার করবে?

**উত্তর:**

Public-facing ID guess করা কঠিন হয় এবং distributed system-এ সুবিধা দেয়।

---

### Q2.

Money-এর জন্য FloatField কেন খারাপ?

**উত্তর:**

Floating-point precision error হতে পারে। তাই `DecimalField` ব্যবহার করা উচিত।

---

### Q3.

`TextChoices`-এর সুবিধা কী?

**উত্তর:**

Type-safe constant, autocomplete, কম typo, readable code।

---

### Q4.

Soft Delete কেন?

**উত্তর:**

Data recover করা যায় এবং historical data হারায় না।

---

# 🧠 Senior Thinking

একটি Model লেখার আগে ভাবো:

* Public API হবে?
* URL share হবে?
* Data recover করতে হবে?
* Status কত ধরনের?
* Audit দরকার?
* History রাখতে হবে?
* Money আছে?
* Multiple image/file লাগবে?

---

# 🔥 Final Enterprise Architecture

```
Base Models
│
├── TimeStampedModel
├── SoftDeleteModel
├── AuditModel
│
├── Product
├── Category
├── Order
├── OrderItem
├── Review
├── Payment
└── Inventory
```

এটাই অনেক Enterprise Django Project-এর foundation।

---

# 🎯 এখান পর্যন্ত তুমি যা শিখেছ

তুমি এখন জানো:

* ✅ Advanced Model Design
* ✅ Relationships
* ✅ Meta
* ✅ Managers
* ✅ QuerySets
* ✅ Model Methods
* ✅ Database Normalization
* ✅ Performance
* ✅ Transactions
* ✅ Enterprise Model Patterns

এগুলো একজন Mid-Level Django Developer-এর জন্য অত্যন্ত গুরুত্বপূর্ণ দক্ষতা।

---

# 📚 Lesson 14 (শেষের আগের Lesson)

**Production Database Migrations & Schema Evolution**

এখানে আমরা শিখব:

* Migration internals
* Safe migrations
* Data migration
* Large database migration strategy
* Renaming fields safely
* Zero-downtime migration
* Production deployment strategy

এটি এমন একটি বিষয় যা অনেক developer চাকরিতে গিয়ে প্রথমবারের মতো গুরুত্ব বুঝতে পারে।
# Django Model Design Mastery

# Lesson 14: Production Database Migrations & Schema Evolution

এটি এমন একটি বিষয় যেখানে **local project** আর **production project**-এর মধ্যে বিশাল পার্থক্য।

Beginner ভাবে:

> "Model change করলাম → `makemigrations` → `migrate` → Done."

Senior ভাবে:

> "Production database-এ ৫ কোটি row আছে। এই migration কি website বন্ধ করে দেবে?"

---

# আজকের Goal

আজ শিখবে:

* Migration আসলে কী?
* Migration File পড়া
* Migration Dependency
* Safe Migration Strategy
* Data Migration
* Renaming Field Safely
* Adding Non-null Field
* Zero Downtime Thinking
* Production Checklist

---

# Step 1: Migration আসলে কী?

ধরো Model

```python
class Product(models.Model):
    title = models.CharField(max_length=100)
```

তারপর নতুন Field যোগ করলে

```python
price = models.DecimalField(...)
```

`makemigrations` চালালে Django একটা Migration File তৈরি করে।

Example

```python
0002_add_price.py
```

এখানে লেখা থাকে

```python
operations = [
    migrations.AddField(...)
]
```

অর্থাৎ,

> **Migration = Database পরিবর্তনের ইতিহাস (history)।**

---

# Step 2: Migration Flow

```text
Model Change
      ↓
makemigrations
      ↓
Migration File
      ↓
migrate
      ↓
Database Change
```

---

# Step 3: Migration File পড়তে শেখো

Example

```python
operations = [
    migrations.CreateModel(
        name="Product",
        ...
    )
]
```

মানে

```text
নতুন Table তৈরি হবে
```

---

আরেকটা

```python
migrations.AddField(
    model_name="product",
    name="price",
)
```

মানে

```text
নতুন Column যোগ হবে
```

---

আরেকটা

```python
migrations.RemoveField(...)
```

মানে

```text
Column Delete হবে
```

---

# Senior Rule

**Migration File না পড়ে Production-এ migrate করবে না।**

---

# Step 4: Migration Dependency

Migration

```text
0001_initial

↓

0002_product

↓

0003_order
```

Django এগুলো sequence অনুযায়ী চালায়।

যদি

```text
0002
```

না থাকে,

```text
0003
```

চলবে না।

---

# Step 5: Adding a New Field

Beginner

```python
price = models.DecimalField(...)
```

Migration

↓

Error

কারণ পুরনো Row-তে Price নেই।

---

Solution 1

```python
price = models.DecimalField(
    ...,
    null=True
)
```

Migration

↓

Run

↓

Data Fill

↓

দ্বিতীয় Migration

```python
null=False
```

---

## Senior Strategy (Two-Step Migration)

Step 1

```python
price = models.DecimalField(
    null=True
)
```

↓

Deploy

↓

Backfill Data

↓

Step 2

```python
null=False
```

এটি Production-এর safest approach।

---

# Step 6: Renaming Field

Beginner

```python
title
```

↓

```python
name
```

ভাবলো Django বুঝবে।

সবসময় না।

অনেক সময় Django

```text
Remove Field

+

Add Field
```

করে।

Data হারাতে পারে।

---

Correct

```python
migrations.RenameField(...)
```

---

Senior Tip

Migration Prompt-এ যদি Django জিজ্ঞেস করে:

```text
Did you rename title to name?
```

ঠিক উত্তর দাও।

---

# Step 7: Removing Field

```python
price
```

Delete।

Production-এ?

না।

---

Safe Strategy

1. Code-এ ব্যবহার বন্ধ করো।
2. Deploy করো।
3. পরে Migration দিয়ে Remove করো।

---

# Step 8: Data Migration

শুধু Structure নয়,

Data-ও Change করা যায়।

Example

আগে

```text
status

1
2
3
```

এখন

```text
pending

paid

cancelled
```

Migration

```python
RunPython(...)
```

ব্যবহার করা হয়।

---

Example

```python
def convert_status(apps, schema_editor):

    Order = apps.get_model(
        "shop",
        "Order"
    )

    ...
```

এটি Data Migration।

---

# Step 9: Schema Migration vs Data Migration

Schema Migration

```text
Table

Column

Index
```

---

Data Migration

```text
Row-এর Data পরিবর্তন
```

---

# Step 10: Fake Migration

কখনো Database already updated থাকে।

কিন্তু Django জানে না।

তখন

```bash
python manage.py migrate --fake
```

---

⚠️

Production-এ খুব সতর্কভাবে ব্যবহার করবে।

---

# Step 11: Large Table Thinking

ধরো

Product

```text
5 কোটি Row
```

তুমি

```python
price = models.DecimalField(
    default=0
)
```

Add করলে?

অনেক Database-এ পুরো Table rewrite হতে পারে।

Website slow হয়ে যেতে পারে।

---

Senior Strategy

```text
NULL Field

↓

Backfill

↓

NOT NULL
```

---

# Step 12: Index Migration

Index

```python
models.Index(...)
```

Production-এ

Large Table-এ

Index Build করতে সময় লাগে।

তাই Migration-এর সময় Performance ভাবতে হবে।

---

# Step 13: Production Deployment

Bad

```text
Deploy

↓

Huge Migration

↓

Website Down
```

---

Better

```text
Deploy Code

↓

Run Safe Migration

↓

Deploy Next Step
```

---

# Step 14: Rollback Thinking

Migration Fail।

কি করবে?

Migration Reverse হতে পারবে?

সব Migration reversible না।

Example

```python
RemoveField
```

Data হারালে

Reverse করলেও Data ফিরে আসবে না।

---

# Step 15: Common Beginner Mistakes

## Mistake 1

Migration File Delete।

❌

---

## Mistake 2

Database Delete করে

আবার Migration।

Production-এ অসম্ভব।

---

## Mistake 3

Migration Conflict Ignore।

---

## Mistake 4

Migration Review না করা।

---

## Mistake 5

Direct NOT NULL Field Add।

---

## Mistake 6

Rename-এর বদলে Remove + Add।

---

# Real Production Example

ধরো

```python
title
```

কে

```python
name
```

করতে চাও।

Safe Way

```text
RenameField Migration

↓

Deploy

↓

Test

↓

Done
```

---

# Another Example

New Field

```python
sku
```

Required।

Production Strategy

```text
1. sku NULL

↓

2. Generate SKU

↓

3. NOT NULL

↓

4. Unique Constraint
```

এটাই Enterprise Migration Strategy।

---

# Interview Questions

### Q1.

Migration কী?

**উত্তর:**

Database schema পরিবর্তনের version-controlled history।

---

### Q2.

Schema Migration আর Data Migration-এর পার্থক্য?

**উত্তর:**

* Schema Migration table/column/index পরিবর্তন করে।
* Data Migration existing row-এর data পরিবর্তন করে।

---

### Q3.

Production-এ Non-null Field কীভাবে Add করবে?

**উত্তর:**

প্রথমে `null=True` দিয়ে add করব, data backfill করব, তারপর `null=False` migration দেব।

---

### Q4.

Migration File Delete করা উচিত?

**উত্তর:**

না। Migration project history-এর অংশ।

---

### Q5.

Rename Field-এর safest way কী?

**উত্তর:**

`RenameField` migration ব্যবহার করা।

---

# Senior Migration Checklist

প্রতিটি Migration-এর আগে নিজেকে জিজ্ঞেস করো:

* এটা কতগুলো row-তে প্রভাব ফেলবে?
* Table lock হবে?
* Data loss হতে পারে?
* Rollback সম্ভব?
* Migration review করেছি?
* Two-step migration দরকার?

---

# 🧠 Senior Thinking

Production Database-এ কাজ করার সময়:

**Code change-এর চেয়ে Database change বেশি risky।**

একটি ভুল Migration:

* Data Loss করতে পারে
* Website Down করতে পারে
* Rollback কঠিন করতে পারে

তাই Senior Developer সবসময় Migration আগে review করে।

---

# Homework

তোমার E-commerce Project-এ `Product` model-এ নতুন field যোগ করতে হবে:

```python
sku = models.CharField(max_length=50, unique=True)
```

কিন্তু Database-এ ইতিমধ্যে **২০ লাখ Product** আছে।

Design করো:

1. এক ধাপে migration করবে, নাকি একাধিক ধাপে?
2. `unique=True` কখন apply করবে?
3. Existing product-গুলোর SKU কীভাবে generate করবে?
4. কোন migration হবে Schema Migration, আর কোনটা Data Migration?

---

# 🎯 Model Design Mastery Status

এখন পর্যন্ত তুমি শিখেছ:

* ✅ Advanced Model Design
* ✅ Relationships
* ✅ Meta
* ✅ Managers & QuerySets
* ✅ Performance
* ✅ Transactions
* ✅ Enterprise Patterns
* ✅ Production Migrations

এখন তুমি শুধু Django Model লিখতে পারো না, **Production Database পরিবর্তনের চিন্তাও করতে পারো।**

---

# 🚀 Lesson 15 (Final & Most Advanced)

**Senior Django Model Architecture & Domain-Driven Design (DDD)**

এখানে আমরা শিখব:

* Fat Model vs Thin Model
* Service Layer Pattern
* Repository Pattern (কখন দরকার, কখন নয়)
* Domain Logic কোথায় থাকবে?
* Signals কখন ব্যবহার করবে?
* Large Django Project Structure
* Amazon/Stripe-স্টাইল Architecture
* Model Design Mistakes that Senior Developers Avoid

এটাই পুরো Django Model Mastery সিরিজের শেষ এবং সবচেয়ে advanced lesson।
# Django Model Design Mastery

# Lesson 15: Senior Django Model Architecture & Domain-Driven Design (DDD)

🎉 **অভিনন্দন!** এটি পুরো Django Model Mastery সিরজের শেষ lesson।

এখন পর্যন্ত তুমি Model-এর syntax শিখেছ, Query optimization শিখেছ, Transaction শিখেছ, Migration শিখেছ।

আজ শিখবে—

> **একটি বড় (100k+ lines) Django project কীভাবে organize করা হয়।**

এটাই Senior Developer-এর চিন্তাভাবনা।

---

# আজকের Goal

আজ শিখবে:

* Fat Model vs Thin Model
* Service Layer
* Domain Logic
* Signals
* Repository Pattern
* Large Project Structure
* DDD Thinking
* Production Mistakes

---

# Step 1: MVC vs Django Reality

অনেকে ভাবে

```text
View

↓

Serializer

↓

Model
```

কিন্তু Production Project-এ সাধারণত হয়

```text
API(View)

↓

Serializer

↓

Service Layer

↓

Model

↓

Database
```

Service Layer হচ্ছে Business Logic-এর Home।

---

# Step 2: Fat Model vs Thin Model

অনেক বছর আগে Django Community বলতো

```text
Fat Models

Thin Views
```

মানে

সব Logic Model-এ রাখো।

---

Example

```python
class Order(models.Model):

    def checkout(self):

        payment()

        email()

        inventory()

        invoice()

        sms()

        analytics()

        log()
```

Model বিশাল হয়ে গেল।

---

## Problem

Model এখন

* Payment জানে
* Email জানে
* SMS জানে
* Inventory জানে

Single Responsibility ভেঙে গেল।

---

# Modern Thinking

Model

↓

নিজের State জানবে।

Service

↓

Workflow Handle করবে।

---

# Step 3: Model-এর দায়িত্ব

Model জানবে

✅ নিজের Data

✅ নিজের Rule

✅ নিজের Validation

✅ নিজের Calculation

Example

```python
class Order(models.Model):

    @property
    def total(self):
        ...
```

---

আর

```python
def can_cancel(self):
    return self.status == "pending"
```

এগুলো Model-এর কাজ।

---

# Step 4: Service Layer

Checkout Example

```text
Customer

↓

Checkout

↓

Payment

↓

Inventory

↓

Order

↓

Invoice

↓

Email
```

এগুলো Model-এর কাজ?

না।

---

Example

```python
class CheckoutService:

    def checkout(self, user, cart):

        ...

        payment

        order

        email
```

সব Workflow এখানে।

---

# Step 5: Serializer-এর কাজ

অনেক Beginner

```python
create()
```

এর ভিতরে

২০০ লাইন।

---

Serializer-এর কাজ

* Validation
* Data Conversion

শুধু।

---

Business Logic?

না।

---

# Step 6: View-এর কাজ

View

```text
Request

↓

Permission

↓

Serializer

↓

Service

↓

Response
```

View-এর ভিতরে

Inventory Update?

না।

---

# Step 7: Signals

Signals খুব Powerful।

কিন্তু অনেক Abuse করে।

---

Good Example

User Create

↓

Profile Automatically Create

এখানে Signal ভালো।

---

Bad Example

Order Save

↓

Payment

↓

Inventory

↓

Email

↓

SMS

↓

Invoice

↓

Analytics

সব Signal।

Debug করা কঠিন।

---

## Senior Rule

Signal ব্যবহার করো যখন

**loosely coupled** event দরকার।

---

# Step 8: Repository Pattern

অনেক Java/.NET Developer Repository ব্যবহার করে।

Django-তে

QuerySet + Manager

আগেই Repository-এর অনেক সুবিধা দেয়।

Example

```python
Product.objects.active()
```

এটাই এক ধরনের repository-style abstraction।

---

Senior Rule

অপ্রয়োজনীয় Repository Layer যোগ করে code জটিল করো না।

---

# Step 9: Manager + Service

Model

```python
class Product(models.Model):
    ...
```

Manager

```python
Product.objects.active()
```

Service

```python
ProductService.publish()
```

এভাবে Responsibility ভাগ হয়।

---

# Step 10: Large Project Structure

একটি Enterprise Project

```text
shop/

    models/

        product.py
        order.py
        category.py
        inventory.py

    services/

        checkout.py
        payment.py
        inventory.py

    selectors/

        product.py
        order.py

    serializers/

    views/

    permissions/

    tasks/

    signals/

    tests/
```

Model file

১০০০ লাইনের হবে না।

---

# Step 11: Selectors (Read Layer)

অনেক বড় Project-এ

Read Query আলাদা রাখা হয়।

Example

```python
get_featured_products()
```

```python
get_best_sellers()
```

সব View-এ না লিখে Selector-এ রাখা হয়।

---

# Step 12: Domain Thinking

Business Requirement

> Customer refund চাইছে।

Beginner ভাবে

```text
Refund View
```

Senior ভাবে

```text
Refund Domain
```

তার Rules কী?

* Refund Time Limit
* Payment Status
* Admin Approval
* Wallet Update

এগুলো Domain Rule।

---

# Step 13: Rich Domain Model vs Anemic Model

## Anemic Model

Model

```python
class Product(models.Model):

    title

    price
```

সব Logic বাইরে।

---

## Rich Model

```python
class Product(models.Model):

    def discount_price(...)

    def can_publish(...)

    def is_available(...)
```

Model নিজের Behavior জানে।

---

কিন্তু Payment Logic Model-এ যাবে না।

---

# Step 14: Common Architecture Mistakes

### Mistake 1

View-এ ৫০০ লাইন।

---

### Mistake 2

Serializer-এ Business Logic।

---

### Mistake 3

সব Signal।

---

### Mistake 4

সব Model Method।

---

### Mistake 5

God Service

```text
ShopService
```

যা সব কাজ করে।

---

# Step 15: Production Flow

Customer Buy Product

```text
Request

↓

View

↓

Permission

↓

Serializer Validation

↓

CheckoutService

↓

Transaction

↓

Models

↓

Database

↓

Commit

↓

Celery Task

↓

Email

↓

Response
```

এটাই অনেক বড় Django Project-এর Flow।

---

# Decision Tree (সবচেয়ে গুরুত্বপূর্ণ)

## প্রশ্ন ১

এটা কি শুধু Data Validation?

↓

Serializer

---

## প্রশ্ন ২

এটা কি Object-এর নিজের Behavior?

↓

Model Method

---

## প্রশ্ন ৩

এটা কি Business Workflow?

↓

Service Layer

---

## প্রশ্ন ৪

এটা কি Read Query?

↓

Manager / Selector

---

## প্রশ্ন ৫

এটা কি Background কাজ?

↓

Celery Task

---

## প্রশ্ন ৬

এটা কি Cross-App Event?

↓

Signal (সীমিতভাবে)

---

# Real Example

### Requirement

Customer Checkout।

Beginner

```text
View

↓

Payment

↓

Inventory

↓

Invoice

↓

Email
```

সব View-তে।

---

Senior

```text
View

↓

CheckoutService

↓

transaction.atomic()

↓

Order

↓

Inventory

↓

Payment

↓

Commit

↓

Celery

↓

Email
```

Clean।

---

# Enterprise Checklist

প্রতিটি Feature-এর আগে নিজেকে জিজ্ঞেস করো:

* এটা Validation?
* এটা Business Rule?
* এটা Object Behavior?
* এটা Query?
* এটা Workflow?
* এটা Background Task?
* এটা External API?

তারপর ঠিক Layer বেছে নাও।

---

# Real Interview Questions

### Q1. সব Business Logic Model-এ রাখা উচিত?

**উত্তর:**

না। Object-specific behavior Model-এ থাকবে, কিন্তু multi-step workflow (checkout, payment, email, inventory) Service Layer-এ থাকবে।

---

### Q2. Signal কখন ব্যবহার করবে?

**উত্তর:**

যখন loosely coupled event handling দরকার, যেমন User তৈরি হলে Profile তৈরি করা।

---

### Q3. Serializer-এর মূল দায়িত্ব কী?

**উত্তর:**

Validation এবং data serialization/deserialization।

---

### Q4. View-এর মূল দায়িত্ব কী?

**উত্তর:**

HTTP request/response, permission, serializer call এবং service call orchestrate করা।

---

### Q5. Service Layer কেন দরকার?

**উত্তর:**

Business workflow আলাদা রাখতে, code reusable করতে এবং testing সহজ করতে।

---

# 🔥 Final Senior Architecture

```text
                Client
                  │
                  ▼
              Django View
                  │
                  ▼
             Serializer
                  │
                  ▼
            Service Layer
        ┌────────┼────────┐
        ▼        ▼        ▼
     Models   Managers  Selectors
        │
        ▼
     Database
        │
        ▼
 Transaction Commit
        │
        ▼
 Celery / Email / Notification
```

---

# 🎯 পুরো Django Model Mastery শেষ

তুমি এখন শিখেছ:

### Foundation

* ✅ Model Basics
* ✅ Fields
* ✅ Relationships
* ✅ Meta
* ✅ Validation

### Intermediate

* ✅ Managers
* ✅ QuerySets
* ✅ Model Methods
* ✅ Performance
* ✅ Normalization

### Advanced

* ✅ Transactions
* ✅ Concurrency
* ✅ Production Patterns
* ✅ Migrations
* ✅ Architecture

---

# এখন কী শিখবে?

এখন Model Design থেকে এগিয়ে **Production Django Backend Architecture**-এ যাও।

আমি এই ক্রমে এগোনোর পরামর্শ দিই:

1. **Authentication & Authorization (Production-Level)**
   JWT, Refresh Token, RBAC, Object-level permissions।

2. **Service Layer Implementation**
   বাস্তব CheckoutService, OrderService, PaymentService তৈরি।

3. **Caching**
   Redis, cache-aside pattern, cache invalidation।

4. **Background Jobs**
   Celery, Redis, scheduled tasks।

5. **API Security**
   Rate limiting, throttling, CORS, CSRF, secure headers।

6. **Testing**
   Unit test, API test, integration test, factory pattern।

7. **Deployment & Monitoring**
   Gunicorn, Nginx, Docker, logging, monitoring।

---

## তোমার জন্য একটি গুরুত্বপূর্ণ পর্যবেক্ষণ

তোমার আগের প্রশ্নগুলো (transactions, `annotate()`, serializers, viewsets, multi-vendor architecture) দেখে বোঝা যায় তুমি শুধু syntax নয়, **production-level reasoning** শেখার চেষ্টা করছ। এই mindset বজায় রাখলে Django-তে অনেক দ্রুত এগোতে পারবে।

**আমার পরামর্শ:** এখন আর নতুন model topic না শিখে, একটি **production-grade E-commerce backend** তৈরি করো এবং প্রতিটি lesson সেখানে প্রয়োগ করো। বাস্তব প্রয়োগ ছাড়া এই concepts পুরোপুরি আয়ত্ত করা কঠিন।
হ্যাঁ—**Self Relation** Django Model Design-এর খুব গুরুত্বপূর্ণ একটা concept। এটাকে ভালোভাবে বুঝলে hierarchical data design অনেক সহজ হয়ে যাবে।

# Lesson: Self Relation

## 1. Self Relation কী?

যখন একটি Model-এর `ForeignKey` **নিজের একই Model-কে reference করে**, তখন সেটাকে Self Relation বলে।

সহজভাবে:

```text
Employee
   │
   └── manager → Employee
```

অর্থাৎ `Employee`-এর manager-ও একজন `Employee`।

---

# 2. Django-তে কীভাবে লিখবে?

```python
class Employee(models.Model):
    name = models.CharField(max_length=100)

    manager = models.ForeignKey(
        "self",
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="employees"
    )
```

এখানে:

```python
manager = models.ForeignKey(
    "self",
    ...
)
```

এর অর্থ:

> `manager` field-এ অন্য কোনো Model নয়, একই `Employee` Model-এর object থাকবে।

---

# 3. Example

ধরো:

```text
Rahim
Karim
Hasan
```

Database concept:

```text
Rahim
manager = NULL

Karim
manager = Rahim

Hasan
manager = Rahim
```

অর্থাৎ:

```text
             Rahim
            /     \
        Karim     Hasan
```

---

# 4. Object দিয়ে দেখলে

```python
rahim = Employee.objects.create(
    name="Rahim"
)

karim = Employee.objects.create(
    name="Karim",
    manager=rahim
)

hasan = Employee.objects.create(
    name="Hasan",
    manager=rahim
)
```

এখন:

```python
karim.manager
```

Output:

```text
Rahim
```

আর:

```python
rahim.employees.all()
```

পাবে:

```text
Karim
Hasan
```

কারণ আমরা দিয়েছি:

```python
related_name="employees"
```

---

# 5. কেন Self Relation দরকার?

মূলত যখন **একই ধরনের Entity-এর মধ্যে hierarchical বা recursive relationship** থাকে।

এই প্রশ্নটা মনে রাখো:

> "একটা object কি একই ধরনের আরেকটা object-এর parent/manager/supervisor/reference হতে পারে?"

যদি উত্তর **হ্যাঁ** হয়, Self Relation লাগতে পারে।

---

# 6. সবচেয়ে common example: Employee → Manager

```text
CEO
│
├── CTO
│   ├── Senior Developer
│   └── Junior Developer
│
└── CFO
```

সবাই একই Entity:

```text
Employee
```

তাই:

```python
manager = models.ForeignKey(
    "self",
    ...
)
```

---

# 7. Category → Parent Category

এটা Django-তে Self Relation-এর আরেকটা অত্যন্ত common use case।

ধরো E-commerce Category:

```text
Electronics
│
├── Mobile
│   ├── Android
│   └── iPhone
│
└── Laptop
    ├── Gaming Laptop
    └── Business Laptop
```

এখানে সবগুলোই:

```text
Category
```

তাই:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)

    parent = models.ForeignKey(
        "self",
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name="children"
    )
```

---

# 8. Data কেমন হবে?

```python
electronics = Category.objects.create(
    name="Electronics"
)

mobile = Category.objects.create(
    name="Mobile",
    parent=electronics
)

android = Category.objects.create(
    name="Android",
    parent=mobile
)
```

Relationship:

```text
Electronics
    │
    └── Mobile
          │
          └── Android
```

---

# 9. Parent এবং Children

```python
mobile.parent
```

→ `Electronics`

আর:

```python
electronics.children.all()
```

→ `Mobile`

---

Android:

```python
android.parent
```

→ `Mobile`

---

# 10. কখন `CASCADE` ব্যবহার করবে?

এটা খুব গুরুত্বপূর্ণ।

```python
parent = models.ForeignKey(
    "self",
    on_delete=models.CASCADE
)
```

এর অর্থ:

Parent delete করলে children-ও delete হবে।

---

Example:

```text
Electronics
│
├── Mobile
└── Laptop
```

Electronics delete করলে:

```text
Mobile ❌
Laptop ❌
```

এটা সব business-এর জন্য safe নয়।

---

# 11. `SET_NULL` কখন ভালো?

Employee example:

```python
manager = models.ForeignKey(
    "self",
    on_delete=models.SET_NULL,
    null=True,
    blank=True
)
```

Manager delete করলে Employee থাকবে।

শুধু:

```text
manager = NULL
```

হবে।

এটাই সাধারণত employee hierarchy-তে বেশি sensible।

---

# 12. `PROTECT` কখন?

ধরো Category parent।

তুমি চাইছো:

> Parent Category-এর children থাকলে parent delete করা যাবে না।

তাহলে:

```python
parent = models.ForeignKey(
    "self",
    on_delete=models.PROTECT,
    null=True,
    blank=True
)
```

এখন:

```text
Electronics
│
└── Mobile
```

Electronics delete করতে গেলে error হবে।

---

# 13. Self Relation-এর 3টা গুরুত্বপূর্ণ Pattern

| Use Case                 | Field     |
| ------------------------ | --------- |
| Employee → Manager       | `manager` |
| Category → Parent        | `parent`  |
| Comment → Parent Comment | `parent`  |

---

# 14. Comment System

এটা খুব সুন্দর example।

Reddit/Facebook-style comments:

```text
Comment 1
│
├── Reply 1
│   └── Reply 2
│
└── Reply 3
```

সবই:

```text
Comment
```

তাই:

```python
class Comment(models.Model):
    text = models.TextField()

    parent = models.ForeignKey(
        "self",
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name="replies"
    )
```

---

Create:

```python
comment = Comment.objects.create(
    text="Main comment"
)

reply = Comment.objects.create(
    text="My reply",
    parent=comment
)
```

তারপর:

```python
comment.replies.all()
```

পাবে:

```text
My reply
```

---

# 15. Important: `null=True, blank=True` কেন?

Root object-এর কোনো parent নেই।

যেমন:

```text
Electronics
```

এর parent নেই।

তাই:

```python
parent = None
```

হতে দিতে হবে।

```python
null=True
blank=True
```

---

# 16. Self Relation কি সব hierarchy-এর জন্য?

না।

এখানে একটা Senior Thinking দরকার।

ধরো:

```text
Company
Employee
Department
```

Employee → Manager হলে Self Relation ভালো।

কিন্তু:

```text
Employee → Department
```

এখানে Self Relation নয়।

এটা:

```python
department = models.ForeignKey(
    Department,
    ...
)
```

কারণ দুইটি আলাদা Entity।

---

# 17. Self Relation বনাম Normal ForeignKey

### Normal

```text
Employee → Department
```

```python
department = models.ForeignKey(
    Department,
    ...
)
```

দুইটি আলাদা Model।

---

### Self

```text
Employee → Employee
```

```python
manager = models.ForeignKey(
    "self",
    ...
)
```

একই Model।

---

# 18. `related_name` কেন গুরুত্বপূর্ণ?

ধরো:

```python
manager = models.ForeignKey(
    "self",
    related_name="subordinates",
    ...
)
```

তাহলে:

```python
employee.subordinates.all()
```

দিয়ে তার অধীনে থাকা Employee পাবে।

আর:

```python
employee.manager
```

দিয়ে তার Manager পাবে।

তাই relationship দুই direction-এ সহজে navigate করা যায়।

---

# 19. আরেকটা Important Example: Organization

ধরো:

```text
CEO
│
├── Director
│   ├── Manager
│   │   ├── Employee
│   │   └── Employee
│   └── Manager
│
└── Director
```

এখানে:

```python
class Employee(models.Model):

    name = models.CharField(
        max_length=100
    )

    manager = models.ForeignKey(
        "self",
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="team_members"
    )
```

এটাই যথেষ্ট।

আলাদা:

```text
CEO Model
Director Model
Manager Model
Employee Model
```

বানানোর দরকার নেই।

কারণ সবাই একই Entity:

```text
Employee
```

---

# 20. Senior Thinking: কখন Self Relation করবে?

এই ৪টি প্রশ্ন করো:

### Question 1

দুই পাশের Entity কি একই ধরনের?

```text
Employee → Employee
```

হ্যাঁ।

---

### Question 2

একজন কি অন্যজনের parent/manager হতে পারে?

```text
Employee → Manager
```

হ্যাঁ।

---

### Question 3

Data কি tree/hierarchy তৈরি করছে?

```text
Parent
 └── Child
      └── Child
```

হ্যাঁ।

---

### Question 4

Depth কত হতে পারে?

```text
Category
 → Subcategory
 → Subcategory
 → ...
```

যদি unlimited/multiple levels হয়, Self Relation খুব natural solution।

---

# 21. কখন Self Relation করবে না?

যদি relationship আসলে আলাদা Entity-এর মধ্যে হয়।

উদাহরণ:

```text
Product → Category
```

এখানে:

```python
category = ForeignKey(Category)
```

Self Relation নয়।

---

# 22. Self Relation-এর একটা বড় Problem

Tree বড় হলে query complexity বাড়তে পারে।

ধরো:

```text
Electronics
 ↓
Mobile
 ↓
Android
 ↓
Samsung
 ↓
Galaxy
```

তুমি যদি পুরো tree একসাথে load করতে চাও, multiple query বা recursive processing লাগতে পারে।

তাই বড় hierarchical system হলে পরে তোমাকে জানতে হবে:

* Recursive Query
* Tree Traversal
* Caching
* `select_related()`
* `prefetch_related()`
* কখন Nested Set / MPTT দরকার

---

# 23. Self Relation + Index

ForeignKey সাধারণত database index তৈরি করে।

তাই:

```python
parent = models.ForeignKey(
    "self",
    ...
)
```

দিয়ে:

```python
Category.objects.filter(
    parent=electronics
)
```

efficiently করা যায়।

---

# 24. সবচেয়ে Important Mental Model

Self Relation দেখলেই ভাববে:

```text
Is this an Entity → Entity relationship
where both entities are the SAME type?
```

যদি:

```text
Employee → Employee
Category → Category
Comment → Comment
Folder → Folder
```

তাহলে Self Relation-এর কথা ভাববে।

---

# 25. Real Production Examples

Self Relation সাধারণত এখানে দেখতে পাবে:

```text
Employee
  └── Manager

Category
  └── Parent Category

Comment
  └── Parent Comment

Folder
  └── Parent Folder

Organization
  └── Parent Organization

Page
  └── Parent Page

Location
  └── Parent Location
```

---

# 🔥 একটি Production Example

E-commerce Category-এর জন্য আমি সাধারণত শুরু করতাম:

```python
class Category(models.Model):

    name = models.CharField(
        max_length=150
    )

    parent = models.ForeignKey(
        "self",
        on_delete=models.PROTECT,
        null=True,
        blank=True,
        related_name="children"
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["parent"]
            ),
        ]

    def __str__(self):
        return self.name
```

এখন hierarchy:

```text
Electronics
│
├── Mobile
│   ├── Android
│   └── iPhone
│
└── Laptop
    ├── Gaming
    └── Business
```

এটা খুব clean design।

---

# 🧠 Final Rule

Self Relation করার আগে এই sentence মনে রাখো:

> **"Same Model-এর object যদি অন্য একই Model-এর object-এর parent, manager, owner, predecessor, অথবা related node হয়—তখন Self Relation consider করব."**

আর সবচেয়ে common syntax:

```python
parent = models.ForeignKey(
    "self",
    on_delete=models.PROTECT,
    null=True,
    blank=True,
    related_name="children"
)
```

**পরবর্তী level:** Self Relation-এর পরে তোমার শেখা উচিত **`select_related()`/`prefetch_related()` দিয়ে self-relation query করা এবং DRF-তে nested parent → children API বানানো**। এটা করলে conceptটা পুরোপুরি practical হয়ে যাবে।


---
অবশ্যই। Self-relation comment system-এ **প্রথমে Django/DRF query design**, তারপর **React recursive rendering** বুঝলে পুরো বিষয়টা clear হয়ে যাবে।

আমরা এই structure ধরব:

```text
Post
 └── Comment
      ├── Comment
      │    └── Comment
      └── Comment
```

অর্থাৎ:

```text
Comment
   ↓
parent = another Comment
```

---

# 1. Django Model

ধরি Post-এর comment:

```python
class Comment(models.Model):
    post = models.ForeignKey(
        Post,
        on_delete=models.CASCADE,
        related_name="comments"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="comments"
    )

    text = models.TextField()

    parent = models.ForeignKey(
        "self",
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name="replies"
    )

    created_at = models.DateTimeField(auto_now_add=True)
```

এখানে সবচেয়ে গুরুত্বপূর্ণ:

```python
parent = models.ForeignKey(
    "self",
    ...
    related_name="replies"
)
```

---

# 2. Database-এ Data কেমন থাকবে?

ধরো:

```text
Comment 1
"আজকের post খুব ভালো"
parent = NULL
```

তার reply:

```text
Comment 2
"হ্যাঁ, আমিও পছন্দ করেছি"
parent = Comment 1
```

তারপর আরেকটি reply:

```text
Comment 3
"আমিও"
parent = Comment 2
```

Database:

| id | text                    | parent_id |
| -- | ----------------------- | --------: |
| 1  | আজকের post খুব ভালো     |      NULL |
| 2  | হ্যাঁ, আমিও পছন্দ করেছি |         1 |
| 3  | আমিও                    |         2 |

অর্থাৎ:

```text
1
└── 2
    └── 3
```

---

# 3. প্রথম প্রশ্ন: সব Comment কীভাবে Query করবো?

সব comment:

```python
comments = Comment.objects.all()
```

কিন্তু API-তে এটা সরাসরি দিলে:

```json
[
    {
        "id": 1,
        "text": "আজকের post খুব ভালো",
        "parent": null
    },
    {
        "id": 2,
        "text": "হ্যাঁ",
        "parent": 1
    }
]
```

React-এ hierarchy বানানোর কাজ frontend-কে করতে হবে।

আমরা বরং backend থেকেই tree structure তৈরি করতে পারি।

---

# 4. শুধু Root Comments Query করতে চাইলে

এটা খুব গুরুত্বপূর্ণ।

Root comment মানে যার:

```text
parent = NULL
```

তাই:

```python
comments = Comment.objects.filter(
    post_id=post_id,
    parent__isnull=True
)
```

এখন শুধু:

```text
Comment 1
Comment 4
Comment 8
```

এরকম top-level comments আসবে।

---

# 5. একটি Comment-এর Replies Query

ধরি:

```python
comment = Comment.objects.get(id=1)
```

তার replies:

```python
comment.replies.all()
```

কারণ আমরা দিয়েছিলাম:

```python
related_name="replies"
```

---

# 6. Nested Replies Query

ধরো:

```text
Comment 1
├── Comment 2
│   ├── Comment 3
│   └── Comment 5
└── Comment 4
```

এখন:

```python
comment.replies.all()
```

শুধু Comment 2 এবং 4 দেবে।

Comment 3 পেতে:

```python
comment.replies.all()[0].replies.all()
```

কিন্তু এটা production solution না।

কারণ depth কত হবে আমরা জানি না।

---

# 7. Recursive Thinking

Comment system-এর মূল idea:

```text
Comment
   ↓
replies
   ↓
replies
   ↓
replies
   ↓
...
```

তাই Serializer-এ recursive structure বানানো খুব useful।

---

# 8. DRF Serializer

প্রথমে:

```python
class CommentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Comment
        fields = [
            "id",
            "user",
            "text",
            "parent",
            "created_at",
        ]
```

এতে শুধু flat data আসবে।

---

# 9. Nested Replies Add করা

```python
class CommentSerializer(serializers.ModelSerializer):

    replies = serializers.SerializerMethodField()

    class Meta:
        model = Comment
        fields = [
            "id",
            "user",
            "text",
            "parent",
            "created_at",
            "replies",
        ]

    def get_replies(self, obj):
        return CommentSerializer(
            obj.replies.all(),
            many=True
        ).data
```

এখন response হবে:

```json
[
    {
        "id": 1,
        "text": "Main comment",
        "parent": null,
        "replies": [
            {
                "id": 2,
                "text": "Reply",
                "parent": 1,
                "replies": [
                    {
                        "id": 3,
                        "text": "Nested reply",
                        "parent": 2,
                        "replies": []
                    }
                ]
            }
        ]
    }
]
```

🔥 এটাই Recursive Serializer।

---

# 10. View-তে শুধু Root Comment Query

```python
class PostCommentListAPIView(APIView):

    def get(self, request, post_id):

        comments = Comment.objects.filter(
            post_id=post_id,
            parent__isnull=True
        )

        serializer = CommentSerializer(
            comments,
            many=True
        )

        return Response(serializer.data)
```

API:

```text
GET /api/posts/10/comments/
```

---

# 11. কিন্তু এখানে Performance Problem আছে ⚠️

এই serializer:

```python
obj.replies.all()
```

প্রতিটি comment-এর জন্য query করতে পারে।

ধরো:

```text
10 root comments
+
50 replies
```

অনেক query হতে পারে।

এটা N+1 problem-এর দিকে যেতে পারে।

---

# 12. Simple Solution: `prefetch_related`

প্রথম level:

```python
comments = Comment.objects.filter(
    post_id=post_id,
    parent__isnull=True
).prefetch_related(
    "replies"
)
```

এতে root comments-এর replies efficiently load হবে।

---

কিন্তু nested depth:

```text
root
 └── reply
      └── reply
           └── reply
```

হলে সমস্যা আবার আসতে পারে।

---

# 13. Real Production Strategy

এখানে তোমাকে একটা architectural decision নিতে হবে।

### Option A

Backend পুরো tree বানাবে।

```text
API
 ↓
Nested JSON
 ↓
React
```

### Option B

Backend flat comments পাঠাবে।

```text
API
 ↓
Flat JSON
 ↓
React tree বানাবে
```

Comment system-এর জন্য **দুই approach-ই valid**।

---

# 14. আমি কোনটা Recommend করবো?

সাধারণ blog/social media comment system হলে:

```text
Backend
↓
Nested JSON
↓
React recursive component
```

খুব clean।

কিন্তু অনেক বড় comment system হলে:

```text
Backend
↓
Paginated flat comments
↓
Frontend tree
```

অনেক সময় better।

কারণ ১০,০০০ nested comments এক response-এ পাঠানো উচিত না।

---

# 15. React Implementation

Backend response:

```json
[
    {
        "id": 1,
        "text": "Main comment",
        "replies": [
            {
                "id": 2,
                "text": "Reply",
                "replies": [
                    {
                        "id": 3,
                        "text": "Nested reply",
                        "replies": []
                    }
                ]
            }
        ]
    }
]
```

React-এ recursive component বানাবো।

---

# 16. `CommentItem.jsx`

```jsx
function CommentItem({ comment, onReply }) {
    return (
        <div className="comment">
            <div>
                <strong>
                    {comment.user}
                </strong>

                <p>
                    {comment.text}
                </p>

                <button
                    onClick={() => onReply(comment.id)}
                >
                    Reply
                </button>
            </div>

            <div className="replies">
                {comment.replies?.map((reply) => (
                    <CommentItem
                        key={reply.id}
                        comment={reply}
                        onReply={onReply}
                    />
                ))}
            </div>
        </div>
    );
}

export default CommentItem;
```

এখানে সবচেয়ে important অংশ:

```jsx
<CommentItem
    comment={reply}
/>
```

Component নিজেকেই আবার call করছে।

এটাই **React Recursive Component**।

---

# 17. Main Component

```jsx
import { useEffect, useState } from "react";
import CommentItem from "./CommentItem";

function Comments({ postId }) {

    const [comments, setComments] = useState([]);

    useEffect(() => {

        fetch(
            `/api/posts/${postId}/comments/`
        )
            .then(res => res.json())
            .then(data => {
                setComments(data);
            });

    }, [postId]);

    return (
        <div>

            {comments.map(comment => (
                <CommentItem
                    key={comment.id}
                    comment={comment}
                    onReply={(commentId) => {
                        console.log(
                            "Reply to:",
                            commentId
                        );
                    }}
                />
            ))}

        </div>
    );
}

export default Comments;
```

---

# 18. UI দেখতে কেমন হবে?

```text
Rahim
আজকের post খুব ভালো

    Reply

    Karim
    হ্যাঁ, আমিও পছন্দ করেছি

        Reply

        Hasan
        আমিও

            Reply

    Sakib
    ঠিক বলেছেন
```

React recursion নিজে নিজেই depth handle করবে।

---

# 19. Reply POST কীভাবে করবে?

ধরো user:

```text
Comment 1
```

এর Reply দিল:

```text
"হ্যাঁ, ঠিক বলেছেন"
```

Frontend থেকে:

```javascript
const data = {
    post: 10,
    text: "হ্যাঁ, ঠিক বলেছেন",
    parent: 1
};
```

POST:

```text
POST /api/comments/
```

Body:

```json
{
    "post": 10,
    "text": "হ্যাঁ, ঠিক বলেছেন",
    "parent": 1
}
```

Backend:

```python
Comment.objects.create(
    post_id=10,
    user=request.user,
    text="হ্যাঁ, ঠিক বলেছেন",
    parent_id=1
)
```

---

# 20. Root Comment Create

Root comment হলে:

```json
{
    "post": 10,
    "text": "Nice post",
    "parent": null
}
```

---

# 21. Reply Create

Reply হলে:

```json
{
    "post": 10,
    "text": "I agree",
    "parent": 1
}
```

এখানেই Self Relation-এর আসল power।

---

# 22. React-এ Reply Form

```jsx
function ReplyForm({ parentId, postId, onSuccess }) {

    const [text, setText] = useState("");

    const handleSubmit = async (e) => {

        e.preventDefault();

        const response = await fetch(
            "/api/comments/",
            {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    post: postId,
                    text: text,
                    parent: parentId,
                }),
            }
        );

        const data = await response.json();

        onSuccess(data);

        setText("");
    };

    return (
        <form onSubmit={handleSubmit}>

            <input
                value={text}
                onChange={(e) =>
                    setText(e.target.value)
                }
            />

            <button type="submit">
                Reply
            </button>

        </form>
    );
}
```

---

# 23. কিন্তু একটা Important Validation দরকার

User যেন অন্য Post-এর Comment-এর reply দিতে না পারে।

ধরো:

```text
Post A
 └── Comment 1
```

User যদি Post B-এর মধ্যে:

```json
{
    "parent": 1
}
```

দিয়ে request করে?

❌ Allow করা উচিত না।

Serializer-এ validate করো:

```python
def validate(self, attrs):

    parent = attrs.get("parent")
    post = attrs.get("post")

    if parent and parent.post_id != post.id:
        raise serializers.ValidationError(
            "Parent comment must belong to the same post."
        )

    return attrs
```

🔥 এটা production-level thinking।

---

# 24. আরেকটা Important Rule

নিজেকেই parent করা যাবে না।

```text
Comment 1
parent = Comment 1
```

❌

Validation:

```python
def validate_parent(self, value):

    if value and value.id == self.instance.id:
        raise serializers.ValidationError(
            "A comment cannot be its own parent."
        )

    return value
```

---

# 25. Infinite Loop Problem

আরেকটা বড় বিষয়:

```text
Comment 1
 ↓
Comment 2
 ↓
Comment 1
```

যদি circular relationship somehow তৈরি হয়, recursive serializer infinite loop করতে পারে।

তাই production system-এ validation দরকার যাতে cycle তৈরি না হয়।

---

# 26. Practical Architecture

আমি তোমাকে এই architecture recommend করবো:

```text
Django

Post
│
└── Comment
     │
     ├── parent
     └── replies
```

API:

```text
GET  /posts/{id}/comments/
POST /comments/
PATCH /comments/{id}/
DELETE /comments/{id}/
```

React:

```text
Comments
   │
   └── CommentItem
          │
          └── CommentItem
                 │
                 └── CommentItem
```

---

# 🧠 পুরো Concept এক লাইনে

Backend:

```text
parent = "self"
```

↓

Database:

```text
Comment → Comment → Comment
```

↓

DRF:

```text
Recursive Serializer
```

↓

API:

```text
Nested JSON
```

↓

React:

```text
Recursive Component
```

---

## সবচেয়ে গুরুত্বপূর্ণ ৫টা জিনিস মনে রাখো

```text
1. parent = ForeignKey("self")

2. root comment = parent__isnull=True

3. child comments = comment.replies.all()

4. DRF = recursive serializer

5. React = recursive Comment component
```

**Next practical step:** এই comment system-টা যদি তুমি বাস্তবে বানাতে চাও, পরের ধাপে আমি তোমাকে **Django Model + DRF Serializer + ViewSet + URLs + React + Axios + Reply + Delete + Pagination + `prefetch_related()`—একটা সম্পূর্ণ working comment/reply system** project-style code দিয়ে দেখাতে পারি।
অবশ্যই। এবার আমরা **একদম project-style complete Comment/Reply System** বানাবো।

Stack:

```text
Django
Django REST Framework
ViewSet
Router
Self ForeignKey
Recursive Serializer
prefetch_related()
Pagination
Reply
Delete
React
Axios
Recursive React Component
```

আমরা ধরে নিচ্ছি:

```text
Post
 └── Comments
      ├── Comment A
      │    ├── Reply A1
      │    │    └── Reply A1.1
      │    └── Reply A2
      │
      └── Comment B
```

---

# Part 1 — Django Project Structure

আমি এই structure recommend করছি:

```text
backend/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│   └── ...
│
├── posts/
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── pagination.py
│   └── ...
│
└── manage.py
```

Frontend:

```text
frontend/
│
├── src/
│   ├── api/
│   │   └── axios.js
│   │
│   ├── components/
│   │   ├── Comments.jsx
│   │   ├── CommentItem.jsx
│   │   └── ReplyForm.jsx
│   │
│   └── App.jsx
```

---

# Part 2 — Models

## Post

```python
# posts/models.py

from django.db import models
from django.conf import settings


class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()

    author = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="posts"
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    def __str__(self):
        return self.title
```

---

# Part 3 — Comment Model

এটাই আমাদের মূল Model।

```python
class Comment(models.Model):

    post = models.ForeignKey(
        Post,
        on_delete=models.CASCADE,
        related_name="comments"
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="comments"
    )

    text = models.TextField()

    parent = models.ForeignKey(
        "self",
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name="replies"
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        ordering = ["created_at"]

    def __str__(self):
        return f"{self.user} - {self.text[:30]}"
```

---

# Part 4 — এই Model কী তৈরি করলো?

Relationship:

```text
Post
 │
 └── comments
       │
       ├── Comment 1
       │      │
       │      ├── replies
       │      │
       │      └── Comment 2
       │
       └── Comment 3
```

আর:

```python
parent = models.ForeignKey(
    "self"
)
```

মানে:

```text
Comment → Comment
```

---

# Part 5 — Migration

```bash
python manage.py makemigrations
python manage.py migrate
```

---

# Part 6 — Serializer Design

এখানে একটু careful হতে হবে।

আমরা চাই:

```json
{
    "id": 1,
    "text": "Main comment",
    "user": {
        "id": 5,
        "username": "atiar"
    },
    "replies": [
        {
            "id": 2,
            "text": "Reply",
            "replies": []
        }
    ]
}
```

---

# Part 7 — User Serializer

```python
# posts/serializers.py

from rest_framework import serializers
from .models import Comment


class CommentUserSerializer(serializers.Serializer):

    id = serializers.IntegerField()

    username = serializers.CharField()
```

---

# Part 8 — Recursive Comment Serializer

```python
class CommentSerializer(
    serializers.ModelSerializer
):

    user = CommentUserSerializer(
        read_only=True
    )

    replies = serializers.SerializerMethodField()

    class Meta:

        model = Comment

        fields = [
            "id",
            "text",
            "user",
            "parent",
            "created_at",
            "updated_at",
            "replies",
        ]

        read_only_fields = [
            "id",
            "user",
            "created_at",
            "updated_at",
            "replies",
        ]

    def get_replies(self, obj):

        queryset = obj.replies.all()

        return CommentSerializer(
            queryset,
            many=True,
            context=self.context
        ).data
```

---

# ⚠️ কিন্তু এখানে একটা সমস্যা

এভাবে:

```python
obj.replies.all()
```

প্রতিটি comment-এর জন্য database query হতে পারে।

ধরো:

```text
10 root comments
50 replies
```

অনেক Query হতে পারে।

এটাই N+1 problem।

---

# Part 9 — `prefetch_related()` ব্যবহার

এখানে আমরা একটু advanced solution ব্যবহার করব।

প্রথম level:

```python
queryset = Comment.objects.filter(
    post_id=post_id,
    parent__isnull=True
).prefetch_related(
    "replies"
)
```

এতে root comments এবং তাদের immediate replies efficiently load হবে।

কিন্তু nested reply unlimited হলে আরও query লাগতে পারে।

তাই practical system-এ আমরা **recursive prefetch** ব্যবহার করতে পারি।

---

# Part 10 — Recursive Prefetch Helper

```python
# posts/views.py

from django.db.models import Prefetch
from .models import Comment


def build_comment_prefetch(depth=3):

    if depth <= 0:
        return []

    return [
        Prefetch(
            "replies",
            queryset=Comment.objects.select_related(
                "user"
            ).prefetch_related(
                *build_comment_prefetch(depth - 1)
            )
        )
    ]
```

এখানে:

```text
depth = 3
```

মানে আমরা ৩ level পর্যন্ত prefetch করছি।

---

# কেন Depth দরকার?

কারণ theoretically comment হতে পারে:

```text
Comment
 ↓
Reply
 ↓
Reply
 ↓
Reply
 ↓
Reply
 ↓
Reply
 ↓
...
```

Unlimited recursive database loading করা dangerous।

তাই production system-এ depth limit রাখা ভালো।

---

# Part 11 — Pagination

Root comments paginate করব।

```python
# posts/pagination.py

from rest_framework.pagination import PageNumberPagination


class CommentPagination(
    PageNumberPagination
):

    page_size = 10

    page_size_query_param = "page_size"

    max_page_size = 50
```

এখন:

```text
?page=1
```

অথবা

```text
?page=2&page_size=20
```

---

# Part 12 — ViewSet

এখন মূল অংশ।

```python
# posts/views.py

from django.db import transaction

from rest_framework import status, viewsets
from rest_framework.permissions import IsAuthenticatedOrReadOnly
from rest_framework.response import Response

from .models import Comment
from .serializers import CommentSerializer
from .pagination import CommentPagination
```

---

# Part 13 — Comment ViewSet

```python
class CommentViewSet(viewsets.ModelViewSet):

    serializer_class = CommentSerializer

    permission_classes = [
        IsAuthenticatedOrReadOnly
    ]

    pagination_class = CommentPagination
```

---

# Part 14 — Queryset

আমাদের Post ID frontend থেকে আসবে।

ধরো:

```text
GET /api/posts/10/comments/
```

আমাদের root comments লাগবে।

```python
def get_queryset(self):

    post_id = self.kwargs.get(
        "post_pk"
    )

    return (
        Comment.objects
        .filter(
            post_id=post_id,
            parent__isnull=True
        )
        .select_related("user")
        .prefetch_related(
            *build_comment_prefetch(depth=3)
        )
    )
```

---

# Part 15 — গুরুত্বপূর্ণ বিষয়

আমরা এখানে:

```python
parent__isnull=True
```

ব্যবহার করছি।

কারণ API প্রথমে শুধু root comments return করবে।

তারপর:

```text
root
 ↓
replies
 ↓
nested replies
```

serializer tree তৈরি করবে।

---

# Part 16 — Create Comment / Reply

এখন POST।

```python
def perform_create(self, serializer):

    post_id = self.kwargs.get(
        "post_pk"
    )

    serializer.save(
        user=self.request.user,
        post_id=post_id
    )
```

---

# কিন্তু Validation কোথায়?

Serializer-এ।

---

# Part 17 — Validate Parent

```python
class CommentSerializer(
    serializers.ModelSerializer
):

    user = CommentUserSerializer(
        read_only=True
    )

    replies = serializers.SerializerMethodField()

    class Meta:

        model = Comment

        fields = [
            "id",
            "text",
            "user",
            "parent",
            "created_at",
            "updated_at",
            "replies",
        ]

        read_only_fields = [
            "id",
            "user",
            "created_at",
            "updated_at",
            "replies",
        ]

    def validate(self, attrs):

        parent = attrs.get("parent")

        if parent:

            post_id = self.context[
                "view"
            ].kwargs.get("post_pk")

            if parent.post_id != int(post_id):

                raise serializers.ValidationError({
                    "parent": (
                        "Parent comment must "
                        "belong to the same post."
                    )
                })

        return attrs

    def get_replies(self, obj):

        return CommentSerializer(
            obj.replies.all(),
            many=True,
            context=self.context
        ).data
```

---

# এখন API Create

## Root Comment

```http
POST /api/posts/10/comments/
```

Body:

```json
{
    "text": "Great post!",
    "parent": null
}
```

---

## Reply

```http
POST /api/posts/10/comments/
```

Body:

```json
{
    "text": "I agree!",
    "parent": 15
}
```

এখানে:

```text
parent = 15
```

মানে Comment #15-এর reply।

---

# Part 18 — Delete

`ModelViewSet` already gives:

```http
DELETE /api/comments/15/
```

কিন্তু আমরা চাই:

> শুধু নিজের comment delete করতে পারবে।

---

# Part 19 — Delete Permission

```python
def perform_destroy(self, instance):

    if instance.user != self.request.user:

        from rest_framework.exceptions import PermissionDenied

        raise PermissionDenied(
            "You can delete only your own comment."
        )

    instance.delete()
```

---

# Complete ViewSet

সব একসাথে:

```python
class CommentViewSet(viewsets.ModelViewSet):

    serializer_class = CommentSerializer

    permission_classes = [
        IsAuthenticatedOrReadOnly
    ]

    pagination_class = CommentPagination

    def get_queryset(self):

        post_id = self.kwargs.get(
            "post_pk"
        )

        return (
            Comment.objects
            .filter(
                post_id=post_id,
                parent__isnull=True
            )
            .select_related("user")
            .prefetch_related(
                *build_comment_prefetch(
                    depth=3
                )
            )
        )

    def perform_create(self, serializer):

        post_id = self.kwargs.get(
            "post_pk"
        )

        serializer.save(
            user=self.request.user,
            post_id=post_id
        )

    def perform_destroy(self, instance):

        if instance.user != self.request.user:

            from rest_framework.exceptions import PermissionDenied

            raise PermissionDenied(
                "You can delete only your own comment."
            )

        instance.delete()
```

---

# Part 20 — URLs

আমরা Nested URL চাই:

```text
/posts/{post_id}/comments/
```

এজন্য `drf-nested-routers` ব্যবহার করতে পারো।

Install:

```bash
pip install drf-nested-routers
```

---

# Main URLs

```python
# config/urls.py

from django.urls import path, include

urlpatterns = [

    path(
        "api/",
        include("posts.urls")
    ),

]
```

---

# posts/urls.py

```python
from rest_framework.routers import DefaultRouter
from rest_framework_nested.routers import NestedDefaultRouter

from .views import CommentViewSet
from .views import PostViewSet
```

ধরি PostViewSet আছে:

```python
router = DefaultRouter()

router.register(
    "posts",
    PostViewSet,
    basename="post"
)
```

Nested router:

```python
posts_router = NestedDefaultRouter(
    router,
    "posts",
    lookup="post"
)

posts_router.register(
    "comments",
    CommentViewSet,
    basename="post-comments"
)
```

URLs:

```python
urlpatterns = [
    *router.urls,
    *posts_router.urls,
]
```

---

# Result

GET:

```text
GET /api/posts/10/comments/
```

POST:

```text
POST /api/posts/10/comments/
```

DELETE:

```text
DELETE /api/posts/10/comments/15/
```

PATCH:

```text
PATCH /api/posts/10/comments/15/
```

---

# Part 21 — Pagination Response

GET:

```text
/api/posts/10/comments/?page=1
```

Response:

```json
{
    "count": 25,
    "next": "...page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "text": "Great post",
            "user": {
                "id": 2,
                "username": "atiar"
            },
            "parent": null,
            "replies": [
                {
                    "id": 2,
                    "text": "I agree",
                    "user": {
                        "id": 3,
                        "username": "rahim"
                    },
                    "parent": 1,
                    "replies": []
                }
            ]
        }
    ]
}
```

---

# Part 22 — React Setup

Install Axios:

```bash
npm install axios
```

---

# Part 23 — Axios Instance

```javascript
// src/api/axios.js

import axios from "axios";

const api = axios.create({
    baseURL: "http://localhost:8000/api",
});

export default api;
```

Production-এ:

```javascript
const api = axios.create({
    baseURL: import.meta.env.VITE_API_URL,
});
```

---

# Part 24 — Comments Component

```jsx
// Comments.jsx

import { useEffect, useState } from "react";
import api from "../api/axios";
import CommentItem from "./CommentItem";

function Comments({ postId }) {

    const [comments, setComments] = useState([]);

    const [loading, setLoading] = useState(true);

    const [error, setError] = useState(null);

    const fetchComments = async () => {

        try {

            setLoading(true);

            const response = await api.get(
                `/posts/${postId}/comments/`
            );

            setComments(
                response.data.results
            );

        } catch (error) {

            setError(
                "Failed to load comments"
            );

        } finally {

            setLoading(false);
        }
    };

    useEffect(() => {

        fetchComments();

    }, [postId]);

    if (loading) {
        return <p>Loading comments...</p>;
    }

    if (error) {
        return <p>{error}</p>;
    }

    return (
        <div>

            <h2>
                Comments
            </h2>

            {comments.map(comment => (

                <CommentItem
                    key={comment.id}
                    comment={comment}
                    postId={postId}
                    onRefresh={fetchComments}
                />

            ))}

        </div>
    );
}

export default Comments;
```

---

# Part 25 — CommentItem

এখানেই React recursion।

```jsx
// CommentItem.jsx

import { useState } from "react";
import api from "../api/axios";
import ReplyForm from "./ReplyForm";

function CommentItem({
    comment,
    postId,
    onRefresh
}) {

    const [showReply, setShowReply] =
        useState(false);

    const [deleting, setDeleting] =
        useState(false);

    const handleDelete = async () => {

        try {

            setDeleting(true);

            await api.delete(
                `/posts/${postId}/comments/${comment.id}/`
            );

            onRefresh();

        } catch (error) {

            console.error(error);

        } finally {

            setDeleting(false);
        }
    };

    return (
        <div
            style={{
                marginLeft: "20px",
                marginTop: "15px"
            }}
        >

            <div>

                <strong>
                    {comment.user.username}
                </strong>

                <p>
                    {comment.text}
                </p>

                <small>
                    {new Date(
                        comment.created_at
                    ).toLocaleString()}
                </small>

            </div>

            <button
                onClick={() =>
                    setShowReply(!showReply)
                }
            >
                Reply
            </button>

            <button
                onClick={handleDelete}
                disabled={deleting}
            >
                {deleting
                    ? "Deleting..."
                    : "Delete"}
            </button>

            {showReply && (

                <ReplyForm
                    postId={postId}
                    parentId={comment.id}
                    onSuccess={() => {
                        setShowReply(false);
                        onRefresh();
                    }}
                />

            )}

            <div>

                {comment.replies?.map(
                    reply => (

                        <CommentItem
                            key={reply.id}
                            comment={reply}
                            postId={postId}
                            onRefresh={onRefresh}
                        />

                    )
                )}

            </div>

        </div>
    );
}

export default CommentItem;
```

---

# 🔥 এই অংশটা খুব ভালোভাবে বুঝো

```jsx
{comment.replies?.map(reply => (

    <CommentItem
        comment={reply}
    />

))}
```

`CommentItem` আবার নিজেকেই render করছে।

তাই:

```text
CommentItem
   ↓
CommentItem
   ↓
CommentItem
   ↓
CommentItem
```

যত nested reply থাকবে তত depth render হবে।

এটাই **Recursive React Component**।

---

# Part 26 — ReplyForm

```jsx
// ReplyForm.jsx

import { useState } from "react";
import api from "../api/axios";

function ReplyForm({
    postId,
    parentId,
    onSuccess
}) {

    const [text, setText] =
        useState("");

    const [loading, setLoading] =
        useState(false);

    const handleSubmit = async (e) => {

        e.preventDefault();

        if (!text.trim()) {
            return;
        }

        try {

            setLoading(true);

            await api.post(
                `/posts/${postId}/comments/`,
                {
                    text: text,
                    parent: parentId
                }
            );

            setText("");

            onSuccess();

        } catch (error) {

            console.error(error);

        } finally {

            setLoading(false);
        }
    };

    return (
        <form
            onSubmit={handleSubmit}
            style={{
                marginTop: "10px"
            }}
        >

            <input
                type="text"
                value={text}
                onChange={(e) =>
                    setText(e.target.value)
                }
                placeholder="Write a reply..."
            />

            <button
                type="submit"
                disabled={loading}
            >
                {loading
                    ? "Posting..."
                    : "Reply"}
            </button>

        </form>
    );
}

export default ReplyForm;
```

---

# Part 27 — Root Comment Form

Reply-এর জন্য `parentId` আছে।

Root comment-এর জন্য:

```text
parent = null
```

তাই:

```jsx
function CommentForm({
    postId,
    onSuccess
}) {

    const [text, setText] =
        useState("");

    const handleSubmit = async (e) => {

        e.preventDefault();

        await api.post(
            `/posts/${postId}/comments/`,
            {
                text,
                parent: null
            }
        );

        setText("");

        onSuccess();
    };

    return (
        <form onSubmit={handleSubmit}>

            <input
                value={text}
                onChange={(e) =>
                    setText(e.target.value)
                }
            />

            <button>
                Comment
            </button>

        </form>
    );
}
```

---

# Part 28 — App

```jsx
import Comments from "./components/Comments";

function App() {

    const postId = 10;

    return (
        <div>

            <h1>
                My Blog Post
            </h1>

            <Comments
                postId={postId}
            />

        </div>
    );
}

export default App;
```

---

# Part 29 — Complete Flow

এখন পুরো system:

```text
                   React
                     │
                     │ GET
                     ▼
       /posts/10/comments/
                     │
                     ▼
               Django ViewSet
                     │
                     ▼
              get_queryset()
                     │
                     ▼
         parent IS NULL
                     │
                     ▼
          select_related(user)
                     │
                     ▼
          prefetch_related()
                     │
                     ▼
              Serializer
                     │
                     ▼
             Nested JSON
                     │
                     ▼
                  React
                     │
                     ▼
             CommentItem
                     │
                     ▼
              replies.map()
                     │
                     ▼
             CommentItem
```

---

# Part 30 — Reply Flow

User clicks:

```text
Reply
```

↓

React:

```javascript
parent: comment.id
```

↓

POST:

```text
POST /api/posts/10/comments/
```

Body:

```json
{
    "text": "Nice!",
    "parent": 15
}
```

↓

Django:

```python
Comment.objects.create(
    post=post,
    user=request.user,
    text="Nice!",
    parent_id=15
)
```

↓

Database:

```text
Comment 15
    │
    └── Comment 20
```

↓

React refresh

↓

Nested comment appears।

---

# Part 31 — Delete Flow

User:

```text
Delete
```

↓

```text
DELETE /api/posts/10/comments/20/
```

↓

ViewSet:

```python
perform_destroy()
```

↓

Check:

```python
instance.user == request.user
```

↓

True

↓

```python
instance.delete()
```

---

# ⚠️ একটা Important Design Issue

আমাদের Model:

```python
parent = models.ForeignKey(
    "self",
    on_delete=models.CASCADE
)
```

মানে:

```text
Comment A
 ├── Reply B
 │    └── Reply C
```

A delete করলে:

```text
A ❌
B ❌
C ❌
```

কারণ `CASCADE`।

---

# Alternative: Soft Delete

Real social media/comment system-এ তুমি অনেক সময়:

```python
is_deleted = models.BooleanField(
    default=False
)
```

রাখতে পারো।

তাহলে:

```text
Comment deleted
```

কিন্তু reply structure রাখা যাবে।

UI:

```text
[This comment has been deleted]
```

এটা অনেক ক্ষেত্রে better UX।

---

# Part 32 — Pagination-এর Important Limitation

আমরা root comments paginate করছি:

```text
Page 1

Comment A
Comment B
Comment C
```

কিন্তু প্রতিটি root comment-এর সব replies একসাথে আসছে।

ধরো:

```text
Comment A
 ├── 1000 replies
 ├── 1001 replies
 └── ...
```

এখানে root pagination করলেও response বিশাল হতে পারে।

### Production solution

Replies-ও আলাদা pagination endpoint দিতে পারো:

```text
GET /api/comments/15/replies/
```

তখন:

```text
Comment
   ↓
View Replies
   ↓
GET /comments/15/replies/?page=2
```

এটি large-scale application-এর জন্য অনেক ভালো।

---

# Part 33 — Production API Design

ছোট/মাঝারি project:

```text
GET  /posts/{post_id}/comments/
POST /posts/{post_id}/comments/
DELETE /posts/{post_id}/comments/{id}/
```

বড় project:

```text
GET  /posts/{post_id}/comments/

GET  /comments/{comment_id}/replies/

POST /posts/{post_id}/comments/

PATCH /comments/{comment_id}/

DELETE /comments/{comment_id}/
```

---

# Part 34 — `prefetch_related()` কীভাবে কাজ করছে?

আমাদের:

```python
.select_related("user")
```

কারণ:

```text
Comment → User
```

এটি ForeignKey।

আর:

```python
.prefetch_related(...)
```

কারণ:

```text
Comment → Replies
```

এটি reverse ForeignKey।

অর্থাৎ:

```text
Comment
   │
   ├── user
   │     ↓
   │  select_related
   │
   └── replies
         ↓
      prefetch_related
```

---

# 🔥 Golden Rule

Self relation-এর ক্ষেত্রে:

```python
parent = ForeignKey("self")
```

কিন্তু query করার সময় relationship direction বুঝতে হবে।

### Parent থেকে children:

```python
comment.replies.all()
```

### Child থেকে parent:

```python
comment.parent
```

---

# Part 35 — Production Optimization

আমাদের Query:

```python
Comment.objects.filter(
    post_id=post_id,
    parent__isnull=True
).select_related(
    "user"
).prefetch_related(
    ...
)
```

এখানে আমরা তিনটি optimization করেছি:

```text
1. Filter
2. select_related
3. prefetch_related
```

---

# Part 36 — আরেকটি Optimization

Serializer-এ:

```python
obj.replies.all()
```

ব্যবহার করছি।

Prefetch করা থাকলে Django cached result ব্যবহার করতে পারে।

তাই:

```python
obj.replies.all()
```

সবসময় নতুন query করবে এমন নয়—যদি ওই relation আগে properly prefetched থাকে।

---

# Part 37 — Final Folder Structure

```text
backend/
│
├── config/
│   ├── settings.py
│   ├── urls.py
│
├── posts/
│   ├── __init__.py
│   ├── models.py
│   ├── serializers.py
│   ├── views.py
│   ├── urls.py
│   ├── pagination.py
│   └── migrations/
│
└── manage.py
```

Frontend:

```text
frontend/
│
├── src/
│   │
│   ├── api/
│   │   └── axios.js
│   │
│   ├── components/
│   │   ├── Comments.jsx
│   │   ├── CommentItem.jsx
│   │   ├── CommentForm.jsx
│   │   └── ReplyForm.jsx
│   │
│   ├── App.jsx
│   └── main.jsx
│
└── package.json
```

---

# 🧠 এখন সবচেয়ে গুরুত্বপূর্ণ Architecture

তুমি পুরো system-টা এইভাবে মনে রাখবে:

```text
                    POST
                     │
                     ▼
              ┌─────────────┐
              │   Comment   │
              └─────────────┘
                     │
              parent = self
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
     Parent Comment          Reply
          │                     │
          └──────────┬──────────┘
                     ▼
                  Database
                     │
                     ▼
               ViewSet Query
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
    select_related        prefetch_related
       User                  Replies
          │                     │
          └──────────┬──────────┘
                     ▼
             Recursive JSON
                     │
                     ▼
                  React
                     │
                     ▼
             CommentItem
                     │
                     ▼
              replies.map()
                     │
                     ▼
             CommentItem
```

---

# 🎯 এখন তোমার Practice Task

এই system-এ আরও ৫টা feature নিজে implement করো:

### Level 1

**Edit Comment**

```text
PATCH /comments/{id}/
```

শুধু owner edit করতে পারবে।

### Level 2

**Like Comment**

```text
Comment
 └── CommentLike
```

### Level 3

**Soft Delete**

```text
is_deleted
deleted_at
```

### Level 4

**Reply Pagination**

```text
GET /comments/{id}/replies/?page=2
```

### Level 5 — Advanced

**Comment tree-এর জন্য flat API + React-side tree building** implement করো:

```json
[
  {"id": 1, "parent": null},
  {"id": 2, "parent": 1},
  {"id": 3, "parent": 1},
  {"id": 4, "parent": 2}
]
```

React-এ convert করবে:

```text
1
├── 2
│   └── 4
└── 3
```

এটা করলে তুমি শুধু Self Relation জানবে না—**recursive data modeling + API design + database optimization + recursive React rendering**—চারটিই practically বুঝে যাবে।
হ্যাঁ, **Self Relation না করেও comment system বানানো যায়**। কিন্তু তখন তোমার requirement-এর ওপর depend করবে।

### যদি শুধু simple comment হয়

যেমন:

```text
Post
 ├── Comment 1
 ├── Comment 2
 └── Comment 3
```

তাহলে Self Relation দরকার নেই।

```python
class Comment(models.Model):
    post = models.ForeignKey(
        Post,
        on_delete=models.CASCADE,
        related_name="comments"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    text = models.TextField()
```

Query:

```python
post.comments.all()
```

এটাই যথেষ্ট।

---

### কিন্তু যদি Reply করতে চাও

যেমন:

```text
Comment 1
 ├── Reply 1
 ├── Reply 2
 │    └── Reply 2.1
 └── Reply 3
```

তখন Self Relation সবচেয়ে natural:

```python
parent = models.ForeignKey(
    "self",
    null=True,
    blank=True,
    on_delete=models.CASCADE,
    related_name="replies"
)
```

কারণ database-কে বলতে হবে:

> "এই Comment-টি কোন Comment-এর reply?"

---

## Self Relation না করলে কী হবে?

তুমি আলাদা `Reply` model বানাতে পারো:

```python
class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    text = models.TextField()


class Reply(models.Model):
    comment = models.ForeignKey(
        Comment,
        on_delete=models.CASCADE,
        related_name="replies"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE
    )

    text = models.TextField()
```

এতে:

```text
Comment
   │
   └── Reply
```

করা যাবে।

কিন্তু সমস্যা হলো:

```text
Comment
 └── Reply
      └── Reply
           └── Reply
```

এই unlimited nesting আর naturally করা যাবে না, কারণ `Reply` নিজেকে reference করছে না।

---

# তাই Decision Rule

### শুধু comment:

```text
Post → Comment
```

**Self relation ❌**

### Comment + one-level reply:

```text
Post
 └── Comment
      └── Reply
```

Self relation **না করেও** করা যায়।

### Comment + unlimited/multiple-level reply:

```text
Comment
 └── Reply
      └── Reply
           └── Reply
```

**Self relation ✅ strongly recommended**

---

### সহজ ভাষায়

**Self relation কোনো বাধ্যতামূলক জিনিস না।**

এটা দরকার হয় যখন:

> **একই ধরনের object-এর মধ্যে relationship তৈরি করতে হয়।**

Comment system-এ যদি `Comment → Comment` relationship দরকার হয়, তখন Self Relation।

আর যদি তোমার requirement শুধু:

```text
Post
 ↓
Comment
 ↓
Reply
```

তাহলে `Comment` এবং `Reply` আলাদা model করেও সুন্দরভাবে করা যায়।

**Senior-level model design-এর মূল প্রশ্ন:**
`"আমার data কি একই entity-এর মধ্যে recursive relationship তৈরি করছে?"`

হ্যাঁ → Self Relation consider করো।
না → আলাদা model / normal ForeignKey যথেষ্ট।
