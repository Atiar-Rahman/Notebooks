অবশ্যই। আপনি সম্ভবত **Seaborn**-এর কথা বলছেন। নিচে আমি **Beginner → Intermediate → Advanced → Real Dataset Project** পর্যন্ত একটি complete Seaborn tutorial দিচ্ছি। যেহেতু আপনি Data Analysis/ML-এর দিকে যাচ্ছেন, আমি Seaborn-কে **Pandas + NumPy + Matplotlib**-এর সাথে ব্যবহার করে শেখাচ্ছি।

# 📊 Seaborn Complete Tutorial — Beginner to Advanced

## 0. Seaborn কী?

**Seaborn** হলো Python-এর একটি statistical data visualization library।

এটি মূলত:

* Dataset visualize করতে
* Statistical relationship বুঝতে
* Distribution দেখতে
* Category compare করতে
* Correlation analyze করতে
* Machine Learning-এর আগে EDA করতে

ব্যবহার করা হয়।

Seaborn সাধারণত **Pandas DataFrame**-এর সাথে খুব ভালো কাজ করে।

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```

---

# Phase 1 — Seaborn Setup

## 1. Install Seaborn

Terminal:

```bash
pip install seaborn
```

Jupyter Notebook:

```python
!pip install seaborn
```

Check version:

```python
import seaborn as sns

print(sns.__version__)
```

---

# Phase 2 — প্রথম Plot

Seaborn-এর built-in dataset ব্যবহার করি।

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

Output-এর মতো:

```text
   total_bill   tip     sex smoker  day    time  size
0       16.99  1.01  Female     No  Sun  Dinner     2
1       10.34  1.66    Male     No  Sun  Dinner     3
2       21.01  3.50    Male     No  Sun  Dinner     3
```

Basic plot:

```python
sns.scatterplot(data=df, x="total_bill", y="tip")

plt.show()
```

এখানে:

* `data` → DataFrame
* `x` → X-axis
* `y` → Y-axis

---

# Phase 3 — Seaborn-এর Main Plot Categories

Seaborn-এর plotগুলোকে মূলত কয়েকটি category-তে ভাগ করে শেখা যায়:

### Distribution

* histplot
* kdeplot
* ecdfplot
* rugplot

### Relationship

* scatterplot
* lineplot

### Categorical

* barplot
* countplot
* boxplot
* violinplot
* stripplot
* swarmplot
* pointplot

### Matrix

* heatmap
* clustermap

### Regression

* regplot
* lmplot

### Multi-variable

* pairplot
* jointplot

---

# Phase 4 — Scatter Plot

Scatter plot দুইটি numerical variable-এর relationship দেখায়।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

## Hue

তৃতীয় variable অনুযায়ী color:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এখানে `sex` অনুযায়ী points আলাদা হবে।

---

## Size

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    size="size"
)

plt.show()
```

---

## Style

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    style="time"
)

plt.show()
```

---

# Phase 5 — Line Plot

Time-series বা ordered data-এর জন্য খুব গুরুত্বপূর্ণ।

```python
sns.lineplot(
    data=df,
    x="size",
    y="total_bill"
)

plt.show()
```

আরেকটি ভালো dataset:

```python
flights = sns.load_dataset("flights")

print(flights.head())
```

```python
sns.lineplot(
    data=flights,
    x="year",
    y="passengers"
)

plt.show()
```

---

# Phase 6 — Histogram

একটি numerical variable-এর distribution দেখতে:

```python
sns.histplot(
    data=df,
    x="total_bill"
)

plt.show()
```

---

## Number of bins

```python
sns.histplot(
    data=df,
    x="total_bill",
    bins=20
)

plt.show()
```

---

## Hue সহ Histogram

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex"
)

plt.show()
```

---

## KDE সহ Histogram

```python
sns.histplot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

এটি distribution-এর smooth curve দেখাবে।

---

# Phase 7 — KDE Plot

KDE = **Kernel Density Estimation**

```python
sns.kdeplot(
    data=df,
    x="total_bill"
)

plt.show()
```

Multiple groups:

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    hue="sex"
)

plt.show()
```

---

# Phase 8 — Count Plot

Categorical data-এর count দেখতে।

```python
sns.countplot(
    data=df,
    x="sex"
)

plt.show()
```

আরেকটি:

```python
sns.countplot(
    data=df,
    x="day"
)

plt.show()
```

Hue:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.show()
```

---

# Phase 9 — Bar Plot

Bar plot সাধারণত category অনুযায়ী numerical value-এর **statistical aggregation** দেখায়।

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Defaultভাবে mean দেখাতে পারে।

---

## Estimator

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="mean"
)

plt.show()
```

Median:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="median"
)

plt.show()
```

---

# Phase 10 — Box Plot

Dataset-এর:

* Median
* Q1
* Q3
* IQR
* Outlier

বোঝার জন্য Box Plot অত্যন্ত গুরুত্বপূর্ণ।

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

---

## Hue

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

---

# Phase 11 — Violin Plot

Violin plot = Box plot + Distribution information।

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Hue:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

---

# Phase 12 — Strip Plot

Individual observations দেখতে:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Jitter:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True
)

plt.show()
```

---

# Phase 13 — Swarm Plot

Swarm plot individual points overlap না করে দেখানোর চেষ্টা করে।

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Dataset বড় হলে swarm plot expensive হতে পারে।

---

# Phase 14 — Regression Plot

Relationship + regression line:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটি ML শেখার সময়ও useful।

Conceptually:

```text
Y
│          •
│       •
│    •
│  •
│ •
└──────────────── X

      Regression line
```

---

# Phase 15 — LM Plot

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Hue:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

---

# Phase 16 — Heatmap ⭐

Data Analyst এবং ML-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

প্রথমে correlation:

```python
corr = df.select_dtypes("number").corr()

print(corr)
```

তারপর:

```python
sns.heatmap(corr)

plt.show()
```

---

## Annotation

```python
sns.heatmap(
    corr,
    annot=True
)

plt.show()
```

এতে correlation values দেখা যাবে।

---

## Better Heatmap

```python
plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

---

# Phase 17 — Pair Plot ⭐

একসাথে অনেক numerical variable-এর relationship দেখতে।

```python
sns.pairplot(df)

plt.show()
```

Hue:

```python
sns.pairplot(
    df,
    hue="sex"
)

plt.show()
```

এটি EDA-এর জন্য খুব useful।

---

# Phase 18 — Joint Plot

দুই variable-এর relationship + distribution।

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

KDE:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="kde"
)

plt.show()
```

Regression:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

plt.show()
```

---

# Phase 19 — FacetGrid

একটি variable অনুযায়ী multiple plots তৈরি করতে।

```python
g = sns.FacetGrid(
    df,
    col="sex"
)

g.map(
    sns.histplot,
    "total_bill"
)

plt.show()
```

---

# Phase 20 — CatPlot

Categorical visualization-এর high-level interface।

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="box"
)

plt.show()
```

Bar:

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="bar"
)

plt.show()
```

Count:

```python
sns.catplot(
    data=df,
    x="day",
    kind="count"
)

plt.show()
```

---

# Phase 21 — RelPlot

Relationship plots-এর high-level interface।

```python
sns.relplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="scatter"
)

plt.show()
```

Line:

```python
sns.relplot(
    data=flights,
    x="year",
    y="passengers",
    kind="line"
)

plt.show()
```

---

# Phase 22 — Data Filtering + Seaborn

Pandas এবং Seaborn একসাথে ব্যবহার করা খুব গুরুত্বপূর্ণ।

ধরি:

```python
male = df[df["sex"] == "Male"]
```

তারপর:

```python
sns.histplot(
    data=male,
    x="total_bill"
)

plt.show()
```

---

# Phase 23 — Missing Values

আগে check:

```python
print(df.isnull().sum())
```

Missing value visualization-এর আগে data clean করা উচিত।

```python
df = df.dropna()
```

তারপর:

```python
sns.histplot(
    data=df,
    x="total_bill"
)

plt.show()
```

---

# Phase 24 — Seaborn + Matplotlib

Seaborn visualization তৈরি করে, কিন্তু Matplotlib দিয়ে আরও customize করা যায়।

```python
plt.figure(figsize=(10, 6))

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.title("Total Bill vs Tip")
plt.xlabel("Total Bill")
plt.ylabel("Tip")

plt.show()
```

---

# Phase 25 — Figure Size

```python
plt.figure(figsize=(12, 7))

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# Phase 26 — Title

```python
sns.histplot(
    data=df,
    x="total_bill"
)

plt.title("Distribution of Total Bill")

plt.show()
```

---

# Phase 27 — Axis Labels

```python
plt.xlabel("Total Bill Amount")
plt.ylabel("Frequency")
```

---

# Phase 28 — Rotation

যদি category নাম বড় হয়:

```python
plt.xticks(rotation=45)
```

---

# Phase 29 — Themes

Seaborn-এর built-in theme:

```python
sns.set_theme()
```

Whitegrid:

```python
sns.set_theme(style="whitegrid")
```

Dark:

```python
sns.set_theme(style="darkgrid")
```

White:

```python
sns.set_theme(style="white")
```

Ticks:

```python
sns.set_theme(style="ticks")
```

---

# Phase 30 — Color Palette

Seaborn-এর অনেক built-in palette আছে।

```python
sns.set_palette("deep")
```

অথবা:

```python
sns.set_palette("muted")
```

আরও:

```python
sns.set_palette("bright")
```

```python
sns.set_palette("pastel")
```

```python
sns.set_palette("dark")
```

---

# Phase 31 — Custom Palette

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    palette="viridis"
)

plt.show()
```

---

# Phase 32 — Ordering

Category-এর order নিজে specify করা যায়।

```python
order = ["Thur", "Fri", "Sat", "Sun"]

sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    order=order
)

plt.show()
```

---

# Phase 33 — Sorting

Pandas দিয়ে sort করে visualization:

```python
summary = (
    df.groupby("day")["total_bill"]
    .mean()
    .sort_values()
    .reset_index()
)

print(summary)
```

তারপর:

```python
sns.barplot(
    data=summary,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# Phase 34 — Statistical Aggregation

Seaborn-এর বড় সুবিধা হলো statistical aggregation।

```python
sns.barplot(
    data=df,
    x="day",
    y="tip"
)

plt.show()
```

এখানে প্রতিটি day-এর average tip দেখতে পারবেন।

---

# Phase 35 — Confidence Interval

Bar plot-এ uncertainty/error information দেখানো যায়।

```python
sns.barplot(
    data=df,
    x="day",
    y="tip",
    errorbar="sd"
)

plt.show()
```

এটি statistical interpretation-এর ক্ষেত্রে গুরুত্বপূর্ণ।

---

# Phase 36 — Numeric vs Categorical

এটি ভালোভাবে বুঝুন।

### Numerical → Numerical

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

### Categorical → Numerical

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)
```

### Categorical → Categorical

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)
```

### Numerical Distribution

```python
sns.histplot(
    data=df,
    x="total_bill"
)
```

---

# Phase 37 — EDA Workflow ⭐⭐⭐

Data Analyst হিসেবে আপনার Seaborn ব্যবহার করার সবচেয়ে গুরুত্বপূর্ণ workflow:

```text
Dataset
   ↓
Load Data
   ↓
Understand Data
   ↓
Missing Values
   ↓
Data Cleaning
   ↓
Univariate Analysis
   ↓
Bivariate Analysis
   ↓
Multivariate Analysis
   ↓
Correlation
   ↓
Outlier Detection
   ↓
Insights
```

---

# Phase 38 — Univariate Analysis

একটি variable analyze করা।

Example:

```python
sns.histplot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

Question:

* Distribution কেমন?
* Mean কোথায়?
* Outlier আছে?
* Data skewed কিনা?

---

# Phase 39 — Bivariate Analysis

দুই variable-এর relationship।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Question:

* Positive relationship?
* Negative relationship?
* No relationship?

---

# Phase 40 — Multivariate Analysis

একসাথে multiple variables।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    size="size",
    style="time"
)

plt.show()
```

এখানে এক plot-এ অনেক dimension এসেছে।

---

# Phase 41 — Correlation Analysis

```python
numeric_df = df.select_dtypes(include="number")

corr = numeric_df.corr()

print(corr)
```

Heatmap:

```python
plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

Correlation:

```text
+1 → Strong positive
 0 → No linear relationship
-1 → Strong negative
```

---

# Phase 42 — Outlier Detection ⭐

Boxplot:

```python
sns.boxplot(
    data=df,
    y="total_bill"
)

plt.show()
```

Category-wise:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# Phase 43 — Real Dataset Load

CSV:

```python
df = pd.read_csv("sales.csv")
```

Excel:

```python
df = pd.read_excel("sales.xlsx")
```

তারপর:

```python
print(df.head())
print(df.info())
print(df.describe())
```

---

# Phase 44 — Real Data EDA Example

ধরি dataset:

```text
Age
Salary
Experience
Department
Gender
Performance
```

### Age distribution

```python
sns.histplot(
    data=df,
    x="Age",
    kde=True
)

plt.show()
```

### Salary distribution

```python
sns.histplot(
    data=df,
    x="Salary",
    kde=True
)

plt.show()
```

### Salary by Department

```python
sns.boxplot(
    data=df,
    x="Department",
    y="Salary"
)

plt.show()
```

### Experience vs Salary

```python
sns.scatterplot(
    data=df,
    x="Experience",
    y="Salary"
)

plt.show()
```

### Gender distribution

```python
sns.countplot(
    data=df,
    x="Gender"
)

plt.show()
```

### Department distribution

```python
sns.countplot(
    data=df,
    x="Department"
)

plt.show()
```

### Correlation

```python
numeric = df.select_dtypes("number")

sns.heatmap(
    numeric.corr(),
    annot=True
)

plt.show()
```

---

# Phase 45 — Seaborn + Machine Learning

আপনার ML workflow-এ Seaborn এভাবে ব্যবহার করবেন:

```text
CSV Dataset
     ↓
Pandas
     ↓
Data Cleaning
     ↓
Seaborn EDA
     ↓
Feature Understanding
     ↓
Correlation
     ↓
Outlier Analysis
     ↓
Feature Engineering
     ↓
Train/Test Split
     ↓
ML Model
     ↓
Evaluation
```

উদাহরণ:

```python
sns.scatterplot(
    data=df,
    x="age",
    y="salary"
)
```

যদি strong relationship থাকে, ML model-এর জন্য featureটি গুরুত্বপূর্ণ হতে পারে।

---

# Phase 46 — Classification Dataset

ধরি Titanic dataset:

```python
titanic = sns.load_dataset("titanic")

print(titanic.head())
```

Survival:

```python
sns.countplot(
    data=titanic,
    x="survived"
)

plt.show()
```

Gender বনাম survival:

```python
sns.countplot(
    data=titanic,
    x="sex",
    hue="survived"
)

plt.show()
```

Age distribution:

```python
sns.histplot(
    data=titanic,
    x="age",
    kde=True
)

plt.show()
```

Age vs Survival:

```python
sns.boxplot(
    data=titanic,
    x="survived",
    y="age"
)

plt.show()
```

Class vs Survival:

```python
sns.countplot(
    data=titanic,
    x="class",
    hue="survived"
)

plt.show()
```

এভাবেই classification problem-এর আগে EDA করা হয়।

---

# Phase 47 — Regression Dataset

Regression-এর জন্য:

```python
sns.scatterplot(
    data=df,
    x="experience",
    y="salary"
)

plt.show()
```

Regression line:

```python
sns.regplot(
    data=df,
    x="experience",
    y="salary"
)

plt.show()
```

এতে relationship visually বুঝতে পারবেন।

---

# Phase 48 — Seaborn-এর Most Important Functions

আপনার এগুলো অবশ্যই master করা উচিত:

| Function        | Purpose                 |
| --------------- | ----------------------- |
| `scatterplot()` | Numerical relationship  |
| `lineplot()`    | Trend/time series       |
| `histplot()`    | Distribution            |
| `kdeplot()`     | Density                 |
| `countplot()`   | Category count          |
| `barplot()`     | Aggregated value        |
| `boxplot()`     | Distribution + outliers |
| `violinplot()`  | Distribution shape      |
| `stripplot()`   | Individual observations |
| `swarmplot()`   | Individual observations |
| `regplot()`     | Regression              |
| `lmplot()`      | Regression analysis     |
| `heatmap()`     | Correlation/matrix      |
| `pairplot()`    | Multiple relationships  |
| `jointplot()`   | Joint relationship      |
| `catplot()`     | Categorical plots       |
| `relplot()`     | Relationship plots      |
| `FacetGrid()`   | Multiple subplots       |

---

# Phase 49 — Seaborn Syntax Pattern

প্রায় সব সময় এই structure মনে রাখুন:

```python
sns.plot_function(
    data=df,
    x="column1",
    y="column2",
    hue="column3"
)

plt.show()
```

উদাহরণ:

```python
sns.scatterplot(
    data=df,
    x="age",
    y="salary",
    hue="gender"
)

plt.show()
```

এটাই Seaborn শেখার core pattern।

---

# Phase 50 — একটি Complete EDA Project

এখন আমরা একটি সম্পূর্ণ project structure দেখি।

## Step 1 — Import

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
```

## Step 2 — Load

```python
df = pd.read_csv("dataset.csv")
```

## Step 3 — Understand

```python
print(df.head())
print(df.shape)
print(df.info())
print(df.describe())
```

## Step 4 — Missing Values

```python
print(df.isnull().sum())
```

## Step 5 — Numeric Distribution

```python
sns.histplot(
    data=df,
    x="salary",
    kde=True
)

plt.show()
```

## Step 6 — Category Distribution

```python
sns.countplot(
    data=df,
    x="department"
)

plt.show()
```

## Step 7 — Relationship

```python
sns.scatterplot(
    data=df,
    x="experience",
    y="salary"
)

plt.show()
```

## Step 8 — Category Comparison

```python
sns.boxplot(
    data=df,
    x="department",
    y="salary"
)

plt.show()
```

## Step 9 — Correlation

```python
corr = df.select_dtypes("number").corr()

plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

## Step 10 — Pairplot

```python
sns.pairplot(
    df.select_dtypes("number")
)

plt.show()
```

---

# 🎯 আপনার জন্য Seaborn Learning Roadmap

আপনি যেহেতু **Data Analysis → ML → Deep Learning** দিকে যেতে চাচ্ছেন, আমি Seaborn এভাবে শেখার পরামর্শ দেব:

### Level 1 — Foundation

1. Seaborn কী
2. Installation
3. Dataset loading
4. `data`
5. `x`
6. `y`
7. `hue`
8. `style`
9. `size`

### Level 2 — Distribution

10. `histplot`
11. `kdeplot`
12. `ecdfplot`
13. `rugplot`

### Level 3 — Relationship

14. `scatterplot`
15. `lineplot`
16. `relplot`

### Level 4 — Categorical

17. `countplot`
18. `barplot`
19. `boxplot`
20. `violinplot`
21. `stripplot`
22. `swarmplot`
23. `catplot`

### Level 5 — Statistical

24. Aggregation
25. Mean
26. Median
27. Standard deviation
28. Error bars
29. Confidence intervals
30. Regression

### Level 6 — Advanced

31. `regplot`
32. `lmplot`
33. `pairplot`
34. `jointplot`
35. `FacetGrid`
36. `heatmap`
37. `clustermap`

### Level 7 — Professional EDA

38. Pandas + Seaborn
39. Missing values
40. Outliers
41. Correlation
42. Feature relationships
43. Categorical analysis
44. Multivariate analysis
45. Statistical interpretation
46. ML preprocessing

### Level 8 — Projects

47. Titanic EDA
48. Tips EDA
49. Sales Analysis
50. Customer Analysis
51. Employee Salary Analysis
52. E-commerce Analysis
53. Bank Customer Analysis
54. Supervised ML EDA

---

## ⭐ সবচেয়ে গুরুত্বপূর্ণ বিষয়

শুধু syntax মুখস্থ করলে Seaborn ভালোভাবে শেখা হবে না। প্রতিটি plot দেখে নিজেকে প্রশ্ন করবেন:

> **"এই visualization আমাকে dataset সম্পর্কে কী information দিচ্ছে?"**

যেমন:

```python
sns.boxplot(
    data=df,
    x="department",
    y="salary"
)
```

শুধু এটা জানা যথেষ্ট নয় যে এটি Box Plot।

আপনাকে বুঝতে হবে:

```text
Department
     ↓
Salary distribution
     ↓
Median
     ↓
Spread
     ↓
Outliers
     ↓
Department comparison
```

এটাই **Data Analysis mindset**।

আপনার জন্য পরবর্তী ধাপে সবচেয়ে ভালো হবে **“Seaborn M01 → M30”** হিসেবে একটি structured course করা—যেখানে প্রতিটি lesson-এ **concept → syntax → example → visualization → practice → mini task** থাকবে, এবং শেষে **একটি real-world EDA project** সম্পূর্ণ করবেন।



----
# Seaborn M01 — Introduction to Seaborn

আজকের lesson-এ আমরা Seaborn-এর **ভিত্তি** তৈরি করব। এখনই সব plot শেখার দরকার নেই। আগে বুঝব **Seaborn কী, কেন ব্যবহার করব, কীভাবে install/import করব এবং একটি basic visualization তৈরি করব।**

---

## 1. Seaborn কী?

**Seaborn** হলো Python-এর একটি data visualization library, যা বিশেষভাবে **statistical visualization** এবং **Exploratory Data Analysis (EDA)**-এর জন্য তৈরি।

সহজভাবে:

```text
Pandas
  ↓
Data তৈরি / Clean / Analyze
  ↓
Seaborn
  ↓
Data Visualization
  ↓
Insights
```

উদাহরণ:

আপনার dataset-এ যদি থাকে:

```text
Age     Salary
22      25000
25      32000
28      40000
30      45000
35      60000
```

তাহলে Seaborn দিয়ে আমরা দেখতে পারি:

* Age এবং Salary-এর relationship
* Salary distribution
* Outlier
* Correlation
* Category অনুযায়ী comparison

---

# 2. কেন Seaborn শিখব?

Data Analysis এবং Machine Learning-এ visualization অত্যন্ত গুরুত্বপূর্ণ।

ধরুন আপনার কাছে 100,000 rows data আছে।

শুধু:

```python
print(df)
```

করলে data বোঝা কঠিন।

কিন্তু:

```python
sns.scatterplot(data=df, x="age", y="salary")
```

করলে relationship চোখে দেখা যায়।

### Seaborn-এর সুবিধা

* সুন্দর default visualization
* Pandas DataFrame-এর সাথে সহজে কাজ করে
* Statistical visualization সহজ
* Group/category analysis সহজ
* Correlation visualization
* EDA-এর জন্য খুব useful
* Matplotlib-এর উপর ভিত্তি করে কাজ করে

---

# 3. Seaborn এবং Matplotlib-এর সম্পর্ক

এটি খুব গুরুত্বপূর্ণ।

**Matplotlib** হলো general-purpose visualization library।

**Seaborn** হলো statistical/data-analysis-focused visualization library।

একটি সহজ comparison:

```text
Matplotlib
    ↓
Low-level / More control
    ↓
Detailed customization


Seaborn
    ↓
High-level
    ↓
Statistical visualization
    ↓
EDA-friendly
```

তবে দুটো একসাথে ব্যবহার করা যায়।

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.scatterplot(...)
plt.title(...)
plt.xlabel(...)
plt.show()
```

অর্থাৎ:

> **Seaborn plot তৈরি করবে, Matplotlib দিয়ে সেটিকে আরও customize করতে পারবেন।**

---

# 4. Seaborn Install

Terminal-এ:

```bash
pip install seaborn
```

Jupyter Notebook হলে:

```python
!pip install seaborn
```

Install হয়েছে কিনা:

```python
import seaborn as sns

print(sns.__version__)
```

---

# 5. Seaborn Import

সাধারণত আমরা লিখি:

```python
import seaborn as sns
```

এখানে:

```text
seaborn → library
sns     → short name
```

`seaborn`-কে `sns` নামে ব্যবহার করা Python data science community-তে প্রচলিত convention।

তারপর plotting-এর জন্য:

```python
import matplotlib.pyplot as plt
```

Complete import:

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

---

# 6. প্রথম Seaborn Dataset

Seaborn-এর কিছু built-in dataset আছে।

আমরা `tips` dataset ব্যবহার করব।

```python
import seaborn as sns

df = sns.load_dataset("tips")

print(df)
```

প্রথম কয়েকটি row দেখতে:

```python
print(df.head())
```

সম্ভাব্য output:

```text
   total_bill   tip     sex smoker  day    time  size
0       16.99  1.01  Female     No   Sun  Dinner     2
1       10.34  1.66  Male      No   Sun  Dinner     3
2       21.01  3.50  Male      No   Sun  Dinner     3
3       23.68  3.31  Male      No   Sun  Dinner     2
4       24.59  3.61  Female    No   Sun  Dinner     4
```

---

# 7. Dataset-এর Column বুঝি

```python
print(df.columns)
```

Output:

```text
Index(['total_bill', 'tip', 'sex', 'smoker', 'day', 'time', 'size'])
```

এখানে:

| Column       | Meaning      |
| ------------ | ------------ |
| `total_bill` | মোট বিল      |
| `tip`        | Tip          |
| `sex`        | Gender       |
| `smoker`     | Smoker কিনা  |
| `day`        | কোন দিন      |
| `time`       | Lunch/Dinner |
| `size`       | কতজন         |

---

# 8. Dataset-এর Shape

```python
print(df.shape)
```

এতে:

```text
(rows, columns)
```

format-এ output পাবেন।

---

# 9. Dataset Information

```python
print(df.info())
```

এটি আপনাকে দেখাবে:

* Column
* Data type
* Non-null values
* Memory usage

---

# 10. প্রথম Visualization

এখন আমরা `total_bill` এবং `tip`-এর relationship দেখব।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এখানে:

```text
data=df
```

মানে dataset হলো `df`।

```text
x="total_bill"
```

মানে X-axis-এ `total_bill`।

```text
y="tip"
```

মানে Y-axis-এ `tip`।

---

# 11. এই Plot কী বলছে?

Visualization দেখে আমরা প্রশ্ন করতে পারি:

> বেশি bill হলে কি সাধারণত বেশি tip দেওয়া হয়?

যদি points-এর মধ্যে upward trend দেখতে পাই, তাহলে বলতে পারি:

**Total bill এবং tip-এর মধ্যে positive relationship আছে বলে মনে হচ্ছে।**

এখানে একটি গুরুত্বপূর্ণ Data Analysis habit তৈরি করুন:

> **Plot বানানোর পর সবসময় plot থেকে insight বের করার চেষ্টা করবেন।**

---

# 12. `hue` কী?

Seaborn-এর অন্যতম গুরুত্বপূর্ণ parameter হলো:

```python
hue
```

এটি কোনো category অনুযায়ী data আলাদা করতে সাহায্য করে।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এখন `sex` অনুযায়ী observations আলাদা হবে।

Concept:

```text
total_bill ───────→ X

tip
│
│    Male
│    Female
│
↓
Y
```

---

# 13. `hue` কেন গুরুত্বপূর্ণ?

ধরুন শুধু এই plot:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

আপনি relationship দেখতে পাচ্ছেন।

কিন্তু:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)
```

করলে আরও একটি dimension যোগ হলো।

অর্থাৎ:

```text
X → total_bill
Y → tip
Color → sex
```

এটি **multivariate visualization**-এর basic example।

---

# 14. Seaborn-এর Basic Syntax

এই structure খুব ভালোভাবে মনে রাখুন:

```python
sns.plot_function(
    data=df,
    x="column_name",
    y="column_name"
)

plt.show()
```

উদাহরণ:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

আর category যোগ করলে:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

---

# 15. `style`

আরেকটি useful parameter:

```python
style
```

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    style="time"
)

plt.show()
```

এখন:

```text
X       → total_bill
Y       → tip
Color   → sex
Shape   → time
```

একটি plot-এর মধ্যে একাধিক variable দেখা যাচ্ছে।

---

# 16. `size`

Point-এর size কোনো variable অনুযায়ী পরিবর্তন করতে:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    size="size"
)

plt.show()
```

এখন:

```text
X       → total_bill
Y       → tip
Size    → party size
```

---

# 17. তিনটি একসাথে

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    style="time",
    size="size"
)

plt.show()
```

এটি Seaborn-এর শক্তিশালী একটি feature দেখায়।

---

# 18. Matplotlib-এর সাথে ব্যবহার

Seaborn এবং Matplotlib একসাথে ব্যবহার করা খুব common।

```python
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.title("Total Bill vs Tip")
plt.xlabel("Total Bill")
plt.ylabel("Tip")

plt.show()
```

এখানে:

```text
Seaborn
   ↓
Plot তৈরি

Matplotlib
   ↓
Title
Labels
Figure size
Show
```

---

# 19. একটি Complete M01 Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load dataset
df = sns.load_dataset("tips")

# Display data
print(df.head())

# Dataset information
print(df.info())

# Scatter plot
plt.figure(figsize=(8, 5))

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.title("Total Bill vs Tip")
plt.xlabel("Total Bill")
plt.ylabel("Tip")

plt.show()
```

---

# 20. M01-এ যা শিখলেন

আজকের lesson-এর core concepts:

```text
Seaborn
│
├── What is Seaborn?
├── Why Seaborn?
├── Seaborn vs Matplotlib
├── Installation
├── Import
├── Built-in Dataset
├── sns.load_dataset()
├── DataFrame
├── data=
├── x=
├── y=
├── hue=
├── style=
├── size=
└── Matplotlib integration
```

---

# 🧠 Practice Task — M01

নিজে এই কাজগুলো করুন।

### Task 1

`tips` dataset load করুন।

```python
df = sns.load_dataset("tips")
```

তারপর:

```python
print(df.head())
print(df.shape)
print(df.columns)
print(df.info())
```

### Task 2

`total_bill` বনাম `tip` scatter plot তৈরি করুন।

### Task 3

`sex` দিয়ে `hue` ব্যবহার করুন।

### Task 4

`time` দিয়ে `style` ব্যবহার করুন।

### Task 5

`size` দিয়ে point size পরিবর্তন করুন।

### Task 6 ⭐

একটি plot-এ ব্যবহার করুন:

```text
x = total_bill
y = tip
hue = sex
style = time
size = size
```

### Task 7 ⭐⭐

নিজের ভাষায় এই প্রশ্নের উত্তর লিখুন:

> **এই visualization থেকে total_bill এবং tip সম্পর্কে কী বোঝা যাচ্ছে?**

---

## 🎯 M01-এর লক্ষ্য

M01 শেষ করার পর আপনি যেন এই code **না দেখে** লিখতে পারেন:

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এটি পারলে **Seaborn M01 complete**।

**পরের lesson: Seaborn M02 — Seaborn Dataset, Pandas DataFrame & Data Understanding Deep Dive**।

---
# Seaborn M02 — Dataset & DataFrame Deep Dive

M01-এ আমরা Seaborn কী, `load_dataset()`, `data`, `x`, `y`, `hue`, `style`, `size` এবং basic `scatterplot()` শিখেছি।

**M02-এর লক্ষ্য:** Seaborn দিয়ে visualization করার আগে dataset-কে কীভাবে **বোঝা, inspect, filter এবং prepare** করতে হয়—এটি শেখা। Data Analysis/EDA-তে এই অংশটি খুব গুরুত্বপূর্ণ।

---

## 1. Seaborn Dataset কী?

Seaborn-এর কিছু example dataset রয়েছে, যেগুলো practice করার জন্য ব্যবহার করা যায়।

যেমন:

```python
import seaborn as sns

df = sns.load_dataset("tips")

print(df.head())
```

এখানে:

```text
sns
 ↓
Seaborn

load_dataset()
 ↓
Dataset load

df
 ↓
Pandas DataFrame
```

অর্থাৎ dataset load করার পর আমরা আসলে **Pandas DataFrame** নিয়ে কাজ করছি।

---

# 2. `tips` Dataset

আজকের lesson-এ মূলত `tips` dataset ব্যবহার করব।

```python
import seaborn as sns

df = sns.load_dataset("tips")
```

প্রথম 5 rows:

```python
print(df.head())
```

শেষ 5 rows:

```python
print(df.tail())
```

---

# 3. Dataset-এর সব Rows দেখা উচিত নয়

Beginner হিসেবে অনেকেই করে:

```python
print(df)
```

যদি dataset বড় হয়, তাহলে হাজার হাজার row terminal-এ চলে আসবে।

তার পরিবর্তে:

```python
print(df.head())
```

অথবা:

```python
print(df.head(10))
```

শেষের:

```python
print(df.tail(10))
```

---

# 4. Dataset Shape

Dataset-এ কত row এবং column আছে:

```python
print(df.shape)
```

Output-এর format:

```text
(rows, columns)
```

ধরা যাক:

```text
(244, 7)
```

এর অর্থ:

```text
244 → rows
7   → columns
```

---

# 5. Number of Rows

```python
print(len(df))
```

অথবা:

```python
print(df.shape[0])
```

---

# 6. Number of Columns

```python
print(df.shape[1])
```

---

# 7. Column Names

```python
print(df.columns)
```

অথবা list হিসেবে:

```python
print(df.columns.tolist())
```

Output:

```text
[
    'total_bill',
    'tip',
    'sex',
    'smoker',
    'day',
    'time',
    'size'
]
```

---

# 8. Data Types

প্রতিটি column-এর datatype দেখতে:

```python
print(df.dtypes)
```

সম্ভাব্যভাবে:

```text
total_bill    float64
tip           float64
sex            object
smoker         object
day            object
time           object
size            int64
```

এখানে:

```text
float64 → decimal number
int64   → integer
object  → categorical/text-like data
```

---

# 9. `info()` ⭐

Dataset বোঝার জন্য সবচেয়ে গুরুত্বপূর্ণ function:

```python
df.info()
```

এটি দেখায়:

* Column name
* Non-null count
* Data type
* Memory usage

Example:

```python
df.info()
```

এটি Data Analysis-এর প্রতিটি project-এ ব্যবহার করার অভ্যাস করুন।

---

# 10. Statistical Summary

Numerical columns-এর basic statistics:

```python
print(df.describe())
```

এতে সাধারণত দেখা যায়:

```text
count
mean
std
min
25%
50%
75%
max
```

---

# 11. `describe()` কীভাবে বুঝবেন?

ধরি:

```text
total_bill

mean = 19.78
min  = 3.07
max  = 50.81
```

এর অর্থ:

```text
Average bill ≈ 19.78

Lowest bill ≈ 3.07

Highest bill ≈ 50.81
```

`50%` হলো median।

---

# 12. শুধু একটি Column-এর Statistics

```python
print(df["total_bill"].describe())
```

অথবা:

```python
print(df["tip"].describe())
```

---

# 13. একটি Column নির্বাচন

```python
print(df["total_bill"])
```

এটি একটি Pandas Series।

একাধিক column:

```python
print(
    df[
        ["total_bill", "tip"]
    ]
)
```

---

# 14. Numerical Columns

```python
numeric_df = df.select_dtypes(include="number")

print(numeric_df)
```

এতে numerical columns পাওয়া যাবে।

```text
total_bill
tip
size
```

---

# 15. Categorical Columns

```python
categorical_df = df.select_dtypes(include="object")

print(categorical_df)
```

যেমন:

```text
sex
smoker
day
time
```

---

# 16. Unique Values

একটি categorical column-এ কী কী value আছে:

```python
print(df["sex"].unique())
```

Output:

```text
['Female' 'Male']
```

আর:

```python
print(df["day"].unique())
```

সম্ভাব্য:

```text
['Sun', 'Sat', 'Thur', 'Fri']
```

---

# 17. Number of Unique Values

```python
print(df["day"].nunique())
```

এটি বলবে মোট কতটি unique category আছে।

---

# 18. `value_counts()` ⭐

প্রতিটি category কতবার এসেছে:

```python
print(df["sex"].value_counts())
```

যেমন:

```text
Male      ...
Female    ...
```

এটি EDA-তে অত্যন্ত গুরুত্বপূর্ণ।

---

# 19. Category Visualization

এখন `value_counts()`-কে Seaborn-এর visualization-এর সাথে compare করুন।

Pandas:

```python
print(df["day"].value_counts())
```

Seaborn:

```python
sns.countplot(
    data=df,
    x="day"
)

plt.show()
```

দুটোই একই underlying question-এর উত্তর দিতে পারে:

> কোন day-তে কত observation আছে?

---

# 20. Missing Values ⭐⭐⭐

প্রতিটি column-এ missing value কত:

```python
print(df.isnull().sum())
```

অথবা:

```python
print(df.isna().sum())
```

দুটো এখানে একই ধরনের কাজ করবে।

---

# 21. Missing Percentage

আরও professional EDA:

```python
missing_percentage = (
    df.isnull().mean() * 100
)

print(missing_percentage)
```

এতে প্রতিটি column-এর missing data percentage পাওয়া যাবে।

---

# 22. Duplicate Rows

Duplicate আছে কিনা:

```python
print(df.duplicated().sum())
```

Duplicate rows দেখতে:

```python
print(df[df.duplicated()])
```

---

# 23. Duplicate Remove

যদি প্রয়োজন হয়:

```python
df = df.drop_duplicates()
```

**তবে blindly duplicate remove করবেন না।**

কখনও duplicate row legitimate হতে পারে।

---

# 24. Data Filtering

ধরি আমরা শুধু Male observations চাই।

```python
male = df[df["sex"] == "Male"]

print(male.head())
```

Female:

```python
female = df[df["sex"] == "Female"]
```

---

# 25. Numerical Filtering

যাদের total bill 20-এর বেশি:

```python
high_bill = df[df["total_bill"] > 20]

print(high_bill)
```

---

# 26. Multiple Conditions

Male এবং bill > 20:

```python
result = df[
    (df["sex"] == "Male") &
    (df["total_bill"] > 20)
]

print(result)
```

খেয়াল করুন:

```python
&
```

ব্যবহার করতে হবে।

---

# 27. OR Condition

Male অথবা Female:

```python
result = df[
    (df["sex"] == "Male") |
    (df["sex"] == "Female")
]
```

OR-এর জন্য:

```python
|
```

---

# 28. Filtering + Seaborn ⭐

এটি খুব গুরুত্বপূর্ণ।

প্রথমে:

```python
male = df[df["sex"] == "Male"]
```

তারপর:

```python
sns.histplot(
    data=male,
    x="total_bill"
)

plt.show()
```

অথবা সরাসরি filter করা DataFrame ব্যবহার করতে পারেন।

---

# 29. `hue` বনাম Filtering

দুটো approach:

### Approach 1 — Filtering

```python
male = df[df["sex"] == "Male"]

sns.histplot(
    data=male,
    x="total_bill"
)
```

### Approach 2 — Hue

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex"
)
```

যদি groups compare করতে চান, অনেক সময় `hue` বেশি convenient।

---

# 30. GroupBy + Seaborn

এখন একটু advanced EDA।

প্রতিদিনের average bill:

```python
summary = (
    df.groupby("day")["total_bill"]
    .mean()
)

print(summary)
```

DataFrame হিসেবে:

```python
summary = (
    df.groupby("day", as_index=False)["total_bill"]
    .mean()
)

print(summary)
```

তারপর visualization:

```python
sns.barplot(
    data=summary,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# 31. GroupBy + Multiple Variables

Average tip by day and sex:

```python
summary = (
    df.groupby(
        ["day", "sex"],
        as_index=False
    )["tip"]
    .mean()
)

print(summary)
```

তারপর:

```python
sns.barplot(
    data=summary,
    x="day",
    y="tip",
    hue="sex"
)

plt.show()
```

এটি বাস্তব EDA-তে খুব common workflow।

---

# 32. Correlation-এর জন্য Numeric Data

Correlation করতে categorical columns সরিয়ে numerical data নিতে পারেন:

```python
numeric_df = df.select_dtypes(
    include="number"
)

corr = numeric_df.corr()

print(corr)
```

তারপর:

```python
sns.heatmap(
    corr,
    annot=True
)

plt.show()
```

---

# 33. `pairplot()`-এর আগে Data Understanding

```python
sns.pairplot(df)

plt.show()
```

এটি multiple numerical variables-এর relationship দেখাবে।

কিন্তু মনে রাখবেন:

> Pairplot চালানোর আগে dataset-এর numerical/categorical structure বোঝা উচিত।

---

# 34. Dataset-এর Distribution বুঝতে Histogram

```python
sns.histplot(
    data=df,
    x="total_bill"
)

plt.show()
```

KDE যোগ:

```python
sns.histplot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

---

# 35. Column Selection + Visualization

শুধু selected data:

```python
selected = df[
    ["total_bill", "tip"]
]

sns.scatterplot(
    data=selected,
    x="total_bill",
    y="tip"
)

plt.show()
```

---

# 36. Sorting + Visualization

Average bill বের করে sort:

```python
summary = (
    df.groupby("day", as_index=False)
    ["total_bill"]
    .mean()
    .sort_values("total_bill")
)

print(summary)
```

Visualization:

```python
sns.barplot(
    data=summary,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# 37. M02-এর Professional EDA Template ⭐⭐⭐

বাস্তব dataset পেলে শুরুতে এই code structure ব্যবহার করতে পারেন:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Load
df = sns.load_dataset("tips")

# Basic inspection
print(df.head())
print(df.tail())

# Shape
print("Shape:", df.shape)

# Columns
print("Columns:", df.columns.tolist())

# Data types
print(df.dtypes)

# Information
df.info()

# Statistics
print(df.describe())

# Missing values
print(df.isnull().sum())

# Duplicate values
print("Duplicates:", df.duplicated().sum())

# Unique values
print(df["day"].unique())

# Category counts
print(df["day"].value_counts())
```

এটি আপনার **EDA starting template** হিসেবে মনে রাখতে পারেন।

---

# 38. এরপর Visualization

Basic inspection-এর পরে:

```python
sns.histplot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

Relationship:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

Category:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.show()
```

Distribution comparison:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Correlation:

```python
corr = df.select_dtypes("number").corr()

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

---

# 🧠 M02-এর মূল ধারণা

পুরো M02-কে এই workflow হিসেবে মনে রাখুন:

```text
                 Dataset
                    ↓
              df.head()
                    ↓
              df.shape
                    ↓
            df.columns
                    ↓
              df.info()
                    ↓
            df.describe()
                    ↓
          Missing Values
                    ↓
             Duplicates
                    ↓
          Unique / Counts
                    ↓
             Filtering
                    ↓
              GroupBy
                    ↓
              Seaborn
                    ↓
                 EDA
```

---

# 🎯 M02 Practice

নিজে code না দেখে করার চেষ্টা করুন।

### Task 1

`tips` dataset load করুন।

### Task 2

তার:

* first 10 rows
* last 10 rows
* shape
* columns
* datatypes

দেখুন।

### Task 3

`total_bill`, `tip`, `size` numerical columns বের করুন।

### Task 4

`sex`, `day`, `time`-এর unique values বের করুন।

### Task 5

`day`-এর `value_counts()` বের করুন।

### Task 6

Missing values check করুন।

### Task 7

Duplicate rows check করুন।

### Task 8

শুধু `total_bill > 30` observations বের করুন।

### Task 9

শুধু Sunday-এর data নিয়ে:

```python
sns.histplot(...)
```

তৈরি করুন।

### Task 10 ⭐

প্রতিটি `day`-এর **average total bill** বের করে একটি Seaborn `barplot` তৈরি করুন।

### Task 11 ⭐⭐

`day` + `sex` অনুযায়ী **average tip** বের করে:

```text
X → day
Y → average tip
hue → sex
```

দিয়ে visualization তৈরি করুন।

---

## ✅ M02 Complete Checklist

নিজেকে পরীক্ষা করুন:

* [ ] `sns.load_dataset()`
* [ ] `df.head()`
* [ ] `df.tail()`
* [ ] `df.shape`
* [ ] `df.columns`
* [ ] `df.dtypes`
* [ ] `df.info()`
* [ ] `df.describe()`
* [ ] `df.isnull().sum()`
* [ ] `df.duplicated()`
* [ ] `unique()`
* [ ] `nunique()`
* [ ] `value_counts()`
* [ ] Data filtering
* [ ] Multiple conditions
* [ ] `groupby()`
* [ ] GroupBy + Seaborn
* [ ] Numerical vs categorical columns

**M02-এর সবচেয়ে গুরুত্বপূর্ণ শিক্ষা:** Seaborn শেখা মানে শুধু `sns.scatterplot()` বা `sns.histplot()` মুখস্থ করা নয়। **আগে DataFrame বুঝবেন → তারপর সঠিক visualization নির্বাচন করবেন → তারপর visualization থেকে insight বের করবেন।**

**M03-এ আমরা শুরু করব Seaborn-এর প্রথম major visualization family: *Distribution Analysis* — `histplot()`, `kdeplot()`, bins, hue, multiple distributions, density এবং distribution interpretation।**

---
# Seaborn M03 — Distribution Analysis 📊

M02-এ আমরা dataset **inspect, clean, filter, groupby** করা শিখেছি।
এখন M03-এ আমরা শিখব একটি variable-এর **distribution** কীভাবে Seaborn দিয়ে analyze করতে হয়।

এটি Data Analysis এবং ML-এর জন্য খুব গুরুত্বপূর্ণ, কারণ model বানানোর আগে আমাদের জানতে হয়:

* Data কোথায় বেশি concentrated?
* Distribution normal নাকি skewed?
* Outlier আছে কি?
* Data-এর range কত?
* দুইটি group-এর distribution কি আলাদা?

---

# 1. Distribution Analysis কী?

ধরুন আপনার কাছে 1,000 জন মানুষের `age` আছে।

```text
Age
20
21
22
23
...
60
```

আমরা জানতে চাই:

> কোন age বেশি common?

এটাই distribution analysis-এর একটি basic উদ্দেশ্য।

Conceptually:

```text
Frequency
   │
   │        █
   │      █ █ █
   │    █ █ █ █ █
   │  █ █ █ █ █ █ █
   └──────────────────
       Age
```

---

# 2. আজকের Dataset

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

আমরা `total_bill` নিয়ে কাজ করব।

---

# 3. `histplot()` — Histogram ⭐⭐⭐

Histogram numerical data-এর distribution দেখায়।

```python
sns.histplot(
    data=df,
    x="total_bill"
)

plt.show()
```

এখানে:

```text
data → df
x    → total_bill
```

---

# 4. Histogram কী দেখায়?

ধরুন:

```python
sns.histplot(data=df, x="total_bill")
```

Histogram data-কে বিভিন্ন **interval/bin**-এ ভাগ করে।

যেমন:

```text
10–15
15–20
20–25
25–30
30–35
```

তারপর প্রতিটি interval-এ কত observation আছে তা দেখায়।

```text
Frequency
   │
   │       █
   │     █ █ █
   │   █ █ █ █
   │ █ █ █ █ █ █
   └────────────────
     10 15 20 25 30
```

---

# 5. `bins` ⭐

Histogram-এর সবচেয়ে গুরুত্বপূর্ণ parameter-এর একটি হলো `bins`।

```python
sns.histplot(
    data=df,
    x="total_bill",
    bins=10
)

plt.show()
```

আরও বেশি bins:

```python
sns.histplot(
    data=df,
    x="total_bill",
    bins=20
)

plt.show()
```

### Difference

কম bins:

```text
কম detail
```

বেশি bins:

```text
বেশি detail
```

কিন্তু খুব বেশি bins দিলে visualization noisy হতে পারে।

---

# 6. KDE কী?

KDE = **Kernel Density Estimation**

এটি distribution-এর একটি smooth estimate তৈরি করে।

Histogram:

```python
sns.histplot(
    data=df,
    x="total_bill"
)
```

KDE:

```python
sns.kdeplot(
    data=df,
    x="total_bill"
)

plt.show()
```

---

# 7. Histogram + KDE ⭐⭐⭐

বাস্তবে এটি অনেক ব্যবহার করবেন।

```python
sns.histplot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

এখানে:

```text
Histogram
    +
KDE curve
    ↓
Distribution বুঝতে সহজ
```

---

# 8. KDE Curve কীভাবে পড়বেন?

ধরুন curve:

```text
Density
  │
  │        /\
  │       /  \
  │      /    \
  │_____/      \____
  └──────────────────
          Value
```

যেখানে curve বেশি উঁচু:

> সেই range-এ data বেশি concentrated।

---

# 9. `kdeplot()` আলাদাভাবে

```python
sns.kdeplot(
    data=df,
    x="total_bill"
)

plt.show()
```

KDE continuous-looking distribution দেখায়।

---

# 10. `fill=True`

KDE-এর নিচের area fill করতে:

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    fill=True
)

plt.show()
```

এটি distribution-এর shape আরও visually clear করে।

---

# 11. `bw_adjust`

KDE-এর smoothness control করতে:

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    bw_adjust=0.5
)

plt.show()
```

অন্যদিকে:

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    bw_adjust=2
)

plt.show()
```

সহজভাবে:

```text
bw_adjust ছোট
→ বেশি detail
→ বেশি wiggly

bw_adjust বড়
→ বেশি smooth
```

শুরুতে এর mathematical details মুখস্থ করার দরকার নেই।

---

# 12. `hue` দিয়ে Distribution Compare

ধরুন আমরা Male এবং Female-এর bill distribution compare করতে চাই।

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex"
)

plt.show()
```

এখানে:

```text
X → total_bill
Color → sex
```

---

# 13. KDE দিয়ে Group Comparison

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    hue="sex"
)

plt.show()
```

এতে Male এবং Female-এর distribution আলাদাভাবে দেখা যাবে।

---

# 14. `multiple` Parameter ⭐

`histplot()`-এ multiple display modes আছে।

### `layer`

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    multiple="layer"
)

plt.show()
```

Distributionগুলো overlap করবে।

---

# 15. `multiple="stack"`

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    multiple="stack"
)

plt.show()
```

এতে categories stacked হবে।

---

# 16. `multiple="dodge"`

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    multiple="dodge"
)

plt.show()
```

এতে categories পাশাপাশি থাকবে।

---

# 17. `multiple="fill"`

```python
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    multiple="fill"
)

plt.show()
```

এতে প্রতিটি bin-এর relative proportion বোঝা যায়।

---

# 18. `stat` Parameter

Histogram-এর Y-axis কী represent করবে তা পরিবর্তন করা যায়।

Default:

```python
sns.histplot(
    data=df,
    x="total_bill",
    stat="count"
)

plt.show()
```

অর্থাৎ:

> কতগুলো observation আছে।

---

## Density

```python
sns.histplot(
    data=df,
    x="total_bill",
    stat="density"
)

plt.show()
```

এখানে Y-axis density।

---

# 19. Probability

```python
sns.histplot(
    data=df,
    x="total_bill",
    stat="probability"
)

plt.show()
```

এতে proportion/probability দেখা যায়।

---

# 20. Cumulative Histogram

```python
sns.histplot(
    data=df,
    x="total_bill",
    cumulative=True
)

plt.show()
```

এতে cumulative distribution দেখা যায়।

---

# 21. `element="step"`

Histogram-এর bars-এর পরিবর্তে step-style:

```python
sns.histplot(
    data=df,
    x="total_bill",
    element="step"
)

plt.show()
```

---

# 22. `element="poly"`

```python
sns.histplot(
    data=df,
    x="total_bill",
    element="poly"
)

plt.show()
```

এতে polygon-style representation পাওয়া যায়।

---

# 23. `discrete=True`

যখন numerical variable actually discrete/count data, তখন useful।

যেমন `size`:

```python
sns.histplot(
    data=df,
    x="size",
    discrete=True
)

plt.show()
```

কারণ `size` সাধারণত:

```text
1
2
3
4
5
6
```

এর মতো integer values।

---

# 24. `binwidth`

নিজে bin-এর width নির্ধারণ করতে:

```python
sns.histplot(
    data=df,
    x="total_bill",
    binwidth=5
)

plt.show()
```

অর্থাৎ প্রতিটি bin-এর width 5 units।

---

# 25. `binrange`

Distribution-এর নির্দিষ্ট range:

```python
sns.histplot(
    data=df,
    x="total_bill",
    binrange=(0, 50)
)

plt.show()
```

---

# 26. Distribution of Tip

এখন `tip`:

```python
sns.histplot(
    data=df,
    x="tip",
    kde=True
)

plt.show()
```

নিজেকে প্রশ্ন করুন:

* Tip কোন range-এ বেশি?
* Distribution symmetric?
* Right-skewed?
* Outlier আছে?

---

# 27. Distribution of Party Size

```python
sns.histplot(
    data=df,
    x="size",
    discrete=True
)

plt.show()
```

এটি একটি discrete distribution।

---

# 28. Boxplot দিয়ে Distribution-এর আরেক View

Distribution analysis শুধু histogram-এর মধ্যে সীমাবদ্ধ নয়।

```python
sns.boxplot(
    data=df,
    y="total_bill"
)

plt.show()
```

Boxplot আমাদের দেখাতে পারে:

```text
        Outlier
           •
           │
      ┌────┴────┐
      │         │
      │ Median  │
      │         │
      └─────────┘
           │
           │
```

M04-এ আমরা Boxplot বিস্তারিত শিখব।

---

# 29. Distribution + Category

প্রতিটি day-এর bill distribution:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এটি একটি powerful comparison।

---

# 30. Histogram vs KDE vs Boxplot

এক নজরে:

| Visualization | কী দেখায়                                 |
| ------------- | ----------------------------------------- |
| Histogram     | Frequency distribution                    |
| KDE           | Smooth density                            |
| Boxplot       | Median, spread, outliers                  |
| Violinplot    | Distribution shape + boxplot-like summary |

---

# 31. Distribution Shape বুঝুন ⭐⭐⭐

EDA করার সময় distribution-এর shape খুব গুরুত্বপূর্ণ।

সাধারণভাবে:

### Normal Distribution

```text
       /\
      /  \
     /    \
____/      \____
```

মাঝখানে peak।

---

### Right Skewed

```text
       /\
      /  \
     /    \
____/      \________
```

ডানদিকে long tail।

---

### Left Skewed

```text
          /\
         /  \
________/    \____
```

বামদিকে long tail।

---

# 32. Skewness কেন গুরুত্বপূর্ণ?

Machine Learning-এ distribution skewed হলে কিছু model/feature preprocessing-এর ক্ষেত্রে সমস্যা হতে পারে।

উদাহরণ:

```text
Salary
Income
House Price
Transaction Amount
```

এগুলো অনেক সময় right-skewed হতে পারে।

তখন আমরা প্রয়োজন অনুযায়ী transformation বিবেচনা করতে পারি।

যেমন:

```python
import numpy as np

df["log_salary"] = np.log1p(df["salary"])
```

তারপর:

```python
sns.histplot(
    data=df,
    x="log_salary",
    kde=True
)

plt.show()
```

এটি এখনই সব dataset-এ করতে হবে এমন নয়—শুধু conceptটি বুঝুন।

---

# 33. Two Distributions Compare

ধরুন:

```python
sns.kdeplot(
    data=df,
    x="total_bill",
    hue="time"
)

plt.show()
```

এখন:

```text
Lunch distribution
vs
Dinner distribution
```

compare করতে পারবেন।

---

# 34. Faceting দিয়ে Distribution

`col` ব্যবহার করে আলাদা panel:

```python
sns.displot(
    data=df,
    x="total_bill",
    col="sex",
    kde=True
)

plt.show()
```

এখানে `displot()` একটি high-level distribution interface।

---

# 35. `displot()` বনাম `histplot()`

এটি গুরুত্বপূর্ণ।

### `histplot()`

```python
sns.histplot(...)
```

একটি axes-level plot।

### `displot()`

```python
sns.displot(...)
```

figure-level distribution interface।

সহজভাবে:

```text
histplot
→ একটি plot-এর উপর বেশি direct control

displot
→ multiple distributions/facets-এর জন্য convenient
```

---

# 36. `displot()` Example

```python
sns.displot(
    data=df,
    x="total_bill",
    kde=True
)

plt.show()
```

Hue:

```python
sns.displot(
    data=df,
    x="total_bill",
    hue="sex",
    kde=True
)

plt.show()
```

---

# 37. `kind` in `displot()`

Histogram:

```python
sns.displot(
    data=df,
    x="total_bill",
    kind="hist"
)
```

KDE:

```python
sns.displot(
    data=df,
    x="total_bill",
    kind="kde"
)
```

ECDF:

```python
sns.displot(
    data=df,
    x="total_bill",
    kind="ecdf"
)
```

---

# 38. ECDF Plot

ECDF = **Empirical Cumulative Distribution Function**

```python
sns.ecdfplot(
    data=df,
    x="total_bill"
)

plt.show()
```

এটি বলে:

> নির্দিষ্ট একটি value-এর নিচে/সমান কত proportion data রয়েছে?

---

# 39. ECDF সহজ উদাহরণ

ধরুন:

```text
Bill ≤ 20
```

ECDF থেকে বোঝা যাবে:

```text
প্রায় কত % customer-এর bill 20 বা তার কম?
```

এটি distribution বোঝার একটি খুব useful statistical method।

---

# 40. Rug Plot

Rug plot individual observations-এর অবস্থান mark করে।

```python
sns.rugplot(
    data=df,
    x="total_bill"
)

plt.show()
```

এভাবে:

```text
────────────────────────
  | | || ||| | | || |
```

প্রতিটি ছোট line একটি observation-এর location নির্দেশ করে।

---

# 41. Histogram + Rug

```python
sns.histplot(
    data=df,
    x="total_bill"
)

sns.rugplot(
    data=df,
    x="total_bill"
)

plt.show()
```

এতে distribution এবং individual observations দুটোই দেখা যায়।

---

# 42. Distribution Analysis Workflow ⭐⭐⭐

বাস্তব project-এ আপনি এমনভাবে এগোতে পারেন:

```text
Numerical Column
       ↓
histplot()
       ↓
kde=True
       ↓
Distribution Shape
       ↓
Skewness?
       ↓
Outlier?
       ↓
Group Comparison
       ↓
boxplot()
       ↓
Statistical Insight
```

---

# 43. Complete M03 Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load dataset
df = sns.load_dataset("tips")

# Theme
sns.set_theme(style="whitegrid")

# Distribution
plt.figure(figsize=(10, 6))

sns.histplot(
    data=df,
    x="total_bill",
    bins=20,
    kde=True
)

plt.title("Distribution of Total Bill")
plt.xlabel("Total Bill")
plt.ylabel("Frequency")

plt.show()
```

---

# 44. Group Distribution Example ⭐

```python
plt.figure(figsize=(10, 6))

sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    bins=20,
    kde=True
)

plt.title("Total Bill Distribution by Sex")

plt.show()
```

---

# 45. KDE Comparison

```python
plt.figure(figsize=(10, 6))

sns.kdeplot(
    data=df,
    x="total_bill",
    hue="sex",
    fill=True
)

plt.title("Bill Density by Sex")

plt.show()
```

---

# 46. Day-wise Distribution

```python
plt.figure(figsize=(10, 6))

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Total Bill Distribution by Day")

plt.show()
```

---

# 47. M03-এ Data Analyst কী প্রশ্ন করবে?

Visualization করার পর এই প্রশ্নগুলো করবেন:

### Distribution

> Data কোথায় concentrated?

### Spread

> Data কতটা ছড়িয়ে আছে?

### Shape

> Distribution symmetric নাকি skewed?

### Outlier

> Extreme value আছে?

### Group

> Male বনাম Female-এর distribution আলাদা?

### Time

> Lunch বনাম Dinner-এর distribution আলাদা?

### Category

> কোন day-তে bill বেশি/কম?

এগুলোই আপনাকে **plot maker** থেকে **data analyst** বানাবে।

---

# 🧠 M03 Cheat Sheet

```python
# Histogram
sns.histplot(data=df, x="total_bill")

# Histogram + KDE
sns.histplot(data=df, x="total_bill", kde=True)

# KDE
sns.kdeplot(data=df, x="total_bill")

# Filled KDE
sns.kdeplot(data=df, x="total_bill", fill=True)

# Group distribution
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex"
)

# KDE group comparison
sns.kdeplot(
    data=df,
    x="total_bill",
    hue="sex"
)

# ECDF
sns.ecdfplot(
    data=df,
    x="total_bill"
)

# Rug
sns.rugplot(
    data=df,
    x="total_bill"
)

# Figure-level distribution
sns.displot(
    data=df,
    x="total_bill",
    kde=True
)
```

---

# 🎯 M03 Practice Tasks

### Task 1 — Basic Histogram

`total_bill` দিয়ে histogram বানান।

---

### Task 2 — Bins

একই data:

```text
bins=10
bins=20
bins=30
```

দিয়ে তিনটি histogram তৈরি করুন এবং difference observe করুন।

---

### Task 3 — Histogram + KDE

```text
total_bill
+
kde
```

---

### Task 4 — Tip Distribution

`tip`-এর distribution visualize করুন।

---

### Task 5 — Party Size

`size`-এর distribution দেখান এবং `discrete=True` ব্যবহার করুন।

---

### Task 6 — Gender Comparison ⭐

```text
total_bill
hue = sex
```

ব্যবহার করে distribution compare করুন।

---

### Task 7 — Lunch vs Dinner ⭐

```text
total_bill
hue = time
```

দিয়ে distribution compare করুন।

---

### Task 8 — KDE ⭐

Male বনাম Female `total_bill`-এর KDE তৈরি করুন।

---

### Task 9 — ECDF

`total_bill`-এর ECDF plot তৈরি করুন।

---

### Task 10 — Real EDA Question ⭐⭐⭐

নিজের visualization দেখে উত্তর দিন:

> **Tips dataset-এ total bill-এর distribution কেমন?**

তারপর:

> **Male এবং Female customer-এর bill distribution-এর মধ্যে কোনো visual difference আছে কি?**

---

# ✅ M03 Completion Checklist

* [ ] Distribution কী বুঝি
* [ ] `histplot()`
* [ ] `bins`
* [ ] `binwidth`
* [ ] `binrange`
* [ ] `kde=True`
* [ ] `kdeplot()`
* [ ] `fill=True`
* [ ] `bw_adjust`
* [ ] `hue`
* [ ] `multiple`
* [ ] `stat`
* [ ] `cumulative`
* [ ] `discrete`
* [ ] `displot()`
* [ ] `ecdfplot()`
* [ ] `rugplot()`
* [ ] Distribution comparison
* [ ] Skewness-এর basic ধারণা
* [ ] EDA থেকে insight বের করা

### 🔥 M03-এর মূল কথা

```text
Histogram
   ↓
Frequency বুঝুন

KDE
   ↓
Distribution shape বুঝুন

ECDF
   ↓
Cumulative proportion বুঝুন

Rug
   ↓
Individual observations বুঝুন

সবগুলো
   ↓
EDA
   ↓
Data সম্পর্কে Insight
```

**M04 হবে — Seaborn `Boxplot` Deep Dive: Median, Quartile, IQR, Outlier, Whisker, Hue, Group Comparison এবং বাস্তব EDA-তে outlier detection।**

---
# Seaborn M04 — Boxplot Deep Dive 📦📊

M03-এ আমরা **Distribution Analysis** শিখেছি—`histplot()`, `kdeplot()`, `ecdfplot()` ইত্যাদি।

আজকের M04-এর মূল বিষয়:

> **Boxplot কীভাবে distribution, median, quartile, IQR এবং outlier বুঝতে সাহায্য করে।**

Data Analyst এবং ML-এর জন্য Boxplot খুব গুরুত্বপূর্ণ, বিশেষ করে **outlier detection** এবং **group comparison**-এর জন্য।

---

# 1. Boxplot কী?

Boxplot একটি numerical variable-এর distribution-এর গুরুত্বপূর্ণ statistical summary দেখায়।

একটি সাধারণ boxplot:

```text
              •  ← Outlier
              │
         ─────┤  ← Upper whisker
         ┌────┐
         │    │
         │ ───│  ← Median
         │    │
         └────┘
              │
         ─────┤  ← Lower whisker
```

এখানে আমরা সাধারণত দেখি:

* Minimum / lower whisker
* Q1
* Median
* Q3
* Maximum / upper whisker
* Outliers

---

# 2. কেন Boxplot গুরুত্বপূর্ণ?

ধরুন আপনার dataset-এ `salary` আছে:

```text
25000
30000
35000
40000
45000
50000
...
500000
```

Histogram দেখে distribution বোঝা যাবে।

কিন্তু Boxplot খুব দ্রুত দেখাতে পারে:

```text
Median
Spread
IQR
Outlier
```

বিশেষ করে:

> **একাধিক category-এর distribution compare করার জন্য Boxplot অসাধারণ useful।**

---

# 3. Dataset Load

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

---

# 4. Basic Boxplot

`total_bill`-এর boxplot:

```python
sns.boxplot(
    data=df,
    y="total_bill"
)

plt.show()
```

এখানে:

```text
Y-axis → total_bill
```

---

# 5. Horizontal Boxplot

এবার `x` ব্যবহার করি:

```python
sns.boxplot(
    data=df,
    x="total_bill"
)

plt.show()
```

এতে box horizontal হবে।

---

# 6. Vertical বনাম Horizontal

### Vertical

```python
sns.boxplot(
    data=df,
    y="total_bill"
)
```

### Horizontal

```python
sns.boxplot(
    data=df,
    x="total_bill"
)
```

Concept:

```text
y="total_bill"
      ↓
Vertical


x="total_bill"
      ↓
Horizontal
```

---

# 7. Boxplot-এর ভিতরের অংশগুলো ⭐⭐⭐

এখন সবচেয়ে গুরুত্বপূর্ণ অংশ।

একটি box:

```text
        Q3
    ┌────────┐
    │        │
    │ Median │
    │        │
    └────────┘
        Q1
```

এখানে:

### Q1

25th percentile

```text
25% data
```

এর নিচে থাকে।

### Median

50th percentile।

### Q3

75th percentile।

---

# 8. IQR ⭐⭐⭐

IQR = **Interquartile Range**

Formula:

```text
IQR = Q3 - Q1
```

উদাহরণ:

```text
Q1 = 10
Q3 = 25
```

তাহলে:

```text
IQR = 25 - 10
    = 15
```

Box-এর height/width মূলত IQR represent করে।

---

# 9. Median

Box-এর ভিতরের line হলো median।

```text
    ┌────────┐
    │        │
    │────────│ ← Median
    │        │
    └────────┘
```

Median = 50th percentile।

অর্থাৎ:

```text
50% observations
        ↓
Median
        ↓
50% observations
```

---

# 10. Whisker কী?

Box-এর বাইরে যে lines থাকে সেগুলো whisker।

Conceptually:

```text
       •
       │
    ───┤ ← Upper whisker
    ┌───┐
    │   │
    │───│ ← Median
    │   │
    └───┘
    ───┤ ← Lower whisker
```

Whisker সাধারণত data-এর non-outlier range পর্যন্ত যায়।

---

# 11. Outlier ⭐⭐⭐

Boxplot-এর বাইরে isolated points থাকলে সেগুলো potential outlier।

```text
       •
       •
       │
    ───┤
    ┌───┐
    │───│
    └───┘
    ───┤
```

এখানে উপরের `•`গুলো potential outlier।

---

# 12. Outlier-এর Standard Rule

সাধারণভাবে:

```text
Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR
```

যদি কোনো observation:

```text
< Lower Bound
```

অথবা:

```text
> Upper Bound
```

হয়, তাহলে সেটি সাধারণত outlier হিসেবে চিহ্নিত হয়।

---

# 13. Example

ধরি:

```text
Q1 = 10
Q3 = 20
```

তাহলে:

```text
IQR = 20 - 10
    = 10
```

Lower bound:

```text
10 - 1.5 × 10
= -5
```

Upper bound:

```text
20 + 1.5 × 10
= 35
```

তাহলে:

```text
< -5 → potential outlier

> 35 → potential outlier
```

---

# 14. Seaborn কীভাবে Outlier দেখায়?

```python
sns.boxplot(
    data=df,
    y="total_bill"
)

plt.show()
```

যদি whisker-এর বাইরে points থাকে, সেগুলো visualভাবে potential outlier হিসেবে দেখা যাবে।

---

# 15. Category অনুযায়ী Boxplot ⭐⭐⭐

এখন সবচেয়ে useful কাজ।

প্রতিটি day-এর `total_bill` compare করি:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এখানে:

```text
X → day
Y → total_bill
```

অর্থাৎ:

```text
Thursday
Friday
Saturday
Sunday
```

প্রতিটি দিনের bill distribution compare হচ্ছে।

---

# 16. কীভাবে Plot Interpret করবেন?

প্রতিটি box দেখে compare করুন:

### Median

কোন day-এর median bill বেশি?

### Box size

কোন day-এর spread বেশি?

### Whisker

কোন group-এর range বেশি?

### Outlier

কোন day-তে extreme observation আছে?

---

# 17. `hue` ⭐⭐⭐

Gender অনুযায়ী day-এর bill distribution compare:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

এখন:

```text
X     → day
Y     → total_bill
Color → sex
```

একটি plot-এ:

```text
Day
 ↓
Male vs Female
 ↓
Bill distribution
```

compare করা যাচ্ছে।

---

# 18. Boxplot + Time

Lunch বনাম Dinner:

```python
sns.boxplot(
    data=df,
    x="time",
    y="total_bill"
)

plt.show()
```

এতে:

```text
Lunch
vs
Dinner
```

bill distribution compare করা যাবে।

---

# 19. Boxplot + Smoker

```python
sns.boxplot(
    data=df,
    x="smoker",
    y="total_bill"
)

plt.show()
```

Question:

> Smoker এবং non-smoker customer-এর bill distribution কি আলাদা?

---

# 20. `order`

Category-এর order নিজে specify করতে পারেন।

```python
order = ["Thur", "Fri", "Sat", "Sun"]

sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    order=order
)

plt.show()
```

এটি presentation-এর জন্য useful।

---

# 21. `orient`

Orientation explicitly দিতে পারেন:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    orient="v"
)

plt.show()
```

Horizontal হলে:

```python
sns.boxplot(
    data=df,
    x="total_bill",
    y="day",
    orient="h"
)

plt.show()
```

---

# 22. `width`

Box-এর width পরিবর্তন:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    width=0.5
)

plt.show()
```

---

# 23. `whis`

Whisker-এর range control করতে `whis` ব্যবহার করা যায়।

Default behavior সাধারণত 1.5 × IQR ভিত্তিক।

উদাহরণ:

```python
sns.boxplot(
    data=df,
    y="total_bill",
    whis=2
)

plt.show()
```

এটি whisker-এর definition পরিবর্তন করে।

---

# 24. `showfliers`

Outlier points hide করতে:

```python
sns.boxplot(
    data=df,
    y="total_bill",
    showfliers=False
)

plt.show()
```

এখানে box এবং whisker থাকবে, কিন্তু individual outlier markers দেখাবে না।

### কেন hide করবেন?

যদি dataset অনেক বড় হয়:

```text
অনেক outlier points
       ↓
Plot cluttered
```

তখন `showfliers=False` useful হতে পারে।

---

# 25. কিন্তু Outlier Hide মানেই Remove নয় ⚠️

এটি খুব গুরুত্বপূর্ণ।

```python
showfliers=False
```

করলে শুধু **visualization থেকে points hide** হয়।

Dataset থেকে outlier remove হয় না।

অর্থাৎ:

```text
showfliers=False
       ↓
Plot থেকে hide
       ≠
Data থেকে delete
```

---

# 26. Boxplot-এর Mean

Boxplot মূলত median-centric।

তবে mean দেখানো যায়।

```python
sns.boxplot(
    data=df,
    y="total_bill",
    showmeans=True
)

plt.show()
```

এখন mean-এর marker দেখতে পারবেন।

---

# 27. Mean বনাম Median ⭐

এটি Data Analysis-এর জন্য খুব গুরুত্বপূর্ণ।

ধরুন:

```text
10
11
12
13
100
```

Mean:

```text
(10+11+12+13+100)/5
= 29.2
```

Median:

```text
12
```

Outlier `100` mean-কে অনেক বেশি influence করেছে।

তাই skewed data-এর ক্ষেত্রে:

> **Median অনেক সময় central tendency-এর জন্য বেশি robust।**

Boxplot এজন্য খুব useful।

---

# 28. Boxplot দিয়ে Skewness-এর Basic Idea

যদি median box-এর এক পাশে বেশি কাছাকাছি থাকে এবং whiskers অসমান হয়, তাহলে distribution skewed হওয়ার indication হতে পারে।

উদাহরণ:

```text
       ┌────┐
       │    │
       │─   │
       │    │
       └────┘
          \
           \
            \
```

Long right whisker:

> Right-skewed-এর indication হতে পারে।

তবে exact skewness বিচার করতে histogram/KDE-ও দেখবেন।

---

# 29. Histogram + Boxplot ⭐⭐⭐

Professional EDA-তে দুটো একসাথে ব্যবহার করা খুব useful।

```python
fig, axes = plt.subplots(
    2,
    1,
    figsize=(10, 8)
)

sns.histplot(
    data=df,
    x="total_bill",
    kde=True,
    ax=axes[0]
)

sns.boxplot(
    data=df,
    x="total_bill",
    ax=axes[1]
)

plt.tight_layout()
plt.show()
```

এখানে:

```text
Histogram
   ↓
Distribution shape

Boxplot
   ↓
Median + IQR + Outlier
```

---

# 30. Group-wise Outlier Analysis ⭐⭐⭐

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এটি খুব useful কারণ overall outlier এবং group-wise outlier এক জিনিস নয়।

উদাহরণ:

```text
Overall dataset
      ↓
Outlier

কিন্তু

Specific category
      ↓
Maybe normal for that category
```

তাই category-wise boxplot করা গুরুত্বপূর্ণ।

---

# 31. Boxplot + Stripplot

Individual points-ও দেখতে চাইলে:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এতে:

```text
Boxplot
+
Individual observations
```

দুটোই দেখা যায়।

---

# 32. Boxplot + Swarmplot

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এটি dataset ছোট হলে খুব সুন্দরভাবে individual distribution বুঝতে সাহায্য করে।

---

# 33. Real-World Example

ধরুন employee dataset:

```text
Employee
Department
Salary
Experience
```

আমরা salary distribution department অনুযায়ী দেখতে চাই:

```python
sns.boxplot(
    data=df,
    x="Department",
    y="Salary"
)

plt.show()
```

এখন আমরা জানতে পারি:

* কোন department-এর median salary বেশি?
* কোন department-এ salary variation বেশি?
* কোন department-এ potential outlier আছে?

---

# 34. ML-এর জন্য Boxplot ⭐⭐⭐

Machine Learning-এর আগে Boxplot ব্যবহার করতে পারেন:

```text
Raw Dataset
     ↓
EDA
     ↓
Boxplot
     ↓
Outlier Detection
     ↓
Investigate Outliers
     ↓
Feature Engineering
     ↓
ML Model
```

কিন্তু একটি গুরুত্বপূর্ণ rule:

> **Outlier দেখলেই delete করবেন না।**

প্রথমে বুঝুন outlierটি:

* Data entry error?
* Genuine observation?
* Rare event?
* Business-important event?

---

# 35. Outlier Detect করার জন্য Pandas + IQR

Seaborn visualization-এর পাশাপাশি Pandas দিয়ে calculation করতে পারেন।

```python
Q1 = df["total_bill"].quantile(0.25)
Q3 = df["total_bill"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

print("Q1:", Q1)
print("Q3:", Q3)
print("IQR:", IQR)
print("Lower:", lower)
print("Upper:", upper)
```

Outliers:

```python
outliers = df[
    (df["total_bill"] < lower) |
    (df["total_bill"] > upper)
]

print(outliers)
```

---

# 36. Outlier Count

```python
print("Outlier count:", len(outliers))
```

Percentage:

```python
percentage = len(outliers) / len(df) * 100

print("Outlier percentage:", percentage)
```

---

# 37. Boxplot + IQR Workflow ⭐⭐⭐

```text
Numerical Feature
       ↓
Boxplot
       ↓
Potential Outliers
       ↓
Calculate Q1
       ↓
Calculate Q3
       ↓
IQR = Q3 - Q1
       ↓
Lower / Upper Bound
       ↓
Investigate
       ↓
Decision
```

এটাই practical workflow।

---

# 38. Complete M04 Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load dataset
df = sns.load_dataset("tips")

# Theme
sns.set_theme(style="whitegrid")

# Boxplot
plt.figure(figsize=(10, 6))

sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.title("Total Bill Distribution by Day and Sex")
plt.xlabel("Day")
plt.ylabel("Total Bill")

plt.show()
```

---

# 39. Another Complete Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

plt.figure(figsize=(10, 6))

sns.boxplot(
    data=df,
    x="time",
    y="total_bill"
)

plt.title("Total Bill Distribution: Lunch vs Dinner")

plt.show()
```

নিজেকে প্রশ্ন করুন:

> Dinner-এর median কি Lunch-এর চেয়ে বেশি?

> কোন group-এর spread বেশি?

> কোনো potential outlier আছে?

---

# 40. M04 Cheat Sheet

```python
# Basic vertical
sns.boxplot(
    data=df,
    y="total_bill"
)

# Horizontal
sns.boxplot(
    data=df,
    x="total_bill"
)

# Category comparison
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

# Hue
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

# Custom order
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    order=["Thur", "Fri", "Sat", "Sun"]
)

# Hide outliers visually
sns.boxplot(
    data=df,
    y="total_bill",
    showfliers=False
)

# Show mean
sns.boxplot(
    data=df,
    y="total_bill",
    showmeans=True
)
```

---

# 🧠 M04-এর সবচেয়ে গুরুত্বপূর্ণ Formula

এগুলো অবশ্যই বুঝে রাখবেন:

```text
Q1 = 25th percentile

Median = 50th percentile

Q3 = 75th percentile

IQR = Q3 - Q1
```

Outlier rule:

```text
Lower Bound = Q1 - 1.5 × IQR

Upper Bound = Q3 + 1.5 × IQR
```

---

# 🎯 M04 Practice Tasks

### Task 1 — Basic

`total_bill`-এর vertical boxplot তৈরি করুন।

---

### Task 2

`total_bill`-এর horizontal boxplot তৈরি করুন।

---

### Task 3

`day` অনুযায়ী `total_bill` compare করুন।

```text
x = day
y = total_bill
```

---

### Task 4 ⭐

`day` + `sex` ব্যবহার করে:

```python
hue="sex"
```

সহ boxplot বানান।

---

### Task 5

`time` অনুযায়ী `total_bill` compare করুন।

---

### Task 6

`smoker` অনুযায়ী `tip` distribution-এর boxplot তৈরি করুন।

---

### Task 7 ⭐

`total_bill`-এর:

```text
Q1
Q3
IQR
Lower Bound
Upper Bound
```

নিজে Python দিয়ে calculate করুন।

---

### Task 8 ⭐⭐

IQR rule ব্যবহার করে potential outlier rows বের করুন।

---

### Task 9 ⭐⭐⭐

একই dataset-এর জন্য:

```text
Histogram + KDE
        +
Boxplot
```

তৈরি করুন।

তারপর লিখুন:

> Distribution কেমন?

> Median কোথায়?

> Outlier আছে কি?

> Data skewed মনে হচ্ছে কি?

---

# ✅ M04 Completion Checklist

* [ ] Boxplot কী
* [ ] Median
* [ ] Q1
* [ ] Q3
* [ ] IQR
* [ ] Whisker
* [ ] Outlier
* [ ] 1.5 × IQR rule
* [ ] `sns.boxplot()`
* [ ] Horizontal boxplot
* [ ] Vertical boxplot
* [ ] Category comparison
* [ ] `hue`
* [ ] `order`
* [ ] `width`
* [ ] `whis`
* [ ] `showfliers`
* [ ] `showmeans`
* [ ] Boxplot + Stripplot
* [ ] Boxplot + Swarmplot
* [ ] Pandas + IQR
* [ ] Outlier interpretation

## 🔥 M04 Mental Model

```text
                 Boxplot
                    │
        ┌───────────┼───────────┐
        ↓           ↓           ↓
     Center       Spread      Outlier
        │           │           │
      Median       IQR       1.5×IQR
        │           │           │
        └───────────┼───────────┘
                    ↓
                   EDA
                    ↓
             Data Understanding
                    ↓
              ML Preparation
```

**M05-এ আমরা `Violinplot` শিখব — Boxplot-এর সাথে KDE/Distribution Shape কীভাবে combine হয়, `inner`, `split`, `hue`, `density`, category comparison এবং Boxplot বনাম Violinplot কখন ব্যবহার করবেন।**


---
# Seaborn M05 — Violinplot Deep Dive 🎻📊

M04-এ আমরা **Boxplot** শিখেছি। এখন M05-এ শিখব **Violinplot**।

Violinplot খুব গুরুত্বপূর্ণ কারণ এটি একসাথে:

* Distribution shape দেখায়
* Median দেখাতে পারে
* Quartile দেখাতে পারে
* Category অনুযায়ী data compare করতে পারে
* KDE ব্যবহার করে data density দেখায়

বিশেষ করে **EDA + Machine Learning dataset analysis**-এ এটি অনেক useful।

---

# 1. Violinplot কী?

**Violin Plot = Distribution/KDE shape + Summary statistics**

একটি violinplot দেখতে অনেকটা violin-এর মতো:

```text
       ╭────╮
       │    │
      ╭╯    ╰╮
     ╭╯      ╰╮
     │   ──   │
     │  ────  │
     ╰╮      ╭╯
      ╰╮    ╭╯
       │    │
       ╰────╯
```

এখানে width বোঝায়:

> কোন value-এর আশেপাশে data কত বেশি concentrated।

---

# 2. Boxplot বনাম Violinplot

ধরো আমাদের কাছে:

```text
10, 12, 13, 14, 15, 15, 16, 17, 18, 30
```

Boxplot আমাদের বলবে:

```text
Minimum
Q1
Median
Q3
Maximum / whisker
Outliers
```

কিন্তু Violinplot আরও একটি গুরুত্বপূর্ণ বিষয় দেখাবে:

```text
কোন range-এ data বেশি concentrated?
```

অর্থাৎ:

**Boxplot → summary**

**Violinplot → summary + distribution shape**

---

# 3. Basic Violinplot

প্রথমে dataset:

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

তারপর:

```python
sns.violinplot(data=df, y="total_bill")

plt.show()
```

এখানে:

* `data=df` → dataset
* `y="total_bill"` → যে numerical variable analyse করছি

---

# 4. Horizontal Violinplot

চাইলে horizontal করা যায়:

```python
sns.violinplot(
    data=df,
    x="total_bill"
)

plt.show()
```

Vertical:

```python
sns.violinplot(
    data=df,
    y="total_bill"
)

plt.show()
```

---

# 5. Violinplot কীভাবে Read করব?

ধরো:

```python
sns.violinplot(
    data=df,
    y="total_bill"
)

plt.show()
```

Violin-এর **মোটা অংশ**:

> সেখানে বেশি data আছে।

Violin-এর **পাতলা অংশ**:

> সেখানে কম data আছে।

Example:

```text
       │
      ╭╮
     ╭  ╮
     │  │
    ╭    ╮   ← বেশি density
    │    │
    │    │
     ╲  ╱
      ╲╱
       │
```

অর্থাৎ width = **density**।

---

# 6. Category অনুযায়ী Violinplot

এটাই সবচেয়ে useful অংশ।

ধরো আমরা দেখতে চাই:

> কোন দিনে restaurant bill বেশি?

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এখন:

```text
Thur
Fri
Sat
Sun
```

প্রতিটি category-এর distribution আলাদাভাবে দেখতে পারব।

---

# 7. `hue` ব্যবহার

এখন ধরো আমরা দেখতে চাই:

> Male এবং Female customer-এর bill distribution কেমন?

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

এখানে:

* `x` → category
* `y` → numerical variable
* `hue` → দ্বিতীয় category

এটি EDA-তে খুব powerful।

---

# 8. `inner` Parameter

Violinplot-এর ভিতরে বিভিন্ন ধরনের information দেখানো যায়।

### `inner="box"`

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="box"
)

plt.show()
```

এতে violin-এর ভিতরে ছোট boxplot থাকবে।

---

### `inner="quart"`

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="quart"
)

plt.show()
```

এতে quartiles দেখা যায়।

---

### `inner="point"`

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="point"
)

plt.show()
```

---

### `inner="stick"`

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="stick"
)

plt.show()
```

এতে individual observations-এর মতো ছোট lines দেখা যায়।

---

### `inner=None`

শুধু distribution দেখতে চাইলে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

plt.show()
```

---

# 9. `fill`

Violin fill করা বা না করা যায়।

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    fill=True
)

plt.show()
```

Unfilled:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    fill=False
)

plt.show()
```

---

# 10. `split`

`hue` দিয়ে দুইটি distribution পাশাপাশি compare করার পরিবর্তে split করা যায়।

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    split=True
)

plt.show()
```

Conceptually:

```text
       Male | Female
          ╲ | ╱
           ╲|╱
           ││
          ╱│╲
         ╱ │ ╲
```

এটি বিশেষভাবে useful যখন দুইটি hue category-এর distribution পাশাপাশি খুব compactভাবে compare করতে চাই।

---

# 11. `density_norm`

Modern Seaborn-এ violin-এর width কীভাবে normalize হবে তা `density_norm` দিয়ে control করা যায়।

### Default:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    density_norm="area"
)

plt.show()
```

### Width অনুযায়ী:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    density_norm="width"
)

plt.show()
```

### Count-এর প্রভাব রাখতে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    density_norm="count"
)

plt.show()
```

সহজভাবে মনে রাখো:

| `density_norm` | ধারণা                                   |
| -------------- | --------------------------------------- |
| `"area"`       | violin-এর area comparable               |
| `"width"`      | maximum width comparable                |
| `"count"`      | observation count-এর প্রভাব width-এ আসে |

---

# 12. `bw_adjust`

Violinplot-এর KDE কতটা smooth হবে তা control করা যায়।

```python
sns.violinplot(
    data=df,
    y="total_bill",
    bw_adjust=0.5
)

plt.show()
```

আরও smooth:

```python
sns.violinplot(
    data=df,
    y="total_bill",
    bw_adjust=2
)

plt.show()
```

Concept:

```text
bw_adjust ছোট
→ বেশি detail
→ বেশি variation

bw_adjust বড়
→ বেশি smooth
→ distribution simpler
```

---

# 13. `cut`

KDE curve-এর range কতটা extend করবে তা control করা যায়।

```python
sns.violinplot(
    data=df,
    y="total_bill",
    cut=0
)

plt.show()
```

`cut=0` দিলে violin observed data range-এর বাইরে KDE extension করবে না।

EDA-তে এটি বেশ useful হতে পারে।

---

# 14. Category Order

Default order পরিবর্তন করা যায়।

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    order=["Sun", "Sat", "Fri", "Thur"]
)

plt.show()
```

এতে category এই order-এ দেখাবে:

```text
Sun → Sat → Fri → Thur
```

---

# 15. `hue_order`

`hue` category-এর order-ও control করা যায়।

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    hue_order=["Female", "Male"]
)

plt.show()
```

---

# 16. Horizontal Category Violinplot

```python
sns.violinplot(
    data=df,
    x="total_bill",
    y="day"
)

plt.show()
```

এখানে:

```text
total_bill → numerical
day        → categorical
```

---

# 17. Violinplot + Boxplot

একটি violinplot-এর ভিতরে boxplot দেখানো যায়:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="box"
)

plt.show()
```

এটি খুব useful combination:

```text
Violin
   ↓
Distribution shape

Box
   ↓
Median + Quartile + IQR
```

---

# 18. Violinplot + Stripplot

Individual observations দেখতে চাইলে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এতে:

**Violin → overall distribution**

**Stripplot → individual data points**

দুটো একসাথে দেখা যায়।

---

# 19. Violinplot + Swarmplot

আরও সুন্দরভাবে individual observations দেখতে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.show()
```

এটি EDA-তে খুব useful।

---

# 20. Real EDA Example

ধরো প্রশ্ন:

> Saturday এবং Sunday-তে customer bill distribution কেমন?

```python
weekend = df[df["day"].isin(["Sat", "Sun"])]

sns.violinplot(
    data=weekend,
    x="day",
    y="total_bill",
    inner="box"
)

plt.title("Weekend Bill Distribution")
plt.xlabel("Day")
plt.ylabel("Total Bill")

plt.show()
```

এখানে আমরা একই সাথে দেখতে পারি:

* Distribution
* Median
* Quartiles
* Density
* Category difference

---

# 21. Gender + Day Analysis

আরও interesting analysis:

> কোন দিনে Male/Female customer-এর bill distribution কেমন?

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    inner="quart"
)

plt.title("Bill Distribution by Day and Gender")
plt.show()
```

এটি একটি real-world EDA question-এর মতো।

---

# 22. Violinplot থেকে কী কী বুঝব?

একটি violinplot দেখার সময় এই প্রশ্নগুলো করো:

### 1. Center কোথায়?

Median/central tendency কোথায়?

### 2. Width কোথায় বেশি?

সেখানে observation বেশি concentrated।

### 3. Shape symmetric?

হলে distribution প্রায় symmetric।

### 4. একদিকে লম্বা?

তাহলে skewness থাকতে পারে।

### 5. একাধিক peak আছে?

হলে distribution **multimodal** হতে পারে।

### 6. Categoryগুলোর shape কি আলাদা?

তাহলে category অনুযায়ী behavior আলাদা হতে পারে।

---

# 23. Violinplot দিয়ে Skewness

ধরো:

```text
Normal-ish

       ╭╮
      ╭  ╮
     ╭    ╮
     │    │
      ╲  ╱
       ╲╱
```

Right-skewed হলে:

```text
     ╭╮
    ╭  ╮
   ╭   ╰────────
  ╭
 ╭
```

অর্থাৎ distribution একদিকে tail করছে।

EDA-তে এটি গুরুত্বপূর্ণ কারণ skewed feature-এর ক্ষেত্রে পরে transformation দরকার হতে পারে।

---

# 24. Multimodal Distribution

ধরো violin-এর মধ্যে দুইটি বড় অংশ:

```text
       ╭╮
      ╭  ╮
      │  │
     ╭    ╮
     │    │
      ╲  ╱
       │
      ╭ ╮
     ╭   ╮
     │   │
      ╲ ╱
```

এখানে দুইটি peak থাকতে পারে।

এটি indicate করতে পারে:

> Data-এর মধ্যে দুই ধরনের population/group আছে।

Machine Learning EDA-তে এটি খুব interesting finding।

---

# 25. Boxplot বনাম Violinplot

| বিষয়                | Boxplot | Violinplot           |
| ------------------- | ------- | -------------------- |
| Median              | ✅       | ✅/inner option       |
| Q1/Q3               | ✅       | ✅/inner option       |
| IQR                 | ✅       | কিছুটা               |
| Outlier detection   | ⭐⭐⭐     | ⭐                    |
| Distribution shape  | ❌       | ⭐⭐⭐                  |
| Density             | ❌       | ✅                    |
| Category comparison | ✅       | ✅                    |
| Individual points   | ❌       | strip/swarm যোগ করলে |
| সহজ interpretation  | ⭐⭐⭐     | ⭐⭐                   |
| Detailed EDA        | ⭐⭐      | ⭐⭐⭐                  |

### Rule:

**Outlier দেখতে → Boxplot**

**Distribution shape দেখতে → Violinplot**

**দুটোই দেখতে → Violinplot + inner="box"**

---

# 26. একটি গুরুত্বপূর্ণ বিষয়

Violinplot-এর width দেখে কখনো সরাসরি বলবে না:

> "এই category-তে data বেশি।"

কারণ width normalization-এর setting-এর উপর interpretation নির্ভর করতে পারে।

যদি observation count compare করতে চাও, `density_norm="count"`-এর মতো appropriate normalization ব্যবহার করো অথবা আলাদাভাবে countplot দেখো।

---

# 27. ML Dataset-এ Violinplot

ধরো তোমার dataset:

```text
Age
Income
CreditScore
LoanAmount
Default
```

তাহলে:

```python
sns.violinplot(
    data=df,
    x="Default",
    y="Income"
)

plt.show()
```

প্রশ্ন:

> Default এবং Non-default customer-এর income distribution কি আলাদা?

আর:

```python
sns.violinplot(
    data=df,
    x="Default",
    y="CreditScore"
)

plt.show()
```

প্রশ্ন:

> Credit score কি দুই class-এর মধ্যে আলাদা distribution তৈরি করছে?

এগুলো **feature analysis**-এর খুব ভালো starting point।

---

# 28. Classification Dataset Example

ধরো:

```text
Class 0 = Normal
Class 1 = Suspicious
```

এবং feature:

```text
motion_score
brightness
person_count
```

তাহলে:

```python
sns.violinplot(
    data=df,
    x="class",
    y="motion_score",
    inner="box"
)

plt.show()
```

এতে দেখা যাবে:

```text
Normal
   vs
Suspicious
```

এর `motion_score` distribution কেমন।

যদি দুই class-এর distribution অনেক আলাদা হয়, featureটি classification-এর জন্য potentially useful হতে পারে।

তবে **শুধু violinplot দেখে feature useful নিশ্চিত করা যাবে না**—statistical analysis এবং model validation দরকার।

---

# 29. Complete Violinplot EDA Code

একটি reusable template:

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Dataset
df = sns.load_dataset("tips")

# Basic information
print(df.head())
print(df.shape)
print(df.dtypes)

# Violinplot
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    inner="box",
    density_norm="width"
)

plt.title("Total Bill Distribution by Day and Sex")
plt.xlabel("Day")
plt.ylabel("Total Bill")

plt.show()
```

এটা ভালোভাবে বুঝতে পারলে তুমি real dataset-এ একই pattern apply করতে পারবে।

---

# 30. Violinplot Cheat Sheet

### Basic

```python
sns.violinplot(data=df, y="total_bill")
```

### Category

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill"
)
```

### Hue

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)
```

### Box inside

```python
inner="box"
```

### Quartiles

```python
inner="quart"
```

### No inner

```python
inner=None
```

### Split

```python
split=True
```

### Width normalization

```python
density_norm="width"
```

### Count normalization

```python
density_norm="count"
```

### KDE smoothing

```python
bw_adjust=0.5
```

### No KDE extension outside data

```python
cut=0
```

### Custom order

```python
order=["Sun", "Sat", "Fri", "Thur"]
```

---

# 31. Practice — Beginner 🟢

### Task 1

`tips` dataset-এর `total_bill` দিয়ে basic violinplot বানাও।

### Task 2

`day` অনুযায়ী `total_bill` compare করো।

### Task 3

`sex` অনুযায়ী `total_bill` compare করো।

### Task 4

`inner="box"` ব্যবহার করো।

### Task 5

Horizontal violinplot বানাও।

---

# 32. Practice — Intermediate 🟡

### Task 6

`day + sex + total_bill` analyse করো:

```text
day → x
total_bill → y
sex → hue
```

### Task 7

`split=True` ব্যবহার করো।

### Task 8

`density_norm="count"` এবং `"width"` compare করো।

### Task 9

`bw_adjust=0.5` এবং `2` compare করো।

### Task 10

Violinplot-এর সাথে `stripplot` যোগ করো।

---

# 33. Practice — Advanced 🔴

নিজের কোনো dataset নিয়ে:

### Task 11

একটি categorical variable এবং একটি numerical variable নির্বাচন করো।

তারপর:

```text
Category → Distribution
```

analyse করো।

### Task 12

Violinplot + Boxplot ব্যবহার করে:

* Median
* Quartiles
* Distribution
* Density

ব্যাখ্যা করো।

### Task 13

দুইটি class থাকলে:

```text
Class 0
Class 1
```

একটি numerical feature-এর distribution compare করো।

### Task 14

একটি feature-এর মধ্যে:

* skewness
* multiple peaks
* concentration
* class separation

খুঁজে বের করো।

---

# 34. M05 Completion Checklist ✅

M05 শেষ করার পর এগুলো নিজে explain করতে পারা উচিত:

* [ ] Violinplot কী?
* [ ] Violinplot কেন ব্যবহার করি?
* [ ] Density কী?
* [ ] Width কী represent করে?
* [ ] `x` এবং `y`
* [ ] `hue`
* [ ] `inner`
* [ ] `inner="box"`
* [ ] `inner="quart"`
* [ ] `inner=None`
* [ ] `split`
* [ ] `fill`
* [ ] `density_norm`
* [ ] `bw_adjust`
* [ ] `cut`
* [ ] `order`
* [ ] `hue_order`
* [ ] Violinplot + Stripplot
* [ ] Violinplot + Swarmplot
* [ ] Boxplot বনাম Violinplot
* [ ] Distribution shape interpret করা
* [ ] ML feature distribution analysis

---

## 🎯 M05-এর মূল ধারণা

সবচেয়ে গুরুত্বপূর্ণভাবে মনে রাখো:

```text
BOXPLOT
   ↓
Median + Quartile + IQR + Outlier
```

আর

```text
VIOLINPLOT
   ↓
Distribution + Density
   +
Median/Quartile (যদি inner ব্যবহার করি)
```

আর real EDA-তে সবচেয়ে শক্তিশালী combination:

```text
Pandas
   ↓
Data Cleaning
   ↓
Violinplot
   ↓
Distribution বুঝা
   ↓
Feature Comparison
   ↓
ML Feature Selection-এর ধারণা
```

**M05 complete হলে পরের logical step হলো M06 — `Countplot & Barplot Deep Dive`**, যেখানে categorical data, frequency, proportion, `hue`, ordering এবং category-based EDA গভীরভাবে শিখব।

---
# Seaborn M06 — Countplot & Barplot Deep Dive 📊

M05-এ আমরা **Violinplot** দিয়ে numerical data-এর distribution দেখেছি।

এখন M06-এ শিখব **Categorical Data Analysis**-এর দুইটি সবচেয়ে গুরুত্বপূর্ণ plot:

1. **Countplot** → কতগুলো observation আছে?
2. **Barplot** → প্রতিটি category-এর numerical value-এর summary/average কেমন?

এই দুইটার পার্থক্য ভালোভাবে বোঝা খুব গুরুত্বপূর্ণ। EDA, Data Analysis এবং Machine Learning—সব জায়গাতেই এগুলো ব্যবহার হবে।

---

# 1. প্রথমে Countplot বনাম Barplot বুঝি

ধরো আমাদের dataset:

```text
Day
---
Thur
Fri
Sat
Sat
Sun
Sat
Thur
Sun
```

আমরা জানতে চাই:

> কোন দিনে কতজন customer এসেছে?

এখানে **Countplot** ব্যবহার করব।

```text
Thur  █████
Fri   ██
Sat   ███████
Sun   ████
```

অন্যদিকে যদি প্রশ্ন হয়:

> কোন দিনে average bill কত?

তাহলে **Barplot** ব্যবহার করব।

```text
Thur  ███████
Fri   █████
Sat   █████████
Sun   ████████
```

অর্থাৎ:

```text
Countplot
    ↓
COUNT / FREQUENCY

Barplot
    ↓
NUMERICAL SUMMARY
যেমন Mean
```

---

# 2. Dataset তৈরি

আমরা Seaborn-এর `tips` dataset ব্যবহার করব।

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

Dataset-এর গুরুত্বপূর্ণ columns:

```text
total_bill
tip
sex
smoker
day
time
size
```

---

# 3. Countplot কী?

`countplot()` একটি categorical variable-এর প্রতিটি category-তে **কতটি observation আছে** সেটা দেখায়।

Basic syntax:

```python
sns.countplot(data=df, x="day")

plt.show()
```

এখানে:

```text
x = day
```

Seaborn নিজে count করবে:

```text
Thur → কতটি row
Fri  → কতটি row
Sat  → কতটি row
Sun  → কতটি row
```

---

# 4. Countplot-এর কাজ নিজে বুঝি

ধরো:

```python
print(df["day"].value_counts())
```

Output-এর ধারণা:

```text
Sat     ...
Sun     ...
Thur    ...
Fri     ...
```

Countplot basically এই frequency-কে visual form-এ দেখাচ্ছে।

```python
sns.countplot(data=df, x="day")
plt.show()
```

---

# 5. Countplot কেন গুরুত্বপূর্ণ?

EDA-তে প্রথমেই categorical variable-এর distribution দেখতে হয়।

যেমন:

```text
Gender
------
Male
Female
```

প্রশ্ন:

> Male কতজন? Female কতজন?

```python
sns.countplot(data=df, x="sex")
plt.show()
```

---

# 6. Horizontal Countplot

Vertical:

```python
sns.countplot(
    data=df,
    x="day"
)

plt.show()
```

Horizontal:

```python
sns.countplot(
    data=df,
    y="day"
)

plt.show()
```

Horizontal plot useful যখন category name বড় হয়।

---

# 7. `hue` দিয়ে দ্বিতীয় category

এটি Countplot-এর সবচেয়ে গুরুত্বপূর্ণ feature।

ধরো:

> প্রতিটি দিনে Male এবং Female customer কতজন?

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.show()
```

এখন প্রতিটি day-এর মধ্যে:

```text
Thur → Male / Female
Fri  → Male / Female
Sat  → Male / Female
Sun  → Male / Female
```

compare করা যাবে।

---

# 8. Countplot থেকে কী বুঝব?

ধরো plot:

```text
Sat   █████████ Male
      ████      Female

Sun   █████ Male
      ████  Female
```

তাহলে আমরা বুঝতে পারি:

* কোন day-তে বেশি customer
* কোন day-তে কম customer
* gender distribution
* category imbalance

---

# 9. `order`

Default category order পরিবর্তন করতে পারি।

```python
sns.countplot(
    data=df,
    x="day",
    order=["Sun", "Sat", "Fri", "Thur"]
)

plt.show()
```

এখন order হবে:

```text
Sun → Sat → Fri → Thur
```

---

# 10. `hue_order`

`hue`-এর order-ও পরিবর্তন করা যায়।

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex",
    hue_order=["Female", "Male"]
)

plt.show()
```

---

# 11. Countplot-এর সংখ্যা বের করা

Plot দেখার পাশাপাশি numerical count দেখতে পারো:

```python
print(df["day"].value_counts())
```

আর sorted order চাইলে:

```python
print(df["day"].value_counts().sort_index())
```

---

# 12. Countplot + Percentage

অনেক সময় শুধু count যথেষ্ট নয়।

ধরো:

```text
Male   = 157
Female = 87
```

Count জানা গেল।

কিন্তু percentage?

```python
percentage = df["sex"].value_counts(normalize=True) * 100

print(percentage)
```

Output-এর ধারণা:

```text
Male      64%
Female    36%
```

EDA-তে count এবং percentage দুটোই useful।

---

# 13. Percentage Countplot

Seaborn `countplot()` সরাসরি percentage bar তৈরি করার জন্য মূলত count plot করে; percentage display চাইলে আগে aggregation করে `barplot()` ব্যবহার করা বেশি পরিষ্কার।

উদাহরণ:

```python
percentage = (
    df["sex"]
    .value_counts(normalize=True)
    .mul(100)
    .rename_axis("sex")
    .reset_index(name="percentage")
)

print(percentage)
```

তারপর:

```python
sns.barplot(
    data=percentage,
    x="sex",
    y="percentage"
)

plt.ylabel("Percentage (%)")
plt.show()
```

এখানে Countplot নয়—**Barplot** ব্যবহার করছি কারণ এখন আমাদের কাছে aggregated numerical value (`percentage`) আছে।

---

# 14. Barplot কী?

এখন আসি Barplot-এ।

Barplot সাধারণত:

> একটি categorical variable-এর প্রতিটি category-এর numerical variable-এর aggregated value দেখায়।

Basic:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এখানে Seaborn প্রতিটি day-এর `total_bill`-এর **mean** দেখাবে।

Concept:

```text
Thur → mean(total_bill)
Fri  → mean(total_bill)
Sat  → mean(total_bill)
Sun  → mean(total_bill)
```

---

# 15. Countplot বনাম Barplot — সবচেয়ে গুরুত্বপূর্ণ পার্থক্য

এই দুইটি line মনে রাখো:

```text
Countplot:
"What is the COUNT?"

Barplot:
"What is the SUMMARY VALUE?"
```

Example:

### Question 1

> Saturday-তে কতজন customer?

```python
sns.countplot(data=df, x="day")
```

### Question 2

> Saturday-তে average bill কত?

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

---

# 16. Barplot-এর Default Aggregation

Basic:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

এখানে default estimator সাধারণত:

```text
mean
```

অর্থাৎ:

```text
average total_bill
```

---

# 17. Mean নিজে Calculate করি

ধরো:

```python
print(
    df.groupby("day")["total_bill"].mean()
)
```

এটি প্রায় একই concept-এর numerical result দেয় যা barplot visualize করছে।

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# 18. Median Barplot

সবসময় mean ব্যবহার করতে হবে এমন নয়।

Median ব্যবহার করতে পারো:

```python
import numpy as np

sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator=np.median
)

plt.show()
```

এখন প্রতিটি category-এর:

```text
median(total_bill)
```

দেখাবে।

---

# 19. Sum Barplot

ধরো তুমি জানতে চাও:

> প্রতিটি দিনে মোট bill কত?

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="sum"
)

plt.show()
```

এখন:

```text
Thur → total bill
Fri  → total bill
Sat  → total bill
Sun  → total bill
```

---

# 20. `estimator` Concept

Barplot-এর খুব গুরুত্বপূর্ণ concept:

```text
estimator
```

এটি বলে:

> প্রতিটি category-এর numerical data কীভাবে summarize করব?

Examples:

```python
estimator="mean"
```

```python
estimator=np.median
```

```python
estimator="sum"
```

সহজভাবে:

```text
Raw Data
   ↓
Group by Category
   ↓
Aggregation
   ↓
Barplot
```

---

# 21. `hue` with Barplot

ধরো:

> প্রতিটি day-তে Male/Female-এর average bill কত?

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

এটি খুব powerful analysis।

---

# 22. Barplot + `estimator=np.median`

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    estimator=np.median
)

plt.show()
```

এখন:

```text
Day
 ↓
Sex
 ↓
Median Bill
```

---

# 23. Error Bars

এখানে একটি গুরুত্বপূর্ণ বিষয় আছে।

Barplot শুধু average দেখায় না; statistical uncertainty/error information-ও দেখাতে পারে।

উদাহরণ:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Bar-এর উপরে ছোট vertical line দেখতে পারো।

Concept:

```text
       │
       │  ← uncertainty / error interval
     ███
     ███
     ███
```

Modern Seaborn-এ `errorbar` দিয়ে এটি control করা যায়।

---

# 24. Confidence Interval

উদাহরণ:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar=("ci", 95)
)

plt.show()
```

এটি mean-এর uncertainty বোঝাতে confidence interval ব্যবহার করে।

তবে মনে রাখবে:

> Error bar মানেই data-এর range নয়।

এটি সাধারণত estimate-এর uncertainty বোঝায়।

---

# 25. Error Bar বন্ধ করা

যদি শুধু mean দেখতে চাও:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar=None
)

plt.show()
```

---

# 26. `order` with Barplot

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    order=["Sun", "Sat", "Fri", "Thur"]
)

plt.show()
```

---

# 27. Sorting by Mean

EDA-তে category-গুলো value অনুযায়ী sort করা useful।

প্রথমে:

```python
mean_bill = (
    df.groupby("day")["total_bill"]
    .mean()
    .sort_values(ascending=False)
)

print(mean_bill)
```

তারপর:

```python
sns.barplot(
    data=df,
    x=mean_bill.index,
    y=mean_bill.values
)

plt.show()
```

এতে highest average bill থেকে lowest average bill দেখা যাবে।

---

# 28. Countplot Sort করা

Count অনুযায়ী sort করতে:

```python
order = df["day"].value_counts().index

sns.countplot(
    data=df,
    x="day",
    order=order
)

plt.show()
```

এখন সবচেয়ে বেশি observation-এর category প্রথমে আসবে।

---

# 29. Countplot — One Categorical Variable

Example:

```python
sns.countplot(
    data=df,
    x="smoker"
)

plt.show()
```

Question:

> Smoker এবং non-smoker customer কতজন?

---

# 30. Countplot — Two Categorical Variables

```python
sns.countplot(
    data=df,
    x="smoker",
    hue="sex"
)

plt.show()
```

এখন দেখতে পারি:

```text
Smoker
 ├── Male
 └── Female

Non-smoker
 ├── Male
 └── Female
```

---

# 31. Barplot — Category + Numerical

```python
sns.barplot(
    data=df,
    x="smoker",
    y="tip"
)

plt.show()
```

Question:

> Smoker এবং non-smoker-এর average tip কত?

---

# 32. Groupby + Barplot

Seaborn নিজে aggregation করতে পারে। কিন্তু Pandas দিয়েও আগে aggregation করতে পারো।

```python
avg_tip = (
    df.groupby("day")["tip"]
    .mean()
    .reset_index()
)

print(avg_tip)
```

তারপর:

```python
sns.barplot(
    data=avg_tip,
    x="day",
    y="tip"
)

plt.show()
```

এই workflow খুব গুরুত্বপূর্ণ:

```text
Pandas
 ↓
Groupby
 ↓
Aggregation
 ↓
Seaborn
 ↓
Visualization
```

---

# 33. Countplot vs Pandas `value_counts()`

দুটোর সম্পর্ক:

```python
df["day"].value_counts()
```

এটি numerical answer দেয়।

আর:

```python
sns.countplot(
    data=df,
    x="day"
)
```

visual answer দেয়।

অর্থাৎ:

```text
value_counts()
     ↓
Numbers

countplot()
     ↓
Visual
```

---

# 34. Real EDA Example — Customer Analysis

ধরো প্রশ্ন:

### Q1. কোন দিনে বেশি customer?

```python
sns.countplot(
    data=df,
    x="day"
)

plt.title("Customers by Day")
plt.show()
```

### Q2. কোন দিনে average bill বেশি?

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Average Bill by Day")
plt.show()
```

দুইটি প্রশ্নের উত্তর এক নয়।

এটা খুব গুরুত্বপূর্ণ।

---

# 35. Customer Count বনাম Average Bill

ধরো result:

```text
Saturday → অনেক customer
Sunday   → কম customer
```

কিন্তু:

```text
Sunday   → highest average bill
Saturday → lower average bill
```

তাহলে conclusion হতে পারে:

> Saturday-তে customer বেশি হলেও Sunday-তে per-customer average spending বেশি।

এটাই EDA-এর power।

---

# 36. Countplot + Barplot Together

একটি analysis:

```python
plt.figure(figsize=(12, 5))

plt.subplot(1, 2, 1)

sns.countplot(
    data=df,
    x="day"
)

plt.title("Customer Count")


plt.subplot(1, 2, 2)

sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Average Bill")

plt.tight_layout()
plt.show()
```

এখানে দুইটি আলাদা question-এর answer পাচ্ছি:

```text
COUNT
vs
AVERAGE
```

---

# 37. Business EDA Example

ধরো e-commerce dataset:

```text
category
price
quantity
```

Question:

> কোন category-তে product বেশি?

```python
sns.countplot(
    data=df,
    x="category"
)

plt.show()
```

Question:

> কোন category-এর average price বেশি?

```python
sns.barplot(
    data=df,
    x="category",
    y="price"
)

plt.show()
```

Question:

> কোন category-তে total sales বেশি?

```python
sns.barplot(
    data=df,
    x="category",
    y="sales",
    estimator="sum"
)

plt.show()
```

---

# 38. Machine Learning Dataset Example

ধরো classification dataset:

```text
Class
-----
Normal
Suspicious
```

প্রথমে class distribution:

```python
sns.countplot(
    data=df,
    x="Class"
)

plt.show()
```

এতে বুঝতে পারবে:

```text
Normal      → কত samples
Suspicious  → কত samples
```

এটি অত্যন্ত গুরুত্বপূর্ণ কারণ:

> Dataset balanced নাকি imbalanced?

---

# 39. Class Imbalance

ধরো:

```text
Normal       ████████████████████  9000
Suspicious   ██                    1000
```

এখানে:

```text
Normal = 90%
Suspicious = 10%
```

এটি class imbalance।

ML model training-এর আগে এই distribution জানা খুব গুরুত্বপূর্ণ।

---

# 40. Class + Another Category

ধরো:

```text
Class
Normal
Suspicious

Camera
Camera-1
Camera-2
Camera-3
```

তাহলে:

```python
sns.countplot(
    data=df,
    x="Camera",
    hue="Class"
)

plt.show()
```

এতে camera অনুযায়ী class distribution দেখতে পারবে।

---

# 41. Barplot for ML Feature Analysis

ধরো:

```text
class
motion_score
```

তাহলে:

```python
sns.barplot(
    data=df,
    x="class",
    y="motion_score"
)

plt.show()
```

এতে class-wise average `motion_score` দেখা যাবে।

তবে এখানে একটি গুরুত্বপূর্ণ point:

**Mean আলাদা হলেই feature অবশ্যই ভালো classifier হবে—এমন নয়।**

Distribution overlap, variance, sample size এবং model performance-ও দেখতে হবে।

---

# 42. Countplot-এর Common Mistake

অনেকে লিখে:

```python
sns.countplot(
    data=df,
    x="total_bill"
)
```

এটি numerical continuous variable-এর জন্য সাধারণত ভালো visualization নয়।

কারণ `total_bill`:

```text
16.99
17.50
18.20
19.40
...
```

অনেক unique value থাকতে পারে।

এখানে বরং:

```python
sns.histplot(
    data=df,
    x="total_bill"
)
```

ব্যবহার করা ভালো।

---

# 43. Barplot-এর Common Mistake

ধরো:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

এটি **individual bill distribution** দেখাচ্ছে না।

এটি category-wise aggregated value, সাধারণত mean।

Individual distribution দেখতে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill"
)
```

অথবা:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)
```

ব্যবহার করো।

---

# 44. কোন Plot কখন ব্যবহার করব?

| Question                    | Best Plot       |
| --------------------------- | --------------- |
| কতগুলো observation?         | Countplot       |
| Category frequency?         | Countplot       |
| Category + category         | Countplot + hue |
| Category-এর average value?  | Barplot         |
| Category-এর median value?   | Barplot         |
| Category-এর total value?    | Barplot + sum   |
| Distribution shape?         | Violinplot      |
| Outlier?                    | Boxplot         |
| Numerical distribution?     | Histogram       |
| Two numerical relationship? | Scatterplot     |

---

# 45. Countplot Mental Model

সবসময় এই pattern মনে রাখো:

```text
Categorical Column
       ↓
 Count / Frequency
       ↓
   Countplot
```

Example:

```python
sns.countplot(
    data=df,
    x="day"
)
```

---

# 46. Barplot Mental Model

```text
Categorical Column
       +
Numerical Column
       ↓
   Aggregation
       ↓
    Barplot
```

Example:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

---

# 47. EDA Decision Tree

একটি নতুন column দেখলে নিজেকে প্রশ্ন করো:

```text
Column
  │
  ├── Categorical?
  │      │
  │      ├── শুধু count জানতে চাই?
  │      │       ↓
  │      │   Countplot
  │      │
  │      └── Numerical value compare?
  │              ↓
  │           Barplot
  │
  └── Numerical?
         │
         ├── Distribution?
         │      ↓
         │   Histogram
         │
         └── Category অনুযায়ী distribution?
                ↓
             Boxplot / Violinplot
```

---

# 48. Complete M06 Example

```python
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np

# Load dataset
df = sns.load_dataset("tips")

# -------------------------
# 1. Customer count by day
# -------------------------

sns.countplot(
    data=df,
    x="day"
)

plt.title("Customer Count by Day")
plt.xlabel("Day")
plt.ylabel("Number of Customers")

plt.show()


# -------------------------
# 2. Average bill by day
# -------------------------

sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar=None
)

plt.title("Average Bill by Day")
plt.xlabel("Day")
plt.ylabel("Average Total Bill")

plt.show()


# -------------------------
# 3. Average bill by day + sex
# -------------------------

sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    estimator=np.mean,
    errorbar=None
)

plt.title("Average Bill by Day and Sex")
plt.show()


# -------------------------
# 4. Customer count by day + sex
# -------------------------

sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.title("Customer Count by Day and Sex")
plt.show()
```

---

# 49. M06 Practice — Beginner 🟢

### Task 1

`tips` dataset-এ:

```text
day
```

এর countplot বানাও।

### Task 2

```text
sex
```

এর countplot বানাও।

### Task 3

```text
smoker
```

এর countplot বানাও।

### Task 4

`day + sex` দিয়ে countplot বানাও।

### Task 5

`time` column-এর countplot বানাও।

---

# 50. M06 Practice — Intermediate 🟡

### Task 6

প্রতিটি day-এর average `tip` বের করো:

```python
sns.barplot(
    data=df,
    x="day",
    y="tip"
)
```

### Task 7

Day-wise median `total_bill`:

```python
estimator=np.median
```

ব্যবহার করো।

### Task 8

Day-wise total bill:

```python
estimator="sum"
```

ব্যবহার করো।

### Task 9

`day + sex + total_bill` দিয়ে barplot বানাও।

### Task 10

Error bar বন্ধ করে plot তৈরি করো:

```python
errorbar=None
```

---

# 51. M06 Practice — Advanced 🔴

নিজের dataset ব্যবহার করে:

### Task 11 — Class Distribution

```text
Class
```

এর countplot বানাও।

তারপর বের করো:

```text
Count
Percentage
```

---

### Task 12 — Group Analysis

একটি categorical এবং numerical feature নিয়ে:

```text
Category
   ↓
Average Feature
```

barplot তৈরি করো।

---

### Task 13 — Count vs Average

একই category-এর জন্য:

```text
Countplot
+
Barplot
```

তৈরি করো।

তারপর লিখো:

> কোন category-তে sample বেশি?

এবং:

> কোন category-তে average value বেশি?

---

### Task 14 — ML EDA

একটি classification dataset নিয়ে:

```text
Class
Feature
```

দিয়ে:

```python
sns.countplot(...)
```

এবং

```python
sns.barplot(...)
```

ব্যবহার করো।

তারপর analysis লিখো:

```text
1. Class balance
2. Sample count
3. Feature average
4. Difference between classes
5. Possible data imbalance
```

---

# 52. M06-এর সবচেয়ে গুরুত্বপূর্ণ 10টি Code

### 1. Basic Countplot

```python
sns.countplot(data=df, x="day")
```

### 2. Horizontal Countplot

```python
sns.countplot(data=df, y="day")
```

### 3. Countplot + hue

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)
```

### 4. Basic Barplot

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

### 5. Median

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator=np.median
)
```

### 6. Sum

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="sum"
)
```

### 7. Barplot + hue

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)
```

### 8. No error bar

```python
errorbar=None
```

### 9. Custom order

```python
order=["Sun", "Sat", "Fri", "Thur"]
```

### 10. Pandas + Seaborn

```python
result = (
    df.groupby("day")["total_bill"]
    .mean()
    .reset_index()
)

sns.barplot(
    data=result,
    x="day",
    y="total_bill"
)
```

---

# 53. M06 Completion Checklist ✅

M06 শেষ করার পর তোমার এগুলো পরিষ্কার হওয়া উচিত:

* [ ] Categorical data কী
* [ ] Countplot কী
* [ ] Barplot কী
* [ ] Countplot বনাম Barplot
* [ ] `x`
* [ ] `y`
* [ ] `hue`
* [ ] `order`
* [ ] `hue_order`
* [ ] `value_counts()`
* [ ] `estimator`
* [ ] Mean
* [ ] Median
* [ ] Sum
* [ ] `errorbar`
* [ ] Confidence interval-এর basic ধারণা
* [ ] Count + percentage analysis
* [ ] Pandas `groupby()` + Seaborn
* [ ] Class imbalance visualization
* [ ] ML dataset-এর categorical EDA

---

## 🧠 M06-এর Core Concept

শেষে শুধু এই mental model-টা মনে রাখো:

```text
                 CATEGORICAL DATA
                       │
             ┌─────────┴─────────┐
             │                   │
       COUNT জানতে চাই?     VALUE compare?
             │                   │
             ↓                   ↓
        COUNTplot             BARplot
             │                   │
       Frequency             Aggregation
                               │
                     ┌─────────┼─────────┐
                     ↓         ↓         ↓
                    Mean     Median      Sum
```

আর M04–M06 একসাথে মনে রাখলে:

```text
Boxplot
   ↓
Median + Quartile + Outlier

Violinplot
   ↓
Distribution + Density

Countplot
   ↓
Category Frequency

Barplot
   ↓
Category-wise Numerical Summary
```

এগুলো ভালোভাবে আয়ত্ত করলে Seaborn-এর **categorical EDA foundation** শক্ত হয়ে যাবে। পরের ধাপে `Stripplot & Swarmplot` শিখলে individual observations-ও category-এর ভেতরে কীভাবে ছড়িয়ে আছে সেটা দেখা যাবে।

----
# Seaborn M07 — Stripplot & Swarmplot Deep Dive 🎯📊

M04-এ শিখেছি **Boxplot**, M05-এ **Violinplot**, আর M06-এ **Countplot & Barplot**।

এখন M07-এ শিখব:

* `stripplot()`
* `swarmplot()`
* Individual observations
* Jitter
* `hue`
* `dodge`
* `size`
* `alpha`
* `order`
* Violin + Stripplot
* Violin + Swarmplot
* Boxplot + Swarmplot
* Overplotting
* কোন পরিস্থিতিতে কোনটা ব্যবহার করব
* ML/EDA-তে practical use

---

# 1. Stripplot কী?

**Stripplot** হলো এমন একটি categorical plot যেখানে প্রতিটি individual observation-এর জন্য একটি point দেখানো হয়।

ধরো:

```text
Day       Total Bill

Thur       •
           •
          ••
           •
          •••

Fri        •
           ••
            •

Sat       •••
         ••••
          ••
```

এখানে প্রতিটি `•` একটি **actual data point**।

---

# 2. কেন Stripplot দরকার?

আগের plot-গুলো:

### Countplot

```text
কতগুলো observation?
```

### Barplot

```text
Average / aggregated value কত?
```

### Boxplot

```text
Median + quartile + outlier
```

### Violinplot

```text
Distribution shape + density
```

কিন্তু প্রশ্ন যদি হয়:

> **প্রতিটি individual data point কোথায় আছে?**

তাহলে:

```text
Stripplot
```

---

# 3. Basic Stripplot

প্রথমে dataset:

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")
```

তারপর:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এখানে প্রতিটি bill একটি point।

---

# 4. Stripplot কী দেখাচ্ছে?

ধরো:

```text
day = Thur
total_bill:

10
12
15
18
20
25
```

Stripplot:

```text
Thur

25       •
20       •
18       •
15       •
12       •
10       •
```

অর্থাৎ raw observations দেখতে পাচ্ছি।

---

# 5. Problem: Overlapping Points

যদি একই বা কাছাকাছি value অনেকবার থাকে:

```text
      •
      •
      •
      •
      •
```

সব point এক জায়গায় overlap করতে পারে।

তখন বুঝতে সমস্যা হয় কতগুলো observation আছে।

এই problem-এর solution:

```text
jitter
```

---

# 6. `jitter`

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True
)

plt.show()
```

Jitter point-গুলোকে সামান্য horizontal direction-এ ছড়িয়ে দেয়।

```text
Without jitter:

     •
     •
     •
     •


With jitter:

   • •
    •
  •   •
    • •
```

Important:

> Jitter actual numerical value পরিবর্তন করে না; শুধু visualization-এর জন্য point-এর display position সামান্য সরায়।

---

# 7. Jitter-এর value control

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=0.2
)

plt.show()
```

আরও spread:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=0.4
)

plt.show()
```

সাধারণভাবে:

```text
jitter ছোট
→ points কম ছড়াবে

jitter বড়
→ points বেশি ছড়াবে
```

---

# 8. Horizontal Stripplot

```python
sns.stripplot(
    data=df,
    x="total_bill",
    y="day"
)

plt.show()
```

এখানে:

```text
x → numerical
y → categorical
```

---

# 9. `hue`

ধরো:

> প্রতিটি day-তে Male এবং Female customer-এর bill distribution কেমন?

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    jitter=True
)

plt.show()
```

এখন একই category-এর মধ্যে দুই ধরনের observation দেখতে পারবে।

---

# 10. `dodge`

`hue` ব্যবহার করলে category-গুলোকে আলাদা করে দেখাতে `dodge` ব্যবহার করা যায়।

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    dodge=True,
    jitter=True
)

plt.show()
```

Concept:

```text
          Thur
       Male | Female
         •      •
        ••     ••
         •      •

          Fri
       Male | Female
         •      •
```

এতে comparison সহজ হয়।

---

# 11. `size`

Point-এর size পরিবর্তন করা যায়।

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    size=6,
    jitter=True
)

plt.show()
```

ছোট:

```python
size=3
```

বড়:

```python
size=8
```

---

# 12. `alpha`

অনেক point থাকলে transparency ব্যবহার করা যায়।

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    alpha=0.5,
    jitter=True
)

plt.show()
```

`alpha` সাধারণত:

```text
0 → invisible
1 → fully opaque
```

অনেক data point থাকলে overlap বোঝার জন্য transparency useful।

---

# 13. `order`

Category-এর order পরিবর্তন:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    order=["Sun", "Sat", "Fri", "Thur"],
    jitter=True
)

plt.show()
```

---

# 14. `hue_order`

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    hue_order=["Female", "Male"],
    dodge=True,
    jitter=True
)

plt.show()
```

---

# 15. Stripplot + Boxplot

এটি অত্যন্ত useful combination।

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    color="black",
    jitter=True,
    alpha=0.5
)

plt.show()
```

এখানে:

```text
Boxplot
   ↓
Summary statistics

Stripplot
   ↓
Individual observations
```

---

# 16. কেন এই combination powerful?

শুধু Boxplot:

```text
Median
Q1
Q3
Whisker
Outlier
```

কিন্তু individual data দেখতে পাচ্ছি না।

শুধু Stripplot:

```text
সব observation
```

কিন্তু median/Q1/Q3 সহজে দেখা যায় না।

দুটো একসাথে:

```text
Boxplot + Raw Data
```

EDA-তে খুব powerful।

---

# 17. Violinplot + Stripplot

আরও powerful combination:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True,
    alpha=0.5
)

plt.show()
```

এখানে:

```text
Violin
 ↓
Density

Strip
 ↓
Actual observations
```

---

# 18. Violin + Box + Strip

তিনটি একসাথে ব্যবহার করা যায়:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner="box"
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True,
    alpha=0.4
)

plt.show()
```

এখানে আমরা দেখতে পাচ্ছি:

```text
Distribution
+
Median/Quartiles
+
Individual observations
```

---

# 19. Swarmplot কী?

এখন আসি **Swarmplot**-এ।

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Swarmplot-ও individual points দেখায়।

কিন্তু Stripplot-এর মতো random jitter নয়।

Swarmplot চেষ্টা করে:

> Point-গুলোকে এমনভাবে position করতে যাতে তারা একে অপরের উপর overlap না করে।

---

# 20. Stripplot vs Swarmplot

ধরো অনেক point:

### Stripplot

```text
     •
    ••
     •
   •••
    •
```

Jitter-এর কারণে point ছড়িয়ে যায়।

### Swarmplot

```text
      •
     • •
    •   •
   •     •
```

Points collision avoid করার চেষ্টা করে।

---

# 21. Basic Swarmplot

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

---

# 22. Swarmplot + Hue

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

---

# 23. Swarmplot + Dodge

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    dodge=True
)

plt.show()
```

এতে Male/Female observations আলাদা position-এ থাকবে।

---

# 24. Swarmplot + Violinplot

এটি খুব popular EDA combination:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.show()
```

Interpretation:

```text
Violin
  ↓
Where data is dense

Swarm
  ↓
Where actual observations are
```

---

# 25. Swarmplot + Boxplot

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.show()
```

এখানে:

```text
Box
 ↓
Summary

Swarm
 ↓
Individual points
```

---

# 26. Stripplot vs Swarmplot

| বিষয়                       | Stripplot | Swarmplot                      |
| -------------------------- | --------- | ------------------------------ |
| Individual points          | ✅         | ✅                              |
| Jitter                     | ✅         | Automatic positioning          |
| Overlap control            | Basic     | Better                         |
| Large dataset              | Better    | Can become expensive/cluttered |
| Exact point visualization  | ✅         | ✅                              |
| Distribution understanding | ⭐⭐        | ⭐⭐⭐                            |
| Speed                      | Faster    | তুলনামূলক ধীর                  |
| Small/medium dataset       | ✅         | Excellent                      |

---

# 27. কখন Stripplot ব্যবহার করব?

Stripplot ভালো যখন:

* Dataset ছোট/মাঝারি
* অনেক category নেই
* Individual observations দেখতে চাই
* Jitter দরকার
* দ্রুত plot করতে চাই

Example:

```python
sns.stripplot(
    data=df,
    x="day",
    y="tip",
    jitter=True
)
```

---

# 28. কখন Swarmplot ব্যবহার করব?

Swarmplot ভালো যখন:

* Dataset ছোট বা medium
* Individual points clearly দেখতে চাই
* Overlap minimize করতে চাই
* Category-wise distribution visually compare করতে চাই

Example:

```python
sns.swarmplot(
    data=df,
    x="day",
    y="tip"
)
```

---

# 29. Large Dataset-এর সমস্যা

ধরো:

```text
10,000 points
```

Swarmplot সব points সুন্দরভাবে arrange করতে গেলে:

* Slow হতে পারে
* Plot cluttered হতে পারে
* Visualization unreadable হতে পারে

তখন:

```text
Histogram
Boxplot
Violinplot
KDE
```

এর মতো aggregated/distribution plots বেশি useful হতে পারে।

---

# 30. Categorical + Numerical Relationship

Stripplot-এর মূল pattern:

```text
Categorical
     +
Numerical
     ↓
Individual observations
```

Example:

```python
sns.stripplot(
    data=df,
    x="day",
    y="tip"
)
```

এখানে:

```text
day → categorical
tip → numerical
```

---

# 31. `size` দিয়ে Observation Emphasis

ধরো point ছোট:

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=2
)

plt.show()
```

বড়:

```python
size=5
```

তবে খুব বড় size ব্যবহার করলে overlap/clutter বাড়তে পারে।

---

# 32. Practical EDA Example

ধরো প্রশ্ন:

> কোন day-তে customer spending বেশি spread করে?

প্রথমে:

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.title("Total Bill Distribution by Day")
plt.show()
```

এখানে তুমি দেখতে পারবে:

* Density
* Individual points
* Concentration
* Possible outliers
* Category differences

---

# 33. Gender Comparison

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    dodge=True,
    jitter=True,
    alpha=0.5
)

plt.show()
```

তবে একই plot-এ violin এবং strip উভয়েই `hue` দিলে legend duplicate হতে পারে। বাস্তবে legend cleanup করা ভালো।

---

# 34. Better Combined Visualization

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    color="black",
    jitter=True,
    alpha=0.4
)

plt.title("Distribution + Individual Observations")
plt.show()
```

এটি conceptually cleaner।

---

# 35. ML Dataset-এ ব্যবহার

ধরো তোমার classification dataset:

```text
class
feature_1
```

যেখানে:

```text
Normal
Suspicious
```

তাহলে:

```python
sns.stripplot(
    data=df,
    x="class",
    y="feature_1",
    jitter=True,
    alpha=0.5
)

plt.show()
```

এতে তুমি দেখতে পারবে:

```text
Normal
  •
 • •
  •

Suspicious
   •
 • ••
   •
```

দুই class-এর individual feature values কতটা overlap করছে সেটা বোঝা যায়।

---

# 36. Feature Separation

ধরো:

```text
Normal:

10 12 13 14 15

Suspicious:

25 27 29 30 32
```

Plot করলে দুই class আলাদা:

```text
Normal          Suspicious

 •                  •
 •                  •
 •                  •
 •                  •
```

এখানে featureটি potentially useful হতে পারে।

কিন্তু:

```text
Normal:

10 15 20 25

Suspicious:

18 20 22 25
```

তাহলে অনেক overlap।

```text
Normal       Suspicious

 •               •
      •       •
          •
        •
```

Feature separation কম।

**তবে visualization alone দিয়ে feature quality নিশ্চিত করা যাবে না।**

---

# 37. Class Imbalance + Individual Data

ধরো:

```text
Normal       → 9000
Suspicious   → 1000
```

Countplot:

```python
sns.countplot(
    data=df,
    x="class"
)

plt.show()
```

তারপর feature distribution:

```python
sns.violinplot(
    data=df,
    x="class",
    y="feature"
)

plt.show()
```

তারপর individual observations:

```python
sns.stripplot(
    data=df.sample(1000),
    x="class",
    y="feature",
    jitter=True,
    alpha=0.4
)

plt.show()
```

Large dataset হলে sample নেওয়া visualization-এর জন্য useful হতে পারে।

---

# 38. M04 → M07 Connection

এখন চারটি plot একসাথে বুঝি:

```text
M04
BOXPLOT
    ↓
Summary + Outlier


M05
VIOLINPLOT
    ↓
Distribution + Density


M06
COUNTPLOT
    ↓
Frequency


M06
BARPLOT
    ↓
Aggregated Numerical Value


M07
STRIPPLOT
    ↓
Individual Observations


M07
SWARMPLOT
    ↓
Individual Observations
+ Better Collision Avoidance
```

---

# 39. EDA Workflow

একটি নতুন dataset পেলে:

```text
Dataset
   ↓
Categorical Distribution
   ↓
Countplot
   ↓
Numerical Distribution
   ↓
Histogram
   ↓
Category-wise Distribution
   ↓
Boxplot / Violinplot
   ↓
Individual Observations
   ↓
Stripplot / Swarmplot
```

---

# 40. Complete M07 Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Load dataset
df = sns.load_dataset("tips")


# -------------------------
# 1. Basic Stripplot
# -------------------------

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True
)

plt.title("Stripplot")
plt.show()


# -------------------------
# 2. Swarmplot
# -------------------------

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.title("Swarmplot")
plt.show()


# -------------------------
# 3. Violin + Strip
# -------------------------

sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True,
    alpha=0.5
)

plt.title("Violin + Stripplot")
plt.show()


# -------------------------
# 4. Box + Swarm
# -------------------------

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)

plt.title("Boxplot + Swarmplot")
plt.show()
```

---

# 41. M07 Cheat Sheet

### Basic Stripplot

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill"
)
```

### Jitter

```python
jitter=True
```

### Custom Jitter

```python
jitter=0.2
```

### Hue

```python
hue="sex"
```

### Dodge

```python
dodge=True
```

### Point size

```python
size=5
```

### Transparency

```python
alpha=0.5
```

### Swarmplot

```python
sns.swarmplot(
    data=df,
    x="day",
    y="total_bill"
)
```

### Violin + Strip

```python
sns.violinplot(
    data=df,
    x="day",
    y="total_bill",
    inner=None
)

sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    jitter=True
)
```

### Box + Swarm

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.swarmplot(
    data=df,
    x="day",
    y="total_bill",
    size=3
)
```

---

# 42. Practice — Beginner 🟢

### Task 1

`day` এবং `total_bill` দিয়ে basic Stripplot বানাও।

### Task 2

`jitter=True` ব্যবহার করো।

### Task 3

Horizontal Stripplot বানাও।

### Task 4

`sex` দিয়ে `hue` যোগ করো।

### Task 5

`size=5` এবং `alpha=0.5` ব্যবহার করো।

---

# 43. Practice — Intermediate 🟡

### Task 6

`day + total_bill` দিয়ে Swarmplot বানাও।

### Task 7

`day + sex + total_bill` দিয়ে Swarmplot বানাও।

### Task 8

`dodge=True` ব্যবহার করো।

### Task 9

তৈরি করো:

```text
Violinplot + Stripplot
```

### Task 10

তৈরি করো:

```text
Boxplot + Swarmplot
```

---

# 44. Practice — Advanced 🔴

নিজের ML dataset নিয়ে:

### Task 11

একটি categorical column এবং numerical feature নির্বাচন করো।

```text
Category
   +
Feature
```

তারপর:

```python
sns.stripplot(...)
```

ব্যবহার করো।

### Task 12

একই data দিয়ে:

```text
Boxplot
+
Stripplot
```

compare করো।

### Task 13

তারপর:

```text
Violinplot
+
Swarmplot
```

তৈরি করো।

### Task 14

দেখো:

* কোথায় data concentrated?
* কোথায় overlap?
* কোন category-তে variation বেশি?
* কোনো extreme observation আছে?
* দুই class-এর separation কেমন?

---

# 45. M07 Completion Checklist ✅

* [ ] Stripplot কী
* [ ] Swarmplot কী
* [ ] Individual observation কী
* [ ] `jitter`
* [ ] `hue`
* [ ] `dodge`
* [ ] `size`
* [ ] `alpha`
* [ ] `order`
* [ ] `hue_order`
* [ ] Stripplot vs Swarmplot
* [ ] Overplotting
* [ ] Boxplot + Stripplot
* [ ] Boxplot + Swarmplot
* [ ] Violinplot + Stripplot
* [ ] Violinplot + Swarmplot
* [ ] ML class-wise feature analysis
* [ ] Feature overlap বোঝা
* [ ] Individual observations interpret করা

---

# 🧠 M07-এর Core Mental Model

```text
                 CATEGORICAL + NUMERICAL
                          │
              ┌───────────┴───────────┐
              │                       │
        Distribution              Raw Points
              │                       │
       ┌──────┴──────┐          ┌─────┴─────┐
       │             │          │           │
   Boxplot       Violinplot  Stripplot   Swarmplot
       │             │          │           │
 Summary +       Density +    Individual   Individual
 Outlier         Distribution  Points       Points
```

সবচেয়ে গুরুত্বপূর্ণ:

> **Countplot বলে কতগুলো data আছে।**
> **Barplot বলে category-wise summary কত।**
> **Boxplot বলে data-এর summary ও outlier কোথায়।**
> **Violinplot বলে distribution-এর shape কেমন।**
> **Stripplot/Swarmplot বলে actual individual observations কোথায় আছে।**

**M07 complete হলে Seaborn-এর categorical visualization foundation অনেকটাই শক্ত হবে।** পরের ধাপে **M08 — `Heatmap & Correlation Analysis Deep Dive`** শেখা সবচেয়ে logical, কারণ সেখানে numerical features-এর relationship এবং ML feature analysis-এর দিকে যাওয়া শুরু হবে।


----
# Seaborn M08 — Heatmap & Correlation Analysis Deep Dive 🔥📊

M07 পর্যন্ত আমরা mainly **categorical data + individual observations** নিয়ে কাজ করেছি।

এখন M08-এ আমরা numerical features-এর মধ্যে **relationship** খুঁজব।

এই lesson-এর সবচেয়ে গুরুত্বপূর্ণ দুইটি concept:

```text
Correlation
    ↓
দুইটি numerical variable কতটা related?

Heatmap
    ↓
অনেকগুলো correlation একসাথে visualভাবে দেখা
```

এটি **EDA এবং Machine Learning**-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 1. Correlation কী?

ধরো dataset-এ:

```text
Hours Studied    Exam Score
       1              40
       2              45
       3              52
       4              60
       5              70
```

Hours বাড়ার সাথে Score-ও বাড়ছে।

এখানে positive relationship আছে।

```text
Hours ↑
   ↓
Score ↑
```

এটাই correlation-এর basic idea।

---

# 2. Correlation-এর Range

সাধারণ Pearson correlation:

```text
-1 ≤ r ≤ +1
```

অর্থাৎ:

```text
-1       0       +1
│────────│────────│
```

### `+1`

Perfect positive correlation:

```text
X ↑
Y ↑
```

### `0`

Linear relationship নেই বা খুব কম:

```text
X ↗
Y ↘/random
```

### `-1`

Perfect negative correlation:

```text
X ↑
Y ↓
```

---

# 3. Positive Correlation

Example:

```text
Hours Studied ↑
Exam Score   ↑
```

Correlation:

```text
r = +0.90
```

এটি strong positive relationship।

---

# 4. Negative Correlation

ধরো:

```text
Speed ↑
Travel Time ↓
```

তাহলে:

```text
r = -0.85
```

এটি strong negative relationship।

---

# 5. Correlation Strength

একটি practical guideline:

| `|r|` | সাধারণ interpretation |
|---:|---|
| 0.00–0.19 | Very weak |
| 0.20–0.39 | Weak |
| 0.40–0.59 | Moderate |
| 0.60–0.79 | Strong |
| 0.80–1.00 | Very strong |

এগুলো **strict universal boundaries নয়**। Domain অনুযায়ী interpretation পরিবর্তন হতে পারে।

---

# 6. Correlation আর Causation এক নয় ⚠️

এটি খুব গুরুত্বপূর্ণ।

যদি:

```text
Ice Cream Sales ↑
Swimming Incidents ↑
```

দুটির correlation থাকতে পারে।

কিন্তু এর মানে এই নয়:

> Ice cream খাওয়ার কারণে swimming incident হচ্ছে।

তৃতীয় variable যেমন:

```text
Hot Weather
```

দুটোকেই influence করতে পারে।

তাই:

```text
Correlation ≠ Causation
```

---

# 7. `tips` Dataset দিয়ে শুরু করি

```python id="4wuw4c"
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

Numerical columns:

```text
total_bill
tip
size
```

---

# 8. Correlation Matrix

Pandas দিয়ে:

```python id="x0e5me"
corr = df.corr(numeric_only=True)

print(corr)
```

Conceptual output:

```text
             total_bill    tip    size
total_bill      1.00      ...     ...
tip              ...      1.00    ...
size             ...       ...    1.00
```

এটাই **correlation matrix**।

---

# 9. কেন Matrix দরকার?

ধরো আমাদের 5টি feature:

```text
A
B
C
D
E
```

তাহলে আমাদের অনেক pair relationship আছে:

```text
A-B
A-C
A-D
A-E
B-C
B-D
...
```

সব numerical value table-এ দেখা কঠিন।

Heatmap এগুলো visual করে।

---

# 10. Basic Heatmap

```python id="7g2dai"
corr = df.corr(numeric_only=True)

sns.heatmap(corr)

plt.show()
```

এটাই basic correlation heatmap।

---

# 11. Heatmap কীভাবে Read করব?

ধরো:

```text
       A      B      C
A    1.00   0.80  -0.20
B    0.80   1.00  -0.50
C   -0.20  -0.50   1.00
```

Heatmap-এ:

```text
A ↔ B
0.80
```

মানে strong positive relationship।

আর:

```text
B ↔ C
-0.50
```

মানে moderate negative relationship।

---

# 12. `annot=True`

শুধু color দেখে exact value বোঝা কঠিন হতে পারে।

তাই:

```python id="5nxyza"
sns.heatmap(
    corr,
    annot=True
)

plt.show()
```

এখন প্রতিটি cell-এর মধ্যে correlation value দেখা যাবে।

যেমন:

```text
1.00
0.75
-0.42
```

---

# 13. `fmt`

Decimal places control করতে:

```python id="h6l1ro"
sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

`.2f`:

```text
0.812345
```

কে:

```text
0.81
```

দেখাবে।

---

# 14. `cmap`

Heatmap-এর color palette পরিবর্তন করা যায়।

```python id="8eyzqh"
sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm"
)

plt.show()
```

Correlation-এর ক্ষেত্রে diverging palette useful, কারণ:

```text
Negative ← 0 → Positive
```

---

# 15. `center=0`

Correlation heatmap-এর জন্য zero-centered visualization useful:

```python id="7m4r4m"
sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm",
    center=0
)

plt.show()
```

এখানে:

```text
Negative
    ↓
   0
    ↓
Positive
```

---

# 16. `vmin` এবং `vmax`

Correlation-এর range সাধারণত:

```text
-1 → +1
```

তাই explicitly set করতে পারি:

```python id="o7v7ct"
sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

এটি correlation heatmap-কে visually consistent করতে সাহায্য করে।

---

# 17. Figure Size

Feature অনেক হলে বড় figure দরকার।

```python id="tq8d3n"
plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

---

# 18. Square Heatmap

Correlation matrix সাধারণত square।

তাই:

```python id="7hh55e"
sns.heatmap(
    corr,
    annot=True,
    square=True
)

plt.show()
```

এতে cells square রাখা হয়।

---

# 19. `linewidths`

Cell-এর মধ্যে separation:

```python id="1a1j0c"
sns.heatmap(
    corr,
    annot=True,
    linewidths=0.5
)

plt.show()
```

---

# 20. `linecolor`

Cell boundary-এর color control করা যায়:

```python id="gh8w4y"
sns.heatmap(
    corr,
    annot=True,
    linewidths=0.5,
    linecolor="white"
)

plt.show()
```

---

# 21. Heatmap-এর Anatomy

একটি heatmap:

```text
          Feature A  Feature B  Feature C
Feature A    1.00       0.75       -0.20
Feature B    0.75       1.00       -0.55
Feature C   -0.20      -0.55        1.00
```

এখানে:

* Rows → variables
* Columns → variables
* Cell → correlation
* Color → strength/direction
* Number → exact correlation

---

# 22. Diagonal সবসময় কেন `1`?

Correlation:

```text
A with A
```

অর্থাৎ একটি variable নিজের সাথেই compare হচ্ছে।

তাই:

```text
corr(A, A) = 1
```

Matrix-এর diagonal:

```text
A-A = 1
B-B = 1
C-C = 1
```

হবে।

---

# 23. Matrix Symmetric কেন?

যদি:

```text
corr(A, B) = 0.80
```

তাহলে:

```text
corr(B, A) = 0.80
```

তাই:

```text
       A      B
A     1     .80
B    .80     1
```

উপরের এবং নিচের triangle একই।

---

# 24. শুধু Lower Triangle দেখানো

Duplicate information remove করতে mask ব্যবহার করা যায়।

```python id="yqj91n"
import numpy as np

mask = np.triu(np.ones_like(corr, dtype=bool))

sns.heatmap(
    corr,
    annot=True,
    mask=mask,
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

এখানে upper triangle hide হবে।

---

# 25. Mask কী করছে?

```python id="xlj3uw"
mask = np.triu(
    np.ones_like(corr, dtype=bool)
)
```

Conceptually:

```text
Original:

1   .8  .2
.8  1   .5
.2  .5  1


After mask:

X   X   X
.8  X   X
.2  .5  X
```

শুধু lower triangle দেখা যায়।

---

# 26. `annot` + `fmt` + `mask`

একটি professional correlation heatmap:

```python id="y6ek2k"
corr = df.corr(numeric_only=True)

mask = np.triu(
    np.ones_like(corr, dtype=bool)
)

plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    mask=mask,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1,
    square=True
)

plt.title("Correlation Matrix")

plt.show()
```

এটি real EDA-তে খুব common pattern।

---

# 27. Strong Correlation খুঁজে বের করা

Heatmap দেখার পাশাপাশি numericalভাবে বের করতে পারি।

```python id="b1n6o5"
corr = df.corr(numeric_only=True)

print(corr)
```

তারপর:

```python id="i5d5gd"
print(
    corr["total_bill"].sort_values(
        ascending=False
    )
)
```

এতে `total_bill`-এর সাথে অন্য numerical variables-এর correlation দেখতে পারবে।

---

# 28. Positive Correlation Filter

ধরো:

```python id="j6q4tj"
strong_positive = corr[
    corr > 0.7
]

print(strong_positive)
```

কিন্তু এতে diagonal-সহ অনেক `NaN` থাকবে।

Pairwise analysis-এর জন্য matrix format ব্যবহার করতে হবে।

---

# 29. Feature Pair বের করা

Correlation matrix থেকে pair বের করার একটি practical approach:

```python id="u3o0j5"
corr_pairs = corr.unstack()

print(corr_pairs.sort_values(
    ascending=False
))
```

এতে:

```text
A-A
B-B
A-B
B-A
...
```

আসবে।

Diagonal বাদ দিতে পারি।

---

# 30. Diagonal বাদ দেওয়া

```python id="fbd6ez"
corr_pairs = corr.where(
    ~np.eye(corr.shape[0], dtype=bool)
)

corr_pairs = corr_pairs.unstack()

print(
    corr_pairs.sort_values(
        ascending=False
    )
)
```

এখন self-correlation বাদ যাবে।

---

# 31. Duplicate Pair বাদ দেওয়া

আরও clean approach:

```python id="snhbyr"
upper = corr.where(
    np.triu(
        np.ones(corr.shape),
        k=1
    ).astype(bool)
)

pairs = (
    upper
    .stack()
    .sort_values(ascending=False)
)

print(pairs)
```

এতে unique feature pairs পাওয়া যায়।

---

# 32. Multicollinearity

Machine Learning-এ correlation-এর আরেকটি গুরুত্বপূর্ণ ব্যবহার:

> **Multicollinearity**

ধরো:

```text
age
age_in_months
```

দুটো প্রায় একই information দেয়।

Correlation:

```text
r ≈ 1
```

হতে পারে।

আর:

```text
feature_A
feature_B
```

যদি:

```text
r = 0.95
```

তাহলে তারা highly correlated।

কিছু ML model-এর ক্ষেত্রে redundant features সমস্যা তৈরি করতে পারে।

---

# 33. Feature Selection

ধরো:

```text
Feature A ↔ Target = 0.85
Feature B ↔ Target = 0.10
Feature C ↔ Target = -0.75
```

Initial EDA-তে আমরা ভাবতে পারি:

```text
A → potentially useful
C → potentially useful
B → weak linear relationship
```

কিন্তু:

**Low correlation মানেই useless feature নয়।**

কারণ relationship nonlinear হতে পারে।

---

# 34. Correlation এবং Nonlinear Relationship

ধরো:

```text
Y = X²
```

এখানে X এবং Y-এর মধ্যে strong relationship আছে।

কিন্তু Pearson correlation সবসময় এটিকে strong linear correlation হিসেবে ধরবে না।

অর্থাৎ:

```text
Correlation
    ↓
Linear relationship-এর measure
```

বিশেষ করে Pearson-এর ক্ষেত্রে।

---

# 35. Pearson Correlation

Pandas-এর:

```python id="p7q0m1"
df.corr(numeric_only=True)
```

defaultভাবে Pearson correlation দেয়।

Pearson মূলত linear relationship measure করে।

---

# 36. Spearman Correlation

Rank-based monotonic relationship দেখতে:

```python id="rb4gh5"
corr_spearman = df.corr(
    numeric_only=True,
    method="spearman"
)

print(corr_spearman)
```

Spearman useful যখন:

* relationship monotonic
* data non-normal হতে পারে
* outlier concern আছে
* exact linearity না থাকলেও ordered relationship আছে

---

# 37. Pearson vs Spearman

| বিষয়                   | Pearson       | Spearman     |
| ---------------------- | ------------- | ------------ |
| Linear relationship    | Excellent     | Good         |
| Monotonic relationship | Yes           | Excellent    |
| Rank-based             | ❌             | ✅            |
| Outlier sensitivity    | বেশি          | তুলনামূলক কম |
| Normality assumptions  | বেশি relevant | কম           |
| Common EDA             | খুব common    | খুব useful   |

---

# 38. Correlation Matrix — Pearson

```python id="9gk1az"
pearson_corr = df.corr(
    numeric_only=True,
    method="pearson"
)

sns.heatmap(
    pearson_corr,
    annot=True,
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

---

# 39. Correlation Matrix — Spearman

```python id="3kmqv7"
spearman_corr = df.corr(
    numeric_only=True,
    method="spearman"
)

sns.heatmap(
    spearman_corr,
    annot=True,
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

দুটো compare করলে relationship সম্পর্কে আরও ভালো ধারণা পাওয়া যায়।

---

# 40. Heatmap শুধু Correlation-এর জন্য নয়

Heatmap আরও অনেক matrix visualize করতে পারে।

যেমন:

```python id="7n9m0c"
data = [
    [10, 20, 30],
    [15, 25, 35],
    [12, 22, 40]
]

sns.heatmap(
    data,
    annot=True
)

plt.show()
```

অর্থাৎ:

```text
Heatmap
    ↓
Any matrix-like numerical data
```

তবে EDA-তে correlation heatmap সবচেয়ে common use case-এর একটি।

---

# 41. Pivot Table + Heatmap

এটি খুব important Seaborn pattern।

ধরো:

```python id="jy7lq6"
pivot = df.pivot_table(
    values="total_bill",
    index="day",
    columns="sex",
    aggfunc="mean"
)

print(pivot)
```

তারপর:

```python id="p6c5n2"
sns.heatmap(
    pivot,
    annot=True,
    fmt=".2f"
)

plt.show()
```

এখানে:

```text
Rows → day
Columns → sex
Values → average total_bill
```

---

# 42. Pivot Heatmap কেন Useful?

ধরো:

```text
             Male   Female
Thur          19      17
Fri           21      16
Sat           23      18
Sun           22      20
```

Heatmap এক নজরে দেখাবে:

> কোন day + gender combination-এর average bill বেশি/কম।

---

# 43. Real Business Example

E-commerce data:

```text
category
month
sales
```

Pivot:

```python id="7r9e4n"
pivot = df.pivot_table(
    values="sales",
    index="month",
    columns="category",
    aggfunc="sum"
)
```

Heatmap:

```python id="nkn4iy"
sns.heatmap(
    pivot,
    annot=True,
    fmt=".0f"
)

plt.show()
```

এতে:

```text
Month × Category
```

এর sales pattern দেখা যাবে।

---

# 44. ML Dataset Example

ধরো features:

```text
age
income
credit_score
loan_amount
debt
```

Correlation:

```python id="82y6hx"
corr = df[
    [
        "age",
        "income",
        "credit_score",
        "loan_amount",
        "debt"
    ]
].corr()
```

Heatmap:

```python id="fdh3b4"
plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

এখন feature relationships দেখতে পারবে।

---

# 45. Target Correlation

ধরো target:

```text
default
```

এবং numerical features:

```text
income
age
credit_score
loan_amount
```

Correlation:

```python id="m5m0ft"
corr = df.corr(numeric_only=True)

print(
    corr["default"]
    .sort_values(ascending=False)
)
```

এতে target-এর সাথে numerical variables-এর linear association দেখতে পারবে।

---

# 46. কিন্তু Classification Target হলে সতর্ক ⚠️

যদি:

```text
default = 0 / 1
```

তাহলে Pearson correlation বের করা mathematically possible হলেও interpretation-টা সাধারণ continuous target-এর মতো নয়।

EDA-তে এটি initial signal দিতে পারে, কিন্তু classification feature importance-এর final answer হিসেবে ব্যবহার করা যাবে না।

আর categorical features-এর জন্য:

```text
sex
city
category
```

এগুলোকে শুধু numeric code দিয়ে correlation করা misleading হতে পারে।

---

# 47. Correlation ≠ Feature Importance

ধরো:

```text
Feature A → correlation = 0.10
```

এর মানে এই নয়:

> Feature A useless.

কারণ:

```text
Correlation
    ↓
One type of association
```

Feature importance:

```text
Model
+
Data
+
Algorithm
```

এর উপর নির্ভর করে।

---

# 48. Heatmap দিয়ে Data Quality

Correlation matrix কখনো কখনো unusual relationship ধরতেও সাহায্য করে।

যেমন:

```text
height_cm
height_meter
```

যদি:

```text
r = 1.00
```

হয়, তাহলে duplicate information থাকতে পারে।

অথবা:

```text
total_price
quantity
unit_price
```

এর মধ্যে খুব strong correlation expected হতে পারে।

এগুলো data leakage নয় necessarily—domain knowledge দিয়ে বুঝতে হবে relationship expected কিনা।

---

# 49. Missing Values-এর প্রভাব

Correlation calculation-এর আগে missing values থাকলে Pandas pairwise available observations ব্যবহার করতে পারে।

তাই correlation result-এর sample size সব pair-এর জন্য একই নাও হতে পারে।

এজন্য serious analysis-এ শুধু:

```python id="h6z91p"
corr = df.corr()
```

দেখে শেষ না করে missingness এবং sample size-ও investigate করা উচিত।

---

# 50. Complete Professional Correlation Heatmap

এটি save করে রাখার মতো template:

```python id="9db8is"
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Load dataset
df = sns.load_dataset("tips")

# Correlation matrix
corr = df.corr(numeric_only=True)

# Mask upper triangle
mask = np.triu(
    np.ones_like(corr, dtype=bool)
)

# Plot
plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    mask=mask,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1,
    square=True,
    linewidths=0.5
)

plt.title("Correlation Heatmap")
plt.tight_layout()
plt.show()
```

---

# 51. Complete EDA Workflow

একটি নতুন dataset পেলে:

```text
Dataset
   ↓
Check columns
   ↓
Select numerical columns
   ↓
Check missing values
   ↓
Calculate correlation
   ↓
Heatmap
   ↓
Find strong relationships
   ↓
Investigate with scatterplot
   ↓
Check outliers with boxplot
   ↓
Consider ML implications
```

---

# 52. Heatmap-এর পরে কী করব?

ধরো heatmap দেখাল:

```text
income ↔ spending
r = 0.82
```

তখন শুধু conclusion:

> Strong correlation.

দিয়ে থেমে যাবে না।

পরের plot:

```python id="7s3fba"
sns.scatterplot(
    data=df,
    x="income",
    y="spending"
)

plt.show()
```

এখন relationship visually inspect করো।

---

# 53. Correlation + Scatterplot

এটি খুব powerful combination:

```text
Heatmap
   ↓
Relationship identify

Scatterplot
   ↓
Relationship visually verify
```

Example:

```python id="7o7x0v"
corr = df[["total_bill", "tip"]].corr()

print(corr)
```

তারপর:

```python id="7y2c7j"
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

---

# 54. M08 Mini Project

`tips` dataset দিয়ে এই analysis করো।

### Step 1

Numerical columns identify করো।

```python id="p3e3cs"
print(
    df.select_dtypes(
        include="number"
    ).columns
)
```

### Step 2

Correlation matrix:

```python id="e9j5b1"
corr = df.corr(numeric_only=True)
print(corr)
```

### Step 3

Heatmap:

```python id="qgq8ac"
sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.show()
```

### Step 4

Strongest relationship খুঁজে বের করো।

### Step 5

সেই দুই variable-এর scatterplot বানাও।

### Step 6

তারপর boxplot দিয়ে outlier inspect করো।

---

# 55. M08 Practice — Beginner 🟢

### Task 1

`tips` dataset-এর numerical columns বের করো।

### Task 2

Correlation matrix তৈরি করো।

### Task 3

Basic heatmap তৈরি করো।

### Task 4

`annot=True` যোগ করো।

### Task 5

`fmt=".2f"` ব্যবহার করো।

### Task 6

`center=0` ব্যবহার করো।

---

# 56. M08 Practice — Intermediate 🟡

### Task 7

Correlation heatmap-এ:

```python
vmin=-1
vmax=1
```

ব্যবহার করো।

### Task 8

Upper triangle mask করো।

### Task 9

Pearson এবং Spearman correlation compare করো।

### Task 10

সবচেয়ে strongly correlated pair বের করো।

### Task 11

সেই pair-এর scatterplot বানাও।

### Task 12

একটি pivot table বানিয়ে সেটির heatmap তৈরি করো।

---

# 57. M08 Practice — Advanced 🔴

নিজের ML dataset ব্যবহার করো।

### Task 13

সব numerical features-এর correlation heatmap তৈরি করো।

### Task 14

Correlation:

```text
> +0.80
```

এমন feature pairs খুঁজে বের করো।

### Task 15

Correlation:

```text
< -0.80
```

এমন feature pairs খুঁজে বের করো।

### Task 16

Target-এর সাথে feature correlations বের করো।

### Task 17

Strong correlation পাওয়া প্রতিটি pair-এর scatterplot বানাও।

### Task 18

Highly correlated features থাকলে:

```text
Are they redundant?
Is the relationship expected?
Could one feature be derived from another?
```

investigate করো।

---

# 58. M08 Common Mistakes ❌

### Mistake 1

Categorical column সরাসরি correlation-এ দেওয়া।

```python
df.corr()
```

এখানে `numeric_only=True` ব্যবহার করা safer:

```python
df.corr(numeric_only=True)
```

---

### Mistake 2

Correlation দেখে causation ধরে নেওয়া।

```text
Correlation ≠ Causation
```

---

### Mistake 3

Correlation = Feature importance ধরে নেওয়া।

দুটো এক নয়।

---

### Mistake 4

শুধু heatmap দেখে relationship final করা।

এরপর:

```text
Scatterplot
Boxplot
Distribution
Domain knowledge
```

দেখা উচিত।

---

### Mistake 5

`r = 0` মানেই কোনো relationship নেই ভাবা।

Pearson `r=0` মূলত **linear correlation নেই** বোঝায়। Nonlinear relationship থাকতে পারে।

---

# 59. M08 Cheat Sheet

### Correlation

```python id="7ky4v4"
df.corr(numeric_only=True)
```

### Pearson

```python id="7ry0pn"
df.corr(
    numeric_only=True,
    method="pearson"
)
```

### Spearman

```python id="l1hz0t"
df.corr(
    numeric_only=True,
    method="spearman"
)
```

### Basic Heatmap

```python id="d8f43h"
sns.heatmap(corr)
```

### Show values

```python id="3ijy3y"
sns.heatmap(
    corr,
    annot=True
)
```

### Two decimals

```python id="ddm9ws"
fmt=".2f"
```

### Center at zero

```python id="ey0flk"
center=0
```

### Correlation range

```python id="8q1nqi"
vmin=-1
vmax=1
```

### Mask

```python id="q8j8qj"
mask = np.triu(
    np.ones_like(corr, dtype=bool)
)
```

### Professional heatmap

```python id="1s7u9j"
sns.heatmap(
    corr,
    mask=mask,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1,
    square=True
)
```

---

# 60. M08 Completion Checklist ✅

M08 শেষ হলে এগুলো confidently explain করতে পারা উচিত:

* [ ] Correlation কী
* [ ] Positive correlation
* [ ] Negative correlation
* [ ] Zero/weak correlation
* [ ] Correlation range `-1` থেকে `+1`
* [ ] Correlation strength
* [ ] Correlation matrix
* [ ] Heatmap
* [ ] `sns.heatmap()`
* [ ] `annot`
* [ ] `fmt`
* [ ] `cmap`
* [ ] `center`
* [ ] `vmin`
* [ ] `vmax`
* [ ] `square`
* [ ] `linewidths`
* [ ] Mask
* [ ] Pearson correlation
* [ ] Spearman correlation
* [ ] Multicollinearity
* [ ] Feature relationship
* [ ] Correlation বনাম causation
* [ ] Correlation বনাম feature importance
* [ ] Pivot table + heatmap
* [ ] Heatmap + scatterplot workflow
* [ ] ML dataset correlation analysis

---

# 🧠 M08-এর Core Mental Model

```text
             NUMERICAL FEATURES
                    │
                    ↓
              Correlation
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
      Positive             Negative
       -1 → 0 → +1
                    │
                    ↓
           Correlation Matrix
                    │
                    ↓
                Heatmap
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
 Strong relationships     Weak relationships
          │
          ↓
     Investigate further
          │
    ┌─────┼─────┐
    ↓     ↓     ↓
Scatter Boxplot Domain
plot             Knowledge
```

### ⭐ সবচেয়ে গুরুত্বপূর্ণ ৫টি কথা

```text
1. Correlation measures association.
2. Pearson mainly measures linear association.
3. Correlation ≠ causation.
4. Heatmap makes many correlations easy to inspect.
5. Strong correlation ≠ automatically important ML feature.
```

**M01–M08 পর্যন্ত এখন Seaborn-এর EDA foundation তৈরি হচ্ছে:**

```text
M01 → Seaborn Basics
M02 → Dataset & DataFrame
M03 → Distribution
M04 → Boxplot
M05 → Violinplot
M06 → Countplot & Barplot
M07 → Stripplot & Swarmplot
M08 → Heatmap & Correlation
```

পরবর্তী logical step হবে **M09 — Pairplot & Jointplot Deep Dive**, যেখানে একসাথে multiple numerical features-এর relationship, distribution এবং pairwise interaction visualভাবে analyse করা হবে।

---
# 📊 Seaborn M09 — Pairplot & Jointplot Deep Dive

M01–M08 পর্যন্ত তুমি individual plot, distribution, category comparison, correlation ইত্যাদি শিখেছো। এখন **M09-এর মূল লক্ষ্য হলো একসাথে অনেকগুলো numerical feature-এর relationship দেখা**।

```text
M01 → Seaborn Basics
M02 → Dataset & DataFrame
M03 → Distribution
M04 → Boxplot
M05 → Violinplot
M06 → Countplot & Barplot
M07 → Stripplot & Swarmplot
M08 → Heatmap & Correlation
M09 → Pairplot & Jointplot ⭐
```

---

# 1. Pairplot কী?

`pairplot()` একটি dataset-এর **multiple numerical columns-এর pairwise relationship** একসাথে দেখায়।

ধরো আমাদের কাছে:

```text
total_bill
tip
size
```

তাহলে pairplot দেখাবে:

```text
              total_bill      tip       size

total_bill      hist         scatter    scatter

tip             scatter      hist       scatter

size            scatter      scatter    hist
```

অর্থাৎ প্রতিটি numerical feature-এর সাথে অন্য feature-এর relationship দেখা যায়।

---

# 2. Dataset তৈরি করি

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

Dataset:

```text
   total_bill   tip     sex smoker  day    time  size
0       16.99  1.01  Female     No  Sun  Dinner     2
1       10.34  1.66    Male     No  Sun  Dinner     3
2       21.01  3.50    Male     No  Sun  Dinner     3
```

---

# 3. Basic Pairplot

সব numerical feature automatically নেওয়া:

```python
sns.pairplot(df)

plt.show()
```

এটি সাধারণত numerical columns-এর pairwise relationship দেখাবে।

---

# 4. শুধু নির্দিষ্ট columns

সব feature দেখানো সবসময় ভালো নয়।

তুমি চাইলে:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"]
)

plt.show()
```

এখানে শুধু:

```text
total_bill
tip
size
```

ব্যবহার হবে।

---

# 5. Pairplot কীভাবে পড়বে?

ধরো:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"]
)
plt.show()
```

তাহলে diagonal-এ থাকবে:

```text
total_bill → distribution
tip        → distribution
size       → distribution
```

আর diagonal-এর বাইরে:

```text
total_bill vs tip
total_bill vs size
tip vs size
```

এর relationship দেখা যাবে।

---

# 6. Diagonal কী দেখায়?

Pairplot-এর diagonal খুব গুরুত্বপূর্ণ।

সাধারণত diagonal-এ distribution দেখানো হয়।

যেমন:

```text
total_bill
     ↓
  ▁▂▃▅▇▅▃▂
```

এখানে তুমি বুঝতে পারবে:

* data কোথায় বেশি concentrated
* distribution shape
* skewness
* possible outliers
* multiple peaks

---

# 7. `hue` — সবচেয়ে গুরুত্বপূর্ণ parameter ⭐

Category অনুযায়ী data আলাদা করতে:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    hue="sex"
)

plt.show()
```

এখন:

```text
Male
Female
```

দুই category আলাদা করে দেখা যাবে।

এটি EDA-তে অনেক useful।

---

# 8. `hue="smoker"`

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    hue="smoker"
)

plt.show()
```

এখানে:

```text
Yes
No
```

আলাদা হবে।

---

# 9. ML-এর জন্য `hue` কেন গুরুত্বপূর্ণ?

ধরো তোমার classification problem:

```text
Class 0
Class 1
```

তুমি দেখতে চাও:

> দুই class কি feature space-এ আলাদা?

তাহলে:

```python
sns.pairplot(
    df,
    hue="target"
)

plt.show()
```

যদি দুই class আলাদা cluster তৈরি করে:

```text
Class 0     ● ● ● ●

                  ○ ○ ○
               ○ ○ ○ ○
Class 1
```

তাহলে featureগুলো classification-এর জন্য useful হতে পারে।

আর যদি:

```text
● ○ ● ○ ●
○ ● ○ ● ○
● ○ ● ○ ●
```

তাহলে classes heavily overlap করছে।

---

# 10. `diag_kind`

Diagonal-এ কী দেখাবে সেটা control করা যায়।

### Histogram

```python
sns.pairplot(
    df,
    diag_kind="hist"
)

plt.show()
```

### KDE

```python
sns.pairplot(
    df,
    diag_kind="kde"
)

plt.show()
```

KDE distribution আরও smoothভাবে দেখায়।

---

# 11. `kind`

Pairplot-এর main relationship plot সাধারণত scatterplot।

তবে `kind` দিয়ে পরিবর্তন করা যায়।

```python
sns.pairplot(
    df,
    kind="scatter"
)

plt.show()
```

---

# 12. Regression pairplot

```python
sns.pairplot(
    df,
    kind="reg"
)

plt.show()
```

এখানে scatter-এর সাথে regression line দেখা যায়।

এটি relationship-এর direction বুঝতে সাহায্য করে।

যেমন:

```text
tip
│
│             ●
│          ●
│       ●
│    ●
│ ●
└──────────────── total_bill
```

Positive relationship বোঝা যায়।

---

# 13. `corner=True`

Pairplot symmetric হওয়ায় একই relationship দুইবার দেখা যায়।

যেমন:

```text
A vs B
B vs A
```

দুটো একই information।

তাই শুধু নিচের অংশ দেখতে:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    corner=True
)

plt.show()
```

এতে plot অনেক clean হয়।

---

# 14. `height`

প্রতিটি subplot-এর size control:

```python
sns.pairplot(
    df,
    height=2.5
)

plt.show()
```

---

# 15. `plot_kws`

Scatterplot customize করতে:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    plot_kws={
        "alpha": 0.6
    }
)

plt.show()
```

Large dataset হলে `alpha` useful।

---

# 16. Pairplot + Hue + Corner

একটি practical combination:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    hue="sex",
    corner=True,
    diag_kind="kde",
    plot_kws={
        "alpha": 0.6
    }
)

plt.show()
```

এটি একটি ভালো EDA visualization।

---

# 17. Pairplot-এ categorical column দেওয়া যাবে?

সরাসরি সাধারণত numerical relationship-এর জন্য pairplot বেশি useful।

যেমন:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip"],
    hue="day"
)

plt.show()
```

এখানে `day` category হিসেবে `hue` কাজ করবে।

---

# 18. Pairplot-এর limitation

এখানে খুব গুরুত্বপূর্ণ বিষয় আছে।

ধরো dataset-এ 10টি numerical feature আছে।

Pairplot প্রায়:

```text
10 × 10 = 100
```

subplot তৈরি করতে পারে।

তাই plot অত্যন্ত বড় হয়ে যেতে পারে।

সেজন্য:

❌ সব feature blindly দেওয়া উচিত নয়।

বরং:

```python
important_features = [
    "feature1",
    "feature2",
    "feature3",
    "feature4"
]
```

তারপর:

```python
sns.pairplot(
    df,
    vars=important_features
)
```

---

# 19. Pairplot বনাম Heatmap

M08-এ আমরা correlation heatmap শিখেছি।

দুটোর difference:

| Heatmap                           | Pairplot                       |
| --------------------------------- | ------------------------------ |
| Correlation দেখায়                 | Actual data points দেখায়       |
| Compact                           | তুলনামূলক বড়                   |
| Numerical summary                 | Visual relationship            |
| Linear relationship সহজে বোঝা যায় | Shape/cluster/outlier বোঝা যায় |
| Correlation coefficient দেয়       | Scatter distribution দেয়       |

Best workflow:

```text
Correlation Heatmap
       ↓
Strong relationships identify
       ↓
Pairplot
       ↓
Actual relationship inspect
       ↓
Scatterplot
       ↓
Detailed investigation
```

---

# 20. Pairplot বনাম Scatterplot

### Scatterplot

দুই feature:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

### Pairplot

অনেক feature:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"]
)
```

অর্থাৎ:

```text
Scatterplot → One relationship

Pairplot → Many relationships
```

---

# 21. এখন Jointplot ⭐

`jointplot()` একটি **দুটি numerical variable-এর relationship + তাদের individual distributions** একসাথে দেখায়।

Example:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এখানে:

```text
             tip distribution
                    │
                    │
       scatter      │
                    │
                    │
                    └────────────
                     total_bill distribution
```

---

# 22. Jointplot-এর তিনটি প্রধান অংশ

Jointplot-এ:

### Center

দুই variable-এর relationship।

```text
X vs Y
```

### Top

X-এর distribution।

### Right

Y-এর distribution।

অর্থাৎ:

```text
             Y distribution
                  │
                  │
       X vs Y     │
                  │
                  │
                  └────────────
                  X distribution
```

---

# 23. `kind="scatter"`

Default style:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="scatter"
)

plt.show()
```

---

# 24. `kind="reg"`

Regression relationship:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

plt.show()
```

এখানে regression line পাওয়া যাবে।

---

# 25. `kind="hist"`

Central relationship histogram দিয়ে:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="hist"
)

plt.show()
```

---

# 26. `kind="kde"`

Smooth density:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="kde"
)

plt.show()
```

এটি density concentration দেখতে useful।

---

# 27. `kind="hex"`

Large dataset-এর জন্য খুব useful।

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="hex"
)

plt.show()
```

Hexagonal bins ব্যবহার করে data density দেখায়।

Large dataset-এ thousands/millions of points থাকলে scatterplot-এর চেয়ে অনেক readable হতে পারে।

---

# 28. Jointplot + Hue

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এতে category-wise relationship দেখা যায়।

---

# 29. Jointplot + Regression

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

plt.show()
```

Interpretation:

যদি line upward হয়:

```text
total_bill ↑
      ↓
tip ↑
```

Positive relationship।

---

# 30. Jointplot vs Pairplot

এটা খুব ভালোভাবে মনে রাখো।

### Pairplot

অনেক variable:

```text
A ↔ B
A ↔ C
A ↔ D
B ↔ C
B ↔ D
C ↔ D
```

### Jointplot

মূলত দুই variable:

```text
A ↔ B
```

তাই:

```text
Pairplot  → Multi-feature exploration

Jointplot → Deep investigation of 2 features
```

---

# 31. Pairplot → Jointplot workflow ⭐

Professional EDA-তে এমন workflow করতে পারো:

### Step 1 — Correlation

```python
corr = df.corr(numeric_only=True)

sns.heatmap(
    corr,
    annot=True
)

plt.show()
```

### Step 2 — Strong relationship খুঁজবে

ধরো:

```text
total_bill ↔ tip
```

এর correlation strong।

### Step 3 — Pairplot

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    hue="sex"
)

plt.show()
```

### Step 4 — Jointplot

আরও গভীরভাবে:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

plt.show()
```

### Step 5 — Conclusion

যেমন:

```text
total_bill and tip have positive relationship.
Higher bills generally correspond to higher tips.
```

---

# 32. Pairplot দিয়ে Outlier দেখা

ধরো:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"]
)

plt.show()
```

কোনো plot-এ যদি একটি point অনেক দূরে থাকে:

```text
● ● ● ●
 ● ● ●

                         ●
```

এটি potential outlier হতে পারে।

তারপর:

```python
sns.boxplot(
    data=df,
    y="total_bill"
)

plt.show()
```

দিয়ে confirm করতে পারো।

---

# 33. Pairplot দিয়ে Cluster দেখা

Machine Learning-এর জন্য এটি অত্যন্ত important।

ধরো:

```text
Class A:

● ● ●
 ● ●
  ●


Class B:


                ○ ○
              ○ ○ ○
               ○
```

এখানে দুই class-এর separation ভালো।

এতে feature combination classification-এর জন্য useful হতে পারে।

---

# 34. Pairplot দিয়ে Feature Separation

ধরো তোমার dataset:

```text
Age
Income
Spending
Target
```

তুমি:

```python
sns.pairplot(
    df,
    vars=["Age", "Income", "Spending"],
    hue="Target"
)

plt.show()
```

এখন প্রশ্ন করবে:

> কোন feature combination target classes-কে সবচেয়ে ভালো আলাদা করছে?

এটি ML feature analysis-এর গুরুত্বপূর্ণ অংশ।

---

# 35. Pairplot দিয়ে Non-linear Relationship

Correlation কম হলেও relationship থাকতে পারে।

যেমন:

```text
Y
│       ●
│     ●   ●
│   ●       ●
│ ●           ●
└──────────────── X
```

এটি curved relationship।

Pearson correlation হয়তো relationship পুরোপুরি capture করবে না।

Pairplot/scatterplot কিন্তু shape দেখাতে পারে।

তাই:

```text
Correlation ≠ Complete Relationship Analysis
```

---

# 36. Jointplot দিয়ে Distribution + Relationship

ধরো:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)
```

একসাথে জানতে পারবে:

### X distribution

```text
total_bill
```

### Y distribution

```text
tip
```

### Relationship

```text
total_bill ↔ tip
```

এটাই Jointplot-এর বড় advantage।

---

# 37. Real EDA Example

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

features = [
    "total_bill",
    "tip",
    "size"
]

sns.pairplot(
    df,
    vars=features,
    hue="sex",
    corner=True,
    diag_kind="kde",
    plot_kws={
        "alpha": 0.6
    }
)

plt.show()
```

তারপর:

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

plt.show()
```

---

# 38. ML Dataset Example

ধরো:

```python
df = pd.read_csv("dataset.csv")
```

Columns:

```text
age
income
experience
education_score
target
```

Pairplot:

```python
sns.pairplot(
    df,
    vars=[
        "age",
        "income",
        "experience",
        "education_score"
    ],
    hue="target",
    corner=True
)

plt.show()
```

এখানে তুমি investigate করবে:

```text
1. কোন feature correlated?
2. কোন feature-এর distribution skewed?
3. Outlier আছে?
4. Class separation কেমন?
5. Feature overlap কেমন?
6. Non-linear relationship আছে?
```

---

# 39. একটি গুরুত্বপূর্ণ সতর্কতা ⚠️

Pairplot দেখে সরাসরি বলা যাবে না:

> "এই feature সবচেয়ে important."

কারণ pairplot শুধু visualization।

Feature importance জানতে ব্যবহার করতে পারো:

```text
Correlation
Mutual Information
Random Forest Feature Importance
Permutation Importance
SHAP
Model coefficients
```

অর্থাৎ:

```text
Pairplot
   ↓
Explore
   ↓
Hypothesis
   ↓
Statistical / ML analysis
   ↓
Conclusion
```

---

# 40. Pairplot-এর গুরুত্বপূর্ণ Parameters

```python
sns.pairplot(
    data=df,
    vars=None,
    hue=None,
    kind="scatter",
    diag_kind="auto",
    corner=False,
    height=2.5
)
```

মনে রাখবে:

| Parameter   | কাজ                    |
| ----------- | ---------------------- |
| `data`      | DataFrame              |
| `vars`      | কোন columns            |
| `hue`       | category অনুযায়ী color |
| `kind`      | relationship plot      |
| `diag_kind` | diagonal plot          |
| `corner`    | half matrix            |
| `height`    | subplot size           |

---

# 41. Jointplot-এর গুরুত্বপূর্ণ Parameters

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="scatter",
    hue="sex"
)
```

| Parameter | কাজ         |
| --------- | ----------- |
| `data`    | DataFrame   |
| `x`       | X variable  |
| `y`       | Y variable  |
| `kind`    | plot type   |
| `hue`     | category    |
| `height`  | figure size |

---

# 42. Pairplot Cheat Sheet

```python
# Basic
sns.pairplot(df)

# Selected features
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"]
)

# Hue
sns.pairplot(
    df,
    hue="sex"
)

# Corner
sns.pairplot(
    df,
    corner=True
)

# KDE diagonal
sns.pairplot(
    df,
    diag_kind="kde"
)

# Regression
sns.pairplot(
    df,
    kind="reg"
)
```

---

# 43. Jointplot Cheat Sheet

```python
# Scatter
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip"
)

# Regression
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)

# KDE
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="kde"
)

# Histogram
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="hist"
)

# Hex
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="hex"
)
```

---

# 🧠 M09 Mental Model

এটা খুব ভালোভাবে মনে রাখো:

```text
                 SEABORN EDA
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
      Pairplot              Jointplot
          │                     │
    Many features          Two features
          │                     │
    Pairwise relation       Deep relation
          │                     │
    Distribution            Distribution
          │                     │
       hue/class             regression
          │                     │
          └──────────┬──────────┘
                     ↓
              EDA Understanding
                     ↓
              ML Feature Analysis
```

---

# 🎯 M09 Practice

### Beginner

**Task 1**

```python
sns.pairplot(df)
```

নিজে run করো এবং প্রতিটি subplot identify করো।

### Task 2

শুধু:

```text
total_bill
tip
size
```

দিয়ে pairplot বানাও।

### Task 3

`sex` দিয়ে `hue` করো।

### Task 4

`corner=True` ব্যবহার করো।

### Task 5

`diag_kind="kde"` ব্যবহার করো।

---

## Intermediate

### Task 6

`kind="reg"` দিয়ে pairplot তৈরি করো।

### Task 7

```python
sns.jointplot(
    data=df,
    x="total_bill",
    y="tip",
    kind="reg"
)
```

এর regression line interpret করো।

### Task 8

একই X/Y-এর জন্য:

```text
scatter
reg
kde
hex
```

চারটি jointplot তৈরি করে difference লিখো।

### Task 9

`hue="sex"` দিয়ে jointplot তৈরি করো।

### Task 10

Pairplot দেখে কোন feature pair-এর relationship strongest মনে হচ্ছে সেটা identify করো এবং M08 correlation heatmap দিয়ে verify করো।

---

# 🔥 M09 Mini Project

`tips` dataset ব্যবহার করে একটি ছোট EDA report বানাও।

### Step 1

```python
df.info()
```

### Step 2

Numerical columns বের করো।

### Step 3

Correlation heatmap বানাও।

### Step 4

Pairplot:

```python
sns.pairplot(
    df,
    vars=["total_bill", "tip", "size"],
    hue="sex",
    corner=True
)
```

### Step 5

সবচেয়ে interesting দুইটি feature নির্বাচন করো।

### Step 6

Jointplot বানাও।

### Step 7

শেষে এই ৫টি প্রশ্নের উত্তর দাও:

```text
1. কোন feature-এর distribution skewed?
2. কোন দুই feature-এর positive relationship আছে?
3. Outlier আছে কি?
4. Category অনুযায়ী relationship পরিবর্তন হচ্ছে কি?
5. কোন feature pair ML-এর জন্য potentially useful?
```

---

# ✅ M09 Completion Checklist

M09 শেষ হয়েছে ধরে নেবে যখন তুমি নিজে explanation ছাড়া এগুলো করতে পারবে:

* [ ] `pairplot()`
* [ ] `vars`
* [ ] `hue`
* [ ] `diag_kind`
* [ ] `kind`
* [ ] `corner=True`
* [ ] Pairplot interpretation
* [ ] Class separation analysis
* [ ] Outlier observation
* [ ] `jointplot()`
* [ ] `kind="scatter"`
* [ ] `kind="reg"`
* [ ] `kind="kde"`
* [ ] `kind="hist"`
* [ ] `kind="hex"`
* [ ] Pairplot vs Jointplot
* [ ] Correlation → Pairplot → Jointplot workflow

### ⭐ সবচেয়ে গুরুত্বপূর্ণ

```text
M08: Correlation
        ↓
M09: Pairplot
        ↓
M09: Jointplot
        ↓
Relationship বুঝা
        ↓
Feature analysis
        ↓
ML-এর জন্য better EDA
```

**Next: M10 — Regression Plots & Relationship Analysis Deep Dive** — `regplot`, `lmplot`, regression line, residuals, confidence interval, linear vs non-linear relationship এবং ML regression-এর সাথে visualization-এর connection।


---
# 📈 Seaborn M10 — Regression Plots & Relationship Analysis Deep Dive

M09-এ আমরা `pairplot()` এবং `jointplot()` দিয়ে **দুই বা অনেক feature-এর relationship** দেখেছি। এখন M10-এ সেই relationship-কে আরও গভীরভাবে analyze করব।

```text
M08 → Correlation
M09 → Pairplot & Jointplot
M10 → Regression & Relationship Analysis ⭐
```

M10-এর মূল লক্ষ্য:

```text
X → Y relationship
       ↓
Scatterplot
       ↓
Regression Line
       ↓
Confidence Interval
       ↓
Residuals
       ↓
Linear / Non-linear relationship
       ↓
ML Regression Understanding
```

---

# 1. Regression Plot কী?

ধরো:

```text
X = total_bill
Y = tip
```

আমরা জানতে চাই:

> Total bill বাড়লে tip কি বাড়ে?

প্রথমে scatterplot:

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এখানে প্রতিটি dot একটি observation।

---

# 2. Regression Line কী?

Data points-এর trend বোঝার জন্য একটি best-fit line ব্যবহার করা যায়।

Conceptually:

```text
Y
│
│              ●
│           ●
│        ●
│     ●
│  ●
│
└──────────────── X
```

Regression line:

```text
Y
│
│             ●
│          ● /
│       ●  /
│    ●   /
│ ●    /
│    /
└──────────────── X
```

এটি আমাদের overall trend বোঝায়।

---

# 3. `sns.regplot()` ⭐

Seaborn-এর সবচেয়ে গুরুত্বপূর্ণ regression visualization function:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটি সাধারণত:

* scatter points
* regression line
* confidence interval

দেখায়।

---

# 4. `regplot()` কী করছে?

Conceptually:

```text
Actual Data
    ↓
● ● ● ● ●
    ↓
Best-fit relationship
    ↓
Regression Line
```

Simple Linear Regression:

$$
y = mx + b
$$

Machine Learning-এর ভাষায়:

$$
\hat{y} = \beta_0 + \beta_1x
$$

যেখানে:

* `x` = input feature
* `y` = target
* `β₀` = intercept
* `β₁` = coefficient

---

# 5. Regression Line কীভাবে interpret করবে?

### Positive relationship

```text
Y
│
│        /
│      /
│    /
│  /
│/
└──────── X
```

অর্থ:

```text
X ↑ → Y ↑
```

---

### Negative relationship

```text
Y
│\
│ \
│  \
│   \
│    \
└──────── X
```

অর্থ:

```text
X ↑ → Y ↓
```

---

### Weak / almost no linear relationship

```text
Y
│ ●    ●
│    ●
│ ●      ●
│   ●
│      ●
└──────── X
```

Regression line প্রায় flat হতে পারে।

---

# 6. `scatterplot()` বনাম `regplot()`

### Scatterplot

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

শুধু observations দেখায়।

### Regplot

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

Observations + regression trend দেখায়।

তাই:

```text
scatterplot → What does the data look like?

regplot → What is the overall linear trend?
```

---

# 7. Confidence Interval কী?

`regplot()`-এ regression line-এর চারপাশে shaded area দেখতে পারো।

এটি সাধারণত **confidence interval**।

Concept:

```text
Y
│
│       ╱──────
│      ╱
│     ╱
│    ╱──────
│
└──────────── X
```

Line হলো estimated relationship।

Shaded band হলো uncertainty-এর ধারণা।

Default confidence level সাধারণত 95%।

---

# 8. `ci`

Confidence interval পরিবর্তন:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    ci=95
)

plt.show()
```

অথবা:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    ci=99
)
```

Confidence interval বন্ধ:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    ci=None
)
```

---

# 9. Confidence Interval কীভাবে বুঝবে?

যদি band narrow হয়:

```text
→ estimate relatively more precise
```

যদি band wide হয়:

```text
→ more uncertainty
```

তবে confidence interval-কে সরাসরি "data range" ভাববে না।

এটি regression estimate-এর uncertainty সম্পর্কিত।

---

# 10. `scatter_kws`

Scatter points customize করতে:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    scatter_kws={
        "alpha": 0.5
    }
)

plt.show()
```

Large dataset-এর ক্ষেত্রে transparency useful।

---

# 11. `line_kws`

Regression line customize করতে:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    line_kws={
        "linewidth": 2
    }
)

plt.show()
```

---

# 12. Scatter + Regression একসাথে

একটি clean visualization:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    scatter_kws={"alpha": 0.6},
    line_kws={"linewidth": 2}
)

plt.xlabel("Total Bill")
plt.ylabel("Tip")
plt.title("Total Bill vs Tip")

plt.show()
```

---

# 13. `sns.lmplot()` ⭐

আরেকটি গুরুত্বপূর্ণ function হলো:

```python
sns.lmplot()
```

Example:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটিও regression plot তৈরি করে।

তাহলে `regplot()` আর `lmplot()`-এর পার্থক্য কী?

---

# 14. `regplot()` vs `lmplot()`

| `regplot()`                        | `lmplot()`                        |
| ---------------------------------- | --------------------------------- |
| Axes-level function                | Figure-level function             |
| Existing axes-এর সাথে সহজে কাজ করে | Faceting সহজ                      |
| Single relationship                | Multiple groups/facets            |
| More flexible in Matplotlib layout | `hue`, `col`, `row` দিয়ে grouping |

সহজভাবে:

```text
regplot → One regression plot

lmplot → Regression + groups/facets
```

---

# 15. `lmplot()` + Hue

ধরো তুমি male/female অনুযায়ী relationship দেখতে চাও:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এখন প্রত্যেক category-এর regression trend দেখা যাবে।

---

# 16. কেন Group-wise Regression গুরুত্বপূর্ণ?

ধরো overall relationship:

```text
total_bill ↑
      ↓
tip ↑
```

কিন্তু male এবং female-এর trend আলাদা হতে পারে।

```text
Male:
    /
   /

Female:
  /
 /
```

অথবা:

```text
Male:
  /
 /

Female:
    /
   /
```

এতে বোঝা যায় relationship category অনুযায়ী পরিবর্তিত হচ্ছে কি না।

---

# 17. `col`

একাধিক subplot তৈরি:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    col="sex"
)

plt.show()
```

তাহলে:

```text
Male              Female
─────────         ─────────
scatter + line    scatter + line
```

---

# 18. `row`

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    row="time"
)

plt.show()
```

যেমন:

```text
Lunch
Dinner
```

আলাদা regression plot।

---

# 19. `hue + col`

আরও advanced:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    col="time"
)

plt.show()
```

এখন:

```text
             Lunch             Dinner

Male         regression        regression
Female       regression        regression
```

এটি EDA-তে খুব powerful।

---

# 20. `order` — Polynomial Regression

এখন একটি গুরুত্বপূর্ণ বিষয়।

সব relationship linear নয়।

যদি curved relationship হয়:

```text
Y
│        ●
│      ●   ●
│    ●       ●
│  ●           ●
│ ●             ●
└──────────────── X
```

তখন linear regression যথেষ্ট নাও হতে পারে।

Seaborn-এ:

```python
sns.regplot(
    data=df,
    x="x",
    y="y",
    order=2
)

plt.show()
```

এটি polynomial degree 2 fit করার চেষ্টা করে।

---

# 21. `order=3`

```python
sns.regplot(
    data=df,
    x="x",
    y="y",
    order=3
)

plt.show()
```

Polynomial degree 3।

Concept:

$$
y = \beta_0 + \beta_1x + \beta_2x^2 + \beta_3x^3
$$

---

# 22. Linear বনাম Polynomial

### Linear

$$
y = \beta_0 + \beta_1x
$$

Shape:

```text
/
```

### Polynomial

$$
y = \beta_0 + \beta_1x + \beta_2x^2
$$

Shape:

```text
╲___╱
```

বা:

```text
╱‾‾╲
```

---

# 23. কিন্তু সাবধান ⚠️

Higher-order polynomial ব্যবহার করলেই model ভালো হবে না।

যেমন:

```python
order=10
```

দিলে training data-এর noise পর্যন্ত fit করতে পারে।

এটি:

```text
Overfitting
```

করতে পারে।

EDA visualization-এ polynomial curve দেখে model quality conclude করা যাবে না।

---

# 24. `lowess=True`

Non-linear smooth trend দেখতে:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    lowess=True
)

plt.show()
```

LOWESS একটি locally weighted smoothing approach।

এটি useful যখন:

```text
relationship linear নয়
```

এবং তুমি trend দেখতে চাও।

---

# 25. Linear বনাম LOWESS

### Linear regression

```text
Y
│       /
│     /
│   /
│ /
└──────── X
```

### LOWESS

```text
Y
│      ╭──╮
│    ╭─╯  ╰╮
│  ╭─╯     ╰
│╭─╯
└──────────── X
```

LOWESS data-এর local pattern follow করতে পারে।

---

# 26. Residual কী?

Regression model prediction করে:

$$
\hat y
$$

Actual value:

$$
y
$$

Residual:

$$
e = y - \hat y
$$

অর্থাৎ:

```text
Residual = Actual - Predicted
```

উদাহরণ:

```text
Actual = 10
Predicted = 8

Residual = 10 - 8
         = 2
```

---

# 27. Residual কেন গুরুত্বপূর্ণ?

একটি ভালো linear regression-এর ক্ষেত্রে residual ideally:

```text
randomly distributed
```

হওয়া উচিত।

যদি pattern থাকে:

```text
Residual
│ ●
│    ●
│       ●
│          ●
└──────────── X
```

তাহলে model relationship পুরোপুরি capture করছে না।

---

# 28. Residual Pattern

### Good

```text
+     ●    ●
│  ●      ●
0 ─────────────────
│    ●    ●
-      ●
```

Random scatter।

### Problematic

```text
+ ●
│   ●
│     ●
0 ─────────────
│
│
```

Pattern আছে।

এতে:

* non-linearity
* heteroscedasticity
* missing variables

ইত্যাদি issue থাকতে পারে।

---

# 29. `residplot()`

Seaborn-এ residual visualization:

```python
sns.residplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটি regression residuals visualize করতে সাহায্য করে।

---

# 30. Residual Plot কীভাবে পড়বে?

```text
Residual
│
│ ●    ●
│    ●
0 ───────────────
│  ●     ●
│     ●
│ ●
└──────────────── X
```

যদি points roughly random:

```text
→ linear model reasonable হতে পারে
```

যদি clear curve:

```text
→ non-linear relationship হতে পারে
```

---

# 31. Heteroscedasticity

আরেকটি গুরুত্বপূর্ণ concept।

ধরো residual:

```text
│       ●
│      ● ●
│    ●   ● ●
│  ●        ● ●
│●              ●
└──────────────── X
```

X বাড়ার সাথে residual spread বাড়ছে।

এটাকে বলা হয়:

```text
Heteroscedasticity
```

Regression analysis-এ এটি গুরুত্বপূর্ণ diagnostic issue।

---

# 32. Regression Plot + Correlation

M08-এ correlation শিখেছো।

ধরো:

```python
corr = df["total_bill"].corr(df["tip"])

print(corr)
```

তারপর:

```python
sns.regplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

দুটো একসাথে ব্যবহার করো।

```text
Correlation
     ↓
Strength of linear association
     
Regression Plot
     ↓
Visual trend + outliers + spread
```

---

# 33. Correlation strong কিন্তু সমস্যা থাকতে পারে

ধরো:

```text
r = 0.85
```

এটি strong positive correlation।

কিন্তু scatterplot-এ যদি:

```text
একটি extreme outlier
```

থাকে, correlation প্রভাবিত হতে পারে।

তাই:

```text
Correlation → Summary
Scatter/Regression → Visual evidence
```

দুটোই দরকার।

---

# 34. Outlier এবং Regression Line

একটি extreme outlier:

```text
Y
│             ●
│          ●
│       ●
│    ●
│ ●
│                         ●
└──────────────────────── X
```

Regression line outlier দ্বারা significantly পরিবর্তিত হতে পারে।

এটাকে বলা যায়:

```text
Influential observation
```

তাই regression করার আগে:

```text
Outlier analysis
```

গুরুত্বপূর্ণ।

---

# 35. ML-এর সাথে Connection ⭐

ধরো তুমি একটি ML model বানাবে:

```text
Input:
House Size

Target:
House Price
```

প্রথমে:

```python
sns.regplot(
    data=df,
    x="house_size",
    y="price"
)
```

তুমি দেখতে পারবে:

```text
1. Positive relationship?
2. Linear relationship?
3. Outlier?
4. Variance constant?
5. Data spread?
```

এরপর Linear Regression model তৈরি করতে পারো।

---

# 36. Regression EDA Workflow

Professional workflow:

```text
Raw Dataset
     ↓
Data Cleaning
     ↓
Distribution
     ↓
Correlation
     ↓
Scatterplot
     ↓
Regression Plot
     ↓
Residual Plot
     ↓
Outlier Analysis
     ↓
Feature Engineering
     ↓
ML Regression
```

---

# 37. একটি Complete Example

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

# Scatter + Regression
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    scatter_kws={
        "alpha": 0.6
    }
)

plt.title("Total Bill vs Tip")
plt.xlabel("Total Bill")
plt.ylabel("Tip")

plt.show()
```

---

# 38. Group-wise Regression Example

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()
```

এখানে Male/Female-এর trend compare করতে পারবে।

---

# 39. Facet Regression

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    col="time",
    hue="sex"
)

plt.show()
```

এখন investigate করতে পারবে:

```text
Lunch:
    Male vs Female

Dinner:
    Male vs Female
```

---

# 40. Residual Analysis

```python
sns.residplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.axhline(
    0,
    linestyle="--"
)

plt.title("Residual Plot")

plt.show()
```

Zero line-এর চারপাশে residual কীভাবে distributed সেটা দেখো।

---

# 41. Polynomial Example

নিজের artificial data দিয়ে:

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

x = np.arange(1, 21)

y = x**2 + np.random.normal(
    0,
    20,
    20
)

data = pd.DataFrame({
    "x": x,
    "y": y
})
```

Linear:

```python
sns.regplot(
    data=data,
    x="x",
    y="y"
)

plt.show()
```

Polynomial:

```python
sns.regplot(
    data=data,
    x="x",
    y="y",
    order=2
)

plt.show()
```

এখন দুইটি fit compare করো।

---

# 42. Linear Relationship-এর assumptions সম্পর্কে ধারণা

Seaborn নিজে assumptions validate করে না। কিন্তু regression analysis-এর ক্ষেত্রে সাধারণত গুরুত্বপূর্ণ বিষয়:

```text
1. Linearity
2. Independence
3. Constant variance
4. Residual behavior
5. Outliers / influential observations
```

এগুলো ML/statistics-এর পরের গভীর topics-এর সাথে যুক্ত।

---

# 43. `regplot()` vs `lmplot()` vs `residplot()`

এক নজরে:

| Function                | Purpose                               |
| ----------------------- | ------------------------------------- |
| `regplot()`             | Scatter + regression                  |
| `lmplot()`              | Regression + grouping/faceting        |
| `residplot()`           | Residual analysis                     |
| `scatterplot()`         | Raw relationship                      |
| `jointplot(kind="reg")` | Relationship + marginal distributions |

---

# 44. M10-এর Complete EDA Example ⭐

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

# 1. Scatter + regression
sns.regplot(
    data=df,
    x="total_bill",
    y="tip",
    scatter_kws={"alpha": 0.6}
)

plt.title("Total Bill vs Tip")
plt.show()


# 2. Group-wise regression
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)

plt.show()


# 3. Residual analysis
sns.residplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.axhline(
    0,
    linestyle="--"
)

plt.title("Residual Analysis")
plt.show()


# 4. Correlation
correlation = df["total_bill"].corr(
    df["tip"]
)

print("Correlation:", correlation)
```

---

# 🧠 M10 Mental Model

এটা মনে রাখো:

```text
                Two Variables
                     │
                     ↓
              Scatterplot
                     │
                     ↓
            Is there a trend?
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
        Yes                    No
          │                     │
          ↓                     ↓
    Regression Plot        Investigate
          │
          ↓
   Linear or Non-linear?
          │
     ┌────┴────┐
     ↓         ↓
  Linear    Non-linear
     │         │
 regplot    order / LOWESS
     │
     ↓
 Residual Analysis
     │
     ↓
 ML Regression
```

---

# 🎯 M10 Practice Tasks

### Beginner

**Task 1**

`total_bill` এবং `tip` দিয়ে `regplot()` তৈরি করো।

**Task 2**

Regression line ছাড়া এবং regression line সহ দুইটি plot compare করো।

**Task 3**

`ci=None` ব্যবহার করে দেখো।

**Task 4**

`scatter_kws={"alpha": 0.5}` ব্যবহার করো।

---

### Intermediate

**Task 5**

`lmplot()` ব্যবহার করে `sex` অনুযায়ী regression compare করো।

**Task 6**

`time` অনুযায়ী separate regression plot বানাও।

**Task 7**

`hue="sex"` এবং `col="time"` একসাথে ব্যবহার করো।

**Task 8**

`residplot()` তৈরি করো এবং residual pattern explain করো।

---

### Advanced ⭐

**Task 9**

একটি artificial curved dataset তৈরি করে:

```text
order=1
order=2
order=3
```

compare করো।

**Task 10**

একটি dataset নিয়ে এই workflow সম্পূর্ণ করো:

```text
Correlation
    ↓
Scatterplot
    ↓
Regression Plot
    ↓
Residual Plot
    ↓
Outlier Analysis
    ↓
Conclusion
```

---

# ✅ M10 Completion Checklist

M10 complete হয়েছে ধরে নেবে যখন তুমি explanation ছাড়া করতে পারবে:

* [ ] `sns.regplot()`
* [ ] Regression line explain
* [ ] Positive/negative relationship
* [ ] Confidence interval
* [ ] `ci`
* [ ] `scatter_kws`
* [ ] `line_kws`
* [ ] `sns.lmplot()`
* [ ] `hue`
* [ ] `row`
* [ ] `col`
* [ ] `order`
* [ ] Polynomial regression visualization
* [ ] `lowess=True`
* [ ] Residual কী
* [ ] `sns.residplot()`
* [ ] Heteroscedasticity-এর basic ধারণা
* [ ] Outlier-এর regression-এর উপর effect
* [ ] Correlation + regression visualization
* [ ] EDA → ML regression workflow

### ⭐ Final takeaway

```text
M08 → Correlation
          ↓
M09 → Pairplot / Jointplot
          ↓
M10 → Regression Plot
          ↓
       Trend
          ↓
   Linear / Non-linear
          ↓
      Residual
          ↓
   Outlier Analysis
          ↓
   ML Regression
```

**পরবর্তী: M11 — Categorical Data Visualization Deep Dive** — `countplot`, `barplot`, `pointplot`, `catplot`, category ordering, percentage analysis, grouped comparison এবং categorical EDA workflow আরও গভীরভাবে।


---
# 📊 Seaborn M11 — Categorical Data Visualization Deep Dive

M10 পর্যন্ত আমরা numerical relationship, regression, residual ইত্যাদি দেখেছি। এখন M11-এ আমরা **categorical data analysis** আরও গভীরভাবে শিখব।

```text
M08 → Heatmap & Correlation
M09 → Pairplot & Jointplot
M10 → Regression & Relationship
M11 → Categorical Data Visualization ⭐
```

M11-এর মূল লক্ষ্য:

```text
Categorical Data
      ↓
Count
      ↓
Mean / Median / Sum
      ↓
Category Comparison
      ↓
Percentage
      ↓
Grouped Analysis
      ↓
EDA
      ↓
ML Feature Understanding
```

---

# 1. Categorical Data কী?

যে data সাধারণত কোনো **group/category/label** প্রকাশ করে তাকে categorical data বলা হয়।

`tips` dataset-এ:

```python
df = sns.load_dataset("tips")
```

Categorical columns:

```text
sex
smoker
day
time
```

Numerical columns:

```text
total_bill
tip
size
```

উদাহরণ:

```text
sex:

Male
Female
Male
Male
Female
```

এখানে `Male` / `Female` হলো categories।

---

# 2. Categorical Visualization কেন গুরুত্বপূর্ণ?

ধরো তোমার dataset:

```text
customer_type
sales
```

তুমি জানতে চাও:

> কোন customer category সবচেয়ে বেশি?

অথবা:

> কোন category-এর average sales বেশি?

অথবা:

> কোন class-এর observation সবচেয়ে কম?

এগুলোর জন্য categorical plots খুব useful।

---

# 3. Countplot ⭐

`countplot()` কোনো category-তে **কতগুলো observation আছে** সেটা দেখায়।

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

sns.countplot(
    data=df,
    x="sex"
)

plt.show()
```

Concept:

```text
Male      █████████████
Female    ████████
```

অর্থাৎ এটি frequency/count দেখাচ্ছে।

---

# 4. `countplot()` কীভাবে কাজ করে?

ধরো:

```text
sex
----
Male
Male
Female
Male
Female
```

Count:

```text
Male   → 3
Female → 2
```

Countplot:

```text
Male      ███
Female    ██
```

---

# 5. Vertical Countplot

```python
sns.countplot(
    data=df,
    x="day"
)

plt.show()
```

এখানে:

```text
Thu
Fri
Sat
Sun
```

প্রতিটি দিনের observation count দেখা যাবে।

---

# 6. Horizontal Countplot

```python
sns.countplot(
    data=df,
    y="day"
)

plt.show()
```

এটি অনেক category থাকলে readable হতে পারে।

---

# 7. `hue` ⭐

Category-এর ভিতরে আরেকটি category compare করতে:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.show()
```

এখন:

```text
        Male    Female

Thu      ███      ██
Fri      ██       ██
Sat      █████    ███
Sun      ████     ███
```

এটি **grouped categorical analysis**।

---

# 8. `hue` কেন গুরুত্বপূর্ণ?

শুধু:

```python
sns.countplot(data=df, x="day")
```

বলবে:

> কোন দিনে কত observations?

কিন্তু:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex"
)
```

বলবে:

> কোন দিনে male/female observation কত?

অর্থাৎ একটি additional dimension পাওয়া যায়।

---

# 9. `order`

Category-এর order নিজে নির্ধারণ করা যায়।

```python
sns.countplot(
    data=df,
    x="day",
    order=["Thur", "Fri", "Sat", "Sun"]
)

plt.show()
```

এটি useful যখন category-এর natural order আছে।

---

# 10. Frequency অনুযায়ী Sorting

প্রথমে:

```python
order = (
    df["day"]
    .value_counts()
    .index
)
```

তারপর:

```python
sns.countplot(
    data=df,
    x="day",
    order=order
)

plt.show()
```

এখন সবচেয়ে বেশি count থেকে কম count অনুযায়ী category সাজানো যাবে।

---

# 11. `value_counts()` বনাম `countplot()`

Pandas:

```python
print(df["day"].value_counts())
```

Visualization:

```python
sns.countplot(
    data=df,
    x="day"
)
```

অর্থাৎ:

```text
value_counts()
     ↓
Numerical summary

countplot()
     ↓
Visual summary
```

দুটো একসাথে ব্যবহার করা খুব ভালো EDA practice।

---

# 12. Barplot কী?

`barplot()` সাধারণত category অনুযায়ী কোনো **numerical variable-এর aggregated value** দেখায়।

উদাহরণ:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এখানে প্রতিটি day's **average total_bill** সাধারণত দেখানো হয়।

---

# 13. Countplot বনাম Barplot ⭐

এটি খুব গুরুত্বপূর্ণ।

### Countplot

```python
sns.countplot(
    data=df,
    x="day"
)
```

প্রশ্ন:

> কতগুলো observation?

### Barplot

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

প্রশ্ন:

> প্রতিটি category-এর numerical value-এর average কত?

সহজভাবে:

```text
countplot → COUNT

barplot   → AGGREGATED NUMERICAL VALUE
```

---

# 14. Barplot-এর Default Aggregation

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

সাধারণভাবে এখানে:

$$
Mean(total\_bill)
$$

দেখানো হয়।

অর্থাৎ:

```text
Thursday → average bill
Friday   → average bill
Saturday → average bill
Sunday   → average bill
```

---

# 15. `estimator`

Barplot-এর aggregation function পরিবর্তন করা যায়।

### Mean

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="mean"
)
```

### Median

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="median"
)
```

এতে median comparison হবে।

---

# 16. Sum

Total value দেখতে:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    estimator="sum",
    errorbar=None
)

plt.show()
```

এখন প্রতিটি day's total bill-এর aggregate দেখা যাবে।

---

# 17. `errorbar`

Barplot-এ bar-এর সাথে uncertainty/error information থাকতে পারে।

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Error bar দেখে estimate-এর uncertainty সম্পর্কে ধারণা পাওয়া যায়।

Errorbar বন্ধ:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar=None
)
```

---

# 18. Standard Deviation

Variation দেখাতে:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar="sd"
)

plt.show()
```

এখানে bar-এর চারপাশে standard deviation-based error information থাকবে।

---

# 19. Bootstrap Confidence Interval

Barplot-এর uncertainty estimate bootstrap-এর মাধ্যমেও হতে পারে।

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    errorbar=("ci", 95)
)

plt.show()
```

এখানে confidence interval concept ব্যবহার করা হয়।

---

# 20. `hue` দিয়ে Barplot

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

এখন:

```text
Day
 ↓
Male average bill
Female average bill
```

compare করা যাবে।

---

# 21. Countplot + Barplot Together

EDA-তে খুব useful combination:

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

sns.countplot(
    data=df,
    x="day",
    ax=axes[0]
)

sns.barplot(
    data=df,
    x="day",
    y="total_bill",
    ax=axes[1]
)

plt.tight_layout()
plt.show()
```

এখানে:

```text
Plot 1 → How many?
Plot 2 → Average value?
```

---

# 22. Category Frequency বনাম Category Value

ধরো:

```text
Category A → 100 customers
Category B → 20 customers
```

কিন্তু:

```text
Category A → average sales = $10
Category B → average sales = $100
```

তাহলে শুধু countplot দেখলে ভুল conclusion হতে পারে।

তাই:

```text
Count
+
Numerical Aggregation
```

দুটোই দেখা দরকার।

---

# 23. Percentage Analysis ⭐

Countplot count দেখায়।

কিন্তু percentage আরও useful হতে পারে।

```python
percentage = (
    df["day"]
    .value_counts(normalize=True)
    .mul(100)
)

print(percentage)
```

উদাহরণ:

```text
Sat → 35%
Sun → 32%
Thur → 25%
Fri → 8%
```

---

# 24. Percentage Barplot

```python
percentage = (
    df["day"]
    .value_counts(normalize=True)
    .mul(100)
    .reset_index()
)

percentage.columns = [
    "day",
    "percentage"
]

sns.barplot(
    data=percentage,
    x="day",
    y="percentage"
)

plt.ylabel("Percentage (%)")
plt.show()
```

---

# 25. Grouped Percentage

ধরো তুমি দেখতে চাও:

> প্রতিটি day-তে male/female proportion কেমন?

Pandas দিয়ে:

```python
grouped = pd.crosstab(
    df["day"],
    df["sex"],
    normalize="index"
) * 100

print(grouped)
```

এখন:

```text
day      Male    Female
Thur      55       45
Fri       60       40
Sat       65       35
Sun       58       42
```

---

# 26. Crosstab + Heatmap

M08-এর heatmap-এর সাথে combine করা যায়:

```python
grouped = pd.crosstab(
    df["day"],
    df["sex"],
    normalize="index"
) * 100

sns.heatmap(
    grouped,
    annot=True,
    fmt=".1f"
)

plt.show()
```

এটি categorical percentage analysis-এর জন্য excellent।

---

# 27. `catplot()` ⭐

Seaborn-এর `catplot()` হলো categorical plots-এর একটি **figure-level interface**।

এটি ব্যবহার করে বিভিন্ন categorical plot তৈরি করা যায়।

Basic:

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Default categorical relationship plot সাধারণত strip-style হতে পারে।

---

# 28. `catplot(kind="bar")`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="bar"
)

plt.show()
```

এটি barplot-এর figure-level version হিসেবে ভাবতে পারো।

---

# 29. `catplot(kind="box")`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="box"
)

plt.show()
```

এটি boxplot তৈরি করবে।

---

# 30. `catplot(kind="violin")`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="violin"
)

plt.show()
```

---

# 31. `catplot(kind="strip")`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="strip"
)

plt.show()
```

---

# 32. `catplot(kind="swarm")`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="swarm"
)

plt.show()
```

এভাবে `catplot()` অনেক categorical visualization-এর unified interface দেয়।

---

# 33. `catplot()` + `col`

এখানে `catplot()` খুব powerful।

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="box",
    col="time"
)

plt.show()
```

তাহলে:

```text
Lunch                  Dinner
────────────           ────────────
Thu                    Thu
Fri                    Fri
Sat                    Sat
Sun                    Sun
```

আলাদা panel-এ analysis করা যাবে।

---

# 34. `catplot()` + `row`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="box",
    row="smoker"
)

plt.show()
```

এখন:

```text
Smoker = Yes
Smoker = No
```

আলাদা panel।

---

# 35. `catplot()` + `hue`

```python
sns.catplot(
    data=df,
    x="day",
    y="total_bill",
    kind="bar",
    hue="sex"
)

plt.show()
```

---

# 36. Pointplot ⭐

`pointplot()` category অনুযায়ী numerical estimate-এর point এবং uncertainty দেখায়।

```python
sns.pointplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

Concept:

```text
Day

Thu       ●
Fri          ●
Sat      ●
Sun           ●
```

Line দিয়ে trend দেখা যায়।

---

# 37. Pointplot + Hue

```python
sns.pointplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.show()
```

Male/Female-এর average trend compare করা যায়।

---

# 38. Pointplot কখন ব্যবহার করবে?

যখন তোমার মূল প্রশ্ন:

> Category পরিবর্তনের সাথে average numerical value-এর trend কীভাবে পরিবর্তন হচ্ছে?

তখন pointplot useful।

বিশেষ করে অনেক category থাকলে barplot-এর চেয়ে pointplot cleaner হতে পারে।

---

# 39. Countplot বনাম Barplot বনাম Pointplot

| Plot       | কী দেখায়                                     |
| ---------- | -------------------------------------------- |
| Countplot  | Number of observations                       |
| Barplot    | Aggregated numerical value                   |
| Pointplot  | Aggregated value + trend                     |
| Boxplot    | Distribution + median + spread               |
| Violinplot | Distribution shape                           |
| Stripplot  | Individual observations                      |
| Swarmplot  | Individual observations without much overlap |

---

# 40. একটি গুরুত্বপূর্ণ EDA Question Framework

Categorical data দেখার সময় নিজেকে প্রশ্ন করবে:

```text
1. কোন category সবচেয়ে বেশি?
2. কোন category সবচেয়ে কম?
3. Category distribution balanced?
4. Category অনুযায়ী average value কী?
5. Median কি average-এর থেকে আলাদা?
6. Outlier আছে?
7. Category-এর মধ্যে numerical distribution কেমন?
8. Category এবং target-এর relationship কী?
9. কোনো category খুব rare?
10. ML-এর জন্য category encoding কীভাবে করব?
```

---

# 41. ML-এ Categorical Data

ধরো:

```text
gender
city
education
occupation
```

এগুলো সরাসরি বেশিরভাগ ML model-এ numerical input হিসেবে দেওয়া যায় না।

তাই encoding করতে হয়:

```text
Categorical Data
      ↓
Encoding
      ↓
Numerical Representation
      ↓
ML Model
```

Common methods:

```text
One-Hot Encoding
Label Encoding
Ordinal Encoding
Target Encoding
```

M11-এর লক্ষ্য encoding শেখানো নয়; visualization দিয়ে category বুঝে নেওয়া।

---

# 42. Class Imbalance ⭐

Classification dataset-এ:

```text
Normal      95,000
Suspicious   5,000
```

এটি imbalance।

Countplot:

```python
sns.countplot(
    data=df,
    x="target"
)

plt.show()
```

এখানে immediately বুঝতে পারবে class distribution balanced কি না।

তোমার AI CCTV project-এর মতো classification problem-এ এটি খুব important।

---

# 43. Class Distribution Percentage

```python
print(
    df["target"]
    .value_counts(normalize=True)
    * 100
)
```

উদাহরণ:

```text
Normal       95%
Suspicious    5%
```

এখন শুধু accuracy দেখে model evaluate করা বিপজ্জনক হতে পারে।

---

# 44. Category + Target Analysis

ধরো:

```text
day
target
```

তাহলে:

```python
sns.countplot(
    data=df,
    x="day",
    hue="target"
)

plt.show()
```

এতে category-wise target distribution দেখা যাবে।

---

# 45. Category + Numerical Target

ধরো:

```text
day
total_bill
```

তাহলে:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.show()
```

এতে শুধু average নয়, distribution-ও দেখতে পারবে।

---

# 46. Best Practice: শুধু Barplot ব্যবহার করো না

ধরো:

```python
sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)
```

এতে average দেখবে।

কিন্তু distribution দেখতে:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)
```

আর individual points দেখতে:

```python
sns.stripplot(
    data=df,
    x="day",
    y="total_bill",
    alpha=0.5
)
```

তাই:

```text
Barplot
   ↓
Average

Boxplot
   ↓
Distribution

Stripplot
   ↓
Actual observations
```

---

# 47. Professional Categorical EDA Workflow ⭐

```text
Categorical Column
        ↓
value_counts()
        ↓
Countplot
        ↓
Percentage
        ↓
Numerical Variable?
        ↓
Barplot / Boxplot / Violinplot
        ↓
hue
        ↓
Group comparison
        ↓
Target relationship
        ↓
ML feature analysis
```

---

# 48. Complete M11 Example

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

# -------------------------
# 1. Category frequency
# -------------------------

print(df["day"].value_counts())

sns.countplot(
    data=df,
    x="day",
    order=df["day"].value_counts().index
)

plt.title("Number of Observations by Day")
plt.show()


# -------------------------
# 2. Category + Sex
# -------------------------

sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.title("Day-wise Sex Distribution")
plt.show()


# -------------------------
# 3. Average bill
# -------------------------

sns.barplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Average Total Bill by Day")
plt.show()


# -------------------------
# 4. Distribution
# -------------------------

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Total Bill Distribution by Day")
plt.show()


# -------------------------
# 5. Point comparison
# -------------------------

sns.pointplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)

plt.title("Average Bill Trend")
plt.show()
```

---

# 49. M11-এর সবচেয়ে গুরুত্বপূর্ণ Difference

এটা memorize করো:

```text
COUNT
 ↓
countplot()
 ↓
"How many?"

AVERAGE / AGGREGATE
 ↓
barplot()
 ↓
"How much?"

TREND OF AGGREGATE
 ↓
pointplot()
 ↓
"How does it change?"

DISTRIBUTION
 ↓
boxplot / violinplot
 ↓
"How is the data distributed?"

INDIVIDUAL DATA
 ↓
stripplot / swarmplot
 ↓
"What do actual observations look like?"
```

---

# 🎯 M11 Practice Tasks

## Beginner

### Task 1

`tips` dataset-এর `sex` দিয়ে countplot বানাও।

### Task 2

`day` দিয়ে countplot বানাও।

### Task 3

`smoker` দিয়ে countplot বানাও।

### Task 4

`day` + `sex` দিয়ে `hue` ব্যবহার করো।

### Task 5

`day`-কে frequency অনুযায়ী sort করো।

---

## Intermediate

### Task 6

`day` অনুযায়ী average `tip`:

```python
sns.barplot(
    data=df,
    x="day",
    y="tip"
)
```

তৈরি করো।

### Task 7

Average-এর বদলে median দেখাও।

### Task 8

`day + sex + total_bill` grouped barplot তৈরি করো।

### Task 9

`day + total_bill`-এর boxplot তৈরি করে barplot-এর সাথে compare করো।

### Task 10

Percentage calculation করো:

```text
sex
smoker
day
time
```

---

# 🔥 Advanced Practice

### Task 11 — Class Imbalance

নিজের কোনো classification dataset load করো।

```python
sns.countplot(
    data=df,
    x="target"
)
```

তারপর percentage বের করো।

---

### Task 12 — Category vs Target

```text
categorical_feature
        ↓
target
```

দিয়ে `hue="target"` ব্যবহার করে countplot বানাও।

---

### Task 13 — Category vs Numerical Feature

একটি categorical feature এবং numerical feature নির্বাচন করো।

তারপর:

```text
Countplot
Barplot
Boxplot
Violinplot
```

চারটি plot বানিয়ে difference explain করো।

---

### Task 14 — `catplot()`

একই data-এর জন্য:

```text
kind="bar"
kind="box"
kind="violin"
kind="strip"
kind="swarm"
```

তৈরি করে compare করো।

---

# 🧪 M11 Mini Project

`tips` dataset দিয়ে একটি **Categorical EDA Report** তৈরি করো।

### Part 1 — Frequency

```text
sex
smoker
day
time
```

এর count বের করো।

### Part 2 — Percentage

প্রতিটি category-এর percentage বের করো।

### Part 3 — Numerical Comparison

প্রতিটি `day`-এর:

```text
average total_bill
median total_bill
average tip
```

বের করো।

### Part 4 — Visualization

তৈরি করো:

```text
1. Countplot
2. Grouped Countplot
3. Barplot
4. Boxplot
5. Violinplot
6. Pointplot
```

### Part 5 — Conclusion

এই প্রশ্নগুলোর উত্তর দাও:

```text
1. কোন category সবচেয়ে বেশি?
2. কোন category সবচেয়ে কম?
3. Data balanced কি?
4. কোন category-এর average bill বেশি?
5. Average বনাম median-এর মধ্যে বড় difference আছে?
6. কোন category-তে বেশি variation?
7. Outlier কোথায়?
8. Sex অনুযায়ী category distribution পরিবর্তন হচ্ছে?
9. কোন visualization সবচেয়ে useful মনে হয়েছে এবং কেন?
```

---

# ✅ M11 Completion Checklist

M11 complete হলে তুমি এগুলো explanation ছাড়াই করতে পারবে:

* [ ] Categorical vs numerical data
* [ ] `countplot()`
* [ ] `hue`
* [ ] `order`
* [ ] `value_counts()`
* [ ] Frequency analysis
* [ ] Percentage analysis
* [ ] `barplot()`
* [ ] `estimator`
* [ ] mean
* [ ] median
* [ ] sum
* [ ] `errorbar`
* [ ] `pointplot()`
* [ ] `catplot()`
* [ ] `kind`
* [ ] `row`
* [ ] `col`
* [ ] Group comparison
* [ ] Class imbalance
* [ ] Category vs target
* [ ] Category vs numerical feature
* [ ] Categorical EDA workflow

---

# 🧠 M11 Final Mental Model

```text
              CATEGORICAL DATA
                     │
        ┌────────────┼────────────┐
        ↓            ↓            ↓
      COUNT       NUMERICAL      TARGET
        │            │            │
        ↓            ↓            ↓
  countplot       barplot      countplot
        │         boxplot         │
        │        violinplot       │
        │        pointplot        │
        └────────────┼────────────┘
                     ↓
               GROUP ANALYSIS
                     ↓
              EDA UNDERSTANDING
                     ↓
             ML PREPROCESSING
```

### 🔥 M08 → M11 একসাথে

```text
M08
Correlation
   ↓
Numerical Relationship

M09
Pairplot / Jointplot
   ↓
Multi-feature Relationship

M10
Regression / Residual
   ↓
Relationship + Trend

M11
Categorical Visualization
   ↓
Category + Group + Target
```

এরপর **M12 — FacetGrid, PairGrid & Advanced Multi-Plot Layouts** শেখা হবে। এখানে `row`, `col`, `hue`, `FacetGrid`, `PairGrid` ব্যবহার করে বড় dataset-কে systematicভাবে বিভিন্ন group-এ ভেঙে analysis করা শিখবে।


---
# 📊 Seaborn M12 — FacetGrid, PairGrid & Advanced Multi-Plot Layouts

M11-এ আমরা categorical data visualization শিখেছি। এখন M12-এ Seaborn-এর **multi-dimensional visualization** শিখব।

এখানে মূল idea হলো—একটা বড় dataset-কে বিভিন্ন category/group অনুযায়ী ছোট ছোট plot-এ ভাগ করে একই analysis করা।

```text
M08 → Heatmap & Correlation
M09 → Pairplot & Jointplot
M10 → Regression & Relationship
M11 → Categorical Visualization
M12 → FacetGrid & PairGrid ⭐
```

---

# 1. কেন Facet দরকার?

ধরো `tips` dataset-এ তুমি দেখতে চাও:

```text
total_bill → tip
```

সাধারণভাবে:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)
```

কিন্তু তুমি যদি জানতে চাও:

> Lunch এবং Dinner-এ relationship কি একই?

তাহলে একটি plot-এ সব data না রেখে:

```text
Lunch
────────────
● ● ● ●
 ● ● ●


Dinner
────────────
● ● ● ●
  ● ● ●
```

আলাদা plot তৈরি করা বেশি useful।

এটাই **faceting**।

---

# 2. Facet কী?

সহজ ভাষায়:

> একটি dataset-কে কোনো categorical variable অনুযায়ী বিভিন্ন ছোট plot-এ ভাগ করাকে faceting বলা যায়।

```text
Dataset
   ↓
Category
   ↓
Multiple subsets
   ↓
Multiple plots
```

উদাহরণ:

```text
time = Lunch / Dinner
```

তাহলে:

```text
Lunch Plot
Dinner Plot
```

---

# 3. FacetGrid কী?

Seaborn-এর:

```python
sns.FacetGrid()
```

একটি grid তৈরি করে, যেখানে একই ধরনের visualization বিভিন্ন subset-এর জন্য তৈরি করা যায়।

Basic:

```python
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

Concept:

```text
              time

      Lunch              Dinner
   ┌───────────┐       ┌───────────┐
   │ ●         │       │     ●     │
   │   ● ●     │       │  ● ●      │
   │ ●    ●    │       │ ●    ●    │
   └───────────┘       └───────────┘
```

---

# 4. `col` — Column-wise Faceting ⭐

সবচেয়ে গুরুত্বপূর্ণ parameter:

```python
col="time"
```

মানে:

```text
time-এর প্রতিটি category
        ↓
একটি আলাদা column/plot
```

Example:

```python
g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

---

# 5. `row` — Row-wise Faceting

এবার:

```python
g = sns.FacetGrid(
    df,
    row="time"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

এখন:

```text
Lunch
────────────
● ●
 ● ●

Dinner
────────────
● ●
  ● ●
```

---

# 6. `row + col` ⭐

এটাই FacetGrid-এর সবচেয়ে powerful feature।

ধরো:

```text
row = smoker
col = time
```

তাহলে:

```python
g = sns.FacetGrid(
    df,
    row="smoker",
    col="time"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

Grid:

```text
                 Lunch          Dinner
              ┌──────────┐   ┌──────────┐
Smoker = No   │ ● ●      │   │ ● ●      │
              │   ●      │   │  ● ●     │
              └──────────┘   └──────────┘

Smoker = Yes  ┌──────────┐   ┌──────────┐
              │ ●  ●     │   │ ● ●      │
              │   ● ●    │   │   ●      │
              └──────────┘   └──────────┘
```

এখানে একই relationship চারটি subgroup-এ compare করা হচ্ছে।

---

# 7. `hue`

Color দিয়ে আরেকটি categorical dimension যোগ করা যায়।

```python
g = sns.FacetGrid(
    df,
    col="time",
    hue="sex"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

g.add_legend()

plt.show()
```

এখন:

```text
time → Separate plots
sex  → Different colors
```

---

# 8. FacetGrid-এর Mental Model

এটা মনে রাখো:

```text
FacetGrid
│
├── row  → rows
├── col  → columns
└── hue  → colors
```

অর্থাৎ:

```text
row + col + hue
       ↓
3-dimensional categorical grouping
```

---

# 9. `map()` কী করে?

এই code:

```python
g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)
```

এর অর্থ:

> FacetGrid-এর প্রতিটি subset-এর উপর `scatterplot()` apply করো।

Conceptually:

```text
FacetGrid
    ↓
Lunch data → scatterplot()
Dinner data → scatterplot()
```

---

# 10. Histogram দিয়ে FacetGrid

শুধু scatterplot নয়।

```python
g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.histplot,
    "total_bill"
)

plt.show()
```

এখন Lunch এবং Dinner-এর `total_bill` distribution compare করা যাবে।

---

# 11. KDE দিয়ে FacetGrid

```python
g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.kdeplot,
    "total_bill"
)

plt.show()
```

এতে smooth distribution compare করা যায়।

---

# 12. Boxplot-এর সাথে FacetGrid

```python
g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.boxplot,
    y=df["total_bill"]
)

plt.show()
```

তবে modern Seaborn workflow-এ categorical faceting-এর জন্য `catplot()` অনেক সহজ। তাই FacetGrid শেখার উদ্দেশ্য হলো **custom multi-plot architecture** বোঝা।

---

# 13. `height`

প্রতিটি facet-এর size:

```python
g = sns.FacetGrid(
    df,
    col="time",
    height=4
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

---

# 14. `aspect`

Width/height ratio:

```python
g = sns.FacetGrid(
    df,
    col="time",
    height=4,
    aspect=1.2
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

---

# 15. `col_wrap`

অনেক category থাকলে সব plot এক row-তে রাখা inconvenient হতে পারে।

```python
g = sns.FacetGrid(
    df,
    col="day",
    col_wrap=2
)

g.map(
    sns.histplot,
    "total_bill"
)

plt.show()
```

ধরো 4 categories:

```text
Thu      Fri
──────────────
Sat      Sun
```

`col_wrap=2` হওয়ার কারণে প্রতি row-তে 2টি plot।

---

# 16. `margin_titles`

Row/column title আরও readable করার জন্য:

```python
g = sns.FacetGrid(
    df,
    row="smoker",
    col="time",
    margin_titles=True
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

plt.show()
```

---

# 17. `set_axis_labels()`

Axis label:

```python
g.set_axis_labels(
    "Total Bill",
    "Tip"
)
```

Full:

```python
g = sns.FacetGrid(
    df,
    col="time"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

g.set_axis_labels(
    "Total Bill",
    "Tip"
)

plt.show()
```

---

# 18. `set_titles()`

Facet title customize:

```python
g.set_titles(
    "{col_name} Time"
)
```

যেমন:

```text
Lunch Time
Dinner Time
```

---

# 19. `add_legend()`

যদি `hue` ব্যবহার করো:

```python
g.add_legend()
```

Example:

```python
g = sns.FacetGrid(
    df,
    col="time",
    hue="sex"
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

g.add_legend()

plt.show()
```

---

# 20. FacetGrid + Regression

এখানে M10-এর concept ব্যবহার করতে পারো।

```python
g = sns.FacetGrid(
    df,
    col="time",
    hue="sex"
)

g.map(
    sns.regplot,
    "total_bill",
    "tip"
)

g.add_legend()

plt.show()
```

Concept:

```text
Lunch
Male   → regression
Female → regression

Dinner
Male   → regression
Female → regression
```

এটি group-wise relationship analysis-এর জন্য খুব powerful।

---

# 21. `lmplot()` বনাম FacetGrid

M10-এ `lmplot()` দেখেছিলে।

যেমন:

```python
sns.lmplot(
    data=df,
    x="total_bill",
    y="tip",
    row="smoker",
    col="time",
    hue="sex"
)
```

এটি internally faceting-এর concept ব্যবহার করে।

তাই:

```text
lmplot
   ↓
Convenient high-level interface

FacetGrid
   ↓
More manual/custom control
```

---

# 22. PairGrid কী?

এবার আসি `PairGrid()`-এ।

`pairplot()` আমরা M09-এ শিখেছি।

`PairGrid()` হলো তার **more customizable / lower-level framework**।

Basic:

```python
g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ]
)

g.map(
    sns.scatterplot
)

plt.show()
```

এটি pairplot-এর মতো matrix তৈরি করবে।

---

# 23. Pairplot বনাম PairGrid ⭐

### Pairplot

```python
sns.pairplot(df)
```

সহজ এবং দ্রুত।

### PairGrid

```python
g = sns.PairGrid(df)
g.map(sns.scatterplot)
```

আরও control।

সহজভাবে:

```text
pairplot → Ready-made

PairGrid → Build your own pairwise visualization
```

---

# 24. PairGrid-এর Structure

ধরো তিনটি features:

```text
A
B
C
```

Grid:

```text
        A        B        C

A       ?        ?        ?

B       ?        ?        ?

C       ?        ?        ?
```

তুমি চাইলে:

```text
Diagonal → KDE
Upper    → Regression
Lower    → Scatter
```

এই ধরনের custom design করতে পারো।

---

# 25. `map()`

সব cell একই plot:

```python
g = sns.PairGrid(
    df,
    vars=["total_bill", "tip", "size"]
)

g.map(
    sns.scatterplot
)

plt.show()
```

---

# 26. `map_diag()`

Diagonal-এর plot আলাদা করতে:

```python
g = sns.PairGrid(
    df,
    vars=["total_bill", "tip", "size"]
)

g.map_diag(
    sns.histplot
)

plt.show()
```

অর্থ:

```text
Diagonal → histogram
```

---

# 27. `map_offdiag()`

Diagonal ছাড়া বাকি cells:

```python
g.map_offdiag(
    sns.scatterplot
)
```

Complete:

```python
g = sns.PairGrid(
    df,
    vars=["total_bill", "tip", "size"]
)

g.map_diag(
    sns.histplot
)

g.map_offdiag(
    sns.scatterplot
)

plt.show()
```

---

# 28. `map_upper()` এবং `map_lower()` ⭐

আরও advanced control:

```python
g = sns.PairGrid(
    df,
    vars=["total_bill", "tip", "size"]
)

g.map_upper(
    sns.scatterplot
)

g.map_lower(
    sns.regplot
)

g.map_diag(
    sns.histplot
)

plt.show()
```

Concept:

```text
Diagonal
   ↓
Histogram

Upper Triangle
   ↓
Scatter

Lower Triangle
   ↓
Regression
```

---

# 29. কেন এটা useful?

একই information বারবার দেখানোর দরকার নেই।

কারণ:

```text
A vs B
B vs A
```

একই relationship।

তাই:

```text
Upper → Scatter
Lower → Regression
```

দিলে দুই ধরনের analysis একসাথে পাওয়া যায়।

---

# 30. PairGrid + Hue

```python
g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ],
    hue="sex"
)

g.map(
    sns.scatterplot
)

g.add_legend()

plt.show()
```

---

# 31. PairGrid + Different Diagonal

```python
g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ],
    hue="sex"
)

g.map_diag(
    sns.histplot
)

g.map_offdiag(
    sns.scatterplot
)

g.add_legend()

plt.show()
```

এটি খুব useful custom pairwise EDA।

---

# 32. `corner=True` Concept

PairGrid-এও শুধু lower triangle ব্যবহার করা যায়:

```python
g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ],
    corner=True
)

g.map_lower(
    sns.scatterplot
)

g.map_diag(
    sns.histplot
)

plt.show()
```

---

# 33. PairGrid + Regression

```python
g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ]
)

g.map_upper(
    sns.scatterplot
)

g.map_lower(
    sns.regplot
)

g.map_diag(
    sns.histplot
)

plt.show()
```

এখন একই matrix-এ:

```text
Upper  → Raw relationship
Lower  → Regression trend
Diagonal → Distribution
```

---

# 34. FacetGrid বনাম PairGrid ⭐

এটি খুব গুরুত্বপূর্ণ।

| FacetGrid               | PairGrid                              |
| ----------------------- | ------------------------------------- |
| Dataset groups compare  | Feature pairs compare                 |
| `row`, `col`, `hue`     | Multiple feature matrix               |
| Same plot across groups | Different plots across matrix regions |
| Categorical grouping    | Numerical feature relationship        |
| Group-wise EDA          | Pairwise EDA                          |

সহজভাবে:

```text
FacetGrid
↓
"Same analysis for different groups"

PairGrid
↓
"Different analysis for different feature pairs"
```

---

# 35. FacetGrid Example — ML

ধরো:

```text
features:
age
income

group:
education
```

তুমি:

```python
g = sns.FacetGrid(
    df,
    col="education"
)

g.map(
    sns.scatterplot,
    "age",
    "income"
)

plt.show()
```

এখন education group অনুযায়ী:

```text
Age ↔ Income
```

relationship compare করতে পারবে।

---

# 36. PairGrid Example — ML

ধরো:

```text
age
income
experience
score
```

তুমি:

```python
g = sns.PairGrid(
    df,
    vars=[
        "age",
        "income",
        "experience",
        "score"
    ]
)

g.map(
    sns.scatterplot
)

plt.show()
```

এখানে সব numerical feature-এর pairwise relationship পাওয়া যাবে।

---

# 37. Classification Dataset-এ FacetGrid

ধরো:

```text
target
gender
```

তুমি দেখতে চাও:

> Gender অনুযায়ী feature relationship কেমন?

```python
g = sns.FacetGrid(
    df,
    col="gender",
    hue="target"
)

g.map(
    sns.scatterplot,
    "feature1",
    "feature2"
)

g.add_legend()

plt.show()
```

এতে class separation group-wise দেখতে পারবে।

---

# 38. AI CCTV Dataset-এর ক্ষেত্রে Connection ⭐

তোমার suspicious detection dataset-এর মতো dataset-এ ধরো features:

```text
motion_score
brightness
person_count
duration
target
```

তাহলে PairGrid:

```python
g = sns.PairGrid(
    df,
    vars=[
        "motion_score",
        "brightness",
        "person_count",
        "duration"
    ],
    hue="target"
)

g.map_diag(
    sns.histplot
)

g.map_offdiag(
    sns.scatterplot
)

g.add_legend()

plt.show()
```

এতে তুমি investigate করতে পারবে:

```text
Normal vs Suspicious
        ↓
Feature Distribution
        ↓
Feature Relationship
        ↓
Class Separation
        ↓
Potentially useful features
```

---

# 39. FacetGrid দিয়ে CCTV Feature Analysis

ধরো:

```text
target = Normal / Suspicious
camera_type = Indoor / Outdoor
```

তাহলে:

```python
g = sns.FacetGrid(
    df,
    col="camera_type",
    hue="target"
)

g.map(
    sns.scatterplot,
    "motion_score",
    "person_count"
)

g.add_legend()

plt.show()
```

এখন Indoor বনাম Outdoor-এ suspicious/normal pattern compare করতে পারবে।

---

# 40. `catplot()` বনাম FacetGrid

M11-এ:

```python
sns.catplot(
    ...
    row=,
    col=,
    hue=
)
```

দেখেছিলে।

`catplot()` categorical plots-এর জন্য high-level interface।

FacetGrid আরও general-purpose।

```text
catplot
 ↓
Categorical visualization

FacetGrid
 ↓
General faceted visualization
```

---

# 41. FacetGrid + Multiple Dimensions

একটি advanced example:

```python
g = sns.FacetGrid(
    df,
    row="smoker",
    col="time",
    hue="sex",
    height=4
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

g.add_legend()

g.set_axis_labels(
    "Total Bill",
    "Tip"
)

plt.show()
```

এখানে simultaneously:

```text
row  → smoker
col  → time
hue  → sex
x    → total_bill
y    → tip
```

একটি plot-এর মধ্যে 5টি dimension effectively analyze করা হচ্ছে।

---

# 42. Advanced EDA Strategy ⭐

একটি বড় dataset-এর ক্ষেত্রে:

### Step 1

Overall relationship:

```python
sns.scatterplot(...)
```

### Step 2

Group-wise:

```python
sns.lmplot(...)
```

### Step 3

Multiple groups:

```python
FacetGrid(...)
```

### Step 4

Multiple numerical features:

```python
PairGrid(...)
```

### Step 5

Strong relationships:

```python
Jointplot(...)
```

অর্থাৎ:

```text
Overall
  ↓
Group
  ↓
Multi-group
  ↓
Multi-feature
  ↓
Deep investigation
```

---

# 43. FacetGrid Cheat Sheet

```python
g = sns.FacetGrid(
    df,
    row="category1",
    col="category2",
    hue="category3"
)

g.map(
    sns.scatterplot,
    "x",
    "y"
)

g.add_legend()
```

Important:

```text
row
col
hue
height
aspect
col_wrap
map()
set_axis_labels()
set_titles()
add_legend()
```

---

# 44. PairGrid Cheat Sheet

```python
g = sns.PairGrid(
    df,
    vars=["A", "B", "C"],
    hue="category"
)

g.map_diag(
    sns.histplot
)

g.map_upper(
    sns.scatterplot
)

g.map_lower(
    sns.regplot
)

g.add_legend()

plt.show()
```

---

# 45. Pairplot বনাম PairGrid

```text
Pairplot
   ↓
Quick EDA
   ↓
Simple
   ↓
Less customization

PairGrid
   ↓
Advanced EDA
   ↓
Custom matrix
   ↓
More control
```

---

# 46. FacetGrid বনাম `lmplot()`

```text
lmplot
   ↓
Regression-specific
   ↓
Easy

FacetGrid
   ↓
General-purpose
   ↓
Custom visualization
```

---

# 47. M12 Professional EDA Template ⭐

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

# ----------------------------
# FacetGrid
# ----------------------------

g = sns.FacetGrid(
    df,
    row="smoker",
    col="time",
    hue="sex",
    height=3.5
)

g.map(
    sns.scatterplot,
    "total_bill",
    "tip"
)

g.add_legend()

g.set_axis_labels(
    "Total Bill",
    "Tip"
)

plt.show()


# ----------------------------
# PairGrid
# ----------------------------

g = sns.PairGrid(
    df,
    vars=[
        "total_bill",
        "tip",
        "size"
    ],
    hue="sex"
)

g.map_diag(
    sns.histplot
)

g.map_upper(
    sns.scatterplot
)

g.map_lower(
    sns.regplot
)

g.add_legend()

plt.show()
```

---

# 🧠 M12 Mental Model

এটাই M12-এর সবচেয়ে important concept:

```text
                         DATASET
                            │
              ┌─────────────┴─────────────┐
              ↓                           ↓
          CATEGORIES                 FEATURES
              │                           │
              ↓                           ↓
          FacetGrid                    PairGrid
              │                           │
       row / col / hue            feature × feature
              │                           │
              ↓                           ↓
       Group Comparison            Relationship
              │                           │
              └─────────────┬─────────────┘
                            ↓
                         EDA
                            ↓
                    ML Feature Analysis
```

---

# 🎯 M12 Practice Tasks

## Beginner

### Task 1

`time` অনুযায়ী FacetGrid তৈরি করো।

```text
Lunch
Dinner
```

প্রতিটির `total_bill` distribution দেখাও।

---

### Task 2

`smoker` অনুযায়ী দুইটি scatterplot তৈরি করো:

```text
total_bill
     vs
tip
```

---

### Task 3

`row="smoker"` এবং `col="time"` ব্যবহার করে 2×2 grid বানাও।

---

### Task 4

`hue="sex"` যোগ করো।

---

### Task 5

`col_wrap=2` দিয়ে `day` অনুযায়ী histogram তৈরি করো।

---

# 🔥 Intermediate

### Task 6

FacetGrid দিয়ে `time` অনুযায়ী regression analysis:

```text
total_bill → tip
```

করো।

---

### Task 7

PairGrid তৈরি করো:

```text
total_bill
tip
size
```

এর জন্য।

---

### Task 8

PairGrid-এ:

```text
Diagonal → histogram
Upper → scatter
Lower → regression
```

করো।

---

### Task 9

PairGrid-এ `hue="sex"` যোগ করো।

---

### Task 10

`pairplot()` এবং custom `PairGrid()` একই dataset-এ তৈরি করে compare করো।

---

# 🚀 Advanced Practice

### Task 11

নিজের ML dataset load করো:

```python
df = pd.read_csv("dataset.csv")
```

তারপর:

```text
FacetGrid:
    row = category1
    col = category2
    hue = target
```

ব্যবহার করো।

---

### Task 12

চারটি numerical feature নিয়ে:

```text
PairGrid

Diagonal → KDE
Upper → Scatter
Lower → Regression
```

বানাও।

---

### Task 13

তোমার classification dataset-এ:

```text
Class 0
Class 1
```

`hue` দিয়ে feature separation investigate করো।

---

# 🧪 M12 Mini Project

একটি dataset নিয়ে এই complete workflow করো:

```text
                 DATASET
                    ↓
            Basic EDA (M02)
                    ↓
         Distribution (M03)
                    ↓
           Box/Violin (M04-05)
                    ↓
       Categorical Analysis (M06-07)
                    ↓
        Correlation (M08)
                    ↓
       Pair/Joint Analysis (M09)
                    ↓
      Regression Analysis (M10)
                    ↓
    Categorical Analysis (M11)
                    ↓
     ┌──────────────┴──────────────┐
     ↓                             ↓
 FacetGrid                      PairGrid
     ↓                             ↓
Group Comparison             Feature Comparison
     └──────────────┬──────────────┘
                    ↓
             EDA Conclusion
```

শেষে report-এ এই প্রশ্নগুলোর উত্তর দাও:

```text
1. কোন category-এর distribution আলাদা?
2. কোন group-এর average বেশি?
3. কোন group-এর relationship strongest?
4. কোন feature pair-এর relationship strongest?
5. Class separation কোথায় ভালো?
6. কোন feature pair-এ non-linear pattern আছে?
7. Outlier কোন group-এ বেশি?
8. Group পরিবর্তনের সাথে relationship পরিবর্তন হচ্ছে কি?
9. কোন features ML model-এর জন্য potentially useful?
```

---

# ✅ M12 Completion Checklist

* [ ] Faceting concept
* [ ] `FacetGrid()`
* [ ] `row`
* [ ] `col`
* [ ] `hue`
* [ ] `map()`
* [ ] `col_wrap`
* [ ] `height`
* [ ] `aspect`
* [ ] `set_axis_labels()`
* [ ] `set_titles()`
* [ ] `add_legend()`
* [ ] Group-wise scatterplot
* [ ] Group-wise histogram
* [ ] Group-wise regression
* [ ] `PairGrid()`
* [ ] `map_diag()`
* [ ] `map_offdiag()`
* [ ] `map_upper()`
* [ ] `map_lower()`
* [ ] PairGrid + hue
* [ ] Pairplot vs PairGrid
* [ ] FacetGrid vs PairGrid
* [ ] Multi-dimensional EDA
* [ ] ML feature analysis

### 🔥 M12-এর মূল পার্থক্য

```text
FacetGrid
    ↓
একই visualization
বিভিন্ন GROUP-এর জন্য

PairGrid
    ↓
বিভিন্ন FEATURE-এর
pairwise relationship
```

পরবর্তী ধাপে **M13 — Seaborn Styling, Themes, Color Palettes & Professional Visualization**: plot সুন্দর করা নয় শুধু—কোন palette কখন ব্যবহার করবে, `set_theme()`, `set_context()`, `set_style()`, `despine()`, custom palette, accessibility এবং publication/dashboard-ready visualization শেখা হবে।

----
# Seaborn M13 — Styling, Themes, Color Palettes & Professional Visualization

M12 পর্যন্ত তুমি **multi-dimensional visualization** শিখেছো। এখন M13-তে আমরা শিখব কীভাবে Seaborn graph-কে **clean, professional, readable এবং presentation/dashboard-ready** করা যায়।

এই lesson-এর পরে তুমি শুধু graph বানাবে না—**কোন graph কীভাবে visually communicate করবে**, সেটাও বুঝতে পারবে।

---

# 1. M13 Learning Goals

M13 শেষে তুমি জানতে পারবে:

```text
Seaborn Visualization
        ↓
Theme
        ↓
Style
        ↓
Context
        ↓
Color Palette
        ↓
Figure Size
        ↓
Labels / Titles
        ↓
Spines
        ↓
Legend
        ↓
Professional Chart
```

Main topics:

1. `sns.set_theme()`
2. `sns.set_style()`
3. `sns.set_context()`
4. `sns.despine()`
5. Color palettes
6. Sequential palettes
7. Diverging palettes
8. Qualitative palettes
9. Custom colors
10. `palette=`
11. `hue`
12. Figure size
13. Titles & labels
14. Tick customization
15. Legend customization
16. Professional visualization
17. Accessibility
18. ML/EDA visualization standards

---

# 2. Dataset Setup

আমরা `tips` dataset ব্যবহার করব।

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("tips")

print(df.head())
```

---

# 3. Why Styling Matters?

ধরো তুমি এই graph বানালে:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Graph technically correct।

কিন্তু professional report-এর জন্য আরও কিছু দরকার:

```text
Correct Data
    +
Good Visualization
    +
Readable Labels
    +
Proper Scale
    +
Good Color
    +
Good Layout
    =
Professional Visualization
```

একজন Data Analyst শুধু graph বানায় না।

সে graph-এর মাধ্যমে **story communicate** করে।

---

# 4. `sns.set_theme()`

Seaborn-এর overall visual theme সেট করার সবচেয়ে convenient method:

```python
sns.set_theme()
```

Example:

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme()

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটি পুরো Seaborn visualization-এর default appearance পরিবর্তন করে।

---

# 5. `sns.set_style()`

Seaborn-এর পাঁচটি গুরুত্বপূর্ণ built-in style:

```text
darkgrid
whitegrid
dark
white
ticks
```

---

## 5.1 darkgrid

```python
sns.set_style("darkgrid")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Background-এর উপর grid থাকবে।

---

## 5.2 whitegrid

```python
sns.set_style("whitegrid")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Data analysis-এর জন্য এটি খুব useful।

---

## 5.3 dark

```python
sns.set_style("dark")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

---

## 5.4 white

```python
sns.set_style("white")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Minimal chart তৈরি করতে ভালো।

---

## 5.5 ticks

```python
sns.set_style("ticks")

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Scientific/publication-style graph-এর জন্য useful।

---

# 6. কোন Style কখন ব্যবহার করবে?

| Style       | ব্যবহার            |
| ----------- | ------------------ |
| `darkgrid`  | General analysis   |
| `whitegrid` | Data analysis      |
| `dark`      | Dark presentation  |
| `white`     | Clean presentation |
| `ticks`     | Scientific/report  |

আমার recommendation:

```text
EDA → whitegrid
Report → white / ticks
Dashboard → white
Presentation → white / dark
```

---

# 7. `sns.set_context()`

এটি graph-এর **overall scale** control করে।

Options:

```text
paper
notebook
talk
poster
```

---

## 7.1 paper

```python
sns.set_context("paper")
```

Small figure / research paper-এর জন্য।

---

## 7.2 notebook

```python
sns.set_context("notebook")
```

Jupyter Notebook-এর জন্য ভালো।

---

## 7.3 talk

```python
sns.set_context("talk")
```

Presentation-এর জন্য।

---

## 7.4 poster

```python
sns.set_context("poster")
```

Large presentation / poster-এর জন্য।

---

# 8. Context + Style একসাথে

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)
```

তারপর:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

এটি একটি খুব useful professional pattern।

---

# 9. Context Scaling

আরও fine control:

```python
sns.set_context(
    "notebook",
    font_scale=1.2
)
```

`font_scale`:

```text
1.0 → normal
1.2 → slightly larger
1.5 → larger
2.0 → very large
```

Example:

```python
sns.set_context(
    "talk",
    font_scale=1.1
)
```

---

# 10. `sns.despine()`

Graph-এর চারপাশের unnecessary border remove করতে:

```python
sns.despine()
```

Example:

```python
sns.set_style("whitegrid")

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

sns.despine()

plt.show()
```

---

## Top/right spine remove

```python
sns.despine(
    top=True,
    right=True
)
```

---

## Left/bottom রাখা

সাধারণত:

```python
sns.despine(
    top=True,
    right=True
)
```

professional charts-এর জন্য খুব common।

---

# 11. Color Palette কী?

Color palette হলো graph-এ ব্যবহৃত colors-এর collection।

Seaborn-এর অনেক built-in palette আছে।

```python
sns.color_palette()
```

---

# 12. Basic Color Palette

```python
sns.color_palette("deep")
```

অন্যগুলো:

```python
sns.color_palette("muted")
sns.color_palette("bright")
sns.color_palette("pastel")
sns.color_palette("dark")
sns.color_palette("colorblind")
```

---

# 13. `palette=` ব্যবহার

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    palette="Set2"
)

plt.show()
```

এখানে:

```text
palette="Set2"
```

color scheme নির্ধারণ করছে।

---

# 14. Qualitative Palette

Categorical data-এর জন্য qualitative palette ব্যবহার করা হয়।

Examples:

```python
"Set1"
"Set2"
"Set3"
"Pastel1"
"Pastel2"
"Dark2"
"Paired"
```

Example:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex",
    palette="Set2"
)

plt.show()
```

---

# 15. Sequential Palette

যখন numerical value low → high দেখাতে হবে তখন sequential palette useful।

Examples:

```text
Blues
Greens
Reds
Purples
Oranges
```

Example:

```python
sns.heatmap(
    df.corr(numeric_only=True),
    cmap="Blues",
    annot=True
)

plt.show()
```

এখানে:

```python
cmap="Blues"
```

ব্যবহার হয়েছে।

---

# 16. Diverging Palette

যেখানে value-এর দুই direction আছে:

```text
Negative
   ↓
Zero
   ↓
Positive
```

তখন diverging palette useful।

Example:

```python
sns.heatmap(
    df.corr(numeric_only=True),
    cmap="coolwarm",
    center=0,
    annot=True
)

plt.show()
```

Correlation heatmap-এর জন্য খুব useful।

Other examples:

```text
RdBu
PiYG
BrBG
coolwarm
```

---

# 17. Palette Selection Rule

খুব important:

### Categorical

```text
Set2
Set3
Pastel
Dark2
colorblind
```

### Numerical low → high

```text
Blues
Greens
Reds
```

### Negative → Positive

```text
coolwarm
RdBu
```

Mental model:

```text
Category
   ↓
Qualitative

Low → High
   ↓
Sequential

Negative → Positive
   ↓
Diverging
```

---

# 18. Colorblind-friendly Palette

Professional visualization-এ accessibility গুরুত্বপূর্ণ।

Seaborn:

```python
sns.color_palette("colorblind")
```

Example:

```python
sns.set_palette("colorblind")

sns.countplot(
    data=df,
    x="day",
    hue="sex"
)

plt.show()
```

এটি visually distinguishable colors দিতে সাহায্য করে।

---

# 19. Custom Color List

নিজের colors দিতে পারো:

```python
palette = [
    "#4C72B0",
    "#55A868",
    "#C44E52"
]
```

তারপর:

```python
sns.countplot(
    data=df,
    x="day",
    hue="sex",
    palette=palette
)
```

তবে বাস্তব project-এ arbitrary অনেক colors ব্যবহার না করাই ভালো।

---

# 20. `sns.set_palette()`

পুরো notebook/session-এর default palette পরিবর্তন:

```python
sns.set_palette("Set2")
```

এরপর:

```python
sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex"
)
```

---

# 21. Temporary Palette

একটি specific block-এর জন্য:

```python
with sns.color_palette("Set2"):
    sns.countplot(
        data=df,
        x="day",
        hue="sex"
    )

plt.show()
```

এতে পুরো notebook-এর palette permanently change হবে না।

---

# 22. Figure Size

Matplotlib দিয়ে:

```python
plt.figure(figsize=(10, 6))
```

Example:

```python
plt.figure(figsize=(10, 6))

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip"
)

plt.show()
```

Format:

```text
figsize=(width, height)
```

---

# 23. Title

```python
plt.title("Total Bill vs Tip")
```

Better:

```python
plt.title(
    "Relationship Between Total Bill and Tip",
    fontsize=16
)
```

---

# 24. Axis Labels

```python
plt.xlabel("Total Bill")
plt.ylabel("Tip")
```

Better:

```python
plt.xlabel(
    "Total Bill ($)",
    fontsize=12
)

plt.ylabel(
    "Tip ($)",
    fontsize=12
)
```

---

# 25. Complete Styled Scatterplot

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)

plt.figure(figsize=(10, 6))

sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    palette="Set2",
    s=80,
    alpha=0.7
)

plt.title(
    "Relationship Between Total Bill and Tip",
    fontsize=16
)

plt.xlabel("Total Bill ($)")
plt.ylabel("Tip ($)")

sns.despine()

plt.tight_layout()
plt.show()
```

এটাই basic professional visualization workflow।

---

# 26. `alpha`

Transparency control করতে:

```python
alpha=0.5
```

Example:

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    alpha=0.5
)
```

Useful যখন অনেক points overlap করে।

---

# 27. `s` — Point Size

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    s=100
)
```

এখানে:

```text
s=50 → small
s=100 → medium
s=200 → large
```

---

# 28. Marker Style

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex",
    style="time"
)
```

এখানে color এবং marker shape দুইভাবেই group বোঝানো হচ্ছে।

---

# 29. Legend

Legend সাধারণত automatically আসে।

```python
sns.scatterplot(
    data=df,
    x="total_bill",
    y="tip",
    hue="sex"
)
```

Legend position control:

```python
plt.legend(
    title="Gender"
)
```

---

# 30. Legend বাইরে নেওয়া

```python
plt.legend(
    bbox_to_anchor=(1.05, 1),
    loc="upper left"
)
```

এটি dashboard/report-এ useful হতে পারে।

---

# 31. Tick Rotation

Categorical labels বড় হলে:

```python
plt.xticks(rotation=45)
```

Example:

```python
sns.countplot(
    data=df,
    x="day"
)

plt.xticks(rotation=45)

plt.show()
```

---

# 32. Tick Font Size

```python
plt.xticks(fontsize=10)
plt.yticks(fontsize=10)
```

---

# 33. `plt.tight_layout()`

অনেক সময় title/label cut হয়ে যায়।

Use:

```python
plt.tight_layout()
```

Example:

```python
plt.figure(figsize=(10, 6))

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Total Bill by Day")

plt.tight_layout()
plt.show()
```

**Professional habit:** প্রায় সব complex plot-এ `tight_layout()` check করবে।

---

# 34. Heatmap Styling

M08-এর correlation heatmap এবার professional করি।

```python
sns.set_theme(
    style="white",
    context="notebook"
)

corr = df.corr(numeric_only=True)

plt.figure(figsize=(8, 6))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1,
    square=True,
    linewidths=0.5
)

plt.title(
    "Feature Correlation Matrix",
    fontsize=16
)

plt.tight_layout()
plt.show()
```

---

# 35. Professional Boxplot

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)

plt.figure(figsize=(10, 6))

sns.boxplot(
    data=df,
    x="day",
    y="total_bill",
    hue="sex",
    palette="Set2"
)

plt.title(
    "Total Bill Distribution by Day and Gender",
    fontsize=16
)

plt.xlabel("Day")
plt.ylabel("Total Bill ($)")

sns.despine()

plt.tight_layout()
plt.show()
```

---

# 36. Professional Histogram

```python
sns.set_theme(
    style="whitegrid"
)

plt.figure(figsize=(10, 6))

sns.histplot(
    data=df,
    x="total_bill",
    bins=20,
    kde=True,
    color="steelblue"
)

plt.title(
    "Distribution of Total Bill",
    fontsize=16
)

plt.xlabel("Total Bill ($)")
plt.ylabel("Frequency")

sns.despine()

plt.tight_layout()
plt.show()
```

---

# 37. Professional Countplot

```python
sns.set_theme(
    style="whitegrid"
)

plt.figure(figsize=(9, 6))

sns.countplot(
    data=df,
    x="day",
    hue="sex",
    palette="Set2"
)

plt.title(
    "Customer Count by Day and Gender",
    fontsize=16
)

plt.xlabel("Day")
plt.ylabel("Number of Customers")

plt.tight_layout()
plt.show()
```

---

# 38. Styling Hierarchy

একটি professional graph-এ এই hierarchy রাখো:

```text
1. Data
   ↓
2. Correct Plot
   ↓
3. Color
   ↓
4. Title
   ↓
5. Axis Labels
   ↓
6. Legend
   ↓
7. Grid/Spines
   ↓
8. Layout
```

প্রথমে decoration নয়।

**প্রথমে analytical correctness।**

---

# 39. Don't Overuse Colors

Bad:

```text
10 categories
10 completely different colors
```

Better:

```text
Main category
    ↓
2–5 meaningful colors
```

বিশেষ করে business/ML report-এ color-এর semantic meaning consistent রাখা ভালো।

---

# 40. Color-এর Meaning Consistent রাখো

ধরো ML project:

```text
Normal → one consistent color
Suspicious → another consistent color
```

তাহলে পুরো project-এ একই mapping রাখো।

Example:

```python
class_palette = {
    "Normal": "...",
    "Suspicious": "..."
}
```

তারপর বিভিন্ন plot-এ একই palette ব্যবহার করো।

এতে reader-এর cognitive load কমে।

---

# 41. AI CCTV Project-এ Styling

তোমার suspicious detection project-এর কথা ধরো।

Dataset:

```text
target
------
Normal
Suspicious
```

ধরো features:

```text
motion_score
brightness
person_count
duration
```

Countplot:

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)

plt.figure(figsize=(8, 5))

sns.countplot(
    data=df,
    x="target"
)

plt.title("Class Distribution")
plt.xlabel("Class")
plt.ylabel("Number of Samples")

plt.tight_layout()
plt.show()
```

এখানে তুমি প্রথমেই বুঝতে পারবে:

```text
Normal       → ?
Suspicious   → ?
```

Class imbalance আছে কি না।

---

# 42. CCTV Feature Visualization

ধরো:

```python
sns.boxplot(
    data=df,
    x="target",
    y="motion_score"
)
```

এর মাধ্যমে:

```text
Normal
   vs
Suspicious
```

motion score-এর distribution compare করা যায়।

---

# 43. Feature Distribution

```python
sns.histplot(
    data=df,
    x="motion_score",
    hue="target",
    kde=True
)

plt.title("Motion Score Distribution by Class")

plt.tight_layout()
plt.show()
```

এখন তুমি দেখতে পারবে classes কতটা overlap করছে।

---

# 44. PairGrid Styled for ML

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)

g = sns.PairGrid(
    df,
    vars=[
        "motion_score",
        "brightness",
        "person_count",
        "duration"
    ],
    hue="target"
)

g.map_diag(sns.histplot)
g.map_offdiag(sns.scatterplot)

g.add_legend()

plt.show()
```

এখানে styling + M12-এর knowledge একসাথে ব্যবহার হচ্ছে।

---

# 45. EDA Professional Template

তোমার ML dataset-এর জন্য এই structure follow করতে পারো:

### Step 1 — Dataset overview

```python
df.shape
df.info()
df.describe()
```

### Step 2 — Missing values

```python
df.isnull().sum()
```

### Step 3 — Target distribution

```python
sns.countplot(
    data=df,
    x="target"
)
```

### Step 4 — Numerical distributions

```python
sns.histplot(...)
```

### Step 5 — Outliers

```python
sns.boxplot(...)
```

### Step 6 — Correlation

```python
sns.heatmap(...)
```

### Step 7 — Feature relationships

```python
sns.pairplot(...)
```

### Step 8 — Class separation

```python
sns.scatterplot(
    data=df,
    x="feature1",
    y="feature2",
    hue="target"
)
```

### Step 9 — Professional styling

```text
theme
palette
labels
title
legend
layout
```

---

# 46. `set_theme()` Professional Configuration

একটি reusable configuration বানাতে পারো:

```python
sns.set_theme(
    style="whitegrid",
    context="notebook",
    font_scale=1.0
)
```

তারপর প্রতিটি plot-এর জন্য শুধু data analysis করো।

---

# 47. Visualization Function বানানো

বড় project-এ repeated code avoid করতে function বানানো ভালো।

```python
def setup_plot():
    sns.set_theme(
        style="whitegrid",
        context="notebook",
        font_scale=1.0
    )
```

তারপর:

```python
setup_plot()

sns.boxplot(
    data=df,
    x="day",
    y="total_bill"
)

plt.title("Total Bill by Day")
plt.tight_layout()
plt.show()
```

---

# 48. Analyst হিসেবে কী Avoid করবে?

### ❌ Too many colors

### ❌ 3D chart unnecessarily

### ❌ Huge title

### ❌ Tiny labels

### ❌ Overlapping legend

### ❌ Excessive grid

### ❌ Decorative effects without analytical purpose

### ❌ Misleading axis

### ❌ Inconsistent colors between charts

### ❌ Too many plots in one figure

---

# 49. Data Visualization-এর Golden Rule

মনে রাখবে:

> **Visualization-এর উদ্দেশ্য হলো data বোঝানো, decoration করা নয়।**

একটি সুন্দর graph যদি ভুল conclusion তৈরি করে, তাহলে সেটি ভালো visualization নয়।

---

# 50. M13 Cheat Sheet

| কাজ            | Code                         |
| -------------- | ---------------------------- |
| Theme          | `sns.set_theme()`            |
| Style          | `sns.set_style()`            |
| Context        | `sns.set_context()`          |
| Remove spines  | `sns.despine()`              |
| Palette        | `sns.set_palette()`          |
| Color palette  | `sns.color_palette()`        |
| Figure size    | `plt.figure(figsize=(10,6))` |
| Title          | `plt.title()`                |
| X label        | `plt.xlabel()`               |
| Y label        | `plt.ylabel()`               |
| Rotate ticks   | `plt.xticks(rotation=45)`    |
| Layout         | `plt.tight_layout()`         |
| Transparency   | `alpha=`                     |
| Point size     | `s=`                         |
| Category color | `palette=`                   |
| Heatmap colors | `cmap=`                      |

---

# 51. Most Important Patterns

### General EDA

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)
```

### Report

```python
sns.set_theme(
    style="ticks",
    context="paper"
)
```

### Presentation

```python
sns.set_theme(
    style="white",
    context="talk"
)
```

### Heatmap

```python
sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)
```

### Categorical

```python
sns.countplot(
    data=df,
    x="category",
    hue="target",
    palette="Set2"
)
```

### Distribution

```python
sns.histplot(
    data=df,
    x="feature",
    hue="target",
    kde=True
)
```

---

# 52. M13 Practice Tasks

এগুলো নিজে code করে করবে।

### Beginner

**Task 1**

`tips` dataset-এর `total_bill` histogram বানাও।

Requirements:

```text
whitegrid
figure size
title
xlabel
ylabel
```

---

**Task 2**

`day` অনুযায়ী countplot বানাও।

Add:

```text
palette
title
labels
```

---

**Task 3**

`total_bill` vs `tip` scatterplot বানাও।

Add:

```text
hue="sex"
alpha
figure size
title
```

---

### Intermediate

**Task 4**

এই তিনটি style compare করো:

```python
darkgrid
whitegrid
ticks
```

---

**Task 5**

এই palette compare করো:

```text
Set2
Pastel2
colorblind
```

---

**Task 6**

Correlation heatmap professional style-এ বানাও।

Requirements:

```text
annot=True
fmt=".2f"
center=0
vmin=-1
vmax=1
square=True
```

---

### Advanced

**Task 7**

CCTV dataset-এর জন্য:

```text
Normal vs Suspicious
```

class distribution visualization বানাও।

---

**Task 8**

`motion_score`:

```text
Normal vs Suspicious
```

এর জন্য:

```text
boxplot
histplot
```

দুটো বানিয়ে compare করো।

---

**Task 9**

এই features দিয়ে PairGrid বানাও:

```python
motion_score
brightness
person_count
duration
```

`target` দিয়ে `hue` করো।

---

# 53. M13 Completion Checklist

M13 complete করার আগে নিজেকে জিজ্ঞেস করো:

```text
[ ] sns.set_theme()
[ ] sns.set_style()
[ ] sns.set_context()
[ ] sns.despine()
[ ] qualitative palette
[ ] sequential palette
[ ] diverging palette
[ ] colorblind palette
[ ] custom palette
[ ] alpha
[ ] figure size
[ ] title
[ ] axis labels
[ ] legend
[ ] tick rotation
[ ] tight_layout
[ ] professional EDA styling
[ ] ML dataset visualization
```

সবগুলো পারলে **M13 complete**।

---

# M13-এর Core Mental Model

```text
                 SEABORN
                    │
        ┌───────────┴───────────┐
        ↓                       ↓
    Analysis                  Styling
        │                       │
 Histogram                  Theme
 Boxplot                    Style
 Violin                     Context
 Scatter                    Palette
 Heatmap                    Labels
 Pairplot                   Legend
        │                       │
        └───────────┬───────────┘
                    ↓
          Professional EDA
                    ↓
            ML Understanding
                    ↓
          Better Model Decisions
```

**পরবর্তী:** **M14 — Seaborn Advanced EDA Workflow**, যেখানে আলাদা আলাদা plot না শিখে একটি real dataset নিয়ে **Data Cleaning → Univariate → Bivariate → Multivariate → Target Analysis → Outlier → Correlation → Feature Relationship → Insight Extraction → ML-ready EDA report** পুরো workflow হিসেবে করব।

---
# Seaborn M14 — Advanced EDA Workflow Deep Dive

M13-তে তুমি **professional styling** শিখেছো। এখন M14 থেকে আমরা আলাদা আলাদা chart শেখার বাইরে গিয়ে **একটি complete EDA workflow** শিখব।

এখানে সবচেয়ে important বিষয় হলো:

> **EDA মানে শুধু graph বানানো নয়; data দেখে প্রশ্ন করা, evidence খোঁজা এবং insight বের করা।**

বিশেষ করে তোমার **Machine Learning / AI CCTV** project-এর জন্য এই workflow খুব গুরুত্বপূর্ণ।

---

# 1. M14-তে আমরা কী শিখব?

পুরো workflow:

```text
Raw Dataset
     ↓
1. Data Understanding
     ↓
2. Data Quality Check
     ↓
3. Missing Value Analysis
     ↓
4. Duplicate Analysis
     ↓
5. Univariate Analysis
     ↓
6. Bivariate Analysis
     ↓
7. Multivariate Analysis
     ↓
8. Target Analysis
     ↓
9. Outlier Analysis
     ↓
10. Correlation Analysis
     ↓
11. Feature Relationship
     ↓
12. Data Leakage Check
     ↓
13. ML Readiness
     ↓
14. EDA Insights
```

---

# 2. EDA-এর আসল উদ্দেশ্য

ধরো তোমার dataset:

```text
motion_score
brightness
person_count
duration
target
```

Target:

```text
Normal
Suspicious
```

তুমি শুধু graph বানাবে না।

তোমার প্রশ্ন হবে:

```text
1. Dataset কত বড়?
2. Missing values আছে?
3. Duplicate আছে?
4. Class imbalance আছে?
5. কোন feature-এর distribution কেমন?
6. Suspicious class-এর motion বেশি?
7. কোন feature-এর outlier আছে?
8. Features-এর মধ্যে correlation কেমন?
9. কোন feature target আলাদা করতে সাহায্য করছে?
10. Data leakage আছে?
```

এটাই **real EDA**।

---

# 3. Step 1 — Dataset Load

ধরি CSV dataset:

```python
import pandas as pd
import numpy as np

import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("cctv_dataset.csv")

print(df.head())
```

---

# 4. Step 2 — Dataset Shape

```python
print("Rows:", df.shape[0])
print("Columns:", df.shape[1])
```

অথবা:

```python
print(df.shape)
```

Example:

```text
(10000, 5)
```

মানে:

```text
10,000 rows
5 columns
```

---

# 5. Step 3 — Columns

```python
print(df.columns.tolist())
```

Example:

```text
[
    'motion_score',
    'brightness',
    'person_count',
    'duration',
    'target'
]
```

---

# 6. Step 4 — Data Types

```python
print(df.dtypes)
```

Example:

```text
motion_score     float64
brightness       float64
person_count       int64
duration         float64
target            object
```

এখান থেকেই তুমি বুঝতে পারবে:

```text
Numerical
Categorical
```

কোনগুলো।

---

# 7. Step 5 — `info()`

```python
df.info()
```

এখানে দেখতে হবে:

```text
Column
Non-Null Count
Dtype
```

এটি data quality-এর প্রথম check।

---

# 8. Step 6 — Statistical Summary

```python
df.describe()
```

এখানে পাবো:

```text
count
mean
std
min
25%
50%
75%
max
```

---

## Example

```text
motion_score

mean = 0.45
std  = 0.20
min  = 0.01
max  = 0.98
```

এখানে প্রশ্ন:

> motion score-এর range reasonable কি?

---

# 9. Step 7 — Numerical vs Categorical

```python
numeric_cols = df.select_dtypes(
    include=np.number
).columns

categorical_cols = df.select_dtypes(
    exclude=np.number
).columns

print("Numerical:", numeric_cols.tolist())
print("Categorical:", categorical_cols.tolist())
```

এটি খুব useful automation।

---

# 10. Step 8 — Missing Value Analysis

প্রথমে:

```python
df.isnull().sum()
```

Percentage:

```python
missing_pct = (
    df.isnull().mean() * 100
)

print(missing_pct)
```

---

## Visualization

```python
missing = (
    df.isnull()
      .sum()
      .sort_values(ascending=False)
)

missing = missing[missing > 0]

plt.figure(figsize=(8, 5))

sns.barplot(
    x=missing.values,
    y=missing.index
)

plt.title("Missing Values by Feature")
plt.xlabel("Missing Count")
plt.ylabel("Feature")

plt.tight_layout()
plt.show()
```

---

# 11. Missing Value থেকে Insight

ধরো:

```text
brightness       0%
motion_score     0%
person_count     2%
duration         15%
target           0%
```

তাহলে:

```text
duration
   ↓
15% missing
   ↓
Investigate
   ↓
Drop / Impute / Recalculate
```

EDA এখানেই decision-making শুরু করে।

---

# 12. Step 9 — Duplicate Analysis

```python
print(
    "Duplicates:",
    df.duplicated().sum()
)
```

Duplicate rows দেখতে:

```python
duplicates = df[
    df.duplicated()
]

print(duplicates)
```

Remove করার আগে অবশ্যই investigate করবে।

---

# 13. Step 10 — Target Analysis

ML project-এ **Target প্রথমে বুঝতে হবে।**

```python
print(df["target"].value_counts())
```

Percentage:

```python
print(
    df["target"]
      .value_counts(normalize=True)
      .mul(100)
)
```

---

# 14. Target Visualization

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)

plt.figure(figsize=(8, 5))

sns.countplot(
    data=df,
    x="target"
)

plt.title("Target Class Distribution")
plt.xlabel("Class")
plt.ylabel("Count")

plt.tight_layout()
plt.show()
```

---

# 15. Class Imbalance

ধরো:

```text
Normal       9000
Suspicious   1000
```

Percentage:

```text
Normal       90%
Suspicious   10%
```

এটি:

```text
90 : 10
```

class imbalance।

ML-এ এটি গুরুত্বপূর্ণ কারণ accuracy misleading হতে পারে।

---

# 16. Percentage Plot

```python
class_pct = (
    df["target"]
    .value_counts(normalize=True)
    .mul(100)
    .reset_index()
)

class_pct.columns = [
    "target",
    "percentage"
]

print(class_pct)
```

Visualization:

```python
plt.figure(figsize=(8, 5))

sns.barplot(
    data=class_pct,
    x="target",
    y="percentage"
)

plt.ylabel("Percentage (%)")
plt.title("Class Distribution (%)")

plt.tight_layout()
plt.show()
```

---

# 17. Step 11 — Univariate Analysis

**Univariate = একটি variable বিশ্লেষণ।**

Example:

```text
motion_score
```

Questions:

```text
Distribution?
Mean?
Median?
Skewness?
Outliers?
Range?
```

---

# 18. Histogram

```python
plt.figure(figsize=(9, 5))

sns.histplot(
    data=df,
    x="motion_score",
    kde=True
)

plt.title("Motion Score Distribution")

plt.tight_layout()
plt.show()
```

---

# 19. Boxplot

```python
plt.figure(figsize=(8, 4))

sns.boxplot(
    data=df,
    x="motion_score"
)

plt.title("Motion Score Boxplot")

plt.tight_layout()
plt.show()
```

এখানে দেখতে পারবে:

```text
Median
IQR
Whiskers
Outliers
```

---

# 20. Numerical Feature Loop

অনেক feature থাকলে manually chart না বানিয়ে loop:

```python
for col in numeric_cols:

    plt.figure(figsize=(8, 4))

    sns.histplot(
        data=df,
        x=col,
        kde=True
    )

    plt.title(f"Distribution of {col}")

    plt.tight_layout()
    plt.show()
```

এটি automated EDA-এর basic technique।

---

# 21. Numerical Boxplot Loop

```python
for col in numeric_cols:

    plt.figure(figsize=(8, 4))

    sns.boxplot(
        data=df,
        x=col
    )

    plt.title(f"Boxplot of {col}")

    plt.tight_layout()
    plt.show()
```

---

# 22. Categorical Analysis

Categorical columns:

```python
for col in categorical_cols:

    print(
        f"\n{col}"
    )

    print(
        df[col].value_counts()
    )
```

Visualization:

```python
for col in categorical_cols:

    plt.figure(figsize=(8, 5))

    sns.countplot(
        data=df,
        x=col
    )

    plt.title(f"Distribution of {col}")

    plt.xticks(rotation=45)

    plt.tight_layout()
    plt.show()
```

---

# 23. Step 12 — Bivariate Analysis

**Bivariate = দুইটি variable-এর relationship।**

Examples:

```text
motion_score vs target
brightness vs target
motion_score vs duration
```

---

# 24. Numerical vs Numerical

```python
sns.scatterplot(
    data=df,
    x="motion_score",
    y="duration"
)

plt.show()
```

Question:

> Motion বাড়লে duration কি বাড়ছে?

---

# 25. Numerical vs Categorical

এটি ML-এ অত্যন্ত গুরুত্বপূর্ণ।

```python
sns.boxplot(
    data=df,
    x="target",
    y="motion_score"
)

plt.title(
    "Motion Score by Target Class"
)

plt.show()
```

এখানে:

```text
Normal
   vs
Suspicious
```

comparison হচ্ছে।

---

# 26. Violinplot

আরও distribution দেখতে:

```python
sns.violinplot(
    data=df,
    x="target",
    y="motion_score"
)

plt.show()
```

এখানে শুধু median নয়, distribution shape-ও দেখা যায়।

---

# 27. Stripplot + Boxplot

Individual observations দেখতে:

```python
sns.boxplot(
    data=df,
    x="target",
    y="motion_score"
)

sns.stripplot(
    data=df,
    x="target",
    y="motion_score",
    alpha=0.4
)

plt.show()
```

এটি অনেক useful combination।

---

# 28. Step 13 — Multivariate Analysis

**Multivariate = 3 বা তার বেশি variables একসাথে।**

Example:

```text
motion_score
brightness
person_count
duration
target
```

---

# 29. Scatterplot + Hue

```python
sns.scatterplot(
    data=df,
    x="motion_score",
    y="duration",
    hue="target",
    alpha=0.7
)

plt.title(
    "Motion Score vs Duration by Class"
)

plt.show()
```

এখানে তুমি দেখতে পারো:

```text
Class separation
Overlap
Clusters
Outliers
```

---

# 30. Pairplot

```python
sns.pairplot(
    df,
    vars=[
        "motion_score",
        "brightness",
        "person_count",
        "duration"
    ],
    hue="target"
)

plt.show()
```

এটি multiple feature relationships দেখতে powerful।

---

# 31. Pairplot কখন ব্যবহার করবে?

Small/medium number of features হলে:

```text
3–8 features
```

ভালো।

যদি:

```text
50 features
100 features
```

থাকে, pairplot খুব cluttered হয়ে যাবে।

তখন correlation/feature selection ব্যবহার করবে।

---

# 32. Step 14 — Correlation Analysis

```python
corr = df.corr(
    numeric_only=True
)

print(corr)
```

Heatmap:

```python
plt.figure(figsize=(9, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)

plt.title("Correlation Heatmap")

plt.tight_layout()
plt.show()
```

---

# 33. Correlation থেকে কী বুঝবে?

ধরো:

```text
motion_score ↔ duration
r = 0.82
```

Strong positive relationship।

কিন্তু:

> correlation মানেই causal relationship নয়।

এটি M08-তে শিখেছো।

---

# 34. Step 15 — Outlier Analysis

Boxplot:

```python
sns.boxplot(
    data=df,
    x="motion_score"
)

plt.show()
```

IQR method:

```python
Q1 = df["motion_score"].quantile(0.25)
Q3 = df["motion_score"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["motion_score"] < lower) |
    (df["motion_score"] > upper)
]

print(outliers)
```

---

# 35. Important: Outlier ≠ Error

এটি খুব গুরুত্বপূর্ণ।

ধরো:

```text
Normal motion:
0.1
0.2
0.3

একটি value:
0.95
```

এটি outlier হতে পারে।

কিন্তু CCTV-তে:

> 0.95 motion সত্যিই একটি unusual event হতে পারে।

তাই blindly delete করবে না।

---

# 36. Outlier Investigation Workflow

```text
Outlier detected
      ↓
Check raw data
      ↓
Is it data-entry error?
      ↓
       ├── Yes → Fix/Remove
       │
       └── No
            ↓
       Real observation?
            ↓
       Keep / Transform
```

---

# 37. Step 16 — Feature vs Target Analysis

প্রতিটি numerical feature-এর জন্য:

```python
for col in numeric_cols:

    if col == "target":
        continue

    plt.figure(figsize=(8, 5))

    sns.boxplot(
        data=df,
        x="target",
        y=col
    )

    plt.title(
        f"{col} Distribution by Target"
    )

    plt.tight_layout()
    plt.show()
```

এটি ML feature analysis-এর খুব useful automation।

---

# 38. Feature Separation

ধরো:

```text
motion_score
```

দুই class:

```text
Normal:
0.1 ───── 0.4

Suspicious:
0.6 ───── 0.9
```

তাহলে featureটি potentially useful।

কিন্তু যদি:

```text
Normal:
0.1 ───────── 0.8

Suspicious:
0.2 ───────── 0.9
```

তাহলে অনেক overlap।

Feature-এর standalone separation কম হতে পারে।

---

# 39. Feature Leakage

EDA-এর সবচেয়ে important advanced concepts-এর একটি।

ধরো target:

```text
Suspicious = 1
Normal = 0
```

আর feature:

```text
suspicious_score
```

যেটা আসলে target calculation থেকে তৈরি হয়েছে।

তাহলে model আগে থেকেই answer দেখে ফেলছে।

এটাই **data leakage**।

---

# 40. Leakage Check

প্রতিটি feature নিয়ে প্রশ্ন করো:

```text
এই feature prediction-এর সময় available থাকবে?
```

যদি answer:

```text
NO
```

তাহলে featureটি suspicious।

---

# 41. Train/Test Leakage

আরেকটি common problem:

```text
Same video
   ↓
Train clips

Same video
   ↓
Test clips
```

এটি CCTV/video dataset-এ খুব dangerous।

কারণ model একই video's visual pattern train ও test দুটোতেই দেখতে পারে।

Better:

```text
Video A → Train
Video B → Train
Video C → Validation
Video D → Test
```

অর্থাৎ **split by video/source**, শুধু frame/clip দিয়ে random split নয়।

এটি তোমার CCTV project-এর জন্য বিশেষভাবে গুরুত্বপূর্ণ।

---

# 42. Step 17 — Target + All Features

একটি useful approach:

```python
features = [
    "motion_score",
    "brightness",
    "person_count",
    "duration"
]
```

তারপর:

```python
for feature in features:

    plt.figure(figsize=(8, 5))

    sns.violinplot(
        data=df,
        x="target",
        y=feature
    )

    plt.title(
        f"{feature} by Target"
    )

    plt.tight_layout()
    plt.show()
```

---

# 43. Step 18 — Statistical Summary by Class

শুধু graph নয়।

```python
print(
    df.groupby("target")[numeric_cols]
      .mean()
)
```

Median:

```python
print(
    df.groupby("target")[numeric_cols]
      .median()
)
```

---

# 44. Mean Comparison

Example:

```text
                 Normal   Suspicious
motion_score      0.21      0.72
brightness        0.61      0.58
duration          4.2       8.7
```

এখান থেকে initial hypothesis তৈরি করা যায়:

```text
Suspicious events
→ higher motion
→ longer duration
```

তারপর visualization দিয়ে validate করতে হবে।

---

# 45. Groupby + Aggregation

```python
summary = (
    df.groupby("target")
      .agg({
          "motion_score": ["mean", "median"],
          "brightness": ["mean", "median"],
          "duration": ["mean", "median"]
      })
)

print(summary)
```

এটি EDA report-এ খুব useful।

---

# 46. Crosstab

Categorical variables-এর relationship:

```python
pd.crosstab(
    df["target"],
    df["some_category"]
)
```

Percentage:

```python
pd.crosstab(
    df["target"],
    df["some_category"],
    normalize="index"
) * 100
```

---

# 47. Heatmap of Crosstab

```python
ct = pd.crosstab(
    df["target"],
    df["some_category"],
    normalize="index"
) * 100

plt.figure(figsize=(8, 5))

sns.heatmap(
    ct,
    annot=True,
    fmt=".1f",
    cmap="Blues"
)

plt.title(
    "Target vs Category (%)"
)

plt.tight_layout()
plt.show()
```

---

# 48. EDA থেকে Insight কীভাবে লিখবে?

এটি খুব important skill।

শুধু:

> "I created a boxplot."

বলবে না।

বরং:

> "Suspicious samples show a higher median motion score than normal samples, although some overlap exists between the two classes."

অর্থাৎ:

```text
Observation
     ↓
Evidence
     ↓
Interpretation
     ↓
Potential ML implication
```

---

# 49. Example Insight

ধরো graph দেখাচ্ছে:

```text
Normal motion median = 0.25
Suspicious median = 0.70
```

Insight:

```text
Suspicious samples generally exhibit higher motion scores
than normal samples, suggesting motion_score may be a
useful predictive feature.
```

কিন্তু মনে রাখবে:

> একটি feature useful মনে হলেই model-এ automatically useful হবে—এমন guarantee নেই।

---

# 50. Full Advanced EDA Pipeline

এখন পুরো workflow একসাথে:

```python
import pandas as pd
import numpy as np

import seaborn as sns
import matplotlib.pyplot as plt


# =========================
# 1. LOAD DATA
# =========================

df = pd.read_csv("cctv_dataset.csv")


# =========================
# 2. BASIC INFORMATION
# =========================

print("Shape:", df.shape)

print("\nColumns:")
print(df.columns.tolist())

print("\nData Types:")
print(df.dtypes)

print("\nInfo:")
df.info()

print("\nStatistics:")
print(df.describe())


# =========================
# 3. DATA QUALITY
# =========================

print("\nMissing Values:")
print(df.isnull().sum())

print("\nDuplicates:")
print(df.duplicated().sum())


# =========================
# 4. COLUMN TYPES
# =========================

numeric_cols = df.select_dtypes(
    include=np.number
).columns

categorical_cols = df.select_dtypes(
    exclude=np.number
).columns


# =========================
# 5. TARGET ANALYSIS
# =========================

print("\nTarget Distribution:")

print(
    df["target"].value_counts()
)

print(
    df["target"]
    .value_counts(normalize=True)
    * 100
)


plt.figure(figsize=(8, 5))

sns.countplot(
    data=df,
    x="target"
)

plt.title("Target Distribution")

plt.tight_layout()
plt.show()


# =========================
# 6. NUMERICAL DISTRIBUTIONS
# =========================

for col in numeric_cols:

    if col == "target":
        continue

    plt.figure(figsize=(8, 4))

    sns.histplot(
        data=df,
        x=col,
        kde=True
    )

    plt.title(
        f"Distribution of {col}"
    )

    plt.tight_layout()
    plt.show()


# =========================
# 7. OUTLIER ANALYSIS
# =========================

for col in numeric_cols:

    if col == "target":
        continue

    plt.figure(figsize=(8, 4))

    sns.boxplot(
        data=df,
        x=col
    )

    plt.title(
        f"Boxplot of {col}"
    )

    plt.tight_layout()
    plt.show()


# =========================
# 8. FEATURE vs TARGET
# =========================

for col in numeric_cols:

    if col == "target":
        continue

    plt.figure(figsize=(8, 5))

    sns.boxplot(
        data=df,
        x="target",
        y=col
    )

    plt.title(
        f"{col} by Target"
    )

    plt.tight_layout()
    plt.show()


# =========================
# 9. CORRELATION
# =========================

corr = df.corr(
    numeric_only=True
)

plt.figure(figsize=(9, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)

plt.title(
    "Correlation Matrix"
)

plt.tight_layout()
plt.show()
```

এটি তোমার একটি **EDA foundation template**।

---

# 51. কিন্তু Professional EDA এখানেই শেষ নয়

Real-world EDA-তে এই questions-ও করতে হবে:

```text
✓ Is target balanced?
✓ Are features valid?
✓ Are units correct?
✓ Missing values?
✓ Duplicate rows?
✓ Outliers?
✓ Skewness?
✓ Feature correlation?
✓ Multicollinearity?
✓ Target relationship?
✓ Data leakage?
✓ Train/test contamination?
✓ Sampling bias?
✓ Temporal bias?
✓ Source/video bias?
```

---

# 52. CCTV Dataset-এর জন্য বিশেষ EDA

তোমার project যেহেতু video-based suspicious detection, তাই সাধারণ tabular EDA-এর পাশাপাশি:

```text
Video
 ↓
Frame
 ↓
Clip
 ↓
Label
```

এই hierarchy বুঝতে হবে।

---

# 53. Frame-Level বনাম Clip-Level Data

ধরো:

```text
Video_001
   ├── Frame 1
   ├── Frame 2
   ├── ...
   └── Frame 1000
```

16-frame clips:

```text
Clip 1 → Frames 1–16
Clip 2 → Frames 9–24
Clip 3 → Frames 17–32
```

এখানে overlap আছে।

তাই random clip split করলে:

```text
Clip 1 → Train
Clip 2 → Test
```

দুই clip-এই প্রায় একই visual information থাকতে পারে।

এটি evaluation artificially ভালো দেখাতে পারে।

---

# 54. CCTV EDA Metadata

যদি metadata থাকে:

```text
video_id
clip_id
frame_start
frame_end
target
```

তাহলে analysis করো:

```python
df["video_id"].nunique()
```

তারপর:

```python
df.groupby("video_id")["target"].value_counts()
```

এতে video-level distribution বুঝবে।

---

# 55. Video-Level Class Distribution

```python
video_class = (
    df.groupby("video_id")["target"]
      .first()
)

print(
    video_class.value_counts()
)
```

এখানে দেখতে পারো:

```text
কতগুলো Normal video?
কতগুলো Suspicious video?
```

এটি clip count-এর চেয়েও গুরুত্বপূর্ণ হতে পারে।

---

# 56. Clip Count vs Video Count

ধরো:

```text
Normal videos       = 10
Suspicious videos   = 2
```

কিন্তু clips:

```text
Normal clips        = 10,000
Suspicious clips    = 8,000
```

Clip-level data মোটামুটি balanced মনে হতে পারে।

কিন্তু source video-level distribution:

```text
10 vs 2
```

খুব imbalance।

তাই:

> **Data hierarchy বুঝে EDA করতে হবে।**

---

# 57. M14-এর সবচেয়ে গুরুত্বপূর্ণ Mental Model

```text
                DATASET
                   ↓
           ┌───────┴───────┐
           ↓               ↓
       Structure         Quality
           ↓               ↓
       Shape            Missing
       Types            Duplicate
       Target           Invalid
           │
           └───────┬───────┘
                   ↓
               UNIVARIATE
                   ↓
              Distribution
                   ↓
               BIVARIATE
                   ↓
              Relationship
                   ↓
              MULTIVARIATE
                   ↓
              Interactions
                   ↓
             TARGET ANALYSIS
                   ↓
              Feature Signal
                   ↓
              OUTLIER CHECK
                   ↓
             CORRELATION
                   ↓
            LEAKAGE CHECK
                   ↓
             ML READINESS
                   ↓
                INSIGHTS
```

---

# 58. M14 Practice Project

এখন একটি mini EDA project করো।

Dataset:

```python
df = sns.load_dataset("titanic")
```

### Phase 1 — Understand

```text
1. shape
2. columns
3. dtypes
4. info
5. describe
```

### Phase 2 — Quality

```text
6. missing values
7. missing percentage
8. duplicates
```

### Phase 3 — Target

```text
9. survived distribution
10. survived percentage
```

### Phase 4 — Univariate

Analyze:

```text
age
fare
sibsp
parch
```

### Phase 5 — Bivariate

Analyze:

```text
sex vs survived
class vs survived
age vs survived
fare vs survived
```

### Phase 6 — Multivariate

```text
age
fare
class
sex
survived
```

Pairplot/other appropriate plots দিয়ে analysis করো।

### Phase 7 — Correlation

```text
numerical correlation
```

### Phase 8 — Insights

কমপক্ষে **10টি meaningful insight** লিখবে।

---

# 59. EDA Report Structure

Future-এ Data Analyst/ML project-এ report লিখলে এই structure follow করতে পারো:

```text
1. Dataset Overview

2. Data Quality Analysis

3. Missing Value Analysis

4. Target Distribution

5. Univariate Analysis

6. Bivariate Analysis

7. Multivariate Analysis

8. Outlier Analysis

9. Correlation Analysis

10. Feature-Target Analysis

11. Data Leakage Analysis

12. Key Findings

13. ML Recommendations
```

---

# 60. M14 Completion Checklist

```text
[ ] Dataset structure analysis
[ ] Data type analysis
[ ] Missing value analysis
[ ] Duplicate analysis
[ ] Target distribution
[ ] Class imbalance
[ ] Univariate analysis
[ ] Histogram
[ ] Boxplot
[ ] Bivariate analysis
[ ] Scatterplot
[ ] Boxplot by target
[ ] Violinplot
[ ] Multivariate analysis
[ ] Pairplot
[ ] Correlation
[ ] Heatmap
[ ] Outlier investigation
[ ] Groupby analysis
[ ] Crosstab
[ ] Feature-target analysis
[ ] Data leakage
[ ] Train/test contamination
[ ] Video-level analysis
[ ] Insight writing
[ ] ML readiness analysis
```

## M14-এর মূল শিক্ষা

**M01–M13**-তে তুমি Seaborn-এর individual tools শিখেছো।

এখন M14 থেকে mindset হবে:

```text
"Which plot should I use?"
          ↓
"Which question am I trying to answer?"
          ↓
"Which evidence does the data provide?"
          ↓
"What does this mean?"
          ↓
"How does this affect my ML model?"
```

এই transition-টাই একজন **plot learner → Data Analyst / ML practitioner** হওয়ার গুরুত্বপূর্ণ ধাপ।

**পরবর্তী: M15 — Seaborn EDA Mini Project: Real Dataset End-to-End**, যেখানে আমরা একটি dataset শুরু থেকে শেষ পর্যন্ত হাতে নিয়ে **cleaning → analysis → visualization → insights → ML preparation** করব।


---
# Seaborn M15 — End-to-End EDA Mini Project

M14-তে আমরা **EDA workflow** শিখেছি। এখন M15-এ আমরা সেটাকে একটি **complete real-world project** হিসেবে apply করব।

এই lesson-এর লক্ষ্য হলো:

> **একটি raw dataset → বুঝব → clean করব → visualize করব → relationship খুঁজব → insight বের করব → ML-এর জন্য প্রস্তুত করব।**

আমরা `Titanic` dataset ব্যবহার করব, কারণ এতে numerical + categorical + missing values + target—সবই আছে।

---

# 1. M15 Project Overview

আমাদের workflow:

```text
Titanic Dataset
      ↓
Load
      ↓
Understand
      ↓
Clean
      ↓
Missing Values
      ↓
Target Analysis
      ↓
Univariate EDA
      ↓
Bivariate EDA
      ↓
Multivariate EDA
      ↓
Outlier Analysis
      ↓
Correlation
      ↓
Feature Engineering
      ↓
ML Preparation
      ↓
Final Insights
```

---

# 2. Project Question

আমাদের main question:

> **কোন factors একজন passenger-এর survival-এর সাথে related ছিল?**

Target:

```text
survived

0 → Did not survive
1 → Survived
```

Features:

```text
age
sex
class
fare
sibsp
parch
embarked
alone
```

---

# 3. Step 1 — Import Libraries

```python
import pandas as pd
import numpy as np

import seaborn as sns
import matplotlib.pyplot as plt
```

Theme:

```python
sns.set_theme(
    style="whitegrid",
    context="notebook"
)
```

---

# 4. Step 2 — Load Dataset

```python
df = sns.load_dataset("titanic")
```

দেখি:

```python
df.head()
```

শেষের rows:

```python
df.tail()
```

---

# 5. Step 3 — Dataset Shape

```python
print("Shape:", df.shape)
```

এখানে আমরা জানব:

```text
Rows
Columns
```

---

# 6. Step 4 — Columns

```python
print(df.columns.tolist())
```

Dataset-এর columns দেখতে:

```python
for col in df.columns:
    print(col)
```

---

# 7. Step 5 — Data Types

```python
print(df.dtypes)
```

এখানে numerical এবং categorical variables আলাদা করতে পারি।

```python
numeric_cols = df.select_dtypes(
    include=np.number
).columns

categorical_cols = df.select_dtypes(
    exclude=np.number
).columns

print("Numerical:")
print(numeric_cols.tolist())

print("\nCategorical:")
print(categorical_cols.tolist())
```

---

# 8. Step 6 — Dataset Information

```python
df.info()
```

এখানে বিশেষভাবে লক্ষ্য করো:

```text
Non-Null Count
Dtype
```

যে column-এর non-null count কম, সেখানে missing value থাকতে পারে।

---

# 9. Step 7 — Statistical Summary

```python
df.describe()
```

আর categorical-এর জন্য:

```python
df.describe(
    include="object"
)
```

অথবা পুরো dataset:

```python
df.describe(
    include="all"
)
```

---

# 10. Step 8 — Missing Value Analysis

```python
df.isnull().sum()
```

Percentage:

```python
missing_pct = (
    df.isnull().mean() * 100
)

print(
    missing_pct.sort_values(
        ascending=False
    )
)
```

এখানে আমরা জানতে চাই:

```text
কোন column-এ missing আছে?
কত percentage missing?
```

---

# 11. Missing Value Visualization

```python
missing = (
    df.isnull()
      .sum()
      .sort_values(ascending=False)
)

missing = missing[missing > 0]

plt.figure(figsize=(9, 5))

sns.barplot(
    x=missing.values,
    y=missing.index
)

plt.title(
    "Missing Values by Feature"
)

plt.xlabel("Missing Count")
plt.ylabel("Feature")

plt.tight_layout()
plt.show()
```

---

# 12. Missing Value Decision

Titanic dataset-এ `age`-এ missing value আছে।

আমরা median ব্যবহার করতে পারি:

```python
df["age"] = df["age"].fillna(
    df["age"].median()
)
```

কিন্তু real project-এ blindly median fill করবে না।

তুমি প্রশ্ন করবে:

```text
Why missing?
Random?
Systematic?
Does missingness contain information?
```

---

# 13. `embarked` Missing

Categorical variable হলে mode ব্যবহার করা যায়:

```python
df["embarked"] = df["embarked"].fillna(
    df["embarked"].mode()[0]
)
```

---

# 14. `deck` Column

অনেক missing থাকলে একটি column-এর usefulness evaluate করতে হবে।

প্রথমে:

```python
print(
    df["deck"].isnull().mean() * 100
)
```

যদি missing অত্যন্ত বেশি হয় এবং featureটি useful না হয়, drop করার কথা ভাবা যায়:

```python
df = df.drop(
    columns=["deck"]
)
```

**কিন্তু আগে analysis, তারপর decision।**

---

# 15. Step 9 — Duplicate Analysis

```python
print(
    "Duplicate rows:",
    df.duplicated().sum()
)
```

Duplicate থাকলে:

```python
duplicates = df[
    df.duplicated()
]

print(duplicates)
```

তারপর business/data context অনুযায়ী সিদ্ধান্ত নেবে।

---

# 16. Step 10 — Target Analysis

আমাদের target:

```python
target = "survived"
```

Count:

```python
print(
    df["survived"].value_counts()
)
```

Percentage:

```python
print(
    df["survived"]
      .value_counts(normalize=True)
      .mul(100)
)
```

---

# 17. Target Visualization

```python
plt.figure(figsize=(7, 5))

sns.countplot(
    data=df,
    x="survived"
)

plt.title(
    "Titanic Survival Distribution"
)

plt.xlabel("Survived")
plt.ylabel("Passenger Count")

plt.tight_layout()
plt.show()
```

এখানে প্রথম insight:

```text
Survived = 0
Survived = 1
```

কোন class বেশি তা বুঝতে পারবে।

---

# 18. Better Target Labels

Raw `0/1` এর পরিবর্তে readable labels ব্যবহার করা যায়।

```python
df["survival_label"] = df[
    "survived"
].map({
    0: "Did Not Survive",
    1: "Survived"
})
```

তারপর:

```python
sns.countplot(
    data=df,
    x="survival_label"
)

plt.xticks(rotation=15)

plt.tight_layout()
plt.show()
```

---

# 19. Step 11 — Gender Analysis

প্রথম প্রশ্ন:

> Survival কি gender-এর সাথে related?

```python
sns.countplot(
    data=df,
    x="sex",
    hue="survival_label"
)

plt.title(
    "Survival by Gender"
)

plt.tight_layout()
plt.show()
```

---

# 20. Survival Rate by Gender

Count-এর চেয়ে survival rate বেশি informative।

```python
gender_survival = (
    df.groupby("sex")["survived"]
      .mean()
      .sort_values(ascending=False)
)

print(gender_survival)
```

কারণ:

```text
survived = 1
```

এর mean = survival rate।

---

# 21. Percentage Visualization

```python
gender_survival_pct = (
    gender_survival * 100
)

print(gender_survival_pct)
```

এখন তুমি বলতে পারবে:

> কোন gender group-এর survival rate বেশি ছিল।

---

# 22. Step 12 — Passenger Class

```python
sns.countplot(
    data=df,
    x="class",
    hue="survival_label"
)

plt.title(
    "Survival by Passenger Class"
)

plt.tight_layout()
plt.show()
```

---

# 23. Survival Rate by Class

```python
class_survival = (
    df.groupby("class")["survived"]
      .mean()
)

print(
    class_survival
)
```

এখানে একটি গুরুত্বপূর্ণ EDA pattern:

```text
Categorical Feature
        ↓
Groupby
        ↓
Target Mean
        ↓
Survival Rate
```

---

# 24. Class + Gender

এখন আরও interesting question:

> Class এবং gender একসাথে survival-এর সাথে কীভাবে related?

```python
sns.barplot(
    data=df,
    x="class",
    y="survived",
    hue="sex"
)

plt.title(
    "Survival Rate by Class and Gender"
)

plt.ylabel("Survival Rate")

plt.tight_layout()
plt.show()
```

এটি **multivariate EDA**।

---

# 25. Step 13 — Age Distribution

```python
plt.figure(figsize=(9, 5))

sns.histplot(
    data=df,
    x="age",
    bins=30,
    kde=True
)

plt.title(
    "Age Distribution"
)

plt.xlabel("Age")
plt.ylabel("Count")

plt.tight_layout()
plt.show()
```

এখানে দেখতে পারবে:

```text
Distribution
Central tendency
Spread
Possible skewness
```

---

# 26. Age vs Survival

```python
plt.figure(figsize=(8, 5))

sns.boxplot(
    data=df,
    x="survival_label",
    y="age"
)

plt.title(
    "Age Distribution by Survival"
)

plt.xlabel("Survival")
plt.ylabel("Age")

plt.tight_layout()
plt.show()
```

এতে দুই class-এর age distribution compare করা যায়।

---

# 27. Age + Gender + Survival

আরও detail:

```python
plt.figure(figsize=(9, 6))

sns.violinplot(
    data=df,
    x="survival_label",
    y="age",
    hue="sex"
)

plt.title(
    "Age Distribution by Survival and Gender"
)

plt.tight_layout()
plt.show()
```

এখানে:

```text
Age
 +
Survival
 +
Gender
```

একসাথে দেখা হচ্ছে।

---

# 28. Step 14 — Fare Analysis

```python
sns.histplot(
    data=df,
    x="fare",
    bins=30,
    kde=True
)

plt.title(
    "Fare Distribution"
)

plt.show()
```

সম্ভবত distribution heavily skewed হতে পারে।

---

# 29. Fare Outliers

```python
sns.boxplot(
    data=df,
    x="fare"
)

plt.title(
    "Fare Outliers"
)

plt.show()
```

এখানে extreme values দেখা যেতে পারে।

---

# 30. Fare vs Survival

```python
sns.boxplot(
    data=df,
    x="survival_label",
    y="fare"
)

plt.title(
    "Fare Distribution by Survival"
)

plt.show()
```

এখানে question:

> Higher fare passengers-এর survival rate কি different?

---

# 31. Step 15 — Family Size

Titanic dataset-এ:

```text
sibsp
parch
```

থাকে।

আমরা একটি নতুন feature বানাতে পারি:

```python
df["family_size"] = (
    df["sibsp"] +
    df["parch"] +
    1
)
```

কারণ passenger নিজেকেও count করতে হবে।

---

# 32. Family Size Distribution

```python
plt.figure(figsize=(9, 5))

sns.countplot(
    data=df,
    x="family_size"
)

plt.title(
    "Family Size Distribution"
)

plt.tight_layout()
plt.show()
```

---

# 33. Family Size vs Survival

```python
plt.figure(figsize=(10, 5))

sns.barplot(
    data=df,
    x="family_size",
    y="survived"
)

plt.title(
    "Survival Rate by Family Size"
)

plt.ylabel("Survival Rate")

plt.tight_layout()
plt.show()
```

এখানে আমরা দেখতে পারি family size এবং survival-এর relationship।

---

# 34. Step 16 — Alone Feature

আরেকটি useful feature:

```python
df["is_alone"] = (
    df["family_size"] == 1
)
```

তারপর:

```python
print(
    df["is_alone"].value_counts()
)
```

Visualization:

```python
sns.countplot(
    data=df,
    x="is_alone",
    hue="survival_label"
)

plt.title(
    "Survival by Alone Status"
)

plt.show()
```

---

# 35. Step 17 — Embarked Analysis

```python
sns.countplot(
    data=df,
    x="embarked",
    hue="survival_label"
)

plt.title(
    "Survival by Embarkation Port"
)

plt.tight_layout()
plt.show()
```

Survival rate:

```python
print(
    df.groupby("embarked")["survived"]
      .mean()
)
```

---

# 36. Step 18 — Correlation

শুধু numerical columns:

```python
corr = df.corr(
    numeric_only=True
)

print(corr)
```

Heatmap:

```python
plt.figure(figsize=(10, 8))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0,
    vmin=-1,
    vmax=1
)

plt.title(
    "Titanic Numerical Feature Correlation"
)

plt.tight_layout()
plt.show()
```

---

# 37. Correlation Interpretation

Correlation দেখে প্রশ্ন করবে:

```text
Which features are related?
How strongly?
Are some features redundant?
```

কিন্তু:

> correlation ≠ causation

এবং:

> correlation ≠ feature importance

এগুলো আলাদা concepts।

---

# 38. Step 19 — Pairplot

Selected features:

```python
pair_cols = [
    "age",
    "fare",
    "family_size",
    "survived"
]
```

তারপর:

```python
sns.pairplot(
    df[pair_cols],
    hue="survived",
    corner=True
)

plt.show()
```

এখানে multiple relationships একসাথে দেখতে পারবে।

---

# 39. Step 20 — Class Separation

ML-এর জন্য একটি গুরুত্বপূর্ণ প্রশ্ন:

> কোন feature target classes আলাদা করতে পারছে?

উদাহরণ:

```python
sns.scatterplot(
    data=df,
    x="age",
    y="fare",
    hue="survived",
    alpha=0.6
)

plt.title(
    "Age vs Fare by Survival"
)

plt.show()
```

যদি classes আলাদা cluster তৈরি করে, feature combination potentially useful হতে পারে।

---

# 40. Step 21 — Grouped EDA

একটি reusable function বানাতে পারো:

```python
def survival_rate_by(column):

    result = (
        df.groupby(column)["survived"]
          .mean()
          .sort_values(
              ascending=False
          )
    )

    print(result)
```

Use:

```python
survival_rate_by("sex")
```

```python
survival_rate_by("class")
```

```python
survival_rate_by("embarked")
```

এটি real-world analysis-এ খুব useful pattern।

---

# 41. Step 22 — Numerical Summary by Target

```python
summary = (
    df.groupby("survival_label")[
        ["age", "fare", "family_size"]
    ]
    .agg(
        ["mean", "median", "std"]
    )
)

print(summary)
```

এখন statistical summary এবং visualization দুটোই আছে।

---

# 42. Step 23 — Outlier Analysis Function

```python
def find_outliers_iqr(data, column):

    Q1 = data[column].quantile(0.25)
    Q3 = data[column].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    return data[
        (data[column] < lower) |
        (data[column] > upper)
    ]
```

Use:

```python
fare_outliers = find_outliers_iqr(
    df,
    "fare"
)

print(
    fare_outliers.shape
)
```

---

# 43. Important: Outlier Remove করব?

না, automatically নয়।

EDA থেকে আমরা শুধু বলব:

```text
Fare has extreme observations.
```

তারপর domain context অনুযায়ী সিদ্ধান্ত।

ML model-এর ক্ষেত্রে:

```text
Outlier
  ↓
Error?
  ↓
Remove/Fix

Real event?
  ↓
Keep / Transform
```

---

# 44. Step 24 — Feature Engineering

EDA-এর পর feature engineering শুরু করা যায়।

আমরা already:

```python
df["family_size"] = (
    df["sibsp"] +
    df["parch"] +
    1
)
```

করেছি।

আর:

```python
df["is_alone"] = (
    df["family_size"] == 1
)
```

---

# 45. Age Groups

Age-কে category-তে convert করা যায়:

```python
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 12, 18, 35, 60, 100],
    labels=[
        "Child",
        "Teen",
        "Young Adult",
        "Adult",
        "Senior"
    ]
)
```

তারপর:

```python
sns.countplot(
    data=df,
    x="age_group",
    hue="survival_label"
)

plt.xticks(rotation=30)

plt.tight_layout()
plt.show()
```

---

# 46. Step 25 — Target Relationship Summary

এখন কয়েকটি feature একসাথে দেখি।

```python
features = [
    "sex",
    "class",
    "embarked",
    "is_alone"
]
```

প্রতিটির জন্য:

```python
for feature in features:

    print(
        f"\n--- {feature} ---"
    )

    print(
        df.groupby(feature)["survived"]
          .mean()
          .sort_values(
              ascending=False
          )
    )
```

---

# 47. EDA Insight Writing

এখন সবচেয়ে important part।

EDA শেষে শুধু graph রেখে দিলে হবে না।

তোমাকে লিখতে হবে:

```text
Finding
Evidence
Interpretation
ML implication
```

---

# 48. Example Insight 1

ধরো analysis দেখালো gender অনুযায়ী survival rate আলাদা।

তাহলে লিখবে:

> **Gender appears to be strongly associated with survival, with substantial differences in survival rates between the two groups. Therefore, gender is likely to be an informative predictive feature.**

---

# 49. Example Insight 2

Class:

> **Passenger class shows a noticeable relationship with survival. Higher-class passengers generally exhibit higher survival rates than lower-class passengers.**

---

# 50. Example Insight 3

Fare:

> **Fare is right-skewed and contains high-value observations. The distribution of fare also differs between survivors and non-survivors, suggesting that fare may contain predictive information.**

---

# 51. Example Insight 4

Age:

> **Age distributions overlap substantially between survival classes, indicating that age alone may provide limited separation, although it may become more informative when combined with other features.**

এই ধরনের interpretation বেশি professional।

---

# 52. Step 26 — ML Readiness

EDA শেষে আমাদের dataset-এর জন্য প্রশ্ন:

```text
Missing values?
       ↓
Handled

Duplicates?
       ↓
Checked

Categorical features?
       ↓
Need encoding

Numerical features?
       ↓
Need scaling depending on model

Outliers?
       ↓
Investigated

Target?
       ↓
Identified

Leakage?
       ↓
Checked

Train/Test split?
       ↓
Ready
```

---

# 53. Feature Selection-এর আগে

EDA থেকে আমরা potential features identify করতে পারি:

```text
sex
class
age
fare
family_size
is_alone
embarked
```

কিন্তু EDA একাই final feature selection করে না।

পরের ধাপে:

```text
Feature Engineering
        ↓
Encoding
        ↓
Train/Test Split
        ↓
Baseline Model
        ↓
Feature Importance
        ↓
Evaluation
```

---

# 54. Data Leakage Reminder

একটি common mistake:

```text
Full Dataset
    ↓
Feature Engineering
    ↓
Scaling
    ↓
Train/Test
```

কিছু preprocessing operation-এ এটি leakage তৈরি করতে পারে।

সঠিক ML workflow সাধারণত:

```text
Raw Data
   ↓
Train/Test Split
   ↓
Fit preprocessing on Train
   ↓
Transform Train
   ↓
Transform Test
```

যেমন scaler-এর mean/std test set থেকে শেখা উচিত নয়।

---

# 55. Complete M15 Project Code

এখন একটি compact end-to-end version:

```python
import pandas as pd
import numpy as np

import seaborn as sns
import matplotlib.pyplot as plt


# ==================================
# 1. SETUP
# ==================================

sns.set_theme(
    style="whitegrid",
    context="notebook"
)


# ==================================
# 2. LOAD
# ==================================

df = sns.load_dataset("titanic")


# ==================================
# 3. BASIC EDA
# ==================================

print("Shape:", df.shape)

print("\nColumns:")
print(df.columns.tolist())

print("\nData Types:")
print(df.dtypes)

print("\nInfo:")
df.info()

print("\nStatistics:")
print(df.describe())


# ==================================
# 4. MISSING VALUES
# ==================================

print("\nMissing Values:")
print(df.isnull().sum())

print("\nMissing Percentage:")
print(
    df.isnull()
      .mean()
      .mul(100)
      .sort_values(
          ascending=False
      )
)


# ==================================
# 5. DUPLICATES
# ==================================

print(
    "\nDuplicates:",
    df.duplicated().sum()
)


# ==================================
# 6. HANDLE MISSING VALUES
# ==================================

df["age"] = df["age"].fillna(
    df["age"].median()
)

df["embarked"] = df["embarked"].fillna(
    df["embarked"].mode()[0]
)


# ==================================
# 7. FEATURE ENGINEERING
# ==================================

df["family_size"] = (
    df["sibsp"] +
    df["parch"] +
    1
)

df["is_alone"] = (
    df["family_size"] == 1
)


# ==================================
# 8. TARGET LABEL
# ==================================

df["survival_label"] = df[
    "survived"
].map({
    0: "Did Not Survive",
    1: "Survived"
})


# ==================================
# 9. TARGET DISTRIBUTION
# ==================================

plt.figure(figsize=(8, 5))

sns.countplot(
    data=df,
    x="survival_label"
)

plt.title(
    "Titanic Survival Distribution"
)

plt.tight_layout()
plt.show()


# ==================================
# 10. GENDER
# ==================================

plt.figure(figsize=(8, 5))

sns.countplot(
    data=df,
    x="sex",
    hue="survival_label"
)

plt.title(
    "Survival by Gender"
)

plt.tight_layout()
plt.show()


# ==================================
# 11. CLASS
# ==================================

plt.figure(figsize=(8, 5))

sns.barplot(
    data=df,
    x="class",
    y="survived",
    hue="sex"
)

plt.title(
    "Survival Rate by Class and Gender"
)

plt.ylabel("Survival Rate")

plt.tight_layout()
plt.show()


# ==================================
# 12. AGE
# ==================================

plt.figure(figsize=(9, 5))

sns.histplot(
    data=df,
    x="age",
    hue="survival_label",
    kde=True,
    bins=30
)

plt.title(
    "Age Distribution by Survival"
)

plt.tight_layout()
plt.show()


# ==================================
# 13. FARE
# ==================================

plt.figure(figsize=(9, 5))

sns.boxplot(
    data=df,
    x="survival_label",
    y="fare"
)

plt.title(
    "Fare Distribution by Survival"
)

plt.tight_layout()
plt.show()


# ==================================
# 14. FAMILY SIZE
# ==================================

plt.figure(figsize=(10, 5))

sns.barplot(
    data=df,
    x="family_size",
    y="survived"
)

plt.title(
    "Survival Rate by Family Size"
)

plt.ylabel("Survival Rate")

plt.tight_layout()
plt.show()


# ==================================
# 15. CORRELATION
# ==================================

corr = df.corr(
    numeric_only=True
)

plt.figure(figsize=(10, 8))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)

plt.title(
    "Correlation Heatmap"
)

plt.tight_layout()
plt.show()


# ==================================
# 16. PAIRPLOT
# ==================================

pair_cols = [
    "age",
    "fare",
    "family_size",
    "survived"
]

sns.pairplot(
    df[pair_cols],
    hue="survived",
    corner=True
)

plt.show()
```

---

# 56. M15 Project-এর Final EDA Questions

Project শেষ করার পরে এই প্রশ্নগুলোর answer তোমার নিজের ভাষায় লিখবে:

### Dataset

```text
1. Dataset-এর size কত?
2. Numerical features কোনগুলো?
3. Categorical features কোনগুলো?
```

### Data Quality

```text
4. Missing values কোথায়?
5. কেন missing হতে পারে?
6. Duplicate আছে?
```

### Target

```text
7. Target balanced?
8. কোন class বেশি?
```

### Feature Analysis

```text
9. Gender-এর সাথে survival-এর relationship কী?
10. Class-এর সাথে survival-এর relationship কী?
11. Age-এর distribution কেমন?
12. Fare-এর distribution কেমন?
13. Family size কি survival-এর সাথে related?
14. Alone passenger-দের survival কেমন?
```

### Advanced

```text
15. কোন feature strongest signal দিতে পারে?
16. কোন feature-এর outlier আছে?
17. কোন numerical features correlated?
18. Multicollinearity আছে?
19. Data leakage-এর সম্ভাবনা আছে?
20. কোন features ML model-এ candidate হিসেবে রাখা যায়?
```

---

# 57. M15-এর সবচেয়ে গুরুত্বপূর্ণ Skill

এখন থেকে তোমার mindset হবে না:

```text
"আজকে histogram শিখলাম।"
```

বরং:

```text
"আমার dataset-এর কোন প্রশ্নের উত্তর দরকার?"
                 ↓
"কোন visualization সেই প্রশ্নের উত্তর দেবে?"
                 ↓
"Graph কী দেখাচ্ছে?"
                 ↓
"এর statistical meaning কী?"
                 ↓
"ML model-এর জন্য এর implication কী?"
```

এটাই **EDA thinking**।

---

# 58. M01 → M15 Progress

তুমি এখন পর্যন্ত:

```text
M01 → Seaborn Introduction
M02 → Dataset & DataFrame
M03 → Distribution
M04 → Boxplot
M05 → Violinplot
M06 → Countplot & Barplot
M07 → Stripplot & Swarmplot
M08 → Heatmap & Correlation
M09 → Pairplot & Jointplot
M10 → Regression & Relationships
M11 → Categorical Visualization
M12 → FacetGrid & PairGrid
M13 → Styling & Professional Visualization
M14 → Advanced EDA Workflow
M15 → Complete EDA Mini Project
```

এখন তুমি **Seaborn-এর individual plots থেকে complete EDA workflow**-এ চলে এসেছো।

---

# M15 Completion Checklist

```text
[✓] Dataset loading
[✓] Dataset understanding
[✓] Data types
[✓] Missing value analysis
[✓] Duplicate analysis
[✓] Target analysis
[✓] Class distribution
[✓] Univariate EDA
[✓] Bivariate EDA
[✓] Multivariate EDA
[✓] Categorical analysis
[✓] Numerical analysis
[✓] Outlier analysis
[✓] Correlation
[✓] Pairplot
[✓] Feature engineering
[✓] Target relationship
[✓] Insight writing
[✓] Data leakage awareness
[✓] ML readiness
```

**M15-এর পরে সবচেয়ে logical transition হলো `M16 — Advanced Statistical EDA: Skewness, Kurtosis, Distribution Testing, Z-score, IQR, Outlier Detection & Transformation`।** এটা করলে Seaborn visualization-এর সাথে **statistics**-এর connection তৈরি হবে, যা Data Analyst এবং ML—দুই ক্ষেত্রেই খুব গুরুত্বপূর্ণ।

----
# Seaborn M16 — Advanced Statistical EDA 🔬

## Skewness, Kurtosis, Distribution Testing, Z-score, IQR, Outlier Detection & Transformation

M15 পর্যন্ত তুমি **End-to-End EDA workflow** শিখেছ। এখন M16 থেকে আমরা EDA-কে আরও **statistical + ML-oriented** করব।

আজকের lesson-এর মূল লক্ষ্য:

```text
Raw Numerical Data
       ↓
Distribution Analysis
       ↓
Skewness
       ↓
Kurtosis
       ↓
Outlier Detection
       ↓
Z-score / IQR
       ↓
Distribution Testing
       ↓
Transformation
       ↓
ML-ready Feature
```

---

# 1. Statistical EDA কেন দরকার?

ধরো তোমার dataset-এ একটা feature আছে:

```text
income
```

Values:

```text
20k
22k
25k
28k
30k
35k
40k
500k
```

এখানে `500k` অনেক বড়।

শুধু:

```python
df["income"].describe()
```

দেখলে পুরো story বোঝা যাবে না।

আমাদের জানতে হবে:

* Distribution কেমন?
* Skewed কিনা?
* Outlier আছে কিনা?
* Extreme value কতটা?
* Normal distribution-এর কাছাকাছি কিনা?
* Transformation দরকার কিনা?
* ML model-এর উপর এর effect কী?

এগুলোই M16-এর মূল বিষয়।

---

# 2. Skewness কী?

**Skewness** হলো distribution কতটা asymmetric সেটা measure করার একটি statistical measure।

সহজভাবে:

```text
Symmetric
      ↓
Left side ≈ Right side
```

আর skewed হলে একদিকে tail বেশি হয়।

তিন ধরনের case:

```text
1. Symmetric

       /\
      /  \
     /    \
----/------\----


2. Right Skewed

      /\
     /  \
    /    \________
---/-------------->


3. Left Skewed

          /\
         /  \
________/    \
<--------------
```

---

# 3. Positive / Right Skewness

যদি ডানদিকে long tail থাকে:

```text
Right tail → long
```

তাহলে:

```text
Positive Skewness
```

Example:

```text
Salary
Income
House Price
Hospital Cost
```

কারণ কিছু মানুষের income অত্যন্ত বেশি হতে পারে।

---

# 4. Negative / Left Skewness

যদি বামদিকে long tail থাকে:

```text
Left tail → long
```

তাহলে:

```text
Negative Skewness
```

---

# 5. Skewness Calculate করা

Pandas:

```python
df["fare"].skew()
```

Example:

```python
import seaborn as sns

df = sns.load_dataset("titanic")

print(df["fare"].skew())
```

---

# 6. Skewness Interpret করা

একটা সাধারণ guideline:

|  Skewness | Interpretation          |
| --------: | ----------------------- |
|       ≈ 0 | Approximately symmetric |
|   0 – 0.5 | Low positive skew       |
|   0.5 – 1 | Moderate positive skew  |
|       > 1 | Strong positive skew    |
|  -0.5 – 0 | Low negative skew       |
| -1 – -0.5 | Moderate negative skew  |
|      < -1 | Strong negative skew    |

এগুলো **strict mathematical rules না**, practical guideline।

---

# 7. Visual + Statistical Analysis

শুধু skewness value দেখবে না।

একসাথে:

```python
sns.histplot(data=df, x="fare", kde=True)
```

তারপর:

```python
print("Skewness:", df["fare"].skew())
```

Workflow:

```text
Histogram
   +
KDE
   +
Skewness
```

এতে distribution ভালোভাবে বোঝা যায়।

---

# 8. Mean vs Median এবং Skewness

Right-skewed distribution:

```text
Mode < Median < Mean
```

Example:

```text
10
11
12
13
14
15
100
```

এখানে `100` mean-কে অনেকটা ডানদিকে টেনে নেয়।

তাই:

```text
Mean > Median
```

হওয়ার সম্ভাবনা বেশি।

---

# 9. Kurtosis কী?

**Kurtosis** distribution-এর tail/extreme values-এর tendency সম্পর্কে ধারণা দেয়।

সহজভাবে:

```text
Kurtosis
   ↓
Extreme values / tail behavior
```

Skewness বলে:

> Distribution কোন দিকে asymmetric?

Kurtosis বলে:

> Distribution-এর tails কতটা heavy/extreme?

---

# 10. Kurtosis Calculate

```python
df["fare"].kurt()
```

Example:

```python
print("Kurtosis:", df["fare"].kurt())
```

---

# 11. Kurtosis Types

সাধারণভাবে:

### Mesokurtic

Normal-like tail behavior.

```text
Moderate tails
```

### Leptokurtic

Heavy tails।

```text
More extreme values
```

### Platykurtic

Light tails।

```text
Fewer extreme values
```

Pandas-এর `kurt()` সাধারণত **excess kurtosis** দেয়।

তাই:

```text
Normal distribution ≈ 0
```

---

# 12. Skewness + Kurtosis একসাথে

একটা feature-এর statistical profile:

```python
feature = df["fare"]

print("Mean:", feature.mean())
print("Median:", feature.median())
print("Std:", feature.std())
print("Skewness:", feature.skew())
print("Kurtosis:", feature.kurt())
```

এটা খুব useful EDA pattern।

---

# 13. সব Numerical Feature-এর Skewness

```python
numeric_cols = df.select_dtypes(
    include="number"
).columns

print(
    df[numeric_cols].skew()
)
```

আর:

```python
print(
    df[numeric_cols].kurt()
)
```

---

# 14. একসাথে Statistical Summary

আরও সুন্দরভাবে:

```python
stats = pd.DataFrame({
    "mean": df[numeric_cols].mean(),
    "median": df[numeric_cols].median(),
    "std": df[numeric_cols].std(),
    "skewness": df[numeric_cols].skew(),
    "kurtosis": df[numeric_cols].kurt()
})

print(stats)
```

Output concept:

```text
             mean   median    std   skewness   kurtosis
age            29       28     14      0.39       0.1
fare           32       14     49      4.78      33.4
sibsp           0        0      1      3.70      17.8
parch           0        0      1      2.75       9.0
```

এখন immediately বুঝতে পারবে:

```text
fare → highly right-skewed
sibsp → highly right-skewed
```

---

# 15. Outlier কী?

Outlier হলো এমন observation যা dataset-এর সাধারণ pattern থেকে অনেক দূরে।

Example:

```text
10
11
12
13
14
15
100
```

এখানে:

```text
100 → possible outlier
```

কিন্তু গুরুত্বপূর্ণ বিষয়:

> **Outlier মানেই ভুল data না।**

---

# 16. Outlier-এর কারণ

Outlier হতে পারে:

### 1. Data entry error

```text
Age = 250
```

### 2. Measurement error

Sensor ভুল reading দিয়েছে।

### 3. Genuine rare event

একজন billionaire-এর income।

### 4. Fraud/anomaly

Financial transaction dataset-এ।

### 5. Important ML signal

CCTV dataset-এ unusual movement হতে পারে suspicious behavior।

তাই blindly outlier delete করা যাবে না।

---

# 17. IQR Method

M04-এ তুমি IQR শিখেছিলে। এখন এটাকে statistical workflow হিসেবে ব্যবহার করব।

Formula:

```text
IQR = Q3 - Q1
```

Lower bound:

```text
Q1 - 1.5 × IQR
```

Upper bound:

```text
Q3 + 1.5 × IQR
```

---

# 18. Python IQR Detection

```python
Q1 = df["fare"].quantile(0.25)
Q3 = df["fare"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["fare"] < lower) |
    (df["fare"] > upper)
]

print(outliers)
```

---

# 19. কতগুলো Outlier আছে?

```python
print("Outliers:", len(outliers))
```

Percentage:

```python
outlier_percentage = (
    len(outliers) / len(df)
) * 100

print(outlier_percentage)
```

---

# 20. Reusable IQR Function

Professional EDA-তে function বানানো ভালো।

```python
def detect_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[
        (df[column] < lower) |
        (df[column] > upper)
    ]

    return outliers
```

Use:

```python
outliers = detect_outliers_iqr(
    df,
    "fare"
)

print(outliers)
```

---

# 21. সব Numerical Feature-এর Outlier

```python
for col in numeric_cols:

    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)

    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    count = (
        (df[col] < lower) |
        (df[col] > upper)
    ).sum()

    print(
        col,
        "→",
        count
    )
```

---

# 22. Z-score কী?

Z-score বলে একটি value mean থেকে কত standard deviation দূরে।

Formula:

$$
z = \frac{x-\mu}{\sigma}
$$

যেখানে:

```text
x = observation
μ = mean
σ = standard deviation
```

---

# 23. Example

ধরো:

```text
Mean = 50
Std = 10
Value = 80
```

তাহলে:

$$
z = \frac{80-50}{10}
$$

```text
z = 3
```

অর্থাৎ value টি:

```text
Mean থেকে 3 standard deviations দূরে।
```

---

# 24. Python Z-score

SciPy ব্যবহার করতে পারো:

```python
from scipy.stats import zscore

df["fare_zscore"] = zscore(
    df["fare"]
)
```

তারপর:

```python
print(df[["fare", "fare_zscore"]])
```

---

# 25. Z-score দিয়ে Outlier

একটি common rule:

```text
|z| > 3
```

possible extreme observation।

```python
outliers = df[
    df["fare_zscore"].abs() > 3
]

print(outliers)
```

---

# 26. IQR vs Z-score

| IQR                                | Z-score                             |
| ---------------------------------- | ----------------------------------- |
| Median/Q1/Q3 ভিত্তিক               | Mean/Std ভিত্তিক                    |
| Robust                             | Outlier-sensitive                   |
| Skewed data-তে useful              | Approximately normal data-তে useful |
| Distribution normal হওয়া দরকার নেই | Normality assumption বেশি relevant  |
| EDA-তে খুব common                  | Statistical analysis-এ useful       |

Mental model:

```text
Skewed data
    ↓
IQR

Approximately normal data
    ↓
Z-score
```

তবে বাস্তবে method selection dataset/context-এর উপর নির্ভর করবে।

---

# 27. Outlier Visualize

Boxplot:

```python
sns.boxplot(
    data=df,
    y="fare"
)

plt.show()
```

Histogram:

```python
sns.histplot(
    data=df,
    x="fare",
    kde=True
)

plt.show()
```

দুটো একসাথে করলে:

```text
Histogram → distribution
Boxplot   → outliers
```

---

# 28. Distribution Testing

এখন আরও advanced অংশ।

আমরা জানতে চাই:

> Data কি normal distribution-এর মতো?

একটি জনপ্রিয় test:

```text
Shapiro-Wilk Test
```

---

# 29. Shapiro-Wilk Test

```python
from scipy.stats import shapiro

stat, p = shapiro(
    df["age"].dropna()
)

print("Statistic:", stat)
print("p-value:", p)
```

---

# 30. Hypothesis

Normality test-এ:

```text
H0:
Data is normally distributed

H1:
Data is not normally distributed
```

Decision:

```text
p > 0.05
    ↓
H0 reject করার যথেষ্ট evidence নেই

p < 0.05
    ↓
H0 reject
    ↓
Data significantly differs from normality
```

**Important:** `p > 0.05` মানে "data অবশ্যই normal" নয়; শুধু normality reject করার যথেষ্ট evidence পাওয়া যায়নি।

---

# 31. Shapiro Test-এর Limitation

Large dataset-এ Shapiro test খুব sensitive হতে পারে।

যেমন:

```text
1,000,000 rows
```

সামান্য deviation থাকলেও:

```text
p < 0.05
```

হতে পারে।

তাই শুধু statistical test-এর উপর নির্ভর করবে না।

Use:

```text
Histogram
+
Q-Q Plot
+
Skewness
+
Statistical Test
```

---

# 32. Q-Q Plot

Q-Q plot normality বোঝার জন্য খুব useful।

```python
import scipy.stats as stats
import matplotlib.pyplot as plt

stats.probplot(
    df["age"].dropna(),
    dist="norm",
    plot=plt
)

plt.show()
```

যদি points প্রায় straight line follow করে:

```text
Approximately normal
```

---

# 33. Normal Distribution Workflow

একটি numerical feature-এর জন্য:

```text
Histogram
      ↓
KDE
      ↓
Skewness
      ↓
Kurtosis
      ↓
Q-Q Plot
      ↓
Normality Test
```

এটাই M16-এর গুরুত্বপূর্ণ workflow।

---

# 34. Log Transformation

যদি feature strongly right-skewed হয়:

```text
Income
House price
Fare
Sales
Population
```

তখন log transformation useful হতে পারে।

Formula:

$$
x' = \log(x)
$$

Python:

```python
import numpy as np

df["fare_log"] = np.log(
    df["fare"]
)
```

কিন্তু `fare = 0` থাকলে:

```python
np.log(0)
```

সমস্যা করবে।

তাই সাধারণভাবে:

```python
df["fare_log"] = np.log1p(
    df["fare"]
)
```

`log1p(x)` = `log(1+x)`।

---

# 35. Transformation-এর আগে/পরে Compare

```python
print(
    "Before:",
    df["fare"].skew()
)

print(
    "After:",
    df["fare_log"].skew()
)
```

Visual:

```python
sns.histplot(
    data=df,
    x="fare_log",
    kde=True
)

plt.show()
```

---

# 36. কেন Log Transformation?

ধরো:

```text
Original:

10
20
30
50
100
500
1000
```

অনেক বড় values distribution-কে stretch করছে।

Log transformation:

```text
log(10)
log(20)
log(30)
...
log(1000)
```

large values-এর scale compress করে।

Concept:

```text
Huge range
    ↓
Log transformation
    ↓
Compressed range
    ↓
Less skewed distribution
```

---

# 37. Square Root Transformation

আরেকটি transformation:

$$
x' = \sqrt{x}
$$

Python:

```python
df["fare_sqrt"] = np.sqrt(
    df["fare"]
)
```

সাধারণত moderate right-skewness-এ useful হতে পারে।

---

# 38. Reciprocal Transformation

আরও strong transformation:

$$
x' = \frac{1}{x}
$$

Python:

```python
df["x_reciprocal"] = (
    1 / df["x"]
)
```

তবে zero থাকলে সমস্যা হবে।

---

# 39. Box-Cox Transformation

Positive data-এর জন্য:

```python
from scipy.stats import boxcox

transformed, lambda_value = boxcox(
    df["fare"].dropna()
)

print(lambda_value)
```

Box-Cox automatically একটি suitable power transformation খুঁজতে সাহায্য করে।

---

# 40. Yeo-Johnson Transformation

যদি data-তে:

```text
zero
+
negative
+
positive
```

থাকে, Yeo-Johnson useful।

Scikit-learn:

```python
from sklearn.preprocessing import PowerTransformer

pt = PowerTransformer(
    method="yeo-johnson"
)

df["fare_yj"] = pt.fit_transform(
    df[["fare"]]
)
```

---

# 41. Transformation Comparison

| Transformation | Negative values? | Zero? | Common use            |
| -------------- | ---------------: | ----: | --------------------- |
| Log            |                ❌ |     ❌ | Strong right skew     |
| `log1p`        |                ❌ |     ✅ | Right skew + zero     |
| Square root    |                ❌ |     ✅ | Moderate skew         |
| Reciprocal     |                ❌ |     ❌ | Strong transformation |
| Box-Cox        |                ❌ |     ❌ | Positive data         |
| Yeo-Johnson    |                ✅ |     ✅ | General-purpose       |

---

# 42. Important: Outlier Remove vs Transform

ধরো:

```text
100
110
120
130
5000
```

তুমি automatically:

```python
drop()
```

করবে না।

প্রথমে প্রশ্ন করবে:

```text
5000 কি ভুল?
```

যদি genuine:

```text
Keep it
```

যদি data entry error:

```text
Correct/remove
```

যদি genuine but extreme:

```text
Maybe transform
```

---

# 43. ML-এর সাথে Connection

এটা তোমার জন্য সবচেয়ে গুরুত্বপূর্ণ অংশ।

কিছু ML algorithm outlier/skewness-এর প্রতি বেশি sensitive:

```text
Linear Regression
Logistic Regression
KNN
K-Means
SVM
Neural Networks
```

বিশেষ করে distance/gradient/scale-based models-এ extreme values সমস্যা তৈরি করতে পারে।

Tree-based models:

```text
Decision Tree
Random Forest
Gradient Boosting
```

সাধারণত skew/outlier-এর ক্ষেত্রে বেশি robust হতে পারে, যদিও feature distribution analysis তবুও গুরুত্বপূর্ণ।

---

# 44. Feature Scaling-এর সাথে সম্পর্ক

ধরো:

```text
age:
18 → 70

income:
10,000 → 1,000,000
```

Scale অনেক different।

প্রথমে:

```text
Distribution
↓
Outlier
↓
Transformation
```

তারপর প্রয়োজন হলে:

```text
StandardScaler
or
MinMaxScaler
```

Workflow:

```text
Raw Feature
     ↓
EDA
     ↓
Skewness / Outlier
     ↓
Transformation if needed
     ↓
Scaling
     ↓
ML Model
```

---

# 45. AI CCTV Project-এ M16

তোমার suspicious detection project-এর ক্ষেত্রে ধরো:

```text
motion_score
brightness
person_count
duration
velocity
frame_difference
```

তুমি করতে পারো:

```python
features = [
    "motion_score",
    "brightness",
    "person_count",
    "duration"
]

for col in features:
    print(
        col,
        "Skew:",
        df[col].skew(),
        "Kurtosis:",
        df[col].kurt()
    )
```

---

# 46. CCTV Outlier Analysis

ধরো:

```text
motion_score
```

এর distribution:

```text
Normal videos → low motion
Suspicious → high motion
```

Extreme value হতে পারে:

```text
motion_score = 999
```

প্রথমে investigate করবে:

```text
Is it a real event?
        ↓
Yes → keep
        ↓
No → data issue
```

এখানে outlier detection নিজেই anomaly detection-এর একটা basic statistical idea হিসেবে কাজ করতে পারে।

---

# 47. Class-wise Skewness

আরও useful:

```python
df.groupby("target")["motion_score"].skew()
```

অথবা:

```python
for target_value, group in df.groupby("target"):

    print(
        target_value,
        group["motion_score"].skew()
    )
```

এতে বুঝতে পারবে:

```text
Normal distribution
vs
Suspicious distribution
```

আলাদাভাবে কেমন।

---

# 48. Complete M16 Statistical EDA Code

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
from scipy.stats import shapiro
import scipy.stats as stats

# -------------------------
# Load Dataset
# -------------------------

df = sns.load_dataset("titanic")

# -------------------------
# Numerical Columns
# -------------------------

numeric_cols = df.select_dtypes(
    include="number"
).columns

# -------------------------
# Statistical Summary
# -------------------------

summary = pd.DataFrame({
    "mean": df[numeric_cols].mean(),
    "median": df[numeric_cols].median(),
    "std": df[numeric_cols].std(),
    "skewness": df[numeric_cols].skew(),
    "kurtosis": df[numeric_cols].kurt()
})

print(summary)

# -------------------------
# Distribution
# -------------------------

sns.histplot(
    data=df,
    x="fare",
    kde=True
)

plt.title("Fare Distribution")
plt.show()

# -------------------------
# Boxplot
# -------------------------

sns.boxplot(
    data=df,
    y="fare"
)

plt.title("Fare Outliers")
plt.show()

# -------------------------
# IQR
# -------------------------

Q1 = df["fare"].quantile(0.25)
Q3 = df["fare"].quantile(0.75)

IQR = Q3 - Q1

lower = Q1 - 1.5 * IQR
upper = Q3 + 1.5 * IQR

outliers = df[
    (df["fare"] < lower) |
    (df["fare"] > upper)
]

print("IQR Outliers:", len(outliers))

# -------------------------
# Z-score
# -------------------------

from scipy.stats import zscore

fare_clean = df["fare"].dropna()

z = zscore(fare_clean)

z_outliers = fare_clean[
    np.abs(z) > 3
]

print(
    "Z-score Outliers:",
    len(z_outliers)
)

# -------------------------
# Shapiro Test
# -------------------------

age = df["age"].dropna()

stat, p = shapiro(age)

print("Shapiro p-value:", p)

# -------------------------
# Q-Q Plot
# -------------------------

stats.probplot(
    age,
    dist="norm",
    plot=plt
)

plt.title("Age Q-Q Plot")
plt.show()

# -------------------------
# Log Transformation
# -------------------------

df["fare_log"] = np.log1p(
    df["fare"]
)

print(
    "Original skew:",
    df["fare"].skew()
)

print(
    "Log skew:",
    df["fare_log"].skew()
)

# -------------------------
# Transformed Distribution
# -------------------------

sns.histplot(
    data=df,
    x="fare_log",
    kde=True
)

plt.title("Log Transformed Fare")
plt.show()
```

---

# 49. Professional Statistical EDA Workflow

একজন Data Analyst/ML Engineer হিসেবে এই order follow করতে পারো:

```text
1. Numerical Features
        ↓
2. Describe
        ↓
3. Mean / Median / Std
        ↓
4. Histogram
        ↓
5. KDE
        ↓
6. Skewness
        ↓
7. Kurtosis
        ↓
8. Boxplot
        ↓
9. IQR Outlier Detection
        ↓
10. Z-score if appropriate
        ↓
11. Q-Q Plot
        ↓
12. Normality Test
        ↓
13. Transformation
        ↓
14. Re-check Distribution
        ↓
15. ML Readiness
```

---

# 50. একটা গুরুত্বপূর্ণ Decision Tree

EDA করার সময়:

```text
Feature
   ↓
Histogram
   ↓
Strong skew?
 ┌───────┴────────┐
No                Yes
↓                  ↓
Check outlier     Investigate
↓                  ↓
Normal-ish?       Outlier genuine?
                   ┌──────┴──────┐
                  Yes            No
                   ↓              ↓
              Consider         Fix/remove
              transform        data issue
                   ↓
             Re-check skew
```

---

# 51. M16-এর সবচেয়ে গুরুত্বপূর্ণ Concepts

তোমাকে এই ১০টা অবশ্যই mastery করতে হবে:

```text
1. Skewness
2. Positive skew
3. Negative skew
4. Kurtosis
5. Outlier
6. IQR method
7. Z-score
8. Normality test
9. Q-Q plot
10. Transformation
```

---

# 52. Practice — Beginner

### Task 1

`titanic` dataset load করো।

```python
df = sns.load_dataset("titanic")
```

Calculate:

```text
age skewness
fare skewness
age kurtosis
fare kurtosis
```

---

### Task 2

`fare` histogram তৈরি করো:

```text
Histogram + KDE
```

তারপর লিখবে:

```text
Distribution:
Skewness:
Kurtosis:
```

---

### Task 3

`fare`-এর IQR outlier বের করো।

---

# 53. Practice — Intermediate

### Task 4

এই columns analyze করো:

```python
[
    "age",
    "fare",
    "sibsp",
    "parch"
]
```

প্রতিটির জন্য:

```text
Mean
Median
Std
Skewness
Kurtosis
Outlier count
```

একটা DataFrame তৈরি করো।

---

# 54. Practice — Advanced

### Task 5

`fare`-এর জন্য:

```text
Original
↓
Histogram
↓
Skewness
↓
Log transformation
↓
New histogram
↓
New skewness
```

তারপর answer করো:

> Log transformation কি skewness কমিয়েছে?

---

# 55. Practice — ML Level

ধরো তোমার dataset:

```text
motion_score
brightness
person_count
duration
target
```

Analyze:

### Step 1

প্রতিটি numerical feature-এর:

```text
Skewness
Kurtosis
```

### Step 2

প্রতিটির:

```text
IQR outliers
```

### Step 3

Histogram:

```text
Normal vs Suspicious
```

### Step 4

Determine:

```text
Which features need transformation?
```

### Step 5

Transformation-এর পরে আবার:

```text
Skewness
Histogram
Boxplot
```

compare করো।

---

# 56. M16 Master Checklist ✅

নিজে বলতে পারলে M16 complete:

* [ ] Skewness কী?
* [ ] Positive skew কী?
* [ ] Negative skew কী?
* [ ] Mean vs median-এর সাথে skewness-এর relationship?
* [ ] Kurtosis কী?
* [ ] Excess kurtosis কী?
* [ ] Outlier কী?
* [ ] Outlier কেন blindly remove করা যাবে না?
* [ ] IQR কী?
* [ ] IQR দিয়ে outlier কীভাবে detect করতে হয়?
* [ ] Z-score কী?
* [ ] `|z| > 3` কী বোঝায়?
* [ ] IQR vs Z-score difference?
* [ ] Normality কী?
* [ ] Shapiro-Wilk কী?
* [ ] p-value কীভাবে interpret করতে হয়?
* [ ] Q-Q plot কী?
* [ ] Log transformation কেন করা হয়?
* [ ] `log()` vs `log1p()`?
* [ ] Square-root transformation?
* [ ] Box-Cox?
* [ ] Yeo-Johnson?
* [ ] Transformation-এর আগে/পরে কীভাবে compare করবে?
* [ ] ML model-এর সাথে skewness/outlier-এর relationship?

---

## M01 → M16 পর্যন্ত তোমার Seaborn/EDA progression

```text
M01  Seaborn Introduction
M02  Dataset & DataFrame
M03  Distribution Analysis
M04  Boxplot
M05  Violinplot
M06  Countplot & Barplot
M07  Stripplot & Swarmplot
M08  Heatmap & Correlation
M09  Pairplot & Jointplot
M10  Regression & Relationship
M11  Categorical Data Visualization
M12  FacetGrid & PairGrid
M13  Styling & Professional Visualization
M14  Advanced EDA Workflow
M15  End-to-End EDA Project
M16  Statistical EDA ⭐
```

**M16-এর মূল transition হলো:** এতদিন তুমি মূলত **“data দেখতে”** শিখেছ; এখন থেকে **“data-এর statistical behavior বুঝতে এবং ML-এর জন্য সিদ্ধান্ত নিতে”** শিখছ।

পরবর্তী logical lesson: **M17 — Feature Engineering for EDA: Binning, Encoding, Interaction Features, Date/Time Features, Ratio Features & ML-oriented Feature Analysis.**

----
# Seaborn M17 — Feature Engineering for EDA & ML 🔥

M16-এ আমরা numerical feature-এর **distribution, skewness, kurtosis, outlier, transformation** শিখেছি।

এখন M17-এ একটা খুব গুরুত্বপূর্ণ transition:

```text
Raw Dataset
    ↓
EDA
    ↓
Feature Engineering
    ↓
Better Features
    ↓
Better Visualization
    ↓
Better ML Input
```

Feature Engineering হলো raw data থেকে এমন নতুন/পরিবর্তিত features তৈরি করা যেগুলো analysis ও machine learning-এর জন্য বেশি useful।

---

# 1. Feature Engineering কী?

ধরো Titanic dataset-এ আছে:

```text
sibsp
parch
```

`SibSp` = siblings/spouses aboard
`Parch` = parents/children aboard

এই দুইটা feature থেকে আমরা বানাতে পারি:

```python
df["family_size"] = df["sibsp"] + df["parch"] + 1
```

এখন:

```text
sibsp = 1
parch = 2

family_size = 1 + 2 + 1
            = 4
```

এটাই Feature Engineering।

---

# 2. কেন Feature Engineering গুরুত্বপূর্ণ?

ধরো model-এর কাছে:

```text
sibsp
parch
```

আছে।

কিন্তু model-এর জন্য হয়তো:

```text
family_size
is_alone
```

আরও meaningful।

তাই:

```text
Raw Features
     ↓
Domain Understanding
     ↓
New Features
     ↓
Better Information
```

---

# 3. Feature Engineering-এর প্রধান ধরন

M17-এ আমরা শিখব:

```text
1. Mathematical Features
2. Ratio Features
3. Binning
4. Categorical Encoding
5. Binary Features
6. Interaction Features
7. Date/Time Features
8. String Features
9. Aggregation Features
10. Domain-specific Features
11. Feature transformation
12. Leakage prevention
```

---

# 4. Mathematical Feature Engineering

সবচেয়ে basic হলো existing columns থেকে mathematical operation।

ধরো:

```text
height
weight
```

থেকে:

```python
df["bmi"] = df["weight"] / (df["height"] ** 2)
```

এখানে:

```text
height + weight
       ↓
      BMI
```

নতুন feature তৈরি হলো।

---

# 5. Titanic Example

```python
import seaborn as sns

df = sns.load_dataset("titanic")

df["family_size"] = (
    df["sibsp"]
    + df["parch"]
    + 1
)
```

Check:

```python
print(
    df[
        ["sibsp", "parch", "family_size"]
    ].head()
)
```

---

# 6. Ratio Features

Ratio feature খুব powerful।

ধরো:

```text
income
family_size
```

তাহলে:

```python
df["income_per_person"] = (
    df["income"] /
    df["family_size"]
)
```

এটা raw income-এর চেয়ে কখনো কখনো বেশি meaningful হতে পারে।

---

# 7. Titanic Ratio Example

ধরো:

```text
fare
family_size
```

তাহলে:

```python
df["fare_per_person"] = (
    df["fare"] /
    df["family_size"]
)
```

এখন আমরা দেখতে পারি:

> Family size account করার পর কে বেশি fare দিয়েছে?

---

# 8. Zero Division Problem

Ratio feature বানানোর সময় একটা common problem:

```python
a / b
```

যদি:

```text
b = 0
```

হয় তাহলে problem।

তাই:

```python
df["ratio"] = (
    df["a"] /
    df["b"].replace(0, 1)
)
```

অথবা domain অনুযায়ী missing value handle করতে হবে।

---

# 9. Binary Feature

অনেক সময় continuous value থেকে একটা yes/no feature বানানো useful।

Titanic:

```python
df["is_alone"] = (
    df["family_size"] == 1
)
```

Result:

```text
True
False
True
False
```

এটা binary feature।

---

# 10. Binary Feature থেকে 0/1

ML-এর জন্য চাইলে:

```python
df["is_alone"] = (
    df["family_size"] == 1
).astype(int)
```

তাহলে:

```text
True  → 1
False → 0
```

---

# 11. Conditional Feature

`np.where()` খুব useful।

```python
import numpy as np

df["large_family"] = np.where(
    df["family_size"] >= 5,
    1,
    0
)
```

Meaning:

```text
family_size >= 5
        ↓
large_family = 1

otherwise
        ↓
large_family = 0
```

---

# 12. Multiple Conditions

```python
df["adult"] = np.where(
    df["age"] >= 18,
    1,
    0
)
```

আরও complex:

```python
df["high_fare"] = np.where(
    df["fare"] > 50,
    1,
    0
)
```

---

# 13. Binning কী?

Continuous numerical feature-কে কয়েকটি category/bin-এ ভাগ করা।

Example:

```text
Age
 ↓
Child
Young
Adult
Senior
```

এটাকে বলে:

**Binning / Discretization**

---

# 14. `pd.cut()`

```python
df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 12, 18, 40, 60, 100],
    labels=[
        "Child",
        "Teen",
        "Adult",
        "Middle_Age",
        "Senior"
    ]
)
```

এখন:

```text
Age = 8
→ Child

Age = 25
→ Adult

Age = 70
→ Senior
```

---

# 15. Binning Visualize করা

```python
sns.countplot(
    data=df,
    x="age_group"
)

plt.xticks(rotation=30)
plt.show()
```

তারপর survival:

```python
sns.barplot(
    data=df,
    x="age_group",
    y="survived"
)

plt.show()
```

এখানে `survived` mean হিসেবে aggregate হবে।

অর্থাৎ:

```text
bar height
=
survival rate
```

---

# 16. `pd.qcut()`

`cut()` যেখানে তুমি manually boundaries দাও, `qcut()` সেখানে quantile অনুযায়ী ভাগ করে।

```python
df["fare_group"] = pd.qcut(
    df["fare"],
    q=4,
    labels=[
        "Low",
        "Medium",
        "High",
        "Very High"
    ]
)
```

এতে roughly equal number of observations per bin পাওয়ার চেষ্টা করে।

---

# 17. `cut()` vs `qcut()`

| `cut()`                       | `qcut()`                       |
| ----------------------------- | ------------------------------ |
| Manual ranges                 | Quantiles                      |
| Domain-based                  | Distribution-based             |
| Unequal observations হতে পারে | Roughly equal observations     |
| Age group-এর জন্য useful      | Income quartile-এর জন্য useful |

Example:

```text
Age:
0–12
13–18
19–40
41–60
60+
```

এখানে:

```text
cut()
```

ভালো।

Income-এর ক্ষেত্রে:

```text
Bottom 25%
25–50%
50–75%
Top 25%
```

এখানে:

```text
qcut()
```

useful।

---

# 18. Categorical Encoding

ML model সাধারণত text বুঝতে পারে না।

ধরো:

```text
sex

male
female
```

এগুলো numerical representation দরকার।

---

# 19. Label Encoding / Binary Mapping

যদি দুইটি category থাকে:

```python
df["sex_encoded"] = df["sex"].map({
    "male": 0,
    "female": 1
})
```

Result:

```text
male   → 0
female → 1
```

Binary categorical feature-এর জন্য এটি simple approach।

---

# 20. One-Hot Encoding

ধরো:

```text
day

Thur
Fri
Sat
Sun
```

এগুলোকে:

```text
day_Thur
day_Fri
day_Sat
day_Sun
```

এভাবে represent করা যায়।

Pandas:

```python
encoded = pd.get_dummies(
    df,
    columns=["embarked"],
    drop_first=True
)
```

---

# 21. কেন `drop_first=True`?

ধরো category:

```text
A
B
C
```

One-hot:

```text
A B C
1 0 0
0 1 0
0 0 1
```

কিন্তু একটি column বাদ দিয়েও বাকি columns থেকে information infer করা যায়:

```text
B C
0 0 → A
1 0 → B
0 1 → C
```

এতে unnecessary redundancy কমতে পারে।

তবে tree-based models বা certain preprocessing pipelines-এ সব dummy রাখাও acceptable হতে পারে। Model/context অনুযায়ী সিদ্ধান্ত নিতে হবে।

---

# 22. `OneHotEncoder`

Production ML pipeline-এ scikit-learn-এর encoder বেশি appropriate:

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(
    handle_unknown="ignore"
)
```

`handle_unknown="ignore"` গুরুত্বপূর্ণ।

কারণ training data-তে না থাকা নতুন category test/production data-তে আসতে পারে।

---

# 23. Ordinal Encoding

যদি category-এর natural order থাকে:

```text
Low
Medium
High
```

তাহলে:

```python
df["level"] = df["level"].map({
    "Low": 1,
    "Medium": 2,
    "High": 3
})
```

এখানে order meaningful।

কিন্তু:

```text
Dhaka
Chittagong
Rajshahi
```

এখানে 1, 2, 3 দিলে false ordering তৈরি হবে।

---

# 24. Interaction Features

দুই বা তার বেশি feature-এর interaction থেকে নতুন feature।

Titanic example:

```python
df["family_fare"] = (
    df["family_size"] *
    df["fare"]
)
```

আরেকটি:

```python
df["age_class"] = (
    df["age"] *
    df["pclass"]
)
```

এগুলো domain অনুযায়ী useful হতে পারে।

---

# 25. কেন Interaction Feature?

ধরো:

```text
age
pclass
```

আলাদাভাবে দুইটি feature।

কিন্তু:

```text
age × pclass
```

একটি combined relationship capture করতে পারে।

Concept:

```text
Feature A
    +
Feature B
    ↓
Interaction
    ↓
New Feature
```

---

# 26. CCTV Project-এ Interaction

তোমার suspicious detection dataset-এ ধরো:

```text
motion_score
person_count
```

তাহলে:

```python
df["motion_per_person"] = (
    df["motion_score"] /
    df["person_count"].replace(0, 1)
)
```

এটা অনেক বেশি meaningful হতে পারে:

> একজন person-এর প্রতি average motion কত?

---

# 27. CCTV Duration Feature

ধরো:

```text
start_frame
end_frame
fps
```

Duration:

```python
df["duration_seconds"] = (
    df["end_frame"] -
    df["start_frame"]
) / df["fps"]
```

এখন raw frame number-এর বদলে:

```text
duration_seconds
```

হলো interpretable feature।

---

# 28. Date/Time Feature Engineering

Real-world dataset-এ date/time অত্যন্ত গুরুত্বপূর্ণ।

ধরো:

```text
timestamp
```

প্রথমে:

```python
df["timestamp"] = pd.to_datetime(
    df["timestamp"]
)
```

তারপর:

```python
df["year"] = df["timestamp"].dt.year
df["month"] = df["timestamp"].dt.month
df["day"] = df["timestamp"].dt.day
df["hour"] = df["timestamp"].dt.hour
df["weekday"] = df["timestamp"].dt.dayofweek
```

---

# 29. Time-based Features

আরও:

```python
df["is_weekend"] = (
    df["weekday"] >= 5
).astype(int)
```

এখন:

```text
Saturday/Sunday → 1
Other days      → 0
```

---

# 30. Hour → Time Category

```python
df["time_of_day"] = pd.cut(
    df["hour"],
    bins=[0, 6, 12, 18, 24],
    labels=[
        "Night",
        "Morning",
        "Afternoon",
        "Evening"
    ],
    right=False
)
```

এখন:

```text
03:00 → Night
09:00 → Morning
15:00 → Afternoon
21:00 → Evening
```

---

# 31. Cyclical Features

এটা একটু advanced এবং ML-এর জন্য খুব গুরুত্বপূর্ণ।

ধরো:

```text
hour = 23
hour = 0
```

Numerically:

```text
23 and 0
```

অনেক দূরে।

কিন্তু বাস্তবে:

```text
23:00 ↔ 00:00
```

খুব কাছাকাছি।

তাই cyclic encoding ব্যবহার করা যায়।

---

# 32. Sin/Cos Encoding

Hour:

$$
hour\_sin = \sin(2\pi \frac{hour}{24})
$$

$$
hour\_cos = \cos(2\pi \frac{hour}{24})
$$

Python:

```python
df["hour_sin"] = np.sin(
    2 * np.pi * df["hour"] / 24
)

df["hour_cos"] = np.cos(
    2 * np.pi * df["hour"] / 24
)
```

এটা advanced feature engineering-এর একটি গুরুত্বপূর্ণ technique।

---

# 33. String Feature Engineering

ধরো:

```text
email
```

থেকে:

```python
df["email_domain"] = (
    df["email"]
    .str.split("@")
    .str[-1]
)
```

Example:

```text
atiar@gmail.com
```

becomes:

```text
gmail.com
```

---

# 34. Text Length

```python
df["name_length"] = (
    df["name"]
    .str.len()
)
```

আর:

```python
df["word_count"] = (
    df["text"]
    .str.split()
    .str.len()
)
```

Text-related EDA-তে useful।

---

# 35. Titanic Name Feature

Titanic-এর `name` থেকে title বের করা যায়:

```python
df["title"] = (
    df["who"]
)
```

যদিও `titanic` dataset-এ `who` already provided আছে।

Raw dataset হলে:

```python
df["title"] = (
    df["name"]
    .str.extract(r",\s*([^.]*)\.")
)
```

Example:

```text
"Smith, Mr. John"
```

→

```text
Mr
```

---

# 36. Aggregation Features

Group-level information থেকে feature বানানো যায়।

ধরো customer dataset:

```text
customer_id
transaction_amount
```

প্রতি customer-এর:

```text
total spending
average spending
transaction count
```

বানাতে পারো।

```python
customer_stats = (
    df.groupby("customer_id")
      ["transaction_amount"]
      .agg(
          total="sum",
          average="mean",
          count="count"
      )
      .reset_index()
)
```

---

# 37. Rolling Features

Time-series data-তে:

```text
sales
```

থেকে:

```python
df["sales_7day_avg"] = (
    df["sales"]
    .rolling(7)
    .mean()
)
```

এটা recent trend বুঝতে সাহায্য করে।

---

# 38. Lag Features

Time-series ML-এর খুব গুরুত্বপূর্ণ concept:

```python
df["sales_lag_1"] = (
    df["sales"].shift(1)
)
```

Meaning:

```text
Today's row
    ↓
Yesterday's sales
```

আর:

```python
df["sales_lag_7"] = (
    df["sales"].shift(7)
)
```

মানে previous 7th observation/day-এর value।

---

# 39. Feature Engineering + Seaborn

Feature তৈরি করেই শেষ না।

নতুন feature analyze করতে হবে।

ধরো:

```python
df["family_size"] = (
    df["sibsp"] +
    df["parch"] +
    1
)
```

তারপর:

```python
sns.histplot(
    data=df,
    x="family_size"
)

plt.show()
```

---

# 40. New Feature vs Target

```python
sns.boxplot(
    data=df,
    x="survived",
    y="family_size"
)

plt.show()
```

অথবা:

```python
sns.barplot(
    data=df,
    x="family_size",
    y="survived"
)

plt.show()
```

এখন feature-এর target relationship দেখা যাচ্ছে।

---

# 41. Feature Correlation

নতুন numerical feature তৈরি করার পর:

```python
corr = df.select_dtypes(
    include="number"
).corr()
```

তারপর:

```python
sns.heatmap(
    corr,
    annot=True,
    fmt=".2f"
)

plt.show()
```

এতে নতুন feature অন্য features-এর সাথে কতটা related দেখা যায়।

---

# 42. Feature Redundancy

ধরো:

```text
sibsp
parch
family_size
```

এখানে:

```text
family_size = sibsp + parch + 1
```

তাই family_size-এর সাথে sibsp/parch-এর strong correlation থাকতে পারে।

এটা সবসময় সমস্যা নয়, কিন্তু linear models-এর ক্ষেত্রে multicollinearity consideration হতে পারে।

---

# 43. Feature Engineering-এর সবচেয়ে বড় Danger — Data Leakage 🚨

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```text
Target = survived
```

এখন এমন feature তৈরি করলে যা target-এর information directly/indirectly ব্যবহার করে:

```text
survival_status
```

তাহলে model cheating করবে।

---

# 44. Leakage Example

ধরো তোমার target:

```text
loan_default
```

আর তুমি feature বানালে:

```text
amount_recovered_after_default
```

এটা future information।

Model training-এর সময় এমন information বাস্তবে prediction-এর মুহূর্তে available থাকবে না।

এটাই leakage।

---

# 45. Train/Test Leakage

ধরো তুমি:

```python
scaler.fit(
    X
)
```

পুরো dataset-এর উপর করেছো।

তারপর:

```text
train
test
```

split করেছো।

এটা leakage হতে পারে কারণ test distribution-এর information preprocessing-এর মধ্যে ঢুকে গেছে।

Correct:

```text
Raw Data
   ↓
Train/Test Split
   ↓
Fit preprocessing on Train
   ↓
Transform Train
   ↓
Transform Test
```

---

# 46. Feature Engineering Correct Order

Professional ML workflow:

```text
Raw Dataset
      ↓
Basic EDA
      ↓
Train/Test Split
      ↓
Feature Engineering
      ↓
Preprocessing
      ↓
Feature Selection
      ↓
Model
```

তবে কিছু purely descriptive EDA transformations split-এর আগেও করা যায়। কিন্তু **target-dependent statistics, imputation values, scaling parameters, encoding learned from data**—এসব train data থেকে fit করতে হবে।

---

# 47. Feature Engineering Pipeline

Scikit-learn:

```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import (
    StandardScaler,
    OneHotEncoder
)
```

Concept:

```text
Numerical
    ↓
Imputation
    ↓
Scaling

Categorical
    ↓
Imputation
    ↓
One-Hot Encoding

        ↓
     Model
```

M17-এ মূল focus concept; pipeline detail পরবর্তী ML lessons-এ আরও গভীরে আসবে।

---

# 48. AI CCTV Feature Engineering

তোমার project-এর জন্য একটি realistic feature table:

```text
frame_count
fps
person_count
motion_score
brightness
duration
```

নতুন features:

```python
df["duration_seconds"] = (
    df["frame_count"] /
    df["fps"]
)
```

---

### Motion per person

```python
df["motion_per_person"] = (
    df["motion_score"] /
    df["person_count"].replace(0, 1)
)
```

---

### Motion intensity

ধরো duration আছে:

```python
df["motion_intensity"] = (
    df["motion_score"] /
    df["duration_seconds"].replace(0, 1)
)
```

---

### High motion flag

```python
df["high_motion"] = (
    df["motion_score"] > 0.7
).astype(int)
```

---

# 49. CCTV Feature Analysis

তারপর:

```python
sns.boxplot(
    data=df,
    x="target",
    y="motion_intensity"
)

plt.show()
```

আর:

```python
sns.histplot(
    data=df,
    x="motion_intensity",
    hue="target",
    kde=True
)

plt.show()
```

এতে প্রশ্ন করা যাবে:

> Suspicious clips-এ motion intensity কি Normal clips-এর তুলনায় বেশি?

---

# 50. Feature Engineering → EDA → ML

পুরো process:

```text
Raw CCTV Data
      ↓
Frame/Clip Extraction
      ↓
Feature Creation
      ↓
motion_intensity
duration_seconds
motion_per_person
      ↓
Distribution Analysis
      ↓
Skewness / Outlier
      ↓
Target Relationship
      ↓
Correlation
      ↓
Feature Selection
      ↓
ML/DL Model
```

---

# 51. Feature Engineering Quality Check

প্রতিবার নতুন feature বানানোর পর ৬টি প্রশ্ন:

```text
1. Feature-এর অর্থ কী?
2. Feature-এর units কী?
3. Missing values আছে?
4. Outliers আছে?
5. Target-এর সাথে relationship আছে?
6. Data leakage হচ্ছে?
```

আর একটি গুরুত্বপূর্ণ প্রশ্ন:

> Prediction করার সময় এই feature সত্যিই available থাকবে?

যদি না থাকে → feature বাদ।

---

# 52. Complete M17 Example

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("titanic")

# -------------------------
# 1. Family Size
# -------------------------

df["family_size"] = (
    df["sibsp"]
    + df["parch"]
    + 1
)

# -------------------------
# 2. Is Alone
# -------------------------

df["is_alone"] = (
    df["family_size"] == 1
).astype(int)

# -------------------------
# 3. Fare Per Person
# -------------------------

df["fare_per_person"] = (
    df["fare"] /
    df["family_size"].replace(0, 1)
)

# -------------------------
# 4. Age Group
# -------------------------

df["age_group"] = pd.cut(
    df["age"],
    bins=[0, 12, 18, 40, 60, 100],
    labels=[
        "Child",
        "Teen",
        "Adult",
        "Middle_Age",
        "Senior"
    ]
)

# -------------------------
# 5. High Fare
# -------------------------

df["high_fare"] = np.where(
    df["fare"] > 50,
    1,
    0
)

# -------------------------
# 6. Feature Analysis
# -------------------------

print(
    df[
        [
            "family_size",
            "is_alone",
            "fare_per_person",
            "age_group",
            "high_fare"
        ]
    ].head()
)

# -------------------------
# 7. Visualization
# -------------------------

sns.barplot(
    data=df,
    x="family_size",
    y="survived"
)

plt.title(
    "Family Size vs Survival Rate"
)

plt.show()
```

---

# 53. M17 Mini Project 🎯

এবার তোমার কাজ হবে একটা **Feature Engineering + EDA project**।

Dataset:

```python
df = sns.load_dataset("titanic")
```

### Step 1 — Create Features

তৈরি করবে:

```text
family_size
is_alone
fare_per_person
age_group
high_fare
```

---

### Step 2 — Analyze

প্রতিটি feature-এর জন্য চিন্তা করবে:

```text
Distribution?
Missing?
Outlier?
Target relationship?
```

---

### Step 3 — Visualization

কমপক্ষে:

```text
1. family_size → countplot
2. family_size vs survived → barplot
3. age_group → countplot
4. age_group vs survived → barplot
5. fare_per_person → histogram
6. fare_per_person vs survived → boxplot
7. correlation heatmap
```

---

# 54. Advanced Practice — CCTV 🚨

তোমার নিজের CCTV dataset-এর জন্য এই features তৈরি করার চেষ্টা করো:

```text
frame_count
fps
person_count
motion_score
brightness
```

Create:

```text
1. duration_seconds
2. motion_per_person
3. motion_intensity
4. high_motion
5. high_person_count
```

তারপর:

```text
Feature
   ↓
Histogram
   ↓
Boxplot
   ↓
Skewness
   ↓
Outlier
   ↓
Target comparison
   ↓
Correlation
```

এটা করলে তুমি শুধু Seaborn শিখবে না—**real ML dataset-এর feature analysis** করতে শিখবে।

---

# 55. M17 Cheat Sheet

### Mathematical

```python
df["new"] = df["a"] + df["b"]
```

### Ratio

```python
df["ratio"] = df["a"] / df["b"].replace(0, 1)
```

### Binary

```python
df["flag"] = (df["x"] > threshold).astype(int)
```

### Conditional

```python
df["flag"] = np.where(
    df["x"] > threshold,
    1,
    0
)
```

### Binning

```python
df["group"] = pd.cut(
    df["age"],
    bins=[0, 18, 40, 60, 100]
)
```

### Quantile Binning

```python
df["group"] = pd.qcut(
    df["income"],
    q=4
)
```

### One-Hot

```python
pd.get_dummies(
    df,
    columns=["category"],
    drop_first=True
)
```

### Date

```python
df["year"] = df["date"].dt.year
df["month"] = df["date"].dt.month
df["day"] = df["date"].dt.day
df["hour"] = df["date"].dt.hour
```

### Lag

```python
df["lag_1"] = df["value"].shift(1)
```

### Rolling

```python
df["rolling_mean"] = (
    df["value"]
    .rolling(7)
    .mean()
)
```

---

# 56. M01 → M17 Progress

```text
M01  Seaborn Introduction
M02  Dataset & DataFrame
M03  Distribution Analysis
M04  Boxplot
M05  Violinplot
M06  Countplot & Barplot
M07  Stripplot & Swarmplot
M08  Heatmap & Correlation
M09  Pairplot & Jointplot
M10  Regression & Relationship
M11  Categorical Visualization
M12  FacetGrid & PairGrid
M13  Styling & Professional Visualization
M14  Advanced EDA Workflow
M15  End-to-End EDA Project
M16  Statistical EDA
M17  Feature Engineering ⭐
```

## M17-এর মূল mental model

```text
Raw Feature
     ↓
Understand the Domain
     ↓
Create Meaningful Feature
     ↓
Check Distribution
     ↓
Check Outliers
     ↓
Check Target Relationship
     ↓
Check Correlation / Redundancy
     ↓
Check Leakage
     ↓
Keep / Transform / Remove
```

**M17 শেষ করলে তুমি শুধু `sns.xxxplot()` জানবে না; তুমি বুঝতে শুরু করবে কোন feature তৈরি করা উচিত, কেন তৈরি করা উচিত, এবং তৈরি করার পর সেটি ML-এর জন্য আদৌ useful কিনা।**

---
# Seaborn M18 — Missing Values, Data Quality & Imputation Deep Dive 🔥

M17-এ আমরা **Feature Engineering** শিখেছি। এখন M18-এ যাবো dataset-এর সবচেয়ে গুরুত্বপূর্ণ practical problem-এর দিকে:

> **Missing data, invalid data, duplicate data এবং data quality কীভাবে systematically handle করতে হয়।**

এটা Data Analysis এবং ML—দুটোর জন্যই অত্যন্ত গুরুত্বপূর্ণ।

---

# 1. M18-এ কী শিখবে?

```text
M18
│
├── Missing Values
├── NaN / None / NaT
├── Missing Value Detection
├── Missing Percentage
├── Missing Pattern
├── Visualization
├── MCAR / MAR / MNAR
├── Drop Missing Data
├── Mean / Median / Mode Imputation
├── Group-wise Imputation
├── Forward / Backward Fill
├── Interpolation
├── KNN Imputation
├── Iterative Imputation
├── Missing Indicator
├── Invalid Values
├── Duplicate Rows
├── Data Validation
├── Data Quality Report
└── ML Leakage Prevention
```

---

# 2. Missing Value কী?

ধরো dataset:

```text
Name       Age    Fare
-----------------------
Rahim      25     500
Karim      NaN    700
Hasan      30     NaN
```

এখানে:

```text
Age → Karim-এর value missing
Fare → Hasan-এর value missing
```

Pandas-এ সাধারণত:

```python
NaN
```

দেখাবে।

---

# 3. Missing Values কেন হয়?

Missing data-এর কারণ অনেক হতে পারে:

### 1. User input দেয়নি

```text
Phone = missing
```

### 2. Sensor failure

CCTV:

```text
brightness = NaN
```

### 3. Data collection problem

কোনো field collect করা হয়নি।

### 4. Database issue

Join করার পরে কিছু rows-এর value পাওয়া যায়নি।

### 5. Not applicable

যেমন:

```text
pregnancy_month = NaN
```

কোনো male record-এর ক্ষেত্রে এটি applicable নাও হতে পারে।

---

# 4. Missing Value Detect

সবচেয়ে basic:

```python
df.isnull()
```

এটা প্রতিটি cell-এর জন্য:

```text
True
False
```

দেবে।

---

# 5. Total Missing Values

```python
df.isnull().sum()
```

Example:

```text
age           177
embarked        2
deck          688
```

এখন বুঝতে পারছো কোন column-এ কত missing।

---

# 6. `isna()` vs `isnull()`

দুটো practically একই:

```python
df.isna()
```

এবং:

```python
df.isnull()
```

দুটোই ব্যবহার করতে পারো।

---

# 7. Missing Percentage

শুধু count যথেষ্ট নয়।

ধরো:

```text
Dataset = 1000 rows
Missing = 100
```

Missing percentage:

```text
10%
```

Calculate:

```python
missing_percent = (
    df.isnull().sum()
    / len(df)
) * 100

print(missing_percent)
```

---

# 8. Professional Missing Report

```python
missing_report = pd.DataFrame({
    "missing_count": df.isnull().sum(),
    "missing_percent": (
        df.isnull().sum() / len(df)
    ) * 100
})

print(missing_report)
```

শুধু missing columns:

```python
missing_report = (
    missing_report[
        missing_report["missing_count"] > 0
    ]
)

print(missing_report)
```

---

# 9. Missing Values Visualization

Seaborn দিয়ে:

```python
sns.heatmap(
    df.isnull(),
    cbar=False
)

plt.show()
```

এতে missing pattern visualভাবে দেখা যায়।

---

# 10. Titanic Dataset

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = sns.load_dataset("titanic")

print(df.shape)
print(df.isnull().sum())
```

Titanic-এ বিশেষ করে:

```text
age
deck
embarked
```

এর missing values দেখা যায়।

---

# 11. Missing Percentage Visualization

```python
missing = (
    df.isnull()
      .mean()
      .sort_values(ascending=False)
)

missing = missing[missing > 0]

sns.barplot(
    x=missing.values,
    y=missing.index
)

plt.xlabel("Missing Percentage")
plt.ylabel("Column")
plt.show()
```

এটা professional EDA report-এ useful।

---

# 12. Missing Data কতটা?

একটি practical rule হিসেবে:

```text
< 5%
→ Usually easy to handle

5–20%
→ Investigate carefully

20–50%
→ Need stronger reasoning

> 50%
→ Consider dropping or special treatment
```

⚠️ এগুলো **fixed rules নয়**।

Domain এবং feature importance-এর উপর decision নির্ভর করে।

---

# 13. Missing Value সবসময় Delete করা যাবে?

না।

ধরো:

```text
age = missing
```

তুমি পুরো row delete করলে হয়তো valuable information হারাবে।

```python
df.dropna()
```

এটা dangerous হতে পারে যদি missing অনেক হয়।

---

# 14. `dropna()`

সব missing row remove:

```python
df_clean = df.dropna()
```

Example:

```text
Original → 891 rows
After drop → অনেক কম
```

---

# 15. নির্দিষ্ট Column-এর Missing Remove

```python
df_clean = df.dropna(
    subset=["age"]
)
```

মানে:

> যাদের age missing, তাদের remove করো।

---

# 16. Column Drop

যদি কোনো column-এর missing অত্যন্ত বেশি এবং business value কম:

```python
df = df.drop(
    columns=["deck"]
)
```

কিন্তু আগে investigate:

```text
Is it useful?
Why is it missing?
Can it be recovered?
```

তারপর সিদ্ধান্ত।

---

# 17. Mean Imputation

Numerical feature:

```python
df["age"] = df["age"].fillna(
    df["age"].mean()
)
```

Example:

```text
20
25
30
NaN
35
```

Mean:

```text
27.5
```

তাহলে:

```text
NaN → 27.5
```

---

# 18. Mean কখন ব্যবহার করবে?

Mean ভালো হতে পারে যখন:

```text
Distribution ≈ symmetric
```

এবং extreme outlier খুব বেশি নেই।

---

# 19. Median Imputation

যদি data skewed হয়:

```python
df["fare"] = df["fare"].fillna(
    df["fare"].median()
)
```

Median সাধারণত outlier-এর প্রতি বেশি robust।

Mental model:

```text
Normal-ish data
    ↓
Mean

Skewed data
    ↓
Median
```

---

# 20. Mode Imputation

Categorical feature:

```python
df["embarked"] = df["embarked"].fillna(
    df["embarked"].mode()[0]
)
```

Example:

```text
Dhaka
Dhaka
Chittagong
Dhaka
NaN
```

Mode:

```text
Dhaka
```

তাই:

```text
NaN → Dhaka
```

---

# 21. Mean vs Median vs Mode

| Method | Suitable                 |
| ------ | ------------------------ |
| Mean   | Symmetric numerical data |
| Median | Skewed numerical data    |
| Mode   | Categorical data         |

---

# 22. Group-wise Imputation ⭐

এটা খুব গুরুত্বপূর্ণ।

ধরো age-এর missing value আছে।

পুরো dataset-এর median ব্যবহার না করে:

```text
Male → Male median
Female → Female median
```

ব্যবহার করা যেতে পারে।

```python
df["age"] = (
    df.groupby("sex")["age"]
      .transform(
          lambda x: x.fillna(x.median())
      )
)
```

এটা global median-এর চেয়ে context-aware হতে পারে।

---

# 23. আরও ভালো Group-wise Example

Titanic-এ:

```text
sex
+
class
```

ব্যবহার করা যায়।

```python
df["age"] = (
    df.groupby(
        ["sex", "pclass"]
    )["age"]
    .transform(
        lambda x: x.fillna(x.median())
    )
)
```

Meaning:

```text
Male + 1st class
Female + 1st class
Male + 2nd class
Female + 2nd class
...
```

প্রতিটি group-এর নিজের median।

---

# 24. কেন Group-wise Imputation?

ধরো:

```text
Group A median age = 25
Group B median age = 45
```

Global median:

```text
35
```

যদি Group A-এর missing value-তে 35 বসাও, context নষ্ট হতে পারে।

Group-wise:

```text
Group A → 25
Group B → 45
```

বেশি realistic হতে পারে।

---

# 25. Forward Fill

Time-series data:

```text
10
20
NaN
40
```

Forward fill:

```python
df["value"] = df["value"].ffill()
```

Result:

```text
10
20
20
40
```

আগের value ব্যবহার করে।

---

# 26. Backward Fill

```python
df["value"] = df["value"].bfill()
```

Result:

```text
10
20
40
40
```

পরের value ব্যবহার করে।

---

# 27. Time-Series-এ সতর্কতা ⚠️

Forward/backward fill সব dataset-এ ব্যবহার করবে না।

বিশেষ করে:

```text
future information
```

যদি বর্তমান prediction-এর মধ্যে ঢুকে যায়, তাহলে leakage হতে পারে।

Example:

```text
Today's prediction
      ↓
Tomorrow's value ব্যবহার
      ↓
Leakage
```

---

# 28. Interpolation

Time-series:

```text
10
20
NaN
40
50
```

Interpolation:

```python
df["value"] = (
    df["value"]
    .interpolate()
)
```

Result approximate:

```text
10
20
30
40
50
```

---

# 29. KNN Imputation

আরও advanced technique:

**K-Nearest Neighbors Imputation**

Idea:

```text
Missing row
    ↓
Similar rows খুঁজে বের করো
    ↓
তাদের values ব্যবহার করো
    ↓
Missing value estimate করো
```

Scikit-learn:

```python
from sklearn.impute import KNNImputer

imputer = KNNImputer(
    n_neighbors=5
)
```

তারপর numerical data:

```python
X_imputed = imputer.fit_transform(
    X
)
```

---

# 30. Iterative Imputation

এক feature-এর missing value অন্য features ব্যবহার করে estimate করা।

Concept:

```text
Age missing
   ↓
Fare
Pclass
Sex
SibSp
...
   ↓
Predict Age
```

Scikit-learn:

```python
from sklearn.experimental import (
    enable_iterative_imputer
)

from sklearn.impute import (
    IterativeImputer
)

imputer = IterativeImputer()

X_imputed = imputer.fit_transform(X)
```

---

# 31. Missing Indicator

কখনো missing হওয়াটাই information।

ধরো:

```text
income = NaN
```

Missing হওয়ার অর্থ হতে পারে:

> User income দিতে চায়নি।

তাই:

```python
df["income_missing"] = (
    df["income"].isna()
).astype(int)
```

Result:

```text
income    income_missing
50000          0
60000          0
NaN            1
70000          0
```

এখন:

```text
1 → originally missing
0 → originally present
```

---

# 32. Missingness Itself Predictive হতে পারে

CCTV example:

```text
brightness = NaN
```

যদি camera malfunction বা dark scene-এর সাথে related হয়, তাহলে:

```text
brightness_missing
```

feature-টিও useful হতে পারে।

কিন্তু এটা domain-specific—সবসময় রাখার দরকার নেই।

---

# 33. MCAR, MAR, MNAR

এখন statistical concept।

### MCAR

**Missing Completely At Random**

Missing হওয়ার সাথে observed/unobserved data-এর সম্পর্ক নেই।

```text
Randomly missing
```

---

### MAR

**Missing At Random**

Missingness observed variables-এর সাথে related।

Example:

```text
Age missing
```

কিন্তু missingness `gender` বা `class`-এর সাথে related হতে পারে।

---

### MNAR

**Missing Not At Random**

Missing হওয়ার কারণ missing value-এর নিজের unobserved value-এর সাথে related।

Example:

```text
Very high income
    ↓
Income disclose করতে চায় না
```

তাহলে missingness itself meaningful।

---

# 34. কেন MCAR/MAR/MNAR জানা দরকার?

কারণ:

```text
Missing
  ↓
Why missing?
  ↓
Choose strategy
```

Blindly:

```python
fillna(mean)
```

করলে information নষ্ট হতে পারে।

---

# 35. Duplicate Data

Missing values-এর পাশাপাশি duplicate check করতে হবে।

```python
df.duplicated().sum()
```

---

# 36. Duplicate Rows দেখো

```python
duplicates = df[
    df.duplicated()
]

print(duplicates)
```

---

# 37. Duplicate Remove

```python
df = df.drop_duplicates()
```

কিন্তু এখানেও প্রশ্ন:

> Duplicate সত্যিই duplicate?

কিছু transaction-এর একই value legitimate হতে পারে।

---

# 38. Invalid Values

Data quality-এর আরেকটি বড় অংশ।

ধরো:

```text
Age
25
30
-5
250
```

এখানে:

```text
-5
250
```

সম্ভবত invalid।

Detect:

```python
invalid_age = df[
    (df["age"] < 0) |
    (df["age"] > 120)
]
```

---

# 39. Range Validation

```python
df["age"].describe()
```

তারপর domain rule:

```python
0 <= age <= 120
```

Check:

```python
invalid = df[
    ~df["age"].between(0, 120)
]

print(invalid)
```

---

# 40. Logical Validation

ধরো:

```text
age = 5
job_experience = 20 years
```

দুটো আলাদাভাবে valid হতে পারে।

কিন্তু একসাথে:

```text
Logical inconsistency
```

তাই data validation শুধু range checking নয়।

---

# 41. CCTV Data Validation

ধরো:

```text
fps = 30
frame_count = 300
duration = 10 sec
```

Check:

$$
duration = \frac{frame\_count}{fps}
$$

```python
df["expected_duration"] = (
    df["frame_count"] /
    df["fps"]
)
```

তারপর:

```python
difference = (
    df["duration_seconds"]
    - df["expected_duration"]
)
```

যদি difference অস্বাভাবিক হয়:

```text
Possible data quality problem
```

---

# 42. Missing Values + Seaborn

Missing value নিজেও visualize করতে পারো।

```python
sns.heatmap(
    df.isna(),
    cbar=False
)

plt.title("Missing Value Pattern")
plt.show()
```

আর missing count:

```python
missing = df.isna().sum()

missing = missing[
    missing > 0
]

sns.barplot(
    x=missing.values,
    y=missing.index
)

plt.show()
```

---

# 43. Missingness vs Target

এটা ML EDA-তে খুব useful।

ধরো:

```text
age_missing
```

তৈরি করলাম:

```python
df["age_missing"] = (
    df["age"].isna()
).astype(int)
```

তারপর:

```python
sns.barplot(
    data=df,
    x="age_missing",
    y="survived"
)

plt.show()
```

যদি:

```text
Missing Age
   ↓
Different survival rate
```

হয়, তাহলে missingness potentially informative।

---

# 44. Missing Value Handling-এর Wrong Approach ❌

এটা করো না:

```python
df.fillna(0)
```

সব columns-এর জন্য।

কারণ:

```text
Age = 0
```

এর অর্থ আলাদা।

আর:

```text
Gender = 0
```

এর অর্থ আলাদা।

Missing-এর meaning column অনুযায়ী ভিন্ন।

---

# 45. আরেকটি Wrong Approach ❌

সব numerical column:

```python
df.fillna(
    df.mean()
)
```

এটা blindly করা উচিত নয়।

কারণ:

```text
Age → median হতে পারে
Income → median/log strategy হতে পারে
Time-series → interpolation হতে পারে
```

প্রতিটি feature-এর context আলাদা।

---

# 46. ML-এর জন্য সবচেয়ে গুরুত্বপূর্ণ বিষয় 🚨

Imputation-এর আগে:

```text
Train/Test Split
```

করাই safe।

ধরো:

```text
Age missing
```

তুমি পুরো dataset-এর median বের করলে:

```python
median = df["age"].median()
```

এতে test data-এর information training preprocessing-এ ঢুকে যেতে পারে।

Better:

```text
Raw Data
   ↓
Train/Test Split
   ↓
Fit imputer on Train
   ↓
Transform Train
   ↓
Transform Test
```

---

# 47. Scikit-learn SimpleImputer

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(
    strategy="median"
)
```

Train:

```python
X_train = imputer.fit_transform(
    X_train
)
```

Test:

```python
X_test = imputer.transform(
    X_test
)
```

Notice:

```text
fit_transform → train
transform      → test
```

এটা খুব important।

---

# 48. Categorical Imputer

```python
categorical_imputer = SimpleImputer(
    strategy="most_frequent"
)
```

অথবা:

```python
strategy="constant"
```

দিয়ে custom value দেওয়া যায়।

---

# 49. Numerical + Categorical Pipeline

Professional ML workflow:

```text
                 Dataset
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
     Numerical             Categorical
          ↓                   ↓
      Imputer              Imputer
          ↓                   ↓
       Scaler              Encoder
          └─────────┬─────────┘
                    ↓
                  Model
```

এটা পরবর্তী ML preprocessing lessons-এ আরও deeply আসবে।

---

# 50. Complete M18 Data Quality Report

একটি reusable function বানাতে পারো:

```python
def data_quality_report(df):

    report = pd.DataFrame({
        "dtype": df.dtypes,
        "missing_count": df.isna().sum(),
        "missing_percent": (
            df.isna().mean() * 100
        ),
        "unique_count": df.nunique(),
        "duplicate_count": [
            df[col].duplicated().sum()
            for col in df.columns
        ]
    })

    return report
```

Use:

```python
report = data_quality_report(df)

print(report)
```

---

# 51. Numerical Quality Report

```python
numeric_cols = df.select_dtypes(
    include="number"
).columns

numeric_report = pd.DataFrame({
    "mean": df[numeric_cols].mean(),
    "median": df[numeric_cols].median(),
    "std": df[numeric_cols].std(),
    "min": df[numeric_cols].min(),
    "max": df[numeric_cols].max(),
    "skewness": df[numeric_cols].skew(),
    "kurtosis": df[numeric_cols].kurt(),
    "missing": df[numeric_cols].isna().sum()
})

print(numeric_report)
```

এটা M16 + M18 combine করে।

---

# 52. Professional EDA Data Quality Workflow

```text
Raw Dataset
    ↓
Shape
    ↓
Data Types
    ↓
Missing Values
    ↓
Missing %
    ↓
Duplicate Rows
    ↓
Invalid Values
    ↓
Logical Consistency
    ↓
Outliers
    ↓
Distribution
    ↓
Imputation Strategy
    ↓
Re-check
```

---

# 53. M18 + M16 Combined Workflow

এখন তোমার EDA আরও mature হচ্ছে:

```text
                Dataset
                   ↓
             Data Quality
                   ↓
       ┌───────────┼───────────┐
       ↓           ↓           ↓
    Missing     Duplicate    Invalid
       ↓
   Imputation
       ↓
  Distribution
       ↓
 Skewness/Kurtosis
       ↓
   Outliers
       ↓
 Transformation
       ↓
 Feature Engineering
       ↓
 Target Analysis
       ↓
 ML Ready Dataset
```

---

# 54. AI CCTV-এর জন্য M18

তোমার dataset-এ ধরো:

```text
video_id
clip_id
motion_score
brightness
person_count
duration
fps
target
```

প্রথমে:

```python
print(df.isnull().sum())
```

তারপর:

```python
missing = (
    df.isnull()
      .mean()
      .sort_values(
          ascending=False
      )
) * 100

print(missing)
```

---

## Motion Score Missing

```python
df["motion_missing"] = (
    df["motion_score"].isna()
).astype(int)
```

তারপর investigate:

```python
sns.barplot(
    data=df,
    x="motion_missing",
    y="target"
)

plt.show()
```

---

# 55. CCTV-এর একটি বিশেষ সতর্কতা 🚨

তোমার dataset যদি:

```text
Video
 ↓
Frames
 ↓
16-frame clips
 ↓
Overlapping clips
```

থেকে তৈরি হয়, তাহলে একই source video-এর অনেক clip থাকবে।

যদি randomভাবে train/test split করো:

```text
Video A
 ├── Clip 1 → Train
 ├── Clip 2 → Test
 ├── Clip 3 → Train
 └── Clip 4 → Test
```

তাহলে highly similar visual information train এবং test উভয় জায়গায় চলে যেতে পারে।

এটা **data leakage** তৈরি করতে পারে।

Better:

```text
Video A → Train
Video B → Train
Video C → Test
Video D → Validation
```

অর্থাৎ **source-video-level split**।

এটা তোমার CCTV project-এর ক্ষেত্রে খুব গুরুত্বপূর্ণ।

---

# 56. M18 Practice Tasks

## Beginner

### Task 1

Titanic load করো:

```python
df = sns.load_dataset("titanic")
```

Calculate:

```text
missing count
missing %
duplicates
```

---

### Task 2

Missing heatmap তৈরি করো।

---

### Task 3

Missing percentage অনুযায়ী columns sort করো।

---

# 57. Intermediate Practice

### Task 4

`age`:

```text
Mean imputation
Median imputation
```

দুইটা DataFrame copy-তে apply করো।

তারপর compare:

```text
mean
median
skewness
```

---

### Task 5

`embarked`:

```text
Mode imputation
```

করো।

---

### Task 6

`age`-এর জন্য group-wise imputation:

```text
sex + pclass
```

ব্যবহার করো।

---

# 58. Advanced Practice

একটি data quality report তৈরি করো:

```text
column
dtype
missing_count
missing_percentage
unique_count
mean
median
std
skewness
kurtosis
```

শুধু relevant numerical columns-এ numerical statistics রাখবে।

---

# 59. ML Practice

তোমার CCTV dataset-এ:

```text
1. Missing report
2. Duplicate report
3. Invalid values
4. Missing indicators
5. Group-wise analysis
6. Imputation strategy
7. Re-check missing
8. Distribution re-check
```

তারপর লিখবে:

```text
Feature              Strategy
----------------------------------
motion_score         ?
brightness           ?
person_count         ?
duration             ?
```

প্রতিটির জন্য **কেন সেই strategy** বেছে নিয়েছো সেটাও লিখবে।

---

# 60. M18 Master Checklist ✅

নিজে explain করতে পারলে M18 complete:

* [ ] Missing value কী?
* [ ] `NaN`, `None`, `NaT` কী?
* [ ] `isnull()` / `isna()`
* [ ] Missing count
* [ ] Missing percentage
* [ ] Missing visualization
* [ ] `dropna()`
* [ ] Column dropping
* [ ] Mean imputation
* [ ] Median imputation
* [ ] Mode imputation
* [ ] Group-wise imputation
* [ ] Forward fill
* [ ] Backward fill
* [ ] Interpolation
* [ ] KNN Imputation
* [ ] Iterative Imputation
* [ ] Missing indicator
* [ ] MCAR
* [ ] MAR
* [ ] MNAR
* [ ] Duplicate detection
* [ ] Invalid value detection
* [ ] Logical validation
* [ ] Train/test leakage
* [ ] `SimpleImputer`
* [ ] `fit_transform()` vs `transform()`
* [ ] CCTV video-level split

---

# M01 → M18

```text
M01  Seaborn Introduction
M02  Dataset & DataFrame
M03  Distribution Analysis
M04  Boxplot
M05  Violinplot
M06  Countplot & Barplot
M07  Stripplot & Swarmplot
M08  Heatmap & Correlation
M09  Pairplot & Jointplot
M10  Regression & Relationship
M11  Categorical Visualization
M12  FacetGrid & PairGrid
M13  Styling & Professional Visualization
M14  Advanced EDA Workflow
M15  End-to-End EDA Project
M16  Statistical EDA
M17  Feature Engineering
M18  Data Quality & Missing Values ⭐
```

### M18-এর core mental model

```text
Missing Data
     ↓
Why is it missing?
     ↓
How much is missing?
     ↓
Is missingness informative?
     ↓
Drop / Impute / Indicator
     ↓
Re-check distribution
     ↓
Avoid leakage
     ↓
ML-ready data
```

**M19-এর logical next step:** **Feature Selection & Dimensionality Reduction — Variance, Correlation Filtering, Multicollinearity, VIF, Mutual Information, SelectKBest, PCA এবং কোন feature রাখা/বাদ দেওয়া উচিত।**

----
# M19 — Feature Selection & Dimensionality Reduction Deep Dive

M18 পর্যন্ত আমরা শিখেছি **data quality + missing values + outlier + feature engineering**। এখন খুব গুরুত্বপূর্ণ প্রশ্ন:

> **Dataset-এর সব feature কি ML model-এ রাখা উচিত?**

উত্তর: **না।**

অনেক সময় 30টা feature-এর মধ্যে 8–12টা feature-ই যথেষ্ট হতে পারে। অপ্রয়োজনীয় feature বাদ দিলে model দ্রুত train করতে পারে, noise কমতে পারে এবং interpretation সহজ হয়।

---

# 1. Feature Selection কী?

ধরো তোমার dataset:

| Feature       | Type        |
| ------------- | ----------- |
| age           | numerical   |
| income        | numerical   |
| height        | numerical   |
| weight        | numerical   |
| city          | categorical |
| education     | categorical |
| random_id     | numerical   |
| customer_code | numerical   |

এখানে `random_id` বা `customer_code` হয়তো target predict করতে কোনো useful information দেয় না।

তাই:

```text
Raw Features
     ↓
Analyze Features
     ↓
Remove useless/redundant features
     ↓
Useful Features
     ↓
ML Model
```

এটাই **Feature Selection**।

---

# 2. Feature Selection কেন দরকার?

ধরো:

```text
Dataset
100 features
1,000,000 rows
```

সব feature ব্যবহার করলে:

* training time বাড়তে পারে
* memory বেশি লাগতে পারে
* noise বাড়তে পারে
* overfitting হতে পারে
* model interpretation কঠিন হয়
* redundant information তৈরি হতে পারে

Feature selection-এর মাধ্যমে:

```text
100 features
      ↓
30 useful features
      ↓
Better / simpler model
```

তবে গুরুত্বপূর্ণ:

> Feature selection করলে সবসময় accuracy বাড়বে—এমন guarantee নেই।

---

# 3. Feature Selection-এর প্রধান 3 ধরনের Method

সাধারণভাবে:

```text
Feature Selection
│
├── Filter Methods
│
├── Wrapper Methods
│
└── Embedded Methods
```

---

# 4. Filter Method

Filter method model train না করেই statistical relationship দেখে feature নির্বাচন করে।

উদাহরণ:

* Variance Threshold
* Correlation
* Mutual Information
* Chi-square

Mental model:

```text
Features
   ↓
Statistical Test
   ↓
Useful Features
```

এগুলো সাধারণত fast।

---

# 5. Wrapper Method

Wrapper method বিভিন্ন feature subset নিয়ে model train করে performance compare করে।

উদাহরণ:

* RFE
* RFECV

```text
Features
   ↓
Select subset
   ↓
Train model
   ↓
Evaluate
   ↓
Try another subset
   ↓
Best subset
```

এগুলো computationally expensive হতে পারে।

---

# 6. Embedded Method

Feature selection model training-এর মধ্যেই হয়।

উদাহরণ:

* Lasso / L1 Regularization
* Tree-based feature importance

```text
Features
   ↓
Model Training
   ↓
Feature Importance
   ↓
Selected Features
```

---

# 7. Variance Threshold

এটি সবচেয়ে সহজ feature selection method-এর একটি।

ধরো:

```text
Feature A:
5
5
5
5
5
5
```

এর variance:

```text
0
```

Feature-এর value প্রায় কখনো পরিবর্তন হচ্ছে না।

এ ধরনের feature সাধারণত prediction-এর জন্য খুব useful নয়।

---

## Python

```python
from sklearn.feature_selection import VarianceThreshold

selector = VarianceThreshold(threshold=0)

X_selected = selector.fit_transform(X)
```

এটি zero-variance feature remove করবে।

---

# 8. Variance কী?

Variance বোঝায় data কতটা spread করছে।

```text
Low variance:

10
10
10
11
10

High variance:

2
20
5
40
15
```

তবে সাবধান:

> Low variance মানেই useless feature নয়।

একটি feature-এর variance কম হলেও সেটি target-এর জন্য গুরুত্বপূর্ণ হতে পারে।

---

# 9. Correlation Filtering

এটি খুব গুরুত্বপূর্ণ।

ধরো:

```text
age
age_in_months
```

দুটো feature প্রায় একই information দিচ্ছে।

Correlation:

```text
age ↔ age_in_months
r ≈ 1
```

এখানে একটি feature বাদ দেওয়া যেতে পারে।

---

## Correlation Matrix

```python
corr = df.corr(numeric_only=True)

print(corr)
```

Heatmap:

```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)

plt.show()
```

---

# 10. High Correlation Feature Remove

ধরো:

```text
income       salary
  │             │
  └──── 0.95 ───┘
```

দুটো highly correlated।

একটি রাখার strategy হতে পারে:

```text
income → keep
salary → remove
```

কিন্তু blindly remove করবে না।

Domain knowledge দরকার।

---

# 11. Correlation ≠ Feature Importance

এটা খুব গুরুত্বপূর্ণ।

ধরো:

```text
Feature A ↔ Target = 0.1
```

Correlation কম।

তার মানে Feature A useless—এটা বলা যাবে না।

কারণ relationship nonlinear হতে পারে।

উদাহরণ:

```text
y = x²
```

এখানে x এবং y-এর Pearson correlation কিছু ক্ষেত্রে প্রায় zero হতে পারে, কিন্তু x clearly y-এর সাথে সম্পর্কিত।

তাই:

```text
Correlation
≠
Feature Importance
```

---

# 12. Multicollinearity

যখন multiple features একে অপরের সাথে strongly related হয়, তখন তাকে **multicollinearity** বলা হয়।

উদাহরণ:

```text
salary
annual_income
monthly_income
```

এগুলো একই underlying information-এর অংশ হতে পারে।

Linear Regression-এর মতো model-এ multicollinearity সমস্যা তৈরি করতে পারে।

সমস্যা:

* coefficient unstable হতে পারে
* interpretation কঠিন হয়
* standard error বাড়তে পারে

---

# 13. VIF — Variance Inflation Factor

Multicollinearity detect করার জন্য VIF ব্যবহার করা হয়।

Concept:

```text
VIF ≈ 1
```

ভালো।

```text
VIF > 5
```

সমস্যা consider করা যায়।

```text
VIF > 10
```

strong multicollinearity-এর warning হিসেবে প্রচলিত।

এগুলো strict universal rules নয়।

---

## VIF Python

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
import pandas as pd

X = df[
    ["age", "income", "experience", "education_years"]
].dropna()

vif = pd.DataFrame()

vif["feature"] = X.columns

vif["VIF"] = [
    variance_inflation_factor(
        X.values,
        i
    )
    for i in range(X.shape[1])
]

print(vif)
```

Example output:

```text
feature             VIF
age                 2.1
income              8.4
experience          7.9
education_years     1.8
```

এখানে `income` এবং `experience` investigate করা উচিত।

---

# 14. Mutual Information

Correlation মূলত linear relationship ধরতে ভালো।

Mutual Information আরও general dependency ধরতে পারে।

Concept:

```text
X
↓
How much information does X provide about Y?
↓
Mutual Information
```

Python:

```python
from sklearn.feature_selection import mutual_info_classif

mi = mutual_info_classif(
    X,
    y,
    random_state=42
)
```

তারপর:

```python
mi_df = pd.DataFrame({
    "feature": X.columns,
    "MI": mi
})

print(
    mi_df.sort_values(
        "MI",
        ascending=False
    )
)
```

Example:

```text
feature        MI
income         0.42
age            0.31
experience     0.20
random_id      0.00
```

Higher MI সাধারণত target-এর সাথে বেশি dependency নির্দেশ করে।

তবে MI score-কে সরাসরি "effect size" হিসেবে interpret করা উচিত নয়।

---

# 15. SelectKBest

ধরো:

```text
100 features
```

তুমি top 10 রাখতে চাও।

```python
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import mutual_info_classif

selector = SelectKBest(
    score_func=mutual_info_classif,
    k=10
)

X_selected = selector.fit_transform(X, y)
```

এখানে:

```text
100 features
     ↓
MI score
     ↓
Top 10
```

---

# 16. Selected Feature Names

শুধু transformed array দেখলে feature-এর নাম পাওয়া যায় না।

তাই:

```python
mask = selector.get_support()

selected_features = X.columns[mask]

print(selected_features)
```

---

# 17. Chi-Square Feature Selection

Categorical/non-negative feature এবং classification target-এর ক্ষেত্রে `chi2` ব্যবহার করা যায়।

```python
from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import chi2

selector = SelectKBest(
    score_func=chi2,
    k=5
)

X_selected = selector.fit_transform(
    X,
    y
)
```

**Important:** `chi2` features সাধারণত non-negative হওয়া দরকার।

যেমন:

```text
0, 1, 2, 3...
```

Negative value থাকলে আগে appropriate transformation/scaling দরকার হতে পারে।

---

# 18. RFE — Recursive Feature Elimination

RFE একটি wrapper method।

ধরো:

```text
10 features
```

RFE:

```text
Train model
↓
Least important feature remove
↓
Train again
↓
Least important feature remove
↓
...
↓
Best N features
```

---

## Example

```python
from sklearn.feature_selection import RFE
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

rfe = RFE(
    estimator=model,
    n_features_to_select=5
)

X_selected = rfe.fit_transform(X, y)
```

Selected features:

```python
print(X.columns[rfe.support_])
```

Ranking:

```python
print(rfe.ranking_)
```

যেখানে:

```text
1 = selected
```

---

# 19. RFECV

RFE-তে তুমি manually বলেছ:

```python
n_features_to_select=5
```

কিন্তু কতগুলো feature রাখা উচিত সেটা যদি না জানো?

তখন:

**RFECV**

Recursive Feature Elimination + Cross Validation

```text
Features
 ↓
RFE
 ↓
Cross Validation
 ↓
Compare performance
 ↓
Best number of features
```

Example:

```python
from sklearn.feature_selection import RFECV
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(max_iter=1000)

selector = RFECV(
    estimator=model,
    cv=5,
    scoring="accuracy"
)

selector.fit(X, y)

print(selector.n_features_)
```

---

# 20. L1 / Lasso Feature Selection

L1 regularization ছোট coefficient-গুলোকে zero করতে পারে।

Concept:

```text
Feature A → coefficient = 2.4
Feature B → coefficient = 0
Feature C → coefficient = 1.8
```

`Feature B` effectively remove করা যায়।

Classification:

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(
    penalty="l1",
    solver="liblinear"
)

model.fit(X, y)
```

Coefficient:

```python
print(model.coef_)
```

যেসব coefficient zero:

```text
→ feature selection candidate
```

Regression-এর ক্ষেত্রে:

```python
from sklearn.linear_model import Lasso
```

---

# 21. Tree-Based Feature Importance

Random Forest / Gradient Boosting-এর মতো tree models feature importance দিতে পারে।

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(
    n_estimators=200,
    random_state=42
)

model.fit(X, y)

importance = pd.DataFrame({
    "feature": X.columns,
    "importance": model.feature_importances_
})

print(
    importance.sort_values(
        "importance",
        ascending=False
    )
)
```

Visualization:

```python
sns.barplot(
    data=importance.sort_values(
        "importance",
        ascending=False
    ),
    x="importance",
    y="feature"
)

plt.show()
```

---

# 22. কিন্তু Tree Importance-এরও Limitation আছে

`feature_importances_` সবসময় perfect না।

বিশেষ করে:

* correlated features
* high-cardinality features
* biased split opportunities

এর কারণে importance misleading হতে পারে।

তাই আরেকটি useful method:

## Permutation Importance

ধারণা:

```text
Original model performance
        ↓
একটি feature randomly shuffle
        ↓
Performance কত কমল?
```

যদি performance অনেক কমে:

```text
Feature important
```

---

## Python

```python
from sklearn.inspection import permutation_importance

result = permutation_importance(
    model,
    X,
    y,
    n_repeats=10,
    random_state=42
)

importance = pd.DataFrame({
    "feature": X.columns,
    "importance": result.importances_mean
})

print(
    importance.sort_values(
        "importance",
        ascending=False
    )
)
```

---

# 23. Feature Selection-এর একটি গুরুত্বপূর্ণ Rule

**Test set দিয়ে feature selection করবে না।**

ভুল:

```text
Entire Dataset
      ↓
Feature Selection
      ↓
Train/Test Split
```

এতে test information training process-এ ঢুকে যায়।

সঠিক:

```text
Raw Dataset
     ↓
Train / Validation / Test Split
     ↓
Feature Selection on Train
     ↓
Apply selection to Validation/Test
     ↓
Evaluate
```

---

# 24. Pipeline ব্যবহার করা কেন ভালো?

Example:

```python
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.feature_selection import SelectKBest
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ("imputer", SimpleImputer(strategy="median")),
    ("selector", SelectKBest(k=10)),
    ("scaler", StandardScaler()),
    ("model", LogisticRegression(max_iter=1000))
])
```

তারপর:

```python
pipeline.fit(X_train, y_train)

pred = pipeline.predict(X_test)
```

এভাবে cross-validation-এর সময়ও preprocessing/selection leakage কমানো যায়।

---

# 25. Feature Selection বনাম Feature Extraction

এখন খুব গুরুত্বপূর্ণ distinction।

### Feature Selection

Existing features থেকে কিছু feature রাখি।

```text
A B C D E F
↓
A C F
```

নতুন feature তৈরি করছি না।

---

### Feature Extraction

পুরনো feature combine করে নতুন feature তৈরি করি।

যেমন PCA:

```text
A B C D E
     ↓
    PCA
     ↓
PC1 PC2
```

এখানে `PC1`, `PC2` নতুন transformed features।

---

# 26. PCA — Principal Component Analysis

PCA হলো একটি **dimensionality reduction / feature extraction** technique।

ধরো:

```text
100 features
```

PCA:

```text
100-dimensional
      ↓
      PCA
      ↓
10 principal components
```

তথ্য যতটা সম্ভব preserve করার চেষ্টা করে।

---

# 27. PCA কীভাবে চিন্তা করবে?

ধরো দুইটা feature:

```text
       *
     *
   *
 *
```

দুটো feature strongly related।

PCA এমন একটি নতুন axis খুঁজে:

```text
       PC1
        /
       /
      /
```

যেখানে data-এর maximum variance capture হয়।

---

# 28. Principal Component

PCA-এর output:

```text
PC1
PC2
PC3
...
```

প্রতিটি component হলো original features-এর weighted combination।

ধারণাগতভাবে:

```text
PC1 =
0.5 × feature1
+ 0.7 × feature2
- 0.2 × feature3
...
```

তাই PCA-এর components সরাসরি human-readable feature নাও হতে পারে।

---

# 29. PCA-এর আগে Standardization

PCA scale-sensitive।

ধরো:

```text
age:       18–80
income:    10,000–500,000
```

Income-এর scale অনেক বড়।

তাই সাধারণত:

```text
Raw Data
   ↓
StandardScaler
   ↓
PCA
```

---

# 30. PCA Python

```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA

scaler = StandardScaler()

X_scaled = scaler.fit_transform(X)

pca = PCA(n_components=2)

X_pca = pca.fit_transform(X_scaled)

print(X_pca.shape)
```

যদি:

```text
X = (1000, 10)
```

তাহলে:

```text
X_pca = (1000, 2)
```

---

# 31. Explained Variance

PCA-এর সবচেয়ে গুরুত্বপূর্ণ concept।

```python
print(pca.explained_variance_ratio_)
```

Example:

```text
PC1 = 0.52
PC2 = 0.27
```

মানে:

```text
PC1 → 52% variance
PC2 → 27% variance
```

দুটো মিলে:

```text
79%
```

---

# 32. Cumulative Explained Variance

```python
import numpy as np

cumulative = np.cumsum(
    pca.explained_variance_ratio_
)

print(cumulative)
```

Example:

```text
PC1 → 52%
PC2 → 79%
PC3 → 88%
PC4 → 94%
PC5 → 97%
```

তাহলে 94% variance রাখতে:

```text
4 components
```

ব্যবহার করা যেতে পারে।

---

# 33. Automatically PCA Components নির্বাচন

তুমি চাইলে:

```python
pca = PCA(
    n_components=0.95
)

X_pca = pca.fit_transform(X_scaled)
```

এর অর্থ:

> এমন সংখ্যক components রাখো যাতে প্রায় 95% variance preserve হয়।

তারপর:

```python
print(pca.n_components_)
```

---

# 34. Scree Plot

প্রতিটি principal component কত variance explain করছে সেটা visualize করা যায়।

```python
pca = PCA()

X_pca = pca.fit_transform(X_scaled)

plt.figure(figsize=(8, 5))

plt.plot(
    range(1, len(pca.explained_variance_ratio_) + 1),
    pca.explained_variance_ratio_,
    marker="o"
)

plt.xlabel("Principal Component")
plt.ylabel("Explained Variance Ratio")
plt.title("PCA Scree Plot")

plt.show()
```

Cumulative:

```python
cumulative = np.cumsum(
    pca.explained_variance_ratio_
)

plt.figure(figsize=(8, 5))

plt.plot(
    range(1, len(cumulative) + 1),
    cumulative,
    marker="o"
)

plt.axhline(
    0.95,
    linestyle="--"
)

plt.xlabel("Number of Components")
plt.ylabel("Cumulative Explained Variance")

plt.show()
```

---

# 35. PCA 2D Visualization

ধরো:

```text
10 features
```

PCA করে:

```text
PC1
PC2
```

তারপর Seaborn:

```python
pca_df = pd.DataFrame(
    X_pca,
    columns=["PC1", "PC2"]
)

pca_df["target"] = y.values
```

Plot:

```python
sns.scatterplot(
    data=pca_df,
    x="PC1",
    y="PC2",
    hue="target"
)

plt.title("PCA 2D Visualization")
plt.show()
```

এখানে দেখতে পারবে:

```text
Class 0       Class 1

  • •            ○ ○
 • • •          ○ ○ ○
  •              ○
```

যদি classes আলাদা cluster তৈরি করে, dataset-এর class structure সম্পর্কে useful ধারণা পাওয়া যায়।

---

# 36. PCA + ML

Pipeline:

```text
Raw Dataset
     ↓
Data Cleaning
     ↓
Train/Test Split
     ↓
Scaling
     ↓
PCA
     ↓
ML Model
     ↓
Evaluation
```

Example:

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
from sklearn.linear_model import LogisticRegression

pipeline = Pipeline([
    ("scaler", StandardScaler()),
    ("pca", PCA(n_components=0.95)),
    ("model", LogisticRegression(max_iter=1000))
])

pipeline.fit(X_train, y_train)

accuracy = pipeline.score(
    X_test,
    y_test
)

print("Accuracy:", accuracy)
```

---

# 37. PCA-এর Advantage

PCA ব্যবহার করলে:

* dimensionality কমে
* training faster হতে পারে
* redundant information কমতে পারে
* visualization সহজ হয়
* high-dimensional data compress করা যায়

---

# 38. PCA-এর Disadvantage

সবসময় PCA ব্যবহার করা উচিত নয়।

কারণ:

```text
age
income
experience
```

বোঝা সহজ।

কিন্তু:

```text
PC1
PC2
PC3
```

এর অর্থ বোঝা কঠিন হতে পারে।

তাই interpretability গুরুত্বপূর্ণ হলে original features রাখা preferable হতে পারে।

---

# 39. Feature Selection vs PCA

| বিষয়                       | Feature Selection | PCA      |
| -------------------------- | ----------------- | -------- |
| Existing feature রাখে?     | Yes               | No       |
| নতুন feature তৈরি করে?     | No                | Yes      |
| Interpretability           | বেশি              | কম       |
| Dimensionality কমায়        | Yes               | Yes      |
| Feature meaning preserve   | Yes               | No       |
| Correlated features handle | কিছু ক্ষেত্রে     | ভালো     |
| Visualization              | ভালো              | খুব ভালো |

---

# 40. AI CCTV Dataset-এ Feature Selection

ধরো তোমার CCTV clip-level dataset:

```text
motion_score
brightness
person_count
duration
velocity
frame_difference
edge_density
object_count
camera_id
clip_id
video_id
target
```

এখন প্রথমে দেখতে হবে:

```text
camera_id
clip_id
video_id
```

এগুলো prediction feature কিনা?

অনেক ক্ষেত্রে এগুলো identifiers/metadata।

তাই blindly model-এ দেওয়া উচিত নয়।

---

# 41. CCTV Correlation Analysis

```python
features = [
    "motion_score",
    "brightness",
    "person_count",
    "duration",
    "velocity",
    "frame_difference",
    "edge_density",
    "object_count"
]

corr = df[features].corr()

plt.figure(figsize=(10, 7))

sns.heatmap(
    corr,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    center=0
)

plt.show()
```

ধরো:

```text
motion_score ↔ frame_difference = 0.91
```

তাহলে দুটো feature একই ধরনের information বহন করতে পারে।

Investigation করা উচিত।

---

# 42. CCTV Mutual Information

```python
from sklearn.feature_selection import mutual_info_classif

X = df[features]
y = df["target"]

mi = mutual_info_classif(
    X,
    y,
    random_state=42
)

mi_df = pd.DataFrame({
    "feature": features,
    "MI": mi
})

print(
    mi_df.sort_values(
        "MI",
        ascending=False
    )
)
```

এতে দেখতে পারবে কোন feature target-এর সাথে বেশি dependency রাখছে।

---

# 43. CCTV Feature Selection Strategy

আমি তোমার CCTV project-এ এই workflow recommend করব:

```text
Raw Features
     ↓
Remove IDs / leakage features
     ↓
Missing Value Analysis
     ↓
Variance Check
     ↓
Correlation Analysis
     ↓
Multicollinearity / VIF
     ↓
Mutual Information
     ↓
Model-based Importance
     ↓
Permutation Importance
     ↓
Feature Subset
     ↓
Train ML Model
     ↓
Compare Performance
```

সব method একসাথে blindly apply করা দরকার নেই।

---

# 44. সবচেয়ে গুরুত্বপূর্ণ — Leakage

ধরো:

```text
video_id
```

এটা target-এর সাথে indirectly strongly associated।

যদি suspicious videos-এর IDs এক range-এ হয় এবং normal videos অন্য range-এ হয়, model:

```text
video_id → target
```

শিখে ফেলতে পারে।

এতে test accuracy:

```text
98%
```

হলেও real-world performance খারাপ হতে পারে।

এটাকে বলি:

**Data Leakage**

---

# 45. CCTV-তে আরেকটি বড় সমস্যা

তোমার dataset যদি এমন হয়:

```text
Video A
 ├── Clip 1
 ├── Clip 2
 ├── Clip 3
 ├── Clip 4
```

এবং overlapping clips হয়:

```text
Clip 1 = frames 1–16
Clip 2 = frames 9–24
Clip 3 = frames 17–32
```

তাহলে Clip 1 এবং Clip 2 প্রায় একই visual information বহন করে।

যদি:

```text
Clip 1 → train
Clip 2 → test
```

তাহলে leakage হতে পারে।

সঠিক approach:

```text
Video-level split
       ↓
Train Videos
Validation Videos
Test Videos
       ↓
Create clips
```

এটি তোমার CCTV project-এর জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# 46. Professional Feature Selection Report

তুমি এমন report তৈরি করতে পারো:

| Feature          | Variance | Target Corr |   MI | VIF | Decision    |
| ---------------- | -------: | ----------: | ---: | --: | ----------- |
| motion_score     |     high |        0.62 | 0.41 | 2.1 | Keep        |
| brightness       |   medium |        0.18 | 0.12 | 1.4 | Keep        |
| frame_difference |     high |        0.59 | 0.39 | 8.2 | Investigate |
| video_id         |     high |       0.70* | 0.02 |   — | Remove      |
| random_id        |     high |        0.01 | 0.00 |   — | Remove      |

`*` correlation থাকলেও সেটা meaningful causal signal কিনা investigate করতে হবে।

---

# 47. M19-এর Complete Mental Model

এটা ভালোভাবে মনে রাখো:

```text
                 FEATURE SELECTION
                        │
       ┌────────────────┼────────────────┐
       ↓                ↓                ↓
     Filter           Wrapper         Embedded
       │                │                │
       ↓                ↓                ↓
 Variance          RFE/RFECV        L1/Lasso
 Correlation                       Tree Importance
 Mutual Info
 Chi-square
       │
       └──────────────┬─────────────────┘
                      ↓
              Useful Features
                      ↓
                 ML Model
```

আর:

```text
DIMENSIONALITY REDUCTION
          │
          ↓
         PCA
          │
          ↓
Standardization
          │
          ↓
Principal Components
          │
          ↓
Explained Variance
          │
          ↓
Reduced Dimensions
```

---

# 48. কখন কোন Method ব্যবহার করবে?

### Dataset ছোট/মাঝারি

```text
Correlation
+
Mutual Information
+
Model Importance
```

দিয়ে শুরু করো।

### অনেক feature

```text
Variance Threshold
↓
Correlation Filtering
↓
SelectKBest
↓
Model-based selection
```

### Linear model

```text
Correlation
+
VIF
+
L1
```

খুব useful।

### Tree model

```text
Feature Importance
+
Permutation Importance
```

### Visualization / very high dimensional data

```text
StandardScaler
↓
PCA
↓
2D/3D visualization
```

---

# 49. M19 Practical Project

Titanic dataset দিয়ে:

### Task 1

```python
df = sns.load_dataset("titanic")
```

নিচের features identify করো:

```text
Numerical
Categorical
Identifier
Potential leakage
```

### Task 2

Correlation heatmap তৈরি করো।

### Task 3

Highly correlated feature pairs বের করো।

### Task 4

VIF calculate করো।

### Task 5

Mutual Information calculate করো।

### Task 6

`SelectKBest` দিয়ে top 5 features বের করো।

### Task 7

Random Forest feature importance বের করো।

### Task 8

Permutation importance বের করো।

### Task 9

PCA করে 2D visualization তৈরি করো।

### Task 10

Compare:

```text
Original Features
vs
Selected Features
vs
PCA Features
```

তারপর Logistic Regression-এর performance compare করো।

---

# 50. M19 Completion Checklist

M19 শেষ হয়েছে কিনা নিজেকে প্রশ্ন করো:

* [ ] Feature Selection কী?
* [ ] কেন feature selection দরকার?
* [ ] Filter method কী?
* [ ] Wrapper method কী?
* [ ] Embedded method কী?
* [ ] Variance Threshold কী?
* [ ] Correlation filtering কী?
* [ ] Multicollinearity কী?
* [ ] VIF কী?
* [ ] Mutual Information কী?
* [ ] SelectKBest কী?
* [ ] Chi-square কখন ব্যবহার হয়?
* [ ] RFE কী?
* [ ] RFECV কী?
* [ ] L1 feature selection কী?
* [ ] Tree feature importance কী?
* [ ] Permutation importance কী?
* [ ] Feature selection leakage কীভাবে হয়?
* [ ] PCA কী?
* [ ] PCA-এর আগে scaling কেন?
* [ ] Explained variance কী?
* [ ] Cumulative explained variance কী?
* [ ] Scree plot কী?
* [ ] Feature Selection vs Feature Extraction বুঝতে পারো?
* [ ] CCTV dataset-এ leakage identify করতে পারো?

---

## M01 → M19 পর্যন্ত তোমার EDA progression

```text
M01  Seaborn Introduction
 ↓
M02  Dataset & DataFrame
 ↓
M03  Distribution
 ↓
M04  Boxplot
 ↓
M05  Violinplot
 ↓
M06  Countplot & Barplot
 ↓
M07  Stripplot & Swarmplot
 ↓
M08  Heatmap & Correlation
 ↓
M09  Pairplot & Jointplot
 ↓
M10  Regression Analysis
 ↓
M11  Categorical EDA
 ↓
M12  FacetGrid & PairGrid
 ↓
M13  Styling & Professional Visualization
 ↓
M14  Advanced EDA Workflow
 ↓
M15  End-to-End EDA Project
 ↓
M16  Statistical EDA
 ↓
M17  Feature Engineering
 ↓
M18  Missing Values & Data Quality
 ↓
M19  Feature Selection & Dimensionality Reduction
```

**M19-এর মূল শিক্ষা:**

> **সব feature model-এ দেওয়া নয়; প্রথমে বুঝতে হবে কোন feature useful, কোনটা redundant, কোনটা noisy এবং কোনটা leakage তৈরি করছে।**

এর পরের logical step হলো **M20 — Statistical Hypothesis Testing & A/B Analysis: Mean Comparison, t-test, Chi-square Test, ANOVA, p-value, confidence interval, effect size এবং ML/EDA-তে এগুলোর practical use।**


---
# M20 — Statistical Hypothesis Testing & A/B Analysis Deep Dive

M19-এ আমরা শিখেছি **কোন feature রাখা/বাদ দেওয়া উচিত**।
এখন M20-তে আমরা আরও গভীরে যাব:

> **দুইটা group-এর মধ্যে যে difference দেখছি, সেটা সত্যিই meaningful, নাকি শুধু random chance-এর কারণে হয়েছে?**

এটাই Statistical Hypothesis Testing-এর মূল উদ্দেশ্য।

---

# 1. Hypothesis Testing কী?

ধরো তোমার CCTV dataset-এ:

```text
Normal videos:
Average motion_score = 25

Suspicious videos:
Average motion_score = 42
```

এখন প্রশ্ন:

> Suspicious video-তে motion score সত্যিই বেশি, নাকি sample-এর কারণে এমন দেখা যাচ্ছে?

শুধু:

```python
df.groupby("target")["motion_score"].mean()
```

দেখলেই answer পাওয়া যায় না।

আমাদের statistical test দরকার।

---

# 2. Statistical Hypothesis Testing-এর Mental Model

```text
Data
 ↓
Question
 ↓
H₀ / H₁
 ↓
Statistical Test
 ↓
Test Statistic
 ↓
p-value
 ↓
Decision
 ↓
Business / ML Interpretation
```

---

# 3. Null Hypothesis — H₀

**Null Hypothesis** হলো:

> কোনো meaningful difference/relationship নেই।

উদাহরণ:

```text
H₀:
Normal এবং Suspicious group-এর
average motion_score একই।
```

---

# 4. Alternative Hypothesis — H₁

Alternative hypothesis বলে:

> Difference/relationship আছে।

```text
H₁:
Normal এবং Suspicious group-এর
average motion_score একই নয়।
```

---

# 5. Simple Example

ধরো:

```text
Group A mean = 50
Group B mean = 55
```

Difference:

```text
5
```

কিন্তু প্রশ্ন:

```text
এই 5 কি statistically significant?
```

এখানেই hypothesis testing।

---

# 6. p-value কী?

p-value খুব গুরুত্বপূর্ণ।

সহজভাবে:

> **যদি H₀ সত্য হয়, তাহলে observed result বা তার চেয়েও extreme result পাওয়ার probability কত?**

যদি:

```text
p-value = 0.01
```

তাহলে H₀ সত্য ধরে এমন extreme result পাওয়া relatively unlikely।

---

# 7. Significance Level — α

সাধারণভাবে:

```text
α = 0.05
```

ব্যবহার করা হয়।

Decision rule:

```text
p < 0.05
↓
Reject H₀
```

আর:

```text
p >= 0.05
↓
Fail to reject H₀
```

**"Accept H₀" না বলে সাধারণত "Fail to reject H₀" বলা বেশি সঠিক।**

---

# 8. Example

ধরো:

```text
p = 0.02
```

তাহলে:

```text
0.02 < 0.05
```

সুতরাং:

```text
Reject H₀
```

Interpretation:

> Evidence suggests that the groups are statistically different.

---

যদি:

```text
p = 0.35
```

তাহলে:

```text
0.35 > 0.05
```

তাই:

```text
Fail to reject H₀
```

অর্থাৎ observed difference statistically convincing নয়।

---

# 9. Important Warning

```text
p < 0.05
```

মানে **difference অবশ্যই practically important**—এমন নয়।

Example:

```text
Group A mean = 50.00
Group B mean = 50.02
```

এক কোটি observations থাকলে tiny difference-ও statistically significant হতে পারে।

তাই:

```text
Statistical Significance
+
Practical Significance
```

দুটোই দেখতে হবে।

---

# 10. Confidence Interval

Confidence interval হলো parameter-এর plausible range বোঝার একটি উপায়।

Example:

```text
Mean difference = 5.2
95% CI = [2.1, 8.3]
```

Interpretation:

> Estimated difference positive, এবং plausible range zero-এর বাইরে।

এটি শুধু p-value-এর চেয়ে বেশি informative হতে পারে।

---

# 11. Mean Comparison

ধরো:

```python id="x4j1j9"
import seaborn as sns

df = sns.load_dataset("tips")
```

Male এবং female-এর average bill:

```python id="a8d5ce"
df.groupby("sex")["total_bill"].mean()
```

---

# 12. Visualization আগে করো

Statistical test করার আগে data visualize করা খুব ভালো practice।

```python id="p7h0vz"
sns.boxplot(
    data=df,
    x="sex",
    y="total_bill"
)

plt.show()
```

তারপর distribution:

```python id="n4l9qv"
sns.histplot(
    data=df,
    x="total_bill",
    hue="sex",
    kde=True
)

plt.show()
```

Mental model:

```text
Visualize
   ↓
Understand data
   ↓
Choose test
   ↓
Run test
```

---

# 13. Independent Two-Sample t-test

যখন দুইটি independent group-এর mean compare করতে চাই।

Example:

```text
Group A → Normal
Group B → Suspicious
```

Hypothesis:

```text
H₀: μA = μB
H₁: μA ≠ μB
```

---

## Python

```python id="v1o1jo"
from scipy.stats import ttest_ind

group_a = df[df["sex"] == "Male"]["total_bill"]
group_b = df[df["sex"] == "Female"]["total_bill"]

stat, p = ttest_ind(
    group_a,
    group_b,
    equal_var=False
)

print("t-statistic:", stat)
print("p-value:", p)
```

`equal_var=False` ব্যবহার করলে Welch's t-test পাওয়া যায়, যা unequal variance-এর ক্ষেত্রে সাধারণত safer choice।

---

# 14. t-test Result Interpret

ধরো:

```text
t-statistic = 2.35
p-value = 0.021
```

যেহেতু:

```text
0.021 < 0.05
```

তাই:

```text
Reject H₀
```

Conclusion:

> দুই group-এর mean-এর মধ্যে statistically significant difference-এর evidence আছে।

---

# 15. One-Sample t-test

একটি sample-এর mean কোনো নির্দিষ্ট value থেকে আলাদা কিনা দেখতে ব্যবহার করা হয়।

ধরো:

```text
Expected mean = 100
```

Test:

```python id="y5l6yn"
from scipy.stats import ttest_1samp

stat, p = ttest_1samp(
    df["total_bill"],
    popmean=20
)

print(p)
```

---

# 16. Paired t-test

যখন **একই observation-এর before এবং after measurement** থাকে।

Example:

```text
Student
Before training score
After training score
```

এখানে দুই group independent নয়।

```python id="ndt4u0"
from scipy.stats import ttest_rel

stat, p = ttest_rel(
    before,
    after
)
```

Mental model:

```text
Independent:
Person A vs Person B

Paired:
Same Person Before vs After
```

---

# 17. t-test কখন ব্যবহার করবে?

দুই group-এর numerical variable-এর mean compare করতে:

```text
Two independent groups
+
Numerical outcome
```

যেমন:

```text
Male vs Female → income
Normal vs Suspicious → motion_score
Treatment vs Control → blood_pressure
```

---

# 18. t-test-এর Assumptions

বিশেষ করে classical t-test-এর ক্ষেত্রে:

1. observations appropriately independent
2. outcome numerical/continuous
3. distribution roughly suitable, especially for small samples
4. extreme outlier না থাকা গুরুত্বপূর্ণ
5. equal variance assumption traditional Student's t-test-এ গুরুত্বপূর্ণ

তাই data আগে দেখতে হবে।

---

# 19. Non-parametric Alternative — Mann-Whitney U

যদি data strongly skewed হয় বা assumptions problematic হয়:

```python id="5s4o9h"
from scipy.stats import mannwhitneyu

stat, p = mannwhitneyu(
    group_a,
    group_b,
    alternative="two-sided"
)

print("p-value:", p)
```

এটি দুই independent group-এর distribution/rank-based difference পরীক্ষা করে।

একটি গুরুত্বপূর্ণ বিষয়:

> Mann-Whitney U-কে সবসময় "median test" হিসেবে interpret করা ঠিক নয়; distribution shapes/assumptions-এর ওপর interpretation নির্ভর করে।

---

# 20. t-test vs Mann-Whitney

| Situation                                | Test                    |
| ---------------------------------------- | ----------------------- |
| Two independent groups                   | t-test                  |
| Paired observations                      | Paired t-test           |
| Strong non-normality / ordinal-like data | Mann-Whitney            |
| Before-after                             | Paired t-test           |
| Small sample + problematic assumptions   | Consider non-parametric |

---

# 21. Chi-Square Test

এখন numerical mean নয়।

ধরো:

```text
Gender
Survived
```

দুটো categorical variable।

Question:

> Gender এবং survival-এর মধ্যে relationship আছে কি?

এখানে **Chi-square test of independence** ব্যবহার করা যায়।

---

# 22. Contingency Table

```python id="w7py2k"
table = pd.crosstab(
    df["sex"],
    df["survived"]
)

print(table)
```

Example:

```text
survived    0    1
sex
female      81  233
male       468  109
```

---

# 23. Chi-Square Python

```python id="4h9tne"
from scipy.stats import chi2_contingency

chi2, p, dof, expected = chi2_contingency(
    table
)

print("Chi-square:", chi2)
print("p-value:", p)
print("dof:", dof)
```

---

# 24. Chi-Square Interpretation

যদি:

```text
p < 0.05
```

তাহলে:

```text
Reject H₀
```

Conclusion:

> দুই categorical variable independent নয়—association-এর evidence আছে।

কিন্তু:

> Association ≠ Causation.

---

# 25. Expected Frequency

Chi-square internally observed frequency-এর সাথে expected frequency compare করে।

```text
Observed
vs
Expected
```

যদি H₀ সত্য হয়, expected counts কী হতে পারত—সেটা হিসাব করা হয়।

---

# 26. Chi-Square Assumption

Expected cell counts খুব ছোট হলে ordinary chi-square approximation সমস্যা করতে পারে।

বিশেষ করে 2×2 table-এ small counts থাকলে **Fisher's Exact Test** consider করা যায়।

```python id="6a9d0c"
from scipy.stats import fisher_exact

odds_ratio, p = fisher_exact(table)

print(p)
```

---

# 27. ANOVA

এখন ধরো দুই group নয়:

```text
Group A
Group B
Group C
Group D
```

সবগুলোর mean compare করতে চাই।

তখন:

**One-Way ANOVA**

---

# 28. Example

Titanic-এর মতো dataset বাদ দিয়ে simple example:

```text
Class 1
Class 2
Class 3
```

প্রতিটি class-এর average score compare করতে চাই।

```python id="8z3jyk"
from scipy.stats import f_oneway

group1 = df[df["day"] == "Thur"]["total_bill"]
group2 = df[df["day"] == "Fri"]["total_bill"]
group3 = df[df["day"] == "Sat"]["total_bill"]
group4 = df[df["day"] == "Sun"]["total_bill"]

stat, p = f_oneway(
    group1,
    group2,
    group3,
    group4
)

print("F-statistic:", stat)
print("p-value:", p)
```

---

# 29. ANOVA Result

যদি:

```text
p < 0.05
```

তাহলে:

> অন্তত একটি group-এর mean অন্য group-এর থেকে আলাদা হওয়ার evidence আছে।

কিন্তু ANOVA বলবে না:

```text
Exactly which groups differ?
```

এর জন্য post-hoc test দরকার।

---

# 30. Post-Hoc Test — Tukey HSD

```python id="m8e5fv"
from statsmodels.stats.multicomp import pairwise_tukeyhsd

result = pairwise_tukeyhsd(
    endog=df["total_bill"],
    groups=df["day"],
    alpha=0.05
)

print(result)
```

এতে pairwise comparison পাওয়া যাবে।

যেমন:

```text
Thur vs Fri
Thur vs Sat
Thur vs Sun
Fri vs Sat
...
```

---

# 31. ANOVA Mental Model

```text
2 groups
   ↓
t-test

3+ groups
   ↓
ANOVA
   ↓
Significant?
   ↓
Post-hoc
   ↓
Which groups differ?
```

---

# 32. Effect Size

এখন খুব গুরুত্বপূর্ণ একটি concept।

p-value বলে:

> Difference statistically detectable কি না?

Effect size বলে:

> Difference কতটা বড়?

দুটো আলাদা।

---

# 33. Cohen's d

দুই group-এর mean difference-এর standardized effect size হিসেবে Cohen's d বহুল ব্যবহৃত।

Concept:

```text
d =
difference in means
------------------
pooled standard deviation
```

Rough guideline:

```text
0.2 → small
0.5 → medium
0.8 → large
```

এগুলো context-dependent guidelines, universal laws নয়।

---

# 34. Python — Cohen's d

```python id="1xg2x8"
import numpy as np

def cohens_d(x, y):
    nx = len(x)
    ny = len(y)

    pooled_std = np.sqrt(
        (
            (nx - 1) * x.std(ddof=1)**2 +
            (ny - 1) * y.std(ddof=1)**2
        )
        /
        (nx + ny - 2)
    )

    return (
        (x.mean() - y.mean())
        / pooled_std
    )

d = cohens_d(
    group_a,
    group_b
)

print("Cohen's d:", d)
```

---

# 35. Statistical vs Practical Significance

ধরো:

```text
p = 0.001
```

কিন্তু:

```text
mean difference = 0.02
```

তাহলে statistically significant হলেও practical impact খুব ছোট হতে পারে।

আবার:

```text
mean difference = 20
effect size = large
p = 0.08
```

এখানে sample size ছোট হলে strong practical difference থাকলেও evidence insufficient হতে পারে।

তাই report:

```text
Difference
+
Confidence Interval
+
p-value
+
Effect Size
```

---

# 36. Multiple Testing Problem

ধরো তুমি 100টা hypothesis test করেছ।

প্রতিটি test-এর:

```text
α = 0.05
```

তাহলে chance-এর কারণে কিছু false positive পাওয়া স্বাভাবিক।

এটাকে multiple comparisons problem বলে।

---

# 37. Bonferroni Correction

Simple correction:

```text
Adjusted alpha =
0.05 / number of tests
```

Python:

```python id="1qj7jv"
from statsmodels.stats.multitest import multipletests

p_values = [
    0.01,
    0.03,
    0.20,
    0.001
]

adjusted = multipletests(
    p_values,
    method="bonferroni"
)

print(adjusted)
```

আরও powerful approaches যেমন FDR correction-ও আছে।

---

# 38. A/B Testing

Hypothesis testing-এর practical application হলো **A/B testing**।

ধরো একটি website-এর দুই version:

```text
A = Old button
B = New button
```

Metrics:

```text
Conversion rate
```

Question:

> B কি সত্যিই A-এর চেয়ে better?

---

# 39. A/B Testing Structure

```text
Users
  │
  ├── Group A
  │     ↓
  │   Conversion
  │
  └── Group B
        ↓
      Conversion

        ↓
Statistical Test
        ↓
Decision
```

---

# 40. A/B Hypothesis

```text
H₀:
A এবং B-এর conversion rate একই।

H₁:
A এবং B-এর conversion rate আলাদা।
```

যদি directional question হয়:

```text
H₁:
B-এর conversion rate A-এর চেয়ে বেশি।
```

---

# 41. Conversion Example

ধরো:

```text
A:
1000 users
100 conversions
= 10%

B:
1000 users
130 conversions
= 13%
```

Difference:

```text
3 percentage points
```

কিন্তু প্রশ্ন:

> এই 3% statistically convincing?

---

# 42. Proportion Test

Conversion rate categorical outcome হওয়ায় proportion-based test ব্যবহার করা যায়।

```python id="2o4v0v"
from statsmodels.stats.proportion import proportions_ztest

success = [
    100,
    130
]

total = [
    1000,
    1000
]

stat, p = proportions_ztest(
    success,
    total
)

print("z-statistic:", stat)
print("p-value:", p)
```

---

# 43. A/B Test Interpretation

যদি:

```text
p < 0.05
```

তাহলে:

> Evidence suggests A এবং B-এর conversion rate statistically different।

তারপর দেখতে হবে:

```text
B conversion
-
A conversion
```

এবং effect size / confidence interval।

শুধু p-value দেখে "B is better" বলা উচিত নয়।

---

# 44. Seaborn দিয়ে A/B Visualization

```python id="6e6g3p"
sns.barplot(
    data=ab_df,
    x="group",
    y="conversion"
)

plt.ylabel("Conversion Rate")
plt.title("A/B Test")
plt.show()
```

আর raw outcomes থাকলে countplot:

```python id="y5y4kq"
sns.countplot(
    data=ab_df,
    x="group",
    hue="converted"
)

plt.show()
```

---

# 45. Confidence Interval Visualization

A/B test report ideally:

```text
A = 10.0%
B = 13.0%

Difference = +3.0 percentage points

95% CI = [something, something]
p-value = ...
```

এতে decision অনেক বেশি informative হয়।

---

# 46. M20-তে Statistical Test Selection Cheat Sheet

| Question                                 | Test               |
| ---------------------------------------- | ------------------ |
| One sample mean vs fixed value           | One-sample t-test  |
| Two independent means                    | Independent t-test |
| Same subjects before/after               | Paired t-test      |
| Two independent non-parametric groups    | Mann-Whitney U     |
| 3+ group means                           | ANOVA              |
| Which ANOVA groups differ?               | Tukey HSD          |
| Two categorical variables                | Chi-square         |
| Small 2×2 categorical counts             | Fisher's exact     |
| Two conversion rates                     | Proportion test    |
| Relationship between numerical variables | Pearson/Spearman   |
| Effect size for 2 means                  | Cohen's d          |

---

# 47. Hypothesis Testing Workflow

Professional workflow:

```text
1. Define business/ML question
        ↓
2. Identify variables
        ↓
3. Visualize
        ↓
4. Define H₀ and H₁
        ↓
5. Choose appropriate test
        ↓
6. Check assumptions
        ↓
7. Run test
        ↓
8. Calculate p-value
        ↓
9. Calculate confidence interval
        ↓
10. Calculate effect size
        ↓
11. Interpret
        ↓
12. Make practical decision
```

---

# 48. AI CCTV-তে M20-এর ব্যবহার

এখানেই তোমার project-এর সাথে M20 খুব useful।

ধরো:

```text
target
0 = Normal
1 = Suspicious
```

এবং feature:

```text
motion_score
velocity
person_count
brightness
duration
```

তোমার প্রশ্ন হতে পারে:

> Suspicious এবং Normal videos-এর motion score কি statistically different?

---

## Step 1 — Visualization

```python id="ecqg7v"
sns.boxplot(
    data=df,
    x="target",
    y="motion_score"
)

plt.show()
```

---

## Step 2 — Group Statistics

```python id="qg0npx"
print(
    df.groupby("target")["motion_score"]
      .agg(["count", "mean", "median", "std"])
)
```

---

## Step 3 — t-test

```python id="g6m5i1"
normal = df[
    df["target"] == 0
]["motion_score"].dropna()

suspicious = df[
    df["target"] == 1
]["motion_score"].dropna()

stat, p = ttest_ind(
    normal,
    suspicious,
    equal_var=False
)

print("p-value:", p)
```

---

## Step 4 — Effect Size

```python id="q0m2t8"
d = cohens_d(
    normal,
    suspicious
)

print("Cohen's d:", d)
```

এখন তোমার conclusion হবে অনেক stronger:

```text
Normal mean = ...
Suspicious mean = ...

p-value = ...
Cohen's d = ...

Conclusion:
...
```

---

# 49. কিন্তু CCTV-তে একটা বড় সতর্কতা

যদি একই video থেকে অনেক overlapping clips থাকে:

```text
Video A
 ├── Clip 1
 ├── Clip 2
 ├── Clip 3
 ├── Clip 4
```

তাহলে প্রতিটি clip-কে independent observation ধরে statistical test করলে সমস্যা হতে পারে।

কারণ:

```text
Clip 1
Clip 2
Clip 3
```

এগুলো পরস্পরের সাথে highly dependent হতে পারে।

এক্ষেত্রে **source video-level analysis** অনেক বেশি defensible হতে পারে।

এটি তোমার CCTV dataset-এর জন্য বিশেষভাবে গুরুত্বপূর্ণ।

---

# 50. M20 Complete Practical Example

```python id="8o6y2g"
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

from scipy.stats import ttest_ind

# Load data
df = pd.read_csv("cctv_features.csv")

# -------------------------
# 1. Group statistics
# -------------------------

summary = (
    df.groupby("target")["motion_score"]
      .agg(["count", "mean", "median", "std"])
)

print(summary)


# -------------------------
# 2. Visualization
# -------------------------

sns.boxplot(
    data=df,
    x="target",
    y="motion_score"
)

plt.title(
    "Motion Score by Target Class"
)

plt.show()


# -------------------------
# 3. Separate groups
# -------------------------

normal = df[
    df["target"] == 0
]["motion_score"].dropna()

suspicious = df[
    df["target"] == 1
]["motion_score"].dropna()


# -------------------------
# 4. Welch's t-test
# -------------------------

stat, p = ttest_ind(
    normal,
    suspicious,
    equal_var=False
)

print("t-statistic:", stat)
print("p-value:", p)


# -------------------------
# 5. Decision
# -------------------------

alpha = 0.05

if p < alpha:
    print(
        "Statistically significant difference."
    )
else:
    print(
        "No statistically significant evidence "
        "of a difference."
    )
```

---

# 51. M19 + M20 Connection

এখন তোমার EDA অনেক powerful হয়ে গেল।

```text
M17
Feature Engineering
       ↓
M18
Data Quality
       ↓
M19
Feature Selection
       ↓
M20
Statistical Validation
       ↓
ML Model
```

অর্থাৎ:

```text
Feature তৈরি করলাম
       ↓
Feature clean কিনা দেখলাম
       ↓
Feature useful কিনা দেখলাম
       ↓
Statistically meaningful relationship আছে কিনা দেখলাম
       ↓
Model-এ ব্যবহার করলাম
```

---

# 52. M20-তে যে ভুলগুলো করবে না

### ❌ ভুল 1

```text
p < 0.05
↓
Feature অবশ্যই important
```

না।

Statistical significance ≠ predictive importance।

---

### ❌ ভুল 2

```text
p > 0.05
↓
H₀ proven true
```

না।

শুধু:

> Evidence insufficient to reject H₀.

---

### ❌ ভুল 3

অনেক test চালিয়ে correction না করা।

```text
100 tests
↓
some false positives
```

---

### ❌ ভুল 4

Visualization না করে test চালানো।

---

### ❌ ভুল 5

Causation দাবি করা।

```text
Correlation / Association
≠
Causation
```

---

### ❌ ভুল 6

Overlapping CCTV clips-কে fully independent observation ধরে নেওয়া।

---

# 53. M20 Practice Project

একটি dataset নিয়ে নিচের analysis করো।

### Part A — Two Groups

```text
Normal vs Suspicious
```

একটি numerical feature নির্বাচন করো:

```text
motion_score
```

করো:

* mean
* median
* standard deviation
* boxplot
* histogram
* Welch's t-test
* Mann-Whitney U
* Cohen's d
* confidence interval

---

### Part B — Categorical

```text
target
camera_type
```

এর মধ্যে relationship:

* crosstab
* percentage
* stacked/count plot
* Chi-square test

---

### Part C — Multiple Groups

ধরো:

```text
camera_type
```

এর 3+ category আছে।

একটি numerical feature-এর mean compare করো:

```text
ANOVA
↓
Tukey HSD
```

---

### Part D — A/B Test

Simulate করো:

```text
A = old model
B = new model
```

তারপর:

```text
accuracy
precision
recall
```

এর মধ্যে একটি metric নিয়ে comparison করার statistical framework তৈরি করো।

**তবে model metrics-এর statistical comparison-এর জন্য simple t-test সবসময় যথাযথ নয়; repeated folds, paired observations বা appropriate resampling/permutation methods অনেক ক্ষেত্রে বেশি উপযুক্ত।**

---

# 54. M20 Final Cheat Sheet

```text
H₀
↓
No difference / no association

H₁
↓
Difference / association exists

α
↓
Significance threshold

p-value
↓
Evidence against H₀

Confidence Interval
↓
Plausible range of effect

Effect Size
↓
How large is the effect?

t-test
↓
Compare 1/2 means

Mann-Whitney
↓
Two independent groups, non-parametric alternative

Chi-square
↓
Categorical vs categorical

ANOVA
↓
3+ group means

Tukey
↓
Which groups differ?

A/B Test
↓
Compare two alternatives
```

## M01 → M20 এখন তোমার progression

```text
M01–M13 → Seaborn Visualization
M14–M15 → End-to-End EDA
M16     → Statistical EDA
M17     → Feature Engineering
M18     → Data Quality & Missing Values
M19     → Feature Selection & PCA
M20     → Hypothesis Testing & A/B Analysis
```

**M20-এর মূল লক্ষ্য:**

> Data-তে একটা difference/relationship দেখা গেলেই সেটা সত্যি ধরে না নিয়ে, **statistical evidence + uncertainty + effect size + domain context** দিয়ে conclusion নেওয়া।

পরের logical milestone হবে **M21 — Advanced Numerical Relationship Analysis: Covariance, Pearson vs Spearman, Partial Correlation, Confounding, Causation, Simpson’s Paradox এবং Statistical Relationship Visualization**।
