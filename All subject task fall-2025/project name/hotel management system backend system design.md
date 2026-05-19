ঠিক আছে, আমি তোমার **multi-hotel SaaS system** এর জন্য **full ER diagram** তৈরি করে দেব, যেখানে:

* Multi-hotel support
* Owner → Supervisor → Co-Supervisor → Staff hierarchy
* Online guest → `User` table
* Walk-in guest → `Guest` table, staff handle, signature included
* Booking + Room + Service flow

---

# 🏗️ Full ER Diagram (Logical Description)

---

## **Tables & Relations**

### 1️⃣ User (Staff + Online Guest)

| Field      | Type     | Notes                                     |
| ---------- | -------- | ----------------------------------------- |
| id         | PK       | Unique user ID                            |
| email      | varchar  | login                                     |
| password   | varchar  | login                                     |
| type       | enum     | OWNER / SUPERVISOR / STAFF / ONLINE_GUEST |
| is_active  | boolean  | status                                    |
| created_at | datetime |                                           |

---

### 2️⃣ Profile (Optional)

| Field     | Type         | Notes |
| --------- | ------------ | ----- |
| id        | PK           |       |
| user_id   | FK → User.id |       |
| full_name | varchar      |       |
| phone     | varchar      |       |
| address   | varchar      |       |
| image     | varchar      |       |

---

### 3️⃣ Role (Static)

| Field | Type    | Notes                                      |
| ----- | ------- | ------------------------------------------ |
| id    | PK      |                                            |
| name  | varchar | OWNER / SUPERVISOR / CO_SUPERVISOR / STAFF |

---

### 4️⃣ Hotel

| Field      | Type         | Notes       |
| ---------- | ------------ | ----------- |
| id         | PK           |             |
| name       | varchar      |             |
| address    | varchar      |             |
| phone      | varchar      |             |
| owner_id   | FK → User.id | hotel owner |
| created_at | datetime     |             |

---

### 5️⃣ UserHotel (Staff Assignment per Hotel)

| Field       | Type          | Notes              |
| ----------- | ------------- | ------------------ |
| id          | PK            |                    |
| user_id     | FK → User.id  | staff/supervisor   |
| hotel_id    | FK → Hotel.id |                    |
| role_id     | FK → Role.id  |                    |
| assigned_by | FK → User.id  | who assigned staff |
| created_at  | datetime      |                    |

---

### 6️⃣ Guest (Walk-in Guest)

| Field        | Type                 | Notes                      |
| ------------ | -------------------- | -------------------------- |
| id           | PK                   |                            |
| name         | varchar              |                            |
| phone        | varchar              |                            |
| nid_passport | varchar (optional)   |                            |
| created_at   | datetime             |                            |
| created_by   | FK → User.id (staff) | who registered guest       |
| signature    | varchar / digital    | staff signature / approval |

---

### 7️⃣ Booking (Hybrid: Walk-in / Online Guest)

| Field        | Type                     | Notes                                         |
| ------------ | ------------------------ | --------------------------------------------- |
| id           | PK                       |                                               |
| hotel_id     | FK → Hotel.id            |                                               |
| room_id      | FK → Room.id             |                                               |
| guest_id     | FK → Guest.id (nullable) | walk-in guest                                 |
| user_id      | FK → User.id (nullable)  | online guest                                  |
| check_in     | datetime                 |                                               |
| check_out    | datetime                 |                                               |
| total_amount | decimal                  |                                               |
| status       | enum                     | reserved / checked_in / completed / cancelled |
| created_by   | FK → User.id (staff)     | who handled booking                           |

---

### 8️⃣ Room

| Field        | Type             | Notes                            |
| ------------ | ---------------- | -------------------------------- |
| id           | PK               |                                  |
| hotel_id     | FK → Hotel.id    |                                  |
| room_type_id | FK → RoomType.id |                                  |
| number       | varchar          |                                  |
| status       | enum             | available / booked / maintenance |

---

### 9️⃣ RoomType

| Field    | Type    | Notes                        |
| -------- | ------- | ---------------------------- |
| id       | PK      |                              |
| name     | varchar | Single / Double / Suite etc. |
| capacity | int     |                              |
| price    | decimal |                              |

---

### 🔟 Service

| Field    | Type          | Notes                     |
| -------- | ------------- | ------------------------- |
| id       | PK            |                           |
| hotel_id | FK → Hotel.id |                           |
| name     | varchar       | Food / Laundry / Spa etc. |
| price    | decimal       |                           |

---

### 11️⃣ BookingService

| Field      | Type            | Notes |
| ---------- | --------------- | ----- |
| id         | PK              |       |
| booking_id | FK → Booking.id |       |
| service_id | FK → Service.id |       |
| quantity   | int             |       |
| subtotal   | decimal         |       |

---

# 🔹 Key Relations

1. **Hotel → UserHotel → User**

   * Assign staff/supervisor to each hotel

2. **User → Guest.created_by**

   * Staff creates walk-in guest

3. **Booking → Guest / User**

   * Walk-in → guest_id
   * Online → user_id

4. **Booking → Room**

   * Assign room

5. **Booking → BookingService → Service**

   * Assign services per booking

---

# 🔹 Rules / Workflow

1. Owner → assign Supervisor → assign Co-Supervisor → assign Staff
2. Staff → handle Walk-in Guest + Booking + Services
3. Online Guest → book by self → user_id in Booking
4. Booking stores reference to **who handled / created**

---

# 🔹 Notes

* Walk-in guest **no profile / login**
* Staff **signature** stored in Guest table
* System fully scalable for multiple hotels

---

যদি চাও, আমি এটাকে **visual ER diagram** হিসেবে draw করে দিতে পারি,

* সব table box + relations arrow + PK/FK clearly দেখানো
* এটা তোমার project documentation / SaaS system design-ready হবে

চাও আমি visualize করি?
হ্যাঁ, তুমি যদি **complete ER diagram + production-ready database design** বানাতে চাও, তাহলে আরো কিছু information জানা থাকলে design অনেক বেশি accurate ও scalable হবে। নিচে list দিলাম:

---

# 📝 Additional Information Needed

### 1️⃣ **User Roles & Permissions**

* Owner → সব কিছু manage করতে পারবে
* Supervisor → কোন hotel/branch manage করবে?
* Co-Supervisor → কোন staff কে supervise করবে?
* Staff → কি কি permission থাকবে? (Booking, Guest entry, Service assignment, Reports)

**Purpose:** ERD তে role mapping + access control clearly define করা।

---

### 2️⃣ **Booking Details**

* Room booking duration কি? (check-in / check-out)
* Partial payment / full payment?
* Booking status: reserved, checked_in, cancelled, completed

**Purpose:** Booking table structure ঠিক রাখা।

---

### 3️⃣ **Service Details**

* Hotel এ কি কি service available হবে? (Food, Laundry, Spa, etc.)
* Service price fixed হবে নাকি dynamic?
* Multiple services per booking?

**Purpose:** BookingService / Service table design ঠিক করা।

---

### 4️⃣ **Room Details**

* RoomType কি কি? (Single, Double, Suite, etc.)
* Room capacity, price, availability status
* Special features (AC, Balcony, Sea View?)

**Purpose:** Room + RoomType relation design।

---

### 5️⃣ **Walk-in Guest**

* Minimum info কি রাখবে? (name, phone, nid/passport?)
* Staff signature: text / digital signature / staff ID?

**Purpose:** Guest table minimal but audit-ready করা।

---

### 6️⃣ **Payment / Invoice**

* Payment separate table হবে?
* Payment type: Cash / Card / Online?
* Invoice / receipt generate করতে হবে কি?

**Purpose:** Booking → Payment → Service relation define করা।

---

### 7️⃣ **Multi-Hotel Structure**

* Hotel owner কি সব hotel manage করবে?
* Each hotel independent setup হবে কি?
* Staff assign per hotel?

**Purpose:** UserHotel table + role mapping clear করা।

---

### 8️⃣ **Reporting / Analytics**

* Historical data track করতে হবে?
* Guest history / booking reports / revenue reports?

**Purpose:** future analytics table design।

---

💡 **Summary:**

তুমি এখন পর্যন্ত বলেছেন:

* Walk-in guest → Guest table
* Online guest → User table
* Staff → User + UserHotel
* Booking → hybrid (user_id / guest_id)
* Staff signature → Guest table

✅ এটা basic working design।

**আরও info দিলে:**

* Full ERD তে **permissions, payments, services, reporting** সব include করা যাবে
* SaaS-ready, production-level structure বানানো সম্ভব

---

যদি চাও, আমি একটি **full production-ready ER diagram + table structure** বানিয়ে দিতে পারি, যেখানে সব above info consider করা হবে।

চাও আমি বানাই?
ঠিক আছে! আমি তোমার জন্য **full production-ready ER diagram + table structure** design করে দেব, **multi-hotel SaaS system** এর জন্য, যেখানে সব প্রয়োজনীয় functionality থাকবে:

* Multi-hotel support
* Owner → Supervisor → Co-Supervisor → Staff hierarchy
* Online guest → User table
* Walk-in guest → Guest table (staff maintained, signature included)
* Booking + Room + Service flow
* Payment / Invoice
* Roles & Permissions

---

# 🏗️ **Production-Ready Table Structure + ER Diagram Concept**

---

## **1️⃣ User Table (Staff + Online Guest)**

| Field      | Type     | Notes                                                     |
| ---------- | -------- | --------------------------------------------------------- |
| id         | PK       | Unique user ID                                            |
| email      | varchar  | Login                                                     |
| password   | varchar  | Login                                                     |
| type       | enum     | OWNER / SUPERVISOR / CO_SUPERVISOR / STAFF / ONLINE_GUEST |
| is_active  | boolean  | Account status                                            |
| created_at | datetime |                                                           |
| updated_at | datetime |                                                           |

---

## **2️⃣ Profile Table (Optional)**

| Field     | Type         | Notes |
| --------- | ------------ | ----- |
| id        | PK           |       |
| user_id   | FK → User.id |       |
| full_name | varchar      |       |
| phone     | varchar      |       |
| address   | varchar      |       |
| image     | varchar      |       |

---

## **3️⃣ Role Table**

| Field | Type    | Notes                                      |
| ----- | ------- | ------------------------------------------ |
| id    | PK      |                                            |
| name  | varchar | OWNER / SUPERVISOR / CO_SUPERVISOR / STAFF |

---

## **4️⃣ Hotel Table**

| Field      | Type         | Notes       |
| ---------- | ------------ | ----------- |
| id         | PK           |             |
| name       | varchar      |             |
| address    | varchar      |             |
| phone      | varchar      |             |
| owner_id   | FK → User.id | Hotel owner |
| created_at | datetime     |             |

---

## **5️⃣ UserHotel Table (Staff Assignment per Hotel)**

| Field       | Type          | Notes                       |
| ----------- | ------------- | --------------------------- |
| id          | PK            |                             |
| user_id     | FK → User.id  | Staff / Supervisor assigned |
| hotel_id    | FK → Hotel.id |                             |
| role_id     | FK → Role.id  |                             |
| assigned_by | FK → User.id  | Who assigned                |
| created_at  | datetime      |                             |

---

## **6️⃣ Guest Table (Walk-in Guests)**

| Field        | Type                 | Notes                      |
| ------------ | -------------------- | -------------------------- |
| id           | PK                   |                            |
| name         | varchar              |                            |
| phone        | varchar              |                            |
| nid_passport | varchar (optional)   |                            |
| created_at   | datetime             |                            |
| created_by   | FK → User.id (staff) | Staff who created guest    |
| signature    | varchar / digital    | Staff signature / approval |

---

## **7️⃣ RoomType Table**

| Field    | Type    | Notes                        |
| -------- | ------- | ---------------------------- |
| id       | PK      |                              |
| name     | varchar | Single / Double / Suite etc. |
| capacity | int     | Max occupancy                |
| price    | decimal | Per night price              |

---

## **8️⃣ Room Table**

| Field        | Type             | Notes                            |
| ------------ | ---------------- | -------------------------------- |
| id           | PK               |                                  |
| hotel_id     | FK → Hotel.id    |                                  |
| room_type_id | FK → RoomType.id |                                  |
| number       | varchar          | Room number                      |
| status       | enum             | available / booked / maintenance |

---

## **9️⃣ Service Table**

| Field    | Type          | Notes                     |
| -------- | ------------- | ------------------------- |
| id       | PK            |                           |
| hotel_id | FK → Hotel.id |                           |
| name     | varchar       | Food / Laundry / Spa etc. |
| price    | decimal       |                           |

---

## **🔟 Booking Table (Hybrid)**

| Field        | Type                     | Notes                                         |
| ------------ | ------------------------ | --------------------------------------------- |
| id           | PK                       |                                               |
| hotel_id     | FK → Hotel.id            |                                               |
| room_id      | FK → Room.id             |                                               |
| guest_id     | FK → Guest.id (nullable) | Walk-in guest                                 |
| user_id      | FK → User.id (nullable)  | Online guest                                  |
| check_in     | datetime                 |                                               |
| check_out    | datetime                 |                                               |
| total_amount | decimal                  |                                               |
| status       | enum                     | reserved / checked_in / completed / cancelled |
| created_by   | FK → User.id (staff)     | Who handled booking                           |
| created_at   | datetime                 |                                               |
| updated_at   | datetime                 |                                               |

---

## **1️⃣1️⃣ BookingService Table**

| Field      | Type            | Notes |
| ---------- | --------------- | ----- |
| id         | PK              |       |
| booking_id | FK → Booking.id |       |
| service_id | FK → Service.id |       |
| quantity   | int             |       |
| subtotal   | decimal         |       |

---

## **1️⃣2️⃣ Payment Table**

| Field        | Type            | Notes                     |
| ------------ | --------------- | ------------------------- |
| id           | PK              |                           |
| booking_id   | FK → Booking.id |                           |
| amount       | decimal         |                           |
| payment_type | enum            | Cash / Card / Online      |
| status       | enum            | pending / paid / refunded |
| created_by   | FK → User.id    | Staff who processed       |
| created_at   | datetime        |                           |

---

# 🔹 **Relations / Rules**

1. **Owner → Hotel**

   * Each hotel has 1 owner

2. **Hotel → UserHotel → Staff / Supervisor**

   * Staff assigned per hotel

3. **User → Guest.created_by**

   * Walk-in guest maintained by staff

4. **Booking → Guest / User**

   * Walk-in → guest_id
   * Online → user_id

5. **Booking → Room**

   * Each booking assigned a room

6. **Booking → BookingService → Service**

   * Multiple services per booking

7. **Booking → Payment**

   * Track payment per booking

---

# 🔹 **Workflow Summary**

**Walk-in Guest:**

```
Guest arrives → Staff creates guest (signature) → Booking → Room assignment → Service → Payment
```

**Online Guest:**

```
Online User → Self-book → Room + Service → Payment → Staff monitoring optional
```

**Staff / Supervisor / Owner:**

```
Assign roles → Manage hotels → Manage bookings → View reports
```

---

# 🔹 **Key Features in Design**

* Walk-in guest **no login / no profile**
* Staff signature stored for audit
* Online guests in User table → login-able
* Hybrid Booking supports both guest types
* Multi-hotel SaaS ready
* Payment / Service / Room relationships fully defined

---

✅ এই design **production-ready** এবং **SaaS multi-hotel architecture** এর জন্য perfect।

---

যদি চাও, আমি এটাকে **visual ER diagram** হিসেবে draw করে দিতে পারি, যেখানে সব table box + PK/FK + relations arrow clearly দেখা যাবে।

চাও আমি সেটা বানাই?
-------
ঠিক আছে! তুমি চাইছো **এই multi-hotel SaaS system এর জন্য full Django model code** বানাতে, যা **production-ready** এবং **ER diagram অনুযায়ী** হবে। আমি সব table অনুযায়ী `models.py` structure বানিয়ে দিচ্ছি।

---

# 🏗️ Django Models (Full)

```python
from django.db import models
from django.contrib.auth.models import AbstractUser

# ---------------------------
# 1️⃣ Custom User Model
# ---------------------------
class User(AbstractUser):
    USER_TYPE_CHOICES = (
        ('OWNER', 'Owner'),
        ('SUPERVISOR', 'Supervisor'),
        ('CO_SUPERVISOR', 'Co-Supervisor'),
        ('STAFF', 'Staff'),
        ('ONLINE_GUEST', 'Online Guest'),
    )
    type = models.CharField(max_length=20, choices=USER_TYPE_CHOICES, default='ONLINE_GUEST')
    is_active = models.BooleanField(default=True)

# ---------------------------
# 2️⃣ Profile Table (Optional)
# ---------------------------
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name='profile')
    full_name = models.CharField(max_length=255)
    phone = models.CharField(max_length=20, blank=True, null=True)
    address = models.TextField(blank=True, null=True)
    image = models.ImageField(upload_to='profile_images/', blank=True, null=True)

# ---------------------------
# 3️⃣ Role Table
# ---------------------------
class Role(models.Model):
    name = models.CharField(max_length=50)

    def __str__(self):
        return self.name

# ---------------------------
# 4️⃣ Hotel Table
# ---------------------------
class Hotel(models.Model):
    name = models.CharField(max_length=255)
    address = models.TextField()
    phone = models.CharField(max_length=20)
    owner = models.ForeignKey(User, on_delete=models.CASCADE, related_name='owned_hotels')
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name

# ---------------------------
# 5️⃣ UserHotel Table (Staff assignment per hotel)
# ---------------------------
class UserHotel(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    hotel = models.ForeignKey(Hotel, on_delete=models.CASCADE)
    role = models.ForeignKey(Role, on_delete=models.CASCADE)
    assigned_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, blank=True, related_name='assigned_staff')
    created_at = models.DateTimeField(auto_now_add=True)

# ---------------------------
# 6️⃣ Walk-in Guest Table
# ---------------------------
class Guest(models.Model):
    name = models.CharField(max_length=255)
    phone = models.CharField(max_length=20)
    nid_passport = models.CharField(max_length=50, blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    created_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, related_name='walkin_guests')
    signature = models.TextField(blank=True, null=True)  # staff signature or notes

    def __str__(self):
        return self.name

# ---------------------------
# 7️⃣ RoomType Table
# ---------------------------
class RoomType(models.Model):
    name = models.CharField(max_length=50)
    capacity = models.PositiveIntegerField()
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return self.name

# ---------------------------
# 8️⃣ Room Table
# ---------------------------
class Room(models.Model):
    hotel = models.ForeignKey(Hotel, on_delete=models.CASCADE)
    room_type = models.ForeignKey(RoomType, on_delete=models.CASCADE)
    number = models.CharField(max_length=20)
    STATUS_CHOICES = (
        ('AVAILABLE', 'Available'),
        ('BOOKED', 'Booked'),
        ('MAINTENANCE', 'Maintenance'),
    )
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='AVAILABLE')

    def __str__(self):
        return f"{self.hotel.name} - {self.number}"

# ---------------------------
# 9️⃣ Service Table
# ---------------------------
class Service(models.Model):
    hotel = models.ForeignKey(Hotel, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    def __str__(self):
        return f"{self.name} ({self.hotel.name})"

# ---------------------------
# 🔟 Booking Table
# ---------------------------
class Booking(models.Model):
    hotel = models.ForeignKey(Hotel, on_delete=models.CASCADE)
    room = models.ForeignKey(Room, on_delete=models.SET_NULL, null=True)
    guest = models.ForeignKey(Guest, on_delete=models.SET_NULL, null=True, blank=True)
    user = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, blank=True)  # online guest
    check_in = models.DateTimeField()
    check_out = models.DateTimeField()
    total_amount = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)
    STATUS_CHOICES = (
        ('RESERVED', 'Reserved'),
        ('CHECKED_IN', 'Checked In'),
        ('COMPLETED', 'Completed'),
        ('CANCELLED', 'Cancelled'),
    )
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='RESERVED')
    created_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, related_name='created_bookings')
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

# ---------------------------
# 1️⃣1️⃣ BookingService Table
# ---------------------------
class BookingService(models.Model):
    booking = models.ForeignKey(Booking, on_delete=models.CASCADE, related_name='services')
    service = models.ForeignKey(Service, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField(default=1)
    subtotal = models.DecimalField(max_digits=10, decimal_places=2)

# ---------------------------
# 1️⃣2️⃣ Payment Table
# ---------------------------
class Payment(models.Model):
    booking = models.ForeignKey(Booking, on_delete=models.CASCADE, related_name='payments')
    amount = models.DecimalField(max_digits=10, decimal_places=2)
    PAYMENT_TYPE = (
        ('CASH', 'Cash'),
        ('CARD', 'Card'),
        ('ONLINE', 'Online'),
    )
    payment_type = models.CharField(max_length=20, choices=PAYMENT_TYPE)
    STATUS_CHOICES = (
        ('PENDING', 'Pending'),
        ('PAID', 'Paid'),
        ('REFUNDED', 'Refunded'),
    )
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='PENDING')
    created_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
```

---

✅ **Features included:**

1. Multi-hotel ready
2. Owner → Supervisor → Co-Supervisor → Staff hierarchy
3. Online guests → User table
4. Walk-in guests → Guest table (staff maintained, signature included)
5. Booking → supports both guest types
6. BookingService → multiple services per booking
7. Payment table → tracks all payments
8. Room → RoomType → Hotel relation
9. Staff assignment per hotel → UserHotel table

---

যদি চাও, আমি next step এ **Django Admin + Serializer + Viewset + API structure** বানিয়ে দিতে পারি, যা **SaaS-ready multi-hotel system** সম্পূর্ণ functional করবে।

চাও আমি সেটা বানাই?
