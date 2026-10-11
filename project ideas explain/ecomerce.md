অবশ্যই। **Multi-vendor E-commerce** project production-grade করতে হলে শুধু `User`, `Product`, `Order` model বানালেই হবে না। User identity, seller/vendor, customer profile, address, product catalog, inventory, cart, order, payment, shipment, coupon, review—সবগুলো আলাদা responsibility অনুযায়ী design করা ভালো।

আমি Django/DRF ধরে একটি **scalable model architecture** দিচ্ছি।

## 1. Overall architecture

```text
User
 ├── Profile
 ├── Address
 ├── SellerProfile
 │    └── SellerDocument / SellerBankAccount
 │
 └── UserRole / Permission

Category
 ├── Product
 │    ├── ProductImage
 │    ├── ProductVariant
 │    ├── ProductAttribute
 │    └── ProductTag
 │
 └── SubCategory

Seller
 ├── Product
 ├── Inventory
 └── OrderItem

Customer
 ├── Cart
 ├── Wishlist
 ├── Review
 └── Order

Order
 ├── OrderItem
 ├── Payment
 ├── Shipment
 └── OrderStatusHistory

Coupon
 └── CouponUsage

Review
 └── ReviewImage
```

---

# 2. `User` Model

Production project-এ Django-এর `AbstractUser`/`AbstractBaseUser` ভিত্তিক custom user রাখব।

```python
class User(AbstractUser):
    class Role(models.TextChoices):
        ADMIN = "ADMIN", "Admin"
        CUSTOMER = "CUSTOMER", "Customer"
        SELLER = "SELLER", "Seller"
        STAFF = "STAFF", "Staff"

    username = None

    email = models.EmailField(
        unique=True,
        db_index=True
    )

    first_name = models.CharField(
        max_length=100,
        blank=True
    )

    last_name = models.CharField(
        max_length=100,
        blank=True
    )

    phone_number = models.CharField(
        max_length=20,
        unique=True,
        null=True,
        blank=True,
        db_index=True
    )

    role = models.CharField(
        max_length=20,
        choices=Role.choices,
        default=Role.CUSTOMER,
        db_index=True
    )

    is_email_verified = models.BooleanField(
        default=False
    )

    is_phone_verified = models.BooleanField(
        default=False
    )

    last_login_ip = models.GenericIPAddressField(
        null=True,
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    is_active = models.BooleanField(
        default=True
    )

    USERNAME_FIELD = "email"
    REQUIRED_FIELDS = []
```

### কেন এগুলো?

|Field|Purpose|
|---|---|
|`email`|Login|
|`phone_number`|OTP/contact|
|`role`|Customer/Seller/Admin|
|`is_email_verified`|Email verification|
|`is_phone_verified`|Phone verification|
|`is_active`|Account activation|
|`last_login_ip`|Security/audit|
|timestamps|Record tracking|

### একটা important point

তুমি আগে `is_active` + `is_deleted` নিয়ে কাজ করছিলে।

Production design-এ আমি সাধারণত:

```text
is_active
is_deleted
deleted_at
```

এই তিনটা আলাদা meaning-এ রাখতে পারি।

```text
is_active = user can login/use system?
is_deleted = soft deleted?
deleted_at = কখন delete হয়েছে?
```

---

# 3. `Profile`

`User` আর `Profile` আলাদা রাখা ভালো।

```python
class Profile(models.Model):

    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="profile"
    )

    avatar = models.ImageField(
        upload_to="profiles/",
        null=True,
        blank=True
    )

    date_of_birth = models.DateField(
        null=True,
        blank=True
    )

    gender = models.CharField(
        max_length=20,
        null=True,
        blank=True
    )

    bio = models.TextField(
        blank=True
    )

    website = models.URLField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

### User vs Profile

```text
User
 ├── email
 ├── password
 ├── phone
 ├── role
 └── verification

Profile
 ├── avatar
 ├── DOB
 ├── gender
 ├── bio
 └── website
```

অর্থাৎ authentication-related data → `User`

additional personal information → `Profile`

---

# 4. Customer Address

একজন customer-এর multiple address থাকতে পারে।

```python
class Address(models.Model):

    class AddressType(models.TextChoices):
        HOME = "HOME", "Home"
        OFFICE = "OFFICE", "Office"
        OTHER = "OTHER", "Other"

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="addresses"
    )

    address_type = models.CharField(
        max_length=20,
        choices=AddressType.choices,
        default=AddressType.HOME
    )

    full_name = models.CharField(
        max_length=150
    )

    phone_number = models.CharField(
        max_length=20
    )

    address_line_1 = models.CharField(
        max_length=255
    )

    address_line_2 = models.CharField(
        max_length=255,
        blank=True
    )

    city = models.CharField(
        max_length=100
    )

    state = models.CharField(
        max_length=100,
        blank=True
    )

    postal_code = models.CharField(
        max_length=20
    )

    country = models.CharField(
        max_length=100,
        default="Bangladesh"
    )

    is_default = models.BooleanField(
        default=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

একজন user:

```text
User
 ├── Address 1 → Home
 ├── Address 2 → Office
 └── Address 3 → Village Home
```

---

# 5. Vendor / Seller

Multi-vendor system-এর সবচেয়ে important অংশ।

User এবং Seller আলাদা concept।

```python
class SellerProfile(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        APPROVED = "APPROVED", "Approved"
        REJECTED = "REJECTED", "Rejected"
        SUSPENDED = "SUSPENDED", "Suspended"

    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="seller_profile"
    )

    store_name = models.CharField(
        max_length=200,
        unique=True
    )

    store_slug = models.SlugField(
        max_length=220,
        unique=True
    )

    store_logo = models.ImageField(
        upload_to="seller/logos/",
        null=True,
        blank=True
    )

    store_banner = models.ImageField(
        upload_to="seller/banners/",
        null=True,
        blank=True
    )

    description = models.TextField(
        blank=True
    )

    business_name = models.CharField(
        max_length=255,
        blank=True
    )

    business_registration_number = models.CharField(
        max_length=100,
        blank=True
    )

    tax_identification_number = models.CharField(
        max_length=100,
        blank=True
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING,
        db_index=True
    )

    commission_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        default=10
    )

    is_verified = models.BooleanField(
        default=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

এখন structure:

```text
User
  │
  ├── Customer
  │
  └── SellerProfile
          │
          ├── Store
          ├── Products
          ├── Orders
          └── Commission
```

---

# 6. Seller Bank Account

Seller-এর টাকা কোথায় যাবে সেটা track করতে হবে।

```python
class SellerBankAccount(models.Model):

    seller = models.ForeignKey(
        SellerProfile,
        on_delete=models.CASCADE,
        related_name="bank_accounts"
    )

    account_name = models.CharField(
        max_length=150
    )

    bank_name = models.CharField(
        max_length=150
    )

    account_number = models.CharField(
        max_length=100
    )

    branch_name = models.CharField(
        max_length=150,
        blank=True
    )

    routing_number = models.CharField(
        max_length=100,
        blank=True
    )

    is_primary = models.BooleanField(
        default=False
    )

    is_verified = models.BooleanField(
        default=False
    )
```

Production system-এ account number-এর মতো sensitive information-এর storage/access carefully handle করতে হবে।

---

# 7. Category

```python
class Category(models.Model):

    name = models.CharField(
        max_length=150
    )

    slug = models.SlugField(
        unique=True
    )

    description = models.TextField(
        blank=True
    )

    image = models.ImageField(
        upload_to="categories/",
        null=True,
        blank=True
    )

    parent = models.ForeignKey(
        "self",
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="children"
    )

    is_active = models.BooleanField(
        default=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

এতে:

```text
Electronics
 ├── Mobile
 ├── Laptop
 └── Camera

Fashion
 ├── Men
 ├── Women
 └── Kids
```

---

# 8. Product

Product-এর seller থাকতে হবে।

```python
class Product(models.Model):

    seller = models.ForeignKey(
        SellerProfile,
        on_delete=models.CASCADE,
        related_name="products"
    )

    category = models.ForeignKey(
        Category,
        on_delete=models.PROTECT,
        related_name="products"
    )

    name = models.CharField(
        max_length=255
    )

    slug = models.SlugField(
        max_length=280
    )

    sku = models.CharField(
        max_length=100,
        unique=True
    )

    description = models.TextField()

    short_description = models.CharField(
        max_length=500,
        blank=True
    )

    brand = models.CharField(
        max_length=150,
        blank=True
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    discount_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True
    )

    weight = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        null=True,
        blank=True
    )

    is_active = models.BooleanField(
        default=True
    )

    is_published = models.BooleanField(
        default=False
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

---

# 9. Product Image

এক product-এর multiple image থাকবে।

```python
class ProductImage(models.Model):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="images"
    )

    image = models.ImageField(
        upload_to="products/"
    )

    alt_text = models.CharField(
        max_length=255,
        blank=True
    )

    sort_order = models.PositiveIntegerField(
        default=0
    )

    is_primary = models.BooleanField(
        default=False
    )
```

---

# 10. Product Variant

Production e-commerce-এ খুব গুরুত্বপূর্ণ।

যেমন:

```text
T-Shirt

Size:
 S
 M
 L
 XL

Color:
 Black
 White
 Red
```

Model:

```python
class ProductVariant(models.Model):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="variants"
    )

    sku = models.CharField(
        max_length=100,
        unique=True
    )

    name = models.CharField(
        max_length=150
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    stock_quantity = models.PositiveIntegerField(
        default=0
    )

    is_active = models.BooleanField(
        default=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

---

# 11. Inventory

Product-এর stock management আলাদা model-এ রাখা scalable।

```python
class Inventory(models.Model):

    product = models.OneToOneField(
        Product,
        on_delete=models.CASCADE,
        related_name="inventory"
    )

    quantity = models.PositiveIntegerField(
        default=0
    )

    reserved_quantity = models.PositiveIntegerField(
        default=0
    )

    reorder_level = models.PositiveIntegerField(
        default=5
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

Available stock:

```text
available =
quantity - reserved_quantity
```

---

# 12. Cart

```python
class Cart(models.Model):

    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE,
        related_name="cart"
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

Cart item:

```python
class CartItem(models.Model):

    cart = models.ForeignKey(
        Cart,
        on_delete=models.CASCADE,
        related_name="items"
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE
    )

    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.SET_NULL,
        null=True,
        blank=True
    )

    quantity = models.PositiveIntegerField(
        default=1
    )
```

---

# 13. Wishlist

```python
class Wishlist(models.Model):

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="wishlist"
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="wishlisted_by"
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

এখানে unique constraint:

```text
user + product
```

দিয়ে duplicate wishlist prevent করবে।

---

# 14. Order

এখানে একটা important production concept আছে।

Customer একবার checkout করলেও তার cart-এ যদি ৩ seller-এর product থাকে:

```text
Seller A → Product 1
Seller B → Product 2
Seller C → Product 3
```

তাহলে **একটা customer order-এর মধ্যে multiple seller order** থাকতে পারে।

তাই:

```text
Order
 ├── SellerOrder
 │     └── OrderItem
 │
 ├── SellerOrder
 │     └── OrderItem
 │
 └── SellerOrder
       └── OrderItem
```

এটা multi-vendor architecture-এর জন্য খুব useful।

---

# 15. Main Order

```python
class Order(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        CONFIRMED = "CONFIRMED", "Confirmed"
        COMPLETED = "COMPLETED", "Completed"
        CANCELLED = "CANCELLED", "Cancelled"

    order_number = models.CharField(
        max_length=50,
        unique=True
    )

    customer = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="orders"
    )

    shipping_address = models.ForeignKey(
        Address,
        on_delete=models.PROTECT
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    shipping_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

---

# 16. SellerOrder

এটা Multi-vendor-এর জন্য অত্যন্ত important।

```python
class SellerOrder(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PROCESSING = "PROCESSING", "Processing"
        SHIPPED = "SHIPPED", "Shipped"
        DELIVERED = "DELIVERED", "Delivered"
        CANCELLED = "CANCELLED", "Cancelled"

    order = models.ForeignKey(
        Order,
        on_delete=models.CASCADE,
        related_name="seller_orders"
    )

    seller = models.ForeignKey(
        SellerProfile,
        on_delete=models.PROTECT,
        related_name="orders"
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    commission = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    seller_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )
```

Example:

```text
Order #1001
Customer: Atiar

SellerOrder 1
    Seller A
    iPhone
    Laptop

SellerOrder 2
    Seller B
    T-Shirt
```

---

# 17. OrderItem

```python
class OrderItem(models.Model):

    seller_order = models.ForeignKey(
        SellerOrder,
        on_delete=models.CASCADE,
        related_name="items"
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT
    )

    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.PROTECT,
        null=True,
        blank=True
    )

    product_name = models.CharField(
        max_length=255
    )

    sku = models.CharField(
        max_length=100
    )

    quantity = models.PositiveIntegerField()

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    total_price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )
```

### কেন `product_name` আবার রাখছি?

ধরো customer আজ কিনলো:

```text
iPhone 17
```

৬ মাস পরে seller product-এর নাম পরিবর্তন করল:

```text
iPhone 17 Pro Max
```

পুরনো invoice/order-এ আগের নাম রাখতে চাই।

তাই order-এর সময় snapshot data রাখা হয়।

---

# 18. Payment

```python
class Payment(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PAID = "PAID", "Paid"
        FAILED = "FAILED", "Failed"
        REFUNDED = "REFUNDED", "Refunded"

    order = models.OneToOneField(
        Order,
        on_delete=models.PROTECT,
        related_name="payment"
    )

    transaction_id = models.CharField(
        max_length=255,
        unique=True,
        null=True,
        blank=True
    )

    payment_method = models.CharField(
        max_length=50
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

# 19. Shipment

```python
class Shipment(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PROCESSING = "PROCESSING", "Processing"
        SHIPPED = "SHIPPED", "Shipped"
        DELIVERED = "DELIVERED", "Delivered"
        RETURNED = "RETURNED", "Returned"

    seller_order = models.OneToOneField(
        SellerOrder,
        on_delete=models.PROTECT,
        related_name="shipment"
    )

    courier_name = models.CharField(
        max_length=100,
        blank=True
    )

    tracking_number = models.CharField(
        max_length=150,
        blank=True
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )

    shipped_at = models.DateTimeField(
        null=True,
        blank=True
    )

    delivered_at = models.DateTimeField(
        null=True,
        blank=True
    )
```

---

# 20. Review

```python
class Review(models.Model):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="reviews"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="reviews"
    )

    order_item = models.ForeignKey(
        OrderItem,
        on_delete=models.PROTECT
    )

    rating = models.PositiveSmallIntegerField()

    title = models.CharField(
        max_length=255,
        blank=True
    )

    comment = models.TextField(
        blank=True
    )

    is_verified_purchase = models.BooleanField(
        default=True
    )

    is_approved = models.BooleanField(
        default=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )
```

এখানে `order_item` থাকার কারণে verify করা যায়:

> সত্যিই customer এই product কিনেছে কিনা।

---

# 21. Coupon

```python
class Coupon(models.Model):

    code = models.CharField(
        max_length=50,
        unique=True
    )

    description = models.TextField(
        blank=True
    )

    discount_percentage = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        null=True,
        blank=True
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True
    )

    minimum_order_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    maximum_discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True
    )

    usage_limit = models.PositiveIntegerField(
        null=True,
        blank=True
    )

    used_count = models.PositiveIntegerField(
        default=0
    )

    starts_at = models.DateTimeField()

    expires_at = models.DateTimeField()

    is_active = models.BooleanField(
        default=True
    )
```

---

# 22. Coupon Usage

```python
class CouponUsage(models.Model):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT
    )

    user = models.ForeignKey(
        User,
        on_delete=models.PROTECT
    )

    order = models.ForeignKey(
        Order,
        on_delete=models.PROTECT
    )

    used_at = models.DateTimeField(
        auto_now_add=True
    )
```

---

# 23. Seller Commission

Multi-vendor system-এ platform commission track করতে হবে।

```python
class SellerCommission(models.Model):

    seller_order = models.OneToOneField(
        SellerOrder,
        on_delete=models.PROTECT,
        related_name="commission_record"
    )

    seller = models.ForeignKey(
        SellerProfile,
        on_delete=models.PROTECT
    )

    order_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    commission_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2
    )

    commission_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    seller_earning = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

Example:

```text
Product sale = ৳10,000

Platform commission = 10%

Platform = ৳1,000
Seller = ৳9,000
```

---

# 24. Model relationship পুরোটা

শেষে architecture হবে:

```text
                         ┌──────────────┐
                         │     User     │
                         └──────┬───────┘
                                │
              ┌─────────────────┼─────────────────┐
              │                 │                 │
              ▼                 ▼                 ▼
          Profile            Address        SellerProfile
                                                  │
                                                  │
                                                  ▼
                                              Product
                                                  │
                          ┌───────────────────────┼─────────────────┐
                          │                       │                 │
                          ▼                       ▼                 ▼
                       Category             ProductImage       Variant
                          │
                          ▼
                       Products


User
 │
 ├── Cart
 │    └── CartItem
 │
 ├── Wishlist
 │
 ├── Orders
 │      │
 │      ▼
 │    Order
 │      │
 │      ├── Payment
 │      │
 │      └── SellerOrder
 │             │
 │             ├── OrderItem
 │             │
 │             ├── Shipment
 │             │
 │             └── Commission
 │
 └── Reviews
```

---

# 25. Production-grade project structure

আমি সব model এক `models.py`-তে রাখতাম না।

```text
apps/
│
├── users/
│   ├── models/
│   │   ├── user.py
│   │   ├── profile.py
│   │   ├── address.py
│   │   └── seller.py
│   │
│   ├── serializers/
│   ├── views/
│   └── urls.py
│
├── catalog/
│   ├── models/
│   │   ├── category.py
│   │   ├── product.py
│   │   ├── variant.py
│   │   ├── image.py
│   │   └── inventory.py
│   ├── serializers/
│   ├── views/
│   └── urls.py
│
├── cart/
│   ├── models/
│   │   ├── cart.py
│   │   └── cart_item.py
│   └── ...
│
├── orders/
│   ├── models/
│   │   ├── order.py
│   │   ├── seller_order.py
│   │   └── order_item.py
│   └── ...
│
├── payments/
│   ├── models/
│   │   └── payment.py
│   └── ...
│
├── shipping/
│   ├── models/
│   │   └── shipment.py
│   └── ...
│
├── reviews/
│   ├── models/
│   │   └── review.py
│   └── ...
│
├── coupons/
│   └── ...
│
└── core/
    ├── models/
    │   └── base.py
    ├── permissions/
    ├── exceptions/
    └── utils/
```

## সবচেয়ে গুরুত্বপূর্ণ design decision

তোমার project-এ আমি এই flow রাখব:

```text
User
 ↓
SellerProfile
 ↓
Product
 ↓
Cart
 ↓
Order
 ↓
SellerOrder
 ↓
OrderItem
 ↓
Payment
 ↓
Shipment
 ↓
SellerCommission
```

এখানে **`Order → SellerOrder → OrderItem`** structure-টাই multi-vendor e-commerce-এর সবচেয়ে গুরুত্বপূর্ণ অংশ। কারণ একজন customer একই checkout-এ একাধিক seller-এর product কিনতে পারবে, কিন্তু প্রত্যেক seller নিজের অংশের order, shipment এবং earning আলাদাভাবে manage করতে পারবে।

এরপর চাইলে এই architecture-এর উপর **Django 6 + DRF দিয়ে সম্পূর্ণ production-grade `models.py` files**, `BaseModel`, custom managers, constraints/indexes, `on_delete` কেন কোথায় কোনটা হবে, এবং **ER diagram-style relationship** একসাথে ধাপে ধাপে বানানো যায়।


---

# User model 

```py
last_login_ip = models.GenericIPAddressField(
        null=True,
        blank=True
    )

```

### find


`last_login_ip` Django নিজে automatically fill করবে না। Login করার সময় **request থেকে user's IP বের করে `User.last_login_ip`-তে save** করতে হবে।

DRF + JWT project হলে সবচেয়ে ভালো জায়গা হলো **login view / serializer**।

### 1. IP বের করার helper

```python
def get_client_ip(request):
    x_forwarded_for = request.META.get("HTTP_X_FORWARDED_FOR")

    if x_forwarded_for:
        # proxy/load balancer থাকলে প্রথম IP সাধারণত client IP
        ip = x_forwarded_for.split(",")[0].strip()
    else:
        ip = request.META.get("REMOTE_ADDR")

    return ip
```

### 2. Login-এর সময় save

যদি তোমার নিজের login API থাকে:

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from django.contrib.auth import authenticate

class LoginView(APIView):

    def post(self, request):

        email = request.data.get("email")
        password = request.data.get("password")

        user = authenticate(
            request,
            username=email,
            password=password
        )

        if user is None:
            return Response(
                {"detail": "Invalid credentials"},
                status=401
            )

        # IP বের করা
        ip = get_client_ip(request)

        # User-এর last login IP update
        user.last_login_ip = ip
        user.save(update_fields=["last_login_ip"])

        return Response({
            "message": "Login successful"
        })
```

তাহলে database:

```text
User
--------------------------------
email: atiar@example.com
last_login_ip: 192.168.1.10
```

পরেরবার অন্য IP থেকে login করলে:

```text
last_login_ip = নতুন IP
```

অর্থাৎ এটা **শুধু সর্বশেষ login-এর IP** রাখবে।

---

### 3. কিন্তু production-এ একটা বিষয় গুরুত্বপূর্ণ

যদি তোমার application থাকে:

```text
User
 ↓
Cloudflare / Nginx / Load Balancer
 ↓
Django
```

তাহলে:

```python
request.META["REMOTE_ADDR"]
```

সবসময় আসল user's IP নাও হতে পারে। Proxy configuration অনুযায়ী `X-Forwarded-For` handle করতে হবে।

---

### 4. আরেকটা better production design

`last_login_ip` শুধু User table-এ রাখলে তুমি জানতে পারবে:

> সর্বশেষ কোন IP থেকে login করেছে?

কিন্তু জানতে পারবে না:

> গত ১০ বার কোন কোন IP থেকে login করেছে?

সেজন্য আলাদা model করা যায়:

```python
class LoginHistory(models.Model):

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="login_history"
    )

    ip_address = models.GenericIPAddressField()

    user_agent = models.TextField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

তখন login হলে:

```python
LoginHistory.objects.create(
    user=user,
    ip_address=ip,
    user_agent=request.META.get("HTTP_USER_AGENT", "")
)

user.last_login_ip = ip
user.save(update_fields=["last_login_ip"])
```

তাহলে:

```text
User
 └── last_login_ip
        ↓
     103.45.x.x


LoginHistory
 ├── 103.45.x.x   → Sep 24
 ├── 103.46.x.x   → Sep 20
 ├── 192.168.x.x  → Sep 18
 └── 103.45.x.x   → Sep 15
```

**তোমার multi-vendor e-commerce production project-এর জন্য আমি `last_login_ip` + `LoginHistory` দুটোই রাখার পক্ষে**, কারণ `last_login_ip` quick access-এর জন্য এবং `LoginHistory` security/audit-এর জন্য।

হ্যাঁ—**checkout/order করার সময় customer-এর address নেওয়া উচিত**, কিন্তু production-grade e-commerce-এ একটা গুরুত্বপূর্ণ design আছে:

> **Customer-এর saved `Address` থাকবে, কিন্তু Order-এর জন্য address-এর একটা snapshot আলাদাভাবে সংরক্ষণ করা উচিত।**

### কেন?

ধরো customer আগে address save করল:

```text
Address
---------------------------
Name: Atiar Rahman
Phone: 017xxxxxxxx
City: Dhaka
Address: Mirpur, Dhaka
```

আজ order করল।

তারপর কাল সে নিজের saved address পরিবর্তন করল:

```text
City: Rajbari
Address: Goalanda, Rajbari
```

তাহলে আগের order-এর delivery address **পরিবর্তন হয়ে যাওয়া উচিত না**।

তাই:

```text
Customer
   │
   └── Address
          │
          │ checkout-এর সময়
          ▼
        Order
          │
          └── Shipping Address Snapshot
```

### তোমার `Order` model-এ এভাবে রাখা ভালো

আমি আগের model-এর:

```python
shipping_address = models.ForeignKey(
    Address,
    on_delete=models.PROTECT
)
```

এর বদলে production design-এ **snapshot fields** রাখার পরামর্শ দেব:

```python
class Order(models.Model):

    customer = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="orders"
    )

    shipping_name = models.CharField(
        max_length=150
    )

    shipping_phone = models.CharField(
        max_length=20
    )

    shipping_address_line_1 = models.CharField(
        max_length=255
    )

    shipping_address_line_2 = models.CharField(
        max_length=255,
        blank=True
    )

    shipping_city = models.CharField(
        max_length=100
    )

    shipping_state = models.CharField(
        max_length=100,
        blank=True
    )

    shipping_postal_code = models.CharField(
        max_length=20
    )

    shipping_country = models.CharField(
        max_length=100
    )

    # amount/status...
```

### Checkout flow

```text
1. Customer saved address select করবে
             ↓
2. Checkout
             ↓
3. Backend Address validate করবে
             ↓
4. Address-এর data copy হবে Order-এ
             ↓
5. Order তৈরি হবে
```

যেমন:

```python
address = Address.objects.get(
    id=address_id,
    user=request.user
)

order = Order.objects.create(
    customer=request.user,

    shipping_name=address.full_name,
    shipping_phone=address.phone_number,
    shipping_address_line_1=address.address_line_1,
    shipping_address_line_2=address.address_line_2,
    shipping_city=address.city,
    shipping_state=address.state,
    shipping_postal_code=address.postal_code,
    shipping_country=address.country,

    # ...
)
```

### তাহলে Address model-এর কাজ কী?

```text
Address
   ↓
Customer-এর reusable saved addresses

Order.shipping_*
   ↓
এই নির্দিষ্ট order-এর historical delivery address
```

এটা production e-commerce-এর জন্য গুরুত্বপূর্ণ কারণ **Order হলো historical record**। Customer পরে address edit/delete করলেও পুরোনো order-এর invoice, shipment এবং delivery information একই থাকবে।

আর একটা জিনিস: **billing address** আর **shipping address** আলাদা হতে পারে। তাই production project-এ `billing_*` snapshot fields-ও রাখা ভালো।
হ্যাঁ, **checkout-এর সময় address নেওয়া অবশ্যই রাখা উচিত**। তবে সবচেয়ে ভালো design হলো **দুটোই রাখা**:

### Recommended flow

```text
Customer
   │
   ├── Saved Address 1
   ├── Saved Address 2
   └── Saved Address 3
            │
            ▼
        Checkout
            │
      ┌─────┴─────┐
      │           │
Saved Address   New Address
      │           │
      └─────┬─────┘
            ▼
          Order
            │
            ▼
   Shipping Address Snapshot
```

### Checkout UI

Customer checkout করার সময়:

```text
Shipping Address

○ Home
  Atiar Rahman
  Dhaka, Bangladesh

○ Office
  Atiar Rahman
  Uttara, Dhaka

○ Use a new address
  [Name]
  [Phone]
  [Address]
  [City]
  [Postal Code]
```

তারপর backend:

```python
POST /api/orders/
```

```json
{
    "address_id": 12
}
```

যদি saved address ব্যবহার করে।

অথবা:

```json
{
    "shipping_name": "Atiar Rahman",
    "shipping_phone": "017xxxxxxx",
    "shipping_address_line_1": "Mirpur",
    "shipping_city": "Dhaka",
    "shipping_postal_code": "1216",
    "shipping_country": "Bangladesh"
}
```

যদি নতুন address হয়।

### সবচেয়ে গুরুত্বপূর্ণ

Order তৈরি হওয়ার সময় address-এর data **Order-এর মধ্যে copy/snapshot** করে রাখবে।

```text
Address table
     ↓
checkout
     ↓
Order.shipping_name
Order.shipping_phone
Order.shipping_address
Order.shipping_city
...
```

কারণ পরে customer তার saved address পরিবর্তন করলেও **পুরোনো Order-এর address পরিবর্তন হওয়া উচিত না**।

তাই তোমার multi-vendor e-commerce-এর জন্য আমি এই approach রাখব:

**Saved Address + Checkout-time New Address + Order Address Snapshot** — তিনটিই।


হ্যাঁ, **checkout-এর সময় address নেওয়াই better**। User-কে purchase করার আগে বাধ্যতামূলকভাবে address setup করানো দরকার নেই।

Production flow:

```text
Register
   ↓
Browse Products
   ↓
Add to Cart
   ↓
Checkout
   ↓
Select saved address
   OR
Enter new address
   ↓
Save as default? → Yes/No
   ↓
Create Order
```

### Different place থেকে order করলে

Customer যদি Dhaka থেকে একবার এবং Rajbari থেকে আরেকবার order করে:

```text
Checkout 1
→ New Address: Dhaka
→ Save Address ✓

Checkout 2
→ New Address: Rajbari
→ Save Address ✓
```

তার saved addresses হবে:

```text
Home → Dhaka
Village Home → Rajbari
```

পরেরবার শুধু select করবে।

### তাই আমার recommendation

**Address আগে setup করা optional। Checkout-এর সময় address নেওয়া mandatory।**

আর যদি নতুন address দেয়, তাকে:

> `Save this address for future orders`

option দাও।

এটাই তোমার multi-vendor e-commerce-এর জন্য clean UX + scalable design।


হ্যাঁ। তোমার সিদ্ধান্ত অনুযায়ী **Address আলাদা model থাকবে**, আর checkout-এর সময় নতুন address নেওয়া যাবে। Order তৈরি হওয়ার সময় address-এর data **snapshot** হবে।

### Core models

```text id="m1p0a7"
User
Profile
Address
SellerProfile

Category
Product
ProductImage
ProductVariant
Inventory

Cart
CartItem
Wishlist

Order
SellerOrder
OrderItem

Payment
Shipment

Review
Coupon
CouponUsage
SellerCommission
```

### Address model

```python id="4f8k2m"
class Address(BaseModel):

    class AddressType(models.TextChoices):
        HOME = "HOME", "Home"
        OFFICE = "OFFICE", "Office"
        OTHER = "OTHER", "Other"

    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="addresses"
    )

    address_type = models.CharField(
        max_length=20,
        choices=AddressType.choices,
        default=AddressType.HOME
    )

    full_name = models.CharField(max_length=150)

    phone_number = models.CharField(max_length=20)

    address_line_1 = models.CharField(max_length=255)

    address_line_2 = models.CharField(
        max_length=255,
        blank=True
    )

    city = models.CharField(max_length=100)

    state = models.CharField(
        max_length=100,
        blank=True
    )

    postal_code = models.CharField(max_length=20)

    country = models.CharField(
        max_length=100,
        default="Bangladesh"
    )

    is_default = models.BooleanField(default=False)
```

### Order-এ Address FK + Snapshot

আমি দুটোই রাখব:

```python id="z8nq2c"
class Order(BaseModel):

    customer = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="orders"
    )

    # যে saved address ব্যবহার করা হয়েছিল
    address = models.ForeignKey(
        Address,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="orders"
    )

    # Snapshot
    shipping_name = models.CharField(max_length=150)
    shipping_phone = models.CharField(max_length=20)
    shipping_address_line_1 = models.CharField(max_length=255)
    shipping_address_line_2 = models.CharField(
        max_length=255,
        blank=True
    )
    shipping_city = models.CharField(max_length=100)
    shipping_state = models.CharField(
        max_length=100,
        blank=True
    )
    shipping_postal_code = models.CharField(max_length=20)
    shipping_country = models.CharField(max_length=100)

    # amount/status...
```

**Final flow:**

```text
User
 └── Address (0, 1, or many)
          ↓
      Checkout
       ↙     ↘
Saved       New Address
Address          ↓
   └──────→ Order
              ├── address FK
              └── shipping_* snapshot
```

এভাবে user **কেনার আগে address setup করতে বাধ্য নয়**, আবার চাইলে address save করে পরের order-এ দ্রুত ব্যবহার করতে পারবে।


হ্যাঁ, **permanently/future use করতে চাইলে `Address` model-এ save করা উচিত।** তবে user-কে বাধ্য করা উচিত না।

Best design:

```text
Checkout
   │
   ├── Existing Address select
   │
   └── New Address
          │
          └── "Save this address" ☑
```

যদি checkbox select করে:

```python
Address.objects.create(
    user=request.user,
    ...
)
```

না করলে শুধু ওই order-এর জন্য:

```text
Order.shipping_* → snapshot
```

### Final rule

* 🟢 **Future use করতে চাইলে** → `Address` table-এ save
* 🟢 **শুধু current order-এর জন্য** → `Order`-এ snapshot
* 🟢 **Default address** → `Address.is_default = True`
* 🔴 User-কে purchase-এর আগে address create করতে বাধ্য করবে না

এটাই তোমার project-এর জন্য clean production design।


---
# productvariant model

```py
sku = models.CharField(
        max_length=100,
        unique=True
    )
```

`ProductVariant`-এর `sku` হলো **প্রতিটি specific variant-কে uniquely identify করার জন্য একটি code**।

ধরো Product:

```text
T-Shirt
```

এর variants:

```text
Size: M, Color: Black
Size: L, Color: Black
Size: M, Color: White
```

তাহলে প্রত্যেকটার আলাদা SKU থাকবে:

```text
TSH-BLK-M
TSH-BLK-L
TSH-WHT-M
```

### কেন দরকার?

SKU দিয়ে system সহজে বুঝবে **ঠিক কোন variant-এর stock/order/sale হচ্ছে**।

```text
Product
└── T-Shirt

    Variant 1
    ├── Size: M
    ├── Color: Black
    ├── SKU: TSH-BLK-M
    └── Stock: 20

    Variant 2
    ├── Size: L
    ├── Color: Black
    ├── SKU: TSH-BLK-L
    └── Stock: 15
```

যখন customer `M + Black` কিনবে:

```python
ProductVariant.objects.get(
    sku="TSH-BLK-M"
)
```

তখন নির্দিষ্ট variant-এর stock কমাবে।

### `Product`-এও SKU কেন ছিল?

যদি product-এর কোনো variant না থাকে:

```text
Product: Logitech Mouse
SKU: LOG-MOUSE-001
```

আর variant থাকলে:

```text
Product: T-Shirt
    Variant → TSH-BLK-M
    Variant → TSH-BLK-L
    Variant → TSH-WHT-M
```

অর্থাৎ:

**Product SKU = পুরো product identify করে**

**Variant SKU = নির্দিষ্ট variation identify করে**

আর production system-এ `ProductVariant.sku`-কে `unique=True` রাখা ভালো।


---
# update Productvariant model

তোমার **multi-vendor production e-commerce** architecture ধরে `ProductVariant` এবং `Inventory` আমি এভাবে final করতাম।

### 1. `ProductVariant`

```python
from django.db import models
from core.models import BaseModel


class ProductVariant(BaseModel):
    product = models.ForeignKey(
        "products.Product",
        on_delete=models.CASCADE,
        related_name="variants",
    )

    sku = models.CharField(
        max_length=100,
        db_index=True,
    )

    name = models.CharField(
        max_length=150,
        help_text="Example: Black / Medium",
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_active = models.BooleanField(default=True)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["product", "sku"],
                name="unique_product_variant_sku",
            )
        ]
        indexes = [
            models.Index(fields=["product", "is_active"]),
        ]

    def __str__(self):
        return f"{self.product.name} - {self.name}"
```

### 2. `Warehouse`

যেহেতু `Inventory` warehouse অনুযায়ী stock রাখবে:

```python
class Warehouse(BaseModel):
    seller = models.ForeignKey(
        "sellers.SellerProfile",
        on_delete=models.CASCADE,
        related_name="warehouses",
    )

    name = models.CharField(max_length=150)

    address = models.TextField()

    city = models.CharField(max_length=100)

    is_active = models.BooleanField(default=True)

    def __str__(self):
        return self.name
```

### 3. `Inventory`

```python
class Inventory(BaseModel):
    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.CASCADE,
        related_name="inventories",
    )

    warehouse = models.ForeignKey(
        Warehouse,
        on_delete=models.CASCADE,
        related_name="inventories",
    )

    quantity = models.PositiveIntegerField(default=0)

    reserved_quantity = models.PositiveIntegerField(default=0)

    reorder_level = models.PositiveIntegerField(default=5)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["variant", "warehouse"],
                name="unique_variant_warehouse_inventory",
            )
        ]

        indexes = [
            models.Index(fields=["variant", "warehouse"]),
        ]

    @property
    def available_quantity(self):
        return self.quantity - self.reserved_quantity

    def __str__(self):
        return f"{self.variant.sku} - {self.warehouse.name}"
```

### সম্পর্কটা হবে

```text
Product
   │
   └── ProductVariant
          │
          ├── Inventory ── Warehouse
          │                  └── Seller
          │
          └── Inventory ── Warehouse
```

ধরো:

```text
Product: T-Shirt

Variants:
 ├── Black / M
 │     SKU: TSH-BLK-M
 │
 ├── Black / L
 │     SKU: TSH-BLK-L
 │
 └── White / M
       SKU: TSH-WHT-M
```

Inventory:

```text
TSH-BLK-M
 ├── Dhaka Warehouse       20
 └── Chittagong Warehouse  10

TSH-BLK-L
 └── Dhaka Warehouse       15
```

তাহলে:

```python
variant = ProductVariant.objects.get(sku="TSH-BLK-M")

variant.inventories.all()
```

দিলে:

```text
Dhaka       → 20
Chittagong  → 10
```

আর total stock:

```python
from django.db.models import Sum

total = variant.inventories.aggregate(
    total=Sum("quantity")
)["total"] or 0
```

**সবচেয়ে গুরুত্বপূর্ণ সিদ্ধান্ত:** `ProductVariant`-এ `stock_quantity` রাখছি না। Stock-এর **single source of truth হলো `Inventory`**। ফলে একই stock দুই জায়গায় রাখার কারণে inconsistency হবে না।

---
হ্যাঁ, আগে আমরা যেটা রেখেছিলাম সেটা ছিল:

```text
Product
   │
   ├── ProductVariant
   │      └── stock_quantity
   │
   └── Inventory
          └── quantity
```

কিন্তু **production multi-vendor e-commerce** হিসেবে এটা একটু problematic, কারণ একই stock দুই জায়গায় রাখা হচ্ছে।

### কেন সমস্যা?

ধরি:

```text
Product: T-Shirt

Variant: Black / M
ProductVariant.stock_quantity = 20

Inventory.quantity = 20
```

এখন customer 2টা কিনল।

যদি ভুল করে শুধু:

```python
variant.stock_quantity -= 2
```

করা হয়, তাহলে:

```text
Variant stock = 18
Inventory stock = 20
```

দুই জায়গায় দুই রকম stock হয়ে গেল।

---

## আমার final recommendation

### `ProductVariant`

```python
class ProductVariant(BaseModel):
    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="variants"
    )

    sku = models.CharField(
        max_length=100,
        db_index=True
    )

    name = models.CharField(
        max_length=150
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    is_active = models.BooleanField(
        default=True
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["product", "sku"],
                name="unique_product_variant_sku"
            )
        ]

    def __str__(self):
        return f"{self.product.name} - {self.name}"
```

এখানে **`stock_quantity` থাকবে না**।

---

### `Inventory`

যদি তোমার একাধিক warehouse থাকে:

```python
class Inventory(BaseModel):
    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.CASCADE,
        related_name="inventories"
    )

    warehouse = models.ForeignKey(
        Warehouse,
        on_delete=models.CASCADE,
        related_name="inventories"
    )

    quantity = models.PositiveIntegerField(
        default=0
    )

    reserved_quantity = models.PositiveIntegerField(
        default=0
    )

    reorder_level = models.PositiveIntegerField(
        default=5
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["variant", "warehouse"],
                name="unique_variant_warehouse"
            )
        ]

    @property
    def available_quantity(self):
        return self.quantity - self.reserved_quantity
```

### তাহলে structure হবে

```text
T-Shirt
│
├── Black / M
│     │
│     ├── Dhaka Warehouse
│     │      quantity = 20
│     │
│     └── Chittagong Warehouse
│            quantity = 10
│
├── Black / L
│     │
│     └── Dhaka Warehouse
│            quantity = 15
│
└── White / M
       │
       └── Dhaka Warehouse
              quantity = 8
```

অর্থাৎ:

**ProductVariant = কোন ধরনের product**

```text
Black / M
Black / L
White / M
```

**Inventory = সেই variant কোথায় কত আছে**

```text
Black/M → Dhaka = 20
Black/M → Chittagong = 10
```

আর:

```python
available_quantity = quantity - reserved_quantity
```

এটাই রাখলে architecture পরিষ্কার থাকবে।

**সুতরাং তোমার আগের `ProductVariant.stock_quantity` + `Inventory.product` design-এর বদলে আমি `ProductVariant → Inventory → Warehouse` design-টাই final করব।**

---
# main order and sellerorder and orderitem

হ্যাঁ। এখানে **`Order` আর `SellerOrder` কেন আলাদা**, সেটা বুঝলে পুরো multi-vendor checkout architecture পরিষ্কার হয়ে যাবে।

## 1. সহজভাবে ধারণাটা

Customer একবার **Checkout** করবে।

ধরো cart:

```text
Customer: Atiar

Cart
├── iPhone       → Seller A
├── Laptop       → Seller A
└── T-Shirt      → Seller B
```

Customer-এর কাছে এটা **একটা order**।

তাই:

```text
Order #1001
```

কিন্তু Seller A এবং Seller B আলাদাভাবে তাদের product manage করবে।

তাই Order-কে seller অনুযায়ী ভাগ করা হবে:

```text
Order #1001
│
├── SellerOrder #1
│     Seller A
│     ├── iPhone
│     └── Laptop
│
└── SellerOrder #2
      Seller B
      └── T-Shirt
```

---

# 2. `Order` কী?

`Order` হলো **customer-এর পুরো checkout-এর record**।

```python
class Order(models.Model):

    order_number = models.CharField(
        max_length=50,
        unique=True
    )

    customer = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="orders"
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    shipping_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING
    )
```

ধরো:

```text
Order #1001

Customer: Atiar

Subtotal:       ৳85,000
Shipping:       ৳200
Discount:       ৳500
----------------------
Total:          ৳84,700
```

এটা customer-এর **পুরো order**।

---

# 3. `SellerOrder` কী?

`SellerOrder` হলো মূল Order-এর ভিতরে **একজন seller-এর অংশ**।

ধরো:

```text
Order #1001

Seller A:
    iPhone       ৳60,000
    Laptop       ৳20,000

Seller B:
    T-Shirt      ৳5,000
```

তাহলে database-এ:

```text
Order #1001
│
├── SellerOrder #5001
│      Seller A
│      subtotal = ৳80,000
│
└── SellerOrder #5002
       Seller B
       subtotal = ৳5,000
```

অর্থাৎ:

```text
Order
  ↓
SellerOrder
  ↓
OrderItem
```

---

# 4. `OrderItem` কোথায়?

এটাই সবচেয়ে গুরুত্বপূর্ণ।

`SellerOrder`-এর ভিতরে actual product থাকবে `OrderItem` হিসেবে।

```text
Order #1001
│
├── SellerOrder #5001
│     Seller A
│     │
│     ├── OrderItem
│     │     iPhone × 1
│     │
│     └── OrderItem
│           Laptop × 1
│
└── SellerOrder #5002
      Seller B
      │
      └── OrderItem
            T-Shirt × 2
```

Model:

```python
class OrderItem(models.Model):

    seller_order = models.ForeignKey(
        SellerOrder,
        on_delete=models.CASCADE,
        related_name="items"
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT
    )

    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.PROTECT,
        null=True,
        blank=True
    )

    product_name = models.CharField(
        max_length=255
    )

    sku = models.CharField(
        max_length=100
    )

    quantity = models.PositiveIntegerField()

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    total_price = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )
```

---

# 5. বাস্তব Example

ধরো Atiar-এর cart:

```text
iPhone
Seller A
Price = 60,000
Qty = 1

Laptop
Seller A
Price = 20,000
Qty = 1

T-Shirt
Seller B
Price = 2,500
Qty = 2
```

Checkout করার পরে:

### Main Order

```text
Order #1001
Customer: Atiar

Subtotal = 85,000
Shipping = 200
Discount = 500
Total = 84,700
```

### SellerOrder 1

```text
SellerOrder #5001

Order: Order #1001
Seller: Seller A

Items:
    iPhone     × 1 = 60,000
    Laptop     × 1 = 20,000

Subtotal = 80,000
```

### SellerOrder 2

```text
SellerOrder #5002

Order: Order #1001
Seller: Seller B

Items:
    T-Shirt × 2 = 5,000

Subtotal = 5,000
```

Database relationship:

```text
Order #1001
│
│
├──────── SellerOrder #5001
│              │
│              ├── iPhone × 1
│              └── Laptop × 1
│
└──────── SellerOrder #5002
               │
               └── T-Shirt × 2
```

---

# 6. তাহলে Seller A কী দেখতে পাবে?

Seller A তার dashboard-এ:

```text
Order #1001
--------------------
iPhone   × 1
Laptop   × 1

Subtotal: ৳80,000
Status: Processing
```

সে **Seller B-এর T-Shirt দেখতে পাবে না**।

কারণ:

```python
SellerOrder.objects.filter(
    seller=request.user.seller_profile
)
```

দিয়ে নিজের `SellerOrder`-গুলো বের করবে।

---

# 7. Customer কী দেখতে পাবে?

Customer পুরো order দেখতে পাবে:

```text
Order #1001

Seller A
    iPhone × 1
    Laptop × 1
    Status: Shipped

Seller B
    T-Shirt × 2
    Status: Processing

Total: ৳84,700
```

এখানে Seller A-এর order shipped হতে পারে, কিন্তু Seller B এখনো processing হতে পারে।

এই কারণেই শুধু:

```text
Order.status
```

দিয়ে multi-vendor order manage করা যথেষ্ট নয়।

তোমার দরকার:

```text
Order.status
+
SellerOrder.status
```

---

# 8. Shipping-ও কেন SellerOrder-এর সাথে?

ধরো:

```text
Seller A → Pathao → Tracking A123
Seller B → Steadfast → Tracking B456
```

তাহলে দুই seller-এর আলাদা shipment হতে পারে।

তাই:

```text
SellerOrder
    ↓
Shipment
```

ভালো architecture।

```text
Order #1001
│
├── SellerOrder A
│      └── Shipment A
│            Tracking: A123
│
└── SellerOrder B
       └── Shipment B
             Tracking: B456
```

---

## সবচেয়ে সহজে মনে রাখো

```text
Order
= Customer-এর পুরো checkout

SellerOrder
= ঐ checkout-এর একজন seller-এর অংশ

OrderItem
= seller-এর কোন product কত quantity
```

অর্থাৎ:

```text
1 Customer
    ↓
1 Order
    ↓
Multiple SellerOrder
    ↓
Multiple OrderItem
```

**এই architecture-টাই তোমার multi-vendor e-commerce-এর জন্য রাখা উচিত।**



---

# `Coupon` আর `CouponUsage`-এর কাজ আলাদা। সহজভাবে:

* **Coupon** = coupon-এর rules/configuration
* **CouponUsage** = কে, কোন order-এ, কখন coupon ব্যবহার করেছে তার history

ধরো coupon:

```text
Code: SAVE20
Discount: 20%
Minimum Order: ৳1,000
Maximum Discount: ৳500
Usage Limit: 1,000
```

## 1. `Coupon` কী করবে?

Admin coupon তৈরি করবে:

```python
coupon = Coupon.objects.create(
    code="SAVE20",
    discount_percentage=20,
    minimum_order_amount=1000,
    maximum_discount=500,
    usage_limit=1000,
    starts_at=...,
    expires_at=...,
)
```

এখানে এখনো কেউ coupon ব্যবহার করেনি।

```text
Coupon
--------------------------------
SAVE20
20%
Minimum: ৳1,000
Maximum discount: ৳500
Usage limit: 1,000
Used: 0
```

---

# 2. Customer checkout করবে

ধরো Atiar-এর order:

```text
Subtotal = ৳3,000

Coupon = SAVE20
```

Backend প্রথমে check করবে:

```text
Coupon exists?
        ↓
is_active?
        ↓
starts_at পার হয়েছে?
        ↓
expires_at পার হয়নি?
        ↓
minimum_order_amount পূরণ হয়েছে?
        ↓
usage_limit শেষ হয়নি?
        ↓
এই user আগে ব্যবহার করেছে কি না?
        ↓
সব ঠিক?
        ↓
Discount calculate
```

20% of ৳3,000:

```text
3000 × 20% = ৳600
```

কিন্তু maximum discount ৳500।

তাই:

```text
Discount = ৳500
```

Order:

```text
Subtotal = ৳3,000
Discount = ৳500
Total = ৳2,500
```

---

# 3. এরপর `CouponUsage` তৈরি হবে

Order successfully তৈরি হওয়ার পরে:

```python
CouponUsage.objects.create(
    coupon=coupon,
    user=request.user,
    order=order
)
```

Database:

```text
CouponUsage
------------------------------------------------
coupon     user      order       used_at
SAVE20     Atiar     #1001       2026-09-25
```

এর মানে:

> Atiar `SAVE20` coupon ব্যবহার করে Order #1001 করেছে।

---

# 4. তাহলে `used_count` কেন আছে?

`Coupon.used_count` দিয়ে মোট কতবার coupon ব্যবহার হয়েছে সেটা দ্রুত জানা যায়।

প্রথমে:

```text
Coupon.used_count = 0
```

Atiar ব্যবহার করল:

```text
used_count = 1
```

আরেকজন ব্যবহার করল:

```text
used_count = 2
```

এভাবে:

```text
SAVE20

usage_limit = 1000
used_count  = 350
```

মানে এখনো:

```text
1000 - 350 = 650
```

বার ব্যবহার করা যাবে।

---

# 5. তাহলে `CouponUsage` না রেখে শুধু `used_count` রাখলে হবে?

**হবে না**, production system-এ।

কারণ `used_count` শুধু বলে:

```text
350 times used
```

কিন্তু বলে না:

```text
কে ব্যবহার করেছে?
কোন order-এ?
কখন ব্যবহার করেছে?
```

`CouponUsage` এগুলো রাখে।

```text
Coupon
   │
   └── CouponUsage
          ├── User
          └── Order
```

---

# 6. একই user আবার ব্যবহার করতে পারবে?

এটা business rule-এর ওপর নির্ভর করে।

যদি coupon হয়:

```text
SAVE20
প্রতি customer একবার
```

তাহলে constraint দিতে পারো:

```python
class CouponUsage(models.Model):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT,
        related_name="usages"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="coupon_usages"
    )

    order = models.ForeignKey(
        Order,
        on_delete=models.PROTECT,
        related_name="coupon_usages"
    )

    used_at = models.DateTimeField(
        auto_now_add=True
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["coupon", "user"],
                name="unique_coupon_per_user"
            )
        ]
```

তাহলে:

```text
SAVE20 + Atiar
```

একবারের বেশি ব্যবহার করতে পারবে না।

---

# 7. কিন্তু সব coupon কি একবারই ব্যবহারযোগ্য?

না।

ধরো:

### Coupon A

```text
SAVE20
Per user: 1 time
```

### Coupon B

```text
FREESHIP
Per user: unlimited
```

তখন `Coupon` model-এ একটা field রাখা ভালো:

```python
usage_limit_per_user = models.PositiveIntegerField(
    null=True,
    blank=True
)
```

অর্থ:

```text
null = unlimited
1    = প্রতি user একবার
2    = প্রতি user দুইবার
```

তাহলে `UniqueConstraint(coupon, user)` সব coupon-এর জন্য দেওয়া ঠিক হবে না।

---

# 8. আমি তোমার production model-এ এটা রাখব

```python
class Coupon(models.Model):

    code = models.CharField(
        max_length=50,
        unique=True
    )

    description = models.TextField(
        blank=True
    )

    discount_percentage = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        null=True,
        blank=True
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True
    )

    minimum_order_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0
    )

    maximum_discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True
    )

    usage_limit = models.PositiveIntegerField(
        null=True,
        blank=True
    )

    usage_limit_per_user = models.PositiveIntegerField(
        null=True,
        blank=True
    )

    used_count = models.PositiveIntegerField(
        default=0
    )

    starts_at = models.DateTimeField()

    expires_at = models.DateTimeField()

    is_active = models.BooleanField(
        default=True
    )
```

আর:

```python
class CouponUsage(models.Model):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT,
        related_name="usages"
    )

    user = models.ForeignKey(
        User,
        on_delete=models.PROTECT,
        related_name="coupon_usages"
    )

    order = models.ForeignKey(
        Order,
        on_delete=models.PROTECT,
        related_name="coupon_usages"
    )

    used_at = models.DateTimeField(
        auto_now_add=True
    )
```

### পুরো flow

```text
Customer enters "SAVE20"
             ↓
       Find Coupon
             ↓
       Validate Coupon
             ↓
       Calculate Discount
             ↓
       Create Order
             ↓
     Create CouponUsage
             ↓
     Increase used_count
```

একটা গুরুত্বপূর্ণ production বিষয় হলো **checkout-এর সময় `transaction.atomic()` + row locking** ব্যবহার করা, যাতে একই সময়ে অনেক customer coupon ব্যবহার করলে `usage_limit` অতিক্রম না করে।


---
# Serializer
হ্যাঁ। তোমার এখন পর্যন্ত তৈরি করা **multi-vendor e-commerce-এর সব model** ধরে DRF serializers সাজালে structureটা এমন হবে।

আমি এখানে **ModelSerializer + nested read serializer + write serializer** আলাদা রাখছি। Production project-এ এটাই বেশি maintainable।

## 1. User / Profile / Address

```python
# serializers.py

from rest_framework import serializers

from .models import (
    User,
    Profile,
    Address,
    SellerProfile,
    SellerBankAccount,
    Category,
    Product,
    ProductImage,
    ProductVariant,
    Warehouse,
    Inventory,
    Cart,
    CartItem,
    Wishlist,
    Order,
    SellerOrder,
    OrderItem,
    Payment,
    Shipment,
    Review,
    Coupon,
    CouponUsage,
    SellerCommission,
)
```

### User

```python
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = [
            "id",
            "email",
            "first_name",
            "last_name",
            "phone_number",
            "role",
            "is_email_verified",
            "is_phone_verified",
            "last_login_ip",
            "is_active",
            "created_at",
            "updated_at",
        ]
        read_only_fields = [
            "id",
            "role",
            "is_email_verified",
            "is_phone_verified",
            "last_login_ip",
            "created_at",
            "updated_at",
        ]
```

### Profile

```python
class ProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = Profile
        fields = "__all__"

        read_only_fields = [
            "id",
            "user",
            "created_at",
            "updated_at",
        ]
```

### Address

```python
class AddressSerializer(serializers.ModelSerializer):
    class Meta:
        model = Address
        fields = [
            "id",
            "address_type",
            "full_name",
            "phone_number",
            "address_line_1",
            "address_line_2",
            "city",
            "state",
            "postal_code",
            "country",
            "is_default",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
            "updated_at",
        ]
```

`user` request থেকে নেওয়া হবে, তাই frontend থেকে `user_id` পাঠানোর দরকার নেই।

---

# 2. Seller

### SellerProfile

```python
class SellerProfileSerializer(serializers.ModelSerializer):
    user = UserSerializer(read_only=True)

    class Meta:
        model = SellerProfile
        fields = [
            "id",
            "user",
            "store_name",
            "store_slug",
            "logo",
            "banner",
            "description",
            "business_name",
            "business_registration_number",
            "tax_identification_number",
            "status",
            "commission_rate",
            "is_verified",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "user",
            "status",
            "is_verified",
            "created_at",
            "updated_at",
        ]
```

### Bank Account

```python
class SellerBankAccountSerializer(serializers.ModelSerializer):
    class Meta:
        model = SellerBankAccount
        fields = [
            "id",
            "account_name",
            "bank_name",
            "account_number",
            "branch_name",
            "routing_number",
            "is_primary",
            "is_verified",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "is_verified",
            "created_at",
            "updated_at",
        ]
```

---

# 3. Category

```python
class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = [
            "id",
            "name",
            "slug",
            "description",
            "image",
            "parent",
            "is_active",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
            "updated_at",
        ]
```

---

# 4. Product

এখানে product details-এর সাথে variants/images read করতে পারো।

```python
class ProductImageSerializer(serializers.ModelSerializer):
    class Meta:
        model = ProductImage
        fields = [
            "id",
            "image",
            "alt_text",
            "sort_order",
            "is_primary",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
            "updated_at",
        ]
```

### Variant

```python
class ProductVariantSerializer(serializers.ModelSerializer):
    available_quantity = serializers.SerializerMethodField()

    class Meta:
        model = ProductVariant
        fields = [
            "id",
            "product",
            "sku",
            "name",
            "price",
            "is_active",
            "available_quantity",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "available_quantity",
            "created_at",
            "updated_at",
        ]

    def get_available_quantity(self, obj):
        return sum(
            inventory.available_quantity
            for inventory in obj.inventories.all()
        )
```

এখানে যদি:

```text
Black/M
Dhaka = 20
Chittagong = 10
```

তাহলে API:

```json
{
    "id": "...",
    "sku": "TSH-BLK-M",
    "name": "Black / M",
    "price": "1200.00",
    "available_quantity": 30
}
```

---

# 5. Product Serializer

```python
class ProductSerializer(serializers.ModelSerializer):
    images = ProductImageSerializer(
        many=True,
        read_only=True
    )

    variants = ProductVariantSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = Product
        fields = [
            "id",
            "seller",
            "category",
            "name",
            "slug",
            "sku",
            "description",
            "short_description",
            "brand",
            "price",
            "discount_price",
            "weight",
            "is_active",
            "is_published",
            "images",
            "variants",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "seller",
            "created_at",
            "updated_at",
        ]
```

এতে Product API response হবে:

```text
Product
 ├── images[]
 └── variants[]
```

---

# 6. Warehouse

```python
class WarehouseSerializer(serializers.ModelSerializer):

    class Meta:
        model = Warehouse

        fields = [
            "id",
            "seller",
            "name",
            "address",
            "city",
            "is_active",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "seller",
            "created_at",
            "updated_at",
        ]
```

---

# 7. Inventory

```python
class InventorySerializer(serializers.ModelSerializer):

    available_quantity = serializers.ReadOnlyField()

    class Meta:
        model = Inventory

        fields = [
            "id",
            "variant",
            "warehouse",
            "quantity",
            "reserved_quantity",
            "available_quantity",
            "reorder_level",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "available_quantity",
            "created_at",
            "updated_at",
        ]
```

---

# 8. Cart

```python
class CartItemSerializer(serializers.ModelSerializer):

    total_price = serializers.SerializerMethodField()

    class Meta:
        model = CartItem

        fields = [
            "id",
            "product",
            "variant",
            "quantity",
            "total_price",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "total_price",
            "created_at",
            "updated_at",
        ]

    def get_total_price(self, obj):
        price = (
            obj.variant.price
            if obj.variant
            else obj.product.price
        )

        return price * obj.quantity
```

### Cart

```python
class CartSerializer(serializers.ModelSerializer):

    items = CartItemSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = Cart

        fields = [
            "id",
            "user",
            "items",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "user",
            "created_at",
            "updated_at",
        ]
```

---

# 9. Wishlist

```python
class WishlistSerializer(serializers.ModelSerializer):

    class Meta:
        model = Wishlist

        fields = [
            "id",
            "product",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
        ]
```

---

# 10. Order

এখানে nested structure দেখানো হবে।

```text
Order
 └── SellerOrders
       └── OrderItems
```

### OrderItem

```python
class OrderItemSerializer(serializers.ModelSerializer):

    class Meta:
        model = OrderItem

        fields = [
            "id",
            "product",
            "variant",
            "product_name",
            "sku",
            "quantity",
            "unit_price",
            "total_price",
        ]

        read_only_fields = [
            "id",
            "product_name",
            "sku",
            "unit_price",
            "total_price",
        ]
```

### SellerOrder

```python
class SellerOrderSerializer(serializers.ModelSerializer):

    items = OrderItemSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = SellerOrder

        fields = [
            "id",
            "order",
            "seller",
            "subtotal",
            "commission",
            "seller_amount",
            "status",
            "items",
        ]

        read_only_fields = [
            "id",
            "order",
            "seller",
            "subtotal",
            "commission",
            "seller_amount",
        ]
```

### Main Order

```python
class OrderSerializer(serializers.ModelSerializer):

    seller_orders = SellerOrderSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = Order

        fields = [
            "id",
            "order_number",
            "customer",
            "shipping_address",
            "subtotal",
            "shipping_cost",
            "discount",
            "total_amount",
            "status",
            "seller_orders",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "order_number",
            "customer",
            "subtotal",
            "shipping_cost",
            "discount",
            "total_amount",
            "status",
            "seller_orders",
            "created_at",
            "updated_at",
        ]
```

---

# 11. Payment

```python
class PaymentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Payment

        fields = [
            "id",
            "order",
            "transaction_id",
            "payment_method",
            "amount",
            "status",
            "paid_at",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "transaction_id",
            "status",
            "paid_at",
            "created_at",
        ]
```

Payment সাধারণত customer নিজে `status=PAID` পাঠাবে না। Payment gateway/backend সেট করবে।

---

# 12. Shipment

```python
class ShipmentSerializer(serializers.ModelSerializer):

    class Meta:
        model = Shipment

        fields = [
            "id",
            "seller_order",
            "courier_name",
            "tracking_number",
            "status",
            "shipped_at",
            "delivered_at",
        ]

        read_only_fields = [
            "id",
            "tracking_number",
            "shipped_at",
            "delivered_at",
        ]
```

---

# 13. Review

```python
class ReviewSerializer(serializers.ModelSerializer):

    class Meta:
        model = Review

        fields = [
            "id",
            "product",
            "user",
            "order_item",
            "rating",
            "title",
            "comment",
            "is_verified_purchase",
            "is_approved",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "user",
            "is_verified_purchase",
            "is_approved",
            "created_at",
            "updated_at",
        ]
```

---

# 14. Coupon

```python
class CouponSerializer(serializers.ModelSerializer):

    class Meta:
        model = Coupon

        fields = [
            "id",
            "code",
            "description",
            "discount_percentage",
            "discount_amount",
            "minimum_order_amount",
            "maximum_discount",
            "usage_limit",
            "usage_limit_per_user",
            "used_count",
            "starts_at",
            "expires_at",
            "is_active",
        ]

        read_only_fields = [
            "id",
            "used_count",
        ]
```

---

# 15. CouponUsage

```python
class CouponUsageSerializer(serializers.ModelSerializer):

    class Meta:
        model = CouponUsage

        fields = [
            "id",
            "coupon",
            "user",
            "order",
            "used_at",
        ]

        read_only_fields = [
            "id",
            "user",
            "order",
            "used_at",
        ]
```

`CouponUsage` customer সরাসরি create করবে না। Checkout logic-এর মাধ্যমে backend তৈরি করবে।

---

# 16. SellerCommission

```python
class SellerCommissionSerializer(serializers.ModelSerializer):

    class Meta:
        model = SellerCommission

        fields = [
            "id",
            "seller_order",
            "seller",
            "order_amount",
            "commission_rate",
            "commission_amount",
            "seller_earning",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "order_amount",
            "commission_rate",
            "commission_amount",
            "seller_earning",
            "created_at",
        ]
```

---

## সবচেয়ে গুরুত্বপূর্ণ architecture

Frontend-এর জন্য response ideally এমন হবে:

```json
{
    "id": 1,
    "order_number": "ORD-1001",
    "subtotal": "85000.00",
    "shipping_cost": "200.00",
    "discount": "500.00",
    "total_amount": "84700.00",

    "seller_orders": [
        {
            "id": 10,
            "seller": 5,
            "subtotal": "80000.00",
            "status": "SHIPPED",

            "items": [
                {
                    "product": 20,
                    "variant": 101,
                    "product_name": "iPhone",
                    "sku": "IPH-001",
                    "quantity": 1,
                    "unit_price": "60000.00",
                    "total_price": "60000.00"
                },
                {
                    "product": 21,
                    "variant": 102,
                    "product_name": "Laptop",
                    "sku": "LAP-001",
                    "quantity": 1,
                    "unit_price": "20000.00",
                    "total_price": "20000.00"
                }
            ]
        },

        {
            "id": 11,
            "seller": 8,
            "subtotal": "5000.00",
            "status": "PROCESSING",

            "items": [
                {
                    "product": 30,
                    "variant": 103,
                    "product_name": "T-Shirt",
                    "sku": "TSH-BLK-M",
                    "quantity": 2,
                    "unit_price": "2500.00",
                    "total_price": "5000.00"
                }
            ]
        }
    ]
}
```

এখানে একটা গুরুত্বপূর্ণ বিষয়: **সব model-এর জন্য একই serializer দিয়ে Create/Update/Read করার চেষ্টা করো না।** বিশেষ করে `Order`, `Payment`, `CouponUsage`, `Inventory`-এর ক্ষেত্রে আলাদা **ReadSerializer / CreateSerializer / UpdateSerializer** করলে production code অনেক বেশি নিরাপদ হবে।

পরের ধাপে তোমার এই modelগুলোর জন্য **proper `CreateSerializer + UpdateSerializer + ListSerializer + DetailSerializer` এবং `ViewSet` একসাথে** বানানো সবচেয়ে ভালো হবে।

ঠিক আছে। এবার আমরা **production-style DRF serializer architecture** করব। বিশেষ করে `Order`, `Payment`, `CouponUsage`, `Inventory`-এর ক্ষেত্রে client যেন sensitive field manipulate করতে না পারে—এটাই মূল লক্ষ্য।

একটা গুরুত্বপূর্ণ rule আগে:

```text
ListSerializer   → কম data, list page-এর জন্য
DetailSerializer → বেশি data, detail page-এর জন্য
CreateSerializer → client কী পাঠাতে পারবে
UpdateSerializer → client কী পরিবর্তন করতে পারবে
```

আর **Order / Payment / CouponUsage**-এর ক্ষেত্রে অনেক কাজ client সরাসরি করবে না; service/checkout logic করবে।

---

# Part 1 — Inventory

আমাদের final model:

```python
class Inventory(BaseModel):
    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.CASCADE,
        related_name="inventories"
    )

    warehouse = models.ForeignKey(
        Warehouse,
        on_delete=models.CASCADE,
        related_name="inventories"
    )

    quantity = models.PositiveIntegerField(default=0)
    reserved_quantity = models.PositiveIntegerField(default=0)
    reorder_level = models.PositiveIntegerField(default=5)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["variant", "warehouse"],
                name="unique_variant_warehouse"
            )
        ]

    @property
    def available_quantity(self):
        return self.quantity - self.reserved_quantity
```

## 1. Inventory List

List page-এ বেশি data দরকার নেই।

```python
class InventoryListSerializer(serializers.ModelSerializer):

    variant_name = serializers.CharField(
        source="variant.name",
        read_only=True
    )

    sku = serializers.CharField(
        source="variant.sku",
        read_only=True
    )

    warehouse_name = serializers.CharField(
        source="warehouse.name",
        read_only=True
    )

    available_quantity = serializers.ReadOnlyField()

    class Meta:
        model = Inventory
        fields = [
            "id",
            "variant",
            "variant_name",
            "sku",
            "warehouse",
            "warehouse_name",
            "quantity",
            "reserved_quantity",
            "available_quantity",
        ]
```

Response:

```json
{
    "id": 1,
    "variant": 10,
    "variant_name": "Black / M",
    "sku": "TSH-BLK-M",
    "warehouse": 2,
    "warehouse_name": "Dhaka Warehouse",
    "quantity": 20,
    "reserved_quantity": 3,
    "available_quantity": 17
}
```

---

## 2. Inventory Detail

```python
class InventoryDetailSerializer(serializers.ModelSerializer):

    available_quantity = serializers.ReadOnlyField()

    class Meta:
        model = Inventory
        fields = [
            "id",
            "variant",
            "warehouse",
            "quantity",
            "reserved_quantity",
            "available_quantity",
            "reorder_level",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "available_quantity",
            "created_at",
            "updated_at",
        ]
```

---

## 3. Inventory Create

এখানে `available_quantity` client পাঠাতে পারবে না।

```python
class InventoryCreateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Inventory
        fields = [
            "variant",
            "warehouse",
            "quantity",
            "reserved_quantity",
            "reorder_level",
        ]

    def validate(self, attrs):

        if attrs["reserved_quantity"] > attrs["quantity"]:
            raise serializers.ValidationError({
                "reserved_quantity":
                    "Reserved quantity cannot exceed quantity."
            })

        return attrs
```

---

## 4. Inventory Update

```python
class InventoryUpdateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Inventory
        fields = [
            "quantity",
            "reorder_level",
        ]

    def validate_quantity(self, value):

        if value < self.instance.reserved_quantity:
            raise serializers.ValidationError(
                "Quantity cannot be less than reserved quantity."
            )

        return value
```

### কেন `reserved_quantity` update করতে দিলাম না?

কারণ এটা সাধারণ CRUD update না।

Order reservation হলে:

```text
quantity = 20
reserved = 3
```

checkout/cancel হলে backend transaction-এর মাধ্যমে reservation change করবে।

---

# Part 2 — Order

এখানে সবচেয়ে গুরুত্বপূর্ণ security।

Customer কখনো এভাবে request পাঠাতে পারবে না:

```json
{
    "customer": 50,
    "total_amount": 10,
    "status": "COMPLETED"
}
```

এসব backend calculate করবে।

---

## 5. Order List Serializer

```python
class OrderListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Order
        fields = [
            "id",
            "order_number",
            "subtotal",
            "shipping_cost",
            "discount",
            "total_amount",
            "status",
            "created_at",
        ]
```

Customer order list:

```text
ORD-1001   ৳5000   CONFIRMED
ORD-1002   ৳2500   SHIPPED
ORD-1003   ৳9000   COMPLETED
```

---

# 6. Order Detail Serializer

এখানে nested seller order থাকবে।

```python
class OrderItemDetailSerializer(serializers.ModelSerializer):

    class Meta:
        model = OrderItem
        fields = [
            "id",
            "product",
            "variant",
            "product_name",
            "sku",
            "quantity",
            "unit_price",
            "total_price",
        ]
```

```python
class SellerOrderDetailSerializer(serializers.ModelSerializer):

    items = OrderItemDetailSerializer(
        many=True,
        read_only=True
    )

    class Meta:
        model = SellerOrder
        fields = [
            "id",
            "seller",
            "subtotal",
            "commission",
            "seller_amount",
            "status",
            "items",
        ]
```

তারপর:

```python
class OrderDetailSerializer(serializers.ModelSerializer):

    seller_orders = SellerOrderDetailSerializer(
        many=True,
        read_only=True
    )

    shipping_address = AddressSerializer(
        read_only=True
    )

    class Meta:
        model = Order

        fields = [
            "id",
            "order_number",
            "customer",
            "shipping_address",
            "subtotal",
            "shipping_cost",
            "discount",
            "total_amount",
            "status",
            "seller_orders",
            "created_at",
            "updated_at",
        ]
```

---

# 7. Order Create Serializer

Production e-commerce-এ আমি সরাসরি `OrderSerializer.create()` দিয়ে পুরো checkout logic করব না।

বরং:

```text
OrderCreateSerializer
        ↓
CheckoutService
        ↓
Order
SellerOrder
OrderItem
Inventory reservation
CouponUsage
Payment
```

Serializer শুধু input validate করবে।

```python
class OrderCreateSerializer(serializers.Serializer):

    shipping_address_id = serializers.UUIDField()

    coupon_code = serializers.CharField(
        required=False,
        allow_blank=True
    )

    payment_method = serializers.CharField(
        max_length=30
    )
```

তারপর service:

```python
class CheckoutService:

    @transaction.atomic
    def checkout(
        self,
        user,
        shipping_address_id,
        coupon_code=None,
        payment_method=None
    ):
        ...
```

এটা production architecture-এ অনেক cleaner।

---

# Part 3 — Payment

Payment-এর ক্ষেত্রে client-কে status control দেওয়া **খুব dangerous**।

Client:

```json
{
    "status": "PAID"
}
```

পাঠিয়ে দিলেই যেন paid না হয়ে যায়।

---

## 8. Payment List

```python
class PaymentListSerializer(serializers.ModelSerializer):

    class Meta:
        model = Payment
        fields = [
            "id",
            "order",
            "amount",
            "payment_method",
            "status",
            "paid_at",
            "created_at",
        ]
```

---

## 9. Payment Detail

```python
class PaymentDetailSerializer(serializers.ModelSerializer):

    class Meta:
        model = Payment
        fields = [
            "id",
            "order",
            "transaction_id",
            "payment_method",
            "amount",
            "status",
            "paid_at",
            "created_at",
        ]
```

---

## 10. Payment Create

Customer payment initiate করবে:

```python
class PaymentCreateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Payment

        fields = [
            "order",
            "payment_method",
        ]
```

`amount` client পাঠাবে না।

কারণ:

```text
Order.total_amount
        ↓
Payment.amount
```

backend সেট করবে।

---

## 11. Payment Update

সাধারণ customer-এর জন্য Payment Update endpoint রাখা উচিত না।

Payment status পরিবর্তন করবে:

```text
Payment Gateway
       ↓
Webhook
       ↓
Backend
       ↓
Payment.status = PAID
```

তাই:

```python
class PaymentUpdateSerializer(serializers.ModelSerializer):

    class Meta:
        model = Payment
        fields = []
```

Admin-এর জন্য আলাদা serializer/action রাখা যায়।

---

# Part 4 — CouponUsage

এটা customer CRUD resource না।

Customer:

```text
POST /coupon-usages/
```

করবে না।

Checkout-এর সময় backend তৈরি করবে।

---

## 12. CouponUsage List

Admin-এর জন্য:

```python
class CouponUsageListSerializer(serializers.ModelSerializer):

    coupon_code = serializers.CharField(
        source="coupon.code",
        read_only=True
    )

    class Meta:
        model = CouponUsage

        fields = [
            "id",
            "coupon",
            "coupon_code",
            "user",
            "order",
            "used_at",
        ]
```

---

## 13. CouponUsage Detail

```python
class CouponUsageDetailSerializer(serializers.ModelSerializer):

    coupon_code = serializers.CharField(
        source="coupon.code",
        read_only=True
    )

    class Meta:
        model = CouponUsage

        fields = [
            "id",
            "coupon",
            "coupon_code",
            "user",
            "order",
            "used_at",
        ]
```

---

## 14. CouponUsage Create

**Public create endpoint রাখব না।**

কারণ:

```text
CouponUsage
```

তৈরি হবে:

```text
CheckoutService
```

থেকে।

যেমন:

```python
CouponUsage.objects.create(
    coupon=coupon,
    user=user,
    order=order,
)
```

---

# Part 5 — ViewSet

এখন এগুলোকে ViewSet-এর সাথে connect করি।

## InventoryViewSet

```python
class InventoryViewSet(ModelViewSet):

    queryset = Inventory.objects.select_related(
        "variant",
        "warehouse",
    )

    def get_serializer_class(self):

        if self.action == "list":
            return InventoryListSerializer

        if self.action == "retrieve":
            return InventoryDetailSerializer

        if self.action == "create":
            return InventoryCreateSerializer

        if self.action in ["update", "partial_update"]:
            return InventoryUpdateSerializer

        return InventoryDetailSerializer
```

---

# OrderViewSet

Order create-এ checkout service ব্যবহার করব।

```python
class OrderViewSet(ModelViewSet):

    queryset = Order.objects.select_related(
        "customer",
        "shipping_address",
    ).prefetch_related(
        "seller_orders__items"
    )

    def get_serializer_class(self):

        if self.action == "list":
            return OrderListSerializer

        if self.action == "retrieve":
            return OrderDetailSerializer

        if self.action == "create":
            return OrderCreateSerializer

        return OrderDetailSerializer

    def get_queryset(self):
        return self.queryset.filter(
            customer=self.request.user
        )
```

তাহলে customer:

```text
GET /api/orders/
```

করলে শুধু নিজের orders পাবে।

---

# PaymentViewSet

```python
class PaymentViewSet(ModelViewSet):

    queryset = Payment.objects.select_related(
        "order"
    )

    def get_serializer_class(self):

        if self.action == "list":
            return PaymentListSerializer

        if self.action == "retrieve":
            return PaymentDetailSerializer

        if self.action == "create":
            return PaymentCreateSerializer

        return PaymentDetailSerializer

    def get_queryset(self):
        return self.queryset.filter(
            order__customer=self.request.user
        )
```

---

# CouponUsageViewSet

এটা সাধারণত admin/reporting endpoint হিসেবে রাখব।

```python
class CouponUsageViewSet(ReadOnlyModelViewSet):

    queryset = CouponUsage.objects.select_related(
        "coupon",
        "user",
        "order",
    )

    serializer_class = CouponUsageDetailSerializer
```

Customer-এর জন্য coupon usage history দরকার হলে:

```python
def get_queryset(self):
    return self.queryset.filter(
        user=self.request.user
    )
```

---

# পুরো architecture

এখন তোমার API architecture অনেকটা এমন:

```text
                         Product
                            │
                     ProductVariant
                            │
                        Inventory
                            │
                        Warehouse


Customer
   │
   └── Cart
        │
        └── CartItem
               │
               ↓
          CheckoutService
               │
               ├── Order
               │    │
               │    ├── SellerOrder
               │    │      └── OrderItem
               │    │
               │    └── SellerOrder
               │           └── OrderItem
               │
               ├── Inventory reservation
               │
               ├── CouponUsage
               │
               └── Payment
```

### সবচেয়ে গুরুত্বপূর্ণ security boundary

```text
Client
  │
  ├── shipping_address_id
  ├── coupon_code
  └── payment_method
  │
  ↓
Backend
  │
  ├── calculate subtotal
  ├── validate stock
  ├── calculate discount
  ├── calculate shipping
  ├── calculate total
  ├── create Order
  ├── create SellerOrder
  ├── create OrderItem
  ├── reserve Inventory
  ├── create CouponUsage
  └── initiate Payment
```

অর্থাৎ **client কখনো `total_amount`, `commission`, `seller_amount`, `used_count`, `payment.status`, `reserved_quantity`, `order.status` ইত্যাদি নিজের মতো করে পাঠিয়ে পরিবর্তন করতে পারবে না।**

এটাই production DRF-এ serializer আলাদা করার মূল কারণ।


---
হ্যাঁ। তোমার এখন পর্যন্ত final করা **multi-vendor e-commerce models** ধরে production-grade ViewSet structure দিচ্ছি।

একটা গুরুত্বপূর্ণ সিদ্ধান্ত: **সব model-এ blindly `ModelViewSet` ব্যবহার করব না।** কিছু model public/customer CRUD করবে, কিছু শুধু authenticated user নিজের data দেখবে, আর কিছু backend/admin controlled হবে।

---

# 1. Common imports

```python
# views.py

from django.db.models import Prefetch

from rest_framework import status, viewsets
from rest_framework.decorators import action
from rest_framework.permissions import (
    AllowAny,
    IsAuthenticated,
    IsAdminUser,
)
from rest_framework.response import Response

from .models import (
    User,
    Profile,
    Address,
    SellerProfile,
    SellerBankAccount,
    Category,
    Product,
    ProductImage,
    ProductVariant,
    Warehouse,
    Inventory,
    Cart,
    CartItem,
    Wishlist,
    Order,
    SellerOrder,
    OrderItem,
    Payment,
    Shipment,
    Review,
    Coupon,
    CouponUsage,
    SellerCommission,
)

from .serializers import (
    UserSerializer,
    ProfileSerializer,
    AddressSerializer,
    SellerProfileSerializer,
    SellerBankAccountSerializer,
    CategorySerializer,
    ProductSerializer,
    ProductImageSerializer,
    ProductVariantSerializer,
    WarehouseSerializer,
    InventoryListSerializer,
    InventoryDetailSerializer,
    InventoryCreateSerializer,
    InventoryUpdateSerializer,
    CartSerializer,
    CartItemSerializer,
    WishlistSerializer,
    OrderListSerializer,
    OrderDetailSerializer,
    OrderCreateSerializer,
    PaymentListSerializer,
    PaymentDetailSerializer,
    PaymentCreateSerializer,
    CouponSerializer,
    CouponUsageListSerializer,
    CouponUsageDetailSerializer,
    ReviewSerializer,
    ShipmentSerializer,
    SellerCommissionSerializer,
)
```

---

# 2. UserViewSet

User registration আর User management এক জিনিস না।

Production-এ সাধারণ user যেন অন্য user's data access করতে না পারে।

```python
class UserViewSet(viewsets.ModelViewSet):

    serializer_class = UserSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        user = self.request.user

        if user.is_staff:
            return User.objects.all()

        return User.objects.filter(id=user.id)
```

এখন:

```text
GET /api/users/
```

customer শুধু নিজের user দেখতে পারবে।

Admin সব দেখতে পারবে।

---

# 3. ProfileViewSet

```python
class ProfileViewSet(viewsets.ModelViewSet):

    serializer_class = ProfileSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        user = self.request.user

        if user.is_staff:
            return Profile.objects.select_related("user")

        return Profile.objects.filter(
            user=user
        )

    def perform_create(self, serializer):
        serializer.save(
            user=self.request.user
        )
```

---

# 4. AddressViewSet

Address user-specific।

```python
class AddressViewSet(viewsets.ModelViewSet):

    serializer_class = AddressSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        return Address.objects.filter(
            user=self.request.user
        )

    def perform_create(self, serializer):
        serializer.save(
            user=self.request.user
        )
```

Customer:

```text
GET /api/addresses/
```

করলে শুধু নিজের address পাবে।

---

# 5. SellerProfileViewSet

Seller নিজের profile manage করবে।

```python
class SellerProfileViewSet(viewsets.ModelViewSet):

    serializer_class = SellerProfileSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        user = self.request.user

        if user.is_staff:
            return SellerProfile.objects.select_related("user")

        return SellerProfile.objects.filter(
            user=user
        )

    def perform_create(self, serializer):
        serializer.save(
            user=self.request.user
        )
```

`status`, `is_verified` customer/seller নিজে change করতে পারবে না, কারণ serializer-এ read-only করেছি।

---

# 6. SellerBankAccountViewSet

```python
class SellerBankAccountViewSet(viewsets.ModelViewSet):

    serializer_class = SellerBankAccountSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        user = self.request.user

        if user.is_staff:
            return SellerBankAccount.objects.select_related(
                "seller"
            )

        return SellerBankAccount.objects.filter(
            seller__user=user
        )

    def perform_create(self, serializer):
        seller = self.request.user.seller_profile

        serializer.save(
            seller=seller
        )
```

---

# 7. CategoryViewSet

Category সাধারণত public read করতে পারে।

```python
class CategoryViewSet(viewsets.ModelViewSet):

    serializer_class = CategorySerializer

    def get_permissions(self):

        if self.action in ["list", "retrieve"]:
            return [AllowAny()]

        return [IsAdminUser()]

    def get_queryset(self):
        return Category.objects.filter(
            is_active=True
        ).select_related("parent")
```

এখানে:

```text
GET     → public
POST    → admin
PUT     → admin
PATCH   → admin
DELETE  → admin
```

---

# 8. ProductViewSet

এটা একটু গুরুত্বপূর্ণ।

```python
class ProductViewSet(viewsets.ModelViewSet):

    serializer_class = ProductSerializer

    def get_permissions(self):

        if self.action in ["list", "retrieve"]:
            return [AllowAny()]

        return [IsAuthenticated()]

    def get_queryset(self):

        return (
            Product.objects
            .select_related(
                "seller",
                "category",
            )
            .prefetch_related(
                "images",
                "variants",
            )
            .filter(
                is_active=True,
                is_published=True,
            )
        )
```

কিন্তু seller যেন অন্য seller-এর product update করতে না পারে—এটা অবশ্যই check করতে হবে।

```python
def perform_update(self, serializer):

    product = self.get_object()

    if (
        not self.request.user.is_staff
        and product.seller.user != self.request.user
    ):
        from rest_framework.exceptions import PermissionDenied

        raise PermissionDenied(
            "You cannot modify this product."
        )

    serializer.save()
```

Create:

```python
def perform_create(self, serializer):

    seller = self.request.user.seller_profile

    serializer.save(
        seller=seller
    )
```

---

# 9. ProductImageViewSet

```python
class ProductImageViewSet(viewsets.ModelViewSet):

    serializer_class = ProductImageSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return ProductImage.objects.filter(
            product__seller__user=self.request.user
        ).select_related(
            "product"
        )
```

---

# 10. ProductVariantViewSet

```python
class ProductVariantViewSet(viewsets.ModelViewSet):

    serializer_class = ProductVariantSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return ProductVariant.objects.filter(
            product__seller__user=self.request.user
        ).select_related(
            "product"
        )

    def perform_create(self, serializer):

        product = Product.objects.get(
            id=self.request.data.get("product")
        )

        if product.seller.user != self.request.user:
            from rest_framework.exceptions import PermissionDenied

            raise PermissionDenied(
                "You cannot add variant to this product."
            )

        serializer.save()
```

---

# 11. WarehouseViewSet

```python
class WarehouseViewSet(viewsets.ModelViewSet):

    serializer_class = WarehouseSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return Warehouse.objects.filter(
            seller__user=self.request.user
        )

    def perform_create(self, serializer):

        seller = self.request.user.seller_profile

        serializer.save(
            seller=seller
        )
```

---

# 12. InventoryViewSet

Inventory sensitive resource।

```python
class InventoryViewSet(viewsets.ModelViewSet):

    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Inventory.objects
            .select_related(
                "variant",
                "warehouse",
            )
            .filter(
                warehouse__seller__user=self.request.user
            )
        )

    def get_serializer_class(self):

        if self.action == "list":
            return InventoryListSerializer

        if self.action == "retrieve":
            return InventoryDetailSerializer

        if self.action == "create":
            return InventoryCreateSerializer

        if self.action in [
            "update",
            "partial_update",
        ]:
            return InventoryUpdateSerializer

        return InventoryDetailSerializer
```

Production-এ inventory quantity change আরও controlled করা ভালো।

যেমন:

```text
PATCH /inventory/1/
```

এর বদলে:

```text
POST /inventory/1/adjust/
```

করতে পারো।

```python
@action(
    detail=True,
    methods=["post"],
    url_path="adjust"
)
def adjust(self, request, pk=None):

    inventory = self.get_object()

    # inventory adjustment service
    # transaction.atomic()
    # select_for_update()

    return Response({
        "message": "Inventory adjusted successfully."
    })
```

---

# 13. CartViewSet

একজন user-এর একটা cart।

```python
class CartViewSet(viewsets.ReadOnlyModelViewSet):

    serializer_class = CartSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Cart.objects
            .filter(user=self.request.user)
            .prefetch_related(
                "items"
            )
        )
```

Cart create সাধারণত login-এর সময়/প্রথম add-to-cart-এর সময় backend করবে।

---

# 14. CartItemViewSet

```python
class CartItemViewSet(viewsets.ModelViewSet):

    serializer_class = CartItemSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return CartItem.objects.filter(
            cart__user=self.request.user
        ).select_related(
            "cart",
            "product",
            "variant",
        )

    def perform_create(self, serializer):

        cart, _ = Cart.objects.get_or_create(
            user=self.request.user
        )

        serializer.save(
            cart=cart
        )
```

---

# 15. WishlistViewSet

```python
class WishlistViewSet(viewsets.ModelViewSet):

    serializer_class = WishlistSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return Wishlist.objects.filter(
            user=self.request.user
        ).select_related(
            "product"
        )

    def perform_create(self, serializer):

        serializer.save(
            user=self.request.user
        )
```

---

# 16. OrderViewSet

এটাই সবচেয়ে sensitive অংশ।

```python
class OrderViewSet(viewsets.ModelViewSet):

    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Order.objects
            .filter(
                customer=self.request.user
            )
            .select_related(
                "customer",
                "shipping_address",
            )
            .prefetch_related(
                "seller_orders__items"
            )
        )

    def get_serializer_class(self):

        if self.action == "list":
            return OrderListSerializer

        if self.action == "retrieve":
            return OrderDetailSerializer

        if self.action == "create":
            return OrderCreateSerializer

        return OrderDetailSerializer
```

### কিন্তু create-এর ক্ষেত্রে

Order সরাসরি serializer দিয়ে create না করে:

```text
OrderViewSet
     ↓
CheckoutService
     ↓
transaction.atomic()
     ↓
Order
SellerOrder
OrderItem
Inventory
CouponUsage
Payment
```

এটা ব্যবহার করা উচিত।

---

# 17. SellerOrderViewSet

Seller নিজের orders দেখবে।

```python
class SellerOrderViewSet(viewsets.ReadOnlyModelViewSet):

    serializer_class = SellerOrderDetailSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            SellerOrder.objects
            .filter(
                seller__user=self.request.user
            )
            .select_related(
                "order",
                "seller",
            )
            .prefetch_related(
                "items"
            )
        )
```

Seller A:

```text
GET /api/seller-orders/
```

করলে Seller B-এর order দেখতে পাবে না।

---

# 18. OrderItemViewSet

Customer/Seller-এর জন্য আলাদা queryset দরকার।

```python
class OrderItemViewSet(viewsets.ReadOnlyModelViewSet):

    serializer_class = OrderItemSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            OrderItem.objects
            .filter(
                seller_order__order__customer=self.request.user
            )
            .select_related(
                "seller_order",
                "product",
                "variant",
            )
        )
```

---

# 19. PaymentViewSet

Payment customer নিজের order-এর জন্য দেখতে পারবে।

```python
class PaymentViewSet(viewsets.ModelViewSet):

    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Payment.objects
            .filter(
                order__customer=self.request.user
            )
            .select_related(
                "order"
            )
        )

    def get_serializer_class(self):

        if self.action == "list":
            return PaymentListSerializer

        if self.action == "retrieve":
            return PaymentDetailSerializer

        if self.action == "create":
            return PaymentCreateSerializer

        return PaymentDetailSerializer
```

**Payment status update customer করতে পারবে না।**

Gateway webhook/service করবে।

---

# 20. ShipmentViewSet

Shipment seller-specific।

```python
class ShipmentViewSet(viewsets.ModelViewSet):

    serializer_class = ShipmentSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Shipment.objects
            .filter(
                seller_order__seller__user=self.request.user
            )
            .select_related(
                "seller_order"
            )
        )
```

Seller নিজের shipment manage করবে।

---

# 21. ReviewViewSet

```python
class ReviewViewSet(viewsets.ModelViewSet):

    serializer_class = ReviewSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            Review.objects
            .filter(
                user=self.request.user
            )
            .select_related(
                "product",
                "order_item",
            )
        )

    def perform_create(self, serializer):

        serializer.save(
            user=self.request.user
        )
```

তবে production-এ create করার আগে verify করতে হবে:

```text
User
 ↓
OrderItem
 ↓
Product
```

অর্থাৎ customer সত্যিই product কিনেছে কিনা।

---

# 22. CouponViewSet

Coupon public validation-এর জন্য আলাদা endpoint/action ভালো।

Admin coupon CRUD করবে।

```python
class CouponViewSet(viewsets.ModelViewSet):

    serializer_class = CouponSerializer
    permission_classes = [IsAdminUser]

    queryset = Coupon.objects.all()
```

Customer-এর জন্য coupon list endpoint দেওয়ার প্রয়োজন নেই।

বরং checkout:

```text
POST /api/orders/checkout/
```

এর মধ্যে:

```json
{
    "coupon_code": "SAVE20"
}
```

পাঠাবে।

---

# 23. CouponUsageViewSet

Customer manually create করবে না।

```python
class CouponUsageViewSet(viewsets.ReadOnlyModelViewSet):

    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return CouponUsage.objects.filter(
            user=self.request.user
        ).select_related(
            "coupon",
            "order",
        )

    def get_serializer_class(self):

        if self.action == "list":
            return CouponUsageListSerializer

        return CouponUsageDetailSerializer
```

---

# 24. SellerCommissionViewSet

Seller নিজের commission দেখতে পারবে।

```python
class SellerCommissionViewSet(viewsets.ReadOnlyModelViewSet):

    serializer_class = SellerCommissionSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):

        return (
            SellerCommission.objects
            .filter(
                seller__user=self.request.user
            )
            .select_related(
                "seller",
                "seller_order",
            )
        )
```

Commission সাধারণ seller CRUD resource নয়।

Backend তৈরি করবে।

---

# 25. Router

শেষে `urls.py`:

```python
from rest_framework.routers import DefaultRouter

from .views import (
    UserViewSet,
    ProfileViewSet,
    AddressViewSet,
    SellerProfileViewSet,
    SellerBankAccountViewSet,
    CategoryViewSet,
    ProductViewSet,
    ProductImageViewSet,
    ProductVariantViewSet,
    WarehouseViewSet,
    InventoryViewSet,
    CartViewSet,
    CartItemViewSet,
    WishlistViewSet,
    OrderViewSet,
    SellerOrderViewSet,
    OrderItemViewSet,
    PaymentViewSet,
    ShipmentViewSet,
    ReviewViewSet,
    CouponViewSet,
    CouponUsageViewSet,
    SellerCommissionViewSet,
)

router = DefaultRouter()

router.register("users", UserViewSet, basename="users")
router.register("profiles", ProfileViewSet, basename="profiles")
router.register("addresses", AddressViewSet, basename="addresses")

router.register(
    "seller-profiles",
    SellerProfileViewSet,
    basename="seller-profiles"
)

router.register(
    "seller-bank-accounts",
    SellerBankAccountViewSet,
    basename="seller-bank-accounts"
)

router.register(
    "categories",
    CategoryViewSet,
    basename="categories"
)

router.register(
    "products",
    ProductViewSet,
    basename="products"
)

router.register(
    "product-images",
    ProductImageViewSet,
    basename="product-images"
)

router.register(
    "product-variants",
    ProductVariantViewSet,
    basename="product-variants"
)

router.register(
    "warehouses",
    WarehouseViewSet,
    basename="warehouses"
)

router.register(
    "inventory",
    InventoryViewSet,
    basename="inventory"
)

router.register(
    "cart",
    CartViewSet,
    basename="cart"
)

router.register(
    "cart-items",
    CartItemViewSet,
    basename="cart-items"
)

router.register(
    "wishlist",
    WishlistViewSet,
    basename="wishlist"
)

router.register(
    "orders",
    OrderViewSet,
    basename="orders"
)

router.register(
    "seller-orders",
    SellerOrderViewSet,
    basename="seller-orders"
)

router.register(
    "order-items",
    OrderItemViewSet,
    basename="order-items"
)

router.register(
    "payments",
    PaymentViewSet,
    basename="payments"
)

router.register(
    "shipments",
    ShipmentViewSet,
    basename="shipments"
)

router.register(
    "reviews",
    ReviewViewSet,
    basename="reviews"
)

router.register(
    "coupons",
    CouponViewSet,
    basename="coupons"
)

router.register(
    "coupon-usages",
    CouponUsageViewSet,
    basename="coupon-usages"
)

router.register(
    "seller-commissions",
    SellerCommissionViewSet,
    basename="seller-commissions"
)

urlpatterns = router.urls
```

## Final architecture

তোমার API এখন broadly এমন হবে:

```text
/api/
│
├── users/
├── profiles/
├── addresses/
│
├── seller-profiles/
├── seller-bank-accounts/
│
├── categories/
├── products/
├── product-images/
├── product-variants/
│
├── warehouses/
├── inventory/
│
├── cart/
├── cart-items/
├── wishlist/
│
├── orders/
├── seller-orders/
├── order-items/
│
├── payments/
├── shipments/
│
├── reviews/
│
├── coupons/
├── coupon-usages/
│
└── seller-commissions/
```

### তবে production-grade করতে আরও ৪টা জিনিস অবশ্যই যোগ করব

```text
1. Permission classes
       ↓
   Customer / Seller / Admin আলাদা permission

2. CheckoutService
       ↓
   Order creation-এর সব business logic

3. InventoryService
       ↓
   select_for_update() + transaction.atomic()

4. PaymentService
       ↓
   Gateway + webhook + payment verification
```

বিশেষ করে **`OrderViewSet`-এর `create()`-কে সরাসরি `serializer.save()` দিয়ে করা উচিত নয়**। Checkout-এর সময় cart → seller split → stock reservation → coupon → order → payment—সবগুলোকে একটি `CheckoutService` এবং `transaction.atomic()`-এর মাধ্যমে handle করাই production architecture-এর পরের গুরুত্বপূর্ণ ধাপ।

---
ঠিক আছে। এখন সবচেয়ে গুরুত্বপূর্ণ next step হলো **CheckoutService** বানানো। কারণ তোমার e-commerce-এর মূল business logic এখানে থাকবে।

আমাদের flow হবে:

```text
Cart
 ↓
Checkout API
 ↓
CheckoutService
 ↓
Validate Address
 ↓
Validate Cart
 ↓
Validate Stock
 ↓
Calculate Subtotal
 ↓
Apply Coupon
 ↓
Create Order
 ↓
Split by Seller
 ↓
Create SellerOrder
 ↓
Create OrderItem
 ↓
Reserve Inventory
 ↓
Create Payment
 ↓
Commit Transaction
```

## 1. Checkout Serializer

```python
from rest_framework import serializers


class CheckoutSerializer(serializers.Serializer):

    shipping_address_id = serializers.UUIDField()

    coupon_code = serializers.CharField(
        required=False,
        allow_blank=True,
        max_length=50
    )

    payment_method = serializers.ChoiceField(
        choices=[
            ("COD", "Cash on Delivery"),
            ("ONLINE", "Online Payment"),
        ]
    )
```

এখানে client শুধু এই information দেবে:

```json
{
    "shipping_address_id": "address-uuid",
    "coupon_code": "SAVE20",
    "payment_method": "COD"
}
```

**Subtotal, discount, total, seller, commission, stock—কোনোটাই client পাঠাবে না।**

---

# 2. CheckoutService

`services/checkout.py`

```python
from decimal import Decimal

from django.db import transaction
from django.db.models import Sum

from orders.models import (
    Order,
    SellerOrder,
    OrderItem,
    Payment,
)

from products.models import ProductVariant
from inventory.models import Inventory
from coupons.models import Coupon, CouponUsage
from addresses.models import Address


class CheckoutService:

    @classmethod
    @transaction.atomic
    def checkout(
        cls,
        *,
        user,
        shipping_address_id,
        coupon_code=None,
        payment_method="COD",
    ):

        # --------------------------------
        # 1. Get Cart
        # --------------------------------

        cart = (
            user.cart
        )

        cart_items = list(
            cart.items.select_related(
                "product",
                "variant",
                "product__seller",
            )
        )

        if not cart_items:
            raise ValueError(
                "Your cart is empty."
            )

        # --------------------------------
        # 2. Validate Address
        # --------------------------------

        address = Address.objects.get(
            id=shipping_address_id,
            user=user,
        )

        # --------------------------------
        # 3. Validate Cart Items
        # --------------------------------

        subtotal = Decimal("0.00")

        for item in cart_items:

            variant = item.variant

            if variant:

                inventory = (
                    Inventory.objects
                    .select_for_update()
                    .filter(
                        variant=variant,
                    )
                    .first()
                )

                if not inventory:
                    raise ValueError(
                        f"No inventory for {variant.sku}"
                    )

                available = (
                    inventory.quantity
                    - inventory.reserved_quantity
                )

                if available < item.quantity:
                    raise ValueError(
                        f"Insufficient stock for {variant.name}"
                    )

                price = variant.price

            else:

                price = item.product.price

            subtotal += price * item.quantity

        # --------------------------------
        # 4. Coupon
        # --------------------------------

        discount = Decimal("0.00")

        coupon = None

        if coupon_code:

            coupon = Coupon.objects.select_for_update().get(
                code__iexact=coupon_code,
                is_active=True,
            )

            discount = cls.calculate_coupon_discount(
                coupon,
                user,
                subtotal,
            )

        # --------------------------------
        # 5. Shipping
        # --------------------------------

        shipping_cost = Decimal("0.00")

        # এখানে পরে shipping service বসাতে পারো

        # --------------------------------
        # 6. Total
        # --------------------------------

        total_amount = (
            subtotal
            + shipping_cost
            - discount
        )

        # --------------------------------
        # 7. Create Order
        # --------------------------------

        order = Order.objects.create(
            customer=user,
            shipping_address=address,

            subtotal=subtotal,
            shipping_cost=shipping_cost,
            discount=discount,
            total_amount=total_amount,

            status=Order.Status.PENDING,
        )

        # --------------------------------
        # 8. Split Seller Orders
        # --------------------------------

        seller_groups = {}

        for item in cart_items:

            seller = item.product.seller

            seller_groups.setdefault(
                seller.id,
                []
            ).append(item)

        # --------------------------------
        # 9. Create SellerOrder
        # --------------------------------

        for seller_id, items in seller_groups.items():

            seller = items[0].product.seller

            seller_subtotal = Decimal("0.00")

            seller_order = SellerOrder.objects.create(
                order=order,
                seller=seller,
                subtotal=0,
                commission=0,
                seller_amount=0,
                status=SellerOrder.Status.PENDING,
            )

            # --------------------------------
            # 10. Create OrderItems
            # --------------------------------

            for item in items:

                if item.variant:

                    price = item.variant.price
                    sku = item.variant.sku
                    product_name = (
                        f"{item.product.name} - "
                        f"{item.variant.name}"
                    )

                else:

                    price = item.product.price
                    sku = item.product.sku
                    product_name = item.product.name

                total_price = (
                    price * item.quantity
                )

                seller_subtotal += total_price

                OrderItem.objects.create(
                    seller_order=seller_order,

                    product=item.product,
                    variant=item.variant,

                    product_name=product_name,
                    sku=sku,

                    quantity=item.quantity,
                    unit_price=price,
                    total_price=total_price,
                )

                # --------------------------------
                # 11. Reserve Inventory
                # --------------------------------

                if item.variant:

                    inventory = (
                        Inventory.objects
                        .select_for_update()
                        .filter(
                            variant=item.variant,
                        )
                        .first()
                    )

                    inventory.reserved_quantity += (
                        item.quantity
                    )

                    inventory.save(
                        update_fields=[
                            "reserved_quantity"
                        ]
                    )

            # --------------------------------
            # 12. Commission
            # --------------------------------

            commission_rate = (
                seller.commission_rate
            )

            commission = (
                seller_subtotal
                * commission_rate
                / Decimal("100")
            )

            seller_amount = (
                seller_subtotal
                - commission
            )

            seller_order.subtotal = (
                seller_subtotal
            )

            seller_order.commission = (
                commission
            )

            seller_order.seller_amount = (
                seller_amount
            )

            seller_order.save(
                update_fields=[
                    "subtotal",
                    "commission",
                    "seller_amount",
                ]
            )

        # --------------------------------
        # 13. Coupon Usage
        # --------------------------------

        if coupon:

            CouponUsage.objects.create(
                coupon=coupon,
                user=user,
                order=order,
            )

            coupon.used_count += 1

            coupon.save(
                update_fields=[
                    "used_count"
                ]
            )

        # --------------------------------
        # 14. Payment
        # --------------------------------

        Payment.objects.create(
            order=order,
            payment_method=payment_method,
            amount=total_amount,
        )

        # --------------------------------
        # 15. Clear Cart
        # --------------------------------

        cart.items.all().delete()

        return order
```

---

# 3. Coupon calculation আলাদা method

একই service-এর মধ্যে:

```python
@staticmethod
def calculate_coupon_discount(
    coupon,
    user,
    subtotal,
):
    from django.utils import timezone

    now = timezone.now()

    # Date validation
    if now < coupon.starts_at:
        raise ValueError(
            "Coupon is not active yet."
        )

    if now > coupon.expires_at:
        raise ValueError(
            "Coupon has expired."
        )

    # Minimum order
    if subtotal < coupon.minimum_order_amount:
        raise ValueError(
            f"Minimum order amount is "
            f"{coupon.minimum_order_amount}"
        )

    # Global usage limit
    if (
        coupon.usage_limit is not None
        and coupon.used_count >= coupon.usage_limit
    ):
        raise ValueError(
            "Coupon usage limit exceeded."
        )

    # Per-user usage
    if coupon.usage_limit_per_user:

        user_usage = CouponUsage.objects.filter(
            coupon=coupon,
            user=user,
        ).count()

        if (
            user_usage
            >= coupon.usage_limit_per_user
        ):
            raise ValueError(
                "You have reached the coupon usage limit."
            )

    # Percentage discount
    if coupon.discount_percentage:

        discount = (
            subtotal
            * coupon.discount_percentage
            / Decimal("100")
        )

    # Fixed discount
    elif coupon.discount_amount:

        discount = coupon.discount_amount

    else:

        discount = Decimal("0.00")

    # Maximum discount
    if coupon.maximum_discount:

        discount = min(
            discount,
            coupon.maximum_discount,
        )

    # Never discount more than subtotal
    discount = min(
        discount,
        subtotal,
    )

    return discount
```

---

# 4. Checkout ViewSet / Action

OrderViewSet-এর মধ্যে আলাদা `checkout` action করব।

```python
from rest_framework.decorators import action
from rest_framework.response import Response


class OrderViewSet(viewsets.ModelViewSet):

    permission_classes = [
        IsAuthenticated
    ]

    def get_queryset(self):

        return (
            Order.objects
            .filter(
                customer=self.request.user
            )
            .select_related(
                "customer",
                "shipping_address",
            )
            .prefetch_related(
                "seller_orders__items"
            )
        )

    def get_serializer_class(self):

        if self.action == "list":
            return OrderListSerializer

        if self.action == "retrieve":
            return OrderDetailSerializer

        if self.action == "checkout":
            return CheckoutSerializer

        return OrderDetailSerializer

    @action(
        detail=False,
        methods=["post"],
        url_path="checkout",
    )
    def checkout(self, request):

        serializer = CheckoutSerializer(
            data=request.data
        )

        serializer.is_valid(
            raise_exception=True
        )

        try:

            order = CheckoutService.checkout(
                user=request.user,

                shipping_address_id=(
                    serializer.validated_data[
                        "shipping_address_id"
                    ]
                ),

                coupon_code=(
                    serializer.validated_data.get(
                        "coupon_code"
                    )
                ),

                payment_method=(
                    serializer.validated_data[
                        "payment_method"
                    ]
                ),
            )

        except ValueError as exc:

            return Response(
                {
                    "detail": str(exc)
                },
                status=status.HTTP_400_BAD_REQUEST,
            )

        return Response(
            OrderDetailSerializer(
                order,
                context={
                    "request": request
                }
            ).data,
            status=status.HTTP_201_CREATED,
        )
```

তাহলে endpoint হবে:

```text
POST /api/orders/checkout/
```

Request:

```json
{
    "shipping_address_id": "address-uuid",
    "coupon_code": "SAVE20",
    "payment_method": "COD"
}
```

---

# 5. কেন `select_for_update()`?

ধরো stock:

```text
quantity = 10
reserved = 0
```

Customer A এবং Customer B একই সময়ে 8টা করে order করল।

Lock না থাকলে দুজনই দেখতে পারে:

```text
available = 10
```

এবং দুজনই 8টা reserve করতে পারে।

ফলে:

```text
reserved = 16
```

যা impossible।

`select_for_update()` database row lock করে:

```text
Customer A
    ↓
Lock Inventory
    ↓
Check stock
    ↓
Reserve 8
    ↓
Commit
    ↓
Unlock

Customer B
    ↓
Check updated stock
    ↓
Only 2 available
    ↓
Order rejected
```

এটাই production inventory handling-এর মূল ধারণা।

---

# 6. একটা গুরুত্বপূর্ণ correction

তোমার বর্তমান Inventory যদি **multiple warehouse** support করে:

```text
Variant
 ├── Dhaka Warehouse = 10
 └── Chittagong = 20
```

তাহলে checkout-এ:

```python
Inventory.objects.filter(
    variant=item.variant
).first()
```

ব্যবহার করা ঠিক হবে না।

কারণ কোন warehouse থেকে stock যাবে সেটা নির্ধারণ করতে হবে।

Production flow হবে:

```text
Order
 ↓
Shipping Address
 ↓
Determine Warehouse
 ↓
Lock that Warehouse Inventory
 ↓
Reserve Stock
```

অর্থাৎ পরে আমাদের `WarehouseSelectionService` লাগবে।

---

## এখন তোমার e-commerce-এর সবচেয়ে গুরুত্বপূর্ণ layer দাঁড়ালো

```text
                 API
                  │
                  ↓
             ViewSet
                  │
                  ↓
             Serializer
                  │
                  ↓
              Service
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Inventory    Coupon    Payment
    Service     Service    Service
       │          │          │
       └──────────┼──────────┘
                  ↓
              Database
```

**Next logical step:** `InventoryService` বানানো—`stock reserve`, `release`, `deduct`, `restore`, `select_for_update()`, `transaction.atomic()` এবং concurrent checkout/overselling কীভাবে safely handle করবে। এরপর `PaymentService + webhook` করলে পুরো checkout flow production-level হবে।

---
হ্যাঁ। এখন আমরা **InventoryService**-টা production-grade করি। এখানে সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো **overselling prevent করা**।

## 1. Inventory-এর lifecycle আগে বুঝি

একটা product-এর stock:

```text
quantity = 100
reserved_quantity = 0

available = 100 - 0
```

Customer order করলে:

```text
reserve(10)

quantity = 100
reserved = 10

available = 90
```

Payment সফল হলে:

```text
deduct(10)

quantity = 90
reserved = 0

available = 90
```

Order cancel হলে payment হওয়ার আগে:

```text
release(10)

quantity = 100
reserved = 0

available = 100
```

অর্থাৎ:

```text
               ┌── reserve ──→ Payment
               │                  │
Available ─────┤                  ├── deduct
               │                  │
               └── release ← Cancel
```

---

# 2. InventoryService

ধরি:

```text
inventory/services.py
```

```python
from django.db import transaction
from django.core.exceptions import ValidationError

from inventory.models import Inventory


class InventoryService:

    @staticmethod
    def get_locked_inventory(*, variant, warehouse=None):
        """
        Inventory row database lock করে return করবে।
        """

        queryset = (
            Inventory.objects
            .select_for_update()
            .select_related(
                "variant",
                "warehouse",
            )
            .filter(
                variant=variant,
            )
        )

        if warehouse:
            queryset = queryset.filter(
                warehouse=warehouse
            )

        inventory = queryset.first()

        if not inventory:
            raise ValidationError(
                "Inventory not found."
            )

        return inventory

    @classmethod
    @transaction.atomic
    def reserve(
        cls,
        *,
        variant,
        quantity,
        warehouse=None,
    ):
        """
        Customer checkout করলে stock reserve করবে।
        """

        if quantity <= 0:
            raise ValidationError(
                "Quantity must be greater than zero."
            )

        inventory = cls.get_locked_inventory(
            variant=variant,
            warehouse=warehouse,
        )

        available_quantity = (
            inventory.quantity
            - inventory.reserved_quantity
        )

        if available_quantity < quantity:
            raise ValidationError(
                f"Insufficient stock. "
                f"Available: {available_quantity}"
            )

        inventory.reserved_quantity += quantity

        inventory.save(
            update_fields=[
                "reserved_quantity",
                "updated_at",
            ]
        )

        return inventory
```

---

# 3. কেন `select_for_update()` এখানে এত গুরুত্বপূর্ণ?

ধরি database:

```text
quantity = 10
reserved_quantity = 0
```

দুইজন customer একই সময়ে 8টা করে order করল।

### Lock ছাড়া

```text
Customer A → available = 10
Customer B → available = 10

A reserve 8
B reserve 8

reserved = 16 ❌
```

Overselling হয়ে গেল।

### Lock সহ

```text
Customer A
    ↓
select_for_update()
    ↓
row locked
    ↓
available = 10
    ↓
reserve 8
    ↓
COMMIT
    ↓
unlock
```

তারপর:

```text
Customer B
    ↓
gets lock
    ↓
available = 2
    ↓
requested = 8
    ↓
REJECT ❌
```

তাই:

```python
.select_for_update()
```

**inventory concurrency-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।**

---

# 4. Release

Order payment-এর আগে cancel হলে reserved stock ফেরত দিতে হবে।

```python
@classmethod
@transaction.atomic
def release(
    cls,
    *,
    variant,
    quantity,
    warehouse=None,
):
    if quantity <= 0:
        raise ValidationError(
            "Quantity must be greater than zero."
        )

    inventory = cls.get_locked_inventory(
        variant=variant,
        warehouse=warehouse,
    )

    if inventory.reserved_quantity < quantity:
        raise ValidationError(
            "Cannot release more stock than reserved."
        )

    inventory.reserved_quantity -= quantity

    inventory.save(
        update_fields=[
            "reserved_quantity",
            "updated_at",
        ]
    )

    return inventory
```

Example:

```text
Before:

quantity = 100
reserved = 20
available = 80
```

Release 10:

```text
quantity = 100
reserved = 10
available = 90
```

---

# 5. Deduct

Payment সফল হওয়ার পরে actual stock কমাতে হবে।

```python
@classmethod
@transaction.atomic
def deduct(
    cls,
    *,
    variant,
    quantity,
    warehouse=None,
):
    if quantity <= 0:
        raise ValidationError(
            "Quantity must be greater than zero."
        )

    inventory = cls.get_locked_inventory(
        variant=variant,
        warehouse=warehouse,
    )

    if inventory.reserved_quantity < quantity:
        raise ValidationError(
            "Not enough reserved stock."
        )

    inventory.quantity -= quantity
    inventory.reserved_quantity -= quantity

    inventory.save(
        update_fields=[
            "quantity",
            "reserved_quantity",
            "updated_at",
        ]
    )

    return inventory
```

Example:

```text
Before:

quantity = 100
reserved = 20
available = 80
```

Payment successful → deduct 20:

```text
quantity = 80
reserved = 0
available = 80
```

---

# 6. Restore

ধরো payment সফল হয়েছে এবং:

```text
quantity = 80
reserved = 0
```

Customer পরে product return করল।

তখন:

```python
@classmethod
@transaction.atomic
def restore(
    cls,
    *,
    variant,
    quantity,
    warehouse=None,
):
    if quantity <= 0:
        raise ValidationError(
            "Quantity must be greater than zero."
        )

    inventory = cls.get_locked_inventory(
        variant=variant,
        warehouse=warehouse,
    )

    inventory.quantity += quantity

    inventory.save(
        update_fields=[
            "quantity",
            "updated_at",
        ]
    )

    return inventory
```

Result:

```text
Before:

quantity = 80

Return 5

After:

quantity = 85
```

---

# 7. Full InventoryService

শেষ পর্যন্ত service দেখতে এমন হবে:

```python
from django.db import transaction
from django.core.exceptions import ValidationError

from inventory.models import Inventory


class InventoryService:

    @staticmethod
    def get_locked_inventory(*, variant, warehouse=None):

        queryset = (
            Inventory.objects
            .select_for_update()
            .select_related(
                "variant",
                "warehouse",
            )
            .filter(
                variant=variant,
            )
        )

        if warehouse:
            queryset = queryset.filter(
                warehouse=warehouse
            )

        inventory = queryset.first()

        if not inventory:
            raise ValidationError(
                "Inventory not found."
            )

        return inventory

    @classmethod
    @transaction.atomic
    def reserve(
        cls,
        *,
        variant,
        quantity,
        warehouse=None,
    ):

        if quantity <= 0:
            raise ValidationError(
                "Quantity must be greater than zero."
            )

        inventory = cls.get_locked_inventory(
            variant=variant,
            warehouse=warehouse,
        )

        available = (
            inventory.quantity
            - inventory.reserved_quantity
        )

        if available < quantity:
            raise ValidationError(
                f"Insufficient stock. "
                f"Available: {available}"
            )

        inventory.reserved_quantity += quantity

        inventory.save(
            update_fields=[
                "reserved_quantity",
                "updated_at",
            ]
        )

        return inventory

    @classmethod
    @transaction.atomic
    def release(
        cls,
        *,
        variant,
        quantity,
        warehouse=None,
    ):

        if quantity <= 0:
            raise ValidationError(
                "Quantity must be greater than zero."
            )

        inventory = cls.get_locked_inventory(
            variant=variant,
            warehouse=warehouse,
        )

        if inventory.reserved_quantity < quantity:
            raise ValidationError(
                "Cannot release more than reserved stock."
            )

        inventory.reserved_quantity -= quantity

        inventory.save(
            update_fields=[
                "reserved_quantity",
                "updated_at",
            ]
        )

        return inventory

    @classmethod
    @transaction.atomic
    def deduct(
        cls,
        *,
        variant,
        quantity,
        warehouse=None,
    ):

        if quantity <= 0:
            raise ValidationError(
                "Quantity must be greater than zero."
            )

        inventory = cls.get_locked_inventory(
            variant=variant,
            warehouse=warehouse,
        )

        if inventory.reserved_quantity < quantity:
            raise ValidationError(
                "Not enough reserved stock."
            )

        inventory.quantity -= quantity
        inventory.reserved_quantity -= quantity

        inventory.save(
            update_fields=[
                "quantity",
                "reserved_quantity",
                "updated_at",
            ]
        )

        return inventory

    @classmethod
    @transaction.atomic
    def restore(
        cls,
        *,
        variant,
        quantity,
        warehouse=None,
    ):

        if quantity <= 0:
            raise ValidationError(
                "Quantity must be greater than zero."
            )

        inventory = cls.get_locked_inventory(
            variant=variant,
            warehouse=warehouse,
        )

        inventory.quantity += quantity

        inventory.save(
            update_fields=[
                "quantity",
                "updated_at",
            ]
        )

        return inventory
```

---

# 8. এখন CheckoutService-এর সাথে connect করি

আগের `CheckoutService`-এ আমরা নিজের হাতে করছিলাম:

```python
inventory.reserved_quantity += item.quantity
```

এটা আর করা উচিত না।

এর পরিবর্তে:

```python
InventoryService.reserve(
    variant=item.variant,
    quantity=item.quantity,
)
```

অর্থাৎ:

```text
CheckoutService
       │
       ↓
InventoryService
       │
       ├── select_for_update()
       ├── stock check
       ├── reserve
       └── transaction
```

এতে inventory-এর business logic এক জায়গায় থাকবে।

---

# 9. কিন্তু Multi-Warehouse হলে একটা সমস্যা আছে

তোমার architecture:

```text
ProductVariant
      │
      ├── Inventory → Dhaka Warehouse
      │
      └── Inventory → Chittagong Warehouse
```

তখন:

```python
Inventory.objects.filter(
    variant=variant
).first()
```

**production-এর জন্য যথেষ্ট নয়।**

কারণ system-কে সিদ্ধান্ত নিতে হবে:

```text
Customer address = Dhaka
        ↓
Dhaka Warehouse
        ↓
Stock available?
        ↓
Reserve
```

এজন্য পরের layer:

```text
WarehouseSelectionService
```

বানানো ভালো।

---

# 10. সবচেয়ে গুরুত্বপূর্ণ architecture

শেষে inventory system এমন হবে:

```text
                    Checkout
                       │
                       ↓
             WarehouseSelectionService
                       │
                       ↓
                 InventoryService
                       │
            ┌──────────┼──────────┐
            ↓          ↓          ↓
         reserve     release    deduct
            │          │          │
            └──────────┼──────────┘
                       ↓
                select_for_update
                       ↓
                  PostgreSQL
```

আর lifecycle:

```text
Checkout
   │
   ├── reserve()
   │
   ↓
Payment Pending
   │
   ├── Payment Failed
   │       ↓
   │    release()
   │
   └── Payment Success
           ↓
        deduct()
           │
           ↓
       Order Paid
```

Return হলে:

```text
Delivered
    ↓
Return Approved
    ↓
restore()
```

---

## একটি production improvement আরও দরকার

শুধু `quantity` + `reserved_quantity` দিয়ে system কাজ করবে, কিন্তু বড় production system-এ **InventoryTransaction / StockMovement** table রাখা খুব উপকারী।

যেমন:

```text
Inventory
    quantity = 100
    reserved = 10

InventoryTransaction

+10  PURCHASE
-10  SALE
+10  RETURN
+10  RELEASE
-10  DAMAGE
```

তাহলে পরে প্রশ্নের উত্তর দিতে পারবে:

> “এই product-এর stock 100 থেকে 73 হলো কেন?”

Audit history পাওয়া যাবে।

### Final architecture

```text
ProductVariant
      │
      ↓
Inventory
      │
      ↓
InventoryTransaction
      │
      ├── PURCHASE
      ├── RESERVE
      ├── RELEASE
      ├── SALE
      ├── RETURN
      └── DAMAGE
```

**পরের step হিসেবে `InventoryTransaction` model + complete `InventoryService` transaction logging + multi-warehouse stock allocation implement করা সবচেয়ে logical।** এরপর তার ওপর `PaymentService` এবং payment gateway webhook বসালে checkout flow সম্পূর্ণ production architecture-এর দিকে যাবে।

---
ঠিক আছে। এবার আমরা **InventoryTransaction + Multi-Warehouse Allocation + Complete InventoryService** একসাথে production-style করব।

সবচেয়ে আগে architecture:

```text
ProductVariant
      │
      ├──────────────┐
      ↓              ↓
 Warehouse A      Warehouse B
      │              │
   Inventory       Inventory
      │              │
      └──────┬───────┘
             ↓
   InventoryTransaction
```

Checkout-এর সময়:

```text
Checkout
   ↓
WarehouseSelectionService
   ↓
InventoryAllocation
   ↓
InventoryService.reserve()
   ↓
InventoryTransaction
```

---

# 1. InventoryTransaction Model

`inventory/models.py`

```python
from django.db import models

from core.models import BaseModel


class InventoryTransaction(BaseModel):

    class TransactionType(models.TextChoices):
        PURCHASE = "PURCHASE", "Purchase"
        RESERVE = "RESERVE", "Reserve"
        RELEASE = "RELEASE", "Release"
        SALE = "SALE", "Sale"
        RETURN = "RETURN", "Return"
        DAMAGE = "DAMAGE", "Damage"
        ADJUSTMENT = "ADJUSTMENT", "Adjustment"

    inventory = models.ForeignKey(
        "inventory.Inventory",
        on_delete=models.PROTECT,
        related_name="transactions",
    )

    transaction_type = models.CharField(
        max_length=20,
        choices=TransactionType.choices,
    )

    quantity = models.IntegerField(
        help_text="Positive or negative stock movement."
    )

    reference_type = models.CharField(
        max_length=50,
        blank=True,
    )

    reference_id = models.UUIDField(
        null=True,
        blank=True,
    )

    note = models.TextField(
        blank=True,
    )

    created_by = models.ForeignKey(
        "accounts.User",
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="inventory_transactions",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=[
                    "inventory",
                    "transaction_type",
                ]
            ),
            models.Index(
                fields=[
                    "reference_type",
                    "reference_id",
                ]
            ),
        ]
```

---

# 2. `quantity` কেন signed রাখলাম?

ধরি stock 100।

Purchase:

```text
+50
```

Sale:

```text
-10
```

Return:

```text
+5
```

Damage:

```text
-2
```

তাহলে history:

```text
PURCHASE    +50
SALE        -10
RETURN      +5
DAMAGE      -2
```

এটা audit করা অনেক সহজ।

---

# 3. Multi-Warehouse-এর জন্য Allocation Model

এখানে একটা গুরুত্বপূর্ণ production case আছে।

ধরি customer 15টা product কিনেছে।

Warehouse A:

```text
available = 10
```

Warehouse B:

```text
available = 20
```

তাহলে এক warehouse থেকে 15 পাওয়া যাবে না।

System করতে পারে:

```text
Warehouse A → 10
Warehouse B → 5
```

তাই `OrderItem`-এর সাথে inventory allocation রাখা ভালো।

```python
class OrderItemInventoryAllocation(BaseModel):

    order_item = models.ForeignKey(
        "orders.OrderItem",
        on_delete=models.CASCADE,
        related_name="inventory_allocations",
    )

    inventory = models.ForeignKey(
        "inventory.Inventory",
        on_delete=models.PROTECT,
        related_name="order_allocations",
    )

    quantity = models.PositiveIntegerField()

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "order_item",
                    "inventory",
                ],
                name="unique_order_item_inventory",
            )
        ]
```

এখন structure:

```text
OrderItem
   │
   ├── Allocation
   │      └── Warehouse A → 10
   │
   └── Allocation
          └── Warehouse B → 5
```

এটা ভবিষ্যতে split shipment-এর জন্যও useful।

---

# 4. Warehouse selection-এর দায়িত্ব আলাদা Service-এ

`inventory/services/warehouse.py`

```python
from django.core.exceptions import ValidationError

from inventory.models import Inventory


class WarehouseSelectionService:

    @staticmethod
    def get_available_inventories(
        *,
        seller,
        variant,
    ):
        return (
            Inventory.objects
            .select_related("warehouse")
            .filter(
                variant=variant,
                warehouse__seller=seller,
                warehouse__is_active=True,
                is_active=True,
            )
        )

    @classmethod
    def allocate(
        cls,
        *,
        seller,
        variant,
        quantity,
    ):
        """
        Multiple warehouse থেকে requested quantity allocate করবে।
        """

        inventories = cls.get_available_inventories(
            seller=seller,
            variant=variant,
        )

        allocations = []

        remaining = quantity

        for inventory in inventories:

            available = (
                inventory.quantity
                - inventory.reserved_quantity
            )

            if available <= 0:
                continue

            allocated = min(
                available,
                remaining,
            )

            allocations.append(
                {
                    "inventory": inventory,
                    "quantity": allocated,
                }
            )

            remaining -= allocated

            if remaining == 0:
                break

        if remaining > 0:
            raise ValidationError(
                "Insufficient stock across all warehouses."
            )

        return allocations
```

---

# 5. Example

ধরি:

```text
Product = iPhone
Requested = 15
```

Warehouse:

```text
Dhaka:
quantity = 10
reserved = 2

Available = 8
```

আর:

```text
Chittagong:
quantity = 20
reserved = 3

Available = 17
```

Allocation:

```text
Dhaka       → 8
Chittagong  → 7
----------------
Total       → 15
```

---

# 6. কিন্তু এখানেও concurrency problem আছে

উপরের method শুধু allocation calculate করছে।

এখনো অন্য checkout একই stock reserve করতে পারে।

তাই **allocation calculation এবং reservation একই database transaction-এর মধ্যে করতে হবে।**

এটাই গুরুত্বপূর্ণ।

---

# 7. Production InventoryService

`inventory/services/inventory.py`

```python
from django.db import transaction
from django.core.exceptions import ValidationError

from inventory.models import (
    Inventory,
    InventoryTransaction,
)


class InventoryService:

    @staticmethod
    def _get_locked_inventory(inventory_id):

        try:
            return (
                Inventory.objects
                .select_for_update()
                .select_related(
                    "variant",
                    "warehouse",
                )
                .get(
                    id=inventory_id,
                )
            )

        except Inventory.DoesNotExist:
            raise ValidationError(
                "Inventory not found."
            )

    @classmethod
    @transaction.atomic
    def reserve(
        cls,
        *,
        allocations,
        reference_type="ORDER",
        reference_id=None,
        created_by=None,
    ):
        """
        allocations:

        [
            {
                "inventory_id": "...",
                "quantity": 8,
            },
            {
                "inventory_id": "...",
                "quantity": 7,
            }
        ]
        """

        transactions = []

        for allocation in allocations:

            inventory = cls._get_locked_inventory(
                allocation["inventory_id"]
            )

            quantity = allocation["quantity"]

            available = (
                inventory.quantity
                - inventory.reserved_quantity
            )

            if available < quantity:
                raise ValidationError(
                    f"Insufficient stock for "
                    f"{inventory.variant.name}."
                )

            inventory.reserved_quantity += quantity

            inventory.save(
                update_fields=[
                    "reserved_quantity",
                    "updated_at",
                ]
            )

            transactions.append(
                InventoryTransaction(
                    inventory=inventory,
                    transaction_type=(
                        InventoryTransaction
                        .TransactionType
                        .RESERVE
                    ),
                    quantity=quantity,
                    reference_type=reference_type,
                    reference_id=reference_id,
                    created_by=created_by,
                )
            )

        InventoryTransaction.objects.bulk_create(
            transactions
        )

        return True
```

---

# 8. কেন আগে allocation করে পরে আবার lock?

এখানে একটা subtle issue আছে।

যদি:

```text
Step 1:
allocate()

Step 2:
reserve()
```

দুটি completely separate transaction হয়, তাহলে race condition হতে পারে।

Production solution:

```text
BEGIN TRANSACTION
      ↓
SELECT inventory FOR UPDATE
      ↓
calculate available
      ↓
allocate
      ↓
reserve
      ↓
create transaction logs
      ↓
COMMIT
```

অর্থাৎ **allocation + reservation একই atomic operation** হওয়া সবচেয়ে নিরাপদ।

তাই আরও ভালো design হলো `reserve_for_order()` একাই allocation করবে।

---

# 9. Final `reserve_for_order()`

```python
class InventoryService:

    @classmethod
    @transaction.atomic
    def reserve_for_order(
        cls,
        *,
        seller,
        variant,
        quantity,
        order_id,
        created_by=None,
    ):
        inventories = list(
            Inventory.objects
            .select_for_update()
            .select_related("warehouse")
            .filter(
                variant=variant,
                warehouse__seller=seller,
                warehouse__is_active=True,
                is_active=True,
            )
            .order_by("warehouse_id")
        )

        remaining = quantity
        allocations = []
        transactions = []

        for inventory in inventories:

            available = (
                inventory.quantity
                - inventory.reserved_quantity
            )

            if available <= 0:
                continue

            allocated = min(
                available,
                remaining,
            )

            inventory.reserved_quantity += allocated

            inventory.save(
                update_fields=[
                    "reserved_quantity",
                    "updated_at",
                ]
            )

            allocations.append(
                {
                    "inventory": inventory,
                    "quantity": allocated,
                }
            )

            transactions.append(
                InventoryTransaction(
                    inventory=inventory,
                    transaction_type=(
                        InventoryTransaction
                        .TransactionType
                        .RESERVE
                    ),
                    quantity=allocated,
                    reference_type="ORDER",
                    reference_id=order_id,
                    created_by=created_by,
                )
            )

            remaining -= allocated

            if remaining == 0:
                break

        if remaining > 0:
            raise ValidationError(
                "Insufficient stock."
            )

        InventoryTransaction.objects.bulk_create(
            transactions
        )

        return allocations
```

এটাই অনেক বেশি reliable।

---

# 10. `release()` এবার allocation অনুযায়ী হবে

কারণ order item-এর stock দুই warehouse-এ থাকতে পারে।

```python
@classmethod
@transaction.atomic
def release(
    cls,
    *,
    allocations,
    order_id,
    created_by=None,
):

    transactions = []

    for allocation in allocations:

        inventory = cls._get_locked_inventory(
            allocation["inventory_id"]
        )

        quantity = allocation["quantity"]

        if inventory.reserved_quantity < quantity:
            raise ValidationError(
                "Invalid reserved quantity."
            )

        inventory.reserved_quantity -= quantity

        inventory.save(
            update_fields=[
                "reserved_quantity",
                "updated_at",
            ]
        )

        transactions.append(
            InventoryTransaction(
                inventory=inventory,
                transaction_type=(
                    InventoryTransaction
                    .TransactionType
                    .RELEASE
                ),
                quantity=quantity,
                reference_type="ORDER",
                reference_id=order_id,
                created_by=created_by,
            )
        )

    InventoryTransaction.objects.bulk_create(
        transactions
    )
```

---

# 11. Payment successful হলে `deduct()`

Payment successful:

```text
reserved → actual sold
```

```python
@classmethod
@transaction.atomic
def deduct(
    cls,
    *,
    allocations,
    order_id,
    created_by=None,
):

    transactions = []

    for allocation in allocations:

        inventory = cls._get_locked_inventory(
            allocation["inventory_id"]
        )

        quantity = allocation["quantity"]

        if inventory.reserved_quantity < quantity:
            raise ValidationError(
                "Reserved stock is insufficient."
            )

        inventory.quantity -= quantity
        inventory.reserved_quantity -= quantity

        inventory.save(
            update_fields=[
                "quantity",
                "reserved_quantity",
                "updated_at",
            ]
        )

        transactions.append(
            InventoryTransaction(
                inventory=inventory,
                transaction_type=(
                    InventoryTransaction
                    .TransactionType
                    .SALE
                ),
                quantity=-quantity,
                reference_type="ORDER",
                reference_id=order_id,
                created_by=created_by,
            )
        )

    InventoryTransaction.objects.bulk_create(
        transactions
    )
```

---

# 12. Return হলে restore

```python
@classmethod
@transaction.atomic
def restore(
    cls,
    *,
    allocations,
    order_id,
    created_by=None,
):

    transactions = []

    for allocation in allocations:

        inventory = cls._get_locked_inventory(
            allocation["inventory_id"]
        )

        quantity = allocation["quantity"]

        inventory.quantity += quantity

        inventory.save(
            update_fields=[
                "quantity",
                "updated_at",
            ]
        )

        transactions.append(
            InventoryTransaction(
                inventory=inventory,
                transaction_type=(
                    InventoryTransaction
                    .TransactionType
                    .RETURN
                ),
                quantity=quantity,
                reference_type="RETURN",
                reference_id=order_id,
                created_by=created_by,
            )
        )

    InventoryTransaction.objects.bulk_create(
        transactions
    )
```

---

# 13. পুরো stock lifecycle

এখন একটা complete example দেখি।

Initial:

```text
Warehouse A

quantity = 100
reserved = 0
available = 100
```

Customer order:

```text
quantity = 100
reserved = 10
available = 90
```

Transaction:

```text
RESERVE +10
```

---

### Payment failed

```text
quantity = 100
reserved = 0
available = 100
```

Transaction:

```text
RELEASE +10
```

---

### অথবা Payment successful

```text
quantity = 90
reserved = 0
available = 90
```

Transaction:

```text
SALE -10
```

---

### পরে Return

```text
quantity = 100
reserved = 0
available = 100
```

Transaction:

```text
RETURN +10
```

---

# 14. সবচেয়ে গুরুত্বপূর্ণ concurrency scenario

ধরি:

```text
Stock = 10
```

দুই customer:

```text
Customer A → 8
Customer B → 5
```

একই সময়ে checkout।

Database row lock:

```text
Customer A
    ↓
SELECT FOR UPDATE
    ↓
Stock locked
    ↓
available = 10
    ↓
reserve 8
    ↓
COMMIT
    ↓
unlock
```

তারপর:

```text
Customer B
    ↓
gets lock
    ↓
available = 2
    ↓
requested = 5
    ↓
ValidationError
```

Result:

```text
Reserved = 8
Available = 2
```

**Overselling হবে না।**

---

# 15. একটি গুরুত্বপূর্ণ production rule

`Inventory.quantity` এবং `reserved_quantity` কখনো frontend থেকে update করতে দেবে না।

ভুল:

```http
PATCH /api/inventory/123/

{
    "quantity": 500
}
```

Customer তো অবশ্যই না।

Seller/admin-এর manual stock adjustment থাকলেও:

```text
ViewSet
   ↓
InventoryAdjustmentService
   ↓
select_for_update()
   ↓
update stock
   ↓
InventoryTransaction
```

অর্থাৎ:

```text
সব stock mutation
       ↓
Service Layer
       ↓
InventoryTransaction
```

---

# 16. আরেকটি production issue: duplicate webhook

Payment gateway একই webhook দুইবার পাঠাতে পারে।

যেমন:

```text
Webhook #1 → payment success
Webhook #2 → payment success
```

যদি blindly:

```python
InventoryService.deduct(...)
```

করো, তাহলে দুইবার stock deduct হতে পারে।

তাই PaymentService-এ পরে **idempotency** লাগবে।

Flow হবে:

```text
Webhook
   ↓
transaction.atomic()
   ↓
lock Payment
   ↓
already PAID?
   ├── YES → return
   └── NO
        ↓
      PAID
        ↓
InventoryService.deduct()
```

এটা খুব গুরুত্বপূর্ণ production concept।

---

# 17. Final architecture এখন

```text
                    CHECKOUT
                       │
                       ↓
              Warehouse Allocation
                       │
                       ↓
                InventoryService
                       │
              ┌────────┼────────┐
              ↓        ↓        ↓
           RESERVE   RELEASE   DEDUCT
              │        │        │
              └────────┼────────┘
                       ↓
                Inventory
                       │
                       ↓
             InventoryTransaction
```

তারপর payment:

```text
Checkout
   ↓
Order = PENDING
   ↓
Payment = PENDING
   ↓
Reserve Stock
   ↓
Payment Gateway
   ↓
Webhook
   ↓
PaymentService
   ↓
Payment = PAID
   ↓
InventoryService.deduct()
   ↓
Order = CONFIRMED
```

Payment fail:

```text
Payment Gateway
      ↓
Webhook
      ↓
PaymentService
      ↓
Payment = FAILED
      ↓
InventoryService.release()
      ↓
Order = CANCELLED
```

### এরপরের logical class

এখন inventory layer প্রায় দাঁড়িয়ে গেছে। **পরবর্তী অংশ হবে `PaymentService`**, যেখানে আমরা দেখব:

1. `Payment` state machine
2. COD বনাম Online Payment
3. Payment gateway abstraction
4. `PaymentService.create_payment()`
5. `PaymentService.handle_success()`
6. `PaymentService.handle_failure()`
7. webhook signature verification
8. duplicate webhook/idempotency
9. payment + inventory transaction boundary
10. payment failure হলে automatic stock release
11. Celery দিয়ে expired reservation release

এটার পরেই **OrderService + PaymentService + InventoryService মিলিয়ে সম্পূর্ণ production checkout flow** দাঁড়াবে।


---
একদম। এবার আমরা **PaymentService — Production Payment Architecture** শুরু করি। এখানে মূল লক্ষ্য হলো payment gateway-এর code-কে business logic থেকে আলাদা রাখা এবং **duplicate webhook / double payment / stock inconsistency** prevent করা।

---

# Class 1 — PaymentService Production Architecture

আমাদের final flow:

```text
                    Checkout
                       │
                       ↓
                  Order Created
                       │
                       ↓
                 Stock Reserved
                       │
                       ↓
                 Payment Created
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
            COD               ONLINE
             │                   │
             ↓                   ↓
       Order Confirmed      Payment Gateway
                                 │
                                 ↓
                              Webhook
                                 │
                                 ↓
                          PaymentService
                                 │
                    ┌────────────┴────────────┐
                    ↓                         ↓
                 SUCCESS                    FAILED
                    ↓                         ↓
              Deduct Stock              Release Stock
                    ↓                         ↓
              Order Confirmed          Order Cancelled
```

---

# 1. প্রথমে Payment State Machine

Payment-এর status client নিজের ইচ্ছামতো change করতে পারবে না।

```python id="9h5s7j"
class Payment(models.Model):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PROCESSING = "PROCESSING", "Processing"
        PAID = "PAID", "Paid"
        FAILED = "FAILED", "Failed"
        CANCELLED = "CANCELLED", "Cancelled"
        REFUNDED = "REFUNDED", "Refunded"
```

State transition:

```text id="7ecq4m"
PENDING
   │
   ├──→ PROCESSING
   │        │
   │        ├──→ PAID
   │        │
   │        └──→ FAILED
   │
   └──→ CANCELLED

PAID
   │
   └──→ REFUNDED
```

কিন্তু:

```text id="s8v4xg"
PAID → PENDING ❌
REFUNDED → PAID ❌
FAILED → PAID
```

শেষেরটা technically webhook reconciliation-এর মাধ্যমে controlled transition হতে পারে, কিন্তু arbitrary update নয়।

---

# 2. Payment Model আরও production-ready করি

```python id="t2j9p4"
class Payment(BaseModel):

    class Method(models.TextChoices):
        COD = "COD", "Cash on Delivery"
        ONLINE = "ONLINE", "Online Payment"

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PROCESSING = "PROCESSING", "Processing"
        PAID = "PAID", "Paid"
        FAILED = "FAILED", "Failed"
        CANCELLED = "CANCELLED", "Cancelled"
        REFUNDED = "REFUNDED", "Refunded"

    order = models.OneToOneField(
        "orders.Order",
        on_delete=models.PROTECT,
        related_name="payment",
    )

    payment_method = models.CharField(
        max_length=20,
        choices=Method.choices,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING,
    )

    transaction_id = models.CharField(
        max_length=255,
        unique=True,
        null=True,
        blank=True,
    )

    gateway_name = models.CharField(
        max_length=50,
        blank=True,
    )

    gateway_transaction_id = models.CharField(
        max_length=255,
        unique=True,
        null=True,
        blank=True,
    )

    gateway_response = models.JSONField(
        null=True,
        blank=True,
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

এখানে:

```text
transaction_id
```

আমাদের internal transaction identifier।

আর:

```text
gateway_transaction_id
```

payment provider-এর transaction ID।

---

# 3. COD আর Online Payment-এর পার্থক্য

## COD

```text id="tq3w8n"
Checkout
   ↓
Order
   ↓
Reserve stock
   ↓
Payment(PENDING)
   ↓
COD selected
   ↓
Order Confirmed
```

COD-এর ক্ষেত্রে gateway webhook দরকার নেই।

Payment technically পরে collect হবে।

তবে তুমি চাইলে:

```text
Payment.status = PENDING
```

রাখতে পারো যতক্ষণ না delivery-এর সময় payment collect হয়।

---

# 4. Online Payment

```text id="d8lqz0"
Checkout
   ↓
Order
   ↓
Reserve stock
   ↓
Payment PENDING
   ↓
Gateway
   ↓
Customer pays
   ↓
Gateway webhook
   ↓
PaymentService
   ↓
PAID
```

---

# 5. Gateway abstraction কেন?

ধরো আজ:

```text id="d7z8vh"
SSLCommerz
```

ব্যবহার করছ।

আগামীতে:

```text id="w5f6ag"
Stripe
```

অথবা:

```text id="4s6t3u"
PayPal
```

যোগ করতে পারো।

যদি checkout-এর মধ্যে সরাসরি:

```python
sslcommerz_api(...)
```

লিখে ফেলো, architecture tightly coupled হয়ে যাবে।

তাই:

```text id="7ep5vz"
PaymentService
      │
      ↓
PaymentGateway
      │
 ┌────┼──────┐
 ↓    ↓      ↓
SSL  Stripe  PayPal
```

---

# 6. Gateway Interface

`payments/gateways/base.py`

```python id="n6v2ma"
from abc import ABC, abstractmethod


class PaymentGateway(ABC):

    @abstractmethod
    def create_payment(
        self,
        *,
        payment,
    ):
        pass

    @abstractmethod
    def verify_webhook(
        self,
        *,
        request,
    ):
        pass

    @abstractmethod
    def parse_webhook(
        self,
        *,
        request,
    ):
        pass
```

এখন gateway implementation আলাদা হবে।

---

# 7. Example Gateway

ধরি:

```text id="83z7ws"
payments/gateways/sslcommerz.py
```

```python id="nccj5j"
from .base import PaymentGateway


class SSLCommerzGateway(PaymentGateway):

    def create_payment(
        self,
        *,
        payment,
    ):

        # Real SSLCommerz API call এখানে হবে

        return {
            "success": True,
            "payment_url": "https://gateway.example/pay/123",
        }

    def verify_webhook(
        self,
        *,
        request,
    ):

        # Gateway signature/hash verification
        return True

    def parse_webhook(
        self,
        *,
        request,
    ):

        data = request.data

        return {
            "transaction_id": data.get(
                "tran_id"
            ),
            "status": data.get(
                "status"
            ),
        }
```

**এটা শুধু architecture example।** Real gateway integration-এ provider-এর official signature/hash verification এবং API specification অনুসরণ করতে হবে।

---

# 8. PaymentService

এখন আসল business logic।

`payments/services/payment.py`

```python id="1xk6bd"
from django.db import transaction
from django.utils import timezone
from django.core.exceptions import ValidationError

from payments.models import Payment
from orders.models import Order

from inventory.services.inventory import (
    InventoryService,
)


class PaymentService:

    @classmethod
    @transaction.atomic
    def create_payment(
        cls,
        *,
        order,
        payment_method,
    ):

        if hasattr(order, "payment"):
            raise ValidationError(
                "Payment already exists."
            )

        payment = Payment.objects.create(
            order=order,
            payment_method=payment_method,
            amount=order.total_amount,
            status=Payment.Status.PENDING,
        )

        return payment
```

---

# 9. কিন্তু Online Payment হলে Gateway call কোথায়?

এখানে একটা গুরুত্বপূর্ণ production rule:

> **Database transaction-এর ভিতরে external API call করবে না।**

ভুল:

```python
@transaction.atomic
def create_payment():

    payment = Payment.objects.create()

    gateway.create_payment()

    # অনেকক্ষণ network request চলতে পারে

    return payment
```

কারণ database transaction unnecessarily open থাকবে।

Better:

```text id="z4s7wx"
1. DB transaction
      ↓
2. Payment create
      ↓
3. COMMIT
      ↓
4. Gateway API call
      ↓
5. Payment update
```

---

# 10. তাই Online Payment flow

```python id="4n9x3b"
class PaymentService:

    @classmethod
    @transaction.atomic
    def create_payment(
        cls,
        *,
        order,
        payment_method,
    ):

        payment = Payment.objects.create(
            order=order,
            payment_method=payment_method,
            amount=order.total_amount,
            status=Payment.Status.PENDING,
        )

        return payment
```

View/service layer থেকে:

```python id="uj5p0b"
payment = PaymentService.create_payment(
    order=order,
    payment_method="ONLINE",
)

gateway_response = gateway.create_payment(
    payment=payment
)
```

তারপর:

```python id="m0f6vq"
payment.status = Payment.Status.PROCESSING
payment.save(
    update_fields=[
        "status",
        "updated_at",
    ]
)
```

---

# 11. Payment Success

সবচেয়ে গুরুত্বপূর্ণ method:

```python id="c5k0e2"
@classmethod
@transaction.atomic
def handle_success(
    cls,
    *,
    payment_id,
    gateway_transaction_id,
    gateway_response=None,
):
    payment = (
        Payment.objects
        .select_for_update()
        .select_related("order")
        .get(
            id=payment_id
        )
    )

    # Idempotency
    if payment.status == Payment.Status.PAID:
        return payment

    if payment.status == Payment.Status.REFUNDED:
        raise ValidationError(
            "Refunded payment cannot become paid."
        )

    payment.status = Payment.Status.PAID
    payment.gateway_transaction_id = (
        gateway_transaction_id
    )
    payment.gateway_response = gateway_response
    payment.paid_at = timezone.now()

    payment.save(
        update_fields=[
            "status",
            "gateway_transaction_id",
            "gateway_response",
            "paid_at",
            "updated_at",
        ]
    )

    return payment
```

কিন্তু এখানেই stock deduct করা উচিত।

---

# 12. Payment Success + Inventory Deduct

Payment successful হলে:

```text id="gy0f4e"
Payment
   ↓
PAID
   ↓
InventoryService.deduct()
   ↓
Order Confirmed
```

কিন্তু আমাদের OrderItem থেকে allocation বের করতে হবে।

ধরি:

```python id="5s4s8p"
allocations = OrderItemInventoryAllocation.objects.filter(
    order_item__seller_order__order=payment.order
)
```

তারপর প্রতিটি allocation-এর জন্য deduct।

Production implementation:

```python id="slz5w6"
@classmethod
@transaction.atomic
def handle_success(
    cls,
    *,
    payment_id,
    gateway_transaction_id,
    gateway_response=None,
):

    payment = (
        Payment.objects
        .select_for_update()
        .select_related("order")
        .get(
            id=payment_id
        )
    )

    # Duplicate webhook
    if payment.status == Payment.Status.PAID:
        return payment

    if payment.status not in [
        Payment.Status.PENDING,
        Payment.Status.PROCESSING,
    ]:
        raise ValidationError(
            "Invalid payment state."
        )

    payment.status = Payment.Status.PAID
    payment.gateway_transaction_id = (
        gateway_transaction_id
    )
    payment.gateway_response = gateway_response
    payment.paid_at = timezone.now()

    payment.save(
        update_fields=[
            "status",
            "gateway_transaction_id",
            "gateway_response",
            "paid_at",
            "updated_at",
        ]
    )

    # Inventory deduction
    # এখানে OrderItemInventoryAllocation
    # অনুযায়ী deduct করা হবে।

    order = payment.order

    order.status = Order.Status.CONFIRMED

    order.save(
        update_fields=[
            "status",
            "updated_at",
        ]
    )

    return payment
```

এখানে `InventoryService.deduct()` integration-টা actual allocation table-এর সাথে করা উচিত; আগের `reserve_for_order()`-এর returned allocations database-এ `OrderItemInventoryAllocation` হিসেবে persist করতে হবে।

---

# 13. Payment Failed

Payment fail হলে reserved stock release করতে হবে।

```python id="c3y6g0"
@classmethod
@transaction.atomic
def handle_failure(
    cls,
    *,
    payment_id,
    gateway_response=None,
):

    payment = (
        Payment.objects
        .select_for_update()
        .select_related("order")
        .get(
            id=payment_id
        )
    )

    if payment.status == Payment.Status.PAID:
        raise ValidationError(
            "Paid payment cannot be marked failed."
        )

    if payment.status == Payment.Status.FAILED:
        return payment

    payment.status = Payment.Status.FAILED
    payment.gateway_response = gateway_response

    payment.save(
        update_fields=[
            "status",
            "gateway_response",
            "updated_at",
        ]
    )

    order = payment.order

    order.status = Order.Status.CANCELLED

    order.save(
        update_fields=[
            "status",
            "updated_at",
        ]
    )

    # এখানে reserved inventory release হবে

    return payment
```

---

# 14. Payment webhook

Webhook endpoint:

```text
POST /api/payments/webhook/
```

Flow:

```text id="n7p4zs"
Gateway
   ↓
POST /webhook/
   ↓
Verify signature
   ↓
Parse transaction
   ↓
Find Payment
   ↓
PaymentService.handle_success()
```

---

# 15. Signature Verification

Webhook কখনো blindly trust করবে না।

ভুল:

```python id="f0u4b1"
payment.status = "PAID"
```

কারণ attacker নিজে request পাঠাতে পারে:

```http
POST /webhook/

{
    "status": "SUCCESS"
}
```

তাই:

```python id="d9zq7r"
if not gateway.verify_webhook(
    request=request
):
    raise ValidationError(
        "Invalid webhook signature."
    )
```

তারপর:

```python id="pxj4h8"
data = gateway.parse_webhook(
    request=request
)
```

---

# 16. Webhook View

```python id="c4zq2h"
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status


class PaymentWebhookView(APIView):

    authentication_classes = []
    permission_classes = []

    def post(self, request):

        gateway = get_payment_gateway(
            request
        )

        if not gateway.verify_webhook(
            request=request
        ):
            return Response(
                {"detail": "Invalid signature"},
                status=status.HTTP_400_BAD_REQUEST,
            )

        data = gateway.parse_webhook(
            request=request
        )

        if data["status"] == "SUCCESS":

            PaymentService.handle_success(
                payment_id=data["payment_id"],
                gateway_transaction_id=(
                    data["transaction_id"]
                ),
                gateway_response=data,
            )

        elif data["status"] == "FAILED":

            PaymentService.handle_failure(
                payment_id=data["payment_id"],
                gateway_response=data,
            )

        return Response(
            {"detail": "Webhook processed"},
            status=status.HTTP_200_OK,
        )
```

---

# 17. Duplicate webhook কীভাবে prevent হচ্ছে?

ধরি gateway:

```text id="8w0u8n"
Webhook #1
SUCCESS
```

Payment:

```text
PENDING → PAID
```

আবার:

```text
Webhook #2
SUCCESS
```

`select_for_update()`:

```python id="qph4c4"
payment = (
    Payment.objects
    .select_for_update()
    .get(id=payment_id)
)
```

তারপর:

```python id="0ok5sn"
if payment.status == Payment.Status.PAID:
    return payment
```

তাই দ্বিতীয়বার:

```text
Inventory.deduct()
```

হবে না।

এটাই **idempotency**।

---

# 18. Payment + Inventory একই transaction কেন?

ধরি:

```text id="u9z7th"
Payment → PAID
Inventory → deduct()
```

Inventory deduct fail করল।

যদি আলাদা transaction হয়:

```text
Payment = PAID
Inventory = unchanged ❌
```

খুব dangerous।

তাই:

```python id="h9h8kh"
@transaction.atomic
def handle_success():
    payment → PAID
    inventory → deduct
    order → CONFIRMED
```

যেকোনো জায়গায় error:

```text id="bqj7fr"
Payment update
     ↓
Inventory error
     ↓
ROLLBACK
     ↓
Payment আবার আগের state
```

---

# 19. তবে External Gateway transaction-এর ক্ষেত্রে একটা boundary আছে

এটা মনে রাখবে:

```text id="w7j1ub"
Database transaction
       │
       ├── Order
       ├── Payment
       └── Inventory
```

এগুলো আমাদের DB।

কিন্তু:

```text id="f2m3ty"
Stripe / SSLCommerz / PayPal
```

আমাদের database transaction-এর বাইরে।

তাই:

```text id="l6w7y8"
Create Order
      ↓
Reserve Stock
      ↓
Create Payment PENDING
      ↓
COMMIT
      ↓
Call Gateway
      ↓
Webhook
      ↓
atomic DB transaction
      ↓
PAID + deduct + confirm
```

এটাই correct boundary।

---

# 20. Expired reservation

আরেকটা গুরুত্বপূর্ণ problem:

Customer payment page খুলে রেখে চলে গেল।

তখন:

```text id="b8x4kq"
reserved_quantity = 10
```

কিন্তু payment কখনো complete হলো না।

Stock forever reserved থাকলে অন্য customer কিনতে পারবে না।

তাই reservation expiry দরকার।

Order বা reservation-এ:

```python id="3w6j8a"
payment_expires_at = models.DateTimeField(
    null=True,
    blank=True,
)
```

যেমন:

```text id="p7t8x0"
Checkout
   ↓
Reserve stock
   ↓
payment_expires_at = now + 15 minutes
```

---

# 21. Celery task

ধরি:

```text id="q2s6kl"
payments/tasks.py
```

```python id="k8x0m2"
from celery import shared_task

from django.utils import timezone

from orders.models import Order
from payments.models import Payment
from payments.services.payment import PaymentService


@shared_task
def release_expired_payments():

    payments = (
        Payment.objects
        .filter(
            status=Payment.Status.PENDING,
            order__payment_expires_at__lt=timezone.now(),
        )
        .select_related("order")
    )

    for payment in payments:

        PaymentService.handle_expiry(
            payment_id=payment.id
        )
```

---

# 22. `handle_expiry()`

```python id="3t4y9k"
@classmethod
@transaction.atomic
def handle_expiry(
    cls,
    *,
    payment_id,
):

    payment = (
        Payment.objects
        .select_for_update()
        .select_related("order")
        .get(id=payment_id)
    )

    if payment.status != Payment.Status.PENDING:
        return payment

    payment.status = Payment.Status.CANCELLED

    payment.save(
        update_fields=[
            "status",
            "updated_at",
        ]
    )

    # InventoryService.release(...)
    # allocation অনুযায়ী

    order = payment.order

    order.status = Order.Status.CANCELLED

    order.save(
        update_fields=[
            "status",
            "updated_at",
        ]
    )

    return payment
```

এখানেও idempotency আছে।

যদি task দুইবার চলে:

```text
First:
PENDING → CANCELLED

Second:
CANCELLED → return
```

---

# 23. Celery schedule

Celery Beat দিয়ে প্রতি মিনিটে চালাতে পারো:

```text id="v3y8w5"
Celery Beat
    │
    ↓
প্রতি 1 minute
    │
    ↓
release_expired_payments()
```

তবে production-এ query volume বড় হলে batch processing এবং proper indexes দরকার হবে।

---

# 24. এখন পুরো Architecture

আমাদের system এখন:

```text id="9r6x7m"
                    CUSTOMER
                       │
                       ↓
                    CART
                       │
                       ↓
                    CHECKOUT
                       │
             ┌─────────┴─────────┐
             ↓                   ↓
          ADDRESS             COUPON
             │                   │
             └─────────┬─────────┘
                       ↓
                     ORDER
                       │
                       ↓
             Warehouse Allocation
                       │
                       ↓
                InventoryService
                       │
                       ↓
                   RESERVE
                       │
                       ↓
                  PAYMENT
                       │
              ┌────────┴────────┐
              ↓                 ↓
             COD              ONLINE
              │                 │
              ↓                 ↓
          CONFIRMED          GATEWAY
                                │
                                ↓
                             WEBHOOK
                                │
                       Signature Verify
                                │
                                ↓
                         PaymentService
                                │
                  ┌─────────────┴─────────────┐
                  ↓                           ↓
               SUCCESS                     FAILED
                  ↓                           ↓
              DEDUCT                       RELEASE
                  ↓                           ↓
             CONFIRMED                   CANCELLED
```

---

## সবচেয়ে গুরুত্বপূর্ণ ৫টা production rule

### Rule 1

```python
select_for_update()
```

Inventory এবং Payment state transition-এর সময় ব্যবহার করবে।

### Rule 2

```python
transaction.atomic()
```

একই business operation-এর DB changes atomic করবে।

### Rule 3

Frontend কখনো বলবে না:

```json
{
    "status": "PAID",
    "amount": 100
}
```

Backend/gateway webhook এগুলো determine করবে।

### Rule 4

Webhook **idempotent** হতে হবে।

```text
PAID → PAID
```

দ্বিতীয় webhook-এ কোনো নতুন stock deduction হবে না।

### Rule 5

External gateway API call এবং database transaction এক transaction-এর মধ্যে রাখবে না।

---

# এখন আমাদের next architecture

এখন পর্যন্ত:

```text
Cart
 ↓
CheckoutService
 ↓
InventoryService
 ↓
PaymentService
```

এখন শেষ বড় অংশ হলো **OrderService**।

সেখানে আমরা সবকিছু একত্র করব:

```text
OrderService
    │
    ├── validate cart
    ├── validate address
    ├── calculate subtotal
    ├── calculate coupon
    ├── create Order
    ├── create SellerOrder
    ├── create OrderItem
    ├── allocate warehouse
    ├── reserve inventory
    ├── create Payment
    └── clear cart
```

তারপর:

```text
PaymentService
      ↓
Webhook
      ↓
InventoryService
      ↓
OrderService
```

অর্থাৎ পরের class হবে **“Production Checkout Orchestrator — OrderService + CheckoutService + InventoryService + PaymentService একসাথে”**। সেখানে আমরা একটা সম্পূর্ণ multi-vendor checkout-এর end-to-end code flow সাজাব, including seller grouping, warehouse split, coupon, commission, stock reservation, COD/online payment এবং rollback।


---
# Class — Production Checkout Orchestrator

এবার আমরা আগের সবগুলো service একসাথে connect করব:

```text
Cart
 ↓
CheckoutService
 ↓
OrderService
 ├── Order
 ├── SellerOrder
 ├── OrderItem
 ├── Coupon
 ├── Commission
 └── Inventory Allocation
        ↓
   InventoryService
        ↓
      RESERVE
        ↓
   PaymentService
        ↓
   COD / ONLINE
```

এখানে সবচেয়ে গুরুত্বপূর্ণ লক্ষ্য:

> **একটা checkout operation-এর মাঝখানে যেকোনো validation/business error হলে database-এর partial data থাকবে না।**

---

# 1. Final Checkout Flow

ধরি customer cart-এ রেখেছে:

```text
Product A → Seller 1 → 2 pcs
Product B → Seller 1 → 1 pc
Product C → Seller 2 → 3 pcs
```

তাহলে:

```text
Order #1001
│
├── SellerOrder #1
│    ├── Product A × 2
│    └── Product B × 1
│
└── SellerOrder #2
     └── Product C × 3
```

Inventory:

```text
Product A
 ├── Dhaka Warehouse → 1 available
 └── Gazipur Warehouse → 10 available

Requested = 2

Allocation:
 ├── Dhaka → 1
 └── Gazipur → 1
```

---

# 2. একটা গুরুত্বপূর্ণ Design Decision

Checkout-এর মধ্যে সব logic রাখব না।

ভুল architecture:

```python
CheckoutView
    ├── create order
    ├── calculate coupon
    ├── reserve stock
    ├── calculate commission
    ├── payment
    └── clear cart
```

এতে View বিশাল হয়ে যাবে।

আমরা রাখব:

```text
CheckoutView
     ↓
CheckoutService
     ↓
OrderService
     ↓
InventoryService
     ↓
PaymentService
```

---

# 3. Service Responsibilities

| Service             | দায়িত্ব                          |
| ------------------- | -------------------------------- |
| `CheckoutService`   | পুরো checkout orchestrate করবে   |
| `OrderService`      | Order/SellerOrder/OrderItem তৈরি |
| `InventoryService`  | reserve/release/deduct/restore   |
| `PaymentService`    | payment create/success/failure   |
| `CouponService`     | coupon validate/calculate        |
| `CommissionService` | seller commission calculate      |

---

# 4. CouponService

আগের coupon logic-টাকে আলাদা করি।

```python
# coupons/services/coupon.py

from decimal import Decimal

from django.core.exceptions import ValidationError
from django.db import transaction
from django.utils import timezone

from coupons.models import Coupon, CouponUsage


class CouponService:

    @staticmethod
    def get_coupon(code):
        if not code:
            return None

        code = code.strip().upper()

        try:
            return Coupon.objects.get(
                code=code
            )
        except Coupon.DoesNotExist:
            raise ValidationError(
                "Invalid coupon."
            )

    @classmethod
    def validate(
        cls,
        *,
        coupon,
        user,
        subtotal,
    ):
        if not coupon:
            return Decimal("0.00")

        now = timezone.now()

        if not coupon.is_active:
            raise ValidationError(
                "Coupon is inactive."
            )

        if now < coupon.starts_at:
            raise ValidationError(
                "Coupon is not active yet."
            )

        if now > coupon.expires_at:
            raise ValidationError(
                "Coupon has expired."
            )

        if subtotal < coupon.minimum_order_amount:
            raise ValidationError(
                "Minimum order amount not reached."
            )

        if (
            coupon.usage_limit is not None
            and coupon.used_count >= coupon.usage_limit
        ):
            raise ValidationError(
                "Coupon usage limit reached."
            )

        user_usage = CouponUsage.objects.filter(
            coupon=coupon,
            user=user,
        ).count()

        if (
            coupon.usage_limit_per_user is not None
            and user_usage >= coupon.usage_limit_per_user
        ):
            raise ValidationError(
                "You have already used this coupon."
            )

        if coupon.discount_percentage is not None:

            discount = (
                subtotal
                * coupon.discount_percentage
                / Decimal("100")
            )

        elif coupon.discount_amount is not None:

            discount = coupon.discount_amount

        else:
            discount = Decimal("0.00")

        if coupon.maximum_discount is not None:
            discount = min(
                discount,
                coupon.maximum_discount,
            )

        discount = min(
            discount,
            subtotal,
        )

        return discount
```

---

# 5. CommissionService

Seller commission calculation-ও আলাদা রাখি।

```python
# sellers/services/commission.py

from decimal import Decimal


class CommissionService:

    @staticmethod
    def calculate(
        *,
        seller,
        amount,
    ):
        rate = seller.commission_rate or Decimal("0")

        commission = (
            amount * rate / Decimal("100")
        )

        seller_earning = (
            amount - commission
        )

        return {
            "commission": commission,
            "seller_earning": seller_earning,
        }
```

---

# 6. এখন OrderService

এটাই Order creation-এর দায়িত্ব নেবে।

```python
# orders/services/order.py

from django.core.exceptions import ValidationError

from orders.models import (
    Order,
    SellerOrder,
    OrderItem,
)

from sellers.services.commission import (
    CommissionService,
)
```

প্রথমে একটা helper:

```python
class OrderService:

    @staticmethod
    def group_cart_items_by_seller(cart_items):

        groups = {}

        for item in cart_items:

            seller_id = item.product.seller_id

            groups.setdefault(
                seller_id,
                []
            ).append(item)

        return groups
```

---

# 7. Order Create

```python
class OrderService:

    @classmethod
    def create_order(
        cls,
        *,
        user,
        cart_items,
        shipping_address,
        subtotal,
        discount,
        shipping_cost,
    ):

        total_amount = (
            subtotal
            + shipping_cost
            - discount
        )

        if total_amount < 0:
            total_amount = 0

        order = Order.objects.create(
            customer=user,
            shipping_address=shipping_address,

            subtotal=subtotal,
            shipping_cost=shipping_cost,
            discount=discount,
            total_amount=total_amount,

            status=Order.Status.PENDING,
        )

        return order
```

---

# 8. SellerOrder তৈরি

```python
class OrderService:

    @classmethod
    def create_seller_orders(
        cls,
        *,
        order,
        seller_groups,
    ):

        seller_orders = []

        for seller_id, items in seller_groups.items():

            seller = items[0].product.seller

            seller_subtotal = sum(
                (
                    item.variant.price
                    if item.variant
                    else item.product.price
                )
                * item.quantity
                for item in items
            )

            commission_data = (
                CommissionService.calculate(
                    seller=seller,
                    amount=seller_subtotal,
                )
            )

            seller_order = SellerOrder.objects.create(
                order=order,
                seller=seller,

                subtotal=seller_subtotal,

                commission=(
                    commission_data["commission"]
                ),

                seller_amount=(
                    commission_data["seller_earning"]
                ),

                status=SellerOrder.Status.PENDING,
            )

            seller_orders.append(
                seller_order
            )

        return seller_orders
```

**Note:** Production-এ coupon/shipping cost SellerOrder-এ কীভাবে allocate হবে সেটা business rule হিসেবে নির্ধারণ করতে হবে। উপরের code illustrative; commission সাধারণত discount-adjusted seller share-এর ওপর হবে কিনা সেটাও তোমার marketplace rule অনুযায়ী নির্ধারণ করতে হবে।

---

# 9. OrderItem Create

এখানে সবচেয়ে গুরুত্বপূর্ণ হলো **price snapshot**।

```python
class OrderService:

    @staticmethod
    def create_order_items(
        *,
        seller_order,
        cart_items,
    ):

        order_items = []

        for cart_item in cart_items:

            product = cart_item.product
            variant = cart_item.variant

            if variant:
                unit_price = variant.price
                sku = variant.sku
            else:
                unit_price = product.price
                sku = product.sku

            total_price = (
                unit_price
                * cart_item.quantity
            )

            order_item = OrderItem.objects.create(
                seller_order=seller_order,

                product=product,
                variant=variant,

                product_name=product.name,
                sku=sku,

                quantity=cart_item.quantity,

                unit_price=unit_price,
                total_price=total_price,
            )

            order_items.append(
                order_item
            )

        return order_items
```

এতে পরে product-এর price পরিবর্তন হলেও old order-এর price পরিবর্তন হবে না।

---

# 10. এখন সবচেয়ে গুরুত্বপূর্ণ অংশ — Inventory Allocation

আমাদের আগের `InventoryService.reserve_for_order()` ব্যবহার করব।

কিন্তু এবার একটা improvement করব।

Reservation-এর পর allocation information database-এ save করতে হবে:

```text
OrderItem
   │
   ├── InventoryAllocation
   │      └── Warehouse A → 5
   │
   └── InventoryAllocation
          └── Warehouse B → 3
```

---

# 11. CheckoutService

এখন পুরো orchestration।

```python
# orders/services/checkout.py

from decimal import Decimal

from django.db import transaction
from django.core.exceptions import ValidationError

from carts.models import Cart
from orders.models import Order

from coupons.services.coupon import (
    CouponService,
)

from orders.services.order import (
    OrderService,
)

from inventory.services.inventory import (
    InventoryService,
)

from payments.services.payment import (
    PaymentService,
)
```

---

# 12. `CheckoutService.checkout()`

```python
class CheckoutService:

    @classmethod
    @transaction.atomic
    def checkout(
        cls,
        *,
        user,
        shipping_address_id,
        payment_method,
        coupon_code=None,
    ):

        # --------------------------------
        # 1. Get Cart
        # --------------------------------

        cart = (
            Cart.objects
            .select_related("user")
            .prefetch_related(
                "items__product__seller",
                "items__variant",
            )
            .get(
                user=user
            )
        )

        cart_items = list(
            cart.items.all()
        )

        if not cart_items:
            raise ValidationError(
                "Cart is empty."
            )

        # --------------------------------
        # 2. Validate Address
        # --------------------------------

        shipping_address = (
            user.addresses
            .filter(
                id=shipping_address_id
            )
            .first()
        )

        if not shipping_address:
            raise ValidationError(
                "Invalid shipping address."
            )

        # --------------------------------
        # 3. Calculate Subtotal
        # --------------------------------

        subtotal = Decimal("0.00")

        for item in cart_items:

            if item.variant:
                price = item.variant.price
            else:
                price = item.product.price

            subtotal += (
                price
                * item.quantity
            )

        # --------------------------------
        # 4. Coupon
        # --------------------------------

        coupon = CouponService.get_coupon(
            coupon_code
        )

        discount = CouponService.validate(
            coupon=coupon,
            user=user,
            subtotal=subtotal,
        )

        # --------------------------------
        # 5. Shipping
        # --------------------------------

        shipping_cost = Decimal("0.00")

        # এখানে future-এ ShippingService
        # ব্যবহার করা যাবে।

        # --------------------------------
        # 6. Create Order
        # --------------------------------

        order = OrderService.create_order(
            user=user,
            cart_items=cart_items,
            shipping_address=shipping_address,
            subtotal=subtotal,
            discount=discount,
            shipping_cost=shipping_cost,
        )

        # --------------------------------
        # 7. Group by Seller
        # --------------------------------

        seller_groups = (
            OrderService.group_cart_items_by_seller(
                cart_items
            )
        )

        # --------------------------------
        # 8. Create SellerOrders
        # --------------------------------

        seller_orders = (
            OrderService.create_seller_orders(
                order=order,
                seller_groups=seller_groups,
            )
        )

        # --------------------------------
        # 9. Create OrderItems
        # --------------------------------

        for seller_order in seller_orders:

            seller_items = seller_groups[
                seller_order.seller_id
            ]

            order_items = (
                OrderService.create_order_items(
                    seller_order=seller_order,
                    cart_items=seller_items,
                )
            )

            # --------------------------------
            # 10. Reserve Inventory
            # --------------------------------

            for order_item in order_items:

                InventoryService.reserve_for_order(
                    seller=order_item.product.seller,
                    variant=order_item.variant,
                    quantity=order_item.quantity,
                    order_id=order.id,
                    created_by=user,
                )

        # --------------------------------
        # 11. Coupon Usage
        # --------------------------------

        if coupon:

            # CouponUsage create এখানে হবে
            # এবং used_count increment হবে।

            pass

        # --------------------------------
        # 12. Create Payment
        # --------------------------------

        payment = (
            PaymentService.create_payment(
                order=order,
                payment_method=payment_method,
            )
        )

        # --------------------------------
        # 13. Clear Cart
        # --------------------------------

        cart.items.all().delete()

        return {
            "order": order,
            "payment": payment,
        }
```

এখানে একটা **খুব গুরুত্বপূর্ণ correction** আছে: multi-warehouse allocation-কে শুধু reserve করে হারিয়ে ফেলা যাবে না। `reserve_for_order()` থেকে যে allocation পাওয়া যাবে সেটা `OrderItemInventoryAllocation`-এ save করতে হবে। নইলে payment success/cancel হলে কোন warehouse থেকে কত stock deduct/release করতে হবে সেটা আর নির্ভরযোগ্যভাবে জানা যাবে না।

---

# 13. তাই `reserve_for_order()` return করবে

আগের service:

```python
return allocations
```

যেখানে:

```python
[
    {
        "inventory": inventory_a,
        "quantity": 5,
    },
    {
        "inventory": inventory_b,
        "quantity": 3,
    }
]
```

তারপর:

```python
allocations = (
    InventoryService.reserve_for_order(
        seller=order_item.product.seller,
        variant=order_item.variant,
        quantity=order_item.quantity,
        order_id=order.id,
        created_by=user,
    )
)
```

তারপর:

```python
for allocation in allocations:

    OrderItemInventoryAllocation.objects.create(
        order_item=order_item,
        inventory=allocation["inventory"],
        quantity=allocation["quantity"],
    )
```

এটাই পরে PaymentService-এর জন্য source of truth হবে।

---

# 14. Full Inventory Lifecycle

এখন ধরো:

```text
OrderItem
quantity = 15
```

Warehouse:

```text
Dhaka       available = 8
Gazipur     available = 20
```

Allocation:

```text
Dhaka       → 8
Gazipur     → 7
```

Database:

```text
OrderItemInventoryAllocation

OrderItem 1001
    │
    ├── Inventory Dhaka      8
    └── Inventory Gazipur    7
```

---

# 15. Online Payment

Checkout শেষে:

```text
Order = PENDING
Payment = PENDING
Inventory = RESERVED
```

Gateway URL return:

```json
{
    "order_id": "1001",
    "payment_id": "5001",
    "payment_url": "..."
}
```

Customer gateway-তে যায়।

---

# 16. Successful Webhook

Gateway:

```text
SUCCESS
```

Webhook:

```text
POST /api/payments/webhook/
```

তারপর:

```python
PaymentService.handle_success(
    payment_id=payment_id,
    gateway_transaction_id=transaction_id,
)
```

Service:

```text
Payment
   ↓
PENDING
   ↓
PAID
   ↓
InventoryService.deduct()
   ↓
reserved -= quantity
quantity -= quantity
   ↓
Order = CONFIRMED
```

---

# 17. Payment Failure

```text
Payment
   ↓
FAILED
   ↓
InventoryService.release()
   ↓
reserved_quantity -= quantity
   ↓
Order = CANCELLED
```

---

# 18. COD Flow

COD একটু আলাদা।

Checkout:

```text
Order
 ↓
Reserve stock
 ↓
Payment(PENDING, COD)
 ↓
Order = CONFIRMED
```

এখানে online gateway নেই।

Delivery-এর সময়:

```text
Courier
   ↓
Cash collected
   ↓
Payment = PAID
   ↓
Inventory already reserved
   ↓
Inventory deduct
```

COD-এর business rule তুমি চাইলে fulfillment-এর সময়েও deduct করতে পারো; গুরুত্বপূর্ণ হলো একই stock যেন দ্বিতীয়বার deduct না হয়।

---

# 19. Rollback কীভাবে কাজ করবে?

ধরি:

```text
Step 1 → Order created
Step 2 → SellerOrder created
Step 3 → OrderItem created
Step 4 → Inventory reserved
Step 5 → Payment created
Step 6 → Error ❌
```

কারণ:

```text
CouponUsage creation failed
```

আমাদের:

```python
@transaction.atomic
```

এর কারণে:

```text
ROLLBACK
```

হবে।

ফলে:

```text
Order ❌
SellerOrder ❌
OrderItem ❌
Inventory reservation ❌
Payment ❌
```

সব rollback।

এটাই atomic checkout-এর মূল সুবিধা।

---

# 20. কিন্তু Gateway call এখানে করবে না

এটা অত্যন্ত গুরুত্বপূর্ণ।

`CheckoutService`:

```text
DB transaction
   │
   ├── Order
   ├── SellerOrder
   ├── OrderItem
   ├── Inventory Reserve
   └── Payment PENDING
        │
        ↓
     COMMIT
```

তারপর বাইরে:

```text
Payment Gateway API
```

অর্থাৎ:

```text
CheckoutService
      ↓
DB COMMIT
      ↓
Payment Gateway
      ↓
Webhook
      ↓
PaymentService
```

**Gateway API call-কে `transaction.atomic()`-এর ভিতরে রাখবে না।**

---

# 21. Coupon Usage অবশ্যই atomic

Checkout-এ:

```python
if coupon:

    CouponUsage.objects.create(
        coupon=coupon,
        user=user,
        order=order,
    )

    coupon.used_count += 1

    coupon.save(
        update_fields=[
            "used_count",
            "updated_at",
        ]
    )
```

কিন্তু concurrent coupon checkout হলে race হতে পারে।

Production version:

```python
coupon = (
    Coupon.objects
    .select_for_update()
    .get(
        id=coupon.id
    )
)
```

তারপর আবার usage limit check করতে হবে।

অর্থাৎ:

```text
Checkout A
   ↓
lock coupon
   ↓
check usage
   ↓
increment
   ↓
commit
   ↓
unlock

Checkout B
   ↓
gets lock
   ↓
check latest usage
```

এভাবে usage limit overshoot prevent করা যায়।

---

# 22. আরেকটি গুরুত্বপূর্ণ race condition

ধরি coupon usage limit:

```text
usage_limit = 100
used_count = 99
```

দুই customer একই সময়ে checkout করল।

Lock ছাড়া:

```text
A sees 99
B sees 99

A → 100
B → 100

দুজনেই allowed ❌
```

Lock সহ:

```text
A → lock
A → 100
A → commit

B → lock
B → sees 100
B → reject
```

---

# 23. Final Production Flow

এখন পুরো system:

```text
                         CUSTOMER
                            │
                            ↓
                           CART
                            │
                            ↓
                     CheckoutService
                            │
             ┌──────────────┼──────────────┐
             ↓              ↓              ↓
          Address         Coupon         Cart
             │              │
             └──────────────┼──────────────┘
                            ↓
                         Order
                            │
                            ↓
                    Seller Grouping
                            │
                ┌───────────┴───────────┐
                ↓                       ↓
          SellerOrder 1           SellerOrder 2
                │                       │
                ↓                       ↓
           OrderItems              OrderItems
                │                       │
                └───────────┬───────────┘
                            ↓
                  Warehouse Allocation
                            │
                            ↓
                   InventoryService
                            │
                         RESERVE
                            │
                            ↓
                     PaymentService
                            │
                ┌───────────┴───────────┐
                ↓                       ↓
               COD                    ONLINE
                │                       │
                ↓                       ↓
           CONFIRMED                Gateway
                                        │
                                        ↓
                                     Webhook
                                        │
                                        ↓
                                Signature Verify
                                        │
                                        ↓
                                  PaymentService
                                        │
                           ┌────────────┴────────────┐
                           ↓                         ↓
                        SUCCESS                   FAILED
                           ↓                         ↓
                 Inventory.deduct()        Inventory.release()
                           ↓                         ↓
                     Order Confirmed          Order Cancelled
```

---

# 24. Service Layer-এর final responsibility

```text
id="3e4v8j"
orders/
│
└── services/
    ├── checkout.py
    └── order.py

inventory/
│
└── services/
    ├── inventory.py
    └── warehouse.py

payments/
│
└── services/
    └── payment.py

coupons/
│
└── services/
    └── coupon.py

sellers/
│
└── services/
    └── commission.py
```

এখন architecture অনেক clean:

```text
View
 ↓
Service
 ↓
Model
```

View-এর মধ্যে business logic থাকবে না।

---

## সবচেয়ে গুরুত্বপূর্ণ production checklist

এই checkout system-এ এখন যেগুলো cover হয়েছে:

* ✅ Multi-vendor order
* ✅ SellerOrder
* ✅ OrderItem price snapshot
* ✅ Seller grouping
* ✅ Coupon calculation
* ✅ Coupon usage
* ✅ Seller commission
* ✅ Multi-warehouse allocation
* ✅ Inventory reservation
* ✅ `select_for_update()`
* ✅ `transaction.atomic()`
* ✅ Overselling prevention
* ✅ Inventory transaction logging
* ✅ Payment state
* ✅ COD
* ✅ Online payment
* ✅ Gateway abstraction
* ✅ Webhook
* ✅ Webhook signature verification
* ✅ Duplicate webhook protection
* ✅ Payment failure → stock release
* ✅ Payment success → stock deduction
* ✅ Expired payment → reservation release
* ✅ Celery-based expiry handling
* ✅ Database rollback

### তবে production-ready করার আগে ৩টি জিনিস আরও শক্ত করতে হবে

**১. Checkout idempotency key**
একই customer double-click করলে যেন দুইটা Order না হয়।

**২. Address snapshot**
Customer পরে saved address edit করলেও historical Order-এর address যেন পরিবর্তন না হয়।

**৩. Exact warehouse allocation persistence**
`OrderItemInventoryAllocation`-এ allocation save করে তারপর payment success/failure/return-এর সময় **সেই exact allocation** ব্যবহার করতে হবে।

এই তিনটি যোগ করলে এরপর **Order State Machine + Cancellation + Refund + Return + Payment Reconciliation** layer করা যাবে—যেটাই e-commerce backend-এর পরের বড় production stage।


----
হ্যাঁ। এই ৩টি আগে শক্ত করা উচিত। এগুলো যোগ করলে checkout flow অনেক বেশি production-grade হবে।

আমরা order flow-টা এভাবে রাখব:

```text
Client
  │
  │ POST /checkout/
  │ Idempotency-Key: abc-123
  ▼
CheckoutService
  │
  ├── 1. Idempotency check
  │
  ├── 2. Address snapshot
  │
  ├── 3. Create Order
  │
  ├── 4. Group items by Seller
  │
  ├── 5. Create SellerOrder
  │
  ├── 6. Create OrderItem
  │
  ├── 7. Reserve inventory
  │       └── Warehouse A → 5
  │       └── Warehouse B → 3
  │
  ├── 8. Save OrderItemInventoryAllocation
  │
  ├── 9. Coupon + commission
  │
  └── 10. Create Payment(PENDING)
             │
             ├── COD
             └── ONLINE
```

তারপর payment event:

```text
Payment Success
      │
      ▼
PaymentService
      │
      ├── Lock Payment
      ├── Read exact allocations
      ├── Deduct exact inventory
      ├── Payment → PAID
      └── Order → CONFIRMED
```

আর failure হলে:

```text
Payment Failed
      │
      ▼
PaymentService
      │
      ├── Lock Payment
      ├── Read exact allocations
      ├── Release reservation
      ├── Payment → FAILED
      └── Order → CANCELLED
```

---

# 1. Checkout Idempotency

প্রথমে আলাদা model করি।

```python
class CheckoutIdempotency(BaseModel):
    key = models.CharField(
        max_length=100,
        unique=True,
        db_index=True,
    )

    user = models.ForeignKey(
        "accounts.User",
        on_delete=models.CASCADE,
        related_name="checkout_idempotencies",
    )

    order = models.OneToOneField(
        "orders.Order",
        on_delete=models.CASCADE,
        related_name="idempotency_record",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["key", "user"],
                name="unique_checkout_idempotency_key_user",
            )
        ]
```

এখানে:

```text
customer
   │
   ├── key: checkout-abc-123
   │
   └── order: ORD-10001
```

Customer আবার একই request করলে:

```text
key = checkout-abc-123
```

আমরা existing record খুঁজব।

পেলে নতুন Order বানাব না।

```python
existing = CheckoutIdempotency.objects.filter(
    key=idempotency_key,
    user=request.user,
).select_related("order").first()

if existing:
    return existing.order
```

### কিন্তু একটা গুরুত্বপূর্ণ সমস্যা

শুধু এই check যথেষ্ট না।

দুটি request একই সময়ে এলে:

```text
Request A ──┐
            ├── check → নেই
Request B ──┘
            └── check → নেই
```

দুটিই Order বানাতে পারে।

তাই database-level unique constraint + `transaction.atomic()` ব্যবহার করতে হবে।

Conceptually:

```python
@transaction.atomic
def checkout(...):
    try:
        idempotency = CheckoutIdempotency.objects.create(
            key=idempotency_key,
            user=user,
            order=order,
        )
    except IntegrityError:
        return (
            CheckoutIdempotency.objects
            .select_related("order")
            .get(
                key=idempotency_key,
                user=user,
            )
            .order
        )
```

Production-এ আরও ভালো pattern হলো **Order তৈরি করার আগে idempotency record reserve করা**, তারপর সেই operation-এর ফলাফল record করা।

---

# 2. Address Snapshot

এটা খুব গুরুত্বপূর্ণ।

ধরো আজ customer checkout করল:

```text
Name: Atiar
Address: Dhaka
Phone: 01711111111
```

Order হলো:

```text
ORD-1001
```

দুই মাস পরে customer saved address edit করল:

```text
Address: Rajbari
Phone: 01822222222
```

যদি Order শুধু রাখে:

```python
shipping_address = ForeignKey(Address)
```

তাহলে historical order-এর address বদলে যেতে পারে।

এটা আমরা চাই না।

---

## Order-এ snapshot fields

```python
class Order(BaseModel):

    order_number = models.CharField(
        max_length=50,
        unique=True,
    )

    customer = models.ForeignKey(
        "accounts.User",
        on_delete=models.PROTECT,
        related_name="orders",
    )

    # Optional reference to original saved address
    shipping_address = models.ForeignKey(
        "accounts.Address",
        on_delete=models.PROTECT,
        null=True,
        blank=True,
        related_name="orders",
    )

    # Historical snapshot
    shipping_full_name = models.CharField(
        max_length=150
    )

    shipping_phone_number = models.CharField(
        max_length=20
    )

    shipping_address_line_1 = models.CharField(
        max_length=255
    )

    shipping_address_line_2 = models.CharField(
        max_length=255,
        blank=True,
    )

    shipping_city = models.CharField(
        max_length=100
    )

    shipping_state = models.CharField(
        max_length=100,
        blank=True,
    )

    shipping_postal_code = models.CharField(
        max_length=20
    )

    shipping_country = models.CharField(
        max_length=100,
        default="Bangladesh",
    )
```

Checkout-এর সময়:

```python
address = Address.objects.get(
    id=shipping_address_id,
    user=user,
)
```

তারপর:

```python
Order.objects.create(
    customer=user,

    shipping_address=address,

    shipping_full_name=address.full_name,
    shipping_phone_number=address.phone_number,

    shipping_address_line_1=address.address_line_1,
    shipping_address_line_2=address.address_line_2,

    shipping_city=address.city,
    shipping_state=address.state,
    shipping_postal_code=address.postal_code,
    shipping_country=address.country,
)
```

এখন:

```text
Address
   ↓
Current saved address

Order
   ↓
Historical snapshot
```

Customer Address পরিবর্তন করলেও Order পরিবর্তন হবে না।

---

# 3. Exact Warehouse Allocation Persistence

এটাই inventory architecture-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

ধরো:

```text
Product Variant: iPhone 15

Warehouse A
quantity = 5
available = 5

Warehouse B
quantity = 10
available = 10
```

Customer order করল:

```text
quantity = 8
```

InventoryService বলল:

```text
Warehouse A → 5
Warehouse B → 3
```

এই তথ্য শুধু memory-তে রাখা যাবে না।

Database-এ save করতে হবে:

```text
OrderItem
    │
    ├── Allocation
    │      Warehouse A → 5
    │
    └── Allocation
           Warehouse B → 3
```

আমাদের model:

```python
class OrderItemInventoryAllocation(BaseModel):

    order_item = models.ForeignKey(
        "orders.OrderItem",
        on_delete=models.CASCADE,
        related_name="inventory_allocations",
    )

    inventory = models.ForeignKey(
        "inventory.Inventory",
        on_delete=models.PROTECT,
        related_name="order_allocations",
    )

    quantity = models.PositiveIntegerField()

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["order_item", "inventory"],
                name="unique_order_item_inventory",
            )
        ]
```

---

# Checkout-এ allocation save

ধরো InventoryService return করল:

```python
allocations = [
    {
        "inventory": inventory_a,
        "quantity": 5,
    },
    {
        "inventory": inventory_b,
        "quantity": 3,
    },
]
```

তারপর:

```python
for allocation in allocations:
    OrderItemInventoryAllocation.objects.create(
        order_item=order_item,
        inventory=allocation["inventory"],
        quantity=allocation["quantity"],
    )
```

এখন database-এ exact record আছে।

---

# Payment success-এর সময়

আগে যদি আমরা শুধু বলি:

```python
InventoryService.deduct(
    variant=variant,
    quantity=8,
)
```

তাহলে সমস্যা হতে পারে।

কারণ checkout-এর সময় allocation ছিল:

```text
A → 5
B → 3
```

কিন্তু payment success-এর সময় Warehouse A-তে অন্য order-এর কারণে stock পরিবর্তিত হয়ে গেছে।

তাই payment success-এ **আবার warehouse নির্বাচন করা যাবে না।**

বরং database থেকে exact allocation পড়ব:

```python
allocations = (
    OrderItemInventoryAllocation.objects
    .select_related("inventory")
    .filter(
        order_item__seller_order__order=order
    )
)
```

তারপর:

```python
for allocation in allocations:
    InventoryService.deduct(
        inventory_id=allocation.inventory_id,
        quantity=allocation.quantity,
        order_id=order.id,
    )
```

অর্থাৎ:

```text
Checkout
   ↓
A = 5
B = 3
   ↓
SAVE

Payment Success
   ↓
READ
   ↓
A = 5
B = 3
   ↓
DEDUCT
```

---

# Payment failure

একই allocation ব্যবহার করে:

```text
A → 5 reserved
B → 3 reserved
```

Payment failed:

```text
A → release 5
B → release 3
```

নতুন warehouse search করা যাবে না।

---

# Return-এর সময়

Customer যদি পরে return করে:

```text
Original allocation

Warehouse A → 5
Warehouse B → 3
```

Return হলে exact allocation অনুযায়ী inventory restore করার strategy থাকবে।

যদি business rule হয় original warehouse-এই stock ফেরত যাবে:

```text
A → +5
B → +3
```

তাহলে allocation history থেকেই সেটা জানা যাবে।

---

# এখন CheckoutService-এর structure

Production architecture-এ আমি এটাকে এভাবে ভাগ করব:

```text
CheckoutService
│
├── validate_checkout()
│
├── get_or_create_idempotency()
│
├── create_order()
│
├── create_seller_orders()
│
├── create_order_items()
│
├── reserve_inventory()
│
├── persist_inventory_allocations()
│
├── apply_coupon()
│
├── calculate_commission()
│
└── create_payment()
```

কিন্তু CheckoutService নিজে সব business logic করবে না।

বরং:

```text
CheckoutService
      │
      ├── OrderService
      │
      ├── InventoryService
      │
      ├── CouponService
      │
      ├── CommissionService
      │
      └── PaymentService
```

---

# Final production flow

সবগুলো একসাথে করলে:

```text
                    CHECKOUT
                       │
                       ▼
              Idempotency Check
                       │
                ┌──────┴──────┐
                │             │
             Exists         New Key
                │             │
                ▼             ▼
          Return Order    Address Validate
                              │
                              ▼
                       Address Snapshot
                              │
                              ▼
                       Create Order
                              │
                              ▼
                    Group by Seller
                              │
                              ▼
                    Create SellerOrder
                              │
                              ▼
                       Create Items
                              │
                              ▼
                    Reserve Inventory
                              │
                 ┌────────────┴────────────┐
                 ▼                         ▼
            Warehouse A                Warehouse B
                 5                         3
                 └────────────┬────────────┘
                              ▼
                 Save Allocation Records
                              │
                              ▼
                       Apply Coupon
                              │
                              ▼
                     Calculate Commission
                              │
                              ▼
                     Create Payment
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
                   COD               ONLINE
                    │                   │
                    ▼                   ▼
              Order Pending       Gateway Payment
                                        │
                                        ▼
                                   Webhook
                                        │
                              ┌─────────┴─────────┐
                              ▼                   ▼
                           SUCCESS              FAILED
                              │                   │
                              ▼                   ▼
                     Exact Allocation      Exact Allocation
                         Deduct                 Release
                              │                   │
                              ▼                   ▼
                     Order Confirmed       Order Cancelled
```

## এই ৩টা যোগ করার পর

আমাদের e-commerce backend-এর foundation হবে:

```text
✅ Multi-vendor Order
✅ SellerOrder
✅ OrderItem
✅ Address Snapshot
✅ Checkout Idempotency
✅ Multi-warehouse Inventory
✅ Stock Reservation
✅ Exact Warehouse Allocation
✅ Inventory Transaction Audit
✅ Coupon
✅ Seller Commission
✅ COD
✅ Online Payment
✅ Payment Webhook
✅ Payment Idempotency
```

এর পরের বড় layer সত্যিই হবে:

```text
Order State Machine
        ↓
Cancellation
        ↓
Refund
        ↓
Return
        ↓
Exchange
        ↓
Payment Reconciliation
        ↓
Settlement / Seller Payout
```

এখানে গিয়ে আমরা **Order + Payment + Inventory-এর state transition** একসাথে design করব—যাতে `CANCELLED`, `PAID`, `SHIPPED`, `DELIVERED`, `REFUNDED`, `RETURNED` ইত্যাদি status ইচ্ছেমতো API থেকে পরিবর্তন করা না যায়।


----
ঠিক। এখন আমাদের **Order + Payment + Inventory State Machine** design করতে হবে। Production e-commerce-এ সবচেয়ে গুরুত্বপূর্ণ বিষয় হলো—**status field শুধু database-এর একটা string না; status change-এর নির্দিষ্ট rule থাকবে।**

---

# 1. প্রথমে পুরো State Architecture

আমরা তিনটা আলাদা state machine রাখব:

```text
Order State
Payment State
Inventory State
```

তবে এগুলো একে অপরের সাথে coordinated থাকবে।

### Order

```text
PENDING
   │
   ├──→ CONFIRMED
   │       │
   │       ├──→ PROCESSING
   │       │       │
   │       │       ├──→ SHIPPED
   │       │       │       │
   │       │       │       └──→ DELIVERED
   │       │       │
   │       │       └──→ CANCELLED
   │       │
   │       └──→ CANCELLED
   │
   └──→ CANCELLED
```

Refund/return-এর জন্য Order-এর মূল status দিয়ে সবকিছু represent করব না। আলাদা `Return` এবং `Refund` state রাখাই ভালো।

---

# 2. Payment State Machine

```text
PENDING
   │
   ├──→ PROCESSING
   │       │
   │       ├──→ PAID
   │       │
   │       └──→ FAILED
   │
   └──→ CANCELLED

PAID
  │
  └──→ REFUNDED
```

খেয়াল করো:

```text
FAILED → PAID
```

এভাবে arbitrary transition করা যাবে না।

---

# 3. Inventory State আসলে কী?

Inventory-এর ক্ষেত্রে শুধু:

```python
status = "AVAILABLE"
```

রাখলে production architecture দুর্বল হবে।

আমাদের মূল state হচ্ছে:

```text
quantity
reserved_quantity
available_quantity
```

যেখানে:

```python
available_quantity = quantity - reserved_quantity
```

উদাহরণ:

```text
quantity = 100
reserved = 20

available = 80
```

Order checkout:

```text
100 → quantity
20  → reserved

available = 80
```

Payment success:

```text
quantity → 92
reserved → 12
```

কারণ 8টা বিক্রি হয়েছে।

Payment failure:

```text
quantity → 100
reserved → 12
```

অর্থাৎ reservation release হয়েছে।

---

# 4. সবচেয়ে গুরুত্বপূর্ণ Rule

Client কখনো এমন request করতে পারবে না:

```http
PATCH /orders/123/
```

```json
{
    "status": "DELIVERED"
}
```

অথবা:

```http
PATCH /payments/123/
```

```json
{
    "status": "PAID"
}
```

অথবা:

```http
PATCH /inventory/123/
```

```json
{
    "quantity": 10000
}
```

এই তিনটা production-এ dangerous।

Status transition হবে **Service Layer** দিয়ে।

---

# 5. Order Model

আমি Order status একটু পরিষ্কার করে সাজাব:

```python
class Order(BaseModel):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        CONFIRMED = "CONFIRMED", "Confirmed"
        PROCESSING = "PROCESSING", "Processing"
        SHIPPED = "SHIPPED", "Shipped"
        DELIVERED = "DELIVERED", "Delivered"
        CANCELLED = "CANCELLED", "Cancelled"

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING,
        db_index=True,
    )
```

---

# 6. Allowed Order Transitions

এটা সবচেয়ে গুরুত্বপূর্ণ অংশ।

```python
ORDER_TRANSITIONS = {
    Order.Status.PENDING: {
        Order.Status.CONFIRMED,
        Order.Status.CANCELLED,
    },

    Order.Status.CONFIRMED: {
        Order.Status.PROCESSING,
        Order.Status.CANCELLED,
    },

    Order.Status.PROCESSING: {
        Order.Status.SHIPPED,
        Order.Status.CANCELLED,
    },

    Order.Status.SHIPPED: {
        Order.Status.DELIVERED,
    },

    Order.Status.DELIVERED: set(),

    Order.Status.CANCELLED: set(),
}
```

এখন:

```text
PENDING → CONFIRMED
```

valid।

কিন্তু:

```text
DELIVERED → PENDING
```

invalid।

আবার:

```text
CANCELLED → CONFIRMED
```

invalid।

---

# 7. OrderStateService

```python
from django.db import transaction


class OrderStateService:

    @staticmethod
    @transaction.atomic
    def transition(*, order_id, new_status):

        order = (
            Order.objects
            .select_for_update()
            .get(id=order_id)
        )

        current_status = order.status

        allowed_statuses = ORDER_TRANSITIONS.get(
            current_status,
            set(),
        )

        if new_status not in allowed_statuses:
            raise ValueError(
                f"Invalid order transition: "
                f"{current_status} -> {new_status}"
            )

        order.status = new_status
        order.save(
            update_fields=["status", "updated_at"]
        )

        return order
```

এখন কেউ:

```python
OrderStateService.transition(
    order_id=order.id,
    new_status="DELIVERED",
)
```

করলে যদি Order বর্তমানে `PENDING` হয়:

```text
PENDING → DELIVERED
```

সরাসরি reject হবে।

---

# 8. Payment State Machine

```python
PAYMENT_TRANSITIONS = {
    Payment.Status.PENDING: {
        Payment.Status.PROCESSING,
        Payment.Status.FAILED,
        Payment.Status.CANCELLED,
    },

    Payment.Status.PROCESSING: {
        Payment.Status.PAID,
        Payment.Status.FAILED,
    },

    Payment.Status.PAID: {
        Payment.Status.REFUNDED,
    },

    Payment.Status.FAILED: set(),

    Payment.Status.CANCELLED: set(),

    Payment.Status.REFUNDED: set(),
}
```

তাহলে:

```text
PENDING → PROCESSING
PROCESSING → PAID
PAID → REFUNDED
```

valid।

কিন্তু:

```text
FAILED → PAID
REFUNDED → PAID
PAID → PENDING
```

invalid।

---

# 9. PaymentStateService

```python
class PaymentStateService:

    @staticmethod
    @transaction.atomic
    def transition(*, payment_id, new_status):

        payment = (
            Payment.objects
            .select_for_update()
            .get(id=payment_id)
        )

        current_status = payment.status

        allowed_statuses = PAYMENT_TRANSITIONS.get(
            current_status,
            set(),
        )

        if new_status not in allowed_statuses:
            raise ValueError(
                f"Invalid payment transition: "
                f"{current_status} -> {new_status}"
            )

        payment.status = new_status

        payment.save(
            update_fields=[
                "status",
                "updated_at",
            ]
        )

        return payment
```

---

# 10. কিন্তু একটা গুরুত্বপূর্ণ বিষয়

শুধু:

```python
PaymentStateService.transition(
    payment_id=1,
    new_status="PAID"
)
```

করাই যথেষ্ট না।

কারণ `PAID` হওয়ার সাথে business operation আছে।

Payment `PAID` হলে:

```text
Payment
   ↓
Inventory deduct
   ↓
Order confirm
```

তাই আমরা আলাদা:

```text
PaymentStateService
```

এবং:

```text
PaymentService
```

রাখব।

---

# 11. PaymentService.handle_success()

এখানে আসল orchestration হবে।

```python
class PaymentService:

    @staticmethod
    @transaction.atomic
    def handle_success(
        *,
        payment_id,
        gateway_transaction_id,
        gateway_response,
    ):

        payment = (
            Payment.objects
            .select_for_update()
            .select_related("order")
            .get(id=payment_id)
        )

        # Idempotency
        if payment.status == Payment.Status.PAID:
            return payment

        if payment.status not in [
            Payment.Status.PENDING,
            Payment.Status.PROCESSING,
        ]:
            raise ValueError(
                f"Payment cannot become PAID "
                f"from {payment.status}"
            )

        # 1. Deduct exact inventory allocation
        InventoryService.deduct_for_payment(
            order=payment.order,
        )

        # 2. Payment → PAID
        payment.status = Payment.Status.PAID
        payment.gateway_transaction_id = (
            gateway_transaction_id
        )
        payment.gateway_response = gateway_response
        payment.paid_at = timezone.now()

        payment.save(
            update_fields=[
                "status",
                "gateway_transaction_id",
                "gateway_response",
                "paid_at",
                "updated_at",
            ]
        )

        # 3. Order → CONFIRMED
        OrderStateService.transition(
            order_id=payment.order_id,
            new_status=Order.Status.CONFIRMED,
        )

        return payment
```

এখানে পুরো operation:

```text
BEGIN TRANSACTION
       │
       ├── lock Payment
       ├── deduct exact inventory
       ├── Payment = PAID
       └── Order = CONFIRMED
       │
COMMIT
```

যদি মাঝখানে error হয়:

```text
ROLLBACK
```

---

# 12. Payment Failure

Payment failure হলে inventory আবার warehouse search করবে না।

আগে save করা allocation ব্যবহার করবে।

```python
class PaymentService:

    @staticmethod
    @transaction.atomic
    def handle_failure(
        *,
        payment_id,
        gateway_response=None,
    ):

        payment = (
            Payment.objects
            .select_for_update()
            .select_related("order")
            .get(id=payment_id)
        )

        if payment.status in [
            Payment.Status.FAILED,
            Payment.Status.CANCELLED,
        ]:
            return payment

        if payment.status == Payment.Status.PAID:
            raise ValueError(
                "Paid payment cannot be marked failed."
            )

        InventoryService.release_for_payment(
            order=payment.order,
        )

        payment.status = Payment.Status.FAILED
        payment.gateway_response = gateway_response

        payment.save(
            update_fields=[
                "status",
                "gateway_response",
                "updated_at",
            ]
        )

        OrderStateService.transition(
            order_id=payment.order_id,
            new_status=Order.Status.CANCELLED,
        )

        return payment
```

---

# 13. তাহলে InventoryService কী করবে?

InventoryService status পরিবর্তনের বদলে **stock operation** করবে।

```text
InventoryService
│
├── reserve()
├── release()
├── deduct()
├── restore()
└── adjust()
```

### Reserve

```text
quantity = 100
reserved = 0

reserve 10

quantity = 100
reserved = 10
available = 90
```

### Release

```text
reserved = 10

release 10

reserved = 0
```

### Deduct

```text
quantity = 100
reserved = 10

deduct 10

quantity = 90
reserved = 0
```

### Restore

Return হলে:

```text
quantity = 90

restore 10

quantity = 100
```

---

# 14. State Machine + Inventory একসাথে

এখন পুরো business relationship দেখো:

### Checkout

```text
Order
PENDING

Payment
PENDING

Inventory
RESERVED
```

---

### Online payment success

```text
Payment
PENDING
   ↓
PROCESSING
   ↓
PAID

Inventory
RESERVED
   ↓
DEDUCTED

Order
PENDING
   ↓
CONFIRMED
```

---

### Payment failed

```text
Payment
PENDING
   ↓
FAILED

Inventory
RESERVED
   ↓
RELEASED

Order
PENDING
   ↓
CANCELLED
```

---

### Shipment

```text
Order
CONFIRMED
   ↓
PROCESSING
   ↓
SHIPPED
```

---

### Delivery

```text
SHIPPED
   ↓
DELIVERED
```

---

# 15. SellerOrder-এরও State Machine লাগবে

কারণ Multi-vendor system-এ:

```text
Order #1001

Seller A → SHIPPED
Seller B → PROCESSING
Seller C → DELIVERED
```

তাই `SellerOrder`-এর status আলাদাভাবে transition হবে।

```python
SELLER_ORDER_TRANSITIONS = {
    SellerOrder.Status.PENDING: {
        SellerOrder.Status.PROCESSING,
        SellerOrder.Status.CANCELLED,
    },

    SellerOrder.Status.PROCESSING: {
        SellerOrder.Status.SHIPPED,
        SellerOrder.Status.CANCELLED,
    },

    SellerOrder.Status.SHIPPED: {
        SellerOrder.Status.DELIVERED,
    },

    SellerOrder.Status.DELIVERED: set(),

    SellerOrder.Status.CANCELLED: set(),
}
```

---

# 16. Parent Order status কীভাবে হবে?

এখানে একটা গুরুত্বপূর্ণ production rule আছে।

ধরো:

```text
SellerOrder A → DELIVERED
SellerOrder B → SHIPPED
SellerOrder C → PROCESSING
```

Parent `Order`-কে সরাসরি client update করতে দেওয়া যাবে না।

বরং `OrderStatusService` seller orders দেখে overall status calculate করবে।

যেমন:

```text
All SellerOrders PROCESSING
        ↓
Order PROCESSING
```

সব seller order delivered হলে:

```text
All SellerOrders DELIVERED
        ↓
Order DELIVERED
```

অর্থাৎ:

```text
SellerOrder
     ↓
Order status aggregation
```

এটা খুব গুরুত্বপূর্ণ।

---

# 17. API Architecture

শেষ পর্যন্ত API হবে এরকম:

```text
POST /checkout/
```

Customer checkout করবে।

কিন্তু:

```text
PATCH /orders/{id}/status/
```

দিয়ে arbitrary status change করা যাবে না।

Seller-এর জন্য:

```text
POST /seller-orders/{id}/process/
POST /seller-orders/{id}/ship/
POST /seller-orders/{id}/deliver/
POST /seller-orders/{id}/cancel/
```

অথবা আরও clean ভাবে:

```text
POST /seller-orders/{id}/transition/
```

কিন্তু backend transition rules enforce করবে।

Payment:

```text
POST /payments/webhook/
```

Gateway event থেকে Payment state change হবে।

Customer:

```text
POST /orders/{id}/cancel/
```

করতে পারবে **শুধু cancellation policy-এর মধ্যে থাকলে**।

---

# 18. সবচেয়ে গুরুত্বপূর্ণ Architecture

শেষ পর্যন্ত আমাদের structure হবে:

```text
                    API
                     │
                     ▼
              CheckoutService
                     │
        ┌────────────┼────────────┐
        ▼            ▼            ▼
   OrderService  InventoryService CouponService
        │            │
        │            ▼
        │       InventoryTransaction
        │
        ▼
    OrderStateService


Payment Webhook
       │
       ▼
PaymentService
       │
       ├── PaymentStateService
       │
       ├── InventoryService
       │
       └── OrderStateService
```

এখানে সবচেয়ে গুরুত্বপূর্ণ principle:

> **Model শুধু data রাখবে, Serializer input validate করবে, ViewSet request handle করবে, আর business state transition Service Layer control করবে।**

পরের layer-এ আমরা এই state machine-এর ওপর **Cancellation → Refund → Return → Exchange → Payment Reconciliation** বসাতে পারি। তখন `OrderCancellationService`, `RefundService`, `ReturnService`, এবং শেষ পর্যন্ত gateway-vs-database reconciliation flow তৈরি হবে।

---
হ্যাঁ। এখন আমরা **E-commerce Post-Payment Lifecycle** layer-এ যাব। এখানে সবচেয়ে গুরুত্বপূর্ণ হলো—Cancellation, Refund, Return, Exchange—এগুলোকে শুধু status update হিসেবে না দেখে **transactional business workflow** হিসেবে তৈরি করা।

---

# Production Stage: Cancellation → Refund → Return → Exchange → Reconciliation

পুরো architecture:

```text
Order
 │
 ├── Cancellation
 │       │
 │       └── Refund
 │
 ├── Shipment
 │       │
 │       └── Delivery
 │
 └── Return
         │
         ├── Refund
         │
         └── Exchange
```

আর payment side:

```text
Payment
   │
   ├── Paid
   │
   ├── Refund Requested
   │
   ├── Refund Processing
   │
   └── Refunded
```

সবশেষে:

```text
Gateway
   │
   │ reconciliation
   ▼
Our Database
```

---

# 1. প্রথমে Cancellation

Cancellation-এর জন্য Order-এর `status = CANCELLED` করলেই production-ready হবে না।

Cancellation-এর একটি আলাদা record রাখা ভালো।

```python
class OrderCancellation(BaseModel):

    class Reason(models.TextChoices):
        CUSTOMER_REQUEST = "CUSTOMER_REQUEST", "Customer Request"
        PAYMENT_FAILED = "PAYMENT_FAILED", "Payment Failed"
        SELLER_REJECTED = "SELLER_REJECTED", "Seller Rejected"
        OUT_OF_STOCK = "OUT_OF_STOCK", "Out of Stock"
        ADMIN = "ADMIN", "Admin"

    order = models.ForeignKey(
        "orders.Order",
        on_delete=models.PROTECT,
        related_name="cancellations",
    )

    cancelled_by = models.ForeignKey(
        "accounts.User",
        on_delete=models.PROTECT,
        related_name="order_cancellations",
    )

    reason = models.CharField(
        max_length=30,
        choices=Reason.choices,
    )

    note = models.TextField(blank=True)

    cancelled_at = models.DateTimeField(
        auto_now_add=True
    )
```

এখন historical information থাকবে:

```text
Order #1001

Cancelled by: Customer
Reason: Customer Request
Date: ...
```

---

# 2. Cancellation Rule

সব order cancel করা যাবে না।

ধরো:

```text
PENDING       → CANCEL ✅
CONFIRMED     → CANCEL ✅
PROCESSING    → CANCEL maybe
SHIPPED       → CANCEL ❌
DELIVERED     → CANCEL ❌
```

তাই:

```python
CANCELLABLE_ORDER_STATES = {
    Order.Status.PENDING,
    Order.Status.CONFIRMED,
    Order.Status.PROCESSING,
}
```

তবে বাস্তবে business rule অনুযায়ী `PROCESSING` পর্যন্ত cancellation allowed কি না সেটা configurable করা যায়।

---

# 3. OrderCancellationService

এখন আসল service:

```python
class OrderCancellationService:

    @staticmethod
    @transaction.atomic
    def cancel(
        *,
        order_id,
        user,
        reason,
        note="",
    ):

        order = (
            Order.objects
            .select_for_update()
            .get(id=order_id)
        )

        if order.status not in CANCELLABLE_ORDER_STATES:
            raise ValueError(
                f"Order cannot be cancelled "
                f"from {order.status}"
            )

        # 1. Create cancellation record
        OrderCancellation.objects.create(
            order=order,
            cancelled_by=user,
            reason=reason,
            note=note,
        )

        # 2. Release inventory
        InventoryService.release_for_order(
            order=order,
            created_by=user,
        )

        # 3. Change order state
        OrderStateService.transition(
            order_id=order.id,
            new_status=Order.Status.CANCELLED,
        )

        # 4. Refund if already paid
        payment = getattr(
            order,
            "payment",
            None,
        )

        if payment and payment.status == Payment.Status.PAID:
            RefundService.create_refund(
                payment=payment,
                reason="ORDER_CANCELLED",
            )

        return order
```

এখানে একটা গুরুত্বপূর্ণ ব্যাপার:

**Cancellation ≠ Refund**

Cancellation হলো order lifecycle event।

Refund হলো টাকা ফেরত দেওয়ার financial event।

দুটো আলাদা রাখা উচিত।

---

# 4. Refund Model

এখন Refund।

```python
class Refund(BaseModel):

    class Status(models.TextChoices):
        PENDING = "PENDING", "Pending"
        PROCESSING = "PROCESSING", "Processing"
        COMPLETED = "COMPLETED", "Completed"
        FAILED = "FAILED", "Failed"

    payment = models.ForeignKey(
        "payments.Payment",
        on_delete=models.PROTECT,
        related_name="refunds",
    )

    order = models.ForeignKey(
        "orders.Order",
        on_delete=models.PROTECT,
        related_name="refunds",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    reason = models.CharField(
        max_length=100,
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.PENDING,
    )

    gateway_refund_id = models.CharField(
        max_length=255,
        unique=True,
        null=True,
        blank=True,
    )

    gateway_response = models.JSONField(
        null=True,
        blank=True,
    )

    processed_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

---

# 5. Refund State Machine

```text
PENDING
   │
   ▼
PROCESSING
   │
   ├──→ COMPLETED
   │
   └──→ FAILED
```

`COMPLETED` থেকে আবার:

```text
COMPLETED → PROCESSING
```

যাবে না।

---

# 6. RefundService

Refund request তৈরি:

```python
class RefundService:

    @staticmethod
    @transaction.atomic
    def create_refund(
        *,
        payment,
        amount=None,
        reason,
    ):

        payment = (
            Payment.objects
            .select_for_update()
            .get(id=payment.id)
        )

        if payment.status != Payment.Status.PAID:
            raise ValueError(
                "Only paid payment can be refunded."
            )

        refund_amount = (
            amount
            if amount is not None
            else payment.amount
        )

        already_refunded = (
            Refund.objects
            .filter(
                payment=payment,
                status=Refund.Status.COMPLETED,
            )
            .aggregate(
                total=Sum("amount")
            )["total"]
            or 0
        )

        if already_refunded + refund_amount > payment.amount:
            raise ValueError(
                "Refund amount exceeds paid amount."
            )

        refund = Refund.objects.create(
            payment=payment,
            order=payment.order,
            amount=refund_amount,
            reason=reason,
        )

        return refund
```

এটা শুধু refund **request** তৈরি করছে।

Gateway-তে টাকা ফেরত দেওয়ার call আলাদা।

---

# 7. External Gateway-এর সাথে Refund

খুব গুরুত্বপূর্ণ:

```text
Database transaction
        ❌
        │
Gateway API call
        ❌
```

Gateway API call-কে দীর্ঘ `transaction.atomic()`-এর মধ্যে রাখা উচিত না।

Flow:

```text
Create Refund(PENDING)
       │
       ▼
COMMIT
       │
       ▼
Call Payment Gateway
       │
       ├── Success
       │
       └── Failed
```

Success হলে:

```python
RefundService.handle_gateway_success(...)
```

---

# 8. Return System

Cancellation delivery-এর আগে।

Return সাধারণত delivery-এর পরে।

তাই Return-এর আলাদা model দরকার।

```python
class ReturnRequest(BaseModel):

    class Status(models.TextChoices):
        REQUESTED = "REQUESTED", "Requested"
        APPROVED = "APPROVED", "Approved"
        REJECTED = "REJECTED", "Rejected"
        RECEIVED = "RECEIVED", "Received"
        INSPECTED = "INSPECTED", "Inspected"
        COMPLETED = "COMPLETED", "Completed"
        CANCELLED = "CANCELLED", "Cancelled"

    order = models.ForeignKey(
        "orders.Order",
        on_delete=models.PROTECT,
        related_name="return_requests",
    )

    customer = models.ForeignKey(
        "accounts.User",
        on_delete=models.PROTECT,
        related_name="return_requests",
    )

    reason = models.CharField(
        max_length=255,
    )

    note = models.TextField(
        blank=True,
    )

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.REQUESTED,
    )
```

কিন্তু return কোন product-এর জন্য সেটা জানতে item-level model লাগবে।

---

# 9. ReturnItem

```python
class ReturnItem(BaseModel):

    return_request = models.ForeignKey(
        ReturnRequest,
        on_delete=models.CASCADE,
        related_name="items",
    )

    order_item = models.ForeignKey(
        "orders.OrderItem",
        on_delete=models.PROTECT,
        related_name="return_items",
    )

    quantity = models.PositiveIntegerField()

    reason = models.CharField(
        max_length=255,
        blank=True,
    )
```

এখন:

```text
Order #1001

iPhone → qty 2
Mouse   → qty 1
Keyboard → qty 1
```

Customer শুধু:

```text
iPhone → qty 1
```

return করতে পারবে।

---

# 10. Return State Machine

```text
REQUESTED
    │
    ├──→ APPROVED
    │       │
    │       ▼
    │    RECEIVED
    │       │
    │       ▼
    │    INSPECTED
    │       │
    │       ▼
    │    COMPLETED
    │
    └──→ REJECTED
```

---

# 11. Return ≠ Refund

এটা খুব ভালোভাবে বুঝতে হবে।

```text
Return
   =
Product ফেরত আসছে
```

আর:

```text
Refund
   =
Customer-এর টাকা ফেরত যাচ্ছে
```

তাই:

```text
Return completed
       │
       ├── Restore inventory
       │
       └── Create refund
```

Business policy অনুযায়ী refund আগে/পরে হতে পারে।

---

# 12. Exchange

Exchange হলো:

```text
Customer returns old item
          +
Customer gets replacement item
```

এটার জন্য Return-এর ওপর আলাদা Exchange record রাখতে পারি।

```python
class ExchangeRequest(BaseModel):

    class Status(models.TextChoices):
        REQUESTED = "REQUESTED", "Requested"
        APPROVED = "APPROVED", "Approved"
        PROCESSING = "PROCESSING", "Processing"
        SHIPPED = "SHIPPED", "Shipped"
        COMPLETED = "COMPLETED", "Completed"
        REJECTED = "REJECTED", "Rejected"

    return_request = models.OneToOneField(
        ReturnRequest,
        on_delete=models.PROTECT,
        related_name="exchange",
    )

    original_variant = models.ForeignKey(
        "products.ProductVariant",
        on_delete=models.PROTECT,
        related_name="exchange_originals",
    )

    replacement_variant = models.ForeignKey(
        "products.ProductVariant",
        on_delete=models.PROTECT,
        related_name="exchange_replacements",
    )

    quantity = models.PositiveIntegerField()

    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.REQUESTED,
    )
```

Exchange-এর সময় replacement inventory reserve করতে হবে।

অর্থাৎ:

```text
Exchange
   │
   ├── Old item → Return
   │
   └── New item → Inventory Reserve
```

---

# 13. Payment Reconciliation

এখন আসল advanced layer।

ধরো আমাদের database বলছে:

```text
Payment #1001
status = PAID
amount = 5000
gateway_transaction_id = TX123
```

কিন্তু gateway-এর dashboard/API বলছে:

```text
TX123
status = REFUNDED
amount = 5000
```

Database outdated।

অথবা:

```text
Our DB → PENDING
Gateway → PAID
```

এটা reconciliation-এর সমস্যা।

---

# 14. Reconciliation Model

একটা audit model রাখা যায়:

```python
class PaymentReconciliation(BaseModel):

    payment = models.ForeignKey(
        Payment,
        on_delete=models.PROTECT,
        related_name="reconciliations",
    )

    database_status = models.CharField(
        max_length=20,
    )

    gateway_status = models.CharField(
        max_length=50,
    )

    gateway_transaction_id = models.CharField(
        max_length=255,
        blank=True,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_matched = models.BooleanField(
        default=False,
    )

    discrepancy = models.TextField(
        blank=True,
    )

    checked_at = models.DateTimeField(
        auto_now_add=True,
    )
```

---

# 15. Reconciliation Flow

Celery দিয়ে periodic job চালানো যায়:

```text
Every 10 minutes / 1 hour
           │
           ▼
Find suspicious payments
           │
           ▼
Query Gateway
           │
           ▼
Compare
    ┌──────┴──────┐
    ▼             ▼
 MATCH       MISMATCH
    │             │
    ▼             ▼
is_matched     Create
=True          discrepancy
```

উদাহরণ:

```text
Database:
PAID

Gateway:
PAID

Amount:
5000 == 5000

Result:
MATCHED
```

অন্যদিকে:

```text
Database:
PENDING

Gateway:
PAID

Result:
MISMATCH
```

তারপর manual বা automated recovery policy অনুযায়ী PaymentService event process করবে।

---

# 16. পুরো Production Lifecycle

এখন আমাদের architecture দাঁড়াচ্ছে:

```text
                    CHECKOUT
                       │
                       ▼
                    PENDING
                       │
              Payment Success
                       │
                       ▼
                   CONFIRMED
                       │
                       ▼
                  PROCESSING
                       │
                       ▼
                    SHIPPED
                       │
                       ▼
                   DELIVERED
                       │
                       ▼
                Return Request
                       │
              ┌────────┴────────┐
              ▼                 ▼
           Refund            Exchange
              │                 │
              ▼                 ▼
          REFUNDED         Replacement
```

Cancellation path:

```text
PENDING / CONFIRMED / eligible PROCESSING
                │
                ▼
            CANCELLED
                │
                ▼
          Refund if PAID
```

---

# 17. Service Layer এখন এমন হবে

```text
services/
│
├── checkout_service.py
│
├── order_service.py
│
├── order_state_service.py
│
├── order_cancellation_service.py
│
├── inventory_service.py
│
├── payment_service.py
│
├── payment_state_service.py
│
├── refund_service.py
│
├── return_service.py
│
├── exchange_service.py
│
├── coupon_service.py
│
├── commission_service.py
│
└── reconciliation_service.py
```

এটা যথেষ্ট পরিষ্কার separation।

---

# 18. সবচেয়ে গুরুত্বপূর্ণ Transaction Rules

এই layer-এ এগুলো মনে রাখতে হবে:

### Cancellation

```text
Lock Order
   ↓
Validate state
   ↓
Create Cancellation
   ↓
Release exact inventory allocation
   ↓
Cancel Order
   ↓
If paid → create Refund
```

### Refund

```text
Lock Payment
   ↓
Validate PAID
   ↓
Check refundable amount
   ↓
Create Refund
   ↓
Gateway API
   ↓
Webhook/response
   ↓
Refund COMPLETED
```

### Return

```text
Lock OrderItem
   ↓
Validate DELIVERED
   ↓
Validate return window
   ↓
Create ReturnRequest
   ↓
Approve
   ↓
Receive
   ↓
Inspect
   ↓
Restore inventory
   ↓
Refund / Exchange
```

### Exchange

```text
Return approved
      ↓
Reserve replacement inventory
      ↓
Receive old product
      ↓
Inspect
      ↓
Ship replacement
      ↓
Exchange COMPLETED
```

---

## একটি খুব গুরুত্বপূর্ণ production rule

**Refund, Return এবং Exchange-এর জন্য কখনো সরাসরি Order status পরিবর্তন করে business logic শেষ করা যাবে না।**

যেমন:

```python
order.status = "REFUNDED"
```

এটা করা যাবে না।

কারণ Refund হলে আরও অনেক operation থাকতে পারে:

```text
Refund
 ├── Payment
 ├── Gateway
 ├── Refund amount
 ├── Refund transaction
 ├── Inventory
 ├── Seller commission reversal
 └── Accounting
```

তাই এগুলো **নিজস্ব domain object + service + state machine** হিসেবে থাকবে।

এখন এই architecture-এর পরবর্তী সবচেয়ে গুরুত্বপূর্ণ অংশ হবে **`OrderCancellationService + RefundService`-এর complete production implementation**, যেখানে partial cancellation, partial refund, seller commission reversal, exact inventory release এবং gateway webhook idempotency একসাথে handle করা হবে।


