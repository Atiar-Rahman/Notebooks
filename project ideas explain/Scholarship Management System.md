
Scholarship Management System ডিজাইন করার সময় **Model (Database Design)** সবচেয়ে গুরুত্বপূর্ণ অংশ। আমি এটা **Django mindset + real-world system** ধরে বুঝাচ্ছি, যেন ভবিষ্যতে ML / analytics / scalability-ও add করা যায়।

---

## 1️⃣ প্রথমে কোন দিক থেকে চিন্তা করবে? (Thinking Approach)

সবসময় এই ৩টা প্রশ্ন করো:

### 🔹 Q1: কারা এই সিস্টেম ব্যবহার করবে?

👉 **Actors / Roles**

- Student
    
- Scholarship Provider / Organization
    
- Admin
    
- Reviewer / Committee (optional)
    

### 🔹 Q2: তারা কী কী কাজ করবে?

👉 **Actions / Use-cases**

- Scholarship post করা
    
- Apply করা
    
- Document upload
    
- Eligibility check
    
- Review & approval
    
- Payment tracking
    
- Notification
    

### 🔹 Q3: এই কাজগুলোর জন্য কী data দরকার?

👉 এখান থেকেই **Model বের হয়**

---

## 2️⃣ Core Models (Must Have)

### 🔹 1. User Model (Custom User – Strongly Recommended)

```text
User
----
id
name
email
password
role (STUDENT / PROVIDER / ADMIN)
is_active
created_at
```

👉 Django তে:

- `AbstractUser` extend করবে
    
- role = `choices`
    

---

### 🔹 2. Student Profile

```text
StudentProfile
---------------
user (OneToOne)
date_of_birth
gender
institution
department
cgpa
family_income
address
```

📌 Reason:

- User generic
    
- Student-specific data আলাদা রাখা clean design
    

---

### 🔹 3. Organization / Provider

```text
Organization
------------
user (OneToOne)
organization_name
type (Govt / NGO / Private)
contact_email
website
verified
```

---

### 🔹 4. Scholarship Model (Heart of System ❤️)

```text
Scholarship
-----------
id
title
description
amount
category
deadline
min_cgpa
max_income
eligible_degree
organization (ForeignKey)
created_at
status (OPEN / CLOSED)
```

👉 এখান থেকেই:

- Apply
    
- Eligibility check
    
- Search & filter
    

---

## 3️⃣ Application & Process Models

### 🔹 5. Scholarship Application

```text
Application
-----------
student (ForeignKey)
scholarship (ForeignKey)
status (APPLIED / UNDER_REVIEW / APPROVED / REJECTED)
applied_at
remarks
score (optional – ML future)
```

📌 **Most important relation table**

- Many students → many scholarships
    

---

### 🔹 6. Documents Model

```text
Document
--------
application (ForeignKey)
document_type (Transcript / Income Certificate)
file
verified
```

---

### 🔹 7. Review / Evaluation

```text
Review
------
application (ForeignKey)
reviewer (ForeignKey -> User)
score
comment
reviewed_at
```

---

## 4️⃣ Admin & System Models

### 🔹 8. Payment / Disbursement

```text
Payment
-------
application (OneToOne)
amount
payment_date
status (PENDING / PAID)
transaction_id
```

---

### 🔹 9. Notification

```text
Notification
------------
user (ForeignKey)
message
is_read
created_at
```

---

## 5️⃣ Optional but Advanced (Real-World Touch 🔥)

### 🔹 Eligibility Rule (Dynamic)

```text
EligibilityRule
---------------
scholarship
rule_type (CGPA / INCOME / DEPARTMENT)
min_value
max_value
```

👉 Future:

- Rule Engine
    
- Auto eligibility checker
    

---

### 🔹 ML / Analytics Ready Model

```text
ApplicationScore
----------------
application
eligibility_score
document_score
final_score
```

👉 Later:

- ML model দিয়ে **approve probability**
    
- Ranking system
    

---

## 6️⃣ Relationships Summary (Interview Friendly)

```text
User
 ├── StudentProfile (1–1)
 ├── Organization (1–1)

Organization
 └── Scholarship (1–M)

Scholarship
 └── Application (1–M)

Student
 └── Application (1–M)

Application
 ├── Document (1–M)
 ├── Review (1–M)
 └── Payment (1–1)
```

---

## 7️⃣ Django App Structure (Best Practice)

```text
accounts/
scholarships/
applications/
reviews/
payments/
notifications/
```

---

## 8️⃣ তুমি চাইলে পরের ধাপে আমি দিতে পারি:

- ✅ **Django models.py code**
    
- ✅ **ER Diagram (visual)**
    
- ✅ **REST API design (DRF)**
    
- ✅ **ML-based eligibility checker idea**
    
- ✅ **Admin dashboard workflow**
    

👉 বলো, **কোনটা next চাই?**