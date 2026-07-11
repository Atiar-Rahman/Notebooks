হ্যাঁ, **nested router ব্যবহার না করেও** খুব সুন্দরভাবে করা যায়। আসলে **বেশিরভাগ DRF project-এ nested router ব্যবহার করা হয় না**।

ধরো তোমার Model:

```python
class Category(models.Model):
    name = models.CharField(max_length=100)


class Product(models.Model):
    category = models.ForeignKey(
        Category,
        on_delete=models.CASCADE,
        related_name="products"
    )
    name = models.CharField(max_length=100)
```

## URL

```http
GET    /categories/
POST   /categories/

GET    /products/
POST   /products/

GET    /products/{id}/
PATCH  /products/{id}/
DELETE /products/{id}/
```

এখানে কোনো nested router নেই।

---

## Product Create

```http
POST /products/
```

Body

```json
{
    "category": 2,
    "name": "Samsung S25",
    "price": 100000
}
```

Serializer:

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = "__all__"
```

DRF নিজেই `category=2` দেখে ForeignKey relation তৈরি করে।

---

## Category অনুযায়ী Product দেখাতে

Nested URL:

```http
GET /categories/2/products/
```

না করে,

Query Parameter ব্যবহার করো:

```http
GET /products/?category=2
```

ViewSet:

```python
class ProductViewSet(ModelViewSet):
    serializer_class = ProductSerializer

    def get_queryset(self):
        queryset = Product.objects.all()

        category = self.request.query_params.get("category")
        if category:
            queryset = queryset.filter(category_id=category)

        return queryset
```

এখন

```http
GET /products/?category=2
```

শুধু Category 2-এর products দেবে।

---

## কেন এটা ভালো?

- ✅ URL সহজ
    
- ✅ Nested router লাগবে না
    
- ✅ DRF-এর default router দিয়েই হবে
    
- ✅ Search, Filter, Pagination সহজ
    
- ✅ Production project-এ খুব common
    

### Final Recommendation

আমি তোমাকে **nested router ব্যবহার করতে বলব না**, যদি না সত্যিই nested URL দরকার হয়।

এই structure follow করো:

```http
GET    /categories/
POST   /categories/

GET    /products/
GET    /products/?category=2
POST   /products/

GET    /products/{id}/
PATCH  /products/{id}/
DELETE /products/{id}/
```

এটি clean, RESTful এবং production-ready design।

--------

**না, nested route অবশ্যই লাগবে না।** এটা design choice। অনেক বড় production API-তেও nested route ব্যবহার করা হয় না।

ধরো তোমার Model:

```python
Product
    id
    name

Review
    id
    product (FK)
    user (FK)
    rating
    comment

ProductImage
    id
    product (FK)
    image
```

## Option 1 (Recommended) - Flat API

### Reviews

```http
GET    /reviews/
POST   /reviews/
GET    /reviews/{id}/
PATCH  /reviews/{id}/
DELETE /reviews/{id}/
```

Review create:

```json
{
    "product": 15,
    "rating": 5,
    "comment": "Excellent"
}
```

Product অনুযায়ী reviews:

```http
GET /reviews/?product=15
```

---

### Product Images

```http
GET    /product-images/
POST   /product-images/
DELETE /product-images/{id}/
```

Create:

```json
{
    "product": 15,
    "image": "..."
}
```

Product-এর images:

```http
GET /product-images/?product=15
```

---

## Option 2 - Nested API

Reviews

```http
GET /products/15/reviews/
POST /products/15/reviews/
```

Images

```http
GET /products/15/images/
POST /products/15/images/
```

এটাও সঠিক।

---

# কোনটা ব্যবহার করবে?

আমি **Flat API** recommend করব।

```http
GET    /products/
POST   /products/

GET    /reviews/?product=15
POST   /reviews/

GET    /product-images/?product=15
POST   /product-images/
```

কারণ:

- Filter করা সহজ।
    
- Pagination সহজ।
    
- একই endpoint বিভিন্ন জায়গায় reuse করা যায়।
    
- DRF-এর `ModelViewSet` ও `DjangoFilterBackend` দিয়ে সহজে implement করা যায়।
    

---

## তাহলে Nested Route কখন ব্যবহার করব?

যখন child resource **parent ছাড়া কোনো অর্থই বহন করে না** এবং সব access সবসময় parent-এর context-এ হবে।

উদাহরণ:

```http
GET /orders/101/items/
POST /orders/101/items/
```

এখানে `OrderItem` সাধারণত `Order` ছাড়া ব্যবহার হয় না।

---

## E-commerce Project-এর জন্য Recommendation

```http
GET    /products/
POST   /products/

GET    /product-images/?product=15
POST   /product-images/

GET    /reviews/?product=15
POST   /reviews/

GET    /categories/
POST   /categories/
```

এটাই একটি clean, scalable এবং production-ready API design।

> **Rule of thumb:** যদি child model-এ `ForeignKey` থাকে (যেমন `Review → Product`, `ProductImage → Product`), তাহলে nested route **বাধ্যতামূলক নয়**। `product` ID request body বা query parameter হিসেবে পাঠিয়েই সম্পর্ক তৈরি করা যায়।


--------
**না, লাগবে না।** Product আগে `GET` করে আনা **বাধ্যতামূলক নয়**।

ধরো Product-এর ID = `15`।

তুমি সরাসরি review create করতে পারো।

```http
POST /reviews/
```

```json
{
    "product": 15,
    "rating": 5,
    "comment": "Excellent product"
}
```

Backend কী করবে?

1. `product=15` পেল।
    
2. Database-এ Product ID 15 আছে কিনা check করবে।
    
3. থাকলে Review create করবে।
    
4. না থাকলে error দেবে।
    

উদাহরণ:

```json
{
    "product": ["Invalid pk \"15\" - object does not exist."]
}
```

---

## তাহলে GET Product কবে করবে?

Frontend সাধারণত Product Details page-এ গেলে:

```http
GET /products/15/
```

Response:

```json
{
    "id": 15,
    "name": "iPhone 16",
    "price": 120000
}
```

User এই page-তেই review লিখবে।

Submit করলে:

```http
POST /reviews/
```

```json
{
    "product": 15,
    "rating": 5,
    "comment": "Awesome!"
}
```

এখানে `product: 15` frontend-এর কাছেই আগে থেকে আছে (কারণ user Product Details page-এ আছে), তাই আবার `GET` করার দরকার নেই।

---

## Real-world Flow

1. User opens:
    

```http
GET /products/15/
```

2. Product details দেখা হলো।
    
3. User clicks "Write Review".
    
4. Frontend sends:
    

```http
POST /reviews/
```

```json
{
    "product": 15,
    "rating": 5,
    "comment": "Very good."
}
```

---

### Best Practice

- **Review create করার আগে আলাদা করে GET করা বাধ্যতামূলক নয়।**
    
- শুধু **Product ID** থাকলেই যথেষ্ট।
    
- Backend অবশ্যই validate করবে যে Product ID সত্যিই exists কিনা।
    

এটাই DRF এবং বেশিরভাগ production REST API-এর standard practice।

----------
চলো একটা **বাস্তব E-commerce** উদাহরণ দেখি যেখানে অনেক relation আছে। এতে বুঝতে পারবে **কখন nested route দরকার, আর কখন দরকার নেই।**

---

# Database Design

```text
Category
    ↓
Product
    ↓
ProductImage
    ↓
Review
    ↓
Wishlist
    ↓
CartItem
    ↓
OrderItem
```

Model Relation

```text
Category (1)
      │
      │
      ▼
Product (Many)
      │
      ├────────► ProductImage (Many)
      │
      ├────────► Review (Many)
      │
      ├────────► Wishlist (Many)
      │
      └────────► CartItem (Many)
                        │
                        ▼
                    OrderItem
```

---

# Step 1: Category Create (Admin)

```http
POST /categories/
```

```json
{
    "name": "Mobile"
}
```

Database

```text
Category

id | name
------------
1  | Mobile
```

---

# Step 2: Product Create (Admin)

```http
POST /products/
```

```json
{
    "category": 1,
    "name": "Samsung S25",
    "price": 120000
}
```

Database

```text
Product

id | category_id | name
-------------------------
10 |      1      | Samsung S25
```

**এখানে Product শুধু Category ID জানলেই যথেষ্ট।**

---

# Step 3: Product Image Add

```http
POST /product-images/
```

```json
{
    "product": 10,
    "image": "front.jpg"
}
```

Database

```text
ProductImage

id | product_id | image
-------------------------
1  |     10     | front.jpg
```

ProductImage জানে Product ID = 10।

---

# Step 4: User Review দিল

User Product Details page-এ আছে।

সে দেখে

```http
GET /products/10/
```

Response

```json
{
    "id":10,
    "name":"Samsung S25"
}
```

Review Submit

```http
POST /reviews/
```

```json
{
    "product":10,
    "rating":5,
    "comment":"Awesome"
}
```

Database

```text
Review

id | product_id | user_id
----------------------------
1  |     10     |    8
```

Review শুধু Product ID জানে।

---

# Step 5: Wishlist

```http
POST /wishlist/
```

```json
{
    "product":10
}
```

Backend User JWT থেকে User ID নেবে।

Database

```text
Wishlist

id | user_id | product_id
----------------------------
1  |    8    |    10
```

---

# Step 6: Cart

```http
POST /cart/items/
```

```json
{
    "product":10,
    "quantity":2
}
```

Database

```text
CartItem

id | user_id | product_id | qty
--------------------------------
1  |    8    |     10     | 2
```

---

# Step 7: Order

User Checkout করল।

```http
POST /orders/
```

Body

```json
{}
```

Backend নিজেই Cart থেকে Order ও OrderItem তৈরি করবে।

Order

```text
id | user
------------
5  | 8
```

OrderItem

```text
id | order_id | product_id
----------------------------
1  |    5     |    10
```

---

# তাহলে Nested Route কোথায়?

অনেকেই লিখে

```http
POST /products/10/reviews/
POST /products/10/images/
```

কিন্তু একই কাজ Flat API দিয়েও হয়

```http
POST /reviews/
```

```json
{
    "product":10,
    "rating":5
}
```

এবং

```http
POST /product-images/
```

```json
{
    "product":10,
    "image":"front.jpg"
}
```

দুটোর ফলাফল একই।

---

# তাহলে Nested Route কবে ভালো?

ধরো `OrderItem`।

`OrderItem`-এর নিজস্ব কোনো অর্থ নেই, এটি সবসময় একটি `Order`-এর অংশ।

তাই

```http
GET /orders/5/items/
POST /orders/5/items/
```

বোঝা সহজ।

কিন্তু যদি Flat API ব্যবহার করো,

```http
POST /order-items/
```

```json
{
    "order":5,
    "product":10,
    "quantity":2
}
```

এটাও ঠিক।

---

# Production Projects কী করে?

বেশিরভাগ production API (DRF, Laravel, NestJS, Spring Boot) **Flat API** ব্যবহার করে।

```http
GET    /products/
POST   /products/

GET    /reviews/?product=10
POST   /reviews/

GET    /product-images/?product=10
POST   /product-images/

POST   /wishlist/

POST   /cart/items/

POST   /orders/
```

**Rule of thumb:** যদি child model-এর `ForeignKey` (যেমন `product`, `order`, `category`) request body-তে পাঠানো যায়, তাহলে nested route **প্রয়োজনীয় নয়**। Nested route মূলত URL-এ parent context দেখানোর জন্য ব্যবহৃত হয়, relation তৈরি করার জন্য নয়।