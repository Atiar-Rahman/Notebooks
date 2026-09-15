অবশ্যই। এবার **Event / Ticket Booking System**-এর জন্য আগের projectগুলোর মতো **production-level complete model architecture** দেব।

এখানে শুধু Event + Ticket না রেখে **Event → Venue → Session → Ticket Type → Inventory → Booking → Payment → Ticket → Check-in → Refund → Coupon → Notification → Audit** পুরো lifecycle cover করব।

আমি **45টি model** দিচ্ছি এবং প্রতিটির **model/file name + field name + Django data type + relationship + important constraints** থাকবে।

# 🎫 Event / Ticket Booking System

## Complete Model List

```text
1.  BaseModel
2.  Organization
3.  OrganizationMember

4.  Venue
5.  VenueAddress
6.  VenueHall
7.  VenueSeat

8.  EventCategory
9.  Event
10. EventImage
11. EventOrganizer

12. EventSession
13. SessionSpeaker
14. Speaker

15. TicketType
16. TicketTier
17. TicketInventory

18. CustomerProfile
19. CustomerAddress

20. Booking
21. BookingItem
22. BookingAttendee

23. Ticket
24. TicketTransfer
25. TicketCheckIn

26. PaymentMethod
27. Payment

28. Refund
29. RefundItem

30. Coupon
31. CouponUsage

32. EventReview

33. Wishlist
34. WishlistEvent

35. Notification

36. PromoCode

37. EventCommission
38. OrganizerPayout
39. OrganizerPayoutItem

40. Waitlist
41. WaitlistEntry

42. IdempotencyRecord
43. AuditLog

44. SeatingReservation
45. BookingStatusHistory
```

---

# 📁 Recommended File Structure

একটা বড় `models.py` না রেখে আলাদা file করা ভালো:

```text
events/
│
├── models/
│   ├── __init__.py
│   ├── base.py
│   ├── organization.py
│   ├── venue.py
│   ├── event.py
│   ├── speaker.py
│   ├── session.py
│   ├── ticket.py
│   ├── customer.py
│   ├── booking.py
│   ├── payment.py
│   ├── refund.py
│   ├── coupon.py
│   ├── review.py
│   ├── wishlist.py
│   ├── notification.py
│   ├── commission.py
│   ├── payout.py
│   ├── waitlist.py
│   ├── reservation.py
│   ├── history.py
│   ├── idempotency.py
│   └── audit.py
```

---

# 1. `base.py`

## BaseModel

সব model-এর common fields।

```python
id = models.UUIDField(
    primary_key=True,
    default=uuid.uuid4,
    editable=False
)

created_at = models.DateTimeField(auto_now_add=True)
updated_at = models.DateTimeField(auto_now=True)

is_active = models.BooleanField(default=True)
deleted_at = models.DateTimeField(null=True, blank=True)
```

### Data Type

|Field|Django Type|
|---|---|
|id|UUIDField|
|created_at|DateTimeField|
|updated_at|DateTimeField|
|is_active|BooleanField|
|deleted_at|DateTimeField|

---

# 2. `organization.py`

## Organization

Event platform / event company।

```text
Organization
├── name
├── slug
├── legal_name
├── registration_number
├── email
├── phone
├── website
├── logo
├── description
├── currency
└── is_verified
```

|Field|Type|
|---|---|
|name|CharField(200)|
|slug|SlugField(220, unique=True)|
|legal_name|CharField(250)|
|registration_number|CharField(100)|
|email|EmailField|
|phone|CharField(30)|
|website|URLField|
|logo|ImageField|
|description|TextField|
|currency|CharField(3)|
|is_verified|BooleanField|

---

## OrganizationMember

```text
organization → Organization
user → User
```

|Field|Type|
|---|---|
|organization|ForeignKey|
|user|ForeignKey|
|role|CharField(30)|
|joined_at|DateTimeField|
|is_active|BooleanField|

Roles:

```text
owner
admin
event_manager
staff
accountant
viewer
```

Constraint:

```text
Unique(organization, user)
```

---

# 3. `venue.py`

# Venue

Event location।

```text
Venue
├── organization
├── name
├── code
├── description
├── venue_type
├── capacity
├── phone
├── email
└── is_active
```

|Field|Type|
|---|---|
|organization|ForeignKey|
|name|CharField(200)|
|code|CharField(50)|
|description|TextField|
|venue_type|CharField(30)|
|capacity|PositiveIntegerField|
|phone|CharField(30)|
|email|EmailField|
|is_active|BooleanField|

Venue types:

```text
stadium
auditorium
hall
conference_center
outdoor
theater
cinema
other
```

Constraint:

```text
Unique(organization, code)
```

---

# VenueAddress

```text
venue → Venue
address_line
city
state
country
postal_code
latitude
longitude
```

|Field|Type|
|---|---|
|venue|OneToOneField|
|address_line|TextField|
|city|CharField(100)|
|state|CharField(100)|
|country|CharField(100)|
|postal_code|CharField(20)|
|latitude|DecimalField(9,6)|
|longitude|DecimalField(9,6)|

---

# VenueHall

এক venue-এর multiple hall থাকতে পারে।

```text
VenueHall
├── venue
├── name
├── code
├── capacity
└── seating_type
```

|Field|Type|
|---|---|
|venue|ForeignKey|
|name|CharField(150)|
|code|CharField(50)|
|capacity|PositiveIntegerField|
|seating_type|CharField(30)|

---

# VenueSeat

Reserved seating-এর জন্য।

```text
VenueSeat
├── hall
├── row
├── seat_number
├── seat_type
└── is_active
```

|Field|Type|
|---|---|
|hall|ForeignKey|
|row|CharField(20)|
|seat_number|PositiveIntegerField|
|seat_type|CharField(30)|
|is_active|BooleanField|

Constraint:

```text
Unique(hall, row, seat_number)
```

---

# 4. `event.py`

# EventCategory

```text
EventCategory
├── parent
├── name
├── slug
├── description
└── is_active
```

|Field|Type|
|---|---|
|parent|ForeignKey(self)|
|name|CharField(100)|
|slug|SlugField|
|description|TextField|
|is_active|BooleanField|

Examples:

```text
Music
 ├── Concert
 └── Festival

Technology
 ├── Conference
 └── Workshop

Sports
```

---

# Event

Main model।

```text
Event
├── organization
├── category
├── venue
├── name
├── slug
├── description
├── event_type
├── start_datetime
├── end_datetime
├── timezone
├── booking_start
├── booking_end
├── capacity
├── age_limit
├── status
├── is_featured
└── is_online
```

|Field|Type|
|---|---|
|organization|ForeignKey|
|category|ForeignKey|
|venue|ForeignKey|
|name|CharField(250)|
|slug|SlugField|
|description|TextField|
|event_type|CharField(30)|
|start_datetime|DateTimeField|
|end_datetime|DateTimeField|
|timezone|CharField(50)|
|booking_start|DateTimeField|
|booking_end|DateTimeField|
|capacity|PositiveIntegerField|
|age_limit|PositiveIntegerField|
|status|CharField(30)|
|is_featured|BooleanField|
|is_online|BooleanField|

Status:

```text
draft
published
booking_open
booking_closed
ongoing
completed
cancelled
```

---

# EventImage

```text
event
image
alt_text
sort_order
```

|Field|Type|
|---|---|
|event|ForeignKey|
|image|ImageField|
|alt_text|CharField(200)|
|sort_order|PositiveIntegerField|

---

# EventOrganizer

```text
event
user
role
is_primary
```

|Field|Type|
|---|---|
|event|ForeignKey|
|user|ForeignKey|
|role|CharField(30)|
|is_primary|BooleanField|

Constraint:

```text
Unique(event, user)
```

---

# 5. `speaker.py`

# Speaker

```text
Speaker
├── user
├── name
├── designation
├── company
├── bio
├── photo
├── email
├── linkedin
└── website
```

|Field|Type|
|---|---|
|user|OneToOneField(null=True)|
|name|CharField(150)|
|designation|CharField(150)|
|company|CharField(150)|
|bio|TextField|
|photo|ImageField|
|email|EmailField|
|linkedin|URLField|
|website|URLField|

---

# 6. `session.py`

## EventSession

এক event-এর ভিতরে multiple session।

```text
Event
 ├── Opening
 ├── Keynote
 ├── Workshop
 └── Closing
```

|Field|Type|
|---|---|
|event|ForeignKey|
|hall|ForeignKey|
|title|CharField(250)|
|description|TextField|
|start_datetime|DateTimeField|
|end_datetime|DateTimeField|
|session_type|CharField(30)|
|capacity|PositiveIntegerField|
|status|CharField(30)|

---

# SessionSpeaker

```text
session
speaker
role
sort_order
```

Constraint:

```text
Unique(session, speaker)
```

---

# 7. `ticket.py`

## TicketType ⭐⭐⭐

Ticket category।

```text
TicketType
├── event
├── name
├── code
├── description
├── price
├── currency
├── quantity
├── min_quantity_per_booking
├── max_quantity_per_booking
├── sales_start
├── sales_end
├── is_transferable
├── is_refundable
└── is_active
```

|Field|Type|
|---|---|
|event|ForeignKey|
|name|CharField(100)|
|code|CharField(50)|
|description|TextField|
|price|DecimalField(12,2)|
|currency|CharField(3)|
|quantity|PositiveIntegerField|
|min_quantity_per_booking|PositiveIntegerField|
|max_quantity_per_booking|PositiveIntegerField|
|sales_start|DateTimeField|
|sales_end|DateTimeField|
|is_transferable|BooleanField|
|is_refundable|BooleanField|
|is_active|BooleanField|

Example:

```text
VIP          ৳5000
Premium      ৳3000
General      ৳1500
```

---

# TicketTier

Dynamic pricing / early bird।

```text
ticket_type
name
price
quantity
sales_start
sales_end
priority
```

Example:

```text
Early Bird     1000
Regular        1500
Late Bird      2000
```

---

# TicketInventory

Ticket stock tracking।

```text
ticket_type
total_quantity
reserved_quantity
sold_quantity
available_quantity
```

Formula:

```text
available_quantity
=
total_quantity
-
reserved_quantity
-
sold_quantity
```

Constraint:

```text
Unique(ticket_type)
```

---

# 8. `customer.py`

## CustomerProfile

```text
user
customer_code
phone
date_of_birth
profile_image
is_verified
```

|Field|Type|
|---|---|
|user|OneToOneField|
|customer_code|CharField(50)|
|phone|CharField(30)|
|date_of_birth|DateField|
|profile_image|ImageField|
|is_verified|BooleanField|

---

# CustomerAddress

```text
customer
label
address_line
city
country
postal_code
is_default
```

---

# 9. `booking.py`

# Booking ⭐⭐⭐

সবচেয়ে important model।

```text
Booking
├── booking_number
├── customer
├── event
├── status
├── subtotal
├── discount
├── tax
├── service_fee
├── total_amount
├── paid_amount
├── refund_amount
├── expires_at
├── booked_at
└── created_by
```

|Field|Type|
|---|---|
|booking_number|CharField(50, unique=True)|
|customer|ForeignKey|
|event|ForeignKey|
|status|CharField(30)|
|subtotal|DecimalField(12,2)|
|discount|DecimalField(12,2)|
|tax|DecimalField(12,2)|
|service_fee|DecimalField(12,2)|
|total_amount|DecimalField(12,2)|
|paid_amount|DecimalField(12,2)|
|refund_amount|DecimalField(12,2)|
|expires_at|DateTimeField|
|booked_at|DateTimeField|
|created_by|ForeignKey|

Status:

```text
pending
reserved
payment_pending
confirmed
cancelled
expired
completed
refunded
```

---

# BookingItem

এক booking-এ multiple ticket type।

```text
booking
ticket_type
quantity
unit_price
discount
tax
total_price
```

---

# BookingAttendee

এক booking-এর প্রতিটি attendee।

```text
booking
ticket
name
email
phone
date_of_birth
```

---

# 10. `ticket.py`

# Ticket ⭐⭐⭐

একটি actual issued ticket।

```text
Ticket
├── booking
├── booking_item
├── ticket_type
├── attendee
├── ticket_number
├── qr_code
├── barcode
├── status
├── issued_at
├── used_at
└── transferred_at
```

Status:

```text
issued
active
used
cancelled
refunded
transferred
```

Constraint:

```text
Unique(ticket_number)
Unique(qr_code)
```

---

# TicketTransfer

Ticket অন্য user-কে transfer।

```text
ticket
from_customer
to_customer
transfer_code
transferred_at
status
```

---

# TicketCheckIn

Entry gate-এ ticket scan।

```text
ticket
event
checked_in_by
checked_in_at
gate
device_id
```

Constraint:

এক ticket ideally একবার check-in।

---

# 11. `payment.py`

## PaymentMethod

```text
PaymentMethod
├── organization
├── name
├── method_type
├── provider
└── is_active
```

Types:

```text
cash
card
bank
bkash
nagad
stripe
paypal
```

---

# Payment

```text
Payment
├── booking
├── payment_method
├── transaction_id
├── amount
├── currency
├── status
├── payment_date
├── failure_reason
└── metadata
```

|Field|Type|
|---|---|
|booking|ForeignKey|
|payment_method|ForeignKey|
|transaction_id|CharField(150)|
|amount|DecimalField(12,2)|
|currency|CharField(3)|
|status|CharField(30)|
|payment_date|DateTimeField|
|failure_reason|TextField|
|metadata|JSONField|

Payment status:

```text
pending
processing
successful
failed
cancelled
```

এক booking-এ multiple payment attempts রাখা যাবে।

---

# 12. `refund.py`

## Refund

```text
Refund
├── payment
├── booking
├── refund_number
├── amount
├── reason
├── status
├── processed_at
└── processed_by
```

Status:

```text
requested
approved
processing
completed
rejected
```

---

# RefundItem

```text
refund
ticket
amount
reason
```

---

# 13. `coupon.py`

## Coupon

```text
Coupon
├── organization
├── code
├── name
├── discount_type
├── discount_value
├── minimum_amount
├── maximum_discount
├── usage_limit
├── usage_count
├── valid_from
├── valid_until
└── is_active
```

Discount:

```text
percentage
fixed
```

---

# CouponUsage

```text
coupon
customer
booking
discount_amount
used_at
```

Constraint:

```text
Unique(coupon, booking)
```

---

# 14. `review.py`

## EventReview

```text
event
customer
booking
rating
title
comment
is_verified
is_published
```

|Field|Type|
|---|---|
|event|ForeignKey|
|customer|ForeignKey|
|booking|ForeignKey|
|rating|PositiveSmallIntegerField|
|title|CharField(150)|
|comment|TextField|
|is_verified|BooleanField|
|is_published|BooleanField|

Constraint:

```text
Unique(event, customer, booking)
```

---

# 15. `wishlist.py`

## Wishlist

```text
customer
created_at
```

Usually one wishlist/customer।

---

# WishlistEvent

```text
wishlist
event
added_at
```

Constraint:

```text
Unique(wishlist, event)
```

---

# 16. `notification.py`

## Notification

```text
user
event
booking
title
message
notification_type
is_read
read_at
```

Types:

```text
booking
payment
ticket
event_update
reminder
refund
promotion
```

---

# 17. `promo.py`

## PromoCode

Coupon-এর campaign-level abstraction চাইলে:

```text
PromoCode
├── organization
├── name
├── code
├── campaign_type
├── start_date
├── end_date
├── usage_limit
└── is_active
```

**Note:** যদি Coupon-ই যথেষ্ট হয়, production system-এ `PromoCode` বাদও দিতে পারো। দুটো একই business concept হলে duplicate রাখবে না।

---

# 18. `commission.py`

## EventCommission

Platform কত commission নেবে।

```text
EventCommission
├── event
├── booking
├── commission_type
├── commission_rate
├── commission_amount
└── created_at
```

Types:

```text
percentage
fixed
```

---

# 19. `payout.py`

## OrganizerPayout

Organizer-কে টাকা দেওয়া।

```text
OrganizerPayout
├── organization
├── organizer
├── payout_number
├── gross_amount
├── commission
├── refund_amount
├── net_amount
├── status
├── payout_date
└── transaction_reference
```

---

# OrganizerPayoutItem

```text
payout
booking
amount
commission
net_amount
```

এতে payout-এর exact source trace করা যায়।

---

# 20. `waitlist.py`

## Waitlist

Event sold out হলে।

```text
event
ticket_type
max_entries
status
created_at
```

---

# WaitlistEntry

```text
waitlist
customer
quantity
position
status
joined_at
notified_at
expires_at
```

Status:

```text
waiting
notified
converted
expired
cancelled
```

---

# 21. `reservation.py`

## SeatingReservation ⭐⭐⭐

Reserved seat booking-এর temporary lock।

```text
SeatingReservation
├── event
├── session
├── seat
├── booking
├── customer
├── reservation_token
├── reserved_at
├── expires_at
└── status
```

Status:

```text
reserved
confirmed
released
expired
```

### Very important

একই seat একই session-এ simultaneously দুইজন reserve করতে পারবে না।

PostgreSQL-এ transaction + constraint/locking ব্যবহার করা উচিত।

---

# 22. `history.py`

## BookingStatusHistory

Booking lifecycle tracking।

```text
booking
old_status
new_status
changed_by
reason
created_at
```

Example:

```text
pending
 ↓
payment_pending
 ↓
confirmed
 ↓
completed
```

---

# 23. `idempotency.py`

## IdempotencyRecord

Payment/booking duplicate request prevent।

```text
organization
user
key
endpoint
status
response_data
created_at
expires_at
```

Constraint:

```text
Unique(organization, key)
```

---

# 24. `audit.py`

## AuditLog

```text
organization
user
action
model_name
object_id
old_data
new_data
ip_address
created_at
```

Actions:

```text
create
update
delete
approve
cancel
refund
transfer
checkin
```

---

# 🔗 Complete Relationship

```text
Organization
    │
    ├── OrganizationMember
    │
    ├── Venue
    │     ├── VenueAddress
    │     ├── VenueHall
    │     │      └── VenueSeat
    │     │
    │
    └── Event
          │
          ├── EventCategory
          ├── EventImage
          ├── EventOrganizer
          │
          ├── EventSession
          │      └── SessionSpeaker
          │             └── Speaker
          │
          ├── TicketType
          │      ├── TicketTier
          │      └── TicketInventory
          │
          ├── Booking
          │      ├── BookingItem
          │      ├── BookingAttendee
          │      ├── Payment
          │      ├── Refund
          │      └── BookingStatusHistory
          │
          ├── Ticket
          │      ├── TicketTransfer
          │      └── TicketCheckIn
          │
          ├── Waitlist
          │      └── WaitlistEntry
          │
          ├── SeatingReservation
          │
          └── EventReview
```

---

# 🎟️ Complete Booking Flow

```text
Customer
   ↓
Browse Event
   ↓
Select Event
   ↓
Select Ticket Type
   ↓
Select Quantity / Seat
   ↓
SeatingReservation
   ↓
Booking
   ↓
Payment
   ↓
Payment Successful
   ↓
Booking Confirmed
   ↓
Generate Ticket
   ↓
QR Code
   ↓
Event Day
   ↓
Scan QR
   ↓
TicketCheckIn
```

---

# 🔥 Ticket Inventory Logic

ধরি:

```text
VIP total = 100
```

বর্তমানে:

```text
Sold       = 70
Reserved   = 10
```

তাহলে:

```text
Available
= 100 - 70 - 10
= 20
```

**Important:** শুধু `available_quantity` client-side থেকে update করা যাবে না।

Production logic:

```python
transaction.atomic()

TicketInventory
    ↓
select_for_update()

check available

reserve

Booking create

commit
```

এতে concurrent booking-এ overselling prevent করা যায়।

---

# 🪑 Reserved Seating

ধরি:

```text
Hall A

A1 A2 A3 A4
B1 B2 B3 B4
C1 C2 C3 C4
```

User A:

```text
A2 → reserve
```

User B একই সময়ে:

```text
A2 → reserve
```

এখানে database transaction/locking ব্যবহার করতে হবে।

```text
A2
 ↓
locked
 ↓
User A → success
User B → reject
```

---

# 💳 Payment Flow

```text
Booking
   ↓
Payment
   ↓
Gateway
   ↓
Success
   ↓
Atomic Transaction
   │
   ├── Payment = successful
   ├── Booking = confirmed
   ├── Ticket inventory = sold
   ├── Ticket = issued
   └── Ticket QR generated
```

**একটা operation fail হলে পুরো transaction rollback** করা উচিত।

---

# 🔐 Important Constraints

সবচেয়ে গুরুত্বপূর্ণ constraints:

```text
Organization
    Unique(slug)

OrganizationMember
    Unique(organization, user)

Venue
    Unique(organization, code)

VenueHall
    Unique(venue, code)

VenueSeat
    Unique(hall, row, seat_number)

Event
    Unique(organization, slug)

EventOrganizer
    Unique(event, user)

SessionSpeaker
    Unique(session, speaker)

TicketType
    Unique(event, code)

TicketInventory
    Unique(ticket_type)

Booking
    Unique(booking_number)

Ticket
    Unique(ticket_number)
    Unique(qr_code)

Payment
    Unique(transaction_id)

Coupon
    Unique(organization, code)

CouponUsage
    Unique(coupon, booking)

WishlistEvent
    Unique(wishlist, event)

WaitlistEntry
    Unique(waitlist, customer)

IdempotencyRecord
    Unique(organization, key)
```

---

# 📊 Important Indexes

### Event

```text
organization + status
category + status
start_datetime
venue + start_datetime
booking_start + booking_end
```

### Booking

```text
customer + created_at
event + status
status + created_at
```

### Ticket

```text
ticket_type + status
booking + status
event + status
qr_code
```

### Payment

```text
booking + status
status + created_at
transaction_id
```

### Check-in

```text
event + checked_in_at
ticket + checked_in_at
```

### Waitlist

```text
event + status
ticket_type + status
position
```

---

# 🧠 Production Business Rules

### Rule 1 — Event capacity

```text
Total confirmed tickets
<=
Event capacity
```

### Rule 2 — Ticket inventory

```text
sold + reserved
<=
total_quantity
```

### Rule 3 — Booking expiration

ধরি user payment page-এ গেল।

```text
expires_at = now + 10 minutes
```

Payment না হলে:

```text
Booking → expired
Reservation → released
Inventory → available
```

---

### Rule 4 — Ticket একবার check-in

```text
Ticket status = used
```

হলে আবার scan করলে:

```text
Already Checked In
```

---

### Rule 5 — Refund

```text
Refund amount
<=
Paid amount
```

---

### Rule 6 — Coupon

Check করবে:

```text
current_date
minimum_order
usage_limit
customer_usage
event eligibility
```

---

# 📱 Recommended Django App Structure

```text
event_booking/
│
├── accounts/
├── organizations/
├── venues/
├── events/
├── speakers/
├── sessions/
├── tickets/
├── bookings/
├── payments/
├── refunds/
├── coupons/
├── customers/
├── reviews/
├── wishlist/
├── notifications/
├── commissions/
├── payouts/
├── waitlist/
├── reservations/
├── audit/
└── core/
```

---

# 🚀 Implementation Phases

## Phase 1 — Organization + Venue

```text
BaseModel
Organization
OrganizationMember
Venue
VenueAddress
VenueHall
VenueSeat
```

## Phase 2 — Event

```text
EventCategory
Event
EventImage
EventOrganizer
```

## Phase 3 — Session

```text
Speaker
EventSession
SessionSpeaker
```

## Phase 4 — Ticket

```text
TicketType
TicketTier
TicketInventory
```

## Phase 5 — Customer + Booking ⭐

```text
CustomerProfile
CustomerAddress
Booking
BookingItem
BookingAttendee
```

## Phase 6 — Payment

```text
PaymentMethod
Payment
```

## Phase 7 — Ticket Issuing

```text
Ticket
TicketTransfer
TicketCheckIn
```

## Phase 8 — Refund + Coupon

```text
Refund
RefundItem
Coupon
CouponUsage
```

## Phase 9 — Advanced

```text
Waitlist
WaitlistEntry
SeatingReservation
EventReview
Wishlist
WishlistEvent
```

## Phase 10 — Marketplace/Production

```text
EventCommission
OrganizerPayout
OrganizerPayoutItem
Notification
BookingStatusHistory
IdempotencyRecord
AuditLog
```

---

# ⭐ এই Project দিয়ে যে Advanced Django ORM Topics Practice হবে

তোমার আগের ORM learning-এর সাথে এই projectটা খুব ভালোভাবে connect করবে:

```text
select_related()
prefetch_related()
Prefetch()

annotate()
aggregate()

Count()
Sum()
Avg()
Min()
Max()

Q()
F()
Case()
When()

Exists()
Subquery()
OuterRef()

transaction.atomic()

select_for_update()

UniqueConstraint

CheckConstraint

Conditional UniqueConstraint

Composite Index

Pagination

EXPLAIN

Concurrency

Idempotency

Soft Delete

Audit Logging
```

বিশেষ করে **Ticket Inventory + SeatingReservation + Booking + Payment** অংশে তুমি বাস্তব-world concurrency problem practice করতে পারবে।

### সবচেয়ে গুরুত্বপূর্ণ architecture

```text
EVENT
  ↓
TICKET TYPE
  ↓
INVENTORY
  ↓
RESERVATION
  ↓
BOOKING
  ↓
PAYMENT
  ↓
TICKET
  ↓
CHECK-IN
  ↓
SETTLEMENT
```

এটাই এই project-এর **core business architecture**।



----
