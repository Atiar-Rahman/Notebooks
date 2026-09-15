অবশ্যই। এবার **Hospital Management System (HMS)**-এর জন্যও আগেরগুলোর মতো **complete production-style Django ORM model architecture** দিচ্ছি।

এখানে আমরা শুধু basic `Patient`, `Doctor`, `Appointment` রাখব না। বরং **Hospital → Department → Doctor → Patient → Appointment → Admission → Treatment → Prescription → Lab → Billing → Payment → Insurance → Pharmacy → Discharge**—পুরো workflow ধরব।

> **Design assumption:** এটি একটি multi-branch / multi-department hospital system। একই hospital-এর multiple branch থাকতে পারে এবং একই doctor একাধিক department-এ কাজ করতে পারে।

---

# 🏥 Complete Hospital Management System

## Overall Architecture

```text
USER
│
├── HOSPITAL
│   ├── Branch
│   ├── Department
│   ├── Staff
│   ├── Doctors
│   └── Services
│
└── PATIENT
    ├── Profile
    ├── Address
    ├── Appointment
    ├── Admission
    ├── Treatment
    ├── Prescription
    ├── Lab Tests
    ├── Pharmacy
    ├── Billing
    ├── Insurance
    └── Medical Records
```

---

# 1. BaseModel

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

---

# 2. Hospital

একটি platform-এ multiple hospital থাকতে পারে।

```python
class Hospital(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("approved", "Approved"),
        ("suspended", "Suspended"),
        ("inactive", "Inactive"),
    ]

    name = models.CharField(max_length=200)

    registration_number = models.CharField(
        max_length=100,
        unique=True,
    )

    email = models.EmailField()

    phone = models.CharField(
        max_length=30,
    )

    address = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    country = models.CharField(
        max_length=100,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(fields=["status"]),
            models.Index(fields=["city", "status"]),
        ]
```

---

# 3. Hospital Branch

একটি hospital-এর multiple branches থাকতে পারে।

```python
class HospitalBranch(BaseModel):

    hospital = models.ForeignKey(
        Hospital,
        on_delete=models.CASCADE,
        related_name="branches",
    )

    name = models.CharField(
        max_length=150,
    )

    address = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    phone = models.CharField(
        max_length=30,
    )

    latitude = models.DecimalField(
        max_digits=9,
        decimal_places=6,
        null=True,
        blank=True,
    )

    longitude = models.DecimalField(
        max_digits=9,
        decimal_places=6,
        null=True,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["hospital", "name"],
                name="unique_hospital_branch",
            )
        ]
```

---

# 4. Department

```text
Cardiology
Neurology
Orthopedics
Dermatology
Pediatrics
ENT
General Medicine
```

```python
class Department(BaseModel):

    hospital = models.ForeignKey(
        Hospital,
        on_delete=models.CASCADE,
        related_name="departments",
    )

    name = models.CharField(
        max_length=150,
    )

    description = models.TextField(
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["hospital", "name"],
                name="unique_hospital_department",
            )
        ]

        indexes = [
            models.Index(
                fields=["hospital", "is_active"]
            ),
        ]
```

---

# 5. Staff

Hospital-এর employee।

```python
class HospitalStaff(BaseModel):

    ROLE_CHOICES = [
        ("admin", "Admin"),
        ("doctor", "Doctor"),
        ("nurse", "Nurse"),
        ("receptionist", "Receptionist"),
        ("lab_staff", "Lab Staff"),
        ("pharmacist", "Pharmacist"),
        ("accountant", "Accountant"),
        ("technician", "Technician"),
    ]

    hospital = models.ForeignKey(
        Hospital,
        on_delete=models.CASCADE,
        related_name="staff",
    )

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="hospital_staff",
    )

    role = models.CharField(
        max_length=30,
        choices=ROLE_CHOICES,
    )

    employee_id = models.CharField(
        max_length=100,
        unique=True,
    )

    phone = models.CharField(
        max_length=30,
    )

    joining_date = models.DateField()

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["hospital", "role"]
            ),
            models.Index(
                fields=["hospital", "is_active"]
            ),
        ]
```

---

# 6. Doctor Profile

```python
class DoctorProfile(BaseModel):

    staff = models.OneToOneField(
        HospitalStaff,
        on_delete=models.PROTECT,
        related_name="doctor_profile",
    )

    license_number = models.CharField(
        max_length=100,
        unique=True,
    )

    specialization = models.CharField(
        max_length=150,
    )

    qualification = models.CharField(
        max_length=300,
    )

    experience_years = models.PositiveIntegerField(
        default=0,
    )

    consultation_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    bio = models.TextField(
        blank=True,
    )

    is_available = models.BooleanField(
        default=True,
    )
```

---

# 7. Doctor Department

একজন doctor multiple department-এ থাকতে পারে।

```python
class DoctorDepartment(BaseModel):

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.CASCADE,
        related_name="departments",
    )

    department = models.ForeignKey(
        Department,
        on_delete=models.PROTECT,
        related_name="doctors",
    )

    is_primary = models.BooleanField(
        default=False,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["doctor", "department"],
                name="unique_doctor_department",
            )
        ]
```

---

# 8. Patient Profile

```python
class PatientProfile(BaseModel):

    BLOOD_GROUPS = [
        ("A+", "A+"),
        ("A-", "A-"),
        ("B+", "B+"),
        ("B-", "B-"),
        ("AB+", "AB+"),
        ("AB-", "AB-"),
        ("O+", "O+"),
        ("O-", "O-"),
    ]

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="patient_profile",
    )

    patient_number = models.CharField(
        max_length=100,
        unique=True,
    )

    date_of_birth = models.DateField()

    gender = models.CharField(
        max_length=20,
    )

    blood_group = models.CharField(
        max_length=5,
        choices=BLOOD_GROUPS,
        blank=True,
    )

    phone = models.CharField(
        max_length=30,
    )

    emergency_contact_name = models.CharField(
        max_length=150,
        blank=True,
    )

    emergency_contact_phone = models.CharField(
        max_length=30,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 9. Patient Address

```python
class PatientAddress(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.CASCADE,
        related_name="addresses",
    )

    address_line = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    country = models.CharField(
        max_length=100,
    )

    postal_code = models.CharField(
        max_length=20,
        blank=True,
    )

    is_default = models.BooleanField(
        default=False,
    )
```

---

# 10. Emergency Contact

```python
class EmergencyContact(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.CASCADE,
        related_name="emergency_contacts",
    )

    name = models.CharField(
        max_length=150,
    )

    relationship = models.CharField(
        max_length=50,
    )

    phone = models.CharField(
        max_length=30,
    )

    is_primary = models.BooleanField(
        default=False,
    )
```

---

# 11. Doctor Schedule

```python
class DoctorSchedule(BaseModel):

    WEEKDAYS = [
        (0, "Monday"),
        (1, "Tuesday"),
        (2, "Wednesday"),
        (3, "Thursday"),
        (4, "Friday"),
        (5, "Saturday"),
        (6, "Sunday"),
    ]

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.CASCADE,
        related_name="schedules",
    )

    branch = models.ForeignKey(
        HospitalBranch,
        on_delete=models.PROTECT,
        related_name="doctor_schedules",
    )

    weekday = models.PositiveSmallIntegerField(
        choices=WEEKDAYS,
    )

    start_time = models.TimeField()

    end_time = models.TimeField()

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["doctor", "weekday"]
            ),
        ]
```

---

# 12. Appointment

Hospital-এর সবচেয়ে important modelগুলোর একটি।

```python
class Appointment(BaseModel):

    STATUS_CHOICES = [
        ("scheduled", "Scheduled"),
        ("confirmed", "Confirmed"),
        ("completed", "Completed"),
        ("cancelled", "Cancelled"),
        ("no_show", "No Show"),
    ]

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="appointments",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="appointments",
    )

    department = models.ForeignKey(
        Department,
        on_delete=models.PROTECT,
        related_name="appointments",
    )

    branch = models.ForeignKey(
        HospitalBranch,
        on_delete=models.PROTECT,
        related_name="appointments",
    )

    appointment_number = models.CharField(
        max_length=100,
        unique=True,
    )

    appointment_date = models.DateField()

    start_time = models.TimeField()

    end_time = models.TimeField()

    reason = models.TextField(
        blank=True,
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="scheduled",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=[
                    "doctor",
                    "appointment_date",
                ]
            ),
            models.Index(
                fields=[
                    "patient",
                    "-appointment_date",
                ]
            ),
            models.Index(
                fields=[
                    "status",
                    "appointment_date",
                ]
            ),
        ]
```

---

# 13. Medical Record

Patient-এর long-term medical history।

```python
class MedicalRecord(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="medical_records",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="medical_records",
    )

    appointment = models.ForeignKey(
        Appointment,
        on_delete=models.PROTECT,
        related_name="medical_records",
        null=True,
        blank=True,
    )

    diagnosis = models.TextField()

    symptoms = models.TextField(
        blank=True,
    )

    notes = models.TextField(
        blank=True,
    )

    recorded_at = models.DateTimeField()
```

---

# 14. Allergy

```python
class PatientAllergy(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.CASCADE,
        related_name="allergies",
    )

    allergen = models.CharField(
        max_length=150,
    )

    reaction = models.TextField(
        blank=True,
    )

    severity = models.CharField(
        max_length=30,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 15. Chronic Condition

```python
class ChronicCondition(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.CASCADE,
        related_name="chronic_conditions",
    )

    name = models.CharField(
        max_length=150,
    )

    diagnosed_date = models.DateField(
        null=True,
        blank=True,
    )

    notes = models.TextField(
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 16. Hospital Room

```python
class HospitalRoom(BaseModel):

    ROOM_TYPES = [
        ("general", "General"),
        ("private", "Private"),
        ("icu", "ICU"),
        ("ccu", "CCU"),
        ("emergency", "Emergency"),
        ("cabin", "Cabin"),
    ]

    STATUS_CHOICES = [
        ("available", "Available"),
        ("occupied", "Occupied"),
        ("maintenance", "Maintenance"),
        ("inactive", "Inactive"),
    ]

    branch = models.ForeignKey(
        HospitalBranch,
        on_delete=models.CASCADE,
        related_name="rooms",
    )

    room_number = models.CharField(
        max_length=50,
    )

    room_type = models.CharField(
        max_length=30,
        choices=ROOM_TYPES,
    )

    floor = models.CharField(
        max_length=50,
        blank=True,
    )

    daily_rate = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="available",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["branch", "room_number"],
                name="unique_branch_room",
            )
        ]

        indexes = [
            models.Index(
                fields=["branch", "status"]
            ),
            models.Index(
                fields=["room_type", "status"]
            ),
        ]
```

---

# 17. Admission

Patient hospital-এ admit হলে।

```python
class Admission(BaseModel):

    STATUS_CHOICES = [
        ("admitted", "Admitted"),
        ("transferred", "Transferred"),
        ("discharged", "Discharged"),
        ("cancelled", "Cancelled"),
    ]

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="admissions",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="admissions",
    )

    room = models.ForeignKey(
        HospitalRoom,
        on_delete=models.PROTECT,
        related_name="admissions",
    )

    admission_number = models.CharField(
        max_length=100,
        unique=True,
    )

    admitted_at = models.DateTimeField()

    discharged_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    reason = models.TextField()

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="admitted",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["patient", "-admitted_at"]
            ),
            models.Index(
                fields=["room", "status"]
            ),
            models.Index(
                fields=["status", "-admitted_at"]
            ),
        ]
```

---

# 18. Nurse Assignment

```python
class NurseAssignment(BaseModel):

    admission = models.ForeignKey(
        Admission,
        on_delete=models.CASCADE,
        related_name="nurse_assignments",
    )

    nurse = models.ForeignKey(
        HospitalStaff,
        on_delete=models.PROTECT,
        related_name="nurse_assignments",
    )

    assigned_at = models.DateTimeField()

    ended_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

---

# 19. Treatment

```python
class Treatment(BaseModel):

    admission = models.ForeignKey(
        Admission,
        on_delete=models.CASCADE,
        related_name="treatments",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="treatments",
    )

    treatment_name = models.CharField(
        max_length=200,
    )

    description = models.TextField(
        blank=True,
    )

    treatment_date = models.DateTimeField()

    notes = models.TextField(
        blank=True,
    )
```

---

# 20. Medicine

```python
class Medicine(BaseModel):

    name = models.CharField(
        max_length=200,
    )

    generic_name = models.CharField(
        max_length=200,
        blank=True,
    )

    manufacturer = models.CharField(
        max_length=200,
        blank=True,
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    stock_quantity = models.PositiveIntegerField(
        default=0,
    )

    reorder_level = models.PositiveIntegerField(
        default=10,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["name"]
            ),
            models.Index(
                fields=["generic_name"]
            ),
        ]
```

---

# 21. Prescription

```python
class Prescription(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="prescriptions",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="prescriptions",
    )

    appointment = models.ForeignKey(
        Appointment,
        on_delete=models.PROTECT,
        related_name="prescriptions",
        null=True,
        blank=True,
    )

    prescription_number = models.CharField(
        max_length=100,
        unique=True,
    )

    notes = models.TextField(
        blank=True,
    )

    prescribed_at = models.DateTimeField()
```

---

# 22. Prescription Item

```python
class PrescriptionItem(BaseModel):

    prescription = models.ForeignKey(
        Prescription,
        on_delete=models.CASCADE,
        related_name="items",
    )

    medicine = models.ForeignKey(
        Medicine,
        on_delete=models.PROTECT,
        related_name="prescription_items",
    )

    dosage = models.CharField(
        max_length=100,
    )

    frequency = models.CharField(
        max_length=100,
    )

    duration = models.CharField(
        max_length=100,
    )

    instructions = models.TextField(
        blank=True,
    )
```

---

# 23. Lab Test

```python
class LabTest(BaseModel):

    name = models.CharField(
        max_length=200,
    )

    description = models.TextField(
        blank=True,
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["name"],
                name="unique_lab_test",
            )
        ]
```

---

# 24. Lab Order

Doctor patient-এর জন্য test order করলে।

```python
class LabOrder(BaseModel):

    STATUS_CHOICES = [
        ("ordered", "Ordered"),
        ("sample_collected", "Sample Collected"),
        ("processing", "Processing"),
        ("completed", "Completed"),
        ("cancelled", "Cancelled"),
    ]

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="lab_orders",
    )

    doctor = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="lab_orders",
    )

    appointment = models.ForeignKey(
        Appointment,
        on_delete=models.PROTECT,
        related_name="lab_orders",
        null=True,
        blank=True,
    )

    order_number = models.CharField(
        max_length=100,
        unique=True,
    )

    status = models.CharField(
        max_length=30,
        choices=STATUS_CHOICES,
        default="ordered",
    )

    ordered_at = models.DateTimeField()
```

---

# 25. Lab Order Item

```python
class LabOrderItem(BaseModel):

    order = models.ForeignKey(
        LabOrder,
        on_delete=models.CASCADE,
        related_name="items",
    )

    lab_test = models.ForeignKey(
        LabTest,
        on_delete=models.PROTECT,
        related_name="order_items",
    )

    result = models.TextField(
        blank=True,
    )

    reference_range = models.CharField(
        max_length=200,
        blank=True,
    )

    result_unit = models.CharField(
        max_length=50,
        blank=True,
    )

    completed_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

---

# 26. Lab Report

```python
class LabReport(BaseModel):

    order = models.OneToOneField(
        LabOrder,
        on_delete=models.PROTECT,
        related_name="report",
    )

    report_file = models.FileField(
        upload_to="lab_reports/",
        blank=True,
        null=True,
    )

    summary = models.TextField(
        blank=True,
    )

    verified_by = models.ForeignKey(
        HospitalStaff,
        on_delete=models.PROTECT,
        related_name="verified_lab_reports",
        null=True,
        blank=True,
    )

    verified_at = models.DateTimeField(
        null=True,
        blank=True,
    )
```

---

# 27. Hospital Service

```python
class HospitalService(BaseModel):

    name = models.CharField(
        max_length=200,
    )

    description = models.TextField(
        blank=True,
    )

    price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["name"],
                name="unique_hospital_service",
            )
        ]
```

Examples:

```text
Doctor Consultation
Emergency
X-Ray
Ultrasound
ECG
Operation
ICU
Physiotherapy
```

---

# 28. Patient Service

Patient কোন service নিয়েছে।

```python
class PatientService(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="services",
    )

    service = models.ForeignKey(
        HospitalService,
        on_delete=models.PROTECT,
        related_name="patient_services",
    )

    appointment = models.ForeignKey(
        Appointment,
        on_delete=models.PROTECT,
        related_name="services",
        null=True,
        blank=True,
    )

    quantity = models.PositiveIntegerField(
        default=1,
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 29. Invoice

Hospital billing-এর central model।

```python
class HospitalInvoice(BaseModel):

    STATUS_CHOICES = [
        ("draft", "Draft"),
        ("pending", "Pending"),
        ("partial", "Partial"),
        ("paid", "Paid"),
        ("cancelled", "Cancelled"),
        ("refunded", "Refunded"),
    ]

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="invoices",
    )

    admission = models.ForeignKey(
        Admission,
        on_delete=models.PROTECT,
        related_name="invoices",
        null=True,
        blank=True,
    )

    invoice_number = models.CharField(
        max_length=100,
        unique=True,
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    tax = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    issued_at = models.DateTimeField()

    due_date = models.DateField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["patient", "-created_at"]
            ),
            models.Index(
                fields=["status", "due_date"]
            ),
        ]
```

---

# 30. Invoice Item

```python
class HospitalInvoiceItem(BaseModel):

    invoice = models.ForeignKey(
        HospitalInvoice,
        on_delete=models.CASCADE,
        related_name="items",
    )

    description = models.CharField(
        max_length=250,
    )

    quantity = models.PositiveIntegerField(
        default=1,
    )

    unit_price = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    subtotal = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 31. Payment

```python
class HospitalPayment(BaseModel):

    METHOD_CHOICES = [
        ("cash", "Cash"),
        ("card", "Card"),
        ("bank", "Bank"),
        ("mobile_banking", "Mobile Banking"),
        ("insurance", "Insurance"),
    ]

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
        ("partial", "Partial"),
    ]

    invoice = models.ForeignKey(
        HospitalInvoice,
        on_delete=models.PROTECT,
        related_name="payments",
    )

    transaction_id = models.CharField(
        max_length=150,
        unique=True,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    method = models.CharField(
        max_length=30,
        choices=METHOD_CHOICES,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    paid_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["invoice", "status"]
            ),
            models.Index(
                fields=["status", "-created_at"]
            ),
        ]
```

---

# 32. Insurance Provider

```python
class InsuranceProvider(BaseModel):

    name = models.CharField(
        max_length=200,
        unique=True,
    )

    phone = models.CharField(
        max_length=30,
    )

    email = models.EmailField(
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 33. Patient Insurance

```python
class PatientInsurance(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.PROTECT,
        related_name="insurances",
    )

    provider = models.ForeignKey(
        InsuranceProvider,
        on_delete=models.PROTECT,
        related_name="patient_insurances",
    )

    policy_number = models.CharField(
        max_length=150,
    )

    coverage_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    valid_from = models.DateField()

    valid_until = models.DateField()

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["provider", "policy_number"],
                name="unique_insurance_policy",
            )
        ]
```

---

# 34. Discharge Summary

```python
class DischargeSummary(BaseModel):

    admission = models.OneToOneField(
        Admission,
        on_delete=models.PROTECT,
        related_name="discharge_summary",
    )

    diagnosis = models.TextField()

    treatment_summary = models.TextField()

    medicines = models.TextField(
        blank=True,
    )

    follow_up_instructions = models.TextField(
        blank=True,
    )

    discharged_at = models.DateTimeField()

    prepared_by = models.ForeignKey(
        DoctorProfile,
        on_delete=models.PROTECT,
        related_name="discharge_summaries",
    )
```

---

# 35. Hospital Review

```python
class HospitalReview(BaseModel):

    patient = models.ForeignKey(
        PatientProfile,
        on_delete=models.CASCADE,
        related_name="hospital_reviews",
    )

    hospital = models.ForeignKey(
        Hospital,
        on_delete=models.CASCADE,
        related_name="reviews",
    )

    appointment = models.ForeignKey(
        Appointment,
        on_delete=models.PROTECT,
        related_name="review",
    )

    rating = models.PositiveSmallIntegerField()

    comment = models.TextField(
        blank=True,
    )

    is_published = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.CheckConstraint(
                condition=(
                    models.Q(rating__gte=1)
                    & models.Q(rating__lte=5)
                ),
                name="hospital_rating_1_5",
            ),

            models.UniqueConstraint(
                fields=["patient", "appointment"],
                name="one_review_per_appointment",
            ),
        ]
```

---

# 36. Notification

```python
class HospitalNotification(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="hospital_notifications",
    )

    title = models.CharField(
        max_length=200,
    )

    message = models.TextField()

    notification_type = models.CharField(
        max_length=50,
    )

    is_read = models.BooleanField(
        default=False,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=[
                    "user",
                    "is_read",
                    "-created_at",
                ]
            )
        ]
```

---

# 37. Idempotency Record

Payment / appointment / billing-এর duplicate request prevent করার জন্য।

```python
class HospitalIdempotencyRecord(BaseModel):

    STATUS_CHOICES = [
        ("processing", "Processing"),
        ("completed", "Completed"),
        ("failed", "Failed"),
    ]

    key = models.CharField(
        max_length=150,
        unique=True,
    )

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="hospital_idempotency_records",
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
    )

    response_data = models.JSONField(
        null=True,
        blank=True,
    )
```

---

# 38. Audit Log

Medical system-এ audit অত্যন্ত গুরুত্বপূর্ণ।

```python
class HospitalAuditLog(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="hospital_audit_logs",
    )

    action = models.CharField(
        max_length=100,
    )

    model_name = models.CharField(
        max_length=100,
    )

    object_id = models.CharField(
        max_length=100,
    )

    old_data = models.JSONField(
        null=True,
        blank=True,
    )

    new_data = models.JSONField(
        null=True,
        blank=True,
    )

    ip_address = models.GenericIPAddressField(
        null=True,
        blank=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["model_name", "object_id"]
            ),
            models.Index(
                fields=["user", "-created_at"]
            ),
        ]
```

---

# 🔗 Complete Relationship Diagram

```text
                             USER
                              │
                 ┌────────────┴─────────────┐
                 │                          │
              HOSPITAL                   PATIENT
                 │                          │
        ┌────────┼───────────┐       ┌──────┼───────────┐
        │        │           │       │      │           │
      Branch  Department   Staff   Profile Address    Insurance
                 │
              Doctors
                 │
        ┌────────┼──────────┐
        │        │          │
    Schedule  Appointment  Treatment
                  │
         ┌────────┼─────────────┐
         │        │             │
    Prescription LabOrder     MedicalRecord
         │          │
      Medicine    LabTest
         │          │
    Prescription  LabReport
       Items
```

### Admission side

```text
Patient
   │
   ↓
Admission
   │
   ├── Doctor
   ├── Room
   ├── NurseAssignment
   ├── Treatment
   ├── Invoice
   └── DischargeSummary
```

### Billing side

```text
Patient
   │
   ↓
Invoice
   │
   ├── InvoiceItem
   │
   └── Payment
```

---

# 🏥 Complete Hospital Workflow

### OPD

```text
Patient
   ↓
Appointment
   ↓
Doctor Consultation
   ↓
Medical Record
   ↓
Prescription
   ↓
Lab Order
   ↓
Invoice
   ↓
Payment
```

### Emergency / IPD

```text
Patient
   ↓
Emergency
   ↓
Admission
   ↓
Room
   ↓
Doctor
   ↓
Nurse
   ↓
Treatment
   ↓
Lab
   ↓
Medicine
   ↓
Invoice
   ↓
Payment
   ↓
Discharge
   ↓
Discharge Summary
```

---

# 🔥 Hospital ORM Practice Topics

এই project-এ তোমার Django ORM-এর প্রায় সব advanced topic practice করা যাবে।

```text
1. Hospital → Branches
2. Hospital → Departments
3. Department → Doctors
4. Doctor → Patients
5. Doctor → Appointments
6. Patient → Appointments
7. Patient → Medical Records
8. Patient → Allergies
9. Patient → Chronic Conditions

10. Doctor Schedule
11. Available Doctors
12. Available Rooms
13. Appointment filtering
14. Appointment date filtering
15. Cancelled appointments
16. Completed appointments

17. Patient admissions
18. Active admissions
19. Discharged patients
20. Room occupancy
21. ICU occupancy
22. Doctor admissions

23. Patient prescriptions
24. Prescription medicines
25. Most prescribed medicine
26. Medicine stock
27. Low-stock medicines

28. Lab orders
29. Pending lab tests
30. Completed lab tests
31. Patient lab history
32. Doctor lab orders

33. Patient invoices
34. Paid invoices
35. Unpaid invoices
36. Partial payments
37. Hospital revenue
38. Monthly revenue

39. Doctor consultation revenue
40. Department revenue
41. Average bill
42. Most expensive treatment

43. Count()
44. Sum()
45. Avg()
46. Min()
47. Max()

48. annotate()
49. aggregate()
50. Q()
51. F()
52. Case()
53. When()

54. Exists()
55. Subquery()
56. OuterRef()
57. Window Functions

58. select_related()
59. prefetch_related()
60. Prefetch()

61. transaction.atomic()
62. select_for_update()
63. Race Condition
64. Appointment conflict
65. Room allocation
66. Medicine stock race

67. Constraints
68. Indexing
69. EXPLAIN
70. Query Optimization
71. Pagination
72. Hospital data isolation
73. Audit logging
74. Idempotency
```

---

# ⚡ গুরুত্বপূর্ণ Production Problems

Hospital project-এ কয়েকটি জায়গা বিশেষভাবে challenging হবে।

### 1. Double Appointment

একই doctor-এর একই সময়ে দুই patient:

```text
10:00 ───── 10:30
       Doctor A

Patient 1 → 10:00–10:30
Patient 2 → 10:00–10:30

❌ Conflict
```

এখানে শুধু Python validation যথেষ্ট নয়। Production PostgreSQL-এ transaction + locking / appropriate database constraint ব্যবহার করা উচিত।

---

### 2. Room Double Allocation

```text
Room 301

Patient A → admitted
Patient B → admitted

❌ Same room
```

Admission create করার সময় concurrency handle করতে হবে।

---

### 3. Medicine Stock Race

ধরো stock:

```text
Medicine = 5
```

দুইজন simultaneously medicine issue করলে:

```text
Request A → 5 → 4
Request B → 5 → 4

Wrong ❌
```

এখানে:

```python
transaction.atomic()
```

এর সাথে প্রয়োজন অনুযায়ী:

```python
select_for_update()
```

এবং database-side `F()` expression ব্যবহার করতে হবে।

---

# 🧠 Important Database Design Rules

এই project বানানোর সময় বিশেষভাবে মনে রাখবে:

### Rule 1

`Patient` এবং `Appointment` এক জিনিস না।

```text
Patient = person
Appointment = visit/scheduled event
```

### Rule 2

`Prescription` এবং `Medicine` সরাসরি Many-to-Many না করে:

```text
Prescription
     ↓
PrescriptionItem
     ↓
Medicine
```

করেছি।

### Rule 3

একইভাবে:

```text
LabOrder
   ↓
LabOrderItem
   ↓
LabTest
```

### Rule 4

Invoice:

```text
Invoice
   ↓
InvoiceItem
```

এতে billing-এর historical price preserve করা যায়।

### Rule 5

Medical data অত্যন্ত sensitive। Production system-এ **role-based access control, audit logging, encryption/access controls এবং strict data minimization** দরকার।

---

# 📦 Recommended Django Apps

```text
hospital_management/
│
├── accounts/
│
├── hospitals/
│
├── departments/
│
├── staff/
│
├── doctors/
│
├── patients/
│
├── appointments/
│
├── admissions/
│
├── medical_records/
│
├── pharmacy/
│
├── laboratory/
│
├── billing/
│
├── payments/
│
├── insurance/
│
├── reviews/
│
├── notifications/
│
└── audit/
```

## ⭐ Core Models — আগে এগুলো বানাবে

যদি একসাথে 38টা model বানানো overwhelming হয়, implementation order হবে:

```text
Phase 1
Hospital
Branch
Department
Staff
Doctor
Patient

Phase 2
DoctorDepartment
DoctorSchedule
Appointment

Phase 3
MedicalRecord
Allergy
ChronicCondition

Phase 4
Room
Admission
NurseAssignment
Treatment
DischargeSummary

Phase 5
Medicine
Prescription
PrescriptionItem

Phase 6
LabTest
LabOrder
LabOrderItem
LabReport

Phase 7
HospitalService
PatientService
Invoice
InvoiceItem
Payment

Phase 8
Insurance
Review
Notification
Idempotency
AuditLog
```

এই structure-টা **Django ORM শেখার জন্য খুব strong database-design project**, কারণ এতে তোমার আগে শেখা `relationships → constraints → indexes → aggregation → subquery → select_related/prefetch → transactions → select_for_update → concurrency → EXPLAIN`—প্রায় সবকিছু বাস্তবে প্রয়োগ করা যাবে।
