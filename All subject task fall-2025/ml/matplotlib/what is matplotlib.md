## What is Matplotlib?

Matplotlib is the most popular Python library for **data visualization**. It helps you turn numbers and data into charts, graphs, and plots.

Think of it like:

|Library|Purpose|
|---|---|
|NumPy|Numerical calculations|
|Pandas|Data manipulation|
|Matplotlib|Data visualization|
|Scikit-learn|Machine learning|

---

# Why Use Matplotlib?

Suppose you have sales data:

```python
sales = [100, 200, 150, 300, 250]
```

Looking at numbers is difficult.

With `Matplotlib`:

📈 Line Chart

```text
300 |            *
250 |         *
200 |      *
150 |   *
100 | *
    +----------------
```

You can instantly see trends.

---

# Install

```bash
pip install matplotlib
```

Import:

```python
import matplotlib.pyplot as plt
```

`plt` is the standard alias.

---

# First Plot

```python
import matplotlib.pyplot as plt

x = [1,2,3,4,5]
y = [10,20,30,40,50]

plt.plot(x,y)

plt.show()
```

This creates a simple line graph.

---

# Basic Terminology

## Figure

The entire chart.

```text
+----------------------+
|       Figure         |
|                      |
|     Plot Area        |
|                      |
+----------------------+
```

---
## Axes

The plotting area.

```text
Y-axis
|
|
|
+------------ X-axis
```

---

## X-axis

Horizontal axis.

```python
x=[1,2,3,4]
```

---

## Y-axis

Vertical axis.

```python
y=[10,20,30,40]
```

---

# 1. Line Plot

Most common chart.

```python
import matplotlib.pyplot as plt

x=[1,2,3,4]
y=[10,20,15,30]

plt.plot(x,y)

plt.show()
```

Used for:
- Stock prices
- Sales trends
- Temperature changes
    
---

# 2. Bar Chart

Compare categories.

```python
import matplotlib.pyplot as plt

names=["A","B","C"]
marks=[80,90,70]

plt.bar(names,marks)

plt.show()
```

Used for:

- Student marks
    
- Product sales
    
- Survey results
    
---

# 3. Horizontal Bar Chart

```python
plt.barh(names,marks)
```

---

# 4. Histogram

Shows distribution.

```python
import numpy as np
import matplotlib.pyplot as plt

data=np.random.randn(1000)
plt.hist(data)
plt.show()
```

Used for:

- Age distribution
    
- Salary distribution
    
- Exam scores
    

---

# 5. Scatter Plot

Shows relationships.

```python
import matplotlib.pyplot as plt

height=[150,160,170,180]
weight=[50,60,70,80]

plt.scatter(height,weight)

plt.show()
```

Used for:

- Correlation analysis
    
- Machine learning
    

---

# 6. Pie Chart

Percentage distribution.

```python
import matplotlib.pyplot as plt

sizes=[40,30,20,10]

plt.pie(sizes)

plt.show()
```

Used for:

- Market share
    
- Budget allocation
    

---

# Labels

## Title

```python
plt.title("Sales Report")
```

---

## X Label

```python
plt.xlabel("Month")
```

---

## Y Label

```python
plt.ylabel("Sales")
```

---

Complete Example:

```python
plt.plot(x,y)

plt.title("Monthly Sales")

plt.xlabel("Month")

plt.ylabel("Revenue")

plt.show()
```

---

# Legend

Useful when multiple lines exist.

```python
plt.plot(x,y1,label="2024")

plt.plot(x,y2,label="2025")

plt.legend()

plt.show()
```

---

# Grid

```python
plt.grid(True)
```

Makes graphs easier to read.

---
# Line Styles

```python
plt.plot(
    x,
    y,
    linestyle="--"
)
```

Common styles:

```text
-   solid
--  dashed
:   dotted
-.  dash-dot
```

---

# Markers

```python
plt.plot(
    x,
    y,
    marker="o"
)
```

Examples:

```text
o circle
s square
^ triangle
* star
```

---

# Multiple Plots

```python
plt.subplot(1,2,1)

plt.plot(x,y)

plt.subplot(1,2,2)

plt.bar(x,y)

plt.show()
```

---

# Save Graph

```python
plt.savefig("graph.png")
```

---

# Matplotlib + NumPy

```python
import numpy as np
import matplotlib.pyplot as plt

x=np.arange(0,10)

y=x**2

plt.plot(x,y)

plt.show()
```

Creates:

```text
y = x²
```

graph.

---

# Matplotlib + Pandas

```python
import pandas as pd

df=pd.read_csv("sales.csv")

plt.plot(
    df["Month"],
    df["Sales"]
)

plt.show()
```

Very common in data analysis.

---

# Real-Life Uses

### Data Analyst

- Sales reports
    
- Revenue trends
    
- Customer analytics
    

### Data Scientist

- Data exploration
    
- Feature analysis
    
- Correlation checking
    

### Machine Learning Engineer

- Training curves
    
- Accuracy graphs
    
- Loss graphs
    

### Finance

- Stock charts
    
- Market analysis
    

### Healthcare

- Patient statistics
    
- Disease trends
    

---

# Most Important Matplotlib Topics

Learn these first:

1. `plot()`
    
2. `bar()`
    
3. `hist()`
    
4. `scatter()`
    
5. `pie()`
    
6. `title()`
    
7. `xlabel()`
    
8. `ylabel()`
    
9. `legend()`
    
10. `grid()`
    
11. `savefig()`
    
12. NumPy integration
    
13. Pandas integration
    

---

## Complete Data Science Roadmap

1. Python
    
2. NumPy
    
3. Pandas
    
4. Matplotlib
    
5. Seaborn (advanced visualization)
    
6. Scikit-learn
    
7. Machine Learning
    

NumPy handles calculations, Pandas handles data, and Matplotlib helps you **see and understand the data visually**.