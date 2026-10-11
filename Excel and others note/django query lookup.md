অবশ্যই। Django ORM-এর **field lookups** অনেকগুলো আছে। নিচে সবচেয়ে গুরুত্বপূর্ণগুলো category অনুযায়ী দিলাম। এগুলো `filter()`, `exclude()`, `get()` ইত্যাদিতে ব্যবহার করতে পারো।

ধরি আমাদের model:

```python
class Entry(models.Model):
    headline = models.CharField(max_length=200)
    pub_date = models.DateTimeField()
    rating = models.IntegerField()
    author = models.CharField(max_length=100)
```

## 1. Exact matching

```python
Entry.objects.filter(headline__exact="Django")
```

মানে:

```text
headline == "Django"
```

`exact` না লিখলেও চলে:

```python
Entry.objects.filter(headline="Django")
```

---

## 2. Text search

### `contains`

```python
Entry.objects.filter(headline__contains="Django")
```

`headline`-এর মধ্যে `"Django"` আছে কিনা।

### `icontains`

```python
Entry.objects.filter(headline__icontains="django")
```

Case-insensitive search।

অর্থাৎ `Django`, `django`, `DJANGO`—সব match করতে পারে।

### `startswith`

```python
Entry.objects.filter(headline__startswith="Django")
```

Django দিয়ে শুরু হয়।

### `istartswith`

```python
Entry.objects.filter(headline__istartswith="django")
```

Case-insensitive।

### `endswith`

```python
Entry.objects.filter(headline__endswith="Tutorial")
```

Tutorial দিয়ে শেষ হয়।

### `iendswith`

```python
Entry.objects.filter(headline__iendswith="tutorial")
```

Case-insensitive।

---

# 3. Comparison lookups

এগুলো খুব গুরুত্বপূর্ণ।

### `gt` — Greater Than

```python
Entry.objects.filter(rating__gt=5)
```

মানে:

```text
rating > 5
```

### `gte` — Greater Than or Equal

```python
Entry.objects.filter(rating__gte=5)
```

মানে:

```text
rating >= 5
```

### `lt` — Less Than

```python
Entry.objects.filter(rating__lt=5)
```

মানে:

```text
rating < 5
```

### `lte` — Less Than or Equal

```python
Entry.objects.filter(rating__lte=5)
```

মানে:

```text
rating <= 5
```

মনে রাখো:

```text
gt   → >
gte  → >=
lt   → <
lte  → <=
```

---

# 4. `in`

একাধিক value-এর মধ্যে খুঁজতে:

```python
Entry.objects.filter(rating__in=[1, 3, 5])
```

মানে:

```text
rating = 1 OR rating = 3 OR rating = 5
```

আর:

```python
Entry.objects.filter(author__in=["Rahim", "Karim"])
```

মানে author Rahim অথবা Karim।

---

# 5. `range`

একটা range-এর মধ্যে:

```python
Entry.objects.filter(rating__range=(1, 5))
```

মানে:

```text
1 <= rating <= 5
```

Date-এর ক্ষেত্রেও ব্যবহার করা যায়:

```python
Entry.objects.filter(
    pub_date__range=("2026-01-01", "2026-12-31")
)
```

---

# 6. `isnull`

Field `NULL` কিনা:

```python
Entry.objects.filter(author__isnull=True)
```

মানে author-এর value `NULL`।

আর:

```python
Entry.objects.filter(author__isnull=False)
```

মানে NULL নয়।

---

# 7. Date/Time lookups

এগুলো তোমার আগের `pub_date__year`-এর মতো।

### `year`

```python
Entry.objects.filter(pub_date__year=2026)
```

২০২৬ সালের entry।

### `month`

```python
Entry.objects.filter(pub_date__month=9)
```

September মাসের entry।

### `day`

```python
Entry.objects.filter(pub_date__day=20)
```

মাসের ২০ তারিখ।

### `week`

```python
Entry.objects.filter(pub_date__week=38)
```

বছরের নির্দিষ্ট week।

### `week_day`

```python
Entry.objects.filter(pub_date__week_day=1)
```

Week-এর নির্দিষ্ট day।

### `quarter`

```python
Entry.objects.filter(pub_date__quarter=3)
```

Third quarter।

### `hour`

```python
Entry.objects.filter(pub_date__hour=10)
```

সকাল ১০টার hour।

### `minute`

```python
Entry.objects.filter(pub_date__minute=30)
```

### `second`

```python
Entry.objects.filter(pub_date__second=45)
```

---

# 8. Date-এর comparison

এগুলোও খুব useful:

```python
Entry.objects.filter(pub_date__gt="2026-01-01")
```

মানে:

```text
pub_date > 2026-01-01
```

```python
Entry.objects.filter(pub_date__gte="2026-01-01")
```

```python
Entry.objects.filter(pub_date__lt="2026-12-31")
```

```python
Entry.objects.filter(pub_date__lte="2026-12-31")
```

---

# 9. Related model-এর সাথে lookup

এখানেই `__` আরও interesting হয়ে যায়।

ধরি:

```python
class Blog(models.Model):
    name = models.CharField(max_length=100)

class Entry(models.Model):
    blog = models.ForeignKey(Blog, on_delete=models.CASCADE)
    headline = models.CharField(max_length=200)
```

এখন:

```python
Entry.objects.filter(blog__name="Django Blog")
```

এখানে:

```text
blog → related field
__   → related field-এর ভিতরে যাও
name → Blog-এর field
```

আরও গভীরে যাওয়া যায়:

```python
Entry.objects.filter(blog__owner__name="Rahim")
```

মানে:

```text
Entry
  ↓
blog
  ↓
owner
  ↓
name
```

---

# 10. Related field + lookup একসাথে

এটা খুব গুরুত্বপূর্ণ pattern:

```python
Entry.objects.filter(blog__name__icontains="django")
```

এখানে:

```text
blog       → related field
name       → Blog-এর field
icontains  → lookup
```

অর্থাৎ:

> Blog-এর name-এর মধ্যে "django" আছে কিনা।

আর:

```python
Entry.objects.filter(blog__id__gt=10)
```

মানে:

> Related Blog-এর id 10-এর চেয়ে বড় কিনা।

---

# 11. `regex`

Regular expression দিয়ে search:

```python
Entry.objects.filter(headline__regex=r"^Django")
```

মানে headline `Django` দিয়ে শুরু হচ্ছে কিনা।

Case-insensitive:

```python
Entry.objects.filter(headline__iregex=r"django")
```

এগুলো সাধারণ text search-এর চেয়ে advanced।

---

# 12. `search`

কিছু database/backend-এর ক্ষেত্রে:

```python
Entry.objects.filter(headline__search="Django")
```

Full-text search-এর জন্য ব্যবহার হয়।

এটা database/backend-dependent, তাই সব database-এ একইভাবে available নয়।

---

# সবচেয়ে গুরুত্বপূর্ণ cheat sheet

```text
exact       → exact match
contains    → text-এর মধ্যে আছে
icontains   → case-insensitive contains

startswith  → শুরু হয়
istartswith → case-insensitive শুরু
endswith    → শেষ হয়
iendswith   → case-insensitive শেষ

gt          → >
gte         → >=
lt          → <
lte         → <=

in          → list-এর মধ্যে আছে
range       → range-এর মধ্যে
isnull      → NULL কিনা

year        → year
month       → month
day         → day
week        → week
week_day    → weekday
quarter     → quarter
hour        → hour
minute      → minute
second      → second

regex       → regular expression
iregex      → case-insensitive regex
search      → full-text search (backend dependent)
```

### একটা জিনিস খুব ভালোভাবে বুঝে রাখো

`lookup` আর `field` এক জিনিস না।

```python
Entry.objects.filter(pub_date__year=2026)
```

এখানে:

```text
pub_date  = FIELD
year      = LOOKUP
2026      = VALUE
```

আর:

```python
Entry.objects.filter(headline__icontains="django")
```

এখানে:

```text
headline  = FIELD
icontains = LOOKUP
"django"  = VALUE
```

**আর `__` হলো field এবং lookup (বা related field-এর ধাপ) আলাদা করার syntax।**

চাইলে পরের ধাপে আমি **Django ORM-এর `filter()`, `exclude()`, `get()`, `Q()`, `F()`, `annotate()`, `aggregate()`, `order_by()` সহ প্রায় পুরো QuerySet-এর একটা "Django ORM Complete Cheat Sheet"** exampleসহ সাজিয়ে দিতে পারি।

For Django lookups

- Learn Q object queries
    
- See lookup combinations