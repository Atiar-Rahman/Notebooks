1. drf project set up
2. debug toolbar add
3. swagger add
4. 
5. user model Customization

ঠিক আছে 👍, তুমি চাইছো **production-ready, solid Django models** যেখানে **validation সব serializer-এ হবে**, **models clean & simple**, কোন extra validation logic models-এ থাকবে না।

তাহলে তোমার `ProductCategory` ও `ProductSubCategory` হবে minimalist, relationally correct, slug auto-generate এবং ready for serializers.

---

# 🔹 Production-ready Models (no validation in model)

```python id="x1s4qz"
import uuid
from django.db import models
from django.utils.text import slugify

class ProductCategory(models.Model):
    category = models.CharField(max_length=100, db_index=True)
    slug = models.SlugField(max_length=120, unique=True, blank=True)
    cat_script = models.TextField(blank=True, null=True)
    category_image = models.ImageField(upload_to="products/title", blank=True, null=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.category)
            slug = base_slug
            counter = 1
            while ProductCategory.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return self.category


class ProductSubCategory(models.Model):
    product_category = models.ForeignKey(
        ProductCategory, 
        on_delete=models.CASCADE, 
        related_name='subcategories'
    )
    subcategory = models.CharField(max_length=100, db_index=True)
    slug = models.SlugField(max_length=120, unique=True, blank=True)
    subc_script = models.TextField(blank=True, null=True)
    subtitle_image = models.ImageField(upload_to="products/subtitle", blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(f"{self.product_category.category}-{self.subcategory}")
            slug = base_slug
            counter = 1
            while ProductSubCategory.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return f"{self.product_category} - {self.subcategory}"
```

---

## 🔹 Key Features

1. **Slug auto-generate** ✅

   * Unique, collision-safe
2. **ForeignKey relation solid** ✅

   * `product_category.subcategories.all()` works
3. **No validation in models** ✅

   * Validation (required, length, format) handled only in serializer
4. **Indexing added** ✅

   * `category` and `subcategory` for faster search/filter

---

## 🔹 Serializer-level validation (example)

```python id="p4qg9u"
from rest_framework import serializers
from .models import ProductCategory, ProductSubCategory

class ProductCategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = ProductCategory
        fields = ['id', 'category', 'slug', 'cat_script', 'category_image']

    def validate_category(self, value):
        if not value:
            raise serializers.ValidationError("Category is required")
        return value


class ProductSubCategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = ProductSubCategory
        fields = ['id', 'product_category', 'subcategory', 'slug', 'subc_script', 'subtitle_image']

    def validate(self, attrs):
        if 'product_category' not in attrs:
            raise serializers.ValidationError("Subcategory must have a parent category")
        if not attrs.get('subcategory'):
            raise serializers.ValidationError("Subcategory name is required")
        return attrs
```

---

💡 **Advantage of this approach**

* Models stay **clean, simple, and fast**
* All validation logic **centralized in serializers**
* Easier to maintain and test
* Ready for **DRF CRUD & nested API**

---

যদি চাও, আমি তোমার জন্য **Category → SubCategory nested API** ( `/categories/1/subcategories/` ) production-ready ভাবে বানিয়ে দিতে পারি।
চাও আমি সেটা দেখাই?


ঠিক আছে, তাহলে তোমার **Product model**-এ multiple images রাখার জন্য **একটি separate ProductImage model** বানানো হবে।

Django এর conventional approach:

* **One-to-many relationship** → 1 product → অনেক image
* Image URL/Path database এ save হবে
* Serializer/DRF layer থেকে easily manage করা যাবে

---

# 🔹 Updated Product Models with Multiple Images

```python id="g8xj3p"
import uuid
from django.db import models
from django.utils.text import slugify

# -----------------------------
# Product Category
# -----------------------------
class ProductCategory(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    category = models.CharField(max_length=100, db_index=True)
    slug = models.SlugField(max_length=120, unique=True, blank=True)
    description = models.TextField(blank=True, null=True)
    category_image = models.ImageField(upload_to="products/category", blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.category)
            slug = base_slug
            counter = 1
            while ProductCategory.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return self.category

# -----------------------------
# Product SubCategory
# -----------------------------
class ProductSubCategory(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    product_category = models.ForeignKey(
        ProductCategory, 
        on_delete=models.CASCADE, 
        related_name='subcategories'
    )
    subcategory = models.CharField(max_length=100, db_index=True)
    slug = models.SlugField(max_length=120, unique=True, blank=True)
    description = models.TextField(blank=True, null=True)
    subcategory_image = models.ImageField(upload_to="products/subcategory", blank=True, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(f"{self.product_category.category}-{self.subcategory}")
            slug = base_slug
            counter = 1
            while ProductSubCategory.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return f"{self.product_category} - {self.subcategory}"

# -----------------------------
# Product Model
# -----------------------------
class Product(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    name = models.CharField(max_length=150, db_index=True)
    slug = models.SlugField(max_length=150, unique=True, blank=True)
    category = models.ForeignKey(ProductCategory, on_delete=models.PROTECT, related_name='products')
    subcategory = models.ForeignKey(ProductSubCategory, on_delete=models.PROTECT, related_name='products')
    description = models.TextField(blank=True, null=True)
    price = models.DecimalField(max_digits=12, decimal_places=2, null=True, blank=True)
    is_active = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.name)
            slug = base_slug
            counter = 1
            while Product.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return self.name

# -----------------------------
# Product Images (Multiple)
# -----------------------------
class ProductImage(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to="products/items")
    is_main = models.BooleanField(default=False)  # main image flag
    uploaded_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return f"{self.product.name} Image"
```

---

## 🔹 Highlights

1. **ProductImage model**

   * 1 Product → Many Images
   * `is_main` → choose featured image

2. **ForeignKey** with `related_name='images'`

   * `product.images.all()` → all images of a product

3. **UUID** for Product & ProductImage

   * Secure & globally unique

4. **Minimal model logic**

   * Slug generation still in Product
   * Validation handled at serializer/API layer

---

💡 Next step (optional, but recommended):

* Serializer with nested images:

```python id="3x4dj0"
class ProductImageSerializer(serializers.ModelSerializer):
    class Meta:
        model = ProductImage
        fields = ['id', 'image', 'is_main']

class ProductSerializer(serializers.ModelSerializer):
    images = ProductImageSerializer(many=True, read_only=True)

    class Meta:
        model = Product
        fields = ['id','name','slug','category','subcategory','description','price','is_active','images']
```

* Allows **nested API for product + images**

---

যদি চাও, আমি তোমার জন্য **full nested DRF API** বানিয়ে দিতে পারি:

* `/products/` → list all products with images
* `/products/<uuid>/` → product detail + images
* `/products/<uuid>/images/` → manage multiple images

চাও আমি সেটা বানাই?
You’re doing really good progress 🔥 — but your current code has **some critical bugs + design issues** that will break in production.

I’ll give you:
👉 ❌ What’s wrong
👉 ✅ Fixed clean version (production-ready)

---

# ❌ **Problems in Your Code**

### 1. 🔴 Slug save() bug (VERY SERIOUS)

```python
while ProductCategory.objects.filter(slug=slug).exists():
    slug= f'{base_slug}-{couter}'
    couter+=1
    self.slug = slug
    super().save(*args,**kwargs)
```

👉 Problem:

* `super().save()` inside loop ❌ (infinite loop risk)
* `self.slug` not set properly outside loop

---

### 2. 🔴 Duplicate Model

```python
class ProductSubCategory(models.Model):
```

👉 You defined it **TWICE** ❌ → Django will crash

---

### 3. 🔴 Wrong UUID default

```python
default=uuid.uuid   ❌
```

👉 Must be:

```python
default=uuid.uuid4
```

---

### 4. 🔴 Category Design Not Scalable

You are using:

* ProductCategory
* ProductSubCategory

👉 This is **not scalable** (real systems don’t do this)

---

### 5. ⚠️ Missing Company (your business requirement)

You said:

> company product dibe ami sell korbo

👉 But Product has **no company relation** ❌

---

# ✅ **FINAL CLEAN VERSION (BEST PRACTICE)**

👉 I fixed everything + optimized for real marketplace

---

## 🧱 **1️⃣ Category (Replace both Category + SubCategory)**

```python
import uuid
from django.db import models
from django.utils.text import slugify

class Category(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    name = models.CharField(max_length=200, db_index=True)
    slug = models.SlugField(max_length=120, unique=True, blank=True)

    parent = models.ForeignKey(
        'self',
        null=True,
        blank=True,
        on_delete=models.CASCADE,
        related_name='children'
    )

    description = models.TextField(blank=True, null=True)
    image = models.ImageField(upload_to='products/category/', blank=True, null=True)

    created_at = models.DateTimeField(auto_now_add=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.name)
            slug = base_slug
            counter = 1
            while Category.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return self.name
```

---

## 🏢 **2️⃣ Company**

```python
class Company(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    name = models.CharField(max_length=255)
    email = models.EmailField(blank=True, null=True)
    website = models.URLField(blank=True, null=True)

    def __str__(self):
        return self.name
```

---

## 📦 **3️⃣ Product**

```python
class Product(models.Model):

    PRODUCT_TYPE = [
        ('software', 'Software'),
        ('physical', 'Physical'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    company = models.ForeignKey(
        Company,
        on_delete=models.CASCADE,
        related_name='products'
    )

    name = models.CharField(max_length=150, db_index=True)
    slug = models.SlugField(max_length=150, unique=True, blank=True)

    category = models.ForeignKey(
        Category,
        on_delete=models.PROTECT,
        related_name='products'
    )

    product_type = models.CharField(max_length=20, choices=PRODUCT_TYPE)

    live_url = models.URLField(blank=True, null=True)
    description = models.TextField(blank=True, null=True)

    is_active = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)

    def save(self, *args, **kwargs):
        if not self.slug:
            base_slug = slugify(self.name)
            slug = base_slug
            counter = 1
            while Product.objects.filter(slug=slug).exists():
                slug = f"{base_slug}-{counter}"
                counter += 1
            self.slug = slug
        super().save(*args, **kwargs)

    def __str__(self):
        return self.name
```

---

## 🧩 **4️⃣ ProductVersion**

```python
class ProductVersion(models.Model):

    LICENSE_TYPES = [
        ('single', 'Single User'),
        ('multi', 'Multi User'),
        ('extended', 'Extended'),
    ]

    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='versions')

    version = models.CharField(max_length=50)

    price = models.DecimalField(max_digits=12, decimal_places=2)
    discount_price = models.DecimalField(max_digits=12, decimal_places=2, null=True, blank=True)

    license_type = models.CharField(max_length=20, choices=LICENSE_TYPES, default='single')

    file = models.FileField(upload_to='products/files/', null=True, blank=True)

    release_date = models.DateField(blank=True, null=True)
    docs_url = models.URLField(blank=True, null=True)

    is_featured = models.BooleanField(default=False)
    is_active = models.BooleanField(default=True)

    class Meta:
        unique_together = ('product', 'version')

    def __str__(self):
        return f"{self.product.name} v{self.version}"
```

---

## 🖼️ **5️⃣ ProductImage**

```python
class ProductImage(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)

    product = models.ForeignKey(
        Product,
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name='images'
    )

    product_version = models.ForeignKey(
        ProductVersion,
        on_delete=models.CASCADE,
        null=True,
        blank=True,
        related_name='images'
    )

    image = models.ImageField(upload_to="products/images/")
    is_main = models.BooleanField(default=False)

    def __str__(self):
        return "Product Image"
```

---

# 🔥 **Final Improvements Summary**

✔ Removed duplicate models
✔ Fixed slug bug
✔ Fixed UUID bug
✔ Replaced category/subcategory with scalable tree
✔ Added Company (VERY IMPORTANT)
✔ Added license + file support
✔ Made it SaaS-ready

---

# 🧠 **Final Advice (Important)**

👉 Your original code = **good beginner level**
👉 This version = **real production architecture**

---

# 🚀 Next Step

Now you should build:

1. **Serializer (DRF)**
2. **Product API**
3. **Add to Cart**
4. **Checkout + Payment**
5. **License generation after payment**

---

If you want, next I can build:
👉 **Full DRF API (step by step like job-ready backend)**

Just say: **“build API”** 🔥



---------------

update model 

তুমি এখন already advanced level এ আছো — তাই আমি তোমাকে **production-grade Django model checklist** দিচ্ছি 🔥  
👉 এটা follow করলে তোমার model **industry standard (Amazon/Envato level)** হবে

---

# 🚀 ✅ MUST HAVE (Every Production Model)

## 1️⃣ Primary Key (ID)

```python
id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)
```

✔ secure  
✔ scalable  
✔ guess করা যায় না

---

## 2️⃣ Basic Fields

```python
name = models.CharField(max_length=200, db_index=True)
```

👉 Always:

- `max_length`
    
- `db_index=True` (searchable হলে)
    

---

## 3️⃣ Slug (🔥 VERY IMPORTANT for public system)

```python
slug = models.SlugField(unique=True, db_index=True)
```

✔ SEO  
✔ clean URL  
✔ frontend routing

---

## 4️⃣ Relationships (ForeignKey)

```python
category = models.ForeignKey(Category, on_delete=models.PROTECT)
```

👉 Rule:

- `CASCADE` → child delete হবে
    
- `PROTECT` → important data protect
    

---

## 5️⃣ Status Field (VERY IMPORTANT)

```python
status = models.CharField(choices=STATUS, default='draft')
```

✔ draft / published / archived control

---

## 6️⃣ Boolean Flags

```python
is_active = models.BooleanField(default=True)
```

👉 optional:

```python
is_featured = models.BooleanField(default=False)
is_deleted = models.BooleanField(default=False)
```

---

## 7️⃣ Timestamps (MUST)

```python
created_at = models.DateTimeField(auto_now_add=True)
updated_at = models.DateTimeField(auto_now=True)
```

✔ audit  
✔ sorting  
✔ analytics

---

## 8️⃣ Indexing (Performance 🔥)

```python
class Meta:
    indexes = [
        models.Index(fields=['slug']),
        models.Index(fields=['status']),
    ]
```

👉 large data হলে must

---

## 9️⃣ Validation (clean method)

```python
def clean(self):
    if self.price < 0:
        raise ValidationError("Price cannot be negative")
```

✔ business logic protection

---

## 🔟 Unique Constraints

```python
class Meta:
    unique_together = ('product', 'version')
```

✔ duplicate prevent

---

# 🔥 ADVANCED MUST (Real Production System)

## 1️⃣ Slug Auto Generate

✔ already করছো (good)

---

## 2️⃣ Soft Delete (IMPORTANT)

```python
is_deleted = models.BooleanField(default=False)
```

✔ data recovery possible

---

## 3️⃣ Audit Fields (Enterprise level)

```python
created_by = models.ForeignKey(User, ...)
updated_by = models.ForeignKey(User, ...)
```

---

## 4️⃣ Aggregated Fields

```python
rating = models.FloatField()
total_sales = models.IntegerField()
```

✔ performance optimization (avoid heavy query)

---

## 5️⃣ File/Image Handling

```python
image = models.ImageField(upload_to='products/')
```

✔ media support

---

## 6️⃣ Ordering

```python
class Meta:
    ordering = ['-created_at']
```

---

## 7️⃣ Constraints (🔥 VERY IMPORTANT)

```python
models.UniqueConstraint(
    fields=['product'],
    condition=models.Q(is_main=True),
    name='unique_main_image'
)
```

---

# 🧠 THINK LIKE SENIOR ENGINEER

Model design করার সময় নিজেকে জিজ্ঞেস করো:

### ❓ Questions

- data delete হলে কি হবে?
    
- duplicate হলে কি হবে?
    
- future scaling কেমন হবে?
    
- query fast হবে?
    

---

# 🏆 FINAL STRUCTURE TEMPLATE

👉 Almost every model এ থাকা উচিত:

```python
id
name / title
slug
foreign keys
status
is_active
created_at
updated_at
```

---

# 🔥 FINAL VERDICT

👉 Minimum production model = **8/10 features above**

👉 Full production (Amazon-level) = **all + advanced**

---

# 🚀 Next Level (If you want)

তুমি already model design master করতে যাচ্ছো 😎  
Next step হওয়া উচিত:

👉 DRF API design  
👉 Query optimization  
👉 System design (multi-vendor)

---

বললেই আমি তোমার এই model দিয়ে  
🔥 full backend architecture বানিয়ে দিবো (real company level)