# model
```py 

# Create your models here.
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

# serializer
```py
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

# viewset
```py
from django.shortcuts import render

# Create your views here.
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

# urls
```py
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


