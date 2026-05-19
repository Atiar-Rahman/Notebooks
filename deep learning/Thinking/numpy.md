
# 🔷 `NumPy` কী?

`**NumPy `(Numerical Python)** হলো Python-এর সবচেয়ে fast numerical library  
👉 array, matrix, vector নিয়ে কাজ করে  
👉 ML, DL, CV, Pandas—সবকিছুর base

---

# 🔷 Python List vs NumPy Array

|Feature|List|NumPy Array|
|---|---|---|
|Speed|Slow|🔥 Very Fast|
|Type|Mixed|Same dtype|
|Math|Manual loop|Built-in|
|ML|❌|✅|

```python
import numpy as np
a = [1,2,3]
b = np.array([1,2,3])
```

---

# 🔷 Array Creation (সব ধরনের)

```python
np.array([1,2,3])
np.array([[1,2],[3,4]])

np.zeros((3,3))
np.ones((2,4))
np.full((2,2), 7)

np.arange(0, 10, 2)
np.linspace(0, 1, 5)

np.random.rand(3,3)
np.random.randn(3,3)
np.random.randint(1, 10, (3,3))
```

---

# 🔷 Array Properties (Must Know)

```python
a = np.array([[1,2,3],[4,5,6]])

a.shape     # (2,3)
a.ndim      # 2
a.size      # 6
a.dtype     # int64
```

---

# 🔷 Indexing & Slicing (🔥 Very Important)

## 1D

```python
a = np.array([10,20,30,40,50])

a[0]
a[-1]
a[1:4]
```

## 2D

```python
b = np.array([[1,2,3],[4,5,6]])

b[0,1]
b[:,1]
b[1,:]
```

---

# 🔷 Reshape / Flatten

```python
a = np.arange(12)

a.reshape(3,4)
a.reshape(-1,1)
a.flatten()
```

---

# 🔷 Mathematical Operations

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

a + b
a - b
a * b
a / b
a ** 2

np.sqrt(a)
np.log(a)
np.exp(a)
```

---

# 🔷 Aggregation Functions

```python
a = np.array([10,20,30])

np.sum(a)
np.mean(a)
np.max(a)
np.min(a)
np.std(a)
np.var(a)
```

---

# 🔷 Axis Explained (Confusing but Must)

```python
a = np.array([[1,2,3],[4,5,6]])

np.sum(a, axis=0)  # column
np.sum(a, axis=1)  # row
```

🧠 Rule:

- axis=0 → vertically
    
- axis=1 → horizontally
    

---

# 🔷 Broadcasting (🔥 Interview Favorite)

```python
a = np.array([[1,2,3],[4,5,6]])
b = np.array([1,2,3])

a + b
```

👉 ছোট array বড় array-এর সাথে auto adjust হয়

---

# 🔷 Boolean Indexing (Very Important)

```python
a = np.array([10,20,30,40,50])

a[a > 30]
a[(a > 20) & (a < 50)]
```

❌ Wrong:

```python
a > 20 & a < 50
```

---

# 🔷 Copy vs View

```python
a = np.array([1,2,3])
b = a.copy()

b[0] = 100
```

👉 copy করলে original change হয় না

---

# 🔷 Stack / Split

```python
a = np.array([1,2])
b = np.array([3,4])

np.hstack((a,b))
np.vstack((a,b))

np.split(np.array([1,2,3,4]), 2)
```

---

# 🔷 Sorting & Searching

```python
a = np.array([40,10,30,20])

np.sort(a)
np.argsort(a)
np.where(a > 25)
```

---

# 🔷 Linear Algebra (ML Base)

```python
A = np.array([[1,2],[3,4]])
B = np.array([[5,6],[7,8]])

np.dot(A, B)
A.T
np.linalg.det(A)
np.linalg.inv(A)
```

---

# 🔷 Random & Seed

```python
np.random.seed(42)
np.random.rand(3)
```

---

# 🔷 NumPy in Machine Learning

```python
X = np.array([[1,2],[3,4],[5,6]])
y = np.array([0,1,1])

X.shape
y.reshape(-1,1)
```

---

# 🔷 Mini Project (Exam + Viva)

```python
marks = np.array([45, 67, 89, 32, 55])

avg = marks.mean()
topper = marks.max()
passed = marks[marks >= 40]
failed = marks[marks < 40]
```

---

# 🔥 MUST-REMEMBER (Exam)

- list vs array
    
- reshape vs flatten
    
- axis meaning
    
- broadcasting
    
- boolean indexing
    
- dot vs *
    

---

# 🚀 Next Step (Strong Path for You)

**NumPy → Pandas → Matplotlib → ML → CV**

(তুমি already Pandas/ML করছো, তাই NumPy mastery খুব দরকার)

---

চাও তো আমি next করে দিতে পারি:  
1️⃣ **50 NumPy Practice Problems + Solution**  
2️⃣ **Exam MCQ + Short Questions**  
3️⃣ **NumPy দিয়ে ML from scratch (KNN / Linear Regression)**

বললেই শুরু করবো ✅

------
ঠিক আছে 👍  
এগুলোই **NumPy–র সবচেয়ে important exam + interview questions**।  
আমি **simple English + Bengali explanation + example** দিচ্ছি।

---

# 🔹 1️⃣ List vs NumPy Array

### 📌 Difference Table

|Feature|Python List|NumPy Array|
|---|---|---|
|Speed|Slow|🔥 Very Fast|
|Data Type|Mixed allowed|Same dtype|
|Memory|More|Less|
|Math Ops|Loop লাগে|Direct|
|ML Use|❌|✅|

### ✅ Example

```python
# List
a = [1, 2, 3]
print(a * 2)   # [1,2,3,1,2,3]

# NumPy Array
import numpy as np
b = np.array([1, 2, 3])
print(b * 2)   # [2 4 6]
```

📝 **Exam Line**

> NumPy array is faster and supports vectorized operations, unlike Python list.

---

# 🔹 2️⃣ Reshape vs Flatten

### 🔸 reshape()

- Shape change করে
    
- Data same থাকে
    
- Size same হতে হবে
    

```python
a = np.arange(6)
a.reshape(2,3)
```

Output:

```
[[0 1 2]
 [3 4 5]]
```

### 🔸 flatten()

- 2D → 1D বানায়
    
- New copy তৈরি করে
    

```python
b = np.array([[1,2],[3,4]])
b.flatten()
```

Output:

```
[1 2 3 4]
```

📌 Difference

|reshape|flatten|
|---|---|
|Shape change|1D করে|
|Same data|New copy|
|ML input prep|Data cleaning|

📝 **Exam Line**

> reshape changes array shape, flatten converts multi-dimensional array into 1D.

---

# 🔹 3️⃣ Axis Meaning (🔥 Most Confusing)

### Rule:

- **axis = 0 → column-wise**
    
- **axis = 1 → row-wise**
    

### Example

```python
a = np.array([[1,2,3],
              [4,5,6]])
```

#### axis = 0

```python
np.sum(a, axis=0)
```

➡️ (1+4, 2+5, 3+6) = `[5 7 9]`

#### axis = 1

```python
np.sum(a, axis=1)
```

➡️ (1+2+3, 4+5+6) = `[6 15]`

🧠 Trick:

> axis যেদিকে কাজ করে, সেই direction বাদ যায়

---

# 🔹 4️⃣ Broadcasting

### 📌 What is Broadcasting?

Small array automatically expands to match larger array shape.

### Example

```python
a = np.array([[1,2,3],
              [4,5,6]])
b = np.array([1,2,3])

a + b
```

Output:

```
[[2 4 6]
 [5 7 9]]
```

📝 **Exam Line**

> Broadcasting allows arithmetic operations on arrays of different shapes.

---

# 🔹 5️⃣ Boolean Indexing

### 📌 Condition দিয়ে data filter করা

```python
a = np.array([10,20,30,40,50])

a[a > 30]
```

Output:

```
[40 50]
```

### Multiple Condition

```python
a[(a > 20) & (a < 50)]
```

❌ Wrong

```python
a > 20 & a < 50
```

📝 **Exam Line**

> Boolean indexing is used to select elements based on condition.

---

# 🔹 6️⃣ Dot vs * (🔥 ML Question)

### 🔸 * (Element-wise Multiplication)

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

a * b
```

Output:

```
[4 10 18]
```

---

### 🔸 dot() (Matrix / Vector Multiplication)

```python
np.dot(a, b)
```

Output:

```
32
```

### 2D Matrix

```python
A = np.array([[1,2],
              [3,4]])
B = np.array([[5,6],
              [7,8]])

np.dot(A, B)
```

---

📌 Difference Summary

|*|dot|
|---|---|
|Element-wise|Matrix multiply|
|Same shape|Compatible shape|
|Simple math|ML / DL use|

📝 **Exam Line**

> `*` performs element-wise multiplication, while `dot()` performs matrix multiplication.

---

# ✅ FINAL EXAM SUMMARY (5 lines)

- List is slower; NumPy array is faster and optimized
    
- reshape changes shape; flatten converts to 1D
    
- axis=0 → column, axis=1 → row
    
- Broadcasting handles different shapes
    
- Boolean indexing filters data
    
- `*` is element-wise, `dot()` is matrix multiplication
    

---

চাও তো আমি এটাকে:

- 📄 **PDF notes**
    
- ❓ **MCQ + Viva Q&A**
    
- 🧠 **ML-based numerical examples**
    

যেকোনোটা বানিয়ে দিতে পারি। বলো ✔️

---------
চল 💪  
নিচে **50 NumPy Practice Problems + Full Solutions** দেওয়া হলো —  
👉 **Beginner → Intermediate → Advanced (ML-ready)**  
👉 Exam + Interview + Project সব কভার করবে

---

# 🔰 Beginner Level (1–15)

### 1️⃣ Create 1D array from 1 to 10

```python
np.arange(1, 11)
```

---

### 2️⃣ Create 3×3 zero matrix

```python
np.zeros((3,3))
```

---

### 3️⃣ Create 2×4 ones matrix

```python
np.ones((2,4))
```

---

### 4️⃣ Create array of 5 random numbers

```python
np.random.rand(5)
```

---

### 5️⃣ Find shape of array

```python
a.shape
```

---

### 6️⃣ Find number of dimensions

```python
a.ndim
```

---

### 7️⃣ Convert list to NumPy array

```python
np.array([5,10,15])
```

---

### 8️⃣ Create array of even numbers from 0–20

```python
np.arange(0, 21, 2)
```

---

### 9️⃣ Get first 3 elements

```python
a[:3]
```

---

### 🔟 Reverse array

```python
a[::-1]
```

---

### 1️⃣1️⃣ Change datatype to float

```python
a.astype(float)
```

---

### 1️⃣2️⃣ Find max value

```python
np.max(a)
```

---

### 1️⃣3️⃣ Find mean

```python
np.mean(a)
```

---

### 1️⃣4️⃣ Create identity matrix

```python
np.eye(3)
```

---

### 1️⃣5️⃣ Count elements

```python
a.size
```

---

# ⚡ Intermediate Level (16–35)

### 1️⃣6️⃣ Reshape 1D → 2D

```python
np.arange(12).reshape(3,4)
```

---

### 1️⃣7️⃣ Flatten array

```python
a.flatten()
```

---

### 1️⃣8️⃣ Element-wise addition

```python
a + b
```

---

### 1️⃣9️⃣ Element-wise multiplication

```python
a * b
```

---

### 2️⃣0️⃣ Matrix multiplication

```python
np.dot(a, b)
```

---

### 2️⃣1️⃣ Boolean indexing (>50)

```python
a[a > 50]
```

---

### 2️⃣2️⃣ Replace values < 40 with 0

```python
a[a < 40] = 0
```

---

### 2️⃣3️⃣ Sum column-wise

```python
np.sum(a, axis=0)
```

---

### 2️⃣4️⃣ Sum row-wise

```python
np.sum(a, axis=1)
```

---

### 2️⃣5️⃣ Sort array

```python
np.sort(a)
```

---

### 2️⃣6️⃣ Find index of max value

```python
np.argmax(a)
```

---

### 2️⃣7️⃣ Stack vertically

```python
np.vstack((a,b))
```

---

### 2️⃣8️⃣ Stack horizontally

```python
np.hstack((a,b))
```

---

### 2️⃣9️⃣ Split array into 2 parts

```python
np.split(a, 2)
```

---

### 3️⃣0️⃣ Unique elements

```python
np.unique(a)
```

---

### 3️⃣1️⃣ Standard deviation

```python
np.std(a)
```

---

### 3️⃣2️⃣ Variance

```python
np.var(a)
```

---

### 3️⃣3️⃣ Transpose matrix

```python
a.T
```

---

### 3️⃣4️⃣ Generate random integers

```python
np.random.randint(1,100,(3,3))
```

---

### 3️⃣5️⃣ Set random seed

```python
np.random.seed(42)
```

---

# 🚀 Advanced / ML Level (36–50)

### 3️⃣6️⃣ Normalize array (0–1)

```python
(a - a.min()) / (a.max() - a.min())
```

---

### 3️⃣7️⃣ Compute Euclidean distance

```python
np.sqrt(np.sum((a-b)**2))
```

---

### 3️⃣8️⃣ Convert 2D → column vector

```python
a.reshape(-1,1)
```

---

### 3️⃣9️⃣ One-hot encoding

```python
np.eye(3)[[0,1,2]]
```

---

### 4️⃣0️⃣ Replace NaN with 0

```python
np.nan_to_num(a)
```

---

### 4️⃣1️⃣ Check NaN

```python
np.isnan(a)
```

---

### 4️⃣2️⃣ Clip values (0–100)

```python
np.clip(a, 0, 100)
```

---

### 4️⃣3️⃣ Find correlation coefficient

```python
np.corrcoef(a, b)
```

---

### 4️⃣4️⃣ Calculate cosine similarity

```python
np.dot(a,b)/(np.linalg.norm(a)*np.linalg.norm(b))
```

---

### 4️⃣5️⃣ Shuffle array

```python
np.random.shuffle(a)
```

---

### 4️⃣6️⃣ Count non-zero elements

```python
np.count_nonzero(a)
```

---

### 4️⃣7️⃣ Find diagonal elements

```python
np.diag(a)
```

---

### 4️⃣8️⃣ Create mask (>mean)

```python
a > a.mean()
```

---

### 4️⃣9️⃣ Convert boolean to int

```python
(a > 50).astype(int)
```

---

### 5️⃣0️⃣ Mini ML Prep (Feature + Label)

```python
X = np.array([[1,2],[3,4],[5,6]])
y = np.array([0,1,1])
```

---

# 🔥 How to Practice (Best Way)

1️⃣ Copy each problem  
2️⃣ Try without seeing solution  
3️⃣ Compare  
4️⃣ Modify values

---

# 📌 Want Next?

- 📄 **PDF Notes**
    
- ❓ **MCQ + Viva Questions**
    
- 🤖 **NumPy → ML (KNN / Linear Regression from scratch)**
    

বললেই শুরু করবো ✔️

------------

ভালো প্রশ্ন 👍  
**NumPy শেখার পর “আর কী জানা দরকার”**—এইটাই আসল turning point।

তুমি যেহেতু **Pandas, ML, CV project** করছো, তাই আমি **honest + practical roadmap** দিচ্ছি।

---

# ✅ NumPy শেষ করলে এখন যেগুলো জানা MUST

## 🔥 1️⃣ NumPy Advanced (Must for ML)

যেগুলো না জানলে ML কোডে আটকে যাবে:

- `vectorization` (loop বাদ দিয়ে কাজ)
    
- `where()` vs boolean indexing
    
- `einsum()` (advanced but powerful)
    
- `memory view vs copy`
    
- `performance comparison (loop vs numpy)`
    

📌 Example:

```python
np.where(a > 50, 1, 0)
```

---

## 🔥 2️⃣ Pandas (You already started – go deeper)

এখন NumPy + Pandas combine করতে হবে:

Must know:

- `loc vs iloc`
    
- `groupby`
    
- `merge / join`
    
- `apply vs vectorized ops`
    
- datetime handling
    
- missing value pipeline
    

👉 Real skill = **data cleaning + feature engineering**

---

## 🔥 3️⃣ Matplotlib + Seaborn (Data Visualization)

ML model বুঝাতে visualization লাগে।

Must know:

- line, bar, histogram
    
- boxplot (outlier)
    
- heatmap (correlation)
    

👉 Project + Viva = visualization required

---

## 🔥 4️⃣ Statistics (Very Important for ML)

এটা অনেকেই skip করে ❌

You must know:

- mean, median, mode
    
- variance, std
    
- probability basics
    
- correlation vs covariance
    
- normal distribution
    

👉 Model evaluation এখানেই depend করে

---

## 🔥 5️⃣ Machine Learning Core (Next Big Step)

এখন **NumPy knowledge directly কাজে লাগবে**:

Learn order:

1. Linear Regression (from scratch using NumPy)
    
2. Logistic Regression
    
3. KNN
    
4. K-Means
    
5. Evaluation metrics
    

📌 Example:

```python
y_pred = X.dot(w) + b
```

---

## 🔥 6️⃣ Scikit-learn (Industry Tool)

From scratch বোঝার পর:

- train_test_split
    
- StandardScaler
    
- model.fit(), predict()
    
- confusion matrix
    
- cross-validation
    

---

## 🔥 7️⃣ Computer Vision (Your Strong Area)

Since তুমি YOLO / CV নিয়ে কাজ করছো:

- NumPy image as array
    
- OpenCV
    
- image normalization
    
- bounding box operations
    
- batch processing
    

---

# 🧠 Smart Learning Path (For You)

```
NumPy ✔
↓
Pandas (Advanced)
↓
Statistics
↓
Matplotlib
↓
ML from Scratch (NumPy)
↓
scikit-learn
↓
CV / DL
```

---

# 🎯 Now I Recommend (Next Action)

তুমি এখন ready এইগুলোর জন্য 👇

### Option 1️⃣

📘 **NumPy → Linear Regression from Scratch**

### Option 2️⃣

📊 **Advanced Pandas (Real Dataset Cleaning Project)**

### Option 3️⃣

🤖 **ML Interview + Viva Preparation**

বল কোনটা আগে করবো—আমি step-by-step শুরু করে দেবো 💪

----
