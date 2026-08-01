# Module 1 — Lesson 1: Why NumPy? (Foundation)

আজকের লক্ষ্য হলো **NumPy কী, কেন এটি তৈরি হয়েছে, এবং কেন Data Engineer ও ML Engineer-দের জন্য এটি বাধ্যতামূলক**—এগুলো গভীরভাবে বোঝা।

---

# Learning Objectives

এই লেসন শেষে তুমি জানতে পারবে:

* Python List কেন যথেষ্ট নয়
* NumPy কী
* `ndarray` কী
* কেন NumPy এত দ্রুত
* Memory কীভাবে বাঁচায়
* কোথায় NumPy ব্যবহার হয়

---

# একটি বাস্তব সমস্যা

ধরো তোমার কাছে ১ কোটি (10,000,000) সংখ্যার একটি তালিকা আছে।

Python List

```python
numbers = [1, 2, 3, 4, 5]
```

এখন প্রতিটি সংখ্যাকে ২ দিয়ে গুণ করতে হবে।

Python-এ সাধারণত লিখবে—

```python
result = []

for n in numbers:
    result.append(n * 2)
```

এখানে কী হচ্ছে?

```
CPU

↓

১ম সংখ্যা

↓

২য় সংখ্যা

↓

৩য় সংখ্যা

↓

...

↓

১০,০০,০০০ তম সংখ্যা
```

একটি করে কাজ করছে।

এটাকে বলে **Loop-based Processing**।

---

# সমস্যা কোথায়?

ধরো

```
10 million numbers
```

তাহলে

```
Loop

↓

10 million iterations
```

Loop যত বড় হবে

↓

সময় তত বাড়বে।

---

# তাহলে সমাধান?

NumPy

```python
import numpy as np

numbers = np.array([1,2,3,4,5])

result = numbers * 2
```

মাত্র একটি লাইন।

---

# এখানে ভিতরে কী হচ্ছে?

তুমি একটি লাইন লিখেছো।

কিন্তু NumPy ভিতরে

```
C Language

↓

Optimized Loop

↓

SIMD Instruction

↓

CPU Cache Optimization
```

ব্যবহার করছে।

অর্থাৎ

তুমি Python লিখছো

↓

কিন্তু কাজ করছে C।

এটাই NumPy-এর সবচেয়ে বড় শক্তি।

---

# NumPy কী?

NumPy = Numerical Python

এটি Python-এর একটি Library।

এটি মূলত

```
Large Numerical Data

+

Fast Computation

+

Matrix Operation

+

Linear Algebra
```

এর জন্য তৈরি।

---

# NumPy কোথায় ব্যবহার হয়?

প্রায় সব Data Science লাইব্রেরি NumPy-এর উপর ভিত্তি করে।

```
NumPy

↓

Pandas

↓

Scikit-learn

↓

TensorFlow

↓

PyTorch

↓

OpenCV

↓

SciPy
```

অর্থাৎ

NumPy না জানলে

পরবর্তী লাইব্রেরিগুলো বোঝা অনেক কঠিন হবে।

---

# NumPy-এর প্রধান Data Structure

NumPy-এর সবচেয়ে গুরুত্বপূর্ণ অবজেক্ট হলো

```
ndarray
```

এর পূর্ণরূপ

```
N-dimensional Array
```

এটি হতে পারে—

### 1D

```
[1 2 3 4]
```

---

### 2D

```
[[1 2]

 [3 4]]
```

---

### 3D

```
[
 [[1 2]
  [3 4]]

 [[5 6]
  [7 8]]
]
```

---

এমনকি

```
4D

5D

10D

100D
```

অ্যারেও NumPy সাপোর্ট করে।

---

# Python List vs NumPy Array

## Python List

```python
numbers = [1,2,3]
```

এর মধ্যে থাকতে পারে

```python
[1, "hello", 5.6, True]
```

অর্থাৎ

একই List-এ

```
int

string

float

bool
```

সব থাকতে পারে।

এটাকে বলে

**Heterogeneous Data**

---

## NumPy Array

```python
arr = np.array([1,2,3])
```

এখানে

সবগুলো একই ধরনের।

```
int

int

int
```

অথবা

```
float

float

float
```

এটাকে বলে

**Homogeneous Data**

---

# কেন একই Data Type দরকার?

ধরো

```
int

int

int

int

int
```

সবগুলোর Size সমান।

CPU খুব সহজে পড়তে পারে।

---

কিন্তু

```
int

string

float

dict

bool
```

প্রতিটি আলাদা।

Memory-তে খুঁজে বের করতে বেশি সময় লাগে।

---

# Memory Layout

Python List

```
Pointer

↓

Object

↓

Pointer

↓

Object

↓

Pointer

↓

Object
```

অর্থাৎ

Memory-তে ছড়িয়ে থাকে।

---

NumPy Array

```
1 2 3 4 5 6 7 8 9
```

একটানা (contiguous) Memory-তে থাকে।

---

CPU Cache খুব দ্রুত পড়তে পারে।

---

# Visual Example

Python List

```
Memory

100

800

250

900

600
```

ডেটা ছড়িয়ে আছে।

---

NumPy

```
100

104

108

112

116

120
```

সব একসাথে।

CPU একবারেই অনেক ডেটা নিয়ে কাজ করতে পারে।

---

# কেন NumPy Fast?

কারণ:

### 1. C Language

Python নয়

↓

C

---

### 2. Contiguous Memory

সব Data পাশাপাশি থাকে।

---

### 3. Same Data Type

সব int

অথবা

সব float

---

### 4. Vectorization

Loop তুমি লিখো না।

NumPy লিখে।

---

### 5. CPU Optimization

SIMD Instruction

Cache Friendly

Low-level Optimization

---

# Real Example

Python

```python
numbers = [1,2,3,4]

result = []

for i in numbers:
    result.append(i * 2)
```

---

NumPy

```python
numbers = np.array([1,2,3,4])

result = numbers * 2
```

একই কাজ।

কম কোড।

বেশি গতি।

---

# কোথায় NumPy ব্যবহার করবে?

## Data Engineering

* Large numeric datasets
* ETL preprocessing
* Feature engineering
* Batch processing

---

## Machine Learning

* Feature matrix
* Labels
* Normalization
* Gradient Descent
* Matrix Multiplication

---

## Computer Vision

Image আসলে

```
Height

×

Width

×

Channel
```

অর্থাৎ

একটি 3D NumPy Array।

---

## Deep Learning

TensorFlow

```
Tensor
```

↓

NumPy-এর ধারণার উপর ভিত্তি করে।

---

PyTorch

```
Tensor
```

↓

NumPy-এর মতোই কাজ করে।

---

# আজকের গুরুত্বপূর্ণ ধারণা

* NumPy = Numerical Python
* প্রধান অবজেক্ট = `ndarray`
* `ndarray` হলো N-dimensional homogeneous array
* NumPy দ্রুত কারণ এটি C-তে ইমপ্লিমেন্টেড, contiguous memory ব্যবহার করে এবং vectorized operations চালায়
* Data Science, ML, Deep Learning, Computer Vision—সব ক্ষেত্রেই NumPy ভিত্তি

---

# Common Mistakes

❌ NumPy Array-কে Python List মনে করা

❌ অপ্রয়োজনীয় `for` loop ব্যবহার করা

❌ NumPy-এর vectorized operation ব্যবহার না করা

❌ `ndarray` এবং Python List-এর পার্থক্য না বোঝা

---

# Interview Questions

1. NumPy কী এবং কেন ব্যবহার করা হয়?
2. Python List এবং NumPy Array-এর মধ্যে প্রধান পার্থক্য কী?
3. `ndarray` কী?
4. NumPy কেন Python List-এর তুলনায় দ্রুত?
5. Homogeneous data বলতে কী বোঝায়?
6. Vectorization কী?
7. Contiguous memory কী এবং কেন গুরুত্বপূর্ণ?

---

# Practice

### সহজ

1. NumPy কী?
2. `ndarray`-এর পূর্ণরূপ কী?
3. Homogeneous data কী?

### মাঝারি

1. Python List কেন বড় numerical computation-এর জন্য ধীর?
2. Contiguous memory কীভাবে performance বাড়ায়?

### কঠিন

নিজের ভাষায় ব্যাখ্যা করো: **কেন Pandas, TensorFlow, PyTorch শেখার আগে NumPy ভালোভাবে শেখা উচিত?**

---

🚀 **কেন Pandas, TensorFlow এবং PyTorch শেখার আগে NumPy ভালোভাবে শেখা উচিত?**

অনেকেই সরাসরি Pandas, TensorFlow বা PyTorch শেখা শুরু করেন। কিন্তু যদি আগে **NumPy**-তে ভালো দক্ষতা অর্জন করেন, তাহলে পরবর্তী শেখার যাত্রা অনেক সহজ ও কার্যকর হবে।

**কেন?**

✅ **১. NumPy হলো Foundation**  
Pandas-এর `DataFrame` এবং `Series` মূলত NumPy array-এর ওপর ভিত্তি করে তৈরি। অন্যদিকে TensorFlow ও PyTorch-এর Tensor ধারণাও NumPy-এর সাথে খুবই মিল।

✅ **২. Faster Mathematical Operations**  
Vectorized operations-এর মাধ্যমে বড় ডেটার ওপর খুব দ্রুত গণনা করা যায়, যা Machine Learning ও Deep Learning-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

✅ **৩. Broadcasting Concept**  
ভিন্ন আকারের array-এর মধ্যে কীভাবে অপারেশন হয়, তা NumPy শেখায়। একই ধারণা TensorFlow এবং PyTorch-এও ব্যবহৃত হয়।

✅ **৪. Linear Algebra-এর ভিত্তি**  
Matrix multiplication, transpose, reshape, dot product—এসবই Machine Learning-এর মৌলিক অংশ, আর NumPy এগুলো শেখার সেরা জায়গা।

✅ **৫. Data Manipulation সহজ হয়**  
Indexing, slicing, filtering, reshaping, concatenation—এসব দক্ষতা Pandas, TensorFlow এবং PyTorch ব্যবহারকে অনেক সহজ করে দেয়।

📚 **Recommended Learning Path:**  
🐍 Python → 🔢 NumPy → 🐼 Pandas → 📊 Matplotlib/Seaborn → 🤖 Scikit-learn → 🧠 TensorFlow/PyTorch

💡 **মনে রাখবেন:** NumPy শেখা বাধ্যতামূলক নয়, তবে এটি আপনার Data Science, Machine Learning এবং Deep Learning শেখার ভিত্তিকে অনেক শক্তিশালী করে।

আপনার শেখার যাত্রা শুরু হলে ভিত্তিটা শক্ত করুন—পরবর্তী সবকিছুই সহজ হয়ে যাবে। 🚀

#Python #NumPy #Pandas #TensorFlow #PyTorch #MachineLearning #DeepLearning #DataScience #Programming #LearningJourney
---
## পরবর্তী লেসন (Lesson 2)

আমরা হাতে-কলমে শুরু করব:

* `import numpy as np`
* `np.array()`
* `np.zeros()`
* `np.ones()`
* `np.empty()`
* `np.eye()`
* `np.arange()`
* `np.linspace()`

এগুলোর প্রতিটি ফাংশন কীভাবে কাজ করে, কখন ব্যবহার করতে হয়, এবং বাস্তব উদাহরণসহ শিখব।
# Module 1 — Lesson 2: Creating Arrays (Hands-on)

আজ থেকে আমরা আসল NumPy ব্যবহার শুরু করব।

এই লেসন শেষে তুমি শিখবে:

* `import numpy as np`
* `np.array()`
* `np.zeros()`
* `np.ones()`
* `np.empty()`
* `np.eye()`
* `np.arange()`
* `np.linspace()`
* কোন ফাংশন কখন ব্যবহার করতে হয়

---

# Learning Objectives

এই লেসন শেষে তুমি পারবে:

* বিভিন্ন ধরনের NumPy array তৈরি করতে
* Shape বুঝতে
* কোন function কেন ব্যবহার করা হয় তা ব্যাখ্যা করতে
* ML/Data Engineering-এ এর ব্যবহার বুঝতে

---

# Step 1: NumPy Import

প্রথমে NumPy import করতে হবে।

```python
import numpy as np
```

এখানে,

* `numpy` = লাইব্রেরির নাম
* `np` = alias (সংক্ষিপ্ত নাম)

এখন আমরা লিখতে পারি:

```python
np.array(...)
```

পরিবর্তে

```python
numpy.array(...)
```

এটা Python community-এর standard convention।

---

# Step 2: `np.array()`

এটাই সবচেয়ে গুরুত্বপূর্ণ function।

Syntax:

```python
np.array(object)
```

Example:

```python
import numpy as np

numbers = np.array([10, 20, 30, 40])

print(numbers)
```

Output:

```python
[10 20 30 40]
```

---

## ভিতরে কী হলো?

Python List

```python
[10, 20, 30, 40]
```

↓

NumPy

```python
array([10,20,30,40])
```

↓

`ndarray`

---

## Type Check

```python
type(numbers)
```

Output

```python
numpy.ndarray
```

এটা আর List না।

---

# Creating a 2D Array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(matrix)
```

Output

```python
[[1 2 3]
 [4 5 6]]
```

এটা হলো

```
2 rows

3 columns
```

---

# Creating a 3D Array

```python
cube = np.array([
    [
        [1,2],
        [3,4]
    ],
    [
        [5,6],
        [7,8]
    ]
])
```

Visual

```
Layer 1

1 2
3 4

Layer 2

5 6
7 8
```

---

# Step 3: `np.zeros()`

ধরো তুমি ML model-এর জন্য একটি খালি matrix বানাতে চাও।

Syntax

```python
np.zeros(shape)
```

Example

```python
arr = np.zeros((3,4))

print(arr)
```

Output

```python
[[0. 0. 0. 0.]
 [0. 0. 0. 0.]
 [0. 0. 0. 0.]]
```

খেয়াল করো

```
0.0
```

Float তৈরি হয়েছে।

---

## Integer Zeros

```python
arr = np.zeros((3,4), dtype=int)

print(arr)
```

Output

```python
[[0 0 0 0]
 [0 0 0 0]
 [0 0 0 0]]
```

---

## বাস্তব ব্যবহার

* Initialize weight matrix
* Empty image
* Feature matrix
* Placeholder data

---

# Step 4: `np.ones()`

সব জায়গায় ১ বসাবে।

```python
arr = np.ones((2,5))

print(arr)
```

Output

```python
[[1. 1. 1. 1. 1.]
 [1. 1. 1. 1. 1.]]
```

Integer

```python
np.ones((2,5), dtype=int)
```

---

## কোথায় ব্যবহার হয়?

* Initial mask
* Default values
* Testing
* Matrix operations

---

# Step 5: `np.empty()`

অনেকেই ভুল বোঝে।

```python
arr = np.empty((3,3))

print(arr)
```

Output হতে পারে

```python
[[4.65e-310 0.00e+000 6.92e-310]
 [6.92e-310 6.92e-310 4.65e-310]
 [0.00e+000 6.92e-310 4.65e-310]]
```

অথবা অন্য কিছু।

---

## কেন?

`empty()` কোনো value initialize করে না।

Memory-তে যা আগে ছিল, তাই দেখায়।

তাই

```
empty ≠ zeros
```

---

## সুবিধা

খুব দ্রুত।

কারণ

```
Memory Allocate

↓

Done
```

কোনো initialization নেই।

---

# Step 6: `np.eye()`

Identity Matrix তৈরি করে।

```python
identity = np.eye(4)

print(identity)
```

Output

```python
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]]
```

---

## কোথায় ব্যবহার হয়?

Linear Algebra

Deep Learning

Matrix Multiplication

Computer Vision

---

# Step 7: `np.arange()`

Python-এর `range()`-এর মতো।

Syntax

```python
np.arange(start, stop, step)
```

Example

```python
arr = np.arange(10)

print(arr)
```

Output

```python
[0 1 2 3 4 5 6 7 8 9]
```

---

Example

```python
np.arange(2,10)
```

Output

```python
[2 3 4 5 6 7 8 9]
```

---

Example

```python
np.arange(0,20,2)
```

Output

```python
[0 2 4 6 8 10 12 14 16 18]
```

---

## Negative Step

```python
np.arange(10,0,-1)
```

Output

```python
[10 9 8 7 6 5 4 3 2 1]
```

---

# Step 8: `np.linspace()`

এটা interview-এ খুবই গুরুত্বপূর্ণ।

Syntax

```python
np.linspace(start, stop, num)
```

এখানে

`num`

মানে

কতটি সংখ্যা চাই।

---

Example

```python
arr = np.linspace(0,10,5)

print(arr)
```

Output

```python
[0.  2.5  5.  7.5 10.]
```

খেয়াল করো

```
শেষ সংখ্যাও (10) অন্তর্ভুক্ত হয়েছে।
```

---

আরেকটি উদাহরণ

```python
np.linspace(1,100,10)
```

Output

```python
[  1.  12.  23.  34.  45.  56.  67.  78.  89. 100.]
```

---

# `arange()` vs `linspace()`

| Function     | কী নির্ধারণ করো? | Stop Included? |
| ------------ | ---------------- | -------------- |
| `arange()`   | Step size        | ❌ না           |
| `linspace()` | Number of values | ✅ হ্যাঁ        |

উদাহরণ:

```python
np.arange(0, 10, 2)
```

```
Step = 2
```

↓

```python
[0 2 4 6 8]
```

---

```python
np.linspace(0,10,6)
```

```
6টি সংখ্যা
```

↓

```python
[0. 2. 4. 6. 8. 10.]
```

---

# Data Type নির্ধারণ

```python
arr = np.array([1,2,3], dtype=np.float32)

print(arr)
print(arr.dtype)
```

Output

```python
[1. 2. 3.]
float32
```

---

# Real ML Example

ধরো তোমার কাছে 100টি Feature আছে।

সবগুলো শুরুতে 0।

```python
weights = np.zeros(100)
```

---

Image তৈরি

```python
image = np.zeros((720,1280,3), dtype=np.uint8)
```

এটি একটি কালো RGB Image।

---

Identity Matrix

```python
I = np.eye(5)
```

Machine Learning-এ Regularization এবং Linear Algebra-তে ব্যবহৃত হয়।

---

# Common Mistakes

❌

```python
np.zeros(3,4)
```

সঠিক:

```python
np.zeros((3,4))
```

কারণ `shape` একটি tuple।

---

❌

```python
np.arange(0,10,0)
```

Step কখনো 0 হতে পারে না।

---

❌

`empty()` কে `zeros()` মনে করা।

---

# Practice Problems

### Easy

1.

```python
[1,2,3,4,5]
```

থেকে NumPy Array বানাও।

2.

4×4 zeros matrix তৈরি করো।

3.

3×5 ones matrix তৈরি করো।

---

### Medium

1.

১০ থেকে ১০০ পর্যন্ত জোড় সংখ্যা তৈরি করো।

2.

5×5 Identity Matrix তৈরি করো।

3.

০ থেকে ১ পর্যন্ত ১১টি সমান দূরত্বের সংখ্যা তৈরি করো।

---

### Hard

শুধু NumPy ব্যবহার করে নিচের output তৈরি করো:

```text
[[0 0 0 0]
 [0 0 0 0]
 [0 0 0 0]]

[[1 1 1 1]
 [1 1 1 1]
 [1 1 1 1]]

[10 20 30 40 50]

[0.   0.25 0.50 0.75 1.00]
```

---

# Interview Questions

1. `np.array()` এবং Python List-এর মধ্যে পার্থক্য কী?
2. `np.zeros()` এবং `np.empty()`-এর মধ্যে পার্থক্য কী?
3. `np.arange()` এবং `np.linspace()`-এর মধ্যে পার্থক্য কী?
4. `np.eye()` কোথায় ব্যবহার হয়?
5. `dtype` কেন গুরুত্বপূর্ণ?

---

## Lesson 2 Summary

আজ আমরা শিখলাম:

* ✅ `np.array()` — Python list থেকে `ndarray` তৈরি
* ✅ `np.zeros()` — শূন্য দিয়ে array initialize
* ✅ `np.ones()` — এক দিয়ে array initialize
* ✅ `np.empty()` — initialization ছাড়া দ্রুত memory allocate
* ✅ `np.eye()` — identity matrix তৈরি
* ✅ `np.arange()` — step অনুযায়ী সংখ্যা তৈরি
* ✅ `np.linspace()` — নির্দিষ্ট সংখ্যক সমান দূরত্বের মান তৈরি
* ✅ `dtype` ব্যবহার করে data type নিয়ন্ত্রণ

**পরবর্তী Lesson 3**-এ আমরা `ndarray`-এর anatomy শিখব—`shape`, `ndim`, `size`, `dtype`, `itemsize`, `nbytes` ইত্যাদি, যাতে তুমি যেকোনো array-এর গঠন মুহূর্তেই বুঝতে পারো।


# Module 1 — Lesson 3: Understanding `ndarray` Attributes (Anatomy of an Array)

আজকের লেসনটি খুবই গুরুত্বপূর্ণ। একজন **Data Engineer** বা **ML Engineer** হিসেবে যখনই কোনো dataset বা model input নিয়ে কাজ করবে, প্রথমেই তুমি array-এর এই attributes গুলো চেক করবে।

**Rule of thumb:**

> **প্রথমে array বুঝো, তারপর operation করো।**

---

# Learning Objectives

এই লেসনের শেষে তুমি জানতে পারবে:

* `shape`
* `ndim`
* `size`
* `dtype`
* `itemsize`
* `nbytes`

এগুলো কী এবং কেন গুরুত্বপূর্ণ।

---

# Step 1: একটি Array তৈরি করি

```python
import numpy as np

arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(arr)
```

Output

```text
[[10 20 30]
 [40 50 60]]
```

Visual:

```text
        Column
        0   1   2
      +---+---+---+
Row 0 |10 |20 |30 |
      +---+---+---+
Row 1 |40 |50 |60 |
      +---+---+---+
```

এখানে

* Rows = 2
* Columns = 3

---

# 1. `shape`

```python
print(arr.shape)
```

Output

```python
(2, 3)
```

### এর মানে কী?

```text
(2,3)

↓

2 Rows

3 Columns
```

`shape` সবসময় **tuple** return করে।

---

### আরও উদাহরণ

### 1D

```python
a = np.array([1,2,3,4])

print(a.shape)
```

Output

```python
(4,)
```

খেয়াল করো

শেষে comma আছে।

কারণ এটা Python tuple।

---

### 3D Array

```python
cube = np.zeros((2,3,4))

print(cube.shape)
```

Output

```python
(2,3,4)
```

মানে

```text
2 Layers

↓

3 Rows

↓

4 Columns
```

---

# Shape কেন গুরুত্বপূর্ণ?

ধরো

```python
A = np.zeros((5,3))
```

আর

```python
B = np.zeros((5,4))
```

তুমি

```python
A + B
```

করতে পারবে?

না।

কারণ shape match করছে না।

---

Machine Learning-এ অনেক error-এর কারণ:

```text
Shape Mismatch
```

---

# 2. `ndim`

মানে

```text
Number of Dimensions
```

Example

```python
print(arr.ndim)
```

Output

```python
2
```

কারণ

```text
Rows

Columns
```

দুটি dimension আছে।

---

### আরও উদাহরণ

```python
a = np.array([1,2,3])

print(a.ndim)
```

Output

```python
1
```

---

```python
cube = np.zeros((3,4,5))

print(cube.ndim)
```

Output

```python
3
```

---

Visual

```text
1D

[1 2 3]

↓

ndim = 1
```

---

```text
2D

1 2

3 4

↓

ndim = 2
```

---

```text
3D

Layer 1

Layer 2

↓

ndim = 3
```

---

# 3. `size`

মোট কতটি element আছে?

```python
print(arr.size)
```

Output

```python
6
```

কারণ

```text
10

20

30

40

50

60
```

মোট ৬টি সংখ্যা।

---

Formula

```text
size

=

Rows × Columns
```

---

আরও উদাহরণ

```python
cube = np.zeros((2,3,4))
```

Size

```text
2×3×4

=

24
```

```python
print(cube.size)
```

Output

```python
24
```

---

# 4. `dtype`

Data Type

```python
print(arr.dtype)
```

Output

```python
int64
```

(তোমার operating system অনুযায়ী `int32`-ও হতে পারে।)

---

Float Example

```python
a = np.array([1.2, 5.6])

print(a.dtype)
```

Output

```python
float64
```

---

Boolean

```python
b = np.array([True, False])

print(b.dtype)
```

Output

```python
bool
```

---

### কেন গুরুত্বপূর্ণ?

Machine Learning-এ

```text
float32
```

সবচেয়ে বেশি ব্যবহার হয়।

কারণ

* কম memory লাগে
* GPU-তে দ্রুত কাজ করে

---

# 5. `itemsize`

একটি element কত byte নিচ্ছে?

```python
print(arr.itemsize)
```

Output

```python
8
```

কারণ

```text
int64

↓

64 bit

↓

8 byte
```

---

Float32

```python
a = np.array([1,2,3], dtype=np.float32)

print(a.itemsize)
```

Output

```python
4
```

কারণ

```text
32 bit

=

4 byte
```

---

# 6. `nbytes`

মোট memory usage

Formula

```text
nbytes

=

size × itemsize
```

Example

```python
print(arr.nbytes)
```

Output

```python
48
```

কারণ

```text
6 elements

×

8 bytes

=

48 bytes
```

---

আরও উদাহরণ

```python
a = np.zeros((1000,1000))
```

Shape

```text
1000 ×1000
```

↓

Size

```text
1,000,000
```

↓

Itemsize

```text
8
```

↓

Memory

```text
8,000,000 bytes

≈7.63 MB
```

---

# সব Attributes একসাথে

```python
import numpy as np

arr = np.array([
    [10,20,30],
    [40,50,60]
])

print("Shape:", arr.shape)
print("Dimension:", arr.ndim)
print("Size:", arr.size)
print("Datatype:", arr.dtype)
print("Item Size:", arr.itemsize)
print("Memory:", arr.nbytes)
```

Output

```text
Shape: (2, 3)
Dimension: 2
Size: 6
Datatype: int64
Item Size: 8
Memory: 48
```

---

# একটি গুরুত্বপূর্ণ Interview Question

ধরো

```python
a = np.zeros((5,4))
```

না চালিয়ে বলো—

### Shape?

```text
(5,4)
```

### Dimension?

```text
2
```

### Size?

```text
20
```

### যদি dtype = float64 হয়

Itemsize?

```text
8
```

Memory?

```text
20 × 8

=

160 bytes
```

---

# Real Data Engineering Example

ধরো CSV থেকে data load করলে:

```python
data = np.loadtxt("sales.csv", delimiter=",")
```

প্রথমে কী করবে?

```python
print(data.shape)
print(data.dtype)
print(data.ndim)
```

এতে সঙ্গে সঙ্গে বুঝবে:

* কত rows
* কত columns
* data numeric কিনা
* model-এ দেওয়ার উপযোগী কিনা

---

# Common Mistakes

### ❌ `shape` এবং `size` গুলিয়ে ফেলা

```text
shape = structure

size = total elements
```

---

### ❌ `ndim` কে `size` মনে করা

```text
ndim = কতটি dimension

size = কতটি value
```

---

### ❌ `itemsize` এবং `nbytes` এক মনে করা

```text
itemsize

↓

একটি element

```

```text
nbytes

↓

পুরো array
```

---

# Practice

## Easy

1.

```python
a = np.array([1,2,3,4,5])
```

Find:

* shape
* ndim
* size

---

2.

```python
b = np.zeros((3,4))
```

Find:

* shape
* size
* ndim

---

## Medium

```python
a = np.ones((4,5,6))
```

না চালিয়ে বলো

* shape
* ndim
* size

---

## Hard

```python
a = np.zeros((20,30), dtype=np.float32)
```

না চালিয়ে বলো

* size
* itemsize
* nbytes

---

# Interview Questions

1. `shape` এবং `size`-এর পার্থক্য কী?
2. `ndim` কী?
3. `itemsize` কী?
4. `nbytes` কীভাবে গণনা করা হয়?
5. `float32` কেন `float64`-এর চেয়ে কম memory ব্যবহার করে?
6. কেন ML-এ `float32` বেশি ব্যবহৃত হয়?

---

# Cheat Sheet

| Attribute  | Meaning                           | Example Output |
| ---------- | --------------------------------- | -------------- |
| `shape`    | Array-এর গঠন (rows, columns, ...) | `(2, 3)`       |
| `ndim`     | Dimension-এর সংখ্যা               | `2`            |
| `size`     | মোট element                       | `6`            |
| `dtype`    | Data type                         | `int64`        |
| `itemsize` | প্রতি element-এর byte             | `8`            |
| `nbytes`   | মোট memory usage                  | `48`           |

---

## Assignment (Production Mindset)

নিচের কোডটি লিখে **প্রতিটি output কী হবে, আগে অনুমান করো**, তারপর Python-এ চালিয়ে মিলিয়ে দেখো।

```python
import numpy as np

arr = np.arange(1, 13).reshape(3, 4)

print(arr)
print("Shape:", arr.shape)
print("Dimension:", arr.ndim)
print("Size:", arr.size)
print("Datatype:", arr.dtype)
print("Item Size:", arr.itemsize)
print("Memory:", arr.nbytes)
```

> **আগে predict, পরে run**—এটি একজন ভালো Engineer-এর অভ্যাস।

### পরবর্তী Lesson 4

আমরা শিখব **NumPy Data Types (`dtype`)** গভীরভাবে:

* `int8`, `int16`, `int32`, `int64`
* `float16`, `float32`, `float64`
* `bool`
* `astype()`
* Memory optimization techniques
* Production ML-এ কোন `dtype` কখন ব্যবহার করতে হয়।

# Module 1 — Lesson 4: NumPy Data Types (`dtype`) Mastery

আজকের Lesson খুবই গুরুত্বপূর্ণ।

অনেক Junior Developer শুধুমাত্র `int` আর `float` জানে। কিন্তু একজন **Data Engineer** বা **ML Engineer**-কে জানতে হবে **কোন data type কখন ব্যবহার করলে memory কম লাগবে, computation দ্রুত হবে, এবং overflow এড়ানো যাবে।**

---

# Learning Objectives

এই Lesson শেষে তুমি জানতে পারবে:

* `dtype` কী?
* `int8`, `int16`, `int32`, `int64`
* `float16`, `float32`, `float64`
* `bool`
* `astype()`
* Type Conversion
* Overflow
* Memory Optimization

---

# `dtype` কী?

`dtype` = **Data Type**

এটি বলে দেয় array-এর প্রতিটি element কী ধরনের data।

```python
import numpy as np

arr = np.array([10, 20, 30])

print(arr.dtype)
```

Output

```text
int64
```

---

# NumPy কেন Data Type ব্যবহার করে?

ধরো তোমার কাছে ১ কোটি সংখ্যা আছে।

যদি প্রতিটি সংখ্যা ৮ byte নেয়,

তাহলে

```text
10,000,000 × 8

=

80 MB
```

কিন্তু যদি ২ byte-এ রাখা যায়?

```text
10,000,000 × 2

=

20 MB
```

**৬০ MB memory বাঁচল।**

Production-এ এটা বিশাল পার্থক্য।

---

# Integer Types

| Type  | Bytes |               Range |
| ----- | ----: | ------------------: |
| int8  |     1 |          -128 → 127 |
| int16 |     2 |      -32768 → 32767 |
| int32 |     4 | প্রায় ±2.1 Billion |
| int64 |     8 |      খুব বড় সংখ্যা |

---

## int8

```python
a = np.array([10, 20, 30], dtype=np.int8)

print(a)
print(a.dtype)
```

Output

```text
[10 20 30]

int8
```

---

## int16

```python
a = np.array([1000, 2000], dtype=np.int16)
```

---

## int32

```python
a = np.array([100000], dtype=np.int32)
```

---

## int64

```python
a = np.array([999999999999], dtype=np.int64)
```

---

# Memory Comparison

```python
a = np.array([1], dtype=np.int8)

print(a.itemsize)
```

Output

```text
1
```

---

```python
a = np.array([1], dtype=np.int64)

print(a.itemsize)
```

Output

```text
8
```

---

Visual

```text
int8

□
```

```text
int64

□□□□□□□□
```

একটি element-এর জন্য ৮ গুণ memory লাগছে।

---

# Floating Point Types

| Type    | Bytes |
| ------- | ----: |
| float16 |     2 |
| float32 |     4 |
| float64 |     8 |

---

## float16

```python
a = np.array([3.14], dtype=np.float16)
```

কম memory

কম precision

---

## float32

```python
a = np.array([3.14], dtype=np.float32)
```

Deep Learning-এ সবচেয়ে বেশি ব্যবহৃত।

---

## float64

```python
a = np.array([3.14], dtype=np.float64)
```

বেশি precision

বেশি memory

---

# Precision

```python
a = np.array([1.123456789], dtype=np.float16)

print(a)
```

Output (আনুমানিক)

```text
1.123
```

---

```python
a = np.array([1.123456789], dtype=np.float64)

print(a)
```

Output

```text
1.123456789
```

---

# Boolean

```python
mask = np.array([True, False, True])

print(mask.dtype)
```

Output

```text
bool
```

---

Boolean Indexing-এ পরে এটি অনেক ব্যবহার হবে।

---

# String

```python
names = np.array(["Ali", "Rahim", "Karim"])

print(names.dtype)
```

Output (উদাহরণ)

```text
<U5
```

এর মানে Unicode String।

---

# Automatic Type Inference

NumPy নিজে data type নির্ধারণ করতে পারে।

```python
a = np.array([1, 2, 3])

print(a.dtype)
```

↓

```text
int64
```

---

```python
b = np.array([1.2, 3.4])

print(b.dtype)
```

↓

```text
float64
```

---

Mixed Data

```python
c = np.array([1, 2.5, 3])

print(c.dtype)
```

↓

```text
float64
```

কারণ

```text
int

↓

float
```

Promotion হয়েছে।

---

আরেকটি উদাহরণ

```python
d = np.array([1, True])
```

Output

```text
int64
```

কারণ

```text
True

=

1
```

---

# Type Conversion

এটি Interview-এ অনেক আসে।

```python
a = np.array([1,2,3])

b = a.astype(np.float32)

print(b.dtype)
```

Output

```text
float32
```

---

আরও উদাহরণ

```python
a = np.array([1.8, 2.9, 3.5])

b = a.astype(np.int32)

print(b)
```

Output

```text
[1 2 3]
```

**দশমিক অংশ কেটে যায় (truncate হয়)।**

---

# Memory Optimization

ধরো

```python
a = np.arange(1000000)
```

Default

```text
int64
```

Memory

```python
print(a.nbytes)
```

↓

```text
8000000
```

---

Convert

```python
b = a.astype(np.int16)
```

↓

Memory

```python
print(b.nbytes)
```

↓

```text
2000000
```

**৭৫% memory কমে গেল।**

---

# Overflow

এটি খুব গুরুত্বপূর্ণ।

```python
a = np.array([127], dtype=np.int8)

print(a + 1)
```

Output

```text
[-128]
```

**কেন?**

কারণ

`int8`

```text
Maximum

127
```

তার বেশি রাখা যায় না।

তাই আবার minimum-এ চলে যায়।

এটাকে বলে

**Overflow**।

---

# Real Machine Learning Example

Images

```python
image = np.zeros((720,1280,3), dtype=np.uint8)
```

কেন `uint8`?

কারণ Pixel Value

```text
0

↓

255
```

এর বেশি লাগে না।

---

Deep Learning

```python
features = np.array(data, dtype=np.float32)
```

কেন?

* কম memory
* GPU friendly
* দ্রুত computation

---

# Common Mistakes

## ❌ Memory না ভেবে সব `float64` ব্যবহার করা।

---

## ❌ `astype()` original array পরিবর্তন করে মনে করা।

```python
a.astype(np.float32)
```

এটি **নতুন array** return করে।

---

## ❌ Overflow সম্পর্কে না জানা।

---

# Practice

## Easy

### 1

```python
a = np.array([1,2,3], dtype=np.int16)
```

Find:

* dtype
* itemsize

---

### 2

```python
b = np.array([1.2,3.5], dtype=np.float32)
```

Find:

* dtype
* itemsize

---

## Medium

Convert

```python
a = np.array([1,2,3])
```

↓

float32

↓

int8

---

## Hard

```python
a = np.arange(1000000)
```

Calculate

* Default memory
* After `astype(np.int16)`
* কত memory save হলো?

---

# Interview Questions

1. `dtype` কী?
2. `float32` এবং `float64`-এর পার্থক্য কী?
3. `astype()` কী করে?
4. `int8`-এর range কত?
5. Overflow কী?
6. Deep Learning-এ `float32` কেন জনপ্রিয়?
7. `uint8` কোথায় ব্যবহার হয়?

---

# Cheat Sheet

| Type      | Bytes | সাধারণ ব্যবহার                      |
| --------- | ----: | ----------------------------------- |
| `int8`    |     1 | ছোট integer                         |
| `int16`   |     2 | মাঝারি integer                      |
| `int32`   |     4 | সাধারণ integer                      |
| `int64`   |     8 | বড় integer (default অনেক সিস্টেমে) |
| `float16` |     2 | Low precision                       |
| `float32` |     4 | ML / GPU                            |
| `float64` |     8 | Scientific computing                |
| `bool`    |     1 | Masking / Boolean indexing          |
| `uint8`   |     1 | Images (0–255)                      |

---

# Mini Challenge

নিচের কোডটি **run করার আগে output predict করো**:

```python
import numpy as np

a = np.array([1, 2, 3], dtype=np.int16)

print(a.dtype)
print(a.itemsize)

b = a.astype(np.float32)

print(b.dtype)
print(b.itemsize)

c = np.array([127], dtype=np.int8)

print(c + 1)
```

যদি তুমি প্রতিটি output সঠিকভাবে predict করতে পারো, তাহলে `dtype` বিষয়টি ভালোভাবে বুঝতে শুরু করেছ।

---

## পরবর্তী Lesson 5

এবার আমরা **Array Arithmetic & Universal Functions (UFuncs)** শিখব:

* `+`, `-`, `*`, `/`
* `**`
* `//`
* `%`
* `np.sqrt()`
* `np.exp()`
* `np.log()`
* `np.sin()`, `np.cos()`
* Vectorization (কেন NumPy loop ছাড়া দ্রুত কাজ করে)
# Module 2 — Lesson 5: Array Arithmetic & Universal Functions (UFuncs)

এটি NumPy-এর সবচেয়ে শক্তিশালী ফিচারগুলোর একটি।

আজকের Lesson শেষে তুমি বুঝবে কেন Data Scientist বা ML Engineer-রা **প্রায় কখনোই `for` loop ব্যবহার করেন না** যখন NumPy দিয়ে numerical computation করেন।

---

# Learning Objectives

আজ আমরা শিখব:

* Arithmetic Operations
* Broadcasting-এর প্রাথমিক ধারণা
* Universal Functions (UFuncs)
* Vectorization
* Mathematical Functions
* Performance Mindset

---

# What is Vectorization?

ধরো, আমাদের প্রতিটি সংখ্যাকে 10 দিয়ে গুণ করতে হবে।

### Python Way

```python
numbers = [1, 2, 3, 4, 5]

result = []

for n in numbers:
    result.append(n * 10)

print(result)
```

Output

```text
[10, 20, 30, 40, 50]
```

এখানে loop একবারে একটি element নিয়ে কাজ করছে।

---

### NumPy Way

```python
import numpy as np

numbers = np.array([1, 2, 3, 4, 5])

result = numbers * 10

print(result)
```

Output

```text
[10 20 30 40 50]
```

**কোনো loop লিখতে হলো না।**

এটিই **Vectorization**।

> **Definition:** একাধিক element-এর উপর একসাথে operation চালানোকে Vectorization বলে।

---

# Element-wise Operation

দুটি array:

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
```

Visualization:

```text
a = [1 2 3]
b = [4 5 6]
```

---

## Addition

```python
print(a + b)
```

Output

```text
[5 7 9]
```

কী হলো?

```text
1 + 4 = 5

2 + 5 = 7

3 + 6 = 9
```

---

## Subtraction

```python
print(a - b)
```

Output

```text
[-3 -3 -3]
```

---

## Multiplication

```python
print(a * b)
```

Output

```text
[4 10 18]
```

⚠️ **এটি Matrix Multiplication নয়।**

এটি **Element-wise Multiplication**।

---

## Division

```python
print(a / b)
```

Output

```text
[0.25 0.4 0.5]
```

---

## Floor Division

```python
print(b // a)
```

Output

```text
[4 2 2]
```

---

## Modulus

```python
print(b % a)
```

Output

```text
[0 1 0]
```

---

## Power

```python
print(a ** 2)
```

Output

```text
[1 4 9]
```

---

আরও উদাহরণ

```python
print(a ** 3)
```

Output

```text
[1 8 27]
```

---

# Scalar Operations

Scalar মানে একটি মাত্র সংখ্যা।

```python
a = np.array([1,2,3])
```

---

## Add Scalar

```python
print(a + 5)
```

Output

```text
[6 7 8]
```

---

## Multiply Scalar

```python
print(a * 100)
```

Output

```text
[100 200 300]
```

---

## Divide

```python
print(a / 2)
```

Output

```text
[0.5 1.0 1.5]
```

---

Visual

```text
[1 2 3]

+

5

↓

[6 7 8]
```

NumPy নিজেই প্রতিটি element-এ `5` যোগ করেছে।

---

# Universal Functions (UFuncs)

NumPy-তে অনেক built-in mathematical function আছে।

এগুলোকেই বলে **Universal Functions (UFuncs)**।

এগুলো **element-wise** কাজ করে।

---

# Square Root

```python
a = np.array([1, 4, 9, 16])

print(np.sqrt(a))
```

Output

```text
[1. 2. 3. 4.]
```

---

# Exponential

```python
a = np.array([1,2,3])

print(np.exp(a))
```

Output (প্রায়)

```text
[ 2.718  7.389 20.085]
```

এখানে `exp(x)` = (e^x)

---

# Logarithm

```python
a = np.array([1, 10, 100])

print(np.log(a))
```

Output (Natural Log)

```text
[0.      2.3025 4.6051]
```

---

## Base-10 Log

```python
print(np.log10(a))
```

Output

```text
[0. 1. 2.]
```

---

# Absolute Value

```python
a = np.array([-5,-2,3])

print(np.abs(a))
```

Output

```text
[5 2 3]
```

---

# Square

```python
a = np.array([2,3,4])

print(np.square(a))
```

Output

```text
[4 9 16]
```

এটি

```python
a ** 2
```

এর সমান।

---

# Trigonometric Functions

## Sin

```python
angles = np.array([0, np.pi/2])

print(np.sin(angles))
```

Output

```text
[0. 1.]
```

---

## Cos

```python
print(np.cos(angles))
```

Output

```text
[1. 0.]
```

---

# Round

```python
a = np.array([1.2345, 3.9876])

print(np.round(a, 2))
```

Output

```text
[1.23 3.99]
```

---

# Maximum

```python
a = np.array([1,5,9])

b = np.array([3,4,2])

print(np.maximum(a,b))
```

Output

```text
[3 5 9]
```

---

# Minimum

```python
print(np.minimum(a,b))
```

Output

```text
[1 4 2]
```

---

# Why UFuncs are Fast?

ধরো

```python
for i in range(10000000):
    ...
```

Python

↓

10 Million Loop

↓

Slow

---

NumPy

```python
array * 5
```

↓

C Loop

↓

SIMD

↓

Fast

---

# Real Machine Learning Example

ধরো Pixel Value

```text
0 → 255
```

Model-এ দেওয়ার আগে Normalize করতে হবে।

```python
image = image / 255.0
```

এক লাইনে পুরো image normalize হয়ে গেল।

---

আরও উদাহরণ

ধরো Salary বাড়াতে হবে ১০%।

```python
salary = np.array([30000, 45000, 50000])

new_salary = salary * 1.10

print(new_salary)
```

Output

```text
[33000. 49500. 55000.]
```

---

# Common Mistakes

## ❌ Matrix Multiplication ভেবে নেওয়া

```python
a * b
```

এটি Matrix Multiplication নয়।

এটি Element-wise Multiplication।

Matrix Multiplication পরে শিখব (`@`, `np.dot()`).

---

## ❌ Different Shape

```python
a = np.array([1,2,3])

b = np.array([1,2])

print(a+b)
```

Error

```text
ValueError
```

(কিছু ক্ষেত্রে Broadcasting কাজ করবে, যা আমরা পরে বিস্তারিত শিখব।)

---

# Practice

## Easy

```python
a = np.array([2,4,6])

b = np.array([1,2,3])
```

Find:

1.

```python
a+b
```

2.

```python
a-b
```

3.

```python
a*b
```

---

## Medium

```python
a = np.array([4,9,16,25])
```

Find:

* Square Root
* Square
* Log

---

## Hard

ধরো

```python
salary = np.array([
    25000,
    40000,
    60000,
    80000
])
```

করতে হবে

* ১৫% বৃদ্ধি
* তারপর ৫% tax কাটা
* শেষে nearest integer-এ round করা

ইঙ্গিত:

```python
salary = salary * 1.15
salary = salary * 0.95
salary = np.round(salary)
```

---

# Interview Questions

1. Vectorization কী?
2. NumPy কেন Loop-এর চেয়ে দ্রুত?
3. UFunc কী?
4. `a * b` কী ধরনের multiplication?
5. `np.sqrt()` কী করে?
6. `np.log()` এবং `np.log10()`-এর পার্থক্য কী?
7. `np.maximum()` এবং `max()`-এর পার্থক্য কী?

---

# Cheat Sheet

| Operation      | Example            |
| -------------- | ------------------ |
| Addition       | `a + b`            |
| Subtraction    | `a - b`            |
| Multiplication | `a * b`            |
| Division       | `a / b`            |
| Floor Division | `a // b`           |
| Modulus        | `a % b`            |
| Power          | `a ** 2`           |
| Square Root    | `np.sqrt(a)`       |
| Exponential    | `np.exp(a)`        |
| Natural Log    | `np.log(a)`        |
| Base-10 Log    | `np.log10(a)`      |
| Absolute       | `np.abs(a)`        |
| Square         | `np.square(a)`     |
| Sin            | `np.sin(a)`        |
| Cos            | `np.cos(a)`        |
| Round          | `np.round(a, 2)`   |
| Maximum        | `np.maximum(a, b)` |
| Minimum        | `np.minimum(a, b)` |

---

# Assignment (Production Mindset)

একটি e-commerce store-এর product price array আছে:

```python
import numpy as np

prices = np.array([1200, 2500, 5000, 8000])
```

নিচের কাজগুলো **কোনো `for` loop ছাড়া** করো:

1. সব product-এর উপর ১০% discount দাও।
2. Discount-এর পর ১৫% VAT যোগ করো।
3. Final price-কে ২ decimal place পর্যন্ত round করো।
4. 3000 টাকার বেশি product-গুলোর final price আলাদা array হিসেবে বের করো (ইঙ্গিত: Boolean indexing — এটি আমরা পরের লেসনে বিস্তারিত শিখব)।

---

## পরবর্তী Lesson 6

আমরা শিখব **Comparison Operations & Boolean Arrays**:

* `>`, `<`, `>=`, `<=`, `==`, `!=`
* Boolean Array
* Boolean Mask
* Filtering Data
* Real-world Data Cleaning
* Feature Selection
* Pandas Filtering-এর ভিত্তি

এই লেসনের পর তুমি NumPy দিয়ে data filter করতে পারবে, যা Data Engineering এবং Machine Learning-এ প্রতিদিন ব্যবহৃত হয়।



# Module 2 — Lesson 6: Comparison Operations & Boolean Arrays

আজকের Lesson **Data Engineer** এবং **ML Engineer**-দের জন্য সবচেয়ে বেশি ব্যবহৃত বিষয়গুলোর একটি।

বাস্তব প্রজেক্টে আমরা প্রায়ই এমন প্রশ্ন করি:

* কোন salary 50,000-এর বেশি?
* কোন student pass করেছে?
* কোন pixel 128-এর বেশি?
* কোন customer VIP?
* কোন transaction fraud হতে পারে?

এই সবকিছুর ভিত্তি হলো **Boolean Arrays**।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে:

* Comparison Operators ব্যবহার করতে
* Boolean Array বুঝতে
* Boolean Mask তৈরি করতে
* Data Filter করতে
* Multiple Condition ব্যবহার করতে

---

# Step 1: Comparison Operators

প্রথমে একটি Array তৈরি করি।

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50])
```

Visual

```text
Index : 0   1   2   3   4
Value :10  20  30  40  50
```

---

# Greater Than (`>`)

```python
print(a > 25)
```

Output

```python
[False False  True  True  True]
```

Visual

```text
10 > 25 ❌

20 > 25 ❌

30 > 25 ✅

40 > 25 ✅

50 > 25 ✅
```

---

# Less Than (`<`)

```python
print(a < 30)
```

Output

```python
[ True  True False False False]
```

---

# Greater Than or Equal (`>=`)

```python
print(a >= 30)
```

Output

```python
[False False True True True]
```

---

# Less Than or Equal (`<=`)

```python
print(a <= 20)
```

Output

```python
[ True True False False False]
```

---

# Equal (`==`)

```python
print(a == 30)
```

Output

```python
[False False True False False]
```

---

# Not Equal (`!=`)

```python
print(a != 30)
```

Output

```python
[ True True False True True]
```

---

# Boolean Array

খেয়াল করো—

Comparison-এর result কখনো number না।

সবসময়

```text
True

False
```

এগুলোই Boolean Array।

```python
mask = a > 25

print(mask)
```

Output

```python
[False False True True True]
```

Type দেখো

```python
print(mask.dtype)
```

Output

```python
bool
```

---

# Boolean Mask কী?

Boolean Array-কে যখন filtering-এর জন্য ব্যবহার করা হয়, তখন তাকে **Boolean Mask** বলা হয়।

```text
Original

[10 20 30 40 50]

Mask

[F F T T T]
```

---

# Data Filtering

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

```python
a = np.array([10,20,30,40,50])

print(a[a > 25])
```

Output

```python
[30 40 50]
```

ভিতরে কী হলো?

```text
Original

10 20 30 40 50

Mask

 F  F  T  T  T

↓

30 40 50
```

এটাই Boolean Indexing।

---

# আরেকটি উদাহরণ

```python
marks = np.array([33, 45, 67, 90, 21, 78])

passed = marks >= 40

print(marks[passed])
```

Output

```python
[45 67 90 78]
```

---

# Multiple Conditions

ধরো

৩০-এর বেশি

এবং

৫০-এর কম

---

অনেকেই লিখে

```python
a > 30 and a < 50
```

❌ ভুল

কারণ

Python-এর `and`

NumPy Array-এর জন্য কাজ করে না।

---

সঠিক

```python
(a > 30) & (a < 50)
```

Example

```python
print(a[(a > 20) & (a < 50)])
```

Output

```python
[30 40]
```

---

Visual

```text
Greater than 20

F F T T T

Less than 50

T T T T F

AND

F F T T F
```

↓

```text
30

40
```

---

# OR Condition

```python
(a < 20) | (a > 40)
```

Example

```python
print(a[(a < 20) | (a > 40)])
```

Output

```python
[10 50]
```

---

# NOT Condition

```python
~(a > 30)
```

Example

```python
print(a[~(a > 30)])
```

Output

```python
[10 20 30]
```

---

# Summary of Operators

| Operation | NumPy |
| --------- | ----- |
| AND       | `&`   |
| OR        | `\|`  |
| NOT       | `~`   |

**মনে রাখবে:**

```python
(a > 10) & (a < 30)
```

না লিখে

```python
a > 10 & a < 30
```

লিখলে precedence-এর কারণে ভুল result আসতে পারে।

সব comparison-এর চারপাশে parentheses ব্যবহার করা ভালো অভ্যাস।

---

# Filtering Negative Numbers

```python
a = np.array([-5,-2,3,8,-1])

print(a[a >= 0])
```

Output

```python
[3 8]
```

---

# Filtering Even Numbers

```python
a = np.arange(1,11)

print(a[a % 2 == 0])
```

Output

```python
[2 4 6 8 10]
```

---

# Filtering Odd Numbers

```python
print(a[a % 2 != 0])
```

Output

```python
[1 3 5 7 9]
```

---

# Real Data Engineering Example

ধরো

Employee Salary

```python
salary = np.array([
    25000,
    40000,
    55000,
    80000,
    15000
])
```

যাদের salary

৫০,০০০-এর বেশি

```python
high_salary = salary[salary > 50000]

print(high_salary)
```

Output

```python
[55000 80000]
```

---

# Real Machine Learning Example

Image

```python
image = np.array([
    [100,150],
    [200,80]
])
```

Bright Pixel

```python
print(image > 128)
```

Output

```python
[[False True]
 [ True False]]
```

এই mask ব্যবহার করে image processing করা হয়।

---

# Common Mistakes

## ❌ `and` ব্যবহার করা

```python
a > 10 and a < 20
```

সঠিক

```python
(a > 10) & (a < 20)
```

---

## ❌ `or`

ভুল

```python
a < 5 or a > 20
```

সঠিক

```python
(a < 5) | (a > 20)
```

---

## ❌ Parentheses না দেওয়া

ভুল

```python
a > 5 & a < 20
```

সঠিক

```python
(a > 5) & (a < 20)
```

---

# Practice

## Easy

```python
a = np.array([5,10,15,20,25])
```

Find

1.

```python
a > 10
```

2.

```python
a == 20
```

3.

```python
a <= 15
```

---

## Medium

```python
marks = np.array([22,45,67,88,34,95])
```

Find

* Pass Marks
* Above 80
* Below 35

---

## Hard

```python
salary = np.array([
    20000,
    35000,
    50000,
    65000,
    80000
])
```

Find

1.

Salary between

30000

and

70000

---

2.

Salary below

30000

or

above

70000

---

3.

Salary NOT greater than

50000

---

# Interview Questions

### 1.

Boolean Mask কী?

---

### 2.

`a > 5`

কি return করে?

---

### 3.

`and`

কেন কাজ করে না?

---

### 4.

Difference

```python
&
```

vs

```python
and
```

---

### 5.

Filtering কীভাবে করা হয়?

---

# Cheat Sheet

| Condition | Example               |
| --------- | --------------------- |
| Greater   | `a > 5`               |
| Less      | `a < 5`               |
| Equal     | `a == 5`              |
| Not Equal | `a != 5`              |
| AND       | `(a > 5) & (a < 20)`  |
| OR        | `(a < 5) \| (a > 20)` |
| NOT       | `~(a > 5)`            |
| Filter    | `a[a > 5]`            |

---

# Mini Project

ধরো একটি online store-এর order amount আছে:

```python
import numpy as np

orders = np.array([
    250,
    1200,
    5000,
    300,
    8000,
    150,
    4500
])
```

শুধু NumPy ব্যবহার করে বের করো:

1. 1000 টাকার বেশি order
2. 500 টাকার কম order
3. 1000–5000 টাকার মধ্যে order
4. 5000 টাকার বেশি বা 200 টাকার কম order
5. 1000 টাকার বেশি order-এর সংখ্যা (`len(...)` বা পরে `np.count_nonzero()` শিখবে)

---

## Lesson 6 Summary

আজ আমরা শিখলাম:

* ✅ Comparison operators (`>`, `<`, `>=`, `<=`, `==`, `!=`)
* ✅ Boolean arrays
* ✅ Boolean masks
* ✅ Boolean indexing দিয়ে filtering
* ✅ Multiple conditions (`&`, `|`, `~`)
* ✅ Data filtering-এর production use cases

---

## পরবর্তী Lesson 7

Lesson 7-এ আমরা **Logical Functions** গভীরভাবে শিখব:

* `np.logical_and()`
* `np.logical_or()`
* `np.logical_not()`
* `np.logical_xor()`
* `np.any()`
* `np.all()`

এগুলো complex filtering, validation, data quality checks এবং production data pipelines-এ নিয়মিত ব্যবহৃত হয়।
# Module 2 — Lesson 6: Comparison Operations & Boolean Arrays

আজকের Lesson **Data Engineer** এবং **ML Engineer**-দের জন্য সবচেয়ে বেশি ব্যবহৃত বিষয়গুলোর একটি।

বাস্তব প্রজেক্টে আমরা প্রায়ই এমন প্রশ্ন করি:

* কোন salary 50,000-এর বেশি?
* কোন student pass করেছে?
* কোন pixel 128-এর বেশি?
* কোন customer VIP?
* কোন transaction fraud হতে পারে?

এই সবকিছুর ভিত্তি হলো **Boolean Arrays**।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে:

* Comparison Operators ব্যবহার করতে
* Boolean Array বুঝতে
* Boolean Mask তৈরি করতে
* Data Filter করতে
* Multiple Condition ব্যবহার করতে

---

# Step 1: Comparison Operators

প্রথমে একটি Array তৈরি করি।

```python
import numpy as np

a = np.array([10, 20, 30, 40, 50])
```

Visual

```text
Index : 0   1   2   3   4
Value :10  20  30  40  50
```

---

# Greater Than (`>`)

```python
print(a > 25)
```

Output

```python
[False False  True  True  True]
```

Visual

```text
10 > 25 ❌

20 > 25 ❌

30 > 25 ✅

40 > 25 ✅

50 > 25 ✅
```

---

# Less Than (`<`)

```python
print(a < 30)
```

Output

```python
[ True  True False False False]
```

---

# Greater Than or Equal (`>=`)

```python
print(a >= 30)
```

Output

```python
[False False True True True]
```

---

# Less Than or Equal (`<=`)

```python
print(a <= 20)
```

Output

```python
[ True True False False False]
```

---

# Equal (`==`)

```python
print(a == 30)
```

Output

```python
[False False True False False]
```

---

# Not Equal (`!=`)

```python
print(a != 30)
```

Output

```python
[ True True False True True]
```

---

# Boolean Array

খেয়াল করো—

Comparison-এর result কখনো number না।

সবসময়

```text
True

False
```

এগুলোই Boolean Array।

```python
mask = a > 25

print(mask)
```

Output

```python
[False False True True True]
```

Type দেখো

```python
print(mask.dtype)
```

Output

```python
bool
```

---

# Boolean Mask কী?

Boolean Array-কে যখন filtering-এর জন্য ব্যবহার করা হয়, তখন তাকে **Boolean Mask** বলা হয়।

```text
Original

[10 20 30 40 50]

Mask

[F F T T T]
```

---

# Data Filtering

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

```python
a = np.array([10,20,30,40,50])

print(a[a > 25])
```

Output

```python
[30 40 50]
```

ভিতরে কী হলো?

```text
Original

10 20 30 40 50

Mask

 F  F  T  T  T

↓

30 40 50
```

এটাই Boolean Indexing।

---

# আরেকটি উদাহরণ

```python
marks = np.array([33, 45, 67, 90, 21, 78])

passed = marks >= 40

print(marks[passed])
```

Output

```python
[45 67 90 78]
```

---

# Multiple Conditions

ধরো

৩০-এর বেশি

এবং

৫০-এর কম

---

অনেকেই লিখে

```python
a > 30 and a < 50
```

❌ ভুল

কারণ

Python-এর `and`

NumPy Array-এর জন্য কাজ করে না।

---

সঠিক

```python
(a > 30) & (a < 50)
```

Example

```python
print(a[(a > 20) & (a < 50)])
```

Output

```python
[30 40]
```

---

Visual

```text
Greater than 20

F F T T T

Less than 50

T T T T F

AND

F F T T F
```

↓

```text
30

40
```

---

# OR Condition

```python
(a < 20) | (a > 40)
```

Example

```python
print(a[(a < 20) | (a > 40)])
```

Output

```python
[10 50]
```

---

# NOT Condition

```python
~(a > 30)
```

Example

```python
print(a[~(a > 30)])
```

Output

```python
[10 20 30]
```

---

# Summary of Operators

| Operation | NumPy |
| --------- | ----- |
| AND       | `&`   |
| OR        | `\|`  |
| NOT       | `~`   |

**মনে রাখবে:**

```python
(a > 10) & (a < 30)
```

না লিখে

```python
a > 10 & a < 30
```

লিখলে precedence-এর কারণে ভুল result আসতে পারে।

সব comparison-এর চারপাশে parentheses ব্যবহার করা ভালো অভ্যাস।

---

# Filtering Negative Numbers

```python
a = np.array([-5,-2,3,8,-1])

print(a[a >= 0])
```

Output

```python
[3 8]
```

---

# Filtering Even Numbers

```python
a = np.arange(1,11)

print(a[a % 2 == 0])
```

Output

```python
[2 4 6 8 10]
```

---

# Filtering Odd Numbers

```python
print(a[a % 2 != 0])
```

Output

```python
[1 3 5 7 9]
```

---

# Real Data Engineering Example

ধরো

Employee Salary

```python
salary = np.array([
    25000,
    40000,
    55000,
    80000,
    15000
])
```

যাদের salary

৫০,০০০-এর বেশি

```python
high_salary = salary[salary > 50000]

print(high_salary)
```

Output

```python
[55000 80000]
```

---

# Real Machine Learning Example

Image

```python
image = np.array([
    [100,150],
    [200,80]
])
```

Bright Pixel

```python
print(image > 128)
```

Output

```python
[[False True]
 [ True False]]
```

এই mask ব্যবহার করে image processing করা হয়।

---

# Common Mistakes

## ❌ `and` ব্যবহার করা

```python
a > 10 and a < 20
```

সঠিক

```python
(a > 10) & (a < 20)
```

---

## ❌ `or`

ভুল

```python
a < 5 or a > 20
```

সঠিক

```python
(a < 5) | (a > 20)
```

---

## ❌ Parentheses না দেওয়া

ভুল

```python
a > 5 & a < 20
```

সঠিক

```python
(a > 5) & (a < 20)
```

---

# Practice

## Easy

```python
a = np.array([5,10,15,20,25])
```

Find

1.

```python
a > 10
```

2.

```python
a == 20
```

3.

```python
a <= 15
```

---

## Medium

```python
marks = np.array([22,45,67,88,34,95])
```

Find

* Pass Marks
* Above 80
* Below 35

---

## Hard

```python
salary = np.array([
    20000,
    35000,
    50000,
    65000,
    80000
])
```

Find

1.

Salary between

30000

and

70000

---

2.

Salary below

30000

or

above

70000

---

3.

Salary NOT greater than

50000

---

# Interview Questions

### 1.

Boolean Mask কী?

---

### 2.

`a > 5`

কি return করে?

---

### 3.

`and`

কেন কাজ করে না?

---

### 4.

Difference

```python
&
```

vs

```python
and
```

---

### 5.

Filtering কীভাবে করা হয়?

---

# Cheat Sheet

| Condition | Example               |
| --------- | --------------------- |
| Greater   | `a > 5`               |
| Less      | `a < 5`               |
| Equal     | `a == 5`              |
| Not Equal | `a != 5`              |
| AND       | `(a > 5) & (a < 20)`  |
| OR        | `(a < 5) \| (a > 20)` |
| NOT       | `~(a > 5)`            |
| Filter    | `a[a > 5]`            |

---

# Mini Project

ধরো একটি online store-এর order amount আছে:

```python
import numpy as np

orders = np.array([
    250,
    1200,
    5000,
    300,
    8000,
    150,
    4500
])
```

শুধু NumPy ব্যবহার করে বের করো:

1. 1000 টাকার বেশি order
2. 500 টাকার কম order
3. 1000–5000 টাকার মধ্যে order
4. 5000 টাকার বেশি বা 200 টাকার কম order
5. 1000 টাকার বেশি order-এর সংখ্যা (`len(...)` বা পরে `np.count_nonzero()` শিখবে)

---

## Lesson 6 Summary

আজ আমরা শিখলাম:

* ✅ Comparison operators (`>`, `<`, `>=`, `<=`, `==`, `!=`)
* ✅ Boolean arrays
* ✅ Boolean masks
* ✅ Boolean indexing দিয়ে filtering
* ✅ Multiple conditions (`&`, `|`, `~`)
* ✅ Data filtering-এর production use cases

---

## পরবর্তী Lesson 7

Lesson 7-এ আমরা **Logical Functions** গভীরভাবে শিখব:

* `np.logical_and()`
* `np.logical_or()`
* `np.logical_not()`
* `np.logical_xor()`
* `np.any()`
* `np.all()`

এগুলো complex filtering, validation, data quality checks এবং production data pipelines-এ নিয়মিত ব্যবহৃত হয়।
# Module 2 — Lesson 7: Logical Functions (`np.logical_and`, `np.logical_or`, `np.logical_not`, `np.any`, `np.all`)

গত Lesson-এ আমরা শিখেছি:

```python
(a > 10) & (a < 20)
```

আজ আমরা একই কাজ **NumPy Logical Functions** দিয়ে করব।

Production code-এ এগুলো অনেক বেশি দেখা যায়, বিশেষ করে complex condition, data validation এবং machine learning preprocessing-এ।

---

# Learning Objectives

এই Lesson শেষে তুমি জানতে পারবে—

* `np.logical_and()`
* `np.logical_or()`
* `np.logical_not()`
* `np.logical_xor()`
* `np.any()`
* `np.all()`
* Production Use Cases

---

# Dataset

```python
import numpy as np

numbers = np.array([10, 20, 30, 40, 50])
```

Visual

```
Index   0   1   2   3   4

Value  10  20  30  40  50
```

---

# What is a Logical Function?

Logical Function মানে—

একটি condition-এর ফলাফল (`True` বা `False`) নিয়ে কাজ করা।

---

# 1. `np.logical_and()`

ধরো আমাদের দরকার—

২০-এর বেশি

এবং

৫০-এর কম

---

আগের Lesson

```python
(numbers > 20) & (numbers < 50)
```

এখন

```python
mask = np.logical_and(
    numbers > 20,
    numbers < 50
)

print(mask)
```

Output

```python
[False False  True  True False]
```

Filtering

```python
print(numbers[mask])
```

Output

```python
[30 40]
```

---

## ভিতরে কী হচ্ছে?

প্রথম Condition

```python
numbers > 20
```

↓

```
F

F

T

T

T
```

---

দ্বিতীয় Condition

```python
numbers < 50
```

↓

```
T

T

T

T

F
```

---

AND

```
F

F

T

T

F
```

↓

```
30

40
```

---

# 2. `np.logical_or()`

ধরো

২০-এর কম

অথবা

৪০-এর বেশি

```python
mask = np.logical_or(
    numbers < 20,
    numbers > 40
)

print(mask)
```

Output

```python
[ True False False False True]
```

Filtering

```python
print(numbers[mask])
```

Output

```python
[10 50]
```

---

# 3. `np.logical_not()`

Condition উল্টে দেয়।

```python
mask = numbers > 30

print(mask)
```

Output

```python
[False False False True True]
```

NOT

```python
print(np.logical_not(mask))
```

Output

```python
[ True True True False False]
```

Filtering

```python
print(numbers[np.logical_not(mask)])
```

Output

```python
[10 20 30]
```

---

# 4. `np.logical_xor()`

XOR

মানে

Exactly One Condition True

---

Truth Table

| A | B | XOR |
| - | - | --- |
| F | F | F   |
| F | T | T   |
| T | F | T   |
| T | T | F   |

---

Example

```python
mask = np.logical_xor(
    numbers > 20,
    numbers > 40
)

print(mask)
```

---

Condition 1

```
F

F

T

T

T
```

Condition 2

```
F

F

F

F

T
```

XOR

```
F

F

T

T

F
```

Filtering

```python
print(numbers[mask])
```

Output

```python
[30 40]
```

---

# 5. `np.any()`

এটি Interview-এ অনেক আসে।

প্রশ্ন

একটিও কি True আছে?

---

Example

```python
a = np.array([False, False, True])

print(np.any(a))
```

Output

```python
True
```

---

আরেকটি

```python
a = np.array([False, False, False])

print(np.any(a))
```

Output

```python
False
```

---

## Real Example

কোন employee-এর salary কি ১ লক্ষের বেশি?

```python
salary = np.array([
    30000,
    45000,
    120000,
    50000
])

print(np.any(salary > 100000))
```

Output

```python
True
```

---

# 6. `np.all()`

সবগুলো True কি?

```python
a = np.array([True, True, True])

print(np.all(a))
```

Output

```python
True
```

---

আরেকটি

```python
a = np.array([
    True,
    False,
    True
])

print(np.all(a))
```

Output

```python
False
```

---

## Real Example

সব Marks কি Pass করেছে?

```python
marks = np.array([
    50,
    70,
    85,
    60
])

print(np.all(marks >= 40))
```

Output

```python
True
```

---

Fail Example

```python
marks = np.array([
    50,
    20,
    80
])

print(np.all(marks >= 40))
```

Output

```python
False
```

---

# Difference

## `any`

```
একটিও True?

↓

True
```

---

## `all`

```
সবগুলো True?

↓

True
```

---

# Axis-এর সাথে `any()` এবং `all()`

২D Array:

```python
arr = np.array([
    [True, False],
    [True, True]
])
```

---

## `axis=0`

```python
print(np.any(arr, axis=0))
```

Output

```python
[True True]
```

কারণ

Column-wise check করছে।

---

## `axis=1`

```python
print(np.all(arr, axis=1))
```

Output

```python
[False True]
```

কারণ

Row-wise check করছে।

---

# Real Data Engineering Example

ধরো

Age

```python
age = np.array([
    25,
    30,
    -5,
    40
])
```

Negative Age আছে?

```python
print(np.any(age < 0))
```

↓

```
True
```

Production Pipeline

```
CSV

↓

Validation

↓

Reject
```

---

# Machine Learning Example

Image

```python
image = np.array([
    [120, 250],
    [180, 300]
])
```

Invalid Pixel?

```python
print(np.any(image > 255))
```

↓

```
True
```

এভাবে model-এ ভুল data যাওয়া আটকানো যায়।

---

# Common Mistakes

## ❌ Python `and`

```python
a and b
```

NumPy array-এর জন্য নয়।

---

## ✔ NumPy

```python
np.logical_and(a, b)
```

---

## ❌ `any` vs `all`

অনেকে উল্টো করে ফেলে।

```
any

↓

একটি True হলেই True
```

```
all

↓

সব True হলে True
```

---

# Practice

## Easy

```python
a = np.array([
    5,
    15,
    25,
    35
])
```

Find

```python
np.logical_and(a > 10, a < 30)
```

---

## Medium

```python
marks = np.array([
    33,
    45,
    78,
    91,
    20
])
```

Find

1.

Pass

2.

Above 80

3.

Pass OR Above 80

---

## Hard

```python
salary = np.array([
    25000,
    50000,
    90000,
    120000
])
```

Check

1.

Any salary above 1 lakh?

2.

All salary above 20k?

3.

Salary between

40k

and

100k

---

# Interview Questions

### 1.

Difference

```python
&
```

vs

```python
np.logical_and()
```

**উত্তর:** সাধারণ ক্ষেত্রে একই কাজ করে। `np.logical_and()` function আকারে লেখা হয় এবং complex expressions বা readable code-এ বেশি ব্যবহৃত হয়।

---

### 2.

`np.any()` কী?

---

### 3.

`np.all()` কী?

---

### 4.

`logical_xor()` কী?

---

### 5.

Production-এ `any()` কোথায় ব্যবহার হয়?

উদাহরণ:

* Data validation
* Missing value detection
* Invalid pixel check
* Fraud detection rules

---

# Cheat Sheet

| Function               | কাজ                    |
| ---------------------- | ---------------------- |
| `np.logical_and(a, b)` | AND                    |
| `np.logical_or(a, b)`  | OR                     |
| `np.logical_not(a)`    | NOT                    |
| `np.logical_xor(a, b)` | XOR                    |
| `np.any(a)`            | অন্তত একটি `True` আছে? |
| `np.all(a)`            | সবগুলো `True`?         |

---

# Mini Project

একটি online exam-এর marks:

```python
import numpy as np

marks = np.array([
    75,
    45,
    32,
    90,
    55,
    20,
    80
])
```

শুধু NumPy ব্যবহার করে বের করো—

1. Pass করা students (`>=40`)
2. Distinction (`>=80`)
3. Pass কিন্তু Distinction নয়
4. কোনো student কি 100-এর বেশি marks পেয়েছে? (`np.any`)
5. সব student কি pass করেছে? (`np.all`)

---

## Lesson 7 Summary

আজ আমরা শিখলাম:

* ✅ `np.logical_and()`
* ✅ `np.logical_or()`
* ✅ `np.logical_not()`
* ✅ `np.logical_xor()`
* ✅ `np.any()`
* ✅ `np.all()`
* ✅ Data validation-এর production use cases

---

## পরবর্তী Lesson 8

Lesson 8-এ আমরা **Aggregation Functions** শিখব, যা Data Analysis-এর ভিত্তি:

* `np.sum()`
* `np.mean()`
* `np.median()`
* `np.max()`
* `np.min()`
* `np.std()`
* `np.var()`
* `np.prod()`
* `axis` ব্যবহার করে Row-wise এবং Column-wise aggregation

এই Lesson-এর পর তুমি NumPy দিয়ে dataset-এর summary statistics বের করতে পারবে, যা Pandas এবং Machine Learning-এর জন্য অপরিহার্য।
# Module 2 — Lesson 8: Aggregation Functions (Production-Level Guide)

আজকের Lesson হলো **Data Analysis-এর হৃদয় (Heart of Data Analysis)**।

প্রায় প্রতিটি Data Engineer, Data Analyst, ML Engineer প্রতিদিন এই functions ব্যবহার করেন।

যখনই নতুন dataset পাবে, প্রথম কাজ হবে dataset-এর summary বের করা।

যেমন:

* মোট কত sales?
* Average salary কত?
* সর্বোচ্চ marks কত?
* Minimum temperature কত?
* Standard deviation কত?
* প্রতি column-এর average কত?

এসবই Aggregation Functions দিয়ে করা হয়।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে—

* `np.sum()`
* `np.mean()`
* `np.median()`
* `np.max()`
* `np.min()`
* `np.std()`
* `np.var()`
* `np.prod()`
* `axis=0`
* `axis=1`

---

# Dataset

```python
import numpy as np

sales = np.array([
    [100, 200, 300],
    [150, 250, 350],
    [200, 300, 400]
])

print(sales)
```

Output

```text
[[100 200 300]
 [150 250 350]
 [200 300 400]]
```

Visual

```text
        Jan  Feb  Mar
Shop A 100  200  300

Shop B 150  250  350

Shop C 200  300  400
```

---

# Understanding `axis` (সবচেয়ে গুরুত্বপূর্ণ)

অনেকেই `axis` নিয়ে কনফিউজ হয়।

এটা ভালোভাবে বুঝো।

## axis = 0

মানে

**Rows-এর উপর দিয়ে নিচে নামবে**

↓

Column-wise Operation

Visual

```text
100

150

200

↓

Sum
```

---

## axis = 1

মানে

**Columns-এর উপর দিয়ে ডানে যাবে**

↓

Row-wise Operation

```text
100 → 200 → 300

↓

Sum
```

---

## মনে রাখার Trick

```
axis = 0

↓

Vertical

↓

Column Result
```

```
axis = 1

↓

Horizontal

↓

Row Result
```

---

# 1. `np.sum()`

সব element যোগ করবে।

```python
print(np.sum(sales))
```

Output

```text
2250
```

কারণ

```
100+200+300+

150+250+350+

200+300+400

=

2250
```

---

## Column-wise Sum

```python
print(np.sum(sales, axis=0))
```

Output

```text
[450 750 1050]
```

Calculation

```
100+150+200 = 450

200+250+300 = 750

300+350+400 = 1050
```

---

## Row-wise Sum

```python
print(np.sum(sales, axis=1))
```

Output

```text
[600 750 900]
```

---

# 2. `np.mean()`

Average বের করে।

```python
print(np.mean(sales))
```

Output

```text
250.0
```

---

## Column Mean

```python
print(np.mean(sales, axis=0))
```

Output

```text
[150. 250. 350.]
```

---

## Row Mean

```python
print(np.mean(sales, axis=1))
```

Output

```text
[200. 250. 300.]
```

---

# 3. `np.median()`

Median = Middle Value

```python
a = np.array([
    5,
    2,
    8,
    10,
    100
])

print(np.median(a))
```

Output

```text
8
```

কারণ

Sorted

```
2

5

8

10

100
```

Middle = 8

---

যদি even number হয়

```python
a = np.array([
    10,
    20,
    30,
    40
])

print(np.median(a))
```

Output

```text
25
```

কারণ

```
20+30

÷2
```

---

# Mean vs Median

Dataset

```
10

12

13

15

500
```

Mean

```
110
```

Median

```
13
```

Outlier থাকলে Median অনেক বেশি reliable।

---

# 4. `np.max()`

```python
print(np.max(sales))
```

Output

```text
400
```

---

Column Maximum

```python
print(np.max(sales, axis=0))
```

Output

```text
[200 300 400]
```

---

# 5. `np.min()`

```python
print(np.min(sales))
```

Output

```text
100
```

---

# 6. `np.std()`

Standard Deviation

Data কতটা spread হয়েছে।

```python
a = np.array([
    10,
    20,
    30
])

print(np.std(a))
```

Output

```text
8.164965...
```

---

ছোট Standard Deviation

↓

সব data কাছাকাছি।

---

বড় Standard Deviation

↓

Data ছড়িয়ে আছে।

---

# Real Example

Salary

```
30000

31000

30500

29900
```

↓

Low Standard Deviation

---

```
10000

50000

120000

25000
```

↓

High Standard Deviation

---

# 7. `np.var()`

Variance

Formula

```
Variance

=

(Standard Deviation)^2
```

```python
print(np.var(a))
```

---

Machine Learning-এ Feature Scaling-এর আগে Variance দেখা হয়।

---

# 8. `np.prod()`

সব element গুণ করে।

```python
a = np.array([
    2,
    3,
    4
])

print(np.prod(a))
```

Output

```text
24
```

কারণ

```
2×3×4
```

---

# Multiple Aggregation

```python
print(np.sum(sales))

print(np.mean(sales))

print(np.max(sales))

print(np.min(sales))
```

---

# Real Data Engineering Example

Sales Data

```python
sales = np.array([
    2500,
    4000,
    5000,
    3000,
    4500
])
```

Total

```python
np.sum(sales)
```

Average

```python
np.mean(sales)
```

Highest

```python
np.max(sales)
```

Lowest

```python
np.min(sales)
```

---

# Machine Learning Example

Feature Matrix

```python
features = np.array([
    [170,65],
    [180,75],
    [160,55]
])
```

Average Height

```python
np.mean(features, axis=0)
```

Output

```text
[170. 65.]
```

---

# Common Mistakes

## ❌ axis উল্টো করা

মনে রাখো

```
axis=0

↓

Column Result
```

```
axis=1

↓

Row Result
```

---

## ❌ Mean আর Median গুলিয়ে ফেলা

Mean

↓

Average

Median

↓

Middle

---

## ❌ `max()` আর `np.max()`

Python

```python
max([1,2,3])
```

NumPy

```python
np.max(array)
```

`np.max()`-এর `axis` parameter আছে, যা Python-এর `max()`-এ নেই।

---

# Practice

## Easy

```python
a = np.array([
    10,
    20,
    30,
    40
])
```

Find

* Sum
* Mean
* Max
* Min

---

## Medium

```python
marks = np.array([
    [80,70,90],
    [60,75,85],
    [95,88,91]
])
```

Find

* Total Marks
* Subject-wise Average
* Student-wise Total

---

## Hard

```python
salary = np.array([
    25000,
    35000,
    45000,
    60000,
    100000
])
```

Calculate

* Mean
* Median
* Standard Deviation
* Variance

তারপর ব্যাখ্যা করো:

**Median কেন Mean-এর থেকে আলাদা হলো?**

---

# Interview Questions

### 1.

Difference

```
Mean

vs

Median
```

---

### 2.

`axis=0`

মানে কী?

---

### 3.

`axis=1`

মানে কী?

---

### 4.

Standard Deviation কী বোঝায়?

---

### 5.

Variance কী?

---

### 6.

কখন Median ব্যবহার করবে?

**উত্তর:** যখন dataset-এ outlier (অস্বাভাবিক বড় বা ছোট মান) থাকে।

---

# Cheat Sheet

| Function      | কাজ                 |
| ------------- | ------------------- |
| `np.sum()`    | মোট যোগফল           |
| `np.mean()`   | Average             |
| `np.median()` | মধ্যম মান           |
| `np.max()`    | সর্বোচ্চ মান        |
| `np.min()`    | সর্বনিম্ন মান       |
| `np.std()`    | Standard Deviation  |
| `np.var()`    | Variance            |
| `np.prod()`   | সব element-এর গুণফল |

---

# Mini Project

ধরো তিনটি দোকানের ৭ দিনের বিক্রির data আছে:

```python
import numpy as np

sales = np.array([
    [1200, 1500, 1300, 1700, 1600, 1800, 2000],
    [1000, 1100, 1200, 1300, 1250, 1400, 1500],
    [2000, 2100, 1900, 2200, 2300, 2400, 2500]
])
```

শুধু NumPy ব্যবহার করে বের করো—

1. মোট বিক্রি
2. প্রতিটি দোকানের মোট বিক্রি (`axis=1`)
3. প্রতিদিনের মোট বিক্রি (`axis=0`)
4. প্রতিটি দোকানের গড় বিক্রি
5. কোন দোকানের সর্বোচ্চ একদিনের বিক্রি হয়েছে?
6. কোন দিনের মোট বিক্রি সবচেয়ে কম?

---

# Lesson 8 Summary

আজ আমরা শিখলাম:

* ✅ `np.sum()`
* ✅ `np.mean()`
* ✅ `np.median()`
* ✅ `np.max()`
* ✅ `np.min()`
* ✅ `np.std()`
* ✅ `np.var()`
* ✅ `np.prod()`
* ✅ `axis=0` বনাম `axis=1`
* ✅ Data analysis এবং ML-এ aggregation-এর ব্যবহার

---

## পরবর্তী Lesson 9

আমরা শুরু করব **Module 3: Indexing & Slicing**।

এটি NumPy-এর সবচেয়ে গুরুত্বপূর্ণ দক্ষতাগুলোর একটি। আমরা শিখব:

* 1D Indexing
* Negative Indexing
* Slicing
* Step Slicing
* View vs Copy (প্রাথমিক ধারণা)
* বাস্তব dataset থেকে data extraction

এই Lesson-এর পর তুমি NumPy array থেকে যেকোনো অংশ দক্ষতার সঙ্গে বের করতে পারবে।
# Module 3 — Lesson 9: Indexing & Slicing (1D Arrays)

এটি NumPy-এর সবচেয়ে গুরুত্বপূর্ণ অধ্যায়গুলোর একটি।

বাস্তব জীবনে আমরা খুব কমই পুরো array নিয়ে কাজ করি। বেশিরভাগ সময় আমাদের দরকার হয়—

* প্রথম ১০টি record
* শেষ ৫টি record
* প্রতি ২য় element
* নির্দিষ্ট range-এর data
* sample data

এসবই **Indexing** এবং **Slicing** দিয়ে করা হয়।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে—

* Single Indexing
* Negative Indexing
* Slicing
* Step Slicing
* Reverse Array
* View vs Copy-এর প্রাথমিক ধারণা

---

# Dataset

```python
import numpy as np

numbers = np.array([10, 20, 30, 40, 50, 60, 70])
```

Visual

```text
Index :   0   1   2   3   4   5   6

Value :  10  20  30  40  50  60  70
```

---

# What is Index?

Index হলো element-এর অবস্থান (position)।

প্রথম element-এর index সবসময়

```text
0
```

---

# Positive Indexing

```python
print(numbers[0])
```

Output

```text
10
```

---

```python
print(numbers[3])
```

Output

```text
40
```

---

```python
print(numbers[6])
```

Output

```text
70
```

---

Visual

```text
Index

0 → 10

1 → 20

2 → 30

3 → 40

4 → 50

5 → 60

6 → 70
```

---

# Index Error

```python
print(numbers[10])
```

Output

```text
IndexError
```

কারণ

Array-তে মাত্র ৭টি element আছে।

---

# Negative Indexing

Python এবং NumPy-এর খুব সুন্দর একটি feature।

শেষ element

```python
print(numbers[-1])
```

Output

```text
70
```

---

শেষ থেকে দ্বিতীয়

```python
print(numbers[-2])
```

Output

```text
60
```

---

Visual

```text
Positive

0 1 2 3 4 5 6

Negative

-7 -6 -5 -4 -3 -2 -1
```

---

# Slicing

Syntax

```python
array[start : stop]
```

**গুরুত্বপূর্ণ নিয়ম:**

* `start` অন্তর্ভুক্ত (included)
* `stop` অন্তর্ভুক্ত নয় (excluded)

এটাকে বলে:

> **Start Included, Stop Excluded**

---

## Example 1

```python
print(numbers[1:4])
```

Output

```text
[20 30 40]
```

Visual

```text
Index

0   1   2   3   4

10 20 30 40 50

   ↑       ↑

start=1

stop=4

4 include হবে না
```

---

## Example 2

```python
print(numbers[0:3])
```

Output

```text
[10 20 30]
```

---

## Example 3

```python
print(numbers[2:6])
```

Output

```text
[30 40 50 60]
```

---

# Omitting Start

যদি start না দাও

```python
print(numbers[:4])
```

Output

```text
[10 20 30 40]
```

মানে

```text
0

↓

4
```

---

# Omitting Stop

```python
print(numbers[3:])
```

Output

```text
[40 50 60 70]
```

মানে

```text
3

↓

শেষ পর্যন্ত
```

---

# পুরো Array

```python
print(numbers[:])
```

Output

```text
[10 20 30 40 50 60 70]
```

---

# Step Slicing

Syntax

```python
array[start:stop:step]
```

---

## Every 2nd Element

```python
print(numbers[::2])
```

Output

```text
[10 30 50 70]
```

Visual

```text
10

↓

30

↓

50

↓

70
```

---

## Every 3rd Element

```python
print(numbers[::3])
```

Output

```text
[10 40 70]
```

---

## Custom Step

```python
print(numbers[1:7:2])
```

Output

```text
[20 40 60]
```

---

# Reverse Array

```python
print(numbers[::-1])
```

Output

```text
[70 60 50 40 30 20 10]
```

এটি Interview-এ খুবই common।

---

# Reverse Every Second

```python
print(numbers[::-2])
```

Output

```text
[70 50 30 10]
```

---

# Slice Assignment

NumPy Slice দিয়ে value পরিবর্তন করা যায়।

```python
numbers = np.array([10,20,30,40,50])

numbers[1:4] = 0

print(numbers)
```

Output

```text
[10 0 0 0 50]
```

---

আরেকটি উদাহরণ

```python
numbers = np.array([1,2,3,4,5])

numbers[:2] = 100

print(numbers)
```

Output

```text
[100 100   3   4   5]
```

---

# View vs Copy (অত্যন্ত গুরুত্বপূর্ণ)

অনেকেই এখানে ভুল করে।

```python
a = np.array([10,20,30,40,50])

b = a[1:4]
```

এখন

```python
b[0] = 999
```

```python
print(a)
```

Output

```text
[10 999 30 40 50]
```

---

**কেন?**

কারণ

```python
b = a[1:4]
```

নতুন array তৈরি করেনি।

এটি **View** তৈরি করেছে।

---

Visual

```text
a

↓

Memory

↓

10 20 30 40 50

↑

b
```

দুজন একই memory দেখছে।

---

# Copy

যদি আলাদা memory চাও

```python
b = a[1:4].copy()
```

এখন

```python
b[0] = 999
```

Original

```python
print(a)
```

Output

```text
[10 20 30 40 50]
```

পরিবর্তন হবে না।

---

# Real Data Engineering Example

ধরো

```python
sales = np.array([
    1200,
    1300,
    1400,
    1500,
    1600,
    1700,
    1800
])
```

প্রথম ৫ দিনের data

```python
sales[:5]
```

---

শেষ ৩ দিনের data

```python
sales[-3:]
```

---

প্রতি ২ দিনের data

```python
sales[::2]
```

---

# Machine Learning Example

Dataset

```python
X = np.arange(100)
```

Training Data

```python
train = X[:80]
```

Testing Data

```python
test = X[80:]
```

এটি Train-Test Split-এর একটি সাধারণ ধারণা (বাস্তবে আমরা `scikit-learn`-এর `train_test_split` বেশি ব্যবহার করি)।

---

# Common Mistakes

## ❌ Stop Included মনে করা

```python
a[1:4]
```

Output

```text
20

30

40
```

`50` আসবে না।

---

## ❌ Slice Copy মনে করা

```python
b = a[1:4]
```

এটি Copy নয়।

এটি View।

---

## ❌ Reverse ভুল করা

ভুল

```python
a[-1]
```

এটি শুধু শেষ element।

Reverse নয়।

Reverse

```python
a[::-1]
```

---

# Practice

## Easy

```python
a = np.array([
    10,
    20,
    30,
    40,
    50,
    60
])
```

Find

1.

```python
a[2]
```

2.

```python
a[-1]
```

3.

```python
a[:3]
```

4.

```python
a[3:]
```

---

## Medium

```python
a = np.arange(1,11)
```

Find

* Every second number
* Last five numbers
* Reverse array

---

## Hard

```python
a = np.arange(1,21)
```

Find

1. First 10 numbers
2. Last 10 numbers
3. Even-index elements
4. Odd-index elements
5. Reverse every third element (`a[::-3]`)

---

# Interview Questions

### 1.

Difference

```python
a[2]
```

vs

```python
a[2:3]
```

**উত্তর:**

* `a[2]` → একটি scalar value return করে।
* `a[2:3]` → একটি 1D NumPy array return করে।

উদাহরণ:

```python
a = np.array([10, 20, 30])

print(a[2])     # 30
print(a[2:3])   # [30]
```

---

### 2.

Negative Indexing কী?

---

### 3.

Why

```python
a[::-1]
```

works?

**উত্তর:** `step=-1` হওয়ায় NumPy শেষ element থেকে শুরু করে এক ধাপ করে পিছনের দিকে যায়।

---

### 4.

Difference

```python
View

vs

Copy
```

* **View** → একই memory share করে।
* **Copy** → নতুন memory allocate করে।

---

### 5.

Stop কেন include হয় না?

**উত্তর:** Python slicing convention অনুযায়ী `start` inclusive এবং `stop` exclusive। এতে slice-এর length সহজে হিসাব করা যায় এবং slice গুলো সহজে একে অপরের সাথে জোড়া লাগানো যায়।

---

# Cheat Sheet

| Syntax     | Meaning             |
| ---------- | ------------------- |
| `a[0]`     | First element       |
| `a[-1]`    | Last element        |
| `a[2:5]`   | Index 2–4           |
| `a[:4]`    | First four          |
| `a[3:]`    | From index 3 to end |
| `a[:]`     | Whole array         |
| `a[::2]`   | Every 2nd element   |
| `a[::-1]`  | Reverse array       |
| `a.copy()` | Deep copy           |

---

# Mini Project

ধরো এক সপ্তাহের website visitors:

```python
import numpy as np

visitors = np.array([
    120,
    150,
    180,
    160,
    200,
    220,
    190
])
```

শুধু NumPy ব্যবহার করে বের করো—

1. প্রথম ৩ দিনের visitors
2. শেষ ২ দিনের visitors
3. প্রতি ২ দিনের visitors
4. Reverse order
5. মাঝের ৩ দিনের visitors
6. শেষ visitor count পরিবর্তন করে `500` করো
7. একই কাজ View দিয়ে এবং Copy দিয়ে করে পার্থক্য দেখো

---

# Lesson 9 Summary

আজ আমরা শিখলাম:

* ✅ Positive Indexing
* ✅ Negative Indexing
* ✅ Slicing (`start:stop`)
* ✅ Step Slicing (`start:stop:step`)
* ✅ Reverse (`[::-1]`)
* ✅ Slice Assignment
* ✅ **View vs Copy** (খুবই গুরুত্বপূর্ণ)

---

## পরবর্তী Lesson 10

Lesson 10-এ আমরা **2D Array Indexing & Slicing** শিখব:

* `arr[row, column]`
* Row Selection
* Column Selection
* Sub-matrix Extraction
* Row/Column Slicing
* Real dataset manipulation

এটি NumPy-এর সবচেয়ে বেশি ব্যবহৃত দক্ষতাগুলোর একটি, কারণ বাস্তব dataset প্রায় সবসময়ই 2D matrix আকারে থাকে।

# Module 3 — Lesson 10: 2D Array Indexing & Slicing (Mastery Guide)

এখন পর্যন্ত আমরা 1D Array নিয়ে কাজ করেছি।

কিন্তু বাস্তব জীবনে Data Engineering, Machine Learning, Pandas—প্রায় সব dataset-ই **2D Matrix** আকারে থাকে।

উদাহরণ:

| ID | Age | Salary |
| -- | --- | ------ |
| 1  | 25  | 30000  |
| 2  | 30  | 45000  |
| 3  | 35  | 60000  |

এটি NumPy-তে একটি **2D Array**।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে—

* 2D Array Indexing
* Row Selection
* Column Selection
* Submatrix Selection
* Row & Column Slicing
* Entire Row / Entire Column
* Production Dataset Manipulation

---

# Dataset

```python
import numpy as np

employees = np.array([
    [101, 25, 30000],
    [102, 30, 45000],
    [103, 35, 60000],
    [104, 40, 80000]
])

print(employees)
```

Output

```text
[[  101    25 30000]
 [  102    30 45000]
 [  103    35 60000]
 [  104    40 80000]]
```

Visual

```text
        ID   Age Salary

Row0   101   25  30000

Row1   102   30  45000

Row2   103   35  60000

Row3   104   40  80000
```

---

# 2D Indexing Syntax

```python
array[row, column]
```

প্রথমে Row

তারপর Column

---

# Access Single Element

```python
print(employees[0,0])
```

Output

```text
101
```

---

```python
print(employees[0,1])
```

Output

```text
25
```

---

```python
print(employees[2,2])
```

Output

```text
60000
```

---

Visual

```text
employees[2,2]

↓

Row 2

↓

Column 2

↓

60000
```

---

# Entire Row

```python
print(employees[0])
```

Output

```text
[101 25 30000]
```

---

Second Row

```python
print(employees[1])
```

Output

```text
[102 30 45000]
```

---

Last Row

```python
print(employees[-1])
```

Output

```text
[104 40 80000]
```

---

# Entire Column

সবচেয়ে বেশি ব্যবহৃত।

Syntax

```python
array[:, column]
```

---

## First Column (ID)

```python
print(employees[:,0])
```

Output

```text
[101 102 103 104]
```

---

## Age Column

```python
print(employees[:,1])
```

Output

```text
[25 30 35 40]
```

---

## Salary Column

```python
print(employees[:,2])
```

Output

```text
[30000 45000 60000 80000]
```

---

Visual

```text
:

↓

সব Row

↓

Column 2
```

---

# Row Slice

প্রথম দুই Row

```python
print(employees[:2])
```

Output

```text
[[101 25 30000]
 [102 30 45000]]
```

---

শেষ দুই Row

```python
print(employees[2:])
```

Output

```text
[[103 35 60000]
 [104 40 80000]]
```

---

# Column Slice

প্রথম দুই Column

```python
print(employees[:, :2])
```

Output

```text
[[101 25]
 [102 30]
 [103 35]
 [104 40]]
```

---

শেষ দুই Column

```python
print(employees[:,1:])
```

Output

```text
[[   25 30000]
 [   30 45000]
 [   35 60000]
 [   40 80000]]
```

---

# Submatrix Selection

ধরো

প্রথম দুই Row

এবং

শেষ দুই Column

```python
print(employees[:2,1:])
```

Output

```text
[[25 30000]
 [30 45000]]
```

---

আরেকটি

```python
print(employees[1:3,0:2])
```

Output

```text
[[102 30]
 [103 35]]
```

---

# Single Row, Multiple Columns

```python
print(employees[1,0:2])
```

Output

```text
[102 30]
```

---

# Multiple Rows, Single Column

```python
print(employees[1:4,2])
```

Output

```text
[45000 60000 80000]
```

---

# Using Negative Index

Last Row

```python
print(employees[-1])
```

Last Column

```python
print(employees[:,-1])
```

Output

```text
[30000 45000 60000 80000]
```

---

# Step Slicing

Every Second Row

```python
print(employees[::2])
```

Output

```text
[[101 25 30000]
 [103 35 60000]]
```

---

Every Second Column

```python
print(employees[:,::2])
```

Output

```text
[[101 30000]
 [102 45000]
 [103 60000]
 [104 80000]]
```

---

# Modify Values

Increase first employee salary

```python
employees[0,2] = 35000

print(employees)
```

---

Entire Salary Column

```python
employees[:,2] = employees[:,2] + 5000
```

Output

```text
[35000 50000 65000 85000]
```

---

Production Version

```python
employees[:,2] += 5000
```

---

# Real Data Engineering Example

CSV Data

```text
ID Age Salary
```

Need only Salary

```python
salary = employees[:,2]
```

Average Salary

```python
np.mean(salary)
```

Highest Salary

```python
np.max(salary)
```

---

# Machine Learning Example

Dataset

```python
X = employees[:,1:]
```

Output

```text
Age Salary
```

Target

```python
y = employees[:,0]
```

এভাবে Features (`X`) এবং Labels (`y`) আলাদা করা হয়।

---

# View vs Copy (Again)

```python
salary = employees[:,2]
```

এটি **View**।

```python
salary[0] = 99999
```

Original array-ও পরিবর্তিত হবে।

যদি না চাও

```python
salary = employees[:,2].copy()
```

---

# Common Mistakes

## ❌ Row এবং Column উল্টো করা

```python
employees[2,1]
```

মানে

Row 2

Column 1

---

## ❌ Column নিতে

ভুল

```python
employees[2]
```

এটি Row দেয়।

সঠিক

```python
employees[:,2]
```

---

## ❌ Submatrix

```python
employees[1:3]
```

এটি শুধু Row slice।

Column slice চাইলে

```python
employees[1:3,1:]
```

---

# Practice

## Easy

```python
arr = np.array([
    [1,2,3],
    [4,5,6],
    [7,8,9]
])
```

Find

1.

```python
arr[1,2]
```

2.

```python
arr[:,1]
```

3.

```python
arr[2]
```

---

## Medium

Find

* First Row
* Last Column
* Middle Row
* First Two Columns

---

## Hard

```python
marks = np.array([
    [80,90,70],
    [75,60,88],
    [95,92,91]
])
```

Find

1. Subject-1 marks
2. Student-2 marks
3. Last two students
4. First two subjects
5. Bottom-right 2×2 matrix

---

# Interview Questions

### 1.

Difference

```python
arr[0]
```

vs

```python
arr[:,0]
```

**Answer**

```text
arr[0]

↓

First Row

arr[:,0]

↓

First Column
```

---

### 2.

Meaning

```python
:
```

**Answer**

সব Row অথবা সব Column (যেখানে ব্যবহার করা হয়েছে)।

---

### 3.

Difference

```python
arr[1:3]
```

vs

```python
arr[1:3,:]
```

দুটিই এখানে একই Row দেয়, তবে দ্বিতীয়টি স্পষ্টভাবে "সব Column" বোঝায় এবং complex slicing-এ বেশি readable।

---

### 4.

How to get last column?

```python
arr[:,-1]
```

---

### 5.

How to get first two rows and last column?

```python
arr[:2,-1]
```

---

# Cheat Sheet

| Syntax       | Meaning                      |
| ------------ | ---------------------------- |
| `arr[0]`     | First Row                    |
| `arr[:,0]`   | First Column                 |
| `arr[:2]`    | First Two Rows               |
| `arr[:,1:]`  | All Rows, Last Columns       |
| `arr[:2,1:]` | First Two Rows, Last Columns |
| `arr[-1]`    | Last Row                     |
| `arr[:,-1]`  | Last Column                  |
| `arr[::2]`   | Every Second Row             |
| `arr[:,::2]` | Every Second Column          |

---

# Mini Project (Production-Level)

একটি e-commerce sales dataset:

```python
import numpy as np

sales = np.array([
    [101, 1200, 5],
    [102, 2500, 8],
    [103, 1800, 3],
    [104, 3000, 10],
    [105, 2200, 7]
])
```

Columns:

```text
ProductID

Revenue

Quantity
```

### Tasks

1. সব Revenue বের করো।
2. সব Quantity বের করো।
3. প্রথম ৩টি Product-এর data বের করো।
4. শেষ ২টি Product-এর Revenue বের করো।
5. Revenue column-এ ১০% বৃদ্ধি করো।
6. Average Revenue বের করো।
7. Highest Quantity বের করো।
8. Revenue > 2000 এমন Product-এর পুরো Row বের করো (Boolean Indexing ব্যবহার করে)।

---

# Lesson 10 Summary

আজ আমরা শিখলাম:

* ✅ 2D Indexing (`arr[row, column]`)
* ✅ Row Selection
* ✅ Column Selection
* ✅ Row Slicing
* ✅ Column Slicing
* ✅ Submatrix Extraction
* ✅ Step Slicing
* ✅ Column Update
* ✅ Real-world dataset manipulation

---

# পরবর্তী Lesson 11 (Advanced Indexing)

এখন আমরা NumPy-এর আরও শক্তিশালী অংশে যাব:

* **Fancy Indexing**
* Integer Array Indexing
* Boolean Indexing (Advanced)
* `np.where()`
* `np.nonzero()`
* `np.argwhere()`
* Conditional Selection
* Production Data Filtering

এই Lesson-এর পর তুমি Pandas filtering-এর পেছনের NumPy logic-ও সহজে বুঝতে পারবে।

# Module 3 — Lesson 11: Advanced Indexing (Fancy Indexing, Boolean Indexing, `np.where`, `np.nonzero`, `np.argwhere`)

এটি NumPy-এর অন্যতম গুরুত্বপূর্ণ অধ্যায়।

বাস্তব Data Engineering এবং Machine Learning-এ dataset থেকে নির্দিষ্ট row, column বা condition অনুযায়ী data বের করার জন্য এই techniques প্রতিদিন ব্যবহার করা হয়।

আজকের Lesson শেষে তুমি Pandas-এর filtering-এর পেছনের NumPy logic-ও বুঝতে পারবে।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে—

* Fancy Indexing
* Integer Array Indexing
* Advanced Boolean Indexing
* `np.where()`
* `np.nonzero()`
* `np.argwhere()`
* Production Filtering

---

# Dataset

```python
import numpy as np

employees = np.array([
    [101, 25, 30000],
    [102, 30, 45000],
    [103, 35, 60000],
    [104, 40, 80000],
    [105, 28, 50000]
])
```

Visual

```
ID    Age   Salary

101   25    30000
102   30    45000
103   35    60000
104   40    80000
105   28    50000
```

---

# Part 1 — Fancy Indexing

Fancy Indexing মানে

**Index-এর array ব্যবহার করে data select করা।**

---

## Example

```python
ids = np.array([0, 2, 4])

print(employees[ids])
```

Output

```
[[101 25 30000]
 [103 35 60000]
 [105 28 50000]]
```

এখানে

```
Row 0

Row 2

Row 4
```

select হয়েছে।

---

আরেকটি

```python
print(employees[[1,3]])
```

Output

```
[[102 30 45000]
 [104 40 80000]]
```

---

# Duplicate Index

```python
print(employees[[0,0,2]])
```

Output

```
[[101 25 30000]
 [101 25 30000]
 [103 35 60000]]
```

Duplicate রাখা যায়।

---

# Reorder Rows

```python
print(employees[[4,3,2,1,0]])
```

Output

```
Reverse Order
```

Fancy Indexing দিয়ে যেকোনো order-এ data সাজানো যায়।

---

# Fancy Column Selection

শুধু

ID

এবং

Salary

```python
print(employees[:, [0,2]])
```

Output

```
[[101 30000]
 [102 45000]
 [103 60000]
 [104 80000]
 [105 50000]]
```

---

# Part 2 — Advanced Boolean Indexing

Salary

৫০,০০০-এর বেশি

```python
salary = employees[:,2]

print(employees[salary > 50000])
```

Output

```
[[103 35 60000]
 [104 40 80000]]
```

---

Age

৩০-এর নিচে

```python
print(employees[employees[:,1] < 30])
```

Output

```
[[101 25 30000]
 [105 28 50000]]
```

---

Multiple Condition

```python
mask = (
    (employees[:,1] >= 30)
    &
    (employees[:,2] >= 50000)
)

print(employees[mask])
```

Output

```
[[103 35 60000]
 [104 40 80000]]
```

---

# Part 3 — np.where()

এটি Interview-এ খুব common।

Syntax

```python
np.where(condition)
```

---

Example

```python
salary = employees[:,2]

print(np.where(salary > 50000))
```

Output

```
(array([2,3]),)
```

মানে

Row

```
2

3
```

---

# Using where()

```python
index = np.where(salary > 50000)

print(employees[index])
```

Output

```
[[103 35 60000]
 [104 40 80000]]
```

---

# Replace Values using where()

Salary

৫০,০০০-এর বেশি হলে

Bonus

১০%

```python
salary = employees[:,2]

bonus = np.where(
    salary > 50000,
    salary * 1.10,
    salary
)

print(bonus)
```

Output

```
[30000.
45000.
66000.
88000.
50000.]
```

---

# Think of np.where Like Excel IF

```text
IF(condition)

THEN value1

ELSE value2
```

NumPy

```python
np.where(
    condition,
    value_if_true,
    value_if_false
)
```

---

# Part 4 — np.nonzero()

Example

```python
a = np.array([
    0,
    5,
    0,
    8,
    2
])

print(np.nonzero(a))
```

Output

```
(array([1,3,4]),)
```

কারণ

```
Index

1

3

4
```

non-zero।

---

Data

```python
print(a[np.nonzero(a)])
```

Output

```
[5 8 2]
```

---

# 2D Example

```python
matrix = np.array([
    [0,1],
    [3,0]
])

print(np.nonzero(matrix))
```

Output

```
(array([0,1]),
 array([1,0]))
```

মানে

```
(0,1)

(1,0)
```

---

# Part 5 — np.argwhere()

এটি coordinate দেয়।

```python
matrix = np.array([
    [0,1],
    [3,0]
])

print(np.argwhere(matrix))
```

Output

```
[[0 1]
 [1 0]]
```

Visual

```
Row

Column
```

---

Difference

```
nonzero()

↓

Tuple
```

```
argwhere()

↓

Coordinates
```

---

# Production Example

Inventory

```python
stock = np.array([
    50,
    0,
    10,
    0,
    80
])
```

Out of Stock

```python
print(np.where(stock == 0))
```

Output

```
(array([1,3]),)
```

---

In Stock

```python
print(np.nonzero(stock))
```

Output

```
(array([0,2,4]),)
```

---

# Machine Learning Example

Image

```python
image = np.array([
    [255,0],
    [100,255]
])
```

White Pixels

```python
print(np.argwhere(image == 255))
```

Output

```
[[0 0]
 [1 1]]
```

---

# Fancy Indexing vs Slice

Slice

```python
a[1:4]
```

View

---

Fancy

```python
a[[1,2,3]]
```

Copy

⚠️ এটি খুব গুরুত্বপূর্ণ Interview Question।

---

# View vs Copy

```python
a = np.array([10,20,30])

b = a[[0,1]]

b[0] = 999

print(a)
```

Output

```
[10 20 30]
```

কারণ

Fancy Indexing

↓

Copy

---

Slice

```python
b = a[0:2]
```

↓

View

---

# Common Mistakes

## ভুল

```python
employees[0,2]
```

একটি element।

---

যদি পুরো Row দরকার

```python
employees[0]
```

---

যদি Salary Column দরকার

```python
employees[:,2]
```

---

যদি Salary > 50000

```python
employees[
    employees[:,2] > 50000
]
```

---

# Practice

## Easy

```python
a = np.array([
    10,
    20,
    30,
    40,
    50
])
```

Find

```
a[[0,2,4]]
```

---

```
np.where(a>25)
```

---

```
np.nonzero(a)
```

---

## Medium

```python
marks = np.array([
    80,
    45,
    20,
    90,
    75
])
```

Find

* Pass
* Distinction
* Fail Index

---

## Hard

```python
salary = np.array([
    25000,
    40000,
    55000,
    80000,
    120000
])
```

Tasks

* Salary >50000
* Salary between 40k and 100k
* Bonus using `np.where()`
* Index using `np.nonzero()`

---

# Interview Questions

### 1

Difference

```python
a[1:4]
```

vs

```python
a[[1,2,3]]
```

| Slice      | Fancy Index     |
| ---------- | --------------- |
| View       | Copy            |
| Continuous | Any order       |
| Faster     | Slightly slower |

---

### 2

Difference

```
where

vs

nonzero
```

* `np.where(condition)` → Condition অনুযায়ী index দেয়।
* `np.nonzero(array)` → যেসব element zero নয়, তাদের index দেয়।

---

### 3

Difference

```
nonzero

vs

argwhere
```

* `nonzero()` → Tuple of index arrays।
* `argwhere()` → Row-Column coordinate array।

---

### 4

Why use `np.where()`?

কারণ condition অনুযায়ী **select** বা **replace** দুই কাজই করা যায়।

---

# Cheat Sheet

| Function             | কাজ              |
| -------------------- | ---------------- |
| `a[[1,3]]`           | Fancy Index      |
| `arr[:,[0,2]]`       | Multiple Columns |
| `np.where(cond)`     | Index            |
| `np.where(cond,x,y)` | IF-ELSE Replace  |
| `np.nonzero(a)`      | Non-zero Index   |
| `np.argwhere(a)`     | Coordinates      |

---

# Production Mini Project

ধরো একটি e-commerce inventory dataset:

```python
inventory = np.array([
    [101, 1200, 10],
    [102, 2500, 0],
    [103, 1800, 5],
    [104, 3000, 0],
    [105, 2200, 8]
])
```

Columns:

```
ProductID
Price
Stock
```

### Tasks

1. Stock > 0 এমন সব product বের করো।
2. Out of stock product-এর row index বের করো (`np.where`)।
3. Stock > 0 product-এর index বের করো (`np.nonzero`)।
4. Price > 2000 product-এর পুরো row বের করো।
5. Stock == 0 হলে `"OUT"` এবং অন্যথায় `"IN"` status array তৈরি করো (`np.where`)।
6. শুধু `ProductID` এবং `Price` column Fancy Indexing দিয়ে বের করো।

---

# Lesson 11 Summary

আজ আমরা শিখলাম:

* ✅ Fancy Indexing
* ✅ Integer Array Indexing
* ✅ Advanced Boolean Indexing
* ✅ `np.where()`
* ✅ `np.nonzero()`
* ✅ `np.argwhere()`
* ✅ Slice (View) বনাম Fancy Indexing (Copy)

---

# পরবর্তী Lesson 12 — NumPy Reshaping & Dimension Manipulation

এখন আমরা Array-এর shape পরিবর্তন করা শিখব, যা Deep Learning, Computer Vision এবং Data Engineering-এ অত্যন্ত গুরুত্বপূর্ণ।

শিখব:

* `reshape()`
* `flatten()`
* `ravel()`
* `resize()`
* `transpose()`
* `.T`
* `expand_dims()`
* `squeeze()`

> **এটি CNN, TensorFlow, PyTorch এবং Pandas-এর জন্য অন্যতম গুরুত্বপূর্ণ Lesson।**
# Module 3 — Lesson 12: Reshaping & Dimension Manipulation (Mastery Guide)

এটি NumPy-এর সবচেয়ে গুরুত্বপূর্ণ অধ্যায়গুলোর একটি।

বাস্তব Machine Learning, Deep Learning, Computer Vision এবং Data Engineering-এ **ডেটার shape পরিবর্তন করা** খুবই সাধারণ কাজ।

উদাহরণ:

* CSV → Matrix
* Image → Vector
* Vector → Matrix
* Batch তৈরি করা
* CNN input reshape করা
* LSTM sequence তৈরি করা

এই Lesson-এর পর তুমি TensorFlow, PyTorch এবং Pandas-এর shape-related error অনেক সহজে বুঝতে পারবে।

---

# Learning Objectives

এই Lesson শেষে তুমি পারবে—

* `reshape()`
* `flatten()`
* `ravel()`
* `resize()`
* `transpose()`
* `.T`
* `expand_dims()`
* `squeeze()`
* `shape`
* `ndim`
* `size`

---

# Step 1 — Understanding Shape

প্রথমে একটি Array তৈরি করি।

```python
import numpy as np

a = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

Visual

```text
1 2 3
4 5 6
```

Shape

```python
print(a.shape)
```

Output

```text
(2, 3)
```

মানে

```text
2 Rows

3 Columns
```

---

# ndim

Dimension সংখ্যা

```python
print(a.ndim)
```

Output

```text
2
```

---

# size

মোট element

```python
print(a.size)
```

Output

```text
6
```

---

# Rule

```text
Shape

↓

Rows

Columns

↓

(2,3)

↓

6 Elements
```

---

# Part 1 — reshape()

সবচেয়ে গুরুত্বপূর্ণ function।

ধরো

```python
a = np.arange(12)

print(a)
```

Output

```text
[0 1 2 3 4 5 6 7 8 9 10 11]
```

Shape

```text
(12,)
```

---

## Reshape to 3×4

```python
b = a.reshape(3,4)

print(b)
```

Output

```text
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

Shape

```python
print(b.shape)
```

```text
(3,4)
```

---

## Reshape to 2×6

```python
print(a.reshape(2,6))
```

Output

```text
[[0 1 2 3 4 5]
 [6 7 8 9 10 11]]
```

---

## Important Rule

মোট element একই থাকতে হবে।

```text
12 Elements

↓

3×4

↓

12

✔
```

---

ভুল

```python
a.reshape(5,3)
```

Output

```text
ValueError
```

কারণ

```text
5×3

=

15

Elements
```

কিন্তু Array-তে মাত্র

```text
12
```

আছে।

---

# Auto Calculate (-1)

NumPy নিজেই Dimension বের করবে।

```python
print(a.reshape(-1,4))
```

Output

```text
[[ 0 1 2 3]
 [ 4 5 6 7]
 [ 8 9 10 11]]
```

---

আরেকটি

```python
print(a.reshape(2,-1))
```

Output

```text
[[0 1 2 3 4 5]
 [6 7 8 9 10 11]]
```

---

# Rule

শুধু **একটি** `-1` ব্যবহার করা যায়।

```python
a.reshape(-1,-1)
```

❌ Error

---

# Part 2 — flatten()

Matrix

↓

Vector

```python
a = np.array([
    [1,2,3],
    [4,5,6]
])

print(a.flatten())
```

Output

```text
[1 2 3 4 5 6]
```

Shape

```text
(6,)
```

---

## flatten() returns Copy

```python
b = a.flatten()

b[0] = 999

print(a)
```

Output

```text
Original unchanged
```

---

# Part 3 — ravel()

দেখতে একই

```python
b = a.ravel()
```

Output

```text
[1 2 3 4 5 6]
```

---

কিন্তু

```python
b[0] = 999
```

Original

```python
print(a)
```

Output

```text
[[999 2 3]
 [4 5 6]]
```

কারণ

```text
ravel()

↓

Usually View
```

> **Note:** `ravel()` সম্ভব হলে View return করে, না পারলে Copy return করতে পারে। তাই "Usually View" বলা বেশি সঠিক।

---

# Difference

| flatten | ravel        |
| ------- | ------------ |
| Copy    | Usually View |
| Slower  | Faster       |

---

# Part 4 — transpose()

Row

↓

Column

Column

↓

Row

```python
a = np.array([
    [1,2,3],
    [4,5,6]
])

print(a.T)
```

Output

```text
[[1 4]
 [2 5]
 [3 6]]
```

Shape

```text
Before

(2,3)

After

(3,2)
```

---

Equivalent

```python
print(np.transpose(a))
```

---

# Part 5 — resize()

```python
a = np.array([1,2,3,4])

a.resize((2,2))

print(a)
```

Output

```text
[[1 2]
 [3 4]]
```

---

Resize বড় করলে

```python
a = np.array([1,2,3])

a.resize((2,3))

print(a)
```

Output

```text
[[1 2 3]
 [0 0 0]]
```

নতুন জায়গা `0` দিয়ে পূরণ হয়।

> `resize()` মূল array-কে **in-place** পরিবর্তন করে।

---

# Part 6 — expand_dims()

Dimension বাড়ায়।

```python
a = np.array([1,2,3])

print(a.shape)
```

Output

```text
(3,)
```

---

Axis=0

```python
b = np.expand_dims(a, axis=0)

print(b.shape)
```

Output

```text
(1,3)
```

Visual

```text
[[1 2 3]]
```

---

Axis=1

```python
b = np.expand_dims(a, axis=1)

print(b)
```

Output

```text
[[1]
 [2]
 [3]]
```

Shape

```text
(3,1)
```

---

# Why?

Machine Learning Models

অনেক সময়

```text
(samples,

features)
```

shape চায়।

---

# Part 7 — squeeze()

Extra Dimension remove করে।

```python
a = np.array([[[5]]])

print(a.shape)
```

Output

```text
(1,1,1)
```

---

```python
print(np.squeeze(a))
```

Output

```text
5
```

Shape

```text
()
```

আরেকটি

```python
b = np.array([[1,2,3]])

print(np.squeeze(b).shape)
```

Output

```text
(3,)
```

---

# Real Data Engineering Example

CSV

```text
1000 Rows

5 Columns
```

NumPy

```python
data.shape
```

↓

```text
(1000,5)
```

Features

```python
X = data[:,1:]
```

Target

```python
y = data[:,0]
```

Model যদি `y`-কে `(1000,1)` shape চায়:

```python
y = np.expand_dims(y, axis=1)
```

---

# Machine Learning Example

Grayscale Image

```text
28×28
```

CNN চায়

```text
28×28×1
```

```python
image = np.expand_dims(image, axis=-1)
```

---

Batch

```text
32

↓

32×28×28×1
```

---

# Common Mistakes

## ❌ reshape()

```python
a.reshape(5,3)
```

Elements mismatch

---

## ❌ flatten()

অনেকে ভাবেন

View

না।

এটি Copy।

---

## ❌ transpose()

শুধু square matrix-এর জন্য নয়।

সব matrix-এ কাজ করে।

---

## ❌ resize()

Original array পরিবর্তন করে।

---

# Practice

## Easy

```python
a = np.arange(12)
```

Find

1.

```python
a.reshape(3,4)
```

2.

```python
a.reshape(2,6)
```

3.

```python
a.reshape(-1,3)
```

---

## Medium

```python
a = np.array([
    [1,2,3],
    [4,5,6]
])
```

Find

* Shape
* Size
* Transpose
* Flatten
* Ravel

---

## Hard

```python
image = np.arange(784)
```

Tasks

* Reshape to `(28,28)`
* Flatten again
* Expand channel dimension → `(28,28,1)`
* Add batch dimension → `(1,28,28,1)`

---

# Interview Questions

### 1.

Difference

```text
reshape

vs

resize
```

| reshape                | resize                  |
| ---------------------- | ----------------------- |
| Returns new view/copy  | Modifies original array |
| Same elements required | Can grow/shrink array   |

---

### 2.

Difference

```text
flatten

vs

ravel
```

| flatten | ravel        |
| ------- | ------------ |
| Copy    | Usually View |

---

### 3.

Why use `-1`?

**উত্তর:** NumPy-কে একটি dimension স্বয়ংক্রিয়ভাবে হিসাব করতে দেওয়ার জন্য।

---

### 4.

Difference

```text
.T

vs

transpose()
```

দুটিই transpose করে। `.T` হলো property, আর `np.transpose()` হলো function।

---

### 5.

When use `expand_dims()`?

* CNN Input
* Batch Creation
* Feature Matrix
* Model Input Shape

---

# Cheat Sheet

| Function        | কাজ                    |
| --------------- | ---------------------- |
| `.shape`        | Array shape            |
| `.ndim`         | Number of dimensions   |
| `.size`         | Total elements         |
| `reshape()`     | Shape পরিবর্তন         |
| `flatten()`     | Copy করে 1D            |
| `ravel()`       | Usually View করে 1D    |
| `.T`            | Transpose              |
| `transpose()`   | Transpose              |
| `resize()`      | Original array resize  |
| `expand_dims()` | Dimension যোগ          |
| `squeeze()`     | Size-1 dimension সরায় |

---

# Production Mini Project

একটি image dataset:

```python
import numpy as np

images = np.arange(32 * 28 * 28)
```

Tasks:

1. `images`-কে `(32, 28, 28)` shape-এ reshape করো।
2. প্রথম image বের করো।
3. প্রথম image-তে channel dimension যোগ করে `(28, 28, 1)` বানাও।
4. সব image-কে flatten করে `(32, 784)` shape বানাও।
5. প্রথম image transpose করো।
6. `flatten()` এবং `ravel()` ব্যবহার করে পার্থক্য পরীক্ষা করো (একটিতে পরিবর্তন করলে original বদলায় কি না দেখো)।

---

# Lesson 12 Summary

আজ আমরা শিখলাম:

* ✅ `shape`
* ✅ `ndim`
* ✅ `size`
* ✅ `reshape()`
* ✅ `flatten()`
* ✅ `ravel()`
* ✅ `resize()`
* ✅ `transpose()` / `.T`
* ✅ `expand_dims()`
* ✅ `squeeze()`

---

# পরবর্তী Lesson 13 — Stacking & Splitting Arrays

Lesson 13-এ আমরা শিখব:

* `np.concatenate()`
* `np.vstack()`
* `np.hstack()`
* `np.dstack()`
* `np.column_stack()`
* `np.row_stack()`
* `np.split()`
* `np.hsplit()`
* `np.vsplit()`

এগুলো Data Engineering-এ multiple datasets merge করা, feature matrix তৈরি করা এবং data pipeline তৈরির জন্য অত্যন্ত গুরুত্বপূর্ণ।

# Module 3 — Lesson 13: Stacking & Splitting Arrays (Mastery Guide)

এটি Data Engineering এবং Machine Learning-এর জন্য অত্যন্ত গুরুত্বপূর্ণ একটি Lesson।

বাস্তব প্রজেক্টে তোমাকে প্রায়ই একাধিক dataset একসাথে **merge** করতে হবে, আবার বড় dataset-কে ছোট ছোট অংশে **split** করতে হবে।

উদাহরণ:

* দুইটি CSV merge করা
* Feature matrix তৈরি করা
* Train/Test data আলাদা করা
* Image channels combine করা
* Batch তৈরি করা

এসব কাজের জন্য NumPy-এর stacking এবং splitting functions ব্যবহার করা হয়।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে—

* `np.concatenate()`
* `np.vstack()`
* `np.hstack()`
* `np.dstack()`
* `np.column_stack()`
* `np.row_stack()`
* `np.split()`
* `np.hsplit()`
* `np.vsplit()`
* `np.array_split()`

---

# Part 1 — concatenate()

এটি সবচেয়ে বেশি ব্যবহৃত function।

## 1D Example

```python
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

c = np.concatenate((a, b))

print(c)
```

Output

```text
[1 2 3 4 5 6]
```

---

## 2D Example (Rows)

```python
a = np.array([
    [1,2],
    [3,4]
])

b = np.array([
    [5,6],
    [7,8]
])

print(np.concatenate((a, b), axis=0))
```

Output

```text
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
```

Shape

```text
(4,2)
```

---

## Concatenate Columns

```python
print(np.concatenate((a,b), axis=1))
```

Output

```text
[[1 2 5 6]
 [3 4 7 8]]
```

Shape

```text
(2,4)
```

---

# Rule

`axis=0`

↓

Rows বাড়ে

`axis=1`

↓

Columns বাড়ে

---

# Part 2 — vstack()

Vertical Stack

এটি `concatenate(axis=0)`-এর shortcut।

```python
print(np.vstack((a,b)))
```

Output

```text
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
```

---

# Part 3 — hstack()

Horizontal Stack

```python
print(np.hstack((a,b)))
```

Output

```text
[[1 2 5 6]
 [3 4 7 8]]
```

---

# Difference

| Function   | Direction    |
| ---------- | ------------ |
| `vstack()` | Up → Down    |
| `hstack()` | Left → Right |

---

# Part 4 — column_stack()

ধরো

```python
name_id = np.array([101,102,103])

salary = np.array([30000,40000,50000])
```

Column বানাতে

```python
result = np.column_stack((name_id,salary))

print(result)
```

Output

```text
[[  101 30000]
 [  102 40000]
 [  103 50000]]
```

Production-এ এটি খুব common।

---

# Part 5 — row_stack()

```python
print(np.row_stack((a,b)))
```

Output

```text
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
```

> **Note:** `np.row_stack()` কার্যত `vstack()`-এর মতোই কাজ করে। নতুন কোডে `vstack()` ব্যবহার করাই বেশি প্রচলিত।

---

# Part 6 — dstack()

Depth Stack

```python
x = np.array([[1,2]])

y = np.array([[3,4]])

print(np.dstack((x,y)))
```

Output

```text
[[[1 3]
  [2 4]]]
```

Shape

```python
print(np.dstack((x,y)).shape)
```

Output

```text
(1,2,2)
```

এটি Image Processing-এ ব্যবহৃত হয়।

---

# Part 7 — split()

একটি array-কে সমান ভাগে ভাগ করা।

```python
a = np.arange(12)

parts = np.split(a,3)

print(parts)
```

Output

```text
[array([0,1,2,3]),
 array([4,5,6,7]),
 array([8,9,10,11])]
```

---

# Part 8 — array_split()

যদি সমানভাবে ভাগ না হয়

```python
a = np.arange(10)

parts = np.array_split(a,3)

print(parts)
```

Output

```text
[array([0,1,2,3]),
 array([4,5,6]),
 array([7,8,9])]
```

`array_split()` অসমান ভাগও করতে পারে।

---

# Difference

| Function        | Equal Split Required |
| --------------- | -------------------- |
| `split()`       | ✅ Yes                |
| `array_split()` | ❌ No                 |

---

# Part 9 — hsplit()

Column অনুযায়ী ভাগ।

```python
a = np.array([
    [1,2,3,4],
    [5,6,7,8]
])

parts = np.hsplit(a,2)

print(parts)
```

Output

```text
[array([[1,2],
        [5,6]]),

 array([[3,4],
        [7,8]])]
```

---

# Part 10 — vsplit()

Row অনুযায়ী ভাগ।

```python
a = np.array([
    [1,2],
    [3,4],
    [5,6],
    [7,8]
])

parts = np.vsplit(a,2)

print(parts)
```

Output

```text
[array([[1,2],
        [3,4]]),

 array([[5,6],
        [7,8]])]
```

---

# Real Data Engineering Example

ধরো দুটি CSV থেকে data এসেছে।

```python
customers = np.array([
    [101],
    [102],
    [103]
])

salary = np.array([
    [30000],
    [40000],
    [50000]
])
```

Merge

```python
data = np.hstack((customers,salary))

print(data)
```

Output

```text
[[101 30000]
 [102 40000]
 [103 50000]]
```

---

# Machine Learning Example

Features

```python
height = np.array([170,180,160])

weight = np.array([65,75,55])
```

Feature Matrix

```python
X = np.column_stack((height,weight))

print(X)
```

Output

```text
[[170 65]
 [180 75]
 [160 55]]
```

---

# Image Example

Red

Green

Blue

```python
red = np.array([[255]])

green = np.array([[100]])

blue = np.array([[50]])
```

RGB Image

```python
rgb = np.dstack((red,green,blue))

print(rgb)
```

Output

```text
[[[255 100 50]]]
```

---

# Common Mistakes

## ❌ Different Shape

```python
a = np.array([[1,2]])

b = np.array([[3,4,5]])

np.vstack((a,b))
```

Error

কারণ column সংখ্যা এক নয়।

---

## ❌ Wrong Axis

```python
np.concatenate((a,b),axis=1)
```

সবসময় shape check করবে।

```python
print(a.shape)
```

---

## ❌ split()

```python
np.split(np.arange(10),3)
```

Error

কারণ

10

÷3

সমান ভাগ হয় না।

---

# Practice

## Easy

```python
a = np.array([1,2,3])

b = np.array([4,5,6])
```

Tasks

* concatenate
* hstack
* vstack

---

## Medium

```python
a = np.array([
    [1,2],
    [3,4]
])

b = np.array([
    [5,6],
    [7,8]
])
```

Tasks

* concatenate axis=0
* concatenate axis=1
* hstack
* vstack

---

## Hard

```python
features = np.array([
    [170],
    [180],
    [160]
])

salary = np.array([
    [50000],
    [70000],
    [45000]
])

age = np.array([
    [25],
    [30],
    [22]
])
```

Tasks

1. Feature Matrix তৈরি করো।
2. ৩টি column merge করো।
3. Dataset-কে ২ ভাগে split করো।
4. শুধু salary column আলাদা করো।
5. Feature Matrix transpose করো।

---

# Interview Questions

### 1.

Difference

| `concatenate()`          | `stack()`          |
| ------------------------ | ------------------ |
| Existing axis-এ join করে | নতুন axis তৈরি করে |

> `np.stack()` আমরা পরের Lesson-এ বিস্তারিত শিখব।

---

### 2.

Difference

| `hstack()`      | `vstack()`   |
| --------------- | ------------ |
| Columns বাড়ায় | Rows বাড়ায় |

---

### 3.

Difference

| `split()`        | `array_split()`       |
| ---------------- | --------------------- |
| Equal split only | Unequal split allowed |

---

### 4.

When use `column_stack()`?

যখন একাধিক 1D feature combine করে একটি feature matrix বানাতে হয়।

---

### 5.

When use `dstack()`?

Image Processing, RGB channels, এবং 3D data combine করতে।

---

# Cheat Sheet

| Function         | কাজ                                  |
| ---------------- | ------------------------------------ |
| `concatenate()`  | Existing axis-এ join                 |
| `vstack()`       | Vertical join                        |
| `hstack()`       | Horizontal join                      |
| `column_stack()` | 1D → Columns                         |
| `row_stack()`    | Rows combine (`vstack()`-এর সমতুল্য) |
| `dstack()`       | Depth combine                        |
| `split()`        | Equal split                          |
| `array_split()`  | Unequal split                        |
| `hsplit()`       | Column split                         |
| `vsplit()`       | Row split                            |

---

# Production Mini Project

একটি HR dataset:

```python
import numpy as np

emp_id = np.array([[101],[102],[103],[104]])

age = np.array([[25],[30],[35],[40]])

salary = np.array([[30000],[45000],[60000],[80000]])
```

Tasks:

1. `emp_id`, `age`, `salary` merge করে একটি `(4,3)` matrix তৈরি করো।
2. Dataset-কে `age` এবং `salary` অংশে `hsplit()` ব্যবহার করে ভাগ করো।
3. প্রথম ২ জন employee এবং শেষ ২ জন employee আলাদা করো (`vsplit()` ব্যবহার করে)।
4. Salary column-এর average বের করো।
5. Salary অনুযায়ী descending order-এ sort করার প্রস্তুতি হিসেবে salary column আলাদা করে নাও (sorting আমরা পরের মডিউলে শিখব)।

---

# Lesson 13 Summary

আজ আমরা শিখলাম:

* ✅ `concatenate()`
* ✅ `vstack()`
* ✅ `hstack()`
* ✅ `column_stack()`
* ✅ `row_stack()`
* ✅ `dstack()`
* ✅ `split()`
* ✅ `array_split()`
* ✅ `hsplit()`
* ✅ `vsplit()`

---

# পরবর্তী Lesson 14 — Broadcasting (NumPy-এর Superpower)

এটি NumPy-এর সবচেয়ে শক্তিশালী feature-গুলোর একটি। আমরা শিখব:

* Broadcasting Rules
* Shape Compatibility
* Scalar Broadcasting
* Vector Broadcasting
* Matrix Broadcasting
* Practical ML Examples
* Broadcasting Errors
* Performance Optimization

> **Broadcasting ভালোভাবে বুঝতে পারলে তুমি NumPy-এর ৮০% vectorized code সহজেই পড়তে এবং লিখতে পারবে।**

# Module 3 — Lesson 14: Broadcasting (NumPy-এর Superpower)

Broadcasting হলো NumPy-এর সবচেয়ে শক্তিশালী এবং সবচেয়ে বেশি ব্যবহৃত feature।

যদি Broadcasting না বুঝো, তাহলে TensorFlow, PyTorch, Pandas, Scikit-learn-এর অনেক code বুঝতে সমস্যা হবে।

Production Data Engineering এবং Machine Learning-এ এটি প্রতিদিন ব্যবহৃত হয়।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে—

* Broadcasting কী
* Broadcasting Rules
* Scalar Broadcasting
* Vector Broadcasting
* Matrix Broadcasting
* Shape Compatibility
* Broadcasting Errors
* Performance Benefits
* Real ML Examples

---

# What is Broadcasting?

Broadcasting হলো এমন একটি mechanism যার মাধ্যমে **ভিন্ন shape-এর array-এর মধ্যে arithmetic operation করা যায়**, যদি তাদের shape compatible হয়।

উদাহরণ:

```python
import numpy as np

a = np.array([10, 20, 30])

print(a + 5)
```

Output

```text
[15 25 35]
```

প্রশ্ন:

`5` কি `[5,5,5]` হয়ে গেছে?

**Conceptually হ্যাঁ**, NumPy এমনভাবে আচরণ করে।

বাস্তবে NumPy **নতুন array তৈরি না করেই** broadcasting ব্যবহার করে operation করে। এ কারণেই এটি দ্রুত।

---

# Rule 1 — Scalar Broadcasting

```python
a = np.array([1,2,3,4])

print(a * 10)
```

Output

```text
[10 20 30 40]
```

Visual

```text
[1 2 3 4]

×

10

↓

[10 20 30 40]
```

---

# Matrix + Scalar

```python
matrix = np.array([
    [1,2],
    [3,4]
])

print(matrix + 100)
```

Output

```text
[[101 102]
 [103 104]]
```

---

# Rule 2 — Same Shape

```python
a = np.array([1,2,3])

b = np.array([10,20,30])

print(a + b)
```

Output

```text
[11 22 33]
```

Element-wise Operation

```text
1+10

2+20

3+30
```

---

# Rule 3 — Different Shape

সব broadcasting সম্ভব নয়।

NumPy shape compare করে **ডান দিক (rightmost dimension)** থেকে।

---

## Example

```python
a = np.array([
    [1],
    [2],
    [3]
])

print(a.shape)
```

Output

```text
(3,1)
```

---

```python
b = np.array([10,20,30])
```

Shape

```text
(3,)
```

---

Operation

```python
print(a + b)
```

Output

```text
[[11 21 31]
 [12 22 32]
 [13 23 33]]
```

---

Visual

```text
a

[[1]
 [2]
 [3]]

+

b

[10 20 30]

↓

[[11 21 31]
 [12 22 32]
 [13 23 33]]
```

---

# Why?

NumPy internally treats shapes like:

```text
a

(3,1)

b

(1,3)

↓

Result

(3,3)
```

---

# Broadcasting Rules (Must Memorize)

NumPy compares dimensions from **right to left**.

দুটি dimension compatible যদি—

1. Equal হয়
2. একটি dimension `1` হয়

---

## Examples

### Compatible

```text
(5,3)

(5,3)
```

✔

---

```text
(5,1)

(5,3)
```

✔

---

```text
(1,3)

(5,3)
```

✔

---

```text
(3,)

(5,3)
```

NumPy এটিকে `(1,3)` হিসেবে বিবেচনা করে।

✔

---

## Not Compatible

```text
(4,3)

(5,3)
```

❌

কারণ

```text
4

≠

5
```

এবং কোনোটিই `1` নয়।

---

# Broadcasting Error

```python
a = np.array([
    [1,2],
    [3,4]
])

b = np.array([
    10,
    20,
    30
])

print(a + b)
```

Output

```text
ValueError:
operands could not be broadcast together
```

কারণ

```text
a

(2,2)

b

(3,)
```

Compatible নয়।

---

# Column-wise Broadcasting

Salary

```python
salary = np.array([
    [30000],
    [40000],
    [50000]
])
```

Tax

```python
tax = np.array([
    1000,
    2000,
    3000
])
```

```python
print(salary + tax)
```

Output

```text
[[31000 32000 33000]
 [41000 42000 43000]
 [51000 52000 53000]]
```

---

# Row-wise Broadcasting

```python
matrix = np.array([
    [10,20,30],
    [40,50,60]
])

bonus = np.array([
    100,
    200,
    300
])

print(matrix + bonus)
```

Output

```text
[[110 220 330]
 [140 250 360]]
```

---

# Broadcasting with Multiplication

```python
price = np.array([
    100,
    200,
    300
])

discount = 0.90

print(price * discount)
```

Output

```text
[ 90. 180. 270.]
```

---

# Broadcasting with Division

```python
marks = np.array([
    80,
    90,
    70
])

print(marks / 100)
```

Output

```text
[0.8 0.9 0.7]
```

Normalization-এর জন্য এটি খুব common।

---

# Broadcasting with Images

Grayscale Image

```python
image = np.array([
    [100,150],
    [200,250]
])
```

Brightness বাড়ানো

```python
bright = image + 20
```

Output

```text
[[120 170]
 [220 255]]
```

> বাস্তবে image processing-এ `uint8` overflow সম্পর্কে সতর্ক থাকতে হয়। সাধারণত `np.clip()` ব্যবহার করা হয়।

---

# Production Example

Product Price

```python
price = np.array([
    1000,
    1500,
    2000
])
```

VAT

```python
vat = 1.15
```

```python
final = price * vat

print(final)
```

Output

```text
[1150. 1725. 2300.]
```

---

# Machine Learning Example

Feature Scaling

```python
X = np.array([
    [170,65],
    [180,75],
    [160,55]
])
```

Mean

```python
mean = np.mean(X, axis=0)

print(mean)
```

Output

```text
[170. 65.]
```

Scaling

```python
centered = X - mean
```

Output

```text
[[  0   0]
 [ 10  10]
 [-10 -10]]
```

এখানে `mean` vector পুরো matrix-এর প্রতিটি row-তে broadcast হয়েছে।

---

# Performance Advantage

### Traditional Python

```python
result = []

for x in a:
    result.append(x + 10)
```

---

### NumPy Broadcasting

```python
result = a + 10
```

NumPy-এর version অনেক দ্রুত, কারণ loop Python-এ নয়, C-level implementation-এ চলে।

---

# Common Mistakes

## ❌ Shape না দেখে Operation করা

```python
print(a.shape)
print(b.shape)
```

সবসময় আগে shape check করো।

---

## ❌ Broadcasting মানে Copy মনে করা

Broadcasting সাধারণত **conceptually expand** করে।

বাস্তবে NumPy অপ্রয়োজনীয় memory copy এড়িয়ে চলে।

---

## ❌ Wrong Dimension

```python
(3,2)

+

(4,)
```

❌ Compatible নয়।

---

# Broadcasting Compatibility Cheat

| Shape A | Shape B | Result    |
| ------- | ------- | --------- |
| `(3,)`  | `(3,)`  | ✅         |
| `(3,1)` | `(3,)`  | ✅ `(3,3)` |
| `(2,3)` | `(3,)`  | ✅ `(2,3)` |
| `(2,3)` | `(2,1)` | ✅ `(2,3)` |
| `(2,3)` | `(4,)`  | ❌         |

---

# Practice

## Easy

```python
a = np.array([10,20,30])
```

Tasks

```python
a + 5
```

```python
a * 2
```

```python
a / 10
```

---

## Medium

```python
matrix = np.array([
    [1,2,3],
    [4,5,6]
])

vector = np.array([
    10,
    20,
    30
])
```

Tasks

* Add vector
* Multiply by 10
* Divide by 2

---

## Hard

```python
salary = np.array([
    [30000],
    [45000],
    [60000]
])

bonus = np.array([
    1000,
    2000,
    3000
])
```

Tasks

1. Add salary and bonus
2. Add 10% increment
3. Normalize salary by dividing by 1000
4. Explain the resulting shapes

---

# Interview Questions

### 1.

What is Broadcasting?

**Answer:** NumPy-এর এমন একটি mechanism যা compatible shape-এর array-এর মধ্যে element-wise operation করতে দেয়, ছোট array-কে conceptually expand করে।

---

### 2.

Broadcasting Rules?

দুটি dimension compatible যদি—

* Equal হয়
* অথবা একটি `1` হয়

---

### 3.

NumPy কোন দিক থেকে shape compare করে?

**Answer:** Rightmost dimension (ডান দিক) থেকে।

---

### 4.

Difference

```python
a + 5
```

vs

```python
a + np.array([5,5,5])
```

ফলাফল একই হতে পারে, কিন্তু scalar broadcasting বেশি efficient।

---

### 5.

Why is Broadcasting Fast?

কারণ NumPy C-implemented vectorized operations ব্যবহার করে এবং অপ্রয়োজনীয় data copy এড়ায়।

---

# Cheat Sheet

| Operation        | Example           |
| ---------------- | ----------------- |
| Scalar Broadcast | `a + 5`           |
| Multiply         | `a * 10`          |
| Matrix + Vector  | `matrix + vector` |
| Normalize        | `X / 255`         |
| Center Data      | `X - mean`        |

---

# Production Mini Project

একটি e-commerce dataset:

```python
import numpy as np

products = np.array([
    [1000, 5],
    [1500, 10],
    [2000, 7]
])
```

Columns:

* Column 0 = Price
* Column 1 = Quantity

Tasks:

1. সব Product-এর Price-এ ১৫% VAT যোগ করো।
2. সব Quantity দ্বিগুণ করো।
3. Price column-কে ১০০০ দিয়ে divide করে হাজার টাকায় convert করো।
4. প্রতিটি Product-এর মোট Revenue বের করো (`Price × Quantity`)।
5. Revenue-এর average বের করো।

---

# Lesson 14 Summary

আজ আমরা শিখলাম:

* ✅ Broadcasting কী
* ✅ Scalar Broadcasting
* ✅ Vector Broadcasting
* ✅ Matrix Broadcasting
* ✅ Broadcasting Rules
* ✅ Shape Compatibility
* ✅ Broadcasting Errors
* ✅ Performance Benefits
* ✅ Real-world ML এবং Data Engineering examples

---

# পরবর্তী Lesson 15 — Universal Functions (UFuncs)

এটি NumPy-এর আরেকটি শক্তিশালী অংশ। আমরা শিখব:

* `np.sqrt()`
* `np.square()`
* `np.power()`
* `np.exp()`
* `np.log()`
* `np.sin()`
* `np.cos()`
* `np.tan()`
* `np.abs()`
* `np.round()`
* `np.floor()`
* `np.ceil()`

এই Lesson-এর পর তুমি vectorized mathematical computation দক্ষভাবে করতে পারবে, যা Data Engineering, Scientific Computing এবং Machine Learning-এ অত্যন্ত গুরুত্বপূর্ণ।

# Module 3 — Lesson 15: Universal Functions (UFuncs) — Zero to Mastery

এটি NumPy-এর সবচেয়ে শক্তিশালী feature-গুলোর একটি।

**Universal Functions (UFuncs)** হলো এমন function যেগুলো **পুরো array-এর প্রতিটি element-এর উপর একসাথে operation করে।**

এগুলো এতটাই optimized যে Python loop-এর তুলনায় অনেক দ্রুত কাজ করে।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে—

* UFunc কী
* Unary vs Binary UFunc
* `np.sqrt()`
* `np.square()`
* `np.power()`
* `np.exp()`
* `np.log()`
* `np.log10()`
* `np.sin()`
* `np.cos()`
* `np.tan()`
* `np.abs()`
* `np.round()`
* `np.floor()`
* `np.ceil()`
* `np.clip()`
* `np.maximum()`
* `np.minimum()`

---

# What is a UFunc?

ধরো,

```python
numbers = np.array([1, 4, 9, 16])
```

Python Loop

```python
result = []

for x in numbers:
    result.append(x ** 0.5)
```

NumPy

```python
np.sqrt(numbers)
```

দুইটিই একই কাজ করে।

কিন্তু NumPy version অনেক দ্রুত।

---

# UFunc Types

## Unary UFunc

একটি array লাগে।

```
sqrt()

log()

sin()

abs()
```

---

## Binary UFunc

দুটি array লাগে।

```
add()

subtract()

multiply()

divide()

maximum()
```

---

# Dataset

```python
import numpy as np

a = np.array([
    1,
    4,
    9,
    16,
    25
])
```

---

# Part 1 — sqrt()

```python
print(np.sqrt(a))
```

Output

```text
[1. 2. 3. 4. 5.]
```

---

Production Example

Distance

```
Distance Formula

↓

sqrt(x²+y²)
```

---

# Part 2 — square()

```python
print(np.square(a))
```

Output

```text
[  1  16  81 256 625]
```

Equivalent

```python
a**2
```

---

# Part 3 — power()

```python
print(np.power(a,3))
```

Output

```text
[    1
    64
   729
  4096
 15625]
```

---

# Part 4 — exp()

Mathematics

```
e^x
```

```python
x = np.array([
    1,
    2,
    3
])

print(np.exp(x))
```

Output

```text
[ 2.718...

7.389...

20.085...]
```

Machine Learning-এ Softmax, Logistic Regression ইত্যাদিতে ব্যবহৃত হয়।

---

# Part 5 — log()

Natural Log

```python
x = np.array([
    1,
    10,
    100
])

print(np.log(x))
```

Output

```text
[0.

2.302

4.605]
```

---

## log10()

```python
print(np.log10(x))
```

Output

```text
[0.

1.

2.]
```

---

⚠️ গুরুত্বপূর্ণ

```python
np.log(0)
```

↓

```
-inf
```

কারণ

```
log(0)

Undefined
```

Production-এ সাধারণত `np.clip()` ব্যবহার করে `0` এড়ানো হয়।

---

# Part 6 — abs()

```python
x = np.array([
    -10,
    20,
    -30
])

print(np.abs(x))
```

Output

```text
[10 20 30]
```

---

# Part 7 — round()

```python
x = np.array([
    2.123,
    5.678,
    7.999
])

print(np.round(x,2))
```

Output

```text
[2.12

5.68

8.00]
```

---

# Part 8 — floor()

সবসময় নিচের পূর্ণসংখ্যা।

```python
x = np.array([
    2.9,
    5.2,
    7.8
])

print(np.floor(x))
```

Output

```text
[2.

5.

7.]
```

---

# Part 9 — ceil()

সবসময় উপরের পূর্ণসংখ্যা।

```python
print(np.ceil(x))
```

Output

```text
[3.

6.

8.]
```

---

# Difference

| Function      | Result                                       |
| ------------- | -------------------------------------------- |
| `floor(2.9)`  | 2                                            |
| `ceil(2.1)`   | 3                                            |
| `round(2.49)` | 2                                            |
| `round(2.50)` | 2 *(NumPy uses bankers rounding by default)* |

> **Note:** NumPy-এর `round()` সাধারণত "round half to even" (banker's rounding) ব্যবহার করে। তাই `2.5 → 2` এবং `3.5 → 4` হতে পারে।

---

# Part 10 — Trigonometric Functions

Radians ব্যবহার করে।

```python
angle = np.array([
    0,
    np.pi/2,
    np.pi
])
```

---

## sin()

```python
print(np.sin(angle))
```

Output

```text
[0.

1.

0.]
```

---

## cos()

```python
print(np.cos(angle))
```

Output

```text
[1.

0.

-1.]
```

---

## tan()

```python
print(np.tan(angle))
```

---

# Part 11 — clip()

Production-এ খুব common।

```python
score = np.array([
    -5,
    50,
    120
])

print(np.clip(score,0,100))
```

Output

```text
[0

50

100]
```

---

# Why?

Negative Score

↓

0

---

Score >100

↓

100

---

Machine Learning

Pixel Values

```
0

↓

255
```

---

# Part 12 — maximum()

```python
a = np.array([
    10,
    50,
    30
])

b = np.array([
    20,
    40,
    35
])

print(np.maximum(a,b))
```

Output

```text
[20

50

35]
```

---

# minimum()

```python
print(np.minimum(a,b))
```

Output

```text
[10

40

30]
```

---

# Real Data Engineering Example

Temperature

```python
temp = np.array([
    25,
    31,
    42,
    38
])
```

Cap Temperature

```python
safe = np.clip(temp,0,40)
```

Output

```text
[25

31

40

38]
```

---

# Machine Learning Example

Normalize Image

```python
image = np.array([
    [0,255],
    [120,200]
])
```

```python
image = image / 255
```

Output

```text
0

↓

1
```

---

Feature Engineering

```python
salary = np.array([
    30000,
    40000,
    50000
])

log_salary = np.log(salary)
```

Log transform skewed data কমাতে সাহায্য করে।

---

# Performance Comparison

Python Loop

```python
result = []

for x in a:
    result.append(x*x)
```

NumPy

```python
result = np.square(a)
```

NumPy version অনেক দ্রুত এবং কম memory overhead তৈরি করে।

---

# Common Mistakes

## ❌ log(0)

```python
np.log(0)
```

↓

```
-inf
```

সমাধান

```python
safe = np.clip(a,1e-9,None)

np.log(safe)
```

---

## ❌ Trigonometric Function

Degrees নয়।

Radians।

যদি degree থাকে:

```python
degree = np.array([0,90,180])

radian = np.deg2rad(degree)

print(np.sin(radian))
```

---

## ❌ floor vs round

```
floor

↓

Always Down
```

```
round

↓

Nearest
```

---

# Practice

## Easy

```python
a = np.array([
    4,
    9,
    16,
    25
])
```

Tasks

* sqrt
* square
* power 3

---

## Medium

```python
x = np.array([
    2.4,
    5.7,
    8.9
])
```

Tasks

* round
* floor
* ceil

---

## Hard

```python
salary = np.array([
    30000,
    50000,
    80000,
    120000
])
```

Tasks

1. Log Transform
2. Square Root
3. Salary Cap = 100000
4. Normalize (salary / max salary)

---

# Interview Questions

### 1.

What is UFunc?

একটি highly optimized vectorized function যা পুরো array-এর প্রতিটি element-এর উপর operation করে।

---

### 2.

Difference

| Unary     | Binary     |
| --------- | ---------- |
| One input | Two inputs |

---

### 3.

Difference

| floor       | ceil      |
| ----------- | --------- |
| নিচে নামায় | উপরে তোলে |

---

### 4.

Why use `clip()`?

Outlier control, pixel range, score validation, numerical stability-এর জন্য।

---

### 5.

Why use `log()` in ML?

Skewed data কমাতে এবং কিছু model-এর জন্য distribution আরও উপযোগী করতে।

---

# Cheat Sheet

| Function       | কাজ                  |
| -------------- | -------------------- |
| `np.sqrt()`    | Square Root          |
| `np.square()`  | Square               |
| `np.power()`   | Power                |
| `np.exp()`     | e^x                  |
| `np.log()`     | Natural Log          |
| `np.log10()`   | Base-10 Log          |
| `np.sin()`     | Sine                 |
| `np.cos()`     | Cosine               |
| `np.tan()`     | Tangent              |
| `np.abs()`     | Absolute             |
| `np.round()`   | Round                |
| `np.floor()`   | Floor                |
| `np.ceil()`    | Ceil                 |
| `np.clip()`    | Limit Values         |
| `np.maximum()` | Element-wise Maximum |
| `np.minimum()` | Element-wise Minimum |

---

# Production Mini Project

ধরো একটি e-commerce pricing dataset:

```python
import numpy as np

price = np.array([
    1200,
    2500,
    1800,
    3500,
    5000
])

discount = np.array([
    100,
    200,
    150,
    500,
    1000
])
```

Tasks:

1. Final price = `price - discount`
2. Final price কখনো `0`-এর নিচে যাবে না (`np.clip()` ব্যবহার করো)
3. Discount percentage বের করো
4. Price-এর `log` transform করো
5. Final price nearest integer-এ round করো
6. `np.maximum()` ব্যবহার করে প্রতিটি product-এর জন্য minimum selling price `1500` নিশ্চিত করো

---

# Lesson 15 Summary

আজ আমরা শিখলাম:

* ✅ Universal Functions (UFuncs)
* ✅ `sqrt()`
* ✅ `square()`
* ✅ `power()`
* ✅ `exp()`
* ✅ `log()` / `log10()`
* ✅ `sin()` / `cos()` / `tan()`
* ✅ `abs()`
* ✅ `round()`
* ✅ `floor()`
* ✅ `ceil()`
* ✅ `clip()`
* ✅ `maximum()` / `minimum()`
* ✅ Production ও Machine Learning-এ UFunc-এর ব্যবহার

---

# 🎯 পরবর্তী Module (Lesson 16)

এখন আমরা **NumPy Sorting, Searching & Statistics** শুরু করব।

সেখানে শিখব:

* `np.sort()`
* `np.argsort()`
* `np.lexsort()`
* `np.unique()`
* `np.bincount()`
* `np.searchsorted()`
* `np.percentile()`
* `np.quantile()`
* `np.corrcoef()`
* `np.cov()`

এগুলো Data Engineering, Feature Engineering, এবং Data Analysis-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।


# Module 4 — Lesson 16: NumPy Sorting, Searching & Statistics (Mastery Guide)

এখন থেকে আমরা NumPy-এর **Data Analysis ও Data Processing অংশে** প্রবেশ করছি।

বাস্তব Data Engineering এবং Machine Learning pipeline-এ তোমাকে প্রতিদিন করতে হয়:

* Data sort করা
* Top-K value বের করা
* Duplicate remove করা
* Frequency count করা
* Median/Percentile বের করা
* Feature correlation বের করা

এই Lesson-এ এগুলো শিখব।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* `np.sort()`
* `np.argsort()`
* `np.lexsort()`
* `np.unique()`
* `np.bincount()`
* `np.searchsorted()`
* `np.percentile()`
* `np.quantile()`
* `np.mean()`
* `np.median()`
* `np.std()`
* `np.var()`
* `np.corrcoef()`
* `np.cov()`

---

# Part 1 — np.sort()

Array sort করার জন্য।

---

## 1D Sorting

```python
import numpy as np

scores = np.array([
    90,
    70,
    85,
    60,
    95
])

print(np.sort(scores))
```

Output:

```text
[60 70 85 90 95]
```

---

## Descending Sort

NumPy direct descending দেয় না।

Method:

```python
sorted_scores = np.sort(scores)[::-1]

print(sorted_scores)
```

Output:

```text
[95 90 85 70 60]
```

---

# Important

`np.sort()` original array পরিবর্তন করে না।

Example:

```python
print(scores)
```

Output:

```text
[90 70 85 60 95]
```

---

# In-place Sorting

```python
scores.sort()

print(scores)
```

Output:

```text
[60 70 85 90 95]
```

Difference:

| np.sort()            | array.sort()        |
| -------------------- | ------------------- |
| New array return করে | Original modify করে |

---

# Part 2 — 2D Sorting

Dataset:

```python
employees = np.array([
    [101,50000],
    [102,30000],
    [103,70000],
    [104,40000]
])
```

---

## Sort rows

```python
print(np.sort(employees, axis=0))
```

Output:

```text
[
[101 30000]
[102 40000]
[103 50000]
[104 70000]
]
```

---

## Column অনুযায়ী Sort

Salary column:

```python
print(
    employees[
        employees[:,1].argsort()
    ]
)
```

Output:

```text
[
[102 30000]
[104 40000]
[101 50000]
[103 70000]
]
```

---

# Part 3 — np.argsort()

`argsort()` value না দিয়ে index return করে।

Example:

```python
a = np.array([
    50,
    20,
    80,
    10
])


print(np.argsort(a))
```

Output:

```text
[3 1 0 2]
```

Meaning:

```
index 3 → 10
index 1 → 20
index 0 → 50
index 2 → 80
```

---

# Why Important?

Machine Learning-এ:

* Top prediction বের করতে
* Ranking তৈরি করতে
* Recommendation system

ব্যবহার হয়।

---

Example:

Model Prediction:

```python
prob = np.array([
    0.2,
    0.9,
    0.5,
    0.8
])
```

Top index:

```python
idx = np.argsort(prob)[::-1]

print(idx)
```

Output:

```text
[1 3 2 0]
```

---

# Part 4 — np.lexsort()

Multiple column অনুযায়ী sorting।

Example:

```python
students = np.array([
    [90,20],
    [80,22],
    [90,18],
    [70,21]
])
```

Columns:

```
Score
Age
```

---

Score তারপর Age অনুযায়ী:

```python
index = np.lexsort(
    (
        students[:,1],
        students[:,0]
    )
)

print(students[index])
```

Output:

```text
[
[70 21]
[80 22]
[90 18]
[90 20]
]
```

---

# Part 5 — np.unique()

Duplicate remove করে।

```python
a = np.array([
    10,
    20,
    10,
    30,
    20
])

print(np.unique(a))
```

Output:

```text
[10 20 30]
```

---

## Count Frequency

```python
values, counts = np.unique(
    a,
    return_counts=True
)


print(values)
print(counts)
```

Output:

```
[10 20 30]

[2 2 1]
```

---

Real Example:

Class labels:

```python
labels = np.array([
    0,1,1,0,2,1
])
```

```python
np.unique(
    labels,
    return_counts=True
)
```

Output:

```
classes:

[0 1 2]


count:

[2 3 1]
```

---

# Part 6 — np.bincount()

Frequency counting-এর fast method।

```python
a = np.array([
    0,
    1,
    1,
    2,
    2,
    2
])


print(np.bincount(a))
```

Output:

```
[1 2 3]
```

Meaning:

```
0 → 1 times

1 → 2 times

2 → 3 times
```

---

Machine Learning:

Class distribution বের করতে ব্যবহার হয়।

---

# Part 7 — np.searchsorted()

Sorted array-তে কোথায় insert হবে তা বের করে।

Example:

```python
a = np.array([
    10,
    20,
    30,
    40
])
```

---

```python
print(
    np.searchsorted(a,25)
)
```

Output:

```
2
```

Meaning:

```
10 20 |25| 30 40

index 2
```

---

Multiple:

```python
print(
np.searchsorted(
    a,
    [5,25,50]
))
```

Output:

```
[0 2 4]
```

---

# Part 8 — Statistics Functions

Dataset:

```python
data = np.array([
    10,
    20,
    30,
    40,
    50
])
```

---

# Mean

Average

```python
print(np.mean(data))
```

Output:

```
30
```

---

# Median

Middle value

```python
print(np.median(data))
```

Output:

```
30
```

---

# Variance

Spread কত

```python
print(np.var(data))
```

---

# Standard Deviation

```python
print(np.std(data))
```

---

Formula:

```
std = √variance
```

---

# Part 9 — Percentile

Percentile বলে data-এর position।

Example:

```python
data = np.array([
10,20,30,40,50
])
```

---

50 percentile:

```python
print(
np.percentile(data,50)
)
```

Output:

```
30
```

এটাই median।

---

90 percentile:

```python
print(
np.percentile(data,90)
)
```

---

Real Example:

Website response time:

```
90% request এর response time
```

এটি বের করতে percentile ব্যবহার হয়।

---

# Part 10 — Quantile

Percentile-এর decimal version।

```python
np.quantile(
data,
0.5
)
```

Output:

```
30
```

Relationship:

```
percentile 50

=

quantile 0.5
```

---

# Part 11 — Correlation

Machine Learning-এ Feature relationship বের করতে।

Example:

```python
x = np.array([
1,2,3,4,5
])

y = np.array([
2,4,6,8,10
])
```

```python
print(
np.corrcoef(x,y)
)
```

Output:

```
[[1. 1.]
 [1. 1.]]
```

Meaning:

Perfect positive correlation।

---

# Part 12 — Covariance

```python
print(
np.cov(x,y)
)
```

Covariance বলে দুই variable একসাথে কিভাবে change করে।

---

# Real Data Engineering Example

Sales Data:

```python
sales = np.array([
500,
700,
400,
900,
800
])
```

Tasks:

Average:

```python
np.mean(sales)
```

Median:

```python
np.median(sales)
```

Highest:

```python
np.max(sales)
```

Lowest:

```python
np.min(sales)
```

---

# Machine Learning Example

Prediction Scores:

```python
prediction = np.array([
0.2,
0.95,
0.7,
0.4
])
```

Top prediction:

```python
top = np.argsort(prediction)[::-1]

print(top)
```

Output:

```
[1 2 3 0]
```

---

# Common Mistakes

## ❌ argsort value দেয় মনে করা

Wrong:

```python
np.argsort([5,1,3])
```

Output:

```
[1,2,0]
```

এগুলো index।

---

## ❌ percentile ভুল বোঝা

90 percentile মানে:

"90% data এর নিচে এই value আছে"

---

## ❌ correlation মানে causation না

Correlation ≠ Cause

---

# Practice

## Easy

```python
a=np.array([
50,20,80,10
])
```

Find:

1. Sort
2. Descending sort
3. argsort

---

## Medium

```python
marks=np.array([
80,90,70,90,60,80
])
```

Find:

1. Unique marks
2. Frequency
3. Mean
4. Median
5. Standard deviation

---

## Hard

E-commerce:

```python
price=np.array([
1000,
2000,
1500,
3000,
2500
])
```

Tasks:

1. Ascending price sort
2. Top 3 expensive product index
3. Median price
4. 90 percentile price
5. Normalize price

---

# Interview Questions

### 1. Difference between sort and argsort?

| sort              | argsort          |
| ----------------- | ---------------- |
| Values return করে | Index return করে |

---

### 2. Why use argsort in ML?

Ranking, top-k prediction, recommendation system।

---

### 3. Difference between percentile and quantile?

```
percentile → 0-100

quantile → 0-1
```

---

### 4. Difference mean and median?

Mean outlier sensitive।

Median outlier resistant।

---

### 5. Why correlation?

Feature relationship বুঝতে।

---

# Cheat Sheet

| Function            | কাজ               |
| ------------------- | ----------------- |
| `np.sort()`         | Sorting           |
| `np.argsort()`      | Sorted index      |
| `np.lexsort()`      | Multi-column sort |
| `np.unique()`       | Unique values     |
| `np.bincount()`     | Frequency         |
| `np.searchsorted()` | Insert position   |
| `np.mean()`         | Average           |
| `np.median()`       | Middle            |
| `np.std()`          | Spread            |
| `np.var()`          | Variance          |
| `np.percentile()`   | Percentile        |
| `np.quantile()`     | Quantile          |
| `np.corrcoef()`     | Correlation       |
| `np.cov()`          | Covariance        |

---

# Production Mini Project

একটি e-commerce order dataset:

```python
orders = np.array([
    [101,500],
    [102,200],
    [103,900],
    [104,300],
    [105,700]
])
```

Columns:

```
Order_ID
Amount
```

Tasks:

1. Amount অনুযায়ী ascending sort করো।
2. Top 3 highest order বের করো।
3. Top 3 order ID বের করো (`argsort`)।
4. Average order value বের করো।
5. Median order value বের করো।
6. 90 percentile order value বের করো।

---

# Lesson 16 Summary

আজ শিখলাম:

✅ Sorting
✅ Ranking
✅ Searching
✅ Frequency Analysis
✅ Mean/Median/Variance
✅ Percentile
✅ Correlation
✅ Covariance

---

## Next Lesson 17 — NumPy Random Module & Data Generation

শিখব:

* `np.random`
* Random seed
* Random distribution
* Normal distribution
* Uniform distribution
* Random sampling
* Train/Test dataset generation
* ML dataset simulation

এটি Machine Learning practice এবং experiment-এর জন্য খুব গুরুত্বপূর্ণ।

# Module 5 — Lesson 17: NumPy Random Module & Data Generation (Mastery Guide)

Machine Learning এবং Data Engineering-এ random data generation খুব গুরুত্বপূর্ণ।

তুমি যখন:

* Model test করো
* Dummy dataset বানাও
* Weight initialization করো
* Sampling করো
* Train/Test split practice করো

তখন NumPy Random Module ব্যবহার করবে।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* `np.random`
* Random seed
* Random number generation
* `rand()`
* `randn()`
* `randint()`
* `random()`
* `choice()`
* `shuffle()`
* `permutation()`
* Normal distribution
* Uniform distribution
* Data simulation

---

# Part 1 — np.random কী?

NumPy-এর random module হলো random number generate করার system।

Import:

```python
import numpy as np
```

---

# Part 2 — Random Float Generation

## np.random.random()

0 থেকে 1 এর মধ্যে random number দেয়।

```python
x = np.random.random()

print(x)
```

Example output:

```text
0.62341
```

প্রতিবার নতুন value আসবে।

---

## Multiple Values

```python
x = np.random.random(5)

print(x)
```

Output:

```text
[
0.23
0.55
0.12
0.89
0.44
]
```

Shape:

```python
x.shape
```

Output:

```
(5,)
```

---

# Part 3 — Random Seed

এটি খুব গুরুত্বপূর্ণ।

Problem:

```python
np.random.random(3)
```

প্রতিবার আলাদা result।

Machine Learning experiment reproduce করতে চাইলে seed দরকার।

---

## Without Seed

```python
print(np.random.random(3))
```

Output:

```
[0.23 0.56 0.89]
```

আবার:

```
[0.11 0.43 0.72]
```

Different।

---

## With Seed

```python
np.random.seed(42)

print(np.random.random(3))
```

Output:

```
[0.3745 0.9507 0.7319]
```

আবার run করলে একই result।

---

# কেন Seed ব্যবহার করি?

Machine Learning:

```
Same Code

+

Same Data

+

Same Randomness

=

Same Result
```

Reproducibility।

---

# Part 4 — randint()

Integer random number।

Syntax:

```python
np.random.randint(
    low,
    high,
    size
)
```

---

Example:

```python
x = np.random.randint(
    1,
    10,
    5
)

print(x)
```

Output:

```
[3 8 1 5 9]
```

Meaning:

```
1 <= value < 10
```

---

## Matrix

```python
x = np.random.randint(
    0,
    100,
    (3,4)
)

print(x)
```

Output:

```
[
[23 45 67 12]
[89 34 56 78]
[10 22 90 11]
]
```

Shape:

```
(3,4)
```

---

# Part 5 — rand()

0 থেকে 1 random float।

```python
x = np.random.rand(3)

print(x)
```

Output:

```
[0.2 0.8 0.5]
```

---

Matrix:

```python
x = np.random.rand(2,3)
```

Shape:

```
(2,3)
```

---

# rand vs random

| rand                         | random          |
| ---------------------------- | --------------- |
| Old API                      | Modern API      |
| Multiple dimensions directly | size parameter  |
| `rand(2,3)`                  | `random((2,3))` |

---

# Part 6 — randn()

Normal Distribution।

Mean:

```
0
```

Standard deviation:

```
1
```

Example:

```python
x = np.random.randn(5)

print(x)
```

Output:

```
[
-0.5
0.8
-1.2
0.3
0.9
]
```

---

ML-এ:

* Neural Network initialization
* Noise generation

ব্যবহার হয়।

---

# Part 7 — Normal Distribution

More control:

```python
x = np.random.normal(
    loc=50,
    scale=10,
    size=5
)

print(x)
```

Meaning:

```
Mean = 50

Std = 10

5 values
```

---

Example:

Student Marks:

```python
marks = np.random.normal(
    70,
    10,
    100
)
```

মানে:

100 জন student's marks।

---

# Part 8 — Uniform Distribution

সব value-এর probability সমান।

```python
x = np.random.uniform(
    10,
    20,
    5
)

print(x)
```

Output:

```
[12.4 18.2 15.7 11.8 19.3]
```

---

Difference:

| Normal        | Uniform           |
| ------------- | ----------------- |
| Bell curve    | Equal probability |
| Mean centered | Flat distribution |

---

# Part 9 — choice()

Random selection।

Example:

```python
names = np.array([
    "Ali",
    "Rahim",
    "Karim"
])


print(
np.random.choice(names)
)
```

Output:

```
Rahim
```

---

Multiple:

```python
print(
np.random.choice(
    names,
    5
)
)
```

Output:

```
[
Ali
Karim
Ali
Rahim
Karim
]
```

---

## Probability Control

```python
np.random.choice(
    [0,1],
    size=10,
    p=[0.7,0.3]
)
```

Meaning:

```
0 probability = 70%

1 probability = 30%
```

Machine Learning class imbalance simulation-এ ব্যবহার হয়।

---

# Part 10 — shuffle()

Original array পরিবর্তন করে।

```python
a = np.array([
1,2,3,4,5
])


np.random.shuffle(a)

print(a)
```

Output:

```
[3 1 5 2 4]
```

---

# Part 11 — permutation()

Copy return করে।

```python
a = np.array([
1,2,3,4,5
])


b = np.random.permutation(a)

print(b)

print(a)
```

Output:

```
[4 1 3 5 2]

Original:

[1 2 3 4 5]
```

---

Difference:

| shuffle         | permutation |
| --------------- | ----------- |
| Original change | New array   |
| None return     | Copy return |

---

# Part 12 — Random Sampling

Dataset:

```python
data = np.arange(100)
```

Random 10 sample:

```python
sample = np.random.choice(
    data,
    10,
    replace=False
)

print(sample)
```

---

`replace=False`

মানে:

একই value দুইবার আসবে না।

---

`replace=True`

মানে:

duplicate allowed।

---

# Part 13 — Train/Test Dataset Simulation

ধরো:

1000 samples

```python
X = np.random.rand(
    1000,
    5
)
```

Shape:

```
(1000,5)
```

Target:

```python
y = np.random.randint(
    0,
    2,
    1000
)
```

Binary classification:

```
0 = Normal

1 = Fraud
```

---

# Part 14 — Generate Fake E-commerce Data

Customer Age:

```python
age = np.random.randint(
    18,
    60,
    1000
)
```

Income:

```python
income = np.random.normal(
    50000,
    10000,
    1000
)
```

Purchase:

```python
purchase = np.random.randint(
    100,
    5000,
    1000
)
```

Dataset:

```python
dataset = np.column_stack(
    (
        age,
        income,
        purchase
    )
)
```

Shape:

```
(1000,3)
```

---

# Part 15 — Modern Random Generator (Recommended)

নতুন NumPy-তে:

```python
rng = np.random.default_rng(42)

x = rng.random(5)

print(x)
```

এটি recommended।

---

Random Integer:

```python
rng.integers(
    1,
    10,
    5
)
```

---

Normal:

```python
rng.normal(
    50,
    10,
    100
)
```

---

# Common Mistakes

## ভুল:

```python
np.random.randint(10)
```

এটি হবে:

```
0 থেকে 9
```

---

## ভুল:

```python
np.random.randint(
10,
20
)
```

একটি value return করবে।

Multiple চাইলে:

```python
size=10
```

---

## ভুল:

Random এবং reproducibility mix করা।

Experiment-এর শুরুতে:

```python
np.random.seed(42)
```

---

# Practice

## Easy

Generate:

1. 10 random float number
2. 20 random integer (1-100)
3. 5×5 random matrix

---

## Medium

Create:

Student dataset:

Columns:

```
ID
Age
Marks
```

Requirements:

* ID: 1-100
* Age: 18-25
* Marks: Normal distribution(mean=70,std=10)

---

## Hard

E-commerce simulation:

Generate 10,000 customers:

Columns:

```
Age
Income
Purchase
Category
```

Rules:

Age:

```
18-60
```

Income:

```
mean=50000
std=15000
```

Category:

```
Electronics
Fashion
Food
```

Tasks:

1. Dataset তৈরি করো
2. Mean income বের করো
3. Top 100 purchase বের করো
4. Category frequency বের করো
5. Train/Test split manually করো

---

# Interview Questions

### 1. Why use random seed?

Reproducible results পাওয়ার জন্য।

---

### 2. Difference between shuffle and permutation?

| shuffle         | permutation |
| --------------- | ----------- |
| Original modify | Copy return |

---

### 3. Normal vs Uniform distribution?

Normal:

```
Mean centered
```

Uniform:

```
Equal probability
```

---

### 4. rand vs randint?

`rand`

→ float

`randint`

→ integer

---

### 5. Why random data generation important?

* Testing
* Simulation
* ML experiments
* Algorithm validation

---

# Cheat Sheet

| Function        | কাজ                  |
| --------------- | -------------------- |
| `random()`      | Random float         |
| `rand()`        | Random float         |
| `randint()`     | Random integer       |
| `randn()`       | Normal distribution  |
| `normal()`      | Controlled normal    |
| `uniform()`     | Uniform distribution |
| `choice()`      | Random selection     |
| `shuffle()`     | Shuffle inplace      |
| `permutation()` | Shuffle copy         |
| `seed()`        | Reproducibility      |
| `default_rng()` | Modern generator     |

---

# Lesson 17 Summary

আজ আমরা শিখলাম:

✅ Random number generation
✅ Seed & reproducibility
✅ Random integer
✅ Normal distribution
✅ Uniform distribution
✅ Sampling
✅ Shuffle
✅ Permutation
✅ Fake dataset generation
✅ ML dataset simulation

---

## Next Lesson 18 — NumPy Linear Algebra (Deep Dive)

পরের Lesson-এ শিখব:

* Matrix multiplication
* Dot product
* Inner product
* Outer product
* Transpose
* Inverse
* Determinant
* Eigenvalues
* Solving linear equations

এটি Machine Learning-এর Mathematics foundation-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।
# Module 6 — Lesson 18: NumPy Linear Algebra (Mastery Guide)

Machine Learning, Deep Learning, Computer Vision, Recommendation System — সব জায়গায় **Linear Algebra** ব্যবহার হয়।

Neural Network-এর ভিতরের operation আসলে:

```
Input × Weight + Bias
```

এটাই Matrix Multiplication।

আজ আমরা NumPy দিয়ে Linear Algebra শিখব।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* Vector কী
* Matrix কী
* Transpose
* Dot Product
* Matrix Multiplication
* Inner Product
* Outer Product
* Determinant
* Matrix Inverse
* Solving Linear Equations
* Eigenvalues & Eigenvectors

---

# Part 1 — Vector এবং Matrix

## Vector

একটি 1D array:

```python
import numpy as np

v = np.array([
    1,
    2,
    3
])

print(v)
```

Output:

```
[1 2 3]
```

Shape:

```python
print(v.shape)
```

Output:

```
(3,)
```

---

## Matrix

2D array:

```python
matrix = np.array([
    [1,2],
    [3,4]
])

print(matrix)
```

Shape:

```
(2,2)
```

---

# Part 2 — Transpose

Transpose মানে:

Row → Column

Column → Row

Example:

```python
A = np.array([
    [1,2,3],
    [4,5,6]
])

print(A.T)
```

Output:

```
[
[1 4]
[2 5]
[3 6]
]
```

Shape:

Before:

```
(2,3)
```

After:

```
(3,2)
```

---

## Machine Learning Example

Dataset:

```
Samples × Features
```

Example:

```
1000 × 20
```

কখনো দরকার:

```
20 × 1000
```

তখন transpose ব্যবহার হয়।

---

# Part 3 — Dot Product

দুটি vector-এর multiplication।

Example:

```python
a = np.array([
    1,
    2,
    3
])


b = np.array([
    4,
    5,
    6
])


result = np.dot(a,b)

print(result)
```

Calculation:

```
1×4 + 2×5 + 3×6

=4+10+18

=32
```

Output:

```
32
```

---

# Part 4 — Matrix Multiplication

সবচেয়ে গুরুত্বপূর্ণ।

Syntax:

```python
np.matmul(A,B)
```

বা

```python
A @ B
```

---

Example:

```python
A = np.array([
    [1,2],
    [3,4]
])


B = np.array([
    [5,6],
    [7,8]
])


print(A @ B)
```

Calculation:

```
[1 2] [5 6]
[3 4] [7 8]


Result:

1×5 + 2×7 =19

1×6 + 2×8 =22


3×5 + 4×7 =43

3×6 + 4×8 =50
```

Output:

```
[
[19 22]
[43 50]
]
```

---

# Matrix Multiplication Rule

যদি:

```
A = (m,n)

B = (n,p)
```

তাহলে result:

```
(m,p)
```

---

Example:

```
(3,4)

×

(4,2)

=

(3,2)
```

---

# Common Error

Wrong:

```python
A.shape

(3,4)


B.shape

(5,2)
```

Cannot multiply।

কারণ:

```
4 ≠ 5
```

---

# Part 5 — Inner Product

```python
a = np.array([1,2,3])

b = np.array([4,5,6])


print(
np.inner(a,b)
)
```

Output:

```
32
```

Vector-এর ক্ষেত্রে dot-এর মতো।

---

# Part 6 — Outer Product

Outer product নতুন matrix তৈরি করে।

```python
a = np.array([
1,2,3
])

b = np.array([
4,5
])


print(
np.outer(a,b)
)
```

Output:

```
[
[4 5]
[8 10]
[12 15]
]
```

Shape:

```
(3,2)
```

---

# Part 7 — Matrix Multiplication vs Element-wise

অনেক beginner এখানে ভুল করে।

---

## Element-wise

```python
A * B
```

Example:

```python
A=np.array([
[1,2],
[3,4]
])


B=np.array([
[5,6],
[7,8]
])


print(A*B)
```

Output:

```
[
[5 12]
[21 32]
]
```

---

## Matrix Multiplication

```python
A @ B
```

Output:

```
[
[19 22]
[43 50]
]
```

---

Difference:

| Operation             | Symbol |
| --------------------- | ------ |
| Element-wise          | `*`    |
| Matrix multiplication | `@`    |

---

# Part 8 — Determinant

একটি square matrix-এর বিশেষ value।

Function:

```python
np.linalg.det()
```

Example:

```python
A=np.array([
[1,2],
[3,4]
])


print(
np.linalg.det(A)
)
```

Calculation:

```
(1×4)-(2×3)

=4-6

=-2
```

Output:

```
-2
```

---

# Part 9 — Matrix Inverse

Inverse:

```
A × A⁻¹ = Identity Matrix
```

Function:

```python
np.linalg.inv()
```

Example:

```python
A=np.array([
[1,2],
[3,4]
])


print(
np.linalg.inv(A)
)
```

Output:

```
[
[-2 ,1]
[1.5,-0.5]
]
```

---

Important:

শুধু square matrix-এর inverse থাকে।

এবং determinant 0 হলে inverse নেই।

---

# Part 10 — Identity Matrix

```python
I = np.eye(3)

print(I)
```

Output:

```
[
[1 0 0]
[0 1 0]
[0 0 1]
]
```

---

# Part 11 — Solve Linear Equation

Problem:

```
2x + 3y = 8

5x + 4y = 13
```

Matrix form:

```
AX = B
```

---

A:

```python
A=np.array([
[2,3],
[5,4]
])
```

B:

```python
B=np.array([
8,
13
])
```

Solve:

```python
solution=np.linalg.solve(A,B)

print(solution)
```

Output:

```
[1 2]
```

Meaning:

```
x=1

y=2
```

---

# Part 12 — Eigenvalues and Eigenvectors

Machine Learning এবং PCA-তে ব্যবহার হয়।

Function:

```python
np.linalg.eig()
```

Example:

```python
A=np.array([
[2,0],
[0,3]
])


values,vectors=np.linalg.eig(A)


print(values)

print(vectors)
```

Output:

```
[2 3]
```

---

Use:

* PCA
* Dimensionality Reduction
* Feature Extraction

---

# Part 13 — Norm

Vector magnitude।

```python
v=np.array([
3,
4
])


print(
np.linalg.norm(v)
)
```

Calculation:

```
√(3²+4²)

=5
```

Output:

```
5
```

---

# Part 14 — Real ML Example

Neural Network:

Input:

```
X

(2,3)
```

Weights:

```
W

(3,4)
```

Calculation:

```python
output = X @ W
```

Shape:

```
(2,3)

×

(3,4)

=

(2,4)
```

এটাই Neural Network-এর core operation।

---

# Part 15 — Linear Regression Example

Formula:

```
Prediction = XW
```

Example:

```python
X=np.array([
[1,2],
[3,4],
[5,6]
])


W=np.array([
10,
20
])


prediction = X @ W


print(prediction)
```

Output:

```
[50 110 170]
```

---

# Common Mistakes

## Mistake 1

Matrix multiplication:

Wrong:

```python
A*B
```

Correct:

```python
A@B
```

---

## Mistake 2

Shape না দেখা।

সবসময়:

```python
print(A.shape)
print(B.shape)
```

---

## Mistake 3

Inverse নেওয়া:

```python
np.linalg.inv(A)
```

যেখানে determinant:

```
0
```

---

# Practice

## Easy

```python
A=np.array([
[1,2],
[3,4]
])
```

Find:

1. Transpose
2. Determinant
3. Inverse

---

## Medium

```python
A=np.array([
[1,2,3],
[4,5,6]
])

B=np.array([
[7,8],
[9,10],
[11,12]
])
```

Tasks:

1. Shape বের করো
2. Matrix multiplication করো
3. Result shape বের করো

---

## Hard

Neural Network:

```python
X=np.array([
[1,2,3],
[4,5,6]
])


W=np.array([
[0.5,0.2],
[0.3,0.4],
[0.1,0.7]
])
```

Tasks:

1. Compute `X @ W`
2. Add bias:

```python
bias=[1,2]
```

3. Apply ReLU:

```
max(0,x)
```

---

# Interview Questions

### 1. Difference between * and @?

`*`

→ Element-wise multiplication

`@`

→ Matrix multiplication

---

### 2. Matrix multiplication rule?

First matrix-এর column সংখ্যা = second matrix-এর row সংখ্যা।

---

### 3. Why transpose?

Shape change এবং matrix operation-এর জন্য।

---

### 4. Where eigenvalues used?

* PCA
* Feature reduction
* Computer vision

---

### 5. Why solve() instead of inverse?

`solve()` faster এবং numerically stable।

---

# Cheat Sheet

| Function            | কাজ                   |
| ------------------- | --------------------- |
| `.T`                | Transpose             |
| `np.dot()`          | Dot product           |
| `@`                 | Matrix multiplication |
| `np.matmul()`       | Matrix multiplication |
| `np.inner()`        | Inner product         |
| `np.outer()`        | Outer product         |
| `np.linalg.det()`   | Determinant           |
| `np.linalg.inv()`   | Inverse               |
| `np.linalg.solve()` | Equation solve        |
| `np.linalg.eig()`   | Eigen                 |
| `np.linalg.norm()`  | Magnitude             |

---

# Lesson 18 Summary

আজ তুমি শিখলে:

✅ Vector
✅ Matrix
✅ Transpose
✅ Dot Product
✅ Matrix Multiplication
✅ Inner/Outer Product
✅ Determinant
✅ Inverse
✅ Linear Equation Solve
✅ Eigenvalues
✅ ML Matrix Operations

---

## Next Lesson 19 — NumPy Advanced Indexing & Boolean Masking

পরের Lesson-এ শিখব:

* Boolean indexing
* Conditional filtering
* Fancy indexing
* Mask creation
* Data cleaning with NumPy
* Outlier detection
* Real ML dataset filtering

এটি Data Analysis এবং Data Engineering-এর জন্য খুব গুরুত্বপূর্ণ।
# Module 7 — Lesson 19: NumPy Advanced Indexing & Boolean Masking (Mastery Guide)

Data Engineering এবং Machine Learning-এ সবচেয়ে বেশি যে কাজগুলো করতে হয়:

* নির্দিষ্ট data filter করা
* condition অনুযায়ী row বের করা
* outlier remove করা
* missing/invalid data খুঁজে বের করা
* dataset clean করা

এসব কাজের জন্য NumPy-এর **Advanced Indexing** এবং **Boolean Masking** অত্যন্ত গুরুত্বপূর্ণ।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* Basic indexing recap
* Boolean indexing
* Conditional filtering
* Multiple conditions
* Fancy indexing
* Index arrays
* Mask তৈরি করা
* Data cleaning
* Outlier detection
* ML dataset filtering

---

# Part 1 — Basic Indexing Recap

Array:

```python
import numpy as np

data = np.array([
    10,
    20,
    30,
    40,
    50
])
```

---

## Single element

```python
print(data[0])
```

Output:

```
10
```

---

## Negative index

```python
print(data[-1])
```

Output:

```
50
```

---

## Slice

```python
print(data[1:4])
```

Output:

```
[20 30 40]
```

---

# Part 2 — Boolean Indexing

Boolean indexing মানে condition দিয়ে data select করা।

Example:

```python
data = np.array([
    10,
    20,
    30,
    40,
    50
])
```

Condition:

```python
mask = data > 30

print(mask)
```

Output:

```
[False False False True True]
```

---

এখন mask apply:

```python
print(data[mask])
```

Output:

```
[40 50]
```

---

Concept:

```
data

10 20 30 40 50


mask

F  F  F  T  T


Result

40 50
```

---

# Part 3 — Direct Boolean Filtering

Mask variable দরকার নেই।

```python
print(
    data[data > 30]
)
```

Output:

```
[40 50]
```

এটাই সবচেয়ে বেশি ব্যবহার হবে।

---

# Part 4 — Multiple Conditions

ধরো:

যে value:

* 20 এর বেশি
* 50 এর কম

```python
data = np.array([
10,
20,
30,
40,
50,
60
])


result = data[
    (data > 20) &
    (data < 50)
]


print(result)
```

Output:

```
[30 40]
```

---

# Important Operators

NumPy-তে:

| Python | NumPy |   |
| ------ | ----- | - |
| and    | `&`   |   |
| or     | `     | ` |
| not    | `~`   |   |

---

## ভুল ❌

```python
data > 20 and data < 50
```

Error হবে।

কারণ NumPy array-এর জন্য ব্যবহার করতে হবে:

```python
(data > 20) & (data < 50)
```

---

# Part 5 — OR Condition

Example:

30 অথবা 50 বের করো।

```python
data[
    (data == 30) |
    (data == 50)
]
```

Output:

```
[30 50]
```

---

# Part 6 — NOT Condition

সব value except 30:

```python
data[
    ~(data == 30)
]
```

Output:

```
[10 20 40 50 60]
```

---

# Part 7 — Fancy Indexing

Fancy indexing হলো index list ব্যবহার করে data select করা।

Example:

```python
a = np.array([
10,
20,
30,
40,
50
])
```

Indexes:

```python
idx = [0,2,4]
```

Select:

```python
print(a[idx])
```

Output:

```
[10 30 50]
```

---

# Difference

Normal:

```python
a[2]
```

একটি value।

Fancy:

```python
a[[0,2,4]]
```

Multiple value।

---

# Part 8 — 2D Fancy Indexing

Matrix:

```python
matrix = np.array([
[10,20,30],
[40,50,60],
[70,80,90]
])
```

---

Row select:

```python
print(
matrix[[0,2]]
)
```

Output:

```
[
[10 20 30]
[70 80 90]
]
```

---

# Part 9 — Selecting Specific Elements

Example:

Row index:

```
[0,1,2]
```

Column index:

```
[2,1,0]
```

```python
print(
matrix[
    [0,1,2],
    [2,1,0]
]
)
```

Output:

```
[30 50 70]
```

Meaning:

```
matrix[0,2]

matrix[1,1]

matrix[2,0]
```

---

# Part 10 — Boolean Mask in 2D

Matrix:

```python
sales = np.array([
[100,200,300],
[400,500,600],
[700,800,900]
])
```

Find values > 500:

```python
print(
sales[sales > 500]
)
```

Output:

```
[600 700 800 900]
```

---

# Part 11 — Filtering Rows

এটি খুব important।

Dataset:

```python
employees = np.array([
[101,25,50000],
[102,30,70000],
[103,22,30000],
[104,40,90000]
])
```

Columns:

```
ID
Age
Salary
```

---

Age > 25:

```python
result = employees[
    employees[:,1] > 25
]


print(result)
```

Output:

```
[
[102 30 70000]
[104 40 90000]
]
```

---

# Part 12 — Multiple Column Filtering

Age > 25 এবং Salary > 60000

```python
result = employees[
    (employees[:,1] > 25) &
    (employees[:,2] > 60000)
]


print(result)
```

Output:

```
[
[102 30 70000]
[104 40 90000]
]
```

---

# Part 13 — np.where()

Condition অনুযায়ী index বের করে।

Example:

```python
a=np.array([
10,
20,
30,
40,
50
])


print(
np.where(a>30)
)
```

Output:

```
(array([3,4]),)
```

---

Value replace:

```python
a = np.where(
    a>30,
    1,
    0
)

print(a)
```

Output:

```
[0 0 0 1 1]
```

---

# Part 14 — Data Cleaning Example

Dataset:

```python
salary=np.array([
30000,
50000,
-1000,
70000,
90000
])
```

Negative salary remove:

```python
clean = salary[
    salary > 0
]

print(clean)
```

Output:

```
[30000 50000 70000 90000]
```

---

# Part 15 — Outlier Detection

Dataset:

```python
price=np.array([
100,
200,
300,
400,
10000
])
```

Maximum limit:

```python
normal = price[
    price < 1000
]


print(normal)
```

Output:

```
[100 200 300 400]
```

---

# Part 16 — Missing Value Filtering

Example:

```python
data=np.array([
10,
20,
np.nan,
40
])
```

Check:

```python
mask=np.isnan(data)

print(mask)
```

Output:

```
[False False True False]
```

Remove:

```python
clean=data[
    ~np.isnan(data)
]

print(clean)
```

Output:

```
[10 20 40]
```

---

# Part 17 — ML Dataset Example

Feature:

```python
X=np.array([
[20,50000],
[30,70000],
[40,90000],
[18,20000]
])
```

Target:

```python
y=np.array([
0,
1,
1,
0
])
```

High income customers:

```python
high_income = X[
    X[:,1] > 60000
]


print(high_income)
```

Output:

```
[
[30 70000]
[40 90000]
]
```

---

# Part 18 — Combining Fancy + Boolean

Example:

Top salary employees:

```python
idx=np.argsort(
    employees[:,2]
)[::-1]


top=employees[idx[:2]]

print(top)
```

Output:

```
[
[104 40 90000]
[102 30 70000]
]
```

---

# Common Mistakes

## Mistake 1

Wrong:

```python
data[data > 20 and data <50]
```

Correct:

```python
data[
(data>20)&
(data<50)
]
```

---

## Mistake 2

Condition parentheses না দেওয়া:

Wrong:

```python
data > 20 & data <50
```

Correct:

```python
(data>20)&(data<50)
```

---

## Mistake 3

Boolean mask size mismatch

Wrong:

```python
a=np.array([1,2,3])

mask=np.array([True,False])

a[mask]
```

Error।

কারণ:

```
3 elements

2 mask
```

---

# Practice

## Easy

```python
a=np.array([
5,10,15,20,25,30
])
```

Tasks:

1. Values > 15 বের করো
2. Values between 10 and 25 বের করো
3. Even numbers বের করো

---

## Medium

```python
students=np.array([
[1,80],
[2,50],
[3,90],
[4,40],
[5,70]
])
```

Columns:

```
ID
Marks
```

Tasks:

1. Pass students (marks >=50)
2. Top 3 students
3. Failed students

---

## Hard

E-commerce:

```python
products=np.array([
[1,500,10],
[2,1000,5],
[3,2000,2],
[4,300,20],
[5,5000,1]
])
```

Columns:

```
ID
Price
Stock
```

Tasks:

1. Price > 1000 filter
2. Stock > 5 filter
3. Low stock products
4. Top expensive products
5. Remove invalid price

---

# Interview Questions

### 1. What is Boolean Masking?

Condition ব্যবহার করে array-এর নির্দিষ্ট element select করার technique।

---

### 2. Difference between Fancy Indexing and Boolean Indexing?

| Fancy             | Boolean               |
| ----------------- | --------------------- |
| Index দিয়ে select | Condition দিয়ে select |

---

### 3. Why use np.where()?

Condition অনুযায়ী index বের করা বা value replace করার জন্য।

---

### 4. Why use & instead of and?

NumPy array element-wise operation করে।

---

### 5. Where used in ML?

* Data filtering
* Outlier removal
* Feature selection
* Dataset cleaning

---

# Cheat Sheet

| Function           | কাজ                   |    |
| ------------------ | --------------------- | -- |
| `array[condition]` | Filtering             |    |
| `array[index]`     | Fancy indexing        |    |
| `np.where()`       | Condition index/value |    |
| `np.isnan()`       | Missing check         |    |
| `&`                | AND                   |    |
| `                  | `                     | OR |
| `~`                | NOT                   |    |

---

# Lesson 19 Summary

আজ তুমি শিখলে:

✅ Advanced Indexing
✅ Boolean Masking
✅ Conditional Filtering
✅ Fancy Indexing
✅ Row Filtering
✅ Data Cleaning
✅ Outlier Detection
✅ ML Dataset Selection

---

## Next Lesson 20 — NumPy Memory Management & Performance Optimization

পরের Lesson-এ শিখব:

* Copy vs View
* Memory sharing
* `np.copy()`
* Strides
* Contiguous arrays
* Vectorization
* Performance optimization
* Large dataset handling

এগুলো Data Engineer হিসেবে তোমাকে অনেক শক্তিশালী করবে।
# Module 8 — Lesson 20: NumPy Memory Management & Performance Optimization (Mastery Guide)

আজকের Lesson অনেক গুরুত্বপূর্ণ, কারণ Data Engineering এবং Machine Learning-এ শুধু code লিখলেই হবে না — **memory efficient এবং fast code লিখতে হবে।**

যখন তুমি:

* Millions of rows process করবে
* Large image dataset handle করবে
* Deep Learning preprocessing করবে
* Big CSV/Parquet data নিয়ে কাজ করবে

তখন NumPy memory management জানা খুব দরকার।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* NumPy memory model
* Copy vs View
* `np.copy()`
* Array memory sharing
* `base`
* `strides`
* Contiguous arrays
* Vectorization
* Loop vs NumPy performance
* Memory optimization techniques

---

# Part 1 — NumPy Memory Model

NumPy array দুইটি জিনিস দিয়ে তৈরি:

```
Array Object
+
Data Buffer
```

Example:

```python
import numpy as np

a = np.array([10,20,30,40])
```

Memory:

```
a
|
|
[10][20][30][40]
```

Array object শুধু data কোথায় আছে সেটা জানে।

---

# Part 2 — Copy vs View

এটি NumPy-এর সবচেয়ে important concept।

---

# View কী?

View হলো original data-এর একটি reference।

নতুন data তৈরি করে না।

Example:

```python
a = np.array([
    10,
    20,
    30
])


b = a.view()


b[0] = 100


print(a)
```

Output:

```
[100 20 30]
```

কেন?

কারণ:

```
a
 |
 |
[10][20][30]


b
 |
 |
same memory
```

দুইজন একই data ব্যবহার করছে।

---

# Check Memory Sharing

```python
print(b.base)
```

Output:

```
[100 20 30]
```

মানে:

b অন্য array থেকে এসেছে।

---

# Part 3 — Copy কী?

Copy সম্পূর্ণ নতুন memory তৈরি করে।

Example:

```python
a = np.array([
10,
20,
30
])


b = a.copy()


b[0]=100


print(a)
print(b)
```

Output:

```
a:

[10 20 30]


b:

[100 20 30]
```

কারণ:

```
a

[10][20][30]


b

[100][20][30]
```

আলাদা memory।

---

# View vs Copy

| View                    | Copy        |
| ----------------------- | ----------- |
| Same memory             | New memory  |
| Fast                    | Slower      |
| Less memory             | More memory |
| Change affects original | Independent |

---

# Part 4 — Slicing Creates View

এটি অনেক গুরুত্বপূর্ণ।

Example:

```python
a=np.array([
10,20,30,40,50
])


b=a[1:4]


b[0]=999


print(a)
```

Output:

```
[10 999 30 40 50]
```

কারণ slice সাধারণত view।

---

Safe way:

```python
b=a[1:4].copy()
```

---

# Part 5 — Fancy Indexing Creates Copy

Example:

```python
a=np.array([
10,20,30,40
])


b=a[[0,2]]
```

এটি copy তৈরি করে।

Check:

```python
print(b.base)
```

Output:

```
None
```

---

# Rule:

### Slice

```python
a[1:5]
```

↓

View

### Fancy Index

```python
a[[1,3]]
```

↓

Copy

---

# Part 6 — np.shares_memory()

দুই array একই memory share করছে কিনা।

Example:

```python
a=np.array([1,2,3])

b=a.view()

print(
np.shares_memory(a,b)
)
```

Output:

```
True
```

---

Copy:

```python
c=a.copy()

print(
np.shares_memory(a,c)
)
```

Output:

```
False
```

---

# Part 7 — Array Strides

Stride বলে memory-তে পরবর্তী element কত byte পরে আছে।

Example:

```python
a=np.array([
1,2,3,4
])


print(a.strides)
```

Output:

```
(8,)
```

কারণ:

Integer সাধারণত 8 byte নেয়।

---

2D:

```python
a=np.array([
[1,2,3],
[4,5,6]
])


print(a.strides)
```

Output:

```
(24,8)
```

Meaning:

```
Next row = 24 byte

Next column = 8 byte
```

---

# Part 8 — Contiguous Memory

CPU দ্রুত কাজ করে যখন data memory-তে continuous থাকে।

Example:

```
[1][2][3][4][5]
```

এটি contiguous।

---

Check:

```python
a.flags
```

Output:

```
C_CONTIGUOUS : True
```

---

# Part 9 — C Order vs F Order

Memory arrangement দুই ধরনের।

---

## C Order

Row-major

Default NumPy।

Example:

```
1 2 3
4 5 6
```

Memory:

```
1 2 3 4 5 6
```

---

## F Order

Column-major

```
1 4 2 5 3 6
```

---

Create:

```python
a=np.array(
[
[1,2],
[3,4]
],
order='F'
)
```

---

# Part 10 — Vectorization

এটাই NumPy-এর speed-এর মূল কারণ।

---

## Python Loop

```python
numbers=list(range(1000000))

result=[]

for x in numbers:
    result.append(x*2)
```

---

## NumPy

```python
a=np.arange(1000000)

result=a*2
```

NumPy অনেক দ্রুত।

কারণ:

```
Python Loop

↓


Python interpreter


↓


Slow
```

কিন্তু:

```
NumPy

↓

C code

↓

Fast
```

---

# Part 11 — Performance Comparison

Measure:

```python
import time


start=time.time()

for i in range(1000000):
    x=i*i


print(
time.time()-start
)
```

---

NumPy:

```python
start=time.time()

a=np.arange(1000000)

x=a*a


print(
time.time()-start
)
```

NumPy faster হবে।

---

# Part 12 — Avoid Unnecessary Copies

Bad:

```python
for batch in data:

    temp=batch.copy()

    process(temp)
```

প্রতিবার copy memory খায়।

---

Better:

```python
process(batch)
```

যদি modify করার দরকার না হয়।

---

# Part 13 — dtype Optimization

Memory কমানোর সবচেয়ে ভালো উপায়।

Example:

```python
a=np.array(
[1,2,3,4]
)

print(a.dtype)
```

Output:

```
int64
```

---

যদি int8 যথেষ্ট হয়:

```python
a=np.array(
[1,2,3,4],
dtype=np.int8
)
```

Memory কমবে।

---

Size:

```python
print(a.nbytes)
```

---

Example:

```python
int64

8 bytes


int32

4 bytes


int8

1 byte
```

---

# Part 14 — Large Dataset Example

ধরো:

Image Dataset:

```
100000 images

224x224

RGB
```

Memory:

```
100000 × 224 × 224 × 3
```

Huge।

Optimization:

```python
images=np.array(
images,
dtype=np.uint8
)
```

কারণ:

Pixel range:

```
0-255
```

তাই uint8 যথেষ্ট।

---

# Part 15 — Memory Efficient Processing

Bad:

```python
data=np.load("huge.npy")

result=data*2
```

দুইটা বড় array memory নেয়।

---

Better:

```python
data *= 2
```

in-place operation।

---

Example:

```python
a=np.array([1,2,3])

a*=10

print(a)
```

Output:

```
[10 20 30]
```

---

# Part 16 — Broadcasting Memory Advantage

Example:

```python
a=np.array([
[1,2,3],
[4,5,6]
])


a+10
```

NumPy conceptually:

```
10 10 10
10 10 10
```

তৈরি করে না।

Memory save করে।

---

# Part 17 — Real Data Engineering Example

CSV Data:

```
10 million rows
```

Columns:

```
age
salary
score
```

Optimization:

### Before:

```python
data=np.array(rows)
```

dtype:

```
float64
```

---

### After:

```python
data=np.array(
rows,
dtype=np.float32
)
```

Memory প্রায় অর্ধেক হবে।

---

# Common Mistakes

## Mistake 1

ভাবা:

```
b=a[:]
```

copy তৈরি করে।

ভুল।

এটি view।

---

## Mistake 2

Large data-তে copy করা।

```python
data.copy()
```

Memory বাড়ায়।

---

## Mistake 3

সবসময় float64 ব্যবহার করা।

অনেক ক্ষেত্রে:

```
float32
int32
uint8
```

যথেষ্ট।

---

# Practice

## Easy

```python
a=np.array([1,2,3,4,5])
```

Tasks:

1. View তৈরি করো
2. Copy তৈরি করো
3. দুইটার difference দেখো
4. `shares_memory()` test করো

---

## Medium

একটি array:

```python
a=np.arange(1000000)
```

Tasks:

1. dtype দেখো
2. nbytes দেখো
3. int32 convert করো
4. Memory difference বের করো

---

## Hard

Image simulation:

```python
images=np.random.randint(
0,
256,
(100,224,224,3)
)
```

Tasks:

1. dtype check করো
2. uint8 convert করো
3. Memory before/after compare করো
4. Brightness increase করো without unnecessary copy

---

# Interview Questions

### 1. Difference between View and Copy?

View:

* Same memory
* Fast

Copy:

* New memory
* Independent

---

### 2. Why NumPy faster than Python list?

কারণ:

* C implementation
* Vectorization
* Contiguous memory

---

### 3. What is stride?

Memory-তে next element access করার byte distance।

---

### 4. Why dtype important?

Memory এবং performance optimize করার জন্য।

---

### 5. How reduce NumPy memory?

* Smaller dtype
* Avoid copy
* Use inplace operations
* Process batches

---

# Cheat Sheet

| Concept      | Method            |
| ------------ | ----------------- |
| Copy         | `np.copy()`       |
| View         | `array.view()`    |
| Memory check | `shares_memory()` |
| Size         | `nbytes`          |
| Type         | `dtype`           |
| Stride       | `strides`         |
| Inplace      | `+=`, `*=`, `-=`  |
| Contiguous   | `flags`           |

---

# Lesson 20 Summary

আজ তুমি শিখলে:

✅ NumPy Memory Model
✅ View vs Copy
✅ Memory Sharing
✅ Strides
✅ Contiguous Array
✅ Vectorization
✅ Performance Optimization
✅ dtype Optimization
✅ Large Dataset Handling

---

## Next Lesson 21 — NumPy File Handling & Real Dataset Processing

পরবর্তী Lesson:

* `np.save()`
* `np.load()`
* `.npy`
* `.npz`
* CSV Reading/Writing
* Large Dataset Storage
* Memory Mapping (`memmap`)
* ML Dataset Pipeline

এগুলো Data Engineer এবং ML Engineer-এর জন্য production-level skill।
# Module 9 — Lesson 21: NumPy File Handling & Real Dataset Processing (Mastery Guide)

Machine Learning এবং Data Engineering-এ শুধু array তৈরি করলেই হবে না। তোমাকে data:

* Save করতে হবে
* Load করতে হবে
* Share করতে হবে
* Large dataset efficiently handle করতে হবে

আজ আমরা NumPy দিয়ে **real dataset storage pipeline** শিখব।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* `np.save()`
* `np.load()`
* `.npy` file
* `.npz` file
* `np.savez()`
* CSV read/write
* Text file handling
* Memory Mapping (`memmap`)
* Large dataset processing
* ML dataset pipeline

---

# Part 1 — কেন NumPy File Handling দরকার?

ধরো তুমি:

* Image preprocessing করেছ
* Feature extraction করেছ
* Model training data তৈরি করেছ

এখন প্রতিবার আবার calculation করা expensive।

তাই:

```text
Raw Data

↓

Preprocessing

↓

NumPy Array

↓

Save

↓

Future Training
```

---

# Part 2 — np.save()

NumPy array save করার জন্য।

Example:

```python id="save01"
import numpy as np

data = np.array([
    10,
    20,
    30,
    40
])


np.save(
    "numbers.npy",
    data
)
```

এখন file তৈরি হবে:

```
numbers.npy
```

---

# .npy কী?

`.npy` হলো NumPy-এর binary format।

Features:

✅ Fast
✅ Preserve dtype
✅ Preserve shape
✅ Less storage

---

# Part 3 — np.load()

Saved file load করা।

```python id="load01"
loaded = np.load(
    "numbers.npy"
)


print(loaded)
```

Output:

```
[10 20 30 40]
```

---

Check:

```python id="load02"
print(loaded.dtype)

print(loaded.shape)
```

Original information থাকবে।

---

# Part 4 — Save Matrix

Example:

```python id="matrix01"
matrix = np.array([
    [1,2,3],
    [4,5,6]
])


np.save(
    "matrix.npy",
    matrix
)
```

Load:

```python id="matrix02"
x=np.load(
"matrix.npy"
)

print(x)
```

Output:

```
[
[1 2 3]
[4 5 6]
]
```

---

# Part 5 — np.savez()

Multiple arrays save করতে ব্যবহার হয়।

Example:

```python id="savez01"
X = np.array([
[1,2],
[3,4]
])


y = np.array([
0,
1
])


np.savez(
    "dataset.npz",
    features=X,
    labels=y
)
```

File:

```
dataset.npz
```

---

# Load npz

```python id="savez02"
data=np.load(
"dataset.npz"
)


print(data.files)
```

Output:

```
['features','labels']
```

---

Access:

```python id="savez03"
X_loaded=data["features"]

y_loaded=data["labels"]
```

---

# .npy vs .npz

| .npy         | .npz            |
| ------------ | --------------- |
| Single array | Multiple arrays |
| Simple       | Dataset storage |
| Faster       | More flexible   |

---

# Part 6 — Compression with savez_compressed()

Large data-এর জন্য।

```python id="compress01"
np.savez_compressed(
    "data_compressed.npz",
    X=X,
    y=y
)
```

Advantages:

* Less disk space

Disadvantage:

* Slightly slower

---

# Part 7 — CSV File Handling

অনেক real dataset CSV format-এ থাকে।

Example:

```python id="csv01"
data=np.array([
[1,100],
[2,200],
[3,300]
])
```

Save:

```python id="csv02"
np.savetxt(
    "data.csv",
    data,
    delimiter=","
)
```

---

File:

```
data.csv

1,100
2,200
3,300
```

---

# Load CSV

```python id="csv03"
loaded=np.loadtxt(
    "data.csv",
    delimiter=","
)


print(loaded)
```

Output:

```
[
[1 100]
[2 200]
[3 300]
]
```

---

# Part 8 — CSV Header Handling

Example:

```
id,price
1,500
2,700
```

Load:

```python id="csv04"
data=np.loadtxt(
    "data.csv",
    delimiter=",",
    skiprows=1
)
```

---

# Part 9 — String Data Loading

NumPy মূলত numeric data-এর জন্য।

Example:

```
name,age
Ali,25
Rahim,30
```

Use:

```python id="string01"
data=np.genfromtxt(
    "people.csv",
    delimiter=",",
    dtype=None,
    encoding="utf-8"
)
```

---

# Part 10 — Memory Mapping (Very Important)

Large dataset:

Example:

```
100GB dataset
```

RAM:

```
16GB
```

Problem:

পুরো file memory-তে load করা যাবে না।

Solution:

`memmap`

---

# Normal Loading

```python id="normalload"
data=np.load(
"huge.npy"
)
```

সব RAM-এ আসে।

---

# Memory Mapping

```python id="memmap01"
data=np.load(
    "huge.npy",
    mmap_mode="r"
)
```

এখন:

* পুরো data RAM-এ আসে না
* প্রয়োজন অনুযায়ী অংশ load হয়

---

# memmap Modes

| Mode | কাজ           |
| ---- | ------------- |
| r    | Read only     |
| r+   | Read/write    |
| w+   | Create        |
| c    | Copy on write |

---

# Part 11 — Create Memory Mapped Array

Example:

```python id="create_memmap"
fp=np.memmap(
    "large.dat",
    dtype="float32",
    mode="w+",
    shape=(10000,100)
)
```

এখন disk-based array।

---

Write:

```python id="write_memmap"
fp[0]=np.ones(100)

fp.flush()
```

---

# Part 12 — ML Dataset Pipeline

Real workflow:

```
Raw Images

↓

Preprocessing

↓

NumPy Array

↓

Save .npy

↓

Training
```

Example:

Images:

```python id="imagepipeline"
images.shape

(50000,224,224,3)
```

Save:

```python id="saveimages"
np.save(
"images.npy",
images
)
```

---

Training:

```python id="trainload"
images=np.load(
"images.npy",
mmap_mode="r"
)
```

---

# Part 13 — Dataset Split Save

Machine Learning:

```python
Train
Validation
Test
```

Example:

```python id="split01"
X_train=np.random.random(
(800,10)
)

X_test=np.random.random(
(200,10)
)
```

Save:

```python id="split02"
np.savez(
"split_data.npz",
train=X_train,
test=X_test
)
```

---

# Part 14 — Real Data Engineering Example

E-commerce Dataset:

Columns:

```
customer_id
age
income
purchase
```

Create:

```python id="ecommerce01"
customers=np.array([
[1,25,50000,2000],
[2,30,70000,5000],
[3,22,30000,1000]
])
```

Save:

```python id="ecommerce02"
np.save(
"customers.npy",
customers
)
```

Future:

```python id="ecommerce03"
customers=np.load(
"customers.npy"
)
```

---

# Part 15 — Performance Tips

## Use .npy instead of CSV

CSV:

```
slow
large
dtype lost
```

.npy:

```
fast
compact
dtype preserved
```

---

## Batch Processing

Bad:

```python
data=np.load(
"huge.npy"
)
```

Better:

```python
for batch in data:
    process(batch)
```

---

## Use mmap

Huge file:

```python
np.load(
file,
mmap_mode="r"
)
```

---

# Common Mistakes

## Mistake 1

CSV দিয়ে huge dataset store করা।

Better:

```
.npy
.npz
Parquet
```

---

## Mistake 2

Huge file normal load করা।

Wrong:

```python
np.load(
"100GB.npy"
)
```

Use:

```python
mmap_mode="r"
```

---

## Mistake 3

dtype ignore করা।

Example:

Image:

```
0-255
```

Use:

```python
uint8
```

না হলে:

```
float64
```

memory বেশি খাবে।

---

# Practice

## Easy

Create:

```python
a=np.arange(100)
```

Tasks:

1. Save as `.npy`
2. Load
3. Check shape
4. Check dtype

---

## Medium

Create:

```python
X=np.random.random(
(1000,20)
)

y=np.random.randint(
0,2,
1000
)
```

Tasks:

1. Save using `.npz`
2. Load
3. Separate X and y

---

## Hard

Image Dataset:

```python
images=np.random.randint(
0,
256,
(1000,64,64,3),
dtype=np.uint8
)
```

Tasks:

1. Save images
2. Load with mmap
3. Check memory usage
4. Create train/test split
5. Save split dataset

---

# Interview Questions

### 1. Difference between npy and npz?

`.npy`

→ Single array

`.npz`

→ Multiple arrays

---

### 2. Why NumPy binary format faster than CSV?

কারণ:

* Binary storage
* No parsing
* Shape/dtype preserved

---

### 3. What is memmap?

Disk-based array access technique যেখানে পুরো dataset RAM-এ load করতে হয় না।

---

### 4. When use savez_compressed?

Large dataset যেখানে storage কমাতে চাই।

---

### 5. Why dtype important when saving?

Memory এবং performance optimize করার জন্য।

---

# Cheat Sheet

| Function                | কাজ                |
| ----------------------- | ------------------ |
| `np.save()`             | Save array         |
| `np.load()`             | Load array         |
| `np.savez()`            | Multiple arrays    |
| `np.savez_compressed()` | Compressed save    |
| `np.savetxt()`          | Save CSV           |
| `np.loadtxt()`          | Load CSV           |
| `np.genfromtxt()`       | Complex CSV        |
| `mmap_mode`             | Large file loading |
| `np.memmap()`           | Disk array         |

---

# Lesson 21 Summary

আজ তুমি শিখলে:

✅ NumPy file storage
✅ `.npy`
✅ `.npz`
✅ CSV handling
✅ Compression
✅ Memory mapping
✅ Large dataset processing
✅ ML dataset pipeline

---

## Next Lesson 22 — NumPy Practical Project: Build a Mini Data Processing Pipeline

পরবর্তী Lesson-এ আমরা একটি production-style project করবো:

**E-commerce Data Analytics Pipeline using NumPy**

যেখানে থাকবে:

* Raw dataset creation
* Cleaning
* Filtering
* Feature engineering
* Statistics
* Ranking
* Saving processed data

এটি তোমার Data Engineer + ML Engineer foundation শক্ত করবে।
# Module 10 — Lesson 22: NumPy Practical Project — E-commerce Data Processing Pipeline (Production Style)

এখন পর্যন্ত তুমি NumPy-এর প্রায় সব core concept শিখেছো:

✅ Array
✅ Indexing
✅ Broadcasting
✅ Statistics
✅ Linear Algebra
✅ Random Data
✅ Memory Optimization
✅ File Handling

এখন আমরা সবকিছু একসাথে ব্যবহার করে একটি **real-world Data Engineering pipeline** তৈরি করবো।

Project:

# E-commerce Sales Analytics Pipeline

আমরা একটি fake e-commerce dataset তৈরি করবো এবং:

```
Raw Data

↓

Data Cleaning

↓

Filtering

↓

Feature Engineering

↓

Analytics

↓

Save Processed Data
```

---

# Project Requirements

Dataset:

```
customer_id
age
income
product_price
quantity
rating
category
```

Example:

| ID | Age | Income | Price | Qty | Rating |
| -- | --- | ------ | ----- | --- | ------ |
| 1  | 25  | 50000  | 1000  | 2   | 4.5    |
| 2  | 35  | 70000  | 2500  | 1   | 5      |

---

# Step 1 — Import NumPy

```python
import numpy as np
```

---

# Step 2 — Generate Raw Dataset

আমরা 10,000 customers তৈরি করবো।

---

## Customer ID

```python
customer_id = np.arange(
    1,
    10001
)
```

Output:

```
[1 2 3 ... 10000]
```

---

## Age

18-60:

```python
age = np.random.randint(
    18,
    60,
    10000
)
```

---

## Income

Normal distribution:

Mean:

```
50000
```

Std:

```
15000
```

```python
income = np.random.normal(
    50000,
    15000,
    10000
)
```

---

## Product Price

```python
price = np.random.randint(
    100,
    10000,
    10000
)
```

---

## Quantity

```python
quantity = np.random.randint(
    1,
    10,
    10000
)
```

---

## Rating

```python
rating = np.random.uniform(
    1,
    5,
    10000
)
```

---

# Step 3 — Create Dataset

সব column combine:

```python
data = np.column_stack(
    (
        customer_id,
        age,
        income,
        price,
        quantity,
        rating
    )
)
```

Check:

```python
print(data.shape)
```

Output:

```
(10000,6)
```

---

# Step 4 — Dataset Inspection

First 5 rows:

```python
print(
data[:5]
)
```

---

Shape:

```python
data.shape
```

---

Datatype:

```python
data.dtype
```

---

# Problem

সব data float হয়ে গেছে।

কারণ:

income এবং rating float।

Example:

```
[1. 25. 50000.5]
```

---

# Step 5 — Data Cleaning

## Remove Negative Income

Fake data-তে কিছু negative থাকতে পারে।

Check:

```python
income[income < 0]
```

---

Filter:

```python
clean_data = data[
    data[:,2] > 0
]
```

---

# Step 6 — Remove Invalid Rating

Valid:

```
1 <= rating <= 5
```

Filter:

```python
clean_data = clean_data[
    (clean_data[:,5]>=1)
    &
    (clean_data[:,5]<=5)
]
```

---

# Step 7 — Feature Engineering

Data Engineer হিসেবে নতুন feature তৈরি করতে হয়।

---

## Total Purchase Amount

Formula:

```
price × quantity
```

---

Price:

```python
price_column = clean_data[:,3]
```

Quantity:

```python
qty_column = clean_data[:,4]
```

Calculate:

```python
total_purchase = (
    price_column *
    qty_column
)
```

---

Add column:

```python
processed = np.column_stack(
(
clean_data,
total_purchase
)
)
```

Now:

Shape:

```python
processed.shape
```

Output:

```
(rows,7)
```

---

New column:

```
total_purchase
```

---

# Step 8 — Sales Analytics

## Total Revenue

```python
revenue = np.sum(
processed[:,6]
)

print(revenue)
```

---

## Average Order Value

```python
average = np.mean(
processed[:,6]
)

print(average)
```

---

## Median Purchase

```python
median = np.median(
processed[:,6]
)

print(median)
```

---

# Step 9 — Top Customers

Highest purchase বের করবো।

Sort index:

```python
idx = np.argsort(
processed[:,6]
)
```

Descending:

```python
idx = idx[::-1]
```

Top 10:

```python
top10 = processed[
    idx[:10]
]
```

---

Output:

```
Customer ID
Age
Income
Price
Quantity
Rating
Total Purchase
```

---

# Step 10 — Customer Segmentation

Business-এ customer ভাগ করা হয়।

Rule:

High Value:

```
Purchase > 20000
```

---

```python
high_value = processed[
    processed[:,6] > 20000
]
```

---

Count:

```python
len(high_value)
```

---

# Step 11 — Age Analysis

Young customers:

```
age < 30
```

```python
young = processed[
    processed[:,1] < 30
]
```

---

Average purchase:

```python
np.mean(
young[:,6]
)
```

---

# Step 12 — Income Analysis

High income:

```
income > 70000
```

```python
rich = processed[
    processed[:,2] > 70000
]
```

---

Average:

```python
np.mean(
rich[:,6]
)
```

---

# Step 13 — Find Outliers

Purchase:

```python
purchase = processed[:,6]
```

Mean:

```python
mean = np.mean(
purchase
)
```

Std:

```python
std = np.std(
purchase
)
```

---

Z-score:

Formula:

```
z = (x - mean)/std
```

---

```python
z_score = (
    purchase - mean
) / std
```

---

Outlier:

```python
outliers = processed[
    np.abs(z_score)>3
]
```

---

# Step 14 — Normalize Feature

Machine Learning-এর জন্য।

Formula:

```
(x-min)/(max-min)
```

---

Price normalize:

```python
price = processed[:,3]


normalized_price = (
price-price.min()
) / (
price.max()-price.min()
)
```

---

# Step 15 — Save Processed Dataset

Save:

```python
np.save(
    "processed_sales.npy",
    processed
)
```

---

Load:

```python
data=np.load(
"processed_sales.npy"
)
```

---

# Step 16 — Save Analytics Report

Create summary:

```python
report=np.array(
[
revenue,
average,
median
]
)
```

Save:

```python
np.save(
"report.npy",
report
)
```

---

# Complete Pipeline Architecture

Production Data Pipeline:

```
Raw Data Generator

        |
        ↓

NumPy Array

        |
        ↓

Cleaning

        |
        ↓

Feature Engineering

        |
        ↓

Analytics

        |
        ↓

Save .npy

        |
        ↓

ML Training / Dashboard
```

---

# Performance Improvement

## Use dtype

Before:

```python
float64
```

Memory:

Large

---

Better:

```python
processed.astype(
np.float32
)
```

---

# Advanced Version

Real company pipeline:

```
CSV
 |
 |
Pandas
 |
 |
NumPy Processing
 |
 |
Feature Store
 |
 |
ML Model
```

---

# Interview Questions

### 1. Why use NumPy for data processing?

Because:

* Fast
* Vectorized
* Memory efficient

---

### 2. Difference NumPy and Pandas?

| NumPy           | Pandas             |
| --------------- | ------------------ |
| Numerical array | Table data         |
| Fast math       | Data analysis      |
| ML foundation   | Business analytics |

---

### 3. Why feature engineering?

Raw data থেকে ML-friendly features তৈরি করার জন্য।

---

### 4. Why normalize data?

Different scale feature একই range-এ আনার জন্য।

---

### 5. Why save processed data?

Repeated preprocessing time কমানোর জন্য।

---

# Final Project Practice

নিজে implement করো:

Dataset:

```
100000 customers
```

Columns:

```
ID
Age
Income
Price
Quantity
Rating
```

Tasks:

1. Generate dataset
2. Clean invalid data
3. Create total_sales feature
4. Find top 100 customers
5. Detect outliers
6. Normalize price
7. Save `.npy`
8. Load and verify

---

# Lesson 22 Summary

আজ তুমি শিখলে:

✅ Real Data Pipeline
✅ Data Generation
✅ Cleaning
✅ Filtering
✅ Feature Engineering
✅ Analytics
✅ Ranking
✅ Outlier Detection
✅ Normalization
✅ Saving Processed Dataset

---

## Next Lesson 23 — NumPy + Machine Learning Pipeline

পরবর্তী Lesson:

**Build ML preprocessing pipeline with NumPy**

শিখব:

* Feature matrix তৈরি
* Label encoding manually
* Train/Test split
* Scaling
* Batch generation
* Mini-batch training preparation

এটি তোমাকে ML Engineer track-এর দিকে নিয়ে যাবে।
# Module 11 — Lesson 23: NumPy + Machine Learning Data Pipeline (Mastery Guide)

এখন আমরা NumPy-কে **Machine Learning workflow-এর সাথে connect করবো**।

একজন ML Engineer হিসেবে তোমাকে raw data থেকে model-ready data তৈরি করতে হবে।

Real ML Pipeline:

```text
Raw Dataset

      ↓

Data Cleaning

      ↓

Feature Engineering

      ↓

Encoding

      ↓

Scaling

      ↓

Train/Test Split

      ↓

Batch Generation

      ↓

Model Training
```

আজ আমরা NumPy দিয়ে পুরো pipeline তৈরি করবো।

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

* Feature Matrix কী
* Label Vector কী
* X এবং y তৈরি করা
* Train/Test split
* Random shuffling
* Normalization
* Standardization
* One-hot encoding
* Mini-batch generation
* ML-ready dataset তৈরি

---

# Part 1 — Feature Matrix এবং Label

Machine Learning dataset সাধারণত দুই ভাগ:

## Features (X)

Model যেগুলো দেখে।

Example:

```text
Age
Income
Experience
```

---

## Label (y)

Model যেটা predict করে।

Example:

```text
Buy / Not Buy
```

---

Example dataset:

| Age | Income | Buy |
| --- | ------ | --- |
| 25  | 50000  | 1   |
| 30  | 70000  | 1   |
| 20  | 30000  | 0   |

---

Feature:

```python
X =
[
[25,50000],
[30,70000],
[20,30000]
]
```

Label:

```python
y =
[1,1,0]
```

---

# Part 2 — Create Dataset

```python
import numpy as np
```

Dataset:

```python
data = np.array([
    [25,50000,1],
    [30,70000,1],
    [20,30000,0],
    [35,90000,1],
    [22,40000,0]
])
```

Shape:

```python
print(data.shape)
```

Output:

```
(5,3)
```

---

# Part 3 — Split X and y

Features:

```python
X = data[:, :2]
```

Check:

```python
print(X)
```

Output:

```
[
[25 50000]
[30 70000]
[20 30000]
[35 90000]
[22 40000]
]
```

---

Label:

```python
y = data[:,2]
```

Output:

```
[1 1 0 1 0]
```

---

# Important

ML convention:

```text
X → Features

y → Target
```

---

# Part 4 — Train/Test Split Manually

Normally:

```text
80% Train

20% Test
```

---

Dataset size:

```python
n = len(X)

print(n)
```

Output:

```
5
```

---

Split index:

```python
split = int(
    n*0.8
)
```

Output:

```
4
```

---

Train:

```python
X_train = X[:split]

y_train = y[:split]
```

---

Test:

```python
X_test = X[split:]

y_test = y[split:]
```

---

# Problem

এভাবে split করলে data order maintain থাকে।

ML-এ random split দরকার।

---

# Part 5 — Random Shuffle

Dataset:

```python
indices = np.arange(
    len(X)
)
```

Output:

```
[0 1 2 3 4]
```

---

Shuffle:

```python
np.random.shuffle(indices)

print(indices)
```

Example:

```
[3 1 4 0 2]
```

---

Apply:

```python
X = X[indices]

y = y[indices]
```

এখন data random।

---

# Part 6 — Better Train/Test Split Function

নিজে function বানাই:

```python
def train_test_split(
    X,
    y,
    test_size=0.2
):

    indices=np.arange(
        len(X)
    )

    np.random.shuffle(
        indices
    )


    split=int(
        len(X)*(1-test_size)
    )


    train_idx=indices[:split]

    test_idx=indices[split:]


    return (
        X[train_idx],
        X[test_idx],
        y[train_idx],
        y[test_idx]
    )
```

---

Use:

```python
X_train,X_test,y_train,y_test = train_test_split(
    X,
    y
)
```

---

# Part 7 — Feature Scaling

Machine Learning model scale sensitive।

Example:

Feature 1:

```
Age

20-50
```

Feature 2:

```
Income

30000-90000
```

Income dominates করবে।

Solution:

Scaling।

---

# Min-Max Normalization

Formula:

```
x' = (x-min)/(max-min)
```

---

Example:

```python
feature=np.array([
10,
20,
30,
40,
50
])
```

---

Code:

```python
normalized = (
    feature-feature.min()
) / (
    feature.max()-feature.min()
)
```

Output:

```
[0
0.25
0.5
0.75
1]
```

---

# Apply to Matrix

Dataset:

```python
X=np.array([
[20,30000],
[30,50000],
[40,70000]
])
```

---

Column wise:

```python
X_min=X.min(axis=0)

X_max=X.max(axis=0)
```

---

Normalize:

```python
X_scaled = (
    X-X_min
) / (
    X_max-X_min
)
```

---

Output:

```
[
[0,0],
[0.5,0.5],
[1,1]
]
```

---

# Part 8 — Standardization (Z-score)

Formula:

```
z = (x-mean)/std
```

---

Code:

```python
mean=X.mean(axis=0)

std=X.std(axis=0)


X_standard = (
    X-mean
)/std
```

---

Output:

Mean:

```
0
```

Std:

```
1
```

---

# Normalization vs Standardization

| Normalization | Standardization |
| ------------- | --------------- |
| Range 0-1     | Mean 0 Std 1    |
| Image data    | Linear models   |
| Bounded data  | General ML      |

---

# Part 9 — Categorical Data Encoding

Example:

Categories:

```
Red
Blue
Green
```

Machine learning numbers চায়।

---

## Label Encoding

```python
colors=np.array([
"red",
"blue",
"green",
"red"
])
```

Mapping:

```
red=0

blue=1

green=2
```

---

Manual:

```python
unique,encoded=np.unique(
    colors,
    return_inverse=True
)

print(encoded)
```

Output:

```
[2 0 1 2]
```

---

# Part 10 — One Hot Encoding

Example:

```
Red

Blue

Green
```

Convert:

```
Red

[1 0 0]


Blue

[0 1 0]
```

---

Code:

```python
categories=np.array([
0,
1,
2,
1
])


one_hot=np.eye(3)[categories]

print(one_hot)
```

Output:

```
[
[1 0 0]
[0 1 0]
[0 0 1]
[0 1 0]
]
```

---

# Part 11 — Mini Batch Generation

Deep Learning-এ পুরো dataset একসাথে train করা যায় না।

Example:

```
100000 samples

Batch size = 32
```

---

Function:

```python
def batch_generator(
    X,
    y,
    batch_size
):

    for i in range(
        0,
        len(X),
        batch_size
    ):

        yield (
            X[i:i+batch_size],
            y[i:i+batch_size]
        )
```

---

Use:

```python
for X_batch,y_batch in batch_generator(
    X,
    y,
    2
):

    print(X_batch)
    print(y_batch)
```

---

Output:

```
Batch 1

Batch 2

Batch 3
```

---

# Part 12 — Image Dataset Example

CNN এর জন্য:

Image:

```
10000 images

224x224x3
```

Shape:

```python
X.shape
```

Output:

```
(10000,224,224,3)
```

Label:

```python
y.shape
```

Output:

```
(10000,)
```

---

Normalize:

```python
X=X/255.0
```

কারণ:

Pixel:

```
0-255
```

Convert:

```
0-1
```

---

# Part 13 — Complete ML Pipeline

```python
# 1. Load data

data=np.load(
"dataset.npy"
)


# 2. Split

X=data[:,:-1]

y=data[:,-1]


# 3. Shuffle

idx=np.random.permutation(
len(X)
)


X=X[idx]

y=y[idx]


# 4. Scale

X=(X-X.mean(0))/X.std(0)


# 5. Train/Test

split=int(
len(X)*0.8
)


X_train=X[:split]

X_test=X[split:]


y_train=y[:split]

y_test=y[split:]
```

---

# Production ML Pipeline

```
Dataset

 |

Load

 |

NumPy Array

 |

Cleaning

 |

Feature Engineering

 |

Encoding

 |

Scaling

 |

Split

 |

Batch

 |

Model
```

---

# Practice

## Easy

Create:

```python
X=np.array([
[10,100],
[20,200],
[30,300]
])
```

Tasks:

1. Normalize
2. Standardize

---

## Medium

Dataset:

```python
[
Age,
Salary,
Purchased
]
```

Tasks:

1. Create X
2. Create y
3. Shuffle
4. Split 80/20

---

## Hard

Build complete pipeline:

Dataset:

```
10000 customers
```

Columns:

```
Age
Income
Gender
Purchase
```

Tasks:

1. Encode Gender
2. Normalize features
3. Split train/test
4. Create batch generator
5. Save processed dataset

---

# Interview Questions

### 1. Why split train and test?

Model-এর generalization test করার জন্য।

---

### 2. Why scaling needed?

Different range feature-এর effect balance করার জন্য।

---

### 3. Normalization vs Standardization?

Normalization:

```
0-1 range
```

Standardization:

```
mean=0 std=1
```

---

### 4. Why mini batch?

* Less memory
* Faster training
* Better optimization

---

### 5. What is feature matrix?

Input variables-এর matrix।

---

# Cheat Sheet

| Task        | NumPy Method              |
| ----------- | ------------------------- |
| Split X/y   | Slicing                   |
| Shuffle     | `np.random.shuffle()`     |
| Permutation | `np.random.permutation()` |
| Normalize   | Min-Max formula           |
| Standardize | Mean/Std                  |
| Encoding    | `np.unique()`             |
| One hot     | `np.eye()`                |
| Batch       | Generator                 |

---

# Lesson 23 Summary

আজ তুমি শিখলে:

✅ ML Dataset Structure
✅ Feature Matrix
✅ Label Vector
✅ Train/Test Split
✅ Shuffle
✅ Normalization
✅ Standardization
✅ Encoding
✅ Mini Batch Generation
✅ Complete ML Pipeline

---

## Next Lesson 24 — NumPy Advanced Project: Build Neural Network Operations From Scratch

পরবর্তী Lesson-এ আমরা NumPy দিয়ে:

* Forward propagation
* Weight initialization
* Activation function
* Loss calculation
* Gradient calculation
* Simple Neural Network

নিজে implement করবো।

এটি Deep Learning-এর ভিতরের mechanism বুঝতে সাহায্য করবে।
# Module 12 — Lesson 24: Build Neural Network Operations From Scratch Using NumPy (Mastery Guide)

আজকের Lesson অনেক গুরুত্বপূর্ণ।

এখন আমরা **Deep Learning framework (TensorFlow/PyTorch) ছাড়াই** NumPy দিয়ে একটি ছোট Neural Network তৈরি করবো।

এতে তুমি বুঝবে:

* Neural Network ভিতরে কীভাবে কাজ করে
* Matrix multiplication কোথায় লাগে
* Weight কেন দরকার
* Activation function কী করে
* Loss কীভাবে calculate হয়

---

# Learning Objectives

এই Lesson শেষে তুমি শিখবে:

✅ Neural Network Architecture
✅ Weight Initialization
✅ Forward Propagation
✅ Activation Function
✅ Sigmoid
✅ ReLU
✅ Loss Function
✅ Prediction
✅ Simple Binary Classifier

---

# Part 1 — Neural Network Basic Structure

একটি Neural Network:

```
Input Layer

      ↓

Hidden Layer

      ↓

Output Layer
```

Example:

```
2 Features

   ↓

3 Neurons

   ↓

1 Output
```

Mathematically:

```
Input × Weight + Bias
```

---

# Part 2 — Dataset Create

আমরা simple binary classification করবো।

Problem:

Input:

```
x1
x2
```

Output:

```
0 অথবা 1
```

Example:

```python
import numpy as np


X = np.array([
    [0,0],
    [0,1],
    [1,0],
    [1,1]
])


y = np.array([
    0,
    1,
    1,
    1
])
```

এটি OR gate problem।

---

# Part 3 — Understand Shapes

X:

```python
print(X.shape)
```

Output:

```
(4,2)
```

Meaning:

```
4 samples

2 features
```

---

y:

```python
print(y.shape)
```

Output:

```
(4,)
```

---

# Part 4 — Weight Initialization

Neural Network শুরুতে random weight নেয়।

Input:

```
2 features
```

Hidden:

```
3 neurons
```

তাহলে:

```
Weight shape:

(2,3)
```

---

Create:

```python
np.random.seed(42)


W1 = np.random.randn(
    2,
    3
)


b1 = np.zeros(
    (1,3)
)
```

---

Check:

```python
print(W1.shape)

print(b1.shape)
```

Output:

```
(2,3)

(1,3)
```

---

# Part 5 — Activation Function

Neural network-এর ভিতরে non-linearity আনার জন্য activation ব্যবহার হয়।

---

# ReLU Function

Formula:

```
max(0,x)
```

Code:

```python
def relu(x):

    return np.maximum(
        0,
        x
    )
```

Example:

```python
a=np.array([
-2,
0,
3
])


print(
relu(a)
)
```

Output:

```
[0 0 3]
```

---

# Part 6 — Forward Propagation

এখন প্রথম layer:

Formula:

```
Z1 = XW1 + b1
```

Code:

```python
Z1 = X @ W1 + b1
```

Check:

```python
print(Z1)
```

Shape:

```
(4,3)
```

কারণ:

```
(4,2)

×

(2,3)

=

(4,3)
```

---

Activation:

```python
A1 = relu(Z1)
```

---

# Part 7 — Output Layer

Hidden layer থেকে output:

Architecture:

```
2 Input

↓

3 Hidden

↓

1 Output
```

Weight:

```
(3,1)
```

---

Create:

```python
W2 = np.random.randn(
    3,
    1
)


b2 = np.zeros(
    (1,1)
)
```

---

Output calculation:

```python
Z2 = A1 @ W2 + b2
```

Shape:

```
(4,1)
```

---

# Part 8 — Sigmoid Activation

Binary classification-এর জন্য sigmoid ব্যবহার হয়।

Formula:

```
1
------
1 + e^-x
```

---

Code:

```python
def sigmoid(x):

    return 1/(1+np.exp(-x))
```

---

Apply:

```python
prediction = sigmoid(Z2)
```

Output:

Example:

```
[
0.45
0.72
0.88
0.91
]
```

Meaning:

Probability।

---

# Part 9 — Complete Forward Function

আমরা function বানাই:

```python
def forward(X):

    Z1 = X @ W1 + b1

    A1 = relu(Z1)


    Z2 = A1 @ W2 + b2

    A2 = sigmoid(Z2)


    return A2
```

---

Run:

```python
output = forward(X)

print(output)
```

---

# Part 10 — Prediction

Probability থেকে class:

Rule:

```
if probability > 0.5

class = 1
```

---

Code:

```python
predictions = (
    output > 0.5
).astype(int)


print(predictions)
```

---

# Part 11 — Loss Function

Model কত ভুল করছে সেটা measure করতে loss লাগে।

Binary Cross Entropy:

Formula:

```
Loss =
-y log(p)
-
(1-y) log(1-p)
```

---

Code:

```python
def binary_cross_entropy(
    y,
    p
):

    loss = -(
        y*np.log(p)
        +
        (1-y)*np.log(1-p)
    )

    return np.mean(loss)
```

---

Calculate:

```python
loss = binary_cross_entropy(
    y.reshape(-1,1),
    output
)


print(loss)
```

---

# Part 12 — Why Training Needed?

এখন:

```
Random Weight

↓

Prediction

↓

Loss
```

কিন্তু weight update হচ্ছে না।

Training-এর জন্য দরকার:

```
Forward

↓

Loss

↓

Gradient

↓

Update Weight
```

---

# Part 13 — Gradient Descent Concept

Formula:

```
New Weight

=

Old Weight

-

Learning Rate × Gradient
```

---

Example:

```python
learning_rate = 0.01
```

---

# Part 14 — Simple Gradient Idea

Suppose:

Weight:

```
5
```

Gradient:

```
2
```

Learning rate:

```
0.1
```

Update:

```
5 - (0.1×2)

=4.8
```

---

# Part 15 — Neural Network Flow

Complete:

```
Input X


↓

X @ W1 + b1


↓

ReLU


↓

A1 @ W2 + b2


↓

Sigmoid


↓

Prediction


↓

Loss
```

---

# Part 16 — NumPy vs PyTorch Relation

এই code:

```python
X @ W + b
```

PyTorch:

```python
torch.matmul(X,W)+b
```

TensorFlow:

```python
tf.matmul(X,W)+b
```

Concept একই।

---

# Part 17 — Real ML Example

Image:

```
28×28 pixels
```

Flatten:

```
784 features
```

Network:

```
784

↓

128 neurons

↓

10 classes
```

Weights:

First layer:

```
(784,128)
```

Second:

```
(128,10)
```

---

# Common Mistakes

## Mistake 1

Wrong weight shape:

```python
W=(3,2)
```

যেখানে দরকার:

```
(2,3)
```

সবসময় shape check করো।

---

## Mistake 2

Activation ভুলে যাওয়া।

Without activation:

```
Only linear model
```

---

## Mistake 3

Sigmoid input huge হওয়া।

Example:

```
exp(1000)
```

overflow হতে পারে।

---

# Practice

## Easy

Implement:

```python
def sigmoid(x):
    pass
```

Test:

```python
[-1,0,1]
```

---

## Medium

Create:

```
Input:

3 features


Hidden:

4 neurons


Output:

1 neuron
```

Find:

1. Weight shapes
2. Forward propagation

---

## Hard

Build:

```
XOR Dataset
```

Architecture:

```
2

↓

4

↓

1
```

Implement:

1. Weight initialization
2. Forward pass
3. Prediction
4. Loss calculation

---

# Interview Questions

### 1. Why matrix multiplication in neural network?

কারণ:

Input এবং weight combine করার জন্য।

---

### 2. Why activation function?

Non-linear pattern শেখার জন্য।

---

### 3. Why sigmoid in output layer?

Binary probability output দেয়।

---

### 4. Difference between weight and bias?

Weight:

```
Feature importance
```

Bias:

```
Offset control
```

---

### 5. What is forward propagation?

Input থেকে output calculate করার process।

---

# Cheat Sheet

| Concept      | Formula              |
| ------------ | -------------------- |
| Linear layer | `XW+b`               |
| ReLU         | `max(0,x)`           |
| Sigmoid      | `1/(1+e^-x)`         |
| Prediction   | `p>0.5`              |
| Loss         | Binary Cross Entropy |
| Update       | `W-lr*gradient`      |

---

# Lesson 24 Summary

আজ তুমি শিখলে:

✅ Neural Network structure
✅ Weight initialization
✅ Forward propagation
✅ Matrix operation
✅ ReLU
✅ Sigmoid
✅ Prediction
✅ Loss calculation
✅ ML framework-এর ভিতরের কাজ

---

## Next Lesson 25 — NumPy Capstone Project: Complete Machine Learning Pipeline

পরবর্তী Lesson-এ আমরা বানাবো:

**NumPy দিয়ে Complete ML System**

যেখানে থাকবে:

* Dataset generation
* Preprocessing
* Feature engineering
* Neural Network
* Training loop
* Backpropagation
* Evaluation

এটি NumPy mastery-এর final project হবে।
# Module 13 — Lesson 25: NumPy Capstone Project — Build a Complete Neural Network From Scratch

আজকের Lesson হলো NumPy Mastery Course-এর **Capstone Project**।

এখানে আমরা শুরু থেকে শেষ পর্যন্ত একটি Machine Learning system তৈরি করবো:

```text
Dataset

 ↓

Preprocessing

 ↓

Neural Network

 ↓

Forward Propagation

 ↓

Loss Calculation

 ↓

Backpropagation

 ↓

Weight Update

 ↓

Prediction

 ↓

Evaluation
```

এটি করলে তুমি বুঝবে TensorFlow/PyTorch ভিতরে কীভাবে কাজ করে।

---

# Project: Binary Classification Neural Network

Problem:

আমরা predict করবো:

```
Customer Purchase

0 = Not Buy
1 = Buy
```

Input:

```
Age
Income
```

Output:

```
Purchase Probability
```

---

# Step 1 — Import NumPy

```python
import numpy as np
```

---

# Step 2 — Create Dataset

আমরা synthetic dataset তৈরি করবো।

```python
np.random.seed(42)


X = np.random.randn(
    500,
    2
)
```

Shape:

```python
print(X.shape)
```

Output:

```
(500,2)
```

মানে:

```
500 samples

2 features
```

---

Create label:

Rule:

যদি x1+x2 > 0 হয়:

```
1
```

না হলে:

```
0
```

---

```python
y = (
    X[:,0] + X[:,1] > 0
).astype(int)
```

Check:

```python
print(y[:10])
```

---

# Step 3 — Normalize Dataset

Neural Network scaling পছন্দ করে।

Formula:

```
x' = (x-mean)/std
```

---

```python
mean = X.mean(axis=0)

std = X.std(axis=0)


X = (
    X-mean
)/std
```

---

# Step 4 — Train/Test Split

80% training:

20% testing

Shuffle:

```python
indices=np.random.permutation(
    len(X)
)


X=X[indices]

y=y[indices]
```

---

Split:

```python
split=int(
    len(X)*0.8
)


X_train=X[:split]

X_test=X[split:]


y_train=y[:split]

y_test=y[split:]
```

---

# Step 5 — Design Neural Network

Architecture:

```
Input

2 neurons

↓

Hidden Layer

4 neurons

↓

Output

1 neuron
```

---

Shape:

First weight:

```
(2,4)
```

Second:

```
(4,1)
```

---

# Step 6 — Initialize Parameters

```python
np.random.seed(1)


W1=np.random.randn(
    2,
    4
)*0.01


b1=np.zeros(
    (1,4)
)



W2=np.random.randn(
    4,
    1
)*0.01


b2=np.zeros(
    (1,1)
)
```

---

# Step 7 — Activation Functions

## ReLU

```python
def relu(x):

    return np.maximum(
        0,
        x
    )
```

---

## ReLU Derivative

Backpropagation-এর জন্য:

```python
def relu_derivative(x):

    return x>0
```

---

## Sigmoid

```python
def sigmoid(x):

    return (
        1/
        (1+np.exp(-x))
    )
```

---

# Step 8 — Forward Propagation

Function:

```python
def forward(X):

    Z1 = X @ W1 + b1


    A1 = relu(Z1)


    Z2 = A1 @ W2 + b2


    A2 = sigmoid(Z2)


    return Z1,A1,Z2,A2
```

---

Test:

```python
Z1,A1,Z2,A2 = forward(
    X_train
)


print(A2.shape)
```

Output:

```
(400,1)
```

---

# Step 9 — Loss Function

Binary Cross Entropy:

```python
def loss_function(
    y,
    prediction
):

    y=y.reshape(-1,1)


    loss = -(
        y*np.log(prediction)
        +
        (1-y)
        *
        np.log(1-prediction)
    )


    return np.mean(loss)
```

---

Calculate:

```python
loss=loss_function(
    y_train,
    A2
)


print(loss)
```

---

# Step 10 — Backpropagation

এখন সবচেয়ে important part।

Flow:

```
Loss

 ↓

Gradient

 ↓

Weight update
```

---

Derivative output:

```python
def backward(
    X,
    y,
    Z1,
    A1,
    A2
):

    m=len(X)


    y=y.reshape(-1,1)
```

---

Output layer gradient:

```python
    dZ2 = A2-y
```

---

Weight gradient:

```python
    dW2 = (
        A1.T @ dZ2
    ) / m


    db2 = (
        np.sum(
            dZ2,
            axis=0,
            keepdims=True
        )
    ) / m
```

---

Hidden layer:

```python
    dA1 = dZ2 @ W2.T


    dZ1 = (
        dA1 *
        relu_derivative(Z1)
    )
```

---

First layer:

```python
    dW1 = (
        X.T @ dZ1
    ) / m


    db1 = (
        np.sum(
            dZ1,
            axis=0,
            keepdims=True
        )
    ) / m
```

---

Return:

```python
    return (
        dW1,
        db1,
        dW2,
        db2
    )
```

---

# Step 11 — Training Loop

Learning rate:

```python
learning_rate=0.1
```

Epoch:

```python
epochs=1000
```

---

Training:

```python
for epoch in range(epochs):


    Z1,A1,Z2,A2 = forward(
        X_train
    )


    loss=loss_function(
        y_train,
        A2
    )


    dW1,db1,dW2,db2 = backward(
        X_train,
        y_train,
        Z1,
        A1,
        A2
    )


    W1 -= learning_rate*dW1

    b1 -= learning_rate*db1


    W2 -= learning_rate*dW2

    b2 -= learning_rate*db2


    if epoch%100==0:

        print(
            epoch,
            loss
        )
```

---

Expected:

```
0 0.69

100 0.40

500 0.10

900 0.05
```

Loss কমবে।

---

# Step 12 — Prediction Function

```python
def predict(X):

    _,_,_,output = forward(X)


    prediction = (
        output>0.5
    ).astype(int)


    return prediction
```

---

# Step 13 — Evaluate Model

Prediction:

```python
y_pred=predict(
    X_test
)
```

---

Accuracy:

```python
accuracy=np.mean(
    y_pred.reshape(-1)
    ==
    y_test
)


print(
accuracy
)
```

Example:

```
0.96
```

---

# Complete Neural Network Flow

```text
Input Data

↓

Normalize

↓

XW1+b1

↓

ReLU

↓

XW2+b2

↓

Sigmoid

↓

Prediction

↓

Loss

↓

Backward

↓

Gradient

↓

Update Weight

↓

Repeat
```

---

# NumPy Concepts Used

এই project-এ তুমি ব্যবহার করেছো:

| Concept               | Use                   |
| --------------------- | --------------------- |
| Array                 | Dataset               |
| Matrix multiplication | Neural network        |
| Broadcasting          | Bias                  |
| Random                | Weight initialization |
| Mean                  | Loss                  |
| Transpose             | Gradient              |
| Vectorization         | Speed                 |
| Slicing               | Dataset split         |

---

# TensorFlow/PyTorch এর সাথে Relation

আমরা লিখেছি:

```python
X @ W + b
```

PyTorch:

```python
torch.matmul(X,W)+b
```

TensorFlow:

```python
tf.matmul(X,W)+b
```

---

Activation:

NumPy:

```python
np.maximum(0,x)
```

PyTorch:

```python
torch.relu(x)
```

Concept একই।

---

# Advanced Practice

## Project Upgrade 1

Dataset:

```
10000 samples
10 features
```

Network:

```
10

↓

64

↓

32

↓

1
```

---

## Project Upgrade 2

Add:

* Multiple hidden layers
* Different activation
* Learning rate decay
* Mini batch training

---

## Project Upgrade 3

Implement:

* Softmax
* Multi-class classification
* Cross entropy loss

---

# Interview Questions

### 1. Why backpropagation?

Weight কত পরিবর্তন করতে হবে বের করার জন্য।

---

### 2. Why transpose in gradient?

Matrix dimension match করার জন্য।

---

### 3. Why initialize weights small?

Large value হলে gradient সমস্যা হতে পারে।

---

### 4. Why vectorization?

Python loop-এর থেকে অনেক fast।

---

### 5. NumPy কেন ML-এর foundation?

কারণ:

* Matrix computation
* Linear algebra
* Numerical operations

---

# 🎓 NumPy Course Completion

তুমি এখন শিখেছো:

## Beginner

✅ Array
✅ Shape
✅ Indexing
✅ Slicing

## Intermediate

✅ Broadcasting
✅ Statistics
✅ Linear Algebra
✅ Random

## Advanced

✅ Memory Optimization
✅ File Handling
✅ Data Pipeline
✅ Feature Engineering

## ML Engineer Level

✅ Neural Network Forward Pass
✅ Backpropagation
✅ Gradient Descent
✅ Training Loop

---

## Next Recommended Track

এখন তোমার জন্য সবচেয়ে logical next step:

**Pandas Mastery Course (Data Engineering + ML জন্য)**

তারপর:

```
NumPy
  ↓
Pandas
  ↓
Matplotlib
  ↓
Scikit-Learn
  ↓
PyTorch
  ↓
ML Engineer
```

NumPy foundation এখন strong হবে।
হ্যাঁ, **কিছু ক্ষেত্রে DRF (Django REST Framework) project-এ NumPy ব্যবহার করা হয়**, কিন্তু সাধারণ CRUD API বানানোর সময় সাধারণত NumPy লাগে না।

একজন Backend Developer হিসেবে তোমার DRF project-এ NumPy কোথায় লাগে সেটা বুঝি।

---

# 1. Normal DRF API তে NumPy লাগে না

ধরো তুমি E-commerce API বানাচ্ছো:

```
products/
orders/
users/
payments/
cart/
```

Example:

```python
class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

এখানে:

* Django ORM
* PostgreSQL
* Serializer
* Validation

এসব লাগে।

NumPy লাগে না।

---

# 2. তাহলে NumPy কোথায় ব্যবহার হয় DRF-এ?

মূলত **Data Processing এবং AI/ML Feature-এর জন্য।**

Architecture:

```
React
 |
 |
DRF API
 |
 |
AI Service
 |
 |
NumPy
 |
 |
ML Model
```

---

# Example 1 — AI Prediction API

ধরো তুমি CCTV anomaly detection system বানাচ্ছো।

Frontend:

```
Upload Video
```

DRF:

```
POST /api/detect/
```

Backend:

```python
class DetectionAPIView(APIView):

    def post(self, request):

        image = request.FILES["image"]

        result = model.predict(image)

        return Response({
            "prediction": result
        })
```

ভিতরে:

```python
image_array = np.array(image)
```

তারপর:

```
Image

↓

NumPy Array

↓

Model

↓

Prediction
```

---

# Example 2 — Data Analytics API

ধরো Admin Dashboard:

API:

```
GET /api/sales/report/
```

Response:

```json
{
 "total_sales":500000,
 "average_order":2500,
 "top_customer":101
}
```

Backend:

```python
import numpy as np


sales=np.array([
1000,
2000,
3000
])


total=np.sum(sales)

average=np.mean(sales)
```

তারপর:

```python
return Response({
    "total":total,
    "average":average
})
```

---

# Example 3 — Recommendation System

E-commerce:

```
GET /api/recommendations/
```

তোমার কাছে:

```
User Vector

[0.2,0.5,0.8]
```

Product Vector:

```
[0.1,0.4,0.9]
```

Similarity:

```python
np.dot(
    user_vector,
    product_vector
)
```

তারপর:

```
Recommended Products
```

---

# Example 4 — Image Processing API

ধরো:

```
POST /api/image/process/
```

Image:

```python
from PIL import Image
import numpy as np


img=Image.open(
"test.jpg"
)


arr=np.array(img)
```

এখন:

```python
arr.shape
```

Output:

```
(224,224,3)
```

CNN model এ পাঠাবে।

---

# Example 5 — ML Model Serving

Real production architecture:

```
Django DRF
       |
       |
       |
ML Service
       |
       |
NumPy
       |
       |
PyTorch/TensorFlow
```

Example:

DRF:

```python
prediction = predictor.predict(
    data
)
```

Predictor:

```python
def predict(data):

    x=np.array(data)

    result=model(x)

    return result
```

---

# DRF Project যেখানে NumPy লাগতে পারে

| Project Type          | NumPy Use |
| --------------------- | --------- |
| E-commerce CRUD       | ❌ No      |
| Blog API              | ❌ No      |
| Authentication API    | ❌ No      |
| Payment API           | ❌ No      |
| Analytics Dashboard   | ✅ Yes     |
| Recommendation System | ✅ Yes     |
| Image Processing      | ✅ Yes     |
| Computer Vision       | ✅ Yes     |
| ML Prediction API     | ✅ Yes     |
| Data Pipeline         | ✅ Yes     |

---

# তোমার ক্ষেত্রে (তুমি যেহেতু DRF + ML শিখছো)

তোমার project:

```
AI CCTV System
```

এখানে NumPy অবশ্যই লাগবে।

Flow:

```
Camera Stream

↓

OpenCV

↓

NumPy Array

↓

CNN/LSTM Model

↓

Prediction

↓

Django REST API

↓

React Dashboard
```

---

# একজন ML Engineer + Backend Engineer হিসেবে তোমার Stack হবে:

```
Python
 |
 ├── Django
 ├── DRF
 |
 ├── NumPy
 ├── Pandas
 |
 ├── Scikit-learn
 |
 ├── PyTorch
 |
 └── TensorFlow
```

---

তাই তোমার DRF mastery-এর জন্য NumPy দিয়ে CRUD API শেখার দরকার নেই।
বরং তোমার জন্য সবচেয়ে useful হবে:

**DRF + NumPy + OpenCV + PyTorch + Celery দিয়ে AI API build করা।**

পরের ধাপে আমি তোমাকে দেখাতে পারি:

**"DRF project এ PyTorch model + NumPy inference service কীভাবে integrate করতে হয় (production architecture + code)"**.
হ্যাঁ, **API-এর operation করার জন্য NumPy ব্যবহার করা যায়**, কিন্তু সব ধরনের API operation-এর জন্য না।

DRF API-তে সাধারণ CRUD operation:

* Create
* Read
* Update
* Delete

এসবের জন্য NumPy ব্যবহার করা হয় না।

কারণ Django ORM database operation খুব ভালোভাবে handle করে।

Example:

```python
product = Product.objects.create(
    name="Laptop",
    price=50000
)
```

এখানে NumPy দরকার নেই।

---

কিন্তু API-এর ভিতরে যদি **numerical computation** থাকে, তখন NumPy ব্যবহার করা যায়।

---

## Example 1: Statistics API

ধরো:

```
GET /api/sales/statistics/
```

Response:

```json
{
    "total_sales": 500000,
    "average_sales": 2500,
    "max_sale": 10000
}
```

Backend:

```python
import numpy as np
from rest_framework.views import APIView
from rest_framework.response import Response


class SalesStatisticsAPIView(APIView):

    def get(self, request):

        sales = np.array([
            1000,
            2000,
            3000,
            5000
        ])

        data = {
            "total": np.sum(sales),
            "average": np.mean(sales),
            "maximum": np.max(sales)
        }

        return Response(data)
```

এখানে NumPy useful।

---

## Example 2: Product Recommendation API

API:

```
GET /api/products/recommend/
```

ধরো user vector:

```python
user = np.array([
    0.2,
    0.5,
    0.8
])
```

Product vector:

```python
product = np.array([
    0.3,
    0.4,
    0.9
])
```

Similarity:

```python
score = np.dot(
    user,
    product
)
```

তারপর:

```json
{
 "product_id":10,
 "score":0.89
}
```

---

## Example 3: Data Transformation API

ধরো API তে data আসলো:

```json
{
 "prices":[100,200,300]
}
```

DRF:

```python
prices = request.data["prices"]

arr = np.array(prices)

normalized = (
    arr-arr.min()
) / (
    arr.max()-arr.min()
)
```

Response:

```json
{
 "normalized":[0,0.5,1]
}
```

---

## Example 4: Image Processing API

Request:

```
POST /api/image/analyze/
```

Image:

```
jpg/png
```

Convert:

```python
image_array = np.array(image)
```

তারপর:

```
NumPy Array
       |
       |
CNN Model
       |
       |
Prediction
```

---

## Example 5: ML Prediction API

DRF:

```python
class PredictAPIView(APIView):

    def post(self, request):

        features = request.data["features"]

        x = np.array(features)

        prediction = model.predict(x)

        return Response({
            "result": prediction
        })
```

---

# কোথায় NumPy ব্যবহার করবে না

এই ধরনের API:

```
POST /products/
GET /products/
PUT /products/1/
DELETE /products/1/

POST /orders/
POST /login/
POST /register/
```

এগুলোতে:

* Django ORM
* Serializer
* Validation

ব্যবহার করবে।

---

# Real Production Architecture

বড় project-এ সাধারণত:

```
Client
  |
  |
DRF API
  |
  |
Business Logic
  |
  |
----------------
|              |
Database       ML Service
               |
               |
             NumPy
               |
             PyTorch
```

---

তোমার মতো **DRF + ML Engineer track** হলে NumPy সবচেয়ে বেশি কাজে লাগবে:

1. ML prediction API
2. Recommendation API
3. Analytics API
4. Computer Vision API
5. Data processing pipeline

কিন্তু **normal e-commerce API operation-এর জন্য NumPy শেখা দরকার নেই**।
