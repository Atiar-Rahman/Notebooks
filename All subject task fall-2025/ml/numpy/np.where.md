`numpy.where()` is used in real life whenever you need to **find positions, filter data, or make decisions on large datasets quickly**.

Think of it as a NumPy version of:

> "Where is this condition true?"

---

## 1. Find positions of values

Example: Student marks

```python
import numpy as np

marks = np.array([45, 78, 90, 33, 85])

result = np.where(marks >= 50)

print(result)
```

Output:

```text
(array([1, 2, 4]),)
```

Meaning:

```
Index 1 → 78
Index 2 → 90
Index 4 → 85
```

Real life:

- Find students who passed
    
- Find customers above a score
    
- Find products with high ratings
    

---

# 2. Replace values (very common)

Example: Temperature monitoring

```python
temperature = np.array([25, 35, 40, 20, 50])

status = np.where(
    temperature > 30,
    "Hot",
    "Normal"
)

print(status)
```

Output:

```text
['Normal' 'Hot' 'Hot' 'Normal' 'Hot']
```

Meaning:

```
if temperature > 30:
       Hot
else:
       Normal
```

Real life:

- Weather apps
    
- IoT sensors
    
- Machine monitoring
    

---

# 3. Data cleaning

Example: Replace negative values

```python
sales = np.array([100, 200, -50, 300, -10])

clean = np.where(
    sales < 0,
    0,
    sales
)

print(clean)
```

Output:

```text
[100 200 0 300 0]
```

Real life:

- Remove bad data
    
- Fix missing measurements
    
- Clean datasets before ML
    

---

# 4. Find expensive products

Example:

```python
prices = np.array([100, 500, 1200, 300, 2000])

expensive = np.where(prices > 1000)

print(expensive)
```

Output:

```text
(array([2,4]),)
```

Products:

```
1200
2000
```

Real life:

- E-commerce recommendation
    
- Price analysis
    

---

# 5. Machine Learning preprocessing

Example: Convert labels

Before:

```python
labels=np.array([
"cat",
"dog",
"cat",
"bird"
])
```

Convert:

```python
numbers=np.where(
labels=="cat",
1,
0
)

print(numbers)
```

Output:

```text
[1 0 1 0]
```

Real life:

- Convert categories into numbers
    
- Prepare data for ML models
    

---

# 6. Find missing values

Example:

```python
data=np.array([10,20,np.nan,40])

missing=np.where(
np.isnan(data)
)

print(missing)
```

Output:

```text
(array([2]),)
```

Meaning:

```
Index 2 has missing data
```

Real life:

- Detect incomplete records
    

---

# 7. Image processing

Images are arrays.

Example:

```python
image=np.array([
[50,200,30],
[250,80,100]
])

bright=np.where(
image>150,
255,
0
)

print(bright)
```

Output:

```text
[
[0 255 0]
[255 0 0]
]
```

Meaning:

```
Bright pixel → white
Dark pixel → black
```

Real life:

- Face detection
    
- Image filters
    
- Computer vision
    

---

# 8. Finance example

Stock prices:

```python
prices=np.array([
100,120,90,150,80
])

signal=np.where(
prices>100,
"BUY",
"WAIT"
)

print(signal)
```

Output:

```text
['WAIT' 'BUY' 'WAIT' 'BUY' 'WAIT']
```

Used for:

- Market analysis
    
- Trading algorithms
    

---

# 9. Multiple conditions

Example: Student grades

```python
marks=np.array([95,75,40,88])

grade=np.where(
marks>=80,
"A",
np.where(
marks>=50,
"B",
"Fail"
)
)

print(grade)
```

Output:

```text
['A' 'B' 'Fail' 'A']
```

---

# 10. Difference from normal filtering

Normal:

```python
a[a>10]
```

gives values:

```text
[20 30]
```

`where()`:

```python
np.where(a>10)
```

gives locations:

```text
[1 2]
```

---

## Real-world places you use `np.where()`

|Field|Example|
|---|---|
|Data Science|Filter datasets|
|Machine Learning|Label encoding|
|Finance|Buy/sell signals|
|Healthcare|Detect abnormal values|
|IoT|Sensor alerts|
|E-commerce|Price filtering|
|Computer Vision|Pixel processing|
|Business Analytics|Customer segmentation|

In practice, `np.where()` is one of the most used NumPy functions after `array()`, `reshape()`, and aggregation functions.