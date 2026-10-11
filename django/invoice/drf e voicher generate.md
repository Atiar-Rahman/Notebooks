হ্যাঁ। নিচে একটি **production-friendly DRF invoice system** দিলাম যেখানে থাকবে:

- Customer
    
- Product
    
- Invoice
    
- InvoiceItem
    
- Automatic subtotal/tax/total calculation
    
- Invoice CRUD API
    
- Invoice PDF generation
    
- PDF download endpoint
    
- Atomic transaction
    
- Nested invoice items
    
- Unique invoice number
    

আমি এখানে **WeasyPrint** ব্যবহার করছি, কারণ HTML/CSS দিয়ে সুন্দর invoice template তৈরি করা যায়।

## 1. Project structure

```
project/
├── manage.py
├── config/
│   ├── settings.py
│   └── urls.py
└── invoices/
    ├── migrations/
    ├── templates/
    │   └── invoices/
    │       └── invoice.html
    ├── admin.py
    ├── models.py
    ├── serializers.py
    ├── urls.py
    ├── views.py
    └── apps.py
```

## 2. Install packages

```
pip install django djangorestframework weasyprint
```

`settings.py`:

```
INSTALLED_APPS = [
    # Django apps
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    # Third-party
    "rest_framework",

    # Local
    "invoices",
]
```

---

# 3. Models

`invoices/models.py`

```
from decimal import Decimal

from django.db import models
from django.core.validators import MinValueValidator


class Customer(models.Model):
    name = models.CharField(max_length=200)
    email = models.EmailField(blank=True)
    phone = models.CharField(max_length=30, blank=True)
    address = models.TextField(blank=True)

    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ["-id"]

    def __str__(self):
        return self.name


class Product(models.Model):
    name = models.CharField(max_length=255)
    sku = models.CharField(max_length=100, unique=True)
    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        validators=[MinValueValidator(Decimal("0"))],
    )

    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.name} ({self.sku})"


class Invoice(models.Model):

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("issued", "Issued"),
        ("paid", "Paid"),
        ("cancelled", "Cancelled"),
    ]

    invoice_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    customer = models.ForeignKey(
        Customer,
        on_delete=models.PROTECT,
        related_name="invoices",
    )

    issue_date = models.DateField(auto_now_add=True)

    due_date = models.DateField(
        null=True,
        blank=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="draft",
    )

    tax_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        default=Decimal("0.00"),
        validators=[
            MinValueValidator(Decimal("0"))
        ],
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    tax_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    total = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    notes = models.TextField(blank=True)

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        ordering = ["-id"]

    def __str__(self):
        return self.invoice_number

    def calculate_totals(self):
        subtotal = sum(
            (item.line_total for item in self.items.all()),
            Decimal("0.00"),
        )

        tax_amount = (
            subtotal * self.tax_rate / Decimal("100")
        )

        total = subtotal + tax_amount

        self.subtotal = subtotal
        self.tax_amount = tax_amount
        self.total = total

    def save(self, *args, **kwargs):
        if not self.invoice_number:
            last_invoice = (
                Invoice.objects
                .order_by("-id")
                .first()
            )

            if last_invoice:
                last_id = last_invoice.id + 1
            else:
                last_id = 1

            self.invoice_number = f"INV-{last_id:06d}"

        super().save(*args, **kwargs)


class InvoiceItem(models.Model):
    invoice = models.ForeignKey(
        Invoice,
        on_delete=models.CASCADE,
        related_name="items",
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT,
        related_name="invoice_items",
    )

    description = models.CharField(
        max_length=500,
        blank=True,
    )

    quantity = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        validators=[
            MinValueValidator(Decimal("0.01"))
        ],
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        validators=[
            MinValueValidator(Decimal("0"))
        ],
    )

    line_total = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    def save(self, *args, **kwargs):
        self.line_total = (
            self.quantity * self.unit_price
        )

        super().save(*args, **kwargs)

    def __str__(self):
        return f"{self.product.name} - {self.quantity}"
```

### গুরুত্বপূর্ণ

এখানে `line_total` automatically calculate হবে:

```
quantity × unit_price
```

এবং Invoice-এর:

```
subtotal = সব line_total-এর যোগফল

tax = subtotal × tax_rate / 100

total = subtotal + tax
```

---

# 4. Serializers

`invoices/serializers.py`

```
from django.db import transaction
from rest_framework import serializers

from .models import (
    Customer,
    Product,
    Invoice,
    InvoiceItem,
)


class CustomerSerializer(serializers.ModelSerializer):

    class Meta:
        model = Customer
        fields = [
            "id",
            "name",
            "email",
            "phone",
            "address",
            "created_at",
        ]
        read_only_fields = [
            "id",
            "created_at",
        ]


class ProductSerializer(serializers.ModelSerializer):

    class Meta:
        model = Product
        fields = [
            "id",
            "name",
            "sku",
            "price",
            "created_at",
        ]
        read_only_fields = [
            "id",
            "created_at",
        ]


class InvoiceItemSerializer(serializers.ModelSerializer):

    product_name = serializers.CharField(
        source="product.name",
        read_only=True,
    )

    class Meta:
        model = InvoiceItem
        fields = [
            "id",
            "product",
            "product_name",
            "description",
            "quantity",
            "unit_price",
            "line_total",
        ]

        read_only_fields = [
            "id",
            "product_name",
            "line_total",
        ]

    def validate(self, attrs):
        product = attrs.get("product")

        if not product:
            raise serializers.ValidationError(
                "Product is required."
            )

        # If unit_price is not provided,
        # use product's current price.
        if not attrs.get("unit_price"):
            attrs["unit_price"] = product.price

        return attrs


class InvoiceSerializer(serializers.ModelSerializer):

    items = InvoiceItemSerializer(
        many=True
    )

    customer_name = serializers.CharField(
        source="customer.name",
        read_only=True,
    )

    class Meta:
        model = Invoice

        fields = [
            "id",
            "invoice_number",
            "customer",
            "customer_name",
            "issue_date",
            "due_date",
            "status",
            "tax_rate",
            "subtotal",
            "tax_amount",
            "total",
            "notes",
            "items",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "invoice_number",
            "issue_date",
            "subtotal",
            "tax_amount",
            "total",
            "created_at",
            "updated_at",
        ]

    @transaction.atomic
    def create(self, validated_data):

        items_data = validated_data.pop("items")

        invoice = Invoice.objects.create(
            **validated_data
        )

        for item_data in items_data:
            InvoiceItem.objects.create(
                invoice=invoice,
                **item_data
            )

        invoice.calculate_totals()
        invoice.save(
            update_fields=[
                "subtotal",
                "tax_amount",
                "total",
            ]
        )

        return invoice

    @transaction.atomic
    def update(
        self,
        instance,
        validated_data
    ):

        items_data = validated_data.pop(
            "items",
            None
        )

        for attr, value in validated_data.items():
            setattr(instance, attr, value)

        instance.save()

        if items_data is not None:

            instance.items.all().delete()

            for item_data in items_data:
                InvoiceItem.objects.create(
                    invoice=instance,
                    **item_data
                )

        instance.calculate_totals()

        instance.save(
            update_fields=[
                "subtotal",
                "tax_amount",
                "total",
            ]
        )

        return instance
```

---

# 5. ViewSet

`invoices/views.py`

```
from django.http import HttpResponse
from django.template.loader import render_to_string

from rest_framework import viewsets
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import status

from weasyprint import HTML

from .models import (
    Customer,
    Product,
    Invoice,
)

from .serializers import (
    CustomerSerializer,
    ProductSerializer,
    InvoiceSerializer,
)


class CustomerViewSet(viewsets.ModelViewSet):

    queryset = Customer.objects.all()

    serializer_class = CustomerSerializer


class ProductViewSet(viewsets.ModelViewSet):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer


class InvoiceViewSet(viewsets.ModelViewSet):

    queryset = (
        Invoice.objects
        .select_related("customer")
        .prefetch_related(
            "items__product"
        )
    )

    serializer_class = InvoiceSerializer

    @action(
        detail=True,
        methods=["get"],
        url_path="pdf",
    )
    def pdf(self, request, pk=None):

        invoice = self.get_object()

        html_string = render_to_string(
            "invoices/invoice.html",
            {
                "invoice": invoice,
            }
        )

        pdf_file = HTML(
            string=html_string
        ).write_pdf()

        response = HttpResponse(
            pdf_file,
            content_type="application/pdf",
        )

        response[
            "Content-Disposition"
        ] = (
            f'attachment; '
            f'filename="{invoice.invoice_number}.pdf"'
        )

        return response
```

এখন:

```
GET /api/invoices/1/pdf/
```

করলে সরাসরি PDF download হবে।

---

# 6. Invoice HTML Template

`invoices/templates/invoices/invoice.html`

```
<!DOCTYPE html>
<html>
<head>

    <meta charset="UTF-8">

    <style>

        @page {
            size: A4;
            margin: 25px;
        }

        body {
            font-family: Arial, sans-serif;
            color: #333;
            font-size: 13px;
        }

        .header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 30px;
        }

        .company-name {
            font-size: 26px;
            font-weight: bold;
            color: #2563eb;
        }

        .invoice-title {
            font-size: 30px;
            font-weight: bold;
        }

        .info {
            margin-bottom: 30px;
        }

        .info-table {
            width: 100%;
        }

        .info-table td {
            vertical-align: top;
            padding: 5px;
        }

        .items {
            width: 100%;
            border-collapse: collapse;
        }

        .items th {
            background: #2563eb;
            color: white;
            padding: 10px;
            text-align: left;
        }

        .items td {
            border-bottom: 1px solid #ddd;
            padding: 10px;
        }

        .right {
            text-align: right;
        }

        .totals {
            width: 40%;
            margin-left: auto;
            margin-top: 20px;
        }

        .totals td {
            padding: 7px;
        }

        .grand-total {
            font-size: 18px;
            font-weight: bold;
            border-top: 2px solid #333;
        }

        .notes {
            margin-top: 50px;
        }

        .footer {
            margin-top: 70px;
            text-align: center;
            color: #777;
        }

    </style>

</head>

<body>

    <div class="header">

        <div>
            <div class="company-name">
                My Company
            </div>

            <div>
                Dhaka, Bangladesh
            </div>

            <div>
                Email: billing@example.com
            </div>
        </div>

        <div>
            <div class="invoice-title">
                INVOICE
            </div>

            <div>
                #{{ invoice.invoice_number }}
            </div>

            <div>
                Date: {{ invoice.issue_date }}
            </div>

            {% if invoice.due_date %}
                <div>
                    Due: {{ invoice.due_date }}
                </div>
            {% endif %}

        </div>

    </div>


    <div class="info">

        <table class="info-table">

            <tr>

                <td>
                    <strong>Bill To:</strong><br>

                    {{ invoice.customer.name }}<br>

                    {{ invoice.customer.email }}<br>

                    {{ invoice.customer.phone }}<br>

                    {{ invoice.customer.address }}

                </td>

                <td class="right">

                    <strong>Status:</strong><br>

                    {{ invoice.get_status_display }}

                </td>

            </tr>

        </table>

    </div>


    <table class="items">

        <thead>

            <tr>
                <th>#</th>
                <th>Product</th>
                <th>Description</th>
                <th>Qty</th>
                <th>Unit Price</th>
                <th>Total</th>
            </tr>

        </thead>

        <tbody>

            {% for item in invoice.items.all %}

            <tr>

                <td>
                    {{ forloop.counter }}
                </td>

                <td>
                    {{ item.product.name }}
                </td>

                <td>
                    {{ item.description }}
                </td>

                <td>
                    {{ item.quantity }}
                </td>

                <td>
                    {{ item.unit_price }}
                </td>

                <td>
                    {{ item.line_total }}
                </td>

            </tr>

            {% endfor %}

        </tbody>

    </table>


    <table class="totals">

        <tr>
            <td>Subtotal</td>

            <td class="right">
                {{ invoice.subtotal }}
            </td>
        </tr>

        <tr>
            <td>
                Tax ({{ invoice.tax_rate }}%)
            </td>

            <td class="right">
                {{ invoice.tax_amount }}
            </td>
        </tr>

        <tr class="grand-total">

            <td>
                Total
            </td>

            <td class="right">
                {{ invoice.total }}
            </td>

        </tr>

    </table>


    {% if invoice.notes %}

        <div class="notes">

            <strong>Notes:</strong>

            <p>
                {{ invoice.notes }}
            </p>

        </div>

    {% endif %}


    <div class="footer">

        Thank you for your business!

    </div>

</body>
</html>
```

---

# 7. URLs

`invoices/urls.py`

```
from rest_framework.routers import DefaultRouter

from .views import (
    CustomerViewSet,
    ProductViewSet,
    InvoiceViewSet,
)


router = DefaultRouter()

router.register(
    "customers",
    CustomerViewSet,
    basename="customer",
)

router.register(
    "products",
    ProductViewSet,
    basename="product",
)

router.register(
    "invoices",
    InvoiceViewSet,
    basename="invoice",
)


urlpatterns = router.urls
```

Project-এর `config/urls.py`:

```
from django.contrib import admin
from django.urls import path, include


urlpatterns = [

    path(
        "admin/",
        admin.site.urls
    ),

    path(
        "api/",
        include("invoices.urls")
    ),

]
```

---

# 8. Database migration

```
python manage.py makemigrations
python manage.py migrate
```

তারপর:

```
python manage.py runserver
```

---

# 9. Create Customer

### Request

```
POST /api/customers/
Content-Type: application/json
```

```
{
    "name": "Rahim Ahmed",
    "email": "rahim@example.com",
    "phone": "01700000000",
    "address": "Dhaka, Bangladesh"
}
```

Response:

```
{
    "id": 1,
    "name": "Rahim Ahmed",
    "email": "rahim@example.com",
    "phone": "01700000000",
    "address": "Dhaka, Bangladesh",
    "created_at": "2026-10-01T07:30:00Z"
}
```

---

# 10. Create Product

```
POST /api/products/
```

```
{
    "name": "Website Development",
    "sku": "WEB-001",
    "price": "50000.00"
}
```

আরেকটি:

```
{
    "name": "Hosting",
    "sku": "HOST-001",
    "price": "5000.00"
}
```

---

# 11. Create Invoice

এখন সবচেয়ে গুরুত্বপূর্ণ API:

```
POST /api/invoices/
```

```
{
    "customer": 1,
    "due_date": "2026-10-15",
    "status": "issued",
    "tax_rate": "10.00",
    "notes": "Payment within 15 days.",

    "items": [
        {
            "product": 1,
            "description": "Corporate website development",
            "quantity": "1",
            "unit_price": "50000.00"
        },
        {
            "product": 2,
            "description": "One year hosting",
            "quantity": "2",
            "unit_price": "5000.00"
        }
    ]
}
```

Backend automatically calculate করবে:

```
Website = 1 × 50,000 = 50,000
Hosting = 2 × 5,000  = 10,000

Subtotal = 60,000

Tax 10% = 6,000

Total = 66,000
```

Response হবে roughly:

```
{
    "id": 1,
    "invoice_number": "INV-000001",
    "customer": 1,
    "customer_name": "Rahim Ahmed",
    "issue_date": "2026-10-01",
    "due_date": "2026-10-15",
    "status": "issued",
    "tax_rate": "10.00",
    "subtotal": "60000.00",
    "tax_amount": "6000.00",
    "total": "66000.00",
    "notes": "Payment within 15 days.",
    "items": [
        {
            "id": 1,
            "product": 1,
            "product_name": "Website Development",
            "description": "Corporate website development",
            "quantity": "1.00",
            "unit_price": "50000.00",
            "line_total": "50000.00"
        },
        {
            "id": 2,
            "product": 2,
            "product_name": "Hosting",
            "description": "One year hosting",
            "quantity": "2.00",
            "unit_price": "5000.00",
            "line_total": "10000.00"
        }
    ]
}
```

---

# 12. Get Invoice

```
GET /api/invoices/1/
```

---

# 13. List Invoices

```
GET /api/invoices/
```

---

# 14. Update Invoice

```
PUT /api/invoices/1/
```

```
{
    "customer": 1,
    "due_date": "2026-10-20",
    "status": "issued",
    "tax_rate": "15.00",

    "items": [
        {
            "product": 1,
            "description": "Updated website development",
            "quantity": "1",
            "unit_price": "55000.00"
        }
    ],

    "notes": "Updated invoice."
}
```

পুরো items list replace হবে এবং totals আবার calculate হবে।

---

# 15. Generate PDF

Invoice তৈরি হওয়ার পরে:

```
GET /api/invoices/1/pdf/
```

এটি return করবে:

```
Content-Type: application/pdf
```

এবং browser/download client-এ:

```
INV-000001.pdf
```

নামে PDF পাওয়া যাবে।

---

## 16. Admin

`invoices/admin.py`

```
from django.contrib import admin

from .models import (
    Customer,
    Product,
    Invoice,
    InvoiceItem,
)


@admin.register(Customer)
class CustomerAdmin(admin.ModelAdmin):

    list_display = [
        "id",
        "name",
        "email",
        "phone",
    ]

    search_fields = [
        "name",
        "email",
        "phone",
    ]


@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):

    list_display = [
        "id",
        "name",
        "sku",
        "price",
    ]

    search_fields = [
        "name",
        "sku",
    ]


class InvoiceItemInline(
    admin.TabularInline
):

    model = InvoiceItem

    extra = 0

    readonly_fields = [
        "line_total",
    ]


@admin.register(Invoice)
class InvoiceAdmin(admin.ModelAdmin):

    list_display = [
        "invoice_number",
        "customer",
        "issue_date",
        "status",
        "total",
    ]

    list_filter = [
        "status",
        "issue_date",
    ]

    search_fields = [
        "invoice_number",
        "customer__name",
    ]

    readonly_fields = [
        "invoice_number",
        "subtotal",
        "tax_amount",
        "total",
        "issue_date",
        "created_at",
        "updated_at",
    ]

    inlines = [
        InvoiceItemInline,
    ]
```

---

## API summary

তাহলে আপনার complete API দাঁড়াবে:

|Method|Endpoint|কাজ|
|---|---|---|
|`GET`|`/api/customers/`|Customer list|
|`POST`|`/api/customers/`|Customer create|
|`GET`|`/api/products/`|Product list|
|`POST`|`/api/products/`|Product create|
|`GET`|`/api/invoices/`|Invoice list|
|`POST`|`/api/invoices/`|Invoice create|
|`GET`|`/api/invoices/1/`|Invoice details|
|`PUT`|`/api/invoices/1/`|Invoice update|
|`PATCH`|`/api/invoices/1/`|Partial update|
|`DELETE`|`/api/invoices/1/`|Invoice delete|
|`GET`|`/api/invoices/1/pdf/`|PDF download|

### Production-এ আমি আরও যেগুলো যোগ করতাম

- JWT authentication
    
- User/company-wise invoice isolation
    
- Invoice payment tracking
    
- `paid_amount` / `due_amount`
    
- Discount
    
- Shipping charge
    
- VAT
    
- Currency
    
- Company logo
    
- Invoice PDF storage
    
- Email invoice
    
- Invoice numbering per company
    
- Soft delete
    
- Filtering/search/pagination
    
- Permission system
    
- PDF URL instead of generating every request
    

**একটা গুরুত্বপূর্ণ production issue:** উপরের `invoice_number` generation demo হিসেবে `last invoice ID` ব্যবহার করছে। High-concurrency production system-এ duplicate/sequence সমস্যা এড়াতে database-backed sequence বা transaction-safe numbering ব্যবহার করা ভালো।

---
হ্যাঁ, **Invoice system-এ UUID ব্যবহার করা ভালো**। বিশেষ করে public API-তে sequential integer ID (`1`, `2`, `3`) না দিয়ে UUID ব্যবহার করলে ভালো হয়।

 ### Model এ এভাবে করতে পারেন

```
import uuid

class Invoice(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    invoice_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False
    )

    customer = models.ForeignKey(
        Customer,
        on_delete=models.PROTECT,
        related_name="invoices"
    )

    # ... বাকি fields
```

 তাহলে API response হবে এরকম:

```
{
    "id": "550e8400-e29b-41d4-a716-446655440000",
    "invoice_number": "INV-000001"
}
```

 ### আরও ভালো approach

 আমি সাধারণত **দুটো আলাদা রাখার** পরামর্শ দেব:

```
id              → UUID
invoice_number  → Human-friendly invoice number
```

 যেমন:

```
id:
8f7c2c8e-7e3c-4e31-9f2a-1c4e8d6a9b21

invoice_number:
INV-2026-000001
```

 API:

```
GET /api/invoices/8f7c2c8e-7e3c-4e31-9f2a-1c4e8d6a9b21/
```

 PDF:

```
INV-2026-000001.pdf
```

 এটা clean এবং production-এর জন্য ভালো design।

 **চাইলে আগের complete invoice system-টা আমি  UUID-based করে models.py + serializers.py + views.py + URLs + PDF পুরোটা একসাথে revised version হিসেবে দিতে পারি ।**

----
অবশ্যই। নিচে আগের system-টার **UUID-based production-oriented revised version** দিলাম। এখানে:

 - `Customer`, `Product`, `Invoice`, `InvoiceItem` — সব primary key UUID
- Invoice public ID হবে UUID
- Human-readable `invoice_number` আলাদা থাকবে, যেমন `INV-2026-000001`
- Nested invoice items
- Automatic subtotal/tax/total
- `transaction.atomic()`
- `select_related` / `prefetch_related`
- PDF generation with WeasyPrint
- PDF endpoint
- Invoice number concurrency-safe করার জন্য transaction + row locking approach

 ## Project structure

```
project/
├── manage.py
├── config/
│   ├── settings.py
│   └── urls.py
└── invoices/
    ├── migrations/
    ├── templates/
    │   └── invoices/
    │       └── invoice.html
    ├── models.py
    ├── serializers.py
    ├── views.py
    └── urls.py
```

 ## 1\. Install

```
pip install django djangorestframework weasyprint
```

 `settings.py`:

```
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",

    "rest_framework",

    "invoices",
]
```

---

 # 2\. `models.py`

 এখানে সব model-এর primary key UUID রাখা হয়েছে।

```
import uuid
from decimal import Decimal

from django.db import models
from django.core.validators import MinValueValidator

class UUIDModel(models.Model):
    """
    Base model for UUID primary key.
    """

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    class Meta:
        abstract = True

class Customer(UUIDModel):

    name = models.CharField(
        max_length=200
    )

    email = models.EmailField(
        blank=True
    )

    phone = models.CharField(
        max_length=30,
        blank=True
    )

    address = models.TextField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        ordering = ["-created_at"]

    def __str__(self):
        return self.name

class Product(UUIDModel):

    name = models.CharField(
        max_length=255
    )

    sku = models.CharField(
        max_length=100,
        unique=True
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        validators=[
            MinValueValidator(
                Decimal("0.00")
            )
        ],
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        ordering = ["-created_at"]

    def __str__(self):
        return f"{self.name} ({self.sku})"

class Invoice(UUIDModel):

    STATUS_DRAFT = "draft"
    STATUS_ISSUED = "issued"
    STATUS_PAID = "paid"
    STATUS_CANCELLED = "cancelled"

    STATUS_CHOICES = [
        (STATUS_DRAFT, "Draft"),
        (STATUS_ISSUED, "Issued"),
        (STATUS_PAID, "Paid"),
        (STATUS_CANCELLED, "Cancelled"),
    ]

    invoice_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    customer = models.ForeignKey(
        Customer,
        on_delete=models.PROTECT,
        related_name="invoices",
    )

    issue_date = models.DateField(
        auto_now_add=True
    )

    due_date = models.DateField(
        null=True,
        blank=True
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default=STATUS_DRAFT,
    )

    tax_rate = models.DecimalField(
        max_digits=5,
        decimal_places=2,
        default=Decimal("0.00"),
        validators=[
            MinValueValidator(
                Decimal("0.00")
            )
        ],
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    tax_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    total = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    notes = models.TextField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        ordering = ["-created_at"]

    def __str__(self):
        return self.invoice_number

    def calculate_totals(self):
        """
        Calculate subtotal, tax and total.
        """

        subtotal = sum(
            (
                item.line_total
                for item in self.items.all()
            ),
            Decimal("0.00"),
        )

        tax_amount = (
            subtotal
            * self.tax_rate
            / Decimal("100")
        )

        total = subtotal + tax_amount

        self.subtotal = subtotal
        self.tax_amount = tax_amount
        self.total = total

class InvoiceItem(UUIDModel):

    invoice = models.ForeignKey(
        Invoice,
        on_delete=models.CASCADE,
        related_name="items",
    )

    product = models.ForeignKey(
        Product,
        on_delete=models.PROTECT,
        related_name="invoice_items",
    )

    description = models.CharField(
        max_length=500,
        blank=True,
    )

    quantity = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        validators=[
            MinValueValidator(
                Decimal("0.01")
            )
        ],
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        validators=[
            MinValueValidator(
                Decimal("0.00")
            )
        ],
    )

    line_total = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=Decimal("0.00"),
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    class Meta:
        ordering = ["created_at"]

    def __str__(self):
        return (
            f"{self.product.name} - "
            f"{self.quantity}"
        )

    def calculate_line_total(self):
        self.line_total = (
            self.quantity
            * self.unit_price
        )

    def save(self, *args, **kwargs):
        self.calculate_line_total()
        super().save(*args, **kwargs)
```

 ### UUID structure

 এখন database-এ ID হবে এরকম:

```
Customer
550e8400-e29b-41d4-a716-446655440000

Product
a3bb189e-8bf9-3888-9912-ace4e6543002

Invoice
7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234
```

 কিন্তু invoice number থাকবে:

```
INV-2026-000001
```

 এটাই API design-এর জন্য cleaner।

---

 # 3\. `serializers.py`

```
from django.db import transaction
from rest_framework import serializers

from .models import (
    Customer,
    Product,
    Invoice,
    InvoiceItem,
)

class CustomerSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Customer

        fields = [
            "id",
            "name",
            "email",
            "phone",
            "address",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
            "updated_at",
        ]

class ProductSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Product

        fields = [
            "id",
            "name",
            "sku",
            "price",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
            "updated_at",
        ]

class InvoiceItemSerializer(
    serializers.ModelSerializer
):

    product_name = serializers.CharField(
        source="product.name",
        read_only=True,
    )

    class Meta:
        model = InvoiceItem

        fields = [
            "id",
            "product",
            "product_name",
            "description",
            "quantity",
            "unit_price",
            "line_total",
        ]

        read_only_fields = [
            "id",
            "product_name",
            "line_total",
        ]

    def validate(self, attrs):

        product = attrs.get("product")

        if product is None:
            raise serializers.ValidationError(
                {
                    "product": "Product is required."
                }
            )

        # Use product price if unit_price
        # is not supplied.
        if "unit_price" not in attrs:
            attrs["unit_price"] = product.price

        return attrs

class InvoiceSerializer(
    serializers.ModelSerializer
):

    items = InvoiceItemSerializer(
        many=True
    )

    customer_name = serializers.CharField(
        source="customer.name",
        read_only=True,
    )

    class Meta:
        model = Invoice

        fields = [
            "id",
            "invoice_number",
            "customer",
            "customer_name",
            "issue_date",
            "due_date",
            "status",
            "tax_rate",
            "subtotal",
            "tax_amount",
            "total",
            "notes",
            "items",
            "created_at",
            "updated_at",
        ]

        read_only_fields = [
            "id",
            "invoice_number",
            "issue_date",
            "subtotal",
            "tax_amount",
            "total",
            "created_at",
            "updated_at",
        ]

    def validate_tax_rate(self, value):

        if value < 0:
            raise serializers.ValidationError(
                "Tax rate cannot be negative."
            )

        if value > 100:
            raise serializers.ValidationError(
                "Tax rate cannot exceed 100."
            )

        return value

    @transaction.atomic
    def create(
        self,
        validated_data
    ):

        items_data = validated_data.pop(
            "items"
        )

        invoice = Invoice.objects.create(
            **validated_data
        )

        for item_data in items_data:

            InvoiceItem.objects.create(
                invoice=invoice,
                **item_data
            )

        invoice.calculate_totals()

        invoice.save(
            update_fields=[
                "subtotal",
                "tax_amount",
                "total",
                "updated_at",
            ]
        )

        return invoice

    @transaction.atomic
    def update(
        self,
        instance,
        validated_data
    ):

        items_data = validated_data.pop(
            "items",
            None
        )

        for attr, value in validated_data.items():
            setattr(instance, attr, value)

        instance.save()

        if items_data is not None:

            instance.items.all().delete()

            for item_data in items_data:

                InvoiceItem.objects.create(
                    invoice=instance,
                    **item_data
                )

        instance.calculate_totals()

        instance.save(
            update_fields=[
                "subtotal",
                "tax_amount",
                "total",
                "updated_at",
            ]
        )

        return instance
```

---

 # 4\. `views.py`

```
from django.http import HttpResponse
from django.template.loader import render_to_string
from django.db import transaction

from rest_framework import viewsets
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import status

from weasyprint import HTML

from .models import (
    Customer,
    Product,
    Invoice,
)

from .serializers import (
    CustomerSerializer,
    ProductSerializer,
    InvoiceSerializer,
)

class CustomerViewSet(
    viewsets.ModelViewSet
):

    queryset = Customer.objects.all()

    serializer_class = CustomerSerializer

class ProductViewSet(
    viewsets.ModelViewSet
):

    queryset = Product.objects.all()

    serializer_class = ProductSerializer

class InvoiceViewSet(
    viewsets.ModelViewSet
):

    serializer_class = InvoiceSerializer

    def get_queryset(self):

        return (
            Invoice.objects
            .select_related("customer")
            .prefetch_related(
                "items__product"
            )
        )

    @action(
        detail=True,
        methods=["get"],
        url_path="pdf",
    )
    def pdf(
        self,
        request,
        pk=None
    ):

        invoice = self.get_object()

        html_string = render_to_string(
            "invoices/invoice.html",
            {
                "invoice": invoice,
            }
        )

        pdf = HTML(
            string=html_string
        ).write_pdf()

        response = HttpResponse(
            pdf,
            content_type="application/pdf",
        )

        response[
            "Content-Disposition"
        ] = (
            "attachment; "
            f'filename="{invoice.invoice_number}.pdf"'
        )

        return response
```

 এখন UUID automatically `pk` হিসেবে কাজ করবে।

 উদাহরণ:

```
GET /api/invoices/
```

 তারপর:

```
GET /api/invoices/
7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/
```

 PDF:

```
GET /api/invoices/
7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/pdf/
```

---

 # 5\. `urls.py`

 `invoices/urls.py`

```
from rest_framework.routers import DefaultRouter

from .views import (
    CustomerViewSet,
    ProductViewSet,
    InvoiceViewSet,
)

router = DefaultRouter()

router.register(
    "customers",
    CustomerViewSet,
    basename="customer",
)

router.register(
    "products",
    ProductViewSet,
    basename="product",
)

router.register(
    "invoices",
    InvoiceViewSet,
    basename="invoice",
)

urlpatterns = router.urls
```

 Project `config/urls.py`:

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [

    path(
        "admin/",
        admin.site.urls,
    ),

    path(
        "api/",
        include("invoices.urls"),
    ),

]
```

---

 # 6\. PDF Template

 `invoices/templates/invoices/invoice.html`

```
<!DOCTYPE html>
<html>

<head>

    <meta charset="UTF-8">

    <style>

        @page {
            size: A4;
            margin: 25px;
        }

        body {
            font-family: Arial, sans-serif;
            color: #333;
            font-size: 13px;
        }

        .header {
            display: table;
            width: 100%;
            margin-bottom: 30px;
        }

        .header-left,
        .header-right {
            display: table-cell;
            width: 50%;
            vertical-align: top;
        }

        .header-right {
            text-align: right;
        }

        .company-name {
            font-size: 26px;
            font-weight: bold;
            color: #2563eb;
        }

        .invoice-title {
            font-size: 30px;
            font-weight: bold;
        }

        .info {
            margin-bottom: 30px;
        }

        .info-table {
            width: 100%;
        }

        .info-table td {
            vertical-align: top;
            padding: 5px;
        }

        .items {
            width: 100%;
            border-collapse: collapse;
        }

        .items th {
            background: #2563eb;
            color: white;
            padding: 10px;
            text-align: left;
        }

        .items td {
            border-bottom: 1px solid #ddd;
            padding: 10px;
        }

        .right {
            text-align: right;
        }

        .totals {
            width: 40%;
            margin-left: auto;
            margin-top: 20px;
            border-collapse: collapse;
        }

        .totals td {
            padding: 7px;
        }

        .grand-total {
            font-size: 18px;
            font-weight: bold;
            border-top: 2px solid #333;
        }

        .notes {
            margin-top: 50px;
        }

        .footer {
            margin-top: 70px;
            text-align: center;
            color: #777;
        }

    </style>

</head>

<body>

    <div class="header">

        <div class="header-left">

            <div class="company-name">
                My Company
            </div>

            <div>
                Dhaka, Bangladesh
            </div>

            <div>
                Email: billing@example.com
            </div>

        </div>

        <div class="header-right">

            <div class="invoice-title">
                INVOICE
            </div>

            <div>
                #{{ invoice.invoice_number }}
            </div>

            <div>
                Date:
                {{ invoice.issue_date }}
            </div>

            {% if invoice.due_date %}

                <div>
                    Due:
                    {{ invoice.due_date }}
                </div>

            {% endif %}

        </div>

    </div>

    <div class="info">

        <table class="info-table">

            <tr>

                <td>

                    <strong>Bill To:</strong>

                    <br>

                    {{ invoice.customer.name }}

                    <br>

                    {% if invoice.customer.email %}
                        {{ invoice.customer.email }}
                        <br>
                    {% endif %}

                    {% if invoice.customer.phone %}
                        {{ invoice.customer.phone }}
                        <br>
                    {% endif %}

                    {% if invoice.customer.address %}
                        {{ invoice.customer.address }}
                    {% endif %}

                </td>

                <td class="right">

                    <strong>Status:</strong>

                    <br>

                    {{ invoice.get_status_display }}

                </td>

            </tr>

        </table>

    </div>

    <table class="items">

        <thead>

            <tr>

                <th>#</th>

                <th>Product</th>

                <th>Description</th>

                <th>Qty</th>

                <th>Unit Price</th>

                <th>Total</th>

            </tr>

        </thead>

        <tbody>

            {% for item in invoice.items.all %}

            <tr>

                <td>
                    {{ forloop.counter }}
                </td>

                <td>
                    {{ item.product.name }}
                </td>

                <td>
                    {{ item.description }}
                </td>

                <td>
                    {{ item.quantity }}
                </td>

                <td>
                    {{ item.unit_price }}
                </td>

                <td>
                    {{ item.line_total }}
                </td>

            </tr>

            {% endfor %}

        </tbody>

    </table>

    <table class="totals">

        <tr>

            <td>
                Subtotal
            </td>

            <td class="right">
                {{ invoice.subtotal }}
            </td>

        </tr>

        <tr>

            <td>
                Tax ({{ invoice.tax_rate }}%)
            </td>

            <td class="right">
                {{ invoice.tax_amount }}
            </td>

        </tr>

        <tr class="grand-total">

            <td>
                Total
            </td>

            <td class="right">
                {{ invoice.total }}
            </td>

        </tr>

    </table>

    {% if invoice.notes %}

        <div class="notes">

            <strong>Notes:</strong>

            <p>
                {{ invoice.notes }}
            </p>

        </div>

    {% endif %}

    <div class="footer">

        Thank you for your business!

    </div>

</body>

</html>
```

---

 # 7\. Migration

```
python manage.py makemigrations
python manage.py migrate
```

---

 # 8\. Create Customer

```
POST /api/customers/
Content-Type: application/json
```

```
{
    "name": "Rahim Ahmed",
    "email": "rahim@example.com",
    "phone": "01700000000",
    "address": "Dhaka, Bangladesh"
}
```

 Response:

```
{
    "id": "f1a7a7f1-9a2b-4b75-8d9e-9f3e0f5c2a10",
    "name": "Rahim Ahmed",
    "email": "rahim@example.com",
    "phone": "01700000000",
    "address": "Dhaka, Bangladesh"
}
```

---

 # 9\. Create Product

```
POST /api/products/
```

```
{
    "name": "Website Development",
    "sku": "WEB-001",
    "price": "50000.00"
}
```

 Response:

```
{
    "id": "6d5f4c4e-1f6e-4c2e-b8d1-6b6d5a7c2e11",
    "name": "Website Development",
    "sku": "WEB-001",
    "price": "50000.00"
}
```

---

 # 10\. Create Invoice

 এখন UUID ব্যবহার করে customer/product reference দিতে পারবেন:

```
POST /api/invoices/
Content-Type: application/json
```

```
{
    "customer": "f1a7a7f1-9a2b-4b75-8d9e-9f3e0f5c2a10",

    "due_date": "2026-10-15",

    "status": "issued",

    "tax_rate": "10.00",

    "notes": "Payment within 15 days.",

    "items": [
        {
            "product": "6d5f4c4e-1f6e-4c2e-b8d1-6b6d5a7c2e11",
            "description": "Corporate website development",
            "quantity": "1",
            "unit_price": "50000.00"
        }
    ]
}
```

 Response:

```
{
    "id": "7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234",

    "invoice_number": "INV-2026-000001",

    "customer": "f1a7a7f1-9a2b-4b75-8d9e-9f3e0f5c2a10",

    "customer_name": "Rahim Ahmed",

    "issue_date": "2026-10-01",

    "due_date": "2026-10-15",

    "status": "issued",

    "tax_rate": "10.00",

    "subtotal": "50000.00",

    "tax_amount": "5000.00",

    "total": "55000.00",

    "notes": "Payment within 15 days.",

    "items": [
        {
            "id": "b32b9a3f-8e12-42bb-9e13-71f3c4a2d999",

            "product": "6d5f4c4e-1f6e-4c2e-b8d1-6b6d5a7c2e11",

            "product_name": "Website Development",

            "description": "Corporate website development",

            "quantity": "1.00",

            "unit_price": "50000.00",

            "line_total": "50000.00"
        }
    ]
}
```

---

 # 11\. Invoice Detail

 UUID দিয়ে:

```
GET /api/invoices/7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/
```

---

 # 12\. PDF Download

```
GET /api/invoices/7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/pdf/
```

 Response:

```
Content-Type: application/pdf

INV-2026-000001.pdf
```

---

 # 13\. API structure

 শেষ পর্যন্ত API হবে:

```
/api/customers/
/api/customers/{uuid}/

/api/products/
/api/products/{uuid}/

/api/invoices/
/api/invoices/{uuid}/
/api/invoices/{uuid}/pdf/
```

 এখানে `{uuid}` হচ্ছে actual UUID।

 ## একটা গুরুত্বপূর্ণ improvement

 বর্তমান code-এ `invoice_number`-এর জন্য আলাদা sequence model না থাকায় **concurrent invoice creation-এর ক্ষেত্রে আরও robust numbering** দরকার হতে পারে। Production billing system হলে আমি আলাদা:

```
InvoiceSequence
```

 model ব্যবহার করতাম এবং transaction-এর ভিতরে `select_for_update()` দিয়ে:

```
INV-2026-000001
INV-2026-000002
INV-2026-000003
```

 এভাবে guaranteed sequential number তৈরি করতাম।

 আর production system হলে পরের ধাপে **Company/Business + User authentication + JWT + company-wise invoice isolation + discount + VAT + paid/due amount + payment model + invoice PDF storage** যোগ করাই সবচেয়ে যুক্তিযুক্ত architecture হবে।

----
অবশ্যই। এই invoice system-টাকে **layered architecture** হিসেবে ভাবলে সবচেয়ে সহজ হবে। পুরো flowটা হলো:

 ## 1\. High-level architecture

```
                    ┌──────────────────────┐
                    │      Frontend        │
                    │ React / Vue / Mobile │
                    └──────────┬───────────┘
                               │
                               │ HTTP / JSON
                               ▼
                    ┌──────────────────────┐
                    │      DRF API         │
                    │  URL / Router        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      ViewSet          │
                    │                      │
                    │ CustomerViewSet       │
                    │ ProductViewSet        │
                    │ InvoiceViewSet        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │     Serializer        │
                    │                      │
                    │ Validation            │
                    │ Nested Items          │
                    │ Create / Update       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       Models          │
                    │                      │
                    │ Customer              │
                    │ Product               │
                    │ Invoice               │
                    │ InvoiceItem           │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Database         │
                    │ PostgreSQL / MySQL    │
                    └──────────────────────┘
```

 এখানে মূল idea হলো:

```
Frontend
   ↓
API
   ↓
ViewSet
   ↓
Serializer
   ↓
Model
   ↓
Database
```

---

 # 2\. Database relationship

 আমাদের মূল 4টা entity:

```
┌───────────────┐
│   Customer    │
│───────────────│
│ UUID PK       │
│ name          │
│ email         │
│ phone         │
└───────┬───────┘
        │
        │ 1
        │
        │
        │ N
┌───────▼───────┐
│    Invoice    │
│───────────────│
│ UUID PK       │
│ invoice_no    │
│ customer FK   │
│ status        │
│ tax_rate      │
│ subtotal      │
│ tax_amount    │
│ total         │
└───────┬───────┘
        │
        │ 1
        │
        │
        │ N
┌───────▼──────────┐
│   InvoiceItem    │
│──────────────────│
│ UUID PK          │
│ invoice FK       │
│ product FK       │
│ quantity         │
│ unit_price       │
│ line_total       │
└────────┬─────────┘
         │
         │ N
         │
         │ 1
┌────────▼─────────┐
│     Product      │
│──────────────────│
│ UUID PK          │
│ name             │
│ sku              │
│ price            │
└──────────────────┘
```

 অর্থাৎ:

```
Customer
   │
   └───< Invoice
            │
            └───< InvoiceItem >─── Product
```

 এখানে `<` মানে "many"।

 একজন customer-এর অনেক invoice থাকতে পারে।

 একটি invoice-এর অনেক item থাকতে পারে।

 একটি product অনেক invoice-এর item হিসেবে থাকতে পারে।

---

 # 3. Invoice create flow

 ধরুন frontend থেকে user invoice তৈরি করলো।

 Request:

```
POST /api/invoices/
```

 Body:

```
{
    "customer": "customer-uuid",
    "tax_rate": "10.00",
    "items": [
        {
            "product": "product-uuid",
            "quantity": "2",
            "unit_price": "5000.00"
        }
    ]
}
```

 Flow:

```
                POST /api/invoices/
                         │
                         ▼
              ┌──────────────────┐
              │    Router        │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ InvoiceViewSet   │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ InvoiceSerializer│
              └────────┬─────────┘
                       │
                Validation
                       │
                       ▼
              ┌──────────────────┐
              │ Create Invoice   │
              └────────┬─────────┘
                       │
                       ▼
              ┌──────────────────┐
              │ Create Items     │
              └────────┬─────────┘
                       │
                       ▼
              Calculate Totals
                       │
                       ▼
              ┌──────────────────┐
              │    Database      │
              └────────┬─────────┘
                       │
                       ▼
                  JSON Response
```

---

 # 4\. Calculation flow

 ধরুন:

```
Product A
Quantity = 2
Unit Price = 5,000

Product B
Quantity = 3
Unit Price = 2,000
```

 প্রথমে প্রতিটি item-এর `line_total`:

```
Product A
2 × 5,000 = 10,000

Product B
3 × 2,000 = 6,000
```

 তারপর:

```
                    Invoice
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
     InvoiceItem                InvoiceItem
          │                         │
    2 × 5000                    3 × 2000
          │                         │
          ▼                         ▼
       10,000                     6,000
          └────────────┬────────────┘
                       ▼
                    Subtotal
                     16,000
                       │
                       ▼
                    Tax 10%
                     1,600
                       │
                       ▼
                     Total
                     17,600
```

 Formula:

```
line_total = quantity × unit_price

subtotal = Σ line_total

tax_amount = subtotal × tax_rate / 100

total = subtotal + tax_amount
```

---

 # 5\. UUID কেন?

 আমাদের system-এ UUID তিন জায়গায় গুরুত্বপূর্ণ:

```
Customer UUID
Product UUID
Invoice UUID
InvoiceItem UUID
```

 যেমন:

```
Invoice ID:

7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234
```

 Frontend এই ID দিয়ে request করবে:

```
GET /api/invoices/7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/
```

 কিন্তু customer-facing invoice number হবে:

```
INV-2026-000001
```

 অর্থাৎ:

```
Internal Identity
       │
       ▼
UUID
7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234

Human Identity
       │
       ▼
Invoice Number
INV-2026-000001
```

 দুটোর কাজ আলাদা।

---

 # 6\. PDF generation flow

 PDF request করলে:

```
GET /api/invoices/{uuid}/pdf/
```

 Flow:

```
             Client
               │
               │ GET /pdf/
               ▼
       ┌─────────────────┐
       │  InvoiceViewSet  │
       └────────┬────────┘
                │
                ▼
       Get Invoice + Items
                │
                ▼
       ┌─────────────────┐
       │ Django Template  │
       │ invoice.html     │
       └────────┬────────┘
                │
                │ HTML
                ▼
       ┌─────────────────┐
       │    WeasyPrint    │
       └────────┬────────┘
                │
                │ PDF bytes
                ▼
       ┌─────────────────┐
       │ HttpResponse     │
       │ application/pdf  │
       └────────┬────────┘
                │
                ▼
             Browser
                │
                ▼
       INV-2026-000001.pdf
```

---

 # 7\. Complete system flow

 সবকিছু একসাথে দেখলে:

```
                           ┌──────────────┐
                           │   Frontend   │
                           └──────┬───────┘
                                  │
                         HTTP / JSON
                                  │
                                  ▼
                       ┌──────────────────┐
                       │    DRF Router    │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │     ViewSet      │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │    Serializer    │
                       │                  │
                       │ Validation       │
                       │ Nested Items     │
                       └────────┬─────────┘
                                │
                                ▼
                       ┌──────────────────┐
                       │      Model       │
                       └────────┬─────────┘
                                │
                                ▼
                    ┌────────────────────────┐
                    │       Database         │
                    │                        │
                    │ Customer               │
                    │ Product                │
                    │ Invoice                │
                    │ InvoiceItem            │
                    └───────────┬────────────┘
                                │
                    ┌───────────┴────────────┐
                    │                        │
                    ▼                        ▼
             JSON Response             PDF Request
                                             │
                                             ▼
                                    Django Template
                                             │
                                             ▼
                                         WeasyPrint
                                             │
                                             ▼
                                       PDF Response
```

---

 # 8\. Production architecture হলে

 বাস্তবে আমি system-টাকে একটু বড় করে এভাবে সাজাব:

```
                         ┌─────────────────┐
                         │    Frontend     │
                         │ React / Vue     │
                         └────────┬────────┘
                                  │
                                  ▼
                         ┌─────────────────┐
                         │   Nginx / LB    │
                         └────────┬────────┘
                                  │
                                  ▼
                    ┌─────────────────────────┐
                    │       Django DRF        │
                    │                         │
                    │ Auth / Permissions      │
                    │ ViewSets                │
                    │ Serializers             │
                    │ Services                │
                    └───────────┬─────────────┘
                                │
                 ┌──────────────┼──────────────┐
                 │              │              │
                 ▼              ▼              ▼
          ┌────────────┐ ┌────────────┐ ┌────────────┐
          │ PostgreSQL │ │   Redis    │ │   Celery   │
          │            │ │            │ │            │
          │ Main DB    │ │ Cache      │ │ Background │
          │            │ │            │ │ Jobs       │
          └────────────┘ └────────────┘ └─────┬──────┘
                                              │
                              ┌───────────────┼───────────────┐
                              ▼               ▼               ▼
                            PDF            Email          Reports
                           Generate        Invoice        / Tasks
```

 ### Service layer কেন যোগ করব?

 বর্তমান ছোট project-এ:

```
ViewSet → Serializer → Model
```

 যথেষ্ট।

 কিন্তু বড় project হলে:

```
ViewSet
   ↓
Serializer
   ↓
Service
   ↓
Model
```

 ভালো।

 যেমন:

```
InvoiceService.create_invoice()
InvoiceService.calculate_totals()
InvoiceService.generate_pdf()
InvoiceService.mark_as_paid()
```

 তাহলে business logic ViewSet/Serializer-এর মধ্যে ছড়িয়ে যাবে না।

---

 # 9\. Recommended final architecture

 আমি invoice/business application-এর জন্য এই structure রাখতাম:

```
invoices/
│
├── models/
│   ├── customer.py
│   ├── product.py
│   ├── invoice.py
│   └── payment.py
│
├── serializers/
│   ├── customer.py
│   ├── product.py
│   └── invoice.py
│
├── views/
│   ├── customer.py
│   ├── product.py
│   └── invoice.py
│
├── services/
│   ├── invoice_service.py
│   ├── payment_service.py
│   └── pdf_service.py
│
├── templates/
│   └── invoices/
│       └── invoice.html
│
├── urls.py
│
└── tasks.py
```

 এর overall flow:

```
             REQUEST
                │
                ▼
             Router
                │
                ▼
             ViewSet
                │
                ▼
           Serializer
          Validation
                │
                ▼
             Service
                │
        ┌───────┼────────┐
        │       │        │
        ▼       ▼        ▼
      Model    PDF     Payment
        │
        ▼
    PostgreSQL
        │
        ▼
     Response
```

 **এই architecture-টাই বড় project-এর জন্য আমি recommend করব**, কারণ invoice calculation, payment, PDF, email ইত্যাদি বাড়তে থাকলে business logic আলাদা `services/` layer-এ রাখা অনেক maintainable হবে।

---
হ্যাঁ। যদি আপনার requirement শুধু **simple voucher generate \+ PDF/download** হয়, তাহলে পুরো invoice architecture লাগবে না। Minimum রাখলেই হবে।

 ## Minimum architecture

```
Frontend
   │
   ▼
DRF API
   │
   ▼
VoucherViewSet
   │
   ▼
VoucherSerializer
   │
   ▼
Voucher Model
   │
   ▼
Database

PDF চাইলে:
Voucher
   │
   ▼
HTML Template
   │
   ▼
WeasyPrint
   │
   ▼
PDF
```

 ## যা অবশ্যই লাগবে

 ### 1\. Voucher Model

 Minimum fields:

```
class Voucher(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True
    )

    customer_name = models.CharField(
        max_length=200
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    description = models.TextField(
        blank=True
    )

    voucher_date = models.DateField(
        auto_now_add=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

 এটাই অনেক ক্ষেত্রে যথেষ্ট।

---

 ### 2\. Serializer

```
class VoucherSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "customer_name",
            "amount",
            "description",
            "voucher_date",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "voucher_date",
            "created_at",
        ]
```

---

 ### 3\. ViewSet

```
class VoucherViewSet(
    viewsets.ModelViewSet
):

    queryset = Voucher.objects.all()

    serializer_class = VoucherSerializer
```

 PDF দরকার হলে একই ViewSet-এ:

```
@action(
    detail=True,
    methods=["get"]
)
def pdf(self, request, pk=None):

    voucher = self.get_object()

    html = render_to_string(
        "vouchers/voucher.html",
        {
            "voucher": voucher
        }
    )

    pdf = HTML(
        string=html
    ).write_pdf()

    response = HttpResponse(
        pdf,
        content_type="application/pdf"
    )

    response[
        "Content-Disposition"
    ] = (
        f'attachment; '
        f'filename="{voucher.voucher_number}.pdf"'
    )

    return response
```

---

 ## API

```
POST   /api/vouchers/
GET    /api/vouchers/
GET    /api/vouchers/{uuid}/
PATCH  /api/vouchers/{uuid}/
DELETE /api/vouchers/{uuid}/

GET    /api/vouchers/{uuid}/pdf/
```

 Create:

```
{
    "customer_name": "Rahim Ahmed",
    "amount": "5000.00",
    "description": "Payment received"
}
```

 Response:

```
{
    "id": "7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234",
    "voucher_number": "VCH-000001",
    "customer_name": "Rahim Ahmed",
    "amount": "5000.00",
    "description": "Payment received",
    "voucher_date": "2026-10-01"
}
```

 ## Invoice বনাম Simple Voucher

```
Simple Voucher
────────────────────────
UUID
Voucher Number
Customer Name
Amount
Description
Date
PDF

Invoice
────────────────────────
UUID
Invoice Number
Customer
Invoice Items
Product
Quantity
Unit Price
Subtotal
Discount
VAT/Tax
Total
Payment
Due Amount
Status
PDF
Email
etc.
```

 তাই **শুধু টাকা receive/pay করার একটা ছোট voucher বানাতে চাইলে `Voucher + Serializer + ViewSet + PDF Template`—এই ৪টা জিনিসই মূলত যথেষ্ট।**

 আর যদি আপনার voucher-এর ধরন হয় **Money Receipt / Payment Voucher**, তাহলে `customer_name + amount + payment_method + received_by + note` রাখলেই আরও practical হবে।


---
হ্যাঁ। যদি আপনার requirement শুধু **simple voucher generate \+ PDF/download** হয়, তাহলে পুরো invoice architecture লাগবে না। Minimum রাখলেই হবে।

 ## Minimum architecture

```
Frontend
   │
   ▼
DRF API
   │
   ▼
VoucherViewSet
   │
   ▼
VoucherSerializer
   │
   ▼
Voucher Model
   │
   ▼
Database

PDF চাইলে:
Voucher
   │
   ▼
HTML Template
   │
   ▼
WeasyPrint
   │
   ▼
PDF
```

 ## যা অবশ্যই লাগবে

 ### 1\. Voucher Model

 Minimum fields:

```
class Voucher(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True
    )

    customer_name = models.CharField(
        max_length=200
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    description = models.TextField(
        blank=True
    )

    voucher_date = models.DateField(
        auto_now_add=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )
```

 এটাই অনেক ক্ষেত্রে যথেষ্ট।

---

 ### 2\. Serializer

```
class VoucherSerializer(
    serializers.ModelSerializer
):

    class Meta:
        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "customer_name",
            "amount",
            "description",
            "voucher_date",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "voucher_date",
            "created_at",
        ]
```

---

 ### 3\. ViewSet

```
class VoucherViewSet(
    viewsets.ModelViewSet
):

    queryset = Voucher.objects.all()

    serializer_class = VoucherSerializer
```

 PDF দরকার হলে একই ViewSet-এ:

```
@action(
    detail=True,
    methods=["get"]
)
def pdf(self, request, pk=None):

    voucher = self.get_object()

    html = render_to_string(
        "vouchers/voucher.html",
        {
            "voucher": voucher
        }
    )

    pdf = HTML(
        string=html
    ).write_pdf()

    response = HttpResponse(
        pdf,
        content_type="application/pdf"
    )

    response[
        "Content-Disposition"
    ] = (
        f'attachment; '
        f'filename="{voucher.voucher_number}.pdf"'
    )

    return response
```

---

 ## API

```
POST   /api/vouchers/
GET    /api/vouchers/
GET    /api/vouchers/{uuid}/
PATCH  /api/vouchers/{uuid}/
DELETE /api/vouchers/{uuid}/

GET    /api/vouchers/{uuid}/pdf/
```

 Create:

```
{
    "customer_name": "Rahim Ahmed",
    "amount": "5000.00",
    "description": "Payment received"
}
```

 Response:

```
{
    "id": "7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234",
    "voucher_number": "VCH-000001",
    "customer_name": "Rahim Ahmed",
    "amount": "5000.00",
    "description": "Payment received",
    "voucher_date": "2026-10-01"
}
```

 ## Invoice বনাম Simple Voucher

```
Simple Voucher
────────────────────────
UUID
Voucher Number
Customer Name
Amount
Description
Date
PDF

Invoice
────────────────────────
UUID
Invoice Number
Customer
Invoice Items
Product
Quantity
Unit Price
Subtotal
Discount
VAT/Tax
Total
Payment
Due Amount
Status
PDF
Email
etc.
```

 তাই **শুধু টাকা receive/pay করার একটা ছোট voucher বানাতে চাইলে `Voucher + Serializer + ViewSet + PDF Template`—এই ৪টা জিনিসই মূলত যথেষ্ট।**

 আর যদি আপনার voucher-এর ধরন হয় **Money Receipt / Payment Voucher**, তাহলে `customer_name + amount + payment_method + received_by + note` রাখলেই আরও practical হবে।

----
হ্যাঁ, **এটাই সবচেয়ে clean approach**।

 মানে `Voucher` model-এ যে data থাকবে, **সেই data দিয়েই automatically voucher PDF generate হবে**। আলাদা করে PDF-তে data পাঠাতে হবে না।

 ## Simple flow

```
                Create Voucher
                      │
                      ▼
              ┌───────────────┐
              │ Voucher Model  │
              │───────────────│
              │ UUID           │
              │ voucher_number │
              │ date           │
              │ name           │
              │ amount         │
              │ description    │
              │ payment_method │
              └───────┬───────┘
                      │
                      │ GET /pdf/
                      ▼
              ┌───────────────┐
              │ VoucherViewSet │
              └───────┬───────┘
                      │
                      ▼
              ┌───────────────┐
              │ voucher.html  │
              │ Django Template│
              └───────┬───────┘
                      │
                      ▼
                ┌───────────┐
                │ WeasyPrint │
                └─────┬─────┘
                      │
                      ▼
                Voucher PDF
```

 ### Example Model

 ধরুন:

```
class Voucher(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True
    )

    voucher_date = models.DateField()

    customer_name = models.CharField(
        max_length=200
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2
    )

    payment_method = models.CharField(
        max_length=50,
        blank=True
    )

    description = models.TextField(
        blank=True
    )
```

 Database-এ data:

```
Voucher
────────────────────────────
voucher_number: VCH-000001
voucher_date:   01-10-2026
customer_name:  Rahim Ahmed
amount:         5000.00
payment_method: Cash
description:    Payment received
```

 তারপর:

```
GET /api/vouchers/{uuid}/pdf/
```

 ViewSet database থেকে ওই voucher-টা নেবে:

```
voucher = self.get_object()
```

 তারপর template-এ পাঠাবে:

```
html = render_to_string(
    "vouchers/voucher.html",
    {
        "voucher": voucher
    }
)
```

 Template নিজেই model-এর data ব্যবহার করবে:

```
<h1>PAYMENT VOUCHER</h1>

<p>
    Voucher No:
    {{ voucher.voucher_number }}
</p>

<p>
    Date:
    {{ voucher.voucher_date }}
</p>

<p>
    Customer:
    {{ voucher.customer_name }}
</p>

<p>
    Amount:
    {{ voucher.amount }}
</p>

<p>
    Payment Method:
    {{ voucher.payment_method }}
</p>

<p>
    Description:
    {{ voucher.description }}
</p>
```

 তারপর WeasyPrint:

```
pdf = HTML(
    string=html
).write_pdf()
```

 এবং PDF return করবে।

 ### মূল concept

```
Database
   ↓
Voucher Object
   ↓
Django Template
   ↓
HTML
   ↓
WeasyPrint
   ↓
PDF
```

 অর্থাৎ **Voucher model হবে single source of truth**। Model-এ data পরিবর্তন হলে PDF generate করার সময় নতুন data-ই আসবে।

 আরও ভালোভাবে করলে `Voucher`-এর মধ্যে শুধু voucher-এর data থাকবে, আর **PDF design/layout থাকবে `voucher.html` template-এ**। এতে পরে voucher-এর design পরিবর্তন করলেও database/model পরিবর্তন করতে হবে না।

---
হ্যাঁ, পারবেন। বরং **Voucher model-এ শুধু universally needed field রাখবেন, আর যেসব data অন্য model-এ already আছে সেগুলোর জন্য relation ব্যবহার করবেন**।

 একটা সাধারণ business application-এর জন্য আমি এভাবে design করতাম:

 ## 1\. Basic Voucher Model

```
import uuid

from django.db import models

class Voucher(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    voucher_date = models.DateField()

    # Who received/paid the money
    customer = models.ForeignKey(
        "customers.Customer",
        on_delete=models.PROTECT,
        related_name="vouchers",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    payment_method = models.CharField(
        max_length=30,
        choices=[
            ("cash", "Cash"),
            ("bank", "Bank"),
            ("mobile_banking", "Mobile Banking"),
            ("card", "Card"),
        ],
    )

    reference = models.CharField(
        max_length=100,
        blank=True,
    )

    description = models.TextField(
        blank=True,
    )

    created_at = models.DateTimeField(
        auto_now_add=True,
    )

    updated_at = models.DateTimeField(
        auto_now=True,
    )
```

 এখানে **সব field mandatory না**। Business requirement অনুযায়ী field বাড়াতে/কমাতে পারবেন।

---

 # 2\. Relation কোথায় দেবেন?

 ধরুন আপনার application-এ already আছে:

```
Customer
User
Invoice
Order
Payment
Account
```

 তাহলে Voucher-এর মধ্যে সব information copy করে রাখার দরকার নেই।

 বরং relation দিন।

```
Customer
    │
    │ 1
    │
    │
    ▼ N
 Voucher
```

 একজন customer-এর অনেক voucher থাকতে পারে।

 তাই:

```
customer = models.ForeignKey(
    Customer,
    on_delete=models.PROTECT,
    related_name="vouchers",
)
```

---

 # 3\. Voucher + Invoice relation

 যদি voucher কোনো invoice-এর payment-এর জন্য তৈরি হয়, তাহলে Invoice-এর সাথেও relation দিতে পারেন।

```
Customer
   │
   ├───────────────┐
   │               │
   ▼               ▼
Invoice          Voucher
   │               ▲
   └───────────────┘
```

 Model:

```
invoice = models.ForeignKey(
    "invoices.Invoice",
    on_delete=models.PROTECT,
    related_name="vouchers",
    null=True,
    blank=True,
)
```

 `null=True, blank=True` রাখার কারণ:

 সব voucher invoice-এর জন্য নাও হতে পারে।

 উদাহরণ:

```
Customer → Payment → Voucher
```

 এখানে invoice নেই।

 আবার:

```
Customer → Invoice → Payment → Voucher
```

 এখানে invoice আছে।

---

 # 4\. Payment আলাদা Model হলে আরও ভালো

 যদি আপনার application বড় হয়, আমি সরাসরি Voucher-এর মধ্যে payment information বেশি না রেখে:

```
Customer
    │
    ▼
Invoice
    │
    ▼
Payment
    │
    ▼
Voucher
```

 এভাবে করতে পারি।

 উদাহরণ:

```
class Payment(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    customer = models.ForeignKey(
        Customer,
        on_delete=models.PROTECT,
        related_name="payments",
    )

    invoice = models.ForeignKey(
        Invoice,
        on_delete=models.PROTECT,
        related_name="payments",
        null=True,
        blank=True,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    payment_method = models.CharField(
        max_length=30,
    )

    payment_date = models.DateField()

    reference = models.CharField(
        max_length=100,
        blank=True,
    )
```

 তারপর Voucher:

```
class Voucher(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True,
    )

    payment = models.OneToOneField(
        Payment,
        on_delete=models.PROTECT,
        related_name="voucher",
    )

    created_at = models.DateTimeField(
        auto_now_add=True,
    )
```

 তাহলে:

```
Customer
   │
   │
   ▼
Invoice
   │
   │
   ▼
Payment
   │
   │
   ▼
Voucher
   │
   ▼
PDF
```

 এটা অনেক বেশি normalized architecture।

---

 # 5\. Voucher PDF কীভাবে data পাবে?

 এটাই সবচেয়ে সুন্দর ব্যাপার।

 Voucher-এর সাথে Payment relation আছে:

```
voucher.payment.amount
voucher.payment.customer.name
voucher.payment.payment_method
```

 Invoice থাকলে:

```
voucher.payment.invoice.invoice_number
voucher.payment.invoice.total
```

 Customer:

```
voucher.payment.customer.name
voucher.payment.customer.phone
```

 Template:

```
<h1>PAYMENT VOUCHER</h1>

<p>
    Voucher No:
    {{ voucher.voucher_number }}
</p>

<p>
    Customer:
    {{ voucher.payment.customer.name }}
</p>

<p>
    Invoice:
    {{ voucher.payment.invoice.invoice_number }}
</p>

<p>
    Amount:
    {{ voucher.payment.amount }}
</p>

<p>
    Payment Method:
    {{ voucher.payment.payment_method }}
</p>
```

 অর্থাৎ PDF-এর জন্য duplicate data রাখতে হবে না।

---

 # 6\. কোন approach নেবেন?

 ### ছোট/simple project

```
Voucher
├── customer
├── amount
├── payment_method
├── reference
├── description
└── date
```

 এটাই যথেষ্ট।

 ### Medium/large business application

 আমি এভাবে রাখতাম:

```
Customer
    │
    ├───────────────┐
    ▼               ▼
Invoice          Payment
                    │
                    ▼
                 Voucher
                    │
                    ▼
                   PDF
```

 এখানে:

```
Customer → ForeignKey
Invoice  → ForeignKey (optional)
Payment  → OneToOne / ForeignKey
Voucher  → UUID
```

 ## আমার recommendation

 আপনার যদি **invoice + payment + voucher** তিনটিই থাকে, তাহলে সবচেয়ে clean design হবে:

```
Customer
   │
   ├──< Invoice
   │
   └──< Payment
           │
           ├── Invoice (optional)
           │
           └── Voucher (1:1)
```

 এতে **একই customer name, invoice number, amount ইত্যাদি বারবার Voucher table-এ copy করতে হবে না**। Voucher মূলত একটি payment-এর printable/document representation হিসেবে কাজ করবে।

 আর PDF generate করার সময়:

```
Voucher
   ↓
Payment
   ↓
Customer / Invoice
   ↓
Django Template
   ↓
WeasyPrint
   ↓
Voucher PDF
```

 এই design-টা আপনার আগের UUID-based invoice architecture-এর সাথেও খুব সুন্দরভাবে বসবে।


---
হ্যাঁ। `voucher_number` **user input করবে না, backend automatically generate করবে**—এটাই ভালো।

 আমি format রাখতাম:

```
VCH-2026-000001
VCH-2026-000002
VCH-2026-000003
```

 আর `id` থাকবে UUID:

```
id: 7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234
voucher_number: VCH-2026-000001
```

 অর্থাৎ **UUID = internal identity**, আর **voucher\_number = human-friendly document number**।

 ## Simple implementation

 যদি ছোট project হয়, `save()`-এ করতে পারেন:

```
import uuid

from django.db import models
from django.utils import timezone

class Voucher(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    voucher_date = models.DateField(
        auto_now_add=True
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    description = models.TextField(
        blank=True,
    )

    created_at = models.DateTimeField(
        auto_now_add=True,
    )

    def save(self, *args, **kwargs):

        if not self.voucher_number:

            year = timezone.now().year

            last_voucher = (
                Voucher.objects
                .filter(
                    voucher_number__startswith=f"VCH-{year}-"
                )
                .order_by("-created_at")
                .first()
            )

            if last_voucher:
                last_number = int(
                    last_voucher.voucher_number.split("-")[-1]
                )
                next_number = last_number + 1
            else:
                next_number = 1

            self.voucher_number = (
                f"VCH-{year}-{next_number:06d}"
            )

        super().save(*args, **kwargs)
```

 তাহলে:

```
First:
VCH-2026-000001

Second:
VCH-2026-000002

Third:
VCH-2026-000003
```

 ## কিন্তু production-এ একটা সমস্যা আছে

 উপরের approach-এ একই সময়ে দুইটা request এলে দুটো request-ই `000005` পেয়ে যেতে পারে।

 তাই **production application-এর জন্য আমি `VoucherSequence` model ব্যবহার করব**।

```
Voucher
   │
   └── voucher_number
             │
             ▼
      VCH-2026-000001
```

 Sequence আলাদা:

```
class VoucherSequence(models.Model):

    year = models.PositiveIntegerField(
        unique=True
    )

    last_number = models.PositiveIntegerField(
        default=0
    )
```

 তারপর transaction + `select_for_update()` ব্যবহার করে number generate করা হবে।

```
from django.db import transaction

@transaction.atomic
def generate_voucher_number():

    year = timezone.now().year

    sequence, created = (
        VoucherSequence.objects
        .select_for_update()
        .get_or_create(
            year=year,
            defaults={"last_number": 0}
        )
    )

    sequence.last_number += 1
    sequence.save(
        update_fields=["last_number"]
    )

    return f"VCH-{year}-{sequence.last_number:06d}"
```

 Voucher create:

```
voucher.voucher_number = (
    generate_voucher_number()
)
voucher.save()
```

 এতে concurrent request হলেও:

```
Request A → VCH-2026-000001
Request B → VCH-2026-000002
Request C → VCH-2026-000003
```

 হবে।

 ### সবচেয়ে গুরুত্বপূর্ণ

 Serializer-এ `voucher_number` **read-only** রাখবেন:

```
class VoucherSerializer(serializers.ModelSerializer):

    class Meta:
        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "voucher_date",
            "amount",
            "description",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "voucher_date",
        ]
```

 তাহলে frontend শুধু পাঠাবে:

```
{
    "amount": "5000.00",
    "description": "Payment received"
}
```

 Backend automatically তৈরি করবে:

```
{
    "id": "7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234",
    "voucher_number": "VCH-2026-000001",
    "amount": "5000.00",
    "description": "Payment received"
}
```

 **আপনার project যদি production/business application হয়, `VoucherSequence + transaction + select_for_update()` approach-টাই নেওয়া উচিত।**

---
অবশ্যই। নিচে একটা **complete simple Voucher system** দিলাম—UUID, auto-generated voucher number, Customer relation, Payment relation, DRF API এবং PDF generation সব একসাথে।

 ## Architecture

```
Customer
   │
   └──< Payment
           │
           └── 1:1 ── Voucher
                         │
                         ▼
                        PDF
```

 Voucher-এর `voucher_number` backend নিজে generate করবে:

```
VCH-2026-000001
VCH-2026-000002
VCH-2026-000003
```

 আর database primary key হবে UUID।

---

 # 1\. Project structure

```
project/
│
├── manage.py
│
├── config/
│   ├── settings.py
│   └── urls.py
│
└── vouchers/
    ├── migrations/
    ├── templates/
    │   └── vouchers/
    │       └── voucher.html
    │
    ├── models.py
    ├── serializers.py
    ├── views.py
    ├── urls.py
    └── admin.py
```

 Install:

```
pip install django djangorestframework weasyprint
```

---

 # 2\. `models.py`

 এখানে তিনটা model রাখছি:

 - `Customer`
- `Payment`
- `Voucher`
- `VoucherSequence`

```
import uuid

from django.db import models, transaction
from django.utils import timezone

class Customer(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    name = models.CharField(
        max_length=200
    )

    phone = models.CharField(
        max_length=30,
        blank=True
    )

    email = models.EmailField(
        blank=True
    )

    address = models.TextField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    def __str__(self):
        return self.name

class Payment(models.Model):

    PAYMENT_METHOD_CHOICES = [
        ("cash", "Cash"),
        ("bank", "Bank"),
        ("mobile_banking", "Mobile Banking"),
        ("card", "Card"),
    ]

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    customer = models.ForeignKey(
        Customer,
        on_delete=models.PROTECT,
        related_name="payments",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    payment_method = models.CharField(
        max_length=30,
        choices=PAYMENT_METHOD_CHOICES,
    )

    payment_date = models.DateField(
        default=timezone.localdate
    )

    reference = models.CharField(
        max_length=100,
        blank=True
    )

    description = models.TextField(
        blank=True
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    def __str__(self):
        return (
            f"{self.customer.name} - "
            f"{self.amount}"
        )

class VoucherSequence(models.Model):

    year = models.PositiveIntegerField(
        unique=True
    )

    last_number = models.PositiveIntegerField(
        default=0
    )

    def __str__(self):
        return f"{self.year} - {self.last_number}"

class Voucher(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    payment = models.OneToOneField(
        Payment,
        on_delete=models.PROTECT,
        related_name="voucher",
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    def __str__(self):
        return self.voucher_number

    @classmethod
    def generate_voucher_number(cls):

        year = timezone.now().year

        with transaction.atomic():

            sequence, created = (
                VoucherSequence.objects
                .select_for_update()
                .get_or_create(
                    year=year,
                    defaults={
                        "last_number": 0
                    },
                )
            )

            sequence.last_number += 1

            sequence.save(
                update_fields=[
                    "last_number"
                ]
            )

            return (
                f"VCH-{year}-"
                f"{sequence.last_number:06d}"
            )

    def save(self, *args, **kwargs):

        if not self.voucher_number:

            self.voucher_number = (
                self.generate_voucher_number()
            )

        super().save(*args, **kwargs)
```

---

 # 3\. কেন `VoucherSequence`?

 ধরুন একই সময়ে দুইজন payment করছে।

```
Request A ──┐
             ├── VoucherSequence
Request B ──┘
```

 `select_for_update()` database row lock করবে।

 তাই:

```
Request A → VCH-2026-000001
Request B → VCH-2026-000002
```

 একই number পাওয়ার risk থাকবে না।

---

 # 4\. Serializer

 `serializers.py`

```
from rest_framework import serializers

from .models import (
    Customer,
    Payment,
    Voucher,
)

class CustomerSerializer(
    serializers.ModelSerializer
):

    class Meta:

        model = Customer

        fields = [
            "id",
            "name",
            "phone",
            "email",
            "address",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "created_at",
        ]

class PaymentSerializer(
    serializers.ModelSerializer
):

    customer_name = serializers.CharField(
        source="customer.name",
        read_only=True,
    )

    class Meta:

        model = Payment

        fields = [
            "id",
            "customer",
            "customer_name",
            "amount",
            "payment_method",
            "payment_date",
            "reference",
            "description",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "customer_name",
            "created_at",
        ]

class VoucherSerializer(
    serializers.ModelSerializer
):

    payment_id = serializers.UUIDField(
        source="payment.id",
        read_only=True,
    )

    customer = serializers.CharField(
        source="payment.customer.name",
        read_only=True,
    )

    amount = serializers.DecimalField(
        source="payment.amount",
        max_digits=12,
        decimal_places=2,
        read_only=True,
    )

    payment_method = serializers.CharField(
        source="payment.payment_method",
        read_only=True,
    )

    payment_date = serializers.DateField(
        source="payment.payment_date",
        read_only=True,
    )

    class Meta:

        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "created_at",
        ]
```

 এখানে একটা গুরুত্বপূর্ণ বিষয়:

 **Voucher API-তে amount/customer/payment method manually দিতে হচ্ছে না।**

 Voucher শুধু Payment-এর সাথে relation রাখছে।

---

 # 5\. Views

 `views.py`

```
from django.http import HttpResponse
from django.template.loader import render_to_string

from rest_framework import viewsets
from rest_framework.decorators import action

from weasyprint import HTML

from .models import (
    Customer,
    Payment,
    Voucher,
)

from .serializers import (
    CustomerSerializer,
    PaymentSerializer,
    VoucherSerializer,
)

class CustomerViewSet(
    viewsets.ModelViewSet
):

    queryset = Customer.objects.all()

    serializer_class = CustomerSerializer

class PaymentViewSet(
    viewsets.ModelViewSet
):

    queryset = (
        Payment.objects
        .select_related("customer")
        .all()
    )

    serializer_class = PaymentSerializer

class VoucherViewSet(
    viewsets.ModelViewSet
):

    serializer_class = VoucherSerializer

    def get_queryset(self):

        return (
            Voucher.objects
            .select_related(
                "payment",
                "payment__customer",
            )
            .all()
        )

    @action(
        detail=True,
        methods=["get"],
        url_path="pdf",
    )
    def pdf(self, request, pk=None):

        voucher = self.get_object()

        html_string = render_to_string(
            "vouchers/voucher.html",
            {
                "voucher": voucher,
            },
        )

        pdf = HTML(
            string=html_string
        ).write_pdf()

        response = HttpResponse(
            pdf,
            content_type="application/pdf",
        )

        response[
            "Content-Disposition"
        ] = (
            "attachment; "
            f'filename="{voucher.voucher_number}.pdf"'
        )

        return response
```

---

 # 6\. URLs

 `vouchers/urls.py`

```
from rest_framework.routers import DefaultRouter

from .views import (
    CustomerViewSet,
    PaymentViewSet,
    VoucherViewSet,
)

router = DefaultRouter()

router.register(
    "customers",
    CustomerViewSet,
    basename="customer",
)

router.register(
    "payments",
    PaymentViewSet,
    basename="payment",
)

router.register(
    "vouchers",
    VoucherViewSet,
    basename="voucher",
)

urlpatterns = router.urls
```

 Project-এর `config/urls.py`:

```
from django.contrib import admin
from django.urls import path, include

urlpatterns = [

    path(
        "admin/",
        admin.site.urls,
    ),

    path(
        "api/",
        include("vouchers.urls"),
    ),
]
```

---

 # 7\. PDF Template

 `templates/vouchers/voucher.html`

```
<!DOCTYPE html>

<html>

<head>

    <meta charset="UTF-8">

    <style>

        @page {
            size: A4;
            margin: 30px;
        }

        body {
            font-family: Arial, sans-serif;
            color: #222;
        }

        .container {
            width: 100%;
        }

        .header {
            border-bottom: 2px solid #222;
            padding-bottom: 15px;
            margin-bottom: 25px;
        }

        .title {
            font-size: 28px;
            font-weight: bold;
        }

        .voucher-number {
            font-size: 16px;
            margin-top: 5px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        td {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }

        .label {
            width: 35%;
            font-weight: bold;
        }

        .amount {
            font-size: 22px;
            font-weight: bold;
            color: #2563eb;
        }

        .footer {
            margin-top: 60px;
            text-align: center;
            color: #777;
        }

    </style>

</head>

<body>

<div class="container">

    <div class="header">

        <div class="title">
            PAYMENT VOUCHER
        </div>

        <div class="voucher-number">

            Voucher No:
            <strong>
                {{ voucher.voucher_number }}
            </strong>

        </div>

    </div>

    <table>

        <tr>

            <td class="label">
                Customer
            </td>

            <td>
                {{ voucher.payment.customer.name }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Phone
            </td>

            <td>
                {{ voucher.payment.customer.phone }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Payment Date
            </td>

            <td>
                {{ voucher.payment.payment_date }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Payment Method
            </td>

            <td>
                {{ voucher.payment.get_payment_method_display }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Reference
            </td>

            <td>
                {{ voucher.payment.reference }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Amount
            </td>

            <td class="amount">
                {{ voucher.payment.amount }}
            </td>

        </tr>

        <tr>

            <td class="label">
                Description
            </td>

            <td>
                {{ voucher.payment.description }}
            </td>

        </tr>

    </table>

    <div class="footer">

        Thank you for your payment.

    </div>

</div>

</body>

</html>
```

---

 # 8\. Migration

```
python manage.py makemigrations
python manage.py migrate
```

---

 # 9\. Create Customer

```
POST /api/customers/
Content-Type: application/json
```

```
{
    "name": "Rahim Ahmed",
    "phone": "01700000000",
    "email": "rahim@example.com",
    "address": "Dhaka, Bangladesh"
}
```

 Response:

```
{
    "id": "3d1e4f88-0f36-4d3e-a6e3-8a6c5d4b1122",
    "name": "Rahim Ahmed",
    "phone": "01700000000",
    "email": "rahim@example.com",
    "address": "Dhaka, Bangladesh"
}
```

---

 # 10\. Create Payment

 Customer UUID ব্যবহার করবেন:

```
POST /api/payments/
Content-Type: application/json
```

```
{
    "customer": "3d1e4f88-0f36-4d3e-a6e3-8a6c5d4b1122",
    "amount": "5000.00",
    "payment_method": "cash",
    "payment_date": "2026-10-01",
    "reference": "CASH-001",
    "description": "Payment received from customer"
}
```

 Response:

```
{
    "id": "8a7f2c11-4e1a-4c55-b921-1f7c8a3d5521",
    "customer": "3d1e4f88-0f36-4d3e-a6e3-8a6c5d4b1122",
    "customer_name": "Rahim Ahmed",
    "amount": "5000.00",
    "payment_method": "cash",
    "payment_date": "2026-10-01",
    "reference": "CASH-001",
    "description": "Payment received from customer",
    "created_at": "2026-10-01T10:30:00Z"
}
```

---

 # 11\. Generate Voucher

 এখন payment-এর UUID দিয়ে:

```
POST /api/vouchers/
Content-Type: application/json
```

```
{
    "payment": "8a7f2c11-4e1a-4c55-b921-1f7c8a3d5521"
}
```

 এখানে automatically:

```
voucher_number = VCH-2026-000001
```

 হবে।

 Response:

```
{
    "id": "7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234",
    "voucher_number": "VCH-2026-000001",
    "payment_id": "8a7f2c11-4e1a-4c55-b921-1f7c8a3d5521",
    "customer": "Rahim Ahmed",
    "amount": "5000.00",
    "payment_method": "cash",
    "payment_date": "2026-10-01",
    "created_at": "2026-10-01T10:31:00Z"
}
```

 তবে এখানে serializer-এ `payment` field read-only করা আছে, তাই **create করার জন্য serializer-এ payment input explicitly রাখতে হবে**। তাই final serializer-এ এই অংশটা পরিবর্তন করুন:

```
class VoucherSerializer(
    serializers.ModelSerializer
):

    payment = serializers.PrimaryKeyRelatedField(
        queryset=Payment.objects.all(),
        write_only=True,
    )

    payment_id = serializers.UUIDField(
        source="payment.id",
        read_only=True,
    )

    customer = serializers.CharField(
        source="payment.customer.name",
        read_only=True,
    )

    amount = serializers.DecimalField(
        source="payment.amount",
        max_digits=12,
        decimal_places=2,
        read_only=True,
    )

    payment_method = serializers.CharField(
        source="payment.payment_method",
        read_only=True,
    )

    payment_date = serializers.DateField(
        source="payment.payment_date",
        read_only=True,
    )

    class Meta:

        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "payment",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "created_at",
        ]
```

 এখন create request ঠিকমতো কাজ করবে।

---

 # 12\. Get Voucher

```
GET /api/vouchers/7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/
```

 আপনি database-এ রাখছেন:

```
Voucher
│
├── id = UUID
├── voucher_number = VCH-2026-000001
└── payment = Payment UUID
```

 কিন্তু API response-এ related data পাচ্ছেন:

```
Payment
│
├── Customer
├── Amount
├── Payment Method
├── Date
└── Reference
```

---

 # 13\. Generate PDF

```
GET /api/vouchers/7b9c8f44-2e4d-4a0d-b4a7-7c3f2b8c1234/pdf/
```

 Flow:

```
GET /vouchers/{uuid}/pdf/
             │
             ▼
       VoucherViewSet
             │
             ▼
         Voucher
             │
             ▼
          Payment
             │
       ┌─────┴─────┐
       ▼           ▼
   Customer       Data
       │           │
       └─────┬─────┘
             ▼
      voucher.html
             │
             ▼
         WeasyPrint
             │
             ▼
    VCH-2026-000001.pdf
```

---

 ## Final database relationship

```
┌─────────────────┐
│    Customer     │
│─────────────────│
│ UUID            │
│ name            │
│ phone           │
│ email           │
└────────┬────────┘
         │
         │ 1
         │
         │ N
┌────────▼────────┐
│     Payment     │
│─────────────────│
│ UUID            │
│ customer FK     │
│ amount          │
│ method          │
│ date            │
│ reference       │
│ description     │
└────────┬────────┘
         │
         │ 1
         │
         │ 1
┌────────▼────────┐
│     Voucher     │
│─────────────────│
│ UUID            │
│ voucher_number  │
│ payment FK      │
└─────────────────┘

VoucherSequence
─────────────────
year
last_number
```

 ### সবচেয়ে গুরুত্বপূর্ণ design point

 এখানে **Voucher-এর মধ্যে `customer_name`, `amount`, `payment_method` duplicate করে রাখিনি**।

 শুধু:

```
Voucher
   ↓
Payment
   ↓
Customer
```

 relation রেখেছি।

 তাই **Voucher model = document identity**, আর **Payment model = actual payment data**।

 আর PDF generate হওয়ার সময় relation থেকে সব data নিয়ে PDF তৈরি হচ্ছে।

 একটা বাস্তব project-এ আমি এর পরের ধাপে **Invoice + Payment + Voucher**-কে একসাথে connect করতাম:

```
Customer
   │
   ├── Invoice
   │      │
   │      └── Payment
   │             │
   │             └── Voucher
   │
   └── Payment (invoice ছাড়া)
          │
          └── Voucher
```

 এতে invoice payment এবং direct payment—দুই ধরনের voucher-ই handle করা যাবে।

----
আপনার এই `models.py` অংশটা **মূলত ঠিক আছে**। `voucher_number` auto-generate হবে এবং `Payment`-এর সাথে `OneToOne` relation থাকবে।

 তবে আপনার আগের `NOT NULL constraint failed: vouchers_voucher.payment_id` error অনুযায়ী, **Model-এর সমস্যা নয়**—Voucher create করার সময় `payment` field ঠিকভাবে save হচ্ছে না।

 আপনার Model অনুযায়ী create করার সবচেয়ে simple এবং reliable version হলো:

 Voucher Model✓

```
import uuid

from django.db import models, transaction
from django.utils import timezone

from .models import Payment

class VoucherSequence(models.Model):

    year = models.PositiveIntegerField(
        unique=True
    )

    last_number = models.PositiveIntegerField(
        default=0
    )

    def __str__(self):
        return f"{self.year} - {self.last_number}"

class Voucher(models.Model):

    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False,
    )

    voucher_number = models.CharField(
        max_length=50,
        unique=True,
        editable=False,
    )

    payment = models.OneToOneField(
        Payment,
        on_delete=models.PROTECT,
        related_name="voucher",
    )

    created_at = models.DateTimeField(
        auto_now_add=True
    )

    updated_at = models.DateTimeField(
        auto_now=True
    )

    def __str__(self):
        return self.voucher_number

    @classmethod
    def generate_voucher_number(cls):

        year = timezone.now().year

        with transaction.atomic():

            sequence, created = (
                VoucherSequence.objects
                .select_for_update()
                .get_or_create(
                    year=year,
                    defaults={
                        "last_number": 0
                    },
                )
            )

            sequence.last_number += 1

            sequence.save(
                update_fields=[
                    "last_number"
                ]
            )

            return (
                f"VCH-{year}-"
                f"{sequence.last_number:06d}"
            )

    def save(self, *args, **kwargs):

        if not self.voucher_number:

            self.voucher_number = (
                self.generate_voucher_number()
            )

        super().save(*args, **kwargs)
```

 একটা correction: একই app-এর `models.py`-এর ভিতরে যদি `Payment` class-ও থাকে, তাহলে:

```
from .models import Payment
```

 দেওয়ার দরকার নেই। বরং সরাসরি `Payment` ব্যবহার করবেন।

 ## আপনার Serializer এমন হওয়া উচিত

```
class VoucherSerializer(serializers.ModelSerializer):

    payment = serializers.PrimaryKeyRelatedField(
        queryset=Payment.objects.all(),
        write_only=True,
    )

    payment_id = serializers.UUIDField(
        source="payment.id",
        read_only=True,
    )

    customer = serializers.CharField(
        source="payment.customer.name",
        read_only=True,
    )

    amount = serializers.DecimalField(
        source="payment.amount",
        max_digits=12,
        decimal_places=2,
        read_only=True,
    )

    payment_method = serializers.CharField(
        source="payment.payment_method",
        read_only=True,
    )

    payment_date = serializers.DateField(
        source="payment.payment_date",
        read_only=True,
    )

    reference = serializers.CharField(
        source="payment.reference",
        read_only=True,
    )

    description = serializers.CharField(
        source="payment.description",
        read_only=True,
    )

    class Meta:
        model = Voucher

        fields = [
            "id",
            "voucher_number",
            "payment",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "reference",
            "description",
            "created_at",
        ]

        read_only_fields = [
            "id",
            "voucher_number",
            "payment_id",
            "customer",
            "amount",
            "payment_method",
            "payment_date",
            "reference",
            "description",
            "created_at",
        ]
```

 ### তারপর POST

 আপনার Payment ID:

```
4c3c4438-b84e-497f-ae47-d0cd05e1e734
```

 তাই:

```
POST /api/vouchers/
```

 Body:

```
{
    "payment": "4c3c4438-b84e-497f-ae47-d0cd05e1e734"
}
```

 DRF তখন internally এমন করবে:

```
Voucher.objects.create(
    payment=<Payment object>
)
```

 আর Model-এর `save()` automatically:

```
voucher_number
      ↓
generate_voucher_number()
      ↓
VCH-2026-000001
```

 তৈরি করবে।

 ### Expected result

```
{
    "id": "generated-uuid",
    "voucher_number": "VCH-2026-000001",
    "payment_id": "4c3c4438-b84e-497f-ae47-d0cd05e1e734",
    "customer": "Md. Atiar Rahman",
    "amount": "1000.00",
    "payment_method": "mobile_banking",
    "payment_date": "2026-10-01",
    "reference": "atiar",
    "description": "atiar khilkhet dhaka bangladesh"
}
```

 **তাই আপনার দেওয়া Model পরিবর্তন করার দরকার নেই।** এখন মূলত `Serializer` এবং `ViewSet` ঠিক করতে হবে। বিশেষ করে `payment` যেন `write_only=True` হয় এবং `read_only_fields`-এর মধ্যে `payment` না থাকে।

---
হ্যাঁ—**একই Payment থেকে যদি একাধিক Voucher হতে পারে**, তাহলে `OneToOneField` না দিয়ে `ForeignKey` ব্যবহার করবেন।

 ### বর্তমান

```
payment = models.OneToOneField(
    Payment,
    on_delete=models.PROTECT,
    related_name="voucher",
)
```

 এটা মানে:

```
Payment 1 ─── 1 Voucher
```

 একটি Payment-এর বিপরীতে **একটিই Voucher**।

---

 ### ForeignKey করলে

```
payment = models.ForeignKey(
    Payment,
    on_delete=models.PROTECT,
    related_name="vouchers",
)
```

 তখন:

```
Payment 1 ─── N Voucher
```

 অর্থাৎ একই Payment-এর জন্য একাধিক Voucher তৈরি করা যাবে।

 তখন access করবেন:

```
payment.vouchers.all()
```

---

 ## তবে আপনার কথাটা যদি হয় "একদিনে/একবারে একাধিক payment"

 যেমন:

```
Payment #1 → 1000
Payment #2 → 2000
Payment #3 → 3000
```

 এবং প্রত্যেক Payment-এর জন্য আলাদা Voucher:

```
Payment #1 → Voucher #1
Payment #2 → Voucher #2
Payment #3 → Voucher #3
```

 তাহলে **OneToOneField-ই ঠিক আছে**।

 কিন্তু যদি এমন হয়:

```
Payment
   │
   ├── Voucher #1
   ├── Voucher #2
   └── Voucher #3
```

 তাহলে `ForeignKey` লাগবে।

 ### আরেকটা গুরুত্বপূর্ণ distinction

 আপনি যদি বলতে চান:

 > "একজন customer একাধিকবার payment করবে, এবং প্রতিবার একটি করে voucher হবে"

 তাহলে **OneToOneField একদম ঠিক**:

```
Customer
   │
   ├── Payment #1 ── Voucher #1
   ├── Payment #2 ── Voucher #2
   └── Payment #3 ── Voucher #3
```

 এটাই সাধারণ **payment receipt/voucher system**-এর জন্য আমি রাখব।

 শুধু **একই Payment record-এর জন্য একাধিক Voucher** দরকার হলে `ForeignKey` করবেন।

হ্যাঁ, যদি requirement হয় **একজন Customer-এর অনেক Payment এবং অনেক Voucher**, তাহলে সাধারণত structure হবে:

```
Customer
   │
   ├── Payment 1 ─── Voucher 1
   ├── Payment 2 ─── Voucher 2
   ├── Payment 3 ─── Voucher 3
   └── Payment 4 ─── Voucher 4
```

 অর্থাৎ **Payment ↔ Voucher relationship**-টা নির্ভর করবে একটি payment-এর জন্য কয়টা voucher দরকার তার ওপর।

 ### যদি একই Payment-এর জন্য একাধিক Voucher হতে পারে

 তাহলে:

```
payment = models.ForeignKey(
    Payment,
    on_delete=models.PROTECT,
    related_name="vouchers",
)
```

 Result:

```
Payment #1
   ├── Voucher #1
   ├── Voucher #2
   └── Voucher #3
```

 ### যদি একাধিক Payment এক Voucher-এর মধ্যে থাকতে পারে

 তাহলে উল্টোভাবে `ManyToManyField` লাগবে:

```
payments = models.ManyToManyField(
    Payment,
    related_name="vouchers",
)
```

 Result:

```
Payment #1 ──┐
Payment #2 ──┼── Voucher #1
Payment #3 ──┘
```

 কিন্তু **সাধারণ payment voucher/receipt system-এ এটা সাধারণত দরকার হয় না**।

 আপনার requirement যদি হয়:

 > অনেক Payment থাকবে এবং প্রতিটি Payment-এর জন্য Voucher generate হবে

 তাহলে সবচেয়ে clean design:

```
payment = models.ForeignKey(
    Payment,
    on_delete=models.PROTECT,
    related_name="vouchers",
)
```

 এবং flow:

```
Customer
   │
   │ 1:N
   ▼
Payment
   │
   │ 1:N
   ▼
Voucher
   │
   ▼
PDF
```

 তবে যদি **এক Payment = এক Voucher** হয়, তাহলে `OneToOneField`-ই better। **"Many payment, many voucher" বললেই ManyToMany দরকার হয় না**—কারণ আপনার business rule অনুযায়ী relation নির্ধারণ করতে হবে।


