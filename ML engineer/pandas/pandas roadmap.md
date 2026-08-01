আপনি যেহেতু **Data Engineer / ML Engineer** দিকে যেতে চাচ্ছেন, Pandas শুধু syntax শেখা যথেষ্ট না। আপনাকে **data manipulation, cleaning, transformation, performance optimization, real-world pipeline** level পর্যন্ত যেতে হবে।

আমি আপনাকে **Pandas Mastery Course (Zero → Production Level)** হিসেবে সাজিয়ে দিচ্ছি।

# Pandas Mastery Course Roadmap

## Phase 0: Setup & Mindset

### Lesson 1: Pandas কেন লাগে?

শিখবেন:

* Data Engineer workflow এ Pandas কোথায় ব্যবহার হয়
* NumPy vs Pandas
* Pandas vs SQL
* Pandas vs Spark

Real-world use:

```
CSV
 |
Pandas
 |
Clean Data
 |
Transform
 |
Database / ML Model
```

---

# Phase 1: Pandas Foundation

## Lesson 2: Installation & Basic Structure

Topics:

* Installing pandas
* Import convention

```python
import pandas as pd
```

Pandas objects:

* Series
* DataFrame

Example:

```python
import pandas as pd

data = [10,20,30]

s = pd.Series(data)

print(s)
```

---

## Lesson 3: Series Mastery

Learn:

* Creating Series
* Indexing
* Custom index
* Vector operations
* Attributes

Example:

```python
sales = pd.Series(
    [100,200,300],
    index=["Jan","Feb","Mar"]
)

print(sales["Feb"])
```

---

## Lesson 4: DataFrame Deep Dive

Master:

* Creating DataFrame
* Columns
* Rows
* Index

Example:

```python
data = {
    "name":["Rahim","Karim"],
    "age":[25,30]
}


df = pd.DataFrame(data)

print(df)
```

---

# Phase 2: Data Loading Mastery

## Lesson 5: Reading Data

Real world files:

### CSV

```python
df = pd.read_csv(
    "users.csv"
)
```

### Excel

```python
df = pd.read_excel(
    "sales.xlsx"
)
```

### JSON

```python
df = pd.read_json(
    "data.json"
)
```

### SQL

```python
pd.read_sql()
```

---

# Phase 3: Data Exploration (Very Important)

## Lesson 6: Understanding Dataset

Commands:

```python
df.head()

df.tail()

df.shape

df.columns

df.info()

df.describe()
```

Master:

* Dataset size
* Missing values
* Data types
* Statistics

---

# Phase 4: Indexing & Selection

## Lesson 7: Selecting Data

Learn:

### Column selection

```python
df["salary"]
```

Multiple columns:

```python
df[
 ["name","salary"]
]
```

---

## Lesson 8: loc and iloc Mastery

loc:

```python
df.loc[0]
```

Condition:

```python
df.loc[
df.salary > 50000
]
```

iloc:

```python
df.iloc[0:5]
```

---

# Phase 5: Data Cleaning Mastery

## Lesson 9: Missing Data Handling

Learn:

```python
df.isnull()

df.dropna()

df.fillna()
```

Example:

```python
df["age"].fillna(
df["age"].mean()
)
```

---

## Lesson 10: Duplicate Handling

```python
df.duplicated()

df.drop_duplicates()
```

---

## Lesson 11: Data Type Conversion

Example:

```python
df["date"] = pd.to_datetime(
df["date"]
)
```

Learn:

* astype()
* datetime
* category

---

# Phase 6: Data Transformation

## Lesson 12: Filtering Data

Example:

```python
df[
(df.age>25)
&
(df.salary>50000)
]
```

---

## Lesson 13: Sorting

```python
df.sort_values(
"salary",
ascending=False
)
```

---

## Lesson 14: Adding / Removing Columns

Create:

```python
df["tax"] = df.salary*0.1
```

Remove:

```python
df.drop(
"tax",
axis=1
)
```

---

# Phase 7: Advanced Pandas

## Lesson 15: apply()

Very important.

```python
df["name"].apply(
lambda x:x.upper()
)
```

---

## Lesson 16: map()

```python
df["gender"].map(
{
"M":"Male",
"F":"Female"
}
)
```

---

## Lesson 17: GroupBy Mastery

SQL GROUP BY এর মতো:

```python
df.groupby(
"department"
)["salary"].mean()
```

Learn:

* aggregation
* multiple grouping
* custom aggregation

---

## Lesson 18: Pivot Table

```python
pd.pivot_table(
df,
values="sales",
index="city",
columns="year"
)
```

---

## Lesson 19: Merge & Join

Database JOIN এর equivalent:

INNER JOIN

```python
pd.merge(
df1,
df2,
on="id"
)
```

Learn:

* inner
* left
* right
* outer

---

# Phase 8: Time Series Pandas

## Lesson 20: DateTime Mastery

Learn:

* Date parsing
* Time index
* Resampling

Example:

```python
df.resample(
"M"
).mean()
```

---

# Phase 9: Performance Mastery

## Lesson 21: Pandas Optimization

Learn:

Bad:

```python
for row in df:
    pass
```

Good:

```python
df.apply()
```

Topics:

* vectorization
* memory optimization
* categorical dtype
* chunk processing

---

# Phase 10: Production Data Engineering

## Lesson 22: Large Dataset Handling

Learn:

CSV 20GB হলে?

Techniques:

* chunksize

```python
for chunk in pd.read_csv(
"big.csv",
chunksize=10000
):
    process(chunk)
```

---

## Lesson 23: Pandas + SQL

Learn:

Database pipeline:

```
PostgreSQL
      |
   Pandas
      |
 Cleaning
      |
 Analytics
```

Tools:

* SQLAlchemy
* psycopg

---

## Lesson 24: Pandas + APIs

REST API data:

```python
import requests

data=requests.get(url).json()

df=pd.DataFrame(data)
```

---

## Lesson 25: Pandas + Machine Learning

Pipeline:

```
Raw Data

↓

Pandas Cleaning

↓

Feature Engineering

↓

Model Training
```

Learn:

* encoding
* scaling
* feature creation

---

# Phase 11: Real Projects

## Project 1: Sales Data Analysis

Dataset:

* 1 million rows

Tasks:

* cleaning
* revenue calculation
* monthly report
* visualization

---

## Project 2: E-commerce Data Pipeline

আপনার DRF e-commerce project এর মতো:

Tables:

```
customers

orders

products

payments
```

Pandas দিয়ে:

* sales analysis
* customer segmentation
* revenue report

---

## Project 3: Data Engineer ETL Pipeline

Build:

```
API
 |
Pandas
 |
Transform
 |
PostgreSQL
 |
Dashboard
```

---

# Mastery Timeline

আপনার বর্তমান background অনুযায়ী:

| Level        | Time    |
| ------------ | ------- |
| Basic        | 7 days  |
| Intermediate | 15 days |
| Advanced     | 20 days |
| Projects     | 15 days |

Total:

**45-60 days এ Pandas production level এ যেতে পারবেন।**

---

আমি আপনাকে এটা **Lesson by Lesson hands-on course** হিসেবে করাতে পারি।

প্রতিটি lesson এ থাকবে:

1. Concept
2. Deep explanation
3. Code
4. Real dataset example
5. Practice task
6. Data Engineer interview questions

শুরু করবো:

**Pandas Mastery Course - Lesson 1: Pandas কী, কেন, এবং Data Engineer workflow এ কোথায় ব্যবহার হয়** থেকে।
