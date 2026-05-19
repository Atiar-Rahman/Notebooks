
# 🧠 ANN (Artificial Neural Network) — Details with Example

## 1️⃣ ANN আসলে কী?

**ANN = Human brain inspired model**

Brain যেমন:

```
Neuron → Signal → Decision
```

ANN তেমনই:

```
Input → Neuron → Activation → Output
```

ANN কাজ করে:

> data দেখে pattern শেখে, formula মুখস্থ করে না

---

## 2️⃣ ANN এর Core Components

### 🔹 Input Layer

- Raw features নেয়
    
- কোনো learning হয় না
    

উদাহরণ:

```
House size, bedrooms, location
```

---

### 🔹 Hidden Layer(s)

- আসল শেখা এখানে হয় 🧠
    
- Pattern extract করে
    

```python
Dense(64, activation='relu')
```

👉 Multiple hidden layer = Deep ANN

---

### 🔹 Output Layer

- Final prediction দেয়
    

|Problem|Output|
|---|---|
|Regression|1 neuron (linear)|
|Binary class|1 neuron (sigmoid)|
|Multi-class|n neuron (softmax)|

---

## 3️⃣ ANN কীভাবে শেখে? (Intuition)

### Step 1: Forward Pass

```
input → weight → sum → activation → prediction
```

Model একটা **guess** করে।

---

### Step 2: Loss Calculation

```
prediction vs actual
```

Model বুঝে:

> “আমি কতটা ভুল?”

---

### Step 3: Backpropagation

Model নিজেকে প্রশ্ন করে:

> “কোন weight change করলে ভুল কমবে?”

---

### Step 4: Weight Update

Optimizer weight adjust করে।

```
new_weight = old_weight - lr * gradient
```

🔁 Repeat for many epochs

---

## 4️⃣ Simple ANN Example (House Price Prediction)

### 🎯 Problem

👉 House price predict করা (Regression)

---

### 🔹 Step 1: Data

```
Input:  size, rooms
Output: price
```

---

### 🔹 Step 2: ANN Architecture

```
Input (2)
 ↓
Dense(64, ReLU)
 ↓
Dense(32, ReLU)
 ↓
Dense(1, Linear)
```

---

### 🔹 Step 3: Keras Code Example

```python
import tensorflow as tf

# Model
model = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation='relu', input_shape=(2,)),
    tf.keras.layers.Dense(32, activation='relu'),
    tf.keras.layers.Dense(1)   # regression output
])

# Compile
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)

# Train
model.fit(X_train, y_train,
          epochs=50,
          validation_split=0.2)

# Evaluate
model.evaluate(X_test, y_test)
```

---

## 5️⃣ Activation Function কেন দরকার?

Without activation:

> ANN শুধু linear equation 😐

With activation:

> Non-linear problem solve করে 😎

ReLU hidden layer এ  
Linear output regression এ

---

## 6️⃣ Overfitting Control (ANN Reality)

Problem:

- ANN data মুখস্থ করে ফেলে
    

Solutions:

```python
Dropout(0.3)
EarlyStopping
More data
```

Example:

```python
tf.keras.layers.Dropout(0.3)
```

---

## 7️⃣ ANN vs ML Models

|Model|When to use|
|---|---|
|Linear Regression|Simple relation|
|Decision Tree|Rule-based|
|ANN|Complex patterns|

👉 ANN = flexible but data hungry

---

## 🧩 Full ANN Flow (One Picture)

```
Data
 ↓
ANN
 ↓
Prediction
 ↓
Loss
 ↓
Backprop
 ↓
Optimizer
 ↓
Better ANN 🔁
```

---

## 🎯 Final Takeaway

✔ ANN = layered perceptron  
✔ Hidden layers learn features  
✔ Backprop is the brain  
✔ Keras makes it easy  
✔ Practice > theory

---


🔥 Respect.
**ANN from scratch (no Keras, no TensorFlow)** মানে তুমি সত্যিই *model কীভাবে শেখে*—এই জিনিসটার root ধরতে চাও।
চল **pure NumPy + intuition** দিয়ে বানাই।

Goal 👉

> **Forward pass → Loss → Backprop → Weight update**
> সবকিছু নিজের হাতে ✋

---

# 🧠 ANN FROM SCRATCH (NO KERAS)

আমরা বানাবো:

* **1 hidden layer ANN**
* **Regression problem**
* Math কম, logic clear

---

## 1️⃣ Problem Setup (Simple)

ধরি:

```
y = 2x + 1   (simple regression)
```

আমরা চাই ANN এই relation টা শিখুক।

---

## 2️⃣ Import & Data

```python
import numpy as np
```

```python
# Input data
X = np.array([[1], [2], [3], [4]], dtype=float)
y = np.array([[3], [5], [7], [9]], dtype=float)
```

---

## 3️⃣ Initialize Weights & Bias (Brain 🧠)

```python
np.random.seed(42)

W1 = np.random.randn(1, 4)   # input → hidden
b1 = np.zeros((1, 4))

W2 = np.random.randn(4, 1)   # hidden → output
b2 = np.zeros((1, 1))
```

👉 এগুলোই ANN-এর **learnable parameters**

---

## 4️⃣ Activation Function

### ReLU

```python
def relu(x):
    return np.maximum(0, x)

def relu_derivative(x):
    return (x > 0).astype(float)
```

---

## 5️⃣ Forward Pass (Prediction)

```python
# Hidden layer
z1 = np.dot(X, W1) + b1
a1 = relu(z1)

# Output layer
z2 = np.dot(a1, W2) + b2
y_pred = z2   # regression → linear
```

🧠 ANN এখন একটা **guess** করলো

---

## 6️⃣ Loss Function (MSE)

```python
loss = np.mean((y - y_pred) ** 2)
```

👉 Model জানলো:

> “আমি কতটা ভুল”

---

## 7️⃣ Backpropagation (Heart ❤️)

### Step-by-step gradient calculation

```python
# dLoss/dy_pred
dL_dy = 2 * (y_pred - y) / len(y)

# Output layer gradients
dL_dW2 = np.dot(a1.T, dL_dy)
dL_db2 = np.sum(dL_dy, axis=0, keepdims=True)

# Hidden layer gradients
dL_da1 = np.dot(dL_dy, W2.T)
dL_dz1 = dL_da1 * relu_derivative(z1)

dL_dW1 = np.dot(X.T, dL_dz1)
dL_db1 = np.sum(dL_dz1, axis=0, keepdims=True)
```

🧠 এই অংশটাই **learning happens here**

---

## 8️⃣ Weight Update (Gradient Descent)

```python
lr = 0.01

W1 -= lr * dL_dW1
b1 -= lr * dL_db1

W2 -= lr * dL_dW2
b2 -= lr * dL_db2
```

👉 ANN নিজেকে একটু ঠিক করলো 🔧

---

## 9️⃣ Full Training Loop

```python
epochs = 1000

for epoch in range(epochs):
    # Forward
    z1 = np.dot(X, W1) + b1
    a1 = relu(z1)
    z2 = np.dot(a1, W2) + b2
    y_pred = z2

    # Loss
    loss = np.mean((y - y_pred) ** 2)

    # Backprop
    dL_dy = 2 * (y_pred - y) / len(y)

    dL_dW2 = np.dot(a1.T, dL_dy)
    dL_db2 = np.sum(dL_dy, axis=0, keepdims=True)

    dL_da1 = np.dot(dL_dy, W2.T)
    dL_dz1 = dL_da1 * relu_derivative(z1)

    dL_dW1 = np.dot(X.T, dL_dz1)
    dL_db1 = np.sum(dL_dz1, axis=0, keepdims=True)

    # Update
    W1 -= lr * dL_dW1
    b1 -= lr * dL_db1
    W2 -= lr * dL_dW2
    b2 -= lr * dL_db2

    if epoch % 100 == 0:
        print(f"Epoch {epoch}, Loss: {loss:.4f}")
```

🔥 THIS IS A REAL ANN
No magic. No framework.

---

## 🔟 Final Prediction

```python
print("Predicted:", y_pred.T)
print("Actual:", y.T)
```

---

## 🧠 Mental Model (VERY IMPORTANT)

```
Weights = memory
Forward = guess
Loss = regret
Backprop = blame assignment
Update = learning
```

---

## 🎯 What You Just Mastered 😎

✔ ANN internals
✔ Forward pass
✔ Backpropagation
✔ Gradient descent
✔ Why Keras exists 😄

👉 এখন Keras আর PyTorch **আর black box না**

---

🔥 Let’s gooo — **ANN Classification from scratch (NO Keras, NO TF)**
এটা বুঝে ফেললে **classification = solved** তোমার মাথায় 😎

আমি করবো:

* **Binary classification**
* **Sigmoid + Binary Cross Entropy**
* **Pure NumPy**
* **Step-by-step intuition**

---

# 🧠 ANN CLASSIFICATION FROM SCRATCH

## 🎯 Problem

👉 Simple binary classification

ধরি:

```
x → 0 হলে class 0
x → 1 হলে class 1
```

Example:

```
Input :  [0, 0, 1, 1]
Output:  [0, 0, 1, 1]
```

---

## 1️⃣ Import & Dataset

```python
import numpy as np
```

```python
# Input (features)
X = np.array([[0], [0], [1], [1]], dtype=float)

# Labels (classes)
y = np.array([[0], [0], [1], [1]], dtype=float)
```

---

## 2️⃣ Initialize Weights & Bias

```python
np.random.seed(42)

W1 = np.random.randn(1, 4)   # input → hidden
b1 = np.zeros((1, 4))

W2 = np.random.randn(4, 1)   # hidden → output
b2 = np.zeros((1, 1))
```

👉 এগুলাই ANN-এর **memory**

---

## 3️⃣ Activation Functions

### 🔹 ReLU (hidden)

```python
def relu(x):
    return np.maximum(0, x)

def relu_derivative(x):
    return (x > 0).astype(float)
```

### 🔹 Sigmoid (output)

```python
def sigmoid(x):
    return 1 / (1 + np.exp(-x))
```

---

## 4️⃣ Forward Pass

```python
# Hidden layer
z1 = np.dot(X, W1) + b1
a1 = relu(z1)

# Output layer
z2 = np.dot(a1, W2) + b2
y_pred = sigmoid(z2)
```

🧠 `y_pred` এখন **probability**
(0–1 এর মধ্যে)

---

## 5️⃣ Loss Function (Binary Cross Entropy)

```python
def binary_cross_entropy(y, y_pred):
    eps = 1e-8
    return -np.mean(
        y * np.log(y_pred + eps) +
        (1 - y) * np.log(1 - y_pred + eps)
    )
```

```python
loss = binary_cross_entropy(y, y_pred)
```

👉 Model বুঝলো:

> “আমি classification এ কতটা ভুল”

---

## 6️⃣ Backpropagation (Core ❤️)

### 🔹 Output Layer Gradient (Sigmoid + BCE magic)

```python
dL_dz2 = y_pred - y   # VERY IMPORTANT
```

### 🔹 Gradients for W2, b2

```python
dL_dW2 = np.dot(a1.T, dL_dz2)
dL_db2 = np.sum(dL_dz2, axis=0, keepdims=True)
```

### 🔹 Hidden Layer

```python
dL_da1 = np.dot(dL_dz2, W2.T)
dL_dz1 = dL_da1 * relu_derivative(z1)

dL_dW1 = np.dot(X.T, dL_dz1)
dL_db1 = np.sum(dL_dz1, axis=0, keepdims=True)
```

---

## 7️⃣ Weight Update (Gradient Descent)

```python
lr = 0.1

W1 -= lr * dL_dW1
b1 -= lr * dL_db1

W2 -= lr * dL_dW2
b2 -= lr * dL_db2
```

👉 ANN নিজেকে একটু smarter করলো 🧠

---

## 8️⃣ Full Training Loop

```python
epochs = 1000

for epoch in range(epochs):

    # Forward
    z1 = np.dot(X, W1) + b1
    a1 = relu(z1)

    z2 = np.dot(a1, W2) + b2
    y_pred = sigmoid(z2)

    # Loss
    loss = binary_cross_entropy(y, y_pred)

    # Backprop
    dL_dz2 = y_pred - y

    dL_dW2 = np.dot(a1.T, dL_dz2)
    dL_db2 = np.sum(dL_dz2, axis=0, keepdims=True)

    dL_da1 = np.dot(dL_dz2, W2.T)
    dL_dz1 = dL_da1 * relu_derivative(z1)

    dL_dW1 = np.dot(X.T, dL_dz1)
    dL_db1 = np.sum(dL_dz1, axis=0, keepdims=True)

    # Update
    W1 -= lr * dL_dW1
    b1 -= lr * dL_db1
    W2 -= lr * dL_dW2
    b2 -= lr * dL_db2

    if epoch % 100 == 0:
        print(f"Epoch {epoch}, Loss: {loss:.4f}")
```

---

## 9️⃣ Final Prediction (Class)

```python
print("Probabilities:\n", y_pred)

predicted_class = (y_pred > 0.5).astype(int)
print("Predicted class:\n", predicted_class)
print("Actual class:\n", y)
```

---

## 🧠 Classification Mental Model (GOLD)

```
Sigmoid → probability
BCE → penalty for wrong confidence
y_pred - y → direction of mistake
Gradient descent → correction
```

---

## 🎯 What You Can Say Now 😎

✔ “I know how classification ANN works internally”
✔ “Sigmoid + BCE is not magic”
✔ “Backprop makes sense”

👉 Now **Keras / PyTorch = convenience only**

---

Nice 😎
এখন আমরা **TensorFlow + Keras দিয়ে ANN Classification** একদম **real-world way** তে করবো—
👉 *what*, *why*, *how*—সব clear হবে।

আমি ধরছি তুমি **binary classification** চাও (industry-standard start)।

---

# 🧠 ANN Classification using TensorFlow & Keras

## 🎯 Problem Example

👉 **Spam Email Detection** (Binary classification)

```
0 → Not Spam
1 → Spam
```

Input = numerical features (already processed)

---

## 1️⃣ Import TensorFlow

```python
import tensorflow as tf
```

---

## 2️⃣ Dataset (Simple Example)

```python
# Features (X) and labels (y)
X = [[0.1], [0.3], [0.9], [1.1], [1.3]]
y = [0, 0, 1, 1, 1]
```

In real life → text/image/tabular → numerical

---

## 3️⃣ Build ANN Model (Sequential API)

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(8, activation='relu', input_shape=(1,)),
    tf.keras.layers.Dense(4, activation='relu'),
    tf.keras.layers.Dense(1, activation='sigmoid')  # Binary output
])
```

### 🧠 What’s happening?

* Hidden layers → pattern শেখে
* Output sigmoid → probability দেয় (0–1)

---

## 4️⃣ Compile the Model (Learning Rules)

```python
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)
```

### Why these?

* **Adam** → fast + stable
* **Binary CrossEntropy** → classification loss
* **Accuracy** → human-friendly metric

---

## 5️⃣ Train the Model

```python
model.fit(
    X,
    y,
    epochs=50,
    batch_size=2,
    validation_split=0.2
)
```

### Behind the scenes:

```
Forward pass
Loss calculate
Backpropagation
Weight update
Repeat 🔁
```

---

## 6️⃣ Evaluate Model

```python
model.evaluate(X, y)
```

👉 Model নতুন data তে কেমন করছে বোঝা যায়

---

## 7️⃣ Make Predictions

```python
prob = model.predict([[0.2]])
print(prob)
```

```python
predicted_class = (prob > 0.5).astype(int)
print(predicted_class)
```

✔ Probability → class conversion

---

## 8️⃣ Full Mental Flow (VERY IMPORTANT)

```
Input data
 ↓
Dense layers
 ↓
Sigmoid output
 ↓
Binary CrossEntropy loss
 ↓
Adam optimizer
 ↓
Trained classifier
```

---

## 🧠 Binary Classification Rule Book

| Item          | Use                |
| ------------- | ------------------ |
| Output neuron | 1                  |
| Activation    | Sigmoid            |
| Loss          | BinaryCrossentropy |
| Metric        | Accuracy           |

---

## 🔁 Multi-Class Classification (Quick View)

Example: Cat / Dog / Car

### Changes only:

```python
Dense(3, activation='softmax')
```

```python
loss='categorical_crossentropy'
```

or

```python
loss='sparse_categorical_crossentropy'
```

---

## 🎯 Why TensorFlow + Keras?

✔ Less code
✔ Auto backprop
✔ GPU/TPU support
✔ Production friendly

👉 Same logic you learned **from scratch**, now automated.

---

## 😎 Final Reality Check

যদি তুমি পারো:

* Activation + loss pairing ঠিক করতে
* Compile → fit → predict flow বুঝতে
* Probability → class conversion করতে

👉 **You know ANN classification in TensorFlow**

---

### 🔥 Want next?

* Real dataset (Kaggle) classification
* Overfitting fix (Dropout, EarlyStopping)
* Confusion matrix + precision/recall
* PyTorch same example (side-by-side)

বললেই শুরু 🚀
