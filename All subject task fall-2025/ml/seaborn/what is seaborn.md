## What is Seaborn?

Seaborn is a Python **data visualization library** built on top of Matplotlib. It makes statistical graphs easier to create and gives them a more professional style by default.

Simple idea:

- **Matplotlib** → low-level control, build anything
    
- **Seaborn** → easier, beautiful statistical visualization
    

---

## Why use Seaborn?

Suppose you have data:

|Age|Salary|Gender|
|---|---|---|
|20|30000|M|
|25|50000|F|
|30|70000|M|

Seaborn can quickly show:

- relationships
    
- distributions
    
- categories
    
- trends
    
- correlations
    

with only a few lines.

---

# Install

```bash
pip install seaborn
```

Import:

```python
import seaborn as sns
import matplotlib.pyplot as plt
```

---

# Seaborn vs Matplotlib

|Feature|Matplotlib|Seaborn|
|---|---|---|
|Level|Low-level|High-level|
|Styling|Manual|Automatic|
|Statistical plots|Basic|Excellent|
|DataFrame support|Good|Excellent|
|ML visualization|Good|Very good|

---

# Basic Example

```python
import seaborn as sns
import matplotlib.pyplot as plt

data = sns.load_dataset("tips")

sns.scatterplot(
    x="total_bill",
    y="tip",
    data=data
)

plt.show()
```

Output idea:

Shows relationship between:

```
Bill amount → Tip amount
```

---

# Important Seaborn Topics (Basic → Advanced)

## 1. Loading Data

Built-in datasets:

```python
sns.load_dataset("tips")
```

Examples:

- tips
    
- iris
    
- titanic
    
- flights
    

---

# 2. Scatter Plot

Shows relationship.

```python
sns.scatterplot(
    x="total_bill",
    y="tip",
    data=data
)
```

Used:

- correlation
    
- feature analysis
    

---

# 3. Line Plot

Shows trends.

```python
sns.lineplot(
    x="year",
    y="passengers",
    data=data
)
```

Used:

- time series
    
- business trends
    

---

# 4. Bar Plot

Compare categories.

```python
sns.barplot(
    x="day",
    y="total_bill",
    data=data
)
```

Example:

```
Monday   █████
Tuesday  ███████
Friday   █████████
```

---

# 5. Count Plot

Counts categories.

```python
sns.countplot(
    x="sex",
    data=data
)
```

Used:

- customer groups
    
- surveys
    

---

# 6. Histogram

Distribution.

```python
sns.histplot(
    data["total_bill"]
)
```

Shows:

```
small values → many
large values → few
```

---

# 7. KDE Plot

Smooth distribution curve.

```python
sns.kdeplot(
    data["total_bill"]
)
```

Used:

- probability distribution
    

---

# 8. Box Plot

Find outliers.

```python
sns.boxplot(
    x="day",
    y="total_bill",
    data=data
)
```

Shows:

- median
    
- spread
    
- outliers
    

---

# 9. Violin Plot

Combination of:

Box plot + KDE

```python
sns.violinplot(
    x="day",
    y="total_bill",
    data=data
)
```

---

# 10. Pair Plot ⭐

Very useful for ML.

```python
sns.pairplot(data)
```

Shows relationships between all columns.

Example:

```
Age vs Salary
Age vs Score
Salary vs Score
```

---

# 11. Heatmap ⭐

Shows matrix relationships.

Example:

Correlation matrix:

```python
corr=data.corr()

sns.heatmap(
    corr,
    annot=True
)
```

Used for:

- feature selection
    
- correlation analysis
    

---

# 12. Regression Plot

Shows trend line.

```python
sns.regplot(
    x="total_bill",
    y="tip",
    data=data
)
```

---

# 13. Styling

Change theme:

```python
sns.set_style("darkgrid")
```

Styles:

```text
white
dark
whitegrid
darkgrid
ticks
```

---

# 14. Color Palette

```python
sns.set_palette("deep")
```

---

# 15. Hue (Grouping)

Example:

```python
sns.scatterplot(
    x="total_bill",
    y="tip",
    hue="sex",
    data=data
)
```

Creates groups:

```
Male
Female
```

---

# 16. FacetGrid

Create multiple plots.

```python
g=sns.FacetGrid(
data,
col="sex"
)

g.map(
sns.histplot,
"total_bill"
)
```

---

# 17. PairGrid

Custom pair plots.

```python
g=sns.PairGrid(data)

g.map(sns.scatterplot)
```

---

# 18. Categorical Plots

Learn:

- `catplot()`
    
- `boxplot()`
    
- `violinplot()`
    
- `stripplot()`
    
- `swarmplot()`
    

---

# 19. Distribution Plots

Learn:

- `histplot()`
    
- `kdeplot()`
    
- `ecdfplot()`
    
- `rugplot()`
    

---

# 20. Advanced Topics

Learn:

- Themes
    
- Color palettes
    
- Custom styles
    
- Figure-level plots
    
- Axes-level plots
    
- Combining with Matplotlib
    
- Saving figures
    

---

# Seaborn Real-Life Uses

## Data Analyst

- Sales analysis
    
- Customer behavior
    
- Reports
    

## Data Scientist

- Exploratory Data Analysis (EDA)
    
- Feature relationships
    
- Outlier detection
    

## Machine Learning

- Correlation heatmap
    
- Feature selection
    
- Model evaluation visualization
    

---

# Data Science Visualization Stack

Typical workflow:

```
NumPy
  ↓
Pandas
  ↓
Seaborn
  ↓
Matplotlib
  ↓
Machine Learning
```

---

## Most Important Seaborn Topics (80% Work)

Master these first:

1. `scatterplot()`
    
2. `lineplot()`
    
3. `barplot()`
    
4. `countplot()`
    
5. `histplot()`
    
6. `boxplot()`
    
7. `violinplot()`
    
8. `pairplot()`
    
9. `heatmap()`
    
10. `regplot()`
    
11. `catplot()`
    
12. Themes & colors
    

After these, you can do most **professional data analysis visualizations**.