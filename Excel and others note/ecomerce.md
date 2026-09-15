অবশ্যই। তুমি যেহেতু **Django ORM practice** করবে, আমি এমন একটা **production-style Multi-Vendor E-commerce model architecture** দিচ্ছি যেখানে তোমার শেখা প্রায় সব advanced ORM concept practice করা যাবে।

এখানে আমরা **Amazon/Daraz-type marketplace** ধরে নিচ্ছি:

```text
Platform
│
├── Users
│
├── Vendors
│   ├── Store
│   ├── Products
│   ├── Inventory
│   └── Orders
│
├── Customers
│   ├── Addresses
│   ├── Cart
│   ├── Orders
│   ├── Payments
│   └── Reviews
│
└── Platform
    ├── Categories
    ├── Coupons
    ├── Commission
    ├── Payouts
    └── Audit Logs
```

# 🏗️ Complete Multi-Vendor E-commerce Models

> Practice-এর জন্য সব model একসাথে দিলাম। Production project-এ এগুলো আলাদা app-এ ভাগ করবে।

```python
# models.py

from decimal import Decimal

from django.conf import settings
from django.contrib.postgres.constraints import ExclusionConstraint
from django.contrib.postgres.fields import ArrayField
from django.contrib.postgres.fields.ranges import RangeOperators
from django.db import models
from django.db.models import Q


# =========================================================
# 1. BASE MODEL
# =========================================================

class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True


# =========================================================
# 2. VENDOR
# =========================================================

class Vendor(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("approved", "Approved"),
        ("suspended", "Suspended"),
        ("rejected", "Rejected"),
    ]

    owner = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="vendor_profile",
    )

    business_name = models.CharField(max_length=150)
    business_email = models.EmailField()
    phone = models.CharField(max_length=30)

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    commission_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        default=10,
    )

    is_active = models.BooleanField(default=True)

    class Meta:
        indexes = [
            models.Index(fields=["status"]),
            models.Index(fields=["is_active"]),
        ]

    def __str__(self):
        return self.business_name


# =========================================================
# 3. VENDOR MEMBERSHIP
# =========================================================

class VendorMembership(BaseModel):

    ROLE_CHOICES = [
        ("owner", "Owner"),
        ("manager", "Manager"),
        ("staff", "Staff"),
        ("accountant", "Accountant"),
    ]

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.CASCADE,
        related_name="memberships",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="vendor_memberships",
    )

    role = models.CharField(
        max_length=30,
        choices=ROLE_CHOICES,
    )

    is_active = models.BooleanField(default=True)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["vendor", "user"],
                name="unique_vendor_member",
            )
        ]


# =========================================================
# 4. STORE
# =========================================================

class Store(BaseModel):

    vendor = models.OneToOneField(
        Vendor,
        on_delete=models.PROTECT,
        related_name="store",
    )

    name = models.CharField(max_length=150)
    slug = models.SlugField(unique=True)

    description = models.TextField(blank=True)

    logo = models.ImageField(
        upload_to="stores/logos/",
        blank=True,
        null=True,
    )

    banner = models.ImageField(
        upload_to="stores/banners/",
        blank=True,
        null=True,
    )

    address = models.TextField()
    city = models.CharField(max_length=100)
    country = models.CharField(max_length=100)

    is_active = models.BooleanField(default=True)

    class Meta:
        indexes = [
            models.Index(fields=["city"]),
            models.Index(fields=["is_active"]),
        ]


# =========================================================
# 5. CATEGORY
# =========================================================

class Category(BaseModel):

    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)

    parent = models.ForeignKey(
        "self",
        on_delete=models.PROTECT,
        null=True,
        blank=True,
        related_name="children",
    )

    description = models.TextField(blank=True)

    is_active = models.BooleanField(default=True)

    class Meta:
        verbose_name_plural = "Categories"
        indexes = [
            models.Index(fields=["parent"]),
            models.Index(fields=["is_active"]),
        ]

    def __str__(self):
        return self.name


# =========================================================
# 6. BRAND
# =========================================================

class Brand(BaseModel):

    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)

    description = models.TextField(blank=True)

    is_active = models.BooleanField(default=True)

    def __str__(self):
        return self.name


# =========================================================
# 7. PRODUCT
# =========================================================

class Product(BaseModel):

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("active", "Active"),
        ("inactive", "Inactive"),
        ("blocked", "Blocked"),
    ]

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="products",
    )

    category = models.ForeignKey(
        Category,
        on_delete=models.PROTECT,
        related_name="products",
    )

    brand = models.ForeignKey(
        Brand,
        on_delete=models.PROTECT,
        related_name="products",
        null=True,
        blank=True,
    )

    name = models.CharField(max_length=200)
    slug = models.SlugField()

    sku = models.CharField(
        max_length=100,
        unique=True,
    )

    description = models.TextField()

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    discount_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="draft",
    )

    tags = ArrayField(
        models.CharField(max_length=50),
        default=list,
        blank=True,
    )

    attributes = models.JSONField(
        default=dict,
        blank=True,
    )

    is_active = models.BooleanField(default=True)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["vendor", "slug"],
                name="unique_product_slug_per_vendor",
            ),
            models.CheckConstraint(
                condition=Q(price__gte=0),
                name="product_price_non_negative",
            ),
        ]

        indexes = [
            models.Index(
                fields=["vendor", "status"]
            ),
            models.Index(
                fields=["category", "status"]
            ),
            models.Index(
                fields=["price"]
            ),
        ]

    def __str__(self):
        return self.name


# =========================================================
# 8. PRODUCT IMAGE
# =========================================================

class ProductImage(BaseModel):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="products/",
    )

    alt_text = models.CharField(
        max_length=200,
        blank=True,
    )

    is_primary = models.BooleanField(
        default=False
    )

    sort_order = models.PositiveIntegerField(
        default=0
    )

    class Meta:
        ordering = ["sort_order", "id"]


# =========================================================
# 9. PRODUCT VARIANT
# =========================================================

class ProductVariant(BaseModel):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="variants",
    )

    name = models.CharField(
        max_length=100
    )

    sku = models.CharField(
        max_length=100,
        unique=True,
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True,
    )

    attributes = models.JSONField(
        default=dict,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["product", "is_active"]
            )
        ]


# =========================================================
# 10. INVENTORY
# =========================================================

class Inventory(BaseModel):

    product = models.OneToOneField(
        Product,
        on_delete=models.PROTECT,
        related_name="inventory",
    )

    quantity = models.PositiveIntegerField(
        default=0
    )

    reserved_quantity = models.PositiveIntegerField(
        default=0
    )

    low_stock_threshold = models.PositiveIntegerField(
        default=5
    )

    version = models.PositiveIntegerField(
        default=1
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=Q(quantity__gte=0),
                name="inventory_quantity_non_negative",
            ),
            models.CheckConstraint(
                condition=Q(reserved_quantity__gte=0),
                name="reserved_quantity_non_negative",
            ),
        ]


# =========================================================
# 11. CUSTOMER ADDRESS
# =========================================================

class Address(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="addresses",
    )

    full_name = models.CharField(
        max_length=150
    )

    phone = models.CharField(
        max_length=30
    )

    address_line = models.TextField()

    city = models.CharField(
        max_length=100
    )

    postal_code = models.CharField(
        max_length=20
    )

    country = models.CharField(
        max_length=100
    )

    is_default = models.BooleanField(
        default=False
    )


# =========================================================
# 12. CART
# =========================================================

class Cart(BaseModel):

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="cart",
    )

    is_active = models.BooleanField(
        default=True
    )


# =========================================================
# 13. CART ITEM
# =========================================================

class CartItem(BaseModel):

    cart = models.ForeignKey(
        Cart,
        on_delete=models.CASCADE,
        related_name="items",
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT,
        related_name="cart_items",
    )

    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.PROTECT,
        null=True,
        blank=True,
        related_name="cart_items",
    )

    quantity = models.PositiveIntegerField()

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "cart",
                    "product",
                    "variant",
                ],
                name="unique_cart_product_variant",
            ),
        ]


# =========================================================
# 14. ORDER
# =========================================================

class Order(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("confirmed", "Confirmed"),
        ("processing", "Processing"),
        ("shipped", "Shipped"),
        ("delivered", "Delivered"),
        ("cancelled", "Cancelled"),
        ("refunded", "Refunded"),
    ]

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="orders",
    )

    order_number = models.CharField(
        max_length=50,
        unique=True,
    )

    shipping_address = models.ForeignKey(
        Address,
        on_delete=models.PROTECT,
        related_name="orders",
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="pending",
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    shipping_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["user", "-created_at"]
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]


# =========================================================
# 15. ORDER ITEM
# =========================================================

class OrderItem(BaseModel):

    order = models.ForeignKey(
        Order,
        on_delete=models.PROTECT,
        related_name="items",
    )

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="order_items",
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT,
        related_name="order_items",
    )

    variant = models.ForeignKey(
        ProductVariant,
        on_delete=models.PROTECT,
        null=True,
        blank=True,
        related_name="order_items",
    )

    product_name = models.CharField(
        max_length=200
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    quantity = models.PositiveIntegerField()

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["vendor", "-created_at"]
            ),
            models.Index(
                fields=["product", "-created_at"]
            ),
        ]


# =========================================================
# 16. PAYMENT
# =========================================================

class Payment(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
    ]

    METHOD_CHOICES = [
        ("cod", "Cash on Delivery"),
        ("card", "Card"),
        ("mobile_banking", "Mobile Banking"),
        ("bank", "Bank"),
    ]

    order = models.OneToOneField(
        Order,
        on_delete=models.PROTECT,
        related_name="payment",
    )

    transaction_id = models.CharField(
        max_length=150,
        unique=True,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    method = models.CharField(
        max_length=30,
        choices=METHOD_CHOICES,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )


# =========================================================
# 17. COMMISSION
# =========================================================

class Commission(BaseModel):

    order_item = models.OneToOneField(
        OrderItem,
        on_delete=models.PROTECT,
        related_name="commission",
    )

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="commissions",
    )

    gross_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    commission_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2,
    )

    platform_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    vendor_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )


# =========================================================
# 18. VENDOR PAYOUT
# =========================================================

class VendorPayout(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("processing", "Processing"),
        ("paid", "Paid"),
        ("failed", "Failed"),
    ]

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="payouts",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    reference = models.CharField(
        max_length=150,
        unique=True,
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True,
    )


# =========================================================
# 19. REVIEW
# =========================================================

class Review(BaseModel):

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    order_item = models.ForeignKey(
        OrderItem,
        on_delete=models.PROTECT,
        related_name="review",
    )

    rating = models.PositiveSmallIntegerField()

    comment = models.TextField(
        blank=True
    )

    is_verified_purchase = models.BooleanField(
        default=False
    )

    is_published = models.BooleanField(
        default=True
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "user",
                    "order_item",
                ],
                name="one_review_per_order_item",
            ),
            models.CheckConstraint(
                condition=Q(rating__gte=1)
                & Q(rating__lte=5),
                name="rating_between_1_and_5",
            ),
        ]

        indexes = [
            models.Index(
                fields=["product", "-created_at"]
            ),
            models.Index(
                fields=["rating"]
            ),
        ]


# =========================================================
# 20. COUPON
# =========================================================

class Coupon(BaseModel):

    DISCOUNT_TYPE_CHOICES = [
        ("percentage", "Percentage"),
        ("fixed", "Fixed"),
    ]

    code = models.CharField(
        max_length=50,
        unique=True,
    )

    discount_type = models.CharField(
        max_length=20,
        choices=DISCOUNT_TYPE_CHOICES,
    )

    discount_value = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    minimum_order_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    maximum_discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        null=True,
        blank=True,
    )

    usage_limit = models.PositiveIntegerField(
        null=True,
        blank=True,
    )

    used_count = models.PositiveIntegerField(
        default=0
    )

    valid_from = models.DateTimeField()

    valid_until = models.DateTimeField()

    is_active = models.BooleanField(
        default=True
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["code"]
            ),
            models.Index(
                fields=["valid_from", "valid_until"]
            ),
        ]


# =========================================================
# 21. COUPON USAGE
# =========================================================

class CouponUsage(BaseModel):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT,
        related_name="usages",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="coupon_usages",
    )

    order = models.ForeignKey(
        Order,
        on_delete=models.PROTECT,
        related_name="coupon_usages",
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["coupon", "user", "order"],
                name="unique_coupon_usage",
            )
        ]


# =========================================================
# 22. WISHLIST
# =========================================================

class Wishlist(BaseModel):

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="wishlist",
    )


# =========================================================
# 23. WISHLIST ITEM
# =========================================================

class WishlistItem(BaseModel):

    wishlist = models.ForeignKey(
        Wishlist,
        on_delete=models.CASCADE,
        related_name="items",
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        related_name="wishlist_items",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["wishlist", "product"],
                name="unique_wishlist_product",
            )
        ]


# =========================================================
# 24. STOCK MOVEMENT
# =========================================================

class StockMovement(BaseModel):

    MOVEMENT_TYPES = [
        ("purchase", "Purchase"),
        ("sale", "Sale"),
        ("return", "Return"),
        ("adjustment", "Adjustment"),
        ("damage", "Damage"),
    ]

    inventory = models.ForeignKey(
        Inventory,
        on_delete=models.PROTECT,
        related_name="movements",
    )

    movement_type = models.CharField(
        max_length=30,
        choices=MOVEMENT_TYPES,
    )

    quantity = models.IntegerField()

    reference = models.CharField(
        max_length=150,
        blank=True,
    )

    note = models.TextField(
        blank=True
    )


# =========================================================
# 25. RETURN
# =========================================================

class ReturnRequest(BaseModel):

    STATUS_CHOICES = [
        ("requested", "Requested"),
        ("approved", "Approved"),
        ("rejected", "Rejected"),
        ("received", "Received"),
        ("refunded", "Refunded"),
    ]

    order_item = models.ForeignKey(
        OrderItem,
        on_delete=models.PROTECT,
        related_name="returns",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="return_requests",
    )

    quantity = models.PositiveIntegerField()

    reason = models.TextField()

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="requested",
    )


# =========================================================
# 26. NOTIFICATION
# =========================================================

class Notification(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="notifications",
    )

    title = models.CharField(
        max_length=200
    )

    message = models.TextField()

    is_read = models.BooleanField(
        default=False
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["user", "is_read", "-created_at"]
            )
        ]


# =========================================================
# 27. IDEMPOTENCY RECORD
# =========================================================

class IdempotencyRecord(BaseModel):

    STATUS_CHOICES = [
        ("processing", "Processing"),
        ("completed", "Completed"),
        ("failed", "Failed"),
    ]

    key = models.CharField(
        max_length=150,
        unique=True,
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="idempotency_records",
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
    )

    response_data = models.JSONField(
        null=True,
        blank=True,
    )


# =========================================================
# 28. AUDIT LOG
# =========================================================

class AuditLog(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="audit_logs",
    )

    action = models.CharField(
        max_length=100
    )

    model_name = models.CharField(
        max_length=100
    )

    object_id = models.CharField(
        max_length=100
    )

    old_data = models.JSONField(
        null=True,
        blank=True,
    )

    new_data = models.JSONField(
        null=True,
        blank=True,
    )

    ip_address = models.GenericIPAddressField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["model_name", "object_id"]
            ),
            models.Index(
                fields=["user", "-created_at"]
            ),
        ]
```

# 🔗 পুরো Relationship

এটা মুখস্থ করার দরকার নেই—diagram দেখে বুঝবে।

```text
                         User
                          │
            ┌─────────────┼─────────────┐
            ↓             ↓             ↓
         Vendor        Customer       Admin
            │
      ┌─────┴──────┐
      ↓            ↓
    Store      Membership
      │
      │
   Products
      │
 ┌────┼──────────────┐
 ↓    ↓              ↓
Category Brand     Variant
 │
 ↓
Product
 │
 ├── Images
 ├── Inventory
 │      │
 │      └── StockMovement
 │
 └── Reviews
```

Customer side:

```text
User
 │
 ├── Address
 ├── Cart
 │    └── CartItem
 │
 ├── Wishlist
 │    └── WishlistItem
 │
 ├── Order
 │    └── OrderItem
 │          │
 │          ├── Vendor
 │          ├── Product
 │          ├── Commission
 │          └── Return
 │
 ├── Payment
 ├── Reviews
 ├── CouponUsage
 └── Notifications
```

Vendor financial flow:

```text
Order
  ↓
OrderItem
  ↓
Commission
  ↓
Vendor Amount
  ↓
VendorPayout
```

---

# 🔥 এখন তোমার আসল ORM Practice শুরু

এই project-এ শুধু model বানালে হবে না। প্রতিটি model নিয়ে query practice করবে।

## Level 1 — Basic

```text
1. সব active products
2. সব vendors
3. একটি vendor-এর products
4. একটি category-এর products
5. price > 1000 products
6. price range
7. latest products
8. top-rated products
9. inactive products
10. product count
```

## Level 2 — Relationships

```text
11. Vendor → Products
12. Vendor → Orders
13. Product → Reviews
14. Product → Images
15. Product → Inventory
16. User → Orders
17. Order → Items
18. OrderItem → Vendor
19. Category → Products
20. Parent Category → Children
```

## Level 3 — Optimization

Practice করবে:

```python
select_related()
prefetch_related()
Prefetch()
```

যেমন:

```python
Product.objects.select_related(
    "vendor",
    "category",
    "brand",
).prefetch_related(
    "images",
    "reviews",
)
```

---

# Level 4 — Aggregation

Vendor dashboard:

```text
Total Products
Total Orders
Total Sales
Total Commission
Total Payout
Average Product Rating
```

Practice:

```python
Count()
Sum()
Avg()
Min()
Max()
```

---

# Level 5 — Advanced ORM

এখানে তোমার আগের শেখা concepts সব ব্যবহার করবে:

```text
Q()
F()
Case()
When()
ExpressionWrapper()
Subquery()
OuterRef()
Exists()
Window()
```

উদাহরণ:

```text
প্রতিটি vendor-এর:

total_products
total_orders
total_sales
average_order_value
total_commission
```

এক QuerySet-এ করার চেষ্টা করবে।

---

# 🔥 Level 6 — Inventory Concurrency

এটা অবশ্যই করবে।

ধরো:

```text
Product stock = 10
```

একসাথে:

```text
User A → 7 কিনতে চায়
User B → 5 কিনতে চায়
```

Expected:

```text
A → Success
B → Failed
```

এখানে practice করবে:

```python
transaction.atomic()

select_for_update()

F()
```

---

# 🔥 Level 7 — Multi-Vendor Isolation

এটা তোমার project-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

Vendor A যেন Vendor B-এর:

```text
Product
Order
Inventory
Commission
Payout
```

কোনোটাই দেখতে/modify করতে না পারে।

Example:

```python
Product.objects.filter(
    vendor=request.user.vendor_profile
)
```

Orders:

```python
OrderItem.objects.filter(
    vendor=request.user.vendor_profile
)
```

---

# 🔥 Level 8 — Analytics

শেষে dashboard বানাবে:

```text
Vendor Dashboard

Products       150
Orders         840
Revenue        ৳850,000
Commission     ৳85,000
Payout         ৳765,000
```

Admin dashboard:

```text
Total Vendors
Total Customers
Total Products
Total Orders
Gross Revenue
Platform Revenue
Vendor Revenue
Top Products
Top Vendors
Monthly Sales
```

এখানে তোমার:

```text
Aggregation
Annotation
Subquery
Exists
Window Functions
```

সব কাজে লাগবে।

---

## 🧠 Project-এর App Structure

সব model এক `models.py`-তে না রেখে:

```text
ecommerce/
│
├── accounts/
│
├── vendors/
│
├── catalog/
│
├── inventory/
│
├── cart/
│
├── orders/
│
├── payments/
│
├── promotions/
│
├── reviews/
│
├── payouts/
│
├── notifications/
│
└── audit/
```

এটাই practice-এর জন্য অনেক বেশি professional structure।

### তোমার Practice Roadmap

```text
Phase 1  → Models
Phase 2  → Migrations
Phase 3  → Basic ORM Queries
Phase 4  → Relationships
Phase 5  → Query Optimization
Phase 6  → Aggregation
Phase 7  → Advanced ORM
Phase 8  → Inventory
Phase 9  → Transactions
Phase 10 → Concurrency
Phase 11 → Vendor Isolation
Phase 12 → Analytics
Phase 13 → DRF API
Phase 14 → Testing
Phase 15 → PostgreSQL Optimization
```

**আমার recommendation:** এখনই DRF API শুরু কোরো না। আগে এই models দিয়ে **শুধু Django shell-এ 100+ ORM query practice** করো। এতে তোমার ORM knowledge সত্যিকারের strong হবে।