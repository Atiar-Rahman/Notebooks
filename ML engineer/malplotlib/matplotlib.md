অবশ্যই। আমি তোমাকে **Matplotlib Mastery Course (Beginner → Advanced → Production Data Visualization)** করাবো। যেহেতু তুমি Data Engineer / ML Engineer track follow করছো, তাই শুধু basic plotting না, **data analysis, ML visualization, dashboard-level charting** পর্যন্ত নিয়ে যাবো।

## Matplotlib Mastery Course Roadmap

### Phase 1: Foundation (Lesson 1-5)

1. Matplotlib Introduction + Installation
2. Figure এবং Axes ধারণা
3. Basic Plot (Line, Scatter, Bar)
4. Labels, Titles, Legends
5. Styling এবং Customization

### Phase 2: Data Visualization Core (Lesson 6-12)

6. Multiple plots এবং Subplots
7. Histogram এবং Distribution Analysis
8. Box Plot এবং Statistical Visualization
9. Pie Chart, Area Chart
10. Working with NumPy Arrays
11. Working with Pandas DataFrame
12. Real Dataset Visualization

### Phase 3: Advanced Matplotlib (Lesson 13-20)

13. Object-Oriented API Mastery
14. Figure Size, DPI, Resolution
15. Colors, Colormaps, Themes
16. Annotations এবং Text Control
17. Custom Ticks এবং Axis Formatting
18. Dates এবং Time Series Plot
19. Saving Publication Quality Figures
20. Matplotlib Performance Optimization

### Phase 4: ML/Data Science Visualization (Lesson 21-30)

21. ML Dataset Exploration (EDA)
22. Correlation Heatmap
23. Feature Distribution Analysis
24. Model Training Visualization
25. Loss Curve Visualization
26. Accuracy Curve Visualization
27. Confusion Matrix Visualization
28. ROC Curve এবং AUC
29. Deep Learning Metrics Visualization
30. Production Visualization Project

---

## Final Projects

### Project 1:

**Sales Data Analysis Dashboard**

* CSV data
* Pandas + Matplotlib
* Revenue trends
* Customer analysis

### Project 2:

**Machine Learning Model Visualization**

* Training loss
* Validation accuracy
* Confusion matrix
* Prediction analysis

### Project 3:

**AI CCTV Dataset Visualization (তোমার UCF Crime project অনুযায়ী)**

* Frame visualization
* Class distribution
* Clip length analysis
* Model performance plots

---

# Lesson 1 শুরু করি

# Lesson 1: Matplotlib Introduction + First Plot

## Matplotlib কী?

Matplotlib হলো Python এর সবচেয়ে জনপ্রিয় visualization library।

এটা ব্যবহার করে আমরা তৈরি করতে পারি:

* Line chart
* Bar chart
* Scatter plot
* Histogram
* Heatmap
* Statistical graphs
* ML/DL training graphs

Install:

```bash
pip install matplotlib
```

Import:

```python
import matplotlib.pyplot as plt
```

`pyplot` হলো Matplotlib এর main interface.

---

# First Line Plot

ধরি:

```python
x = [1,2,3,4,5]

y = [10,20,15,30,25]
```

Plot:

```python
import matplotlib.pyplot as plt


x = [1,2,3,4,5]

y = [10,20,15,30,25]


plt.plot(x,y)

plt.show()
```

Output:

একটা line graph দেখাবে।

---

# Understanding Flow

```
Data
 |
 |
plt.plot()
 |
 |
Figure তৈরি
 |
 |
plt.show()
 |
 |
Screen এ display
```

---

# Add Title

```python
plt.plot(x,y)

plt.title("Sales Report")

plt.show()
```

---

# X এবং Y Label

```python
plt.plot(x,y)


plt.xlabel("Month")

plt.ylabel("Sales")


plt.title("Monthly Sales")


plt.show()
```

---

# Add Marker

```python
plt.plot(
    x,
    y,
    marker="o"
)


plt.show()
```

এখানে:

```
o = circle marker
s = square
^ = triangle
* = star
```

Example:

```python
plt.plot(
    x,
    y,
    marker="*",
    linestyle="--"
)

plt.show()
```

---

# Line Style

```python
plt.plot(
    x,
    y,
    linestyle="--"
)
```

Available:

```
-   solid

--  dashed

-.  dash dot

:   dotted
```

---

# Line Width

```python
plt.plot(
    x,
    y,
    linewidth=3
)
```

---

# Complete Example

```python
import matplotlib.pyplot as plt


months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May"
]


sales = [
    100,
    150,
    120,
    200,
    180
]


plt.plot(
    months,
    sales,
    marker="o",
    linewidth=3
)


plt.title(
    "Monthly Sales"
)


plt.xlabel(
    "Month"
)


plt.ylabel(
    "Revenue"
)


plt.grid()


plt.show()
```

---

# Important Concept

Matplotlib দুইভাবে ব্যবহার করা যায়:

## 1. Pyplot Style

Beginner friendly:

```python
plt.plot()
plt.show()
```

## 2. Object Oriented Style

Professional way:

```python
fig, ax = plt.subplots()

ax.plot(x,y)

plt.show()
```

Industry এবং ML project এ দ্বিতীয়টা বেশি ব্যবহার হয়।

---

# Practice Task (Lesson 1)

এই তিনটা plot বানাও:

### Task 1

Temperature:

```
Days = [1,2,3,4,5,6,7]

Temp = [30,32,31,35,36,34,33]
```

Requirements:

* Title
* X label
* Y label
* Marker
* Grid

### Task 2

একটা Student Result graph:

```
Subjects:
Python
Django
ML
Database

Marks:
80
90
75
85
```

### Task 3

একটা stock price graph বানাও।

---

পরের Lesson:

**Lesson 2: Figure, Axes এবং Matplotlib Object-Oriented Programming (Professional Way)**

এটা শিখলে তুমি ML project-এর visualization professionally করতে পারবে।


---------

# Matplotlib Mastery Course

# Lesson 2: Figure এবং Axes (Professional Matplotlib Architecture)

গত lesson-এ আমরা `plt.plot()` দিয়ে basic plotting শিখেছি। কিন্তু production-level data science, ML, research project-এ সাধারণত **Object-Oriented API** ব্যবহার করা হয়।

আজকের lesson-এর সবচেয়ে গুরুত্বপূর্ণ বিষয়:

* Figure কী?
* Axes কী?
* Figure এবং Axes এর সম্পর্ক
* `plt.subplots()` ব্যবহার
* Professional plotting structure

---

# 1. Matplotlib Architecture

Matplotlib এর structure:

```
Figure
 |
 |
 +----------------+
 |                |
Axes             Axes
 |                |
Plot             Plot
```

সহজ ভাষায়:

### Figure

পুরো canvas বা window।

### Axes

যেখানে actual graph আঁকা হয়।

একটা Figure-এর ভিতরে এক বা একাধিক Axes থাকতে পারে।

---

# 2. Traditional Way vs Professional Way

## Traditional Pyplot Style

```python
import matplotlib.pyplot as plt


x = [1,2,3,4]
y = [10,20,15,30]


plt.plot(x,y)

plt.show()
```

এটা ছোট কাজের জন্য ভালো।

---

# 3. Object-Oriented Style

Professional approach:

```python
import matplotlib.pyplot as plt


x = [1,2,3,4]
y = [10,20,15,30]


fig, ax = plt.subplots()


ax.plot(x,y)


plt.show()
```

এখানে:

```python
fig
```

= Figure object

```python
ax
```

= Axes object

---

# 4. Figure Object

Example:

```python
fig, ax = plt.subplots()


print(type(fig))

print(type(ax))
```

Output:

```
<class 'matplotlib.figure.Figure'>

<class 'matplotlib.axes._axes.Axes'>
```

---

# 5. Figure Size Control

Default:

```python
fig, ax = plt.subplots()
```

Custom size:

```python
fig, ax = plt.subplots(
    figsize=(10,5)
)


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.show()
```

`figsize`

format:

```
(width, height)
```

unit:

```
inch
```

---

# 6. DPI Control

DPI = dots per inch

Higher DPI → better quality

```python
fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=150
)


ax.plot(
    [1,2,3],
    [4,5,6]
)


plt.show()
```

---

# 7. Axes Object দিয়ে Control

## Title

```python
fig, ax = plt.subplots()


ax.plot(
    [1,2,3],
    [10,20,30]
)


ax.set_title(
    "Sales Graph"
)


plt.show()
```

---

## X Label

```python
ax.set_xlabel(
    "Month"
)
```

---

## Y Label

```python
ax.set_ylabel(
    "Revenue"
)
```

---

# Complete Professional Example

```python
import matplotlib.pyplot as plt


months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr"
]


sales = [
    100,
    150,
    120,
    200
]


fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=120
)


ax.plot(
    months,
    sales,
    marker="o"
)


ax.set_title(
    "Monthly Sales"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Sales"
)


ax.grid()


plt.show()
```

এটাই production style।

---

# 8. Multiple Axes in One Figure

একটা Figure এর ভিতরে multiple graph:

```python
fig, axes = plt.subplots(
    nrows=2,
    ncols=1
)


axes[0].plot(
    [1,2,3],
    [10,20,30]
)


axes[1].plot(
    [1,2,3],
    [30,20,10]
)


plt.show()
```

Result:

```
Figure

+-------------+
|  Graph 1   |
+-------------+

+-------------+
|  Graph 2   |
+-------------+
```

---

# 9. Rows এবং Columns

2×2 grid:

```python
fig, axes = plt.subplots(
    nrows=2,
    ncols=2
)
```

Structure:

```
axes[0,0]   axes[0,1]


axes[1,0]   axes[1,1]

```

Example:

```python
fig, axes = plt.subplots(
    2,
    2,
    figsize=(10,8)
)


axes[0,0].plot([1,2,3])


axes[0,1].plot([3,2,1])


axes[1,0].bar(
    ["A","B"],
    [10,20]
)


axes[1,1].scatter(
    [1,2,3],
    [5,10,15]
)


plt.show()
```

---

# 10. Why Object-Oriented API Important?

কারণ ML project এ:

Example:

Training visualization:

```
Figure

Loss Curve
Accuracy Curve
Validation Curve
Confusion Matrix

```

একসাথে manage করতে হয়।

যেমন:

```python
fig, axes = plt.subplots(
    2,2
)

axes[0,0]
loss graph


axes[0,1]
accuracy graph


axes[1,0]
confusion matrix


axes[1,1]
ROC curve
```

এভাবে professional ML paper এবং dashboard তৈরি করা হয়।

---

# Lesson 2 Practice Task

## Task 1

একটা Figure তৈরি করো:

Size:

```
figsize=(10,6)
dpi=150
```

তার ভিতরে:

* Line chart
* Title
* X label
* Y label
* Grid

---

## Task 2

একটা 2×2 dashboard বানাও:

Top-left:

```
Line chart
```

Top-right:

```
Bar chart
```

Bottom-left:

```
Scatter plot
```

Bottom-right:

```
Histogram
```

---

## Task 3 (ML Related)

একটা fake training history তৈরি করো:

```python
epochs = [1,2,3,4,5]

loss = [0.9,0.7,0.5,0.3,0.2]

accuracy = [50,60,75,85,90]
```

এক Figure এ:

* Loss curve
* Accuracy curve

দেখাও।

---

পরের Lesson:

# Lesson 3: Line Plot Mastery

* multiple lines
* legend
* colors
* markers
* styles
* real dataset visualization
* ML training curve তৈরি করা

এটা শেষ করলে Matplotlib-এর সবচেয়ে বেশি ব্যবহৃত অংশ আয়ত্ত হয়ে যাবে।
# Matplotlib Mastery Course

# Lesson 3: Line Plot Mastery (Professional Level)

আজ আমরা Matplotlib-এর সবচেয়ে বেশি ব্যবহৃত chart **Line Plot** গভীরভাবে শিখবো।

Line plot ব্যবহার হয়:

* Time series data
* Stock price
* Sensor data
* ML training curve
* Loss / Accuracy visualization
* Business analytics

---

# 1. Basic Line Plot

আগে আমরা দেখেছি:

```python
import matplotlib.pyplot as plt


x = [1,2,3,4,5]

y = [10,20,15,30,25]


fig, ax = plt.subplots()


ax.plot(
    x,
    y
)


plt.show()
```

এখানে:

```
x → horizontal axis
y → vertical axis
```

---

# 2. Multiple Lines Plot

একই graph-এ একাধিক line দেখানো যায়।

Example:

ধরি দুইটা company-এর sales:

```python
import matplotlib.pyplot as plt


month = [
    1,2,3,4,5
]


company_a = [
    100,
    150,
    130,
    180,
    200
]


company_b = [
    80,
    120,
    160,
    140,
    220
]


fig, ax = plt.subplots()


ax.plot(
    month,
    company_a
)


ax.plot(
    month,
    company_b
)


plt.show()
```

Output:

```
Graph

Company A ----

Company B ----
```

---

# 3. Adding Labels with Legend

Multiple line থাকলে বুঝতে হবে কোনটা কোন data।

এর জন্য:

```python
fig, ax = plt.subplots()


ax.plot(
    month,
    company_a,
    label="Company A"
)


ax.plot(
    month,
    company_b,
    label="Company B"
)


ax.legend()


plt.show()
```

`legend()` automatically label show করে।

---

# 4. Line Color Control

```python
ax.plot(
    x,
    y,
    color="red"
)
```

কিছু common color:

```python
"red"

"blue"

"green"

"black"

"orange"
```

Example:

```python
ax.plot(
    x,
    y,
    color="green"
)
```

---

# 5. Line Style

Syntax:

```python
linestyle
```

Example:

```python
ax.plot(
    x,
    y,
    linestyle="--"
)
```

Options:

```
-   solid

--  dashed

-.  dash-dot

:   dotted
```

Example:

```python
ax.plot(
    x,
    y,
    linestyle=":"
)
```

---

# 6. Marker Customization

Marker data point highlight করে।

```python
ax.plot(
    x,
    y,
    marker="o"
)
```

Common markers:

```
o  circle

s  square

^  triangle

*  star

+  plus

x  cross
```

Example:

```python
ax.plot(
    x,
    y,
    marker="*"
)
```

---

# 7. Line Width

```python
ax.plot(
    x,
    y,
    linewidth=3
)
```

Default:

```
linewidth=1
```

Thicker line:

```python
linewidth=5
```

---

# 8. Marker Size

```python
ax.plot(
    x,
    y,
    marker="o",
    markersize=10
)
```

---

# 9. Complete Professional Example

```python
import matplotlib.pyplot as plt


months = [
    "Jan",
    "Feb",
    "Mar",
    "Apr",
    "May"
]


sales_2025 = [
    100,
    150,
    130,
    180,
    220
]


sales_2026 = [
    120,
    170,
    160,
    210,
    250
]


fig, ax = plt.subplots(
    figsize=(10,5),
    dpi=120
)


ax.plot(
    months,
    sales_2025,
    label="2025 Sales",
    marker="o",
    linestyle="--",
    linewidth=2
)


ax.plot(
    months,
    sales_2026,
    label="2026 Sales",
    marker="s",
    linewidth=3
)


ax.set_title(
    "Yearly Sales Comparison"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Revenue"
)


ax.legend()


ax.grid()


plt.show()
```

---

# 10. Axis Limit Control

কখনো graph-এর range control করতে হয়।

## X Axis

```python
ax.set_xlim(
    1,
    10
)
```

## Y Axis

```python
ax.set_ylim(
    0,
    300
)
```

Example:

```python
ax.set_ylim(
    0,
    500
)
```

---

# 11. Grid Customization

Basic:

```python
ax.grid()
```

Customize:

```python
ax.grid(
    linestyle="--",
    alpha=0.5
)
```

---

# 12. Real ML Example: Training Loss Curve

Deep Learning training:

```python
epochs = [
    1,2,3,4,5,6
]


train_loss = [
    0.9,
    0.7,
    0.5,
    0.35,
    0.2,
    0.1
]


val_loss = [
    1.0,
    0.8,
    0.6,
    0.5,
    0.45,
    0.4
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.plot(
    epochs,
    train_loss,
    label="Training Loss",
    marker="o"
)


ax.plot(
    epochs,
    val_loss,
    label="Validation Loss",
    marker="s"
)


ax.set_title(
    "Model Loss Curve"
)


ax.set_xlabel(
    "Epoch"
)


ax.set_ylabel(
    "Loss"
)


ax.legend()


ax.grid()


plt.show()
```

এই ধরনের graph CNN, LSTM, Transformer training analysis-এ ব্যবহার হয়।

---

# 13. Saving Line Plot

Graph save:

```python
plt.savefig(
    "loss_curve.png"
)
```

High quality:

```python
plt.savefig(
    "loss_curve.png",
    dpi=300,
    bbox_inches="tight"
)
```

---

# Lesson 3 Practice

## Task 1

একটা temperature monitoring graph বানাও:

```python
days = [1,2,3,4,5,6,7]

temperature = [30,31,29,32,35,34,33]
```

Requirements:

* Marker
* Line style
* Title
* Labels
* Grid

---

## Task 2

একই graph-এ:

```
Train Accuracy
Validation Accuracy
```

plot করো।

Data:

```python
epochs=[1,2,3,4,5]

train=[60,70,80,88,95]

val=[55,68,75,80,82]
```

---

## Task 3 (Real World)

একটা stock price visualization তৈরি করো:

```
Day:
1 2 3 4 5

Price:
100 105 103 110 115
```

---

পরের Lesson:

# Lesson 4: Bar Chart Mastery

* Vertical bar
* Horizontal bar
* Grouped bar
* Stacked bar
* Data comparison
* Business analytics visualization

এটা Data Engineer এবং Data Analyst কাজের জন্য খুব গুরুত্বপূর্ণ।
# Matplotlib Mastery Course

# Lesson 4: Bar Chart Mastery (Professional Level)

আজ আমরা শিখবো **Bar Chart**।

Bar chart ব্যবহার হয় যখন আমাদের **different categories এর মধ্যে comparison** করতে হয়।

ব্যবহার:

* Sales comparison
* Product analysis
* Feature importance
* Class distribution
* Survey result
* ML dataset analysis

---

# 1. Basic Bar Chart

Matplotlib এ bar chart:

```python
ax.bar()
```

Example:

```python
import matplotlib.pyplot as plt


products = [
    "Laptop",
    "Mobile",
    "Tablet",
    "Watch"
]


sales = [
    100,
    250,
    150,
    80
]


fig, ax = plt.subplots()


ax.bar(
    products,
    sales
)


plt.show()
```

Output:

```
Sales

|
|       █
|   █   █
|   █ █ █
| █ █ █ █
--------------
Laptop Mobile...
```

---

# 2. Add Title and Labels

```python
fig, ax = plt.subplots()


ax.bar(
    products,
    sales
)


ax.set_title(
    "Product Sales"
)


ax.set_xlabel(
    "Products"
)


ax.set_ylabel(
    "Sales"
)


plt.show()
```

---

# 3. Bar Color

Single color:

```python
ax.bar(
    products,
    sales,
    color="green"
)
```

Example:

```python
ax.bar(
    products,
    sales,
    color="orange"
)
```

---

# 4. Bar Width

Default:

```python
width=0.8
```

Change:

```python
ax.bar(
    products,
    sales,
    width=0.5
)
```

---

# 5. Horizontal Bar Chart

Vertical:

```python
ax.bar()
```

Horizontal:

```python
ax.barh()
```

Example:

```python
fig, ax = plt.subplots()


ax.barh(
    products,
    sales
)


plt.show()
```

Output:

```
Laptop ███████

Mobile █████████████

Tablet ████████
```

---

# 6. Add Value Labels on Bars

Real dashboard এ value দেখানো হয়।

Example:

```python
fig, ax = plt.subplots()


bars = ax.bar(
    products,
    sales
)


for bar in bars:

    height = bar.get_height()

    ax.text(
        bar.get_x()+bar.get_width()/2,
        height,
        str(height),
        ha="center",
        va="bottom"
    )


plt.show()
```

Output:

```
       250
       █
100    █
█      █
-------------
Laptop Mobile
```

---

# 7. Multiple Bar Chart (Grouped Bar)

Example:

2025 এবং 2026 sales comparison

Data:

```python
products = [
    "Laptop",
    "Mobile",
    "Tablet"
]


sales_2025 = [
    100,
    200,
    150
]


sales_2026 = [
    150,
    250,
    180
]
```

Implementation:

```python
import numpy as np


x = np.arange(
    len(products)
)


width = 0.35


fig, ax = plt.subplots()


ax.bar(
    x-width/2,
    sales_2025,
    width,
    label="2025"
)


ax.bar(
    x+width/2,
    sales_2026,
    width,
    label="2026"
)


ax.set_xticks(
    x
)


ax.set_xticklabels(
    products
)


ax.legend()


plt.show()
```

Result:

```
Laptop

2025 ███
2026 █████
```

---

# 8. Stacked Bar Chart

একটার উপর আরেকটা bar:

Example:

Company expense:

```python
salary = [
    50,
    60,
    70
]


marketing = [
    20,
    30,
    25
]
```

Code:

```python
fig, ax = plt.subplots()


ax.bar(
    products,
    salary,
    label="Salary"
)


ax.bar(
    products,
    marketing,
    bottom=salary,
    label="Marketing"
)


ax.legend()


plt.show()
```

Result:

```
|
|   █ marketing
|   █
|   █ salary
|   █
--------------
```

---

# 9. Bar Chart with Pandas DataFrame

Real data সাধারণত pandas থেকে আসে।

Example:

```python
import pandas as pd


df = pd.DataFrame({

"City":[
"Dhaka",
"Chittagong",
"Rajshahi"
],

"Sales":[
500,
300,
200
]

})


df
```

Plot:

```python
df.plot(
    kind="bar",
    x="City",
    y="Sales"
)


plt.show()
```

---

# 10. ML Dataset Class Distribution

তোমার UCF Crime project এর মতো:

ধরি:

```python
classes = [
    "Normal",
    "Suspicious"
]


count = [
    30000,
    10000
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.bar(
    classes,
    count
)


ax.set_title(
    "Dataset Class Distribution"
)


ax.set_ylabel(
    "Number of Samples"
)


plt.show()
```

এটা ML paper এবং EDA তে ব্যবহার হয়।

---

# 11. Feature Importance Visualization

Machine Learning model:

```python
features = [
    "Age",
    "Income",
    "Experience",
    "Score"
]


importance = [
    0.3,
    0.5,
    0.2,
    0.7
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.barh(
    features,
    importance
)


ax.set_title(
    "Feature Importance"
)


plt.show()
```

---

# 12. Professional Example

```python
import matplotlib.pyplot as plt


departments = [
    "AI",
    "Backend",
    "Frontend",
    "Data"
]


employees = [
    25,
    40,
    30,
    20
]


fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=120
)


bars = ax.bar(
    departments,
    employees
)


ax.set_title(
    "Team Distribution"
)


ax.set_xlabel(
    "Department"
)


ax.set_ylabel(
    "Employees"
)


ax.grid(
    axis="y"
)


plt.show()
```

---

# Lesson 4 Practice Task

## Task 1

একটা Company Revenue chart বানাও:

```python
years = [
2021,
2022,
2023,
2024
]


revenue = [
100,
150,
220,
300
]
```

Requirements:

* Bar chart
* Title
* Labels
* Grid
* Value display

---

## Task 2

Grouped bar chart:

Compare:

```
Python
Django
ML
Database
```

Student A:

```
80
90
75
85
```

Student B:

```
70
85
90
80
```

---

## Task 3 (ML)

Dataset distribution:

```
Normal       5000
Abnormal     1200
```

একটা professional class distribution chart তৈরি করো।

---

পরের Lesson:

# Lesson 5: Scatter Plot Mastery

* Relationship analysis
* Correlation visualization
* ML feature analysis
* Regression data visualization
* Clustering visualization

এটা Machine Learning-এর জন্য অনেক গুরুত্বপূর্ণ।

# Matplotlib Mastery Course

# Lesson 5: Scatter Plot Mastery (Professional Level)

আজ আমরা শিখবো **Scatter Plot**।

Scatter plot ব্যবহার করা হয় দুইটা variable-এর মধ্যে **relationship, pattern, correlation** বোঝার জন্য।

Data Science এবং Machine Learning-এ এটি খুব গুরুত্বপূর্ণ।

ব্যবহার:

* Feature relationship analysis
* Correlation analysis
* Regression visualization
* Clustering visualization
* Outlier detection
* Dataset exploration (EDA)

---

# 1. Scatter Plot কী?

Line plot:

```
Point ---- Point ---- Point
```

Scatter plot:

```
   *
       *
 *
          *
    *
```

প্রতিটা data point আলাদা আলাদা দেখায়।

---

# 2. Basic Scatter Plot

Syntax:

```python
ax.scatter(
    x,
    y
)
```

Example:

```python
import matplotlib.pyplot as plt


hours = [
    1,2,3,4,5,6
]


marks = [
    40,
    50,
    60,
    65,
    80,
    90
]


fig, ax = plt.subplots()


ax.scatter(
    hours,
    marks
)


plt.show()
```

এখানে:

```
x = Study Hours

y = Marks
```

আমরা দেখতে পারছি:

Study hour বাড়লে marks বাড়ছে কিনা।

---

# 3. Add Title and Labels

```python
fig, ax = plt.subplots()


ax.scatter(
    hours,
    marks
)


ax.set_title(
    "Study Hours vs Marks"
)


ax.set_xlabel(
    "Study Hours"
)


ax.set_ylabel(
    "Marks"
)


plt.show()
```

---

# 4. Marker Size

Parameter:

```python
s
```

Example:

```python
ax.scatter(
    hours,
    marks,
    s=100
)
```

বড় point:

```python
s=200
```

ছোট point:

```python
s=20
```

---

# 5. Marker Color

```python
ax.scatter(
    hours,
    marks,
    color="red"
)
```

Example:

```python
ax.scatter(
    hours,
    marks,
    color="green"
)
```

---

# 6. Transparency (Alpha)

অনেক point overlap করলে:

```python
alpha
```

Example:

```python
ax.scatter(
    hours,
    marks,
    alpha=0.5
)
```

Range:

```
0 → invisible

1 → full visible
```

---

# 7. Different Colors for Different Groups

Example:

Student groups:

```python
hours = [
1,2,3,4,5,6
]


marks = [
40,50,60,70,80,90
]


group = [
"A",
"A",
"B",
"B",
"C",
"C"
]
```

Color:

```python
colors = [
"red",
"red",
"blue",
"blue",
"green",
"green"
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.scatter(
    hours,
    marks,
    c=colors
)


plt.show()
```

---

# 8. Scatter Plot with Colormap

Machine learning data-তে useful।

Example:

```python
import numpy as np


x = np.random.rand(100)

y = np.random.rand(100)

value = np.random.rand(100)
```

Plot:

```python
fig, ax = plt.subplots()


scatter = ax.scatter(
    x,
    y,
    c=value,
    cmap="viridis"
)


plt.colorbar(
    scatter
)


plt.show()
```

এখানে:

```
c = value অনুযায়ী color change
```

---

# 9. Bubble Chart

Scatter plot-এ size variable যোগ করলে:

```python
s
```

ব্যবহার করা হয়।

Example:

```python
x = [
1,2,3,4
]


y = [
10,20,30,40
]


size = [
100,
200,
300,
500
]


fig, ax = plt.subplots()


ax.scatter(
    x,
    y,
    s=size
)


plt.show()
```

এখানে:

* X position
* Y position
* Point size

তিনটা dimension দেখা যায়।

---

# 10. Scatter Plot for Correlation

Example:

Temperature এবং Ice Cream Sales:

```python
temperature = [
20,
25,
30,
35,
40
]


sales = [
100,
150,
250,
300,
400
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.scatter(
    temperature,
    sales
)


ax.set_title(
    "Temperature vs Ice Cream Sales"
)


ax.set_xlabel(
    "Temperature"
)


ax.set_ylabel(
    "Sales"
)


plt.show()
```

যদি point upward যায়:

```
Positive Correlation
```

---

# 11. ML Example: Feature Relationship

Dataset:

```python
age = [
20,25,30,35,40
]


salary = [
20000,
30000,
45000,
60000,
80000
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.scatter(
    age,
    salary
)


ax.set_title(
    "Age vs Salary"
)


plt.show()
```

ML model train করার আগে EDA-তে এটা করা হয়।

---

# 12. Regression Line Add করা

Example:

```python
import numpy as np


x = np.array(
    [1,2,3,4,5]
)


y = np.array(
    [2,4,6,8,10]
)


```

Regression line:

```python
fig, ax = plt.subplots()


ax.scatter(
    x,
    y
)


z = np.polyfit(
    x,
    y,
    1
)


p = np.poly1d(z)


ax.plot(
    x,
    p(x)
)


plt.show()
```

Output:

```
Points + Regression Line
```

---

# 13. Outlier Detection

Example:

```python
x = [
1,2,3,4,5,20
]


y = [
10,20,30,40,50,500
]
```

Scatter:

```
*
 *
  *
   *
        *
```

শেষের point হলো outlier।

---

# 14. Real ML Example: UCF Crime Dataset

তোমার AI CCTV project-এর ক্ষেত্রে:

Feature:

```
Motion Score

Brightness
```

Visualization:

```python
motion = [
0.2,
0.4,
0.8,
0.9
]


brightness = [
100,
120,
200,
220
]


labels = [
"Normal",
"Normal",
"Suspicious",
"Suspicious"
]
```

Scatter plot দিয়ে দেখা যাবে:

Normal এবং Suspicious আলাদা cluster করছে কিনা।

---

# 15. Professional Scatter Plot Example

```python
import matplotlib.pyplot as plt


x = [
10,
20,
30,
40,
50
]


y = [
15,
35,
40,
60,
80
]


fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=120
)


ax.scatter(
    x,
    y,
    s=120,
    alpha=0.7
)


ax.set_title(
    "Feature Relationship"
)


ax.set_xlabel(
    "Feature X"
)


ax.set_ylabel(
    "Feature Y"
)


ax.grid()


plt.show()
```

---

# Lesson 5 Practice Task

## Task 1

Student Study Analysis:

```python
hours = [1,2,3,4,5,6,7]

marks = [40,45,55,65,75,85,95]
```

Requirements:

* Scatter plot
* Title
* Labels
* Marker size
* Alpha

---

## Task 2

Salary Analysis:

```python
experience = [1,2,3,4,5,6]

salary = [20000,30000,45000,60000,80000,100000]
```

Create:

* Scatter plot
* Regression line

---

## Task 3 (ML)

Fake dataset:

```python
normal_x=[1,2,3,4]

normal_y=[10,12,15,18]


attack_x=[7,8,9,10]

attack_y=[50,55,60,70]
```

Create:

* Two class scatter visualization
* Different colors
* Legend

---

পরের Lesson:

# Lesson 6: Subplots Mastery

* Multiple charts in one figure
* Dashboard design
* ML experiment visualization
* Professional reporting layout

এটা শিখলে তুমি একসাথে অনেক analysis graph তৈরি করতে পারবে।
# Matplotlib Mastery Course

# Lesson 6: Subplots Mastery (Dashboard & ML Visualization)

আজ আমরা শিখবো **Subplots**।

Subplot হলো একটি Figure-এর ভিতরে একাধিক chart তৈরি করা।

এটা খুব গুরুত্বপূর্ণ কারণ real-world project-এ একসাথে অনেক visualization দেখাতে হয়।

ব্যবহার:

* ML training report
* Data analysis dashboard
* Model comparison
* Research paper figure
* Business report

---

# 1. Subplot কী?

Normal plot:

```
Figure

+----------------+
|                |
|    Chart       |
|                |
+----------------+
```

Subplot:

```
Figure

+---------+---------+
| Chart 1 | Chart 2 |
+---------+---------+
| Chart 3 | Chart 4 |
+---------+---------+

```

---

# 2. Basic Subplot

আগে:

```python
fig, ax = plt.subplots()
```

একটা Axes তৈরি করতো।

এখন:

```python
fig, axes = plt.subplots(
    nrows=2,
    ncols=2
)
```

মানে:

```
2 rows
2 columns
```

Total:

```
2 × 2 = 4 charts
```

---

# 3. First 2×2 Dashboard

```python
import matplotlib.pyplot as plt


fig, axes = plt.subplots(
    2,
    2
)


plt.show()
```

Output:

```
+---------+---------+
| axes[0,0]|axes[0,1]|
+---------+---------+
| axes[1,0]|axes[1,1]|
+---------+---------+
```

---

# 4. Accessing Axes

2D array:

```python
axes[0,0]
```

Top-left

```python
axes[0,1]
```

Top-right

```python
axes[1,0]
```

Bottom-left

```python
axes[1,1]
```

Bottom-right

---

# 5. Add Different Charts

Example:

```python
import matplotlib.pyplot as plt


fig, axes = plt.subplots(
    2,
    2,
    figsize=(10,8)
)


# Line chart

axes[0,0].plot(
    [1,2,3],
    [10,20,30]
)


# Bar chart

axes[0,1].bar(
    ["A","B","C"],
    [20,40,30]
)


# Scatter plot

axes[1,0].scatter(
    [1,2,3],
    [5,10,15]
)


# Histogram

axes[1,1].hist(
    [10,20,20,30,40]
)


plt.show()
```

---

# 6. Add Title to Each Subplot

```python
axes[0,0].set_title(
    "Line Chart"
)


axes[0,1].set_title(
    "Bar Chart"
)
```

Complete:

```python
fig, axes = plt.subplots(
    2,
    2
)


axes[0,0].plot(
    [1,2,3],
    [10,20,30]
)

axes[0,0].set_title(
    "Sales Trend"
)


axes[0,1].bar(
    ["A","B"],
    [10,20]
)

axes[0,1].set_title(
    "Category Sales"
)


plt.show()
```

---

# 7. One Row Multiple Charts

Example:

```
+---------+---------+---------+
| Chart 1 | Chart 2 | Chart 3 |
+---------+---------+---------+

```

Code:

```python
fig, axes = plt.subplots(
    1,
    3,
    figsize=(12,4)
)


axes[0].plot(
    [1,2,3]
)


axes[1].bar(
    ["A","B"],
    [10,20]
)


axes[2].scatter(
    [1,2,3],
    [3,2,5]
)


plt.show()
```

---

# 8. Share Axis

যদি একই x-axis হয়:

```python
fig, axes = plt.subplots(
    2,
    1,
    sharex=True
)
```

Example:

```
Temperature
     |
Chart 1


Humidity
     |
Chart 2

same time axis
```

---

# 9. Spacing Control

Default spacing:

```
chart chart

chart chart
```

Improve:

```python
plt.tight_layout()
```

Example:

```python
fig, axes = plt.subplots(
    2,
    2
)


plt.tight_layout()


plt.show()
```

---

# 10. ML Training Dashboard Example

Deep Learning model training:

Data:

```python
epochs = [
1,2,3,4,5
]


loss = [
0.9,
0.6,
0.4,
0.25,
0.15
]


accuracy = [
50,
65,
75,
85,
92
]
```

Dashboard:

```python
import matplotlib.pyplot as plt


fig, axes = plt.subplots(
    1,
    2,
    figsize=(12,4)
)


# Loss

axes[0].plot(
    epochs,
    loss,
    marker="o"
)


axes[0].set_title(
    "Training Loss"
)


# Accuracy

axes[1].plot(
    epochs,
    accuracy,
    marker="o"
)


axes[1].set_title(
    "Training Accuracy"
)


plt.tight_layout()

plt.show()
```

Output:

```
+----------------+----------------+
| Training Loss  | Accuracy       |
|                |                |
+----------------+----------------+
```

---

# 11. Real ML Experiment Comparison

ধরি:

আমরা compare করছি:

* CNN
* LSTM
* CNN-LSTM

এক Figure:

```
+-------------+-------------+
| CNN Loss    | LSTM Loss   |
+-------------+-------------+
| CNN-LSTM    | Accuracy    |
+-------------+-------------+

```

Code structure:

```python
fig, axes = plt.subplots(
    2,
    2
)


axes[0,0].plot(
    cnn_loss
)


axes[0,1].plot(
    lstm_loss
)


axes[1,0].plot(
    cnn_lstm_loss
)


axes[1,1].plot(
    accuracy
)


plt.show()
```

---

# 12. Subplot Object-Oriented Best Practice

Professional template:

```python
fig, axes = plt.subplots(
    rows,
    cols,
    figsize=(width,height),
    dpi=120
)


axes[index].plot(data)


axes[index].set_title(
    "Title"
)


axes[index].set_xlabel(
    "X"
)


axes[index].set_ylabel(
    "Y"
)


plt.tight_layout()

plt.show()
```

এটা সব project-এ ব্যবহার করা যায়।

---

# Lesson 6 Practice Task

## Task 1

একটা 2×2 Data Dashboard বানাও:

Chart 1:

```
Line chart
Sales trend
```

Chart 2:

```
Bar chart
Product sales
```

Chart 3:

```
Scatter
Feature relationship
```

Chart 4:

```
Histogram
Data distribution
```

---

## Task 2 (ML)

একটা Model Training Dashboard তৈরি করো:

Top-left:

```
Training Loss
```

Top-right:

```
Validation Loss
```

Bottom-left:

```
Training Accuracy
```

Bottom-right:

```
Validation Accuracy
```

---

## Task 3 (Advanced)

UCF Crime Dataset Visualization:

এক Figure এ:

1. Normal vs Suspicious sample count (bar)
2. Frame distribution (histogram)
3. Clip length distribution (line)
4. Sample frame visualization

---

পরের Lesson:

# Lesson 7: Histogram Mastery

* Data distribution
* Bins কীভাবে কাজ করে
* Normal distribution
* Outlier detection
* ML dataset analysis

এটা EDA (Exploratory Data Analysis)-এর সবচেয়ে গুরুত্বপূর্ণ chart।

# Matplotlib Mastery Course

# Lesson 7: Histogram Mastery (Data Distribution Analysis)

আজ আমরা শিখবো **Histogram**।

Histogram হলো এমন একটি chart যা কোনো dataset-এর **distribution বা spread** দেখায়।

Data Science এবং Machine Learning-এ এটি খুব গুরুত্বপূর্ণ কারণ model train করার আগে data বুঝতে হয়।

ব্যবহার:

* Data distribution analysis
* Normal distribution check
* Outlier detection
* Feature engineering
* Dataset exploration (EDA)
* ML preprocessing

---

# 1. Histogram কী?

ধরি student marks:

```python
marks = [
45,50,55,60,65,
70,75,80,85,90
]
```

Histogram দেখাবে:

* কতগুলো value কোন range-এর মধ্যে আছে।

Example:

```
Frequency

 |
 |        █
 |     █  █
 |  █  █  █
 |  █  █  █
 ----------------
 40 50 60 70 80 90

       Marks
```

---

# 2. Basic Histogram

Syntax:

```python
ax.hist()
```

Example:

```python
import matplotlib.pyplot as plt


marks = [
45,50,55,60,65,
70,75,80,85,90
]


fig, ax = plt.subplots()


ax.hist(
    marks
)


plt.show()
```

---

# 3. Histogram Parameters

Main parameters:

```python
ax.hist(
    data,
    bins,
)
```

Example:

```python
ax.hist(
    marks,
    bins=5
)
```

---

# 4. Understanding Bins

Bins মানে হলো data ভাগ করার range।

Example:

Data:

```
0 10 20 30 40 50
```

bins=5

মানে:

```
0-10
10-20
20-30
30-40
40-50
```

---

# 5. Different Bin Values

Small bins:

```python
ax.hist(
    marks,
    bins=20
)
```

More detail:

```
|||||||||||||||||
```

---

Large bins:

```python
ax.hist(
    marks,
    bins=3
)
```

Less detail:

```
||| 
```

---

# 6. Add Labels

```python
fig, ax = plt.subplots()


ax.hist(
    marks,
    bins=5
)


ax.set_title(
    "Student Marks Distribution"
)


ax.set_xlabel(
    "Marks"
)


ax.set_ylabel(
    "Frequency"
)


plt.show()
```

---

# 7. Histogram Color

```python
ax.hist(
    marks,
    color="green"
)
```

Example:

```python
ax.hist(
    marks,
    color="orange"
)
```

---

# 8. Histogram Transparency

Alpha:

```python
ax.hist(
    marks,
    alpha=0.5
)
```

Range:

```
0 → transparent

1 → solid
```

---

# 9. Multiple Histograms

Example:

Two class marks comparison:

```python
class_a = [
60,65,70,75,80
]


class_b = [
50,55,60,65,70
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.hist(
    class_a,
    bins=5,
    alpha=0.5,
    label="Class A"
)


ax.hist(
    class_b,
    bins=5,
    alpha=0.5,
    label="Class B"
)


ax.legend()


plt.show()
```

---

# 10. Density Histogram

Normal frequency এর বদলে probability দেখাতে:

```python
ax.hist(
    marks,
    density=True
)
```

Output:

```
Probability distribution
```

---

# 11. Histogram with NumPy

Real data অনেক সময় NumPy array হয়।

Example:

```python
import numpy as np


data = np.random.randn(1000)


fig, ax = plt.subplots()


ax.hist(
    data,
    bins=30
)


plt.show()
```

এখানে আমরা random normal distribution দেখছি।

---

# 12. Normal Distribution Visualization

```python
import numpy as np


data = np.random.normal(
    loc=50,
    scale=10,
    size=1000
)


fig, ax = plt.subplots()


ax.hist(
    data,
    bins=30
)


plt.show()
```

এখানে:

```
loc = mean

scale = standard deviation
```

---

# 13. Histogram এবং Outlier Detection

Example:

```python
data = [
10,12,15,18,
20,22,25,
100
]
```

Histogram:

```
          *
          |
**** ****
------------
10       100
```

শেষের value:

```
100
```

হলো outlier।

---

# 14. ML Feature Analysis Example

ধরি:

House dataset:

```python
price = [
200000,
250000,
300000,
350000,
400000
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.hist(
    price,
    bins=5
)


ax.set_title(
    "House Price Distribution"
)


plt.show()
```

---

# 15. UCF Crime Dataset Example

তোমার AI CCTV project-এ:

ধরি:

Normal clips:

```python
normal_clips = 30000
```

Suspicious:

```python
suspicious_clips = 10000
```

Histogram দিয়ে:

* Frame count distribution
* Motion score distribution
* Prediction confidence distribution

দেখা যায়।

Example:

```python
confidence = [
0.2,
0.3,
0.5,
0.7,
0.9
]


fig, ax = plt.subplots()


ax.hist(
    confidence,
    bins=10
)


ax.set_title(
    "Model Confidence Distribution"
)


plt.show()
```

---

# 16. Histogram + Subplot Dashboard

Professional EDA:

```python
fig, axes = plt.subplots(
    1,
    2,
    figsize=(10,4)
)


axes[0].hist(
    age,
    bins=10
)


axes[0].set_title(
    "Age Distribution"
)


axes[1].hist(
    salary,
    bins=10
)


axes[1].set_title(
    "Salary Distribution"
)


plt.tight_layout()

plt.show()
```

---

# 17. Histogram vs Bar Chart

অনেকে confuse করে:

## Bar Chart

Used for:

```
Category comparison
```

Example:

```
Dhaka   500
Chittagong 300
```

---

## Histogram

Used for:

```
Continuous data distribution
```

Example:

```
Age
Height
Salary
Temperature
```

---

# Lesson 7 Practice Task

## Task 1

Student marks distribution:

```python
marks=[
45,50,55,60,
65,70,75,80,
85,90,95
]
```

Create:

* Histogram
* 5 bins
* Title
* Labels
* Grid

---

## Task 2

Generate random data:

```python
import numpy as np

data=np.random.normal(
50,
10,
1000
)
```

Create:

* Histogram
* 30 bins
* Density plot

---

## Task 3 (ML)

Fake model confidence:

```python
confidence=[
0.1,0.2,0.3,
0.5,0.6,0.7,
0.8,0.9,0.95
]
```

Create:

"Prediction Confidence Distribution"

---

পরের Lesson:

# Lesson 8: Box Plot Mastery

* Median
* Quartile
* IQR
* Outlier detection
* ML feature analysis
* Comparing multiple distributions

Box plot শিখলে dataset-এর statistical behavior অনেক ভালো বুঝতে পারবে।
# Matplotlib Mastery Course

# Lesson 8: Box Plot Mastery (Statistics + Outlier Analysis)

আজ আমরা শিখবো **Box Plot**।

Box plot হলো একটি statistical visualization যা একটি dataset-এর:

* Minimum value
* Maximum value
* Median
* Quartile
* Spread
* Outlier

দেখায়।

Data Science এবং Machine Learning-এ এটি খুব গুরুত্বপূর্ণ।

ব্যবহার:

* Outlier detection
* Feature analysis
* Dataset comparison
* Data preprocessing
* Statistical analysis

---

# 1. Box Plot কী?

একটি box plot দেখতে এমন:

```
Minimum        Maximum

 |--------------|

       |
   +-------+
   |       |
---|---|---|---
   |       |
   +-------+

       |
     Median
```

মূল অংশ:

```
Box = Middle 50% data

Line inside box = Median

Whisker = Range

Points = Outliers
```

---

# 2. Five Number Summary

Box plot পাঁচটি value ব্যবহার করে:

## 1. Minimum

সবচেয়ে ছোট value

## 2. Q1 (First Quartile)

২৫% data এর নিচের value

## 3. Median

৫০% data এর middle value

## 4. Q3 (Third Quartile)

৭৫% data এর নিচের value

## 5. Maximum

সবচেয়ে বড় value

---

# 3. IQR (Interquartile Range)

Formula:

```
IQR = Q3 - Q1
```

Outlier detection:

```
Lower Bound:

Q1 - 1.5 × IQR


Upper Bound:

Q3 + 1.5 × IQR
```

এই range-এর বাইরে value হলে:

```
Outlier
```

---

# 4. Basic Box Plot

Syntax:

```python
ax.boxplot()
```

Example:

```python
import matplotlib.pyplot as plt


marks = [
45,
50,
55,
60,
65,
70,
75,
80,
85,
90,
95
]


fig, ax = plt.subplots()


ax.boxplot(
    marks
)


plt.show()
```

---

# 5. Add Labels

```python
fig, ax = plt.subplots()


ax.boxplot(
    marks
)


ax.set_title(
    "Student Marks Distribution"
)


ax.set_ylabel(
    "Marks"
)


plt.show()
```

---

# 6. Horizontal Box Plot

Default:

```
Vertical
|
|
|
```

Horizontal:

```python
fig, ax = plt.subplots()


ax.boxplot(
    marks,
    vert=False
)


plt.show()
```

Output:

```
|----[====]------|
```

---

# 7. Detecting Outliers

Example:

```python
data = [
10,
12,
15,
18,
20,
22,
25,
100
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.boxplot(
    data
)


plt.show()
```

Output:

```
      *
      |
----[====]----
```

`100` outlier হিসেবে দেখাবে।

---

# 8. Multiple Box Plot

ধরি তিনটা class:

```python
class_a = [
60,65,70,75,80
]


class_b = [
50,55,60,65,70
]


class_c = [
70,75,80,85,90
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.boxplot(
    [
        class_a,
        class_b,
        class_c
    ]
)


plt.show()
```

Output:

```
Class A   Class B   Class C

  |         |         |
 [ ]       [ ]       [ ]
```

---

# 9. Add Tick Labels

```python
fig, ax = plt.subplots()


ax.boxplot(
    [
        class_a,
        class_b,
        class_c
    ]
)


ax.set_xticklabels(
    [
        "Class A",
        "Class B",
        "Class C"
    ]
)


plt.show()
```

---

# 10. Box Plot with Pandas

Real dataset সাধারণত DataFrame হয়।

Example:

```python
import pandas as pd


df = pd.DataFrame({

"Age":[20,25,30,35,40],

"Salary":[20000,30000,50000,70000,100000]

})


df.boxplot()


plt.show()
```

Output:

একসাথে সব numerical column visualize করবে।

---

# 11. Box Plot in EDA

ধরি dataset:

```
Age

20
22
25
30
100
```

Box plot দেখাবে:

```
Age

      *
      |
 ---[====]---
```

এখানে:

```
100
```

হতে পারে ভুল data।

---

# 12. ML Feature Analysis

Machine Learning model train করার আগে:

Features:

```
Age
Income
Experience
Score
```

Box plot:

```python
features = [
age,
income,
experience,
score
]


fig, ax = plt.subplots()


ax.boxplot(
    features
)


plt.show()
```

দেখা যাবে:

* কোন feature-এ outlier আছে
* কোন feature বেশি spread

---

# 13. UCF Crime Dataset Example

তোমার AI CCTV project:

Prediction confidence:

```python
normal_confidence = [
0.1,
0.2,
0.3,
0.4,
0.5
]


suspicious_confidence = [
0.6,
0.7,
0.8,
0.9,
0.95
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.boxplot(
    [
        normal_confidence,
        suspicious_confidence
    ]
)


ax.set_xticklabels(
    [
        "Normal",
        "Suspicious"
    ]
)


plt.show()
```

এতে দেখা যাবে model confidence দুই class-এ কেমন।

---

# 14. Styling Box Plot

Notch:

```python
ax.boxplot(
    data,
    notch=True
)
```

Show mean:

```python
ax.boxplot(
    data,
    showmeans=True
)
```

---

# 15. Box Plot vs Histogram

## Histogram

দেখায়:

```
Distribution shape
```

Example:

```
████
██████
████████
```

---

## Box Plot

দেখায়:

```
Statistical summary
```

Example:

```
----[====]----
```

---

# 16. Professional EDA Example

একটি dataset analysis:

```python
import matplotlib.pyplot as plt


age = [
20,25,30,35,40,45,50,100
]


salary = [
20000,
30000,
45000,
60000,
80000,
100000,
120000,
500000
]


fig, axes = plt.subplots(
    1,
    2,
    figsize=(10,4)
)


axes[0].boxplot(
    age
)

axes[0].set_title(
    "Age Distribution"
)


axes[1].boxplot(
    salary
)

axes[1].set_title(
    "Salary Distribution"
)


plt.tight_layout()

plt.show()
```

---

# Lesson 8 Practice Task

## Task 1

Student marks:

```python
marks=[
40,45,50,55,
60,65,70,75,
80,85,200
]
```

Create:

* Box plot
* Find outlier

---

## Task 2

Compare three departments:

```python
AI=[
70,75,80,85,90
]

Backend=[
60,65,70,75,80
]

Frontend=[
50,60,65,70,75
]
```

Create:

* Multiple box plot
* Labels

---

## Task 3 (ML)

Model confidence:

```
CNN:

0.5,0.6,0.7,0.8,0.9


CNN-LSTM:

0.7,0.8,0.85,0.9,0.95
```

Compare using box plot.

---

পরের Lesson:

# Lesson 9: Pie Chart + Area Chart Mastery

* Percentage visualization
* Composition analysis
* Stacked area
* Time-based cumulative data
* Dashboard usage

এগুলো business analytics এবং reporting-এ বেশি ব্যবহার হয়।
# Matplotlib Mastery Course

# Lesson 9: Pie Chart + Area Chart Mastery

আজ আমরা শিখবো দুই ধরনের visualization:

1. **Pie Chart**
2. **Area Chart**

দুটোই composition এবং trend analysis-এর জন্য ব্যবহার হয়।

---

# Part 1: Pie Chart Mastery

## 1. Pie Chart কী?

Pie chart একটি dataset-এর **percentage contribution** দেখায়।

Example:

একটি company's employees distribution:

```
Backend     40%
Frontend    30%
AI          20%
Data        10%
```

Pie chart:

```
        ______
     .-'      '-.
   /  Backend    \
  |     Frontend  |
  | AI      Data  |
   \            /
     '-.____.-'
```

---

# 2. Basic Pie Chart

Syntax:

```python
ax.pie()
```

Example:

```python
import matplotlib.pyplot as plt


sizes = [
    40,
    30,
    20,
    10
]


labels = [
    "Backend",
    "Frontend",
    "AI",
    "Data"
]


fig, ax = plt.subplots()


ax.pie(
    sizes,
    labels=labels
)


plt.show()
```

---

# 3. Add Percentage

`autopct` ব্যবহার করা হয় percentage দেখানোর জন্য।

```python
fig, ax = plt.subplots()


ax.pie(
    sizes,
    labels=labels,
    autopct="%1.1f%%"
)


plt.show()
```

Output:

```
Backend 40.0%

Frontend 30.0%

AI 20.0%

Data 10.0%
```

---

# 4. Explode Slice

কোনো অংশ highlight করতে:

```python
explode=[
0.1,
0,
0,
0
]
```

Example:

```python
fig, ax = plt.subplots()


ax.pie(
    sizes,
    labels=labels,
    explode=explode,
    autopct="%1.1f%%"
)


plt.show()
```

Output:

```
Backend slice বাইরে বের হয়ে থাকবে
```

---

# 5. Start Angle

Rotation control:

```python
ax.pie(
    sizes,
    labels=labels,
    startangle=90
)
```

---

# 6. Shadow

```python
ax.pie(
    sizes,
    labels=labels,
    shadow=True
)
```

---

# 7. Complete Professional Pie Chart

```python
import matplotlib.pyplot as plt


labels = [
    "Python",
    "Django",
    "ML",
    "Database"
]


usage = [
    40,
    30,
    20,
    10
]


explode=[
    0.05,
    0,
    0,
    0
]


fig, ax = plt.subplots(
    figsize=(6,6)
)


ax.pie(
    usage,
    labels=labels,
    autopct="%1.1f%%",
    explode=explode,
    shadow=True,
    startangle=90
)


ax.set_title(
    "Technology Usage"
)


plt.show()
```

---

# Pie Chart কোথায় ব্যবহার হয়?

### Business:

* Market share
* Revenue contribution
* Customer segment

### ML:

* Class distribution

Example:

UCF Crime Dataset:

```
Normal       75%

Suspicious   25%
```

Visualization:

```python
classes=[
"Normal",
"Suspicious"
]


count=[
30000,
10000
]


ax.pie(
    count,
    labels=classes,
    autopct="%1.1f%%"
)
```

---

# Part 2: Area Chart Mastery

## 8. Area Chart কী?

Area chart হলো line chart যেখানে line-এর নিচের অংশ filled থাকে।

Line:

```
      *
    *
  *
*
----------------
```

Area:

```
      *
    ****
  ******
**********
----------------
```

ব্যবহার:

* Growth trend
* Cumulative data
* Resource usage
* Time series

---

# 9. Basic Area Chart

Syntax:

```python
ax.fill_between()
```

Example:

```python
import matplotlib.pyplot as plt


months=[
1,2,3,4,5
]


sales=[
100,
150,
200,
250,
300
]


fig, ax = plt.subplots()


ax.fill_between(
    months,
    sales
)


plt.show()
```

---

# 10. Add Line with Area

Professional way:

```python
fig, ax = plt.subplots()


ax.plot(
    months,
    sales
)


ax.fill_between(
    months,
    sales,
    alpha=0.3
)


plt.show()
```

---

# 11. Area Chart Labels

```python
fig, ax = plt.subplots()


ax.fill_between(
    months,
    sales
)


ax.set_title(
    "Sales Growth"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Revenue"
)


plt.show()
```

---

# 12. Multiple Area Chart

Example:

Company growth:

```python
company_a=[
100,
150,
200,
250
]


company_b=[
80,
120,
180,
220
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.fill_between(
    months,
    company_a,
    alpha=0.5,
    label="Company A"
)


ax.fill_between(
    months,
    company_b,
    alpha=0.5,
    label="Company B"
)


ax.legend()


plt.show()
```

---

# 13. Stacked Area Chart

Multiple data combine করতে:

```python
ax.stackplot()
```

Example:

```python
import matplotlib.pyplot as plt


months=[
1,2,3,4
]


backend=[
50,
60,
70,
80
]


frontend=[
30,
40,
50,
60
]


ai=[
20,
30,
40,
50
]


fig, ax = plt.subplots()


ax.stackplot(
    months,
    backend,
    frontend,
    ai,
    labels=[
        "Backend",
        "Frontend",
        "AI"
    ]
)


ax.legend()


plt.show()
```

---

# 14. Area Chart in ML

Training progress:

```python
epochs=[
1,2,3,4,5
]


accuracy=[
50,
60,
75,
85,
92
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.fill_between(
    epochs,
    accuracy
)


ax.set_title(
    "Accuracy Growth"
)


plt.show()
```

---

# 15. Pie Chart vs Bar Chart

## Pie Chart

Use:

```
Part of whole
```

Example:

```
Normal 75%
Attack 25%
```

---

## Bar Chart

Use:

```
Category comparison
```

Example:

```
Normal 30000
Attack 10000
```

---

# 16. Area Chart vs Line Chart

## Line Chart:

Trend দেখতে:

```
Revenue increase
```

## Area Chart:

Trend + magnitude দেখতে:

```
Total growth volume
```

---

# Lesson 9 Practice Task

## Task 1: Pie Chart

Technology skill distribution:

```
Python     40
Django     25
React      20
ML         15
```

Create:

* Pie chart
* Percentage
* Explode Python slice

---

## Task 2: Area Chart

Monthly revenue:

```python
months=[
1,2,3,4,5,6
]


revenue=[
100,
150,
180,
220,
300,
350
]
```

Create:

* Area chart
* Title
* Labels
* Grid

---

## Task 3 (ML)

UCF Crime class distribution:

```
Normal       30000
Suspicious   10000
```

Create:

1. Pie chart
2. Area chart of model accuracy over epochs

---

পরের Lesson:

# Lesson 10: Working with NumPy Arrays in Matplotlib

শিখবো:

* NumPy + Matplotlib integration
* Vectorized plotting
* Random data generation
* Scientific visualization
* ML dataset visualization pipeline

এটা Data Science workflow-এর জন্য খুব গুরুত্বপূর্ণ।
# Matplotlib Mastery Course

# Lesson 10: NumPy + Matplotlib Integration (Scientific Visualization)

আজ আমরা শিখবো কীভাবে **NumPy array ব্যবহার করে Matplotlib-এ professional visualization** তৈরি করতে হয়।

Data Science, Machine Learning, Deep Learning-এ সাধারণত data আসে:

* NumPy array
* Pandas DataFrame
* Tensor

তাই Matplotlib-এর সাথে NumPy integration জানা খুব গুরুত্বপূর্ণ।

---

# 1. কেন NumPy + Matplotlib?

Python list:

```python
x = [1,2,3,4,5]
```

ছোট data-এর জন্য ভালো।

কিন্তু ML/Data Science-এ:

```python
x = np.array([
1,2,3,4,5
])
```

ব্যবহার করা হয়।

কারণ NumPy:

* দ্রুত
* vectorized operation support করে
* large dataset handle করতে পারে
* mathematical operation সহজ করে

---

# 2. NumPy Import

```python
import numpy as np

import matplotlib.pyplot as plt
```

---

# 3. NumPy Array দিয়ে Simple Line Plot

```python
import numpy as np
import matplotlib.pyplot as plt


x = np.array(
    [1,2,3,4,5]
)


y = np.array(
    [10,20,30,40,50]
)


fig, ax = plt.subplots()


ax.plot(
    x,
    y
)


plt.show()
```

Matplotlib সরাসরি NumPy array accept করে।

---

# 4. NumPy দিয়ে Data Generate করা

Manual data না লিখে:

```python
np.arange()
```

ব্যবহার করা যায়।

Example:

```python
x = np.arange(
    0,
    10,
    1
)


print(x)
```

Output:

```
[0 1 2 3 4 5 6 7 8 9]
```

---

# 5. Mathematical Function Plot

এটা scientific computing-এ অনেক ব্যবহার হয়।

Example:

y = x²

```python
import numpy as np
import matplotlib.pyplot as plt


x = np.arange(
    0,
    10,
    0.1
)


y = x**2


fig, ax = plt.subplots()


ax.plot(
    x,
    y
)


ax.set_title(
    "y = x²"
)


plt.show()
```

---

# 6. Sin Wave Visualization

Machine Learning এবং signal processing-এ useful।

Formula:

```
y = sin(x)
```

Code:

```python
import numpy as np
import matplotlib.pyplot as plt


x = np.linspace(
    0,
    2*np.pi,
    100
)


y = np.sin(x)


fig, ax = plt.subplots()


ax.plot(
    x,
    y
)


ax.set_title(
    "Sine Wave"
)


plt.show()
```

---

# 7. np.linspace() কী?

`linspace()` নির্দিষ্ট সংখ্যক evenly spaced value তৈরি করে।

Example:

```python
np.linspace(
0,
10,
5
)
```

Output:

```
[0,2.5,5,7.5,10]
```

Syntax:

```python
np.linspace(
start,
stop,
number_of_values
)
```

---

# 8. Random Data Visualization

Machine Learning experiment-এ random data দরকার হয়।

Generate:

```python
data = np.random.randn(1000)
```

Example:

```python
import numpy as np
import matplotlib.pyplot as plt


data = np.random.randn(
    1000
)


fig, ax = plt.subplots()


ax.hist(
    data,
    bins=30
)


plt.show()
```

এখানে আমরা normal distribution দেখছি।

---

# 9. NumPy Array Statistics

Example:

```python
data = np.random.randn(1000)


print(
    np.mean(data)
)


print(
    np.std(data)
)
```

Output:

```
mean ≈ 0

std ≈ 1
```

---

# 10. Multiple Lines with NumPy

Example:

```python
x = np.arange(
0,
10,
0.5
)


y1 = x

y2 = x**2

y3 = x**3
```

Plot:

```python
fig, ax = plt.subplots()


ax.plot(
    x,
    y1,
    label="x"
)


ax.plot(
    x,
    y2,
    label="x²"
)


ax.plot(
    x,
    y3,
    label="x³"
)


ax.legend()


plt.show()
```

---

# 11. NumPy Matrix Visualization

Machine Learning-এ matrix data অনেক আসে।

Example:

```python
matrix = np.random.rand(
10,
10
)
```

Visualize:

```python
fig, ax = plt.subplots()


ax.imshow(
    matrix
)


plt.colorbar()


plt.show()
```

এটা heatmap-এর base concept।

---

# 12. Image Visualization (Important for Deep Learning)

Image হলো NumPy array।

Example:

```python
image = np.random.rand(
64,
64
)
```

Display:

```python
fig, ax = plt.subplots()


ax.imshow(
    image
)


ax.axis(
"off"
)


plt.show()
```

---

# 13. UCF Crime Dataset Connection

তোমার AI CCTV project-এ:

একটি frame:

```
Image Shape:

(64,64,3)
```

মানে:

```
Height = 64

Width = 64

Channel = 3
```

NumPy array:

```python
frame.shape
```

Output:

```
(64,64,3)
```

Visualize:

```python
plt.imshow(frame)

plt.show()
```

---

# 14. ML Training Data Visualization

ধরি:

```python
epochs = np.arange(
1,
11
)


loss = np.array(
[
0.9,
0.8,
0.7,
0.5,
0.4,
0.3,
0.25,
0.2,
0.15,
0.1
]
)
```

Plot:

```python
fig, ax = plt.subplots()


ax.plot(
    epochs,
    loss,
    marker="o"
)


ax.set_title(
    "Training Loss"
)


plt.show()
```

---

# 15. NumPy + Subplot Dashboard

Example:

```python
import numpy as np
import matplotlib.pyplot as plt


x = np.linspace(
0,
10,
100
)


fig, axes = plt.subplots(
2,
2,
figsize=(10,8)
)


axes[0,0].plot(
x,
x
)


axes[0,1].plot(
x,
x**2
)


axes[1,0].plot(
x,
np.sin(x)
)


axes[1,1].hist(
np.random.randn(500),
bins=30
)


plt.tight_layout()

plt.show()
```

---

# 16. Real Data Science Pipeline

সাধারণ workflow:

```
Raw Data

↓

NumPy Array

↓

Data Processing

↓

Matplotlib Visualization

↓

Model Training
```

---

# Lesson 10 Practice Task

## Task 1

NumPy দিয়ে:

```python
x = np.linspace(
0,
10,
100
)
```

Create:

```
y = x²
```

Plot:

* Title
* Labels
* Grid

---

## Task 2

Generate:

```python
data=np.random.normal(
50,
10,
1000
)
```

Create:

* Histogram
* 30 bins
* Mean line

---

## Task 3 (Deep Learning)

Create fake image:

```python
image=np.random.rand(
64,
64
)
```

Show:

* Image visualization
* Colorbar
* Remove axis

---

## Task 4 (ML)

Create training dashboard:

Data:

```python
epochs=np.arange(1,11)

loss=np.random.rand(10)

accuracy=np.random.rand(10)*100
```

Show:

* Loss curve
* Accuracy curve

একটি Figure-এ।

---

পরের Lesson:

# Lesson 11: Matplotlib + Pandas Integration

শিখবো:

* DataFrame থেকে plotting
* CSV data visualization
* Real dataset analysis
* E-commerce sales analysis
* ML dataset EDA pipeline

এটা Data Engineer এবং ML Engineer workflow-এর জন্য সবচেয়ে বেশি ব্যবহার হবে।


# Matplotlib Mastery Course

# Lesson 11: Matplotlib + Pandas Integration (Real Dataset Visualization)

আজ আমরা শিখবো কীভাবে **Pandas DataFrame থেকে সরাসরি Matplotlib visualization** তৈরি করতে হয়।

Real-world data সাধারণত আসে:

* CSV file
* Excel file
* Database query
* API response

এবং সেগুলো আমরা Pandas DataFrame-এ রাখি।

তারপর:

```
Data Source
     |
     ↓
 Pandas DataFrame
     |
     ↓
 Matplotlib Visualization
```

এই workflow Data Engineer, Data Analyst এবং ML Engineer-দের জন্য খুব গুরুত্বপূর্ণ।

---

# 1. Pandas + Matplotlib Import

```python
import pandas as pd
import matplotlib.pyplot as plt
```

---

# 2. DataFrame Create করা

Example:

```python
import pandas as pd


data = {
    "Month": [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May"
    ],

    "Sales": [
        100,
        150,
        120,
        200,
        250
    ]
}


df = pd.DataFrame(data)


print(df)
```

Output:

```
  Month  Sales
0 Jan     100
1 Feb     150
2 Mar     120
3 Apr     200
4 May     250
```

---

# 3. DataFrame থেকে Line Plot

```python
fig, ax = plt.subplots()


ax.plot(
    df["Month"],
    df["Sales"]
)


ax.set_title(
    "Monthly Sales"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Sales"
)


plt.show()
```

---

# 4. Pandas Built-in Plot

Pandas নিজেও Matplotlib ব্যবহার করে।

Example:

```python
df.plot(
    x="Month",
    y="Sales",
    kind="line"
)


plt.show()
```

Internally:

```
Pandas
 |
 |
Matplotlib
```

---

# 5. CSV File থেকে Visualization

Real project:

```
sales.csv
```

Example:

```csv
Month,Sales
Jan,100
Feb,150
Mar,120
Apr,200
```

Load:

```python
df = pd.read_csv(
    "sales.csv"
)
```

Check:

```python
df.head()
```

Plot:

```python
df.plot(
    x="Month",
    y="Sales",
    kind="line"
)


plt.show()
```

---

# 6. Bar Chart from DataFrame

Example:

```python
df = pd.DataFrame({

"Product":[
"Laptop",
"Mobile",
"Tablet"
],

"Sales":[
100,
250,
150
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.bar(
    df["Product"],
    df["Sales"]
)


ax.set_title(
    "Product Sales"
)


plt.show()
```

---

# 7. DataFrame Histogram

Dataset:

```python
df = pd.DataFrame({

"Age":[
20,
22,
25,
30,
35,
40,
45
]

})
```

Histogram:

```python
fig, ax = plt.subplots()


ax.hist(
    df["Age"],
    bins=5
)


ax.set_title(
    "Age Distribution"
)


plt.show()
```

---

# 8. Scatter Plot from DataFrame

Example:

```python
df = pd.DataFrame({

"Experience":[
1,2,3,4,5
],

"Salary":[
20000,
30000,
45000,
60000,
80000
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.scatter(
    df["Experience"],
    df["Salary"]
)


ax.set_xlabel(
    "Experience"
)


ax.set_ylabel(
    "Salary"
)


plt.show()
```

---

# 9. Multiple Columns Visualization

Example:

```python
df = pd.DataFrame({

"Month":[
"Jan",
"Feb",
"Mar"
],

"2025":[
100,
150,
200
],

"2026":[
130,
180,
250
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.plot(
    df["Month"],
    df["2025"],
    label="2025"
)


ax.plot(
    df["Month"],
    df["2026"],
    label="2026"
)


ax.legend()


plt.show()
```

---

# 10. DataFrame Box Plot

Machine Learning EDA-তে খুব দরকার।

Example:

```python
df = pd.DataFrame({

"Age":[
20,
25,
30,
35,
100
],

"Salary":[
20000,
30000,
50000,
70000,
500000
]

})
```

Plot:

```python
df.boxplot()


plt.show()
```

এখানে outlier দেখা যাবে।

---

# 11. Correlation Analysis

ML-এ feature relationship দেখতে:

```python
df.corr()
```

Example:

```python
correlation = df.corr()


print(correlation)
```

Output:

```
          Age Salary

Age       1.0  0.9

Salary    0.9  1.0
```

---

# 12. Correlation Heatmap (Matplotlib)

Pure Matplotlib:

```python
fig, ax = plt.subplots()


image = ax.imshow(
    correlation
)


plt.colorbar(
    image
)


plt.show()
```

---

# 13. Real E-commerce Data Example

ধরি:

```python
df = pd.DataFrame({

"Category":[
"Phone",
"Laptop",
"Camera",
"Watch"
],

"Revenue":[
50000,
90000,
30000,
20000
]

})
```

Visualization:

```python
fig, ax = plt.subplots(
    figsize=(8,5)
)


ax.bar(
    df["Category"],
    df["Revenue"]
)


ax.set_title(
    "Revenue by Category"
)


plt.show()
```

---

# 14. ML Dataset EDA Workflow

Example:

Dataset:

```
UCF Crime Dataset
```

Workflow:

```
Images
  |
  ↓
NumPy Array
  |
  ↓
Pandas Metadata
  |
  ↓
Matplotlib

Visualization:

- Class distribution
- Frame count
- Confidence score
- Accuracy
```

---

# 15. Complete Data Analysis Dashboard

```python
import pandas as pd
import matplotlib.pyplot as plt


df = pd.DataFrame({

"Month":[
"Jan",
"Feb",
"Mar",
"Apr"
],

"Sales":[
100,
200,
150,
300
],

"Profit":[
20,
50,
30,
80
]

})


fig, axes = plt.subplots(
1,
2,
figsize=(10,4)
)


axes[0].plot(
df["Month"],
df["Sales"]
)

axes[0].set_title(
"Sales"
)


axes[1].bar(
df["Month"],
df["Profit"]
)

axes[1].set_title(
"Profit"
)


plt.tight_layout()

plt.show()
```

---

# 16. Production Workflow

Industry workflow:

```
Database
   |
   ↓
SQL Query
   |
   ↓
Pandas DataFrame
   |
   ↓
EDA
   |
   ↓
Matplotlib
   |
   ↓
ML Model
```

---

# Lesson 11 Practice Task

## Task 1: Sales Dataset

Create DataFrame:

```python
data = {

"Month":[
"Jan",
"Feb",
"Mar",
"Apr",
"May"
],

"Sales":[
100,
200,
150,
300,
350
]

}
```

Create:

* Line chart
* Bar chart

---

## Task 2: Employee Analysis

Dataset:

```python
Name:
A,B,C,D,E


Salary:
30000,50000,70000,45000,90000


Experience:
1,3,5,2,7
```

Create:

* Salary distribution histogram
* Experience vs Salary scatter plot

---

## Task 3 (ML)

Create fake model result DataFrame:

```python
Epoch:
1,2,3,4,5


Loss:
0.9,0.6,0.4,0.2,0.1


Accuracy:
50,65,75,85,95
```

Create:

* Loss curve
* Accuracy curve
* Same figure using subplot

---

পরের Lesson:

# Lesson 12: Real Dataset Visualization Project

শিখবো:

* CSV dataset analysis
* Data cleaning
* EDA workflow
* Missing value visualization
* Distribution analysis
* Professional report তৈরি

এখান থেকে Matplotlib real-world usage শুরু হবে।
# Matplotlib Mastery Course

# Lesson 11: Matplotlib + Pandas Integration (Real Dataset Visualization)

আজ আমরা শিখবো কীভাবে **Pandas DataFrame থেকে সরাসরি Matplotlib visualization** তৈরি করতে হয়।

Real-world data সাধারণত আসে:

* CSV file
* Excel file
* Database query
* API response

এবং সেগুলো আমরা Pandas DataFrame-এ রাখি।

তারপর:

```
Data Source
     |
     ↓
 Pandas DataFrame
     |
     ↓
 Matplotlib Visualization
```

এই workflow Data Engineer, Data Analyst এবং ML Engineer-দের জন্য খুব গুরুত্বপূর্ণ।

---

# 1. Pandas + Matplotlib Import

```python
import pandas as pd
import matplotlib.pyplot as plt
```

---

# 2. DataFrame Create করা

Example:

```python
import pandas as pd


data = {
    "Month": [
        "Jan",
        "Feb",
        "Mar",
        "Apr",
        "May"
    ],

    "Sales": [
        100,
        150,
        120,
        200,
        250
    ]
}


df = pd.DataFrame(data)


print(df)
```

Output:

```
  Month  Sales
0 Jan     100
1 Feb     150
2 Mar     120
3 Apr     200
4 May     250
```

---

# 3. DataFrame থেকে Line Plot

```python
fig, ax = plt.subplots()


ax.plot(
    df["Month"],
    df["Sales"]
)


ax.set_title(
    "Monthly Sales"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Sales"
)


plt.show()
```

---

# 4. Pandas Built-in Plot

Pandas নিজেও Matplotlib ব্যবহার করে।

Example:

```python
df.plot(
    x="Month",
    y="Sales",
    kind="line"
)


plt.show()
```

Internally:

```
Pandas
 |
 |
Matplotlib
```

---

# 5. CSV File থেকে Visualization

Real project:

```
sales.csv
```

Example:

```csv
Month,Sales
Jan,100
Feb,150
Mar,120
Apr,200
```

Load:

```python
df = pd.read_csv(
    "sales.csv"
)
```

Check:

```python
df.head()
```

Plot:

```python
df.plot(
    x="Month",
    y="Sales",
    kind="line"
)


plt.show()
```

---

# 6. Bar Chart from DataFrame

Example:

```python
df = pd.DataFrame({

"Product":[
"Laptop",
"Mobile",
"Tablet"
],

"Sales":[
100,
250,
150
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.bar(
    df["Product"],
    df["Sales"]
)


ax.set_title(
    "Product Sales"
)


plt.show()
```

---

# 7. DataFrame Histogram

Dataset:

```python
df = pd.DataFrame({

"Age":[
20,
22,
25,
30,
35,
40,
45
]

})
```

Histogram:

```python
fig, ax = plt.subplots()


ax.hist(
    df["Age"],
    bins=5
)


ax.set_title(
    "Age Distribution"
)


plt.show()
```

---

# 8. Scatter Plot from DataFrame

Example:

```python
df = pd.DataFrame({

"Experience":[
1,2,3,4,5
],

"Salary":[
20000,
30000,
45000,
60000,
80000
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.scatter(
    df["Experience"],
    df["Salary"]
)


ax.set_xlabel(
    "Experience"
)


ax.set_ylabel(
    "Salary"
)


plt.show()
```

---

# 9. Multiple Columns Visualization

Example:

```python
df = pd.DataFrame({

"Month":[
"Jan",
"Feb",
"Mar"
],

"2025":[
100,
150,
200
],

"2026":[
130,
180,
250
]

})
```

Plot:

```python
fig, ax = plt.subplots()


ax.plot(
    df["Month"],
    df["2025"],
    label="2025"
)


ax.plot(
    df["Month"],
    df["2026"],
    label="2026"
)


ax.legend()


plt.show()
```

---

# 10. DataFrame Box Plot

Machine Learning EDA-তে খুব দরকার।

Example:

```python
df = pd.DataFrame({

"Age":[
20,
25,
30,
35,
100
],

"Salary":[
20000,
30000,
50000,
70000,
500000
]

})
```

Plot:

```python
df.boxplot()


plt.show()
```

এখানে outlier দেখা যাবে।

---

# 11. Correlation Analysis

ML-এ feature relationship দেখতে:

```python
df.corr()
```

Example:

```python
correlation = df.corr()


print(correlation)
```

Output:

```
          Age Salary

Age       1.0  0.9

Salary    0.9  1.0
```

---

# 12. Correlation Heatmap (Matplotlib)

Pure Matplotlib:

```python
fig, ax = plt.subplots()


image = ax.imshow(
    correlation
)


plt.colorbar(
    image
)


plt.show()
```

---

# 13. Real E-commerce Data Example

ধরি:

```python
df = pd.DataFrame({

"Category":[
"Phone",
"Laptop",
"Camera",
"Watch"
],

"Revenue":[
50000,
90000,
30000,
20000
]

})
```

Visualization:

```python
fig, ax = plt.subplots(
    figsize=(8,5)
)


ax.bar(
    df["Category"],
    df["Revenue"]
)


ax.set_title(
    "Revenue by Category"
)


plt.show()
```

---

# 14. ML Dataset EDA Workflow

Example:

Dataset:

```
UCF Crime Dataset
```

Workflow:

```
Images
  |
  ↓
NumPy Array
  |
  ↓
Pandas Metadata
  |
  ↓
Matplotlib

Visualization:

- Class distribution
- Frame count
- Confidence score
- Accuracy
```

---

# 15. Complete Data Analysis Dashboard

```python
import pandas as pd
import matplotlib.pyplot as plt


df = pd.DataFrame({

"Month":[
"Jan",
"Feb",
"Mar",
"Apr"
],

"Sales":[
100,
200,
150,
300
],

"Profit":[
20,
50,
30,
80
]

})


fig, axes = plt.subplots(
1,
2,
figsize=(10,4)
)


axes[0].plot(
df["Month"],
df["Sales"]
)

axes[0].set_title(
"Sales"
)


axes[1].bar(
df["Month"],
df["Profit"]
)

axes[1].set_title(
"Profit"
)


plt.tight_layout()

plt.show()
```

---

# 16. Production Workflow

Industry workflow:

```
Database
   |
   ↓
SQL Query
   |
   ↓
Pandas DataFrame
   |
   ↓
EDA
   |
   ↓
Matplotlib
   |
   ↓
ML Model
```

---

# Lesson 11 Practice Task

## Task 1: Sales Dataset

Create DataFrame:

```python
data = {

"Month":[
"Jan",
"Feb",
"Mar",
"Apr",
"May"
],

"Sales":[
100,
200,
150,
300,
350
]

}
```

Create:

* Line chart
* Bar chart

---

## Task 2: Employee Analysis

Dataset:

```python
Name:
A,B,C,D,E


Salary:
30000,50000,70000,45000,90000


Experience:
1,3,5,2,7
```

Create:

* Salary distribution histogram
* Experience vs Salary scatter plot

---

## Task 3 (ML)

Create fake model result DataFrame:

```python
Epoch:
1,2,3,4,5


Loss:
0.9,0.6,0.4,0.2,0.1


Accuracy:
50,65,75,85,95
```

Create:

* Loss curve
* Accuracy curve
* Same figure using subplot

---

পরের Lesson:

# Lesson 12: Real Dataset Visualization Project

শিখবো:

* CSV dataset analysis
* Data cleaning
* EDA workflow
* Missing value visualization
* Distribution analysis
* Professional report তৈরি

এখান থেকে Matplotlib real-world usage শুরু হবে।

# Matplotlib Mastery Course

# Lesson 13: Object-Oriented API Mastery (Professional Matplotlib Architecture)

আজ থেকে আমরা Matplotlib-এর **advanced/professional level** শুরু করছি।

আগের lesson পর্যন্ত আমরা:

```python
plt.plot()
plt.bar()
plt.hist()
```

ব্যবহার করেছি।

কিন্তু বড় project, ML research, production dashboard-এ ব্যবহার করা হয়:

```python
Figure + Axes Object-Oriented API
```

---

# 1. Matplotlib Architecture বুঝি

Matplotlib-এর hierarchy:

```text
Matplotlib

    |
    |
  Figure
    |
    |
  Axes
    |
    |
  Axis
    |
    |
 Artists
```

## Figure

পুরো canvas।

Example:

```text
+----------------------+
|                      |
|      Figure          |
|                      |
+----------------------+
```

---

## Axes

যেখানে graph আঁকা হয়।

```text
Figure

+----------------+
|                |
|     Axes       |
|   (Graph)      |
|                |
+----------------+
```

---

# 2. Figure এবং Axes তৈরি

Professional way:

```python
import matplotlib.pyplot as plt


fig, ax = plt.subplots()


print(fig)

print(ax)
```

এখানে:

```python
fig
```

= Figure object

```python
ax
```

= Axes object

---

# 3. কেন Object-Oriented API ব্যবহার করবো?

কারণ:

## Multiple charts

```text
Figure

+--------+--------+
| Axes1  | Axes2  |
+--------+--------+

```

## Better control

যেমন:

```python
ax.set_title()

ax.set_xlabel()

ax.set_ylabel()
```

## Large ML experiments

Example:

```text
Figure

Loss Curve

Accuracy Curve

Confusion Matrix

ROC Curve

```

সব manage করা সহজ।

---

# 4. Figure Control

## Figure Size

```python
fig, ax = plt.subplots(
    figsize=(8,5)
)
```

Meaning:

```text
width = 8 inch

height = 5 inch
```

---

## DPI

DPI = Resolution

```python
fig, ax = plt.subplots(
    dpi=150
)
```

Higher DPI:

* Better quality
* Publication ready

---

# 5. Axes Control

Example:

```python
import matplotlib.pyplot as plt


x=[1,2,3,4]

y=[10,20,30,40]


fig, ax = plt.subplots()


ax.plot(
    x,
    y
)


ax.set_title(
    "Sales Growth"
)


ax.set_xlabel(
    "Month"
)


ax.set_ylabel(
    "Revenue"
)


plt.show()
```

---

# 6. Difference: plt vs ax

## Pyplot style

```python
plt.title(
"Sales"
)

plt.xlabel(
"Month"
)

plt.ylabel(
"Revenue"
)
```

---

## Object style

```python
ax.set_title(
"Sales"
)


ax.set_xlabel(
"Month"
)


ax.set_ylabel(
"Revenue"
)
```

Professional projects:

```text
ax method বেশি ব্যবহার হয়
```

---

# 7. Multiple Axes Control

Example:

```python
fig, axes = plt.subplots(
    1,
    2
)


axes[0].plot(
    [1,2,3],
    [10,20,30]
)


axes[1].bar(
    ["A","B"],
    [20,30]
)


plt.show()
```

এখানে:

```python
axes[0]
```

প্রথম graph

```python
axes[1]
```

দ্বিতীয় graph

---

# 8. Axis Object

Axes-এর ভিতরে Axis থাকে।

Example:

```python
ax.xaxis

ax.yaxis
```

দিয়ে axis control করা যায়।

---

# 9. Tick Control

Example:

```python
fig, ax = plt.subplots()


x=[
1,
2,
3,
4,
5
]


y=[
10,
20,
30,
40,
50
]


ax.plot(
x,
y
)


ax.set_xticks(
[1,2,3,4,5]
)


plt.show()
```

---

# 10. Custom Tick Labels

Example:

```python
months=[
"Jan",
"Feb",
"Mar",
"Apr"
]


sales=[
100,
200,
150,
300
]


fig, ax = plt.subplots()


ax.plot(
range(4),
sales
)


ax.set_xticks(
range(4)
)


ax.set_xticklabels(
months
)


plt.show()
```

---

# 11. Spine Control

Spine হলো graph border।

Example:

```python
fig, ax = plt.subplots()


ax.plot(
[1,2,3],
[10,20,30]
)


ax.spines[
"top"
].set_visible(False)


ax.spines[
"right"
].set_visible(False)


plt.show()
```

Common:

```text
top

bottom

left

right
```

---

# 12. Annotation

Graph-এর নির্দিষ্ট point explain করা।

Example:

```python
fig, ax = plt.subplots()


x=[
1,2,3,4
]


y=[
10,20,30,40
]


ax.plot(
x,
y,
marker="o"
)


ax.annotate(
"Highest Point",
xy=(4,40),
xytext=(2,35),
arrowprops={}
)


plt.show()
```

---

# 13. ML Training Visualization Example

ধরি:

```python
epochs=[
1,2,3,4,5
]


loss=[
0.9,
0.6,
0.4,
0.2,
0.1
]


accuracy=[
50,
65,
75,
85,
95
]
```

Professional dashboard:

```python
fig, axes = plt.subplots(
1,
2,
figsize=(12,4)
)


axes[0].plot(
epochs,
loss,
marker="o"
)


axes[0].set_title(
"Loss Curve"
)



axes[1].plot(
epochs,
accuracy,
marker="o"
)


axes[1].set_title(
"Accuracy Curve"
)



plt.tight_layout()

plt.show()
```

---

# 14. Real Project Structure

Production visualization code:

```python
def create_training_plot(history):

    fig, axes = plt.subplots(
        1,
        2
    )


    axes[0].plot(
        history["loss"]
    )


    axes[1].plot(
        history["accuracy"]
    )


    plt.show()
```

এভাবে reusable visualization function তৈরি করা হয়।

---

# 15. Object-Oriented Best Practice Template

এটা মনে রাখবে:

```python
import matplotlib.pyplot as plt


fig, ax = plt.subplots(
    figsize=(10,6),
    dpi=120
)


ax.plot(
    x,
    y
)


ax.set_title(
    "Title"
)


ax.set_xlabel(
    "X Label"
)


ax.set_ylabel(
    "Y Label"
)


ax.grid()


plt.tight_layout()

plt.show()
```

এটাই industry standard pattern।

---

# Lesson 13 Practice Task

## Task 1

Object-oriented style দিয়ে তৈরি করো:

Data:

```python
x=[1,2,3,4,5]

y=[5,10,15,20,25]
```

Requirements:

* Figure size
* DPI
* Title
* Labels
* Grid

---

## Task 2

একটি dashboard তৈরি করো:

Figure:

```
+-------------+-------------+
| Line Plot   | Bar Plot    |
+-------------+-------------+
| Scatter     | Histogram   |
+-------------+-------------+
```

---

## Task 3 (ML)

Training visualization function লিখো:

Input:

```python
history={
"loss":[0.9,0.5,0.2],
"accuracy":[50,75,90]
}
```

Output:

* Loss graph
* Accuracy graph

---

পরের Lesson:

# Lesson 14: Figure Size, DPI এবং Publication Quality Visualization

শিখবো:

* High resolution image
* Paper quality figure
* Export settings
* PNG/PDF/SVG
* Professional report visualization

এগুলো ML research এবং production reporting-এ ব্যবহার হয়।
# Matplotlib Mastery Course

# Lesson 14: Figure Size, DPI & Publication Quality Visualization

আজ আমরা শিখবো কীভাবে **professional quality graph** তৈরি করতে হয়।

একজন Data Scientist / ML Engineer শুধু graph বানায় না, তাকে graph:

* Research paper
* Presentation
* Dashboard
* Report
* Client documentation

এর জন্য **high quality format-এ export** করতে হয়।

আজকের topic:

* Figure size
* DPI
* Resolution
* Aspect ratio
* Savefig
* PNG/PDF/SVG export
* Publication quality settings

---

# 1. Figure Size কী?

Figure size হলো graph-এর physical size।

Syntax:

```python id="4o4n7p"
fig, ax = plt.subplots(
    figsize=(width, height)
)
```

Example:

```python id="8lqkzv"
import matplotlib.pyplot as plt


fig, ax = plt.subplots(
    figsize=(10,5)
)


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.show()
```

এখানে:

```text id="0q1k5f"
width  = 10 inch

height = 5 inch
```

---

# 2. Figure Size কেন Important?

Wrong size:

```text id="8qv1z7"
Small graph

Text overlap

Labels unreadable
```

Good size:

```text id="xqv6gk"
Large canvas

Clear labels

Professional look
```

---

# 3. Common Figure Sizes

## Small chart

```python id="l1x8cz"
figsize=(5,3)
```

Use:

* Blog
* Small report

---

## Standard

```python id="3q1h1n"
figsize=(8,5)
```

Use:

* General analysis

---

## Presentation

```python id="m8x6r5"
figsize=(12,7)
```

Use:

* Slides
* Dashboard

---

## Research Paper

```python id="qk47q5"
figsize=(6,4)
```

---

# 4. DPI কী?

DPI:

```
Dots Per Inch
```

মানে প্রতি inch-এ কত pixel থাকবে।

Low DPI:

```python id="0p4u1s"
dpi=50
```

Result:

```text
Low quality
Blur image
```

High DPI:

```python id="x0w2u1"
dpi=300
```

Result:

```text
Sharp image
Publication quality
```

---

# 5. DPI Example

```python id="3w1d2u"
fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=300
)


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.show()
```

---

# 6. Figure Size + DPI Combination

Professional template:

```python id="9xq2vq"
fig, ax = plt.subplots(
    figsize=(10,6),
    dpi=300
)
```

এটা:

* ML paper
* Research report
* Documentation

এর জন্য ভালো।

---

# 7. Save Figure

Graph save করতে:

```python id="m1xv6g"
plt.savefig(
    "graph.png"
)
```

Example:

```python id="2x7m6v"
fig, ax = plt.subplots()


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.savefig(
    "sales.png"
)
```

---

# 8. High Quality Save

Important parameters:

```python id="h8z1dc"
plt.savefig(
    "graph.png",
    dpi=300,
    bbox_inches="tight"
)
```

## dpi

Resolution

## bbox_inches="tight"

Extra white space remove করে।

---

# 9. Different File Formats

Matplotlib support করে:

## PNG

```python id="l5h2tq"
plt.savefig(
"chart.png"
)
```

Use:

* Web
* Presentation

---

## PDF

```python id="5r8n5j"
plt.savefig(
"chart.pdf"
)
```

Use:

* Research paper
* Report

---

## SVG

```python id="3n1l2w"
plt.savefig(
"chart.svg"
)
```

Use:

* Vector graphics
* Editing

---

# 10. Transparent Background

Example:

```python id="h1k5pv"
plt.savefig(
"chart.png",
transparent=True
)
```

Useful:

* Website
* Slides

---

# 11. Multiple Export

একই graph:

```python id="3h9m0d"
plt.savefig(
"result.png",
dpi=300
)


plt.savefig(
"result.pdf"
)
```

---

# 12. Tight Layout

Problem:

```text
Title cut off

Labels overlap
```

Solution:

```python id="8x7m3k"
plt.tight_layout()
```

Example:

```python id="v0n7xk"
fig, ax = plt.subplots(
figsize=(10,6)
)


ax.plot(
[1,2,3],
[10,20,30]
)


plt.tight_layout()


plt.show()
```

---

# 13. Constrained Layout

আরেকটি modern approach:

```python id="9xq8bw"
fig, ax = plt.subplots(
constrained_layout=True
)
```

---

# 14. ML Research Example

ধরি CNN training result:

```python id="v9m2k8"
epochs=[
1,2,3,4,5
]


accuracy=[
60,
70,
80,
90,
95
]
```

Publication quality:

```python id="5q8p3n"
import matplotlib.pyplot as plt


fig, ax = plt.subplots(
    figsize=(7,5),
    dpi=300
)


ax.plot(
    epochs,
    accuracy,
    marker="o"
)


ax.set_title(
    "CNN Training Accuracy"
)


ax.set_xlabel(
    "Epoch"
)


ax.set_ylabel(
    "Accuracy (%)"
)


ax.grid()


plt.tight_layout()


plt.savefig(
    "cnn_accuracy.pdf",
    bbox_inches="tight"
)


plt.show()
```

---

# 15. Image Dimension Calculation

Formula:

```
Pixels = Figure Size × DPI
```

Example:

```text
figsize=(10,5)

dpi=300
```

Result:

```
width:
10 × 300 = 3000 pixels


height:
5 × 300 = 1500 pixels
```

Final image:

```
3000 × 1500 px
```

---

# 16. Professional Visualization Checklist

Graph export করার আগে:

✅ Proper figure size

✅ DPI >= 300

✅ Clear labels

✅ Readable font

✅ No overlapping

✅ Tight layout

✅ Correct file format

---

# 17. Real Data Engineering Usage

Production report:

```text
SQL Database

↓

Pandas Analysis

↓

Matplotlib Visualization

↓

PDF Report

↓

Business Decision
```

---

# Lesson 14 Practice Task

## Task 1

একটি graph তৈরি করো:

Requirements:

```python
figsize=(10,6)

dpi=300
```

Data:

```python
x=[1,2,3,4,5]

y=[20,40,60,80,100]
```

Save:

* PNG
* PDF

---

## Task 2 (ML)

Fake model:

```python
epochs=[1,2,3,4,5]

accuracy=[60,70,80,88,95]
```

Create:

* Publication quality accuracy curve
* dpi=300
* Save as PDF

---

## Task 3

একটি 2×2 ML dashboard তৈরি করো:

* Loss curve
* Accuracy curve
* Confusion matrix
* Prediction distribution

Export:

```text
model_report.png
```

---

পরের Lesson:

# Lesson 15: Colors, Colormaps & Professional Styling

শিখবো:

* Color theory
* Built-in colormap
* Continuous vs categorical colors
* Heatmap coloring
* ML visualization styling

এটা graph-কে professional এবং readable করে তুলবে।


------

# Matplotlib Mastery Course

# Lesson 14: Figure Size, DPI & Publication Quality Visualization

আজ আমরা শিখবো কীভাবে **professional quality graph** তৈরি করতে হয়।

একজন Data Scientist / ML Engineer শুধু graph বানায় না, তাকে graph:

* Research paper
* Presentation
* Dashboard
* Report
* Client documentation

এর জন্য **high quality format-এ export** করতে হয়।

আজকের topic:

* Figure size
* DPI
* Resolution
* Aspect ratio
* Savefig
* PNG/PDF/SVG export
* Publication quality settings

---

# 1. Figure Size কী?

Figure size হলো graph-এর physical size।

Syntax:

```python id="4o4n7p"
fig, ax = plt.subplots(
    figsize=(width, height)
)
```

Example:

```python id="8lqkzv"
import matplotlib.pyplot as plt


fig, ax = plt.subplots(
    figsize=(10,5)
)


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.show()
```

এখানে:

```text id="0q1k5f"
width  = 10 inch

height = 5 inch
```

---

# 2. Figure Size কেন Important?

Wrong size:

```text id="8qv1z7"
Small graph

Text overlap

Labels unreadable
```

Good size:

```text id="xqv6gk"
Large canvas

Clear labels

Professional look
```

---

# 3. Common Figure Sizes

## Small chart

```python id="l1x8cz"
figsize=(5,3)
```

Use:

* Blog
* Small report

---

## Standard

```python id="3q1h1n"
figsize=(8,5)
```

Use:

* General analysis

---

## Presentation

```python id="m8x6r5"
figsize=(12,7)
```

Use:

* Slides
* Dashboard

---

## Research Paper

```python id="qk47q5"
figsize=(6,4)
```

---

# 4. DPI কী?

DPI:

```
Dots Per Inch
```

মানে প্রতি inch-এ কত pixel থাকবে।

Low DPI:

```python id="0p4u1s"
dpi=50
```

Result:

```text
Low quality
Blur image
```

High DPI:

```python id="x0w2u1"
dpi=300
```

Result:

```text
Sharp image
Publication quality
```

---

# 5. DPI Example

```python id="3w1d2u"
fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=300
)


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.show()
```

---

# 6. Figure Size + DPI Combination

Professional template:

```python id="9xq2vq"
fig, ax = plt.subplots(
    figsize=(10,6),
    dpi=300
)
```

এটা:

* ML paper
* Research report
* Documentation

এর জন্য ভালো।

---

# 7. Save Figure

Graph save করতে:

```python id="m1xv6g"
plt.savefig(
    "graph.png"
)
```

Example:

```python id="2x7m6v"
fig, ax = plt.subplots()


ax.plot(
    [1,2,3],
    [10,20,30]
)


plt.savefig(
    "sales.png"
)
```

---

# 8. High Quality Save

Important parameters:

```python id="h8z1dc"
plt.savefig(
    "graph.png",
    dpi=300,
    bbox_inches="tight"
)
```

## dpi

Resolution

## bbox_inches="tight"

Extra white space remove করে।

---

# 9. Different File Formats

Matplotlib support করে:

## PNG

```python id="l5h2tq"
plt.savefig(
"chart.png"
)
```

Use:

* Web
* Presentation

---

## PDF

```python id="5r8n5j"
plt.savefig(
"chart.pdf"
)
```

Use:

* Research paper
* Report

---

## SVG

```python id="3n1l2w"
plt.savefig(
"chart.svg"
)
```

Use:

* Vector graphics
* Editing

---

# 10. Transparent Background

Example:

```python id="h1k5pv"
plt.savefig(
"chart.png",
transparent=True
)
```

Useful:

* Website
* Slides

---

# 11. Multiple Export

একই graph:

```python id="3h9m0d"
plt.savefig(
"result.png",
dpi=300
)


plt.savefig(
"result.pdf"
)
```

---

# 12. Tight Layout

Problem:

```text
Title cut off

Labels overlap
```

Solution:

```python id="8x7m3k"
plt.tight_layout()
```

Example:

```python id="v0n7xk"
fig, ax = plt.subplots(
figsize=(10,6)
)


ax.plot(
[1,2,3],
[10,20,30]
)


plt.tight_layout()


plt.show()
```

---

# 13. Constrained Layout

আরেকটি modern approach:

```python id="9xq8bw"
fig, ax = plt.subplots(
constrained_layout=True
)
```

---

# 14. ML Research Example

ধরি CNN training result:

```python id="v9m2k8"
epochs=[
1,2,3,4,5
]


accuracy=[
60,
70,
80,
90,
95
]
```

Publication quality:

```python id="5q8p3n"
import matplotlib.pyplot as plt


fig, ax = plt.subplots(
    figsize=(7,5),
    dpi=300
)


ax.plot(
    epochs,
    accuracy,
    marker="o"
)


ax.set_title(
    "CNN Training Accuracy"
)


ax.set_xlabel(
    "Epoch"
)


ax.set_ylabel(
    "Accuracy (%)"
)


ax.grid()


plt.tight_layout()


plt.savefig(
    "cnn_accuracy.pdf",
    bbox_inches="tight"
)


plt.show()
```

---

# 15. Image Dimension Calculation

Formula:

```
Pixels = Figure Size × DPI
```

Example:

```text
figsize=(10,5)

dpi=300
```

Result:

```
width:
10 × 300 = 3000 pixels


height:
5 × 300 = 1500 pixels
```

Final image:

```
3000 × 1500 px
```

---

# 16. Professional Visualization Checklist

Graph export করার আগে:

✅ Proper figure size

✅ DPI >= 300

✅ Clear labels

✅ Readable font

✅ No overlapping

✅ Tight layout

✅ Correct file format

---

# 17. Real Data Engineering Usage

Production report:

```text
SQL Database

↓

Pandas Analysis

↓

Matplotlib Visualization

↓

PDF Report

↓

Business Decision
```

---

# Lesson 14 Practice Task

## Task 1

একটি graph তৈরি করো:

Requirements:

```python
figsize=(10,6)

dpi=300
```

Data:

```python
x=[1,2,3,4,5]

y=[20,40,60,80,100]
```

Save:

* PNG
* PDF

---

## Task 2 (ML)

Fake model:

```python
epochs=[1,2,3,4,5]

accuracy=[60,70,80,88,95]
```

Create:

* Publication quality accuracy curve
* dpi=300
* Save as PDF

---

## Task 3

একটি 2×2 ML dashboard তৈরি করো:

* Loss curve
* Accuracy curve
* Confusion matrix
* Prediction distribution

Export:

```text
model_report.png
```

---

পরের Lesson:

# Lesson 15: Colors, Colormaps & Professional Styling

শিখবো:

* Color theory
* Built-in colormap
* Continuous vs categorical colors
* Heatmap coloring
* ML visualization styling

এটা graph-কে professional এবং readable করে তুলবে।
# Matplotlib Mastery Course

# Lesson 15: Colors, Colormaps & Professional Styling

আজ আমরা শিখবো কীভাবে Matplotlib graph-কে **professional, readable এবং research-quality** করা যায়।

একটি ভালো visualization শুধু সুন্দর না, বরং:

* সহজে বোঝা যায়
* গুরুত্বপূর্ণ pattern highlight করে
* ভুল interpretation কমায়

আজকের বিষয়:

* Basic colors
* Custom colors
* Color map (cmap)
* Continuous vs categorical colors
* Heatmap coloring
* ML visualization styling

---

# 1. Matplotlib Color System

Matplotlib বিভিন্নভাবে color নেয়:

## Color name

```python
color="red"
```

Example:

```python
import matplotlib.pyplot as plt


fig, ax = plt.subplots()


ax.plot(
    [1,2,3],
    [10,20,30],
    color="red"
)


plt.show()
```

---

# 2. Common Color Names

```text
red
blue
green
orange
purple
black
gray
yellow
pink
brown
```

Example:

```python
ax.bar(
    ["A","B","C"],
    [10,20,30],
    color="green"
)
```

---

# 3. Hex Color ব্যবহার

Professional design-এ hex বেশি ব্যবহার হয়।

Format:

```text
#RRGGBB
```

Example:

```python
ax.plot(
    x,
    y,
    color="#1f77b4"
)
```

Hex সুবিধা:

* Exact color control
* Brand color maintain করা যায়

---

# 4. RGB Color

RGB tuple:

```python
color=(red,green,blue)
```

Range:

```text
0 → 1
```

Example:

```python
ax.plot(
    x,
    y,
    color=(0.2,0.5,0.8)
)
```

---

# 5. Line Style + Color

একসাথে:

```python
ax.plot(
    x,
    y,
    color="blue",
    linestyle="--",
    marker="o"
)
```

Result:

```text
--o--o--o--
```

---

# 6. Multiple Lines Styling

Example:

```python
import matplotlib.pyplot as plt


epochs=[
1,2,3,4,5
]


loss=[
0.9,
0.6,
0.4,
0.2,
0.1
]


accuracy=[
50,
65,
75,
85,
95
]


fig, ax = plt.subplots()


ax.plot(
    epochs,
    loss,
    label="Loss",
    color="red"
)


ax.plot(
    epochs,
    accuracy,
    label="Accuracy",
    color="blue"
)


ax.legend()


plt.show()
```

---

# 7. Colormap কী?

Colormap হলো অনেকগুলো color-এর একটি sequence।

ব্যবহার:

* Heatmap
* Image visualization
* Scatter plot
* Matrix data

Example:

```python
cmap="viridis"
```

---

# 8. Built-in Colormap

Matplotlib-এর জনপ্রিয় cmap:

## Sequential

যখন value কম থেকে বেশি:

```text
light → dark
```

Examples:

```python
viridis

plasma

inferno

magma
```

---

## Diverging

দুই direction:

```text
negative ← center → positive
```

Examples:

```python
coolwarm

seismic
```

---

## Categorical

Different category:

```python
tab10

Set1

Accent
```

---

# 9. Scatter Plot with Colormap

Example:

```python
import numpy as np
import matplotlib.pyplot as plt


x=np.random.rand(100)

y=np.random.rand(100)

values=np.random.rand(100)


fig, ax = plt.subplots()


scatter=ax.scatter(
    x,
    y,
    c=values,
    cmap="viridis"
)


plt.colorbar(
    scatter
)


plt.show()
```

এখানে:

```text
value অনুযায়ী color change হবে
```

---

# 10. Heatmap Coloring

Matrix:

```python
matrix=np.random.rand(
10,
10
)
```

Visualization:

```python
fig, ax = plt.subplots()


image=ax.imshow(
    matrix,
    cmap="hot"
)


plt.colorbar(
    image
)


plt.show()
```

---

# 11. Image Visualization

Deep Learning-এ:

Image:

```python
image.shape

(64,64,3)
```

Show:

```python
plt.imshow(
    image
)

plt.axis(
"off"
)

plt.show()
```

---

# 12. Different Image Colormap

Grayscale:

```python
plt.imshow(
    image,
    cmap="gray"
)
```

Heat style:

```python
plt.imshow(
    image,
    cmap="hot"
)
```

---

# 13. Bar Chart Styling

Example:

```python
products=[
"Laptop",
"Mobile",
"Tablet"
]


sales=[
100,
200,
150
]


fig, ax = plt.subplots()


ax.bar(
    products,
    sales,
    color=[
        "blue",
        "green",
        "orange"
    ]
)


plt.show()
```

---

# 14. ML Confusion Matrix Coloring

Machine Learning-এ খুব common:

Example matrix:

```python
cm=[
[90,10],
[5,95]
]
```

Visualization:

```python
fig, ax = plt.subplots()


image=ax.imshow(
    cm,
    cmap="Blues"
)


plt.colorbar(
    image
)


plt.show()
```

---

# 15. Training Curve Professional Style

Example:

```python
epochs=[
1,2,3,4,5
]


loss=[
0.8,
0.6,
0.4,
0.2,
0.1
]


fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=300
)


ax.plot(
    epochs,
    loss,
    color="#d62728",
    marker="o",
    linewidth=2,
    label="Training Loss"
)


ax.set_title(
    "Model Training Loss"
)


ax.set_xlabel(
    "Epoch"
)


ax.set_ylabel(
    "Loss"
)


ax.legend()


ax.grid()


plt.show()
```

---

# 16. Style Sheet

Matplotlib built-in styles:

দেখতে:

```python
plt.style.available
```

Example:

```python
plt.style.use(
"ggplot"
)
```

তারপর:

```python
plt.plot(
x,
y
)

plt.show()
```

---

# 17. Professional Font Size Control

```python
fig, ax = plt.subplots()


ax.set_title(
    "Sales Analysis",
    fontsize=16
)


ax.set_xlabel(
    "Month",
    fontsize=12
)


ax.set_ylabel(
    "Sales",
    fontsize=12
)
```

---

# 18. UCF Crime AI Project Example

তোমার CCTV detection project:

Prediction confidence:

```python
confidence=[
0.2,
0.4,
0.6,
0.8,
0.95
]
```

Visualization:

```python
fig, ax = plt.subplots()


ax.plot(
confidence,
marker="o",
color="red"
)


ax.set_title(
"Suspicious Activity Confidence"
)


ax.grid()


plt.show()
```

---

# 19. Color Selection Rule

## Continuous data:

Use:

```text
viridis
plasma
coolwarm
```

Example:

* Temperature
* Confidence score
* Probability

---

## Categories:

Use:

```text
tab10
Set1
```

Example:

* Class labels
* Product categories

---

# 20. Visualization Mistakes

Avoid:

❌ Too many colors

❌ Dark background with unreadable text

❌ Random colors

❌ Missing legend

❌ Low contrast

---

# Lesson 15 Practice Task

## Task 1

Create scatter plot:

Data:

```python
x=np.random.rand(100)

y=np.random.rand(100)

value=np.random.rand(100)
```

Requirements:

* cmap="viridis"
* colorbar
* title

---

## Task 2

Create heatmap:

```python
matrix=np.random.rand(20,20)
```

Requirements:

* imshow()
* cmap="hot"
* colorbar

---

## Task 3 (Deep Learning)

Create CNN training graph:

```python
epochs=[
1,2,3,4,5
]


accuracy=[
60,70,80,90,95
]
```

Requirements:

* dpi=300
* custom hex color
* marker
* legend
* grid

---

পরের Lesson:

# Lesson 16: Advanced Statistical Visualization

শিখবো:

* Error bars
* Confidence interval
* Mean ± Standard deviation
* Scientific plotting
* ML experiment result visualization

এটা research paper এবং model comparison-এর জন্য খুব গুরুত্বপূর্ণ।
# Matplotlib Mastery Course

# Lesson 16: Advanced Statistical Visualization

## Error Bars, Confidence Interval & ML Experiment Visualization

আজ আমরা Matplotlib-এর একটি খুব গুরুত্বপূর্ণ অংশ শিখবো।

Machine Learning / Data Science-এ শুধু value দেখানো যথেষ্ট নয়। আমাদের জানতে হয়:

* Prediction কতটা reliable?
* Result-এর uncertainty কত?
* Model কতবার experiment করলে variation কেমন?

এগুলোর জন্য ব্যবহার হয়:

* Error Bar
* Standard Deviation
* Confidence Interval
* Mean ± Variance Visualization

---

# 1. কেন Statistical Visualization দরকার?

ধরি তুমি একটি model 5 বার train করেছো:

```
Experiment 1 → Accuracy 92%

Experiment 2 → Accuracy 90%

Experiment 3 → Accuracy 94%

Experiment 4 → Accuracy 91%

Experiment 5 → Accuracy 93%
```

Average:

```
92%
```

কিন্তু শুধু 92% বললে পুরো picture পাওয়া যায় না।

Variation:

```
±2%
```

তখন বোঝা যায় model কত stable।

---

# 2. Error Bar কী?

Error bar একটি point-এর uncertainty দেখায়।

Normal plot:

```
      *
      |
      |
```

Error bar:

```
      |
      *
      |
      |
```

এখানে:

```
Point = Mean value

Line = Error range
```

---

# 3. Basic Error Bar

Function:

```python
ax.errorbar()
```

Example:

```python
import matplotlib.pyplot as plt


x=[
1,2,3,4,5
]


y=[
10,
20,
30,
40,
50
]


error=[
2,
3,
1,
4,
2
]


fig, ax = plt.subplots()


ax.errorbar(
    x,
    y,
    yerr=error,
    marker="o"
)


plt.show()
```

---

# 4. yerr কী?

```python
yerr
```

মানে:

Vertical error

Example:

```
Value = 50

Error = 5


Range:

45 ---- 50 ---- 55
```

---

# 5. Horizontal Error

x-axis error:

```python
ax.errorbar(
    x,
    y,
    xerr=error
)
```

Example:

```
<----*---->
```

---

# 6. Error Bar Styling

Example:

```python
fig, ax = plt.subplots()


ax.errorbar(
    x,
    y,
    yerr=error,
    fmt="o",
    capsize=5
)


plt.show()
```

---

# 7. capsize কী?

Error bar-এর শেষের ছোট line:

Without:

```
 |
 *
 |
```

With cap:

```
 ─
 |
 *
 |
 ─
```

Example:

```python
capsize=5
```

---

# 8. Mean এবং Standard Deviation

Statistics:

Mean:

```python
np.mean()
```

Standard deviation:

```python
np.std()
```

Example:

```python
import numpy as np


data=[
90,
92,
94,
91,
93
]


mean=np.mean(data)

std=np.std(data)


print(mean)

print(std)
```

---

# 9. ML Model Accuracy Visualization

ধরি:

CNN:

```
90
92
91
94
```

Calculate:

```python
cnn_scores=[
90,
92,
91,
94
]


mean=np.mean(
cnn_scores
)


std=np.std(
cnn_scores
)
```

---

Plot:

```python
import matplotlib.pyplot as plt


fig, ax = plt.subplots()


ax.errorbar(
    ["CNN"],
    [mean],
    yerr=[std],
    fmt="o",
    capsize=5
)


ax.set_ylabel(
    "Accuracy"
)


plt.show()
```

---

# 10. Multiple Model Comparison

ধরি:

```
CNN

CNN-LSTM

3D CNN
```

Scores:

```python
cnn=[
90,
92,
91
]


cnn_lstm=[
94,
95,
93
]


cnn3d=[
96,
95,
97
]
```

Mean:

```python
models=[
cnn,
cnn_lstm,
cnn3d
]


means=[]

stds=[]


for model in models:

    means.append(
        np.mean(model)
    )

    stds.append(
        np.std(model)
    )
```

---

Visualization:

```python
fig, ax = plt.subplots()


ax.errorbar(
    [
    "CNN",
    "CNN-LSTM",
    "3D CNN"
    ],
    means,
    yerr=stds,
    fmt="o",
    capsize=5
)


ax.set_ylabel(
"Accuracy (%)"
)


plt.show()
```

---

# 11. Confidence Interval কী?

Confidence Interval বলে:

"আমাদের estimated value কত range-এর মধ্যে হতে পারে"

Example:

```
Accuracy:

92%

95% Confidence Interval:

90% - 94%
```

---

# 12. Shaded Confidence Region

Line + confidence area:

Function:

```python
ax.fill_between()
```

Example:

```python
import numpy as np
import matplotlib.pyplot as plt


epochs=np.arange(
1,
11
)


accuracy=np.array(
[
60,
65,
70,
75,
80,
85,
88,
90,
92,
94
]
)


std=3


upper=accuracy+std

lower=accuracy-std


fig, ax = plt.subplots()


ax.plot(
epochs,
accuracy
)


ax.fill_between(
    epochs,
    lower,
    upper,
    alpha=0.3
)


plt.show()
```

---

# 13. ML Training Visualization

Deep Learning model training:

```
Epoch

Accuracy

Loss

Validation Accuracy

Validation Loss
```

Professional graph:

```python
fig, axes = plt.subplots(
1,
2
)
```

Left:

```
Loss curve
```

Right:

```
Accuracy curve
```

---

# 14. Bar Chart with Error

Example:

Department performance:

```python
departments=[
"A",
"B",
"C"
]


scores=[
80,
85,
90
]


errors=[
3,
2,
4
]
```

Plot:

```python
fig, ax = plt.subplots()


ax.bar(
    departments,
    scores
)


ax.errorbar(
    departments,
    scores,
    yerr=errors,
    fmt="none",
    capsize=5
)


plt.show()
```

---

# 15. Real AI CCTV Project Example

তোমার UCF Crime project:

Models:

```
CNN

CNN-LSTM

MobileNet-LSTM

3D CNN
```

Experiment:

Run:

```
5 times
```

Collect:

```
Accuracy scores
F1 scores
Precision
Recall
```

Visualization:

```
Model Accuracy ± Std
```

এটা research paper-এর standard visualization।

---

# 16. Complete Research Style Example

```python
import numpy as np
import matplotlib.pyplot as plt


models=[
"CNN",
"CNN-LSTM",
"3D CNN"
]


results=[
[90,91,92],
[94,95,93],
[96,97,95]
]


means=[]

stds=[]


for r in results:

    means.append(
        np.mean(r)
    )

    stds.append(
        np.std(r)
    )


fig, ax = plt.subplots(
    figsize=(8,5),
    dpi=300
)


ax.errorbar(
    models,
    means,
    yerr=stds,
    fmt="o",
    capsize=5
)


ax.set_title(
"Model Accuracy Comparison"
)


ax.set_ylabel(
"Accuracy (%)"
)


ax.grid()


plt.show()
```

---

# 17. Statistical Visualization Rules

✅ Always show uncertainty

✅ Use mean ± std for experiments

✅ Use error bars for comparison

✅ Avoid misleading graphs

✅ Mention sample size

---

# Lesson 16 Practice Task

## Task 1

Create error bar plot:

Data:

```python
models=[
"Model A",
"Model B",
"Model C"
]


accuracy=[
90,
95,
97
]


error=[
2,
1,
1.5
]
```

Requirements:

* errorbar()
* capsize
* labels

---

## Task 2 (Deep Learning)

Training:

```python
epochs=[
1,2,3,4,5
]


accuracy=[
60,70,80,88,92
]
```

Create:

* Accuracy curve
* Confidence region (±3)

---

## Task 3 (Research)

Compare:

```
CNN
CNN-LSTM
3D CNN
```

Each model:

5 experiment result

Create:

```
Accuracy Mean ± Standard Deviation
```

---

পরের Lesson:

# Lesson 17: Matplotlib Animation & Real-Time Visualization

শিখবো:

* Live plotting
* Camera frame visualization
* Streaming data
* AI CCTV real-time monitoring graph
* FuncAnimation

এটা তোমার AI surveillance project-এর সাথে directly related।
# Matplotlib Mastery Course

# Lesson 17: Matplotlib Animation & Real-Time Visualization

আজ আমরা শিখবো **Matplotlib Animation**।

এটি ব্যবহার করা হয় যখন data সময়ের সাথে পরিবর্তন হয়।

Real-world examples:

* Live sensor monitoring
* Stock price movement
* Training loss update
* CCTV frame visualization
* Real-time AI prediction
* IoT dashboard

---

# 1. Static vs Dynamic Visualization

## Static Plot

একবার তৈরি হয়:

```text
Data → Graph
```

Example:

```python
plt.plot(x,y)
```

---

## Dynamic Plot

সময় অনুযায়ী update হয়:

```text
Data
 |
 ↓
New Data
 |
 ↓
Update Graph
```

---

# 2. Matplotlib Animation Module

আমরা ব্যবহার করবো:

```python
matplotlib.animation
```

Import:

```python
from matplotlib.animation import FuncAnimation
```

---

# 3. Basic Animation Structure

Template:

```python
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


fig, ax = plt.subplots()


def update(frame):

    pass


animation = FuncAnimation(
    fig,
    update
)


plt.show()
```

---

# 4. Simple Moving Line Animation

Example:

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


fig, ax = plt.subplots()


x = []
y = []


line, = ax.plot(
    [],
    []
)


def update(frame):

    x.append(frame)

    y.append(
        np.sin(frame)
    )

    line.set_data(
        x,
        y
    )

    ax.relim()

    ax.autoscale_view()

    return line,


ani = FuncAnimation(
    fig,
    update,
    frames=100,
    interval=100
)


plt.show()
```

---

# 5. update() Function

Animation-এর মূল অংশ:

```python
def update(frame):
```

প্রতিবার নতুন frame আসলে এই function run হয়।

Example:

```text
Frame 1

update(1)


Frame 2

update(2)


Frame 3

update(3)
```

---

# 6. frames Parameter

কতগুলো update হবে:

```python
frames=100
```

মানে:

```text
0 → 99
```

---

# 7. interval Parameter

Animation speed:

```python
interval=100
```

Unit:

```text
milliseconds
```

Example:

Fast:

```python
interval=20
```

Slow:

```python
interval=1000
```

---

# 8. Real-Time Data Simulation

ধরি sensor data আসছে:

```python
import random


value=random.random()
```

প্রতি মুহূর্তে নতুন value:

```python
def update(frame):

    value=random.random()

```

---

# 9. Real-Time Sensor Dashboard

Example:

```python
import random
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


fig, ax = plt.subplots()


x=[]
y=[]


line, = ax.plot(
    [],
    []
)


def update(frame):

    x.append(frame)

    y.append(
        random.randint(
            0,
            100
        )
    )


    line.set_data(
        x,
        y
    )


    ax.relim()

    ax.autoscale_view()


    return line,


ani=FuncAnimation(
    fig,
    update,
    frames=100,
    interval=200
)


plt.show()
```

---

# 10. Animation Save করা

GIF:

```python
ani.save(
"animation.gif"
)
```

---

MP4:

```python
ani.save(
"animation.mp4",
writer="ffmpeg"
)
```

---

# 11. Scatter Animation

Moving points:

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


fig, ax = plt.subplots()


scatter=ax.scatter(
    [],
    []
)


def update(frame):

    x=np.random.rand(10)

    y=np.random.rand(10)


    scatter.set_offsets(
        np.c_[x,y]
    )


    return scatter,


ani=FuncAnimation(
    fig,
    update,
    frames=100
)


plt.show()
```

---

# 12. Training Progress Visualization

Deep Learning training:

Normally:

```text
Epoch 1
Loss = 0.8


Epoch 2
Loss = 0.6


Epoch 3
Loss = 0.4
```

Live graph:

```text
Loss

|
| *
|   *
|      *
--------------
Epoch
```

---

Example:

```python
epochs=[]

loss=[]


def update(epoch):

    epochs.append(epoch)

    loss.append(
        np.random.random()
    )


    line.set_data(
        epochs,
        loss
    )
```

---

# 13. AI CCTV Real-Time Example

তোমার AI surveillance project-এর সাথে:

Pipeline:

```text
Camera Stream

      ↓

Frame Capture

      ↓

CNN-LSTM Model

      ↓

Prediction Score

      ↓

Matplotlib Dashboard
```

Live graph:

```
Time

|
|        *
|     *
|  *
| *
--------------
Confidence
```

---

# 14. Frame Visualization Animation

Image sequence:

```python
frames=[
image1,
image2,
image3
]
```

Update:

```python
def update(frame):

    img.set_array(
        frames[frame]
    )

    return img,
```

---

# 15. Live Model Confidence Monitoring

Example:

```python
confidence=[]


def update(frame):

    score=model.predict(
        frame
    )

    confidence.append(
        score
    )

    line.set_data(
        range(len(confidence)),
        confidence
    )
```

---

# 16. Animation with Multiple Charts

Example:

AI Monitoring Dashboard:

```
+----------------+
| Confidence     |
+----------------+

+----------------+
| FPS            |
+----------------+

+----------------+
| Alert Count    |
+----------------+
```

Implementation:

```python
fig, axes = plt.subplots(
3,
1
)
```

---

# 17. Important Animation Concepts

## Artist

যে object update হয়:

Example:

```python
line
scatter
image
```

---

## Blitting

Performance optimization:

```python
blit=True
```

Example:

```python
ani=FuncAnimation(
    fig,
    update,
    blit=True
)
```

এতে শুধু পরিবর্তিত অংশ redraw হয়।

---

# 18. Matplotlib Animation Limitations

Matplotlib ভালো:

✅ Small real-time visualization

✅ Research demo

✅ Training monitoring

কিন্তু:

Large production dashboard-এর জন্য:

* Plotly Dash
* Streamlit
* Grafana
* React Charts

বেশি ব্যবহার হয়।

---

# 19. ML Engineer Workflow

Training:

```text
Model Training

↓

Callback

↓

Save Metrics

↓

Matplotlib Animation

↓

Monitor Learning
```

---

# Lesson 17 Practice Task

## Task 1

Create moving sine wave:

Requirements:

* FuncAnimation
* update()
* 100 frames

---

## Task 2

Create live sensor dashboard:

Generate:

```python
random temperature
```

Show:

* Time
* Temperature curve

---

## Task 3 (AI CCTV)

Fake confidence:

```python
confidence=[
0.1,
0.2,
0.4,
0.7,
0.9
]
```

Create:

Real-time confidence monitoring graph.

---

পরের Lesson:

# Lesson 18: Matplotlib + Machine Learning Visualization

শিখবো:

* Confusion Matrix
* ROC Curve
* Precision-Recall Curve
* Feature Importance
* Model Evaluation Dashboard

এটা ML Engineer হওয়ার জন্য খুব গুরুত্বপূর্ণ অংশ।
# Matplotlib Mastery Course

# Lesson 18: Matplotlib + Machine Learning Visualization

আজ থেকে আমরা Matplotlib-এর সবচেয়ে গুরুত্বপূর্ণ practical অংশে যাচ্ছি।

Machine Learning model শুধু train করলেই হবে না, model **কেমন perform করছে সেটা visualize করতে হবে**।

আজ শিখবো:

* Confusion Matrix
* Accuracy Visualization
* ROC Curve
* Precision-Recall Curve
* Feature Importance
* Model Evaluation Dashboard

---

# 1. ML Visualization কেন দরকার?

ধরি model result:

```text id="q6m1su"
Accuracy = 95%
```

শুধু accuracy জানলে সব বোঝা যায় না।

আমাদের জানতে হবে:

```text id="r5k0kf"
কোন class ভুল করছে?

False Positive কত?

False Negative কত?

Threshold পরিবর্তনে কী হয়?
```

Visualization এগুলো বুঝতে সাহায্য করে।

---

# Part 1: Confusion Matrix

# 2. Confusion Matrix কী?

Binary Classification:

Example:

AI CCTV:

```text
0 = Normal

1 = Suspicious
```

Confusion Matrix:

```
                Predicted

              0        1

Actual 0     TN       FP


Actual 1     FN       TP
```

Meaning:

## True Negative (TN)

Normal → Normal

## False Positive (FP)

Normal → Suspicious

## False Negative (FN)

Suspicious → Normal

## True Positive (TP)

Suspicious → Suspicious

---

# 3. Confusion Matrix তৈরি

Example:

```python id="1m4x8h"
from sklearn.metrics import confusion_matrix


y_true=[
0,0,0,1,1,1
]


y_pred=[
0,0,1,1,1,0
]


cm = confusion_matrix(
    y_true,
    y_pred
)


print(cm)
```

Output:

```
[[2 1]

 [1 2]]
```

---

# 4. Matplotlib দিয়ে Confusion Matrix

```python id="e0f7gh"
import matplotlib.pyplot as plt


fig, ax = plt.subplots()


image=ax.imshow(
    cm,
    cmap="Blues"
)


plt.colorbar(
    image
)


ax.set_xlabel(
"Predicted"
)


ax.set_ylabel(
"Actual"
)


plt.show()
```

---

# 5. Confusion Matrix Value দেখানো

Professional way:

```python id="9hj8qw"
for i in range(2):

    for j in range(2):

        ax.text(
            j,
            i,
            cm[i,j],
            ha="center",
            va="center"
        )
```

---

# 6. Complete Confusion Matrix Function

```python id="6j34nn"
def plot_confusion_matrix(cm):

    fig, ax = plt.subplots()


    image=ax.imshow(
        cm,
        cmap="Blues"
    )


    plt.colorbar(
        image
    )


    for i in range(cm.shape[0]):

        for j in range(cm.shape[1]):

            ax.text(
                j,
                i,
                cm[i,j],
                ha="center",
                va="center"
            )


    plt.show()
```

---

# Part 2: ROC Curve

# 7. ROC Curve কী?

ROC:

```text
Receiver Operating Characteristic
```

এটি দেখায়:

Threshold পরিবর্তন করলে model কেমন behave করে।

Axes:

```text
Y-axis:

True Positive Rate


X-axis:

False Positive Rate
```

---

# 8. ROC Curve তৈরি

Example:

```python id="4xj5bc"
from sklearn.metrics import roc_curve


y_true=[
0,0,1,1
]


y_score=[
0.1,
0.4,
0.8,
0.9
]


fpr, tpr, threshold = roc_curve(
    y_true,
    y_score
)
```

---

Plot:

```python id="k3a8ty"
fig, ax = plt.subplots()


ax.plot(
    fpr,
    tpr
)


ax.set_xlabel(
"False Positive Rate"
)


ax.set_ylabel(
"True Positive Rate"
)


ax.set_title(
"ROC Curve"
)


plt.show()
```

---

# 9. AUC Score

AUC:

```text
Area Under Curve
```

Range:

```text
0.5 = Random

1.0 = Perfect
```

Calculate:

```python id="4p8f6n"
from sklearn.metrics import roc_auc_score


auc = roc_auc_score(
    y_true,
    y_score
)


print(auc)
```

---

# Part 3: Precision Recall Curve

# 10. কেন Precision Recall?

Imbalanced dataset-এর জন্য গুরুত্বপূর্ণ।

Example:

UCF Crime:

```text
Normal:

30000


Suspicious:

10000
```

---

# 11. Create Curve

```python id="4s4y2u"
from sklearn.metrics import precision_recall_curve


precision, recall, threshold = precision_recall_curve(
    y_true,
    y_score
)
```

Plot:

```python id="j3l1hk"
fig, ax = plt.subplots()


ax.plot(
    recall,
    precision
)


ax.set_xlabel(
"Recall"
)


ax.set_ylabel(
"Precision"
)


ax.set_title(
"Precision Recall Curve"
)


plt.show()
```

---

# Part 4: Feature Importance

# 12. Feature Importance কী?

Model কোন feature বেশি important মনে করছে।

Example:

House price:

```
Feature

Area       80%

Room       50%

Age        20%
```

---

# 13. Bar Chart Feature Importance

```python id="m4w3yq"
features=[
"Area",
"Room",
"Age"
]


importance=[
0.8,
0.5,
0.2
]


fig, ax = plt.subplots()


ax.bar(
features,
importance
)


ax.set_title(
"Feature Importance"
)


plt.show()
```

---

# 14. ML Model Evaluation Dashboard

একজন ML Engineer সাধারণত একসাথে দেখে:

```
+----------------+
| Confusion Mat  |
+----------------+

+----------------+
| ROC Curve      |
+----------------+

+----------------+
| Loss Accuracy  |
+----------------+
```

---

# 15. Complete ML Dashboard Example

```python id="7y2h9q"
import matplotlib.pyplot as plt


fig, axes = plt.subplots(
2,
2,
figsize=(10,8)
)


# Confusion Matrix

axes[0,0].imshow(
cm,
cmap="Blues"
)

axes[0,0].set_title(
"Confusion Matrix"
)



# ROC

axes[0,1].plot(
fpr,
tpr
)

axes[0,1].set_title(
"ROC Curve"
)



# Feature Importance

axes[1,0].bar(
features,
importance
)

axes[1,0].set_title(
"Feature Importance"
)



# Accuracy

axes[1,1].plot(
epochs,
accuracy
)

axes[1,1].set_title(
"Training Accuracy"
)



plt.tight_layout()

plt.show()
```

---

# 16. UCF Crime AI Project Connection

তোমার AI CCTV model:

Model:

```
CNN-LSTM
```

Evaluation:

## Confusion Matrix

দেখাবে:

```
Normal ভুল করে Suspicious বলছে কিনা
```

## ROC

Threshold নির্বাচন:

```
0.5?
0.7?
0.85?
```

## Precision Recall

Suspicious detection কত reliable।

## Confidence Distribution

Model confidence pattern।

---

# 17. Research Paper Visualization

একটি ML paper-এ সাধারণত থাকে:

```
Figure 1:

Training Loss


Figure 2:

Accuracy Curve


Figure 3:

Confusion Matrix


Figure 4:

ROC Curve


Figure 5:

Model Comparison
```

---

# Lesson 18 Practice Task

## Task 1

Create confusion matrix:

```python
cm=[
[90,10],
[5,95]
]
```

Requirements:

* imshow()
* colorbar
* values show

---

## Task 2

Create ROC curve:

```python
fpr=[
0,0.1,0.2,0.5,1
]

tpr=[
0,0.6,0.8,0.9,1
]
```

---

## Task 3 (AI Project)

Compare:

```
CNN

CNN-LSTM

3D CNN
```

Metrics:

```
Accuracy

Precision

Recall

F1-score
```

Create:

ML evaluation dashboard

---

পরের Lesson:

# Lesson 19: Matplotlib + Deep Learning Visualization

শিখবো:

* CNN feature map visualization
* Activation visualization
* Training history plotting
* Grad-CAM visualization
* Model prediction visualization

এটা তোমার AI CCTV / Computer Vision project-এর জন্য সবচেয়ে গুরুত্বপূর্ণ অংশ।
# Matplotlib Mastery Course

# Lesson 19: Matplotlib + Deep Learning Visualization

আজ আমরা Deep Learning model-এর ভিতরের behavior visualize করা শিখবো।

বিশেষ করে Computer Vision project-এর জন্য এটি খুব গুরুত্বপূর্ণ।

আজকের বিষয়:

* Training history visualization
* Loss & Accuracy curve
* CNN Feature Map visualization
* Activation visualization
* Prediction visualization
* Grad-CAM concept

তোমার AI CCTV / UCF Crime project-এর সাথে সরাসরি সম্পর্কিত।

---

# 1. Deep Learning Visualization কেন দরকার?

ধরি model:

```text id="4j0xw5"
Input Image

      ↓

CNN Layers

      ↓

Feature Extraction

      ↓

Classifier

      ↓

Prediction
```

আমরা জানতে চাই:

```
Model কী শিখছে?

কোন জায়গায় focus করছে?

Training ভালো হচ্ছে কিনা?

Prediction কেন দিল?
```

---

# Part 1: Training History Visualization

# 2. Model Training History

TensorFlow/Keras:

```python
history = model.fit(
    train_data,
    epochs=20
)
```

History object:

```python
history.history
```

Output:

```python
{
"loss":[...],

"accuracy":[...],

"val_loss":[...],

"val_accuracy":[...]
}
```

---

# 3. Training Loss Curve

Example:

```python
import matplotlib.pyplot as plt


loss = [
0.9,
0.7,
0.5,
0.3,
0.2
]


epochs=[
1,2,3,4,5
]


fig, ax = plt.subplots()


ax.plot(
    epochs,
    loss,
    marker="o"
)


ax.set_title(
"Training Loss"
)


ax.set_xlabel(
"Epoch"
)


ax.set_ylabel(
"Loss"
)


ax.grid()


plt.show()
```

---

# 4. Accuracy Curve

```python
accuracy=[
50,
65,
75,
85,
92
]


fig, ax = plt.subplots()


ax.plot(
epochs,
accuracy,
marker="o"
)


ax.set_title(
"Training Accuracy"
)


ax.set_ylabel(
"Accuracy (%)"
)


plt.show()
```

---

# 5. Complete Training Visualization Function

Reusable function:

```python
def plot_history(history):

    fig, axes = plt.subplots(
        1,
        2,
        figsize=(12,4)
    )


    axes[0].plot(
        history["loss"]
    )

    axes[0].set_title(
        "Loss"
    )


    axes[1].plot(
        history["accuracy"]
    )

    axes[1].set_title(
        "Accuracy"
    )


    plt.show()
```

---

# Part 2: Validation Curve Analysis

# 6. Overfitting Detection

Training:

```
accuracy ↑
```

Validation:

```
accuracy ↓
```

মানে:

```
Model memorize করছে
```

---

Visualization:

```python
fig, ax = plt.subplots()


ax.plot(
train_accuracy,
label="Train"
)


ax.plot(
val_accuracy,
label="Validation"
)


ax.legend()


plt.show()
```

---

# Part 3: CNN Feature Map Visualization

# 7. Feature Map কী?

CNN image থেকে feature extract করে।

Example:

Input:

```
Cat image
```

CNN layer:

```
Edge detection

↓

Texture

↓

Shape

↓

Object
```

এই intermediate output হলো:

```
Feature Map
```

---

# 8. CNN Layer Output বের করা

Keras:

```python
from tensorflow.keras.models import Model


layer_output = Model(
    inputs=model.input,
    outputs=model.layers[0].output
)
```

---

# 9. Feature Map Show করা

Example:

```python
activation = layer_output.predict(
    image
)
```

Shape:

```
(1,64,64,32)
```

মানে:

```
32 feature maps
```

---

# 10. Feature Map Visualization

```python
fig, axes = plt.subplots(
4,
4,
figsize=(8,8)
)


for i, ax in enumerate(axes.flat):

    ax.imshow(
        activation[0,:,:,i],
        cmap="viridis"
    )

    ax.axis("off")


plt.show()
```

---

# Part 4: Image Prediction Visualization

# 11. Model Prediction

Example:

```python
prediction = model.predict(
image
)
```

Output:

```
0.92
```

Meaning:

```
92% suspicious probability
```

---

# 12. Prediction Display

```python
plt.imshow(
image
)


plt.title(
f"Confidence: {prediction[0]:.2f}"
)


plt.axis(
"off"
)


plt.show()
```

---

# Part 5: Grad-CAM Visualization

# 13. Grad-CAM কী?

Grad-CAM দেখায়:

```
Model image-এর কোন অংশে focus করেছে
```

Example:

Original:

```
Person walking
```

Grad-CAM:

```
🔥 Head area
🔥 Body area
```

---

# 14. Grad-CAM Pipeline

```text
Image

 ↓

CNN Layer

 ↓

Gradient Calculation

 ↓

Important Region

 ↓

Heatmap
```

---

# 15. Heatmap Overlay Concept

Original image:

```
RGB Image
```

Heatmap:

```
Red = Important
Blue = Less important
```

Combine:

```
Final Visualization
```

---

# 16. Matplotlib Heatmap Overlay

Example:

```python
plt.imshow(
image
)


plt.imshow(
heatmap,
alpha=0.4,
cmap="jet"
)


plt.axis(
"off"
)


plt.show()
```

---

# Part 6: AI CCTV Project Connection

তোমার UCF Crime Detection System:

Pipeline:

```
Video Frame

↓

CNN-LSTM

↓

Suspicious Probability

↓

Visualization
```

Visualization:

## 1. Confidence Curve

```
Time vs Probability
```

## 2. Frame Prediction

```
Frame

Label

Confidence
```

## 3. Grad-CAM

```
Person/Action region highlight
```

---

# 17. Complete Deep Learning Dashboard

Structure:

```
+-----------------------+
| Training Loss         |
+-----------------------+

+-----------------------+
| Accuracy Curve        |
+-----------------------+

+-----------------------+
| Prediction Image      |
+-----------------------+

+-----------------------+
| Grad-CAM Heatmap      |
+-----------------------+
```

---

# 18. Production Visualization Function

```python
def visualize_prediction(
    image,
    confidence
):

    fig, ax = plt.subplots()


    ax.imshow(
        image
    )


    ax.set_title(
        f"Confidence: {confidence:.2f}"
    )


    ax.axis(
        "off"
    )


    plt.show()
```

---

# Lesson 19 Practice Task

## Task 1

Fake training history তৈরি করো:

```python
epochs=10

loss decrease করবে

accuracy increase করবে
```

Plot:

* Loss curve
* Accuracy curve

---

## Task 2

একটি random feature map তৈরি করো:

```python
feature_map=np.random.rand(
64,
64
)
```

Show:

* imshow()
* cmap

---

## Task 3 (AI CCTV)

Fake prediction:

```python
confidence=[
0.2,
0.4,
0.6,
0.8,
0.95
]
```

Create:

* Confidence timeline graph
* Threshold line (0.85)

---

পরের Lesson:

# Lesson 20: Matplotlib Advanced Project — AI Model Evaluation Dashboard

শিখবো:

* Complete ML dashboard
* Multiple plots integration
* Model report generation
* Production-style visualization architecture

এটা Matplotlib-এর একটি বড় project হবে।
# Matplotlib Mastery Course

# Lesson 20: Matplotlib Advanced Project — AI Model Evaluation Dashboard

আজ আমরা Matplotlib দিয়ে একটি **complete ML Model Evaluation Dashboard** তৈরি করবো।

এটি একজন ML Engineer বাস্তবে ব্যবহার করে:

* Model training analysis
* Model comparison
* Error analysis
* Prediction monitoring
* Research report তৈরি করতে

আজকের project:

```text
AI Model Evaluation Dashboard

+-------------------+-------------------+
| Loss Curve        | Accuracy Curve    |
+-------------------+-------------------+
| Confusion Matrix  | ROC Curve         |
+-------------------+-------------------+
| Prediction Stats  | Confidence Plot   |
+-------------------+-------------------+
```

---

# 1. Project Structure

আমরা ধরে নিচ্ছি:

Model:

```text
CNN-LSTM
```

Dataset:

```text
UCF Crime Dataset
```

Metrics:

```text
Loss
Accuracy
Precision
Recall
F1-score
Confidence
```

---

# 2. Import Libraries

```python
import numpy as np
import matplotlib.pyplot as plt
```

---

# Part 1: Training History

# 3. Fake Training Data

```python
epochs = np.arange(1,11)


train_loss = [
0.9,
0.75,
0.6,
0.5,
0.4,
0.3,
0.25,
0.2,
0.15,
0.1
]


val_loss = [
0.95,
0.8,
0.65,
0.55,
0.5,
0.45,
0.42,
0.4,
0.38,
0.37
]
```

---

# 4. Accuracy Data

```python
train_accuracy=[
50,
60,
70,
78,
85,
88,
91,
94,
96,
98
]


val_accuracy=[
48,
58,
68,
75,
80,
83,
85,
86,
87,
88
]
```

---

# Part 2: Confusion Matrix

# 5. Create Matrix

```python
cm = np.array(
[
[900,100],
[50,950]
]
)
```

Meaning:

```text
Normal:

900 correct
100 wrong


Suspicious:

950 correct
50 wrong
```

---

# Part 3: ROC Data

```python
fpr=[
0,
0.1,
0.2,
0.4,
0.7,
1
]


tpr=[
0,
0.6,
0.75,
0.85,
0.95,
1
]
```

---

# Part 4: Prediction Confidence

```python
confidence=[
0.1,
0.25,
0.4,
0.65,
0.75,
0.92,
0.95
]


frames=np.arange(
len(confidence)
)
```

---

# 6. Create Dashboard Figure

আমরা ব্যবহার করবো:

```python
plt.subplots()
```

Structure:

```text
3 rows

2 columns
```

Code:

```python
fig, axes = plt.subplots(
    3,
    2,
    figsize=(14,12),
    dpi=300
)
```

---

# 7. Loss Curve

```python
axes[0,0].plot(
    epochs,
    train_loss,
    label="Train"
)


axes[0,0].plot(
    epochs,
    val_loss,
    label="Validation"
)


axes[0,0].set_title(
"Loss Curve"
)


axes[0,0].set_xlabel(
"Epoch"
)


axes[0,0].set_ylabel(
"Loss"
)


axes[0,0].legend()


axes[0,0].grid()
```

---

# 8. Accuracy Curve

```python
axes[0,1].plot(
    epochs,
    train_accuracy,
    label="Train"
)


axes[0,1].plot(
    epochs,
    val_accuracy,
    label="Validation"
)


axes[0,1].set_title(
"Accuracy Curve"
)


axes[0,1].set_xlabel(
"Epoch"
)


axes[0,1].set_ylabel(
"Accuracy (%)"
)


axes[0,1].legend()


axes[0,1].grid()
```

---

# 9. Confusion Matrix

```python
image = axes[1,0].imshow(
    cm,
    cmap="Blues"
)


axes[1,0].set_title(
"Confusion Matrix"
)


plt.colorbar(
image,
ax=axes[1,0]
)
```

Values show:

```python
for i in range(2):

    for j in range(2):

        axes[1,0].text(
            j,
            i,
            cm[i,j],
            ha="center",
            va="center"
        )
```

---

# 10. ROC Curve

```python
axes[1,1].plot(
    fpr,
    tpr
)


axes[1,1].plot(
    [0,1],
    [0,1],
    linestyle="--"
)


axes[1,1].set_title(
"ROC Curve"
)


axes[1,1].set_xlabel(
"False Positive Rate"
)


axes[1,1].set_ylabel(
"True Positive Rate"
)


axes[1,1].grid()
```

---

# 11. Confidence Timeline

```python
axes[2,0].plot(
    frames,
    confidence,
    marker="o"
)


axes[2,0].axhline(
    0.85,
    linestyle="--"
)


axes[2,0].set_title(
"Prediction Confidence"
)


axes[2,0].set_xlabel(
"Frame"
)


axes[2,0].set_ylabel(
"Confidence"
)


axes[2,0].grid()
```

---

# 12. Model Metrics

ধরি:

```python
metrics=[
0.92,
0.89,
0.90,
0.91
]


names=[
"Accuracy",
"Precision",
"Recall",
"F1"
]
```

Bar chart:

```python
axes[2,1].bar(
    names,
    metrics
)


axes[2,1].set_ylim(
0,
1
)


axes[2,1].set_title(
"Model Metrics"
)
```

---

# 13. Final Layout

```python
plt.tight_layout()


plt.show()
```

---

# 14. Dashboard Output

তুমি পাবে:

## Row 1

### Training Loss

দেখাবে:

* Learning হচ্ছে কিনা
* Overfitting হচ্ছে কিনা

### Accuracy

দেখাবে:

* Model improvement

---

## Row 2

### Confusion Matrix

দেখাবে:

* False alarm
* Miss detection

### ROC Curve

দেখাবে:

* Threshold performance

---

## Row 3

### Confidence Timeline

AI CCTV-এর জন্য:

```text
Frame 1 → 0.2

Frame 50 → 0.95

Alert Trigger
```

### Metrics

Final performance summary

---

# 15. Save Dashboard

Production report:

```python
plt.savefig(
"model_evaluation_dashboard.png",
dpi=300,
bbox_inches="tight"
)
```

PDF:

```python
plt.savefig(
"model_report.pdf",
bbox_inches="tight"
)
```

---

# 16. Real AI CCTV Architecture

তোমার project:

```text
Camera

 ↓

Frame Extraction

 ↓

CNN-LSTM Model

 ↓

Prediction Score

 ↓

Database

 ↓

Matplotlib Report

 ↓

Admin Dashboard
```

---

# 17. Reusable Dashboard Function

Industry style:

```python
def create_model_dashboard(
    history,
    confusion_matrix,
    metrics
):

    fig, axes = plt.subplots(
        2,
        2,
        figsize=(12,8)
    )

    # plots here


    plt.tight_layout()

    return fig
```

---

# 18. Matplotlib Mastery Progress

এখন পর্যন্ত তুমি শিখেছো:

✅ Basic plotting
✅ Figure/Axes architecture
✅ Professional styling
✅ Statistical visualization
✅ Animation
✅ ML evaluation
✅ Deep Learning visualization
✅ Dashboard creation

---

# Lesson 20 Practice Project

নিজের AI Model Dashboard তৈরি করো:

Input:

```python
training history

confusion matrix

prediction confidence

model metrics
```

Output:

একটি:

```
AI_Model_Report.pdf
```

যেখানে থাকবে:

1. Loss curve
2. Accuracy curve
3. Confusion matrix
4. ROC curve
5. Confidence graph
6. Metrics summary

---

পরের Lesson:

# Lesson 21: Matplotlib + Computer Vision Visualization

শিখবো:

* Image grid visualization
* Video frame visualization
* Bounding box drawing
* Object detection visualization
* OpenCV + Matplotlib integration

এটি তোমার AI CCTV project-এর জন্য সবচেয়ে practical অংশ হবে।
# Matplotlib Mastery Course

# Lesson 21: Matplotlib + Computer Vision Visualization

আজ থেকে আমরা **Computer Vision visualization** শিখবো।

AI Engineer / ML Engineer হিসেবে model শুধু prediction দিলেই হবে না, prediction কে মানুষের বোঝার মতো করে দেখাতে হবে।

আজকের বিষয়:

* Image visualization
* Image grid
* Multiple image display
* Bounding box drawing
* Object detection visualization
* OpenCV + Matplotlib integration
* AI CCTV frame visualization

---

# 1. Computer Vision Pipeline

Real-world CV pipeline:

```text
Camera / Video

      ↓

Image Frame

      ↓

Preprocessing

      ↓

Deep Learning Model

      ↓

Prediction

      ↓

Visualization
```

Visualization অংশে Matplotlib গুরুত্বপূর্ণ।

---

# 2. Image কীভাবে Represent হয়?

Computer image:

```text
Height × Width × Channel
```

Example:

```python
image.shape
```

Output:

```text
(224,224,3)
```

Meaning:

```text
Height  = 224

Width   = 224

Channel = RGB
```

---

# 3. Basic Image Display

Import:

```python
import matplotlib.pyplot as plt
import numpy as np
```

Random image:

```python
image=np.random.rand(
224,
224,
3
)
```

Display:

```python
plt.imshow(
    image
)


plt.axis(
"off"
)


plt.show()
```

---

# 4. Grayscale Image Visualization

Grayscale image:

```python
gray=np.random.rand(
100,
100
)
```

Display:

```python
plt.imshow(
    gray,
    cmap="gray"
)


plt.axis(
"off"
)


plt.show()
```

---

# 5. Image Size Control

Professional:

```python
fig, ax = plt.subplots(
    figsize=(5,5),
    dpi=300
)


ax.imshow(
    image
)


ax.axis(
"off"
)


plt.show()
```

---

# 6. Multiple Image Grid

Computer Vision dataset analysis-এ দরকার হয়।

Example:

একসাথে 16টা image দেখা:

```python
images=[
np.random.rand(64,64,3)
for _ in range(16)
]
```

Grid:

```python
fig, axes = plt.subplots(
    4,
    4,
    figsize=(8,8)
)


for img, ax in zip(
    images,
    axes.flat
):

    ax.imshow(
        img
    )

    ax.axis(
        "off"
    )


plt.show()
```

---

# 7. Dataset Visualization

ধরি:

UCF Crime Dataset:

```text
Normal

Suspicious
```

Sample দেখানো:

```python
fig, axes = plt.subplots(
2,
5,
figsize=(12,5)
)


for ax in axes.flat:

    ax.imshow(
        np.random.rand(64,64,3)
    )

    ax.axis(
        "off"
    )


plt.show()
```

---

# 8. Image Label Display

Dataset analysis:

```python
labels=[
"Normal",
"Suspicious"
]
```

Title:

```python
ax.set_title(
"Normal"
)
```

Example:

```python
fig, ax = plt.subplots()


ax.imshow(
image
)


ax.set_title(
"Suspicious"
)


ax.axis(
"off"
)


plt.show()
```

---

# 9. Bounding Box Visualization

Object Detection-এ সবচেয়ে গুরুত্বপূর্ণ।

Example:

Image:

```text
+----------------+
|                |
|    Person      |
|   +------+     |
|   |      |     |
|   +------+     |
|                |
+----------------+
```

---

# 10. Rectangle Add করা

Matplotlib:

```python
from matplotlib.patches import Rectangle
```

Example:

```python
fig, ax = plt.subplots()


ax.imshow(
image
)


box = Rectangle(
    (50,50),
    100,
    150,
    fill=False
)


ax.add_patch(
    box
)


plt.show()
```

---

# 11. Rectangle Parameters

```python
Rectangle(
(x,y),
width,
height
)
```

Example:

```text
Starting point:

(50,50)


Width:

100


Height:

150
```

---

# 12. Detection Label Add করা

Example:

```python
ax.text(
50,
40,
"Person"
)
```

Full:

```python
fig, ax = plt.subplots()


ax.imshow(
image
)


ax.add_patch(
Rectangle(
(50,50),
100,
150,
fill=False
)
)


ax.text(
50,
45,
"Person"
)


plt.show()
```

---

# 13. Multiple Bounding Boxes

Object detection:

```python
boxes=[
(20,30,50,80),
(100,60,40,90)
]
```

Loop:

```python
fig, ax = plt.subplots()


ax.imshow(
image
)


for x,y,w,h in boxes:

    rect=Rectangle(
        (x,y),
        w,
        h,
        fill=False
    )

    ax.add_patch(
        rect
    )


plt.show()
```

---

# 14. AI CCTV Frame Visualization

তোমার project:

```text
Video Frame

      ↓

CNN-LSTM

      ↓

Suspicious Score

      ↓

Alert
```

Visualization:

```text
+----------------+
|                |
|  Person        |
|  [BOX]         |
|                |
| Confidence 92% |
+----------------+
```

---

# 15. Confidence Text

Example:

```python
confidence=0.92


ax.text(
10,
20,
f"Confidence: {confidence:.2f}"
)
```

Output:

```text
Confidence: 0.92
```

---

# 16. OpenCV + Matplotlib

OpenCV image format:

```text
BGR
```

Matplotlib:

```text
RGB
```

তাই convert করতে হয়:

```python
import cv2


image=cv2.imread(
"frame.jpg"
)


image=cv2.cvtColor(
image,
cv2.COLOR_BGR2RGB
)
```

---

# 17. Video Frame Display

OpenCV:

```python
cap=cv2.VideoCapture(
"video.mp4"
)
```

Frame:

```python
ret, frame = cap.read()
```

Show:

```python
plt.imshow(
frame
)
```

---

# 18. AI Detection Result Visualization

Example:

Model output:

```python
prediction=0.87
```

Display:

```python
if prediction>0.85:

    label="Suspicious"

else:

    label="Normal"
```

Show:

```python
ax.set_title(
f"{label} {prediction:.2f}"
)
```

---

# 19. Computer Vision Report

একটি CV project report:

```text
+-------------------+
| Input Image       |
+-------------------+

+-------------------+
| Prediction        |
+-------------------+

+-------------------+
| Bounding Box      |
+-------------------+

+-------------------+
| Confidence        |
+-------------------+
```

---

# 20. Production Visualization Function

Reusable:

```python
def visualize_detection(
    image,
    boxes,
    label,
    confidence
):

    fig, ax = plt.subplots()


    ax.imshow(
        image
    )


    for x,y,w,h in boxes:

        ax.add_patch(
            Rectangle(
                (x,y),
                w,
                h,
                fill=False
            )
        )


    ax.set_title(
        f"{label}: {confidence:.2f}"
    )


    ax.axis(
        "off"
    )


    plt.show()
```

---

# 21. UCF Crime Project Connection

তোমার AI CCTV system:

Visualization:

### Frame Level:

```text
Frame 120

Prediction:
Suspicious

Confidence:
0.91
```

### Video Level:

```text
Time

↓

Confidence curve

↓

Alert point
```

### Model Explainability:

```text
Grad-CAM

↓

Important region
```

---

# Lesson 21 Practice Task

## Task 1

একটি random image তৈরি করো:

```python
224x224x3
```

Display:

* figsize
* dpi
* title

---

## Task 2

একটি image-এ:

* 3টি bounding box draw করো
* label add করো

---

## Task 3 (AI CCTV)

Fake output:

```python
boxes=[
(20,30,50,100)
]

label="Suspicious"

confidence=0.93
```

Create:

AI detection visualization

---

পরের Lesson:

# Lesson 22: Matplotlib + OpenCV + Real-Time Video Analytics

শিখবো:

* Video frame processing
* Live camera visualization
* FPS monitoring
* Detection overlay
* AI CCTV real-time dashboard

এটা তোমার surveillance project-এর production অংশের সাথে সরাসরি সম্পর্কিত।
# Matplotlib Mastery Course

# Lesson 22: Matplotlib + OpenCV + Real-Time Video Analytics

আজ আমরা Computer Vision-এর একটি খুব practical অংশ শিখবো:

**Real-time video analytics visualization**

এটি ব্যবহার হয়:

* AI CCTV System
* Object Detection
* Face Recognition
* Traffic Monitoring
* Industrial Monitoring
* Security System

তোমার AI CCTV project-এর জন্য এই lesson অনেক গুরুত্বপূর্ণ।

---

# 1. Real-Time Video Analytics Pipeline

Production pipeline:

```text
Camera

 ↓

OpenCV Capture

 ↓

Frame Processing

 ↓

AI Model Prediction

 ↓

Detection Result

 ↓

Matplotlib Visualization
```

---

# 2. OpenCV Installation

যদি না থাকে:

```bash
pip install opencv-python
```

Import:

```python
import cv2
import matplotlib.pyplot as plt
```

---

# 3. Video Capture

Video file:

```python
cap = cv2.VideoCapture(
    "video.mp4"
)
```

Webcam:

```python
cap = cv2.VideoCapture(
    0
)
```

---

# 4. Frame Read

একটি frame:

```python
ret, frame = cap.read()
```

Return:

```text
ret

True / False


frame

Image array
```

---

# 5. Frame Shape

Check:

```python
frame.shape
```

Example:

```text
(720,1280,3)
```

Meaning:

```text
Height = 720

Width = 1280

Channel = 3
```

---

# 6. OpenCV থেকে Matplotlib

Important:

OpenCV:

```text
BGR
```

Matplotlib:

```text
RGB
```

Conversion:

```python
frame_rgb = cv2.cvtColor(
    frame,
    cv2.COLOR_BGR2RGB
)
```

---

# 7. Single Frame Visualization

```python
import cv2
import matplotlib.pyplot as plt


cap=cv2.VideoCapture(
    "video.mp4"
)


ret, frame=cap.read()


frame=cv2.cvtColor(
    frame,
    cv2.COLOR_BGR2RGB
)


plt.imshow(
    frame
)


plt.axis(
"off"
)


plt.show()


cap.release()
```

---

# 8. Real-Time Loop

Basic:

```python
while True:

    ret, frame = cap.read()


    if not ret:
        break


    cv2.imshow(
        "Video",
        frame
    )


    if cv2.waitKey(1)==27:
        break


cap.release()

cv2.destroyAllWindows()
```

---

# 9. FPS (Frame Per Second)

Real-time system-এ FPS গুরুত্বপূর্ণ।

Formula:

```text
FPS = processed frames / time
```

---

# 10. FPS Calculate

```python
import time


prev_time=0


while True:

    current_time=time.time()


    fps=1/(current_time-prev_time)


    prev_time=current_time
```

---

# 11. FPS Display

```python
cv2.putText(
    frame,
    f"FPS: {fps:.2f}",
    (20,40),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (0,255,0),
    2
)
```

---

# 12. Object Detection Overlay

Model output:

```python
boxes=[
(100,100,200,300)
]
```

Format:

```text
x,y,width,height
```

---

# 13. Bounding Box Draw

```python
for x,y,w,h in boxes:


    cv2.rectangle(
        frame,
        (x,y),
        (x+w,y+h),
        (0,255,0),
        2
    )
```

---

# 14. Label Add

```python
cv2.putText(
    frame,
    "Person",
    (x,y-10),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (0,255,0),
    2
)
```

---

# 15. AI Prediction Overlay

ধরি:

```python
confidence=0.92
```

Label:

```python
label="Suspicious"
```

Display:

```python
text=f"{label}: {confidence:.2f}"


cv2.putText(
    frame,
    text,
    (20,70),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (0,0,255),
    2
)
```

---

# 16. AI CCTV Complete Example

Architecture:

```text
Camera

 ↓

Frame

 ↓

CNN-LSTM

 ↓

Probability

 ↓

Threshold

 ↓

Alert
```

Code structure:

```python
while True:


    ret, frame = cap.read()


    if not ret:
        break


    prediction=model.predict(
        frame
    )


    if prediction>0.85:

        label="Suspicious"

    else:

        label="Normal"



    cv2.putText(
        frame,
        label,
        (20,40),
        cv2.FONT_HERSHEY_SIMPLEX,
        1,
        (0,0,255),
        2
    )


    cv2.imshow(
        "AI CCTV",
        frame
    )
```

---

# 17. Matplotlib Live Dashboard

Production system:

```text
+----------------+
| Camera Frame   |
+----------------+

+----------------+
| Confidence     |
+----------------+

+----------------+
| Alert Count    |
+----------------+
```

---

# 18. Multiple Visualization

Example:

```python
fig, axes = plt.subplots(
2,
2
)
```

Show:

```text
axes[0,0]

Current Frame


axes[0,1]

Confidence


axes[1,0]

FPS


axes[1,1]

Alert Statistics
```

---

# 19. Confidence Graph During Video

Store:

```python
confidence_history=[]
```

Every frame:

```python
confidence_history.append(
    confidence
)
```

Plot:

```python
ax.plot(
    confidence_history
)
```

---

# 20. Real-Time AI Monitoring Dashboard

Final architecture:

```text
                Camera

                  ↓

            OpenCV Stream

                  ↓

            AI Model

                  ↓

        +----------------+

        | Prediction     |

        | Confidence     |

        | FPS            |

        | Alert          |

        +----------------+

                  ↓

          Visualization

                  ↓

             Dashboard
```

---

# 21. Performance Optimization

Real-time AI system-এর জন্য:

## Resize Frame

```python
frame=cv2.resize(
    frame,
    (640,480)
)
```

---

## Skip Frame

Example:

```text
Process:

Every 5th frame
```

কারণ:

Deep Learning inference expensive।

---

## Use GPU

TensorFlow/PyTorch:

```text
CPU → Slow

GPU → Fast
```

---

# 22. AI CCTV Project Improvement

তোমার project:

Current:

```text
Video
 ↓
CNN-LSTM
 ↓
Prediction
```

Production:

```text
Camera Stream

 ↓

Frame Queue

 ↓

Celery Worker

 ↓

GPU Inference

 ↓

Redis Result

 ↓

WebSocket

 ↓

React Dashboard
```

Matplotlib এখানে:

* Testing
* Research
* Report

এর জন্য ব্যবহার হবে।

---

# Lesson 22 Practice Task

## Task 1

OpenCV দিয়ে:

* Video open করো
* Frame read করো
* RGB convert করো
* Matplotlib দিয়ে show করো

---

## Task 2

একটি frame-এ:

* Bounding box
* Label
* Confidence score

দেখাও।

---

## Task 3 (AI CCTV)

Fake prediction:

```python
confidence=[
0.2,
0.4,
0.7,
0.9
]
```

Create:

* Confidence timeline
* Threshold line = 0.85
* Alert point

---

পরের Lesson:

# Lesson 23: Matplotlib + Data Engineering Visualization

শিখবো:

* Large dataset visualization
* Performance monitoring
* ETL pipeline metrics
* Database analytics charts
* Production data reports

এটি Data Engineer role-এর জন্য গুরুত্বপূর্ণ।
