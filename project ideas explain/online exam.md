Database design করার সময় শুধু টেবিল বানালেই হবে না, **Normalization**, **Relationship**, **Scalability** এবং **Data Integrity** মাথায় রাখতে হবে। তোমার Online Exam System-এর জন্য নিচের design অনুসরণ করলে ভবিষ্যতে feature যোগ করাও সহজ হবে।

# Database ER Diagram (Concept)

```text
User
 │
 ├──────────────┐
 │              │
Teacher      Student
 │              │
 └──────┬───────┘
        │
      Exam
        │
 ┌──────┼──────────┐
 │      │          │
Question AccessKey Registration
 │                  │
Choice          ExamAttempt
                     │
              StudentAnswer
```

---

# 1. User

একটি User টেবিলেই সব Role রাখো।

|Field|Type|
|---|---|
|id|PK|
|username|varchar|
|email|varchar|
|password|varchar|
|role|Admin/Teacher/Student|
|is_active|boolean|
|created_at|datetime|

Relationship

```
One User
     │
     ├── Teacher
     └── Student
```

---

# 2. Teacher

|Field|Type|
|---|---|
|id|PK|
|user_id|FK(User)|
|department|varchar|

---

# 3. Student

|Field|Type|
|---|---|
|id|PK|
|user_id|FK(User)|
|student_id|varchar|
|department|varchar|
|semester|int|

---

# 4. Exam

একটি Exam মানে একটি Question Set।

|Field|Type|
|---|---|
|id|PK|
|teacher_id|FK(Teacher)|
|title|varchar|
|description|text|
|duration|int|
|total_marks|int|
|start_time|datetime|
|end_time|datetime|
|status|Draft/Published/Closed|

Relationship

```
Teacher
    │
    └──────< Exam
```

একজন Teacher অনেক Exam তৈরি করতে পারে।

---

# 5. Exam Access Key

প্রতিটি Exam-এর জন্য একটি Access Code থাকবে।

|Field|Type|
|---|---|
|id|PK|
|exam_id|FK|
|access_code|varchar|
|valid_from|datetime|
|valid_until|datetime|
|is_active|boolean|

Example

```
Exam

Mid Final

↓

Access Code

458963

↓

Valid

9:50 AM

to

10:10 AM
```

Student এই সময়ের মধ্যে Code ব্যবহার করতে পারবে।

---

# 6. Registration

Student আগে Registration করবে।

|Field|Type|
|---|---|
|id|PK|
|exam_id|FK|
|student_id|FK|
|registered_at|datetime|
|status|Registered/Cancelled|

Relationship

```
Student

     M
      \
       \
        Registration
       /
      /
     M

Exam
```

এটা Many-to-Many Relationship।

---

# 7. Question

|Field|Type|
|---|---|
|id|PK|
|exam_id|FK|
|question|text|
|type|MCQ/TrueFalse/Short|
|marks|int|
|order|int|

Relationship

```
Exam

│

├── Question 1

├── Question 2

├── Question 3
```

---

# 8. Choice

শুধু MCQ-এর জন্য।

|Field|Type|
|---|---|
|id|PK|
|question_id|FK|
|option|text|
|is_correct|boolean|

Relationship

```
Question

│

├── A

├── B

├── C

└── D
```

---

# 9. Exam Attempt

Student Exam Start করলে একটি Attempt তৈরি হবে।

|Field|Type|
|---|---|
|id|PK|
|exam_id|FK|
|student_id|FK|
|started_at|datetime|
|submitted_at|datetime|
|score|decimal|
|status|Running/Submitted/Timeout|

Relationship

```
Student

│

└── Attempt

        │

        └── Exam
```

---

# 10. Student Answer

|Field|Type|
|---|---|
|id|PK|
|attempt_id|FK|
|question_id|FK|
|choice_id|FK (nullable)|
|text_answer|text|
|obtained_marks|decimal|

Relationship

```
Attempt

│

├── Answer 1

├── Answer 2

└── Answer 3
```

---

# Relationship Summary

```
User (1)
   │
   ├────────Teacher (1)
   │            │
   │            └────────── Exam (M)
   │                         │
   │                         ├──────── Question (M)
   │                         │              │
   │                         │              └──── Choice (M)
   │                         │
   │                         ├──────── AccessKey (1)
   │                         │
   │                         └──────── Registration (M)
   │
   └────────Student (1)
                    │
                    ├──────── Registration (M)
                    │
                    └──────── Attempt (M)
                                   │
                                   └────── StudentAnswer (M)
```

# Normalization

এই ডিজাইনটি **Third Normal Form (3NF)** অনুসরণ করে:

- User-এর তথ্য এক জায়গায়।
    
- Teacher/Student-এর আলাদা তথ্য আলাদা টেবিলে।
    
- Exam, Question, Choice আলাদা টেবিলে।
    
- একই তথ্য বারবার সংরক্ষণ করা হয় না (Redundancy কমে)।
    
- Foreign Key ব্যবহার করে Referential Integrity বজায় থাকে।
    

# Django Model Mapping

এই ERD থেকে Django-তে আলাদা app করা ভালো হবে:

```
accounts/
    models.py
        User
        Teacher
        Student

exams/
    models.py
        Exam
        AccessKey
        Registration

questions/
    models.py
        Question
        Choice

attempts/
    models.py
        Attempt
        StudentAnswer
```

এই structure maintain করা সহজ এবং বড় project-এও scalable থাকে।

**পরামর্শ:** Exam Access Key-কে আলাদা টেবিলে রাখার পরিবর্তে `Exam` টেবিলেই `access_code`, `valid_from`, `valid_until` রাখা যেতে পারে যদি প্রতিটি Exam-এর জন্য সবসময় একটি মাত্র code থাকে। কিন্তু ভবিষ্যতে যদি একই Exam-এর জন্য একাধিক code বা ভিন্ন batch-এর জন্য আলাদা code দিতে চাও, তাহলে আলাদা `ExamAccessKey` টেবিল রাখাই বেশি flexible হবে।


তোমার Online Examination System-এর জন্য নিচের **main tables** যথেষ্ট। এই design ভবিষ্যতে নতুন feature যোগ করলেও পরিবর্তন কম লাগবে।

| Table              | Purpose                       |
| ------------------ | ----------------------------- |
| users              | Admin, Teacher, Student login |
| student_profiles   | Student information           |
| teacher_profiles   | Teacher information           |
| exams              | Exam information              |
| exam_access_keys   | Exam access code              |
| exam_registrations | Student registration          |
| questions          | Exam questions                |
| choices            | MCQ options                   |
| exam_attempts      | Student exam session          |
| student_answers    | Student answers               |

---

# 1. users

```sql
id (PK)
username
email
password
first_name
last_name
role
is_active
is_staff
created_at
updated_at
```

**role**

* ADMIN
* TEACHER
* STUDENT

---

# 2. student_profiles

```sql
id (PK)
user_id (FK -> users.id)
student_id
department
semester
session
phone
address
created_at
updated_at
```

---

# 3. teacher_profiles

```sql
id (PK)
user_id (FK -> users.id)
employee_id
department
designation
phone
created_at
updated_at
```

---

# 4. exams

```sql
id (PK)
teacher_id (FK -> teacher_profiles.id)

title
description

duration_minutes

total_marks

pass_marks

start_time

end_time

status

created_at
updated_at
```

**status**

```text
Draft
Published
Closed
```

---

# 5. exam_access_keys

```sql
id (PK)
exam_id (FK -> exams.id)

access_code

valid_from

valid_until

is_active

created_at
```

একটি Exam-এর একাধিক Access Key রাখা সম্ভব হবে (যদি ভবিষ্যতে দরকার হয়)।

---

# 6. exam_registrations

```sql
id (PK)

student_id (FK -> student_profiles.id)

exam_id (FK -> exams.id)

registered_at

status
```

**status**

```text
Registered
Cancelled
Completed
Absent
```

একজন Student অনেক Exam-এ Register করতে পারে এবং একটি Exam-এ অনেক Student Register করতে পারে (Many-to-Many সম্পর্ক)।

---

# 7. questions

```sql
id (PK)

exam_id (FK -> exams.id)

question_text

question_type

marks

order_no

created_at
updated_at
```

**question_type**

```text
MCQ
TRUE_FALSE
SHORT
LONG
```

---

# 8. choices

```sql
id (PK)

question_id (FK -> questions.id)

choice_text

is_correct

order_no
```

শুধুমাত্র MCQ প্রশ্নের জন্য ব্যবহার হবে।

---

# 9. exam_attempts

```sql
id (PK)

exam_id (FK -> exams.id)

student_id (FK -> student_profiles.id)

started_at

submitted_at

total_score

status
```

**status**

```text
Running
Submitted
Timeout
```

এই টেবিল বলে দেবে কোন Student কখন Exam শুরু করেছে, শেষ করেছে এবং কত নম্বর পেয়েছে।

---

# 10. student_answers

```sql
id (PK)

attempt_id (FK -> exam_attempts.id)

question_id (FK -> questions.id)

choice_id (FK -> choices.id, NULL)

text_answer

obtained_marks

answered_at
```

MCQ হলে `choice_id` ব্যবহার হবে, Short/Long প্রশ্ন হলে `text_answer` ব্যবহার হবে।

---

# Relationship Summary

```text
users
 │
 ├── teacher_profiles
 │         │
 │         └──────── exams
 │                    │
 │                    ├──────── questions
 │                    │            │
 │                    │            └────── choices
 │                    │
 │                    ├──────── exam_access_keys
 │                    │
 │                    └──────── exam_registrations
 │
 └── student_profiles
           │
           ├──────── exam_registrations
           │
           └──────── exam_attempts
                        │
                        └──────── student_answers
```

## Optional Tables (ভবিষ্যতের জন্য)

প্রজেক্টকে আরও উন্নত করতে চাইলে পরে এগুলো যোগ করতে পারো:

* `subjects` – কোন Subject-এর Exam
* `departments` – Department আলাদা টেবিল
* `results` – Published Result আলাদা রাখা
* `notifications` – Student/Teacher Notification
* `exam_logs` – কে কখন Login/Start/Submit করেছে

এই ১০টি মূল টেবিল দিয়ে একটি সম্পূর্ণ Online Examination System তৈরি করা যায় এবং Django REST Framework-এ API বানানোর জন্য এটি একটি পরিষ্কার ও scalable database structure।
