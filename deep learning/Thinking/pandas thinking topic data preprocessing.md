
# 🐼 Data Processing Techniques in Pandas (A–Z)

---

## 1️⃣ Data Loading (Input)

### ✔ Read data

```python
import pandas as pd

df = pd.read_csv("data.csv")
df = pd.read_excel("data.xlsx")
df = pd.read_json("data.json")
df = pd.read_sql(query, connection)
```

---

## 2️⃣ Data Inspection (Understanding Data)

### ✔ Basic info

```python
df.head()
df.tail()
df.shape
df.columns
df.info()
df.describe()
```

📌 **Purpose**: Dataset size, column types, missing values

---

## 3️⃣ Handling Missing Data

### ✔ Detect missing values

```python
df.isnull()
df.isnull().sum()
```

### ✔ Drop missing values

```python
df.dropna()
df.dropna(axis=1)
```

### ✔ Fill missing values

```python
df.fillna(0)
df.fillna(df.mean())
df['age'].fillna(df['age'].median())
```

---

## 4️⃣ Data Cleaning

### ✔ Remove duplicates

```python
df.duplicated()
df.drop_duplicates()
```

### ✔ Rename columns

```python
df.rename(columns={'old':'new'}, inplace=True)
```

### ✔ Change data type

```python
df['age'] = df['age'].astype(int)
```

---

## 5️⃣ Data Selection & Indexing

### ✔ Column selection

```python
df['name']
df[['name','age']]
```

### ✔ Row selection

```python
df.loc[0]
df.iloc[0]
df.loc[0:5]
```

### ✔ Conditional selection

```python
df[df['age'] > 18]
```

---

## 6️⃣ Sorting Data

```python
df.sort_values(by='age')
df.sort_values(by='age', ascending=False)
```

---

## 7️⃣ Filtering Data

```python
df[(df['age'] > 18) & (df['gender'] == 'Male')]
```

---

## 8️⃣ Data Transformation

### ✔ Apply function

```python
df['salary'] = df['salary'].apply(lambda x: x*1.1)
```

### ✔ Map values

```python
df['gender'] = df['gender'].map({'M':0, 'F':1})
```

---

## 9️⃣ Feature Engineering (ML Important ⭐)

### ✔ Create new column

```python
df['BMI'] = df['weight'] / (df['height']**2)
```

### ✔ Binning

```python
df['age_group'] = pd.cut(df['age'], bins=[0,18,40,60,100])
```

---

## 🔟 Encoding Categorical Data

### ✔ Label Encoding

```python
df['gender'] = df['gender'].astype('category').cat.codes
```

### ✔ One-Hot Encoding

```python
pd.get_dummies(df, columns=['city'])
```

---

## 1️⃣1️⃣ Grouping & Aggregation

```python
df.groupby('gender')['salary'].mean()
df.groupby('city').agg({'salary':'mean','age':'max'})
```

📌 Used in **EDA & analytics**

---

## 1️⃣2️⃣ Merging & Joining Data

### ✔ Merge

```python
pd.merge(df1, df2, on='id', how='inner')
```

### ✔ Join

```python
df1.join(df2)
```

---

## 1️⃣3️⃣ Concatenation

```python
pd.concat([df1, df2], axis=0)
```

---

## 1️⃣4️⃣ Handling Date & Time

```python
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
```

---

## 1️⃣5️⃣ Scaling / Normalization (ML Prep)

```python
df['age_norm'] = (df['age'] - df['age'].min()) / (df['age'].max() - df['age'].min())
```

---

## 1️⃣6️⃣ Outlier Detection

```python
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

df = df[(df['salary'] >= Q1 - 1.5*IQR) & (df['salary'] <= Q3 + 1.5*IQR)]
```

---

## 1️⃣7️⃣ Sampling Data

```python
df.sample(n=100)
df.sample(frac=0.2)
```

---

## 1️⃣8️⃣ Export Data (Output)

```python
df.to_csv("cleaned.csv", index=False)
df.to_excel("cleaned.xlsx")
```

---

## 🔚 Complete Data Processing Pipeline (Example)

```python
df = pd.read_csv("data.csv")
df.drop_duplicates(inplace=True)
df.fillna(df.mean(), inplace=True)
df = pd.get_dummies(df, drop_first=True)
```

---

## 🧠 Exam Summary (5 Marks)

> Pandas provides various data processing techniques such as data loading, cleaning, handling missing values, transformation, encoding, grouping, merging, and exporting. These techniques help prepare raw data into clean and structured form suitable for analysis and machine learning.

---

# 🐼 Pandas Practice Problems + Solutions (50)

Assume:

```python
import pandas as pd
import numpy as np

df = pd.read_csv("data.csv")
```

---

## 🟢 EASY (1–15)

### 1️⃣ Load CSV file

```python
df = pd.read_csv("data.csv")
```

### 2️⃣ Show first 5 rows

```python
df.head()
```

### 3️⃣ Show last 10 rows

```python
df.tail(10)
```

### 4️⃣ Number of rows & columns

```python
df.shape
```

### 5️⃣ Column names

```python
df.columns
```

### 6️⃣ Dataset info

```python
df.info()
```

### 7️⃣ Summary statistics

```python
df.describe()
```

### 8️⃣ Select one column

```python
df['age']
```

### 9️⃣ Select multiple columns

```python
df[['name', 'salary']]
```

### 🔟 Check missing values

```python
df.isnull().sum()
```

### 1️⃣1️⃣ Fill missing values with 0

```python
df.fillna(0, inplace=True)
```

### 1️⃣2️⃣ Drop rows with missing values

```python
df.dropna(inplace=True)
```

### 1️⃣3️⃣ Remove duplicates

```python
df.drop_duplicates(inplace=True)
```

### 1️⃣4️⃣ Sort by age

```python
df.sort_values(by='age')
```

### 1️⃣5️⃣ Sort salary descending

```python
df.sort_values(by='salary', ascending=False)
```

---

## 🟡 MEDIUM (16–35)

### 1️⃣6️⃣ Filter age > 30

```python
df[df['age'] > 30]
```

### 1️⃣7️⃣ Filter multiple conditions

```python
df[(df['age'] > 25) & (df['gender'] == 'Male')]
```

### 1️⃣8️⃣ Rename column

```python
df.rename(columns={'old_name':'new_name'}, inplace=True)
```

### 1️⃣9️⃣ Change datatype

```python
df['age'] = df['age'].astype(int)
```

### 2️⃣0️⃣ Add new column

```python
df['bonus'] = df['salary'] * 0.1
```

### 2️⃣1️⃣ Apply function

```python
df['salary'] = df['salary'].apply(lambda x: x+500)
```

### 2️⃣2️⃣ Replace values

```python
df['gender'].replace({'M':'Male','F':'Female'}, inplace=True)
```

### 2️⃣3️⃣ Unique values

```python
df['city'].unique()
```

### 2️⃣4️⃣ Value counts

```python
df['city'].value_counts()
```

### 2️⃣5️⃣ Group by city (mean salary)

```python
df.groupby('city')['salary'].mean()
```

### 2️⃣6️⃣ Multiple aggregation

```python
df.groupby('gender').agg({'salary':'mean','age':'max'})
```

### 2️⃣7️⃣ Count per group

```python
df.groupby('city').size()
```

### 2️⃣8️⃣ One-hot encoding

```python
pd.get_dummies(df, columns=['city'])
```

### 2️⃣9️⃣ Label encoding

```python
df['gender'] = df['gender'].astype('category').cat.codes
```

### 3️⃣0️⃣ Random sample (10 rows)

```python
df.sample(10)
```

### 3️⃣1️⃣ Fraction sample (20%)

```python
df.sample(frac=0.2)
```

### 3️⃣2️⃣ Index reset

```python
df.reset_index(drop=True, inplace=True)
```

### 3️⃣3️⃣ Set column as index

```python
df.set_index('id', inplace=True)
```

### 3️⃣4️⃣ Export to CSV

```python
df.to_csv("cleaned.csv", index=False)
```

### 3️⃣5️⃣ Check correlation

```python
df.corr(numeric_only=True)
```

---

## 🔴 ADVANCED (36–50)

### 3️⃣6️⃣ Convert string to datetime

```python
df['date'] = pd.to_datetime(df['date'])
```

### 3️⃣7️⃣ Extract year

```python
df['year'] = df['date'].dt.year
```

### 3️⃣8️⃣ Filter by date

```python
df[df['date'] > '2024-01-01']
```

### 3️⃣9️⃣ Merge two DataFrames

```python
pd.merge(df1, df2, on='id', how='inner')
```

### 4️⃣0️⃣ Concatenate DataFrames

```python
pd.concat([df1, df2])
```

### 4️⃣1️⃣ Detect outliers (IQR)

```python
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1
df[(df['salary'] >= Q1 - 1.5*IQR) & (df['salary'] <= Q3 + 1.5*IQR)]
```

### 4️⃣2️⃣ Normalize column

```python
df['salary_norm'] = (df['salary']-df['salary'].min()) / (df['salary'].max()-df['salary'].min())
```

### 4️⃣3️⃣ Binning age

```python
df['age_group'] = pd.cut(df['age'], bins=[0,18,40,60,100])
```

### 4️⃣4️⃣ Rank values

```python
df['salary_rank'] = df['salary'].rank()
```

### 4️⃣5️⃣ Rolling mean

```python
df['rolling_avg'] = df['salary'].rolling(3).mean()
```

### 4️⃣6️⃣ Apply function row-wise

```python
df.apply(lambda x: x['salary']*2 if x['age']>30 else x['salary'], axis=1)
```

### 4️⃣7️⃣ Conditional column

```python
df['status'] = np.where(df['salary'] > 50000, 'High', 'Low')
```

### 4️⃣8️⃣ Pivot table

```python
pd.pivot_table(df, values='salary', index='city', columns='gender', aggfunc='mean')
```

### 4️⃣9️⃣ Memory usage

```python
df.memory_usage(deep=True)
```

### 5️⃣0️⃣ Complete cleaning pipeline

```python
df = (
    df.drop_duplicates()
      .fillna(df.mean(numeric_only=True))
      .reset_index(drop=True)
)
```

---

## 🎯 Exam Tip (5 Marks)

> Pandas provides powerful tools for data loading, cleaning, filtering, transformation, aggregation, and feature engineering which are essential for data analysis and machine learning.

---

 
#  I’ll show you a **REAL-WORLD dataset cleaning workflow (step-by-step)** exactly how it’s done in **industry ML / Data Science projects**.

I’ll use a **realistic messy dataset** (like Employee / Customer / Medical / ML dataset).

---

# 🧹 Real Project Dataset Cleaning (Step-by-Step)

## 🎯 Project Scenario

**Problem:**  
We have a **raw dataset** collected from different sources.  
It contains:

- Missing values
    
- Wrong data types
    
- Duplicates
    
- Outliers
    
- Categorical data
    
- Date columns
    
- Inconsistent values
    

Goal 👉 **Clean & prepare data for ML model**

---

## 📁 STEP 0: Load Dataset

```python
import pandas as pd
import numpy as np

df = pd.read_csv("raw_data.csv")
```

---

## 🔍 STEP 1: Understand the Dataset (EDA)

```python
df.head()
df.tail()
df.shape
df.columns
df.info()
df.describe()
```

✔ Identify:

- Missing values
    
- Datatypes
    
- Numerical vs categorical
    
- Wrong columns
    

---

## ❌ STEP 2: Remove Duplicate Records

```python
df.duplicated().sum()
df.drop_duplicates(inplace=True)
```

📌 **Why?**  
Duplicates bias ML models.

---

## 🚫 STEP 3: Handle Missing Values

### 🔹 Check missing values

```python
df.isnull().sum()
```

### 🔹 Numerical columns → mean / median

```python
df['age'].fillna(df['age'].median(), inplace=True)
df['salary'].fillna(df['salary'].mean(), inplace=True)
```

### 🔹 Categorical columns → mode

```python
df['gender'].fillna(df['gender'].mode()[0], inplace=True)
```

### 🔹 Drop column if too many missing

```python
df.drop(columns=['useless_column'], inplace=True)
```

---

## 🔄 STEP 4: Fix Data Types

```python
df['age'] = df['age'].astype(int)
df['salary'] = df['salary'].astype(float)
```

### Date column

```python
df['join_date'] = pd.to_datetime(df['join_date'], errors='coerce')
```

---

## 🧽 STEP 5: Clean Text & Categorical Data

### 🔹 Standardize values

```python
df['gender'] = df['gender'].str.lower().str.strip()
df['gender'].replace({'m':'male','f':'female'}, inplace=True)
```

### 🔹 Fix inconsistent city names

```python
df['city'] = df['city'].str.title()
```

---

## 🚨 STEP 6: Handle Outliers (IQR Method)

```python
Q1 = df['salary'].quantile(0.25)
Q3 = df['salary'].quantile(0.75)
IQR = Q3 - Q1

df = df[(df['salary'] >= Q1 - 1.5*IQR) & 
        (df['salary'] <= Q3 + 1.5*IQR)]
```

📌 **Why?**  
Outliers destroy ML accuracy.

---

## 🧠 STEP 7: Feature Engineering

### 🔹 New features

```python
df['experience_level'] = pd.cut(
    df['experience'],
    bins=[0,2,5,10,40],
    labels=['Junior','Mid','Senior','Expert']
)
```

### 🔹 Date features

```python
df['join_year'] = df['join_date'].dt.year
df['join_month'] = df['join_date'].dt.month
```

---

## 🔠 STEP 8: Encode Categorical Features (ML Ready)

### 🔹 Label Encoding

```python
df['gender'] = df['gender'].astype('category').cat.codes
```

### 🔹 One-Hot Encoding

```python
df = pd.get_dummies(df, columns=['city','experience_level'], drop_first=True)
```

---

## 📏 STEP 9: Scaling / Normalization

```python
df['salary_norm'] = (
    df['salary'] - df['salary'].min()
) / (
    df['salary'].max() - df['salary'].min()
)
```

---

## 🧪 STEP 10: Final Validation Check

```python
df.isnull().sum()
df.info()
df.describe()
```

✔ No missing values  
✔ Correct datatypes  
✔ ML-ready numeric data

---

## 💾 STEP 11: Save Clean Dataset

```python
df.to_csv("cleaned_data.csv", index=False)
```

---

## 🚀 COMPLETE PIPELINE (Industry Style)

```python
df = (
    pd.read_csv("raw_data.csv")
      .drop_duplicates()
      .assign(
          age=lambda x: x['age'].fillna(x['age'].median()),
          salary=lambda x: x['salary'].fillna(x['salary'].mean())
      )
)

df.to_csv("cleaned_data.csv", index=False)
```

---

## 🧠 Interview / Viva Ready Summary (5 Marks)

> In a real project, dataset cleaning involves removing duplicates, handling missing values, fixing data types, cleaning categorical data, detecting outliers, performing feature engineering, encoding categorical features, scaling numerical values, and validating the dataset before saving it for model training.

---

# 🚨 Data Cleaning Mistakes Interviewers Ask (With Correct Answers)

---

## 1️⃣ Deleting Rows Without Analysis ❌

### ❌ Mistake

```python
df.dropna(inplace=True)
```

### ❓ Why wrong?

You may delete **important data** and introduce **bias**.

### ✅ Correct Answer

> Analyze missing pattern first, then decide fill or drop.

```python
df.isnull().sum()
df['age'].fillna(df['age'].median(), inplace=True)
```

---

## 2️⃣ Filling All Missing Values With Mean ❌

### ❌ Mistake

```python
df.fillna(df.mean(), inplace=True)
```

### ❓ Why wrong?

Mean is bad for **skewed data & categorical features**.

### ✅ Correct

- Mean → normal distribution
    
- Median → skewed
    
- Mode → categorical
    

---

## 3️⃣ Ignoring Duplicate Records ❌

### ❌ Mistake

Not checking duplicates at all.

### ❓ Why wrong?

Duplicates distort **statistics & ML training**.

### ✅ Correct

```python
df.duplicated().sum()
df.drop_duplicates(inplace=True)
```

---

## 4️⃣ Not Checking Data Types ❌

### ❌ Mistake

Treating numeric column as object.

### ❓ Why wrong?

Math operations fail or give wrong results.

### ✅ Correct

```python
df.info()
df['salary'] = df['salary'].astype(float)
```

---

## 5️⃣ Removing Outliers Blindly ❌

### ❌ Mistake

```python
df = df[df['salary'] < 100000]
```

### ❓ Why wrong?

Outliers may be **valid business cases**.

### ✅ Correct

> Understand domain before removal.

Use IQR or Z-score **with justification**.

---

## 6️⃣ Encoding Categorical Data Incorrectly ❌

### ❌ Mistake

Label encoding unordered categories.

### ❓ Why wrong?

Introduces **false order**.

### ✅ Correct

- Nominal → One-Hot
    
- Ordinal → Label
    

```python
pd.get_dummies(df, columns=['city'])
```

---

## 7️⃣ Data Leakage ❌🔥 (Very Important)

### ❌ Mistake

Scaling before train-test split.

### ❓ Why wrong?

Model sees test data information.

### ✅ Correct

> Always split first, then scale.

```python
from sklearn.preprocessing import StandardScaler
```

---

## 8️⃣ Dropping Columns Without Understanding ❌

### ❌ Mistake

```python
df.drop(columns=['id'])
```

### ❓ Why wrong?

Column may be useful for joins or tracking.

### ✅ Correct

> Drop only non-informative features.

---

## 9️⃣ Not Handling Inconsistent Text ❌

### ❌ Mistake

```text
Male, male, MALE
```

### ❓ Why wrong?

Creates multiple categories.

### ✅ Correct

```python
df['gender'] = df['gender'].str.lower().str.strip()
```

---

## 🔟 Ignoring Date-Time Features ❌

### ❌ Mistake

Using date as string.

### ❓ Why wrong?

You miss time patterns.

### ✅ Correct

```python
df['date'] = pd.to_datetime(df['date'])
df['year'] = df['date'].dt.year
```

---

## 1️⃣1️⃣ Over-Cleaning Data ❌

### ❌ Mistake

Removing too much data.

### ❓ Why wrong?

Loss of information → poor model.

### ✅ Correct

> Balance cleanliness & data richness.

---

## 1️⃣2️⃣ Not Validating After Cleaning ❌

### ❌ Mistake

Saving dataset without checking.

### ❓ Why wrong?

Hidden issues remain.

### ✅ Correct

```python
df.isnull().sum()
df.describe()
df.info()
```

---

## 1️⃣3️⃣ Ignoring Class Imbalance ❌

### ❌ Mistake

Training without checking target distribution.

### ❓ Why wrong?

Model becomes biased.

### ✅ Correct

```python
df['target'].value_counts(normalize=True)
```

---

## 1️⃣4️⃣ Cleaning Train and Test Separately ❌

### ❌ Mistake

Different preprocessing logic.

### ❓ Why wrong?

Inconsistent model behavior.

### ✅ Correct

> Use **same pipeline**.

---

## 1️⃣5️⃣ Not Saving Cleaning Steps ❌

### ❌ Mistake

Manual cleaning without reproducibility.

### ❓ Why wrong?

Impossible to debug or deploy.

### ✅ Correct

> Use scripts or pipelines.

---

# ⭐ TOP 5 MOST ASKED (Remember These)

1️⃣ Data leakage  
2️⃣ Missing value strategy  
3️⃣ Outlier handling  
4️⃣ Encoding mistake  
5️⃣ Over-cleaning data

---

## 🎯 Interview One-Line Answer (Golden)

> Data cleaning mistakes include improper handling of missing values, ignoring duplicates, incorrect encoding, data leakage, and removing outliers without domain understanding, all of which can negatively impact model performance.

---

# 🤖 Automated Data Cleaning Pipeline (Industry Standard)

## 🎯 What is an Automated Data Cleaning Pipeline?

> A reusable system that **automatically cleans raw data** using predefined rules so that the **same logic is applied every time** (no manual mistakes).

✅ Reproducible  
✅ Scalable  
✅ ML-ready  
✅ Interview favorite topic

---

## 🧠 What This Pipeline Will Handle

- Remove duplicates
    
- Handle missing values (numeric & categorical)
    
- Fix data types
    
- Clean text columns
    
- Handle outliers
    
- Encode categorical features
    
- Scale numeric features
    
- Prevent data leakage
    

---

# 🔹 STEP 1: Import Libraries

```python
import pandas as pd
import numpy as np
```

---

# 🔹 STEP 2: Create a Cleaning Configuration (Very Important)

This makes it **flexible & reusable**.

```python
CONFIG = {
    "drop_columns": ["unnecessary_column"],
    "numeric_fill": "median",   # mean / median
    "categorical_fill": "mode",
    "outlier_method": "iqr",    # iqr / none
    "encode": "onehot",         # onehot / label
}
```

---

# 🔹 STEP 3: Define Cleaning Functions

### 1️⃣ Remove duplicates

```python
def remove_duplicates(df):
    return df.drop_duplicates()
```

---

### 2️⃣ Handle missing values

```python
def handle_missing_values(df):
    for col in df.columns:
        if df[col].dtype in ['int64','float64']:
            if CONFIG["numeric_fill"] == "median":
                df[col].fillna(df[col].median(), inplace=True)
            else:
                df[col].fillna(df[col].mean(), inplace=True)
        else:
            df[col].fillna(df[col].mode()[0], inplace=True)
    return df
```

---

### 3️⃣ Fix data types

```python
def fix_data_types(df):
    for col in df.columns:
        if df[col].dtype == 'object':
            try:
                df[col] = pd.to_numeric(df[col])
            except:
                pass
    return df
```

---

### 4️⃣ Clean text columns

```python
def clean_text(df):
    for col in df.select_dtypes(include='object'):
        df[col] = df[col].str.lower().str.strip()
    return df
```

---

### 5️⃣ Handle outliers (IQR)

```python
def remove_outliers(df):
    if CONFIG["outlier_method"] != "iqr":
        return df

    for col in df.select_dtypes(include=['int64','float64']):
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        df = df[(df[col] >= Q1 - 1.5*IQR) &
                (df[col] <= Q3 + 1.5*IQR)]
    return df
```

---

### 6️⃣ Encode categorical features

```python
def encode_features(df):
    if CONFIG["encode"] == "onehot":
        df = pd.get_dummies(df, drop_first=True)
    else:
        for col in df.select_dtypes(include='object'):
            df[col] = df[col].astype('category').cat.codes
    return df
```

---

# 🔹 STEP 4: Build the Pipeline Function

```python
def clean_data_pipeline(df):
    df = remove_duplicates(df)
    df = df.drop(columns=CONFIG["drop_columns"], errors='ignore')
    df = handle_missing_values(df)
    df = fix_data_types(df)
    df = clean_text(df)
    df = remove_outliers(df)
    df = encode_features(df)
    df.reset_index(drop=True, inplace=True)
    return df
```

---

# 🔹 STEP 5: Run Pipeline on Raw Data

```python
raw_df = pd.read_csv("raw_data.csv")

clean_df = clean_data_pipeline(raw_df)

clean_df.to_csv("cleaned_data.csv", index=False)
```

---

# 🔥 BONUS: ML-SAFE PIPELINE (No Data Leakage)

> Interviewers LOVE this answer.

```python
from sklearn.model_selection import train_test_split

X = df.drop('target', axis=1)
y = df['target']

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

👉 **Cleaning & scaling must be fitted on TRAIN only**

---

# 🧠 Interview Explanation (Golden Answer)

> An automated data cleaning pipeline is a reusable preprocessing workflow that removes duplicates, handles missing values, fixes data types, cleans text, treats outliers, encodes categorical features, and prepares data consistently for machine learning while preventing data leakage.

---

দারুণ প্রশ্ন 👍
তুমি যেহেতু **pandas basic + filtering + assignment** শিখছো, তাই নিচের জিনিসগুলো **এখনই জানা খুব জরুরি**। এগুলো জানলে 80–90% real-world pandas কাজ কভার হয়ে যাবে।

আমি **exam + project + interview**—সব দিক মাথায় রেখে দিচ্ছি।

---

# ✅ Pandas MUST-KNOW Topics (Priority List)

## 🔥 1. `.loc` vs `.iloc` (সবচেয়ে important)

```python
df.loc[rows, columns]     # label based
df.iloc[rows, columns]    # index based
```

Example:

```python
df.loc[df['age'] > 30, 'salary'] = 50000
df.iloc[0:5, 1:3]
```

🧠 Rule:

* condition থাকলে → `.loc`
* index number থাকলে → `.iloc`

---

## 🔥 2. Missing Values (NaN handling)

```python
df.isna()
df.isna().sum()

df.fillna(0)
df.fillna(df.mean(numeric_only=True))

df.dropna()
df.dropna(axis=1)
```

---

## 🔥 3. `apply()` vs `map()` vs `applymap()`

### 🔹 map → single column

```python
df['grade'] = df['mark'].map(lambda x: 'Pass' if x>=40 else 'Fail')
```

### 🔹 apply → row / column

```python
df['status'] = df.apply(lambda r: 'Adult' if r['age']>=18 else 'Child', axis=1)
```

### 🔹 applymap → whole DataFrame

```python
df.applymap(str)
```

---

## 🔥 4. `groupby()` (MOST USED)

```python
df.groupby('city')['salary'].mean()
df.groupby('city').agg({
    'salary':'mean',
    'age':'max'
})
```

🔥 Real use:

* report
* analytics
* ML feature engineering

---

## 🔥 5. Sorting & Ranking

```python
df.sort_values('age')
df.sort_values('salary', ascending=False)

df['rank'] = df['salary'].rank(ascending=False)
```

---

## 🔥 6. String Operations (`str`)

```python
df['name'].str.lower()
df['email'].str.contains('gmail')
df['phone'].str.replace('-', '')
df['name'].str.split().str[0]
```

---

## 🔥 7. Date & Time

```python
df['date'] = pd.to_datetime(df['date'])

df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
df['day'] = df['date'].dt.day
```

---

## 🔥 8. Conditional Column Creation

```python
import numpy as np

df['status'] = np.where(df['age'] >= 18, 'Adult', 'Minor')
```

---

## 🔥 9. Duplicates

```python
df.duplicated()
df.drop_duplicates()
df.drop_duplicates(subset=['email'])
```

---

## 🔥 10. Merge / Join / Concat (DATABASE LEVEL)

### 🔹 merge

```python
pd.merge(df1, df2, on='id', how='inner')
```

### 🔹 concat

```python
pd.concat([df1, df2], axis=0)
```

---

## 🔥 11. Value Counts & Unique

```python
df['city'].value_counts()
df['city'].unique()
df['city'].nunique()
```

---

## 🔥 12. Performance Tricks (Important)

❌ Avoid:

```python
for i in df:
    ...
```

✅ Use:

```python
vectorized operations
```

---

# 🧠 EXAM / INTERVIEW Golden Rules

* Always use `& | ~` not `and or not`
* Every condition → `( )`
* Column assignment → Series only
* Prefer `.loc` for safe assignment
* Avoid chained indexing

---

# 🚀 Next Step (Suggested)

যেহেতু তুমি:

* ML project করছো
* Django / FastAPI backend বানাচ্ছো
* Dataset নিয়ে কাজ করো

👉 পরের ধাপে শেখা উচিত:

1. **EDA (Exploratory Data Analysis)**
2. **Feature Engineering with pandas**
3. **Time-series data handling**
4. **Memory optimization (`astype`, `category`)**

---

চমৎকার 👍  
নিচে তোমার জন্য **30টা Pandas Practice Problem + Full Solution** দিলাম।  
👉 **Beginner → Intermediate → Advanced** লেভেলে সাজানো  
👉 **Exam + Interview + Real Project**—সব কাজে লাগবে

---

# 🟢 BASIC (1–10)

### 1️⃣ CSV file load করো

```python
df = pd.read_csv("data.csv")
```

---

### 2️⃣ First 5 rows দেখাও

```python
df.head()
```

---

### 3️⃣ Column names দেখাও

```python
df.columns
```

---

### 4️⃣ DataFrame shape দেখাও

```python
df.shape
```

---

### 5️⃣ age column-এর max value

```python
df['age'].max()
```

---

### 6️⃣ salary column-এর mean

```python
df['salary'].mean()
```

---

### 7️⃣ age > 30 rows filter করো

```python
df[df['age'] > 30]
```

---

### 8️⃣ gender = "Male" rows

```python
df[df['gender'] == 'Male']
```

---

### 9️⃣ Missing value count

```python
df.isna().sum()
```

---

### 🔟 Duplicate rows remove

```python
df.drop_duplicates()
```

---

# 🟡 INTERMEDIATE (11–20)

### 1️⃣1️⃣ age 25–40 range

```python
df[(df['age'] >= 25) & (df['age'] <= 40)]
```

---

### 1️⃣2️⃣ New column: Adult / Minor

```python
df['status'] = np.where(df['age'] >= 18, 'Adult', 'Minor')
```

---

### 1️⃣3️⃣ salary NaN → mean

```python
df['salary'].fillna(df['salary'].mean(), inplace=True)
```

---

### 1️⃣4️⃣ Sort by salary descending

```python
df.sort_values('salary', ascending=False)
```

---

### 1️⃣5️⃣ city-wise average salary

```python
df.groupby('city')['salary'].mean()
```

---

### 1️⃣6️⃣ Multiple aggregation

```python
df.groupby('city').agg({
    'salary':'mean',
    'age':'max'
})
```

---

### 1️⃣7️⃣ salary rank create

```python
df['rank'] = df['salary'].rank(ascending=False)
```

---

### 1️⃣8️⃣ name column lowercase

```python
df['name'] = df['name'].str.lower()
```

---

### 1️⃣9️⃣ email contains gmail

```python
df[df['email'].str.contains('gmail', na=False)]
```

---

### 2️⃣0️⃣ duplicate email remove

```python
df.drop_duplicates(subset='email')
```

---

# 🔴 ADVANCED (21–30)

### 2️⃣1️⃣ date column → datetime

```python
df['date'] = pd.to_datetime(df['date'])
```

---

### 2️⃣2️⃣ year & month extract

```python
df['year'] = df['date'].dt.year
df['month'] = df['date'].dt.month
```

---

### 2️⃣3️⃣ Conditional salary update

```python
df.loc[df['age'] > 40, 'salary'] *= 1.1
```

---

### 2️⃣4️⃣ Apply function (row-wise)

```python
df['category'] = df.apply(
    lambda r: 'High' if r['salary'] > 50000 else 'Low',
    axis=1
)
```

---

### 2️⃣5️⃣ Merge two DataFrames

```python
pd.merge(df1, df2, on='id', how='inner')
```

---

### 2️⃣6️⃣ Concatenate rows

```python
pd.concat([df1, df2], axis=0)
```

---

### 2️⃣7️⃣ Value counts of city

```python
df['city'].value_counts()
```

---

### 2️⃣8️⃣ Top 3 salary per city

```python
df.sort_values('salary', ascending=False)\
  .groupby('city')\
  .head(3)
```

---

### 2️⃣9️⃣ Memory optimization

```python
df['city'] = df['city'].astype('category')
```

---

### 3️⃣0️⃣ Replace values

```python
df['gender'] = df['gender'].replace({'M':'Male', 'F':'Female'})
```

---

# 🧠 FINAL EXAM CHEAT RULES

✔ Always use `( )` in conditions  
✔ Use `& | ~` not `and or`  
✔ Prefer `.loc` for assignment  
✔ Avoid loops  
✔ Think vectorized

---

যদি চাও, আমি পরের ধাপে দিতে পারি:  
🔥 **10টা Trick Question**  
🔥 **Mini EDA Project (real dataset)**  
🔥 **Interview Q&A PDF style**

বললেই শুরু করে দেবো 👍



-------
দারুণ 👍
এখন আমি তোমাকে **🔥 Mini EDA Project (Real Dataset)** দিচ্ছি — **step-by-step + exam/interview ready**।

আমরা ব্যবহার করবো খুব জনপ্রিয় **Titanic Dataset**
👉 Real-world
👉 ML + Pandas শেখার জন্য BEST
👉 Interview-এ সবাই চেনে

---

# 🔥 Mini EDA Project

## 📌 Project Title

**Exploratory Data Analysis (EDA) on Titanic Dataset**

---

## 🎯 Objective

* Passenger data explore করা
* Survival-এর pattern বোঝা
* Missing data handle করা
* Feature understanding

---

## 📂 Dataset Columns (Important)

| Column   | Meaning         |
| -------- | --------------- |
| Survived | 0 = No, 1 = Yes |
| Pclass   | Ticket class    |
| Sex      | Gender          |
| Age      | Age             |
| Fare     | Ticket price    |
| Embarked | Port (C, Q, S)  |

---

## 🧪 Step 1: Dataset Load

```python
import pandas as pd
import numpy as np

df = pd.read_csv("titanic.csv")
```

---

## 🧪 Step 2: Basic Inspection

```python
df.head()
df.shape
df.info()
df.describe()
```

🧠 Question:

* Total rows?
* Which columns numeric?

---

## 🧪 Step 3: Missing Values Check

```python
df.isna().sum()
```

🔍 Observation:

* `Age` → missing
* `Cabin` → too many missing

---

## 🧪 Step 4: Handle Missing Data

### 🔹 Age → median

```python
df['Age'].fillna(df['Age'].median(), inplace=True)
```

### 🔹 Cabin drop

```python
df.drop(columns=['Cabin'], inplace=True)
```

---

## 🧪 Step 5: Target Variable Analysis (Survived)

```python
df['Survived'].value_counts()
df['Survived'].value_counts(normalize=True)
```

🧠 Insight:

* ~38% survived
* ~62% did not

---

## 🧪 Step 6: Gender vs Survival

```python
df.groupby('Sex')['Survived'].mean()
```

📌 Insight:

* Female survival rate much higher

---

## 🧪 Step 7: Class vs Survival

```python
df.groupby('Pclass')['Survived'].mean()
```

📌 Insight:

* 1st class > 2nd > 3rd

---

## 🧪 Step 8: Age Distribution

```python
df['Age'].describe()
```

Optional filtering:

```python
df[df['Age'] < 10]['Survived'].mean()
```

---

## 🧪 Step 9: Fare Analysis

```python
df['Fare'].describe()
```

High fare survival:

```python
df[df['Fare'] > 50]['Survived'].mean()
```

---

## 🧪 Step 10: Feature Engineering

### 🔹 Age group

```python
df['AgeGroup'] = pd.cut(
    df['Age'],
    bins=[0,12,18,40,60,100],
    labels=['Child','Teen','Adult','Mid','Senior']
)
```

```python
df.groupby('AgeGroup')['Survived'].mean()
```

---

## 🧪 Step 11: Embarked Analysis

```python
df['Embarked'].value_counts()
df.groupby('Embarked')['Survived'].mean()
```

---

## 🧪 Step 12: Final Clean Dataset

```python
df.isna().sum()
```

Ready for:

* ML model
* Django / FastAPI backend
* CSV export

```python
df.to_csv("clean_titanic.csv", index=False)
```

---

# 📊 Summary (Exam / Viva Ready)

✔ Females survived more than males
✔ Higher class → higher survival
✔ Children survival rate high
✔ Fare & class strongly related to survival

---

# 💡 Interview Question Examples

❓ Why median for Age?
✔ Because Age has outliers

❓ Why drop Cabin?
✔ Too many missing values

❓ Which feature most important?
✔ Sex, Pclass, Fare

---

# 🚀 Next Level (Tell me what you want)

🔥 Titanic → **ML model (Logistic Regression)**
🔥 EDA with **Visualization (matplotlib)**
🔥 **Bank Marketing / Sales / Medical Dataset**
🔥 Convert this into **Jupyter Notebook Report**

বললেই আমি next step শুরু করে দেবো 👍

---------
চমৎকার 👍
এখন আমি **🔥 Mini EDA Project – Bank Marketing Dataset (Real Dataset)** দিচ্ছি
👉 **Business + ML + Interview friendly**
👉 Pandas skill একদম solid হবে

---

# 🔥 Mini EDA Project

## 📌 Project Title

**Exploratory Data Analysis (EDA) on Bank Marketing Dataset**

---

## 🎯 Business Problem

একটা ব্যাংক জানতে চায়—
👉 কোন ধরনের customer **term deposit subscribe করবে (yes/no)**

আমাদের কাজ:

* Customer behavior analyze করা
* Important factors বের করা
* Data clean করে ML-ready করা

---

## 📂 Dataset Overview (Important Columns)

| Column    | Meaning            |
| --------- | ------------------ |
| age       | Customer age       |
| job       | Job type           |
| marital   | Marital status     |
| education | Education level    |
| balance   | Account balance    |
| housing   | Housing loan       |
| loan      | Personal loan      |
| contact   | Contact type       |
| duration  | Call duration      |
| campaign  | Number of contacts |
| y         | Target (yes / no)  |

---

## 🧪 Step 1: Dataset Load

```python
import pandas as pd
import numpy as np

df = pd.read_csv("bank.csv", sep=';')
```

---

## 🧪 Step 2: First Look

```python
df.head()
df.shape
df.info()
df.describe()
```

🧠 Questions:

* Total customers?
* Numeric vs categorical columns?

---

## 🧪 Step 3: Missing Values Check

```python
df.isna().sum()
```

📌 Observation:

* Usually no NaN
* `"unknown"` = hidden missing value

---

## 🧪 Step 4: Handle "unknown" Values

```python
df.replace("unknown", np.nan, inplace=True)
df.isna().sum()
```

Fill categorical:

```python
df['job'].fillna(df['job'].mode()[0], inplace=True)
df['education'].fillna(df['education'].mode()[0], inplace=True)
```

---

## 🧪 Step 5: Target Variable Analysis (`y`)

```python
df['y'].value_counts()
df['y'].value_counts(normalize=True)
```

📌 Insight:

* Majority customers → **did NOT subscribe**
* Dataset is **imbalanced**

---

## 🧪 Step 6: Age vs Subscription

```python
df.groupby('y')['age'].mean()
```

Age group:

```python
df['age_group'] = pd.cut(
    df['age'],
    bins=[0,25,40,60,100],
    labels=['Young','Adult','Mid','Senior']
)

df.groupby('age_group')['y'].value_counts(normalize=True)
```

---

## 🧪 Step 7: Job vs Subscription

```python
df.groupby('job')['y'].value_counts(normalize=True)
```

📌 Insight:

* Retired & students → higher subscription

---

## 🧪 Step 8: Balance Analysis

```python
df['balance'].describe()
```

High balance customers:

```python
df[df['balance'] > 10000]['y'].value_counts(normalize=True)
```

📌 Insight:

* Higher balance → higher probability of "yes"

---

## 🧪 Step 9: Loan Effect

```python
df.groupby('loan')['y'].value_counts(normalize=True)
df.groupby('housing')['y'].value_counts(normalize=True)
```

📌 Insight:

* Loan holders less likely to subscribe

---

## 🧪 Step 🔟 Call Duration Impact (IMPORTANT)

```python
df.groupby('y')['duration'].mean()
```

📌 Insight:

* Longer call → higher chance of success
  ⚠️ (ML leakage warning — interview gold point)

---

## 🧪 Step 11: Feature Engineering

### 🔹 Binary encode target

```python
df['y'] = df['y'].map({'yes':1, 'no':0})
```

### 🔹 Balance category

```python
df['balance_level'] = pd.cut(
    df['balance'],
    bins=[-9999,0,5000,20000,1000000],
    labels=['Negative','Low','Mid','High']
)
```

---

## 🧪 Step 12: Final Clean Dataset

```python
df.isna().sum()
```

Export:

```python
df.to_csv("clean_bank_marketing.csv", index=False)
```

---

# 📊 Final Insights (Exam / Interview Ready)

✔ Older & retired customers subscribe more
✔ High balance customers are valuable
✔ Loan holders are less responsive
✔ Call duration strongly affects outcome

---

# 💡 Interview Questions (With Smart Answers)

❓ Why convert "unknown" to NaN?
✔ To handle missing values properly

❓ Why duration risky for ML?
✔ It's known only after call ends (data leakage)

❓ Business recommendation?
✔ Target high-balance, retired, loan-free customers

---

# 🚀 Next Options (Choose One)

🔥 Convert this to **EDA + Visualization**
🔥 Build **Logistic Regression ML model**
🔥 Same project using **Medical Dataset**
🔥 Make **Jupyter Notebook + Report**

যেটা চাও বলো — আমি immediately next step শুরু করবো 👍

-----
