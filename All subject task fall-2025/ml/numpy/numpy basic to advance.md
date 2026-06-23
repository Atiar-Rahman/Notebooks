
If you want to learn **NumPy from basic to advanced**, here is a structured roadmap:

## 1. NumPy Basics

### What is NumPy?

NumPy is a Python library for numerical computing. It provides fast **multidimensional arrays** and tools for mathematics, statistics, linear algebra, and more.

### Install

```bash
pip install numpy
```

### Import

```python
import numpy as np
```

---

## 2. Creating Arrays

### From Python lists

```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(a)
```

Output:

```
[1 2 3 4]
```

### 2D array

```python
matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(matrix)
```

---

## 3. Array Properties

```python
arr = np.array([[1,2,3],[4,5,6]])

print(arr.shape)   # dimensions
print(arr.size)    # number of elements
print(arr.ndim)    # number of axes
print(arr.dtype)   # data type
```

---

# 4. Creating Special Arrays

### Zeros

```python
np.zeros((3,3))
```

### Ones

```python
np.ones((2,4))
```

### Range

```python
np.arange(0,10,2)
```

Output:

```
[0 2 4 6 8]
```

### Evenly spaced values

```python
np.linspace(0,10,5)
```

Output:

```
[0.  2.5 5.  7.5 10.]
```

---

# 5. Indexing & Slicing

```python
a = np.array([10,20,30,40])

print(a[0])
print(a[-1])
print(a[1:3])
```

2D:

```python
m = np.array([
[1,2,3],
[4,5,6]
])

print(m[0,1])
```

Output:

```
2
```

---

# 6. Array Operations

### Arithmetic

```python
a = np.array([1,2,3])

print(a + 5)
print(a * 2)
```

Output:

```
[6 7 8]
[2 4 6]
```

### Between arrays

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

print(a+b)
print(a*b)
```

---

# 7. Useful Functions

```python
a = np.array([1,2,3,4,5])

np.sum(a)
np.mean(a)
np.max(a)
np.min(a)
np.std(a)
```

---

# 8. Reshaping

Change dimensions:

```python
a = np.arange(12)

b = a.reshape(3,4)

print(b)
```

Output:

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

---

# 9. Joining Arrays

### Concatenate

```python
a = np.array([1,2])
b = np.array([3,4])

np.concatenate([a,b])
```

Output:

```
[1 2 3 4]
```

---

# 10. Boolean Filtering

```python
a = np.array([10,20,30,40])

print(a[a>20])
```

Output:

```
[30 40]
```

---

# 11. Random Numbers

```python
np.random.rand(3,3)
```

Random integers:

```python
np.random.randint(1,100,5)
```

---

# 12. Copy vs View

Copy:

```python
a = np.array([1,2,3])

b = a.copy()

b[0]=100
```

View:

```python
b = a.view()
```

---

# Intermediate NumPy

## 13. Broadcasting

Example:

```python
a = np.array([1,2,3])

print(a + 10)
```

NumPy automatically expands:

```
[11 12 13]
```

---

## 14. Matrix Operations

Matrix multiplication:

```python
A = np.array([
[1,2],
[3,4]
])

B = np.array([
[5,6],
[7,8]
])

A @ B
```

---

## 15. Linear Algebra

```python
np.linalg.det(A)

np.linalg.inv(A)

np.linalg.eig(A)
```

---

## 16. Sorting

```python
a = np.array([5,2,9,1])

np.sort(a)
```

Output:

```
[1 2 5 9]
```

---

## 17. Searching

```python
a = np.array([10,20,30])

np.where(a>15)
```

---

# Advanced NumPy

## 18. Vectorization

Slow:

```python
result=[]

for i in range(100000):
    result.append(i*2)
```

Fast:

```python
a=np.arange(100000)

result=a*2
```

---

## 19. Structured Arrays

```python
data=np.array([
    ("John",20),
    ("Anna",25)
],
dtype=[
    ("name","U10"),
    ("age","i4")
])

print(data["age"])
```

---

## 20. Working with Axis

```python
a=np.array([
[1,2,3],
[4,5,6]
])

np.sum(a,axis=0)
```

Output:

```
[5 7 9]
```

Rows:

```python
np.sum(a,axis=1)
```

Output:

```
[6 15]
```

---

## 21. Saving & Loading

Save:

```python
np.save("data.npy",a)
```

Load:

```python
x=np.load("data.npy")
```

---

## 22. Memory Optimization

Specify datatype:

```python
a=np.array([1,2,3],dtype=np.int8)
```

---

## 23. Advanced Indexing

```python
a=np.array([10,20,30,40])

idx=[0,2]

print(a[idx])
```

Output:

```
[10 30]
```

---

## 24. Useful NumPy Skills for Data Science

Learn:

- Array manipulation
    
- Broadcasting
    
- Vectorization
    
- Linear algebra
    
- Statistics
    
- Random sampling
    
- File handling
    
- Performance optimization
    

Used with:

- Pandas
    
- Matplotlib
    
- Scikit-learn
    

---

A good learning order:

**Beginner**

1. Arrays
    
2. Indexing
    
3. Shapes
    
4. Math operations
    
5. Aggregations
    

**Intermediate**  
6. Broadcasting  
7. Reshaping  
8. Matrix operations  
9. Random  
10. Filtering

**Advanced**  
11. Vectorization  
12. Memory optimization  
13. Linear algebra  
14. Performance tuning  
15. NumPy internals

This roadmap is enough to reach a strong practical NumPy level for data science, AI, and machine learning.

-----
Let's go through these **NumPy skills for Data Science** in detail with examples.

---

# 1. Array Manipulation

Array manipulation means changing the **shape, size, order, or values** of arrays.

## Creating arrays

```python
import numpy as np

a = np.array([1,2,3,4,5])

print(a)
```

Output:

```
[1 2 3 4 5]
```

---

## Reshape

Change dimensions without changing data.

```python
a = np.arange(12)

b = a.reshape(3,4)

print(b)
```

Output:

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

Use case:

- ML datasets
    
- Image processing
    

Example:  
An image:

```
Height × Width × Channels
```

```python
image = np.zeros((128,128,3))
```

---

## Flatten

Convert multi-dimensional array into 1D.

```python
a = np.array([
[1,2],
[3,4]
])

b = a.flatten()

print(b)
```

Output:

```
[1 2 3 4]
```

---

## Transpose

Swap rows and columns.

```python
a=np.array([
[1,2,3],
[4,5,6]
])

print(a.T)
```

Output:

```
[[1 4]
 [2 5]
 [3 6]]
```

Used in:

- Matrix math
    
- Neural networks
    

---

## Stack Arrays

### Vertical stack

```python
a=np.array([1,2,3])
b=np.array([4,5,6])

np.vstack([a,b])
```

Output:

```
[[1 2 3]
 [4 5 6]]
```

---

# 2. Broadcasting

Broadcasting allows NumPy to perform operations between arrays of different shapes.

Example:

```python
a=np.array([1,2,3])

print(a+10)
```

Output:

```
[11 12 13]
```

NumPy expands:

```
[1 2 3]

+

[10 10 10]
```

---

## 2D Broadcasting

```python
A=np.array([
[1,2,3],
[4,5,6]
])

b=np.array([10,20,30])


print(A+b)
```

Output:

```
[[11 22 33]
 [14 25 36]]
```

Explanation:

```
A:

1 2 3
4 5 6


b:

10 20 30


result:

11 22 33
14 25 36
```

---

### Real data science example

Normalize data:

```python
data=np.array([
[10,20],
[30,40],
[50,60]
])

mean=data.mean(axis=0)

normalized=data-mean

print(normalized)
```

Output:

```
[[-20 -20]
 [  0   0]
 [ 20  20]]
```

---

# 3. Vectorization

Vectorization means avoiding Python loops and using NumPy operations.

## Slow way

```python
numbers=range(1000000)

result=[]

for x in numbers:
    result.append(x*2)
```

Problem:

- slow
    
- uses Python loop
    

---

## NumPy way

```python
a=np.arange(1000000)

result=a*2
```

Much faster.

Why?

NumPy uses optimized C code internally.

---

## Example: Temperature conversion

Loop:

```python
temps=[20,30,40]

fahrenheit=[]

for t in temps:
    fahrenheit.append(t*9/5+32)
```

Vectorized:

```python
temps=np.array([20,30,40])

fahrenheit=temps*9/5+32

print(fahrenheit)
```

Output:

```
[68. 86. 104.]
```

---

# 4. Linear Algebra

Used heavily in:

- Machine learning
    
- Deep learning
    
- Statistics
    

---

## Matrix multiplication

```python
A=np.array([
[1,2],
[3,4]
])


B=np.array([
[5,6],
[7,8]
])


C=A@B

print(C)
```

Output:

```
[[19 22]
 [43 50]]
```

Math:

```
1*5 + 2*7 = 19
```

---

## Dot product

```python
a=np.array([1,2,3])
b=np.array([4,5,6])

np.dot(a,b)
```

Output:

```
32
```

Because:

```
1*4 + 2*5 + 3*6
```

---

## Matrix inverse

```python
A=np.array([
[1,2],
[3,4]
])


np.linalg.inv(A)
```

---

## Eigenvalues

Important in:

- PCA
    
- Dimensionality reduction
    

```python
A=np.array([
[2,0],
[0,3]
])

values,vectors=np.linalg.eig(A)

print(values)
```

Output:

```
[2 3]
```

---

# 5. Statistics

NumPy provides statistical functions.

Example:

```python
data=np.array([10,20,30,40,50])
```

---

## Mean

Average:

```python
np.mean(data)
```

Output:

```
30
```

---

## Median

Middle value:

```python
np.median(data)
```

---

## Standard deviation

Measure spread:

```python
np.std(data)
```

---

## Variance

```python
np.var(data)
```

---

## Percentile

```python
np.percentile(data,50)
```

Output:

```
30
```

---

## Real ML example

Feature scaling:

```python
x=np.array([10,20,30,40])

scaled=(x-x.mean())/x.std()

print(scaled)
```

Output:

```
[-1.34 -0.44 0.44 1.34]
```

---

# 6. Random Sampling

Used for:

- simulations
    
- ML train/test split
    
- experiments
    

---

## Random number

```python
np.random.rand(3)
```

Example output:

```
[0.23 0.71 0.55]
```

---

## Random integers

```python
np.random.randint(
1,
100,
5
)
```

Example:

```
[23 67 91 12 45]
```

---

## Random matrix

```python
np.random.randn(3,3)
```

Creates normal distribution data.

---

## Shuffle data

```python
a=np.array([1,2,3,4,5])

np.random.shuffle(a)

print(a)

```

---

## Reproducibility

Set seed:

```python
np.random.seed(10)

print(np.random.rand(3))
```

Same output every time.

---

# 7. File Handling

Save and load data.

---

## Save NumPy file

```python
a=np.array([1,2,3,4])

np.save("numbers.npy",a)
```

---

## Load file

```python
data=np.load("numbers.npy")

print(data)
```

---

## CSV files

Save:

```python
data=np.array([
[1,2],
[3,4]
])


np.savetxt(
"data.csv",
data,
delimiter=","
)
```

---

Load:

```python
x=np.loadtxt(
"data.csv",
delimiter=","
)

print(x)
```

---

# 8. Performance Optimization

Making NumPy code faster.

---

## Avoid loops

Bad:

```python
result=[]

for i in range(1000000):
    result.append(i*2)
```

Good:

```python
a=np.arange(1000000)

result=a*2
```

---

## Use correct datatype

Large:

```python
a=np.array(
[1,2,3],
dtype=np.int64
)
```

Smaller:

```python
a=np.array(
[1,2,3],
dtype=np.int8
)
```

Uses less memory.

---

## Avoid unnecessary copies

Copy:

```python
a=np.array([1,2,3])

b=a.copy()
```

Memory:

```
a -> data
b -> new data
```

---

View:

```python
b=a.view()
```

Memory:

```
a
|
b
```

---

## Vectorized comparison

Slow:

```python
for x in a:
    if x>10:
        print(x)
```

Fast:

```python
a[a>10]
```

Example:

```python
a=np.array([5,15,20])

print(a[a>10])
```

Output:

```
[15 20]
```

---

# Data Science NumPy Workflow

Typical pipeline:

```
Load Data
    |
NumPy Array
    |
Clean Data
    |
Normalize
    |
Matrix Operations
    |
Statistics
    |
Machine Learning Model
```

---

Mastering these 8 areas gives you the NumPy foundation needed for:

- Pandas
    
- TensorFlow
    
- PyTorch
    
- Scikit-learn
    

for data science and AI.

