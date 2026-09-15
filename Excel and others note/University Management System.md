অবশ্যই। এবার **University Management System (UMS)**-এর জন্যও আগের Project গুলোর মতো **complete production-style Django ORM model architecture** দিচ্ছি।

এখানে আমরা শুধু `Student`, `Teacher`, `Course` রাখব না। পুরো university workflow ধরব:

**University → Campus → Faculty → Department → Program → Semester → Course → Section → Teacher → Student → Enrollment → Attendance → Exam → Result → Fee → Payment → Scholarship → Library → Hostel**

---

# 🎓 Complete University Management System

## 1. Overall Architecture

```text
                              UNIVERSITY
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                 CAMPUS                      FACULTY
                    │                           │
                    │                      DEPARTMENT
                    │                           │
                    │                        PROGRAM
                    │                           │
                    └──────────────┬────────────┘
                                   │
                              ACADEMIC YEAR
                                   │
                               SEMESTER
                                   │
                                COURSE
                                   │
                                SECTION
                                   │
                     ┌─────────────┼─────────────┐
                     │             │             │
                  TEACHER       STUDENT       CLASS
                     │             │
                     │        ENROLLMENT
                     │             │
                     └─────── COURSE ───────────┘
```

---

# 2. BaseModel

```python
from django.db import models
from django.conf import settings


class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

---

# 3. University

```python
class University(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("active", "Active"),
        ("suspended", "Suspended"),
        ("inactive", "Inactive"),
    ]

    name = models.CharField(
        max_length=200,
    )

    code = models.CharField(
        max_length=50,
        unique=True,
    )

    registration_number = models.CharField(
        max_length=100,
        unique=True,
    )

    email = models.EmailField()

    phone = models.CharField(
        max_length=30,
    )

    website = models.URLField(
        blank=True,
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
            models.Index(
                fields=["status"]
            ),
            models.Index(
                fields=["city", "status"]
            ),
        ]
```

---

# 4. Campus

একটি university-এর multiple campus থাকতে পারে।

```python
class Campus(BaseModel):

    university = models.ForeignKey(
        University,
        on_delete=models.CASCADE,
        related_name="campuses",
    )

    name = models.CharField(
        max_length=150,
    )

    code = models.CharField(
        max_length=50,
    )

    address = models.TextField()

    city = models.CharField(
        max_length=100,
    )

    phone = models.CharField(
        max_length=30,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["university", "code"],
                name="unique_university_campus_code",
            )
        ]

        indexes = [
            models.Index(
                fields=["university", "is_active"]
            ),
        ]
```

---

# 5. Faculty

```text
Faculty of Science
Faculty of Engineering
Faculty of Business
Faculty of Arts
```

```python
class Faculty(BaseModel):

    university = models.ForeignKey(
        University,
        on_delete=models.CASCADE,
        related_name="faculties",
    )

    name = models.CharField(
        max_length=150,
    )

    code = models.CharField(
        max_length=50,
    )

    dean_name = models.CharField(
        max_length=150,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["university", "code"],
                name="unique_university_faculty_code",
            )
        ]
```

---

# 6. Department

```text
CSE
EEE
BBA
English
Law
```

```python
class Department(BaseModel):

    faculty = models.ForeignKey(
        Faculty,
        on_delete=models.CASCADE,
        related_name="departments",
    )

    name = models.CharField(
        max_length=150,
    )

    code = models.CharField(
        max_length=50,
    )

    description = models.TextField(
        blank=True,
    )

    head_name = models.CharField(
        max_length=150,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["faculty", "code"],
                name="unique_faculty_department_code",
            )
        ]

        indexes = [
            models.Index(
                fields=["faculty", "is_active"]
            ),
        ]
```

---

# 7. Academic Program

একটি department-এর বিভিন্ন program:

```text
BSc in CSE
MSc in CSE
BBA
MBA
```

```python
class AcademicProgram(BaseModel):

    PROGRAM_TYPES = [
        ("undergraduate", "Undergraduate"),
        ("graduate", "Graduate"),
        ("postgraduate", "Postgraduate"),
        ("diploma", "Diploma"),
        ("phd", "PhD"),
    ]

    department = models.ForeignKey(
        Department,
        on_delete=models.PROTECT,
        related_name="programs",
    )

    name = models.CharField(
        max_length=200,
    )

    code = models.CharField(
        max_length=50,
    )

    program_type = models.CharField(
        max_length=30,
        choices=PROGRAM_TYPES,
    )

    duration_years = models.DecimalField(
        max_digits=4,
        decimal_places=1,
    )

    total_credits = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["department", "code"],
                name="unique_department_program_code",
            )
        ]
```

---

# 8. Academic Year

```text
2025-2026
2026-2027
```

```python
class AcademicYear(BaseModel):

    university = models.ForeignKey(
        University,
        on_delete=models.CASCADE,
        related_name="academic_years",
    )

    name = models.CharField(
        max_length=20,
    )

    start_date = models.DateField()

    end_date = models.DateField()

    is_current = models.BooleanField(
        default=False,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["university", "name"],
                name="unique_university_academic_year",
            )
        ]
```

---

# 9. Semester

```python
class Semester(BaseModel):

    SEMESTER_TYPES = [
        ("spring", "Spring"),
        ("summer", "Summer"),
        ("fall", "Fall"),
        ("winter", "Winter"),
    ]

    academic_year = models.ForeignKey(
        AcademicYear,
        on_delete=models.CASCADE,
        related_name="semesters",
    )

    name = models.CharField(
        max_length=50,
    )

    semester_type = models.CharField(
        max_length=20,
        choices=SEMESTER_TYPES,
    )

    start_date = models.DateField()

    end_date = models.DateField()

    is_current = models.BooleanField(
        default=False,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "academic_year",
                    "semester_type",
                ],
                name="unique_academic_year_semester",
            )
        ]
```

---

# 10. Teacher

```python
class TeacherProfile(BaseModel):

    DESIGNATIONS = [
        ("lecturer", "Lecturer"),
        ("assistant_professor", "Assistant Professor"),
        ("associate_professor", "Associate Professor"),
        ("professor", "Professor"),
        ("visiting", "Visiting Faculty"),
    ]

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="teacher_profile",
    )

    department = models.ForeignKey(
        Department,
        on_delete=models.PROTECT,
        related_name="teachers",
    )

    employee_id = models.CharField(
        max_length=100,
        unique=True,
    )

    designation = models.CharField(
        max_length=40,
        choices=DESIGNATIONS,
    )

    qualification = models.CharField(
        max_length=300,
        blank=True,
    )

    specialization = models.CharField(
        max_length=300,
        blank=True,
    )

    joining_date = models.DateField()

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["department", "designation"]
            ),
            models.Index(
                fields=["department", "is_active"]
            ),
        ]
```

---

# 11. Student

```python
class StudentProfile(BaseModel):

    GENDER_CHOICES = [
        ("male", "Male"),
        ("female", "Female"),
        ("other", "Other"),
    ]

    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.PROTECT,
        related_name="student_profile",
    )

    student_id = models.CharField(
        max_length=100,
        unique=True,
    )

    program = models.ForeignKey(
        AcademicProgram,
        on_delete=models.PROTECT,
        related_name="students",
    )

    campus = models.ForeignKey(
        Campus,
        on_delete=models.PROTECT,
        related_name="students",
    )

    admission_date = models.DateField()

    date_of_birth = models.DateField()

    gender = models.CharField(
        max_length=20,
        choices=GENDER_CHOICES,
    )

    phone = models.CharField(
        max_length=30,
        blank=True,
    )

    guardian_name = models.CharField(
        max_length=150,
        blank=True,
    )

    guardian_phone = models.CharField(
        max_length=30,
        blank=True,
    )

    status = models.CharField(
        max_length=30,
        default="active",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["program", "status"]
            ),
            models.Index(
                fields=["campus", "status"]
            ),
        ]
```

---

# 12. Student Address

```python
class StudentAddress(BaseModel):

    student = models.ForeignKey(
        StudentProfile,
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

    is_current = models.BooleanField(
        default=True,
    )
```

---

# 13. Course

```text
CSE101
CSE201
CSE301
```

```python
class Course(BaseModel):

    department = models.ForeignKey(
        Department,
        on_delete=models.PROTECT,
        related_name="courses",
    )

    code = models.CharField(
        max_length=50,
    )

    title = models.CharField(
        max_length=200,
    )

    description = models.TextField(
        blank=True,
    )

    credit = models.DecimalField(
        max_digits=4,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["department", "code"],
                name="unique_department_course_code",
            )
        ]

        indexes = [
            models.Index(
                fields=["department", "is_active"]
            ),
        ]
```

---

# 14. Course Prerequisite

একটি course-এর prerequisite অন্য course হতে পারে।

```python
class CoursePrerequisite(BaseModel):

    course = models.ForeignKey(
        Course,
        on_delete=models.CASCADE,
        related_name="prerequisites",
    )

    prerequisite_course = models.ForeignKey(
        Course,
        on_delete=models.PROTECT,
        related_name="required_for_courses",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "course",
                    "prerequisite_course",
                ],
                name="unique_course_prerequisite",
            )
        ]
```

Example:

```text
Data Structures
      ↑
Programming Fundamentals
```

---

# 15. Course Offering

কোন semester-এ কোন course চালু হচ্ছে।

```python
class CourseOffering(BaseModel):

    course = models.ForeignKey(
        Course,
        on_delete=models.PROTECT,
        related_name="offerings",
    )

    semester = models.ForeignKey(
        Semester,
        on_delete=models.PROTECT,
        related_name="course_offerings",
    )

    max_students = models.PositiveIntegerField(
        default=40,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "course",
                    "semester",
                ],
                name="unique_course_semester_offering",
            )
        ]
```

---

# 16. Course Section

একই course-এর multiple section হতে পারে।

```text
CSE101-A
CSE101-B
CSE101-C
```

```python
class CourseSection(BaseModel):

    offering = models.ForeignKey(
        CourseOffering,
        on_delete=models.CASCADE,
        related_name="sections",
    )

    section_name = models.CharField(
        max_length=50,
    )

    room = models.CharField(
        max_length=100,
        blank=True,
    )

    capacity = models.PositiveIntegerField(
        default=40,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "offering",
                    "section_name",
                ],
                name="unique_offering_section",
            )
        ]
```

---

# 17. Section Teacher

একটি section-এ একাধিক teacher থাকতে পারে।

```python
class SectionTeacher(BaseModel):

    section = models.ForeignKey(
        CourseSection,
        on_delete=models.CASCADE,
        related_name="teachers",
    )

    teacher = models.ForeignKey(
        TeacherProfile,
        on_delete=models.PROTECT,
        related_name="sections",
    )

    is_primary = models.BooleanField(
        default=False,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "section",
                    "teacher",
                ],
                name="unique_section_teacher",
            )
        ]
```

---

# 18. Class Schedule

```python
class ClassSchedule(BaseModel):

    WEEKDAYS = [
        (0, "Monday"),
        (1, "Tuesday"),
        (2, "Wednesday"),
        (3, "Thursday"),
        (4, "Friday"),
        (5, "Saturday"),
        (6, "Sunday"),
    ]

    section = models.ForeignKey(
        CourseSection,
        on_delete=models.CASCADE,
        related_name="schedules",
    )

    weekday = models.PositiveSmallIntegerField(
        choices=WEEKDAYS,
    )

    start_time = models.TimeField()

    end_time = models.TimeField()

    room = models.CharField(
        max_length=100,
        blank=True,
    )
```

---

# 19. Enrollment

Student course/section register করলে।

```python
class Enrollment(BaseModel):

    STATUS_CHOICES = [
        ("enrolled", "Enrolled"),
        ("dropped", "Dropped"),
        ("completed", "Completed"),
        ("withdrawn", "Withdrawn"),
    ]

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="enrollments",
    )

    section = models.ForeignKey(
        CourseSection,
        on_delete=models.PROTECT,
        related_name="enrollments",
    )

    enrolled_at = models.DateTimeField(
        auto_now_add=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="enrolled",
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["student", "section"],
                name="unique_student_section_enrollment",
            )
        ]

        indexes = [
            models.Index(
                fields=["student", "status"]
            ),
            models.Index(
                fields=["section", "status"]
            ),
        ]
```

---

# 20. Attendance

```python
class Attendance(BaseModel):

    STATUS_CHOICES = [
        ("present", "Present"),
        ("absent", "Absent"),
        ("late", "Late"),
        ("excused", "Excused"),
    ]

    enrollment = models.ForeignKey(
        Enrollment,
        on_delete=models.CASCADE,
        related_name="attendance_records",
    )

    date = models.DateField()

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
    )

    remarks = models.CharField(
        max_length=200,
        blank=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["enrollment", "date"],
                name="unique_enrollment_attendance_date",
            )
        ]

        indexes = [
            models.Index(
                fields=["enrollment", "date"]
            ),
        ]
```

---

# 21. Exam

```python
class Exam(BaseModel):

    EXAM_TYPES = [
        ("quiz", "Quiz"),
        ("midterm", "Midterm"),
        ("final", "Final"),
        ("assignment", "Assignment"),
        ("lab", "Lab"),
    ]

    section = models.ForeignKey(
        CourseSection,
        on_delete=models.PROTECT,
        related_name="exams",
    )

    name = models.CharField(
        max_length=150,
    )

    exam_type = models.CharField(
        max_length=30,
        choices=EXAM_TYPES,
    )

    exam_date = models.DateField()

    total_marks = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["section", "exam_date"]
            ),
        ]
```

---

# 22. Exam Result

```python
class ExamResult(BaseModel):

    exam = models.ForeignKey(
        Exam,
        on_delete=models.CASCADE,
        related_name="results",
    )

    enrollment = models.ForeignKey(
        Enrollment,
        on_delete=models.PROTECT,
        related_name="exam_results",
    )

    marks = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    grade = models.CharField(
        max_length=5,
        blank=True,
    )

    grade_point = models.DecimalField(
        max_digits=4,
        decimal_places=2,
        null=True,
        blank=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["exam", "enrollment"],
                name="unique_exam_enrollment_result",
            )
        ]
```

---

# 23. Final Course Result

Semester শেষে course-এর final grade।

```python
class CourseResult(BaseModel):

    enrollment = models.OneToOneField(
        Enrollment,
        on_delete=models.PROTECT,
        related_name="course_result",
    )

    total_marks = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    grade = models.CharField(
        max_length=5,
    )

    grade_point = models.DecimalField(
        max_digits=4,
        decimal_places=2,
    )

    passed = models.BooleanField(
        default=False,
    )
```

---

# 24. Student Semester Result

```python
class SemesterResult(BaseModel):

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="semester_results",
    )

    semester = models.ForeignKey(
        Semester,
        on_delete=models.PROTECT,
        related_name="student_results",
    )

    semester_gpa = models.DecimalField(
        max_digits=4,
        decimal_places=2,
    )

    total_credits = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    earned_credits = models.DecimalField(
        max_digits=6,
        decimal_places=2,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["student", "semester"],
                name="unique_student_semester_result",
            )
        ]
```

---

# 25. Student Academic Summary

CGPA-এর জন্য summary table রাখতে পারো।

```python
class StudentAcademicSummary(BaseModel):

    student = models.OneToOneField(
        StudentProfile,
        on_delete=models.CASCADE,
        related_name="academic_summary",
    )

    total_credits = models.DecimalField(
        max_digits=7,
        decimal_places=2,
        default=0,
    )

    earned_credits = models.DecimalField(
        max_digits=7,
        decimal_places=2,
        default=0,
    )

    cgpa = models.DecimalField(
        max_digits=4,
        decimal_places=2,
        default=0,
    )

    completed_semesters = models.PositiveIntegerField(
        default=0,
    )
```

> এখানে `CGPA` derived data। Production-এ এটি source-of-truth না করে result data থেকে calculate করার architecture ভালো; performance-এর জন্য cached summary রাখা যেতে পারে।

---

# 26. Fee Structure

```python
class FeeStructure(BaseModel):

    program = models.ForeignKey(
        AcademicProgram,
        on_delete=models.PROTECT,
        related_name="fee_structures",
    )

    semester = models.ForeignKey(
        Semester,
        on_delete=models.PROTECT,
        related_name="fee_structures",
    )

    tuition_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    lab_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    library_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    other_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["program", "semester"],
                name="unique_program_semester_fee",
            )
        ]
```

---

# 27. Student Invoice

```python
class StudentInvoice(BaseModel):

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("partial", "Partial"),
        ("paid", "Paid"),
        ("cancelled", "Cancelled"),
        ("refunded", "Refunded"),
    ]

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="invoices",
    )

    semester = models.ForeignKey(
        Semester,
        on_delete=models.PROTECT,
        related_name="student_invoices",
    )

    invoice_number = models.CharField(
        max_length=100,
        unique=True,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    discount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
        default=0,
    )

    total_amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    due_date = models.DateField()

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="pending",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["student", "status"]
            ),
            models.Index(
                fields=["semester", "status"]
            ),
        ]
```

---

# 28. Invoice Item

```python
class StudentInvoiceItem(BaseModel):

    invoice = models.ForeignKey(
        StudentInvoice,
        on_delete=models.CASCADE,
        related_name="items",
    )

    description = models.CharField(
        max_length=200,
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )
```

---

# 29. Payment

```python
class StudentPayment(BaseModel):

    METHOD_CHOICES = [
        ("cash", "Cash"),
        ("card", "Card"),
        ("bank", "Bank"),
        ("mobile_banking", "Mobile Banking"),
    ]

    STATUS_CHOICES = [
        ("pending", "Pending"),
        ("paid", "Paid"),
        ("failed", "Failed"),
        ("refunded", "Refunded"),
    ]

    invoice = models.ForeignKey(
        StudentInvoice,
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

# 30. Scholarship

```python
class Scholarship(BaseModel):

    name = models.CharField(
        max_length=200,
    )

    description = models.TextField(
        blank=True,
    )

    discount_type = models.CharField(
        max_length=20,
        choices=[
            ("percentage", "Percentage"),
            ("fixed", "Fixed"),
        ],
    )

    discount_value = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 31. Student Scholarship

```python
class StudentScholarship(BaseModel):

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="scholarships",
    )

    scholarship = models.ForeignKey(
        Scholarship,
        on_delete=models.PROTECT,
        related_name="students",
    )

    semester = models.ForeignKey(
        Semester,
        on_delete=models.PROTECT,
        related_name="student_scholarships",
    )

    amount = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    approved_at = models.DateTimeField()

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "student",
                    "scholarship",
                    "semester",
                ],
                name="unique_student_scholarship_semester",
            )
        ]
```

---

# 32. Library Book

```python
class LibraryBook(BaseModel):

    isbn = models.CharField(
        max_length=30,
        unique=True,
    )

    title = models.CharField(
        max_length=300,
    )

    author = models.CharField(
        max_length=300,
    )

    publisher = models.CharField(
        max_length=200,
        blank=True,
    )

    category = models.CharField(
        max_length=100,
        blank=True,
    )

    total_copies = models.PositiveIntegerField(
        default=1,
    )

    available_copies = models.PositiveIntegerField(
        default=1,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["title"]
            ),
            models.Index(
                fields=["category"]
            ),
        ]
```

---

# 33. Library Borrow

```python
class LibraryBorrow(BaseModel):

    STATUS_CHOICES = [
        ("borrowed", "Borrowed"),
        ("returned", "Returned"),
        ("overdue", "Overdue"),
        ("lost", "Lost"),
    ]

    book = models.ForeignKey(
        LibraryBook,
        on_delete=models.PROTECT,
        related_name="borrows",
    )

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="borrowed_books",
    )

    borrowed_at = models.DateTimeField()

    due_date = models.DateField()

    returned_at = models.DateTimeField(
        null=True,
        blank=True,
    )

    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default="borrowed",
    )

    class Meta:
        indexes = [
            models.Index(
                fields=["student", "status"]
            ),
            models.Index(
                fields=["book", "status"]
            ),
            models.Index(
                fields=["status", "due_date"]
            ),
        ]
```

---

# 34. Hostel

```python
class Hostel(BaseModel):

    university = models.ForeignKey(
        University,
        on_delete=models.CASCADE,
        related_name="hostels",
    )

    name = models.CharField(
        max_length=150,
    )

    gender = models.CharField(
        max_length=20,
    )

    address = models.TextField()

    is_active = models.BooleanField(
        default=True,
    )
```

---

# 35. Hostel Room

```python
class HostelRoom(BaseModel):

    hostel = models.ForeignKey(
        Hostel,
        on_delete=models.CASCADE,
        related_name="rooms",
    )

    room_number = models.CharField(
        max_length=50,
    )

    capacity = models.PositiveIntegerField()

    monthly_fee = models.DecimalField(
        max_digits=12,
        decimal_places=2,
    )

    occupied_beds = models.PositiveIntegerField(
        default=0,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=["hostel", "room_number"],
                name="unique_hostel_room",
            )
        ]
```

---

# 36. Hostel Allocation

```python
class HostelAllocation(BaseModel):

    student = models.ForeignKey(
        StudentProfile,
        on_delete=models.PROTECT,
        related_name="hostel_allocations",
    )

    room = models.ForeignKey(
        HostelRoom,
        on_delete=models.PROTECT,
        related_name="allocations",
    )

    bed_number = models.CharField(
        max_length=30,
    )

    start_date = models.DateField()

    end_date = models.DateField(
        null=True,
        blank=True,
    )

    is_active = models.BooleanField(
        default=True,
    )

    class Meta:
        constraints = [
            models.UniqueConstraint(
                fields=[
                    "room",
                    "bed_number",
                    "start_date",
                ],
                name="unique_room_bed_start",
            )
        ]
```

---

# 37. Notification

```python
class UniversityNotification(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
        related_name="university_notifications",
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

# 38. Idempotency Record

```python
class UniversityIdempotencyRecord(BaseModel):

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
        related_name="university_idempotency_records",
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

# 39. Audit Log

```python
class UniversityAuditLog(BaseModel):

    user = models.ForeignKey(
        settings.AUTH_USER_MODEL,
        on_delete=models.SET_NULL,
        null=True,
        blank=True,
        related_name="university_audit_logs",
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
                              UNIVERSITY
                                  │
                 ┌────────────────┼─────────────────┐
                 │                │                 │
              CAMPUS            FACULTY           HOSTEL
                 │                │                 │
                 │          DEPARTMENT             ROOM
                 │                │                 │
                 │             PROGRAM          ALLOCATION
                 │                │
                 │          ┌─────┴─────┐
                 │       STUDENT      TEACHER
                 │          │             │
                 │          │          SECTION
                 │          │             │
                 │          └── ENROLLMENT┘
                 │                 │
                 │          ┌──────┼───────────┐
                 │          │      │           │
                 │     ATTENDANCE EXAM       RESULT
                 │                 │
                 │            EXAM RESULT
                 │
                 └────────── ACADEMIC YEAR
                                  │
                               SEMESTER
                                  │
                              COURSE OFFERING
                                  │
                               SECTION
```

---

# 🎓 Academic Flow

```text
University
    ↓
Faculty
    ↓
Department
    ↓
Program
    ↓
Student
```

Course flow:

```text
Department
    ↓
Course
    ↓
Course Offering
    ↓
Semester
    ↓
Section
    ↓
Teacher
    ↓
Student Enrollment
```

Academic result:

```text
Student
   ↓
Enrollment
   ↓
Exam
   ↓
ExamResult
   ↓
CourseResult
   ↓
SemesterResult
   ↓
CGPA
```

---

# 💰 Financial Flow

```text
Student
   ↓
Semester
   ↓
FeeStructure
   ↓
StudentInvoice
   ↓
InvoiceItem
   ↓
StudentPayment
```

Scholarship:

```text
Student
   ↓
StudentScholarship
   ↓
Scholarship
   ↓
Fee/Invoice adjustment
```

---

# 📚 Library Flow

```text
LibraryBook
     ↓
LibraryBorrow
     ↓
Student
```

Example:

```text
Student
   ↓
Borrow Database Systems
   ↓
Due Date
   ↓
Return
```

---

# 🏠 Hostel Flow

```text
University
   ↓
Hostel
   ↓
HostelRoom
   ↓
Bed
   ↓
HostelAllocation
   ↓
Student
```

---

# 🔥 Important University ORM Practice

এই project-এ তোমার Django ORM-এর almost সব advanced topic practice করা যাবে।

```text
1. University → Faculties
2. Faculty → Departments
3. Department → Programs
4. Department → Courses
5. Program → Students
6. Department → Teachers

7. Current Semester
8. Current Academic Year
9. Semester Courses
10. Course Sections
11. Section Teachers
12. Student Enrollments

13. Student Courses
14. Student Teachers
15. Student Attendance
16. Student Exams
17. Student Results

18. GPA
19. CGPA
20. Failed Courses
21. Passed Courses
22. Retake Courses
23. Completed Credits
24. Remaining Credits

25. Course Prerequisites
26. Available Courses
27. Course Capacity
28. Section Capacity
29. Enrollment Count

30. Teacher Course Load
31. Teacher Schedule
32. Student Schedule
33. Classroom Schedule

34. Student Invoice
35. Paid Invoice
36. Unpaid Invoice
37. Partial Payment
38. University Revenue
39. Semester Revenue
40. Scholarship Amount

41. Library Books
42. Borrowed Books
43. Overdue Books
44. Student Borrow History

45. Hostel Rooms
46. Available Beds
47. Occupied Beds
48. Hostel Allocation

49. Count()
50. Sum()
51. Avg()
52. Min()
53. Max()

54. annotate()
55. aggregate()
56. Q()
57. F()
58. Case()
59. When()

60. Exists()
61. Subquery()
62. OuterRef()
63. Window Functions

64. select_related()
65. prefetch_related()
66. Prefetch()

67. transaction.atomic()
68. select_for_update()
69. Race Condition
70. Course Registration
71. Section Capacity
72. Library Stock
73. Hostel Allocation

74. Database Constraints
75. Indexing
76. EXPLAIN
77. Query Optimization
78. Pagination
79. Multi-campus isolation
80. Audit Logging
81. Idempotency
```

---

# ⚠️ সবচেয়ে গুরুত্বপূর্ণ Production Problems

## 1. Course Registration Race Condition

ধরো section capacity:

```text
Capacity = 40
Current students = 39
```

একই সময়ে দুই student register করলে:

```text
Student A → 40
Student B → 41
```

❌ Capacity exceeded.

এখানে:

```python
transaction.atomic()
```

এর সাথে appropriate locking/constraint strategy দরকার।

---

## 2. Duplicate Enrollment

একজন student যেন একই section-এ দুইবার enroll করতে না পারে:

```python
models.UniqueConstraint(
    fields=["student", "section"],
    name="unique_student_section_enrollment",
)
```

---

## 3. Duplicate Attendance

একই student-এর একই course-এ একই date-এ দুই attendance:

```text
Student A
CSE101
2026-09-13
```

দ্বিতীয় record হওয়া উচিত নয়।

তাই:

```python
UniqueConstraint(
    fields=["enrollment", "date"],
)
```

---

## 4. Prerequisite Validation

Student যদি:

```text
CSE201
```

নিতে চায় কিন্তু:

```text
CSE101
```

pass করেনি, registration reject করতে হবে।

এটা সাধারণত **service layer + transaction** দিয়ে enforce করা ভালো।

---

# 🧠 Database Designer হিসেবে বিশেষ গুরুত্বপূর্ণ

এই project-এ কিছু জিনিস intentionally আলাদা table করেছি:

```text
Course
CourseOffering
CourseSection
Enrollment
```

এগুলো এক model করলে database design খারাপ হবে।

কারণ:

```text
Course
=
"Database Systems"

CourseOffering
=
Database Systems → Fall 2026

Section
=
Database Systems → Fall 2026 → Section A

Enrollment
=
Student 101 → Section A
```

এই separation-টা একজন **database designer** হিসেবে তোমার জন্য খুব important।

---

# 📦 Recommended Django Apps

```text
university_management/
│
├── accounts/
│
├── universities/
│
├── campuses/
│
├── faculties/
│
├── departments/
│
├── programs/
│
├── students/
│
├── teachers/
│
├── academics/
│
├── courses/
│
├── enrollments/
│
├── attendance/
│
├── examinations/
│
├── results/
│
├── finance/
│
├── scholarships/
│
├── library/
│
├── hostel/
│
├── notifications/
│
└── audit/
```

## ⭐ Implementation Order

একসাথে 39টা model না বানিয়ে এভাবে করলে সবচেয়ে ভালো হবে:

```text
Phase 1
University
Campus
Faculty
Department
Program

Phase 2
AcademicYear
Semester
Student
Teacher

Phase 3
Course
CoursePrerequisite
CourseOffering
CourseSection
SectionTeacher

Phase 4
ClassSchedule
Enrollment
Attendance

Phase 5
Exam
ExamResult
CourseResult
SemesterResult
AcademicSummary

Phase 6
FeeStructure
StudentInvoice
InvoiceItem
Payment
Scholarship

Phase 7
LibraryBook
LibraryBorrow

Phase 8
Hostel
HostelRoom
HostelAllocation

Phase 9
Notification
Idempotency
AuditLog
```

এটা আগের **Hotel → Property/Rental → Vehicle → Hospital** projectগুলোর পর তোমার ORM/database-design practice-এর জন্য আরেকটি খুব strong project হবে। বিশেষ করে **Course Registration + Enrollment + Attendance + Result + GPA/CGPA + Fee + Payment** অংশে advanced Django ORM এবং database concurrency অনেক ভালোভাবে practice করা যাবে।



