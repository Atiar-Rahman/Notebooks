## What is Pandas?

Pandas is a Python library used for **working with tabular data** (rows and columns), similar to Excel spreadsheets, SQL tables, or CSV files.

Think of it like this:

|Tool|Purpose|
|---|---|
|NumPy|Fast numerical arrays|
|Pandas|Data analysis and manipulation|
|Matplotlib|Data visualization|
|Scikit-learn|Machine learning|

---

## Why Pandas?

Suppose you have student data:

|Name|Age|Marks|
|---|---|---|
|John|20|85|
|Anna|22|92|
|Mike|21|78|

With Pandas, you can:

- Read CSV/Excel files
    
- Filter rows
    
- Select columns
    
- Clean missing data
    
- Calculate statistics
    
- Group and summarize data
    
- Prepare data for machine learning
    

---

## Install

```bash
pip install pandas
```

Import:

```python
import pandas as pd
```

---

## Main Data Structures

### 1. Series (1D)

A Series is like a single column.

```python
import pandas as pd

s = pd.Series([10, 20, 30, 40])

print(s)
```

Output:

```text
0    10
1    20
2    30
3    40
dtype: int64
```

---

### 2. DataFrame (2D)

A DataFrame is like an Excel sheet.

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["John", "Anna", "Mike"],
    "Age": [20, 22, 21],
    "Marks": [85, 92, 78]
})

print(df)
```

Output:

```text
   Name  Age  Marks
0  John   20     85
1  Anna   22     92
2  Mike   21     78
```

---

## Most Important Operations

### View data

```python
df.head()      # first 5 rows
df.tail()      # last 5 rows
df.shape       # rows, columns
df.columns     # column names
df.info()      # data information
```

---

### Select columns

```python
df["Name"]
```

Multiple columns:

```python
df[["Name", "Marks"]]
```

---

### Filter rows

Students with marks above 80:

```python
df[df["Marks"] > 80]
```

Output:

```text
   Name  Age  Marks
0  John   20     85
1  Anna   22     92
```

---

### Add new column

```python
df["Passed"] = df["Marks"] >= 80
```

Output:

```text
   Name  Age  Marks Passed
0  John   20     85   True
1  Anna   22     92   True
2  Mike   21     78  False
```

---

### Statistics

```python
df["Marks"].mean()
df["Marks"].max()
df["Marks"].min()
df["Marks"].sum()
```

---

### Read CSV File

students.csv

```csv
Name,Age,Marks
John,20,85
Anna,22,92
Mike,21,78
```

Read:

```python
df = pd.read_csv("students.csv")
```

---

### Save CSV

```python
df.to_csv("output.csv", index=False)
```

---

## Real-Life Uses of Pandas

### Data Analysis

Sales data:

```python
sales.groupby("Product")["Revenue"].sum()
```

Find total revenue per product.

---

### Data Cleaning

Replace missing values:

```python
df.fillna(0)
```

Remove missing rows:

```python
df.dropna()
```

---

### Machine Learning

Before training a model:

```python
X = df[["Age", "Marks"]]
y = df["Passed"]
```

Pandas prepares the data.

---

## NumPy vs Pandas

|Feature|NumPy|Pandas|
|---|---|---|
|Data Type|Arrays|Tables|
|Rows/Columns|Limited|Excellent|
|CSV Handling|No|Yes|
|Missing Data|Basic|Excellent|
|Data Analysis|Good|Excellent|
|ML Preparation|Good|Excellent|

Example:

NumPy:

```python
import numpy as np

arr = np.array([
    [20,85],
    [22,92]
])
```

Pandas:

```python
import pandas as pd

df = pd.DataFrame({
    "Age":[20,22],
    "Marks":[85,92]
})
```

Pandas is easier to understand because columns have names.

---

## If you want to become a Data Scientist

Learn in this order:

1. Python Basics
    
2. NumPy
    
3. Pandas
    
4. Matplotlib
    
5. Scikit-learn
    
6. Machine Learning
    

NumPy handles the math; Pandas handles the data. Together they form the foundation of almost all Python data science work.

------------
