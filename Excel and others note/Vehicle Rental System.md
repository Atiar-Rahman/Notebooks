অবশ্যই। এবার **Vehicle Rental System**-এর জন্যও আগের **E-commerce → Hotel → Property/Rental** pattern-এর মতো একটি **complete production-style Django ORM model architecture** দিচ্ছি।

এটাকে আমরা **Multi-Vendor Vehicle Rental Marketplace** হিসেবে ধরব—যেখানে একাধিক vehicle owner/company vehicle list করবে, customer rent করবে, payment করবে, vehicle return করবে, maintenance/history track হবে।

---

# 🚗 Complete Vehicle Rental Model Architecture

```text
USER
│
├── OWNER / RENTAL COMPANY
│   ├── Membership
│   ├── Vehicles
│   ├── Pricing
│   ├── Maintenance
│   └── Payouts
│
└── CUSTOMER
    ├── Profile
    ├── Address
    ├── Rental
    ├── Payment
    ├── Review
    └── Wishlist
```

---

# 1. BaseModel

```python
from django.db import models
from django.conf import settings


class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

---

# 2. Vehicle Owner

একজন owner অনেক vehicle রাখতে পারবে।

```python
class VehicleOwner(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("approved", "Approved"),
        ("suspended", "Suspended"),
        ("rejected", "Rejected"),
    ]

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="vehicle_owner_profile",
    )

    business_name = models.CharField(
        max_length=150,
        blank=True,
    )

    email = models.EmailField()

    phone = models.CharField(
        max_length=30,
    )

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

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(fields=["status"]),
            models.Index(fields=["is_active"]),
        ]

    def __str__(self):
        return self.business_name or self.user.get_username()
```

---

# 3. Owner Membership

Owner-এর manager, accountant, staff ইত্যাদি।

```python
class VehicleOwnerMembership(BaseModel):

    ROLE_CHOICES = [
        ("owner", "Owner"),
        ("manager", "Manager"),
        ("accountant", "Accountant"),
        ("staff", "Staff"),
        ("maintenance", "Maintenance"),
    ]

    owner = models.ForeignKey(
        VehicleOwner,
        on_delete=models.CASCADE,
        related_name="memberships",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="vehicle_owner_memberships",
    )

    role = models.CharField(
        max_length=30,
        choices=ROLE_CHOICES,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["owner", "user"],
                name="unique_vehicle_owner_member",
            )
        ]
```

---

# 4. Vehicle Category

```text
Car
SUV
Bike
Microbus
Bus
Truck
Van
Luxury
```

```python
class VehicleCategory(BaseModel):

    name = models.CharField(
        max_length=100,
        unique=True,
    )

    description = models.TextField(
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    def __str__(self):
        return self.name
```

---

# 5. Vehicle Brand

```text
Toyota
Honda
Nissan
BMW
Mercedes
Tesla
```

```python
class VehicleBrand(BaseModel):

    name = models.CharField(
        max_length=100,
        unique=True,
    )

    logo = models.ImageField(
        upload_to="vehicle_brands/",
        blank=True,
        null=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    def __str__(self):
        return self.name
```

---

# 6. Vehicle Model

```python
class VehicleModel(BaseModel):

    brand = models.ForeignKey(
        VehicleBrand,
        on_delete=models.PROTECT,
        related_name="models",
    )

    name = models.CharField(
        max_length=100,
    )

    category = models.ForeignKey(
        VehicleCategory,
        on_delete=models.PROTECT,
        related_name="vehicle_models",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["brand", "name"],
                name="unique_vehicle_model",
            )
        ]

    def __str__(self):
        return f"{self.brand.name} {self.name}"
```

---

# 7. Vehicle

এটাই main vehicle entity।

```python
class Vehicle(BaseModel):

    STATUS_CHOICES = [
        ("available", "Available"),
        ("reserved", "Reserved"),
        ("rented", "Rented"),
        ("maintenance", "Maintenance"),
        ("inactive", "Inactive"),
    ]

    TRANSMISSION_CHOICES = [
        ("manual", "Manual"),
        ("automatic", "Automatic"),
    ]

    FUEL_CHOICES = [
        ("petrol", "Petrol"),
        ("diesel", "Diesel"),
        ("octane", "Octane"),
        ("cng", "CNG"),
        ("electric", "Electric"),
        ("hybrid", "Hybrid"),
    ]

    owner = models.ForeignKey(
        VehicleOwner,
        on_delete=models.PROTECT,
        related_name="vehicles",
    )

    model = models.ForeignKey(
        VehicleModel,
        on_delete=models.PROTECT,
        related_name="vehicles",
    )

    registration_number = models.CharField(
        max_length=50,
        unique=True,
    )

    vin_number = models.CharField(
        max_length=100,
        unique=True,
        blank=True,
        null=True,
    )

    manufacturing_year = models.PositiveIntegerField()

    color = models.CharField(
        max_length=50,
    )

    seats = models.PositiveIntegerField()

    transmission = models.CharField(
        max_length=20,
        choices=TRANSMISSION_CHOICES,
    )

    fuel_type = models.CharField(
        max_length=20,
        choices=FUEL_CHOICES,
    )

    mileage = models.PositiveIntegerField(
        default=0,
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="available",
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["owner", "status"]
            ),
            models.Index(
                fields=["model", "status"]
            ),
            models.Index(
                fields=["status", "is_active"]
            ),
        ]

    def __str__(self):
        return self.registration_number
```

---

# 8. Vehicle Image

```python
class VehicleImage(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="vehicles/",
    )

    caption = models.CharField(
        max_length=200,
        blank=True,
    )

    is_primary = models.BooleanField(
        default=False,
    )

    sort_order = models.PositiveIntegerField(
        default=0,
    )

    class Meta:
        ordering = ["sort_order", "id"]
```

---

# 9. Vehicle Feature

```text
GPS
AC
Bluetooth
Airbag
Sunroof
Camera
ABS
Child Seat
```

```python
class VehicleFeature(BaseModel):

    name = models.CharField(
        max_length=100,
        unique=True,
    )

    icon = models.CharField(
        max_length=100,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    def __str__(self):
        return self.name
```

---

# 10. Vehicle Feature Mapping

```python
class VehicleFeatureMapping(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="features",
    )

    feature = models.ForeignKey(
        VehicleFeature,
        on_delete=models.PROTECT,
        related_name="vehicle_mappings",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["vehicle", "feature"],
                name="unique_vehicle_feature",
            )
        ]
```

---

# 11. Rental Location

Vehicle কোথা থেকে pickup/dropoff হবে।

```python
class RentalLocation(BaseModel):

    owner = models.ForeignKey(
        VehicleOwner,
        on_delete=models.CASCADE,
        related_name="locations",
    )

    name = models.CharField(
        max_length=150,
    )

    address = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    country = models.CharField(
        max_length=100,
    )

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

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["owner", "city"]
            ),
        ]
```

---

# 12. Vehicle Location Mapping

একটি vehicle কোন location-এ available।

```python
class VehicleLocation(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="locations",
    )

    location = models.ForeignKey(
        RentalLocation,
        on_delete=models.PROTECT,
        related_name="vehicles",
    )

    is_primary = models.BooleanField(
        default=False,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["vehicle", "location"],
                name="unique_vehicle_location",
            )
        ]
```

---

# 13. Vehicle Pricing

Daily/weekly/monthly pricing।

```python
class VehiclePricing(BaseModel):

    vehicle = models.OneToOneField(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="pricing",
    )

    hourly_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    daily_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    weekly_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    monthly_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    security_deposit = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    extra_km_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    late_fee_per_hour = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=models.Q(daily_rate__gte=0),
                name="daily_rate_non_negative",
            ),
        ]
```

---

# 14. Vehicle Availability

```python
class VehicleAvailability(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="availability_periods",
    )

    start_date = models.DateTimeField()

    end_date = models.DateTimeField()

    is_available = models.BooleanField(
        default=True,
    )

    reason = models.CharField(
        max_length=200,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["vehicle", "start_date", "end_date"]
            ),
        ]
```

---

# 15. Customer Profile

```python
class RentalCustomerProfile(BaseModel):

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="rental_customer_profile",
    )

    phone = models.CharField(
        max_length=30,
        blank=True,
    )

    date_of_birth = models.DateField(
        null=True,
        blank=True,
    )

    is_verified = models.BooleanField(
        default=False,
    )
```

---

# 16. Customer Address

```python
class RentalCustomerAddress(BaseModel):

    customer = models.ForeignKey(
        RentalCustomerProfile,
        on_delete=models.CASCADE,
        related_name="addresses",
    )

    full_name = models.CharField(
        max_length=150,
    )

    phone = models.CharField(
        max_length=30,
    )

    address_line = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    country = models.CharField(
        max_length=100,
    )

    postal_code = models.CharField(
        max_length=20,
        blank=True,
    )

    is_default = models.BooleanField(
        default=False,
    )
```

---

# 17. Rental Booking

এটাই system-এর সবচেয়ে important model।

```python
class RentalBooking(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("confirmed", "Confirmed"),
        ("active", "Active"),
        ("completed", "Completed"),
        ("cancelled", "Cancelled"),
        ("no_show", "No Show"),
        ("refunded", "Refunded"),
    ]

    customer = models.ForeignKey(
        RentalCustomerProfile,
        on_delete=models.PROTECT,
        related_name="bookings",
    )

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.PROTECT,
        related_name="bookings",
    )

    pickup_location = models.ForeignKey(
        RentalLocation,
        on_delete=models.PROTECT,
        related_name="pickup_bookings",
    )

    dropoff_location = models.ForeignKey(
        RentalLocation,
        on_delete=models.PROTECT,
        related_name="dropoff_bookings",
    )

    booking_number = models.CharField(
        max_length=100,
        unique=True,
    )

    pickup_at = models.DateTimeField()

    dropoff_at = models.DateTimeField()

    rental_days = models.PositiveIntegerField()

    base_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    extra_charge = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    discount_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    security_deposit = models.DecimalField(
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
        blank=True,
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=models.Q(
                    dropoff_at__gt=models.F("pickup_at")
                ),
                name="dropoff_after_pickup",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    total_amount__gte=0
                ),
                name="booking_total_non_negative",
            ),
        ]

        indexes = [
            models.Index(
                fields=["vehicle", "pickup_at", "dropoff_at"]
            ),
            models.Index(
                fields=["customer", "-created_at"]
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]
```

---

# 18. Booking Extra

যেমন:

```text
GPS
Child Seat
Additional Driver
Insurance
```

```python
class BookingExtra(BaseModel):

    booking = models.ForeignKey(
        RentalBooking,
        on_delete=models.CASCADE,
        related_name="extras",
    )

    name = models.CharField(
        max_length=150,
    )

    quantity = models.PositiveIntegerField(
        default=1,
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 19. Vehicle Handover

Customer vehicle নেওয়ার সময় condition record।

```python
class VehicleHandover(BaseModel):

    HANDOVER_TYPES = [
        ("pickup", "Pickup"),
        ("return", "Return"),
    ]

    booking = models.ForeignKey(
        RentalBooking,
        on_delete=models.CASCADE,
        related_name="handovers",
    )

    handover_type = models.CharField(
        max_length=20,
        choices=HANDOVER_TYPES,
    )

    mileage = models.PositiveIntegerField()

    fuel_level = models.DecimalField(
        max_digits=5,
        decimal_places=2,
    )

    notes = models.TextField(
        blank=True,
    )

    handover_at = models.DateTimeField()

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["booking", "handover_type"],
                name="unique_booking_handover_type",
            )
        ]
```

---

# 20. Handover Image

Vehicle-এর condition-এর ছবি।

```python
class HandoverImage(BaseModel):

    handover = models.ForeignKey(
        VehicleHandover,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="vehicle_handovers/",
    )

    description = models.CharField(
        max_length=200,
        blank=True,
    )
```

---

# 21. Payment

```python
class RentalPayment(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
        ("partial", "Partial"),
    ]

    METHOD_CHOICES = [
        ("cash", "Cash"),
        ("card", "Card"),
        ("bank", "Bank"),
        ("mobile_banking", "Mobile Banking"),
    ]

    booking = models.ForeignKey(
        RentalBooking,
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
        max_length=20,
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
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]
```

---

# 22. Damage Report

Return করার পরে damage পাওয়া গেলে।

```python
class DamageReport(BaseModel):

    STATUS_CHOICES = [
        ("reported", "Reported"),
        ("reviewing", "Reviewing"),
        ("approved", "Approved"),
        ("rejected", "Rejected"),
        ("resolved", "Resolved"),
    ]

    booking = models.ForeignKey(
        RentalBooking,
        on_delete=models.PROTECT,
        related_name="damage_reports",
    )

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.PROTECT,
        related_name="damage_reports",
    )

    description = models.TextField()

    estimated_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    final_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="reported",
    )
```

---

# 23. Damage Image

```python
class DamageImage(BaseModel):

    damage_report = models.ForeignKey(
        DamageReport,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="vehicle_damage/",
    )
```

---

# 24. Maintenance Record

Vehicle-এর complete maintenance history।

```python
class VehicleMaintenance(BaseModel):

    MAINTENANCE_TYPES = [
        ("service", "Service"),
        ("repair", "Repair"),
        ("oil_change", "Oil Change"),
        ("tire", "Tire"),
        ("inspection", "Inspection"),
        ("other", "Other"),
    ]

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.PROTECT,
        related_name="maintenance_records",
    )

    maintenance_type = models.CharField(
        max_length=30,
        choices=MAINTENANCE_TYPES,
    )

    description = models.TextField()

    mileage = models.PositiveIntegerField()

    cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    maintenance_date = models.DateField()

    next_service_date = models.DateField(
        null=True,
        blank=True,
    )

    next_service_mileage = models.PositiveIntegerField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["vehicle", "-maintenance_date"]
            ),
        ]
```

---

# 25. Vehicle Insurance

```python
class VehicleInsurance(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="insurance_records",
    )

    provider = models.CharField(
        max_length=150,
    )

    policy_number = models.CharField(
        max_length=150,
        unique=True,
    )

    start_date = models.DateField()

    end_date = models.DateField()

    coverage_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["vehicle", "end_date"]
            ),
        ]
```

---

# 26. Vehicle Document

যেমন registration, tax token, fitness certificate ইত্যাদি।

```python
class VehicleDocument(BaseModel):

    DOCUMENT_TYPES = [
        ("registration", "Registration"),
        ("tax_token", "Tax Token"),
        ("fitness", "Fitness"),
        ("insurance", "Insurance"),
        ("other", "Other"),
    ]

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="documents",
    )

    document_type = models.CharField(
        max_length=30,
        choices=DOCUMENT_TYPES,
    )

    document_number = models.CharField(
        max_length=150,
        blank=True,
    )

    document_file = models.FileField(
        upload_to="vehicle_documents/",
    )

    expiry_date = models.DateField(
        null=True,
        blank=True,
    )

    is_verified = models.BooleanField(
        default=False,
    )
```

---

# 27. Review

```python
class VehicleReview(BaseModel):

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    customer = models.ForeignKey(
        RentalCustomerProfile,
        on_delete=models.CASCADE,
        related_name="vehicle_reviews",
    )

    booking = models.ForeignKey(
        RentalBooking,
        on_delete=models.PROTECT,
        related_name="review",
    )

    rating = models.PositiveSmallIntegerField()

    title = models.CharField(
        max_length=200,
        blank=True,
    )

    comment = models.TextField(
        blank=True,
    )

    is_published = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=(
                    models.Q(rating__gte=1)
                    & models.Q(rating__lte=5)
                ),
                name="vehicle_rating_1_5",
            ),

            models.UniqueConstraint(
                fields=["customer", "booking"],
                name="one_review_per_vehicle_booking",
            ),
        ]

        indexes = [
            models.Index(
                fields=["vehicle", "-created_at"]
            ),
        ]
```

---

# 28. Wishlist

```python
class VehicleWishlist(BaseModel):

    customer = models.OneToOneField(
        RentalCustomerProfile,
        on_delete=models.CASCADE,
        related_name="wishlist",
    )
```

---

# 29. Wishlist Vehicle

```python
class VehicleWishlistItem(BaseModel):

    wishlist = models.ForeignKey(
        VehicleWishlist,
        on_delete=models.CASCADE,
        related_name="items",
    )

    vehicle = models.ForeignKey(
        Vehicle,
        on_delete=models.CASCADE,
        related_name="wishlist_items",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["wishlist", "vehicle"],
                name="unique_wishlist_vehicle",
            )
        ]
```

---

# 30. Coupon

```python
class VehicleCoupon(BaseModel):

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
        default=0,
    )

    valid_from = models.DateTimeField()

    valid_until = models.DateTimeField()

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 31. Coupon Usage

```python
class VehicleCouponUsage(BaseModel):

    coupon = models.ForeignKey(
        VehicleCoupon,
        on_delete=models.PROTECT,
        related_name="usages",
    )

    customer = models.ForeignKey(
        RentalCustomerProfile,
        on_delete=models.PROTECT,
        related_name="coupon_usages",
    )

    booking = models.ForeignKey(
        RentalBooking,
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
                name="unique_coupon_booking_usage",
            )
        ]
```

---

# 32. Owner Commission

```python
class VehicleOwnerCommission(BaseModel):

    owner = models.ForeignKey(
        VehicleOwner,
        on_delete=models.PROTECT,
        related_name="commissions",
    )

    booking = models.OneToOneField(
        RentalBooking,
        on_delete=models.PROTECT,
        related_name="commission",
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

    owner_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 33. Owner Payout

```python
class VehicleOwnerPayout(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("processing", "Processing"),
        ("paid", "Paid"),
        ("failed", "Failed"),
    ]

    owner = models.ForeignKey(
        VehicleOwner,
        on_delete=models.PROTECT,
        related_name="payouts",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    reference = models.CharField(
        max_length=150,
        unique=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

---

# 34. Notification

```python
class VehicleNotification(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="vehicle_notifications",
    )

    title = models.CharField(
        max_length=200,
    )

    message = models.TextField()

    notification_type = models.CharField(
        max_length=50,
    )

    is_read = models.BooleanField(
        default=False,
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

# 35. Idempotency Record

Payment/booking duplicate request prevent করতে।

```python
class VehicleIdempotencyRecord(BaseModel):

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
        related_name="vehicle_idempotency_records",
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

# 36. Audit Log

```python
class VehicleAuditLog(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="vehicle_audit_logs",
    )

    action = models.CharField(
        max_length=100,
    )

    model_name = models.CharField(
        max_length=100,
    )

    object_id = models.CharField(
        max_length=100,
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

# 🔗 Complete Relationship Diagram

```text
                         USER
                          │
             ┌────────────┴─────────────┐
             │                          │
          OWNER                      CUSTOMER
             │                          │
       ┌─────┴─────┐             ┌──────┴──────┐
       │           │             │             │
   Membership   Vehicles       Profile      Wishlist
                   │
       ┌───────────┼───────────────┐
       │           │               │
     Model       Images         Features
       │
   Brand + Category
                   │
          ┌────────┼─────────┐
          │        │         │
       Pricing  Location  Availability
          │
       Vehicle
          │
       Booking
          │
    ┌─────┼─────────────┐
    │     │             │
 Payment Extras     Handover
                       │
                 ┌─────┴─────┐
                 │           │
              Images      Damage
                              │
                           Images

Vehicle
  │
  ├── Maintenance
  ├── Insurance
  ├── Documents
  ├── Reviews
  └── Bookings
          │
       Commission
          │
      Owner Payout
```

---

# 🚘 Main Rental Flow

```text
Owner
  ↓
Vehicle
  ↓
Pricing
  ↓
Vehicle published
  ↓
Customer searches
  ↓
Availability check
  ↓
RentalBooking
  ↓
Payment
  ↓
Confirmed
  ↓
Vehicle Pickup
  ↓
Active Rental
  ↓
Vehicle Return
  ↓
Damage Check
  ↓
Completed
  ↓
Review
  ↓
Owner Payout
```

---

# 🔥 সবচেয়ে গুরুত্বপূর্ণ Business Logic

Vehicle rental system-এর সবচেয়ে কঠিন অংশ হলো **double booking prevention**।

ধরো:

```text
Vehicle: Toyota Axio

Existing booking:
Sep 15 ───────── Sep 20

New booking:
       Sep 18 ───────── Sep 22

              ❌ CONFLICT
```

Basic overlap query:

```python
RentalBooking.objects.filter(
    vehicle=vehicle,
    pickup_at__lt=requested_dropoff,
    dropoff_at__gt=requested_pickup,
    status__in=[
        "pending",
        "confirmed",
        "active",
    ],
).exists()
```

কিন্তু production-এ শুধু এই query যথেষ্ট না।

ব্যবহার করবে:

```text
transaction.atomic()
        +
select_for_update()
        +
PostgreSQL range
        +
ExclusionConstraint
        +
Idempotency
```

তাহলে concurrent booking-এর race condition handle করা যাবে।

---

# 🧠 Owner Isolation

Owner A যেন Owner B-এর vehicle দেখতে না পারে:

```python
Vehicle.objects.filter(
    owner=request.user.vehicle_owner_profile
)
```

Owner-এর bookings:

```python
RentalBooking.objects.filter(
    vehicle__owner=request.user.vehicle_owner_profile
)
```

Owner revenue:

```python
RentalPayment.objects.filter(
    booking__vehicle__owner=owner,
    status="paid",
)
```

Owner maintenance:

```python
VehicleMaintenance.objects.filter(
    vehicle__owner=owner
)
```

---

# 📊 এই Project দিয়ে ORM Practice

```text
1. Vehicle CRUD
2. Owner → Vehicles
3. Vehicle → Owner
4. Brand → Models
5. Category → Vehicles
6. Vehicle → Features
7. Vehicle → Images
8. Vehicle → Pricing
9. Vehicle → Locations
10. Vehicle → Bookings

11. Available vehicles
12. Rented vehicles
13. Maintenance vehicles
14. Search by city
15. Search by category
16. Search by brand
17. Search by price
18. Search by transmission
19. Search by fuel
20. Search by seats

21. Customer bookings
22. Owner bookings
23. Active rentals
24. Completed rentals
25. Cancelled rentals

26. Revenue
27. Monthly revenue
28. Owner revenue
29. Platform commission
30. Average rental price

31. Count()
32. Sum()
33. Avg()
34. Min()
35. Max()

36. annotate()
37. aggregate()
38. Q()
39. F()
40. Case()
41. When()

42. Exists()
43. Subquery()
44. OuterRef()
45. Window Functions

46. select_related()
47. prefetch_related()
48. Prefetch()

49. transaction.atomic()
50. select_for_update()
51. Race Condition
52. Double Booking
53. Idempotency
54. Constraints
55. EXPLAIN
56. Query Optimization
57. Pagination
58. Filtering
59. Sorting
60. Multi-Tenant Isolation
```

---

# 🏆 Recommended App Structure

Production project হলে:

```text
vehicle_rental/
│
├── accounts/
│
├── owners/
│
├── vehicles/
│
├── locations/
│
├── customers/
│
├── bookings/
│
├── payments/
│
├── maintenance/
│
├── insurance/
│
├── damage/
│
├── reviews/
│
├── promotions/
│
├── commissions/
│
├── payouts/
│
├── notifications/
│
└── audit/
```

### সবচেয়ে important 8টা app

```text
accounts
   ↓
owners
   ↓
vehicles
   ↓
customers
   ↓
bookings
   ↓
payments
   ↓
maintenance
   ↓
reviews
```

এটা **Hotel Management + Property Rental + E-commerce**-এর পর ORM practice-এর জন্য খুব strong project, কারণ এখানে একই সাথে **relationship, availability, financial transaction, concurrency, double-booking, reporting, optimization এবং multi-vendor isolation**—সবগুলো বাস্তবে practice করা যাবে।

