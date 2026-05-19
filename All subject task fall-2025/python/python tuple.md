
# 🔷 1. Tuple কী?

👉 Tuple = ordered + immutable (change করা যায় না)

```python
t = (1, 2, 3)
```

---

# 🔷 2. Tuple Create করার সব উপায়

```python
t1 = (1, 2, 3)
t2 = tuple([4, 5, 6])
t3 = ("a", "b", "c")

# single item (IMPORTANT 🔥)
t4 = (5,)   # comma must
```

---

# 🔷 3. Indexing & Slicing

```python
t = (10, 20, 30, 40)

t[0]     # 10
t[-1]    # 40
t[1:3]   # (20, 30)
```

---

# 🔷 4. Tuple Immutable (CORE CONCEPT)

```python
t = (1,2,3)

# ❌ error
# t[0] = 100
```

👉 change করতে হলে:

```python
t = list(t)
t[0] = 100
t = tuple(t)
```

---

# 🔷 5. Looping

```python
t = (1,2,3)

for x in t:
    print(x)
```

---

# 🔷 6. Tuple Methods (only 2 🔥)

```python
t = (1,2,2,3)

t.count(2)   # 2
t.index(3)   # 3
```

👉 List এর মতো অনেক method নাই

---

# 🔷 7. Packing & Unpacking (🔥 VERY IMPORTANT)

### Packing

```python
t = 1, 2, 3
```

### Unpacking

```python
a, b, c = (1, 2, 3)
```

### Advanced unpacking

```python
a, *b = (1,2,3,4)
# a=1, b=[2,3,4]
```

---

# 🔷 8. Nested Tuple

```python
t = ((1,2), (3,4))

print(t[1][0])  # 3
```

---

# 🔷 9. Tuple vs List (🔥 Interview)

| Feature | Tuple      | List    |
| ------- | ---------- | ------- |
| Mutable | ❌          | ✅       |
| Speed   | faster     | slower  |
| Memory  | less       | more    |
| Use     | fixed data | dynamic |

---

# 🔷 10. Built-in Functions

```python
t = (1,2,3,4)

len(t)
max(t)
min(t)
sum(t)
```

---

# 🔷 11. Tuple with Multiple Data Types

```python
t = (1, "hello", True)
```

---

# 🔷 12. Real Use Cases (IMPORTANT FOR YOU)

## 🔸 Django (choices field)

```python
STATUS = (
    ("P", "Pending"),
    ("C", "Completed")
)
```

---

## 🔸 Data Analysis

```python
point = (10, 20)   # coordinate
```

---

## 🔸 Function Return (VERY COMMON)

```python
def calc():
    return 10, 20

a, b = calc()
```

---

# 🔷 13. Set vs Tuple Confusion

```python
a = (1,2,3)  # tuple
b = {1,2,3}  # set
```

---

# 🔷 14. Tuple Concatenation

```python
t1 = (1,2)
t2 = (3,4)

t3 = t1 + t2   # (1,2,3,4)
```

---

# 🔷 15. Repeat Tuple

```python
t = (1,2) * 3
# (1,2,1,2,1,2)
```

---

# 🔷 16. Membership Test

```python
t = (1,2,3)

print(2 in t)  # True
```

---

# 🔷 17. Convert Tuple ↔ List

```python
list(t)
tuple([1,2,3])
```

---

# 🔷 18. Advanced Concept (🔥 Pro Level)

### Tuple as dictionary key

```python
d = {
    (1,2): "point"
}
```

👉 list key হতে পারে না

---

### Immutable but nested mutable (tricky 🔥)

```python
t = (1, [2,3])

t[1].append(4)

print(t)  # (1, [2,3,4])
```

---

# 🔥 Final Summary

👉 Tuple = fixed data
👉 Fast + memory efficient
👉 Mostly used for:

* return values
* config/constant data
* coordinates
* Django choices

---


# 🟢 EASY LEVEL (1–5)

---

## ✅ 1. Tuple create করো

👉 (1,2,3,4)

✔ Answer:

```python
t = (1, 2, 3, 4)
```

🧠 Explanation: round bracket দিয়ে tuple define করা হয়

---

## ✅ 2. single item tuple বানাও

✔ Answer:

```python
t = (5,)
```

🧠 Explanation: comma না দিলে এটা int হয়ে যাবে

---

## ✅ 3. first element access করো

```python
t = (10,20,30)
```

✔ Answer:

```python
t[0]
```

---

## ✅ 4. last element access করো

✔ Answer:

```python
t[-1]
```

---

## ✅ 5. tuple length বের করো

✔ Answer:

```python
len(t)
```

---

# 🟡 MEDIUM LEVEL (6–10)

---

## ✅ 6. tuple slice করো (20,30 বের করো)

```python
t = (10,20,30,40)
```

✔ Answer:

```python
t[1:3]
```

---

## ✅ 7. tuple loop করো

✔ Answer:

```python
for x in t:
    print(x)
```

---

## ✅ 8. count করো

```python
t = (1,2,2,3)
```

✔ Answer:

```python
t.count(2)
```

---

## ✅ 9. index বের করো

✔ Answer:

```python
t.index(3)
```

---

## ✅ 10. tuple unpack করো

```python
t = (1,2,3)
```

✔ Answer:

```python
a, b, c = t
```

---

# 🔴 ADVANCED LEVEL (11–15)

---

## ✅ 11. extended unpacking

```python
t = (1,2,3,4,5)
```

✔ Answer:

```python
a, *b = t
# a=1, b=[2,3,4,5]
```

---

## ✅ 12. tuple concatenate করো

```python
t1 = (1,2)
t2 = (3,4)
```

✔ Answer:

```python
t3 = t1 + t2
```

---

## ✅ 13. tuple repeat করো

✔ Answer:

```python
t = (1,2) * 3
```

---

## ✅ 14. tuple কে list এ convert করে change করো

```python
t = (1,2,3)
```

✔ Answer:

```python
l = list(t)
l[0] = 100
t = tuple(l)
```

🧠 Explanation: tuple immutable তাই সরাসরি change করা যায় না

---

## ✅ 15. nested tuple access করো

```python
t = ((1,2), (3,4))
```

✔ Answer:

```python
t[1][0]   # 3
```

---

# 🔥 Bonus (Interview Level)

## 👉 Function থেকে multiple value return

```python
def func():
    return 10, 20

a, b = func()
```

---

# 🎯 Important শেখার জিনিস

👉 তুমি যদি এগুলো বুঝো, তুমি already strong:

* tuple immutable concept ✅
* unpacking (🔥 very important)
* nested tuple
* tuple vs list usage

---

# 🔥 1. Function return multiple values (MOST COMMON)

```python
def calc():
    return 10, 20

a, b = calc()
```

👉 কেন tuple?

* multiple value return easy
* safe (change হবে না)

---

# 🔥 2. Django Model Choices (VERY IMPORTANT FOR YOU)

```python
STATUS = (
    ("P", "Pending"),
    ("C", "Completed"),
)
```

👉 কেন tuple?

* fixed data (change হওয়া উচিত না)
* production safe

---

# 🔥 3. Coordinates / Position (Data Analysis / ML)

```python
point = (10, 20)
```

👉 Use:

* image processing
* object detection (x, y)

---

# 🔥 4. Dictionary Key হিসেবে (🔥 interview question)

```python
d = {
    (1,2): "point A"
}
```

👉 কেন tuple?

* immutable → hashable → key হিসেবে use করা যায়
* list ❌ (error দিবে)

---

# 🔥 5. Fixed configuration / settings

```python
COLORS = ("red", "green", "blue")
```

👉 Use:

* config data
* constants

---

# 🔥 6. Looping multiple values (unpacking)

```python
pairs = [(1,2), (3,4)]

for a, b in pairs:
    print(a, b)
```

👉 Clean code 🔥

---

# 🔥 7. Database / Query Result (Real Backend)

```python
row = ("Atiar", 25, "Dhaka")
```

👉 Use:

* SQL query result
* API response (sometimes)

---

# 🔥 8. Performance critical case

👉 Tuple faster than list

```python
t = (1,2,3)
l = [1,2,3]
```

👉 ML / large data → tuple better for fixed data

---

# 🔥 9. Protect data (VERY IMPORTANT)

```python
user_roles = ("admin", "user", "staff")
```

👉 কেউ accidentally change করতে পারবে না

---

# 🔥 10. Set-like structure inside list

```python
data = [(1,2), (3,4)]
```

👉 structured data

---

# 🧠 Tuple vs List (Real Decision Rule)

| Situation      | Use          |
| -------------- | ------------ |
| change দরকার   | list ✅       |
| fixed data     | tuple ✅      |
| dictionary key | tuple ✅      |
| performance    | tuple better |

---

# 🚀 Real Life Analogy

* **List** = shopping cart (change হয়)
* **Tuple** = NID number (fixed)

---

# 🔥 Final Shortcut

👉 Use tuple when:

* data change হবে না
* constant data
* multiple return
* key হিসেবে use

---

# 🚀 Next Level (Recommended)


# 🟢 BASIC TRICKY (1–5)

---

## ✅ 1. List reference problem

```python
a = [1,2,3]
b = a
b.append(4)

print(a)
```

✔ Answer:

```python
[1,2,3,4]
```

🧠 Explanation:
👉 `b = a` → same memory reference

---

## ✅ 2. Copy fix

```python
a = [1,2,3]
b = a.copy()
b.append(4)

print(a)
```

✔ Answer:

```python
[1,2,3]
```

---

## ✅ 3. Mutable default argument (🔥 VERY IMPORTANT)

```python
def func(x=[]):
    x.append(1)
    return x

print(func())
print(func())
```

✔ Answer:

```python
[1]
[1,1]
```

🧠 Explanation:
👉 default list একবারই তৈরি হয়

---

## ✅ 4. is vs ==

```python
a = [1,2]
b = [1,2]

print(a == b)
print(a is b)
```

✔ Answer:

```python
True
False
```

---

## ✅ 5. Tuple single item

```python
t = (5)
print(type(t))
```

✔ Answer:

```python
<class 'int'>
```

✔ Correct:

```python
t = (5,)
```

---

# 🟡 MEDIUM TRICKY (6–10)

---

## ✅ 6. List multiplication trap

```python
a = [[0]*3]*3
a[0][0] = 1

print(a)
```

✔ Answer:

```python
[[1,0,0],[1,0,0],[1,0,0]]
```

🧠 Explanation:
👉 same reference repeated

---

## ✅ 7. Fix above problem

✔ Answer:

```python
a = [[0]*3 for _ in range(3)]
```

---

## ✅ 8. Late binding (lambda)

```python
funcs = []
for i in range(3):
    funcs.append(lambda: i)

print([f() for f in funcs])
```

✔ Answer:

```python
[2,2,2]
```

---

## ✅ 9. Fix lambda problem

✔ Answer:

```python
funcs.append(lambda i=i: i)
```

---

## ✅ 10. List vs tuple speed (concept)

👉 Question: কোনটা faster?

✔ Answer:
👉 Tuple faster (immutable)

---

# 🔴 ADVANCED TRICKY (11–15)

---

## ✅ 11. Mutable inside tuple

```python
t = (1, [2,3])
t[1].append(4)

print(t)
```

✔ Answer:

```python
(1, [2,3,4])
```

🧠 Explanation:
👉 tuple immutable, but ভিতরের list mutable

---

## ✅ 12. String immutability

```python
s = "hello"
s[0] = "H"
```

✔ Answer:

```python
Error
```

---

## ✅ 13. Dictionary key restriction

```python
d = {[1,2]: "value"}
```

✔ Answer:

```python
Error
```

✔ Fix:

```python
d = {(1,2): "value"}
```

---

## ✅ 14. Generator vs list

```python
a = [x*x for x in range(3)]
b = (x*x for x in range(3))
```

✔ Answer:

* `a` → list
* `b` → generator

---

## ✅ 15. Boolean trap

```python
print(bool([]))
print(bool([0]))
```

✔ Answer:

```python
False
True
```

---

# 🔥 BONUS (VERY IMPORTANT)

## 👉 Swap without temp variable

```python
a, b = 5, 10
a, b = b, a
```

---

# 🎯 Interview Insight

👉 interviewer দেখে:

* তুমি concept বুঝো কিনা
* memory & reference বুঝো কিনা
* Pythonic thinking আছে কিনা

---

# 🟢 SECTION 1: List / Tuple / String (1–10)

---

### 1. Reverse a list without using `reverse()`

---

### 2. Remove duplicates from list (order maintain করতে হবে)

---

### 3. Find second largest number in list

---

### 4. Flatten a nested list

```python
[1, [2,3], [4,[5,6]]]
```

---

### 5. Check palindrome string

---

### 6. Count frequency of each element in list

---

### 7. Find missing number

```python
[1,2,3,5]
```

---

### 8. Merge two sorted list without using sort()

---

### 9. Find common elements between two lists

---

### 10. Rotate list k times

```python
[1,2,3,4,5] → k=2 → [4,5,1,2,3]
```

---

# 🟡 SECTION 2: Dictionary / Set (11–18)

---

### 11. Invert dictionary

```python
{"a":1,"b":2} → {1:"a",2:"b"}
```

---

### 12. Count word frequency in sentence

---

### 13. Find first non-repeating character

---

### 14. Group anagrams

```python
["eat","tea","tan","ate"]
```

---

### 15. Merge two dictionaries

---

### 16. Find duplicate elements using set

---

### 17. Sort dictionary by value

---

### 18. Check two strings are anagram

---

# 🔴 SECTION 3: Logic + Algorithms (19–25)

---

### 19. Fibonacci (without recursion)

---

### 20. Fibonacci (with recursion)

---

### 21. Factorial (iterative + recursive)

---

### 22. Binary search

---

### 23. Check prime number

---

### 24. Find all prime numbers in range

---

### 25. Find GCD of two numbers

---

# ⚫ SECTION 4: Advanced Python Concepts (26–30)

---

### 26. Implement your own map() function

---

### 27. Implement your own filter() function

---

### 28. Decorator তৈরি করো (function call count)

---

### 29. Generator তৈরি করো (custom range)

---

### 30. Class বানাও (Bank Account system)

👉 features:

* deposit
* withdraw
* balance check

---

# 🔥 How to Practice (VERY IMPORTANT)

👉 Step-by-step:

1. নিজে solve করো ❗
2. Google/ChatGPT help নিতে পারো
3. clean code লিখো
4. edge case চিন্তা করো

---

# 🚀 Pro Tip (Interview Hack)

👉 interviewer expect:

* logic clear
* readable code
* optimization thinking

---

# 🟢 SECTION 1: List / String (1–10)

---

## ✅ 1. Reverse list

```python
arr[::-1]
```

🧠 slicing → fastest way

---

## ✅ 2. Remove duplicates (order maintain)

```python
arr = [1,2,2,3]
res = []
for x in arr:
    if x not in res:
        res.append(x)
```

---

## ✅ 3. Second largest

```python
arr = [10,20,5,8]
arr = list(set(arr))
arr.sort()
print(arr[-2])
```

---

## ✅ 4. Flatten nested list

```python
def flatten(lst):
    res = []
    for x in lst:
        if isinstance(x, list):
            res.extend(flatten(x))
        else:
            res.append(x)
    return res
```

---

## ✅ 5. Palindrome

```python
s = "madam"
print(s == s[::-1])
```

---

## ✅ 6. Frequency count

```python
arr = [1,2,2,3]
freq = {}
for x in arr:
    freq[x] = freq.get(x, 0) + 1
```

---

## ✅ 7. Missing number

```python
arr = [1,2,3,5]
n = 5
print(n*(n+1)//2 - sum(arr))
```

---

## ✅ 8. Merge sorted list

```python
a = [1,3,5]
b = [2,4,6]
i=j=0
res = []
while i<len(a) and j<len(b):
    if a[i]<b[j]:
        res.append(a[i]); i+=1
    else:
        res.append(b[j]); j+=1
res += a[i:] + b[j:]
```

---

## ✅ 9. Common elements

```python
list(set(a) & set(b))
```

---

## ✅ 10. Rotate list

```python
k = 2
arr = arr[-k:] + arr[:-k]
```

---

# 🟡 SECTION 2: Dictionary / Set (11–18)

---

## ✅ 11. Invert dict

```python
d = {"a":1,"b":2}
inv = {v:k for k,v in d.items()}
```

---

## ✅ 12. Word frequency

```python
s = "hello world hello"
freq = {}
for w in s.split():
    freq[w] = freq.get(w,0)+1
```

---

## ✅ 13. First non-repeating char

```python
for c in s:
    if s.count(c)==1:
        print(c)
        break
```

---

## ✅ 14. Group anagrams

```python
from collections import defaultdict

words = ["eat","tea","tan","ate"]
d = defaultdict(list)

for w in words:
    key = "".join(sorted(w))
    d[key].append(w)

print(list(d.values()))
```

---

## ✅ 15. Merge dict

```python
d = {**d1, **d2}
```

---

## ✅ 16. Find duplicates

```python
arr = [1,2,2,3]
seen = set()
dup = set()

for x in arr:
    if x in seen:
        dup.add(x)
    seen.add(x)
```

---

## ✅ 17. Sort dict by value

```python
sorted(d.items(), key=lambda x: x[1])
```

---

## ✅ 18. Check anagram

```python
sorted(s1) == sorted(s2)
```

---

# 🔴 SECTION 3: Algorithms (19–25)

---

## ✅ 19. Fibonacci (iterative)

```python
a,b = 0,1
for _ in range(10):
    print(a)
    a,b = b,a+b
```

---

## ✅ 20. Fibonacci (recursive)

```python
def fib(n):
    if n<=1: return n
    return fib(n-1)+fib(n-2)
```

---

## ✅ 21. Factorial

```python
# iterative
res=1
for i in range(1,n+1):
    res*=i

# recursive
def fact(n):
    return 1 if n==0 else n*fact(n-1)
```

---

## ✅ 22. Binary search

```python
def binary(arr, target):
    l,r = 0,len(arr)-1
    while l<=r:
        m = (l+r)//2
        if arr[m]==target:
            return m
        elif arr[m]<target:
            l=m+1
        else:
            r=m-1
```

---

## ✅ 23. Prime check

```python
def is_prime(n):
    if n<2: return False
    for i in range(2,int(n**0.5)+1):
        if n%i==0:
            return False
    return True
```

---

## ✅ 24. All primes

```python
[x for x in range(2,50) if is_prime(x)]
```

---

## ✅ 25. GCD

```python
def gcd(a,b):
    while b:
        a,b = b,a%b
    return a
```

---

# ⚫ SECTION 4: Advanced (26–30)

---

## ✅ 26. Custom map

```python
def my_map(func, lst):
    return [func(x) for x in lst]
```

---

## ✅ 27. Custom filter

```python
def my_filter(func, lst):
    return [x for x in lst if func(x)]
```

---

## ✅ 28. Decorator (call count)

```python
def counter(func):
    count = 0
    def wrapper(*args):
        nonlocal count
        count += 1
        print("called", count)
        return func(*args)
    return wrapper
```

---

## ✅ 29. Generator (custom range)

```python
def my_range(n):
    i = 0
    while i<n:
        yield i
        i += 1
```

---

## ✅ 30. Bank Account Class

```python
class Bank:
    def __init__(self, bal=0):
        self.balance = bal

    def deposit(self, amt):
        self.balance += amt

    def withdraw(self, amt):
        if amt <= self.balance:
            self.balance -= amt

    def show(self):
        print(self.balance)
```

---

# 🎯 Final Advice (Important)

👉 তুমি এখন:

* Python core ✔
* Logic ✔
* Interview ready (basic-mid) ✔

---

