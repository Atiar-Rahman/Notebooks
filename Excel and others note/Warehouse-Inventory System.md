অবশ্যই। এবার **Warehouse / Inventory Management System**-এর জন্য আগের E-commerce/Food Delivery project-এর মতো **complete production-level models + fields + relationships + constraints** দিচ্ছি।

এটা এমনভাবে design করছি যাতে **multi-warehouse + multi-product + stock movement + purchase + sales + transfer + supplier + inventory valuation + warehouse staff**—সব handle করা যায়।

# 🏭 Warehouse / Inventory System — Complete Models

মোট **45টি core model**:

```text
1.  BaseModel
2.  Warehouse
3.  WarehouseAddress
4.  WarehouseStaff
5.  WarehouseZone
6.  WarehouseBin

7.  ProductCategory
8.  ProductBrand
9.  UnitOfMeasure
10. Product
11. ProductVariant
12. ProductImage
13. ProductBarcode

14. Supplier
15. SupplierContact
16. SupplierProduct

17. Customer
18. CustomerAddress

19. Inventory
20. InventoryBatch
21. InventorySerialNumber
22. StockMovement
23. StockAdjustment
24. StockAdjustmentItem

25. PurchaseOrder
26. PurchaseOrderItem
27. GoodsReceipt
28. GoodsReceiptItem

29. SalesOrder
30. SalesOrderItem
31. Shipment
32. ShipmentItem

33. StockTransfer
34. StockTransferItem

35. StockReservation
36. StockReservationItem

37. PurchaseReturn
38. PurchaseReturnItem
39. SalesReturn
40. SalesReturnItem

41. InventoryCount
42. InventoryCountItem

43. InventoryValuation
44. InventoryNotification
45. AuditLog
46. IdempotencyRecord
```

---

# 🧱 1. BaseModel

সব model-এর common fields।

```text
BaseModel
├── id
├── created_at
├── updated_at
├── is_active
└── deleted_at
```

---

# 🏭 WAREHOUSE

## 2. Warehouse

Main warehouse entity।

```text
Warehouse
├── id
├── name
├── code
├── description
├── warehouse_type
├── phone
├── email
├── is_active
└── manager
```

### Warehouse Type

```text
main
branch
distribution_center
fulfillment_center
cold_storage
```

### Constraint

```text
code → UNIQUE
```

---

# 📍 3. WarehouseAddress

```text
WarehouseAddress
├── id
├── warehouse
├── address_line
├── city
├── state
├── country
├── postal_code
├── latitude
└── longitude
```

Usually:

```text
OneToOne(Warehouse)
```

---

# 👷 4. WarehouseStaff

Warehouse-এর employee/staff।

```text
WarehouseStaff
├── id
├── warehouse
├── user
├── role
├── employee_id
├── joined_at
└── is_active
```

Roles:

```text
manager
supervisor
picker
packer
receiver
inventory_manager
```

Constraint:

```text
Unique(warehouse, user)
Unique(employee_id)
```

---

# 🗂️ 5. WarehouseZone

Warehouse-এর ভিতরের বড় section।

```text
WarehouseZone
├── id
├── warehouse
├── name
├── code
├── zone_type
├── description
└── is_active
```

Example:

```text
Warehouse
├── Receiving Zone
├── Storage Zone
├── Packing Zone
└── Dispatch Zone
```

---

# 📦 6. WarehouseBin

Exact storage location।

```text
WarehouseBin
├── id
├── zone
├── name
├── code
├── capacity
├── current_capacity
└── is_active
```

Example:

```text
A-01-01
A-01-02
B-02-01
```

Relationship:

```text
Warehouse
 ↓
Zone
 ↓
Bin
```

---

# 📦 PRODUCT CATALOG

## 7. ProductCategory

```text
ProductCategory
├── id
├── parent
├── name
├── slug
├── description
└── is_active
```

Self-relation:

```text
Electronics
 ├── Laptop
 ├── Mobile
 └── Accessories
```

---

# 8. ProductBrand

```text
ProductBrand
├── id
├── name
├── slug
├── description
└── is_active
```

---

# 9. UnitOfMeasure

Product quantity কীভাবে measure হবে।

```text
UnitOfMeasure
├── id
├── name
├── code
├── unit_type
├── conversion_factor
└── is_active
```

Examples:

```text
Piece
Box
Kg
Gram
Liter
Meter
```

---

# 10. Product ⭐

Main product।

```text
Product
├── id
├── category
├── brand
├── sku
├── name
├── description
├── unit
├── product_type
├── cost_price
├── selling_price
├── reorder_level
├── reorder_quantity
├── minimum_stock
├── maximum_stock
├── track_inventory
├── track_batch
├── track_serial
└── is_active
```

Product type:

```text
physical
service
bundle
```

Important:

```text
sku → UNIQUE
```

---

# 11. ProductVariant

যেসব product-এর size/color/version আছে।

```text
ProductVariant
├── id
├── product
├── sku
├── name
├── attributes
├── cost_price
├── selling_price
├── weight
├── barcode
└── is_active
```

Example:

```text
T-Shirt

├── Red / M
├── Red / L
├── Blue / M
└── Blue / L
```

`attributes` → JSONField হতে পারে।

---

# 12. ProductImage

```text
ProductImage
├── id
├── product
├── image
├── alt_text
└── sort_order
```

---

# 13. ProductBarcode

```text
ProductBarcode
├── id
├── product
├── variant
├── barcode
├── barcode_type
└── is_active
```

Constraint:

```text
barcode → UNIQUE
```

---

# 🚚 SUPPLIER

## 14. Supplier

```text
Supplier
├── id
├── name
├── code
├── company_name
├── email
├── phone
├── tax_number
├── payment_terms
├── credit_limit
├── rating
├── address
└── is_active
```

Constraint:

```text
code → UNIQUE
```

---

# 15. SupplierContact

```text
SupplierContact
├── id
├── supplier
├── name
├── designation
├── email
├── phone
└── is_primary
```

---

# 16. SupplierProduct

Supplier কোন product supply করে।

```text
SupplierProduct
├── id
├── supplier
├── product
├── supplier_sku
├── purchase_price
├── minimum_order_quantity
├── lead_time_days
└── is_active
```

Constraint:

```text
Unique(supplier, product)
```

---

# 👤 CUSTOMER

## 17. Customer

```text
Customer
├── id
├── user
├── customer_code
├── company_name
├── phone
├── email
├── credit_limit
├── current_balance
└── is_active
```

---

# 18. CustomerAddress

```text
CustomerAddress
├── id
├── customer
├── label
├── address_line
├── city
├── state
├── country
├── postal_code
├── latitude
├── longitude
└── is_default
```

---

# 📊 INVENTORY

## 19. Inventory ⭐⭐⭐

Warehouse + Product-এর current stock।

```text
Inventory
├── id
├── warehouse
├── bin
├── product
├── variant
├── quantity
├── reserved_quantity
├── available_quantity
├── damaged_quantity
├── reorder_level
├── last_stocked_at
└── last_counted_at
```

### Important formula

```text
available_quantity
=
quantity - reserved_quantity
```

Constraint:

```text
Unique(warehouse, bin, product, variant)
```

---

# 🧾 BATCH

## 20. InventoryBatch

Medicine/food/perishable products-এর জন্য গুরুত্বপূর্ণ।

```text
InventoryBatch
├── id
├── product
├── variant
├── warehouse
├── batch_number
├── manufacturing_date
├── expiry_date
├── quantity
├── unit_cost
└── status
```

Status:

```text
active
expired
blocked
depleted
```

---

# 🔢 SERIAL NUMBER

## 21. InventorySerialNumber

Laptop/mobile-এর মতো serialized products।

```text
InventorySerialNumber
├── id
├── product
├── variant
├── warehouse
├── serial_number
├── status
├── purchase_date
└── sold_at
```

Status:

```text
available
reserved
sold
returned
damaged
```

Constraint:

```text
serial_number → UNIQUE
```

---

# 🔄 STOCK MOVEMENT

## 22. StockMovement ⭐⭐⭐

Inventory system-এর সবচেয়ে important model।

```text
StockMovement
├── id
├── product
├── variant
├── warehouse
├── bin
├── movement_type
├── quantity
├── unit_cost
├── reference_type
├── reference_id
├── batch
├── serial_number
├── performed_by
└── created_at
```

Movement:

```text
purchase
sale
sale_return
purchase_return
transfer_in
transfer_out
adjustment
damage
expired
opening_stock
```

---

# ⚙️ STOCK ADJUSTMENT

## 23. StockAdjustment

Manual inventory correction-এর header।

```text
StockAdjustment
├── id
├── warehouse
├── adjustment_number
├── reason
├── status
├── created_by
├── approved_by
├── approved_at
└── notes
```

---

## 24. StockAdjustmentItem

```text
StockAdjustmentItem
├── id
├── adjustment
├── product
├── variant
├── system_quantity
├── counted_quantity
├── difference
└── reason
```

---

# 🛒 PURCHASE

## 25. PurchaseOrder

Supplier থেকে product কেনার order।

```text
PurchaseOrder
├── id
├── supplier
├── warehouse
├── po_number
├── order_date
├── expected_date
├── subtotal
├── tax
├── discount
├── shipping_cost
├── total_amount
├── status
├── created_by
└── approved_by
```

Status:

```text
draft
submitted
approved
partially_received
received
cancelled
```

---

# 26. PurchaseOrderItem

```text
PurchaseOrderItem
├── id
├── purchase_order
├── product
├── variant
├── quantity
├── received_quantity
├── unit_price
├── discount
├── tax
└── total_price
```

---

# 📥 GOODS RECEIPT

## 27. GoodsReceipt

Warehouse-এ actual product আসার record।

```text
GoodsReceipt
├── id
├── purchase_order
├── warehouse
├── receipt_number
├── received_date
├── received_by
├── status
└── notes
```

---

## 28. GoodsReceiptItem

```text
GoodsReceiptItem
├── id
├── receipt
├── purchase_order_item
├── product
├── variant
├── batch
├── quantity_received
├── damaged_quantity
└── unit_cost
```

Flow:

```text
Supplier
 ↓
PurchaseOrder
 ↓
GoodsReceipt
 ↓
Inventory
 ↓
StockMovement
```

---

# 🛍️ SALES

## 29. SalesOrder

Customer-এর sales order।

```text
SalesOrder
├── id
├── customer
├── warehouse
├── order_number
├── order_date
├── subtotal
├── discount
├── tax
├── shipping_cost
├── total_amount
├── payment_status
├── order_status
├── shipping_address
└── created_by
```

Status:

```text
draft
confirmed
processing
packed
shipped
delivered
cancelled
```

---

## 30. SalesOrderItem

```text
SalesOrderItem
├── id
├── sales_order
├── product
├── variant
├── quantity
├── unit_price
├── discount
├── tax
└── total_price
```

---

# 🚚 SHIPMENT

## 31. Shipment

```text
Shipment
├── id
├── sales_order
├── warehouse
├── shipment_number
├── carrier
├── tracking_number
├── shipping_address
├── shipped_at
├── delivered_at
├── status
└── notes
```

---

## 32. ShipmentItem

```text
ShipmentItem
├── id
├── shipment
├── sales_order_item
├── quantity
└── batch
```

---

# 🔁 WAREHOUSE TRANSFER

## 33. StockTransfer

এক warehouse থেকে অন্য warehouse-এ stock।

```text
StockTransfer
├── id
├── transfer_number
├── source_warehouse
├── destination_warehouse
├── transfer_date
├── expected_date
├── status
├── created_by
├── approved_by
└── notes
```

Status:

```text
draft
requested
approved
in_transit
partially_received
received
cancelled
```

---

## 34. StockTransferItem

```text
StockTransferItem
├── id
├── transfer
├── product
├── variant
├── quantity
├── shipped_quantity
├── received_quantity
└── damaged_quantity
```

Flow:

```text
Warehouse A
   ↓
Transfer
   ↓
In Transit
   ↓
Warehouse B
```

---

# 🔒 STOCK RESERVATION

## 35. StockReservation

Order-এর জন্য stock temporarily reserve করা।

```text
StockReservation
├── id
├── sales_order
├── warehouse
├── status
├── expires_at
└── created_at
```

Status:

```text
active
released
consumed
expired
```

---

## 36. StockReservationItem

```text
StockReservationItem
├── id
├── reservation
├── product
├── variant
├── quantity
└── released_quantity
```

Important:

```text
available_stock
=
physical_stock
-
reserved_stock
```

---

# ↩️ PURCHASE RETURN

## 37. PurchaseReturn

Supplier-কে product ফেরত।

```text
PurchaseReturn
├── id
├── supplier
├── purchase_order
├── warehouse
├── return_number
├── reason
├── status
├── total_amount
├── created_by
└── approved_by
```

---

## 38. PurchaseReturnItem

```text
PurchaseReturnItem
├── id
├── purchase_return
├── product
├── variant
├── batch
├── quantity
├── unit_cost
└── reason
```

---

# ↩️ SALES RETURN

## 39. SalesReturn

Customer থেকে product ফেরত।

```text
SalesReturn
├── id
├── sales_order
├── customer
├── warehouse
├── return_number
├── reason
├── status
├── refund_amount
├── created_by
└── approved_by
```

---

## 40. SalesReturnItem

```text
SalesReturnItem
├── id
├── sales_return
├── sales_order_item
├── product
├── variant
├── quantity
├── condition
└── refund_amount
```

Condition:

```text
good
damaged
defective
```

---

# 📋 INVENTORY COUNT

## 41. InventoryCount

Physical stock counting session।

```text
InventoryCount
├── id
├── warehouse
├── count_number
├── count_date
├── status
├── counted_by
├── approved_by
└── notes
```

---

## 42. InventoryCountItem

```text
InventoryCountItem
├── id
├── inventory_count
├── product
├── variant
├── bin
├── system_quantity
├── counted_quantity
├── difference
└── reason
```

Flow:

```text
System Stock
      ↓
Physical Count
      ↓
Difference
      ↓
Stock Adjustment
      ↓
StockMovement
```

---

# 💰 INVENTORY VALUATION

## 43. InventoryValuation

Inventory-এর financial value tracking।

```text
InventoryValuation
├── id
├── warehouse
├── product
├── variant
├── quantity
├── unit_cost
├── total_value
├── valuation_method
└── valuation_date
```

Valuation methods:

```text
FIFO
Weighted Average
```

---

# 🔔 INVENTORY NOTIFICATION

## 44. InventoryNotification

Low-stock/expiry alert।

```text
InventoryNotification
├── id
├── warehouse
├── product
├── variant
├── notification_type
├── message
├── is_read
└── created_at
```

Types:

```text
low_stock
out_of_stock
expiry_warning
expired
overstock
```

---

# 📝 AUDIT

## 45. AuditLog

```text
AuditLog
├── id
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

# 🔐 IDEMPOTENCY

## 46. IdempotencyRecord

```text
IdempotencyRecord
├── id
├── key
├── user
├── endpoint
├── status
├── response_data
└── created_at
```

বিশেষ করে:

```text
POST /purchase-orders/
POST /sales-orders/
POST /transfers/
POST /adjustments/
```

এর জন্য useful।

---

# 🔗 Complete Relationship Architecture

```text
                         WAREHOUSE
                             │
                ┌────────────┼─────────────┐
                │            │             │
              Staff         Zone        Address
                             │
                            Bin
                             │
                             ↓
                         INVENTORY
                             │
              ┌──────────────┼──────────────┐
              │              │              │
             Batch        SerialNumber   Reservation
              │
              ↓
           STOCK MOVEMENT
```

### Product side

```text
Category
   │
Product
   ├── Brand
   ├── Variant
   ├── Image
   └── Barcode
        │
        ↓
     Inventory
```

### Purchase flow

```text
Supplier
   ↓
PurchaseOrder
   ↓
PurchaseOrderItem
   ↓
GoodsReceipt
   ↓
GoodsReceiptItem
   ↓
Inventory
   ↓
StockMovement
```

### Sales flow

```text
Customer
   ↓
SalesOrder
   ↓
SalesOrderItem
   ↓
StockReservation
   ↓
Shipment
   ↓
StockMovement
   ↓
Inventory
```

### Transfer flow

```text
Warehouse A
   ↓
StockTransfer
   ↓
StockTransferItem
   ↓
In Transit
   ↓
Warehouse B
   ↓
Inventory
```

### Return flow

```text
Customer
   ↓
SalesReturn
   ↓
SalesReturnItem
   ↓
Inventory
```

---

# 🧠 Core Inventory Formula

এটা খুব important:

```text
Physical Stock
    =
Current Inventory Quantity

Reserved Stock
    =
Stock already committed to orders

Available Stock
    =
Physical Stock - Reserved Stock
```

Example:

```text
Physical = 100

Reserved = 30

Available = 70
```

---

# 🚨 সবচেয়ে Important Concurrency Problem

ধরো:

```text
Stock = 10

Customer A → buys 7
Customer B → buys 6
```

Naive code হলে:

```text
A sees 10
B sees 10

A → 3 remaining
B → 4 remaining

Final = wrong
```

Production solution:

```text
transaction.atomic()
        +
select_for_update()
        +
database constraints
        +
stock reservation
```

---

# ⭐ Important Constraints

### Product

```text
sku UNIQUE
```

### Warehouse

```text
code UNIQUE
```

### Product Barcode

```text
barcode UNIQUE
```

### Inventory

```text
Unique(
    warehouse,
    bin,
    product,
    variant
)
```

### Supplier Product

```text
Unique(supplier, product)
```

### Stock Transfer

```text
transfer_number UNIQUE
```

### Purchase Order

```text
po_number UNIQUE
```

### Sales Order

```text
order_number UNIQUE
```

---

# 📊 Important Indexes

High-frequency queries-এর জন্য:

```text
Inventory
├── warehouse
├── product
├── variant
└── warehouse + product
```

```text
StockMovement
├── product + created_at
├── warehouse + created_at
└── movement_type + created_at
```

```text
PurchaseOrder
├── supplier + status
└── warehouse + status
```

```text
SalesOrder
├── customer + created_at
├── warehouse + status
└── status + created_at
```

```text
InventoryBatch
├── product + expiry_date
└── warehouse + expiry_date
```

---

# 🏢 Recommended Django App Structure

একটা বিশাল `models.py` না রেখে:

```text
warehouse_management/
│
├── accounts/
│
├── warehouses/
│
├── products/
│
├── suppliers/
│
├── customers/
│
├── inventory/
│
├── purchasing/
│
├── sales/
│
├── shipments/
│
├── transfers/
│
├── reservations/
│
├── returns/
│
├── stock_counts/
│
├── valuation/
│
├── notifications/
│
└── audit/
```

---

# 🚀 Implementation Phase

### Phase 1 — Warehouse + Product

```text
BaseModel
Warehouse
WarehouseAddress
WarehouseStaff
WarehouseZone
WarehouseBin

ProductCategory
ProductBrand
UnitOfMeasure
Product
ProductVariant
ProductImage
ProductBarcode
```

### Phase 2 — Supplier

```text
Supplier
SupplierContact
SupplierProduct
```

### Phase 3 — Inventory

```text
Inventory
InventoryBatch
InventorySerialNumber
StockMovement
```

### Phase 4 — Purchasing

```text
PurchaseOrder
PurchaseOrderItem
GoodsReceipt
GoodsReceiptItem
```

### Phase 5 — Sales

```text
Customer
CustomerAddress
SalesOrder
SalesOrderItem
Shipment
ShipmentItem
```

### Phase 6 — Stock Control

```text
StockTransfer
StockTransferItem
StockReservation
StockReservationItem
```

### Phase 7 — Returns

```text
PurchaseReturn
PurchaseReturnItem
SalesReturn
SalesReturnItem
```

### Phase 8 — Inventory Control

```text
InventoryCount
InventoryCountItem
InventoryValuation
InventoryNotification
```

### Phase 9 — Production

```text
AuditLog
IdempotencyRecord
```

---

# 🎯 এই Project দিয়ে তোমার ORM Practice

এই project-এ Django ORM-এর প্রায় সব advanced topic খুব ভালোভাবে practice হবে:

```text
filter()
exclude()
get()

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

Window Functions

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

বিশেষ করে **Inventory + StockMovement + Reservation + Purchase + Sales + Transfer** অংশগুলো তোমার **database designer** লক্ষ্য অনুযায়ী সবচেয়ে valuable। কারণ এখানে শুধু CRUD নয়, **stock consistency, transaction, locking, historical data, inventory valuation এবং concurrent order handling** একসাথে practice করা যায়।