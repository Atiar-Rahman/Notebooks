# 🔥 🔹 `context` কী?

👉 `context` হলো একটা **extra data dictionary**, যেটা তুমি serializer-এ পাঠাও
👉 এবং serializer-এর ভিতরে `self.context` দিয়ে access করো

---

# 🔹 তুমি যা লিখছো:

```python
context = {
    'cart_id': cart.id,
    'user': request.user
}
```

👉 মানে:

* তুমি serializer-এ extra info পাঠাচ্ছো
* যা request body-তে নাই
* কিন্তু logic-এ দরকার

---

# 🔥 🔹 কোথায় use করো?

## Serializer call করার সময়:

```python
serializer = CartItemSerializer(
    data=request.data,
    context={'cart_id': cart.id, 'user': request.user}
)
```

---

# 🔹 Serializer-এ access করো:

```python
self.context['cart_id']
self.context['user']
```

---

# 🔥 🔹 Real Example (Cart System 🛒)

## Model

```python
class CartItem(models.Model):
    cart_id = models.IntegerField()
    product = models.CharField(max_length=100)
    quantity = models.IntegerField()
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```

---

## Serializer

```python
class CartItemSerializer(serializers.ModelSerializer):

    class Meta:
        model = CartItem
        fields = ['id', 'product', 'quantity']

    def create(self, validated_data):
        cart_id = self.context['cart_id']
        user = self.context['user']

        return CartItem.objects.create(
            cart_id=cart_id,
            user=user,
            **validated_data
        )
```

---

## View

```python
def post(self, request, cart_id):
    serializer = CartItemSerializer(
        data=request.data,
        context={
            'cart_id': cart_id,
            'user': request.user
        }
    )

    serializer.is_valid(raise_exception=True)
    serializer.save()
```

---

## Request (User পাঠায়)

```json
{
    "product": "Laptop",
    "quantity": 2
}
```

👉 User `cart_id` বা `user` পাঠায় নাই
👉 কিন্তু backend নিজে add করলো

---

## DB-তে save হবে:

```json
{
    "product": "Laptop",
    "quantity": 2,
    "cart_id": 5,
    "user": 1
}
```

---

# 🔥 🔹 কেন `context` use করবো?

### ✅ 1. Hidden data pass করতে

* user
* cart_id
* request info

---

### ✅ 2. Security

👉 user যেন নিজে user_id না পাঠাতে পারে

---

### ✅ 3. Clean API design

👉 client কম data পাঠাবে

---

# 🔥 🔹 Common use cases

✔ `request.user` pass করা
✔ URL parameter pass করা (`cart_id`, `camera_id`)
✔ request object use করা

---

# 🔹 Request access (Very Important 🔥)

```python
request = self.context['request']
user = request.user
```

👉 DRF auto `request` context-এ দেয় (ViewSet-এ)

---

# 🔥 🔹 SerializerMethodField + context

```python
status = serializers.SerializerMethodField()

def get_status(self, obj):
    user = self.context['user']
    return f"{obj.name} - {user.username}"
```

---

# ⚠️ Common Mistake

❌ context না দিয়ে access করা:

```python
self.context['cart_id']  # KeyError হবে
```

✔ Safe way:

```python
self.context.get('cart_id')
```

---

# 🔥 🔹 তোমার Project Example (CCTV 🚨)

```python
serializer = DetectionSerializer(
    data=request.data,
    context={
        'camera_id': camera.id,
        'user': request.user
    }
)
```

---

## Serializer

```python
def create(self, validated_data):
    return Detection.objects.create(
        camera_id=self.context['camera_id'],
        user=self.context['user'],
        **validated_data
    )
```

---
# 🔥 Golden Rule

👉 **"যা user পাঠাবে না, কিন্তু backend-এ দরকার → context use করো"**

---
# `ModelViewSet` use করলে `context` কিভাবে পাঠাবে এটা খুব important।

👉 Good news:
DRF already automatically `context` পাঠায় (like `request`, `view`, `format`)
👉 কিন্তু custom context (যেমন `cart_id`, `camera_id`) add করতে হলে override করতে হয়।

---

# 🔥 🔹 Default context (Auto)

`ModelViewSet` use করলে internally এটা হয়:

```python
context = {
    'request': request,
    'format': self.format_kwarg,
    'view': self
}
```

👉 তাই তুমি serializer-এ সরাসরি এটা use করতে পারো:

```python
self.context['request'].user
```

---

# 🔥 🔹 Custom context send করার way

## ✅ Method: `get_serializer_context()` override

---

## Example (Cart System 🛒)

### ViewSet

```python
from rest_framework.viewsets import ModelViewSet

class CartItemViewSet(ModelViewSet):
    serializer_class = CartItemSerializer

    def get_serializer_context(self):
        context = super().get_serializer_context()
        context['cart_id'] = self.kwargs['cart_pk']  # URL থেকে নিচ্ছি
        return context
```

---

👉 ধরো URL:

```
/api/carts/5/items/
```

👉 এখানে:

```python
self.kwargs['cart_pk'] = 5
```

---

# 🔥 🔹 Serializer-এ use

```python
class CartItemSerializer(serializers.ModelSerializer):

    def create(self, validated_data):
        cart_id = self.context['cart_id']
        user = self.context['request'].user

        return CartItem.objects.create(
            cart_id=cart_id,
            user=user,
            **validated_data
        )
```

---

# 🔥 🔹 Full Flow

### 1. Request

```
POST /api/carts/5/items/
```

```json
{
  "product": "Phone",
  "quantity": 1
}
```

---

### 2. ViewSet

* `cart_id = 5` context-এ add হলো

---

### 3. Serializer

* `self.context['cart_id']` use হলো
* `self.context['request'].user` use হলো

---

### 4. DB Save

```json
{
  "product": "Phone",
  "quantity": 1,
  "cart_id": 5,
  "user": 1
}
```

---

# 🔥 🔹 আরেকটা Example (তোমার CCTV project 🚨)

## ViewSet

```python
class DetectionViewSet(ModelViewSet):
    serializer_class = DetectionSerializer

    def get_serializer_context(self):
        context = super().get_serializer_context()
        context['camera_id'] = self.kwargs['camera_id']
        return context
```

---

## Serializer

```python
def create(self, validated_data):
    return Detection.objects.create(
        camera_id=self.context['camera_id'],
        user=self.context['request'].user,
        **validated_data
    )
```

---

# 🔥 🔹 Alternative (Less common)

👉 directly serializer call করলে:

```python
serializer = self.get_serializer(
    data=request.data,
    context={'cart_id': 5}
)
```

👉 কিন্তু `ModelViewSet`-এ usually দরকার হয় না

---

# ⚠️ Common Mistake

❌ override না করে context use করা:

```python
self.context['cart_id']  # KeyError
```

---

# 🔥 🔹 Pro Tip

👉 Always extend context:

```python
context = super().get_serializer_context()
```

❌ overwrite করো না

---

# 🔥 Final Rule

👉 `ModelViewSet` এ custom context পাঠাতে:

✔ `get_serializer_context()` override করো
✔ `self.kwargs`, `request.user` use করো

---

