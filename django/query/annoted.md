
`annotate()` হলো Django ORM-এর অন্যতম গুরুত্বপূর্ণ feature। এটি **প্রতিটি queryset object-এর সাথে calculated field যোগ করে**, কিন্তু database-এর আসল model field পরিবর্তন করে না।

DRF, E-commerce, Blog, Analytics—সব জায়গায় এটি খুব বেশি ব্যবহার হয়।

---

# annotate() কখন ব্যবহার করবেন?

যখন প্রতিটি object-এর জন্য কোনো **calculated value** দরকার।

যেমন,

* প্রতিটি Author-এর কতগুলো Blog আছে
* প্রতিটি Product-এর Average Rating
* প্রতিটি Category-তে কতগুলো Product
* প্রতিটি Order-এর Total Price
* প্রতিটি Student-এর Total Marks

Database-এ এই field নেই, কিন্তু query result-এ চাই।

---

## Example 1: Count

### Models

```python
class Author(models.Model):
    name = models.CharField(max_length=100)


class Blog(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(
        Author,
        on_delete=models.CASCADE,
        related_name="blogs"
    )
```

ধরুন

```
Author

1 Rahim
2 Karim
```

```
Blog

Django ---- Rahim
Python ---- Rahim
DRF ------ Karim
```

এখন চাই

```
Rahim -> 2 blogs

Karim -> 1 blog
```

তাহলে

```python
from django.db.models import Count

authors = Author.objects.annotate(
    total_blogs=Count("blogs")
)
```

Output

```python
for author in authors:
    print(author.name, author.total_blogs)
```

```
Rahim 2
Karim 1
```

`total_blogs` model-এর field নয়।

এটি annotate() তৈরি করেছে।

---

# Generated SQL

```sql
SELECT
author.id,
author.name,
COUNT(blog.id) AS total_blogs
FROM author
LEFT JOIN blog
GROUP BY author.id;
```

---

# Example 2: Average

```python
class Review(models.Model):
    product = models.ForeignKey(Product,on_delete=models.CASCADE)
    rating = models.IntegerField()
```

Average rating বের করতে

```python
from django.db.models import Avg

products = Product.objects.annotate(
    avg_rating=Avg("review__rating")
)
```

Output

```
Laptop -> 4.6

Phone -> 3.9
```

---

# Example 3: Sum

```python
class OrderItem(models.Model):

    order = models.ForeignKey(Order,on_delete=models.CASCADE)

    quantity = models.IntegerField()

    price = models.DecimalField(...)
```

প্রতি order-এর total

```python
from django.db.models import Sum, F

orders = Order.objects.annotate(
    total=Sum(
        F("orderitem__quantity") *
        F("orderitem__price")
    )
)
```

Output

```
Order 1

Total = 4500
```

---

# Example 4: Conditional Count

Published blog কত?

```python
from django.db.models import Count, Q

authors = Author.objects.annotate(
    published=Count(
        "blogs",
        filter=Q(blogs__status="published")
    )
)
```

Output

```
Rahim

Published = 8
```

---

# Example 5: Boolean

ধরুন

```
Product

Laptop

Phone
```

Review আছে কিনা

```python
from django.db.models import Exists, OuterRef

review_exists = Review.objects.filter(
    product=OuterRef("pk")
)

products = Product.objects.annotate(
    has_review=Exists(review_exists)
)
```

Output

```
Laptop

True

Phone

False
```

---

# Example 6: Case When

Discount দেখাতে চাই

```python
from django.db.models import Case, When, Value

products = Product.objects.annotate(
    discount=Case(
        When(price__gte=1000, then=Value("10%")),
        default=Value("0%")
    )
)
```

Output

```
Laptop

10%
```

---

# Serializer-এ ব্যবহার

```python
class AuthorSerializer(serializers.ModelSerializer):

    class Meta:
        model = Author
        fields = [
            "id",
            "name",
            "total_blogs"
        ]
```

View

```python
queryset = Author.objects.annotate(
    total_blogs=Count("blogs")
)
```

Serializer-এ `total_blogs` model field না হলেও annotate-এর কারণে attribute হিসেবে পাওয়া যাবে।

---

# annotate vs aggregate

### annotate()

প্রতিটি object-এর জন্য value দেয়।

```python
Author.objects.annotate(
    total=Count("blogs")
)
```

Result

```
Rahim 2

Karim 5

Jamal 1
```

---

### aggregate()

পুরো queryset-এর জন্য একটি summary value দেয়।

```python
Author.objects.aggregate(
    total=Count("blogs")
)
```

Output

```python
{
    "total": 8
}
```

---

# annotate + order_by

Most popular author

```python
Author.objects.annotate(
    total=Count("blogs")
).order_by("-total")
```

---

# annotate + filter

```python
Author.objects.annotate(
    total=Count("blogs")
).filter(total__gte=5)
```

Output

```
Authors having 5+ blogs
```

---

# Real-world DRF Example (E-commerce)

```python
from django.db.models import Avg, Count

queryset = Product.objects.annotate(
    average_rating=Avg("reviews__rating"),
    total_reviews=Count("reviews"),
)
```

API Response:

```json
[
    {
        "id": 1,
        "name": "Laptop",
        "average_rating": 4.8,
        "total_reviews": 120
    },
    {
        "id": 2,
        "name": "Phone",
        "average_rating": 4.3,
        "total_reviews": 58
    }
]
```

এখানে `average_rating` এবং `total_reviews` কোনোটিই `Product` model-এর field নয়; `annotate()` query execution-এর সময় এগুলো যোগ করেছে।

---

## `annotate()`-এর জন্য সবচেয়ে ব্যবহৃত Expression

| Function            | কাজ                               |
| ------------------- | --------------------------------- |
| `Count()`           | সম্পর্কিত record-এর সংখ্যা        |
| `Sum()`             | মোট যোগফল                         |
| `Avg()`             | গড়                               |
| `Max()`             | সর্বোচ্চ মান                      |
| `Min()`             | সর্বনিম্ন মান                     |
| `F()`               | Database field-এর উপর calculation |
| `Q()`               | Conditional filter                |
| `Case()` / `When()` | SQL CASE WHEN                     |
| `Value()`           | Constant value                    |
| `Exists()`          | Related record আছে কিনা           |
| `Subquery()`        | অন্য query থেকে value আনা         |
| `Coalesce()`        | `NULL` হলে default value দেওয়া   |

## Senior Django Developer হিসেবে কখন `annotate()` ব্যবহার করবেন?

* Dashboard statistics (প্রতি user-এর order count, revenue)
* Blog site (comment count, like count)
* E-commerce (average rating, review count, stock status)
* Multi-vendor (vendor-wise product count, total sales)
* Reporting ও analytics
* Serializer-এর `SerializerMethodField` এ N+1 query এড়িয়ে calculated data আনতে

**মনে রাখবেন:** যদি calculated value SQL দিয়েই বের করা সম্ভব হয়, তাহলে সাধারণত `annotate()` ব্যবহার করা `SerializerMethodField`-এ আলাদা query চালানোর চেয়ে বেশি efficient এবং scalable।


----
এটা DRF-এর খুব গুরুত্বপূর্ণ একটি বিষয়। উত্তরটি নির্ভর করে **আপনি fieldটি কেন যোগ করছেন** তার উপর।

## Case 1: শুধু Response-এ দেখাতে চান (সবচেয়ে common)

ধরুন `Product` model-এ `average_rating` নামে কোনো field নেই, কিন্তু API response-এ দেখাতে চান।

```python
class ProductSerializer(serializers.ModelSerializer):
    average_rating = serializers.FloatField(read_only=True)

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
            "average_rating",
        ]
```

View:

```python
queryset = Product.objects.annotate(
    average_rating=Avg("reviews__rating")
)
```

এখানে:

* ✅ Response-এ `average_rating` থাকবে।
* ❌ Request body-তে পাঠাতে হবে না।
* কারণ `read_only=True`।

---

## Case 2: Request থেকে value নিতে চান (Model-এ save হবে না)

ধরুন client পাঠাবে

```json
{
    "name": "Laptop",
    "price": 50000,
    "coupon_code": "SAVE10"
}
```

কিন্তু `coupon_code` model-এর field না।

```python
class ProductSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)

    class Meta:
        model = Product
        fields = [
            "name",
            "price",
            "coupon_code",
        ]
```

এখন

```python
def create(self, validated_data):
    coupon = validated_data.pop("coupon_code")

    # coupon validate/apply

    return Product.objects.create(**validated_data)
```

এখানে

* ✅ Request-এ `coupon_code` থাকবে।
* ❌ Response-এ থাকবে না।
* কারণ `write_only=True`।

---

## Case 3: Request এবং Response—দুটোতেই থাকবে

```python
class ProductSerializer(serializers.ModelSerializer):
    discount = serializers.IntegerField()

    class Meta:
        model = Product
        fields = [
            "name",
            "price",
            "discount",
        ]
```

এখন

Request

```json
{
    "name": "Laptop",
    "price": 50000,
    "discount": 10
}
```

Response

```json
{
    "name": "Laptop",
    "price": 50000,
    "discount": 10
}
```

কিন্তু যেহেতু `discount` model-এর field নয়, তাই আপনাকে `create()`/`update()`-এ `validated_data.pop("discount")` করে নিজে handle করতে হবে। না হলে `Product.objects.create(**validated_data)`-এ error হবে, কারণ model `discount` argument চেনে না।

---

## `SerializerMethodField`

```python
class ProductSerializer(serializers.ModelSerializer):
    total_reviews = serializers.SerializerMethodField()

    def get_total_reviews(self, obj):
        return obj.reviews.count()
```

এটি

* ✅ শুধু Response-এ থাকবে।
* ❌ Request-এ কখনোই থাকবে না।
* এটি সবসময় `read_only`।

---

## সারসংক্ষেপ

| Field Type               | Request | Response | Use Case                                                          |
| ------------------------ | ------- | -------- | ----------------------------------------------------------------- |
| `SerializerMethodField`  | ❌       | ✅        | Calculated data                                                   |
| `Field(read_only=True)`  | ❌       | ✅        | `annotate()` বা computed value                                    |
| `Field(write_only=True)` | ✅       | ❌        | Coupon, OTP, Password, confirmation field                         |
| `Field()` (default)      | ✅       | ✅        | Custom input/output, নিজে `create()`/`update()`-এ handle করতে হবে |

### Django/DRF-এ একটি গুরুত্বপূর্ণ নিয়ম

**Serializer-এ model-এর বাইরে field যোগ করা সম্পূর্ণ স্বাভাবিক।** তবে সেই field-এর lifecycle আপনাকেই ঠিক করতে হবে:

* শুধু দেখানোর জন্য → `read_only=True` বা `SerializerMethodField`
* শুধু ইনপুট নেওয়ার জন্য → `write_only=True`
* ইনপুট ও আউটপুট দুটোর জন্য → `create()`/`update()`-এ নিজে handle করতে হবে, কারণ model সেটি স্বয়ংক্রিয়ভাবে save করতে পারে না।


--------------

এটি DRF-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়গুলোর একটি। একজন Senior Django Developer হিসেবে আপনাকে সবসময় আগে ভাবতে হবে:

> **এই field-এর data কোন direction-এ যাবে?**
> 
> - Client ➜ Server?
>     
> - Server ➜ Client?
>     
> - নাকি দুই দিকেই?
>     

এই চিন্তা থেকেই `read_only` এবং `write_only` আসে।

---

# 1. read_only=True

## অর্থ

Server শুধু **পড়ে (read)** client-কে পাঠাবে।

Client কখনো এই field পাঠাতে পারবে না।

```
Database
    │
    ▼
Serializer
    │
    ▼
Response
```

কিন্তু

```
Request
    │
    ▼
Serializer
```

এখানে field ignored হবে।

---

## Example 1

Model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
```

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    average_rating = serializers.FloatField(read_only=True)

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "price",
            "average_rating",
        ]
```

View

```python
queryset = Product.objects.annotate(
    average_rating=Avg("reviews__rating")
)
```

---

### Response

```json
{
    "id":1,
    "name":"Laptop",
    "price":50000,
    "average_rating":4.8
}
```

---

### Client যদি পাঠায়

```json
{
    "name":"Laptop",
    "price":50000,
    "average_rating":1
}
```

কি হবে?

DRF এটাকে **ignore** করবে।

কারণ

```
read_only=True
```

মানে

> "এই field server generate করবে, client না।"

---

# Real Life Examples

```
average_rating

total_reviews

total_sales

created_at

updated_at

id

is_verified
```

এগুলো client পরিবর্তন করতে পারবে না।

---

# 2. write_only=True

এর মানে

Client পাঠাবে

Server receive করবে

Response-এ আর দেখাবে না।

```
Request
    │
    ▼
Serializer
    │
    ▼
Database
```

কিন্তু

```
Database
    │
    ▼
Serializer
    │
    ▼
Response
```

এখানে field থাকবে না।

---

## Example

Registration

Model

```python
class User(AbstractUser):
    pass
```

Serializer

```python
class RegisterSerializer(serializers.ModelSerializer):
    password = serializers.CharField(write_only=True)

    class Meta:
        model = User
        fields = [
            "username",
            "password",
        ]
```

---

### Request

```json
{
    "username":"rahim",
    "password":"123456"
}
```

Serializer password পাবে।

---

create()

```python
def create(self, validated_data):
    password = validated_data.pop("password")

    user = User(**validated_data)

    user.set_password(password)

    user.save()

    return user
```

---

### Response

```json
{
    "username":"rahim"
}
```

Password response-এ নেই।

---

আরও Example

```
OTP

Coupon Code

Old Password

New Password

Confirm Password
```

এগুলো response-এ দেওয়া উচিত নয়।

---

# 3. Neither read_only nor write_only

Default

```
read_only=False

write_only=False
```

মানে

Request-এ থাকবে

Response-এও থাকবে।

---

Example

```python
class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = [
            "name",
            "price",
        ]
```

---

Request

```json
{
    "name":"Laptop",
    "price":50000
}
```

Response

```json
{
    "id":1,
    "name":"Laptop",
    "price":50000
}
```

---

# 4. Non-model field in both request and response

ধরুন

Model

```python
class Product(models.Model):
    name=models.CharField(max_length=100)
```

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):

    discount = serializers.IntegerField()

    class Meta:
        model = Product
        fields = [
            "name",
            "discount"
        ]
```

Request

```json
{
    "name":"Laptop",
    "discount":10
}
```

DRF validation শেষে

```python
validated_data
```

হবে

```python
{
    "name":"Laptop",
    "discount":10
}
```

এখন

```python
Product.objects.create(**validated_data)
```

করলে

Error

```
TypeError

Product() got unexpected keyword argument 'discount'
```

কারণ model-এ

```
discount
```

field নেই।

---

Solution

```python
def create(self, validated_data):

    discount = validated_data.pop("discount")

    product = Product.objects.create(**validated_data)

    return product
```

---

# 5. SerializerMethodField

```python
total_review = serializers.SerializerMethodField()
```

এটা internally

```
read_only=True
```

---

Request

```json
{
    "total_review":100
}
```

Ignored

Response

```json
{
    "total_review":57
}
```

---

# 6. Annotate Field

```python
queryset = Product.objects.annotate(
    avg_rating=Avg("reviews__rating")
)
```

Serializer

```python
avg_rating = serializers.FloatField(read_only=True)
```

Response

```json
{
    "avg_rating":4.8
}
```

Request

```json
{
    "avg_rating":1
}
```

Ignored

---

# DRF Request Flow

```
Client
   │
   ▼
Serializer

↓

Validation

↓

validated_data

↓

create()

↓

Model Save
```

- `write_only` field → `validated_data`-তে থাকে।
    
- `read_only` field → `validated_data`-তে থাকে না।
    

---

# DRF Response Flow

```
Database Object

↓

Serializer

↓

JSON Response
```

- `read_only` field → Response-এ আসে।
    
- `write_only` field → Response-এ আসে না।
    

---

# Senior Developer Best Practices

|Field Type|Request|Response|Best Use|
|---|---|---|---|
|`read_only=True`|❌|✅|`id`, `created_at`, `updated_at`, `average_rating`, `total_reviews`, `total_sales`, `is_verified`|
|`write_only=True`|✅|❌|`password`, `confirm_password`, `otp`, `coupon_code`, `old_password`, `new_password`|
|Default (`read_only=False`, `write_only=False`)|✅|✅|Model-এর সাধারণ editable field যেমন `name`, `email`, `title`, `price`|
|`SerializerMethodField`|❌|✅|Computed বা derived data|
|Non-model field (default)|✅|✅|বিশেষ business logic-এর জন্য, তবে `create()`/`update()`-এ নিজে handle করতে হবে|

## একটি সহজ নিয়ম মনে রাখুন

- **Database বা server যেটি তৈরি/নিয়ন্ত্রণ করে** → `read_only=True`
    
- **Client যেটি পাঠাবে কিন্তু পরে আর ফেরত দেওয়া উচিত নয়** → `write_only=True`
    
- **যেটি user input এবং response—দুটোতেই স্বাভাবিকভাবে থাকা উচিত** → default field (না `read_only`, না `write_only`)
    
- **Model-এ না থাকা field যদি request-এ নেন**, তাহলে `create()` বা `update()`-এ অবশ্যই `validated_data.pop()` করে নিজে handle করতে হবে।

------------------

হ্যাঁ, **পারবেন।** Serializer-এ আপনি **ইচ্ছামতো custom field** যোগ করতে পারেন, এমনকি সেই field model-এ না থাকলেও।

তবে একটি শর্ত আছে:

> **সেই field-এর data কোথা থেকে আসবে বা কোথায় যাবে, সেটা আপনাকেই handle করতে হবে।**

---

## Example 1: Response-এর জন্য custom field

Model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
```

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    message = serializers.CharField(read_only=True)

    class Meta:
        model = Product
        fields = ["id", "name", "price", "message"]
```

এখন `message` model-এ নেই।

আপনাকে `message`-এর value দিতে হবে, যেমন:

```python
class ProductSerializer(serializers.ModelSerializer):
    message = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ["id", "name", "price", "message"]

    def get_message(self, obj):
        return "Available"
```

Response

```json
{
    "id": 1,
    "name": "Laptop",
    "price": 50000,
    "message": "Available"
}
```

---

## Example 2: Request-এর জন্য custom field

```python
class ProductSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)

    class Meta:
        model = Product
        fields = ["name", "price", "coupon_code"]

    def create(self, validated_data):
        coupon = validated_data.pop("coupon_code")

        # coupon validate

        return Product.objects.create(**validated_data)
```

Request

```json
{
    "name": "Laptop",
    "price": 50000,
    "coupon_code": "SAVE10"
}
```

---

## Example 3: Request + Response দুটোতেই

```python
class ProductSerializer(serializers.ModelSerializer):
    discount = serializers.IntegerField()

    class Meta:
        model = Product
        fields = ["name", "price", "discount"]
```

এখন `discount` model-এ নেই, তাই:

```python
def create(self, validated_data):
    discount = validated_data.pop("discount")

    product = Product.objects.create(**validated_data)

    # discount অনুযায়ী অন্য কাজ করুন

    return product
```

---

# Custom field-এর type-ও আপনি ইচ্ছামতো বেছে নিতে পারেন

```python
extra_note = serializers.CharField()

is_premium = serializers.BooleanField()

score = serializers.IntegerField()

amount = serializers.DecimalField(max_digits=10, decimal_places=2)

tags = serializers.ListField(
    child=serializers.CharField()
)

metadata = serializers.JSONField()

email = serializers.EmailField()

website = serializers.URLField()
```

এগুলো model-এ না থাকলেও serializer-এ ব্যবহার করা যায়।

---

# কিন্তু একটা জিনিস মনে রাখবেন

শুধু field declare করলেই হবে না।

যদি fieldটি model-এ না থাকে, তাহলে আপনাকে এর **source** বা **handling** ঠিক করতে হবে।

| Situation          | কী করতে হবে                                                                  |
| ------------------ | ---------------------------------------------------------------------------- |
| Response field     | `SerializerMethodField`, `annotate()`, বা `to_representation()` ব্যবহার করুন |
| Request field      | `create()`/`update()`-এ `validated_data.pop()` করে handle করুন               |
| Request + Response | দুই জায়গাতেই নিজে logic লিখতে হবে                                           |

## Senior Developer Tip

Serializer-এ custom field যোগ করার আগে নিজেকে এই ৩টি প্রশ্ন করুন:

1. **এই data client পাঠাবে, নাকি server তৈরি করবে?**
2. **এই data database-এ save হবে, নাকি শুধু processing-এর জন্য?**
3. **Response-এ দেখানো দরকার, নাকি দরকার নেই?**

এই তিনটি প্রশ্নের উত্তর জানলেই বুঝে যাবেন fieldটি `read_only`, `write_only`, নাকি সাধারণ field হওয়া উচিত।
হ্যাঁ, **আপনার ধারণা একদম সঠিক।** চলুন flow অনুযায়ী দেখি।

ধরুন Model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
```

এখানে `coupon_code` নামে কোনো field নেই।

Serializer:

```python
class ProductSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)

    class Meta:
        model = Product
        fields = ["name", "price", "coupon_code"]
```

Client Request:

```json
{
    "name": "Laptop",
    "price": 50000,
    "coupon_code": "SAVE10"
}
```

Validation-এর পরে `validated_data` হবে:

```python
{
    "name": "Laptop",
    "price": 50000,
    "coupon_code": "SAVE10"
}
```

এখন যদি আপনি কিছুই override না করেন, তাহলে `ModelSerializer`-এর default `create()` চলবে, যা মূলত এমন কাজ করে:

```python
Product.objects.create(**validated_data)
```

অর্থাৎ,

```python
Product.objects.create(
    name="Laptop",
    price=50000,
    coupon_code="SAVE10"   # ❌ Model-এ এই field নেই
)
```

তখন error হবে:

```text
TypeError:
Product() got an unexpected keyword argument 'coupon_code'
```

---

## সঠিক উপায়

```python
class ProductSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)

    class Meta:
        model = Product
        fields = ["name", "price", "coupon_code"]

    def create(self, validated_data):
        coupon = validated_data.pop("coupon_code")

        # coupon নিয়ে business logic
        print(coupon)

        return Product.objects.create(**validated_data)
```

এখন `validated_data` দুই ধাপে হবে:

প্রথমে:

```python
{
    "name": "Laptop",
    "price": 50000,
    "coupon_code": "SAVE10"
}
```

`pop()` করার পরে:

```python
{
    "name": "Laptop",
    "price": 50000
}
```

এখন

```python
Product.objects.create(**validated_data)
```

হবে

```python
Product.objects.create(
    name="Laptop",
    price=50000
)
```

এবার কোনো error হবে না।

---

## কেন `pop()` ব্যবহার করি?

দুইটি কারণে:

1. **Extra field আলাদা করে business logic-এ ব্যবহার করতে পারি।**
2. **Model-এ না থাকা field `validated_data` থেকে সরিয়ে দিই**, যাতে `objects.create()`-এ error না আসে।

---

## মনে রাখার নিয়ম

* **Model-এ নেই + Serializer-এ request field আছে** → `create()`/`update()` override করে `validated_data.pop()` করতে হবে (যদি fieldটি save না করতে চান)।
* **Model-এ আছে** → `pop()` করার দরকার নেই (যদি বিশেষ কোনো processing না লাগে), কারণ `ModelSerializer` নিজেই save করে দেবে।

এটাই DRF-এ custom input field handle করার সবচেয়ে প্রচলিত এবং recommended pattern।
হ্যাঁ, **এটাই Professional/Senior approach।** বাস্তব E-commerce application-এ coupon code সাধারণত আলাদা `Coupon` model-এ থাকে।

Flowটা এমন হবে:

```text
Client
   │
   │ coupon_code = "SAVE10"
   ▼
Serializer
   │
   ▼
validated_data
   │
   ▼
create()
   │
   ▼
Coupon Model থেকে code খুঁজে বের করা
   │
   ▼
Valid?
   │
 ┌─Yes──────────────┐
 │                  │
 ▼                  ▼
Discount Apply   Invalid Coupon Error
 │
 ▼
Order Save
```

---

## Coupon Model

```python
class Coupon(models.Model):
    code = models.CharField(max_length=20, unique=True)
    discount = models.PositiveIntegerField()
    is_active = models.BooleanField(default=True)
```

Database

| id | code   | discount | is_active |
| -- | ------ | -------- | --------- |
| 1  | SAVE10 | 10       | True      |
| 2  | EID50  | 50       | True      |
| 3  | OLD20  | 20       | False     |

---

## Order Model

```python
class Order(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    total = models.DecimalField(max_digits=10, decimal_places=2)
```

এখানে `coupon_code` field নেই।

---

## Serializer

```python
class OrderSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)

    class Meta:
        model = Order
        fields = [
            "product",
            "coupon_code",
        ]
```

---

## create()

```python
from rest_framework.exceptions import ValidationError

def create(self, validated_data):
    coupon_code = validated_data.pop("coupon_code")

    try:
        coupon = Coupon.objects.get(
            code=coupon_code,
            is_active=True
        )
    except Coupon.DoesNotExist:
        raise ValidationError({
            "coupon_code": "Invalid coupon."
        })

    product = validated_data["product"]

    discount_amount = (
        product.price * coupon.discount / 100
    )

    total = product.price - discount_amount

    return Order.objects.create(
        product=product,
        total=total
    )
```

---

## যদি Coupon-ও Order-এ রাখতে চান

অনেক e-commerce site পরে জানতে চায় কোন order-এ কোন coupon ব্যবহার হয়েছে। তখন `Order` model-এ relation রাখা হয়।

```python
class Order(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.SET_NULL,
        null=True,
        blank=True
    )
    total = models.DecimalField(max_digits=10, decimal_places=2)
```

তখন:

```python
return Order.objects.create(
    product=product,
    coupon=coupon,
    total=total
)
```

এখানে লক্ষ্য করুন:

* User `"SAVE10"` string পাঠিয়েছে।
* আপনি `Coupon` model থেকে সেই record বের করেছেন।
* Database-এ `"SAVE10"` string নয়, বরং `Coupon` object-এর **ForeignKey** save হয়েছে।

---

## Senior Best Practice

সাধারণত flowটি হয়:

1. User request-এ `coupon_code` পাঠায়।
2. Serializer এটি receive করে।
3. `create()` বা service layer-এ `Coupon` model থেকে code verify করা হয়।
4. Invalid হলে `ValidationError` return করা হয়।
5. Valid হলে discount calculate করা হয়।
6. Order save হয়।
7. প্রয়োজন হলে `Coupon`-এর ForeignKey order-এর সাথে save করা হয়।

**গুরুত্বপূর্ণ:** Coupon verification-এর logic অনেক project-এ `create()`-এর বদলে `validate_coupon_code()` বা `validate()` method, অথবা আলাদা service class-এ রাখা হয়। এতে serializer পরিষ্কার থাকে এবং business logic reuse করা সহজ হয়।


হ্যাঁ, **সাধারণভাবে উত্তর হলো: হ্যাঁ।** যদি serializer-এ কোনো field **required** হয়, তাহলে সেই serializer ব্যবহার করে `POST`/`PUT` request করলে client-কে সেই field পাঠাতেই হবে।

তবে এখানে কিছু গুরুত্বপূর্ণ ব্যতিক্রম আছে।

---

# Example

Model

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
```

Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ["name", "price"]
```

View

```python
class ProductCreateView(CreateAPIView):
    serializer_class = ProductSerializer
```

---

## Client Request

```json
{
    "name": "Laptop"
}
```

কি হবে?

Response

```json
{
    "price": [
        "This field is required."
    ]
}
```

কারণ `price` required।

---

# কখন required হয়?

DRF model দেখে determine করে।

```python
name = models.CharField(max_length=100)
```

এখানে

* `null=False`
* `blank=False`

তাই serializer-এ

```python
required=True
```

হয়ে যায়।

---

# কখন required হয় না?

## 1. `required=False`

```python
coupon_code = serializers.CharField(required=False)
```

Request

```json
{
    "name": "Laptop",
    "price": 50000
}
```

এখানে `coupon_code` না পাঠালেও validation pass করবে।

---

## 2. `read_only=True`

```python
average_rating = serializers.FloatField(read_only=True)
```

এটি request-এ পাঠানোর দরকার নেই।

---

## 3. Model-এ `blank=True`

```python
description = models.TextField(
    blank=True
)
```

Serializer-এ সাধারণত

```python
required=False
```

হয়ে যায়।

---

## 4. Model-এ `default`

```python
status = models.CharField(
    max_length=20,
    default="pending"
)
```

Client না পাঠালেও Django default value ব্যবহার করবে।

---

# View serializer ব্যবহার করলে কি সব field request-এ লাগবে?

**না।**

শুধু যেগুলো

* required=True
* read_only নয়

সেগুলোই লাগবে।

---

# Example

```python
class ProductSerializer(serializers.ModelSerializer):

    id = serializers.IntegerField(read_only=True)

    name = serializers.CharField()

    price = serializers.IntegerField()

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
            "coupon_code"
        ]
```

Request

```json
{
    "name": "Laptop",
    "price": 50000
}
```

✔ Valid

কারণ

* `id` → read_only
* `coupon_code` → required=False

---

# আর যদি

```json
{
    "price": 50000
}
```

তাহলে

❌ Error

```json
{
    "name": [
        "This field is required."
    ]
}
```

---

# PUT বনাম PATCH

এখানে একটি গুরুত্বপূর্ণ বিষয় আছে।

### PUT

```http
PUT /products/1/
```

সাধারণত serializer-এর **সব required field** পাঠানো উচিত, কারণ এটি পুরো resource replace করার জন্য।

### PATCH

```http
PATCH /products/1/
```

শুধু যে field update করবেন সেটাই পাঠালেই হবে।

যেমন

```json
{
    "price": 55000
}
```

এটাও valid।

কারণ DRF `PATCH`-এ serializer-কে

```python
partial=True
```

দিয়ে চালায়।

---

## সহজে মনে রাখুন

| Field Type        | Request-এ পাঠাতে হবে?                    |
| ----------------- | ---------------------------------------- |
| `required=True`   | ✅ হ্যাঁ                                  |
| `required=False`  | ❌ না                                     |
| `read_only=True`  | ❌ না                                     |
| `write_only=True` | ✅ যদি `required=True` হয়, নইলে optional |
| `PATCH` request   | শুধুমাত্র update হওয়া field             |
| `PUT` request     | সাধারণত সব required field                |

**Rule of thumb:** কোনো serializer view-এ ব্যবহার হচ্ছে মানেই সব field request-এ দিতে হবে—এটা ঠিক নয়। আসল বিষয় হলো প্রতিটি field-এর `required`, `read_only`, `write_only`, `default`, এবং requestটি `POST`/`PUT` নাকি `PATCH`।


একদম ঠিক ধরেছেন। `required` নির্ধারণ হয় **serializer field-এর configuration** এবং `ModelSerializer` হলে **model field-এর metadata** থেকে।

এখন আপনার মূল প্রশ্ন:

> **`write_only` field কি required হয়?**

**উত্তর: `write_only` এবং `required` সম্পূর্ণ আলাদা বিষয়।**

* `write_only` বলে **response-এ দেখানো হবে কি না**।
* `required` বলে **request-এ পাঠানো বাধ্যতামূলক কি না**।

এরা একে অপরের উপর নির্ভরশীল নয়।

---

## Case 1: write_only + required=True (Default)

```python
coupon_code = serializers.CharField(write_only=True)
```

এখানে `required=True` (default)।

Request

```json
{
    "name": "Laptop"
}
```

Response

```json
{
    "coupon_code": [
        "This field is required."
    ]
}
```

অর্থাৎ `coupon_code` পাঠাতেই হবে।

---

## Case 2: write_only + required=False

```python
coupon_code = serializers.CharField(
    write_only=True,
    required=False
)
```

Request

```json
{
    "name": "Laptop"
}
```

✔️ Valid

কারণ `coupon_code` optional।

যদি পাঠায়:

```json
{
    "name": "Laptop",
    "coupon_code": "SAVE10"
}
```

তবুও ✔️ Valid।

---

## Case 3: Password (Real Example)

```python
class RegisterSerializer(serializers.Serializer):
    username = serializers.CharField()
    password = serializers.CharField(write_only=True)
```

এখানে

* `username` → required
* `password` → required

কারণ `password` না দিলে user create করা যাবে না।

---

## Case 4: Coupon (Optional)

```python
class OrderSerializer(serializers.Serializer):
    product = serializers.IntegerField()
    coupon_code = serializers.CharField(
        write_only=True,
        required=False
    )
```

এখানে coupon optional।

User চাইলে coupon ব্যবহার করবে, না চাইলে করবে না।

---

# মনে রাখার সহজ টেবিল

| Property          | কাজ                                      |
| ----------------- | ---------------------------------------- |
| `required=True`   | Request-এ field পাঠাতেই হবে              |
| `required=False`  | Request-এ field না পাঠালেও চলবে          |
| `write_only=True` | Request-এ আসবে, Response-এ যাবে না       |
| `read_only=True`  | Response-এ যাবে, Request-এ নেওয়া হবে না |

### সবচেয়ে গুরুত্বপূর্ণ বিষয়

নিচের দুটি line-এর অর্থ আলাদা:

```python
password = serializers.CharField(write_only=True)
```

মানে:

* ✅ Request-এ `password` আসবে।
* ❌ Response-এ `password` যাবে না।
* ✅ এবং `required=True` হওয়ায় request-এ পাঠানো বাধ্যতামূলক।

আর যদি লিখেন:

```python
password = serializers.CharField(
    write_only=True,
    required=False
)
```

তাহলে:

* ✅ Request-এ পাঠাতে **পারবে**।
* ❌ না পাঠালেও validation error হবে না।
* ❌ Response-এ কখনোই যাবে না।

**সুতরাং, `write_only` হওয়া মানেই required নয়।** `required` আলাদাভাবে নির্ধারণ হয়।
হ্যাঁ। **`required` আপনি নিজেও নির্ধারণ করে দিতে পারেন**, আবার অনেক ক্ষেত্রে DRF নিজেও নির্ধারণ করে দেয়।

## ১. আপনি Explicitly নির্ধারণ করেন

```python
coupon_code = serializers.CharField(required=True)

# অথবা

coupon_code = serializers.CharField(required=False)
```

এখানে DRF আপনার দেওয়া value-ই ব্যবহার করবে।

---

## ২. `ModelSerializer` হলে DRF নিজে নির্ধারণ করে

ধরুন Model:

```python
class Product(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField(blank=True)
```

Serializer:

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = "__all__"
```

DRF নিজেই বানিয়ে ফেলবে:

```python
name = serializers.CharField(required=True)

description = serializers.CharField(required=False)
```

কারণ Model-এ

* `name` → `blank=False`
* `description` → `blank=True`

---

## ৩. Custom Serializer Field

```python
class ProductSerializer(serializers.ModelSerializer):
    coupon_code = serializers.CharField(write_only=True)
```

এখানে `coupon_code` model-এর field নয়।

তাই DRF default হিসেবে ধরে:

```python
required=True
```

আপনি যদি optional করতে চান:

```python
coupon_code = serializers.CharField(
    write_only=True,
    required=False
)
```

---

## সহজ নিয়ম

| Field Type                      | `required` কে ঠিক করে?                                            |
| ------------------------------- | ----------------------------------------------------------------- |
| Model field (`ModelSerializer`) | DRF model দেখে ঠিক করে (আপনি override করতে পারেন)                 |
| Custom serializer field         | DRF-এর default `required=True` (আপনি `required=False` দিতে পারেন) |

### Senior Tip

একটি serializer field-এর ৪টি property আলাদা আলাদা বিষয়:

```python
coupon_code = serializers.CharField(
    required=False,   # Request-এ পাঠানো বাধ্যতামূলক কি?
    write_only=True,  # Response-এ দেখানো হবে কি?
    allow_blank=True, # Empty string "" গ্রহণ করবে কি?
    allow_null=True   # null গ্রহণ করবে কি?
)
```

এগুলো একে অপরের থেকে স্বাধীন। তাই `required`, `write_only`, `allow_blank`, `allow_null`—প্রতিটির কাজ আলাদা এবং প্রয়োজন অনুযায়ী সেট করা হয়।
