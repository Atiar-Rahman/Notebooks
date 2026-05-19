### 🔥 TensorFlow শেখার clean roadmap (Bangla vibe)

#### 1️⃣ TensorFlow basics (foundation)

এগুলো clear না হলে পরের সব জটিল লাগবে

* TensorFlow কী, কেন use করি
* Tensor vs NumPy
* `tf.constant` vs `tf.Variable`
* Tensor shapes (scalar, vector, matrix)
* Basic ops: add, multiply, matmul
* Eager execution (default TF behavior)

👉 Goal: “Tensor দেখে ভয় না লাগা” 😄

---

#### 2️⃣ Neural Network fundamentals

* Perceptron কী
* Activation function (ReLU, Sigmoid, Softmax)
* Loss function (MSE, CrossEntropy)
* Optimizer (SGD, Adam)
* Forward + Backprop (conceptual, maths কম)

👉 Goal: model কীভাবে শেখে সেটা বুঝা

---

#### 3️⃣ Keras (TensorFlow-এর heart ❤️)

* `Sequential` vs `Functional API`
* Dense layer
* Model compile → fit → evaluate
* Overfitting & underfitting
* Validation data

👉 Goal: ২০–৩০ লাইনে model বানাতে পারা

---

#### 4️⃣ Practical ML projects (small but real)

* House price prediction
* Student result prediction
* Spam email classifier

👉 Goal: “ami model বানাতে পারি” confidence

---

#### 5️⃣ Deep Learning

* CNN basics
* Image classification (cats vs dogs / MNIST)
* Convolution, pooling (visual idea)

👉 Goal: image data নিয়ে কাজ শুরু

---

#### 6️⃣ Model tuning & saving

* Callbacks
* Early stopping
* Model save/load (`.h5`, SavedModel)

---

### ⏱️ Simple daily plan (chill version)

**Daily 1–1.5 hour enough**

* 30 min → concept
* 30 min → code
* 15 min → experiment / break model 😄

---

# Step1

---

## 🧠 Lesson 1: TensorFlow আসলে কী?

### 🔹 TensorFlow কী?

TensorFlow হলো **Google-এর বানানো machine learning & deep learning library**
এটা দিয়ে আমরা পারি:

* data → model → prediction
* image, text, number সবকিছু নিয়ে কাজ

👉 Simple ভাষায়:
**TensorFlow = math + data + GPU/CPU magic ✨**

---

## 🧱 Tensor মানে কী?

Tensor = **multi-dimensional data**

| Type        | Example         |
| ----------- | --------------- |
| Scalar (0D) | `5`             |
| Vector (1D) | `[1, 2, 3]`     |
| Matrix (2D) | `[[1,2],[3,4]]` |
| 3D+         | image, video    |

---

## 🛠️ First code (no fear 😄)

```python
import tensorflow as tf

# scalar
a = tf.constant(5)
print(a)

# vector
b = tf.constant([1, 2, 3])
print(b)

# matrix
c = tf.constant([[1, 2],
                 [3, 4]])
print(c)
```

👉 Output হবে:

* dtype (data type)
* shape (dimension)

---

## 🔍 Shape বুঝি

```python
print(a.shape)  # ()
print(b.shape)  # (3,)
print(c.shape)  # (2, 2)
```

📌 Rule:

* `()` → scalar
* `(n,)` → vector
* `(r, c)` → matrix

---

## ⚔️ Tensor vs NumPy (quick idea)

```python
import numpy as np

x_np = np.array([1, 2, 3])
x_tf = tf.constant([1, 2, 3])

print(type(x_np))
print(type(x_tf))
```

👉 Difference:

* NumPy → CPU only
* TensorFlow → CPU / GPU / TPU
* TensorFlow = training + backprop support

---

## 🧪 Tiny experiment (important)

```python
a = tf.constant(10)
b = tf.constant(20)

print(a + b)
print(a * b)
```

👉 No `.value`, no `.numpy()` yet — just trust it 😄

---

## 🧠 আজকের takeaway

* TensorFlow ≠ scary
* Tensor = data with shape
* `tf.constant()` দিয়ে fixed data বানাই

---

## ✅ Homework (easy)

1️⃣ TensorFlow install করা আছে তো?

```bash
pip show tensorflow
```

2️⃣ 3টা tensor বানাও:

* scalar
* vector (5 elements)
* matrix (3x3)

3️⃣ `.shape` print করো

---

# Step2

---

## 🧠 Neural Network Fundamentals (Beginner Friendly)

### 1️⃣ Perceptron কী?

**Perceptron = Neural Network-এর সবচেয়ে basic unit**

ভাবো এটা একটা **smart decision maker**।

**Input → Weight → Sum → Activation → Output**

উদাহরণ:

```
Input:  x1 = house_size
        x2 = bedrooms

Output: price_high (Yes / No)
```

Perceptron কী করে?

```
z = w1*x1 + w2*x2 + bias
output = activation(z)
```

👉 **Weights** = কোন input কতটা important
👉 **Bias** = decision boundary shift
👉 **Activation** = final decision নেবে

📌 একক perceptron শুধু **simple problem** solve পারে
📌 Multiple perceptron → **Neural Network**

---

### 2️⃣ Activation Function কী?

Activation function বলে দেয়:

> “এই neuron fire করবে নাকি করবে না?”

#### 🔹 ReLU (সবচেয়ে popular)

```
f(x) = max(0, x)
```

✔ Fast
✔ Deep network এ ভালো
❌ Negative value গেলে 0

👉 **Hidden layer এ default choice**

---

#### 🔹 Sigmoid

```
Output: 0 থেকে 1
```

✔ Probability বোঝাতে ভালো
❌ Gradient vanish problem

👉 **Binary classification output layer**

---

#### 🔹 Softmax

```
সব output মিলিয়ে = 1
```

✔ Multi-class probability

👉 **Multi-class classification output**

---

### 3️⃣ Loss Function কী?

Loss function বলে দেয়:

> “Model কতটা ভুল করলো?”

#### 🔹 MSE (Mean Squared Error)

```
(predicted - actual)²
```

✔ Regression problem
❌ Classification এ ভালো না

👉 **House price prediction**

---

#### 🔹 Cross Entropy Loss

✔ Classification problem
✔ Probability-based learning

👉 **Spam / Not spam**
👉 **Cat / Dog / Car**

📌 Rule:

```
Regression → MSE
Classification → CrossEntropy
```

---

### 4️⃣ Optimizer কী?

Optimizer হলো **teacher**
সে বলে:

> “Weight কীভাবে change করলে loss কমবে?”

#### 🔹 SGD (Stochastic Gradient Descent)

✔ Simple
❌ Slow
❌ Local minima তে আটকে যায়

---

#### 🔹 Adam (সবচেয়ে popular)

✔ Fast
✔ Smart learning rate
✔ Deep learning friendly

👉 **90% সময় Adam ব্যবহার করো**

---

### 5️⃣ Forward Pass + Backpropagation (Heart ❤️)

#### 🔹 Forward Pass

```
Input → Weight → Activation → Prediction
```

Model একটা guess করে।

---

#### 🔹 Backpropagation

```
Loss → Gradient → Weight Update
```

Model নিজেকে প্রশ্ন করে:

> “কোথায় ভুল করলাম?”

তারপর:

* কোন weight বেশি দোষী?
* কোনটা কম?

এই information দিয়ে:

```
new_weight = old_weight - learning_rate * gradient
```

📌 **এভাবেই model শেখে**

---

## 🧩 পুরো শেখার Flow (Very Important)

```
Input
 ↓
Forward pass
 ↓
Prediction
 ↓
Loss calculate
 ↓
Backpropagation
 ↓
Weight update (Optimizer)
 ↓
Repeat 🔁
```

👉 প্রতিটা epoch এ model একটু একটু smarter হয় 🧠

---

## 🎯 Goal Check: Model কীভাবে শেখে?

✔ Guess করে
✔ ভুল মাপে
✔ নিজেকে ঠিক করে
✔ বারবার করে
✔ একসময় ভালো করে 😄

---

# Step-3

---

## 🧠 3️⃣ Keras — TensorFlow-এর Heart ❤️

### 🔹 Keras আসলে কী?

**Keras = High-level API**
👉 Deep learning model বানানো সহজ করে
👉 TensorFlow এর উপর বসে কাজ করে

Think like:

> TensorFlow = Engine
> Keras = Steering + Dashboard

---

## 1️⃣ Sequential vs Functional API

### 🔸 Sequential API

👉 **Layer by layer, straight line model**

```
Input → Dense → Dense → Output
```

✔ Simple
✔ Beginner friendly
❌ Complex model (multiple input/output) করা যায় না

উদাহরণ (concept):

```python
model = Sequential([
    Dense(64),
    Dense(1)
])
```

📌 Use when:

* Single input
* Single output
* No branching

---

### 🔸 Functional API

👉 **Graph-based model** (advanced)

```
Input ──▶ Dense ──▶ Dense ──▶ Output
      └────────────▶ Dense ─┘
```

✔ Multiple input/output
✔ Skip connection
✔ Real-world models

Concept:

```python
inputs = Input(shape=(10,))
x = Dense(64)(inputs)
outputs = Dense(1)(x)
model = Model(inputs, outputs)
```

📌 Use when:

* Complex architecture
* Custom flow

👉 **Beginner হলে 90% Sequential enough**

---

## 2️⃣ Dense Layer কী?

**Dense = Fully Connected Layer**

মানে:

> আগের layer এর সব neuron → এই layer এর সব neuron

```python
Dense(units=64, activation='relu')
```

🔹 `units` → কত neuron
🔹 `activation` → decision function

📌 Rule of thumb:

* Hidden layer → `ReLU`
* Regression output → No activation / Linear
* Binary classification → `Sigmoid`
* Multi-class → `Softmax`

---

## 3️⃣ Model Lifecycle: compile → fit → evaluate

এইটা Keras-এর **holy trinity** 🛐

---

### 🔹 model.compile()

👉 Model কে বলো **কীভাবে শিখবে**

```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)
```

Includes:

* **Optimizer** → কীভাবে weight update
* **Loss** → কত ভুল
* **Metrics** → মানুষ বুঝার জন্য

---

### 🔹 model.fit()

👉 **Training শুরু**

```python
model.fit(X_train, y_train,
          epochs=50,
          validation_data=(X_val, y_val))
```

Model করে:

* Guess
* Loss calculate
* Backprop
* Repeat 🔁

---

### 🔹 model.evaluate()

👉 Final exam 🎓

```python
model.evaluate(X_test, y_test)
```

📌 Training না, শুধু performance check

---

## 4️⃣ Overfitting vs Underfitting

### 🔻 Underfitting

> Model খুব simple 😵

✔ Training loss high
✔ Validation loss high

Reason:

* Model ছোট
* Epoch কম
* Feature কম

---

### 🔺 Overfitting

> Model মুখস্থ করে ফেলছে 🤯

✔ Training loss low
❌ Validation loss high

Reason:

* Model অনেক complex
* Data কম
* Epoch বেশি

---

### 🧠 Ideal Model

```
Training loss ↓
Validation loss ↓
Gap ছোট
```

---

## 5️⃣ Validation Data কেন দরকার?

Validation data = **Mirror 🪞**

Model কে জিজ্ঞেস করে:

> “তুমি কি নতুন data তেও ভালো করছো?”

Without validation:

* Model নিজেকে deceive করতে পারে 😬

With validation:

* Real performance বোঝা যায়

Ways to give validation:

```python
validation_split=0.2
```

or

```python
validation_data=(X_val, y_val)
```

📌 **Test data কখনো training এ দিও না** ❌

---

## 🧩 Full Keras Flow (Mind Map)

```
Prepare data
 ↓
Build model (Sequential / Functional)
 ↓
Compile
 ↓
Fit (with validation)
 ↓
Evaluate
 ↓
Predict
```

---

## 🎯 Goal Check

✔ Keras কী
✔ Model কীভাবে বানাই
✔ Training কীভাবে চলে
✔ কেন model fail করে
✔ কিভাবে judge করি

🔥 তুমি এখন **real ML model train করার জন্য ready**

---

# Necessary Tensor API
---

# 🔥 TensorFlow Important APIs (Beginner → Pro map)

## 1️⃣ Core Tensor APIs (সবকিছুর base)

### 🔹 `tf.constant()`

➡️ **Fixed value tensor**

```python
x = tf.constant([1, 2, 3])
```

✅ Use when:

* data change হবে না
* input, label, config value

❌ Avoid when:

* training parameter (weight, bias)

---

### 🔹 `tf.Variable()`

➡️ **Trainable tensor (learn করে)**

```python
w = tf.Variable(2.0)
```

✅ Use when:

* model weight
* bias
* learning parameter

📌 **Training মানেই Variable**

---

### 🔹 Shape & dtype APIs

```python
x.shape
x.dtype
tf.shape(x)
```

👉 Model crash হলে ৮০% সময় shape issue 😅
এগুলো debug-এর best friend

---

## 2️⃣ Math & Ops APIs (ML = math 😄)

### 🔹 Basic ops

```python
tf.add(a, b)
tf.multiply(a, b)
tf.matmul(a, b)
```

📌 Matrix multiplication = neural network backbone

---

### 🔹 Reduction ops

```python
tf.reduce_sum(x)
tf.reduce_mean(x)
tf.reduce_max(x)
```

👉 Loss calculate করতে heavily use হয়

---

## 3️⃣ Random APIs (weight initialization)

```python
tf.random.normal(shape=(3, 3))
tf.random.uniform(shape=(3, 3))
```

📌 Neural network সবসময় random weight দিয়ে শুরু করে
না হলে learning হয় না

---

## 4️⃣ Neural Network APIs (`tf.nn`)

### 🔹 Activation functions

```python
tf.nn.relu(x)
tf.nn.sigmoid(x)
tf.nn.softmax(x)
```

🧠 Use:

* ReLU → hidden layer
* Softmax → classification output
* Sigmoid → binary output

---

### 🔹 Loss helpers

```python
tf.nn.softmax_cross_entropy_with_logits(labels, logits)
```

👉 Keras auto handle করে, but concept জানাটা জরুরি

---

## 5️⃣ Gradient & Training APIs (সবচেয়ে IMPORTANT 🔥)

### 🔥 `tf.GradientTape`

➡️ **Backprop magic**

```python
with tf.GradientTape() as tape:
    y = w * x
grad = tape.gradient(y, w)
```

🧠 This is the heart of training
Keras এটা internally করে

---

## 6️⃣ Keras High-Level APIs (Real-world use ❤️)

### 🔹 Layers

```python
tf.keras.layers.Dense(64, activation='relu')
tf.keras.layers.Conv2D(...)
tf.keras.layers.Flatten()
```

👉 Building blocks of model

---

### 🔹 Model

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32),
    tf.keras.layers.Dense(1)
])
```

or

```python
tf.keras.Model(inputs, outputs)
```

📌 90% time `Sequential`
📌 Complex model → `Functional API`

---

### 🔹 Compile

```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['accuracy']
)
```

👉 Model কে বলা:

* কীভাবে শিখবে
* কী দিয়ে ভুল মাপবে

---

### 🔹 Training

```python
model.fit(x_train, y_train, epochs=10)
```

🔥 This single line = forward + backprop + update

---

### 🔹 Evaluation & Prediction

```python
model.evaluate(x_test, y_test)
model.predict(x_new)
```

---

## 7️⃣ Dataset APIs (Large data handle)

```python
tf.data.Dataset.from_tensor_slices((x, y))
    .shuffle(100)
    .batch(32)
```

👉 Big dataset, video, image pipeline এখানেই

---

## 8️⃣ Model Save / Load APIs

```python
model.save("model.h5")
tf.keras.models.load_model("model.h5")
```

📌 Training costly → save mandatory

---

## 🧠 Mental Model (মাথায় রাখো)

```
Tensor → Variable → Ops
        ↓
     Layers
        ↓
     Model
        ↓
 Compile → Fit → Predict
```

---

## 🔥 Most IMPORTANT (exam + interview)

If তুমি শুধু এগুলো master করো:

* `tf.constant`
* `tf.Variable`
* `tf.keras.layers`
* `model.compile()`
* `model.fit()`
* `tf.data.Dataset`

👉 You are already **production-ready beginner** 😎

---

## 1️⃣ `tf.constant`

👉 **Fixed data** (change করা যাবে না)

```python
a = tf.constant([1, 2, 3])
```

🧠 Think:

* Input data
* Labels
* Static values

❌ Training সময় weight হিসেবে ব্যবহার করো না
✔ Safe, fast, simple

📌 Rule:

> Change দরকার নেই → `tf.constant`

---

## 2️⃣ `tf.Variable`

👉 **Trainable data** (change হয়)

```python
w = tf.Variable(0.5)
```

🧠 Think:

* Weights
* Bias
* Any learnable parameter

Optimizer এইগুলোকেই update করে 🔄

📌 Rule:

> Model যেটা শিখবে → `tf.Variable`

---

## 3️⃣ `tf.keras.layers`

👉 **Neural Network building blocks** 🧱

Most-used layers:

```python
Dense
Dropout
BatchNormalization
Flatten
```

Example:

```python
tf.keras.layers.Dense(64, activation='relu')
```

🧠 Each layer:

* Input নেয়
* Weight + bias রাখে
* Activation চালায়

📌 Truth:

> Model = layers এর chain

---

## 4️⃣ `model.compile()`

👉 **Learning strategy setup**

```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)
```

This decides:

* কীভাবে শিখবে (optimizer)
* কী ভুল (loss)
* কী দেখাবে (metrics)

❌ Compile না করলে training চলবে না

📌 Compile = “rules of the game”

---

## 5️⃣ `model.fit()`

👉 **Actual training happens here** 🔥

```python
model.fit(
    X_train,
    y_train,
    epochs=50,
    validation_split=0.2
)
```

Behind the scenes:

```
Forward pass
Loss calculate
Backprop
Weight update
Repeat 🔁
```

📌 Fit = model grows brain 🧠

---

## 6️⃣ `tf.data.Dataset`

👉 **Production-level data pipeline** 🚀

```python
dataset = tf.data.Dataset.from_tensor_slices((X, y))
dataset = dataset.shuffle(1000).batch(32)
```

Why important?
✔ Memory efficient
✔ Large dataset handle
✔ GPU/TPU friendly

🧠 Real-world rule:

> NumPy → learning
> tf.data → production

---

## 🧩 Everything Connected (Mental Model)

```
tf.constant  → input / labels
tf.Variable  → weights
layers       → structure
compile      → learning rules
fit          → training
Dataset      → scalable data feed
```

---

## 🎯 Final Reality Check 😎

যদি তুমি পারো:

* Custom dataset বানাতে
* Keras model build করতে
* Compile + fit ঠিকভাবে দিতে
* Overfitting ধরতে
* Model save/load করতে

👉 **You ARE a production-ready beginner**
No hype. Real skill 💯

---

# How much needed for tensor Flow `api` 

---

## 🤔 “আরও API জানতেই হবে?” — বাস্তব কথা

TensorFlow একটা **সমুদ্র 🌊**
কিন্তু তুমি **মাছ ধরতে শিখতে চাও**, সমুদ্র মাপতে না 😄

👉  **১০–১৫% API = ৮৫% real-world কাজ**

---

## ✅ Beginner–Intermediate হলে MUST know (non-negotiable)

এইগুলো জানলে তুমি confidently model বানাতে পারবা:

### 🔥 Core

* `tf.constant`
* `tf.Variable`
* `tf.shape`
* `tf.cast`
* `tf.reshape`

### 🔥 Math

* `tf.matmul`
* `tf.reduce_mean`
* `tf.reduce_sum`

### 🔥 Training

* `tf.GradientTape`
* `tf.optimizers.Adam`

### 🔥 Keras

* `tf.keras.layers.Dense`
* `tf.keras.Model / Sequential`
* `compile()`, `fit()`, `predict()`

### 🔥 Data

* `tf.data.Dataset`

👉 এগুলো = **TensorFlow survival kit** 🧰

---

## 🟡 Advanced কিন্তু এখনই না জানলেও চলবে

এইগুলো **project-specific**:

* `tf.function` (graph mode)
* `tf.distribute` (multi-GPU)
* `tf.keras.callbacks`
* `tf.image`
* `tf.io`
* `tf.saved_model`

👉 এগুলো তখনই শিখবে যখন দরকার পড়বে

---

## ❌ API যেগুলো জানার দরকারই নেই (এখন)

* Low-level C++ ops
* TPU-specific APIs
* Custom ops (unless researcher)

---

## 🧠 Pro mindset (এটা golden rule ⭐)

> **“API মুখস্থ করবো না — use-case বুঝবো”**

Google engineer রাও সব API মুখস্থ রাখে না
Docs + experience = mastery

---



# **TensorFlow বুঝে যাওয়ার turning point demo**। মন দিয়ে দেখো—এটার পর আর TF ভয়ের জিনিস থাকবে না।

---

# 🚀 Demo: `tf.Variable` vs `tf.constant` + Training (NO Keras)

আমরা করবো:

> **y = 2x** শিখানো একটা tiny model
> মানে model নিজেই `2` discover করবে 😎

---

## 1️⃣ Data (fixed → `tf.constant`)

```python
import tensorflow as tf

# input data
x = tf.constant([1.0, 2.0, 3.0, 4.0])
y_true = tf.constant([2.0, 4.0, 6.0, 8.0])
```

📌 Data change হবে না → `constant`

---

## 2️⃣ Model parameter (learnable → `tf.Variable`)

```python
w = tf.Variable(0.0)  # initial guess
```

📌 Weight শিখবে → **Variable MUST**

---

## 3️⃣ Loss function

```python
def loss_fn(y_true, y_pred):
    return tf.reduce_mean((y_true - y_pred) ** 2)
```

👉 MSE loss

---

## 4️⃣ Training step (🔥 core magic)

```python
optimizer = tf.optimizers.SGD(learning_rate=0.1)

for epoch in range(10):
    with tf.GradientTape() as tape:
        y_pred = w * x
        loss = loss_fn(y_true, y_pred)

    grad = tape.gradient(loss, w)
    optimizer.apply_gradients([(grad, w)])

    print(f"Epoch {epoch}: w={w.numpy():.4f}, loss={loss.numpy():.4f}")
```

---

## 🔍 কী হচ্ছে ভিতরে? (VERY IMPORTANT)

1️⃣ `GradientTape` সব math record করে
2️⃣ loss অনুযায়ী gradient বের করে
3️⃣ optimizer weight update করে

📌 **এইটাই training**
Keras এটাকে শুধু সুন্দর wrapper দিয়েছে

---

## ✅ Expected Output

```
Epoch 0: w=1.2000, loss=18.0000
Epoch 3: w=1.9680, loss=0.0512
Epoch 9: w=1.9999, loss=0.0000
```

🎉 Model নিজেই শিখে ফেললো `w ≈ 2`

---

## ❌ যদি `tf.constant` দিতাম?

```python
w = tf.constant(0.0)
```

❌ Error:

> Cannot apply gradients to a Tensor

📌 Lesson:

> **Trainable → Variable
> Fixed → Constant**

---

## 🧠 Mental click moment 💡

```
Variable → GradientTape → Optimizer
          ↓
        Learning
```

এই triangle বুঝলে
👉 **TensorFlow half mastered** 😎

---

## 🧪 Small challenge (try this)

* Epoch = 50 করো
* Learning rate = 0.01
* Print only every 5 epochs

---
# Now We **real linear regression** করবো —
👉 **y = w·x + b**
👉 2টা parameter (weight + bias)
👉 একদম **from scratch, NO Keras**

এইটা বুঝলে তুমি officially **ML inside TensorFlow** ঢুকে গেলে 🧠🚀

---

# 🚀 Demo: Linear Regression (y = wx + b)

## 1️⃣ Data (fixed → `tf.constant`)

```python
import tensorflow as tf

# y = 3x + 1 (true relation)
x = tf.constant([1.0, 2.0, 3.0, 4.0])
y_true = tf.constant([4.0, 7.0, 10.0, 13.0])
```

---

## 2️⃣ Model parameters (learnable → `tf.Variable`)

```python
w = tf.Variable(0.0)   # weight
b = tf.Variable(0.0)   # bias
```

📌 দুটোই শিখবে → Variable

---

## 3️⃣ Prediction function

```python
def predict(x):
    return w * x + b
```

---

## 4️⃣ Loss function (MSE)

```python
def loss_fn(y_true, y_pred):
    return tf.reduce_mean((y_true - y_pred) ** 2)
```

---

## 5️⃣ Training loop (🔥 heart of ML)

```python
optimizer = tf.optimizers.SGD(learning_rate=0.1)

for epoch in range(20):
    with tf.GradientTape() as tape:
        y_pred = predict(x)
        loss = loss_fn(y_true, y_pred)

    dw, db = tape.gradient(loss, [w, b])
    optimizer.apply_gradients([(dw, w), (db, b)])

    print(
        f"Epoch {epoch:02d} | "
        f"w={w.numpy():.3f}, b={b.numpy():.3f}, "
        f"loss={loss.numpy():.4f}"
    )
```

---

## ✅ Expected learning

শেষে প্রায় এমন হবে:

```
w ≈ 3.0
b ≈ 1.0
loss ≈ 0
```

🎯 Model নিজেই relation discover করেছে

---

## 🔍 ভিতরে কী শিখলা?

* Multiple `tf.Variable` handle
* `tape.gradient(loss, [w, b])`
* Optimizer multiple params update

📌 Exactly এই জিনিস Keras auto করে

---

## ❗ Common mistakes (important)

❌ Forget `tf.Variable`
❌ Shape mismatch
❌ Learning rate too high (loss = NaN)

---

## 🧠 Visualization in head

```
x ──► ( * w ) ──► + b ──► y_pred
           ↑        ↑
        learn     learn
```

---

## 🧪 Mini challenge (strongly recommended)

1️⃣ Change true equation to `y = 5x - 2`
2️⃣ Change learning rate → `0.01`
3️⃣ Epoch → `100`
4️⃣ Observe convergence speed

---
# Now We **Multi Linear Regression** করবো —
মানে 👉 **multiple input features**
👉 formula:

$y = w_1x_1 + w_2x_2 + \dots + w_nx_n + b$


একদম **from scratch (NO Keras)**, pure TensorFlow 💪

---

# 🚀 Demo: Multi Linear Regression (from scratch)

ধরি:

* `x1` = hours studied
* `x2` = hours slept
* target = exam score

True equation (unknown to model):

$y = 2x_1 + 3x_2 + 1$

---

## 1️⃣ Dataset (fixed → `tf.constant`)

```python
import tensorflow as tf

# shape: (samples, features)
X = tf.constant([
    [1.0, 2.0],
    [2.0, 1.0],
    [3.0, 4.0],
    [4.0, 3.0]
])

y_true = tf.constant([
    9.0,   # 2*1 + 3*2 + 1
    8.0,   # 2*2 + 3*1 + 1
    19.0,  # 2*3 + 3*4 + 1
    18.0   # 2*4 + 3*3 + 1
])
```

📌 **Shape check**

* `X` → `(4, 2)`
* `y` → `(4,)`

---

## 2️⃣ Model parameters (learnable)

```python
w = tf.Variable(tf.random.normal(shape=(2,)))  # weights
b = tf.Variable(0.0)                           # bias
```

📌 2 features → 2 weights

---

## 3️⃣ Prediction (matrix math 🔥)

```python
def predict(X):
    return tf.reduce_sum(X * w, axis=1) + b
```

🧠 Equivalent to:

```python
X @ w + b
```

---

## 4️⃣ Loss function

```python
def loss_fn(y_true, y_pred):
    return tf.reduce_mean((y_true - y_pred) ** 2)
```

---

## 5️⃣ Training loop

```python
optimizer = tf.optimizers.SGD(learning_rate=0.05)

for epoch in range(50):
    with tf.GradientTape() as tape:
        y_pred = predict(X)
        loss = loss_fn(y_true, y_pred)

    dw, db = tape.gradient(loss, [w, b])
    optimizer.apply_gradients([(dw, w), (db, b)])

    if epoch % 5 == 0:
        print(
            f"Epoch {epoch:02d} | "
            f"w={w.numpy()}, b={b.numpy():.3f}, "
            f"loss={loss.numpy():.4f}"
        )
```

---

## ✅ Expected result

শেষের দিকে:

```
w ≈ [2.0, 3.0]
b ≈ 1.0
loss ≈ 0
```

🎉 Model শিখে ফেলেছে multiple features handle করা

---

## 🔍 Important concepts (exam + interview)

* Feature vector
* Weight vector
* Broadcasting
* Dot product
* Shape alignment

---

## ❌ Common errors

❌ Shape mismatch
❌ Forget `axis=1`
❌ Wrong learning rate

---

## 🧠 Mental picture

```
x1 ──► (* w1)
x2 ──► (* w2) ─┐
                ├─► sum + b ─► y
```

---

## 🧪 Challenge (level up)

1️⃣ Add 3rd feature (x3)
2️⃣ Change true equation
3️⃣ Print gradient values

---



# 🏠 House Price Prediction (TensorFlow + Keras)

### 🎯 Problem

বাড়ির দাম predict করবো এই feature গুলো দিয়ে:

* `size` (sqft)
* `bedrooms`
* `age` (years)

📐 **Formula (unknown to model):**
[
price = f(size, bedrooms, age)
]

---

## 1️⃣ Dataset (dummy but realistic)

```python
import tensorflow as tf
import numpy as np

# Features: [size, bedrooms, age]
X = np.array([
    [800, 2, 10],
    [900, 2, 5],
    [1200, 3, 8],
    [1500, 4, 3],
    [1800, 4, 2],
    [2000, 5, 1],
], dtype=float)

# House prices (in lakhs)
y = np.array([
    50,
    55,
    75,
    100,
    120,
    140
], dtype=float)
```

---

## 2️⃣ Feature scaling (VERY important ⚠️)

```python
X = X / X.max(axis=0)
y = y / y.max()
```

🧠 Why?

* size = 2000
* bedrooms = 5
* age = 10

Scale না করলে learning slow / unstable হয়

---

## 3️⃣ Model (Linear Regression)

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(1, input_shape=(3,))
])
```

📌 3 features → 1 output

---

## 4️⃣ Compile model

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.1),
    loss='mse'
)
```

---

## 5️⃣ Train model

```python
model.fit(X, y, epochs=200, verbose=0)
```

---

## 6️⃣ Test prediction

```python
# New house: 1600 sqft, 4 bedrooms, 2 years old
new_house = np.array([[1600, 4, 2]], dtype=float)
new_house = new_house / X.max(axis=0)

pred_price = model.predict(new_house)
print("Predicted price (lakhs):", pred_price[0][0] * y.max())
```

---

## ✅ Output (approx)

```
Predicted price (lakhs): 110 – 120
```

🎉 Model successfully learned house pricing trend

---

## 🧠 What you just learned (IMPORTANT)

* Real regression problem
* Feature scaling
* Keras `Sequential` model
* Training → prediction pipeline

📌 **This is 80% of ML jobs**

---

## ❌ Common beginner mistakes

❌ No feature scaling
❌ Too complex model for small data
❌ Expecting 100% accuracy

---

## 🔥 Upgrade ideas (next level)

* Add more data
* Add hidden layer
* Save & load model
* Use real dataset (CSV)

---


# 🔥 Keras: Basic → Advance (Complete Analysis)

## 🧠 Keras আসলে কী?

Keras হলো **TensorFlow-এর high-level API**
👉 Low-level TF (GradientTape, Variable) কে hide করে
👉 Less code, more productivity

> Real life: 90% ML engineer **Keras ব্যবহার করে**

---

# 🟢 BASIC LEVEL (Must know)

## 1️⃣ Model building APIs

### 🔹 `Sequential`

➡️ Straight line model (layer by layer)

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu'),
    tf.keras.layers.Dense(1)
])
```

✅ Use when:

* Simple feed forward model
* CNN stack
  ❌ Avoid when:
* Multiple inputs/outputs

---

### 🔹 `Functional API`

➡️ Graph-based, flexible

```python
inputs = tf.keras.Input(shape=(10,))
x = tf.keras.layers.Dense(32, activation='relu')(inputs)
outputs = tf.keras.layers.Dense(1)(x)

model = tf.keras.Model(inputs, outputs)
```

✅ Use when:

* Multi-input/output
* Skip connection (ResNet)

---

## 2️⃣ Layers (building blocks 🧱)

### 🔹 Dense

```python
Dense(units, activation)
```

Used in:

* Regression
* Classification

---

### 🔹 Activation

* `relu` → hidden
* `sigmoid` → binary output
* `softmax` → multi-class

---

### 🔹 Input shape

```python
Dense(32, input_shape=(n_features,))
```

❌ Very common bug: wrong input shape

---

## 3️⃣ Compile step (MOST IMPORTANT)

```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)
```

### 🧠 Compile decides:

| Part      | Meaning          |
| --------- | ---------------- |
| Optimizer | How model learns |
| Loss      | How wrong it is  |
| Metrics   | What you monitor |

---

## 4️⃣ Training & inference

```python
model.fit(X, y, epochs=50, batch_size=32)
model.predict(X_new)
```

---

# 🟡 INTERMEDIATE LEVEL (Real-world skills)

## 5️⃣ Optimizers (learning behavior)

* `SGD` → slow but stable
* `Adam` → default choice
* `RMSprop` → RNN, noisy data

```python
tf.keras.optimizers.Adam(learning_rate=0.001)
```

---

## 6️⃣ Loss functions (match problem!)

| Problem               | Loss                       |
| --------------------- | -------------------------- |
| Regression            | `mse`, `mae`               |
| Binary classification | `binary_crossentropy`      |
| Multi-class           | `categorical_crossentropy` |

❌ Wrong loss = model never learns

---

## 7️⃣ Callbacks (training control 🔥)

### 🔹 EarlyStopping

```python
EarlyStopping(patience=5)
```

### 🔹 ModelCheckpoint

```python
ModelCheckpoint("best.h5", save_best_only=True)
```

📌 Used in **every serious project**

---

## 8️⃣ Validation & Overfitting

```python
model.fit(X, y, validation_split=0.2)
```

🧠 Watch:

* train loss ↓
* val loss ↑ → overfitting

---

# 🔵 ADVANCED LEVEL (Pro Keras)

## 9️⃣ Custom training loop

```python
with tf.GradientTape():
    ...
```

Used when:

* Research
* Custom loss
* GAN

---

## 🔟 Custom loss & metric

```python
def custom_loss(y_true, y_pred):
    return tf.reduce_mean(tf.abs(y_true - y_pred))
```

---

## 1️⃣1️⃣ Regularization

* Dropout
* L1 / L2

```python
Dense(64, activation='relu',
      kernel_regularizer='l2')
```

---

## 1️⃣2️⃣ Model saving & deployment

```python
model.save("model")
tf.keras.models.load_model("model")
```

Used in:

* Django / FastAPI
* Mobile (TFLite)

---

## 1️⃣3️⃣ `tf.data` with Keras

```python
dataset = tf.data.Dataset.from_tensor_slices((X, y)).batch(32)
model.fit(dataset)
```

For:

* Big data
* Images / videos

---

# 🧠 Pro mental map (memorize this)

```
Data
 ↓
Layers
 ↓
Model
 ↓
Compile
 ↓
Fit
 ↓
Evaluate / Predict
```

---

## ❌ Common beginner mistakes

* Too many layers
* No scaling
* Wrong loss
* Blindly increasing epochs

---

## 🎯 What YOU should master first

If তুমি এগুলো পারো:

* Sequential + Functional
* Dense, activation
* compile / fit
* callbacks
* save/load

👉 You are **job-ready junior ML dev** 😎

---


Perfect 😎🔥
তাহলে আমরা করব **End-to-End Keras Project** —
👉 CSV dataset → model → train → save → predict

আমি একদম clean, beginner-friendly way দেখাবো।

---

# 🏡 End-to-End Keras Project: House Price Prediction from CSV

## 1️⃣ Dataset (CSV)

ধরি CSV ফাইল: `house_prices.csv`

| size | bedrooms | age | price |
| ---- | -------- | --- | ----- |
| 800  | 2        | 10  | 50    |
| 900  | 2        | 5   | 55    |
| 1200 | 3        | 8   | 75    |
| 1500 | 4        | 3   | 100   |
| 1800 | 4        | 2   | 120   |
| 2000 | 5        | 1   | 140   |

---

## 2️⃣ Load CSV with Pandas

```python
import pandas as pd
import tensorflow as tf
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

# Load dataset
df = pd.read_csv("house_prices.csv")
X = df[['size', 'bedrooms', 'age']].values
y = df['price'].values
```

---

## 3️⃣ Train/Test split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

## 4️⃣ Feature scaling (VERY important)

```python
scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)

y_train = scaler_y.fit_transform(y_train.reshape(-1, 1))
y_test = scaler_y.transform(y_test.reshape(-1, 1))
```

---

## 5️⃣ Build Keras Model

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(3,)),
    tf.keras.layers.Dense(16, activation='relu'),
    tf.keras.layers.Dense(1)
])
```

---

## 6️⃣ Compile Model

```python
model.compile(
    optimizer='adam',
    loss='mse',
    metrics=['mae']
)
```

---

## 7️⃣ Train Model

```python
history = model.fit(
    X_train, y_train,
    validation_split=0.2,
    epochs=200,
    batch_size=2,
    verbose=1
)
```

---

## 8️⃣ Evaluate on Test Data

```python
loss, mae = model.evaluate(X_test, y_test)
print(f"Test MAE: {mae}")
```

---

## 9️⃣ Predict New Houses

```python
# New house
new_house = [[1600, 4, 2]]
new_house_scaled = scaler_X.transform(new_house)

pred_price_scaled = model.predict(new_house_scaled)
pred_price = scaler_y.inverse_transform(pred_price_scaled)

print("Predicted price:", pred_price[0][0])
```

---

## 🔟 Save & Load Model

```python
model.save("house_price_model.h5")
# Load
new_model = tf.keras.models.load_model("house_price_model.h5")
```

---

## ✅ What you just learned (End-to-End)

1. CSV → load data → train/test split
2. Feature scaling
3. Keras Sequential + Dense layers
4. Compile → fit → evaluate → predict
5. Save & load model
6. Validation split + small batch size → better learning

---

## 🔥 Next Challenge (Level-Up)

* Add **more features** (garage, location, floor)
* Use **real dataset** (like Kaggle)
* Add **callbacks**: EarlyStopping + ModelCheckpoint
* Visualize **training history**: loss & MAE plots

---


Perfect bondu 😎🔥
তাহলে আমরা করব **Full End-to-End House Price Prediction Project** যা ready হবে **Django/Flask API** জন্য।

চল structured ভাবে দেখে নিই:

---

# 🏡 Full Pipeline: CSV → Keras → Saved Model → API Ready

## 1️⃣ Dataset

* CSV ফাইল: `house_prices.csv`
* Columns: `size`, `bedrooms`, `age`, `price`
* Realistic but small for demo

---

## 2️⃣ Load & Prepare Data

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import MinMaxScaler

# Load CSV
df = pd.read_csv("house_prices.csv")
X = df[['size', 'bedrooms', 'age']].values
y = df['price'].values.reshape(-1,1)

# Split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Scaling
scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)

y_train = scaler_y.fit_transform(y_train)
y_test = scaler_y.transform(y_test)
```

---

## 3️⃣ Build Keras Model

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(3,)),
    tf.keras.layers.Dense(16, activation='relu'),
    tf.keras.layers.Dense(1)
])
```

---

## 4️⃣ Compile Model

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.01),
    loss='mse',
    metrics=['mae']
)
```

---

## 5️⃣ Train Model (with validation)

```python
history = model.fit(
    X_train, y_train,
    validation_split=0.2,
    epochs=200,
    batch_size=2,
    verbose=1
)
```

---

## 6️⃣ Evaluate Model

```python
loss, mae = model.evaluate(X_test, y_test)
print(f"Test MAE: {mae}")
```

---

## 7️⃣ Predict New Data

```python
new_house = [[1600, 4, 2]]
new_scaled = scaler_X.transform(new_house)
pred_scaled = model.predict(new_scaled)
pred_price = scaler_y.inverse_transform(pred_scaled)

print("Predicted price:", pred_price[0][0])
```

---

## 8️⃣ Save Model (API ready)

```python
model.save("house_price_model.h5")
```

📌 Later Flask/Django API এ শুধু:

```python
model = tf.keras.models.load_model("house_price_model.h5")
```

---

## 9️⃣ Optional: Save Scalers

```python
import joblib

joblib.dump(scaler_X, "scaler_X.save")
joblib.dump(scaler_y, "scaler_y.save")
```

👉 API থেকে একই scaling reuse করতে হবে

---

## 10️⃣ Next Steps (API Ready)

1. Flask/Django route: `/predict`
2. JSON input: `{"size":1600,"bedrooms":4,"age":2}`
3. Load model + scalers
4. Return predicted price

---

Perfect bondu 😎🔥
তাহলে আমরা এখন **House Price Prediction Flask API** বানাবো যা **End-to-End ready** থাকবে React/Frontend থেকে call করার জন্য।

আমি step-by-step দেখাচ্ছি:

---

# 🏡 Flask API: House Price Prediction (Full)

## 1️⃣ Install required packages

```bash
pip install flask tensorflow scikit-learn joblib
```

---

## 2️⃣ Project Structure

```
house_price_api/
│
├── house_price_model.h5
├── scaler_X.save
├── scaler_y.save
├── app.py
└── requirements.txt
```

---

## 3️⃣ `app.py` (Flask API)

```python
from flask import Flask, request, jsonify
import tensorflow as tf
import joblib
import numpy as np

app = Flask(__name__)

# Load model and scalers
model = tf.keras.models.load_model("house_price_model.h5")
scaler_X = joblib.load("scaler_X.save")
scaler_y = joblib.load("scaler_y.save")

@app.route("/predict", methods=["POST"])
def predict():
    data = request.get_json()
    
    # Extract features
    size = data.get("size")
    bedrooms = data.get("bedrooms")
    age = data.get("age")
    
    X_new = np.array([[size, bedrooms, age]])
    X_scaled = scaler_X.transform(X_new)
    
    # Prediction
    y_scaled = model.predict(X_scaled)
    y_pred = scaler_y.inverse_transform(y_scaled)
    
    return jsonify({"predicted_price": float(y_pred[0][0])})

if __name__ == "__main__":
    app.run(debug=True)
```

---

## 4️⃣ How to test

Use **Postman / curl / React frontend**:

```bash
curl -X POST http://127.0.0.1:5000/predict \
-H "Content-Type: application/json" \
-d '{"size":1600, "bedrooms":4, "age":2}'
```

**Expected output:**

```json
{"predicted_price": 115.2}
```

---

## 5️⃣ Notes / Pro Tips

* Always scale input features same way as training
* Batch prediction supported by sending multiple rows
* Save model + scalers → API deployment ready

---

## 6️⃣ Next Level Upgrade

* Add **validation** in API input
* Dockerize API
* Add **logging** & error handling
* Integrate with React frontend

---

Ahh bondu 😄🔥, বুঝলাম!
তুমি চাইছো **একদম clean structure**, যেখানে **সব কিছু save হবে**:

* **Keras model**
* **Input scaler**
* **Output scaler**
* **Anything else needed for production**

আমি step-by-step দিয়ে দিচ্ছি যাতে পরে **Flask/React API ready** হয়।

---

# 🏡 Full Save Pipeline: Keras Model + Scalers

## 1️⃣ Imports

```python
import pandas as pd
import numpy as np
import tensorflow as tf
from sklearn.preprocessing import MinMaxScaler
from sklearn.model_selection import train_test_split
import joblib
```

---

## 2️⃣ Load dataset

```python
# CSV
df = pd.read_csv("house_prices.csv")
X = df[['size', 'bedrooms', 'age']].values
y = df['price'].values.reshape(-1, 1)
```

---

## 3️⃣ Train/Test split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

---

## 4️⃣ Scale data (Save scalers!)

```python
scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()

X_train_scaled = scaler_X.fit_transform(X_train)
X_test_scaled = scaler_X.transform(X_test)

y_train_scaled = scaler_y.fit_transform(y_train)
y_test_scaled = scaler_y.transform(y_test)

# Save scalers
joblib.dump(scaler_X, "scaler_X.save")
joblib.dump(scaler_y, "scaler_y.save")
```

✅ Now input & output scaling is saved for later prediction

---

## 5️⃣ Build Keras model

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(3,)),
    tf.keras.layers.Dense(16, activation='relu'),
    tf.keras.layers.Dense(1)
])
```

---

## 6️⃣ Compile model

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.01),
    loss='mse',
    metrics=['mae']
)
```

---

## 7️⃣ Train model

```python
history = model.fit(
    X_train_scaled, y_train_scaled,
    validation_split=0.2,
    epochs=200,
    batch_size=2,
    verbose=1
)
```

---

## 8️⃣ Evaluate

```python
loss, mae = model.evaluate(X_test_scaled, y_test_scaled)
print(f"Test MAE: {mae}")
```

---

## 9️⃣ Save model

```python
model.save("house_price_model.h5")
```

✅ Everything is saved: **model + input scaler + output scaler**

---

## 10️⃣ Load & Predict (Production Ready)

```python
# Load model & scalers
model = tf.keras.models.load_model("house_price_model.h5")
scaler_X = joblib.load("scaler_X.save")
scaler_y = joblib.load("scaler_y.save")

# New data
new_house = np.array([[1600, 4, 2]])
X_new_scaled = scaler_X.transform(new_house)

# Prediction
y_scaled = model.predict(X_new_scaled)
y_pred = scaler_y.inverse_transform(y_scaled)

print("Predicted price:", y_pred[0][0])
```

---

## ✅ Pro Tips (Production Ready)

1. Always save **both scalers** + **model**
2. Keep **feature order consistent**
3. For batch prediction, `scaler_X.transform(multiple_rows)` works
4. Always scale new data before prediction
5. Saved model + scalers = ready for Flask/React API

---

Ahh ঠিক আছে bondu 😎🔥
এখন আমরা Keras/TensorFlow দিয়ে **Regression & Classification এর অন্যান্য গুরুত্বপূর্ণ models** শেখব, যাতে তোমার **ML toolbox** complete হয়।

আমি **from basic → advanced** মডেলগুলো analysis দিবো:

---

# 🧠 TensorFlow/Keras Models: Full Overview

---

## 1️⃣ **Linear Regression** (Single/Multi feature)

* Predict **continuous value**
* Formula: `y = w1*x1 + w2*x2 + ... + b`
* Keras: `Dense(1)`
* Use case: House price, salary prediction

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(1, input_shape=(n_features,))
])
```

---

## 2️⃣ **Polynomial Regression**

* Linear regression with **higher degree features**
* Model is still Dense → just add **x², x³** etc
* Use case: non-linear trend
* Note: Keras doesn’t need explicit formula, just **feature engineering**

```python
X_poly = np.column_stack([X, X**2, X**3])
```

---

## 3️⃣ **Logistic Regression** (Binary Classification)

* Predict **0 or 1**
* Activation: `sigmoid`
* Loss: `binary_crossentropy`

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(1, activation='sigmoid', input_shape=(n_features,))
])
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

* Use case: Loan approval, fraud detection

---

## 4️⃣ **Multi-class Classification**

* Predict multiple classes (3+)
* Activation: `softmax`
* Loss: `categorical_crossentropy`

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(n_features,)),
    tf.keras.layers.Dense(n_classes, activation='softmax')
])
```

* Use case: Digit recognition (MNIST), animal classification

---

## 5️⃣ **Neural Network (Dense / MLP)**

* Multiple hidden layers
* Activation: `relu`, `tanh`
* Can handle complex patterns
* Use case: Tabular regression/classification

```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(64, activation='relu', input_shape=(n_features,)),
    tf.keras.layers.Dense(32, activation='relu'),
    tf.keras.layers.Dense(1)  # regression
])
```

* Add Dropout → prevent overfitting

---

## 6️⃣ **Convolutional Neural Network (CNN)**

* For **images / spatial data**
* Layers: Conv2D → Pooling → Flatten → Dense
* Activation: relu → output depends on task

```python
model = tf.keras.Sequential([
    tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28,28,1)),
    tf.keras.layers.MaxPooling2D(2,2),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])
```

* Use case: Image classification, object detection

---

## 7️⃣ **Recurrent Neural Network (RNN / LSTM / GRU)**

* For **sequence data**
* Input shape: `(timesteps, features)`
* Use case: Time series, text, stock prediction

```python
model = tf.keras.Sequential([
    tf.keras.layers.LSTM(50, input_shape=(timesteps, features)),
    tf.keras.layers.Dense(1)
])
```

* GRU → faster alternative to LSTM

---

## 8️⃣ **Autoencoder**

* Input = Output
* Used for: **Dimensionality reduction, anomaly detection**

```python
input_dim = X.shape[1]
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(input_dim,)),
    tf.keras.layers.Dense(16, activation='relu'),
    tf.keras.layers.Dense(32, activation='relu'),
    tf.keras.layers.Dense(input_dim)
])
```

---

## 9️⃣ **Hybrid / Custom Models**

* Multiple inputs / outputs → **Functional API**
* Example: CCTV anomaly detection (image + sensor)

```python
from tensorflow.keras import Input, Model
inp1 = Input(shape=(10,))
inp2 = Input(shape=(5,))
x1 = tf.keras.layers.Dense(32, activation='relu')(inp1)
x2 = tf.keras.layers.Dense(16, activation='relu')(inp2)
concat = tf.keras.layers.concatenate([x1,x2])
out = tf.keras.layers.Dense(1)(concat)
model = Model([inp1, inp2], out)
```

---

## 🔹 Key Takeaways

1. Regression → Linear / Polynomial / NN
2. Classification → Logistic / Multi-class / NN
3. Images → CNN
4. Sequences → RNN / LSTM / GRU
5. Dimensionality reduction → Autoencoder
6. Multi-input/output → Functional API

---
Ahh হ্যাঁ bondu 😎🔥
এখন আমরা **Polynomial Regression** পুরোপুরি TensorFlow/Keras এ দেখব:

* Concept
* Feature engineering
* Keras implementation
* Prediction
* Scaling best practices

---

# 🧠 Polynomial Regression in Keras

### 1️⃣ Concept

Polynomial regression is basically **Linear Regression with polynomial features**:

[
y = w_0 + w_1 x + w_2 x^2 + w_3 x^3 + ... + w_n x^n
]

* Non-linear trend captured
* Still linear in parameters
* Use **feature transformation**

---

### 2️⃣ Example Dataset

Suppose relationship:

[
y = 2 + 3x - 0.5 x^2 + 0.1 x^3
]

```python
import numpy as np
import matplotlib.pyplot as plt

# Sample data
X = np.linspace(-5, 5, 50)
y = 2 + 3*X - 0.5*X**2 + 0.1*X**3 + np.random.randn(50)*2

plt.scatter(X, y)
plt.show()
```

---

### 3️⃣ Polynomial Feature Engineering

Keras cannot automatically create polynomial terms → **we manually expand features**:

```python
from sklearn.preprocessing import PolynomialFeatures

# Degree 3 polynomial
poly = PolynomialFeatures(degree=3, include_bias=False)
X_poly = poly.fit_transform(X.reshape(-1,1))

print("Original X shape:", X.shape)
print("Polynomial X shape:", X_poly.shape)
```

* `X_poly` columns: `[x, x^2, x^3]`
* Now you can feed this to **Dense layer**

---

### 4️⃣ Scaling Features (Best Practice)

```python
from sklearn.preprocessing import MinMaxScaler

scaler_X = MinMaxScaler()
scaler_y = MinMaxScaler()

X_scaled = scaler_X.fit_transform(X_poly)
y_scaled = scaler_y.fit_transform(y.reshape(-1,1))
```

✅ Always scale inputs & output for stable training

---

### 5️⃣ Keras Model (Dense Regression)

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation='relu', input_shape=(X_scaled.shape[1],)),
    tf.keras.layers.Dense(16, activation='relu'),
    tf.keras.layers.Dense(1)  # Linear output
])

model.compile(optimizer='adam', loss='mse', metrics=['mae'])
```

---

### 6️⃣ Train Model

```python
history = model.fit(X_scaled, y_scaled, epochs=300, batch_size=4, validation_split=0.2)
```

* Watch **loss** decrease
* Use **EarlyStopping** for better control

---

### 7️⃣ Predict & Convert to Actual Output

```python
# New data
X_new = np.array([[2]])  # x = 2
X_new_poly = poly.transform(X_new)
X_new_scaled = scaler_X.transform(X_new_poly)

y_new_scaled = model.predict(X_new_scaled)
y_new_actual = scaler_y.inverse_transform(y_new_scaled)

print("Predicted y:", y_new_actual[0][0])
```

---

### 8️⃣ Visualize Predictions

```python
y_pred_scaled = model.predict(X_scaled)
y_pred = scaler_y.inverse_transform(y_pred_scaled)

plt.scatter(X, y, label='Original')
plt.plot(X, y_pred, color='red', label='Polynomial Regression')
plt.legend()
plt.show()
```

✅ You’ll see a **smooth curve fitting the data**

---

### 🔹 Key Takeaways (Polynomial Regression in Keras)

1. Polynomial features → manually or `PolynomialFeatures`
2. Scale features & output
3. Dense NN can learn **non-linear relationships**
4. Always inverse_transform output to get actual values
5. Works for **small tabular datasets**, not huge degrees (overfitting risk)

---

💡 **Pro Tip bondu:**

* Degree 2–3 → small datasets
* Degree >5 → use regularization (L1/L2) or Dropout to prevent overfitting

---

