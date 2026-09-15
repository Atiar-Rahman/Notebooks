
# ✅ **Array Implementation in Python**

Python does **not** have built-in low-level arrays like C or Java.  
But you can implement arrays in **three ways**:

---

# ⭐ **1. Using List (Most Common in Python)**

Python lists behave like dynamic arrays.

### ✔ Create Array

```python
arr = [10, 20, 30, 40, 50]
print(arr)
```

### ✔ Access Elements

```python
print(arr[0])   # first element
print(arr[-1])  # last element
```

### ✔ Insert Element

```python
arr.append(60)           # add at end
arr.insert(2, 25)        # insert at index 2
print(arr)
```

### ✔ Update Element

```python
arr[1] = 200
```

### ✔ Delete Element

```python
arr.remove(30)      # removes value 30
del arr[3]          # removes index 3
print(arr)
```

---

# ⭐ **2. Using `array` Module (Fixed Type Array)**

This behaves more like C-style arrays, storing elements of the same type.

### ✔ Create Array

```python
import array

arr = array.array('i', [10, 20, 30, 40])
print(arr)
```

`'i'` means **signed int**.

### Type Codes

|Type code|Data type|
|---|---|
|`'i'`|signed int|
|`'f'`|float|
|`'d'`|double|
|`'b'`|signed char|

### ✔ Insert

```python
arr.append(50)
arr.insert(1, 15)
```

### ✔ Remove

```python
arr.remove(30)
```

### ✔ Access

```python
print(arr[2])
```

---

# ⭐ **3. Manual Array Implementation (Low-Level Dynamic Array)**

This mimics how Python lists work internally.

### ✔ Code

```python
import ctypes

class DynamicArray:
    def __init__(self):
        self.n = 0              # actual number of elements
        self.capacity = 1       # initial capacity
        self.arr = self.make_array(self.capacity)

    def make_array(self, capacity):
        return (capacity * ctypes.py_object)()

    def append(self, item):
        if self.n == self.capacity:
            self.resize(2 * self.capacity)   # double capacity
        self.arr[self.n] = item
        self.n += 1

    def resize(self, new_capacity):
        new_arr = self.make_array(new_capacity)
        for i in range(self.n):
            new_arr[i] = self.arr[i]
        self.arr = new_arr
        self.capacity = new_capacity

    def __getitem__(self, index):
        if 0 <= index < self.n:
            return self.arr[index]
        raise IndexError("Index out of bounds")

# Usage
obj = DynamicArray()
obj.append(10)
obj.append(20)
obj.append(30)

print(obj[0])
print(obj[1])
print("Capacity:", obj.capacity)
```

---

# 🎯 Summary Table

|Method|Type|Features|
|---|---|---|
|List|Dynamic|Easiest, flexible, default in Python|
|`array` module|Fixed type|Faster, uses less memory|
|Manual (ctypes)|Low-level|Teaches internal array mechanism|

---


---

# 🚀 **ALL ARRAY OPERATIONS IN PYTHON**

---

# ✅ 1. **Create Array**

```python
arr = [10, 20, 30, 40, 50]
```

---

# ✅ 2. **Access Elements**

```python
print(arr[0])     # first element
print(arr[-1])    # last element
```

---

# ✅ 3. **Traverse Array**

```python
for x in arr:
    print(x)
```

---

# ✅ 4. **Insert Element**

### ➤ Add at End

```python
arr.append(60)
```

### ➤ Add at Specific Index

```python
arr.insert(2, 25)   # insert 25 at index 2
```

### ➤ Add Multiple Elements

```python
arr.extend([70, 80])
```

---

# ✅ 5. **Update Element**

```python
arr[1] = 200   # update index 1
```

---

# ✅ 6. **Delete / Remove Element**

### ➤ Remove by Value

```python
arr.remove(30)    # removes first occurrence of 30
```

### ➤ Remove by Index

```python
del arr[2]        # removes index 2
```

### ➤ Remove Last Element

```python
arr.pop()         # default removes last
```

### ➤ Remove Specific Index

```python
arr.pop(1)        # removes index 1
```

### ➤ Clear All Elements

```python
arr.clear()
```

---

# ✅ 7. **Search Elements**

### ➤ Linear Search

```python
arr = [10, 20, 30, 40, 50]
target = 30

for i in range(len(arr)):
    if arr[i] == target:
        print("Found at index", i)
```

### ➤ Check if Exists

```python
print(30 in arr)  # True / False
```

### ➤ Get Index of Value

```python
print(arr.index(40))   # returns index
```

---

# ✅ 8. **Length of Array**

```python
print(len(arr))
```

---

# ✅ 9. **Reverse Array**

### ➤ Method 1

```python
arr.reverse()
```

### ➤ Method 2 (Slicing)

```python
rev = arr[::-1]
```

---

# ✅ 10. **Sort Array**

### ➤ Ascending

```python
arr.sort()
```

### ➤ Descending

```python
arr.sort(reverse=True)
```

### ➤ New Sorted Array

```python
new = sorted(arr)
```

---

# ✅ 11. **Slicing**

```python
arr = [10, 20, 30, 40, 50]

print(arr[1:4])    # [20, 30, 40]
print(arr[:3])     # first 3
print(arr[2:])     # from index 2 to end
```

---

# ✅ 12. **Concatenate Arrays**

```python
a = [1, 2]
b = [3, 4]

c = a + b
print(c)
```

---

# ✅ 13. **Copy Array**

### ➤ Shallow Copy

```python
new = arr.copy()
```

### ➤ Using Slicing

```python
new = arr[:]
```

---

# ✅ 14. **Min / Max / Sum**

```python
print(min(arr))
print(max(arr))
print(sum(arr))
```

---

# ✅ 15. **Count Occurrences**

```python
arr = [10, 20, 20, 30]
print(arr.count(20))   # 2 times
```

---

# ✅ 16. **Array to String**

```python
s = " ".join(map(str, arr))
```

---

---

# ✅ **1. Convert String → Array of Characters**

```python
s = "hello"
arr = list(s)
print(arr)
```

**Output:**

```
['h', 'e', 'l', 'l', 'o']
```

---

# ✅ **2. Convert String → Array of Words (Split by space)**

```python
s = "I love Python"
arr = s.split()
print(arr)
```

**Output:**

```
['I', 'love', 'Python']
```

---

# ✅ **3. Split by Custom Separator**

```python
s = "apple,banana,mango"
arr = s.split(",")
print(arr)
```

**Output:**

```
['apple', 'banana', 'mango']
```

---

# ✅ **4. Convert Numeric String → Array of Integers**

```python
s = "1 2 3 4 5"
arr = list(map(int, s.split()))
print(arr)
```

**Output:**

```
[1, 2, 3, 4, 5]
```

---

# ✅ **5. Convert Continuous Number String → Array of Digits**

```python
s = "12345"
arr = [int(ch) for ch in s]
print(arr)
```

**Output:**

```
[1, 2, 3, 4, 5]
```

---

# ✅ **6. Convert String → Byte Array**

```python
s = "hello"
arr = bytearray(s, 'utf-8')
print(arr)
```

---

# 🎯 Summary Table

|Goal|Code|
|---|---|
|Characters|`list(s)`|
|Words|`s.split()`|
|Custom split|`s.split(",")`|
|Numbers|`list(map(int, s.split()))`|
|Digits|`[int(ch) for ch in s]`|
|Bytes|`bytearray(s, 'utf-8')`|

---

---

# ⭐ **Multidimensional Array in Python (A to Z)**

In Python, multidimensional arrays are created using **nested lists** or **NumPy**.  
Since you didn't specify NumPy, I will explain both.

---

# 🟦 **1. 2D Array (Matrix) Using Python List**

---

## ✅ **Create a 2D Array**

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

---

## ✅ **Access Elements**

```python
print(matrix[0][1])   # row 0, col 1 → 2
print(matrix[2][2])   # → 9
```

---

## ✅ **Update Element**

```python
matrix[1][1] = 55
```

---

## ✅ **Traverse 2D Array**

```python
for row in matrix:
    for value in row:
        print(value, end=" ")
    print()
```

---

## ✅ **Insert Row**

```python
matrix.append([10, 11, 12])
```

---

## ✅ **Insert Element into Specific Row**

```python
matrix[1].append(99)
```

---

## ✅ **Delete Row**

```python
del matrix[0]   # delete first row
```

---

## ✅ **Delete Element**

```python
del matrix[1][2]   # delete element at row 1 col 2
```

---

## ✅ **Find Value in 2D Array**

```python
target = 5

for i in range(len(matrix)):
    for j in range(len(matrix[i])):
        if matrix[i][j] == target:
            print("Found at:", i, j)
```

---

# 🟦 **2. Create 2D Array With Fixed Size**

```python
rows = 3
cols = 4

matrix = [[0] * cols for _ in range(rows)]
print(matrix)
```

Output:

```
[[0, 0, 0, 0],
 [0, 0, 0, 0],
 [0, 0, 0, 0]]
```

---

# 🟦 **3. 3D Array (Cuboid)**

---

## ✅ **Create 3D Array**

```python
arr3D = [
    [
        [1, 2],
        [3, 4]
    ],
    [
        [5, 6],
        [7, 8]
    ]
]
```

---

## ✅ **Access 3D Element**

```python
print(arr3D[0][1][1])   # → 4
```

---

## ✅ **Update 3D Element**

```python
arr3D[1][0][1] = 66
```

---

## ✅ **Traverse 3D Array**

```python
for layer in arr3D:
    for row in layer:
        for value in row:
            print(value, end=" ")
        print()
    print("----")
```

---

# 🟦 **4. Multidimensional Array Using NumPy (Recommended)**

If you want faster operations, **NumPy** is better.

### ➤ Install NumPy

```
pip install numpy
```

### ✔ Create Array

```python
import numpy as np

arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

### ✔ Access

```python
print(arr[0, 1])   # 2
```

### ✔ Slice (Submatrix)

```python
print(arr[:, 1])   # second column
```

### ✔ Shape

```python
print(arr.shape)   # (2, 3)
```

---

# 🟩 Summary (Very Important)

|Type|Example|Description|
|---|---|---|
|2D array|`arr[r][c]`|matrix|
|3D array|`arr[x][y][z]`|cube|
|nested list|built-in|simple but slower|
|NumPy array|`np.array()`|faster, used in ML|

---
Here are the **MOST IMPORTANT matrix operations using ONLY Python lists** (no NumPy).  
Perfect for **DSA, coding interviews, problem solving**.

I will give **all operations A → Z**:

✔ Create matrix  
✔ Traverse  
✔ Access  
✔ Update  
✔ Row/column sum  
✔ Matrix addition  
✔ Matrix subtraction  
✔ Matrix multiplication  
✔ Matrix transpose  
✔ Identity matrix  
✔ Check symmetric matrix  
✔ Reverse rows/columns

Let's start!

---

# 🟥 **1. Create a Matrix (List of Lists)**

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```

---

# 🟧 **2. Traverse a Matrix**

```python
for row in matrix:
    for val in row:
        print(val, end=" ")
    print()
```

---

# 🟨 **3. Access Element**

```python
print(matrix[1][2])   # row 1, col 2 → 6
```

---

# 🟩 **4. Update Element**

```python
matrix[0][1] = 88   # replace 2 with 88
```

---

# 🟦 **5. Row Sum / Column Sum**

### ➤ Row Sum

```python
for row in matrix:
    print(sum(row))
```

### ➤ Column Sum

```python
cols = len(matrix[0])
for c in range(cols):
    s = 0
    for r in range(len(matrix)):
        s += matrix[r][c]
    print(s)
```

---

# 🟪 **6. Matrix Addition**

Two matrices must have same rows and columns.

```python
A = [[1, 2], [3, 4]]
B = [[5, 6], [7, 8]]

result = [[0, 0], [0, 0]]

for i in range(len(A)):
    for j in range(len(A[0])):
        result[i][j] = A[i][j] + B[i][j]

print(result)
```

---

# 🟫 **7. Matrix Subtraction**

```python
result = [[A[i][j] - B[i][j] for j in range(len(A[0]))] 
          for i in range(len(A))]
```

---

# ⬛ **8. Matrix Multiplication (VERY IMPORTANT)**

Formula:  
C[i][j] = sum(A[i][k] * B[k][j])

```python
A = [
    [1, 2, 3],
    [4, 5, 6]
]

B = [
    [7, 8],
    [9, 10],
    [11, 12]
]

# Result matrix should have rows of A and columns of B
result = [[0] * len(B[0]) for _ in range(len(A))]

for i in range(len(A)):          # A rows
    for j in range(len(B[0])):   # B columns
        for k in range(len(B)):  # columns of A or rows of B
            result[i][j] += A[i][k] * B[k][j]

print(result)
```

**Output**

```
[[58, 64],
 [139, 154]]
```

---

# 🟦 **9. Matrix Transpose (Swap rows & columns)**

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6]
]

transpose = [[0]*len(matrix) for _ in range(len(matrix[0]))]

for i in range(len(matrix)):
    for j in range(len(matrix[0])):
        transpose[j][i] = matrix[i][j]

print(transpose)
```

---

# 🟧 **10. Reverse Each Row**

```python
for row in matrix:
    row.reverse()
```

---

# 🟨 **11. Reverse Each Column**

```python
rows = len(matrix)
cols = len(matrix[0])

for c in range(cols):
    for r in range(rows // 2):
        matrix[r][c], matrix[rows - r - 1][c] = matrix[rows - r - 1][c], matrix[r][c]
```

---

# 🟩 **12. Identity Matrix (n×n)**

```python
n = 4
I = [[1 if i == j else 0 for j in range(n)] for i in range(n)]
print(I)
```

---

# 🟦 **13. Check Symmetric Matrix**

A matrix is symmetric if A == Aᵀ.

```python
def is_symmetric(mat):
    n = len(mat)
    for i in range(n):
        for j in range(n):
            if mat[i][j] != mat[j][i]:
                return False
    return True
```

---

# 🟪 **14. Diagonal Sum**

### Primary Diagonal

```python
s = 0
for i in range(len(matrix)):
    s += matrix[i][i]
```

### Secondary Diagonal

```python
n = len(matrix)
s = 0
for i in range(n):
    s += matrix[i][n - i - 1]
```

---

