# Matplotlib Complete Roadmap (Basic → Advanced)

Matplotlib is a Python visualization library used to create charts, graphs, and plots for **data analysis, statistics, machine learning, and reporting**.

---

# Level 1 — Matplotlib Basics

## 1. Installation

```bash
pip install matplotlib
```

Import:

```python
import matplotlib.pyplot as plt
```

`pyplot` is the most commonly used module.

---

# 2. First Plot

```python
import matplotlib.pyplot as plt

x = [1,2,3,4,5]
y = [10,20,15,30,25]

plt.plot(x,y)

plt.show()
```

Creates a line chart.

---

# 3. Figure and Axes

A chart has:

```
Figure
 └── Axes
      ├── X-axis
      ├── Y-axis
      └── Plot
```

Create manually:

```python
fig, ax = plt.subplots()

ax.plot(x,y)

plt.show()
```

This is the recommended professional style.

---

# 4. Titles and Labels

```python
plt.plot(x,y)

plt.title("Sales Report")

plt.xlabel("Month")

plt.ylabel("Revenue")

plt.show()
```

---

# 5. Line Styling

## Color

```python
plt.plot(
    x,y,
    color="red"
)
```

## Line Width

```python
plt.plot(
    x,y,
    linewidth=3
)
```

## Line Style

```python
plt.plot(
    x,y,
    linestyle="--"
)
```

Styles:

```
-   solid
--  dashed
:   dotted
-.  dash-dot
```

---

# 6. Markers

Add points:

```python
plt.plot(
    x,y,
    marker="o"
)
```

Common:

```
o circle
s square
^ triangle
* star
```

---

# Level 2 — Basic Charts

# 7. Line Plot

Used for trends.

Example:

```python
days=[1,2,3,4,5]
temp=[20,25,23,30,28]

plt.plot(days,temp)

plt.show()
```

Real life:

- Stock price
    
- Temperature
    
- Sales over time
    

---

# 8. Bar Chart

Compare categories.

```python
products=["A","B","C"]

sales=[100,200,150]


plt.bar(products,sales)

plt.show()
```

Used:

- Product comparison
    
- Revenue
    

---

# 9. Horizontal Bar

```python
plt.barh(
    products,
    sales
)
```

---

# 10. Scatter Plot

Shows relationships.

```python
height=[150,160,170,180]

weight=[50,60,70,80]


plt.scatter(
    height,
    weight
)

plt.show()
```

Used:

- Correlation
    
- ML feature analysis
    

---

# 11. Histogram

Shows distribution.

```python
import numpy as np

data=np.random.randn(1000)

plt.hist(data)

plt.show()
```

Used:

- Salary distribution
    
- Age distribution
    

---

# 12. Pie Chart

Percentage visualization.

```python
sizes=[40,30,20,10]

plt.pie(
    sizes,
    labels=["A","B","C","D"]
)

plt.show()
```

---

# Level 3 — Multiple Data

## 13. Multiple Lines

```python
x=[1,2,3,4]

y1=[10,20,30,40]

y2=[5,15,25,35]


plt.plot(x,y1,label="2024")

plt.plot(x,y2,label="2025")


plt.legend()

plt.show()
```

---

# 14. Legend

```python
plt.legend()
```

Position:

```python
plt.legend(
    loc="upper left"
)
```

---

# 15. Grid

```python
plt.grid(True)
```

---

# 16. Axis Control

Limits:

```python
plt.xlim(0,10)

plt.ylim(0,100)
```

---

# Level 4 — Subplots

Create multiple charts.

```python
fig,axs=plt.subplots(2,2)


axs[0,0].plot(x,y)

axs[0,1].bar(products,sales)

axs[1,0].scatter(height,weight)


plt.show()
```

Layout:

```
+-------+-------+
| plot1 | plot2 |
+-------+-------+
| plot3 | plot4 |
+-------+-------+
```

---

# Level 5 — Working With Data

## 17. NumPy Integration

```python
import numpy as np

x=np.arange(0,10)

y=x**2


plt.plot(x,y)

plt.show()
```

---

## 18. Pandas Integration

```python
import pandas as pd

df=pd.DataFrame({
"Month":[1,2,3],
"Sales":[100,200,300]
})


plt.plot(
df["Month"],
df["Sales"]
)

plt.show()
```

---

# Level 6 — Advanced Customization

## 19. Text Annotation

Add notes:

```python
plt.annotate(
"Highest",
xy=(4,30)
)
```

Used in reports.

---

## 20. Figure Size

```python
plt.figure(
figsize=(10,5)
)

plt.plot(x,y)

plt.show()
```

---

## 21. Transparency

```python
plt.plot(
x,y,
alpha=0.5
)
```

Range:

```
0 = invisible
1 = fully visible
```

---

## 22. Tick Control

```python
plt.xticks(
[1,2,3,4],
["Jan","Feb","Mar","Apr"]
)
```

---

# Level 7 — Advanced Plot Types

## 23. Box Plot

Shows spread and outliers.

```python
data=[
10,20,30,40,100
]


plt.boxplot(data)

plt.show()
```

Used:

- Statistics
    
- Outlier detection
    

---

## 24. Area Plot

```python
plt.fill_between(
x,y
)
```

---

## 25. Error Bars

```python
plt.errorbar(
x,
y,
yerr=5
)
```

Used:

- Scientific experiments
    

---

## 26. Stack Bar

```python
plt.bar(
x,
y1
)

plt.bar(
x,
y2,
bottom=y1
)
```

---

# Level 8 — Object-Oriented Matplotlib

Professional style:

```python
fig,ax=plt.subplots()

ax.plot(x,y)

ax.set_title("Sales")

ax.set_xlabel("Month")

ax.set_ylabel("Revenue")

plt.show()
```

Advantages:

- Cleaner code
    
- Multiple charts
    
- Large projects
    

---

# Level 9 — Saving Figures

Save:

```python
plt.savefig(
"chart.png",
dpi=300
)
```

Formats:

```
png
jpg
pdf
svg
```

---

# Level 10 — Styles

View styles:

```python
plt.style.available
```

Apply:

```python
plt.style.use("ggplot")
```

---

# Level 11 — 3D Plotting

```python
from mpl_toolkits.mplot3d import Axes3D


fig=plt.figure()

ax=fig.add_subplot(
111,
projection="3d"
)

ax.scatter(
x,y,z
)

plt.show()
```

Used:

- Scientific visualization
    

---

# Level 12 — Machine Learning Visualization

## Training Loss

```python
epochs=[1,2,3,4]

loss=[0.9,0.5,0.3,0.1]


plt.plot(
epochs,
loss
)

plt.xlabel("Epoch")

plt.ylabel("Loss")
```

---

## Accuracy Curve

```python
accuracy=[50,70,85,95]

plt.plot(accuracy)
```

---

# Level 13 — Performance Tips

Use:

✅ Object-oriented API

```python
fig,ax=plt.subplots()
```

Avoid:

```python
plt.plot()
```

for large projects.

---

# Level 14 — Real Data Science Workflow

Typical:

```
Load Data
     |
Pandas Cleaning
     |
NumPy Calculation
     |
Matplotlib Visualization
     |
Machine Learning
```

---

# Must Master Topics (80% Work)

1. `plot()`
    
2. `bar()`
    
3. `scatter()`
    
4. `hist()`
    
5. `pie()`
    
6. `subplots()`
    
7. labels/title
    
8. legend
    
9. grid
    
10. styling
    
11. annotations
    
12. Pandas + NumPy integration
    
13. saving figures
    
14. object-oriented API
    
15. statistical plots
    

After mastering these, you can create almost any standard visualization needed for **data analysis, AI, and machine learning**.