In Django, **model field relationships** define how models are connected in the database. The three main relationship fields are:

## 1. `ForeignKey` (Many-to-One)

A `ForeignKey` creates a many-to-one relationship.

Example: Many books can belong to one author.

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(
        Author,
        on_delete=models.CASCADE,
        related_name='books'
    )
```

Usage:

```python
author = Author.objects.get(id=1)
books = author.books.all()      # Reverse relationship

book = Book.objects.first()
print(book.author.name)         # Forward relationship
```

---

## 2. `OneToOneField` (One-to-One)

A `OneToOneField` ensures each object has exactly one related object.

Example: Each user has one profile.

```python
from django.contrib.auth.models import User

class Profile(models.Model):
    user = models.OneToOneField(
        User,
        on_delete=models.CASCADE
    )
    bio = models.TextField()
```

Usage:

```python
user = User.objects.get(username="john")
profile = user.profile

profile = Profile.objects.first()
print(profile.user.username)
```

---

## 3. `ManyToManyField` (Many-to-Many)

A `ManyToManyField` allows multiple objects to relate to multiple objects.

Example: Students can enroll in many courses, and courses can have many students.

```python
class Course(models.Model):
    name = models.CharField(max_length=100)

class Student(models.Model):
    name = models.CharField(max_length=100)
    courses = models.ManyToManyField(
        Course,
        related_name='students'
    )
```

Usage:

```python
student = Student.objects.get(id=1)
course = Course.objects.get(id=2)

student.courses.add(course)

student.courses.all()
course.students.all()
```

---

## Self-referencing relationships

A model can relate to itself.

```python
class Employee(models.Model):
    name = models.CharField(max_length=100)
    manager = models.ForeignKey(
        "self",
        on_delete=models.SET_NULL,
        null=True,
        blank=True
    )
```

---

## `on_delete` options (for `ForeignKey` and `OneToOneField`)

| Option               | Behavior                                               |
| -------------------- | ------------------------------------------------------ |
| `models.CASCADE`     | Delete related objects automatically.                  |
| `models.PROTECT`     | Prevent deletion if related objects exist.             |
| `models.RESTRICT`    | Restrict deletion while preserving database integrity. |
| `models.SET_NULL`    | Set the field to `NULL` (requires `null=True`).        |
| `models.SET_DEFAULT` | Set the field to its default value.                    |
| `models.SET(value)`  | Set the field to a specified value or callable result. |
| `models.DO_NOTHING`  | Take no action (may cause database integrity errors).  |

---

## Reverse relationships

Without `related_name`:

```python
class Book(models.Model):
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

Access:

```python
author.book_set.all()
```

With `related_name`:

```python
author = models.ForeignKey(
    Author,
    on_delete=models.CASCADE,
    related_name="books"
)
```

Access:

```python
author.books.all()
```

---

## Summary

|Relationship|Django Field|Example|
|---|---|---|
|One-to-One|`OneToOneField`|User ↔ Profile|
|Many-to-One|`ForeignKey`|Author → Books|
|Many-to-Many|`ManyToManyField`|Students ↔ Courses|
|Self Relationship|`ForeignKey("self")`|Employee → Manager|

These relationship fields let you model common database associations while Django's ORM automatically handles the underlying SQL joins and reverse lookups.