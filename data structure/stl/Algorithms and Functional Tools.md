Excellent — you’re diving into an important Python concept area: **Algorithms and Functional Tools** 💡

Let’s break it down in a **clear, practical, and structured** way 👇

---

## ⚙️ **1. Algorithms in Python**

In Python, **algorithms** are just well-defined **steps or logic** used to solve a problem.  
They can be written using loops, conditionals, recursion, or functional tools.

Here are the main types and common examples:

### 🧩 **Common Algorithm Categories**

|Category|Description|Example|
|---|---|---|
|**Searching**|Find an element in a list or dataset|Linear Search, Binary Search|
|**Sorting**|Arrange data in order|Bubble Sort, Merge Sort, Quick Sort|
|**Recursion**|Function calls itself|Factorial, Fibonacci|
|**Greedy Algorithms**|Pick best local option|Coin Change, Huffman Coding|
|**Divide & Conquer**|Break problem into subproblems|Merge Sort, Quick Sort|
|**Dynamic Programming**|Use previous results for efficiency|Fibonacci with memoization|
|**Graph Algorithms**|Work with nodes and edges|BFS, DFS, Dijkstra’s|

---

### 🧠 Example: **Binary Search**

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1

nums = [1, 3, 5, 7, 9, 11]
print(binary_search(nums, 7))  # Output: 3
```

---

## 🧮 **2. Functional Tools in Python**

Python supports **functional programming**, which treats functions as **first-class citizens** — meaning you can pass them around like variables.

### 🔹 Main Functional Tools:

|Tool|Purpose|Example|
|---|---|---|
|**`map()`**|Apply a function to every element|`map(str.upper, ['a','b'])`|
|**`filter()`**|Keep elements that satisfy a condition|`filter(lambda x: x>0, nums)`|
|**`reduce()`** (from `functools`)|Apply a rolling computation to pairs of elements|`reduce(lambda x,y:x+y, nums)`|
|**`lambda`**|Create small anonymous functions|`lambda x: x*x`|
|**`zip()`**|Combine multiple iterables|`zip(names, scores)`|
|**`enumerate()`**|Get index and value from iterable|`enumerate(items)`|
|**`sorted()`**|Sort with custom key|`sorted(data, key=lambda x: x[1])`|
|**`any()` / `all()`**|Check logical conditions across items|`any(x > 0 for x in nums)`|

---

### 💡 Examples of Functional Tools in Action:

#### 🧩 `map()`

```python
nums = [1, 2, 3, 4]
squares = list(map(lambda x: x ** 2, nums))
print(squares)  # [1, 4, 9, 16]
```

#### 🧩 `filter()`

```python
nums = [10, 15, 20, 25, 30]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)  # [10, 20, 30]
```

#### 🧩 `reduce()`

```python
from functools import reduce

nums = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, nums)
print(product)  # 24
```

#### 🧩 `zip()`

```python
names = ["Alice", "Bob", "Charlie"]
scores = [85, 90, 95]
paired = list(zip(names, scores))
print(paired)  # [('Alice', 85), ('Bob', 90), ('Charlie', 95)]
```

#### 🧩 `enumerate()`

```python
for index, value in enumerate(['a', 'b', 'c']):
    print(index, value)
# 0 a
# 1 b
# 2 c
```

---

## 🧭 **3. Combining Algorithms + Functional Tools**

Functional tools can make algorithm writing **shorter and cleaner**.

Example: **Sum of squares of even numbers**

```python
from functools import reduce

nums = [1, 2, 3, 4, 5, 6]
result = reduce(
    lambda x, y: x + y,
    map(lambda n: n * n, filter(lambda n: n % 2 == 0, nums))
)
print(result)  # (2² + 4² + 6²) = 56
```

---

## 🧱 Summary Table

|Concept|Description|Mutable?|Example|
|---|---|---|---|
|**Algorithm**|Step-by-step procedure for solving a problem|—|Binary Search|
|**Functional Tool**|Built-in methods for data transformations|—|`map()`, `filter()`, `reduce()`|
|**Use Together**|Cleaner and faster algorithmic logic|—|Combine map + filter + reduce|

---

# 🔍 Sorting and Searching Algorithms using Functional Tools

---

## ⚙️ **1. Sorting Algorithms**

Python has a built-in `sorted()` function and a `.sort()` list method.  
They use the **Timsort algorithm** (a hybrid of merge sort and insertion sort), which is **O(n log n)**.

---

### 🧩 **Basic Example**

```python
nums = [5, 2, 9, 1, 5, 6]
sorted_nums = sorted(nums)
print(sorted_nums)  # [1, 2, 5, 5, 6, 9]
```

---

### 🧠 **Using Functional Tools with Sorting**

The `sorted()` function takes two powerful parameters:

- `key` → a function to customize sorting order (uses **functional tools** like `lambda`)
    
- `reverse` → for descending order
    

---

### ✅ **Example 1: Sort with `lambda` (functional key)**

```python
words = ["apple", "banana", "cherry", "date"]
# Sort by length of each word
sorted_words = sorted(words, key=lambda x: len(x))
print(sorted_words)  # ['date', 'apple', 'banana', 'cherry']
```

---

### ✅ **Example 2: Sort a List of Tuples**

```python
students = [("Alice", 25), ("Bob", 20), ("Charlie", 23)]
# Sort by age
sorted_students = sorted(students, key=lambda s: s[1])
print(sorted_students)
# [('Bob', 20), ('Charlie', 23), ('Alice', 25)]
```

---

### ✅ **Example 3: Sort Dictionary by Values**

```python
scores = {"Alice": 85, "Bob": 92, "Charlie": 78}

# Sort by value using items() + lambda
sorted_scores = dict(sorted(scores.items(), key=lambda x: x[1], reverse=True))
print(sorted_scores)
# {'Bob': 92, 'Alice': 85, 'Charlie': 78}
```

---

### ✅ **Example 4: Functional Composition**

You can combine `map()` or `filter()` before sorting:

```python
nums = [10, 3, 5, 7, 2, 9, 8]
# Filter even numbers, then sort them
even_sorted = sorted(filter(lambda x: x % 2 == 0, nums))
print(even_sorted)  # [2, 8, 10]
```

---

## 🔎 **2. Searching Algorithms**

You can write searching algorithms (like linear or binary search) and combine them with functional tools such as `filter()`, `any()`, or `next()`.

---

### 🧩 **Linear Search (with Functional Tools)**

```python
nums = [10, 20, 30, 40, 50]
target = 30

found = any(map(lambda x: x == target, nums))
print("Found:", found)  # True
```

Or return the **first matching element** using `next()` and a generator:

```python
nums = [10, 20, 30, 40, 50]
target = 40

result = next((x for x in nums if x == target), None)
print(result)  # 40
```

---

### 🧩 **Binary Search (Functional Version)**

If the list is sorted, you can use the built-in `bisect` module for binary search efficiently:

```python
import bisect

nums = [10, 20, 30, 40, 50]
target = 30

index = bisect.bisect_left(nums, target)
if index != len(nums) and nums[index] == target:
    print(f"Found {target} at index {index}")
else:
    print("Not found")
```

Or a **manual functional approach** (not optimal but expressive):

```python
def binary_search(arr, target):
    if not arr:
        return False
    mid = len(arr) // 2
    if arr[mid] == target:
        return True
    elif arr[mid] > target:
        return binary_search(arr[:mid], target)
    else:
        return binary_search(arr[mid+1:], target)

print(binary_search([1, 2, 3, 4, 5, 6], 4))  # True
```

---

## 🧮 **3. Combining Sorting + Searching with Functional Tools**

Here’s an elegant example that uses multiple tools together 👇

```python
from functools import reduce

# Dataset: list of (name, score)
data = [("Alice", 85), ("Bob", 92), ("Charlie", 78), ("David", 90)]

# 1️⃣ Filter students who scored above 80
filtered = filter(lambda x: x[1] > 80, data)

# 2️⃣ Sort them by score descending
sorted_data = sorted(filtered, key=lambda x: x[1], reverse=True)

# 3️⃣ Extract only names
names = list(map(lambda x: x[0], sorted_data))

print(names)  # ['Bob', 'David', 'Alice']
```

---

## 🧾 Summary Table

|Operation|Functional Tool Used|Example|
|---|---|---|
|Sort list by rule|`sorted(..., key=lambda ...)`|`sorted(words, key=len)`|
|Sort dictionary|`sorted(dict.items(), key=lambda x: x[1])`|sort by value|
|Filter before sorting|`filter() + sorted()`|sort even numbers|
|Search value|`any()`, `next()`|`any(map(lambda x: x==5, arr))`|
|Binary search|`bisect`|`bisect_left(sorted_list, target)`|

---

#### **custom functional pipeline**

---

# ⚙️ Custom Functional Pipeline in Python

We’ll go step-by-step — starting with raw data and transforming it through **a series of functional tools**.

---

## 🧩 Example Scenario

You have a list of products with their:

- name
    
- price
    
- rating
    

You want to:

1. Filter out cheap products (price < 50)
    
2. Apply a 10% discount to the remaining ones
    
3. Sort them by rating (high → low)
    
4. Compute the **total discounted price** of all high-rated products
    

---

### ✅ Step-by-Step Functional Pipeline

```python
from functools import reduce

# Sample dataset: (product_name, price, rating)
products = [
    ("Laptop", 1000, 4.5),
    ("Headphones", 40, 4.2),
    ("Keyboard", 80, 4.8),
    ("Mouse", 25, 3.9),
    ("Monitor", 300, 4.7),
    ("USB Drive", 15, 4.1),
]

# 1️⃣ Filter: Keep only products with price >= 50
filtered = filter(lambda p: p[1] >= 50, products)

# 2️⃣ Map: Apply 10% discount to the price
discounted = map(lambda p: (p[0], p[1] * 0.9, p[2]), filtered)

# 3️⃣ Sort: By rating (descending)
sorted_products = sorted(discounted, key=lambda p: p[2], reverse=True)

# 4️⃣ Reduce: Sum up the total discounted price
total_price = reduce(lambda acc, p: acc + p[1], sorted_products, 0)

# 5️⃣ Print final results
print("Final Sorted Products (after discount):")
for p in sorted_products:
    print(f"{p[0]} - ${p[1]:.2f} - Rating: {p[2]}⭐")

print("\nTotal discounted price of all filtered products:", round(total_price, 2))
```

---

### 🧠 Output Example

```
Final Sorted Products (after discount):
Keyboard - $72.00 - Rating: 4.8⭐
Monitor - $270.00 - Rating: 4.7⭐
Laptop - $900.00 - Rating: 4.5⭐

Total discounted price of all filtered products: 1242.0
```

---

## 🔍 What Happened (Conceptually)

|Step|Tool Used|Purpose|
|---|---|---|
|1️⃣ Filter|`filter()`|Removed low-priced items|
|2️⃣ Map|`map()`|Transformed (applied discount)|
|3️⃣ Sort|`sorted(..., key=lambda)`|Ordered by rating|
|4️⃣ Reduce|`reduce()`|Aggregated total|
|✅ Result|All functional tools chained together|Clean, readable pipeline|

---

## 🧠 Bonus: Make It a Reusable Function (Functional Pipeline Style)

We can wrap it up in one reusable **pipeline function**:

```python
def product_pipeline(products, min_price=50, discount=0.1):
    from functools import reduce

    # Functional transformation chain
    filtered = filter(lambda p: p[1] >= min_price, products)
    discounted = map(lambda p: (p[0], p[1] * (1 - discount), p[2]), filtered)
    sorted_products = sorted(discounted, key=lambda p: p[2], reverse=True)
    total_price = reduce(lambda acc, p: acc + p[1], sorted_products, 0)

    return sorted_products, total_price


# Usage
products = [
    ("Laptop", 1000, 4.5),
    ("Mouse", 25, 3.9),
    ("Keyboard", 80, 4.8),
    ("Monitor", 300, 4.7),
]
result, total = product_pipeline(products)
print(result)
print("Total:", total)
```

---

## ⚡ Key Takeaways

|Tool|Purpose|Example|
|---|---|---|
|`filter()`|Select specific elements|`filter(lambda x: x > 0, data)`|
|`map()`|Transform elements|`map(lambda x: x*x, data)`|
|`sorted()`|Reorder data|`sorted(data, key=lambda x: x[2])`|
|`reduce()`|Combine all into one result|`reduce(lambda x, y: x+y, data)`|

---

✅ **Functional pipelines** like this are:

- Short, readable, and expressive
    
- Great for data processing, analytics, or ETL
    
- Avoid explicit loops — focus on _what to do_, not _how to do it_
    

---
