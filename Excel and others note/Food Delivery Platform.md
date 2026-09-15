
অবশ্যই। এবার **Food Delivery Platform**-এর জন্যও আগেরগুলোর মতো **production-level complete model architecture** দিচ্ছি। এটাকে **Foodpanda / Uber Eats-style multi-vendor food delivery platform** হিসেবে design করছি।

এখানে থাকবে:

**Customer → Restaurant → Menu → Cart → Order → Payment → Restaurant Preparation → Delivery → Rider → Review → Commission → Payout**

---

# 🍔 Food Delivery Platform — Complete Models

## Core Models

1. `BaseModel`
    
2. `CustomerProfile`
    
3. `Restaurant`
    
4. `RestaurantMembership`
    
5. `RestaurantBranch`
    
6. `RestaurantImage`
    
7. `RestaurantAmenity`
    
8. `Cuisine`
    
9. `RestaurantCuisine`
    
10. `DeliveryZone`
    
11. `DeliveryAddress`
    
12. `DeliveryFeeRule`
    
13. `MenuCategory`
    
14. `MenuItem`
    
15. `MenuItemImage`
    
16. `MenuItemOptionGroup`
    
17. `MenuItemOption`
    
18. `MenuItemAddon`
    
19. `MenuItemAddonGroup`
    
20. `Cart`
    
21. `CartItem`
    
22. `CartItemOption`
    
23. `Coupon`
    
24. `CouponUsage`
    
25. `Order`
    
26. `OrderItem`
    
27. `OrderItemOption`
    
28. `OrderStatusHistory`
    
29. `Payment`
    
30. `Refund`
    
31. `DeliveryPartner`
    
32. `DeliveryPartnerVehicle`
    
33. `DeliveryAssignment`
    
34. `DeliveryTracking`
    
35. `RestaurantReview`
    
36. `DeliveryReview`
    
37. `FavoriteRestaurant`
    
38. `FavoriteMenuItem`
    
39. `RestaurantCommission`
    
40. `RestaurantPayout`
    
41. `Notification`
    
42. `Conversation`
    
43. `Message`
    
44. `SupportTicket`
    
45. `SupportMessage`
    
46. `IdempotencyRecord`
    
47. `AuditLog`
    

---

# 1. BaseModel

সব model-এর common fields:

```text
BaseModel
├── id
├── created_at
├── updated_at
├── is_active
└── deleted_at
```

---

# 2. CustomerProfile

Customer-এর additional information।

```text
CustomerProfile
├── user
├── phone
├── profile_image
├── date_of_birth
├── default_address
├── total_orders
├── total_spent
└── is_verified
```

Relationship:

```text
User
  ↓
CustomerProfile
  ├── Addresses
  ├── Cart
  ├── Orders
  └── Reviews
```

---

# 3. Restaurant ⭐

Platform-এর main vendor।

```text
Restaurant
├── owner
├── name
├── slug
├── description
├── logo
├── cover_image
├── phone
├── email
├── status
├── minimum_order_amount
├── average_preparation_time
├── rating
├── total_reviews
├── is_verified
└── is_active
```

Status:

```text
pending
approved
suspended
closed
```

---

# 4. RestaurantMembership

এক restaurant-এ multiple staff/admin থাকতে পারে।

```text
RestaurantMembership
├── restaurant
├── user
├── role
├── joined_at
└── is_active
```

Roles:

```text
owner
manager
staff
```

Constraint:

```text
Unique(restaurant, user)
```

---

# 5. RestaurantBranch

এক restaurant-এর multiple branches থাকতে পারে।

```text
RestaurantBranch
├── restaurant
├── name
├── address
├── city
├── latitude
├── longitude
├── phone
├── opening_time
├── closing_time
├── is_open
└── is_active
```

Example:

```text
Pizza House
├── Dhanmondi Branch
├── Mirpur Branch
└── Uttara Branch
```

---

# 6. RestaurantImage

```text
RestaurantImage
├── restaurant
├── image
├── caption
└── sort_order
```

---

# 7. RestaurantAmenity

Restaurant facilities।

```text
RestaurantAmenity
├── restaurant
├── name
└── is_active
```

Examples:

```text
WiFi
Parking
Outdoor Seating
AC
```

---

# 8. Cuisine

Global cuisine catalog।

```text
Cuisine
├── name
├── slug
└── is_active
```

Examples:

```text
Bangladeshi
Chinese
Indian
Italian
Thai
Fast Food
```

---

# 9. RestaurantCuisine

Restaurant কোন ধরনের খাবার serve করে।

```text
RestaurantCuisine
├── restaurant
├── cuisine
└── is_primary
```

Constraint:

```text
Unique(restaurant, cuisine)
```

---

# 10. DeliveryZone

Restaurant কোন geographic area-তে delivery দেয়।

```text
DeliveryZone
├── restaurant
├── name
├── description
├── delivery_radius
├── is_active
```

Production version-এ geographic polygon/geospatial data ব্যবহার করা যায়।

---

# 11. DeliveryAddress

Customer-এর saved delivery addresses।

```text
DeliveryAddress
├── customer
├── label
├── address_line
├── city
├── postal_code
├── latitude
├── longitude
├── delivery_instruction
└── is_default
```

Example:

```text
Home
Office
University
```

---

# 12. DeliveryFeeRule

Distance/order amount অনুযায়ী delivery fee।

```text
DeliveryFeeRule
├── restaurant
├── min_distance
├── max_distance
├── base_fee
├── per_km_fee
├── minimum_order
└── is_active
```

Example:

```text
0–2 km  → ৳30
2–5 km  → ৳50
5–8 km  → ৳70
```

---

# 🍕 MENU SYSTEM

# 13. MenuCategory

```text
MenuCategory
├── restaurant
├── name
├── description
├── sort_order
└── is_active
```

Example:

```text
Pizza
Burgers
Drinks
Desserts
```

---

# 14. MenuItem ⭐

Actual food item।

```text
MenuItem
├── restaurant
├── category
├── name
├── description
├── price
├── discount_price
├── preparation_time
├── calories
├── is_vegetarian
├── is_available
├── is_featured
└── sort_order
```

Example:

```text
Chicken Burger
Regular Price: ৳250
Discount Price: ৳220
```

---

# 15. MenuItemImage

```text
MenuItemImage
├── menu_item
├── image
└── sort_order
```

---

# 16. MenuItemOptionGroup

Customer food customize করতে পারবে।

```text
MenuItemOptionGroup
├── menu_item
├── name
├── min_selection
├── max_selection
└── is_required
```

Example:

```text
Choose Size
├── Small
├── Medium
└── Large
```

---

# 17. MenuItemOption

```text
MenuItemOption
├── group
├── name
├── extra_price
└── is_available
```

Example:

```text
Medium → +৳30
Large  → +৳60
```

---

# 18. MenuItemAddonGroup

Optional add-ons।

```text
MenuItemAddonGroup
├── menu_item
├── name
├── min_selection
├── max_selection
└── is_required
```

---

# 19. MenuItemAddon

```text
MenuItemAddon
├── group
├── name
├── price
└── is_available
```

Example:

```text
Extra Cheese → ৳50
Extra Sauce  → ৳20
```

---

# 🛒 CART

# 20. Cart

```text
Cart
├── customer
├── restaurant
├── subtotal
├── delivery_fee
├── discount
├── total
└── updated_at
```

### Important

এক Cart-এ সাধারণত **এক restaurant-এর item** থাকবে।

```text
Cart
  ↓
Restaurant A
  ├── Burger
  ├── Pizza
  └── Coke
```

Multiple restaurant order হলে checkout architecture আলাদাভাবে design করতে হবে।

---

# 21. CartItem

```text
CartItem
├── cart
├── menu_item
├── quantity
├── unit_price
└── total_price
```

---

# 22. CartItemOption

Selected customization।

```text
CartItemOption
├── cart_item
├── option
├── quantity
└── extra_price
```

---

# 🎟️ COUPON

# 23. Coupon

```text
Coupon
├── code
├── discount_type
├── discount_value
├── minimum_order
├── maximum_discount
├── usage_limit
├── used_count
├── start_date
├── end_date
└── is_active
```

Types:

```text
percentage
fixed
free_delivery
```

---

# 24. CouponUsage

```text
CouponUsage
├── coupon
├── customer
├── order
├── discount_amount
└── used_at
```

---

# 📦 ORDER SYSTEM

# 25. Order ⭐⭐⭐

সবচেয়ে important model।

```text
Order
├── customer
├── restaurant
├── branch
├── delivery_address
├── order_number
├── subtotal
├── delivery_fee
├── service_fee
├── discount
├── tax
├── total_amount
├── payment_status
├── order_status
├── estimated_delivery_time
├── special_instruction
├── placed_at
├── accepted_at
├── prepared_at
├── picked_up_at
├── delivered_at
└── cancelled_at
```

Order status:

```text
pending
confirmed
preparing
ready
assigned
picked_up
on_the_way
delivered
cancelled
rejected
```

---

# 26. OrderItem

Order-এর snapshot of menu item।

```text
OrderItem
├── order
├── menu_item
├── item_name
├── unit_price
├── quantity
├── total_price
└── special_instruction
```

### Important

`item_name` এবং `unit_price` এখানে রাখার কারণ:

MenuItem পরে পরিবর্তন হলেও historical order-এর data পরিবর্তন হবে না।

---

# 27. OrderItemOption

Order-এর selected options-এর snapshot।

```text
OrderItemOption
├── order_item
├── option_name
├── extra_price
└── quantity
```

এখানেও historical snapshot রাখা হচ্ছে।

---

# 28. OrderStatusHistory

Order-এর state change tracking।

```text
OrderStatusHistory
├── order
├── status
├── changed_by
├── note
└── created_at
```

Example:

```text
10:00 pending
10:02 confirmed
10:05 preparing
10:25 ready
10:30 picked_up
10:50 delivered
```

---

# 💳 PAYMENT

# 29. Payment

```text
Payment
├── order
├── transaction_id
├── amount
├── payment_method
├── provider
├── status
├── paid_at
└── metadata
```

Payment methods:

```text
cash
card
mobile_banking
wallet
```

Status:

```text
pending
processing
completed
failed
refunded
```

এক order-এর multiple payment attempt থাকতে পারে।

---

# 30. Refund

```text
Refund
├── payment
├── order
├── amount
├── reason
├── refund_transaction_id
├── status
└── processed_at
```

---

# 🛵 DELIVERY PARTNER

# 31. DeliveryPartner ⭐

Rider-এর profile।

```text
DeliveryPartner
├── user
├── phone
├── profile_image
├── partner_id
├── status
├── current_latitude
├── current_longitude
├── rating
├── total_deliveries
└── is_verified
```

Status:

```text
offline
available
busy
suspended
```

---

# 32. DeliveryPartnerVehicle

```text
DeliveryPartnerVehicle
├── partner
├── vehicle_type
├── registration_number
├── model
└── is_active
```

Vehicle:

```text
bike
bicycle
car
```

---

# 33. DeliveryAssignment ⭐

Order কে কোন rider deliver করবে।

```text
DeliveryAssignment
├── order
├── delivery_partner
├── assigned_at
├── accepted_at
├── rejected_at
├── picked_up_at
├── delivered_at
├── status
└── notes
```

Status:

```text
pending
accepted
rejected
picked_up
on_the_way
delivered
cancelled
```

---

# 34. DeliveryTracking

Live location/history।

```text
DeliveryTracking
├── assignment
├── latitude
├── longitude
├── recorded_at
└── status
```

Example:

```text
Rider
 ↓
23.7465, 90.3760
 ↓
23.7501, 90.3850
 ↓
23.7550, 90.3900
```

Real-time application হলে এখানে WebSocket + Redis ব্যবহার করা যেতে পারে।

---

# ⭐ REVIEWS

# 35. RestaurantReview

```text
RestaurantReview
├── customer
├── restaurant
├── order
├── rating
├── comment
└── is_public
```

Production rule:

```text
Only delivered order
→ customer can review restaurant
```

---

# 36. DeliveryReview

Rider-এর review।

```text
DeliveryReview
├── customer
├── delivery_partner
├── order
├── rating
├── comment
└── is_public
```

---

# ❤️ FAVORITES

# 37. FavoriteRestaurant

```text
FavoriteRestaurant
├── customer
├── restaurant
└── created_at
```

Constraint:

```text
Unique(customer, restaurant)
```

---

# 38. FavoriteMenuItem

```text
FavoriteMenuItem
├── customer
├── menu_item
└── created_at
```

Constraint:

```text
Unique(customer, menu_item)
```

---

# 💰 RESTAURANT FINANCE

# 39. RestaurantCommission

Platform commission।

```text
RestaurantCommission
├── restaurant
├── order
├── gross_amount
├── commission_rate
├── commission_amount
└── restaurant_amount
```

Example:

```text
Order = ৳1000

Platform = 15%
Commission = ৳150

Restaurant = ৳850
```

---

# 40. RestaurantPayout

Restaurant-এর settlement।

```text
RestaurantPayout
├── restaurant
├── amount
├── payout_method
├── transaction_id
├── status
├── period_start
├── period_end
├── requested_at
└── processed_at
```

---

# 🔔 NOTIFICATION

# 41. Notification

```text
Notification
├── user
├── title
├── message
├── notification_type
├── reference_type
├── reference_id
├── is_read
└── created_at
```

Examples:

```text
Order Confirmed
Food is ready
Rider assigned
Order delivered
Payment successful
```

---

# 💬 CHAT

# 42. Conversation

```text
Conversation
├── order
├── customer
├── restaurant
├── delivery_partner
├── created_at
└── last_message_at
```

---

# 43. Message

```text
Message
├── conversation
├── sender
├── message
├── attachment
├── is_read
└── created_at
```

---

# 🎧 SUPPORT

# 44. SupportTicket

```text
SupportTicket
├── user
├── order
├── subject
├── category
├── priority
├── status
└── resolved_at
```

Status:

```text
open
in_progress
resolved
closed
```

---

# 45. SupportMessage

```text
SupportMessage
├── ticket
├── sender
├── message
├── attachment
└── created_at
```

---

# 🔐 PRODUCTION

# 46. IdempotencyRecord

Payment/order API duplicate request prevent করার জন্য।

```text
IdempotencyRecord
├── key
├── user
├── endpoint
├── status
├── response_data
└── created_at
```

---

# 47. AuditLog

```text
AuditLog
├── user
├── action
├── model_name
├── object_id
├── old_data
├── new_data
├── ip_address
└── created_at
```

---

# 🔗 Complete Relationship Diagram

```text
                              USER
                  ┌────────────┼─────────────┐
                  │            │             │
              CUSTOMER     RESTAURANT       RIDER
                  │            │             │
                  │            │             ├── Vehicle
                  │            │             │
                  │        Restaurant        │
                  │          Branch          │
                  │            │             │
                  │         Menu             │
                  │            │             │
                  │       MenuCategory       │
                  │            │             │
                  │        MenuItem           │
                  │            │
                  │        Options            │
                  │            │
                  ↓            │
              DELIVERY         │
              ADDRESS          │
                  │            │
                  └──────┬─────┘
                         ↓
                        CART
                         │
                    CartItem
                         │
                         ↓
                       ORDER
                         │
          ┌──────────────┼──────────────┐
          │              │              │
      OrderItem       Payment       Assignment
          │              │              │
       Options         Refund       DeliveryPartner
                                         │
                                   DeliveryTracking
          
ORDER
  │
  ├── StatusHistory
  ├── RestaurantReview
  ├── DeliveryReview
  ├── Commission
  ├── CouponUsage
  ├── Conversation
  └── SupportTicket
```

---

# 🔄 Complete Order Lifecycle

এটাই project-এর সবচেয়ে important business flow:

```text
Customer
   ↓
Browse Restaurants
   ↓
Select Restaurant
   ↓
Browse Menu
   ↓
Add Items
   ↓
Customize Items
   ↓
Cart
   ↓
Apply Coupon
   ↓
Select Address
   ↓
Calculate Delivery Fee
   ↓
Place Order
   ↓
Payment
   ↓
Restaurant Accepts
   ↓
Preparing
   ↓
Food Ready
   ↓
Rider Assigned
   ↓
Rider Picks Up
   ↓
On The Way
   ↓
Delivered
   ↓
Review
   ↓
Restaurant Settlement
```

---

# 💳 Payment Flow

Production system-এ:

```text
Customer
   ↓
Payment
   ↓
Payment Provider
   ↓
Payment Success
   ↓
Order Confirmed
   ↓
Restaurant prepares food
   ↓
Delivery completed
   ↓
Commission calculation
   ↓
Restaurant balance
   ↓
Restaurant payout
```

Payment success-এর আগে order-কে paid ধরে নেওয়া যাবে না।

---

# 🧮 Order Calculation

ধরো:

```text
Burger       ৳300
Pizza        ৳500
Drinks       ৳100
------------------
Subtotal     ৳900

Delivery     ৳60
Service Fee  ৳30
Discount    -৳100
Tax          ৳45
------------------
Total        ৳935
```

Production-এ এই calculation server-side করতে হবে।

Client থেকে:

```text
total = 100
```

পাঠালেই সেটা trust করা যাবে না।

---

# 🚨 Important Race Conditions

এই project তোমার concurrency শেখার জন্য খুব ভালো।

## 1. Same order payment twice

```text
Request A → payment
Request B → payment
```

দুটো request একই payment process করলে duplicate charge হতে পারে।

Solution:

```text
Idempotency Key
+
Database Transaction
+
Payment Provider Transaction ID
```

---

## 2. Rider assignment race

ধরো:

```text
Rider A → available
Rider B → available
```

দুইজন একই order accept করতে চাইছে।

```text
Order
 ↓
select_for_update()
 ↓
assign rider
```

ব্যবহার করা যায়।

---

## 3. Menu availability race

ধরো restaurant একটি item temporarily unavailable করেছে, কিন্তু customer একই সময়ে checkout করছে।

তাই checkout-এর সময় আবার server-side availability validate করতে হবে।

---

# 📌 Important Database Constraints

### Restaurant membership

```text
Unique(restaurant, user)
```

### Restaurant cuisine

```text
Unique(restaurant, cuisine)
```

### Favorite restaurant

```text
Unique(customer, restaurant)
```

### Favorite item

```text
Unique(customer, menu_item)
```

### Payment transaction

```text
transaction_id UNIQUE
```

### Coupon

```text
code UNIQUE
```

### Restaurant branch

```text
Unique(restaurant, name)
```

### Menu category

```text
Unique(restaurant, name)
```

---

# 📊 Important Indexes

## Restaurant

```text
status
is_verified
city
rating
```

## MenuItem

```text
restaurant
category
is_available
is_featured
```

## Order

```text
customer + created_at
restaurant + created_at
status + created_at
payment_status
```

## DeliveryAssignment

```text
delivery_partner + status
order
status
```

## DeliveryTracking

```text
assignment + recorded_at
```

## Payment

```text
order
status
created_at
transaction_id
```

---

# 🏢 Recommended Django Apps

সব model একটা app-এ না রাখাই ভালো।

```text
food_delivery/
│
├── accounts/
├── customers/
├── restaurants/
├── cuisines/
├── menu/
├── delivery_zones/
├── carts/
├── orders/
├── payments/
├── delivery/
├── reviews/
├── coupons/
├── commissions/
├── payouts/
├── messaging/
├── support/
├── notifications/
└── audit/
```

---

# 🚀 Implementation Phases

### Phase 1 — Accounts

```text
BaseModel
CustomerProfile
```

### Phase 2 — Restaurant

```text
Restaurant
RestaurantMembership
RestaurantBranch
RestaurantImage
RestaurantAmenity
Cuisine
RestaurantCuisine
```

### Phase 3 — Menu

```text
MenuCategory
MenuItem
MenuItemImage
MenuItemOptionGroup
MenuItemOption
MenuItemAddonGroup
MenuItemAddon
```

### Phase 4 — Location & Cart

```text
DeliveryAddress
DeliveryZone
DeliveryFeeRule
Cart
CartItem
CartItemOption
```

### Phase 5 — Order

```text
Order
OrderItem
OrderItemOption
OrderStatusHistory
```

### Phase 6 — Payment

```text
Payment
Refund
Coupon
CouponUsage
```

### Phase 7 — Delivery

```text
DeliveryPartner
DeliveryPartnerVehicle
DeliveryAssignment
DeliveryTracking
```

### Phase 8 — Review & Finance

```text
RestaurantReview
DeliveryReview
RestaurantCommission
RestaurantPayout
```

### Phase 9 — Communication

```text
Conversation
Message
Notification
SupportTicket
SupportMessage
```

### Phase 10 — Production

```text
IdempotencyRecord
AuditLog
```

---

# 🧠 এই Project দিয়ে ORM Practice

Food Delivery project দিয়ে তুমি প্রায় পুরো advanced Django ORM practice করতে পারবে:

```text
filter()
exclude()
get()
create()
update()

select_related()
prefetch_related()
Prefetch()

Count()
Sum()
Avg()
Min()
Max()

annotate()
aggregate()

Q()
F()

Case()
When()

Exists()
Subquery()
OuterRef()

Window()

transaction.atomic()

select_for_update()

UniqueConstraint
CheckConstraint

Index
Composite Index

EXPLAIN
Query Optimization

Pagination

Soft Delete

Audit Logging

Idempotency

Concurrency
```

### বিশেষ করে ৫টা বিষয় এখানে খুব ভালোভাবে practice করবে

```text
1. Cart → Order conversion
2. Order state machine
3. Payment idempotency
4. Rider assignment concurrency
5. Restaurant commission + payout
```

এই project-টা **Job Marketplace-এর পাশাপাশি তোমার database designer skill-এর জন্য খুব strong project**, কারণ এখানে relational modeling-এর সাথে **transaction, concurrency, financial consistency, location, real-time tracking এবং high-volume order queries**—সব একসাথে আসে।



----
হ্যাঁ। এবার আগের **E-commerce project-এর মতো শুধু model architecture না**, বরং **Food Delivery Platform-এর complete model list + প্রতিটি model-এর important fields + relationships** একসাথে দিচ্ছি।

এটা **multi-vendor Food Delivery** ধরে design করা হয়েছে।

# 🍔 Food Delivery Platform — Complete Models

মোট **47টি core model**:

```text
1.  BaseModel
2.  CustomerProfile
3.  Restaurant
4.  RestaurantMembership
5.  RestaurantBranch
6.  RestaurantImage
7.  RestaurantAmenity
8.  Cuisine
9.  RestaurantCuisine
10. DeliveryZone
11. DeliveryAddress

12. MenuCategory
13. MenuItem
14. MenuItemImage
15. MenuItemOptionGroup
16. MenuItemOption
17. MenuItemAddonGroup
18. MenuItemAddon

19. Cart
20. CartItem
21. CartItemOption

22. Coupon
23. CouponUsage

24. Order
25. OrderItem
26. OrderItemOption
27. OrderStatusHistory

28. Payment
29. Refund

30. DeliveryPartner
31. DeliveryPartnerVehicle
32. DeliveryAssignment
33. DeliveryTracking

34. RestaurantReview
35. DeliveryReview

36. FavoriteRestaurant
37. FavoriteMenuItem

38. RestaurantCommission
39. RestaurantPayout

40. Notification

41. Conversation
42. Message

43. SupportTicket
44. SupportMessage

45. IdempotencyRecord
46. AuditLog

47. DeliveryFeeRule
```

---

# 1. BaseModel

সব model-এর common parent.

```python
class BaseModel(models.Model):
    id
    created_at
    updated_at
    is_active
    deleted_at
```

---

# 👤 CUSTOMER

## 2. CustomerProfile

```text
CustomerProfile
├── user
├── phone
├── profile_image
├── date_of_birth
├── total_orders
├── total_spent
└── is_verified
```

Relationship:

```text
User
 ↓
CustomerProfile
 ├── DeliveryAddress
 ├── Cart
 ├── Order
 ├── Review
 └── Favorite
```

---

# 🏪 RESTAURANT

## 3. Restaurant

Main vendor.

```text
Restaurant
├── owner
├── name
├── slug
├── description
├── logo
├── cover_image
├── phone
├── email
├── status
├── minimum_order_amount
├── average_preparation_time
├── rating
├── total_reviews
├── is_verified
└── is_active
```

Status:

```text
pending
approved
suspended
closed
```

---

## 4. RestaurantMembership

Restaurant owner/manager/staff.

```text
RestaurantMembership
├── restaurant
├── user
├── role
├── joined_at
└── is_active
```

Roles:

```text
owner
manager
staff
```

Constraint:

```text
Unique(restaurant, user)
```

---

## 5. RestaurantBranch

এক restaurant-এর multiple branch.

```text
RestaurantBranch
├── restaurant
├── name
├── address
├── city
├── latitude
├── longitude
├── phone
├── opening_time
├── closing_time
├── is_open
└── is_active
```

Example:

```text
Pizza House
├── Dhanmondi Branch
├── Uttara Branch
└── Mirpur Branch
```

---

## 6. RestaurantImage

```text
RestaurantImage
├── restaurant
├── image
├── caption
└── sort_order
```

---

## 7. RestaurantAmenity

```text
RestaurantAmenity
├── restaurant
├── name
└── is_active
```

Example:

```text
WiFi
Parking
AC
Outdoor Seating
```

---

## 8. Cuisine

Global cuisine.

```text
Cuisine
├── name
├── slug
└── is_active
```

Example:

```text
Bangladeshi
Chinese
Indian
Italian
Thai
Fast Food
```

---

## 9. RestaurantCuisine

Restaurant কোন cuisine-এর।

```text
RestaurantCuisine
├── restaurant
├── cuisine
└── is_primary
```

Constraint:

```text
Unique(restaurant, cuisine)
```

---

# 📍 LOCATION

## 10. DeliveryZone

```text
DeliveryZone
├── restaurant
├── name
├── description
├── delivery_radius
└── is_active
```

Example:

```text
Dhanmondi Zone
Mirpur Zone
Uttara Zone
```

---

## 11. DeliveryAddress

Customer-এর saved address.

```text
DeliveryAddress
├── customer
├── label
├── address_line
├── city
├── postal_code
├── latitude
├── longitude
├── delivery_instruction
└── is_default
```

Example:

```text
Home
Office
University
```

---

# 🍕 MENU SYSTEM

## 12. MenuCategory

```text
MenuCategory
├── restaurant
├── name
├── description
├── sort_order
└── is_active
```

Example:

```text
Pizza
Burger
Drinks
Dessert
```

---

## 13. MenuItem

Actual food product.

```text
MenuItem
├── restaurant
├── category
├── name
├── description
├── price
├── discount_price
├── preparation_time
├── calories
├── is_vegetarian
├── is_available
├── is_featured
└── sort_order
```

Example:

```text
Chicken Burger
price = 250
discount_price = 220
```

---

## 14. MenuItemImage

```text
MenuItemImage
├── menu_item
├── image
└── sort_order
```

---

## 15. MenuItemOptionGroup

Customer food customize করতে পারবে।

```text
MenuItemOptionGroup
├── menu_item
├── name
├── min_selection
├── max_selection
└── is_required
```

Example:

```text
Choose Size
├── Small
├── Medium
└── Large
```

---

## 16. MenuItemOption

```text
MenuItemOption
├── group
├── name
├── extra_price
└── is_available
```

Example:

```text
Medium → +30
Large  → +60
```

---

## 17. MenuItemAddonGroup

```text
MenuItemAddonGroup
├── menu_item
├── name
├── min_selection
├── max_selection
└── is_required
```

Example:

```text
Extra
├── Cheese
├── Sauce
└── Fries
```

---

## 18. MenuItemAddon

```text
MenuItemAddon
├── group
├── name
├── price
└── is_available
```

---

# 🛒 CART

## 19. Cart

```text
Cart
├── customer
├── restaurant
├── subtotal
├── delivery_fee
├── discount
├── total
└── updated_at
```

### Important

একটি cart সাধারণত একটি restaurant-এর হবে।

```text
Cart
 ↓
Restaurant A
 ├── Burger
 ├── Pizza
 └── Coke
```

---

## 20. CartItem

```text
CartItem
├── cart
├── menu_item
├── quantity
├── unit_price
└── total_price
```

---

## 21. CartItemOption

```text
CartItemOption
├── cart_item
├── option
├── quantity
└── extra_price
```

---

# 🎟️ COUPON

## 22. Coupon

```text
Coupon
├── code
├── discount_type
├── discount_value
├── minimum_order
├── maximum_discount
├── usage_limit
├── used_count
├── start_date
├── end_date
└── is_active
```

Types:

```text
percentage
fixed
free_delivery
```

---

## 23. CouponUsage

```text
CouponUsage
├── coupon
├── customer
├── order
├── discount_amount
└── used_at
```

---

# 📦 ORDER

## 24. Order ⭐

সবচেয়ে গুরুত্বপূর্ণ model.

```text
Order
├── customer
├── restaurant
├── branch
├── delivery_address
├── order_number
├── subtotal
├── delivery_fee
├── service_fee
├── discount
├── tax
├── total_amount
├── payment_status
├── order_status
├── estimated_delivery_time
├── special_instruction
├── placed_at
├── accepted_at
├── prepared_at
├── picked_up_at
├── delivered_at
└── cancelled_at
```

### Order Status

```text
pending
confirmed
preparing
ready
assigned
picked_up
on_the_way
delivered
cancelled
rejected
```

---

## 25. OrderItem

Order-এর historical snapshot.

```text
OrderItem
├── order
├── menu_item
├── item_name
├── unit_price
├── quantity
├── total_price
└── special_instruction
```

### কেন `item_name` আবার রাখছি?

ধরো:

```text
আজ:
Burger = ৳200
```

এক মাস পরে restaurant price change করল:

```text
Burger = ৳300
```

পুরোনো order-এ কিন্তু ৳200-ই থাকতে হবে।

তাই OrderItem-এ snapshot রাখা হয়।

---

## 26. OrderItemOption

```text
OrderItemOption
├── order_item
├── option_name
├── extra_price
└── quantity
```

এটাও historical snapshot.

---

## 27. OrderStatusHistory

```text
OrderStatusHistory
├── order
├── status
├── changed_by
├── note
└── created_at
```

Example:

```text
10:00 pending
10:02 confirmed
10:05 preparing
10:25 ready
10:30 picked_up
10:50 delivered
```

---

# 💳 PAYMENT

## 28. Payment

```text
Payment
├── order
├── transaction_id
├── amount
├── payment_method
├── provider
├── status
├── paid_at
└── metadata
```

Payment method:

```text
cash
card
mobile_banking
wallet
```

Status:

```text
pending
processing
completed
failed
refunded
```

---

## 29. Refund

```text
Refund
├── payment
├── order
├── amount
├── reason
├── refund_transaction_id
├── status
└── processed_at
```

---

# 🛵 DELIVERY

## 30. DeliveryPartner

Rider.

```text
DeliveryPartner
├── user
├── partner_id
├── phone
├── profile_image
├── status
├── current_latitude
├── current_longitude
├── rating
├── total_deliveries
└── is_verified
```

Status:

```text
offline
available
busy
suspended
```

---

## 31. DeliveryPartnerVehicle

```text
DeliveryPartnerVehicle
├── partner
├── vehicle_type
├── registration_number
├── model
└── is_active
```

---

## 32. DeliveryAssignment

কোন order কে deliver করবে।

```text
DeliveryAssignment
├── order
├── delivery_partner
├── assigned_at
├── accepted_at
├── rejected_at
├── picked_up_at
├── delivered_at
├── status
└── notes
```

---

## 33. DeliveryTracking

Rider-এর location history.

```text
DeliveryTracking
├── assignment
├── latitude
├── longitude
├── recorded_at
└── status
```

Production system-এ এখানে অনেক data তৈরি হতে পারে, তাই indexing/retention strategy গুরুত্বপূর্ণ।

---

# ⭐ REVIEW

## 34. RestaurantReview

```text
RestaurantReview
├── customer
├── restaurant
├── order
├── rating
├── comment
└── is_public
```

Business rule:

```text
Only delivered order
→ Review allowed
```

---

## 35. DeliveryReview

```text
DeliveryReview
├── customer
├── delivery_partner
├── order
├── rating
├── comment
└── is_public
```

---

# ❤️ FAVORITES

## 36. FavoriteRestaurant

```text
FavoriteRestaurant
├── customer
├── restaurant
└── created_at
```

```text
Unique(customer, restaurant)
```

---

## 37. FavoriteMenuItem

```text
FavoriteMenuItem
├── customer
├── menu_item
└── created_at
```

```text
Unique(customer, menu_item)
```

---

# 💰 RESTAURANT FINANCE

## 38. RestaurantCommission

Platform commission.

```text
RestaurantCommission
├── restaurant
├── order
├── gross_amount
├── commission_rate
├── commission_amount
└── restaurant_amount
```

Example:

```text
Order = ৳1000

Commission = 15%

Platform = ৳150
Restaurant = ৳850
```

---

## 39. RestaurantPayout

Restaurant settlement.

```text
RestaurantPayout
├── restaurant
├── amount
├── payout_method
├── transaction_id
├── status
├── period_start
├── period_end
├── requested_at
└── processed_at
```

---

# 🔔 NOTIFICATION

## 40. Notification

```text
Notification
├── user
├── title
├── message
├── notification_type
├── reference_type
├── reference_id
├── is_read
└── created_at
```

Examples:

```text
Order confirmed
Food ready
Rider assigned
Payment successful
Order delivered
```

---

# 💬 MESSAGING

## 41. Conversation

```text
Conversation
├── order
├── customer
├── restaurant
├── delivery_partner
├── last_message_at
└── is_active
```

---

## 42. Message

```text
Message
├── conversation
├── sender
├── message
├── attachment
├── is_read
└── created_at
```

---

# 🎧 SUPPORT

## 43. SupportTicket

```text
SupportTicket
├── user
├── order
├── subject
├── category
├── priority
├── status
└── resolved_at
```

Status:

```text
open
in_progress
resolved
closed
```

---

## 44. SupportMessage

```text
SupportMessage
├── ticket
├── sender
├── message
├── attachment
└── created_at
```

---

# 🔐 PRODUCTION MODELS

## 45. IdempotencyRecord

Duplicate API request prevent করার জন্য।

```text
IdempotencyRecord
├── key
├── user
├── endpoint
├── status
├── response_data
└── created_at
```

বিশেষ করে:

```text
Payment
Order creation
Refund
Payout
```

এর ক্ষেত্রে গুরুত্বপূর্ণ।

---

## 46. AuditLog

সব গুরুত্বপূর্ণ action-এর history।

```text
AuditLog
├── user
├── action
├── model_name
├── object_id
├── old_data
├── new_data
├── ip_address
└── created_at
```

---

# 🚚 DELIVERY FEE

## 47. DeliveryFeeRule

Distance অনুযায়ী delivery charge।

```text
DeliveryFeeRule
├── restaurant
├── min_distance
├── max_distance
├── base_fee
├── per_km_fee
├── minimum_order
└── is_active
```

Example:

```text
0–2 km   → ৳30
2–5 km   → ৳50
5–8 km   → ৳70
```

---

# 🔗 পুরো System Relationship

```text
                              USER
                 ┌─────────────┼─────────────┐
                 │             │             │
              CUSTOMER     RESTAURANT      RIDER
                 │             │             │
                 │             │             └── Vehicle
                 │             │
                 │          Branch
                 │             │
                 │           Menu
                 │             │
                 │        MenuCategory
                 │             │
                 │          MenuItem
                 │             │
                 │      ┌──────┴──────┐
                 │      │             │
                 │    Option        Addon
                 │
                 ├── Address
                 │
                 └── Cart
                      │
                   CartItem
                      │
                      ↓
                    ORDER
                      │
       ┌──────────────┼────────────────┐
       │              │                │
   OrderItem       Payment        Assignment
       │              │                │
    Options         Refund          Rider
                                      │
                                Tracking
                      │
          ┌───────────┼────────────┐
          │           │            │
        Review      Coupon       Commission
                                   │
                                Payout
```

---

# 🔄 Main Business Flow

```text
Customer
   ↓
Restaurant Browse
   ↓
Menu Browse
   ↓
Add to Cart
   ↓
Customize Food
   ↓
Apply Coupon
   ↓
Select Address
   ↓
Calculate Delivery Fee
   ↓
Place Order
   ↓
Payment
   ↓
Restaurant Accept
   ↓
Preparing
   ↓
Food Ready
   ↓
Rider Assigned
   ↓
Picked Up
   ↓
On The Way
   ↓
Delivered
   ↓
Review
   ↓
Restaurant Settlement
```

---

# 🏢 Recommended Django Apps

```text
food_delivery/
│
├── accounts/
├── customers/
├── restaurants/
├── cuisines/
├── menu/
├── delivery_zones/
├── carts/
├── orders/
├── payments/
├── delivery/
├── reviews/
├── coupons/
├── commissions/
├── payouts/
├── messaging/
├── support/
├── notifications/
└── audit/
```

---

# ⭐ সবচেয়ে Important Models

যদি প্রথমে পুরো 47টা model একসাথে implement না করো, এই **core 15টা** দিয়ে শুরু করো:

```text
1. CustomerProfile
2. Restaurant
3. RestaurantBranch
4. MenuCategory
5. MenuItem
6. MenuItemOption
7. DeliveryAddress
8. Cart
9. CartItem
10. Order
11. OrderItem
12. Payment
13. DeliveryPartner
14. DeliveryAssignment
15. RestaurantReview
```

তারপর ধাপে ধাপে:

```text
Core
 ↓
Coupon
 ↓
Delivery Tracking
 ↓
Commission
 ↓
Payout
 ↓
Chat
 ↓
Support
 ↓
Idempotency
 ↓
Audit
```

**এই model set-টা E-commerce-এর Product → Cart → Order → Payment flow-এর equivalent, কিন্তু Food Delivery-তে Restaurant → Menu → Cart → Order → Rider → Delivery → Settlement layer যোগ হয়েছে।**


---
হ্যাঁ, অবশ্যই। **শুধু model name না দিয়ে প্রতিটি model-এর actual field, field type, relationship, important constraint** দিলে তোমার জন্য অনেক বেশি useful হবে—বিশেষ করে তুমি যেহেতু Django ORM + database design practice করছো।

নিচে **Food Delivery Platform-এর production-style Django model blueprint** দিলাম। এটা সরাসরি copy-paste করার জন্য নয়; আগে architecture বুঝে তারপর Django models লিখলে ভালো হবে।

# 🍔 Food Delivery Platform — Complete Models + Fields

## 1. `BaseModel`

```python
BaseModel
├── id                  UUID / BigAutoField
├── created_at          DateTime
├── updated_at          DateTime
├── is_active           Boolean
└── deleted_at          DateTime NULL
```

---

# 👤 Customer

## 2. `CustomerProfile`

```python
CustomerProfile
├── id                  PK
├── user                OneToOne(User)
├── phone               CharField
├── profile_image       ImageField NULL
├── date_of_birth       DateField NULL
├── total_orders        PositiveIntegerField
├── total_spent         DecimalField
├── is_verified         BooleanField
├── created_at          DateTime
└── updated_at          DateTime
```

### Important

```text
user → PROTECT
total_orders → cached/derived
total_spent → cached/derived
```

---

# 🏪 Restaurant

## 3. `Restaurant`

```python
Restaurant
├── id                      PK
├── owner                   FK(User)
├── name                    CharField
├── slug                    SlugField
├── description             TextField
├── logo                    ImageField NULL
├── cover_image             ImageField NULL
├── phone                   CharField
├── email                   EmailField
├── address                 TextField
├── city                    CharField
├── latitude                DecimalField
├── longitude               DecimalField
├── minimum_order_amount    DecimalField
├── average_preparation_time PositiveIntegerField
├── rating                  DecimalField
├── total_reviews           PositiveIntegerField
├── status                  CharField
├── is_verified             BooleanField
└── is_active               BooleanField
```

### Status

```text
pending
approved
suspended
closed
```

### Constraints

```text
slug → UNIQUE
```

---

## 4. `RestaurantMembership`

```python
RestaurantMembership
├── id              PK
├── restaurant      FK(Restaurant)
├── user            FK(User)
├── role             CharField
├── joined_at        DateTime
└── is_active        Boolean
```

### Roles

```text
owner
manager
staff
```

### Constraint

```text
Unique(restaurant, user)
```

---

## 5. `RestaurantBranch`

```python
RestaurantBranch
├── id              PK
├── restaurant      FK(Restaurant)
├── name            CharField
├── address         TextField
├── city            CharField
├── latitude        DecimalField
├── longitude       DecimalField
├── phone            CharField
├── opening_time    TimeField
├── closing_time    TimeField
├── is_open         BooleanField
└── is_active       BooleanField
```

### Constraint

```text
Unique(restaurant, name)
```

---

## 6. `RestaurantImage`

```python
RestaurantImage
├── id              PK
├── restaurant      FK(Restaurant)
├── image           ImageField
├── caption         CharField NULL
└── sort_order      PositiveIntegerField
```

---

## 7. `RestaurantAmenity`

```python
RestaurantAmenity
├── id              PK
├── restaurant      FK(Restaurant)
├── name            CharField
└── is_active       BooleanField
```

Example:

```text
WiFi
Parking
AC
Outdoor Seating
```

---

# 🍜 Cuisine

## 8. `Cuisine`

```python
Cuisine
├── id              PK
├── name            CharField
├── slug            SlugField
└── is_active       BooleanField
```

Constraint:

```text
slug → UNIQUE
```

---

## 9. `RestaurantCuisine`

```python
RestaurantCuisine
├── id              PK
├── restaurant      FK(Restaurant)
├── cuisine         FK(Cuisine)
├── is_primary      BooleanField
└── created_at      DateTime
```

Constraint:

```text
Unique(restaurant, cuisine)
```

---

# 📍 Delivery Location

## 10. `DeliveryZone`

```python
DeliveryZone
├── id                  PK
├── restaurant          FK(Restaurant)
├── name                CharField
├── description         TextField NULL
├── min_distance_km    DecimalField
├── max_distance_km    DecimalField
├── is_active           BooleanField
└── created_at          DateTime
```

---

## 11. `DeliveryAddress`

```python
DeliveryAddress
├── id                    PK
├── customer              FK(CustomerProfile)
├── label                 CharField
├── address_line          TextField
├── apartment             CharField NULL
├── city                  CharField
├── postal_code           CharField NULL
├── latitude              DecimalField
├── longitude             DecimalField
├── delivery_instruction  TextField NULL
├── is_default            BooleanField
└── is_active             BooleanField
```

Example:

```text
label = "Home"
address_line = "Mirpur 10"
latitude = 23.xxxx
longitude = 90.xxxx
```

---

# 🍕 Menu

## 12. `MenuCategory`

```python
MenuCategory
├── id              PK
├── restaurant      FK(Restaurant)
├── name            CharField
├── description     TextField NULL
├── sort_order      PositiveIntegerField
└── is_active       BooleanField
```

Constraint:

```text
Unique(restaurant, name)
```

---

## 13. `MenuItem`

```python
MenuItem
├── id                  PK
├── restaurant          FK(Restaurant)
├── category            FK(MenuCategory)
├── name                CharField
├── slug                SlugField
├── description         TextField
├── price               DecimalField
├── discount_price      DecimalField NULL
├── preparation_time    PositiveIntegerField
├── calories            PositiveIntegerField NULL
├── is_vegetarian       BooleanField
├── is_available        BooleanField
├── is_featured         BooleanField
├── sort_order          PositiveIntegerField
└── created_at          DateTime
```

Important:

```text
price > 0
discount_price <= price
```

---

## 14. `MenuItemImage`

```python
MenuItemImage
├── id              PK
├── menu_item       FK(MenuItem)
├── image           ImageField
├── caption         CharField NULL
└── sort_order      PositiveIntegerField
```

---

# ⚙️ Food Customization

## 15. `MenuItemOptionGroup`

```python
MenuItemOptionGroup
├── id              PK
├── menu_item       FK(MenuItem)
├── name            CharField
├── min_selection   PositiveIntegerField
├── max_selection   PositiveIntegerField
├── is_required     BooleanField
└── sort_order      PositiveIntegerField
```

Example:

```text
Choose Size
min = 1
max = 1
required = True
```

---

## 16. `MenuItemOption`

```python
MenuItemOption
├── id              PK
├── option_group    FK(MenuItemOptionGroup)
├── name            CharField
├── extra_price     DecimalField
├── is_available    BooleanField
└── sort_order      PositiveIntegerField
```

Example:

```text
Small   +0
Medium  +30
Large   +60
```

---

## 17. `MenuItemAddonGroup`

```python
MenuItemAddonGroup
├── id              PK
├── menu_item       FK(MenuItem)
├── name            CharField
├── min_selection   PositiveIntegerField
├── max_selection   PositiveIntegerField
├── is_required     BooleanField
└── sort_order      PositiveIntegerField
```

---

## 18. `MenuItemAddon`

```python
MenuItemAddon
├── id              PK
├── addon_group     FK(MenuItemAddonGroup)
├── name            CharField
├── price            DecimalField
├── is_available     BooleanField
└── sort_order       PositiveIntegerField
```

Example:

```text
Extra Cheese → 50
Extra Sauce  → 20
Fries        → 80
```

---

# 🛒 Cart

## 19. `Cart`

```python
Cart
├── id              PK
├── customer        FK(CustomerProfile)
├── restaurant      FK(Restaurant)
├── subtotal        DecimalField
├── delivery_fee    DecimalField
├── discount        DecimalField
├── total            DecimalField
├── status           CharField
└── updated_at      DateTime
```

Status:

```text
active
converted
abandoned
```

### Important constraint

এক customer-এর এক restaurant-এর active cart:

```text
Unique(customer, restaurant, status)
```

বাস্তবে conditional unique constraint ব্যবহার করা ভালো।

---

## 20. `CartItem`

```python
CartItem
├── id              PK
├── cart            FK(Cart)
├── menu_item       FK(MenuItem)
├── quantity        PositiveIntegerField
├── unit_price      DecimalField
└── total_price     DecimalField
```

Constraint:

```text
Unique(cart, menu_item)
```

---

## 21. `CartItemOption`

```python
CartItemOption
├── id              PK
├── cart_item       FK(CartItem)
├── option          FK(MenuItemOption)
├── quantity        PositiveIntegerField
└── extra_price     DecimalField
```

---

# 🎟️ Coupon

## 22. `Coupon`

```python
Coupon
├── id                  PK
├── code                CharField
├── discount_type       CharField
├── discount_value      DecimalField
├── minimum_order       DecimalField
├── maximum_discount    DecimalField NULL
├── usage_limit         PositiveIntegerField NULL
├── used_count          PositiveIntegerField
├── start_date          DateTimeField
├── end_date            DateTimeField
└── is_active           BooleanField
```

Types:

```text
percentage
fixed
free_delivery
```

---

## 23. `CouponUsage`

```python
CouponUsage
├── id                  PK
├── coupon              FK(Coupon)
├── customer            FK(CustomerProfile)
├── order               FK(Order)
├── discount_amount     DecimalField
└── used_at             DateTimeField
```

---

# 📦 Order

## 24. `Order` ⭐

```python
Order
├── id                      PK
├── order_number            CharField UNIQUE
├── customer                FK(CustomerProfile)
├── restaurant              FK(Restaurant)
├── branch                  FK(RestaurantBranch)
├── delivery_address        FK(DeliveryAddress)
├── subtotal                DecimalField
├── delivery_fee            DecimalField
├── service_fee             DecimalField
├── discount                DecimalField
├── tax                     DecimalField
├── total_amount            DecimalField
├── payment_status          CharField
├── order_status            CharField
├── estimated_delivery_time DateTimeField NULL
├── special_instruction     TextField NULL
├── placed_at               DateTimeField
├── accepted_at             DateTimeField NULL
├── prepared_at             DateTimeField NULL
├── picked_up_at            DateTimeField NULL
├── delivered_at            DateTimeField NULL
└── cancelled_at            DateTimeField NULL
```

### Order Status

```text
pending
confirmed
preparing
ready
assigned
picked_up
on_the_way
delivered
cancelled
rejected
```

---

# 25. `OrderItem`

```python
OrderItem
├── id                    PK
├── order                 FK(Order)
├── menu_item             FK(MenuItem)
├── item_name             CharField
├── unit_price            DecimalField
├── quantity              PositiveIntegerField
├── total_price           DecimalField
└── special_instruction   TextField NULL
```

### কেন `item_name` + `unit_price` রাখছি?

এগুলো **snapshot**।

```text
Order
 ↓
OrderItem
 ↓
item_name = "Chicken Burger"
unit_price = 250
```

পরবর্তীতে MenuItem-এর price 300 হলেও পুরোনো order-এর price 250 থাকবে।

---

# 26. `OrderItemOption`

```python
OrderItemOption
├── id              PK
├── order_item      FK(OrderItem)
├── option_name     CharField
├── extra_price     DecimalField
└── quantity        PositiveIntegerField
```

এটাও historical snapshot।

---

# 27. `OrderStatusHistory`

```python
OrderStatusHistory
├── id              PK
├── order           FK(Order)
├── status           CharField
├── changed_by       FK(User) NULL
├── note             TextField NULL
└── created_at       DateTimeField
```

---

# 💳 Payment

## 28. `Payment`

```python
Payment
├── id                  PK
├── order               FK(Order)
├── transaction_id      CharField UNIQUE
├── amount              DecimalField
├── payment_method      CharField
├── provider            CharField
├── status              CharField
├── paid_at             DateTimeField NULL
├── failure_reason      TextField NULL
└── metadata            JSONField
```

Payment methods:

```text
cash
card
mobile_banking
wallet
```

---

## 29. `Refund`

```python
Refund
├── id                      PK
├── payment                 FK(Payment)
├── order                   FK(Order)
├── amount                  DecimalField
├── reason                  TextField
├── refund_transaction_id   CharField NULL
├── status                  CharField
├── requested_at            DateTimeField
└── processed_at            DateTimeField NULL
```

---

# 🛵 Delivery

## 30. `DeliveryPartner`

```python
DeliveryPartner
├── id                  PK
├── user                OneToOne(User)
├── partner_id          CharField UNIQUE
├── phone               CharField
├── profile_image       ImageField NULL
├── status              CharField
├── current_latitude    DecimalField NULL
├── current_longitude   DecimalField NULL
├── rating              DecimalField
├── total_deliveries    PositiveIntegerField
├── is_verified         BooleanField
└── joined_at           DateTimeField
```

Status:

```text
offline
available
busy
suspended
```

---

## 31. `DeliveryPartnerVehicle`

```python
DeliveryPartnerVehicle
├── id                    PK
├── partner               FK(DeliveryPartner)
├── vehicle_type          CharField
├── registration_number   CharField
├── model                 CharField NULL
├── color                 CharField NULL
└── is_active             BooleanField
```

---

## 32. `DeliveryAssignment`

```python
DeliveryAssignment
├── id                  PK
├── order               OneToOne(Order)
├── delivery_partner    FK(DeliveryPartner)
├── assigned_at         DateTimeField
├── accepted_at         DateTimeField NULL
├── rejected_at         DateTimeField NULL
├── picked_up_at        DateTimeField NULL
├── delivered_at        DateTimeField NULL
├── status              CharField
└── notes               TextField NULL
```

---

## 33. `DeliveryTracking`

```python
DeliveryTracking
├── id              PK
├── assignment      FK(DeliveryAssignment)
├── latitude        DecimalField
├── longitude       DecimalField
├── status          CharField
└── recorded_at     DateTimeField
```

এটা high-volume table হতে পারে।

---

# ⭐ Review

## 34. `RestaurantReview`

```python
RestaurantReview
├── id              PK
├── customer        FK(CustomerProfile)
├── restaurant      FK(Restaurant)
├── order            OneToOne(Order)
├── rating           PositiveSmallIntegerField
├── comment          TextField NULL
├── is_public        BooleanField
└── created_at       DateTimeField
```

Constraint:

```text
Unique(customer, order)
```

---

## 35. `DeliveryReview`

```python
DeliveryReview
├── id                  PK
├── customer            FK(CustomerProfile)
├── delivery_partner    FK(DeliveryPartner)
├── order               OneToOne(Order)
├── rating              PositiveSmallIntegerField
├── comment             TextField NULL
├── is_public           BooleanField
└── created_at          DateTimeField
```

---

# ❤️ Favorites

## 36. `FavoriteRestaurant`

```python
FavoriteRestaurant
├── id              PK
├── customer        FK(CustomerProfile)
├── restaurant      FK(Restaurant)
└── created_at      DateTimeField
```

```text
Unique(customer, restaurant)
```

---

## 37. `FavoriteMenuItem`

```python
FavoriteMenuItem
├── id              PK
├── customer        FK(CustomerProfile)
├── menu_item       FK(MenuItem)
└── created_at      DateTimeField
```

```text
Unique(customer, menu_item)
```

---

# 💰 Commission

## 38. `RestaurantCommission`

```python
RestaurantCommission
├── id                  PK
├── restaurant          FK(Restaurant)
├── order               OneToOne(Order)
├── gross_amount        DecimalField
├── commission_rate     DecimalField
├── commission_amount   DecimalField
├── restaurant_amount   DecimalField
└── created_at          DateTimeField
```

Example:

```text
Order = 1000

Commission = 15%

Platform = 150
Restaurant = 850
```

---

# 💵 Restaurant Payout

## 39. `RestaurantPayout`

```python
RestaurantPayout
├── id                  PK
├── restaurant          FK(Restaurant)
├── amount               DecimalField
├── payout_method       CharField
├── transaction_id      CharField UNIQUE
├── status               CharField
├── period_start         DateField
├── period_end           DateField
├── requested_at         DateTimeField
└── processed_at         DateTimeField NULL
```

---

# 🔔 Notification

## 40. `Notification`

```python
Notification
├── id                  PK
├── user                FK(User)
├── title               CharField
├── message             TextField
├── notification_type   CharField
├── reference_type      CharField NULL
├── reference_id        UUID/Integer NULL
├── is_read             BooleanField
└── created_at          DateTimeField
```

---

# 💬 Messaging

## 41. `Conversation`

```python
Conversation
├── id                  PK
├── order               FK(Order) NULL
├── customer            FK(CustomerProfile)
├── restaurant          FK(Restaurant) NULL
├── delivery_partner    FK(DeliveryPartner) NULL
├── last_message_at     DateTimeField NULL
└── is_active           BooleanField
```

---

## 42. `Message`

```python
Message
├── id                  PK
├── conversation        FK(Conversation)
├── sender              FK(User)
├── message             TextField
├── attachment          FileField NULL
├── is_read             BooleanField
└── created_at          DateTimeField
```

---

# 🎧 Support

## 43. `SupportTicket`

```python
SupportTicket
├── id              PK
├── user            FK(User)
├── order           FK(Order) NULL
├── subject         CharField
├── category        CharField
├── priority        CharField
├── status          CharField
├── created_at      DateTimeField
└── resolved_at     DateTimeField NULL
```

---

## 44. `SupportMessage`

```python
SupportMessage
├── id              PK
├── ticket          FK(SupportTicket)
├── sender          FK(User)
├── message         TextField
├── attachment      FileField NULL
└── created_at      DateTimeField
```

---

# 🔐 Production

## 45. `IdempotencyRecord`

```python
IdempotencyRecord
├── id              PK
├── key             CharField UNIQUE
├── user            FK(User)
├── endpoint        CharField
├── status           CharField
├── response_data   JSONField
└── created_at      DateTimeField
```

বিশেষ করে:

```text
POST /orders/
POST /payments/
POST /refunds/
POST /payouts/
```

এর জন্য useful।

---

# 📝 Audit

## 46. `AuditLog`

```python
AuditLog
├── id              PK
├── user            FK(User) NULL
├── action          CharField
├── model_name      CharField
├── object_id       CharField
├── old_data        JSONField NULL
├── new_data        JSONField NULL
├── ip_address      GenericIPAddressField NULL
└── created_at      DateTimeField
```

---

# 🚚 Delivery Fee

## 47. `DeliveryFeeRule`

```python
DeliveryFeeRule
├── id                  PK
├── restaurant          FK(Restaurant)
├── min_distance_km     DecimalField
├── max_distance_km     DecimalField
├── base_fee             DecimalField
├── per_km_fee           DecimalField
├── minimum_order        DecimalField
└── is_active            BooleanField
```

---

# 🔗 Final Relationship Structure

```text
USER
│
├── CustomerProfile
│    ├── DeliveryAddress
│    ├── Cart
│    ├── Order
│    ├── FavoriteRestaurant
│    └── FavoriteMenuItem
│
├── Restaurant Owner
│    └── Restaurant
│         ├── RestaurantMembership
│         ├── RestaurantBranch
│         ├── RestaurantImage
│         ├── RestaurantAmenity
│         ├── RestaurantCuisine
│         ├── DeliveryZone
│         ├── DeliveryFeeRule
│         │
│         └── MenuCategory
│              └── MenuItem
│                   ├── MenuItemImage
│                   ├── MenuItemOptionGroup
│                   │    └── MenuItemOption
│                   └── MenuItemAddonGroup
│                        └── MenuItemAddon
│
└── DeliveryPartner
     └── DeliveryPartnerVehicle
```

### Order side

```text
Cart
 ↓
CartItem
 ↓
Order
 ├── OrderItem
 │    └── OrderItemOption
 │
 ├── Payment
 │    └── Refund
 │
 ├── OrderStatusHistory
 │
 ├── DeliveryAssignment
 │    └── DeliveryTracking
 │
 ├── RestaurantReview
 ├── DeliveryReview
 ├── CouponUsage
 └── RestaurantCommission
       ↓
   RestaurantPayout
```

---

# ⭐ Production-এর জন্য Important Rules

এই project-এ শুধু field বানালেই হবে না। নিচেরগুলোও database design-এর অংশ:

|Area|Important rule|
|---|---|
|Cart|এক cart → এক restaurant|
|CartItem|`Unique(cart, menu_item)`|
|Order|Server-side total calculation|
|OrderItem|Price/name snapshot|
|Payment|`transaction_id` unique|
|Coupon|Usage validation|
|Review|Delivered order ছাড়া review নয়|
|Delivery|এক order-এর active assignment|
|Rider|Concurrent assignment prevent|
|Commission|Order payment-এর পরে calculate|
|Payout|Settlement period maintain|
|Payment|Idempotency ব্যবহার|
|Audit|Important state changes log|
|Tracking|`assignment + recorded_at` index|

### সবচেয়ে গুরুত্বপূর্ণ architecture

```text
Restaurant
   ↓
Menu
   ↓
Cart
   ↓
Order
   ↓
Payment
   ↓
Restaurant Preparation
   ↓
Delivery Assignment
   ↓
Rider
   ↓
Delivery Tracking
   ↓
Delivered
   ↓
Commission
   ↓
Restaurant Payout
```

এই format-টাই তোমার পরের **Job Marketplace, Hotel, Rental, University, E-commerce** model design-এর ক্ষেত্রেও সবচেয়ে useful হবে—**প্রতিটি model + fields + relationship + constraints + production rules** একসাথে।


----
