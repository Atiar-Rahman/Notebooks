 **Optimizers in Deep Learning (TensorFlow/Keras)** — the heart of training.

---

# 🔹 What is an Optimizer?

- An **optimizer** is an algorithm that **updates weights & biases** of your neural network to minimize the **loss function**.
    
- It decides **how fast and in what direction** the model learns.
    

👉 Without optimizers, the model would never improve.

---

# 🔹 Core Idea: Gradient Descent

Training uses **Gradient Descent**:

$θ=θ−η⋅∇L$

- θ = model parameters (weights, biases)
    
- η = learning rate
    
- ∇L(θ) = gradient of loss
    

---

# 🔹 Types of Optimizers

## 1. **Gradient Descent Variants**

### (a) **Batch Gradient Descent**

- Uses **all training data** in one step.
    
- Very slow for large datasets.
    

### (b) **Stochastic Gradient Descent (SGD)**

- Updates parameters **for each sample**.
    
- Faster but noisy.
    

### (c) **Mini-batch Gradient Descent**

- Uses **small batches of data**.
    
- Balanced approach (commonly used).
    

---

## 2. **Popular Optimizers in TensorFlow/Keras**

### 🔸 **SGD (Stochastic Gradient Descent)**

```python
optimizer = tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9)
```

- Updates weights step by step.
    
- `momentum` helps move faster in right direction.
    
- Works well but may be slow.
    

---

### 🔸 **Momentum**

- Variant of SGD with memory of past gradients.
    
- Helps escape local minima.
    

$vt=γvt−1+η∇L$

---

### 🔸 **Adagrad**

```python
optimizer = tf.keras.optimizers.Adagrad(learning_rate=0.01)
```

- Adjusts learning rate **for each parameter**.
    
- Good for sparse data (like text).
    
- Problem: learning rate decreases too much over time.
    

---

### 🔸 **RMSProp**

```python
optimizer = tf.keras.optimizers.RMSprop(learning_rate=0.001, rho=0.9)
```

- Fixes Adagrad’s problem by using moving averages.
    
- Works well in RNNs and non-stationary problems.
    

---

### 🔸 **Adam (Most Popular)**

```python
optimizer = tf.keras.optimizers.Adam(learning_rate=0.001, beta_1=0.9, beta_2=0.999)
```

- Combines **Momentum + RMSProp**.
    
- Adapts learning rates & keeps past momentum.
    
- Default choice in most deep learning projects.
    

---

### 🔸 **Adamax**

- Variant of Adam, works better in some cases with large gradients.
    

---

### 🔸 **Nadam**

- Adam + Nesterov Momentum.
    
- Sometimes converges faster.
    

---

# 🔹 Summary Table

|Optimizer|Best For|Notes|
|---|---|---|
|**SGD**|Simple tasks, small models|Slow, needs tuning|
|**SGD + Momentum**|Faster convergence|Avoids oscillations|
|**Adagrad**|Sparse data (text/NLP)|Learning rate shrinks too much|
|**RMSProp**|RNNs, time series|Handles non-stationary data|
|**Adam**|General-purpose (default)|Fast, widely used|
|**Adamax**|Large gradients|Variant of Adam|
|**Nadam**|Complex deep nets|Adam + Nesterov|

---

# 🔹 Example in TensorFlow

```python
import tensorflow as tf
from tensorflow import keras

model = keras.Sequential([
    keras.layers.Dense(16, activation='relu'),
    keras.layers.Dense(1, activation='sigmoid')
])

# Try different optimizers
optimizer = tf.keras.optimizers.Adam(learning_rate=0.001)

model.compile(optimizer=optimizer,
              loss='binary_crossentropy',
              metrics=['accuracy'])
```

---

⚡ **In short:**  
Optimizers = algorithms that update weights to minimize loss.  
👉 **Adam** is the most commonly used, but sometimes **SGD with momentum** or **RMSProp** can perform better depending on the task.

---

## Epoch

1 epoch means 1 full training cycle on the dataset. once every sample in the dataset is seen then we start the next epoch

**how optimization works in deep learning** in a simple, step-by-step way.

---

# 🔹 What is Optimization in Deep Learning?

- **Optimization** = the process of **finding the best weights and biases** to minimize the loss function.
    
- The goal is:
    

$minimize L(θ)where θ=weights and biases$

---

# 🔹 Step 1: Forward Pass

1. Input data is fed into the network.
    
2. Network computes **predictions** using current weights & biases.
    

$y^=f(x;θ)$

3. Compute **loss**:
    

$L=Loss(y^,y)$

---

# 🔹 Step 2: Compute Gradients (Backward Pass)

- Use **backpropagation** to calculate **gradients** of the loss w.r.t each parameter:
    

$∂L∂wi,∂L∂bi\frac{\partial L}{\partial w_i}, \quad \frac{\partial L}{\partial b_i}$

- This tells us **how much each weight/bias contributes to the loss**.
    

---

# 🔹 Step 3: Update Parameters (Optimizer Step)

- The optimizer updates weights using gradients:
    

$θ=θ−η⋅∇θL$

Where:

- η\eta = learning rate (step size)
    
- ∇θL\nabla_\theta L = gradient of loss
    

Different optimizers modify this step:

|Optimizer|How it updates|
|---|---|
|**SGD**|θ = θ - η * gradient|
|**Momentum**|Uses previous gradient’s direction to speed up|
|**RMSProp**|Uses moving average of squared gradients to adjust learning rate|
|**Adam**|Combines momentum + RMSProp for adaptive learning|

---

# 🔹 Step 4: Repeat

- Repeat **forward pass → compute loss → backward pass → update parameters** for multiple iterations (epochs) until:
    
    - Loss stops decreasing significantly, or
        
    - Maximum epochs reached.
        

This iterative process **gradually “pushes” the weights to the optimal values**.

---

# 🔹 Visualization Analogy

Imagine trying to **find the lowest point in a valley** while blindfolded:

- You feel the slope under your feet (gradient).
    
- Take a step in the downward direction (update weights).
    
- Optimizer decides **how big each step should be** and sometimes **looks at previous steps** to move faster and avoid bumps.
    

---

# 🔹 TensorFlow Example (Manual Gradient Step)

```python
import tensorflow as tf

# Simple linear model: y = wx + b
w = tf.Variable(0.5)
b = tf.Variable(-0.5)
x = tf.constant([1.0, 2.0, 3.0])
y_true = tf.constant([1.0, 2.0, 3.0])

learning_rate = 0.1

for i in range(100):
    with tf.GradientTape() as tape:
        y_pred = w * x + b
        loss = tf.reduce_mean((y_true - y_pred)**2)
    
    # Compute gradients
    dw, db = tape.gradient(loss, [w, b])
    
    # Update parameters manually
    w.assign_sub(learning_rate * dw)
    b.assign_sub(learning_rate * db)
    
print(f"Trained weight: {w.numpy()}, bias: {b.numpy()}")
```

✅ This shows **how optimization iteratively updates parameters** to minimize loss.

---

⚡ **In short:**

1. Forward pass → compute predictions and loss
    
2. Backward pass → compute gradients
    
3. Update weights using optimizer
    
4. Repeat until convergence
    

---

