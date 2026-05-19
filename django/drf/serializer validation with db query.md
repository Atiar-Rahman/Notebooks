Django REST Framework (DRF) serializer theke data **validate** kora o **query** kora onek flexible. Ami apnar jonno **complete guideline** step by step dekhacchi, jekhane multiple model theke validation, custom validation, queryset validation, and field-level validation cover kora ache.

---

## 1️⃣ Serializer Validation Types

DRF e serializer validation er main tin type ache:

### a) Field-level validation

* Specific field er value check korte use hoy.
* Method name format: `validate_<fieldname>`

```python
from rest_framework import serializers

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price']

    def validate_price(self, value):
        if value < 0:
            raise serializers.ValidationError("Price cannot be negative.")
        return value
```

✅ Ei validation automatically field e apply hoy create/update er somoy.

---

### b) Object-level (serializer-level) validation

* Puro object er combination validate korte use hoy.
* Method: `validate(self, data)`

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'category']

    def validate(self, data):
        if data['category'].name == 'Electronics' and data['price'] > 10000:
            raise serializers.ValidationError("Electronics cannot be priced above 10,000")
        return data
```

---

### c) Cross-model / database validation

* Serializer er create/update e query kore **already exist** ache kina check kora.
* Example: `unique_together` validation manually kora.

```python
class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = ['id', 'product', 'rating', 'comment']

    def validate(self, data):
        product = data['product']
        user = self.context['request'].user  # jodi user field thake
        if Review.objects.filter(product=product, user=user).exists():
            raise serializers.ValidationError("You have already reviewed this product.")
        return data
```

---

## 2️⃣ Using `SerializerMethodField` to validate or compute

* Serializer e extra computed fields add korte use hoy, optionally validation check kora jay.

```python
class ProductSerializer(serializers.ModelSerializer):
    discount_price = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'discount_price']

    def get_discount_price(self, obj):
        if obj.price > 1000:
            return obj.price * 0.9
        return obj.price
```

* Ei field **read_only**, kintu calculated data diye validation o decision nite parben.

---

## 3️⃣ Nested serializer validation

* Nested serializer use korle parent serializer e `validate` method override kora jay.
* Example: `Category → Product → Review`

```python
class ProductNestedSerializer(serializers.ModelSerializer):
    reviews = ReviewSerializer(many=True)

    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'reviews']

    def validate_reviews(self, value):
        for review in value:
            if review['rating'] < 0 or review['rating'] > 5:
                raise serializers.ValidationError("Rating must be between 0 and 5")
        return value

    def create(self, validated_data):
        reviews_data = validated_data.pop('reviews')
        product = Product.objects.create(**validated_data)
        for review_data in reviews_data:
            Review.objects.create(product=product, **review_data)
        return product
```

✅ Ei approach e **nested create/update** er somoy validation smooth hoy.

---

## 4️⃣ Queryset-based validation

* Serializer e context use kore request data or query parameter check kora jay.
* Example: Only allow review create if product belongs to certain category

```python
class ReviewSerializer(serializers.ModelSerializer):
    class Meta:
        model = Review
        fields = ['id', 'product', 'rating', 'comment']

    def validate_product(self, value):
        if value.category.name != 'Electronics':
            raise serializers.ValidationError("Reviews allowed only for Electronics")
        return value
```

* `self.context['request']` er maddhome request user, query params access kora jay.

---

## 5️⃣ Overriding `create` / `update` for extra validation

* Sometimes `validate` sufficient hoy na, ekhon `create`/`update` override korte hoy.

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'category']

    def create(self, validated_data):
        if validated_data['price'] < 10:
            raise serializers.ValidationError("Price too low to create product")
        return super().create(validated_data)
```

---

## 6️⃣ DRF Validators (built-in)

* DRF e `validators` argument use kore direct field validation kora jay.

```python
from rest_framework.validators import UniqueValidator

class ProductSerializer(serializers.ModelSerializer):
    name = serializers.CharField(
        max_length=100,
        validators=[UniqueValidator(queryset=Product.objects.all(), message="Product name must be unique")]
    )
    class Meta:
        model = Product
        fields = ['id', 'name', 'price']
```

---

## 7️⃣ Summary of Validation Levels

| Level                     | Where Applied                         | Example                        |
| ------------------------- | ------------------------------------- | ------------------------------ |
| Field-level               | Single field (`validate_<field>`)     | price < 0                      |
| Object-level              | Whole serializer (`validate`)         | category + price check         |
| Nested serializer         | Parent serializer for children        | reviews rating check           |
| Database/query validation | Query DB in validate or create/update | unique review per user/product |
| Built-in DRF validators   | Field `validators`                    | UniqueValidator                |

---

💡 **Pro Tips:**

1. `self.context` diye request, view, user, kwargs access kora jay.
2. Nested serializer e **read_only=True** na dile parent create/update e validation lage.
3. Always raise `serializers.ValidationError` with meaningful messages.
4. Use `UniqueValidator` for simple unique checks, database query only if complex.
5. Combine multiple validation methods for robust checks.

---

