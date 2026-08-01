# Pandas Mastery Course — Lesson 1

# Pandas কী, কেন এবং Data Engineer Workflow এ কোথায় ব্যবহার হয়

আজকের lesson এর লক্ষ্য:

* Pandas আসলে কী বুঝা
* কেন Data Engineer / ML Engineer রা Pandas ব্যবহার করে
* NumPy vs Pandas পার্থক্য
* Real-world data pipeline এ Pandas এর জায়গা
* প্রথম DataFrame তৈরি করা

---

# 1. Pandas কী?

**Pandas হলো Python-এর একটি powerful data analysis এবং data manipulation library।**

সহজ ভাষায়:

> Pandas দিয়ে আমরা টেবিল আকারের data (rows + columns) নিয়ে কাজ করি।

যেমন Excel sheet:

| name  | age | salary |
| ----- | --- | ------ |
| Rahim | 25  | 40000  |
| Karim | 30  | 60000  |
| Hasan | 28  | 50000  |

এই ধরনের data Pandas দিয়ে খুব সহজে handle করা যায়।

---

# 2. Pandas নাম কেন?

Pandas এসেছে:

**Panel Data → Pandas**

মূলত financial এবং statistical data analysis এর জন্য তৈরি করা হয়েছিল।

Created by:

Wes McKinney

Released:

2008

---

# 3. Data Engineer কেন Pandas শিখবে?

একজন Data Engineer এর কাজ:

```
Collect Data

      ↓

Clean Data

      ↓

Transform Data

      ↓

Store Data

      ↓

Analytics / ML
```

Pandas মূলত মাঝের অংশে কাজ করে:

```
Raw Data

CSV
JSON
API
Database

      ↓

   Pandas

      ↓

Clean + Transform

      ↓

Database
ML Model
Dashboard
```

---

# 4. Real World Example

ধরুন একটি e-commerce company আছে।

তাদের database:

```
customers table

id
name
email


orders table

id
customer_id
amount
date
```

প্রতিদিন:

100000 order আসে।

Data Engineer এর কাজ:

* কত revenue হলো?
* কোন product বেশি বিক্রি হলো?
* কোন customer বেশি কিনেছে?

Pandas দিয়ে:

```python
df.groupby("product")["sales"].sum()
```

এক লাইনে analysis।

---

# 5. Pandas কোথায় ব্যবহার হয়?

## 1. Data Cleaning

Example:

Raw data:

```
Name

Rahim

Karim

NULL

Hasan
```

Pandas:

```python
df.dropna()
```

---

## 2. Data Transformation

Example:

Salary:

```
40000
50000
60000
```

Tax add করতে হবে:

```python
df["tax"] = df["salary"]*0.1
```

Result:

```
salary    tax

40000     4000
50000     5000
60000     6000
```

---

## 3. Data Analysis

Example:

Average salary:

```python
df["salary"].mean()
```

Maximum:

```python
df["salary"].max()
```

---

## 4. Machine Learning Preparation

Machine Learning model raw data নিতে পারে না।

Raw:

```
Gender

Male
Female
Male
```

Convert:

```
0
1
0
```

Pandas দিয়ে:

```python
pd.get_dummies(df)
```

---

# 6. Pandas এর দুইটি Main Object

Pandas এর backbone হলো:

## 1. Series

একটি column।

Example:

```
Age

20
25
30
```

Python:

```python
import pandas as pd


age = pd.Series(
    [20,25,30]
)


print(age)
```

Output:

```
0    20
1    25
2    30
dtype: int64
```

---

## 2. DataFrame

পুরো table।

Example:

```
Name     Age

Rahim    25
Karim    30
```

Code:

```python
import pandas as pd


data = {

"name":["Rahim","Karim"],

"age":[25,30]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
    name     age

0   Rahim    25

1   Karim    30
```

---

# 7. NumPy vs Pandas

অনেকের confusion থাকে।

## NumPy

Mainly:

* Mathematical operation
* Numerical array

Example:

```python
import numpy as np


arr=np.array(
[1,2,3]
)
```

---

## Pandas

Mainly:

* Table data
* CSV
* Database data
* Cleaning

Example:

```python
import pandas as pd


df=pd.DataFrame(
{
"name":["A","B"],
"age":[20,30]
}
)
```

---

Comparison:

|                    | NumPy   | Pandas    |
| ------------------ | ------- | --------- |
| Data type          | Array   | Table     |
| Rows/columns       | ❌       | ✅         |
| CSV                | Hard    | Easy      |
| Missing data       | Basic   | Advanced  |
| SQL like operation | ❌       | ✅         |
| ML preprocessing   | Limited | Excellent |

---

# 8. Pandas Installation

Terminal:

```bash
pip install pandas
```

Check:

```python
import pandas as pd

print(pd.__version__)
```

---

# 9. প্রথম Pandas Program

```python
import pandas as pd


students = {

"name":[
"Rahim",
"Karim",
"Hasan"
],

"marks":[
80,
90,
70
]

}


df = pd.DataFrame(students)


print(df)
```

Output:

```
     name     marks

0    Rahim     80

1    Karim     90

2    Hasan     70
```

---

# 10. Data Engineer Mindset

একজন beginner ভাবে:

> "আমি Pandas এর function শিখবো"

একজন Data Engineer ভাবে:

> "আমার raw data কীভাবে clean করে usable data বানাবো?"

Example:

Raw:

```
order_date

01-01-26
2026/01/02
Jan 03 2026
```

Goal:

```
2026-01-01
2026-01-02
2026-01-03
```

এটাই Pandas skill।

---

# Lesson 1 Practice Task

নিজে করুন:

### Task 1

একটি DataFrame তৈরি করুন:

Columns:

```
product
price
quantity
```

Data:

```
Laptop 80000 2
Phone 30000 5
Mouse 1000 10
```

---

### Task 2

Calculate করুন:

```
total_price = price * quantity
```

Expected:

```
Laptop 160000
Phone 150000
Mouse 10000
```

---

### Task 3

Find করুন:

* Maximum price
* Average price

---

পরের lesson:

# Lesson 2: Pandas Series Mastery

(Series internals, index, dtype, vectorization, operations)


# Pandas Mastery Course — Lesson 2

# Pandas Series Mastery (Foundation of Pandas)

আজকের lesson এ আমরা Pandas এর সবচেয়ে basic building block **Series** নিয়ে deep dive করবো।

আজ শিখবো:

* Series কী?
* Series কেন দরকার?
* Series তৈরি করার বিভিন্ন উপায়
* Index কীভাবে কাজ করে
* dtype বুঝা
* Series operation
* Vectorization
* Real-world example

---

# 1. Pandas Series কী?

**Series হলো একটি one-dimensional labeled array।**

সহজ ভাষায়:

> Series হলো একটি single column যার প্রত্যেক value এর সাথে একটি label (index) থাকে।

Example:

একটি Excel column:

| Index | Salary |
| ----- | ------ |
| 0     | 50000  |
| 1     | 60000  |
| 2     | 70000  |

এটাই Pandas Series।

---

# 2. Series এর Structure

একটি Series এর তিনটি অংশ:

```
Index

  |

  ↓

Data

  |

  ↓

dtype
```

Example:

```python
import pandas as pd


salary = pd.Series(
    [50000,60000,70000]
)


print(salary)
```

Output:

```
0    50000
1    60000
2    70000
dtype: int64
```

এখানে:

```
Index     Value

0         50000
1         60000
2         70000
```

dtype:

```
int64
```

---

# 3. Series তৈরি করার উপায়

## Method 1: List থেকে Series

```python
import pandas as pd


numbers = [
    10,
    20,
    30,
    40
]


s = pd.Series(numbers)


print(s)
```

Output:

```
0    10
1    20
2    30
3    40
```

Default index:

```
0,1,2,3
```

---

# 4. Custom Index ব্যবহার

Default index সবসময় ব্যবহার করতে হবে এমন না।

Example:

```python
sales = pd.Series(
    [1000,2000,3000],
    index=[
        "January",
        "February",
        "March"
    ]
)


print(sales)
```

Output:

```
January      1000
February     2000
March        3000
```

এখন index meaningful।

---

# 5. Real World Example

ধরুন একটি shop এর monthly sales:

```python
sales = pd.Series(
{
"Jan":50000,
"Feb":70000,
"Mar":90000
}
)


print(sales)
```

Output:

```
Jan    50000
Feb    70000
Mar    90000
```

Dictionary দিলে:

* key → index
* value → data

হয়ে যায়।

---

# 6. Series এর গুরুত্বপূর্ণ Attributes

ধরি:

```python
sales = pd.Series(
[100,200,300]
)
```

## 1. values

Data দেখতে:

```python
sales.values
```

Output:

```
array([100,200,300])
```

---

## 2. index

Index দেখতে:

```python
sales.index
```

Output:

```
RangeIndex(start=0, stop=3)
```

---

## 3. dtype

```python
sales.dtype
```

Output:

```
int64
```

---

## 4. shape

```python
sales.shape
```

Output:

```
(3,)
```

---

## 5. size

```python
sales.size
```

Output:

```
3
```

---

# 7. Series Indexing

## Position দিয়ে access

```python
sales = pd.Series(
[100,200,300]
)


print(
sales[0]
)
```

Output:

```
100
```

---

## Custom index দিয়ে

```python
sales = pd.Series(
{
"Jan":100,
"Feb":200,
"Mar":300
}
)


print(
sales["Feb"]
)
```

Output:

```
200
```

---

# 8. Multiple Values Access

```python
sales[
[
"Jan",
"Mar"
]
]
```

Output:

```
Jan    100
Mar    300
```

---

# 9. Slicing

Example:

```python
numbers = pd.Series(
[10,20,30,40,50]
)


print(
numbers[1:4]
)
```

Output:

```
1    20
2    30
3    40
```

---

# 10. Series Mathematical Operation

Pandas এর সবচেয়ে powerful বিষয়:

## Vectorization

Normal Python:

```python
numbers=[1,2,3]


result=[]

for x in numbers:
    result.append(x*2)
```

Pandas:

```python
s = pd.Series(
[1,2,3]
)


s*2
```

Output:

```
0    2
1    4
2    6
```

No loop required।

---

# 11. Series Arithmetic

```python
price = pd.Series(
[100,200,300]
)


price + 50
```

Output:

```
0    150
1    250
2    350
```

---

Multiplication:

```python
price * 10
```

Output:

```
0    1000
1    2000
2    3000
```

---

# 12. Series Comparison

Example:

```python
salary = pd.Series(
[
30000,
50000,
70000
]
)


salary > 40000
```

Output:

```
False
True
True
```

এটা filtering এর base।

---

# 13. Boolean Filtering

```python
salary[
salary > 40000
]
```

Output:

```
1    50000
2    70000
```

মানে:

"যাদের salary 40000 এর বেশি তাদের বের করো"

---

# 14. Important Series Functions

## sum()

```python
sales.sum()
```

---

## mean()

```python
sales.mean()
```

---

## max()

```python
sales.max()
```

---

## min()

```python
sales.min()
```

---

## count()

```python
sales.count()
```

---

# 15. Missing Value Introduction

Example:

```python
data = pd.Series(
[
10,
20,
None,
40
]
)


print(data)
```

Output:

```
0    10
1    20
2    NaN
3    40
```

NaN মানে:

Not Available

---

Check:

```python
data.isnull()
```

Output:

```
False
False
True
False
```

---

# 16. Data Engineer Example

ধরি:

Daily website visitors:

```python
visitors = pd.Series(
{
"Monday":1200,
"Tuesday":1500,
"Wednesday":2000,
"Thursday":1700
}
)
```

Average visitors:

```python
visitors.mean()
```

Highest traffic:

```python
visitors.max()
```

Days above 1600:

```python
visitors[
visitors>1600
]
```

Output:

```
Wednesday    2000
Thursday     1700
```

---

# 17. Series vs Python List

| Feature        | List    | Series   |
| -------------- | ------- | -------- |
| Index          | ❌       | ✅        |
| Label          | ❌       | ✅        |
| Math operation | Limited | Powerful |
| Missing value  | Hard    | Easy     |
| Filtering      | Manual  | Easy     |
| SQL-like       | ❌       | ✅        |

---

# Lesson 2 Practice

## Task 1

একটি Series তৈরি করুন:

```
Product Sales

Laptop    80000
Phone     50000
Tablet    30000
```

---

## Task 2

Calculate করুন:

* Total sales
* Average sales
* Maximum sales

---

## Task 3

Filter করুন:

যেসব product এর sales > 40000

Expected:

```
Laptop    80000
Phone     50000
```

---

## Task 4 (Data Engineer Thinking)

একটি Series:

```
Temperature

Mon 32
Tue 35
Wed 30
Thu 40
```

Find:

* Average temperature
* Days where temperature > 33

---

পরের Lesson:

# Lesson 3: Pandas DataFrame Mastery

(DataFrame internals, columns, rows, index, creating real datasets, production usage)


# Pandas Mastery Course — Lesson 3

# Pandas DataFrame Mastery (The Heart of Pandas)

আজকের lesson খুব গুরুত্বপূর্ণ, কারণ **real-world Data Engineering, Data Analysis, ML pipeline — সব জায়গায় DataFrame সবচেয়ে বেশি ব্যবহার হয়।**

আজ শিখবো:

* DataFrame কী?
* DataFrame structure
* Series vs DataFrame
* DataFrame তৈরি করার বিভিন্ন উপায়
* Column, Row, Index বুঝা
* DataFrame properties
* Basic DataFrame operations
* Real-world dataset handling

---

# 1. DataFrame কী?

**DataFrame হলো Pandas এর দুই-dimensional labeled data structure।**

সহজ ভাষায়:

> DataFrame হলো Excel spreadsheet বা SQL table এর মতো।

Example:

| index | name  | age | salary |
| ----- | ----- | --- | ------ |
| 0     | Rahim | 25  | 40000  |
| 1     | Karim | 30  | 60000  |
| 2     | Hasan | 28  | 50000  |

এখানে:

* Rows → records
* Columns → features
* Index → row identifier

---

# 2. DataFrame এর Structure

একটি DataFrame:

```
              DataFrame

        Column     Column

          ↓          ↓

Index  Name        Salary

 0     Rahim       40000

 1     Karim       60000

 2     Hasan       50000
```

প্রতিটি column আসলে একটি Series।

মানে:

```
DataFrame

    |
    |
    +---- name column (Series)
    |
    +---- salary column (Series)
```

---

# 3. Series vs DataFrame

## Series

একটি column:

```
Salary

40000
50000
60000
```

## DataFrame

পুরো table:

```
Name      Salary

Rahim     40000
Karim     50000
Hasan     60000
```

Comparison:

| Feature     | Series | DataFrame |
| ----------- | ------ | --------- |
| Dimension   | 1D     | 2D        |
| Column      | Single | Multiple  |
| SQL table   | ❌      | ✅         |
| Excel sheet | ❌      | ✅         |
| ML Dataset  | ❌      | ✅         |

---

# 4. DataFrame তৈরি করা

## Method 1: Dictionary থেকে

সবচেয়ে বেশি ব্যবহার হয়।

```python
import pandas as pd


data = {

"name":[
"Rahim",
"Karim",
"Hasan"
],

"age":[
25,
30,
28
],

"salary":[
40000,
60000,
50000
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
    name    age   salary

0   Rahim    25   40000

1   Karim    30   60000

2   Hasan    28   50000
```

---

# 5. List of Lists থেকে DataFrame

Example:

```python
data = [

["Rahim",25,40000],

["Karim",30,60000],

["Hasan",28,50000]

]


df = pd.DataFrame(
data,
columns=[
"name",
"age",
"salary"
]
)


print(df)
```

---

# 6. NumPy Array থেকে DataFrame

```python
import numpy as np
import pandas as pd


arr = np.array(
[
[1,100],
[2,200],
[3,300]
]
)


df = pd.DataFrame(
arr,
columns=[
"id",
"price"
]
)


print(df)
```

---

# 7. DataFrame থেকে Column দেখা

ধরি:

```python
df
```

আমাদের data:

```
name age salary

Rahim 25 40000
Karim 30 60000
Hasan 28 50000
```

---

## Single column

```python
df["name"]
```

Output:

```
0 Rahim
1 Karim
2 Hasan
```

এটা একটি Series।

---

## Multiple columns

```python
df[
[
"name",
"salary"
]
]
```

Output:

```
name      salary

Rahim     40000

Karim     60000

Hasan     50000
```

---

# 8. DataFrame Index

Index হলো প্রতিটি row এর identifier।

Default:

```
0
1
2
```

Example:

```python
df.index
```

Output:

```
RangeIndex(start=0, stop=3)
```

---

# 9. Custom Index সেট করা

Example:

```python
df.index=[
"emp1",
"emp2",
"emp3"
]


print(df)
```

Output:

```
       name    age   salary

emp1   Rahim   25   40000

emp2   Karim   30   60000

emp3   Hasan   28   50000
```

---

# 10. DataFrame Important Attributes

ধরি:

```python
df
```

---

## shape

Rows এবং columns কত?

```python
df.shape
```

Output:

```
(3,3)
```

মানে:

```
3 rows
3 columns
```

---

## columns

```python
df.columns
```

Output:

```
Index(['name','age','salary'])
```

---

## index

```python
df.index
```

---

## values

```python
df.values
```

Output:

```
[
['Rahim',25,40000],
['Karim',30,60000]
]
```

---

## size

```python
df.size
```

Output:

```
9
```

কারণ:

```
rows × columns

3×3 = 9
```

---

# 11. DataFrame Information

সবচেয়ে গুরুত্বপূর্ণ:

```python
df.info()
```

Output:

```
<class pandas.DataFrame>

3 entries

Columns:

name object

age int64

salary int64
```

এখানে বুঝবেন:

* Column name
* Data type
* Missing value

---

# 12. Statistical Summary

```python
df.describe()
```

Output:

```
          age    salary

count     3      3

mean      27.6   50000

max       60000
```

এটা Data Analysis এ অনেক ব্যবহার হয়।

---

# 13. Add New Column

ধরি bonus দিতে হবে:

```python
df["bonus"] = df["salary"] * 0.1
```

Result:

```
name salary bonus

Rahim 40000 4000

Karim 60000 6000

Hasan 50000 5000
```

---

# 14. Remove Column

```python
df.drop(
"bonus",
axis=1,
inplace=True
)
```

এখানে:

```
axis=1 → column

axis=0 → row
```

---

# 15. Rename Column

Before:

```
salary
```

After:

```
monthly_salary
```

Code:

```python
df.rename(
columns={
"salary":"monthly_salary"
},
inplace=True
)
```

---

# 16. Selecting Rows

## First rows

```python
df.head()
```

Default:

প্রথম 5 row

Specific:

```python
df.head(2)
```

---

## Last rows

```python
df.tail()
```

---

# 17. DataFrame এর ভিতরে Data Type

Example:

```
name       object

age        int64

salary     int64
```

Check:

```python
df.dtypes
```

---

# 18. Real Data Engineer Example

ধরি e-commerce order data:

```python
orders = {

"order_id":[1,2,3,4],

"customer":[
"Rahim",
"Karim",
"Hasan",
"Rafi"
],

"amount":[
500,
700,
300,
900
]

}


df=pd.DataFrame(orders)
```

এখন:

Total revenue:

```python
df["amount"].sum()
```

Average order:

```python
df["amount"].mean()
```

Highest order:

```python
df["amount"].max()
```

---

# 19. DataFrame Mental Model (Important)

একজন beginner ভাবে:

> DataFrame হলো একটা table

একজন Data Engineer ভাবে:

> DataFrame হলো memory তে থাকা temporary database table

কারণ:

SQL:

```sql
SELECT *
FROM orders;
```

Pandas:

```python
df
```

---

# Lesson 3 Practice Task

## Task 1

এই DataFrame তৈরি করুন:

Columns:

```
product
category
price
stock
```

Data:

```
Laptop Electronics 80000 10

Phone Electronics 30000 20

Chair Furniture 5000 50
```

---

## Task 2

Find করুন:

1. Total products
2. Average price
3. Highest price

---

## Task 3

একটি নতুন column add করুন:

```
inventory_value = price * stock
```

Expected:

```
Laptop 800000

Phone 600000

Chair 250000
```

---

## Task 4 (Data Engineer Thinking)

আপনার তৈরি DataFrame থেকে বের করুন:

যেসব product এর price > 10000

---

পরের Lesson:

# Lesson 4: Data Loading Mastery

(CSV, Excel, JSON, SQL থেকে DataFrame তৈরি — Real Data Engineering Workflow)


# Pandas Mastery Course — Lesson 4

# Data Loading Mastery (CSV, Excel, JSON, SQL → Pandas DataFrame)

Data Engineer হিসেবে Pandas শেখার সবচেয়ে গুরুত্বপূর্ণ skill হলো:

> **বিভিন্ন source থেকে data এনে Pandas DataFrame এ load করা।**

বাস্তব জীবনে data কখনো সরাসরি Python list আকারে আসে না।

সাধারণত data আসে:

```
Database
   |
CSV
   |
Excel
   |
API
   |
JSON
   |
Cloud Storage

        ↓

     Pandas

        ↓

 Clean + Transform
```

---

# 1. Real Data Pipeline বুঝা

একজন Data Engineer এর workflow:

```
Source System

(MySQL/PostgreSQL/API)

          ↓

    Extract

          ↓

     Pandas

          ↓

 Transform

          ↓

     Load

          ↓

 Data Warehouse
```

এটাকে বলে:

**ETL Pipeline**

* Extract
* Transform
* Load

Pandas মূলত এখানে **Transform layer** এ বেশি ব্যবহার হয়।

---

# 2. CSV File থেকে Data Load

CSV = Comma Separated Values

সবচেয়ে common format।

Example CSV:

`employees.csv`

```
name,age,salary
Rahim,25,40000
Karim,30,60000
Hasan,28,50000
```

---

## read_csv()

```python
import pandas as pd


df = pd.read_csv(
    "employees.csv"
)


print(df)
```

Output:

```
    name   age   salary

0  Rahim   25   40000

1  Karim   30   60000

2  Hasan   28   50000
```

---

# 3. CSV এর প্রথম ৫ row দেখা

```python
df.head()
```

Output:

```
name    age   salary

Rahim   25    40000

Karim   30    60000
```

---

# 4. CSV এর Location দেওয়া

Folder structure:

```
project/

    data/

        employees.csv

    app.py
```

Load:

```python
df = pd.read_csv(
"data/employees.csv"
)
```

---

# 5. CSV এর Separator পরিবর্তন

সব CSV comma দিয়ে হয় না।

Example:

```
name|age|salary

Rahim|25|40000
```

এখানে:

```python
df = pd.read_csv(
"employees.csv",
sep="|"
)
```

---

# 6. Header না থাকলে

CSV:

```
Rahim,25,40000
Karim,30,60000
```

Load:

```python
df = pd.read_csv(
"employees.csv",
header=None
)
```

Output:

```
0       1       2

Rahim   25   40000
```

---

নিজে column name দিতে:

```python
df = pd.read_csv(
"employees.csv",
names=[
"name",
"age",
"salary"
]
)
```

---

# 7. Specific Columns Load করা

ধরি CSV:

```
name age salary department
```

আমাদের শুধু:

```
name
salary
```

দরকার।

```python
df = pd.read_csv(
"employees.csv",
usecols=[
"name",
"salary"
]
)
```

---

# 8. Large CSV Handling

ধরি:

```
sales.csv

50GB
```

একবারে memory তে load করলে crash করবে।

Solution:

## chunksize

```python
for chunk in pd.read_csv(
"sales.csv",
chunksize=10000
):

    print(chunk.shape)
```

এখানে:

একবারে 10000 row করে load হবে।

Data Engineer এ এটা খুব গুরুত্বপূর্ণ।

---

# 9. Excel File Load

Excel:

```
sales.xlsx
```

Install:

```bash
pip install openpyxl
```

Load:

```python
df = pd.read_excel(
"sales.xlsx"
)
```

---

# 10. Multiple Sheet Excel

Excel:

```
Sheet1
Sheet2
Sheet3
```

Specific sheet:

```python
df = pd.read_excel(
"sales.xlsx",
sheet_name="January"
)
```

---

সব sheet:

```python
data = pd.read_excel(
"sales.xlsx",
sheet_name=None
)
```

Output:

Dictionary:

```
{
January: DataFrame,

February: DataFrame
}
```

---

# 11. JSON File Load

JSON API এবং Web data এর জন্য খুব common।

Example:

`users.json`

```json
[
{
"name":"Rahim",
"age":25
},

{
"name":"Karim",
"age":30
}
]
```

Load:

```python
df = pd.read_json(
"users.json"
)
```

Output:

```
name     age

Rahim    25

Karim    30
```

---

# 12. Nested JSON Handling

Real API response:

```json
{
"users":[

{
"id":1,
"name":"Rahim"
}

]
}
```

এক্ষেত্রে:

```python
import json


data=json.load(
open("data.json")
)


df=pd.json_normalize(
data["users"]
)
```

---

# 13. API থেকে Data Load

Real example:

একটি API:

```
https://api.example.com/users
```

Response:

```json
[
{
"id":1,
"name":"Rahim"
}
]
```

Code:

```python
import requests
import pandas as pd


response=requests.get(
url
)


data=response.json()


df=pd.DataFrame(data)
```

---

# 14. SQL Database থেকে Data Load

Data Engineer এর জন্য খুব গুরুত্বপূর্ণ।

Install:

```bash
pip install sqlalchemy
```

Example:

PostgreSQL:

```
Database

     ↓

SQL Query

     ↓

Pandas
```

Code:

```python
import pandas as pd
from sqlalchemy import create_engine


engine=create_engine(
"postgresql://user:password@localhost/db"
)


df=pd.read_sql(
"SELECT * FROM orders",
engine
)
```

---

# 15. Django Project এর সাথে সম্পর্ক

আপনার DRF e-commerce project চিন্তা করুন:

Database:

```
Product

Order

Payment

Customer
```

Pandas দিয়ে:

```python
df=pd.read_sql(
"SELECT * FROM orders",
engine
)
```

তারপর:

Revenue:

```python
df["amount"].sum()
```

Monthly report:

```python
df.groupby("month")
```

---

# 16. Data Loading Best Practices

## 1. Always inspect after loading

```python
df.head()

df.info()

df.shape
```

---

## 2. Check missing values

```python
df.isnull().sum()
```

---

## 3. Check data types

```python
df.dtypes
```

---

# 17. Common Errors

## File Not Found

Error:

```
FileNotFoundError
```

Solution:

Check:

```python
import os

os.getcwd()
```

---

## Encoding Error

Problem:

```
UnicodeDecodeError
```

Solution:

```python
df=pd.read_csv(
"file.csv",
encoding="utf-8"
)
```

অথবা:

```python
encoding="latin1"
```

---

# 18. Data Engineer Mindset

Beginner:

> "আমি CSV read করতে পারি"

Data Engineer:

> "আমি যেকোনো data source থেকে data extract করে pipeline এ আনতে পারি"

---

# Lesson 4 Practice Task

## Task 1

একটি CSV তৈরি করুন:

`products.csv`

```
product,category,price

Laptop,Electronics,80000

Phone,Electronics,30000

Chair,Furniture,5000
```

Load করুন Pandas দিয়ে।

---

## Task 2

এই commands চালান:

```python
df.head()

df.info()

df.shape

df.describe()
```

Output বুঝার চেষ্টা করুন।

---

## Task 3

একটি JSON file তৈরি করুন:

```json
[
{
"name":"Rahim",
"order":500
},

{
"name":"Karim",
"order":700
}
]
```

Pandas DataFrame বানান।

---

## Task 4 (Data Engineer Challenge)

একটি fake e-commerce dataset তৈরি করুন:

Columns:

```
order_id

customer

product

amount

date
```

তারপর:

* CSV save করুন
* আবার CSV থেকে load করুন
* Total revenue বের করুন

---

পরের Lesson:

# Lesson 5: Data Exploration Mastery

(`head()`, `info()`, `describe()`, missing data analysis, dataset profiling — Real Data Analyst Skill)


# Pandas Mastery Course — Lesson 5

# Data Exploration Mastery (Dataset কে বুঝার Skill)

একজন Data Engineer বা Data Scientist যখন নতুন dataset পায়, সে প্রথমে কোনো transformation করে না।

প্রথম কাজ:

> **"এই data আসলে কেমন?"**

এই process কে বলে:

# Exploratory Data Analysis (EDA)

আজ আমরা শিখবো:

* Dataset overview নেওয়া
* Rows এবং columns বুঝা
* Data types check করা
* Statistical summary
* Missing value analysis
* Unique values
* Dataset profiling mindset

---

# 1. Real Data Workflow

একটি নতুন dataset আসলো:

```
customers.csv
```

প্রথমে:

```
Load Data

    ↓

Understand Data

    ↓

Clean Data

    ↓

Transform Data

    ↓

Analysis / ML
```

আজকের lesson শুধু:

```
Understand Data
```

---

# 2. Sample Dataset তৈরি করি

ধরি আমাদের e-commerce data:

```python
import pandas as pd


data = {

"customer":[
"Rahim",
"Karim",
"Hasan",
"Rafi",
None
],

"age":[
25,
30,
28,
35,
40
],

"order_amount":[
500,
700,
300,
900,
None
],

"city":[
"Dhaka",
"Chittagong",
"Dhaka",
"Khulna",
"Dhaka"
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
 customer       age   order_amount       city

 Rahim          25       500          Dhaka

 Karim          30       700          Chittagong

 Hasan          28       300          Dhaka

 Rafi           35       900          Khulna

 NaN            40       NaN          Dhaka
```

---

# 3. Dataset এর প্রথম কয়েকটি Row দেখা

## head()

```python
df.head()
```

Output:

প্রথম 5 rows দেখাবে।

---

Specific rows:

```python
df.head(3)
```

Output:

প্রথম 3 rows।

---

## কেন ব্যবহার করি?

Large dataset:

```
10 million rows
```

পুরো print করা যাবে না।

তাই:

```python
df.head()
```

দিয়ে sample দেখি।

---

# 4. শেষের Data দেখা

## tail()

```python
df.tail()
```

Output:

শেষের 5 rows।

---

Use case:

নতুন data append হয়েছে কিনা দেখতে।

---

# 5. Dataset এর Size জানা

## shape

```python
df.shape
```

Output:

```
(5,4)
```

মানে:

```
5 rows

4 columns
```

---

Data Engineer হিসেবে প্রথম প্রশ্ন:

"আমার কাছে কত data আছে?"

Answer:

```python
df.shape
```

---

# 6. Column Name দেখা

```python
df.columns
```

Output:

```
Index([
'customer',
'age',
'order_amount',
'city'
])
```

---

Use case:

Column spelling check করা।

---

# 7. Data Type Check

## dtypes

```python
df.dtypes
```

Output:

```
customer          object

age               int64

order_amount      float64

city              object
```

---

Data type কেন গুরুত্বপূর্ণ?

Example:

Date:

```
2026-01-01
```

যদি string হয়:

```
object
```

তাহলে:

Month বের করতে সমস্যা হবে।

Convert করতে হবে:

```python
pd.to_datetime()
```

---

# 8. Complete Dataset Information

সবচেয়ে important command:

# info()

```python
df.info()
```

Output:

```
<class pandas.DataFrame>

RangeIndex: 5 entries

Data columns:

customer       4 non-null

age            5 non-null

order_amount   4 non-null

city           5 non-null


dtypes:

object
int64
float64
```

---

এখানে আমরা পাই:

* Total rows
* Column names
* Missing values
* Data types
* Memory usage

---

# 9. Statistical Summary

## describe()

```python
df.describe()
```

Output:

```
 age    order_amount


count     5          4

mean      31.6       600

min       25         300

max       40         900
```

---

কি পাওয়া যায়?

Numeric column এর:

* count
* mean
* std
* min
* max
* percentile

---

# 10. Object Column এর Summary

Default:

```python
df.describe()
```

শুধু numeric দেয়।

সব column:

```python
df.describe(
include="all"
)
```

Output:

```
customer

unique

top

freq
```

---

# 11. Missing Value Analysis

Data cleaning এর প্রথম step।

## Check missing

```python
df.isnull()
```

Output:

```
customer

False

False

False

False

True
```

---

কিন্তু বড় dataset এ:

এটা useful না।

---

## Total missing count

```python
df.isnull().sum()
```

Output:

```
customer        1

age             0

order_amount    1

city            0
```

---

Meaning:

```
customer column এ 1টা missing

order_amount এ 1টা missing
```

---

# 12. Missing Percentage বের করা

Real Data Engineering এ খুব useful।

```python
missing_percentage = (
df.isnull().sum()
/
len(df)
)*100


print(missing_percentage)
```

Output:

```
customer        20%

order_amount    20%
```

---

Rule:

যদি:

```
Missing > 50%
```

তাহলে column remove করার কথা চিন্তা করা যায়।

---

# 13. Unique Values Count

## unique()

```python
df["city"].unique()
```

Output:

```
[
Dhaka,
Chittagong,
Khulna
]
```

---

## কতগুলো unique?

```python
df["city"].nunique()
```

Output:

```
3
```

---

# 14. Value Count

সবচেয়ে বেশি ব্যবহার হয়।

```python
df["city"].value_counts()
```

Output:

```
Dhaka          3

Chittagong     1

Khulna         1
```

---

Use case:

Customer কোন city থেকে বেশি?

---

# 15. Dataset Memory Usage

```python
df.memory_usage()
```

Large dataset optimization এ লাগে।

---

# 16. Data Profiling Checklist

নতুন dataset পেলে:

## Step 1

Rows:

```python
df.shape
```

---

## Step 2

Columns:

```python
df.columns
```

---

## Step 3

Data types:

```python
df.dtypes
```

---

## Step 4

Missing:

```python
df.isnull().sum()
```

---

## Step 5

Statistics:

```python
df.describe()
```

---

## Step 6

Unique:

```python
df.nunique()
```

---

# 17. Real Data Engineer Example

ধরি আপনার DRF e-commerce project এর order table:

Columns:

```
order_id

customer_id

product_id

amount

status

created_at
```

প্রথমে:

```python
df.info()
```

দেখবেন:

```
created_at object
```

তাহলে:

Problem:

Date হিসেবে ব্যবহার করা যাবে না।

Solution:

```python
df["created_at"] = pd.to_datetime(
df["created_at"]
)
```

---

# 18. Beginner vs Data Engineer Thinking

Beginner:

> "আমি df.head() জানি"

Data Engineer:

> "আমি dataset profile করে বুঝতে পারি কোথায় quality problem আছে"

---

# Lesson 5 Practice Task

একটি dataset তৈরি করুন:

```python
data = {

"name":[
"Rahim",
"Karim",
"Hasan",
None
],

"salary":[
40000,
50000,
None,
70000
],

"department":[
"IT",
"HR",
"IT",
"Finance"
]

}
```

---

Tasks:

### 1.

DataFrame তৈরি করুন।

### 2.

Run করুন:

```python
df.head()

df.shape

df.info()

df.describe()
```

---

### 3.

Find করুন:

* কোন column এ missing value আছে?
* কোন department সবচেয়ে বেশি আছে?
* কয়টি unique department আছে?

---

### 4. Data Engineer Challenge

একটি 100-row employee dataset তৈরি করে:

* missing analysis
* data type check
* summary report তৈরি করুন।

---

পরের Lesson:

# Lesson 6: Data Selection Mastery

(`loc`, `iloc`, column selection, row filtering, conditional data extraction — Pandas এর সবচেয়ে বেশি ব্যবহৃত skill)


----------

# Pandas Mastery Course — Lesson 6

# Data Selection Mastery (`loc`, `iloc`, Column Selection, Filtering)

আজকের lesson Pandas এর সবচেয়ে বেশি ব্যবহার হওয়া অংশগুলোর একটি।

বাস্তব Data Engineering এ 80% সময় আপনাকে করতে হয়:

* নির্দিষ্ট column বের করা
* নির্দিষ্ট row বের করা
* condition দিয়ে data filter করা
* প্রয়োজনীয় data আলাদা করা

আজ শিখবো:

* Column selection
* Row selection
* `loc[]`
* `iloc[]`
* Conditional filtering
* Multiple conditions
* Real-world examples

---

# 1. Sample Dataset

আমরা এই dataset ব্যবহার করবো:

```python
import pandas as pd


data = {

"employee":[
"Rahim",
"Karim",
"Hasan",
"Rafi",
"Sakib"
],

"department":[
"IT",
"HR",
"IT",
"Finance",
"Marketing"
],

"age":[
25,
30,
28,
35,
27
],

"salary":[
40000,
60000,
50000,
70000,
45000
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
   employee department age salary

0  Rahim    IT         25 40000

1  Karim    HR         30 60000

2  Hasan    IT         28 50000

3  Rafi     Finance    35 70000

4  Sakib    Marketing  27 45000
```

---

# 2. Column Selection

## Single Column

```python
df["salary"]
```

Output:

```
0    40000
1    60000
2    50000
3    70000
4    45000
```

এটা return করে:

```
Series
```

---

# 3. Multiple Columns

```python
df[
[
"employee",
"salary"
]
]
```

Output:

```
employee   salary

Rahim      40000

Karim      60000
```

এটা return করে:

```
DataFrame
```

---

# 4. Column Selection Using dot notation

Example:

```python
df.salary
```

Output:

```
0    40000
1    60000
```

কাজ করে।

কিন্তু recommended:

```python
df["salary"]
```

কারণ:

যদি column name হয়:

```
total salary
```

তাহলে:

```python
df.total salary
```

কাজ করবে না।

---

# 5. Row Selection

এখন প্রশ্ন:

"আমার নির্দিষ্ট row দরকার"

এখানে আসে:

# loc এবং iloc

---

# 6. loc[] কী?

`loc` ব্যবহার হয়:

> Label based selection

মানে index নাম দিয়ে data select করা।

---

Default index:

```
0
1
2
3
4
```

Example:

```python
df.loc[0]
```

Output:

```
employee        Rahim
department        IT
age                25
salary          40000
```

---

# 7. Multiple Rows using loc

```python
df.loc[
[
0,
2,
4
]
]
```

Output:

```
Rahim

Hasan

Sakib
```

---

# 8. Range Selection with loc

```python
df.loc[0:3]
```

Output:

```
0
1
2
3
```

Important:

`loc` এর ক্ষেত্রে শেষ value include হয়।

মানে:

```
0:3

= 0,1,2,3
```

---

# 9. loc দিয়ে Column Selection

Syntax:

```python
df.loc[
row,
column
]
```

Example:

```python
df.loc[
0,
"salary"
]
```

Output:

```
40000
```

---

Multiple:

```python
df.loc[
0:2,
[
"employee",
"salary"
]
]
```

Output:

```
employee salary

Rahim    40000

Karim    60000

Hasan    50000
```

---

# 10. iloc[] কী?

`iloc`:

> Integer location based selection

মানে position দিয়ে selection।

---

Example:

```python
df.iloc[0]
```

প্রথম row।

---

# 11. iloc Multiple Rows

```python
df.iloc[
0:3
]
```

Output:

```
0
1
2
```

Important:

`iloc` এ শেষ value include হয় না।

Python slicing এর মতো।

```
0:3

=0,1,2
```

---

# 12. loc vs iloc Difference

|              | loc          | iloc         |
| ------------ | ------------ | ------------ |
| Based on     | Label        | Position     |
| Input        | string/index | integer      |
| End included | Yes          | No           |
| SQL style    | More similar | Python style |

Example:

Index:

```
10
20
30
```

loc:

```python
df.loc[20]
```

কাজ করবে।

iloc:

```python
df.iloc[20]
```

20 নম্বর position খুঁজবে।

---

# 13. Conditional Filtering

এটাই সবচেয়ে important।

Question:

"যাদের salary 50000 এর বেশি তাদের বের করো"

Code:

```python
df[
df["salary"] > 50000
]
```

Output:

```
Karim

Rafi
```

---

# 14. Multiple Conditions

## AND condition

Example:

Salary > 40000

এবং

Age > 28

```python
df[
(df["salary"] > 40000)
&
(df["age"] > 28)
]
```

Output:

```
Karim

Rafi
```

---

Important:

Pandas এ:

```
and ❌
```

ব্যবহার করা যাবে না।

Use:

```
& ✅
```

---

# 15. OR Condition

Example:

IT অথবা HR department

```python
df[
(df["department"]=="IT")
|
(df["department"]=="HR")
]
```

Use:

```
| 
```

---

# 16. isin() ব্যবহার

Alternative:

```python
df[
df["department"].isin(
[
"IT",
"HR"
]
)
]
```

Output:

```
IT

HR
```

অনেক clean।

---

# 17. String Filtering

Example:

যাদের নাম R দিয়ে শুরু:

```python
df[
df["employee"].str.startswith("R")
]
```

Output:

```
Rahim
Rafi
```

---

Contains:

```python
df[
df["employee"].str.contains("a")
]
```

---

# 18. Query Method

আরেকটি সুন্দর syntax:

```python
df.query(
"salary > 50000"
)
```

Output:

```
Karim

Rafi
```

---

Multiple:

```python
df.query(
"salary > 40000 and age > 28"
)
```

---

# 19. Real E-commerce Example

Order Data:

```
order_id customer amount status
1        Rahim    500    paid
2        Karim    800    pending
3        Hasan    300    paid
```

Question:

শুধু paid orders:

```python
df[
df["status"]=="paid"
]
```

---

Revenue > 500:

```python
df[
df["amount"]>500
]
```

---

# 20. Data Engineer Use Case

Database থেকে 10 million rows এসেছে:

```python
df
```

কিন্তু দরকার:

শুধু:

```
customer_id
amount
date
```

তাহলে:

```python
df[
[
"customer_id",
"amount",
"date"
]
]
```

Memory কম লাগবে।

---

# 21. Performance Tip

Avoid:

```python
df[df.column]
```

Prefer:

```python
df["column"]
```

কারণ:

* readable
* safe
* production friendly

---

# Lesson 6 Summary

আজ শিখলেন:

✅ Column selection
✅ Row selection
✅ loc
✅ iloc
✅ Filtering
✅ Multiple conditions
✅ isin()
✅ query()
✅ String filtering

---

# Practice Task

এই dataset:

```python
data = {

"name":["A","B","C","D"],

"age":[20,30,25,35],

"salary":[30000,60000,45000,80000],

"department":[
"IT",
"HR",
"IT",
"Finance"
]

}
```

Tasks:

### 1.

শুধু:

```
name
salary
```

column বের করুন।

---

### 2.

শুধু:

```
age > 25
```

employees বের করুন।

---

### 3.

যাদের:

```
salary > 50000
AND
department = IT
```

তাদের বের করুন।

---

### 4.

`loc` ব্যবহার করে প্রথম 3 row এবং শুধু name + salary বের করুন।

---

### 5.

`iloc` ব্যবহার করে last 2 row বের করুন।

---

পরের Lesson:

# Lesson 7: Data Cleaning Mastery Part-1

(Missing Values, `dropna()`, `fillna()`, Null handling — Real Production Data Cleaning)

------
# Pandas Mastery Course — Lesson 7

# Data Cleaning Mastery Part-1

## Missing Values, `dropna()`, `fillna()`, Null Handling

Data Engineer হিসেবে সবচেয়ে বেশি সময় যায়:

> **Dirty data কে clean এবং usable করা।**

Real-world data কখনো perfect হয় না।

Example:

Customer Data:

| name  | age  | salary | city       |
| ----- | ---- | ------ | ---------- |
| Rahim | 25   | 40000  | Dhaka      |
| Karim | 30   | NULL   | Chittagong |
| Hasan | NULL | 50000  | Dhaka      |
| Rafi  | 35   | 70000  | NULL       |

এখানে সমস্যা:

* age missing
* salary missing
* city missing

এগুলো handle করতে হবে।

---

# 1. Missing Value কী?

যখন কোনো data পাওয়া যায় না:

Examples:

```
NULL

NaN

None

Blank cell

```

Pandas এ এগুলো সাধারণত:

```python
NaN
```

হিসেবে থাকে।

---

# 2. Sample Dataset

```python
import pandas as pd
import numpy as np


data = {

"name":[
"Rahim",
"Karim",
"Hasan",
"Rafi",
None
],

"age":[
25,
30,
None,
35,
40
],

"salary":[
40000,
None,
50000,
70000,
60000
],

"city":[
"Dhaka",
"Chittagong",
"Dhaka",
None,
"Khulna"
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
     name        age   salary        city

0   Rahim       25    40000       Dhaka

1   Karim       30    NaN        Chittagong

2   Hasan       NaN   50000       Dhaka

3   Rafi        35    70000       NaN

4   NaN         40    60000       Khulna
```

---

# 3. Missing Value Check

## isnull()

```python
df.isnull()
```

Output:

```
name     age    salary    city

False   False   False    False

False   False   True     False

False   True    False    False

False   False   False    True

True    False   False    False
```

---

কিন্তু বড় dataset এ এটা useful না।

আমরা count চাই।

---

# 4. Total Missing Count

```python
df.isnull().sum()
```

Output:

```
name      1

age       1

salary    1

city      1
```

Meaning:

```
name column এ 1টা missing

age column এ 1টা missing
```

---

# 5. Missing Percentage

Production data এ খুব গুরুত্বপূর্ণ।

Formula:

```
missing percentage = missing / total rows * 100
```

Code:

```python
missing_percentage = (
    df.isnull().sum()
    /
    len(df)
)*100


print(missing_percentage)
```

Output:

```
name      20%

age       20%

salary    20%

city      20%
```

---

# 6. Missing Value Remove করা

## dropna()

যে row তে missing আছে:

remove করে দেয়।

Example:

```python
df.dropna()
```

Output:

```
Rahim 25 40000 Dhaka
```

কারণ:

যে row তে কোনো missing নেই শুধু সেটাই থাকে।

---

# 7. dropna() এর সমস্যা

ধরি:

Dataset:

```
10 million rows
```

মাত্র:

```
1000 row missing
```

সব delete করলে অনেক data loss হবে।

তাই বুঝে ব্যবহার করতে হয়।

---

# 8. dropna(axis)

## Row remove (default)

```python
df.dropna(
axis=0
)
```

মানে:

row remove।

---

## Column remove

```python
df.dropna(
axis=1
)
```

Example:

যে column এ missing আছে:

সেই column delete হবে।

---

# 9. Drop Condition Control

## how="all"

শুধু সব value missing হলে delete:

```python
df.dropna(
how="all"
)
```

Example:

```
name age salary

NaN NaN NaN
```

এই row delete হবে।

---

## how="any"

Default:

```python
df.dropna(
how="any"
)
```

একটা missing থাকলেই remove।

---

# 10. subset ব্যবহার

ধরি:

আমাদের জন্য salary important।

salary missing হলে row delete:

```python
df.dropna(
subset=[
"salary"
]
)
```

এখন শুধু salary column check করবে।

---

# 11. Missing Value Fill করা

সবসময় delete করা ঠিক না।

অনেক সময় fill করতে হয়।

Function:

```python
fillna()
```

---

# 12. Constant Value দিয়ে Fill

Example:

```python
df["city"].fillna(
"Unknown"
)
```

Output:

```
Dhaka

Chittagong

Dhaka

Unknown

Khulna
```

---

# 13. Mean দিয়ে Fill

Age:

```python
df["age"].fillna(
df["age"].mean()
)
```

Example:

Age:

```
25
30
NaN
35
40
```

Mean:

```
32.5
```

Result:

```
25
30
32.5
35
40
```

---

# 14. Median দিয়ে Fill

Outlier থাকলে median ভালো।

Example:

Salary:

```
40000
50000
70000
1000000
```

Mean ভুল হতে পারে।

Use:

```python
df["salary"].fillna(
df["salary"].median()
)
```

---

# 15. Mode দিয়ে Fill

Categorical data:

Example:

City:

```
Dhaka
Dhaka
Khulna
NaN
```

সবচেয়ে বেশি:

```
Dhaka
```

Code:

```python
df["city"].fillna(
df["city"].mode()[0]
)
```

---

# 16. Forward Fill (ffill)

আগের value দিয়ে fill করে।

Example:

Before:

```
Date      Sales

Jan       100

Feb       NaN

Mar       300
```

Code:

```python
df.ffill()
```

After:

```
Jan 100

Feb 100

Mar 300
```

---

# 17. Backward Fill (bfill)

পরের value দিয়ে fill:

```python
df.bfill()
```

Example:

Before:

```
Jan NaN

Feb 200
```

After:

```
Jan 200

Feb 200
```

---

# 18. inplace Parameter

Without inplace:

```python
df.fillna(0)
```

শুধু output change হবে।

Original dataframe change হবে না।

---

With inplace:

```python
df.fillna(
0,
inplace=True
)
```

Original change হবে।

---

# 19. Real Data Engineer Example

ধরি e-commerce order data:

```
order_id

customer_id

amount

payment_status
```

Problem:

```
payment_status

paid

NULL

pending
```

Solution:

```python
df["payment_status"].fillna(
"unknown",
inplace=True
)
```

---

# 20. Missing Handling Strategy

Data Engineer এ decision:

## Case 1:

Column:

```
Customer phone
```

50% missing

Action:

Remove column

---

## Case 2:

Column:

```
Age
```

5% missing

Action:

Mean/Median fill

---

## Case 3:

Column:

```
Payment status
```

Missing

Action:

Unknown category

---

# 21. Best Practice

Cleaning এর আগে:

Always check:

```python
df.isnull().sum()
```

তারপর সিদ্ধান্ত:

* Drop?
* Fill?
* Keep?

Blindly:

```python
df.dropna()
```

করবেন না।

---

# Lesson 7 Practice Task

Dataset:

```python
data={

"name":[
"A",
"B",
"C",
"D"
],

"age":[
20,
None,
30,
40
],

"salary":[
30000,
50000,
None,
70000
],

"department":[
"IT",
None,
"HR",
"IT"
]

}
```

Tasks:

### 1.

Missing values count করুন।

---

### 2.

Age missing হলে mean দিয়ে fill করুন।

---

### 3.

Salary missing হলে median দিয়ে fill করুন।

---

### 4.

Department missing হলে "Unknown" দিন।

---

### 5.

যেসব row তে name missing আছে delete করুন।

---

### 6. Data Engineer Challenge

একটি fake customer dataset তৈরি করুন:

Columns:

```
customer_id

name

email

age

city

purchase_amount
```

তার মধ্যে ইচ্ছা করে missing value রাখুন।

তারপর:

* Missing report তৈরি করুন
* Cleaning strategy লিখুন
* Clean dataframe তৈরি করুন

---

পরের Lesson:

# Lesson 8: Data Cleaning Mastery Part-2

(Duplicates, Data Types, String Cleaning, Date Cleaning, Production Data Quality Checks)


-----------

# Pandas Mastery Course — Lesson 8

# Data Cleaning Mastery Part-2

## Duplicates, Data Types, String Cleaning, Date Cleaning, Data Quality Checks

গত lesson এ আমরা শিখেছি:

* Missing value কী
* `isnull()`
* `dropna()`
* `fillna()`

আজ আমরা শিখবো:

* Duplicate data remove করা
* Data type ঠিক করা
* String cleaning
* Date cleaning
* Data quality validation

এগুলো **Production Data Engineering-এর core skill**।

---

# 1. Duplicate Data কী?

Duplicate মানে একই data একাধিকবার থাকা।

Example:

Customer table:

| id | name  | email                                     |
| -- | ----- | ----------------------------------------- |
| 1  | Rahim | [rahim@gmail.com](mailto:rahim@gmail.com) |
| 2  | Karim | [karim@gmail.com](mailto:karim@gmail.com) |
| 3  | Rahim | [rahim@gmail.com](mailto:rahim@gmail.com) |

এখানে row 1 এবং row 3 duplicate।

---

# 2. Sample Dataset

```python id="9r0q7c"
import pandas as pd


data = {

"customer_id":[
1,
2,
3,
4,
5
],

"name":[
"Rahim",
"Karim",
"Rahim",
"Hasan",
"Karim"
],

"email":[
"rahim@gmail.com",
"karim@gmail.com",
"rahim@gmail.com",
"hasan@gmail.com",
"karim@gmail.com"
]

}


df = pd.DataFrame(data)


print(df)
```

---

# 3. Duplicate Check

## duplicated()

```python id="5v8n2x"
df.duplicated()
```

Output:

```id="m94z7c"
False

False

True

False

True
```

Meaning:

* প্রথম Rahim → original
* দ্বিতীয় Rahim → duplicate

---

# 4. Total Duplicate Count

```python id="6zq4sc"
df.duplicated().sum()
```

Output:

```
2
```

মানে:

2টা duplicate row আছে।

---

# 5. Duplicate Remove করা

## drop_duplicates()

```python id="svx7w4"
df.drop_duplicates()
```

Output:

```id="4o8wqg"
1 Rahim

2 Karim

4 Hasan
```

---

# 6. Original Data Change

Default:

```python id="8k6y3a"
df.drop_duplicates()
```

শুধু output change করে।

Permanent:

```python id="q7a3ks"
df.drop_duplicates(
inplace=True
)
```

---

# 7. Specific Column Based Duplicate

ধরি:

আমাদের email unique হওয়া উচিত।

```python id="2n9q0p"
df.drop_duplicates(
subset=[
"email"
]
)
```

এখন শুধু email দেখে duplicate remove করবে।

---

# 8. Keep Parameter

Default:

```python id="u0g0cx"
keep="first"
```

প্রথমটা রাখে।

Example:

```python id="g0tq67"
df.drop_duplicates(
keep="last"
)
```

শেষেরটা রাখবে।

সব delete:

```python id="f8x9d6"
df.drop_duplicates(
keep=False
)
```

---

# 9. Data Type Cleaning

Real data এ অনেক সময় type ভুল থাকে।

Example:

```python id="j98wq4"
Age

"25"

"30"

"40"
```

এগুলো number না।

এগুলো string।

---

Check:

```python id="8a7gqi"
df.dtypes
```

---

# 10. Type Conversion

## astype()

String থেকে integer:

```python id="nvjv1s"
df["age"].astype(
int
)
```

---

Example:

Before:

```
"25"
```

After:

```
25
```

---

# 11. Numeric Conversion

অনেক সময়:

```id="9d1n0s"
salary

"40000"

"50000"

"abc"
```

Problem:

abc number না।

Solution:

```python id="y9szb1"
pd.to_numeric(
df["salary"],
errors="coerce"
)
```

---

`errors="coerce"`

মানে:

Invalid value → NaN

---

# 12. Category Data Type

Example:

Department:

```
IT
HR
Finance
```

এগুলো repeated data।

Normal:

```id="x2k6qp"
object
```

Better:

```python id="o7s8gt"
df["department"] = df["department"].astype(
"category"
)
```

Benefit:

* Memory কম লাগে
* Performance বাড়ে

---

# 13. String Cleaning

Real data:

```
" Rahim "
" KARIM "
"hasan "
```

Problem:

Extra space + uppercase/lowercase issue।

---

# 14. Remove Extra Space

Before:

```
" Rahim "
```

Code:

```python id="ojkq6r"
df["name"].str.strip()
```

After:

```
"Rahim"
```

---

# 15. Lowercase Conversion

```python id="x1v2y7"
df["name"].str.lower()
```

Before:

```
RAHIM
```

After:

```
rahim
```

---

# 16. Uppercase Conversion

```python id="h2m8d4"
df["name"].str.upper()
```

---

# 17. Title Case

```python id="qf9h5w"
df["name"].str.title()
```

Example:

```
rahim rahman
```

becomes:

```
Rahim Rahman
```

---

# 18. Replace Text

Example:

Before:

```
Dhaka City
```

Need:

```
Dhaka
```

Code:

```python id="6j9r7v"
df["city"].str.replace(
" City",
""
)
```

---

# 19. Date Cleaning

Date data খুব গুরুত্বপূর্ণ।

Example:

```
01-01-2026
2026/01/02
Jan 03 2026
```

সব format different।

---

# 20. Convert Date

```python id="p7d3la"
df["date"] = pd.to_datetime(
df["date"]
)
```

Output:

```
2026-01-01
2026-01-02
2026-01-03
```

---

# 21. Date থেকে Information বের করা

Year:

```python id="7wq1hb"
df["date"].dt.year
```

Month:

```python id="xk9f8p"
df["date"].dt.month
```

Day:

```python id="t8m5yy"
df["date"].dt.day
```

---

# 22. Data Quality Checks

Production pipeline এ data আসার পরে check করা হয়।

Example:

## Check 1: Duplicate

```python id="12zq4m"
df.duplicated().sum()
```

---

## Check 2: Missing

```python id="8j2m8h"
df.isnull().sum()
```

---

## Check 3: Data Type

```python id="o4c9qa"
df.dtypes
```

---

## Check 4: Unique

```python id="a1f6l8"
df.nunique()
```

---

# 23. Real E-commerce Example

Order data:

```
order_id
customer_email
amount
created_at
```

Problem:

```
customer_email

" USER@gmail.com "

" user@gmail.com"
```

Same user।

Cleaning:

```python id="c9y0ts"
df["customer_email"] = (
df["customer_email"]
.str.strip()
.str.lower()
)
```

---

# 24. Complete Cleaning Pipeline

একজন Data Engineer সাধারণত:

```python id="u0f3u9"
Load Data

↓

Check Shape

↓

Check Missing

↓

Remove Duplicate

↓

Fix Data Types

↓

Clean Strings

↓

Fix Dates

↓

Validate

↓

Store
```

---

# 25. Production Mindset

Beginner:

> "Data clean করা মানে null remove করা"

Engineer:

> "Data quality নিশ্চিত করা যাতে downstream system ভুল না করে"

---

# Lesson 8 Practice Task

Dataset:

```python id="yt4p2x"
data={

"name":[
" rahim ",
"KARIM",
"rahim",
"Hasan "
],

"age":[
"25",
"30",
"25",
"40"
],

"email":[
"RAHIM@gmail.com",
"karim@gmail.com",
"rahim@gmail.com",
"hasan@gmail.com"
],

"date":[
"2026/01/01",
"01-02-2026",
"Jan 03 2026",
"2026-01-04"
]

}
```

Tasks:

### 1.

Duplicate email remove করুন।

### 2.

Name clean করুন:

* strip
* lowercase

### 3.

Age integer করুন।

### 4.

Date datetime করুন।

### 5.

Final cleaned DataFrame তৈরি করুন।

---

পরের Lesson:

# Lesson 9: Data Transformation Mastery

(Column creation, apply(), map(), lambda, feature engineering — Real Data Pipeline Skill)
# Pandas Mastery Course — Lesson 9

# Data Transformation Mastery

## Column Creation, `apply()`, `map()`, Lambda, Feature Engineering

আজকের lesson থেকে আমরা Pandas এর সবচেয়ে powerful অংশে ঢুকবো।

Data Engineer এর কাজ শুধু data clean করা না।

Clean data কে business-friendly format এ transform করতে হয়।

Example:

Raw data:

| price | quantity |
| ----- | -------- |
| 1000  | 5        |
| 2000  | 3        |

আমাদের দরকার:

| price | quantity | total_sales |
| ----- | -------- | ----------- |
| 1000  | 5        | 5000        |
| 2000  | 3        | 6000        |

এই transformation Pandas দিয়ে করা হয়।

---

# 1. Data Transformation কী?

সহজ ভাষায়:

> Existing data থেকে নতুন useful data তৈরি করা।

Pipeline:

```id="1h8j2k"
Raw Data

    ↓

Cleaning

    ↓

Transformation

    ↓

Analytics / ML
```

---

# 2. Sample Dataset

```python id="2h1q8f"
import pandas as pd


data = {

"product":[
"Laptop",
"Phone",
"Mouse",
"Keyboard"
],

"price":[
80000,
30000,
1000,
3000
],

"quantity":[
2,
5,
10,
4
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```id="s6j2q1"
Product      price    quantity

Laptop       80000       2

Phone        30000       5

Mouse        1000       10

Keyboard     3000        4
```

---

# 3. New Column Create করা

সবচেয়ে basic transformation।

## Total Amount

Formula:

```
price × quantity
```

Code:

```python id="9n2l4v"
df["total_amount"] = (
    df["price"] *
    df["quantity"]
)
```

Result:

```id="c8v3y5"
Product    total_amount

Laptop       160000

Phone        150000

Mouse         10000

Keyboard      12000
```

---

# 4. Constant Value Column

Example:

সব product এর country:

```python id="7m4x9p"
df["country"] = "Bangladesh"
```

Result:

```id="r3p8q2"
country

Bangladesh
Bangladesh
Bangladesh
```

---

# 5. Conditional Column Creation

Problem:

Sales amount দেখে category তৈরি করতে হবে।

Rule:

```
>=100000 → High

<100000 → Low
```

Traditional Python:

```python id="8f4k1q"
if amount >= 100000:
    return "High"
```

Pandas:

```python id="k8m5q3"
df["sales_type"] = (
    df["total_amount"]
    .apply(
        lambda x:
        "High"
        if x>=100000
        else "Low"
    )
)
```

---

# 6. apply() কী?

`apply()` ব্যবহার হয়:

> প্রতিটি value এর উপর একটি function চালানোর জন্য।

Structure:

```python id="v6h2p9"
Series.apply(function)
```

---

Example:

```python id="t7q3m1"
def discount(price):

    return price*0.9


df["discount_price"] = (
df["price"]
.apply(discount)
)
```

---

Result:

```id="e5r8k0"
price   discount_price

80000      72000

30000      27000
```

---

# 7. Lambda Function

Small function লেখার shortcut।

Normal:

```python id="m2v9s7"
def square(x):
    return x*x
```

Lambda:

```python id="q4z8w2"
lambda x: x*x
```

---

Example:

```python id="s9x3n5"
df["double_price"] = (
df["price"]
.apply(
lambda x:x*2
)
)
```

---

# 8. String apply()

Example:

Name uppercase:

```python id="h8c4z6"
df["product"].apply(
lambda x:x.upper()
)
```

Output:

```id="p7m2k9"
LAPTOP
PHONE
MOUSE
```

---

# 9. map() কী?

`map()` সাধারণত:

> Value mapping করার জন্য ব্যবহার হয়।

Example:

Gender:

Before:

```id="x8w4q1"
M
F
M
```

Need:

```id="z5k7p2"
Male
Female
Male
```

---

Code:

```python id="j4m8c6"
df["gender"].map(
{
"M":"Male",
"F":"Female"
}
)
```

---

# 10. map() দিয়ে Category Change

Example:

```python id="c3q9v5"
status_map = {

1:"Active",

0:"Inactive"

}


df["status"].map(
status_map
)
```

---

# 11. apply() vs map()

|                    | apply() | map()   |
| ------------------ | ------- | ------- |
| Function চালানো    | ✅       | Limited |
| Dictionary mapping | ❌       | ✅       |
| Complex logic      | ✅       | ❌       |
| Simple replace     | ❌       | ✅       |

---

# 12. Multiple Column Transformation

Example:

Discount:

Formula:

```
price - discount
```

```python id="r6n8p0"
df["final_price"] = (
df["price"]
-
df["price"]*0.1
)
```

---

# 13. Feature Engineering

Machine Learning এ খুব গুরুত্বপূর্ণ।

Raw:

```id="f3k7w9"
birth_year
```

Need:

```id="v8m2q5"
age
```

Formula:

```
current_year - birth_year
```

Code:

```python id="y2p6s8"
df["age"] = (
2026 -
df["birth_year"]
)
```

---

# 14. Date Feature Engineering

Data:

```id="n7c4k2"
created_at

2026-01-10
```

Extract:

Month:

```python id="w5j8x1"
df["month"] = (
df["created_at"]
.dt.month
)
```

---

Day:

```python id="q9m3z7"
df["day"] = (
df["created_at"]
.dt.day
)
```

---

# 15. Real E-commerce Example

Orders:

```id="a8c5r2"
order_id

amount

date
```

Need:

Revenue category:

```
amount > 5000

VIP


otherwise

Normal
```

Code:

```python id="b4v7n9"
df["customer_type"] = (
df["amount"]
.apply(
lambda x:
"VIP"
if x>5000
else
"Normal"
)
)
```

---

# 16. Vectorization vs apply()

Important:

এইটা:

```python id="e7r2m4"
df["price"]*10
```

Better than:

```python id="x9c5k1"
df["price"].apply(
lambda x:x*10
)
```

কারণ:

Vectorized operation অনেক fast।

---

# 17. Production Example

Data:

```
orders table
```

Columns:

```
price
quantity
discount
```

Create:

```python id="m5z8q3"
total_price =
(price*quantity)-discount
```

Code:

```python id="d2f7s9"
df["net_amount"] = (
df["price"]*
df["quantity"]
-
df["discount"]
)
```

---

# 18. Transformation Pipeline

Production style:

```python id="p8x4m6"
df = (
df
.assign(
total=lambda x:
x.price*x.quantity
)
.assign(
tax=lambda x:
x.total*0.15
)
)
```

---

# 19. Data Engineer Thinking

Beginner:

> "আমি column add করতে পারি"

Engineer:

> "আমি raw business data থেকে analytical dataset তৈরি করতে পারি"

---

# Lesson 9 Practice Task

Dataset:

```python id="k3m7q9"
data={

"product":[
"Laptop",
"Phone",
"Mouse"
],

"price":[
80000,
30000,
1000
],

"quantity":[
2,
5,
10
]

}
```

Tasks:

### 1.

`total_price` column তৈরি করুন।

Formula:

```
price * quantity
```

---

### 2.

`discount_price` তৈরি করুন।

Formula:

```
price - 10%
```

---

### 3.

`category` তৈরি করুন:

Rule:

```
price >= 50000

Premium


else

Normal
```

---

### 4.

সব product name uppercase করুন।

---

### 5. Data Engineer Challenge

একটি e-commerce order dataset তৈরি করুন:

Columns:

```
order_id

price

quantity

discount

date
```

Create:

```
total_amount

final_amount

month

order_category
```

---

পরের Lesson:

# Lesson 10: Sorting & Ranking Mastery

(`sort_values()`, `sort_index()`, ranking, top-N analysis, business reporting)


------
# Pandas Mastery Course — Lesson 10

# Sorting & Ranking Mastery

## `sort_values()`, `sort_index()`, Ranking, Top-N Analysis

আজকের lesson এ আমরা শিখবো কীভাবে data কে **order করা, ranking করা এবং business report তৈরি করা হয়।**

Data Engineer / Data Analyst হিসেবে প্রায়ই প্রশ্ন আসে:

* Top selling product কোনটি?
* Highest salary কার?
* Lowest price কোন product এর?
* Top 10 customer কে?
* Monthly sales ranking কী?

এসবের জন্য sorting এবং ranking ব্যবহার হয়।

---

# 1. Sample Dataset

```python
import pandas as pd


data = {

"product":[
"Laptop",
"Phone",
"Mouse",
"Keyboard",
"Monitor"
],

"category":[
"Electronics",
"Electronics",
"Accessory",
"Accessory",
"Electronics"
],

"price":[
80000,
30000,
1000,
3000,
25000
],

"sales":[
150,
300,
500,
200,
250
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
    product       price   sales

0   Laptop        80000    150

1   Phone         30000    300

2   Mouse          1000    500

3   Keyboard       3000    200

4   Monitor       25000    250
```

---

# 2. sort_values() কী?

`sort_values()` ব্যবহার হয়:

> কোনো column এর value অনুযায়ী DataFrame সাজানোর জন্য।

Syntax:

```python
df.sort_values(
    by="column_name"
)
```

---

# 3. Ascending Sorting

Default:

```python
df.sort_values(
    by="price"
)
```

Output:

```
Mouse       1000
Keyboard    3000
Monitor    25000
Phone      30000
Laptop     80000
```

ছোট থেকে বড়।

---

# 4. Descending Sorting

বড় থেকে ছোট:

```python
df.sort_values(
    by="price",
    ascending=False
)
```

Output:

```
Laptop     80000
Phone      30000
Monitor    25000
Keyboard   3000
Mouse      1000
```

---

# 5. Multiple Column Sorting

ধরি:

প্রথমে category,

তারপর price।

```python
df.sort_values(
    by=[
        "category",
        "price"
    ]
)
```

Logic:

```
category অনুযায়ী group

তারপর price অনুযায়ী sort
```

---

# 6. Different Sorting Order

Example:

category ascending

price descending

```python
df.sort_values(
    by=[
        "category",
        "price"
    ],
    ascending=[
        True,
        False
    ]
)
```

---

# 7. Original Data Change করা

Default:

```python
df.sort_values(
    by="price"
)
```

শুধু output change করে।

Permanent:

```python
df.sort_values(
    by="price",
    inplace=True
)
```

---

# 8. sort_index()

Index অনুযায়ী sort করে।

Example:

```python
df.sort_index()
```

Default:

```
0
1
2
3
4
```

---

Custom index:

```python
df.index=[
5,
2,
9,
1,
7
]
```

তারপর:

```python
df.sort_index()
```

Output:

```
1
2
5
7
9
```

---

# 9. Top N Data বের করা

Real analytics এ খুব common।

Question:

"Top 3 expensive product"

## Method 1: sort + head

```python
df.sort_values(
    by="price",
    ascending=False
).head(3)
```

Output:

```
Laptop
Phone
Monitor
```

---

# 10. nlargest()

আরও clean method:

```python
df.nlargest(
3,
"price"
)
```

Output:

```
Laptop
Phone
Monitor
```

---

# 11. nsmallest()

Lowest price:

```python
df.nsmallest(
3,
"price"
)
```

Output:

```
Mouse
Keyboard
Monitor
```

---

# 12. Ranking কী?

Ranking মানে:

কোন data কত নম্বরে আছে।

Example:

Sales:

```
Laptop     150
Phone      300
Mouse      500
```

Ranking:

```
Mouse      1
Phone      2
Laptop     3
```

---

# 13. rank() ব্যবহার

```python
df["sales_rank"] = (
    df["sales"]
    .rank(
        ascending=False
    )
)
```

Output:

```
product    sales    rank

Mouse       500      1

Phone       300      2

Monitor     250      3

Keyboard   200       4

Laptop     150       5
```

---

# 14. Ranking Method

Duplicate value থাকলে সমস্যা হয়।

Example:

```
Sales

500
500
300
```

Rank:

```python
df["sales"].rank()
```

---

## method="dense"

```python
df["rank"] = df["sales"].rank(
    method="dense"
)
```

Example:

```
500 → 1
500 → 1
300 → 2
```

---

# 15. Customer Ranking Example

E-commerce:

```
customer

total_purchase


Rahim     50000

Karim     90000

Hasan     30000
```

Top customer:

```python
df.nlargest(
5,
"total_purchase"
)
```

---

# 16. Group Wise Ranking

Real business case:

প্রতি department এর ভিতরে salary ranking।

Dataset:

```
name   department salary

Rahim  IT         60000

Hasan  IT         50000

Karim  HR         70000
```

Code:

```python
df["rank"] = (
df.groupby("department")
["salary"]
.rank(
ascending=False
)
)
```

Output:

```
Rahim IT 1

Hasan IT 2

Karim HR 1
```

---

# 17. Sort + Filter Combination

Question:

IT department এর highest salary:

```python
df[
df["department"]=="IT"
].sort_values(
    "salary",
    ascending=False
)
```

---

# 18. Real Data Engineer Example

আপনার e-commerce project:

Orders table:

```
order_id

customer

amount

date
```

Business asks:

"Top 10 highest order"

Solution:

```python
top_orders = df.nlargest(
10,
"amount"
)
```

---

"Top 5 customer":

```python
df.groupby(
"customer"
)["amount"]
.sum()
.sort_values(
ascending=False
)
.head(5)
```

---

# 19. Performance Tip

Large dataset:

```
50 million rows
```

Avoid:

```python
df.sort_values()
.head(10)
```

Better:

```python
df.nlargest(
10,
"column"
)
```

কারণ পুরো sort করার দরকার নেই।

---

# 20. Production Reporting Example

Daily sales report:

```python
report = (
df
.sort_values(
    "sales",
    ascending=False
)
.head(10)
)
```

Result:

```
Top 10 Products Report
```

---

# Lesson 10 Summary

আজ শিখলেন:

✅ `sort_values()`
✅ `sort_index()`
✅ Ascending / Descending sorting
✅ Multiple column sorting
✅ `nlargest()`
✅ `nsmallest()`
✅ Ranking
✅ Group ranking
✅ Business reporting

---

# Lesson 10 Practice Task

Dataset:

```python
data={

"employee":[
"A",
"B",
"C",
"D",
"E"
],

"department":[
"IT",
"HR",
"IT",
"Finance",
"HR"
],

"salary":[
50000,
70000,
60000,
80000,
40000
]

}
```

Tasks:

### 1.

Salary অনুযায়ী highest থেকে lowest sort করুন।

---

### 2.

Top 3 highest salary employee বের করুন।

---

### 3.

Salary ranking column তৈরি করুন।

---

### 4.

Department অনুযায়ী salary ranking তৈরি করুন।

---

### 5. Data Engineer Challenge

একটি e-commerce dataset তৈরি করুন:

Columns:

```
customer

product

amount

date
```

Find:

* Top 10 orders
* Top 5 customers
* Best selling products

---

পরের Lesson:

# Lesson 11: GroupBy Mastery

(SQL GROUP BY এর মতো — Aggregation, Multiple Grouping, Business Analytics)

# Pandas Mastery Course — Lesson 11

# GroupBy Mastery

## SQL GROUP BY, Aggregation, Multiple Grouping, Business Analytics

আজকের lesson Pandas এর সবচেয়ে powerful concept গুলোর একটি।

Data Engineer হিসেবে আপনাকে প্রায়ই এই ধরনের প্রশ্নের উত্তর দিতে হবে:

* কোন category সবচেয়ে বেশি sales করেছে?
* কোন customer সবচেয়ে বেশি purchase করেছে?
* Department অনুযায়ী average salary কত?
* Monthly revenue কত?
* City অনুযায়ী order count কত?

এসবের জন্য ব্যবহার হয়:

# `groupby()`

---

# 1. GroupBy কী?

সহজ ভাষায়:

> Similar data কে group করে তার উপর calculation করা।

SQL এ:

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

Pandas এ:

```python
df.groupby("department")["salary"].mean()
```

---

# 2. Sample Dataset

```python id="a8q2fd"
import pandas as pd


data = {

"employee":[
"Rahim",
"Karim",
"Hasan",
"Rafi",
"Sakib",
"Jony"
],

"department":[
"IT",
"HR",
"IT",
"Finance",
"HR",
"IT"
],

"salary":[
50000,
60000,
70000,
80000,
45000,
90000
],

"city":[
"Dhaka",
"Dhaka",
"Chittagong",
"Dhaka",
"Khulna",
"Dhaka"
]

}


df = pd.DataFrame(data)


print(df)
```

Output:

```
employee  department salary

Rahim       IT       50000

Karim       HR       60000

Hasan       IT       70000

Rafi        Finance  80000

Sakib       HR       45000

Jony        IT       90000
```

---

# 3. Basic GroupBy

Question:

## Department অনুযায়ী salary

```python id="9sh8k1"
df.groupby(
"department"
)["salary"].mean()
```

Output:

```
Finance     80000

HR          52500

IT          70000
```

---

Explanation:

Step 1:

```python
groupby("department")
```

মানে:

```
IT group

HR group

Finance group
```

Step 2:

```python
["salary"]
```

salary column select

Step 3:

```python
.mean()
```

average বের করা।

---

# 4. GroupBy Object বুঝা

```python id="p5n9k3"
group = df.groupby(
"department"
)


print(group)
```

Output:

```
<pandas.core.groupby...>
```

এটা নিজে data না।

এটা একটি grouped object।

---

# 5. Aggregation Functions

GroupBy এর সাথে সবচেয়ে বেশি ব্যবহার হয়:

| Function | Meaning        |
| -------- | -------------- |
| sum()    | Total          |
| mean()   | Average        |
| count()  | Count          |
| size()   | Number of rows |
| min()    | Minimum        |
| max()    | Maximum        |

---

# 6. Sum Example

Question:

Department wise total salary:

```python id="b9w4n7"
df.groupby(
"department"
)["salary"]
.sum()
```

Output:

```
Finance    80000

HR         105000

IT         210000
```

---

# 7. Count Example

Question:

কোন department এ কত employee?

```python id="j2m6x8"
df.groupby(
"department"
)["employee"]
.count()
```

Output:

```
Finance    1

HR         2

IT         3
```

---

# 8. Size ব্যবহার

```python id="g4k8z2"
df.groupby(
"department"
).size()
```

Output:

```
Finance    1

HR         2

IT         3
```

Difference:

`count()`

* null ignore করে

`size()`

* সব row count করে

---

# 9. Multiple Aggregation

Question:

Department salary:

* total
* average
* maximum

Code:

```python id="q7x2m4"
df.groupby(
"department"
)["salary"]
.agg(
[
"sum",
"mean",
"max"
]
)
```

Output:

```
department

Finance

sum     80000

mean    80000

max     80000
```

---

# 10. Named Aggregation

Production code এ ভালো:

```python id="m6p9v3"
df.groupby(
"department"
).agg(

total_salary=
("salary","sum"),

avg_salary=
("salary","mean")

)
```

Output:

```
department

IT

total_salary

avg_salary
```

---

# 11. Multiple Grouping

একাধিক column দিয়ে group করা যায়।

Question:

Department + City অনুযায়ী salary:

```python id="w5k7r1"
df.groupby(
[
"department",
"city"
]
)["salary"]
.mean()
```

Output:

```
IT Dhaka        70000

IT Chittagong   70000

HR Dhaka        60000
```

---

# 12. Reset Index

GroupBy এর result:

```python id="d3q8z5"
department
IT       70000
HR       52500
```

অনেক সময় DataFrame দরকার হয়।

```python id="r8v1k4"
result = (
df.groupby(
"department"
)["salary"]
.mean()
.reset_index()
)
```

Output:

```
department salary

IT          70000

HR          52500
```

---

# 13. Sorting After GroupBy

Question:

Highest average salary department:

```python id="q9s2j6"
(
df.groupby(
"department"
)["salary"]
.mean()
.sort_values(
ascending=False
)
)
```

Output:

```
IT        70000

Finance   80000

HR        52500
```

---

# 14. Filtering Groups

Question:

যে department এ employee 2 এর বেশি:

```python id="h7p4m8"
df.groupby(
"department"
).filter(
lambda x: len(x)>2
)
```

Output:

শুধু IT group থাকবে।

---

# 15. Transform ব্যবহার

Difference:

`agg()` group result দেয়।

`transform()` original size রাখে।

Example:

Department average salary বের করে প্রতিটি row তে বসানো:

```python id="n3q8w6"
df["dept_avg"] = (
df.groupby(
"department"
)["salary"]
.transform("mean")
)
```

Result:

```
employee salary dept_avg

Rahim    50000  70000

Hasan    70000  70000

Jony     90000  70000
```

---

# 16. Real E-commerce Example

Orders:

```
customer   amount

Rahim      500

Karim      700

Rahim      300
```

Customer total purchase:

```python id="t8m2q5"
df.groupby(
"customer"
)["amount"]
.sum()
```

Output:

```
Rahim    800

Karim    700
```

---

# 17. Monthly Sales Report

Data:

```
date          amount

2026-01-01    500

2026-01-02    700
```

First:

```python id="u7k9m2"
df["month"] = (
df["date"]
.dt.month
)
```

Then:

```python id="c6p4r8"
df.groupby(
"month"
)["amount"]
.sum()
```

---

# 18. SQL vs Pandas GroupBy

SQL:

```sql
SELECT city,
SUM(amount)
FROM orders
GROUP BY city;
```

Pandas:

```python
df.groupby(
"city"
)["amount"]
.sum()
```

---

# 19. Data Engineer Use Cases

### E-commerce

```
Customer → Total Spend
Product → Total Sales
Category → Revenue
```

### HR

```
Department → Avg Salary
City → Employee Count
```

### Finance

```
Month → Revenue
Year → Profit
```

---

# 20. Performance Tip

Large dataset:

```id="v5k2m9"
100 million rows
```

Better:

```python
df.groupby(
"category",
sort=False
)
```

কারণ sorting cost কমে।

---

# Lesson 11 Summary

আজ শিখলেন:

✅ `groupby()`
✅ Aggregation
✅ `sum()`
✅ `mean()`
✅ `count()`
✅ `agg()`
✅ Multiple grouping
✅ `reset_index()`
✅ `transform()`
✅ `filter()`
✅ SQL GROUP BY equivalent

---

# Lesson 11 Practice Task

Dataset:

```python id="f8m3q7"
data={

"customer":[
"A",
"B",
"A",
"C",
"B",
"A"
],

"product":[
"Laptop",
"Phone",
"Mouse",
"Laptop",
"Phone",
"Mouse"
],

"amount":[
80000,
30000,
1000,
90000,
40000,
2000
]

}
```

Tasks:

### 1.

Customer wise total purchase বের করুন।

---

### 2.

Product wise average sales বের করুন।

---

### 3.

Top customer কে বের করুন।

---

### 4.

Product অনুযায়ী:

* total sales
* max sales
* average sales

একসাথে বের করুন।

---

### 5. Data Engineer Challenge

আপনার e-commerce project এর জন্য sales report বানান:

Columns:

```
order_id
customer
product
category
amount
date
```

Generate:

* Daily revenue
* Monthly revenue
* Top customers
* Best selling products

---

পরের Lesson:

# Lesson 12: Pivot Table Mastery

(Excel Pivot Table + Business Reporting + Multi-dimensional Analysis)
# Pandas Mastery Course — Lesson 12

# Pivot Table Mastery

## Excel Pivot Table + Business Reporting + Multi-dimensional Analysis

আজ আমরা Pandas এর একটি খুব গুরুত্বপূর্ণ analytical tool শিখবো:

# `pivot_table()`

Data Engineer / Data Analyst হিসেবে যখন business team report চায়, তখন pivot table অনেক কাজে লাগে।

Example:

Manager প্রশ্ন করলো:

* কোন category সবচেয়ে বেশি revenue করেছে?
* কোন month এ sales বেশি?
* City অনুযায়ী product sales কত?
* Department অনুযায়ী average salary কত?

এই ধরনের report খুব দ্রুত তৈরি করা যায় `pivot_table()` দিয়ে।

---

# 1. Pivot Table কী?

সহজ ভাষায়:

> Multiple dimension অনুযায়ী data summarize করা।

SQL এ:

```sql
GROUP BY + Aggregation
```

Excel এ:

```
Insert → Pivot Table
```

Pandas এ:

```python
pd.pivot_table()
```

---

# 2. Sample Dataset

```python
import pandas as pd


data = {

"date":[
"2026-01-01",
"2026-01-02",
"2026-01-03",
"2026-02-01",
"2026-02-05",
"2026-02-10"
],


"city":[
"Dhaka",
"Dhaka",
"Chittagong",
"Dhaka",
"Khulna",
"Chittagong"
],


"category":[
"Laptop",
"Phone",
"Laptop",
"Phone",
"Mouse",
"Laptop"
],


"sales":[
80000,
30000,
90000,
40000,
5000,
70000
]

}


df = pd.DataFrame(data)


df
```

---

# 3. Basic Pivot Table

Question:

## Category অনুযায়ী total sales

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    aggfunc="sum"
)
```

Output:

```
category

Laptop      240000

Phone        70000

Mouse         5000
```

---

Explanation:

### values

যে column calculate করবো:

```python
values="sales"
```

---

### index

যার উপর group করবো:

```python
index="category"
```

---

### aggfunc

কী calculation হবে:

```python
sum
```

---

# 4. Different Aggregation

Average sales:

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    aggfunc="mean"
)
```

---

Maximum sales:

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    aggfunc="max"
)
```

---

# 5. Multiple Index

Question:

City + Category অনুযায়ী sales:

```python
pd.pivot_table(
    df,
    values="sales",
    index=[
        "city",
        "category"
    ],
    aggfunc="sum"
)
```

Output:

```
city          category

Dhaka         Laptop    80000

Dhaka         Phone     70000

Chittagong    Laptop   160000
```

---

# 6. Columns Parameter

Pivot table এর সবচেয়ে powerful feature।

Example:

City কে column বানাবো:

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    columns="city",
    aggfunc="sum"
)
```

Output:

```
              Dhaka     Khulna    Chittagong

Laptop        80000       NaN       160000

Phone         70000       NaN          NaN

Mouse           NaN      5000          NaN
```

---

এটা business report এর মতো দেখায়।

---

# 7. Fill Missing Values

উপরের output এ NaN আছে।

Fix:

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    columns="city",
    aggfunc="sum",
    fill_value=0
)
```

Output:

```
Laptop

Dhaka       80000

Khulna          0

Chittagong 160000
```

---

# 8. Multiple Aggregation

একসাথে:

* total sales
* average sales
* max sales

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    aggfunc=[
        "sum",
        "mean",
        "max"
    ]
)
```

Output:

```
category

Laptop

sum
mean
max
```

---

# 9. Margins ব্যবহার

Grand Total বের করতে:

```python
pd.pivot_table(
    df,
    values="sales",
    index="category",
    aggfunc="sum",
    margins=True
)
```

Output:

```
Laptop       240000

Phone         70000

Mouse          5000

All          315000
```

---

# 10. GroupBy vs Pivot Table

## GroupBy

```python
df.groupby(
"category"
)["sales"].sum()
```

Output:

```
Laptop 240000
Phone 70000
```

---

## Pivot Table

```python
pd.pivot_table(
df,
values="sales",
index="category",
aggfunc="sum"
)
```

Same result।

---

Difference:

| GroupBy                 | Pivot Table                     |
| ----------------------- | ------------------------------- |
| Developer friendly      | Business report friendly        |
| Flexible                | Excel style                     |
| Pipeline এ বেশি ব্যবহার | Dashboard/report এ বেশি ব্যবহার |

---

# 11. Real E-commerce Example

Orders table:

```
order_id

customer

category

amount

date
```

Question:

## Category wise monthly revenue

প্রথমে:

```python
df["month"] = (
pd.to_datetime(df["date"])
.dt.month
)
```

তারপর:

```python
pd.pivot_table(
df,
values="amount",
index="category",
columns="month",
aggfunc="sum",
fill_value=0
)
```

Output:

```
             Jan     Feb

Laptop      80000   160000

Phone       70000        0
```

---

# 12. Customer Purchase Report

Question:

প্রতি customer কোন category তে কত purchase করেছে?

```python
pd.pivot_table(
df,
values="amount",
index="customer",
columns="category",
aggfunc="sum",
fill_value=0
)
```

---

Output:

```
          Laptop Phone Mouse

Rahim      80000   0    2000

Karim          0 30000    0
```

---

# 13. Pivot Table with Count

Question:

প্রতি city তে কয়টি order?

```python
pd.pivot_table(
df,
index="city",
values="sales",
aggfunc="count"
)
```

---

# 14. Real Data Engineering Pipeline

Example:

Raw orders:

```
10 million rows
```

Transformation:

```
Raw Data

↓

Cleaning

↓

Create month column

↓

Pivot report

↓

Export Excel/dashboard
```

---

# 15. Export Pivot Report

Excel:

```python
report.to_excel(
"sales_report.xlsx"
)
```

CSV:

```python
report.to_csv(
"sales_report.csv"
)
```

---

# 16. Production Use Case

আপনার e-commerce backend থেকে data:

Orders:

```text
Order ID
Customer
Product
Category
Amount
Date
```

Management চাই:

```
Monthly Category Revenue Report
```

আপনি:

```python
pivot_table()
```

দিয়ে 5 মিনিটে report বানাতে পারবেন।

---

# Lesson 12 Summary

আজ শিখলেন:

✅ `pivot_table()`
✅ values
✅ index
✅ columns
✅ aggfunc
✅ fill_value
✅ margins
✅ Multiple aggregation
✅ Business reporting
✅ GroupBy vs Pivot Table

---

# Lesson 12 Practice Task

Dataset:

```python
data={

"customer":[
"Rahim",
"Karim",
"Rahim",
"Hasan",
"Karim"
],

"category":[
"Laptop",
"Phone",
"Mouse",
"Laptop",
"Phone"
],

"city":[
"Dhaka",
"Dhaka",
"Khulna",
"Dhaka",
"Chittagong"
],

"amount":[
80000,
30000,
1000,
90000,
40000
]

}
```

Tasks:

### 1.

Category wise total sales বের করুন।

---

### 2.

City + Category wise sales report তৈরি করুন।

---

### 3.

Customer vs Category purchase matrix তৈরি করুন।

---

### 4.

Grand total সহ report তৈরি করুন।

---

### 5. Data Engineer Challenge

আপনার e-commerce project এর জন্য তৈরি করুন:

**Sales Dashboard Dataset**

Report:

* Monthly revenue
* Category revenue
* City revenue
* Top customers
* Product performance

---

পরের Lesson:

# Lesson 13: Merge & Join Mastery

(SQL JOIN এর মতো — Combining Multiple Data Sources, Database Style Data Processing)
# Pandas Mastery Course — Lesson 13

# Merge & Join Mastery

## SQL JOIN, Multiple Data Sources Combine, Database Style Data Processing

আজকের lesson Data Engineer দের জন্য খুব গুরুত্বপূর্ণ।

বাস্তব জীবনে data কখনো একটি table এ থাকে না।

Example:

আপনার e-commerce system এ:

### customers table

| customer_id | name  | city       |
| ----------- | ----- | ---------- |
| 1           | Rahim | Dhaka      |
| 2           | Karim | Chittagong |

---

### orders table

| order_id | customer_id | amount |
| -------- | ----------- | ------ |
| 101      | 1           | 5000   |
| 102      | 2           | 7000   |

---

Question:

"Customer name সহ order report তৈরি করুন"

তাহলে দুইটা table combine করতে হবে।

এখানেই আসে:

# Merge / Join

---

# 1. SQL JOIN vs Pandas Merge

SQL:

```sql
SELECT *
FROM customers
JOIN orders
ON customers.customer_id =
orders.customer_id;
```

Pandas:

```python
pd.merge(
customers,
orders,
on="customer_id"
)
```

---

# 2. Sample Dataset

## Customers

```python id="4q0x8s"
import pandas as pd


customers = pd.DataFrame({

"customer_id":[
1,
2,
3
],

"name":[
"Rahim",
"Karim",
"Hasan"
],

"city":[
"Dhaka",
"Chittagong",
"Khulna"
]

})


customers
```

Output:

```
customer_id  name    city

1            Rahim   Dhaka

2            Karim   Chittagong

3            Hasan   Khulna
```

---

## Orders

```python id="1w9s6k"
orders = pd.DataFrame({

"order_id":[
101,
102,
103,
104
],

"customer_id":[
1,
2,
1,
4
],

"amount":[
5000,
7000,
3000,
9000
]

})


orders
```

Output:

```
order_id customer_id amount

101       1          5000

102       2          7000

103       1          3000

104       4          9000
```

---

# 3. Inner Join

সবচেয়ে common join।

Meaning:

> দুই table এ যে key দুটোর মধ্যে আছে শুধু সেগুলো রাখবে।

---

Code:

```python id="1j8d0x"
df = pd.merge(
customers,
orders,
on="customer_id",
how="inner"
)


df
```

Output:

```
customer_id name   city   order_id amount

1           Rahim  Dhaka   101     5000

2           Karim  Chittagong 102  7000

1           Rahim  Dhaka   103     3000
```

---

Notice:

Customer 4 নেই কারণ customers table এ নেই।

---

# 4. Left Join

Meaning:

> Left table এর সব data রাখবে।

Code:

```python id="5y9v3p"
pd.merge(
customers,
orders,
on="customer_id",
how="left"
)
```

Output:

```
customer_id name city order_id amount

1 Rahim Dhaka 101 5000

2 Karim Chittagong 102 7000

3 Hasan Khulna NaN NaN
```

---

Customer Hasan এর order নেই।

তবুও থাকবে।

---

# 5. Right Join

Right table এর সব data:

```python id="6m4s1q"
pd.merge(
customers,
orders,
on="customer_id",
how="right"
)
```

Output:

```
order 104

customer_id 4
```

এটাও থাকবে।

কারণ order table এ আছে।

---

# 6. Outer Join

সব data রাখবে।

Union এর মতো।

```python id="8v3m5x"
pd.merge(
customers,
orders,
on="customer_id",
how="outer"
)
```

Output:

```
customer_id

1

2

3

4
```

---

# 7. Merge Syntax

Basic:

```python id="6p8y2d"
pd.merge(
df1,
df2,
on="column"
)
```

---

Different column name হলে:

Customers:

```text
id
```

Orders:

```text
customer_id
```

Code:

```python id="1d6v0p"
pd.merge(

customers,

orders,

left_on="id",

right_on="customer_id"

)
```

---

# 8. Multiple Column Join

Example:

Sales:

```
product_id
store_id
```

Inventory:

```
product_id
store_id
```

Code:

```python id="x7k3q9"
pd.merge(
sales,
inventory,
on=[
"product_id",
"store_id"
]
)
```

---

# 9. Suffix ব্যবহার

দুই table এ একই column থাকলে:

Customers:

```
name
```

Orders:

```
name
```

Problem:

duplicate column

Solution:

```python id="g4x9m2"
pd.merge(

customers,

orders,

on="customer_id",

suffixes=(
"_customer",
"_order"
)

)
```

---

# 10. concat() কী?

Merge:

> Column এর মাধ্যমে combine

Concat:

> Row বা column append

---

# 11. Row Concatenation

January sales:

```python id="8k1m3v"
jan = pd.DataFrame({

"sales":[100,200]

})
```

February:

```python id="7c5q8h"
feb = pd.DataFrame({

"sales":[300,400]

})
```

Combine:

```python id="4j7p2m"
pd.concat(
[
jan,
feb
]
)
```

Output:

```
100

200

300

400
```

---

# 12. Column Concatenation

```python id="8m2f7v"
pd.concat(
[
df1,
df2
],
axis=1
)
```

`axis=1`

মানে:

column wise combine।

---

# 13. Merge vs Join vs Concat

| Method   | Use              |
| -------- | ---------------- |
| merge()  | SQL JOIN         |
| join()   | Index based join |
| concat() | Append data      |

---

# 14. Real E-commerce Example

আপনার project এ:

## Product Table

```
product_id

name

category
```

## Order Table

```
order_id

product_id

quantity
```

Report:

```
Order ID
Product Name
Category
Quantity
```

Solution:

```python id="u5p8z3"
report = pd.merge(

orders,

products,

on="product_id",

how="inner"

)
```

---

# 15. Multiple Data Source Pipeline

Real Data Engineer workflow:

```
CRM Database

      |

      ↓

Customer Data


      +

      
Order Database

      |

      ↓

Merge


      |

      ↓

Analytics Table

```

---

# 16. Performance Tips

Large dataset:

```text
100 million rows
```

Avoid unnecessary columns:

Bad:

```python
pd.merge(
df1,
df2
)
```

Better:

```python
pd.merge(

df1[
["id","amount"]
],

df2[
["id","name"]
],

on="id"

)
```

শুধু দরকারি column নিন।

---

# 17. Data Engineer Mindset

Beginner:

> "আমি দুইটা dataframe merge করতে পারি"

Engineer:

> "আমি multiple data source combine করে analytical dataset তৈরি করতে পারি"

---

# Lesson 13 Summary

আজ শিখলেন:

✅ `merge()`
✅ Inner Join
✅ Left Join
✅ Right Join
✅ Outer Join
✅ Multiple key join
✅ Different column join
✅ `concat()`
✅ Data warehouse style combining

---

# Lesson 13 Practice Task

Create:

## Customers

```python
customer_id
name
city
```

## Orders

```python
order_id
customer_id
amount
```

Tasks:

### 1.

Inner join করুন।

---

### 2.

সব customer সহ order report তৈরি করুন।

(Hint: left join)

---

### 3.

সব order সহ customer report তৈরি করুন।

(Hint: right join)

---

### 4.

January এবং February sales concatenate করুন।

---

### 5. Data Engineer Challenge

আপনার e-commerce system এর জন্য:

Tables:

```
Users

Products

Orders

Payments

Reviews
```

Pandas দিয়ে একটি final analytics dataframe তৈরি করুন:

```
Customer Name

Product Name

Order Amount

Payment Status

Review Rating
```

---

পরের Lesson:

# Lesson 14: Advanced Data Reshaping

(`melt()`, `stack()`, `unstack()`, Wide vs Long Data, Analytics Data Modeling)


----
# Pandas Mastery Course — Lesson 14

# Advanced Data Reshaping

## `melt()`, `stack()`, `unstack()`, Wide vs Long Data, Analytics Data Modeling

আজকের lesson Data Engineering এবং Analytics এর জন্য খুব গুরুত্বপূর্ণ।

অনেক সময় data আমাদের প্রয়োজন অনুযায়ী format এ থাকে না।

Example:

একটি sales report:

## Wide Format

| Product | Jan | Feb | Mar |
| ------- | --- | --- | --- |
| Laptop  | 100 | 200 | 300 |
| Phone   | 50  | 80  | 120 |

কিন্তু অনেক analytics tool বা database এই format পছন্দ করে:

## Long Format

| Product | Month | Sales |
| ------- | ----- | ----- |
| Laptop  | Jan   | 100   |
| Laptop  | Feb   | 200   |
| Laptop  | Mar   | 300   |

এই format change করার জন্য ব্যবহার হয়:

* `melt()`
* `stack()`
* `unstack()`

---

# 1. Wide vs Long Data

## Wide Data

একটি row তে অনেক information:

```id="7m9p2x"
Product | Jan | Feb | Mar
```

Advantages:

* Human readable
* Excel report এর জন্য ভালো

Problems:

* Machine learning এ অনেক সময় সমস্যা করে
* Database normalization এর জন্য ভালো না

---

## Long Data

প্রতিটি observation আলাদা row:

```id="4z1q8m"
Product | Month | Sales
```

Advantages:

* Analytics friendly
* SQL friendly
* Visualization friendly

---

# 2. Sample Wide Dataset

```python id="p3k8w1"
import pandas as pd


df = pd.DataFrame({

"product":[
"Laptop",
"Phone",
"Mouse"
],

"Jan":[
100,
50,
30
],

"Feb":[
200,
80,
40
],

"Mar":[
300,
120,
60
]

})


df
```

Output:

```
product   Jan   Feb   Mar

Laptop    100   200   300

Phone      50    80   120

Mouse      30    40    60
```

---

# 3. melt() কী?

`melt()` ব্যবহার হয়:

> Wide data কে Long data তে convert করার জন্য।

Syntax:

```python
pd.melt(
    dataframe,
    id_vars=[],
    value_vars=[]
)
```

---

# 4. Basic melt()

```python id="n8x3p5"
long_df = pd.melt(
    df,
    id_vars=[
        "product"
    ]
)


long_df
```

Output:

```
product   variable   value

Laptop    Jan        100

Laptop    Feb        200

Laptop    Mar        300
```

---

এখানে:

`product`

থাকছে fixed।

`Jan, Feb, Mar`

হয়ে গেছে row।

---

# 5. Column Name Customize করা

Default:

```id="y2k5m8"
variable

value
```

এগুলো change করতে পারি।

```python id="v7r3q9"
long_df = pd.melt(

df,

id_vars=[
"product"
],

var_name="month",

value_name="sales"

)
```

Output:

```
product   month   sales

Laptop    Jan     100

Laptop    Feb     200
```

---

# 6. Real Business Example

আগে:

Sales Report:

```
Product Jan Feb Mar
```

Need:

```
Product Month Revenue
```

Code:

```python id="u9h4k2"
sales = pd.melt(

df,

id_vars="product",

var_name="month",

value_name="revenue"

)
```

---

# 7. value_vars ব্যবহার

শুধু কিছু column convert করতে চাই:

```python id="s5d7m1"
pd.melt(

df,

id_vars="product",

value_vars=[
"Jan",
"Feb"
]

)
```

Output:

শুধু Jan এবং Feb আসবে।

---

# 8. stack() কী?

`stack()`:

> Column কে row index এ নিয়ে যায়।

Example:

```python id="r4m8z2"
df_stack = df.set_index(
"product"
).stack()


df_stack
```

Output:

```
product

Laptop Jan 100

Laptop Feb 200

Phone Jan 50
```

---

# 9. unstack()

`unstack()`:

> stack করা data আবার column এ ফেরত আনে।

Example:

```python id="q7m1x9"
df_stack.unstack()
```

আগের wide format ফিরে আসবে।

---

# 10. stack vs melt

|                   | melt      | stack  |
| ----------------- | --------- | ------ |
| Output            | DataFrame | Series |
| Index use         | না        | হ্যাঁ  |
| Beginner friendly | ✅         | Medium |
| Analytics         | ✅         | ✅      |

---

# 11. Pivot এবং Melt এর সম্পর্ক

মনে রাখবেন:

Wide:

```
Product Jan Feb
```

Convert:

```
melt()
```

↓

Long:

```
Product Month Sales
```

Reverse:

```
pivot_table()
```

↓

Wide

---

# 12. Example: melt + pivot

Wide:

```id="x8k5n3"
Product Jan Feb
```

Long:

```python id="w5p9d1"
long_df = pd.melt(
df,
id_vars="product"
)
```

আবার Wide:

```python id="c4r7m2"
long_df.pivot(
index="product",
columns="variable",
values="value"
)
```

---

# 13. MultiIndex Data Reshaping

Example:

```python id="m2q8v5"
df.groupby(
[
"city",
"category"
]
)["sales"].sum()
```

Output:

```
city       category

Dhaka      Laptop       10000

Dhaka      Phone         5000
```

এটা MultiIndex।

---

# 14. unstack() দিয়ে Report

```python id="j9w3k6"
report = (
df.groupby(
[
"city",
"category"
]
)["sales"]
.sum()
.unstack()
)
```

Output:

```
category    Laptop   Phone

Dhaka        10000    5000
```

---

# 15. Real Data Engineering Use Case

আপনার e-commerce analytics pipeline:

Raw Sales:

```
customer
product
month
amount
```

Business Dashboard চায়:

```
          Jan Feb Mar

Laptop    10  20  30

Phone     5   8   12
```

আপনি:

```python id="f5v8z2"
pivot_table()
```

দিয়ে তৈরি করবেন।

---

# 16. Machine Learning Example

ML dataset:

Wrong:

```
Jan Feb Mar
100 200 300
```

Better:

```
month sales
Jan   100
Feb   200
Mar   300
```

কারণ:

Models সাধারণত structured long format পছন্দ করে।

---

# 17. Data Warehouse Perspective

ETL Pipeline:

```
Source Database

        ↓

Raw Wide Data

        ↓

Transformation

        ↓

Long Analytical Table

        ↓

BI Dashboard / ML
```

---

# 18. Production Tips

### Dashboard এর জন্য:

Use:

```
pivot_table()
```

---

### ML / Analytics এর জন্য:

Use:

```
melt()
```

---

### Complex index data:

Use:

```
stack()
unstack()
```

---

# Lesson 14 Summary

আজ শিখলেন:

✅ Wide Data
✅ Long Data
✅ `melt()`
✅ `stack()`
✅ `unstack()`
✅ Data reshaping
✅ Analytics data modeling
✅ Pivot ↔ Melt relationship

---

# Lesson 14 Practice Task

Dataset:

```python
data={

"product":[
"Laptop",
"Phone",
"Mouse"
],

"Jan":[
100,
200,
300
],

"Feb":[
150,
250,
350
],

"Mar":[
200,
300,
400
]

}
```

Tasks:

### 1.

Wide → Long করুন।

Output:

```
product month sales
```

---

### 2.

Long data থেকে আবার Wide format তৈরি করুন।

---

### 3.

`stack()` ব্যবহার করে reshape করুন।

---

### 4.

একটি e-commerce sales report কে dashboard-friendly format এ convert করুন।

---

পরের Lesson:

# Lesson 15: Time Series Data Mastery

(`datetime`, date filtering, resampling, rolling window, sales trend analysis)
# Pandas Mastery Course — Lesson 15

# Time Series Data Mastery

## `datetime`, Date Filtering, Resampling, Rolling Window, Trend Analysis

আজকের lesson Data Engineer এবং Data Analyst দুইজনের জন্য খুব গুরুত্বপূর্ণ।

কারণ real-world data এর বড় অংশ:

* Transaction data
* Sensor data
* Logs
* User activity
* Sales data

সবই **time-based data**।

Example:

E-commerce:

| order_date | amount |
| ---------- | ------ |
| 2026-01-01 | 5000   |
| 2026-01-02 | 7000   |

আজ শিখবো:

* Date কে datetime এ convert করা
* Year / Month / Day বের করা
* Date filtering
* Time indexing
* Resampling
* Rolling calculation
* Trend analysis

---

# 1. Time Series Data কী?

যে data এর সাথে সময় যুক্ত থাকে তাকে Time Series data বলে।

Example:

```id="x9h3m2"
2026-01-01 10:30:00
2026-01-01 10:31:00
2026-01-01 10:32:00
```

---

# 2. Sample Dataset

```python id="8m4q1v"
import pandas as pd


data = {

"date":[
"2026-01-01",
"2026-01-05",
"2026-02-01",
"2026-02-10",
"2026-03-01"
],

"sales":[
5000,
7000,
6000,
9000,
10000
]

}


df = pd.DataFrame(data)


df
```

Output:

```id="1n7x4m"
date          sales

2026-01-01    5000

2026-01-05    7000

2026-02-01    6000

2026-02-10    9000

2026-03-01    10000
```

---

# 3. Date Column এর সমস্যা

Check:

```python id="2j9w6q"
df.dtypes
```

Output:

```id="8w3m7p"
date      object

sales     int64
```

Problem:

Date এখনো string।

আমরা date operation করতে পারবো না।

---

# 4. Convert String to Datetime

```python id="v8k2p5"
df["date"] = pd.to_datetime(
    df["date"]
)
```

Check:

```python id="h5z9q1"
df.dtypes
```

Output:

```id="q7m3v8"
date      datetime64

sales     int64
```

---

# 5. Datetime থেকে Year বের করা

```python id="w6p2x9"
df["year"] = (
    df["date"]
    .dt.year
)
```

Output:

```id="m3n8q5"
2026
2026
2026
```

---

# 6. Month বের করা

```python id="k9x4s2"
df["month"] = (
    df["date"]
    .dt.month
)
```

Output:

```id="4v7m2p"
1
1
2
2
3
```

---

# 7. Month Name

```python id="q5n8x3"
df["month_name"] = (
    df["date"]
    .dt.month_name()
)
```

Output:

```id="6m1q9z"
January

January

February
```

---

# 8. Day বের করা

```python id="r3p7m8"
df["day"] = (
    df["date"]
    .dt.day
)
```

---

# 9. Day of Week

```python id="s8q2m4"
df["weekday"] = (
    df["date"]
    .dt.day_name()
)
```

Output:

```id="y7v5k1"
Thursday

Monday
```

---

# 10. Date Filtering

Question:

শুধু January এর data চাই।

Method 1:

```python id="g2m8p4"
df[
df["date"].dt.month == 1
]
```

Output:

January sales।

---

# 11. Date Range Filtering

Question:

January 1 থেকে February 1 পর্যন্ত:

```python id="z4x8m6"
df[
(df["date"] >= "2026-01-01")
&
(df["date"] <= "2026-02-01")
]
```

---

# 12. Between ব্যবহার

```python id="n6q3v9"
df[
df["date"].between(
"2026-01-01",
"2026-02-01"
)
]
```

Clean syntax।

---

# 13. Datetime Index তৈরি করা

Time series analysis এর জন্য:

```python id="m8x2q5"
df = df.set_index(
"date"
)
```

এখন:

```
date
 |
2026-01-01
2026-01-05
```

---

# 14. Resampling কী?

Resampling মানে:

> Time frequency change করা।

Example:

Daily sales:

```
Jan 1 500
Jan 2 700
Jan 3 900
```

Convert:

Monthly sales:

```
January 2100
```

---

# 15. Monthly Sales

```python id="k5m9q2"
monthly_sales = (
df["sales"]
.resample("M")
.sum()
)
```

Output:

```
January     12000

February    15000

March       10000
```

---

# 16. Common Frequency

| Code | Meaning   |
| ---- | --------- |
| D    | Daily     |
| W    | Weekly    |
| M    | Monthly   |
| Q    | Quarterly |
| Y    | Yearly    |
| H    | Hourly    |

---

# 17. Weekly Sales

```python id="p4v8m1"
df["sales"]
.resample("W")
.sum()
```

---

# 18. Rolling Window

Rolling মানে:

> চলমান average/calculation

Example:

Sales:

```
100
200
300
400
```

3-day moving average:

```
-
-
200
300
```

---

# 19. Rolling Mean

```python id="x8m3q7"
df["sales"]
.rolling(
3
)
.mean()
```

Meaning:

প্রতি 3টা data নিয়ে average।

---

# 20. Real Business Example

Daily revenue:

| date | revenue |
| ---- | ------- |
| Jan1 | 5000    |
| Jan2 | 7000    |
| Jan3 | 9000    |

7-day moving average:

```python id="z6q1m9"
df["7_day_avg"] = (
df["revenue"]
.rolling(7)
.mean()
)
```

---

# 21. Growth Calculation

Sales growth:

```python id="c7m2x8"
df["growth"] = (
df["sales"]
.pct_change()
)
```

Output:

```
NaN

40%

-14%
```

---

# 22. Shift ব্যবহার

Previous day sales:

```python id="n9p4x6"
df["previous_sales"] = (
df["sales"]
.shift(1)
)
```

Example:

| sales | previous |
| ----- | -------- |
| 5000  | NaN      |
| 7000  | 5000     |

---

# 23. Real E-commerce Analytics

Orders table:

```
order_id
customer
amount
created_at
```

Monthly Revenue:

```python id="b5m7q9"
(
df
.set_index("created_at")
["amount"]
.resample("M")
.sum()
)
```

---

# 24. Data Engineer Pipeline

Real workflow:

```
Database

   ↓

Load Data

   ↓

Convert datetime

   ↓

Create features

   ↓

Resample

   ↓

Analytics table

   ↓

Dashboard
```

---

# 25. Time Series Feature Engineering

Machine Learning এর জন্য:

From:

```
2026-07-13
```

Create:

```
year
month
day
weekday
week_number
quarter
```

Code:

```python id="u8m2p6"
df["quarter"] = (
df["date"]
.dt.quarter
)
```

---

# Lesson 15 Summary

আজ শিখলেন:

✅ `pd.to_datetime()`
✅ datetime accessor `.dt`
✅ Date filtering
✅ Datetime index
✅ `resample()`
✅ Rolling window
✅ `shift()`
✅ `pct_change()`
✅ Time series feature engineering

---

# Lesson 15 Practice Task

Dataset:

```python id="s7m4q8"
data={

"date":[
"2026-01-01",
"2026-01-02",
"2026-01-03",
"2026-02-01",
"2026-02-05"
],

"revenue":[
1000,
2000,
3000,
4000,
5000
]

}
```

Tasks:

### 1.

Date column datetime করুন।

---

### 2.

Year, Month, Day column তৈরি করুন।

---

### 3.

January মাসের revenue বের করুন।

---

### 4.

Monthly revenue report তৈরি করুন।

---

### 5.

3-day rolling average তৈরি করুন।

---

### 6. Data Engineer Challenge

আপনার e-commerce project এর জন্য তৈরি করুন:

**Sales Trend Pipeline**

Output:

```
Daily Sales

Monthly Revenue

7 Day Moving Average

Growth Rate
```

---

পরের Lesson:

# Lesson 16: Advanced Pandas Performance Optimization

(Memory Optimization, Vectorization, Efficient Processing, Large Dataset Handling)
# Pandas Mastery Course — Lesson 16

# Advanced Pandas Performance Optimization

## Memory Optimization, Vectorization, Efficient Processing, Large Dataset Handling

আজকের lesson থেকে আমরা beginner Pandas থেকে **production-level Pandas** এ যাবো।

বাস্তব Data Engineering এ data ছোট হয় না।

Example:

* E-commerce orders → 50 million rows
* User logs → 500 million rows
* Sensor data → billions of records

তখন শুধু Pandas syntax জানলেই হবে না।

জানতে হবে:

* কোন operation fast?
* Memory কিভাবে কমাবো?
* Slow code কিভাবে optimize করবো?

---

# 1. Pandas Performance Problem কেন হয়?

Example:

```python
import pandas as pd

df = pd.read_csv(
    "large_file.csv"
)
```

একটি CSV:

```
5 GB
```

Load করতে গেলে:

```
RAM overflow
```

হতে পারে।

---

# 2. Check Dataset Size

Dataset:

```python
df.shape
```

Output:

```
(10000000, 20)
```

মানে:

```
10 million rows
20 columns
```

---

Memory check:

```python
df.info()
```

Output:

```
memory usage: 2GB
```

---

# 3. Memory Optimization

## Problem

Default Pandas অনেক বড় datatype নেয়।

Example:

Integer:

```text
int64
```

কিন্তু data:

```
0 - 100
```

হলে int8 যথেষ্ট।

---

# 4. Downcasting

Before:

```python
df["age"].dtype
```

Output:

```
int64
```

Convert:

```python
df["age"] = (
    pd.to_numeric(
        df["age"],
        downcast="integer"
    )
)
```

Now:

```
int8
```

---

# 5. Float Optimization

Before:

```
float64
```

After:

```python
df["price"] = (
pd.to_numeric(
df["price"],
downcast="float"
)
)
```

Result:

```
float32
```

---

# 6. Category Data Type

একটি column:

```
country
```

Values:

```
Bangladesh
India
USA
```

Repeated data।

Default:

```
object
```

Convert:

```python
df["country"] = (
df["country"]
.astype("category")
)
```

---

Memory difference:

Before:

```
500 MB
```

After:

```
50 MB
```

হতে পারে।

---

# 7. Object কেন Slow?

Example:

```python
df["city"]
```

dtype:

```
object
```

Pandas প্রতিটি string আলাদা Python object হিসেবে রাখে।

Slow + বেশি memory।

---

Category:

```
unique value dictionary
```

ব্যবহার করে।

---

# 8. Vectorization

সবচেয়ে গুরুত্বপূর্ণ optimization।

---

## Slow Way

```python
for i in range(len(df)):

    df.loc[i,"total"] = (
        df.loc[i,"price"] *
        df.loc[i,"quantity"]
    )
```

Problem:

* Python loop
* খুব slow

---

# 9. Fast Way

Vectorized:

```python
df["total"] = (
df["price"]
*
df["quantity"]
)
```

এটা অনেক fast।

---

# 10. apply() কেন Slow?

Example:

```python
df["price"]
.apply(
lambda x:x*2
)
```

এটা Python function call করে।

---

Better:

```python
df["price"]*2
```

---

Rule:

যেখানে সম্ভব:

```
Vectorization > apply() > loop
```

---

# 11. Query Optimization

Slow:

```python
df[
(df["age"]>25)
&
(df["city"]=="Dhaka")
]
```

Works।

কিন্তু বড় data তে:

```python
df.query(
"age > 25 and city == 'Dhaka'"
)
```

আরও readable।

---

# 12. Read Only Required Columns

Problem:

CSV:

```
50 columns
```

আপনার দরকার:

```
5 columns
```

Bad:

```python
df=pd.read_csv(
"data.csv"
)
```

Good:

```python
df=pd.read_csv(
"data.csv",
usecols=[
"id",
"price",
"date"
]
)
```

---

# 13. Chunk Processing

Large CSV:

```
20GB CSV
```

RAM:

```
8GB
```

Solution:

chunksize

```python
for chunk in pd.read_csv(
    "large.csv",
    chunksize=100000
):

    process(chunk)
```

---

Meaning:

একবারে সব load না করে:

```
100k rows
+
100k rows
+
100k rows
```

---

# 14. Example Chunk Aggregation

Total sales:

```python
total = 0


for chunk in pd.read_csv(
"orders.csv",
chunksize=50000
):

    total += (
        chunk["amount"]
        .sum()
    )
```

---

# 15. Avoid Copying Data

Problem:

```python
df2=df.copy()
```

Large data হলে:

Memory double।

---

Use:

```python
df2=df[["column1","column2"]]
```

---

# 16. inplace নিয়ে সতর্কতা

অনেকে করে:

```python
df.drop(
"column",
inplace=True
)
```

সবসময় faster না।

Modern Pandas এ difference অনেক কম।

Readable code বেশি important।

---

# 17. Index Optimization

Searching:

```python
df[
df["customer_id"]==100
]
```

বারবার করলে:

Index:

```python
df.set_index(
"customer_id",
inplace=True
)
```

তারপর:

```python
df.loc[100]
```

Fast।

---

# 18. Sorting Optimization

Bad:

```python
df.sort_values(
"date"
)
.head(10)
```

Better:

```python
df.nlargest(
10,
"amount"
)
```

কারণ পুরো sort লাগে না।

---

# 19. Memory Usage Compare

Check:

```python
df.memory_usage()
```

Total:

```python
df.memory_usage(
deep=True
).sum()
```

---

# 20. Large Dataset Strategy

Million rows:

```
Pandas OK
```

Hundred million:

```
Optimize Pandas
```

Billion rows:

```
Spark / Polars / DuckDB
```

---

# 21. Data Engineer Production Pipeline

Example:

E-commerce:

```
orders.csv

500 million rows
```

Pipeline:

```
Read chunks

↓

Clean data

↓

Optimize dtype

↓

Transform

↓

Aggregate

↓

Save result

```

---

# 22. Pandas vs Alternatives

| Tool   | Use Case                   |
| ------ | -------------------------- |
| Pandas | Small-Medium data          |
| Polars | High performance dataframe |
| DuckDB | SQL analytics              |
| Spark  | Big Data                   |
| Dask   | Distributed Pandas         |

---

# 23. Performance Golden Rules

সবসময় মনে রাখবেন:

### Rule 1

Avoid loops

```
Vectorization first
```

---

### Rule 2

Avoid unnecessary columns

```
select only needed data
```

---

### Rule 3

Optimize dtype

```
int64 → int8
object → category
```

---

### Rule 4

Process large files in chunks

```
chunksize
```

---

# Lesson 16 Summary

আজ শিখলেন:

✅ Memory optimization
✅ dtype optimization
✅ Category datatype
✅ Vectorization
✅ apply vs vectorization
✅ Chunk processing
✅ Large CSV handling
✅ Index optimization
✅ Production performance mindset

---

# Lesson 16 Practice Task

একটি dataset:

```python
data={

"id":[1,2,3,4],

"city":[
"Dhaka",
"Dhaka",
"Dhaka",
"Chittagong"
],

"price":[100,200,300,400],

"quantity":[2,3,4,5]

}
```

Tasks:

### 1.

Memory usage check করুন।

---

### 2.

City column কে category করুন।

---

### 3.

Vectorized ভাবে total price তৈরি করুন।

Formula:

```
price * quantity
```

---

### 4.

একটি বড় CSV chunk করে পড়ার code লিখুন।

---

### 5. Data Engineer Challenge

ধরুন:

```
orders.csv

100 million rows
```

Columns:

```
order_id
customer_id
product_id
amount
date
```

একটি optimized processing strategy লিখুন:

* কোন column load করবেন?
* কোন dtype ব্যবহার করবেন?
* chunk কিভাবে করবেন?
* final analytics table কিভাবে তৈরি করবেন?

---

পরের Lesson:

# Lesson 17: Pandas Data Cleaning Mastery

(Missing Values, Duplicates, Outliers, Data Quality Pipeline)
# Pandas Mastery Course — Lesson 17

# Pandas Data Cleaning Mastery

## Missing Values, Duplicates, Outliers, Data Quality Pipeline

আজকের lesson Data Engineer এর জন্য সবচেয়ে গুরুত্বপূর্ণ অংশগুলোর একটি।

বাস্তব data কখনো clean থাকে না।

Database থেকে আসা data তে থাকে:

* Missing value
* Duplicate row
* Wrong format
* Invalid data
* Outlier
* Inconsistent text

একজন Data Engineer এর কাজ:

> Raw data কে reliable, trustworthy dataset এ convert করা।

---

# 1. Data Cleaning Pipeline

Real production pipeline:

```
Raw Data

   ↓

Inspect Data

   ↓

Handle Missing Values

   ↓

Remove Duplicates

   ↓

Fix Data Types

   ↓

Handle Outliers

   ↓

Clean Dataset

   ↓

Analytics / ML
```

---

# 2. Sample Dirty Dataset

```python id="8j2m5p"
import pandas as pd
import numpy as np


data = {

"name":[
"Rahim",
"Karim",
"Rahim",
None,
"Hasan"
],

"age":[
25,
30,
25,
None,
200
],

"salary":[
50000,
60000,
50000,
70000,
None
]

}


df = pd.DataFrame(data)


df
```

Output:

```
name      age     salary

Rahim     25      50000

Karim     30      60000

Rahim     25      50000

None      NaN     70000

Hasan     200     NaN
```

---

# 3. Data Inspection

## Shape

```python
df.shape
```

Output:

```
(5,3)
```

---

## Information

```python
df.info()
```

দেখাবে:

* datatype
* missing value
* memory

---

## Statistical Summary

```python
df.describe()
```

Output:

```
age

mean
min
max
```

---

# 4. Missing Values কী?

Missing value:

```
NaN
None
Null
```

Example:

```
name

Rahim

Karim

NaN
```

---

# 5. Missing Value Detect করা

## Single column

```python
df["age"].isnull()
```

Output:

```
False
False
False
True
False
```

---

## Total Missing

```python
df.isnull().sum()
```

Output:

```
name      1

age       1

salary    1
```

---

# 6. Missing Percentage

Production এ দরকার:

```python
(
df.isnull().sum()
/
len(df)
)*100
```

Output:

```
name      20%

age       20%

salary    20%
```

---

# 7. Missing Value Remove করা

## Drop rows

```python
df.dropna()
```

যে row এ missing আছে remove হবে।

Before:

```
5 rows
```

After:

```
2 rows
```

---

# 8. Drop Specific Column

যে column এ অনেক missing:

```python
df.dropna(
axis=1
)
```

---

# 9. Missing Value Fill করা

সবচেয়ে common method:

## Mean দিয়ে fill

```python
df["age"].fillna(
df["age"].mean()
)
```

---

Example:

Age:

```
25
30
NaN
```

Mean:

```
27.5
```

Result:

```
25
30
27.5
```

---

# 10. Median দিয়ে Fill

Outlier থাকলে mean risky।

```python
df["age"].fillna(
df["age"].median()
)
```

---

# 11. Mode দিয়ে Fill

Categorical data:

```python
df["city"].fillna(
df["city"].mode()[0]
)
```

---

# 12. Forward Fill

আগের value দিয়ে fill:

```python
df.fillna(
method="ffill"
)
```

Example:

```
100

NaN

NaN
```

Result:

```
100

100

100
```

---

# 13. Backward Fill

```python
df.fillna(
method="bfill"
)
```

পরের value ব্যবহার করে।

---

# 14. Duplicate Data

Duplicate মানে:

একই row একাধিকবার আছে।

Check:

```python
df.duplicated()
```

Output:

```
False

False

True
```

---

# 15. Duplicate Count

```python
df.duplicated().sum()
```

---

# 16. Duplicate Remove

```python
df.drop_duplicates()
```

---

# 17. Specific Column Duplicate

Customer duplicate:

```python
df.drop_duplicates(
subset=[
"email"
]
)
```

---

# 18. Keep Option

Default:

```python
keep="first"
```

Example:

```
A

A

A
```

First রাখবে।

---

Last রাখতে:

```python
df.drop_duplicates(
keep="last"
)
```

---

# 19. Data Type Cleaning

Example:

Price:

```
"5000"
"7000"
```

এগুলো string।

Check:

```python
df.dtypes
```

Convert:

```python
df["price"] = pd.to_numeric(
df["price"]
)
```

---

# 20. String Cleaning

Example:

```
" Dhaka "
"dhaka"
```

Problem:

Different value মনে হবে।

Remove space:

```python
df["city"] = (
df["city"]
.str.strip()
)
```

Lowercase:

```python
df["city"] = (
df["city"]
.str.lower()
)
```

---

# 21. Outlier কী?

যে value normal range এর বাইরে।

Example:

Age:

```
25
30
28
200
```

200 suspicious।

---

# 22. Detect Outlier

## Describe

```python
df["age"].describe()
```

Check:

```
max
min
```

---

# 23. IQR Method

Most common statistical method।

Formula:

```
IQR = Q3 - Q1
```

Lower:

```
Q1 - 1.5*IQR
```

Upper:

```
Q3 + 1.5*IQR
```

---

# 24. Python Implementation

```python
Q1 = df["age"].quantile(
0.25
)


Q3 = df["age"].quantile(
0.75
)


IQR = Q3-Q1


outliers = df[
(df["age"] < Q1-1.5*IQR)
|
(df["age"] > Q3+1.5*IQR)
]
```

---

# 25. Outlier Remove

```python
clean_df = df[
(df["age"] >= Q1-1.5*IQR)
&
(df["age"] <= Q3+1.5*IQR)
]
```

---

# 26. Data Quality Check Function

Production style:

```python
def data_quality_check(df):

    print("Rows:", df.shape[0])

    print("Columns:", df.shape[1])

    print("\nMissing:")

    print(df.isnull().sum())

    print("\nDuplicates:")

    print(df.duplicated().sum())
```

Use:

```python
data_quality_check(df)
```

---

# 27. Real E-commerce Cleaning Example

Raw Orders:

```
order_id

customer

amount

date
```

Problems:

```
amount = "5000"

customer = " Rahim "

duplicate orders

missing date
```

Cleaning:

```python
df["amount"] = pd.to_numeric(
df["amount"]
)


df["customer"] = (
df["customer"]
.str.strip()
)


df.drop_duplicates(
inplace=True
)


df.dropna(
subset=["date"],
inplace=True
)
```

---

# 28. Production Data Quality Rules

একজন Data Engineer সাধারণত rules তৈরি করে:

Example:

```
order_id cannot be null

amount must be positive

email must be unique

date must be valid
```

---

# 29. Data Cleaning Mindset

Beginner:

> "আমি missing value remove করতে পারি"

Engineer:

> "আমি data কে trustworthy বানাতে পারি"

---

# Lesson 17 Summary

আজ শিখলেন:

✅ Data inspection
✅ Missing value detection
✅ `dropna()`
✅ `fillna()`
✅ Mean/Median/Mode filling
✅ Duplicate handling
✅ Data type cleaning
✅ String cleaning
✅ Outlier detection
✅ Data quality pipeline

---

# Lesson 17 Practice Task

Dataset:

```python
data={

"name":[
" Rahim ",
"Karim",
"Rahim",
None
],

"age":[
25,
30,
25,
200
],

"salary":[
50000,
60000,
50000,
None
]

}
```

Tasks:

### 1.

Missing value count বের করুন।

---

### 2.

Salary missing value median দিয়ে fill করুন।

---

### 3.

Duplicate row remove করুন।

---

### 4.

Name column clean করুন।

(space remove + lowercase)

---

### 5.

Age column এর outlier detect করুন।

---

### 6. Data Engineer Challenge

একটি raw e-commerce dataset ধরুন:

```
orders.csv
```

Problems:

* Missing customer
* Duplicate order
* Wrong amount datatype
* Invalid date
* Negative price

একটি complete cleaning pipeline লিখুন।

---

পরের Lesson:

# Lesson 18: Pandas Data Validation & ETL Pipeline

(Data Quality Rules, Automated Cleaning, Production Data Workflow)
# Pandas Mastery Course — Lesson 18

# Pandas Data Validation & ETL Pipeline

## Data Quality Rules, Automated Cleaning, Production Data Workflow

আজকের lesson থেকে আমরা Data Engineer mindset এ কাজ করবো।

আগের lesson এ আমরা manually data clean করেছি।

Production environment এ কেউ প্রতিদিন বসে:

```python
df.dropna()
df.fillna()
df.drop_duplicates()
```

চালায় না।

বরং তৈরি করা হয়:

> Automated Data Validation + ETL Pipeline

---

# 1. ETL কী?

ETL =

## Extract

Source থেকে data নেওয়া।

Example:

```text
Database
CSV
API
Logs
```

---

## Transform

Data clean এবং modify করা।

Example:

```text
Remove duplicate

Fix datatype

Create new columns
```

---

## Load

Clean data destination এ রাখা।

Example:

```text
Data Warehouse

PostgreSQL

BigQuery
```

---

# 2. Complete Data Pipeline

```text
Source Data

     |
     ↓

Extract

     |
     ↓

Validation

     |
     ↓

Cleaning

     |
     ↓

Transformation

     |
     ↓

Load

     |
     ↓

Analytics
```

---

# 3. Sample Raw Data

```python
import pandas as pd


data = {

"order_id":[
101,
102,
102,
None,
105
],

"customer":[
" Rahim ",
"Karim",
"Karim",
"Hasan",
None
],

"amount":[
5000,
7000,
7000,
-2000,
9000
],

"status":[
"paid",
"paid",
"paid",
"cancelled",
"paid"
]

}


df = pd.DataFrame(data)


df
```

---

# 4. Data Validation কী?

Validation মানে:

> Data expected rule follow করছে কিনা check করা।

Example:

Rule:

```text
order_id cannot be null

amount cannot be negative

customer must exist
```

---

# 5. Basic Validation Checks

## Check Missing

```python
df.isnull().sum()
```

Output:

```
order_id     1
customer     1
amount       0
```

---

# 6. Create Validation Function

Production style:

```python
def validate_data(df):

    errors = []


    # order_id check

    if df["order_id"].isnull().any():

        errors.append(
            "order_id contains null"
        )


    # amount check

    if (df["amount"] < 0).any():

        errors.append(
            "Negative amount found"
        )


    return errors
```

---

Run:

```python
errors = validate_data(df)


print(errors)
```

Output:

```
[
'order_id contains null',
'Negative amount found'
]
```

---

# 7. Data Cleaning Function

আমরা cleaning আলাদা function এ রাখবো।

```python
def clean_data(df):


    # remove spaces

    df["customer"] = (
        df["customer"]
        .str.strip()
    )


    # remove duplicates

    df = df.drop_duplicates()


    # remove invalid amount

    df = df[
        df["amount"] >= 0
    ]


    return df
```

---

# 8. Transformation Function

Example:

Revenue category:

```python
def transform_data(df):


    df["tax"] = (
        df["amount"]*0.15
    )


    df["total"] = (
        df["amount"]
        +
        df["tax"]
    )


    return df
```

---

# 9. Complete ETL Pipeline

এখন সব combine:

```python
def etl_pipeline(df):


    print(
        "Starting ETL"
    )


    # Validation

    errors = validate_data(df)


    if errors:

        print(
            "Validation Errors:",
            errors
        )


    # Cleaning

    df = clean_data(df)


    # Transformation

    df = transform_data(df)


    print(
        "ETL Completed"
    )


    return df
```

---

Run:

```python
clean_df = etl_pipeline(df)
```

---

# 10. Why Separate Functions?

Bad:

```python
# 500 lines code
```

Problem:

* Maintain করা কঠিন
* Debug কঠিন

Good:

```
extract.py

validate.py

clean.py

transform.py

load.py
```

---

# 11. Production Project Structure

Data Engineering project:

```
data_pipeline/


│
├── data/

│   └── raw.csv
│
├── src/

│   ├── extract.py
│   ├── validation.py
│   ├── cleaning.py
│   ├── transform.py
│   └── load.py
│
└── main.py

```

---

# 12. Extract Function

CSV থেকে:

```python
def extract_data(path):

    df = pd.read_csv(
        path
    )

    return df
```

---

# 13. Load Function

CSV:

```python
def load_data(df,path):

    df.to_csv(
        path,
        index=False
    )
```

---

Database:

```python
df.to_sql(
    "orders",
    connection
)
```

---

# 14. Data Quality Rules

Real company তে rules থাকে:

## Completeness

Example:

```text
customer_id cannot be null
```

---

## Accuracy

Example:

```text
age cannot be 500
```

---

## Consistency

Example:

```text
Dhaka

dhaka

DHAKA
```

same হতে হবে।

---

## Uniqueness

Example:

```text
email unique
order_id unique
```

---

# 15. Schema Validation

Expected:

```text
order_id → integer

amount → float

date → datetime
```

Check:

```python
df.dtypes
```

---

# 16. Data Validation with Pandas

Example:

```python
expected_columns = [

"order_id",

"customer",

"amount"

]


missing = set(
expected_columns
) - set(
df.columns
)


print(missing)
```

---

# 17. Logging

Production pipeline এ print না করে:

```python
import logging


logging.info(
"Cleaning started"
)
```

ব্যবহার করা হয়।

---

# 18. Failed Data Handling

সব data reject করা হয় না।

Example:

```
valid_data

invalid_data
```

Invalid আলাদা রাখা হয়:

```python
invalid_rows.to_csv(
"failed_records.csv"
)
```

---

# 19. Real E-commerce ETL Example

Source:

```
Orders Database
```

Extract:

```
10 million orders
```

Validate:

```
order_id exists

amount > 0

date valid
```

Transform:

```
add tax

add month

calculate revenue
```

Load:

```
Analytics Database
```

---

# 20. Data Engineer Mindset

Beginner:

> "আমি dataframe clean করতে পারি"

Data Engineer:

> "আমি automated reliable data pipeline তৈরি করতে পারি"

---

# Lesson 18 Summary

আজ শিখলেন:

✅ ETL concept
✅ Data validation
✅ Cleaning pipeline
✅ Transformation pipeline
✅ Automated workflow
✅ Project structure
✅ Data quality rules
✅ Error handling
✅ Production mindset

---

# Lesson 18 Practice Task

Create an ETL pipeline for:

Input:

```text
orders.csv
```

Columns:

```
order_id
customer
price
quantity
date
```

Rules:

### Validation

* order_id null allowed না
* price negative allowed না
* customer empty allowed না

### Cleaning

* duplicate remove
* customer strip
* datatype fix

### Transformation

Create:

```
total_amount

month

tax

final_amount
```

### Load

Save:

```
clean_orders.csv
```

---

পরের Lesson:

# Lesson 19: Pandas + SQL Database Integration

(Reading SQL Data, Writing Data, Database Analytics Workflow)
# Pandas Mastery Course — Lesson 19

# Pandas + SQL Database Integration

## Reading SQL Data, Writing Data, Database Analytics Workflow

আজকের lesson Data Engineer career এর জন্য খুব গুরুত্বপূর্ণ।

কারণ production environment এ data সাধারণত CSV file এ থাকে না।

Data থাকে:

* PostgreSQL
* MySQL
* SQL Server
* Data Warehouse

Pandas ব্যবহার হয়:

> Database থেকে data নিয়ে analysis করা এবং processed data আবার database এ রাখা।

---

# 1. Real Data Engineering Workflow

```text
Database

    ↓

Pandas

    ↓

Cleaning

    ↓

Transformation

    ↓

Analytics

    ↓

Database / Report
```

---

# 2. Required Libraries

Install:

```bash
pip install sqlalchemy psycopg2-binary
```

---

# 3. Database Connection Concept

Pandas নিজে database connect করে না।

এটা ব্যবহার করে:

```text
Pandas

 +

SQLAlchemy Engine

 +

Database Driver
```

---

# 4. SQLAlchemy Engine তৈরি

Example: PostgreSQL

```python id="a8k2p5"
from sqlalchemy import create_engine


engine = create_engine(

"postgresql://username:password@localhost:5432/database_name"

)
```

---

MySQL:

```python id="k7m3x9"
engine = create_engine(

"mysql+pymysql://username:password@localhost/db"

)
```

---

# 5. Database থেকে Data Read

ধরি table:

```sql
orders
```

Columns:

```text
id
customer
amount
date
```

---

Pandas:

```python id="m9q4v2"
import pandas as pd


df = pd.read_sql(

"SELECT * FROM orders",

engine

)


df.head()
```

---

# 6. SQL Query ব্যবহার

সব data না নিয়ে:

```python id="x5n8m3"
query = """

SELECT

customer,
amount

FROM orders

WHERE amount > 5000

"""


df = pd.read_sql(

query,

engine

)
```

---

# 7. Table Read করা

শুধু table name:

```python id="p8v3m1"
df = pd.read_sql_table(

"orders",

engine

)
```

---

# 8. SQL + Pandas Combination

Example:

Database:

```text
10 million orders
```

SQL দিয়ে filter:

```sql
WHERE date >= '2026-01-01'
```

তারপর Pandas:

```python
df.groupby(
"category"
)["amount"]
.sum()
```

---

# 9. Data Write to Database

Pandas dataframe:

```python
df.to_sql(

"sales_report",

engine,

if_exists="replace",

index=False

)
```

---

# 10. if_exists Options

## replace

```python
if_exists="replace"
```

পুরো table delete করে নতুন তৈরি করবে।

---

## append

```python
if_exists="append"
```

পুরনো data এর সাথে add করবে।

---

## fail

```python
if_exists="fail"
```

Table থাকলে error।

---

# 11. Production এ replace ব্যবহার করবেন না

Example:

Daily pipeline:

```text
January Data

+

February Data
```

replace করলে:

```text
January delete
```

হয়ে যাবে।

Use:

```python
append
```

---

# 12. SQL Query Result Analysis

Example:

```python
query = """

SELECT

category,

SUM(amount) revenue


FROM orders


GROUP BY category

"""


sales = pd.read_sql(

query,

engine

)
```

Output:

```text
category     revenue

Laptop       500000

Phone        200000
```

---

# 13. Large Data Handling

Problem:

```text
Database table

500 million rows
```

এটা একবারে load করা যাবে না।

---

Solution:

## chunksize

```python
for chunk in pd.read_sql(

query,

engine,

chunksize=100000

):

    process(chunk)
```

---

Meaning:

```text
100k rows

↓

Process

↓

Next 100k

↓

Process
```

---

# 14. Transaction Data Example

Orders:

```text
order_id
customer_id
product_id
amount
created_at
```

Need:

Monthly Revenue Report

SQL:

```sql
SELECT

DATE_TRUNC(
'month',
created_at
) month,

SUM(amount)


FROM orders


GROUP BY month
```

Pandas:

```python
report = pd.read_sql(
query,
engine
)
```

---

# 15. ORM vs SQL + Pandas

Django ORM:

```python
Order.objects.all()
```

Good:

* Application development

Pandas + SQL:

```python
pd.read_sql()
```

Good:

* Analytics
* ETL
* Data Engineering

---

# 16. Django Project + Pandas

আপনার DRF e-commerce project এ:

Database:

```text
PostgreSQL
```

Tables:

```text
users

products

orders

payments
```

Analytics:

```python
orders = pd.read_sql(
"SELECT * FROM orders",
engine
)
```

Generate:

```text
Daily Revenue

Top Customers

Product Report
```

---

# 17. Database Connection Secure Way

Bad:

```python
engine = create_engine(
"postgresql://admin:12345@localhost/db"
)
```

Password code এ রাখা উচিত না।

Good:

Environment variable:

`.env`

```text
DB_USER=admin
DB_PASSWORD=password
```

Python:

```python
import os


password=os.getenv(
"DB_PASSWORD"
)
```

---

# 18. ETL Example

Complete flow:

```python
# Extract

orders = pd.read_sql(
"SELECT * FROM orders",
engine
)


# Transform

orders["total"] = (
orders.price *
orders.quantity
)


# Load

orders.to_sql(
"clean_orders",
engine,
if_exists="append"
)
```

---

# 19. Database Index Importance

Large table:

```text
orders

100 million rows
```

Query:

```sql
WHERE customer_id=100
```

Index থাকলে:

```text
milliseconds
```

না থাকলে:

```text
minutes
```

---

# 20. Data Engineer Architecture

Production:

```text
PostgreSQL

      |

      ↓

Extract Layer

      |

      ↓

Pandas Transformation

      |

      ↓

Validation

      |

      ↓

Data Warehouse

      |

      ↓

Dashboard
```

---

# Lesson 19 Summary

আজ শিখলেন:

✅ SQLAlchemy connection
✅ PostgreSQL/MySQL connection
✅ `read_sql()`
✅ `read_sql_table()`
✅ `to_sql()`
✅ chunksize processing
✅ SQL + Pandas workflow
✅ ETL database pipeline
✅ Production database thinking

---

# Lesson 19 Practice Task

Create:

Database:

```
ecommerce_db
```

Table:

```
orders
```

Columns:

```
order_id
customer
product
amount
date
```

Tasks:

### 1.

PostgreSQL connect করুন।

---

### 2.

Orders table Pandas dataframe এ load করুন।

---

### 3.

Query দিয়ে:

```
amount > 5000
```

orders বের করুন।

---

### 4.

Create:

```
monthly_sales_report
```

table।

---

### 5. Data Engineer Challenge

একটি ETL pipeline তৈরি করুন:

Source:

```
orders table
```

Transform:

```
total_amount

tax

month
```

Load:

```
analytics_orders table
```

---

পরের Lesson:

# Lesson 20: Pandas Advanced Analytics Project

(End-to-End E-commerce Data Pipeline Project)

# Pandas Mastery Course — Lesson 20

# End-to-End E-commerce Data Analytics Pipeline Project

## Real Data Engineer Project Using Pandas + SQL + ETL

আজ আমরা এতদিন যা শিখেছি সব একসাথে ব্যবহার করবো।

এটি হবে একটি **production-style data pipeline**।

Project:

# E-commerce Sales Analytics Pipeline

---

# 1. Project Goal

আমাদের কাছে raw order data আছে।

আমরা তৈরি করবো:

* Clean dataset
* Revenue analysis
* Customer analysis
* Product performance
* Monthly report
* Database analytics table

---

# 2. Architecture

```text
              PostgreSQL
                  |
                  |
                  ↓
             Extract Layer
                  |
                  |
                  ↓
              Pandas ETL
                  |
        --------------------
        |                  |
        ↓                  ↓
 Data Cleaning       Data Transformation

        |
        ↓

 Analytics Tables

        |
        ↓

 Dashboard / BI

```

---

# 3. Database Table Design

## orders table

| Column      | Type     |
| ----------- | -------- |
| order_id    | integer  |
| customer_id | integer  |
| product_id  | integer  |
| quantity    | integer  |
| price       | float    |
| created_at  | datetime |

Example:

```text
order_id | customer_id | product_id | quantity | price

1          101           5            2          500
2          102           3            1          700
```

---

# 4. Step 1 — Extract Data

Database থেকে data আনবো।

```python
import pandas as pd
from sqlalchemy import create_engine


engine = create_engine(
"postgresql://user:password@localhost/ecommerce"
)


orders = pd.read_sql(
"""
SELECT *

FROM orders

""",
engine
)


orders.head()
```

---

# 5. Step 2 — Data Inspection

প্রথমে data বুঝতে হবে।

```python
orders.shape
```

Example:

```
(1000000,6)
```

---

Check:

```python
orders.info()
```

---

Statistics:

```python
orders.describe()
```

---

# 6. Step 3 — Data Validation

আমাদের rules:

## Rule 1

order_id null হতে পারবে না

```python
orders["order_id"].isnull().sum()
```

---

## Rule 2

Price negative হতে পারবে না

```python
orders[
orders["price"] < 0
]
```

---

## Rule 3

Quantity positive হতে হবে

```python
orders[
orders["quantity"] <=0
]
```

---

# 7. Step 4 — Data Cleaning

## Remove duplicate

```python
orders = orders.drop_duplicates()
```

---

## Remove invalid price

```python
orders = orders[
orders["price"] >= 0
]
```

---

## Fix datatype

```python
orders["created_at"] = pd.to_datetime(
orders["created_at"]
)
```

---

# 8. Step 5 — Feature Engineering

এখন নতুন column তৈরি করবো।

## Total Amount

Formula:

```
price × quantity
```

Code:

```python
orders["total_amount"] = (

orders["price"]

*

orders["quantity"]

)
```

---

# 9. Extract Date Features

Year:

```python
orders["year"] = (
orders["created_at"]
.dt.year
)
```

Month:

```python
orders["month"] = (

orders["created_at"]
.dt.month

)
```

Month Name:

```python
orders["month_name"] = (

orders["created_at"]
.dt.month_name()

)
```

---

# 10. Tax Calculation

ধরি:

Tax = 15%

```python
orders["tax"] = (

orders["total_amount"]

*

0.15

)
```

---

Final amount:

```python
orders["final_amount"] = (

orders["total_amount"]

+

orders["tax"]

)
```

---

# 11. Sales Analytics

## Total Revenue

```python
orders["final_amount"].sum()
```

Example:

```
50,000,000
```

---

# 12. Monthly Revenue

```python
monthly_sales = (

orders

.groupby("month_name")

["final_amount"]

.sum()

)
```

Output:

```
January     500000

February    700000

March       900000
```

---

# 13. Daily Sales Trend

```python
daily_sales = (

orders

.set_index(
"created_at"
)

["final_amount"]

.resample("D")

.sum()

)
```

---

# 14. Top Customers

```python
top_customers = (

orders

.groupby(
"customer_id"
)

["final_amount"]

.sum()

.sort_values(
ascending=False
)

.head(10)

)
```

Output:

```
customer_id     revenue

101             500000

205             450000
```

---

# 15. Product Performance

```python
product_sales = (

orders

.groupby(
"product_id"
)

["quantity"]

.sum()

.sort_values(
ascending=False
)

)
```

---

# 16. Rolling Average

৭ দিনের sales trend:

```python
daily_sales = daily_sales.to_frame()


daily_sales["7_day_avg"] = (

daily_sales["final_amount"]

.rolling(7)

.mean()

)
```

---

# 17. Load Analytics Data

Clean data database এ save করবো।

```python
orders.to_sql(

"analytics_orders",

engine,

if_exists="replace",

index=False

)
```

---

# 18. Save Reports

CSV:

```python
monthly_sales.to_csv(
"monthly_sales.csv"
)
```

---

Excel:

```python
monthly_sales.to_excel(
"sales_report.xlsx"
)
```

---

# 19. Production Folder Structure

Real project:

```
ecommerce_pipeline/


│

├── data/

│   └── raw/

│

├── src/

│
├── extract.py

├── validate.py

├── clean.py

├── transform.py

├── analytics.py

├── load.py


│

└── main.py

```

---

# 20. main.py

Pipeline controller:

```python
from extract import extract_data
from clean import clean_data
from transform import transform_data
from load import load_data



df = extract_data()


df = clean_data(df)


df = transform_data(df)


load_data(df)
```

---

# 21. Production Improvements

Real company তে add করা হয়:

## Logging

```python
logger.info(
"Pipeline started"
)
```

---

## Error Handling

```python
try:

    pipeline()

except Exception as e:

    send_alert(e)
```

---

## Scheduling

Tools:

* Airflow
* Prefect
* Dagster

---

# 22. What You Built

এই project এ আপনি ব্যবহার করেছেন:

### Pandas Skills

✅ Data loading
✅ Cleaning
✅ Missing handling
✅ Duplicate removal
✅ Datetime processing
✅ GroupBy
✅ Aggregation
✅ Resampling
✅ Rolling window
✅ Export

### Data Engineering Skills

✅ ETL
✅ Data validation
✅ Database integration
✅ Analytics pipeline

---

# Lesson 20 Final Challenge

নিজের DRF E-commerce project এর database ব্যবহার করুন।

Tables:

```
users

products

orders

payments

reviews
```

Create:

## Customer Analytics

```
customer_id

total_orders

total_spent

average_order_value
```

## Product Analytics

```
product_id

total_sales

total_quantity

revenue
```

## Monthly Report

```
month

revenue

orders

customers
```

---

# Next Phase (Lesson 21 → Advanced Pandas)

পরের lesson থেকে শুরু হবে:

# Lesson 21: Pandas for Machine Learning

## Feature Engineering, Dataset Preparation, Encoding, Scaling, Train-Test Split

এখান থেকে Pandas + ML Engineering শুরু হবে।

# Pandas Mastery Course — Lesson 21

# Pandas for Machine Learning

## Feature Engineering, Dataset Preparation, Encoding, Scaling, Train-Test Split

আজ থেকে আমরা Pandas কে Machine Learning এর perspective থেকে ব্যবহার করা শুরু করবো।

একজন ML Engineer এর জন্য model বানানোই শুধু কাজ না।

সবচেয়ে গুরুত্বপূর্ণ কাজ:

> Raw Data → Machine Learning Ready Dataset তৈরি করা

এই কাজের 80% Pandas দিয়ে হয়।

---

# 1. ML Pipeline Overview

একটি Machine Learning pipeline:

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

Model Training

      ↓

Evaluation
```

---

# 2. Sample Dataset

ধরি আমরা House Price Prediction করবো।

Dataset:

| area | bedrooms | city       | price   |
| ---- | -------- | ---------- | ------- |
| 1200 | 3        | Dhaka      | 5000000 |
| 1500 | 4        | Dhaka      | 7000000 |
| 800  | 2        | Khulna     | 3000000 |
| 2000 | 5        | Chittagong | 9000000 |

---

Create dataframe:

```python
import pandas as pd


data = {

"area":[1200,1500,800,2000],

"bedrooms":[3,4,2,5],

"city":[
"Dhaka",
"Dhaka",
"Khulna",
"Chittagong"
],

"price":[
5000000,
7000000,
3000000,
9000000
]

}


df = pd.DataFrame(data)


df
```

---

# 3. Feature এবং Target বুঝা

Machine Learning এ দুই ধরনের data থাকে:

## Feature (X)

যা model কে দেওয়া হয়।

Example:

```text
area

bedrooms

city
```

---

## Target (y)

যেটা predict করতে চাই।

Example:

```text
price
```

---

Split:

```python
X = df.drop(
"price",
axis=1
)


y = df["price"]
```

---

# 4. Missing Value Handling

ML model সাধারণত:

```text
NaN
```

handle করতে পারে না।

Check:

```python
df.isnull().sum()
```

---

Fill:

Numerical:

```python
df["area"].fillna(
df["area"].mean(),
inplace=True
)
```

Categorical:

```python
df["city"].fillna(
df["city"].mode()[0],
inplace=True
)
```

---

# 5. Feature Engineering

Raw feature:

```text
area
bedrooms
```

আমরা নতুন feature বানাতে পারি:

Example:

Price per area:

Formula:

```
price / area
```

```python
df["price_per_area"] = (

df["price"]

/

df["area"]

)
```

---

# 6. Date Feature Engineering

E-commerce example:

Raw:

```text
2026-07-13 10:30:00
```

Create:

```python
df["year"] = (
df["date"]
.dt.year
)


df["month"] = (
df["date"]
.dt.month
)


df["day"] = (
df["date"]
.dt.day
)
```

---

# 7. Categorical Data Problem

Machine Learning বুঝে:

```text
number
```

কিন্তু data:

```
Dhaka
Khulna
Chittagong
```

এগুলো text।

Convert করতে হবে।

একে বলে:

# Encoding

---

# 8. Label Encoding

Example:

Before:

```
Dhaka

Khulna

Chittagong
```

After:

```
0

1

2
```

Code:

```python
from sklearn.preprocessing import LabelEncoder


encoder = LabelEncoder()


df["city_encoded"] = encoder.fit_transform(
df["city"]
)
```

---

Output:

| city       | encoded |
| ---------- | ------- |
| Dhaka      | 0       |
| Khulna     | 1       |
| Chittagong | 2       |

---

# 9. One Hot Encoding

Problem:

Label Encoding:

```
Dhaka = 0
Khulna = 1
```

Model ভাবতে পারে:

```
Khulna > Dhaka
```

কিন্তু আসলে category এর order নেই।

Solution:

One Hot Encoding

Before:

```
city
Dhaka
Khulna
```

After:

| Dhaka | Khulna |
| ----- | ------ |
| 1     | 0      |
| 0     | 1      |

---

Code:

```python
pd.get_dummies(
df,
columns=[
"city"
]
)
```

---

# 10. Numerical Scaling

কিছু model scale sensitive:

Example:

```
age = 30

salary = 500000
```

salary অনেক বড়।

Solution:

Scaling

---

# 11. Standardization

Formula:

```
z = (x - mean) / std
```

Code:

```python
from sklearn.preprocessing import StandardScaler


scaler = StandardScaler()


df[

["area"]

] = scaler.fit_transform(

df[["area"]]

)
```

---

# 12. Min-Max Scaling

Range:

```
0 to 1
```

Code:

```python
from sklearn.preprocessing import MinMaxScaler


scaler = MinMaxScaler()


df["area"] = scaler.fit_transform(
df[["area"]]
)
```

---

# 13. Train-Test Split

Model train করার আগে:

Data ভাগ করি:

```
80%

Train


20%

Test
```

---

Code:

```python
from sklearn.model_selection import train_test_split


X_train, X_test, y_train, y_test = train_test_split(

X,

y,

test_size=0.2,

random_state=42

)
```

---

# 14. কেন Split করি?

যদি একই data দিয়ে:

Train:

```
100%
```

Test:

```
same data
```

তাহলে model cheating করবে।

একে বলে:

```
Overfitting
```

---

# 15. Real E-commerce ML Example

ধরি:

Customer churn prediction:

Raw:

```
customer_id

age

city

total_orders

last_login

status
```

Feature:

```
age

city_encoded

total_orders

days_since_login
```

Target:

```
churn
```

---

# 16. Complete ML Preparation Pipeline

```python
# Load data

df = pd.read_csv(
"customers.csv"
)


# Missing

df.fillna(
0,
inplace=True
)


# Encoding

df = pd.get_dummies(
df,
columns=["city"]
)


# Split

X = df.drop(
"churn",
axis=1
)


y = df["churn"]


X_train, X_test, y_train, y_test = train_test_split(

X,

y,

test_size=0.2

)
```

---

# 17. Data Leakage Important Concept

Wrong:

```python
scaler.fit(
all_data
)
```

কারণ:

Test data এর information train এ চলে গেছে।

Correct:

```python
scaler.fit(
X_train
)


scaler.transform(
X_test
)
```

---

# 18. ML Engineer Mindset

Beginner:

> "আমি model train করতে চাই"

ML Engineer:

> "আমি model এর জন্য high quality features তৈরি করতে চাই"

---

# Lesson 21 Summary

আজ শিখলেন:

✅ ML data pipeline
✅ Feature vs Target
✅ Feature Engineering
✅ Missing value handling
✅ Label Encoding
✅ One Hot Encoding
✅ Scaling
✅ Train-Test Split
✅ Data Leakage

---

# Lesson 21 Practice Task

Dataset:

```python
data={

"age":[25,30,35,40],

"city":[
"Dhaka",
"Khulna",
"Dhaka",
"Chittagong"
],

"income":[
30000,
40000,
50000,
60000
],

"buy":[
0,
1,
1,
1
]

}
```

Tasks:

### 1.

`city` encode করুন।

---

### 2.

income scale করুন।

---

### 3.

X এবং y তৈরি করুন।

---

### 4.

Train-test split করুন।

---

### 5. ML Ready Dataset তৈরি করুন।

---

পরের Lesson:

# Lesson 22: Advanced Feature Engineering with Pandas

## (Datetime Features, Aggregation Features, Customer RFM Analysis, ML Feature Creation)

# Pandas Mastery Course — Lesson 22

# Advanced Feature Engineering with Pandas

## Datetime Features, Aggregation Features, Customer RFM Analysis, ML Feature Creation

আজকের lesson থেকে আমরা Data Analyst নয়, **ML Engineer / Data Engineer level feature creation** শিখবো।

Machine Learning model ভালো করার জন্য শুধু model change করলেই হয় না।

অনেক সময়:

> Better Features → Better Model

---

# 1. Feature Engineering কী?

Raw data:

```text
customer_id
order_date
amount
```

Model এর জন্য তৈরি:

```text
total_orders

average_amount

days_since_last_order

customer_age
```

এই process:

# Feature Engineering

---

# 2. Feature Engineering Pipeline

```text
Raw Data

    ↓

Understand Business Problem

    ↓

Create Features

    ↓

Remove Noise

    ↓

Train Model

```

---

# 3. Dataset Example

E-commerce orders:

```python id="p8f2v9"
import pandas as pd


orders = pd.DataFrame({

"customer_id":[
1,1,2,2,3,3
],

"order_date":[
"2026-01-01",
"2026-02-01",
"2026-01-10",
"2026-03-01",
"2026-01-15",
"2026-03-10"
],

"amount":[
500,
700,
300,
800,
1000,
1200
]

})


orders
```

---

# 4. Convert Date

```python id="9s4h2m"
orders["order_date"] = pd.to_datetime(

orders["order_date"]

)
```

---

# 5. Datetime Feature Creation

## Year

```python id="m2x7k8"
orders["year"] = (

orders["order_date"]

.dt.year

)
```

---

## Month

```python id="w5z9q2"
orders["month"] = (

orders["order_date"]

.dt.month

)
```

---

## Day

```python id="n8k4p6"
orders["day"] = (

orders["order_date"]

.dt.day

)
```

---

## Weekday

```python id="q4m8x1"
orders["weekday"] = (

orders["order_date"]

.dt.day_name()

)
```

---

# 6. Business Time Features

E-commerce এ useful:

Weekend order:

```python id="6m2p9q"
orders["is_weekend"] = (

orders["order_date"]

.dt.weekday >= 5

)
```

---

Output:

```text
True
False
```

---

# 7. Month Start / End

Month start:

```python id="r7m3x5"
orders["month_start"] = (

orders["order_date"]

.dt.to_period("M")

.dt.start_time

)
```

---

# 8. Aggregation Features

Raw orders:

```text
customer_id

amount
```

Need:

```text
Total spending per customer
```

---

GroupBy:

```python id="j9q2m4"
customer_features = (

orders

.groupby(
"customer_id"
)

["amount"]

.sum()

.reset_index()

)
```

Output:

| customer | total |
| -------- | ----- |
| 1        | 1200  |
| 2        | 1100  |

---

# 9. Count Feature

Customer কত order করেছে?

```python id="a6v8p3"
order_count = (

orders

.groupby(
"customer_id"
)

["amount"]

.count()

)
```

---

Feature:

```text
number_of_orders
```

---

# 10. Average Order Value

Formula:

```text
Total Amount / Total Orders
```

Code:

```python id="t3m7x9"
avg_order = (

orders

.groupby(
"customer_id"
)

["amount"]

.mean()

)
```

---

# 11. Multiple Aggregation

একসাথে:

```python id="k8p4z6"
customer_features = (

orders

.groupby(
"customer_id"
)

["amount"]

.agg(
[
"sum",
"count",
"mean",
"max"
]
)

)
```

Output:

| customer | sum  | count | mean | max |
| -------- | ---- | ----- | ---- | --- |
| 1        | 1200 | 2     | 600  | 700 |

---

# 12. RFM Analysis

E-commerce এর সবচেয়ে famous feature engineering technique।

RFM:

## R = Recency

শেষ order কতদিন আগে?

## F = Frequency

কতবার order করেছে?

## M = Monetary

কত টাকা spend করেছে?

---

# 13. Recency Feature

ধরি:

আজ:

```text
2026-04-01
```

Code:

```python id="n6x2m7"
today = pd.Timestamp(
"2026-04-01"
)


orders["days_since_order"] = (

today -

orders["order_date"]

).dt.days
```

---

# 14. Customer Recency

```python id="v9m3k2"
recency = (

orders

.groupby(
"customer_id"
)

["days_since_order"]

.min()

)
```

কারণ:

সবচেয়ে recent order চাই।

---

# 15. Frequency

```python id="p2x7m8"
frequency = (

orders

.groupby(
"customer_id"
)

.size()

)
```

---

# 16. Monetary

```python id="w3k9q5"
monetary = (

orders

.groupby(
"customer_id"
)

["amount"]

.sum()

)
```

---

# 17. Combine RFM

```python id="s6m2v8"
rfm = pd.DataFrame({

"recency":recency,

"frequency":frequency,

"monetary":monetary

})


rfm
```

Output:

| customer | recency | frequency | monetary |
| -------- | ------- | --------- | -------- |
| 1        | 60      | 2         | 1200     |
| 2        | 31      | 2         | 1100     |

---

# 18. ML Feature Creation Example

Customer Churn Model:

Raw:

```text
orders
```

Create:

```text
total_orders

total_spent

avg_order_value

last_order_days

```

---

# 19. Rolling Features

Time series ML এ:

Daily sales:

```python id="u4m7x2"
daily_sales = (

orders

.set_index(
"order_date"
)

["amount"]

.sum()

)
```

7 day average:

```python id="q8p3m6"
daily_sales.rolling(7).mean()
```

---

# 20. Lag Features

Previous value:

```python id="d5n9k3"
orders["previous_amount"] = (

orders["amount"]

.shift(1)

)
```

---

Used in:

* Forecasting
* Recommendation
* Demand prediction

---

# 21. Feature Interaction

Two features combine:

Example:

```text
price

quantity
```

Create:

```python id="z7m2p9"
orders["revenue"] = (

orders["price"]

*

orders["quantity"]

)
```

---

# 22. Binning Features

Age:

```text
18
25
40
60
```

Create groups:

```text
Young

Adult

Senior
```

---

Code:

```python id="h5q8m4"
pd.cut(

df["age"],

bins=[
0,
18,
40,
100
],

labels=[
"young",
"adult",
"senior"
]

)
```

---

# 23. Feature Selection

সব feature দরকার নেই।

Remove:

```python id="b8m3x6"
df.drop(
"customer_id",
axis=1
)
```

কারণ:

ID সাধারণত prediction করে না।

---

# 24. Real ML Pipeline Example

Customer Prediction:

Input:

```text
Orders Table

↓

Feature Engineering

↓

Customer Feature Table

↓

ML Model

↓

Churn Prediction
```

---

# 25. Final Feature Table

Example:

```text
customer_id

total_orders

total_spent

avg_order_value

last_order_days

preferred_month

```

এটাই ML model এ যাবে।

---

# Lesson 22 Summary

আজ শিখলেন:

✅ Feature Engineering concept
✅ Datetime features
✅ GroupBy aggregation features
✅ Customer analytics features
✅ RFM analysis
✅ Rolling features
✅ Lag features
✅ Feature interaction
✅ Feature selection

---

# Lesson 22 Practice Task

E-commerce dataset:

```python
orders

customer_id

order_date

amount

product_category
```

Create:

### Customer Feature Table

Columns:

```text
customer_id

total_orders

total_spent

average_order_value

last_order_date

days_since_last_order

favorite_category
```

---

### ML Challenge:

Customer churn prediction এর জন্য কমপক্ষে 10টি feature তৈরি করুন।

---

পরের Lesson:

# Lesson 23: Pandas Advanced GroupBy & Aggregation Mastery

## (Multi-level Grouping, Pivot Table, Window Functions, Business Analytics)

# Pandas Mastery Course — Lesson 23

# Advanced GroupBy & Aggregation Mastery

## Multi-Level Grouping, Pivot Table, Window Functions, Business Analytics

আজকের lesson Pandas এর সবচেয়ে powerful অংশগুলোর একটি।

বাস্তব Data Engineering / Analytics এ সবচেয়ে বেশি ব্যবহার হয়:

* `groupby()`
* `agg()`
* `pivot_table()`
* Window Function
* Ranking
* Cumulative Analysis

---

# 1. GroupBy কী?

GroupBy মানে:

> Data কে category অনুযায়ী ভাগ করে calculation করা।

Example:

Orders:

| customer | category | amount |
| -------- | -------- | ------ |
| Rahim    | Laptop   | 5000   |
| Karim    | Phone    | 3000   |
| Rahim    | Phone    | 2000   |

Question:

প্রতি customer কত spend করেছে?

---

# 2. Sample Dataset

```python
import pandas as pd


orders = pd.DataFrame({

"customer":[
"Rahim",
"Karim",
"Rahim",
"Hasan",
"Karim"
],

"category":[
"Laptop",
"Phone",
"Phone",
"Laptop",
"Laptop"
],

"amount":[
5000,
3000,
2000,
7000,
4000
],

"quantity":[
1,
2,
1,
1,
2
]

})


orders
```

---

# 3. Basic GroupBy

Customer wise sales:

```python
orders.groupby(
"customer"
)["amount"]
.sum()
```

Output:

```
Rahim     7000
Karim     7000
Hasan     7000
```

---

# 4. GroupBy Result DataFrame করা

```python
sales = (

orders

.groupby("customer")

["amount"]

.sum()

.reset_index()

)


sales
```

Output:

| customer | amount |
| -------- | ------ |
| Rahim    | 7000   |
| Karim    | 7000   |

---

# 5. Multiple Aggregation

একই সাথে:

* total sales
* average sales
* max sales

```python
orders.groupby(
"customer"
)["amount"]
.agg(
[
"sum",
"mean",
"max",
"count"
]
)
```

Output:

| customer | sum  | mean | max  | count |
| -------- | ---- | ---- | ---- | ----- |
| Rahim    | 7000 | 3500 | 5000 | 2     |

---

# 6. Named Aggregation

Production এ বেশি readable:

```python
report = (

orders

.groupby("customer")

.agg(

total_sales=("amount","sum"),

avg_sales=("amount","mean"),

orders=("amount","count")

)

)


report
```

Output:

| customer | total_sales | avg_sales | orders |
| -------- | ----------- | --------- | ------ |
| Rahim    | 7000        | 3500      | 2      |

---

# 7. Multiple Column Grouping

Question:

Customer + Category sales

```python
orders.groupby(

[
"customer",
"category"
]

)["amount"].sum()
```

Output:

```
Rahim Laptop 5000
Rahim Phone 2000
Karim Laptop 4000
```

---

# 8. Multi-Level GroupBy

Example:

Region → Category → Sales

```python
orders.groupby(

[
"customer",
"category"

])

["amount"]

.sum()
```

এখানে তৈরি হয়:

```
MultiIndex
```

---

# 9. Reset Index

MultiIndex থেকে normal dataframe:

```python
df = (

orders.groupby(
[
"customer",
"category"
]
)

["amount"]

.sum()

.reset_index()

)
```

---

# 10. Pivot Table

Pivot table হলো:

> Excel Pivot এর মতো analysis tool

Example:

```python
pd.pivot_table(

orders,

values="amount",

index="customer",

columns="category",

aggfunc="sum"

)
```

Output:

| customer | Laptop | Phone |
| -------- | ------ | ----- |
| Rahim    | 5000   | 2000  |
| Karim    | 4000   | 3000  |

---

# 11. Pivot Table Multiple Calculation

```python
pd.pivot_table(

orders,

values="amount",

index="customer",

aggfunc=[
"sum",
"mean",
"count"
]

)
```

---

# 12. GroupBy vs Pivot Table

| GroupBy              | Pivot           |
| -------------------- | --------------- |
| Programming friendly | Report friendly |
| Complex logic        | Dashboard       |
| ETL                  | Business report |

---

# 13. Ranking Analysis

Question:

Top customers কে?

```python
sales_rank = (

orders

.groupby("customer")

["amount"]

.sum()

.rank(
ascending=False
)

)
```

---

Output:

```
Rahim 1
Karim 2
Hasan 3
```

---

# 14. Sort Ranking

```python
top = (

orders

.groupby("customer")

["amount"]

.sum()

.sort_values(
ascending=False
)

)
```

---

# 15. Percentage Contribution

Customer revenue share:

```python
customer_sales = (

orders.groupby(
"customer"
)

["amount"]

.sum()

)


customer_sales / customer_sales.sum()
```

Output:

```
Rahim 33%
Karim 33%
Hasan 33%
```

---

# 16. Cumulative Sum

Business:

"Year-to-date sales"

Example:

```python
orders["running_sales"] = (

orders["amount"]

.cumsum()

)
```

Output:

| amount | running |
| ------ | ------- |
| 5000   | 5000    |
| 3000   | 8000    |

---

# 17. Group-wise Cumulative Sum

Customer অনুযায়ী:

```python
orders["customer_total"] = (

orders

.groupby("customer")

["amount"]

.cumsum()

)
```

---

# 18. Window Function Concept

SQL এ:

```sql
SUM(amount)
OVER(
PARTITION BY customer
)
```

Pandas:

```python
groupby()

+

transform()
```

---

# 19. Transform()

Difference:

GroupBy:

```python
groupby().sum()
```

row কমায়।

Transform:

```python
groupby().transform()
```

row একই রাখে।

---

# 20. Example Transform

Customer total প্রতিটি row তে:

```python
orders["customer_sales"] = (

orders

.groupby("customer")

["amount"]

.transform("sum")

)
```

Output:

| customer | amount | customer_sales |
| -------- | ------ | -------------- |
| Rahim    | 5000   | 7000           |
| Rahim    | 2000   | 7000           |

---

# 21. Difference Calculation

Customer average থেকে difference:

```python
orders["difference"] = (

orders["amount"]

-

orders

.groupby("customer")

["amount"]

.transform("mean")

)
```

---

# 22. Business Analytics Example

E-commerce:

Need:

```
Customer

Total Orders

Revenue

Average Order

Rank
```

Code:

```python
customer_report = (

orders

.groupby("customer")

.agg(

orders=("amount","count"),

revenue=("amount","sum"),

avg_order=("amount","mean")

)

)

customer_report["rank"] = (

customer_report["revenue"]

.rank(
ascending=False
)

)
```

---

# 23. Category Performance

```python
category_report = (

orders

.groupby("category")

.agg(

sales=("amount","sum"),

quantity=("quantity","sum")

)

)
```

---

# 24. Real Data Engineer Use Case

Raw Orders:

```
100 million rows
```

Create:

Customer Analytics Table:

```
customer_id

total_orders

total_spent

avg_order_value

rank
```

Product Analytics Table:

```
product_id

sales

quantity

revenue
```

---

# 25. Production Pipeline

```text
Raw Orders

      ↓

GroupBy

      ↓

Aggregation

      ↓

Feature Table

      ↓

Database

      ↓

Dashboard / ML
```

---

# Lesson 23 Summary

আজ শিখলেন:

✅ Advanced GroupBy
✅ Multi-level grouping
✅ Named aggregation
✅ Pivot table
✅ Ranking
✅ Percentage analysis
✅ Cumulative sum
✅ Window function
✅ Transform

---

# Lesson 23 Practice Task

Dataset:

```python
sales = {

"customer":[
"A",
"A",
"B",
"B",
"C"
],

"product":[
"Laptop",
"Phone",
"Laptop",
"Phone",
"Laptop"
],

"amount":[
5000,
3000,
7000,
2000,
6000
]

}
```

Tasks:

### 1.

Customer total sales বের করুন।

---

### 2.

Customer + Product অনুযায়ী sales বের করুন।

---

### 3.

Pivot table তৈরি করুন:

```
          Laptop Phone

A

B

C
```

---

### 4.

Customer rank তৈরি করুন।

---

### 5.

প্রতিটি row তে customer total sales যোগ করুন (`transform` ব্যবহার করে)।

---

পরের Lesson:

# Lesson 24: Pandas Visualization & Exploratory Data Analysis (EDA)

## (Matplotlib, Seaborn, Distribution, Correlation, Business Insights)
# Pandas Mastery Course — Lesson 24

# Pandas Visualization & Exploratory Data Analysis (EDA)

## Matplotlib, Seaborn, Distribution, Correlation, Business Insights

আজকের lesson এ আমরা data কে শুধু দেখবো না, **data থেকে insight বের করা শিখবো।**

একজন Data Engineer / ML Engineer এর জন্য:

> Data বুঝতে না পারলে ভালো pipeline বা model তৈরি করা যায় না।

EDA (Exploratory Data Analysis) ব্যবহার করা হয়:

* Dataset বুঝতে
* Pattern খুঁজতে
* Problem detect করতে
* Feature নির্বাচন করতে
* Business decision নিতে

---

# 1. EDA Pipeline

```text
Raw Dataset

      ↓

Understand Data

      ↓

Statistics

      ↓

Visualization

      ↓

Find Pattern

      ↓

Feature Engineering

      ↓

Model / Analytics
```

---

# 2. Required Libraries

```python
import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns
```

---

# 3. Sample Dataset

E-commerce sales:

```python
import pandas as pd


sales = pd.DataFrame({

"month":[
"Jan",
"Feb",
"Mar",
"Apr",
"May"
],

"revenue":[
10000,
15000,
12000,
18000,
25000
],

"orders":[
100,
120,
110,
150,
200
]

})


sales
```

---

# 4. Basic Data Understanding

## First rows

```python
sales.head()
```

---

## Shape

```python
sales.shape
```

Output:

```
(5,3)
```

---

## Information

```python
sales.info()
```

---

## Statistics

```python
sales.describe()
```

---

# 5. Line Chart

Time series data এর জন্য।

Question:

Revenue growth কেমন?

```python
plt.plot(
sales["month"],
sales["revenue"]
)

plt.xlabel("Month")

plt.ylabel("Revenue")

plt.title(
"Monthly Revenue"
)

plt.show()
```

---

Insight:

```
Revenue increasing
```

---

# 6. Bar Chart

Category comparison এর জন্য।

Example:

```python
plt.bar(

sales["month"],

sales["revenue"]

)

plt.show()
```

---

Use cases:

* Product sales
* Category comparison
* Region analysis

---

# 7. Histogram

Distribution বুঝতে।

Example:

Customer spending:

```python
df["amount"].hist()

plt.show()
```

দেখাবে:

* Data spread
* Outlier
* Distribution

---

# 8. Box Plot

Outlier detect করার জন্য।

```python
sns.boxplot(

x=df["amount"]

)

plt.show()
```

---

Output:

```
Normal range

Outliers
```

---

# 9. Scatter Plot

দুই feature relationship।

Example:

Price vs Sales:

```python
plt.scatter(

df["price"],

df["sales"]

)

plt.xlabel("Price")

plt.ylabel("Sales")

plt.show()
```

---

Question:

Price বাড়লে sales বাড়ে কিনা?

---

# 10. Correlation Analysis

Correlation:

দুই variable এর সম্পর্ক।

Example:

```python
corr = df.corr()

corr
```

Output:

|       | price | sales |
| ----- | ----- | ----- |
| price | 1     | 0.8   |
| sales | 0.8   | 1     |

---

Meaning:

```
0.8 = strong positive relation
```

---

# 11. Heatmap

Correlation visualize:

```python
sns.heatmap(

corr,

annot=True

)

plt.show()
```

---

ML এ খুব important।

কারণ:

যে feature target এর সাথে related:

```
keep
```

যে feature useless:

```
remove
```

---

# 12. Missing Value Visualization

Missing check:

```python
sns.heatmap(

df.isnull(),

cbar=False

)

plt.show()
```

---

দেখাবে:

কোন জায়গায় missing আছে।

---

# 13. Customer Analysis Example

Dataset:

```python
customers = pd.DataFrame({

"age":[20,25,30,35,40],

"spending":[

1000,
3000,
5000,
7000,
9000

]

})
```

---

Scatter:

```python
plt.scatter(

customers["age"],

customers["spending"]

)

plt.show()
```

---

Insight:

Age বাড়লে spending বাড়ছে।

---

# 14. Category Sales Analysis

Example:

```python
category = pd.DataFrame({

"category":[
"Laptop",
"Phone",
"Tablet"
],

"sales":[
50000,
70000,
30000
]

})
```

---

Bar:

```python
sns.barplot(

data=category,

x="category",

y="sales"

)

plt.show()
```

---

# 15. Distribution Analysis

Customer income:

```python
sns.histplot(

df["income"],

kde=True

)

plt.show()
```

---

এখান থেকে বুঝবো:

* Normal distribution?
* Skewed?
* Outlier?

---

# 16. Skewness

Check:

```python
df["income"].skew()
```

Output:

```
2.5
```

Meaning:

Right skewed.

---

# 17. Log Transformation

Highly skewed data:

```python
import numpy as np


df["log_income"] = (

np.log1p(
df["income"]
)

)
```

---

ML model এর জন্য useful।

---

# 18. Pair Plot

Multiple feature relation:

```python
sns.pairplot(
df
)

plt.show()
```

---

দেখাবে:

* Feature relationship
* Distribution
* Pattern

---

# 19. EDA for E-commerce

Dataset:

```
orders
```

Questions:

## 1. Monthly Revenue?

```python
orders.groupby(
"month"
)["amount"].sum()
```

---

## 2. Top Products?

```python
orders.groupby(
"product"
)["amount"].sum()
```

---

## 3. Customer Behavior?

```python
orders.groupby(
"customer"
)["amount"].sum()
```

---

# 20. EDA + ML Workflow

```text
Dataset

 ↓

EDA

 ↓

Find Problems

 ↓

Feature Engineering

 ↓

Train Model

 ↓

Evaluate

```

---

# 21. Real Data Engineer Usage

Production এ EDA দিয়ে:

Detect করা হয়:

## Data Drift

Example:

January:

```
Average price = 500
```

July:

```
Average price = 5000
```

Problem হতে পারে।

---

# 22. Business Insight Example

Visualization থেকে:

Finding:

```
Laptop sales highest in December
```

Decision:

```
Increase inventory
```

---

# 23. EDA Checklist

প্রতিটি dataset এ:

## Structure

✅ shape
✅ columns
✅ datatype

## Quality

✅ missing values
✅ duplicates
✅ invalid data

## Statistics

✅ mean
✅ median
✅ distribution

## Visualization

✅ trend
✅ correlation
✅ outlier

---

# Lesson 24 Summary

আজ শিখলেন:

✅ EDA concept
✅ Matplotlib basics
✅ Seaborn basics
✅ Line chart
✅ Bar chart
✅ Histogram
✅ Box plot
✅ Scatter plot
✅ Correlation
✅ Heatmap
✅ Business insight extraction

---

# Lesson 24 Practice Task

Dataset:

```python
data={

"month":[
"Jan",
"Feb",
"Mar",
"Apr"
],

"sales":[
1000,
2000,
1500,
3000
],

"orders":[
10,
20,
15,
30
]

}
```

Tasks:

### 1.

Sales line chart তৈরি করুন।

---

### 2.

Orders bar chart তৈরি করুন।

---

### 3.

Sales distribution দেখুন।

---

### 4.

Correlation heatmap তৈরি করুন।

---

### 5. Business Insight লিখুন:

Example:

```
Which month performed best?
Sales trend increasing নাকি decreasing?
```

---

পরের Lesson:

# Lesson 25: Pandas Capstone Project

## End-to-End Data Engineering + ML Ready Pipeline (Final Mastery Project)
# Pandas Mastery Course — Lesson 25 (Final Capstone)

# End-to-End Data Engineering + ML Ready Pipeline Project

## Production Style E-commerce Analytics System Using Pandas

আজকে আমরা পুরো Pandas course এর সব concept একসাথে ব্যবহার করবো।

এই project শেষে আপনি বলতে পারবেন:

> "আমি Pandas দিয়ে real-world data pipeline তৈরি করতে পারি।"

---

# Project: E-commerce Data Intelligence Pipeline

## Goal

একটি e-commerce কোম্পানির:

* Sales analytics
* Customer analytics
* Product analytics
* ML feature dataset

তৈরি করা।

---

# 1. Complete Architecture

```text
                 PostgreSQL
                     |
                     |
                     ↓
              Extract Data
                     |
                     |
                     ↓
              Pandas DataFrame
                     |
          ---------------------
          |                   |
          ↓                   ↓
    Validation          Cleaning
          |
          ↓
    Feature Engineering
          |
          ↓
    Analytics Tables
          |
          ↓
    ML Feature Store
          |
          ↓
    Dashboard / Model
```

---

# 2. Project Structure

Production style:

```
ecommerce_pipeline/


│
├── data/

│   ├── raw/

│   └── processed/


│
├── src/

│
│── extract.py

│── validate.py

│── clean.py

│── feature_engineering.py

│── analytics.py

│── load.py


│
└── main.py

```

---

# 3. Raw Dataset

ধরি orders table:

| column      | meaning       |
| ----------- | ------------- |
| order_id    | Order ID      |
| customer_id | Customer      |
| product_id  | Product       |
| price       | Product price |
| quantity    | Quantity      |
| order_date  | Date          |
| category    | Category      |

---

# 4. Extract Layer

`extract.py`

```python
import pandas as pd


def extract_orders(engine):

    query = """

    SELECT *

    FROM orders

    """


    df = pd.read_sql(
        query,
        engine
    )


    return df
```

---

# 5. Validation Layer

`validate.py`

```python
def validate(df):

    errors = []


    if df["order_id"].isnull().any():

        errors.append(
            "Missing order id"
        )


    if (df["price"] < 0).any():

        errors.append(
            "Negative price"
        )


    if (df["quantity"] <=0).any():

        errors.append(
            "Invalid quantity"
        )


    return errors
```

---

# 6. Cleaning Layer

`clean.py`

```python
def clean(df):


    # duplicate remove

    df = df.drop_duplicates()


    # datatype fix

    df["order_date"] = (
        pd.to_datetime(
            df["order_date"]
        )
    )


    # remove invalid rows

    df = df[
        df["price"] > 0
    ]


    return df
```

---

# 7. Feature Engineering Layer

`feature_engineering.py`

```python
def create_features(df):


    # Revenue

    df["revenue"] = (

        df["price"]

        *

        df["quantity"]

    )


    # Date features


    df["year"] = (

        df["order_date"]

        .dt.year

    )


    df["month"] = (

        df["order_date"]

        .dt.month

    )


    return df
```

---

# 8. Customer Feature Creation

ML এর জন্য:

```python
def customer_features(df):


    customer = (

        df.groupby(
            "customer_id"
        )

        .agg(

        total_orders=(
            "order_id",
            "count"
        ),

        total_spent=(
            "revenue",
            "sum"
        ),

        avg_order_value=(
            "revenue",
            "mean"
        )

        )

    )


    return customer
```

---

# Output:

Customer Feature Table:

| customer | orders | spent | avg  |
| -------- | ------ | ----- | ---- |
| 101      | 20     | 50000 | 2500 |
| 102      | 10     | 20000 | 2000 |

---

# 9. Product Analytics

```python
def product_report(df):


    report = (

    df.groupby(
        "product_id"
    )

    .agg(

    sales=(
        "quantity",
        "sum"
    ),

    revenue=(
        "revenue",
        "sum"
    )

    )

    )


    return report
```

---

# 10. Monthly Sales Report

```python
def monthly_report(df):


    monthly = (

    df.groupby(
        "month"
    )

    ["revenue"]

    .sum()

    )


    return monthly
```

---

# 11. Load Layer

`load.py`

```python
def load(df, engine, table):


    df.to_sql(

        table,

        engine,

        if_exists="replace",

        index=False

    )
```

---

# 12. Main Pipeline

`main.py`

```python
from extract import extract_orders

from validate import validate

from clean import clean

from feature_engineering import create_features


orders = extract_orders(engine)



errors = validate(
    orders
)



if errors:

    print(errors)



orders = clean(
    orders
)



orders = create_features(
    orders
)



load(

orders,

engine,

"analytics_orders"

)

```

---

# 13. EDA Integration

Pipeline শেষে:

```python
orders.describe()
```

Check:

* Revenue distribution
* Outlier
* Missing data

---

Visualization:

```python
orders.groupby(
"month"
)["revenue"]
.sum()
.plot()
```

---

# 14. ML Dataset তৈরি

Customer churn model:

Feature table:

```
customer_id

total_orders

total_spent

avg_order_value

last_order_days

favorite_category

```

---

Split:

```python
from sklearn.model_selection import train_test_split


X_train, X_test = train_test_split(

customer_features,

test_size=0.2

)
```

---

# 15. Production Improvements

Real company pipeline এ add করা হয়:

## Logging

```python
import logging


logging.info(
"Pipeline Started"
)
```

---

## Error Handling

```python
try:

    run_pipeline()


except Exception as e:

    logging.error(e)
```

---

## Scheduling

Tools:

* Apache Airflow
* Prefect
* Dagster

Example:

```
Every day 2 AM

        ↓

Extract orders

        ↓

Generate report
```

---

# 16. Pandas Mastery Completed Skills

## Data Manipulation

✅ DataFrame
✅ Series
✅ Filtering
✅ Sorting
✅ Merge
✅ Join

---

## Data Cleaning

✅ Missing value
✅ Duplicate
✅ Datatype
✅ Outlier

---

## Analytics

✅ GroupBy
✅ Aggregation
✅ Pivot Table
✅ Window Function

---

## Data Engineering

✅ ETL Pipeline
✅ SQL Integration
✅ Validation
✅ Data Quality

---

## ML Preparation

✅ Feature Engineering
✅ Encoding
✅ Scaling
✅ Train-Test Split

---

## EDA

✅ Visualization
✅ Correlation
✅ Distribution Analysis

---

# Final Capstone Challenge

আপনার নিজের DRF E-commerce project ব্যবহার করুন:

Database:

```
users

products

orders

payments

reviews
```

Create:

## 1. Customer Analytics Table

```
customer_id

total_orders

total_spent

avg_order_value

last_purchase_date

```

---

## 2. Product Analytics Table

```
product_id

total_sales

quantity_sold

revenue

rating_average

```

---

## 3. ML Feature Table

```
customer_id

purchase_frequency

purchase_amount

days_since_last_purchase

customer_segment

```

---

# Congratulations 🎉

আপনি এখন Pandas এর:

**Beginner → Advanced → Data Engineering → ML Pipeline Level**

শেষ করেছেন।

পরবর্তী ধাপে আপনার জন্য সবচেয়ে logical হবে:

# Advanced Data Engineering Track

### Module 1:

**NumPy + Pandas Performance Optimization**

* Vectorization
* Memory optimization
* Large dataset processing

### Module 2:

**Pandas + PySpark**

* Big Data Processing
* Distributed Computing

### Module 3:

**Production Data Pipeline**

* Airflow
* Docker
* PostgreSQL
* Data Warehouse

### Module 4:

**ML Engineer Data Pipeline**

* Feature Store
* Model Training Pipeline
* MLOps

এগুলো শিখলে Data Engineer / ML Engineer দুই দিকেই strong foundation হবে।



