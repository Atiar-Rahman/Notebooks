তোমার লক্ষ্য যেহেতু **Data Engineer → ML Engineer**, তাই আমি NumPy শুধু syntax হিসেবে না, **production ML/Data Engineering mindset** দিয়ে শেখাব।

এই কোর্স শেষ করলে তুমি সহজেই Pandas, Scikit-learn, TensorFlow, PyTorch, OpenCV বুঝতে পারবে। কারণ এগুলোর ভিত্তি হচ্ছে NumPy।

---

# NumPy Mastery Course (Zero → Advanced)

## Module 1: NumPy Fundamentals (Foundation)

### Lesson 1

* Why NumPy?
* Python List vs NumPy Array
* ndarray কী?
* Why ndarray এত fast?

### Lesson 2

Creating Arrays

```python
import numpy as np

a = np.array([1,2,3])

b = np.zeros((3,4))

c = np.ones((5,5))

d = np.empty((4,4))

e = np.eye(5)

f = np.arange(10)

g = np.linspace(0,100,11)
```

---

### Lesson 3

Array Attributes

```python
a.shape

a.ndim

a.size

a.dtype

a.itemsize

a.nbytes
```

---

### Lesson 4

Data Types

```
int8
int16
int32
int64

float16
float32
float64

bool

str

object
```

Changing dtype

```python
a.astype(np.float32)
```

---

# Module 2 : Array Operations

### Lesson 5

Arithmetic

```python
a+b

a-b

a*b

a/2

a**2

np.sqrt(a)

np.exp(a)

np.log(a)
```

---

### Lesson 6

Comparison

```python
a>5

a<10

a==3

a!=2
```

---

### Lesson 7

Logical

```python
np.logical_and()

np.logical_or()

np.logical_not()
```

---

### Lesson 8

Aggregation

```python
sum()

mean()

median()

max()

min()

std()

var()

prod()
```

---

# Module 3 : Indexing

### Lesson 9

Basic Indexing

```python
a[0]

a[-1]

a[2:8]
```

---

### Lesson 10

2D Indexing

```python
arr[0,1]

arr[:,1]

arr[1,:]

arr[1:3,2:]
```

---

### Lesson 11

Boolean Indexing

```python
a[a>5]
```

---

### Lesson 12

Fancy Indexing

```python
a[[1,3,5]]
```

---

# Module 4 : Reshaping

### Lesson 13

```python
reshape()

flatten()

ravel()

resize()
```

---

### Lesson 14

Transpose

```python
.T

transpose()
```

---

### Lesson 15

Expand Dimensions

```python
expand_dims()

squeeze()

newaxis
```

---

# Module 5 : Broadcasting

এটা NumPy-এর সবচেয়ে গুরুত্বপূর্ণ টপিক।

```
(3,1)

+

(1,4)

↓

(3,4)
```

শিখবে

* Broadcasting Rules
* Memory Saving
* Performance

---

# Module 6 : Matrix

### Matrix Multiplication

```python
@

dot()

matmul()
```

---

### Inverse

```python
np.linalg.inv()
```

---

### Determinant

```python
np.linalg.det()
```

---

### Eigen Value

```python
np.linalg.eig()
```

---

### SVD

```python
np.linalg.svd()
```

---

# Module 7 : Random

```python
rand()

randn()

randint()

choice()

permutation()

shuffle()

seed()
```

---

# Module 8 : Statistics

```python
mean

median

percentile

quantile

corrcoef

cov
```

---

# Module 9 : Sorting

```python
sort

argsort

lexsort

unique
```

---

# Module 10 : Searching

```python
where

argmax

argmin

nonzero
```

---

# Module 11 : Joining

```python
concatenate

stack

hstack

vstack

dstack
```

---

# Module 12 : Splitting

```python
split

vsplit

hsplit
```

---

# Module 13 : File Handling

```python
save

load

savez

savetxt

loadtxt
```

---

# Module 14 : Performance

Timing

```python
time

timeit
```

Memory

```python
copy()

view()
```

---

Vectorization

Python Loop

↓

NumPy Vectorization

↓

100x Faster

---

# Module 15 : Advanced NumPy

Views vs Copy

Stride

Memory Layout

Contiguous Array

C order

Fortran order

Buffer

Broadcast Internals

---

# Module 16 : Linear Algebra

Matrix

Rank

Trace

Norm

QR

LU

Cholesky

Pseudo Inverse

Least Squares

---

# Module 17 : Real Data Analysis

CSV

Cleaning

Normalization

Standardization

One Hot Encoding

Missing Values

---

# Module 18 : Image Processing

Images as Arrays

RGB

Grayscale

Cropping

Rotation

Flipping

Masking

Filtering

---

# Module 19 : Machine Learning

Feature Scaling

Normalization

Mini Batch

Gradient Descent

Loss Calculation

Distance

Cosine Similarity

---

# Module 20 : Interview Questions

৫০+ NumPy Interview Questions

সহ

Coding Problems

---

# Module 21 : Production Level

Memory Optimization

Huge Arrays

Chunk Processing

np.memmap

Performance Tricks

Best Practices

---

# Module 22 : Final Project

Project-1

NumPy Data Analysis Library

---

Project-2

Mini Image Processing Library

---

Project-3

Linear Regression from Scratch

---

Project-4

Neural Network Forward Pass

Only NumPy

---

Project-5

KNN From Scratch

---

Project-6

PCA From Scratch

---

Project-7

Logistic Regression From Scratch

---

Project-8

Mini Pandas Clone

---

# Daily Study Plan (2–2.5 ঘণ্টা)

| Week   | Topics                                                                                        |
| ------ | --------------------------------------------------------------------------------------------- |
| Week 1 | Modules 1–4 (Fundamentals, Arrays, Indexing, Reshaping)                                       |
| Week 2 | Modules 5–8 (Broadcasting, Matrix, Random, Statistics)                                        |
| Week 3 | Modules 9–15 (Sorting, Searching, Joining, Splitting, Files, Performance, Advanced)           |
| Week 4 | Modules 16–22 (Linear Algebra, Data Analysis, ML, Image Processing, Projects, Interview Prep) |

## কীভাবে আমরা এগোব

তোমার জন্য আমি এটাকে **একটি বিশ্ববিদ্যালয়-লেভেলের কোর্স** হিসেবে পড়াব। প্রতিটি লেসনে থাকবে:

1. তত্ত্ব (কেন এই ধারণা দরকার)
2. Visual explanation (মেন্টাল মডেল)
3. Syntax
4. প্রতিটি লাইনের কোড ব্যাখ্যা
5. Common mistakes
6. Interview questions
7. Practice problems (Easy → Medium → Hard)
8. Mini project
9. Assignment
10. Data Engineer ও ML Engineer-এ বাস্তব ব্যবহার

এইভাবে শেষ করলে তুমি শুধু NumPy ব্যবহার করতে নয়, **NumPy দিয়ে সমস্যা সমাধান ও production-grade কোড লিখতে** পারবে।
