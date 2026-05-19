
# 🧠 🎯 System Design Overview

👉 Core Modules:

- Auth (User + Role)
    
- Paper Submission
    
- Review System
    
- Conference Management
    
- Payment
    
- Notification
    

---

# 🧱 1. Base Model (Industry Standard)

```python
from django.db import models

class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)

    class Meta:
        abstract = True
```

---

# 👤 2. User & Role System

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('author', 'Author'),
        ('reviewer', 'Reviewer'),
        ('guest', 'Guest'),
    )

    role = models.CharField(max_length=20, choices=ROLE_CHOICES)
    institution = models.CharField(max_length=255, blank=True)
```

---

# 📚 3. Conference Model

```python
class Conference(BaseModel):
    name = models.CharField(max_length=255)
    description = models.TextField()
    start_date = models.DateField()
    end_date = models.DateField()
```

---

# 🧩 4. Track Model

```python
class Track(BaseModel):
    conference = models.ForeignKey(Conference, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)  # AI, Data Science
```

---

# 📅 5. Important Dates

```python
class ImportantDate(BaseModel):
    conference = models.ForeignKey(Conference, on_delete=models.CASCADE)
    name = models.CharField(max_length=100)  # submission deadline
    date = models.DateTimeField()
```

---

# 📄 6. Paper Submission

```python
class Paper(BaseModel):
    STATUS_CHOICES = (
        ('submitted', 'Submitted'),
        ('under_review', 'Under Review'),
        ('accepted', 'Accepted'),
        ('rejected', 'Rejected'),
    )

    author = models.ForeignKey(User, on_delete=models.CASCADE)
    track = models.ForeignKey(Track, on_delete=models.CASCADE)

    title = models.CharField(max_length=255)
    abstract = models.TextField()
    keywords = models.CharField(max_length=255)

    pdf = models.FileField(upload_to='papers/')
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='submitted')
```

---

# 👥 7. Co-Authors (Important!)

```python
class CoAuthor(BaseModel):
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, related_name="co_authors")
    name = models.CharField(max_length=255)
    email = models.EmailField()
    institution = models.CharField(max_length=255)
```

---

# 🔍 8. Reviewer Assignment

```python
class ReviewAssignment(BaseModel):
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE)
    reviewer = models.ForeignKey(User, on_delete=models.CASCADE)
    assigned_at = models.DateTimeField(auto_now_add=True)
```

---

# 📝 9. Review Model

```python
class Review(BaseModel):
    RECOMMENDATION_CHOICES = (
        ('accept', 'Accept'),
        ('reject', 'Reject'),
        ('revision', 'Revision'),
    )

    paper = models.ForeignKey(Paper, on_delete=models.CASCADE)
    reviewer = models.ForeignKey(User, on_delete=models.CASCADE)

    comment = models.TextField()
    plagiarism_score = models.FloatField()
    recommendation = models.CharField(max_length=20, choices=RECOMMENDATION_CHOICES)
```

---

# 📢 10. Notification System

```python
class Notification(BaseModel):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    message = models.TextField()
    is_read = models.BooleanField(default=False)
```

---

# 📅 11. Session / Schedule

```python
class Session(BaseModel):
    conference = models.ForeignKey(Conference, on_delete=models.CASCADE)
    track = models.ForeignKey(Track, on_delete=models.CASCADE)

    title = models.CharField(max_length=255)
    start_time = models.DateTimeField()
    end_time = models.DateTimeField()
```

---

# 💰 12. Payment System

```python
class Payment(BaseModel):
    STATUS_CHOICES = (
        ('pending', 'Pending'),
        ('paid', 'Paid'),
        ('failed', 'Failed'),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE)
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, null=True, blank=True)

    amount = models.DecimalField(max_digits=10, decimal_places=2)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES)
    transaction_id = models.CharField(max_length=255)
```

---

# 📊 13. Dashboard Optimization (IMPORTANT)

👉 Query optimization:

```python
Paper.objects.select_related('author', 'track').prefetch_related('co_authors')
```

---

# 🔐 14. Permission Logic (Idea)

```python
if request.user.role == 'author':
    # only own paper
elif request.user.role == 'reviewer':
    # assigned papers only
elif request.user.role == 'admin':
    # full access
```

---

# 🚀 Database Relationship Diagram (Concept)

```
User
 ├── Paper (author)
 │     ├── CoAuthor
 │     ├── Review
 │     ├── ReviewAssignment
 │
 ├── Payment
 ├── Notification

Conference
 ├── Track
 │     ├── Paper
 │     ├── Session
 ├── ImportantDate
```

---

# 🔥 Production Level Add-ons

👉 তুমি চাইলে add করতে পারো:

- Soft Delete Manager
    
- Audit Log
    
- File versioning (paper revision history)
    
- Email Queue (Celery + Redis)
    
- Plagiarism API integration
    

---

# 🎯 Final Result

এই design দিয়ে তুমি করতে পারবে:

✅ Full conference system  
✅ Scalable (10k+ users)  
✅ Clean role-based architecture  
✅ Easy API build (DRF)

---


ভালো—এখন তোমার এই Conference Paper Management System-টা **clean, scalable Django project structure**-এ সাজাই 👇
(Industry-level + DRF friendly)

---

# 🧱 🎯 Recommended Project Structure

```id="a3xq7r"
conference_system/
│
├── config/                 # main project config
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
├── apps/                   # all apps in one place
│   │
│   ├── users/
│   ├── conference/
│   ├── papers/
│   ├── reviews/
│   ├── payments/
│   ├── notifications/
│   └── dashboard/
│
├── common/                 # shared logic
│   ├── models.py           # BaseModel
│   ├── permissions.py
│   ├── utils.py
│   └── constants.py
│
├── media/
├── static/
│
├── manage.py
└── requirements.txt
```

---

# 📦 App-wise Breakdown

## 👤 1. `users` app

👉 authentication + role system

```id="3paj3i"
users/
├── models.py        # Custom User model
├── serializers.py
├── views.py
├── permissions.py
├── urls.py
```

👉 handles:

* register/login
* role (admin/author/reviewer)

---

## 📅 2. `conference` app

```id="p7x6kz"
conference/
├── models.py        # Conference, Track, ImportantDate, Session
├── serializers.py
├── views.py
├── urls.py
```

👉 handles:

* event create
* tracks
* schedule

---

## 📄 3. `papers` app

```id="pn6b69"
papers/
├── models.py        # Paper, CoAuthor
├── serializers.py
├── views.py
├── filters.py
├── urls.py
```

👉 handles:

* paper submit
* edit
* status tracking

---

## 🔍 4. `reviews` app

```id="4c41z0"
reviews/
├── models.py        # Review, ReviewAssignment
├── serializers.py
├── views.py
├── urls.py
```

👉 handles:

* reviewer assignment
* review submission

---

## 💰 5. `payments` app

```id="k4c9z7"
payments/
├── models.py
├── serializers.py
├── views.py
├── services.py      # payment gateway logic
├── urls.py
```

👉 handles:

* payment
* transaction tracking

---

## 🔔 6. `notifications` app

```id="7qeqjk"
notifications/
├── models.py
├── services.py      # email sending logic
├── signals.py
```

👉 handles:

* email alerts
* in-app notifications

---

## 📊 7. `dashboard` app

```id="h7ffxg"
dashboard/
├── views.py
├── serializers.py
```

👉 handles:

* stats
* analytics

---

# 🧠 Common Folder (VERY IMPORTANT)

```id="d3g6bl"
common/
├── models.py        # BaseModel
├── permissions.py   # IsAdmin, IsAuthor
├── utils.py         # helper functions
├── constants.py     # choices, enums
```

---

# 🔗 URL Structure

## config/urls.py

```python id="cfiknn"
from django.urls import path, include

urlpatterns = [
    path('api/users/', include('apps.users.urls')),
    path('api/conference/', include('apps.conference.urls')),
    path('api/papers/', include('apps.papers.urls')),
    path('api/reviews/', include('apps.reviews.urls')),
    path('api/payments/', include('apps.payments.urls')),
]
```

---

# ⚡ DRF Structure (Inside Each App)

Standard pattern follow করো:

```id="ozj31j"
models.py
serializers.py
views.py
urls.py
```

Optional:

* services.py (business logic)
* selectors.py (query logic)
* filters.py

---

# 🔥 Advanced Structure (Production Level)

```id="a3k9kx"
papers/
├── services/
│   ├── paper_service.py
│   └── upload_service.py
│
├── selectors/
│   └── paper_selector.py
```

👉 benefits:

* clean code
* reusable logic
* testable system

---

# 🧪 Testing Folder (Optional but Recommended)

```id="9m3vzx"
tests/
├── test_users.py
├── test_papers.py
├── test_reviews.py
```

---

# 🚀 Best Practices

✅ apps separate রাখো
✅ business logic → services
✅ DB query → selectors
✅ permissions → separate file
✅ constants reuse করো

---

# 🎯 Final Architecture Flow

```id="g3x0vy"
View → Serializer → Service → Model
```

---

# 💡 Real-world Tip

👉 বড় project এ:

* apps = micro-module
* loosely coupled system
* easy scaling

---

# 👉 চাইলে আমি next এ করে দিতে পারি:

✅ Full DRF ViewSet (all apps)
✅ Role-based permission system
✅ Reviewer assignment algorithm
✅ API testing (Postman step-by-step)

বললেই next step শুরু করি 👍

--------

# All Model

# 🧱 🔥 Updated BaseModel (Important Upgrade)

```python
from django.db import models
import uuid

class BaseModel(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    updated_at = models.DateTimeField(auto_now=True)

    is_active = models.BooleanField(default=True, db_index=True)
    is_deleted = models.BooleanField(default=False, db_index=True)

    class Meta:
        abstract = True
```

👉 কেন?

- UUID → scalable
    
- soft delete ready
    
- indexed timestamps → fast filtering
    

---

# 👤 User Model (Optimized)

```python
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    ROLE_CHOICES = (
        ('admin', 'Admin'),
        ('author', 'Author'),
        ('reviewer', 'Reviewer'),
        ('guest', 'Guest'),
    )

    role = models.CharField(max_length=20, choices=ROLE_CHOICES, db_index=True)
    institution = models.CharField(max_length=255, blank=True)

    email = models.EmailField(unique=True, db_index=True)

    REQUIRED_FIELDS = ['email']
```

---

# 📅 Conference

```python
class Conference(BaseModel):
    name = models.CharField(max_length=255, db_index=True)
    slug = models.SlugField(unique=True)

    description = models.TextField()

    start_date = models.DateField(db_index=True)
    end_date = models.DateField(db_index=True)

    is_published = models.BooleanField(default=False, db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['start_date', 'end_date']),
        ]
```

---

# 🧩 Track

```python
class Track(BaseModel):
    conference = models.ForeignKey(Conference, on_delete=models.CASCADE, db_index=True)
    name = models.CharField(max_length=100)

    class Meta:
        unique_together = ('conference', 'name')
        indexes = [
            models.Index(fields=['conference', 'name']),
        ]
```

---

# 📄 Paper (Core Model - Highly Optimized)

```python
class Paper(BaseModel):
    STATUS_CHOICES = (
        ('submitted', 'Submitted'),
        ('under_review', 'Under Review'),
        ('accepted', 'Accepted'),
        ('rejected', 'Rejected'),
    )

    author = models.ForeignKey(User, on_delete=models.CASCADE, related_name="papers", db_index=True)
    track = models.ForeignKey(Track, on_delete=models.CASCADE, db_index=True)

    title = models.CharField(max_length=255, db_index=True)
    abstract = models.TextField()
    keywords = models.CharField(max_length=255, db_index=True)

    pdf = models.FileField(upload_to='papers/')

    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='submitted', db_index=True)

    submission_date = models.DateTimeField(auto_now_add=True, db_index=True)

    is_final_submission = models.BooleanField(default=False)

    class Meta:
        indexes = [
            models.Index(fields=['status', 'track']),
            models.Index(fields=['author', 'status']),
            models.Index(fields=['submission_date']),
        ]
```

---

# 👥 CoAuthor

```python
class CoAuthor(BaseModel):
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, related_name="co_authors", db_index=True)

    name = models.CharField(max_length=255)
    email = models.EmailField(db_index=True)
    institution = models.CharField(max_length=255)

    class Meta:
        indexes = [
            models.Index(fields=['paper', 'email']),
        ]
```

---

# 🔍 ReviewAssignment

```python
class ReviewAssignment(BaseModel):
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, db_index=True)
    reviewer = models.ForeignKey(User, on_delete=models.CASCADE, db_index=True)

    assigned_at = models.DateTimeField(auto_now_add=True, db_index=True)
    is_completed = models.BooleanField(default=False, db_index=True)

    class Meta:
        unique_together = ('paper', 'reviewer')
        indexes = [
            models.Index(fields=['reviewer', 'is_completed']),
        ]
```

---

# 📝 Review

```python
class Review(BaseModel):
    RECOMMENDATION_CHOICES = (
        ('accept', 'Accept'),
        ('reject', 'Reject'),
        ('revision', 'Revision'),
    )

    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, db_index=True)
    reviewer = models.ForeignKey(User, on_delete=models.CASCADE, db_index=True)

    comment = models.TextField()
    plagiarism_score = models.FloatField(db_index=True)

    recommendation = models.CharField(max_length=20, choices=RECOMMENDATION_CHOICES, db_index=True)

    submitted_at = models.DateTimeField(auto_now_add=True, db_index=True)

    class Meta:
        unique_together = ('paper', 'reviewer')
        indexes = [
            models.Index(fields=['recommendation']),
        ]
```

---

# 📅 Session

```python
class Session(BaseModel):
    conference = models.ForeignKey(Conference, on_delete=models.CASCADE, db_index=True)
    track = models.ForeignKey(Track, on_delete=models.CASCADE, db_index=True)

    title = models.CharField(max_length=255)
    start_time = models.DateTimeField(db_index=True)
    end_time = models.DateTimeField(db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['conference', 'start_time']),
        ]
```

---

# 💰 Payment

```python
class Payment(BaseModel):
    STATUS_CHOICES = (
        ('pending', 'Pending'),
        ('paid', 'Paid'),
        ('failed', 'Failed'),
    )

    user = models.ForeignKey(User, on_delete=models.CASCADE, db_index=True)
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, null=True, blank=True)

    amount = models.DecimalField(max_digits=10, decimal_places=2)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, db_index=True)

    transaction_id = models.CharField(max_length=255, unique=True)

    paid_at = models.DateTimeField(null=True, blank=True, db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['status', 'user']),
        ]
```

---

# 🔔 Notification

```python
class Notification(BaseModel):
    user = models.ForeignKey(User, on_delete=models.CASCADE, db_index=True)

    message = models.TextField()
    is_read = models.BooleanField(default=False, db_index=True)

    sent_at = models.DateTimeField(auto_now_add=True, db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['user', 'is_read']),
        ]
```

---

# 📊 EXTRA (Highly Recommended)

## 🧠 Paper Versioning (VERY IMPORTANT)

```python
class PaperVersion(BaseModel):
    paper = models.ForeignKey(Paper, on_delete=models.CASCADE, db_index=True)

    version_number = models.IntegerField()
    file = models.FileField(upload_to='paper_versions/')

    class Meta:
        unique_together = ('paper', 'version_number')
```

---

# ⚡ Performance Tips (Real-world)

👉 Always use:

```python
Paper.objects.select_related('author', 'track').prefetch_related('co_authors')
```

---

# 🔥 Final Improvements You Got

✅ Proper indexing (fast query)  
✅ Unique constraints (data integrity)  
✅ Soft delete ready  
✅ Scalable UUID PK  
✅ Review workflow optimized  
✅ Payment + notification optimized  
✅ Version control added

---

# 🧠 🎯 Core Idea

👉 Hard delete:

```python
obj.delete()  # DB থেকে permanently delete
```

👉 Soft delete:

```python
obj.is_deleted = True  # hide only
```

---

# ✅ Step 1: BaseModel update

```python
from django.db import models

class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    updated_at = models.DateTimeField(auto_now=True)

    is_active = models.BooleanField(default=True, db_index=True)
    is_deleted = models.BooleanField(default=False, db_index=True)

    class Meta:
        abstract = True
```

---

# 🔥 Step 2: Custom Manager (MOST IMPORTANT)

👉 default query থেকে deleted data hide করতে হবে

```python
class ActiveManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_deleted=False)
```

---

# 🔧 Step 3: Model এ manager apply

```python
class Paper(BaseModel):
    title = models.CharField(max_length=255)

    objects = ActiveManager()      # default → only active
    all_objects = models.Manager() # show all (including deleted)
```

---

# ⚡ Step 4: Custom delete() override

👉 `.delete()` call করলে soft delete হবে

```python
def delete(self, *args, **kwargs):
    self.is_deleted = True
    self.save()
```

👉 optional: restore method

```python
def restore(self):
    self.is_deleted = False
    self.save()
```

---

# 🧱 Final Combined Example

```python
class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True, db_index=True)
    updated_at = models.DateTimeField(auto_now=True)

    is_deleted = models.BooleanField(default=False, db_index=True)

    objects = ActiveManager()
    all_objects = models.Manager()

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):
        self.is_deleted = True
        self.save()

    def hard_delete(self):
        super().delete(*args, **kwargs)

    def restore(self):
        self.is_deleted = False
        self.save()
```

---

# 🚀 Step 5: DRF ViewSet handle

👉 delete API call করলে:

```python
def perform_destroy(self, instance):
    instance.delete()  # soft delete হবে
```

---

# 🔍 Query Example

### ✅ Normal query

```python
Paper.objects.all()
```

👉 only active (not deleted)

---

### 🔎 Include deleted

```python
Paper.all_objects.all()
```

---

### ♻️ Restore data

```python
paper = Paper.all_objects.get(id=1)
paper.restore()
```

---

# ⚠️ Important Real-world Considerations

### 1. Unique fields problem 😬

👉 soft delete করলে duplicate create issue হতে পারে

Solution:

```python
UniqueConstraint(
    fields=['email'],
    condition=models.Q(is_deleted=False),
    name='unique_active_email'
)
```

---

### 2. ForeignKey relation

👉 deleted object still referenced থাকবে  
✔️ এটা normal behaviour

---

### 3. Admin panel support (optional)

```python
class PaperAdmin(admin.ModelAdmin):
    list_filter = ['is_deleted']
```

---

# 🎯 Summary

👉 Soft delete = 4 components:

|Component|Required|
|---|---|
|is_deleted field|✅|
|custom manager|✅|
|delete override|✅|
|restore method|✅|

---

# 🔥 Pro Level Upgrade (Optional)

👉 add this:

- `deleted_at = DateTimeField`
    
- `deleted_by = ForeignKey(User)`
    

---

চাও হলে আমি next step এ:

✅ full soft delete middleware  
✅ audit log system  
✅ admin toggle (show deleted / hide deleted)

complete production-ready system বানিয়ে দিতে পারি 👍-


---
তুমি যে JSON structure দিয়েছো সেটা basically একটা **CMS-driven conference website + submission system**।
👉 তাই model design করতে হবে **2 layer** এ:

1. **Dynamic Content (CMS)** → hero, welcome, aboutEvent, etc.
2. **Core System (Paper, Review, Payment)** → যেগুলো আমরা আগেই করেছি

এখন আমি তোমাকে **final production-ready model design** দিচ্ছি — fully structured + scalable + indexing সহ 👇

---

# 🧱 🔥 1. Conference (Main Root)

```python
class Conference(BaseModel):
    name = models.CharField(max_length=255, db_index=True)
    short_name = models.CharField(max_length=100, db_index=True)  # IICSD-2027
    slug = models.SlugField(unique=True)

    location = models.CharField(max_length=255)
    start_date = models.DateField(db_index=True)
    end_date = models.DateField(db_index=True)

    description = models.TextField(blank=True)

    is_published = models.BooleanField(default=False, db_index=True)

    class Meta:
        indexes = [
            models.Index(fields=['start_date', 'end_date']),
        ]
```

---

# 🎯 2. Hero Section

```python
class HeroSection(BaseModel):
    conference = models.OneToOneField(Conference, on_delete=models.CASCADE)

    eyebrow = models.CharField(max_length=255)
    pretitle = models.CharField(max_length=255)
    title = models.TextField()

    date_line = models.CharField(max_length=255)
    summary = models.TextField()

    cta_primary_label = models.CharField(max_length=100)
    cta_primary_link = models.CharField(max_length=255)

    cta_secondary_label = models.CharField(max_length=100)
    cta_secondary_link = models.CharField(max_length=255)
```

---

# 🧩 3. Hero Info Cards

```python
class HeroInfoCard(BaseModel):
    hero = models.ForeignKey(HeroSection, on_delete=models.CASCADE, related_name="info_cards")

    label = models.CharField(max_length=100)
    text = models.TextField()

    order = models.IntegerField(default=0)

    class Meta:
        ordering = ['order']
```

---

# 📘 4. Welcome Section

```python
class WelcomeSection(BaseModel):
    conference = models.OneToOneField(Conference, on_delete=models.CASCADE)

    heading = models.CharField(max_length=255)
    conference_name = models.TextField()

    theme_title = models.CharField(max_length=255)
    theme_intro = models.TextField()

    scope_title = models.CharField(max_length=255)
    abstract_note_title = models.CharField(max_length=255)
    abstract_note = models.TextField()
```

---

# 📌 Theme Highlights

```python
class ThemeHighlight(BaseModel):
    welcome = models.ForeignKey(WelcomeSection, on_delete=models.CASCADE, related_name="highlights")
    text = models.TextField()
```

---

# 📌 Scope Areas

```python
class ScopeArea(BaseModel):
    welcome = models.ForeignKey(WelcomeSection, on_delete=models.CASCADE, related_name="scopes")
    name = models.CharField(max_length=255, db_index=True)
```

---

# 🎤 5. Keynote Speakers

```python
class KeynoteSpeaker(BaseModel):
    conference = models.ForeignKey(  
		Conference,  
		on_delete=models.CASCADE,  
		related_name='keynote_speakers'  
	)

    name = models.CharField(max_length=255, db_index=True)
    title = models.CharField(max_length=255)
    affiliation = models.TextField()

    image = models.ImageField(upload_to='keynotes/',blank=True,null=True)
    profile_url = models.URLField(blank=True)

    order = models.IntegerField(default=0)

    class Meta:
        ordering = ['order']
```

---

# 🏛 6. Committee

```python
class CommitteeGroup(BaseModel):
    conference = models.ForeignKey(  
		Conference,  
		on_delete=models.CASCADE,  
		related_name='committee_groups'  
	)

    title = models.CharField(max_length=255)
```

```python
class CommitteeMember(BaseModel):
    group = models.ForeignKey(
        CommitteeGroup,
        on_delete=models.CASCADE,
        related_name="members"
    )

    name = models.CharField(max_length=255)
    designation = models.CharField(max_length=255, blank=True)
    affiliation = models.CharField(max_length=255, blank=True)
    description = models.TextField(blank=True)

    image = models.ImageField(upload_to='committee/', blank=True, null=True)

    order = models.IntegerField(default=0)

    class Meta:
        ordering = ['order', 'id']


```

---

# 🗂 7. Archives

```python
class Archive(BaseModel):
    conference = models.ForeignKey(
        Conference,
        on_delete=models.CASCADE,
        related_name='archives'
    )

    year = models.PositiveIntegerField(db_index=True)
    title = models.CharField(max_length=255)

    description = models.TextField(blank=True)
    cover_image = models.ImageField(upload_to='archives/')

    class Meta:
        ordering = ['-year']
```

```python
class ArchiveLink(BaseModel):
    archive = models.ForeignKey(Archive, on_delete=models.CASCADE, related_name="links")

    label = models.CharField(max_length=100, blank='True')
    url = models.URLField()
    
    
    
	class Meta:
	    unique_together = ('archive', 'url')
```

---

# 📘 8. About Event (BIG SECTION)

```python
class AboutEvent(BaseModel):
    conference = models.OneToOneField(
	    Conference,
	    on_delete=models.CASCADE,
	    related_name='about_event'
	)

    hero_badge = models.CharField(max_length=100)
    hero_title = models.CharField(max_length=255, db_index=True)
    hero_summary = models.TextField(null=True,blank=True)
```

---

# 📌 Generic Text List (Reusable)

```python
class TextItem(BaseModel):

    SECTION_CHOICES = (
        ('submission', 'Submission'),
        ('full_paper', 'Full Paper'),
        ('proceedings', 'Proceedings'),
    )

    about = models.ForeignKey(
        AboutEvent,
        on_delete=models.CASCADE,
        related_name="text_items"
    )

    section = models.CharField(
        max_length=100,
        choices=SECTION_CHOICES,
        db_index=True
    )

    text = models.TextField()
```

---

# 📍 Venue Info

```python
class VenueInfo(BaseModel):
    about = models.ForeignKey(AboutEvent, on_delete=models.CASCADE, related_name="venues")

    label = models.CharField(max_length=100)
    value = models.TextField()
    
    class Meta:
        ordering = ['created_at']
        constraints = [
            models.UniqueConstraint(
                fields=['about', 'label'],
                name='unique_venue_label_per_about'
            )
        ]
```

---

# 🏷 Indexing Targets

```python
class IndexingTarget(BaseModel):
    about = models.ForeignKey(AboutEvent, on_delete=models.CASCADE, related_name="indexings")

    label = models.CharField(max_length=255)
    image = models.ImageField(upload_to='indexing/')
    class Meta:
	    constraints = [
	        models.UniqueConstraint(
	            fields=['about', 'label'],
	            name='unique_indexing_label_per_about'
	        )
	    ]
    
```

---

# 🤝 Sponsors

```python
class Sponsor(BaseModel):
    about = models.ForeignKey(AboutEvent, on_delete=models.CASCADE, related_name="sponsors")

    label = models.CharField(max_length=255)
    image = models.ImageField(upload_to='sponsors/',null=True, blank=True)
    class Meta:
	    constraints = [
	        models.UniqueConstraint(
	            fields=['about', 'label'],
	            name='unique_sponsor_per_about'
	        )
	    ]
    
```



---

# 📅 Timeline (IMPORTANT)

```python
class ImportantDate(BaseModel):
    conference = models.ForeignKey(
	    Conference,
	    on_delete=models.CASCADE,
	    related_name='important_dates'
	)

    title = models.CharField(max_length=255)
    date = models.DateField(db_index=True)
    class Meta:
	    ordering = ['-date']
    
```

---

# 💰 Fees

```python
class RegistrationFee(BaseModel):

    CURRENCY_CHOICES = (
        ('USD', 'USD'),
        ('BDT', 'BDT'),
        ('EUR', 'EUR'),
    )

    conference = models.ForeignKey(
        Conference,
        on_delete=models.CASCADE,
        related_name='registration_fees'
    )

    category = models.CharField(max_length=255, db_index=True)
    amount = models.DecimalField(max_digits=10, decimal_places=2)
    currency = models.CharField(max_length=3, choices=CURRENCY_CHOICES)

    class Meta:
        ordering = ['amount']
        constraints = [
            models.UniqueConstraint(
                fields=['conference', 'category'],
                name='unique_fee_category_per_conference'
            )
        ]
```


---

# 📞 Contact

```python
class ContactInfo(BaseModel):
    conference = models.OneToOneField(
	    Conference,
	    on_delete=models.CASCADE,
	    related_name='contact_info'
	)

    name = models.CharField(max_length=255)
    role = models.CharField(max_length=255)
    organization = models.CharField(max_length=255)

    phone = models.CharField(max_length=100, blanl=True)
    cell = models.CharField(max_length=100, blank=True)

    email = models.EmailField(unique=True)
    
```

---

# 📥 Submission Config

```python
class SubmissionConfig(BaseModel):
    conference = models.OneToOneField(
        Conference,
        on_delete=models.CASCADE,
        related_name='submission_config'
    )

    abstract_limit = models.PositiveIntegerField()
    paper_limit = models.PositiveIntegerField()

    REVIEW_CHOICES = (
        ('single_blind', 'Single Blind'),
        ('double_blind', 'Double Blind'),
        ('open', 'Open Review'),
    )
    review_type = models.CharField(max_length=20, choices=REVIEW_CHOICES)

    LANGUAGE_CHOICES = (
        ('en', 'English'),
        ('bn', 'Bengali'),
    )
    language = models.CharField(max_length=10, choices=LANGUAGE_CHOICES)
```

---

# 🧠 Final Architecture Summary

👉 তুমি এখন পেয়েছো:

### ✅ CMS Part

* Hero
* Welcome
* AboutEvent
* Speakers
* Committee
* Sponsors
* Archive

### ✅ System Part

* Paper
* Review
* Payment
* Notification (আগে দেয়া)

---

# 🚀 Why this design is powerful?

✅ Fully dynamic (admin panel দিয়ে change করা যাবে)
✅ scalable (multi conference support)
✅ indexed (fast query)
✅ reusable components (TextItem, etc.)
✅ DRF friendly

---

# 🎯 Next Step

চাও হলে আমি next এ করে দিতে পারি:

✅ Full DRF serializers (nested response like your JSON)
✅ API response exactly same JSON structure
✅ Admin panel customization
✅ Frontend (React) integration

বললেই next step 🚀


-------
ঠিক আছে—এখন তোমার goal হলো:
👉 **DB model → exact ওই JSON structure (nested)** return করা (DRF দিয়ে)

আমি তোমাকে **production-ready nested serializer + API** দেখাচ্ছি 👇

---

# 🧠 🎯 Strategy

👉 2টা approach আছে:

### ❌ Wrong (beginner)

* সব data manually dict বানানো

### ✅ Correct (industry)

* nested serializers + custom mapping

---

# 🧱 1. Serializer Structure Plan

তোমার JSON অনুযায়ী:

```
Conference
 ├── hero
 │     └── infoCards
 ├── welcome
 │     ├── themeHighlights
 │     └── scopeAreas
 ├── keynoteSpeakers
 ├── committeeGroups
 ├── archives
 ├── aboutEvent
 └── submission
```

---

# 🔥 2. Hero Serializers

```python
from rest_framework import serializers
from .models import *

class HeroInfoCardSerializer(serializers.ModelSerializer):
    class Meta:
        model = HeroInfoCard
        fields = ['label', 'text']


class HeroSerializer(serializers.ModelSerializer):
    infoCards = HeroInfoCardSerializer(source='info_cards', many=True)

    class Meta:
        model = HeroSection
        fields = [
            'eyebrow',
            'pretitle',
            'title',
            'date_line',
            'summary',
            'cta_primary_label',
            'cta_primary_link',
            'cta_secondary_label',
            'cta_secondary_link',
            'infoCards'
        ]

    def to_representation(self, instance):
        data = super().to_representation(instance)

        # rename keys to match JSON
        data['dateLine'] = data.pop('date_line')

        data['ctaPrimary'] = {
            "label": data.pop('cta_primary_label'),
            "href": data.pop('cta_primary_link')
        }

        data['ctaSecondary'] = {
            "label": data.pop('cta_secondary_label'),
            "href": data.pop('cta_secondary_link')
        }

        return data
```

---

# 📘 3. Welcome Serializer

```python
class ThemeHighlightSerializer(serializers.ModelSerializer):
    class Meta:
        model = ThemeHighlight
        fields = ['text']


class ScopeAreaSerializer(serializers.ModelSerializer):
    class Meta:
        model = ScopeArea
        fields = ['name']


class WelcomeSerializer(serializers.ModelSerializer):
    themeHighlights = serializers.SerializerMethodField()
    scopeAreas = serializers.SerializerMethodField()

    class Meta:
        model = WelcomeSection
        fields = [
            'heading',
            'conference_name',
            'theme_title',
            'theme_intro',
            'themeHighlights',
            'scope_title',
            'scopeAreas',
            'abstract_note_title',
            'abstract_note'
        ]

    def get_themeHighlights(self, obj):
        return [i.text for i in obj.highlights.all()]

    def get_scopeAreas(self, obj):
        return [i.name for i in obj.scopes.all()]

    def to_representation(self, instance):
        data = super().to_representation(instance)

        # rename keys
        data['conferenceName'] = data.pop('conference_name')
        data['themeTitle'] = data.pop('theme_title')
        data['themeIntro'] = data.pop('theme_intro')
        data['scopeTitle'] = data.pop('scope_title')
        data['abstractNoteTitle'] = data.pop('abstract_note_title')
        data['abstractNote'] = data.pop('abstract_note')

        return data
```

---

# 🎤 4. Keynote Speakers

```python
class KeynoteSerializer(serializers.ModelSerializer):
    imageAlt = serializers.CharField(source='name')
    profileLabel = serializers.CharField(default="Profile")

    class Meta:
        model = KeynoteSpeaker
        fields = [
            'name',
            'title',
            'affiliation',
            'image',
            'imageAlt',
            'profile_url',
            'profileLabel'
        ]

    def to_representation(self, instance):
        data = super().to_representation(instance)
        data['profileUrl'] = data.pop('profile_url')
        return data
```

---

# 🏛 5. Committee

```python
class CommitteeMemberSerializer(serializers.ModelSerializer):
    class Meta:
        model = CommitteeMember
        fields = ['description']


class CommitteeGroupSerializer(serializers.ModelSerializer):
    summary = serializers.SerializerMethodField()

    class Meta:
        model = CommitteeGroup
        fields = ['title', 'summary']

    def get_summary(self, obj):
        return [m.description for m in obj.members.all()]
```

---

# 🗂 6. Archives

```python
class ArchiveLinkSerializer(serializers.ModelSerializer):
    class Meta:
        model = ArchiveLink
        fields = ['label', 'url']


class ArchiveSerializer(serializers.ModelSerializer):
    links = ArchiveLinkSerializer(many=True)

    class Meta:
        model = Archive
        fields = ['year', 'title', 'description', 'cover_image', 'links']

    def to_representation(self, instance):
        data = super().to_representation(instance)
        data['coverImage'] = data.pop('cover_image')
        return data
```

---

# 📘 7. About Event (Simplified)

```python
class AboutEventSerializer(serializers.ModelSerializer):
    class Meta:
        model = AboutEvent
        fields = [
            'hero_badge',
            'hero_title',
            'hero_summary',
        ]

    def to_representation(self, instance):
        data = super().to_representation(instance)

        data['heroBadge'] = data.pop('hero_badge')
        data['heroTitle'] = data.pop('hero_title')
        data['heroSummary'] = data.pop('hero_summary')

        return data
```

---

# 📥 8. Submission

```python
class SubmissionSerializer(serializers.ModelSerializer):
    class Meta:
        model = SubmissionConfig
        fields = [
            'abstract_limit',
            'paper_limit',
            'review_type',
            'language'
        ]

    def to_representation(self, instance):
        data = super().to_representation(instance)

        data['abstractLimit'] = data.pop('abstract_limit')
        data['paperLimit'] = data.pop('paper_limit')
        data['reviewType'] = data.pop('review_type')

        return data
```

---

# 🚀 9. Final API Serializer (MASTER)

```python
class ConferenceDetailSerializer(serializers.ModelSerializer):
    hero = HeroSerializer(source='herosection')
    welcome = WelcomeSerializer(source='welcomesection')

    keynoteSpeakers = KeynoteSerializer(source='keynotespeaker_set', many=True)
    committeeGroups = CommitteeGroupSerializer(source='committeegroup_set', many=True)
    archives = ArchiveSerializer(source='archive_set', many=True)

    aboutEvent = AboutEventSerializer(source='aboutevent')
    submission = SubmissionSerializer(source='submissionconfig')

    class Meta:
        model = Conference
        fields = [
            'hero',
            'welcome',
            'keynoteSpeakers',
            'committeeGroups',
            'archives',
            'aboutEvent',
            'submission'
        ]
```

---

# ⚡ 10. View (API)

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class ConferenceDetailAPIView(APIView):
    def get(self, request, slug):
        conference = Conference.objects.get(slug=slug)

        serializer = ConferenceDetailSerializer(conference)
        return Response(serializer.data)
```

## only viewset

```python 
from rest_framework.viewsets import GenericViewSet
from rest_framework.mixins import ListModelMixin, RetrieveModelMixin

from cms.serializers import ConferenceDetailSerializer
from conferences.models import Conference


class ConferenceViewSet(ListModelMixin, RetrieveModelMixin, GenericViewSet):
    queryset = Conference.objects.all()
    serializer_class = ConferenceDetailSerializer
    lookup_field = 'slug'
```


---

# 🔥 11. Query Optimization (VERY IMPORTANT)

```python
Conference.objects.select_related(
    'herosection',
    'welcomesection',
    'aboutevent',
    'submissionconfig'
).prefetch_related(
    'herosection__info_cards',
    'welcomesection__highlights',
    'welcomesection__scopes',
    'keynotespeaker_set',
    'committeegroup_set__members',
    'archive_set__links'
)
```

---

# 🎯 Final Result

👉 API response হবে EXACTLY তোমার JSON-এর মতো 👇

```json
{
  "hero": { ... },
  "welcome": { ... },
  "keynoteSpeakers": [ ... ],
  "committeeGroups": [ ... ],
  "archives": [ ... ],
  "aboutEvent": { ... },
  "submission": { ... }
}
```

---

# 🚀 Next Level

চাও হলে আমি next এ:

✅ Full AboutEvent nested (timeline, fees, sponsors, indexing)
✅ Admin panel customization
✅ React frontend binding

complete করে দিতে পারি 👍



তোমার projectটা একটা **International Conference Management + Paper Submission System**, তাই app নাম এমন হওয়া উচিত যাতে **scalable, clear, industry-level** মনে হয়।

আমি তোমাকে best naming options দিচ্ছি 👇

---

# 🧠 🎯 Recommended App Name Strategy

👉 Rule:

* feature-based না, domain-based নাম দাও
* future scaling support থাকতে হবে (multi conference possible)

---

# 🏆 🔥 Best App Name Ideas

## 🥇 Core System Name (BEST CHOICE)

### 👉 `conference`

✔ clean
✔ scalable
✔ industry standard

---

## 🥈 Alternative Professional Names

### 👉 `conferences`

(better if multi conference system)

### 👉 `events`

(generic but scalable)

### 👉 `symposium`

(academic tone, very formal)

### 👉 `icms`

👉 *International Conference Management System*

---

## 🥉 Modular App Naming (BEST PRACTICE)

👉 Recommended real-world structure:

```
apps/
├── core/
├── users/
├── conferences/
├── papers/
├── reviews/
├── payments/
├── notifications/
├── cms/
```

---

# 🚀 💡 My Final Recommendation (for your project)

👉 Use this:

```text
conference_system/
│
├── users
├── conferences   ← main app (ALL conference content)
├── papers
├── reviews
├── payments
├── notifications
└── cms           ← optional (hero, welcome, aboutEvent)
```

---

# 🧠 Why this is BEST

✔ `conferences` → core domain
✔ `papers/reviews/payments` → business logic
✔ `cms` → JSON-driven frontend content
✔ clean separation (industry-level)
✔ easy to scale to DUET + multi events

---

# ⚠️ What NOT to use

❌ `myapp`
❌ `project1`
❌ `conference_app_v2`
❌ mixed names like `paper_submission_system_app`

---

# 🎯 Final Verdict

👉 Best choice:

```
conferences (main app)
```

or production-level:

```
cms + conferences + papers + reviews + payments
```

---

# 🚀 If you want next step

আমি তোমাকে দিতে পারি:

✅ full enterprise folder structure (Django + DRF + Celery)
✅ multi-conference architecture (like real event platforms)
✅ admin CMS system design

just বলো 👍
Perfect — এখন তুমি যেটা করেছো সেটা basically **real production-level CMS + Conference Management System design** 👍
আমি তোমাকে এখন বলবো:

👉 কোন model-এর জন্য ViewSet লাগবে
👉 কোনটা nested থাকবে
👉 এবং clean architecture final structure

---

# 🧠 🎯 CORE RULE (VERY IMPORTANT)

## ✔️ ViewSet লাগে শুধু “ROOT / MAIN ENTITIES” এর জন্য

## ❌ Nested / child models এর জন্য আলাদা API দরকার নেই

---

# 🏗️ 📦 FINAL ARCHITECTURE (Your Project)

---

# 🟦 1. MAIN CONFERENCE CONTENT APIs (YES ViewSet)

## 🔥 HeroSection

```python
class HeroViewSet(ModelViewSet):
    queryset = HeroSection.objects.prefetch_related('info_cards')
    serializer_class = HeroSerializer
```

---

## 🔥 WelcomeSection

```python
class WelcomeViewSet(ModelViewSet):
    queryset = WelcomeSection.objects.prefetch_related('highlights', 'scopes')
    serializer_class = WelcomeSerializer
```

---

## 🔥 KeynoteSpeaker

```python
class KeynoteViewSet(ModelViewSet):
    queryset = KeynoteSpeaker.objects.all().order_by('order')
    serializer_class = KeynoteSerializer
```

---

## 🔥 CommitteeGroup (with members inside)

```python
class CommitteeGroupViewSet(ModelViewSet):
    queryset = CommitteeGroup.objects.prefetch_related('members')
    serializer_class = CommitteeGroupSerializer
```

---

## 🔥 Archive

```python
class ArchiveViewSet(ModelViewSet):
    queryset = Archive.objects.prefetch_related('links')
    serializer_class = ArchiveSerializer
```

---

## 🔥 AboutEvent (HEAVY AGGREGATION)

```python
class AboutEventViewSet(ModelViewSet):
    queryset = AboutEvent.objects.select_related(
        'conference',
        'contact_info'
    ).prefetch_related(
        'herohighlights',
        'text_items',
        'venues',
        'indexings',
        'sponsors',
        'conference__important_dates',
        'conference__registration_fees'
    )

    serializer_class = AboutEventSerializer
```

---

## 🔥 SubmissionConfig

```python
class SubmissionConfigViewSet(ModelViewSet):
    queryset = SubmissionConfig.objects.all()
    serializer_class = SubmissionConfigSerializer
```

---

## 🔥 ContactInfo

```python
class ContactViewSet(ModelViewSet):
    queryset = ContactInfo.objects.all()
    serializer_class = ContactSerializer
```

---

# 🟨 2. CHILD / NESTED MODELS (NO ViewSet ❌)

👉 এগুলোর জন্য আলাদা API লাগবে না:

### ❌ HeroInfoCard

→ HeroSection ভিতরে nested

### ❌ ThemeHighlight

→ WelcomeSection ভিতরে nested

### ❌ ScopeArea

→ WelcomeSection ভিতরে nested

### ❌ CommitteeMember (optional direct API)

### ❌ HeroHighlight

→ AboutEvent ভিতরে nested

### ❌ TextItem

→ AboutEvent inside dynamic filtering

### ❌ VenueInfo

→ AboutEvent

### ❌ IndexingTarget

→ AboutEvent

### ❌ Sponsor

→ AboutEvent

### ❌ ImportantDate

→ Conference under AboutEvent aggregation

### ❌ RegistrationFee

→ Conference under AboutEvent aggregation

---

# 🧠 🔥 SIMPLE RULE

## ✔️ Use ViewSet when:

* standalone model
* admin can CRUD directly
* not dependent on another model

---

## ❌ No ViewSet when:

* model is part of another model
* used only for JSON structure
* accessed via ForeignKey only

---

# 🚀 FINAL SYSTEM DESIGN

## 🔹 Admin APIs

```
/hero/
/welcome/
/keynotes/
/committee/
/archives/
/about-event/
/submission-config/
/contact/
```

---

## 🔹 Nested handled internally

```
HeroInfoCard ❌
TextItem ❌
VenueInfo ❌
Sponsor ❌
```

---

## 🔹 Public API (BEST PRACTICE)

👉 optional single endpoint:

```python
class PublicConferenceViewSet(ViewSet):
    def list(self, request):
        ...
```

Output:

```json
{
  "hero": {},
  "welcome": {},
  "aboutEvent": {},
  "committee": {}
}
```

---

# 🏆 FINAL VERDICT

👉 তোমার system:

✔ 8–10টা ViewSet enough
✔ 20+ model হলেও সব ViewSet লাগে না
✔ nested models = serializer handled

---

# 💡 REAL-WORLD INSIGHT

👉 DUET / Conference system এ এই pattern use করা হয়:

* Models = normalized DB
* ViewSets = core entities only
* Serializer = JSON builder layer

---

# 🚀 NEXT STEP (recommended)

আমি তোমাকে দিতে পারি:

✅ full router.py setup
✅ permissions (Admin/Author/Reviewer system)
✅ optimized single API (/public/)
✅ Postman full testing collection

বললেই next level production system বানিয়ে দিব 🚀
