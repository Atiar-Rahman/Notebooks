 Now that you understand **CNN theory**, let’s go into a **step-by-step implementation** of a CNN using **TensorFlow/Keras**.

I’ll use the classic **MNIST dataset (handwritten digits)** as an example, since it’s simple and widely used.

---

# 🔹 Step 1: Import Libraries

```python
import tensorflow as tf
from tensorflow.keras import datasets, layers, models
```

---

# 🔹 Step 2: Load Dataset (MNIST)

```python
# Load MNIST dataset (28x28 grayscale images of digits 0–9)
(X_train, y_train), (X_test, y_test) = datasets.mnist.load_data()

# Reshape to add channel dimension (needed for Conv2D)
X_train = X_train.reshape((X_train.shape[0], 28, 28, 1))
X_test = X_test.reshape((X_test.shape[0], 28, 28, 1))

# Normalize pixel values (0–255 → 0–1)
X_train, X_test = X_train / 255.0, X_test / 255.0
```

---

# 🔹 Step 3: Build CNN Model

```python
model = models.Sequential([
    # Convolutional Layer + ReLU
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(28,28,1)),
    layers.MaxPooling2D((2,2)),

    # Second Conv Layer
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),

    # Flatten + Fully Connected Layers
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')  # 10 output classes
])
```

---

# 🔹 Step 4: Compile Model

```python
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

---

# 🔹 Step 5: Train Model

```python
history = model.fit(X_train, y_train, epochs=5, batch_size=64, validation_data=(X_test, y_test))
```

---

# 🔹 Step 6: Evaluate Model

```python
test_loss, test_acc = model.evaluate(X_test, y_test, verbose=2)
print(f"Test Accuracy: {test_acc * 100:.2f}%")
```

✅ You should get **~99% accuracy** after just a few epochs.

---

# 🔹 Step 7: Make Predictions

```python
import numpy as np

# Pick a random test image
i = np.random.randint(0, len(X_test))
image = X_test[i].reshape(1,28,28,1)

prediction = model.predict(image)
print("Predicted Label:", np.argmax(prediction))
print("True Label:", y_test[i])
```

---

# 🔹 Summary of Pipeline

1. Load & preprocess data (reshape + normalize)
    
2. Build CNN with Conv → ReLU → Pool → Flatten → Dense → Output
    
3. Compile with optimizer + loss
    
4. Train using `.fit()`
    
5. Evaluate accuracy on test set
    
6. Predict new samples
    

---

💡 You can replace **MNIST** with **CIFAR-10** (colored images, 10 classes) just by changing the dataset and input shape `(32,32,3)`.

👉 Do you want me to show you the **CIFAR-10 CNN implementation** too, so you can practice on **color images**?

---
Perfect 👍 You want to know how to use a **custom dataset** (your own images) with CNN in TensorFlow. Let’s go step by step 👇

---

# 🔹 1. Organize Your Dataset

For TensorFlow/Keras, the **recommended format** is:

```
dataset/
│
├── train/
│   ├── cats/
│   │   ├── cat1.jpg
│   │   ├── cat2.jpg
│   │   └── ...
│   ├── dogs/
│   │   ├── dog1.jpg
│   │   ├── dog2.jpg
│   │   └── ...
│
├── test/
│   ├── cats/
│   ├── dogs/
│
└── validation/   (optional)
    ├── cats/
    ├── dogs/
```

👉 Each **subfolder = class label**  
👉 TensorFlow will automatically assign labels.

---

# 🔹 2. Load Custom Dataset

```python
import tensorflow as tf
from tensorflow.keras import layers, models

# Set dataset paths
train_dir = "dataset/train"
test_dir = "dataset/test"

# Load images (automatically labeled by folder name)
img_size = (128, 128)  # resize all images to same size
batch_size = 32

train_ds = tf.keras.utils.image_dataset_from_directory(
    train_dir,
    image_size=img_size,
    batch_size=batch_size
)

test_ds = tf.keras.utils.image_dataset_from_directory(
    test_dir,
    image_size=img_size,
    batch_size=batch_size
)
```

---

# 🔹 3. Preprocess Images

- Normalize pixels (0–255 → 0–1)
    
- Prefetch for speed
    

```python
# Normalize
normalization_layer = layers.Rescaling(1./255)

train_ds = train_ds.map(lambda x, y: (normalization_layer(x), y))
test_ds = test_ds.map(lambda x, y: (normalization_layer(x), y))

# Improve performance
train_ds = train_ds.cache().shuffle(1000).prefetch(buffer_size=tf.data.AUTOTUNE)
test_ds = test_ds.cache().prefetch(buffer_size=tf.data.AUTOTUNE)
```

---

# 🔹 4. Build CNN Model

```python
num_classes = len(train_ds.class_names)  # automatically detects classes

model = models.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(128,128,3)),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(128, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Flatten(),
    layers.Dense(128, activation='relu'),
    layers.Dense(num_classes, activation='softmax')
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

model.summary()
```

---

# 🔹 5. Train Model

```python
history = model.fit(train_ds, validation_data=test_ds, epochs=10)
```

---

# 🔹 6. Evaluate Model

```python
loss, acc = model.evaluate(test_ds)
print(f"Test Accuracy: {acc*100:.2f}%")
```

---

# 🔹 7. Predict on New Images

```python
from tensorflow.keras.preprocessing import image
import numpy as np

img_path = "dataset/test/cats/cat5.jpg"  # example image
img = image.load_img(img_path, target_size=(128,128))
img_array = image.img_to_array(img) / 255.0
img_array = np.expand_dims(img_array, axis=0)

prediction = model.predict(img_array)
predicted_class = train_ds.class_names[np.argmax(prediction)]

print("Predicted class:", predicted_class)
```

---

✅ With this pipeline you can use **any custom dataset** (cats vs dogs, fruits, flowers, medical images, etc.).  
✅ Just place your images in folder structure, and TensorFlow handles labeling.

---

👉 Do you want me to also show you how to **use data augmentation (rotation, flip, zoom)** to improve accuracy on custom datasets?

---
Good question 👌 — CNNs (Convolutional Neural Networks) are **not strictly supervised or unsupervised by themselves**.  
They are a **neural network architecture**, and how they are used depends on the type of **training objective**.

Let’s break it down:

---

# 🔹 1. CNN in **Supervised Learning**

👉 This is the **most common use case**.

- CNNs are trained on **labeled data** (image + class).
    
- The goal is to minimize a **loss function** (e.g., cross-entropy) comparing predicted labels with true labels.
    
- Example tasks:
    
    - Image classification (Cat vs Dog)
        
    - Object detection (YOLO, Faster R-CNN)
        
    - Semantic segmentation
        

✅ CNNs are mostly known for **supervised learning in computer vision**.

---

# 🔹 2. CNN in **Unsupervised Learning**

CNNs can also be adapted for **unsupervised tasks** (no labels).  
In this case, CNN acts as a **feature extractor**, and learning happens via other methods.

Examples:

- **Autoencoders (CNN-based):** Learn to reconstruct input images → useful for anomaly detection, image denoising.
    
- **Self-supervised CNNs:** Train on pretext tasks (like predicting missing parts of an image, rotation angle) → later used for classification.
    
- **Clustering with CNNs:** Use CNN features + clustering (e.g., k-means).
    

---

# 🔹 3. CNN in **Semi-Supervised Learning**

- Uses **a small amount of labeled data + large amount of unlabeled data**.
    
- CNN learns representations from unlabeled images (unsupervised pretraining) and fine-tunes on labeled data.
    

Example: Medical imaging, where labels are expensive.

---

# 🔹 4. CNN in **Reinforcement Learning**

- CNNs are also used as **feature extractors** in RL (e.g., DeepMind’s Atari games).
    
- The CNN processes game frames → outputs state representation → used by reinforcement algorithm (Q-learning, policy gradient).
    

---

# ✅ Final Answer:

- **CNN itself is an architecture**.
    
- It is **mostly used in supervised learning** (classification, detection).
    
- But it can also be applied in **unsupervised (autoencoders, clustering), semi-supervised, and reinforcement learning** depending on how you train it.
    

---

👉 Do you want me to prepare a **comparison table (Supervised vs Unsupervised CNN usage)** so you can see it at a glance?

