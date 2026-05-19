implementing a **multi-vendor hotel management system** with **role-based users** and **customization features**. Let’s break this down step by step. I’ll outline the architecture, roles, features, and customization options.

---

## 1. **Overview of Multi-Vendor Hotel Management System**

A **multi-vendor hotel management system (HMS)** allows multiple hotels or properties (vendors) to register on a platform and manage their bookings, rooms, pricing, and services independently, while the platform admin oversees the entire ecosystem. Think of it like a “marketplace” for hotels.

Key aspects:

* Vendors manage their own hotels.
* Guests can book rooms across multiple vendors.
* Admin manages the platform, sets rules, and oversees operations.
* Role-based access ensures security and proper responsibilities.

---

## 2. **Role-Based Users**

### **Core Roles**

| Role                           | Description        | Key Permissions                                                          |
| ------------------------------ | ------------------ | ------------------------------------------------------------------------ |
| **Super Admin**                | Platform owner     | Full access: manage vendors, users, payments, analytics, system settings |
| **Vendor Admin / Hotel Owner** | Hotel management   | Manage rooms, bookings, pricing, staff, hotel info, reports              |
| **Vendor Staff / Manager**     | Hotel operations   | Handle bookings, check-ins, check-outs, customer requests                |
| **Front Desk / Receptionist**  | Daily operations   | Check-in/check-out, billing, guest queries                               |
| **Guest / Customer**           | Book rooms         | Search, book, pay, provide reviews                                       |
| **Finance / Accountant**       | Payment management | Access to invoices, payouts, commissions                                 |

> Optional roles: Marketing manager, Housekeeping manager, Customer support.

---

## 3. **Key Modules and Features**

### **Vendor Modules**

* Hotel profile management (images, facilities, descriptions)
* Room management (availability, room types, pricing)
* Booking management (view, confirm, cancel)
* Staff management (add/remove staff, assign roles)
* Reports & analytics (occupancy rate, revenue, cancellations)
* Promotions / discounts

### **Admin Modules**

* Vendor approval & management
* User management (vendors, staff, guests)
* Commission and payment settings
* Platform-wide analytics & reports
* System settings & notifications

### **Guest Modules**

* Search & filter hotels
* Booking & payment
* View booking history
* Ratings & reviews
* Notifications

---

## 4. **Role-Based Access Control (RBAC)**

Implement **RBAC** to restrict access based on roles:

* Use **permissions tables** like this:

| Resource         | Super Admin | Vendor Admin | Vendor Staff | Guest   |
| ---------------- | ----------- | ------------ | ------------ | ------- |
| Manage Hotels    | ✔           | ✔ (own)      | ✖            | ✖       |
| Manage Rooms     | ✔           | ✔ (own)      | ✔ (assigned) | ✖       |
| Manage Bookings  | ✔           | ✔ (own)      | ✔ (assigned) | ✔ (own) |
| View Reports     | ✔           | ✔ (own)      | ✖            | ✖       |
| Payment & Payout | ✔           | ✔ (own)      | ✖            | ✔ (own) |

* Assign **roles** and **permissions dynamically** in the database.

---

## 5. **Customization Options**

For a **multi-vendor system**, customization improves flexibility:

### **Vendor-Side Customization**

* Branding (logo, colors, fonts)
* Room types & pricing structure
* Policies (cancellation, check-in/out)
* Add-ons or services (spa, airport pickup)
* Payment options (gateway integration)

### **Platform-Wide Customization**

* Commission models (percentage, fixed fee)
* Multi-currency & multi-language support
* Dynamic notifications & email templates
* Reporting dashboards

### **User Interface Customization**

* Dashboards per role
* Widget-based reporting
* Notifications & alerts per role

---

## 6. **Technology Stack Suggestions**

* **Backend:** Node.js + Express, Django, or Laravel
* **Frontend:** React.js, Vue.js, or Angular
* **Database:** PostgreSQL or MySQL
* **Authentication & RBAC:** JWT, OAuth2
* **Cloud & Hosting:** AWS, Azure, or Google Cloud
* **Payment Integration:** Stripe, PayPal, Razorpay

---

Sure! Since you want a **full Django model structure** for a **multi-vendor hotel management system** with **role-based users** and **customization**, I’ll provide a detailed set of models, including vendors, rooms, bookings, users, roles, and permissions. This is a production-ready blueprint you can extend.

---

## **Django Models for Multi-Vendor Hotel Management System**

```python
from django.db import models
from django.contrib.auth.models import AbstractUser
from django.utils.translation import gettext_lazy as _

# ---------------------------
# 1. Custom User Model
# ---------------------------
class User(AbstractUser):
    class Role(models.TextChoices):
        SUPER_ADMIN = "super_admin", _("Super Admin")
        VENDOR_ADMIN = "vendor_admin", _("Vendor Admin")
        VENDOR_STAFF = "vendor_staff", _("Vendor Staff")
        GUEST = "guest", _("Guest")

    role = models.CharField(max_length=20, choices=Role.choices)
    phone = models.CharField(max_length=20, blank=True, null=True)

    def __str__(self):
        return f"{self.username} ({self.role})"

# ---------------------------
# 2. Vendor / Hotel Model
# ---------------------------
class Vendor(models.Model):
    owner = models.ForeignKey(User, on_delete=models.CASCADE, limit_choices_to={'role': 'vendor_admin'})
    name = models.CharField(max_length=255)
    description = models.TextField(blank=True)
    address = models.CharField(max_length=500)
    city = models.CharField(max_length=100)
    country = models.CharField(max_length=100)
    phone = models.CharField(max_length=20, blank=True)
    email = models.EmailField()
    logo = models.ImageField(upload_to='vendor_logos/', blank=True, null=True)
    is_approved = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name

# ---------------------------
# 3. Hotel Rooms
# ---------------------------
class RoomType(models.Model):
    vendor = models.ForeignKey(Vendor, on_delete=models.CASCADE, related_name='room_types')
    name = models.CharField(max_length=100)
    description = models.TextField(blank=True)
    capacity = models.PositiveIntegerField(default=1)
    price_per_night = models.DecimalField(max_digits=10, decimal_places=2)
    total_rooms = models.PositiveIntegerField(default=1)
    amenities = models.TextField(blank=True)  # JSON or comma-separated list
    image = models.ImageField(upload_to='room_images/', blank=True, null=True)

    def __str__(self):
        return f"{self.name} - {self.vendor.name}"

# ---------------------------
# 4. Booking Model
# ---------------------------
class Booking(models.Model):
    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("confirmed", "Confirmed"),
        ("cancelled", "Cancelled"),
        ("completed", "Completed"),
    ]

    guest = models.ForeignKey(User, on_delete=models.CASCADE, limit_choices_to={'role': 'guest'})
    room = models.ForeignKey(RoomType, on_delete=models.CASCADE)
    check_in = models.DateField()
    check_out = models.DateField()
    guests_count = models.PositiveIntegerField(default=1)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default="pending")
    total_price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Booking {self.id} - {self.room.name} ({self.status})"

# ---------------------------
# 5. Vendor Staff
# ---------------------------
class VendorStaff(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, limit_choices_to={'role': 'vendor_staff'})
    vendor = models.ForeignKey(Vendor, on_delete=models.CASCADE, related_name='staff')
    designation = models.CharField(max_length=100, blank=True)
    phone = models.CharField(max_length=20, blank=True, null=True)

    def __str__(self):
        return f"{self.user.username} - {self.vendor.name}"

# ---------------------------
# 6. Payments / Transactions
# ---------------------------
import uuid

class Payment(models.Model):
    booking = models.OneToOneField(Booking, on_delete=models.CASCADE)
    amount = models.DecimalField(max_digits=10, decimal_places=2)
    payment_method = models.CharField(max_length=50, blank=True)
    payment_status = models.CharField(
        max_length=20,
        choices=[("pending","Pending"),("paid","Paid"),("failed","Failed")],
        default="pending"
    )
    transaction_id = models.UUIDField(default=uuid.uuid4, editable=False, unique=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Payment {self.id} - {self.booking.id} ({self.payment_status})"

# ---------------------------
# 7. Vendor Customization
# ---------------------------
class VendorCustomization(models.Model):
    vendor = models.OneToOneField(Vendor, on_delete=models.CASCADE, related_name='customization')
    primary_color = models.CharField(max_length=7, default="#000000")  # HEX
    secondary_color = models.CharField(max_length=7, default="#FFFFFF")
    logo = models.ImageField(upload_to='vendor_custom_logos/', blank=True, null=True)
    custom_css = models.TextField(blank=True, null=True)

    def __str__(self):
        return f"Customization - {self.vendor.name}"

# ---------------------------
# 8. Reviews & Ratings
# ---------------------------
class Review(models.Model):
    booking = models.OneToOneField(Booking, on_delete=models.CASCADE)
    rating = models.PositiveIntegerField(default=5)
    comment = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Review {self.id} - Booking {self.booking.id}"

```

---

### ✅ **Highlights**

1. **Role-Based Users**

   * `User.role` defines access (super admin, vendor, staff, guest).
2. **Multi-Vendor**

   * Each `Vendor` is independent, with `RoomType`, `VendorStaff`, and `VendorCustomization`.
3. **Bookings & Payments**

   * `Booking` links guest → room → vendor.
   * `Payment` handles transactions.
4. **Customization**

   * Vendors can set colors, logos, and CSS.
5. **Reviews**

   * One review per booking.

---

If you want, I can **also create the full Django admin setup** with **role-based dashboards and permissions**, so each type of user sees only what they are allowed to manage. This is critical for multi-vendor systems.

Do you want me to create that admin setup next?
Got it! You want to extend your custom `User` model to use **email-based login** instead of username, and also add **more fields**. Let me show you a clean, **production-ready Django `AbstractUser` replacement** for this.

---

## 1️⃣ **Custom User Model with Email Login & Extra Fields**

```python id="v8c6mj"
from django.contrib.auth.models import AbstractBaseUser, PermissionsMixin, BaseUserManager
from django.db import models
from django.utils import timezone
from django.utils.translation import gettext_lazy as _

# ---------------------------
# 1. User Manager
# ---------------------------
class CustomUserManager(BaseUserManager):
    """
    Custom manager for User with email login
    """
    def create_user(self, email, password=None, **extra_fields):
        if not email:
            raise ValueError('Email must be set')
        email = self.normalize_email(email)
        user = self.model(email=email, **extra_fields)
        user.set_password(password)
        user.save(using=self._db)
        return user

    def create_superuser(self, email, password=None, **extra_fields):
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)
        extra_fields.setdefault('role', User.Role.SUPER_ADMIN)
        if extra_fields.get('is_staff') is not True:
            raise ValueError('Superuser must have is_staff=True')
        if extra_fields.get('is_superuser') is not True:
            raise ValueError('Superuser must have is_superuser=True')
        return self.create_user(email, password, **extra_fields)

# ---------------------------
# 2. Custom User Model
# ---------------------------
class User(AbstractBaseUser, PermissionsMixin):
    class Role(models.TextChoices):
        SUPER_ADMIN = "super_admin", _("Super Admin")
        VENDOR_ADMIN = "vendor_admin", _("Vendor Admin")
        VENDOR_STAFF = "vendor_staff", _("Vendor Staff")
        GUEST = "guest", _("Guest")

    # Required fields
    email = models.EmailField(unique=True)
    role = models.CharField(max_length=20, choices=Role.choices, default=Role.GUEST)
    phone = models.CharField(max_length=20, blank=True, null=True)
    full_name = models.CharField(max_length=255, blank=True)
    is_active = models.BooleanField(default=True)
    is_staff = models.BooleanField(default=False)
    date_joined = models.DateTimeField(default=timezone.now)

    # Set email as username field
    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['role']  # fields required when creating superuser

    objects = CustomUserManager()

    def __str__(self):
        return f"{self.email} ({self.role})"
```

---

## 2️⃣ **Key Changes & Features**

1. **Email login**

   * `USERNAME_FIELD = 'email'` replaces username login.
   * `email` is unique and required.
2. **Custom fields**

   * `phone`
   * `full_name`
   * `role` (from your `TextChoices`)
   * `is_active`, `is_staff`, `date_joined`
3. **Custom User Manager**

   * Handles `create_user` and `create_superuser` with role assignment.
4. **Permissions**

   * Works with Django’s built-in permissions system (`PermissionsMixin`).

---

## 3️⃣ **Settings Update**

In `settings.py`:

```python id="2dfzsh"
AUTH_USER_MODEL = 'myapp.User'  # Replace 'myapp' with your app name
```

---

## 4️⃣ **Create Superuser**

```bash
python manage.py createsuperuser
```

* It will ask for **email**, **password**, and **role** (defaulted to SUPER_ADMIN).

---

✅ Now your `User` model supports:

* Email login
* Role-based access
* Extra fields like `phone` and `full_name`

---

If you want, I can also **extend this model with profile images, addresses, and vendor link** for a fully ready **multi-vendor hotel system user model**.

Do you want me to do that next?
Perfect! In a **multi-vendor hotel system**, it’s a good practice to create a **separate profile model** for every user. This keeps the user authentication model clean while allowing you to store additional details (like address, profile photo, vendor info, etc.).

Here’s a **clean Django setup** for that:

---

## 1️⃣ **Profile Model Linked to User**

```python id="s8n0hf"
from django.db import models
from django.conf import settings
from django.utils.translation import gettext_lazy as _

class UserProfile(models.Model):
    class Gender(models.TextChoices):
        MALE = "male", _("Male")
        FEMALE = "female", _("Female")
        OTHER = "other", _("Other")

    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='profile')
    full_name = models.CharField(max_length=255, blank=True)
    phone = models.CharField(max_length=20, blank=True)
    profile_image = models.ImageField(upload_to='profile_images/', blank=True, null=True)
    gender = models.CharField(max_length=10, choices=Gender.choices, blank=True)
    address = models.TextField(blank=True)
    city = models.CharField(max_length=100, blank=True)
    country = models.CharField(max_length=100, blank=True)
    zip_code = models.CharField(max_length=20, blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return f"{self.user.email} Profile"
```

---

## 2️⃣ **Automatically Create Profile on User Creation**

Use Django signals so every time a user is created, a profile is also created:

```python id="5yz6sf"
from django.db.models.signals import post_save
from django.dispatch import receiver
from .models import User, UserProfile

@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        UserProfile.objects.create(user=instance)

@receiver(post_save, sender=User)
def save_user_profile(sender, instance, **kwargs):
    instance.profile.save()
```

* This ensures **every user**, no matter the role, has a profile.
* You can safely add extra fields to the profile later without touching the `User` model.

---

## 3️⃣ **Accessing Profile Data**

```python id="7az3wh"
user = User.objects.get(email="john@example.com")

# Access profile info
print(user.profile.full_name)
print(user.profile.address)
```

* `user.profile` works automatically because of the `related_name='profile'`.

---

## 4️⃣ **Optional: Role-Based Profile Extension**

If you want, you can **extend profiles per role**:

```python id="8ds4gh"
class VendorProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    vendor_name = models.CharField(max_length=255)
    tax_id = models.CharField(max_length=100, blank=True)
    logo = models.ImageField(upload_to='vendor_logos/', blank=True, null=True)
```

* Only for `VENDOR_ADMIN` users.
* You can also add `VendorStaffProfile` if needed.

---

✅ **Advantages of this approach**

1. Keeps authentication and user info separate.
2. Profiles can store **role-specific fields**.
3. Easy to extend later without breaking login system.
4. Works with your **email-based login and TextChoices roles**.

---

I can also make a **complete multi-vendor profile structure**:

* `UserProfile` for all users
* `VendorProfile` for vendor admins
* `VendorStaffProfile` for staff
* Automatic creation via signals

This will give a **full multi-role profile system** for your hotel platform.

Do you want me to build that full structure?
Perfect! Let’s design a **complete multi-vendor profile structure** for your hotel management system. This will handle **all roles** and automatically create the right profile when a user is created.

---

## 1️⃣ **Base UserProfile for All Users**

```python
from django.db import models
from django.conf import settings
from django.utils.translation import gettext_lazy as _

class UserProfile(models.Model):
    class Gender(models.TextChoices):
        MALE = "male", _("Male")
        FEMALE = "female", _("Female")
        OTHER = "other", _("Other")

    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='profile')
    full_name = models.CharField(max_length=255, blank=True)
    phone = models.CharField(max_length=20, blank=True)
    profile_image = models.ImageField(upload_to='profile_images/', blank=True, null=True)
    gender = models.CharField(max_length=10, choices=Gender.choices, blank=True)
    address = models.TextField(blank=True)
    city = models.CharField(max_length=100, blank=True)
    country = models.CharField(max_length=100, blank=True)
    zip_code = models.CharField(max_length=20, blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return f"{self.user.email} Profile"
```

* **All users** get this profile.
* Stores generic info like name, contact, and address.

---

## 2️⃣ **VendorProfile for Vendor Admins**

```python
class VendorProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='vendor_profile')
    vendor_name = models.CharField(max_length=255)
    tax_id = models.CharField(max_length=100, blank=True)
    logo = models.ImageField(upload_to='vendor_logos/', blank=True, null=True)
    website = models.URLField(blank=True)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Vendor {self.vendor_name} ({self.user.email})"
```

* Only assigned to users with `role = VENDOR_ADMIN`.
* Stores **hotel/vendor-specific information**.

---

## 3️⃣ **VendorStaffProfile for Vendor Staff**

```python
class VendorStaffProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='staff_profile')
    vendor = models.ForeignKey('VendorProfile', on_delete=models.CASCADE, related_name='staff_members')
    designation = models.CharField(max_length=100, blank=True)
    phone = models.CharField(max_length=20, blank=True)

    def __str__(self):
        return f"{self.user.email} - {self.designation}"
```

* Assigned to `VENDOR_STAFF` users.
* Linked to a specific vendor via `vendor`.

---

## 4️⃣ **Automatic Profile Creation via Signals**

```python
from django.db.models.signals import post_save
from django.dispatch import receiver
from .models import User, UserProfile, VendorProfile, VendorStaffProfile

@receiver(post_save, sender=User)
def create_user_profiles(sender, instance, created, **kwargs):
    if created:
        # Always create base profile
        UserProfile.objects.create(user=instance)

        # Role-specific profiles
        if instance.role == User.Role.VENDOR_ADMIN:
            VendorProfile.objects.create(user=instance, vendor_name=f"{instance.email}'s Hotel")
        elif instance.role == User.Role.VENDOR_STAFF:
            # Staff profile will need a vendor assigned later
            VendorStaffProfile.objects.create(user=instance)

@receiver(post_save, sender=User)
def save_user_profiles(sender, instance, **kwargs):
    if hasattr(instance, 'profile'):
        instance.profile.save()
    if hasattr(instance, 'vendor_profile'):
        instance.vendor_profile.save()
    if hasattr(instance, 'staff_profile'):
        instance.staff_profile.save()
```

✅ Features:

1. Every user gets a **base `UserProfile`**.
2. Vendor admins get a **`VendorProfile`** automatically.
3. Vendor staff get a **`VendorStaffProfile`** (linked later to a vendor).
4. Works for **all roles**, cleanly separated.

---

## 5️⃣ **Accessing Profiles**

```python
user = User.objects.get(email="vendor@example.com")

# Base profile
print(user.profile.full_name)

# Vendor-specific info
if user.role == User.Role.VENDOR_ADMIN:
    print(user.vendor_profile.vendor_name)

# Staff-specific info
if user.role == User.Role.VENDOR_STAFF:
    print(user.staff_profile.vendor.vendor_name)
```

---

✅ **Advantages of this Structure**

* Clean separation of **generic vs role-specific data**.
* Scalable for future roles (e.g., guests with loyalty points, finance users).
* Easy integration with your **multi-vendor hotel system**.

---

If you want, I can **extend this further** to include:

* **GuestProfile** with booking history and loyalty points.
* **Admin dashboards** showing role-based data automatically.

Do you want me to create that next?
Perfect! Let’s extend your **multi-vendor profile system** to include **GuestProfile** with booking history and loyalty points, and set up **role-based admin dashboards** so each user sees only what they are allowed to manage.

---

## 1️⃣ **GuestProfile with Booking History & Loyalty Points**

```python id="g1v3h8"
class GuestProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='guest_profile')
    loyalty_points = models.PositiveIntegerField(default=0)
    favorite_hotels = models.ManyToManyField('VendorProfile', blank=True, related_name='favored_by')
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Guest {self.user.email} (Points: {self.loyalty_points})"

    def total_bookings(self):
        # Returns all bookings for this guest
        return self.user.bookings.count()
    
    def add_loyalty_points(self, points):
        self.loyalty_points += points
        self.save()
```

* Linked to `User` with role `GUEST`.
* Stores **loyalty points**, **favorite hotels**, and easily tracks bookings.

---

### 2️⃣ **Update Booking Model to Link GuestProfile**

```python id="h7y2db"
class Booking(models.Model):
    guest = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='bookings')
    room = models.ForeignKey('RoomType', on_delete=models.CASCADE)
    check_in = models.DateField()
    check_out = models.DateField()
    guests_count = models.PositiveIntegerField(default=1)
    status = models.CharField(
        max_length=20,
        choices=[("pending","Pending"),("confirmed","Confirmed"),("cancelled","Cancelled"),("completed","Completed")],
        default="pending"
    )
    total_price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Booking {self.id} - {self.room.name} ({self.status})"
```

* The `guest` foreign key allows us to query **all bookings per guest**.

```python id="j2x5kf"
# Example: Get all bookings for a guest
guest = User.objects.get(email="john@example.com")
bookings = guest.bookings.all()  # all Booking objects
```

---

## 3️⃣ **Update Signals for Automatic GuestProfile Creation**

```python id="k4b1mc"
@receiver(post_save, sender=User)
def create_user_profiles(sender, instance, created, **kwargs):
    if created:
        # Base profile
        UserProfile.objects.create(user=instance)

        if instance.role == User.Role.VENDOR_ADMIN:
            VendorProfile.objects.create(user=instance, vendor_name=f"{instance.email}'s Hotel")
        elif instance.role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.create(user=instance)
        elif instance.role == User.Role.GUEST:
            GuestProfile.objects.create(user=instance)
```

---

## 4️⃣ **Role-Based Admin Dashboards**

Django Admin can be customized to **show only data relevant to the user role**:

```python id="l8y7df"
from django.contrib import admin
from .models import User, UserProfile, VendorProfile, VendorStaffProfile, GuestProfile, Booking

# Base Admin: Super Admin sees everything
@admin.register(User)
class UserAdmin(admin.ModelAdmin):
    list_display = ('email', 'role', 'is_active')
    list_filter = ('role',)
    search_fields = ('email',)

# Vendor Admin: Can see only their hotel rooms & bookings
class BookingInline(admin.TabularInline):
    model = Booking
    extra = 0
    readonly_fields = ('total_price', 'status')

@admin.register(VendorProfile)
class VendorProfileAdmin(admin.ModelAdmin):
    list_display = ('vendor_name', 'user')
    inlines = [BookingInline]

    def get_queryset(self, request):
        qs = super().get_queryset(request)
        # Vendor Admin sees only their own vendor
        if request.user.role == User.Role.VENDOR_ADMIN:
            return qs.filter(user=request.user)
        return qs

# Guest Admin: See guest details & booking history
@admin.register(GuestProfile)
class GuestProfileAdmin(admin.ModelAdmin):
    list_display = ('user', 'loyalty_points', 'total_bookings')
    search_fields = ('user__email',)

    def total_bookings(self, obj):
        return obj.total_bookings()
```

✅ **How this works:**

1. **Super Admin** sees all users, bookings, vendors.
2. **Vendor Admin** sees only their hotel, rooms, and related bookings.
3. **Vendor Staff** can be restricted via `BookingInline` and permissions.
4. **Guest** data is available only to admins, but the guest can view their own bookings via the app.

---

## 5️⃣ **Example Queries by Role**

```python id="m3c2kx"
# Vendor Admin: get all bookings for their hotel
vendor = request.user.vendor_profile
bookings = Booking.objects.filter(room__vendor=vendor)

# Guest: get own bookings
guest_bookings = request.user.bookings.all()

# Super Admin: all bookings
all_bookings = Booking.objects.all()
```

---

### ✅ **Benefits of this Extended Structure**

1. **Clean separation of profiles by role**
2. **Automatic creation of profiles** via signals
3. **GuestProfile with loyalty points & booking tracking**
4. **Admin dashboards** that respect roles and data boundaries
5. Fully scalable for multi-vendor hotel systems

---

I can also **draw a full diagram** showing **User → Profile → Vendor/Staff/Guest → Booking/Hotel relationships** for easier visualization and database planning.

Do you want me to create that diagram?
Absolutely! Here’s a **full entity-relationship diagram (ERD)** for your **multi-vendor hotel system** showing how `User` connects to `Profile`, `Vendor`, `Staff`, `Guest`, `Booking`, and `Hotel/Room`. I’ll describe it clearly and provide a visual layout.

---

## **Entity-Relationship Overview**

```
               ┌──────────┐
               │  User    │
               │──────────│
               │ id       │
               │ email    │
               │ role     │
               │ password │
               └──────────┘
                     │
          ┌──────────┴───────────┐
          │                      │
   ┌─────────────┐       ┌────────────────┐
   │ UserProfile │       │ GuestProfile   │
   │─────────────│       │────────────────│
   │ full_name   │       │ loyalty_points │
   │ phone       │       │ favorite_hotels│
   │ address     │       └────────────────┘
   │ city        │
   │ country     │
   └─────────────┘
          │
          │
  ┌───────┴─────────┐
  │Role-Specific     │
  │Profiles          │
  ├─────────────────┤
  │ VendorProfile    │
  │ - vendor_name    │
  │ - tax_id         │
  │ - logo           │
  │ - website        │
  └─────────────────┘
          │
          │
    ┌─────┴─────┐
    │ VendorStaff│
    │ Profile    │
    │ - designation │
    │ - vendor FK   │
    └──────────────┘
          │
          │
   ┌──────┴───────┐
   │   Booking    │
   │──────────────│
   │ guest FK     │
   │ room FK      │
   │ check_in     │
   │ check_out    │
   │ status       │
   └──────────────┘
          │
          │
   ┌──────┴───────┐
   │   RoomType   │
   │──────────────│
   │ vendor FK    │
   │ name         │
   │ price        │
   │ capacity     │
   └──────────────┘
          │
          │
   ┌──────┴───────┐
   │   Vendor     │
   │──────────────│
   │ name         │
   │ address      │
   │ city         │
   │ phone/email  │
   └──────────────┘
```

---

### **Legend / Relationships**

1. **User → UserProfile**

   * Every user has **one base profile** (`1-to-1`).

2. **User → VendorProfile / GuestProfile / VendorStaffProfile**

   * Role-specific profiles; `1-to-1` with user.

3. **VendorProfile → VendorStaffProfile**

   * Each staff member is linked to a vendor (`FK`).

4. **Booking → User (Guest)**

   * Each booking belongs to a guest (`FK`).

5. **Booking → RoomType**

   * Each booking is linked to a room (`FK`).

6. **RoomType → Vendor**

   * Each room belongs to a vendor/hotel.

7. **GuestProfile → favorite_hotels**

   * Many-to-many relationship with `VendorProfile` for favorites.

---

### **How It Works in Practice**

* **Super Admin** → sees all Users, Vendors, Bookings.
* **Vendor Admin** → has VendorProfile, sees only their own rooms, bookings, staff.
* **Vendor Staff** → linked to Vendor, sees bookings only for their vendor.
* **Guest** → sees own GuestProfile and bookings, loyalty points, favorite hotels.

---

If you want, I can also **draw this as a proper diagram image** with **boxes and arrows** like a UML/ERD diagram, so you can include it in documentation or developer planning.

Do you want me to make that image version?



# upgrade

# 🚀 🔥 UPGRADED VERSION (Clean + Scalable)

## ✅ 1. User Model (Minor Improvement)

```python
class User(AbstractUser):
    class Role(models.TextChoices):
        SUPER_ADMIN = "super_admin", _("Super Admin")
        VENDOR_ADMIN = "vendor_admin", _("Vendor Admin")
        VENDOR_STAFF = "vendor_staff", _("Vendor Staff")
        GUEST = "guest", _("Guest")

    role = models.CharField(max_length=20, choices=Role.choices)
    phone = models.CharField(max_length=20, blank=True, null=True)

    def is_vendor(self):
        return self.role in ["vendor_admin", "vendor_staff"]

    def __str__(self):
        return f"{self.username} ({self.role})"
```

---

# ✅ 2. Vendor Model (Add Slug + Better Control)

```python
from django.utils.text import slugify

class Vendor(models.Model):
    owner = models.ForeignKey(User, on_delete=models.CASCADE, limit_choices_to={'role': 'vendor_admin'})
    name = models.CharField(max_length=255)
    slug = models.SlugField(unique=True, blank=True)
    description = models.TextField(blank=True)

    address = models.CharField(max_length=500)
    city = models.CharField(max_length=100)
    country = models.CharField(max_length=100)

    phone = models.CharField(max_length=20, blank=True)
    email = models.EmailField()

    logo = models.ImageField(upload_to='vendor_logos/', blank=True, null=True)

    is_approved = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(self.name)
        super().save(*args, **kwargs)

    def __str__(self):
        return self.name
```

---

# ✅ 3. Amenities (Normalized)

```python
class Amenity(models.Model):
    name = models.CharField(max_length=100)

    def __str__(self):
        return self.name
```

---

# ✅ 4. RoomType (Improved)

```python
class RoomType(models.Model):
    vendor = models.ForeignKey(Vendor, on_delete=models.CASCADE, related_name='room_types')
    name = models.CharField(max_length=100)
    description = models.TextField(blank=True)

    capacity = models.PositiveIntegerField(default=1)
    price_per_night = models.DecimalField(max_digits=10, decimal_places=2)
    total_rooms = models.PositiveIntegerField(default=1)

    amenities = models.ManyToManyField(Amenity, blank=True)

    def __str__(self):
        return f"{self.name} - {self.vendor.name}"
```

---

# ✅ 5. Room Image Gallery (NEW)

```python
class RoomImage(models.Model):
    room = models.ForeignKey(RoomType, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to='room_gallery/')
```

---

# ✅ 6. Room Inventory (🔥 CRITICAL FIX)

```python
class RoomInventory(models.Model):
    room = models.ForeignKey(RoomType, on_delete=models.CASCADE)
    date = models.DateField()
    available_rooms = models.PositiveIntegerField()

    class Meta:
        unique_together = ('room', 'date')
```

---

# ✅ 7. Booking Model (Auto Price + Validation)

```python
class Booking(models.Model):
    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("confirmed", "Confirmed"),
        ("cancelled", "Cancelled"),
        ("completed", "Completed"),
    ]

    guest = models.ForeignKey(User, on_delete=models.CASCADE, limit_choices_to={'role': 'guest'})
    room = models.ForeignKey(RoomType, on_delete=models.CASCADE)

    check_in = models.DateField()
    check_out = models.DateField()

    guests_count = models.PositiveIntegerField(default=1)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default="pending")

    total_price = models.DecimalField(max_digits=10, decimal_places=2, blank=True)

    created_at = models.DateTimeField(auto_now_add=True)

    def save(self, *args, **kwargs):
        if self.check_out <= self.check_in:
            raise ValueError("Check-out must be after check-in")

        nights = (self.check_out - self.check_in).days
        self.total_price = nights * self.room.price_per_night

        super().save(*args, **kwargs)

    def __str__(self):
        return f"Booking {self.id} - {self.room.name}"
```

---

# ✅ 8. Payment Model (Production Ready)

```python
import uuid

class Payment(models.Model):
    booking = models.OneToOneField(Booking, on_delete=models.CASCADE)

    amount = models.DecimalField(max_digits=10, decimal_places=2)

    payment_method = models.CharField(max_length=50, blank=True)
    payment_status = models.CharField(
        max_length=20,
        choices=[("pending","Pending"),("paid","Paid"),("failed","Failed")],
        default="pending"
    )

    transaction_id = models.UUIDField(default=uuid.uuid4, editable=False, unique=True)

    gateway_name = models.CharField(max_length=50, blank=True)
    gateway_transaction_id = models.CharField(max_length=150, blank=True)

    paid_at = models.DateTimeField(null=True, blank=True)

    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Payment {self.id} - {self.payment_status}"
```

---

# ✅ 9. Review উন্নতি

```python
class Review(models.Model):
    booking = models.OneToOneField(Booking, on_delete=models.CASCADE)
    rating = models.PositiveIntegerField(default=5)
    comment = models.TextField(blank=True)

    created_at = models.DateTimeField(auto_now_add=True)

    def clean(self):
        if self.booking.status != "completed":
            raise ValueError("Cannot review incomplete booking")
```

---

# 🎯 Final Upgrade Summary

## 🔥 তুমি এখন পাচ্ছো:

✔ Overbooking prevention  
✔ Clean database design  
✔ Scalable amenities system  
✔ Multiple images support  
✔ Secure payment tracking  
✔ Auto price calculation  
✔ Booking validation  
✔ SaaS-ready structure

---

# 💡 Next Step (Very Important)

এখন তোমার focus হওয়া উচিত:

1. Booking API logic
    
2. Availability check algorithm
    
3. Payment gateway integration (SSLCommerz / Stripe)
    
4. Role-based permissions (DRF)
    

---

👉 চাইলে আমি next step এ তোমাকে  
**“complete booking system with API + availability logic”**  
real project style এ build করে দেখাতে পারি 🚀


ঠিক আছে — আমি তোমার `User` model টাকে **clean + production-ready update** করে দিচ্ছি, সাথে সব **profile models structuredভাবে** দিচ্ছি 👇

---

# 🚀 ✅ Updated User Model (Best Practice)

```python id="userfinal"
from django.contrib.auth.models import AbstractUser
from django.db import models
from django.utils.translation import gettext_lazy as _


class User(AbstractUser):

    class Role(models.TextChoices):
        SUPER_ADMIN = "super_admin", _("Super Admin")
        VENDOR_ADMIN = "vendor_admin", _("Vendor Admin")
        VENDOR_STAFF = "vendor_staff", _("Vendor Staff")
        GUEST = "guest", _("Guest")

    role = models.CharField(
        max_length=20,
        choices=Role.choices,
        default=Role.GUEST
    )

    phone = models.CharField(max_length=20, blank=True, null=True)

    is_verified = models.BooleanField(default=False)

    def is_vendor(self):
        return self.role in [self.Role.VENDOR_ADMIN, self.Role.VENDOR_STAFF]

    def is_admin(self):
        return self.role == self.Role.SUPER_ADMIN

    def __str__(self):
        return f"{self.username} ({self.role})"
```

---

# 🧱 ✅ Profile Models (Clean Architecture)

## 👤 1. Guest Profile

```python id="guestfinal"
class GuestProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="guest_profile")

    address = models.TextField(blank=True)
    date_of_birth = models.DateField(null=True, blank=True)

    def __str__(self):
        return f"Guest: {self.user.username}"
```

---

## 🏨 2. Vendor Admin Profile

```python id="vendoradminfinal"
class VendorAdminProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="vendor_admin_profile")

    company_name = models.CharField(max_length=255)
    nid_number = models.CharField(max_length=50, blank=True)
    trade_license = models.CharField(max_length=100, blank=True)

    def __str__(self):
        return f"Vendor Admin: {self.user.username}"
```

---

## 👨‍💼 3. Vendor Staff Profile

```python id="vendorstafffinal"
class VendorStaffProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="vendor_staff_profile")

    vendor = models.ForeignKey("Vendor", on_delete=models.CASCADE, related_name="staff_profiles")

    designation = models.CharField(max_length=100)
    joined_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Staff: {self.user.username} ({self.vendor.name})"
```

---

# 🔥 ✅ Default Profile Creation (Signal)

👉 সব user প্রথমে guest:

```python id="signalfinal"
from django.db.models.signals import post_save
from django.dispatch import receiver


@receiver(post_save, sender=User)
def create_default_guest_profile(sender, instance, created, **kwargs):
    if created and instance.role == User.Role.GUEST:
        GuestProfile.objects.create(user=instance)
```

---

# 🔁 ✅ Role Change Service (IMPORTANT)

```python id="rolefinal"
def change_user_role(user, new_role, vendor=None):

    # delete old profiles
    if hasattr(user, "guest_profile"):
        user.guest_profile.delete()

    if hasattr(user, "vendor_admin_profile"):
        user.vendor_admin_profile.delete()

    if hasattr(user, "vendor_staff_profile"):
        user.vendor_staff_profile.delete()

    # update role
    user.role = new_role
    user.save()

    # create new profile
    if new_role == User.Role.VENDOR_ADMIN:
        VendorAdminProfile.objects.create(user=user)

    elif new_role == User.Role.VENDOR_STAFF:
        VendorStaffProfile.objects.create(user=user, vendor=vendor)

    elif new_role == User.Role.GUEST:
        GuestProfile.objects.create(user=user)
```

---

# 🎯 Final Structure Overview

## 🧠 Clean Design:

* `User` → auth + role
* `GuestProfile` → booking মানুষ
* `VendorAdminProfile` → business owner
* `VendorStaffProfile` → employee

---

# 🔥 Why This is Production Ready

✔ Role-based separation
✔ No duplicate profile
✔ Scalable (SaaS ready)
✔ নিরাপদ (user role controlled)
✔ Clean DRF integration

---

# 🚀 Next Step (Recommended)

চাও হলে আমি next এ দেখাতে পারি:

* 🔐 DRF Role-based permission system
* 🔑 JWT login + role response
* 🧩 Vendor dashboard API structure

বললেই next level 🚀


Nice 👍 তাহলে আমরা next step এ যাই — **real-world booking flow + availability logic** 🔥
আমি এমনভাবে বুঝাবো যাতে তুমি direct project এ apply করতে পারো।

---

# 🚀 Step 1: Booking Flow (End-to-End)

একটা booking system সাধারণত এই flow follow করে:

### 🧭 Flow:

1. User date select করে (check-in / check-out)
2. System availability check করে
3. Room reserve করে
4. Booking create হয় (pending)
5. Payment করে
6. Payment success → booking confirmed

---

# 🔥 Step 2: Availability Check Logic (CORE PART)

## ✅ Function: Check room availability

```python id="xk9v2s"
from datetime import timedelta

def is_room_available(room, check_in, check_out):
    current_date = check_in

    while current_date < check_out:
        inventory = RoomInventory.objects.filter(
            room=room,
            date=current_date
        ).first()

        if not inventory or inventory.available_rooms <= 0:
            return False

        current_date += timedelta(days=1)

    return True
```

---

## ✅ Reserve Room (Important)

Booking করার সময় inventory কমাতে হবে:

```python id="5r3i6g"
def reserve_room(room, check_in, check_out):
    from datetime import timedelta

    current_date = check_in

    while current_date < check_out:
        inventory = RoomInventory.objects.get(room=room, date=current_date)

        if inventory.available_rooms <= 0:
            raise ValueError("Room not available")

        inventory.available_rooms -= 1
        inventory.save()

        current_date += timedelta(days=1)
```

---

# ⚠️ VERY IMPORTANT (Concurrency Issue)

Real-world এ multiple user একসাথে booking করলে problem হবে 😬

👉 later তুমি use করবে:

```python
select_for_update()
```

(DB locking)

---

# 🚀 Step 3: Booking Create Service

```python id="2v9p0j"
def create_booking(user, room, check_in, check_out, guests):
    
    if not is_room_available(room, check_in, check_out):
        raise ValueError("Room not available for selected dates")

    booking = Booking.objects.create(
        guest=user,
        room=room,
        check_in=check_in,
        check_out=check_out,
        guests_count=guests,
        status="pending"
    )

    reserve_room(room, check_in, check_out)

    return booking
```

---

# 🚀 Step 4: Payment Flow

## ✅ যখন payment শুরু:

```python id="zjdf3x"
payment = Payment.objects.create(
    booking=booking,
    amount=booking.total_price,
    payment_status="pending"
)
```

---

## ✅ Payment Success হলে:

```python id="g1kzcl"
def handle_payment_success(payment, gateway_id):
    payment.payment_status = "paid"
    payment.gateway_transaction_id = gateway_id
    payment.paid_at = timezone.now()
    payment.save()

    booking = payment.booking
    booking.status = "confirmed"
    booking.save()
```

---

## ❌ Payment Failed হলে:

```python id="2y4l1v"
def handle_payment_failed(payment):
    payment.payment_status = "failed"
    payment.save()

    # inventory rollback
```

👉 এখানে inventory rollback করতে হবে (important)

---

# 🔁 Step 5: Inventory Rollback (Critical)

```python id="s8h1qw"
def release_room(room, check_in, check_out):
    from datetime import timedelta

    current_date = check_in

    while current_date < check_out:
        inventory = RoomInventory.objects.get(room=room, date=current_date)
        inventory.available_rooms += 1
        inventory.save()

        current_date += timedelta(days=1)
```

---

# 🔐 Step 6: Atomic Transaction (PRO LEVEL)

সবকিছু একসাথে safe রাখতে:

```python id="4p6z2l"
from django.db import transaction

@transaction.atomic
def safe_booking_create(user, room, check_in, check_out, guests):
    if not is_room_available(room, check_in, check_out):
        raise ValueError("Not available")

    booking = Booking.objects.create(
        guest=user,
        room=room,
        check_in=check_in,
        check_out=check_out,
        guests_count=guests
    )

    reserve_room(room, check_in, check_out)

    return booking
```

---

# 🎯 এখন তুমি যা শিখলে

✔ Real booking flow
✔ Availability algorithm
✔ Inventory management
✔ Payment integration logic
✔ Failure handling
✔ Atomic transactions

---

# 🔥 Next Level (Optional কিন্তু Powerful)

চাও তাহলে next step এ আমি দেখাতে পারি:

* ✅ DRF API (Booking endpoint)
* ✅ Live availability API
* ✅ SSLCommerz integration (Bangladesh ready 💰)
* ✅ Admin dashboard logic

---

👉 তুমি বলো next কি চাও:

1. API বানানো
2. Payment integration
3. Full SaaS architecture

আমি step-by-step guide করে দিবো 🚀
তুমি যদি বলো **“every user profile model distributed”**, তাহলে বুঝাচ্ছো তুমি system টাকে clean, scalable আর role-basedভাবে আলাদা করতে চাও — এটা actually **very good architecture decision** 👍

চল সহজভাবে বুঝাই 👇

---

# 🎯 Problem (Current Design)

এখন তোমার `User` model এর মধ্যে সব role mix হয়ে আছে:

* Guest
* Vendor Admin
* Vendor Staff

👉 Issue:

* Future এ fields বাড়লে model messy হয়ে যাবে
* Role-specific data manage করা কঠিন হবে

---

# ✅ Best Practice: Separate Profile Models

👉 Core idea:

* `User` থাকবে **authentication + common info**
* Role অনুযায়ী আলাদা profile থাকবে

---

# 🧱 Recommended Architecture

## ✅ 1. Base User (Clean)

```python id="u1base"
class User(AbstractUser):
    class Role(models.TextChoices):
        SUPER_ADMIN = "super_admin"
        VENDOR_ADMIN = "vendor_admin"
        VENDOR_STAFF = "vendor_staff"
        GUEST = "guest"

    role = models.CharField(max_length=20, choices=Role.choices)
```

---

## ✅ 2. Guest Profile

```python id="guestp"
class GuestProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="guest_profile")
    phone = models.CharField(max_length=20)
    address = models.TextField(blank=True)

    def __str__(self):
        return f"Guest: {self.user.username}"
```

---

## ✅ 3. Vendor Admin Profile

```python id="vendoradminp"
class VendorAdminProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="vendor_admin_profile")
    phone = models.CharField(max_length=20)
    company_name = models.CharField(max_length=255, blank=True)

    def __str__(self):
        return f"Vendor Admin: {self.user.username}"
```

---

## ✅ 4. Vendor Staff Profile

```python id="vendorstaffp"
class VendorStaffProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name="vendor_staff_profile")
    vendor = models.ForeignKey("Vendor", on_delete=models.CASCADE)
    designation = models.CharField(max_length=100)

    def __str__(self):
        return f"Staff: {self.user.username}"
```

---

# 🔥 Why This is Better

## ✅ 1. Clean Separation

* Guest → booking related data
* Vendor → business data
* Staff → operational data

---

## ✅ 2. Scalable 🚀

আগামীতে তুমি add করতে পারবে:

* loyalty points (guest)
* subscription plan (vendor)
* permissions (staff)

---

## ✅ 3. নিরাপদ (Safer Logic)

```python id="checkrole"
if user.role == "guest":
    user.guest_profile
```

---

## ✅ 4. Django Admin Friendly

প্রতিটা role আলাদা manage করা সহজ

---

# ⚠️ Important Rule (VERY IMPORTANT)

👉 Ensure one user = one profile

Use signals:

```python id="signalex"
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        if instance.role == "guest":
            GuestProfile.objects.create(user=instance)
        elif instance.role == "vendor_admin":
            VendorAdminProfile.objects.create(user=instance)
```

---

# 💡 Alternative (Advanced)

👉 যদি ultra scalable system বানাও (like SaaS):

* Use **Generic Profile सिस्टम**
* অথবা **polymorphic models**

---

# 🎯 Final Verdict

✔ Small project → current model OK
✔ Medium project → separate profiles 👍
✔ SaaS multi-vendor → MUST use distributed profiles 🚀

---

👉 Honest suggestion:
তুমি যেহেতু **multi-vendor system বানাচ্ছো**,
➡️ **Separate profile model use করা উচিত (recommended)**

---

👉 চাইলে next step এ আমি দেখাতে পারি:

* DRF serializer with multiple profiles
* Role-based login system
* Permission system (very important 🔐)

বললেই step-by-step করে দিবো 🚀
খুব ভালো question — এটা আসলে **real-world system design এর core problem** 🔥

👉 তুমি ঠিকই ধরছো:
**User যদি নিজের role নিজে select করে → system insecure হয়ে যাবে ❌**

---

# 🎯 Short Answer

👉 **User role নিজে select করবে না**
👉 **System / Admin / Flow অনুযায়ী automatically assign হবে**

---

# 🧠 Real-World Approach

## ✅ 1. Guest (Default User)

👉 যখন কেউ signup করে:

```python id="signupguest"
user = User.objects.create_user(
    username=username,
    password=password,
    role="guest"
)
```

✔ Default role = `guest`
✔ সাথে সাথে `GuestProfile` create হবে (signal দিয়ে)

---

## ✅ 2. Vendor Admin (Controlled Registration)

### Option A: Admin Creates Vendor

👉 safest way

```python id="admincreate"
user.role = "vendor_admin"
VendorAdminProfile.objects.create(user=user)
```

---

### Option B: Vendor আবেদন করবে (Recommended 🔥)

👉 flow:

1. User signup (guest হিসেবে)
2. “Become a Vendor” button click করে
3. Request submit করে
4. Admin approve করে

```python id="vendorapprove"
user.role = "vendor_admin"
user.save()

VendorAdminProfile.objects.create(user=user)
```

---

## ✅ 3. Vendor Staff (Assigned by Vendor Admin)

👉 Staff নিজে account বানাবে না

Flow:

1. Vendor admin staff create করবে
2. System automatically role assign করবে

```python id="staffcreate"
user = User.objects.create_user(
    username="staff1",
    password="1234",
    role="vendor_staff"
)

VendorStaffProfile.objects.create(
    user=user,
    vendor=vendor
)
```

---

# 🔐 🔥 Golden Rule

👉 কখনোই এটা করো না:

```python
role = request.data.get("role") ❌
```

❌ User input থেকে role নেওয়া dangerous
✔ Always backend decide করবে

---

# ⚙️ Profile Distribution Logic

## ✅ Signal + Role Based Creation

```python id="signalrole"
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        if instance.role == "guest":
            GuestProfile.objects.create(user=instance)

        elif instance.role == "vendor_admin":
            VendorAdminProfile.objects.create(user=instance)

        elif instance.role == "vendor_staff":
            VendorStaffProfile.objects.create(user=instance)
```

---

# 🚀 Better Architecture (Pro Level)

👉 Instead of signal, use **service layer** (clean approach)

```python id="servicecreate"
def create_guest_user(data):
    user = User.objects.create_user(**data, role="guest")
    GuestProfile.objects.create(user=user)
    return user
```

---

# 🎯 Final Flow Summary

| User Type    | Role কে assign করবে? | Profile create হবে |
| ------------ | -------------------- | ------------------ |
| Guest        | System (default)     | Auto               |
| Vendor Admin | Admin approve        | Auto               |
| Vendor Staff | Vendor Admin         | Auto               |

---

# 💡 Real Insight

👉 Production system এ:

* Role = **controlled field**
* Profile = **auto-generated**
* User input = **never trusted for roles**

---

# 🔥 Final Verdict

✔ User role নিজে select করবে না
✔ Backend control করবে
✔ Role অনুযায়ী profile auto create হবে

---

👉 চাইলে next step এ আমি দেখাতে পারি:

* 🔐 Role-based permission (DRF)
* 🔑 Login system (JWT + roles)
* 🧩 Multi-vendor dashboard structure

বললেই deep dive করে দিবো 🚀
হ্যাঁ — তুমি যে approachটা বলছো সেটা **logically ঠিক**, কিন্তু একটু refine করলে এটা **production-ready + bug-free** হবে 👍

আমি তোমার idea টাকে clean architecture এ সাজিয়ে দিচ্ছি 👇

---

# 🎯 তোমার Idea (Rewritten Cleanভাবে)

👉 তুমি করতে চাচ্ছো:

1. **User create হলে → default profile (GuestProfile) auto create (signal)**
2. পরে যদি role change হয় → manually correct profile assign

✔ এটা workable
❗ কিন্তু কিছু edge case handle করতে হবে

---

# ⚠️ Potential Problem

ধরো:

* User signup → GuestProfile তৈরি হলো
* পরে vendor_admin হলো

👉 তখন:
❌ GuestProfile রয়ে যাবে
❌ VendorAdminProfile নতুন create হবে

➡️ এক user এর multiple profile হয়ে যাবে 😬

---

# ✅ Clean Solution (Recommended Architecture)

## 🔥 Rule:

👉 **One user = One active profile**

---

# ✅ Step 1: Signal → Default GuestProfile

```python id="signdefault"
@receiver(post_save, sender=User)
def create_default_profile(sender, instance, created, **kwargs):
    if created:
        GuestProfile.objects.create(user=instance)
```

✔ সব user শুরুতে guest

---

# ✅ Step 2: Role Change Handler (IMPORTANT)

👉 যখন role change হবে, তখন:

* old profile delete / deactivate
* new profile create

---

## 🔥 Example:

```python id="rolechangeclean"
def change_user_role(user, new_role, vendor=None):

    # delete old profiles
    if hasattr(user, "guest_profile"):
        user.guest_profile.delete()

    if hasattr(user, "vendor_admin_profile"):
        user.vendor_admin_profile.delete()

    if hasattr(user, "vendor_staff_profile"):
        user.vendor_staff_profile.delete()

    # update role
    user.role = new_role
    user.save()

    # create new profile
    if new_role == "vendor_admin":
        VendorAdminProfile.objects.create(user=user)

    elif new_role == "vendor_staff":
        VendorStaffProfile.objects.create(user=user, vendor=vendor)

    elif new_role == "guest":
        GuestProfile.objects.create(user=user)
```

---

# ✅ Why This is Best

✔ No duplicate profiles
✔ Clean database
✔ predictable behavior
✔ easy debugging

---

# 🔥 Alternative (Better for Scaling)

👉 delete না করে “soft switch” করতে পারো:

```python id="softswitch"
is_active = models.BooleanField(default=True)
```

👉 old profile → inactive
👉 new profile → active

---

# 🚀 Final Recommendation

👉 তোমার final system হওয়া উচিত:

✔ Signal → only for default guest তৈরি
✔ Role change → always service function দিয়ে
✔ Profile → controlled, one per user

---

# 🎯 Final Verdict

✔ তোমার idea correct direction এ
❗ কিন্তু directly করলে messy হবে
🔥 Proper way = **signal + controlled role change logic**

---

👉 চাইলে next step এ আমি দেখাতে পারি:

* DRF serializer এ multiple profile handle
* Role-based permission system (real project level 🔐)
* Vendor approval API

বললেই deep dive 🚀
Nice — এটা আসলে **real-world DRF design problem** 🔥
Multi-profile system এ serializer cleanভাবে handle করতে পারলে তোমার API professional level হয়ে যাবে।

আমি তোমাকে **3টা level এ solution** দেখাচ্ছি:

---

# 🎯 Goal

👉 একটাই API `/me/` call করলে:

* Guest হলে → GuestProfile data
* Vendor হলে → VendorProfile data
* Staff হলে → StaffProfile data

---

# ✅ Step 1: Profile Serializers

```python id="guestser"
from rest_framework import serializers

class GuestProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = GuestProfile
        fields = ["phone", "address"]
```

---

```python id="vendoradminser"
class VendorAdminProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = VendorAdminProfile
        fields = ["phone", "company_name"]
```

---

```python id="vendorstaffser"
class VendorStaffProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = VendorStaffProfile
        fields = ["vendor", "designation"]
```

---

# 🔥 Step 2: Dynamic User Serializer (CORE)

👉 এখানে magic হবে 👇

```python id="dynamicuser"
class UserSerializer(serializers.ModelSerializer):
    profile = serializers.SerializerMethodField()

    class Meta:
        model = User
        fields = ["id", "username", "role", "profile"]

    def get_profile(self, obj):
        if obj.role == "guest" and hasattr(obj, "guest_profile"):
            return GuestProfileSerializer(obj.guest_profile).data

        elif obj.role == "vendor_admin" and hasattr(obj, "vendor_admin_profile"):
            return VendorAdminProfileSerializer(obj.vendor_admin_profile).data

        elif obj.role == "vendor_staff" and hasattr(obj, "vendor_staff_profile"):
            return VendorStaffProfileSerializer(obj.vendor_staff_profile).data

        return None
```

---

# 🧪 Output Example

## 👉 Guest User Response:

```json
{
  "id": 1,
  "username": "john",
  "role": "guest",
  "profile": {
    "phone": "017xxxx",
    "address": "Dhaka"
  }
}
```

---

## 👉 Vendor Admin Response:

```json
{
  "id": 2,
  "username": "hotel_owner",
  "role": "vendor_admin",
  "profile": {
    "phone": "018xxxx",
    "company_name": "ABC Hotel"
  }
}
```

---

# 🚀 Step 3: Update Profile (Important)

👉 update করার সময় dynamic handling লাগবে

```python id="updateprofile"
class UserUpdateSerializer(serializers.ModelSerializer):
    profile = serializers.JSONField(write_only=True)

    class Meta:
        model = User
        fields = ["username", "profile"]

    def update(self, instance, validated_data):
        profile_data = validated_data.pop("profile", {})

        instance.username = validated_data.get("username", instance.username)
        instance.save()

        # update profile based on role
        if instance.role == "guest":
            for key, value in profile_data.items():
                setattr(instance.guest_profile, key, value)
            instance.guest_profile.save()

        elif instance.role == "vendor_admin":
            for key, value in profile_data.items():
                setattr(instance.vendor_admin_profile, key, value)
            instance.vendor_admin_profile.save()

        return instance
```

---

# 🔐 Step 4: View Example

```python id="meapi"
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
from rest_framework.response import Response

class MeAPIView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        serializer = UserSerializer(request.user)
        return Response(serializer.data)
```

---

# 🔥 Pro Tips (Important)

## ✅ 1. N+1 Query Problem Avoid করো

```python id="prefetch"
User.objects.select_related(
    "guest_profile",
    "vendor_admin_profile",
    "vendor_staff_profile"
)
```

---

## ✅ 2. Clean Code Alternative (Advanced)

👉 mapping use করতে পারো:

```python id="mapping"
PROFILE_SERIALIZER_MAP = {
    "guest": ( "guest_profile", GuestProfileSerializer ),
    "vendor_admin": ( "vendor_admin_profile", VendorAdminProfileSerializer ),
    "vendor_staff": ( "vendor_staff_profile", VendorStaffProfileSerializer ),
}
```

---

# 🎯 Final Verdict

✔ DRF এ multiple profile handle করার best way =
👉 `SerializerMethodField` + role-based logic

✔ Clean, scalable, production-ready

---

# 🚀 Next Level (Optional)

চাও তাহলে আমি দেখাতে পারি:

* 🔐 Role-based permission (DRF custom permission)
* 🧩 Separate dashboard API per role
* ⚡ JWT login with role response

বললেই next level এ নিয়ে যাবো 😎
ঠিক বলেছো — project flow ঠিকভাবে organize করা খুব গুরুত্বপূর্ণ, নাহলে পরে dependency conflict বা messy API হবার সম্ভাবনা থাকে। Multi-vendor hotel system এর জন্য আমি step-by-step **recommended development flow** দিচ্ছি:

---

# 🎯 Recommended Flow for Models & API

## 1️⃣ Core / Authentication Layer

**Models to create first:**

* `User` + `GuestProfile` (default profile)
* `VendorAdminProfile`
* `VendorStaffProfile`

**Reason:**
সবকিছুর root হলো `User` → সব other models তার উপর depend করে।

**API focus:**

* Signup API (guest)
* Login API
* `/me/` profile API (dynamic serializer)

---

## 2️⃣ Vendor Layer

**Models:**

* `Vendor`
* `VendorCustomization` (optional later)

**API focus:**

* Vendor creation / approval
* Vendor list / detail
* Vendor dashboard

**Dependency:**
Vendor model depend করে `VendorAdminProfile` এর উপর → তাই `User` + `VendorAdminProfile` আগে বানাতে হবে।

---

## 3️⃣ Rooms / Inventory Layer

**Models:**

* `RoomType`

**API focus:**

* Room list / create / update (vendor restricted)
* Room detail API

**Dependency:**
RoomType needs `Vendor` → so Vendor model must exist first.

---

## 4️⃣ Booking Layer

**Models:**

* `Booking`

**API focus:**

* Booking creation (guest)
* Booking detail
* Booking list (guest / vendor staff access)

**Dependency:**
Booking depends on `RoomType` + `User` (guest)

---

## 5️⃣ Payments Layer

**Models:**

* `Payment`

**API focus:**

* Payment creation / update
* Transaction ID auto generate
* Payment status update

**Dependency:**
Payment needs `Booking` → Booking must exist

---

## 6️⃣ Reviews / Ratings

**Models:**

* `Review`

**API focus:**

* Guest can create review after booking
* Vendor / admin can see review

**Dependency:**
Review depends on `Booking` → Booking must exist

---

## 7️⃣ Vendor Staff Management

**Models:**

* `VendorStaffProfile` (already in core)

**API focus:**

* Vendor admin can create staff
* Staff dashboard
* Assign rooms, bookings etc.

**Dependency:**
Depends on `Vendor` + `User` + `VendorStaffProfile`

---

## 8️⃣ Optional / Customization

* VendorCustomization
* Notifications
* Loyalty points / coupons

---

# 🏗 Flow Summary (Priority Order)

1. **User + Profile** → Signup, Login, Me API
2. **Vendor + VendorAdminProfile** → Approval workflow
3. **RoomType** → Inventory
4. **Booking** → Guest booking
5. **Payment** → Transactions
6. **Review** → Feedback
7. **VendorStaffProfile** → Staff management
8. **Customization / Extras** → Optional features

---

# 🔥 Pro Tips

* Always **create API for a model after the model exists**
* Start from **core models → dependencies → dependent models**
* Maintain **role-based access from day one**
* Write **signals / services** for auto profile creation & role change
* Use **prefetch/select_related** in DRF serializers to avoid N+1 queries

---

💡 Quick tip:
তুমি চাইলে আমি তোমার জন্য একটা **complete DRF project roadmap** বানিয়ে দিতে পারি, step-by-step **which API first, which permission, which serializer**, ready-to-code style।

চাইলে সেটা বানাই?
ঠিক আছে! আমি তোমার জন্য বানাচ্ছি **multi-vendor hotel management system এর complete DRF project roadmap** — step-by-step, ready-to-code style, API / permission / serializer included। 🎯

---

# 🏗 Multi-Vendor Hotel Management DRF Roadmap

---

## 1️⃣ Core Layer: User & Profiles

**Models:**

* `User` (with `role`)
* `GuestProfile` (default profile)
* `VendorAdminProfile`
* `VendorStaffProfile`

**Serializers:**

* `UserSerializer` → dynamic `profile` field
* `GuestProfileSerializer`
* `VendorAdminProfileSerializer`
* `VendorStaffProfileSerializer`

**API Endpoints:**

* `POST /api/signup/` → Guest signup (role auto = guest)
* `POST /api/login/` → JWT / Token login
* `GET /api/me/` → returns role-based profile

**Permissions:**

* Public for signup/login
* Authenticated for `/me/`

---

## 2️⃣ Vendor Layer

**Models:**

* `Vendor`
* `VendorCustomization` (optional)

**Serializers:**

* `VendorSerializer`
* `VendorDetailSerializer` → includes customization

**API Endpoints:**

* `POST /api/vendor/apply/` → guest applies (pending)
* `PATCH /api/vendor/{id}/approve/` → admin approves
* `GET /api/vendors/` → list all approved vendors
* `GET /api/vendor/{id}/` → vendor detail

**Permissions:**

* Admin only → approve vendor
* Authenticated → view vendor list
* Vendor admin → view own vendor detail

---

## 3️⃣ Room / Inventory Layer

**Models:**

* `RoomType`

**Serializers:**

* `RoomTypeSerializer`
* `RoomTypeDetailSerializer` → includes vendor info

**API Endpoints:**

* `POST /api/vendor/{vendor_id}/rooms/` → create room (vendor admin only)
* `GET /api/rooms/` → list rooms
* `GET /api/rooms/{id}/` → room detail
* `PATCH /api/rooms/{id}/` → update room (vendor admin only)

**Permissions:**

* Vendor admin → manage own rooms
* Guests → read-only

---

## 4️⃣ Booking Layer

**Models:**

* `Booking`

**Serializers:**

* `BookingSerializer`
* `BookingDetailSerializer` → room + vendor info

**API Endpoints:**

* `POST /api/bookings/` → guest create booking
* `GET /api/bookings/` → guest view own bookings
* `GET /api/vendor/bookings/` → vendor staff/admin view bookings for their rooms
* `PATCH /api/bookings/{id}/` → cancel or update (guest only if pending)

**Permissions:**

* Guests → create + read own bookings
* Vendor admin/staff → read bookings for their rooms

---

## 5️⃣ Payments Layer

**Models:**

* `Payment`

**Serializers:**

* `PaymentSerializer`

**API Endpoints:**

* `POST /api/bookings/{booking_id}/payment/` → create payment
* `GET /api/bookings/{booking_id}/payment/` → check payment status

**Permissions:**

* Guests → pay their booking
* Vendor admin → view payment for their bookings

**Extra:**

* `transaction_id` = UUIDField auto-generate
* status = pending → paid → failed

---

## 6️⃣ Reviews / Ratings

**Models:**

* `Review`

**Serializers:**

* `ReviewSerializer`

**API Endpoints:**

* `POST /api/bookings/{booking_id}/review/` → guest creates review
* `GET /api/vendor/{vendor_id}/reviews/` → vendor sees reviews

**Permissions:**

* Guest → create review for own completed booking
* Vendor admin → read reviews

---

## 7️⃣ Vendor Staff Management

**Models:**

* `VendorStaffProfile` (already in core)

**Serializers:**

* `VendorStaffSerializer`

**API Endpoints:**

* `POST /api/vendor/{vendor_id}/staff/` → create staff (vendor admin only)
* `GET /api/vendor/{vendor_id}/staff/` → list staff
* `PATCH /api/vendor/staff/{id}/` → update designation/phone

**Permissions:**

* Vendor admin → manage their staff
* Vendor staff → read-only own profile

---

## 8️⃣ Optional Features / Customization

* VendorCustomization → branding per vendor
* Notifications → email / in-app
* Loyalty points / coupons

**Permissions:**

* Vendor admin → manage customization
* Guests → read customization for display

---

# 🔥 Pro Tips

1. **Role-based Permissions:**
   Use DRF custom permission classes:

```python
class IsVendorAdmin(permissions.BasePermission):
    def has_permission(self, request, view):
        return request.user.role == "vendor_admin"
```

2. **Serializer Optimization:**
   Use `select_related` and `prefetch_related` for nested serializers to avoid N+1 queries.

3. **Signals / Service Layer:**

   * Auto create guest profile on signup
   * Service layer for role changes → create corresponding profile

4. **Start Small:**

   * First implement **User + Profile + Vendor apply** flow
   * Then build **Rooms → Booking → Payment → Review** sequentially

---

💡 **Summary:**
Start from **core auth & profile**, then **vendor**, then **rooms**, then **booking/payment/review**, and finally **staff/customization/extras**.

---

যদি চাও আমি তোমার জন্য বানাতে পারি **ready-to-use folder structure + file map + DRF views + serializer boilerplate**, যেন তুমি **copy-paste** শুরু করতে পারো।

চাও কি আমি সেটা বানাই?
ঠিক আছে! 😎
এক্ষেত্রে আমরা signal logic এ **permission check** যোগ করতে পারি যাতে শুধু **super_admin বা admin user** role পরিবর্তন করতে পারে।

DRF বা Django admin এ এটি enforce করা যায়। এখানে **signal + clean logic** ready-to-use দেখাচ্ছি।

---

## 1️⃣ Signals: Admin-only Role Change

```python id="t1qf9x"
# users/signals.py
from django.db.models.signals import pre_save, post_save
from django.dispatch import receiver
from django.contrib.auth import get_user_model
from .models import GuestProfile, VendorAdminProfile, VendorStaffProfile

User = get_user_model()

# ----------------------------
# 1. Auto-create GuestProfile for new user
# ----------------------------
@receiver(post_save, sender=User)
def create_guest_profile(sender, instance, created, **kwargs):
    if created:
        if instance.role == User.Role.GUEST:
            GuestProfile.objects.create(user=instance)


# ----------------------------
# 2. Role change → Admin-only
# ----------------------------
@receiver(pre_save, sender=User)
def handle_role_change(sender, instance, **kwargs):
    if not instance.pk:
        return  # new user already handled in post_save

    previous = User.objects.get(pk=instance.pk)
    old_role = previous.role
    new_role = instance.role

    if old_role != new_role:
        # Only allow role change if current actor is admin
        # Note: instance does not know the "request.user" here
        # So you need to enforce this check in DRF serializer or admin clean()

        # Delete old role profile
        if old_role == User.Role.GUEST:
            GuestProfile.objects.filter(user=instance).delete()
        elif old_role == User.Role.VENDOR_ADMIN:
            VendorAdminProfile.objects.filter(user=instance).delete()
        elif old_role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.filter(user=instance).delete()

        # Create new profile according to new role
        if new_role == User.Role.GUEST:
            GuestProfile.objects.create(user=instance)
        elif new_role == User.Role.VENDOR_ADMIN:
            VendorAdminProfile.objects.create(user=instance, vendor=None)
        elif new_role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.create(user=instance, vendor=None)
```

---

## 2️⃣ Admin-only Enforcement

**Signal-level এ `request.user` পাওয়া যায় না**, তাই **role change permission** **serializer বা viewset level** enforce করতে হবে।

```python id="gq7c8k"
# users/serializers.py
from rest_framework import serializers
from .models import User

class UserRoleUpdateSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['role']

    def validate_role(self, value):
        request = self.context.get('request')
        if request and not request.user.role == User.Role.SUPER_ADMIN:
            raise serializers.ValidationError("Only super admins can change roles.")
        return value
```

* এই serializer use করলে **DRF API** এ normal users role change করতে পারবে না।
* Admin (super_admin) request দিলে signal automatically profile create/delete করবে।

---

✅ এখন system এর flow:

1. New user → automatically GuestProfile।
2. Role change → signal triggers → old profile deleted, new profile created.
3. Only super_admin / admin API / admin panel থেকে role change করা যাবে।

---

যদি চাও, আমি তোমার জন্য **complete DRF-ready code** বানিয়ে দিতে পারি যেখানে:

* User / GuestProfile / VendorAdminProfile / VendorStaffProfile
* Role change only admin allowed
* Signals circular-import safe
* Serializer & viewset ready

এভাবে তুমি একেবারে plug-and-play system পাবে।

চাও আমি সেটা বানাই?
ঠিক আছে! আমরা পুরো **multi-role user system + vendor system** এর জন্য production-ready DRF structure বানাবো। ⚡

এই structure circular-import safe, signals auto-profile, role-change admin-only, এবং DRF serializer-ready।

---

## 1️⃣ Users App Models (`users/models.py`)

```python
from django.db import models
from django.contrib.auth.models import AbstractUser
from django.utils.translation import gettext_lazy as _
from django.conf import settings

class User(AbstractUser):
    username = None
    email = models.EmailField(unique=True)

    class Role(models.TextChoices):
        SUPER_ADMIN = 'super_admin', _('Super Admin')
        VENDOR_ADMIN = 'vendor_admin', _('Vendor Admin')
        VENDOR_STAFF = 'vendor_staff', _('Vendor Staff')
        GUEST = 'guest', _('Guest')

    role = models.CharField(max_length=20, choices=Role.choices, default=Role.GUEST)

    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = []

    def __str__(self):
        return self.email

# -----------------------------
# Profiles
# -----------------------------
class GuestProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='guest_profile')
    phone = models.CharField(max_length=20, blank=True, null=True)

    def __str__(self):
        return f"Guest: {self.user.email}"

class VendorAdminProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='vendor_admin_profile')
    phone = models.CharField(max_length=20, blank=True, null=True)
    vendor = models.ForeignKey('hotels.Vendor', on_delete=models.CASCADE, related_name='admins', blank=True, null=True)

    def __str__(self):
        return f"Vendor Admin: {self.user.email}"

class VendorStaffProfile(models.Model):
    user = models.OneToOneField(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, related_name='vendor_staff_profile')
    vendor = models.ForeignKey('hotels.Vendor', on_delete=models.CASCADE, related_name='staff')
    designation = models.CharField(max_length=100, blank=True, null=True)

    def __str__(self):
        return f"Staff: {self.user.email}"
```

---

## 2️⃣ Hotels App Models (`hotels/models.py`)

```python
from django.db import models
from django.conf import settings
from core.soft_delete import SoftDeleteModel

class Vendor(SoftDeleteModel):
    owner = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, limit_choices_to={'role': 'vendor_admin'})
    name = models.CharField(max_length=255)
    address = models.TextField(blank=True)
    city = models.CharField(max_length=100)
    country = models.CharField(max_length=100)
    phone = models.CharField(max_length=20, blank=True)
    email = models.EmailField()
    logo = models.ImageField(upload_to='vendor_logos/', blank=True, null=True)
    is_approved = models.BooleanField(default=False)

    def __str__(self):
        return f"{self.name} ({self.owner.email})"
```

---

## 3️⃣ Signals (`users/signals.py`)

```python
from django.db.models.signals import post_save, pre_save
from django.dispatch import receiver
from django.contrib.auth import get_user_model
from .models import GuestProfile, VendorAdminProfile, VendorStaffProfile

User = get_user_model()

# -----------------------------
# Auto-create profile on user creation
# -----------------------------
@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created:
        if instance.role == User.Role.GUEST:
            GuestProfile.objects.create(user=instance)
        elif instance.role == User.Role.VENDOR_ADMIN:
            VendorAdminProfile.objects.create(user=instance)
        elif instance.role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.create(user=instance, vendor=None)


# -----------------------------
# Handle role change
# -----------------------------
@receiver(pre_save, sender=User)
def handle_role_change(sender, instance, **kwargs):
    if not instance.pk:
        return

    previous = User.objects.get(pk=instance.pk)
    old_role = previous.role
    new_role = instance.role

    if old_role != new_role:
        # Delete old profile
        if old_role == User.Role.GUEST:
            GuestProfile.objects.filter(user=instance).delete()
        elif old_role == User.Role.VENDOR_ADMIN:
            VendorAdminProfile.objects.filter(user=instance).delete()
        elif old_role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.filter(user=instance).delete()

        # Create new profile
        if new_role == User.Role.GUEST:
            GuestProfile.objects.create(user=instance)
        elif new_role == User.Role.VENDOR_ADMIN:
            VendorAdminProfile.objects.create(user=instance, vendor=None)
        elif new_role == User.Role.VENDOR_STAFF:
            VendorStaffProfile.objects.create(user=instance, vendor=None)
```

> ⚠️ Note: Admin-only role change enforcement is done at **serializer/view level**, not in signal.

---

## 4️⃣ DRF Serializers (`users/serializers.py`)

```python
from rest_framework import serializers
from .models import User, GuestProfile, VendorAdminProfile, VendorStaffProfile

class GuestProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = GuestProfile
        fields = ['phone']

class VendorAdminProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = VendorAdminProfile
        fields = ['phone', 'vendor']

class VendorStaffProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = VendorStaffProfile
        fields = ['vendor', 'designation']

class UserSerializer(serializers.ModelSerializer):
    guest_profile = GuestProfileSerializer(read_only=True)
    vendor_admin_profile = VendorAdminProfileSerializer(read_only=True)
    vendor_staff_profile = VendorStaffProfileSerializer(read_only=True)

    class Meta:
        model = User
        fields = ['id', 'email', 'role', 'guest_profile', 'vendor_admin_profile', 'vendor_staff_profile']
        read_only_fields = ['id']

class UserRoleUpdateSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
	        fields = ['role']

    def validate_role(self, value):
        request = self.context.get('request')
        if request and not request.user.role == User.Role.SUPER_ADMIN:
            raise serializers.ValidationError("Only super admins can change roles.")
        return value
```

---

✅ এই setup gives:

1. Automatic profile creation for all users.
2. Role change deletes old profile, creates new one.
3. Admin-only enforcement for role change via serializer.
4. DRF-ready serializers with nested profile display.
5. Circular import safe (`ForeignKey('hotels.Vendor')` string reference).

---

আমি চাইলে এই structure এর **viewsets + routers + permissions** ও ready-to-use বানিয়ে দিতে পারি যাতে API plug-and-play হয়।

চাও আমি সেটা বানাই?
ঠিক আছে! এবার আমরা **views, viewsets, routers, permissions** বানাবো। এই structure production-ready, role-based permission safe, এবং DRF plug-and-play।

---

## 1️⃣ Permissions (`users/permissions.py`)

```python id="u4jgk7"
from rest_framework import permissions
from .models import User

class IsSuperAdmin(permissions.BasePermission):
    """
    Only super admins can access.
    """

    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == User.Role.SUPER_ADMIN

class IsVendorAdmin(permissions.BasePermission):
    """
    Only vendor admins can access.
    """

    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == User.Role.VENDOR_ADMIN

class IsVendorStaff(permissions.BasePermission):
    """
    Only vendor staff can access.
    """

    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == User.Role.VENDOR_STAFF

class IsGuest(permissions.BasePermission):
    """
    Only guests can access.
    """

    def has_permission(self, request, view):
        return request.user.is_authenticated and request.user.role == User.Role.GUEST
```

---

## 2️⃣ Views / ViewSets (`users/views.py`)

```python id="h8x19f"
from rest_framework import viewsets, permissions
from .models import User
from .serializers import UserSerializer, UserRoleUpdateSerializer
from .permissions import IsSuperAdmin

# -----------------------------
# User ViewSet
# -----------------------------
class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer
    permission_classes = [permissions.IsAuthenticated]

    def get_serializer_class(self):
        if self.action in ['update', 'partial_update']:
            return UserRoleUpdateSerializer
        return UserSerializer

    def get_permissions(self):
        """
        Role update restricted to super admins.
        """
        if self.action in ['update', 'partial_update']:
            self.permission_classes = [permissions.IsAuthenticated, IsSuperAdmin]
        return super().get_permissions()
```

> 🔹 **Notes**:
>
> * `UserSerializer` for read/list.
> * `UserRoleUpdateSerializer` for role updates (admin-only).
> * `get_permissions` ensures only super admin can change roles.

---

## 3️⃣ Routers (`users/urls.py`)

```python id="k5y29b"
from rest_framework.routers import DefaultRouter
from django.urls import path, include
from .views import UserViewSet

router = DefaultRouter()
router.register(r'users', UserViewSet, basename='user')

urlpatterns = [
    path('', include(router.urls)),
]
```

---

## 4️⃣ Hotels App ViewSets (`hotels/views.py`)

```python id="l8q37c"
from rest_framework import viewsets, permissions
from .models import Vendor
from .serializers import VendorSerializer
from users.permissions import IsSuperAdmin, IsVendorAdmin

class VendorViewSet(viewsets.ModelViewSet):
    queryset = Vendor.objects.active_objects.all()  # soft delete aware
    serializer_class = VendorSerializer

    def get_permissions(self):
        if self.action in ['create', 'update', 'partial_update', 'destroy']:
            self.permission_classes = [permissions.IsAuthenticated, IsVendorAdmin]
        else:
            self.permission_classes = [permissions.IsAuthenticated]
        return super().get_permissions()
```

---

## 5️⃣ Hotels Routers (`hotels/urls.py`)

```python id="v6k91t"
from rest_framework.routers import DefaultRouter
from django.urls import path, include
from .views import VendorViewSet

router = DefaultRouter()
router.register(r'vendors', VendorViewSet, basename='vendor')

urlpatterns = [
    path('', include(router.urls)),
]
```

---

## 6️⃣ DRF Serializer for Vendor (`hotels/serializers.py`)

```python id="f4w29x"
from rest_framework import serializers
from .models import Vendor

class VendorSerializer(serializers.ModelSerializer):
    class Meta:
        model = Vendor
        fields = ['id', 'name', 'address', 'city', 'country', 'phone', 'email', 'logo', 'owner']
        read_only_fields = ['id']
```

---

### ✅ Features Covered:

1. **User API**:

   * `/api/users/` → list, retrieve
   * `/api/users/<id>/` → update role (super admin only)
   * Nested profiles in read responses (`guest_profile`, `vendor_admin_profile`, `vendor_staff_profile`)

2. **Vendor API**:

   * `/api/vendors/` → list, retrieve, create, update, soft delete
   * Role-based permissions: vendor admins can create/update

3. **Soft delete** support via `active_objects` manager.

4. **Signals** auto-create/update profiles on user creation/role change.

5. **DRF Router-based, plug-and-play**.

---

💡 পরবর্তী ধাপ:

* Booking, RoomType, Payment এবং Review API + serializers + permissions একই pattern অনুসারে বানানো।
* Soft delete-aware filtering + role-based access control।

---

আমি চাইলে আমি তোমার জন্য **complete multi-vendor hotel management API structure** DRF-ready বানিয়ে দিতে পারি **Booking + Room + Payment + Review** সহ।

চাও আমি সেটা বানাই?
