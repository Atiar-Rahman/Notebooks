Got it! You want a **Scholarship Management System** database design for a **SaaS project**. Let’s structure this step by step and provide a **production-ready ER diagram + table structure** suitable for SaaS. I’ll also consider **multi-tenant capability**, as SaaS platforms usually serve multiple institutions or organizations.

---

## **1. Core Entities**

Here are the main entities:

1. **Organization / Institution** – Each tenant (school, university, NGO)
2. **User** – Admin, Staff, Students
3. **Scholarship** – Scholarship programs offered
4. **Application** – Students apply for scholarships
5. **Eligibility Criteria** – Rules for each scholarship
6. **Documents** – Supporting files uploaded by students
7. **Payment / Disbursement** – Scholarship funds disbursed
8. **Notification / Message** – Alerts to users
9. **Audit / Logs** – Track activities for compliance

---

## **2. ER Diagram Structure (Textual)**

```
Organization (Tenant)
-------------------
org_id (PK)
name
address
contact_email
created_at
updated_at

User
----
user_id (PK)
org_id (FK -> Organization.org_id)
name
email
role (Admin/Staff/Student)
password_hash
created_at
updated_at

Scholarship
-----------
scholarship_id (PK)
org_id (FK -> Organization.org_id)
title
description
total_amount
application_deadline
status (Open/Closed)
created_at
updated_at

EligibilityCriteria
------------------
criteria_id (PK)
scholarship_id (FK -> Scholarship.scholarship_id)
description
min_gpa
required_documents
other_conditions

Application
-----------
application_id (PK)
scholarship_id (FK -> Scholarship.scholarship_id)
user_id (FK -> User.user_id)
status (Pending/Approved/Rejected)
applied_at
reviewed_by (FK -> User.user_id, nullable)
reviewed_at

Document
--------
document_id (PK)
application_id (FK -> Application.application_id)
document_type
file_path
uploaded_at

Payment
-------
payment_id (PK)
application_id (FK -> Application.application_id)
amount
payment_date
payment_status

Notification
------------
notification_id (PK)
user_id (FK -> User.user_id)
message
type (Info/Alert)
read_status (Read/Unread)
created_at

AuditLog
--------
log_id (PK)
user_id (FK -> User.user_id)
action
entity_type (User/Application/Scholarship etc.)
entity_id
timestamp
```

---

## **3. Notes for SaaS Design**

* **Multi-tenancy**: Each `User` and `Scholarship` belongs to an `Organization`.
* **Security**: Store hashed passwords, sensitive info encrypted.
* **Extensibility**: `EligibilityCriteria` allows custom rules per scholarship.
* **Audit**: `AuditLog` helps track all CRUD operations for accountability.
* **Document Management**: `Document.file_path` could point to cloud storage (S3, Firebase Storage).

---

## **4. Optional Advanced Tables**

* **ScholarshipCategory** – For types like Merit-based, Need-based, etc.
* **ScholarshipHistory** – Track changes in scholarship details over time.
* **RolePermissions** – Flexible RBAC system for admin/staff/student roles.

---

## **5. Visual ER Diagram**

If you want, I can generate a **production-ready visual ER diagram** showing all these tables with relationships, foreign keys, and cardinalities — ready for SaaS implementation.

---

Do you want me to create that **visual ER diagram** next?
Absolutely! Adding **categories** to scholarships is actually **very useful**, especially for a SaaS Scholarship Management System. Here’s why and how we can structure it:

---

## **Why Category-Wise Scholarships Are Beneficial**

1. **Better Organization & Filtering**

   * Students can filter scholarships by type: **Merit-based, Need-based, Sports, Research, Minority**, etc.
   * Admins can manage large numbers of scholarships more efficiently.

2. **Analytics & Reporting**

   * You can easily generate reports like: “How many students applied for Merit-based scholarships this year?”
   * Helps in decision-making for funding allocation.

3. **Eligibility Rules by Category**

   * Different categories may have different **criteria**, e.g., GPA threshold for Merit vs. family income for Need-based.

4. **Improved User Experience**

   * Students see only relevant scholarships for them.
   * Staff can assign scholarships more quickly.

---

## **How to Implement Category-Wise Scholarships**

We can create a separate table for **Scholarship Categories** and link it to scholarships.

### **Schema Update**

```sql
ScholarshipCategory
------------------
category_id (PK)
org_id (FK -> Organization.org_id) -- optional, if each org has custom categories
name           -- e.g., Merit-based, Need-based, Sports
description

Scholarship
-----------
scholarship_id (PK)
org_id (FK -> Organization.org_id)
category_id (FK -> ScholarshipCategory.category_id)
title
description
total_amount
application_deadline
status (Open/Closed)
created_at
updated_at
```

* Now each scholarship **belongs to a category**.
* Filtering and reporting become easier.
* If your system grows, you can also support **subcategories** (like “Sports → Football, Cricket”) by adding `parent_category_id` in `ScholarshipCategory`.

---

✅ **Recommendation:** For a SaaS system, **category-wise scholarships are a must**. It makes the platform scalable, easier to manage, and more user-friendly.

---

If you want, I can **update the full ER diagram** to include **categories** and even show **subcategories** for advanced filtering.

Do you want me to do that?
Perfect! Let’s create a **complete, production-ready database system design** for a **SaaS Scholarship Management System** including **category-wise scholarships** and all essential tables for multi-tenant usage, audit, and documents. I’ll provide:

1. **Tables with fields and relationships**
2. **Category support**
3. **Multi-tenancy ready**
4. **Optional advanced features**

---

# **Scholarship Management System – Full Database Design**

---

## **1. Core Entities & Tables**

### **Organization (Tenant)**

Stores each institution using the SaaS system.

| Field         | Type      | Notes                  |
| ------------- | --------- | ---------------------- |
| org_id        | UUID (PK) | Unique organization ID |
| name          | VARCHAR   | Organization name      |
| address       | TEXT      | Optional               |
| contact_email | VARCHAR   | Admin contact          |
| created_at    | TIMESTAMP | Default now()          |
| updated_at    | TIMESTAMP | Auto-update            |

---

### **User**

Stores all users (Admin, Staff, Student) linked to an organization.

| Field         | Type                            | Notes             |
| ------------- | ------------------------------- | ----------------- |
| user_id       | UUID (PK)                       | Unique user ID    |
| org_id        | UUID (FK → Organization.org_id) | Multi-tenant link |
| name          | VARCHAR                         | Full name         |
| email         | VARCHAR                         | Unique per org    |
| role          | ENUM('Admin','Staff','Student') | User role         |
| password_hash | VARCHAR                         | Secure hash       |
| created_at    | TIMESTAMP                       | Default now()     |
| updated_at    | TIMESTAMP                       | Auto-update       |

---

### **ScholarshipCategory**

Categorizes scholarships for filtering and analytics.

| Field              | Type                                        | Notes                             |
| ------------------ | ------------------------------------------- | --------------------------------- |
| category_id        | UUID (PK)                                   | Unique category ID                |
| org_id             | UUID (FK → Organization.org_id)             | Optional, org-specific categories |
| parent_category_id | UUID (FK → ScholarshipCategory.category_id) | For subcategories (nullable)      |
| name               | VARCHAR                                     | e.g., Merit-based, Need-based     |
| description        | TEXT                                        | Optional                          |
| created_at         | TIMESTAMP                                   | Default now()                     |
| updated_at         | TIMESTAMP                                   | Auto-update                       |

---

### **Scholarship**

Represents individual scholarship programs.

| Field                | Type                                        | Notes                  |
| -------------------- | ------------------------------------------- | ---------------------- |
| scholarship_id       | UUID (PK)                                   | Unique scholarship ID  |
| org_id               | UUID (FK → Organization.org_id)             | Tenant link            |
| category_id          | UUID (FK → ScholarshipCategory.category_id) | Scholarship category   |
| title                | VARCHAR                                     | Scholarship name       |
| description          | TEXT                                        | Details of scholarship |
| total_amount         | DECIMAL                                     | Fund amount            |
| application_deadline | DATE                                        | Last date for applying |
| status               | ENUM('Open','Closed')                       | Current status         |
| created_at           | TIMESTAMP                                   | Default now()          |
| updated_at           | TIMESTAMP                                   | Auto-update            |

---

### **EligibilityCriteria**

Defines the rules for each scholarship.

| Field              | Type                                   | Notes                             |
| ------------------ | -------------------------------------- | --------------------------------- |
| criteria_id        | UUID (PK)                              | Unique criteria ID                |
| scholarship_id     | UUID (FK → Scholarship.scholarship_id) | Scholarship link                  |
| description        | TEXT                                   | Description of criteria           |
| min_gpa            | DECIMAL                                | Minimum GPA required (nullable)   |
| required_documents | TEXT                                   | List of required docs (JSON/text) |
| other_conditions   | TEXT                                   | Optional rules                    |
| created_at         | TIMESTAMP                              | Default now()                     |
| updated_at         | TIMESTAMP                              | Auto-update                       |

---

### **Application**

Represents student applications to scholarships.

| Field          | Type                                   | Notes                         |
| -------------- | -------------------------------------- | ----------------------------- |
| application_id | UUID (PK)                              | Unique application ID         |
| scholarship_id | UUID (FK → Scholarship.scholarship_id) | Linked scholarship            |
| user_id        | UUID (FK → User.user_id)               | Student who applied           |
| status         | ENUM('Pending','Approved','Rejected')  | Application status            |
| applied_at     | TIMESTAMP                              | Application timestamp         |
| reviewed_by    | UUID (FK → User.user_id)               | Staff who reviewed (nullable) |
| reviewed_at    | TIMESTAMP                              | Review timestamp (nullable)   |

---

### **Document**

Files uploaded by students for scholarship applications.

| Field          | Type                                   | Notes                         |
| -------------- | -------------------------------------- | ----------------------------- |
| document_id    | UUID (PK)                              | Unique document ID            |
| application_id | UUID (FK → Application.application_id) | Linked application            |
| document_type  | VARCHAR                                | e.g., Transcript, Certificate |
| file_path      | TEXT                                   | Storage path or URL           |
| uploaded_at    | TIMESTAMP                              | Timestamp                     |

---

### **Payment**

Tracks scholarship fund disbursement.

| Field          | Type                                   | Notes              |
| -------------- | -------------------------------------- | ------------------ |
| payment_id     | UUID (PK)                              | Unique payment ID  |
| application_id | UUID (FK → Application.application_id) | Linked application |
| amount         | DECIMAL                                | Amount disbursed   |
| payment_date   | DATE                                   | Date of payment    |
| payment_status | ENUM('Pending','Completed','Failed')   | Status             |

---

### **Notification**

System messages for users.

| Field           | Type                     | Notes                  |
| --------------- | ------------------------ | ---------------------- |
| notification_id | UUID (PK)                | Unique notification ID |
| user_id         | UUID (FK → User.user_id) | Recipient              |
| message         | TEXT                     | Content                |
| type            | ENUM('Info','Alert')     | Message type           |
| read_status     | ENUM('Read','Unread')    | Status                 |
| created_at      | TIMESTAMP                | Timestamp              |

---

### **AuditLog**

Tracks user activity for accountability.

| Field       | Type                     | Notes                             |
| ----------- | ------------------------ | --------------------------------- |
| log_id      | UUID (PK)                | Unique log ID                     |
| user_id     | UUID (FK → User.user_id) | Actor                             |
| action      | VARCHAR                  | e.g., CREATE, UPDATE, DELETE      |
| entity_type | VARCHAR                  | User/Application/Scholarship etc. |
| entity_id   | UUID                     | ID of affected entity             |
| timestamp   | TIMESTAMP                | Action timestamp                  |

---

## **2. Relationships / Cardinality**

* **Organization 1 — M Users**
* **Organization 1 — M Scholarships**
* **ScholarshipCategory 1 — M Scholarships**
* **Scholarship 1 — M EligibilityCriteria**
* **Scholarship 1 — M Applications**
* **Application 1 — M Documents**
* **Application 1 — 1 Payment**
* **User 1 — M Applications**
* **User 1 — M Notifications**
* **User 1 — M AuditLogs**

---

## **3. Advanced Notes**

* **Multi-Tenant SaaS**: Every table except `AuditLog` and maybe `ScholarshipCategory` is linked to `org_id` for separation.
* **Flexible Categories**: `parent_category_id` allows nested categories.
* **Security**: Password hashing + document storage in S3 or Firebase Storage.
* **Extensibility**: Add `RolePermissions` table for more complex RBAC.

---

If you want, I can **draw a full visual ER diagram** showing **all these tables, foreign keys, and cardinalities** so you can hand it to developers or use it in your SaaS project documentation.

Do you want me to do that next?


--------
# Update
Perfect! Let’s update the **full Scholarship Management System database design** to include:

1. **Resume upload** for students.
2. **Application → Documents multi-upload** workflow.
3. **Category-wise scholarships**.
4. **SaaS-ready multi-tenant support**.

This version is **production-ready and student-friendly**.

---

# **Scholarship Management System – Full Updated Database Design**

---

## **1. Core Entities & Tables**

### **Organization (Tenant)**

| Field         | Type      | Notes                  |
| ------------- | --------- | ---------------------- |
| org_id        | UUID PK   | Unique organization ID |
| name          | VARCHAR   | Organization name      |
| address       | TEXT      | Optional               |
| contact_email | VARCHAR   | Admin contact          |
| created_at    | TIMESTAMP | Default now()          |
| updated_at    | TIMESTAMP | Auto-update            |

---

### **User**

All users (Admin, Staff, Student) with multi-tenant support.

| Field         | Type                            | Notes                                       |
| ------------- | ------------------------------- | ------------------------------------------- |
| user_id       | UUID PK                         | Unique user ID                              |
| org_id        | UUID FK → Organization.org_id   | Tenant link                                 |
| name          | VARCHAR                         | Full name                                   |
| email         | VARCHAR                         | Unique per org                              |
| role          | ENUM('Admin','Staff','Student') | User role                                   |
| password_hash | VARCHAR                         | Secure hash                                 |
| resume_path   | TEXT                            | Optional – single resume upload per student |
| created_at    | TIMESTAMP                       | Default now()                               |
| updated_at    | TIMESTAMP                       | Auto-update                                 |

---

### **ScholarshipCategory**

Optional nested categories for scholarships.

| Field              | Type                                      | Notes                                  |
| ------------------ | ----------------------------------------- | -------------------------------------- |
| category_id        | UUID PK                                   | Unique category ID                     |
| org_id             | UUID FK → Organization.org_id             | Optional – org-specific categories     |
| parent_category_id | UUID FK → ScholarshipCategory.category_id | Nullable – subcategories               |
| name               | VARCHAR                                   | Category name, e.g., Merit, Need-based |
| description        | TEXT                                      | Optional description                   |
| created_at         | TIMESTAMP                                 | Default now()                          |
| updated_at         | TIMESTAMP                                 | Auto-update                            |

---

### **Scholarship**

Each scholarship program, linked to category.

| Field                | Type                                      | Notes                 |
| -------------------- | ----------------------------------------- | --------------------- |
| scholarship_id       | UUID PK                                   | Unique scholarship ID |
| org_id               | UUID FK → Organization.org_id             | Tenant link           |
| category_id          | UUID FK → ScholarshipCategory.category_id | Scholarship category  |
| title                | VARCHAR                                   | Scholarship name      |
| description          | TEXT                                      | Details               |
| total_amount         | DECIMAL                                   | Fund amount           |
| application_deadline | DATE                                      | Last date             |
| status               | ENUM('Open','Closed')                     | Current status        |
| created_at           | TIMESTAMP                                 | Default now()         |
| updated_at           | TIMESTAMP                                 | Auto-update           |

---

### **EligibilityCriteria**

Rules for scholarships.

| Field              | Type                                 | Notes                           |
| ------------------ | ------------------------------------ | ------------------------------- |
| criteria_id        | UUID PK                              | Unique criteria ID              |
| scholarship_id     | UUID FK → Scholarship.scholarship_id | Scholarship link                |
| description        | TEXT                                 | Criteria description            |
| min_gpa            | DECIMAL                              | Optional                        |
| required_documents | TEXT                                 | JSON/text list of required docs |
| other_conditions   | TEXT                                 | Optional                        |
| created_at         | TIMESTAMP                            | Default now()                   |
| updated_at         | TIMESTAMP                            | Auto-update                     |

---

### **Application**

Students apply to scholarships. Supports document uploads.

| Field          | Type                                  | Notes                   |
| -------------- | ------------------------------------- | ----------------------- |
| application_id | UUID PK                               | Unique application ID   |
| scholarship_id | UUID FK → Scholarship.scholarship_id  | Linked scholarship      |
| user_id        | UUID FK → User.user_id                | Student                 |
| status         | ENUM('Pending','Approved','Rejected') | Application status      |
| applied_at     | TIMESTAMP                             | Timestamp of submission |
| reviewed_by    | UUID FK → User.user_id                | Staff reviewer          |
| reviewed_at    | TIMESTAMP                             | Nullable                |

---

### **Document**

Multiple documents per application.

| Field          | Type                                 | Notes                         |
| -------------- | ------------------------------------ | ----------------------------- |
| document_id    | UUID PK                              | Unique document ID            |
| application_id | UUID FK → Application.application_id | Linked application            |
| document_type  | VARCHAR                              | Transcript, Certificate, etc. |
| file_path      | TEXT                                 | Cloud storage URL/path        |
| uploaded_at    | TIMESTAMP                            | Timestamp                     |
| is_mandatory   | BOOLEAN                              | Check required documents      |

---

### **Payment**

Tracks scholarship disbursement.

| Field          | Type                                 | Notes              |
| -------------- | ------------------------------------ | ------------------ |
| payment_id     | UUID PK                              | Unique payment ID  |
| application_id | UUID FK → Application.application_id | Linked application |
| amount         | DECIMAL                              | Amount paid        |
| payment_date   | DATE                                 | Date of payment    |
| payment_status | ENUM('Pending','Completed','Failed') | Status             |

---

### **Notification**

Alerts for users.

| Field           | Type                   | Notes                  |
| --------------- | ---------------------- | ---------------------- |
| notification_id | UUID PK                | Unique notification ID |
| user_id         | UUID FK → User.user_id | Recipient              |
| message         | TEXT                   | Content                |
| type            | ENUM('Info','Alert')   | Notification type      |
| read_status     | ENUM('Read','Unread')  | Status                 |
| created_at      | TIMESTAMP              | Timestamp              |

---

### **AuditLog**

Tracks user activity.

| Field       | Type                   | Notes                             |
| ----------- | ---------------------- | --------------------------------- |
| log_id      | UUID PK                | Unique log ID                     |
| user_id     | UUID FK → User.user_id | Actor                             |
| action      | VARCHAR                | CREATE/UPDATE/DELETE              |
| entity_type | VARCHAR                | User/Application/Scholarship/etc. |
| entity_id   | UUID                   | ID of affected entity             |
| timestamp   | TIMESTAMP              | Action timestamp                  |

---

## **2. Relationships**

* **Organization 1 — M Users**
* **Organization 1 — M Scholarships**
* **ScholarshipCategory 1 — M Scholarships**
* **Scholarship 1 — M EligibilityCriteria**
* **Scholarship 1 — M Applications**
* **Application 1 — M Documents**
* **Application 1 — 1 Payment**
* **User 1 — M Applications**
* **User 1 — M Notifications**
* **User 1 — M AuditLogs**

---

## **3. Notes & Best Practices**

1. **Resume Upload:** Stored per student in `User.resume_path`. Optional.
2. **Multiple Documents:** `Document` table supports **any number of uploads per application**.
3. **Validation:** Use `EligibilityCriteria.required_documents` + `Document.is_mandatory` to check submission completeness.
4. **SaaS Ready:** All main entities are linked to `org_id` for multi-tenancy.
5. **Cloud Storage:** Keep file paths in DB, store documents/resumes in S3/Firebase/GCS.
6. **Extensibility:** Can add `ScholarshipSubmissions`, `RolePermissions`, or `DocumentVersion` if needed in the future.

---

If you want, I can **draw a visual ER diagram** for this **updated full database design** showing **all tables, foreign keys, and multi-document support**, ready to hand to developers.

Do you want me to create that visual ER diagram?


Perfect! Let’s write a **full, production-ready Django model code** for your **Scholarship Management System** including:

* **Multi-tenant support** (`Organization`)
* **Category-wise scholarships** (`ScholarshipCategory`)
* **Application → Documents multi-upload**
* **Resume upload per student**
* All other entities like `Payment`, `Notification`, `AuditLog`

This will be **complete and ready to plug into Django**.

---

```python
# models.py
from django.db import models
import uuid

# ---------------------------
# Organization / Tenant
# ---------------------------
class Organization(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    name = models.CharField(max_length=255)
    address = models.TextField(blank=True, null=True)
    contact_email = models.EmailField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.name


# ---------------------------
# User
# ---------------------------
class User(models.Model):
    ROLE_CHOICES = [
        ('Admin', 'Admin'),
        ('Staff', 'Staff'),
        ('Student', 'Student'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    org = models.ForeignKey(Organization, on_delete=models.CASCADE, related_name='users')
    name = models.CharField(max_length=255)
    email = models.EmailField()
    role = models.CharField(max_length=20, choices=ROLE_CHOICES)
    password_hash = models.CharField(max_length=255)
    resume_path = models.TextField(blank=True, null=True)  # Optional resume
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        unique_together = ('org', 'email')  # unique email per organization

    def __str__(self):
        return self.name


# ---------------------------
# Scholarship Category
# ---------------------------
class ScholarshipCategory(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    org = models.ForeignKey(Organization, on_delete=models.CASCADE, related_name='categories')
    parent_category = models.ForeignKey('self', on_delete=models.SET_NULL, null=True, blank=True, related_name='subcategories')
    name = models.CharField(max_length=255)
    description = models.TextField(blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.name


# ---------------------------
# Scholarship
# ---------------------------
class Scholarship(models.Model):
    STATUS_CHOICES = [
        ('Open', 'Open'),
        ('Closed', 'Closed'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    org = models.ForeignKey(Organization, on_delete=models.CASCADE, related_name='scholarships')
    category = models.ForeignKey(ScholarshipCategory, on_delete=models.SET_NULL, null=True, blank=True, related_name='scholarships')
    title = models.CharField(max_length=255)
    description = models.TextField()
    total_amount = models.DecimalField(max_digits=12, decimal_places=2)
    application_deadline = models.DateField()
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='Open')
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title


# ---------------------------
# Eligibility Criteria
# ---------------------------
class EligibilityCriteria(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    scholarship = models.ForeignKey(Scholarship, on_delete=models.CASCADE, related_name='criteria')
    description = models.TextField()
    min_gpa = models.DecimalField(max_digits=4, decimal_places=2, null=True, blank=True)
    required_documents = models.JSONField(default=list, blank=True)  # list of required document types
    other_conditions = models.TextField(blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return f"Criteria for {self.scholarship.title}"


# ---------------------------
# Application
# ---------------------------
class Application(models.Model):
    STATUS_CHOICES = [
        ('Pending', 'Pending'),
        ('Approved', 'Approved'),
        ('Rejected', 'Rejected'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    scholarship = models.ForeignKey(Scholarship, on_delete=models.CASCADE, related_name='applications')
    student = models.ForeignKey(User, on_delete=models.CASCADE, related_name='applications')
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='Pending')
    applied_at = models.DateTimeField(auto_now_add=True)
    reviewed_by = models.ForeignKey(User, on_delete=models.SET_NULL, null=True, blank=True, related_name='reviewed_applications')
    reviewed_at = models.DateTimeField(null=True, blank=True)

    def __str__(self):
        return f"{self.student.name} - {self.scholarship.title}"


# ---------------------------
# Document (Multiple per Application)
# ---------------------------
class Document(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    application = models.ForeignKey(Application, on_delete=models.CASCADE, related_name='documents')
    document_type = models.CharField(max_length=100)
    file_path = models.TextField()
    uploaded_at = models.DateTimeField(auto_now_add=True)
    is_mandatory = models.BooleanField(default=False)

    def __str__(self):
        return f"{self.document_type} for {self.application}"


# ---------------------------
# Payment
# ---------------------------
class Payment(models.Model):
    STATUS_CHOICES = [
        ('Pending', 'Pending'),
        ('Completed', 'Completed'),
        ('Failed', 'Failed'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    application = models.OneToOneField(Application, on_delete=models.CASCADE, related_name='payment')
    amount = models.DecimalField(max_digits=12, decimal_places=2)
    payment_date = models.DateField()
    payment_status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='Pending')

    def __str__(self):
        return f"Payment for {self.application}"


# ---------------------------
# Notification
# ---------------------------
class Notification(models.Model):
    TYPE_CHOICES = [
        ('Info', 'Info'),
        ('Alert', 'Alert'),
    ]

    STATUS_CHOICES = [
        ('Read', 'Read'),
        ('Unread', 'Unread'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='notifications')
    message = models.TextField()
    type = models.CharField(max_length=20, choices=TYPE_CHOICES)
    read_status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='Unread')
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"Notification for {self.user.name}"


# ---------------------------
# Audit Log
# ---------------------------
class AuditLog(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    user = models.ForeignKey(User, on_delete=models.CASCADE, related_name='audit_logs')
    action = models.CharField(max_length=100)  # CREATE, UPDATE, DELETE
    entity_type = models.CharField(max_length=50)  # User, Application, Scholarship, etc.
    entity_id = models.UUIDField()
    timestamp = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.action} by {self.user.name} on {self.entity_type}"
```

---

## ✅ **Key Features of This Model Design**

1. **Multi-Tenant Ready:** All main entities link to `Organization`.
2. **Category-Wise Scholarships:** `ScholarshipCategory` with optional subcategories.
3. **Resume Upload:** `User.resume_path` stores optional resume.
4. **Application → Documents:** One-to-many relationship supports multiple document uploads.
5. **Payments, Notifications, Audit Logs:** Fully integrated.
6. **Production-Ready:** UUID PKs, timestamps, proper relationships, ready for Django ORM.

---

If you want, I can **also make a visual ER diagram** from this **full model**, showing **all relationships, foreign keys, and multi-document support**.

Do you want me to do that next?

