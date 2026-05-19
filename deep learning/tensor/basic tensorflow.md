

# 🧠 CNN from Scratch (Image-Based Surveillance)

### 🎯 Goal

Classify surveillance images like:

- `normal`
    
- `suspicious`
    

(We’ll start with **image classification**, then this easily extends to **video frames**)

---

## 1️⃣ What is a CNN?

CNN = **Convolutional Neural Network**

Specially designed for **images**.

### Why not Dense layers?

- Images have **spatial structure**
    
- CNN learns:
    
    - edges
        
    - shapes
        
    - motion patterns (later in video)
        

---

## 2️⃣ CNN Architecture (Simple & Effective)

```
Input Image (128x128x3)
↓
Conv2D + ReLU
↓
MaxPooling
↓
Conv2D + ReLU
↓
MaxPooling
↓
Flatten
↓
Dense
↓
Output (Normal / Suspicious)
```

---

## 3️⃣ Dataset Structure (VERY IMPORTANT)

This works **directly with Keras**:

```
dataset/
├── train/
│   ├── normal/
│   └── suspicious/
│
└── test/
    ├── normal/
    └── suspicious/
```

📌 Images can be extracted from surveillance video (frames).

---

## 4️⃣ Load Images (Keras Way)

```python
import tensorflow as tf

IMG_SIZE = (128, 128)
BATCH_SIZE = 16

train_ds = tf.keras.preprocessing.image_dataset_from_directory(
    "dataset/train",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)

test_ds = tf.keras.preprocessing.image_dataset_from_directory(
    "dataset/test",
    image_size=IMG_SIZE,
    batch_size=BATCH_SIZE
)
```

👉 Automatically:

- Reads folders
    
- Labels images
    
- Batches data
    

---

## 5️⃣ Normalize Images (Important)

```python
normalization = tf.keras.layers.Rescaling(1./255)
```

Why?

- Pixel range: `0–255`
    
- NN prefers `0–1`
    

---

## 6️⃣ Build CNN from Scratch 🔥

```python
from tensorflow.keras import layers, models

model = models.Sequential([
    normalization,

    layers.Conv2D(32, (3,3), activation='relu', input_shape=(128,128,3)),
    layers.MaxPooling2D(2,2),

    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D(2,2),

    layers.Conv2D(128, (3,3), activation='relu'),
    layers.MaxPooling2D(2,2),

    layers.Flatten(),

    layers.Dense(128, activation='relu'),
    layers.Dense(1, activation='sigmoid')
])
```

---

## 7️⃣ Compile the Model

```python
model.compile(
    optimizer='adam',
    loss='binary_crossentropy',
    metrics=['accuracy']
)
```

### Why?

- **Binary problem** → `binary_crossentropy`
    
- **Sigmoid** → probability (0–1)
    

---

## 8️⃣ Train the CNN

```python
history = model.fit(
    train_ds,
    validation_data=test_ds,
    epochs=10
)
```

📌 CPU-friendly tips:

- Use `128x128`
    
- Small batch size
    
- Fewer layers
    

---

## 9️⃣ Test with a Single Image

```python
import numpy as np
from tensorflow.keras.preprocessing import image

img = image.load_img("test.jpg", target_size=(128,128))
img = image.img_to_array(img) / 255.0
img = np.expand_dims(img, axis=0)

prediction = model.predict(img)

if prediction[0][0] > 0.5:
    print("Suspicious Activity 🚨")
else:
    print("Normal Activity ✅")
```

---

## 🔟 How This Becomes VIDEO Surveillance 🎥

### Step-by-step:

1️⃣ Capture video  
2️⃣ Extract frames  
3️⃣ Run CNN on each frame  
4️⃣ Alert if suspicious detected

---

### Frame Extraction (OpenCV)

```python
import cv2

cap = cv2.VideoCapture("video.mp4")

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break

    frame = cv2.resize(frame, (128,128))
    frame = frame / 255.0
    frame = frame.reshape(1,128,128,3)

    pred = model.predict(frame)

    if pred[0][0] > 0.5:
        print("🚨 Suspicious frame detected")

cap.release()
```

---

## 🧠 Real-World Improvements (Next Level)

When you’re ready:

- ✅ Data augmentation
    
- ✅ CNN + LSTM (motion detection)
    
- ✅ YOLO / SSD (object detection)
    
- ✅ Django + REST API
    
- ✅ Multi-camera support
    

---

## 🎯 What Should We Do NEXT?

Choose ONE 👇  
1️⃣ Improve accuracy (augmentation + regularization)  
2️⃣ CNN + LSTM (video motion detection 🔥)  
3️⃣ Save model + use in Django backend  
4️⃣ Object detection (YOLO vs CNN)

Say the number — we go deep 🚀