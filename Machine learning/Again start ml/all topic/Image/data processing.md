
Data process pipeline

---


Perfect! Let’s create a **complete preprocessing pipeline** for your phone dataset step by step. This will handle:

1. Missing values
    
2. Removing duplicates
    
3. Processing categorical data
    
4. Extracting numeric features from `specs`
    
5. Normalizing numeric features
    
6. Splitting into **X (features)** and **y (target)**
    

---

```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder, MinMaxScaler

# -------------------------------
# 1. Load dataset
# -------------------------------
df = pd.read_csv("phones.csv")

# -------------------------------
# 2. Remove duplicates
# -------------------------------
df.drop_duplicates(inplace=True)

# -------------------------------
# 3. Handle missing values
# -------------------------------
# Numeric column: price
df['price'] = df['price'].fillna(df['price'].median())

# Text columns: phone_brand, phone_model
df['phone_brand'] = df['phone_brand'].fillna('Unknown')
df['phone_model'] = df['phone_model'].fillna('Unknown')

# Specs column
df['specs'] = df['specs'].fillna('RAM:0GB;Storage:0GB;Battery:0mAh')

# -------------------------------
# 4. Extract numeric features from specs
# -------------------------------
# Assuming specs format: "RAM:4GB;Storage:64GB;Battery:4000mAh"
specs_df = df['specs'].str.split(';', expand=True)
specs_df.columns = ['RAM', 'Storage', 'Battery']

# Extract numbers only
df['RAM'] = specs_df['RAM'].str.extract('(\d+)').astype(float)
df['Storage'] = specs_df['Storage'].str.extract('(\d+)').astype(float)
df['Battery'] = specs_df['Battery'].str.extract('(\d+)').astype(float)

# Drop original specs column
df.drop('specs', axis=1, inplace=True)

# -------------------------------
# 5. Encode categorical data
# -------------------------------
le_brand = LabelEncoder()
df['phone_brand_enc'] = le_brand.fit_transform(df['phone_brand'])

le_model = LabelEncoder()
df['phone_model_enc'] = le_model.fit_transform(df['phone_model'])

# Drop original categorical columns
df.drop(['phone_brand', 'phone_model'], axis=1, inplace=True)

# -------------------------------
# 6. Split into X and y
# -------------------------------
X = df.drop('price', axis=1)  # features
y = df['price']               # target

# -------------------------------
# 7. Normalize numeric features
# -------------------------------
numeric_cols = X.select_dtypes(include=['int64', 'float64']).columns
scaler = MinMaxScaler()
X[numeric_cols] = scaler.fit_transform(X[numeric_cols])

# -------------------------------
# 8. Check final dataset
# -------------------------------
print("Features (X):")
print(X.head())
print("\nTarget (y):")
print(y.head())
```

---

### ✅ **What this pipeline does**

- Fills missing values in numeric & categorical columns.
    
- Removes duplicates.
    
- Extracts numeric values from `specs`.
    
- Encodes `phone_brand` and `phone_model`.
    
- Normalizes numeric features in **X**.
    
- Keeps **y (price)** unmodified (or you can normalize if needed for regression).
    

---

If you want, I can also make this into a **single reusable function** so you can just call `preprocess(df, target='price')` and get ready-to-use `X` and `y`.

Do you want me to do that?

---


ঠিক আছে 😄  
আমি আপনাকে দেখাই **Data Processing Step-by-Step** যেটা আপনি **Mini Project** এর জন্য ব্যবহার করতে পারেন। আমরা উদাহরণ হিসেবে **Titanic dataset (classification)** ব্যবহার করব।

---

# **Step 1: Load Dataset**

```python
import pandas as pd

# CSV file থেকে data load করা
data = pd.read_csv("titanic.csv")
print(data.head())
```

**Output:** আপনি দেখবেন columns যেমন `PassengerId`, `Survived`, `Pclass`, `Sex`, `Age` ইত্যাদি।

---

# **Step 2: Explore Data**

```python
print(data.info())       # Null value check
print(data.describe())   # Numerical summary
print(data.isnull().sum())  # Null value per column
```

- লক্ষ্য করুন কোন column-এ missing values আছে
    
- Numerical / Categorical columns আলাদা করা
    

---

# **Step 3: Handle Missing Values**

```python
# Age এর missing value median দিয়ে fill করা
data['Age'] = data['Age'].fillna(data['Age'].median())

# Cabin column অনেক missing, drop করে দেওয়া
data = data.drop(columns=['Cabin', 'Ticket', 'Name', 'PassengerId'])
```

---

# **Step 4: Encode Categorical Variables**

```python
# Sex column → 0,1
data['Sex'] = data['Sex'].map({'male':0, 'female':1})

# Embarked → One-hot encoding
data = pd.get_dummies(data, columns=['Embarked'], drop_first=True)
```

---

# **Step 5: Feature & Target Split**

```python
X = data.drop('Survived', axis=1)  # Features
y = data['Survived']               # Target
```

---

# **Step 6: Train-Test Split**

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

# **Step 7: Feature Scaling (Optional for some algorithms)**

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

---

# **Step 8: Mini Project Example (Logistic Regression)**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

model = LogisticRegression()
model.fit(X_train_scaled, y_train)
y_pred = model.predict(X_test_scaled)

print("Accuracy:", accuracy_score(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

### **Step 9: Summary of Data Processing Steps**

1. Load dataset → `pd.read_csv()`
    
2. Explore → check nulls, data types, summary
    
3. Handle missing values → fill/drop
    
4. Encode categorical → Label Encoding / One-hot Encoding
    
5. Split features & target → `X` and `y`
    
6. Train-test split → `train_test_split()`
    
7. Scale features (optional) → `StandardScaler`
    
8. Train model → predict → evaluate
    

---

💡 **Tip:**  
এই workflow **প্রায় সব mini project dataset** এর জন্য প্রযোজ্য। শুধু dataset অনুযায়ী columns adjust করতে হবে।

---

আপনি চাইলে আমি এই **data processing workflow** কে **all ML algorithms (LR, KNN, SVM, Decision Tree, Random Forest, Naive Bayes)** এর সাথে **ready-to-run mini-project template** বানিয়ে দিতে পারি।

আপনি কি আমি সেটা বানাই?

---
ঠিক আছে 😄  
আমি আপনাকে দেখাই **Data Processing Step-by-Step** যেটা আপনি **Mini Project** এর জন্য ব্যবহার করতে পারেন। আমরা উদাহরণ হিসেবে **Titanic dataset (classification)** ব্যবহার করব।

---

# **Step 1: Load Dataset**

```python
import pandas as pd

# CSV file থেকে data load করা
data = pd.read_csv("titanic.csv")
print(data.head())
```

**Output:** আপনি দেখবেন columns যেমন `PassengerId`, `Survived`, `Pclass`, `Sex`, `Age` ইত্যাদি।

---

# **Step 2: Explore Data**

```python
print(data.info())       # Null value check
print(data.describe())   # Numerical summary
print(data.isnull().sum())  # Null value per column
```

- লক্ষ্য করুন কোন column-এ missing values আছে
    
- Numerical / Categorical columns আলাদা করা
    

---

# **Step 3: Handle Missing Values**

```python
# Age এর missing value median দিয়ে fill করা
data['Age'] = data['Age'].fillna(data['Age'].median())

# Cabin column অনেক missing, drop করে দেওয়া
data = data.drop(columns=['Cabin', 'Ticket', 'Name', 'PassengerId'])
```

---

# **Step 4: Encode Categorical Variables**

```python
# Sex column → 0,1
data['Sex'] = data['Sex'].map({'male':0, 'female':1})

# Embarked → One-hot encoding
data = pd.get_dummies(data, columns=['Embarked'], drop_first=True)
```

---

# **Step 5: Feature & Target Split**

```python
X = data.drop('Survived', axis=1)  # Features
y = data['Survived']               # Target
```

---

# **Step 6: Train-Test Split**

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

# **Step 7: Feature Scaling (Optional for some algorithms)**

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

---

# **Step 8: Mini Project Example (Logistic Regression)**

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

model = LogisticRegression()
model.fit(X_train_scaled, y_train)
y_pred = model.predict(X_test_scaled)

print("Accuracy:", accuracy_score(y_test, y_pred))
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

---

### **Step 9: Summary of Data Processing Steps**

1. Load dataset → `pd.read_csv()`
    
2. Explore → check nulls, data types, summary
    
3. Handle missing values → fill/drop
    
4. Encode categorical → Label Encoding / One-hot Encoding
    
5. Split features & target → `X` and `y`
    
6. Train-test split → `train_test_split()`
    
7. Scale features (optional) → `StandardScaler`
    
8. Train model → predict → evaluate
    

---

💡 **Tip:**  
এই workflow **প্রায় সব mini project dataset** এর জন্য প্রযোজ্য। শুধু dataset অনুযায়ী columns adjust করতে হবে।

---

আপনি চাইলে আমি এই **data processing workflow** কে **all ML algorithms (LR, KNN, SVM, Decision Tree, Random Forest, Naive Bayes)** এর সাথে **ready-to-run mini-project template** বানিয়ে দিতে পারি।

আপনি কি আমি সেটা বানাই?

---
ঠিক আছে 😄  
আমি আপনাকে দেখাচ্ছি **Dataset Load + Visualization Techniques** step-by-step। আমরা উদাহরণ হিসেবে **Titanic / Iris / MNIST** যেকোন dataset ব্যবহার করতে পারি।

---

# **1️⃣ Load Dataset**

### **a) CSV dataset (Titanic)**

```python
import pandas as pd

data = pd.read_csv("titanic.csv")
print(data.head())       # প্রথম 5 row
print(data.info())       # Column info, null values
print(data.describe())   # Numerical summary
```

### **b) Built-in dataset (Iris)**

```python
from sklearn.datasets import load_iris

iris = load_iris()
X = iris.data
y = iris.target
print(X[:5])
print(y[:5])
print(iris.feature_names)
```

### **c) Image dataset (MNIST via sklearn)**

```python
from sklearn.datasets import fetch_openml
mnist = fetch_openml('mnist_784', version=1)
X = mnist.data
y = mnist.target
print(X.shape, y.shape)
```

---

# **2️⃣ Basic Visualization**

### **a) Numerical / Categorical Distribution**

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Target distribution (Titanic example)
sns.countplot(x='Survived', data=data)
plt.show()

# Age distribution
sns.histplot(data['Age'], bins=20, kde=True)
plt.show()
```

### **b) Pairplot / Scatterplot (Iris example)**

```python
import seaborn as sns
iris_df = pd.DataFrame(X, columns=iris.feature_names)
iris_df['target'] = y
sns.pairplot(iris_df, hue='target')
plt.show()
```

### **c) Correlation Heatmap**

```python
corr = data.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.show()
```

---

# **3️⃣ Image Visualization (MNIST / custom images)**

```python
import matplotlib.pyplot as plt

# Show first 5 MNIST images
for i in range(5):
    plt.imshow(X.iloc[i].values.reshape(28,28), cmap='gray')
    plt.title(f"Label: {y[i]}")
    plt.show()
```

### **For your custom video frames**

```python
import cv2
import matplotlib.pyplot as plt

frame = cv2.imread("frame1.jpg")  # read frame
frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
plt.imshow(frame_rgb)
plt.title("Sample Frame")
plt.show()
```

---

# **4️⃣ Tips for Visualization**

1. **Categorical Data:** `countplot`, `barplot`
    
2. **Numerical Data:** `histplot`, `boxplot`, `violinplot`
    
3. **Feature Relations:** `pairplot`, `scatterplot`
    
4. **Correlation:** `heatmap`
    
5. **Images / Frames:** OpenCV + Matplotlib
    

---

💡 **Mini Project Idea:**

- Load **Titanic dataset** → Visualize survival distribution by `Sex` and `Pclass`
    
- Load **Iris dataset** → Pairplot of features with class hue
    
- Load **MNIST dataset** → Show 10 random digits
    

---

আপনি চাইলে আমি একটি **ready-to-use Python notebook template** বানিয়ে দিতে পারি যেখানে **CSV, sklearn, images, video frames** সব ধরনের dataset load + visualize করা যাবে।

আপনি কি আমি সেটা বানাই?

---
ঠিক আছে 😄  
আমি দেখাচ্ছি **Custom Image Dataset Load + Preprocess + Visualize** step-by-step।

---

# **1️⃣ Directory Structure Assumption**

```
dataset/
   train/
       cats/
           cat1.jpg
           cat2.jpg
           ...
       dogs/
           dog1.jpg
           dog2.jpg
           ...
   test/
       cats/
       dogs/
```

- প্রতিটি class-এর আলাদা folder
    
- Images `.jpg` বা `.png`
    

---

# **2️⃣ Load Dataset using Python / OpenCV**

```python
import os
import cv2
import numpy as np

DATA_DIR = "dataset/train"
IMG_SIZE = 64  # Resize all images

images = []
labels = []

classes = os.listdir(DATA_DIR)
print("Classes:", classes)

for idx, cls in enumerate(classes):
    cls_folder = os.path.join(DATA_DIR, cls)
    for fname in os.listdir(cls_folder):
        if fname.endswith(".jpg") or fname.endswith(".png"):
            img_path = os.path.join(cls_folder, fname)
            img = cv2.imread(img_path)
            img = cv2.resize(img, (IMG_SIZE, IMG_SIZE))
            img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
            images.append(img)
            labels.append(idx)

X = np.array(images, dtype=np.float32)/255.0  # Normalize
y = np.array(labels)

print("Images shape:", X.shape)
print("Labels shape:", y.shape)
```

---

# **3️⃣ Visualize Some Images**

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10,5))
for i in range(6):
    plt.subplot(2,3,i+1)
    plt.imshow(X[i])
    plt.title(classes[y[i]])
    plt.axis('off')
plt.show()
```

---

# **4️⃣ Optional: Use `tf.keras.preprocessing.image_dataset_from_directory`**

```python
import tensorflow as tf

train_dataset = tf.keras.preprocessing.image_dataset_from_directory(
    "dataset/train",
    image_size=(IMG_SIZE, IMG_SIZE),
    batch_size=32,
    label_mode='int'
)

# Visualize batch
for images, labels in train_dataset.take(1):
    plt.figure(figsize=(10,5))
    for i in range(6):
        plt.subplot(2,3,i+1)
        plt.imshow(images[i].numpy().astype("uint8"))
        plt.title(classes[labels[i]])
        plt.axis('off')
    plt.show()
```

---

# **5️⃣ Tips for Custom Image Dataset**

1. Folder structure must follow **class-wise separation**
    
2. Resize images to **same size** before training
    
3. Normalize images (`0-1`)
    
4. Use `image_dataset_from_directory` for **direct TensorFlow pipeline**
    
5. For PyTorch, use `torchvision.datasets.ImageFolder` + `DataLoader`
    

---

💡 **Mini Project Idea:**

- Load 2-class custom dataset (e.g., Cats vs Dogs)
    
- Visualize 6–10 images per class
    
- Normalize & prepare for model training
    

---

আপনি চাইলে আমি **PyTorch + TensorFlow দুইটি version** এ **custom image dataset load + train-test split + dataloader ready** template বানিয়ে দিতে পারি।

আপনি কি আমি সেটা বানাই?

---
