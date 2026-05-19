 **step by step into CNN (Convolutional Neural Networks)** in detail but in a clear and easy way.

---

# 🔹 1. What is a CNN?

- A **Convolutional Neural Network (CNN)** is a type of **deep learning model** specially designed for processing data with a **grid-like structure** (e.g., images, audio spectrograms).
    
- In computer vision, CNNs are used for tasks like **image classification, object detection, face recognition, segmentation**, etc.
    

💡 Key Idea: Instead of fully connecting all neurons (like in an MLP), CNNs use **convolutional layers** to extract spatial features (edges, shapes, textures).

---

# 🔹 2. Why CNN for Images?

- Images are **high-dimensional** (e.g., 224×224×3 = 150,528 pixels).
    
- Fully connected networks would need **huge parameters** → not efficient.
    
- CNN reduces parameters by **sharing weights** through filters (kernels).
    
- Also captures **spatial relationships** (nearby pixels are related).
    

---

# 🔹 3. CNN Architecture (Step by Step)

A CNN is usually built as a stack of:

### (a) **Input Layer**

- Accepts raw data (e.g., image 32×32×3 for RGB).
    

---

### (b) **Convolutional Layer**

- Applies **filters (kernels)** that slide over the input and compute a **dot product** (convolution).
    
- Purpose: Extract **features** like edges, corners, textures.
    
- Output is a **feature map**.
    

👉 Example:

- Input: 5×5 image
    
- Filter: 3×3
    
- Stride: 1 → output size = (5-3)/1 + 1 = 3×3
    

---

### (c) **Activation Function (ReLU)**

- Introduces **non-linearity**.
    
- ReLU: f(x)=max⁡(0,x)f(x) = \max(0, x)
    
- Helps prevent vanishing gradients and makes CNN learn complex features.
    

---

### (d) **Pooling Layer (Downsampling)**

- Reduces spatial size of feature maps → less computation, less overfitting.
    
- Types:
    
    - **Max Pooling**: Takes max value (common)
        
    - **Average Pooling**: Takes average value
        

👉 Example:

- Input: 4×4
    
- Pool: 2×2 (stride=2)
    
- Output: 2×2
    

---

### (e) **Flatten Layer**

- Converts 2D feature maps → 1D vector.
    
- Needed before fully connected layers.
    

---

### (f) **Fully Connected (Dense) Layer**

- Works like a traditional MLP (weights + bias).
    
- Combines extracted features for final decision-making.
    

---

### (g) **Output Layer**

- Uses **Softmax (for multi-class)** or **Sigmoid (for binary classification)**.
    
- Produces class probabilities.
    

---

# 🔹 4. CNN Workflow Example (Image Classification)

1. Input: 32×32×3 image (RGB)
    
2. Conv layer (32 filters 3×3) → 32 feature maps
    
3. ReLU activation
    
4. MaxPooling (2×2) → smaller feature maps
    
5. Conv + ReLU + Pool again → deeper features
    
6. Flatten → 1D vector
    
7. Dense (Fully Connected) → combine features
    
8. Output layer (Softmax with 10 classes, e.g., digits 0–9)
    

---

# 🔹 5. Key Concepts

✅ **Filter/Kernel:** Small matrix that extracts local features.  
✅ **Stride:** How many steps the filter moves.  
✅ **Padding:** Adding zeros around image to preserve dimensions.  
✅ **Feature Hierarchy:**

- Lower layers → edges, textures
    
- Middle layers → shapes, motifs
    
- Higher layers → objects, faces
    

---

# 🔹 6. Applications of CNN

- **Image Classification** (Cats vs Dogs, MNIST digits)
    
- **Object Detection** (YOLO, Faster R-CNN)
    
- **Face Recognition** (FaceNet, DeepFace)
    
- **Medical Imaging** (tumor detection, X-ray analysis)
    
- **Self-driving Cars** (lane detection, obstacle recognition)
    
- **Video Analysis** (action recognition, anomaly detection)
    

---

# 🔹 7. Advantages of CNN

- Fewer parameters (compared to MLPs)
    
- Automatic feature extraction
    
- Works very well for spatial data
    
- High accuracy in vision tasks
    

---

# 🔹 8. Limitations

- Requires large labeled datasets
    
- Computationally expensive (need GPU)
    
- Black-box nature → hard to interpret decisions
    

---

# 🔹 9. Example (TensorFlow/Keras)

```python
import tensorflow as tf
from tensorflow.keras import layers, models

# Build a simple CNN
model = models.Sequential([
    layers.Conv2D(32, (3,3), activation='relu', input_shape=(32,32,3)),
    layers.MaxPooling2D((2,2)),
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D((2,2)),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')  # for 10 classes
])

model.summary()
```

---

# 🔹 10. Summary Table

|Layer|Purpose|
|---|---|
|Conv|Extract local features|
|ReLU|Add non-linearity|
|Pooling|Reduce dimensions|
|Flatten|Convert to 1D|
|Dense|Combine features|
|Output|Classification|

---

💡 **Quick Analogy:**

- Think of CNN like **human vision**:
    
    - Eyes detect edges & colors (convolution)
        
    - Brain filters important details (pooling)
        
    - Final understanding → decision (dense layers).
        

---
ঠিক আছে, তুমি জিজ্ঞেস করেছ “CNN এর কতগুলো মডেল আছে” — আসলে CNN-এর **কোনও নির্দিষ্ট সংখ্যা নেই**, কারণ এটা একটি আর্কিটেকচারাল ধারণা। তবে আমরা অনেক জনপ্রিয় **standard CNN মডেল** আছে, যা বিভিন্ন কাজের জন্য তৈরি হয়েছে। আমি সবকে সহজভাবে ভাগ করে দেখাচ্ছি:

---

## 1️⃣ **Simple / Custom CNN**

- নিজের তৈরি ছোট CNN
    
- সাধারণত 2–5 Conv layers + Pooling + Dense
    
- Dataset: MNIST, CIFAR10 (ছোট dataset)
    
- উদাহরণ:
    
    - 2 Conv + MaxPool + Dense
        
    - 3 Conv + MaxPool + Dropout + Dense
        

---

## 2️⃣ **Classic CNN Models**

- **LeNet-5** (1998)
    
    - 2 Conv + Pooling + Fully Connected
        
    - মূলত digit recognition (MNIST)
        
- **AlexNet** (2012)
    
    - 5 Conv + 3 Fully Connected
        
    - ReLU, Dropout, Data Augmentation
        
- **ZFNet / ZFNet-5**
    
    - AlexNet-এর আপগ্রেড
        
- **VGG (VGG16, VGG19)**
    
    - 16 বা 19 layers
        
    - শুধু 3x3 Conv + MaxPooling
        
- **GoogLeNet / Inception**
    
    - Inception Modules
        
    - Deep but lightweight
        
- **ResNet (50, 101, 152)**
    
    - Residual Connections (Skip Connections)
        
    - খুব deep network train করা সম্ভব
        

---

## 3️⃣ **Lightweight / Mobile CNNs**

- MobileNet (V1, V2, V3) → Mobile / Edge devices
    
- EfficientNet → Accuracy + Speed optimized
    
- ShuffleNet → Low compute device
    

---

## 4️⃣ **Specialized CNN**

- **Segmentation**: U-Net, SegNet
    
- **Detection**: YOLO, Faster R-CNN
    
- **Attention-based CNNs**: CBAM, SENet
    

---

### ✅ Summary

- **Total models = অসংখ্য**, কারণ তুমি নিজের CNN বানাতে পারো
    
- **Popular pretrained CNNs (ImageNet)**:
    
    1. LeNet
        
    2. AlexNet
        
    3. VGG16 / VGG19
        
    4. GoogLeNet / Inception
        
    5. ResNet (50,101,152)
        
    6. MobileNet
        
    7. EfficientNet
        
    8. DenseNet
        
    9. NASNet / Xception
        

প্রয়োজন অনুযায়ী **ছোট, হালকা, বা গভীর** network বেছে নাও।

---

ঠিক আছে 😎 এবার আমি **প্রতিটি জনপ্রিয় CNN মডেল** এর **layer structure + parameter overview** সহজভাবে দেখাবো। আমি diagram হিসেবে text/ASCII আকারে বা flowchart-style বানাবো, যাতে বোঝা সহজ হয়।

---

# 1️⃣ **LeNet-5 (1998)**

- কাজ: Digit recognition (MNIST)
    
- Input: 32×32 grayscale
    

```
Input: 32x32x1
│
Conv1: 6 filters, 5x5 → 28x28x6
│
AvgPool1: 2x2 → 14x14x6
│
Conv2: 16 filters, 5x5 → 10x10x16
│
AvgPool2: 2x2 → 5x5x16
│
Flatten → 400
│
FC1: 120
│
FC2: 84
│
Output: 10 (softmax)
```

- Parameters: ~60K
    
- Feature: Small, simple
    

---

# 2️⃣ **AlexNet (2012)**

- Input: 224x224x3
    
- 5 Conv + 3 FC
    

```
Input: 224x224x3
│
Conv1: 96 11x11, stride 4 → 55x55x96
│
MaxPool1: 3x3, stride 2 → 27x27x96
│
Conv2: 256 5x5 → 27x27x256
│
MaxPool2: 3x3 → 13x13x256
│
Conv3: 384 3x3 → 13x13x384
Conv4: 384 3x3 → 13x13x384
Conv5: 256 3x3 → 13x13x256
│
MaxPool3: 3x3 → 6x6x256
│
Flatten → 9216
│
FC1: 4096
FC2: 4096
FC3: 1000
```

- Parameters: ~60M
    
- Features: First deep CNN with ReLU & Dropout
    

---

# 3️⃣ **VGG16 (2014)**

- Input: 224x224x3
    
- 16 layers (13 Conv + 3 FC)
    

```
Conv3-64
Conv3-64
MaxPool
Conv3-128
Conv3-128
MaxPool
Conv3-256
Conv3-256
Conv3-256
MaxPool
Conv3-512
Conv3-512
Conv3-512
MaxPool
Conv3-512
Conv3-512
Conv3-512
MaxPool
Flatten
FC-4096
FC-4096
FC-1000
```

- Parameters: ~138M (heavy)
    
- Feature: Simple 3x3 Conv stack
    

---

# 4️⃣ **GoogLeNet / Inception v1**

- Input: 224x224x3
    
- Key: **Inception module**
    

```
Input
│
Conv1: 7x7, stride2
MaxPool
Conv2: 1x1, 3x3, 1x1
Inception modules x9
GlobalAvgPool
FC: 1000
```

- Parameters: ~6.8M (light)
    
- Feature: Multi-scale convolutions in parallel
    

---

# 5️⃣ **ResNet50 (2015)**

- Input: 224x224x3
    
- 50 layers, **residual blocks**
    

```
Input
Conv1: 7x7 → 112x112
MaxPool
Conv2_x: 3 residual blocks
Conv3_x: 4 residual blocks
Conv4_x: 6 residual blocks
Conv5_x: 3 residual blocks
GlobalAvgPool
FC: 1000
```

- Parameters: ~25.6M
    
- Feature: Skip connections → very deep without vanishing gradient
    

---

# 6️⃣ **MobileNetV2**

- Input: 224x224x3
    
- Lightweight, for mobile
    

```
Input
Conv2D 3x3
Bottleneck Residual Blocks x17
Conv1x1
GlobalAvgPool
FC: 1000
```

- Parameters: ~3.4M (very small)
    
- Feature: Depthwise separable conv → light & fast
    

---

# 7️⃣ **EfficientNet (B0–B7)**

- Scalable width, depth, resolution
    
- Example: B0
    

```
Input
Stem Conv
MBConv blocks x16
GlobalAvgPool
FC: 1000
```

- Parameters: B0 ~5M, B7 ~66M
    
- Feature: High accuracy, efficient computation
    

---

# ✅ Quick Comparison Table

|Model|Depth|Params|Notes|
|---|---|---|---|
|LeNet-5|7|60K|Small, MNIST|
|AlexNet|8|60M|First deep CNN|
|VGG16|16|138M|Heavy, simple|
|GoogLeNet|22|6.8M|Inception module|
|ResNet50|50|25.6M|Residual blocks|
|MobileNetV2|53|3.4M|Lightweight|
|EfficientNetB0|16|5M|Efficient, high accuracy|

---

💡 Observations:

1. LeNet & AlexNet → academic / classic
    
2. VGG → simple but heavy
    
3. ResNet → deep, skip connections
    
4. MobileNet / EfficientNet → modern, fast, light
    

---

ঠিক আছে 😎 এবার আমি দেখাচ্ছি **Simple / Custom CNN বানানোর পুরো pipeline** **শুরু থেকে শেষ পর্যন্ত**, উদাহরণ হিসেবে আমরা **MNIST বা CIFAR-10** dataset ব্যবহার করব। এটি ছোট, শিক্ষামূলক CNN যা নতুনদের জন্য perfect।

---

# ✅ Full Pipeline: Simple / Custom CNN

## 1️⃣ Libraries Import

```python
import tensorflow as tf
from tensorflow.keras import layers, models
import matplotlib.pyplot as plt
import numpy as np
```

---

## 2️⃣ Load Dataset (MNIST / CIFAR-10)

### Example: CIFAR-10

```python
(x_train, y_train), (x_test, y_test) = tf.keras.datasets.cifar10.load_data()

# Normalize images
x_train, x_test = x_train / 255.0, x_test / 255.0

# Classes
class_names = ['airplane','car','bird','cat','deer','dog','frog','horse','ship','truck']
```

---

## 3️⃣ Data Augmentation (Optional, improves accuracy)

```python
data_augmentation = tf.keras.Sequential([
    layers.RandomFlip("horizontal"),
    layers.RandomRotation(0.1),
    layers.RandomZoom(0.1)
])
```

---

## 4️⃣ Build Simple CNN Model

### Example 1: 2 Conv + MaxPool + Dense

```python
model = models.Sequential([
    layers.Input(shape=(32,32,3)),

    # Data Augmentation (optional)
    data_augmentation,

    # Conv Layer 1
    layers.Conv2D(32, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    # Conv Layer 2
    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Flatten(),
    layers.Dense(128, activation='relu'),
    layers.Dense(10, activation='softmax')  # 10 classes
])
```

### Example 2: 3 Conv + MaxPool + Dropout + Dense

```python
model = models.Sequential([
    layers.Input(shape=(32,32,3)),

    data_augmentation,

    layers.Conv2D(32, (3,3), activation='relu'),
    layers.Conv2D(32, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Flatten(),
    layers.Dense(128, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(10, activation='softmax')
])
```

---

## 5️⃣ Compile Model

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

---

## 6️⃣ Train Model

```python
history = model.fit(
    x_train, y_train,
    epochs=20,
    batch_size=64,
    validation_split=0.2
)
```

---

## 7️⃣ Plot Accuracy & Loss

```python
plt.plot(history.history['accuracy'], label='train_acc')
plt.plot(history.history['val_accuracy'], label='val_acc')
plt.legend()
plt.show()

plt.plot(history.history['loss'], label='train_loss')
plt.plot(history.history['val_loss'], label='val_loss')
plt.legend()
plt.show()
```

---

## 8️⃣ Evaluate on Test Data

```python
test_loss, test_acc = model.evaluate(x_test, y_test)
print("Test accuracy:", test_acc)
```

---

## 9️⃣ Confusion Matrix + Classification Report

```python
from sklearn.metrics import confusion_matrix, classification_report

y_pred = np.argmax(model.predict(x_test), axis=1)
y_true = y_test.flatten()

cm = confusion_matrix(y_true, y_pred)
print("Confusion Matrix:\n", cm)
print(classification_report(y_true, y_pred, target_names=class_names))
```

---

## 10️⃣ Save & Load Model

```python
model.save("custom_cnn_model.h5")
# Load
# model = tf.keras.models.load_model("custom_cnn_model.h5")
```

---

# ✅ Summary Pipeline (Simple CNN)

```
Images → Normalize → (Optional Data Augmentation)
      → Conv2D + ReLU → MaxPooling
      → Conv2D + ReLU → MaxPooling (Optional more layers)
      → Flatten → Dense → Dropout (Optional)
      → Output Dense + Softmax
      → Compile → Train → Evaluate → Save
```

---

💡 Tip:

- ছোট dataset → small CNN (2–3 Conv)
    
- বড় dataset → deeper CNN or Pretrained model
    
- Dropout → overfitting কমানোর জন্য
    

---


 এবার দেখাই **Custom Dataset** (নিজের ছবি) ব্যবহার করে **Custom CNN** train করার পুরো pipeline, step by step। আমি TensorFlow/Keras দিয়ে দেখাচ্ছি।

---

# ✅ 1️⃣ Custom Dataset Folder Structure

CNN খুব সহজে **folder names → labels** ধরে নেয়। ধরো dataset আছে cats vs dogs:

```
dataset/
 ├── train/
 │    ├── cat/
 │    └── dog/
 ├── val/
 │    ├── cat/
 │    └── dog/
 └── test/
      ├── cat/
      └── dog/
```

- প্রতিটি folder-এ ছবি থাকবে
    
- Folder নামগুলোই label হবে
    

---

# 2️⃣ Import Libraries

```python
import tensorflow as tf
from tensorflow.keras import layers, models
import matplotlib.pyplot as plt
import numpy as np
```

---

# 3️⃣ Load Dataset using `image_dataset_from_directory`

```python
img_size = (128, 128)
batch_size = 32

train_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/train",
    image_size=img_size,
    batch_size=batch_size
)

val_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/val",
    image_size=img_size,
    batch_size=batch_size
)

test_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/test",
    image_size=img_size,
    batch_size=batch_size,
    shuffle=False
)

class_names = train_ds.class_names
print("Classes:", class_names)
```

---

# 4️⃣ Data Augmentation (Optional)

```python
data_augmentation = tf.keras.Sequential([
    layers.RandomFlip("horizontal"),
    layers.RandomRotation(0.1),
    layers.RandomZoom(0.1)
])
```

---

# 5️⃣ Normalization Layer

```python
normalization = layers.Rescaling(1./255)

train_ds = train_ds.map(lambda x, y: (normalization(x), y))
val_ds   = val_ds.map(lambda x, y: (normalization(x), y))
test_ds  = test_ds.map(lambda x, y: (normalization(x), y))
```

---

# 6️⃣ Build Custom CNN Model

### Example: 3 Conv + MaxPool + Dropout

```python
model = models.Sequential([
    layers.Input(shape=(128,128,3)),
    data_augmentation,

    layers.Conv2D(32, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Conv2D(64, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Conv2D(128, (3,3), activation='relu'),
    layers.MaxPooling2D(),

    layers.Flatten(),
    layers.Dense(128, activation='relu'),
    layers.Dropout(0.5),
    layers.Dense(len(class_names), activation='softmax')
])
```

---

# 7️⃣ Compile Model

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

---

# 8️⃣ Train Model

```python
history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=20
)
```

---

# 9️⃣ Evaluate on Test Set

```python
test_loss, test_acc = model.evaluate(test_ds)
print("Test Accuracy:", test_acc)
```

---

# 🔟 Confusion Matrix + Classification Report

```python
from sklearn.metrics import confusion_matrix, classification_report

y_true = np.concatenate([y for x,y in test_ds], axis=0)
y_pred = np.argmax(model.predict(test_ds), axis=1)

cm = confusion_matrix(y_true, y_pred)
print("Confusion Matrix:\n", cm)
print(classification_report(y_true, y_pred, target_names=class_names))
```

---

# 1️⃣1️⃣ Predict New Images

```python
import numpy as np
from tensorflow.keras.preprocessing import image

img = image.load_img("my_image.jpg", target_size=img_size)
img_array = image.img_to_array(img)
img_array = img_array / 255.0
img_array = np.expand_dims(img_array, axis=0)

pred = model.predict(img_array)
pred_class = class_names[np.argmax(pred)]
print("Prediction:", pred_class)
```

---

# ✅ Summary Pipeline for Custom Dataset

```
Custom Images → Folder structure → Load with image_dataset_from_directory
               → Resize → Normalize → Data Augmentation
               → Custom CNN (Conv + Pool + Dense + Dropout)
               → Compile → Train → Evaluate → Predict
```

---

💡 Tips for Custom Dataset:

1. Folder structure + labels ঠিক থাকলে খুব সহজ।
    
2. Data Augmentation অনেক কাজে লাগে, বিশেষ করে small dataset।
    
3. Batch size & learning rate dataset অনুযায়ী adjust করতে হবে।
    
4. যদি dataset খুব ছোট → overfitting হবে → Dropout বা smaller CNN use করতে হবে।
    

---

ঠিক আছে 😎 এবার দেখাবো **Custom Dataset + Pretrained CNN (Transfer Learning) ব্যবহার করে full pipeline**, যেটা **accuracy দ্রুত বাড়াতে** সবচেয়ে বেশি ব্যবহার হয়। আমরা **TensorFlow/Keras** ব্যবহার করবো।

---

# ✅ 1️⃣ Folder Structure

ধরি dataset: cats vs dogs

```
dataset/
 ├── train/
 │    ├── cat/
 │    └── dog/
 ├── val/
 │    ├── cat/
 │    └── dog/
 └── test/
      ├── cat/
      └── dog/
```

- Folder নাম = label
    
- সব ছবি jpg/png
    

---

# 2️⃣ Import Libraries

```python
import tensorflow as tf
from tensorflow.keras import layers, models
import numpy as np
import matplotlib.pyplot as plt
from sklearn.metrics import confusion_matrix, classification_report
import seaborn as sns
```

---

# 3️⃣ Load Dataset

```python
img_size = (224, 224)  # Pretrained models usually need 224x224
batch_size = 32

train_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/train",
    image_size=img_size,
    batch_size=batch_size
)
val_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/val",
    image_size=img_size,
    batch_size=batch_size
)
test_ds = tf.keras.utils.image_dataset_from_directory(
    "dataset/test",
    image_size=img_size,
    batch_size=batch_size,
    shuffle=False
)

class_names = train_ds.class_names
print("Classes:", class_names)
```

---

# 4️⃣ Data Augmentation

```python
data_augmentation = tf.keras.Sequential([
    layers.RandomFlip("horizontal"),
    layers.RandomRotation(0.1),
    layers.RandomZoom(0.1),
    layers.RandomContrast(0.1)
])
```

---

# 5️⃣ Normalization Layer

```python
normalization = layers.Rescaling(1./255)

train_ds = train_ds.map(lambda x, y: (normalization(x), y))
val_ds   = val_ds.map(lambda x, y: (normalization(x), y))
test_ds  = test_ds.map(lambda x, y: (normalization(x), y))
```

---

# 6️⃣ Load Pretrained CNN (MobileNetV2)

```python
base_model = tf.keras.applications.MobileNetV2(
    input_shape=(224,224,3),
    include_top=False,
    weights="imagenet"
)
base_model.trainable = False  # Freeze base model
```

---

# 7️⃣ Build Full Model

```python
inputs = layers.Input(shape=(224,224,3))
x = data_augmentation(inputs)
x = base_model(x, training=False)  # feature extraction
x = layers.GlobalAveragePooling2D()(x)
x = layers.Dense(128, activation='relu')(x)
x = layers.Dropout(0.5)(x)
outputs = layers.Dense(len(class_names), activation='softmax')(x)

model = tf.keras.Model(inputs, outputs)
```

---

# 8️⃣ Compile Model

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=1e-4),
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
```

---

# 9️⃣ Train Model (Feature Extraction)

```python
history = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=10
)
```

---

# 🔟 Optional: Fine-Tuning (Increase Accuracy)

```python
base_model.trainable = True
for layer in base_model.layers[:-30]:  # Freeze first layers
    layer.trainable = False

model.compile(
    optimizer=tf.keras.optimizers.Adam(1e-5),  # lower learning rate
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)

history_finetune = model.fit(
    train_ds,
    validation_data=val_ds,
    epochs=5
)
```

---

# 1️⃣1️⃣ Evaluate on Test Set

```python
test_loss, test_acc = model.evaluate(test_ds)
print("Test Accuracy:", test_acc)
```

---

# 1️⃣2️⃣ Confusion Matrix + Classification Report

```python
y_true = np.concatenate([y for x,y in test_ds], axis=0)
y_pred = np.argmax(model.predict(test_ds), axis=1)

cm = confusion_matrix(y_true, y_pred)
plt.figure(figsize=(6,5))
sns.heatmap(cm, annot=True, fmt="d", xticklabels=class_names, yticklabels=class_names)
plt.xlabel("Predicted")
plt.ylabel("Actual")
plt.title("Confusion Matrix")
plt.show()

print(classification_report(y_true, y_pred, target_names=class_names))
```

---

# 1️⃣3️⃣ Predict New Images

```python
from tensorflow.keras.preprocessing import image
img = image.load_img("my_image.jpg", target_size=img_size)
img_array = image.img_to_array(img)/255.0
img_array = np.expand_dims(img_array, axis=0)

pred = model.predict(img_array)
pred_class = class_names[np.argmax(pred)]
print("Prediction:", pred_class)
```

---

# ✅ Full Pipeline Summary

```
Custom Images → Resize → Normalize → Data Augmentation
      → Pretrained CNN (MobileNetV2) feature extraction
      → GlobalAveragePooling → Dense → Dropout → Softmax
      → Compile → Train → Fine-tune
      → Evaluate → Confusion Matrix + Precision/Recall
      → Predict new images
```

---

💡 **Tips for Custom Dataset:**

1. Dataset ছোট হলে → Data Augmentation + Dropout খুব জরুরি
    
2. Pretrained CNN (MobileNet, ResNet, EfficientNet) ব্যবহার করলে **accuracy অনেক দ্রুত বাড়ে**
    
3. Fine-tuning করলে model আরও adapt হয় আপনার custom classes এর জন্য
    

---

