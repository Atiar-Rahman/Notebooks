Python-এর **OOP (Object-Oriented Programming)** এর **4টি Pillar (Four Pillars)** হলো:

1. **Encapsulation (এনক্যাপসুলেশন)**
    
2. **Abstraction (অ্যাবস্ট্রাকশন)**
    
3. **Inheritance (ইনহেরিটেন্স)**
    
4. **Polymorphism (পলিমরফিজম)**
    

নিচে প্রতিটি বিস্তারিত উদাহরণসহ দেওয়া হলো।

---

# 1. Encapsulation (Data Hiding)

**Definition:**  
ডাটা (attributes) এবং মেথড (methods) কে একই ক্লাসের মধ্যে রাখা এবং ডাটাকে সরাসরি পরিবর্তন করা থেকে রক্ষা করাকে Encapsulation বলে।

### Example

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance    # Private variable

    def deposit(self, amount):
        self.__balance += amount

    def withdraw(self, amount):
        if amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Insufficient Balance")

    def get_balance(self):
        return self.__balance


account = BankAccount(1000)

account.deposit(500)
account.withdraw(300)

print(account.get_balance())
```

### Output

```
1200
```

### Wrong Way

```python
print(account.__balance)
```

Output

```
AttributeError
```

কারণ `__balance` private variable।

---

# 2. Abstraction (Implementation Hiding)

**Definition:**  
যে জিনিস ব্যবহারকারীকে জানানো দরকার শুধু সেটাই দেখানো এবং ভিতরের implementation লুকিয়ে রাখাকে Abstraction বলে।

Python-এ সাধারণত `ABC (Abstract Base Class)` ব্যবহার করা হয়।

### Example

```python
from abc import ABC, abstractmethod

class Animal(ABC):

    @abstractmethod
    def sound(self):
        pass


class Dog(Animal):

    def sound(self):
        print("Dog says Woof")


class Cat(Animal):

    def sound(self):
        print("Cat says Meow")


dog = Dog()
cat = Cat()

dog.sound()
cat.sound()
```

### Output

```
Dog says Woof
Cat says Meow
```

---

যদি

```python
animal = Animal()
```

করেন তাহলে

```
TypeError
```

কারণ abstract class-এর object তৈরি করা যায় না।

---

# 3. Inheritance (Code Reusability)

**Definition:**  
একটি class-এর properties এবং methods অন্য class ব্যবহার করতে পারলে তাকে Inheritance বলে।

### Parent Class

```python
class Animal:

    def eat(self):
        print("Animal is eating")
```

### Child Class

```python
class Dog(Animal):

    def bark(self):
        print("Dog is barking")


dog = Dog()

dog.eat()
dog.bark()
```

### Output

```
Animal is eating
Dog is barking
```

---

## Types of Inheritance

### Single Inheritance

```python
class A:
    pass

class B(A):
    pass
```

---

### Multiple Inheritance

```python
class Father:
    def money(self):
        print("Father Money")

class Mother:
    def gold(self):
        print("Mother Gold")

class Child(Father, Mother):
    pass

c = Child()

c.money()
c.gold()
```

---

### Multilevel Inheritance

```python
class A:
    pass

class B(A):
    pass

class C(B):
    pass
```

---

### Hierarchical Inheritance

```python
class Animal:
    pass

class Dog(Animal):
    pass

class Cat(Animal):
    pass
```

---

### Hybrid Inheritance

Multiple + Multilevel এর combination।

---

# 4. Polymorphism (One Interface, Many Forms)

**Definition:**  
একই method বিভিন্ন class-এ ভিন্নভাবে কাজ করাকে Polymorphism বলে।

### Example

```python
class Dog:
    def sound(self):
        print("Woof")


class Cat:
    def sound(self):
        print("Meow")


animals = [Dog(), Cat()]

for animal in animals:
    animal.sound()
```

### Output

```
Woof
Meow
```

---

## Method Overriding

```python
class Animal:

    def sound(self):
        print("Animal Sound")


class Dog(Animal):

    def sound(self):
        print("Woof")


dog = Dog()
dog.sound()
```

Output

```
Woof
```

---

## Method Overloading

Python-এ Java/C++ এর মতো **true method overloading** নেই।

এর পরিবর্তে default arguments বা `*args` ব্যবহার করা হয়।

```python
class Math:

    def add(self, a, b=0, c=0):
        return a + b + c


m = Math()

print(m.add(5))
print(m.add(5, 3))
print(m.add(5, 3, 2))
```

Output

```
5
8
10
```

---

# Summary

|Pillar|Purpose|Example|
|---|---|---|
|Encapsulation|Data hide & protect|Private variable (`__balance`)|
|Abstraction|Hide implementation|`ABC`, `@abstractmethod`|
|Inheritance|Reuse code|Parent → Child|
|Polymorphism|Same method, different behavior|Method overriding|

---

# সহজে মনে রাখার ট্রিক

- **E – Encapsulation** → **Protect Data**
    
- **A – Abstraction** → **Hide Complexity**
    
- **I – Inheritance** → **Reuse Code**
    
- **P – Polymorphism** → **Many Behaviors**
    

**মনে রাখার সূত্র:** **EAIP** → **Encapsulation → Abstraction → Inheritance → Polymorphism**

এই ৪টি Pillar ভালোভাবে বুঝে নিলে Django এবং Django REST Framework-এর class-based views, serializers, permissions, mixins, viewsets ইত্যাদি শেখা অনেক সহজ হয়ে যায়, কারণ এগুলো OOP-এর এই ধারণাগুলোর ওপরই ভিত্তি করে তৈরি।

-------

Django-তে **Abstract Class** সাধারণ Python abstract class (`ABC`) থেকে আলাদা। Django Model-এ **abstract base model** ব্যবহার করা হয়, যাতে common fields এবং methods এক জায়গায় লিখে একাধিক model-এ reuse করা যায়।

---

# Basic Syntax

```python
from django.db import models

class BaseModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

এখানে

```python
class Meta:
    abstract = True
```

এই লাইনটাই model-টিকে abstract করে।

---

# Example

ধরুন অনেক model-এ একই field লাগবে।

Without Abstract Model ❌

```python
class Product(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

class Category(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

class Brand(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
```

একই code বারবার লিখতে হচ্ছে।

---

## With Abstract Model ✅

```python
from django.db import models

class TimeStampModel(models.Model):
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    class Meta:
        abstract = True
```

এখন inherit করো।

```python
class Category(TimeStampModel):
    name = models.CharField(max_length=100)

class Product(TimeStampModel):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)

class Brand(TimeStampModel):
    name = models.CharField(max_length=100)
```

---

## Database Table

Migration করলে table হবে

```
Category
---------
id
name
created_at
updated_at

Product
---------
id
name
price
created_at
updated_at

Brand
---------
id
name
created_at
updated_at
```

কিন্তু

```
TimeStampModel
```

নামে **কোন table তৈরি হবে না।**

---

# Another Example

সব model-এ UUID লাগবে।

```python
import uuid
from django.db import models

class UUIDModel(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    class Meta:
        abstract = True
```

ব্যবহার

```python
class Product(UUIDModel):
    name = models.CharField(max_length=200)

class Category(UUIDModel):
    name = models.CharField(max_length=100)
```

---

# Methods Also Inherited

```python
class BaseModel(models.Model):

    class Meta:
        abstract = True

    def hello(self):
        return "Hello Django"
```

```python
class Product(BaseModel):
    name = models.CharField(max_length=100)
```

```python
product = Product(name="Laptop")
print(product.hello())
```

Output

```
Hello Django
```

---

# Real Project Example

```python
import uuid
from django.db import models

class BaseModel(models.Model):
    id = models.UUIDField(
        primary_key=True,
        default=uuid.uuid4,
        editable=False
    )

    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    is_active = models.BooleanField(default=True)

    class Meta:
        abstract = True
```

এখন

```python
class Category(BaseModel):
    name = models.CharField(max_length=100)

class Product(BaseModel):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)

class Order(BaseModel):
    total = models.DecimalField(max_digits=10, decimal_places=2)
```

সব model-এ automatically থাকবে

- `id`
    
- `created_at`
    
- `updated_at`
    
- `is_active`
    

---

# Abstract Model vs Normal Model

|Feature|Abstract Model|Normal Model|
|---|---|---|
|Database Table|❌ No|✅ Yes|
|Can Create Object|❌ No|✅ Yes|
|Used for Inheritance|✅ Yes|✅ Yes|
|Common Fields|✅ Yes|❌ Not its main purpose|

---

# কখন Abstract Model ব্যবহার করবেন?

যখন একাধিক model-এ একই field বা method দরকার, যেমন:

- `id = UUIDField`
    
- `created_at`
    
- `updated_at`
    
- `is_active`
    
- `created_by`
    
- `updated_by`
    
- Common helper methods (`soft_delete()`, `activate()`, `deactivate()`)
    

এসব ক্ষেত্রে abstract base model ব্যবহার করলে code reuse হয়, duplication কমে এবং maintenance সহজ হয়।

> **নোট:** Django-র built-in `models.Model` নিজেও একটি base class। আপনি `Meta.abstract = True` সেট করলে সেটি reusable base model হয়ে যায় এবং migration-এর সময় এর জন্য আলাদা database table তৈরি হয় না।


------
