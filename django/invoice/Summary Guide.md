Got it—you don’t just want this fixed, you want a **complete “any-way” invoice system guide** you can reuse in any Django project (Todo, Order, ML project, anything). Let’s build that properly.

---

# 🚀 COMPLETE DJANGO INVOICE SYSTEM (ALL METHODS)

You can generate invoices in **3 main ways**:

|Method|Use Case|Difficulty|
|---|---|---|
|HTML → PDF (WeasyPrint)|✅ Best & modern|⭐⭐|
|ReportLab (Pure Python)|No HTML needed|⭐⭐⭐|
|External API (Stripe etc.)|Production SaaS|⭐⭐⭐⭐|

---

# ✅ METHOD 1: HTML → PDF (BEST PRACTICE)

This is what you're already doing 👍 — just do it **properly structured**

---

## 🧱 Step 1: Create Invoice Template

`templates/invoice.html`

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body { font-family: Arial; }
        .header { text-align: center; }
        .box { margin-top: 20px; }
        .title { font-size: 22px; font-weight: bold; }
    </style>
</head>
<body>

<div class="header">
    <div class="title">INVOICE</div>
</div>

<div class="box">
    <p><strong>Title:</strong> {{ title }}</p>
    <p><strong>Description:</strong> {{ description }}</p>
    <p><strong>Priority:</strong> {{ priority }}</p>
    <p><strong>Status:</strong> {{ status }}</p>
    <p><strong>Due Date:</strong> {{ due_date }}</p>
</div>

</body>
</html>
```

---

## ⚙️ Step 2: Service Layer (VERY IMPORTANT)

👉 Don’t keep logic inside ViewSet (bad practice)  
👉 Create a reusable service

`services/invoice_service.py`

```python
from django.template.loader import render_to_string
from weasyprint import HTML
from io import BytesIO
import cloudinary.uploader
import re

def generate_invoice(todo):
    data = {
        'title': todo.title,
        'description': todo.description,
        'priority': todo.priority,
        'due_date': todo.due_date.strftime('%Y-%m-%d %H:%M'),
        'status': todo.status,
    }

    html = render_to_string("invoice.html", data)
    pdf = HTML(string=html).write_pdf()

    pdf_io = BytesIO(pdf)

    safe_title = re.sub(r'[^a-zA-Z0-9_-]', '_', todo.title)

    upload = cloudinary.uploader.upload(
        pdf_io,
        resource_type="raw",
        format="pdf",
        public_id=f"invoice_{safe_title}",
        folder="invoices/"
    )

    return upload['secure_url']
```

---

## 🔗 Step 3: Use in ViewSet

```python
from rest_framework.decorators import action
from rest_framework.response import Response
from .services.invoice_service import generate_invoice

@action(detail=True, methods=['post'])
def generate_invoice(self, request, pk=None):
    todo = self.get_object()

    try:
        pdf_url = generate_invoice(todo)

        todo.invoice_url = pdf_url
        todo.save()

        return Response({
            "pdf_url": pdf_url
        })

    except Exception as e:
        return Response({"error": str(e)}, status=500)
```

---

# ⚡ METHOD 2: REPORTLAB (NO HTML)

Use this if:

- You don’t want templates
    
- You want full Python control
    

---

## Example:

```python
from reportlab.platypus import SimpleDocTemplate, Paragraph
from reportlab.lib.styles import getSampleStyleSheet
from io import BytesIO

def generate_invoice_reportlab(todo):
    buffer = BytesIO()
    doc = SimpleDocTemplate(buffer)

    styles = getSampleStyleSheet()

    content = []
    content.append(Paragraph(f"Title: {todo.title}", styles['Normal']))
    content.append(Paragraph(f"Status: {todo.status}", styles['Normal']))

    doc.build(content)

    buffer.seek(0)
    return buffer
```

👉 Then upload same as Cloudinary

---

# ⚡ METHOD 3: AUTO INVOICE ON ORDER CREATE

If you're building **E-commerce (important for you)**

---

## In `OrderSerializer.create()`

```python
from .services.invoice_service import generate_invoice

def create(self, validated_data):
    order = super().create(validated_data)

    pdf_url = generate_invoice(order)
    order.invoice_url = pdf_url
    order.save()

    return order
```

---

# 📧 METHOD 4: SEND INVOICE VIA EMAIL

---

```python
from django.core.mail import EmailMessage

def send_invoice(email, pdf_bytes):
    mail = EmailMessage(
        subject="Your Invoice",
        body="Please find your invoice attached",
        to=[email]
    )

    mail.attach("invoice.pdf", pdf_bytes, "application/pdf")
    mail.send()
```

---

# 🔥 METHOD 5: ADD QR CODE (ADVANCED 🔥)

---

```python
import qrcode
from io import BytesIO

def generate_qr(data):
    qr = qrcode.make(data)
    buffer = BytesIO()
    qr.save(buffer)
    return buffer
```

👉 Add inside HTML template

---

# 🧠 BEST ARCHITECTURE (IMPORTANT FOR INTERVIEW)

Structure like this:

```
project/
 ├── invoices/
 │    ├── services/
 │    │     └── invoice_service.py
 │    ├── templates/
 │    │     └── invoice.html
 │    ├── utils/
 │    │     └── qr.py
```

---

# ❌ COMMON MISTAKES (YOU SHOULD AVOID)

- ❌ Generating PDF inside ViewSet directly
    
- ❌ Not sanitizing filename
    
- ❌ Not handling errors
    
- ❌ Not saving invoice URL
    
- ❌ Heavy logic in serializer
    

---

# 🧠 FOR YOUR LEVEL (IMPORTANT ADVICE)

Since you're learning **ML + Django**, do this next:

👉 Build:

- Order system + Invoice
    
- Auto invoice on checkout
    
- Email system
    
- Admin dashboard to download invoices
    

👉 Bonus ML idea:

- Predict order cost
    
- Smart invoice categorization
    

---

# 👉 What next?

Tell me what you want:

1. 🔥 “Professional Bootstrap invoice template”
    
2. 📧 “Auto email with Celery (background task)”
    
3. 🛒 “Full Order + Payment + Invoice system”
    
4. 🤖 “ML-based invoice analyzer project”

