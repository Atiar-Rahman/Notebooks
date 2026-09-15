অবশ্যই। এবার **Property/Rental Management System**-এর জন্য আগের Multi-Vendor Hotel-এর মতো **complete production-style model set** দিচ্ছি।

এটা আমরা **Airbnb/Booking rental marketplace + Property Management System** হিসেবে ধরব।

```text
Platform
│
├── Users
│
├── Landlords / Property Owners
│   ├── Properties
│   ├── Units
│   ├── Amenities
│   ├── Pricing
│   └── Maintenance
│
├── Tenants / Customers
│   ├── Addresses
│   ├── Applications
│   ├── Bookings / Rentals
│   ├── Payments
│   └── Reviews
│
└── Platform
    ├── Commissions
    ├── Payouts
    ├── Coupons
    ├── Notifications
    └── Audit Logs
```

---

# 🏗️ Complete Model Set

## 1. BaseModel

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

# 2. Owner / Landlord

একজন owner অনেক property রাখতে পারবে।

```python
class Owner(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("approved", "Approved"),
        ("suspended", "Suspended"),
        ("rejected", "Rejected"),
    ]

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="owner_profile",
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

# 3. Owner Membership / Staff

Property manager, accountant, maintenance staff ইত্যাদি।

```python
class OwnerMembership(BaseModel):

    ROLE_CHOICES = [
        ("owner", "Owner"),
        ("manager", "Manager"),
        ("accountant", "Accountant"),
        ("maintenance", "Maintenance"),
        ("staff", "Staff"),
    ]

    owner = models.ForeignKey(
        Owner,
        on_delete=models.CASCADE,
        related_name="memberships",
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="owner_memberships",
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
                name="unique_owner_member",
            )
        ]
```

---

# 4. Property

মূল property/building/house।

```python
class Property(BaseModel):

    PROPERTY_TYPES = [
        ("apartment", "Apartment"),
        ("house", "House"),
        ("villa", "Villa"),
        ("office", "Office"),
        ("shop", "Shop"),
        ("warehouse", "Warehouse"),
        ("land", "Land"),
        ("commercial", "Commercial"),
    ]

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("pending", "Pending Approval"),
        ("active", "Active"),
        ("inactive", "Inactive"),
        ("blocked", "Blocked"),
    ]

    owner = models.ForeignKey(
        Owner,
        on_delete=models.PROTECT,
        related_name="properties",
    )

    name = models.CharField(
        max_length=200,
    )

    slug = models.SlugField()

    property_type = models.CharField(
        max_length=30,
        choices=PROPERTY_TYPES,
    )

    description = models.TextField(
        blank=True,
    )

    address = models.TextField()

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

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="draft",
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["owner", "slug"],
                name="unique_property_slug_per_owner",
            ),
        ]

        indexes = [
            models.Index(
                fields=["owner", "status"]
            ),
            models.Index(
                fields=["city", "status"]
            ),
            models.Index(
                fields=["property_type", "status"]
            ),
        ]

    def __str__(self):
        return self.name
```

---

# 5. Property Image

```python
class PropertyImage(BaseModel):

    property = models.ForeignKey(
        Property,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="properties/",
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

# 6. Amenity

```text
WiFi
Parking
Swimming Pool
Gym
Generator
Elevator
Security
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
        default=True,
    )

    def __str__(self):
        return self.name
```

---

# 7. Property Amenity

```python
class PropertyAmenity(BaseModel):

    property = models.ForeignKey(
        Property,
        on_delete=models.CASCADE,
        related_name="property_amenities",
    )

    amenity = models.ForeignKey(
        Amenity,
        on_delete=models.PROTECT,
        related_name="property_amenities",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["property", "amenity"],
                name="unique_property_amenity",
            )
        ]
```

---

# 8. Unit Type

একটি property-তে multiple unit থাকতে পারে।

```text
1 Bedroom
2 Bedroom
3 Bedroom
Studio
Shop
Office
```

```python
class UnitType(BaseModel):

    name = models.CharField(
        max_length=100,
    )

    description = models.TextField(
        blank=True,
    )

    bedrooms = models.PositiveIntegerField(
        default=0,
    )

    bathrooms = models.PositiveIntegerField(
        default=0,
    )

    max_occupants = models.PositiveIntegerField(
        default=1,
    )

    is_active = models.BooleanField(
        default=True,
    )

    def __str__(self):
        return self.name
```

---

# 9. Unit

একটি apartment/building-এর individual rental unit।

```python
class Unit(BaseModel):

    STATUS_CHOICES = [
        ("available", "Available"),
        ("occupied", "Occupied"),
        ("maintenance", "Maintenance"),
        ("reserved", "Reserved"),
        ("inactive", "Inactive"),
    ]

    property = models.ForeignKey(
        Property,
        on_delete=models.PROTECT,
        related_name="units",
    )

    unit_type = models.ForeignKey(
        UnitType,
        on_delete=models.PROTECT,
        related_name="units",
    )

    unit_number = models.CharField(
        max_length=50,
    )

    floor = models.IntegerField(
        null=True,
        blank=True,
    )

    area_sqft = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        null=True,
        blank=True,
    )

    bedrooms = models.PositiveIntegerField(
        default=0,
    )

    bathrooms = models.PositiveIntegerField(
        default=0,
    )

    monthly_rent = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    security_deposit = models.DecimalField(
        max_digits=12,
        decimal_places=2,
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
        constraints = [
            models.UniqueConstraint(
                fields=["property", "unit_number"],
                name="unique_unit_number_per_property",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    monthly_rent__gte=0
                ),
                name="unit_rent_non_negative",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    security_deposit__gte=0
                ),
                name="security_deposit_non_negative",
            ),
        ]

        indexes = [
            models.Index(
                fields=["property", "status"]
            ),
            models.Index(
                fields=["unit_type", "monthly_rent"]
            ),
        ]

    def __str__(self):
        return f"{self.property.name} - {self.unit_number}"
```

---

# 10. Unit Image

```python
class UnitImage(BaseModel):

    unit = models.ForeignKey(
        Unit,
        on_delete=models.CASCADE,
        related_name="images",
    )

    image = models.ImageField(
        upload_to="units/",
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
```

---

# 11. Unit Amenity

```python
class UnitAmenity(BaseModel):

    unit = models.ForeignKey(
        Unit,
        on_delete=models.CASCADE,
        related_name="unit_amenities",
    )

    amenity = models.ForeignKey(
        Amenity,
        on_delete=models.PROTECT,
        related_name="unit_amenities",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["unit", "amenity"],
                name="unique_unit_amenity",
            )
        ]
```

---

# 12. Tenant Profile

```python
class TenantProfile(BaseModel):

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="tenant_profile",
    )

    date_of_birth = models.DateField(
        null=True,
        blank=True,
    )

    occupation = models.CharField(
        max_length=150,
        blank=True,
    )

    phone = models.CharField(
        max_length=30,
        blank=True,
    )

    emergency_contact = models.CharField(
        max_length=30,
        blank=True,
    )

    is_verified = models.BooleanField(
        default=False,
    )
```

---

# 13. Tenant Address

```python
class TenantAddress(BaseModel):

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.CASCADE,
        related_name="addresses",
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

# 14. Rental Application

Long-term rental-এর জন্য application।

```python
class RentalApplication(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("approved", "Approved"),
        ("rejected", "Rejected"),
        ("cancelled", "Cancelled"),
    ]

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.PROTECT,
        related_name="applications",
    )

    unit = models.ForeignKey(
        Unit,
        on_delete=models.PROTECT,
        related_name="applications",
    )

    move_in_date = models.DateField()

    requested_duration_months = models.PositiveIntegerField()

    message = models.TextField(
        blank=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["unit", "status"]
            ),
            models.Index(
                fields=["tenant", "-created_at"]
            ),
        ]
```

---

# 15. Rental Agreement / Lease

Application approve হওয়ার পর actual contract।

```python
class Lease(BaseModel):

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("active", "Active"),
        ("expired", "Expired"),
        ("terminated", "Terminated"),
        ("cancelled", "Cancelled"),
    ]

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.PROTECT,
        related_name="leases",
    )

    unit = models.ForeignKey(
        Unit,
        on_delete=models.PROTECT,
        related_name="leases",
    )

    lease_number = models.CharField(
        max_length=100,
        unique=True,
    )

    start_date = models.DateField()

    end_date = models.DateField()

    monthly_rent = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    security_deposit = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="draft",
    )

    terms = models.TextField(
        blank=True,
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=models.Q(
                    end_date__gt=models.F("start_date")
                ),
                name="lease_end_after_start",
            ),

            models.CheckConstraint(
                condition=models.Q(
                    monthly_rent__gte=0
                ),
                name="lease_rent_non_negative",
            ),
        ]

        indexes = [
            models.Index(
                fields=["unit", "status"]
            ),
            models.Index(
                fields=["tenant", "status"]
            ),
            models.Index(
                fields=["start_date", "end_date"]
            ),
        ]
```

---

# 16. Lease Document

```python
class LeaseDocument(BaseModel):

    lease = models.ForeignKey(
        Lease,
        on_delete=models.CASCADE,
        related_name="documents",
    )

    document = models.FileField(
        upload_to="leases/",
    )

    document_type = models.CharField(
        max_length=100,
    )

    is_signed = models.BooleanField(
        default=False,
    )
```

---

# 17. Rent Invoice

প্রতি মাসে rent invoice।

```python
class RentInvoice(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("partial", "Partial"),
        ("overdue", "Overdue"),
        ("cancelled", "Cancelled"),
    ]

    lease = models.ForeignKey(
        Lease,
        on_delete=models.PROTECT,
        related_name="rent_invoices",
    )

    invoice_number = models.CharField(
        max_length=100,
        unique=True,
    )

    billing_month = models.DateField()

    due_date = models.DateField()

    rent_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    late_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["lease", "billing_month"],
                name="unique_lease_billing_month",
            ),
        ]

        indexes = [
            models.Index(
                fields=["lease", "status"]
            ),
            models.Index(
                fields=["due_date", "status"]
            ),
        ]
```

---

# 18. Rent Payment

```python
class RentPayment(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
    ]

    METHOD_CHOICES = [
        ("cash", "Cash"),
        ("card", "Card"),
        ("bank", "Bank"),
        ("mobile_banking", "Mobile Banking"),
    ]

    invoice = models.ForeignKey(
        RentInvoice,
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
                fields=["invoice", "status"]
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]
```

---

# 19. Maintenance Request

```python
class MaintenanceRequest(BaseModel):

    PRIORITY_CHOICES = [
        ("low", "Low"),
        ("medium", "Medium"),
        ("high", "High"),
        ("urgent", "Urgent"),
    ]

    STATUS_CHOICES = [
        ("open", "Open"),
        ("assigned", "Assigned"),
        ("in_progress", "In Progress"),
        ("completed", "Completed"),
        ("cancelled", "Cancelled"),
    ]

    unit = models.ForeignKey(
        Unit,
        on_delete=models.PROTECT,
        related_name="maintenance_requests",
    )

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.PROTECT,
        related_name="maintenance_requests",
    )

    title = models.CharField(
        max_length=200,
    )

    description = models.TextField()

    priority = models.CharField(
        max_length=20,
        choices=PRIORITY_CHOICES,
        default="medium",
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="open",
    )

    estimated_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    actual_cost = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    resolved_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["unit", "status"]
            ),
            models.Index(
                fields=["priority", "status"]
            ),
        ]
```

---

# 20. Maintenance Assignment

কে maintenance করবে:

```python
class MaintenanceAssignment(BaseModel):

    request = models.ForeignKey(
        MaintenanceRequest,
        on_delete=models.CASCADE,
        related_name="assignments",
    )

    staff = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="maintenance_assignments",
    )

    assigned_at = models.DateTimeField(
        auto_now_add=True,
    )

    completed_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    note = models.TextField(
        blank=True,
    )
```

---

# 21. Property Expense

Owner-এর expense tracking।

```python
class PropertyExpense(BaseModel):

    CATEGORY_CHOICES = [
        ("maintenance", "Maintenance"),
        ("utility", "Utility"),
        ("tax", "Tax"),
        ("insurance", "Insurance"),
        ("cleaning", "Cleaning"),
        ("other", "Other"),
    ]

    owner = models.ForeignKey(
        Owner,
        on_delete=models.PROTECT,
        related_name="expenses",
    )

    property = models.ForeignKey(
        Property,
        on_delete=models.PROTECT,
        related_name="expenses",
    )

    category = models.CharField(
        max_length=30,
        choices=CATEGORY_CHOICES,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    description = models.TextField(
        blank=True,
    )

    expense_date = models.DateField()

    class Meta:
        indexes = [
            models.Index(
                fields=["property", "-expense_date"]
            ),
            models.Index(
                fields=["owner", "-expense_date"]
            ),
        ]
```

---

# 22. Property Review

```python
class PropertyReview(BaseModel):

    property = models.ForeignKey(
        Property,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.CASCADE,
        related_name="property_reviews",
    )

    lease = models.ForeignKey(
        Lease,
        on_delete=models.PROTECT,
        related_name="reviews",
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
                name="property_rating_1_5",
            ),

            models.UniqueConstraint(
                fields=["tenant", "lease"],
                name="one_review_per_lease",
            ),
        ]

        indexes = [
            models.Index(
                fields=["property", "-created_at"]
            ),
        ]
```

---

# 23. Wishlist

```python
class Wishlist(BaseModel):

    tenant = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="property_wishlist",
    )
```

---

# 24. Wishlist Property

```python
class WishlistProperty(BaseModel):

    wishlist = models.ForeignKey(
        Wishlist,
        on_delete=models.CASCADE,
        related_name="items",
    )

    property = models.ForeignKey(
        Property,
        on_delete=models.CASCADE,
        related_name="wishlist_items",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["wishlist", "property"],
                name="unique_wishlist_property",
            )
        ]
```

---

# 25. Coupon

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
        default=0,
    )

    valid_from = models.DateTimeField()

    valid_until = models.DateTimeField()

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 26. Coupon Usage

```python
class CouponUsage(BaseModel):

    coupon = models.ForeignKey(
        Coupon,
        on_delete=models.PROTECT,
        related_name="usages",
    )

    tenant = models.ForeignKey(
        TenantProfile,
        on_delete=models.PROTECT,
        related_name="coupon_usages",
    )

    invoice = models.ForeignKey(
        RentInvoice,
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
                fields=["coupon", "tenant", "invoice"],
                name="unique_coupon_invoice_usage",
            )
        ]
```

---

# 27. Owner Commission

Marketplace হলে platform commission নেবে।

```python
class OwnerCommission(BaseModel):

    owner = models.ForeignKey(
        Owner,
        on_delete=models.PROTECT,
        related_name="commissions",
    )

    lease = models.ForeignKey(
        Lease,
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

    owner_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 28. Owner Payout

```python
class OwnerPayout(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("processing", "Processing"),
        ("paid", "Paid"),
        ("failed", "Failed"),
    ]

    owner = models.ForeignKey(
        Owner,
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

# 29. Notification

```python
class Notification(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="notifications",
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

# 30. Idempotency Record

Payment/application-এর duplicate request prevent করতে:

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
        related_name="rental_idempotency_records",
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

# 31. Audit Log

```python
class AuditLog(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="rental_audit_logs",
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

# 🔗 Complete Relationship

এখন পুরো system-টা একবার diagram দিয়ে দেখো:

```text
                         USER
                          │
             ┌────────────┴─────────────┐
             │                          │
           OWNER                      TENANT
             │                          │
      ┌──────┴────────┐         ┌───────┴─────────┐
      │               │         │                 │
  Membership      Properties   Profile          Wishlist
                      │
              ┌───────┼───────────┐
              │       │           │
            Units   Amenities    Images
              │
       ┌──────┼──────────┐
       │      │          │
    Leases  Applications Maintenance
       │                    │
       │                 Assignment
       │
       ├── RentInvoice
       │       │
       │       └── RentPayment
       │
       ├── Review
       │
       └── Commission
               │
               └── OwnerPayout
```

---

# 🔥 Core Business Flow

## Property Listing

```text
Owner
 ↓
Property
 ↓
Unit
 ↓
Property published
 ↓
Tenant searches
```

---

## Rental Flow

```text
Tenant
 ↓
RentalApplication
 ↓
Owner approves
 ↓
Lease
 ↓
Monthly RentInvoice
 ↓
RentPayment
```

---

## Maintenance Flow

```text
Tenant
 ↓
MaintenanceRequest
 ↓
Owner/Manager
 ↓
MaintenanceAssignment
 ↓
Work completed
 ↓
Actual Cost
```

---

## Financial Flow

```text
Tenant
 ↓
Rent Payment
 ↓
Rent Invoice
 ↓
Owner Revenue
 ↓
Platform Commission
 ↓
Owner Payout
```

---

# ⭐ Multi-Vendor Isolation

এখানে `Vendor`-এর পরিবর্তে আমরা `Owner`-কে tenant হিসেবে ব্যবহার করছি।

Owner A যেন Owner B-এর property দেখতে না পারে।

```python
Property.objects.filter(
    owner=request.user.owner_profile
)
```

Owner-এর Units:

```python
Unit.objects.filter(
    property__owner=request.user.owner_profile
)
```

Owner-এর Leases:

```python
Lease.objects.filter(
    unit__property__owner=request.user.owner_profile
)
```

Owner-এর Revenue:

```python
RentPayment.objects.filter(
    invoice__lease__unit__property__owner=owner,
    status="paid",
)
```

এটাই **tenant isolation**।

---

# 🔥 ORM Practice-এর জন্য সবচেয়ে গুরুত্বপূর্ণ Queries

এই project-এ এগুলো practice করবে:

```text
1. Owner → Properties
2. Owner → Units
3. Owner → Tenants
4. Owner → Active Leases
5. Property → Units
6. Property → Reviews
7. Property → Expenses
8. Unit → Leases
9. Unit → Maintenance
10. Tenant → Applications
11. Tenant → Leases
12. Tenant → Payments
13. Lease → Invoices
14. Invoice → Payments
15. Owner revenue
16. Property revenue
17. Monthly rent revenue
18. Outstanding rent
19. Overdue invoices
20. Maintenance cost
21. Property profit
22. Average rent
23. Average property rating
24. Most expensive units
25. Available units
26. Occupied units
27. Vacancy rate
28. Tenant spending
29. Repeat tenants
30. Latest lease
31. Latest payment
32. Exists()
33. Subquery()
34. OuterRef()
35. Q()
36. F()
37. Case()
38. When()
39. Count()
40. Sum()
41. Avg()
42. Min()
43. Max()
44. Window Functions
45. select_related()
46. prefetch_related()
47. Prefetch()
48. transaction.atomic()
49. select_for_update()
50. Database Constraints
51. EXPLAIN
```

---

# 🚨 Advanced Rental Availability

যদি **short-term rental / Airbnb-style** করতে চাও, তখন সবচেয়ে গুরুত্বপূর্ণ হবে date overlap।

```text
Existing Rental:

Sep 10 ───────── Sep 20

New Request:

       Sep 15 ───────── Sep 25

❌ Conflict
```

Query:

```python
Lease.objects.filter(
    unit=unit,
    start_date__lt=requested_end,
    end_date__gt=requested_start,
    status="active",
).exists()
```

আর PostgreSQL production version-এ:

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

ব্যবহার করতে পারবে।

---

# 🏆 Project App Structure

সব model এক file-এ রাখবে না।

```text
rental_platform/
│
├── accounts/
│
├── owners/
│
├── properties/
│
├── units/
│
├── tenants/
│
├── rentals/
│
├── billing/
│
├── payments/
│
├── maintenance/
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

---

# 🎯 এই Project দিয়ে তোমার কোন ORM Topics Practice হবে?

```text
Basic CRUD
      ↓
Relationships
      ↓
Reverse Relationships
      ↓
select_related
      ↓
prefetch_related
      ↓
Prefetch
      ↓
Q()
      ↓
F()
      ↓
Aggregation
      ↓
Annotation
      ↓
Case / When
      ↓
Subquery / OuterRef
      ↓
Exists
      ↓
Window Functions
      ↓
Constraints
      ↓
Transactions
      ↓
select_for_update
      ↓
Concurrency
      ↓
Idempotency
      ↓
Query Optimization
      ↓
EXPLAIN
      ↓
Multi-Tenant / Owner Isolation
```

**তোমার ORM practice-এর জন্য এই project-টা Hotel project-এর পরের excellent project হবে**, কারণ Hotel-এ তুমি booking-centric system দেখেছ, আর এখানে **property → unit → tenant → lease → monthly billing → maintenance → revenue** পুরো lifecycle practice করতে পারবে।


