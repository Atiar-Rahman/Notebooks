Django admin-এ model register করার দুইটা common way আছে। Professional project-এ সাধারণত `@admin.register()` + custom `ModelAdmin` ব্যবহার করা ভালো।

---

## Method 1: Simple register (ছোট project)

```python
from django.contrib import admin
from blogs.models import Category, Tag, Blog, BlogImage


admin.site.register(Category)
admin.site.register(Tag)
admin.site.register(Blog)
admin.site.register(BlogImage)
```

এটা কাজ করবে, কিন্তু customization করা যায় না।

---

# Method 2: Recommended (Professional)

```python
from django.contrib import admin
from blogs.models import Category, Tag, Blog, BlogImage


@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = [
        "id",
        "name",
        "slug",
        "created_at",
        "updated_at",
    ]

    search_fields = [
        "name",
    ]

    ordering = [
        "-created_at"
    ]


@admin.register(Tag)
class TagAdmin(admin.ModelAdmin):
    list_display = [
        "id",
        "name",
        "slug",
        "created_at",
    ]

    search_fields = [
        "name",
    ]


@admin.register(Blog)
class BlogAdmin(admin.ModelAdmin):

    list_display = [
        "id",
        "title",
        "user",
        "category",
        "status",
        "is_featured",
        "created_at",
    ]

    list_filter = [
        "status",
        "is_featured",
        "category",
    ]

    search_fields = [
        "title",
        "description",
    ]

    prepopulated_fields = {
        "slug": ("title",)
    }


@admin.register(BlogImage)
class BlogImageAdmin(admin.ModelAdmin):

    list_display = [
        "id",
        "blog",
        "created_at",
    ]
```

---

## Common Admin Options

### `list_display`

Admin list page-এ কোন field দেখাবে।

Example:

```python
list_display = [
    "title",
    "status",
]
```

Result:

```
Title          Status
----------------------
Django Blog    Published
Python         Draft
```

---

### `search_fields`

Search box enable করে।

```python
search_fields = [
    "title",
    "description"
]
```

---

### `list_filter`

Right side filter দেয়।

```python
list_filter = [
    "status",
    "category"
]
```

---

### `ordering`

Default sorting:

```python
ordering = [
    "-created_at"
]
```

Latest আগে দেখাবে।

---

### `readonly_fields`

কোন field edit করা যাবে না।

```python
readonly_fields = [
    "created_at",
    "updated_at"
]
```

---

### `prepopulated_fields`

Slug auto generate:

```python
prepopulated_fields = {
    "slug": ("title",)
}
```

---

## আপনার Blog project-এর জন্য আরও useful

আপনার যেহেতু Soft Delete আছে:

```python
class BlogAdmin(admin.ModelAdmin):

    list_display = [
        "title",
        "status",
        "is_deleted",
        "created_at",
    ]

    list_filter = [
        "status",
        "is_deleted",
    ]
```

তাহলে admin থেকে deleted object সহজে track করতে পারবেন।

---

## Recommended structure

বড় project হলে:

```
blogs/
│
├── admin.py
├── models.py
├── serializers.py
├── views.py
```

`admin.py`:

```
CategoryAdmin
TagAdmin
BlogAdmin
BlogImageAdmin
```

প্রতিটি model-এর জন্য আলাদা `ModelAdmin` রাখলে maintenance সহজ হয়।
