অবশ্যই। এবার **Logistics / Delivery Management System**-টা E-commerce project-এর মতো **complete production-level model architecture** হিসেবে দিচ্ছি।

এটা শুধু `Order → Delivery → Driver` system হবে না। এখানে **multi-branch logistics company, warehouse, shipment, parcel, vehicle, driver, route, delivery assignment, tracking, proof of delivery, COD, payment, return, failed delivery, pricing, commission, payout, notification, audit, idempotency**—সব cover করব।

# 🚚 Logistics / Delivery Management System

আমি এখানে **52টি model** রাখছি।

## Complete Model List

```text
1.  BaseModel

2.  Organization
3.  OrganizationMember
4.  Branch

5.  Warehouse
6.  WarehouseZone
7.  WarehouseBin
8.  WarehouseStaff

9.  Customer
10. CustomerAddress

11. DeliveryService
12. ServiceArea
13. DeliveryZone
14. DeliveryRate

15. Shipment
16. ShipmentItem
17. Parcel
18. ParcelDimension
19. ParcelPackage

20. ShipmentAddress
21. ShipmentStatusHistory

22. ShipmentAssignment
23. DeliveryAgent
24. DeliveryAgentDocument
25. DeliveryAgentVehicle
26. Vehicle
27. VehicleMaintenance

28. DeliveryRoute
29. RouteStop
30. RouteAssignment

31. DeliveryTracking
32. DeliveryLocation

33. DeliveryAttempt
34. ProofOfDelivery
35. DeliveryOTP

36. CODCollection
37. CODSettlement
38. DeliveryPayment

39. ShipmentInvoice
40. ShipmentInvoiceItem

41. DeliveryPricingRule
42. AdditionalCharge

43. ShipmentReturn
44. ReturnItem
45. FailedDelivery

46. DeliverySchedule
47. DeliveryTimeSlot

48. Notification
49. CustomerReview

50. Commission
51. AgentPayout

52. AuditLog
53. IdempotencyRecord
```

**Actually count = 53 models.** Production system হিসেবে এই structure বেশি practical।

---

# 📁 Recommended Django Structure

একটা huge `models.py` না করে:

```text
logistics/
│
├── models/
│   ├── __init__.py
│   ├── base.py
│   ├── organization.py
│   ├── branch.py
│   ├── warehouse.py
│   ├── customer.py
│   ├── service.py
│   ├── shipment.py
│   ├── parcel.py
│   ├── agent.py
│   ├── vehicle.py
│   ├── route.py
│   ├── tracking.py
│   ├── delivery.py
│   ├── payment.py
│   ├── cod.py
│   ├── invoice.py
│   ├── pricing.py
│   ├── return.py
│   ├── schedule.py
│   ├── notification.py
│   ├── commission.py
│   ├── payout.py
│   ├── audit.py
│   └── idempotency.py
```

---

# 1. `base.py`

## BaseModel

সব model-এর common fields।

|Field|Django Type|
|---|---|
|id|UUIDField|
|created_at|DateTimeField|
|updated_at|DateTimeField|
|is_active|BooleanField|
|deleted_at|DateTimeField|

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

---

# 🏢 2. `organization.py`

## Organization

Logistics company।

```text
Organization
├── name
├── slug
├── legal_name
├── registration_number
├── tax_number
├── email
├── phone
├── website
├── logo
├── currency
└── is_verified
```

|Field|Type|
|---|---|
|name|CharField(200)|
|slug|SlugField(220)|
|legal_name|CharField(250)|
|registration_number|CharField(100)|
|tax_number|CharField(100)|
|email|EmailField|
|phone|CharField(30)|
|website|URLField|
|logo|ImageField|
|currency|CharField(3)|
|is_verified|BooleanField|

---

# 3. OrganizationMember

```text
organization
user
role
joined_at
is_active
```

Roles:

```text
owner
admin
manager
dispatcher
warehouse_manager
accountant
customer_support
viewer
```

Constraint:

```text
Unique(organization, user)
```

---

# 🏢 4. `branch.py`

## Branch

```text
organization
name
code
address
city
state
country
postal_code
phone
manager
latitude
longitude
is_active
```

Constraint:

```text
Unique(organization, code)
```

---

# 🏭 5. `warehouse.py`

## Warehouse

```text
organization
branch
name
code
warehouse_type
capacity
phone
manager
is_active
```

Warehouse types:

```text
main
hub
sorting_center
distribution_center
fulfillment_center
```

---

# WarehouseZone

Warehouse-এর section।

```text
warehouse
name
code
zone_type
description
is_active
```

Types:

```text
receiving
storage
packing
sorting
dispatch
return
damaged
```

---

# WarehouseBin

```text
zone
name
code
capacity
current_capacity
is_active
```

Constraint:

```text
Unique(zone, code)
```

---

# WarehouseStaff

```text
warehouse
user
role
employee_id
joined_at
is_active
```

Roles:

```text
manager
supervisor
picker
packer
receiver
sorter
dispatcher
```

---

# 👤 6. `customer.py`

## Customer

E-commerce seller বা individual customer।

```text
user
customer_code
name
company_name
email
phone
customer_type
credit_limit
current_balance
is_verified
is_active
```

Customer types:

```text
individual
business
merchant
```

Constraint:

```text
Unique(organization, customer_code)
```

---

# CustomerAddress

```text
customer
label
contact_name
phone
address_line
city
state
country
postal_code
latitude
longitude
delivery_instruction
is_default
```

---

# 📦 7. `service.py`

## DeliveryService

Courier service type।

```text
organization
name
code
service_type
description
estimated_days
base_price
is_active
```

Types:

```text
same_day
next_day
standard
express
international
```

---

# ServiceArea

```text
organization
name
city
state
country
postal_code
is_active
```

---

# DeliveryZone

Geographical delivery zone।

```text
organization
name
code
zone_type
description
is_active
```

Types:

```text
local
metro
regional
national
international
```

---

# DeliveryRate

```text
service
zone
weight_from
weight_to
base_price
per_kg_price
is_active
```

---

# 📦 8. `shipment.py`

## Shipment ⭐⭐⭐

System-এর সবচেয়ে important model।

```text
Shipment
├── organization
├── customer
├── service
├── origin_branch
├── destination_branch
├── tracking_number
├── reference_number
├── shipment_type
├── payment_type
├── total_weight
├── total_amount
├── cod_amount
├── status
├── pickup_date
├── expected_delivery_date
├── delivered_at
└── created_by
```

|Field|Type|
|---|---|
|organization|ForeignKey|
|customer|ForeignKey|
|service|ForeignKey|
|origin_branch|ForeignKey|
|destination_branch|ForeignKey|
|tracking_number|CharField(100)|
|reference_number|CharField(100)|
|shipment_type|CharField(30)|
|payment_type|CharField(30)|
|total_weight|DecimalField(10,3)|
|total_amount|DecimalField(12,2)|
|cod_amount|DecimalField(12,2)|
|status|CharField(30)|
|pickup_date|DateTimeField|
|expected_delivery_date|DateTimeField|
|delivered_at|DateTimeField|
|created_by|ForeignKey|

Shipment type:

```text
parcel
document
fragile
perishable
bulk
```

Payment type:

```text
prepaid
cod
credit
```

Status:

```text
draft
booked
pickup_pending
picked_up
at_origin_hub
in_transit
at_destination_hub
out_for_delivery
delivered
failed
returned
cancelled
```

Constraint:

```text
Unique(organization, tracking_number)
```

---

# ShipmentItem

এক shipment-এ multiple products।

```text
shipment
product_name
sku
quantity
unit_price
total_price
```

|Field|Type|
|---|---|
|shipment|ForeignKey|
|product_name|CharField(250)|
|sku|CharField(100)|
|quantity|PositiveIntegerField|
|unit_price|DecimalField(12,2)|
|total_price|DecimalField(12,2)|

এখানে product snapshot রাখার সুবিধা হলো পরে product পরিবর্তন হলেও shipment history ঠিক থাকে।

---

# 📦 9. `parcel.py`

## Parcel

এক shipment-এ multiple parcel থাকতে পারে।

```text
shipment
parcel_number
weight
length
width
height
declared_value
is_fragile
is_active
```

---

# ParcelDimension

```text
parcel
length
width
height
unit
```

---

# ParcelPackage

Packaging information।

```text
parcel
package_type
material
quantity
cost
```

Types:

```text
box
poly
envelope
carton
crate
```

---

# 📍 10. ShipmentAddress

Sender এবং receiver address snapshot।

```text
shipment
address_type
name
phone
email
address_line
city
state
country
postal_code
latitude
longitude
instruction
```

Address types:

```text
pickup
delivery
```

### কেন CustomerAddress-এর duplicate snapshot?

Customer পরে address change করলেও **পুরনো shipment-এর address পরিবর্তন হবে না।**

এটা production design-এ খুব important।

---

# ShipmentStatusHistory

```text
shipment
old_status
new_status
changed_by
branch
remarks
created_at
```

Example:

```text
booked
 ↓
picked_up
 ↓
in_transit
 ↓
out_for_delivery
 ↓
delivered
```

---

# 🚴 11. `agent.py`

## DeliveryAgent

```text
organization
user
agent_code
phone
agent_type
status
current_latitude
current_longitude
rating
total_deliveries
joined_at
is_verified
```

Agent types:

```text
employee
contractor
partner
```

Status:

```text
available
busy
offline
suspended
```

---

# DeliveryAgentDocument

```text
agent
document_type
document_number
document_file
expiry_date
verified_at
verified_by
status
```

Documents:

```text
nid
driving_license
passport
vehicle_document
```

---

# 🚗 12. `vehicle.py`

## Vehicle

```text
organization
vehicle_number
vehicle_type
brand
model
registration_number
capacity_kg
status
current_latitude
current_longitude
is_active
```

Vehicle types:

```text
bike
motorcycle
car
van
truck
pickup
```

Status:

```text
available
assigned
maintenance
inactive
```

---

# DeliveryAgentVehicle

Agent ↔ Vehicle relation।

```text
agent
vehicle
assigned_at
unassigned_at
is_current
```

Constraint:

এক agent-এর এক current vehicle।

---

# VehicleMaintenance

```text
vehicle
maintenance_type
description
cost
maintenance_date
next_service_date
status
```

---

# 🛣️ 13. `route.py`

## DeliveryRoute

```text
organization
route_number
origin_branch
destination_branch
route_date
distance_km
estimated_duration
status
created_by
```

Status:

```text
planned
assigned
in_progress
completed
cancelled
```

---

# RouteStop

এক route-এর প্রতিটি stop।

```text
route
branch
stop_order
arrival_time
departure_time
status
```

Constraint:

```text
Unique(route, stop_order)
```

---

# RouteAssignment

```text
route
agent
vehicle
assigned_at
started_at
completed_at
status
```

---

# 📍 14. `tracking.py`

## DeliveryTracking ⭐⭐⭐

High-volume table।

```text
shipment
status
latitude
longitude
location_name
recorded_at
source
```

Sources:

```text
gps
agent_app
hub_scan
manual
```

### Index

```text
shipment + recorded_at
```

Large system হলে partitioning consider করবে।

---

# DeliveryLocation

Current/latest location।

```text
agent
latitude
longitude
accuracy
speed
heading
recorded_at
```

এটা delivery agent live tracking-এর জন্য।

---

# 🚪 15. `delivery.py`

## DeliveryAttempt

এক shipment delivery করতে multiple attempt হতে পারে।

```text
shipment
agent
attempt_number
attempted_at
status
failure_reason
remarks
```

Status:

```text
successful
failed
customer_unavailable
address_issue
refused
```

Constraint:

```text
Unique(shipment, attempt_number)
```

---

# ProofOfDelivery

Delivery successful হওয়ার proof।

```text
shipment
attempt
receiver_name
receiver_phone
signature
photo
otp_verified
notes
submitted_at
```

---

# DeliveryOTP

```text
shipment
otp_hash
purpose
expires_at
verified_at
attempt_count
status
```

Purpose:

```text
delivery
pickup
return
```

**Production system-এ plaintext OTP database-এ রাখা উচিত নয়।**

---

# 💰 16. `cod.py`

## CODCollection

Cash on delivery amount।

```text
shipment
agent
expected_amount
collected_amount
collected_at
status
```

Status:

```text
pending
collected
partial
failed
```

---

# CODSettlement

Agent থেকে company settlement।

```text
organization
agent
settlement_number
total_collected
total_settled
difference
settlement_date
status
approved_by
```

Status:

```text
pending
submitted
approved
completed
disputed
```

---

# DeliveryPayment

Delivery charge payment।

```text
shipment
payment_type
amount
transaction_reference
status
paid_at
```

Payment types:

```text
cash
card
mobile_banking
bank
wallet
```

---

# 🧾 17. `invoice.py`

## ShipmentInvoice

```text
organization
shipment
invoice_number
invoice_date
subtotal
tax
discount
total_amount
paid_amount
due_amount
status
```

Status:

```text
draft
issued
partially_paid
paid
overdue
cancelled
```

---

# ShipmentInvoiceItem

```text
invoice
description
quantity
unit_price
amount
```

---

# 💵 18. `pricing.py`

## DeliveryPricingRule

Dynamic delivery pricing।

```text
organization
service
zone
weight_from
weight_to
distance_from
distance_to
base_fee
per_kg_fee
per_km_fee
cod_fee
is_active
```

---

# AdditionalCharge

Extra charges।

```text
shipment
charge_type
description
amount
created_by
```

Types:

```text
fragile
remote_area
waiting
return
fuel
storage
```

---

# 🔄 19. `return.py`

## ShipmentReturn

```text
shipment
return_number
reason
status
requested_at
approved_at
completed_at
created_by
```

Status:

```text
requested
approved
in_transit
received
completed
cancelled
```

---

# ReturnItem

```text
shipment_return
shipment_item
quantity
condition
reason
```

Conditions:

```text
good
damaged
lost
defective
```

---

# FailedDelivery

```text
shipment
attempt
reason
description
next_action
created_at
resolved_at
```

Reasons:

```text
customer_unavailable
wrong_address
customer_refused
phone_unreachable
damaged_parcel
cash_issue
```

---

# 📅 20. `schedule.py`

## DeliverySchedule

```text
organization
name
service
zone
start_time
end_time
max_shipments
is_active
```

---

# DeliveryTimeSlot

```text
schedule
date
start_time
end_time
capacity
booked_count
is_active
```

---

# 🔔 21. `notification.py`

## Notification

```text
user
shipment
title
message
notification_type
is_read
read_at
```

Types:

```text
shipment_booked
pickup
in_transit
out_for_delivery
delivered
failed
return
payment
cod
```

---

# ⭐ 22. `review.py`

## CustomerReview

```text
shipment
customer
agent
rating
comment
is_verified
is_published
```

Constraint:

```text
Unique(shipment, customer)
```

---

# 💼 23. `commission.py`

## Commission

Agent/platform commission।

```text
organization
agent
shipment
commission_type
commission_rate
commission_amount
status
created_at
```

Types:

```text
percentage
fixed
```

---

# 💰 24. `payout.py`

## AgentPayout

```text
organization
agent
payout_number
period_start
period_end
gross_amount
commission
adjustment
net_amount
status
payout_date
transaction_reference
```

Status:

```text
pending
processing
paid
failed
cancelled
```

---

# 📝 25. `audit.py`

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

---

# 🔐 26. `idempotency.py`

## IdempotencyRecord

```text
organization
user
key
endpoint
status
response_data
expires_at
created_at
```

Constraint:

```text
Unique(organization, key)
```

---

# 🔗 Complete Architecture

```text
                         ORGANIZATION
                              │
              ┌───────────────┼────────────────┐
              │               │                │
            Branch          Users           Warehouse
              │                                │
              │                         Zone → Bin
              │
        ┌─────┴──────────────┐
        │                    │
     Customer            Delivery Service
        │                    │
   CustomerAddress      ServiceArea
                             │
                        DeliveryZone
                             │
                        DeliveryRate
                             │
                             ▼
                         SHIPMENT
                             │
             ┌───────────────┼───────────────────┐
             │               │                   │
        ShipmentItem      Parcel          ShipmentAddress
             │               │
             │         ParcelDimension
             │
             ▼
       ShipmentStatusHistory
             │
             ▼
      ShipmentAssignment
             │
      ┌──────┴────────┐
      │               │
 DeliveryAgent      Vehicle
      │               │
 AgentDocument   VehicleMaintenance
      │
      ▼
   RouteAssignment
      │
 DeliveryRoute
      │
 RouteStop
      │
      ▼
DeliveryTracking
      │
      ▼
DeliveryAttempt
      │
 ┌────┴───────────────┐
 │                    │
ProofOfDelivery    FailedDelivery
 │
 └───────┐
         ▼
     Delivered
         │
    CODCollection
         │
    CODSettlement
```

---

# 📦 Shipment Lifecycle

```text
Customer
   ↓
Create Shipment
   ↓
Calculate Delivery Fee
   ↓
Booking Confirmed
   ↓
Pickup Pending
   ↓
Agent Assigned
   ↓
Picked Up
   ↓
Origin Hub
   ↓
In Transit
   ↓
Destination Hub
   ↓
Out For Delivery
   ↓
Delivery Attempt
   ↓
┌───────────────┐
│               │
Delivered     Failed
│               │
↓               ↓
POD          Retry/Return
│
↓
COD Collection
│
↓
Settlement
```

---

# 🚚 Warehouse Flow

```text
Pickup
   ↓
Origin Warehouse
   ↓
Receiving
   ↓
Sorting
   ↓
Dispatch
   ↓
In Transit
   ↓
Destination Warehouse
   ↓
Sorting
   ↓
Dispatch
   ↓
Delivery Agent
```

---

# 💰 COD Flow

ধরি:

```text
Product value = ৳2,000
Delivery fee  = ৳100
COD amount    = ৳2,100
```

Delivery agent customer থেকে collect করল:

```text
CODCollection
expected = 2100
collected = 2100
```

তারপর:

```text
Agent
  ↓
CODSettlement
  ↓
Company
```

---

# 🔥 Concurrency Problem

ধরি warehouse-এ 1টা parcel আছে।

দুই dispatcher একই shipment assign করতে চাচ্ছে:

```text
Dispatcher A ──┐
               ├── Shipment
Dispatcher B ──┘
```

Naive implementation হলে duplicate assignment হতে পারে।

Production:

```python
with transaction.atomic():

    shipment = (
        Shipment.objects
        .select_for_update()
        .get(id=shipment_id)
    )

    # validate current status

    # assign agent

    # update status
```

---

# 🚨 Important Constraints

```text
Organization
    Unique(slug)

OrganizationMember
    Unique(organization, user)

Branch
    Unique(organization, code)

Warehouse
    Unique(organization, code)

WarehouseZone
    Unique(warehouse, code)

WarehouseBin
    Unique(zone, code)

Customer
    Unique(organization, customer_code)

Shipment
    Unique(organization, tracking_number)

ShipmentStatusHistory
    Index(shipment, created_at)

Parcel
    Unique(shipment, parcel_number)

DeliveryAgent
    Unique(organization, agent_code)

Vehicle
    Unique(organization, vehicle_number)

Route
    Unique(organization, route_number)

RouteStop
    Unique(route, stop_order)

DeliveryAttempt
    Unique(shipment, attempt_number)

ShipmentInvoice
    Unique(organization, invoice_number)

CODSettlement
    Unique(organization, settlement_number)

AgentPayout
    Unique(organization, payout_number)

IdempotencyRecord
    Unique(organization, key)
```

---

# 📊 Important Database Indexes

## Shipment

```text
organization + status
customer + created_at
tracking_number
origin_branch + status
destination_branch + status
expected_delivery_date
```

## Tracking

```text
shipment + recorded_at
```

এটা খুব important কারণ tracking table huge হবে।

## Delivery Agent

```text
organization + status
status + updated_at
```

## Delivery Attempt

```text
shipment + created_at
agent + created_at
status + created_at
```

## COD

```text
agent + status
settlement_date
```

## Invoice

```text
customer + status
status + due_date
```

---

# ⚡ High-Volume Tables

এই তিনটা table future-এ অনেক বড় হতে পারে:

```text
DeliveryTracking
DeliveryLocation
ShipmentStatusHistory
```

যদি লাখ/কোটি records হয়:

```text
Partitioning
Archiving
Retention Policy
Indexes
```

consider করতে হবে।

---

# 🧠 Important Production Rules

### 1. Tracking number immutable

একবার:

```text
TRK-2026-000001
```

generate হলে change করবে না।

---

### 2. Shipment address snapshot

Customer address change হলেও পুরনো shipment-এর address change হবে না।

---

### 3. Delivery status transition validate করতে হবে

যেমন:

```text
draft
→ booked
→ pickup_pending
→ picked_up
→ in_transit
→ out_for_delivery
→ delivered
```

কিন্তু:

```text
delivered → picked_up
```

সরাসরি allow করা উচিত না।

---

### 4. Delivered shipment আবার deliver করা যাবে না

```text
status == delivered
```

হলে new delivery attempt reject।

---

### 5. COD amount server-side calculate

Client থেকে:

```text
cod_amount = 100
```

পাঠালেই trust করবে না।

---

### 6. Payment duplicate prevent

Payment endpoint-এ:

```text
Idempotency-Key
```

ব্যবহার করবে।

---

### 7. Agent assignment race prevent

```text
transaction.atomic()
+
select_for_update()
```

---

# 🏗️ Implementation Phases

## Phase 1 — Organization

```text
BaseModel
Organization
OrganizationMember
Branch
```

## Phase 2 — Warehouse

```text
Warehouse
WarehouseZone
WarehouseBin
WarehouseStaff
```

## Phase 3 — Customer

```text
Customer
CustomerAddress
```

## Phase 4 — Delivery Configuration

```text
DeliveryService
ServiceArea
DeliveryZone
DeliveryRate
DeliveryPricingRule
```

## Phase 5 — Shipment ⭐⭐⭐

```text
Shipment
ShipmentItem
Parcel
ParcelDimension
ParcelPackage
ShipmentAddress
ShipmentStatusHistory
```

## Phase 6 — Agent + Vehicle

```text
DeliveryAgent
DeliveryAgentDocument
Vehicle
DeliveryAgentVehicle
VehicleMaintenance
```

## Phase 7 — Route

```text
DeliveryRoute
RouteStop
RouteAssignment
```

## Phase 8 — Tracking

```text
DeliveryTracking
DeliveryLocation
```

## Phase 9 — Delivery

```text
DeliveryAttempt
ProofOfDelivery
DeliveryOTP
FailedDelivery
```

## Phase 10 — Payment

```text
CODCollection
CODSettlement
DeliveryPayment
ShipmentInvoice
ShipmentInvoiceItem
AdditionalCharge
```

## Phase 11 — Return

```text
ShipmentReturn
ReturnItem
```

## Phase 12 — Schedule

```text
DeliverySchedule
DeliveryTimeSlot
```

## Phase 13 — Business

```text
Notification
CustomerReview
Commission
AgentPayout
```

## Phase 14 — Production

```text
AuditLog
IdempotencyRecord
```

---

# ⭐ এই Project-এ তোমার Django ORM-এর কোন কোন topic ব্যবহার হবে?

তুমি যেগুলো already শিখেছো, প্রায় সবই এখানে practicalভাবে ব্যবহার করা যাবে:

```text
select_related()
prefetch_related()
Prefetch()

filter()
exclude()

Q()

F()

annotate()
aggregate()

Count()
Sum()
Avg()

Case()
When()

Exists()
Subquery()
OuterRef()

Window Functions

transaction.atomic()

select_for_update()

UniqueConstraint

CheckConstraint

Composite Index

Conditional Index

Pagination

EXPLAIN / EXPLAIN ANALYZE

Soft Delete

Audit Logging

Idempotency

Concurrency Control
```

বিশেষ করে এই ৫টা অংশ তোমার **database designer** skill-এর জন্য সবচেয়ে valuable:

```text
1. Shipment lifecycle
2. DeliveryTracking
3. CODSettlement
4. Agent assignment concurrency
5. Route + delivery optimization
```

### 🎯 Core Business Architecture

```text
Customer
   ↓
Shipment
   ↓
Parcel
   ↓
Warehouse
   ↓
Route
   ↓
Delivery Agent
   ↓
Tracking
   ↓
Delivery Attempt
   ↓
Proof of Delivery
   ↓
COD / Payment
   ↓
Settlement
   ↓
Payout
```

এভাবে implement করলে এটা শুধু **Courier CRUD project** থাকবে না—বরং **Pathao/RedX/Steadfast-type logistics backend-এর simplified production architecture** হিসেবে portfolio-তে দেখানো যাবে।


