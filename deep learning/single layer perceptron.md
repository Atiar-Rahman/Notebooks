
# 🔹 What is a Single Layer Perceptron?

- The **simplest type of neural network**.
    
- Consists of only **one layer of neurons** (no hidden layers).
    
- Takes inputs → applies weights & bias → passes through an **activation function** → gives output.
    

👉 Think of it as a **linear classifier**.

---

# 🔹 Structure

$y=f(∑(wi​⋅xi​)+b)$

Where:

- xix_i = input features
    
- wiw_i = weights
    
- bb = bias
    
- f(⋅) = activation function (e.g., step, sigmoid, ReLU)
    

---

# 🔹 Steps of a Perceptron

1. **Input** → values/features (e.g., x1,x2x_1, x_2)
    
2. **Weighted Sum** → multiply inputs by weights & add bias
    
    `z=w1x1+w2x2+b`
1. **Activation Function** → apply function to decide output
    
    - Step function → for binary classification
        
    - Sigmoid/Softmax → for probabilities
        
2. **Output** → final prediction (e.g., class 0 or 1)
    

---

# 🔹 Example (Binary Classification)

Suppose:

- Inputs: x1=1,x2=0x_1=1, x_2=0
    
- Weights: w1=0.6,w2=0.4w_1=0.6, w_2=0.4
    
- Bias: b=−0.2b=-0.2
    
- Activation: Step function
    

Step 1: Weighted sum

`z=(0.6)(1)+(0.4)(0)−0.2=0.4z = (0.6)(1) + (0.4)(0) - 0.2 = 0.4`

Step 2: Apply activation (Step: output 1 if z>0 else 0)

y=1

✅ Prediction = Class 1

---

# 🔹 Code Example in TensorFlow/Keras

```python
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras import layers

# Simple dataset (XOR won’t work, use linearly separable)
X = [[0,0],[0,1],[1,0],[1,1]]
y = [0, 0, 0, 1]   # AND logic

# Build single layer perceptron
model = keras.Sequential([
    layers.Dense(1, activation='sigmoid', input_shape=(2,))
])

# Compile
model.compile(optimizer='sgd', loss='binary_crossentropy', metrics=['accuracy'])

# Train
model.fit(X, y, epochs=500, verbose=0)

# Test
print(model.predict([[1,1]]))   # 👉 Should be close to 1
print(model.predict([[0,1]]))   # 👉 Should be close to 0
```

---

# 🔹 Limitations of Single Layer Perceptron

- Can only solve **linearly separable problems** (like AND, OR).
    
- Cannot solve problems like **XOR** (requires multiple layers → MLP).
    

---

⚡ **In short**:  
A **Single Layer Perceptron** is the building block of neural networks. It takes inputs, applies weights & bias, passes through an activation function, and produces output.

---
## What is weight

weight is just used to handle vanishing gradients or exploring gradients(vectors)

 error = n(d-y)x
  Higher error value = poor model performance
  low error value = higher model performance
---
  
  erfect 👍 Let’s go step by step into **Loss Functions in Deep Learning**.  
Loss functions are one of the most important concepts because they **measure how well the model is learning**.

---

# 🔹 What is a Loss Function?

- A **loss function** tells us **how far the predicted output is from the true output**.
    
- During training, the model tries to **minimize this loss** (using optimization algorithms like Gradient Descent).
    

👉 **Smaller loss = better model.**

---

# 🔹 Types of Loss Functions

We can divide them based on the **task**:

---

## 1. **Regression Loss Functions** (for predicting numbers)

📌 Used when the output is **continuous** (e.g., predicting house price, temperature).

### (a) **Mean Squared Error (MSE)**

$L=1n∑i=1n(yi−y^i)2$

- Punishes large errors more (because of squaring).
    
- Commonly used in regression.
    
- Sensitive to outliers.
    

---

### (b) **Mean Absolute Error (MAE)**

L=1n∑i=1n∣yi−y^i∣L = \frac{1}{n} \sum_{i=1}^n |y_i - \hat{y}_i|

- Measures average absolute difference.
    
- More robust to outliers than MSE.
    

---

### (c) **Huber Loss**

$L={21​(y−y^​)2δ⋅∣y−y^​∣−21​δ2​if ∣y−y^​∣≤δotherwise​$

- Combination of MSE & MAE.
    
- Less sensitive to outliers than MSE.
    

---

## 2. **Classification Loss Functions** (for predicting classes)

📌 Used when the output is **categorical** (e.g., cat vs dog, spam vs not spam).

### (a) **Binary Cross-Entropy (Log Loss)**

$L=−1/n∑i=1n[yilog⁡(y^i)+(1−yi)log⁡(1−y^i)$

- Used for **binary classification** (0 or 1).
    
- Works with **sigmoid activation**.
    

---

### (b) **Categorical Cross-Entropy**

$L=−∑i=1Cyilog⁡(y^i)L = -\sum_{i=1}^C y_i \log(\hat{y}_i)$

- Used for **multi-class classification**.
    
- Works with **softmax activation**.
    

---

### (c) **Sparse Categorical Cross-Entropy**

- Same as categorical, but **labels are integers (0,1,2,…)** instead of one-hot vectors.
    

---

### (d) **Hinge Loss**

$L=max⁡(0,1−y⋅y^)L = \max(0, 1 - y \cdot \hat{y})$

- Used for **SVMs** (Support Vector Machines).
    
- Works well when margin-based classification is needed.
    

---

## 3. **Ranking / Special Loss Functions**

📌 Used for advanced tasks like ranking, embeddings, or GANs.

- **Contrastive Loss** → used in Siamese networks (face verification).
    
- **Triplet Loss** → ensures positive examples are closer than negative ones (used in FaceNet).
    
- **KL Divergence** → measures difference between probability distributions.
    
- **Hinge Embedding Loss** → used for embeddings and similarity learning.
    

---

## 4. **Loss Functions in GANs**

- **Generator Loss** → how well generator fools discriminator.
    
- **Discriminator Loss** → how well discriminator detects fake vs real.
    

---

# 🔹 Choosing the Right Loss Function

|Problem Type|Common Loss Function|
|---|---|
|Regression (continuous)|MSE, MAE, Huber|
|Binary classification|Binary Cross-Entropy|
|Multi-class classification|Categorical Cross-Entropy|
|Imbalanced classification|Focal Loss|
|Embeddings / similarity|Contrastive, Triplet|
|Generative models (GANs)|GAN-specific losses|

---

# 🔹 Example in TensorFlow/Keras

```python
import tensorflow as tf

# Regression
mse = tf.keras.losses.MeanSquaredError()

# Binary classification
bce = tf.keras.losses.BinaryCrossentropy()

# Multi-class classification
cce = tf.keras.losses.CategoricalCrossentropy()
```

---

# ⚡ Summary

- **Regression** → MSE, MAE, Huber
    
- **Classification** → Cross-Entropy (binary/multi-class), Hinge
    
- **Advanced tasks** → Contrastive, Triplet, KL Divergence, Focal Loss
    

---

