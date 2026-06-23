A truly **basic-to-advanced Pandas course** would be hundreds of pages long. The most effective way is to learn the concepts in a structured order and practice each one.

# Pandas Roadmap (Basic → Advanced)

## Level 1: Foundations

### 1. Import Pandas

```python
import pandas as pd
```

---

### 2. Series

A Series is a **single column** of data.

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

Think of it as:

|Index|Value|
|---|---|
|0|10|
|1|20|
|2|30|
|3|40|

---

### 3. DataFrame

A DataFrame is a **table**.

```python
df = pd.DataFrame({
    "Name": ["John", "Anna", "Mike"],
    "Age": [20, 22, 21]
})

print(df)
```

Output:

|Name|Age|
|---|---|
|John|20|
|Anna|22|
|Mike|21|

---

## Level 2: Reading Data

### CSV

```python
df = pd.read_csv("students.csv")
```

### Excel

```python
df = pd.read_excel("students.xlsx")
```

### JSON

```python
df = pd.read_json("data.json")
```

### Save CSV

```python
df.to_csv("output.csv", index=False)
```

---

## Level 3: Inspecting Data

### First rows

```python
df.head()
```

### Last rows

```python
df.tail()
```

### Shape

```python
df.shape
```

Output:

```python
(100, 5)
```

Means:

```text
100 rows
5 columns
```

---

### Columns

```python
df.columns
```

---

### Data Types

```python
df.dtypes
```

---

### Information

```python
df.info()
```

Shows:

- Rows
    
- Columns
    
- Null values
    
- Data types
    

---

## Level 4: Selecting Data

### Single Column

```python
df["Name"]
```

Returns Series.

---

### Multiple Columns

```python
df[["Name", "Age"]]
```

Returns DataFrame.

---

### Specific Row

```python
df.iloc[0]
```

First row.

---

### Row and Column

```python
df.iloc[0, 1]
```

Row 0, Column 1.

---

## Level 5: Filtering

### Simple Filter

```python
df[df["Age"] > 20]
```

---

### Multiple Conditions

```python
df[
    (df["Age"] > 20) &
    (df["Marks"] > 80)
]
```

---

### OR Condition

```python
df[
    (df["Age"] > 20) |
    (df["Marks"] > 80)
]
```

---

## Level 6: Adding Columns

```python
df["Passed"] = df["Marks"] >= 50
```

---

### Calculated Column

```python
df["Bonus"] = df["Salary"] * 0.1
```

---

## Level 7: Missing Values

### Check Missing

```python
df.isnull()
```

---

### Count Missing

```python
df.isnull().sum()
```

---

### Fill Missing

```python
df.fillna(0)
```

---

### Remove Missing

```python
df.dropna()
```

---

## Level 8: Statistics

Example:

```python
df["Marks"]
```

### Mean

```python
df["Marks"].mean()
```

### Median

```python
df["Marks"].median()
```

### Maximum

```python
df["Marks"].max()
```

### Minimum

```python
df["Marks"].min()
```

### Standard Deviation

```python
df["Marks"].std()
```

### Summary

```python
df.describe()
```

---

## Level 9: Sorting

### Ascending

```python
df.sort_values("Marks")
```

---

### Descending

```python
df.sort_values(
    "Marks",
    ascending=False
)
```

---

## Level 10: GroupBy (Most Important)

Data:

|Department|Salary|
|---|---|
|IT|1000|
|IT|2000|
|HR|1500|

---

### Group Sum

```python
df.groupby("Department")["Salary"].sum()
```

Output:

|Department|Salary|
|---|---|
|HR|1500|
|IT|3000|

---

### Group Mean

```python
df.groupby("Department")["Salary"].mean()
```

---

## Level 11: Aggregation

```python
df.groupby("Department").agg({
    "Salary": ["sum", "mean", "max"]
})
```

Output:

|Department|Sum|Mean|Max|
|---|---|---|---|

---

## Level 12: Unique Values

```python
df["City"].unique()
```

---

### Count Values

```python
df["City"].value_counts()
```

---

## Level 13: Merge (SQL Join)

Students:

|ID|Name|
|---|---|

Marks:

|ID|Marks|
|---|---|

Merge:

```python
pd.merge(
    students,
    marks,
    on="ID"
)
```

---

## Level 14: Concatenate

```python
pd.concat([df1, df2])
```

Combines tables.

---

## Level 15: String Operations

### Uppercase

```python
df["Name"].str.upper()
```

---

### Lowercase

```python
df["Name"].str.lower()
```

---

### Contains

```python
df[
    df["Name"].str.contains("John")
]
```

---

## Level 16: DateTime

Convert:

```python
df["Date"] = pd.to_datetime(
    df["Date"]
)
```

---

Extract Year

```python
df["Date"].dt.year
```

---

Extract Month

```python
df["Date"].dt.month
```

---

Extract Day

```python
df["Date"].dt.day
```

---

## Level 17: Apply Function

```python
df["Marks"].apply(
    lambda x: x + 5
)
```

---

Custom Function

```python
def grade(x):
    if x >= 80:
        return "A"
    return "B"

df["Grade"] = df["Marks"].apply(grade)
```

---

## Level 18: Pivot Table

```python
pd.pivot_table(
    df,
    values="Sales",
    index="Region",
    aggfunc="sum"
)
```

Very common in business analytics.

---

## Level 19: MultiIndex

```python
df.set_index(
    ["Department", "Employee"]
)
```

Creates hierarchical indexes.

---

## Level 20: Advanced Indexing

### loc

Label-based:

```python
df.loc[0]
```

### iloc

Position-based:

```python
df.iloc[0]
```

---

## Level 21: Performance

### Vectorized

Good:

```python
df["Salary"] * 1.1
```

Bad:

```python
for row in df:
    pass
```

Avoid loops.

---

## Level 22: Window Functions

Rolling Average

```python
df["Sales"].rolling(3).mean()
```

Used in:

- Stock analysis
    
- Time series
    

---

## Level 23: Time Series

Set Date Index

```python
df.set_index("Date")
```

Monthly Data

```python
df.resample("M").sum()
```

Daily Data

```python
df.resample("D").mean()
```

---

## Level 24: Machine Learning Preparation

### One-Hot Encoding

```python
pd.get_dummies(
    df["City"]
)
```

---

### Feature Selection

```python
X = df[
    ["Age", "Salary"]
]

y = df["Target"]
```

---

# Most Important Pandas Topics (80% of Real Work)

If you master these 10 topics, you'll handle most real-world Pandas tasks:

1. DataFrame creation
    
2. `read_csv()`
    
3. `head()`, `info()`, `describe()`
    
4. Column selection
    
5. Filtering
    
6. Missing values (`fillna`, `dropna`)
    
7. `groupby()`
    
8. `merge()`
    
9. `apply()`
    
10. DateTime handling
    

These are the topics used daily by data analysts, data scientists, and machine learning engineers.