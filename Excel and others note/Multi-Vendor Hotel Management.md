অবশ্যই। এবার **Multi-Vendor Hotel Management System**-কে আমরা e-commerce marketplace-এর মতো **complete production-style model architecture** হিসেবে ধরব।

এটা হবে অনেকটা:

**Booking.com / Agoda-style marketplace + Hotel Management**

```text
Platform
│
├── Users
│
├── Vendors
│   ├── Hotel
│   ├── Hotel Staff
│   ├── Rooms
│   ├── Services
│   ├── Inventory
│   └── Bookings
│
├── Customers
│   ├── Addresses
│   ├── Bookings
│   ├── Payments
│   ├── Reviews
│   └── Wishlist
│
└── Platform
    ├── Commission
    ├── Payout
    ├── Coupon
    ├── Audit Log
    └── Notifications
```

নিচের models-গুলো তোমার **Django ORM practice-এর জন্য complete set** হিসেবে ব্যবহার করতে পারো।

---

# 1. Base Model

```python
from django.db import models


class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

---

# 2. Vendor

একজন vendor এক বা একাধিক hotel পরিচালনা করতে পারবে।

```python
from django.conf import settings


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

    email = models.EmailField()

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
```

Relationship:

```text
User
 ↓
Vendor
 ↓
Hotels
```

---

# 3. Vendor Membership / Staff

একজন vendor-এর একাধিক staff থাকতে পারে।

```python
class VendorMembership(BaseModel):

    ROLE_CHOICES = [
        ("owner", "Owner"),
        ("manager", "Manager"),
        ("receptionist", "Receptionist"),
        ("accountant", "Accountant"),
        ("staff", "Staff"),
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
                name="unique_vendor_user",
            )
        ]
```

---

# 4. Hotel

```python
class Hotel(BaseModel):

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("pending", "Pending Approval"),
        ("approved", "Approved"),
        ("suspended", "Suspended"),
        ("inactive", "Inactive"),
    ]

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="hotels",
    )

    name = models.CharField(max_length=200)

    slug = models.SlugField()

    description = models.TextField()

    email = models.EmailField()

    phone = models.CharField(max_length=30)

    address = models.TextField()

    city = models.CharField(max_length=100)

    country = models.CharField(max_length=100)

    latitude = models.DecimalField(
        max_digits=9,
        decimal_places=6,
        null=True,
        blank=True,
    )

    longitude = models.DecimalField(
        max_digits=9,
        decimal_places=6,
        null=True,
        blank=True,
    )

    star_rating = models.PositiveSmallIntegerField(
        default=0
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="draft",
    )

    is_active = models.BooleanField(default=True)

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["vendor", "slug"],
                name="unique_hotel_slug_per_vendor",
            ),
            models.CheckConstraint(
                condition=(
                    models.Q(star_rating__gte=0)
                    & models.Q(star_rating__lte=5)
                ),
                name="hotel_star_rating_0_5",
            ),
        ]

        indexes = [
            models.Index(fields=["vendor", "status"]),
            models.Index(fields=["city", "status"]),
            models.Index(fields=["star_rating"]),
        ]

    def __str__(self):
        return self.name
```

---

# 5. Hotel Image

```python
class HotelImage(BaseModel):

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="hotels/"
    )

    caption = models.CharField(
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
```

---

# 6. Hotel Amenity

যেমন:

```text
WiFi
Swimming Pool
Parking
Gym
Restaurant
```

```python
class Amenity(BaseModel):

    name = models.CharField(
        max_length=100,
        unique=True,
    )

    icon = models.CharField(
        max_length=100,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True
    )

    def __str__(self):
        return self.name
```

Hotel-এর সাথে M2M:

```python
class HotelAmenity(BaseModel):

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.CASCADE,
        related_name="hotel_amenities",
    )

    amenity = models.ForeignKey(
        Amenity,
        on_delete=models.PROTECT,
        related_name="hotel_amenities",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["hotel", "amenity"],
                name="unique_hotel_amenity",
            )
        ]
```

---

# 7. Room Type

```text
Single
Double
Deluxe
Suite
Family
```

```python
class RoomType(BaseModel):

    name = models.CharField(
        max_length=100
    )

    description = models.TextField(
        blank=True
    )

    max_guests = models.PositiveIntegerField()

    is_active = models.BooleanField(
        default=True
    )

    def __str__(self):
        return self.name
```

---

# 8. Room

```python
class Room(BaseModel):

    STATUS_CHOICES = [
        ("available", "Available"),
        ("maintenance", "Maintenance"),
        ("inactive", "Inactive"),
    ]

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.PROTECT,
        related_name="rooms",
    )

    room_type = models.ForeignKey(
        RoomType,
        on_delete=models.PROTECT,
        related_name="rooms",
    )

    room_number = models.CharField(
        max_length=30
    )

    floor = models.PositiveIntegerField(
        null=True,
        blank=True,
    )

    price_per_night = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    capacity = models.PositiveIntegerField()

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="available",
    )

    is_active = models.BooleanField(
        default=True
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["hotel", "room_number"],
                name="unique_room_number_per_hotel",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    price_per_night__gte=0
                ),
                name="room_price_non_negative",
            ),
        ]

        indexes = [
            models.Index(
                fields=["hotel", "status"]
            ),
            models.Index(
                fields=["room_type", "price_per_night"]
            ),
        ]

    def __str__(self):
        return f"{self.hotel.name} - {self.room_number}"
```

---

# 9. Room Image

```python
class RoomImage(BaseModel):

    room = models.ForeignKey(
        Room,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="rooms/"
    )

    caption = models.CharField(
        max_length=200,
        blank=True,
    )

    is_primary = models.BooleanField(
        default=False
    )

    sort_order = models.PositiveIntegerField(
        default=0
    )
```

---

# 10. Room Amenity

```python
class RoomAmenity(BaseModel):

    room = models.ForeignKey(
        Room,
        on_delete=models.CASCADE,
        related_name="room_amenities",
    )

    amenity = models.ForeignKey(
        Amenity,
        on_delete=models.PROTECT,
        related_name="room_amenities",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["room", "amenity"],
                name="unique_room_amenity",
            )
        ]
```

---

# 11. Room Inventory

```python
class RoomInventory(BaseModel):

    room = models.OneToOneField(
        Room,
        on_delete=models.PROTECT,
        related_name="inventory",
    )

    available_units = models.PositiveIntegerField(
        default=1
    )

    reserved_units = models.PositiveIntegerField(
        default=0
    )

    version = models.PositiveIntegerField(
        default=1
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=models.Q(
                    available_units__gte=0
                ),
                name="available_units_non_negative",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    reserved_units__gte=0
                ),
                name="reserved_units_non_negative",
            ),
        ]
```

এখানে practice করবে:

```python
select_for_update()
F()
atomic()
```

---

# 12. Hotel Service

```text
Breakfast
Airport Pickup
Laundry
Spa
Extra Bed
Room Service
```

```python
class Service(BaseModel):

    vendor = models.ForeignKey(
        Vendor,
        on_delete=models.PROTECT,
        related_name="services",
    )

    name = models.CharField(
        max_length=150
    )

    description = models.TextField(
        blank=True
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["vendor", "is_active"]
            )
        ]
```

---

# 13. Customer Address

```python
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

    country = models.CharField(
        max_length=100
    )

    postal_code = models.CharField(
        max_length=20,
        blank=True,
    )

    is_default = models.BooleanField(
        default=False
    )
```

---

# 14. Guest / Customer Profile

User model-এর সাথে hotel-specific information রাখতে:

```python
class CustomerProfile(BaseModel):

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="customer_profile",
    )

    date_of_birth = models.DateField(
        null=True,
        blank=True,
    )

    nationality = models.CharField(
        max_length=100,
        blank=True,
    )

    passport_number = models.CharField(
        max_length=100,
        blank=True,
    )

    emergency_contact = models.CharField(
        max_length=30,
        blank=True,
    )
```

> Production-এ sensitive identity data রাখলে encryption/access-control carefully design করবে।

---

# 15. Booking

এটাই core model।

```python
class Booking(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("confirmed", "Confirmed"),
        ("checked_in", "Checked In"),
        ("checked_out", "Checked Out"),
        ("cancelled", "Cancelled"),
        ("no_show", "No Show"),
        ("refunded", "Refunded"),
    ]

    customer = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="bookings",
    )

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.PROTECT,
        related_name="bookings",
    )

    room = models.ForeignKey(
        Room,
        on_delete=models.PROTECT,
        related_name="bookings",
    )

    booking_number = models.CharField(
        max_length=50,
        unique=True,
    )

    check_in = models.DateField()

    check_out = models.DateField()

    guests = models.PositiveIntegerField()

    nights = models.PositiveIntegerField()

    room_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    service_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="pending",
    )

    special_request = models.TextField(
        blank=True
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["hotel", "-created_at"]
            ),
            models.Index(
                fields=["room", "check_in", "check_out"]
            ),
            models.Index(
                fields=["customer", "-created_at"]
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]

        constraints = [
            models.CheckConstraint(
                condition=models.Q(
                    check_out__gt=models.F("check_in")
                ),
                name="booking_checkout_after_checkin",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    total_amount__gte=0
                ),
                name="booking_total_non_negative",
            ),
        ]
```

---

# 16. Booking Service

Booking-এর সাথে services:

```python
class BookingService(BaseModel):

    booking = models.ForeignKey(
        Booking,
        on_delete=models.CASCADE,
        related_name="booking_services",
    )

    service = models.ForeignKey(
        Service,
        on_delete=models.PROTECT,
        related_name="booking_services",
    )

    quantity = models.PositiveIntegerField(
        default=1
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["booking", "service"],
                name="unique_booking_service",
            )
        ]
```

---

# 17. Payment

```python
class Payment(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
        ("partially_refunded", "Partially Refunded"),
    ]

    METHOD_CHOICES = [
        ("cash", "Cash"),
        ("card", "Card"),
        ("mobile_banking", "Mobile Banking"),
        ("bank", "Bank"),
    ]

    booking = models.ForeignKey(
        Booking,
        on_delete=models.PROTECT,
        related_name="payments",
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
        max_length=30,
        choices=STATUS_CHOICES,
        default="pending",
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["booking", "status"]
            )
        ]
```

---

# 18. Review

```python
class Review(BaseModel):

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    room = models.ForeignKey(
        Room,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="reviews",
    )

    customer = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="hotel_reviews",
    )

    booking = models.ForeignKey(
        Booking,
        on_delete=models.PROTECT,
        related_name="reviews",
    )

    rating = models.PositiveSmallIntegerField()

    title = models.CharField(
        max_length=200,
        blank=True,
    )

    comment = models.TextField(
        blank=True
    )

    is_verified = models.BooleanField(
        default=False
    )

    is_published = models.BooleanField(
        default=True
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=(
                    models.Q(rating__gte=1)
                    & models.Q(rating__lte=5)
                ),
                name="review_rating_1_5",
            ),

            models.UniqueConstraint(
                fields=["customer", "booking"],
                name="one_review_per_booking",
            ),
        ]

        indexes = [
            models.Index(
                fields=["hotel", "-created_at"]
            ),
            models.Index(
                fields=["rating"]
            ),
        ]
```

---

# 19. Wishlist

```python
class Wishlist(BaseModel):

    customer = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="hotel_wishlist",
    )
```

---

# 20. Wishlist Hotel

```python
class WishlistHotel(BaseModel):

    wishlist = models.ForeignKey(
        Wishlist,
        on_delete=models.CASCADE,
        related_name="items",
    )

    hotel = models.ForeignKey(
        Hotel,
        on_delete=models.CASCADE,
        related_name="wishlists",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["wishlist", "hotel"],
                name="unique_wishlist_hotel",
            )
        ]
```

---

# 21. Coupon

```python
class Coupon(BaseModel):

    DISCOUNT_TYPES = [
        ("percentage", "Percentage"),
        ("fixed", "Fixed"),
    ]

    code = models.CharField(
        max_length=50,
        unique=True,
    )

    discount_type = models.CharField(
        max_length=20,
        choices=DISCOUNT_TYPES,
    )

    discount_value = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    minimum_amount = models.DecimalField(
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
```

---

# 22. Coupon Usage

```python
class CouponUsage(BaseModel):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT,
        related_name="usages",
    )

    customer = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="coupon_usages",
    )

    booking = models.ForeignKey(
        Booking,
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
                fields=["coupon", "customer", "booking"],
                name="unique_coupon_usage",
            )
        ]
```

---

# 23. Commission

Platform কত টাকা রাখবে:

```python
class Commission(BaseModel):

    booking = models.OneToOneField(
        Booking,
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
```

Example:

```text
Booking = ৳10,000

Platform = ৳1,000
Vendor   = ৳9,000
```

---

# 24. Vendor Payout

```python
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
```

---

# 25. Notification

```python
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

    notification_type = models.CharField(
        max_length=50
    )

    is_read = models.BooleanField(
        default=False
    )

    class Meta:
        indexes = [
            models.Index(
                fields=[
                    "user",
                    "is_read",
                    "-created_at",
                ]
            )
        ]
```

---

# 26. Idempotency Record

Booking/payment duplicate request prevent করতে:

```python
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
```

---

# 27. Audit Log

```python
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

---

# 🔗 Complete Relationship

এখন পুরো system-টা এভাবে চিন্তা করো:

```text
                         USER
                          │
              ┌───────────┴───────────┐
              │                       │
            VENDOR                 CUSTOMER
              │                       │
       ┌──────┼───────┐       ┌───────┼────────┐
       │      │       │       │       │        │
     Hotel  Staff   Service  Address Wishlist Booking
       │                           │             │
       ├──────────────┐            │       ┌─────┼─────┐
       │              │            │       │     │     │
     Rooms         Amenities       │     Payment Review Coupon
       │                           │
       ├── RoomImage               │
       ├── RoomAmenity             │
       └── Inventory               │
                                   
Booking
   │
   ├── Room
   ├── Hotel
   ├── Customer
   ├── BookingService
   ├── Payment
   ├── Review
   ├── CouponUsage
   └── Commission
          │
          └── Vendor
                 │
                 └── VendorPayout
```

---

# ⭐ সবচেয়ে গুরুত্বপূর্ণ ORM Relationships

তোমার practice-এর জন্য এগুলো বিশেষভাবে গুরুত্বপূর্ণ:

### Vendor → Hotels

```python
vendor.hotels.all()
```

### Hotel → Rooms

```python
hotel.rooms.all()
```

### Hotel → Bookings

```python
hotel.bookings.all()
```

### Room → Bookings

```python
room.bookings.all()
```

### Customer → Bookings

```python
customer.bookings.all()
```

### Booking → Services

```python
booking.booking_services.all()
```

### Product-এর বদলে এখানে Hotel-এর nested relationship

```python
Booking.objects.filter(
    hotel__vendor=vendor
)
```

এটাই **multi-vendor ORM-এর সবচেয়ে গুরুত্বপূর্ণ query pattern**।

---

# 🔥 তোমার ORM Practice-এর জন্য Core Queries

এই project দিয়ে তুমি practice করবে:

```text
1. Vendor → Hotels
2. Vendor → Rooms
3. Vendor → Bookings
4. Vendor → Revenue
5. Hotel → Rooms
6. Hotel → Bookings
7. Room → Booking history
8. Customer → Booking history
9. Available rooms
10. Booking overlap
11. Hotel search
12. Room filtering
13. Price filtering
14. Capacity filtering
15. Hotel rating
16. Review aggregation
17. Average hotel rating
18. Total hotel bookings
19. Vendor total revenue
20. Monthly revenue
21. Top hotels
22. Top vendors
23. Customer spending
24. Repeat customers
25. Latest booking
26. Exists booking
27. Subquery latest booking
28. Window ranking
29. select_related
30. prefetch_related
31. Prefetch
32. Q()
33. F()
34. Case/When
35. transaction.atomic()
36. select_for_update()
37. Idempotency
38. ExclusionConstraint
39. Database constraints
40. EXPLAIN
```

---

## 🧠 বিশেষ একটা গুরুত্বপূর্ণ design point

আগের Hotel project-এ আমরা `check_in`, `check_out` দিয়ে overlap check করেছিলাম। **Production PostgreSQL version**-এ চাইলে `Booking`-এ `DateRangeField` যোগ করে database-level `ExclusionConstraint` ব্যবহার করা যায়।

Concept:

```text
Room A

Booking 1:
[Sep 10, Sep 15)

Booking 2:
[Sep 15, Sep 20)

✅ Allowed

Booking 3:
[Sep 13, Sep 18)

❌ Conflict
```

এতে তোমার আগের শেখা:

```text
DateRangeField
+
ExclusionConstraint
+
transaction.atomic()
+
select_for_update()
+
Idempotency
```

একসাথে practice করা যাবে।

---

# 🏆 পুরো Project-এর Modules

```text
multi_vendor_hotel/
│
├── accounts
│
├── vendors
│
├── hotels
│
├── rooms
│
├── bookings
│
├── payments
│
├── reviews
│
├── coupons
│
├── commissions
│
├── payouts
│
├── notifications
│
└── audit
```

**এই model set-টাই তোমার practice database হিসেবে ব্যবহার করো।** প্রথমে সব model লিখে migration করবে, তারপর আমি হলে **Phase 1: Django Shell ORM Practice — 50টি প্রশ্ন** দিয়ে শুরু করতাম; এরপর Phase 2-তে `select_related/prefetch`, Phase 3-তে aggregation/subquery/window, আর শেষে **concurrent booking engine** বানাতাম।