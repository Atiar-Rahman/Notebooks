
# 🔹 1. List কী?

List = ordered, mutable collection

```python
my_list = [1, 2, 3, 4]
```

---

# 🔹 2. List Create করার সব উপায়

```python
a = [1, 2, 3]
b = list((4, 5, 6))
c = list("hello")   # ['h','e','l','l','o']
d = [1, "abc", True]  # mixed type
```

---

# 🔹 3. Access (Indexing + Slicing)

```python
arr = [10, 20, 30, 40, 50]

arr[0]      # 10
arr[-1]     # 50
arr[1:4]    # [20, 30, 40]
arr[:3]     # [10, 20, 30]
arr[::2]    # [10, 30, 50]
```

---

# 🔹 4. List Change (Modify)

```python
arr[1] = 200
arr[1:3] = [100, 150]
```

---

# 🔹 5. Add Item

```python
arr.append(60)       # end e add
arr.insert(1, 15)    # specific position
arr.extend([70,80])  # multiple add
```

---

# 🔹 6. Remove Item

```python
arr.remove(20)   # value diye remove
arr.pop()        # last remove
arr.pop(1)       # index diye remove
del arr[0]
arr.clear()
```

---

# 🔹 7. Looping

```python
for x in arr:
    print(x)

for i in range(len(arr)):
    print(arr[i])
```

---

# 🔹 8. Important Built-in Functions

```python
len(arr)
max(arr)
min(arr)
sum(arr)
```

---

# 🔹 9. List Methods (VERY IMPORTANT 🔥)

```python
arr.sort()
arr.sort(reverse=True)

arr.reverse()

arr.copy()

arr.count(10)
arr.index(30)
```

---

# 🔹 10. List Comprehension (🔥 MUST KNOW)

```python
# normal
new = []
for x in range(5):
    new.append(x)

# comprehension
new = [x for x in range(5)]

# condition
even = [x for x in range(10) if x % 2 == 0]
```

---

# 🔹 11. Nested List

```python
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

print(matrix[1][2])  # 6
```

---

# 🔹 12. Unpacking

```python
a, b, c = [1, 2, 3]
```

---

# 🔹 13. List vs Tuple (Interview 🔥)

| Feature | List         | Tuple      |
| ------- | ------------ | ---------- |
| Mutable | ✅            | ❌          |
| Speed   | slower       | faster     |
| Use     | dynamic data | fixed data |

---

# 🔹 14. Real Use (VERY IMPORTANT FOR YOU)

## 🔸 Django

```python
users = ["admin", "staff", "user"]
```

## 🔸 Data Analysis (NumPy/Pandas)

```python
data = [10, 20, 30, 40]
```

## 🔸 Machine Learning

```python
features = [height, weight, age]
```

---

# 🔹 15. Common Interview Questions

✔ Reverse list

```python
arr[::-1]
```

✔ Remove duplicates

```python
list(set(arr))
```

✔ Find max

```python
max(arr)
```

✔ Flatten list

```python
[x for sub in matrix for x in sub]
```

---

# 🔹 16. Advanced (Pro Level 🔥)

### Lambda + map + filter

```python
list(map(lambda x: x*2, arr))
list(filter(lambda x: x%2==0, arr))
```

### Sorting with key

```python
arr = ["apple", "banana", "kiwi"]
arr.sort(key=len)
```

---

# 🔹 17. Memory Concept

* List stores reference
* Mutable → change possible

---
# MUST master:

✅ List comprehension
✅ Nested list
✅ Sorting
✅ Looping
✅ map/filter

---

# ✅ 1. List Comprehension (🔥 MUST)

👉 Short way to create list

### Basic

```python
nums = [x for x in range(5)]
# [0, 1, 2, 3, 4]
```

### With condition

```python
even = [x for x in range(10) if x % 2 == 0]
# [0,2,4,6,8]
```

### Real Use (ML/Data)

```python
squared = [x**2 for x in [1,2,3,4]]
```

---

# ✅ 2. Nested List (2D / Matrix)

👉 List ভিতরে list

```python
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]
```

### Access

```python
matrix[1][2]   # 6
```

### Loop

```python
for row in matrix:
    for col in row:
        print(col)
```

### Flatten (🔥 important)

```python
flat = [x for row in matrix for x in row]
```

---

# ✅ 3. Sorting (🔥 খুব important)

### Basic

```python
arr = [5,2,9,1]
arr.sort()   # [1,2,5,9]
```

### Reverse

```python
arr.sort(reverse=True)
```

### Custom (🔥 pro)

```python
words = ["apple", "banana", "kiwi"]
words.sort(key=len)
# ['kiwi', 'apple', 'banana']
```

### Dictionary sort (real project)

```python
students = [
    {"name": "A", "marks": 80},
    {"name": "B", "marks": 60}
]

students.sort(key=lambda x: x["marks"])
```

---

# ✅ 4. Looping (Core skill)

### Normal loop

```python
for x in arr:
    print(x)
```

### Index সহ

```python
for i in range(len(arr)):
    print(i, arr[i])
```

### Best way (🔥)

```python
for i, val in enumerate(arr):
    print(i, val)
```

---

# ✅ 5. map() & filter() (🔥 Pro Level)

---

## 🔹 map()

👉 Apply function to all elements

```python
nums = [1,2,3,4]

result = list(map(lambda x: x*2, nums))
# [2,4,6,8]
```

---

## 🔹 filter()

👉 Condition apply করে select করা

```python
nums = [1,2,3,4,5,6]

even = list(filter(lambda x: x%2==0, nums))
# [2,4,6]
```

---

# 🔥 map/filter vs list comprehension

### Same কাজ (comparison)

```python
# map
list(map(lambda x: x*2, nums))

# comprehension (better)
[x*2 for x in nums]
```

👉 Interview answer:

* Pythonic way = list comprehension ✅
* Functional style = map/filter

---

# 🚀 Real Project Example (IMPORTANT FOR YOU)

### Django / API data process

```python
users = [
    {"name": "A", "age": 17},
    {"name": "B", "age": 22}
]

adults = [u for u in users if u["age"] >= 18]
```

---

### ML / Data filtering

```python
data = [10, 20, 30, 40]

normalized = [x/100 for x in data]
```

---

# 🔥 Final Shortcut Summary

| Topic              | Use                    |
| ------------------ | ---------------------- |
| List Comprehension | fast + clean           |
| Nested List        | matrix / table         |
| Sorting            | data organize          |
| Looping            | iterate                |
| map/filter         | functional programming |


---

# 🔥 1. append() → item add (end এ)

```python
arr = [1, 2, 3]
arr.append(4)

print(arr)  # [1, 2, 3, 4]
```

👉 Use: single item add

---

# 🔥 2. extend() → multiple item add

```python
arr = [1, 2]
arr.extend([3, 4, 5])

print(arr)  # [1,2,3,4,5]
```

👉 Difference:

* append → one item
* extend → multiple items

---

# 🔥 3. insert() → specific position এ add

```python
arr = [1, 2, 3]
arr.insert(1, 100)

print(arr)  # [1,100,2,3]
```

---

# 🔥 4. remove() → value দিয়ে delete

```python
arr = [1, 2, 3, 2]
arr.remove(2)

print(arr)  # [1,3,2]
```

👉 first match remove করে

---

# 🔥 5. pop() → index দিয়ে delete

```python
arr = [10, 20, 30]

arr.pop()      # last remove
arr.pop(1)     # index remove
```

👉 return value দেয়

---

# 🔥 6. clear() → সব delete

```python
arr = [1,2,3]
arr.clear()

print(arr)  # []
```

---

# 🔥 7. index() → position বের করা

```python
arr = [10, 20, 30]

print(arr.index(20))  # 1
```

---

# 🔥 8. count() → কতবার আছে

```python
arr = [1,2,2,3]

print(arr.count(2))  # 2
```

---

# 🔥 9. sort() → sort করা

```python
arr = [5,1,4,2]
arr.sort()

print(arr)  # [1,2,4,5]
```

### reverse sort

```python
arr.sort(reverse=True)
```

---

# 🔥 10. reverse() → উল্টানো

```python
arr = [1,2,3]
arr.reverse()

print(arr)  # [3,2,1]
```

---

# 🔥 11. copy() → list copy

```python
arr = [1,2,3]
new = arr.copy()

new.append(4)

print(arr)  # [1,2,3]
print(new)  # [1,2,3,4]
```

👉 important: original change হয় না

---

# 🔥 12. Practical Example (🔥 Django / Real use)

```python
users = ["admin", "staff"]

users.append("user")
users.remove("staff")

print(users)
```

---

# 🔥 13. Common Mistake (VERY IMPORTANT)

```python
a = [1,2,3]
b = a   # ❌ same reference

b.append(4)

print(a)  # [1,2,3,4]
```

👉 Solution:

```python
b = a.copy()  # ✅
```

---

# 🔥 Final Summary Table

| Method    | কাজ               |
| --------- | ----------------- |
| append()  | item add          |
| extend()  | multiple add      |
| insert()  | specific position |
| remove()  | value delete      |
| pop()     | index delete      |
| clear()   | empty list        |
| index()   | position find     |
| count()   | frequency         |
| sort()    | sorting           |
| reverse() | reverse           |
| copy()    | clone             |

---



---

# 🟢 EASY LEVEL (1–7)

---

## ✅ 1. List এর শেষে 10 add করো

```python
arr = [1,2,3]
```

✔ Answer:

```python
arr.append(10)
```

---

## ✅ 2. [4,5] add করো

```python
arr = [1,2,3]
```

✔ Answer:

```python
arr.extend([4,5])
```

---

## ✅ 3. index 1 এ 100 insert করো

✔ Answer:

```python
arr.insert(1, 100)
```

---

## ✅ 4. value 2 remove করো

```python
arr = [1,2,3,2]
```

✔ Answer:

```python
arr.remove(2)
```

---

## ✅ 5. last element delete করো

✔ Answer:

```python
arr.pop()
```

---

## ✅ 6. list empty করো

✔ Answer:

```python
arr.clear()
```

---

## ✅ 7. 2 কতবার আছে বের করো

```python
arr = [1,2,2,3]
```

✔ Answer:

```python
arr.count(2)
```

---

# 🟡 MEDIUM LEVEL (8–14)

---

## ✅ 8. list reverse করো

```python
arr = [1,2,3]
```

✔ Answer:

```python
arr.reverse()
```

---

## ✅ 9. ascending sort করো

✔ Answer:

```python
arr.sort()
```

---

## ✅ 10. descending sort করো

✔ Answer:

```python
arr.sort(reverse=True)
```

---

## ✅ 11. largest number বের করো

```python
arr = [10,5,20]
```

✔ Answer:

```python
max(arr)
```

---

## ✅ 12. even numbers বের করো

✔ Answer:

```python
[x for x in arr if x % 2 == 0]
```

---

## ✅ 13. সব elements square করো

✔ Answer:

```python
[x**2 for x in arr]
```

---

## ✅ 14. list copy করো

✔ Answer:

```python
new = arr.copy()
```

---

# 🔴 ADVANCED LEVEL (15–20)

---

## ✅ 15. duplicate remove করো

```python
arr = [1,2,2,3,3]
```

✔ Answer:

```python
list(set(arr))
```

---

## ✅ 16. nested list flatten করো

```python
matrix = [[1,2],[3,4]]
```

✔ Answer:

```python
[x for row in matrix for x in row]
```

---

## ✅ 17. string length দিয়ে sort করো

```python
words = ["apple","kiwi","banana"]
```

✔ Answer:

```python
words.sort(key=len)
```

---

## ✅ 18. even numbers using filter()

✔ Answer:

```python
list(filter(lambda x: x % 2 == 0, arr))
```

---

## ✅ 19. সব elements double করো using map()

✔ Answer:

```python
list(map(lambda x: x*2, arr))
```

---

## ✅ 20. dictionary list থেকে age > 18 বের করো

```python
users = [
    {"name": "A", "age": 17},
    {"name": "B", "age": 22}
]
```

✔ Answer:

```python
[u for u in users if u["age"] > 18]
```

---

# 🔥 Bonus Challenge (Interview Level)

👉 reverse without reverse()

```python
arr[::-1]
```

---

# 🚀 Pro Tip (VERY IMPORTANT)

👉 শুধু answer দেখলে হবে না
👉 নিজে code run করো (VS Code / Jupyter)

---


