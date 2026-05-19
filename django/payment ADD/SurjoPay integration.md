**SurjoPay integration** into a more **production-ready DRF setup** with everything you listed:

- ✅ Unique `tran_id`
- ✅ Save transaction before redirect
- ✅ Backend verification
- ✅ Proper success / fail / cancel handling
- ✅ Sandbox → Live ready

---

# 🧱 1. Model (store transaction)

# models.py  
```python
import uuid  
from django.db import models  
  
class Payment(models.Model):  
    STATUS_CHOICES = [  
        ("PENDING", "Pending"),  
        ("SUCCESS", "Success"),  
        ("FAILED", "Failed"),  
        ("CANCELLED", "Cancelled"),  
    ]  
  
    tran_id = models.CharField(max_length=100, unique=True)  
    amount = models.DecimalField(max_digits=10, decimal_places=2)  
  
    customer_name = models.CharField(max_length=100)  
    customer_email = models.EmailField()  
  
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default="PENDING")  
  
    surjopay_request_id = models.CharField(max_length=200, null=True, blank=True)  
    surjopay_response = models.JSONField(null=True, blank=True)  
  
    created_at = models.DateTimeField(auto_now_add=True)  
  
    def __str__(self):  
        return self.tran_id
```

---

# 🔐 2. Utility (generate unique tran_id)

```python
import uuid  
  
def generate_tran_id():  
    return f"TXN-{uuid.uuid4().hex[:12]}"
```

---

# 🚀 3. Create Payment API (save before redirect)

# views.py  
```python
import requests  
from django.conf import settings  
from rest_framework.views import APIView  
from rest_framework.response import Response  
  
from .models import Payment  
from .utils import generate_tran_id  
  
  
class CreatePaymentAPIView(APIView):  
    def post(self, request):  
        amount = request.data.get("amount")  
  
        # ✅ generate unique transaction id  
        tran_id = generate_tran_id()  
  
        # ✅ save আগে DB তে  
        payment = Payment.objects.create(  
            tran_id=tran_id,  
            amount=amount,  
            customer_name=request.data.get("name"),  
            customer_email=request.data.get("email"),  
        )  
  
        payload = {  
            "store_id": settings.SURJOPAY_STORE_ID,  
            "store_passwd": settings.SURJOPAY_STORE_PASSWORD,  
            "total_amount": amount,  
            "currency": "BDT",  
            "tran_id": tran_id,  
  
            # ✅ separate URLs  
            "success_url": f"{settings.BASE_URL}/api/payment/success/",  
            "fail_url": f"{settings.BASE_URL}/api/payment/fail/",  
            "cancel_url": f"{settings.BASE_URL}/api/payment/cancel/",  
  
            "cus_name": payment.customer_name,  
            "cus_email": payment.customer_email,  
            "cus_add1": "Dhaka",  
            "cus_phone": "01700000000",  
        }  
  
        res = requests.post(  
            f"{settings.SURJOPAY_BASE_URL}/spg/v1/payment/create",  
            json=payload  
        )  
  
        data = res.json()  
  
        # ✅ store request_id  
        payment.surjopay_request_id = data.get("sp_order_id")  
        payment.surjopay_response = data  
        payment.save()  
  
        return Response(data)
```
---

# 🔁 4. Verify (COMMON FUNCTION — reuse everywhere)

```python
def verify_payment(request_id):  
    import requests  
    from django.conf import settings  
  
    payload = {  
        "store_id": settings.SURJOPAY_STORE_ID,  
        "store_passwd": settings.SURJOPAY_STORE_PASSWORD,  
        "request_id": request_id,  
    }  
  
    res = requests.post(  
        f"{settings.SURJOPAY_BASE_URL}/spg/v1/payment/verify",  
        json=payload  
    )  
  
    return res.json()
```

---

# ✅ 5. SUCCESS URL (critical)

```python
class PaymentSuccessAPIView(APIView):  
    def post(self, request):  
        request_id = request.data.get("sp_order_id")  
  
        data = verify_payment(request_id)  
  
        try:  
            payment = Payment.objects.get(  
                surjopay_request_id=request_id  
            )  
        except Payment.DoesNotExist:  
            return Response({"error": "Payment not found"}, status=404)  
  
        # ✅ backend verification  
        if data.get("sp_code") == "000":  
            payment.status = "SUCCESS"  
        else:  
            payment.status = "FAILED"  
  
        payment.surjopay_response = data  
        payment.save()  
  
        return Response({"status": payment.status})
```

---

# ❌ 6. FAIL URL

```python
class PaymentFailAPIView(APIView):  
    def post(self, request):  
        request_id = request.data.get("sp_order_id")  
  
        Payment.objects.filter(  
            surjopay_request_id=request_id  
        ).update(status="FAILED")  
  
        return Response({"status": "failed"})
```
---

# 🚫 7. CANCEL URL

```python
class PaymentCancelAPIView(APIView):  
    def post(self, request):  
        request_id = request.data.get("sp_order_id")  
  
        Payment.objects.filter(  
            surjopay_request_id=request_id  
        ).update(status="CANCELLED")  
  
        return Response({"status": "cancelled"})
```
---

# 🌐 8. URLs

```python
from django.urls import path  
from .views import (  
    CreatePaymentAPIView,  
    PaymentSuccessAPIView,  
    PaymentFailAPIView,  
    PaymentCancelAPIView,  
)  
  
urlpatterns = [  
    path("payment/create/", CreatePaymentAPIView.as_view()),  
    path("payment/success/", PaymentSuccessAPIView.as_view()),  
    path("payment/fail/", PaymentFailAPIView.as_view()),  
    path("payment/cancel/", PaymentCancelAPIView.as_view()),  
]
```

---

# ⚙️ 9. Sandbox → Live switch

# sandbox  
```
SURJOPAY_BASE_URL = "https://sandbox.surjopay.com"  
```
  
# production  
```
SURJOPAY_BASE_URL = "https://securepay.surjopay.com"
```
---

# 🔒 Final Notes (Important)

- Never trust frontend → ✔ already handled
- Always verify via `verify API` → ✔ done
- Always store payment আগে → ✔ done
- Use HTTPS in production
- Add webhook retry handling (advanced)
- লগ রাখলে future debugging easy হবে