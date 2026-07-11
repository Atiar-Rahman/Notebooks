হ্যাঁ, বেশিরভাগ ক্ষেত্রে **আগে parent, তারপর child** তৈরি করতে হয়।

কারণ child object-এর `ForeignKey` বা `OneToOneField`-এ parent-এর instance (বা primary key) দরকার হয়।

উদাহরণ:

```python
def create(self, validated_data):
    profile_data = validated_data.pop("profile")

    # 1. Parent create
    user = User.objects.create(**validated_data)

    # 2. Child create
    Profile.objects.create(user=user, **profile_data)

    return user
```

**ক্রম:**

1. `validated_data.pop("profile")`
    
2. Parent object create (`User`)
    
3. Child object create (`Profile`)
    
4. Parent return
    

**ব্যতিক্রম:** যদি parent model-এ child-এর `ForeignKey` থাকে (যা কম দেখা যায়), তাহলে আগে child তৈরি করতে হতে পারে। তবে DRF-এর writable nested serializer-এর সাধারণ এবং সবচেয়ে প্রচলিত pattern হলো **parent → child**।


-----
নিচে একটি **4–5 level writable nested serializer**-এর সম্পূর্ণ উদাহরণ দিলাম। এতে `create()` এবং `update()` দুটোই আছে।

## Models

```python
from django.db import models

class University(models.Model):
    name = models.CharField(max_length=100)


class Department(models.Model):
    university = models.ForeignKey(
        University,
        on_delete=models.CASCADE,
        related_name="departments"
    )
    name = models.CharField(max_length=100)


class Teacher(models.Model):
    department = models.ForeignKey(
        Department,
        on_delete=models.CASCADE,
        related_name="teachers"
    )
    name = models.CharField(max_length=100)


class Student(models.Model):
    teacher = models.ForeignKey(
        Teacher,
        on_delete=models.CASCADE,
        related_name="students"
    )
    name = models.CharField(max_length=100)


class Subject(models.Model):
    student = models.ForeignKey(
        Student,
        on_delete=models.CASCADE,
        related_name="subjects"
    )
    title = models.CharField(max_length=100)
```

---

## Serializers

```python
from rest_framework import serializers
from .models import *

class SubjectSerializer(serializers.ModelSerializer):
    class Meta:
        model = Subject
        fields = ["id", "title"]


class StudentSerializer(serializers.ModelSerializer):
    subjects = SubjectSerializer(many=True)

    class Meta:
        model = Student
        fields = ["id", "name", "subjects"]


class TeacherSerializer(serializers.ModelSerializer):
    students = StudentSerializer(many=True)

    class Meta:
        model = Teacher
        fields = ["id", "name", "students"]


class DepartmentSerializer(serializers.ModelSerializer):
    teachers = TeacherSerializer(many=True)

    class Meta:
        model = Department
        fields = ["id", "name", "teachers"]


class UniversitySerializer(serializers.ModelSerializer):
    departments = DepartmentSerializer(many=True)

    class Meta:
        model = University
        fields = ["id", "name", "departments"]
```

---

# CREATE

```python
class UniversitySerializer(serializers.ModelSerializer):
    departments = DepartmentSerializer(many=True)

    class Meta:
        model = University
        fields = ["id", "name", "departments"]

    def create(self, validated_data):

        departments_data = validated_data.pop("departments")

        # Level 1
        university = University.objects.create(**validated_data)

        # Level 2
        for department_data in departments_data:

            teachers_data = department_data.pop("teachers")

            department = Department.objects.create(
                university=university,
                **department_data
            )

            # Level 3
            for teacher_data in teachers_data:

                students_data = teacher_data.pop("students")

                teacher = Teacher.objects.create(
                    department=department,
                    **teacher_data
                )

                # Level 4
                for student_data in students_data:

                    subjects_data = student_data.pop("subjects")

                    student = Student.objects.create(
                        teacher=teacher,
                        **student_data
                    )

                    # Level 5
                    for subject_data in subjects_data:

                        Subject.objects.create(
                            student=student,
                            **subject_data
                        )

        return university
```

---

# UPDATE

এখানে সহজভাবে সব পুরোনো nested data delete করে নতুন data insert করা হয়েছে।

```python
class UniversitySerializer(serializers.ModelSerializer):
    departments = DepartmentSerializer(many=True)

    class Meta:
        model = University
        fields = ["id", "name", "departments"]

    def update(self, instance, validated_data):

        departments_data = validated_data.pop("departments")

        instance.name = validated_data.get("name", instance.name)
        instance.save()

        # Delete all nested data
        instance.departments.all().delete()

        # Re-create nested data

        for department_data in departments_data:

            teachers_data = department_data.pop("teachers")

            department = Department.objects.create(
                university=instance,
                **department_data
            )

            for teacher_data in teachers_data:

                students_data = teacher_data.pop("students")

                teacher = Teacher.objects.create(
                    department=department,
                    **teacher_data
                )

                for student_data in students_data:

                    subjects_data = student_data.pop("subjects")

                    student = Student.objects.create(
                        teacher=teacher,
                        **student_data
                    )

                    for subject_data in subjects_data:

                        Subject.objects.create(
                            student=student,
                            **subject_data
                        )

        return instance
```

---

# JSON Input

```json
{
    "name": "Dhaka University",
    "departments": [
        {
            "name": "CSE",
            "teachers": [
                {
                    "name": "Rahim",
                    "students": [
                        {
                            "name": "Karim",
                            "subjects": [
                                {
                                    "title": "Python"
                                },
                                {
                                    "title": "Django"
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
```

---

## Nested Serializer-এর মূল নিয়ম

প্রতিটি level-এ একই ধাপ অনুসরণ করবেন:

1. `pop()` দিয়ে nested data আলাদা করুন।
    
2. Parent object তৈরি বা update করুন।
    
3. Parent instance দিয়ে Child object তৈরি করুন।
    
4. Child-এর ভিতরে আরও nested data থাকলে একই নিয়ম recursiveভাবে অনুসরণ করুন।
    

এটাই DRF-এ writable nested serializer-এর সবচেয়ে প্রচলিত pattern। বড় প্রজেক্টে অনেকেই এই nested creation/update-এর লজিককে আলাদা helper function বা service class-এ ভাগ করে লেখেন, যাতে serializer অনেক বড় হয়ে না যায়।


---------
হ্যাঁ। এটাকে **parallel nested serializer** বা **multiple nested serializers at the same level** বলা যায়।

উদাহরণ:

```
Company
├── Employees
├── Departments
├── Branches
└── Projects
```

এখানে `Employees`, `Departments`, `Branches`, `Projects`—সবগুলো **Company-এর child**, অর্থাৎ একই level-এর nested serializer।

### Models

```python
class Company(models.Model):
    name = models.CharField(max_length=100)

class Employee(models.Model):
    company = models.ForeignKey(Company, related_name="employees", on_delete=models.CASCADE)
    name = models.CharField(max_length=100)

class Department(models.Model):
    company = models.ForeignKey(Company, related_name="departments", on_delete=models.CASCADE)
    name = models.CharField(max_length=100)

class Branch(models.Model):
    company = models.ForeignKey(Company, related_name="branches", on_delete=models.CASCADE)
    city = models.CharField(max_length=100)

class Project(models.Model):
    company = models.ForeignKey(Company, related_name="projects", on_delete=models.CASCADE)
    title = models.CharField(max_length=100)
```

### Serializer

```python
class CompanySerializer(serializers.ModelSerializer):

    employees = EmployeeSerializer(many=True)
    departments = DepartmentSerializer(many=True)
    branches = BranchSerializer(many=True)
    projects = ProjectSerializer(many=True)

    class Meta:
        model = Company
        fields = "__all__"
```

### create()

```python
def create(self, validated_data):

    employees = validated_data.pop("employees")
    departments = validated_data.pop("departments")
    branches = validated_data.pop("branches")
    projects = validated_data.pop("projects")

    # Parent
    company = Company.objects.create(**validated_data)

    # Child 1
    for emp in employees:
        Employee.objects.create(company=company, **emp)

    # Child 2
    for dept in departments:
        Department.objects.create(company=company, **dept)

    # Child 3
    for branch in branches:
        Branch.objects.create(company=company, **branch)

    # Child 4
    for project in projects:
        Project.objects.create(company=company, **project)

    return company
```

### Execution order

```
Company
│
├── Employees
├── Departments
├── Branches
└── Projects
```

অর্থাৎ:

1. `Company` তৈরি হবে।
    
2. তারপর `Employees` তৈরি হবে।
    
3. তারপর `Departments`।
    
4. তারপর `Branches`।
    
5. তারপর `Projects`।
    

এগুলো একে অপরের উপর নির্ভরশীল নয়, শুধু `Company`-এর উপর নির্ভরশীল।

---

আরও জটিল উদাহরণ হতে পারে:

```
School
├── Teachers
│   ├── Subjects
│   └── Awards
├── Students
│   ├── Results
│   └── Guardians
├── Buildings
└── Buses
```

এখানে **Teachers, Students, Buildings, Buses** একই level-এর (parallel nested), আবার **Teachers-এর মধ্যে Subjects ও Awards**, এবং **Students-এর মধ্যে Results ও Guardians** আরও nested। এটিই বড় প্রজেক্টে দেখা যায়।





--------

**DRF-এ nested serializer-এর নির্দিষ্ট কোনো level limit নেই।** তাত্ত্বিকভাবে যত level দরকার তত level nested করা যায়।

উদাহরণ:

```
Level 1
Company
│
├── Level 2
│   Employees
│   Departments
│
├── Level 3
│   Employee
│   ├── Address
│   ├── Salary
│
├── Level 4
│   Salary
│   ├── Bonus
│
├── Level 5
│   Bonus
│   ├── Tax
│
└── Level 6
    Tax
    ├── History
```

এগুলো সবই DRF-এ করা সম্ভব।

### কিন্তু বাস্তবে?

সাধারণত:

* **1–2 level** → খুবই সাধারণ।
* **3 level** → মাঝারি প্রজেক্টে দেখা যায়।
* **4 level** → কম দেখা যায়।
* **5+ level** → খুব বিরল। কোড জটিল হয়ে যায়, তাই অনেক টিম nested serializer-এর বদলে আলাদা API endpoint বা service layer ব্যবহার করে।

### Interview-তে বলতে পারেন

> "Django REST Framework-এ nested serializer-এর fixed level limit নেই। যত level দরকার করা যায়। তবে maintainability, performance এবং readability-এর জন্য সাধারণত ২–৩ level-এর বেশি nested serializer ব্যবহার করা হয় না।"


---------

