
## **1. What is a Variable?**

A **variable** is like a container that stores data in a computer program. You can store, change, and use this data as needed.

**Example in Python:**

```python
age = 25
name = "Atiar"
is_student = True
```

Here:

- `age` stores a number (integer)
    
- `name` stores text (string)
    
- `is_student` stores a boolean value (`True` or `False`)
    

---

## **2. Properties of Variables**

1. **Name** – Identifier of the variable (like `age`, `name`)
    
2. **Value** – Data stored in the variable (like `25`, `"Atiar"`)
    
3. **Type** – Kind of data stored (integer, string, etc.)
    

---

## **3. Rules for Naming Variables**

- Must start with a letter or underscore (`_`)
    
- Can contain letters, numbers, and underscores
    
- Case-sensitive (`age` and `Age` are different)
    
- Cannot use reserved keywords (`if`, `while`, `class`, etc.)
    

**Example:**

```python
_age = 30
studentName = "Rahman"
# 2age = 25   <- Wrong
```

---

## **4. Types of Variables**

### **a) Based on Data Type**

1. **Integer** – Whole numbers (`10`, `-5`)
    
2. **Float** – Decimal numbers (`10.5`, `-3.14`)
    
3. **String** – Text (`"Hello"`, `'Atiar'`)
    
4. **Boolean** – True/False values (`True`, `False`)
    
5. **List/Array** – Collection of items (`[1,2,3]`, `["a","b"]`)
    
6. **Dictionary/Object** – Key-value pairs (`{"name": "Atiar", "age": 25}`)
    

---

### **b) Based on Scope**

1. **Local Variable** – Declared inside a function and used only there
    
2. **Global Variable** – Declared outside functions and accessible everywhere
    
3. **Instance Variable** – Belongs to an object in OOP
    
4. **Class Variable** – Shared by all objects of a class
    

---

### **c) Based on Mutability**

1. **Mutable Variable** – Value can change (lists, dictionaries)
    
2. **Immutable Variable** – Value cannot change (integers, strings, tuples)
    

---

## **5. Why Use Variables?**

- To store temporary data
    
- To make programs flexible
    
- To avoid repeating the same value
    
- To make code readable and maintainable
    

---

### **6. Example in Python**

```python
# Global variable
school = "ABC High School"

def student_info():
    # Local variable
    name = "Atiar"
    age = 18
    print(f"{name} studies at {school} and is {age} years old")

student_info()
```

Output:

```
Atiar studies at ABC High School and is 18 years old
```

---


### Example of Immutable variable

## **1. What is an Immutable Variable?**

An **immutable variable** is a variable whose **value cannot be changed** after it’s created.  
If you try to change it, a **new variable/object** is created instead.

---

## **2. Common Immutable Types in Python**

- **Integer** (`int`)
    
- **Float** (`float`)
    
- **String** (`str`)
    
- **Tuple** (`tuple`)
    
- **Boolean** (`bool`)
    

---

## **3. Example 1: Integer (Immutable)**

```python
x = 10
print(id(x))  # memory address of x
x = x + 5     # changes value
print(x)
print(id(x))  # new memory address
```

Output:

```
10
15
```

> Notice: The `id` (memory address) changes because integers are immutable.

---

## **4. Example 2: String (Immutable)**

```python
name = "Atiar"
print(id(name))   # memory address
name = name + " Rahman"
print(name)
print(id(name))   # new memory address
```

Output:

```
Atiar
Atiar Rahman
```

> The original string `"Atiar"` did not change; a **new string** was created.

---

## **5. Example 3: Tuple (Immutable)**

```python
numbers = (1, 2, 3)
# numbers[0] = 10  <- This will give an error
print(numbers)
```

Output:

```
(1, 2, 3)
```

> Tuples cannot be changed once created.

---

## 🧱 **1. What is a Constant?**

A **constant** is a **fixed value** that **cannot be changed** during the execution of a program.

You can think of it as a **locked box** — once you store a value, it stays the same.

---

### **Example (in Python):**

```python
PI = 3.1416
GRAVITY = 9.8
```

- Here, `PI` and `GRAVITY` are **constants**.
    
- By naming convention, constants are usually written in **UPPERCASE** letters (but Python does not enforce it strictly).
    

---

### **In C or Java:**

You can use the `const` or `final` keyword to make a true constant:

```c
const float PI = 3.1416;
```

```java
final double GRAVITY = 9.8;
```

---

### ✅ **Why Use Constants?**

1. Makes your code easier to understand
    
2. Prevents accidental value changes
    
3. Improves readability and maintenance
    

---

## 🧮 **2. What are Data Types?**

A **data type** tells the computer **what kind of value** a variable or constant holds — number, text, true/false, etc.

---

### **Common Data Types (with examples):**

|Data Type|Description|Example|
|---|---|---|
|**Integer (int)**|Whole numbers|`x = 10`|
|**Float (float)**|Decimal numbers|`pi = 3.14`|
|**String (str)**|Text|`name = "Atiar"`|
|**Boolean (bool)**|True or False|`is_active = True`|
|**List (array)**|Ordered, changeable collection|`numbers = [1, 2, 3]`|
|**Tuple**|Ordered, unchangeable collection|`point = (4, 5)`|
|**Set**|Unordered collection, no duplicates|`{1, 2, 3}`|
|**Dictionary (object)**|Key-value pairs|`student = {"name": "Atiar", "age": 20}`|

---

### **Example (Python):**

```python
age = 20               # int
height = 5.9           # float
name = "Atiar"         # string
is_student = True      # bool
marks = [85, 90, 78]   # list
person = {"name": "Atiar", "age": 20}  # dictionary
```

---

## 🧠 **Summary Table**

|Concept|Can Change?|Example|Mutable?|
|---|---|---|---|
|**Constant**|❌ No|`PI = 3.1416`|No|
|**Variable**|✅ Yes|`x = 10`|Depends on data type|
|**Integer**|✅ Yes|`10, 50`|Immutable|
|**List**|✅ Yes|`[1, 2, 3]`|Mutable|
|**String**|✅ Yes|`"Hello"`|Immutable|

---
