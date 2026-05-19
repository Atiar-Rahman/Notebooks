
# model design


চল তাহলে 👍  
আমি **Super Shop Management System (DRF)** এর জন্য একটা **real-world, scalable কিন্তু শেখার জন্য friendly model design** দিচ্ছি।

এটা:

- Inventory-safe
    
- Sales + Purchase covered
    
- Payment + Return ready
    
- DRF-friendly (query optimize করা সহজ)
    

---

# 🏪 Super Shop Management – Model Design

## 1️⃣ User & Role

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'ADMIN'),
        ('manager', 'MANAGER'),
        ('cashier', 'CASHIER'),
        ('customer', 'CUSTOMER'),
    )
    role = models.CharField(max_length=20, choices=ROLE_CHOICES)
```

---

## 2️⃣ Category, Brand, Unit

```python
class Category(models.Model):
    name = models.CharField(max_length=100)
    parent = models.ForeignKey(
        'self', null=True, blank=True,
        on_delete=models.SET_NULL,
        related_name='children'
    )

class Brand(models.Model):
    name = models.CharField(max_length=100)

class Unit(models.Model):
    name = models.CharField(max_length=20)  # kg, pcs, liter
```

---

## 3️⃣ Product (Core)

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    category = models.ForeignKey(Category, on_delete=models.CASCADE, related_name='products')
    brand = models.ForeignKey(Brand, on_delete=models.SET_NULL, null=True)
    unit = models.ForeignKey(Unit, on_delete=models.SET_NULL, null=True)
    barcode = models.CharField(max_length=100, unique=True)
    selling_price = models.FloatField()
    is_active = models.BooleanField(default=True)

    def __str__(self):
        return self.name
```

---

## 4️⃣ Supplier

```python
class Supplier(models.Model):
    name = models.CharField(max_length=200)
    phone = models.CharField(max_length=20)
    address = models.TextField()
```

---

## 5️⃣ Inventory / Stock (⚠️ Critical)

```python
class Stock(models.Model):
    product = models.OneToOneField(Product, on_delete=models.CASCADE, related_name='stock')
    quantity = models.PositiveIntegerField(default=0)
    minimum_stock = models.PositiveIntegerField(default=5)
```

👉 **One product = one stock row**  
👉 Race condition control সহজ

---

## 6️⃣ Purchase (Stock IN)

```python
class Purchase(models.Model):
    supplier = models.ForeignKey(Supplier, on_delete=models.CASCADE, related_name='purchases')
    created_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)
    created_at = models.DateTimeField(auto_now_add=True)

class PurchaseItem(models.Model):
    purchase = models.ForeignKey(Purchase, on_delete=models.CASCADE, related_name='items')
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    cost_price = models.FloatField()
    quantity = models.PositiveIntegerField()
```

---

## 7️⃣ Sale / Invoice (Stock OUT)

```python
class Sale(models.Model):
    customer = models.ForeignKey(
        User, null=True, blank=True,
        on_delete=models.SET_NULL,
        related_name='sales'
    )
    cashier = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)
    total_amount = models.FloatField()
    discount = models.FloatField(default=0)
    created_at = models.DateTimeField(auto_now_add=True)

class SaleItem(models.Model):
    sale = models.ForeignKey(Sale, on_delete=models.CASCADE, related_name='items')
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    price = models.FloatField()
    quantity = models.PositiveIntegerField()
```

---

## 8️⃣ Payment

```python
class Payment(models.Model):
    METHOD_CHOICES = (
        ('cash', 'CASH'),
        ('card', 'CARD'),
        ('online', 'ONLINE'),
    )
    sale = models.ForeignKey(Sale, on_delete=models.CASCADE, related_name='payments')
    amount = models.FloatField()
    method = models.CharField(max_length=20, choices=METHOD_CHOICES)
    paid_at = models.DateTimeField(auto_now_add=True)
```

---

## 9️⃣ Return (Advanced but Realistic)

```python
class SaleReturn(models.Model):
    sale = models.ForeignKey(Sale, on_delete=models.CASCADE, related_name='returns')
    created_at = models.DateTimeField(auto_now_add=True)

class SaleReturnItem(models.Model):
    sale_return = models.ForeignKey(SaleReturn, on_delete=models.CASCADE, related_name='items')
    product = models.ForeignKey(Product, on_delete=models.CASCADE)
    quantity = models.PositiveIntegerField()
```

---

# 🔥 Why This Design Is GOOD

✔ Inventory safe  
✔ No duplicate stock row  
✔ Easy aggregation  
✔ Transaction friendly  
✔ Query optimization easy

---

# 🚀 Query Optimization Ready

```python
Sale.objects.select_related(
    'customer', 'cashier'
).prefetch_related(
    'items__product',
    'payments'
)
```

---

# ⚠️ Critical Business Logic (Stock Reduce)

```python
@transaction.atomic
def sell_product(product_id, qty):
    stock = Stock.objects.select_for_update().get(product_id=product_id)

    if stock.quantity < qty:
        raise ValidationError("Out of stock")

    stock.quantity -= qty
    stock.save()
```

---

# 🎯 Next Step (তুমি যেটা চাও)

আমি পরের ধাপে দিতে পারি:  
1️⃣ Complete DRF ViewSet  
2️⃣ Serializer validation  
3️⃣ Stock race condition full flow  
4️⃣ Report API (daily sale, profit)

👉 বলো **পরের step কোনটা**?




-----

ঠিক আছে! আমরা **Super Shop Management System** এর জন্য **সম্পূর্ণ Serializer set** বানাবো, যা **তোমার আগের model design অনুযায়ী**।  
এই serializers গুলো DRF-এ ব্যবহার করলে CRUD, nested creation, এবং stock validation সব ঠিকঠাক কাজ করবে।

---

# 1️⃣ User Serializer

```python
from rest_framework import serializers
from .models import User

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'username', 'email', 'role', 'first_name', 'last_name']
```

---

# 2️⃣ Category, Brand, Unit Serializer

```python
from .models import Category, Brand, Unit

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = ['id', 'name', 'parent']

class BrandSerializer(serializers.ModelSerializer):
    class Meta:
        model = Brand
        fields = ['id', 'name']

class UnitSerializer(serializers.ModelSerializer):
    class Meta:
        model = Unit
        fields = ['id', 'name']
```

---

# 3️⃣ Product Serializer

```python
from .models import Product

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'category', 'brand', 'unit', 'barcode', 'selling_price', 'is_active']

    def validate_selling_price(self, value):
        if value <= 0:
            raise serializers.ValidationError("Selling price must be positive")
        return value
```

---

# 4️⃣ Supplier Serializer

```python
from .models import Supplier

class SupplierSerializer(serializers.ModelSerializer):
    class Meta:
        model = Supplier
        fields = ['id', 'name', 'phone', 'address']
```

---

# 5️⃣ Stock Serializer

```python
from .models import Stock

class StockSerializer(serializers.ModelSerializer):
    product_name = serializers.CharField(source='product.name', read_only=True)

    class Meta:
        model = Stock
        fields = ['id', 'product', 'product_name', 'quantity', 'minimum_stock']

    def validate_quantity(self, value):
        if value < 0:
            raise serializers.ValidationError("Stock quantity cannot be negative")
        return value
```

---

# 6️⃣ Purchase Serializer (Nested)

```python
from .models import Purchase, PurchaseItem
from django.db import transaction

class PurchaseItemSerializer(serializers.ModelSerializer):
    class Meta:
        model = PurchaseItem
        fields = ['product', 'cost_price', 'quantity']

    def validate_quantity(self, value):
        if value <= 0:
            raise serializers.ValidationError("Quantity must be greater than zero")
        return value

class PurchaseSerializer(serializers.ModelSerializer):
    items = PurchaseItemSerializer(many=True)

    class Meta:
        model = Purchase
        fields = ['id', 'supplier', 'created_by', 'created_at', 'items']
        read_only_fields = ['created_at', 'created_by']

    @transaction.atomic
    def create(self, validated_data):
        items_data = validated_data.pop('items')
        validated_data['created_by'] = self.context['request'].user
        purchase = Purchase.objects.create(**validated_data)

        for item_data in items_data:
            product = item_data['product']
            quantity = item_data['quantity']

            # update stock
            stock, created = Stock.objects.get_or_create(product=product)
            stock.quantity += quantity
            stock.save()

            PurchaseItem.objects.create(purchase=purchase, **item_data)

        return purchase
```

---

# 7️⃣ Sale Serializer (Nested & Stock-safe)

```python
from .models import Sale, SaleItem, Stock
from rest_framework import serializers
from django.db import transaction

class SaleItemSerializer(serializers.ModelSerializer):
    product_name = serializers.CharField(source='product.name', read_only=True)

    class Meta:
        model = SaleItem
        fields = ['product', 'product_name', 'price', 'quantity']

    def validate(self, data):
        product = data['product']
        quantity = data['quantity']
        if quantity <= 0:
            raise serializers.ValidationError("Quantity must be positive")
        stock = getattr(product, 'stock', None)
        if not stock or stock.quantity < quantity:
            raise serializers.ValidationError(f"Not enough stock for {product.name}")
        return data

class SaleSerializer(serializers.ModelSerializer):
    items = SaleItemSerializer(many=True)

    class Meta:
        model = Sale
        fields = ['id', 'customer', 'cashier', 'total_amount', 'discount', 'created_at', 'items']
        read_only_fields = ['created_at', 'cashier', 'total_amount']

    def validate_discount(self, value):
        if value < 0:
            raise serializers.ValidationError("Discount cannot be negative")
        return value

    def validate(self, data):
        total_amount = sum([item['price'] * item['quantity'] for item in data['items']])
        if total_amount < data.get('discount', 0):
            raise serializers.ValidationError("Discount cannot exceed total amount")
        data['total_amount'] = total_amount
        return data

    @transaction.atomic
    def create(self, validated_data):
        items_data = validated_data.pop('items')
        validated_data['cashier'] = self.context['request'].user
        sale = Sale.objects.create(**validated_data)

        for item_data in items_data:
            product = item_data['product']
            quantity = item_data['quantity']

            # Reduce stock safely
            stock = Stock.objects.select_for_update().get(product=product)
            if stock.quantity < quantity:
                raise serializers.ValidationError(f"Not enough stock for {product.name}")
            stock.quantity -= quantity
            stock.save()

            SaleItem.objects.create(sale=sale, **item_data)

        return sale
```

---

# 8️⃣ Payment Serializer

```python
from .models import Payment

class PaymentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Payment
        fields = ['id', 'sale', 'amount', 'method', 'paid_at']
        read_only_fields = ['paid_at']
```

---

# 9️⃣ Sale Return Serializer

```python
from .models import SaleReturn, SaleReturnItem

class SaleReturnItemSerializer(serializers.ModelSerializer):
    product_name = serializers.CharField(source='product.name', read_only=True)

    class Meta:
        model = SaleReturnItem
        fields = ['product', 'quantity']

class SaleReturnSerializer(serializers.ModelSerializer):
    items = SaleReturnItemSerializer(many=True)

    class Meta:
        model = SaleReturn
        fields = ['id', 'sale', 'created_at', 'items']
        read_only_fields = ['created_at']

    @transaction.atomic
    def create(self, validated_data):
        items_data = validated_data.pop('items')
        sale_return = SaleReturn.objects.create(**validated_data)

        for item_data in items_data:
            product = item_data['product']
            quantity = item_data['quantity']

            # Increase stock back
            stock, created = Stock.objects.get_or_create(product=product)
            stock.quantity += quantity
            stock.save()

            SaleReturnItem.objects.create(sale_return=sale_return, **item_data)

        return sale_return
```

---

# ✅ Summary

- **Nested Serializers**: Purchase, Sale, SaleReturn
    
- **Stock-safe**: `select_for_update()` + atomic transaction
    
- **Field + Object validation**: Quantity, Discount, Stock
    
- **Read-only fields**: created_at, cashier, etc.
    
- **DRF ready**: Compatible with ViewSets
    

---

💡 পরবর্তী step:

- আমি চাইলে **Complete DRF ViewSet + Router + API flow diagram** বানিয়ে দিতে পারি  
    যা দিয়ে **full super shop system API ready** হবে।
    

চাও কি আমি সেটা বানাই?


--------

অবশ্যই! 😎  
আমি তোমাকে **Super Shop Management System** এর জন্য **views.py** তৈরি করে দেখাবো।  
এটা **DRF ViewSets + complete business logic** handle করবে:

- Sale create → Stock reduce
    
- Purchase create → Stock increase
    
- Sale Return → Stock restore
    
- Payment → simple creation
    
- Serializer validation included
    
- Transaction safety + nested handling
    

এটা step-by-step লেখা হবে, যাতে তুমি **complex business logic** বুঝতে পারো।

---

# **views.py – Complete Example**

```python
from rest_framework import viewsets, status
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated
from django.db import transaction
from .models import (
    Product, Stock, Purchase, PurchaseItem,
    Sale, SaleItem, SaleReturn, SaleReturnItem,
    Payment, Supplier
)
from .serializers import (
    ProductSerializer, StockSerializer,
    PurchaseSerializer, SaleSerializer,
    SaleReturnSerializer, PaymentSerializer,
    SupplierSerializer
)

# =======================
# Product & Stock Views
# =======================
class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all().select_related('category', 'brand', 'unit')
    serializer_class = ProductSerializer
    permission_classes = [IsAuthenticated]

class StockViewSet(viewsets.ModelViewSet):
    queryset = Stock.objects.all().select_related('product')
    serializer_class = StockSerializer
    permission_classes = [IsAuthenticated]


# =======================
# Supplier Views
# =======================
class SupplierViewSet(viewsets.ModelViewSet):
    queryset = Supplier.objects.all()
    serializer_class = SupplierSerializer
    permission_classes = [IsAuthenticated]


# =======================
# Purchase Views (Stock IN)
# =======================
class PurchaseViewSet(viewsets.ModelViewSet):
    queryset = Purchase.objects.all().select_related('supplier', 'created_by').prefetch_related('items__product')
    serializer_class = PurchaseSerializer
    permission_classes = [IsAuthenticated]

    @transaction.atomic
    def perform_create(self, serializer):
        """
        Purchase creation automatically updates stock.
        Nested serializer handles PurchaseItem creation.
        """
        serializer.save(created_by=self.request.user)


# =======================
# Sale Views (Stock OUT)
# =======================
class SaleViewSet(viewsets.ModelViewSet):
    queryset = Sale.objects.all().select_related('customer', 'cashier').prefetch_related('items__product', 'payments')
    serializer_class = SaleSerializer
    permission_classes = [IsAuthenticated]

    @transaction.atomic
    def perform_create(self, serializer):
        """
        Sale creation reduces stock atomically.
        """
        serializer.save(cashier=self.request.user)


# =======================
# Sale Return Views (Stock Restore)
# =======================
class SaleReturnViewSet(viewsets.ModelViewSet):
    queryset = SaleReturn.objects.all().select_related('sale').prefetch_related('items__product')
    serializer_class = SaleReturnSerializer
    permission_classes = [IsAuthenticated]

    @transaction.atomic
    def perform_create(self, serializer):
        """
        Sale return restores stock for returned products.
        """
        serializer.save()


# =======================
# Payment Views
# =======================
class PaymentViewSet(viewsets.ModelViewSet):
    queryset = Payment.objects.all().select_related('sale')
    serializer_class = PaymentSerializer
    permission_classes = [IsAuthenticated]

```

---

# **Key Business Logic & Learning Points**

1. **Atomic Transactions** ✅
    

```python
@transaction.atomic
def perform_create(self, serializer):
    serializer.save()
```

- Sale / Purchase / Return → stock safe
    
- Race condition avoided using `select_for_update()` in serializer
    

2. **Nested Serializer Handling** ✅
    

- Purchase → PurchaseItem
    
- Sale → SaleItem
    
- SaleReturn → SaleReturnItem
    

3. **select_related / prefetch_related** ✅
    

- Heavy queries optimized
    
- Example:
    

```python
queryset = Sale.objects.all().select_related('customer', 'cashier').prefetch_related('items__product', 'payments')
```

4. **DRF Permissions** ✅
    

- Only authenticated users can access
    

5. **Business Logic in Serializer vs View** ✅
    

- Stock update → serializer (create override)
    
- ViewSet → just `perform_create` with transaction
    

6. **Separation of Concerns** ✅
    

- Validation → Serializer
    
- Transaction & atomic safety → ViewSet `perform_create`
    
- Query optimization → ViewSet queryset
    

---

# **Extra Tips for Learning Complex Apps**

- Always **override `create()` in serializer** for nested objects & logic
    
- Use `transaction.atomic` in both serializer and view to ensure DB integrity
    
- Keep **query optimization** in mind (`select_related` / `prefetch_related`)
    
- Maintain **business logic in serializer**, not in view, whenever possible
    
- Use **nested serializers** to keep your code DRY
    

---

💡 Next step:  
আমি চাইলে তোমার জন্য **full project API router + urls.py setup** এবং **example API requests for sale, purchase, return, payment** দেখাতে পারি।

তুমি কি সেটা দেখতে চাও?


------


ঠিক আছে! 😎  
এখন আমি তোমাকে **Super Shop Management System** এর জন্য **full DRF router + urls.py setup** দেখাচ্ছি।  
এটি দিয়ে তুমি পুরো API structure ready করে দিতে পারবে।

---

# **project/urls.py** (Main)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include('shop.urls')),  # shop app API
]
```

---

# **shop/urls.py** (App level)

```python
from rest_framework import routers
from django.urls import path, include
from .views import (
    ProductViewSet, StockViewSet, SupplierViewSet,
    PurchaseViewSet, SaleViewSet, SaleReturnViewSet,
    PaymentViewSet
)

router = routers.DefaultRouter()
router.register(r'products', ProductViewSet, basename='product')
router.register(r'stocks', StockViewSet, basename='stock')
router.register(r'suppliers', SupplierViewSet, basename='supplier')
router.register(r'purchases', PurchaseViewSet, basename='purchase')
router.register(r'sales', SaleViewSet, basename='sale')
router.register(r'sale-returns', SaleReturnViewSet, basename='sale-return')
router.register(r'payments', PaymentViewSet, basename='payment')

urlpatterns = [
    path('', include(router.urls)),
]
```

---

# **Example API Routes Generated**

|Endpoint|Method|Action|
|---|---|---|
|`/api/products/`|GET|List all products|
|`/api/products/`|POST|Create product|
|`/api/products/{id}/`|GET|Retrieve product|
|`/api/products/{id}/`|PUT/PATCH|Update product|
|`/api/stocks/`|GET|List stock|
|`/api/stocks/{id}/`|PATCH|Update stock quantity|
|`/api/suppliers/`|GET|List suppliers|
|`/api/purchases/`|POST|Create purchase + update stock|
|`/api/sales/`|POST|Create sale + reduce stock|
|`/api/sale-returns/`|POST|Create return + restore stock|
|`/api/payments/`|POST|Create payment for sale|

---

# **Key Notes**

1. **DefaultRouter** → automatically generates all CRUD routes.
    
2. All **ViewSets** already handle business logic.
    
3. Nested creation like Sale → SaleItems, Purchase → PurchaseItems is **handled in serializer**.
    
4. Stock safety ensured using **transaction.atomic + select_for_update()**.
    
5. Authentication handled via **IsAuthenticated** permission in views.
    

---

# **Optional: JWT Authentication Setup**

If you want token-based auth:

```python
# install djangorestframework-simplejwt
from rest_framework_simplejwt.views import (
    TokenObtainPairView,
    TokenRefreshView,
)

urlpatterns += [
    path('api/token/', TokenObtainPairView.as_view(), name='token_obtain_pair'),
    path('api/token/refresh/', TokenRefreshView.as_view(), name='token_refresh'),
]
```

---

💡 এখন তুমি পুরো project এর **API structure ready**।  
পরের logical step:

- Example **POST requests with nested data**
    
- How to **create sale with multiple items + stock reduce**
    
- How to **create purchase and auto-update stock**
    

চাও আমি সেটা দিয়ে দিই যাতে তুমি **practical API usage** সহজে বুঝতে পারো?



---------
হ্যাঁ, অবশ্যই! 😎

`DefaultRouter` এবং `SimpleRouter` উভয়ই **DRF ViewSets** এর জন্য route তৈরি করে, কিন্তু **subtle difference** আছে:

---

# **DefaultRouter vs SimpleRouter**

|Feature|DefaultRouter|SimpleRouter|
|---|---|---|
|Root API view (`/`)|✅ Creates a default root view with all registered endpoints|❌ No root view|
|Route creation|Same as SimpleRouter|Same as DefaultRouter|
|Use case|Large project, want API root listing|Smaller project, no root needed|

---

# **Example using SimpleRouter**

```python
from rest_framework.routers import SimpleRouter
from django.urls import path, include
from .views import (
    ProductViewSet, StockViewSet, SupplierViewSet,
    PurchaseViewSet, SaleViewSet, SaleReturnViewSet,
    PaymentViewSet
)

router = SimpleRouter()
router.register(r'products', ProductViewSet, basename='product')
router.register(r'stocks', StockViewSet, basename='stock')
router.register(r'suppliers', SupplierViewSet, basename='supplier')
router.register(r'purchases', PurchaseViewSet, basename='purchase')
router.register(r'sales', SaleViewSet, basename='sale')
router.register(r'sale-returns', SaleReturnViewSet, basename='sale-return')
router.register(r'payments', PaymentViewSet, basename='payment')

urlpatterns = [
    path('', include(router.urls)),
]
```

✅ Same API endpoints as DefaultRouter, **except no API root view at `/`**.

---

# **When to use SimpleRouter**

1. ছোট বা internal API project
    
2. যদি API root listing দরকার না হয়
    
3. আপনি চাইলে সব endpoints আলাদাভাবে document করবেন (Swagger/OpenAPI)
    

---

💡 Tip:

- **DefaultRouter** convenient for learning & testing → root view shows all endpoints
    
- **SimpleRouter** lightweight, production-ready if you handle documentation separately
    

---

যদি চাও, আমি তোমার **Super Shop API urls.py** full **SimpleRouter version ready + nested endpoints example** বানিয়ে দেখাতে পারি।

চাও আমি সেটা বানাই?


-------

ঠিক আছে! 😎  
আমি তোমার **Super Shop Management System** এর জন্য **full nested endpoint structure** তৈরি করে দেখাচ্ছি।

এখানে আমরা ব্যবহার করব **drf-nested-routers**, যা DRF-তে parent-child relationship সহজভাবে handle করতে দেয়।

---

# **1️⃣ Install nested routers**

```bash
pip install drf-nested-routers
```

---

# **2️⃣ shop/urls.py – Nested Router Setup**

```python
from rest_framework_nested import routers
from django.urls import path, include
from .views import (
    ProductViewSet, StockViewSet, SupplierViewSet,
    PurchaseViewSet, PurchaseItemViewSet,
    SaleViewSet, SaleItemViewSet,
    SaleReturnViewSet, SaleReturnItemViewSet,
    PaymentViewSet
)

# Parent routers
router = routers.SimpleRouter()
router.register(r'products', ProductViewSet, basename='product')
router.register(r'stocks', StockViewSet, basename='stock')
router.register(r'suppliers', SupplierViewSet, basename='supplier')
router.register(r'purchases', PurchaseViewSet, basename='purchase')
router.register(r'sales', SaleViewSet, basename='sale')
router.register(r'sale-returns', SaleReturnViewSet, basename='sale-return')
router.register(r'payments', PaymentViewSet, basename='payment')

# Nested routers
purchase_items_router = routers.NestedSimpleRouter(router, r'purchases', lookup='purchase')
purchase_items_router.register(r'items', PurchaseItemViewSet, basename='purchase-items')

sale_items_router = routers.NestedSimpleRouter(router, r'sales', lookup='sale')
sale_items_router.register(r'items', SaleItemViewSet, basename='sale-items')

sale_return_items_router = routers.NestedSimpleRouter(router, r'sale-returns', lookup='sale_return')
sale_return_items_router.register(r'items', SaleReturnItemViewSet, basename='sale-return-items')

urlpatterns = [
    path('', include(router.urls)),
    path('', include(purchase_items_router.urls)),
    path('', include(sale_items_router.urls)),
    path('', include(sale_return_items_router.urls)),
]
```

---

# **3️⃣ Views for Nested Resources**

### PurchaseItemViewSet

```python
from rest_framework import viewsets
from .models import PurchaseItem, Purchase
from .serializers import PurchaseItemSerializer
from rest_framework.permissions import IsAuthenticated

class PurchaseItemViewSet(viewsets.ModelViewSet):
    serializer_class = PurchaseItemSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        purchase_id = self.kwargs['purchase_pk']
        return PurchaseItem.objects.filter(purchase_id=purchase_id)
```

### SaleItemViewSet

```python
from .models import SaleItem, Sale
from .serializers import SaleItemSerializer

class SaleItemViewSet(viewsets.ModelViewSet):
    serializer_class = SaleItemSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        sale_id = self.kwargs['sale_pk']
        return SaleItem.objects.filter(sale_id=sale_id)
```

### SaleReturnItemViewSet

```python
from .models import SaleReturnItem, SaleReturn
from .serializers import SaleReturnItemSerializer

class SaleReturnItemViewSet(viewsets.ModelViewSet):
    serializer_class = SaleReturnItemSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        return SaleReturnItem.objects.filter(sale_return_id=self.kwargs['sale_return_pk'])
```

---

# **4️⃣ Generated Nested Endpoints**

|Parent|Child|Endpoint|
|---|---|---|
|Purchase|PurchaseItem|`/purchases/{purchase_id}/items/`|
|Sale|SaleItem|`/sales/{sale_id}/items/`|
|SaleReturn|SaleReturnItem|`/sale-returns/{sale_return_id}/items/`|

- Parent list/create: `/purchases/`, `/sales/`
    
- Child list/create: nested URLs above
    

---

# **5️⃣ Benefits of This Setup**

1. Clear **parent-child relationship**
    
2. Nested objects automatically filtered by parent
    
3. API is intuitive for **frontend developers**
    
4. Keeps **business logic** in serializers / viewsets
    

---

💡 Next Step (Optional):

আমি চাইলে তোমার জন্য **full API usage example** বানিয়ে দেখাতে পারি, যেখানে:

- Create Purchase → Nested Items + Stock update
    
- Create Sale → Nested Items + Stock reduce
    
- Create SaleReturn → Nested Items + Stock restore
    

এই ভাবে তুমি **practical API workflow** পুরোটা বুঝতে পারবে।

চাও আমি সেটা বানাই?







--------
ঠিক আছে! 😎  
আমি তোমার **Super Shop Management System** এর জন্য **full API map + endpoints diagram** বানিয়ে দেখাচ্ছি।  
এতে সব resource, nested relationships এবং key endpoints দেখাবে।

---

# **1️⃣ Authentication**

|Endpoint|Method|Description|
|---|---|---|
|`/api/token/`|POST|Login → get JWT token|
|`/api/token/refresh/`|POST|Refresh JWT token|
|`/api/users/`|POST|Create new user (admin only)|
|`/api/users/{id}/`|GET/PUT/PATCH|Retrieve / update user|

---

# **2️⃣ Master Data / Reference**

|Resource|Endpoint|Method|
|---|---|---|
|Product|`/api/products/`|GET/POST|
|Product|`/api/products/{id}/`|GET/PUT/PATCH/DELETE|
|Stock|`/api/stocks/`|GET/POST|
|Stock|`/api/stocks/{id}/`|GET/PUT/PATCH/DELETE|
|Supplier|`/api/suppliers/`|GET/POST|
|Supplier|`/api/suppliers/{id}/`|GET/PUT/PATCH/DELETE|
|Category|`/api/categories/`|GET/POST|
|Brand|`/api/brands/`|GET/POST|
|Unit|`/api/units/`|GET/POST|

---

# **3️⃣ Purchases (Stock IN)**

|Endpoint|Method|Description|
|---|---|---|
|`/api/purchases/`|GET/POST|List / Create purchase|
|`/api/purchases/{id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete purchase|
|`/api/purchases/{purchase_id}/items/`|GET/POST|List / Create purchase items (nested)|
|`/api/purchases/{purchase_id}/items/{item_id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete purchase item|

---

# **4️⃣ Sales (Stock OUT)**

|Endpoint|Method|Description|
|---|---|---|
|`/api/sales/`|GET/POST|List / Create sale|
|`/api/sales/{id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete sale|
|`/api/sales/{sale_id}/items/`|GET/POST|List / Create sale items (nested)|
|`/api/sales/{sale_id}/items/{item_id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete sale item|

---

# **5️⃣ Sale Returns (Stock Restore)**

|Endpoint|Method|Description|
|---|---|---|
|`/api/sale-returns/`|GET/POST|List / Create sale return|
|`/api/sale-returns/{id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete sale return|
|`/api/sale-returns/{sale_return_id}/items/`|GET/POST|List / Create sale return items (nested)|
|`/api/sale-returns/{sale_return_id}/items/{item_id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete sale return item|

---

# **6️⃣ Payments & Invoices**

|Endpoint|Method|Description|
|---|---|---|
|`/api/payments/`|GET/POST|List / Create payments|
|`/api/payments/{id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete payment|
|`/api/sales/{sale_id}/payments/`|GET|List payments of a sale|
|`/api/invoices/`|GET/POST|List / Create invoices|
|`/api/invoices/{id}/`|GET/PUT/PATCH/DELETE|Retrieve / Update / Delete invoice|

---

# **7️⃣ Reports / Analytics**

|Endpoint|Method|Description|
|---|---|---|
|`/api/reports/stock/`|GET|Low stock / available stock|
|`/api/reports/sales/`|GET|Sales report (filter by date/customer/product)|
|`/api/reports/purchases/`|GET|Purchase report (filter by date/supplier/product)|
|`/api/reports/revenue/`|GET|Revenue / profit summary|

---

# **8️⃣ Nested Relationships Overview**

```
Purchase
 └─ PurchaseItem

Sale
 └─ SaleItem
      └─ Payment (via sale)

SaleReturn
 └─ SaleReturnItem

Stock ← Updated by Purchase / Sale / SaleReturn
```

- **Sale → SaleItem → Payment** → Payment always linked to Sale
    
- **Purchase → PurchaseItem → Stock** → Stock updated on creation
    
- **SaleReturn → SaleReturnItem → Stock** → Stock restored
    

---

# **9️⃣ Diagram (Text Version)**

```
[Products]      [Suppliers]       [Customers]
     |               |                  |
     v               v                  v
  [Stock]           [Purchase]        [Sale] 
     |               |                  |
     |           [PurchaseItem]      [SaleItem]
     |                                  |
     |                              [Payment]
     |
 [Reports / Analytics]
```

- Arrows indicate **data flow / relationship**
    
- Nested endpoints allow **parent → child operations**
    

---

# **10️⃣ Tips for Real API Design**

1. Always **start from master/reference data**
    
2. Implement **CRUD → Transaction → Reporting**
    
3. Use **nested routers** for parent-child relationships
    
4. Keep **business logic in serializers or services**, not views
    
5. Secure endpoints via **JWT + role-based permissions**
    
6. Use **pagination, filtering, search** for lists
    

---

💡 এই structure দিয়ে তুমি **Super Shop এর full backend API** ready করতে পারবে।

যদি চাও, আমি **Swagger / OpenAPI compatible diagram + URL mapping** বানিয়ে দিতে পারি,  
যা দিয়ে frontend developer বা team এক নজরে সব endpoints বুঝবে।

চাও আমি সেটা বানাই?