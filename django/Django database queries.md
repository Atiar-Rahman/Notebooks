Got it! Let’s go **A to Z** on Django database queries. I’ll cover **everything from basics to advanced queries** with examples. Assume we have a model like this:

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    age = models.IntegerField()
    grade = models.CharField(max_length=10)
    enrolled = models.BooleanField(default=True)
    gpa = models.FloatField()
```

---

## **A to Z Django Database Queries**

### **A – All records**

```python
students = Student.objects.all()
```

Gets **all rows** in the `Student` table.

---

### **B – Bulk Create**

```python
students = [
    Student(name="Alice", age=20, grade="A", gpa=3.8),
    Student(name="Bob", age=22, grade="B", gpa=3.2),
]
Student.objects.bulk_create(students)
```

Create multiple rows **efficiently**.

---

### **C – Count**

```python
count = Student.objects.count()
```

Returns total number of records.

---

### **D – Delete**

```python
Student.objects.filter(name="Bob").delete()
```

Deletes records that match the filter.

---

### **E – Exclude**

```python
students = Student.objects.exclude(grade="A")
```

Returns records **excluding** the ones that match.

---

### **F – Filter**

```python
students = Student.objects.filter(grade="A", enrolled=True)
```

Returns records that **match conditions**.

---

### **G – Get**

```python
student = Student.objects.get(id=1)
```

Gets **a single record**. Raises `DoesNotExist` if not found.

---

### **H – Hints / Raw SQL**

```python
students = Student.objects.raw('SELECT * FROM myapp_student WHERE age > 20')
```

Execute **raw SQL** queries.

---

### **I – In**

```python
students = Student.objects.filter(age__in=[20, 22, 25])
```

Filter records **matching any value in a list**.

---

### **J – Join (select_related / prefetch_related)**

```python
# For ForeignKey relationships
students = Student.objects.select_related('related_model').all()
```

Optimizes queries to **avoid N+1 problem**.

---

### **K – Keys (values / values_list)**

```python
names = Student.objects.values_list('name', flat=True)
```

Get **only certain fields** instead of full objects.

---

### **L – Limit**

```python
students = Student.objects.all()[:5]
```

Get **first 5 records**.

---

### **M – Max / Min / Avg / Sum**

```python
from django.db.models import Max, Min, Avg, Sum

max_gpa = Student.objects.aggregate(Max('gpa'))
avg_age = Student.objects.aggregate(Avg('age'))
```

Use **aggregate functions**.

---

### **N – Named Queries / annotate**

```python
from django.db.models import Count

grades = Student.objects.values('grade').annotate(total=Count('id'))
```

Count how many students in **each grade**.

---

### **O – Order By**

```python
students = Student.objects.order_by('age')    # ascending
students = Student.objects.order_by('-gpa')   # descending
```

---

### **P – Prefetch Related**

```python
students = Student.objects.prefetch_related('courses').all()
```

Efficiently fetch **ManyToMany relationships**.

---

### **Q – Q Objects (complex queries)**

```python
from django.db.models import Q

students = Student.objects.filter(Q(age__gte=20) & Q(grade='A'))
```

Combine **AND / OR / NOT** queries.

---

### **R – Reverse**

```python
students = Student.objects.all().order_by('-age')
```

Or:

```python
students = Student.objects.all()[::-1]  # reverse queryset in Python
```

---

### **S – Slice**

```python
students = Student.objects.all()[5:10]
```

Get records **by index**.

---

### **T – Transactions**

```python
from django.db import transaction

with transaction.atomic():
    student = Student.objects.create(name="Charlie", age=21, grade="B", gpa=3.5)
    # other related operations
```

Ensure **all-or-nothing** DB operations.

---

### **U – Update**

```python
Student.objects.filter(name="Alice").update(gpa=4.0)
```

Update records **without fetching them individually**.

---

### **V – Values**

```python
students = Student.objects.values('name', 'gpa')
```

Get **dictionary of specific fields**.

---

### **W – Where (field lookups)**

```python
students = Student.objects.filter(age__gt=20)  # greater than 20
students = Student.objects.filter(name__icontains="ali")  # case-insensitive contains
```

Field lookups examples: `__gt`, `__lt`, `__gte`, `__lte`, `__icontains`, `__startswith`, etc.

---

### **X – eXists**

```python
exists = Student.objects.filter(name="Alice").exists()
```

Check if **any record exists**.

---

### **Y – Yield / Iterator**

```python
for student in Student.objects.all().iterator():
    print(student.name)
```

Iterate large querysets **without loading all into memory**.

---

### **Z – Zero / Null Checks**

```python
students = Student.objects.filter(gpa__isnull=False)
students = Student.objects.filter(age=0)
```

Handle **null or zero values**.

---

💡 **Extra Tips:**

- Chain queries:
    

```python
Student.objects.filter(enrolled=True).exclude(grade='C').order_by('-gpa')[:5]
```

- Lazy evaluation: Django only queries the DB **when needed**.
    
- Debug SQL:
    

```python
print(Student.objects.filter(grade="A").query)
```

---

If you want, I can make a **visual “Django Query Cheat Sheet A–Z”** that you can **keep as a reference PDF** for all queries.

Do you want me to do that?