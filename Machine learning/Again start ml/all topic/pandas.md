Perfect 🚀 Let’s go **Pandas A → Z** with clear explanations + examples.  
Pandas is the **most important library** for data analysis in Python.

---

# 🐼 Pandas A → Z

### 1. Import Pandas

```python
import pandas as pd
```

---

## 🔹 A. Data Structures

### 1. Series (1D)

```python
s = pd.Series([10, 20, 30, 40], index=['a', 'b', 'c', 'd'])
print(s)
print(s['b'])   # 20
```

### 2. DataFrame (2D)

```python
data = {
    "Name": ["Atiar", "Rahim", "Karim"],
    "Age": [21, 22, 23],
    "Score": [85, 90, 95]
}
df = pd.DataFrame(data)
print(df)
```

---

## 🔹 B. Reading & Writing Data

```python
df = pd.read_csv("data.csv")       # read CSV
df.to_csv("output.csv", index=False)  # write CSV

df = pd.read_excel("data.xlsx")    # read Excel
df.to_excel("output.xlsx", index=False)

df = pd.read_json("data.json")     # read JSON
```

---

## 🔹 C. Inspecting Data

```python
print(df.head())       # first 5 rows
print(df.tail(3))      # last 3 rows
print(df.shape)        # (rows, cols)
print(df.info())       # data types
print(df.describe())   # statistics
print(df.columns)      # column names
print(df.index)        # row index
```

---

## 🔹 D. Selecting Data

```python
print(df["Name"])          # single column
print(df[["Name", "Score"]])  # multiple columns
print(df.iloc[0])          # first row (by index)
print(df.iloc[0:2])        # first two rows
print(df.loc[0, "Name"])   # specific cell
```

---

## 🔹 E. Filtering

```python
print(df[df["Age"] > 21])    # filter condition
print(df[(df["Age"] > 21) & (df["Score"] > 90)])
```

---

## 🔹 F. Adding & Modifying Data

```python
df["Grade"] = ["B", "A", "A+"]   # new column
df.loc[0, "Score"] = 88          # update value
df["Pass"] = df["Score"] > 50    # boolean column
```

---

## 🔹 G. Removing Data

```python
df = df.drop("Grade", axis=1)   # drop column
df = df.drop(0, axis=0)         # drop row
```

---

## 🔹 H. Sorting

```python
print(df.sort_values("Age"))         # sort by Age
print(df.sort_values("Score", ascending=False))  # descending
```

---

## 🔹 I. Grouping & Aggregation

```python
print(df.groupby("Age")["Score"].mean())   # avg score by age
print(df.groupby("Age").agg({"Score": ["mean", "max"]}))
```

---

## 🔹 J. Handling Missing Data

```python
df = pd.DataFrame({"Name": ["A", "B", None], "Age": [21, None, 23]})

print(df.isnull())        # check missing
df = df.fillna(0)         # replace with 0
df = df.fillna(df.mean(numeric_only=True))  # replace with mean
df = df.dropna()          # drop missing rows
```

---

## 🔹 K. Merging & Joining

```python
df1 = pd.DataFrame({"ID": [1, 2], "Name": ["A", "B"]})
df2 = pd.DataFrame({"ID": [1, 2], "Score": [90, 95]})

merged = pd.merge(df1, df2, on="ID")
print(merged)
```

---

## 🔹 L. Pivot Tables

```python
df = pd.DataFrame({
    "Name": ["A", "A", "B", "B"],
    "Subject": ["Math", "Science", "Math", "Science"],
    "Score": [85, 90, 78, 88]
})

pivot = pd.pivot_table(df, values="Score", index="Name", columns="Subject")
print(pivot)
```

---

## 🔹 M. Apply Functions

```python
df["Score_doubled"] = df["Score"].apply(lambda x: x * 2)
```

---

## 🔹 N. Date & Time

```python
dates = pd.date_range("2025-01-01", periods=5, freq="D")
print(dates)

df = pd.DataFrame({"Date": dates, "Value": [10, 20, 30, 40, 50]})
print(df.set_index("Date").resample("2D").sum())  # resample by 2 days
```

---

## 🔹 O. Visualization (with Matplotlib)

```python
import matplotlib.pyplot as plt

df["Score"].plot(kind="bar")
plt.show()
```

---

# ✅ Summary

Pandas helps with:

1. **Data Loading** (CSV, Excel, JSON, SQL, etc.)
    
2. **Cleaning & Filtering** (drop, fillna, replace)
    
3. **Transformation** (apply, map, groupby, pivot)
    
4. **Analysis** (stats, aggregation, sorting)
    
5. **Visualization** (plotting)
    

---

👉 Do you want me to make a **full Pandas A–Z practice notebook (step-by-step exercises with solutions)** so you can learn hands-on, like a mini crash course?

-----

Great question 👍 — `iloc` and `loc` are two of the most important indexers in **pandas**, but they work differently. Let’s break it down with **examples**:

---

## 🔹 1. `loc` → **Label-based indexing**

- Selects rows/columns by **labels** (names/index).
    
- Includes both **start and end** in slicing.
    
- Accepts **boolean masks** and **labels**.
    

### Example:

```python
import pandas as pd

# Sample DataFrame
data = {
    "Name": ["Alice", "Bob", "Charlie", "David"],
    "Age": [25, 30, 35, 40],
    "City": ["NY", "LA", "Chicago", "Houston"]
}
df = pd.DataFrame(data, index=["a", "b", "c", "d"])

print("DataFrame:\n", df)

# Using loc (label based)
print("\nRow with index 'b':\n", df.loc["b"])

print("\nRows from 'b' to 'd':\n", df.loc["b":"d"])

print("\nSelect 'Age' column:\n", df.loc[:, "Age"])

print("\nSelect rows where Age > 30:\n", df.loc[df["Age"] > 30])
```

✅ Output:

```
Row with index 'b':
Name      Bob
Age        30
City       LA
Name: b, dtype: object

Rows from 'b' to 'd':
    Name  Age     City
b    Bob   30       LA
c Charlie   35  Chicago
d  David   40  Houston

Select 'Age' column:
a    25
b    30
c    35
d    40
Name: Age, dtype: int64

Select rows where Age > 30:
      Name  Age     City
c  Charlie   35  Chicago
d    David   40  Houston
```

---

## 🔹 2. `iloc` → **Integer-based indexing**

- Selects rows/columns by **position (integer index)**.
    
- Works like Python’s normal list slicing (`start:end` → end **excluded**).
    
- Does **not** care about labels.
    

### Example:

```python
# Using iloc (integer position)
print("\nRow at position 1:\n", df.iloc[1])

print("\nRows from position 1 to 3:\n", df.iloc[1:3])

print("\nSelect 2nd column:\n", df.iloc[:, 1])

print("\nFirst two rows and first two columns:\n", df.iloc[0:2, 0:2])
```

✅ Output:

```
Row at position 1:
Name     Bob
Age       30
City      LA
Name: b, dtype: object

Rows from position 1 to 3:
      Name  Age     City
b      Bob   30       LA
c  Charlie   35  Chicago

Select 2nd column:
a    25
b    30
c    35
d    40
Name: Age, dtype: int64

First two rows and first two columns:
    Name  Age
a  Alice   25
b    Bob   30
```

---

## 🔑 Key Differences: `loc` vs `iloc`

|Feature|`loc` (Label)|`iloc` (Integer Position)|
|---|---|---|
|Index type|Labels (row/col names)|Integer positions|
|Slicing end|Inclusive|Exclusive|
|Boolean indexing|✅ Supported|❌ Not directly supported|
|Example|`df.loc["a":"c", "Age"]`|`df.iloc[0:3, 1]`|

---

👉 Rule of thumb:

- Use **`loc`** when you know the **labels** (row/column names).
    
- Use **`iloc`** when you know the **positions** (row/column numbers).
    

---

### data cleaning with pandas

Perfect 👍 Let’s go step by step through **data cleaning with pandas**. This is one of the most important skills for real-life ML and data analysis.

I’ll cover the **most common cleaning operations with examples**.

---

# 🧹 Data Cleaning with Pandas

```python
import pandas as pd
import numpy as np

# Sample raw data
data = {
    "Name": ["Alice", "Bob", None, "David", "Eve", "Frank", "Grace"],
    "Age": [25, np.nan, 35, 40, -5, 29, 30],
    "City": ["NY", "LA", "NY", None, "Chicago", "LA", "Houston"],
    "Salary": ["50000", "60000", "70000", "not available", "90000", "80000", None]
}

df = pd.DataFrame(data)
print("Raw Data:\n", df)
```

---

## 🔹 1. Handling Missing Data (NaN)

### Check missing values

```python
print(df.isnull().sum())
```

### Drop missing rows

```python
df_dropna = df.dropna()
```

### Fill missing values

```python
df["Name"] = df["Name"].fillna("Unknown")
df["City"] = df["City"].fillna("Unknown")
df["Age"] = df["Age"].fillna(df["Age"].mean())   # Fill with mean
```

---

## 🔹 2. Fixing Wrong Data

### Example: Age has a negative value (-5)

```python
df.loc[df["Age"] < 0, "Age"] = df["Age"].mean()
```

---

## 🔹 3. Converting Data Types

```python
# Salary column is string, needs conversion
df["Salary"] = pd.to_numeric(df["Salary"], errors="coerce")
```

(`errors="coerce"` will replace invalid values like `"not available"` with NaN)

---

## 🔹 4. Removing Duplicates

```python
df = df.drop_duplicates()
```

---

## 🔹 5. Renaming Columns

```python
df = df.rename(columns={"Name": "Employee_Name", "City": "Work_City"})
```

---

## 🔹 6. Handling Outliers

Example: remove salaries above 100k

```python
df = df[df["Salary"] <= 100000]
```

---

## 🔹 7. Standardizing Data

```python
# Trim spaces & convert to lowercase in city names
df["Work_City"] = df["Work_City"].str.strip().str.lower()
```

---

✅ Final Clean DataFrame:

```python
print(df)
```

---

# 📊 Common Cleaning Pipeline

```python
def clean_data(df):
    df = df.copy()
    
    # Handle missing values
    df["Name"].fillna("Unknown", inplace=True)
    df["City"].fillna("Unknown", inplace=True)
    df["Age"].fillna(df["Age"].mean(), inplace=True)

    # Fix negative ages
    df.loc[df["Age"] < 0, "Age"] = df["Age"].mean()

    # Convert salary
    df["Salary"] = pd.to_numeric(df["Salary"], errors="coerce")

    # Remove duplicates
    df.drop_duplicates(inplace=True)

    # Clean text
    df["City"] = df["City"].str.strip().str.title()

    return df

cleaned_df = clean_data(df)
print(cleaned_df)
```

---

👉 With these steps, you can handle **missing data, wrong values, types, outliers, and formatting**.

---
**regular expressions (regex)** with **pandas** (and Python `re` library) to **remove or replace unwanted patterns** in text data.

---

# 🔹 Using Regex in Python (`re` module)

```python
import re

text = "My phone number is 123-456-7890!"

# Remove all digits
clean_text = re.sub(r"\d", "", text)
print(clean_text)   # Output: My phone number is --!
```

---

# 🔹 Using Regex with Pandas

Suppose you have messy data:

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Alice123", "Bob_456", "Charlie!!", "David99"],
    "Email": ["alice@mail.com", "bob#test.com", "charlie@test.net", "david99@mail.com"]
})

print("Before Cleaning:\n", df)
```

---

## 1. Remove Digits

```python
df["Name"] = df["Name"].str.replace(r"\d+", "", regex=True)
```

Result → `["Alice", "Bob_", "Charlie!!", "David"]`

---

## 2. Remove Special Characters

```python
df["Name"] = df["Name"].str.replace(r"[^a-zA-Z]", "", regex=True)
```

Result → `["Alice", "Bob", "Charlie", "David"]`

---

## 3. Validate/Filter Emails

Remove rows with invalid emails:

```python
df = df[df["Email"].str.contains(r"^[\w\.-]+@[\w\.-]+\.\w+$", regex=True)]
```

---

## 4. Extract Specific Pattern

Example: extract only domain names from emails

```python
df["Domain"] = df["Email"].str.extract(r"@([\w\.-]+)")
```

---

✅ Final Cleaned DataFrame:

```python
print(df)
```

---

# ⚡ Common Regex for Cleaning

- `\d` → digits
    
- `\D` → non-digits
    
- `\w` → word characters (letters, numbers, `_`)
    
- `\W` → non-word characters
    
- `[^a-zA-Z0-9]` → keep only letters & numbers (remove special chars)
    
- `.+@.+\..+` → email-like pattern
    

---
 👍 Replacing values **pandas DataFrame column** is very common in data cleaning. You can do it in several ways depending on your need.

---

# 🔹 Example Data

```python
import pandas as pd

df = pd.DataFrame({
    "City": ["NY", "LA", "Chicago", "NY", "Houston", "LA"]
})
print(df)
```

---

## ✅ 1. Replace Single Value

```python
df["City"] = df["City"].replace("NY", "New York")
```

---

## ✅ 2. Replace Multiple Values (Dictionary)

```python
df["City"] = df["City"].replace({
    "NY": "New York",
    "LA": "Los Angeles"
})
```

---

## ✅ 3. Replace Using `map()` (good for categorical mapping)

```python
mapping = {"NY": "New York", "LA": "Los Angeles", "Chicago": "Chicago City"}
df["City"] = df["City"].map(mapping)
```

---

## ✅ 4. Replace Using Regex

```python
# Replace all city names that start with "N" → "North City"
df["City"] = df["City"].replace(r"^N.*", "North City", regex=True)
```

---

## ✅ 5. Replace Condition-Based (using `.loc`)

```python
# If city = "Houston" → replace with "H-Town"
df.loc[df["City"] == "Houston", "City"] = "H-Town"
```

---

### 🔎 Final Cleaned DataFrame

```python
print(df)
```

---

 👍 This is super useful in **data cleaning & feature engineering**.  
In **pandas**, you can replace or assign values in one column **based on conditions from another column** using `.loc`, `np.where`, or `.apply()`.

---

# 🔹 Example Data

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie", "David", "Eve"],
    "Age": [15, 22, 17, 35, 12]
})
print(df)
```

---

## ✅ 1. Using `.loc`

```python
# Create a new column "Category"
df.loc[df["Age"] < 18, "Category"] = "Minor"
df.loc[df["Age"] >= 18, "Category"] = "Adult"
```

---

## ✅ 2. Using `np.where`

```python
df["Category"] = np.where(df["Age"] < 18, "Minor", "Adult")
```

---

## ✅ 3. Using `.apply()` with Lambda

```python
df["Category"] = df["Age"].apply(lambda x: "Minor" if x < 18 else "Adult")
```

---

## ✅ 4. Multiple Conditions

```python
df["Group"] = np.where(df["Age"] < 13, "Child",
                np.where(df["Age"] < 20, "Teen", "Adult"))
```

---

# 🔎 Output

```
      Name  Age Category   Group
0    Alice   15    Minor    Teen
1      Bob   22    Adult   Adult
2  Charlie   17    Minor    Teen
3    David   35    Adult   Adult
4      Eve   12    Minor   Child
```

---
👍 **drop all rows that have empty (NaN) values in any column** and then **reset the index** so it’s clean.

---

# 🔹 Example Data

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "Name": ["Alice", None, "Charlie", "David", None],
    "Age": [25, np.nan, 35, None, 40],
    "City": ["NY", "LA", None, "Chicago", None]
})

print("Original DataFrame:\n", df)
```

---

## ✅ Drop Rows with Any Empty Value

```python
df_clean = df.dropna().reset_index(drop=True)
print("After Dropping NaN:\n", df_clean)
```

👉 `dropna()` removes rows with NaN  
👉 `reset_index(drop=True)` resets the index cleanly

---

## ✅ Drop Rows Only If All Values Are Empty

```python
df_clean2 = df.dropna(how="all").reset_index(drop=True)
```

---

## ✅ Drop Rows with Empty Values in Specific Columns

```python
df_clean3 = df.dropna(subset=["Name", "City"]).reset_index(drop=True)
```

---

### 🔎 Output (for dropna all rows with any NaN)

```
Original DataFrame:
      Name   Age     City
0   Alice  25.0       NY
1    None   NaN       LA
2 Charlie  35.0     None
3   David   NaN  Chicago
4    None  40.0     None

After Dropping NaN:
      Name   Age City
0   Alice  25.0   NY
```

---
Perfect 👍 If you want to **drop rows only when a specific column has empty (NaN) values**, you can use the `subset` option in `dropna()`.

---

# 🔹 Example Data

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "Name": ["Alice", None, "Charlie", "David", None],
    "Age": [25, np.nan, 35, None, 40],
    "City": ["NY", "LA", None, "Chicago", None]
})

print("Original DataFrame:\n", df)
```

---

## ✅ Drop Rows Where `Name` is Empty

```python
df_clean = df.dropna(subset=["Name"]).reset_index(drop=True)
print("After Dropping Empty 'Name':\n", df_clean)
```

---

## ✅ Drop Rows Where `Age` is Empty

```python
df_clean_age = df.dropna(subset=["Age"]).reset_index(drop=True)
print("After Dropping Empty 'Age':\n", df_clean_age)
```

---

## ✅ Drop Rows Where Either `Name` OR `City` is Empty

```python
df_clean_multi = df.dropna(subset=["Name", "City"]).reset_index(drop=True)
print("After Dropping Empty 'Name' or 'City':\n", df_clean_multi)
```

---

### 🔎 Example Output (`dropna(subset=["Name"])`)

```
Original DataFrame:
      Name   Age     City
0   Alice  25.0       NY
1    None   NaN       LA
2 Charlie  35.0     None
3   David   NaN  Chicago
4    None  40.0     None

After Dropping Empty 'Name':
      Name   Age     City
0   Alice  25.0       NY
1 Charlie  35.0     None
2   David   NaN  Chicago
```

---

👍**EDA** = **Exploratory Data Analysis**

It’s the **first step in data analysis**, where you **explore, summarize, and visualize** a dataset to understand:

- What the data looks like
    
- The size & structure
    
- Missing values
    
- Duplicates
    
- Summary statistics
    
- Outliers
    
- Relationships between columns
    

👉 In **pandas**, EDA is usually done with **basic inspection + summary functions**.

---

# 🔹 EDA with Pandas (Step by Step)

```python
import pandas as pd

# Example dataset
df = pd.DataFrame({
    "Name": ["Alice", "Bob", "Charlie", "David", "Eve", "Frank"],
    "Age": [25, 30, 35, 40, None, 29],
    "Salary": [50000, 60000, 70000, 80000, 90000, None],
    "City": ["NY", "LA", "NY", "Chicago", "LA", "Houston"]
})
```

---

## ✅ 1. Basic Info

```python
print(df.shape)       # Rows & columns
print(df.columns)     # Column names
print(df.info())      # Data types + missing values
print(df.head())      # First 5 rows
print(df.tail())      # Last 5 rows
```

---

## ✅ 2. Summary Statistics

```python
print(df.describe())       # Numerical summary (mean, std, min, max, etc.)
print(df["Age"].mean())    # Average age
print(df["Salary"].median()) # Median salary
```

---

## ✅ 3. Check Missing Values

```python
print(df.isnull().sum())
```

---

## ✅ 4. Check Duplicates

```python
print(df.duplicated().sum())
```

---

## ✅ 5. Value Counts (Categorical Data)

```python
print(df["City"].value_counts())
```

---

## ✅ 6. Correlation Between Columns

```python
print(df.corr(numeric_only=True))
```

---

## ✅ 7. Quick Visualization (using pandas + matplotlib)

```python
import matplotlib.pyplot as plt

df["Age"].hist(bins=5)       # Histogram
plt.show()

df["City"].value_counts().plot(kind="bar")  # Bar chart
plt.show()
```

---

# 🔎 EDA Summary

|Step|What You Check|
|---|---|
|Shape|Size of dataset|
|Info|Data types, nulls|
|Describe|Stats summary|
|Missing Values|NaN handling|
|Duplicates|Clean data|
|Value Counts|Distribution of categorical|
|Correlation|Relationships between numbers|
|Visualization|Patterns, trends, outliers|

---

👉 EDA helps you **clean data, find patterns, and decide next analysis/ML steps**.

---

 👍 Let’s break down **correlation** in pandas.

---

# 🔹 What is Correlation?

- **Correlation** measures the relationship between two numerical variables.
    
- It tells you **how strongly they move together**:
    
    - `+1` → Perfect positive correlation (as one increases, the other increases)
        
    - `-1` → Perfect negative correlation (as one increases, the other decreases)
        
    - `0` → No correlation
        

---

# 🔹 Correlation in Pandas

```python
import pandas as pd

# Example data
df = pd.DataFrame({
    "Age": [22, 25, 30, 35, 40, 45],
    "Salary": [25000, 30000, 40000, 45000, 50000, 60000],
    "Experience": [1, 3, 5, 7, 9, 12]
})

print(df)
```

---

## ✅ 1. Correlation Matrix

```python
print(df.corr())
```

👉 Output:

```
                 Age    Salary  Experience
Age         1.000000  0.986241    0.994979
Salary      0.986241  1.000000    0.979957
Experience  0.994979  0.979957    1.000000
```

---

## ✅ 2. Correlation with One Column

```python
print(df["Salary"].corr(df["Age"]))  # correlation between Salary & Age
```

---

## ✅ 3. Different Correlation Methods

By default, `.corr()` uses **Pearson correlation**. You can also use:

```python
df.corr(method="pearson")   # linear correlation
df.corr(method="spearman")  # rank correlation (monotonic)
df.corr(method="kendall")   # ordinal association
```

---

## ✅ 4. Correlation Heatmap (Visualization)

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
plt.show()
```

---

# 🔎 Summary

- Use `.corr()` to calculate correlation.
    
- `+` → variables move together
    
- `-` → one goes up, other goes down
    
- Use **heatmaps** to visualize relationships.
    

---

👍 You can **visualize correlation with a heatmap** in Python using **seaborn** (built on matplotlib).

---

# 🔹 Example: Correlation Heatmap with Pandas + Seaborn

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Example dataset
df = pd.DataFrame({
    "Age": [22, 25, 30, 35, 40, 45],
    "Salary": [25000, 30000, 40000, 45000, 50000, 60000],
    "Experience": [1, 3, 5, 7, 9, 12]
})

# Correlation matrix
corr_matrix = df.corr()

# Heatmap
plt.figure(figsize=(6,4))
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap")
plt.show()
```

---

# 🔎 Output

✅ A **colored matrix** where:

- Dark **red** = strong positive correlation (`+1`)
    
- Dark **blue** = strong negative correlation (`-1`)
    
- Near **white** = weak/no correlation (`0`)
    

---

# 🔹 Example Output Table (from dataset above)

```
             Age    Salary  Experience
Age         1.00     0.99        0.99
Salary      0.99     1.00        0.98
Experience  0.99     0.98        1.00
```

And the heatmap will show strong **red/orange** blocks (because all are highly correlated).

---

##### sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", fmt=".2f") [explain paramete]


👍 Let’s break down the parameters of

```python
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", fmt=".2f")
```

from **seaborn.heatmap()**.

---

# 🔹 Explanation of Parameters

### 1. `corr_matrix`

- This is the **data** you’re plotting (a Pandas DataFrame or NumPy array).
    
- In this case: `df.corr()` → correlation matrix of numerical columns.
    

---

### 2. `annot=True`

- Tells seaborn to **annotate each cell with text** (the numeric value).
    
- Default = `False` (no numbers inside).
    
- If `True`, you’ll see numbers written in the squares.
    
- You can also pass a matrix of the same shape (custom annotations).
    

---

### 3. `cmap="coolwarm"`

- Sets the **color map** (gradient of colors).
    
- `"coolwarm"` → blue (low/negative) → white (neutral) → red (high/positive).
    
- Other options: `"viridis"`, `"magma"`, `"Blues"`, `"RdYlGn"`, etc.
    

---

### 4. `fmt=".2f"`

- Format for the annotation text (inside the cells).
    
- `".2f"` means **floating-point number with 2 decimal places**.  
    Example: `0.986241` → `0.99`.
    
- You can also use:
    
    - `".0f"` → integer
        
    - `".1f"` → 1 decimal
        
    - `".2%"` → percentage with 2 decimals
        

---

# 🔎 Example Visualization

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd

df = pd.DataFrame({
    "A": [1,2,3,4,5],
    "B": [2,4,6,8,10],
    "C": [5,4,3,2,1]
})

corr_matrix = df.corr()

plt.figure(figsize=(6,4))
sns.heatmap(corr_matrix, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Correlation Heatmap")
plt.show()
```

👉 Output will show numbers like `1.00`, `-1.00`, etc. in red/blue squares.

---

⚡ Pro tip: You can add `linewidths=0.5` and `linecolor="black"` to separate cells nicely.

---

Would you like me to make a **table of the most useful `heatmap` parameters** (like `annot_kws`, `mask`, `vmin/vmax`, `linewidths` etc.) for quick reference?



