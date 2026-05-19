ঠিক আছে — **শুধু Django-তে index করার উদাহরণ** দিচ্ছি 👇

---

## 1️⃣ Single Field Index

```python
class Product(models.Model):
    name = models.CharField(max_length=255, db_index=True)
```

---

## 2️⃣ Unique Index

```python
class Product(models.Model):
    sku = models.CharField(max_length=100, unique=True)
```

---

## 3️⃣ Multiple Field (Composite) Index

```python
class Order(models.Model):
    user_id = models.IntegerField()
    status = models.CharField(max_length=50)

    class Meta:
        indexes = [
            models.Index(fields=['user_id', 'status']),
        ]
```

---

## 4️⃣ Ordering Index (DESC)

```python
class Order(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        indexes = [
            models.Index(fields=['-created_at']),
        ]
```

---

## 5️⃣ ForeignKey Index (Auto)

```python
class Order(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

👉 Django নিজে থেকেই index বানায়

---

## 6️⃣ Partial Index (PostgreSQL)

```python
from django.db.models import Q

class Product(models.Model):
    is_active = models.BooleanField(default=True)

    class Meta:
        indexes = [
            models.Index(fields=['is_active'], condition=Q(is_active=True)),
        ]
```

---

## 7️⃣ Migration

```bash
python manage.py makemigrations
python manage.py migrate
```

---




নিচে একটি **Library Management System (Django)** এর জন্য **proper models + database indexing** দেওয়া হলো — **production-ready structure** 👍

---

## 📚 Core Models (Library Management)

### 1️⃣ Author Model

```python
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=255, db_index=True)
    email = models.EmailField(unique=True)

    def __str__(self):
        return self.name
```

✅ Index:

- `name` → search/filter
    
- `email` → unique index (auto)
    

---

### 2️⃣ Category Model

```python
class Category(models.Model):
    title = models.CharField(max_length=100, unique=True)

    def __str__(self):
        return self.title
```

✅ Index:

- `title` → unique index
    

---

### 3️⃣ Book Model (Most Important)

```python
class Book(models.Model):
    isbn = models.CharField(max_length=20, unique=True)
    title = models.CharField(max_length=255, db_index=True)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    category = models.ForeignKey(Category, on_delete=models.SET_NULL, null=True)
    published_date = models.DateField()
    available_copies = models.PositiveIntegerField(default=0)
    created_at = models.DateTimeField(auto_now_add=True)

    class Meta:
        indexes = [
            models.Index(fields=['title']),
            models.Index(fields=['author', 'category']),
            models.Index(fields=['-created_at']),
        ]

    def __str__(self):
        return self.title
```

✅ Index Explanation:

- `isbn` → unique lookup
    
- `title` → fast search
    
- `author + category` → filter books
    
- `created_at DESC` → latest books
    

---

### 4️⃣ Member Model

```python
class Member(models.Model):
    member_id = models.CharField(max_length=20, unique=True)
    name = models.CharField(max_length=255, db_index=True)
    phone = models.CharField(max_length=15)
    joined_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
```

✅ Index:

- `member_id` → unique
    
- `name` → search
    

---

### 5️⃣ Book Issue / Borrow Model

```python
class BookIssue(models.Model):
    book = models.ForeignKey(Book, on_delete=models.CASCADE)
    member = models.ForeignKey(Member, on_delete=models.CASCADE)
    issue_date = models.DateField(auto_now_add=True)
    return_date = models.DateField(null=True, blank=True)
    is_returned = models.BooleanField(default=False)

    class Meta:
        indexes = [
            models.Index(fields=['book', 'is_returned']),
            models.Index(fields=['member', 'is_returned']),
            models.Index(fields=['-issue_date']),
        ]
```

✅ Index Explanation:

- `book + is_returned` → available books
    
- `member + is_returned` → active borrow list
    
- `issue_date DESC` → recent issues
    

---

## 🔄 Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## ⚡ Common Fast Queries (Index Optimized)

```python
# Available books
Book.objects.filter(available_copies__gt=0)

# Member active borrowed books
BookIssue.objects.filter(member=member, is_returned=False)

# Books by author & category
Book.objects.filter(author=author, category=category)

# Recently added books
Book.objects.order_by('-created_at')[:10]
```

---

## ✅ Indexing Best Practices (Library Project)

✔ Index:

- `isbn`
    
- `member_id`
    
- `ForeignKey`
    
- search fields (`title`, `name`)
    

❌ Avoid:

- indexing `BooleanField` alone
    
- unnecessary indexes
    

---

চাও তো আমি:

- **ER Diagram**
    
- **Admin panel optimization**
    
- **Fine calculation logic**
    
- **API (DRF) version**
    
- **PostgreSQL full-text search**
    

বললেই হবে 😊