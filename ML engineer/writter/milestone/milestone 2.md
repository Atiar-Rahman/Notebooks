ঠিক আছে। তুমি যে **M02 — NumPy + Pandas** structure দিয়েছো, সেটাকেই ধরে এবার **একদম complete syllabus** হিসেবে সাজাচ্ছি। শুধু তোমার bullet point-গুলো explain করব না—প্রতিটি topic-এর ভিতরের গুরুত্বপূর্ণ subtopic-ও cover করব, যাতে পরে AI/ML/Data Analysis project করতে গিয়ে foundation gap না থাকে।

# 🟢 M02 — NumPy + Pandas Complete Mastery

## 🎯 Milestone Goal

এই milestone শেষে তুমি পারবে:

```text
Raw Dataset
     ↓
NumPy
     ↓
Numerical Processing
     ↓
Pandas
     ↓
Data Cleaning
     ↓
Data Analysis
     ↓
Visualization-ready Dataset
     ↓
ML / AI Model
```

---

# 📚 Complete M02 Roadmap

## 🔵 Part A — NumPy

```text
M02.01 NumPy Introduction
M02.02 ndarray
M02.03 NumPy Data Types
M02.04 Shape
M02.05 Dimensions / ndim
M02.06 Size
M02.07 Axis
M02.08 Indexing
M02.09 Slicing
M02.10 Reshaping
M02.11 Flatten / Ravel
M02.12 Transpose
M02.13 Concatenation
M02.14 Stacking
M02.15 Splitting
M02.16 Broadcasting
M02.17 Vectorization
M02.18 Mathematical Operations
M02.19 Statistical Operations
M02.20 Matrix Operations
M02.21 Linear Algebra
M02.22 Random Module
M02.23 Boolean Masking
M02.24 Conditional Operations
M02.25 Copy vs View
M02.26 Sorting / Searching
M02.27 NaN / Infinity
M02.28 File I/O
M02.29 Performance
M02.30 NumPy Mini Practice
```

---

# 🟠 Part B — Pandas

```text
M02.31 Pandas Introduction
M02.32 Series
M02.33 DataFrame
M02.34 Index
M02.35 Columns
M02.36 Data Types
M02.37 CSV
M02.38 Excel
M02.39 JSON
M02.40 Data Inspection
M02.41 Selecting Columns
M02.42 loc
M02.43 iloc
M02.44 Filtering
M02.45 Multiple Conditions
M02.46 Sorting
M02.47 Adding / Removing Columns
M02.48 Rename
M02.49 Missing Data
M02.50 Duplicate Data
M02.51 Data Type Conversion
M02.52 String Processing
M02.53 Apply / Map
M02.54 GroupBy
M02.55 Aggregation
M02.56 Merge
M02.57 Join
M02.58 Concat
M02.59 Pivot / Pivot Table
M02.60 Reshape
M02.61 DateTime
M02.62 Categorical Data
M02.63 Query
M02.64 Sampling
M02.65 Data Cleaning
M02.66 Outlier Basics
M02.67 Memory Optimization
M02.68 Export
M02.69 Pandas + NumPy
M02.70 Pandas Performance
```

---

# 🟣 Part C — Mini Project

```text
M02.71 Text Dataset Analyzer
```

Project-এর ভিতরে:

```text
CSV / Excel
     ↓
Load
     ↓
Inspect
     ↓
Clean
     ↓
Missing Values
     ↓
Duplicates
     ↓
Text Processing
     ↓
Statistics
     ↓
GroupBy
     ↓
Analysis
     ↓
Export
```

এখন প্রতিটি topic বিস্তারিতভাবে শুরু করি।

---

# 🔵 M02.01 — NumPy Introduction

**NumPy = Numerical Python**

Python-এর normal list দিয়ে numerical calculation করা যায়, কিন্তু large-scale numerical computation-এর জন্য NumPy অনেক বেশি efficient।

Install:

```bash
pip install numpy
```

Import:

```python
import numpy as np
```

---

# NumPy কেন?

Python list:

```python
numbers = [1, 2, 3, 4]
```

NumPy:

```python
numbers = np.array([1, 2, 3, 4])
```

NumPy মূলত কাজ করে:

* numerical computation
* arrays
* matrices
* statistics
* linear algebra
* scientific computing
* ML preprocessing
* image processing

AI/ML-এ:

```text
Dataset
   ↓
NumPy Array
   ↓
Numerical Processing
   ↓
ML Model
```

---

# 🔵 M02.02 — ndarray

NumPy-এর প্রধান data structure হলো:

**ndarray = N-dimensional array**

```python
import numpy as np

arr = np.array([1, 2, 3, 4])

print(arr)
print(type(arr))
```

Output:

```text
[1 2 3 4]

<class 'numpy.ndarray'>
```

---

# 1D Array

```python
arr = np.array([1, 2, 3])
```

```text
[1 2 3]
```

---

# 2D Array

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

Structure:

```text
1 2 3
4 5 6
```

---

# 3D Array

```python
arr = np.array([
    [
        [1, 2],
        [3, 4]
    ],
    [
        [5, 6],
        [7, 8]
    ]
])
```

AI image data-তে এমন structure দেখা যায়।

---

# 🔵 M02.03 — NumPy Data Types

```python
arr = np.array([1, 2, 3])

print(arr.dtype)
```

Possible:

```text
int64
```

Float:

```python
arr = np.array([1.2, 2.5, 3.7])

print(arr.dtype)
```

---

# নির্দিষ্ট dtype

```python
arr = np.array(
    [1, 2, 3],
    dtype=np.float32
)
```

AI/ML-এ `float32` খুব common।

আর GPU/large model-এর ক্ষেত্রে পরে `float16`, `bfloat16` ইত্যাদি দেখতে পাবে।

---

# 🔵 M02.04 — Shape

`shape` বলে array-এর structure।

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.shape)
```

Output:

```text
(2, 3)
```

মানে:

```text
2 rows
3 columns
```

---

# Image Example

যদি image:

```text
64 × 64
```

তাহলে:

```python
image.shape
```

হতে পারে:

```text
(64, 64)
```

RGB image:

```text
(64, 64, 3)
```

Video:

```text
(frames, height, width, channels)
```

যেমন:

```text
(16, 64, 64, 3)
```

এটা তোমার আগের video/AI কাজেও সরাসরি useful।

---

# 🔵 M02.05 — `ndim`

```python
arr.ndim
```

Example:

```python
arr = np.array([1, 2, 3])

print(arr.ndim)
```

Output:

```text
1
```

2D:

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

print(arr.ndim)
```

Output:

```text
2
```

---

# 🔵 M02.06 — Size

```python
arr.size
```

Example:

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.size)
```

Output:

```text
6
```

---

# তিনটি difference মনে রাখবে

```text
shape → structure
ndim  → number of dimensions
size  → total elements
```

---

# 🔵 M02.07 — Axis

Axis NumPy-এর সবচেয়ে important conceptগুলোর একটি।

Array:

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
```

Structure:

```text
        columns
       0   1   2
     ┌───────────
row 0│ 1   2   3
row 1│ 4   5   6
```

### `axis=0`

Column direction-এ operation।

```python
print(arr.sum(axis=0))
```

Result:

```text
[5 7 9]
```

কারণ:

```text
1+4 = 5
2+5 = 7
3+6 = 9
```

### `axis=1`

Row direction:

```python
print(arr.sum(axis=1))
```

Result:

```text
[ 6 15]
```

---

# 🧠 Axis mental model

```text
axis=0
↓
rows collapse
→ column-wise result

axis=1
→
columns collapse
→ row-wise result
```

---

# 🔵 M02.08 — NumPy Indexing

```python
arr = np.array([10, 20, 30, 40])

print(arr[0])
print(arr[2])
```

Output:

```text
10
30
```

Negative:

```python
print(arr[-1])
```

Output:

```text
40
```

---

# 2D Indexing

```python
arr = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
```

```python
print(arr[0, 1])
```

Output:

```text
20
```

---

# 🔵 M02.09 — Slicing

```python
arr = np.array([10, 20, 30, 40, 50])

print(arr[1:4])
```

Output:

```text
[20 30 40]
```

---

# 2D slicing

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])
```

```python
print(arr[0:2, 1:3])
```

Result:

```text
[[2 3]
 [5 6]]
```

---

# 🔵 M02.10 — Reshaping

```python
arr = np.array([1, 2, 3, 4, 5, 6])

new_arr = arr.reshape(2, 3)

print(new_arr)
```

Result:

```text
[[1 2 3]
 [4 5 6]]
```

---

# Important rule

Total elements একই থাকতে হবে।

6 elements:

```text
6 = 2 × 3
6 = 3 × 2
6 = 1 × 6
```

কিন্তু:

```python
arr.reshape(4, 2)
```

invalid, কারণ:

```text
4 × 2 = 8
```

---

# `-1`

```python
arr.reshape(2, -1)
```

NumPy automatically calculate করবে।

---

# 🔵 M02.11 — Flatten vs Ravel

```python
arr = np.array([
    [1, 2],
    [3, 4]
])
```

### flatten

```python
flat = arr.flatten()
```

সাধারণত নতুন copy তৈরি করে।

### ravel

```python
flat = arr.ravel()
```

সম্ভব হলে view return করতে পারে।

এজন্য memory/performance context-এ difference গুরুত্বপূর্ণ।

---

# 🔵 M02.12 — Transpose

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

print(arr.T)
```

Result:

```text
1 4
2 5
3 6
```

Shape:

```text
(2,3)
```

থেকে:

```text
(3,2)
```

---

# 🔵 M02.13 — Concatenation

```python
a = np.array([1, 2])
b = np.array([3, 4])

result = np.concatenate([a, b])

print(result)
```

Result:

```text
[1 2 3 4]
```

2D:

```python
a = np.array([
    [1, 2]
])

b = np.array([
    [3, 4]
])

result = np.concatenate(
    [a, b],
    axis=0
)
```

---

# 🔵 M02.14 — Stacking

Vertical:

```python
np.vstack([a, b])
```

Horizontal:

```python
np.hstack([a, b])
```

Depth:

```python
np.dstack([a, b])
```

---

# 🔵 M02.15 — Splitting

```python
arr = np.array([1, 2, 3, 4, 5, 6])

result = np.split(arr, 3)
```

Output:

```text
[1 2]
[3 4]
[5 6]
```

---

# 🔵 M02.16 — Broadcasting

NumPy-এর অন্যতম powerful feature।

```python
arr = np.array([1, 2, 3])

print(arr + 10)
```

Result:

```text
[11 12 13]
```

Python list-এ এমন directly করা যায় না।

---

# 2D Broadcasting

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

arr + 10
```

Result:

```text
[[11 12 13]
 [14 15 16]]
```

---

# Vector + Matrix

```python
arr = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

vector = np.array([10, 20, 30])

print(arr + vector)
```

Result:

```text
[[11 22 33]
 [14 25 36]]
```

---

# Broadcasting Rules

NumPy dimensions compare করে **right থেকে left**।

Example:

```text
(2, 3)
(3,)
```

Compatible।

কারণ:

```text
3
3
```

match করে।

আর:

```text
(2, 3)
(2,)
```

সাধারণত compatible নয়।

---

# 🔵 M02.17 — Vectorization

Loop:

```python
numbers = [1, 2, 3, 4]

result = []

for x in numbers:
    result.append(x * 2)
```

NumPy:

```python
arr = np.array([1, 2, 3, 4])

result = arr * 2
```

এটাই vectorized operation।

---

# Vectorized comparison

```python
arr = np.array([10, 20, 30, 40])

print(arr > 20)
```

Result:

```text
[False False  True  True]
```

---

# 🔵 M02.18 — Mathematical Operations

```python
arr = np.array([1, 2, 3, 4])
```

```python
np.add(arr, 10)
np.subtract(arr, 2)
np.multiply(arr, 3)
np.divide(arr, 2)
np.power(arr, 2)
```

---

# Universal Functions

```python
np.sqrt(arr)
np.exp(arr)
np.log(arr)
np.sin(arr)
np.cos(arr)
np.abs(arr)
np.round(arr)
np.floor(arr)
np.ceil(arr)
```

---

# 🔵 M02.19 — Statistical Operations

```python
arr = np.array([10, 20, 30, 40])
```

```python
np.sum(arr)
np.mean(arr)
np.median(arr)
np.std(arr)
np.var(arr)
np.min(arr)
np.max(arr)
```

---

# Percentile

```python
np.percentile(arr, 50)
```

50th percentile ≈ median।

---

# 🔵 M02.20 — Matrix Operations

Matrix:

```python
A = np.array([
    [1, 2],
    [3, 4]
])
```

---

# Matrix Addition

```python
A + B
```

---

# Matrix Multiplication

খুব গুরুত্বপূর্ণ:

```python
A @ B
```

অথবা:

```python
np.matmul(A, B)
```

---

# Element-wise multiplication

```python
A * B
```

Difference:

```text
*  → element-wise
@  → matrix multiplication
```

---

# 🔵 M02.21 — Linear Algebra

```python
np.linalg
```

Important:

```python
np.linalg.det(A)
np.linalg.inv(A)
np.linalg.eig(A)
np.linalg.solve(A, b)
```

---

# Dot Product

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

np.dot(a, b)
```

Calculation:

```text
1×4 + 2×5 + 3×6
= 32
```

Machine Learning-এর mathematical foundation-এ এগুলো গুরুত্বপূর্ণ।

---

# 🔵 M02.22 — Random

```python
rng = np.random.default_rng(42)
```

Random integer:

```python
rng.integers(1, 10, size=5)
```

Random float:

```python
rng.random(5)
```

Normal distribution:

```python
rng.normal(
    loc=0,
    scale=1,
    size=5
)
```

---

# Random Seed

Reproducibility-এর জন্য:

```python
rng = np.random.default_rng(42)
```

একই seed দিলে একই random sequence পাওয়া যায়।

---

# 🔵 M02.23 — Boolean Masking

```python
arr = np.array([10, 20, 30, 40, 50])

mask = arr > 25

print(arr[mask])
```

Output:

```text
[30 40 50]
```

আরও সহজ:

```python
arr[arr > 25]
```

---

# Multiple Conditions

```python
arr[
    (arr > 20) &
    (arr < 50)
]
```

NumPy array-এর জন্য `&` এবং `|` ব্যবহার করার সময় conditions-এ parentheses রাখা জরুরি।

---

# 🔵 M02.24 — Conditional Operations

```python
np.where(
    arr > 25,
    "High",
    "Low"
)
```

Example:

```python
scores = np.array([
    30, 80, 90, 45
])

labels = np.where(
    scores >= 50,
    "Pass",
    "Fail"
)
```

---

# 🔵 M02.25 — Copy vs View

এটা খুব important।

```python
arr = np.array([1, 2, 3])

view = arr[1:]

view[0] = 100

print(arr)
```

Original array-ও পরিবর্তিত হতে পারে, কারণ slicing সাধারণত view দিতে পারে।

Explicit copy:

```python
copy = arr[1:].copy()
```

তারপর change করলে original নিরাপদ থাকে।

---

# 🔵 M02.26 — Sorting & Searching

```python
arr = np.array([5, 2, 9, 1])
```

```python
np.sort(arr)
```

Index:

```python
np.argsort(arr)
```

Maximum index:

```python
np.argmax(arr)
```

Minimum index:

```python
np.argmin(arr)
```

---

# 🔵 M02.27 — NaN / Infinity

```python
arr = np.array([
    1,
    2,
    np.nan,
    4
])
```

Check:

```python
np.isnan(arr)
```

Infinity:

```python
np.inf
```

Check:

```python
np.isinf(arr)
```

---

# 🔵 M02.28 — NumPy File I/O

Save:

```python
np.save(
    "array.npy",
    arr
)
```

Load:

```python
arr = np.load(
    "array.npy"
)
```

Multiple arrays:

```python
np.savez(
    "data.npz",
    x=x,
    y=y
)
```

---

# 🔵 M02.29 — NumPy Performance

NumPy-এর বড় advantage:

```text
Python loop
     ↓
slow for huge numerical data

NumPy vectorization
     ↓
optimized numerical operations
```

তবে vectorization সবসময় magic নয়—algorithm, memory access এবং operation-এর ধরনও গুরুত্বপূর্ণ।

---

# 🟠 M02.31 — Pandas Introduction

Pandas = data analysis/manipulation library।

Install:

```bash
pip install pandas openpyxl
```

Import:

```python
import pandas as pd
```

Pandas-এর দুটি core structure:

```text
Series
DataFrame
```

---

# 🟠 M02.32 — Series

Series হলো one-dimensional labeled data।

```python
import pandas as pd

scores = pd.Series([
    80,
    90,
    75
])

print(scores)
```

---

# Custom Index

```python
scores = pd.Series(
    [80, 90, 75],
    index=["A", "B", "C"]
)
```

---

# Series Access

```python
scores["A"]
```

---

# 🟠 M02.33 — DataFrame

DataFrame = table-like structure।

```python
data = {
    "name": ["Atiar", "Rahim", "Karim"],
    "age": [25, 24, 26],
    "score": [90, 85, 95]
}

df = pd.DataFrame(data)

print(df)
```

---

# DataFrame Structure

```text
     name   age   score
0    Atiar   25    90
1    Rahim   24    85
2    Karim   26    95
```

---

# 🟠 M02.34 — Index

```python
df.index
```

Default:

```text
0
1
2
```

Custom:

```python
df.index = [
    "student1",
    "student2",
    "student3"
]
```

---

# 🟠 M02.35 — Columns

```python
df.columns
```

Access:

```python
df["name"]
```

Multiple:

```python
df[
    ["name", "score"]
]
```

---

# 🟠 M02.36 — Data Types

```python
df.dtypes
```

Common:

```text
int64
float64
object
string
bool
datetime64
category
```

---

# 🟠 M02.37 — CSV

Read:

```python
df = pd.read_csv(
    "dataset.csv"
)
```

Write:

```python
df.to_csv(
    "output.csv",
    index=False
)
```

---

# CSV Options

```python
pd.read_csv(
    "data.csv",
    encoding="utf-8"
)
```

Other useful parameters:

```text
sep
header
names
usecols
dtype
nrows
skiprows
na_values
parse_dates
```

---

# 🟠 M02.38 — Excel

Read:

```python
df = pd.read_excel(
    "data.xlsx"
)
```

Specific sheet:

```python
df = pd.read_excel(
    "data.xlsx",
    sheet_name="Sheet1"
)
```

Write:

```python
df.to_excel(
    "output.xlsx",
    index=False
)
```

Multiple sheets later:

```python
with pd.ExcelWriter("output.xlsx") as writer:
    df.to_excel(
        writer,
        sheet_name="Data",
        index=False
    )
```

---

# 🟠 M02.39 — JSON

```python
df = pd.read_json(
    "data.json"
)
```

JSONL:

```python
df = pd.read_json(
    "data.jsonl",
    lines=True
)
```

---

# 🟠 M02.40 — Data Inspection

প্রথম কাজ:

```python
df.head()
```

শেষ:

```python
df.tail()
```

Shape:

```python
df.shape
```

Columns:

```python
df.columns
```

Data types:

```python
df.dtypes
```

Summary:

```python
df.describe()
```

Information:

```python
df.info()
```

Unique:

```python
df["label"].unique()
```

Number of unique:

```python
df["label"].nunique()
```

---

# 🟠 M02.41 — Selecting Columns

Single:

```python
df["name"]
```

Multiple:

```python
df[
    ["name", "score"]
]
```

Dot notation:

```python
df.name
```

কিন্তু column name conflict বা unusual name থাকলে bracket notation বেশি reliable:

```python
df["name"]
```

---

# 🟠 M02.42 — `loc`

Label-based selection:

```python
df.loc[0]
```

Rows:

```python
df.loc[0:2]
```

Specific columns:

```python
df.loc[
    0:2,
    ["name", "score"]
]
```

---

# Filtering with `loc`

```python
df.loc[
    df["score"] >= 80,
    ["name", "score"]
]
```

---

# 🟠 M02.43 — `iloc`

Position-based:

```python
df.iloc[0]
```

First two rows:

```python
df.iloc[0:2]
```

First 2 rows + first 2 columns:

```python
df.iloc[0:2, 0:2]
```

---

# loc vs iloc

```text
loc
→ label

iloc
→ integer position
```

---

# 🟠 M02.44 — Filtering

```python
df[df["score"] >= 80]
```

---

# Multiple Conditions

```python
df[
    (df["score"] >= 80) &
    (df["age"] > 20)
]
```

OR:

```python
df[
    (df["score"] >= 90) |
    (df["age"] < 25)
]
```

NOT:

```python
df[
    ~(df["score"] >= 80)
]
```

---

# 🟠 M02.45 — Multiple Conditions

Example:

```python
result = df[
    (df["score"] > 80) &
    (df["label"] == "AI")
]
```

---

# `isin()`

```python
df[
    df["label"].isin(
        ["AI", "Human"]
    )
]
```

---

# 🟠 M02.46 — Sorting

```python
df.sort_values(
    "score"
)
```

Descending:

```python
df.sort_values(
    "score",
    ascending=False
)
```

Multiple columns:

```python
df.sort_values(
    ["label", "score"],
    ascending=[True, False]
)
```

---

# 🟠 M02.47 — Add / Remove Columns

Add:

```python
df["passed"] = df["score"] >= 50
```

Calculate:

```python
df["score_percent"] = (
    df["score"] / 100
) * 100
```

Remove:

```python
df.drop(
    columns=["passed"],
    inplace=True
)
```

---

# 🟠 M02.48 — Rename

```python
df.rename(
    columns={
        "score": "final_score"
    }
)
```

Index rename:

```python
df.rename(
    index={0: "first"}
)
```

---

# 🟠 M02.49 — Missing Data

Check:

```python
df.isna()
```

Count:

```python
df.isna().sum()
```

---

# Remove missing rows

```python
df.dropna()
```

---

# Fill missing

```python
df["score"] = df["score"].fillna(0)
```

Mean:

```python
df["score"] = df["score"].fillna(
    df["score"].mean()
)
```

---

# Forward Fill

```python
df.fillna(
    method="ffill"
)
```

Modern pandas versions may prefer dedicated `ffill()`:

```python
df.ffill()
```

Backward:

```python
df.bfill()
```

---

# 🟠 M02.50 — Duplicate Data

Check:

```python
df.duplicated()
```

Count:

```python
df.duplicated().sum()
```

Remove:

```python
df.drop_duplicates()
```

Specific column:

```python
df.drop_duplicates(
    subset=["text"]
)
```

---

# 🟠 M02.51 — Data Type Conversion

```python
df["age"] = df["age"].astype(int)
```

Numeric:

```python
df["score"] = pd.to_numeric(
    df["score"],
    errors="coerce"
)
```

Date:

```python
df["date"] = pd.to_datetime(
    df["date"],
    errors="coerce"
)
```

---

# 🟠 M02.52 — String Processing

Pandas string accessor:

```python
df["text"].str.lower()
```

Strip:

```python
df["text"].str.strip()
```

Contains:

```python
df[
    df["text"].str.contains(
        "AI",
        na=False
    )
]
```

Replace:

```python
df["text"].str.replace(
    "AI",
    "Artificial Intelligence",
    regex=False
)
```

Split:

```python
df["text"].str.split()
```

Length:

```python
df["text"].str.len()
```

---

# 🟠 M02.53 — `apply()` / `map()`

Function:

```python
def clean_text(text):
    return text.strip().lower()
```

Apply:

```python
df["text"] = df["text"].apply(
    clean_text
)
```

Lambda:

```python
df["score"].apply(
    lambda x: x * 2
)
```

---

# `map()`

Series value mapping:

```python
df["label"] = df["label"].map({
    "AI": 1,
    "Human": 0
})
```

---

# `apply()` vs `map()`

```text
Series.map()
→ element-wise mapping

Series.apply()
→ function apply

DataFrame.apply()
→ row/column-wise function
```

---

# 🟠 M02.54 — GroupBy

ধরো:

```text
label     score
AI        90
AI        80
Human     70
Human     85
```

Group:

```python
df.groupby("label")
```

Average:

```python
df.groupby(
    "label"
)["score"].mean()
```

---

# Multiple Aggregations

```python
df.groupby("label")["score"].agg([
    "mean",
    "min",
    "max",
    "count"
])
```

---

# GroupBy multiple columns

```python
df.groupby(
    ["language", "label"]
)["score"].mean()
```

---

# 🟠 M02.55 — Aggregation

Common:

```python
df["score"].sum()
df["score"].mean()
df["score"].median()
df["score"].min()
df["score"].max()
df["score"].count()
```

---

# Named Aggregation

```python
result = df.groupby("label").agg(
    average_score=("score", "mean"),
    maximum_score=("score", "max"),
    sample_count=("score", "count")
)
```

---

# 🟠 M02.56 — Merge

ধরো:

### users

```text
user_id   name
1         Atiar
2         Rahim
```

### scores

```text
user_id   score
1         90
2         85
```

Merge:

```python
result = pd.merge(
    users,
    scores,
    on="user_id"
)
```

---

# Join Types

```text
inner
left
right
outer
cross
```

Inner:

```python
pd.merge(
    a,
    b,
    on="id",
    how="inner"
)
```

Left:

```python
pd.merge(
    a,
    b,
    on="id",
    how="left"
)
```

---

# 🟠 M02.57 — Join

Index-based join:

```python
result = df1.join(
    df2,
    how="left"
)
```

Difference:

```text
merge
→ column/key based relational combination

join
→ often index-based combination
```

---

# 🟠 M02.58 — Concat

Rows:

```python
pd.concat(
    [df1, df2],
    axis=0
)
```

Columns:

```python
pd.concat(
    [df1, df2],
    axis=1
)
```

---

# Merge vs Join vs Concat

```text
merge
→ keys

join
→ index

concat
→ stack datasets
```

---

# 🟠 M02.59 — Pivot Table

```python
pd.pivot_table(
    df,
    values="score",
    index="label",
    aggfunc="mean"
)
```

---

# 🟠 M02.60 — Reshape

### `melt()`

Wide:

```text
name  math  english
A     80    90
```

Long format:

```python
pd.melt(
    df,
    id_vars=["name"]
)
```

---

# Wide vs Long

```text
Wide Data
   ↓
Melt
   ↓
Long Data
```

Long format visualization এবং analytics-এ useful।

---

# 🟠 M02.61 — DateTime

```python
df["date"] = pd.to_datetime(
    df["date"]
)
```

Year:

```python
df["date"].dt.year
```

Month:

```python
df["date"].dt.month
```

Day:

```python
df["date"].dt.day
```

Day name:

```python
df["date"].dt.day_name()
```

---

# 🟠 M02.62 — Categorical Data

যদি values limited:

```text
AI
Human
Unknown
```

category করা যায়:

```python
df["label"] = df["label"].astype(
    "category"
)
```

Large datasets-এ memory efficiency বাড়াতে সাহায্য করতে পারে।

---

# 🟠 M02.63 — `query()`

Instead of:

```python
df[
    df["score"] > 80
]
```

Can use:

```python
df.query(
    "score > 80"
)
```

Multiple:

```python
df.query(
    "score > 80 and age > 20"
)
```

---

# 🟠 M02.64 — Sampling

Random rows:

```python
df.sample(
    n=10,
    random_state=42
)
```

Fraction:

```python
df.sample(
    frac=0.1,
    random_state=42
)
```

Useful for dataset inspection।

---

# 🟠 M02.65 — Complete Data Cleaning

Real dataset:

```text
Raw
 ↓
Missing values
 ↓
Duplicates
 ↓
Wrong types
 ↓
Whitespace
 ↓
Invalid values
 ↓
Outliers
 ↓
Clean Dataset
```

---

# Example Cleaning Pipeline

```python
df = pd.read_csv("dataset.csv")

df = df.drop_duplicates()

df["text"] = (
    df["text"]
    .fillna("")
    .str.strip()
)

df["score"] = pd.to_numeric(
    df["score"],
    errors="coerce"
)

df = df.dropna(
    subset=["text"]
)
```

---

# 🟠 M02.66 — Outlier Basics

ধরো:

```text
10
12
11
13
500
```

500 potentially outlier।

Basic statistical method:

```text
Q1
Q3
IQR = Q3 - Q1
```

Outlier rule:

```text
Lower = Q1 - 1.5 × IQR

Upper = Q3 + 1.5 × IQR
```

Pandas:

```python
Q1 = df["score"].quantile(0.25)
Q3 = df["score"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR
```

---

# 🟠 M02.67 — Memory Optimization

Check:

```python
df.info(
    memory_usage="deep"
)
```

Potential optimization:

```python
df["label"] = df["label"].astype(
    "category"
)
```

Numerical downcasting:

```python
df["score"] = pd.to_numeric(
    df["score"],
    downcast="integer"
)
```

Large dataset-এর ক্ষেত্রে গুরুত্বপূর্ণ।

---

# 🟠 M02.68 — Export

CSV:

```python
df.to_csv(
    "cleaned.csv",
    index=False
)
```

Excel:

```python
df.to_excel(
    "cleaned.xlsx",
    index=False
)
```

JSON:

```python
df.to_json(
    "cleaned.json",
    orient="records"
)
```

JSONL:

```python
df.to_json(
    "cleaned.jsonl",
    orient="records",
    lines=True
)
```

---

# 🟠 M02.69 — Pandas + NumPy

Pandas:

```python
df["score"]
```

NumPy:

```python
scores = df["score"].to_numpy()
```

Then:

```python
scores.mean()
```

Or:

```python
np.mean(scores)
```

---

# NumPy array → DataFrame

```python
arr = np.array([
    [1, 2],
    [3, 4]
])

df = pd.DataFrame(
    arr,
    columns=["A", "B"]
)
```

---

# 🟠 M02.70 — Pandas Performance

Large dataset-এ:

### Avoid unnecessary Python loops

Bad:

```python
for index, row in df.iterrows():
    ...
```

সব ক্ষেত্রে `iterrows()` দরকার নেই।

Prefer:

```python
df["score"] * 2
```

অথবা:

```python
df.loc[
    df["score"] > 80,
    "label"
] = "high"
```

---

# Chunk Processing

Huge CSV:

```python
for chunk in pd.read_csv(
    "huge.csv",
    chunksize=10000
):
    process(chunk)
```

Memory-efficient।

---

# 🟣 M02.71 — Mini Project

# Text Dataset Analyzer

এখন পুরো milestone-এর knowledge এক project-এ ব্যবহার করব।

---

## 🎯 Project Goal

আমরা এমন system বানাব:

```text
CSV / JSONL / Excel
        ↓
      Pandas
        ↓
    Data Inspection
        ↓
      Cleaning
        ↓
 Missing Values
        ↓
   Duplicate Removal
        ↓
   Text Processing
        ↓
    NumPy Analysis
        ↓
     GroupBy
        ↓
   Statistics Report
        ↓
 Cleaned Dataset
```

---

# Dataset

`text_dataset.csv`

```csv
id,text,label,language,score
1,"AI is changing the world.","AI","English",0.91
2,"Python is a powerful language.","Human","English",0.45
3,"  Machine learning is useful.  ","AI","English",0.87
4,"I went to the market yesterday.","Human","English",0.32
5,"AI is changing the world.","AI","English",0.91
6,,"Human","English",0.55
```

এখানে intentionally problem আছে:

```text
duplicate
missing text
extra whitespace
```

---

# Step 1 — Load

```python
import pandas as pd
import numpy as np

df = pd.read_csv(
    "text_dataset.csv"
)

print(df.head())
```

---

# Step 2 — Inspect

```python
print(df.shape)
print(df.columns)
print(df.dtypes)
print(df.info())
```

---

# Step 3 — Missing Data

```python
print(
    df.isna().sum()
)
```

---

# Step 4 — Remove Duplicates

```python
df = df.drop_duplicates(
    subset=["text"]
)
```

---

# Step 5 — Clean Text

```python
df["text"] = (
    df["text"]
    .fillna("")
    .str.strip()
)
```

---

# Step 6 — Remove Empty Text

```python
df = df[
    df["text"] != ""
]
```

---

# Step 7 — Word Count

```python
df["word_count"] = (
    df["text"]
    .str.split()
    .str.len()
)
```

---

# Step 8 — Character Count

```python
df["char_count"] = (
    df["text"]
    .str.len()
)
```

---

# Step 9 — NumPy Statistics

```python
word_counts = (
    df["word_count"]
    .to_numpy()
)

print(
    "Mean:",
    np.mean(word_counts)
)

print(
    "Median:",
    np.median(word_counts)
)

print(
    "Maximum:",
    np.max(word_counts)
)

print(
    "Minimum:",
    np.min(word_counts)
)
```

---

# Step 10 — GroupBy

```python
label_stats = df.groupby(
    "label"
)["score"].agg([
    "count",
    "mean",
    "min",
    "max"
])

print(label_stats)
```

---

# Step 11 — Filter

High score:

```python
high_score = df[
    df["score"] >= 0.80
]
```

---

# Step 12 — Sort

```python
df = df.sort_values(
    "score",
    ascending=False
)
```

---

# Step 13 — Export

```python
df.to_csv(
    "cleaned_text_dataset.csv",
    index=False
)
```

Excel:

```python
df.to_excel(
    "cleaned_text_dataset.xlsx",
    index=False
)
```

---

# Final Project Structure

```text
text_dataset_analyzer/
│
├── data/
│   ├── raw/
│   │   └── text_dataset.csv
│   │
│   ├── cleaned/
│   │   └── cleaned_dataset.csv
│   │
│   └── reports/
│       └── statistics.csv
│
├── src/
│   ├── loader.py
│   ├── cleaner.py
│   ├── analyzer.py
│   └── main.py
│
└── README.md
```

---

# 🔥 Final Challenge

নিজে এমন analyzer বানাবে যেটা automatically:

```text
[ ] CSV load করবে
[ ] Excel load করবে
[ ] JSONL load করবে
[ ] Dataset shape দেখাবে
[ ] Column information দেখাবে
[ ] Missing values count করবে
[ ] Duplicate detect করবে
[ ] Duplicate remove করবে
[ ] Empty text remove করবে
[ ] Whitespace clean করবে
[ ] Text lowercase করবে
[ ] Word count করবে
[ ] Character count করবে
[ ] NumPy দিয়ে mean বের করবে
[ ] NumPy দিয়ে median বের করবে
[ ] NumPy দিয়ে min/max বের করবে
[ ] Label distribution বের করবে
[ ] GroupBy করবে
[ ] Score অনুযায়ী sort করবে
[ ] High-score filter করবে
[ ] Cleaned CSV save করবে
[ ] Cleaned Excel save করবে
[ ] Cleaned JSONL save করবে
[ ] Statistics report তৈরি করবে
```

---

# 🧠 M02-এর Most Important Mental Model

## NumPy

```text
Python Data
     ↓
ndarray
     ↓
shape
     ↓
axis
     ↓
index/slice
     ↓
reshape
     ↓
broadcast
     ↓
vectorization
     ↓
matrix/math
     ↓
statistics
```

## Pandas

```text
CSV / Excel / JSON
        ↓
    DataFrame
        ↓
     Inspect
        ↓
     Select
        ↓
     Filter
        ↓
      Clean
        ↓
 Missing + Duplicate
        ↓
 Transform
        ↓
   GroupBy/Aggregate
        ↓
 Merge / Join / Concat
        ↓
     Analyze
        ↓
     Export
```

---

# ✅ M02 Final Completion Checklist

```text
NUMPY
────────────────────────
[ ] NumPy basics
[ ] ndarray
[ ] dtype
[ ] ndim
[ ] shape
[ ] size
[ ] axis
[ ] indexing
[ ] slicing
[ ] reshape
[ ] flatten
[ ] ravel
[ ] transpose
[ ] concatenate
[ ] vstack
[ ] hstack
[ ] dstack
[ ] split
[ ] broadcasting
[ ] vectorization
[ ] arithmetic
[ ] universal functions
[ ] mean
[ ] median
[ ] std
[ ] variance
[ ] min/max
[ ] percentile
[ ] matrix operations
[ ] element-wise multiplication
[ ] matrix multiplication
[ ] dot product
[ ] linear algebra
[ ] random
[ ] reproducibility
[ ] boolean masking
[ ] np.where
[ ] copy vs view
[ ] sorting
[ ] argsort
[ ] argmin
[ ] argmax
[ ] NaN
[ ] infinity
[ ] npy
[ ] npz
[ ] performance
```

```text
PANDAS
────────────────────────
[ ] Pandas basics
[ ] Series
[ ] DataFrame
[ ] Index
[ ] Columns
[ ] dtype
[ ] CSV
[ ] Excel
[ ] JSON
[ ] JSONL
[ ] head
[ ] tail
[ ] info
[ ] describe
[ ] unique
[ ] nunique
[ ] column selection
[ ] loc
[ ] iloc
[ ] filtering
[ ] multiple conditions
[ ] isin
[ ] sorting
[ ] add column
[ ] remove column
[ ] rename
[ ] missing data
[ ] isna
[ ] dropna
[ ] fillna
[ ] ffill
[ ] bfill
[ ] duplicates
[ ] drop_duplicates
[ ] type conversion
[ ] to_numeric
[ ] to_datetime
[ ] string processing
[ ] str.lower
[ ] str.strip
[ ] str.contains
[ ] str.replace
[ ] str.split
[ ] str.len
[ ] apply
[ ] map
[ ] GroupBy
[ ] aggregation
[ ] merge
[ ] join
[ ] concat
[ ] pivot
[ ] pivot_table
[ ] melt
[ ] reshape
[ ] datetime
[ ] categorical
[ ] query
[ ] sampling
[ ] data cleaning
[ ] outlier basics
[ ] memory optimization
[ ] CSV export
[ ] Excel export
[ ] JSON export
[ ] JSONL export
[ ] Pandas + NumPy
[ ] chunk processing
[ ] performance
```

```text
PROJECT
────────────────────────
[ ] Text Dataset Analyzer
[ ] Raw dataset
[ ] Data loading
[ ] Data inspection
[ ] Data cleaning
[ ] Missing-value handling
[ ] Duplicate handling
[ ] Text processing
[ ] NumPy statistics
[ ] GroupBy analysis
[ ] Filtering
[ ] Sorting
[ ] Report generation
[ ] CSV export
[ ] Excel export
[ ] JSONL export
```

## 🏁 M02 শেষে তুমি কী পারবে?

তখন তোমার data workflow হবে:

```text
                 RAW DATA
                    ↓
          CSV / Excel / JSONL
                    ↓
              ┌───────────┐
              │  Pandas   │
              └─────┬─────┘
                    ↓
              DataFrame
                    ↓
        ┌───────────┼───────────┐
        ↓           ↓           ↓
     Inspect      Clean       Filter
        │           │           │
        └───────────┼───────────┘
                    ↓
               Transform
                    ↓
               GroupBy
                    ↓
             Merge / Join
                    ↓
              NumPy Array
                    ↓
          Numerical Analysis
                    ↓
                Statistics
                    ↓
             Clean Dataset
                    ↓
               ML / AI / NLP
```

**এটাই M02-এর complete target।** এই milestone ভালোভাবে শেষ করলে পরের ML/NLP milestone-এ dataset নিয়ে কাজ করার সময় NumPy/Pandas-এর জন্য আলাদা foundation gap থাকবে না।


----
